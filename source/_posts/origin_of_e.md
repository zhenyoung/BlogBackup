---
title: 自然底数e的由来
date: 2021-02-02 14:56:12
declare: true
tags: 
- doubt
---



与圆周率$\pi$一样，自然底数e是一个常数。然而自从知道e开始，就只记得其大致的值为2.71828182845...，却不知其从何而来，这个数有什么意义。

直到一天我在图书馆无意中翻看到一本关于物理学史的书时，发现上面大致介绍了一下这个常数的由来，特此写一篇博客记录。

<!--more-->

首先，e 这个表示自然底数的符号是由瑞士数学和物理学家Leonhard Euler(莱昂哈德·欧拉)命名的，取的正是Euler的首字母“ ![[公式]](https://www.zhihu.com/equation?tex=e) ”

但实际上，第一个发现这个常数的，并非欧拉本人，而是**雅可比·伯努利**（Jacob Bernoulli）（提出雅各比公式的那位），伯努利家族是17〜18世纪瑞士的一个赫赫有名的家族，其中出了很多著名的数理科学家，雅可比·伯努利是**约翰·伯努利**（Johann Bernoulli）的哥哥，而约翰·伯努利则是欧拉的数学老师。

步入正题。我们知道，很多细菌是通过二分裂进行繁殖的，假设某种细菌1天会分裂1次，也就是 1 个增长周期为1天，这意味着：**每一天，细菌的总数量都是前一天的两倍**。
不难得出：1个细菌分裂$x$天后，细菌总数为$2^x$，那么$K$个细菌分裂$x$天后细菌总数为$Q=K\cdot2^x$

如果将 “**分裂**”或“**翻倍**”换一种更文艺的说法，也可以说是：“**增长率为$100\%$** ”。也就是说，可以将上式写为：$(1+100\%)^x$，然而当增长率不是100%，而是50%、25%之类的时候，则需要将上式的100%更换即可。如此一来，便可得到适用于其他类似增长事物的普适的公式：
$$
Q=(1+r)^x
$$
这个公式的数学内涵是：一个增长周期内的增长率为 $r$ ，在增长了 $x$ 个周期之后，总数也将为初始量的 $Q$ 倍。

以上为指数增长的一个简单实例，下面来看看雅可比·伯努利的发现：

假如你有1元钱存在银行中，而银行的利率飙升到了100%（理想情况，姑且认为是严重的通货膨胀吧），若银行一年付一次利息，则一年后你可以拿到1元的本金和1元的利息，总共2元。

现在银行的年利率不变，但是为了招揽客户，推出每半年就付一次利息（年利率还是100%，只不过一半时间内付一半的利息）的政策，那么在六个月后，你就能拿到1元的本金和0.5元的利息，总共1.5元，若不取出，而是继续存入银行中产生利息（俗称利滚利，专业术语称**复利**），那么再过六个月，存款将为2.25元。可用如下公式模拟：
$$
Q=(1+\frac{100\%}{2})^2
$$
继续，假设现在银行为了和其他银行抢生意，短期不想赚钱了，每四个月就付一次利息！而机智的你依然不取出而是继续存，与半年结算一次利息类似：即，每个结算周期为四个月，每四个月的利率是$\frac{100\%}{3}$，用如下公式模拟：
$$
Q=(1+\frac{100\%}{3})^3\approx2.37037
$$
不难发现，年利率虽然没变，但是随着每年利息交付次数的增加（按照时间每隔一段时间就付之以相对应时间占比的利率，如半年50%，四个月33.33%，三个月25%等），能从银行拿到的钱也在增加。随着交付次数的不断增加，当其趋于无穷时（即相当于每时每刻都在交付利息），经过不断计算发现，其最终的值趋于一个常数2.71828182845...，将其用字母 e 来定义，即得以下极限
$$
e=\lim_{n \to \infty}(1+\frac{1}{n})^n\\
此处的\infty默认为+\infty
$$
然而，实际上银行的利率永远也不会超过100%（银行不做慈善），此外，有些事物的增长率是超过100%甚至是远超的。若将100%用变量x代替，便可得到满足所有自然增长事物的增长规律。以下是推导过程：
$$
e=\lim_{n \to \infty}(1+\frac{1}{n})^n=\lim_{n \to \infty}(1+\frac{1}{\frac{n}{x}})^\frac{n}{x}=\lim_{n \to \infty}(1+\frac{x}{n})^\frac{n}{x}\\
不难发现，e^x=\lim_{n \to \infty}((1+\frac{x}{n})^\frac{n}{x})^x\\
\qquad\qquad\ \ \ =\lim_{n \to \infty}(1+\frac{x}{n})^n
$$
由此便将式中的100%用 x 代替，便可表征所有自然增长的规律（ x代表增长率，既可能大于1，也可能小于1，甚至可能小于0（亏损、减少））

有了自然之数，便有了其他底数为底的指数函数
