## 引言
在[阿尔伯特·爱因斯坦](@entry_id:271868)的狭义相对论革命中，我们对宇宙的基本认知被重塑：空间和时间不再是分离的实体，而是统一为一个四维的“时空”连续体。这一深刻的见解带来了一个核心挑战：我们如何量化这个新时空的几何结构？传统的欧几里得距离概念已不再适用，物理学迫切需要一个新工具来定义事件间的关系、[不变量](@entry_id:148850)和因果律。

本文旨在深入剖析解决这一挑战的核心概念——[闵可夫斯基度规张量](@entry_id:180802)。它是描述[平直时空几何](@entry_id:271109)的基石，其重要性贯穿了从[经典电动力学](@entry_id:270496)到前沿[量子场论](@entry_id:138177)的整个现代物理学。通过本文的学习，您将掌握这一基础工具的精髓。

我们将分三个部分展开探索。在**“原理与机制”**一章中，您将学习[闵可夫斯基度规](@entry_id:154660)的定义、它如何通过[升降指标](@entry_id:161292)在[张量代数](@entry_id:161671)中发挥作用，以及它如何确立时空中的因果关系。随后，在**“应用与跨学科联系”**一章中，我们将展示其在粒子物理、[连续介质力学](@entry_id:155125)中的具体应用，并阐明它作为连接狭义相对论与广义相对论的理论桥梁。最后，**“动手实践”**部分将提供一系列练习，帮助您将理论知识转化为解决实际问题的能力。

## 原理与机制

在狭义相对论中，我们不再将时间和空间视为独立的实体，而是将它们统一为一个四维的连续体，即时空。为了描述这个时空的几何结构，我们需要一个数学工具来测量事件之间的“距离”。这个工具就是 **[闵可夫斯基度规张量](@entry_id:180802) (Minkowski metric tensor)**，记为 $\eta_{\mu\nu}$。它是一切相对论计算的基石，定义了时空中的[内积](@entry_id:158127)、范数和[因果结构](@entry_id:159914)。

### [时空几何](@entry_id:139497)的基石：[闵可夫斯基度规](@entry_id:154660)

在[惯性参考系](@entry_id:276742)中，一个事件由其时空坐标 $x^\mu = (x^0, x^1, x^2, x^3)$ 描述，其中 $x^0 = ct$ 是时间坐标（乘以光速 $c$），而 $(x^1, x^2, x^3)$ 是空间坐标。两个无限接近的事件，其坐标差为 $dx^\mu$，它们之间的 **[时空间隔](@entry_id:154935) (spacetime interval)** 的平方 $ds^2$ 定义为：

$$
ds^2 = \eta_{\mu\nu} dx^\mu dx^\nu
$$

这里我们采用了爱因斯坦求和约定，即对重复出现的希腊字母指标（如 $\mu$ 和 $\nu$）从 0 到 3 进行求和。这个 $ds^2$ 是一个洛伦兹不变量，意味着在所有[惯性参考系](@entry_id:276742)中，它的值都保持不变。这是[狭义相对论](@entry_id:275552)的核心公设——[光速不变原理](@entry_id:201268)的直接数学体现。

[闵可夫斯基度规](@entry_id:154660) $\eta_{\mu\nu}$ 的具体分量取决于所选择的 **符号约定 (signature convention)**。在物理学文献中，最常见的两种约定是 $(+,-,-,-)$ 和 $(-,+,+,+)$。

在 $(+,-,-,-)$ 约定下，[度规张量](@entry_id:160222)的矩阵形式为：
$$
\eta_{\mu\nu} = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & -1 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & -1 \end{pmatrix}
$$
此时，时空间隔写作 $ds^2 = (c dt)^2 - (dx)^2 - (dy)^2 - (dz)^2$。这个约定在广义相对论和宇宙学中尤为常见。

