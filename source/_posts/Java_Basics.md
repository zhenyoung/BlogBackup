---
title: Java基础语法
date: 2021-02-04 14:24:12
tags: Java
---

此前学习了C语言，思维仍是面向过程的编程思想。现在开始学习Java，转变一下思路。特此写博客记录Java的知识点。关于编程语言中的一些通用的重复性内容就不再赘述，在此文中提及的基础，都是当时学习C语言时候自己埋下的坑，都是自己的血泪！！！

此篇博客未完待续......

<a href="#bottom">到达文章底部</a>

<!--more-->

# 1. 前言

## 1.1 语言的特点

1.面向对象<br>两个基本概念：类、对象；三大特性：封装、继承、多态<br>2.健壮性<br>去除了C/C++中的影响健壮性的指针内存的申请与释放等，提供一个相对安全的内存管理和访问机制<br>垃圾回收机制（但是仍然会出现内存溢出和内存泄露的问题）<br>3.跨平台性<br>一次编译，多次运行（Write once，run anywhere）。原理为：在需要运行Java的应用程序的操作系统上，先安装Java虚拟机即可。由虚拟机来负责Java程序在系统中的运行。


## 1.2 java的两种核心机制

虚拟机机制（Java Virtual Machine）、垃圾回收机制（Garbage Collection）

## 1.3 JDK、JRE、JVM

JDK=JRE + 开发工具集（例如javac编译工具等）；JRE=JVM + JavaSE标准类库

# 2. 基本语法

## 2.1 关键字、保留字、标识符

1.关键字：过多，使用时记忆<br>2.保留字：现有JAVA版本尚未使用名，但是以后版本可能会作为关键字使用，因此命名标识符时需要避免使用这些保留字：const、goto<br>3.标识符：变量名、方法名、类名、接口名、包名等凡是自己可以命名的都叫标识符，命名时JAVA是严格区分大小写的


## 2.2 命名规范

- 包名：所有单词小写"xxyyzz"
- 类名、接口名：每个单词的首字母大写（大驼峰命名）"XxYyZz"
- 变量名、方法名：第一个单词小写，后面的单词每个单词首字母大写（小驼峰命名）"xxYyZz"
- 常量名：所有字母大写，多个单词时用下划线连接"XXYYZZ"

## 2.3 数据类型

### 2.3.1 基本数据类型（primitive type）

1.整型（byte、short、int、long）：整型常量默认为 int 型<br>2.浮点型（float、double）：浮点型常量默认为 double 型，定义 long 和 float 类型初始化及赋值时需要在数值后面加上 "L" 或 “l” 和 “F” 或 “f”，常用 int 和 double 类型。若 long 型不加上后缀，则默认为 int 型，而 float 类型必须加上后缀，否则编译报错<br>3.字符型（char）：与C不同，java的字符型 char可以表示任何一个字符（每个字符占2个字节），而不单单是西文字符，如`char a = '我';`，而`char a = '48'; `是错误的，因为 `'48'`是2个字符，哪怕是`'4空格'`也不行，空格也算一个字符，但是`char a = 48;`是对的，因为没有用单引号括起来时，相当于将 ASCII 码值给ａ，编译时机器会查表将其替换成对应的字符。128 个 ASCII 码字符用8位表示，最高位规定为0，剩下7位表示0~127的 ASCII 码字符。<br>4.布尔型（boolean）

### 2.3.2 引用数据类型（reference type）

class（类）、interface（接口）、array（数组）

### 2.3.3 数据类型转换（不包括boolean）

1.自动类型提升<br>当容量小的数据类型的变量与容量大的数据类型的变量做运算时，结果自动提升为容量大的数据类型。<br>即  byte、char、short → int → long → float → double<br>特别地，当byte、char、short 三种类型的变量做运算时，结果为 int 型<br>2.强制类型转换（自动类型提升的逆运算）

## 2.4 运算符

- 自增自减以及 += 和 -= 不会改变数据类型，如：

