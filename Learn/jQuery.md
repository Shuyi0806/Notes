# jQuery(为事件处理特别设计)
## jQuery基本语法：$(selector).action()
选择器允许您对 HTML (DOM）元素组或单个元素（DOM 节点）进行操作。
## jQuery选择器
### 1.jQuery 元素选择器:jQuery 使用 CSS 选择器来选取 HTML 元素。
  $("p") 选取 <p> 元素。
### 2.jQuery 属性选择器:jQuery 使用 XPath 表达式来选择带有给定属性的元素。
  $("[href='#']") 选取所有带有 href 值等于 "#" 的元素。
  $("[href$='.jpg']") 选取所有 href 值以 ".jpg" 结尾的元素。
### 3.jQuery CSS 选择器:jQuery CSS 选择器可用于改变 HTML 元素的 CSS 属性。 
  $("p").css("background-color","red");

## jQuery 事件
### 原则 
#### 把所有 jQuery 代码置于事件处理函数中
#### 把所有事件处理函数置于文档就绪事件处理器中
#### 把 jQuery 代码置于单独的 .js 文件中
#### 如果存在名称冲突，则重命名 jQuery 库
事件处理程序=事件处理方法+事件处理函数
ready和事件方法括号后面要加分号
### jQuery 事件函数（jQuery 中的核心函数）
```
<html>
<head>
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript">
$(document).ready(function(){//文档就绪事件处理器
  $("button").click(function(){//事件处理函数
    $("p").hide();
  });
});
</script>
</head>

<!-- 格式
$(document).ready(function(){
    $(元素).事件方法(function(｛

    ｝);
}); -->


<body>
<h2>This is a heading</h2>
<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
<button>Click me</button>
</body>

</html>
```
## jQuery AJAX 方法
通过 jQuery AJAX 方法，您能够使用 HTTP Get 和 HTTP Post 从远程服务器上请求文本、HTML、XML 或 JSON - 同时您能够把这些外部数据直接载入网页的被选元素中。**只需要一行简单的代码，就可以实现 AJAX 功能。**
### 加载——load() 方法
```
$(selector).load(URL,data,callback);
```
### $.get() 方法
```
//通过 HTTP GET 请求从服务器上请求数据。
$.get(URL,callback);
```
### $.post() 方法
```
//通过 HTTP POST 请求从服务器上请求数据。
$.post(URL,data,callback);//可选的 data 参数规定连同请求发送的数据
```