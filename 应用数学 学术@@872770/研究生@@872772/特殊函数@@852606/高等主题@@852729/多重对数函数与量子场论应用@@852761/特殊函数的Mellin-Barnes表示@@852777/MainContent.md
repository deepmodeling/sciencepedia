## 引言
梅林-巴恩斯（Mellin-Barnes）表示是分析数学和理论物理中一个极其强大的工具，它通过将函数表示为复平面上的围道积分，为研究其深刻的[解析性](@entry_id:140716)质提供了一条独特的途径。面对行为复杂的[特殊函数](@entry_id:143234)以及难以用常规方法求解的[定积分](@entry_id:147612)，传统的[实分析](@entry_id:137229)方法往往显得力不从心。梅林-巴恩斯方法通过将问题转化到复数域，利用伽马函数的优美性质和留数定理的威力，为解决这些挑战提供了系统性的框架。

本文旨在全面介绍这一技术。在“原理与机制”一章中，我们将从[逆梅林变换](@entry_id:180257)出发，揭示该表示的[构造原理](@entry_id:141667)，并详细讲解如何运用[留数定理](@entry_id:164878)计算这些积分，从而推导级数和[渐近展开](@entry_id:173196)。接下来，在“应用与跨学科联系”一章中，我们将探索该方法在计算高等积分、分析[特殊函数](@entry_id:143234)性质，以及在[量子场论](@entry_id:138177)、数论等前沿领域的具体应用。最后，“动手实践”部分将通过一系列精心设计的练习，帮助读者巩固所学知识并将其付诸实践。

## 原理与机制

继前一章对梅林-巴恩斯（Mellin-Barnes）表示的介绍之后，本章将深入探讨其核心原理和工作机制。我们将系统地阐述如何构建和计算这些积分，并展示如何利用它们来推导特殊函数的[级数展开](@entry_id:142878)、渐近行为和解析延拓，以及如何评估复杂的定积分。本章的核心在于将抽象的积分表示与具体的函数性质和应用联系起来。

### [梅林-巴恩斯积分](@entry_id:199868)：[逆梅林变换](@entry_id:180257)

[梅林-巴恩斯积分](@entry_id:199868)的理论基础源于**[梅林变换](@entry_id:264063)**（Mellin Transform）。对于一个定义在 $(0, \infty)$ 上的函数 $f(x)$，其[梅林变换](@entry_id:264063) $\tilde{f}(s)$ 定义为：
$$
\tilde{f}(s) = \mathcal{M}[f(x); s] = \int_0^\infty x^{s-1} f(x) \, dx
$$
其中 $s$ 是一个[复变量](@entry_id:175312)。这个变换在复平面 $s$ 的某个垂直带状区域内收敛，该区域被称为**基本带**（fundamental strip）。

[梅林-巴恩斯积分](@entry_id:199868)正是该变换的**逆变换**，它允许我们从[梅林变换](@entry_id:264063) $\tilde{f}(s)$ 重构原函数 $f(x)$：
$$
f(x) = \frac{1}{2\pi i} \int_{c-i\infty}^{c+i\infty} x^{-s} \tilde{f}(s) \, ds
$$
这里的积分路径是一条平行于虚轴的直线 $\text{Re}(s) = c$，常数 $c$ 的取值必须确保该路径位于 $\tilde{f}(s)$ 的基本带内。积分核中的 $x^{-s}$ 项是连接积分变量 $s$ 和函数[自变量](@entry_id:267118) $x$ 的桥梁，它在后续的分析中起着至关重要的作用。

