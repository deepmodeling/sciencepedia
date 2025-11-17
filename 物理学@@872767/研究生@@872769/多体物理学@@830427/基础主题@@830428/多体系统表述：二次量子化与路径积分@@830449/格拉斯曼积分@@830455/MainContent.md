## 引言
格拉斯曼积分是现代[多体物理学](@entry_id:144526)和[量子场论](@entry_id:138177)中不可或缺的数学工具。当试图将路径积分的思想从[玻色子](@entry_id:138266)推广到[费米子](@entry_id:146235)时，物理学家面临一个根本性难题：如何处理描述[费米子](@entry_id:146235)的、满足[泡利不相容原理](@entry_id:141850)的[反对易](@entry_id:186708)变量。常规的[数值积分方法](@entry_id:141406)在此失效，为解决这一知识鸿沟，格拉斯曼积分应运而生，它为[费米子](@entry_id:146235)系统提供了一套自洽且强大的非微扰计算框架。

本文旨在系统地介绍格拉斯曼积分的理论与实践。通过学习，读者将能够掌握处理[费米子](@entry_id:146235)自由度的核心技术，并理解其在理论物理前沿研究中的广泛应用。文章将分三部分展开：首先，在“原理与机制”一章中，我们将从[格拉斯曼变量](@entry_id:199573)的反对易代数出发，建立起[别列津积分](@entry_id:192484)的规则，并推导至关重要的高斯积分公式与[Wick定理](@entry_id:137086)。接着，在“应用与跨学科联系”一章中，我们将展示这些数学工具如何在凝聚态物理、[高能物理](@entry_id:181260)乃至线性代数等领域解决实际问题，例如描述超导的BCS理论和处理相互作用系统。最后，“动手实践”部分将提供一系列精心设计的练习，帮助读者将理论知识转化为解决问题的能力。

让我们从格拉斯曼积分的基本原理开始，一步步揭开这个描述费米世界的优雅数学语言的神秘面纱。

## 原理与机制

在本章中，我们将深入探讨格拉斯曼积分的原理与机制。作为[费米子](@entry_id:146235)路径积分形式的核心数学工具，格拉斯曼积分提供了一种优雅而强大的方法来处理由反对易变量描述的量子系统。我们将从格拉斯曼代数的基本规则出发，系统地建立起一套积分微积分体系，并展示如何运用它来计算物理系统的[配分函数](@entry_id:193625)和关联函数。本章的重点在于理解其核心公式的来源，并掌握在处理[相互作用费米子](@entry_id:160994)系统时所需的关键技术。

### [格拉斯曼变量](@entry_id:199573)的代数与微积分

[格拉斯曼变量](@entry_id:199573)（或称[格拉斯曼数](@entry_id:136855)）是构成一个代数的数学对象，其定义核心在于它们之间的[反对易关系](@entry_id:153815)。理解这些基本属性是掌握其积分方法的第一步。

#### 基本的[反对易关系](@entry_id:153815)

一组[格拉斯曼变量](@entry_id:199573) $\theta_1, \theta_2, \dots, \theta_N$ 由以下核心代数规则定义：
$$
\theta_i \theta_j = - \theta_j \theta_i
$$
对于任意 $i, j$。这个规则意味着交换任意两个不同的[格拉斯曼变量](@entry_id:199573)的顺序会引入一个负号。

该规则的一个直接且至关重要的推论是任何[格拉斯曼变量](@entry_id:199573)的平方均为零，这一性质被称为**[幂零性](@entry_id:147926)（nilpotency）**。当 $i = j$ 时，[反对易关系](@entry_id:153815)变为 $\theta_i \theta_i = - \theta_i \theta_i$，这唯一可能的解是：
$$
\theta_i^2 = 0
$$
[幂零性](@entry_id:147926)极大地简化了[格拉斯曼变量](@entry_id:199573)的函数。任何关于单个[格拉斯曼变量](@entry_id:199573) $\theta$ 的函数 $f(\theta)$，其[泰勒级数展开](@entry_id:138468)最多只有两项，因为所有高于一次幂的项都为零：
$$
f(\theta) = f(0) + f'(0) \theta
$$
对于包含多个变量的函数，其多项式展开的最高次数也受到变量总数的限制。一旦任何变量在乘积中出现超过一次，该项即为零。

