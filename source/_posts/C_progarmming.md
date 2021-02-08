---
title: C语言基础
date: 2021-02-08 18:28:21
declare: true
tags:
- C
---

在刚学C语言的时候就是奔着考试去的，直到后面学了计算机的工作原理之后才发现底层原理是如此地重要，便又重新将C慢慢捡了回来。本来刚建好博客的时候应该把文章发布的，但是最近事情较多，就没有将文章发布到自己的博客网站上。今天有空就发布了。

以下内容较为基础，且仅涉及我自己容易忘记的重要知识点，供以后再次忘记时查阅。此篇博客未完待续......

<!--more-->

# Switch语句执行机制

**1. 首先，判断;**

- 在所有case关键字后面的值中，查找与“switch(a)”中的“a”一致的值。如果case语句与case语句之间有default语句，直接跳过default语句

**2. 然后，执行;**

- 若有与之匹配相同的值，则执行该case所属的那条语句
- 若没有与之匹配相同的值，则执行该default所属的那条语句

**3. 最后，结束;**
- 若被执行的case语句或者default语句后面没有语句了（即，到了switch语句末尾）,则在执行该语句之后，跳出switch语句，结束；
- 若后面仍有语句，则在执行完该语句之后，对后面的语句不加以判断（default语句也是，不加以判断），直接按顺序执行，直到switch语句末尾，结束；

所以一般会在每个case后面增加一个break语句以跳出switch，从而避免在完成任务后不加判断地执行其后面的语句;

代码如下：
```c
#include<stdio.h>
int main() {
	int a = 1;
      //int a = 2;
      //int a = 3;
	switch (a) {
	case 2:
		printf("2\n");
	case 3:
		printf("3\n");
                break;
	default:
		printf("没有找到对应的值，执行deafault语句\n");
	case 4:
		printf("4\n");
	}
}
```
运行结果如下：

- 当a=1时
![](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210109210221394-821136187.png)
- 当a=2时
![](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210109210450073-968059575.png)
- 当a=3时
![](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210109210613507-1532583958.png)

# 随机数生成

代码如下：
```c
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
//使用系统时钟作为种子,time()
int main() {
	srand((unsigned)time(NULL));	//播种，产生随机数(其类型为unsigned int)
	//randomize();		        //也可用这个函数
	printf("%d\n\n", RAND_MAX/*定义在stdlib.h中*/);	//产生随机数的最大值32767
	for (int i = 0; i < 10; i++)
		printf("%d\n", rand());		       //随机数范围为[0,32767]


		//rand()/32767.0;产生[0,1]之间的随机数（注意此时的格式转换符要换成%f或%lf）
		//rand()%100;产生[0,100)之间的随机数
		//rand()%101;产生[0,100](因为产生的是整数，所以[0,101)与[0,100]是等价的）之间的随机数
		//rand()%a;产生[0,a)之间的随机数
		//rand()%(a+1);产生[0,a]之间的随机数
		//rand()%(a+1)+b;产生[a,a+b]之间的随机数
}
```
运行结果如下：

![](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210109213542768-308089942.png)

# 数据类型的范围及其所占内存空间

## 1.数据范围

代码如下：

