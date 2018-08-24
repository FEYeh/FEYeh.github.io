title: If...Else, or not
categories:
  - 前端
date: 2018-07-28 14:07:00
tags: 前端

---

# 前言
或许编程中最最经典的特性就是条件语句了。但当我开始回避它，我发现我自己写出来的代码更加合理且整洁。

回避条件语句的办法就是降低圈复杂度！（圈复杂度就不赘述了，大家看参考文献即可）

我们在React项目中，遇到特别多的If...Else语句。

而自从引入了Eslint圈复杂度检测，确实重构了特别多的If...Else。

重构后代码的可读性更好了，也更加合理。

因此也对此十分热衷，我想圈复杂度过高说明你的代码并不健康，是时候对它进行体检和重构了。

# 实战经验
当我在Code Review时看到很多条件语句，这时应该怎么做呢？我是这样考虑的：

这个功能实际上是在做不同的事情，而应该分成不同的功能吗？

是否确实有必要在这个功能中检查此条件，还是应该由其他地方负责呢？

可以用更易读的方式完成吗？有不同的模式可以替换条件，我最喜欢的模式之一是对象映射模式。

如果我们必须使用条件。我会删除Else，只保留If和默认情况。

现在，让我们一起来研究下一些处理不同类型条件语句的办法吧！

## 移除Else
这是一个相当简单的办法，但很实用：

```js
if (red) {
  return true;
} else if (blue) {
  return true;
} else {
  return false;
}
```
重构成这样：

```js
if (red || blue) {
 return true;
}
return false;
```
我喜欢第二种方式，原因有二：

有一个default语句，如果if语句不被满足，则可以很清楚的知道返回结果

功能一样，但代码少，可读性强

## 组合
如果你理解你的功能确实是做着不同的事情，那么可以使用一个很棒的模式——组合。

你需要将这个功能分成更小的、更细致的功能，然后将他们组合在一起。

这样的话，你可以自己创建一组可在应用的不同地方去使用的通用功能。

光说不练嘴把戏，这就来个栗子🌰：假如我们有个需求，要获取年龄超过30且怀孕着的女员工

我们的代码会长这样：

代码块
JavaScript
import { flow } from 'lodash';
const femaleEmployeesOverThirtyAndPregnant = flow(
  getFemales,
  getEmployeesOverThirty,
  getEmployeesPregnant,
)(employees);
我们可以很容易看出，上述的每个方法都是可以在不同地方去复用的。

## 对象映射
这是我最喜欢的模式。

它确实可以在很多不同情况下使用，不管前端编程还是后端编程。

最大的好处当然是它够简单，可读性强。

当我使用它时，我感觉我不是在写代码而更像是在写说明文档。

上菜：2.1的代码换了个新衣裳👗

```js
const colors = {
  red: true,
  blue: true,
  default: false,
 };
const colorMapper = color => colors[color] || colors.default;
const color = colorMapper(item.color);
```
它是这样工作的：

* 一个具体说明结果的对象
* 一个映射函数

有一个default结果是十分好的。因为如果我们没传参数或参数为空，这个方法仍然可以工作。

比如我们这样使用：colorMapper(‘green’)，我们将得到一个默认值为false的结果。但后面我们可以在之后添加新的数据进去，十分方便。

我们也可使用switch语句来得到同样的结果，但这样并不能降低圈复杂度。相比switch语句，对象映射模式更加纯净而优雅。

## 对象映射和React
在React中，这个模式真的很棒。

又来一颗例子🌰：假设我们想要将一个数组渲染出不同的组件。我们的数据格式如下：

```js
const items = [{
 type: ‘hero’,
 content: : {…},
}, {
 type: 'text',
 content: : {…},
}, {
 type: 'image_and_text',
 content: : {…},
}, {
 type: 'text',
 content: : {…},
}, {
 type: 'call_to_action',
 content: : {…},
}];
```
数组中每个对象都有type和content属性。

我们写一个映射函数，每一个key对应上述对象中的type，值为一个特定的组件。这个组件，只接受一个属性为content。如下：

```js
const components = {
 hero: HeroComponent,
 text: TextComponent,
 image_and_text: ImageAndTextComponent,
 call_to_action: CallToActionComponent,
 default: null,
};
const componentMapper = type => 
components[type] || components.default;
```
然后我们就可以在React应用中这样用了：

```js
import react from ‘react’;
const RenderItems = props => {
 
 const componentList = props.items((item, index) => {
   const Component = componentMapper(item.type);
   return <Component content={item.content} />
 };
 return (
  <div>
   {componentList}
  </div>
 )
};
```
这里的一个好处是，如果我们的内容来自外部源，并且有人添加了新模块。它将只渲染出null，并且什么都不会中断。我们稍后可以在我们的映射对象中添加一个新组件。

# 后记
可能有更多不同的模式和方法可用于对抗代码中的Ifs和Elses。

但这只是我发现最有用的几种方法。

如果你发现新的，还请不吝赐教！！！

# 参考文献

[become-a-functional-javascript-hero](https://medium.com/front-end-hacking/become-a-functional-javascript-hero-945e72c15bff)

[lodash/flow](https://lodash.com/docs/4.17.10#flow)
