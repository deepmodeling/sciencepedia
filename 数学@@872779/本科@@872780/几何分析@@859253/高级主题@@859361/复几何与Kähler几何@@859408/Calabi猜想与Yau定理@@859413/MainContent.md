## 引言
在复[微分几何](@entry_id:145818)的宏伟蓝图中，寻找[流形](@entry_id:153038)上的“最佳”或“典范”度量是一个核心追求。这些特殊的度量不仅能揭示[流形](@entry_id:153038)最深刻的几何与拓扑性质，还在理论物理中扮演着关键角色。[卡拉比猜想](@entry_id:180885)及其由丘成桐（Shing-Tung Yau）完成的证明，正是这一探索方向上的巅峰之作，它为在凯勒流形上指定曲率形态提供了强大的理论武器。

该理论的核心问题是：我们能在多大程度上自由地规定一个凯勒流形的里奇曲率？是否可以“雕刻”出一个度量，使其曲率恰好符合我们预先给定的形式？这个问题最初由 Eugenio Calabi 提出，它的答案连接了局部[几何分析](@entry_id:157700)与全局[拓扑不变量](@entry_id:138526)。

本文将带领读者系统性地探索这一宏伟理论。在“原理与机制”一章中，我们将奠定[凯勒几何](@entry_id:160314)的基础，阐明猜想如何被转化为一个高度[非线性](@entry_id:637147)的复[蒙日-安培方程](@entry_id:268604)，并概述丘成桐证明其解存在性的关键步骤。接着，在“应用与交叉学科联系”一章中，我们将见证该定理如何催生了[卡拉比-丘流形](@entry_id:159253)这一核心概念，并探讨其在代数几何、规范场论乃至[弦理论](@entry_id:145688)中的深远影响。最后，通过“动手实践”中的具体演算，读者将有机会亲手验证这些抽象理论在具体例子中的表现。

让我们首先深入理论的核心，从理解其基本原理与机制开始。

## 原理与机制

本章旨在系统性地阐述[卡拉比猜想](@entry_id:180885)（Calabi Conjecture）及其证明的核心原理与机制。我们将从[复几何](@entry_id:159080)的基本概念出发，逐步深入到问题的几何与分析表述，最终探讨丘成桐（Shing-Tung Yau）定理的证明策略及其在构造[典范度量](@entry_id:266957)（canonical metrics）方面的深远应用。

### 从埃尔米特几何到[凯勒几何](@entry_id:160314)

在进入[卡拉比猜想](@entry_id:180885)的腹地之前，我们必须首先建立起坚实的几何基础。这一基础始于**复流形 (complex manifold)** 的概念。一个复维度为 $n$ 的复流形，是一个实维度为 $2n$ 的光滑流形，其上配备了一个[坐标图](@entry_id:156506)册，并且任意两个交叠的[坐标图](@entry_id:156506)之间的过渡映射都是全纯函数。这种结构赋予了[流形](@entry_id:153038)一种“刚性”，远比[光滑结构](@entry_id:159394)更为严格。[@problem_id:3066671]

在复流形 $M$ 上，我们可以定义度量结构。一个**[埃尔米特度量](@entry_id:202337) (Hermitian metric)** $h$ 是在全纯切丛 $T^{1,0}M$ 上一个光滑变化的、正定的埃尔米特[半双线性形式](@entry_id:154766)。这意味着在每一点的[切空间](@entry_id:199137)上，$h$ 都定义了一个[内积](@entry_id:158127)，它在第一个变量上是复线性的，在第二个变量上是[共轭线性](@entry_id:268590)的，并满足[埃尔米特对称性](@entry_id:266311) $h(v,w) = \overline{h(w,v)}$。[@problem_id:3066671] 每一个[埃尔米特度量](@entry_id:202337)都唯一对应一个[黎曼度量](@entry_id:754359) $g$ 和一个实 $2$-形式 $\omega$，它们分别是 $h$ 的实部和虚部的相反数。具体而言，$g(X,Y) = \operatorname{Re}h(X,Y)$ 且 $\omega(X,Y) = -\operatorname{Im}h(X,Y)$。这两个量与[复结构](@entry_id:269128) $J$ 密切相关，满足 $g(JX,JY) = g(X,Y)$（度量与[复结构](@entry_id:269128)兼容）以及 $\omega(X,Y) = g(JX,Y)$。这个 $2$-形式 $\omega$ 被称为**基本形式 (fundamental form)**。

