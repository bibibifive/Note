# ES6新特性

ES6 模块的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。



#### ES6 import

import 会被转化为commonjs 格式或者是AMD 格式，所以不要把它认为是一种新的模块引用方式。babel 默认会把ES6 的模块转化为commonjs 规范的，你也不用费劲再把它转成AMD 了。

```js
import list from './list';
//等价于
var list = require('./list');
```

## 预编译
预编译发生在 JavaScript 代码执行前，对代码进行语法分析和代码生成，初始化的创建并存储变量，为执行代码做好准备。
预编译过程：
1. 创建GO/AO对象（GO是全局对象，AO是活动对象）
2. 将形参和变量声明赋值为 undefined
3. 实参形参相统一
4. 函数声明提升（将变量赋值为函数体）

## this
this是函数被调用时发生的绑定，它指向什么完全取决于函数在哪里被调用。我理解的this是函数的调用者对象，当在函数内使用this，可以访问到调用者对象上的属性和方法。
#### this绑定的四种情况：
1. [new 绑定](#new的过程)。new实例化
2. [显示绑定](#callapplybind)。call、apply、bind手动更改指向
3. 隐式绑定。由上下文对象调用，如 obj.fn()，this 指向 obj （`即函数调用`）
4. 默认绑定。默认绑定全局对象，在严格模式下会绑定到undefined

优先级 `new绑定` 最高，最后到 `默认绑定`。


## new的过程
1. 创建一个空对象
2. 设置原型，将对象的 __proto__ 指向构造函数的 prototype
3. 构造函数中的 this 执行对象，并执行构造函数，为空对象添加属性和方法
4. 返回实例对象

`注意点：`
构造函数内出现return:
1. 如果返回基本类型，则提前结束构造过程，返回实例对象；
2. 如果返回引用类型，则返回该引用类型。

```js
// 返回基本类型
function Foo(){
    this.name = 'Joe'
    return 123
    this.age = 20
}
new Foo() // Foo {name: "Joe"}
```
```js
// 返回引用类型
function Foo(){
    this.name = 'Joe'
    return [123]
    this.age = 20
}
new Foo() // [123]
``` 

## call|apply|bind
->三者作用都是改变this指向的。
`call` 和 `apply` 改变 this 指向并调用函数，它们两者区别就是传参形式不同：
前者的参数是*逐个传入*，
后者传入*数组类型*的参数列表。
`bind` 改变 this 并返回一个*函数引用*，bind 多次调用是无效的，它改变的 this 指向只会以*第一次调用为准*。

#### 手写call
```js
Function.prototype.mycall = function () {
  if(typeof this !== 'function'){
    throw 'caller must be a function'
  }
  let othis = arguments[0] || window
  othis._fn = this
  let arg = [...arguments].slice(1)
  let res = othis._fn(...arg)
  Reflect.deleteProperty(othis, '_fn') //删除_fn属性
  return res
}
apply 实现同理，修改传参形式即可
```
#### 手写bind
```js
Function.prototype.mybind = function (oThis) {
  if(typeof this != 'function'){
    throw 'caller must be a function'
  }
  let fThis = this
  //Array.prototype.slice.call 将类数组转为数组
  let arg = Array.prototype.slice.call(arguments,1)
  let NOP = function(){}
  let fBound = function(){
    let arg_ = Array.prototype.slice.call(arguments)
    // new 绑定等级高于显式绑定
    // 作为构造函数调用时，保留指向不做修改
    // 使用 instanceof 判断是否为构造函数调用
    return fThis.apply(this instanceof fBound ? this : oThis, arg.concat(arg_))
  }
  // 维护原型
  if(this.prototype){
    NOP.prototype = this.prototype
    fBound.prototype = new NOP()
  }
  return fBound
}
```


## 对ES6语法的了解

常用：let、const、扩展运算符、模板字符串、对象解构、[箭头函数](#箭头函数和普通函数的区别)、默认参数、[Promise](#promise)

数据结构：[Set](#setweaksetmapweakmap)、[Map](#setweaksetmapweakmap)、Symbol

其他：Proxy、Reflect

#### Set|WeakSet|Map|WeakMap
1. `Set`:
成员的*值都是唯一的*，没有重复的值，类似于数组
可以遍历

2. `WeakSet`:
成员必须为引用类型
成员都是弱引用，可以被垃圾回收。成员所指向的外部引用被回收后，该成员也可以被回收
*不能遍历*

3. `Map`:
键值对的集合，键值可以是任意类型
可以遍历

4. `WeakMap`:
*只接受引用类型作为键名*
键名是弱引用，键值可以是任意值，可以被垃圾回收。键名所指向的外部引用被回收后，对应键名也可以被回收
*不能遍历*


## 箭头函数和普通函数的区别
1. this指向在编写代码时就已经确定，即箭头函数本身所在的作用域；
    普通函数在调用时确定this。
2. 没有arguments
3. 没有prototype属性

## Promise
Promise 是ES6中新增的异步编程解决方案，*避免回调地狱问题*。
Promise 对象是*通过状态的改变来实现*通过*同步的流程来表示异步的操作*, 只要状态发生改变就会自动触发对应的函数。

Promise对象*有三种状态*，分别是：

1. `pending`: 默认状态，只要没有告诉 promise 任务是成功还是失败就是 pending 状态
2. `fulfilled`: 只要调用 resolve 函数, 状态就会变为fulfilled, 表示操作成功
3. `rejected`: 只要调用 rejected 函数, 状态就会变为 rejected, 表示操作失败

状态一旦改变既不可逆，可以通过函数来监听 Promise 状态的变化，
成功执行 `then` 函数的回调，
失败执行 `catch` 函数的回调


## 基本包装类型

基本类型按道理说是没有属性和方法，但是在实际操作时，我们却能从基本类型调用方法，就像一个字符串能调用 split 方法。
```js
let str = 'hello'
str.split('')
```
为了方便操作基本类型值，每当读取一个基本类型值的时候，后台会创建一个对应的基本包装类型的对象，从而让我们能够调用方法来操作这些数据。大概过程如下：

```js
let str = new String('hello') //创建String类型的实例
str.split('') //在实例上调用指定的方法
str = null //销毁这个实例
```

## 闭包:
闭包的本质就是作用域问题。当函数可以记住并访问所在作用域，且*该函数在所处作用域之外被调用时*，就会产生闭包。

简单点说，一个函数内引用着所在作用域的变量，并且它被保存到其他作用域执行，引用变量的作用域并没有消失，而是跟着这个函数。当这个函数执行时，就可以通过作用域链查找到变量。

```js
let bar
function foo() {
    let a = 10
    // 函数被保存到了外部
    bar = function () {
        // 引用着不是当前作用域的变量a
        console.log(a)
    }
}
foo()
// bar函数不是在本身所处的作用域执行
bar() // 10
```
优点:*私有变量*或方法、缓存

缺点:闭包让作用域链得不到释放，会导致*内存泄漏*

## 原型链:
JavaScript 中的对象有一个特殊的内置属性 prototype（原型），它是对于其他对象的引用。当查找一个变量时，会优先在本身的对象上查找，如果找不到就会去该对象的 prototype 上查找，以此类推，最终以 Object.prototype 为终点。多个 prototype 连接在一起被称为原型链。


## 原型继承

#### 圣杯模式

```js
function inherit(Target, Origin){
  function F() {};
  F.prototype = Origin.prototype;
  Target.prototype = new F();
  // 还原 constuctor
  Target.prototype.constuctor = Target;
  // 记录继承自谁
  Target.prototype.uber = Origin.prototype; 
}
```

使用：
```js
function Person() {
  this.name = 'people'
}
Person.prototype.sayName = function () { console.log(this.name) }
function Child() {
  this.name = 'child'
}
inherit(Child, Person)
Child.prototype.age = 18
let child = new Child()
```
圣杯模式的好处在于，使用中间对象隔离，子级添加属性时，都会加在这个对象里面，不会对父级产生影响。而查找属性是沿着 `__proto__` 查找，可以顺利查找到父级的属性，实现继承。

#### ES6 Class

```js
class Person {
    constructor() {
        this.name = 'people'
    }
    sayName() {
        console.log(this.name)
    }
}
class Child extends Person {
    constructor() {
        super()
        this.name = 'child'
    }
}
Child.prototype.age = 18
let child = new Child()
```

Class 可以通过 extends 关键字实现继承，这比 ES5 的通过修改原型链实现继承，要清晰和方便很多。






