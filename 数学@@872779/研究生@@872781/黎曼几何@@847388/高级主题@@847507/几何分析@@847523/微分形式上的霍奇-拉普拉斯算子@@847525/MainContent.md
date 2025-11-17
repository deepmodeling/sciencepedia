## 引言
在现代几何学中，[霍奇-拉普拉斯算子](@entry_id:261049)是连接分析、拓扑与几何的核心工具。它源于一个根本性的问题：如何利用[流形上的分析](@entry_id:637756)方法来揭示其深层的全局拓扑结构？通过将局部几何（由黎曼度量所定义）与[微分形式](@entry_id:146747)的[代数结构](@entry_id:137052)相结合，[霍奇理论](@entry_id:161814)提供了一个强有力的框架来解决这一问题，而[霍奇-拉普拉斯算子](@entry_id:261049)正是该框架的基石。本文旨在系统地阐述这一理论，带领读者穿越其严谨的数学构造，领略其在不同学科中的广泛应用。

在接下来的内容中，我们将分三步深入探索[霍奇-拉普拉斯算子](@entry_id:261049)的世界。在“原理与机制”一章中，我们将从最基本的构件——[外微分](@entry_id:161900)、[霍奇星算子](@entry_id:197539)和[余微分](@entry_id:197182)——出发，逐步构建起[霍奇-拉普拉斯算子](@entry_id:261049)，并证明其核心性质，最终导向宏伟的[霍奇分解定理](@entry_id:199343)。随后，在“应用与跨学科联系”一章中，我们将展示这一理论的强大威力，看它如何通过Bochner方法从曲率推断拓扑信息，如何在[复几何](@entry_id:159080)和凯勒流形上展现更丰富的结构，以及它如何为理论物理中的电磁学和规范场论提供统一的数学语言。最后，“动手实践”部分将通过具体的计算问题，帮助你将抽象的理论转化为切实的理解，让你亲手验证和应用这些深刻的数学思想。

## 原理与机制

本章深入探讨[霍奇-拉普拉斯算子](@entry_id:261049)（Hodge Laplacian）的构造及其基本性质。我们将从微分形式的[外代数](@entry_id:201164)出发，引入[黎曼度量](@entry_id:754359)所诱导的附加结构，并在此基础上定义[霍奇-拉普拉斯算子](@entry_id:261049)。本章旨在揭示该算子如何作为连接[流形](@entry_id:153038)几何、拓扑与分析的关键桥梁。我们将系统地建立其核心性质，阐明其在[霍奇理论](@entry_id:161814)中的中心地位，并探讨其在不同几何情境下的表现。

### 基本构造：算子 $d$、$\star$ 与 $\delta$

[霍奇理论](@entry_id:161814)的舞台是光滑黎曼流形 $(M,g)$ 上的微分形式空间 $\Omega^k(M)$。该理论的构建始于三个基本算子：[外微分](@entry_id:161900)、霍奇星号算子和[余微分](@entry_id:197182)。

**外微分算子** $d: \Omega^k(M) \to \Omega^{k+1}(M)$ 是一个纯粹的拓扑构造，它不依赖于[流形](@entry_id:153038)上的度量。其两个基本性质是核心：

1.  **[幂零性](@entry_id:147926) (Nilpotency)**：连续两次作用恒为零，即 $d^2 = 0$（或更准确地，$d_{k+1} \circ d_k = 0$）。这一性质是[德拉姆上同调](@entry_id:158673)理论的基石，它保证了闭形式（$d\alpha=0$）的空间包含了恰当形式（$\alpha=d\beta$）的空间。

2.  **分次[莱布尼茨法则](@entry_id:157949) (Graded Leibniz Rule)**：对于 $k$-形式 $\alpha$ 和 $\ell$-形式 $\beta$，外微分满足 $d(\alpha \wedge \beta) = d\alpha \wedge \beta + (-1)^k \alpha \wedge d\beta$。这表明 $d$ 是一个次数为 $+1$ 的分次导子。[@problem_id:2998558]

