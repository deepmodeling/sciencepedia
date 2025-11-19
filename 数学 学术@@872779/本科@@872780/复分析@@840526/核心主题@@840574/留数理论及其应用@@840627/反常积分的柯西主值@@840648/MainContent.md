## 引言
在数学和物理学的探索中，我们常常遇到这样一类积分：它们的被积函数在积分路径上存在[奇点](@entry_id:137764)，导致传统的积分方法失效。例如，$\int_{-\infty}^{\infty} (x-1)^{-1} dx$ 在标准定义下是发散的，然而在许多实际问题中，我们需要为这类“坏”积分赋予一个有意义的数值。这个问题构成了我们学习中的一个重要知识缺口。[瑕积分](@entry_id:138794)的[柯西主值](@entry_id:192761)（Cauchy Principal Value）正是为了解决这一挑战而生，它通过一种巧妙的对称极限方法，“驯服”了导致发散的无穷大，从而提取出积分的有限“[主部](@entry_id:168896)”。

本文将系统地引导读者深入理解[柯西主值](@entry_id:192761)的世界。在第一章“原理与机制”中，我们将从[柯西主值](@entry_id:192761)的定义出发，阐明其背后的对称思想，并重点介绍如何利用[复分析中的留数](@entry_id:165494)定理和[缩进围道](@entry_id:192242)等强大工具来高效地计算[主值](@entry_id:189577)。接着，在第二章“应用与跨学科联系”中，我们将展示[柯西主值](@entry_id:192761)并非纯粹的数学构造，而是连接物理学、信号处理等多个领域的桥梁，它深刻地体现在克拉默-克若尼关系和希尔伯特变换等重要理论中。最后，第三章“动手实践”将提供一系列精心设计的问题，帮助读者巩固所学知识，将理论应用于实际计算。通过本文的学习，你将掌握处理[奇异积分](@entry_id:167381)的关键技巧，并领略[复分析](@entry_id:167282)在解决实际问题中的优雅与力量。

## 原理与机制

在[实分析](@entry_id:137229)的领域中，我们处理的[瑕积分](@entry_id:138794)（improper integral）通常要求被积函数在积分区间内的任何有限子区间上都是可积的，并且在积分限趋于无穷时的极限存在。然而，在物理学和工程学的众多分支中，我们经常会遇到一些不满足这些严格条件的积分。例如，当被积函数在积分路径上存在[奇点](@entry_id:137764)（singularity）时，传统的积分定义就会失效。[柯西主值](@entry_id:192761)（Cauchy Principal Value）为这类发散的积分赋予了一个明确且有用的数值，它通过一种对称的极限过程来“驯服”无穷大。本章将系统地阐述[柯西主值](@entry_id:192761)的原理、定义、计算方法及其背后的深刻机制。

### [柯西主值](@entry_id:192761)的必要性

为了理解为何需要引入[柯西主值](@entry_id:192761)这一概念，我们首先考察两个看似相似的[瑕积分](@entry_id:138794) [@problem_id:2270629]：
$$ I_A = \int_{-\infty}^{\infty} \frac{1}{x^2+1}\,dx $$
$$ I_B = \int_{-\infty}^{\infty} \frac{1}{x^2-1}\,dx $$

对于积分 $I_A$，被积函数 $f(x) = \frac{1}{x^2+1}$ 在整个[实轴](@entry_id:148276)上是连续的。其反常性仅来自于无限的积分区间。根据[瑕积分](@entry_id:138794)的标准定义，我们将其拆分为两部分：
$$ I_A = \int_{-\infty}^{0} \frac{1}{x^2+1}\,dx + \int_{0}^{\infty} \frac{1}{x^2+1}\,dx $$
由于 $\int \frac{1}{x^2+1}\,dx = \arctan(x)$，我们可以计算出：
$$ \lim_{b\to\infty} \int_{0}^{b} \frac{1}{x^2+1}\,dx = \lim_{b\to\infty} \arctan(b) - \arctan(0) = \frac{\pi}{2} $$
$$ \lim_{a\to-\infty} \int_{a}^{0} \frac{1}{x^2+1}\,dx = \arctan(0) - \lim_{a\to-\infty} \arctan(a) = 0 - \left(-\frac{\pi}{2}\right) = \frac{\pi}{2} $$
两个极限都独立存在且有限，因此积分 $I_A$ 在标准意义下收敛，其值为 $\pi$。