在 $(-,+,+,+)$ 约定下，度规张量的矩阵形式为：
$$
\eta_{\mu\nu} = \begin{pmatrix} -1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}
$$
此时，[时空间隔](@entry_id:154935)写作 $ds^2 = -(c dt)^2 + (dx)^2 + (dy)^2 + (dz)^2$。这个约定在[粒子物理学](@entry_id:145253)领域较为流行。

选择哪种约定纯粹是习惯问题，物理结论并不会因此改变。关键在于在整个计算过程中保持一致。在本章的论述中，我们将主要采用 $(+,-,-,-)$ 约定，但在讨论特定问题时，会明确指出其所使用的约定。

### 度规的代数功能：[升降指标](@entry_id:161292)

[度规张量](@entry_id:160222)不仅定义了时空的几何，它在[张量代数](@entry_id:161671)中也扮演着至关重要的角色：它建立了 **[逆变](@entry_id:192290) (contravariant)** [四维矢量](@entry_id:275085)（指标在上，如 $A^\mu$）和 **协变 (covariant)** 四维矢量（指标在下，如 $A_\mu$）之间的联系。这个过程被称为 **[升降指标](@entry_id:161292) (raising and lowering indices)**。

将一个[逆变](@entry_id:192290)矢量的指标“降低”，我们使用[协变](@entry_id:634097)[度规张量](@entry_id:160222)：
$$
A_\mu = \eta_{\mu\nu} A^\nu
$$
反之，将一个[协变矢量](@entry_id:263917)的指标“升高”，我们使用[逆变](@entry_id:192290)度规张量 $\eta^{\mu\nu}$：
$$
A^\mu = \eta^{\mu\nu} A_\nu
$$
[逆变](@entry_id:192290)度规张量 $\eta^{\mu\nu}$ 是协变度规张量 $\eta_{\mu\nu}$ 的矩阵逆。由于[闵可夫斯基度规](@entry_id:154660)是[对角矩阵](@entry_id:637782)，其[逆矩阵](@entry_id:140380)的分量就是原矩阵对角线分量的倒数。因此，在 $(+,-,-,-)$ 和 $(-,+,+,+)$ 两种约定下，$\eta^{\mu\nu}$ 的分量恰好与 $\eta_{\mu\nu}$ 相同。

让我们通过一个具体的例子来理解指标降低的过程 [@problem_id:1844782]。假设在一个[粒子加速器](@entry_id:148838)实验中，事件 A 是在时空原点 $(0,0,0,0)$ 产生一个粒子，事件 B 是在时刻 $T$、空间位置 $(L_x, L_y, 0)$ 探测到该粒子。那么，连接这两个事件的[逆变](@entry_id:192290)[时空分离矢量](@entry_id:271167)为 $\Delta x^\mu = x_B^\mu - x_A^\mu = (cT, L_x, L_y, 0)$。我们现在来计算对应的协变分量 $(\Delta x)_\mu$。采用 $(+,-,-,-)$ 约定，即 $\eta_{\mu\nu} = \text{diag}(1, -1, -1, -1)$：
$$
(\Delta x)_0 = \eta_{0\nu} \Delta x^\nu = \eta_{00} \Delta x^0 = (1)(cT) = cT
$$
$$
(\Delta x)_1 = \eta_{1\nu} \Delta x^\nu = \eta_{11} \Delta x^1 = (-1)(L_x) = -L_x
$$
$$
(\Delta x)_2 = \eta_{2\nu} \Delta x^\nu = \eta_{22} \Delta x^2 = (-1)(L_y) = -L_y
$$
$$
(\Delta x)_3 = \eta_{3\nu} \Delta x^\nu = \eta_{33} \Delta x^3 = (-1)(0) = 0
$$
因此，协变[时空分离矢量](@entry_id:271167)为 $(\Delta x)_\mu = (cT, -L_x, -L_y, 0)$。

