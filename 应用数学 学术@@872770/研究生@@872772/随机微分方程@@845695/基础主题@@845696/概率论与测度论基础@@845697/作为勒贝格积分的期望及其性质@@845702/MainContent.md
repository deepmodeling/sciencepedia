## 引言
在[随机过程](@entry_id:159502)和[金融数学](@entry_id:143286)的研究中，“期望”是一个无处不在的概念，直观上代表了[随机变量](@entry_id:195330)的“平均”或“中心趋势”。然而，这种直觉理解在处理复杂的[随机系统](@entry_id:187663)，尤其是涉及连续时间和无限可能性的[随机微分方程](@entry_id:146618)（SDE）时，会遇到严峻的挑战。为了构建一个坚实可靠的理论框架，我们必须超越初等概率论中的求和或黎曼积分，转向一个更为强大和普适的定义。本文旨在填补这一认知鸿沟，系统阐述如何将期望严格地定义为[勒贝格积分](@entry_id:140189)，并揭示这一定义所带来的深刻理论力量。

本文将分为三个核心章节，引导读者逐步深入这一主题。
- 在**“原理与机制”**一章中，我们将回归本源，从 Andrey Kolmogorov 建立的概率空间公理出发，分步构建勒贝格积分的定义：从简单函数到非负[随机变量](@entry_id:195330)，再到一般的可积[随机变量](@entry_id:195330)。我们还将探讨期望的基本性质、重要的收敛定理（如[控制收敛定理](@entry_id:137784)）以及[条件期望](@entry_id:159140)这一关键推广。
- 接下来，在**“应用与跨学科联系”**一章中，我们将展示这些抽象原理的实际威力。您将看到期望的 $L^2$ 理论如何支撑起伊藤积分和[随机微分方程](@entry_id:146618)的整个体系，并理解测度论的严谨性为何在避免理论陷阱中至关重要。此外，我们还将探索这一框架如何在量子力学、信号处理和[计算生物学](@entry_id:146988)等领域提供统一的分析语言。
- 最后，**“动手实践”**部分提供了一系列精心设计的问题，旨在通过具体计算和反例构造，帮助您巩固对逼近理论、[可积性](@entry_id:142415)条件以及收敛定理的理解，将理论知识转化为解决问题的能力。

## 原理与机制

在[随机分析](@entry_id:188809)领域，尤其是在[随机微分方程](@entry_id:146618)（SDE）的研究中，期望的概念是不可或缺的。它不仅为[随机变量](@entry_id:195330)的“平均值”提供了严格的数学基础，而且是定义[鞅](@entry_id:267779)、[随机积分](@entry_id:198356)和分析[随机过程](@entry_id:159502)长期行为等核心工具的基石。本章旨在深入阐释期望作为勒贝格积分的原理与机制，从其[测度论](@entry_id:139744)基础出发，系统地构建其定义，探讨其关键性质，并阐明其在[随机分析](@entry_id:188809)中的应用。

### 概率论的[测度论](@entry_id:139744)基础

期望的严格定义根植于测度论。一切的起点是一个**[概率空间](@entry_id:201477)** $(\Omega, \mathcal{F}, \mathbb{P})$，这是由现代[概率论公理](@entry_id:198155)化的奠基人 Andrey Kolmogorov 建立的框架。

