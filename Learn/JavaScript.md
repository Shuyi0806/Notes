# javascript基础


## 关键字var
```var num=10;//声明一个变量num,并赋值为10 ```
> *JavaScript 是一种弱类型或者说动态语言。*这意味着不用提前声明变量的类型，在程序运行过程中，类型会被自动确定。


## 变量预解析（变量提升）
> 变量的声明会被提升到当前作用域的最上面，变量的赋值不会提升
```
    console.log(num);
    var num=10;
    //实际运行顺序：
    var num;
    console.log(num);//浏览器显示为undefined
    num=10;
```
## 函数预解析（函数提升）
> 函数的声明会被提升到当前作用域的最上面，但是不会调用函数。
```
fun()；
var fun= function(){
    console.log(22);//not is defind
}
//实际运行顺序：
var fun;
fun();
fun=function(){
    onsole.log(22);
}
```


## javascript的输出方式
```
    alert("我是弹出框");
    document.write("我是输出到页面");
    console.log("在控制台输出");
```
## javascript数据类型
- 简单类型：
number(数值）、string(字符串)、boolean(布尔值)；null、undefined,变量的数据直接存放在变量（栈空间）中,**变量在栈空间里的值复制了一份给形参，那么在方法内部对形参做任何修改，都不会影响到的外部变量**
- 复杂/引用类型：
通过 new 关键字创建的对象（系统对象、自定义对象），如 Object、Array、Date等,变量（栈空间）里存放的是地址，真正的对象实例存放在堆空间中,**变量在栈空间里保存的堆地址复制给了形参,操作的是同一个对象**
```
    var timer=null;
    var user{
    age:18;
    name;"wen";
    hunyin:false ;
    }
```
## typeof运算符:判断基本数据类型
```
    console.log(typeof timer);//object 返回空对象
    console.log(typeof age);//number
    console.log(typeof name);//string
    console.log(typeof hunyin);//boolean
```
null一般代表对象为“没有”，undefind一般代表数值为“没有”

## 算术运算符（+ - * / % ++ --）
> +号是拼接字符，——号隐式转换数字
```
    var num=3;
    console.log(++num3);//4
    console.log(--num3);//2

    //++a先加再赋值
    var a=10;
    ++a;// ++a 11   a 11 
    var b= ++a + 2;// ++a 12   a 12
    console.log(b);//14
    //c++先赋值再加
    var c=10;
    c++;// c++ 11   c 11
    var d= c++ + 2;// c++ 11  c 12
    console.log(d);//14

    var e=10;
    var b= e++ + ++e;//1.e++ 10  e 11  2. ++e 12  e 12
    console.log(b);//22
```
自增和自减有两种写法 ++num  num++
++在前，先自增再运算或赋值  ++在后，先运算或赋值再自增
```
    var num4=10;
    console.log(++num4);//11,先自增再打印
    console.log(num4++);//10，先打印再自增
```


## 赋值运算符（= += -= *= /= %=
```
    var x=10;
    var y=10;
    console.log(x+=y);//x=x+y=20
```


## 比较运算符（> < >= <= ==相等 ===严格相等 != !==严格不相等)
严格相等：数值本身是否相等，类型本身是否相等

## 布尔运算符：布尔值取反，非布尔值取反
非布尔值取反：以下6个值(undefinded\null\false\0\NaN\空字符串(‘’)）取反后为true,其他为false
且运算符（&&）
或运算符（||）

if...else:if总是找离他最近的else

三目运算符可赋值给一个变量
```
var result = num % 2 === 0 ? "偶数" :"奇数";
console.log(result);
```
字符串和数字相加：会显示一个字符串的格式"i=" + i => i=3

```
    //打印九九乘法表
    sum=0;
    for(i=1;i<=9;i++){
        document.write("</br>")
        for(j=1,j<=i,j++){
            sum=i*j;
            document.write(i + "*" + j + '=' + sum + " ");
        }
    }
```

> 双引号不能嵌套双引号，单引号中嵌套单引号
要输出带双引号的文本需要再引号前面加转义字符\
字符串默认一行显示，如要换行需要转义, 使用反斜杠\



## 字符串方法
1.返回字符串中的第n个字符：charAt(n)
2.字符串长度：str.length
3.连接字符串，返回新的字符串：concat( ，，，),可直接使用+连接字符
  区别：concat不管什么类型直接合成字符串，+是遇到数字和数字类型直接做运算，遇到字符串和字符串相连接
4.substring （ ，） 截取字符串，返回一个新的字符串，
  结束位置不包含该位置，第二个参数一定要大于第一个参数，参数如果是负数则自动转为0
5.substr(m,n) m是开始位置 n是长度
  - 第一个参数是负数，则倒着数取
  - 第二个参数是负数，则自动转成0，返回空字符串
6.indexOf(‘字符串’，开始位置):用于确定一个字符串第一次在另一个字符串中出现的位置
 - 存在则返回数字下标，不存在则返回-1
7.trim():去除字符串两端的空格、制表符（\t、\v）、换行符（\n）、回车符（\r），返回一个新字符串
  ES6：trimStart():单独去除头部空格  trimEnd():单独去除尾部空格
8.split():按给定规则切割字符串，放到数组中
  若分割规则为空字符串，则返回数组的成员是原字符串的每个字符
  若省略参数，则返回原字符串
  可接受第二个参数，返回数组的最大成员数
> 由于字符串的不可变，所以不要大量拼接字符串，字符串所有方法都不会修改字符串本身，操作完成会返回一个新的字符串。
## 数组

 1. 除定义时赋值，还可以定义后赋值
 2. 任何类型都可以放在数组里
 3. 下标：赋值，读取  数组名.length
 4. 超出数组下标显示undefinded
 5. 遍历数组：for while for...in
 6. Array.isArray():判断是否是数组，返回一个布尔值
 7. push():在数组末端添加一个或多个元素，返回增加新元素后的数组长度
  pop():在数组末端删除一个元素，返回该元素
 8. shift():删除数组第一个元素，返回该元素，可以遍历并清空一个数组
  unshift()：在头部添加一个或多个元素，返回增加新元素后的数组长度
 9. join():以指定参数作为分隔符，将所有数组成员连接为一个字符串返回，若不提供参数，默认以逗号分隔,如果数组成员是undefinded或null或空位，会被转成空字符串
 10. 数组的join配合字符串的split可以实现数组和字符串的相互转换，若split(""),则一个个字符进行切割
 11. concat():多个数组的合并，将新数组添加到原数组后面，返回一个新数组
  也接受其他类型的值作为参数添加到数组尾部
  应用场景：上拉加载，合并数据
```
  [1,2,3].concat(4,5,6)//[1,2,3,4,5,6]
  [1,2,3].concat(4,5,6,[7,8,9])//[1,2,3,4,5,6,7,8,9]
```
 12. reverse():颠倒排序数组元素，返回改变后的数组，原数组会改变 实现字符串的翻转
 13. sort()：排序
```
arr.sort(function(a, b) {
    return b - a;      // 降a序
    // return a - b;   // 升序
});
```
 14. indexOf():返回给定元素在数组中第一次出现的位置，没有则返回-1
   第二个参数是开始搜索的位置



## 函数———一段可以反复调用的代码块
1.函数的声明：
```
    function 函数名(参数){
    函数体；
    }
```

2.函数的调用：

```   函数名();```

3.函数名的提升：可先调用后声明
4.函数体里面return后面不能再加任何代码，因为不会执行
5.对象————一组“键值对”的集合，一种无序的符合数据集合

> a.对象里的数据没有类型限制，可以是函数
    函数名：function(){
      函数体
    }
  b.对象的读取方式：对象名.属性
    对象名.函数名()
  c.链式调用：对象里面的数据是对象
    对象名.对象名.属性

```
//使用字面量创建对象(:)
        var dog={
            name : "name",
            type : "alasijia",
            age : 5,
            color : "棕红色",
            skill: function() {
                console.log("shark");     
            }
        }

//使用new object创建对象(=)
        var obj =new Object();
        obj.uname="zsf";
        obj.ahe=18;
        obj.sex="男";
        obj.sayhi=Function(){
            console.log("hi");
        }
        console.log(obj.uname);
        console.log(obj['sex']);
        obj.sayhi();

//使用构造函数创建对象(=)
//构造函数（类似于类）
function Star(uname,age,sex){
    this.name=uname;
    this.age=age;
    this.sex=sex;
        }
//创建对象（对象实例化）
var ldh=new Star('刘德华',18,'男');//调用函数
返回的是一个对象
console.log(ldh.name)
```

- 使用构造函数创建对象（不用return就可以返回结果）

1.声明语法规范
function 构造函数名（）{
    this.属性 = 值；
    this.方法 = function(){

    }
}
2.调用语法规范
new 构造函数名();//调用函数就创建了一个对象
3.for...in 语句用于对数组或者对象的属性进行循环操作。
```
for (变量 in 对象名字) {
    console.log(k);      // 这里的 k 是属性名
    console.log(obj[k]); // 这里的 obj[k] 是属性值

}
```

> - 普通函数：封装代码
> - 构造函数：封装对象里面一些相同的属性和方法
6.Math对象————js的元素对象，提供各种数学功能

> Math.abs():返回参数值的绝对值
  Math.max():返回最大的值，若为空，则返回-infinity
  Math.min():返回最小的值，若为空，则返回infinity
  Math.floor():向下取整，返回小于参数值的最大整数
  Math.ceil()：向上取整，返回大于参数值的最小整数
  Math.random():返回[0,1)的伪随机数  （最大值-最小值）*随机数=0~最小值之间的随机数+最小值=最小值到最大值之间的随机数


7.Date对象——js的原生时间库，单位为毫秒  
> Date.now():返回当前时间距离零点（格林威治时间1970.01.01 00：00：00）的毫秒数，相当于Unix的时间乘以1000
  Date对象提供一系列get方法
  getTime():返回实例距离零点的毫秒数
  getDate():
  getDay():
  getYear():返回距离1900的年数
  getFullYear():返回四位数的年
  getMonth():月份从0~11，0：1月   11：12月，需要getMonth()+1
  getHours():
  getMillseconds():
  getMinutes:
  getSeconds():

  

# DOM

console.dir()可以打印我们获取的元素对象，更好的查看对象里面的属性和方法。

## document对象——方法——获取元素
  - getElementsByName()//使用率极低
  
1.根据 ID 获取
  - getElementById()//获取带有 ID 的元素对象

2.根据标签名获取
- getElementsByTagName()[]//返回带有指定标签名的对象的集合,如果获取不到元素,则返回为空的伪数组

- element.getElementsByTagName('标签名')//获取某个元素(父元素)内部所有指定标签名的子元素,父元素必须是单个对象(必须指明是哪一个元素对象). 获取的时候不包括父元素自己。

3.通过 HTML5 新增的方法获取
  - getElementsByClassName()[]
  - querySelector()：接受一个CSS选择器作为参数
  - querySelectorAll()[]：返回一个NodeList对象，包含所有匹给定选择器的节点

4.特殊元素获取
- doucumnet.body  // 返回body元素对象
- document.documentElement  // 返回html元素对象 

## document对象——方法——创建元素

-   createElement():创建元素
-   createTextNode():创建元素对应的文本信息
-   appendChild:将内容或者子元素放到容器中
-   createAttribute():创建元素属性
-   setAttributeNode():只能添加属性

 


 
## Element对象——属性

-  Element对象对应网页的HTML元素，每个HTML元素，都会在DOM树上转化成一个Element节点对象
-    Element.id属性返回指定元素的id属性
-    Element.className属性用来读写当前元素节点的class属性，它的值是一个字符串，每个class用空格间隔开
-    Element.clasList
-    add():增加一个class
-    remove():移除一个class
-    contains():检查当前元素是否包含某个class
-    toggle():将某个class移入（不存在时）或移出（存在时）当前元素

1.改变元素内容
-    Element.innerHTML():不设置内容则读取，设置内容则显示内容,包括 html 标签，同时保留空格和换行 **w3c标准**
-    Element.innerText():不设置内容则读取，设置内容则显示内容，去除 html 标签， 同时空格和换行也会去掉 **非标准**
   
2.常用元素的属性操作
-  innerText、innerHTML 改变元素内容
-  src、href
-  id、alt、title
 
3.表单元素的属性操作
type、value、checked、selected、disabled


| querySelectorAll | getElementsByTagName |
|  --------------  |  ------------------- |
|    NodeList      |     HTMLCollection   |
|   克隆，速度慢    |     索引，速度快      |
|       静态        |       动态           |
|   深度优先遍历算法 |   深度优先遍历算法    |

4.元素样式属性操作
- 行内样式操作：element.style
- 类名样式操作：element.className//样式修改较多,会直接更改元素的类名，会覆盖原先的类名,**建议采用“原类名 新类名”的形式**

5.自定义属性的操作
-  获取属性值
element.属性; //获取内置属性值
element.getAttribute('属性'); //主要获得自定义的属性
-  设置属性值
element.属性 = ‘值’  //设置内置属性值。
element.setAttribute('属性', '值'); //主要设置自定义的属性
- 移除属性
element.removeAttribute('属性');


## Element获取元素位置

-  clientHeight:获取元素高度包括padding,不包括border、margin
-    clientWidth:获取元素宽度包括padding,不包括border、margin
-    scrollHeight:元素总高度包括padding,不包括border、margin，包括溢出的不可见内容
-    scrollWidth：:元素总宽度包括padding,不包括border、margin，包括溢出的不可见内容
-    scrollLeft：元素水平滚动条向右滚动的像素数量
-    scrollTop：元素垂直滚动条向右滚动的像素数量
-    offsetHeight（动态获取）：元素的CSS垂直宽度（单位像素），包括元素本身的高度、padding和border
-    offsetWeight（动态获取）：元素的CSS水平宽度（单位像素），包括元素本身的高度、padding和border
-    offsetLeft：到定位父级左边界的间距
-    offsetTop：到定位父级上边界的间距
-    offsetParent:返回定位的父亲
-    parentNode:返回最近一级父亲
> 获取元素大小位置->用offset更合适,  给元素更改值->用style改变
   

## CSS操作

    


1）HTML元素的style属性
使用网页元素节点的setAttribute方法直接操作网页元素的style属性

    var box = document.getElementById("box")
    box.setAttribute("style","width：200px;height:200ox;")

2）元素节点的style属性  

    var box = document.getElementById("box")
    box.style.width=200px; box.style.height=200px;
    
3）cssText属性  

    var box = document.getElementById("box")
    box.style.cssText="width :200px;height:200px;"
    

    

## 事件处理程序
 1）HTML事件处理：缺点：HTML和JS没有分开
 
    <div id="div">
        <button id="btn1" onclick="demo()">按钮</button>
    </div>
    <script>
        function demo(){
            alert("hello html事件处理)；
        }
    </script>
    
 2）DOM0级事件处理：优点：HTML和JS是分离的 缺点：无法同时添加多个事件

    //传统注册方式
    var btn=document.getElementById("btn)
    btn.onclick=function(){
        console.log("点击了");
    }
    var btn=document.getElementById("btn)
    btn.onclick=function(){
        console.log("点击了");
    }
    //传统注册删除事件方式
    btn.onclick=null;


 3）DOM2级事件处理：优点：事件不会被覆盖 缺点：写起来麻烦

    //方法监听注册方式
    var btn=document.getElementById("btn)
    btn.addEventListener("click",function(){
        console.log("点击了");
    })
    //方法监听注册删除事件方式
    var btn=document.getElementById("btn)
    btn.addEventListener("click",fn);
    function fn(){
        alert("22");
        btn.removeEventListener("click",fn);
    }
    btn.removeEventListener("click",function(){
    }

### DOM事件流——事件传播的过程（3个阶段）
JS代码中只能执行不好或冒泡其中一个阶段。
1.**捕获阶段（很少关心）**——逐级向下传播到最具体的元素,addEventListener第三个参数为true document->html->body->father->son,
2.**当前目标阶段**
3.**冒泡阶段（更关注）**——逐级向上传播到最顶层节点（onclick),addEventListener第三个参数为false son->father->body->html->document
注：有些事件没有冒泡：onblur、onfocus、onmouseenter、onmouseleave

### 事件对象
1.写到监听函数的小括号里，当形参来看
2.是事件一系列相关数据的集合，系统自动创建，不需要我们传递参数

## target和this区别
target返回的是**触发事件**的对象，this返回的是**绑定事件**的对象

## 鼠标事件（如果使用addEventListener 不需要加 on）

> onclick:单击事件
    ondbclick:双击事件
    onmousedown:鼠标按下
    onmouseup:鼠标抬起
    onmousemove:鼠标移动
    onmouseenter:鼠标进入
    onmouseleave:鼠标离开
    onmouseover:进入子节点再一次触发
    onmouseout:离开父节点再一次触发
    wheel:滚动鼠标滚轮时

    

## event事件对象——事件发生后，会产生一个事件对象，作为参数传给监听函数

> 1）Event对象属性
    Event.target返回事件当前所在节点
    Event.type返回一个字符串，表示事件类型，只读
 2）Event对象方法
    Event.preventDefault():取消浏览器对当前事件的默认行为
    Event.stopPropagation()：**阻止事件冒泡**阻止事件在DOM中继续传播，防止再触发定义在别的节点上的监听函数，但是不包括在当前节点上的其他的事件监听函数



## 键盘事件（如果使用addEventListener 不需要加 on）

> 1)onkeydown:按下时触发
 2)onkeypress（少用）：按下有值的(数字和字母）键触发，ctrl这样无值的键不会触发，对有值的键，先触发keydown,再触发kepress
 3)onkeyup：松开键盘时触发,获取输入框的值
 4）keycode：能区分大小写，返回不同的ASCII值
 5）三个事件的执行顺序是： keydown --  keypress  --- keyup

 
## 表单事件——在使用表单元素及输入框元素可以监听的一系列事件

> 1）input事件(oninput)：实时输入实时获取
 2）select事件(onselect)：选中内容时触发
 3）change事件(onchange)：不会连续触发，只有回车或者失去焦点时才会触发
 4）reset事件(onreset)：发生在form,而不是表单的成员上
 5）submit事件(onsubmit)：发生在form,而不是表单的成员上  

                                                           


## 事件代理（委托、委派）

> 将子元素交给父元素处理，利用点击子元素会触发父元素这个特性（利用冒泡原理）来通过父元素监听每一个子元素的事件

> 给父元素添加事件，通过子元素触发，同时通过event 对象还获取每个对应所点的标签的行为
> 作用：提高了程序的性能

# BOM
1.BOM 缺乏标准，兼容性较差
2.window 对象是浏览器的顶级对象，JS 访问浏览器窗口的一个接口，还是一个全局变量
3.window下的一个特殊属性 window.name
4.window:document、location、navigation、screen、history

## window 对象的常见事件
### 窗口加载事件
1.window.onload 传统注册事件方式 只能写一次，如果有多个，会以最后一个 window.onload 为准
2.如果使用 addEventListener 则没有限制
```
document.addEventListener('loadd',function(){})//
document.addEventListener('DOMContentLoaded',function(){})//DOM加载完毕就可执行，页面的图片很多,用DOMContentLoaded
```
### 调整窗口大小事件
```
window.onresize = function(){}
window.addEventListener("resize",function(){});
```

## 定时器
### setTimeout(函数，延时时间)
> 如果回调函数是对象的方法，那么setTimeout使得方法内部的this关键字指向全局变量，而不是定义时所在的那个对象

```
function cakback(){
    console.log("爆炸了");
}
setTimeout(callback,3000);
```

cleanrTimeout(timer) 用于取消定时器

### setInterval(函数，延长时间) 
> 用法与setTimeout完全一致，区别在于setInterval指定某个任务每隔一段时间执行一次，也就是无限次执行

cleanerInterval() 用于取消定时器

### this
1. 全局作用域或者普通函数中this指向全局对象window（注意定时器里面的this指向window）
2. 方法调用中谁调用this指向谁
3. 构造函数中this指向构造函数的实例

## JS 执行机制
1. JS 是单线程
### 同步和异步
同步任务——都在主线程上执行，形成一个执行栈
异步任务——通过回调函数实现的，回调函数添加到任务队列（消息队列）中
一般而言，异步任务有以下三种类型:
1、普通事件，如 click、resize 等
2、资源加载，如 load、error 等
3、定时器，包括 setInterval、setTimeout 等
### 执行机制
1. 先执行执行栈中的同步任务。
2. 异步任务（回调函数）放入任务队列中。
3. 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行。
> 由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种机制被称为**事件循环（ event loop）**

## 防抖(debounce)
在某个时间期限内，事件处理函数只执行一次，严格上属于性能优化

### 滚动事件

    window.onscroll=scrollHandle 
	function scrollHandle(){
    	console.log(“页面滚动了”)；
	}

## 节流(throttle)
严格属于性能优化

```
function
```

### 场景

> 1. 搜索框input
2. 页面resize，常见于页面适配，需要对最终呈现出来的页面情况进行don渲染



## 命令行工具
> 常用命令行工具
> 1. CMD
> 2. PowerShell


## 闭包
作用：将局部变量转变成全局变量

 1. 变量的作用域

 > - 函数内部可以直接读取全局变量
 > - 在函数外部无法读取函数内的局部变量
 > - 函数内部声明变量的时候，一定要使用var命令。如果不用的话，你实际上声明了一个全局变量

 2. 从外部读取局部变量
> - 在函数的内部，再定义一个函数

 3. 闭包的概念
> 定义在一个函数内部的函数

 4. 闭包的作用
 > - 可以读取函数内部的变量
 > - 让这些变量的值始终保持在内存中

## Babel转码器

> 可以将ES6转换成ES5

[浏览器支持性查看][1]

[Babel官网][2]


  [1]: https://caniuse.com
  [2]: https://babejs.io
  
### 安装Babel

    npm install --save-dev @babel/core

### 安装Babel转码规则

    npm install --save-dev @babel/preset-env

### 安装Babel命令行转码工具

    npm install --save-dev @babel/cli

### Babel命令行转码
```
# 转码结果输出到标准输出（就是打印出来内部代码）
$ npx babel example.js

# 转码结果写入一个文件
# --out-file 或 -o 参数指定输出文件
$ npx babel example.js --out-file compiled.js
# 或者
$ npx babel example.js -o compiled.js

# 整个目录转码
# --out-dir 或 -d 参数指定输出目录
$ npx babel src --out-dir lib
# 或者
$ npx babel src -d lib

# -s 参数生成source map文件
$ npx babel src -d lib -s
```

## Let命令

> 用来声明变量，用法相当于var,但作用域只在代码块内


>var:函数级的作用域
let:1.块级作用域（花括号级别）
```
for(var i=0;i<10;i++)//每次都是同一个i
for(let i=0;i<10;i++)//每次都是新的i
```
    


>let:2.let不存在变量提升
>let:3.let不存在重复声明

## Const命令

> 1.声明一个只读变量，一旦声明，常量的值就不能改变
>2.一旦声明变量就必须初始化，不能留到以后赋值
>```const names="iwen"```
>3.作用域与let一致，都是块级作用域
>4.也不存在变量提升
>5.不能重复声明

## 对象解构赋值
```
var user={
    name:"iwen",
    age:20
}
const{name,age}=user;
console.log(name,age);
//而不用以下：
console.log(user.name);
console.log(user.age);
```

> 1.可以没有次序，但一定要同名
2.很方便的将现有对象的方法，赋值到某个变量

    const{abs,ceil,floor,random} = Math;
    log(random())
    
3.将一个已经声明的变量用于解构赋值，要小心，建议不用

## 字符串扩展
1.字符串Unicode表示法，允许采用\uxxxx表示一个字符，其中xxxx表示字符的Unicode码点
2.字符串遍历器接口
for...of循环遍历
```
for(let i of 'iwen'){
    console.log(i);
    }
```
3.模板字符串——增强版字符串

> 用反引号（`）标识，可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量
```
let url = "www.itbaizhan.com"
let h1 = "<a href='"+url+"'>itbaizhan</a>"
let h2 = `<a href='${url}'>itbaizhan</a>`
```

## 字符串ES6新增方法

> 1.includes():返回布尔值，表示是否找到了参数字符串
2.startsWith():返回布尔值，表示参数字符串是否在原字符串的头部
3.endsWith():返回布尔值，表示参数字符串是否在原字符串的尾部
都支持第二个参数，表示开始搜索的位置
4.repeat():返回一个新字符串，表示将原字符串重复了n次,n=0则得到一个空字符串
5.padStart(）：将头部补全
padEnd():将尾部补全
```
var h="x"
console.log(h.padStart(5,"ab"));//ababx
```
> 6.trimStart(）：消除头部空格
trimEnd():消除尾部空格
返回新字符串
7.at():接受一个整数作为参数，返回参数指定位置的字符，支持负索引（即倒数位置）
如果超过字符串范围，则返回undefind

## 数组扩展——扩展运算符（spread)

1.扩展运算符是三个点（...），将一个数组转为用逗号分隔的参数序列
```
var arr1 = [10,20,30];
console.log(...arr);//10 20 30
```
2.代替函数apply方法
3.合并数组
```
var arr1 = [10,20,30];
var arr2 = [40,50,60];
console.log([...arr1,...arr2]);//[10 20 30 40 50 60]
```

## 数组扩展——新增方法

 1.Array.from():用于将类数组转换为真正的数组

> 常见三类类数组：（类/伪数组只能使用数组的读取方式和length属性，不能使用数组方法：push）
1.arguments
2.元素集合
3.类似数组的对象

2.Array.of():用于将一组值，转换为数组
而Array(3)是创建数组空间

## 对象的扩展
1.属性名和属性值是同样的变量名称就可以省略

    var name = "iwen"
    var user = {
        name, //而不用name=name
        age:20,
        getName(){ //而不用getName:function()
        console.log(this.name);
        }
    }
    user.getName();//iwen
    
    function getPoint(){
        var x = 10.23;
        var y = 23.34;
        return{x,y}
        //而不用return{
            x:x;
            y:y;
        }
    }
    console.log(getPoint().x,getPoint().y);
2.属性名表达式——允许字面量定义对象时，用表达式作为对象的属性名，即把表达式放在方括号内

    var ib = "itbaizhan"
    var user ={
        [ib]:"web,java,python"
        age :13
    }
    console.log(user);//{itbaizhan:"web,java,python",age :13}
3.对象的扩展运算符

    let z = {a：3，b: 4};
    let n = {...z}//{a：3，b: 4}
    let n = {z}//{z:{...}}
    console.log(n);
    
## 函数的扩展——箭头函数
基本用法：用箭头（=>)定义函数

    
    //第一种
    function fn1(x,y){
        return x+y;
    }
    //第二种：赋值方式声明函数
    var fn2 = function(x,y){
        return x+y;
    }
    //箭头函数
    var fn3 = (x,y) =>x+y
    console.log(fn3(10,20));//30
    
    var fn4 = x => x
    var fn5 =() =>10
    
箭头函数的代码块部分多于一条语句，要用大括号把他们括起来，并用return返回

    var fn6 =function(x,y){
        var z =10;
        return x+y+z;
    }
    
    var fn6 = (x,y) => {
        var z=10;
        return x+y+z;
    }
    
由于大括号被解释成代码块，所以箭头函数直接返回一个对象，必须在对象外面加上大括号，否则会报错

    var add =(x,y) => ({x:10,y:20})

箭头函数的作用是简化回调函数(匿名函数）

    var arr = [10,20,30]
    arr.map(function(element,index){
        console.log(element);//10 20 30
    })
    //改写为：
    arr.map((element,index)=>{
        console.log(element);//10 20 30
    })

> 对普通函数而言，内部this指向函数运行时所在的对象，但是这一点对箭头函数不成立。他没有自己的this对象，内部的this就是定义在上层作用域的this

    var name = "ime";
    //定时器——指向全局变量
    var user = {
        name:"iwen",
        age:20,
        getName(){
            setTimeout(function(){
                console.log(this.name);//ime
        })
      }
    }
    //箭头函数——指向上层作用域的this
    var user = {
        name:"iwen",
        age:20,
        getName(){
            setTimeout(() => {
                console.log(this.name);//iwen
        })
      }
    }
    user.getName();
    
## Set数据结构

> 类似于数组，但是成员唯一，无重复
set本身是一个构造函数，用来生成Set数据结构

    const s = new Set();
    [2，3，4，5，5，2，2].forEach(x => s.add(x));
    for(let i of s){
     console.log(i);// 2 3 4 5
    }
    //add()函数用来向数组中添加数据，不会添加重复值
Set函数可以接受一个数组作为参数，Set也可以用扩展运算符（...)来读取数据
去除数组重复成员
```[...new Set(array)]```
去除字符串重复字符
```[...new Set('ababbc')].join(' ')//abc```
向Set加入值时，不会发生类型转换，5和“5”时不同的值
###size属性——返回Set实例的成员总数

    const items new Set([1,2,3,4,5,5,5]);
    items.size;//5

##Set数据结构方法

> add()：添加方法
delect():删除某个值，返回一个布尔值，表示删除是否
has():返回一个布尔值，表示该值是否为Set的成员
clear():清空所有成员，没有返回值

## Promise对象

> 简单来说就是个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果
从语法上说，promise是一个对象，可以获取异步操作的消息
promise提供统一的api,各种异步操作都可以用同样的方法进行处理
作用：可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数

基本用法
promise对象是一个构造函数，用来生成promise实例

    const promise = new Promise(function(resolve,reject){
    //...some code
    if(异步操作成功）{
        resolve(value);
    }else{
        reject(error);
    }

Promise构造函数接受一个函数作为参数，两个参数分别是resolve和reject,由JavaScript引擎提供
promise实例生成后，可以用then方法分别指定resolved状态和rejected状态的回调函数

    promise.then(function(value){
    //success
    },function(error){
    //failure
    });
    
## JavaScript 严格模式(use strict)

> 它不是一条语句，但是是一个字面量表达式,严格模式下你不能使用未声明的变量。

1.严格模式下你不能使用未声明的变量。
严格模式通过在脚本或函数的头部添加 use strict; 表达式来声明。
2.严格模式的限制
 - 不允许使用未声明的变量，对象也是一个变量
 - 不允许删除变量或对象。
 - 不允许删除函数。
 - 不允许变量重名:
 - 不允许使用八进制:
 - 不允许使用转义字符
 - 不允许对只读属性赋值:
 - 不允许对一个使用get方法读取的属性进行赋值
 - 不允许删除一个不允许删除的属性
 - 变量名不能使用 "eval" 字符串:
 - 变量名不能使用 "arguments" 字符串:
 - 不允许使用以下这种语句:
 - 由于一些安全原因，在作用域 eval() 创建的变量不能被调用：
 - 禁止this关键字指向全局对象。
 - 使用构造函数时，如果忘了加new，this不再指向全局对象，而是报错。
3.保留关键字
 - implements
 - interface
 - let
 - package
 - private
 - protected
 - public
 - static
 - yield
 
## 深浅拷贝
**浅拷贝**的意思就是只复制引用，而未复制真正的值。

**深拷贝**就是对目标的完全拷贝，不像浅拷贝那样只是复制了一层引用，就连值也都复制了。只要进行了深拷贝，它们老死不相往来，谁也不会影响谁。

> 目前实现深拷贝的方法不多，主要是两种：
1.利用 JSON 对象中的 parse 和 stringify
2.利用递归来实现每一层都重新创建对象并赋值


concat和slice 只是对数组的第一层进行深拷贝。
Object.assign() 拷贝的是属性值。假如源对象的属性值是一个指向对象的引用，它也只拷贝那个引用值。
... 展开运算符实现的是对象第一层的深拷贝。后面的只是拷贝的引用值。

> 1.赋值运算符 = 实现的是浅拷贝，只拷贝对象的引用值；
2.JavaScript 中数组和对象自带的拷贝方法（concat、slice、Object.assign()、... 展开运算符）都是“首层浅拷贝”；
3.JSON.stringify 实现的是深拷贝，但是对目标对象有要求，对象中不能有函数；
4.若想真正意义上的深拷贝，请递归。

    function deepClone(source){
        const targetObj = source.constructor === Array ? [] : {}; //              判断复制的目标是数组还是对象
          for(let keys in source){ // 遍历目标
            if(source.hasOwnProperty(keys)){
              if(source[keys] && typeof source[keys] === 'object'){ // 如果值是对象，就递归一下
                targetObj[keys] = source[keys].constructor === Array ? [] : {};
                targetObj[keys] = deepClone(source[keys]);
              }else{ // 如果不是，就直接赋值
                targetObj[keys] = source[keys];
              }
            } 
          }
          return targetObj;
    }
    
## 执行上下文
执行上下文是评估和执行 JavaScript 代码的环境的抽象概念。每当 Javascript 代码在运行的时候，它都是在执行上下文中运行。

    //变量提升
    var foo = function () {
        console.log('foo1');
    }
    foo();  // foo1
    var foo = function () {
        console.log('foo2');
    }
    foo(); // foo2
    

    //函数提升
    function foo() {
        console.log('foo1');
    }
    foo();  // foo2
    function foo() {
        console.log('foo2');
    }
    foo(); // foo2

    
    


> JavaScript 中有三种执行上下文类型。
**全局执行上下文** —这是默认或者说基础的上下文，任何不在函数内部的代码都在全局上下文中。它会执行两件事：创建一个全局的window对象（浏览器的情况下），并且设置this的值等于这个全局对象。**一个程序中只会有一个全局执行上下文**。
**函数执行上下文** —每当一个函数被调用时,都会为该函数创建一个新的上下文。每个函数都有它自己的执行上下文，不过是**在函数被调用时创建的。函数上下文可以有任意多个**。每当一个新的执行上下文被创建，它会按定义的顺序（将在后文讨论）执行一系列步骤。
**Eval 函数执行上下文**—执行在eval函数内部的代码也会有它属于自己的执行上下文，少用，不讨论。

### 执行栈
执行栈，也就是在其它编程语言中所说的“调用栈”，是一种拥有LIFO（后进先出）数据结构的栈，被用来存储代码运行时创建的所有执行上下文。
当 JavaScript 引擎第一次遇到你的脚本时，它会创建一个全局的执行上下文并且压入当前执行栈。每**当引擎遇到一个函数调用**，它**会为该函数创建一个新的执行上下文并压入栈的顶部**。

### 怎么创建执行上下文？
创建执行上下文有两个阶段：1) 创建阶段 和 2) 执行阶段。
#### 创建阶段
**1.this 值的决定，即我们所熟知的 This 绑定。**
在全局执行上下文中，this 的值指向全局对象。(在浏览器中，this引用 Window 对象)。
在函数执行上下文中，this的值取决于该函数是如何被调用的。如果它被一个引用对象调用，那么 this 会被设置成那个对象，否则 this 的值被设置为全局对象或者 undefined（在严格模式下）。
**2.创建词法环境组件。**

在词法环境的内部有**两个组件**：
(1)**环境记录器**是存储变量和函数声明的实际位置。
(2)**外部环境的引用**意味着它可以访问其父级词法环境（作用域）。

词法环境有**两种类型**：
(1)**全局环境**（在全局执行上下文中）是没有外部环境引用的词法环境。全局环境的外部环境引用是 null。它拥有内建的Object/Array/等、在环境记录器内的原型函数（关联全局对象，比如 window 对象）还有任何用户定义的全局变量，并且 this的值指向全局对象。
(2)在**函数环境**中，函数内部用户定义的变量存储在环境记录器中。并且引用的外部环境可能是全局环境，或者任何包含此内部函数的外部函数。

**环境记录器有两种类型**：
(1)**声明式环境记录器**存储变量、函数和参数。
(2)**对象环境记录器**用来定义出现在全局上下文中的变量和函数的关系。
> 简言之，
在全局环境中，环境记录器是对象环境记录器。
在函数环境中，环境记录器是声明式环境记录器。

**3.创建变量环境组件。**
同样是一个词法环境，其环境记录器持有变量声明语句在执行上下文中创建的绑定关系。
词法环境组件和变量环境的一个不同就是前者被用来存储函数声明和变量（let 和 const）绑定，而后者只用来存储 var 变量绑定。

### 变量对象
变量对象是与执行上下文相关的数据作用域，存储了在上下文中定义的变量和函数声明。
#### 全局上下文
全局上下文中的变量对象就是全局对象。
#### 函数上下文
函数上下文用活动对象(activation object,AO)来表示变量对象。只有被激活的变量对象，活动对象上的各种属性才能被访问。
活动对象是在进入函数上下文时刻被创建的，它通过函数的arguments属性初始化。arguments 属性值是 Arguments 对象。
#### 执行过程
执行上下文的代码会分成两个阶段进行处理：分析和执行，我们也可以叫做：
1.进入执行上下文
> 这时候还没有执行代码，变量对象会包括：
1）函数的所有形参 (如果是函数上下文)
由名称和对应值组成的一个变量对象的属性被创建
没有实参，属性值设为 undefined
2）函数声明
由名称和对应值（函数对象(function-object)）组成一个变量对象的属性被创建
如果变量对象已经存在相同名称的属性，则完全替换这个属性
3）变量声明
由名称和对应值（undefined）组成一个变量对象的属性被创建；
如果变量名称跟已经声明的形式参数或函数相同，则变量声明不会干扰已经存在的这类属性

2.代码执行
在代码执行阶段，会顺序执行代码，根据代码，修改变量对象的值

    console.log(foo);
    function foo(){
        console.log("foo");
    }
    var foo = 1;
    //输出foo

> 总结：
1.全局上下文的变量对象初始化是全局对象
2.函数上下文的变量对象初始化只包括 Arguments 对象
3.在进入执行上下文时会给变量对象添加形参、函数声明、变量声明等初始的属性值
4.在代码执行阶段，会再次修改变量对象的属性值

### 作用域链

> 对于每个执行上下文，都有三个重要属性：
变量对象(Variable object，VO)、作用域链(Scope chain)、this
当查找变量的时候，会先从当前上下文的变量对象中查找，如果没有找到，就会从父级(词法层面上的父级)执行上下文的变量对象中查找，一直找到全局上下文的变量对象，也就是全局对象。这样**由多个执行上下文的变量对象构成的链表就叫做作用域链。**
通俗上讲，内部函数访问外部函数的变量，采取的是链式查找的方式来决定取哪个值，这种结构我们称为作用域链（就近原则）




## Git_开源的分布式版本控制系统

> 直接记录快照，重新生成一份文件，类似于备份，Git不再重新存储该文件，而是只保留一个链接指向之前存储的文件，空间换时间，只需要访问本地文件和资源

Git的三个区域：工作区(untracked/unmodified-让工作区的文件都处于“未修改”的状态/modified/staged)，暂存区，Git仓库
Git的三种状态：已修改（modified），已暂存（staged）,已提交（committed）