现在我们转向积分 $I_B$。被积函数 $g(x) = \frac{1}{x^2-1} = \frac{1}{(x-1)(x+1)}$ 在 $x=1$ 和 $x=-1$ 处存在垂直渐近线。这引入了第二类反常性。为了判断其在标准意义下是否收敛，我们必须在[奇点](@entry_id:137764)处将积分拆开。例如，在[奇点](@entry_id:137764) $x=1$ 附近，我们考察[单侧极限](@entry_id:138326)：
$$ \int_{0}^{1} \frac{1}{x^2-1}\,dx = \lim_{\epsilon \to 0^+} \int_{0}^{1-\epsilon} \frac{1}{x^2-1}\,dx $$
其不定积分为 $\frac{1}{2}\ln\left|\frac{x-1}{x+1}\right|$。因此，
$$ \lim_{\epsilon \to 0^+} \left[ \frac{1}{2}\ln\left|\frac{x-1}{x+1}\right| \right]_{0}^{1-\epsilon} = \lim_{\epsilon \to 0^+} \frac{1}{2}\ln\left(\frac{\epsilon}{2-\epsilon}\right) = -\infty $$
由于这个极限发散到负无穷，积分 $I_B$ 在标准意义下是发散的。然而，物理学家和数学家发现，如果我们在处理这类[奇点](@entry_id:137764)时采用一种对称的方式，往往可以得到一个有限且有意义的结果。这正是[柯西主值](@entry_id:192761)的用武之地。其核心思想在于，从[奇点](@entry_id:137764)[两侧对称](@entry_id:136370)地逼近，使得发散的部分能够相互抵消。

### [柯西主值](@entry_id:192761)的定义

[柯西主值](@entry_id:192761)通过强制施行对称极限来处理两类反常性：无限的积分域和路径上的[奇点](@entry_id:137764)。

对于一个在[实轴](@entry_id:148276)上仅在一点 $x=c$ 有[奇点](@entry_id:137764)的函数 $f(x)$，其在有限区间 $[a, b]$（其中 $a \lt c \lt b$）上的[柯西主值](@entry_id:192761)定义为：
$$ \text{P.V.} \int_{a}^{b} f(x) \, dx = \lim_{\epsilon \to 0^+} \left( \int_{a}^{c-\epsilon} f(x) \, dx + \int_{c+\epsilon}^{b} f(x) \, dx \right) $$
这里，我们从[奇点](@entry_id:137764) $c$ 的左右两侧移除了一个对称的小区间 $(c-\epsilon, c+\epsilon)$，然后再取极限 $\epsilon \to 0^+$。

对于在 $(-\infty, \infty)$ 上可积但在无穷远处可能存在问题的函数，其主值定义为：
$$ \text{P.V.} \int_{-\infty}^{\infty} f(x) \, dx = \lim_{R \to \infty} \int_{-R}^{R} f(x) \, dx $$
这里，我们使用对称的区间 $[-R, R]$ 来逼近整个[实轴](@entry_id:148276)。

当一个积分同时具有无限积分域和路径上的[奇点](@entry_id:137764)（例如 $x=c$）时，我们需要将这两种对称性结合起来。其严格定义是一个迭代极限 [@problem_id:2270643]：
$$ \text{P.V.} \int_{-\infty}^{\infty} f(x) \, dx = \lim_{R \to \infty} \left[ \lim_{\epsilon \to 0^+} \left( \int_{-R}^{c-\epsilon} f(x) \, dx + \int_{c+\epsilon}^{R} f(x) \, dx \right) \right] $$
这个定义的关键在于**对称性**。我们必须使用同一个 $\epsilon$ 来挖除[奇点](@entry_id:137764)周围的区间，并使用同一个 $R$ 来截断无穷远处。任何非对称的极限过程都可能导致不同的、甚至是任意的结果。

