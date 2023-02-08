浏览器中有Js解释器

Js 是 解释一句执行一句的，所以报错处停止执行。

Js 是 客户端的脚本语言

<img src="./assets/Js 基础.assets\image-20220326095307391.png" alt="image-20220326095307391" style="zoom:33%;" />



## 浏览器输入输出

```js
console.log('123');(console控制台和log日志)
	输出多个变量用 , 分隔即可
alert('警示框');
prompt('弹出用户输入框');
	取值为字符型(string)
```



# 变量

变量：程序在内存中申请的一块用来存放数据的空间。

`变量的使用`：

1.  声明

    -   （用var(variable)关键字声明变量）

    -   ```js
        var age；
        ```

2.  赋值

    -   ```javascript
        age = 18；
        ```

3.  声明一个变量并赋值，我们称之为变量的 `初始化`。

    -   ```js
        var age = 18；
        ```

4.  声明多个变量，用 `,` 逗号隔开

    -   ```javascript
        var age1 = 18，
        	age2 = 18，
            age3 = 18；
        ```

5.  特殊的变量声明情况

    -   ```js
        // 只声明，未赋值
        var age;
        console.log(age);// undefined(类型为未定义)
        
        // 直接使用
        console.log(age); // 报错
        
        // 没用var关键字
        age = 18；
        console.log(age); // 18
        ```

6.  变量命名规范

    -   由字母(A-Za-z)、数字(0-9)、下划线(_)、美元符号($)组成，
    -   严格区分大小写。
    -   不能以数字开头。18age是错误的
    -   不能是关键字、保留字。例如：var、for、while
    -   变量名最好有意义。age
    -   遵守驼峰命名法。首字母小写，后面单词的首字母需要大写。myFirstName



# 数据类型

在计算机中，不同的数据所需占用的存储空间是不同的，为了便于把数据分成所需内存大小不同的数据，充分利用存储空间，于是定义了不同的数据类型。

-   Js属于弱类型语言
-   Js是动态语言，变量的数据类型可以变化
-   Js的数据类型根据值来判断。



| 简单数据类型       | 说明                                           | 默认值        |
| ------------------ | ---------------------------------------------- | ------------- |
| Number 数字型      | 包含整型值和浮点型值                           | 如21、0.21、0 |
| Boolean 布尔值类型 | 如true、false,等价于1和0                       | false         |
| String 字符串类型  | 如注意咱们js里面，字符串都带引号               | "张三"        |
| Undefined          | var a;，此时a=undefined声明了变量a但是没有给值 | undefined     |
| Null               | vara=null;声明了变量a为空值                    | null          |

---

### Number 数字型

1.  八进制

    -   var num = 010; (：前面加0) // 8

2.  十六进制

    -   var num = 0x10; (前面加0x) // 16

3.  Js中的最大值

    -   Number.MAX_VALUE //1.7976931348623157e+308
    -   Number.MIN_VALUE // 5e-324

4.  特殊值

    -   无穷大：比最大值大 Infinity

    -   无穷大：比最大值大 -Infinity

5.  非数字

    -   NaN - 非数字 （Not a Number） 
    -   console.1og('pink老师'-10); // NaN

6.  isNaN(传参) 

    -   判断非数字
        -   非数字 — 1
        -   赎罪 — 0

---

### String 字符串类型

1.  字符串引号嵌套（双引号单引号间隔嵌套）
    -   "我'爱'你"
2.  字符串转义字符 （均以\开头）
    -   `\n` 换行符（n是newline的意思）
    -   `\\` 斜杠\
    -   `\'` ' 单引号
    -   `\"` " 双引号
    -   `\t` 制表符，tab缩进
    -   `\b` 空格，b是blank的意思
3.  length 返回字符串长度
    -   str.length
4.  字符串的拼接 ( 字符串 + 其他类型相 = 字符串类型 )
    -   console.1og('沙漠' + '骆驼'); //'沙漠骆驼'
        console.1og('pink老师' + 18); //'pink老师18'
        console.log('pink' + true); //'pinktrue'
        conso1e.1og('12' + 12); //'1212'

---

### Boolean 布尔值类型

只有 true 和 false 两种

---

### Undefined 未定义 和 Null 空值

```js
//undefined 未定义
var v undefined;
console.log(v + 'pink'); // 'undefinedpink'
console.log(v + 1); // NaN 
undefined和数字相加最后的结果是 NaN

//null 空值
var n null;
console.log(n +'pink');// 'nullpink'
console.log(n + 1); // 1
```

---

### typeof (运算符/关键字)

-   ```js
    var num 10;
    console.log(typeof num); //number
    var timer null;
    console.log(typeof timer); //object
    ```



### 字面量

数组字面量 []

数字字面量 18

字符串字面量 'wo'

对象字面量 {}



### 数据类型转换

`转换成字符串型`

| 方式            | 说明     | 案例         |
| --------------- | -------- | ------------ |
| toString()      | 属性     | num.toString |
| <u>String()</u> | 函数     | String(num)  |
| 加一个字符串    | 隐式转换 | num+''(空值) |

`转换成数字型`

| 方式                        | 说明                         | 案例                             |
| --------------------------- | ---------------------------- | -------------------------------- |
| parselnt(string)函数        | 将string类型转成整数数值型   | parseInt('78')                   |
| parseFloat(string)函数      | 将string类型转成浮点数数值型 | parseFloat('78.21')              |
| <u>Number()</u>强制转换函数 | 将string类型转换为数值型     | Number('12')                     |
| js隐式转换(- * /)           | 利用算术运算隐式转换为数值型 | '12' - 0         '12' * 1(+不行) |

`转换成布尔型`

| 方式          | 说明               | 案例             |
| ------------- | ------------------ | ---------------- |
| Boolean()函数 | 其他类型转成布尔值 | Boolean('true'); |

-   ```js
    console.log(Boolean('')); //false
    console.log(Boolean(0)); //false
    console.log(Boolean(NaN)); //false
    console.log(Boolean(null)); //false
    console.log(Boolean(undefined)); //false
    
    //除了以上内容，其余的都为true
    console.1og(Boolean('小目'))；//true
    console.log(Boolean(12));//true
    ```




1.标识(zhi)符
就是指开发人员为变量、属性、函数、参数取的名字。
标识符不能是 `关键字` 或 `保留字` 。

2.关键字
是指S本身已经使用了的字，不能再用它们充当变量名、方法名。

3.保留字
实际上就是预留的“关键字”，意思是现在虽然还不是关键字，但是未来可能会成为关键字，同样不能使用它们当变量名或方法名。



# 运算符

#### 算数运算符

运算符(operator)也被称为操作符，是用于实现赋值、比较和执行算数运算等功能的符号。



浮点数的精度问题

-   浮点数值的最高精度是17位小数，但在进行算术计算时其精确度远远不如整数。

-   所以：不要直接判断两个浮点数是否相等！

表达式

-   是由数字、运算符、变量等以能求得数值的有意义排列方法所得的组合

-   表达式最终都会有一个结果，返回给我们，我们成为 `返回值`



#### 递增(减)运算符

前置递增(减)

-   先加加，后使用

```js
let age = 18;
num = ++age;
console.log(num); //19
console.log(age); //19
```

后置递增(减)

-   先使用，后加加

```js
let age = 18;
num = age++;
console.log(num); //18
console.log(age); //19
```

#### 关系运算符

```js
> >= <= < = == === != !==
```

| 符号 | 作用 | 用法                                     |
| ---- | ---- | ---------------------------------------- |
| =    | 赋值 | 把右边给左边                             |
| ==   | 判断 | 判断两边值是否相等（注意此时有隐式转换） |
| ===  | 全等 | 判断两边的值和数据类型是否完全相同       |

#### 逻辑运算符

| 逻辑运算符 | 说明                   | 案例          |
| ---------- | ---------------------- | ------------- |
| &&         | "逻辑与"，简称"与" and | true&&false   |
| \|\|       | "逻辑或"，简称"或” or  | true\|\|false |
| ！（取反） | "逻辑非"，简称"非" not | ！true        |

#### 短路运算（逻辑中断）

逻辑与&&短路

-   遇假中断，返回假值，遇真继续，无假反最后值

逻辑或||短路

-   遇真中断，返回真值，遇假继续，无真反最后值

-   ```js
    let num = 0;
    console.log( 123 || ++num); (短路中断，没有运行++num)
    console.log(num); // 0;
    ```

#### 赋值运算符

