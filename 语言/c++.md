# c++知识点

## 信息的表示和存储

* 八进制  以0开头
* 十六进制 以0x开头

* 存储单位

  bit byte

  1 byte = 8 bit

  1KB = 1024B 

  1MB = 1024K

  1GB = 1024M

* 反码

  符号不变，全部取反

* 补码

  正数不变，负数反码加一

* 溢出

  两个负数之和，相加溢出

* ~~定点方案~~ 

  ~~早期有过，但因为无法表示较大较小的数。所以惨遭淘汰~~

* 浮点方案

​		csapp里有

## C++概述

* 从c语言发展而来

* 完全兼容C，支持面向对象以及面向过程编程的做法

>    问世程序
>
> ```c++
> #include<iostream>
> using namespace std
> int main(){
> 	cout<< "Hello"<<endl;//"<<"插入运算符
>     return 0;
> }
> ```
>
> 

* 命名空间
* **不能以数字字符开头**
* string类，c++用来提供类似于c的字符数组的容器

## c++简单语法

* 初始化

  C++语言中提供了多种初始化方式；

​				int a = 0;

​				int a(0);

​				int a = {0};

​				int a{0};

其中使用大括号的初始化方式称为列表初始化，列表初始化时不允许信息的丢失。例如用double值初始化int变量，就会造成数据丢失。

### 运算

* 基本运算符

  \+ 加  \-减   \* 乘   /除   % 取余 ++自增 --自减（前置和后置不同）

* 复合的赋值运算符	

  

* 逗号运算和逗号表达式

  表达式1，表达式2，链接两个表达式，并且以表达式二为值

* 关系表达式

  等于 不等于的表达式优先级低 ==      != 

* 逻辑

  ！ && || 

  优先级依次降低，||，&&有短路机制

* 条件表达式

  ?  表达式1:表达式2
  
* 按位与或非

  |将某些特定位制1，&将某些特定位取出

* 异或^

  翻转指定位，00001111

* ~按位取反

* \>> <<

  右移，左移

* 运算优先级

  ![image-20220415040634615](/Users/hadesmercy/Desktop/note/c++.assets/image-20220415040634615.png)

### 数据类型

* 显式类型转换

  const_cast、dynamic_cast、reinterpret_cast、static_cast

  int(z)

  (int)z

  Static_cast\<int>(z)

#### 1.整数

#### 2.实数

#### 3.字符

#### 4.布尔类型

#### 5.自定义

### I/O流

* 标准输入和输出流

  cin cout

* ![image-20220415150358217](/Users/hadesmercy/Desktop/note/c++.assets/image-20220415150358217.png)

### 选择结构

* if
* switch

### 自定义类型

* 类型别名

  ```c++
   typedef  已有类型名  新类型名表
       typedef double Area, Volume;
  	 typedef int Natural;
  	 Natural i1,i2;
  	 Area a;
  	 Volume v;
   using  新类型名 = 已有类型名;
  	 using Area = double;
  	 using Volume = double;
  ```

* 枚举类型（不限定作用域）

  ```c++
  enum Weekday {SUN, MON, TUE, WED, THU, FRI, SAT};
  ```

* auto 自动推断

* decltype

  与某一个表达式类型相同，但不使用初始化变量

  ```c++
  例如：decltype(i) j = 2;
  j 以2作为初始值，类型与i一致
  ```

## c++函数

### 函数定义











 

