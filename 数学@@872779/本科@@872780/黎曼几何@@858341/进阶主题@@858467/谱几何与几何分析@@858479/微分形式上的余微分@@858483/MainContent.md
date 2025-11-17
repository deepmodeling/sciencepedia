## 引言
在微分几何的研究中，外微分算子 $d$ 是一个基础工具，它以一种不依赖于任何度量结构的方式，捕捉了微分形式的变化。然而，[黎曼几何](@entry_id:160508)的核心在于研究度量所赋予的丰富几何结构。这就引出了一个核心问题：我们如何将度量结构整合到微分形式的分析中，并建立一个与外微分 $d$ 相辅相成的理论框架？答案就在于**[余微分算子](@entry_id:191334)**（codifferential），记为 $\delta$。它不仅是 $d$ 在度量诱导的[内积](@entry_id:158127)下的“对偶”，更是连接[流形](@entry_id:153038)分析、拓扑和物理学的关键桥梁。

本文旨在系统地介绍[余微分算子](@entry_id:191334)。我们将从其定义和基本性质出发，探索其在现代几何与物理中的核心地位。通过学习本文，你将理解[余微分](@entry_id:197182)是如何被定义的，它与经典向量微积分中的散度有何联系，以及它如何最终导向深刻的[霍奇理论](@entry_id:161814)。

*   在**原理与机制**一章中，我们将首先引入[霍奇星算子](@entry_id:197539)和[微分形式](@entry_id:146747)上的 $L^2$ [内积](@entry_id:158127)，这是定义[余微分](@entry_id:197182)的基础。随后，我们将把[余微分](@entry_id:197182)定义为[外微分](@entry_id:161900)的形式伴随，并推导出其依赖于度量的显式公式。最后，我们将探讨其基本性质，如 $\delta^2=0$，并将其与向量微积分中的[散度算子](@entry_id:265975)联系起来，为后续应用奠定基础。

*   在**应用与跨学科联系**一章中，我们将展示[余微分](@entry_id:197182)的强大威力。我们将看到它如何统一经典向量分析，如何为电磁学中的[麦克斯韦方程组](@entry_id:150940)提供一个优雅的几何表述，以及它如何通过[霍奇-拉普拉斯算子](@entry_id:261049)和调和形式，揭示[流形](@entry_id:153038)拓扑（[德拉姆上同调](@entry_id:158673)）与分析（[偏微分方程](@entry_id:141332)）之间的深刻联系，即[霍奇理论](@entry_id:161814)。

*   最后，在**动手实践**部分，你将通过一系列精心设计的计算练习，从欧氏空间到弯曲球面，亲手计算不同度规和[流形](@entry_id:153038)上的[余微分](@entry_id:197182)，从而将抽象的理论转化为具体的计算技能。

让我们从构建[余微分](@entry_id:197182)所需的基本工具——[霍奇星算子](@entry_id:197539)和[内积](@entry_id:158127)——开始，踏上这段探索几何深层结构的旅程。

## 原理与机制

在黎曼几何中，外微分算子 $d$ 捕捉了微分形式的“旋度”或变化率，并且具有一个基本性质，即 $d^2=0$。这一性质是[德拉姆上同调](@entry_id:158673)理论的基石。然而，$d$ 的定义完全依赖于[流形](@entry_id:153038)的[光滑结构](@entry_id:159394)，与黎曼度量无关。为了将度量结构引入[微分形式](@entry_id:146747)的分析中，我们需要一个与 $d$ 相辅相成的算子。这个算子就是**[余微分](@entry_id:197182)**（codifferential），通常记为 $\delta$。本章将系统地介绍[余微分](@entry_id:197182)的定义、性质及其在[几何分析](@entry_id:157700)中的核心作用。我们将从定义[微分形式](@entry_id:146747)上的[内积](@entry_id:158127)开始，导出[余微分](@entry_id:197182)作为[外微分](@entry_id:161900)的伴随算子，并探讨其与经典向量微积分中[散度算子](@entry_id:265975)的深刻联系。