作为一个基础示例，我们来考虑函数 $f(x) = \frac{1}{x(1+x)}$。我们的目标是为其构建[梅林-巴恩斯积分](@entry_id:199868)表示。[@problem_id:718702] 为此，我们首先需要计算其[梅林变换](@entry_id:264063) $\tilde{f}(s)$。我们可以将函数写为 $f(x) = x^{-1}(1+x)^{-1}$。利用[梅林变换](@entry_id:264063)的性质 $\mathcal{M}[x^k g(x); s] = \mathcal{M}[g(x); s+k]$，并借助已知的变换结果 $\mathcal{M}[(1+ax)^{-b}; s] = a^{-s} \frac{\Gamma(s)\Gamma(b-s)}{\Gamma(b)}$，我们可以进行如下推导：

令 $g(x) = (1+x)^{-1}$，其[梅林变换](@entry_id:264063)（对应 $a=1, b=1$）为：
$$
\mathcal{M}[g(x); s] = \frac{\Gamma(s)\Gamma(1-s)}{\Gamma(1)} = \Gamma(s)\Gamma(1-s)
$$
该变换的基本带是 $0  \text{Re}(s)  1$。
因此，原函数 $f(x) = x^{-1}g(x)$ 的[梅林变换](@entry_id:264063)为：
$$
\tilde{f}(s) = \mathcal{M}[g(x); s-1] = \Gamma(s-1)\Gamma(1-(s-1)) = \Gamma(s-1)\Gamma(2-s)
$$
其基本带也相应地从 $0  \text{Re}(u)  1$（令 $u=s-1$）平移为 $1  \text{Re}(s)  2$。

现在，我们可以写出 $f(x)$ 的[梅林-巴恩斯积分](@entry_id:199868)表示：
$$
f(x) = \frac{1}{2\pi i} \int_{c-i\infty}^{c+i\infty} x^{-s} \Gamma(s-1)\Gamma(2-s) \, ds
$$
其中积分路径的实部 $c$ 满足 $1  c  2$。这个积分表达式就是函数 $f(x)$ 的[梅林-巴恩斯表示](@entry_id:200651)。接下来，我们将探讨如何计算这类积分。

### [梅林-巴恩斯积分](@entry_id:199868)的求值：[留数定理](@entry_id:164878)的应用

直接计算[梅林-巴恩斯积分](@entry_id:199868)通常是困难的。最强大的评估工具是**柯西[留数定理](@entry_id:164878)**（Cauchy's Residue Theorem）。其基本思想是将沿直线路径的开路积分通过一个在无穷远处的半圆弧“闭合”成一个闭合回路，然后将积分值表达为回路内部所有极点的留数之和。

被积函数通常形如 $I(s) = x^{-s} \tilde{f}(s)$。Gamma函数 $\Gamma(z)$ 在 $z=0, -1, -2, \dots$ 处有一系列简单极点，这为 $\tilde{f}(s)$ 提供了极点来源。[积分的收敛](@entry_id:187300)性和闭合方向由因子 $x^{-s} = \exp(-s \ln x)$ 在无穷远处的行为决定。我们总是在积分值衰减为零的方向上闭合积分回路。

设 $s = \sigma + i\tau$，则 $|x^{-s}| = |\exp(-(\sigma+i\tau)\ln x)| = \exp(-\sigma \ln x)$。
1.  如果 $x > 1$，则 $\ln x > 0$。为了使 $\exp(-\sigma \ln x)$ 在 $|s| \to \infty$ 时衰减，我们需要 $\sigma \to +\infty$。因此，我们将积分路径向**右侧**闭合。
2.  如果 $0  x  1$，则 $\ln x  0$。为了使 $\exp(-\sigma \ln x)$ 衰减，我们需要 $\sigma \to -\infty$。因此，我们将积分路径向**左侧**闭合。

根据留数定理，若沿闭合半圆弧的积分贡献为零，则原积分等于闭合路径所包围的所有极点留数之和（注意闭合方向，顺时针闭合会引入一个负号）。

让我们回到之前的例子 $f(x) = \frac{1}{x(1+x)}$ 来具体说明这个过程。[@problem_id:718702] 被积函数为 $h(s) = x^{-s} \Gamma(s-1)\Gamma(2-s)$。
-   $\Gamma(s-1)$ 的极点位于 $s = 1, 0, -1, \dots$ (左侧极点)。
-   $\Gamma(2-s)$ 的极点位于 $s = 2, 3, 4, \dots$ (右侧极点)。
积分路径 $1  c  2$ 恰好将这两组极点分开。