| 赋值运算符 | 说明                   | 案例                    |
| ---------- | ---------------------- | ----------------------- |
| =          | var usrName='我是值'： | 直接赋值                |
| +=、-=     | 加、减一个数后在赋值   | var age 10;age+=5; //15 |
| *=、/=、%= | 乘、除、取模后在赋值   | var age 2;age*=5; //10  |

#### 运算符优先级

| 优先级 | 运算符     | 顺序             |
| ------ | ---------- | ---------------- |
| 1      | 小括号     | ()               |
| 2      | 一元运算符 | ++、!            |
| 3      | 算数运算符 | 先*、/、% 后+、- |
| 4      | 关系运算符 | > >=  < <=       |
| 5      | 相等运算符 | == != === !==    |
| 6      | 逻辑运算符 | 先&& 后 \|\|     |
| 7      | 赋值运算符 | =                |
| 8      | 逗号运算符 | ,                |



# 流程控制

在一个程序执行的过程中，各条代码的执行顺序对程序的结果是有直接影响的。很多时候我们要通过控制代码的执行顺序来实现我们要完成的功能。

流程控制主要有三种结构，分别是`顺序结构`、`分支结构`和`循环结构`，这三种结构代表三种代码执行的顺序。

<img src="./assets/Js 基础.assets\image-20220326105436419.png" alt="image-20220326105436419" style="zoom:33%;" />

## 分支结构

#### if语句

-   按照从大到小的判断思路

```js
if(条件表达式){ //为真执行
	//执行语句1
}else{
	//执行语句2    
}

//多分支语句

if(条件表达式){ //为真执行
	//执行语句1
}else if{
	//执行语句2    
}
```

#### 三元表达式

有三元运算符组成的式子称为三元表达式。

条件表达式 ？表达式1：表达式2

-   ```js
    var num = 10；
    var num2 = num > 10 ? num : 10 //10
    
    el:为0~59中0~9的数字前面补0
    var result = input > 10 ? input : '0' + input
    ```

#### switch语句

switch语句也是多分支语句，它用于基于不同的条件来执行不同的代码。当要针对变量设置一系列的特定值的选项时，就可以使用switch。

```js
switch(条件表达式){
    case value1:
        执行语句1;
		break;
	case value2:
        执行语句2;
		break;
    default:
        执行语句3;
}
```

条件表达式 和 case里的值 是以===全等匹配的

没有break;不会停止执行,而是直接执行下一个case

**同样语义的情况下,switch的效率更高一些**



## 循环结构

在实际问题中，有许多具有规律性的重复操作，因此在程序中要完成这类操作就需要重复执行某些语句

#### for循环语句

在程序中，一组被重复执行的语句被称之为`循环体`，能否继续重复执行，取决于循环的终止条件。由循环体及循环的`终止条件`组成的语句，被称之循环语句

-   ```js
    for(初始化变量；条件表达式；操作表达式){
    	//循环体
    }
    ```

#### while循环语句

whl语句可以在条件表达式为真的前提下，循环执行指定的一段代码，直到表达式不为真时结束循环while语句的语法结构如下：

-   ```js
    var i = 0;(初始化变量)
    while(条件表达式){
    	//循环体
        i++;(操作表达式)
    )
    ```

#### do while循环语句

-   ```js
    var i = 0;(初始化变量)
    do
    	//循环体
        i++;(操作表达式)
    }while(条件表达式)
    ```

#### continue 关键字

continue关键字用于立即跳出本次循环，继续下一次循环（直接跳到操作表达式）
（本次循环体中continue之后的代码就会少执行一次)。

#### break关键字

break关键字用于立即跳出整个循环（循环结束）。



# Js的语法规范

#### 标识符命名规范

-   变量、函数的命名必须要有意义
-   变量的名称一般用名词
-   函数的名称一般用动词、

#### 操作符规范

操作符的左右两侧各保留一个空格

#### 单行注释规范

// 单行注释前面注意有个空格



# 数组Array

数组是指一组数据的集合，其中的每个数据被称作元素，在数组中可以存放任意类型的元素。

-   ```js
    var arr=new Array(); //创建了一个空的数组对象
    var arr=[]; //创建了一个空的数组
    ```

数组的索引

-   索引（下标）：用来访问数组元素的序号（数组下标从0开始）。

超出数组空间的为undefined

-   ```js
    var arr = ['wo','ui'];
    console.log(arr[2]) // undefined
    ```

数组长度(数组元素个数) .length

-   ```
    arr.length
    ```

#### 数组扩容

-   ```js
    var arr ['red',green','blue','pink']
    arr.length =6;
    console.log (arr);
    console.log(arr[4]); //undefined
    console.log(arr[5]); //undefined
    ```

#### 新数组顺序存储索引规律

-   ```js
    let newArr = [];
    newArr[newArr.length] = value;
    //每次新加入一个值，长度自动加一。
    ```

-   倒叙数组

    -   ```js
        let arr = ['1','2','3'];
        let newArr = [];
        for(let i = arr.length-1; i>=0 ; i--){
            newArr[newArr.length] = arr[i];
        }
        console.log(newArr); // ['3','2','1']
        ```

#### 冒泡排序

是一种算法，把一系列的数据按照一定的顺序进行排列显示（从小到大或从大到小）。

```js
var arr = [4, 1, 2, 3, 5];
for (var i = 0; i <= arr.length - 1; i++) { //外层循环管趟数
    //里面的循环管每一趟的交换次数
    for (var j = 0; j <= arr.length - i - 1; j++) { 
        //前一个和后面一个数组元素相比较
        if (arr[j] > arr[j + 1]) {
            var temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
        }
    }
}
```



# 函数

在Js里面，可能会定义非常多的相同代码或者功能相似的代码，这些代码可能需要大量重复使用。虽然for循环语句也能实现一些简单的重复操作，但是比较具有局限性，此时我们就可以使用S中的函数。

**提高代码的复用率**



1.  声明函数
    1.  `function` 声明函数的关键字
    2.  函数是做某件事情，函数名一般是动词
    3.  函数不调用，自己不执行
2.  调用函数
    -   函数名()；
3.  函数的封装
    -   函数的封装是把一个或者多个功能通过函数的方式封装起来，对外只提供一个简单的函数`接口`

### 形参和实参

在声明函数的小括号里面是形参（形式上的参数）

在函数调用的小括号里面是实参（实际的参数）

```
function函数名（形参1,形参2,...）{
}
cook(实参1,实参2，...);
```

#### 函数传参，实参和形参数量可以不一致

多了就跳过，

少了形参会当作undefined。

-   ```js
    function函数名（num1,num2）{
    	console.log(num1+num2);
    }
    cook(1); // NaN (num2为接受到实参传来的值，所以为赋值变量undefined)
    ```

#### return 返回值（终止函数）

-   `return` 语句之后的代码不被执行。

-   ```js
    function getsum(num1,num2){
    	return num1 + num2;
    }
    console.log(getsum(1,2));
    ```

-   `return` 只能返回一个值

-   函数没有 `return` 返回undefined



#### `break`,`continue`,`return`的区别

-   `break`:结束当前的循环体（如for、while)
-   `continue`: 跳出本次循环，继续执行下次循环（如for、while)
-   `return`: 不仅可以退出循环，还能够返回return语句中的值，同时还可以结束当前的函数体内的代码。



#### arguments

-   当我们**不确定有多少个参数**传递的时候，可以用arguments来获取。
-   在JavaScript中，arguments实际上它是当前函数的一个内置对象。
-   所有函数都内置了一个arguments对象
-   arguments对象中存储了传递的所有实参。（以伪数组的形式）
-   arguments的使用只有函数才有

-   伪数组
    -   并不是真正意义上的数组
    -   具有数组的length属性
    -   按照索引的方式进行存储的
    -   它没有真正数组的一些方法，pop()、push()等等



#### 函数是可以相互调用的

#### 函数的2种声明方式

1.  利用函数关键字自定义函数（命名函数）

    -   ```js
        function fn(){
            console.1og('我是函数表达式')；
        }
        fn();
        ```

    -   fun 是函数名。

2.  函数表达式（匿名函数）

    -   ```js
        var fun = function(){
        	console.1og('我是函数表达式')；
        }
        fun();
        ```

    -   fun 是变量名不是函数名。



# 作用域

-   通常来说，一段程序代码中所用到的名字并不总是有效和可用的，而限定这个名字的可用性的代码范围就是这个名字的作用域。
-   作用域的使用提高了程序逻辑的局部性，增强了程序的可靠性，减少了名字冲突。



#### 全局作用域：

