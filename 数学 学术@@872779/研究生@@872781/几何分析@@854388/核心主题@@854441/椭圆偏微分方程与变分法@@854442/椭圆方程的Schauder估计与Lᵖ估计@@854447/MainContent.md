## 引言
[椭圆偏微分方程](@entry_id:178258)是数学物理和[几何分析](@entry_id:157700)的基石，描述了从静电场[分布](@entry_id:182848)到空间度量等诸多平衡态现象。然而，仅仅证明一个解的存在性往往是不够的，我们更关心解的“质量”——它有多光滑？一个根本性的问题是：方程解的[光滑性](@entry_id:634843)在多大程度上继承了方程本身（系数、[源项](@entry_id:269111)）和定义域几何的光滑性？这便是[正则性理论](@entry_id:194071)的核心议题，它构成了从[弱解](@entry_id:161732)的抽象世界通向具有物理和几何意义的经典解的桥梁。本文旨在系统性地回答这一问题，为读者揭示[椭圆方程](@entry_id:169190)[正则性理论](@entry_id:194071)的两大支柱：[Schauder估计](@entry_id:196811)和$L^p$估计。

为实现这一目标，本文将分为三个紧密相连的部分。在“原理与机制”一章中，我们将深入剖析这两类估计的内在逻辑。我们将从区[分散度](@entry_id:163107)与非[散度结构](@entry_id:748609)出发，揭示De Giorgi-Nash-Moser和Krylov-Safonov理论在处理极弱系数时的不同策略，并进而阐述在系数更光滑时，[Schauder理论](@entry_id:185158)的“冻结系数法”和Calderón-Zygmund理论对VMO条件的依赖性如何运作。随后，在“应用与跨学科联系”一章中，我们将展示这些看似抽象的分析工具如何在[连续介质力学](@entry_id:155125)、几何分析和[随机控制](@entry_id:170804)等前沿领域中发挥关键作用，例如用于证明[Ricci流](@entry_id:145202)的光滑性或解决[Calabi猜想](@entry_id:180885)。最后，“动手实践”部分将通过一系列精选问题，引导读者应用所学理论，加深对正则性估计中微妙之处的理解，例如斜导数问题和估计对区域扰动的稳定性。通过这一结构化的学习路径，读者将全面掌握[椭圆方程](@entry_id:169190)[正则性理论](@entry_id:194071)的核心思想及其强大应用。

## 原理与机制

在本章中，我们将深入探讨二阶[椭圆偏微分方程](@entry_id:178258)解的[正则性理论](@entry_id:194071)的核心原理与机制。[正则性理论](@entry_id:194071)旨在回答一个根本问题：方程的解在多大程度上继承了方程系数、源项以及定义域几何的光滑性？我们将系统地剖析两类主要的正则性估计——Schauder 估计（在 Hölder 空间 $C^{k,\alpha}$ 中）和 $L^p$ 估计（在 Sobolev 空间 $W^{k,p}$ 中），并揭示这些估计如何深刻地依赖于方程的[代数结构](@entry_id:137052)。

### 结构的二分性：[散度形式](@entry_id:748608)与非[散度形式](@entry_id:748608)

二阶线性[椭圆算子](@entry_id:181616)通常呈现为两种主要形式，这种结构上的差异是[正则性理论](@entry_id:194071)分野的根源。设 $A(x) = (a^{ij}(x))$ 是一个对称且一致椭圆的[系数矩阵](@entry_id:151473)，即存在常数 $0  \lambda \le \Lambda  \infty$ 使得 $\lambda |\xi|^2 \le a^{ij}(x)\xi_i \xi_j \le \Lambda |\xi|^2$。

第一种是 **[散度形式](@entry_id:748608)（divergence form）** 算子：
$$
L_{\text{div}} u := -\partial_i (a^{ij}(x) \partial_j u)
$$
这种形式天然地与物理学中的守恒律联系在一起，其数学结构与变分原理紧密相关。因此，其解的自然框架是 **弱解（weak solution）**。一个函数 $u \in H^1_{\text{loc}}(\Omega)$ 是方程 $L_{\text{div}} u = f$ 的[弱解](@entry_id:161732)，如果对于所有[检验函数](@entry_id:166589) $\varphi \in C_c^\infty(\Omega)$，它都满足积分恒等式：
$$
\int_{\Omega} a^{ij}(x) \partial_j u \, \partial_i \varphi \, dx = \int_{\Omega} f \varphi \, dx
$$
这种定义仅要求 $u$ 的一阶[弱导数](@entry_id:189356)存在，为处理系数不光滑的情形提供了可能。

