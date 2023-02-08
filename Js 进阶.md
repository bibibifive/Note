# JS 进阶及细节复习

# script 脚本

其实就是短小的、用来让计算机自动化完成一系列工作的程序
这类程序可以用文本编辑器修改
通常是解释运行的——也就是说，计算机里有一个程序能一句一句地把脚本里的内容转换成 CPU 能理解的指令，而且它每次只解释一句，CPU 跑完了才解释下一句。

#### 动态与静态 是 灵活与稳定 的权衡

#### 动态类型语言

JS 是个==动态类型语言==,这直接决定了它不能在运行前编译成机器码,达到快速的运行

所以运用的时==JIT==(Just-In-Time Compilation)运行时编译并执行代码

而偏低级一点语言的静态类型语言用的是,==AOT==(Ahead of Time)在运行前提前生成机器码

所以 JS 需要==JS 引擎==(程序),将 JS 转换成低级的机器语言并执行

#### JS 引擎运行流程

##### JS 源码->AST->字节码->机器码

1.  将 JS 源码通过->(==<u>解析器 parser</u>==)->解析成==抽象语法树 AST==
2.  进而通过->(==<u>解释器 interpreter</u>==)->编译为==字节码 bytecode==(跨平台的中间表示,与平台无关,在不同操作系统中运行)
3.  最后通过->(==<u>编译器 compiler</u>==)->生成==机器码 machine code==(由于不同的处理器平台,使用的机器代码会有差异,所以编译器会根据当前平台编译出相应的==机器代码(汇编代码)==)

#### JS 引擎三个重要组件

解析器 parser

解释器 interpreter

编译器 compiler

以 V8 引擎为例:(C++写的(静态语言))

是用==C++编写==的 Google 开源高性能==JavaScript 和 WebAssembly 引擎==。它用于 Chrome 和 Node.js 等它实现了 ECMAScript 和 WebAssembly,并在 Windows7 或更高版本 nacOS10.12+和使用 x64,1A-32,ARM
或 MIPS 处理器的 Linux 系统上运行。

如今的 V8 引擎有两个特点

<img src="./assets/Js 进阶.assets/image-20220423144340889.png" alt="image-20220423144340889" style="zoom: 25%;" />

##### 基准解释器 Igniton

- 将 AST 生成为字节码(是机器码的 25%-50%),加快了网页初始化解析执行 JS

##### 优化编译器 TruboFan

- 优化执行频次较高的变量类型和函数,将字节码编译为经过优化的机器码
- 当使用这些热点代码时,就直接使用优化后的机器码(==此时优化机器码与运行字节码共存==)
- 当然由于变量类型的使用更改,这些机器码就会逆向还原为字节码(deoptimization)

1.  函数只声明未被调用，不会被解析生成 ast
2.  函数只被调用一次，bytecodej 直接被解释执行
3.  函数被调用多次，可能会被标记为热点函数，可能会被编译成机器代码

面向对象编程(oop), 面向对象实质上是增加了耦合性, 让相关的属性方法操作放在同一对象中使用, 提高了可读性, 同时也会降低复用性, 但是通过原型继承也可以提供其复用性.

## 7 种基础数据类型 + 1 个复杂数据类型

#### 基础数据类型(原始类型)

1.  Number 数值
2.  String 字符串
3.  BigInt 任意长度的整数
    - 在数字后面附加 n
4.  Boolean 布尔型
5.  null 空的
6.  undefined 未定义的
7.  symbol 用于创建对象的唯一标识符

#### 复杂数据类型(原始类型)

1.  object

`typeof` 运算符返回值的类型，但有两个例外：

```javascript
typeof null == 'object' // JavaScript 编程语言的设计错误
typeof function () {} == 'function' // 函数被特殊对待
```

## 三种浏览器自带的模态弹框

#### 模态框(modal)

- 不可在处理完模态框之前与其他界面交互
- 停止页面渲染
- 不可修改其样式

#### alert(message)

提示(警示)用户的内容

不返回 (返回 undefined)

```

```

#### prompt(question[, default\])

title:提示用户的文本

default:替代用户输入的默认值(str)

返回用户输入

```

```

#### confirm(question)

question:要求用户确认的信息

返回布尔值 用户点击(确认:true, 取消:false)

```js

```

## 字符串比较

1.  字符串比较是通过逐个比较字符的 Unicode 编码顺序来确定字符串大小的,

2.  按顺序对比字符,发现不同即可以判断整个字符串的大小.

3.  先没有字符的为小

```js
'cac' < 'cad' //true
'abc' > 'ab' //true
'a' < 'b' //true
```

## 与值的比较

当比较中有一个值, 非值会隐式转换成数值

#### 当 null 在和 undefined 对比时

- 在不严格相等的`==`时 null 和 undefined 是直接判断 true 的且,此时他们是不会进行类型转换的.

- `===`时,null 和 undefined 是不同的两个类型 所以为 false

- 在`> < <= >=` 时,null 和 undefined 还是会转换成数值

#### undefined ->(数值) NaN

#### null ->(数值) 0

# 隐式转换
<img src="./assets/Js 进阶.assets/1665999636373.jpg" alt="1665999636373" style="zoom: 100%;" />

### ToString()
#####null & undefined
null 转化为 [object null]
undefined 转化为 [object Undefined]
#####布尔值
[object Undefined]
#####数字
其加上""
NaN 转化为 [object Undefined] 
> toString(2) // '2'

#####对象
走 ToPrimitive()
已为基本类型非数字 再 进行隐式转化

### ToNumber()
#####null & undefined
null 转化为 0
undefined 转化为 NaN
#####布尔值
true转化为1，false转化为0
#####字符串
字符串的处理遵循通用规则
> Number('25') // 25
Number('a') // NaN
#####对象
走 ToPrimitive()
已为基本类型非数字 再 进行隐式转化

### ToBoolean()
#####null & undefined
null 转化为 `false`
undefined 转化为 `false`
>Boolean(null)  // false

#####字符串
"" 转化为  `false`
其他字符串 转化为 *true*
>Boolean('0')  // true

#####数字
除0(包括+0和-0)和NaN外，所有数字转化为*true*
>Boolean(0)  // false
Boolean(NaN)  // false

#####对象
所有对象 转化为 *true*
>Boolean({})  // true
Boolean([])  // true

### ToPrimitive()
ToPrimitive操作会首先检查对象是否有`valueOf()`方法，如果有并且返回基本类型的值，就调用该方法进行类型转化。 
如果没有就使用`toString()`返回的值。 
若`valueOf()`和`toString()`均不返回基本类型值，就会产生TypeError错误。

如果不对对象和数组的`valueOf()`和`toString()`方法进行重写，那么：
对象的`valueOf()`返回对象*本身*，`toString()`返回"[object Object]"
数组的`valueOf()`返回数组*本身*，`toString()`返回所有单元字符串化以后再用","连接起来。（数组降维算法）
>var a = [1,2,3]
a.toString()  // "1,2,3"

## 运算中的类型转换