### [霍奇星算子](@entry_id:197539)与微分形式上的[内积](@entry_id:158127)

为了在[微分形式](@entry_id:146747)空间上建立一个几何上自然的[内积](@entry_id:158127)结构，我们需要借助[黎曼度量](@entry_id:754359) $g$ 和[流形的定向](@entry_id:160954)。在一个 $n$ 维定向黎曼流形 $(M,g)$ 上，度量 $g$ 不仅在每个切空间 $T_xM$ 上定义了[内积](@entry_id:158127)，也通过对偶性在[余切空间](@entry_id:270516) $T_x^*M$ 及其外幂 $\Lambda^k T_x^*M$（即 $k$-形式空间）上诱导了逐点[内积](@entry_id:158127) $\langle \cdot, \cdot \rangle_g$。此外，$g$ 和[流形的定向](@entry_id:160954)唯一确定了一个**[黎曼体积形式](@entry_id:275973)**（Riemannian volume form）$\mathrm{vol}_g$。

有了这两个工具——逐点[内积](@entry_id:158127)和体积形式——我们就可以定义一个关键的算子：**[霍奇星算子](@entry_id:197539)**（Hodge star operator），记为 $*$。它是一个逐点作用的[线性同构](@entry_id:270529)，将 $k$-形式映射为 $(n-k)$-形式：
$* \colon \Omega^k(M) \to \Omega^{n-k}(M)$
其定义由以下关系唯一确定：对于任意两个 $k$-形式 $\alpha, \beta \in \Omega^k(M)$，它们的[外积](@entry_id:147029)满足
$$
\alpha \wedge *\beta = \langle \alpha, \beta \rangle_g \mathrm{vol}_g
$$
这个定义巧妙地将代数运算（外积）与几何结构（[内积](@entry_id:158127)和体积）联系在一起 [@problem_id:3028951]。从定义可以看出，[霍奇星算子](@entry_id:197539)深度依赖于度量 $g$（因为它决定了[内积](@entry_id:158127)和体积形式）和[流形的定向](@entry_id:160954)（因为它决定了体积形式的符号）。

[霍奇星算子](@entry_id:197539)对度量和定向的依赖性具有重要的理论意义。例如，如果保持度量 $g$ 不变，但反转[流形的定向](@entry_id:160954)（记为 $-\mathfrak{o}$），则体积形式变号，$\mathrm{vol}_{g,-\mathfrak{o}} = -\mathrm{vol}_{g,\mathfrak{o}}$。根据定义，这导致[霍奇星算子](@entry_id:197539)也变号：$*_{g,-\mathfrak{o}} = -*_{g,\mathfrak{o}}$。另一方面，如果保持定向不变，但对度量进行共形变换 $\tilde{g} = e^{2f}g$（其中 $f$ 是光滑函数），则作用于 $k$-形式的[霍奇星算子](@entry_id:197539)会按比例因子 $e^{(n-2k)f}$ 变化。一个特别值得注意的情况是，当[流形](@entry_id:153038)维数 $n$为偶数时，作用于中间次数 $k=n/2$ 的形式时，比例因子为 $e^0=1$，这意味着[霍奇星算子](@entry_id:197539)在中间次数上是**共形不变**的 [@problem_id:3035754]。