这个例子揭示了一个普遍规律 [@problem_id:1844749]：对于任何四维矢量 $A^\mu = (A^0, \vec{A})$，在使用 $(+,-,-,-)$ 约定时，其协变分量的时间部分保持不变，$A_0 = A^0$，而空间部分则反号，$A_i = -A^i$（其中 $i=1,2,3$）。这是[闵可夫斯基时空](@entry_id:156421)与我们熟悉的欧几里得空间的一个关键区别，后者的度规是单位矩阵，[升降指标](@entry_id:161292)不会改变分量的值。

[逆变和协变](@entry_id:151323)[度规张量](@entry_id:160222)互为逆的关系，可以用 **克罗内克-δ (Kronecker delta)** 张量 $\delta^\mu_\nu$ 来精确表述 [@problem_id:1844769]。$\delta^\mu_\nu$ 定义为：当 $\mu=\nu$ 时为 1，当 $\mu\neq\nu$ 时为 0。它们的乘积是：
$$
\eta^{\mu\sigma} \eta_{\sigma\nu} = \delta^\mu_\nu
$$
这在数学上正是矩阵互逆的定义。$\delta^\mu_\nu$ 的作用类似于一个单位矩阵，它在与[张量缩并](@entry_id:193373)时会替换指标。例如，对克罗内克-δ本身进行[降指标](@entry_id:272166)操作，会直接得到[度规张量](@entry_id:160222) [@problem_id:1844734]：
$$
\eta_{\mu\alpha} \delta^\alpha_\nu = \eta_{\mu\nu}
$$
这个简单的恒等式体现了[度规张量](@entry_id:160222)和克罗内克-δ在张量运算中的基础地位。此外，对 $\delta^\mu_\nu$ 取迹（即对角[线元](@entry_id:196833)素求和），我们得到 $\delta^\mu_\mu = \delta^0_0 + \delta^1_1 + \delta^2_2 + \delta^3_3 = 1+1+1+1 = 4$，这个结果正是时空的维度 [@problem_id:1844769]。

### [洛伦兹不变量](@entry_id:161821)：[标量积](@entry_id:138996)与物理实在

度规张量的核心物理意义在于，它能够构造出在洛伦兹变换下保持不变的量，即 **[洛伦兹标量](@entry_id:275319) (Lorentz scalars)**。两个[四维矢量](@entry_id:275085) $A^\mu$ 和 $B^\mu$ 的 **[标量积](@entry_id:138996) (scalar product)** 定义为：
$$
A \cdot B \equiv \eta_{\mu\nu} A^\mu B^\nu = A_\mu B^\mu = A^\mu B_\mu
$$
这个[标量积](@entry_id:138996)的结果是一个与[参考系](@entry_id:169232)无关的数值。一个四维矢量与自身的[标量积](@entry_id:138996)，称为其“模方”(squared norm)。

最重要的应用是计算 **四维动量 (four-momentum)** $p^\mu$ 的模方 [@problem_id:1844781]。一个静止质量为 $m$、三维速度为 $\vec{v}$ 的粒子，其[逆变](@entry_id:192290)[四维动量](@entry_id:272346)为 $p^\mu = (\gamma mc, \gamma m\vec{v})$，其中 $\gamma = (1 - |\vec{v}|^2/c^2)^{-1/2}$ 是洛伦兹因子。