在[复流形](@entry_id:159076)上，$\omega$ 自动是一个 **$(1,1)$-形式**，意味着它在两个 $(1,0)$-型向量或两个 $(0,1)$-型向量上取值为零。然而，埃尔米特几何与一个更特殊、更重要的几何——**[凯勒几何](@entry_id:160314) (Kähler geometry)** 之间存在着一道关键的鸿沟。一个埃尔米特[流形](@entry_id:153038)被称为**凯勒流形 (Kähler manifold)**，当且仅当其基本形式 $\omega$ 是闭的，即 $d\omega = 0$。[@problem_id:3066671]

$d\omega=0$ 这一条件绝非平凡。它施加了一个强大的局部约束，极大地简化了[流形](@entry_id:153038)的几何性质。例如，它等价于复结构 $J$ 在由 $g$ 诱导的[列维-奇维塔联络](@entry_id:161107)下是平行的（$\nabla J = 0$）。许多复流形（如霍普夫[曲面](@entry_id:267450)）可以拥有[埃尔米特度量](@entry_id:202337)，但无法拥有任何凯勒度量，这意味着在这些[流形](@entry_id:153038)上，任何[埃尔米特度量](@entry_id:202337)的基本形式 $\omega$ 都不可能是闭的。[@problem_id:3066671] 值得注意的是，在带有一个几乎复结构 $J$ 和一个兼容度量 $g$ 的[流形](@entry_id:153038)上，$d\omega=0$ 并不意味着 $J$ 是可积的（即其[奈恩黑斯张量](@entry_id:159184)为零）。存在所谓的“严格殆凯勒流形”，它们满足 $d\omega=0$，但其几乎[复结构](@entry_id:269128)并非来自一个[复结构](@entry_id:269128)。[@problem_id:3066671] 我们的讨论将严格限制在 $J$ 可积且 $d\omega=0$ 的凯勒流形框架内。

### [凯勒几何](@entry_id:160314)中的曲率

在[凯勒流形](@entry_id:161192)上，曲率扮演着核心角色。我们需要区分两种主要的曲率概念：黎曼几何中的[里奇张量](@entry_id:159336)和[复几何](@entry_id:159080)中的[里奇形式](@entry_id:183612)。

**[里奇形式](@entry_id:183612) (Ricci form)**，记作 $\mathrm{Ric}(\omega)$ 或 $\rho$，是与凯勒度量 $\omega$ 相关的最重要的曲率[不变量](@entry_id:148850)之一。在局部全纯坐标 $(z^1, \dots, z^n)$ 下，凯勒形式写作 $\omega = \sqrt{-1} \sum_{j,k} g_{j\bar{k}} dz^j \wedge d\bar{z}^k$，其中 $(g_{j\bar{k}})$ 是一个正定[埃尔米特矩阵](@entry_id:155147)。[里奇形式](@entry_id:183612)则由以下公式给出：
$$
\mathrm{Ric}(\omega) = -\sqrt{-1} \partial \bar{\partial} \log \det(g_{j\bar{k}})
$$
这个定义表明，[里奇形式](@entry_id:183612)是一个实值的、闭的 $(1,1)$-形式。[@problem_id:3066689] [@problem_id:3066671]