**情况 1: $x > 1$**
我们向右侧闭合回路，包围了 $s = 2, 3, 4, \dots$ 处的极点。由于是顺时针闭合，积分值为 $-2\pi i$ 乘以这些留数的总和。在极点 $s_k=2+k$ ($k=0,1,2,\dots$) 处的留数为：
$$
\text{Res}_{s=2+k}[h(s)] = x^{-(2+k)}\Gamma(1+k) \cdot \text{Res}_{s=2+k}[\Gamma(2-s)] = x^{-2-k} k! \left(-\frac{(-1)^k}{k!}\right) = -x^{-2}(-x^{-1})^k
$$
这里利用了 $\text{Res}_{u=-n}[\Gamma(u)] = \frac{(-1)^n}{n!}$ 和 $\text{Res}_{s=a+n}[\Gamma(a-s)] = -\frac{(-1)^n}{n!}$。
因此，积分值为：
$$
f(x) = (-1) \sum_{k=0}^{\infty} \text{Res}_{s=2+k}[h(s)] = \sum_{k=0}^{\infty} x^{-2}(-x^{-1})^k = \frac{1}{x^2} \sum_{k=0}^{\infty} \left(-\frac{1}{x}\right)^k
$$
这是一个[公比](@entry_id:275383)为 $-1/x$ 的[几何级数](@entry_id:158490)，由于 $x>1$，[级数收敛](@entry_id:142638)于 $\frac{1}{1 - (-1/x)} = \frac{x}{x+1}$。所以，$f(x) = \frac{1}{x^2} \frac{x}{x+1} = \frac{1}{x(1+x)}$。

**情况 2: $0  x  1$**
我们向左侧闭合回路，包围了 $s=1, 0, -1, \dots$ 处的极点。这是逆时针闭合，积分值为 $2\pi i$ 乘以留数总和。在极点 $s_k=1-k$ ($k=0,1,2,\dots$) 处的留数为：
$$
\text{Res}_{s=1-k}[h(s)] = x^{-(1-k)}\Gamma(2-(1-k)) \cdot \text{Res}_{s=1-k}[\Gamma(s-1)] = x^{-1+k} \Gamma(1+k) \left(\frac{(-1)^k}{k!}\right) = \frac{1}{x}(-x)^k
$$
积分值为：
$$
f(x) = \sum_{k=0}^{\infty} \text{Res}_{s=1-k}[h(s)] = \sum_{k=0}^{\infty} \frac{1}{x}(-x)^k = \frac{1}{x} \sum_{k=0}^{\infty} (-x)^k = \frac{1}{x} \frac{1}{1+x} = \frac{1}{x(1+x)}
$$
两种情况都得到了与原函数一致的结果，这清晰地展示了[梅林-巴恩斯积分](@entry_id:199868)表示的自洽性与强大功能。

### 应用：级数展开、[渐近展开](@entry_id:173196)与解析延拓

通过选择不同的闭合方向，[梅林-巴恩斯积分](@entry_id:199868)成为了研究函数在不同区域行为的统一框架。

#### [级数展开](@entry_id:142878)

当参数 $|z|1$ 时，我们通常向左闭合积分路径，拾取 $\Gamma(\dots+s)$ 型[函数的极点](@entry_id:189069)，从而得到关于 $z$ 的[幂级数展开](@entry_id:273325)（[泰勒级数](@entry_id:147154)）。