一个概率空间由三个部分构成 [@problem_id:2975005]：
1.  **[样本空间](@entry_id:275301)** $\Omega$：一个非空集合，其元素 $\omega$ 代表所有可能的结果。
2.  **事件域** $\mathcal{F}$：$\Omega$ 上的一个 **$\sigma$-代数**。它是一个由 $\Omega$ 的[子集](@entry_id:261956)（称为**事件**）组成的集合，满足以下条件：$\Omega \in \mathcal{F}$；若 $A \in \mathcal{F}$，则其补集 $A^c \in \mathcal{F}$；若 $\{A_n\}_{n=1}^\infty$ 是 $\mathcal{F}$ 中的一个可数集族，则它们的并集 $\cup_{n=1}^\infty A_n$ 也在 $\mathcal{F}$ 中。$\sigma$-代数确保了我们能够对我们关心的事件进行逻辑运算（补、可数并、可数交）。
3.  **[概率测度](@entry_id:190821)** $\mathbb{P}$：一个在 $\mathcal{F}$ 上定义的函数 $\mathbb{P}: \mathcal{F} \to [0, 1]$，满足 $\mathbb{P}(\Omega) = 1$ 和**[可数可加性](@entry_id:186580)**。[可数可加性](@entry_id:186580)指的是，对于 $\mathcal{F}$ 中任意一列两两不交的事件 $\{A_n\}_{n=1}^\infty$，我们有 $\mathbb{P}(\cup_{n=1}^\infty A_n) = \sum_{n=1}^\infty \mathbb{P}(A_n)$。这一性质是构建[勒贝格积分](@entry_id:140189)理论的关键，它比[有限可加性](@entry_id:204532)更强。

在此框架下，一个**实值[随机变量](@entry_id:195330)** $X$ 被定义为一个从样本空间到实数集的**[可测函数](@entry_id:159040)**，即 $X: (\Omega, \mathcal{F}) \to (\mathbb{R}, \mathcal{B}(\mathbb{R}))$。其中 $\mathcal{B}(\mathbb{R})$ 是实数集 $\mathbb{R}$ 上的**波莱尔 $\sigma$-代数**，即包含所有开集的最小 $\sigma$-代数。$X$ 的可测性意味着对于任意波莱尔集 $B \in \mathcal{B}(\mathbb{R})$，其原像 $X^{-1}(B) = \{\omega \in \Omega \mid X(\omega) \in B\}$ 必须是一个事件，即 $X^{-1}(B) \in \mathcal{F}$。这个条件保证了我们可以讨论诸如“[随机变量](@entry_id:195330) $X$ 的值小于等于 $c$”这样的事件的概率，因为事件 $\{\omega \mid X(\omega) \le c\}$ 对应于原像 $X^{-1}((-\infty, c])$，而 $(-\infty, c]$ 是一个波莱尔集。

**[可测性](@entry_id:199191)**是定义期望的绝对前提。如果一个函数不是可测的，那么其勒贝格积分（即期望）在标准理论中是无定义的。[@problem_id:2974997] 考虑一个简单的例子：设概率空间为 $(\Omega, \mathcal{F}, \mathbb{P})$，其中 $\Omega=[0,1]$，$\mathcal{F}=\{\emptyset, \Omega\}$ 是平凡 $\sigma$-代数，$\mathbb{P}(\emptyset)=0, \mathbb{P}(\Omega)=1$。定义函数 $X(\omega) = \omega$。那么对于波莱尔集 $B=[0, 0.5]$，其[原像](@entry_id:150899) $X^{-1}(B)=[0, 0.5]$ 既不是 $\emptyset$ 也不是 $\Omega$，因此不属于 $\mathcal{F}$。所以，$X$ 不是 $\mathcal{F}$-可测的，我们无法为其定义期望。另一个著名的例子是利用[选择公理](@entry_id:150647)构造的**[维塔利集](@entry_id:144157) (Vitali set)** $V \subset [0,1]$，它对于勒贝格测度是不可测的。如果我们在波莱尔 $\sigma$-代数 $\mathcal{B}([0,1])$ 上考虑[勒贝格测度](@entry_id:139781)，[维塔利集](@entry_id:144157) $V$ 就不是一个波莱尔集。因此，指示函数 $X(\omega) = \mathbf{1}_V(\omega)$ 就不是一个可测函数，其期望也无从谈起。[@problem_id:2974997]

### 将期望定义为勒贝格积分

一旦[随机变量](@entry_id:195330)被定义为可测函数，其期望就可以通过勒贝格积分来构建。这个构建过程分三步进行。