另一方面，我们有来自黎曼几何的**[里奇曲率张量](@entry_id:271424) (Ricci curvature tensor)** $\mathrm{Ric}^R$，它是一个对称的 $(0,2)$-型张量，通过追踪[黎曼曲率张量](@entry_id:160189)得到。在[凯勒流形](@entry_id:161192)上，这两个曲率概念通过[复结构](@entry_id:269128) $J$ 优美地联系在一起。它们之间的关系可以表示为：
$$
\mathrm{Ric}(\omega)(X,Y) = \mathrm{Ric}^R(JX,Y)
$$
对于任意实[切向量](@entry_id:265494) $X,Y$。这个等式揭示了[里奇形式](@entry_id:183612)本质上是“旋转”后的里奇张量。[@problem_id:3066689]

从这个关系可以推导出另一个重要的量——**标量曲率 (scalar curvature)** $S$。标量曲率 $S$ 是黎曼[里奇张量](@entry_id:159336) $\mathrm{Ric}^R$ 关于度量 $g$ 的迹。在[凯勒几何](@entry_id:160314)中，它与[里奇形式](@entry_id:183612)的迹 $\operatorname{tr}_\omega \mathrm{Ric}(\omega)$（即用凯勒形式 $\omega$ 的逆去收缩[里奇形式](@entry_id:183612)）密切相关。它们的关系是：
$$
S = 2 \operatorname{tr}_\omega \mathrm{Ric}(\omega)
$$
因子 $2$ 的出现源于实维度（$2n$）和复维度（$n$）之间的差异：$S$ 是在 $2n$ 个实维度上求迹，而 $\operatorname{tr}_\omega \mathrm{Ric}(\omega)$ 是在 $n$ 个复维度上求迹。[@problem_id:3066689]

### [第一陈类](@entry_id:201400)与[里奇曲率](@entry_id:162038)

几何学的一个深刻主题是联结[流形](@entry_id:153038)的局部几何（曲率）与全局拓扑（[拓扑不变量](@entry_id:138526)）。在[凯勒几何](@entry_id:160314)中，这一联结的典范便是[里奇形式](@entry_id:183612)与**[第一陈类](@entry_id:201400) (first Chern class)** $c_1(M)$ 之间的关系。

[第一陈类](@entry_id:201400) $c_1(M) \in H^2(M, \mathbb{Z})$ 是[复流形](@entry_id:159076) $M$ 的一个基本[拓扑不变量](@entry_id:138526)，它衡量了全纯切丛 $T^{1,0}M$ 的“扭曲”程度。根据陈-韦伊理论 (Chern-Weil theory)，这个拓扑不变量可以通过对任意一个切丛[联络的曲率](@entry_id:159154)形式进行积分来计算。对于[凯勒流形](@entry_id:161192)，一个自然的选择是与凯勒度量 $\omega$ 相关的陈联络 (Chern connection)。

通过该理论可以证明一个至关重要的结果：[里奇形式](@entry_id:183612) $\mathrm{Ric}(\omega)$ 的[德拉姆上同调](@entry_id:158673)类 (de Rham cohomology class) 精确地代表了 $2\pi$ 倍的[第一陈类](@entry_id:201400)（将其视为一个实[上同调类](@entry_id:263961)）。即：
$$
[\mathrm{Ric}(\omega)] = 2\pi c_1(M) \in H^2(M, \mathbb{R})
$$
这个等式可以通过典范丛 $K_M = \Lambda^{n,0}T^*M$ 来理解。典范丛的曲率 $F_{K_M}$ 与[里奇形式](@entry_id:183612)有直接关系 $\mathrm{Ric}(\omega) = -\sqrt{-1} F_{K_M}$。另一方面，根据陈-韦伊理论的定义，$c_1(K_M) = [\frac{\sqrt{-1}}{2\pi} F_{K_M}]$。由于 $c_1(M) = -c_1(K_M)$，我们便推导出了上述关系。[@problem_id:3066682] [@problem_id:3066655]

