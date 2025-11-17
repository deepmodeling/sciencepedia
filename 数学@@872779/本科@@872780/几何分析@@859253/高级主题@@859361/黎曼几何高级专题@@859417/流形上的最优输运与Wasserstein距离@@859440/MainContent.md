## 引言
在数学和科学的许多分支中，我们经常需要比较[概率分布](@entry_id:146404)。然而，如何定义一个既有意义又在几何上直观的“距离”呢？例如，我们如何量化两种细胞群落状态[分布](@entry_id:182848)的差异，或者一个[机器学习模型](@entry_id:262335)生成的数据与真实数据[分布](@entry_id:182848)的差距？[最优输运](@entry_id:196008)（Optimal Transport, OT）理论，及其核心概念——[瓦瑟斯坦距离](@entry_id:147338)（Wasserstein distance），为这一根本问题提供了深刻而强大的答案。它不仅是一种度量，更是一个连接概率论、几何分析和[偏微分方程](@entry_id:141332)的桥梁，通过将比较[分布](@entry_id:182848)的问题重新构想为移动“质量”的最小成本问题，从而在[概率测度](@entry_id:190821)空间上建立起丰富的几何结构。

本文旨在系统地介绍[流形](@entry_id:153038)上[最优输运](@entry_id:196008)的理论与应用。我们将从最基本的思想出发，逐步构建起一个完整的理论框架。在“原理与机制”一章中，您将学习从Monge的输运映射到Kantorovich的输运规划的演进，理解[瓦瑟斯坦距离](@entry_id:147338)的定义及其作为[度量空间](@entry_id:138860)的性质，并探索揭示[最优输运](@entry_id:196008)深刻结构的Brenier定理和Benamou-Brenier动态公式。接下来，在“应用与跨学科联系”一章中，我们将看到这一理论如何在数据科学、机器学习、[偏微分方程](@entry_id:141332)和现代微分几何等前沿领域中发挥作用，解决从稳定[GAN训练](@entry_id:634558)到定义非光滑[空间曲率](@entry_id:755140)等一系列挑战。最后，通过“动手实践”部分的具体计算问题，您将有机会亲手应用这些概念，巩固所学知识。让我们一起踏上这场探索[概率空间](@entry_id:201477)几何的旅程。

## 原理与机制

在理解了将一个[质量分布](@entry_id:158451)变换为另一个[质量分布](@entry_id:158451)的基本问题之后，我们现在深入探讨支撑[最优输运](@entry_id:196008)理论的核心原理和数学机制。本章将系统地阐述如何从一个直观的输运映射概念演进到更普适的输运规划，并在此基础上定义[瓦瑟斯坦距离](@entry_id:147338)。随后，我们将探讨[最优输运](@entry_id:196008)的存在性、结构及其[对偶理论](@entry_id:143133)。最后，我们将介绍[最优输运](@entry_id:196008)的动态观点（即Benamou-Brenier公式），并揭示其如何赋予[概率测度](@entry_id:190821)空间丰富的黎曼几何结构，即所谓的奥托演算（Otto calculus）。

### 基本对偶：映射与规划（Monge 与 Kantorovich）