**霍奇星号算子 (Hodge Star Operator)** $\star: \Omega^k(M) \to \Omega^{n-k}(M)$ 是连接[黎曼度量](@entry_id:754359) $g$ 与[微分形式](@entry_id:146747)[外代数](@entry_id:201164)的关键纽带，其中 $n$ 是[流形](@entry_id:153038)的维数。它是一个逐点的[线性同构](@entry_id:270529)，其定义依赖于度量 $g$ 和[流形的定向](@entry_id:160954)。对于任意两个 $k$-形式 $\alpha, \beta \in \Omega^k(M)$，霍奇星号算子由以下关系唯一确定：
$$
\alpha \wedge \star\beta = \langle \alpha, \beta \rangle_g \, d\mathrm{vol}_g
$$
其中 $\langle \cdot, \cdot \rangle_g$ 是由度量 $g$ 在 $\Lambda^k T_x^*M$ 的纤维上诱导的逐点[内积](@entry_id:158127)，$d\mathrm{vol}_g$ 是[黎曼体积形式](@entry_id:275973)。这个定义优雅地将代数运算（楔积）与几何测量（[内积](@entry_id:158127)和体积）联系在一起。

利用度量和[体积形式](@entry_id:203000)，我们可以在微分形式空间上定义一个全局的 $L^2$ **[内积](@entry_id:158127)**：
$$
\langle\langle \alpha, \beta \rangle\rangle = \int_M \alpha \wedge \star \beta = \int_M \langle \alpha, \beta \rangle_g \, d\mathrm{vol}_g
$$
这个[内积](@entry_id:158127)赋予了微分形式空间以希尔伯特空间的结构（在适当完备化后）。

**[余微分算子](@entry_id:191334) (Codifferential)** $\delta: \Omega^k(M) \to \Omega^{k-1}(M)$ 是外微分算子 $d$ 在 $L^2$ [内积](@entry_id:158127)下的**形式[伴随算子](@entry_id:140236) (formal adjoint)**。这意味着对于[紧支撑](@entry_id:276214)形式（或在[紧流形](@entry_id:158804)上），它满足以下积分关系：
$$
\langle\langle d\alpha, \beta \rangle\rangle = \langle\langle \alpha, \delta\beta \rangle\rangle, \quad \forall \alpha \in \Omega^{k-1}(M), \beta \in \Omega^k(M)
$$
[@problem_id:2998558] [@problem_id:3035715]

通过斯托克斯公式和霍奇星号算子的性质，我们可以推导出 $\delta$ 的一个显式表达式。对于一个 $k$-形式 $\alpha$，其[余微分](@entry_id:197182)由下式给出：
$$
\delta\alpha = (-1)^{nk+n+1} \star d \star \alpha
$$
[@problem_id:2998573]
这个公式明确显示了 $\delta$ 对度量的深刻依赖性，因为它通过霍奇星号算子 $\star$ 与度量 $g$ 紧密相连。

与 $d^2=0$ 对偶地，[余微分算子](@entry_id:191334)同样具有**[幂零性](@entry_id:147926)**，即 $\delta^2 = 0$。这可以通过其伴随性质直接证明：对于任意形式 $\alpha, \beta$，我们有 $\langle\langle \delta^2\alpha, \beta \rangle\rangle = \langle\langle \delta\alpha, d\beta \rangle\rangle = \langle\langle \alpha, d^2\beta \rangle\rangle = \langle\langle \alpha, 0 \rangle\rangle = 0$。由于[内积](@entry_id:158127)的非退化性，这必然要求 $\delta^2\alpha=0$。[@problem_id:2998558] [@problem_id:2998573]

需要强调的是，尽管 $d$ 是一个分次导子，但 $\delta$ **不是**。也就是说，它一般不满足关于[楔积](@entry_id:147029)的分次[莱布尼茨法则](@entry_id:157949)。这是因为 $\star$ 算子与楔积的相互作用非常复杂。[@problem_id:2998558]