例如，考虑积分 $\int \frac{1}{x} dx$。其[柯西主值](@entry_id:192761)是：
$$ \text{P.V.} \int_{-\infty}^{\infty} \frac{1}{x} \, dx = \lim_{R \to \infty} \lim_{\epsilon \to 0^+} \left( \int_{-R}^{-\epsilon} \frac{dx}{x} + \int_{\epsilon}^{R} \frac{dx}{x} \right) $$
$$ = \lim_{R \to \infty} \lim_{\epsilon \to 0^+} \left( [\ln|x|]_{-R}^{-\epsilon} + [\ln|x|]_{\epsilon}^{R} \right) = \lim_{R \to \infty} \lim_{\epsilon \to 0^+} \left( (\ln\epsilon - \ln R) + (\ln R - \ln\epsilon) \right) = 0 $$
然而，如果我们采用一个非对称的极限，例如 $\int_{-R}^{2R} \frac{1}{x} dx$ [@problem_id:2270618]，结果就会不同：
$$ \lim_{R \to \infty} \lim_{\epsilon \to 0^+} \left( \int_{-R}^{-\epsilon} \frac{dx}{x} + \int_{\epsilon}^{2R} \frac{dx}{x} \right) = \lim_{R \to \infty} \lim_{\epsilon \to 0^+} \left( (\ln\epsilon - \ln R) + (\ln(2R) - \ln\epsilon) \right) = \lim_{R \to \infty} \ln\left(\frac{2R}{R}\right) = \ln 2 $$
这清晰地表明，主值是一个非常特定的定义，依赖于对称的极限过程。

### 主值积分的存在性

对称的极限过程是否总能产生一个有限值呢？答案是否定的。[主值](@entry_id:189577)的存在性与[奇点](@entry_id:137764)的性质密切相关。让我们比较两个具有不同阶数[奇点](@entry_id:137764)的积分 [@problem_id:2270638]：
$$ V_1 = \text{P.V.} \int_{-\infty}^{\infty} \frac{5}{x-3} \, dx $$
$$ V_2 = \text{P.V.} \int_{-\infty}^{\infty} \frac{1}{(x-3)^2} \, dx $$

对于 $V_1$，被积函数在 $x=3$ 处有一个**一阶极点**（simple pole）。根据定义，我们计算：
$$ V_1 = \lim_{R\to\infty}\lim_{\epsilon\to 0^{+}}\left(\int_{-R+3}^{3-\epsilon}\frac{5}{x-3}\,dx+\int_{3+\epsilon}^{R+3}\frac{5}{x-3}\,dx\right) $$
令 $u=x-3$，积分变为：
$$ \lim_{R\to\infty}\lim_{\epsilon\to 0^{+}}\left( \int_{-R}^{-\epsilon} \frac{5}{u}\,du + \int_{\epsilon}^{R} \frac{5}{u}\,du \right) = \lim_{R\to\infty}\lim_{\epsilon\to 0^{+}} \left( [5\ln|u|]_{-R}^{-\epsilon} + [5\ln|u|]_{\epsilon}^{R} \right) = 0 $$
发散项 $5\ln\epsilon$ 和 $-5\ln\epsilon$ 精确地相互抵消了。这通常发生在被积函数在[奇点](@entry_id:137764)附近“局部奇对称”的情况下。

对于 $V_2$，被积函数在 $x=3$ 处有一个**二阶极点**（pole of order 2）。我们进行类似的计算，令 $u=x-3$：
$$ V_2 = \lim_{R\to\infty}\lim_{\epsilon\to 0^{+}}\left( \int_{-R}^{-\epsilon} \frac{1}{u^2}\,du + \int_{\epsilon}^{R} \frac{1}{u^2}\,du \right) = \lim_{R\to\infty}\lim_{\epsilon\to 0^{+}} \left( \left[-\frac{1}{u}\right]_{-R}^{-\epsilon} + \left[-\frac{1}{u}\right]_{\epsilon}^{R} \right) $$
$$ = \lim_{R\to\infty}\lim_{\epsilon\to 0^{+}} \left( \left(\frac{1}{\epsilon} - \frac{1}{R}\right) + \left(-\frac{1}{R} + \frac{1}{\epsilon}\right) \right) = \lim_{R\to\infty}\lim_{\epsilon\to 0^{+}} \left( \frac{2}{\epsilon} - \frac{2}{R} \right) $$
当 $\epsilon \to 0^+$ 时，$\frac{2}{\epsilon}$ 项发散到 $+\infty$。对称性无法消除这个发散。因此，$V_2$ 的[柯西主值](@entry_id:192761)不存在。这通常发生在被积函数在[奇点](@entry_id:137764)附近“局部偶对称”的情况下。

一般而言，如果一个函数在实轴上的[奇点](@entry_id:137764)是**一阶极点**，其[柯西主值](@entry_id:192761)通常是存在的。但如果[奇点](@entry_id:137764)是**偶数阶极点**（如二阶、四阶等），[主值](@entry_id:189577)通常不存在，因为对称的积分贡献会相加而不是相消。

### 使用围道积分计算[主值](@entry_id:189577)