#### [别列津积分](@entry_id:192484)

对[格拉斯曼变量](@entry_id:199573)的积分，即**[别列津积分](@entry_id:192484)（Berezin integration）**，并非传统意义上的几何求积，而是一种纯粹的代数操作。对于单个[格拉斯曼变量](@entry_id:199573) $\theta$，积分由以下两条线性规则定义：
$$
\int d\theta = 0, \quad \int d\theta \, \theta = 1
$$
其中[微分](@entry_id:158718)符号 $d\theta$ 本身也被视为一个格拉斯曼量，它与所有其他[格拉斯曼变量](@entry_id:199573)（包括 $\theta$ 本身）是[反对易](@entry_id:186708)的：$d\theta \, \theta = - \theta \, d\theta$。

当处理多个变量的积[分时](@entry_id:274419)，例如 $\int d\theta_1 d\theta_2 \dots d\theta_N$，积分是逐次进行的。一个关键的约定是积分的执行顺序由内向外。例如，$\int d\theta_1 d\theta_2 f(\theta_1, \theta_2)$ 表示先对 $\theta_2$ 积分，再对 $\theta_1$ 积分。

一个[多变量积分](@entry_id:139873)要想得到非零结果，被积函数必须包含每一个积分变量恰好一次。根据标准约定，以下积分被归一化为1：
$$
\int d\theta_1 d\theta_2 \cdots d\theta_N \, \theta_N \theta_{N-1} \cdots \theta_1 = 1
$$
这意味着，为了得到结果1，被积函数中变量的顺序必须与[微分](@entry_id:158718)符号的顺序正好相反。任何其他的[排列](@entry_id:136432)顺序将导致一个由[排列](@entry_id:136432)的奇偶性决定的符号因子。

例如，考虑计算积分 $I = \int d\theta_1 d\theta_2 d\theta_3 d\theta_4 \, \theta_1 \theta_2 \theta_3 \theta_4$ [@problem_id:1146532]。这里的规范（canonical）顺序是 $\theta_4 \theta_3 \theta_2 \theta_1$。我们需要通过交换将 $\theta_1 \theta_2 \theta_3 \theta_4$ 转换为标准顺序。将一个包含 $N$ 个元素的序列完全颠倒，需要进行 $\frac{N(N-1)}{2}$ 次相邻交换。对于 $N=4$，这需要 $\frac{4(3)}{2} = 6$ 次交换。因此，$\theta_1 \theta_2 \theta_3 \theta_4 = (-1)^6 \theta_4 \theta_3 \theta_2 \theta_1 = \theta_4 \theta_3 \theta_2 \theta_1$。所以，该积分的值为 $1$。

在多体物理中，我们通常处理成对的**复[格拉斯曼变量](@entry_id:199573)** $(\eta_i, \bar{\eta}_i)$，它们被视为独立的[格拉斯曼变量](@entry_id:199573)。积分测度通常写为 $\prod_i d\bar{\eta}_i d\eta_i$。根据积分规则，同样只有包含所有变量恰好一次的项才能在积分后存活下来。一个基本的归一化结果是 $\int d\bar{\eta} d\eta \, \eta\bar{\eta} = 1$。

### 基石：高斯型格拉斯曼积分

格拉斯曼积分中最强大和最常用的结果是高斯积分公式。它构成了计算非[相互作用费米子](@entry_id:160994)系统[配分函数](@entry_id:193625)的基础，并且是发展[微扰理论](@entry_id:138766)和更高级技术（如[Wick定理](@entry_id:137086)）的出发点。

#### 基本公式

