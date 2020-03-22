># JS命令  

（注：js命令其实就是一些脚本，可以让机器来执行我们的具体命令） 
>### alert() 弹窗  

此命令弹出的弹窗跟页面没关系，只是弹在页面的上方  
alert("弹窗的内容")；  
字符串需要用双引号括起来；若是纯数字可以不加引号，但也可看作是字符串，然后加引号。

>### document.write() 页面里面

此命令是具体的去改变页面的内容即可以把内容写到页面里面  
改变的页面内容的效果是跟放在html里面的效果的一摸一样的。  
字符串还是需要用引号括起来，可以是双引号，也可以是单引号；若是纯数字可以不加引号，但也可看作是字符串，然后加引号。


>### console.log() 控制台

此命令是把内容写到页面的背后即写到页面的控制台  
是提供给编程人员来看的  

>### js变量

用var定义一个变量，然后就可以对变量进行赋值；  
然后可以用document.write(x);来输出x的值；  
但是要是想输出x这个字符串，而不是输出x的值，则将x用引号引起来即可。即document.write("x");  
注：若给变量赋字符串时，字符串是要加上双引号的。  
还可以将ture、false、对象等赋给变量。  
变量其实是一个容器，若只定义了变量，而未给变量赋值，则页面上显示出来的结果为undifined.  
变量和变量之间是可以相互赋值的。就像c语言。  

>### js运算符

js的运算符有：+ — * / %   
除了运算符 / 和c语言的不一样之外（js的 / 求出的是带有小数的。例如 5 / 2 页面出现的会是2.5），其他运算符都跟c语言的作用是一样的。  
注：+ 在js中还有一个功能，那就是可以实现字符串的简单拼接，也可以实现字符串和数 字之间的拼接，因为这时候计算机会把数字转换为字符1  

>### js的if条件判断语句

跟c语言的if条件判断语句一样。注，要判断相等还是要用==.  
可以进行代码的嵌套。  
***三元运算符   ? :***  
js里面也有三元运算符，跟c语言的是一样的。  
***一元运算符***   
**+、- 正号、负号**  正号、负号可以将数字运算符变为数字
**++、--   自增、自减**  
运算顺序：一元 > 二元 > 三元  

>### prompt函数

功能：会在浏览器里面弹出一个窗口（跟alert有一点点像），可以实现人和浏览器，人和代码的一些简单的交互。  

>### 数组

定义一个数组：var 数组名称=["元素1","元素二","元素三",...];  
可通过不同的下标来找到不同的元素    数组名称[0]
获取数组的长度：数组名称.length  

>### 循环

跟c语言的三种循环一样  
在js的循环里面break和continue照样可以用