一旦定义了[霍奇星算子](@entry_id:197539)，我们就可以定义[微分形式](@entry_id:146747)的全局**$L^2$ [内积](@entry_id:158127)**。对于两个[紧支撑](@entry_id:276214)的 $k$-形式 $\alpha, \beta \in \Omega_c^k(M)$（或者在紧流形上，对所有光滑形式），其 $L^2$ [内积](@entry_id:158127)定义为：
$$
(\alpha, \beta)_{L^2} := \int_M \langle \alpha, \beta \rangle_g \mathrm{vol}_g = \int_M \alpha \wedge *\beta
$$
这个[内积](@entry_id:158127)为研究[微分形式](@entry_id:146747)的泛函分析性质提供了基础 [@problem_id:3028951] [@problem_id:3072544]。值得注意的是，即使在非定向[流形](@entry_id:153038)上，虽然无法全局定义[霍奇星算子](@entry_id:197539)（因为[体积形式](@entry_id:203000)无法全局一致地选取符号），但可以定义一个体积密度 $\mu_g$，从而仍然可以定义 $L^2$ [内积](@entry_id:158127)，这保证了后续定义的[余微分算子](@entry_id:191334)在非定向[流形](@entry_id:153038)上也是良定的 [@problem_id:3035754]。

### 作为外微分 $d$ 的形式伴随的[余微分](@entry_id:197182)

外[微分算子](@entry_id:140145) $d$ 将一个 $k$-形式映为一个 $(k+1)$-形式，即它的次数为 $+1$。在[希尔伯特空间](@entry_id:261193)的框架下，每个线性算子都有一个唯一的[伴随算子](@entry_id:140236)。对于微分形式空间上的 $L^2$ [内积](@entry_id:158127)，我们可以寻找 $d$ 的伴随算子。

**[余微分](@entry_id:197182)**（codifferential） $\delta$，有时也记作 $d^*$，被定义为外微分算子 $d$ 关于 $L^2$ [内积](@entry_id:158127)的**形式[伴随算子](@entry_id:140236)**（formal adjoint）。这意味着，对于任意 $(k-1)$-形式 $\alpha$ 和 $k$-形式 $\beta$（在紧流形上，或在一般[流形](@entry_id:153038)上要求它们具有[紧支撑](@entry_id:276214)以避免边界项），以下关系成立 [@problem_id:3068879] [@problem_id:3035534]：
$$
(d\alpha, \beta)_{L^2} = (\alpha, \delta\beta)_{L^2}
$$
展开[内积](@entry_id:158127)的定义，该关系式可以写为：
$$
\int_M \langle d\alpha, \beta \rangle_g \mathrm{vol}_g = \int_M \langle \alpha, \delta\beta \rangle_g \mathrm{vol}_g
$$
从这个定义可以直接看出[余微分算子](@entry_id:191334)的基本属性。因为 $d: \Omega^{k-1}(M) \to \Omega^k(M)$，它的伴随算子 $\delta$ 必须反转映射方向，即 $\delta: \Omega^k(M) \to \Omega^{k-1}(M)$。换言之，$\delta$ 是一个次数为 $-1$ 的算子 [@problem_id:3068879]。

### [余微分](@entry_id:197182)的显式公式

[余微分](@entry_id:197182)的定义是抽象的，但我们可以通过其定义和斯托克斯定理推导出它的一个显式、可计算的公式。这个推导过程是理解 $\delta$ 与度量结构关系的关键。