-   整个script标签或者是一个单独的js文件。

#### 局部作用域（函数作用域）：

-   在函数内部就是局部作用域这个代码的名字只在函数内部起效果和作用。

#### 块级作用域

-   在{}内部就是局部作用域这个代码的名字只在函数内部起效果和作用。



#### 变量的作用域：

-   根据作用域的不同我们变量分为全局变量和局部变量
-   全局变量
    -   在全局作用域下的变量，在全局下都可以使用
-   局部变量
    -   在局部作用域下的变量，只能在函数内部使用
    -   函数的形参也可以看做是局部变量
-   从执行效率来看全局变量和局部变量
    -   全局变量只有浏览器关闭的时候才会销毁，**比较占内存资源**
    -   局部变量当我们程序执行完毕就会销毁



#### 作用域链

-   根据在内部函数可以访问外部函数变量的这种机制，用链式查找决定哪些数据能被内部函数访问，就称作 作用域链

-   就近原则（向外层查找变量）

全局为0级链，向内一层块级域为1级链，以此类推



# 预解析

-   JavaScript代码是由浏览器中的`JavaScript解析器`来执行的。

-   JavaScript解析器在运行JavaScript代码的时候分为两步：`预解析`和`代码执行`

    -   预解析
        -   `js引擎`会把js里面所有的`var`还有`function`**提升**到当前作用域的最前面

    -   代码执行
        -   按照代码书写的顺序从上往下执行

-   预解析分为变量预解析（变量提升）和函数预解析（函数提升）

    -   变量提升

        -   把所有的`变量声明`提升到当前的作用域最前面 不提升赋值操作

        -   ```js
            fun();
            var fun = function(){
            	console.log(22);
            )
            console.log(f);
            var f = 0;
                
            //相当于
            var fun；
            var f；
            fun();
            fun = function(){
            	console.log(22);
            )
            console.log(f);
            f = 0;
            //仅提升声明部分
            ```

    -   函数提升

        -   把所有的`函数声明`提升到当前作用域的最前面 不调用函数

        -   ```js
            fun();
            function fun(){
            	console.log(22);
            )
            //相当于
            function fun(){
            	console.log(22);
            )
            fun();
            //完整可调用的函数被提升
            ```



# 对象 Object

-   **对象为复杂数据类型**

-   现实生活中：万物皆对像，对像是一个具体的事物，看得见摸得着的实物。
    -   例如，一本书、一辆汽车、一个人可以是“对象”，一个数据库、一张网页、一个与远程服务器的连接也可以是“对像”。
-   在JavaScript中，对像是一组**无序的相关属性和方法的集合**，所有的事物都是对象，例如字符串、数值、数组、函数等。
-   对象是由`属性`和`方法`组成的。
    -   属性：事物的特征，在对象中用属性来表示（常用名词）
    -   方法：事物的行为，在对象中用方法来表示（常用动词）
-   Js中的对象表达结构更清晰，更强大。



### 对象的几个原则

-   属性或者方法我们采取`键值对`的形式
-   多个属性或者方法中间用逗号`，`隔开的
-   方法冒号后面跟的是一个`匿名函数`

```js
var obj = {
	name: 'john', // 属性
	age:18,  // 属性
	show:function(){ // 方法
		console.log('john');
	}
}
```

#### 使用对象的属性

1.  调用对象的属性我们采取`对象名.属性名`
2.  调用属性还有一种方法 `对象名['属性名']`

#### 调用对象的方法

1.  调用对象的方法我们采取`对象名.方法名`

#### 变量与属性的异同

-   变量和属性的相同的他们都是用来`存储数据`的

-   `变量` 单独声明并赋值 使用的时候直接写变量名 单独存在
-   `属性` 在对象里面的不需要声明的 使用的时候必须是以对象的属性的形式出现

#### 函数与方法的异同

-   函数和方法的相同点都是实现某种功能做某件事
-   `函数` 是单独声明并且调用的 函数名()单独存在的
-   `方法` 在对象里面 调用的时候 对象.方法()




### 创建对象的三种方法

1.  利用字面量创建对象

    -   ```js
        var obj = {}；
        var obj = {
        	name: 'john', // 属性
        	age:18,  // 属性
        	show:function(){ // 方法
        		console.log('john');
        	}
        }
        ```

2.  利用new Object创建对象

    -   ```js
        var obj = new object();
        obj.name = 'john'; 
        ```

    -   我们是利用等号 = 赋值的方法添加对象的属性和方法

3.  利用构造函数创建对象

    -   重复创建对象

    -   构造函数就是把我们对象里面一些相同的属性和方法抽象出来封装到函数里面

    -   ```js
        function Star(uname,age,sex){
        	this.name = uname;
        	this.age = age;
        	this.sex sex;
        }
        var ldh = new Star('刘德华，18，'男);
        ```

#### 构造函数：

-   是一种特殊的函数，主要用来初始化对像，即为对象成员变量赋初始值

-   它总与new运算符一起使用。

-   我们可以把对象中一些公共的属性和方法抽取出来，然后封装到这个函数里面。

-   ```js
    function 构造函数名(){
    	this.属性 = 值；
    	this.方法 = function(){}；
    new 构造函数名()； 
    ```

-   **构造函数名开头大写**

-   我们调用 构造函数 必须使用 `new`

-   我们构造函数**不需要return**就可以返回结果

#### 构造函数 与 对象的描述

-   构造函数 相当于一个大类 泛指
-   对象 相当于一个具体的事物 特指 （也叫实例）

-   我们利用构造函数创建对象的过程我们也称为**对象的实例化**

#### new关键字执行过程

1.  new构造函数可以在内存中创建了一个`空的对象`
2.  this就会指向刚才创建的空对象
3.  执行构造函数里面的代码给这个空对象添加属性和方法
4.  返回这个对象



#### for in 遍历对象

-   ```js
    for(var k in obj){
    	console.1og(k);			//k -- 属性名
    	console.1og(obj[k]); 	//obj[k] -- 是属性值
    }
    ```



## JavaScript中的对象分为3种：

#### 自定义对像、内置对象、浏览器对象

-   前面两种对象是S基础内容，属于ECMAScript;第三个浏览器对象属于我们JS独有的，Web API讲解

## 内置对象

-   就是指JS语言自带的一些对象，这些对象供开发者使用，并提供了一些常用的或是最基本而必要的功能（属性和方法）
-   到MDN的文档里去查表

### Math对象

```js
Math.PI //圆周率
Math.floor () //向下取整 （地板）
Math.ceil() //向上取整 (天花板)
Math.round() //四舍五入版就近取整 （注意-3.5结果是-3）
Math.abs() //绝对值
Math.max()/Math.min() //求最大和最小值

Math.random //一个[0,1)的数
//想要的到两个数之间的随机数要自己构造
//两数中的随机数[min,max)
Math.random() * (max - min) + min; 
//两数中的随机整数[min,max)
Math.floor(Math.random() * (max - min)) + min;
//两数中的随机整数[min,max]
Math.floor(Math.random() * (max - min + 1)) + min; 

```

### Date对象

-   构造函数 要用new操作符实例化日期对象

| 方法名        | 说明                       | 代码               |
| ------------- | -------------------------- | ------------------ |
| getFullYear() | 获取当年                   | dObj.getFullYear() |
| getMonth()    | 获取当月(0-11)             | dObj.getMonth()    |
| getDate()     | 获取当天日期               | dObj.getDate()     |
| getDay()      | 获取星期几（周日0到周六6） | dObj.getDay()      |
| getHours()    | 获取当前小时               | dObj.getHours()    |
| getMinutes()  | 获取当前分钟               | dobj.getMinutes()  |
| getSeconds()  | 获取当前秒钟               | dobj.getSeconds()  |

#### 获取日期的总的毫秒形式

获得Date总的毫秒数（时间戳：不重复）

```js
//1.Date的方法
var date = new Date();
console.log(date.valueOf());//就是我们现在时间距离1970.1.1总的毫秒数
console.log(date.getTime());
//2.简单的写法（最常用的写法）
var date1 = +new Date(); //+new Date() 返回的就是总的毫秒数
console.log(date1);
//3.H5新增的获得总的毫秒数
console.log(Date.now());
```

```js
//获得某个时间的时间戳
var times = +new Date('2022-3-26 22:00:00');
console.log(times);
```



### Array数组对象

-   构造函数

```js
let arr = [1,2,3];
let arr = new Array();
let arr = new Array(2); // 长度为2空数组
let arr = new Array(2,3); // 相当于创建了数组[2,3]
```

