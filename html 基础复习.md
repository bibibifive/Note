# html 基础复习



# 相对地址规范

【/】指：【根目录】

【./】指：【当前目录】

【../】指：【上一级目录】



# URL

协议://主机:端口/路径/资源



# 代码习惯

#### 语义化标签使用

-   使用大量语义化的标签有利于 理解 阅读 定位
-   因为所有标签地样式都可以通过css更改 这就更体现了使用语义化标签的意义
-   没有严格语义的内容用无语义的 块标签 div和 行内标签 span
-   一般 div 
-   一般 span 用于==微调文本==

## tag 主框架

```html
<body>
	<header>
  	头部区域
  	<nav>
    	导航栏区域
  	</nav>
	</header>

  <main>
    主内容区域(页面一个就行)
    <article>
      文段(块主体区域)
      <section>
        重复块状区域
      </section>
      <aside>
        边栏区域
      </aside>
    </article>
  </main>

	<footer>
		页脚区域 
	</footer>
</body>
```

## tag 不常用

#### <pre 源码打印标签 可以不修饰地输出源码内容

#### <p 文段标签

#### <hr 分隔线

#### <br 换行标签

#### <small 主要用于声明

#### <time 时间

#### <abbr 缩写 title属性为全称

#### <sub 下标

#### <sup 上标

#### <del 删除线

#### <ins 下划线

#### <s 错的 

#### <code 代码块

#### <progress 进度(条) ([value,max])

#### <strong / <em / <mark 突出高亮文本

#### <cite 来源(引用源)

#### <blockquote 块引用源

#### <address 地址



# tag 常用

#### <img 图片 

-   src资源 alt替换文本 title提示文本

-   这些静态文件可以放在云上,他们去实现CDN加速,让用户体验更好,我们只需要按需付费
-   或者自己在各地建设服务器CDN加速,以获得同样的用户体验(昂贵:建设成本,维护成本)

#### <a 链接 

-   href链接 title提示文本 target打开方式(_blank, _self ,覆盖某个标签页)

-   #### 锚点 给链接加上页面中的定位

-   ```html
    <a href='www.123.com/index.html#here'/>
    <div id='here'>
      点击跳转时会翻到here的位置
    </div>
    ```

-   href='tel:12356781234' 拨打电话

-   href='mailto:12356781@qq.com' 拨打电话

-   href='abc.jpg' / href='abc.psd' 

## form 表单

-   action处理脚本 method请求方法

#### <fieldset 表单区块

#### <legend 表单标题

#### <label 输入框标题

-   点到label 对应的input会上焦点

-   ```html
    <label>用户名
      <input type='text' name='username'>
    </label>
    
    <!--这俩一样-->
    
    <label for='user'>用户名</label>
      <input type='text' name='username' id='user'>
    ```

#### <input 输入框

-   type 类型(默认为文本类型)

    -   用一些前端验证库

    -   text 文本

        -   autocomplete 输入历史记录

    -   password 密码

    -   number 数字格式

    -   email 邮件格式

    -   tel 电话格式 移动端配备数字键盘

    -   hidden 隐藏并提交默认

    -   submit 提交表单(表单只接收一个submit)

    -   radio 单选框

        -   checked 选中

    -   checkbox

        -   checked 选中

    -   file 文件

        -   accept 允许文件类型

    -   date 日期 

        -   step 步长 min 最小 max 最大

    -   time 时间

    -   month 月

    -   week 周

    -   datatime-local 详细时期

    -   search 搜索

        -   有个一件删除按钮

        -   ```html
            <input type='search' list='asd'>
            <datalist id='asd'>
              <option value='first'>第一个</option>
              <option value='last'>最后一个</option>
            </datalist>
            ```

-   name 名字(键)(对接后台) 

    -   多个输入

-   value 内容(值/默认值) 

-   required 必填内容

-   readonly 只读文本(一般为后台控制必要文本,防止用户修改出错,可上传后台)

-   disabled 禁用(不可输入且不上传后台)

-   placeholder 提示文本(失焦后消失)

-   maxlength 最长字段

#### <textarea 文本域

-   cols 列数

-   rows 行数

-   ```html
    <textarea cols='20' rows='3' name='text'> 默认值区域 </textarea>
    ```

#### <select 选项组

#### <option 选项 (innerHTML才是文本含义)

#### <optgroup 选项分类

-   label 组名



## 列表

可以用list-style-type来设置列表样式

-   decimal 数字(十进制)…

可以用list-style:none 来取消列表项目头

#### <ol 有序列表 (order list)

-   start 开始序号

#### <ul 无序列表 (unorder list)

#### <li 列表项目 

#### <dl 描述列表 (description list)

#### <dt 描述标题 (title)

#### <dd 描述内容 (data)



## 表格

#### <table 表格

#### <thead 表格头部

#### <tbody 表格内容

#### <tr 行

#### <td 数据

-   rowspan 跨行
-   colspan 跨列

#### 不规则表格 - 单元格合并



## 多媒体

#### <video 视频

-   autoplay 自动播放 (大概率不会播放)
-   muted 静音 配合autoplay可以播放
-   controls 控制器
-   poster 没播放前的预览图片
-   preload 加载方式
    -   auto 自动加载
    -   metadata 关键信息加载
    -   none 不自动加载
-   loop 循环播放
-   video.js - - 第三方插件

#### <source 资源

-   可切换源(适应特殊情况)

-   ```html
    <video autoplay loop controls>
      <source src='abc.mp4' type='video/mp4'/>
      <source src='abc.webm' type='video/webm'/>
    </video>
    ```



#### audio 音频

-   大多属性和video一样

-   ```html
    <audio controls muted preload="auto">
      <source src="houdunren.ogg" type="audio/ogg"/>
      <source src="houdunren.mp3" type="audio/mp3"/>
    </audio>
    ```



# 图片处理

网络带宽成本很高，图片处理在保证用户体验好的前端下，文件尺寸也要尽可能小

图片属性静态文件，不要放在WEB服务器上，而放在云储存服务器上并==使用CDN加速==

#### 文件清晰的情况下 越小越好(节省带宽)

#### 大图 输出jpg的切图(文件小,且颜色较丰富,保留信息相对可观)

#### 小图标 验证码 优先使用==图标文字库==,或使用png无损压缩,支持透明

#### 动画 gif(256色),支持透明

#### (印刷 cmyk 4色 Tiff)



# http协议

#### [http请求之get和post的区别](https://www.cnblogs.com/zymnstlm/p/9479634.html)

Get发一个TCP数据包

Post发两个TCP数据包



#### 无连接

### 无状态

请求行
请求头
空一行
请求体

[cookie，session傻傻分不清楚？](https://www.cnblogs.com/nickjiang/p/9148136.html)

#### cookie 存在客户端的键值对显式信息

-   信息容易被窃取
-   要求客户端占用储存空间

#### session 存在客户端的键值对隐式信息

-   set一个cookie给用户,需要时用户伴随该cookie一同请求
-   保留一个对应session信息以供用户鉴权
-   与服务器的session会话鉴权
-   要求服务器和客户端双方都占用储存空间
-   可能占用大量服务器储存空间

#### token 存在客户端的键值对隐式信息

-   加密一个token给用户,需要时用户伴随该token一同请求
-   通过<u>特定算法</u>解码用户token鉴权
-   要求客户端占用储存空间