让我们在 $(-,+,+,+)$ 约定下计算 $p_\mu p^\mu$。首先，降低指标得到[协变](@entry_id:634097)四维动量：
$p_0 = \eta_{00} p^0 = (-1)(\gamma m c) = -\gamma m c$
$p_i = \eta_{ii} p^i = (1)(\gamma m v_i) = \gamma m v_i$
于是，$p_\mu = (-\gamma mc, \gamma m\vec{v})$。
现在计算[标量积](@entry_id:138996)：
$$
p_\mu p^\mu = p_0 p^0 + \sum_{i=1}^3 p_i p^i = (-\gamma mc)(\gamma mc) + (\gamma m\vec{v}) \cdot (\gamma m\vec{v})
$$
$$
= -(\gamma m c)^2 + (\gamma m)^2 |\vec{v}|^2 = -(\gamma m)^2 (c^2 - |\vec{v}|^2)
$$
利用 $\gamma^{-2} = 1 - |\vec{v}|^2/c^2 = (c^2-|\vec{v}|^2)/c^2$，我们有 $c^2 - |\vec{v}|^2 = c^2/\gamma^2$。代入上式：
$$
p_\mu p^\mu = -(\gamma m)^2 \left(\frac{c^2}{\gamma^2}\right) = -m^2 c^2
$$
这个结果 $-m^2 c^2$ 是一个[不变量](@entry_id:148850)，它只取决于粒子的静止质量。这个关系式被称为 **[在壳条件](@entry_id:189200) (mass-shell condition)**，它定义了物理粒子的能量和动量必须满足的约束。如果在 $(+,-,-,-)$ 约定下计算，结果将是 $p_\mu p^\mu = m^2 c^2$。

### [时空间隔](@entry_id:154935)的物理应用

#### 因果性与[时空结构](@entry_id:158931)

[时空间隔](@entry_id:154935) $\Delta s^2 = \eta_{\mu\nu} \Delta x^\mu \Delta x^\nu$ 的正负号决定了两个事件之间的因果关系。在 $(+,-,-,-)$ 约定下：
- **[类时间隔](@entry_id:276041) (Timelike interval)**: $\Delta s^2 > 0$。这意味着存在一个[参考系](@entry_id:169232)，使得两个事件在同一空间位置发生。它们可以有因果联系，一个事件可以是另一个事件的因或果。
- **[类空间隔](@entry_id:183831) (Spacelike interval)**: $\Delta s^2 < 0$。这意味着存在一个[参考系](@entry_id:169232)，使得两个事件同时发生。它们之间不可能有因果联系，因为没有任何信号（包括光）能从一个事件传播到另一个。
- **[类光间隔](@entry_id:197063) (Lightlike/null interval)**: $\Delta s^2 = 0$。只有以光速传播的信号才能连接这两个事件。

考虑一个更复杂的场景 [@problem_id:410686]：一颗超[新星爆发](@entry_id:160050)（事件 $E_S$），其发出的光穿过[折射率](@entry_id:168910)为 $n>1$ 的星际介质，最终被一颗静止的行星上的天文学家观测到（事件 $E_O$）。设[超新星](@entry_id:161773)与行星间的距离为 $L$。在这个问题中，度规约定为 $(-,+,+,+)$。光在介质中的速度为 $v=c/n$，因此光从 $E_S$ 传播到 $E_O$ 所需的时间为 $\Delta t = L/v = nL/c$。空间分离为 $|\Delta \vec{x}| = L$。时空间隔的平方为：
$$
\Delta s^2 = -(c\Delta t)^2 + |\Delta \vec{x}|^2 = -(c \cdot \frac{nL}{c})^2 + L^2 = -n^2 L^2 + L^2 = L^2(1 - n^2)
$$
由于 $n>1$，所以 $1-n^2 < 0$，因此 $\Delta s^2 < 0$。根据 $(-,+,+,+)$ 约定，这是一个[类时间隔](@entry_id:276041)。这符合物理直觉：超[新星爆发](@entry_id:160050)是观测到的原因，它们之间存在因果联系，因此间隔必须是类时的。

#### 固有时

对于沿着一条类时世界线（一个物体在时[空中运动](@entry_id:172562)的轨迹）的观察者，他们所经历的时间被称为 **[固有时](@entry_id:192124) (proper time)**，记为 $\tau$。[固有时](@entry_id:192124)与时空间隔的关系为：
$$
c^2 d\tau^2 = ds^2
$$
对于两个由类时[世界线](@entry_id:199036)连接的事件 A 和 B，总的固有时是 $\Delta\tau = \frac{1}{c} \int_A^B ds$。如果物体在两事件间做惯性运动，[固有时](@entry_id:192124)就简化为 $\Delta\tau = \frac{1}{c}\sqrt{\Delta s^2}$。

