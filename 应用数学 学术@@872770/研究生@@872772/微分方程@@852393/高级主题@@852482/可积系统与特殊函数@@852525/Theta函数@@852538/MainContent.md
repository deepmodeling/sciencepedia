## 引言
Theta函数是数学中一类极为深刻且优美的特殊函数，其重要性远超其最初在[椭圆积分](@entry_id:174434)研究中的应用。它们如同数学世界的 Rosetta 石碑，在数论、[代数几何](@entry_id:156300)、[数学物理](@entry_id:265403)等看似无关的领域之间建立了惊人的联系。然而，对于学习者而言，Theta函数的理论往往显得抽象，其在不同学科中的应用也显得零散，缺乏一个将核心原理与实际应用贯穿起来的系统性视角。本文旨在填补这一空白，引领读者踏上一段从理论到应用的探索之旅。我们将首先在“原理与机制”一章中，深入剖析Theta函数的核心解析性质与[模变换](@entry_id:184910)行为；接着，在“应用与交叉学科联系”中，我们将见证这些理论如何在数论、物理学等领域大放异彩；最后，通过一系列“动手实践”的例子，巩固和深化理解。让我们首先从构建这一切的基石——Theta函数的基本原理与内在机制开始。

## 原理与机制

本章将深入探讨[雅可比](@entry_id:264467)theta函数的核心性质，从它们的解析行为到在[模变换](@entry_id:184910)下的惊人对称性。我们将揭示这些函数所遵循的基本原理，并阐明其内在的数学机制。这些机制不仅是理论上的优美构造，更是解决从数论到理论物理等诸多领域问题的强大工具。

### 解析性质：[准周期性](@entry_id:272343)与[热方程](@entry_id:144435)

Theta函数作为复变函数，其解析性质构成了研究其结构的基础。其中两个最引人注目的性质是[准周期性](@entry_id:272343)和它们与热方程的深刻联系。

#### [准周期性](@entry_id:272343)

尽管theta函数是基于[傅里叶级数](@entry_id:139455)构建的，但它们并非在由[周期格](@entry_id:176756) $\mathbb{Z}\pi + \mathbb{Z}\pi\tau$ 生成的整个复平面上都具有严格的周期性。相反，它们表现出一种更为精妙的性质，称为**[准周期性](@entry_id:272343) (quasi-periodicity)**。这意味着当自变量 $z$ 平移一个[周期格](@entry_id:176756)向量时，函数值会乘以一个特定的因子，这个因子通常依赖于平移向量和自变量 $z$。

我们以第三[雅可比](@entry_id:264467)theta函数 $\theta_3(z, q)$ 为例来阐明这一点。其级数定义为：
$$
\theta_3(z, q) = \sum_{n=-\infty}^{\infty} q^{n^2} e^{2niz}
$$
其中 $q = e^{i\pi\tau}$，并且 $\mathrm{Im}(\tau) > 0$。现在，我们来考察当变量 $z$ 平移 $\pi\tau$ 时函数的行为：
$$
\begin{align*}
\theta_3(z + \pi\tau, q)  = \sum_{n=-\infty}^{\infty} q^{n^2} e^{2ni(z + \pi\tau)} \\
 = \sum_{n=-\infty}^{\infty} e^{i\pi n^2 \tau} e^{2niz} e^{2ni\pi\tau} \\
 = \sum_{n=-\infty}^{\infty} e^{i\pi \tau (n^2 + 2n)} e^{2niz}
\end{align*}
$$
通过对指数部分进行配方，我们得到 $n^2 + 2n = (n+1)^2 - 1$。代入上式：
$$
\begin{align*}
\theta_3(z + \pi\tau, q)  = \sum_{n=-\infty}^{\infty} e^{i\pi \tau ((n+1)^2 - 1)} e^{2niz} \\
 = e^{-i\pi\tau} \sum_{n=-\infty}^{\infty} e^{i\pi \tau (n+1)^2} e^{2niz}
