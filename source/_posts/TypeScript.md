---
title: TypeScript
date: 2022-03-27 21:02:26
tags: code
---




# TypeScript
`TypeScript`是由微软推出并推动的一个静态类型检查的编译型编程语言，可以完美兼容ES6的`JavaScript`。目前大量前端库和应用使用`TS`开发，已然成为前端的主流开发语言。

## 优势
* 静态编译，减少`JS`动态语言特性带来了的非常多的隐藏bug
* 类型安全检查在编译阶段完成
* 大型项目的更好的进行管理和向后约定维护
* 为前端的彻底的静态安全的类型检查、类型继承、抽象设计体系铺好了基石
* 更加友好的智能提示和文档说明

## 	安装TypeScript
有两种主要的方式来获取`TypeScript`工具

* 通过`npm`安装

	`npm install -g typescript`
* 安装Visual Studio的`TypeScript`插件


## 编译代码


启动编译后，可以添加`-w`参数，让编译工具一直监听文件的变化，`ts`文件变化后自动编译。

	tsc -w tyDemon.ts
		or
	tsc --watch tyDemon.ts

编译多个`ts`文件

* 编译当前目录下的所有的`ts`文件

		tsc -w *.ts

*  编译当前目录及子目录的`ts`文件

		tsc -w ./**/*.ts
	

## 数据类型
### 布尔值
最基本的数据类型就是简单的`true`/`false`值，在`JavaScript`和`TypeScript`里叫做`boolean`

```javascript
	let isDone: boolean = false; 
	// 冒号后面是对当前变量类型的声明，isDone只能赋值布尔类型值，否则会编译失败。
```

### 数字
和`JavaScript`一样，`TypeScript`里的所有数字都是浮点数。 这些浮点数的类型是 `number`。 除了支持十进制和十六进制字面量，`TypeScript`还支持`ES5`中引入的二进制和八进制字面量

```javascript
let num1: number = 6;
let num2: number = 0xf00d;
let num3: number = 0b1010;
let num4: number = 0o744;
```

### 字符串
`JavaScript`程序的另一项基本操作是处理网页或服务器端的文本数据。 像其它语言里一样，我们使用 `string`表示文本数据类型。 和`JavaScript`一样，可以使用双引号`"`或单引号`'`表示字符串

```javascript
	let name: string = "bob";
	name = "smith";
```

### 数组
`TypeScript`像`JavaScript`一样可以操作数组元素。 有两种方式可以定义数组。 第一种，可以在元素类型后面接上 `[]`，表示由此类型元素组成的一个数组

```javascript
	let list: number[] = [1, 2, 3];
	let list: Array<number> = [1, 2, 3];
```
### 元祖
元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。 比如，你可以定义一对值分别为 `string`和`number`类型的元组。

```javascript
	let x: [string, number];
	x = ['hello', 10]; // OK
	x = [10, 'hello']; // Error
```

### any
有时候，会想要为那些在编程阶段还不清楚类型的变量指定一个类型。 这些值可能来自于动态的内容，比如来自用户输入或第三方代码库。 这种情况下，我们不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查。 那么我们可以使用 `any`类型来标记这些变量

```javascript
	let any1: any = 4;
	any1 = "maybe a string instead";
	any2 = false; 
```

### void
它表示没有任何类型。 当一个函数没有返回值时，会见到其返回值类型是`void`

```javascript
	function fn(): void {
    console.log("This is message");
	}
```

声明`void`变量只能给其赋值为`null`, `undefined`

```javascript
	let void1: void = undefined;
```

### Null 和 Undefined
`undefined`和`null`两者各自有自己的类型分别叫做`undefined`和`null`。 和 `void`相似。

```javascript
	let u: undefined = undefined;
	let n: null = null;
```

### Object
`object`表示非原始类型，也就是除`number`，`string`，`boolean`，`symbol`，`null`或`undefined`之外的类型。

```javascript
	declare function create(o: object | null): void;

	create({ prop: 0 }); // OK
	create(null); // OK

	create(42); // Error
	create("string"); // Error
	create(false); // Error
	create(undefined); // Error
```

