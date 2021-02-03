# 1. 前言

### 1.1语言的特点

- 面向对象

  - 两个基本概念：类、对象

  <!--more-->

  - 三大特性：封装、继承、多态

- 健壮性

  - 去除了C/C++中的影响健壮性的指针内存的申请与释放等，提供一个相对安全的内存管理和访问机制
  - 垃圾回收机制（但是仍然会出现内存溢出和内存泄露的问题）

- 跨平台性

  一次编译，多次运行（Write once，run anywhere）
  
  原理为：在需要运行Java的应用程序的操作系统上，先安装虚拟机即可。由虚拟机来负责Java程序在系统中的运行。

### 1.2 java的两种核心机制

- 虚拟机机制（Java Virtual Machine）
- 垃圾回收机制（Garbage Collection）

### 1.3 JDK、JRE、JVM

- JDK=JRE + 开发工具集（例如javac编译工具等）

- JRE=JVM + JavaSE标准类库

### 1.4 文档注释（java特有）

/**

@author	指定JAVA程序的作者

@version	1.8-271

*/

# 2. 基本语法

### 2.1 关键字、保留字、标识符

- 关键字

  过多，使用时记忆

- 保留字

  现有JAVA版本尚未使用名，但是以后版本可能会作为关键字使用，因此命名标识符时需要避免使用这些保留字：const、goto

- 标识符

  变量名、方法名、类名、接口名、包名等凡是自己可以命名的都叫标识符，命名时JAVA是严格区分大小写的

### 2.2 命名规范

- 包名：所有单词小写"xxyyzz"
- 类名、接口名：每个单词的首字母大写（大驼峰命名）"XxYyZz"
- 变量名、方法名：第一个单词小写，后面的单词每个单词首字母大写（小驼峰命名）"xxYyZz"
- 常量名：所有字母大写，多个单词时用下划线连接"XXYYZZ"

### 2.3 数据类型

- 基本数据类型（primitive type）

  - byte、short、int、long（整型）

    整型常量默认为 int 型

  - float、double（浮点型）

    浮点型常量默认为 double 型

    定义 long 和 float 类型初始化及赋值时需要在数值后面加上 "L" 或 “l” 和 “F” 或 “f”，常用 int 和 double 类型。若 long 型不加上后缀，则默认为 int 型，而 float 类型必须加上后缀，否则编译报错

  - char（字符型）

    与C不同，java的字符型 char（占2个字节）可以表示任何一个字符，而不单单是西文字符，如 char a = '我';

    char a = '48'; 是错误的，因为 '48' 是2个字符，哪怕是'4 '也不行，空格也算一个字符，但是 char a = 48; 是对的，因为没有用单引号 '' 括起来时，相当于将 ASCII 码值给ａ，编译时机器会查表将其替换成对应的字符。

    128 个 ASCII 码字符用8位表示，最高位规定为0，剩下7位表示0~127的 ASCII 码字符

  - boolean（布尔型）

- 引用数据类型（reference type）

  - class（类）

  - interface（接口）

  - array（数组）
  
- 数据类型转换（不包括boolean）

  - 自动类型提升

    当容量小的数据类型的变量与容量大的数据类型的变量做运算时，结果自动提升为容量大的数据类型。

    即  byte、char、short → int → long → float → double

    特别地，当byte、char、short 三种类型的变量做运算时，结果为 int 型

  - 强制类型转换（自动类型提升的逆运算）

### 2.4 运算符

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

- 比较运算符

  ==instanceof==：判断对象是否是一个类

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

- 位运算符（实用很少，但是考试会有相关的题目）

  左移操作<<，低位补0（多出的高位丢弃）；右移操作>>，高位补符号位（符号位为何值，就补何值）

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

随机数获取

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

### 2.5 switch-case语句

与C不同，java中的的switch(variable)中的变量variable可以为以下6种数据类型之一：

byte、short、char、int、枚举类型( JDK 5.0新增)、String( JDK 7.0新增)