第二种是 **非[散度形式](@entry_id:748608)（nondivergence form）** 算子：
$$
L_{\text{nondiv}} u := a^{ij}(x) \partial_{ij} u
$$
展开[散度形式](@entry_id:748608)算子，我们得到 $L_{\text{div}} u = -a^{ij}\partial_{ij}u - (\partial_i a^{ij})\partial_j u$。可见，只有当系数 $a^{ij}$ 是常数时，两种形式才一致。非[散度形式](@entry_id:748608)算子直接作用于函数的[二阶导数](@entry_id:144508)，因此其解的经典概念是 **古典解（classical solution）**，即要求 $u \in C^2(\Omega)$ 并逐点满足方程。当系数或解不具备足够[光滑性](@entry_id:634843)时，这一概念被推广为 **黏性解（viscosity solution）**。

这两种形式的本质区别——一个是基于积分（弱）形式，另一个是基于逐点（强）形式——导致了截然不同的[正则性理论](@entry_id:194071)路径和对系数光滑性的不同要求。[@problem_id:3033300]

### 最弱系数光滑性下的正则性：$L^\infty$ 情形

一个惊人的事实是，即便系数 $a^{ij}(x)$ 仅仅是可测有界的（即 $a^{ij} \in L^\infty(\Omega)$），并且满足[一致椭圆性](@entry_id:194714)，我们仍然可以获得解的 Hölder 连续性。然而，实现这一点的机制在[散度形式](@entry_id:748608)和非[散度形式](@entry_id:748608)下完全不同。

#### [散度形式](@entry_id:748608)方程：De Giorgi-Nash-Moser 理论

对于[散度形式](@entry_id:748608)方程 $L_{\text{div}} u = 0$，De Giorgi、Nash 和 Moser 在 20 世纪 50 年代独立证明了一个里程碑式的定理：任何 $H^1_{\text{loc}}$ [弱解](@entry_id:161732)都是局部 Hölder 连续的（$u \in C^\alpha_{\text{loc}}(\Omega)$），并且非负解满足 **Harnack 不等式**。[@problem_id:3034795] 这一理论的证明完全不依赖于系数的连续性。其核心工具是[变分方法](@entry_id:163656)，主要包括：

1.  **Caccioppoli 不等式**：这是一个能量估计，它表明解在一个球内的梯度 $L^2$ 范数可以被解在该球内的 $L^2$ 范数所控制。这是通过在[弱形式](@entry_id:142897)中巧妙地选取检验函数（例如 $\varphi = u \eta^2$，其中 $\eta$ 是一个截断函数）并使用[分部积分](@entry_id:136350)得到的。
2.  **Moser 迭代**：通过 Caccioppoli 不等式和 Sobolev [嵌入定理](@entry_id:150872)，可以建立一个迭代过程，逐步提升解的可积性，最终证明解是局部有界的。
3.  **[振荡](@entry_id:267781)衰减**：证明解在半径不断缩小的球上的[振荡](@entry_id:267781)（[最大值与最小值](@entry_id:145933)之差）以[幂律](@entry_id:143404)形式衰减，这直接导出了 Hölder 连续性。

DGNM 理论的强大之处在于其普适性，它仅依赖于方程的积分结构和[一致椭圆性](@entry_id:194714)。

#### 非[散度形式](@entry_id:748608)方程：[Krylov-Safonov 理论](@entry_id:201750)

对于非[散度形式](@entry_id:748608)方程 $L_{\text{nondiv}} u = 0$，由于没有变分结构，DGNM 的方法完全失效。直到 20 世纪 70 年代末，Krylov 和 Safonov 才为这类方程建立了对应的理论。他们证明了，在同样的 $a^{ij} \in L^\infty$ 和[一致椭圆性](@entry_id:194714)假设下，黏性解也是局部 Hölder 连续的，并且满足 Harnack 不等式。[@problem_id:3034795] 其证明工具与 DGNM 理论迥然不同，主要包括：

