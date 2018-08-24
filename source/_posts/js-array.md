title: 数组常用方法总结
categories:
  - 前端
date: 2018-07-28 14:07:00
tags: 前端

---

# Array.length

## 作用

返回或设置一个数组中的元素个数

## 注意

设置 length 属性值会截断数组

# Array.from()

## 语法

```js
Array.from(arrayLike[, mapFn[, thisArg]])
```

## 作用

将伪数组或可迭代对象（如 arguments、map、set、string...）转换成数组对象

## 参数

`arrayLike`  
想要转换成数组的伪数组对象或可迭代对象。  
`mapFn (可选参数)`  
如果指定了该参数，新数组中的每个元素会执行该回调函数。  
`thisArg (可选参数)`  
可选参数，执行回调函数 mapFn 时 this 对象。

## 示例

```js
Array.from("foo");
// ["f", "o", "o"]

let s = new Set(["foo", window]);
Array.from(s);
// ["foo", window]

let m = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(m);
// [[1, 2], [2, 4], [4, 8]]

function f() {
  return Array.from(arguments);
}
f(1, 2, 3);
// [1, 2, 3]

Array.from([1, 2, 3], x => x + x);
// [2, 4, 6]

Array.from({ length: 5 }, (v, i) => i);
// [0, 1, 2, 3, 4]
```

```js
// 数组去重合并
function combine() {
  //没有去重复的新数组
  let arr = [].concat.apply([], arguments);
  return Array.from(new Set(arr));
}

var m = [1, 2, 2],
  n = [2, 3, 3];
console.log(combine(m, n));
// [1, 2, 3]
```

# Array.isArray()

## 语法

```js
Array.isArray(obj);
```

## 作用

用于确定传递的值是否是一个 Array

## 参数

obj，需要检测的值。

## 返回值

如果对象是 Array，则为 true; 否则为 false。

# Array.of()

## 作用

创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型

## 语法

```js
Array.of(element0[, element1[, ...[, elementN]]])
```

## 参数

elementN，任意个参数，将按顺序成为返回数组中的元素。

### 返回值

新的 Array 实例。

## 注意

Array.of() 和 Array 构造函数之间的区别在于处理整数参数：Array.of(7) 创建一个具有单个元素 7 的数组，而 Array(7) 创建一个长度为 7 的空数组

## 示例

```js
Array.of(7); // [7]
Array.of(1, 2, 3); // [1, 2, 3]
Array.of(undefined); // [undefined]

Array(7); // [ , , , , , , ]
Array(1, 2, 3); // [1, 2, 3]
```

# Array.concat()

## 作用

用于合并两个或多个数组

## 语法

```js
var new_array = old_array.concat(value1[, value2[, ...[, valueN]]])
```

## 参数

valueN，将数组和/或值连接成新数组。

## 返回值

新的 Array 实例。

## 示例

```js
// 连接三个数组
var num1 = [1, 2, 3],
  num2 = [4, 5, 6],
  num3 = [7, 8, 9];
var nums = num1.concat(num2, num3);
console.log(nums);
// results in [1, 2, 3, 4, 5, 6, 7, 8, 9]

// 合并嵌套数组
// 以下代码合并数组并保留引用：
var num1 = [[1]];
var num2 = [2, [3]];
var nums = num1.concat(num2);
console.log(nums);
// results in [[1], 2, [3]]

// modify the first element of num1
num1[0].push(4);

console.log(nums);
// results in [[1, 4], 2, [3]]
```

# Array.copyWithin()

## 作用

浅复制数组的一部分到同一数组中的另一个位置，并返回它，而不修改其大小。

## 语法

```js
arr.copyWithin(target[, start[, end]])
```

## 参数

target，0 为基底的索引，复制序列到该位置。如果是负数，target 将从末尾开始计算。  
如果 target 大于等于 arr.length，将会不发生拷贝。如果 target 在 start 之后，复制的序列将被修改以符合 arr.length。  
start，0 为基底的索引，开始复制元素的起始位置。如果是负数，start 将从末尾开始计算。  
如果 start 被忽略，copyWithin 将会从 0 开始复制。
end，0 为基底的索引，开始复制元素的结束位置。copyWithin 将会拷贝到该位置，但不包括 end 这个位置的元素。如果是负数， end 将从末尾开始计算。  
如果 end 被忽略，copyWithin 将会复制到 arr.length。

## 返回值

改变了的数组。

## 示例

