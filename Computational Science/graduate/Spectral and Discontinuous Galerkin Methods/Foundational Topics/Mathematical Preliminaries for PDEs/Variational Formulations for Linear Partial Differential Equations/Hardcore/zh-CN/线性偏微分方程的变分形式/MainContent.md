## 引言
[线性偏微分方程](@entry_id:172517)（PDEs）是描述从物理学、工程学到金融学等众多领域现象的通用语言。然而，直接求解这些方程，尤其是对于复杂几何或边界条件，往往极具挑战性。[变分形式](@entry_id:166033)为我们提供了一套强大而优雅的理论框架，它不仅能以数学上严谨的方式重新表述PDE问题，更为现代计算方法，如[有限元法](@entry_id:749389)（FEM）、[谱方法](@entry_id:141737)和间断伽辽金（DG）方法，奠定了坚实的理论基石。本文旨在填补从抽象[PDE理论](@entry_id:189232)到具体数值实现之间的知识鸿沟，探讨如何系统地构建、分析并应用[变分形式](@entry_id:166033)来求解线性PDE。

在接下来的内容中，我们将踏上一段从理论到实践的旅程。第一章“原理与机制”将从最基本的[弱形式](@entry_id:142897)推导入手，逐步建立所需的[泛函分析](@entry_id:146220)框架，并讨论保证解存在且唯一的[适定性](@entry_id:148590)理论。第二章“应用与[交叉](@entry_id:147634)学科联系”将展示这些理论原理如何被用于设计稳定精确的[数值格式](@entry_id:752822)，解决[计算流体力学](@entry_id:747620)、波传播等前沿领域的实际问题。最后，第三章“动手实践”将通过一系列精心设计的练习，帮助您将理论知识转化为解决具体问题的能力，从而真正掌握变分方法的核心精髓。

## 原理与机制

本章深入探讨为[线性偏微分方程](@entry_id:172517)（PDEs）构建和分析[变分形式](@entry_id:166033)的核心原理与机制。我们将从最基本的[弱形式](@entry_id:142897)推导开始，逐步建立所需的[泛函分析](@entry_id:146220)框架，讨论其[适定性](@entry_id:148590)理论，并最终将这些概念与伽辽金（Galerkin）[离散化方法](@entry_id:272547)及其在现代计算科学中的高等应用联系起来。

### [变分形式](@entry_id:166033)的推导：弱形式

[变分方法](@entry_id:163656)的核心思想是将一个[微分方程](@entry_id:264184)问题转化为一个等价的积分方程问题。这个积分形式被称为**弱形式**（weak formulation），因为它对解的[光滑性](@entry_id:634843)要求比原始的（或“强的”）[微分形式](@entry_id:146747)更低。这个转化过程通常通过两个关键步骤完成：乘以一个任意的**检验函数**（test function），然后在求解域上积分，最后利用**[分部积分](@entry_id:136350)**（integration by parts）将导数从未知解函数上转移一部分到检验函数上。

让我们通过一个具有[混合边界条件](@entry_id:176456)的典型二阶线性椭圆型[偏微分方程](@entry_id:141332)来阐释这个过程。考虑一个有界Lipschitz区域 $\Omega \subset \mathbb{R}^{d}$，其边界 $\partial \Omega$ 被划分为不相交的Dirichlet边界 $\Gamma_{D}$ 和Neumann边界 $\Gamma_{N}$。问题是求解函数 $u(x)$ 满足：
$$
-\nabla \cdot \big( A(x) \nabla u(x) \big) = f(x) \quad \text{in } \Omega,
$$
同时服从边界条件：
$$
u = g_{D} \quad \text{on } \Gamma_{D}, \qquad \big( A \nabla u \big) \cdot n = g_{N} \quad \text{on } \Gamma_{N}.
$$
这里，$A(x)$ 是一个对称且一致正定的系数矩阵，$f(x)$ 是源项，$g_D$ 和 $g_N$ 是给定的边界数据，$n$ 是 $\partial \Omega$ 上的单位外[法向量](@entry_id:264185)。