```java
short a = 1;
/******************************************************************/
//a = a + 1；
/*此处a+1的结果自动转换成了int型，但是接收的a为short。C中只是警告，但是编译可以通过，自动将结果强制转换成short,而java中则不能通过编译*/
/******************************************************************/
a += 1;
//a++;
//++a;
//自增自减不会修改本身的数据类型，因此是可以在C和java通过编译,且都没有警告
/******************************************************************/
System.out.println(a);//2
```

- 最新标准的 java 和 C 中自增自减的区别

```java
short a = 1;
a += (a++) + (++a);//此类“谭++”式表达式虽然毫无意义，甚至有点反人类，但是考试经常考
/*
C中先计算右边内容：1+(2+1)=4，此时由于(++a)的自增，a=3；然后进行a = a + 4的计算，所以最后结果a = 7
java中同样是先计算右边的内容：1+(2+1)=4，但是a的值不会因为自增而改变，仍然a = 1，然后直接进行a = a + 4的计算，结果a = 5
*/
System.out.println(a);//5
```

- 逻辑运算符（操作对象必须是 boolean 型）

```java
/*
C中只有&&、||、!（即与、或、非）三种逻辑运算符（操作对象可以是任何基本数据类型，只对值进行判断：0即为假，非0即为真）
java中有&、|、&&、||、!、^（即逻辑与、逻辑或、短路与、短路或、逻辑非、逻辑异或）6种逻辑运算符，前面四种也可称单与、双与和单或、双或
java逻辑运算符中的&、|不管前面的表达式如何，都会执行后面的表达式（比较笨），而C中无此类的逻辑运算符
而逻辑运算符有短路情况，即前面的表达式可以得到最终结果时，后面的表达式将不被执行（比较聪明，节省了运行时间），反之执行；在这一点上，C中的&&、||与java相同；
因此一般开发都使用&&、||，|和&多出现在考试中
*/
//下面以&和&&为例，|和||类似
boolean judgement1 = false;
int number1 = 1;
if(judgement1 & (number1++ > 0))
System.out.println(number1);//2

boolean judgement2 = false;
int number2 = 1;
if(judgement2 && (number2++ > 0))
System.out.println(number2);//1
```

- 位运算符（实用很少，但是考试会有相关的题目）：左移操作<<，低位补0（多出的高位丢弃）；右移操作>>，高位补符号位（符号位为何值，就补何值）


```java
//注：所有的位运算都是对补码进行操作的，且符号位不参与移位
//左移操作
//①
int a = 44;
int b = a << 2;
System.out.println(b);
//0 000 0000 0010 1100		44
//0 000 0000 1011 0000		结果176
//②
int c = -8319;
int d = c << 2;
//1 010 0000 0111 1111		原码-8319
//1 101 1111 1000 0001		补码-8319
//1 111 1110 0000 0100		左移结果（补码）
//1 000 0001 1111 1100		左移结果（原码）-33276
System.out.println(d);//-33276

//右移操作
int e = -36;
int f = e >> 2;
//1 000 0000 0010 0100		原码-36
//1 111 1111 1101 1100		补码-36
//1 111 1111 1111 0111		右移结果（补码）
//1 000 0000 0000 1001		右移结果（原码）-9
System.out.println(f);//-9
```

- 比较运算符`instanceof`判断对象是否是一个类

下面是产生随机数的一个例子

```java
public class MathTest{
    public static void main(String[] args){
        double Test1 = Math.random();
        //Math类中的random方法返回一个[0.0,1.0)之间的随机数
        double Test2 = Math.random() * 90 + 10;
        //通过式子处理，产生[10.0,100.0)之间的随机数

        int value = (int)(Math.random() * 90 + 10);
        //通过强制转换，产生[10,100)之间的整数即[10,99]
        System.out.println(value);
        //由上不难得出产生任意范围[a,b]内的随机整数公式:
        //(int)(Math.random()*(b - a + 1) + a)
    }
}
```

## 2.5 switch-case语句

