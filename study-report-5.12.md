># JS环节
## 函数  

注：函数也是一个变量
ps：跟c语言的差不多。函数的语法如下：    
```  
function 名字(0或多个参数){
    //注：这里的形参不用说明变量类型，直接写变量名就好啦
                执行的语句
            }
``` 
js支持函数名的更换  
```  
function solgen(num,x){
                for(var i=1; i<=10; i++){
                    console.log(x + "  " + i + "好好学习，天天向上！");
                }
            }
            var x = 7;
            solgen(10,x);

            // 更换函数名  
            var fname = solgen;
            var x = 12;
            fname(15,x);
            //效果跟上面的是一样的
```  
js函数也可以有返回值，跟c语言的是一样的。  
>## 实现动态参数  
```  
            function add(){
                /*其实，实参是以一个数组(arguments)的形式传给形参的(上面函数的形参x和y可有可无，影响不大)*/
                //就相当于
                // x = arguments[0];
                // y = arguments[1];
                //所以当实参的数目多于形参数目时，
                //只要加一个for循环遍历数组即可。
                var z = 0;
                for(var i = 0; i < arguments.length; i++){
                    z += arguments[i];
                }
                return z;
            }

            var rs = add(1,2,3,4);
            console.log(rs);

            rs = add(3,4);
            console.log(rs);
```  
>作用域  

作用域：可访问变量的集合，包括对象和函数。是跟c语言的划分一样的。  
注：在调用函数之后，可在函数内改变全局变量的值，而c语言不可以，这点是跟c语言不一样的。  
注意一下两段代码的区别：
```  
            function add(){
                var x = 100;  //重新定义变量，为局部变量
                console.log("add():x=" + x);
                
            }

            var x = 1 ;
            add();
            console.log("全局："+x);
```  
```  
            function add(){
                x = 100;   //未重新定义变量，默认为全局变量
                console.log("add():x=" + x);
                
            }

            var x = 1 ;
            add();
            console.log("全局："+x);
```  
> 预解析（即预编译）  
ps：跟c语言的差不多。  
注：函数体内的变量也会被预解析。  
> 闭包  
解决变量的私有化问题。有全局变量的生命周期，但是又属于局部变量。  
eg：
```  
 function add(){
                var counter = 0;//局部变量 -》 实现有全局变量的生命力
                
                //函数定义的另一种方式：用变量的形式  这里的plus是个全局函数
                // var plus = 

                return function(){  //《----
                    counter++;  //全局变量的生命周期  局部变量
                    console.log("count = " + counter);
                };
            }

            var plus = add();  //counter的初始化
            plus();
            plus();
            plus();

            //在函数里面定义一个局部变量，再在函数里面再定义一个函数，
            //来访问这个局部变量，实现了这个局部变量的全局化。
            //即具有全局变量的生命周期，同时它还是个局部变量。
            //counter，plus组成了一个闭包，实现了变量的私有化  
```  
函数的立即执行：即函数声明和执行放在一起.  
eg:  
`  
(add)();  
`  
闭包较为传统、标准的写法：  
```  
            var plus = (function add(){
                var counter = 0;//局部变量 -》 实现有全局变量的生命力
                
                //函数定义的另一种方式：用变量的形式  这里的plus是个全局函数
                // var plus = 

                return function(){  
                    counter++;  //全局变量的生命周期  局部变量
                    console.log("count = " + counter);
                };
            })();
```  





