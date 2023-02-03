# CommonJS


### CommonJS 之 `require`
`require` 命令的基本功能是，读入并执行一个 js 文件，然后返回该模块的 `exports` 对象。

第一次加载某个模块时，Node.js 会缓存该模块。以后再加载该模块，就直接从==缓存==取出该模块的 module.exports 属性返回了。

```js
// a.js
var name = 'morrain'
var age = 18
exports.name = name
exports.getAge = function(){
    return age
}
// b.js
var a = require('a.js')
console.log(a.name) // 'morrain'
a.name = 'rename'
var b = require('a.js')
console.log(b.name) // 'rename'
```

第二次 require 模块A时，并没有重新加载并执行模块A。而是直接返回了第一次 require 时的结果

CommonJS 模块的加载机制是，require 的是被导出的值的拷贝。也就是说，一旦导出一个值，模块内部的变化就影响不到这个值 。

其它前端模块化的方案
后面发展起来了众多的前端模块化规范
![enter image description here](https://pic2.zhimg.com/80/v2-daf2d469b3376d042e11c58782170e55_720w.jpg)


## 但这些都成为历史了

## 现在有ES6的模块化规范了

# ES6 Module

ES6 Module 也是如此，模块功能主要由两个命令构成：`export` 和 `import`。`export` 命令用于导出模块的对外接口，`import` 命令用于导入其他模块导出的内容。

```js
export {
    name,
    getAge
}
```

```js
import { name, getAge } from 'a.js'
```

除了指定加载某个输出值，还可以使用整体加载，即用星号（*）==指定一个对象==，所有输出值都加载在这个对象上面。 

```js
import * as a from 'a.js'
```

使用 import 命令的时候，用户需要知道所要导入的变量名，这有时候比较麻烦，于是 ES6 Module 规定了一种方便的用法，使用 `export default` 命令，为模块指定==默认输出==。

```js
export default {
    name,
    getAge
}
```

```js
import a from 'a.js'
```

显然，一个模块==只能有一个默认输出==，因此 `export default` 命令只能使用一次。同时可以看到，这时 import 命令后面，不需要再使用大括号了。


ES6 Module 的设计思想是尽量的==静态化==，使得编译时就能确定模块的依赖关系，以及导入和导出的变量，也就是所谓的"==编译时加载=="。

正因为如此，`import` 命令具有==提升==效果，会提升到整个模块的头部，首先执行。

也正==因为 ES6 Module 是编译时加载==， 所以==不能使用表达式和变量==，因为这些是只有在运行时才能得到结果的语法结构。如下所示

```js
// 报错
import { 'n' + 'ame' } from 'a.js'

// 报错
let module = 'a.js'
import { name } from module
```