```c
#include<stdio.h>
#include<climits>
#include<limits.h>
//利用标准头文件<limts.h>来确定个类型数据的范围，但是浮点型的范围不能用这种方法表示出来
int main() {
	//signed types
	printf("signed char min=%d\n", SCHAR_MIN);//-2^7
	printf("signed char max=%d\n", SCHAR_MAX);//2^7-1
	printf("signed short min=%d\n", SHRT_MIN);//-2^15
	printf("signed short max=%d\n", SHRT_MAX);//2^15-1
	printf("signed int min=%d\n", INT_MIN);//-2^31
	printf("signed int max=%d\n", INT_MAX);//2^31-1
	printf("signed long min=%ld\n", LONG_MIN);//-2^31
	printf("signed long max=%ld\n", LONG_MAX);//2^31-1

	//unsigned types(最小值就是0)
	printf("unsigned char max=%u\n", UCHAR_MAX);//2^8-1
	printf("unsigned short max=%u\n", USHRT_MAX);//2^16-1
	printf("unsigned int max=%u\n", UINT_MAX);//2^32-1
	printf("unsigned long max=%lu\n", ULONG_MAX);//2^32-1
	printf("%zd\t%zd\n", sizeof(unsigned int), sizeof(signed int));
	//4，4
	//说明有无unsigned只会影响其所能容纳的数据的阈值，而其所占内存不变
	printf("%zd\t%zd\t%zd\t%zd\n",sizeof(char), sizeof(short), sizeof(int), sizeof(long));
	//1，2，4，4
	printf("%zd\t%zd\t%zd\n", sizeof(long long), sizeof(float), sizeof(double));
	//8,4,8
	//故char类型占1个字节，short类型占2个字节，int类型占4个字节
        //long类型：64位Windows中占4个字节，64位linux中占8个字节
	//long long类型占8个字节，float类型占4个字节，double类型占8个字节
}
```
运行结果如下：

![](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210109215905164-1472620072.png)

## 2.强制类型转换

> 只有char与short、char与char、short与short之间的运算都是先将其转换为int型，再进行运算。而其他的情况都是先将其向容量大（能够表示数的范围）的一种类型转换，然后再进行运算的

代码如下：
```c
#include<stdio.h>
int main(void) {
	char charType = 'a';
	short shortType = 1;
	int intType = 2;
	long long longlongType = 3;
	float floatType = 4.0;
	double doubleType = 5.0;
	//先将其转换为int，再进行运算
	printf("%zd\t%zd\t%zd\n", sizeof(charType + charType), sizeof(charType + shortType), sizeof(shortType + shortType));

	//int + longlong，则先将int转化为8个字节的longlong，再运算
	printf("%zd\t%zd\t%zd\n", sizeof(intType + intType), sizeof(intType + longlongType), sizeof(longlongType + longlongType));

	//float的表示范围比int要大（至于为何，比较复杂，此处不赘述，需要的可自行百度），故先将其转换为float，再运算
	printf("%zd\t%zd\t%zd\n", sizeof(intType + floatType), sizeof(intType + doubleType), sizeof(floatType + doubleType));

	//float的表示范围比longlong要大（原因同上），故先将其转换为float，再运算
	printf("%zd\n", sizeof(longlongType + floatType));
}
```
运行结果如下：

![](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210109224453237-1687919133.png)

# 最大公约数及最小公倍数

**最小公倍数 = 两数之积 / 最大公约数，因此只要得出最大公约数，便可得出最小公倍数，下面将通过几种算法进行实现**

## 1.辗转相除法（又称欧几里德算法）

> - 较大的数 % 较小的数 = 第一余数
> 
> - 较小的数 % 第一余数 = 第二余数
> 
> - 第一余数 % 第二余数 = 第三余数
> 
> - ······
> 
> 直到结果为0

代码如下：
```c
#include "stdio.h"
int main(){
    int num1, num2;
    int temp;
    int temp1, temp2;
    printf("输入两个数：");
    scanf_s("%d,%d",&num1, &num2);
    temp1 = num1;
    temp2 = num2;
    if(temp1 < temp2){//确保temp1为输入的两个数中，数值大的那个
        temp = temp1;
        temp1 = temp2;
        temp2 = temp;
    }
    /*********************************************/
    while(temp1 % temp2){
        temp = temp2;
        temp2 = temp1 % temp2;
        temp1 = temp;
    }
    /********************************************/
    printf("最大公约数：%d\n", temp2);
    printf("最小公倍数：%d\n", num1*num2 / temp2);
}
```
运行结果如下：

![](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210111171736895-315719992.png)

![](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210111171643588-400785892.png)

![](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210111171933456-1652579882.png)

## 2.更相减损法

> - 判断两数是否是偶数，若是，则用2约简，否则执行下一步，约简到两者都不是偶数时，执行下一步
>
> - 较大的数 - 较小的数 = 第一差
> 
> - 以较大的数减较小的数，接着把所得的差与较小的数比较，并以大数减小数。继续这个操作，直到所得的减数和差相等为止。
> 
> - 最后相等的值乘上2的幂（约简2的次数）即得最大公约数

