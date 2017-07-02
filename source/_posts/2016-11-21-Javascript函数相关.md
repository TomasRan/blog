title: Javascript函数相关
photos:
  - 'http://o6lqh5p0j.bkt.clouddn.com/functional-javascript-programming-1.png'
categories:
  - Javascript
tags:
  - 硬绑定
  - 绑定丢失
  - this指针
abbrlink: QvKCA14vYKd0ejUlJjdz8w
date: 2016-11-21 15:55:12
---
### 函数之重，重于泰山
在Javascript中函数是一等公民。地为之重，可见一斑。那么它应该是有一些过人之处：

#### 函数式编程不可或缺
Javascript是一门支持函数式编程的语言，当然这不是确立函数至尊地位的关键因素，毕竟支持函数式编程的语言不胜枚举。不过很明显，这种编程思想的核心是函数，举足轻重。

<!-- more -->

#### 面向对象编程的依赖
Javascript使用构造函数实现传统面向对象语言类的概念，构造函数与普通函数并没有任何区别，只是在命名上按照面向对象语言的习惯，统一使用大驼峰形式。

#### 函数声明优先级更高
变量提升时函数声明会覆盖同名的变量，函数声明的优先级高于变量，待遇优厚。比如下面这段代码：

```javascript
	var fn;
	function fn() {};
	var fn;
	console.log(typeof fn);
```

输出的是什么？答案是'function'，函数声明优先于变量声明。


#### 语言采用的是函数作用域
Javascript使用的是函数作用域，至少在ES6出现之前（ES6开始支持块级作用域），作用域的生成以函数为单位。

#### 函数亦可赋值，传参
函数也可以作为参数传递，可以作为返回值返回。正是它一等公民的身份写照！在Javascript中这几乎是随处可见，例如：

```javascript
	function fn() {
		return function() { console.log('I\'m the function inside!') }
	}
```

函数在Javascript国土一手遮天，侵入者是不是应该先跟它打个招呼呢？

### 函数调用
怎样去执行一个函数，在Javascript中大致有四种方式进函数调用。

1. 默认函数调用形式。
2. 对象方法调用形式。
3. 构造器调用形式。
4. bind，call，apply调用。

在此不做详述。

### this关键字
函数中一个非常重要的概念就是this关键字，因为它的多变性，迷惑了一代又一代青年才俊。我们在一个函数中使用this，这个this指向哪里完全取决于函数执行时的调用方式。

非严格模式下，默认调用方式指向全局对象，严格模式下指向undefined；对象方法调用形式指向对象本身；构造器调用形式指向实例化后的对象；bind、call、apply调用指向传递的上下文环境。优先级是：构造函数形式 > bind、call和apply > 方法调用 > 默认调用。例如：

```javascript
var Fn = function(name) { this.name = name; }
var obj = {};

Fn = Fn.bind(obj);
Fn('tomas');
console.log(obj.name); // ‘tomas’
var fn = new Fn('tomasran')
console.log(obj.name); // 'tomas'
console.log(fn.name); // 'tomasran'
```

在上面的例子中，使用两种不同方式，执行被绑定了obj对象的函数Fn，第一次成功修改了obj.name值，因为Fn.bind(obj)使Fn执行时候的this指针绑定到了obj上；第二次采用构造函数调用，而结果obj.name的值并没有修改，这说明构造函数执行时内部的this指针并不是绑定到obj。结论不言而喻，在this指针的绑定上，构造函数的优先级大于bind、call、apply此类硬绑定的形式。

无意中说漏了一个词：硬绑定。为此，不得不多增加一点篇幅解释一下。

### 硬绑定
有一种常见的现象叫做绑定丢失。这是一个什么概念？举例来说，当我们有如下这段代码：

```javascript
var obj = {
	name: 'tomas',
	fn: function() {console.log(this.name);}
}
var foo = obj.fn;
foo(); //  输出 'undefined'
```

如果我们直接调用obj.fn()，显然这是方法调用模式，this指向obj对象，输出为 'tomas'；但是现在我们并没有这样做，而是先将obj.fn赋给了一个变量foo，然后执行__foo()__，之后，便惊奇地发现输出值并非我们所期望的。这是因为此时foo直接指向了obj.fn这个函数的内存地址，此时的调用形式是默认调用，这就是所谓的绑定丢失。如何解决？答案就是采用硬绑定：

```javascript
var foo = function() { return obj.fn.apply(obj, arguments)};
```

这样，调用 __foo()__ 就会执行绑定了obj对象的fn函数。ES5提供的bind方法就是为此需求而诞生的。

### 小结
关于函数，稍微絮叨了一番，累了，歇会儿。