### [霍奇-拉普拉斯算子](@entry_id:261049) Δ

有了外微分 $d$ 和[余微分](@entry_id:197182) $\delta$ 这两个[幂零算子](@entry_id:148875)，我们便可以构造一个二阶[微分算子](@entry_id:140145)，即**[霍奇-拉普拉斯算子](@entry_id:261049) (Hodge Laplacian)**，或简称为**拉普拉斯算子**。它定义为：
$$
\Delta = d\delta + \delta d
$$
这个算子作用于 $k$-形式，并产生一个同次的 $k$-形式，即 $\Delta: \Omega^k(M) \to \Omega^k(M)$。

一个富有启发性的视角来自于引入**德拉姆算子 (de Rham operator)** $D = d + \delta$。这个算子作用于总[微分形式](@entry_id:146747)空间 $\Omega^\bullet(M) = \bigoplus_k \Omega^k(M)$。由于 $d^2=0$ 和 $\delta^2=0$，计算 $D$ 的平方会得到：
$$
D^2 = (d+\delta)(d+\delta) = d^2 + d\delta + \delta d + \delta^2 = d\delta + \delta d = \Delta
$$
因此，[霍奇-拉普拉斯算子](@entry_id:261049)可以被看作是德拉姆算子的平方，这暗示了它与[流形](@entry_id:153038)上的“[二阶导数](@entry_id:144508)”或能量有关。[@problem_id:2998573] 值得注意的是，$\Delta$ 也是 $d$ 和 $\delta$ 的**分次反交换子 (graded anti-commutator)**，即 $\Delta = [d, \delta]_+ = d\delta - (-1)^{(+1)(-1)}\delta d = d\delta + \delta d$。[@problem_id:2998573]

[霍奇-拉普拉斯算子](@entry_id:261049)具有以下几个至关重要的性质：

1.  **与 $d$ 和 $\delta$ 的交换性**：$\Delta$ 与 $d$ 和 $\delta$ 均可交换。例如，证明 $\Delta d = d\Delta$ 如下：
    $$
    \Delta d = (d\delta + \delta d)d = d\delta d + \delta d^2 = d\delta d
    $$
    $$
    d\Delta = d(d\delta + \delta d) = d^2\delta + d\delta d = d\delta d
    $$
    因此 $\Delta d = d\Delta$。同理可证 $\Delta\delta = \delta\Delta$。[@problem_id:2998558] 这一性质意味着[拉普拉斯算子](@entry_id:146319)将闭形式映为闭形式，将余闭形式（$\delta\alpha=0$）映为余闭形式，这对[上同调理论](@entry_id:270863)至关重要。

2.  **自伴性与非负性**：在紧致无边[流形](@entry_id:153038)上，$\Delta$ 是一个**自伴 (self-adjoint)** 且**非负 (non-negative)** 的算子。
    *   **自伴性**：$(\langle\langle \Delta\alpha, \beta \rangle\rangle = \langle\langle \alpha, \Delta\beta \rangle\rangle)$ 来自于 $d$ 和 $\delta$ 之间的伴随关系。
    *   **非负性**：通过计算 $\langle\langle \Delta\alpha, \alpha \rangle\rangle$ 可以揭示其几何意义：
        $$
        \langle\langle \Delta\alpha, \alpha \rangle\rangle = \langle\langle (d\delta+\delta d)\alpha, \alpha \rangle\rangle = \langle\langle d\delta\alpha, \alpha \rangle\rangle + \langle\langle \delta d\alpha, \alpha \rangle\rangle
        $$
        利用伴随关系，上式变为：
        $$
        \langle\langle \Delta\alpha, \alpha \rangle\rangle = \langle\langle \delta\alpha, \delta\alpha \rangle\rangle + \langle\langle d\alpha, d\alpha \rangle\rangle = \|\delta\alpha\|^2 + \|d\alpha\|^2
        $$
        这个优美的恒等式称为**霍奇-德拉姆恒等式 (Hodge-de Rham identity)**。由于范数的平方总是非负的，我们立即得到 $\langle\langle \Delta\alpha, \alpha \rangle\rangle \ge 0$。[@problem_id:2998558] [@problem_id:2998573]