### 枚举
`enum`类型是对`JavaScript`标准数据类型的一个补充。 像`C#`等其它语言一样，使用枚举类型可以为一组数值赋予名字。

```javascript
	enum Color {Red, Green, Blue}
	let c: Color = Color.Green;
```
默认情况下，从0开始为元素编号。 也可以手动的指定成员的数值。 例如，将上面的例子改成从 1开始编号：

```javascript
	enum Color {Red = 1, Green, Blue}
	let c: Color = Color.Green;
```
	
枚举类型提供的一个便利是你可以由枚举的值得到它的名字。 例如，我们知道数值为2，但是不确定它映射到`Color`里的哪个名字，可以查找相应的名字

```javascript
	enum Color {Red = 1, Green, Blue}
	let colorName: string = Color[2];

	console.log(colorName);  // 显示'Green'因为上面代码里它的值是2
```
	
	
### 函数
#### 函数的声明
 一个函数有输入和输出，要在 `TypeScript` 中对其进行约束，需要把输入和输出都考虑到，其中函数声明的类型定义较简单
 
 ```javascript
	function sum(x: number, y: number): number {
    return x + y;
	}
输入多余的（或者少于要求的）参数，是不被允许的

	function sum(x: number, y: number): number {
    return x + y;
	}
	sum(1, 2, 3);
	
	function sum(x: number, y: number): number {
    return x + y;
	}
	sum(1);
```

#### 函数表达式
如果要现在写一个对函数表达式的定义，可能会写成这样

```javascript
	let mySum = function (x: number, y: number): number {
    return x + y;
	};
```
这是可以通过编译的，不过事实上，上面的代码只对等号右侧的匿名函数进行了类型定义，而等号左边的 `mySum`，是通过赋值操作进行类型推论而推断出来的。如果需要手动给 `mySum` 添加类型，则应该是这样：

```javascript
	let mySum: (x: number, y: number) => number = function (x: number, y: number): number {
    return x + y;
	};
```
注意不要混淆了 `TypeScript` 中的 `=>` 和 `ES6` 中的 `=>`。

在 `TypeScript` 的类型定义中，`=>` 用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型。

在 ES6 中，=> 叫做箭头函数，应用十分广泛
#### 用接口定义函数的形状
也可以使用接口的方式来定义一个函数需要符合的形状：

```javascript
	interface SearchFunc {
    (source: string, subString: string): boolean;
	}

	let mySearch: SearchFunc;
	mySearch = function(source: string, subString: string) {
    return source.search(subString) !== -1;
	}
```
#### 可选参数
输入多余的（或者少于要求的）参数，是不允许的。那么如何定义可选的参数呢？

与接口中的可选属性类似，我们用 `?` 表示可选的参数：

```javascript
	function buildName(firstName: string, lastName?: string) {
    if (lastName) {
        return firstName + ' ' + lastName;
    } else {
        return firstName;
    }
	}
	let tomcat = buildName('Tom', 'Cat');
	let tom = buildName('Tom');
```
需要注意的是，可选参数必须接在必需参数后面。换句话说，可选参数后面不允许再出现必需参数了

```javascript
	function buildName(firstName?: string, lastName: string) {
    if (firstName) {
        return firstName + ' ' + lastName;
    } else {
        return lastName;
    }
	}
	let tomcat = buildName('Tom', 'Cat');
	let tom = buildName(undefined, 'Tom');
```
#### 参数默认值
在 ES6 中，允许给函数的参数添加默认值，`TypeScript` 会将添加了默认值的参数识别为可选参数：

```javascript
	function buildName(firstName: string, lastName: string = 'Cat') {
    return firstName + ' ' + lastName;
	}
	let tomcat = buildName('Tom', 'Cat');
	let tom = buildName('Tom');
此时就不受「可选参数必须接在必需参数后面」的限制了：

	function buildName(firstName: string = 'Tom', lastName: string) {
    return firstName + ' ' + lastName;
	}
	let tomcat = buildName('Tom', 'Cat');
	let cat = buildName(undefined, 'Cat');
```

