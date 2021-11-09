---
title: Perceptron
date: 2021-09-18 10:53:13
mathjax: true
tags:
- least sqaure
- he1o
---
# 感知机

感知机（英语：Perceptron）是弗兰克·罗森布拉特（Frank Rosenblatt）在1957年就职于康奈尔航空实验室（Cornell Aeronautical Laboratory）时所发明的一种人工神经网络。在人工神经网络领域中，感知机也被指为单层的人工神经网络，以区别于较复杂的多层感知机（Multilayer Perceptron）。

感知机作为一种二分分类的线性分类模型，其输入为实例的特征向量，输出为实例的类别，取+1或-1二值。感知机学习旨在求出将训练数据进行线性划分的分离超平面，因此，导入基于误分类的损失函数，利用梯度下降法对损失函数进行极小化，求得感知机模型。（单层）感知机可说是最简单的前向人工神经网络形式。尽管结构简单，感知机能够学习并解决相当复杂的问题。感知机主要的本质缺陷是它不能处理线性不可分问题。

感知机是生物神经细胞的简单抽象。神经细胞结构大致可分为：树突、突触、细胞体及轴突。单个神经细胞可被视为一种只有两种状态的机器——激活时为‘是’，而未激活时为‘否’。神经细胞的状态取决于从其它的神经细胞收到的输入信号量，及突触的强度（抑制或加强）。当信号量总和超过了某个阈值时，细胞体就会激活，产生电脉冲。电脉冲沿着轴突并通过突触传递到其它神经元。为了模拟神经细胞行为，与之对应的感知机基础概念被提出，如权量（突触）、偏置（阈值）及激活函数（细胞体）。

## 1、历史背景

1943年，心理学家沃伦·麦卡洛克和数理逻辑学家沃尔特·皮茨在合作的《A logical calculus of the ideas immanent in nervous activity》[1]论文中提出并给出了人工神经网络的概念及人工神经元的数学模型，从而开创了人工神经网络研究的时代。

1949年，心理学家唐纳德·赫布在《The Organization of Behavior》[2]论文中描述了神经元学习法则——赫布型学习。

人工神经网络更进一步被美国神经学家弗兰克·罗森布拉特所发展。他提出了可以模拟人类感知能力的机器，并称之为‘感知机’。1957年，在Cornell航空实验室中，他成功在IBM 704机上完成了感知机的仿真。两年后，他又成功实现了能够识别一些英文字母、基于感知机的神经计算机——Mark1，并于1960年6月23日，展示与众。

为了‘教导’感知机识别图像，弗兰克·罗森布拉特在Hebb学习法则的基础上，发展了一种迭代、试错、类似于人类学习过程的学习算法——感知机学习。除了能够识别出现较多次的字母，感知机也能对不同书写方式的字母图像进行概括和归纳。但是，由于本身的局限，感知机除了那些包含在训练集里的图像以外，不能对受干扰（半遮蔽、不同大小、平移、旋转）的字母图像进行可靠的识别。

首个有关感知机的成果，由弗兰克·罗森布拉特于1958年发表在《The Perceptron: A Probabilistic Model for Information Storage and Organization in the Brain》的文章里。1962年，他又出版了《Principles of Neurodynamics: Perceptrons and the theory of brain mechanisms》一书，向大众深入解释感知机的理论知识及背景假设。此书介绍了一些重要的概念及定理证明，例如感知机收敛定理。

虽然最初被认为有着良好的发展潜能，但感知机最终被证明不能处理诸多的模式识别问题。1969年，马文·明斯基和西摩尔·派普特在《Perceptrons》书中，仔细分析了以感知机为代表的单层神经网络系统的功能及局限，证明感知机不能解决简单的异或（XOR）等线性不可分问题，但弗兰克·罗森布拉特和马文·明斯基和西摩尔·派普特等人在当时已经了解到多层神经网络能够解决线性不可分的问题。

由于弗兰克·罗森布拉特等人没能够及时推广感知机学习算法到多层神经网络上，又由于《Perceptrons》在研究领域中的巨大影响，及人们对书中论点的误解，造成了人工神经领域发展的长年停滞及低潮，直到人们认识到多层感知机没有单层感知机固有的缺陷及反向传播算法在80年代的提出，才有所恢复。1987年，书中的错误得到了校正，并更名再版为《Perceptrons - Expanded Edition》。

近年，在Freund及Schapire（1998）使用核技巧改进感知机学习算法之后，愈来愈多的人对感知机学习算法产生兴趣。后来的研究表明除了二元分类，感知机也能应用在较复杂、被称为structured learning类型的任务上（Collins, 2002），又或使用在分布式计算环境中的大规模机器学习问题上（McDonald, Hall and Mann, 2011）。

## 2、感知机模型

假设输入空间（特征空间）是 ${\displaystyle X\subseteq R^n}$ （代表n维的实数空间），输出空间是 $Y=\{+1, -1\}$ 。输入 $\mathbf x\in X$ 表示实例的特征向量，对应于输入空间（特征空间）的点；输出 $\mathbf y\in Y$ 表示实例的类别。把矩阵上的输入 $x$ 映射到输出值$f(x)$上。