1.  **Aleksandrov–Bakelman–Pucci (ABP) 极大值原理**：这是一个非[散度形式](@entry_id:748608)方程理论的基石，它提供了点态梯度的一个估计，将解的[上确界](@entry_id:140512)与[源项](@entry_id:269111)的 $L^n$ 范数联系起来。
2.  **Krylov–Safonov [覆盖引理](@entry_id:139920)**：这是一个精妙的[测度论](@entry_id:139744)工具，它断言一个集合如果处处具有“足够大的测度”，那么它可以用一系列球进行覆盖，并且这些球的中心都在该集合内部。

通过结合 ABP 原理和[覆盖引理](@entry_id:139920)，Krylov 和 Safonov 得以证明一个关键的[振荡](@entry_id:267781)衰减引理，从而获得 Hölder 连续性和 Harnack 不等式。

#### 低阶项的角色：标度不变性与小性条件

现在考虑包含低阶项的更一般的算子 $L u = a^{ij}D_{ij}u + b^i D_i u + c u$。在 $a^{ij} \in L^\infty$ 的框架下，低阶项的处理非常微妙。让我们通过一个标度变换来理解其影响。假设 $u$ 在一个以 $x_0$ 为中心、半径为 $r$ 的球上满足 $Lu=f$。定义 rescaled 函数 $u_r(y) = u(x_0+ry)$，它在单位球 $B_1$ 上满足一个新的方程：
$$
\tilde{a}^{ij}(y) D_{ij}u_r(y) + (r \tilde{b}^i(y)) D_i u_r(y) + (r^2 \tilde{c}(y)) u_r(y) = r^2 \tilde{f}(y)
$$
其中 $\tilde{a}^{ij}(y) = a^{ij}(x_0+ry)$ 等。这个变换揭示了，当尺度 $r \to 0$ 时，一阶（漂移）项的系数等效地乘以 $r$，而零阶（位势）项的系数等效地乘以 $r^2$。这意味着在足够小的尺度上，低阶项的影响是微扰性的。

为了使 [Krylov-Safonov 理论](@entry_id:201750)（或 DGNM 理论的边界版本）得以推广，我们需要将这种直觉严格化。这要求对低阶项施加一个 **尺度依赖的小性条件（scale-dependent smallness condition）**。具体来说，为了获得边界 Hölder 连续性，我们需要存在一个 $\varepsilon_0  0$ 和一个半径 $r_0  0$，使得在任何以[边界点](@entry_id:176493)为中心、半径为 $r \le r_0$ 的半球上，以下条件成立：
$$
r\|b\|_{L^\infty(B_r^+)} + r^2\|c\|_{L^\infty(B_r^+)} \le \varepsilon_0
$$
如果这个条件满足，那么低阶项就可以被视为一个小的扰动，从而可以得到与没有低阶项时类似的 Hölder 估计，并且估计中的常数不依赖于 $\|b\|_{L^\infty}$ 和 $\|c\|_{L^\infty}$ 的全局范数。[@problem_id:3026081] 如果没有这个小性条件，大的漂移项可能会破坏解的局部正则性。

### 高阶正则性 I：经典 Schauder 理论 ($C^{k,\alpha}$ 估计)

当方程的系数和数据具有比 $L^\infty$ 更高的光滑性，例如 Hölder 连续性时，我们期望解也具有更高的光滑性。这就是经典 Schauder 理论的范畴，其基本原则是：**解比数据光滑两个导数，并且其最高阶导数继承了数据的 Hölder 指数**。

#### 非[散度形式](@entry_id:748608)方程的内部正则性

