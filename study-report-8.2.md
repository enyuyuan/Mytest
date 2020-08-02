># JS环节
>## 事件基本概念及事件注册

**事件包含了四大部分：**  
1. 事件源：产生事件的地方  
2. 事件的类型：比方说点击事件、键盘的事件等等有很多  
3. 事件的对象：记录好信息  
4. 事件的处理程序：事先设定好的方法或者函数  

当产生一个事件后，这个事件会主动的去调用一个设定好的方法或者函数，是通过注册来实现的。  
注册：把以后会发生的事情，先提前报备一下。  
**有两种方式来实现注册：**  
***1.通过html的属性，来实现事件的调用***
    属性名：on+事件的名字   eg：onclick  
    属性值：方法  
        ① 直接在html设定  
        ② 通过js的元素对象来设定
```  
①  
<div id="div1" onclick="add()">div1</div>  
var num = 0;  
function add(){  
    console.log("点击："+ ++num);
}
②  
<div id="div1">div1</div>
var div1 = document.getElementById("div1");
div1.onclick = add;
div1.onclick = null;//删除事件
```  
***2.通过系统提供的方法***
这个方法需要传三个参数：   
`div1.addEventListener(事件类型即事件名例如click，方法函数例如add，事件的处理方式（冒泡或捕获，默认是冒泡，这个值是可以不填的，默认情况下是布尔值false，false代表的就是冒泡的形式，ture代表的就是捕获的形式）);`  
```  
<div id="div1">div1</div>
var num = 0;
function add(){
    console.log("addEventener  点击："+ ++num);
}

var div1 = document.getElementById("div1");
div1.addEventListener("click",add);
```  
***方法2的优势：可以在一个事件上面绑定多个方法，而方法1只能为一个事件绑定一个方法***  
eg：  
```
var num = 0;
function add(){
    console.log("addEventener  点击："+ ++num);
}

var num2 = 0;
function add2(){
    console.log("addEventener2  点击："+ num2--);
}

var div1 = document.getElementById("div1");
//添加事件：
div1.addEventListener("click",add);
div1.addEventListener("click",add2);

//删除事件：
div1.removeEventListener("click",add);
div1.removeEventListener("click",add2);
```  
&emsp;
>## 事件函数和事件对象  

事件函数：当事件发生之后所具体执行的操作    
事件对象 event ：提供了事件的详细信息、具体发生事件的元素、鼠标的位置（坐标）、点击的状态、键盘的按键等很多跟当前事件相关的信息    
```  
    <div id="div1">div1</div>
    <input type="text" name="a" id="input1">
    <a href="http:www.baidu.com" target="_blank" id="a1">百度</a>

    var div1 = document.getElementById("div1");
    div1.addEventListener("click",add);

    var input1 = document.getElementById("input1");
    input1.addEventListener("keydown",add);

    var a1 = document.getElementById("a1");
    a1.addEventListener("click",add);

    function add(event){
        // var e = event || window.event;//可以实现和ie8及以上版本浏览器的兼容，不过可有可无
        console.log(event);

        //默认操作
        //取消默认操作
        event.preventDefault();
    }
```  
注：  
事件的信息中：  
screenX: 28, screenY: 120   
clientX: 28, clientY: 17  
screen X Y : 基于屏幕的左上角  
client X Y : 基于浏览器的左上角  
**事件的默认操作**  
事件有很多的默认操作，比如点击一个网址之后会打开一个新的页面等等，但是我们有时候却不需要  
所以我们首先应该取消默认操作：`event.preventDefault();`  
如果我们绑定事件是通过`a1.onclick = add;`  
那么我们取消默认操作的时候可以通过：`return false;`  
注意`return false;`只针对`a1.onclick = add;`这种方式的绑定  
而`event.preventDefault();`对两种绑定方式都受用  
&emsp;
>### 事件的传播  

在默认的情况下，点击页面的一个标签，处在传播路径上的标签都会监听到对应的事件。  
传播路径大概就是指从所点击的标签一直到这个标签的最外层标签.  
**事件流：**对应标签接受到事件的顺序  
可将事件流分为两大阶段：  
***捕获阶段：***从起始点 到 目标点  
***冒泡阶段：***从目标位置 回到 起始点  
head1.addEventListener("click",head1Click,事件的传播 false true);  
false(默认)则说明方法head1Click在冒泡阶段执行  
true则说明head1Click在捕获阶段执行  
```  
<div id="div1"> div1
    <div id="div2">div2</div>
</div>

var div1 = document.getElementById("div1");
var div2 = document.getElementById("div2");
//捕获阶段
div1.addEventListener("click",div1ClickTure,true);
div2.addEventListener("click",div2ClickTure,true);

function div1ClickTure(){
    console.log("捕获阶段 div1 click");
}
function div2ClickTure(){
    console.log("捕获阶段 div2 click");
}

//冒泡阶段
div1.addEventListener("click",div1Click,false);
div2.addEventListener("click",div2Click,false);

function div1Click(){
    console.log("冒泡阶段 div1 click");
}
function div2Click(event){
    //阻止冒泡事件按照正常的事件流去传播的方法：
    // event.stopPropagation();
    console.log("冒泡阶段 div2 click");
}
```  
**冒泡阶段的活用：事件代理:**通过这样一个父级元素可以去控制所有或者说其他的事件  
```  
<ul>
        <li>li1</li>
        <li>li2</li>
        <li>li3</li>
        <li>li4</li>
        <li>li5</li>
</ul>

var ul1 = document.getElementsByTagName("ul")[0];//因为是获取到的是一个数组，我们用数组的第一个元素
ul1.addEventListener("click",ulclick);
function ulclick(event){
    // console.log("ul click");
    //有很多个li,但不管是哪一个li,ul的事件都能被监听到
    console.log(event.target);
    //然后再通过那个event对象里面我们可以获取到究竟是点击了哪一个li,进而来实现我们一整个业务的逻辑
}
```  