为了推导[弱形式](@entry_id:142897)，我们首先将PDE乘以一个任意的、足够光滑的[检验函数](@entry_id:166589) $v$，并在区域 $\Omega$ 上积分：
$$
-\int_{\Omega} \Big(\nabla \cdot \big( A \nabla u \big)\Big) v \, dx = \int_{\Omega} f v \, dx.
$$
接下来是关键步骤：分部积分。利用向量微积分中的[格林第一恒等式](@entry_id:170345)（Green's first identity），我们可以将左侧的积分重写为：
$$
\int_{\Omega} (A \nabla u) \cdot \nabla v \, dx - \int_{\partial \Omega} v \big( (A \nabla u) \cdot n \big) \, dS = \int_{\Omega} f v \, dx.
$$
这一步成功地将作用在 $u$ 上的[二阶导数](@entry_id:144508)（散度与梯度的复合）转化为了作用在 $u$ 和 $v$ 上的[一阶导数](@entry_id:749425)。这降低了对 $u$ 的光滑性要求。

现在，我们需要处理边界积分项并融入边界条件。边界 $\partial \Omega$ 由 $\Gamma_D$ 和 $\Gamma_N$ 组成，因此边界积分可以分解为：
$$
\int_{\partial \Omega} v \big( (A \nabla u) \cdot n \big) \, dS = \int_{\Gamma_D} v \big( (A \nabla u) \cdot n \big) \, dS + \int_{\Gamma_N} v \big( (A \nabla u) \cdot n \big) \, dS.
$$
在Neumann边界 $\Gamma_N$ 上，我们已知法向通量 $(A \nabla u) \cdot n = g_N$。这个条件可以直接代入积分中。由于这个条件能自然地出现在[变分形式](@entry_id:166033)的推导过程中，[Neumann边界条件](@entry_id:142124)被称为**自然边界条件**（natural boundary condition）。

在Dirichlet边界 $\Gamma_D$ 上，解本身被指定为 $u = g_D$。这个条件必须被强加于解的候选空间。在边界积分中，法向通量 $(A \nabla u) \cdot n$ 在 $\Gamma_D$ 上是未知的。为了消除这个讨厌的未知项，我们做出一个策略[性选择](@entry_id:138426)：要求所有[检验函数](@entry_id:166589) $v$ 在Dirichlet边界 $\Gamma_D$ 上为零，即 $v|_{\Gamma_D} = 0$。这样一来，$\Gamma_D$ 上的积分就消失了。因为[Dirichlet条件](@entry_id:137096)必须通过对函数空间的限制来满足，它被称为**[本质边界条件](@entry_id:173524)**（essential boundary condition）。

结合这些步骤，我们的[积分方程](@entry_id:138643)变为：
$$
\int_{\Omega} (A \nabla u) \cdot \nabla v \, dx = \int_{\Omega} f v \, dx + \int_{\Gamma_N} g_N v \, dS.
$$
这个方程需要在某个合适的函数空间中对所有满足 $v|_{\Gamma_D} = 0$ 的检验函数 $v$ 成立。

我们可以将此问题抽象成[标准形式](@entry_id:153058)：求解 $u \in V$ 使得
$$
a(u,v) = \ell(v) \quad \text{for all } v \in V_0,
$$
其中，$a(\cdot, \cdot)$ 是**双线性形式**（bilinear form），$\ell(\cdot)$ 是**[线性泛函](@entry_id:276136)**（linear functional）。对于我们上面的例子，它们分别是：
*   [双线性形式](@entry_id:746794): $a(u, v) = \int_{\Omega} (A(x)\nabla u) \cdot \nabla v \, dx$
*   线性泛函: $\ell(v) = \int_{\Omega} f v \, dx + \int_{\Gamma_N} g_N v \, dS$

**试验空间**（trial space）$V$ 是允许的解 $u$ 所属的集合，它必须满足[本质边界条件](@entry_id:173524)。**检验空间**（test space）$V_0$ 则是检验函数 $v$ 所属的空间，它通常是与齐次[本质边界条件](@entry_id:173524)相关联的[向量空间](@entry_id:151108)。

### [泛函分析](@entry_id:146220)框架与[适定性](@entry_id:148590)

为了严格地分析[变分问题](@entry_id:756445)，我们需要一个合适的数学舞台。这个舞台由**[索博列夫空间](@entry_id:141995)**（Sobolev spaces）提供。