一个经典的例子是函数 $(1+z)^{-1}$。其[梅林-巴恩斯表示](@entry_id:200651)为（取 $\nu=1$）：[@problem_id:718730]
$$
(1+z)^{-1} = \frac{1}{2\pi i} \int_{c-i\infty}^{c+i\infty} \Gamma(s)\Gamma(1-s) z^{-s} ds, \quad 0  c  1
$$
对于 $|z|1$，我们向左闭合路径，包围 $\Gamma(s)$ 在 $s=-k$ ($k=0,1,2,\dots$) 处的极点。在 $s=-k$ 处的留数为：
$$
\text{Res}_{s=-k}[\Gamma(s)\Gamma(1-s)z^{-s}] = \text{Res}_{s=-k}[\Gamma(s)] \cdot \Gamma(1-(-k)) \cdot z^{-(-k)} = \frac{(-1)^k}{k!} \cdot \Gamma(1+k) \cdot z^k = (-1)^k z^k
$$
将所有留数相加，我们便得到了熟悉的[几何级数](@entry_id:158490)：
$$
(1+z)^{-1} = \sum_{k=0}^{\infty} (-1)^k z^k
$$
这个过程揭示了[函数级数](@entry_id:139536)展开系数的深刻来源——它们本质上是其[梅林-巴恩斯表示](@entry_id:200651)中被积函数在复平面的留数。

#### [渐近展开](@entry_id:173196)与[解析延拓](@entry_id:147225)

当参数 $|z|>1$ 时，我们向右闭合积分路径，拾取 $\Gamma(\dots-s)$ 型[函数的极点](@entry_id:189069)，得到一个关于 $1/z$ 的级数，这通常是原函数在 $z \to \infty$ 时的**[渐近展开](@entry_id:173196)**。

考虑函数 $f(z) = (1+az)^{-\nu}$，其中 $a, \nu > 0$。其积分为：[@problem_id:718682]
$$
(1+az)^{-\nu} = \frac{1}{\Gamma(\nu)} \frac{1}{2\pi i} \int_{c-i\infty}^{c+i\infty} \Gamma(s)\Gamma(\nu-s) (az)^{-s} ds, \quad 0  c  \nu
$$
对于 $|z| \to \infty$，我们向右闭合路径，包围 $\Gamma(\nu-s)$ 在 $s=\nu+k$ ($k=0,1,2,\dots$) 处的极点。其留数贡献的总和给出了一个关于 $(az)^{-1}$ 的级数。其首项（$k=0$，对应极点 $s=\nu$）为：
$$
\text{Leading Term} \propto \text{Res}_{s=\nu}[\Gamma(s)\Gamma(\nu-s)(az)^{-s}] = \Gamma(\nu) \cdot (-1) \cdot (az)^{-\nu}
$$
经过正确的计算（包括积分前的系数和顺时针闭合的负号），我们得到[渐近展开](@entry_id:173196)的首项为 $a^{-\nu}z^{-\nu}$。这与我们通过[二项式展开](@entry_id:269603) $(az(1+1/az))^{-\nu}$ 得到的结论一致。

这一思想可以推广到更复杂的情况，例如[高斯超几何函数](@entry_id:193858) ${}_2F_1(a,b;c;z)$ 的**解析延拓**。该函数由 $|z|1$ 内的幂级数定义，但其[梅林-巴恩斯表示](@entry_id:200651)在更广的范围内有效。
$$
{}_2F_1(a,b;c;z) = \frac{\Gamma(c)}{\Gamma(a)\Gamma(b)} \frac{1}{2\pi i} \int_{\mathcal{L}} \frac{\Gamma(a+s)\Gamma(b+s)\Gamma(-s)}{\Gamma(c+s)} (-z)^s ds
$$
当 $|z|>1$ 时，我们向左闭合路径，此时包围的是 $\Gamma(a+s)$ 和 $\Gamma(b+s)$ 的极点，分别位于 $s=-a-n$ 和 $s=-b-n$ ($n=0,1,2,\dots$)。[@problem_id:718728]
假设 $a-b$ 不是整数，这两系列极点是分离的。计算所有在 $s=-a-n$ 的留数之和，可以得到一个形如 $C_a(-z)^{-a} {}_2F_1(\dots; 1/z)$ 的项。通过细致的[留数计算](@entry_id:174587)，可以确定系数 $C_a$：
$$
C_a = \frac{\Gamma(c)\Gamma(b-a)}{\Gamma(b)\Gamma(c-a)}
$$
同样地，对 $s=-b-n$ 的极点求和会得到另一个系数 $C_b$。最终结果是著名的 ${}_2F_1$ [解析延拓](@entry_id:147225)公式，它将函数在 $|z|>1$ 区域的行为表达为两个以 $1/z$ 为变量的新的[超几何函数](@entry_id:185332)之和。