这个等式是[卡拉比猜想](@entry_id:180885)的出发点。它告诉我们，尽管[里奇形式](@entry_id:183612) $\mathrm{Ric}(\omega)$ 本身依赖于我们选择的凯勒度量 $\omega$，但它的上同调类 $[ \mathrm{Ric}(\omega) ]$ 却是一个不依赖于度量选择的[拓扑不变量](@entry_id:138526)，完全由 $M$ 的复结构决定。这立刻引出了一个自然而深刻的问题：我们能否反过来，在给定的[上同调类](@entry_id:263961)中，指定一个精确的[里奇形式](@entry_id:183612)，并找到一个对应的凯勒度量呢？

### [卡拉比猜想](@entry_id:180885)：指定里奇曲率

这个问题由 Eugenio Calabi 在1954年和1957年精确地表述出来。首先，我们需要明确在哪个范围内寻找度量。在[凯勒几何](@entry_id:160314)中，我们通常固定一个**凯勒类 (Kähler class)**，即一个[德拉姆上同调](@entry_id:158673)类 $[\omega] \in H^2(M, \mathbb{R})$，该类中包含至少一个凯勒形式。根据 $\partial\bar{\partial}$-引理，同一个凯勒类中的任意两个凯勒形式 $\omega$ 和 $\omega'$ 都可以通过一个光滑的实值函数 $\varphi$（称为[凯勒势](@entry_id:154750)的差）联系起来：
$$
\omega' = \omega + \sqrt{-1} \partial\bar{\partial} \varphi
$$
这里我们要求 $\omega'$ 仍然是正定的，这对 $\varphi$ 施加了一个[二阶偏微分方程](@entry_id:175326)的约束。

现在我们可以陈述**[卡拉比猜想](@entry_id:180885) (Calabi Conjecture)**：

> 设 $(M, \omega)$ 是一个紧[凯勒流形](@entry_id:161192)。对于代表上同调类 $2\pi c_1(M)$ 的任意一个实、闭 $(1,1)$-形式 $\tilde{\rho}$，在凯勒类 $[\omega]$ 中存在一个**唯一**的凯勒形式 $\omega_\varphi = \omega + \sqrt{-1}\partial\bar{\partial}\varphi$，使得其[里奇形式](@entry_id:183612)恰好是 $\tilde{\rho}$，即 $\mathrm{Ric}(\omega_\varphi) = \tilde{\rho}$。[@problem_id:3066655]

这个猜想极为强大。它断言，一旦一个凯勒类被固定，那么该类中度量的[里奇曲率](@entry_id:162038)的“自由度”就只剩下上同调所允许的部分。换言之，里奇曲率的几何形态可以被精确地“雕刻”，只要最终的形态在拓扑上是正确的。Calabi 本人证明了如果解存在，那么它是唯一的。猜想的真正难点在于证明解的存在性。

### 复[蒙日-安培方程](@entry_id:268604)：分析表述

为了证明存在性，必须将这个几何问题转化为一个可解的[偏微分方程](@entry_id:141332)（PDE）。这一转化的核心是理解当[凯勒势](@entry_id:154750)变化时，[里奇形式](@entry_id:183612)如何变化。对于两个在同一凯勒类中的度量 $\omega_\varphi = \omega + \sqrt{-1}\partial\bar{\partial}\varphi$ 和 $\omega$，它们的[里奇形式](@entry_id:183612)之差由以下公式给出：
$$
\mathrm{Ric}(\omega_\varphi) - \mathrm{Ric}(\omega) = -\sqrt{-1}\partial\bar{\partial} \log \left( \frac{\det(g_\varphi)}{\det(g)} \right) = -\sqrt{-1}\partial\bar{\partial} \log \left( \frac{\omega_\varphi^n}{\omega^n} \right)
$$
其中 $\omega^n = \omega \wedge \dots \wedge \omega$ ($n$次) 是与度量 $\omega$ 相关的体积形式。[@problem_id:3034357]

