# Ajax

## form表单与模板引擎

### form表单的常用属性
#### action——URL地址
#### method——get或post
#### enctype——编码
#### target——在何处打开 action URL

### 阻止表单的默认提交行为
#### 表单只负责采集数据，Ajax 负责将数据提交到服务器。
#### 当监听到表单的提交事件以后，可以调用事件对象的 event.preventDefault() 函数
### 使用jQuery快速获取表单数据
####  serialize() 函数
##### 一次性获得表单中的所有数据
##### 必须为每个表单元素添加 name 属性！
### 安装和使用模板引擎
1.导入 art-template
在 window 全局，多一个函数，叫做 template('模板的Id', 需要渲染的数据对象) 
2.定义数据
模板的 HTML 结构，必须定义到 script 中
3.定义模板
4.调用 template 函数
函数返回值是一个渲染好的HTML字符串，存储到变量htmlStr里面
5.渲染HTML结构
```
$('#container').html(htmlStr)
```
### 模板引擎的实现原理
#### 定义模板结构
```
<script type="text/html" id="tpl-user">
   <div>姓名：{{name}}</div>
   <div>年龄：{{ age }}</div>
   <div>性别：{{  gender}}</div>
   <div>住址：{{address  }}</div>
</script>
```
#### 预调用模板引擎
```
<script>
   // 定义数据
   var data = { name: 'zs', age: 28, gender: '男', address: '北京顺义马坡' }
   // 调用模板函数
   var htmlStr = template('tpl-user', data)
   // 渲染HTML结构
   document.getElementById('user-box').innerHTML = htmlStr
</script>
```
#### 封装 template 函数
```
function template(id, data) {
  var str = document.getElementById(id).innerHTML
  var pattern = /{{\s*([a-zA-Z]+)\s*}}/
  var pattResult = null
  while ((pattResult = pattern.exec(str))) {
    str = str.replace(pattResult[0], data[pattResult[1]])
  }
  return str
}
```
#### 导入并使用自定义的模板引擎
```
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>自定义模板引擎</title>
    <!-- 导入自定义的模板引擎 -->
    <script src="./js/template.js"></script>
</head>
```

## 同源策略
### 浏览器提供的一个安全功能。
### 同源策略限制了从同一个源加载的文档或脚本如何与来自另一个源的资源进行交互。这是一个用于隔离潜在恶意文件的重要安全机制。

## 跨域
### 同源指的是两个 URL 的协议、域名、端口一致，反之，则是跨域。
### 跨域请求方案
#### JSONP——临时解决方案。缺点是只支持 GET 请求
#### CORS——跨域 Ajax 请求的根本解决方案。支持 GET 和 POST 请求。缺点是不兼容某些低版本的浏览器。

## JSONP 
### (JSON with Padding) 是 JSON 的一种“使用模式”，可用于解决主流浏览器的跨域数据访问的问题。
### 原理：通过script标签的 src 属性，请求跨域的数据接口，并通过函数调用的形式，接收跨域接口响应回来的数据。
### 注：JSONP 和 Ajax 之间没有任何关系，不能把 JSONP 请求数据的方式叫做 Ajax，因为 JSONP 没有用到 XMLHttpRequest 这个对象。
### jQuery中JSONP——动态向 header中append 一个创建和移除 script标签


## 防抖
### 防抖策略（debounce）是当事件被触发后，延迟 n 秒后再执行回调，如果在这 n 秒内事件又被触发，则重新计时。
### 防抖能保证只有最后一次触发生效！

## 节流
### 节流策略（throttle），顾名思义，可以减少一段时间内事件的触发频率。
### 节流是有选择性地执行一部分事件