```js
[1, 2, 3, 4, 5].copyWithin(-2);
// [1, 2, 3, 1, 2]

[1, 2, 3, 4, 5].copyWithin(0, 3);
// [4, 5, 3, 4, 5]

[1, 2, 3, 4, 5].copyWithin(0, 3, 4);
// [4, 2, 3, 4, 5]

[1, 2, 3, 4, 5].copyWithin(-2, -3, -1);
// [1, 2, 3, 3, 4]

[].copyWithin.call({ length: 5, 3: 1 }, 0, 3);
// {0: 1, 3: 1, length: 5}

// ES2015 Typed Arrays are subclasses of Array
var i32a = new Int32Array([1, 2, 3, 4, 5]);

i32a.copyWithin(0, 2);
// Int32Array [3, 4, 5, 4, 5]

// On platforms that are not yet ES2015 compliant:
[].copyWithin.call(new Int32Array([1, 2, 3, 4, 5]), 0, 3, 4);
// Int32Array [4, 2, 3, 4, 5]
```

# Array.entries()

## 作用

返回一个新的 Array Iterator 对象，该对象包含数组中每个索引的键/值对。

## 语法

```js
arr.entries();
```

## 返回值

一个新的 Array 迭代器对象。Array Iterator 是对象，它的原型（**proto**:Array Iterator）上有一个 next 方法，可用用于遍历迭代器取得原数组的[key,value]。

# Array.every()

测试数组的所有元素是否都通过了指定函数的测试。

## 语法

```js
arr.every(callback[, thisArg])
```

## 参数

`callback`  
用来测试每个元素的函数。  
`thisArg`  
执行 callback 时使用的 this 值。

# 示例

```js
function isBigEnough(element, index, array) {
  return element >= 10;
}
var passed = [12, 5, 8, 130, 44].every(isBigEnough);
// passed is false
passed = [12, 54, 18, 130, 44].every(isBigEnough);
// passed is true
```

# Array.fill()

## 作用

用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。

## 语法

arr.fill(value[, start[, end]])

## 参数

`value`  
用来填充数组元素的值。  
`start 可选`  
起始索引，默认值为 0。  
`end 可选`  
终止索引，默认值为 this.length。

## 返回值

修改后的数组。

## 示例

```js
[1, 2, 3].fill(4); // [4, 4, 4]
[1, 2, 3].fill(4, 1); // [1, 4, 4]
[1, 2, 3].fill(4, 1, 2); // [1, 4, 3]
[1, 2, 3].fill(4, 1, 1); // [1, 2, 3]
[1, 2, 3].fill(4, 3, 3); // [1, 2, 3]
[1, 2, 3].fill(4, -3, -2); // [4, 2, 3]
[1, 2, 3].fill(4, NaN, NaN); // [1, 2, 3]
[1, 2, 3].fill(4, 3, 5); // [1, 2, 3]
Array(3).fill(4); // [4, 4, 4]
[].fill.call({ length: 3 }, 4); // {0: 4, 1: 4, 2: 4, length: 3}

// Objects by reference.
var arr = Array(3).fill({}); // [{}, {}, {}];
arr[0].hi = "hi"; // [{ hi: "hi" }, { hi: "hi" }, { hi: "hi" }]
```

# Array.filter()

## 作用

创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。

## 语法

```js
var new_array = arr.filter(callback(element[, index[, array]])[, thisArg])
```

## 参数

`callback`  
用来测试数组的每个元素的函数。调用时使用参数 (element, index, array)。  
返回 true 表示保留该元素（通过测试），false 则不保留。它接受三个参数：  
`element`  
当前在数组中处理的元素  
`index（可选）`  
正在处理元素在数组中的索引  
`array（可选）`  
调用了 filter 筛选器的数组  
`thisArg（可选）`  
可选。执行 callback 时的用于 this 的值。

## 返回值

一个新的通过测试的元素的集合的数组，如果没有通过测试则返回空数组

# Array.find()

## 语法

```js
arr.find(callback[, thisArg])
```

## 参数

`callback`  
在数组每一项上执行的函数，接收 3 个参数：  
`element`  
当前遍历到的元素。  
`index`
当前遍历到的索引。  
`array`  
数组本身。  
`thisArg 可选`  
可选，指定 callback 的 this 参数。

## 返回值

当某个元素通过 callback 的测试时，返回数组中的一个值，否则返回 undefined。

## 示例

```js
var inventory = [
  { name: "apples", quantity: 2 },
  { name: "bananas", quantity: 0 },
  { name: "cherries", quantity: 5 }
];

function findCherries(fruit) {
  return fruit.name === "cherries";
}

console.log(inventory.find(findCherries)); // { name: 'cherries', quantity: 5 }
```