与C不同，java中的的switch(variable)中的变量variable可以为以下6种数据类型之一：byte、short、char、int、枚举类型( JDK 5.0新增)、String( JDK 7.0新增)，而C中的只能为整型。

## 2.6 break和continue关键字

break默认结束当前循环，可用于循环语句和switch-case语句；continue默认只结束当前循环的本次循环，且continue只能用于循环语句。两者相同点是：同一层次位置处，其后面不能有执行语句，否则编译报错。

```java
//标签的使用（java中有，C中没有）
label:for(......){
    for(......){
        break label;//结束label标签处的当前循环
        //continue label;//结束label标签处的外层循环的本次循环
    }
}
```

# 3. 数组

> 数组属于引用数据类型，而数组的元素可以是任何数据类型

## 3.1 一维数组

```java
import java.util.Scanner;

public class OneDimensionalArray {
    public static void main(String[] args) {
        //1.数组静态初始化
        int[] array1_1 = new int[]{1,2,3,4};//引用类型初始化都需要借助new
        String[] array1_2 = new String[]{"川建国","拜振华","FakeNews","China"};

        //2.数组动态初始化
        int[] array2_1 = new int[4];
        String[] array2_2 = new String[4];

        System.out.println(array2_1.length);//length属性返回数组的长度
        //数组一旦初始化，便确定了长度


        //要求：输入学生人数及分数，根据分数与最高分之间的差值来评级：
        //[0,10)为A，[10,20)为B，[20,30)为C，[30,maxScore]为D
        System.out.println("输入人数：");
        Scanner scan = new Scanner(System.in);
        int number = scan.nextInt();
        int[] score = new int[number];
        int maxScore = score[0];
        System.out.println("输入分数：");
        for (int index = 0; index < score.length; index++) {
            score[index] = scan.nextInt();
            if (maxScore < score[index]) {
                maxScore = score[index];
            }
        }
        System.out.println("最高分maxScore = " + maxScore);
        for (int index = 0; index < score.length; index++) {
            if (maxScore - score[index] < 10) {
                System.out.println("学生" + index + "的分数等级为：" + "A");
            } else if (maxScore - score[index] < 20) {
                System.out.println("学生" + index + "的分数等级为：" + "B");
            } else if (maxScore - score[index] < 30) {
                System.out.println("学生" + index + "的分数等级为：" + "C");
            } else if (maxScore - score[index] <= maxScore) {
                System.out.println("学生" + index + "的分数等级为：" + "D");
            }
        }
    }
}
```

在遍历数组时，可以使用增强for循环（JDK1.5新增）

```java
int[] arr = new int[]{1,2,3,4,5};

        //使用普通for循环实现
        for(int i =  0 ; i < arr.length ; i++){
            System.out.println("元素："+ arr[i]);
        }

        //使用增强for循环实现 
        for(int ints : arr){
            System.out.println("元素："+ ints);
        }
```

不同类型的数组元素的默认初始化值不同


| 元素类型                                | 初始化值 |
| :-------------------------------------- | :------: |
| 整型（byte、short、char、int、long）    |    0     |
| 浮点型（float、double）                 |   0.0    |
| 字符型（char）                          |    0     |
| 布尔型（boolean）                       |  false   |
| 引用数据类型（class、interface、array） |   null   |

## 3.2 二维数组

```java
public class TwoDimensionalArray {

    public static void main(String[] args) {
        //1.静态初始化
        int[][] array1 = new int[][]{{1, 2, 3}, {4, 5, 6}};

        //2.动态初始化
        int[][] array2_1 = new int[2][3];
        int[][] array2_2 = new int[2][];

        int[][] arr = new int[4][3];
        System.out.println(arr);//[[I@1b6d3586，“[[”代表二维数组，“I”代表int型，@后面的数表示地址值
        System.out.println(arr[0]);//[I@4554617c
        System.out.println(arr[0][0]);//0
    }
}
```

## 3.3 数组中涉及的常见算法