对于 $N$ 对复[格拉斯曼变量](@entry_id:199573) $(\eta_i, \bar{\eta}_i)$，高斯积分公式如下：
$$
Z = \int \left(\prod_{i=1}^N d\bar{\eta}_i d\eta_i\right) \exp\left(-\sum_{j,k=1}^N \bar{\eta}_j M_{jk} \eta_k\right) = \det(M)
$$
其中 $M$ 是一个 $N \times N$ 的复数矩阵。这个公式是格拉斯曼积分的灵魂，它将一个看似复杂的[指数函数](@entry_id:161417)的积分与一个简单的[矩阵行列式](@entry_id:194066)联系起来。这个结果与[玻色子](@entry_id:138266)的[高斯积分](@entry_id:187139) $\int \exp(-\frac{1}{2} \mathbf{x}^T A \mathbf{x}) d^N x \propto (\det A)^{-1/2}$ 形成了鲜明对比，[行列式](@entry_id:142978)出现在分子上而不是分母。

#### 在[配分函数](@entry_id:193625)中的应用

高斯积分公式直接用于计算非相互作用费米系统的[配分函数](@entry_id:193625) $Z$。考虑一个由 $2N$ 对[格拉斯曼变量](@entry_id:199573) $(\psi_i, \bar{\psi}_i)$ 和 $(\chi_i, \bar{\chi}_i)$ 描述的系统，其作用量为 $S = \sum_{i=1}^{N} ( a \bar{\psi}_i \psi_i + b \bar{\chi}_i \chi_i + c \bar{\psi}_i \chi_i + d \bar{\chi}_i \psi_i )$ [@problem_id:1146527]。

由于作用量是各个指标 $i$ 的独立贡献之和， $S = \sum_{i=1}^N S_i$，[配分函数](@entry_id:193625) $Z = \int e^{-S} d\mu$ 可以因子化为 $Z = \prod_{i=1}^N Z_i$。我们只需计算单一位点 $i$ 的[配分函数](@entry_id:193625) $Z_i$。对于每个位点（省略下标 $i$），作用量为 $S_i = a \bar{\psi} \psi + b \bar{\chi} \chi + c \bar{\psi} \chi + d \bar{\chi} \psi$。我们可以将其写成矩阵形式。定义一个列向量 $\Psi = \begin{pmatrix} \psi \\ \chi \end{pmatrix}$ 和一个行向量 $\bar{\Psi} = \begin{pmatrix} \bar{\psi} & \bar{\chi} \end{pmatrix}$，作用量可以表示为 $\bar{\Psi} M \Psi$，其中矩阵 $M$ 为：
$$
M = \begin{pmatrix} a  c \\ d  b \end{pmatrix}
$$
根据[高斯积分](@entry_id:187139)公式，单一位点的[配分函数](@entry_id:193625)就是 $Z_i = \det(M) = ab - cd$。因此，整个系统的[配分函数](@entry_id:193625)为：
$$
Z = (ab - cd)^N
$$

#### [普法夫值](@entry_id:190772)（Pfaffian）积分

对于实[格拉斯曼变量](@entry_id:199573) $\theta_i$，还有一个与高斯积分密切相关的重要公式。如果矩阵 $B$ 是一个 $2N \times 2N$ 的实反对称矩阵 ($B_{ij} = -B_{ji}$)，则有：
$$
\int d\theta_1 d\theta_2 \cdots d\theta_{2N} \, \exp\left(\frac{1}{2} \sum_{i,j=1}^{2N} \theta_i B_{ij} \theta_j\right) = \text{Pf}(B)
$$
其中 $\text{Pf}(B)$ 是矩阵 $B$ 的**[普法夫值](@entry_id:190772)（Pfaffian）**，其平方等于矩阵的行列式：$(\text{Pf}(B))^2 = \det(B)$。