#### 第一步：简单函数

构建的起点是**[简单函数](@entry_id:137521)**。一个[简单函数](@entry_id:137521)是指一个只取有限个不同值的可测函数。任何这样的函数都可以写成标准形式 $s = \sum_{i=1}^m c_i \mathbf{1}_{C_i}$，其中 $c_i$ 是 $s$ 的不同取值，而 $C_i = \{\omega \mid s(\omega)=c_i\}$ 是一个由不相交的[可测集](@entry_id:159173)构成的对 $\Omega$ 的划分。对于一个非负简单函数（即所有 $c_i \ge 0$），其期望（积分）被**定义**为：
$$
\mathbb{E}[s] := \int_\Omega s \,d\mathbb{P} = \sum_{i=1}^m c_i \mathbb{P}(C_i)
$$
这个定义直观地反映了期望是“取值”与“概率”的加权平均。

一个更普遍的表示形式是 $s = \sum_{k=1}^n a_k \mathbf{1}_{A_k}$，其中 $A_k$ 是可测集，但不一定两两不交。通过利用测度的可加性，可以证明上述定义等价于一个更方便的计算公式 [@problem_id:2975026]：
$$
\mathbb{E}[s] = \sum_{k=1}^n a_k \mathbb{P}(A_k)
$$
这个公式揭示了期望的**线性**本质，它是勒贝格积分最重要的性质之一。例如，考虑一个由[标准布朗运动](@entry_id:197332) $(W_t)_{t \ge 0}$ 生成的简单[随机变量](@entry_id:195330) $s = 2\mathbf{1}_{A_1} - \mathbf{1}_{A_2} + 3\mathbf{1}_{A_3}$，其中 $A_1=\{W_1\ge 0, W_2\ge 0\}$, $A_2=\{W_1\ge 0, W_20\}$, $A_3=\{W_10, W_2\ge 0\}$。利用布朗运动增量的独立性和正态性，我们可以计算出 $\mathbb{P}(A_1) = \frac{3}{8}$, $\mathbb{P}(A_2) = \frac{1}{8}$, $\mathbb{P}(A_3) = \frac{1}{8}$。根据上述公式，其期望为 $\mathbb{E}[s] = 2(\frac{3}{8}) - 1(\frac{1}{8}) + 3(\frac{1}{8}) = 1$。[@problem_id:2975026]

#### 第二步：非负[随机变量](@entry_id:195330)

对于任意一个非负可测[随机变量](@entry_id:195330) $X: \Omega \to [0, \infty]$，它的期望被定义为所有不超过 $X$ 的非负[简单函数](@entry_id:137521) $s$ 的期望的[上确界](@entry_id:140512)：
$$
\mathbb{E}[X] := \sup \left\{ \int_\Omega s \,d\mathbb{P} \mid s \text{ 是简单函数}, 0 \le s \le X \right\}
$$
这个定义是勒贝格积分理论的核心。幸运的是，我们不必每次都通过计算[上确界](@entry_id:140512)来求期望。测度论的一个基本结果是，任何[非负可测函数](@entry_id:192146) $X$ 都可以被一个单调递增的非负简单函数序列 $\{s_n\}$ 逐点逼近，即 $s_n(\omega) \uparrow X(\omega)$ 对所有 $\omega$ 成立。而**[单调收敛定理](@entry_id:147772) (Monotone Convergence Theorem, MCT)** 保证了在这种情况下，期望的极限等于极限的期望 [@problem_id:2974989]：
$$
\lim_{n\to\infty} \mathbb{E}[s_n] = \mathbb{E}[X]
$$
更一般地，对于任意一列满足 $0 \le X_n \uparrow X$ 的非负[随机变量](@entry_id:195330)，我们都有 $\mathbb{E}[X_n] \uparrow \mathbb{E}[X]$。MCT 是连接抽象定义与实际计算的桥梁。

