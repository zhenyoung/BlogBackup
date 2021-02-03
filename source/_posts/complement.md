---
title: 码制的一些问题
date: 2021-02-02 14:57:31
declare: true
tag: 
- doubt
---



以前上课的时候，经常听见老师将补码的问题，很多门课的老师也会反复说码制之间的转换。但是，+0和-0的问题只是一笔带过。平时也很少遇到这种问题，而我自己又懒，就没有深究。现在想来，懒真的才是万恶之源。最近有空，便仔细想了这个问题，百度之后了解了这个问题。顺便把补码的几种求解方法列举了下来。特此，写篇博客记录下来。

<!--more-->

# +0和-0的问题

当使用8位二进制来表示-128~127时，

![image-20210202232615462](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210202232615462.png)

不难发现，+0和-0的补码是相同的，即2个补码表示同一个数 "0"，因此若不作相应的规定，那么8位补码所能表示的数只有-127\~127共255个（注：8位原码范围：-127~-0, +0~127；8位反码范围：同左），而8位本应该能表示256个数，为此，便做了如下规定：

**规定：1000 0000（作为补码）表示-128，且-128仅有补码（1000 0000）而没有对应的反码、原码，因此不能根据-128的补码去反推其原码和反码**

# 求解补码的方法

1.口诀：符号位不变，各位取反，末位加1（有进位则依次进位）

2.将最高位的1和最低位的1之间的数取反，其余不变                 注：若只有一个1，则按照方法1或方法3来

![image-20210202232645268](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210202232645268.png)

3.按照补码的定义，负数的补码，定义如下：

​	![image-20210202232730990](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210202232730990.png)