代码如下：
```c
    /*********************************************/
    while(temp1 != temp2){
        if(temp1 > temp2)
            temp1 -= temp2;
        else
            temp2 -= temp1;
    }
    /*********************************************/
```

运行结果同上

## 3.Stein算法
> 由于对于两个数x y，若有x>y，则必有：
> 
> - x,y均为偶数 $gcd(x,y)=2gcd(\frac{x}{2},\frac{y}{2})$
> 
> - x,y均为奇数 $gcd(x,y)=gcd(\frac{x+y}{2},\frac{x-y}{2})$
> 
> - x为奇y为偶 $gcd(x,y)=gcd(x,\frac{y}{2})$
> 
> - x为偶y为奇 $gcd(x,y)=gcd(\frac{x}{2},y)$
> 
> 故只要将x，y依据上式换算成偶数，偶数换算成奇数后再次依据上式换算成新的偶数，每换算成一次偶数，记数加1，直到两个数最后相等，将相等的值乘上2的幂（计数值）即得最大公约数，
> 
> 上式中的数并不一定必须是2，也可换成其他的任意的数，只不过2是最小的素数，此处便用了2 

代码如下：
```c
int  Stein(int num1,int num2)
{
    int power = 0;
    int temp;
    if (num2 == 0)
        return 0;
    while (num1 != num2){
        if (num1 & 0x1){//when num1 is odd
            if (num2 & 0x1){//when num1 and num2 are both odd
                num1 = (num1 + num2) >> 1;//num1 = (num1 + num2)/2
                num2 = num1  - num2;//num2 = (num1 - num2)/2
            }
            else//when num1 is odd and num2 is even
                num2 >>= 1;
        }
        else{//when num1 is even
            if (num2 & 0x1){//when num1 and num2 are both even
                num1 >>= 1;
                if (num1 < num2){//ensure that num1 is greater than num2
                    temp = num1;
                    num1 = num2;
                    num2 = temp;
                }
            }
            else{//when num1 is even and num2 is odd
                num1 >>= 1;//num1 = mum1/2
                num2 >>= 1;//num2 = num2/2
                power++;
            }
        }
    }
    return (num1 << power);//gcd = num1 * 2^power
}
/*********************************************/
    temp2 = Stein(temp1,temp2);
/*********************************************/
```

运行结果同上

**stein算法是在欧几里德算法上做的改良，可以快速处理任何大数（超过128位的表示范围），而欧几里德算法遇到大数则需要很多时间（因为位运算和加减运算相较于取余运算来说，CPU的计算量更少）**

# 查找一定范围内的素数

代码如下：

```c
#include <stdio.h>
#include <math.h>
int isPrime(int num){//0 means not prime number, 1 means prime number
    int flag = 1;
    for(int index = 2; index <= sqrt(num); index++){
        if(num%index == 0){
            flag =0;
            break;
        }
    }
    return flag;
}
int main(){
    int range, count = 1;
    printf("输入查找范围：");
    scanf_s("%d",&range);
    printf("%d以内的素数如下：\n",range);
    printf("2\t");//Don't judge 2
    for(int index = 3; index <= range ; index += 2){
        if(isPrime(index)){
            printf("%d\t",index);
            count++;
            if(count%10 == 0)
                printf("\n");
        }
    }
    return 0;
}
```

运行结果如下：

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210112172426593-1257207043.png)

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210112172445999-1478334056.png)

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210112172521786-741779603.png)

# 指针数组

> 指针数组主要用于存放具有不同长度的字符串（存放多个字符串的最常用方式）

代码如下：