#### 检测是否为数组

-   instanceof 运算符

    -   ```js
        // instanceof 运算符它可以用来检测是否为数组
        console.log(arr instanceof Array);
        ```


-   Array.isArray(参数)；

    -   ```js
        console.log(Array.isArray(arr));
        ```

#### 添加删除数组元素方法

-   Push() 

    -   给数组后面追加新的元素

    -   push()参数直接写数组元素

    -   push 完毕之后，**return** `新数组的长度`

    -   原数组也会发生变化

    -   ```js
        var arr=[1,2,3];
        arr.push(4);
        console.log(arr.push(3,'pink')); // 5
        //新数组为[1,2,3,3,'pink']
        //unshift同理
        ```

-   unshift()

    -   可以给数组前面追加新的元素
    -   unshift()参数直接写数组元素
    -   unshift 完毕之后，**return** `新数组的长度`
    -   原数组也会发生变化

-   pop()

    -   它可以删除数组的最后一个元素

    -   pop是可以删除数组的最后一个元素 记住一次只能删除一个元素

    -   pop()没有参数

    -   pop完毕之后，**return** 删除的那个元素

    -   原数组也会发生变化

    -   ```js
        var arr=[1,2,3];
        console.log(arr.pop()); // 3
        //新数组为[1,2]
        //shift同理
        ```

-   shift

    -   shift是可以删除数组的第一个元素 记住一次只能删除一个元素
    -   shift()没有参数
    -   shift完毕之后，**return** 删除的那个元素
    -   原数组也会发生变化



#### 数组翻转(函数)

-   ```js
    var arr=['w','a','n'];
    arr.reverse();
    //['n','a','w']
    ```

#### 数组排序(函数)

-   ```js
    var arr=[1,6,4,9,8];
    arr.sort(); // 仅限均为个位
    //[1,4,6,8,9]
    
    //嵌套一个函数即可完成更强的数组排序
    var arr=[1,66,14,91,8];
    arr1.sort(function(a,b)
    	//return a-b;升序的顺序排列
    	//(a-b>0,a后置;a-b<0,a前置,a-b=0,不交换位置)
    	return b-a;//降序的顺序排列
    });
    ```

索引函数

-   indexOf()

    -   **return** 数组中查找给定元素的第一个索引

    -   如果存在返回索引号如果不存在，**return** -1。

        

-   lastIndexOf()

    -   **return** 在数组中的最后一个的索引
    -   如果存在返回索引号如果不存在，**return**-1。

-   ```js
    let arr = [1,2,3,3,'pink'];
    arr.indexOf('pink');
    ```

#### 数组转换为字符串

-   toString()

    -   把数组转换成字符串，逗号分隔每一项

    -   **return **一个字符串

    -   ```js
        var arr=[1,2,3];
        console.log(arr.tostring());//1,2,3
        ```

-   join('分隔符')

    -   方法用于把数组中的所有元素转换为一个字符串。

    -   **return **一个字符串

    -   ```js
        var arr1 ['green','blue','pink'];
        console.log(arr1.join()) //green,blue,pink
        console.log(arr1.join('-')); //green-blue-pink
        
        console.log(arr1.join('&')); //green&blue&pink
        ```

#### concat()

-   `concat()` 方法用于合并两个或多个数组。

-   此方法不会更改现有数组，而是返回一个新数组。（仅当元素不是对象引用时）

-   ```js
    var new_array = old_array.concat(value1[, value2[, ...[, valueN]]])
    
    ```

#### slice()

-   `slice()` 方法返回一个新的数组对象，这一对象是一个由 `begin` 和 `end` 决定的原数组的 `浅拷贝`（包括 `begin`，不包括`end`）。左闭右开

-   原始数组不会被改变。

-   没有`begin`,为浅拷贝

-   如果`begin`超出索引范围,return 空数组

-   没有`end`,截取到最后一个元素

-   ```js
    var arr = arr.slice([begin[, end]])
    
    ```

#### splice()

-   **`splice()`** 方法通过删除或替换现有元素或者原地添加新的元素来修改数组,并以数组形式

-   此方法会改变原数组。

-   **return **被修改的内容。

-   `start`：从第几位

-   `deleteCount`：删除几个 (为0，返回空数组)

-   `itemN`：插入内容

-   ```js
    array.splice(start[, deleteCount[, item1[, item2[, ...]]]])
    
    var arr = ['angel', 'clown', 'drum', 'sturgeon'];
    var removed = myFish.splice(2, 1, "trumpet");
    //在索引 2 处 删除一个元素(arr[2]) , 并插入 'trumpet' 。
    
    // removed = ["angel", "clown", "trumpet", "sturgeon"]
    // return ["drum"]
    ```



## 基本包装类型：

-   把 简单数据类型 包装成为了 复杂数据类型

-   为了方便操作 基本数据类型 ，JavaScript还提供了三个特殊的引用类型：String、Numbera和Boolean

-   ```js
    //(1)把简单数据类型包装为复杂数据类型
    var temp = new string('andy');
    //(2)把临时变量的值给str
    str = temp;
    //(3)销毁这个临时变量
    temp = nu11;
    ```



## 字符串对象

#### 字符串的不可变

-   指的是里面的值不可变，虽然看上去可以改变内容，但其实是地址变了，内存中新开辟了一个内存空间。
-   不要大量拼接字符串
-   字符串所有的方法，都不会修改字符串本身（字符串是不可变的），操作完成会返回一个新的字符串。

#### 根据字符返回位置

#### indexOf()

-   **return** 数组中查找给定字符串的第一个索引

-   如果存在返回索引号如果不存在，**return** -1。

-   ```js
    let arr ='pinknnnn';
    //从第三个开始查找
    arr.indexOf('n'，3); // 4
    ```



#### 根据位置返回字符

-   charAt(index)
    -   返回指定位置的字符(index字符串的索引号)
    -   str.charAt(0)
-   charCodeAt(index)
    -   获取指定位置处字符的`ASCI码`(index索引号)
    -   <img src="./assets/Js 基础.assets\1.jpg" alt="img" style="zoom: 33%;" />
    -   str.charCodeAt(0)
-   str[index]
    -   获取指定位置处字符
    -   HTML5,IE8+支持和charAt()等效

#### replace()

-   替换字符串首位

#### slipt()

-   字符串转数组

#### toUpperCase0

-   字符串转换大写

#### toLowerCase0

-   字符串转换小写



# 简单类型与复杂类型

-   简单类型又叫做基本数据类型或者值类型，复杂类型又做引用类型。

-   值类型：简单数据类型/基本数据类型，在存储时变量中存储的是值本身，因此叫做值类型
    -   string number,boolean undefined,null
    -   简单数据类型 null 返回的是一个空的对象 object
-   引用类型：复杂数据类型，在存储时变量中存储的仅仅是地址（引用），因此叫做引用数据类型
    -   通过new关键字创建的对象（系统对象、自定义对像），
        如Object、Array、.Date等



-   JavaScript中没有堆栈的概念，通过堆栈的方式，可以让大家更容易理解代码的一些执行方式，便于将来学习其他语言

-   栈（操作系统）：
    -   由操作系统自动分配释放存放函数的参数值、局部变量的值等。
        其操作方式类似于数据结构中的栈；
    -   简单数据类型存放到栈里面
    -   简单数据类型是存放在**`栈`**里面里面直接开辟一个空间存放的是值
-   堆（操作系统）：
    -   存储复杂类型（对象），一般由程序员分配释放，若程序员不释放，
        由垃圾回收机制回收。
    -   复杂数据类型存放到堆里面
    -   复杂数据类型首先在**`栈`**里面存放地址十六进制表示,然后这个地址指向堆里面的数据



### 简单类型传参

函数的形参也可以看做是一个变量，当我们把一个值类型变量作为参数传给函数的形参时，其实是把变量在栈空间里的值复制了一份给形参，那么在方法内部对形参做任何修改，都不会影响到的外部变量。

### 复杂类型传参

函数的形参也可以看做是一个变量，当我们把引用类型变量传给形参时，其实是把变量在栈空间里保存的堆地址复制给了形参，形参和实参其实保存的是同一个堆地址，所以操作的是同一个对象。



## API

-   API(Application Programming Interface,应用程序编程接口)是一些预先定义的函数，

-   目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无需访问源码，或理解内部工作机制的细节。



# Web APIs

<img src="./assets/Js 基础.assets\image-20220327130557229.png" alt="image-20220327130557229" style="zoom:33%;" />