### 3.3.1 数组元素的赋值（杨辉三角、回形数等）

```java
import java.util.Scanner;
//以杨辉三角为例
public class YangHuiTriangle {
    public static void main(String[] args) {
        //使用二维数组打印杨辉三角
        System.out.print("输入行数：");
        Scanner scan = new Scanner(System.in);
        int column = scan.nextInt();
        int[][] yangHui = new int[column][];

        for(int i = 0;i < yangHui.length;i++){
            yangHui[i] = new int[i + 1];//第i行有（i+1）列
            yangHui[i][0] = yangHui[i][i] = 1;//每行第一个和最后一个赋值0

            //给每行的非行首行尾的元素赋值
            for(int j = 1;j < yangHui[i].length - 1;j++){
                yangHui[i][j] = yangHui[i-1][j-1] + yangHui[i-1][j];
            }
        }

        //遍历二维数组
        for(int i = 0;i < yangHui.length;i++){
            for(int j = 0;j < yangHui[i].length;j++){
                System.out.print(yangHui[i][j] + "\t");
            }
            System.out.println();
        }
    }
}
```

### 3.3.2 求数组元素的最大值、最小值、总和、平均值

### 3.3.3 数组元素的查找

1.线性查找（按顺序查找）<br>2.二分法查找（折半查找）：使用前提是<font color= "red">有序（升降序都行）的数据</font>

```java
import java.util.Scanner;

public class BinarySearch {
    public static void main(String[] args) {

        int[] array = new int[]{-18, -9, 12, 21, 34, 45, 78, 90, 99, 123};
        int head = 0;
        int end = array.length - 1;

        System.out.print("请输入需要查找的值：");
        Scanner scanner = new Scanner(System.in);
        int number = scanner.nextInt();
        boolean flag = true;
        while (head < end) {
            int middle = (head + end) / 2;
            if (number == array[middle]) {
                System.out.print("找到了指定的元素，索引位置为：" + middle);
                flag = false;
                break;
            } else if (number > array[middle]) {
                head = middle + 1;
            } else {
                end = middle - 1;
            }
        }
        if (flag) {
            System.out.println("很遗憾，没有找到该元素值");
        }
    }
}
```

### 3.3.4 数组元素的排序算法

下面以冒泡法为例，其他的排序算法暂时不提


```java
public class BubbleSort {
    public static void main(String[] args) {
        int[] array = new int[]{0, 12, -9, 123, 121, 90, 65, 1, 32, 19};
        int temp = 0;
        for (int i = 0; i < array.length - 1; i++) {
            for (int j = 0; j < array.length - 1 - i; j++) {
                if (array[j] > array[j + 1]) {
                    temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;
                }
            }
        }
        for (int i = 0; i < array.length; i++) {
            System.out.print(array[i] + "\t");
        }
    }
}
```

## 3.4 关于数组的Arrays类的常用方法

```java
import java.util.Arrays;f

public class ArraysTest {
    public static void main(String[] args) {
        //Arrays类中的常用方法
        //1.boolean equals(int[] a,int[] b)比较两数组是否相等（元素值是否相等）
        int[] array1 = new int[]{4,5,2,3};
        int[] array2 = new int[]{2,3,4,5};
        boolean isEqual = Arrays.equals(array1,array2);
        System.out.println(isEqual);

        //2.String toString(int[] a)输出数组信息
        System.out.println(Arrays.toString(array1));

        //3.void fill(int[] a,int val)将指定值填充到数组中
        Arrays.fill(array2,10);
        System.out.println(Arrays.toString(array2));

        //4.void sort(int[] a)对数组进行排序
        int[] array3 = new int[]{0, 12, -9, 123, 121, 90, 65, 1, 32, 19};
        Arrays.sort(array3);
        System.out.println(Arrays.toString(array3));

        //5.int binarySearch(int[] a,int key)查找数组中元素的索引
        int[] array4 = new int[]{0, 12, -9, 123, 121, 90, 65, 1, 32, 19};
        int index1 = Arrays.binarySearch(array3,121);
        int index2 = Arrays.binarySearch(array3,122);
        System.out.println(index1);
        System.out.println(index2);//若没有找到，则返回负数，具体是负多少，需查看该方法的源码

    }
}
```