#### 剩余参数
ES6 中，可以使用 `...rest` 的方式获取函数中的剩余参数（rest 参数）：

```javascript
	function push(array, ...items) {
    items.forEach(function(item) {
        array.push(item);
    });
	}

	let a = [];
	push(a, 1, 2, 3);
```

事实上，`items` 是一个数组。所以可以用数组的类型来定义它：

```javascript
	function push(array: any[], ...items: any[]) {
    items.forEach(function(item) {
        array.push(item);
    });
	}

	let a = [];
	push(a, 1, 2, 3);
```
注意，rest 参数只能是最后一个参数

#### 重载
重载允许一个函数接受不同数量或类型的参数时，作出不同的处理。

比如，需要实现一个函数 `reverse`，输入数字 `123` 的时候，输出反转的数字 `321`，输入字符串 `'hello'` 的时候，输出反转的字符串 `'olleh'`。

利用联合类型，可以这么实现：

```javascript
		function reverse(x: number | string): number | string {
    if (typeof x === 'number') {
        return Number(x.toString().split('').reverse().join(''));
    } else if (typeof x === 'string') {
        return x.split('').reverse().join('');
    }
	}
```
然而这样有一个缺点，就是不能够精确的表达，输入为数字的时候，输出也应该为数字，输入为字符串的时候，输出也应该为字符串。

这时，可以使用重载定义多个 `reverse` 的函数类型：

```javascript
		function reverse(x: number): number;
		function reverse(x: string): string;
		function reverse(x: number | string): number | string {
		    if (typeof x === 'number') {
       		 return Number(x.toString().split('').reverse().join(''));
		    } else if (typeof x === 'string') {
       		 return x.split('').reverse().join('');
		    }
		}
```
上例中，重复定义了多次函数 `reverse`，前几次都是函数定义，最后一次是函数实现。在编辑器的代码提示中，可以正确的看到前两个提示。

注意，`TypeScript` 会优先从最前面的函数定义开始匹配，所以多个函数定义如果有包含关系，需要优先把精确的定义写在前面。

	
## 对象的类型——接口
在 `TypeScript` 中，使用接口来定义对象的类型。

在面向对象语言中，接口是一个很重要的概念，它是对行为的抽象，而具体如何行动需要由类去实现。

`TypeScript` 中的接口是一个非常灵活的概念，除了可用于对类的一部分行为进行抽象以外，也常用于对「对象的形状」进行描述。

### 简单的例子

```javascript
		interface Person {
	    name: string;
		age: number;
		}

		let tom: Person = {
		name: 'Tom',
		age: 25
		};
```	
定义了一个接口 Person，接着定义了一个变量 tom

它的类型是 Person。这样，我们就约束了 tom 的形状必须和接口 Person 一致

接口一般首字母大写

定义的变量比接口少了、多了一些一些属性是不允许的：

```javascript
	interface Person {
		name: string;
		age: number;
	}

	let tom: Person = {
	    name: 'Tom'
	};

	// index.ts(6,5): error TS2322: Type '{ name: string; }' is not assignable to type 'Person'.
	//   Property 'age' is missing in type '{ name: string; }'.
	
		interface Person {
	    name: string;
	    age: number;
		}

	let tom: Person = {
		name: 'Tom',
	   	age: 25,
		gender: 'male'
	};

	// index.ts(9,5): error TS2322: Type '{ name: string; age: number; gender: string; }' is 	not assignable to type 'Person'.
	//   Object literal may only specify known properties, and 'gender' does not exist in type 	'Person'.
```
### 可选属性

有时希望不要完全匹配一个形状，那么可以用可选属性

```javascript
		interface Person {
			name: string;
		   	age?: number;
		}

		let tom: Person = {
		    name: 'Tom'
		};
		
		nterface Person {
		    name: string;
		    age?: number;
		}

		let tom: Person = {
		    name: 'Tom',
		    age: 25
		};
```

这时仍然不允许添加未定义的属性