固有时是物理学家真正关心的“时间”，它是观察者手表上流逝的时间。一个经典的例子是计算非惯性旅程中的[固有时](@entry_id:192124) [@problem_id:410614]。假设一艘飞船从时空原点 A(0,0) 出发，先匀速飞行到 B($T/2, X/4$)，再立即改变速度匀速飞行到 C($T, X$)。飞船的总固有时 $\tau_{AC}$ 是两段旅程的固有时之和：
$$
\tau_{AC} = \tau_{AB} + \tau_{BC}
$$
对于 AB 段，$\Delta(ct)_{AB} = T/2$, $\Delta x_{AB} = X/4$。
$$
\tau_{AB} = \frac{1}{c}\sqrt{\left(\frac{T}{2}\right)^2 - \left(\frac{X}{4}\right)^2} = \frac{1}{4c}\sqrt{4T^2 - X^2}
$$
对于 BC 段，$\Delta(ct)_{BC} = T/2$, $\Delta x_{BC} = 3X/4$。
$$
\tau_{BC} = \frac{1}{c}\sqrt{\left(\frac{T}{2}\right)^2 - \left(\frac{3X}{4}\right)^2} = \frac{1}{4c}\sqrt{4T^2 - 9X^2}
$$
飞船经历的总[固有时](@entry_id:192124)为 $\tau_{AC} = \frac{1}{4c}(\sqrt{4T^2 - X^2} + \sqrt{4T^2 - 9X^2})$。这个时间通常小于[参考系](@entry_id:169232)中的[坐标时](@entry_id:263720)间 $t_C = T/c$，这正是时间膨胀效应的体现。

### 度规与[时空对称性](@entry_id:179029)：洛伦兹变换

[闵可夫斯基度规](@entry_id:154660)之所以特殊，是因为它在 **洛伦兹变换 (Lorentz transformations)** 下保持不变。洛伦兹变换是连接不同惯性参考系坐标的线性变换，可以看作是[闵可夫斯基时空](@entry_id:156421)中的“旋转”。如果一个[变换矩阵](@entry_id:151616) $\Lambda^\mu_{\ \nu}$ 描述了一个[洛伦兹变换](@entry_id:176827)，那么它必须满足以下条件：
$$
\eta_{\mu\nu} = \Lambda^\alpha_{\ \mu} \eta_{\alpha\beta} \Lambda^\beta_{\ \nu}
$$
用矩阵语言写，就是 $\eta = \Lambda^T \eta \Lambda$。这个等式是洛伦兹变换的定义。

