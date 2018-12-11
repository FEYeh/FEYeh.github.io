title: 前端面试题系列1-JS基础
categories:
  - 面试题
  - 前端
date: 2018-09-13 17:26:00
tags: 前端 面试题
---

不定时更新:-D


# 如何定义一个类？
参考答案：

主要有构造函数原型和对象创建两种方法。

原型法是通用老方法，对象创建是ES5推荐使用的方法。

目前来看，原型法更普遍。

代码：

```js
// 构造函数法
function Person(){
  this.name = 'John';
}
​
Person.prototype.sayName = function(){
  console.log(this.name);
}

var person = new Person();
person.sayName();
```

# js类继承有哪些方法？
参考答案：

原型链法、属性复制法和构造器应用法。另外，由于每个对象可以是一个类，这些方法也可以用于对象类的继承。

代码：

```js
// 原型链法
function Animal() {
  this.name = 'animal';
}
Animal.prototype.sayName = function(){
  console.log(this.name);
};
​
function Person() {}
// 人继承自动物
Person.prototype = Animal.prototype;
// 更新构造函数为人
Person.prototype.constructor = 'Person';
```
```js
// 属性复制法
function Animal() {
  this.name = 'animal';
}
Animal.prototype.sayName = function() {
  console.log(this.name);
};
​
function Person() {}
​
// 复制动物的所有属性到人量边
for(prop in Animal.prototype) {
  Person.prototype[prop] = Animal.prototype[prop];
}
// 更新构造函数为人
Person.prototype.constructor = 'Person'; 
```
```js
// 构造器法
function Animal() {
  this.name = 'animal';
}
Animal.prototype.sayName = function() {
  console.log(this.name);
};
​
function Person() {
  Animal.call(this); // apply, call, bind方法都可以。区别见6
}
```

# js如何实现类多重继承？
参考答案：

就是类继承方法中的属性复制法来实现。因为当所有父类的prototype属性被复制后，子类自然拥有类似行为和属性。

# 什么是js的作用域？
参考答案：

大多数语言使用的都是块作用域，以{}进行限定，js中不是。js中叫函数作用域，就是一个变量在全函数里有效。

比如有个变量p1在函数最后一行定义，第一行也有效，但是值是undefined。

代码：
```js
// 函数作用域
var globalVar = 'global var';
function test() {
  console.log(globalVar); // undefined, 因为globalVar在本函数内被重定义了，导致全局失效，这里使用函数内的变量值，可是此时还没定义
  var globalVar = 'overrided var'; //　globalVar在本函数内被重定义
  console.log(globalVar);　// overrided var
}
console.log(globalVar); // global var，使用全局变量
```

# js的this指的是什么？
参考答案：

this指的是对象本身，而不是构造函数。

代码：

```js
function Person() {}
Person.prototype.sayName() { console.log(this.name); }
​
var person = new Person();
person.name = 'John';
person.sayName(); // John
```

# apply，call和bind的区别
参考答案：

三者都可以把一个函数应用到其他对象上，注意不是自身对象。

apply、call是直接执行函数调用，bind是绑定，执行后需要再次调用。

apply和call的区别是apply接受数组作为参数，而call是接受逗号分隔的无限多个参数列表。

代码：
```js

function Person() {}
Person.prototype.sayName() { console.log(this.name); }
​
var obj = {name: 'John'}; // 注意这是一个普通对象，它不是Person的实例
// 1) apply
Person.prototype.sayName.apply(obj, [param1, param2, param3]);
​
// 2) call
Person.prototype.sayName.call(obj, param1, param2, param3);
​
// 3) bind
var newFunc = Person.prototype.sayName.bind(obj); 
newFunc([param1, param2, param3]); // bind需要先绑定，再执行 
newFunc(param1, param2, param3); // bind需要先绑定，再执行
```

# caller，callee和arguments的区别
参考答案：

caller，callee之间的关系就像是employer和employee之间的关系，就是调用与被调用的关系，二者返回的都是函数对象引用。

arguments是函数的所有参数列表，它是一个类数组的变量。

代码：

```js
function parent(param1, param2, param3) {
  child(param1, param2, param3);
}
​
function child() {
  console.log(arguments); // { '0': 'John1', '1': 'John2', '2': 'Joh3' }
  console.log(arguments.callee); // [Function: child]
  console.log(child.caller); // [Function: parent]
}
​
parent('John1', 'John2', 'John3');
```

# 什么是闭包，它的用处？
参考答案：

通俗的说，闭包就是作用域范围，因为js是函数作用域，所以函数就是闭包。

全局函数的作用域范围就是全局，所以无须讨论。

更多的应用其实是在内嵌函数，这就会涉及到内嵌作用域，或者叫作用域链。

说到内嵌，其实就是父子引用关系（父函数包含子函数，子函数因为函数作用域又引用父函数，所以叫闭包），这就会带来另外一个问题，什么时候引用结束？如果不结束，就会一直占用内存，引起内存泄漏。好吧，不用的时候就将引用设为空，死结就解开了。