-   JS基础学习ECMAScript基础语法为后面作铺垫，
-   Web APIs是JS的应用，大量使用JS基础语法做交互效果



-   Web API是浏览器提供的一套操作浏览器功能和页面元素的API(BOM和DOM)。

-   API是为我们程序员提供的一个接口，帮助我们实现某种功能，我们会使用就可以了，不必纠结内部做如何实现。
-   Web API主要是`针对于浏览器`提供的**接口**，主要针对于浏览器做交互效果。
-   Web API一般都有输入和输出（函数的传参和返回值），Web API很多都是方法（函数）

-   学习Web API可以结合前面学习内置对象方法的思路学习



# DOM

-   文档对象模型(Document Object Model,简称DOM),是W3C组织推荐的处理`可扩展标记语言`(HTML或箸XML)的标准编程**`接口`。**
-   W3C已经定义了一系列的DOM接口，通过这些DOM接口可以改变网页的内容、结构和样式。
-   我们获取过来的DOM元素是一个对象(object),所以称为文档对象模型。



-   **文档**：一个页面就是一个文档，DOM中使用 **document** 表示
-   **元素**：页面中的所有标签都是元素，DOM中使用 **element** 表示
-   **节点**：网页中的所有内容都是节点（标签、属性、文本、注释等），DOM中使用 **node** 表示

#### DOM树

<img src="./assets/Js 基础.assets/image-20220327162001814.png" alt="image-20220327130557229" style="zoom:33%;" />




## 获取元素

### 通过id获取元素

#### getElementById（'id'）

-   因为我们文档页面从上往下加载，所以先得有标签所以我们
    **script写到标签的下面**
-   get获得element元素by通过驼峰命名法
-   参数id是大小写敏感的字符串
-   返回的是一个元素**对像**



**tips**：console.dir打印我们返回的元素对象更好的查看里面的属性和方法

### 通过tagname获取元素

#### getElementsByTagName('tagname')

-   还可以获取某个元素（父元素）内部所有指定标签名的子元素
-   返回的是获取过来元素对象的集合以伪数组的形式存储的
-   我们想要依次打印里面的元素对象我们可以采取遍历的方式
-   如果页面中只有一个11返回的还是伪数组的形式



**注**：父元素必须是单个对象（必须指明是哪一个元素对像）.获取的时候不包括父元素自己。（伪数组不行）

### 通过class获取元素

#### getElementsByClassName('class')

#### querySelector('.class'|'#id'|'li')

-   根据指定选择器返回第一个元素对像

#### querySelectorAll('同上')

-   根据指定选择器返回



### 获取body元素

doucumnet.body //返回body元素对象

### 获取html元素

document.documentElement //返回html元素对象



# 事件

-   JavaScript使我们有能力创建动态页面，而事件是可以被JavaScript侦测到的行为。
-   简单来说： 触发--响应机制。
-   事件三要素
    -   **事件源**
        -   事件源事件被触发的对象
        -   谁 
        -   按钮
    -   **事件类型**
        -   事件类型如何触发 
        -   什么事件 
        -   比如鼠标点击(onclick)还是鼠标经过还是键盘按下
    -   **事件处理程序**
        -   事件处理程序
        -   通过一个函数赋值的方式
        -   完成

```js
let btn = document.getElementById('btn');
btn.onclick = function(){ // 通过匿名函数
	alert('点秋香)；
}
```

1.  获取事件源
2.  注册事件（绑定事件）
3.  添加事件处理程序（采取函数赋值形式）

## 操作元素

-   JavaScript的DOM操作可以改变网页内容、结构和样式，我们可以利用DOM操作元素来改变元素里面的内容、属性等。
-   注意以下都是属性

#### 改变元素内容

#### element.innerText （*）

-   不识别html标签 非标准（W3C）

-   去除空格和换行

-   ```js
    btn.onclick = function(){
    	div.innerText ='2019-6-6';
    }
    ```

#### element.innerHTML

-   识别html标签 

-   保留空格和换行的

-   ```
    btn.onclick = function(){
    	div.innerHtml ='2019-6-6';
    }
    ```

### 修改元素属性

-   element.Attr = value;

### 表单元素的属性操作

-   type、value、checked、selected、disabled

-   ```js
    input.value = '被点击了'；
    this.disabled = true; // 禁用
    ```

 

-   ```js
    var flag = 0; // 切换器
    eye.onclick = function() {
        //点击一次之后，flag一定要变化
        if (flag == 0) {
            pwd.type = 'text';
            this.src = 'images/open.png';
            flag = 1; // 切换
        } else {
            pwd.type = 'password';
            this.src = 'images/close.png';
            flag = 0;
        }
    }
    ```



## 样式属性操作

#### element.style 行内样式操作

-   Js里面的样式采取驼峰命名法比如fontsize、backgroundcolor
-   Js修改style样式操作，产生的是 **行内样式**，css权重比较高

-   如果样式比较少或者功能简单的情况下使用

#### element.className 外部样式操作

-   把修改样式提前写在 css样式表中
-   需要修改的时候直接给标签加一个类名className, 属于外部样式
-   适合于样式较多或者功能复杂的情况
-   className会直接更改元素的类名，会覆盖原先的类名。



## 自定义属性

-   自定义属性目的：是为了保存并使用数据。有些数据可以保存到页面中而不用保存到数据库中。
-   不能直接被自有属性方式查找
-   新H5,字面量是data-开头的为自定义属性

#### element.getAttribute('属性'); (IE-5)

-   获取自定义属性的值

#### element.setAttribute('属性'，'值'); (IE-5)

-   修改自定义属性

#### element.removeAttribute('属性'); (IE-5)

-   移除自定义属性



#### dataset属性 (IE-11)

-   智能获取data-开头的

-   是一个集合里面存放了所有以data开头的自定义属性

-   如果自定义属性里面有多个-连接的单词，我们获取的时候采取驼峰命名法

-   ```js
    <input data-index='123' data-list-name='123' >
    
    //getAttribute 方法 (传参)
    console.log(div.getAttribute('data-list-name'));
    //dataset 对象 (索引属性值)
    console.log(div.dataset.listName);
    console.log(div.dataset['listName'])
    
    ```

    





#### 排他思想

-   如果有同一组元素，我们想要某一个元素实现某种样式，需要用到循环的排他思想算法：
-   注意顺序不能颠倒，首先干掉其他人，再设置自己



与机器

全选与单选:单选全部都选为真(全选),有一个为假(非全选)





# 节点

-   网页中的所有内容都是节点（标签、属性、文本、注释等），在DOM中，节点使用node来表示。
-   HTML DOM树中的所有节点均可通过JavaScript进行访问，所有HTML元素（节点）均可被修改，也可以创建或删除。



## 获取节点

这两种方式都可以获取元素节点，我们后面都会使用，但是节点操作更简单

1.  getElementBy…
2.  节点操作
    -   利用父子兄节点关系获取元素
    -   逻辑性强，但是兼容性稍差



-   一般地，节点至少拥有nodeType(节点类型)、nodeName(节点名称)和nodeValue(节点值)这三个基本属性。

-   nodeType

    -   元素节点nodeType为1

    -   属性节点nodeType为2

    -   文本节点nodeType为3（文本节点包含文字、空格、换行等）
    -   我们在实际开发中，节点操作主要操作的是**元素**节点



## 节点层级

利用DOM树可以把节点划分为不同的层级关系，常见的是父子兄层级关系。

### 父级节点

#### parentNode

-   获取父级节点
-   如果指定的节点没有父节点则返回null;



### 子级节点

#### childNodes(标准)

-   childNodes所有的子节点包含元素节点、文本节点等等
-   如果只想要获得里面的元素节点，则需要专门处理（通过节点类型不同）。所以我们一般不提倡使用child Nodes

#### children(非标准)

-   只会获得子节点的所有元素节点
-   浏览器都支持



#### firstChild（IE-6）

-   firstChi1d第一个子节点不管是文本节点还是元素节点

#### firstElementChild （IE-9）

-   firstElementChild返回第一个子元素节点

#### children[0] （first）

#### children[ol.children.length-1] （last）

-   实际开发的写法既没有兼容性问题又返回第一个子元素



### 兄弟节点

#### nextsibling

-   下一个兄弟节点

#### previoussibling

-   上一个兄弟节点



#### nextElementSibling （IE-9）

-   下一个兄弟元素节点

#### previousElementSibling （IE-9）

-   上一个兄弟元素节点

