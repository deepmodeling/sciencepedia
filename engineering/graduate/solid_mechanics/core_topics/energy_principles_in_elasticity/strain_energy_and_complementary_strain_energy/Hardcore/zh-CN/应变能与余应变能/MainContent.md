## 引言
在固体力学领域，能量不仅是物理守恒定律的体现，更是一种深刻的分析视角。应变能与余应变能作为核心概念，提供了一种从全局能量观点理解和求解复杂力学问题的方法，其重要性贯穿了从基础结构分析到前沿材料科学的各个层面。传统力学分析往往依赖于直接求解复杂的微分方程来满足局部平衡和边界条件，这一过程可能非常繁琐。能量法则通过将问题重新表述为求解整个系统能量泛函的极值问题，为我们开辟了一条更为优雅和强大的路径，从而绕开了直接处理微分方程的复杂性。

本文将系统地探讨应变能与余应变能的理论与应用。在第一章“原理与机制”中，我们将从超弹性本构模型出发，建立应变能和余应变能的数学定义，并通过勒让德变换揭示其深刻的对偶性，最终引出最小势能和最小余能等核心变分原理。第二章“应用与交叉学科联系”将展示这些原理在解决实际工程问题中的威力，从经典结构分析到非线性材料模型，并探讨其与热力学、断裂力学等领域的交叉。最后，第三章“动手实践”提供了一系列精心设计的问题，旨在通过具体计算加深您对能量方法在不同场景下应用的理解。通过这三个章节的递进学习，读者将不仅掌握应变能与余应变能的基本理论，更能体会到能量方法作为一种统一思想在现代力学分析中的核心地位和广阔应用前景。

## Principles and Mechanisms

### 弹性变形中的能量守恒：超弹性本构模型

在连续介质力学中，材料的本构关系描述了应力如何随变形而变化。在众多本构模型中，一类特别重要且基础的模型是**超弹性**（hyperelastic）或**格林弹性**（Green-elastic）模型。这类模型的核心假设是材料的变形过程是**能量守恒**的。具体而言，对于一个在恒温条件下经历纯机械加载的物体，其内部储蓄的能量仅取决于当前的变形状态，而与达到该状态所经历的加载路径无关。

这意味着应力所做的功完全转化为可恢复的**应变能**（strain energy），在卸载后可以完全释放。因此，对于任何一个封闭的变形循环（即从一个状态出发，经历一系列变形后回到初始状态），净机械功的输入为零。这一特性可以用一个积分关系来表达：
$$
\oint \boldsymbol{\sigma} : \mathrm{d}\boldsymbol{\varepsilon} = 0
$$
其中 $\boldsymbol{\sigma}$ 是柯西应力张量，$\boldsymbol{\varepsilon}$ 是无穷小应变张量，符号“$:$”表示张量的双点积。根据斯托克斯定理的推广，上述路径无关性的一个必要且充分的条件是，存在一个仅依赖于应变状态的标量势函数——**应变能密度函数**（strain energy density function），通常记为 $w(\boldsymbol{\varepsilon})$，使得应力可以由该势函数对应变的导数得到：
$$
\boldsymbol{\sigma} = \frac{\partial w}{\partial \boldsymbol{\varepsilon}}
$$
在分量形式下，这写作 $\sigma_{ij} = \partial w / \partial \varepsilon_{ij}$。

理解超弹性模型的最佳方式之一是考察不满足其核心假设的反例。许多工程材料的本构行为并非完全保守 [@problem_id:2687717]。例如：
*   **线性粘弹性（Linear Viscoelasticity）**：考虑 Kelvin-Voigt 模型，其应力由 $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon} + \mathbb{H}:\dot{\boldsymbol{\varepsilon}}$ 给出，其中 $\dot{\boldsymbol{\varepsilon}}$ 是应变率张量。应力不仅依赖于当前应变，还依赖于应变率。在循环加载下，由粘性项 $\mathbb{H}:\dot{\boldsymbol{\varepsilon}}$ 产生的功总是正的，代表能量耗散（通常以热的形式）。因此，$\oint \boldsymbol{\sigma}:\mathrm{d}\boldsymbol{\varepsilon} > 0$，不存在仅依赖于 $\boldsymbol{\varepsilon}$ 的应变能势函数。