对于函数 $u \in L^2(\Omega)$（即在 $\Omega$ 上平方可积的函数），其**[弱导数](@entry_id:189356)** $\partial_{x_i} u$ 是一个函数 $v_i \in L^2(\Omega)$，它对所有具有[紧支集](@entry_id:276214)的无限[可微函数](@entry_id:144590)（[检验函数](@entry_id:166589)）$\phi \in C_c^\infty(\Omega)$ 满足[分部积分公式](@entry_id:145262)：
$$
\int_\Omega u \, \frac{\partial \phi}{\partial x_i} \, d\mathbf{x} = - \int_\Omega v_i \, \phi \, d\mathbf{x}.
$$
[索博列夫空间](@entry_id:141995) $H^1(\Omega)$ 就是由所有自身及其一阶[弱导数](@entry_id:189356)都属于 $L^2(\Omega)$ 的函数组成的空间。它是一个希尔伯特空间，其范数为：
$$
\|u\|_{H^1(\Omega)} = \left( \|u\|_{L^2(\Omega)}^2 + \|\nabla u\|_{L^2(\Omega)}^2 \right)^{1/2}.
$$
对于一般的 $L^2$ 函数，其在边界（一个零测集）上的取值是没有意义的。然而，$H^1(\Omega)$ 中的函数具有足够高的正则性，使得它们的边界值（或称**迹**，trace）可以被良定义。**[迹定理](@entry_id:203967)**（Trace Theorem）指出，对于有界Lipschitz区域 $\Omega$，存在一个唯一的、线性的、连续的**[迹算子](@entry_id:183665)** $\gamma: H^1(\Omega) \to L^2(\partial \Omega)$。更精确地，该算子的值域是分数阶索博列夫空间 $H^{1/2}(\partial \Omega)$，并且映射 $\gamma: H^1(\Omega) \to H^{1/2}(\partial \Omega)$ 是满射的。

[迹算子](@entry_id:183665)为本质边界条件提供了严格的数学含义。条件 $u = g_D$ 在弱形式的框架下被精确地表述为 $\gamma u = g_D$。
*   对于**齐次**[Dirichlet条件](@entry_id:137096) ($g_D=0$)，解位于迹[算子的核](@entry_id:272757)空间 $\ker(\gamma)$ 中。这个空间可以被证明与 $H_0^1(\Omega)$ 等价，后者是 $C_c^\infty(\Omega)$ 在 $H^1$ 范数下的[闭包](@entry_id:148169)。因此，试验空间和检验空间都取为 $H_0^1(\Omega)$。
*   对于**非齐次**[Dirichlet条件](@entry_id:137096) ($g_D \ne 0$)，[迹算子](@entry_id:183665)的满射性保证了存在一个函数（称为**提升**，$u_{g_D}$）$\in H^1(\Omega)$ 使得 $\gamma u_{g_D} = g_D$。总的解可以分解为 $u = u_0 + u_{g_D}$，其中 $u_0 \in H_0^1(\Omega)$ 是一个新的、具有[齐次边界条件](@entry_id:750371)的[变分问题](@entry_id:756445)的解。因此，试验空间是一个[仿射空间](@entry_id:152906) $u_{g_D} + H_0^1(\Omega)$，而检验空间仍然是 $H_0^1(\Omega)$。

一个[变分问题](@entry_id:756445)是**适定**的（well-posed），如果它有唯一解，且解连续地依赖于数据。对于[对称双线性形式](@entry_id:148281)，**[Lax-Milgram定理](@entry_id:137966)**给出了[适定性](@entry_id:148590)的充分条件：
1.  双线性形式 $a(\cdot, \cdot)$ 在[希尔伯特空间](@entry_id:261193) $V_0$ 上是**连续的**（或有界的）：存在常数 $M > 0$ 使得 $|a(u,v)| \le M \|u\|_{V_0} \|v\|_{V_0}$ 对所有 $u, v \in V_0$ 成立。
2.  [双线性形式](@entry_id:746794) $a(\cdot, \cdot)$ 在 $V_0$ 上是**强制的**（coercive）：存在常数 $\alpha > 0$ 使得 $a(v,v) \ge \alpha \|v\|_{V_0}^2$ 对所有 $v \in V_0$ 成立。

对于我们之[前推](@entry_id:158718)导的Poisson问题，如果 $\Gamma_D$ 非空，那么在 $H_0^1(\Omega)$ 上，[庞加莱不等式](@entry_id:142086)（Poincaré inequality）保证了 $a(v,v) = \|\nabla v\|_{L^2(\Omega)}^2$ 是强制的，从而问题是适定的。

#### 强制性的失效及其补救

