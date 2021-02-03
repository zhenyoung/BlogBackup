---
title: Typora插入公式
date: 2021-02-02 14:46:31
declare: true
tags:
- Typora
- LaTex
---



Typora中插入公式是基于LaTex排班系统的。关于LaTex，因为并不是所有的人都懂得专业的书籍及论文的排版，而这些排版的知识的学习成本极高。LaTex相较其而言，学习成本较低，可以让一些排版和程序设计的知识也可以能在几天、甚至几小时内生成很多具有书籍质量的印刷品。

对于生成复杂表格和数学公式，这一点表现得尤为突出。许多的公式编辑器也陆续支持LaTex，用途十分广泛。

关于LaTex的具体介绍，[详见百科](https://baike.baidu.com/item/LaTeX/1212106?fr=aladdin)。以下介绍常用的公式排版，详细的全部公式排版见[LaTex帮助文档](https://latexlive.com/help)。关于书籍以及论文的排版此处不讨论。

<!--more-->

以下所有的公式都是基于	![image-20210203212848586](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210203212848586.png)	或者	![image-20210203212858506](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210203212858506.png)	的形式，因为Markdown语法中插入公式就是通过`美元符$`来实现的

# 公式中的转义字符’\‘

转义字符，和编程语言一样，是用来通过一些易记忆的命令来使得其能够展示符号效果

## 1.一些常见的符号


|          命令          |                             显示                             |         命令         |            显示            |  命令   |                             显示                             |
| :--------------------: | :----------------------------------------------------------: | :------------------: | :------------------------: | :-----: | :----------------------------------------------------------: |
|         \space         |                             空格                             |         \sum         |           $\sum$           | \oiint  | ![image-20210203205118408](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210203205118408.png) |
|          \\\           |                             换行                             |        \prod         |          $\prod$           | \oiiint | ![image-20210203205137688](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210203205137688.png) |
|     \and,\or,\not      | ![image-20210203210252892](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210203210252892.png) |       \partial       |         $\partial$         |   \%    |                             $\%$                             |
|         \exist         | ![image-20210203205930278](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210203205930278.png) |        \rm{d}        |          $\rm{d}$          | \approx |                          $\approx$                           |
|          \to           |                            $\to$                             | a,b,\rm{a},\rm{b}··· | $a,b,\rm{a},\rm{b},\cdots$ |  \leq   |                            $\leq$                            |
|          \neq          |                            $\neq$                            |        \nabla        |          $\nabla$          |  \geq   |                            $\geq$                            |
| \infty,\\+infty,\infty |                   $\infty,+\infty,-\infty$                   |        \Delta        |          $\Delta$          |  \cdot  |                           $\cdot$                            |
|          \lim          |                            $\lim$                            |      \triangle       |        $\triangle$         | \times  |                           $\times$                           |
|          \max          |                            $\max$                            |  \int,\iint,\iiint   |    $\int,\iint,\iiint$     |  \div   |                            $\div$                            |
|          \min          |                            $\min$                            |        \oint         |          $\oint$           |  \exp   |                            $\exp$                            |
|      \overline{Q}      |                        $\overline{Q}$                        |        \dots         |          $\dots$           |         |                                                              |
|     \underline{Q}      |                       $\underline{Q}$                        |        \cdots        |          $\cdots$          |         |                                                              |
|                        |                                                              |                      |                            |         |                                                              |
|                        |                                                              |                      |                            |         |                                                              |
|                        |                                                              |                      |                            |         |                                                              |

此处只是列举一些符号，常用的公式符号下面一一展开。并且由于渲染引擎的问题，本文中一些公式使用了截图来显示效果。

## 2.希腊字母

\字母发音，如下
$$
\alpha,\beta,\gamma
$$
附上一张希腊字母表，如下：


| 序号 | 小写 | LaTeX       | 读音                   | 序号 | 大写 | LaTeX    | 读音        |
| :--: | :--: | :---------- | :--------------------- | :--: | :--: | :------- | :---------- |
|  1   |  α   | \alpha      | /ˈælfə/                |  31  |  Γ   | \Gamma   | /ˈɡæmə/     |
|  2   |  β   | \beta       | /ˈbiːtə/, US: /ˈbeɪtə/ |  32  |  Δ   | \Delta   | /ˈdɛltə/    |
|  3   |  γ   | \gamma      | /ˈɡæmə/                |  33  |  Θ   | \Theta   | /ˈθiːtə/    |
|  4   |  δ   | \delta      | /ˈdɛltə/               |  34  |  Λ   | \Lambda  | /ˈlæmdə/    |
|  5   |  ϵ   | \epsilon    | /ˈɛpsɪlɒn/             |  35  |  Ξ   | \Xi      | /zaɪ, ksaɪ/ |
|  6   |  ε   | \varepsilon | /ˈɛpsɪlɒn/             |  36  |  Π   | \Pi      | /paɪ/       |
|  7   |  ζ   | \zeta       | /ˈzeɪtə/               |  37  |  Σ   | \Sigma   | /ˈsɪɡmə/    |
|  8   |  η   | \eta        | /ˈeɪtə/                |  38  |  Υ   | \Upsilon | /ˈʌpsɪlɒn/  |
|  9   |  θ   | \theta      | /ˈθiːtə/               |  39  |  Φ   | \Phi     | /faɪ/       |
|  10  |  ϑ   | \vartheta   | /ˈθiːtə/               |  40  |  Ψ   | \Psi     | /psaɪ/      |
|  11  |  ι   | \iota       | /aɪˈoʊtə/              |  41  |  Ω   | \Omega   | /oʊˈmeɪɡə/  |
|  12  |  κ   | \kappa      | /ˈkæpə/                |      |      |          |             |
|  13  |  λ   | \lambda     | /ˈlæmdə/               |      |      |          |             |
|  14  |  μ   | \mu         | /mjuː/                 |      |      |          |             |
|  15  |  ν   | \nu         | /njuː/                 |      |      |          |             |
|  16  |  ξ   | \xi         | /zaɪ, ksaɪ/            |      |      |          |             |
|  17  |  o   | o           | /ˈɒmɪkrɒn/             |      |      |          |             |
|  18  |  π   | \pi         | /paɪ/                  |      |      |          |             |
|  19  |  ϖ   | \varpi      | /paɪ/                  |      |      |          |             |
|  20  |  ρ   | \rho        | /roʊ/                  |      |      |          |             |
|  21  |  ϱ   | \varrho     | /roʊ/                  |      |      |          |             |
|  22  |  σ   | \sigma      | /ˈsɪɡmə/               |      |      |          |             |
|  23  |  ς   | \varsigma   | /ˈsɪɡmə/               |      |      |          |             |
|  24  |  τ   | \tau        | /taʊ, tɔː/             |      |      |          |             |
|  25  |  υ   | \upsilon    | /ˈʌpsɪlɒn/             |      |      |          |             |
|  26  |  ϕ   | \phi        | /faɪ/                  |      |      |          |             |
|  27  |  φ   | \varphi     | /faɪ/                  |      |      |          |             |
|  28  |  χ   | \chi        | /kaɪ/                  |      |      |          |             |
|  29  |  ψ   | \psi        | /psaɪ/                 |      |      |          |             |
|  30  |  ω   | \omega      | /oʊˈmeɪɡə/             |      |      |          |             |

# 运算

## 1.根号

格式：`\sqrt3`，如：$\sqrt3$；若开多次方：\sqrt[5]3，如：$\sqrt[5]3$

## 2.分式

`frac{3x}{2y}`，如：$\frac{3x}{2}$

## 3.上标和下标

此处以右上下标为例，正上下标到下一标题中的极限中统一讨论

右上标：`x^t`，如：$x^t$；右下标：`x_i`，如：$x_i$

当上下标多于一个字母或符号时，需要用{}将其括起来，即：`x^{\alpha t},x_{i1}`，如：$x^{\alpha t},x_{i1}$

上下标组合：`a_1^2 + a_2^2 = a_3^2`，如：$ a_1^2 + a_2^2 = a_3^2 $

## 4.极限

1.插入行间公式：

${\lim_{x \to 0^+}}$

2.插入块间公式：
$$
{\lim_{x \to 0^+}}
$$

3.上述插入的行间公式和块间公式是一模一样的。但是由上述区别可以看出，在Typora中，若插入行间公式，则上下标显示在右下角和右上角；若插入块间公式，则上下标显示在正下方和正上方

4.若要移动行间和快件公式的上下标的位置，则在该字符 lim 与下标符 _ 中间添加： 

- 若要将行间公式的上下标强制移动到上下方（一般用于在行间公式中显示上下标），则添加`\limits`，如下

  ​	$\lim\limits_{x \to 0^+}$

- 若要将块间公式的上下标强制移动到右上下放，则添加 `\nolimits`（一般用于在行块间公式中显示右上下标），如下：

$$
{\lim \nolimits_{x \to 0^+}}
$$

5.对于数学符号，要添加上下标，直接操作即可；对于非数学符号的普通符号如Math，若要对其添加上下标（一般是下标）则需要利用`\mathop{Math}`先将其转化为数学符号，再进行添加下标的操作：$\mathop{Math} \limits_{a \to \infty}$

6.几个经典极限如下
$$
{\lim_{x \to 0}\frac{sinx}{x}=1}\\
{\lim_{x \to \infty}(1+\frac{1}{x})^x=e}\\
{\lim_{x \to 0}(1 + x)^{\frac{1}{x}}=e}\\
$$

## 5.积分

格式：`\int_1^{+ \infty}`，如：$\int_1^{+ \infty}$

多重积分：`\iiint_1^{n}`，如：$\iiint_1^{n}$

闭合曲线积分：`\oint \limits_C`，如：$\oint \limits_C$

多重闭合曲积分：`\oiiint \limits_{l}`，如：![image-20210203214856817](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210203214856817.png)

## 6.方程组、行列式、矩阵

$$
方程组：
\left\{
	\begin{array}{}
		a_1x+b_1y+c_1z=d_1\\
		a_2x+b_2y+c_2z=d_2\\
		a_3x+b_3y+c_3z=d_3
	\end{array}
\right.
\\
行列式：
\begin{vmatrix}
    1 &    2    & 3\\ 
    4 &    5    & 6\\ 
    7 &    8    & 9
\end{vmatrix}\\
矩阵：
\begin{matrix} {}
    1 &    2    & 3\\ 
    4 &    5    & 6\\ 
    7 &    8    & 9
\end{matrix}
\ or 
\begin{bmatrix} {}
    1 &    2    & 3\\ 
    4 &    5    & 6\\ 
    7 &    8    & 9
\end{bmatrix}
\ or 
\left(
\begin{array}{}
    1 &    2    & 3\\ 
    4 &    5    & 6\\ 
    7 &    8    & 9
\end{array}
\right)
$$

# 几个重要的公式

## 1.双曲函数

$$
双曲函数
\begin{cases}
双曲正弦函数：\sinh x = \frac{e^x - e^{-x}}{2}\\
双曲余弦函数：\cosh x = \frac{e^x + e^{-x}}{2}
\end{cases}，
满足：\cosh^2 x - \sinh^2 x =1
$$

## 2.欧拉公式

$$
欧拉公式
\begin{cases}
e^{ix} = \cos x + i\sin x \\
\sin x = \frac{e^{ix}-e^{-ix}}{2i}\\
\cos x = \frac{e^{ix}+e^{-ix}}{2}\\
\end{cases}\\
对比上述双曲函数，不难发现，在复数域，满足
\begin{cases}
\sin ix = -i\sinh x\\
\cos ix = \cosh x
\end{cases}
$$

## 3.积化和差、和差化积

$$
积化和差公式
\begin{cases}
\sin x \cos y = \frac{1}{2}[\sin(x+y)+\sin(x-y)]\\
\cos x \cos y = \frac{1}{2}[\cos(x+y)+\cos(x-y)]\\
\sin x \sin y = \frac{1}{2}[\cos(x-y)-\cos(x+y)]
\end{cases}
$$

$$
和差化积公式
\begin{cases}
\sin x \pm \sin y = 2\sin\frac{x \pm y}{2} \cos\frac{x \mp y}{2}\\
\cos x + \cos y = 2\cos\frac{x + y}{2} \cos\frac{x - y}{2}\\
\cos x - \cos y = -2\sin\frac{x + y}{2} \sin\frac{x - y}{2}
\end{cases}
$$

## 4.正切函数

$$
\begin{cases}
\tan(x\pm y) = \frac{\tan x\pm\tan y}{1\mp\tan x\tan y}\\
\tan 2x = \frac{2\tan x}{1- \tan^2x}\\
\tan^2\frac{x}{2} = \frac{1-\cos x}{1+\cos x}
\end{cases}
$$



## 5.万能公式

$$
万能公式
\begin{cases}
\sin x = \frac{2\tan x}{1-\tan^2 x}\\
\cos x = \frac{1- \tan^2 \frac{x}{2}}{1+\tan^2 \frac{x}{2}}\\
\tan x = \frac{2\tan\frac{x}{2}}{1-\tan^2\frac{x}{2}}
\end{cases}
$$

## 6.三倍角公式

$$
三倍角公式
\begin{cases}
\sin 3x = 3\sin x - 4\sin^3 x\\
\cos 3x = 4\cos^3 x - 3\cos x
\end{cases}
$$
