# css基础复习

css 层叠样式表

层叠 即其后面覆盖前面, 新的覆盖旧的, 就近原则的特性(在优先级相同时)



#### css文件解析

遇到无法解析的内容直接跳过, 不解析

每个语句要用分号`;`隔开, 否则会错误解析



#### css原生引用外部样式

```css
@import url("common/menus.css");
```



# 选择器

#### * 通配符选择器

-   通用选择

#### id 选择器

-   唯一的值

#### class 选择器

-   多元素选择器

## 属性选择器

```
[attr]
```

-   表示带有以 attr 命名的属性的元素。

```
[attr=value]
```

-   表示带有以 attr 命名的属性，且属性值<u>为</u> value 的元素。

```
[attr~=value]
```

-   表示带有以 attr 命名的属性的元素，并且该属性是一个<u>以空格作为分隔</u>的<u>值列表</u>，其中<u>至少有一个</u>值为 value。

```
[attr| = value]
```

-   表示带有以 attr 命名的属性的元素，属性值为“value”或是以“value-”为前缀（"`-`"为连字符，Unicode 编码为 U+002D）开头。典型的应用场景是用来匹配语言简写代码（如 zh-CN，zh-TW 可以用 zh 作为 value）。

```
[attr^=value]
```

-   表示带有以 attr 命名的属性，且属性值是以 value <u>开头</u>的元素。

```
[attr$=value]
```

-   表示带有以 attr 命名的属性，且属性值是以 value <u>结尾</u>的元素。

```
[attr*=value]
```

-   表示带有以 attr 命名的属性，且属性值<u>至少包含一个</u> value 值的元素。



#### 代际选择器

`空格` 后代选择器 

`>` 子代选择器

`~` 兄弟选择器(向后查询)

`+` 临近兄弟选择器(向后查询最近一个)



#### 伪类

:link 链接

:hover 悬停

:active 按下

:focus 焦点

:visited 已访问 (缓存状态可删除)



:target 选择器可用于选取当前活动的id元素。(动态赋予样式)

:root 根元素

:empty 没有内容的(没有innerHTML的)



#### 结构伪类选择器

:first-child ==为==第一个子元素

-   ```css
    div :first-child{color:red};
    /*表示div中的所有后代中 取是子元素且为第一个的元素 */
    
    div:first-child{color:red};
    /*为子元素且为第一个的元素 */
    ```

:first-child ==为==第一个子元素
:first-of-type 为第一个该类型子元素

:last-child 为最后一个子元素
:last-of-type 为第一个该类型的子元素

:only-child 为唯一子元素
:only-of-type 为唯一该类型的子元素

:nth-child() 为顺序几个子元素
:nth-of-type() 为顺序该类型的几个子元素

-   :nth-child(1) 为第一个子元素
    :nth-child(n) 为全部子元素(0,1,2,3)
-   :nth-child(2n) 为偶数子元素 (1,3,5,…)
    :nth-child(2n-1) 为奇数子元素 (0,2,4,…)
-   :nth-child(even) 为偶数子元素
    :nth-child(odd) 为奇数子元素
-   :nth-child(-n+2) 为前两个子元素 (2,1,0,…)
    :nth-child(n+2) 为第二个开始的全部子元素 (2,3,4,…)

:nth-last-child() 为逆序几个子元素
:nth-last-of-type() 为逆序该类型的几个子元素

-   跟:nth-child() 用法相似

:not 排除

-   ```css
    body div:not(:nth-child(n+3)) {
      color: red;
    }
    /* 即选中body 中为前两个子元素的div */
    ```



### 表单中的伪元素

input:disabled 禁用元素

input:enabled 可用元素

input:valid 有效元素

input:invalid 无效元素

input:required 必填元素

input:optional 可填元素(非required)

input:checked 选中的(选项)



### 伪类

::first-letter 首个字母

::first-line 首行

::after 后面插入content

::before 前面插入content





# 权重

| 规则           | 权重        |
| -------------- | ----------- |
| ID             | 0100 (100)  |
| class 类属性值 | 0010 (10)   |
| 标签 伪元素    | 0001 (1)    |
| *              | 0000 (0)    |
| 行内样式       | 1000 (1000) |

#### 从父元素继承的样式没有权重

#### 继承并不是全都继承, 像详细的boder不一定会继承



## !important

-   非必要不使用
    -   当得不到元素时,应降低当前最高优先级(如id->属性);
-   没有其他的!important影响下, 无视优先级, 按照就近原则
-   有其他的!important, 按照优先级来选择
-   