### 重要的积分引理

在处理[梅林-巴恩斯积分](@entry_id:199868)时，一些特定[形式的积分](@entry_id:158607)反复出现，它们的求值结果被总结为引理，极大地简化了计算。

#### [巴恩斯引理](@entry_id:183059)

**巴恩斯第一引理**（Barnes's First Lemma）是其中最著名的一个。它给出了一个包含四个Gamma函数乘积的积分的[闭合形式](@entry_id:271343)：
$$
\frac{1}{2\pi i}\int_{L} \Gamma(a+s)\Gamma(b+s)\Gamma(c-s)\Gamma(d-s) ds = \frac{\Gamma(a+c)\Gamma(a+d)\Gamma(b+c)\Gamma(b+d)}{\Gamma(a+b+c+d)}
$$
前提是积分路径 $L$ 能将 $\Gamma(\dots+s)$ 的极点（位于[左半平面](@entry_id:270729)）和 $\Gamma(\dots-s)$ 的极点（位于右半平面）分离开。

例如，考虑计算积分 $I = \frac{1}{2\pi i} \int_{\sigma-i\infty}^{\sigma+i\infty} \Gamma\left(s-\frac{1}{2}\right)^2 \Gamma(1-s)^2 ds$，其中 $\frac{1}{2}  \sigma  1$。[@problem_id:718650]
我们可以将积分写作 $\int \Gamma(s-\frac{1}{2})\Gamma(s-\frac{1}{2})\Gamma(1-s)\Gamma(1-s) ds$。通过与引理的标准形式比对，我们识别出参数：$a = b = -1/2$，$c = d = 1$。给定的积分路径 $\frac{1}{2}  \sigma  1$ 满足分离极点的条件（$-\text{Re}(a)  \sigma  \text{Re}(c)$）。因此，我们可以直接应用引理的右手边公式：
$$
I = \frac{\Gamma(-\frac{1}{2}+1)\Gamma(-\frac{1}{2}+1)\Gamma(-\frac{1}{2}+1)\Gamma(-\frac{1}{2}+1)}{\Gamma(-\frac{1}{2}-\frac{1}{2}+1+1)} = \frac{\Gamma(\frac{1}{2})^4}{\Gamma(1)} = \frac{(\sqrt{\pi})^4}{1} = \pi^2
$$
另一个例子是计算积分 $I = \frac{1}{2\pi i} \int_{L} \Gamma(\frac{1}{2}+s)\Gamma(1+s)\Gamma(\frac{1}{2}-s)\Gamma(1-s) ds$。[@problem_id:718648] 这也是[巴恩斯引理](@entry_id:183059)的直接应用，参数为 $a=1/2, b=1, c=1/2, d=1$。其结果为：
$$
I = \frac{\Gamma(\frac{1}{2}+\frac{1}{2})\Gamma(\frac{1}{2}+1)\Gamma(1+\frac{1}{2})\Gamma(1+1)}{\Gamma(\frac{1}{2}+1+\frac{1}{2}+1)} = \frac{\Gamma(1)\Gamma(\frac{3}{2})\Gamma(\frac{3}{2})\Gamma(2)}{\Gamma(3)} = \frac{1 \cdot (\frac{1}{2}\sqrt{\pi})^2 \cdot 1}{2} = \frac{\pi}{8}
$$