*   **弹塑性（Elastoplasticity）**：在弹塑性材料中，当应力达到屈服面时，会发生不可逆的塑性流动。变形历史通过内部变量（如塑性应变 $\boldsymbol{\varepsilon}^p$）被“记忆”在材料中。在应力-应变图上，加载和卸载路径不重合，形成一个**滞回环**。这个环所包围的面积代表一个加载循环中因塑性变形而耗散的能量。因此，应力不是应变 $\boldsymbol{\varepsilon}$ 的单值函数，不存在一个全局的应变能函数 $w(\boldsymbol{\varepsilon})$。

*   **非可积弹性（Non-integrable Elasticity）**：即便材料是纯弹性的（无耗散），要存在势函数 $w(\boldsymbol{\varepsilon})$，其切线刚度张量 $\mathbb{C}_{ijkl} = \partial \sigma_{ij} / \partial \varepsilon_{kl}$ 必须满足**主对称性**（major symmetry），即 $\mathbb{C}_{ijkl} = \mathbb{C}_{klij}$。这是一个数学上的可积性条件。可以构造一个理论上的线性弹性关系，例如在平面应变中，$\sigma_{11} = k\varepsilon_{11} + \alpha\varepsilon_{22}$ 和 $\sigma_{22} = k\varepsilon_{22}$，当 $\alpha \neq 0$ 时，我们发现 $\partial \sigma_{11} / \partial \varepsilon_{22} = \alpha$ 而 $\partial \sigma_{22} / \partial \varepsilon_{11} = 0$。由于主对称性被破坏，功增量 $\boldsymbol{\sigma}:\mathrm{d}\boldsymbol{\varepsilon}$ 不是一个全微分，在应变空间中的闭路积分不为零，故不存在势函数 $w(\boldsymbol{\varepsilon})$ [@problem_id:2687717]。

因此，本章后续的讨论将主要集中于满足超弹性假设的材料，这类材料的力学行为可以通过能量势函数进行优雅而深刻的描述。

### 应变能：主势函数

对于恒温、可逆的纯机械过程，应变能密度 $w$ 在热力学上与**亥姆霍兹自由能密度** $\Psi$ 等价。亥姆霍兹自由能是联系力学与热力学的桥梁，其定义为 $\Psi = U_{\text{int}} - TS$，其中 $U_{\text{int}}$ 是内能密度， $T$ 是绝对温度，$S$ 是熵密度。其微分形式为 $\mathrm{d}\Psi = \boldsymbol{\sigma}:\mathrm{d}\boldsymbol{\varepsilon} - S\mathrm{d}T$。在恒温过程（$\mathrm{d}T = 0$）中，这简化为 $\mathrm{d}\Psi = \boldsymbol{\sigma}:\mathrm{d}\boldsymbol{\varepsilon}$。由于应变能的定义就是可恢复的机械功，其微分形式为 $\mathrm{d}w = \boldsymbol{\sigma}:\mathrm{d}\boldsymbol{\varepsilon}$。因此，在恒温条件下，$\mathrm{d}\Psi = \mathrm{d}w$。通过选择在无应变状态下两者均为零的参考态，我们可以得出 $w(\boldsymbol{\varepsilon}) = \Psi(\boldsymbol{\varepsilon}, T_0)$。这表明，在恒温弹性力学中，我们所说的应变能实际上就是亥姆霍兹自由能 [@problem_id:2881852]。

对于各向同性线性弹性材料，其应变能密度 $w$ 必须是应变张量[不变量](@entry_id:148850)的函数。在小应变理论中，我们通常只保留到应变的二次项。最一般的二次形式可以用应变张量的第一不变量 $I_1(\boldsymbol{\varepsilon}) = \operatorname{tr}(\boldsymbol{\varepsilon})$ 和应变张量自身的双点积 $\boldsymbol{\varepsilon}:\boldsymbol{\varepsilon} = \operatorname{tr}(\boldsymbol{\varepsilon}^2)$ 来表示：
$$
w(\boldsymbol{\varepsilon}) = \frac{1}{2}\lambda (I_1(\boldsymbol{\varepsilon}))^2 + \mu (\boldsymbol{\varepsilon}:\boldsymbol{\varepsilon})
$$
其中 $\lambda$ 和 $\mu$ 是材料的**拉梅参数**（Lamé parameters）。$\mu$ 也被称为**剪切模量**（shear modulus）。通过对这个表达式求导 $\boldsymbol{\sigma} = \partial w / \partial \boldsymbol{\varepsilon}$，可以恢复胡克定律的各向同性形式 $\boldsymbol{\sigma} = \lambda(\operatorname{tr}\boldsymbol{\varepsilon})\mathbf{1} + 2\mu\boldsymbol{\varepsilon}$，其中 $\mathbf{1}$ 是二阶单位张量 [@problem_id:2687729]。