\end{align*}
$$
为了使指数中的 $z$ 部分匹配，我们再进行一次代数变形 $e^{2niz} = e^{2i(n+1)z}e^{-2iz}$：
$$
\begin{align*}
\theta_3(z + \pi\tau, q)  = e^{-i\pi\tau} e^{-2iz} \sum_{n=-\infty}^{\infty} e^{i\pi \tau (n+1)^2} e^{2i(n+1)z} \\
 = q^{-1} e^{-2iz} \sum_{m=-\infty}^{\infty} e^{i\pi \tau m^2} e^{2imz} \quad (\text{令 } m=n+1) \\
 = q^{-1} e^{-2iz} \theta_3(z, q)
\end{align*}
$$
这个关系式 $\theta_3(z + \pi\tau, q) = q^{-1} e^{-2iz} \theta_3(z, q)$ 精确地描述了 $\theta_3$ 函数的[准周期性](@entry_id:272343)。它揭示了当变量 $z$ 沿着与 $\tau$ 相关的方向移动时，函数值如何以一种可预测的方式进行伸缩和旋转。

为了更具体地理解这一性质的应用，考虑一个计算任务：求 $\theta_3(\pi/2 + i\pi, e^{-\pi})$ 的精确值 [@problem_id:789880]。在这里，参数 $q = e^{-\pi}$，我们可以通过令 $q = e^{i\pi\tau}$ 来确定 $\tau$。显然，$i\pi\tau = -\pi$，所以 $\tau=i$。因此，平移量 $\pi\tau = i\pi$。我们还需要知道 $\theta_3$ 和 $\theta_4$ 之间的关系：$\theta_4(q) = \theta_3(\pi/2, q)$。利用[准周期性](@entry_id:272343)公式，设 $z=\pi/2$：
$$
\theta_3(\pi/2 + i\pi, e^{-\pi}) = (e^{-\pi})^{-1} e^{-2i(\pi/2)} \theta_3(\pi/2, e^{-\pi}) = e^{\pi} e^{-i\pi} \theta_4(e^{-\pi}) = -e^{\pi} \theta_4(e^{-\pi})
$$
如果我们已知 $\theta_4(e^{-\pi})$ 的特定值，例如 $\frac{\Gamma(1/4)}{2^{3/4}\pi^{3/4}}$，我们就可以立即得到 $\theta_3(\pi/2 + i\pi, e^{-\pi}) = -e^{\pi} \frac{\Gamma(1/4)}{2^{3/4}\pi^{3/4}}$。这个例子生动地展示了[准周期性](@entry_id:272343)如何成为计算和推导theta函数在特殊点值的有力工具。

#### [热方程](@entry_id:144435)

Theta函数与数学物理的联系远不止于形式上的相似。一个深刻的发现是，它们是**[一维热方程](@entry_id:175487) (heat equation)** 的解。这个性质揭示了变量 $z$（通常被视为“空间”变量）和 $\tau$（被视为“时间”或演化参数）之间的内在动力学关系。

对于雅可比theta函数，如 $\theta_1(z|\tau)$，其中 $q=e^{i\pi\tau}$，它满足以下[偏微分方程](@entry_id:141332)：
$$
4 \frac{\partial \theta_1(z|\tau)}{\partial \tau} = -i\pi \frac{\partial^2 \theta_1(z|\tau)}{\partial z^2}
$$
这个方程表明，函数对 $\tau$ 的变化率（可以想象成“热流”）正比于它对 $z$ 的[二阶导数](@entry_id:144508)（曲率或“热量[分布](@entry_id:182848)的不均匀性”）。这个令人惊讶的联系不仅为theta函数提供了一个全新的视角，还为计算它们的导数提供了捷径。

