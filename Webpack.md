# Webpack





# 局部 Webpack 配置

在命令行使用全局的Webpack 打包

在命令行使用局部的Webpack 打包 (npx Webpack --entry ./src/main.js) 添加配置

在package.json 配置一些短命令

```json
"scripts": {
  "build": "Webpack --entry ./src/main.js --output-path ./build"
}
```

在命令行中写入的入口导出文件配置可以写在 Webpack.config.js文件中

且 导出路径 为 绝对路径

```json
const path = require('path')

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "build.js",
    path: path.resolve(__dirname, 'dist')
  },
  ...
}
```

且 还可以改变 Webpack 的 config 配置文件的路径

```json
"scripts": {
  "build": "Webpack --config my.Webpack.js"
}
```



#### `Webpack.config.js`

-   有更多的配置项需要自定义



## Webpack依赖图

==要处理某个依赖资源==的时候就把他加到==依赖关系==(入口文件中)当中.Webpack才能对它进行打包操作

如果后期需要自定义配置文件的相关内容, 可以在package.json中的Webpack短语句增加 `--config ~` 来指定当前的配置文件的名称





# loader

Webpack默认情况下只能处理js和json, 所以其他的资源模块需要引进相应的loader.

不是所有模块都能直接当文件进行使用, 所以通过loader对它进行==转换==

loader要安装 (npm i css-loader -D)

用css-loader为例 (让Webpack识别css语法)

#### 3种配置loader的方式

行内loader / 配置文件中设置loader / 使用命令行配置loader(被废弃)

#### 行内语法

```js
import 'css-loader!../css/login.css'
```

#### 配置文件语法

1.  最全写法

```json
module: {
  rules: [
    {
      test: /\.css$/,
      use: [
        {
          loader: 'css-loader'
          options: ...
        }
      ]
    }
  ]
}
```

2.   中档简写

-   有些loader不需要多余的参数

```json
...
      test: /\.css$/,
      use: [
        'css-loader',
        {other loader}
      ]
...
```

3.   最简写

-   只有需要一个loader

```json
...
      test: /\.css$/,
      loader: 'css-loader'
...
```

#### loader执行顺序

从右往左, 从下往上



# sass-loader

npm i sass-loader -D

配置loader

```json
...
      {
        test: /\.scss$/,
        use: ['style-loader', 'css-loader', 'sass-loader']
      }
...
```

#### sass -> css -> style



# browserslistrc

browsers-list-rc

1.  工程化
2.  兼容性(新特性支持)
3.  如何实现兼容? 兼容工具
4.  兼容哪些平台? 一些条件(大于多少市占率的平台) (==caniuse.com==)
4.  一些条件 (==browserslistrc==)

`>1%`
`default`
`dead`
`last 2 version`

#### 在package.json中配置

```json
"browserslist":[
    ">1%",
    "last 4 version",
    "not dead"
]
```

#### 单个配置文件

.browserslistrc 文件写入

```
> 1%
last 1 version
not dead
```





# post css

1.  什么是post css
2.  为处理css的平台兼容性 (我们需要对css的前缀做兼容性处理)

帮助js来转换css样式 (通过browserslistrc来筛选)



npm i postcss -D

npm i postcss-cli -D (在命令行终端可以使用 npx postcss )

npm i autoprefixer -D 

#### autoprefixer 插件

可以给样式添加兼容前缀



# postcss-loader

post-loader

`style-loader` <- `css-loader` <- `postcss-loader`

autoprefixer (浏览器平台兼容)

==postcss-preset-env== (插件集合) (包含autoprefixer)

1.  :颜色16进制 ->rgba (新属性转化)
2.  :--webkit--transition (前缀添加)



postcss-loader 用得比较多而且配置也多 可以做复用, 所以:

可以写一个 `postcss.config.js` 配置文件导出一个配置对象

当读到postcss-loader的时候就查找它是怎么配置的

然后在整体loader配置中就可以简写了



# importLoaders属性

`importLoaders` ==loader回溯==

在该loader 有新的内容引入需要前面的loader再处理时添加的参数

```json
{
  loader: 'css-loader',
  options: {
    importLoaders: 1
  }
}
```

css-loader可以处理 @import 也就引入了新的需要处理(兼容性)的css

但是前面的post-loader已经使用过了, 所以需要一个参数 `importLoaders` 来回溯1次, 有更多的loader就更多次.