### [调和形式](@entry_id:193378)与[霍奇定理](@entry_id:196610)

霍奇-德拉姆恒等式是[霍奇理论](@entry_id:161814)的基石。它直接引出了**调和形式 (harmonic forms)** 的概念和性质。

一个 $k$-形式 $\alpha$ 被称为**调和的**，如果它位于[霍奇-拉普拉斯算子](@entry_id:261049)的核中，即 $\Delta\alpha = 0$。

根据霍奇-德拉姆恒等式，在紧致无边[流形](@entry_id:153038)上，$\langle\langle \Delta\alpha, \alpha \rangle\rangle = 0$ 当且仅当 $\|\delta\alpha\|^2 + \|d\alpha\|^2 = 0$。这又当且仅当 $\|\delta\alpha\|^2=0$ 且 $\|d\alpha\|^2=0$，即 $\delta\alpha=0$ 且 $d\alpha=0$。因此，我们得到了调和形式的根本特征：
> 在紧致无边[流形](@entry_id:153038)上，一个形式是调和的，当且仅当它既是**闭的 (closed)** 又是**余闭的 (co-closed)**。
> $$ \Delta\alpha = 0 \iff d\alpha=0 \text{ and } \delta\alpha=0 $$
[@problem_id:2998558] [@problem_id:3035686]

这个结果的意义非凡。它将一个分析问题（求解一个[二阶偏微分方程](@entry_id:175326) $\Delta\alpha = 0$）与两个[一阶条件](@entry_id:140702)（$d\alpha=0$ 和 $\delta\alpha=0$）等同起来。

**[霍奇分解定理](@entry_id:199343) (Hodge Decomposition Theorem)** 指出，在紧致无边[流形](@entry_id:153038)上，任何 $k$-形式的空间 $\Omega^k(M)$ 都可以正交地分解为三个[子空间之和](@entry_id:180324)：
$$
\Omega^k(M) = \mathcal{H}^k(M) \oplus \mathrm{Im}(d_{k-1}) \oplus \mathrm{Im}(\delta_{k+1})
$$
这里，$\mathcal{H}^k(M)$ 是调和 $k$-形式构成的空间，$\mathrm{Im}(d_{k-1})$ 是恰当 $k$-形式（即 $d$ 的像）的空间，而 $\mathrm{Im}(\delta_{k+1})$ 是余恰当 $k$-形式（即 $\delta$ 的像）的空间。[@problem_id:3035686]

这个分解是[霍奇理论](@entry_id:161814)的巅峰之作，它直接导向了**[霍奇定理](@entry_id:196610) (Hodge Theorem)**：
> 在紧致无边黎曼流形上，每个[德拉姆上同调](@entry_id:158673)类 $[ \alpha ] \in H^k_{\text{dR}}(M)$ 中，存在**唯一一个**调和代表元。

这个调和代表元不仅是唯一的，而且是其所在上同调类中 $L^2$ **范数最小**的元素。这是因为任何与调和形式 $\alpha$ 上同调的另一个形式 $\omega$ 都可以写成 $\omega = \alpha + d\eta$。由于调和形式与恰当形式正交（因为 $\langle\langle \alpha, d\eta \rangle\rangle = \langle\langle \delta\alpha, \eta \rangle\rangle = 0$），我们有 $\|\omega\|^2 = \|\alpha\|^2 + \|d\eta\|^2 \ge \|\alpha\|^2$。[@problem_id:3035686]

[霍奇定理](@entry_id:196610)建立了一个深刻的同构关系：
$$
\mathcal{H}^k(M) \cong H^k_{\text{dR}}(M)
$$
它意味着[流形的拓扑](@entry_id:267834)[不变量](@entry_id:148850)（上同调群）可以通过求解一个分析方程（拉普拉斯方程）来研究。这是一个连接拓扑与分析的壮丽桥梁。