## XMLHttpRequest
查询字符串：格式：url?参数=值&参数=值
URL编码：使用英文字符去表示非英文字符
浏览器会自动对 URL 地址进行编码操作，不关心
数据交换格式：XML和JSON（JavaScript 对象表示法，表示 Javascript 的对象和数组，主流）
### JSON——本质是字符串
#### 对象结构——key 必须是使用英文的双引号包裹的字符串，value 的数据类型可以是数字、字符串、布尔值、null、数组、对象
#### 数组结构——数字、字符串、布尔值、null、数组、对象
#### JSON 序列化——数据对象转换为字符串——JSON.stringify() 
#### JSON 反序列化——字符串转换为数据对象—— JSON.parse()
### 发起Ajax请求
#### 使用xhr发起GET请求
> 1.创建 xhr 对象
2.调用 xhr.open() 函数
3.调用 xhr.send() 函数
4.监听 xhr.onreadystatechange 事件

#### 使用xhr发起POST请求
> 1.创建 xhr 对象
2.调用 xhr.open() 函数
3.设置 Content-Type 属性（固定写法）
4.调用 xhr.send() 函数，同时指定要发送的数据
5.监听 xhr.onreadystatechange 事件

### 封装自己的Ajax函数

```
//1 要实现的效果
<!-- 1. 导入自定义的ajax函数库 -->
<script src="./itheima.js"></script>

<script>
    // 2. 调用自定义的 itheima 函数，发起 Ajax 数据请求
    itheima({
        method: '请求类型',
        url: '请求地址',
        data: { /* 请求参数对象 */ },
        success: function(res) { // 成功的回调函数
            console.log(res)     // 打印数据
        }
    })
</script>
//2 定义options参数选项
```

```
//3 处理data参数
function resolveData(data) {
  var arr = []
  for (var k in data) {
    arr.push(k + '=' + data[k])
  }
  return arr.join('&')
}
```

```
//4 定义itheima函数
function itheima(options) {
  var xhr = new XMLHttpRequest()
  // 拼接查询字符串
  var qs = resolveData(options.data)

  // 监听请求状态改变的事件
  xhr.onreadystatechange = function() {
    if (xhr.readyState === 4 && xhr.status === 200) {
      var result = JSON.parse(xhr.responseText)
      options.success(result)
    }
  }
}
```

```
//5 判断请求的类型
if (options.method.toUpperCase() === 'GET') {
    // 发起 GET 请求
    xhr.open(options.method, options.url + '?' + qs)
    xhr.send()
  } else if (options.method.toUpperCase() === 'POST') {
    // 发起 POST 请求
    xhr.open(options.method, options.url)
    xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
    xhr.send(qs)
  }
```
### Level2中提供的新特性
> 1.可以设置 HTTP 请求的时限
2.可以使用 FormData 对象管理表单数据
3.可以上传文件
4.可以获得数据传输的进度信息

## jQuery中实现文件上传与loading效果
### 文件上传
> 1.定义 UI 结构
2.验证是否选择了文件
3.向 FormData 中追加文件
4.使用 xhr 发起上传文件的请求
5.监听 onreadystatechange 事件

### loading效果
1. ajaxStart(callback)——Ajax 请求开始时
2. ajaxStop(callback)——Ajax 请求结束时
## 使用axios发起Ajax请求
Axios 是专注于网络数据请求的库，比XMLHttpRequest更简单易用，比 jQuery轻量化
### axios发起GET请求
```
axios.get('url', { params: { /*参数*/ } }).then(callback)
```
### axios发起POST请求
```
axios.post('url', { /*参数*/ }).then(callback)
```
### 直接使用axios发起请求
#### 直接使用axios发起GET请求
```
 axios({
     method: 'GET',
     url: 'http://www.liulongbin.top:3006/api/get',
     params: { // GET 参数要通过 params 属性提供
         name: 'zs',
         age: 20
     }
 }).then(function(res) {
     console.log(res.data)
 })
 ```
#### 直接使用axios发起POST请求
```
 axios({
     method: 'POST',
     url: 'http://www.liulongbin.top:3006/api/post',
     data: { // POST 数据要通过 data 属性提供
         bookname: '程序员的自我修养',
         price: 666
     }
 }).then(function(res) {
     console.log(res.data)
 })
 ```