# file-loader

打包图片

## 创建img标签

#### img src

```json
test: /\.(png|svg|gif|jpe?g)$/,
use: ['file-loader']
```

1.  使用require导入图片，此时如果不配置 `esModule:false ` ,则需==.default导出==

    -   在 Webpack5 中 esModule 会把在 4 中的结果封装在一个键为default的对象中

    -   所以要访问 require之后还要补上.default

2.  也可以在配置当中设置 `esModule：false`

    ```json
    test: /\.(png|svg|gif|jpe?g)$/,
    use: [
      {
        loader: 'file-loader',
        options:{
          esModule: false //不转为esModule
         }
      }
    ]
    ```

3.  用 `esModule` 的导出规范
    采用==import== xxx from图片资源，此时可以直接使用XXXX 👍

## 设置背景图片 

require 语法会默认导出一个module 

但是又不能像上一种那样加一个.default, 因为它是css文件

所以只能以第二种方法 <u>在配置当中设置 `esModule：false`</u>



#### 总结: 

1.  #### 首先Webpack默认不能处理图片资源类型, 要借助于file-loader

2.  #### 常用图片场景

    1.  img src属性 (用 `import` 导入图片)
    2.  背景图 (在配置中设置 `esModule：false`)



# file-loader 详细配置

图片名字配置

未配置的名称是用 md4 生成对应文件内容的哈希值

设置占位符 (place-holder)

name 属性

语法

```json
options:{
	name: '[name].[hash:6].[ext]'
}
```

[name] : 文件名
[ext] : 扩展名
[hash] : 文件内容->哈希值
[contentHash] : 
[hash : <length> ]
[path] : 



# url-loader



1.  url-loader base64uri 置入最终导出js文件当中，==减少请求次数==
2.  file-loader 将资源拷贝至指定的目录，==分开请求==
3.  url-loader内部其实也可以调用 file-loader
3.  limit 阈值

url-loader 内置了 file-loader

```json
options:{
	name: '[name].[hash:6].[ext]',
  limit: 200*1024 //200kb以上的用file复制, 以下植入到代码一起请求
}
```



# asset module type

`Webpack5 ` 内置了 asset module type(资源类型模块)

常见配置选项

1.  asset/resource -> file-loader (资源)
2.  asset/inline -> url-loader (行内)
3.  asset/source -> raw-loader 
4.  类limit功能

==type== : asset

==generator== 生产配置

### 重定向输出路径

#### ==全部文件类型==都导出到==单一文件夹==中 语法

```json
entry:'./src/index.js',
output:{
  filename: 'main.js',
  path: path.resolve(_dirname,'dist'),
  assetModuleFilename: "img/[name].[hash:4][ext]"
}
```

#### 按处理文件分组 语法

```json
{
  test: /\.(png svg gif jpe?g)$/ ,
  type:'asset/resource' ,
  generator:{ 													//产出
    filename:"img/[name].[hash:4][ext]"
  }
}
```

<u>分组按照 test也就是正则查找处理的文件导出到同一个文件家中并格式化文件名称</u>



# asset (for Font)

配置跟图片的类似, 且只需要 `asset/resource` ,因为只是复制到指定路径

在css 中引入字体文件 `@font-face`

最好把字体原始css样式放在 `src/font` 文件夹下

把重定义的放在index.css中 ,在 `src/css` 中



# Webpack 插件

1.  安装第三方插件
2.  在GitHub官网参考它的使用规则
3.  在导出配置项中新建一个 `plugin` 数组, 可以放多个插件
4.  一个插件本质就是一个类, 用new 构造一个实例, 传入可能的参数

```js
const { CleanWebpackPlugin } = require('clean-Webpack-plugin')
//引入这个插件

module.exports = {
 ...
  plugins: [
    new CleanWebpackPlugin()
  ]
}
```

#### clean-Webpack-plugin 自动更新 ==dict== 文件





# html-Webpack-plugin