### [拉普拉斯算子](@entry_id:146319)的具体表现

为了更深入地理解[霍奇-拉普拉斯算子](@entry_id:261049)，我们考察它在具体情境下的表现，这能揭示其与经典向量分析和[流形曲率](@entry_id:187680)的联系。

#### [局部坐标](@entry_id:181200)表达式与物理诠释

在[局部坐标](@entry_id:181200)中，[余微分算子](@entry_id:191334) $\delta$ 的表达式可以与经典[向量场的散度](@entry_id:136342)联系起来。特别是在一个 $n$ 维[流形](@entry_id:153038)上：

-   对于 0-形式（函数）$f$，$\delta f = 0$，因为 $\delta$ 将形式的阶数降低 1。[@problem_id:3035715]
-   对于 [1-形式](@entry_id:270392) $\alpha$，可以证明 $\delta\alpha$ 等于与 $\alpha$ 度量对偶的向量场 $\alpha^\sharp$ 的**负散度**：
    $$
    \delta\alpha = -\text{div}(\alpha^\sharp) = -\frac{1}{\sqrt{\det(g_{ij})}} \sum_{j} \frac{\partial}{\partial x^j} \left( \sqrt{\det(g_{ij})} (\alpha^\sharp)^j \right)
    $$
    其中 $(\alpha^\sharp)^j = \sum_i g^{ji}\alpha_i$。这个关系为抽象的[余微分](@entry_id:197182)提供了具体的物理图像。例如，在三维[欧氏空间](@entry_id:138052)中，这对应于经典电磁学中的关系式 $\nabla \cdot \mathbf{A}$。[@problem_id:3035715]

#### 度量共形变化的影响

[霍奇理论](@entry_id:161814)中的算子，除 $d$ 之外，都依赖于度量。考察在度量**共形变化** $\tilde{g} = e^{2f}g$ 下这些算子的行为，可以深化对这种依赖性的理解。在这种变换下：

-   逐点[内积](@entry_id:158127)变换为 $\langle\alpha, \beta\rangle_{\tilde{g}} = e^{-2kf} \langle\alpha, \beta\rangle_g$。
-   体积形式变换为 $d\mathrm{vol}_{\tilde{g}} = e^{nf} d\mathrm{vol}_g$。
-   霍奇星号算子变换为 $\tilde{\star}\omega = e^{(n-2k)f}\star\omega$（对于 $k$-形式 $\omega$）。[@problem_id:3035694]

由于 $\delta$ 和 $\Delta$ 的定义都依赖于 $\star$，它们的变换规律也变得复杂。例如，对于[余微分](@entry_id:197182) $\tilde{\delta}$，其变换不仅包含一个缩放因子 $e^{-2f}$，还额外增加了一项与函数 $f$ 的梯度相关的项。因此，$\tilde{\delta}$ 和 $\tilde{\Delta}$ 一般不与原算子成简单的比例关系。这表明[霍奇-拉普拉斯算子](@entry_id:261049)深刻地反映了[黎曼度量](@entry_id:754359)的局部几何细节，而不仅仅是其共形结构。[@problem_id:3035694]

#### 曲率的浮现：Weitzenböck 公式

[霍奇-拉普拉斯算子](@entry_id:261049)与[流形曲率](@entry_id:187680)之间存在一个惊人的深刻联系，这一联系由 **Weitzenböck 公式** 所揭示。通过在计算 $\Delta\alpha$ 的过程中引入列维-奇维塔联络 $\nabla$ 并利用曲率的定义（二阶[协变导数的[交换](@entry_id:198075)子](@entry_id:158878)），可以推导出作用于 [1-形式](@entry_id:270392) $\alpha$ 的[拉普拉斯算子](@entry_id:146319)具有以下形式：
$$
\Delta\alpha = \nabla^*\nabla\alpha + \mathrm{Ric}(\alpha^\sharp, \cdot)^\flat
$$
这里，$\nabla^*\nabla = -\sum_j \nabla_j \nabla^j$ 是**[联络拉普拉斯算子](@entry_id:197120) (connection Laplacian)**，而 $\mathrm{Ric}$ 是[里奇曲率张量](@entry_id:271424)。