例如，考虑计算[混合偏导数](@entry_id:139334) $\frac{\partial^2}{\partial \tau \partial z} \theta_1(z|\tau)$ 在特定点 $(z, \tau) = (\pi/2, i\beta)$ 的值，其中 $\beta > 0$ [@problem_id:785164]。直接从级数定义出发进行计算会非常繁琐。然而，我们可以利用热方程。将[热方程](@entry_id:144435)两边对 $z$ 求导，我们得到：
$$
4 \frac{\partial^2 \theta_1}{\partial \tau \partial z} = -i\pi \frac{\partial^3 \theta_1}{\partial z^3} \quad \implies \quad \frac{\partial^2 \theta_1}{\partial \tau \partial z} = -\frac{i\pi}{4} \frac{\partial^3 \theta_1}{\partial z^3}
$$
现在，问题转化为计算 $\theta_1$ 对 $z$ 的三阶导数。回顾 $\theta_1$ 的级数定义：
$$
\theta_1(z|\tau) = 2 \sum_{n=0}^{\infty} (-1)^n q^{(n+1/2)^2} \sin((2n+1)z)
$$
对其求三次导数得到：
$$
\frac{\partial^3 \theta_1}{\partial z^3} = 2 \sum_{n=0}^{\infty} (-1)^n q^{(n+1/2)^2} [-(2n+1)^3 \cos((2n+1)z)]
$$
当 $z=\pi/2$ 时，对于所有整数 $n$，$\cos((2n+1)\pi/2)$ 都等于 $0$。因此，在 $z=\pi/2$ 这一点，$\frac{\partial^3 \theta_1}{\partial z^3}$ 恒为零，无论 $\tau$ 取何值。由此可得，[混合偏导数](@entry_id:139334)在这一点也为零。这个例子清晰地表明，热方程这样的[微分](@entry_id:158718)关系如何能极大地简化涉及theta函数的计算。

### 模性质：在 [SL(2,Z)](@entry_id:184647) 变换下的行为

Theta函数最深刻、最强大的性质体现在它们对**[模群](@entry_id:184647) (modular group)** $SL(2, \mathbb{Z})$ 作用的响应中。[模群](@entry_id:184647)由[行列式](@entry_id:142978)为1的 $2 \times 2$ 整数矩阵构成，它通过[分式线性变换](@entry_id:174812)作用于上半复平面 $\mathbb{H}$ 中的参数 $\tau$：
$$
\tau \mapsto \frac{a\tau + b}{c\tau + d}, \quad \begin{pmatrix} a  b \\ c  d \end{pmatrix} \in SL(2, \mathbb{Z})
$$
这种变换对应于描述[复环面](@entry_id:197937)（亏格为1的黎曼面）的不同但几何上等价的方式。Theta函数在这些变换下并非不变，而是以一种高度规律性的方式进行变换，这种性质被称为**模性 (modularity)**。研究[模群](@entry_id:184647)的行为，通常从其两个生成元开始：$T$ 变换（平移）和 $S$ 变换（反演）。

#### T变换：$\tau \to \tau+1$

$T$ 变换是最简单的[模变换](@entry_id:184910)，它对应于将 $\tau$ 平移一个单位。在 $q$ 的语言中，如果 $\tau' = \tau+1$，则 $q' = e^{i\pi(\tau+1)} = e^{i\pi\tau}e^{i\pi} = -q$。让我们以 $\theta_2(z|\tau)$ 为例，直接从其定义出发推导其变换规律 [@problem_id:885540]。
$$
\theta_2(z|\tau) = \sum_{n=-\infty}^{\infty} q^{(n+1/2)^2} e^{i(2n+1)z}
$$
将 $\tau$ 替换为 $\tau+1$：
$$
\theta_2(z|\tau+1) = \sum_{n=-\infty}^{\infty} e^{i\pi(\tau+1)(n+1/2)^2} e^{i(2n+1)z}
$$
我们可以将指数项 $e^{i\pi(\tau+1)(n+1/2)^2}$ 分解为两部分：
$$
e^{i\pi\tau(n+1/2)^2} \cdot e^{i\pi(n+1/2)^2}
$$
关键在于分析第二个因子。展开平方项 $(n+1/2)^2 = n^2 + n + 1/4 = n(n+1) + 1/4$。因为对于任意整数 $n$，$n(n+1)$ 总是偶数，所以 $e^{i\pi n(n+1)} = (e^{2\pi i})^k = 1$。因此，第二个因子简化为一个与 $n$ 无关的常数：
$$
e^{i\pi(n(n+1) + 1/4)} = e^{i\pi n(n+1)} \cdot e^{i\pi/4} = e^{i\pi/4}
$$
由于这个因子是常数，我们可以将它从求和中提出来：
$$
\theta_2(z|\tau+1) = e^{i\pi/4} \sum_{n=-\infty}^{\infty} e^{i\pi\tau(n+1/2)^2} e^{i(2n+1)z} = e^{i\pi/4} \theta_2(z|\tau)
$$
这个结果表明，在 $T$ 变换下，$\theta_2$ 函数仅仅被乘上了一个简单的四次单位根。其他theta函数也具有类似的简单变换行为。

