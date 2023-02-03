# JS内置属性和方法



# 垃圾回收机制

当引用内容没有变量引用时,该内容会被回收



# 处理字符串(string.)

### str.trim()

-   从一个字符串的两端删除空白字符
-   所有的<u>空白字符</u> (space, tab, no-break space 等) 以及所有行终止符字符（如 LF，CR等）
-   LF: Line Feed(换行)
-   CR: carriage return(回车)

#### 应用

按不出空格

-   this.value = this.value.trim();



### $ 字符串转数组

#### str.split('分割符')

-   指定的<u>分隔符字符串</u>将一个String对象分割成子字符串<u>数组</u>

### $ 取字符串的某个字符

-   #### str.charAt(0);

-   #### str[0];  //迭代器的方式

### $ 取字符串的某段字符

#### str.slice( [begin,end) )

-   支持负数
-   返回新数组

#### str.substr( [begin,number) )

-   支持负数
-   返回新数组

#### str.substring( [begin,end) )

-   负数 = 0;
-   返回新数组

### $ 字符串的检索

#### str.indexOf('b',fromIndex);

-   返回 index [-1(没找到)
-   fromIndex(从索引开始找,支持负数,大于length则不找)
-   <u>重在返回位置</u>

#### str.lastindexOf('b',fromIndex);

-   返回 同上
-   fromIndex 同上
-   <u>从最后一位开始找</u>
-   <u>重在返回位置</u>

#### str.includes('b',fromIndex):boolean

-   <u>重在是否存在</u>

#### startsWith('b'):boolean

-   区分大小写

#### endsWith('b'):boolean

-   区分大小写



## $ 增删改

#### str.replace( 'str_1' , 'str_2'|callback )

-   把str中的str_1替换成str_2
-   或对找到的str_1执行一次callback







# 处理数组(array.)

#### let arr = new Array(多参)

-   标准实例化一个数组(对象)
-   let arr = new Array(3)
    -   并非[3] 而是[empty*3] 因为单参默认为开辟数组空间数
    -   Array.of(3) //[3] 新的版本

#### let arr = [];

-   字面量创建数组

#### typeof arr //object

-   数组是个对象 - 引用类型

#### Array.isArray()

-   判断是否为数组

#### Array.from('str'/[]/obj{length:num})

-   对一个<u>类似数组</u>或<u>可迭代对象</u>创建一个新的，<u>浅拷贝</u>的数组实例。
-   obj要有<u>length</u>属性
-   或者用[…arr]



### $ 改变原数组(数组增删改)

#### arr.push(可多参)

-   在原数组中追加一个元素
-   arr.push(…arr_source)展开后传参
-   返回 数组长度

#### arr.pop()

-   弹出在原数组最后一个元素
-   返回 被弹出的元素

#### arr.unshift(可多参)

-   在原数组中顶部压入一个元素
-   arr.unshift(…arr_source)展开后传参

#### arr.shift()

-   移出在原数组顶部的元素
-   返回 被移出的元素

#### arr.fill('value',begin,end)

-   用一个<u>固定值</u>填充一个数组中[begin,end)的全部元素。
-   end 默认为arr.length

#### arr.splice( [begin,count,?value )

-   在数组<u>中间</u>做增删改查

-   支持负数
-   begin:开始索引
-   count:移除几个元素
-   ?value:移除完之后插入的元素
-   <u>会改变原数组</u>
-   返回 被移除的元素的数组

#### arr.copyWithin(target, [begin,end) )

-   支持负数
-   target:粘贴到的索引位
-   将[begin,end)的元素粘贴覆盖自target
-   若target>begin <u>多出来的复制被忽略</u>

#### arr.indexOf('b',fromIndex);

-   返回 index [-1(没找到)
-   fromIndex(从索引开始找,支持负数,大于length则不找)
-   <u>重在返回位置</u>

#### arr.lastindexOf('b',fromIndex);

-   返回 同上
-   fromIndex 同上
-   <u>从最后一位开始找</u>
-   <u>重在返回位置</u>

#### arr.includes('b',fromIndex):boolean

-   <u>重在是否存在</u>

#### arr.sort(callback)

-   一般都要加测试函数
-   测试函数结果>0,b放前

-   ```
    numbers.sort((a, b) => a - b); // 升序
    numbers.sort((a, b) => b - a); // 降序
    ```

#### arr.every( callback(?value,?index,?array) )

-   全部的 callback 为true 返回 true (布尔)
-   跟与很像

#### arr.some( callback(?value,?index,?array) )

-   有一个 callback 为true 返回 true (布尔)
-   跟或很像





### $ 清空数组

#### arr = []; (指向新空数组)

#### arr.length = 0; (改变原数组)

#### arr.splice(0); (清除全部元素)



### $ 生成新数组

#### arr.concat(arr1,arr2)

-   连接数组 返回新数组

#### arr.forEach( callback(?value,?index,?array) )

-   对数组的每个元素执行一次给定的函数
-   与map和reduce不同,它总是返回 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined) 值，并且==不可链式调用==。
-   `forEach()` 被调用时，不会改变原数组，也就是调用它的数组

#### arr.reduce(callback(pre,value,?index,?array),init)

-   遍历数组 把数组前一个返回值和当前值处理 

-   返回 测试函数的结果

-   ```js
    let arr = [1,3,1,4,5,2,1];
    let orr = [
        {name: "a",	price: 1}, 
        {name: "b",price: 2}, 
        {name: "a",	price: 1}
    ];
    
    brr = arr.reduce((pre, cur) => {
        cur > 2 && pre.push(cur);
        return pre
    }, []);//[3,4,5] 重打包分类
    
    
    let sum = arr.reduce((pre, cur) => {
    	return pre + cur
    }, 0)// sum is 17 累加器
    
    
    let quchong = arr.reduce((pre, cur) => {
        !pre.includes(cur) && pre.push(cur);
        return pre
    }, [])//[3,4,5] 去重
    
    let quchong_s = orr.reduce((pre, cur) => {
        let find = pre.find( (el) => el.price == cur.price )
        if (!find) pre.push(cur)
        return pre
    }, []) // 去重
    //[{name: "a",price: 1}, 
    //{name: "b",price: 2},];
    
    ```
    
    

#### arr.map( callback(?value,?index,?array) )

-   返回 测试函数的<u>返回值构成</u>的 新数组
-   当然也可以不返回, 直接操作原数组
-   伪数组不能直接使用map
    -   可以展开(浅拷贝一份)后map
    -   […div].map()


#### arr.filter( callback(?value,?index,?array) )

-   返回 return true的元素组成的 新数组

#### arr.find( callback(?value,?index,?array) )

-   返回 测试函数return true的第一个值

#### arr.findIndex( callback(?value,?index,?array) )

-   返回 测试函数return true的第一个值的索引

#### arr.slice( [begin,end) )

-   支持负数
-   返回 新数组



### $ 迭代器

#### arr.values()

-   可迭代对象
-   done:是否遍历完
-   value:值

#### arr.key()

-   可迭代对象
-   done:是否遍历完
-   key:索引

#### arr.entries()

-   可迭代对象
-   done:是否遍历完
-   value:数组[key,value]







### $ 数组转字符串

#### arr.join('分隔符')

-   默认为,分隔
-   如果数组只有一个项目，那么将返回该项目而<u>不使用分隔符</u>。
-   如果 `arr.length` 为0，则返回<u>空字符串</u>。



# 处理布尔值(boolean.)

### $ 当判断时

-   布尔值不进行隐式转换
-   <u>空字符串为F</u>,其他字符串为T
-   <u>0为F</u>,其他数字为T
-   空[],空{}为T,数组,对象都为T(引用类型为真)

#### Boolean() 隐式转换

-   其值不是 undefined 或 null 的任何对象(包括false)

-   也可以<u>!!变量</u>

    

#### a = !a

-   a先隐转为Boolean,然后再非



# 处理数值(number.)

#### num.isInterger()

-   是否为整数 返回 布尔

#### num.toFixed(num)

-   四舍五入

-   使用定点表示法来格式化一个数值。(保留多少位小数)(一般在0~20)
-   默认为 0

#### num.isNaN()

-   判断是不是非数字(Not a Number)

### $ 处理为数值

#### Number(value)

-   转换为数值
-   字符串必须为全数值 || NaN
-   数组
    -   Number([]) //0
    -   Number([1]) //1
    -   Number([1,2]) //NaN
-   对象
    -   Number({}) //NaN (一般都是NaN)

#### parseInt(value)

-   转换为整数
-   由数字开始
    -   parseInt(89.123jk) //89

#### parseFloat(value)

-   转换为浮点数
-   由数字开始
    -   parseInt(89.123jk) //89.123





# 处理对象(object.)

### $ 所有obj的key都将转换成字符串

-   所以转换后的key如果相等会被覆盖
-   所以obj不会有重复的key

```js
let user1 = 'key'
let obj = {
    user1:1 ,
    [user1]:2
}
//{
//   user1:1 ,
//   'key':2
//}
将对象key在使用变量时,要加[]

console.log(obj[user1]) //2
```

#### obj[age] = 25;

-   给变量增加属性



#### obj.getOwnPropertySymbols()

-   返回一个给定对象自身的所有 <u>Symbol</u> 属性的数组

#### obj.is(value1,value2)

-   判断两个值是否相等,不会强制转换两边的值。
-   -0不等于+0(在===中相等)

#### obj.assign(target, ...sources)

-   返回目标对象 会改变目标对象
-   将所有可枚举属性的值从一个或多个 源对象 分配到 目标对象



# 处理函数(function.)

#### func.apply(this,[])

-   参数列表
-   把数组分参数依次传给func作参数

### 展开语法

#### …array

-   只能用于<u>可迭代对象</u>
-   sum(...array) 等价于 sum.apply(null, array))
-   展开字符串
    -   let […arg] = 'abc' 
    -   […arg] //['a','b','c']



