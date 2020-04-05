># JS环节  

>## 函数

js里面函数的声明和c语言差不多，但是函数的执行却不同。在c语言中，函数的执行是通过函数的调用，而在js里面只需直接引用就好。js的函数与函数之间也可以相互调用，但是要一层一层的去调用。  
注意：函数声明是会被覆盖掉的。  
```  
    <script>
        //函数的声明
        function apple() {
            document.write("洗苹果" + "<br>");
            for (var i = 0; i < 10; i++) {
                document.write("去皮" + (i + 1) + "<br>");
            }
            document.write("切小块"+"<br>");
            document.write("插上牙签"+"<br>");
        }
        //函数的执行
        apple();
        apple();
    </script>  
```  
>## 函数的参数

#### 形参   函数的变量声明  
#### 实参   函数的变量赋值  
```  
//形式参数   形参会接受实参的值
 function fruit(name) {
            /*var name; 注意上面形参的声明和c语言的不太一样，js的声明可以忽略类型*/
            document.write("洗" +name+ "<br>");
            for (var i = 0; i < 10; i++) {
                document.write("去皮" + (i + 1) + "<br>");
            }
            document.write("切小块"+"<br>");
            document.write("插上牙签"+"<br>");
        }
        
        //实际的参数
        fruit("苹果");
        fruit("梨");  
```  
js设置默认值有两种方法：  
* name = name || apple  
（此处的意思为：要是已赋值的话就等于水果名，若没有赋值即水果名为undefined的话则为苹果）  
* 直接在形参那里设置默认值：  
`  
function fruit(name="apple",time=3,size="小块")  
`  
（推荐使用第二种）  

>## 函数的返回值

js语句的返回值也是用return来返回的，不过需要注意一下的就是return和break的区别，例如下面这段代码：  
```  
function fruit(name="apple",time=3,size="小块") {
            var str = name;
            return str;
            document.write("洗" +name+ "<br>");
            for (var i = 0; i < time; i++) {
                document.write("去皮" + (i + 1) + "<br>");
            }
            document.write("切"+size+"块"+"<br>");
            document.write("插上牙签"+"<br>");
            str = "一碟" + size + "的" + str;
            return str;
        }
```  
return代表着函数运行完了，这时候返回的str的值就是name，不会运行下面的代码了。通过这个特性，可以对代码进行改进：  
```  
function fruit(name="apple",time=3,size="小块") {
            document.write("洗" +name+ "<br>");
            var str = name;
            if(size == "不切"){
                return str;
            }
            for (var i = 0; i < time; i++) {
                document.write("去皮" + (i + 1) + "<br>");
            }
            document.write("切"+size+"块"+"<br>");
            document.write("插上牙签"+"<br>");
            str = "一碟" + size + "的" + str;
            return str;
        }
```  
注：要是没有写返回值的话，系统会默认返回undefined.  

># 程序设计与问题求解环节  

## 编程循环-穷举法  
五位跳水高手将参加十米高台跳水决赛，有好事者让五个人据实力预测比赛结果。 A选手说：B第二，我第三；B选手说：我第二，E第四；C选手说：我第一，D第二；D选手说：C最后，我第三； E选手说：我第四，A第一; 决赛成绩公布之后，每位选手的预测都只说对了一半，即一对一错，请编程解出比赛的实际名次。
```  
#include <stdio.h>
#include <stdlib.h>

int main()
{
	int a=1,b=0,c=0,d=0,e=0;
	for( a=1; a<=5; a++ )
	{
		for( b=1; b<=5; b++ )
		{
			for( c=1; c<=5; c++ )
			{
				for( d=1; d<=5; d++ )
				{
					for( e=1; e<=5; e++ )
					{
						if(    /*因为每位选手所说的两个答案只有其中一个是对的，所以每位选手的答案都有两种可能性，并且每种可能性的和为1，因为错误时为0，即1+0=1*/                                                   
							(b==2) + (a==3) ==1 &&                                                            
							(b==2) + (e==4) ==1 &&                                                           
							(c==1) + (d==2) ==1 &&                                                                 
							(c==5) + (d==3) ==1 &&                                                               
							(e==4) + (a==1) ==1 )                                                          
							{
								if (120 == a*b*c*d*e)/*因为a,b,c,d,e这五个人无论位次先后不过就是1，2，3，4，5这几个数，所以不同的五个数的乘积是一个定值，依此来确定判断条件*/
								{
								printf("a=%d  b=%d c=%d  d=%d e=%d\n", a, b, c, d, e);                          
								}
							}
					}
				}
			}
		}
	}
	system("pause");
	return 0;
}
```  
输出结果为：a=3, b=1, c=5, d=2, e=4