我们可以通过一个具体的计算来验证这一点 [@problem_id:410697]。考虑一个沿任意方向 $\vec{v}$ 的[洛伦兹助推](@entry_id:201972)（boost），其[变换矩阵](@entry_id:151616)分量为 $\Lambda^0_{\ 0} = \gamma$, $\Lambda^0_{\ i} = \Lambda^i_{\ 0} = -\gamma v^i/c$, $\Lambda^i_{\ j} = \delta^i_j + (\gamma - 1) \frac{v^i v_j}{v^2}$。让我们在 $(+,-,-,-)$ 约定下，计算 $(\Lambda^T \eta \Lambda)_{0i}$ 分量：
$$
(\Lambda^T \eta \Lambda)_{0i} = \sum_{\alpha, \beta=0}^3 (\Lambda^T)_{0\alpha} \eta_{\alpha\beta} \Lambda^\beta_{\ i} = \sum_{\alpha, \beta=0}^3 \Lambda^\alpha_{\ 0} \eta_{\alpha\beta} \Lambda^\beta_{\ i}
$$
我们将和式分成 $\alpha=0$ 和 $\alpha=k$（空间部分）两部分：
当 $\alpha=0$ 时，项为 $\Lambda^0_{\ 0} \eta_{0\beta} \Lambda^\beta_{\ i} = \gamma \cdot \eta_{00} \Lambda^0_{\ i} = \gamma \cdot (1) \cdot (-\gamma v^i/c) = -\frac{\gamma^2 v^i}{c}$。
当 $\alpha=k$ 时，项为 $\sum_{k=1}^3 \Lambda^k_{\ 0} \eta_{k\beta} \Lambda^\beta_{\ i} = \sum_{k=1}^3 (-\gamma v^k/c) \eta_{kk} \Lambda^k_{\ i} = \sum_{k=1}^3 (-\gamma v^k/c) (-1) \Lambda^k_{\ i} = \frac{\gamma}{c}\sum_{k=1}^3 v^k \Lambda^k_{\ i}$。
其中 $\sum_k v^k \Lambda^k_{\ i} = \sum_k v^k (\delta^k_i + (\gamma-1)\frac{v^k v_i}{v^2}) = v^i + (\gamma-1)\frac{v^2 v_i}{v^2} = \gamma v^i$。
所以空间部分的贡献是 $\frac{\gamma}{c}(\gamma v^i) = \frac{\gamma^2 v^i}{c}$。
将两部分相加，我们得到 $(\Lambda^T \eta \Lambda)_{0i} = -\frac{\gamma^2 v^i}{c} + \frac{\gamma^2 v^i}{c} = 0$。这与 $\eta_{0i}=0$ 相符，验证了洛伦兹变换确实保持了度规的非对角分量为零。

### 进阶主题：[四维矢量](@entry_id:275085)的几何分类与[广义坐标](@entry_id:156576)

#### [四维矢量](@entry_id:275085)的几何分类
我们之前根据时空间隔的符号对事件分离进行了分类。这个思想可以推广到任何四维矢量 $A^\mu$。根据其模方 $A^2 = A_\mu A^\mu$ 的符号（在 $(+,-,-,-)$ 约定下）：
- $A^2 > 0$: 类时矢量
- $A^2 < 0$: 类空矢量
- $A^2 = 0$: 类光（或零）矢量

这个分类具有深刻的几何和物理意义。例如，一个四维矢量 $Q^\mu$ 只有当它是 **类空 (spacelike)** 的，才存在一个[洛伦兹变换](@entry_id:176827)，能将它变换到一个新的[参考系](@entry_id:169232) $S'$，使得其时间分量为零（即 $Q'^0=0$）。

考虑一个由两个粒子四维动量之差构成的矢量 $Q^\mu = p_1^\mu - p_2^\mu$ [@problem_id:410632]。要找到存在一个[参考系](@entry_id:169232)使得 $Q'^0 = 0$ 的条件，我们只需计算其模方 $Q^2$ 并要求它为类空。在 $(+,-,-,-)$ 约定下，即 $Q^2 < 0$。
$$
Q^2 = (p_1 - p_2) \cdot (p_1 - p_2) = p_1^2 - 2 p_1 \cdot p_2 + p_2^2
$$
我们知道 $p_1^2 = (m_1c)^2$ 和 $p_2^2 = (m_2c)^2$。在粒子1的静止系中，$p_1^\mu = (m_1c, \vec{0})$，粒子2的速度为 $\vec{u}$，其四维动量为 $p_2^\mu = (\gamma_u m_2 c, \gamma_u m_2 \vec{u})$。[内积](@entry_id:158127) $p_1 \cdot p_2 = p_{1\mu} p_2^\mu = (m_1c)(\gamma_u m_2 c) - \vec{0} \cdot (\gamma_u m_2 \vec{u}) = \gamma_u m_1 m_2 c^2$。
因此，$Q^2 = (m_1c)^2 + (m_2c)^2 - 2\gamma_u m_1 m_2 c^2$。
$Q^2 < 0$ 的条件变为 $m_1^2 + m_2^2 < 2\gamma_u m_1 m_2$，即 $\gamma_u > \frac{m_1^2 + m_2^2}{2m_1 m_2}$。经过一系列代数运算，这个不等式最终可以表示为对速度 $u$ 的要求：
$$
u > c \frac{|m_1^2 - m_2^2|}{m_1^2 + m_2^2}
$$
这个条件精确地告诉我们，只有当粒子2的速度足够大时，两个四维动量之差才是一个类空矢量，从而可以在某个[参考系](@entry_id:169232)中“抹去”它的时间分量。