# 4. 面向对象编程（上）

> Java类及类的成员：属性、方法、构造器；代码块、内部类
>
> 面向对象的三大特征：封装性、继承性、多态性、（抽象性）
>
> 其他关键字：this、super、static、final、abstract、interface、package、import

## 4.1 类和对象

类：对一类事物的描述，是抽象的、概念上的定义<br>对象：实际存在的该类事物的每个个体，因而可以说是类的实例（instance）<br>匿名对象：不需要创建一个对象去接收new出来的引用类型，或者说创建对象时没有显示地赋给一个变量名，这样即为匿名对象。但是，匿名对象只能使用1次，调用完之后便会被回收掉。

```java
new Student().height = 176;
System.out.println(new Student().height);//结果为0，因为上一句的new Student()的匿名对象在使用完之后便被回收了
```

只有在传入形参等只需要使用1次对象的时候才会被采用。<br><font color="red">面向对象程序设计的重点是类的设计，而设计类，就是设计类的成员</font>，一段示例代码如下：

```java
public class ClassTest {
    public static void main(String[] args) {
        Person p1 = new Person();
        p1.name = "Tom";
        p1.isMale = true;
        Person p2 = new Person();
        System.out.println(p2.name);
        Person p3 = p1;
        p3.age = 10;
        System.out.println(p1.age);
    }
}
class Person{
    String name;
    int age = 1;
    boolean isMale;
}
```

上述关于对象的代码的内存解析如下：![image-20210219173927212](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210219173927212.png)

关于对象数组代码的内存解析如下：

![image-20210219180938556](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210219180938556.png)

stus数组元素都是student类型（即引用类型），所以数组成员在没有初始化时（new创建对象）默认为null。若此时将其属性值打印出来`System.out.println(stus[1].number);`，那么便会报错，为空指针异常。因为null不会指向任何地址，无法读出值。只有初始化数组成员即`stus[1] = new Student();`之后才能读出改成员的属性。

## 4.2 属性（或称 “成员变量” ）与局部变量的区别

>  属性：直接定义在类的一对 {} 内
>
> 局部变量：<font color="red">声明</font>在方法内、方法形参、代码块内、构造器形参、构造器内部的变量

区别如下：<br>1.权限修饰符<br>可以在声明属性时，使用权限修饰符指明其权限。常用权限修饰符：private、public、protected、缺省（就是不写）。但是局部变量不能用修饰符修饰，否则编译不通过，报错。<br>2.默认初始化值<br>局部变量没有默认的初始化值，因此在调用局部变量时，一定要显式赋值（调用形参时赋值即可）。属性默认的初始化值如下（与数组元素的默认初始化值相同）：![image-20210219174910851](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210219174910851.png)

3.内存中加载的位置<br>属性加载到堆空间中（非static）。堆内变量在没有栈内变量的指向时，会被垃圾回收器回收。局部变量加载到栈空间中，在方法结束后，局部变量出栈。

## 4.3 方法

### 4.3.1 方法的重载

在同一个类中，允许存在一个以上的同名（返回值类型不同也可）方法，只要它们的参数个数或者参数类型不同即可，那么这些重名的两个或两个以上的方法之间就是方法重载。

```java
下列方法是否与void show(int a,char b,double c){}构成方法重载

a)void show(int x,char y,double z){}//no，因为尽管形参名字不同，但是形参类型都是一致的

b)int show(int a,double c,char b){}//yes，因为两者的形参列表的顺序不同

c)void show(int a,double c,char b){}//yes，同上

(b)和(c)之间并不构成方法重载，两者完全一致，但是返回值类型不同，会产生歧义

d)boolean show(int c,char b){}//yes，参数列表不同

e)void show(double c){}//yes，同上

f)double show(int x,char y,double z){}//no，形参类型一致

g)void shows(){double c;}//no，方法名字都不一样
```