-   问：如何解决兼容性问题？
-   答：自己封装一个兼容性的函数
    （自定义函数内嵌兼容性好的方法，间接解决方案）



### 创建节点

#### createElement ('tagName')

-   document.createElement()方法创建由tagName指定的HTML元素。因为这些元素原先不存在，是根据我们的需求动态生成的，所以我们也称为动态创建元素节点。

### 添加节点

#### node.appendChild(child) （追加元素）

-   添加子节点

#### node.insertBefore(child,指定元素) 

```js
let ul = document.querySelector('ul');
let li = document.createElement('li');// 创建一个li元素

ul.appendChild( li );// 添加到ul子级中
ul.insertBefore( li , ul.children[0] );// 添加到ul的第一个子级后
```

### 删除节点

#### node.removeChild(child) (删除元素)

-   方法从DOM中删除一个子节点
-   返回删除的节点。



阻止链接跳转需要添加

1.  javascript:void(0); 

2.  javascript:;

    -   ```html
        <a href='javascript:;'> </a>
        ```



### 复制节点 (创建节点)

-   方法返回调用该方法的节点的一个副本。也称为克隆节点/拷贝节点

#### node.cloneNode(false)

-   如果括号参数为空或者为false,则是浅拷贝，即只克隆复制节点本身，不克隆里面的子节点。

#### node.cloneNode(true)

-   如果括号参数为true,，则是深度拷贝，会复制节点本身以及里面所有的子节点。



### 三种动态创建元素区别

#### document.write() （尽量别用）

-   document.write是直接将内容写入页面的内容流，
    但是文档流执行完毕，则它会导致页面全部重绘。

#### element.innerHTML

-   innerHTML是将内容写入某个DOM节点，不会导致页面全部重绘
-   innerHTML创建多个元素效率更高
    （不要拼接字符串，采取数组形式拼接），结构稍微复杂
-   （数组转字符串，join(' ')，以空格分隔）

#### document.createElement()

-   createElement()创建多个元素效率稍低一点点，但是结构更清晰



# DOM重点核心

关于dom操作，我们主要针对于元素的操作。主要有创建、增、删、改、查、属性操作、事件操作。



# 注册事件（绑定事件）

### 传统注册方式

-   以on开头的方法

-   给元素添加事件，称为注册事件或者绑定事件。
-   注册事件有两种方式：传统方式和方法监注册方式
-   特点：注册事件的**唯一性**
-   同一个元素同一个事件只能设置一个处理函数，最后注册的处理函数将会覆盖前面注的处理函数



### 方法监听注册方式

-   w3c标准推荐方式
-   addEventListener() 它是一个方法
-   IE9之前的IE不支持此方法，可使用attachEvent()代替
-   特点：同一个元素同一个事件可以注册多个监听器
-   按注册顺序依次执行

#### addEventListener事件监听方式

-   eventTarget.addEventListener()方法将指定的监听器注册到eventTarget(目标对象)上，
    当该刻对象触发指定的事件时，就会执行事件牧处理函数。

-   eventTarget.addEventListener(type,listener[,useCapture])

    -   type:事件类型字符串，比如click、mouseover,注意这里不要带on

    -   listener:事件处理函数，事件发生时，会调用该监听函数

    -   useCapture:可选参数，是一个布尔值，默认是false。

    -   事件侦听注册事件addEventListener里面的事件类型是字符串必定加引号，而且不带on

    -   ```js
        btns.addEventListener('click',function(){
        	alert(22);
        })
        ```

#### attachEvent事件监听方式 （非标）

不考虑（除非要兼容IE-8）



### 删除事件的方式

1.  #### 传统方式删除事件	

    -   #### element.onclick = null;

2.  #### 方法监听注册方式

    -   #### eventTarget.removeEventListener(type,listener[,useCapture]);

    -   ```js
        divs[1].addEventListener('click',fn)//里面的fn不需要调用加小括号
        function fn(){ // 命名函数（可复用）
        	alert(22);
        	this.removeEventListener('click',fn);
        }
        ```



# DOM事件流

-   事件流描述的是从页面中接收事件的顺序。
-   事件发生时会在元素节点之间按照特定的顺序传播，这个传播过程即DOM事件流。
-   DOM事件流分为3个阶段：
    1.捕获阶段
    2.当前目标阶段
    3.冒泡阶段

<img src="./assets/Js 基础.assets/image-20220329160427238.png" alt="image-20220329160427238" style="zoom: 50%;"/>

-   事件冒泡：IE最早提出，事件开始时由最具体的元素接收，然后逐级向上传播到到DOM最顶层节点的过程。
-   事件捕获：网景最早提出，由DOM最顶层节点开始，然后逐级向下传播到到最具体的元素接收的过程。

<img src="./assets/Js 基础.assets/image-20220329160945316.png" alt="image-20220329160945316" style="zoom: 33%;" />

### 注意

-   JS代码中只能执行捕获或者冒泡其中的一个阶段。
-   onclick 和attachEvent 只能得到冒泡阶段。
-   addEventListener(type,listener[,useCapture])
-   第三个参数如果是true,表示在事件`捕获阶段`调用事件处理程序；
-   如果是false（不写默认就是false),表示在事件`冒泡阶段`调用事件处理程序。
-   实际开发中我们很少使用事件捕获，我们更关注事件冒泡。
-   有些事件是没有冒泡的，比如onblur、on focus、onmouseenter、onmouseleave
-   事件冒泡有时候会带来麻烦，有时候又会帮助很巧妙的做某些事件，我们后面讲解。

### 事件对象

1.  event就是一个事件对象 写到监听函数的小括号里面 当形参来看

2.  事件对象只有有了事件才会存在，它是系统给我们自动创建的，不需要我们传递参数

3.  事件对象是事件的一系列相关数据的集合跟事件相关的
    比如鼠标点击里面就包含了鼠标的相关信息，鼠标坐标等…
    如果是键盘事件里面就包含的键盘事件的信息比如判断用户按下了那个键

4.  这个事件对象我们可以自己命名比如event、evt、e

    -   ```js
        div.addEventListener('click',function(e){
        	console.log(e);
        })
        ```

5.  事件对象也有兼容性问题 ie6~8 通过 window.event

    -   e = e || window.event

6.  当我们注册事件时，evet对象就会被系统自动创建，并依次传递给事件监听器（事件处理函数）。



### 常见事件对象的属性和方法

#### e.target 返回的是<u>触发事件</u>的对象（元素）

#### this 返回的是<u>绑定事件</u>的对象（元素）

-   ```js
    div.addEventListener('click',function(e){
    	console.log(e.target); // div
    	console.log(this); // div
    })
    ```

#### e.type 返回事件类型

-   ```js
    div.addEventListener('click',function(e){
    	console.log(e.type); // click
    })
    ```

#### e.stopPropagation(); 阻止事件冒泡

-   事件冒泡：开始时由最具体的元素接收，然后逐级向上传播到倒DOM最顶层节点。

#### e.preventDefault(); 阻止默认行为



### 事件委托（代理、委派）

-   事件冒泡本身的特性，会带来的坏处，也会带来的好处，需要我们灵活掌握。生活中有如下场景：

#### 事件委托的原理

-   不是每个子节点单独设置事件监听器，而是事件监听器设置在其<u>父节点</u>上，然后利用冒泡原理影响设置每个子节点。



### 常用鼠标点击事件

#### 'contextmenu' 上下文菜单(右键)

```js
document.addEventListener('contextmenu',function(e){
	e.preventDefault();
})
```

#### 'selectstart' 开始选择



### 鼠标事件对象

1.  client鼠标在可视区的x和y坐标
    -   clientX
    -   clientY
2.  page鼠标在页面文档的x和y坐标 (key)
    -   pageX
    -   pageY
3.  screen鼠标在电脑屏幕的x和y坐标
    -   screenX
    -   screenY



### 常用键盘点击事件

| 键盘事件 | 触发条件                                                     | 执行顺序 |
| -------- | ------------------------------------------------------------ | -------- |
| keydown  | 某个键盘按键被按下时触发                                     | 1        |
| keypress | 某个键盘按键被按下时触发 <br />但是<u>它不识别功能键</u>比如ctrl shift箭头等 | 2        |
| keyup    | 某个键盘按键被松开时触发                                     | 3        |

### 键盘事件对象

#### e.keyCode 返回ASCII值

-   onkeydown 和onkeyup <u>不区分</u> 字母大小写
-   onkeypress 区分字母大小写。

(获取元素焦点focus();)





# BOM浏览器对象模型