#### 第三步：可积[随机变量](@entry_id:195330)

对于一个取值为正或负的普通实值[随机变量](@entry_id:195330) $X$，我们通过将其分解为**正部**和**负部**来定义其期望。$X$ 的正部定义为 $X^+(\omega) = \max\{X(\omega), 0\}$，负部定义为 $X^-(\omega) = \max\{-X(\omega), 0\}$。[@problem_id:2975002] 这两个函数都是非负的，并且我们有以下重要的恒等式：
$$
X = X^+ - X^- \quad \text{以及} \quad |X| = X^+ + X^-
$$
一个[随机变量](@entry_id:195330) $X$ 被称为**可积的 (integrable)**，或者说属于 $L^1(\mathbb{P})$ 空间，当且仅当其[绝对值](@entry_id:147688)的期望是有限的，即 $\mathbb{E}[|X|]  \infty$。由于 $|X|=X^++X^-$ 以及期望对非负[随机变量](@entry_id:195330)的线性，这个条件等价于要求 $\mathbb{E}[X^+]$ 和 $\mathbb{E}[X^-]$ **都**是有限的。[@problem_id:2975005] [@problem_id:2975002]

如果 $X$ 是可积的，其期望被定义为：
$$
\mathbb{E}[X] := \mathbb{E}[X^+] - \mathbb{E}[X^-]
$$
值得注意的是，如果 $\mathbb{E}[X^+]$ 和 $\mathbb{E}[X^-]$ 中只有一个是有限的，期望也可以被定义为一个扩展实数（$\infty$ 或 $-\infty$），但此时 $X$ 并不可积。如果两者都是无限的，则期望是形如 $\infty - \infty$ 的[未定式](@entry_id:144301)，此时[勒贝格积分](@entry_id:140189)是**无定义的**。因此，不可能存在一个[随机变量](@entry_id:195330) $X$ 使得 $\mathbb{E}[X]$ 有明确的有限值（如 $0$），但其[绝对值](@entry_id:147688)的期望 $\mathbb{E}[|X|] = \mathbb{E}[X^+] + \mathbb{E}[X^-]$ 却是无穷大。[@problem_id:2975002]

### 基本性质与计算工具

基于勒贝格积分的定义，期望继承了积分的一系列强[大性](@entry_id:268856)质，这些性质是进行[随机分析](@entry_id:188809)的基石。

#### 线性与[单调性](@entry_id:143760)

对于任意可积[随机变量](@entry_id:195330) $X, Y$ 和实数 $a, b$，期望算子是线性的：
$$
\mathbb{E}[aX + bY] = a\mathbb{E}[X] + b\mathbb{E}[Y]
$$
同时，期望是保序的（**[单调性](@entry_id:143760)**）：如果 $X \le Y$ [几乎处处](@entry_id:146631)（即在一个概率为1的集合上成立），那么 $\mathbb{E}[X] \le \mathbb{E}[Y]$。[@problem_id:2974989]

#### [变量替换公式](@entry_id:139692)

在实践中，我们通常不知道底层的[概率空间](@entry_id:201477) $(\Omega, \mathcal{F}, \mathbb{P})$，但知道[随机变量](@entry_id:195330) $X$ 的**[分布](@entry_id:182848)**或**定律**，即它在实数轴上的[概率测度](@entry_id:190821) $\mu_X$，定义为 $\mu_X(A) = \mathbb{P}(X \in A)$。一个极为重要的结果是**[变量替换公式](@entry_id:139692)**（有时被称为“无意识统计学家定律”），它允许我们直接在 $X$ 的值域（[实数轴](@entry_id:147286)）上计算其期望 [@problem_id:2975028]：
$$
\mathbb{E}[X] = \int_\Omega X \,d\mathbb{P} = \int_{\mathbb{R}} x \,d\mu_X(x)
$$
这个公式可以通过标准的三步法（指示函数 $\to$ 简单函数 $\to$ 非负函数 $\to$ [可积函数](@entry_id:191199)）从第一性原理推导出来。如果 $X$ 的[分布](@entry_id:182848)是关于[勒贝格测度](@entry_id:139781)绝对连续的，即存在概率密度函数 (PDF) $\rho(x)$，那么 $d\mu_X(x) = \rho(x)dx$，上式就变成了我们更熟悉的形式：$\mathbb{E}[X] = \int_{-\infty}^{\infty} x \rho(x) dx$。