直接根据定义计算[柯西主值](@entry_id:192761)可能非常繁琐。[复分析](@entry_id:167282)中的**[留数定理](@entry_id:164878)（Residue Theorem）**为我们提供了一个强大得多的工具。其基本策略是构建一个闭合的围道（contour），该围道由以下几部分组成：
1.  沿实轴的两个线段，例如从 $-R$ 到 $c-\epsilon$ 和从 $c+\epsilon$ 到 $R$。
2.  一个或多个半径为 $\epsilon$ 的小半圆弧，称为**[缩进围道](@entry_id:192242)（indented contour）**，用于绕过[实轴](@entry_id:148276)上的[奇点](@entry_id:137764)。通常，我们将这些半圆弧取在上半复平面或下半复平面。
3.  一个半径为 $R$ 的大半圆弧 $\Gamma_R$，用于闭合整个围道，通常也取在上半或下半平面。

这样一个典型的[上半平面](@entry_id:199119)[缩进围道](@entry_id:192242)如下图所示（尽管我们不能在此处显示图像）：它从 $-R$ 出发沿实轴到 $c-\epsilon$，然后顺时针沿一个半径为 $\epsilon$ 的小半圆 $\gamma_\epsilon$ 绕过 $c$ 到达 $c+\epsilon$，再沿[实轴](@entry_id:148276)到 $R$，最后逆时针沿一个半径为 $R$ 的大半圆 $\Gamma_R$ 回到 $-R$。

根据留数定理，沿此闭合围道 $C$ 的积分等于 $2\pi i$ 乘以围道内部所有极点的留数之和：
$$ \oint_C f(z) \, dz = 2\pi i \sum_{k} \text{Res}(f, z_k) $$
另一方面，这个围道积分也可以写成各部分积分之和：
$$ \oint_C f(z) \, dz = \left( \int_{-R}^{c-\epsilon} + \int_{c+\epsilon}^{R} \right) f(x) \, dx + \int_{\gamma_\epsilon} f(z) \, dz + \int_{\Gamma_R} f(z) \, dz $$
在取极限 $R \to \infty$ 和 $\epsilon \to 0^+$ 时，左边的两个[实轴](@entry_id:148276)积分之和就变成了我们想要求的[柯西主值](@entry_id:192761)。因此，我们可以得到计算[主值](@entry_id:189577)的核心公式：
$$ \text{P.V.} \int_{-\infty}^{\infty} f(x) \, dx + \lim_{\epsilon \to 0^+} \int_{\gamma_\epsilon} f(z) \, dz + \lim_{R \to \infty} \int_{\Gamma_R} f(z) \, dz = 2\pi i \sum_{\text{enclosed}} \text{Res}(f, z_k) $$
要成功运用此方法，我们必须能够确定大半圆弧和小半圆弧上积分的极限值。

### 围道各部分的分析

#### 大半圆弧上的积分

我们首先考虑大半圆弧 $\Gamma_R$ 的贡献。对于许多函数，当 $R \to \infty$ 时，这个积分会趋于零。一个重要的判别准则是针对有理函数的 [@problem_id:2270635]。

如果 $f(z) = P(z)/Q(z)$ 是一个有理函数，其中 $P(z)$ 和 $Q(z)$ 是多项式，令 $\deg(P)=m$ 和 $\deg(Q)=n$。当 $|z|=R$ 很大时，$|f(z)|$ 的行为近似于 $C/R^{n-m}$，其中 $C$ 是一个常数。我们可以使用**[估计引理](@entry_id:164334)（Estimation Lemma）**来约束积分的大小：
$$ \left| \int_{\Gamma_R} f(z) \, dz \right| \le (\text{length of } \Gamma_R) \times \max_{z \in \Gamma_R} |f(z)| = (\pi R) \times O\left(\frac{1}{R^{n-m}}\right) = O\left(R^{m-n+1}\right) $$
为了使这个积分在 $R \to \infty$ 时趋于零，我们需要幂指数 $m-n+1 \lt 0$，即 $n \ge m+2$。

**判别法则**：对于[有理函数](@entry_id:154279) $f(z) = P(z)/Q(z)$，如果分母的次数至少比分子的次数大二（$\deg(Q) \ge \deg(P)+2$），那么 $\lim_{R \to \infty} \int_{\Gamma_R} f(z) \, dz = 0$。