考虑定义式 $(d\alpha, \beta)_{L^2} = (\alpha, \delta\beta)_{L^2}$。左边可以写作 $\int_M d\alpha \wedge *\beta$。我们利用外微分的乘法法则 $d(\eta \wedge \zeta) = d\eta \wedge \zeta + (-1)^{\deg \eta} \eta \wedge d\zeta$。令 $\eta = \alpha$（次数为 $k-1$），$\zeta = *\beta$（次数为 $n-k$），我们有：
$$
d(\alpha \wedge *\beta) = d\alpha \wedge *\beta + (-1)^{k-1} \alpha \wedge d(*\beta)
$$
移项后对整个[流形](@entry_id:153038) $M$ 积分：
$$
\int_M d\alpha \wedge *\beta = \int_M d(\alpha \wedge *\beta) - (-1)^{k-1} \int_M \alpha \wedge d(*\beta)
$$
根据斯托克斯定理，对于[紧流形](@entry_id:158804)（或[紧支撑](@entry_id:276214)形式），一个恰当形式（如 $d(\alpha \wedge *\beta)$）在整个[流形上的积分](@entry_id:156150)为零。因此，上式简化为：
$$
\int_M d\alpha \wedge *\beta = (-1)^k \int_M \alpha \wedge d(*\beta)
$$
现在，我们将这个结果与定义式 $\int_M \alpha \wedge *(\delta\beta) = (\alpha, \delta\beta)_{L^2}$ 进行比较。由于该等式对所有 $\alpha$ 均成立，我们必然有：
$$
*(\delta\beta) = (-1)^k d(*\beta)
$$
为了解出 $\delta\beta$，我们在等式两边同时作用[霍奇星算子](@entry_id:197539) $*$。利用[霍奇星算子](@entry_id:197539)的性质 $*(*\omega) = (-1)^{p(n-p)}\omega$（其中 $\omega$ 是一个 $p$-形式），并注意到 $\delta\beta$ 是一个 $(k-1)$-形式，经过一系列符号运算，我们最终得到作用于 $k$-形式 $\omega$ 的[余微分](@entry_id:197182)的显式公式 [@problem_id:2970038] [@problem_id:3035534] [@problem_id:3068872]：
$$
\delta\omega = (-1)^{n(k+1)+1} *d*\omega
$$
这个公式是[余微分](@entry_id:197182)理论中的一个核心结果。它清楚地表明，[余微分算子](@entry_id:191334)是通过[霍奇星算子](@entry_id:197539)和外微分算子构造的。由于外微分 $d$ 是一个纯粹的[拓扑不变量](@entry_id:138526)，不依赖于度量，而[霍奇星算子](@entry_id:197539) $*$ 严重依赖于度量 $g$，因此**[余微分](@entry_id:197182) $\delta$ 是一个依赖于度量的算子** [@problem_id:2970038]。

有趣的是，尽管 $\delta$ 的定义似乎也依赖于定向（通过 $*$），但实际上**[余微分](@entry_id:197182)与定向无关**。从形式伴随的定义 $(\alpha, \delta\beta)_{g,\mathfrak{o}} = (d\alpha, \beta)_{g,\mathfrak{o}}$ 出发，如果反转定向，[内积](@entry_id:158127)双方都会变号，等式依然成立，因此 $\delta$ 保持不变。这也可以从显式公式中看出：反转定向时，两个 $*$ 算子都会变号，它们的效应相互抵消，从而使 $\delta$ 不变 [@problem_id:3035754]。

### 基本性质与实例

利用[余微分](@entry_id:197182)的定义和显式公式，我们可以推导出一系列重要的性质。

1.  **$\delta^2 = 0$**：这个性质是 $d^2=0$ 的直接对偶。证明非常简洁：对于任意形式 $\alpha, \beta$，我们有 $(\delta^2\alpha, \beta)_{L^2} = (\delta\alpha, d\beta)_{L^2} = (\alpha, d(d\beta))_{L^2} = (\alpha, d^2\beta)_{L^2}$。因为 $d^2\beta = 0$，所以 $(\delta^2\alpha, \beta)_{L^2} = 0$。由于这对所有 $\beta$ 都成立，我们必然有 $\delta^2\alpha = 0$。因此，算子本身满足 $\delta^2 = 0$ [@problem_id:3068879] [@problem_id:3068874]。