应变能密度也可以用其他不变量组合来表示。例如，使用第一和第二主不变量 $I_1(\boldsymbol{\varepsilon})$ 和 $I_2(\boldsymbol{\varepsilon}) = \frac{1}{2}[(\operatorname{tr}\boldsymbol{\varepsilon})^2 - \operatorname{tr}(\boldsymbol{\varepsilon}^2)]$，上述能量表达式可以等价地写为 [@problem_id:2687729]：
$$
w(\boldsymbol{\varepsilon}) = \left(\frac{1}{2}\lambda + \mu\right) (I_1(\boldsymbol{\varepsilon}))^2 - 2\mu I_2(\boldsymbol{\varepsilon})
$$
这种形式的转换在某些理论推导中可能更为方便。

### 余应变能：勒让德变换与对偶势

应变能 $w(\boldsymbol{\varepsilon})$ 将应变视为自变量，应力是其导出量。在许多问题中，特别是那些应力（或力）为已知边界条件的问题中，将应力视为自变量，应变作为导出量，会更加自然。这种视角上的转换是通过**勒让德变换**（Legendre transformation）实现的，它引入了一个对偶的能量函数，称为**余应变能密度**（complementary strain energy density），记为 $w^*(\boldsymbol{\sigma})$。

其定义为：
$$
w^*(\boldsymbol{\sigma}) = \boldsymbol{\sigma}:\boldsymbol{\varepsilon} - w(\boldsymbol{\varepsilon})
$$
为了使 $w^*$ 成为应力的单值函数，需要通过本构关系 $\boldsymbol{\sigma} = \partial w / \partial \boldsymbol{\varepsilon}$ 将 $\boldsymbol{\varepsilon}$ 解出并表示为 $\boldsymbol{\sigma}$ 的函数。

勒让德变换具有优美的对偶性质。对 $w^*(\boldsymbol{\sigma})$ 求关于应力的导数，可以得到应变：
$$
\boldsymbol{\varepsilon} = \frac{\partial w^*}{\partial \boldsymbol{\sigma}}
$$
这一对关系 $\boldsymbol{\sigma} = \partial w / \partial \boldsymbol{\varepsilon}$ 和 $\boldsymbol{\varepsilon} = \partial w^* / \partial \boldsymbol{\sigma}$ 体现了应变能和余应变能在描述材料行为时的对偶性。

在几何上，如果绘制一维应力-应变曲线，应变能 $w$ 代表曲线下方的面积（$\int \sigma \, \mathrm{d}\varepsilon$），而余应变能 $w^*$ 代表曲线与应力轴之间的面积（$\int \varepsilon \, \mathrm{d}\sigma$）。两者的和 $w + w^* = \sigma \varepsilon$ 正好是应力-应变图上由原点、点 $(\varepsilon, \sigma)$、以及坐标轴上的投影点构成的矩形面积。