-   BOM(Browser Object Model)即浏览器对象模型，它提供了独立于内容而与浏览器窗口进行交互的对象，其<u>核心对象是window。</u>
-   BOM由一系列相关的对象构成，并且每个对象都提供了很多方法与属性。

-   BOM缺乏标准，JavaScript语法的标准化组织是ECMA,DOM的标准化组织是W3C,BOM最初是Netscape浏览器标准的一部分。

| DOM                                     | BOM                                             |
| :-------------------------------------- | :---------------------------------------------- |
| 文档对象模型                            | 浏览器对象模型                                  |
| DOM就是把「文档」当做一个「对象」来看待 | 把「浏览器」当做一个「对象」来看待              |
| DOM的顶级对象是document                 | BOM的顶级对象是window                           |
| DOM主要学习的是操作页面元素             | BOM学习的是浏览器窗口交互的一些对象             |
| DOM是W3C标准规范                        | BOM是浏览器厂商在各自浏览器上定义的，兼容性较差 |

## BOM的构成

<img src="./assets/Js 基础.assets/image-20220329190039233.png" alt="image-20220329190039233" style="zoom:80%;" />

1.  它是JS访问浏览器窗口的一个接口。
2.  它是一个全局对象。定义在全局作用域中的变量、函数都会变成wdow对象的属性和方法。

在调用的时候可以省略window,前面学习的对话框都属于window对象方法，如alert() 、prompt()等。

-   注意：window下的个特殊属性window.name



#### 'load' 事件 -window

-   等页面内容全部加载完毕，包含页面dom元素图片flash css等等



#### 'DOMContentLoaded' 事件 -document

-   是DoM加载完毕，不包含图片falsh css等就可以执行加载速度
-   <u>比load更快一些</u>



#### 'resize' 事件 -window

-   resize是调整窗口大小加载事件，当触发时就调用的处理函数。
-   我们经常利用这个事件完成响应式布局。window.innerWidth当前屏幕的宽度



### 两种定时器

-   window对象给我们提供了2个非常好用的方法-定时器。

-   #### setTimeout()

    -   window.setTimeout(调用函数，[延迟的毫秒数])；

    -   只调用一次

    -   ```js
        setTimeout(function(){} , during);
        setTimeout(function , during);
        setTimeout('function()' , during);
        //window 可省略
        ```

-   #### setInterval()

    -   间隔时间不断调用
    -   其他同上

回调函数：作为参数被函数调用的函数。

#### clearTimeout(timeoutID)；



### this

-   指向问题一般情况下this的最终指向的是那个调用它的对象

1.  全局作用域或者普通函数中this指向全局对象window(注意定时器里面的this指向window)
2.  方法调用中谁调用this指向谁
3.  构造函数中this指向构造函数的实例



# JS执行机制

### JS是单线程

-   JavaScript语言的一大特点就是单线程，也就是说，同一个时间只能做件事。
-   这是因为Javascript这门脚本语言诞生的使命所致
-   JavaScript是为处理页面中用户的交互，以及操作DOM而诞生的。
-   比如我们对某个DOM元素进行添加和删除操作，不能同时进行。应该先进行添加，之后再删除。
-   单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。
-   这样所导致的问题是：如果JS执行的时间过长，这样就会造成须面的渲染不连贯，导致页面渲染加载阻塞的感觉。



### 同步和异步

-   为了解决这个问题，利用多核CPU的计算能力，HTML5提出Web Worker标准，允许JavaScript脚本创建多个线程。于是，JS中出现了同步和异步。

#### 同步

-   前一个任务结束后再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、同步的。

#### 异步

-   你在做一件事情时，因为这件事情会花费很长时间，在做这件事的同时，你还可以去处理其他事情。

#### 同步任务

-   同步任务都在主线程上执行，形成一个**执行栈**。

#### 异步任务

-   JS的异步是通过回调函数实现的。
-   异步任务相关回调函数添加到任务队列中（任务队列也称为消息队列）。



1.  先执行<u>执行栈</u>中的同步任务。
2.  异步任务（回调函数）放入<u>任务队列</u>中。
3.  一旦执行栈中的所有同步任务执行完毕，
    系统就会按次序读取任务队列中的异步任务，
    于是被读取的异步任务结束等待状态，<u>进入执行栈</u>，开始执行。

-   由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种机制被称为<u>事件循环</u>(event loop)。<img src="./assets/Js 基础.assets/image-20220329221556283.png" alt="image-20220329221556283" style="zoom:50%;" />



## location对象

window对象给我们提供了一个location属性用于获取或设置窗体的URL,并且可以用于解析URL。因为这个属性返回的是一个对象，所以我们将这个属性也称为location对象。

#### URL

-   统一资源定位符(Uniform Resource Locator, URL)是互联网上标准资源的地址。互联网上的每个文件都有一个唯一的URL,它包含的信息指出文件的位置以及浏览器应该怎么处理它。

#### URL的一般语法格式为：

-   protocol://host [port]/path/[?query]#fragment

-   ```
    http://www.itcast.cn/index.html?name=andy&age=18#link
    ```

| 组成     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| protocol | 通信协议 常用的http,ftp,maito等                              |
| host     | 主机（域名） www.itheima.com                                 |
| port     | 端口号 可选，省略时使用方案的默认端口如ttp的默认端口为80     |
| path     | 路径 由零或多个'/'符号隔开的字符串，一般用来表示主机上的一个目录或文件地址 |
| query    | 参数 以键值对的形式，通过&符号分隔开来                       |
| fragment | 片段 #后面内容常见于链接锚点                                 |

#### location对象的属性

| location对象属性  | 返回值                           |
| ----------------- | -------------------------------- |
| location.href     | 获取或者设置 整个URL             |
| location.host     | 返回主机(域名) www.itheima.com   |
| location.port     | 返回端口号 如果未写返回空字符串  |
| location.pathname | 返回路径                         |
| location.search   | 返回参数                         |
| location.hash     | 返回片段 #后面内容常见于链接锚点 |

#### location对象的方法

| location对象方法   | 返回值                                                       |
| ------------------ | ------------------------------------------------------------ |
| location.assign()  | 跟href一样，可以跳转页面（也称为重定向页面）                 |
| location.replace() | 替换当前页面，因为<u>不记录历史</u>，所以不能后退页面        |
| location.reload()  | <u>重新加载页面</u>，相当于刷新按钮或者f5如果参数为true强制刷新ctrl+f5 |

## navigator对象

-   navigator对象包含有关浏览器的信息，它有很多属性，我们最常用的是userAgent,该属性可以返回由客户机发送服务器的user-agent头部的值。

## history对象

-   window对象给我们提供了一个history对象，与浏览器历史记录进行交互。该对象包含用户（在浏览器窗口中）访问过的URL。

| history对象方法 | 作用                                                         |
| --------------- | ------------------------------------------------------------ |
| back()          | 可以后退功能                                                 |
| forward()       | 前进功能                                                     |
| go(参数)        | 前进后退功能参数如果是1前进1个页面<br />如果是-1后退1个页面 -2就是退两个页面 |





# 元素偏移量offset系列

### offset概述

-   offset翻译过来就是<u>偏移量</u>，我们使用offset系列相关属性可以动态的得到该元素的位置（偏移）、大小等。

-   获得元素距离带有定位父元素的位置
-   获得元素自身的大小（宽度高度）
-   <u>注意：返回的数值都不带单位</u>



-   #### element.offsetParent
    
    -   返回作为该元素<u>带有定位</u>的父级元素如果父级都没有定位则返回body
-   #### element.offsetTop
    
    -   返回元素相对带有定位父元素<u>上方的偏移</u>
-   #### element.offsetLeft
    
    -   返回元素相对带有定位父先素<u>左边框的偏移</u>
-   #### element.offsetWidth
    
    -   返回自身包括 padding、内容的width、border，返回数值不带单位
    -   <u>不包含margin</u>
-   #### element.offsetHeight
    
    -   返回自身包括 padding、内容的height、border，返回数值不带单位
    -   <u>不包含margin</u>

#### offset与style区别

| offset                              | style                                 |
| ----------------------------------- | ------------------------------------- |
| 可以得到<u>任意样式表</u>中的样式值 | 只能得到<u>行内</u>样式表中的样式值   |
| 获得的数值是<u>没有单位</u>的       | 获得的是带有单位的字符串              |
| 包含<u>padding+border+width</u>     | 获得不包含padding和border的值         |
| 是<u>只读属性</u>，只能获取不能赋值 | <u>可读写</u>属性，可以获取也可以赋值 |
| 获取元素大小位置，用offset更合适    | 给元素更改值，则需要用stylei改变      |



