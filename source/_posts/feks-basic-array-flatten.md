title: 理解Array.prototype.reduce()
categories:
  - 前端
date: 2018-05-09 18:11:00
tags: 前端
---

自己对js数组的reduce方法和递归还不是很透彻，因此写下此文加深理解。
I hope you find my examples helpful.

*给定一个数组*

```js
var arr = [1, [2], [3, [[4]]]]
```

*想要的输出结果*

```js
var flat = [1, 2, 3, 4]
```

# 使用循环和条件语句

如果我们知道嵌套的最大层数（本例是4），我们就可以使用循环遍历加上条件判断的方法来实现...

```js
function flatten() {
  var flat = [];
  for (var i=0; i<arr.length; i++) {
    if (Array.isArray(arr[i])) {
      for (var ii=0; ii<arr[i].length; ii++) {
        if (Array.isArray(arr[i][ii])) {
          for (var iii=0; iii<arr[i][ii].length; iii++) {
            for (var iiii=0; iiii<arr[i][ii][iii].length; iiii++) {
              if (Array.isArray(arr[i][ii][iii])) {
                flat.push(arr[i][ii][iii][iiii]);
              } else {
                flat.push(arr[i][ii][iii]);
              }
            }
          }
        } else {
          flat.push(arr[i][ii]);
        }
      }
    } else {
      flat.push(arr[i]);
    }
  }
}

// [1, 2, 3, 4]
```

这样是可以实现的，但代码读起来实在是...除此之外，有一个前提条件是你必须知道嵌套的深度，你能想象如何调试这么混乱的代码么？

# 使用reduce

```js
var flat = arr.reduce(function(acc, curr){
    return acc.concat(curr);
}, []);

// [ 1, 2, 3, [ [ 4 ] ] ]
```

看着是不是很简洁，不过看结果好像和我们想要的不太一样，**这里的嵌套数组没有被正确平铺**。

让我们先来理清reduce的作用进而解决这个问题。

**Array.prototype.reduce()**

> The reduce() method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.

这句MDN的解释看起来并不复杂，我们举个🌰更好的理解。

家里来了客人，你要把几个🍎洗干净放入一个盘子中招待客人。

上面这个例子中，几个🍎就是我们*arr*，盘子就是我们的*acc*，也就是*accumulator*，一开始盘子是空的数组，当你拿到当前的🍎，洗好并放入盘子中 (.concat())，当苹果都洗完后，你将装有洗干净🍎的盘子递给客人。

# 使用reduce递归处理嵌套数组

现在看来还不错，我们有了一盘洗干净的🍎。但还有嵌套数组需要解决。

回到我们的例子上。

让我们假设这些苹果是成堆的或包装在盒子里的，且每个盒子里还有可能有几个小盒子包装有🍎。

这里，我们需要列举可能的情况及处理方法：

1. 如果当前拿到的是一堆🍎🍎🍎，则从这堆🍎中取出一个
2. 如果当前拿到的是一个苹果，则洗干净放入盘中
3. 如果当前拿到的是盒子，打开盒子，如果盒子中是一个🍎，则返回步骤2
4. 如果盒子中包含另一个盒子，则打开盒子，返回步骤3
5. 当拿完之后，给客人一盘洗干净的🍎

```js
function flatten(arr) {
  if (Array.isArray(arr)) {
    return arr.reduce(function(acc, curr){
      return acc.concat(flatten(curr));
    }, []);
  } else {
    return arr;
  }
}

// [ 1, 2, 3, 4 ]
```
稍后我们继续来解释，先来看下 **递归**

**Recursion**

> An act of a function calling itself. Recursion is used to solve problems that contain smaller sub-problems. A recursive function can receive two inputs: a base case (ends recursion) or a recursive case (continues recursion).

简单说来，就是函数自己内部调用自己。

一个递归函数由两部分组成，一部分是用来结束递归的条件语句，另一部分是用来继续递归的部分。

再来看上面的代码，你会发现 **flatten** 出现了两次，第一次是声明这个方法，告诉你调用这个方法就可以实现我们想要的。第二次出现告诉你对于你拿到的应该怎么处理，是个🍎还是个盒子，交给它就行了。

现在，我们一行一行代码来剖析：
1. `function flatten(arr) {` 我们命名这一处理函数为flatten，并声明它具有一个参数arr
2. `if (Array.isArray(arr)) {` 判断传入的这个参数是否是数组（虽然一开始它一定是，[偷笑]:-D）
3. `return arr.reduce(function(acc, curr){` 如果是数组，我们将用reduce来处理
4. `return acc.concat(flatten(curr));` 递归处理嵌套函数，并用累加器将结果concat。
5. `}, []);` 告诉reduce初始的累加器为一个空数组。
6. `} else {` 如果不是数组
7. `return arr;` 不管arr是啥，直接返回
8. `}` 结束if-else语句
9. `}` 结束flatten函数

到这里就完工啦！我们成功的将24行好汉四层for循环嵌套的代码，升级成更简洁，只有9行代码的reduce递归方案。

**reduce** 和 **recursion** 一开始理解起来比较费劲，但确实是不错的工具，一旦你理解了它们，做起事来更加事半功倍。

Thanks for reading!