# Array.findIndex()

## 作用

返回数组中满足提供的测试函数的第一个元素的索引。否则返回-1。

## 语法

```js
arr.findIndex(callback[, thisArg])
```

## 参数

`callback`  
针对数组中的每个元素, 都会执行该回调函数, 执行时会自动传入下面三个参数:  
`element`  
当前元素。  
`index`  
当前元素的索引。  
`array`  
调用 findIndex 的数组。  
`thisArg`  
可选。执行 callback 时作为 this 对象的值.

## 示例

```js
var array1 = [5, 12, 8, 130, 44];

function findFirstLargeNumber(element) {
  return element > 13;
}

console.log(array1.findIndex(findFirstLargeNumber));
// expected output: 3
```

# Array.flat()

## 作用

会递归到指定深度将所有子数组连接，并返回一个新数组。（存在兼容性）

## 语法

```js
var newArray = arr.flat(depth);
```

## 参数

`depth 可选`  
指定嵌套数组中的结构深度，默认值为 1。

## 返回值

一个将子数组连接的新数组.

## 示例

```js
// 扁平化嵌套数组
var arr1 = [1, 2, [3, 4]];
arr1.flat();
// [1, 2, 3, 4]

var arr2 = [1, 2, [3, 4, [5, 6]]];
arr2.flat();
// [1, 2, 3, 4, [5, 6]]

// 兼容性（自己实现）
var arr = ["a", ["b", "c", ["e", "f"]]];
function flat(arr) {
  var rtnArr = [];
  var flatter = function($val) {
    if (!Array.isArray($val)) {
      rtnArr.push($val);
    } else {
      for (var i in $val) flatter($val[i]);
    }
  };
  arr.forEach(flatter);
  return rtnArr;
}
var output = flat(arr);
console.log(output);
```

# Array.forEach()

## 作用
对数组的每个元素执行一次提供的函数。

## 语法
```js
array.forEach(callback(currentValue, index, array){
    //do something
}, thisArg)
```

## 参数
`callback`  
为数组中每个元素执行的函数，该函数接收三个参数：  
`currentValue(当前值)`  
数组中正在处理的当前元素。  
`index(索引)`  
数组中正在处理的当前元素的索引。  
`array`  
forEach()方法正在操作的数组。  
`thisArg可选`  
可选参数。当执行回调 函数时用作this的值(参考对象)。

## 返回值
undefined.

# Array.includes()

## 作用
用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回false。

## 语法
```js
arr.includes(searchElement)
arr.includes(searchElement, fromIndex)
```

## 参数
`searchElement`  
需要查找的元素值  。
`fromIndex 可选`  
从该索引处开始查找 searchElement。如果为负值，则按升序从 array.length + fromIndex 的索引开始搜索。默认为 0。

## 返回值
一个 Boolean。

## 示例
```js
[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false

(function() {
  console.log([].includes.call(arguments, 'a')); // true
  console.log([].includes.call(arguments, 'd')); // false
})('a','b','c');
```

# Array.indexOf()

## 作用
返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。

## 语法
```js
arr.indexOf(searchElement)
arr.indexOf(searchElement[, fromIndex = 0])
```

## 参数
`searchElement`  
要查找的元素值。  
`fromIndex 可选`  
开始查找的位置。

## 返回值
首个被找到的元素在数组中的索引位置; 若没有找到则返回 -1。

## 示例
```js
var array = [2, 5, 9];
array.indexOf(2);     // 0
array.indexOf(7);     // -1
```

# Array.join()

## 作用
将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。

## 语法
```js
str = arr.join()
// 默认为 ","

str = arr.join("")
// 分隔符 === 空字符串 ""

str = arr.join(separator)
// 分隔符
```

## 参数
`separator`
指定一个字符串来分隔数组的每个元素。

## 返回值
一个所有数组元素连接的字符串。如果 arr.length 为0，则返回空字符串

# Array.keys()

## 作用
返回一个新的Array迭代器，它包含数组中每个索引的键。

# Array.map()

## 作用
创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

## 语法
```js
let new_array = arr.map(function callback(currentValue, index, array) { 
    // Return element for new_array 
}[, thisArg])
```

## 参数
`callback`  
生成新数组元素的函数，使用三个参数：  
`currentValue`  
callback 的第一个参数，数组中正在处理的当前元素。  
`index`  
callback 的第二个参数，数组中正在处理的当前元素的索引。  
`array`  
callback 的第三个参数，map 方法被调用的数组。  
`thisArg`  
可选的。执行 callback 函数时 使用的this 值。  