[html-Webpack-plugin 使用方法](https://www.npmjs.com/package/html-Webpack-plugin)

可以在 `dict` 动态导出 `html`

```js
const HtmlWebpackPlugin = require('html-Webpack-plugin') 
//源于插件作者怎么规划插件使用, 此处不是解构

module.exports = {
 ...
  plugins: [
    ...,
    new HtmlWebpackPlugin({
      title: 'html-Webpack-plugin',  //动态更新 title
      template: './public/index.html'  //去找到模板文件
    }),
  ]
}
```



### define-plugin

[define-plugin 使用方法](https://Webpack.js.org/plugins/define-plugin/#root)

Webpack自带插件, 只需要从 Webpack 中解构出来就行

```js
const { DefinePlugin } = require('Webpack')

module.exports = {
 ...
  plugins: [
    ...,
    new DefinePlugin({
      BASE_URL: '"./"' //需要额外打包一层引号 1->'1'
    })
  ]
}
```

全局常量



#### `public` 文件夹 一般是放一些直接复制, 不需要Webpack打包的资源





# Babel

1.  为什么需要Babel
    1.  不是所有浏览器都能兼容新特性 (JSX, TS, ES6+)
    2.  Babel只是个工具, 本身不具备什么功能
    3.  应该加载对应修改功能的工具包
2.  Babel应该是个工具包载体

[@babel/plugin-transform-arrow-functions --npm](https://www.npmjs.com/package/@babel/plugin-transform-arrow-functions)

babel有预设

#### npm i @babel/core 微内核

#### npm i @babel/cli 在命令行中使用并配置 babel

#### npm i @babel/preset-env 大部分预设



# Babel-loader

可以自由地在开发阶段使用新特性了

#### npm i babel-loader

1.plugins (根据插件)

```js
{
  test: /\.js$/,
  use: {
    loader: 'babel-loader',
    options: {
      plugins: [
        '@babel/plugin-transform-arrow-functions',
        '@babel/plugin-transform-block-scoping',
      ]
    }
  }
}
```

2.presets (根据预设)

```js
{
  test: /\.js$/,
  use: {
    loader: 'babel-loader',
    options: {
      presets: ['@babel/preset-env']
    }
  }
}
```

#### 配置性的东西最好以文件的形式做管理, 提高复用性

#### 例如:.browserslistrc(兼容阈值查询)

#### 单写配置文件(babel7之后是多包管理方式)

#### 建议使用单拎出来的配置文件(为了==解开嵌套层级==)

#### babel.config.js



# polyfill

#### 问什么使用polyfill

1.  预设preset 转换有限的兼容性问题 需要额外的补丁
2.  按需配置: Webpack4 ->Webpack5时把自带的polyfill删除了, 为了减少打包时间



core-js ->专门处理语法功能 stable

regenerator-runtime -> generator/async/await/promise 之类的这些的

### polyfill配置语法

```js
module.exports = {
  presets: [
    [
      '@babel/preset-env',
      {
        useBuiltIns: 'usage',
        corejs: 3
      }
    ]
  ]
}
```

#### useBuiltIns 属性的三个参数

1.  false: 不对当前的JS处理做polyfill的填充
2.  usage: 依据用户源代码当中所使用到的新语法进行填充
3.  entry: 依据我们当前筛选出来的浏览器决定填充什么

2.presets (根据预设)

#### exclude: /node_modules/,

因为 node_modules 中可能会给promise也加一个polyfill,

而项目打包的时候也加一个polyfill, 同一个浏览器平台可能会出现问题

所以在应该loader的时候把node_modules 的东西去除掉

```js
{
  test: /\.js$/,
  use: {
    loader: 'babel-loader',
    options: {
      exclude: /node_modules/,
      presets: ['@babel/preset-env']
    }
  }
}
```

# copy-Webpack-plugin

#### npm i copy-Webpack-plugin -D

[copy-Webpack-plugin](https://www.npmjs.com/package/copy-Webpack-plugin/v/9.1.0)

@9.1.0 版本比较稳定

不是所有内容都要拷贝的配置

```js
const CopyWebpackPlugin = require('copy-Webpack-plugin')

new CopyWebpackPlugin({
  patterns: [
    {
      from: "public",
      globOptions: {
        ignore: ['**/index.html']
      }
    }
  ],
}),
```



# dev-server

npm i Webpack-dev-server -D

### 开发模式

1.  watch
2.  live server

#### 之前的不足

1.  所有源代码都会重新编译
2.  每次编译成功之后都需要进行文件读写()
3.  live server
4.  不能实现局部刷新 (热刷新)

```js
"scripts": {
  "build": "Webpack --config my.Webpack.js", //手动布局
  "serve": "Webpack serve --config my.Webpack.js" //内存自动布局
},
```

#### dev-server的优点

热更新

内存中完成, 不需要硬盘读写

开启本地服务器



# dev-middleware

#### 高自由度打包 (少用)

先得到配置文件 -> 调用函数Webpack得到一个compiler

利用中间件交给express

```js
const express = require('express')
const Webpack = require('Webpack')
const WebpackDevMiddleware = require('Webpack-dev-middleware')

// 中间件
const app = express()

// 获取配置文件
const config = require('./my.Webpack.js')
const compiler = Webpack(config)

app.use(WebpackDevMiddleware(compiler))

// 开启端口上的服务
app.listen(3000, () => {
  console.log('服务运行在 3000 端口上');
})
```



# 模块热替换 HMR

#### HMR (hot model replacement)

在开发阶段, 把.browserslistrc文件屏蔽掉, 

```js
target:'web' //.browserslistrc文件屏蔽掉
```

然后使用dev-server服务, 并更新配置

```js
devServer: {
  hot: true //允许热更新, 此时还是整个页面一起更新的
},
```

可以在入口文件中(index.js), 把想要热更新的依赖模块

```js
if (module.hot) {
  module.hot.accept(['./title.js'], () => {
    console.log(热更新完毕);
  })
}
```





# HMR->React

1.  Webpack 配置 React 打包操作 (jsx语法)

2.  #### 需要安装的库

    1.  react
    2.  react-dom
    3.  @babel/preset-env (es6+兼容性问题)
    4.  @babel/preset-react (用于转换jsx语法)
    5.  @pmmmwh/react-refresh-Webpack-plugin (使react可以热更新)
    6.  react-refresh  (作为babel loader 的 loader 以让react组件可以热更新)

-   #### 配置文件首先 (Webpack.config.js)

```js
  target: 'web',
  devServer: {
    hot: true,
  },
    
    
module: {
  rules: [
    ...
    {
      test: /\.jsx?$/,  //react 的jsx 也在检索范围内
      use: ['babel-loader']  
    }
]
```

-   #### 配置 babel 配置文件

```js
module.exports = {
  presets: [
    ['@babel/preset-env'],
    ['@babel/preset-react']
  ],
  plugins: [
    ['react-refresh/babel']  //热更新react
  ]
}
```

-   #### 设置react 的模板 (App.jsx)

```js
import React, { Component } from 'react'

class App extends Component{
  constructor(props) {
    super(props)
    this.state = {
      title:'前端123'  //修改模板以验证热更新react
    } 
  }
  
  render() {
    return (<div><h2>{this.state.title}</h2></div>)
  }
}

export default App
```

-   #### 渲染出来react 的组件 (index.js)

```js
import React from 'react'
import ReactDOM from 'react-dom'
import App from './App.jsx'

...
ReactDOM.render(<App />, document.getElementById('app'))
```



# vue-loader

#### -D (开发依赖)

npm i vue

npm i vue-loader -D 

npm i vue-template-compiler -D (编译和操作)



# output

#### **path** 是用于告知 **Webpack** 指向哪个目录下输出本地资源文件

```js
  output: {
    filename: "js/build.js",
    path: path.resolve(__dirname, 'dist'),
    publicPath: ''
  },
```

-   #### publicPath:==index.html==内部的引用路径

-   #### 域名+publicPath+filename

#### publicPath:  (找静态资源)

1.  #### ''   (自动填充'/')  or 

2.  #### '/'  (绝对路径)     or 

3.  #### './' (相对路径)



# devServer

#### publicPath: 告诉浏览器 内部的引用路径

```js
  devServer: {
    hot: true,
    publicPath: '/',
    contentBase: path.resolve(__dirname, 'public'),
    watchContentBase: true
  },
```

#### 强烈建议 把 devServer 里的 ==publicPath== 和 output 中的设置为一样的



#### contentBase 打包后的资源引入了一个没有打包的资源

```js
    contentBase: path.resolve(__dirname, 'public'),
```

#### 没有打包的资源就会在这个目录下查找

#### 强烈建议为绝对路径

#### watchContentBase 用于监视未打包部分的修改刷新





# devServer 其他配置

```js
  devServer: {
    hot: 'only',  //都只热更新
    port: 4000, //设置端口号
    compress: true,  //压缩入口文件
    historyApiFallback: true,  //保证在只有前端流开发spa的时候没有404
  },
```



# 请求代理设置 (开发阶段)

不同的地址, 根据同源策略, 有==跨域==的问题 -> 代理转发操作

通过代理(服务端代替客户端请求服务端数据)的方式完成,

跨域的数据请求(因为服务端之间没有跨域问题)

```js
proxy: {
    '/api': {
      target: 'https://api.github.com',  //数据获取目标地址
      pathRewrite: { "^/api": "" },  //重写Url
      changeOrigin: true  //欺骗服务器, ->客户端伪装请求(实为服务代理)
    }
  },
```



# resolve (解析)

#### 先确定路径

1.  相对路径
2.  绝对路径
3.  模块名称 直接找->(node_modules)

#### 之后 ->

确定这是个 文件 还是个 文件夹

文件夹 -> 补全一个 index文件

文件   -> 补全 默认是 js 或者 json

#### extensions 默认值数组

```js
  resolve: {
    extensions: [".js", ".json", ".ts", ".jsx", ".vue"], //加入常用的文件后缀名
    alias:{  //为常用的路径命名以简化编写
      '@':path.resolve(__dirname,'src')
    }
  },
```





# 模式(Mode)

提供 `mode` 配置选项，告知 Webpack 使用相应模式的内置优化。

```js
  mode: 'production': 'none' | 'development' | 'production'
```



# source-map

映射 -- 在调试的时候可以定位到源代码中的信息 (让源代码和编译后的代码有一一对应关系)

真是的源代码 和浏览器中运行的代码是有差异的, 因为通过Webpack处理过了,

所以在定位代码问题中, 会默认显示打包后的情况, 让修改纠正显得困难

在开发阶段, 我们是需要source-map的, ==有利于调试代码==

```js
  devtool: 'source-map',  //这是vue在开发阶段的默认配置方式
```



# devtool配置

[devtool 文档](https://Webpack.docschina.org/configuration/devtool/)

用devtool 给source-map更多配置

eval ->会把映射关系放在行尾, 提供源代码文件的位置

source-map ->会直接在文件末尾链接到.map的文件, 然后直接提供源代码的错误位置

### Tip

验证 devtool 名称时， 我们期望使用某种模式， 注意不要混淆 devtool 字符串的顺序， 模式是： `[inline-|hidden-|eval-] [nosources-] [cheap-[module-]] source-map`.

1.  eval: 在==eval行末==给到 `base64` 压缩的map信息
2.  inline: 在==文件末尾==给到 `base64` 压缩的map信息
3.  hidden: 会提供.map映射文件, 但是不会在编译后的文件中放链接信息 (==不主动定位到源代码==)
4.  nosource: 会告诉你哪个==源文件有问题==, 但是没有定位到错误位置 (==粗糙==)
5.  cheap: ==减少消耗==(列信息), 只告诉源文件的行信息, 
6.  module: ==友好==地把==loader处理过==的信息按处理前的源代码错误信息定位



#### vue `source-map`

#### react  `cheap-module-source-map`

个人小项目推荐 `cheap-module-source-map`





# ts-loader 编译TS

npm i ts-loader -D

npm i typescript -D

tsc –init ->生成一个tsconfig.json的文件



可以用命令行, 在同一文件夹下编译成js

```
tsc .src/index.ts
```

挂载ts-loader

```js
  {
    test: /\.ts$/,
    use: ['ts-loader']
  },
```

#### 然而这是不够的 

这样子的loader只能将ts->js, 而不能添加polyfill.

```js
  {
    test: /\.ts$/,
    use: ['ts-loader']
  },
```

###### [babel.config.js]

```js
module.exports = {
  presets: [
    ['@babel/preset-env', {
      useBuiltIns: 'usage',
      corejs: 3
    }],
    ['@babel/preset-typescript']
  ],
}
```

#### 但是任然还有缺陷,

因为用babel-loader处理的ts文件不会报语法错误, 即编译阶段不会知道错误, 只有在运行阶段才会发现

用ts-loader就可以

### 折中方案

在打包前进行ts 语法校验

###### [package.json]

```js
  "build": "npm run verifyts && Webpack",
...
  "verifyts": "tsc --noEmit"
```





# 配置文件的拆解和合并

1.  在base配置当中拿到我的打包模式 (prod|dev)
2.  把配置信息做了拆分 (拆分管理难免有路径变更问题: 写一个路径小工具)
3.  基于模式进行合并 (merge())