例如，在满足 $2\kappa\theta > \sigma^2$ 条件下的 Cox-Ingersoll-Ross (CIR) 过程 $dX_t = \kappa(\theta-X_t)dt + \sigma\sqrt{X_t}dW_t$ 中，其[稳态分布](@entry_id:149079)是参数为 $\alpha = 2\kappa\theta/\sigma^2$ 和 $\beta = \sigma^2/(2\kappa)$ 的 Gamma [分布](@entry_id:182848)。利用[变量替换公式](@entry_id:139692)，我们可以通过计算积分 $\int_0^\infty x \rho(x) dx$ 来求其均值，结果恰好为 $\theta$，这证实了参数 $\theta$ 在模型中作为长期均值的作用。[@problem_id:2975028]

#### Jensen 不等式

**Jensen 不等式**是关于期望和[凸函数](@entry_id:143075)的一个深刻结果。如果 $g: \mathbb{R} \to \mathbb{R}$ 是一个**凸函数**（例如 $g(x)=x^2, g(x)=e^x$），$X$ 是一个可积[随机变量](@entry_id:195330)且 $g(X)$ 也可积，则有：
$$
g(\mathbb{E}[X]) \le \mathbb{E}[g(X)]
$$
这个不等式源于凸函数的一个几何性质：函数图像总位于其任意一点的[切线](@entry_id:268870)（或更一般地，支撑线）之上。即对任意 $x_0$，存在 $m$ 使得 $g(x) \ge g(x_0) + m(x - x_0)$ 对所有 $x$ 成立。令 $x_0 = \mathbb{E}[X]$ 并代入 $X$，再对两边取期望，即可得到该不等式。[@problem_id:1360946] Jensen 不等式在金融（风险厌恶）、信息论（熵）和统计学等领域有广泛应用。

### 期望的收敛性

在[随机分析](@entry_id:188809)中，我们经常需要处理[随机变量](@entry_id:195330)序列的极限。一个核心问题是：如果 $X_n \to X$，是否一定有 $\mathbb{E}[X_n] \to \mathbb{E}[X]$？答案是否定的，简单地[交换极限](@entry_id:141487)和期望运算是危险的。

考虑一个经典的例子：在[概率空间](@entry_id:201477) $([0,1], \mathcal{B}([0,1]), \lambda)$（其中 $\lambda$ 是[勒贝格测度](@entry_id:139781)）上定义序列 $X_n(\omega) = n \mathbf{1}_{(0, 1/n]}(\omega)$。[@problem_id:2975001] 对于任意固定的 $\omega \in (0,1]$，当 $n$ 足够大时，$1/n  \omega$，因此 $X_n(\omega) = 0$。对于 $\omega=0$，$X_n(0)$ 始终为 $0$。所以，该序列处处收敛到 $0$，即 $\lim_{n\to\infty} X_n = 0$。然而，对于任意 $n$，其期望为：
$$
\mathbb{E}[X_n] = \int_0^1 n \mathbf{1}_{(0, 1/n]}(\omega) d\lambda(\omega) = n \cdot \lambda((0, 1/n]) = n \cdot \frac{1}{n} = 1
$$
因此，我们得到 $\mathbb{E}[\lim_{n\to\infty} X_n] = \mathbb{E}[0] = 0$，而 $\lim_{n\to\infty} \mathbb{E}[X_n] = \lim_{n\to\infty} 1 = 1$。两者并不相等。