```javascript
	interface Person {
    	name: string;
	   	age?: number;
	}

	let tom: Person = {
    	name: 'Tom',
	   age: 25,
	   gender: 'male'
	};

	// examples/playground/index.ts(9,5): error TS2322: Type '{ name: string; age: number; 	gender: string; }' is not assignable to type 'Person'.
	//   Object literal may only specify known properties, and 'gender' does not exist in type 	'Person'.
```
### 任意属性
有时候希望一个接口允许有任意的属性，可以使用如下方式：

```javascript
	interface Person {
	   	name: string;
		age?: number;
	   [propName: string]: any;
	}

	let tom: Person = {
    	name: 'Tom',
	   gender: 'male'
	};
```

使用 `[propName: string]` 定义了任意属性取 `string` 类型的值。

需要注意的是，一旦定义了任意属性，那么确定属性和可选属性的类型都必须是它的类型的子集：

```javascript
	interface Person {
    name: string;
    age?: number;
    [propName: string]: string;
	}

	let tom: Person = {
    	name: 'Tom',
    	age: 25,
    	gender: 'male'
	};

	// index.ts(3,5): error TS2411: Property 'age' of type 'number' is not assignable to string 	index type 'string'.
	// index.ts(7,5): error TS2322: Type '{ [x: string]: string | number; name: string; age: 	number; gender: string; }' is not assignable to type 'Person'.
	//   Index signatures are incompatible.
	//     Type 'string | number' is not assignable to type 'string'.
	//       Type 'number' is not assignable to type 'string'.
```

上例中，任意属性的值允许是 `string`，但是可选属性 `age` 的值却是 `number`，`number` 不是 `string` 的子属性，所以报错了。

另外，在报错信息中可以看出，此时 `{ name: 'Tom', age: 25, gender: 'male' }` 的类型被推断成了 `{ [x: string]: string | number; name: string; age: number; gender: string; }`，这是联合类型和接口的结合。

### 只读属性
有时候希望对象中的一些字段只能在创建的时候被赋值，那么可以用 `readonly` 定义只读属性：

```javascript
	interface Person {
    	readonly id: number;
    	name: string;
    	age?: number;
    	[propName: string]: any;
	}

	let tom: Person = {
    	id: 89757,
    	name: 'Tom',
    	gender: 'male'
	};

	tom.id = 9527;

	// index.ts(14,5): error TS2540: Cannot assign to 'id' because it is a constant or a read-	only property
```
	
上例中，使用 `readonly` 定义的属性 `id` 初始化后，又被赋值了，所以报错了。

注意，只读的约束存在于第一次给对象赋值的时候，而不是第一次给只读属性赋值的时候：

```javascript
	interface Person {
    	readonly id: number;
    	name: string;
    	age?: number;
    	[propName: string]: any;
	}

	let tom: Person = {
    	name: 'Tom',
	   gender: 'male'
	};

	tom.id = 89757;

	// index.ts(8,5): error TS2322: Type '{ name: string; gender: string; }' is not assignable 	to type 'Person'.
	//   Property 'id' is missing in type '{ name: string; gender: string; }'.
	// index.ts(13,5): error TS2540: Cannot assign to 'id' because it is a constant or a read-	only property.
	
```
上例中，报错信息有两处，第一处是在对 `tom` 进行赋值的时候，没有给 `id` 赋值。

第二处是在给 `tom.id` 赋值的时候，由于它是只读属性，所以报错了。

## 类型断言
类型断言`（Type Assertion）`可以用来手动指定一个值的类型。

语法

	<类型>值
		或
	值 as 类型
在 `tsx` 语法（`React` 的 `jsx` 语法的 `ts` 版）中必须用后一种。

例子：将一个联合类型的变量指定为一个更加具体的类型

当 `TypeScript` 不确定一个联合类型的变量到底是哪个类型的时候，只能访问此联合类型的所有类型里共有的属性或方法：