$$
{\displaystyle f(x)=\text{sign}(\mathbf w\cdot \mathbf x+b)}
$$



$\mathbf w$ 是实数的表示权重的向量，与 $\mathbf x$ 维度相同，$\mathbf {w\cdot x}$ 是点积，$b$ 是偏置，一个不依赖于任何输入值的常数。偏置可以认为是激励函数的偏移量，或者给神经元一个基础活跃等级。sign是符号函数：

$${\displaystyle 
\text{sign}(n)={
    \begin{cases}
        +1&n\geq 0\\
        -1&n<0
    \end{cases}
    }
}
$$

映射函数同样可以写成如下的表述形式：
$$
{\displaystyle y=\text{sign}(\sum_{i=1}^{n}{ {w}_{i}{x}_{i}+b})=\text{sign}( {W}^{T} {X})}
$$

## 3、感知机学习算法

假设训练数据是线性可分的，感知机的学习目标是寻找模型参数$w,b$来将数据集正负实例点通过超平面进行区分，因此需要一个损失函数并得到损失函数的极小值。

> 我们很自然的想到能否还用最小二乘法中的损失函数呢？
> $$Q=min{||\text{sign}(\mathbf w\cdot \mathbf x+b)-y||}^2$$
> 感知机与最小二乘法的不同之处在于 $y$ 即映射函数 $f(x)$ 的不同。最小二乘法是线性函数，用于线性回归；而感知机是sign函数，用于分类。很明显sign是个阶跃的不连续函数，这就导致损失函数同样是不连续的，就无法通过微分来得到极值点。

>为了减少输入，以下还是用不加粗的字母 $w$ 取代向量 $\mathbf w$。

损失函数还有一个自然选择是误分类点的总数，但同样这种损失函数也不是参数 $w,b$ 的连续可导函数。损失函数的另一个选择是误分类点到超平面的距离，通过距离公式可以得到任一点 $x_0$ 到超平面 $S$ 的距离：

$$\frac{1}{\left\|w\right\|}|w\cdot x_0+b|$$

> 在一维空间，一个线性函数如 $Ax+By+C=0$ 的法向量就是 $(A,B)$，点到直线距离相当于该点到法向量投影的长度，假设点 $Q$ 坐标 $(x_0,y_0)$，直线上任意一点坐标 $P(x,y)$
> $$d=|PQ|\cdot \cos\theta$$
> $$d=\frac{|n|\cdot|PQ|\cdot \cos\theta}{|n|}$$
> $$d=\frac{\vec{n}\cdot \vec{PQ}}{|n|}$$
> 同理可以推广到多维空间
> 
> **记住一点：**
>
> **权重向量是超平面的法线**

对于误分类的数据$(x_i,y_i)$，当$w\cdot x_i+b>0$，$y_i=-1$；反之，$y_i=+1$，因此任一点$x_i$到超平面$S$的距离是
$$-\frac{1}{\left\|w\right\|}y_i(w\cdot x_i+b)$$
不考虑$\displaystyle \frac{1}{\left\|w\right\|}$， 感知机学习的损失函数定义为
$$L(w,b)=-\sum_{x_i\in M}y_i(w\cdot x_i+b)$$
$M$ 是误分类点的集合。

显然，损失函数是非负的。如果没有误分类点，损失函数值是0。而且，误分类点越少，误分类点离超平面越近，损失函数值就越小。注意，在分类正确时，损失函数为0。因此，给定训练数据$T$，损失函数$L(w,b)$ 是$w,b$ 的连续可导函数。

感知机学习算法采用随机梯度下降法。首先选取一个超平面$w_0,b_0$，然后用梯度下降法不断地极小化目标函数。极小化过程不是一次使$M$中所有误分类点的梯度下降，而是一次随机选取一个误分类点使其梯度下降。

损失函数 $L(w,b)$ 的梯度：
$$\bigtriangledown_w L(w,b)=-\sum_{x_i\in M}y_ix_i$$
$$\bigtriangledown_b L(w,b)=-\sum_{x_i\in M}y_i$$
随机选取一个误分类点$(x_i,y_i)$，对 $w,b$ 进行更新：
$$w_{t+1}\leftarrow w_{t}+ \eta y_ix_i$$
$$b_{t+1}\leftarrow b_{t}+ \eta y_i$$
式中$\eta$是步长，在统计学习中称为学习率。通过迭代可以期待损失函数不断减少。

为了便于推导，可以将偏置 $b$ 并入权重向量 $w$，将 $d$ 维的输入转为 $(d+1)$ 维的输入，同时传入到对应的 $(d+1)$ 维感知机当中。
$$w\cdot x+b=[w,b]\cdot [x,1]=\mathbf w\cdot \mathbf x$$ 