然而，在某些重要情况下，[双线性形式](@entry_id:746794)并非强制的。
一个典型的例子是纯[Neumann问题](@entry_id:176713)，即在整个边界 $\partial\Omega$上都施加[Neumann条件](@entry_id:165471)（$\Gamma_D = \emptyset$）。此时，试验和检验空间都是 $H^1(\Omega)$。双线性形式为 $a(u,v) = \int_{\Omega} \nabla u \cdot \nabla v \, dx$。考虑任意非零常数函数 $u(x)=c$。显然，$u \in H^1(\Omega)$ 且 $\|u\|_{H^1(\Omega)} > 0$。但是，$\nabla u = 0$，导致 $a(u,u) = 0$。这直接违反了强制性条件 $a(u,u) \ge \alpha \|u\|_{H^1(\Omega)}^2 > 0$。因此，$a(\cdot, \cdot)$ 在 $H^1(\Omega)$ 上不是强制的。物理上，这意味着解至多可在一个任意常数内确定。

为恢复[适定性](@entry_id:148590)，我们必须处理这个非唯一性。
1.  **修改[函数空间](@entry_id:143478)**：我们将问题限制在[商空间](@entry_id:274314) $H^1(\Omega)/\mathbb{R}$ 中，它等价于具有零均值的函数[子空间](@entry_id:150286) $H^1_*(\Omega) = \{ v \in H^1(\Omega) : \int_{\Omega} v \, dx = 0 \}$。在这个[子空间](@entry_id:150286)上，庞加莱-维尔丁格不等式（Poincaré-Wirtinger inequality）成立，它保证了 $a(\cdot, \cdot)$ 的强制性。
2.  **[相容性条件](@entry_id:637057)**：为了保证解的存在性，源项 $f$ 必须满足一个**相容性条件**。通过在[变分形式](@entry_id:166033) $a(u,v)=\ell(v)$ 中选取检验函数 $v$ 为 $a(\cdot, \cdot)$ 的核函数（即 $v=1$），我们得到 $a(u,1) = 0$，因此必须有 $\ell(1)=0$。这导出条件 $\int_{\Omega} f \, dx + \int_{\partial \Omega} g_N dS = 0$。

另一个强制性失效的重要例子是**亥姆霍兹方程**（Helmholtz equation） $-\Delta u - k^2 u = f$。其对应的双线性形式包含一个负的质量项 $-k^2 \int_{\Omega} u \bar{v} \, dx$。这一项使得无论如何都无法满足强制性条件。对于这类问题，[Lax-Milgram定理](@entry_id:137966)不再适用。取而代之的分析工具是**Fredholm抉择**（Fredholm alternative）。其核心思想是将[变分问题](@entry_id:756445)对应的算子 $A$ 分解为一个强制（且可逆）的[部分和](@entry_id:162077)一个**[紧算子](@entry_id:139189)**（compact operator）的和。这种结构的算子被称为[Fredholm算子](@entry_id:268966)，其一个关键性质是：对于[Fredholm指数](@entry_id:276918)为零的算子，解的存在性等价于[解的唯一性](@entry_id:143619)。因此，我们只需证明齐次问题（$f=0, g=0$）只有零解，就可以断定对于任意给定的数据，原问题都存在唯一解。对于带有物理[吸声](@entry_id:187864)边界条件（如阻抗或辐射条件）的亥姆霍兹问题，唯一性通常可以通过能量论证来证明，从而保证了问题的[适定性](@entry_id:148590)。

### 伽辽金方法：离散化与收敛性

[变分形式](@entry_id:166033)为数值近似提供了一条清晰的路径。**伽辽金方法**的核心思想是在无限维的试验和检验空间 $V$ 和 $V_0$ 中，选取有限维的[子空间](@entry_id:150286) $V_N \subset V$ 和 $V_{0,N} \subset V_0$，然后在这些[子空间](@entry_id:150286)中求解[变分问题](@entry_id:756445)。

具体而言，我们寻找近似解 $u_N \in V_N$，使得：
$$
a(u_N, v_N) = \ell(v_N) \quad \text{for all } v_N \in V_{0,N}.
$$
如果我们在[子空间](@entry_id:150286) $V_{0,N}$ 中选取一组[基函数](@entry_id:170178) $\{\phi_j\}_{j=1}^N$，并将近似解表示为这组[基函数](@entry_id:170178)的[线性组合](@entry_id:154743) $u_N = \sum_{i=1}^N c_i \phi_i$，那么上述[变分问题](@entry_id:756445)就转化为一个 $N \times N$ 的[线性方程组](@entry_id:148943) $A\mathbf{c} = \mathbf{f}$，其中矩阵和向量的元素为：
$$
A_{ji} = a(\phi_i, \phi_j), \qquad \mathbf{f}_j = \ell(\phi_j).
$$
$A$ 通常被称为**刚度矩阵**（stiffness matrix），$\mathbf{f}$ 被称为**[载荷向量](@entry_id:635284)**（load vector）。