这个例子表明，要[交换极限](@entry_id:141487)与期望，需要额外的条件。测度论提供了三个主要的收敛定理：
1.  **[单调收敛定理](@entry_id:147772) (MCT)**：如果 $0 \le X_n \uparrow X$ 几乎处处，则 $\mathbb{E}[X_n] \to \mathbb{E}[X]$。
2.  **[法图引理](@entry_id:147006) (Fatou's Lemma)**：如果 $X_n \ge 0$ [几乎处处](@entry_id:146631)，则 $\mathbb{E}[\liminf_{n\to\infty} X_n] \le \liminf_{n\to\infty} \mathbb{E}[X_n]$。
3.  **[控制收敛定理](@entry_id:137784) (Dominated Convergence Theorem, DCT)**：如果 $X_n \to X$ 几乎处处，并且存在一个**可积的**[随机变量](@entry_id:195330) $Y$ (即 $\mathbb{E}[|Y|]  \infty$) 使得 $|X_n| \le Y$ 对所有 $n$ 几乎处处成立，则 $\lim_{n\to\infty} \mathbb{E}[X_n] = \mathbb{E}[X]$。
在上述 $X_n = n \mathbf{1}_{(0, 1/n]}$ 的例子中，交换失败的原因是无法找到一个可积的[控制函数](@entry_id:183140) $Y$。任何[控制函数](@entry_id:183140)都必须满足 $Y(\omega) \ge \sup_n X_n(\omega) = \lfloor 1/\omega \rfloor$，而函数 $\lfloor 1/\omega \rfloor$ 在 $[0,1]$ 上是不可积的。[@problem_id:2975001]

#### [一致可积性](@entry_id:199715)

[控制收敛定理](@entry_id:137784)的条件有时过于严格。一个更普遍且在许多[随机分析](@entry_id:188809)问题中至关重要的概念是**[一致可积性](@entry_id:199715) (Uniform Integrability)**。一个[随机变量](@entry_id:195330)族 $\mathcal{X} \subset L^1(\mathbb{P})$ 被称为[一致可积](@entry_id:202893)的，如果：
$$
\lim_{M\to\infty} \sup_{X \in \mathcal{X}} \int_{\{|X| > M\}} |X| \,d\mathbb{P} = 0
$$
这直观地意味着族中所有[随机变量](@entry_id:195330)的“尾部”对期望的贡献可以被一致地控制得很小。[@problem_id:2975004]

[一致可积性](@entry_id:199715)的核心作用体现在 **Vitali 收敛定理**中：序列 $X_n$ 在 $L^1$ 中收敛于 $X$ (即 $\mathbb{E}[|X_n - X|] \to 0$) 的充要条件是 $X_n$ [依概率收敛](@entry_id:145927)于 $X$ 且 $\{X_n\}$ 是[一致可积](@entry_id:202893)的。由于 $|\mathbb{E}[X_n] - \mathbb{E}[X]| \le \mathbb{E}[|X_n - X|]$， $L^1$ 收敛自然保证了期望的收敛。[@problem_id:2975004]

此外，**Dunford-Pettis 定理**指出，在[概率空间](@entry_id:201477)上，一个集合是[一致可积](@entry_id:202893)的当且仅当它在 $L^1$ 中是相对弱紧的。这意味着[一致可积性](@entry_id:199715)保证了我们可以从序列中提取出一个[弱收敛](@entry_id:146650)的[子序列](@entry_id:147702)。值得注意的是，如果 $X_n \rightharpoonup X_T$ 在 $L^1$ 中[弱收敛](@entry_id:146650)，那么期望的收敛 $\mathbb{E}[X_n] \to \mathbb{E}[X_T]$ 是直接成立的，因为这相当于用常数函数 $Y=1 \in L^\infty$ 对序列进行检验。[@problem_id:2975004]

### 推广：[条件期望](@entry_id:159140)

期望的概念可以被推广到**条件期望**，它形式化了“在给定部分信息的情况下对一个[随机变量](@entry_id:195330)的最佳估计”这一思想。设 $X$ 是一个可积[随机变量](@entry_id:195330)，$\mathcal{G}$ 是 $\mathcal{F}$ 的一个子 $\sigma$-代数，代表我们拥有的信息。$X$ 关于 $\mathcal{G}$ 的条件期望，记为 $\mathbb{E}[X \mid \mathcal{G}]$，被定义为一个满足以下两个条件的[随机变量](@entry_id:195330) $Y$ [@problem_id:2974994]：
1.  **可测性**：$Y$ 是 $\mathcal{G}$-可测的（即 $Y$ 的值完全由 $\mathcal{G}$ 中的信息确定）。
2.  **积分性质**：对于任意事件 $G \in \mathcal{G}$，都有 $\int_G Y \,d\mathbb{P} = \int_G X \,d\mathbb{P}$。

**Radon-Nikodym 定理**保证了这样的[随机变量](@entry_id:195330) $Y$ 存在且是**几乎处处唯一**的。这意味着任何两个满足条件的[随机变量](@entry_id:195330)，只可能在一个概率为零的集合上不相等。[@problem_id:2974994]

[条件期望](@entry_id:159140)具有许多与普通期望平行的性质，例如：
- **线性性**：$\mathbb{E}[aX+bY \mid \mathcal{G}] = a\mathbb{E}[X \mid \mathcal{G}] + b\mathbb{E}[Y \mid \mathcal{G}]$。
- **单调性**：若 $X \le Y$，则 $\mathbb{E}[X \mid \mathcal{G}] \le \mathbb{E}[Y \mid \mathcal{G}]$。
- **提出已知信息**：如果 $X$ 本身是 $\mathcal{G}$-可测的，那么 $\mathbb{E}[X \mid \mathcal{G}] = X$。[@problem_id:2974994]
- **独立性**：如果 $X$ 与 $\mathcal{G}$ [相互独立](@entry_id:273670)，那么 $\mathbb{E}[X \mid \mathcal{G}] = \mathbb{E}[X]$。[@problem_id:2974994]
- **[塔性质](@entry_id:273153)** (Tower Property)：若 $\mathcal{H} \subset \mathcal{G}$，则 $\mathbb{E}[\mathbb{E}[X \mid \mathcal{G}] \mid \mathcal{H}] = \mathbb{E}[X \mid \mathcal{H}]$。
- **条件 Jensen 不等式**：对于[凸函数](@entry_id:143075) $\varphi$，有 $\varphi(\mathbb{E}[X \mid \mathcal{G}]) \le \mathbb{E}[\varphi(X) \mid \mathcal{G}]$。[@problem_id:2974994]

在[随机微分方程理论](@entry_id:202918)中，条件期望是定义和分析**鞅 (martingale)** 的核心。一个适应[随机过程](@entry_id:159502) $(M_t)_{t \ge 0}$ 是一个[鞅](@entry_id:267779)，如果对任意 $s \le t$，都有 $\mathbb{E}[M_t \mid \mathcal{F}_s] = M_s$。[伊藤积分](@entry_id:272774)的一个基本性质就是，对于满足特定[可积条件](@entry_id:158502)的被积过程 $H$，其[随机积分](@entry_id:198356) $M_t = \int_0^t H_u dW_u$ 是一个[鞅](@entry_id:267779)。[@problem_id:2974994] 另一个重要应用是**可选抽样定理 (Optional Sampling Theorem)**，例如，对于有界停时 $\tau$ 和标准布朗运动 $W_t$，我们有 $\mathbb{E}[W_\tau \mid \mathcal{F}_s] = W_{s \wedge \tau}$。[@problem_id:2974994] 这些性质是[随机分析](@entry_id:188809)中进行计算和推断的强大工具。