总结算法流程如下:
1. 初始化参数，迭代次数$t=1$并且$\mathbf w_1$为全是0的权重向量。
2. 对每一个样本 $\mathbf x_t$ 预测，$f(x_t)=+1$ if $\mathbf w_t\cdot \mathbf x_t\ge 0$ else $-1$
3. 对一个分类错误的样本 $y_i(\mathbf w_t \cdot \mathbf x_i) \le 0$ 进行学习，$\mathbf w_{t+1}\leftarrow \mathbf w_{t}+ \eta y_i\mathbf x_i$ 
4. $t\leftarrow t + 1$

## 4、算法收敛性
在证明感知机算法收敛性之前，先证明两个假设。

**定理1(线性可分性).** 对于线性可分的数据集，存在 $\mathbf w^*$ 满足 $\left\|\mathbf w^* \right\|=1$ ,使得超平面 $\mathbf w^* \cdot \mathbf x=0$ 能够将所有训练数据完全正确分开，且存在 $\gamma > 0$，对于所有 $i\in \{1,2,...,n\}$，
$$y_i(\mathbf w^* \cdot \mathbf x_i) > \gamma$$
证明：由于训练数据集是线性可分的，则存在超平面将数据集完全分开，取此超平面为 $\mathbf w^* \cdot \mathbf x=0$，通过向量单位化使 $\left\|\mathbf w^* \right\|=1$ 。由于对于有限的数据集 $i\in \{1,2,...,n\}$，均有
$$y_i(\mathbf w^* \cdot \mathbf x_i) > 0$$
所以存在
$$y_i(\mathbf w^* \cdot \mathbf x_i) \ge \min_i(y_i(\mathbf w^* \cdot \mathbf x_i)) > \gamma$$
**定理2(有界性).** 存在 ${R \in R^n}$ 对于有限的数据集 $i\in \{1,2,...,n\}$，均有
$$\left\|\mathbf x_i \right\| \le R$$
**定理3(收敛性).** 感知机学习算法最多迭代次数（之后得到一个分离超平面），满足不等式：
$$k\le \left( \frac{R}{\gamma}\right) ^2$$
证明：我们需要推导出 $k$ 的上边界是上式，策略是根据 $k$ 推导出 $\mathbf w_{k+1}$ 长度的上下限并将它们关联起来。

注意到 $\mathbf w_{1}=0$，对于 $k\ge1$ ，如果 $\mathbf{x}_j$ 是迭代 $k$ 期间的误分类点，由定理1，我们有:
$$
\begin{aligned}
    \mathbf w_{k+1} \cdot \mathbf{w}^*&=(\mathbf{w}_k + \eta y_j\mathbf{x}_j)\cdot \mathbf{w}^* \\
    &=\mathbf w_{k} \cdot \mathbf{w}^* + \eta y_j(\mathbf{x}_j \cdot \mathbf{w}^*) \\
    &>\mathbf w_{k} \cdot \mathbf{w}^* + \eta \gamma \\
    &>\mathbf w_{k-1} \cdot \mathbf{w}^* + 2\eta \gamma \\
    &>k\eta \gamma
\end{aligned}
$$
由于
$$
\begin{aligned}
\mathbf w_{k+1} \cdot \mathbf{w}^* 
&= \left\|\mathbf w_{k+1} \right\|\left\|\mathbf w^* \right\| \cos \theta \\
&\le \left\|\mathbf w_{k+1} \right\| \left\|\mathbf w^* \right\| 
= \left\|\mathbf w_{k+1} \right\|
\end{aligned}
$$
我们有：
$$\left\|\mathbf w_{k+1} \right\| >k\eta \gamma$$
至此我们得到了$\left\|\mathbf w_{k+1} \right\|$的下界，为了得到上界，我们推断：
$$
\begin{aligned}
\left\|\mathbf w_{k+1} \right\|^2 
&=\left\|\mathbf w_{k}+\eta y_j\mathbf{x}_j \right\|^2 \\
&=\left\|\mathbf w_{k}\right\|^2 + \left\| \eta y_j\mathbf{x}_j \right\|^2 + 2(\mathbf w_{k}\cdot \mathbf x_{j})\eta y_j \\
&=\left\|\mathbf w_{k}\right\|^2 + \left\| \eta \mathbf{x}_j \right\|^2 + 2(\mathbf w_{k}\cdot \mathbf x_{j})\eta y_j \\
&\le \left\|\mathbf w_{k}\right\|^2 + \left\| \eta \mathbf{x}_j \right\|^2 \\
&\le \left\|\mathbf w_{k}\right\|^2 + \eta ^2R^2 \\
&\le \left\|\mathbf w_{k-1}\right\|^2 + 2\eta ^2R^2 \\
&\le k\eta ^2R^2 \\
\end{aligned}
$$
联立$\left\|\mathbf w_{k+1} \right\|$的上下界，我们得到不等式：
$$(k\eta \gamma)^2
<\left\|\mathbf w_{k+1} \right\|
\le k\eta ^2R^2$$
最终得到：
$$k\le \left( \frac{R}{\gamma}\right) ^2$$
Our proof is done!


[1. 感知器-维基百科](https://zh.wikipedia.org/wiki/%E6%84%9F%E7%9F%A5%E5%99%A8)
[2. 点到平面的距离公式](https://www.cnblogs.com/graphics/archive/2010/07/10/1774809.html)