[卡拉比猜想](@entry_id:180885)的目标是令 $\mathrm{Ric}(\omega_\varphi) = \tilde{\rho}$。因为 $\tilde{\rho}$ 和 $\mathrm{Ric}(\omega)$ 在同一个[上同调类](@entry_id:263961) $2\pi c_1(M)$ 中，它们的差是一个 $d$-恰当的 $(1,1)$-形式。更进一步，在[凯勒流形](@entry_id:161192)上，它可以被写成 $\sqrt{-1}\partial\bar{\partial}F$ 的形式，对于某个光滑实函数 $F$。于是，$\tilde{\rho} = \mathrm{Ric}(\omega) + \sqrt{-1}\partial\bar{\partial}F$。将此代入上述关系式，我们得到：
$$
-\sqrt{-1}\partial\bar{\partial}F = \sqrt{-1}\partial\bar{\partial} \log \left( \frac{\omega_\varphi^n}{\omega^n} \right)
$$
这意味着 $\log(\omega_\varphi^n / \omega^n) + F$ 是一个多调和函数（pluriharmonic function）。在[紧流形](@entry_id:158804)上，唯一的多[调和函数](@entry_id:746864)是常数。因此，$\log(\omega_\varphi^n / \omega^n) = -F + c$，其中 $c$ 是一个常数。两边取指数，我们便得到了关于未知势函数 $\varphi$ 的方程：
$$
(\omega + \sqrt{-1}\partial\bar{\partial}\varphi)^n = e^{-F+c} \omega^n
$$
这是一个高度[非线性](@entry_id:637147)的二阶[椭圆偏微分方程](@entry_id:178258)，被称为**复[蒙日-安培方程](@entry_id:268604) (complex Monge-Ampère equation)**。[@problem_id:3066699]

方程右侧的函数 $e^{-F+c}$ 并非任意。由于 $\omega_\varphi$ 和 $\omega$ 在同一个上同调类中，它们的总体积必须相等。通过在整个[流形](@entry_id:153038) $M$ 上对方程两边进行积分，并利用[斯托克斯定理](@entry_id:264534)，我们得到 $\int_M \omega_\varphi^n = \int_M \omega^n$。这导出一个必要的[相容性条件](@entry_id:637057)或**[归一化条件](@entry_id:156486)**：
$$
\int_M e^{-F+c} \omega^n = \int_M \omega^n
$$
这个条件唯一地确定了常数 $c$。因此，[卡拉比猜想](@entry_id:180885)的证明归结为求解一个具有特[定积分](@entry_id:147612)约束的复[蒙日-安培方程](@entry_id:268604)。[@problem_id:3066699] [@problem_id:3034357]

### [丘成桐定理](@entry_id:190158)：[连续性方法](@entry_id:195593)

1976年，丘成桐通过发展强大的[非线性](@entry_id:637147)分析工具，成功证明了这个方程解的存在性，从而证实了[卡拉比猜想](@entry_id:180885)。他的证明核心是**[连续性方法](@entry_id:195593) (continuity method)**。

其策略不是直接攻击目标方程，而是构造一个从简单问题到目标问题的[连续路径](@entry_id:187361)。考虑一个参数 $t \in [0,1]$，我们研究如下的方程族：
$$
(\omega + \sqrt{-1}\partial\bar{\partial}\varphi_t)^n = e^{-tF + c_t} \omega^n
$$
其中函数 $F$ 来自我们想要设定的[里奇曲率](@entry_id:162038)，而常数 $c_t$ 在每一步都被选择以满足积分[归一化条件](@entry_id:156486) $\int_M e^{-tF+c_t}\omega^n = \int_M \omega^n$。[@problem_id:3066695]

我们的目标是证明对于 $t=1$ 时方程有解。为此，我们定义一个集合 $\mathcal{T} \subseteq [0,1]$，其中包含所有使得方程有光滑解的参数 $t$。[连续性方法](@entry_id:195593)的关键在于证明 $\mathcal{T}$ 同时是开集和[闭集](@entry_id:136446)。由于 $[0,1]$ 是连通的，并且 $\mathcal{T}$ 非空，这将意味着 $\mathcal{T}$ 必须是整个区间 $[0,1]$。