### 4.3.2 可变个数的形参

JavaSE 5.0中提供了Varargs(Variable number of arguments)机制，允许直接定义能和多个实参相匹配的形参。从而，可以用一种更简单的方式，来传递个数可变的实参。<br>JDK5.0以前：采用数组形参来定义方法，传入多个同一类型变量public static void test(int a ,String[]books);<br>JDK5.0：采用可变个数形参来定义方法，传入多个同一类型变量public static void test(int a ,String...books);

```java
public static void test(int a,String[] books);
public static void test(int a,int[] books);
public static void test(int a,String...books);
public static void test(int a,int...books);
```

传入的参数可以是：0，1，2，3.......。但是，可变个数形参在方法的形参中必须声明在末尾，并且最多只能声明一个可变形参。上述两个方法之间并不构成方法重载，两者恰恰是完全相同的。

### 4.3.4 方法参数的值传递机制

java中方法的参数传递方式只有一种：值传递。即将实际参数的副本（复制品）传入方法内，而参数本身不受影响。<br>当形参是基本数据类型，则传递基本数据类型的<font color="red">数据值</font>；当形参是引用数据类型，则传递引用数据类型变量的<font color="red">地址值</font>。

### 4.3.5 递归（recursion）方法

```java
//递归求和
public int getSum(int n){
    if(n == 1){
        return 1;
    }else{
        return n + getSum(n - 1);
    }
}
```

```java
//递归求斐波那契数
public class FibonacciSequence {
    public static void main(String[] args) {
        int[] arr = new int[100];
        System.out.print("n = ");
        Scanner input = new Scanner(System.in);
        int n = input.nextInt();

        FibonacciSequence test = new FibonacciSequence();
        //前n项斐波那契数列存到数组arr中
        for(int i = 1;i <= n;i++){
            arr[i] = test.function(arr,i);
        }
        System.out.println("前" + n + "项斐波那契数列如下：");
        for(int i = 1;i <= n;i++){
            System.out.print(arr[i] + "\t");
        }
        System.out.println();
    }
    /*利用递归，创建方法求出斐波那契数列的某一项的值*/
    public int function (int[] arr,int n){
        if(n == 1){
            return 1;
        }else if(n == 2){
            return 1;
        }else{
            return arr[n-1] + arr[n-2];
        }
    }

}
```

## 4.4 面向对象特征

### 4.4.1 权限修饰符

Java规定的4种权限（从小打大）：`private`、缺省（就是不写）、`protected`、`public`置于<font color="red">类的成员（属性、方法、构造器、内部类）</font>定义前，用来限制对象对该类成员的访问权限。<br>而class类只能被`public`、缺省修饰。`public`类可以在任意地方被访问；缺省类只可以被同一个包的类之间访问。修饰符的访问权限如下表所示：

|      修饰符      | 类内部 | 同一个包的不同类 | 不同包的子类 | 同一个工程（含多个包） |
| :--------------: | :----: | :--------------: | :----------: | :--------------------: |
|    `private`     |  yes   |        no        |      no      |           no           |
| 缺省（就是不写） |  yes   |       yes        |      no      |           no           |
|   `protected`    |  yes   |       yes        |     yes      |           no           |
|     `public`     |  yes   |       yes        |     yes      |          yes           |

### 4.4.2 封装性`Encapsulation`（面向对象的特征之一）

当创建一个类的对象后，可以通过`对象.属性`或`对象.方法`的方式进行初始化。但是，在实际问题中，往往需要给属性添加限制条件（如动物的腿的数一般都是偶数even number）。然而这个限制条件就无法在属性声明时设置，只能通过在该类中创建方法添加限制条件而不用对象调用属性。<br>同时，为了避免<font color="red">既使用方法设置限制条件，又通过对象调用设置限制条件</font>的混乱情况，使用`private`关键字将属性或者方法声明为私有的。