而C中的只能为整型

### 2.6 break和continue关键字

break默认结束当前循环，可用于循环语句和switch-case语句

continue默认只结束当前循环的本次循环，且continue只能用于循环语句

两者相同点是：同一层次位置处，其后面不能有执行语句，否则编译报错

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

### 3.1 一维数组

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

不同类型的数组元素的默认初始化值不同



| 元素类型                                | 初始化值 |
| :-------------------------------------- | :------: |
| 整型（byte、short、char、int、long）    |    0     |
| 浮点型（float、double）                 |   0.0    |
| 字符型（char）                          |    0     |
| 布尔型（boolean）                       |  false   |
| 引用数据类型（class、interface、array） |   null   |

![image-20210117163604167](D:%5Clocal%5CPhoto%5CTypora%5Cimage-20210117163604167.png)

### 3.2 二维数组

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

某段示例代码内存解析如下：

![image-20210117221927668](D:%5Clocal%5CPhoto%5CTypora%5Cimage-20210117221927668.png)

### 3.3 数组中涉及的常见算法

- 数组元素的赋值（杨辉三角、回形数等），下面以杨辉三角为例

  ```java
  import java.util.Scanner;
  
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

- 求数组元素的最大值、最小值、总和、平均值

- 数组的赋值、反转、查找

  - 赋值

  - 查找

    - 线性查找（按顺序查找）

    - 二分法查找（折半查找）：使用前提是“有序（升降序都行）的数据”

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

- 数组元素的排序算法

  - 冒泡排序

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

  - 快速排序

  ......

### 3.4 Arrays类的常用方法

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

# 4. 面向对象

> Java类及类的成员：属性、方法、构造器；代码块、内部类
>
> 面向对象的三大特征：封装性、继承性、多态性、（抽象性）
>
> 其他关键字：this、super、static、final、abstract、interface、package、import、

### 4.1 类和对象

类：对一类事物的描述，是抽象的、概念上的定义

对象：实际存在的该类事物的每个个体，因而可以说是类的实例（instance）

**面向对象程序设计的重点是类的设计，而设计类，就是设计类的成员**

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

下述代码的内存解析如下：

![image-20210118160535130](D:%5Clocal%5CPhoto%5CTypora%5Cimage-20210118160535130.png)

- 属性（或称 “成员变量” ）与局部变量

  - 属性：直接定义在类的一对 {} 内

  - 局部变量：==声明==在方法内、方法形参、代码块内、构造器形参、构造器内部的变量

  - 区别

    - 权限修饰符

      可以在声明属性时，使用权限修饰符指明其权限

      常用权限修饰符：private、public、protected、缺省（不写就是缺省）

      但是局部变量不能用修饰符修饰，否则编译不通过，报错

    - 默认初始化值

      属性默认的初始化值如下：

      | 元素类型                             | 初始化值 |
      | ------------------------------------ | :------: |
      | 整型（byte、short、char、int、long） |    0     |
      | 浮点型（float、double）              |   0.0    |
      | 字符型（char）                       |    0     |
      | 布尔型（boolean）                    |  false   |
      | 引用类型（class、interface、array）  |   null   |

      局部变量没有默认的初始化值，因此在调用局部变量时，一定要显式赋值（调用形参时赋值即可）

    - 内存中加载的位置

      属性加载到堆空间中（非static）。堆内变量在没有栈内变量的指向时，

      局部变量加载到栈空间中，在方法结束后，局部变量出栈

- 方法的返回值

  当没有返回值时（void类型），则不能return value; 若想使用return，则可写成return;表明结束方法。

  不管是否有返回值，return后面都不能有执行语句，否则编译报错

> 在方法的使用中，可以调用该方法所属类的属性和方法



进度：P192

public修饰的类名必须和源文件的名称一致

一个源文件可以声明多个class类，然而只能有一个类为public所修饰，所以编译时若有多个类，便会产生多个类对应的字节码文件名（因为一个类对应一个.class字节码文件）