## 返回值
一个新数组，每个元素都是回调函数的结果。

## 示例
```js
["1", "2", "3"].map(parseInt);
// [1, NaN, NaN]
['1', '2', '3'].map(Number);
// [1, 2, 3]

var str = '12345';
Array.prototype.map.call(str, function(x) {
  return x;
}).reverse().join(''); 
// 输出: '54321'
```

# Array.pop()

## 作用
从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。

## 语法
```js
arr.pop()
```

## 返回值
从数组中删除的元素(当数组为空时返回undefined)。

# Array.push()

## 作用
将一个或多个元素添加到数组的末尾，并返回新数组的长度。

## 语法
```js
arr.push(element1, ..., elementN)
```

## 参数
`elementN`
被添加到数组末尾的元素。

## 返回值
当调用该方法时，新的 length 属性值将被返回。

## 示例
```js
var sports = ["soccer", "baseball"];
var total = sports.push("football", "swimming");
console.log(sports); 
// ["soccer", "baseball", "football", "swimming"]
console.log(total);  
// 4

var vegetables = ['parsnip', 'potato'];
var moreVegs = ['celery', 'beetroot'];
// 将第二个数组融合进第一个数组
// 相当于 vegetables.push('celery', 'beetroot');
Array.prototype.push.apply(vegetables, moreVegs);
console.log(vegetables); 
// ['parsnip', 'potato', 'celery', 'beetroot']
```

# Array.reduce()

## 作用
对累加器和数组中的每个元素（从左到右）应用一个函数，将其减少为单个值。

## 语法
```js
arr.reduce(callback[, initialValue])
```

## 参数
`callback`  
执行数组中每个值的函数，包含四个参数：  
`accumulator`  
累加器累加回调的返回值; 它是上一次调用回调时返回的累积值，或initialValue（如下所示）。

`currentValue`  
数组中正在处理的元素。  
`currentIndex可选`  
数组中正在处理的当前元素的索引。 如果提供了initialValue，则索引号为0，否则为索引为1。  
`array可选`  
调用reduce的数组  
`initialValue可选`  
用作第一个调用 callback的第一个参数的值。 如果没有提供初始值，则将使用数组中的第一个元素。 在没有初始值的空数组上调用 reduce 将报错。

## 返回值
函数累计处理的结果

## 示例
```js
var names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];

var countedNames = names.reduce(function (allNames, name) { 
  if (name in allNames) {
    allNames[name]++;
  }
  else {
    allNames[name] = 1;
  }
  return allNames;
}, {});
// countedNames is:
// { 'Alice': 2, 'Bob': 1, 'Tiff': 1, 'Bruce': 1 }

// 数组去重
let arr = [1,2,1,2,3,5,4,5,3,4,4,4,4];
let result = arr.sort().reduce((init, current)=>{
    if(init.length===0 || init[init.length-1]!==current){
        init.push(current);
    }
    return init;
}, []);
console.log(result); //[1,2,3,4,5]
```

# Array.reverse()

## 作用
将数组中元素的位置颠倒。

# Array.shift()

## 作用
从数组中删除第一个元素，并返回该元素的值。此方法更改数组的
长度。

## 返回值
从数组中删除的元素; 如果数组为空则返回undefined 。

## 示例
```js
let myFish = ['angel', 'clown', 'mandarin', 'surgeon'];

console.log('调用 shift 之前: ' + myFish);
// "调用 shift 之前: angel,clown,mandarin,surgeon"

var shifted = myFish.shift(); 

console.log('调用 shift 之后: ' + myFish); 
// "调用 shift 之后: clown,mandarin,surgeon" 

console.log('被删除的元素: ' + shifted); 
// "被删除的元素: angel"
```

# Array.slice()

## 作用
返回一个从开始到结束（不包括结束）选择的数组的一部分浅拷贝到一个新数组对象。且原始数组不会被修改。

## 语法
```js
arr.slice();
// [0, end]

arr.slice(begin);
// [begin, end]

arr.slice(begin, end);
// [begin, end)
```