Schauder 理论在非[散度形式](@entry_id:748608)下表现得最为自然。核心的 **内部 Schauder 估计** 表明：如果 $a^{ij}, f \in C^\alpha(\Omega)$，那么方程 $a^{ij}(x)\partial_{ij}u = f(x)$ 的任何 $C^2$ 解 $u$ 实际上都属于 $C^{2,\alpha}_{\text{loc}}(\Omega)$。[@problem_id:3033300] 其对应的[先验估计](@entry_id:186098)形式为，对任意 $\Omega' \Subset \Omega$：
$$
\|u\|_{C^{2,\alpha}(\Omega')} \le C \left( \|f\|_{C^{\alpha}(\Omega)} + \|u\|_{L^\infty(\Omega)} \right)
$$
常数 $C$ 依赖于 $n, \alpha, \lambda, \Lambda$，以及 $a^{ij}$ 的 $C^\alpha$ 范数和区域 $\Omega', \Omega$。

这个理论的证明机制是 **冻结系数法（method of freezing coefficients）**。其思想是在一个点 $x_0$ 附近，将方程改写为：
$$
a^{ij}(x_0)\partial_{ij}u = f - (a^{ij}(x) - a^{ij}(x_0))\partial_{ij}u
$$
左边是一个[常系数](@entry_id:269842)算子，其[正则性理论](@entry_id:194071)（基于对[泊松方程](@entry_id:143763)解的分析）是已知的。右边的第二项是扰动项。由于 $a^{ij}$ 是 $C^\alpha$ 连续的，当 $x$ 靠近 $x_0$ 时，差值 $a^{ij}(x) - a^{ij}(x_0)$ 会变得很小。这种小性使得我们可以通过一个扰动论证或者紧性论证，将[常系数](@entry_id:269842)算子的正则性“传递”给变系数算子。这个过程可以通过 **Campanato 空间** 的语言来精确表述，该空间刻画了函数在小球上的[振荡](@entry_id:267781)行为，并且与 Hölder 空间等价。

#### 边界正则性：[光滑性](@entry_id:634843)的传递

Schauder 理论可以优雅地延伸到区域的边界，前提是边界本身足够光滑。**边界 Schauder 估计** 的一般原则是，解的正则性是由方程中所有元素——系数、源项、边界数据和边界几何——中最不光滑的一环决定的。

考虑一个 [Dirichlet 问题](@entry_id:274408)：
$$
\begin{cases}
Lu = a^{ij}D_{ij}u + b^i D_i u + c u = f  \text{ in } \Omega, \\
u = g  \text{ on } \partial\Omega.
\end{cases}
$$
为了得到一个直到边界都 $C^{k+2,\alpha}(\overline{\Omega})$ 光滑的解，我们需要一套匹配的[光滑性](@entry_id:634843)假设：
- 区域边界 $\partial\Omega$ 是 $C^{k+2,\alpha}$ 类。
- 系数 $a^{ij}, b^i, c$ 属于 $C^{k,\alpha}(\overline{\Omega})$。
- 源项 $f$ 属于 $C^{k,\alpha}(\overline{\Omega})$。
- 边界数据 $g$ 属于 $C^{k+2,\alpha}(\partial\Omega)$。

在这些条件下，解 $u$ 确实属于 $C^{k+2,\alpha}(\overline{\Omega})$，并满足[先验估计](@entry_id:186098)：
$$
\|u\|_{C^{k+2,\alpha}(\overline{\Omega})} \le C \left( \|f\|_{C^{k,\alpha}(\overline{\Omega})} + \|g\|_{C^{k+2,\alpha}(\partial\Omega)} \right)
$$
(这里我们假设可以通过极大值原理控制 $\|u\|_{C^0}$ 项)。[@problem_id:3026141]

这个结果的证明依赖于 **边界展平（flattening the boundary）** 技术。在任意边界点附近，可以通过一个 $C^{k+2,\alpha}$ 的坐标变换将弯曲的边界 $\partial\Omega$ 拉直成一个超平面。在这个新的[坐标系](@entry_id:156346)下，方程的结构保持不变，但系数会因为坐标[变换的导数](@entry_id:164838)而改变。由于变换是 $C^{k+2,\alpha}$ 的，新系数的正则性足以应用一个[半空间](@entry_id:634770)版本的内部 Schauder 估计，从而得到边界正则性。

例如，对于 $C^{1,\alpha}(\overline{\Omega})$ 正则性，我们需要 $\partial\Omega \in C^{1,\alpha}$, $a^{ij} \in C^{0,\alpha}(\overline{\Omega})$, $f \in C^{0,\alpha}(\overline{\Omega})$ 和 $g \in C^{1,\alpha}(\partial\Omega)$。[@problem_id:3026071]

#### 低阶项的角色：插值与吸收

与 $L^\infty$ 情形形成鲜明对比的是，在 Schauder 理论的框架下，处理低阶项 **不需要任何小性条件**。我们可以通过一个优雅的 **插值与吸收（interpolation and absorption）** 论证来处理它们。

在证明[先验估计](@entry_id:186098) $\|u\|_{C^{2,\alpha}} \le C(\|f\|_{C^\alpha} + \dots)$ 的过程中，我们会遇到形如 $\|b^i D_i u\|_{C^\alpha}$ 和 $\|c u\|_{C^\alpha}$ 的项。使用 Hölder 空间的乘法法则和[插值不等式](@entry_id:196801)，对任意 $\varepsilon  0$，我们有：
$$
\|b^i D_i u\|_{C^\alpha} \le K \|b^i\|_{C^\alpha} \|D_i u\|_{C^\alpha} \le K \|b^i\|_{C^\alpha} (\varepsilon \|u\|_{C^{2,\alpha}} + C_\varepsilon \|u\|_{C^0})
$$
将此式代入主估计中，我们得到：
$$
\|u\|_{C^{2,\alpha}} \le \dots + K' \varepsilon \|b^i\|_{C^\alpha} \|u\|_{C^{2,\alpha}} + \dots
$$
只要我们预先选择 $\varepsilon$ 足够小（例如，使得 $K' \varepsilon \|b^i\|_{C^\alpha}  1/2$），我们就可以将含有 $\|u\|_{C^{2,\alpha}}$ 的项从右边移到左边并 **吸收** 它。最终的常数 $C$ 会依赖于 $\|b^i\|_{C^\alpha}$ 和 $\|c\|_{C^\alpha}$ 的范数，但不需要它们本身很小。这个强大的技术表明，在光滑系数的框架下，低阶项不会降低解的正则性阶数。[@problem_id:3026081]

#### [散度形式](@entry_id:748608)方程的局限性

如果我们将 Schauder 理论直接应用于[散度形式](@entry_id:748608)方程 $-\partial_i(a^{ij}\partial_j u)=f$，其中 $a^{ij}, f \in C^\alpha$，我们通常 **无法** 得到 $u \in C^{2,\alpha}_{\text{loc}}$ 的结论。原因在于其展开形式：
$$
-a^{ij}\partial_{ij}u = f + (\partial_i a^{ij})\partial_j u
$$
要应用非[散度形式](@entry_id:748608)的 Schauder 理论，我们需要右端项是 $C^\alpha$ 的。然而，$\partial_j u$ 最多只能先验地知道是 $C^{1-\text{something}}$，而 $\partial_i a^{ij}$ 这一项甚至可能不存在，因为它要求 $a^{ij}$ 是 $C^1$ 的。事实上，正确的结论是，在这种情况下，解 $u$ 通常只属于 $C^{1,\alpha}_{\text{loc}}(\Omega)$。要获得 $C^{2,\alpha}$ 正则性，我们必须要求系数 $a^{ij}$ 至少是 $C^{1,\alpha}$ 的。[@problem_id:3033300] 这再次凸显了方程结构对正则性结果的决定性影响。

### 高阶正则性 II：Calderón-Zygmund 理论 ($W^{k,p}$ 估计)

Calderón-Zygmund 理论是 Schauder 理论在 $L^p$ 空间中的对应物。其核心思想是，如果[源项](@entry_id:269111)在 $L^p$ 中，那么解的[二阶导数](@entry_id:144508)也在 $L^p$ 中，即 $u \in W^{2,p}$。

#### 系数正则性的关键作用：VMO 条件

$L^p$ 理论对系数[光滑性](@entry_id:634843)的要求，再次揭示了散度与非[散度形式](@entry_id:748608)的深刻差异。

对于 **[散度形式](@entry_id:748608)方程** $-\partial_i(a^{ij}\partial_j u) = \text{div} F$（其中 $F \in L^p$），$L^p$ 理论非常自然。然而，仅有 $a^{ij} \in L^\infty$ 的假设是不够的。Meyers 的工作表明，在这种情况下，$W^{1,p}$ 估计（即 $\|\nabla u\|_{L^p} \le C \|F\|_{L^p}$）仅对某个包含 2 的小区间 $p \in (p_-, p_+)$ 成立。[@problem_id:3033297] 要想让估计对所有 $p \in (1, \infty)$ 都成立，我们需要对系数施加一个比 $L^\infty$ 强但比连续弱的条件。

对于 **非[散度形式](@entry_id:748608)方程** $a^{ij}\partial_{ij}u = f$，情况更为微妙。仅有 $a^{ij} \in L^\infty$ 甚至不足以保证 $W^{2,p}$ 估计对任何 $p \neq 2$ 成立。

令人惊讶的是，在这两种情况下，一个统一的、近乎最优的条件出现了：[系数矩阵](@entry_id:151473) $A(x)$ 的分量属于 **VMO 空间（Vanishing Mean Oscillation）**。一个函数属于 VMO，粗略地说，意味着它在任意小尺度上的平均[振荡](@entry_id:267781)都趋于零。这个条件包含了所有[一致连续函数](@entry_id:159231)，但比 Hölder 连续要弱得多。

- **VMO 与 $W^{2,p}$ 估计**：一个里程碑式的结果（由 Chiarenza, Frasca, Longo 得到）表明，对于非[散度形式](@entry_id:748608)方程，当 $a^{ij} \in \text{VMO}$ 时，$f \in L^p$ 蕴含 $u \in W^{2,p}_{\text{loc}}$ 对所有 $p \in (1, \infty)$ 成立。[@problem_id:3033300] 对于[散度形式](@entry_id:748608)方程，VMO 系数也足以保证对所有 $p \in (1,\infty)$ 成立的 $W^{1,p}$ 估计。[@problem_id:3033297]

#### 内部估计与边界估计

与 Schauder 理论一样，$L^p$ 估计也分为内部估计和边界估计。**内部估计** 是一个纯粹的局部性质。其证明通常通过将问题局部化到一个球上，因此估计中的常数仅依赖于方程的局部参数（如椭圆性常数、系数的 VMO 模），而与定义域 $\Omega$ 的[全局几何](@entry_id:197506)形状或边界[光滑性](@entry_id:634843)完全无关。[@problem_id:3033297]

相反，**边界估计**（或全局估计）则强烈地依赖于边界 $\partial\Omega$ 的[光滑性](@entry_id:634843)。例如，要在一个有界域 $\Omega$ 上为 [Dirichlet 问题](@entry_id:274408)建立全局 $W^{1,p}$ 估计，仅仅 Lipschitz 边界是不够的，因为在“角”附近解的梯度可能会出现奇性。通常需要更强的边界正则性，例如 $C^1$ 或 $C^{1,\alpha}$。在系数和边界都足够光滑的条件下（例如 $a^{ij} \in C^{\alpha}(\overline{\Omega})$ 且 $\partial\Omega \in C^{1,\alpha}$），我们可以获得对所有 $p \in (1,\infty)$ 成立的全局 $L^p$ 估计。[@problem_id:3033297]

### 理论的延伸与应用

上述原理和机制构成了现代[椭圆正则性理论](@entry_id:203755)的基石，并可以被推广到更广泛的设定中。

#### 抛物方程

对于形如 $u_t - \text{div}(A(x,t)\nabla u) = f$ 的抛物方程，也存在平行的 Schauder 理论。关键的区别在于时间和空间变量的地位不对等，这体现在 **抛物距离** $d((x,t),(y,s)) := |x-y| + |t-s|^{1/2}$ 和各向异性的 **抛物 Hölder 空间** $C^{\alpha, \alpha/2}$ 上。抛物 Schauder 估计表明，如果系数 $A$ 和源项 $f$ 属于 $C^{\alpha, \alpha/2}$，那么解 $u$ 属于 $C^{2+\alpha, 1+\alpha/2}$（即空间二阶导和时间一阶导是 $C^{\alpha, \alpha/2}$ 的）。其证明策略与椭圆情形类似，包括冻结系数、与[热方程](@entry_id:144435)解（caloric polynomials）比较、以及在抛物 Campanato 空间中建立[振荡](@entry_id:267781)衰减估计。[@problem_id:3032579]

#### 完全[非线性方程](@entry_id:145852)：Monge-Ampère 方程

Schauder 型的正则性原理也适用于某些完全非线性方程。一个典范例子是 Monge-Ampère 方程 $\det(D^2 u) = f(x)$，其中 $u$ 是一个[凸函数](@entry_id:143075)。这是一个高度[非线性](@entry_id:637147)的方程，因为算子 $\det(D^2 u)$ 依赖于 $u$ 的[二阶导数](@entry_id:144508)的所有组合。Caffarelli 的突破性工作表明，如果 $f \in C^\alpha(\Omega)$ 并且有正常数下界和[上界](@entry_id:274738)（$0  \lambda \le f \le \Lambda$），那么任何（Aleksandrov意义下的）凸解 $u$ 都属于 $C^{2,\alpha}_{\text{loc}}(\Omega)$。[@problem_id:3033137] 这个结果再次体现了“[源项](@entry_id:269111)的 Hölder 连续性传递给解的最高阶导数”这一 Schauder 精神，尽管其证明方法（包括扰动论证和[仿射变换](@entry_id:144885)[不变性](@entry_id:140168)）远比线性理论复杂。

#### 黎曼[流形上的[椭圆方](@entry_id:634949)程](@entry_id:169190)

[正则性理论](@entry_id:194071)可以自然地推广到[黎曼流形](@entry_id:261160) $(M,g)$ 上。[流形](@entry_id:153038)上的核心算子是 Laplace–Beltrami 算子 $\Delta_g u = \text{div}_g(\nabla u)$。在[局部坐标](@entry_id:181200)下，$\Delta_g u = g^{ij}\nabla_i\nabla_j u = \frac{1}{\sqrt{\det g}}\partial_i(\sqrt{\det g} g^{ij}\partial_j u)$。这是一个具有变系数 $g^{ij}(x)$ 的二阶[椭圆算子](@entry_id:181616)。

为了在[流形](@entry_id:153038)上建立统一的 Schauder 估计，我们需要控制这些系数的光滑性。这可以通过几何量来实现。一个关键工具是 **[调和坐标](@entry_id:192917)（harmonic coordinates）**，即满足 $\Delta_g x^k = 0$ 的[坐标系](@entry_id:156346)。在[调和坐标](@entry_id:192917)下，Laplacian 简化为非[散度形式](@entry_id:748608) $g^{ij}\partial_{ij}u$。一个深刻的几何分析结果是，如果[流形](@entry_id:153038)的 Ricci 曲率有界（$|\text{Ric}_g| \le K$）且[单射半径](@entry_id:192335)有下界（$\text{inj}_g \ge i_0  0$），那么在某个由 $n, K, i_0$ 决定的尺度（调和半径 $r_h$）内，我们可以找到[调和坐标](@entry_id:192917)，使得度量张量 $g_{ij}$ 在 $C^{1,\alpha}$ 范数下接近于欧氏度量。这就为系数 $g^{ij}$ 提供了统一的 $C^\alpha$ 估计，从而可以建立一个常数仅依赖于 $n, \alpha, K, i_0$ 的统一 Schauder 估计。[@problem_id:3025616]

#### 一个更深远的结果：[唯一延拓](@entry_id:168709)性

[正则性理论](@entry_id:194071)的一个精妙应用是证明解的 **[唯一延拓](@entry_id:168709)性（unique continuation）**。[强唯一延拓性](@entry_id:183770)（SUCP）断言，如果一个解在一个点附近以无穷阶消失，那么它必定在整个连通区域内恒等于零。证明 SUCP 的现代方法依赖于 **Carleman 估计**，这是一种在奇性权重函数下成立的加权能量不等式。

对于[散度形式](@entry_id:748608)算子 $L u = \text{div}(A\nabla u) + W \cdot \nabla u + V u$，SUCP 是否成立，对低阶项系数的 **可积性** 有着极为苛刻的要求。通过[标度分析](@entry_id:153681)可以发现，临界空间分别是漂移项 $W$ 的 $L^n$ 空间和位势项 $V$ 的 $L^{n/2}$ 空间。
- **超临界情况**：如果 $W \in L^p$ ($pn$) 且 $V \in L^q$ ($qn/2$)，那么 SUCP 成立，不需要额外的小性条件。这是因为在小尺度上，这些范数会自动变小。[@problem_id:3033298]
- **临界情况**：如果 $W \in L^n$ 且 $V \in L^{n/2}$，则 SUCP 成立需要一个关于这些范数在原点附近小球上的 **小性条件**。[@problem_id:3033298]
- **亚临界情况**：如果 $W$ 或 $V$ 的[可积性](@entry_id:142415)更差，则存在著名的反例，表明 SUCP 会失效。

这一领域的研究展示了[正则性理论](@entry_id:194071)如何从定性的光滑性描述，发展到对解的更深层次的、定量的零点结构行为的探索。[@problem_id:3033298]