#### 帕塞瓦尔-梅林定理

**帕塞瓦尔-梅林定理**（Parseval-Mellin Theorem）将两个函数乘积的实轴积分与它们[梅林变换](@entry_id:264063)的复平面积分联系起来：
$$
\int_0^\infty f(x)g(x) dx = \frac{1}{2\pi i} \int_{c-i\infty}^{c+i\infty} F(s) G(1-s) ds
$$
其中 $F(s)$ 和 $G(s)$ 分别是 $f(x)$ 和 $g(x)$ 的[梅林变换](@entry_id:264063)，积分路径 $c$ 位于 $F(s)$ 和 $G(1-s)$ 的共同解析带内。这个定理为计算看似无关的定积分提供了一条意想不到的途径。

例如，我们可以用此方法计算积分 $I = \int_0^\infty \frac{\ln(1+x)}{1+x^2} dx$。[@problem_id:718659]
令 $f(x) = \ln(1+x)$ 和 $g(x) = \frac{1}{1+x^2}$。我们已知它们的[梅林变换](@entry_id:264063)：
-   $F(s) = \mathcal{M}[\ln(1+x); s] = \frac{\pi}{s\sin(\pi s)}$，对 $-1  \text{Re}(s)  0$ 成立。
-   $G(s) = \mathcal{M}[\frac{1}{1+x^2}; s] = \frac{\pi}{2\sin(\pi s/2)}$，对 $0  \text{Re}(s)  2$ 成立。

因此，$G(1-s) = \frac{\pi}{2\sin(\pi(1-s)/2)} = \frac{\pi}{2\cos(\pi s/2)}$。公共解析带为 $-1  c  0$。根据定理，积分可写为：
$$
I = \frac{1}{2\pi i} \int_{c-i\infty}^{c+i\infty} \frac{\pi}{s\sin(\pi s)} \frac{\pi}{2\cos(\pi s/2)} ds
$$
这个[复积分](@entry_id:202758)可以通过向右闭合并计算在正整数 $s=1, 2, 3, \dots$ 处的留数来求值。这个过程涉及对简单和双[重极点](@entry_id:262210)的仔细分析，最终结果为 $I = G + \frac{\pi}{4}\ln 2$，其中 $G$ 是卡塔兰常数。

### 高级应用与现象

[梅林-巴恩斯表示](@entry_id:200651)的框架不仅限于分析已知函数，它本身也可以作为定义新函数和解释复杂现象的工具。

#### 作为定义的[广义函数](@entry_id:182848)：迈耶G函数

许多重要的[特殊函数](@entry_id:143234)，特别是超几何类型的函数，都可以被看作是某个标准形式[梅林-巴恩斯积分](@entry_id:199868)的特例。**迈耶G函数**（Meijer G-function）$G_{p,q}^{m,n}(z)$ 正是这种思想的集大成者，它被定义为一个通用的[梅林-巴恩斯积分](@entry_id:199868)：
$$
G_{p,q}^{m,n}\left(z\middle|\begin{smallmatrix} a_1,\dots,a_p \\ b_1,\dots,b_q \end{smallmatrix}\right) = \frac{1}{2\pi i} \int_L \frac{\prod_{j=1}^m \Gamma(b_j - s) \prod_{k=1}^n \Gamma(1 - a_k + s)}{\prod_{j=m+1}^q \Gamma(1 - b_j + s) \prod_{k=n+1}^p \Gamma(a_k - s)} z^s ds
$$
通过选择不同的参数 $m,n,p,q$ 和 $a_k, b_j$，这个函数可以表示几乎所有常见的[特殊函数](@entry_id:143234)。例如，考虑 $G_{0,1}^{1,0}\left(z\middle|\begin{smallmatrix} - \\ 0 \end{smallmatrix}\right)$。[@problem_id:718707]
根据定义，它等于：
$$
G_{0,1}^{1,0}\left(z\middle|\begin{smallmatrix} - \\ 0 \end{smallmatrix}\right) = \frac{1}{2\pi i} \int_L \Gamma(-s) z^s ds
$$
向右闭合路径并对 $\Gamma(-s)$ 在 $s=k$ ($k=0,1,2,\dots$) 处的极点求留数，我们得到：
$$
G_{0,1}^{1,0}(z) = (-1) \sum_{k=0}^{\infty} \text{Res}_{s=k}[\Gamma(-s)z^s] = (-1) \sum_{k=0}^{\infty} \left(-\frac{(-1)^k}{k!} z^k\right) = \sum_{k=0}^{\infty} \frac{(-1)^k z^k}{k!} = e^{-z}
$$
这表明，[指数函数](@entry_id:161417) $e^{-z}$ 只是迈耶G函数家族中的一个简单成员。