1.  **非空性 (Non-emptiness)**：当 $t=0$ 时，方程变为 $(\omega + \sqrt{-1}\partial\bar{\partial}\varphi_0)^n = e^{c_0}\omega^n$。积分条件给出 $c_0=0$，方程简化为 $(\omega + \sqrt{-1}\partial\bar{\partial}\varphi_0)^n = \omega^n$。一个平凡的解是 $\varphi_0 = 0$。因此，$0 \in \mathcal{T}$，集合非空。[@problem_id:3066695]

2.  **开放性 (Openness)**：这是证明中相对“容易”的部分。假设对于某个 $t_0 \in \mathcal{T}$，我们有一个解 $\varphi_{t_0}$。我们希望证明在 $t_0$ 的一个小邻域内也存在解。这可以通过在[巴拿赫空间](@entry_id:143833)上应用**[反函数定理](@entry_id:275014) (Inverse Function Theorem)** 来实现。关键在于，复蒙日-安培算子的线性化是一个二阶[椭圆算子](@entry_id:181616)——与度量 $\omega_{\varphi_{t_0}}$ 相关的[拉普拉斯算子](@entry_id:146319) $\Delta_{\varphi_{t_0}}$。在[紧流形](@entry_id:158804)上，这个算子在零平均函数的空间上是可逆的。[反函数定理](@entry_id:275014)保证了在 $t_0$ 附近，解是连续依赖于参数 $t$ 的，从而证明了 $\mathcal{T}$ 的开放性。[@problem_id:3066695]

3.  **封闭性 (Closedness)**：这是证明的核心，也是丘成桐的主要贡献所在。我们需要证明，如果一列参数 $t_j \in \mathcal{T}$ 收敛到 $t_\infty$，那么 $t_\infty$ 也属于 $\mathcal{T}$。这需要证明对应的解序列 $\{\varphi_{t_j}\}$ 有一个收敛的子列，其极限是 $t_\infty$ 时刻的方程的解。根据[阿尔泽拉-阿斯科利定理](@entry_id:154538)，这要求我们能建立关于解 $\varphi_t$ 及其各阶导数的、不依赖于 $t$ 的**一致[先验估计](@entry_id:186098) (uniform a priori estimates)**。[@problem_id:3066695]

丘成桐建立的估计链条是[几何分析](@entry_id:157700)中的一座丰碑，其大致顺序如下：[@problem_id:3066673]
    - **$C^0$ 估计**：首先，利用[莫泽迭代](@entry_id:186627) (Moser iteration) 和[索博列夫不等式](@entry_id:157975)，建立解的零阶范数（即最大值）的一致界 $\|\varphi_t\|_{L^\infty} \le C$。这是至关重要的第一步。
    - **$C^2$ 估计**：其次，也是最困难的一步，是建立[二阶导数](@entry_id:144508)的一致界。这等价于证明新度量 $\omega_t$ 与背景度量 $\omega$ 是等价的。丘成桐通过对一个精心构造的辅助函数（例如 $Q = \log(\operatorname{tr}_\omega(\omega_t)) - A\varphi_t$）应用极大值原理，成功地控制了拉普拉斯算子 $\Delta_\omega \varphi_t$，从而获得了 $C^2$ 估计。
    - **高阶估计**：一旦获得了一致的 $C^2$ 估计，方程就变得一致椭圆。利用复蒙日-安培算子的[凹性](@entry_id:139843)，可以应用埃文斯-克雷洛夫理论 (Evans-Krylov theory) 得到 $C^{2,\alpha}$ 估计。之后，通过标准的绍德（Schauder）理论和自举法（bootstrapping），可以依次获得所有更高阶导数的一致界。

这一系列的[先验估计](@entry_id:186098)保证了解序列的紧性，从而证明了 $\mathcal{T}$ 的封闭性。至此，[卡拉比猜想](@entry_id:180885)的存在性部分得以证明。

### 应用与推论：[凯勒-爱因斯坦度量](@entry_id:270601)