# defineProperty, hasOwnProperty, propertyIsEnumerable
参考答案：

Object.defineProperty(obj, prop, descriptor)用来给对象定义属性，有value，writable，configurable，enumerable，set/get等。

hasOwnProerty用于检查某一属性是不是存在于对象本身，继承来的属性不算。

propertyIsEnumerable用来检测某一属性是否可遍历，也就是能不能用for..in循环来取到。

# js常用设计模式
参考答案：

单例，工厂，代理，装饰，观察者模式等

代码：

1) 单例：任意对象都是单例，无须特别处理，适用场景：如日志等
```js
var obj = { name: 'John', age: 30 };
```
2) 工厂：不同参数返回不同的实例，适用场景：根据不同参数产生不同实例，这些实例有一些共性的场景
```js
function Person() { this.name = 'I am a person'; }
function Animal() { this.name = 'I am an animal'; }
​
function Factory() {}
Factory.prototype.getInstance = function(className) {
  return eval('new ' + className + '()');
}
​
var factory = new Factory();
var obj1 = factory.getInstance('Person');
var obj2 = factory.getInstance('Animal');
console.log(obj1.name); // I am a person
console.log(obj2.name); // I am an animal
```
3) 代理：就是新建个类调用老类的接口，包一下
```js
function Person() { }
Person.prototype.sayName = function() { console.log('John'); }
Person.prototype.sayAge = function() { console.log(27); }
​
// 代理
function PersonProxy() { 
  this.person = new Person();
  var that = this;
  this.callMethod = function(functionName) {
    console.log('before proxy:', functionName);
    that.person[functionName]();
    console.log('after proxy:', functionName);
  }
}
​
var pp = new PersonProxy();
// 代理调用Person的方法sayName()
pp.callMethod('sayName'); 
// 代理调用Person的方法sayAge()
pp.callMethod('sayAge');
```
4) 观察者: 就是事件模式，比如按钮的onclick这样的应用
```js
// 发布者
function Publisher() {
  this.listeners = [];
}
Publisher.prototype = {
  'addListener': function(listener) {
    this.listeners.push(listener);
  },
​
  'removeListener': function(listener) {
    delete this.listeners[listener];
  },
​
  'notify': function(obj) {
    for(var i = 0; i < this.listeners.length; i++) {
      var listener = this.listeners[i];
      if (typeof listener !== 'undefined') {
        listener.process(obj);
      }
    }
  }
};
​
// 订阅者
function Subscriber() {}
Subscriber.prototype = {
  'process': function(obj) {
    console.log(obj);
  }
};
​
var publisher = new Publisher();
publisher.addListener(new Subscriber());
publisher.addListener(new Subscriber());
// 发布一个对象到所有订阅者
publisher.notify({name: 'John', ageo: 27});
// 发布一个字符串到所有订阅者
publisher.notify('2 subscribers will both perform process');
```
# 列举数组的常用方法（入参、返回值、使用方式）
参考答案：

push/pop, shift/unshift, join, slice/splice/concat, sort/reverse, map/reduce, forEach, filter

# 列举字符串的常用方法（入参、返回值、使用方式）
参考答案：

indexOf/lastIndexOf/charAt, split/match/test, slice/substring/substr, toLowerCase/toUpperCase

# ES6有哪些新特性
参考答案：

类的支持，模块化，箭头函数，let/const块作用域，字符串模板，解构，参数默认值/不定参数/拓展参数, for-of遍历, generator, Map/Set, Promise

# setTimeout六连击
```js
// 第一击
for (var i = 0; i < 5; i++) {
  console.log(i);
}
// 答案： 0 1 2 3 4

// 第二击
for (var i = 0; i < 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000 * i);
}
// 答案： 5 5 5 5 5

// 第三击
// 怎么修改输出0 1 2 3 4
// 闭包模式或者Es6的`let`
for (var i = 0; i < 5; i++) {
  (function(i) {
    setTimeout(function() {
      console.log(i);
    }, i * 1000);
  })(i);
}

// 第四击
for (var i = 0; i < 5; i++) {
  (function() {
    setTimeout(function() {
      console.log(i);
    }, i * 1000);
  })(i);
}
// 答案： 5 5 5 5 5

// 第五击
for (var i = 0; i < 5; i++) {
  setTimeout((function(i) {
    console.log(i);
  })(i), i * 1000);
}
// 答案： 0 1 2 3 4

// 第六击
// 考察运行机制
setTimeout(function() {
  console.log(1)
}, 0);
new Promise(function executor(resolve) {
  console.log(2);
  for( var i=0 ; i<10000 ; i++ ) {
    i == 9999 && resolve();
  }
  console.log(3);
}).then(function() {
  console.log(4);
});
console.log(5);
// 答案： 2 3 5 4 1
// 解答：setTimeout属于异步进程任务，会放到任务队列等待执行
// Promise里面是立即执行函数，因此先输出2和3，then则会在当前tick的最后执行，因此会先输出5，再接着输出4，最后输出1
```
​