为了理解这个结果的来源，我们可以考虑 $N=2$ (即四个变量) 的情况 [@problem_id:1146557]。积分是 $I = \int d\theta_1 d\theta_2 d\theta_3 d\theta_4 \, \exp(\frac{1}{2} \sum_{i,j=1}^4 \theta_i B_{ij} \theta_j)$。由于被积函数中任何[格拉斯曼变量](@entry_id:199573)的幂次高于1的项均为零，指数的[泰勒展开](@entry_id:145057)是有限的。对于四变量积分，只有展开式中包含所有四个变量 $\theta_1\theta_2\theta_3\theta_4$ 的项才会存活。设 $X = \frac{1}{2}\sum \theta_i B_{ij} \theta_j$。由于 $X$ 是变量的二次型，只有 $X^2$ 项才能提供四次的项。展开 $e^X = 1 + X + \frac{1}{2}X^2 + \dots$，我们发现只有 $\frac{1}{2}X^2$ 项对积分有贡献。
$$
\frac{1}{2} X^2 = \frac{1}{8} (\sum \theta_i B_{ij} \theta_j) (\sum \theta_k B_{kl} \theta_l)
$$
展开这个乘积，并利用反对称性 ($B_{ii}=0$) 和 $\theta_i^2=0$，非零项必须包含四个不同的变量。经过仔细的代数运算，$\theta_1\theta_2\theta_3\theta_4$ 的系数被证明恰好是 $B_{12}B_{34}-B_{13}B_{24}+B_{14}B_{23}$，这正是 $4 \times 4$ [反对称矩阵](@entry_id:155998) $B$ 的[普法夫值](@entry_id:190772)的定义。

### 计算[物理可观测量](@entry_id:154692)：关联函数

除了[配分函数](@entry_id:193625)，格拉斯曼积分最主要的应用是计算物理可观測量的[期望值](@entry_id:153208)，即**关联函数（correlation functions）**。

#### 定义与基本计算

一个算符 $\mathcal{O}$ 的[期望值](@entry_id:153208)（或关联函数）定义为：
$$
\langle \mathcal{O} \rangle = \frac{1}{Z} \int \left(\prod d\bar{\eta}_i d\eta_i\right) \, \mathcal{O} \, e^{-S}
$$
其中 $Z$ 是[配分函数](@entry_id:193625)，起归一化因子的作用。

对于简单的系统，我们可以通过直接展开[指数函数](@entry_id:161417)来计算关联函数。考虑一个由作用量 $S = \sum_{i,j=1}^2 \bar{\eta}_i A_{ij} \eta_j$ 描述的系统，我们希望计算四点关联函数 $\langle \eta_1 \bar{\eta}_2 \eta_2 \bar{\eta}_1 \rangle$ [@problem_id:1146530]。
$$
\langle \eta_1 \bar{\eta}_2 \eta_2 \bar{\eta}_1 \rangle = \frac{1}{Z} \int d\bar{\eta}_1 d\eta_1 d\bar{\eta}_2 d\eta_2 \, (\eta_1 \bar{\eta}_2 \eta_2 \bar{\eta}_1) \, e^{-S}
$$
被积函数中的算符 $\mathcal{O} = \eta_1 \bar{\eta}_2 \eta_2 \bar{\eta}_1$ 已经是一个四次项，包含了所有的[格拉斯曼变量](@entry_id:199573)。当我们展开 $e^{-S} = 1 - S + \frac{1}{2}S^2 - \dots$，任何高于零次的项（如 $S, S^2$ 等）与 $\mathcal{O}$ 相乘都会产生次数超过4的项，这些项在只有四个变量的格拉斯曼代数中为零。因此，只有展开式中的常数项 '1' 有贡献。分子变为：
$$
\int d\bar{\eta}_1 d\eta_1 d\bar{\eta}_2 d\eta_2 \, (\eta_1 \bar{\eta}_2 \eta_2 \bar{\eta}_1) = \int d\bar{\eta}_1 d\eta_1 d\bar{\eta}_2 d\eta_2 \, (-\eta_1 \bar{\eta}_1 \eta_2 \bar{\eta}_2) = -1
$$
分母是[配分函数](@entry_id:193625) $Z = \det(A)$。因此，关联函数的结果是 $-\frac{1}{\det(A)} = -\frac{1}{ad-bc}$。

#### [Wick定理](@entry_id:137086)与传播子

对于高阶关联函数，逐项展开 $e^{-S}$ 变得非常繁琐。幸运的是，对于高斯型理论（即作用量是二次的），存在一个强大的工具——**[Wick定理](@entry_id:137086)**。

该定理指出，任意多点关联函数都可以表示为所有可能的两点关联函数（称为**[传播子](@entry_id:139558)**或收缩）配对的乘[积之和](@entry_id:266697)。对于[费米子](@entry_id:146235)，由于交换变量会引入负号，求和时需要考虑[排列](@entry_id:136432)的符号。