```c
#include<stdio.h>
char* monthName(int n) {//monthName函数返回第n个月份的名字，该函数的定义表明其monthName是一个函数，返回一个指向char类型的指针
    static char* name[] = { "Illegal month",//定义静态指针数组*name[]
                             //元素中存放的是各个字符串的地址
                            "January", "February", "March", "April",
                            "May", "June", "July", "August",
                            "September","October","November","December"
    };
    return (n < 1 || n>12) ? name[0] : name[n];
}
int main() {
    int number = 0;
    printf("输入月份对应的数字：");
    scanf_s("%d",&number);
    printf("%s\n", monthName(number));
    return 0;
}
```

运行结果如下：

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210112174039305-1808900711.png)

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210112174058851-169109391.png)

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210112173904342-827953661.png)

# 统计单词数目

由于每个单词字母不一样，长度不一样，所以来依靠**识别单词**来统计单词数是比较难的，下面观察一个字符串

> I am from China

不难发现，每个单词后面都是紧跟一个空格的

因此可以使用一个标志flag来表示上一个字符的状态（0代表是空格），string[i]来表示当前字符的状态

那么在对输入的字符串进行遍历的时候，如果当前字符string[i]不是空格（string[i]!=' '），而上一个字符是空格（flag==0），则说明有1个新单词

若当前字符不是空格（string[i]!=' '），但是上一个字符也不是空格（flag==1），则说明正在遍历一个单词的内部字符，没有1个新的单词

```c
#include<stdio.h>
int main() {
    char string[100];
    int count = 0, flag = 0;
    // flag==0 means a space
    printf("输入一句英文：");
    gets_s(string,100);
    for(int i = 0; string[i]; i++) {
        if (string[i] == ' ')// set flag to 0
            flag = 0;
        else if (flag == 0) {// flag==0 and string[i]!=' ' means a new word
            flag = 1;
            count++;
        }
    }
    printf("count = %d", count);
    return 0;
}                        
```

运行结果如下：

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210112184346385-768533576.png)

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210112185217988-467131753.png)

# sizeof(s)和strlen(s)的区别

strlen(s)即字符串长度（不包括结束标志'\0'）：返回字符串中的所有字符的个数（1个汉字按2个字符算），其中，每个成对的符号如''、"" 算作2个）；

字母以及英文符号（除标点符号及其他的特殊符号(如$)外还包括空白符）都只占一个字节，汉字以及中文符号都占两个字节

sizeof(s)即字符串所占空间（包括结尾的'\0'）

代码如下：

```c
#include <stdio.h>
#include <string.h>
int main() {
	char* name1 = "张三";
	char name2[] = "zhangsan";
	printf("%zd\n", sizeof("张三"));//5，sizeof()返回值是size_t类型
	printf("%zd\n", sizeof(name1));//4，name1是一个指针类型的变量,所有指针类型都占4个字节，所以不论字符串中内容为何，sizeof(name1)始终为4
	printf("%zd\n", strlen("张三"));//4
	printf("%zd\n", strlen(name1));//4，strlen()始终是计算字符串的长度，而不会去计算name1

	printf("%zd\n", sizeof("zhangsan"));//9
	printf("%zd\n", sizeof(name2));//9
	printf("%zd\n", strlen("zhangsan"));//8
	printf("%zd\n", strlen(name2));//8
	return 0;
}
```

运行结果如下：

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210113122124714-1336883463.png)

> 查看类型定义，如下可以看到，strlen(s)和sizeof(s)一样都是size_t类型，在WIN64系统中，size_t类型是利用typedef给unsigned int类型取的一个别名，本质上还是unsigned int类型，占4个字节

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210113123250302-743491501.png)

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210113121146758-2084078655.png)

# const修饰符

**作用：只想让数据被使用而不能被修改**

代码如下：