## 参数
`begin 可选`  
从该索引处开始提取原数组中的元素（从0开始）。
如果该参数为负数，则表示从原数组中的倒数第几个元素开始提取，slice(-2)表示提取原数组中的倒数第二个元素到最后一个元素（包含最后一个元素）。  
如果省略 begin，则 slice 从索引 0 开始。  
`end可选`  
在该索引处结束提取原数组元素（从0开始）。slice会提取原数组中索引从 begin 到 end 的所有元素（包含begin，但不包含end）。
slice(1,4) 提取原数组中的第二个元素开始直到第四个元素的所有元素 （索引为 1, 2, 3的元素）。  
如果该参数为负数， 则它表示在原数组中的倒数第几个元素结束抽取。 slice(-2,-1)表示抽取了原数组中的倒数第二个元素到最后一个元素（不包含最后一个元素，也就是只有倒数第二个元素）。  
如果 end 被省略，则slice 会一直提取到原数组末尾。  
如果 end 大于数组长度，slice 也会一直提取到原数组末尾。

## 返回值
一个含有提取元素的新数组

## 示例
```js
var animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];
console.log(animals.slice(2));
// expected output: Array ["camel", "duck", "elephant"]
```

# Array.some()

## 作用
测试数组中的某些元素是否通过由提供的函数实现的测试。

## 语法
```js
arr.some(callback[, thisArg])
```

## 参数
`callback`  
用来测试每个元素的函数，接受三个参数：  
`currentValue`  
数组中正在处理的元素。  
`index 可选`  
数组中正在处理的元素的索引值。  
`array可选`  
some()被调用的数组。  
`thisArg可选`  
执行 callback 时使用的 this 值。

## 返回值
如果回调函数返回任何数组元素的truthy值，则返回true；否则为false。

## 示例
```js
function isBiggerThan10(element, index, array) {
  return element > 10;
}
[2, 5, 8, 1, 4].some(isBiggerThan10);  // false
[12, 5, 8, 1, 4].some(isBiggerThan10); // true
```

# Array.sort()

## 作用
对数组的元素进行排序，并返回数组。

## 语法
```js
arr.sort() 

arr.sort(compareFunction)
```

## 参数
`compareFunction`  
可选。用来指定按某种顺序进行排列的函数。如果省略，元素按照转换为的字符串的各个字符的Unicode位点进行排序。

## 返回值
返回排序后的数组。原数组已经被排序后的数组代替。

## 示例
```js
var numbers = [4, 2, 5, 1, 3]; 
numbers.sort((a, b) => a - b); 
console.log(numbers);
// [1, 2, 3, 4, 5]
```

# Array.splice()

## 作用
通过删除现有元素和/或添加新元素来更改一个数组的内容。

## 语法
```js
array.splice(start[, deleteCount[, item1[, item2[, ...]]]])
```

## 参数
`start​`  
指定修改的开始位置（从0计数）。如果超出了数组的长度，则从数组末尾开始添加内容；如果是负值，则表示从数组末位开始的第几位（从-1计数）；若只使用start参数而不使用deleteCount、item，如：array.splice(start) ，表示删除[start，end]的元素。  
`deleteCount 可选`  
整数，表示要移除的数组元素的个数。如果 deleteCount 是 0，则不移除元素。这种情况下，至少应添加一个新元素。如果 deleteCount 大于start 之后的元素的总数，则从 start 后面的元素都将被删除（含第 start 位）。  
如果deleteCount被省略，则其相当于(arr.length - start)。  
`item1, item2, ... 可选`  
要添加进数组的元素,从start 位置开始。如果不指定，则 splice() 将只删除数组元素。

## 返回值
由被删除的元素组成的一个数组。如果只删除了一个元素，则返回只包含一个元素的数组。如果没有删除元素，则返回空数组。

## 示例
```js
var myFish = ["angel", "clown", "mandarin", "surgeon"]; 
//从第 2 位开始删除 0 个元素，插入 "drum" 
var removed = myFish.splice(2, 0, "drum"); 
//运算后的 myFish:["angel", "clown", "drum", "mandarin", "surgeon"] 
//被删除元素数组：[]，没有元素被删除
```

# Array.unshift()

## 作用
将一个或多个元素添加到数组的开头，并返回新数组的长度。

## 语法
```js
arr.unshift(element1, ..., elementN)
```

## 参数
`element1, ..., elementN`
要添加到数组开头的元素。

## 返回值
当一个对象调用该方法时，返回其 length 属性值。

## 示例
```js
var arr = [1, 2];

arr.unshift(0); //result of call is 3, the new array length
//arr is [0, 1, 2]

arr.unshift(-2, -1); // = 5
//arr is [-2, -1, 0, 1, 2]

arr.unshift( [-3] );
//arr is [[-3], -2, -1, 0, 1, 2]
```