在加法运算中，字符串很强势，同[转为字符串](#tostring),其他则按[转为数字](#tonumber)

## 比较中的类型转换

###`==` 不严格比较类型

undefined 等于 null

字符串、布尔值、null比较时，都会[转为数字](#tonumber)比较

引用类型在隐式转换时会先[转为字符串](#tostring)比较，如果不相等然再[转为数字](#tonumber)比较


## 运算符

#### 运算元

- 运算符应用的对象

#### 一元运算符(`+`)

1.  可以将字符串进行数值转换, 相当于 Number(str)

```js
let a = '123'
let b = +a
console.log(typeof b) //number
```

2.  连接字符串,并将数字隐式转换为字符串

#### 一元运算符(`-`)

- 对数字进行正负转换

#### 二元运算符(`**`)

- 求幂

- ```js
  let a = 2 ** 4 //16
  let b = 4 ** (1 / 2) //2 (平方根)
  ```

# 逻辑运算

#### 或(`||`)

#### 与运算寻找第一个真值

或运算 `||` 的链，将返回第一个真值，如果不存在真值，就返回该链的最后一个值。

- #### **短路**

  - 遇真停止处理后续参数, 后续参数内表达式将不被执行.

#### 与(`&&`)

#### 与运算寻找第一个假值

与运算返回第一个假值，如果没有假值, 就返回最后一个值。

- #### **短路**

  - 遇假停止处理后续参数, 后续参数内表达式将不被执行.

**与运算** `&&` **在或运算** `||` **之前进行**

#### 非(`!`)

`!`将操作数转化为布尔类型, 返回相反的值

两个非运算 `!!` 有时候用来将某个值转化为布尔类型 (相当于 Boolean())

非运算符 `!` 的优先级在所有逻辑运算符里面最高，所以它总是在 `&&` 和 `||` 之前执行。

#### 空置合并运算符(`??`)

`a ?? b` 的结果是：

- 如果 `a` 是已定义的，则结果为 `a`，
- 如果 `a` 不是已定义的，则结果为 `b`。

如果第一个参数不是 `null/undefined`，则 `??` 返回第一个参数。否则，返回第二个参数。

它只是一种获得两者中的==第一个“已定义的”值==的不错的语法。

##### 它们之间重要的区别是：

- `||` 返回第一个 **真** 值。
- `??` 返回第一个 **已定义的** 值。

- `??` 运算符的优先级非常低，仅略高于 `?` 和 `=`，因此在表达式中使用它时请考虑添加括号。
- 如果没有明确添加括号，不能将其与 `||` 或 `&&` 一起使用。

优先级 : `!`(15) > `&&`(5) >`||`(4) = `??`(4)

## switch

`switch` 语句为多分支选择的情况提供了一个==更具描述性==的方式。

`switch` 语句有至少一个 `case` 代码块和一个可选的 `default` 代码块。

```js
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]
  default:
    ...
    [break]
}
```

比较 `x` 值与第一个 `case`==是否严格相等(`===`)== (类型很关键)

`switch` 语句就执行相应 `case` 下的代码块，直到遇到最靠近的 `break` 语句

<u>`switch` 和 `case` 都允许任意表达式。</u>

##### “case” 分组

其实是 switch 的一个副作用,没有 break 就会继续执行代码

```javascript
let a = 3
switch (a) {
  case 3: // (*) 下面这两个 case 被分在一组
  case 5:
    alert('Wrong!')
    break
  default:
    alert('The result is strange. Really.')
}
```

| 几种逻辑运算     | 应用场景                            |
| ---------------- | ----------------------------------- | ------ | --------------------------- |
| `switch` 语句    | 一对多的判断比较                    |
| `if` 语句        | 更加复杂的判断比较                  |
| `? :` 三元运算符 | 单判断, 双结果的简单判断比较        |
| `                |                                     | `/`&&` | 多结果(自带判断),求真(假)值 |
| `??`             | 双结果,避免未定义值传入(默认值设置) |

# 循环

循环体的单次执行叫作 **一次迭代**。

#### while

因为循环条件内的表达式会被隐式转换为布尔型

- while (i != 0) `可简写为` while (i)

#### do..while

使用 `do..while` 语法可以将==条件检查==移至==循环体== **下面**：

```js
do {
  // 循环体
} while (condition)
```

#### for

```js
for (begin; condition; step) {
  // ……循环体……
}
```

| 语句段         |             |                                                      |
| :------------- | :---------- | :--------------------------------------------------- |
| begin          | `let i = 0` | 进入循环时==执行一次==。                             |
| condition      | `i < 3`     | 在每次循环==迭代之前检查==，如果为 false，停止循环。 |
| body（循环体） | `alert(i)`  | 条件为真时，重复运行。                               |
| step           | `i++`       | 在每次循环体==迭代后执行==。                         |

#### 循环算法工作原理

开始运行 → (如果 condition 成立 → 运行 body 然后运行 step) ->…

#### 内联变量声明

```js
for (let i = 0; i < 3; i++) {}
alert(i) //未定义
```

这里“计数”变量 `i` 是在循环中声明的。这叫做“内联”变量声明。这样的变量只在循环中可见。

#### `for` 循环的任何语句段都可以被省略。

```js
for (;;) {
  //无限循环
}
```

#### break

跳过整个循环 (例: 为了达成条件跳出无限循环)

#### continue

跳过此次迭代,继续新的迭代 (例: 为了筛掉不需要的迭代内容)

`continue` **指令利于减少嵌套**

##### <u>请注意非表达式的语法结构不能与三元运算符 `?` 一起使用。</u>(break / continue)

### break/continue 标签

**标签** 是在循环之前带有冒号的标识符：(outer)

```js
outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    ...
    if (!input) break outer; //
    ...
  }
}
alert('Done!');
```

此时的 break 就能直接跳出 outer 循环了.

当然 continue 也可以,跳出被标签的循环的那次迭代,继续新的迭代.

当然 break / continue 都只能跳出自身所处的循环.

##### 我们还可以将标签移至单独一行：

```javascript
outer:
for (let i = 0; i < 3; i++) { ... }
```

##### 从技术上讲，任何被标记的代码块都有效，例如：

即 不是循环也可以

```javascript
label: {
  // ...
  break label // 有效
  // ...
}
```

但是 continue 就只能用于循环内.

# 函数

==函数是程序的主要“构建模块”。==函数使该段代码可复用，避免代码重复。

内建函数 如:alert(message)

### 函数声明

1.  function 关键字
2.  函数名
3.  (参数列表)
4.  {函数体}

```js
function showMessage() {
  alert('Hello everyone!')
}
```

!! 函数可以在函数内部修改外部变量,即外部可以感知到修改.

- 就近原则(作用域链查询),函数内没有相应 a,最后找到外部 a

```js
let a = 1
function sum(num1) {
  a += num1
  alert(a) //2
}
sum(1)
alert(a) //2
```

!! 函数当在函数体中修改传参,其实修改的是传入的实参的复制,外部的实参不会感知到修改.

- 就近原则(作用域链查询),所以被修改的不是全局的 a,而是传参中复制的 a

```js
let a = 1
function sum(a) {
  a += a
  alert(a) //2
}
sum(a)
alert(a) //1
```

参数（parameter）: 传参 (声明时参数)

参数（parameter）: 实参 (调用时参数)

#### 默认值 (默认参数)

给传参加一个 `= 默认值` ,否则没有传入的参数将会被视为 undefined

```js
function showMessage(from, text = 'no text given') {
  alert(from + ': ' + text)
}
```

老版本的 js 还不支持参数带默认值时,显示地转换默认值

```js
text = text || 'no text given'
```

在函数执行时判断是否定义 用??语义更为合理

```js
text = text ?? 'no text given'
```

#### 返回值 return

函数的返回值 没有指定或指定缺省即为 undefined

return 语句 不能换行并独占一行,因为 return 后会加一个分号`;`

```js
function func() {
  return
  a + b
} // 返回undefined

//可以这样 ↓
function func() {
  return a + b
}
```

#### 函数命名(建议)

应该遵循动词+名词的搭配,且不要让函数执行函数名语义外的工作。

高并发,低耦合

达到函数名 自描述

### 函数表达式

函数是作为表达式的一部分创建的

把函数赋值给变量

```javascript
let sayHi = function () {
  alert('Hello')
}
```

## [!!函数是一个值](https://zh.javascript.info/function-expressions#han-shu-shi-yi-ge-zhi)

重申一次：无论函数是如何创建的，函数都是一个值。上面的两个示例都在 `sayHi` 变量中存储了一个函数。

我们还可以用 `alert` 打印这个变量的值：↓

```javascript
function sayHi() {
  alert('Hello')
}

alert(sayHi) // 显示函数代码
```

此处没有括号不会调用函数

因为是值所以可以赋给其他的变量 ↓

```js
...
let func = sayHi;
```

**一个函数是表示一个 “行为” 的值**

==字符串或数字==等常规值代表 **数据**。

==函数==可以被视为一个 **==行为（action）==**。

我们可以在变量之间传递它们，并在需要时运行。

#### 回调函数

函数作为其他函数的参数被调用

#### 匿名函数

没有赋给任何变量的函数 也不是声明函数

### 区别 函数声明 & 函数表达式

函数声明 是在 JavaScript 准备运行脚本时被创建的 (==函数提升==)

- 在处理完所有==函数声明==后，代码才被执行。
- 函数声明 也受==块级作用域==影响 只能提升到该块级作用域顶部, 外部同样同样不能调用
- -更醒目, 更灵活

函数表达式 在==代码执行到它时才会被创建==。

- 函数表达式 可以在全局先声明变量, 让块级内的函数赋值可以作用到全局

- -用不了函数声明时

## 箭头函数

创建函数还有另外一种非常简单的语法，并且这种方法通常比函数表达式更好。↓

没有括号 是因为表达式足够简短,不一定只能有返回值(也可以是操作)

```javascript
let sum = (a, b) => a + b

/* 这个箭头函数是下面这个函数的更短的版本：

let sum = function(a, b) {
  return a + b;
};
*/
```

如果我们只有一个参数，还可以==省略掉参数外的圆括号==，使代码更短。↓

```javascript
let double = (n) => n * 2
// 差不多等同于：let double = function(n) { return n * 2 }
```

如果<u>没有参数</u>，==括号则是空的==（但括号必须保留）：↓

```javascript
let sayHi = () => alert('Hello!')
```

动态创建箭头函数 (匿名创建函数)

```
let welcome = (age < 18) ?
  () => alert('Hello'!) :
  () => alert("Greetings!");
```

在这种情况下，我们可以使用花括号将它们括起来。主要区别在于，==用花括号括起来之后，需要包含 `return` 才能返回值==（就像常规函数一样）。↓

```javascript
let sum = (a, b) => {
  // 花括号表示开始一个多行函数
  let result = a + b
  return result // 如果我们使用了花括号，那么我们需要一个显式的 “return”
}
```

声明函数自然不能搭配…

# 对象 Object

属性名可以是==任何字符串==或者 ==symbol==

- 对象的属性名可以是编程语言的某个保留字

数字也会被转换为字符串

我们通常用 null 表示对象中的未知值 和 空值

对象的属性访问方式:

1.  obj.key

    - ==不能为变量==, 连续的字符串(非字符串隐式转为字符串)

2.  obj["key"]

    - 以方括号和字符串搭配,访问对象属性

    - ```js
      user['likes birds'] = true
      ```

3.  obj[key]

    - 数字会隐式转为==字符串==

    - 方括号同样提供了一种可以通过==任意表达式==来获取属性名的方法(可用变量)

    - 计算属性

      - ```js
        let search = prompt('你想搜索什么')
        let bag = {
          [search]: 5, // 属性名是从 search 变量中得到的
        }
        ```

### 属性值简写

属性和值一样可以只写属性

```js
let user = {
  name, // 与 name:name 相同
  age: 30,
}
```

#### 删除 `delete user[key]`

#### 判定属性存在 `"key" in object`

- "key" in obj ("key"->字符串)
- key in obj (key->变量)

- 返回布尔 在或不在对象中

## “for…in” 循环

语法：

```javascript
for (let key in object) {
  // 对此对象属性中的每个键执行的代码
}
```

## 像对象一样排序

整数属性会被放在 obj 最前面, 其他属性按照创建顺序

为了避免整数排序, 需要自定义顺序, 我们用常见的"+1"、"+49"、"+86"

#### 对象是具有一些特殊特性的关联数组。

我们可以用下面的方法访问属性：

- 点符号: `obj.property`。
- 方括号 `obj["property"]`，方括号允许从变量中获取键，例如 `obj[varWithKey]`。

其他操作：

- 删除属性：`delete obj.prop`。
- 检查是否存在给定键的属性：`"key" in obj`。
- 遍历对象：`for(let key in obj)` 循环。

“普通对象（plain object）”，或者就叫对象。

JavaScript 中还有很多其他类型的对象：

- `Array` 用于存储有序数据集合，
- `Date` 用于存储时间日期，
- `Error` 用于存储错误信息。
- ……等等。

## 对象的引用和复制

### Object.assign (浅拷贝)

Object.assign(dest, [src1, src2, src3...])

拷贝一层值类型, 引用类型还是引用

对象通过引用被赋值和拷贝。

同样 ==展开语法==也可以==实现浅拷贝==

```js
let obj_1 = { age: 1 }
let obj_2 = { ...obj_1 }
```

当然 ==for 循环==一一复制也可以实现浅拷贝 (但是比较适合==稍有改变的复制==)

- 换句话说，一个变量存储的不是“对象的值”，而是一个对值的“引用”（内存地址）。

为了创建“真正的拷贝”（一个克隆），我们可以使用 `Object.assign` 来做所谓的“浅拷贝”（嵌套对象被通过引用进行拷贝）或者使用“深拷贝”函数，例如 [\_.cloneDeep(obj)](https://lodash.com/docs#cloneDeep)。

### 深拷贝

就是不断遍历引用对象拷贝值类型, 一般用==递归==实现.

# this

==为了函数的低耦合==, 用 this 代表正在调用该函数/方法的对象.

### 方法中的 “this”

方法可以将对象引用为 `this`。

`this` 的值就是在==点之前的这个对象==，即==调用该方法的对象==。

举个例子：

```javascript
let user = {
  name: 'John',
  age: 30,
  sayHi() {
    // "this" 指的是“当前的对象”
    alert(this.name)
  },
}

user.sayHi() // John(this->user)
```

JavaScript 中的 `this` 可以用于==任何函数==，即使它不是对象的方法。

`this` 的值是在==代码运行时计算出来的==，它取==决于代码上下文==。(动态的)

#### !使用点符号或方括号语法来访问这个方法

```js
user.f(); // John（this == user）
admin.f(); // Admin（this == admin）

admin['f']();
```

#### 没有指定的对象调用函数中的 this:

在这种情况下，严格模式下的 `this` 值为 `undefined`。

在非严格中`this`会指向浏览器中的`window`

#### 箭头函数没有自己的 `this`。

如果我们在这样的函数中引用 `this`，`this` 值取决于外部“正常的”函数。

同样: 不用箭头函数,用普通函数又要用到外部的 this 时就要传递 this 给变量,因为==this 是动态的==.

不是以方法调用的`this`无法通过点符号指向函数前的对象

```javascript
function makeUser() {
  return {
    name: 'John',
    ref: this, //因为是用作函数调用(而不是对象的方法),这里的this指的是undefined
  }
}

let user = makeUser()

alert(user.ref.name) // 错误
```

## 链式调用

关键是每次方法返回 this 就可以再次给下一个方法调用提供对象.

我们也可以每行一个调用。对于长链接它更具可读性：

```javascript
ladder
  .up()
  .up()
  .down()
  .showStep() // 1
  .down()
  .showStep() // 0
```

# 构造器和操作符 "new"

## [构造函数](https://zh.javascript.info/constructor-new#gou-zao-han-shu)

##### 我们经常需要创建很多类似的对象

- 构造函数，或简称==构造器==，就是常规函数，但大家对于构造器有个共同的约定，就是其==命名首字母要大写==。

构造函数在==技术上是常规函数==。不过有两个约定：

1.  它们的命名以大写字母开头。
2.  它们只能由 `"new"` 操作符来执行。

例如：

```javascript
function User(name) {
  this.name = name
  this.isAdmin = false
}

let user = new User('Jack')
```

当一个函数被使用 `new` 操作符执行时，它按照以下步骤：

1.  一个新的空对象被创建并分配给 `this`。
2.  函数体执行。通常它会修改 `this`，为其添加新的属性。
3.  返回 `this` 的值。

换句话说，`new User(...)` 做的就是类似的事情：

```javascript
function User(name) {
  // this = {};（隐式创建）!!

  // 添加属性到 this
  this.name = name
  this.isAdmin = false
  this.read = function () {
    this.value = +prompt('num1?', 0)
  }

  // return this;（隐式返回）!!
}
```

这是构造器的主要目的 —— 实现可重用的对象创建代码。

[**new function() { … }**](https://zh.javascript.info/constructor-new)

如果我们有许多行用于创建单个复杂对象的代码，我们可以将它们封装在一个==立即调用的构造函数==中

这个构造函数不能被再次调用，因为它不保存在任何地方，只是被创建和调用。

### **省略括号**

如果没有参数，我们可以省略 `new` 后的括号：

```javascript
let user = new User() // <-- 没有参数
// 等同于
let user = new User()
```

这里省略括号不被认为是一种“好风格”，但是规范允许使用该语法。

#### [类](https://zh.javascript.info/classes) 是用于创建复杂对象的一个更高级的语法

JavaScript 为许多内建的对象提供了构造函数：比如日期 `Date`、集合 `Set` 以及…

# 垃圾回收算法

## [内部算法](https://zh.javascript.info/garbage-collection#nei-bu-suan-fa)

垃圾回收的基本算法被称为 “mark-and-sweep”。

定期执行以下“垃圾回收”步骤：

- 垃圾收集器找到所有的根，并“标记”（记住）它们。
- 然后它遍历并“标记”来自它们的所有引用。
- 然后它遍历标记的对象并标记 **它们的** 引用。所有被遍历到的对象都会被记住，以免将来再次遍历到同一个对象。
- ……如此操作，直到所有可达的（从根部）引用都被访问到。
- 没有被标记的对象都会被删除。

垃圾回收是自动完成的，我们不能强制执行或是阻止执行。

当对象是可达状态时，它一定是存在于内存中的。

==被引用与可访问（从一个根）不同：一组相互连接的对象可能整体都不可达。==

#### 在熟悉了这门编程语言之后，把熟悉引擎作为下一步计划是明智之选。

# 代码结构

语句用分号分隔：

```javascript
alert('Hello')
alert('World')
```

通常，换行符也被视为分隔符，因此下面的例子也能正常运行：

```javascript
alert('Hello')
alert('World')
```

每个语句后面都加上分号。

在代码块 `{...}` 后以及有代码块的语法结构（例如循环）后==不需要加分号==

## 严格模式

```js
'use strict';
...
```

语言的一些现代特征（比如我们将来要学习的类）会隐式地启用严格模式。

# [在浏览器中调试](https://zh.javascript.info/debugging-chrome)

##### [控制台（Console）](https://zh.javascript.info/debugging-chrome#kong-zhi-tai-console)

##### [断点（Breakpoints）](https://zh.javascript.info/debugging-chrome#duan-dian-breakpoints)

##### 条件断点

1.  **`察看（Watch）` —— 显示任意表达式的当前值。**
2.  **`调用栈（Call Stack）` —— 显示嵌套的调用链。**
3.  **`作用域（Scope）` —— 显示当前的变量。**

**“恢复（Resume）”：继续执行，`快捷键F8`**

**“下一步（Step）”：运行下一条指令，`快捷键F9`**

**“跨步（Step over）”：运行下一条指令，但**不会进入到一个函数中，`快捷键F10`。

**“步入（Step into）”，和“下一步（Step）”类似，但在异步函数调用情况下表现不同。`快捷键F11`**。

**“步出（Step out）”：继续执行到当前函数的末尾，`快捷键Shift+F11`。**

#### 这里有 3 种方式来暂停一个脚本：

1.  一个断点。
2.  `debugger` 语句。
3.  一个错误（如果开发者工具是打开状态，并且按钮 是开启的状态）。

# 代码质量

花括号以 “Egyptian” 风格书写（译注：“egyptian” 风格又称 K&R 风格 — 代码段的开括号位于一行的末尾，而不是另起一行的风格）↓

```javascript
if (condition) {
  // do this
  // ...and that
  // ...and that
}
```

对于 `if` 语句： 一行代码的最大长度应该在团队层面上达成一致。通常是 80 或 120 个字符。

```javascript
if (id === 123 && moonPhase === 'Waning Gibbous' && zodiacSign === 'Libra') {
  letTheSorceryBegin()
}
```

##### 水平方向上的缩进：2 或 4 个空格。

##### 垂直方向上的缩进：用于==将代码拆分成逻辑块==的空行。↓

```javascript
function pow(x, n) {
  let result = 1
  //              <--
  for (let i = 0; i < n; i++) {
    result *= x
  }
  //              <--
  return result
}
```

- 写代码时，不应该出现连续超过 9 行都没有被垂直分割的代码。

#### 分号

每一个语句后面都应该有一个分号。

#### 嵌套层级

不必要的嵌套太深不利于程序高效运行

有时候使用 [`continue`](https://zh.javascript.info/while-for#continue) 指令以避免额外的嵌套是一个好主意。

#### 函数位置

先写调用代码，再写函数(函数声明), 因为调用函数的代码才最常看, 尤其是有自描述的函数名的函数更不需要经常看

# 注释

好的代码应该更少有`"解释型"`的注释, 因为 ↓

函数自己就变成了一个注释。这种代码被称为 **自描述型** 代码。

将命令式编程 ——重构--> 成函数式编程, 更简洁的自描述性

#### 我们应该尽可能地保持代码的简单和“自我描述”性。

## [好的注释](https://zh.javascript.info/comments#hao-de-zhu-shi)

描述架构

对组件进行高层次的整体概括，它们如何相互作用、各种情况下的控制流程是什么样的……
简而言之 —— 代码的鸟瞰图。

记录函数的参数和用法

有一个专门用于记录函数的语法 [JSDoc](http://en.wikipedia.org/wiki/JSDoc)：用法、参数和返回值。

例如：↓

```javascript
/**
 * 返回 x 的 n 次幂的值。
 *
 * @param {number} x 要改变的值。
 * @param {number} n 幂数，必须是一个自然数。
 * @return {number} x 的 n 次幂的值。
 */
function pow(x, n) {
  ...
}
```

这种注释可以帮助我们理解函数的目的，并且不需要研究其内部的实现代码，就可以直接正确地使用它。

## 为什么任务以这种方式解决？

解决方案的注释非常的重要。它们可以帮助你以正确的方式继续开发。
因为一段时间后,你可能不会记得为什么当时要用这个方案而不是其他的乍一看更改好的方案.

#### ==写得好的自描述函数本身就是一种注释==

#### 注释这些内容：

- 整体架构，高层次的观点。
- 函数的用法。
- 重要的解决方案，特别是在不是很明显时。

# 测试

实现 : 被测代码

用例 : 测试代码

一个规范包含==三个主要的模块==：

- `describe("title", function() { ... })`

  表示我们正在描述的功能是什么。在我们的例子中我们正在描述函数 `pow`。用于组织“工人（workers）” —— `it` 代码块。

- `it("use case description", function() { ... })`

  `it` 里面的描述部分，我们以一种 **易于理解** 的方式描述特定的用例，第二个参数是用于对其进行测试的函数。

- `assert.equal(value1, value2)`

  `it` 块中的代码，如果实现是正确的，它应该在执行的时候不产生任何错误。

该页面可分为五个部分：↓

1.  `<head>` —— 添加用于==测试的第三方库和样式文件==。(\*引入测试库)
2.  `<script>` 包含==测试函数==，在我们的例子中 —— 和 `pow` 相关的代码。
3.  ==测试代码== —— 在我们的案例中是名为 `test.js` 的脚本，它包含上面 `describe("pow", ...)` 的那些代码。
4.  HTML 元素 `<div id="mocha">` 将被 Mocha 用来==输出结果==。
5.  可以使用 `mocha.run()` 命令来==开始测试==。

==BDD== 的做法：我们首先写一些暂时无法通过的测试，然后去实现它们。

在 BDD 中，规范先行，实现在后。最后我们同时拥有了规范和代码。

规范有三种使用方式：

1.  作为 **测试** —— 保证代码正确工作。
2.  作为 **文档** —— `describe` 和 `it` 的标题告诉我们函数做了什么。
3.  作为 **案例** —— 测试实际工作的例子展示了一个函数可以被怎样使用。

# symbol

`symbol` 是唯一标识符的基本类型

有一个描述的类字符串类型(本人理解)

symbol 总是不同的值，即使它们有相同的名字。

如果我们希望同名的 symbol 相等，那么我们应该使用全局注册表：`Symbol.for(name)`

- 全局 symbol 注册表–>用于使用描述不重复的 symbol
- symbol.for("name")->找到名为 name 的唯一全局注册表

`Symbol.keyFor(sym)`，它的作用完全反过来：通过全局 symbol 变量返回一个名字 //name。

1.  “隐藏” 对象属性。
    - 该属性将受到保护，防止被意外使用或重写。(不参与一般遍历)
2.  使用 `Symbol.iterator` 来进行 [迭代](https://zh.javascript.info/iterable) 操作
3.  使用 `Symbol.toPrimitive` 来设置 [对象原始值的转换](https://zh.javascript.info/object-toprimitive)

```js
let HOST = symbol()
class Request {
  [HOST]:"http://abc.com"
  set host(url){
    if(!/^https?:/i.test(url)){
      throw new Error("非常网址");
    }
    this.[HOST] = url
return
  }
}
```

# 对象 — 原始值转换

所有对象->"boolean"都是 true

#### 有三种类型（hint）：

- `"string"`（对于 `alert` 和其他需要字符串的操作）
- `"number"`（对于数学运算）
- `"default"`（少数运算符，通常对象以和 `"number"` 相同的方式实现 `"default"` 转换）

#### 转换算法是：

1.  调用 `obj[Symbol.toPrimitive](hint)` 如果这个方法存在，
2.  否则，如果 hint 是 `"string"`
    - 尝试调用 `obj.toString()` 或 `obj.valueOf()`，无论哪个存在。
3.  否则，如果 hint 是 `"number"` 或者 `"default"`
    - 尝试调用 `obj.valueOf()` 或 `obj.toString()`，无论哪个存在。

所有这些方法都必须返回一个原始值才能工作（如果已定义）。

在实际使用中，通常只实现 `obj.toString()` 作为字符串转换的“全能”方法==就足够了==，该方法应该返回对象的“人类可读”表示，用于日志记录或调试。

# 原始类型的方法

1.  原始类型仍然是原始的。与预期相同，提供单个值
2.  JavaScript 允许访问字符串，数字，布尔值和 symbol 的方法和属性。
3.  为了使它们起作用，==创建了提供额外功能的特殊“对象包装器”==，使用后即被销毁。

\

1.  当访问 `str` 的属性时，一个==“对象包装器”==被创建了。
2.  在严格模式下，向其写入内容会报错。
3.  否则，将继续执行带有属性的操作，该对象将获得 `test` 属性，但是此后，“对象包装器”将消失，因此在最后一行，`str` 并没有该属性的踪迹。

**这个例子清楚地表明，原始类型不是对象。**

它们不能存储额外的数据。

# Number 数字类型

## [编写数字的更多方法](https://zh.javascript.info/number#bian-xie-shu-zi-de-geng-duo-fang-fa)

假如我们需要表示 10 亿。显然，我们可以这样写：

```javascript
let billion = 1000000000
```

我们也可以使用下划线 `_` 作为分隔符：(与上方一样)

```javascript
let billion = 1_000_000_000
```

在 JavaScript 中，我们可以通过在数字后面附加字母 `"e"` 并指定零的个数来缩短数字：

```javascript
let billion = 1e9 // 10 亿，字面意思：数字 1 后面跟 9 个 0
```

就像以前一样，可以使用 `"e"` 来完成。如果我们想避免显式地写零，我们可以这样写：

```javascript
let mcs = 1e-6 // 1 的左边有 6 个 0 //0.000001
```

## [十六进制，二进制和八进制数字](https://zh.javascript.info/number#shi-liu-jin-zhi-er-jin-zhi-he-ba-jin-zhi-shu-zi)

可以直接在十六进制（`0x`），八进制（`0o`）和二进制（`0b`）系统中写入数字。

十六进制 数字在 JavaScript 中被广泛用于表示颜色，编码字符以及其他许多东西。所以自然地，有一种较短的写方法：`0x`，然后是数字。

```javascript
alert(0xff) // 255
alert(0xff) // 255（一样，大小写没影响）
```

二进制和八进制数字系统很少使用，但也支持使用 `0b` (二) 和 `0o` (八) 前缀：

```javascript
let a = 0b11111111 // 二进制形式的 255
let b = 0o377 // 八进制形式的 255

alert(a == b) // true，两边是相同的数字，都是 255
```

## [toString(base)](https://zh.javascript.info/number#tostringbase)

方法 `num.toString(base)` 返回在给定 `base` 进制数字系统中 `num` 的==字符串==表示形式。

举个例子：

```javascript
let num = 255

alert(num.toString(16)) // ff
alert(num.toString(2)) // 11111111
```

`base` 的范围可以从 `2` 到 `36`。默认情况下是 `10`。

常见的用例如下：

- **base=16** 用于十六进制颜色，字符编码等，数字可以是 `0..9` 或 `A..F`。
- **base=2** 主要用于调试按位操作，数字可以是 `0` 或 `1`。
- **base=36** 是最大进制，数字可以是 `0..9` 或 `A..Z`。所有拉丁字母都被用于了表示数字。对于 `36` 进制来说，一个有趣且有用的例子是，当我们需要将一个较长的数字标识符转换成较短的时候，例如做一个短的 URL。可以简单地使用基数为 `36` 的数字系统表示：

```javascript
alert((123456).toString(36)) // 2n9c
```

##### 123456..toString(36) == (123456).toString(36)

JavaScript 语法隐含了第一个点之后的部分为小数部分。所以需要第二个点告诉 js 小数部分为空

## 舍入(rounding)

这里有几个对数字进行舍入的内建函数：

- `Math.floor`

  向下舍入：`3.1` 变成 `3`，`-1.1` 变成 `-2`。

- `Math.ceil`

  向上舍入：`3.1` 变成 `4`，`-1.1` 变成 `-1`。

- `Math.round`

  向最近的整数舍入：`3.1` 变成 `3`，`3.6` 变成 `4`，中间值 `3.5` 变成 `4`。

- `Math.trunc`（IE 浏览器不支持这个方法）
  移除小数点后的所有内容而没有舍入：`3.1` 变成 `3`，`-1.1` 变成 `-1`。

#### toFixed(n) ->str

函数 [toFixed(n)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed) 将数字舍入到==小数点后 `n` 位==，并以字符串形式返回结果。
这会向上或向下舍入到最接近的值，类似于 `Math.round`

```javascript
let num = 12.34
alert(num.toFixed(1)) // "12.3"
```

请注意 `toFixed` 的结果是一个==字符串==。如果小数部分比所需要的短，则在结尾添加零.

```javascript
let num = 12.34
alert(num.toFixed(5)) // "12.34000"，在结尾添加了 0，以达到小数点后五位
```

## [不精确的计算](https://zh.javascript.info/number#bu-jing-que-de-ji-suan)

在内部，数字是以 ==64 位==格式 [IEEE-754](http://en.wikipedia.org/wiki/IEEE_754-1985) 表示的，所以正好有 64 位可以存储一个数字：其中 52 位被用于存储这些数字，其中 11 位用于存储小数点的位置（对于整数，它们为零），而 1 位用于符号。

如果一个数字真的很大，则可能会溢出 64 位存储，变成一个特殊的数值 `Infinity`：

```javascript
alert(1e500) // Infinity
```

使用二进制数字系统==无法 **精确** 存储== _0.1_ 或 _0.2_，就像没有办法将三分之一存储为十进制小数一样。

**不仅仅是 JavaScript**

- 许多其他编程语言也存在同样的问题。
  PHP，Java，C，Perl，Ruby 给出的也是完全相同的结果，因为它们基于的是相同的数字格式。

最可靠的方法是借助方法 [toFixed(n)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed) 对结果进行舍入：(最后再通过一元加法转回数字)

```javascript
let sum = 0.1 + 0.2
alert(sum.toFixed(2)) // 0.30
```

因此，乘/除法可以减少误差，但不能完全消除误差。

### **两个零**(0/-0)

数字内部表示的另一个有趣结果是存在两个零：`0` 和 `-0`。

这是因为在存储时，使用一位来存储符号，因此对于包括零在内的任何数字，可以设置这一位或者不设置。

在大多数情况下，这种区别并不明显，因为运算符将它们视为相同的值。

## isFinite 和 isNaN

- `Infinity`（和 `-Infinity`）是一个特殊的数值，比任何数值都大（小）。
- `NaN` 代表一个 error。

它们属于 `number` 类型，但不是“普通”数字，因此，这里有用于检查它们的特殊函数

- `isNaN(value)` 将其参数转换为数字，然后测试它是否为 `NaN`：

- ```javascript
  alert(isNaN(NaN)) // true
  alert(isNaN('str')) // true
  ```

值 "NaN" 是独一无二的，它不等于任何东西，包括它自身：(所以不能用===来判定非数字)

```javascript
alert(NaN === NaN) // false
```

- `isFinite(value)` 将其参数转换为数字，如果是常规数字，则返回 `true`，而不是 `NaN/Infinity/-Infinity`：

  ```javascript
  alert(isFinite('15')) // true
  alert(isFinite('str')) // false，因为是一个特殊的值：NaN
  alert(isFinite(Infinity)) // false，因为是一个特殊的值：Infinity
  ```

有时 `isFinite` 被用于==验证字符串值是否为常规数字==：

```javascript
let num = +prompt('Enter a number', '')

// 结果会是 true，除非你输入的是 Infinity、-Infinity 或不是数字
alert(isFinite(num))
```

请注意，在所有数字函数中，包括 `isFinite`，空字符串或仅有空格的字符串均被视为 `0`。4

#### **与** `Object.is` **进行比较**

1.  它适用于 `NaN`：`Object.is(NaN，NaN) === true`，这是件好事。
2.  值 `0` 和 `-0` 是不同的：`Object.is(0，-0) === false`，从技术上讲这是对的，因为在内部，数字的符号位可能会不同，即使其他所有位均为零。

当内部算法需要比较两个值是否完全相同时，它使用 `Object.is`（内部称为 [SameValue](https://tc39.github.io/ecma262/#sec-samevalue)）。

## [parseInt 和 parseFloat](https://zh.javascript.info/number#parseint-he-parsefloat)

#### 一般用于处理带单位的数字

使用加号 `+` 或 `Number()` 的==数字转换是严格的==。如果一个值不完全是一个数字，就会失败
唯一的例外是字符串开头或结尾的空格，因为它们会被忽略。

```javascript
alert(+'100px') // NaN
```

##### 它们可以从字符串中“读取”数字，直到无法读取为止。

函数 `parseInt` 返回一个整数，而 `parseFloat` 返回一个浮点数

某些情况下，`parseInt/parseFloat` 会返回 `NaN`。当没有数字可读时会发生这种情况：

```javascript
alert(parseInt('a123')) // NaN，第一个符号停止了读取
```

#### **parseInt(str, radix) 的第二个参数** -> 十进制

`parseInt()` 函数具有可选的第二个参数(radix)。它指定了数字系统的基数，因此 `parseInt` 还可以解析十六进制数字、二进制数字等的字符串：

```javascript
alert(parseInt('0xff', 16)) // 255
alert(parseInt('ff', 16)) // 255，没有 0x 仍然有效

alert(parseInt('2n9c', 36)) // 123456
```

**Math.random()**

**Math.max(a, b, c...)**

**Math.min(a, b, c...)**

**Math.pow(n, power)**

`Math` 用于 [`Number`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number) 类型。它不支持 [`BigInt`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/BigInt)。

# String 字符串

字符串的内部格式始终是 [UTF-16](https://en.wikipedia.org/wiki/UTF-16)，它不依赖于页面编码。

单引号和双引号基本相同。但是，反引号允许我们通过 `${…}` 将任何表达式嵌入到字符串中
使用反引号的另一个优点是它们允许字符串跨行

## 特殊字符(转义字符)

以反斜杠字符 `\` 开始

| `\n`                                    | 换行                                                                                                                             |
| --------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `\\`                                    | 反斜线                                                                                                                           |
| `\t`                                    | 制表符                                                                                                                           |
| `\b`, `\f`                              | 退格，换页                                                                                                                       |
| `\xXX`                                  | 具有给定十六进制 Unicode `XX` 的 Unicode 字符，例如：`'\x7A'` 和 `'z'` 相同。                                                    |
| `\uXXXX`                                | 以 UTF-16 编码的十六进制代码 `XXXX` 的 Unicode 字符，例如 `\u00A9` —— 是版权符号 `©` 的 Unicode。它必须正好是 4 个十六进制数字。 |
| `\u{X…XXXXXX}`（1 到 6 个十六进制字符） | 具有给定 UTF-32 编码的 Unicode 符号。一些罕见的字符用两个 Unicode 符号编码，占用 4 个字节。这样我们就可以插入长代码了。          |

## [字符串长度](https://zh.javascript.info/string#zi-fu-chuan-chang-du)

`length` ==属性==表示字符串长度：

```javascript
alert(`My\n`.length) // 3
```

注意 `\n` 是一个单独的“特殊”字符，所以长度确实是 `3`。

#### 我们也可以使用 `for..of` 遍历字符

## 字符串不可更改

想变更只能拼合==新的字符串==

## 改变大小写

[toLowerCase()](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase) 和 [toUpperCase()](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase) 方法可以改变大小写

## str.indexOf / str.lastIndexOf (substr, pos)

找相关字符串的第一个索引

-1 -> 没找到

### \*\*[按位（bitwise）NOT 技巧](https://zh.javascript.info/string#an-wei-bitwisenot-ji-qiao)

- #### 它将数字转换为 32-bit 整数（如果存在小数部分，则删除小数部分），然后对其二进制表示形式中的所有位均取反。

- ~0 == -1 == -(0+1)

- ~-1 == 0 == -(-1+1)

- ```js
  if (str.indexOf('Widget') != -1) {
    alert('We found it') // 现在工作了！
  }
  ```

  因此可以转为

- ```js
  if (~str.indexOf('Widget')) {
    alert('Found it!') // 正常运行
  }
  ```

## str.includes(substr, pos)

#### !!`slice(start, end)`

`substring(start, end)`

`substr(start, length)`

## 字符串的比较

所有的字符串都使用 [UTF-16](https://en.wikipedia.org/wiki/UTF-16) 编码。

#### str.codePointAt(pos)

返回在 `pos` 位置的字符代码 :

```javascript
// 不同的字母有不同的代码
alert('z'.codePointAt(0)) // 122
alert('Z'.codePointAt(0)) // 90
```

#### String.fromCodePoint(code)

通过数字 `code` 创建字符

```javascript
alert(String.fromCodePoint(90)) // Z
```

### 正确的字符串的比较

调用 [str.localeCompare(str2)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare) 会根据==语言规则==返回一个整数，这个整数能指示字符串 `str` 在排序顺序中排在字符串 `str2` 前面、后面、还是相同：

- 如果 `str` 排在 `str2` 前面，则返回负数。
- 如果 `str` 排在 `str2` 后面，则返回正数。
- 如果它们在相同位置，则返回 `0`。

例如：

```javascript
alert('Österreich'.localeCompare('Zealand')) // -1
```

## 代理对

所有常用的字符都是==一个== 2 字节的代码。

所以稀有的符号被称为“代理对”的==一对== 2 字节的符号编码。

获取符号可能会非常麻烦，因为代理对被认为是两个字符

请注意，代理对的各部分没有任何意义。

技术角度来说，代理对也是可以通过它们的代码检测到的：如果一个字符的代码在 `0xd800..0xdbff` 范围内，那么它是代理对的第一部分。下一个字符（第二部分）必须在 `0xdc00..0xdfff` 范围中。(1023\*1023)

#### str.normalize()

为了解决这个问题，有一个 “Unicode 规范化”算法，它将每个字符串都转化成单个“通用”格式。

## 字符串常见问题

字符串查找 .includes()

字符转大小写 .toUpperCase() / .toLowerCase()

字符串过长 .slice()

字符串截取 .slice()

# Array 数组

#### 数组是一种特殊的对象，适用于存储和管理有序的数据项。(有序集合)

#### .at(pos)

更简短的语法 `fruits.at(-1)`：

```javascript
let fruits = ['Apple', 'Orange', 'Plum']

// 与 fruits[fruits.length-1] 相同
alert(fruits.at(-1)) // Plum
```

pop | push 数据结构 ==栈==

- LIFO（Last-In-First-Out），即后进先出法则

shift | push 数据结构 ==队列==

- 与队列相对应的叫做 FIFO（First-In-First-Out），即先进先出。

JavaScript 引擎尝试把这些元素一个接一个地存==储在连续的内存区域==，就像本章的插图显示的一样，而且还有一些其它的优化，以<u>使数组运行得非常快</u>。

## [数组误用]

数组误用的几种方式:

- 添加一个非数字的属性，比如 `arr.test = 5`。
- ==制造空洞==，比如：添加 `arr[0]`，然后添加 `arr[1000]` (它们中间什么都没有)。
- 以==倒序==填充数组，比如 `arr[1000]`，`arr[999]` 等等。

## [性能]

`push/pop` 方法运行的比较快，而 `shift/unshift` 比较慢。

`shift` 操作必须做三件事:

1.  移除索引为 `0` 的元素。
2.  把所有的元素向左移动，把索引 `1` 改成 `0`，`2` 改成 `1` 以此类推，对其重新编号。
3.  更新 `length` 属性。

**数组里的元素越多，移动它们就要花越多的时间，也就意味着越多的内存操作。**

## [循环]

#### for..of

- 不能获取当前元素的索引，只是获取元素值

#### for..in

- 有一些潜在问题存在：

  1.  `for..in` 循环会遍历 **所有属性**，不仅仅是这些数字属性。

      在浏览器和其它环境中有一种称为“类数组”的对象，它们 **看似是数组**。也就是说，它们有 `length` 和索引属性，但是也可能有其它的非数字的属性和方法，这通常是我们不需要的。`for..in` 循环会把它们都列出来。所以如果我们需要处理类数组对象，这些==“额外”的属性==就会存在问题。

  2.  `for..in` 循环适用于普通对象，并且做了对应的优化。但是不适用于数组，因此==速度要慢 10-100 倍==。当然即使是这样也依然非常快。只有在遇到瓶颈时可能会有问题。但是我们仍然应该了解这其中的不同。

  通常来说，我们不应该用 `for..in` 来处理数组。

## [关于 “length”]

length 是最大的数字索引值加一.

length 是可写的

- 如果我们减少它，数组就会被==截断==
- 增加它,不会有特殊的事发生

所以，清空数组最简单的方法就是：`arr.length = 0;`。

## [[多维数组]](https://zh.javascript.info/array#duo-wei-shu-zu)

---

#### .toString

- 会返回以逗号隔开的元素列表

例如：

```javascript
let arr = [1, 2, 3]

alert(arr) // 1,2,3
alert(String(arr) === '1,2,3') // true
```

## [不要使用 == 比较数组]

- 仅当两个对象引用的是同一个对象时，它们才相等 `==`。

- 如果 `==` 左右两个参数之中有一个参数是对象，另一个参数是原始类型，那么该对象将会被转换为原始类型，转换规则如 [对象 — 原始值转换](https://zh.javascript.info/object-toprimitive) 一章所述。
- ……`null` 和 `undefined` 相等 `==`，且各自不等于任何其他的值。

如果我们使用 `==` 来比较数组，除非我们比较的是两个引用同一数组的变量，否则它们永远不相等。

#### 与原始类型的比较也可能会产生看似很奇怪的结果：

```javascript
alert(0 == []) // true

alert('0' == []) // false
```

如 [类型转换](https://zh.javascript.info/type-conversions) 一章所述

```javascript
// 在 [] 被转换为 '' 后
alert(0 == '') // true，因为 '' 被转换成了数字 0

alert('0' == '') // false，没有进一步的类型转换，是不同的字符串
```

很简单，不要使用 `==` 运算符。而是，可以在循环中或者使用下一章中我们将介绍的==迭代方法逐项地比较==

# array 数组方法

- ### [添加/删除元素]

  - `push(...items)` —— 向尾端添加元素，
  - `pop()` —— 从尾端提取一个元素，
  - `shift()` —— 从首端提取一个元素，
  - `unshift(...items)` —— 向首端添加元素，
  - `splice(pos, deleteCount, ...items)` —— 从 `pos` 开始删除 `deleteCount` 个元素，并插入 `items`。
  - `slice(start, end)` —— 创建一个新数组，将从索引 `start` 到索引 `end`（但不包括 `end`）的元素复制进去。
  - `concat(...items)` —— 返回一个新数组：复制当前数组的所有元素，并向其中添加 `items`。如果 `items` 中的任意一项是一个数组，那么就取其元素。

- ### [搜索元素]

  - `indexOf/lastIndexOf(item, pos)` —— 从索引 `pos` 开始搜索 `item`，搜索到则返回该项的索引，否则返回 `-1`。
  - `includes(value)` —— 如果数组有 `value`，则返回 `true`，否则返回 `false`。
  - `find/filter(func)` —— 通过 `func` 过滤元素，返回使 `func` 返回 `true` 的第一个值/所有值。
  - `findIndex` 和 `find` 类似，但返回索引而不是值。

- ### [遍历元素]

  - `forEach(func)` —— 对每个元素都调用 `func`，不返回任何内容。

- ### [转换数组]

  - `map(func)` —— 根据对每个元素调用 `func` 的结果创建一个新数组。
  - `sort(func)` —— 对数组进行原位（in-place）排序，然后返回它。==(a,b)=>a-b==
  - `reverse()` —— 原位（in-place）反转数组，然后返回它。
  - `split/join` —— 将字符串转换为数组并返回。
  - `reduce/reduceRight(func, initial)` —— 通过对每个元素调用 `func` 计算数组上的单个值，并在调用之间传递中间结果。

- ### [其他]

  - `Array.isArray(arr)` 检查 `arr` 是否是一个数组。

请注意，`sort`，`reverse` 和 `splice` 方法修改的是数组本身。

[arr.some(fn)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/some)/[arr.every(fn)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Array/every) 检查数组。

与 `map` 类似，对数组的每个元素调用函数 `fn`。如果任何/所有结果为 `true`，则返回 `true`，否则返回 `false`。

这两个方法的行为类似于 `||` 和 `&&` 运算符：如果 `fn` 返回一个真值，`arr.some()` 立即返回 `true` 并停止迭代其余数组项；如果 `fn` 返回一个假值，`arr.every()` 立即返回 `false` 并停止对其余数组项的迭代。

## 数组常见问题

数组查重 .reduce() ->最好用 Set

对象数组 转 数组数组 .reduce()

数组排序 .sort() (原位)

数组排序新数组 .slice.sort() (先浅拷贝,再排序)

过滤数组(部分留下) .filter()

# Iterable object（可迭代对象）

==可以应用 `for..of` 的对象被称为 **可迭代的**。(可迭代对象)==

- 技术上来说，可迭代对象必须实现 `Symbol.iterator` 方法。
  - `obj[Symbol.iterator]()` 的结果被称为 **迭代器（iterator）**。由它处理进一步的迭代过程。
  - 一个迭代器必须有 `next()` 方法，它返回一个 `{done: Boolean, value: any}` 对象，这里 `done:true` 表明迭代结束，否则 `value` 就是下一个值。
- `Symbol.iterator` 方法会被 `for..of` 自动调用，但我们也可以直接调用它。
- 内建的可迭代对象例如字符串和数组，都实现了 `Symbol.iterator`。
- 字符串迭代器能够识别代理对（surrogate pair）。（译注：代理对也就是 UTF-16 扩展字符。）

==有索引属性和 `length` 属性的对象被称为 **类数组对象**。==这种对象可能还具有其他属性和方法，但是没有数组的内建方法。

如果我们仔细研究一下规范 —— 就会发现大多数内建方法都假设它们需要处理的是可迭代对象或者类数组对象，而不是“真正的”数组，因为这样抽象度更高。

`Array.from(obj[, mapFn, thisArg])` 将可迭代对象或类数组对象 `obj` 转化为真正的数组 `Array`，然后我们就可以对它应用数组的方法。可选参数 `mapFn` 和 `thisArg` 允许我们将函数应用到每个元素。

#### 关键词: 可迭代对象、类数组、Array.from、迭代器

# Map(映射) and Set(集合)

## Map

`Map` —— 是一个带键的数据项的集合。

方法和属性如下：

- `new Map([iterable])` —— 创建 map，可选择带有 `[key,value]` 对的 `iterable`（例如数组）来进行初始化。

- ```js
  let map = new Map([
    [key, value],
    [key, value],
    [key, value],
  ])
  ```

- `map.set(key, value)` —— 根据键存储值，返回 map 自身。

- `map.get(key)` —— 根据键来返回值，如果 `map` 中不存在对应的 `key`，则返回 `undefined`。

- `map.has(key)` —— 如果 `key` 存在则返回 `true`，否则返回 `false`。

- `map.delete(key)` —— 删除指定键对应的值，如果在调用时 `key` 存在，则返回 `true`，否则返回 `false`。

- `map.clear()` —— 清空 map 。

- `map.size` —— 返回当前元素个数。

- `map.keys()` 键的迭代器
- `map.values()` 值的迭代器
- `map.entries()` 是[key,value]的迭代器 (所谓的二维数组)

与普通对象 `Object` 的不同点：

- 任何键、对象都可以作为键。
- 有其他的便捷方法，如 `size` 属性。

#### plain 和 Map 的转换

- plain 对象 => Map 用 Object.entries(obj)转化为键值对的可迭代对象

  - 或者直接将其展开放入数组

  - ```js
    ;[...object] //可迭代对象 同时也是数组
    ```

- Map => plain 对象 用 Obj.fromEntries(Map.entries()) 或直接用 Map 替代

#### map => 的数据结构类似二维数组

```js
;[
  [key, value],
  [key, value],
  [key, value],
]
```

#### 它把键储存在数组[0]中,使得不需要跟 plain 一样都是字符串作键

## Set

`Set` —— 是一组唯一值的集合。

方法和属性：

- `new Set([iterable])` —— 创建 set，可选择带有 `iterable`（例如数组）来进行初始化。
- `set.add(value)` —— 添加一个值（如果 `value` 存在则不做任何修改），返回 set 本身。
- `set.delete(value)` —— 删除值，如果 `value` 在这个方法调用的时候存在则返回 `true` ，否则返回 `false`。
- `set.has(value)` —— 如果 `value` 在 set 中，返回 `true`，否则返回 `false`。
- `set.clear()` —— 清空 set。
- `set.size` —— 元素的个数。
- `set.keys()` 和 `set.values()` 一样都是值的迭代器
- `set.entries()` 是[value,value]的迭代器

在 `Map` 和 `Set` 中迭代总是按照值插入的顺序进行的，所以我们不能说这些集合是无序的，但是我们不能对元素进行重新排序，也不能直接按其编号来获取元素。

set 比普通的 array 的差异在于它是自然去重的,它查重的算法是经过优化的.

#### Set 和 Map 的诞生意味着这两种数据结构在现实生活中有经常用到, 有必要将其深度优化封装使用.

#### 关键词: 新的对象数据结构, 数据项集合(Map), 唯一值集合(Set), 可迭代对象

# WeakMap(弱映射) 和 WeakSet(弱集合)

`WeakMap` 是类似于 `Map` 的集合，它==仅允许对象==作为键，并且一旦通过其他方式无法访问它们，便会将它们与其关联值一同删除。

`WeakSet` 是类似于 `Set` 的集合，它==仅存储对象==，并且一旦通过其他方式无法访问它们，便会将其删除。

它们的主要优点是它们对对象是==弱引用==，所以被它们引用的对象很容易地被垃圾收集器移除。

这是以==不支持== `clear`、`size`、`keys`、`values` 等作为代价换来的…… 即不能迭代, 也没有准确的数量

`WeakMap` 和 `WeakSet` 被用作“主要”对象存储之外的“辅助”数据结构。一旦将对象从主存储器中删除，如果该对象仅被用作 `WeakMap` 或 `WeakSet` 的键，那么它将被==自动清除==。

#### 关键词:仅储存对象, 弱引用, 自动清除, 不可迭代

## [Object.keys，values，entries]

#### 普通的对象也可以提取所有键、值或键值对

但是和 Map 有些不同：

|          | Map          | Object                                  |
| :------- | :----------- | --------------------------------------- |
| 调用语法 | `map.keys()` | `Object.keys(obj)`，而不是 `obj.keys()` |
| 返回值   | 可迭代项     | “真正的”数组                            |

这样更灵活, 你可以避免误用到自己创建的 keys()方法.

这些方法会忽略 symbol, 如果要得到 symbol 的键, 可以用

1.  [Object.getOwnPropertySymbols](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertySymbols)，它会返回一个==只包含 Symbol== 类型的==键==的数组。
2.  [Reflect.ownKeys(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Reflect/ownKeys)，它会返回==**所有**键==。

#### 对象没有数组那么丰富的方法, 想使用==数组的方法== 可以:

1.  先用 Object.entries(obj) => array 转换成数组使用方法
2.  再用 Object.fromEntries(arr) => object 转换为对象数据类型

# 解构赋值

- 解构赋值可以立即将一个对象或数组映射到多个变量上。

- ==解构对象==的完整语法：

- 左侧为 类对象“模式（pattern）

  ```javascript
  let {prop : varName = default, ...rest} = object
  ```

  这表示属性 `prop` 会被赋值给变量 `varName`，如果没有这个属性的话，就会使用默认值 `default`。

  默认值的好处在于减少用户配置难度, 减少失误可能

  没有对应映射的对象属性会被复制到 `rest` 对象。

  #### 函数传参解构

  ```js
  function func({para1:p1=1，para2:p2="c"，}={}){
  	//函数体
  }
  ```

- ==解构数组==的完整语法：

  ```javascript
  let [item1 = default, item2, ...rest] = array
  ```

  数组的第一个元素被赋值给 `item1`，第二个元素被赋值给 `item2`，剩下的所有元素被复制到另一个数组 `rest`。

- 从嵌套数组/对象中提取数据也是可以的，此时等号左侧必须和等号右侧有相同的结构。

- 借用原生 Math 库中的方法 (同样这里也说明可以只取一个属性)

- ```js
  let { random } = Math
  console.log(random()) //[0,1)的随机值
  ```

#### 解构复杂对象

```js
let hd = {
  name:"后盾人"，
  lesson:{
    title:"javascript"
  }
};

let
  name,
  lesson: {title} //相当于把原对象的层级在此次仅用属性名呈现了一变
}=hd;
console.log( title ) //title在此处对应到原对象的title位置
```

#### 忽略使用逗号的元素

数组中不想要的元素也可以通过添加额外的逗号来把它丢弃：

```javascript
// 不需要第二个元素
let [firstName, , title] = [
  'Julius',
  'Caesar',
  'Consul',
  'of the Roman Republic',
]

alert(title) // Consul
```

在上面的代码中，数组的第二个元素被跳过了，第三个元素被赋值给了 `title` 变量，数组中剩下的元素也都被跳过了（因为在这没有对应给它们的变量）。

#### 隐式解构赋值 [.entries()]

方法与解构语法一同使用，来遍历一个对象的“键—值”对：==[key, value]==

```javascript
let user = {
  name: 'John',
  age: 30,
}

// 循环遍历键—值对
for (let [key, value] of Object.entries(user)) {
  alert(`${key}:${value}`) // name:John, then age:30
}
```

#### 关键词:...、函数参数传入、可迭代对象、隐式解构赋值

# Date() 日期和时间

- 在 JavaScript 中，日期和时间使用 [Date](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Date) 对象来表示。我们不能只创建日期，或者只创建时间，`Date` 对象总是同时创建两者。
- `new Date(milliseconds)`
  - `milliseconds` : 毫秒 (与 1970 年 1 月 1 日 UTC+0 毫秒时间后)
- `new Date(datestring)`
  - 如果只有一个参数，并且是字符串，那么它会被自动解析。
- `new Date(year, month, date, hours, minutes, seconds, ms)`
  - 使用当前时区中的给定组件创建日期。只有前两个参数是必须的。
- `year` 必须是四位数
- `month` 从 0 开始计数（对，一月是 0）。
- 一周中的某一天 `getDay()` 同样从 0 开始计算（0 代表星期日）。
- 当设置了超出范围的组件时，`Date` 会进行==自动校准==。这一点对于日/月/小时的加减很有用。
- 日期可以相减，得到的是以毫秒表示的两者的差值。因为当 `Date` 被转换为数字时，`Date` 对象会被转换为时间戳。
- 使用 `Date.now()` 可以==更快地获取当前时间的时间戳==。
- `Date.parse(str)`
  - 字符串的格式应该为：`YYYY-MM-DDTHH:mm:ss.sssZ`
  - `YYYY-MM-DD` —— 日期：年-月-日。
  - 字符 `"T"` 是一个分隔符。
  - `HH:mm:ss.sss` —— 时间：小时，分钟，秒，毫秒。
  - 可选字符 `'Z'` 为 `+-hh:mm` 格式的时区。单个字符 `Z` 代表 UTC+0 时区。

和其他系统不同，JavaScript 中时间戳以毫秒为单位，而不是秒。

有时我们需要==更加精准的时间度量==。JavaScript 自身并没有测量微秒的方法（百万分之一秒），但大多数运行环境会提供。例如：浏览器有 [performance.now()](https://developer.mozilla.org/zh/docs/Web/API/Performance/now) 方法来给出从页面加载开始的以毫秒为单位的微秒数（精确到毫秒的小数点后三位）：

```javascript
alert(`Loading started ${performance.now()}ms ago`)
// 类似于 "Loading started 34731.26000000001ms ago"
// .26 表示的是微秒（260 微秒）
// 小数点后超过 3 位的数字是精度错误，只有前三位数字是正确的
```

Node.js 有 `microtime` 模块以及其他方法。从技术上讲，几乎所有的设备和环境都允许获取更高精度的数值，只是不是通过 `Date` 对象。

#### [设置日期组件](https://zh.javascript.info/date#she-zhi-ri-qi-zu-jian)

#### [访问日期组件](https://zh.javascript.info/date#fang-wen-ri-qi-zu-jian)

#### 关键词：自动校准、Date.now()、new Date()、度量

# JSON 方法，toJSON

- JSON 是一种数据格式，具有自己的独立标准和大多数编程语言的库。
- JSON 支持 object，array，string，number，boolean 和 `null`。
- JavaScript 提供 JSON<->JS 的方法

#### ==序列化==（serialize）成 JSON 的方法 [JSON.stringify](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)

- ```js
  JSON.stringify(obj [,replacer,...], space)
  ```

  `obj`: 转换成 json 的源代码

  `replacer`: 保留的对象属性

  `space`: 制表位空格数

#### 解析 JSON 的方法 [JSON.parse](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)。

- ```js
  JSON.parse(text [, reviver])
  ```

  `text`

  要被解析成 JavaScript 值的字符串，关于 JSON 的语法格式，请参考：[`JSON`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON)。

  `reviver` (可选)

  转换器，如果传入该参数 (函数)，可以用来修改解析生成的原始值，调用时机在 parse 函数返回之前。

这两种方法都支持用于智能读/写的转换函数。

如果一个对象==具有== `toJSON`，那么它会被 `JSON.stringify` 调用。

#### 关键词:JSON 格式, stringify, parse

# 递归和堆栈

术语：

- **递归** 是编程的一个术语，表示从自身调用函数（译注：也就是自调用）。递归函数可用于以更优雅的方式解决问题。

  当一个函数调用自身时，我们称其为 **递归步骤**。递归的 **基础** 是函数参数使任务简单到该函数不再需要进行进一步调用。

- [递归定义](https://en.wikipedia.org/wiki/Recursive_data_type) 的数据结构是指可以使用自身来定义的数据结构。

  例如，链表可以被定义为由对象引用一个列表（或 `null`）而组成的数据结构。

- 像 HTML 元素树或者本章中的 `department` 树等，本质上也是递归：它们有分支，而且分支又可以有其他分支。

  就像我们在示例 `sumSalary` 中看到的那样，可以使用递归函数来遍历它们。

任何递归函数都可以被重写为迭代（译注：也就是循环）形式。有时这是在优化代码时需要做的。但对于大多数任务来说，递归方法足够快，并且容易编写和维护。

#### 关键词:调用自己, 叶子 树枝, 执行上下文 context, 递归结构-链表, 递归深度

#### 递归基础, 递归步骤

# Rest 参数(...)与 Spread 语法(...)

当我们在代码中看到 `"..."` 时，它要么是 rest 参数，要么就是 spread 语法。

有一个简单的方法可以区分它们：

- 若 `...` 出现在函数参数列表的最后，那么它就是 rest 参数，它会把参数列表中剩余的参数收集到一个数组中。
- 若 `...` 出现在函数调用或类似的表达式中，那它就是 spread 语法，它会把一个数组展开为列表。

- `Array.from` 适用于类数组对象也适用于可迭代对象。
- Spread 语法(...)只适用于可迭代对象。(数组,对象...)

```js
let objCopy = { ...obj }
let arrCopy = [...arr]
```

它们俩的出现帮助我们轻松地在列表和参数数组之间来回转换。

“旧式”的 `arguments`（类数组且可迭代的对象）也依然能够帮助我们获取函数调用中的所有参数。

#### 关键词:..., 展开语法, 剩余收集

# 变量作用域，闭包

同一作用域, 使用 `let` 对已存在的变量进行重复声明, 则会出现错误

#### 在变量所在的词法环境中更新变量。

## [垃圾收集](https://zh.javascript.info/closure#la-ji-shou-ji)

通常，函数调用完成后，会将词法环境和其中的所有变量从内存中删除。因为现在没有任何对它们的引用了。与 JavaScript 中的任何其他对象一样，词法环境仅在可达时才会被保留在内存中。

但是，如果有一个嵌套的函数在函数结束后仍可达，则它将具有引用词法环境的 `[[Environment]]` 属性。

在下面这个例子中，即使在（外部）函数执行完成后，它的词法环境仍然可达。因此，此词法环境仍然有效。

例如：

```javascript
function f() {
  let value = 123

  return function () {
    alert(value)
  }
}

let g = f() // g.[[Environment]] 存储了对相应 f() 调用的词法环境的引用
```

#### 理论上当==函数可达时==，它==外部的所有变量==也都将存在。

在实际中，JavaScript 引擎会试图优化它。它们会分析变量的使用情况，如果从代码中可以明显看出有未使用的外部变量，那么就会将其删除。

**在 V8（Chrome，Edge，Opera）中的一个重要的副作用是，此类变量在调试中将不可用。**

#### ! 像 `sum(a)(b) = a+b`

- #### 为了使第二个括号有效，第一个（括号）必须返回一个函数。

#### 从程序执行进入代码块（或函数）的那一刻起，变量就开始进入“未初始化”状态。它一直保持未初始化状态，直至程序执行到相应的 `let` 语句。

#### 变量暂时无法使用的区域（从代码块的开始到 `let`）有时被称为“死区”。

闭包可能会出现内存泄露

当闭包的变量不用时要及时给他赋值为 null, 让它被垃圾处理掉, 减少内存负荷.

```js
let divs document.querySelectorAll("div"); //获取所有的div元素
divs.forEach(function(item){  //遍历每一个div元素
  let desc = item.getAttribute("desc"); //实际用到的变量
  item.addEventListener("click",function()
    console.log(desc);
    console.log(item); //null
  });
  item = null;  //用不到的且占内存的变量 (因为闭包外部变量也包括它)
);
```

#### 关键词: 块级作用域, 全局/局部环境(隐藏属性[[environment]]), 全局/局部变量, 嵌套函数外部环境引用, 死区, 未初始化状态, 闭包, 内部环境, 外部环境

# var(老式变量声明)

`var` 与 `let/const` 有两个主要的区别：

1.  `var` 声明的变量没有块级作用域，它们仅在当前函数内可见，或者全局可见（如果变量是在函数外声明的）。
2.  `var` 变量声明在函数开头就会被处理（脚本启动对应全局变量）。(变量提升 raising/hoisting)
    - 仅有声明被提升, 赋值还留在原处

#### 关键词: 无块级作用域, var

# 全局对象

- 全局对象包含应该在任何位置都可见的变量。

  其中包括 JavaScript 的内建方法，例如 “Array” 和环境特定（environment-specific）的值，例如 `window.innerHeight` — 浏览器中的窗口高度。

- 全局对象有一个通用名称 `globalThis`。

  ……但是更常见的是使用“老式”的环境特定（environment-specific）的名字，例如 `window`（浏览器）和 `global`（Node.js）。

- 仅当值对于我们的项目而言确实是全局的时候，才应将其存储在全局对象中。并保持其数量最少。

- 在浏览器中，除非我们使用 [modules](https://zh.javascript.info/modules)，否则使用 `var` 声明的全局函数和变量会成为全局对象的属性。

- 为了使我们的代码面向未来并更易于理解，我们应该使用直接的方式访问全局对象的属性，如 `window.x`。

#### 关键词: globalThis, var, window, modules

# 函数对象，NFE

函数就是对象。

我们介绍了它们的一些属性：

- `name` —— 函数的名字。通常取自函数定义，但如果函数定义时没设定函数名，JavaScript 会尝试通过函数的上下文猜一个函数名（例如把赋值的变量名取为函数名）。
- `length` —— 函数定义时的入参的个数。Rest 参数不参与计数。

如果函数是通过函数表达式的形式被声明的（不是在主代码流里），并且附带了名字，那么它被称为命名函数表达式 NFE（Named Function Expression）。这个名字可以用于在该函数内部进行自调用，例如递归调用等。

此外，函数可以带有额外的属性。很多知名的 JavaScript 库都充分利用了这个功能。

##### 一个函数本身可以完成一项有用的工作，还可以在自身的属性中附带许多其他功能。

#### !!案例:链式调用函数(操作区分)

```js
function sum(a) {
  sum.sum = a

  function sum(b) {
    sum.sum += b
    return sum
  }

  sum.toString = () => sum.sum

  return sum
}

console.log(sum(6)(-1)(-2)(-3) == 0)
console.log(sum(0)(1)(2)(3)(4)(5) == 15)

// 始终没办法合并数值的初始化和迭代, 这两个动作要分到两个函数区块中调用,
// 不断返回迭代函数本身用作下次调用,
// 最后当结果用作数值对比时(对象-原始类型转换), 调用toString 返回函数的属性sum
```

#### 关键词: NFE(命名函数表达式), 函数的属性和方法, 函数的 length, 链式调用

# "new Function" 语法

语法：

```javascript
let func = new Function([arg1, arg2, ...argN], functionBody)
```

它很少被使用，但有些时候只能选择它。

与我们已知的其他方法相比，这种方法最大的不同在于，它实际上是通过运行时通过参数传递过来的字符串创建的。

使用 `new Function` 创建函数的应用场景非常特殊，比如在复杂的 Web 应用程序中，我们需要从服务器获取代码或者动态地从模板编译函数时才会使用。

##### 闭包

但是如果我们使用 `new Function` 创建一个函数，那么该函数的 `[[Environment]]` 并不指向当前的词法环境，而是指向全局环境。因此，此类函数无法访问外部（outer）变量，只能访问全局变量。

使用 `new Function` 创建的函数，它的 `[[Environment]]` 指向全局词法环境，而不是函数所在的外部词法环境。因此，我们不能在 `new Function` 中直接使用外部变量。不过这样是好事，这有助于降低我们代码出错的可能。并且，从代码架构上讲，显式地使用参数传值是一种更好的方法，并且避免了与使用压缩程序而产生冲突的问题。

#### 关键词: 创建函数,

# 调度：setTimeout 和 setInterval

- `setTimeout(func, delay, ...args)` 和 `setInterval(func, delay, ...args)` 方法允许我们在 `delay` 毫秒之后运行 `func` 一次或以 `delay` 毫秒为时间间隔周期性运行 `func`。
- 要取消函数的执行，我们应该调用 `clearInterval/clearTimeout`，并将 `setInterval/setTimeout` 返回的值作为入参传入。
- 嵌套的 `setTimeout` 比 `setInterval` 用起来更加灵活，允许我们更精确地设置两次执行之间的时间。
- 零延时调度 `setTimeout(func, 0)`（与 `setTimeout(func)` 相同）用来调度需要尽快执行的调用，但是会在当前脚本执行完成后进行调用。
- 浏览器会将 `setTimeout` 或 `setInterval` 的五层或更多层嵌套调用（调用五次之后）的最小延时限制在 4ms。这是历史遗留问题。

请注意，所有的调度方法都不能 **保证** 确切的延时。

例如，浏览器内的计时器可能由于许多原因而变慢：

- CPU 过载。
- 浏览器页签处于后台模式。
- 笔记本电脑用的是电池供电（译注：使用电池供电会以降低性能为代价提升续航）。

所有这些因素，可能会将定时器的最小计时器分辨率（最小延迟）增加到 300ms 甚至 1000ms，具体以浏览器及其设置为准。

#### 关键词: 计时器, 延时, 两种计时器的运作异同, 嵌套 Timeout,

#### 时机型 clearInterval

# 装饰器模式和转发，call/apply

#### 装饰器(decorator) 是一个围绕改变函数行为的包装器。主要工作仍由该函数来完成。

装饰器可以被看作是可以添加到函数的 “features” 或 “aspects”。我们可以添加一个或添加多个。而这一切都无需更改其代码！

为了实现 `cachingDecorator`，我们研究了以下方法：

- [func.call(context, arg1, arg2…)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Function/call) —— 用给定的上下文和参数调用 `func`。
- [func.apply(context, args)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) —— 调用 `func` 将 `context` 作为 `this` 和类数组的 `args` 传递给参数列表。

通用的 **呼叫转移（call forwarding）** 通常是使用 `apply` 完成的

我们也可以看到一个 **方法借用（method borrowing）** 的例子，就是我们从一个对象中获取一个方法，并在另一个对象的上下文中“调用”它。采用数组方法并将它们应用于参数 `arguments` 是很常见的。另一种方法是使用 Rest 参数对象，该对象是一个真正的数组。

funtion.call(obj, para1, para2) 传递一个 this 对象, 和逐个参数

funtion.apply(obj, arg) 传递一个 this 对象, 和一个数组

#### ==均会立即执行==

#### 包装器(wrapper):(函数属性储存, 最后返回函数)

```js
function spy(func) {
  function wrapper(...args) {
    wrapper.calls.push(args)
    return func.apply(this, args)
  }
  wrapper.calls = []
  return wrapper
}
```

#### 计时器:(箭头函数避免涉及错误 this 和 arguments,继续向上查找)

```js
function f(x) {
  console.log(x)
}

function delay(f, x) {
  return function () {
    setTimeout(() => f.apply(this, arguments), x)
  }
}
// create wrappers
let f1000 = delay(f, 1000)
let f1500 = delay(f, 1500)

f1000('test') // 在 1000ms 后显示 "test"
f1500('test') // 在 1500ms 后显示 "test"
```

#### 关键词: call, apply, 装饰器, 包装器, 调用转移, 方法借用,

#### 防抖(一定时间后 输出最后结果), 节流(每隔一定时间 输出结果)

# 函数绑定 bind

方法 `func.bind(context, ...args)` 返回函数 `func` 的“绑定的（bound）变体”，它绑定了上下文 `this` 和第一个参数（如果给定了）。

通常我们应用 `bind` 来绑定对象方法的 `this`，这样我们就可以把它们传递到其他地方使用。例如，传递给 `setTimeout`。

当我们绑定一个现有的函数的某些参数时，绑定后的（不太通用的）函数被称为 **partially applied** 或 **partial**。

`partial` 在装饰器参数中用做固定参数(绑定)(闭包外部环境)

当我们不想一遍又一遍地重复相同的参数时，partial 非常有用。就像我们有一个 `send(from, to)` 函数，并且对于我们的任务来说，`from` 应该总是一样的，那么我们就可以搞一个 partial 并使用它。

#### 关键词: bind(绑定 this 和固定参数), partial(偏函数),

#### 包装器(提供外部环境->有 this 的环境)

apply / call / bind 一般用于调用函数时, 函数中用到了 this, 需要==配置正确的动态的 this==时

# 深入理解箭头函数

箭头函数：

- 没有 `this`
- 没有 `arguments`
- 不能使用 `new` 进行调用
- 它们也没有 `super`，但目前我们还没有学到它。我们将在 [类继承](https://zh.javascript.info/class-inheritance) 一章中学习它。

这是因为，箭头函数是针对那些没有自己的“上下文”，但在==当前上下文中起作用的短代码的==。并且箭头函数确实在这种使用场景中大放异彩。

#### 关键词: 没有 this 和 argument, 不能 new, 简化传递 this

# 属性标志和属性描述符

对象属性（properties），除 **`value`** 外，
还有三个特殊的特性（attributes），也就是所谓的“标志”：

- #### 只读 (false)

  - **`writable`** — 如果为 `true`，则值可以被修改，否则它是只可读的。

- #### 不可枚举 (false)

  - **`enumerable`** — 如果为 `true`，则会被在循环中列出，否则不会被列出。

- #### 不可配置 (删除,修改标志) (false)

  - **`configurable`** — 如果为 `true`，则此属性可以被删除，这些特性也可以被修改，否则不可以。
  - 请注意：`configurable: false` 防止更改和删除属性标志，但是允许更改对象的值。

为了修改标志，我们可以使用 `Object.defineProperty`。
==(定义(没有就创建)一个属性的标志符)==

有一个方法 `Object.defineProperties(obj, descriptors)`，允许一次定义多个属性。

获取==一个属性的描述符==

`Object.getOwnPropertyDescriptor(obj,key)` 方法。

要一次获取==所有属性描述符==，我们可以使用 `Object.getOwnPropertyDescriptors(obj)` 方法。

- 它与 `Object.defineProperties` 一起可以用作克隆对象的“标志感知”方式：

- ```javascript
  let clone = Object.defineProperties({}, Object.getOwnPropertyDescriptors(obj))
  ```

- 通常，当我们克隆一个对象时，我们使用赋值的方式来复制属性，像这样：

- ```javascript
  for (let key in user) {
    clone[key] = user[key]
  }
  ```

### 设定一个全局的密封对象

属性描述符在单个属性的级别上工作。

还有一些限制访问 **整个** 对象的方法：

- [Object.preventExtensions(obj)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions)

  ==(禁止添加)== 禁止向对象添加新属性。

- [Object.seal(obj)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/seal)

  ==(封闭)== 禁止添加/删除属性。为所有现有的属性设置 `configurable: false`。

- [Object.freeze(obj)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)

  ==(冻结)== 禁止添加/删除/更改属性。为所有现有的属性设置 `configurable: false, writable: false`。

还有针对它们的测试：

- [Object.isExtensible(obj)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/isExtensible)

  如果添加属性被禁止，则返回 `false`，否则返回 `true`。

- [Object.isSealed(obj)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/isSealed)

  如果添加/删除属性被禁止，并且所有现有的属性都具有 `configurable: false`则返回 `true`。

- [Object.isFrozen(obj)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/isFrozen)

  如果添加/删除/更改属性被禁止，并且所有当前属性都是 `configurable: false, writable: false`，则返回 `true`。

# 属性的 getter 和 setter

==有两种类型的对象属性。==

第一种是 **数据属性**。我们已经知道如何使用它们了。到目前为止，我们使用过的所有属性都是数据属性。

第二种类型的属性是新东西。它是 **访问器属性（accessor property）**。它们本质上是用于获取和设置值的函数，但从外部代码来看就像常规属性。

在对象字面量中，它们用 `get` 和 `set` 表示

我们不以函数的方式 **调用** `user.fullName`，我们正常 **读取** 它：getter 在幕后运行。

访问器==优先级高于==数据属性

## 访问器描述符

访问器属性的描述符与数据属性的不同。

对于访问器属性，没有 `value` 和 `writable`，但是有 `get` 和 `set` 函数。

所以访问器描述符可能有：

- **`get`** —— 一个没有参数的函数，在读取属性时工作，
- **`set`** —— 带有一个参数的函数，当属性被设置时调用，
- **`enumerable`** —— 与数据属性的相同，
- **`configurable`** —— 与数据属性的相同。

一个属性要么是访问器（具有 `get/set` 方法），要么是数据属性（具有 `value`），但不能两者都是。

==一个众所周知的约定，即以下划线 `"_"` 开头的属性是内部属性，不应该从对象外部进行访问。==

#### 关键词: getter(自计算值), setter(宏设置值)

# 原型继承(Prototypal inheritance)

继承是原型的继承，而不是改变构造函数的原型
保留原始构造函数原型的方法, 且再向上继承其他构造函数原型的方法
`__proto__` **是** `[[Prototype]]` **的因历史原因而留下来的 getter/setter**

**无论在哪里找到方法：在一个对象还是在原型中。在一个方法调用中，`this` 始终是点符号 `.` 前面的对象。**

`for..in` 循环也会迭代继承的属性。

**几乎所有其他键/值获取方法都忽略继承的属性**

- 在 JavaScript 中，所有的对象都有一个隐藏的 `[[Prototype]]` 属性，它要么是另一个对象，要么就是 `null`。
- 我们可以使用 `obj.__proto__` 访问它（历史遗留下来的 getter/setter，这儿还有其他方法，很快我们就会讲到）。
- 通过 `[[Prototype]]` 引用的对象被称为“原型”。
- 如果我们想要读取 `obj` 的一个属性或者调用一个方法，并且它不存在，那么 JavaScript 就会尝试在原型中查找它。
- 写/删除操作直接在对象上进行，它们不使用原型（假设它是数据属性，不是 setter）。
- 如果我们调用 `obj.method()`，而且 `method` 是从原型中获取的，`this` 仍然会引用 `obj`。因此，方法始终与当前对象一起使用，即使方法是继承的。
- `for..in` 循环在其自身和继承的属性上进行迭代。所有其他的键/值获取方法仅对对象本身起作用。

#### in 检测属性是否在对象的原型链中

此处即为 常见的 for...in 中的 i

```js
console.log('prop' in obj)
```

#### hasOwnProperty 检测属性是否在对象中

```js
console.log(obj.hasOwnProperty('prop'))
```

#### 关键词: [[Prototype]], `__proto__`, null, 原型, 继承

#### (向上查询,原位执行)

# F.prototype

在本章中，我们简要介绍了为通过构造函数创建的对象设置 `[[Prototype]]` 的方法。稍后我们将看到更多依赖于此的高级编程模式。

一切都很简单，只需要记住几条重点就可以清晰地掌握了：

- `F.prototype` 属性（不要把它与 `[[Prototype]]` 弄混了）在 `new F` 被调用时为新对象的 `[[Prototype]]` 赋值。
- `F.prototype` 的值要么是一个对象，要么就是 `null`：其他值都不起作用。
- `"prototype"` 属性仅在设置了一个构造函数（constructor function），并通过 `new` 调用时，才具有这种特殊的影响。

在常规对象上，`prototype` 没什么特别的

默认情况下，所有函数都有 `F.prototype = {constructor：F}`，所以我们可以通过访问它的 `"constructor"` 属性来获取一个对象的构造器。

#### 关键词: 构造函数 constructor, 原型指向 F.prototype,

# 原生的原型

#### [从原型中借用]

obj.join = Array.prototype.join;
或者 obj.join = [].join;

#### [总结]

所有的内建对象都遵循相同的模式（pattern）：

- 方法都存储在 prototype 中（`Array.prototype`、`Object.prototype`、`Date.prototype` 等）。
- 对象本身只存储数据（数组元素、对象属性、日期）。

原始数据类型==也将方法存储在包装器对象的 prototype 中==：`Number.prototype`、`String.prototype` 和 `Boolean.prototype`。只有 `undefined` 和 `null` 没有包装器对象。

内建原型可以被修改或被用新的方法填充。但是不建议更改它们。唯一允许的情况可能是，当我们添加一个还没有被 JavaScript 引擎支持，但已经被加入 JavaScript 规范的新标准时，才可能允许这样做。

#### 关键词: 方法借用, 原始数据类型方法, 内建原型修改

# 原型方法，没有 **proto** 的对象

设置和直接访问原型的现代方法有：

- [Object.create(proto, descriptors)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/create) —— 利用给定的 `proto` 作为 `[[Prototype]]`（可以是 `null`）和可选的属性描述来创建一个空对象。
- [Object.getPrototypeOf(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf) —— 返回对象 `obj` 的 `[[Prototype]]`（与 `__proto__` 的 getter 相同）。
- [Object.setPrototypeOf(obj, proto)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf) —— 将对象 `obj` 的 `[[Prototype]]` 设置为 `proto`（与 `__proto__` 的 setter 相同）。

虽然还有浏览器非标开发的.**proto**也可以读写原型,但是
如果要将一个用户生成的键放入一个对象，那么内建的 `__proto__` getter/setter 是不安全的。因为用户可能会输入 `"__proto__"` 作为键，这会导致一个 error，虽然我们希望这个问题不会造成什么大影响，但通常会造成不可预料的后果。

因此，我们可以使用 `Object.create(null)` 创建一个没有 `__proto__` 的 “very plain” 对象，或者对此类场景坚持使用 `Map` 对象就可以了。

此外，`Object.create` 提供了一种简单的方式来浅拷贝一个对象的所有描述符：

```javascript
let clone = Object.create(
  Object.getPrototypeOf(obj),
  Object.getOwnPropertyDescriptors(obj)
)
```

此外，我们还明确了 `__proto__` 是 `[[Prototype]]` 的 getter/setter，就像其他方法一样，它位于 `Object.prototype`。

我们可以通过 `Object.create(null)` 来创建没有原型的对象。这样的对象被用作 “pure dictionaries”，对于它们而言，使用 `"__proto__"` 作为键是没有问题的。

其他方法：

- [Object.keys(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) / [Object.values(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/values) / [Object.entries(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/entries) —— 返回一个可枚举的由自身的字符串属性名/值/键值对组成的数组。
- [Object.getOwnPropertySymbols(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertySymbols) —— 返回一个由自身所有的 symbol 类型的键组成的数组。
- [Object.getOwnPropertyNames(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyNames) —— 返回一个由自身所有的字符串键组成的数组。
- [Reflect.ownKeys(obj)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Reflect/ownKeys) —— 返回一个由自身所有键组成的数组。
- [obj.hasOwnProperty(key)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)：如果 `obj` 拥有名为 `key` 的自身的属性（非继承而来的），则返回 `true`。

所有返回对象属性的方法（如 `Object.keys` 及其他）—— 都返回“自身”的属性。如果我们想继承它们，我们可以使用 `for...in`。

# 类

# Class 基本语法

基本的类语法看起来像这样：

```javascript
class MyClass {
  prop = value; // 属性

  constructor(...) { // 构造器
    // ...
  }

  method(...) {} // method

  get something(...) {} // getter 方法
  set something(...) {} // setter 方法

  [Symbol.iterator]() {} // 有计算名称（computed name）的方法（此处为 symbol）
  // ...
}
```

技术上来说，`MyClass` 是一个函数（我们提供作为 `constructor` 的那个），而 methods、getters 和 settors 都被写入了 `MyClass.prototype`。

#### [Class 字段]

“类字段”是一种允许添加任何属性的语法。

例如，让我们在 `class User` 中添加一个 `name` 属性：

```javascript
class User {
  name = "John";
```

所以，我们就只需在表达式中写 " = "，就这样。

类字段重要的不同之处在于，它们会在==每个独立对象中被设好==，而不是设在 `User.prototype`：

```javascript
class User {
  name = 'John'
}

let user = new User()
alert(user.name) // John
alert(User.prototype.name) // undefined
```

#### [使用类字段制作绑定方法]

我们在 [函数绑定](https://zh.javascript.info/bind) 一章中讲过，有两种可以修复它的方式：

1.  传递一个包装函数，例如 `setTimeout(() => button.click(), 1000)`。
2.  将方法绑定到对象，例如在 constructor 中。

类字段提供了另一种非常优雅的语法：

```javascript
class Button {
  constructor(value) {
    this.value = value
  }
  click = () => {
    alert(this.value)
  }
}

let button = new Button('hello')

setTimeout(button.click, 1000) // hello
```

类字段 `click = () => {...}` 是基于每一个对象被创建的，在这里对于每一个 `Button` 对象==都有一个独立的方法==，在内部都有一个指向此对象的 `this`。我们可以把 `button.click` 传递到任何地方，而且 `this` 的值总是正确的。

#### 类其实就是把属性和方法写到原型中去,然后实例化一个对应的对象, 相当于把构造函数和其指向的原型同时创建。(把构造函数的参数接收回退到内部的 constructor 方法中)

# 类继承

#### super = this._proto_

1.  想要扩展一个类：`class Child extends Parent` :
    - 这意味着 `Child.prototype.__proto__` 将是 `Parent.prototype`，所以方法会被继承。
2.  重写一个 constructor：
    - 在使用 `this` 之前，我们必须在 `Child` 的 constructor 中将父 constructor 调用为 `super()`。
3.  重写一个方法：
    - 我们可以在一个 `Child` 方法中使用 `super.method()` 来调用 `Parent` 方法。
4.  内部：
    - 方法在内部的 `[[HomeObject]]` 属性中记住了它们的类/对象。这就是 `super` 如何解析父方法的。
    - 因此，将一个带有 `super` 的方法从一个对象复制到另一个对象是不安全的。

补充：

- 箭头函数没有自己的 `this` 或 `super`，所以它们能融入到就近的上下文中，像透明似的。

# 静态属性和静态方法

静态属性和方法是设置在函数对象中的, 支持继承.

静态方法被用于实现属于整个类的功能。它与具体的类实例无关。

举个例子， 一个用于进行比较的方法 `Article.compare(article1, article2)` 或一个工厂（factory）方法 `Article.createTodays()`。

在类生命中，它们都被用关键字 `static` 进行了标记。

静态属性被用于当我们想要==存储类级别的数据==时，而不是绑定到实例。

语法如下所示：

```javascript
class MyClass {
  static property = ...;

  static method() {
    ...
  }
}
```

从技术上讲，静态声明与直接给类本身赋值相同：

```javascript
MyClass.property = ...
MyClass.method = ...
```

静态属性和方法是可被继承的。

静态方法需要类来调用. 就跟(`Object.keys()`类似)

对于 `class B extends A`，类 `B` 的 prototype 指向了 `A`：`B.[[Prototype]] = A`。因此，如果一个字段在 `B` 中没有找到，会继续在 `A` 中查找。

#### 关键词: 静态方法, Class 专属的方法(调用需 this 为 Class 本身),

#### 双原型继承(静态/常规)

# 私有的和受保护的属性和方法

就面向对象编程（OOP）而言，内部接口与外部接口的划分被称为 [封装](<https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)>)。

它具有以下优点：

保护用户，使他们不会误伤自己

- 如果一个 class 的使用者想要改变那些本不打算被从外部更改的东西 —— 后果是不可预测的。

可支持性

- 编程的情况比现实生活中的咖啡机要复杂得多，因为我们不只是购买一次。我们还需要不断开发和改进代码。
- **如果我们严格界定内部接口，那么这个 class 的开发人员可以自由地更改其内部属性和方法，甚至无需通知用户。**
- 如果你是这样的 class 的开发者，那么你会很高兴知道可以安全地重命名私有变量，可以更改甚至删除其参数，因为没有外部代码依赖于它们。
- 对于用户来说，当新版本问世时，应用的内部可能被进行了全面检修，但如果外部接口相同，则仍然很容易升级。

隐藏复杂性

- 人们喜欢使用简单的东西。至少从外部来看是这样。内部的东西则是另外一回事了。程序员也不例外。**当实施细节被隐藏，并提供了简单且有据可查的外部接口时，总是很方便的。**

为了隐藏内部接口，我们使用受保护的或私有的属性：

- 受保护的字段以 `_` 开头。这是一个众所周知的约定，不是在语言级别强制执行的。程序员应该只通过它的类和从它继承的类中访问以 `_` 开头的字段。
- ==私有字段==以 `#` 开头。JavaScript 确保我们只能从类的内部访问它们。且子类无法访问.

#### 关键词: 私有字段#, 受保护字段\_,

# 扩展内建类

内建对象有它们自己的静态方法，例如 `Object.keys`，`Array.isArray` 等。

如我们所知道的，原生的类互相扩展。例如，`Array` 扩展自 `Object`。

内建类却是一个例外。它们相互间不继承静态方法。

例如，`Array` 和 `Date` 都继承自 `Object`，所以它们的实例都有来自 `Object.prototype` 的方法。但 `Array.[[Prototype]]` 并不指向 `Object`，所以它们没有例如 `Array.keys()`（或 `Date.keys()`）这些静态方法。

这里有一张 `Date` 和 `Object` 的结构关系图：

<img src="./assets/Js 进阶.assets/image-20220523112819787.png" alt="image-20220523112819787" style="zoom: 50%;" />

正如你所看到的，`Date` 和 `Object` 之间没有连结。它们是独立的，只有 `Date.prototype` 继承自 `Object.prototype`，仅此而已。

与我们所了解的通过 `extends` 获得的继承相比，这是内建对象之间继承的一个重要区别。

#### 关键词: 内建类,

# 类检查："instanceof"

让我们总结一下我们知道的==类型检查方法==：

|                 | 用于                                                         | 返回值     |
| :-------------- | :----------------------------------------------------------- | :--------- |
| `typeof`        | 原始数据类型                                                 | string     |
| `{}.toString`   | 原始数据类型，内建对象，包含 `Symbol.toStringTag` 属性的对象 | string     |
| `instanceof`    | 对象                                                         | true/false |
| `isPrototypeof` | 对象                                                         | true/false |

instanceof 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上。

```Js
// console.log( object instanceof constructor ); 即
console.log( object.__proto__ instanceof Func.prototype );

// console.log( prototypeObj.isPrototypeOf(object) );即
console.log( Func.prototype.isPrototypeOf(object) );

```

正如我们所看到的，从技术上讲，`{}.toString` 是一种“更高级的” `typeof`。

当我们使用类的层次结构（hierarchy），并想要对该类进行检查，同时还要考虑继承时，这种场景下 `instanceof` 操作符确实很出色。

根据 `instanceof` 的逻辑，真正决定类型的是 `prototype`，而不是构造函数。

#### 关键词: 类检查, typeof, {}.toString.call(obj), instanceof

# Mixin 模式

_Mixin_ — 是一个==通用的面向对象编程术语==：一个包含其他类的方法的类。

一些其它编程语言允许多重继承。JavaScript 不支持多重继承，但是可以通过将方法拷贝到原型中来实现 mixin。

我们可以使用 mixin 作为一种通过添加多种行为（例如上文中所提到的事件处理）来扩充类的方法。

一般用 assign 来组合(浅拷贝)对象,让几个有必要方法的对象组合起来.

如果 Mixins 意外覆盖了现有类的方法，那么它们可能会成为一个冲突点。因此，通常应该仔细考虑 mixin 的命名方法，以最大程度地降低发生这种冲突的可能性。

#### 关键词: 扩充类方法, 单原型, assign,

# 错误处理，"try...catch"

`try...catch` 结构允许我们处理执行过程中出现的 error。从字面上看，它允许“尝试”运行代码并“捕获”其中可能发生的错误。

语法如下：

```javascript
try {
  // 执行此处代码
} catch (err) {
  // 如果发生错误，跳转至此处
  // err 是一个 error 对象
} finally {
  // 无论怎样都会在 try/catch 之后执行
}
```

这儿可能会没有 `catch` 部分或者没有 `finally`，所以 `try...catch` 或 `try...finally` 都是可用的。

Error 对象包含下列属性：

- `message` — 人类可读的 error 信息。
- `name` — 具有 error 名称的字符串（Error 构造器的名称）。
- `stack`（没有标准，但得到了很好的支持）— Error 发生时的调用栈。

如果我们不需要 error 对象，我们可以通过使用 `catch {` 而不是 `catch (err) {` 来省略它。

我们也可以使用 `throw` 操作符来生成自定义的 error。从技术上讲，`throw` 的参数可以是任何东西，但通常是继承自内建的 `Error` 类的 error 对象。下一章我们会详细介绍扩展 error。

再次抛出（==rethrowing==）是一种错误处理的重要模式：`catch` 块通常期望并知道如何处理特定的 error 类型，因此它应该再次抛出它不知道的 error。

```js
...
throw error
...
```

即使我们没有 `try...catch`，大多数执行环境也允许我们设置“全局”错误处理程序来捕获“掉出（fall out）”的 error。在浏览器中，就是 `window.onerror`。

#### 关键词: try-catch-finally, 错误也执行

# 自定义 Error，扩展 Error

我们可以正常地从 `Error` 和其他内建的 error 类中进行继承，。我们只需要注意 `name` 属性以及不要忘了调用 `super`。

我们可以使用 `instanceof` 来检查特定的 error。但有时我们有来自第三方库的 error 对象，并且在这儿没有简单的方法来获取它的类。那么可以==将 `name` 属性用于这一类的检查==。

包装异常是一项广泛应用的技术：用于处理低级别异常并创建高级别 error 而不是各种低级别 error 的函数。在上面的示例中，低级别异常有时会成为该对象的属性，例如 `err.cause`，但这不是严格要求的。

### 关键词: super, 包装异常(异常组合),

# 简介：回调

计划 **异步** 行为

这被称为“基于回调”的异步编程风格。异步执行某项功能的函数应该提供一个 `callback` 参数用于在相应事件完成时调用。

名为 `step*` 的函数都是一次性使用的，创建它们就是为了避免“回调地狱”。没有人会在行为链之外重用它们。

#### 关键词: 回调地狱, 异步行为

# Promise

promise 是==维持一个 executor 状态的对象==, 它包装一个 executor 指示并保存它的状态, 提供后面的 handler 以指示.

executor(生产者代码)

```js
let promise = new Promise(function (resolve, reject) {
  // executor（生产者代码，“歌手”）
})
```

当 executor 获得了结果，无论是早还是晚都没关系，它应该==调用以下回调之一==：

- `resolve(value)` —— 如果任务成功完成并带有结果 `value`。
- `reject(error)` —— 如果出现了 error，`error` 即为 error 对象。
- ==只有第一次==对 `reject/resolve` 的调用才会被处理。
-

由 `new Promise` 构造器返回的 `promise` 对象具有以下内部属性：

- `state(状态)` —— 最初是 `"pending"`，然后在 `resolve` 被调用时变为 `"fulfilled"`，或者在 `reject` 被调用时变为 `"rejected"`。
- `result(结果)` —— 最初是 `undefined`，然后在 `resolve(value)` 被调用时变为 `value`，或者在 `reject(error)` 被调用时变为 `error`。

所以，executor 最终将 `promise` 移至以下状态之一：

- `{status:"fulfilled", value:result}` 对于成功的响应，
- `{status:"rejected", reason:error}` 对于 error。

<img src="./assets/Js 进阶.assets/image-20220524234413726.png" alt="image-20220524234413726" style="zoom:50%;" />

#### [then，catch，finally]

#### `.then`

语法如下：

```javascript
promise.then(
  function (result) {
    /* handle a successful result */
  },
  function (error) {
    /* handle an error */
  }
)
```

如果我们==只对成功完成的情况感兴趣==，那么我们可以只为 `.then` 提供一个函数参数

如果我们==只对 error 感兴趣==，那么我们可以使用 `null` 作为第一个参数：`.then(null, errorHandlingFunction)`。

==处理 error 记得在判定在 reject 的时候 new 一个 error 给 result.==

#### `.catch`

`.catch(f)` 调用是 `.then(null, f)` 的完全的模拟，它只是一个简写形式。

#### `finally`

1.  `finally` 处理程序（handler）没有参数。在 `finally` 中，我们不知道 promise 是否成功。没关系，因为我们的任务通常是执行“常规”的定稿程序（finalizing procedures）。
2.  `finally` 处理程序将结果和 error 传递给下一个处理程序。

Promise 很灵活。我们可以随时添加处理程序（handler）：==如果结果已经在了，它们就会执行==。

#### 我们立刻就能发现 promise 相较于基于回调的模式的一些好处：

| Promises                                                                                                                                                                                                           | Callbacks                                                                                                                                                            |
| :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Promises 允许我们按照自然顺序进行编码。首先，我们运行 `loadScript` 和 `.then` 来处理结果。                                                                                                                         | 在调用 `loadScript(script, callback)` 时，在我们处理的地方（disposal）必须有一个 `callback` 函数。换句话说，在调用 `loadScript` **之前**，我们必须知道如何处理结果。 |
| 我们可以根据需要，在 promise 上多次调用 `.then`。每次调用，我们都会在“订阅列表”中添加一个新的“分析”，一个新的订阅函数。在下一章将对此内容进行详细介绍：[Promise 链](https://zh.javascript.info/promise-chaining)。 | 只能有一个回调。                                                                                                                                                     |

#### 关键词: .then/.catch/.finally, promise, state, result

# Promise 链

如果 `.then`（或 `catch/finally` 都可以）处理程序（handler）返回一个 promise，那么链的其余部分将会等待，直到它状态变为 settled。当它被 settled 后，其 result（或 error）将被进一步传递下去。

这是一个完整的流程图：

<img src="./assets/Js 进阶.assets/image-20220525212529588.png" alt="image-20220525212529588" style="zoom:50%;" />

#### `fetch`

我们将使用 [fetch](https://zh.javascript.info/fetch) 方法从远程服务器加载用户信息。

```javascript
let promise = fetch(url)
```

第三方库通过添加.then()方法来将类变得`Thenables`, 它会被当做一个 promise 来对待。

#### 关键词: 链式 promise

# 使用 promise 进行错误处理

`.catch` 处理 promise 中的各种 error：在 `reject()` 调用中的，或者在处理程序（handler）中抛出的（thrown）error。

我们应该将 `.catch` 准确地放到我们想要处理 error，并知道如何处理这些 error 的地方。处理程序应该分析 error（可以自定义 error 类来帮助分析）并再次抛出未知的 error（可能它们是编程错误）。

如果没有办法从 error 中恢复的话，不使用 `.catch` 也可以。

在任何情况下我们都应该有 `unhandledrejection` 事件处理程序（用于浏览器，以及其他环境的模拟），以跟踪未处理的 error 并告知用户（可能还有我们的服务器）有关信息，以使我们的应用程序永远不会“死掉”。

检查具有 HTTP 状态的 `response.status` 属性

如果我们有加载指示（load-indication），`.finally` 是一个很好的处理程序（handler），在 fetch 完成时停止它

#### 关键词: fetch, rejection, unhandledrejection(未处理错误)

# Promise API

`Promise` 类有 6 种静态方法：

1.  `Promise.all(promises)` —— 等待所有 promise 都 resolve 时，==返回存放它们结果的数组==。如果给定的任意一个 promise 为 reject，那么它就会变成 `Promise.all` 的 error，所有其他 promise 的结果都会被忽略。

2.  `Promise.allSettled(promises)`

    （ES2020 新增方法）—— 等待所有 promise 都 settle 时，并以包含以下内容的对象数组的形式返回它们的结果：

    - `status`: `"fulfilled"` 或 `"rejected"`
    - `value`（如果 fulfilled）或 `reason`（如果 rejected）。

3.  `Promise.race(promises)` —— ==等待第一个 settle 的 promise==，并将其 result/error 作为结果返回。

4.  `Promise.any(promises)`（ES2021 新增方法）—— ==等待第一个 fulfilled== 的 promise，并将其结果作为结果返回。如果所有 promise 都 rejected，`Promise.any` 则会抛出 [`AggregateError`](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/AggregateError) 错误类型的 error 实例。

5.  `Promise.resolve(value)` —— 使用给定 value 创建一个 resolved 的 promise。

6.  `Promise.reject(error)` —— 使用给定 error 创建一个 rejected 的 promise。

以上所有方法，`Promise.all` 可能是在实战中使用最多的。

#### 关键词: all, allSettled, race, any

# Promisification

Promisification 将一个接受回调的函数转换为一个返回 promise 的函数。

==promisify 即指 promise 化==

请记住，一个 promise 可能只有一个结果，但从技术上讲，一个回调可能被调用很多次。

因此，promisification 仅适用于调用一次回调的函数。进一步的调用将被忽略。

#### 关键词: promisify 包装->.then 可以承接

# 微任务（Microtask）

Promise 的处理程序（handlers）`.then`、`.catch` 和 `.finally` ==都是异步的==。

#### [==微任务队列==（Microtask queue）](https://zh.javascript.info/microtask-queue#wei-ren-wu-dui-lie-microtaskqueue)

异步任务需要适当的管理。为此，ECMA 标准规定了一个内部队列 `PromiseJobs`，通常被称为“微任务队列（microtask queue）”（V8 术语）。

如 [规范](https://tc39.github.io/ecma262/#sec-jobs-and-job-queues) 中所述：

- 队列（queue）是==先进先出==的：首先进入队列的任务会首先运行。
- 只有在 JavaScript ==引擎中没有其它任务在运行时==，才开始执行任务队列中的任务。

当 JavaScript 引擎执行完当前的代码，它会从队列中获取任务并执行它。

Promise 处理始终是异步的，因为所有 promise 行为都会通过内部的 “promise jobs” 队列，也被称为“微任务队列”（V8 术语）。

因此，`.then/catch/finally` 处理程序（handler）总是在当前代码完成后才会被调用。

如果我们需要确保一段代码在 `.then/catch/finally` 之后被执行，我们可以将它添加到链式调用的 `.then` 中。

在大多数 JavaScript 引擎中（包括浏览器和 Node.js），微任务（microtask）的概念与“事件循环（event loop）”和“宏任务（macrotasks）”紧密相关。

#### 关键词: 队列, 微队列, 先进先出

# Async/await

函数前面的关键字 `async` 有两个作用：(异步函数)

1.  让这个函数总是返回一个 promise。
2.  允许在该函数内使用 `await`。

Promise 前的关键字 `await` 使 JavaScript 引擎等待该 promise settle，然后：

1.  如果有 error，就会抛出异常 —— 就像那里调用了 `throw error` 一样。
2.  否则，就返回结果。
3.  在此期间它会==阻塞==，延迟执行 await 语句后面的语句。

这两个关键字一起提供了一个很好的用来编写异步代码的框架，这种代码易于阅读也易于编写。

有了 `async/await` 之后，我们就几乎不需要使用 `promise.then/catch`，但是不要忘了它们是基于 promise 的，因为有些时候（例如在最外层作用域）我们不得不使用这些方法。并且，当我们需要同时等待需要任务时，`Promise.all` 是很好用的。

#### 关键词: Async 异步, await 等待

# Generator

#### Generator 生成器

- `Generator ` 是通过 `generator ` 函数 `function* f(…) {…}` 创建的。
- 在 `generator`（仅在）内部，存在 `yield` 操作。
- 外部代码和 `generator` 可能会通过 `next/yield` 调用交换结果。

#### [next]

`next()` 的结果始终是一个具有两个属性的对象：

- `value`: 产出的（yielded）的值。
- `done`: 如果 generator 函数已执行完成则为 `true`，否则为 `false`。

#### [...]

因为 `generator` 是可迭代的，我们可以使用 iterator 的所有相关功能，
例如：spread 语法 `...`

#### [Generator 组合]

`yield*` 指令将执行 **委托** 给另一个 generator。这个术语意味着 `yield* gen` 在 generator `gen` 上进行迭代，并将其产出（yield）的值透明地（transparently）转发到外部。就好像这些值就是由外部的 generator yield 的一样。

Generator 组合（composition）是将一个 generator 流插入到另一个 generator 流的自然的方式。它==不需要使用额外的内存来存储中间结果==。

#### [“yield” 是一条双向路]

调用 `generator.next(arg)`，我们就能将参数 `arg` 传递到 generator 内部。这个 `arg` 参数会变成==这次== `yield` 的结果。并同时要到==下一个==`yield`的结果。

<img src="./assets/Js 进阶.assets/image-20220527222044573.png" alt="image-20220527222044573" style="zoom:50%;" />

#### [generator.throw]

要向 `yield` 传递一个 error，我们应该调用 `generator.throw(err)`。在这种情况下，`err` 将被抛到对应的 `yield` 所在的那一行。

#### [generator.return]

提前终止产出数据流, `generator.return(value)` 完成 generator 的执行并返回给定的 `value`。

在现代 JavaScript 中，`generator` 很少被使用。但有时它们会派上用场，因为函数在执行过程中与调用代码交换数据的能力是非常独特的。而且，当然，它们==非常适合创建可迭代对象==。

并且，在下一章我们将会学习 async generator，它们被用于在 `for await ... of` 循环中读取异步生成的数据流（例如，通过网络分页提取 (paginated fetches over a network)）。

在 Web 编程中，我们经常使用数据流，因此这是另一个非常重要的使用场景。

#### 关键词: Generator _, yield _, 可迭代对象

# 异步迭代和 generator

### [回顾可迭代对象](https://zh.javascript.info/async-iterators-generators#hui-gu-ke-die-dai-dui-xiang)

让我们回顾一下可迭代对象的相关内容。

假设我们有一个对象，例如下面的 `range`：

```javascript
let range = {
  from: 1,
  to: 5,
}
```

我们想对它使用 `for..of` 循环，例如 `for(value of range)`，来获取从 `1` 到 `5` 的值。

换句话说，我们想向对象 `range` 添加 **迭代能力**。

这可以通过使用一个名为 `Symbol.iterator` 的特殊方法来实现：

- 当循环开始时，该方法被 `for..of` 结构调用，并且它应该返回一个带有 `next` 方法的对象。
- 对于每次迭代，都会为下一个值调用 `next()` 方法。
- `next()` 方法应该以 `{done: true/false, value:<loop value>}` 的格式返回一个值，其中 `done:true` 表示循环结束。

---

**Spread 语法 `...` ==无法异步工作==**

需要常规的同步 iterator 的功能，无法与异步 iterator 一起使用。

例如，spread 语法无法工作：

```javascript
alert([...range]) // Error, no Symbol.iterator
```

这很正常，因为它期望找到 `Symbol.iterator`，而不是 `Symbol.asyncIterator`。

`for..of` 的情况和这个一样：==没有 `await` 关键字时==，则期望找到的是 `Symbol.iterator`。

#### [回顾 generator]

generator 是“生成（yield）值的函数”

它使我们能够写出更短的迭代代码。在大多数时候，当我们想要创建一个可迭代对象时，我们会使用 generator。

Generator 是标有 `function*`（注意星号）的函数，它使用 `yield` 来生成值，并且我们可以使用 `for..of` 循环来遍历它们。

在常规的 generator 中，我们无法使用 `await`。所有的值都必须按照 `for..of` 构造的要求==同步地出现==。

#### [异步 generator ]

对于大多数的实际应用程序，当我们想创建一个异步生成一系列值的对象时，我们都可以使用异步 generator。

语法很简单：在 `function*` 前面加上 `async`。这即可使 generator 变为异步的。

然后使用 `for await (...)` 来遍历它，像这样：

```javascript
async function* generateSequence(start, end) {
  for (let i = start; i <= end; i++) {
    // 哇，可以使用 await 了！
    await new Promise((resolve) => setTimeout(resolve, 1000))

    yield i
  }
}

;(async () => {
  let generator = generateSequence(1, 5)
  for await (let value of generator) {
    alert(value) // 1，然后 2，然后 3，然后 4，然后 5（在每个 alert 之间有延迟）
  }
})()
```

因为此 generator 是异步的，所以我们可以在其内部使用 `await`，依赖于 `promise`，执行网络请求等任务。

在一个常规的 generator 中，我们使用 `result = generator.next()` 来获得值。但在一个异步 generator 中，我们应该添加 `await` 关键字，像这样：

```javascript
result = await generator.next() // result = {value: ..., done: true/false}
```

这就是为什么异步 generator 可以与 `for await...of` 一起工作。

### 总结:(iterator & generator with async)

常规的 iterator 和 generator 可以很好地处理那些不需要花费时间来生成的的数据。

当我们期望异步地，有延迟地获取数据时，可以使用它们的异步版本，并且使用 `for await..of` 替代 `for..of`。

异步 iterator 与常规 iterator 在语法上的区别：

|                          | Iterable                      | 异步 Iterable                                         |
| :----------------------- | :---------------------------- | :---------------------------------------------------- |
| 提供 iterator 的对象方法 | `Symbol.iterator`             | `Symbol.asyncIterator`                                |
| `next()` 返回的值是      | `{value:…, done: true/false}` | resolve 成 `{value:…, done: true/false}` 的 `Promise` |

异步 generator 与常规 generator 在语法上的区别：

|                     | Generator                     | 异步 generator                                        |
| :------------------ | :---------------------------- | :---------------------------------------------------- |
| 声明方式            | `function*`                   | `async function*`                                     |
| `next()` 返回的值是 | `{value:…, done: true/false}` | resolve 成 `{value:…, done: true/false}` 的 `Promise` |

在 Web 开发中，我们经常会遇到数据流，它们分段流动（flows chunk-by-chunk）。例如，下载或上传大文件。

我们可以使用异步 generator 来处理此类数据。值得注意的是，在一些环境，例如浏览器环境下，还有另一个被称为 Streams 的 API，它提供了特殊的接口来处理此类数据流，转换数据并将数据从一个数据流传递到另一个数据流（例如，从一个地方下载并立即发送到其他地方）。

#### 关键词: iterator(Symbol), generator \*(yield), async(await), 数据流,

# module 模块

#### `外部脚本（external script）`

#### `内联脚本（inline script）`

##### [历史上的模块管理工具]

AMD require.js  
CMD sea.js
COMMONJS (NODE.JS)
UMD

[手写模块工具](https://www.bilibili.com/video/BV1NJ411W7wh?p=262&spm_id_from=pageDriver&vd_source=a01a6b5f172f99e81e9ebc2b4552722b)

#### [什么是模块？]

一个模块（module）就是一个文件。一个脚本就是一个模块。就这么简单。

模块可以相互加载，并可以使用特殊的指令 `export` 和 `import` 来交换功能，从另一个模块调用一个模块的函数：

- `export` 关键字标记了可以从当前模块外部访问的变量和函数。
- `import` 关键字允许从其他模块导入功能。

由于模块支持==特殊的关键字和功能==，因此我们必须通过使用 `<script type="module">` 特性（attribute）来告诉浏览器，此脚本应该被==当作模块（module）来对待==。默认执行==严格模式==

#### [**模块只通过 HTTP(s) 工作，而非本地**]

如果你尝试通过 `file://` 协议在本地打开一个网页，你会发现 `import/export` 指令不起作用。你可以使用本地 Web 服务器，例如 [static-server](https://www.npmjs.com/package/static-server#getting-started)，或者使用编辑器的“实时服务器”功能，例如 VS Code 的 [Live Server Extension](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) 来测试模块。

#### [模块核心功能]

模块始终在严格模式下运行。

每个模块都有自己的顶级作用域（top-level scope）。

模块应该 `export` 它们想要被外部访问的内容，并 `import` 它们所需要的内容。

- `user.js` 应该导出 `user` 变量。
- `hello.js` 应该从 `user.js` 模块中导入它。

在浏览器中，对于 HTML 页面，每个 `<script type="module">` 都存在独立的顶级作用域。

下面是同一页面上的两个脚本，都是 `type="module"`。它们==看不到彼此的顶级变量==：

```html
<script type="module">
  // 变量仅在这个 module script 内可见
  let user = 'John'
</script>

<script type="module">
  alert(user) // Error: user is not defined
</script>
```

在浏览器中，我们可以通过将变量显式地分配给 `window` 的一个属性，==使其成为窗口级别的全局变量==。例如 `window.user = "John"`。

这样所有脚本都会看到它，无论脚本是否带有 `type="module"`。

也就是说，创建这种全局变量并不是一个好的方式。请尽量避免这样做。

#### [如果这个模块被导入到多个文件中]

```javascript
// 📁 admin.js
export let admin = {
  name: 'John',
}
```

如果这个模块被导入到多个文件中, 模块仅在第一次被导入时被解析，并创建 `admin` 对象，然后将其传入到所有的导入。

==所有的导入都只获得了一个唯一的== `admin` 对象：

```javascript
// 📁 1.js
import { admin } from './admin.js'
admin.name = 'Pete'

// 📁 2.js
import { admin } from './admin.js'
alert(admin.name) // Pete

// 1.js 和 2.js 引用的是同一个 admin 对象
// 在 1.js 中对对象做的更改，在 2.js 中也是可见的
```

正如你所看到的，当在 `1.js` 中修改了导入的 `admin` 中的 `name` 属性时，我们在 `2.js` 中可以看到新的 `admin.name`。

这正是因为该模块只执行了一次。生成导出，然后这些导出在导入之间共享，因此如果更改了 `admin` 对象，在其他导入中也会看到。

**这种行为实际上非常方便，因为它允许我们“配置”模块。**

换句话说，模块可以提供需要配置的通用功能。例如身份验证需要凭证。那么模块可以导出一个配置对象，期望外部代码可以对其进行赋值。

这是经典的使用模式：

1.  模块导出一些配置方法，例如一个配置对象。
2.  ==在第一次导入时，我们对其进行初始化==，写入其属性。==可以在应用顶级脚本中进行此操作==。
3.  进一步地导入使用模块。

#### [import.meta](https://zh.javascript.info/modules-intro#importmeta)

`import.meta` 对象包含关于==当前模块的信息==。

它的内容取决于其所在的环境。在浏览器环境中，它包含当前脚本的 URL，或者如果它是在 HTML 中的话，则包含当前页面的 URL。

```HTML
<script type="module">
  alert(import.meta.url); // 脚本的 URL（对于内联脚本来说，则是当前 HTML 页面的 URL）
</script>
```

#### [在一个模块中，“this” 是 undefined](https://zh.javascript.info/modules-intro#zai-yi-ge-mo-kuai-zhong-this-shi-undefined)

这是一个小功能，但为了完整性，我们应该提到它。

在一个模块中，顶级 `this` 是 undefined。

将其与非模块脚本进行比较会发现，非模块脚本的顶级 `this` 是全局对象：

```HTML
<script>
  alert(this); // window
</script>

<script type="module">
  alert(this); // undefined
</script>
```

#### [模块脚本是延迟的](https://zh.javascript.info/modules-intro#mo-kuai-jiao-ben-shi-yan-chi-de)

模块脚本 **总是** 被延迟的，与 `defer` 特性（在 [脚本：async，defer](https://zh.javascript.info/script-async-defer) 一章中描述的）对外部脚本和内联脚本（inline script）的影响相同。

也就是说：

- 下载外部模块脚本 `<script type="module" src="...">` ==不会阻塞 HTML 的处理，它们会与其他资源并行加载。==
- 模块脚本会==等到 HTML 文档完全准备就绪==（即使它们很小并且比 HTML 加载速度更快），然后才会运行。
- 保持脚本的相对顺序：在文档中排在前面的脚本先执行。

它的一个副作用是，模块脚本总是会“看到”已完全加载的 HTML 页面，包括在它们下方的 HTML 元素。

例如：

```HTML
<script type="module">
  alert(typeof button); // object：脚本可以“看见”下面的 button
  // 因为模块是被延迟的（deferred，所以模块脚本会在整个页面加载完成后才运行
</script>

相较于下面这个常规脚本：

<script>
  alert(typeof button); // button 为 undefined，脚本看不到下面的元素
  // 常规脚本会立即运行，常规脚本的运行是在在处理页面的其余部分之前进行的
</script>

<button id="button">Button</button>
```

我们应该放置“==加载指示器==（loading indicator）” 以免 html 先于模块加载而==短暂缺失的功能==。

#### [Async 适用于内联脚本（inline script）](https://zh.javascript.info/modules-intro#async-shi-yong-yu-nei-lian-jiao-ben-inlinescript)

对于非模块脚本，`async` 特性（attribute）仅适用于外部脚本。异步脚本会在准备好后立即运行，独立于其他脚本或 HTML 文档。

对于模块脚本，它也适用于内联脚本。

例如，下面的内联脚本具有 `async` 特性，因此它==不会等待任何东西==。

它执行导入（fetch `./analytics.js`），并在准备导入完成时运行，==即使 HTML 文档还未完成，或者其他脚本仍在等待处理中==。

这对于==不依赖任何其他东西的功能==来说是非常棒的，例如计数器，广告，文档级事件监听器。

```HTML
<!-- 所有依赖都获取完成（analytics.js）然后脚本开始运行 -->
<!-- 不会等待 HTML 文档或者其他 <script> 标签 -->
<script async type="module">
  import {counter} from './analytics.js';

  counter.count();
</script>
```

#### [外部脚本](https://zh.javascript.info/modules-intro#wai-bu-jiao-ben)

具有 `type="module"` 的外部脚本（external script）在两个方面有所不同：

1.  ==具有相同 `src` 的外部脚本仅运行一次==：

    ```HTML
    <!-- 脚本 my.js 被加载完成（fetched）并只被运行一次 -->
    <script type="module" src="my.js"></script>
    <script type="module" src="my.js"></script>
    ```

2.  从另一个源（例如另一个网站）获取的外部脚本需要 [CORS](https://developer.mozilla.org/zh/docs/Web/HTTP/CORS) header，如我们在 [Fetch：==跨源请求==](https://zh.javascript.info/fetch-crossorigin) 一章中所讲的那样。换句话说，如果一个模块脚本是从另一个源获取的，则远程服务器必须提供表示允许获取的 header `Access-Control-Allow-Origin`。

    ```HTML
    <!-- another-site.com 必须提供 Access-Control-Allow-Origin -->
    <!-- 否则，脚本将无法执行 -->
    <script type="module" src="http://another-site.com/their.js"></script>
    ```

    默认这样做可以==确保更好的安全性==。

#### [不允许裸模块（“bare” module）](https://zh.javascript.info/modules-intro#bu-yun-xu-luo-mo-kuai-baremodule)

在浏览器中，`import` ==必须给出相对或绝对的 URL 路径==。没有任何路径的模块被称为“裸（bare）”模块。在 `import` 中不允许这种模块。

例如，下面这个 `import` 是无效的：

```javascript
import { sayHi } from 'sayHi' // Error，“裸”模块
// 模块必须有一个路径，例如 './sayHi.js' 或者其他任何路径
```

#### [构建工具](https://zh.javascript.info/modules-intro#gou-jian-gong-ju)

在实际开发中，浏览器模块很少被以“原始”形式进行使用。通常，我们会使用一些特殊工具，例如 [==Webpack==](https://webpack.js.org/)，将它们打包在一起，然后部署到生产环境的服务器。

使用打包工具的一个好处是 —— 它们可以更好地==控制模块的解析方式==，允许我们使用裸模块和更多的功能，例如 CSS/HTML 模块等。

构建工具做以下这些事儿：

1.  从一个打算放在 HTML 中的 `<script type="module">` ==“主”模块开始==。
2.  ==分析它的依赖==：它的导入，以及它的导入的导入等。
3.  ==使用所有模块构建一个文件==（或者多个文件，这是可调的），==并用打包函数（bundler function）替代原生的 `import` 调用==，以使其正常工作。还支持像 HTML/CSS 模块等==“特殊”的模块类型==。
4.  在处理过程中，可能会应用==其他转换和优化==：
    - 删除无法访问的代码。
    - 删除==未使用的导出==（“==tree-shaking==”）。
    - 删除特定于开发的像 `console` 和 `debugger` 这样的语句。
    - 可以使用 [Babel](https://babeljs.io/) 将前沿的现代的 JavaScript 语法转换为具有类似功能的旧的 JavaScript 语法。
    - ==压缩生成的文件（删除空格，用短的名字替换变量等）。==

如果我们使用打包工具，那么脚本会被打包进一个单一文件（或者几个文件），在这些脚本中的 `import/export` 语句会被替换成特殊的打包函数（bundler function）。因此，最终打包好的脚本中==不包含任何== `import/export`，==它也不需要== `type="module"`，我们可以将其放入常规的 `<script>`：

```HTML
<!-- 假设我们从诸如 Webpack 这类的打包工具中获得了 "bundle.js" 脚本 -->
<script src="bundle.js"></script>
```

下面总结一下模块的核心概念：

1.  一个模块就是一个文件。浏览器需要使用 `<script type="module">` 以使`import/export` 可以工作。模块（译注：相较于常规脚本）有几点差别：
    - 默认是==延迟解析==的（deferred）。
    - ==Async 可用于内联脚本==。
    - 要从==另一个源==（域/协议/端口）加载外部脚本，==需要 CORS header==。
    - ==重复==的外部脚本会被忽略
2.  模块具有自己的本地顶级作用域，并可以通过 `import/export` 交换功能。
3.  模块始终使用 `use strict`。
4.  ==模块代码只执行一次==。==导出仅创建一次==，然后会==在导入之间共享==。

当我们使用模块时，==每个模块都会实现特定功能并将其导出==。然后我们使用 `import` 将其直接导入到需要的地方即可。浏览器会自动加载并解析脚本。

在生产环境中，出于性能和其他原因，开发者经常使用诸如 [Webpack](https://webpack.js.org/) 之类的打包工具将模块打包到一起。

#### 关键词: module, 模块, 单个文件, 导出导入, 异步/延迟, 内联外部,

#### webpack 打包工具, 独立顶级作用域

# 导出和导入

## [在声明前导出](https://zh.javascript.info/import-export#zai-sheng-ming-qian-dao-chu)

我们可以通过在声明之前放置 `export` 来标记任意声明为导出，无论声明的是变量，函数还是类都可以。

例如，这里的所有导出均有效：

```javascript
// 导出数组
export let months = [
  'Jan',
  'Feb',
  'Mar',
  'Apr',
  'Aug',
  'Sep',
  'Oct',
  'Nov',
  'Dec',
]

// 导出 const 声明的变量
export const MODULES_BECAME_STANDARD_YEAR = 2015

// 导出类
export class User {
  constructor(name) {
    this.name = name
  }
}
```

大部分 JavaScript 样式指南都==不建议在函数和类声明后使用分号==。

```javascript
export function sayHi(user) {
  alert(`Hello, ${user}!`)
} // 在这里没有分号 ;
```

#### [Import *]

但是如果有很多要导入的内容，我们可以使用 `import * as <obj>` 将==所有内容导入==为一个对象，例如：

```javascript
// 📁 main.js
import * as say from './say.js'

say.sayHi('John')
say.sayBye('John')
```

### 别名导入导出

#### [Import “as”]

我们也可以使用 `as` 让导入具有不同的名字。

例如，简洁起见，我们将 `sayHi` 导入到局部变量 `hi`，将 `sayBye` 导入到 `bye`：

```javascript
// 📁 main.js
import { sayHi as hi, sayBye as bye } from './say.js'

hi('John') // Hello, John!
bye('John') // Bye, John!
```

#### [Export “as”]

导出也具有类似的语法。

我们将函数导出为 `hi` 和 `bye`：

```javascript
export { sayHi as hi, sayBye as bye }
```

#### [Export default] (默认导出)

模块提供了一个特殊的默认导出 `export default` 语法，以使“==一个模块只做一件事==”的方式看起来更好。

| 命名的导出                | 默认的导出                        |
| :------------------------ | :-------------------------------- |
| `export class User {...}` | `export default class User {...}` |
| `import {User} from ...`  | `import User from ...`            |

从技术上讲，我们可以在一个模块中同时有默认的导出和命名的导出，但是实际上人们通常不会混合使用它们。==模块要么是命名的导出要么是默认的导出。==

默认导出可以任意别名

由于==每个文件最多只能有一个默认的导出==，因此==导出的实体可能没有名称==。

例如，下面这些都是完全有效的默认的导出：

```javascript
export default class { // 没有类名
  constructor() { ... }
}
export default function(user) { // 没有函数名
  alert(`Hello, ${user}!`);
}
// 导出单个值，而不使用变量
export default ['Jan', 'Feb', 'Mar','Apr', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
```

……对于默认的导出，==我们总是在导入时选择名称==：

```javascript
import User from './user.js' // 有效
import MyUser from './user.js' // 也有效
// 使用任何名称导入都没有问题
```

为了避免这种情况并使代码保持一致，可以遵从这条规则，即导入的变量应==与文件名相对应==

#### [重新导出]

#### 重新导出（Re-export）

#### 语法 `export ... from ...` 允许导入内容，并立即将其导出

由于实际导出的功能分散在 package 中，所以我们可以将它们导入到 `auth/index.js`，然后再从中导出它们：

```javascript
// 📁 auth/index.js

// 导入 login/logout 然后立即导出它们
import {login, logout} from './helpers.js';
export {login, logout};

// 将默认导出导入为 User，然后导出它
import User from './user.js';
export {User};
...
```

现在使用我们 package 的人可以 `import {login} from "auth/index.js"`。

语法 `export ... from ...` 只是下面这种导入-导出的简写：

```javascript
// 📁 auth/index.js
// 重新导出 login/logout
export {login, logout} from './helpers.js';

// 将默认导出重新导出为 User
export {default as User} from './user.js'; !!
...
```

`export ... from` 与 `import/export` 相比的显着区别是重新导出的模块在当前文件中不可用。所以在上面的 `auth/index.js` 示例中，我们不能使用重新导出的 `login/logout` 函数。

### 总结:

#### 导出:

- 在声明一个 class/function/… 之前：
  - `export [default] class/function/variable ...`
- 独立的导出：
  - `export {x [as y], ...}`.
- 重新导出：
  - `export {x [as y], ...} from "module"`
  - `export * from "module"`（不会重新导出默认的导出）。
  - `export {default [as y]} from "module"`（重新导出默认的导出）。

#### 导入:

- 导入命名的导出：
  - `import {x [as y], ...} from "module"`
- 导入默认的导出：
  - `import x from "module"`
  - `import {default as x} from "module"`
- 导入所有：
  - `import * as obj from "module"`
- 导入模块（其代码，并运行），但不要将其任何导出赋值给变量：
  - `import "module"`

我们把 `import/export` 语句放在脚本的顶部或底部，都没关系。

因此，从技术上讲，下面这样的代码没有问题：

```javascript
sayHi()

// ...

import { sayHi } from './say.js' // 在文件底部导入
```

在实际开发中，导入通常位于文件的开头，但是这只是为了更加方便。

**请注意在 `{...}` 中的 import/export 语句无效。**

# 动态导入

这是因为 `import`/`export` 旨在提供代码结构的主干。这是非常好的事儿，因为这样便于分析代码结构，可以收集模块，可以使用特殊工具将收集的模块打包到一个文件中，可以删除未使用的导出（“tree-shaken”）。这些只有在 `import`/`export` 结构简单且固定的情况下才能够实现。

#### [import() 表达式]

`import(module)` 表达式加载模块并返回一个 ==promise==，该 promise resolve 为一个包含其所有导出的模块对象。我们可以在代码中的任意位置调用这个表达式。

或者，如果在异步函数中，我们可以使用 `let module = await import(modulePath)`。

<u>动态导入在常规脚本中工作时，它们不需要 `script type="module"`.</u>

尽管 `import()` 看起来像一个函数调用，但它只是一种特殊语法，只是恰好使用了括号（类似于 `super()`）。

因此，我们不能将 `import` 复制到一个变量中，或者对其使用 `call/apply`。因为它==不是一个函数==。

# proxy 代理器

```js
let OBJ = { name: 'may', age: 20 }
let proxy = new Proxy(OBJ, {
  get(obj, property) {
    return obj[property]
  },
  set(obj, property, value) {
    obj[property] = value
    return true
  },
})

proxy.name = 'Fri'
```

#### 请注意：

请注意==代理如何覆盖变量==：

```javascript
dictionary = new Proxy(dictionary, ...);
```

代理应该在所有地方都==完全替代目标对象==。目标对象被代理后，任何人都不应该再引用目标对象。否则很容易搞砸。

内部方法 <u>被</u> Handler 方法 <u>拦截在</u> 何时触发

| 内部方法                | Handler 方法               | 何时触发                                                                                                                                                                                                                                                                                                                    |
| :---------------------- | :------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `[[Get]]`               | `get`                      | 读取属性                                                                                                                                                                                                                                                                                                                    |
| `[[Set]]`               | `set`                      | 写入属性                                                                                                                                                                                                                                                                                                                    |
| `[[HasProperty]]`       | `has`                      | `in` 操作符                                                                                                                                                                                                                                                                                                                 |
| `[[Delete]]`            | `deleteProperty`           | `delete` 操作符                                                                                                                                                                                                                                                                                                             |
| `[[Call]]`              | `apply`                    | 函数调用                                                                                                                                                                                                                                                                                                                    |
| `[[Construct]]`         | `construct`                | `new` 操作符                                                                                                                                                                                                                                                                                                                |
| `[[GetPrototypeOf]]`    | `getPrototypeOf`           | [Object.getPrototypeOf](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf)                                                                                                                                                                                                |
| `[[SetPrototypeOf]]`    | `setPrototypeOf`           | [Object.setPrototypeOf](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf)                                                                                                                                                                                                |
| `[[IsExtensible]]`      | `isExtensible`             | [Object.isExtensible](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/isExtensible)                                                                                                                                                                                                    |
| `[[PreventExtensions]]` | `preventExtensions`        | [Object.preventExtensions](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/preventExtensions)                                                                                                                                                                                          |
| `[[DefineOwnProperty]]` | `defineProperty`           | [Object.defineProperty](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty), [Object.defineProperties](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperties)                                                              |
| `[[GetOwnProperty]]`    | `getOwnPropertyDescriptor` | [Object.getOwnPropertyDescriptor](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptor), `for..in`, `Object.keys/values/entries`                                                                                                                                   |
| `[[OwnPropertyKeys]]`   | `ownKeys`                  | [Object.getOwnPropertyNames](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyNames), [Object.getOwnPropertySymbols](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertySymbols), `for..in`, `Object.keys/values/entries` |

有一个普遍的约定，

即以下划线 `_` 开头的属性和方法是==内部的==。不应从对象外部访问它们。

`get(target, prop, receiver)`

- `target` —— 是目标对象，该对象被作为第一个参数传递给 `new Proxy`，
- `prop` —— 目标属性名，

`set(target, prop, value, receiver)` 要返回 true/false

`deleteProperty(target, prop)` 要返回 true/false

`ownKeys(target)`

`getOwnPropertyDescriptor(target, prop) `

`has(target, prop)`

`apply(target, thisArg, args)`

- `thisArg` 是 `this` 的值。
- `args` 是参数列表。

`Proxy` 的功能要强大得多，因为它可以将所有东西转发到目标对象。

让我们使用 `Proxy` 来==替换掉包装函数==

#### 用 proxy 实现双向绑定

- 用 set 拦截写入操作，然后 set 中同时把值赋给单个或多个实现双向绑定。

---

# 网络请求

# Fetch

JavaScript 可以将网络请求发送到服务器，并在需要时加载新信息。
对于来自 JavaScript 的网络请求，有一个总称术语 “AJAX”（Asynchronous JavaScript And XML 的简称）。
fetch() 方法是一种现代通用的方法.
基本语法：

```js
let promise = fetch(url, [options])
```

url —— 要访问的 URL。
options —— 可选参数：method，header 等。

没有 options ，这就是一个简单的 GET 请求，下载 url 的内容。

获取响应通常经过==两个阶段== :

#### 第一阶段，当服务器发送了响应头（response header）

fetch 返回的 promise 就使用内建的 Response class 对象来对响应头进行解析。
在这个阶段，我们可以通过检查响应头，来检查 HTTP 状态以确定请求是否成功，
==当前还没有响应体==（response body）。

如果 fetch 无法建立一个 HTTP 请求，例如网络问题，亦或是请求的网址不存在，那么 promise 就会 reject。异常的 HTTP 状态，例如 404 或 500，不会导致出现 error。

我们可以在 response 的属性中看到 HTTP 状态：

`status` —— HTTP 状态码，例如 200。
`ok` —— 布尔值，如果 HTTP 状态码为 200-299，则为 true。

例如：

```js
let response = await fetch(url)

if (response.ok) {
  // 如果 HTTP 状态码为 200-299
  // 获取 response body（此方法会在下面解释）
  let json = await response.json()
} else {
  alert('HTTP-Error: ' + response.status)
}
```

#### 第二阶段，为了获取 response body，我们需要使用一个其他的方法调用。

==重要==：

我们只能选择一种读取 body 的方法。
如果我们已经使用了 response.text() 方法来获取 response，那么如果再用 response.json()，则不会生效，因为 body 内容已经被处理过了。

### Response header

要在 fetch 中设置 request header，我们可以使用 `headers` 选项。它有一个带有输出 header 的对象，如下所示：

```js
let response = fetch(protectedUrl, {
  headers: {
    Authentication: 'secret',
  },
})
```

## POST 请求

要创建一个 POST 请求，或者其他方法的请求，我们需要使用 fetch 选项：

`method` —— HTTP 方法，例如 POST，
`body` —— request body，其中之一：

- 字符串（例如 JSON 编码的），
  FormData 对象，以 multipart/form-data 形式发送数据，
  Blob/BufferSource 发送二进制数据，
  URLSearchParams，以 x-www-form-urlencoded 编码形式发送数据，很少使用。

JSON 形式是最常用的。

```js
let user = {
  name: 'John',
  surname: 'Smith',
}

let response = await fetch('/article/fetch/post/user', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json;charset=utf-8',
  },
  body: JSON.stringify(user),
})

let result = await response.json()
alert(result.message)
```

请注意，如果请求的 body 是字符串，则 `Content-Type` 会默认设置为 text/plain;charset=UTF-8。

但是，当我们要发送 JSON 时，我们会使用 `headers` 选项来发送 ==application/json==，这是 JSON 编码的数据的正确的 `Content-Type`。

==总结==
典型的 fetch 请求由两个 `await` 调用组成：

```js
let response = await fetch(url, options) // 解析 response header
let result = await response.json() // 将 body 读取为 json
```

或者以 `promise` 形式：

```js
fetch(url, options)
  .then(response => response.json())
  .then(result => /* process result */)
```

目前 `fetch` 选项：

`method` —— HTTP 方法，
`headers` —— 具有 request header 的对象（不是所有 header 都是被允许的）
`body` —— 要以 string，FormData，BufferSource，Blob 或 UrlSearchParams 对象的形式发送的数据（request body）。

# FormData

FormData 对象用于捕获 HTML 表单，并使用 fetch 或其他网络方法提交。

我们可以从 HTML 表单创建 `new FormData(form)`，也可以创建一个完全没有表单的对象 `new FormData()`，然后使用以下方法附加字段：

formData.`append`(name, value)
formData.`append`(name, blob, fileName)
formData.`set`(name, value)
formData.`set`(name, blob, fileName)

让我们在这里注意两个特点：

`set` 方法会移除具有相同名称（name）的字段，而 `append` 不会。
要发送文件，需要使用三个参数的语法，最后一个参数是文件名，
一般是通过 `<input type="file">` 从用户文件系统中获取的。
其他方法是：

formData.delete(name)
formData.get(name)
formData.has(name)

---

---

---

# 浏览器\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

# 浏览器环境，规格

- DOM 规范

  描述文档的结构、操作和事件，详见 [https://dom.spec.whatwg.org](https://dom.spec.whatwg.org/)。

- CSSOM 规范

  描述样式表和样式规则，对它们进行的操作，以及它们与文档的绑定，详见 https://www.w3.org/TR/cssom-1/。

- HTML 规范

  描述 HTML 语言（例如标签）以及 BOM（浏览器对象模型）— 各种浏览器函数：`setTimeout`，`alert`，`location` 等，详见 [https://html.spec.whatwg.org](https://html.spec.whatwg.org/)。它采用了 DOM 规范，并使用了许多其他属性和方法对其进行了扩展。

此外，某些类被分别描述在 https://spec.whatwg.org/。

请注意这些链接，因为要学的东西太多了，所以不可能涵盖并记住所有内容。

当你想要了解某个属性或方法时，Mozilla 手册 https://developer.mozilla.org/en-US/search 是一个很好的资源，但对应的规范可能会更好：它更复杂，且阅读起来需要更长的时间，但是会使你的基本知识更加全面，更加完整。

要查找某些内容时，你通常可以使用互联网搜索 “WHATWG [term]” 或 “MDN [term]”，例如 [https://google.com?q=whatwg+localstorage](https://google.com/?q=whatwg+localstorage)，[https://google.com?q=mdn+localstorage](https://google.com/?q=mdn+localstorage)。

#### 关键词: DOM, BOM, HTML 规范

# DOM 树

在控制台（Console）中获取元素（Elements）选项卡中的节点的方法:

​ 现在最后选中的元素可以通过 `$0` 来进行操作，先前选择的是 `$1`

HTML/XML 文档在浏览器内均被表示为 DOM 树。

- 标签（tag）成为元素节点，并形成文档结构。
- 文本（text）成为文本节点。
- ……等，HTML 中的所有东西在 DOM 中都有它的位置，甚至对注释也是如此。

我们可以使用开发者工具来检查（inspect）DOM 并手动修改它。

#### 关键词: $0 $1, 都是对象, 都能就地修改, inspect

# 遍历 DOM

**这里有个问题：`document.body` 的值可能是 `null`**

脚本无法访问在运行时不存在的元素。**在 DOM 的世界中，**`null` **就意味着“不存在”**

尤其是，如果一个脚本是在 `<head>` 中，那么脚本是访问不到 `document.body` 元素的，因为浏览器还没有读到它。

- **子节点（或者叫作子）** — 对应的是直系的子元素。换句话说，它们被完全嵌套在给定的元素中。例如，`<head>` 和 `<body>` 就是 `<html>` 元素的子元素。
- **子孙元素** — 嵌套在给定元素中的所有元素，包括子元素，以及子元素的子元素等。(整个子树)

- `childNodes` `firstChild` `lastChild` `hasChildNodes()`

#### DOM 集合是只读的

#### DOM 集合是实时的

#### 不要使用 `for..in` 来遍历集合

### 兄弟节点（Sibling）

- `nextSibling` `previousSibling` `parentNode`

#### 只考虑 **元素节点** 的导航链接（navigation link）

- `children` — 仅那些作为元素节点的子代的节点。
- `firstElementChild`，`lastElementChild` — 第一个和最后一个子元素。
- `previousElementSibling`，`nextElementSibling` — 兄弟元素。
- `parentElement` — 父元素。

#### `<table>` 元素支持 (除了上面给出的，之外) 以下这些属性:

- `table.rows` — `<tr>` 元素的集合。
- `table.caption/tHead/tFoot` — 引用元素 `<caption>`，`<thead>`，`<tfoot>`。
- `table.tBodies` — `<tbody>` 元素的集合（根据标准还有很多元素，但是这里至少会有一个 — 即使没有被写在 HTML 源文件中，浏览器也会将其放入 DOM 中）。

**`<thead>`，`<tfoot>`，`<tbody>`** 元素提供了 `rows` 属性：

- `tbody.rows` — 表格内部 `<tr>` 元素的集合。

**`<tr>`：**

- `tr.cells` — 在给定 `<tr>` 中的 `<td>` 和 `<th>` 单元格的集合。
- `tr.sectionRowIndex` — 给定的 `<tr>` 在封闭的 `<thead>/<tbody>/<tfoot>` 中的位置（索引）。
- `tr.rowIndex` — 在整个表格中 `<tr>` 的编号（包括表格的所有行）。

**`<td>` 和 `<th>`：**

- `td.cellIndex` — 在封闭的 `<tr>` 中单元格的编号。

给定一个 DOM 节点，我们可以使用导航（navigation）属性访问其直接的邻居。

#### 这些属性主要分为两组：

- 对于所有节点：`parentNode`，`childNodes`，`firstChild`，`lastChild`，`previousSibling`，`nextSibling`。
- 仅对于元素节点：`parentElement`，`children`，`firstElementChild`，`lastElementChild`，`previousElementSibling`，`nextElementSibling`。

`elem.lastChild.nextSibling` 值一直都是 `null`

`elem.children[0].previousSibling` 值不一定都是 `null` , 有可能是文字节点

#### 关键词: 兄弟节点, 仅元素节点, table 特殊属性,

# 搜索：getElement，querySelector

### 以 id 查找

document.getElementById 或 id:

```html
<div id="elem">
  <div id="elem-content">Element</div>
</div>

<script>
  // elem 是对带有 id="elem" 的 DOM 元素的引用
  elem.style.background = 'red'

  // id="elem-content" 内有连字符，所以它不能成为一个变量
  // ...但是我们可以通过使用方括号 window['elem-content'] 来访问它
</script>
```

**只有** `document.getElementById`**，没有** `anyElem.getElementById`

`getElementById` 方法只能被在 `document` 对象上调用。它会在整个文档中查找给定的 `id`。

#### elem.querySelectorAll

这个方法确实功能强大，因为可以使用任何 CSS 选择器。

```js
let elements = document.querySelectorAll('ul > li:last-child')
```

#### elem.querySelector

只会查找一个。因此它在速度上更快，并且写起来更短。

#### elem.matches(css)

不会查找任何内容，它只会检查 `elem` 是否与给定的 CSS 选择器匹配。它返回 `true` 或 `false`。

#### elem.closest(css)

方法会查找与 CSS 选择器匹配的最近的祖先。`elem` 自己也会被搜索。

#### 还有其他通过标签，类等查找节点的方法。

#### 如今，它们大多已经成为了历史，因为==`querySelector` 功能更强大，写起来更短。==

## 实时的集合

所有的 `"getElementsBy*"` 方法都会返回一个 **实时的（live）** 集合。这样的集合始终反映的是文档的当前状态，并且在文档发生更改时会“自动更新”。

相反，`querySelectorAll` 返回的是一个 **静态的** 集合。就像元素的固定数组。

#### 有 6 种主要的方法，可以在 DOM 中搜索元素节点：

| 方法名                   | 搜索方式     | 可以在元素上调用？ | 实时的？ |
| ------------------------ | ------------ | ------------------ | -------- |
| `querySelector`          | CSS-selector | ✔                  | -        |
| `querySelectorAll`       | CSS-selector | ✔                  | -        |
| `getElementById`         | `id`         | -                  | -        |
| `getElementsByName`      | `name`       | -                  | ✔        |
| `getElementsByTagName`   | tag or `'*'` | ✔                  | ✔        |
| `getElementsByClassName` | class        | ✔                  | ✔        |

- `elem.matches(css)` 用于检查 `elem` 与给定的 CSS 选择器是否匹配。
- `elem.closest(css)` 用于查找与给定 CSS 选择器相匹配的最近的祖先。`elem` 本身也会被检查。
- 如果 `elemB` 在 `elemA` 内（`elemA` 的后代）或者 `elemA==elemB`，`elemA.contains(elemB)` 将返回 true。

#### document.querySelector('form[name="search"]')

#### ==引号嵌套要切换双引号==, 引号开始用单引号(自定)

#### 关键词: querySelector, querySelectorAll, 静态集合, id 不声明使用

# 节点属性：type，tag 和 content

<img src="./assets/Js 进阶.assets/image-20220514172340507.png" alt="image-20220514172340507" style="zoom:50%;" />

- [EventTarget](https://dom.spec.whatwg.org/#eventtarget) — 是根的“抽象（abstract）”类。该类的对象从未被创建。它作为一个基础，以便让所有 DOM 节点都支持所谓的“事件（event）”

- [Node](http://dom.spec.whatwg.org/#interface-node) — 也是一个“抽象”类，充当 DOM 节点的基础。它提供了树的核心功能：`parentNode`，`nextSibling`，`childNodes` 等（它们都是 getter）。`Node` 类的对象从未被创建。但是有一些继承自它的具体的节点类，例如：文本节点的 `Text`，元素节点的 `Element`，以及更多异域（exotic）类，例如注释节点的 `Comment`。

- [Element](http://dom.spec.whatwg.org/#interface-element) — 是 DOM 元素的基本类。它提供了元素级的导航（navigation），例如 `nextElementSibling`，`children`，以及像 `getElementsByTagName` 和 `querySelector` 这样的搜索方法。浏览器中不仅有 HTML，还会有 XML 和 SVG。`Element` 类充当更多特定类的基本类：`SVGElement`，`XMLElement` 和 `HTMLElement`。

- HTMLElement

  — 最终是所有 HTML 元素的基本类。各种 HTML 元素均继承自它：

  - [HTMLInputElement](https://html.spec.whatwg.org/multipage/forms.html#htmlinputelement) — `<input>` 元素的类，
  - [HTMLBodyElement](https://html.spec.whatwg.org/multipage/semantics.html#htmlbodyelement) — `<body>` 元素的类，
  - [HTMLAnchorElement](https://html.spec.whatwg.org/multipage/semantics.html#htmlanchorelement) — `<a>` 元素的类，
  - …

还有很多其他标签具有自己的类，可能还具有特定的属性和方法，而一些元素，如 `<span>`、`<section>`、`<article>` 等，==没有任何特定的属性，所以它们是 `HTMLElement` 类的实例==。

#### 每个 DOM 节点都属于一个特定的类。这些类形成层次结构（hierarchy）。完整的属性和方法集是继承的结果。

主要的 DOM 节点属性有：

- `nodeType`

  我们可以使用它来查看节点是文本节点还是元素节点。它具有一个数值型值（numeric value）：`1` 表示元素，`3` 表示文本节点，其他一些则代表其他节点类型。只读。

- `nodeName/tagName`

  用于元素名，标签名（除了 XML 模式，都要大写）。对于非元素节点，`nodeName` 描述了它是什么。只读。

- `innerHTML`

  元素的 HTML 内容。可以被修改。

  innerHTML+=” 会进行完全重写 (删除后添加)

- `outerHTML`

  元素的完整 HTML(包括 `<tag>` )。对 `elem.outerHTML` 的写入操作不会触及 `elem` 本身。
  而是在外部上下文中将其替换为新的 HTML。

- `nodeValue/data`

  非元素节点（文本、注释）的内容。两者几乎一样，我们通常使用 `data`。可以被修改。==(注释的内容)==

  ```html
  <body>
    Hello ... let text = document.body.firstChild; alert(text.data); // Hello
  </body>
  ```

- `textContent`

  元素内的文本。写入文本会将文本放入元素内，所有特殊字符和标签均被视为文本。可以安全地插入用户生成的文本，并防止不必要的 HTML 插入。

- `hidden`

  当被设置为 `true` 时，执行与 CSS `display:none` 相同的事。

DOM 节点还具有其他属性，具体有哪些属性则取决于它们的类。例如，`<input>` 元素（`HTMLInputElement`）支持 `value`，`type`，而 `<a>` 元素（`HTMLAnchorElement`）则支持 `href` 等。大多数标准 HTML 特性（attribute）都具有相应的 DOM 属性。

#### 然而，但是 HTML 特性（attribute）和 DOM 属性（property）并不总是相同的

#### 获取 DOM 元素在层次结构的位置:

通过 `__proto__` 来遍历原型链

使用 `constructor.name`, 获取一个类的 name

在 `prototype` 中还有一个==对构造函数的引用==

```js
HTMLDocument.prototype.__proto__.constructor.name
```

#### 关键词: 层次结构(DOM 原型链), IDL, textContent, hidden

# 特性和属性

# （Attributes and properties）

- #### 特性（attribute）— 写在 HTML 中的内容。

- #### 属性（property）— DOM 对象中的内容。

当浏览器加载页面时，它会“读取”（或者称之为：“解析”）HTML 并从中生成 DOM 对象。
例如，如果标签是 `<body id="page">`，那么 DOM 对象就会有 `body.id="page"`。

有些特性和属性不能同步
例如 `input.value` 只能从特性同步到属性，反过来则不行

简略的对比：

|      | 属性                                   | 特性                         |
| :--- | :------------------------------------- | :--------------------------- |
| 类型 | 任何值，标准的属性具有规范中描述的类型 | 字符串                       |
| 名字 | 名字（name）是大小写敏感的             | 名字（name）是大小写不敏感的 |

操作特性的方法：

- `elem.hasAttribute(name)` — 检查是否存在这个特性。
- `elem.getAttribute(name)` — 获取这个特性值。
- `elem.setAttribute(name, value)` — 设置这个特性值。
- `elem.removeAttribute(name)` — 移除这个特性。
- `elem.attributes` — 所有特性的集合。

在大多数情况下，最好使用 DOM 属性。仅当 DOM 属性无法满足开发需求，并且我们真的需要特性时，才使用特性，例如：

- 我们需要一个非标准的特性。但是如果它以 `data-` 开头，那么我们应该使用 `dataset`。
  像 `data-order-state` 这样的多词特性可以以驼峰式进行调用：`dataset.orderState`。
- 我们想要读取 HTML 中“所写的”值。对应的 DOM 属性可能不同，例如 `href` 属性一直是一个 **完整的** URL，但是我们想要的是“原始的”值。

#### 关键词: 特性-属性, 值同步, 自定义特性属性, data-\*, 完整 URL

# 修改文档（document）

- 创建新节点的方法：

  - `document.createElement(tag)` — 用给定的标签创建一个元素节点，
  - `document.createTextNode(value)` — 创建一个文本节点（很少使用），
  - `elem.cloneNode(deep)` — 克隆元素，如果 `deep==true` 则与其后代一起克隆。

- 插入和移除节点的方法：

  - `node.append(...nodes or strings)` — 在 `node` 末尾插入，
  - `node.prepend(...nodes or strings)` — 在 `node` 开头插入，
  - `node.before(...nodes or strings)` — 在 `node` 之前插入，
  - `node.after(...nodes or strings)` — 在 `node` 之后插入，
  - `node.replaceWith(...nodes or strings)` — 替换 `node`。
  - `node.remove()` — 移除 `node`。

  文本字符串被“作为文本”插入。(not code)
  字符串被以一种==安全的方式==插入到页面中，就像 `elem.textContent` 所做的一样。

- 这里还有“旧式”的方法：

  - `parent.appendChild(node)`
  - `parent.insertBefore(node, nextSibling)`
  - `parent.removeChild(node)`
  - `parent.replaceChild(newElem, node)`

  这些方法都返回 `node`。

- 在 `html` 中给定一些 HTML，`elem.insertAdjacentHTML(where, html)`
  会根据 `where` 的值来插入它：

  - `"beforebegin"` — 将 `html` 插入到 `elem` 前面，

  - `"afterbegin"` — 将 `html` 插入到 `elem` 的开头，

  - `"beforeend"` — 将 `html` 插入到 `elem` 的末尾，

  - `"afterend"` — 将 `html` 插入到 `elem` 后面。

  - ```html
    <div id="div"></div>
    <script>
      div.insertAdjacentHTML('beforebegin', '<p>Hello</p>')
      div.insertAdjacentHTML('afterend', '<p>Bye</p>')
    </script>
    ```

另外，还有类似的方法，`elem.insertAdjacentText` 和 `elem.insertAdjacentElement`，它们会插入文本字符串和元素，但很少使用。(因为有 append…之类的方法)

- 要在页面加载完成之前将 HTML 附加到页面：

  - `document.write(html)`

  页面加载完成后，这样的调用将会擦除文档。多见于旧脚本。

#### 关键词: 创建,克隆,更新(插入),删除 DOM, DocumentFragment(传递 Node)

# 样式(css)和类(class)

要管理 class，有两个 DOM 属性：

- `className` — 字符串值，可以很好地管理整个类的集合。
- `classList` — 具有 `add/remove/toggle/contains` 方法的对象，可以很好地支持单个类。
- [注意单位](https://zh.javascript.info/styles-and-classes#zhu-yi-dan-wei)

要改变样式：

- `style` 属性是具有==驼峰（camelCased）样式==的对象。对其进行读取和修改与修改 `"style"` 特性（attribute）中的各个属性具有相同的效果。要了解如何应用 `important` 和其他特殊内容 — 在 [MDN](https://developer.mozilla.org/zh/docs/Web/API/CSSStyleDeclaration) 中有一个方法列表。
- `style.cssText` 属性对应于整个 `"style"` 特性（attribute），即完整的样式字符串。
  因为 `div.style` 是一个对象，并且它是只读的。

要读取已解析的（resolved）样式（对于所有类，在应用所有 CSS 并计算最终值之后）：

- `getComputedStyle(elem, [pseudo])` 返回与 `style` 对象类似的，且包含了所有类的对象。只读。
  现在 `getComputedStyle` 实际上返回的是属性的解析值（resolved）。

#### 关键词: class, style, css, 只读, 解析值(统一绝对单位)

# 元素大小和滚动

元素具有以下几何属性：

- `offsetParent` — 是最接近的 CSS 定位的祖先，或者是 `td`，`th`，`table`，`body`。
- `offsetLeft/offsetTop` — 是相对于 `offsetParent` 的左上角边缘的坐标。
- `offsetWidth/offsetHeight` — 元素的“外部” width/height，边框（border）尺寸计算在内。
- `clientLeft/clientTop` — 从元素左上角外角到左上角内角的距离。
  准确地说 — 这些属性==不是边框的 width/height==，而是内侧与外侧的相对坐标。
  对于从左到右显示内容的操作系统来说，它们始终是左侧/顶部 border 的宽度。而对于从右到左显示内容的操作系统来说，垂直滚动条在左边，所以 `clientLeft` ==也包括滚动条的宽度==。
- `clientWidth/clientHeight` — 内容的 width/height，包括 padding，但不包括滚动条（scrollbar）。
- `scrollWidth/scrollHeight` — 内容的 width/height，就像 `clientWidth/clientHeight` 一样，但还包括元素的滚动出的不可见的部分。
- `scrollLeft/scrollTop` — 从元素的左上角开始，滚动出元素的上半部分的 width/height。

除了 `scrollLeft/scrollTop` 外，所有属性都是只读的。如果我们修改 `scrollLeft/scrollTop`，浏览器会滚动对应的元素。

#### **对于未显示的元素，几何属性为 0/null**

我们可以使用这些属性将元素展开（==expand==）到整个 width/height。
刚好显示全部内容,不需要滚动

像这样：

```javascript
// 将元素展开（expand）到完整的内容高度
element.style.height = `${element.scrollHeight}px`
```

  
#### 关键词: offset, client, scroll, null,0, 数值/字符串,

# Window 大小和滚动

几何：

- 文档可见部分的 width/height（内容区域的 width/height）：`document.documentElement.clientWidth/clientHeight`
  **不是** `window.innerWidth/innerHeight`

- 整个文档的 width/height，其中包括滚动出去的部分：

  ```javascript
  let scrollHeight = Math.max(
    document.body.scrollHeight,
    document.documentElement.scrollHeight,
    document.body.offsetHeight,
    document.documentElement.offsetHeight,
    document.body.clientHeight,
    document.documentElement.clientHeight
  )
  ```

滚动：

- 读取当前的滚动：`window.pageYOffset/pageXOffset`。
  (等于 `window` 的 `scrollX` **和** `scrollY`)
- 更改当前的滚动：
  - `window.scrollTo(pageX,pageY)` — 绝对坐标，
  - `window.scrollBy(x,y)` — 相对当前位置进行滚动，
  - `elem.scrollIntoView(top)` — 滚动以使 `elem` 可见（`elem` 与窗口的顶部(1)/底部对齐(0)）。

要使文档不可滚动，只需要设置 `document.body.style.overflow = "hidden"`。

` document.body.style.overflow = ''` 恢复设置

#### 关键词：页面滚动/尺寸, documentElement(根文档元素)

# 坐标

页面上的任何点都有坐标：

1.  相对于窗口的坐标 — `elem.getBoundingClientRect()`。
2.  相对于文档的坐标 — `elem.getBoundingClientRect()` 加上当前页面滚动。

窗口坐标非常适合和 `position:fixed` 一起使用，文档坐标非常适合和 `position:absolute` 一起使用。

这两个坐标系统各有利弊。有时我们需要其中一个或另一个，就像 CSS `position` 的 `absolute` 和 `fixed` 一样。

<img src='./assets/Js 进阶.assets/DOM定位.jpg' style='zoom:60%'>

#### 关键词: getBoundingClientRect(); top, left, clientX/Y, pageX/Y

---

---

# DOM

#### 把元素解析成对象操作

#### .nodeType 获取节点类型

元素节点 　 Node.ELEMENT_NODE(1)
属性节点 　 Node.ATTRIBUTE_NODE(2)
文本节点 　 Node.TEXT_NODE(3)
CDATA 节点 Node.CDATA_SECTION_NODE(4)
实体引用名称节点 　　 Node.ENTRY_REFERENCE_NODE(5)
实体名称节点 　 Node.ENTITY_NODE(6)
处理指令节点 　 Node.PROCESSING_INSTRUCTION_NODE(7)
注释节点 Node.COMMENT_NODE(8)
文档节点 Node.DOCUMENT_NODE(9)
文档类型节点 　 Node.DOCUMENT_TYPE_NODE(10)
文档片段节点 　 Node.DOCUMENT_FRAGMENT_NODE(11)
DTD 声明节点 Node.NOTATION_NODE(12)

## 同步任务

## 异步任务

# 箭头表达式

#### 和普通函数的区别

1.  this 指向 不同
    箭头的 this 指向外层函数的 this(在定义时就决定了)
2.  不能 new 不能做构造函数
3.  没有 prototype
4.  没有 arguments

# console 控制台对象语法

console.log

控制台 普通呈现

console.dir

控制台 呈现解构更清晰

将对象以表格的形式呈现

console.table

在控制台中显示 time->timeEnd 的代码的运行时间

console.time

console.timeEnd

# eval()

eval() 函数 会将传入的==字符串==当做 JavaScript 代码进行执行。

尽量别这么使用, 有可能会有外部恶意侵入

```js
eval(`console.log("123")`)
```

# 正则表达式

正则表达式是搜索和替换字符串的一种强大方式。
正则表达式（可叫作“regexp”或者“reg”）包含 ==模式*pattern*== 和可选的==修饰符*flags*==。

#### / 斜杠

- 是正则的边界符
  斜杠 "/" 会告诉 JavaScript 我们正在创建一个正则表达式。它的作用类似于字符串的引号。

#### 正则表达式中要使用到很多转义字符

- 为了通过字符串字面量给 RegExp 构造函数创建包含反斜杠的表达式，

- 你需要在<u>字符串级别</u>和<u>正则表达式级别</u>都对它进行转义。

- (意思是字符串时转义一次**`\`**,然后这个**`\`**再去转移其他的内容)

- 所有要在字符串中输入多一个**`\`**来转义字符

- ```js
  let = 'd.d' //d.d
  let = '\\d\\.\\d' //\d\.\d
  ```

#### 字面量 / \d /

- 两个斜杠之间

### 构造函数声明变量

#### let reg = new RegExp('u','g'); (标志,模式)

- ```js
  let arr = 'unfair'
  let a = 'u'
  let reg = new RegExp('u', 'g')
  let reg = new RegExp(a, 'g')

  reg.test(arr)
  ```

  new RegExp 允许从字符串中动态地构造模式。

---

### eval(\`str\`)

无返回

- 把字符串转换成 js 表达式
- ```js
  let arr = 'unfair'
  let a = 'u'
  eval(`/${a}/`).test(arr) //true 这个时候就可以用使用变量
  ```

## [字符串方法](https://zh.javascript.info/regexp-methods) ----------------------

### str.match(reg) 搜索

- 返回数组/null
- 无 `g` ： 它以数组的形式返回第一个匹配项，其中包含分组和属性 index（匹配项的位置）、input（输入字符串，等于 str）
  有 `g` ： 将所有匹配项的数组作为字符串返回，而不包含分组和其他详细信息。

- 没有匹配到 则返回`null`
  所以没找到匹配项就不是数组,更没有其他细节属性.
  如果我们希望结果始终是一个数组，我们可以这样写：
- ```js
  let matches = 'JavaScript'.match(/HTML/) || []
  ```

### str.matchAll(reg)

当我们搜索所有匹配项（标志 g）时，match 方法不会返回组的内容。

```js
let str = '<h1> <h2>'
let tags = str.match(/<(.*?)>/g)
alert(tags) // <h1>,<h2>
```

结果是一个匹配数组，但没有每个匹配项的详细信息。

### str.matchAll(regexp)

- 它返回的不是数组，而是一个==可迭代的对象==。
- 当==标志 g 存在时==，它将每个匹配组作为一个数组返回。
- 如果*没有匹配项*，则不返回 null，而是==返回一个空的可迭代对象==。

```js
let results = '<h1> <h2>'.matchAll(/<(.*?)>/gi)
results = Array.from(results) // 伪数组 ->真数组
alert(results[0]) // <h1>,h1 (1st tag)
alert(results[1]) // <h2>,h2 (2nd tag)
```

...或使用解构：

```js
let [tag1, tag2] = '<h1> <h2>'.matchAll(/<(.*?)>/gi)
```

### str.search(reg)

返回 index/-1

- 仅查找第一个匹配项。
  如果需要后续地匹配项的 `index`, 应该选择 `matchAll` 之类返回项更详细的方法.

### str.split(regexp|substr, limit) 正则 分割字符串

```js
str
alert('12-34-56'.split('-')) // 数组 ['12', '34', '56']
但同样，我们也可以用正则表达式来做：
reg
alert('12, 34, 56'.split(/,\s*/)) // 数组 ['12', '34', '56']
```

### str.replace(str|reg,str|func) 替换

- 当 replace 的==第一个参数是字符串==时，它仅替换第一个匹配项。

str 字符串

```Js
// 用冒号替换连字符
alert('12-34-56'.replace("-", ":")) // 12:34-56
```

reg 正则

```js
// 将连字符替换为冒号
alert('12-34-56'.replace(/-/g, ':')) // 12:34:56
```

#### 第二参数(str|func) : str (匹配替代)

| 符号      | 替换字符串中的操作                                                      |
| --------- | ----------------------------------------------------------------------- |
| $&        | 插入匹配的子串。                                                        |
| $`        | 插入当前匹配的子串左边的内容。                                          |
| $'        | 插入当前匹配的子串右边的内容。                                          |
| $n        | 如果 n 是 1-2 位数字，则插入第 n 个括号的内容，更多信息请参见捕获组一章 |
| $`<name>` | 用给定插入括号的内容 name，更多关于它在捕获组一章                       |
| $$        | 插入字符$                                                               |

#### 第二参数(str|func) : func (函数 替换格式化)

非常自定义、精细化的修改
函数 func(match, p1, p2, ..., pn, offset, input, groups) 带参数调用：
`match` － 匹配项，
`p1, p2, ..., pn` － 分组的内容（如有），
`offset` － 匹配项的位置，
`input` － 源字符串，
`groups` － 所指定分组的对象。
如果正则表达式中==没有括号==，则只有 3 个参数：func(str, offset, input)。
[replace 第二参详细实例](https://zh.javascript.info/regexp-methods#strreplacestrregexpstrfunc)包含

- 对 match 单独操作
- 用 rest 参数（…），收集参数，用序号传参
- 用最后一个参数（groups 对象），pop()获取就好

## [正则方法](https://zh.javascript.info/regexp-methods) ----------------------

### reg.exec(str)

- 如果没有 `g`，那么返回的第一个匹配与 `str.match` 完全相同。
- 当 reg 不用 `g` 时,lastIndex 始终返回 0

- 它返回一个数组（包含额外的属性 `index` 和 `input` ）（未匹配到则返回 null）
- 当用 `g` 时, 调用 regexp.exec(str) 会返回第一个匹配项，
  并将紧随其后的位置保存在属性 regexp.lastIndex 中。
  下一次同样的调用会从位置 regexp.lastIndex 开始搜索。
- `regexp.exec` 是 `str.matchAll` 方法的替代方法。(分解步骤)

### reg.test(str)

- 检验是否有匹配项
- 返回 布尔（T/F）
- 如果有 `g`，则 `regexp.test` 从 `lastIndex` 属性中查找，并更新此属性，就像 `regexp.exec` 一样。
- ```js
  let regexp = /love/gi
  let str = 'I love JavaScript'

  // 从位置 10 开始：
  regexp.lastIndex = 10
  alert(regexp.test(str)) // false（无匹配）
  ```

  ==！ 注意==：正则的方法，lastIndex 跟随正则式，可能会在测试时不为 0，可以预先调零，或用字符串方法。

### 选择符|

- 要满足|左边或右边任一表达式
  要检测 010-9999999 或者是 020-9999999

```js
/010\-\d{7,8}|020\-\d{7,8}/
//即010 或 020\-\d{7,8}
//或者用原子组()框住
/(010|020)\-\d{7,8}/
```

### 字符类（Character classes）

是一个特殊的符号，匹配特定集中的任何符号。
首先，让我们探索“数字”类。它写为`\d`，对应于“任何一个数字”。

`\d`（“d” 来自 “digit”）
数字：从 0 到 9 的字符。

`\s`（“s” 来自 “space”）
空格符号：包括空格，制表符\t、换行符\n、
其他少数稀有字符，例如 \v，\f 和 \r。

`\w`（“w” 来自 “word”）
“单字”字符：拉丁字母、数字、下划线 \_。非拉丁字母（如西里尔字母或印地文）不属于 \w。

### 反向类

对于每个字符类，都有一个“反向类”，用相同的字母表示，但要以大写书写形式
“反向”表示它与所有其他字符匹配，例如：
`\D`
非数字：除 \d 以外的任何字符，例如字母。

`\S`
非空格符号：除 \s 以外的任何字符，例如字母。

`\W`
非单字字符：除 \w 以外的任何字符，例如非拉丁字母或空格。

如何从 +7(903)-123-45-67 这样的字符串中创建一个==只包含数字==的电话号码: 找到所有的数字并将它们连接起来。

```Js
let str = "+7(903)-123-45-67";
alert( str.match(/\d/g).join('') ); // 79031234567
```

另一种快捷的替代方法是==查找非数字== \D 并将其从字符串中删除：

```Js
let str = "+7(903)-123-45-67";
alert( str.replace(/\D/g, "") ); // 79031234567
```

## 模式 pattern

|        字符        | 含义                                                                                                                                                                                                                                                                                 |
| :----------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
|         .          | （小数点）默认匹配<u>除换行符</u>之外的任何单个字符。                                                                                                                                                                                                                                |
|        \\.         | .                                                                                                                                                                                                                                                                                    |
|         ^          | 匹配输入的开始(第一位判断)                                                                                                                                                                                                                                                           |
|         $          | 匹配输入的结束(最后一位判断)                                                                                                                                                                                                                                                         |
|         \*         | 匹配前一个表达式 0 次或<u>多次</u>。 `等价于 {0,}`                                                                                                                                                                                                                                   |
|         ?          | 匹配<u>前面一个</u>表达式 0 次或者 1 次。(禁止贪婪) `等价于 {0,1}`                                                                                                                                                                                                                   |
|         +          | 匹配<u>前面一个</u>表达式 1 次或者<u>多次</u>(贪婪) `等价于 {1,}`                                                                                                                                                                                                                    |
|       (?:x)        | 匹配 'x' 但是不记住匹配项,这种括号叫作*非捕获括号*，<br />使得你能够定义与正则表达式运算符一起使用的==子表达式==。                                                                                                                                                                   |
|       x(?=y)       | 匹配'x'仅当'x'后面跟着'y'.这种叫做==先行断言==。                                                                                                                                                                                                                                     |
|      (?<=y)x       | 匹配'x'仅当'x'前面是'y'.这种叫做==后行断言==。                                                                                                                                                                                                                                       |
|       x(?!y)       | 仅当'x'后面不跟着'y'时匹配'x'，这被称为==先行否定查找==。                                                                                                                                                                                                                            |
|      (?<!y)x       | 仅仅当'x'前面不是'y'时匹配'x'，这被称为==后行否定查找==。                                                                                                                                                                                                                            |
|        x\|y        | 匹配'x'或者'y'。                                                                                                                                                                                                                                                                     |
|        {n}         | n 是一个正整数，匹配了前面一个字符刚好出现了 n 次。                                                                                                                                                                                                                                  |
|       {n,m}        | n 和 m 都是整数。匹配前面的字符至少 n 次，最多 m 次。<br />如果 n 或者 m 的值是 0， 这个值被忽略。                                                                                                                                                                                   |
| [abcd]<br />原子表 | 一个字符集合。匹配方括号中的任意字符，包括[转义序列](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Grammar_and_types)。<br />你可以使用破折号（-）来指定一个字符范围。<br />对于点（.）和星号（\*）这样的特殊符号在[]没有特殊的意义。<br />`[abcd]`和`[a-d]`是一样的 |
|      [^abcd]       | 一个反向字符集。它匹配任何没有包含在方括号中的字符。<br />`[^abcd]` 和 `[^a-d]` 是一样的。                                                                                                                                                                                           |
|        [\b]        | 匹配一个退格(U+0008)。（不要和\b 混淆了。）                                                                                                                                                                                                                                          |
|         \b         | 匹配一个词的边界。                                                                                                                                                                                                                                                                   |
|         \B         | 匹配一个非单词边界。                                                                                                                                                                                                                                                                 |
|         \d         | 匹配一个==数字== `等价于[0–9]`                                                                                                                                                                                                                                                       |
|         \D         | 匹配一个非数字字符 `等价于[^0–9]`                                                                                                                                                                                                                                                    |
|         \f         | 匹配一个换页符 (U+000C)。                                                                                                                                                                                                                                                            |
|         \n         | 匹配一个换行符 (U+000A)。                                                                                                                                                                                                                                                            |
|         \r         | 匹配一个回车符 (U+000D)。                                                                                                                                                                                                                                                            |
|         \s         | 匹配一个空白字符，包括空格、制表符、换页符和换行符                                                                                                                                                                                                                                   |
|         \S         | 匹配一个非空白字符                                                                                                                                                                                                                                                                   |
|         \t         | 匹配一个水平制表符 (U+0009)。                                                                                                                                                                                                                                                        |
|         \v         | 匹配一个垂直制表符 (U+000B)。                                                                                                                                                                                                                                                        |
|         \w         | 匹配一个单字字符（数字、字母、_ (下划线)）<br />`等价于 [A-Za-z0-9_]`                                                                                                                                                                                                                |
|         \W         | 匹配一个非单字字符 <br />`等价于 [^A-Za-z0-9_]`                                                                                                                                                                                                                                      |
|       \\_n_        |                                                                                                                                                                                                                                                                                      |
|         \0         | 匹配 NULL（U+0000）字符                                                                                                                                                                                                                                                              |
|        \xhh        | 匹配一个两位十六进制数（\x00-\xFF）表示的字符。                                                                                                                                                                                                                                      |
|       \uhhhh       | 匹配一个四位十六进制数表示的 UTF-16 代码单元。                                                                                                                                                                                                                                       |
|      \u{hhhh}      | (仅当设置了 u 标志时）匹配一个十六进制数表示的 Unicode 字符。<br />or \u{hhhhh}                                                                                                                                                                                                      |

### 锚点（Anchors)：字符串开始` ^` 和末尾` $`

插入符号 ^ 匹配文本开头，而美元符号 $ － 则匹配文本末尾。

- 测试完全匹配
  这两个锚点 `^...$` 放在一起常常被用于测试一个字符串是否完全匹配一个模式。

### 词边界：`\b`

词边界 `\b` 是一种检查，就像 `^` 和 `$` 一样。
当正则表达式引擎（实现搜索正则表达式的程序模块）遇到 `\b` 时，它会检查字符串中的位置是否是词边界。
有三种不同的位置可作为==词边界==：

- 在字符串开头，如果第一个字符是单词字符 `\w`。
- 在字符串中的两个字符之间，其中一个是单词字符 `\w`，另一个不是。
- 在字符串末尾，如果最后一个字符是单词字符 `\w`。
  即 连续的单词字符`\w`没有`\b`,
  有点像在描述两个字符间的区域。

可以在 Hello, Java! 中找到匹配 `\b`Java`\b` 的单词，其中 Java 是一个独立的单词，而在 Hello, JavaScript! 中则不行。

```js
alert('Hello, Java!'.match(/\bJava\b/)) // Java
alert('Hello, JavaScript!'.match(/\bJava\b/)) // null
```

<img src="./assets/Js 进阶.assets/1655563390808.jpg" alt="image-20220527222044573" style="zoom:70%;" />

这几个地方都是`\b`
`\b` 既可以用于单词，也可以用于==数字==。
模式`\b\d\d\b`查找独立的==两位数==。

```js
alert('1 23 456 78'.match(/\b\d\d\b/g)) // 23,78
alert('12,34,56'.match(/\b\d\d\b/g)) // 12,34,56
```

词边界 `\b` ==不适用于非拉丁字母==
词边界测试 `\b` 检查位置的一侧是否匹配 `\w`，而另一侧则不匹配 “`\w`”。

但是，\w 表示拉丁字母 a-z（或数字或下划线），因此此检查不适用于其他字符，如西里尔字母（cyrillic letters）或象形文字（hieroglyphs）。

### 特殊字符

这里是包含所有特殊字符的列表：`[ \ ^ $ . | ? * + ( )`。
转义 : 如果要把特殊字符作为==常规字符==来使用，只需要在它前面加个反斜杠。

- 斜杠 `/`
  斜杠符号 `/` 并不是一个特殊符号，但是它被用于在 Javascript 中==开启和关闭正则匹配==：/...pattern.../，所以我们也应该转义它。
- 反斜杠 `\`(用于转义)

字符串引号会消费其中的一个`\` (用字符串创建正则需要双倍`\`)

### 原子表`[]`

- 集合和范围 [...]
  在方括号 [...] 中的几个字符或者字符类意味着“搜索给定的字符中的任意一个”。

```js
alert('Exception 0xAF'.match(/x[0-9A-F][0-9A-F]/g)) // xAF
```

字符类是某些字符集的简写
例如：
`\d` —— 和 [0-9] 相同，
`\w` —— 和 [a-zA-Z0-9_] 相同，
`\s` —— 和 [\t\n\v\f\r ] 外加少量罕见的 unicode 空格字符相同。

#### 多语言 `\w`

`\w`还是有点局限,无法找到中文象形文字，西里尔字母等。
`[\p{Alpha}\p{M}\p{Nd}\p{Pc}\p{Join_C}]`

类似于 \w，我们在制作自己的一套字符集，包括以下 unicode 字符：
Alphabetic (Alpha) —— 字母，
Mark (M) —— 重读，
Decimal*Number (Nd) —— 数字，
Connector_Punctuation (Pc) —— 下划线 '*' 和类似的字符，
Join_Control (Join_C) —— 两个特殊代码 200c and 200d，用于连字，例如阿拉伯语。
使用示例：

```js
let regexp = /[\p{Alpha}\p{M}\p{Nd}\p{Pc}\p{Join_C}]/gu
let str = `Hi 你好 12`
alert(str.match(regexp)) // H,i,你,好,1,2
```

对于还没有实现此类匹配的浏览器, 可以使用==库== [XRegExp](http://xregexp.com/)

#### `[^...]` 除了[]之中的内容

- 排除范围

#### 在 `[...]` 中不需要转义 ~~`\`~~

在开头或者结尾表示一个破折号（在这些位置该符号表示的就不是一个范围）
pattern:`-`。(`0-9`表示范围, `-0-9`: `-`和 0-9 范围)
在不是开头的位置表示一个插入符号（在开头位置该符号表示的是排除）`^`。

如果集合中有代理对（surrogate pairs），则需要标志 u 以使其正常工作。

### 量词 `+,*,?` 和 `{n}`

- 数量 `{n}`
- 确切的位数：{5}
  \d{5} 表示 5 位的数字，如同 \d\d\d\d\d。
  我们可以添加 `\b` 来排除更多位数的数字：`\b\d{5}\b`。只能是 5 位数
- 某个范围的位数：{3,5}
  我们可以将限制范围的数字放入括号中，来查找位数为 3 至 5 位的数字：\d{3,5}
- 我们可以省略上限。那么正则表达式 \d{3,} 就会查找位数大于或等于 3 的数字：

```js
alert("I'm not 12, but 345678 years old".match(/\d{3,}/)) // "345678"
```

#### 量词缩写

`+`
代表“一个或多个”，相当于 `{1,}` 。
例如，`\d+` 用来查找所有数字：

```js
let str = '+7(903)-123-45-67'
alert(str.match(/\d+/g)) // 7,903,123,45,67
```

`?`
代表“零个或一个”，相当于 `{0,1}`。换句话说，它使得符号变得可选。
所以模式 `ou?r` 能够在 color 中找到 or，以及在 colour 中找到 our
`*`
代表着“零个或多个”，相当于 `{0,}`。也就是说，这个字符可以多次出现或不出现。

#### 实现: 正则表达式 “浮点数”（小数）：`\d+\.\d+`

```js
alert('0 1 12.345 7890'.match(/\d+\.\d+/g)) // 12.345
```

### 贪婪量词和惰性量词

- 贪婪模式
  在贪婪模式下（默认情况下），量词都会尽可能地重复多次。
  [贪婪模式 工作原理](https://zh.javascript.info/regexp-greedy-and-lazy#tan-lan-sou-suo)
  ==搜索到底再回退, 找最长匹配项==
- 懒惰模式
  懒惰模式中的量词与贪婪模式中的是相反的。它想要“重复最少次数”。
  [懒惰模式 工作原理](https://zh.javascript.info/regexp-greedy-and-lazy#lan-duo-mo-shi)
  ==步步谨慎, 搜索到最短匹配项就停==
  懒惰模式只能够通过带 ? 的量词启用
  其它的量词依旧保持贪婪模式。

- 替代方法(替代懒惰)
  [替代方法 工作原理](https://zh.javascript.info/regexp-greedy-and-lazy#ti-dai-fang-fa)
  在正则表达式中，通常有多种方法来达到某个相同目的。
  在用例中，我们能够在不启用懒惰模式的情况下用 `"[^"]+"` 找到带引号的字符串
  即 找到 `"` 就不会再继续贪婪了, 贪婪的前提是下一个字符属于模式。
  其表达了遇到第二个 `"` 就必须停止查找了。

#### 例子： 对于 /d+? d+?/ 的匹配

```js
alert('123 456'.match(/\d+? \d+?/g)) // 123 4
```

因为是从第一个开始查找，
第一个`\d+?`找到 123
第二个`\d+?`找到 4

#### 实例： 匹配注释

```Js
let reg = /<!--[\s\S]*?-->/g;
let str = `... <!-- My -- comment
 test --> ..  <!----> ..
`;
alert( str.match(reg) ); // '<!-- My -- comment \n test -->', '<!---->'
```

- 因为.匹配不了换行，用[\s\S]替代
  懒惰 0 个或多个用 `*？`

### 捕获组 原子组`()`

组合匹配
如果我们将量词放在括号后，则它将括号视为一个整体。

#### 实例：域名

例如：

```js
mail.com
users.mail.com
smith.users.mail.com
```

正如我们所看到的，一个域名由重复的单词组成，每个单词后面有一个点，除了最后一个单词。

在正则表达式中是 `(\w+\.)+\w+`
该模式无法匹配带有连字符的域名，例如 my-site.com，因为连字符不属于 \w 类。
我们可以通过用 `[\w-]` 替换 `\w` 来匹配除最后一个的每个单词：`([\w-]+\.)+\w+。`

#### 实例：email

前面的示例可以扩展。我们可以基于它为==电子邮件==创建一个正则表达式。
email 格式为：name@domain。名称可以是==任何单词，可以使用连字符和点==。在正则表达式中为 [-.\w]+。
模式：

```Js
let regexp = /[-.\w]+@([\w-]+\.)+[\w-]+/g;
alert("my@mail.com @ his@site.com.uk".match(regexp)); // my@mail.com, his@site.com.uk
```

该正则表达式并不完美的，但多数情况下都可以工作，并且有助于修复意外的错误类型。
==唯一真正可靠==的 email 检查只能通过发送 email 来完成。

#### 匹配括号中的内容

如果 regexp ==没有 g 标志==，将查找第一个匹配并将它作为一个数组返回
括号内的内容会在返回的数组的第二个元素之后中保存.

```js
let str = '<h1>Hello, world!</h1>'
let tag = str.match(/<(.*?)>/)
alert(tag[0]) // <h1>
alert(tag[1]) // h1
```

#### 嵌套组

在搜索标签 <span class="my"> 时我们可能会对以下内容感兴趣：
让我们为它们添加括号：`<(([a-z]+)\s*([^>]*))>`。
这是它们的编号方式（从左到右，由左括号开始）：
<img src="./assets/Js 进阶.assets/Snipaste_2022-06-20_01-32-40.jpg"  style="zoom: 65%;" >

```js
let str = '<span class="my">'
let regexp = /<(([a-z]+)\s*([^>]*))>/

let result = str.match(regexp)
alert(result[0]) // <span class="my">
alert(result[1]) // span class="my"
alert(result[2]) // span
alert(result[3]) // class="my"
```

#### 可选组

即使组是可选的并且在匹配项中不存在，也存在相应的 result 数组项，并且等于 ==undefined==。

```Js
let match = 'ac'.match(/a(z)?(c)?/)

alert( match.length ); // 3
alert( match[0] ); // ac（完全匹配）
alert( match[1] ); // undefined，因为 (z)? 没匹配项
alert( match[2] ); // c
```

数组长度是恒定的：3, 所以结果是 ["ac", undefined, "c"].

#### 命名组

用数字记录组很困难。所以就给括号起个名字。
这是通过在开始括号之后立即放置 `?<name>` 来完成的。
例如，让我们查找 `year-month-day` 格式的日期：

```Js
let dateRegexp = /(?<year>[0-9]{4})-(?<month>[0-9]{2})-(?<day>[0-9]{2})/;
let str = "2019-04-30";
let groups = str.match(dateRegexp).groups;
alert(groups.year); // 2019
alert(groups.month); // 04
alert(groups.day); // 30
```

我们还需要 matchAll 获取完整的组匹配：

```Js
let dateRegexp = /(?<year>[0-9]{4})-(?<month>[0-9]{2})-(?<day>[0-9]{2})/g;
let str = "2019-10-30 2020-01-01";

let results = str.matchAll(dateRegexp);
for(let result of results) {
  let {year, month, day} = result.groups;
  alert(`${day}.${month}.${year}`);
  // 第一个: 30.10.2019
  // 第二个: 01.01.2020
}
```

#### 替换捕获组

方法 str.replace(regexp, replacement) 用 replacement 替换 str 中匹配 regexp 的所有捕获组。这使用 来完成，==其中 n 是组号==。

```Js
let str = "John Bull";
let regexp = /(\w+) (\w+)/;
alert( str.replace(regexp, '$2, $1') ); // Bull, John
```

对于命名括号，引用为 $<name>。
例如，让我们将日期格式从 “year-month-day” 更改为 “day.month.year”：

```js
let regexp = /(?<year>[0-9]{4})-(?<month>[0-9]{2})-(?<day>[0-9]{2})/g
let str = '2019-10-30, 2020-01-01'
alert(str.replace(regexp, '$<day>.$<month>.$<year>'))
// 30.10.2019, 01.01.2020
```

#### 非捕获组 ?:

可以通过在开头添加 ?: 来排除组。
例如，如果我们要查找 `(go)+`，但不希望括号内容`（go）`作为一个单独的数组项，则可以编写：`(?:go)+`。
在下面的示例中，我们仅将名称 John 作为匹配项的单独成员：

```Js
let str = "Gogogo John!";
// ?: 从捕获组中排除 'go'
let regexp = /(?:go)+ (\w+)/i;

let result = str.match(regexp);
alert( result[0] ); // Gogogo John（完全匹配）
alert( result[1] ); // John
alert( result.length ); // 2（数组中没有更多项）
```

### 总结

- 括号将正则表达式的一部分组合在一起，以便量词可以整体应用。
  括号组从左到右编号，可以选择用 (`?<name>...`) 命名。
  可以在结果中获得按组匹配的内容：

- 方法 str.match 仅当不带标志 g 时返回捕获组。
  方法 str.matchAll 始终返回捕获组。
  如果括号没有名称，则匹配数组按编号提供其内容。命名括号还可使用属性 groups。

- 我们还可以使用 str.replace 来替换括号内容中的字符串：使用 `$n` 或者名称 `$<name>`。
  可以通过在组的开头添加 `?:` 来排除编号组。当我们需要对整个组应用量词，但不希望将其作为结果数组中的单独项时这很有用。我们也不能在替换字符串时引用此类括号。

### 模式中的反向引用：`\N`

\1 在模式中进一步的含义是“查找与第一（捕获）分组相同的文本”，在我们的示例中为完全相同的引号。
与此类似，\2 表示第二（捕获）分组的内容，\3 – 第三分组，依此类推。

```Js
let str = `He said: "She's the one!".`;

let regexp = /(['"])(.*?)\1/g;
alert( str.match(regexp) ); // "She's the one!"
```

如果我们在组中使用 ?:，那么我们将无法引用它。用 (?:...) 捕获的组被排除，==引擎不会存储== `?:`。
==不要搞混了： 在模式中用== `\1`，==在替换项中用：== `$1`

### 按命名反向引用：`\k<name>` (命名`?<name>`)

如果正则表达式中有很多括号对（注：捕获组），给它们起个名字方便引用。
要引用命名组，我们可以使用：\k<name>。
在下面的示例中引号组命名为 ?<quote>，因此反向引用为 \k<quote>：

```Js
let str = `He said: "She's the one!".`;
let regexp = /(?<quote>['"])(.*?)\k<quote>/g;
alert( str.match(regexp) ); // "She's the one!"
```

### 选择（OR）|

我们已知的一个==相似==符号 —— 方括号。
选择符号并非在字符级别生效，而是在==表达式级别==生效。

```Js
let reg = /([01]\d|2[0-3]):[0-5]\d/g;
alert("00:00 10:10 23:59 25:99 1:2".match(reg));
\// 00:00,10:10,23:59
```

### 前瞻断言与后瞻断言

前瞻和后瞻断言都是针对 标志匹配项的 它们不是最终匹配的内容, 用于辅助匹配.

#### 前瞻

- 前瞻肯定断言: x(?=y), 匹配 x, 仅在后面是 y 的情况。
  前瞻否定断言: x(?!y), 匹配 x, 仅在后面不是 y 的情况。

```js
let str = '1 turkey costs 30€'
alert(str.match(/\d+(?=€)/)) // 30 （正确地跳过了单个的数字 1）

let str = '2 turkeys cost 60€'
alert(str.match(/\d+(?!€)/)) // 2（正确地跳过了价格）
```

#### 后瞻

- 后瞻肯定断言: (?<=y)x, 匹配 x, 仅在前面是 y 的情况。
  后瞻否定断言: (?<!y)x, 匹配 x, 仅在前面不是 y 的情况。

```js
let str = '1 turkey costs $30'
alert(str.match(/(?<=\$)\d+/)) // 30 （跳过了单个的数字 1）

let str = '2 turkeys cost $60'
alert(str.match(/(?<!\$)\d+/)) // 2 (跳过了价格)
```

在模式 \d+(?!€) 中，€ 符号就不会出现在匹配结果中。
但是如果我们想要捕捉整个==环视表达式==或其中的一部分，那也是有可能的。只需要将其包裹在另加的括号中。
例如，这里货币符号 (€|kr) 和金额一起被捕获了：

```js
let str = '1 turkey costs 30€'
let reg = /\d+(?=(€|kr))/ // €|kr 两边有额外的括号
alert(str.match(reg)) // 30, €
```

### 灾难性回溯

有些正则表达式看上去很简单，但是执行起来耗时非常非常非常长，甚至会导致 JavaScript 引擎「挂起」。
主要是排列组合让引擎考虑多种结果, 尽量让结果唯一,对引擎就语义都好.
占有型量词:
有助于帮助正则把一个单词,一整个更具语义的内容作为匹配项.当有匹配后便不再匹配此单词后续内容.

#### 我们有 2 种处理它的思路：

1. 重写正则表达式，尽可能减少其中排列组合的数量。
2. 防止回溯。

## flag 表

|    标志    | 描述                                                                                             |
| :--------: | :----------------------------------------------------------------------------------------------- |
| `g` global | 全局搜索。(搜索时会查找所有的匹配项)                                                             |
| `i` ignore | 不区分大小写搜索。                                                                               |
|    `m`     | 多行搜索。(单行处理)                                                                             |
|    `s`     | 允许 **`.`** 匹配换行符。(视为==单行匹配==,匹配任何字符)**("dotAll")**                           |
|    `u`     | 使用 unicode 码的模式进行匹配。<br />开启完整的 unicode 支持。该修饰符能够修正对于代理对的处理。 |
|    `y`     | 执行“粘性(`sticky`)”搜索,匹配从目标字符串的当前位置开始。                                        |

## Flag "u"

大多数字符使用 2 个字节编码，但这种方式只能编码最多 65536 个字符。
这个范围不足以对所有可能的字符进行编码，这就是为什么一些罕见的字符使用 4 个字节进行编码

Unicode 中的每一个字符都具有很多的属性。
它们描述了一个字符属于哪个“类别”，包含了各种关于字符的信息。
在下面的例子中 3 种字母将会被查找出：英语、格鲁吉亚语和韩语。

```Js
let str = "A ბ ㄱ";
alert( str.match(/\p{L}/gu) ); // A,ბ,ㄱ
```

[主要的字符类别和它们对应的子类别](https://zh.javascript.info/regexp-unicode#unicode-shu-xing-unicodepropertiesp)
[相关的链接](https://unicode.org/cldr/utility/character.jsp)
[相关例子视频](https://www.bilibili.com/video/BV1NJ411W7wh?p=291&spm_id_from=pageDriver&vd_source=a01a6b5f172f99e81e9ebc2b4552722b)

### 中文字符

为了实现查找一个给定的书写系统中的字符，我们需要使用 Script=`<value>`
==\p{sc=Han}==

```js
let regexp = /\p{sc=Han}/gu // returns Chinese hieroglyphs
let str = `Hello Привет 你好 123_456`
alert(str.match(regexp)) // 你,好
```

### 货币

表示货币的字符，例如 $，€，¥，具有 unicode 属性 \p{Currency_Symbol}，缩写为 ==\p{Sc}==。

```Js
let regexp = /\p{Sc}\d/gu;
let  str = `Prices: $2, €1, ¥9`;
alert( str.match(regexp) ); // $2,€1,¥9
```

### Flag "m" — 多行模式

这仅仅会影响 ^ 和 $ 锚符的行为。
在多行模式下，它们不仅仅匹配文本的开始与结束，还匹配==每一行的开始与结束==。
[相关例子视频](https://www.bilibili.com/video/BV1NJ411W7wh?p=290&vd_source=a01a6b5f172f99e81e9ebc2b4552722b)

### Flag "y"

如果没有标志 "g"，属性 lastIndex 会被忽略
==手动设置==
用标志 `g` 属性 `lastIndex` 设置搜索的起始位置。
从设置的地方开始查找, 可以在目标匹配项之前或者刚好开始位置
即 如果在 lastIndex 位置上没有词，但它在后面的某个地方，那么它就会被找到.

```js
let str = 'let varName = "value"'
let regexp = /\w+/g
regexp.lastIndex = 4
let word = regexp.exec(str)
alert(word) // varName

let str = 'let varName = "value"'
let regexp = /\w+/g
regexp.lastIndex = 3
let word = regexp.exec(str)
alert(word[0]) // varName
alert(word.index) // 4
```

使用标志 `y` 是获得良好性能的关键。
它不会盲目地寻找匹配项(如`g`), 而是从指定位置开始搜寻, 没有就算了.
标记 `y` 使 regexp.exec 正好在 `lastIndex` 位置，而不是在它之前，也不是在它之后。

```js
let str = 'let varName = "value"'
let regexp = /\w+/y
regexp.lastIndex = 3
alert(regexp.exec(str)) // null（位置 3 有一个空格，不是单词）

regexp.lastIndex = 4
alert(regexp.exec(str)) // varName（在位置 4 的单词）
```

## 想匹配任何字符

/./s 匹配任何字符,允许匹配换行符
/[\s\S]/ (匹配空白字符或非空白字符
/[\d\D]/ (匹配数字或非数字字符