[丘成桐定理](@entry_id:190158)最辉煌的应用之一是解决了**[凯勒-爱因斯坦度量](@entry_id:270601) (Kähler-Einstein metrics)** 的存在性问题。一个凯勒度量 $\omega$ 被称为[凯勒-爱因斯坦度量](@entry_id:270601)，如果其[里奇形式](@entry_id:183612)与自身成正比：
$$
\mathrm{Ric}(\omega) = \lambda \omega
$$
对于某个实常数 $\lambda$。[@problem_id:3066658]

对上式两边取上同调类，并结合关系 $[\mathrm{Ric}(\omega)] = 2\pi c_1(M)$，我们立即得到一个必要条件：
$$
2\pi c_1(M) = \lambda [\omega]
$$
这个条件表明，一个紧凯勒流形若要拥有[凯勒-爱因斯坦度量](@entry_id:270601)，其[第一陈类](@entry_id:201400)必须与凯勒类成比例。常数 $\lambda$ 的符号因此由[第一陈类](@entry_id:201400)的“符号”决定。[@problem_id:3066658] [丘成桐定理](@entry_id:190158)对于不同符号的 $\lambda$ 有着不同的影响：

- **情形一：$c_1(M) = 0$ (在实[上同调](@entry_id:160558)中)**
这对应于 $\lambda=0$。此时，我们寻找的是[里奇平坦](@entry_id:159097)（Ricci-flat）的度量。[卡拉比猜想](@entry_id:180885)断言，对于代表 $2\pi c_1(M) = 0$ 的形式 $\tilde{\rho}=0$，存在一个凯勒度量 $\omega_\varphi$ 使得 $\mathrm{Ric}(\omega_\varphi)=0$。因此，[丘成桐定理](@entry_id:190158)直接保证了在任意给定的凯勒类中，都存在一个唯一的[里奇平坦凯勒度量](@entry_id:637038)。具有这种度量的[流形](@entry_id:153038)被称为**卡拉比-丘流形 (Calabi-Yau manifolds)**，它们在数学和[弦理论](@entry_id:145688)中都具有极其重要的地位。[@problem_id:3066671]

- **情形二：$c_1(M)  0$**
这表示 $-c_1(M)$ 是一个正类（即可以由某个凯勒形式代表），对应于 $\lambda  0$。在这种情况下，丘成桐（以及Aubin）的工作同样表明，存在一个唯一的[凯勒-爱因斯坦度量](@entry_id:270601)。证明中的[先验估计](@entry_id:186098)在这种情况下甚至比 $\lambda=0$ 的情况更容易获得。[@problem_id:3066665]

- **情形三：$c_1(M) > 0$**
这类[流形](@entry_id:153038)被称为**[法诺流形](@entry_id:190177) (Fano manifolds)**，对应于 $\lambda > 0$。这是最微妙的情况。丘成桐的分析方法在这里遇到了障碍，[先验估计](@entry_id:186098)不再直接成立。事实证明，此种情况下[凯勒-爱因斯坦度量](@entry_id:270601)的存在性有额外的几何阻碍。例如，松岛（Matsushima）定理指出，如果存在这样的度量，[流形](@entry_id:153038)的全纯[自同构群](@entry_id:139672)的[李代数](@entry_id:137954)必须是约化的。更深刻的阻碍是**“K-稳定性” (K-stability)** 的概念。由丘-田-唐纳森（Yau-Tian-Donaldson）猜想（现已基本被证明为定理）所阐明，一个[法诺流形](@entry_id:190177)上[凯勒-爱因斯坦度量](@entry_id:270601)的存在性等价于该[流形](@entry_id:153038)是 K-稳定的。[@problem_id:3066665]

综上所述，[卡拉比猜想](@entry_id:180885)和[丘成桐定理](@entry_id:190158)不仅解决了复微分几何中一个核心的[偏微分方程](@entry_id:141332)，而且为[代数几何](@entry_id:156300)中的[典范度量](@entry_id:266957)和模空间理论提供了坚实的分析基础，并深刻地影响了理论物理学的发展。