2.  **作用于 0-形式与 n-形式**：
    *   对于任意函数（0-形式）$f \in \Omega^0(M)$，由于 $\delta$ 将 $k$-形式映射到 $(k-1)$-形式，$\delta f$ 将是一个 $(-1)$-形式。约定 $(-1)$-形式空间是[零空间](@entry_id:171336)，因此我们总是有 $\delta f = 0$ [@problem_id:3072580] [@problem_id:3068874]。
    *   对于任意最高次数形式（$n$-形式）$\omega \in \Omega^n(M)$，$\delta\omega$ 通常不为零。任何 $n$-形式都可以写成 $\omega = f \cdot \mathrm{vol}_g$ 的形式，其中 $f$ 是一个函数。使用显式公式计算：$*\omega = f$，$d(*\omega) = df$，因此 $\delta\omega = (-1)^{n(n+1)+1} *(df)$。只要 $f$ 不是常数（在连通[流形](@entry_id:153038)上），$df$ 就不是零形式，从而 $\delta\omega$ 也不是零形式 [@problem_id:3068874]。

    **示例：非标准度量下的计算**
    为了更好地理解这些性质，让我们考虑一个具体的例子。设 $M$ 是一个二维环面 $\mathbb{T}^2$，具有[局部坐标](@entry_id:181200) $(x,y)$ 和一个非[欧几里得度量](@entry_id:147197) $g = dx^2 + 4dy^2$。[体积形式](@entry_id:203000)是 $dV_g = \sqrt{\det(g_{ij})} dx \wedge dy = 2 dx \wedge dy$。我们来计算作用在 $2$-形式 $\omega = \sin(x)\cos(y) dV_g$ 上的[余微分](@entry_id:197182) $\delta\omega$ [@problem_id:3072580]。

    根据公式，对于 $n=2, k=2$，$\delta = -*d*$。
    1.  $*\omega = *(\sin(x)\cos(y) \cdot 2 dx \wedge dy) = \sin(x)\cos(y) \cdot * (2 dx \wedge dy)$。根据定义 $*dV_g = 1$，所以 $*\omega = \sin(x)\cos(y)$。
    2.  $d(*\omega) = d(\sin(x)\cos(y)) = \cos(x)\cos(y) dx - \sin(x)\sin(y) dy$。
    3.  最后一步是计算 $*(d(*\omega))$。我们需要知道 $*$ 在 $1$-形式上的作用。对于给定的度量，我们可以计算出 $*dx = 2dy$ 和 $*dy = -\frac{1}{2}dx$。因此：
        $$
        *(d(*\omega)) = *(\cos(x)\cos(y) dx - \sin(x)\sin(y) dy) \\
        = \cos(x)\cos(y) (2dy) - \sin(x)\sin(y) (-\frac{1}{2}dx) \\
        = \frac{1}{2}\sin(x)\sin(y) dx + 2\cos(x)\cos(y) dy
        $$
    4.  最后，$\delta\omega = -*d*\omega = -\frac{1}{2}\sin(x)\sin(y) dx - 2\cos(x)\cos(y) dy$。这个结果显然不为零。

3.  **与[代数结构](@entry_id:137052)的关系**：外微分 $d$ 是一个**分次导子**（graded derivation），满足莱布尼兹法则。然而，它的[伴随算子](@entry_id:140236) $\delta$ 通常不具备这样的代数性质。在一般的弯曲[流形](@entry_id:153038)上，$\delta$ 不是一个分次反导子 [@problem_id:3068874]。

4.  **与对称性的关系**：如果 $\varphi: M \to M$ 是一个保定向的**[等距同构](@entry_id:273188)**（isometry），那么它保持度量 $g$ 不变。这意味着 $\varphi$ 的[拉回](@entry_id:160816)作用 $\varphi^*$ 与[霍奇星算子](@entry_id:197539) $*$ 可交换。又因为 $\varphi^*$ 总是与 $d$ 可交换，所以它也与由 $d$ 和 $*$ 构成的 $\delta$ 可交换，即 $\varphi^* \circ \delta = \delta \circ \varphi^*$ [@problem_id:3068874]。

### 与向量微积分及物理学的联系

[余微分算子](@entry_id:191334)一个极其重要的作用是它统一并推广了经典向量微积分中的**散度**（divergence）算子。