考虑一个简单的一维非线性弹性材料，其应力-应变关系为幂律形式 $\sigma = K \varepsilon^n$ [@problem_id:1264798]。其应变能密度为 $w(\varepsilon) = \int_0^\varepsilon K (\varepsilon')^n \mathrm{d}\varepsilon' = \frac{K}{n+1}\varepsilon^{n+1}$。通过勒让德变换，其余应变能密度为：
$$
w^*(\sigma) = \sigma \varepsilon - w(\varepsilon) = (K \varepsilon^n) \varepsilon - \frac{K}{n+1}\varepsilon^{n+1} = \frac{n}{n+1}K \varepsilon^{n+1}
$$
有趣的是，该材料的余能与应变能之比为常数 $w^*/w = n$。对于线性弹性材料，$n=1$，此时 $w^* = w$。

这一结论可以推广到三维线性弹性情况。对于各向同性线性弹性材料，应变能密度为 $w(\boldsymbol{\varepsilon}) = \frac{1}{2}\boldsymbol{\sigma}:\boldsymbol{\varepsilon}$。由于本构关系是线性的，余应变能密度同样等于 $\frac{1}{2}\boldsymbol{\sigma}:\boldsymbol{\varepsilon}$。通过将 $\boldsymbol{\varepsilon}$ 表示为 $\boldsymbol{\sigma}$ 的函数，$\boldsymbol{\varepsilon} = \frac{1}{2\mu}\boldsymbol{\sigma} - \frac{\lambda}{2\mu(3\lambda+2\mu)}(\operatorname{tr}\boldsymbol{\sigma})\mathbf{1}$，我们可以得到余应变能密度完全用应力不变量表示的形式 [@problem_id:2687729]：
$$
w^*(\boldsymbol{\sigma}) = \frac{\lambda+\mu}{2\mu(3\lambda+2\mu)} (I_1(\boldsymbol{\sigma}))^2 - \frac{1}{2\mu} I_2(\boldsymbol{\sigma})
$$
对于线性弹性材料，$w(\boldsymbol{\varepsilon})$ 和 $w^*(\boldsymbol{\sigma})$ 相等当且仅当本构关系是线性的。对于非线性材料，两者通常不相等 [@problem_id:2881852]。

### 变分原理：能量泛函的极值

应变能和余应变能的概念从局部（单位体积）推广到整个弹性体，就引出了固体力学中两个最强大的工具：**最小势能原理**和**最小余能原理**。这些变分原理将求解复杂的偏微分方程边值问题，转化为求解一个全局能量泛函的极值问题。

考虑一个弹性杆，其位移场为 $u(x)$。**总势能**（total potential energy）泛函 $\Pi[u]$ 定义为储存在杆内的总应变能与外力所做功的势之差。对于一个在 $x=0$ 处固定 ($u(0)=0$)，在 $x=L$ 处承受端部拉力 $\bar{T}$，并受到体积力 $b(x)$ 作用的杆，其总势能泛函为 [@problem_id:2881859]：
$$
\Pi[u] = \int_0^L \left( \frac{1}{2} E A (u')^2 - A b(x) u(x) \right) \mathrm{d}x - \bar{T} u(L)
$$
其中第一项是总应变能，后两项是外力势。该泛函的求解域是所有满足位移边界条件（$u(0)=0$）且足够光滑的**运动许可位移场**（kinematically admissible displacement fields）。**最小势能原理**断言：在所有运动许可的位移场中，真实的位移场使得总势能泛函 $\Pi[u]$ 取最小值。

与此对偶，**总余能**（total complementary energy）泛函 $\mathcal{C}[N]$ (或 $\Pi^*[N]$) 是在整个杆上对余应变能密度进行积分。对于上述同一问题，其总余能泛函为 [@problem_id:2881859]：
$$
\mathcal{C}[N] = \int_0^L \frac{N(x)^2}{2EA} \mathrm{d}x
$$
该泛函的求解域是所有满足平衡方程（$N'(x) + Ab(x) = 0$）和力边界条件（$N(L)=\bar{T}$）的**静力许可内力场**（statically admissible force fields）。**最小余能原理**断言：在所有静力许可的内力场中，真实的内力场使得总余能泛函 $\mathcal{C}[N]$ 取最小值。

求解最小势能原理的欧拉-拉格朗日方程会得到平衡方程和力边界条件；而求解最小余能原理（在平衡约束下）则会引出几何协调条件。这两个原理为近似方法（如有限元法）提供了坚实的理论基础。

### 能量原理的应用

#### 位移计算：Castigliano 定理与 Crotti-Engesser 定理

能量方法的一个直接应用是计算结构在特定点和方向上的位移。这可以通过对合适的能量泛函求导来实现。这里，区分线性和非线性弹性行为至关重要。

**Crotti-Engesser 定理** 是一个适用于一般（非线性）弹性系统的普适性结论。它指出，广义位移 $q_i$（在广义力 $P_i$ 作用点沿其方向的位移）等于总余能 $U^*$ 对该广义力 $P_i$ 的偏导数 [@problem_id:2628235]：
$$
q_i = \frac{\partial U^*}{\partial P_i}
$$
这里的 $U^*$ 是对整个结构积分得到的总余能，它是外加力 $\{P_i\}$ 的函数。该定理直接源于余能的勒让德变换定义，即 $q_i$ 和 $P_i$ 是对偶变量。

**Castigliano 第二定理** 是一个在工程中广泛应用的版本，它指出广义位移 $q_i$ 等于总**应变能** $U$ 对相应广义力 $P_i$ 的偏导数：
$$
q_i = \frac{\partial U}{\partial P_i}
$$
这个定理有一个关键的隐藏假设：材料必须是**线性弹性**的。只有在线性弹性情况下，应变能和余能才相等（$U = U^*$），并且应变能可以完全用外力来表示。因此，Castigliano 第二定理实质上是 Crotti-Engesser 定理在线性弹性系统下的一个特例 [@problem_id:2628235]。对于非线性弹性问题，必须使用 Crotti-Engesser 定理和余能。

#### 结构单元的能量

这些能量概念可以从三维连续介质的应力/应变推广到梁、杆、轴等结构单元的广义力/广义位移。对于这些一维模型，我们定义单位长度的应变能和余能密度。

例如，对于一个受弯矩 $M$ 作用的欧拉-伯努利梁，其曲率 $\kappa$ 是与 $M$ **功共轭**（work-conjugate）的广义位移。对于受扭矩 $T$ 作用的轴，单位长度扭转角 $\phi'$ 是与 $T$ 功共轭的量 [@problem_id:2881854]。

对于线性弹性梁和轴，其单位长度的应变能密度分别为 $U_0^M = \frac{1}{2}EI \kappa^2$ 和 $U_0^T = \frac{1}{2}GJ (\phi')^2$。通过勒让德变换，可以得到单位长度的余能密度：
$$
U_0^{M*} = \frac{M^2}{2EI}, \quad U_0^{T*} = \frac{T^2}{2GJ}
$$
其中 $EI$ 是抗弯刚度，$GJ$ 是抗扭刚度。通过对这些密度沿结构长度积分，就可以得到整个结构的总余能，并可用于位移计算或变分分析 [@problem_id:2881854]。

#### 圣维南原理的能量诠释

**圣维南原理**（Saint-Venant's principle）指出，局部载荷的分布细节仅在载荷作用点附近区域产生显著影响。在远离该区域的地方，应力场只取决于载荷的静态等效结果（即合力和合力矩）。这个原理也可以从能量的角度来理解。

考虑一个弹性体，在其边界的某个小区域上作用着两种不同的、但**静力等效**的载荷分布。这意味着两种载荷的合力和合力矩完全相同。根据圣维南原理，由这两种载荷之差（一个自平衡的力系）引起的应力场和应变场将随着与加载区距离的增加而迅速衰减。

因此，两种加载情况下应变能密度 $w(\boldsymbol{\varepsilon})$ 的差异也主要局限在加载区附近的一个边界层内。总应变能 $U = \int_\Omega w(\boldsymbol{\varepsilon}) \, dV$ 是一个全局量。如果边界层的体积相对于整个物体的体积非常小，那么这个局部差异对总应变能的贡献也将非常小。当物体的特征尺寸远大于边界层厚度时，两种加载情况下的总应变能之差相对于总能量本身将趋于零 [@problem_id:2687738]。这表明，总应变能这样的全局能量量度对于静力等效载荷的局部细节是**不敏感**的，这为在工程计算中简化载荷模型提供了理论依据。

### 高级主题：凸性、稳定性和有限变形

#### 能量函数的凸性与解的唯一性

应变能函数的数学性质——特别是**凸性**（convexity）——对弹性问题的解具有深远的影响。对于线性弹性材料 $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon}$，其应变能密度为二次型 $w(\boldsymbol{\varepsilon}) = \frac{1}{2}\boldsymbol{\varepsilon}:\mathbb{C}:\boldsymbol{\varepsilon}$。

要使 $w(\boldsymbol{\varepsilon})$ 是一个关于 $\boldsymbol{\varepsilon}$ 的**严格凸函数**，其Hessian矩阵，即刚度张量 $\mathbb{C}$，必须是**正定**的。这意味着对于任何非零的对称应变张量 $\boldsymbol{\varepsilon}$，能量存储必须为正，即 $\boldsymbol{\varepsilon}:\mathbb{C}:\boldsymbol{\varepsilon} > 0$。这个条件被称为**材料稳定性**（material stability）条件 [@problem_id:2675427]。

严格凸的应变能函数确保了总势能泛函 $\Pi[u]$ 也是严格凸的。在数学上，一个严格凸泛函至多只有一个极小值点。这意味着，在给定的边界条件下，弹性体的平衡解是**唯一**的。

同样，余能密度 $w^*(\boldsymbol{\sigma}) = \frac{1}{2}\boldsymbol{\sigma}:\mathbb{S}:\boldsymbol{\sigma}$ 的严格凸性要求柔度张量 $\mathbb{S} = \mathbb{C}^{-1}$ 是正定的。如果 $\mathbb{C}$ 是正定的，那么 $\mathbb{S}$ 也是正定的。这保证了总余能泛函的严格凸性，从而也保证了静力许可应力场解的唯一性 [@problem_id:2675427]。

#### 有限变形理论中的能量

应变能和余能的概念可以自然地推广到**有限变形**（finite deformation）理论中。在这种情况下，我们需要使用更复杂的运动学和应力测度。

在拉格朗日（Lagrangian）描述中，变形由变形梯度张量 $\mathbf{F}$ 描述。一个常用的应变测度是**格林-拉格朗日应变张量** $\mathbf{E} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})$。与其功共轭的应力测度是**第二类皮奥拉-基尔霍夫应力张量**（second Piola-Kirchhoff stress tensor）$\mathbf{S}$。对于有限变形超弹性材料，应变能密度 $\hat{W}$ 是应变测度的函数，例如 $\hat{W}(\mathbf{E})$，并且本构关系为 $S = \partial \hat{W} / \partial \mathbf{E}$。

相应地，余能密度 $\hat{W}^*(\mathbf{S})$ 可以通过勒让德变换定义，并且对偶关系 $\mathbf{E} = \partial \hat{W}^* / \partial \mathbf{S}$ 同样成立。功共轭对 $(\mathbf{S}, \mathbf{E})$ 是有限变形理论中构建变分原理的基石。其他的功共轭对应力-应变率对还包括 $(\mathbf{P}, \dot{\mathbf{F}})$（第一类Piola-Kirchhoff应力与变形梯度率）以及欧拉描述下的 $(\boldsymbol{\sigma}, \mathbf{d})$（柯西应力与变形率张量）[@problem_id:2687724]。

#### 凸性损失与材料失稳

在非线性弹性中，应变能函数的凸性并非总是得到保证。随着材料承受大的变形，应变能函数在某些变形状态下可能会失去其凸性，这预示着材料的**失稳**（instability）。

一个比普通凸性更弱但对稳定性至关重要的条件是**秩一凸性**（rank-one convexity）。它要求能量函数沿着任何秩一张量方向（形如 $\mathbf{a} \otimes \mathbf{b}$ 的张量）是凸的。对于二次可微的能量函数 $w(\mathbf{F})$，秩一凸性等价于**勒让德-阿达马条件**（Legendre-Hadamard condition）。

在物理上，这一条件与增量方程的**强椭圆性**（strong ellipticity）直接相关。强椭圆性要求声学张量 $\mathbf{Q}(\mathbf{n})$ 对所有方向 $\mathbf{n}$ 都是正定的。声学张量决定了弹性波在材料中传播的速度。当材料变形到某一临界状态，导致在某个方向 $\mathbf{n}$ 上声学张量 $\mathbf{Q}(\mathbf{n})$ 失去正定性时（即出现零特征值，$\det\mathbf{Q}(\mathbf{n})=0$），强椭圆性丧失。

这一数学上的临界点标志着物理上的**分岔**（bifurcation）的开始。均匀的变形状态变得不稳定，系统可以选择进入一个新的、非均匀的变形模式。一种典型的失稳模式是**应变局部化**（strain localization），即变形集中在一个非常窄的带内，形成**剪切带**（shear band）。这个剪切带的方向与声学张量奇异的方向 $\mathbf{n}$ 相关。因此，应变能函数的凸性损失，直接预示了材料从均匀变形到发生局部化破坏等宏观失稳现象的转变 [@problem_id:2687698] [@problem_id:2687708]。