在高斯理论中，基本的两点关联函数（或[费米子](@entry_id:146235)[传播子](@entry_id:139558)）由作用量矩阵 $A$ 的逆矩阵给出：
$$
\langle \eta_i \bar{\eta}_j \rangle = (A^{-1})_{ij}
$$
所有其他类型的两点函数，如 $\langle \eta_i \eta_j \rangle$ 和 $\langle \bar{\eta}_i \bar{\eta}_j \rangle$，均为零。

利用[Wick定理](@entry_id:137086)，一个四点关联函数可以表示为一个 $2 \times 2$ [行列式](@entry_id:142978)：
$$
\langle \eta_i \eta_j \bar{\eta}_k \bar{\eta}_l \rangle = \det
\begin{pmatrix}
\langle \eta_i \bar{\eta}_k \rangle  \langle \eta_i \bar{\eta}_l \rangle \\
\langle \eta_j \bar{\eta}_k \rangle  \langle \eta_j \bar{\eta}_l \rangle
\end{pmatrix}
= \langle \eta_i \bar{\eta}_k \rangle \langle \eta_j \bar{\eta}_l \rangle - \langle \eta_i \bar{\eta}_l \rangle \langle \eta_j \bar{\eta}_k \rangle
$$
例如，计算关联函数 $\langle \eta_1 \eta_2 \bar{\eta}_1 \bar{\eta}_3 \rangle$ 对于一个由 $3 \times 3$ 矩阵 $A$ 定义的系统 [@problem_id:1146518]。根据[Wick定理](@entry_id:137086)，我们有：
$$
\langle \eta_1 \eta_2 \bar{\eta}_1 \bar{\eta}_3 \rangle = \langle \eta_1 \bar{\eta}_1 \rangle \langle \eta_2 \bar{\eta}_3 \rangle - \langle \eta_1 \bar{\eta}_3 \rangle \langle \eta_2 \bar{\eta}_1 \rangle
$$
这等价于 $(A^{-1})_{11} (A^{-1})_{23} - (A^{-1})_{13} (A^{-1})_{21}$。任务就简化为计算矩阵 $A$ 的逆矩阵的特定元素，这是一个直接的线性代数问题。

#### 连通与非连通关联函数

在多体物理中，我们常常关心的是**连通关联函数**，它度量了系统各部分之间的真实相互作用，剔除了因[统计独立性](@entry_id:150300)而产生的虚假关联。例如，对于一个算符 $\mathcal{O}$，其两点连通关联函数定义为：
$$
\langle \mathcal{O}^2 \rangle_c = \langle \mathcal{O}^2 \rangle - \langle \mathcal{O} \rangle^2
$$
考虑一个由 $N$ 个独立的[费米子](@entry_id:146235)模式组成的系统，其作用量为 $S = m \sum_{i=1}^N \bar{\psi}_i \psi_i$。我们来计算[复合算符](@entry_id:152160) $\mathcal{O} = \sum_{i=1}^N \bar{\psi}_i \psi_i$ 的连通关联函数 [@problem_id:1146513]。
首先，[配分函数](@entry_id:193625) $Z = m^N$。对于独立的模式，$\langle \psi_i \bar{\psi}_j \rangle = \delta_{ij}/m$。我们需要计算 $\langle \bar{\psi}_i \psi_i \rangle$。使用源场方法或直接积分可以得到 $\langle \bar{\psi}_i \psi_i \rangle = -1/m$。因此，$\langle \mathcal{O} \rangle = \sum_i \langle \bar{\psi}_i \psi_i \rangle = -N/m$。
接着计算 $\langle \mathcal{O}^2 \rangle$：
$$
\mathcal{O}^2 = \left( \sum_{i=1}^N \bar{\psi}_i \psi_i \right)^2 = \sum_{i,j=1}^N (\bar{\psi}_i \psi_i) (\bar{\psi}_j \psi_j)
$$
当 $i=j$ 时，项为 $(\bar{\psi}_i \psi_i)^2 = 0$。因此求和只剩下 $i \neq j$ 的项。
$$
\langle \mathcal{O}^2 \rangle = \sum_{i \neq j} \langle (\bar{\psi}_i \psi_i) (\bar{\psi}_j \psi_j) \rangle
$$
由于不同模式 $i$ 和 $j$ 是独立的，[期望值](@entry_id:153208)可以因子化：$\langle (\bar{\psi}_i \psi_i) (\bar{\psi}_j \psi_j) \rangle = \langle \bar{\psi}_i \psi_i \rangle \langle \bar{\psi}_j \psi_j \rangle = (-1/m)(-1/m) = 1/m^2$。总共有 $N(N-1)$ 个这样的项，所以 $\langle \mathcal{O}^2 \rangle = N(N-1)/m^2$。
最后，连通关联函数为：
$$
\langle \mathcal{O}^2 \rangle_c = \frac{N(N-1)}{m^2} - \left(\frac{-N}{m}\right)^2 = \frac{N^2 - N - N^2}{m^2} = -\frac{N}{m^2}
$$
这个非零结果揭示了由[泡利不相容原理](@entry_id:141850)引起的[费米子](@entry_id:146235)之间的有效关联，即使它们没有直接相互作用。