这个公式的内涵极其丰富。为了看得更清楚，我们可以在一点 $p$ 处的[法坐标](@entry_id:143194)系下计算。在该[坐标系](@entry_id:156346)下，$g_{ij}(p)=\delta_{ij}$ 且克氏符 $\Gamma_{ij}^k(p)=0$。经过计算，$\Delta\alpha$ 的第 $i$ 个分量在点 $p$ 处为：
$$
(\Delta \alpha)_{i}(p) = - \sum_{j=1}^n \frac{\partial^2 \alpha_i}{\partial (x^j)^2} (p) + \sum_{j=1}^n \mathrm{Ric}_{ij}(p) \alpha_j(p)
$$
[@problem_id:2998568]

这个结果——**Weitzenböck-[Lichnerowicz 公式](@entry_id:159658)**——是几何分析中的里程碑。它表明，[霍奇-拉普拉斯算子](@entry_id:261049)可以分解为一个“平坦”的二阶部分（类似于[欧氏空间](@entry_id:138052)中的拉普拉斯算子）和一个零阶的“曲率”部分。曲率在此不再是[高阶导数](@entry_id:140882)中的复杂项，而是直接作为算子的一个线性项（势项）出现。这个公式是证明许多几何与拓扑定理（如 Bochner 消失定理）的出发点，它完美地展示了[分析算子](@entry_id:746429) $\Delta$ 如何蕴含着深刻的几何信息。

### 分析性质与高等主题

[霍奇-拉普拉斯算子](@entry_id:261049)的强大威力源于其作为偏微分算子的优良性质，这些性质使其理论可以扩展到更广泛的几何情境中。

#### 椭圆性

从[偏微分方程](@entry_id:141332)的视角看，$\Delta$ 是一个**[椭圆算子](@entry_id:181616) (elliptic operator)**。一个二阶[微分算子](@entry_id:140145) $L$ 的**主象征 (principal symbol)** $\sigma_2(L)(x, \xi)$ 捕捉了其最高阶（二阶）导数的行为。对于[霍奇-拉普拉斯算子](@entry_id:261049)，其主象征具有非常简单的形式：
$$
\sigma_2(\Delta)(x, \xi) = |\xi|_g^2 \mathrm{Id}
$$
其中 $\xi \in T_x^*M$ 是[余切空间](@entry_id:270516)中的一个余向量，$\mathrm{Id}$ 是作用在 $\Lambda^k T_x^*M$ 上的[恒等映射](@entry_id:634191)。这意味着在任何方向 $\xi$ 上，算子的最高阶部分都表现为一个正的标量乘以[恒等变换](@entry_id:264671)。

这一性质意味着 $\Delta$ 是**强椭圆的 (strongly elliptic)**。强椭圆性是[椭圆算子](@entry_id:181616)理论中最理想的性质，它保证了：
1.  **[椭圆正则性](@entry_id:177548) (Elliptic Regularity)**：若 $\Delta\omega = \eta$，则 $\omega$ 的[光滑性](@entry_id:634843)比 $\eta$ “高两阶”。特别是，如果 $\eta$ 是光滑的，$L^2$ 意义下的解 $\omega$ 也必然是光滑的。这就是为什么[调和形式](@entry_id:193378)（$\Delta\omega=0$ 的解）总是光滑形式的原因。[@problem_id:2998570]
2.  在紧流形上，[椭圆算子](@entry_id:181616)的核（即[调和形式](@entry_id:193378)空间 $\mathcal{H}^k(M)$）是**有限维**的。这保证了上同调群是有限维的。

[@problem_id:3035682]

#### 扩展到[非紧流形](@entry_id:185981)

[霍奇理论](@entry_id:161814)可以推广到[非紧流形](@entry_id:185981)，但这需要更精细的[泛函分析](@entry_id:146220)工具。

