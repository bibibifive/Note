# Http


# HTTP缓存

`优点`
1. 提升响应速度
  - 可复用性有几个优点。首先，由于不需要将请求传递到源服务器，因此**客户端和缓存越近，响应速度就越快**。最典型的例子是浏览器本身为浏览器请求存储缓存。
2. 减轻服务端的压力

## HTTP Cookie

document.cookie
`定义`
Cookie 是直接存储在浏览器中的一小串数据。它们是 HTTP 协议的一部分，由 RFC6265 规范定义。

Cookie 通常是由 Web **服务器**使用响应 `Set-Cookie` `HTTP-header` 设置的。然后**浏览器**使用 `Cookie` `HTTP-header` 将它们自动添加到（几乎）每个对**相同域**的请求中。

可以使用 **document.cookie** 属性从浏览器访问 cookie。

### 特殊字符（空格），需要编码

内建方法 **encodeURIComponent**

```js
//特殊字符（空格），需要编码
let name = 'my name'
let value = 'John Smith'
//将cookie编码为my%20name=John%20 Smith
document.cookie = encodeURIComponent(name) + '=' + encodeURIComponent(value)
alert(document.cookie) //...;my%20name=John%20Smith
```

`限制`

- name=value 对，大小不能超过**4KB**。
- 每个域的 cookie 总数不得超过 20+左右，具体限制取决于浏览器。

### 几个选项

> Cookie 有几个选项，其中很多都很重要，应该设置它。

选项被列在 **key=value 之后**，以`；`分隔，像这样：


# 长轮询

长轮询是一种长连接，长轮询