<strong>封装性的体现1：</strong>将类的属性`xxx`使用`private`私有化，同时，提供公共的方法（即public修饰的）来获取（`getXxx`）和设置（`setXxx`）此属性的值；<br><strong>封装性的体现2：</strong>不对外暴露私有的方法；<br><strong>封装性的体现3：</strong>单例模式（将构造器私有化）；<br><strong>封装性的体现4：</strong>如果不希望类在包外被调用，可以将类设置为缺省的。

## 4.5 构造器（或构造方法，constructor）

### 4.5.1 构造器的特征

具有与类相同的名称、不声明返回值类型（与声明为void不同）、不被`static`、`final`、`synchronized`、`abstract`、`native`修饰，不能用return语句返回值。

### 4.5.2 构造器的作用

<strong>创建对象（最核心的作用），</strong>如：`Order o = new Order();`<br>在创建对象时对属性初始化，如：`Person p = Person("Peter",15);`

### 4.5.3 说明

如果没有显式地定义类的构造器的话，则系统默认提供一个空参构造器；<br>定义构造器的格式：`权限修饰符 类名(形参列表){}`；<br>一个类中定义的多个构造器，彼此构成重载；<br>一旦显式地定义了类的构造器之后，系统就不再提供默认的空参构造器；<br>一个类中，至少有一个构造器。

```java
//        编写两个类，TriAngle和Constructor
//        其中TriAngle类中声明私有的底边长base和高height，同时声明公共方法访问私有变量。此外，提供类必要的构造器
//        Constructor类中使用这些公共方法，计算三角形的面积
public class Constructor {
    public static void main(String[] args) {
        TriAngle angle1 = new TriAngle();
        angle1.setBase(3.0);
        angle1.setHeight(4.9);
        System.out.println("base = " + angle1.getBase() + "\theight = " + angle1.getHeight() + "\tarea = " + angle1.area());

        TriAngle angle2 = new TriAngle(2.0,3.1);
        System.out.println("base = " + angle2.getBase() + "\theight = " + angle2.getHeight() + "\tarea = " + angle2.area());

    }
}

class TriAngle {
    private double base;
    private double height;

    //    通过声明公共的方法访问私有变量
    public void setBase(double b) {
        base = b;
    }

    public double getBase() {
        return base;
    }

    public void setHeight(double h) {
        height = h;
    }

    public double getHeight() {
        return height;
    }
    
    //构造器声明。一旦我们显式地定义了一个如public TriAngle(double b, double h) {}类的造器之后，系统便不再提供默认的空参构造器，即Triangle t1 = new Triangle();就没有用了，必须要再定义一个空的构造器public Triangle(){}才能使用Triangle t1 = new Triangle();创建对象t1
    public TriAngle() {

    }
	
    public TriAngle(double b, double h) {
        base = b;
        height = h;
    }
    //    声明计算面积的公共的方法
    public double area() {
        double area = base * height / 2.0;
        return area;
    }

}
```

## 4.6 JavaBean（后面再提）

所谓JavaBean，其实是一种符合如下标准的Java类：

>类是公共的；
>
>有一个无参的公共的构造器；
>
>有属性，且有对应的get、set方法。

## 4.7 关键字`this`

`this`可以用来修饰和调用属性、方法、构造器

### 4.7.1 `this`修饰调用属性和方法

可以将`this`理解为当前对象或者当前正在创建的对象。<br>在类的方法中，我们可以使用`this.属性`或者`this.方法`的方式，调用当前对象属性或者方法。但是通常情况下，我们都选择省略`this`。特殊情况下即如果方法的形参和类的属性同名时，我们必须显式地使用`this.变量`的方式，表明此变量是属性，而非形参。

```java
public class Person{
    int age;
    String name;
    public void method(int age){
    	//如果这里不是用this修饰，那么便会默认是形参自己给自己赋值
        this.age = age;
	}
}
```