### 处理相互作用

格拉斯曼积分的真正威力体现在处理[相互作用费米子](@entry_id:160994)系统上。虽然一般情况没有精确解，但有多种强大的近似和非微扰方法。

#### [微扰展开](@entry_id:159275)与[幂零性](@entry_id:147926)

对于某些简单的相互作用，我们可以利用[格拉斯曼变量](@entry_id:199573)的[幂零性](@entry_id:147926)直接计算。考虑一个包含四次[相互作用项](@entry_id:637283)的作用量 [@problem_id:1146567]：
$$
S = S_{quad} + \lambda (\bar{\eta}_1 \eta_1) (\bar{\eta}_2 \eta_2)
$$
其中 $S_{quad}$ 是二次项。由于相互作用项 $S_{int} = \lambda (\bar{\eta}_1 \eta_1) (\bar{\eta}_2 \eta_2)$ 包含了全部四个变量，它的任意次幂都为零，$(S_{int})^n = 0$ for $n \ge 2$。因此，[指数函数](@entry_id:161417)可以精确展开：
$$
e^{-S_{int}} = 1 - S_{int} = 1 - \lambda (\bar{\eta}_1 \eta_1) (\bar{\eta}_2 \eta_2)
$$
[配分函数](@entry_id:193625) $Z = \int e^{-S_{quad}} e^{-S_{int}} d\mu$ 的计算分解为两部分：
$$
Z = \int e^{-S_{quad}} d\mu - \lambda \int (\bar{\eta}_1 \eta_1 \bar{\eta}_2 \eta_2) e^{-S_{quad}} d\mu
$$
第一部分是标准的高斯积分，结果为 $\det(M)$，其中 $M$ 是 $S_{quad}$ 对应的矩阵。第二部分的积分中，由于 $(\bar{\eta}_1 \eta_1 \bar{\eta}_2 \eta_2)$ 的存在， $e^{-S_{quad}}$ 展开式中只有常数项 "1" 能给出非零贡献。因此第二项的积分值为 $1$。最终结果为 $Z = \det(M) - \lambda$。

#### Hubbard-Stratonovich 变换

