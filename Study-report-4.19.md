># JS环节

>### 知识点：
> 元素 = document.getElementById("myID");    
> 元素.innerHTML = 字符串  <-修改标签里面的内容    
> 页面是需要交互的    
### 做简单交互的三步骤  
1. 获取元素
2. 绑定事件
3. 修改页面元素
利用id获取元素之后要绑定事件
```  
<body>
    <button id="btn">点我点我</button>

    <script>
        //1.获取元素
         var btndoc = document.getElementById("btn");
        //2.绑定点击事件
        // btndoc.onclick = btnonclick;

        // function btnonclick(){
        //     console.log("点击");
        // }
        //也可以直接把匿名函数赋值给事件
        btndoc.onclick = function (){//这个叫匿名事件
            
        //3.修改页面元素
        var mydivdoc = document.getElementById("mydiv");
        mydivdoc.innerHTML += "点击";
        }
    </script>
</body>
```  

> 元素.onclick = 函数名字        <-点击  
> 元素.onmouseover = 函数名字    <-移入  
> 元素.onmouseout = 函数名字     <-移出
```  
        btndoc.onclick = function (){
            var mydivdoc = document.getElementById("mydiv");
            mydivdoc.innerHTML += "点击<br>";
        }

        btndoc.onmouseover = function (){
            var mydivdoc = document.getElementById("mydiv");
            mydivdoc.innerHTML += "鼠标移入<br>";
        }

        btndoc.onmouseout = function (){
            var mydivdoc = document.getElementById("mydiv");
            mydivdoc.innerHTML += "鼠标移出<br>";
        }
```  
JS也有全局变量和局部变量，跟c语言的差不多。  
注：当一个变量既是全局变量又是局部变量的时候，使用的是局部变量  例如：  
```  
        var y = 1;
        function test(){
            //当有局部变量的时候，使用的是局部变量
            var y = 1;
            y++;
            //console.log(y);
        }
        console.log(y);
        test();
        console.log(y);
        test();
        console.log(y);
```  
JavaScript的数据类型和转换  
弱类型：例如：var x;  
强类型：例如：int a;string b;  
原始类型：数字Number  字符串String  布尔值Boolean  undefined  
对象：Object（把原始值进行多重的组合就可以叫做对象）  
对象又分为：系统自带的对象（数组、函数）和自定义对象    
例如：    
```  
var a ={"a0":60, "a1":61, "a2":62}; 
<!-- //字符串代表变量 
//a0相当于属性名，60相当于属性值
//利用a.a1去访问变量 -->
var b ={0:60, 1:61, 2:62};
<!-- //自定义的下标可以是不用排序的
//例如：var b ={5:60, 1:61, 8:62};
//这样可以利用下标来访问元素，跟数组一样 -->
a[0];

<!-- //自定义对象里面的可以放原始类型，也可以是对象 -->
var a;//表明类型是undefined
var b = null;//表明类型是对象，只不过是空的object
```  
***对象类型转换***  
```
    // 例如将字符型"a"转换成数字型，则可以
    var a = "string";
    var b = Number(a);
    //系统一个自带的简便转化方式，利用了参数的调用方式
    //即通过"."来调用
    a.toString();  
```  

># 程序设计与问题求解环节  
排序问题。10000个用户为某种产品打分，评分区间在0分到100分。要求对用户的打分做一个排序，按从大到小的顺序，输出所有用户的评分。因为产品用户群可能急速扩大到上亿的规模，所以希望程序越快越好，另外为了减小企业为IT设备支出的开销，希望程序越小越好。  
```  
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#define N 10000  
#define M 100

void QuickSort(int *arr, int low, int high)
{
    if (low < high)
    {
        int i = low;
        int j = high;
        int k = arr[low];
        while (i < j)
        {
            while(i < j && arr[j] >= k) // 从右向左找第一个小于k的数
            {
                j--;
            }
 
            if(i < j)
            {
                arr[i++] = arr[j];
            }
 
            while(i < j && arr[i] < k) // 从左向右找第一个大于等于k的数
            {
                i++;
            }
 
            if(i < j)
            {
                arr[j--] = arr[i];
            }
        }
 
        arr[i] = k;
 
        // 递归调用
        QuickSort(arr, low, i - 1);     // 排序k左边
        QuickSort(arr, i + 1, high);    // 排序k右边
    }
}

void display(int array[], int maxlen)
{
    int i,count[N];
 
    for(i = 0; i < maxlen; i++)
    {
        printf("%-5d", 100-array[i]);
    }
    printf("\n");
 
    return ;
}

int main()
{
    int i,score[N],count[M];
    int maxlen = N;
    
    srand((unsigned)time(NULL));//srand()给rand()提供种子
    for(i=0; i<N; i++)//用随机数给数组赋值 
    {
        score[i]=rand()%101;//获取100以内的随机数 
    }
    
    QuickSort(score, 0, maxlen-1);  // 将用户输入的不同数据进行快速排序
    
    display(score, maxlen);//按从大到小的顺序，输出所有用户的评分 
    
    for(i=0; i<=N; i++)
    {
        count[score[i]]++;//统计评相同分数的人数 
    }
    for(i=0;i<=M;i++)
    {
        printf("打 %d 分的有\t%d人\n",i,count[i]);
    } 
    
    return 0;
} 
```  