例如，对于 $f(x) = \frac{x^2 - 1}{x^4 + 1}$ ($n=4, m=2, n-m=2$) 和 $f(x) = \frac{x}{x^3 - 8}$ ($n=3, m=1, n-m=2$)，大半圆弧上的积分都将消失。但对于 $f(x) = \frac{x^3 + 2x}{x^4 - 1}$ ($n=4, m=3, n-m=1$)，该积分将不趋于零。

对于形如 $f(z) e^{ikz}$ ($k>0$) 的函数，有一个更强的结论，即**[若尔当引理](@entry_id:177824)（Jordan's Lemma）**，它表明只要 $|f(z)|$ 在[上半平面](@entry_id:199119)上随 $|z|\to\infty$ 而一致趋于零（即 $\deg(Q) \ge \deg(P)+1$），大半圆弧上的积分也会消失 [@problem_id:2270610]。这在计算[傅里叶变换](@entry_id:142120)时尤其有用。

#### [奇点](@entry_id:137764)处小半圆弧上的积分

现在我们来分析缩进小半圆弧 $\gamma_\epsilon$ 的贡献。这是计算[柯西主值](@entry_id:192761)的关键步骤。

**一阶极点的情况**

假设 $f(z)$ 在[实轴](@entry_id:148276)上的点 $z=c$ 有一个一阶极点。我们可以在 $c$ 点附近将 $f(z)$ 进行洛朗展开：
$$ f(z) = \frac{A}{z-c} + h(z) $$
其中 $A = \text{Res}(f, c)$ 是 $f$ 在 $c$ 点的留数，而 $h(z)$ 在 $c$ 点是解析的（analytic）。
我们计算沿一个绕过 $c$ 的上半平面小半圆弧 $\gamma_\epsilon$ 的积分。此路径通常从 $c-\epsilon$ 顺时针走到 $c+\epsilon$。我们可以[参数化](@entry_id:272587)为 $z(\theta) = c + \epsilon e^{i\theta}$，其中 $\theta$ 从 $\pi$ 减小到 $0$。
$$ \int_{\gamma_\epsilon} f(z) \, dz = \int_{\gamma_\epsilon} \frac{A}{z-c} \, dz + \int_{\gamma_\epsilon} h(z) \, dz $$
第一项的计算是：
$$ \int_{\pi}^{0} \frac{A}{\epsilon e^{i\theta}} (i \epsilon e^{i\theta} d\theta) = A \int_{\pi}^{0} i \, d\theta = -i\pi A = -i\pi \text{Res}(f, c) $$
第二项由于 $h(z)$ 在 $c$ 处有界，其积分大小为 $O(\epsilon)$，因此当 $\epsilon \to 0^+$ 时趋于零。
这个结果，有时被称为**分数[留数定理](@entry_id:164878)**或**[缩进围道](@entry_id:192242)引理**，是一个普遍的结论 [@problem_id:2270646] [@problem_id:2270654]。

**[缩进围道](@entry_id:192242)引理**：如果 $f(z)$ 在[实轴](@entry_id:148276)上的 $z=c$ 有一个一阶极点，那么当 $\epsilon \to 0^+$ 时：
-   沿[上半平面](@entry_id:199119)绕过 $c$ 的**顺时针**小半圆弧的积分极限为 $-i\pi \text{Res}(f, c)$。
-   沿[上半平面](@entry_id:199119)绕过 $c$ 的**逆时针**小半圆弧的积分极限为 $+i\pi \text{Res}(f, c)$。
-   沿下半平面绕过 $c$ 的小半圆弧的积分，结论的符号相反。

**[高阶极点](@entry_id:169853)的情况**

如果 $z=c$ 是一个二阶或更高阶的极点，情况就完全不同了。例如，考虑 $f(z) = \frac{g(z)}{(z-c)^2}$，其中 $g(z)$ 在 $c$ 处解析。洛朗展开为：
$$ f(z) = \frac{A_2}{(z-c)^2} + \frac{A_1}{z-c} + h(z) $$
其中 $A_2 = g(c)$，$A_1 = g'(c)$。沿上半平面顺时针小半圆弧的积分将包含一个发散项 [@problem_id:2270627]：
$$ \int_{\gamma_\epsilon} \frac{A_2}{(z-c)^2} dz = \int_{\pi}^{0} \frac{A_2}{(\epsilon e^{i\theta})^2} (i\epsilon e^{i\theta} d\theta) = \frac{iA_2}{\epsilon} \int_{\pi}^{0} e^{-i\theta} d\theta = \frac{iA_2}{\epsilon} [ie^{-i\theta}]_{\pi}^{0} = \frac{iA_2}{\epsilon} (i - (-i)) = -\frac{2A_2}{\epsilon} $$
这个 $1/\epsilon$ 项在 $\epsilon \to 0^+$ 时发散，这正是[柯西主值](@entry_id:192761)对于二阶极点不存在的根本原因。