对于更普遍的[四费米子相互作用](@entry_id:184227)，例如形如 $(\bar{\psi}\psi)^2$ 的密度-密度相互作用，一种强大的非微扰技术是**Hubbard-Stratonovich (HS) 变换**。其核心思想是引入一个辅助的标量场（玻色场）$\phi$，将四[费米子](@entry_id:146235)项线性化。HS 变换基于以下[高斯积分](@entry_id:187139)恒等式：
$$
e^{\alpha A^2} = \sqrt{\frac{1}{\pi}} \int_{-\infty}^{\infty} d\phi \, e^{-\phi^2 + 2\sqrt{\alpha} \phi A}
$$
考虑一个具有作用量 $S = \omega_1 \bar{\eta}_1 \eta_1 + \omega_2 \bar{\eta}_2 \eta_2 - g (\bar{\eta}_1 \eta_1 + \bar{\eta}_2 \eta_2)^2$ 的系统 [@problem_id:1146516]。我们令 $A = \bar{\eta}_1 \eta_1 + \bar{\eta}_2 \eta_2$ 并应用HS变换来处理 $e^{g A^2}$ 项。[配分函数](@entry_id:193625)变为：
$$
Z = \int d\mu_\eta \frac{1}{\sqrt{\pi}} \int d\phi \, e^{-\phi^2} \exp\left( -(\omega_1-2\sqrt{g}\phi)\bar{\eta}_1\eta_1 - (\omega_2-2\sqrt{g}\phi)\bar{\eta}_2\eta_2 \right)
$$
现在，关于[格拉斯曼变量](@entry_id:199573)的积分变成了高斯形式！我们可以先执行格拉斯曼积分，得到：
$$
Z = \frac{1}{\sqrt{\pi}} \int d\phi \, e^{-\phi^2} \left( (\omega_1-2\sqrt{g}\phi)(\omega_2-2\sqrt{g}\phi) \right)
$$
剩下的只是一个关于辅助场 $\phi$ 的标准高斯积分，可以精确计算，最终得到 $Z = \omega_1\omega_2 + 2g$。HS变换的威力在于它将一个棘手的[相互作用费米子](@entry_id:160994)问题转化为了一个非[相互作用费米子](@entry_id:160994)在一个涨落的标量背景场中的问题，然后对所有可能的背景场进行积分。

#### 积掉[费米子](@entry_id:146235)

在许多[混合系统](@entry_id:271183)中，[费米子与玻色子](@entry_id:138279)相互作用。一个常见的策略是“积掉”费米自由度，以获得一个只包含[玻色子](@entry_id:138266)的[有效作用量](@entry_id:145780)。这种方法揭示了[费米子](@entry_id:146235)如何媒介[玻色子](@entry_id:138266)之间的有效相互作用。

考虑一个由[标量场](@entry_id:151443) $\phi_1, \phi_2$ 和费米场 $\psi_1, \psi_2$ 组成的系统，其作用量包含耦合项 $-g \phi_1 \bar{\psi}_1 \psi_1 - g \phi_2 \bar{\psi}_2 \psi_2$ [@problem_id:1146549]。[配分函数](@entry_id:193625)是关于所有场的积分。我们可以先对[格拉斯曼变量](@entry_id:199573)进行积分：
$$
I_F(\phi_1, \phi_2) = \int d\bar{\psi}_1 d\psi_1 d\bar{\psi}_2 d\psi_2 \, \exp(g \phi_1 \bar{\psi}_1 \psi_1 + g \phi_2 \bar{\psi}_2 \psi_2)
$$
展开指数函数（利用[幂零性](@entry_id:147926)）$(1 + g\phi_1\bar{\psi}_1\psi_1)(1 + g\phi_2\bar{\psi}_2\psi_2)$，唯一能在积分后存活的项是 $g^2 \phi_1 \phi_2 (\bar{\psi}_1 \psi_1 \bar{\psi}_2 \psi_2)$。此项的积分为 $g^2 \phi_1 \phi_2$。
因此，积掉[费米子](@entry_id:146235)后，我们得到了一个只关于玻色场的[有效理论](@entry_id:155490)，其[配分函数](@entry_id:193625)为：
$$
Z = \int d\phi_1 d\phi_2 \, (g^2 \phi_1 \phi_2) \, e^{-S_B(\phi_1, \phi_2)}
$$
其中 $S_B$ 是原始作用量中的纯玻色部分。这个过程生成了一个新的有效[相互作用项](@entry_id:637283) $\propto g^2 \phi_1 \phi_2$，它源于[费米子](@entry_id:146235)圈图的贡献。剩下的积分是一个标准的多变量[高斯积分](@entry_id:187139)，可以解析求解。

通过本章的学习，我们从最基本的代数规则出发，逐步掌握了计算高斯积分、关联函数以及处理相互作用的强大工具。这些原理和机制不仅是理论研究的基础，也为理解[凝聚态物质](@entry_id:747660)中复杂的电子行为提供了基本的框架。