title: Immutable.js中文文档
categories:
  - Translation
tags:
  - Immutable
  - 惰性评估
abbrlink: dsFzdQCcuQr1iO8ubvifYQ
date: 2017-04-05 23:29:58
---
原文链接：http://facebook.github.io/immutable-js/docs

不可变的数据（Immutable data）鼓励我们使用纯函数（数据输入，数据输出），适用于更简单的应用程序开发，并且启用了函数式编程技术，例如惰性评估。

为了将这些强大的函数概念引进Javascript，它提供了一套Javascript工程师熟悉的面向对象的API方法，就好像是Array，Map和Set的镜像方法一般。

<!--more-->

### 如何阅读这篇文档
为了更好地解释什么样的值是Immutable.js API所期望和生成的，本篇文档将会采用和Javascript类似的一种静态语言进行展示说明（例如 [Flow](https://flowtype.org/) 和 [TypeScript](http://www.typescriptlang.org/)）。你不需要使用那些类型检测工具就可以使用 Immutable.js ，只需要熟悉它们的语法就能帮助你更深入地理解这套API。

#### 一些例子以及如何去阅读它们。
所有的方法都会描述它们接受的数据类型和返回的数据类型。举例来说，一个接收两个数字作为参数并且返回一个数字的函数将会是这样的：

```
sum(first: number, second: number) : number
```

有时，方法可以接受不同的数据类型或者返回不同的数据类型，这是通过一个类型变量进行描述的，这个类型变量往往以典型的全部大写的形式给出。举例来说，一个返回值与接收参数的类型相同的函数看起来是这样的：

```
identity<T>(value: T) : T
```

类型变量用类进行定义并在方法中引用。举个例子，一个持有某个值得类可能看起来是这样的：

```
class Box<T>; {
        constructor(value: T)
            getValue(): T
}
```

为了操作Immutable数据，方法调用不再是我们以前所习惯的影响某个Collection本身，取而代之的是返回一个全新的相同类型的Collection。`this` 的类型同一个类的类型。举例来说，当你 `push` 一个值到List 类型数据中时，它会返回新的List：

```
class List<T> {
        push(value: T): this
}
```

Immutable.js 中的很多方法接受实现了Javascript Iterable协议的值，并且对于表示为字符串序列的东西可能会显示为 Iterable&lt;String&gt;。通常在Javascript中当期望使用一个可迭代的对象时，我们会使用数组（[]），然而所有的 Immutable.js 集合都是可以自身迭代的。

举个例子，为了在一个数据结构中获得深处的值，我们可能会使用getIn，它期望一个迭代的路径：

```
getIn(path: Iterable<string | number>): any
```

为了使用这个方法，我们可以传递一个数组： `data.getIn(['key', 2])`。

注意：所有的例子都是使用现代版本的Javascript ES2015 进行展示的。为了在老的浏览器中运行，它们需要被转化为 ES3。

举个例子：

```javascript
// ES2015
const mappedFoo = foo.map(x => x * x);
// ES3
var mappedFoo = foo.map(function (x) { return x * x; });
```

#### API
##### [fromJS()](#fromJS)
##### [is()](#is)
#####[hash()](#hash)
#####[isImmutable()](#isImmutable)
#####[isCollection](#isCollection)
#####[isKeyed](#isKeyed)
#####[isIndexed](#isIndexed)
#####[isAssociative](#isAssociative)
#####[isOrdered](#isOrdered)
#####[isValueObject](#isValueObject)
#####[valueObject](#isCollection)
#####[List](#List)
#####[Map](#Map)
#####[OrderedMap](#OrderedMap)
#####[Set](#Set)
#####[OrderedSet](#OrderedSet)
#####[Stack](#Stack)
#####[Range](#Range)
#####[Repeat](#Repeat)
#####[Record](#Record)
#####[Seq](#Seq)
#####[Collection](#Collection)