在[非紧流形](@entry_id:185981)上，定义在[紧支撑](@entry_id:276214)光滑形式上的 $\Delta$ 算子是一个[对称算子](@entry_id:272489)，但它可能有多个不同的[自伴扩张](@entry_id:264525)。然而，一个关键的定理（Gaffney 定理）指出，如果[流形](@entry_id:153038) $(M,g)$ 是**完备的 (complete)**，那么 $\Delta$ 在 $C_c^\infty(\Lambda^k T^*M)$ 上是**本质自伴的 (essentially self-adjoint)**。这意味着它有**唯一的**[自伴扩张](@entry_id:264525)，从而使得 $L^2$ **调和形式**的空间 $\mathcal{H}^k_{(2)}(M) = \ker(\Delta)$ 得以被明确定义。[@problem_id:2998570]

在[完备流形](@entry_id:190409)上，[霍奇分解定理](@entry_id:199343)依然成立，但需要使用[闭包](@entry_id:148169)：
$$
L^2\Omega^k(M) = \mathcal{H}^k_{(2)}(M) \oplus \overline{\mathrm{Im}(d)} \oplus \overline{\mathrm{Im}(\delta)}
$$
这导致了 $L^2$ **[霍奇定理](@entry_id:196610)**：$L^2$ [调和形式](@entry_id:193378)空间同构于**约化 $L^2$ 上同调群 (reduced $L^2$ cohomology)**：
$$
\mathcal{H}^k_{(2)}(M) \cong H^k_{(2),\text{red}}(M) = \ker(d) / \overline{\mathrm{Im}(d)}
$$
[@problem_id:3035687]
如果 $d$ 的像恰好是[闭集](@entry_id:136446)，那么约化与非[约化上同调](@entry_id:268050)群相等，此时 $\mathcal{H}^k_{(2)}(M)$ 同构于通常的 $L^2$ 上同调群。[@problem_id:3035687] 与紧流形不同，[非紧流形](@entry_id:185981)上的 $L^2$ [调和形式](@entry_id:193378)空间可能是无限维的。

#### [带边流形](@entry_id:159788)

当[流形](@entry_id:153038) $M$ 带有光滑边界 $\partial M$ 时，$\Delta$ 算子一般不再是自伴的，除非施加适当的**边界条件 (boundary conditions)**。[格林公式](@entry_id:173118)显示，在积分 $(\Delta\omega, \eta)$ 时会出现一个边界项。为了使 $\Delta$ 成为[自伴算子](@entry_id:152188)，我们需要选择一个定义域，使得对于定义域中的任何形式 $\omega, \eta$，该边界项恒为零。

两种典范的[自伴扩张](@entry_id:264525)是通过两种不同的边界条件得到的：

1.  **绝对边界条件 (Absolute Boundary Conditions)**：要求形式的**法向分量 (normal part)** 为零。具体而言，对于 $k$-形式 $\omega$，其定义域由以下条件确定：
    $$
    i^*(\iota_\nu \omega) = 0 \quad \text{and} \quad i^*(\iota_\nu d\omega) = 0
    $$
    其中 $\nu$ 是边界上的单位外[法向量场](@entry_id:268853)，$i^*$ 是到边界的限制映射，$\iota_\nu$ 是与 $\nu$ 的[内积](@entry_id:158127)。这定义了拉普拉斯算子 $\Delta_A$。

2.  **相对边界条件 (Relative Boundary Conditions)**：要求形式的**切向分量 (tangential part)** 为零。具体而言，其定义域由以下条件确定：
    $$
    i^*\omega = 0 \quad \text{and} \quad i^*(\delta\omega) = 0
    $$
    这定义了[拉普拉斯算子](@entry_id:146319) $\Delta_R$。

[@problem_id:2998566]
这两种不同的[自伴扩张](@entry_id:264525)分别对应于不同的[上同调理论](@entry_id:270863)（绝对上同调和[相对上同调](@entry_id:272456)），在物理和几何中有广泛的应用。