#### S变换：$\tau \to -1/\tau$

$S$ 变换，即模反演，是[模群](@entry_id:184647)中一个更深刻、更强大的操作。它将 $\tau$ 映到 $-1/\tau$，在几何上对应于[交换环](@entry_id:148261)面的两个[基本周期](@entry_id:267619)。Theta函数在此变换下的行为揭示了其深刻的内在对称性，其推导通常需要借助**泊松求和公式 (Poisson Summation Formula, PSF)**。

PSF指出，对于一个“良好”的函数 $f(x)$（例如[施瓦茨函数](@entry_id:200976)），其在整数点上的求和等于其[傅里叶变换](@entry_id:142120)在整数点上的求和：
$$
\sum_{n=-\infty}^{\infty} f(n) = \sum_{k=-\infty}^{\infty} \hat{f}(k), \quad \text{其中 } \hat{f}(k) = \int_{-\infty}^{\infty} f(x) e^{-2\pi i k x} dx
$$
我们可以利用这个公式来推导theta常数 $\theta_3(0|\tau) = \sum_{n=-\infty}^\infty e^{i\pi n^2 \tau}$ 的 $S$ 变换性质 [@problem_id:785101]。令 $f(x) = e^{i\pi x^2 \tau}$。我们需要计算它的[傅里叶变换](@entry_id:142120)：
$$
\hat{f}(k) = \int_{-\infty}^{\infty} e^{i\pi x^2 \tau} e^{-2\pi i k x} dx
$$
这是一个[高斯积分](@entry_id:187139)。通过在指数上配方，并利用[高斯积分](@entry_id:187139)公式 $\int_{-\infty}^{\infty} e^{-ax^2} dx = \sqrt{\pi/a}$（其中 $\text{Re}(a)>0$），可以得到：
$$
\hat{f}(k) = \frac{1}{\sqrt{-i\tau}} e^{-i\pi k^2/\tau}
$$
应用PSF，我们有：
$$
\sum_{n=-\infty}^{\infty} e^{i\pi n^2 \tau} = \sum_{k=-\infty}^{\infty} \frac{1}{\sqrt{-i\tau}} e^{i\pi k^2 (-1/\tau)}
$$
左边是 $\theta_3(0|\tau)$。右边可以写成：
$$
\frac{1}{\sqrt{-i\tau}} \sum_{k=-\infty}^{\infty} e^{i\pi k^2 (-1/\tau)} = \frac{1}{\sqrt{-i\tau}} \theta_3(0|-1/\tau)
$$
于是我们得到了 $\theta_3$ 常数的 $S$ 变换公式：
$$
\theta_3(0|\tau) = \frac{1}{\sqrt{-i\tau}} \theta_3(0|-1/\tau) \quad \text{或} \quad \theta_3(0|-1/\tau) = \sqrt{-i\tau} \theta_3(0|\tau)
$$
这里的 $\sqrt{-i\tau}$ 是[主分支](@entry_id:164844)平方根。这个公式是模形式理论的基石之一。所有四个theta函数（包括含 $z$ 变量的）都有类似的变换法则。例如：
$$
\begin{aligned}
\vartheta_2(0|-1/\tau) = \sqrt{-i\tau} \, \vartheta_4(0|\tau) \\
\vartheta_3(0|-1/\tau) = \sqrt{-i\tau} \, \vartheta_3(0|\tau) \\
\vartheta_4(0|-1/\tau) = \sqrt{-i\tau} \, \vartheta_2(0|\tau)
\end{aligned}
$$
这些变换规则同样适用于theta函数的导数。例如，给定 $\vartheta_1(z, \tau)$ 的变换公式 $\vartheta_1(z/\tau, -1/\tau) = -i(-i\tau)^{1/2} e^{i\pi z^2/\tau} \vartheta_1(z, \tau)$，我们可以通过对 $z$ 求导并令 $z=0$ 来推导其导数在 $z=0$ 处的变换性质 [@problem_id:1161833]。经过计算可得：
$$
\vartheta_1'(0, -1/\tau) = (-i\tau)^{3/2} \vartheta_1'(0, \tau)
$$
注意，这里的因子是 $(-i\tau)^{3/2}$ 而不是 $(-i\tau)^{1/2}$。这个幂次的变化与**模权重 (modular weight)** 的概念密切相关，导数操作会改变函数的模权重。

