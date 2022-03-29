---
title: JavaScript-高级
date: 2022-03-29 12:47:23
tags: code
---

# JS高级

## this

面向对象语言中`this`表示当前对象的一个引用。

但在`JavaScript`中`this`不是固定不变的，它会随着执行环境的改变而改变。

### 在方法中，`this`表示该方法所属的对象

```javascript
var obj = {
	firstName: "Ma",
	lastName: "QiLin",
	getNameFn: function() {
		return this. firstName + this.lastName
		}
	};
```

* 在对象方法中，`this`指向调用它所在方法的对象。
* 在上面一个实例中，`this`表示`obj`对象。
* `fullName`方法所属的对象就是`obj`。


### 如果单独使用`this`表示全局对象

```javascript
var x = this;

```

* 单独使用`this`，则它指向全局`Global`对象。
* 在浏览器中，`window` 就是该全局对象为` [object Window]:`
* 严格模式下，如果单独使用，`this` 也是指向全局`Global`对象。



### 在函数中，`this`表示全局对象，严格模式下为`undefined`

```javascript
function fn() {
	return this;
};
```

* 在函数中，函数的所属者默认绑定到 `this` 上。
* 在浏览器中，`window` 就是该全局对象为 `[object Window]`:
* 严格模式下函数是没有绑定到 `this` 上，这时候 `this` 是 `undefined`。



### 在事件中，`this`表示接收事件的元素

```javascript
<button onclick="this.style.display='none'">
	点我后我就消失了
</button>
```

* 在 `HTML` 事件句柄中，`this` 指向了接收事件的 `HTML` 元素：


### 类似 `call()` 和 `apply()` 方法可以将 `this` 引用到任何对象（更改`this`指向）

```javascript
var person1 = {
	fullName: function() {
		return this.firstName + " " + this.lastName;
	}
}
var person2 = {
	firstName:"John",
	lastName: "Doe",
}
person1.fullName.call(person2);  // 返回 "John Doe"
```

* 在 `JavaScript` 中函数也是对象，对象则有方法，`apply` 和 `call` 就是函数对象的方法。这两个方法异常强大，他们允许切换函数执行的上下文环境`context`，即 `this` 绑定的对象。

* 在上面面实例中，当我们使用 `person2` 作为参数来调用 `person1.fullName` 方法时, `this` 将指向 `person2`, 即便它是 `person1` 的方法：

### 在构造函数中`this`表示实例

```javascript
function fn (name, age) {
	this.name = name;
	this.age = age;
};
	
const f1 = new fn('mql', 18);
console.log(f1); // { name: 'mql', age: 18 }
```


## 闭包

## 原型、原型链

JS在设计时并没有采用其他语言的`class`概念，而采用的时原型继承的设计模式。可以粗略理解问，原型 + 构造函数 + 原型链 形成的继承模式为 JAVA中的类`class`模式



## 构造函数

### 什么是构造函数

在 `JavaScript` 中，用 `new` 关键字来调用的函数，称为构造函数。

```javascript
function fn() {
	name: 'card',
};
		
const f1 = new fn(); // { name: 'card' };
```

### 为什么实用构造函数

比如：现有一个造车工厂，每个车都有一些配置参数，代码如下
```javascript
card1 = {
	color: "红色",
	name: '奔驰',
	price: '40w'
};
		
card2 = {
	color: '白色',
	name: '奔驰',
	price: '60w'
};
....

```

从数据中可以看出，每辆车有很多属性，有相同的，有独立不同的。如果汽车多了，我们就会写很多类似的代码。构造函数工厂模式就是解决这一难题。代码如下

```javascript
function card(color, price) {
	this.name = '奔驰';
	this.color = color;
	this.price = price;
};
		
const card1 = new card( '红色', 400000 );
// { color: '红色', name: '奔驰', price: '4000000' }
const card2 = new card('白色', 6000000);
```

### 构造函数执行过程及原理

* 当`card1`用`new`关键字调用`card`方法时，会为`card1`开辟一个新内存，且`card`中的`this`指向该内存即`card1`.代码如下

```javascript
const card1 = new card('白色', 6000000); 
// 开辟一个新的内存空间card1 并且card的this指向该空间
```

###  构造函数返回值

由于函数体内部的 `this` 指向新创建的内存空间，默认返回 `this` ，就相当于默认返回了该内存空间，也就是上图中的 `card1`。此时，`card1`的内存空间被变量 `card1` 所接受。也就是说 `card1` 这个变量，保存的内存地址就是 `card1`，同时被标记为 `card` 的实例。


### 缺点

实例在调用构造函数时会开辟一个新的内存空间，前面提到过公共属性，例如`name`属性。如此便在内存空间都会有name属性，这无疑是很浪费内存的。这种情况可以采用原型+原型链的方法共享属性。无需单独创建。代码如下

```javascript

function card(color, price) {
	this.color = color;
	this.price = pirce;
};
// 通过在原型上添加公共属性`name` 让实例继承
card. prototype.name = '奔驰';
const card1 = new card('红色', 400000) // { color:'红色', price: 40000, name: '奔驰' }		

```



## 数据类型 => 栈、堆

## 回调函数

## 异步

## 执行机制、事件循环、事件队列

### 单线程

JavaScript是单线程语言、