### 解构赋值

```js
let [a,b] = [abc,pie];
//a = 'abc';  b = 'pie'

[a, b, ...rest] = [10, 20, 30, 40, 50];
//a = 10
//b = 20
//rest = [30, 40, 50];

[a, b] = [10, 20, 30, 40, 50];
//a = 10
//b = 20

({ a, b } = { a: 10, b: 20 });
//a = 10
//b = 20

({a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40});
// a = 10
// b = 20
//rest = {c: 30, d: 40}

//设置默认值,为了防止从数组中取出一个值为undefined的对象
[a=5, b=7] = [1];
console.log(a); // 1
console.log(b); // 7

//忽略不重要的
[a, ,b] = [10, 20, 30, 40, 50];
//a = 10
//b = 30
```



#### func.call(this,多参)

-   多参数组
-   把参数依次传给func作参数



# Math

#### Math.max(多参)

#### Math.min(多参)

#### Math.ceil(float)

-   向上取整

#### Math.floor(float)

-   向下取整

#### Math.round(float)

-   四舍五入

#### Math.random()

-   得[0,1)的任一浮点数
-   Math.floor(Math.random()*num)
    -   得[0,num)的任一整数
-   Math.floor(Math.random()*(num+1))
    -   得[0,num]的任一整数
-   a + Math.floor(Math.random()*((b-a) + 1))
    -   得[a,b]的任一整数