```c
#include<stdio.h>

int main() {
	//1.const修饰基本数据类型-->只能读不能改
	//只能在初始化时赋值
	const int number = 10;//<=>int const number=10，两中修饰方法都是相同的
	//不能对const修饰的变量进行修改，若加上 number = 1 则编译不通过
	printf("const修饰基本数据类型：%d\n",number);//10

	//2.const修饰数组：其元素值不能改
	const int array[] = { 10,203,123,4,2,213,513,1,351,34 };//<=>int const array[]= { 10,203,123,4,2,213,513,1,351,34 };
	//array[0]=99;//编译不通过
	printf("const修饰数组：");
	for(int index = 0; index < 10; index++)
	    printf("%d\t",array[index]);

	//3.const修饰指针
	//(1)只能修改地址来改变值（此种修饰指针方式较常用）
	int num1 = 1;
	const int* pointer1 = &num1;//<=> int const *pointer1;
	//可以直接操作变量进行修改
	num1 = 10;
	printf("\nconst修饰指针（1）：%d\t", num1);//200
	//不能通过修改*pointer1去修改其指向变量的值，即若加上 *pointer1=200; 则编译不通过
	//但可修改pointer1的值（即修改其指向变量的地址），如下：
	int num1_1 = 100;
	pointer1 = &num1_1;
	printf("%d\n",*pointer1);//18

	//(2)只能修改值，地址不能改
	int num2 = 2;
	int* const pointer2 = &num2;
	//不能通过修改pointer2的值去修改其指向变量的值，即若加上 pointer2 = &age2; 则编译不通过
	//但可修改*pointer2的值（即修改其指向变量的值）；
	int num2_2 = 20;
	*pointer2 = num2_2;
	printf("const修饰指针（2）：%d\n",*pointer2);
}
```

运行结果如下：

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210113152157819-1668293423.png)

# typedef类型定义

**作用：**

**1. 避免数据类型过长难以记忆和书写，如 “cosnt unsigned long long”、“struct student”，通过类似取别名的方式来简化数据类型的名称**

**2. 通过给一个数据类型取一个特定的别名，使得其为特定的数据服务，方便记忆和理解**

**注意：typedef类型定义一般写在最外面**

代码如下：

```c#include<stdio.h>
//1.
typedef struct {
    char* name;
    int age;
    int score;
} Student;
//2.
typedef enum {
    DirectionEast,//默认值为0
    DirectionWest,//默认值为1
    DirectionSouth,//默认值为2
    DirectionNorth//默认值为3
} Direction;
//3.
typedef const unsigned long long cull;
int main() {
    Student stu = { "ZhangSan",1,100};
    Direction dir0 = DirectionEast;
    Direction dir1 = DirectionWest;
    Direction dir2 = DirectionSouth;
    Direction dir3 = DirectionNorth;
    cull number = 3;
    printf("stu.name:%s\n", stu.name);
    printf("stu.age:%d\n", stu.age);
    printf("stu.score:%d\n", stu.score);

    printf("\nDirectionEast:%d\n", dir0);
    printf("DirectionWest:%d\n", dir1);
    printf("DirectionSouth:%d\n", dir2);
    printf("DirectionNorth:%d\n", dir3);

    printf("\nnumber:%lld\n",number);
}
```

运行结果如下：

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210113154722012-2055039727.png)

# 返回指针的函数

> 函数的返回值可以是局部变量的返回值，但是不能返回局部变量的地址，因为当函数执行完毕后，局部变量的的空间会被回收
>
> 若要返回函数内部定义的指针，则需要将指针变量的存储空间申请在堆区
>
> 堆区的空间使用完之后，最后一定要释放掉

代码如下：

```c
#include<stdio.h>
#include<stdlib.h>
int* test()//返回int类型的指针
{
    int* pointer = calloc(3, sizeof(int));//在堆内存中申请3个int类型大小的空间
//堆内存中申请空间（所用函数均在头文件stdlib.h中）：
//malloc(n)申请n个连续字节使用，并返回第一个字节的地址。不会自动清除垃圾值
//calloc(n,m)申请n个m个字节大的空间，并返回第一个字节的地址，如：calloc(4,sizeof(int))。自动清除垃圾值
//free释放空间
    *pointer = 10;//赋值
    *(pointer + 1) = 20;
    *(pointer + 2) = 30;
    return pointer;
}
int main()
{
    int* pointer = test();
    for (int i = 0; i < 3; i++)
        printf("%d ", pointer[i]);
    free(pointer);//堆内存的空间使用完之后，最后一定要释放掉
}
```

运行结果如下：

![img](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2229104-20210113162445937-1370537476.png)

