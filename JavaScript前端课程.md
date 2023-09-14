# JavaScript前端课程

![image-20230721133351552](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721133351552.png)

行内式js

![image-20230721133655708](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721133655708.png)

![image-20230721133848273](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721133848273.png)

内嵌式

![image-20230721133755013](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721133755013.png)

外部式

![image-20230721133917969](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721133917969.png)



JS的数据类型：JS语法是弱语法，声明时不强调数据类型，在编译时根据等号右边的数据类型来确定变量的类型

括号内为默认值

简单数据类型：Number( 0 )，String( "" )，Boolean(false)，Undefined( undefined )，Null( null ) 

复杂数据类型：Object



isNaN()方法：判断是否为非数字，如果是数字放回false，如果不是数字返回true

Js转义符

![image-20230721141438237](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721141438237.png)



对undefined和null操作的结果

var variable = undefined;

console.log(variable  + 'pink');   	//undefinedpink	

console.log(variable  + 1);				//NaN



var space = null;

console.log(space + 'pink');		//nullpink

console.log(space + 1);				//1



###### typeof() 方法:判断变量类型，注意null的判断

![image-20230721143107654](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721143107654.png)

###### 数据类型转换

转字符串

1.变量.toString() 

2.Strting(变量)

3.变量+"字符串" 隐式转换

转数字

parseInt(string)

parseFloat(string)	 

Number()

隐式转换(- * /)

![image-20230721151548384](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721151548384.png)



###### 浮点数的精度问题

不能直接用浮点数来进行比较是否相等

![image-20230721152743965](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721152743965.png)



###### 前置自增和后置自增运算符

后置：先原值计算，后自加

前置：先自加，后运算

![image-20230721155735923](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721155735923.png)



###### 比较运算符

注意判等和全等

![image-20230721161122703](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721161122703.png)



逻辑中断和逻辑与，逻辑或

逻辑与短路运算：遇到真往后走，直到假或者尽头就返回这个值

![image-20230721161541095](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721161541095.png)

逻辑或短路运算：遇到假往后走，直到真或尽头就返回这个值

![image-20230721161740593](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721161740593.png)



![image-20230721161930051](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721161930051.png)



###### 运算符优先级

![image-20230721162134888](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20230721162134888.png)



###### switch例子

var fruit = prompt('请输入查询的水果');

switch (fruit) {

​	case'苹果': alert('3.5元/斤');

​	break;

​	case'榴莲': alert('35元/斤');

​	break;

​	default: alert('查无此果');

}	

###### switch语句和if else语句的区别

switch用于case值比较确定的情况，if else常用于范围判断

###### switch进行判断后直接执行到程序的条件语句，效率高。if else则是顺序向下执行判断到直到条件合适





#### 全局变量和局部变量

全局变量更加消耗资源，只有在浏览器关闭时才会被销毁，**比较占内存**。

​	当函数内部出现了没有声明的变量，这个变量会变成全局变量

<img src="C:\Users\asus\OneDrive\桌面\笔记\images\image-20230905135124278.png" alt="image-20230905135124278" style="zoom: 50%;" />

局部变量旨在函数内部使用，当代码块运行结束后，就会被销毁，因此更节省内存空间。





#### 作用域链

内部函数访问外部函数的变量，采取的是**链式查找**的方式来决定取哪个值，这种结构被称为作用域链



<img src="C:\Users\asus\OneDrive\桌面\笔记\images\image-20230905135605863.png" alt="image-20230905135605863" style="zoom:50%;" />

<img src="C:\Users\asus\OneDrive\桌面\笔记\images\image-20230905140151058.png" alt="image-20230905140151058" style="zoom: 50%;" />





#### 预解析

js引擎循行分为两步 1.预解析 2.代码执行

（1）预解析引擎会把js里面所有的var和function提升到当前作用域的**最前面**

（2）代码执行，按照代码书写的顺序从上往下执行

2.预解析分为**变量提升**和**函数提升**

（1）变量提升，就是把所有的变量声明提升到当前作用域的最前面，**不提升赋值操作**

（2）函数提升，把所有的函数声明提升到当前作用域的最前面 **不调用函数**

<img src="C:\Users\asus\OneDrive\桌面\笔记\images\image-20230905141624410.png" alt="image-20230905141624410" style="zoom: 50%;" />

以上例子就是变量提升但是不提升赋值的举例



##### 预解析案例，面试题

```js
f1();
console.log(c);
console.log(b);
console.log(a);
function f1(){
    var a=b=c=9;
    console.log(a);
    console.log(b);
    console.log(c);
}
//提升之后为以下代码
function f1(){
	var a;
    a=b=c=9;
    //相当于 var a = 9; b = 9; c = 9;  bc直接赋值，没有var声明，是全局变量
    //集体声明应该是这样： var a = 9, b = 9, c = 9;
    console.log(a);
    console.log(b);
    console.log(c);
}
f1();
console.log(c);
console.log(b);
console.log(a);

输出
9
9
9
9
9
bao'c
```