作为一个具体的例子，考虑一维Poisson问题 $-u''=f$ on $(-1,1)$，带有齐次[Dirichlet边界条件](@entry_id:142800)。试验和检验空间都是 $H_0^1(-1,1)$。我们可以选择一个满足边界条件的多项式基底来构建谱伽辽金空间（spectral Galerkin space）。例如，使用[勒让德多项式](@entry_id:141510)（Legendre polynomials）$P_n(x)$，可以构造[基函数](@entry_id:170178) $\phi_n(x) = P_{n+1}(x) - P_{n-1}(x)$，这些[基函数](@entry_id:170178)自动在 $x=\pm 1$ 处为零。对于这个基底，刚度矩阵 $A_{mn} = a(\phi_m, \phi_n) = \int_{-1}^1 \phi_m'(x) \phi_n'(x) dx$ 和质量矩阵 $B_{mn} = \int_{-1}^1 \phi_m(x) \phi_n(x) dx$ 的元素可以利用勒让德多项式的性质（如[微分](@entry_id:158718)关系和正交性）被精确地计算出来。例如，刚度矩阵是对角的，其元素为 $A_{mn} = 2(2m+1)\delta_{mn}$，其中 $\delta_{mn}$ 是克罗内克符号。

伽辽金方法的一个美妙特性是其[误差分析](@entry_id:142477)。**[Céa引理](@entry_id:165386)**（Céa's Lemma）指出，如果[双线性形式](@entry_id:746794)是连续且强制的，那么伽辽金解 $u_N$ 是**准最优**的，即它在[能量范数](@entry_id:274966)（由 $a(v,v)$ 诱导的范数）下的误差与在[子空间](@entry_id:150286) $V_N$ 中的最佳逼近误差只差一个常数因子：
$$
\|u - u_N\|_a \le \frac{M}{\alpha} \inf_{v_N \in V_N} \|u - v_N\|_a.
$$
这意味着伽辽金方法的[收敛速度](@entry_id:636873)完全由近似[子空间](@entry_id:150286)的逼近能力决定。对于使用 $p$ 次多项式、网格尺寸为 $h$ 的高阶有限元或谱元方法，如果真实解足够光滑（例如，$u \in H^{p+1}$），标准逼近理论给出以下[误差估计](@entry_id:141578)：
*   $H^1$ 范数误差：$\|u - u_h\|_{H^1(\Omega)} \lesssim (\frac{h}{p})^{p}$
*   $L^2$ 范数误差：$\|u - u_h\|_{L^2(\Omega)} \lesssim (\frac{h}{p})^{p+1}$
$L^2$ 范数下的更高一阶[收敛率](@entry_id:146534)是通过一个更精巧的**[Aubin-Nitsche对偶](@entry_id:167117)论证**得到的。

### 高等公式：[间断伽辽金方法](@entry_id:748369)

传统（或“连续”）伽辽金方法要求近似函数在整个区域上是连续的，即 $V_N \subset H^1(\Omega)$。**间断伽辽金**（Discontinuous Galerkin, DG）方法放宽了这一限制，允许近似函数在单元边界上存在间断。这带来了极大的灵活性，例如可以方便地处理[非协调网格](@entry_id:752550)、局部变动多项式次数和某些类型的[非线性](@entry_id:637147)问题。

为了处理[间断函数](@entry_id:143848)，[DG方法](@entry_id:748369)需要一套新的工具。
1.  **破碎[索博列夫空间](@entry_id:141995)**（Broken Sobolev Space）：[函数空间](@entry_id:143478)被定义为 $H^1(\mathcal{T}_h) = \{ v \in L^2(\Omega) : v|_K \in H^1(K) \text{ for all } K \in \mathcal{T}_h \}$，其中 $\mathcal{T}_h$ 是区域 $\Omega$ 的一个网格剖分。
2.  **迹、跳跃和[平均算子](@entry_id:746605)**：在两个单元 $K^+$ 和 $K^-$共享的内部面 $F$ 上，函数 $v$ 有两个迹，$v^+$ 和 $v^-$。我们定义**跳跃** $[v] = v^+ \mathbf{n}^+ + v^- \mathbf{n}^-$ 和**平均** $\{v\} = \frac{1}{2}(v^+ + v^-)$ 等算子。这些定义必须以一种不依赖于对单元任意标记为 $K^+$ 或 $K^-$ 的方式进行，以保证公式的内在一致性。
3.  **数值通量**（Numerical Flux）：DG公式的推导始于在每个单元 $K$ 上进行[分部积分](@entry_id:136350)。这会在每个单元的边界 $\partial K$ 上产生边界积分项。由于解是间断的，在内部面上，通量（如 $\mathbf{a}u$ 或 $A\nabla u$）是双值的。DG方法的核心思想是引入一个**数值通量**，记为 $\widehat{(\mathbf{a} u)} \cdot \mathbf{n}$，它是一个在整个面上单值的函数，由相邻单元的迹（以及边界上的边界数据）决定。