### 恒等式与应用

Theta函数的丰富结构导致了大量深刻而优美的恒等式。这些恒等式不仅具有内在的数学美感，而且在应用中极为强大。

#### 加法公式与[傅里叶分析](@entry_id:137640)

Theta函数满足多种类型的加法公式，这些公式可以将函数的乘积分解为函数的和。例如，下面这个恒等式连接了 $\vartheta_2$ 和 $\vartheta_3$：
$$
\vartheta_3(u,q)\vartheta_3(v,q) = \vartheta_3(u+v, q^2)\vartheta_3(u-v, q^2) + \vartheta_2(u+v, q^2)\vartheta_2(u-v, q^2)
$$
这类恒等式在傅里叶分析中非常有用。考虑函数 $f(x) = \vartheta_3(x+\alpha; q) \vartheta_3(x-\alpha; q)$ [@problem_id:415250]。直接计算其[傅里叶系数](@entry_id:144886)是困难的。但通过应用上述加法公式（令 $u=x+\alpha, v=x-\alpha$），我们得到：
$$
f(x) = \vartheta_3(2x, q^2)\vartheta_3(2\alpha, q^2) + \vartheta_2(2x, q^2)\vartheta_2(2\alpha, q^2)
$$
在这个表达式中，$\vartheta_3(2\alpha, q^2)$ 和 $\vartheta_2(2\alpha, q^2)$ 是常数。$\vartheta_3(2x, q^2)$ 和 $\vartheta_2(2x, q^2)$ 的[级数展开](@entry_id:142878)式本身就是[傅里叶级数](@entry_id:139455)的形式。通过将它们的级数定义代入，并与目标傅里叶级数 $f(x) = \sum c_n e^{i2nx}$ 进行比较，我们可以直接读出系数 $c_n$。这种方法将一个复杂函数的[傅里叶分析](@entry_id:137640)问题，通过一个代数恒等式，转化为一个简单的系数[匹配问题](@entry_id:275163)。

#### 与其他[特殊函数](@entry_id:143234)的关联