### 综合应用与深层联系

掌握了以上原理后，我们便可以系统地计算[柯西主值](@entry_id:192761)积分。让我们以一个经典物理问题为例，计算 $I = \text{P.V.} \int_{-\infty}^{\infty} \frac{\exp(ikx)}{x-a} dx$，其中 $k>0$ 且 $a$为实数 [@problem_id:2270612]。

我们构造一个[上半平面](@entry_id:199119)的[缩进围道](@entry_id:192242)，绕过 $x=a$ 处的一阶极点。
1.  **围道积分**：被积函数 $f(z) = \frac{\exp(ikz)}{z-a}$ 在围道内部没有极点（因为唯一的极点 $z=a$ 被绕开了），所以根据留数定理，$\oint_C f(z) dz = 0$。
2.  **各部分积分**：
    $$ \oint_C f(z) \, dz = \text{P.V.} \int f(x) \, dx + \lim_{\epsilon \to 0^+} \int_{\gamma_\epsilon} f(z) \, dz + \lim_{R \to \infty} \int_{\Gamma_R} f(z) \, dz = 0 $$
3.  **大半圆弧**：由于 $k>0$，根据[若尔当引理](@entry_id:177824)，$\lim_{R \to \infty} \int_{\Gamma_R} f(z) \, dz = 0$。
4.  **小半圆弧**：路径是顺时针的，所以积分极限是 $-i\pi$ 乘以留数。$f(z)$ 在 $z=a$ 处的留数是 $\text{Res}(f, a) = \lim_{z \to a} (z-a)f(z) = \exp(ika)$。因此，小半圆弧的贡献是 $-i\pi \exp(ika)$。
5.  **求解主值**：将以上结果代入，我们得到：
    $$ \text{P.V.} + (-i\pi \exp(ika)) + 0 = 0 $$
    $$ \implies \text{P.V.} \int_{-\infty}^{\infty} \frac{\exp(ikx)}{x-a} \, dx = i\pi \exp(ika) $$

这个结果引出了一个更深层的联系。在物理学中，处理[实轴上的极点](@entry_id:191960)还有一种常见的方法，即给极点增加一个无穷小的虚部，称为 $i\epsilon$ 规则。这对应于将积分路径从[实轴](@entry_id:148276)向上或向下平移，从而绕过极点。

考虑两种不同的路径 [@problem_id:2270609]：
-   $I_U$：路径在 $z=a$ 上方绕过（等价于计算 $\int_{-\infty}^\infty \frac{\exp(ix)}{x-(a-i\epsilon)} dx$）。
-   $I_L$：路径在 $z=a$ 下方绕过（等价于计算 $\int_{-\infty}^\infty \frac{\exp(ix)}{x-(a+i\epsilon)} dx$）。

从我们的[围道积分](@entry_id:169446)公式可以推导出：
-   $I_U = \text{P.V.} + (\text{上半平面小弧贡献}) = \text{P.V.} - i\pi \text{Res}(f,a)$
-   $I_L = \text{P.V.} + (\text{下半平面小弧贡献}) = \text{P.V.} + i\pi \text{Res}(f,a)$

由此，我们得到它们之间的差值：
$$ I_L - I_U = 2i\pi \text{Res}(f,a) $$
对于函数 $f(z) = \frac{\exp(iz)}{z-a}$，其留数为 $\exp(ia)$，因此差值为 $2i\pi\exp(ia)$。

这两个关系式，即
$$ \lim_{\epsilon \to 0^+} \frac{1}{x-a \pm i\epsilon} = \text{P.V.} \frac{1}{x-a} \mp i\pi\delta(x-a) $$
被称为**Sokhotski-Plemelj 定理**，它是[量子场论](@entry_id:138177)、[散射理论](@entry_id:143476)和[线性响应理论](@entry_id:145737)中的一个基本工具。它精确地阐明了[柯西主值](@entry_id:192761)与通过移动极点来定义积分这两种方法之间的深刻联系，为处理物理学中的[奇异积分](@entry_id:167381)提供了坚实的数学基础。