#### 挤压极点与对数[奇点](@entry_id:137764)

[梅林-巴恩斯表示](@entry_id:200651)还能深刻地揭示函数在[奇点](@entry_id:137764)附近的行为，特别是对数奇性的来源。在函数的[渐近展开](@entry_id:173196)中，对数项（如 $z^\alpha \ln z$）通常源于其[梅林变换](@entry_id:264063)在 $s=-\alpha$ 处存在**二阶或更高阶的极点**。

这种[高阶极点](@entry_id:169853)常常由所谓的**挤压极点**（pinching poles）现象产生：当函数参数变化时，原本分离的两列简单极点在复平面上相互靠近，并在某个临界参数下“挤压”或合并在一起，形成一个二阶极点。

一个典型的例子是[高斯超几何函数](@entry_id:193858) ${}_2F_1(a,b;c;w)$ 在参数满足 $a+b=c$ 时，在 $w=1$ 处表现出对数[奇点](@entry_id:137764)。我们来分析 $f(z) = {}_2F_1(\frac{1}{2}, \frac{1}{2}; 1; 1-z)$ 在 $z \to 0^+$ 时的行为。[@problem_id:718693]

我们研究其在 $(0,1)$ 上的[梅林变换](@entry_id:264063) $M(s) = \int_0^1 z^{s-1} f(z) dz$。利用已知的积分公式，可以推导出：
$$
M(s) = \frac{\Gamma(s)^2}{\Gamma(s+\frac{1}{2})^2}
$$
当 $s \to 0$ 时，由于 $\Gamma(s) \sim 1/s$，我们看到 $M(s)$ 的行为是：
$$
M(s) \approx \frac{(1/s)^2}{\Gamma(1/2)^2} = \frac{1}{\pi s^2}
$$
$M(s)$ 在 $s=0$ 处有一个二阶极点。这正是对数项的标志。$f(z)$ 在 $z \to 0^+$ 时的展开由 $M(s)z^{-s}$ 在左半平面的留数决定。在 $z \to 0^+$ 时，主导行为由 $M(s)$ 在 $s=0$ 处的二阶极点决定。通过计算 $M(s)z^{-s}$ 在 $s=0$ 的留数可以发现，展开式中 $\ln z$ 项的系数为 $-\lim_{s\to0}[s^2 M(s)]$。我们计算这个极限：
$$
-\lim_{s\to0} s^2 \frac{\Gamma(s)^2}{\Gamma(s+\frac{1}{2})^2} = -\frac{\lim_{s\to0}(s\Gamma(s))^2}{\Gamma(\frac{1}{2})^2} = -\frac{1^2}{(\sqrt{\pi})^2} = -\frac{1}{\pi}
$$
因此，$f(z)$ 在 $z \to 0^+$ 的主导行为是 $-\frac{1}{\pi}\ln z$。这个例子完美地展示了梅林-巴恩斯方法如何将函数在[实轴](@entry_id:148276)上的复杂奇异行为，转化为其[梅林变换](@entry_id:264063)在复平面上更为直观的极点结构。