Theta函数与其他重要的[特殊函数](@entry_id:143234)（如戴德金eta函数）之间存在着深刻的联系。**戴德金eta函数 (Dedekind eta function)** $\eta(\tau)$ 定义为：
$$
\eta(\tau) = q^{1/24} \prod_{n=1}^{\infty} (1 - q^n), \quad \text{其中 } q = e^{2\pi i \tau}
$$
它与theta常数通过**[雅可比恒等式](@entry_id:140480) (Jacobi's identity)** 联系在一起：
$$
\vartheta_2(0|\tau) \vartheta_3(0|\tau) \vartheta_4(0|\tau) = 2\eta(\tau)^3
$$
(注意，这里的 $q$ 定义与theta函数中的 $q=e^{i\pi\tau}$ 有所不同，使用 $\tau$ 作为变量可以避免混淆)。这个恒等式是连接求和与乘积世界的桥梁。更重要的是，我们可以利用它来推导 $\eta$ 函数的模性质 [@problem_id:650904]。将 $\tau$ 替换为 $-1/\tau$：
$$
\vartheta_2(0|-1/\tau) \vartheta_3(0|-1/\tau) \vartheta_4(0|-1/\tau) = 2\eta(-1/\tau)^3
$$
现在，使用我们已知的theta常数的S变换规则代入左侧：
$$
(\sqrt{-i\tau} \vartheta_4(0|\tau)) (\sqrt{-i\tau} \vartheta_3(0|\tau)) (\sqrt{-i\tau} \vartheta_2(0|\tau)) = (-i\tau)^{3/2} \vartheta_2 \vartheta_3 \vartheta_4 = (-i\tau)^{3/2} (2\eta(\tau)^3)
$$
比较两边，我们得到：
$$
2\eta(-1/\tau)^3 = (-i\tau)^{3/2} (2\eta(\tau)^3) \quad \implies \quad \eta(-1/\tau) = \sqrt{-i\tau} \eta(\tau)
$$
这个例子完美地展示了如何利用已知函数的性质，通过代数恒等式来推导出新函数的性质。

#### 利用模形式理论证明恒等式

模性质最强大的应用之一是证明看似深奥的代数恒等式。其核心思想是，特定权重和群的**[模形式](@entry_id:160014) (modular forms)** 构成的[向量空间](@entry_id:151108)是有限维的。如果我们可以证明一个表达式是一个模形式，并且它在一个基底下的坐标是唯一的，我们就可以通过在几个点（或在极限情况下）比较函数值来确定这个表达式。

一个经典的例子是证明**[雅可比](@entry_id:264467)晦涩恒等式 (Jacobi's abstruse identity)**：
$$
\theta_2(0|\tau)^4 - \theta_3(0|\tau)^4 + \theta_4(0|\tau)^4 = 0
$$
直接从级数定义证明这个恒等式极其困难。然而，我们可以利用模形式的框架 [@problem_id:785057]。已知 $\theta_2^4, \theta_3^4, \theta_4^4$ 都是[模群](@entry_id:184647)的某个[子群](@entry_id:146164) $\Gamma(2)$ 的权重为2的[模形式](@entry_id:160014)。该空间 $M_2(\Gamma(2))$ 是二维的，可以由 $\{\theta_3^4, \theta_4^4\}$ 作为基底。因此，$\theta_2^4$ 必然可以写成它们的线性组合：
$$
\theta_2(\tau)^4 = C_1 \theta_3(\tau)^4 + C_2 \theta_4(\tau)^4
$$
为了确定常数 $C_1$ 和 $C_2$，我们利用 $S$ 变换。对上式两边同时进行 $\tau \to -1/\tau$ 变换，并代入theta四次方的变换规则（例如 $\theta_2(-1/\tau)^4 = (-i\tau)^2 \theta_4(\tau)^4$），我们得到一个新的关系：
$$
\theta_4(\tau)^4 = C_1 \theta_3(\tau)^4 + C_2 \theta_2(\tau)^4
$$
我们现在有两个关于 $\theta_k^4$ 的[线性方程](@entry_id:151487)。从第一个方程减去第二个方程，可以解得 $C_2 = -1$。
为了确定 $C_1$，我们可以考察在[尖点](@entry_id:636792) $\tau \to i\infty$ 处的行为。此时 $q = e^{i\pi\tau} \to 0$。根据级数定义，我们有极限：
$$
\theta_2(\tau) \to 0, \quad \theta_3(\tau) \to 1, \quad \theta_4(\tau) \to 1
$$
将这些极限值代入初始关系式 $\theta_2^4 = C_1 \theta_3^4 + C_2 \theta_4^4$，我们得到：
$$
0^4 = C_1 \cdot 1^4 + (-1) \cdot 1^4 \quad \implies \quad 0 = C_1 - 1 \quad \implies \quad C_1 = 1
$$
因此，我们证明了 $\theta_2(\tau)^4 = 1 \cdot \theta_3(\tau)^4 - 1 \cdot \theta_4(\tau)^4$，这正是雅可比晦涩恒等式。这个证明过程彰显了从抽象代数结构（[模形式空间](@entry_id:199790)）推导具体解析恒等式的巨大威力。

### 推广：黎曼Theta函数

[雅可比](@entry_id:264467)theta函数是与亏格为1的黎曼面（[复环面](@entry_id:197937)）相关的函数。这一概念可以自然地推广到任意亏格 $g$ 的黎曼面，从而引出**[黎曼theta函数](@entry_id:188911) (Riemann theta function)**。

亏格为 $g$ 的[黎曼theta函数](@entry_id:188911)带有特征 $[\delta, \epsilon]$，其定义如下：
$$
\theta \begin{bmatrix} \delta \\ \epsilon \end{bmatrix} (z | \Omega) = \sum_{n \in \mathbb{Z}^g} \exp \left( i\pi (n+\delta)^T \Omega (n+\delta) + 2\pi i (n+\delta)^T (z+\epsilon) \right)
$$
这里的 $z \in \mathbb{C}^g$ 是 $g$ 维[复向量](@entry_id:192851)，$\Omega$ 是一个 $g \times g$ 的对称[复矩阵](@entry_id:190650)，其虚部正定，称为**周期矩阵 (period matrix)**。$\delta, \epsilon \in \mathbb{R}^g$ 是构成**特征 (characteristic)** 的实向量。

正如雅可比theta函数的模参数 $\tau$ 受到 $SL(2, \mathbb{Z})$ 的作用，[黎曼theta函数](@entry_id:188911)的周期矩阵 $\Omega$ 也受到**[辛群](@entry_id:189031) (symplectic group)** $Sp(2g, \mathbb{Z})$ 的作用。在这种变换下，不仅周期矩阵会改变，[特征向量](@entry_id:151813) $[\delta, \epsilon]$ 自身也会根据特定的规则进行变换。

对于一个[辛矩阵](@entry_id:142706) $M = \begin{pmatrix} A  B \\ C  D \end{pmatrix} \in Sp(2g, \mathbb{Z})$，特征的变换法则是 [@problem_id:1161841]：
$$
\begin{pmatrix} \delta' \\ \epsilon' \end{pmatrix} = \begin{pmatrix} D  -C \\ -B  A \end{pmatrix} \begin{pmatrix} \delta \\ \epsilon \end{pmatrix} + \frac{1}{2} \begin{pmatrix} \text{diag}(CD^T) \\ \text{diag}(AB^T) \end{pmatrix}
$$
其中 $\text{diag}(M)$ 表示由矩阵 $M$ 的对角线元素构成的列向量。

考虑一个亏格 $g=2$ 的系统，从零特征 $\delta=0, \epsilon=0$ 开始。施加一个由 $M = \begin{pmatrix} I  S \\ T  TS+I \end{pmatrix}$ 定义的辛变换，其中 $S, T$ 是对称整数矩阵。根据变换法则，新的特征 $\delta'$ 将由下式给出：
$$
\delta' = \frac{1}{2} \text{diag}(CD^T) = \frac{1}{2} \text{diag}(T(ST+I)^T) = \frac{1}{2} (\text{diag}(TST^T) + \text{diag}(T))
$$
通过直接的矩阵计算，可以得到 $\delta'$ 的具体表达式。这个例子揭示了高亏格情况下[模变换](@entry_id:184910)的复杂性和丰富性，为我们打开了通往西格尔[模形式](@entry_id:160014)和[阿贝尔簇](@entry_id:183511)理论的窗口。