### 4.7.2 `this`调用构造器

① 在类的构造器中，可以显式地使用`this(形参列表)`方式，调用本类中指定的其他构造器；<br>② 构造器中不能通过`this(形参列表)`调用自己；<br>③ 规定：`this(形参列表)`必须声明在当前构造器的首行；

```java
public constuctor1(){};
public constructor2(double a,int b){
    this.constructor1();
    b = a;
}
```

## 4.8 `package`、`import`关键字

### 4.8.1 `package`关键字

为了解决项目中有众多复杂的类和接口的问题，使用包来进行管理，类似文件夹管理文件。使用`package`在首行声明类或者接口所属的包。一般使用小写字母命名`xxyyzz`，每`.`一次就代表一层文件目录。比如`xx.yy.zz`就说明xx是yy的父目录，yy是zz的父目录。且同一个包下不能有同名的类或接口。JDK中常用的包如下：

| 包名        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| `java.lang` | 包含一些java语言的核心类，如 `String`、`Math`、`Integer`、`System`、`Thread`等，提供常用功能 |
| `java.net`  | 包含执行与网络相关的操作的类和接口                           |
| `java.io`   | 包含能提供多种输入/输出功能的类                              |
| `java.util` | 包含了一些实用的工具类，如定义系统特性、接口的集合框架类、使用与日期日历相关的方法 |
| `java.text` | 包含了一些java格式化相关的类                                 |
| `java.sql`  | 包含了java进行JDBC数据库编程的相关类/接口                    |
| `java.awt`  | 包含了构成抽象窗口工具集（abstract window toolkits）的多个类，这些类用来构建和管理应用程序的图形用户界面（GUI）B/S、C/S<br>由于做出的界面极其丑陋，所以一般不用这个做GUI。现在一般是通过浏览器来访问后台服务器 |

### 4.8.2 `import`关键字

使用`import`结构导入指定包下的类、接口声明在包声明和类声明之间。

```java
import java.util.Scanner;//导入util包下的Scanner类
import java.util.Arrays;//导入util包下的Arrays类
import java.util.*;//导入util包下的所有的类和接口，不包括其子包的类和接口，子包需要额外导入

//注意，源文件都是默认导入了lang包中的所有类和接口，不用再导包
import java.lang.reflect.Field;//lang包中的子包reflect包下的Filed类不是lang包下的类，而是其子包reflect下的，所以一定要显式导包，不能省略

//如果源文件中使用的类或接口是本包下定义的，则可以不用导包，直接调用即可
//尽管不同的包下的类或接口可以同名，但是若是想同时用这些同名的类或接口，则必须在使用前加上完整的包名（这样的类名称作全类名），如：
pers.zhangsan.exercises.Person p1 = new Person();
pers.lisi.exercises.Person p2 = new Person();

//拓展：import static可以导入类或接口中的静态结构（属性或方法），了解即可
import static java.lang.System.*;
import static java.lang.Math.*;//切忌这样写：import static java.lang.Math;
out.println("好好学习，天台向上");
long num = round(123.456);
```

# 5. 面向对象编程（中）

## 5.1 继承性`inheritance`（面型对象特征之二）

继承的格式：`class A extends B{}`，其中，A称作<font color="red">子类或者派生类</font>`subclass`，B称作<font color="red">父类或者基类或者派生类</font>`superclass`。<br>一旦子类A继承父类B以后，子类中就继承了父类B中声明的所有属性和方法。特别的，父类中如果声明了`private`的属性和方法，仍然能被继承，只不过因为封装性的影响使得不能直接调用父类中的属性和方法而已。<br>子类继承父类之后，还可以声明自己特有的属性和方法，实现功能的拓展



## 5.2 方法的重写`override`

## 5.3 四种访问权限修饰符

## 5.4 关键字`super`

## 5.5 子类对象实例化过程

## 5.6 多态性

## 5.7 `Object`类的使用

## 5.8 包装类的使用





P260

<span id="bottom"></span>