```javascript
	function getLength(something: string | number): number {
    	return something.length;
	}

	// index.ts(2,22): error TS2339: Property 'length' does not exist on type 'string | number'.
	//   Property 'length' does not exist on type 'number'.
```
而有时候，确实需要在还不确定类型的时候就访问其中一个类型的属性或方法，比如：

```javascript
	function getLength(something: string | number): number {
    	if (something.length) {
        	return something.length;
    	} else {
        	return something.toString().length;
    	}
	}

	// index.ts(2,19): error TS2339: Property 'length' does not exist on type 'string | number'.
	//   Property 'length' does not exist on type 'number'.
	// index.ts(3,26): error TS2339: Property 'length' does not exist on type 'string | number'.
	//   Property 'length' does not exist on type 'number'.
```
上例中，获取 `something.length` 的时候会报错。

此时可以使用类型断言，将 `something` 断言成 `string4`：

```javascript
	function getLength(something: string | number): number {
    	if ((<string>something).length) {
        	return (<string>something).length;
    	} else {
        	return something.toString().length;
    	}
	}
```
类型断言的用法如上，在需要断言的变量前加上 `<Type>` 即可。

类型断言不是类型转换，断言成一个联合类型中不存在的类型是不允许的：

```javascript
	function toBoolean(something: string | number): boolean {
    	return <boolean>something;
	}

	// index.ts(2,10): error TS2352: Type 'string | number' cannot be converted to type 'boolean'.
	//   Type 'number' is not comparable to type 'boolean'.
```
## 内置对象
`JavaScript` 中有很多内置对象，它们可以直接在 `TypeScript` 中当做定义好了的类型。
内置对象是指根据标准在全局作用域（`Global`）上存在的对象。这里的标准是指 `ECMAScript` 和其他环境（比如 `DOM`）的标准。

### ECMAScript 的内置对象
* Boolean
* Error
* Date
* RegExp
* ......

可以在 `TypeScript` 中将变量定义为这些类型：

```javascript
	let b: Boolean = new Boolean(1);
	let e: Error = new Error('Error occurred');
	let d: Date = new Date();
	let r: RegExp = /[a-z]/;
```

### DOM 和 BOM 的内置对象

* Document
* HTMLElement
* Event
* NodeList
* ......

`TypeScript` 中会经常用到这些类型：

```javascript
	let body: HTMLElement = document.body;
	let allDiv: NodeList = document.querySelectorAll('div');
	document.addEventListener('click', function(e: MouseEvent) {
	  // Do something
	});
```
### TypeScript 核心库的定义文件
`TypeScript` 核心库的定义文件中定义了所有浏览器环境需要用到的类型，并且是预置在 `TypeScript` 中的。

当你在使用一些常用的方法的时候，TypeScript 实际上已经帮你做了很多类型判断的工作了，比如：

```javascript
	Math.pow(10, '2');

	// index.ts(1,14): error TS2345: Argument of type 'string' is not assignable to parameter 	of type 'number'
```
上面的例子中，`Math.pow` 必须接受两个 `number` 类型的参数。事实上 `Math.pow` 的类型定义如下：

```javascript
	interface Math {
		pow(x: number, y: number): number;
	}
```
`DOM` 中的例子：

```javascript
	document.addEventListener('click', function(e) {
    	console.log(e.targetCurrent);
	});

	// index.ts(2,17): error TS2339: Property 'targetCurrent' does not exist on type 	'MouseEvent'.
```
上面的例子中，`addEventListener` 方法是在 `TypeScript` 核心库中定义的：

```javascript
	interface Document extends Node, GlobalEventHandlers, NodeSelector, DocumentEvent {
		addEventListener(type: string, listener: (ev: MouseEvent) => any, useCapture?: 	boolean): void;
	}
```
	
所以 `e` 被推断成了 `MouseEvent`，而 `MouseEvent` 是没有 `targetCurrent` 属性的，所以报错了。

注意，`TypeScript` 核心库的定义中不包含 `Node.js` 部分。

`Node.js` 不是内置对象的一部分，如果想用 `TypeScript` 写 `Node.js`，则需要引入第三方声明文件：

	npm install @types/node --save-dev


## 未完待续...