在一个黎曼流形上，一个向量场 $X$ 的散度 $\operatorname{div} X$ 是一个标量函数，它衡量了 $X$ 产生的流的[体积膨胀](@entry_id:144241)率。散度可以通过与梯度 $\nabla f$ 的关系来定义：
$$
\int_M f (\operatorname{div} X) \mathrm{vol}_g = -\int_M \langle \nabla f, X \rangle_g \mathrm{vol}_g
$$
现在，让我们将此与[余微分](@entry_id:197182)联系起来。利用度量 $g$，我们可以通过**[音乐同构](@entry_id:199976)**（musical isomorphism）在向量场和 $1$-形式之间建立[一一对应](@entry_id:143935)。向量场 $X$ 对应的 $1$-形式是 $X^\flat$（降号），$1$-形式 $\alpha$ 对应的向量场是 $\alpha^\sharp$（升号）。

对于一个 $1$-形式 $\alpha$，$\delta\alpha$ 是一个 $0$-形式（函数）。根据 $\delta$ 的定义，对于任何函数 $f$，我们有 $(df, \alpha)_{L^2} = (f, \delta\alpha)_{L^2}$。展开[内积](@entry_id:158127)，我们得到：
$$
\int_M \langle df, \alpha \rangle_g \mathrm{vol}_g = \int_M f(\delta\alpha) \mathrm{vol}_g
$$
利用[音乐同构](@entry_id:199976)，我们有 $\langle df, \alpha \rangle_g = \langle (\nabla f)^\flat, (\alpha^\sharp)^\flat \rangle_g = \langle \nabla f, \alpha^\sharp \rangle_g$。令 $X = \alpha^\sharp$，上式变为：
$$
\int_M \langle \nabla f, X \rangle_g \mathrm{vol}_g = \int_M f(\delta\alpha) \mathrm{vol}_g
$$
与散度的定义式比较，我们立即得到一个优美的关系 [@problem_id:3068879] [@problem_id:3068874]：
$$
\delta\alpha = -\operatorname{div}(\alpha^\sharp)
$$
这个等式表明，[余微分](@entry_id:197182)作用在 $1$-形式上，本质上就是其[对偶向量](@entry_id:161217)场的负散度。这为散度提供了一个不依赖于坐标的、纯粹的几何定义。

综合来看，在三维[欧氏空间](@entry_id:138052)中，算子 $d$ 和 $\delta$ 重新构建了我们熟悉的梯度、[旋度和散度](@entry_id:269913)：
*   **梯度**：对于函数 $f \in \Omega^0(\mathbb{R}^3)$，$df$ 对应于 $\operatorname{grad} f$。
*   **旋度**：对于 $1$-形式 $\alpha \in \Omega^1(\mathbb{R}^3)$， $d\alpha$ 是一个 $2$-形式，通过[霍奇对偶](@entry_id:263610) $*d\alpha$ 得到一个向量场，即 $\operatorname{curl}(\alpha^\sharp)$。
*   **散度**：对于 $1$-形式 $\alpha \in \Omega^1(\mathbb{R}^3)$，$\delta\alpha$ 对应于 $-\operatorname{div}(\alpha^\sharp)$。

这种统一的观点在电磁学等物理理论中至关重要，其中麦克斯韦方程组可以用微分形式优美地写成 $dF=0$ 和 $\delta F = -J$（$F$ 是[电磁场](@entry_id:265881) $2$-形式，$J$ 是[四维电流密度](@entry_id:262568) $1$-形式）。

### [霍奇-拉普拉斯算子](@entry_id:261049)与[调和形式](@entry_id:193378)