-   针对数组
    -   arr = [1,2,3]
    -   数组随机索引值
    -   Math.floor(Math.random()*arr.length)



# Date

#### let date = new Date('timestr'/多参/…array/)

-   常用参数格式'2000-9-28 12:00:00'

-   默认为<u>现在时间</u>

-   实例化Date()

-   typeof(new Date()) //object

-   date*1 //当前时间戳(转换为number的方法均可)
    -   或者 date.valuOf() //当前时间戳

#### Date.gettime()

-   获取时间戳

#### new Date(timestamp)

-   将时间戳转换为iso格式

#### let date = Date('time')

-   typeof(new Date()) //string

-   date*1 //NaN

#### Date.now()

-   返回时间戳

#### date.getFullYear());

-   年

#### date.getMonth() + 1);

-   月

#### date.getDate());

-   日

#### date.getHours())

-   小时

#### date.getMinutes())

-   分钟

#### date.getSeconds());

-   秒



# Reflect

#### Reflect.ownKeys(obj)

-   返回 一个由目标对象自身的属性键组成的数组



# set

-   set对象允许你存储任何类型的唯一值,无论是[原始值](https://developer.mozilla.org/zh-CN/docs/Glossary/Primitive)或者是对象引用
-   set对象是值的<u>集合</u>,你可以按照插入的顺序迭代它的元素
-   Set中的元素只会**出现一次**，即 Set 中的元素是<u>唯一的</u>

#### let set = new Set([iterable])

-   与数组的区别:数组可以重复内容,set不可以

-   ```js
    let set = new Set('abc');
    // set -> {0:a,1:b,2:c}
    //相当与展开了
    ```

#### set.size()

-   `Set`对象中元素的个数

#### set.add(value)

-   对象尾部添加一个元素
-   返回该set对象

#### set.delete(value)

-   移除Set中与这个值相等的元素
-   返回 布尔 成功true

#### set.has(value)

-   表示该值在`Set`中存在与否

-   返回 布尔值

#### set.values()

-   返回 一个新的迭代器对象

-   该对象包含`Set`对象中的按插入顺序排列的所有元素的值

#### set.keys()

-   返回 一个新的迭代器对象

-   和values()一样

-   该对象包含`Set`对象中的按插入顺序排列的所有元素的值

#### set.entries()

-   返回 一个新的迭代器对象

-   个对象的元素是类似 [value, value] 形式的数组

-   该对象包含`Set`对象中的按插入顺序排列的所有元素的值

#### set.clear()

-   方法用来清空一个 `Set` 对象中的所有元素。

-   返回 undefined

### $ set去重

-   先将数组以可迭代对象的身份转换成set (集合化)
-   然后再展开(数组化)

```js
let arr = [1,2,1,3,2,4,5];
let brr = new Set(arr) //[1,2,3,4,5];
arr = [...brr] //[1,2,3,4,5];
```

#### $ set是的key和value一样的对象

$ 并集 交集 差集

```
let a = new Set([1,2,3,4]);
let b = new Set([2,3,4,5]);

//并集
let bing = new Set([...a,...b]) //[1,2,3,4,5]

//交集
let jiao = new Set([...a].filter((v)=>b.has(v)))

//差集
let cha = new Set([...a].filter((v)=>!b.has(v)))

```



# WeakSet

-   弱引用类型
-   非可迭代对象,即用不了类似values(),.size之类的属性及方法

-   引用时,不会增加引用变量的引用连接,且垃圾回收时会延后通知弱引用类型

####  new WeakSet([iterable])

-   **`WeakSet`** 对象允许你将*弱保持对象*存储在一个集合中。



# console

#### console.('a');

-   启动一个计时器

#### console.timeEnd('a');

-   停止一个同名计时器

-   配合使用,返回两时间戳之差

#### console.table(arr/obj);

-   表格化数组或对象 结构清晰



# Generator

-   生成器对象
-   **生成器**对象是由一个 [generator function](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/function*) 返回的,并且它符合[可迭代协议](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Iteration_protocols#iterable)和[迭代器协议](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Iteration_protocols#iterator)。

#### next()

-   返回 一个包含属性 `done` 和 `value` 的<u>对象</u>
-   done: 是否遍历完
-   value: 值 ,done为true时忽略



# Symbol(新数据类型)

#### let a = Symbol([description])

-   创建新的symbol类型,并用一个可选的字符串作为其描述
-   每次都会创建一个新的 symbol类型
-   不能new ,非完全构造函数

#### typeof a

-   //symbol

#### Symbol.description

一个只读的字符串，意为对该 Symbol 对象的描述

#### symbol.for([description])

-   从全局的symbol注册表设置symbol

#### symbol.keyFor([description])

-   从全局的symbol注册表取得symbol

#### Symbol.length = 0

-   长度为0

### $ 黑箱化数据调用

```js
let user_1 = {
    name: '李四',
    age: 25,
    key: Symbol()
}
let data = {
    [user_1.key]: '我是李四',
}
let need = data[user_2.key];
//这里data引用了一个无语义的key数据储存关于user_1的值
//在无需考虑数据链接语义时很好用
```