一个关键要求是**一致性**（consistency）：当将光滑的真解 $u$ 代入数值通量时，它必须还原为真实的物理通量，即 $\widehat{(\mathbf{a} u)} \cdot \mathbf{n} = (\mathbf{a} u) \cdot \mathbf{n}$。例如，对于[对流](@entry_id:141806)方程 $\nabla \cdot (\mathbf{a} u) = f$，一个常见且重要的一致性[数值通量](@entry_id:752791)是**[迎风通量](@entry_id:143931)**（upwind flux），它在面上简单地选取来自上游单元的解的值。例如，如果信息沿法向 $\mathbf{n}_F$ 从 $K^-$ 流向 $K^+$，则[迎风通量](@entry_id:143931)取 $u^-$ 的值。这种选择不仅保证了一致性，还为离散格式引入了稳定性。

### 实践中的现实：变分犯罪

在理论上，伽辽金方法 $a(u_N, v_N) = \ell(v_N)$ 是精确的。但在计算机上实现时，我们求解的往往是该问题的一个近似版本 $a_h(u_N^h, v_N) = \ell_h(v_N)$。理论与实践之间的这种偏离被称为**变分犯罪**（variational crime）。分析这种非精确方法的主要工具是**Strang第一引理**，它将总[误差分解](@entry_id:636944)为三部分：最佳逼近误差、由 $a_h \neq a$ 引起的[相容性误差](@entry_id:747725)和由 $\ell_h \neq \ell$ 引起的[相容性误差](@entry_id:747725)。

变分犯罪的两个常见来源是：
1.  **不精确积分**：[变分形式](@entry_id:166033)中的积分通常需要通过**数值求积**（numerical quadrature）来计算。如果求积规则的精度不足以精确计算[离散空间](@entry_id:155685)中所有[基函数](@entry_id:170178)组合的积分，就会引入误差。例如，在使用 $N$ 次多项式的谱方法中，刚度矩阵的被积函数最高可能是 $2N-2$ 次多项式。为了精确积分，需要使用至少 $N$ 个求积点的[Gauss-Legendre求积](@entry_id:138201)规则。如果使用的求积点数 $M$ 固定且不足（例如，$M  N$），那么当 $N$ 增加时，求积误差将不会减小，导致总[误差收敛](@entry_id:137755)到某个非零平台，这种现象称为**误差饱和**（error saturation）。
2.  **几何逼近**：当求解域 $\Omega$ 具有弯曲边界时，通常使用**等参元**（isoparametric elements）来近似几何。这意味着每个弯曲的物理单元 $K$ 被视为一个简单参考单元（如正方形或立方体）在某个[多项式映射](@entry_id:153569) $\Phi_h$下的像。[变分形式](@entry_id:166033)中的积分通过变量替换被[拉回](@entry_id:160816)到[参考单元](@entry_id:168425)上，但由于映射 $\Phi_h$ 只是真实几何的近似，其[雅可比行列式](@entry_id:137120) $J_h$ 和度量张量 $G_h$ 也是近似的。这导致离散[双线性形式](@entry_id:746794) $a_h$ 与精确形式 $a$ 不同。只要几何逼近足够精确（例如，映射误差足够小），就可以证明 $a_h$ 的强制性和连续性常数与 $a$ 的常数相差不大，从而保证了离散系统的[适定性](@entry_id:148590)和收敛性。

总之，理解[变分形式](@entry_id:166033)不仅是理论上的要求，也为处理数值方法实现中的各种实际挑战提供了强大的分析工具。从弱形式的推导到[适定性](@entry_id:148590)理论，再到离散化和对实际计算中不可避免的误差的分析，这些原理和机制构成了现代计算[PDE求解方法](@entry_id:170782)的基石。