[余微分](@entry_id:197182)最重要的应用之一是构建**[霍奇-拉普拉斯算子](@entry_id:261049)**（Hodge-Laplacian），也称为**[拉普拉斯-贝尔特拉米算子](@entry_id:267002)**（Laplace-Beltrami operator），记为 $\Delta$。它被定义为 [@problem_id:3068879] [@problem_id:3072544]：
$$
\Delta = d\delta + \delta d
$$
我们来分析这个算子的构成：
*   $\delta$ 作用于 $k$-形式，得到 $(k-1)$-形式；再由 $d$ 作用，得到 $k$-形式。所以 $d\delta: \Omega^k(M) \to \Omega^k(M)$。
*   $d$ 作用于 $k$-形式，得到 $(k+1)$-形式；再由 $\delta$ 作用，得到 $k$-形式。所以 $\delta d: \Omega^k(M) \to \Omega^k(M)$。

因此，$\Delta$ 是一个保持形式次数的算子，$\Delta: \Omega^k(M) \to \Omega^k(M)$。

对于一个函数（0-形式）$f$，由于 $\delta f=0$，拉普拉斯算子简化为 $\Delta f = \delta d f$。在 $n$ 维欧氏空间中，通过计算可以证明 [@problem_id:1551412]：
$$
\Delta f = \delta(df) = -*d*(df) = -\sum_{i=1}^n \frac{\partial^2 f}{(\partial x^i)^2}
$$
这恰好是经典[拉普拉斯算子](@entry_id:146319)的负值。这个符号差异是几何学中的一个常见约定。

[拉普拉斯算子](@entry_id:146319)是一个[正算子](@entry_id:263696)，这一点可以通过[内积](@entry_id:158127)看出。对于任意 $k$-形式 $\omega$：
$$
(\Delta \omega, \omega)_{L^2} = (d\delta\omega + \delta d\omega, \omega)_{L^2} = (d\delta\omega, \omega)_{L^2} + (\delta d\omega, \omega)_{L^2}
$$
利用伴随性质，上式变为：
$$
(\delta\omega, \delta\omega)_{L^2} + (d\omega, d\omega)_{L^2} = \|\delta\omega\|_{L^2}^2 + \|d\omega\|_{L^2}^2
$$
因此，$(\Delta\omega, \omega)_{L^2} \ge 0$。

这个关系式引出了**调和形式**（harmonic forms）的概念。一个形式 $\gamma$ 被称为调和的，如果它位于[拉普拉斯算子](@entry_id:146319)的核中，即 $\Delta\gamma = 0$。根据上述[内积](@entry_id:158127)关系，$\Delta\gamma=0$ 当且仅当 $(\Delta\gamma, \gamma)_{L^2} = 0$，这又等价于 $\|\delta\gamma\|_{L^2}^2 + \|d\gamma\|_{L^2}^2 = 0$。由于范数非负，这成立的唯一可能是：
$$
d\gamma = 0 \quad \text{并且} \quad \delta\gamma = 0
$$
换言之，**一个形式是调和的，当且仅当它既是闭的（closed）又是余闭的（co-closed）**[@problem_id:3072544]。

[调和形式](@entry_id:193378)在[流形的拓扑](@entry_id:267834)和几何中扮演着中心角色。[霍奇理论](@entry_id:161814)的巅峰之作——**[霍奇分解定理](@entry_id:199343)**——断言，在任何紧致无边的定向[黎曼流形](@entry_id:261160)上，任何一个 $k$-形式 $\omega$ 都可以被唯一地[正交分解](@entry_id:148020)为一个恰当形式、一个余恰当形式和一个调和形式的和 [@problem_id:3072544]：
$$
\omega = d\alpha + \delta\beta + \gamma
$$
其中 $\gamma$ 是调和形式，并且三个分量 $d\alpha$, $\delta\beta$, $\gamma$ 在 $L^2$ [内积](@entry_id:158127)下两两正交。这个深刻的定理表明，每个[德拉姆上同调](@entry_id:158673)类都包含一个唯一的调和代表，从而在[流形的拓扑](@entry_id:267834)（上同调群）和分析（[偏微分方程](@entry_id:141332) $\Delta\gamma=0$ 的解）之间建立了一座桥梁。而这座桥梁的构建，完全离不开[余微分算子](@entry_id:191334) $\delta$。