#### [非惯性系](@entry_id:168746)中的度规
[闵可夫斯基度规](@entry_id:154660) $\eta_{\mu\nu}$ 的分量是常数，这一简洁优美的形式只在 **惯性参考系的[笛卡尔坐标](@entry_id:167698)** 中成立。当我们转换到[非惯性系](@entry_id:168746)（例如[加速参考系](@entry_id:168026)）或者使用[曲线坐标](@entry_id:178535)时，[度规张量](@entry_id:160222)的分量通常会变得依赖于时空坐标。这是通往广义相对论的关键一步。

一个典型的例子是 **[林德勒坐标](@entry_id:183624) (Rindler coordinates)**，它描述了一个在 $x$ 方向上做[匀加速](@entry_id:268628)运动的观察者的时空 [@problem_id:410628]。从[惯性系](@entry_id:266190)坐标 $(ct, x)$ 到[林德勒坐标](@entry_id:183624) $(\tau, \xi)$ 的变换为：
$$
ct = \xi \sinh\left(\frac{a\tau}{c}\right)
$$
$$
x = \xi \cosh\left(\frac{a\tau}{c}\right)
$$
其中 $a$ 是一个常数加速度。在[广义坐标](@entry_id:156576)变换下，[度规张量](@entry_id:160222)的变换法则是：
$$
g_{\alpha\beta} = \frac{\partial x^\mu}{\partial \tilde{x}^\alpha} \frac{\partial x^\nu}{\partial \tilde{x}^\beta} \eta_{\mu\nu}
$$
让我们计算新度规的时间分量 $g_{\tau\tau}$ (这里采用 $(-,+,+,+)$ 约定, $\eta = \text{diag}(-1,1,1,1)$)：
$$
\frac{\partial (ct)}{\partial \tau} = \xi \frac{a}{c} \cosh\left(\frac{a\tau}{c}\right), \quad \frac{\partial x}{\partial \tau} = \xi \frac{a}{c} \sinh\left(\frac{a\tau}{c}\right)
$$
$$
g_{\tau\tau} = \eta_{00}\left(\frac{\partial (ct)}{\partial \tau}\right)^2 + \eta_{11}\left(\frac{\partial x}{\partial \tau}\right)^2 = (-1)\left(\xi \frac{a}{c} \cosh\left(\frac{a\tau}{c}\right)\right)^2 + (1)\left(\xi \frac{a}{c} \sinh\left(\frac{a\tau}{c}\right)\right)^2
$$
$$
= -\left(\frac{a\xi}{c}\right)^2 \left[\cosh^2\left(\frac{a\tau}{c}\right) - \sinh^2\left(\frac{a\tau}{c}\right)\right]
$$
利用[双曲函数](@entry_id:165175)恒等式 $\cosh^2\theta - \sinh^2\theta = 1$，我们得到：
$$
g_{\tau\tau} = -\frac{a^2\xi^2}{c^2}
$$
我们发现，在[加速参考系](@entry_id:168026)中，度规分量 $g_{\tau\tau}$ 不再是常数，而是依赖于空间坐标 $\xi$。这导致了许多有趣的物理现象，例如[引力红移](@entry_id:158697)的类比和[安鲁效应](@entry_id:146787)。这个例子清晰地表明，度规张量是一个强大的工具，它不仅能描述平直的[闵可夫斯基时空](@entry_id:156421)，还能通过坐标变换来揭示非惯性运动和[引力](@entry_id:175476)的深刻联系。