#### 弹窗/模态框



# 元素可视区client系列

-   client 翻译过来就是客户端
-   我们使用client系列的相关属性来获取元素可的相关信息。
-   通过client系列的相关属性可以动态的得到该元素的边框大小、元素大小等。



-   #### element.clientTop

    -   返回元素上边框的大小

-   #### element.clientLeft

    -   返回元素左边框的大小

-   #### element.clientWidth

    -   返回自身包括 padding、内容width，返回数值不带单位
    -   <u>不包含 margin、border</u>

-   #### element.clientHeight

    -   返回自身包括 padding、内容height，返回数值不带单位
    -   <u>不包含 margin、border</u>



#### 立即执行函数

-   不需要调用，立马能够自己执行的函数

-   ( function() {})(参数);

-   ( function() {} (参数));
-   主要作用：创建一个独立的作用域。避免了命名冲突问题



#### 'pageshow' 事件 -window

-   重新加载页面触发 的事件
-   区别于<u>load</u>（load在有缓存时前进后退可能不会刷新页面）



# 元素滚动scroll系列

-   scroll翻译过来就是滚动的，我们使用scro川系列的相关属性可以动态的得到该元素的大小、滚动距离等。

-   #### element.scrollTop

    -   返回被卷去的上侧距离，返回数值不带单位

-   #### element.scrollLeft

    -   返回被卷去的左侧距离，返回数值不带单位

-   #### element.scrollWidth

    -   返回自身实际的宽度，内容宽度、padding，返回数值不带单位
    -   <u>不包含 margin、border</u>

-   #### element.scrollHeight

    -   返回自身实际的高度，内容高度、padding，返回数值不带单位
    -   <u>不包含 margin、border</u>

#### 'scroll' 事件 -有scroll的element



-   #### window.pageYOffset

    -   页面纵向被卷去的距离

-   #### window.pageXOffset

    -   页面横向被卷去的距离

### 三大系列总结

-   offset系列经常用于<u>获得元素位置</u> offsetLeft offsetTop
-   client经常用于<u>获取元素大小</u> clientWidth clientHeight
-   scroll经常用于<u>获取滚动距离</u> scrollTop scrollLeft
-   注意页面滚动的距离通过window.pagexoffset获得



### 鼠标移入 不会冒泡

#### 'mouseenter' 鼠标事件 -element

-   进入

#### 'mouseleave' 鼠标事件 -element

-   离开

### 鼠标移入 会冒泡

#### 'mouseover' 鼠标事件 -element

-   悬停(over)

#### 'mouseout' 鼠标事件 -element

-   对应over 移出



# 动画函数封装

### 动画实现原理

核心原理：通过定时器setlnterval()不断移动盒子位置。



### 动画函数简单封装

注意函数需要传递2个参数，动画对象和移动到的距离。



### 缓动效果原理

缓动动画就是让元素运动速度有所变化，最常见的是让速度慢慢停下来

让盒子每次移动的距离慢慢变小，速度就会慢慢落下来。

<u>核心算法：</u>（目标值-现在的位置）/10做为每次移动的距离步长

停止的条件是：让当前盒子位置等于目标位置就停止定时器





### 动画函数添加回调函数

#### 在计算机科学中，<u>回调函数</u>是指一段以参数的形式传递给其它代码的可执行代码。

回调函数原理：函数可以作为一个参数。将这个函数作为参数传到另一个函数里面，当那个函数执行完之后,再执行传进去的这个函数，这个过程就叫做<u>回调</u>。



## 节流阀

-   防止轮播图按钮连续点击造成播放过快。
-   节流阀目的：当上一个函数动画内容执行完毕，再去执行下一个函数动画，让事件无法连续触发。
-   核心实现思路：利用回调函数，添加一个变量来控制，锁住函数和解锁函数。





# 移动端

### 触屏事件

移动端浏览器兼容性较好，我们不需要考虑以前S的兼容性问题，可以放心的使用原生S书写效果，但是移动端也有自己独特的地方。比如触屏事件touch(也称摸事件)，Android和IOS都有。

#### touchstart

-   手指触摸到一个DOM元素时触发

#### touchmove

-   手指在一个DOM元素上滑动时触发

#### touchend

-   手指从一个DOM元素上移开时触发



### 触摸事件对象(TouchEvent)

#### touches

-   正在触摸<u>屏幕</u>的所有手指的列表

#### targetTouches

-   正在触摸当前<u>DoM元素</u>的手指列表
-   `targetTouches` 元素是 `touches` 的真子集。
-   最常用

如果侦听的是一个D0M元素，他们两个是一样的

#### changedTouches

-   手指状态发生了改变的列表从无到 有或者 从有到无



### 移动端拖动元素

#### 获取手指初始坐标：

-   拖动元素需要当前手指的坐标值
-   targetTouches[O]里面的pageX和pageY

#### 移动端拖动的原理：

-   手指移动中，计算出<u>手指移动的距离</u>。然后用<u>盒子原来的位置</u>+手指移动的距离

#### 手指移动的距离：

-   手指滑动中的位置减去手指刚开始触摸的位置



#### classList

元素类伪数组

#### 追加类名

classList.add('class');

#### 移出类名

classList.remove('class');

#### 切换类名

classList.toggle('class');

-   没有就加上

#### className

-   会覆盖类名



### click延时解决方案

#### click 300ms延时

-   原因是移动端屏幕双击会缩放(double tap to zoom)页面。

1.  #### 禁用缩放
-   ```html
    <meta name="viewport"content="user-scalable=no">
    ```

-   浏览器禁用默认的双击缩放行为并且去掉300ms的点击延迟。
2.  #### 利用touch事件

-   自己封装这个事件解决300ms延迟。
    1.  当我们手指触摸屏幕，记录当前摸时间
    2.  当我们手指离开屏幕，用离开的时间减去摸的时间
    3.  如果时间小于150s,并且没有滑动过屏幕，那么我们就定义为点击

3.  #### fastclick 插件解决300ms延迟。使用延时



# 什么是插件

-   移动端要求的是快速开发，所以我们经常会借助于一些插件来帮我完成操作，那么什么是插件呢？

-   JS插件是JS文件，它遵循一定规范编写，方便程序展示效果，拥有特定功能且方便调用。如轮播图和瀑布流插件。
-   特点：它一般是为了解决某个问题而专门存在，其功能单一，并且比较小。
-   我们以前写的animate.js也算一个最简单的插件



### 插件使用

-   插件的使用总结

-   去官网查看使用说明
-   下载插件
-   打开demo实例文件，查看需要引入的相关文件，并且引入
-   复制demo实例文件中的结构html,样式css以及js代码



### 移动端视频插件zy.media,js

-   H5给我们提供了video标签，但是浏览器的支持情况不同。
-   不同的视频格式文件，我们可以通过source解决。
-   但是外观样式，还有暂停，播放，全屏等功能我们只能自己写代码解决。
-   这个时候我们可以使用插件方式来制作。



# 框架概述

-   框架，顾名思义就是一套架构，它会基于自身的特点向用户提供一套较为完整的解决方案。
-   框架的控制权在框架本身，使用者要按照框架所规定的某种规范进行开发。

-   框架：大而全，一整套解决方案
-   插件：小而专一，某个功能的解决方案



# 本地存储

随着互联网的快速发展，基于网页的应用越来越普遍，同时也变的越来越复杂，为了满足各种各样的需求，会经常性在本地存储大量的数据，HTML5规范提出了相关解决方案。

-   数据存储在用户浏览器中
-   设置、读取方便、甚至页面刷新不丢失数据
-   容量较大，sessionStorage约5M、localStorage约20M



### (window.)sessionStorage

-   生命周期为<u>关闭浏览器窗口</u>
-   在同一个窗口（页面）下数据可以共享
-   以键值对的形式存储使用

#### .setltem(key,value)

-   存储数据(修改)

#### .getltem(key)

-   获取数据

#### .removeltem(key)

-   删除数据

#### .clear(key)



### (window.)localStorage

-   生命周期<u>永久生效</u>，除非手动删除否则<u>关闭页面也会存在</u>
-   可以多窗口（页面）共享（<u>同一浏览器可以共享</u>）
-   以键值对的形式存储使用

#### .setltem(key,value)

-   存储数据(修改)

#### .getltem(key)

-   获取数据

#### .removeltem(key)

-   删除数据

#### .clear(key)



# 复选框

### 'change' -事件 -element

