# Node.js——运行在服务端的 JavaScript
基于 Chrome JavaScript 运行时建立的一个平台
**一个事件驱动 I/O 服务端 JavaScript 环境**

## Node.js基础知识
### 把代码进行模块化拆分的好处
1.提高了代码的复用性
2.提高了代码的可维护性
3.可以实现按需加载

### Node.js 将模块分为了 3 大类
 1.内置模块
 2.自定义模块
 3.第三方模块(包）



### CommonJS 规定：
1.每个模块内部，module 变量代表当前模块。
2.module 变量是一个对象，它的 exports 属性（即 module.exports）是对外的接口。
3.加载某个模块，其实是加载该模块的 module.exports 属性。require() 方法用于加载模块。
> Node.js 遵循了 CommonJS模块化规范，CommonJS规定了模块的特性和各模块之间如何相互依赖。
> 
### 模块加载机制：
1.优先从缓存中加载
2.内置模块的加载优先级最高
3.加载自定义模块时，必须指定以 ./ 或 ../ 开头的路径标识符。在加载自定义模块时，如果没有指定 ./ 或 ../ 这样的路径标识符，则 node 会把它当作内置模块或第三方模块进行加载。
4.如果传递给 require() 的模块标识符不是一个内置模块，也没有以 ‘./’ 或 ‘../’ 开头，则 Node.js 会从当前模块的父目录开始，尝试从 /node_modules 文件夹中加载第三方模块。如果没有找到对应的第三方模块，则移动到再上一层父目录中，进行加载，直到文件系统的根目录。
5.当把目录作为模块标识符，传递给 require() 进行加载的时候，有三种加载方式：
1）在被加载的目录下查找一个叫做 package.json 的文件，并寻找 main 属性，作为 require() 加载的入口
2）如果目录里没有 package.json 文件，或者 main 入口不存在或无法解析，则 Node.js 将会试图加载目录下的 index.js 文件。
3）如果以上两步都失败了，则 Node.js 会在终端打印错误消息，报告模块的缺失：Error: Cannot find module 'xxx'


### 创建Node.js应用
步骤一、引入 required 模块
步骤二、创建服务器
```
    var http = require('http');
    http.createServer(function (request, response) {
        // 发送 HTTP 头部 
        // HTTP 状态值: 200 : OK
        // 内容类型: text/plain
        response.writeHead(200, {'Content-Type': 'text/plain'});
        // 发送响应数据 "Hello World"
        response.end('Hello World\n');
    }).listen(8888);
    // 终端打印如下信息
    console.log('Server running at http://127.0.0.1:8888/');
```
步骤三、开启服务
```
    node server.js
```
### NPM 使用介绍
> 常见使用场景：
允许用户从NPM服务器下载**别人编写的第三方包**到本地使用。
允许用户从NPM服务器下载并安装**别人编写的命令行程序**到本地使用。
允许用户**将自己编写的包或命令行程序上传**到NPM服务器供别人使用。

使用 npm 命令安装常用的 Node.js web框架模块 express:

    $ npm install express
    
### Node.js REPL(交互式解释器)
类似 Windows 系统的终端或 Unix/Linux shell

可以执行以下任务：
读取 - 读取用户输入，解析输入的 Javascript 数据结构并存储在内存中。
执行 - 执行输入的数据结构
打印 - 输出结果
循环 - 循环操作以上步骤直到用户两次按下 ctrl-c 按钮退出。

### Node.js 回调函数
Node.js 异步编程的直接体现就是回调。
异步编程依托于回调来实现，但不能说使用了回调后程序就异步化了。

回调函数在完成任务后就会被调用，Node 使用了大量的回调函数，Node 所有 API 都支持回调函数。

例如，我们可以一边读取文件，一边执行其他命令，在文件读取完成后，我们将文件内容作为回调函数的参数返回。这样在执行代码时就没有阻塞或等待文件 I/O 操作。这就大大提高了 Node.js 的性能，可以处理大量的并发请求。

回调函数一般作为函数的最后一个参数出现。

### Node.js 事件循环

> Node.js 是**单进程单线程应用程序**，但是因为V8引擎提供的**异步执行回调接口可以处理大量的并**发，所以性能非常高。
Node.js 几乎每一个 API 都是支持回调函数的。
Node.js 基本上所有的事件机制都是用设计模式中观察者模式实现。
Node.js 单线程类似进入一个while(true)的事件循环，直到没有事件观察者退出，每个异步事件都生成一个事件观察者，如果有事件发生就调用该回调函数.

### 事件驱动程序
Node.js 使用事件驱动模型
1.当webserver接收到请求，就把它关闭然后进行处理，然后去服务下一个web请求。

当这个请求完成，它被放回处理队列，当到达队列开头，这个结果被返回给用户。

这个模型非常高效可扩展性非常强，因为 webserver 一直接受请求而不等待任何读写操作。（这也称之为非阻塞式IO或者事件驱动IO）

在事件驱动模型中，会生成一个主循环来监听事件，当检测到事件时触发回调函数。
```
    // 引入 events 模块
    var events = require('events');
    // 创建 eventEmitter 对象
    var eventEmitter = new events.EventEmitter();
     
    // 创建事件处理程序
    var connectHandler = function connected() {
       console.log('连接成功。');
      
       // 触发 data_received 事件 
       eventEmitter.emit('data_received');
    }
     
    // 绑定 connection 事件处理程序
    eventEmitter.on('connection', connectHandler);
     
    // 使用匿名函数绑定 data_received 事件
    eventEmitter.on('data_received', function(){
       console.log('数据接收成功。');
    });
     
    // 触发 connection 事件 
    eventEmitter.emit('connection');
     
    console.log("程序执行完毕。");
```
### Node.js EventEmitter——核心就是事件触发与事件监听器功能的封装
```
    var events = require('events');
    var eventEmitter = new events.EventEmitter();
    // 监听器 #1
    var listener1 = function listener1() {
       console.log('监听器 listener1 执行。');
    }
    // 监听器 #2
    var listener2 = function listener2() {
      console.log('监听器 listener2 执行。');
    }
    // 绑定 connection 事件，处理函数为 listener1 
    eventEmitter.addListener('connection', listener1);
    // 绑定 connection 事件，处理函数为 listener2
    eventEmitter.on('connection', listener2);
    var eventListeners = eventEmitter.listenerCount('connection');
    console.log(eventListeners + " 个监听器监听连接事件。");
    // 处理 connection 事件 
    eventEmitter.emit('connection');
    // 移除监绑定的 listener1 函数
    eventEmitter.removeListener('connection', listener1);
    console.log("listener1 不再受监听。");
    // 触发连接事件
    eventEmitter.emit('connection');
    eventListeners = eventEmitter.listenerCount('connection');
    console.log(eventListeners + " 个监听器监听连接事件。");
    console.log("程序执行完毕。");
``` 
    $ node main.js
    2 个监听器监听连接事件。
    监听器 listener1 执行。
    监听器 listener2 执行。
    listener1 不再受监听。
    监听器 listener2 执行。
    1 个监听器监听连接事件。
    程序执行完毕。

我们一般要为会触发 error事件的对象设置监听器，避免遇到错误后整个程序崩溃。
大多数时候我们不会直接使用 EventEmitter，而是在对象中继承它。包括 fs、net、 http 在内的，只要是支持事件响应的核心模块都是 EventEmitter 的子类。

## Node.js内置API模块

### fs文件系统模块
#### 读取指定文件fs.readFile()
```
const fs = require('fs')

// 2. 调用 fs.readFile() 方法读取文件
//    参数1：读取文件的存放路径
//    参数2：读取文件时候采用的编码格式，一般默认指定 utf8
//    参数3：回调函数，拿到读取失败和成功的结果  err  dataStr
fs.readFile('./files/11.txt', 'utf8', function(err, dataStr) {
  // 2.1 打印失败的结果
  // 如果读取成功，则 err 的值为 null
  // 如果读取失败，则 err 的值为 错误对象，dataStr 的值为 undefined
  console.log(err)
  console.log('-------')
  // 2.2 打印成功的结果
  console.log(dataStr)
})
```
#### 写入指定文件fs.writeFile()
```
// 1. 导入 fs 文件系统模块
const fs = require('fs')

// 2. 调用 fs.writeFile() 方法，写入文件的内容
//    参数1：表示文件的存放路径
//    参数2：表示要写入的内容
//    参数3：回调函数
fs.writeFile('./files/3.txt', 'ok123', function(err) {
  // 2.1 如果文件写入成功，则 err 的值等于 null
  // 2.2 如果文件写入失败，则 err 的值等于一个 错误对象
  // console.log(err)

  if (err) {
    return console.log('文件写入失败！' + err.message)
  }
  console.log('文件写入成功！')
})
```
### path路径模块
#### 把多个路径片段拼接为完整的路径字符串path.join() 
#### 从路径字符串中，将文件名解析出来path.basename()
#### 获取路径中的扩展名部分path.extname()

### http模块
#### 创建 Web 服务器实例 http.createServer() 
```
// 1. 导入 http 模块
const http = require('http')
// 2. 创建 web 服务器实例
const server = http.createServer()
// 3. 为服务器实例绑定 request 事件，监听客户端的请求
server.on('request', function (req, res) {
  console.log('Someone visit our web server.')
})
// 4. 启动服务器
server.listen(8080, function () {  
  console.log('server running at http://127.0.0.1:8080')
})
```

## 用户自定义模块

## 第三方模块（包）
> 包是基于内置模块封装出来的，提供了更高级、更方便的 API，极大的提高了开发效率,类似于 jQuery 和 浏览器内置 API 之间的关系
>  从 https://www.npmjs.com/ 网站上搜索自己所需要的包
 从 https://registry.npmjs.org/  服务器上下载自己需要的包
Node Package Manager（简称 npm 包管理工具）

### 在项目中安装包的命令 npm install 包的完整名称 包的完整名称
### 安装指定版本的包 npm i 包的完整名称@版本号
### 在项目开发中，一定要把 node_modules 文件夹，添加到 .gitignore 忽略文件中。
### 下载已剔除node_modules的项目， 一次性安装所有的包 npm i 包名 包名 ...
### 卸载包npm uninstall 具体的包名
### 把这些包记录到 devDependencies 节点中 npm i 包名 -D
### 切换 npm 的下包镜像源
#### 查看当前的下包镜像源npm config get registry
#### 将包的镜像源切换为淘宝镜像源 npm config set registry=https://registry.npm.taobao.org/
#### 检查镜像源是否下载成功 npm config get registry
### nrm
#### 将nrm安装为全局可用的工具 npm i nrm -g
#### 查看所有镜像源 nrm ls
#### nrm use taobao
### 包的分类
#### 项目包
##### 开发依赖包devDependencies
##### 核心依赖包dependencies
#### 全局包(工具性质的包)
##### 安装 npm i 包名 -g
##### 卸载 npm uninstall 包名 -g
#### 规范的包结构
1.包必须以单独的目录而存在
2.包的顶级目录下要必须包含 package.json 这个包管理配置文件
3.package.json 中必须包含 name，version，main 这三个属性，分别代表包的名字、版本号、包的入口。

## Express
Express 的本质：就是一个 npm 上的第三方包，提供了快速创建 Web 服务器的便捷方法。是基于内置的 http 模块进一步封装出来的
### 安装npm i express@4.17.1
创建基本的web服务器
```
// 1. 导入 express
const express = require('express')
// 2. 创建 web 服务器
const app = express()

// 4. 监听客户端的 GET 和 POST 请求，并向客户端响应具体的内容
app.get('/user', (req, res) => {
  // 调用 express 提供的 res.send() 方法，向客户端响应一个 JSON 对象
  res.send({ name: 'zs', age: 20, gender: '男' })
})
app.post('/user', (req, res) => {
  // 调用 express 提供的 res.send() 方法，向客户端响应一个 文本字符串
  res.send('请求成功')
})
app.get('/', (req, res) => {
  // 通过 req.query 可以获取到客户端发送过来的 查询参数
  // 注意：默认情况下，req.query 是一个空对象
  console.log(req.query)
  res.send(req.query)
})
// 注意：这里的 :id 是一个动态的参数
app.get('/user/:ids/:username', (req, res) => {
  // req.params 是动态匹配到的 URL 参数，默认也是一个空对象
  console.log(req.params)
  res.send(req.params)
})

// 3. 启动 web 服务器
app.listen(80, () => {
  console.log('express server running at http://127.0.0.1')
})
```
### 托管多个静态资源目录,请多次调用 express.static() 函数(会根据目录的添加顺序查找所需的文件)
### 挂载路径前缀app.use('/public',express.static('public'))
### nodemon-监听项目文件的变动，会自动帮我们重启项目，极大方便了开发和调试
### express路由——客户端的请求与服务器处理函数之间的映射关系
#### 3部分组成：请求的类型、请求的 URL 地址、处理函数
#### 格式：p.METHOD(PATH,HANLER)
#### 注意：1.按照定义的先后顺序进行匹配 2.请求类型和请求的URL同时匹配成功，才会调用对应的处理函数
#### 模块化路由
```
// 创建路由模块
// 1. 导入 express
const express = require('express')
// 2. 创建路由对象
const router = express.Router()

// 3. 挂载具体的路由
router.get('/user/list', (req, res) => {
  res.send('Get user list.')
})
router.post('/user/add', (req, res) => {
  res.send('Add new user.')
})

// 4. 向外导出路由对象
module.exports = router
```

```
//注册路由模块
const express = require('express')
const app = express()
// app.use('/files', express.static('./files'))

// 1. 导入路由模块
const router = require('./03.router')
// 2. 注册路由模块,并添加统一的访问前缀 /api
app.use('/api', router)

// 注意： app.use() 函数的作用，就是来注册全局中间件

app.listen(80, () => {
  console.log('http://127.0.0.1')
})
```
### express中间件
#### 本质：一个 function 处理函数
#### next 函数：表示把流转关系转交给下一个中间件或路由
#### app.use()：定义多个全局中间件,如不使用 app.use() 则是局部生效的中间件
#### 注意事项：一定要在路由之前注册中间件
1.客户端发送过来的请求，可以连续调用多个中间件进行处理
2.执行完中间件的业务代码之后，不要忘记调用 next() 函数
3.为了防止代码逻辑混乱，调用 next() 函数后不要再写额外的代码
4.连续调用多个中间件时，多个中间件之间，共享 req 和 res 对象
#### 中间件的分类
##### 应用级别的中间件： app.use() 或 app.get() 或 app.post() ，绑定到 app 实例上的中间件
##### 路由级别的中间件：express.Router() ，绑定到 router 实例上
##### 错误级别的中间件：专门用来捕获整个项目中发生的异常错误
###### 格式：错误级别中间件的 function 处理函数中，必须有 4 个形参，形参顺序从前到后，分别是 (err, req, res, next)。
###### 注意：必须注册在所有路由之后
##### Express 内置的中间件：
###### express.static 快速托管静态资源的内置中间件，例如： HTML 文件、图片、CSS 样式等（无兼容性）
###### express.json 解析 JSON 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）
###### express.urlencoded 解析 URL-encoded 格式的请求体数据（有兼容性，仅在 4.16.0+ 版本中可用）
##### 第三方的中间件：body-parser

### 使用express写接口
#### 创建基本的服务器
#### 创建 API 路由模块
#### 编写 GET 接口
#### 编写 POST 接口
#### 解决接口跨域问题的方案
##### CORS（主流，推荐）——（Cross-Origin Resource Sharing，跨域资源共享）由一系列 HTTP 响应头组成，这些 HTTP 响应头决定浏览器是否阻止前端 JS 代码跨域获取资源
##### JSONP(只支持GET请求)

## 前后端的身份认证

### web开发模式
#### 服务器端渲染
##### 服务器发送给客户端的 HTML 页面，是在服务器通过字符串的拼接，动态生成的
##### 优点： 前端耗时少。 有利于SEO。 缺点：占用服务器端资源。不利于前后端分离，开发效率低。
#### 前后端分离
##### 后端只负责提供 API 接口，前端使用 Ajax 调用接口
##### 优点：开发体验好。用户体验好。减轻了服务器端的渲染压力。缺点：不利于 SEO

### 身份认证
#### 服务端渲染推荐使用 Session 认证机制(前端请求后端接口不存在跨域问题)
HTTP 协议的无状态性
突破 HTTP 无状态的限制：Cookie——存储在用户浏览器中的一段不超过 4 KB 的字符串
Cookie的几大特性：自动发送 域名独立 过期时限 4KB 限制
Cookie 不具有安全性，Session 认证机制安全性高
##### 原理：![Session 认证机制](../../Code/node.js/Session.png)



#### 前后端分离推荐使用 JWT(跨域认证解决方案) 认证机制(前端需要跨域请求后端接口)
##### 原理：用户的信息通过 Token 字符串的形式，保存在客户端浏览器中。服务器通过还原 Token 字符串的形式来认证用户的身份。

![JWT](../../Code/node.js/JWT.png)