[最优输运](@entry_id:196008)问题的最早形式由 Gaspard Monge 在18世纪提出。其核心思想非常直观：给定两个质量分布 $\mu$（源）和 $\nu$（目标），如何找到一个**输运映射** (transport map) $T: M \to M$，将[分布](@entry_id:182848) $\mu$ “推送”到[分布](@entry_id:182848) $\nu$，并使总的输运成本最小化？这里的推送，记作 $T_{\#}\mu = \nu$，意味着对于任何区域 $A \subset M$，被映射到 $A$ 内的初始质量总量等于最终在 $A$ 内的质量总量，即 $\mu(T^{-1}(A)) = \nu(A)$。如果成本由每单位质量移动的距离决定，那么总成本就是 $\int_M d(x, T(x)) \,d\mu(x)$。

然而，Monge 的公式存在一个根本性的局限：它要求质量不能被“分裂”。也就是说，从一个点 $x$出发的所有质量必须被输运到同一个目标点 $T(x)$。在许多情况下，这是不可能实现的。

考虑一个简单的思想实验：假设在[单位圆](@entry_id:267290) $S^1$ 上，我们需要将位于点 $x_0$ 的全部质量（由[狄拉克测度](@entry_id:197577) $\mu = \delta_{x_0}$ 描述）输运到两个不同的点 $x_1$ 和 $x_2$，其质量分布为 $\nu = \frac{3}{5}\delta_{x_1} + \frac{2}{5}\delta_{x_2}$ [@problem_id:3058018]。Monge 公式要求找到一个映射 $T$，使得 $T(x_0)$ 同时是 $x_1$ 和 $x_2$。然而，一个单值函数 $T$ 无法将一个点的质量分裂并输送到多个目标点。因此，在这种情况下，Monge 问题无解。

为了克服这一困难，Leonid Kantorovich 在20世纪40年代提出了一个更普适的框架。他不再寻找一个确定的映射 $T$，而是寻找一个**输运规划** (transport plan) 或**耦合** (coupling) $\pi$。这是一个定义在乘积空间 $M \times M$ 上的[概率测度](@entry_id:190821)。一个规划 $\pi$ 是 admissible 的，如果它的两个边缘[分布](@entry_id:182848) (marginals)恰好是 $\mu$ 和 $\nu$。这意味着：

- 对于 $M$ 中的任何[可测集](@entry_id:159173) $A$，$\pi(A \times M) = \mu(A)$。
- 对于 $M$ 中的任何可测集 $B$，$\pi(M \times B) = \nu(B)$。

直观上，$\pi(A \times B)$ 表示从集合 $A$ 中输运到集合 $B$ 中的质量总量。Kantorovich 问题就是要在所有可能的输运规划 $\pi \in \Pi(\mu, \nu)$ 中，找到一个能使总成本最小化的规划，这里的总成本定义为 $\int_{M \times M} c(x,y) \,d\pi(x,y)$，其中 $c(x,y)$ 是从 $x$ 到 $y$ 的单位输运成本。

回到上面的例子 [@problem_id:3058018]，任何 admissible 的规划 $\pi$ 的支撑集必须位于 $\text{supp}(\mu) \times \text{supp}(\nu) = \{x_0\} \times \{x_1, x_2\}$ 之内。这意味着 $\pi$ 必然具有形式 $\pi = c_1 \delta_{(x_0, x_1)} + c_2 \delta_{(x_0, x_2)}$。通过边缘[分布](@entry_id:182848)的约束条件，我们可以唯一地确定系数 $c_1 = \frac{3}{5}$ 和 $c_2 = \frac{2}{5}$。由于在这种情况下只有一个 admissible 的规划，它必然是最优的。这个规划完美地描述了将 $x_0$ 处的质量按 $\frac{3}{5}$ 和 $\frac{2}{5}$ 的比例分别输运到 $x_1$ 和 $x_2$ 的过程，而这正是 Monge 框架无法处理的情形。

Kantorovich 的公式不仅解决了 Monge 公式的局限性，而且为一个更深刻的理论奠定了基础，这个理论将[概率测度](@entry_id:190821)空间赋予了几何结构。

### [概率测度](@entry_id:190821)空间上的瓦瑟斯坦度量

基于 Kantorovich 的[最优输运](@entry_id:196008)成本，我们可以定义一族度量，即**[瓦瑟斯坦距离](@entry_id:147338)** (Wasserstein distance)。对于 $p \ge 1$，两个[概率测度](@entry_id:190821) $\mu$ 和 $\nu$ 之间的 $p$-[瓦瑟斯坦距离](@entry_id:147338) $W_p(\mu, \nu)$ 定义为：
$$
W_p(\mu, \nu) = \left( \inf_{\pi \in \Pi(\mu, \nu)} \int_{M \times M} d(x,y)^p \,d\pi(x,y) \right)^{1/p}
$$
这里 $d(x,y)$ 是[流形](@entry_id:153038) $(M,g)$ 上的[测地距离](@entry_id:159682)。这个定义将[最优输运](@entry_id:196008)问题与度量空间理论联系起来。特别地，当 $p=2$ 时，我们得到了**二次[瓦瑟斯坦距离](@entry_id:147338)** (quadratic Wasserstein distance) $W_2$，它在几何分析和[偏微分方程](@entry_id:141332)中扮演着核心角色。其平方 $W_2^2(\mu, \nu)$ 直接对应于二次成本 $c(x,y) = d(x,y)^2$ 下的最小输运成本。

$W_p$ 距离确实满足[度量空间](@entry_id:138860)的所有公理（非负性、同一性、对称性和三角不等式）。[三角不等式](@entry_id:143750) $W_p(\mu, \eta) \le W_p(\mu, \nu) + W_p(\nu, \eta)$ 的证明巧妙地利用了输运规划的**[粘合引理](@entry_id:151713)** (gluing lemma)。该引理指出，给定一个 $(\mu, \nu)$ 的耦合 $\pi_{12}$ 和一个 $(\nu, \eta)$ 的耦合 $\pi_{23}$，总能构造一个定义在 $M \times M \times M$ 上的测度 $\gamma$，其 $(x,y)$-边缘为 $\pi_{12}$，$(y,z)$-边缘为 $\pi_{23}$ [@problem_id:3058010]。通过将这个三元测度 $\gamma$ 对中间变量 $y$积分掉，我们可以得到一个 $(\mu, \eta)$ 的耦合 $\pi_{13}$。尽管通过粘合最优的 $\pi_{12}^*$ 和 $\pi_{23}^*$ 得到的 $\pi_{13}$ 不一定是最优的，但它提供了一个成本上界，从而证明了[三角不等式](@entry_id:143750)。

因此，装备了 $W_p$ 距离的[概率测度](@entry_id:190821)空间 $\mathcal{P}_p(M)$（即具有有限 $p$ 阶矩的概率测度集合）本身就成了一个度量空间。这个观点是革命性的，它允许我们使用几何工具来分析概率测度和与之相关的演化方程。

### [最优输运](@entry_id:196008)的存在性与结构

一个自然的问题是：[最优输运](@entry_id:196008)规划总是存在的吗？如果存在，它是否具有某种特殊的结构？

答案是肯定的，但需要满足一定的技术条件。一个关键的定理指出，在完备且可分的度量空间（即[波兰空间](@entry_id:148642)，Polish space）上，只要测度 $\mu$ 和 $\nu$ 具有有限的 $p$ 阶矩（例如，对于 $W_2$，需要二阶矩有限），那么对于成本函数 $c(x,y) = d(x,y)^p$，最优的 Kantorovich 输运规划总是存在的 [@problem_id:3058014]。**有限二阶矩**的条件至关重要，它确保了质量不会在输运过程中“泄露到无穷远处”，缺少这个条件，[最优耦合](@entry_id:264340)可能不存在 [@problem_id:3058014, part D]。

更有趣的是，在某些条件下，最优的 Kantorovich 规划实际上是由一个 Monge 映射诱导的。这就是著名的 **[Brenier 定理](@entry_id:202746)** (1991) 及其在黎曼流形上的推广 **McCann 定理** (2001) [@problem_id:3058009]。这些定理的核心结论是：

1.  **关键条件**：源测度 $\mu$ 必须是**绝对连续的** (absolutely continuous) (相对于[流形](@entry_id:153038)上的体[积测度](@entry_id:266846))，即它不能包含[狄拉克测度](@entry_id:197577)那样的集中质量点。注意，这个条件是对源测度 $\mu$ 施加的，而非目标测度 $\nu$ [@problem_id:3058009, part C]。

2.  **存在唯一性**：如果 $\mu$ 是绝对连续的，那么对于二次成本 $c(x,y) = \frac{1}{2}d(x,y)^2$，存在一个唯一的（$\mu$-几乎处处）**[最优输运](@entry_id:196008)映射** $T: M \to M$，使得最优规划 $\pi$ 集中在 $T$ 的图像 $\{(x, T(x)) : x \in M\}$ 上。

3.  **映射的结构**：这个最优映射 $T$ 具有[势能](@entry_id:748988)结构。在[欧氏空间](@entry_id:138052) $\mathbb{R}^n$ 中，$T$ 是一个凸函数 $\psi$ 的梯度，即 $T(x) = \nabla \psi(x)$。在[黎曼流形](@entry_id:261160)上，这个关系推广为 $T(x) = \exp_x(-\nabla \varphi(x))$，其中 $\exp_x$ 是从点 $x$ 出发的[黎曼指数映射](@entry_id:264767)，$\varphi$ 是一个所谓的 **$c$-凸** Kantorovich [势函数](@entry_id:176105)。这深刻地揭示了[最优输运](@entry_id:196008)中的粒子沿[测地线](@entry_id:269969)运动。

一个基础但极具启发性的例子是在 $\mathbb{R}$ 上，将区间 $[0,1]$ 上的[均匀分布](@entry_id:194597) $\mu$ 输运到区间 $[b, a+b]$ 上的[均匀分布](@entry_id:194597) $\nu$ [@problem_id:3058006]。在这种一维情况下，最优映射 $T$ 就是连接两个[分布](@entry_id:182848)的**非减重排函数** (non-decreasing rearrangement)。通过计算两个[分布](@entry_id:182848)的[累积分布函数 (CDF)](@entry_id:264700) $F_\mu$ 和 $F_\nu$，我们可以得到 $T(x) = F_\nu^{-1}(F_\mu(x))$。对于这个问题，我们发现最优映射恰好是[线性映射](@entry_id:185132) $T(x) = ax+b$。一旦确定了最优映射，计算 $W_2^2(\mu,\nu)$ 就简化为计算一个积分 $\int_0^1 |x - T(x)|^2 dx$。

然而，即使源测度和目标测度都非常光滑，[最优输运](@entry_id:196008)映射 $T$ 也未必是全局光滑的。其光滑性可能会因为[流形](@entry_id:153038)的**曲率** (curvature) 和**[割迹](@entry_id:161337)** (cut locus) 的存在而破坏 [@problem_id:3058009, part D]。例如，在球面上，从北半球到南半球的输运可能会在赤道上产生不连续性。因此，McCann 定理的结论通常是在“$\mu$-[几乎处处](@entry_id:146631)”的意义下成立的。值得强调的是，[流形](@entry_id:153038)的曲率条件（例如[非正曲率](@entry_id:203441)）对于最优映射的存在性并非必要条件 [@problem_id:3058009, part B]，尽管它在分析输运性质时非常重要。

### 对偶性与 Kantorovich 势

Kantorovich 问题的另一个强大之处在于它的**[对偶理论](@entry_id:143133)** (duality theory)。每一个最小化问题（称为 primal problem）都对应着一个最大化问题（称为 dual problem）。对于[最优输运](@entry_id:196008)，其对偶问题是：
$$
\sup_{(\psi, \phi)} \left\{ \int_M \psi \,d\mu + \int_M \phi \,d\nu \right\}
$$
其中，函数对 $(\psi, \phi)$ 被称为 **Kantorovich 势** (Kantorovich potentials)，它们必须满足约束条件 $\psi(x) + \phi(y) \le c(x,y)$ 对所有 $(x,y) \in M \times M$ 成立。

**强[对偶定理](@entry_id:137804)** (strong duality theorem) 表明，在一般条件下，primal 问题的最小值等于 dual 问题的最大值。这一深刻结果有两个重要的实践意义：
1.  它提供了一种计算最优成本的替代方法。
2.  它给出了一个 optimality criterion：如果一个输运规划 $\pi$ 和一对势函数 $(\psi, \phi)$ 使得 $\pi$ 的成本等于对偶[目标函数](@entry_id:267263)的值，那么 $\pi$ 就是最优的，$(\psi, \phi)$ 也是最优的。当这种情况发生时，我们有 $\psi(x) + \phi(y) = c(x,y)$ 在 $\pi$ 的支撑集上成立。

我们可以通过一个例子来具体感受对偶性的力量 [@problem_id:3058017]。考虑在[单位圆](@entry_id:267290)上计算两个[离散测度](@entry_id:183686)间的 $W_1$ 距离（成本 $c(x,y)=d(x,y)$）。直接计算表明，任何输运规划的成本都是一个常数 $\frac{\pi}{2}$，因此 $W_1(\mu,\nu) \le \frac{\pi}{2}$。为了证明这就是最优值，我们可以构造一对满足约束条件的势函数 $(\psi, \phi)$，使得 $\int \psi d\mu + \int \phi d\nu = \frac{\pi}{2}$。根据[弱对偶](@entry_id:163073)性（primal value $\ge$ dual value），这立刻证明了 $W_1(\mu,\nu) \ge \frac{\pi}{2}$。两者结合，便确定了最优成本。在这个过程中，最[优势函数](@entry_id:635295) $\psi$ 可以被构造成**c-凹** (c-concave) 的形式，即 $\psi(x) = \inf_y \{c(x,y) - \phi(y)\}$，这与 [Brenier 定理](@entry_id:202746)中的势函数紧密相关。值得注意的是，对偶[势函数](@entry_id:176105)一般不需要满足任何特定的边界条件 [@problem_id:3058014, part E]。

### 动态观点：流与动能

2000年，Benamou 和 Brenier 为二次[瓦瑟斯坦距离](@entry_id:147338) $W_2$ 提供了一个全新的动态诠释，将静态的[匹配问题](@entry_id:275163)转化为一个[流体力学](@entry_id:136788)中的[变分问题](@entry_id:756445)。

这个观点的核心是**[连续性方程](@entry_id:195013)** (continuity equation)：
$$
\partial_t \rho_t + \nabla \cdot (\rho_t v_t) = 0
$$
其中 $\rho_t$ 是随时间 $t$ 变化的质量密度，而 $v_t$ 是一个[速度场](@entry_id:271461)。这个方程描述了在[速度场](@entry_id:271461) $v_t$ 的驱动下，密度 $\rho_t$ 如何演化，同时保证总[质量守恒](@entry_id:204015)。如果[流形](@entry_id:153038)有边界，为了确保质量不流失，需要施加**无通量（诺伊曼）边界条件** (no-flux (Neumann) boundary condition)，即速度场的法向分量为零 $v_t \cdot n = 0$ [@problem_id:3058014, part A]。

**Benamou-Brenier 公式**指出，两个测度 $\mu_0$ 和 $\mu_1$（分别对应密度 $\rho_0$ 和 $\rho_1$）之间的平方 $W_2$ 距离，等于在所有满足连续性方程且连接 $\rho_0$ 和 $\rho_1$ 的路径 $(\rho_t, v_t)$ 中，总动能 (total kinetic energy) 的最小值：
$$
W_2^2(\mu_0, \mu_1) = \inf \left\{ \int_0^1 \int_M |v_t(x)|^2 \,d\mu_t(x) \,dt \right\}
$$
其中 $d\mu_t = \rho_t d\text{vol}$。

这个公式的意义非凡：它将[瓦瑟斯坦距离](@entry_id:147338)解释为“移动质量从初始[分布](@entry_id:182848)到最终[分布](@entry_id:182848)所需的最少能量”。最优的路径对应于粒子沿着[流形](@entry_id:153038)上的[测地线](@entry_id:269969)以恒定速度运动。

一个清晰的例子是[单位圆](@entry_id:267290)上密度的刚性旋转 [@problem_id:3058012]。考虑一个初始密度 $\rho_0$ 和一个由它旋转角度 $\alpha$ 得到的最终密度 $\rho_1$。我们可以构造一个路径，其中密度 $\rho_t$ 是 $\rho_0$ 旋转角度 $\alpha t$ 的结果，而[速度场](@entry_id:271461)是恒定的 $v_t(\theta) = \alpha$。可以验证这条路径满足连续性方程。计算其总动能得到 $\alpha^2$。另一方面，通过基本的能量-长度不等式可知，任何连接初始和最终构型的路径的总动能至少是 $\alpha^2$。由于我们构造的路径达到了这个下界，因此它是最优的，故 $W_2^2(\rho_0, \rho_1) = \alpha^2$。

### 瓦瑟斯坦空间的黎曼几何：奥托演算与梯度流

Benamou-Brenier 公式暗示了一个更为深刻的结构：[概率测度](@entry_id:190821)空间 $(\mathcal{P}_2(M), W_2)$ 本身可以被看作是一个（无穷维的）[黎曼流形](@entry_id:261160)。Felix Otto 将这一思想发展成一个强大的计算框架，即**奥托演算** (Otto calculus)。

在这个框架中：
-   **切空间**：在一点 $\rho$（一个密度）的[切空间](@entry_id:199137) $T_\rho \mathcal{P}_2(M)$ 由满足 $\int \sigma d\text{vol}=0$ 的扰动 $\sigma$ 组成。根据 Hodge 分解理论，任何这样的扰动都可以被看作是由一个势函数 $\phi$ 通过连续性方程生成的：$\sigma = - \nabla \cdot (\rho \nabla \phi)$。
-   **[黎曼度量](@entry_id:754359)**：两个[切向量](@entry_id:265494) $\sigma_1 = - \nabla \cdot (\rho \nabla \phi_1)$ 和 $\sigma_2 = - \nabla \cdot (\rho \nabla \phi_2)$ 的[内积](@entry_id:158127)定义为相应速度场动能的[互相关](@entry_id:143353)：
    $$
    \langle \sigma_1, \sigma_2 \rangle_\rho = \int_M \langle \nabla \phi_1, \nabla \phi_2 \rangle_g \, \rho \,d\text{vol}
    $$
    其中 $\langle \cdot, \cdot \rangle_g$ 是底层流形 $M$ 上的度量[内积](@entry_id:158127)。

[瓦瑟斯坦距离](@entry_id:147338)就是这个无穷维[黎曼流形](@entry_id:261160)上的[测地线](@entry_id:269969)距离。对于两个非常接近的密度 $\rho_0$ 和 $\rho_1$，它们之间的平方[瓦瑟斯坦距离](@entry_id:147338)可以近似为它们差[向量的范数](@entry_id:154882)平方：$W_2^2(\rho_0, \rho_1) \approx \|\rho_1 - \rho_0\|_{(\rho_0+\rho_1)/2}^2$。

例如，在一维环面 $T^1$ 上，我们可以计算两个微小扰动密度 $\rho_0(x) = 1 + \varepsilon a \cos(2\pi x)$ 和 $\rho_1(x) = 1 + \varepsilon b \cos(2\pi x) + \varepsilon c \sin(2\pi x)$ 之间的距离 [@problem_id:3058019]。其差向量为 $\sigma(x) = \rho_1(x) - \rho_0(x)$。通过求解泊松方程 $-\phi'' = \sigma$ 找到对应的[势函数](@entry_id:176105) $\phi$，然后计算范数平方 $\|\sigma\|_1^2 = \int_0^1 (\phi'(x))^2 dx$，我们就可以得到 $W_2^2(\rho_0, \rho_1)$ 在 $\varepsilon \to 0$ 时的首项。

这种黎曼几何结构最重要的应用之一是定义泛函在瓦瑟斯坦空间中的**[梯度流](@entry_id:635964)** (gradient flows)。一个泛函 $\mathcal{E}: \mathcal{P}_2(M) \to \mathbb{R}$ 的[梯度流](@entry_id:635964)是一条曲线 $(\mu_t)_{t \ge 0}$，它在每一点都朝着使 $\mathcal{E}$ 下降最快的方向移动。许多重要的[偏微分方程](@entry_id:141332)，如[热方程](@entry_id:144435)和 [Fokker-Planck](@entry_id:635508) 方程，都可以被解释为某个能量泛函在瓦瑟斯坦空间中的梯度流。

**Jordan-Kinderlehrer-Otto (JKO) 格式**是数值计算这种[梯度流](@entry_id:635964)的一种方法。它通过一系列迭代的最小化问题来离散化时间演化：
$$
\mu_{k+1} \in \operatorname*{arg\,min}_{\mu \in \mathcal{P}_2(M)} \left\{ \frac{1}{2\tau} W_2^2(\mu, \mu_k) + \mathcal{E}(\mu) \right\}
$$
每一小步 $\tau$ 的演化都是在“不要离当前位置太远”（$W_2^2$ 项）和“尽可能降低能量”（$\mathcal{E}$ 项）之间做出权衡。

考虑[能量泛函](@entry_id:170311)为二阶矩 $\mathcal{E}(\mu) = \frac{1}{2} \int |x|^2 d\mu(x)$ [@problem_id:3058008]。从一个[高斯分布](@entry_id:154414) $\mu_0 = \mathcal{N}(m_0, \sigma_0^2)$ 出发，执行一步 JKO 格式，并限制在所有[高斯测度](@entry_id:749747)中寻找最小值。通过显式计算[高斯测度](@entry_id:749747)间的 $W_2$ 距离和它们的二阶矩，我们可以求解这个最小化问题，得到新的均值和[标准差](@entry_id:153618)。这个过程精确地再现了 Ornstein-Uhlenbeck 过程的演化，揭示了该[随机过程](@entry_id:159502)与二阶矩泛函在瓦瑟斯坦空间中[梯度流](@entry_id:635964)的深刻联系。

### 与信息论的联系：输运不等式

瓦瑟斯坦空间的几何结构与信息论中的核心概念（如熵和[费雪信息](@entry_id:144784)）之间存在着深刻的联系。这些联系表现为一系列**输运不等式** (transport inequalities)。

一个典型的例子是 **HWI 不等式** [@problem_id:3058011]。它关联了三个量：
-   **[相对熵](@entry_id:263920) (Relative Entropy)**：$H(\mu|\nu) = \int \ln\left(\frac{d\mu}{d\nu}\right) d\mu$，衡量测度 $\mu$ 相对于参考测度 $\nu$ 的“无序性”。
-   **[瓦瑟斯坦距离](@entry_id:147338) (Wasserstein distance)**：$W_2(\mu,\nu)$。
-   **相对[费雪信息](@entry_id:144784) (Relative Fisher Information)**：$I(\mu|\nu) = \int \left|\nabla \ln\left(\frac{d\mu}{d\nu}\right)\right|^2 d\mu$，衡量 $\mu$ 相对于 $\nu$ 的“[振荡](@entry_id:267781)”或“光滑度”。

当参考测度 $\nu \propto \exp(-V(x))$ 的[势函数](@entry_id:176105) $V$ 满足一定的[凸性](@entry_id:138568)条件，即所谓的 **Bakry-Émery 曲率条件** $\nabla^2 V \ge \kappa \, \text{Id}$（其中 $\kappa$ 是一个正常数），那么熵泛函 $H(\cdot|\nu)$ 沿着瓦瑟斯坦空间中的[测地线](@entry_id:269969)是 $\kappa$-凸的。这个几何性质可以导出如下不等式：
$$
H(\mu|\nu) \le W_2(\mu,\nu)\sqrt{I(\mu|\nu)} - \frac{\kappa}{2} W_2^2(\mu,\nu)
$$
这个 HWI 不等式是 Otto 演算威力的一个辉煌范例。它可以被看作是无穷维黎曼流形上曲率下界的一个解析表达。在特定情况下，例如当 $\mu$ 和 $\nu$ 是具有相同[方差](@entry_id:200758)的两个[高斯分布](@entry_id:154414)时，这个不等式是“sharp”的，即等号成立，并且它给出了 $W_2(\mu,\nu)$ 的精确值 [@problem_id:3058011]。这些不等式在概率论、统计物理和[偏微分方程](@entry_id:141332)[收敛性分析](@entry_id:151547)等领域都有着广泛的应用。