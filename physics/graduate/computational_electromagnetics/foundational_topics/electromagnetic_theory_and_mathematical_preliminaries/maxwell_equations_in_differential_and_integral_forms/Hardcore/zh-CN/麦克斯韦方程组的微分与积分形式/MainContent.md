## 引言
麦克斯韦方程组是经典电磁学的基石，它以其无与伦比的优雅和精确性，统一了电、磁和光学现象。这套方程存在两种等价但视角不同的表述：描述宏观区域行为的积分形式，和刻画时空每一点变化的微分形式。深刻理解这两种形式之间的转换、各自的物理内涵以及它们所衍生的重要概念，对于从事电磁学理论研究和工程应用的学者至关重要。然而，许多学习者在将直观的实验定律（积分形式）与抽象的偏微分方程（微分形式）联系起来时会遇到困难，对位移电流、电磁势、规范变换等高级概念的物理必要性也缺乏系统性认识。

本文旨在弥合这一知识鸿沟，为读者构建一个关于麦克斯韦方程组的完整理论框架。我们将带领读者踏上一段从基础到前沿的探索之旅，系统地梳理这套伟大方程的来龙去脉及其深远影响。在“原理与机制”一章中，我们将从基本实验定律出发，推导方程的两种形式，并深入剖析其物理意义、守恒定律和边界条件。随后，在“应用与跨学科联系”一章中，我们将展示这些基本原理如何在工程应用、计算电磁学乃至理论物理的前沿（如广义相对论和拓扑学）中发挥关键作用。最后，通过一系列精心设计的“动手实践”问题，读者将有机会亲手应用所学知识，解决具体的理论和计算挑战，从而将理论内化为自身的能力。

## 原理与机制

继前一章介绍之后，本章将深入探讨麦克斯韦方程组的物理原理与数学机制。我们将从电磁学的基本实验定律出发，推导出其积分与微分形式，并阐明这两种形式之间的深刻联系。在此基础上，我们将逐一剖析每个方程的物理内涵，引入电磁势、规范自由度和本构关系等高级概念，并最终探讨能量守恒和边界条件等重要推论。本章旨在为计算电磁学中的数值方法奠定坚实的理论基础。

### 麦克斯韦方程组的积分与微分形式

电磁学的宏伟殿堂建立在四条基本定律之上，这些定律最初由实验观测总结而来，其最自然、最直观的表述形式是积分形式。积分形式描述了电磁场在有限大小的空间区域（如体积、曲面、闭合路径）上的“全局”行为。

1.  **高斯电场定律 (Gauss's Law for Electricity):** 穿过任意闭合曲面 $S$ 的净电通量等于该曲面所包围的体积 $V$ 内的自由电荷总量 $Q_{\text{free, enc}}$。在宏观媒质中，我们使用 **电通量密度 (electric flux density)** $\mathbf{D}$ 来描述电场，其通量与自由电荷相关。数学上，这表示为：
    $$ \oint_S \mathbf{D} \cdot d\mathbf{S} = \int_V \rho \, dV $$
    其中 $\rho$ 是 **自由体电荷密度 (free volume charge density)**，单位为库仑每立方米 ($\mathrm{C/m^3}$)。

2.  **高斯磁场定律 (Gauss's Law for Magnetism):** 穿过任意闭合曲面的净磁通量恒为零。这反映了一个基本的实验事实：自然界中不存在孤立的磁单极子。我们用 **磁通量密度 (magnetic flux density)** $\mathbf{B}$ 来描述磁场，其单位为特斯拉 ($\mathrm{T}$) 或韦伯每平方米 ($\mathrm{Wb/m^2}$)。其积分形式为：
    $$ \oint_S \mathbf{B} \cdot d\mathbf{S} = 0 $$

3.  **法拉第电磁感应定律 (Faraday's Law of Induction):** 沿任意闭合回路 $C$ 的电动势（即 **电场强度 (electric field intensity)** $\mathbf{E}$ 的环路积分）等于穿过以该回路为边界的任意曲面 $S$ 的磁通量的时间变化率的负值。数学上写作：
    $$ \oint_C \mathbf{E} \cdot d\mathbf{l} = - \frac{d}{dt} \int_S \mathbf{B} \cdot d\mathbf{S} $$
    其中电场强度 $\mathbf{E}$ 的单位为伏特每米 ($\mathrm{V/m}$)。

4.  **安培-麦克斯韦定律 (Ampère-Maxwell Law):** **磁场强度 (magnetic field intensity)** $\mathbf{H}$ 沿任意闭合回路 $C$ 的环流，等于穿过以该回路为边界的任意曲面 $S$ 的自由传导电流 $I_{\text{free, enc}}$ 与电通量的时间变化率（即位移电流）之和。磁场强度 $\mathbf{H}$ 的单位为安培每米 ($\mathrm{A/m}$)。其积分形式为：
    $$ \oint_C \mathbf{H} \cdot d\mathbf{l} = \int_S \mathbf{J} \cdot d\mathbf{S} + \frac{d}{dt} \int_S \mathbf{D} \cdot d\mathbf{S} $$
    其中 $\mathbf{J}$ 是 **自由电流密度 (free current density)**，单位为安培每平方米 ($\mathrm{A/m^2}$)。

虽然积分形式在物理上直观，但在理论分析和数值计算中，描述场在空间每一点行为的微分形式通常更为方便。这两种形式的转换依赖于矢量微积分中的两个基本定理：散度定理和斯托克斯定理。这个转换过程被称为“局域化”，因为它将关于有限区域的“全局”陈述转化为关于无限小邻域的“局部”陈述 [@problem_id:3329618]。

通过对任意无限小体积 $V$ 应用 **散度定理**（$\int_V (\nabla \cdot \mathbf{F}) \, dV = \oint_{\partial V} \mathbf{F} \cdot d\mathbf{S}$），我们可以将两个高斯定律转化为微分形式。由于积分定律对任意体积均成立，被积函数必须处处相等。这一过程将积分方程的全局约束转化为微分方程的局部约束 [@problem_id:3329609]。
-   从高斯电场定律得到：
    $$ \nabla \cdot \mathbf{D} = \rho $$
-   从高斯磁场定律得到：
    $$ \nabla \cdot \mathbf{B} = 0 $$

类似地，通过对任意以闭合路径 $C$ 为边界的无限小曲面 $S$ 应用 **斯托克斯定理**（$\int_S (\nabla \times \mathbf{F}) \cdot d\mathbf{S} = \oint_{\partial S} \mathbf{F} \cdot d\mathbf{l}$），我们可以将法拉第定律和安培-麦克斯韦定律转化为微分形式。
-   从法拉第定律得到（假设曲面静止）：
    $$ \nabla \times \mathbf{E} = - \frac{\partial \mathbf{B}}{\partial t} $$
-   从安培-麦克斯韦定律得到（假设曲面静止）：
    $$ \nabla \times \mathbf{H} = \mathbf{J} + \frac{\partial \mathbf{D}}{\partial t} $$

总之，麦克斯韦方程组的微分形式精确描述了电磁场在时空每一点的瞬时行为，它们构成了经典电动力学的核心。散度 ($\nabla \cdot$) 和旋度 ($\nabla \times$) 算子可以被理解为通量密度和环流密度的点态量度，它们是通过将通量或环流除以体积或面积，并取极限到零得到的 [@problem_id:3329618]。对于非光滑场或奇异源（如点电荷），这种等价性在更广泛的分布理论意义下仍然成立，此时源项表现为狄拉克 $\delta$ 函数，进一步强化了微分形式的“局域”特性 [@problem_id:3329618]。

### 各定律的物理内涵与推论

#### 高斯磁场定律与磁矢量势

$\nabla \cdot \mathbf{B} = 0$ 是麦克斯韦方程组中最简洁的方程之一，它断言了磁场是一个无散场。其直接物理意义是磁力线总是闭合的，既无起点也无终点，这等价于声明宇宙中不存在 **磁单极子 (magnetic monopoles)**。这是从“穿过任何闭合曲面的净磁通量为零”这一“全局”观测事实通过散度定理局域化得到的结果 [@problem_id:3329579]。

矢量微积分中有一个恒等式：任意矢量场的旋度之散度恒为零，即 $\nabla \cdot (\nabla \times \mathbf{A}) = 0$。这启发我们可以引入一个辅助场——**磁矢量势 (magnetic vector potential)** $\mathbf{A}$，使得 $\mathbf{B}$ 可以表示为 $\mathbf{A}$ 的旋度：
$$ \mathbf{B} = \nabla \times \mathbf{A} $$
如此定义，$\nabla \cdot \mathbf{B} = 0$ 这一物理定律便自动得到满足。$\mathbf{A}$ 的引入极大地简化了许多理论和计算问题。然而，矢量势 $\mathbf{A}$ 并非唯一确定。对于任意标量场 $\chi(\mathbf{x}, t)$，如果我们对 $\mathbf{A}$ 做一个变换 $\mathbf{A}' = \mathbf{A} + \nabla \chi$，新的磁场 $\mathbf{B}'$ 仍然与原来的 $\mathbf{B}$ 相同，因为 $\nabla \times (\nabla \chi) = 0$。这种不唯一性被称为 **规范自由度 (gauge freedom)**，是电动力学中一个深刻且重要的概念 [@problem_id:3329579]。

从数学角度看，$\nabla \cdot \mathbf{B} = 0$ 保证了 $\mathbf{B}$ 场在拓扑上是一个“闭合2-形式”。是否存在一个全局定义的、单值的矢量势 $\mathbf{A}$（一个“精确1-形式”）则依赖于空间的拓扑性质。在如全空间 $\mathbb{R}^3$ 这样的“可缩”或“单连通”区域，这样的 $\mathbf{A}$ 总是存在的。但在具有孔洞或环柄的“多连通”区域（如移除一条线的空间），可能不存在一个全局单值的 $\mathbf{A}$。尽管如此，根据庞加莱引理，我们总可以在任何点的局部邻域内找到一个适用的矢量势 $\mathbf{A}$ [@problem_id:3329579]。

#### 法拉第定律与楞次定律

法拉第电磁感应定律的微分形式 $\nabla \times \mathbf{E} = -\partial_t \mathbf{B}$ 描述了变化的磁场如何产生电场。这种由时变磁场产生的电场是一种非保守场（涡旋场），因为它的旋度不为零，其环路积分（电动势）也不为零。

方程中的负号至关重要，它体现了 **楞次定律 (Lenz's Law)**。楞次定律指出，感应电流的方向总是使其产生的磁场反抗引起感应电流的磁通量变化 [@problem_id:3329536]。让我们通过一个思想实验来理解这一点。考虑一个空间均匀但随时间线性增长的磁场 $\mathbf{B}(t) = \beta t \hat{\mathbf{z}}$（其中 $\beta > 0$）。我们考察一个以 z 轴为中心、半径为 $r$ 的圆形回路。根据右手定则，我们选择逆时针方向为回路积分正方向，则穿过回路的磁通量为 $\Phi_B = (\beta t) (\pi r^2)$，其变化率为 $d\Phi_B/dt = \beta \pi r^2$。根据法拉第定律积分形式，感应电动势为 $\oint \mathbf{E} \cdot d\mathbf{l} = -\beta \pi r^2$。由于对称性，感应电场 $\mathbf{E}$ 必定呈圆形，大小仅与半径 $r$ 有关，即 $\mathbf{E} = E_\phi(r) \hat{\boldsymbol{\phi}}$。计算环路积分得到 $E_\phi(r) \cdot 2\pi r$。联立两式可解得 $E_\phi(r) = -(\beta/2)r$。这个负号表明，感应电场是顺时针方向的。如果回路是导体，这个顺时针的电场将驱动顺时针的电流，而顺时针的电流根据右手定则会产生一个指向 $-\hat{\mathbf{z}}$ 方向的感应磁场。这个感应磁场正好与原来磁场在 $+\hat{\mathbf{z}}$ 方向的增长相抗衡。这完美地诠释了楞次定律，它本质上是能量守恒定律在电磁感应现象中的体现 [@problem_id:3329536]。

#### 安培定律与位移电流

在静磁学中，安培定律写作 $\nabla \times \mathbf{H} = \mathbf{J}$。然而，这个形式在处理时变场时遇到了严重困难。对该方程两边取散度，由于 $\nabla \cdot (\nabla \times \mathbf{H}) \equiv 0$，我们得到 $\nabla \cdot \mathbf{J} = 0$。这个结论意味着电流密度必须是无散的，即电流线必须是闭合的。然而，物理上我们知道电荷可以积累或耗散，电荷守恒定律（连续性方程）的正确表述是 $\nabla \cdot \mathbf{J} + \partial_t \rho = 0$。只有当电荷密度不随时间变化时（$\partial_t \rho = 0$），才有 $\nabla \cdot \mathbf{J} = 0$。因此，原始的安培定律与电荷守恒定律在时变情况下是矛盾的 [@problem_id:3329566]。

麦克斯韦通过一个天才的补充解决了这个矛盾。他利用高斯定律 $\nabla \cdot \mathbf{D} = \rho$，将连续性方程改写为：
$$ \nabla \cdot \mathbf{J} = -\frac{\partial \rho}{\partial t} = -\frac{\partial}{\partial t}(\nabla \cdot \mathbf{D}) = - \nabla \cdot \left(\frac{\partial \mathbf{D}}{\partial t}\right) $$
整理后得到：
$$ \nabla \cdot \left( \mathbf{J} + \frac{\partial \mathbf{D}}{\partial t} \right) = 0 $$
这表明，虽然传导电流密度 $\mathbf{J}$ 本身不一定是无散的，但“总电流密度” $\mathbf{J}_{\text{total}} = \mathbf{J} + \partial_t \mathbf{D}$ 总是无散的。因此，正确的安培定律应该是将源项替换为这个守恒的总电流：
$$ \nabla \times \mathbf{H} = \mathbf{J} + \frac{\partial \mathbf{D}}{\partial t} $$
其中新增的项 $\mathbf{J}_d = \partial_t \mathbf{D}$ 被称为 **位移电流密度 (displacement current density)**。

位移电流的必要性也可以通过一个经典的电容器充电思想实验来直观理解 [@problem_id:3329549]。考虑一个正在充电的平行板电容器，一根导线将电流 $I(t)$ 送入其中一个极板。我们取一个环绕导线的闭合回路 $C$。根据斯托克斯定理，安培定律的积分形式 $\oint_C \mathbf{H} \cdot d\mathbf{l} = \int_S (\nabla \times \mathbf{H}) \cdot d\mathbf{S}$ 的值应与以 $C$ 为边界的具体曲面 $S$ 的选择无关。

-   如果我们选择一个简单的平面圆盘形曲面 $S_1$，它被导线刺穿。通过 $S_1$ 的传导电流积分就是 $I(t)$。
-   如果我们选择一个“袋状”曲面 $S_2$，它绕过导线，从电容器两极板之间穿过。由于极板间是绝缘的，没有传导电流穿过 $S_2$，所以传导电流积分为零。

如果安培定律中只有传导电流，那么对于同一个回路 $C$，我们会得到两个不同的结果 ($I(t)$ 和 $0$)，这是一个明显的矛盾。麦克斯韦的位移电流解决了这个问题。在电容器极板间，虽然没有传导电流，但存在着随时间变化的电场，即变化的电通量密度 $\mathbf{D}$。通过 $S_2$ 的位移电流恰好是 $\int_{S_2} (\partial_t \mathbf{D}) \cdot d\mathbf{S}$。由于电容器极板上的电荷 $Q(t)$ 与穿过极板间的电通量成正比（高斯定律），而传导电流 $I(t) = dQ/dt$，我们发现穿过 $S_2$ 的位移电流正好等于穿过 $S_1$ 的传导电流 $I(t)$。这样，对于任意曲面 $S$，总电流的通量 $\int_S (\mathbf{J} + \partial_t \mathbf{D}) \cdot d\mathbf{S}$ 都等于 $I(t)$，从而保证了安培-麦克斯韦定律的自洽性 [@problem_id:3329549] [@problem_id:3329566]。

### 电磁势、规范变换与本构关系

#### 电磁势与[规范变换](@entry_id:176521)

我们已经看到，$\nabla \cdot \mathbf{B} = 0$ 允许我们引入磁矢量势 $\mathbf{A}$ 使得 $\mathbf{B} = \nabla \times \mathbf{A}$。现在将这个定义代入法拉第定律 $\nabla \times \mathbf{E} = -\partial_t \mathbf{B}$：
$$ \nabla \times \mathbf{E} = -\frac{\partial}{\partial t}(\nabla \times \mathbf{A}) = -\nabla \times \left(\frac{\partial \mathbf{A}}{\partial t}\right) $$
整理得：
$$ \nabla \times \left( \mathbf{E} + \frac{\partial \mathbf{A}}{\partial t} \right) = 0 $$
一个旋度为零的矢量场可以表示为某个标量场的梯度。因此，我们可以定义一个 **标量势 (scalar potential)** $\phi$，使得：
$$ \mathbf{E} + \frac{\partial \mathbf{A}}{\partial t} = -\nabla \phi \quad \implies \quad \mathbf{E} = -\nabla \phi - \frac{\partial \mathbf{A}}{\partial t} $$
这样，通过引入一对势 $(\phi, \mathbf{A})$，我们便自动地满足了两个无源的麦克斯韦方程（$\nabla \cdot \mathbf{B} = 0$ 和 $\nabla \times \mathbf{E} = -\partial_t \mathbf{B}$）。

之前我们提到，$\mathbf{A}$ 的定义存在规范自由度。现在我们必须考察这个自由度对 $\phi$ 的影响。考虑一个 **规范变换 (gauge transformation)**，它由任意一个标量函数 $\chi(\mathbf{x}, t)$ 生成：
$$ \mathbf{A}' = \mathbf{A} + \nabla \chi $$
$$ \phi' = \phi - \frac{\partial \chi}{\partial t} $$
可以验证，在这个变换下，电场 $\mathbf{E}$ 和磁场 $\mathbf{B}$ 保持不变 [@problem_id:3329537]。这意味着物理场 $(\mathbf{E}, \mathbf{B})$ 并不唯一地决定势 $(\phi, \mathbf{A})$。我们可以利用这种自由度来选择一组特定的势，使它们满足的方程变得最简单。这种选择被称为 **规范固定 (gauge fixing)**。

两个最常用的规范是：
1.  **洛伦兹规范 (Lorenz Gauge):** 该规范要求势满足以下条件：
    $$ \nabla \cdot \mathbf{A} + \frac{1}{c^2} \frac{\partial \phi}{\partial t} = 0 $$
    在洛伦兹规范下，麦克斯韦方程组可以简化为关于势的一对解耦的、具有洛伦兹协变形式的非齐次波动方程：
    $$ \left(\nabla^2 - \frac{1}{c^2}\frac{\partial^2}{\partial t^2}\right)\phi = -\frac{\rho}{\varepsilon_0}, \qquad \left(\nabla^2 - \frac{1}{c^2}\frac{\partial^2}{\partial t^2}\right)\mathbf{A} = -\mu_0 \mathbf{J} $$
    这种形式在相对论和辐射问题中特别有用 [@problem_id:3329537]。值得注意的是，对于任意一组不满足洛伦兹规范的势 $(\phi, \mathbf{A})$，我们总能找到一个规范函数 $\chi$，它满足波动方程 $\nabla^2 \chi - \frac{1}{c^2}\partial_t^2 \chi = -(\nabla \cdot \mathbf{A} + \frac{1}{c^2}\partial_t \phi)$，从而将原势变换到满足洛伦兹规范的新势 [@problem_id:3329537]。

2.  **库伦规范 (Coulomb Gauge):** 该规范要求：
    $$ \nabla \cdot \mathbf{A} = 0 $$
    在此规范下，高斯定律简化为泊松方程 $\nabla^2 \phi = -\rho/\varepsilon_0$，其解是瞬时的，仿佛电荷的排布瞬间决定了整个空间的标量势。矢量势 $\mathbf{A}$ 则满足一个更复杂的耦合波动方程。库伦规范在量子力学和凝聚态物理中很常用。

#### 本构关系与媒质响应

麦克斯韦方程组本身包含四个场量（$\mathbf{E}, \mathbf{D}, \mathbf{B}, \mathbf{H}$），但只有两个独立的方程（法拉第定律和安培-麦克斯韦定律）。为了构成一个封闭的系统，我们还需要描述媒质如何响应外加电磁场的方程，即 **本构关系 (constitutive relations)**。这些关系将辅助场 $(\mathbf{D}, \mathbf{H})$ 与主场 $(\mathbf{E}, \mathbf{B})$ 联系起来。

对于简单媒质（线性、各向同性、非色散），本构关系是简单的代数关系：
$$ \mathbf{D} = \epsilon \mathbf{E}, \qquad \mathbf{B} = \mu \mathbf{H} $$
其中 $\epsilon$ 是媒质的介电常数，$\mu$ 是磁导率。

然而，在许多现实材料中，媒质的响应不是瞬时的，而是依赖于场的过去历史。这种现象被称为 **色散 (dispersion)**。对于线性、时不变、具有因果性的色散媒质，本构关系必须表示为时间上的卷积积分 [@problem_id:3329585]：
$$ \mathbf{D}(\mathbf{r},t)=\int_{-\infty}^{t}\epsilon(\mathbf{r},t-\tau)\,\mathbf{E}(\mathbf{r},\tau)\,d\tau $$
$$ \mathbf{B}(\mathbf{r},t)=\int_{-\infty}^{t}\mu(\mathbf{r},t-\tau)\,\mathbf{H}(\mathbf{r},\tau)\,d\tau $$
这里的 $\epsilon(t)$ 和 $\mu(t)$ 是时间响应函数（或称为记忆核）。**因果性 (causality)**，即响应不能发生在激励之前，要求响应函数对于负的时间变量必须为零：$\epsilon(t) = 0$ 且 $\mu(t) = 0$ 对于 $t  0$ [@problem_id:3329585]。

在频域中，卷积关系变成了简单的乘积关系 $\hat{\mathbf{D}}(\omega) = \hat{\epsilon}(\omega) \hat{\mathbf{E}}(\omega)$，其中 $\hat{\epsilon}(\omega)$ 是响应函数的时间傅里叶变换。因果性在频域中有一个深刻的数学体现：它要求复介电常数 $\hat{\epsilon}(\omega)$ 和复磁导率 $\hat{\mu}(\omega)$ 在复频率平面的上半平面是解析函数。这一解析性导致其实部和虚部之间通过 **克拉默斯-克勒尼希关系 (Kramers-Kronig relations)** 相互关联，即它们是一对希尔伯特变换。此外，对于无源媒质，能量守恒要求对于正的实频率 $\omega \ge 0$，$\hat{\epsilon}(\omega)$ 和 $\hat{\mu}(\omega)$ 的虚部必须是非负的，这代表了媒质的能量耗散 [@problem_id:3329585]。

### 物理推论与应用

#### 能量守恒与坡印亭定理

麦克斯韦方程组的一个重要推论是电磁场的能量守恒定律，即 **坡印亭定理 (Poynting's Theorem)**。通过对两个旋度方程进行适当的矢量运算，可以推导出如下的微分形式能量平衡方程 [@problem_id:3329575]：
$$ \frac{\partial u_{em}}{\partial t} + \nabla \cdot \mathbf{S} = - \mathbf{J} \cdot \mathbf{E} $$
其中：
-   $u_{em} = \frac{1}{2}(\mathbf{E} \cdot \mathbf{D} + \mathbf{H} \cdot \mathbf{B})$ 是 **电磁场能量密度**，代表单位体积内存储的电场能和磁场能。
-   $\mathbf{S} = \mathbf{E} \times \mathbf{H}$ 是 **坡印亭矢量 (Poynting vector)**，代表单位时间通过单位面积的能量流密度，即功率流密度。
-   $\mathbf{J} \cdot \mathbf{E}$ 是 **功率耗散密度**，代表电场对电流做功的速率。如果电流是传导电流 $\mathbf{J}_c = \sigma \mathbf{E}$，则该项为 $\sigma |\mathbf{E}|^2$，代表焦耳热耗散。如果电流是外部电源提供的驱动电流 $\mathbf{J}_i$，则该项代表电源与电磁场之间的能量交换。

对上式在一个体积 $V$ 内积分，并应用散度定理，我们得到积分形式的坡印亭定理：
$$ \frac{d}{dt} \int_V u_{em} \, dV + \oint_{\partial V} \mathbf{S} \cdot d\mathbf{S} = - \int_V \mathbf{J} \cdot \mathbf{E} \, dV $$
该方程的物理解释是 [@problem_id:3329575]：
$$ \text{（体积V内总电磁能的增加率）} + \text{（通过边界}\partial V\text{向外流出的总功率）} = \text{（体积V内源向场提供的总功率）} $$
其中，右侧的源项是负的 $\mathbf{J} \cdot \mathbf{E}$ 积分，代表场对电流做功的功率。坡印亭定理是电磁学中的能量守恒定律，它在验证数值算法的稳定性和准确性方面起着至关重要的作用。

#### 边界条件

在计算电磁学中，我们经常处理不同媒质的交界面。麦克斯韦方程组的积分形式特别适合于推导电磁场在这些界面上的 **边界条件 (boundary conditions)**。通过在界面上构建一个厚度趋于零的“扁平药盒”和一个高度趋于零的“窄长回路”，我们可以从积分定律得到场的法向和切向分量应满足的关系 [@problem_id:3329614]。

1.  **法向分量：**
    -   对高斯电场定律应用“药盒”论证，得到电通量密度的法向分量在界面上的跳变等于自由面电荷密度 $\rho_s$：
        $$ \hat{\mathbf{n}} \cdot (\mathbf{D}_2 - \mathbf{D}_1) = \rho_s $$
    -   对高斯磁场定律应用“药盒”论证，得到磁通量密度的法向分量总是连续的：
        $$ \hat{\mathbf{n}} \cdot (\mathbf{B}_2 - \mathbf{B}_1) = 0 $$

2.  **切向分量：**
    -   对法拉第定律应用“窄长回路”论证，得到电场强度的切向分量总是连续的（假设没有磁面电流）：
        $$ \hat{\mathbf{n}} \times (\mathbf{E}_2 - \mathbf{E}_1) = 0 $$
    -   对安培-麦克斯韦定律应用“窄长回路”论证，得到磁场强度的切向分量在界面上的跳变等于自由面电流密度 $\mathbf{J}_s$：
        $$ \hat{\mathbf{n}} \times (\mathbf{H}_2 - \mathbf{H}_1) = \mathbf{J}_s $$

作为一个具体应用，考虑一个无限薄的、具有表面电导率 $\sigma_s$ 的电阻片置于 $z=0$ 平面。根据欧姆定律，表面电流密度与切向电场成正比：$\mathbf{J}_s = \sigma_s \mathbf{E}_t$。由于电场的切向分量连续（$\mathbf{E}_{t1} = \mathbf{E}_{t2} = \mathbf{E}_t$），磁场的切向边界条件变为 $\hat{\mathbf{z}} \times (\mathbf{H}_2 - \mathbf{H}_1) = \sigma_s \mathbf{E}_t$。这个条件是解决涉及薄导电层（如石墨烯、频率选择表面）的电磁散射问题的关键 [@problem_id:3329614]。

本章概述的这些原理和机制构成了我们理解和模拟电磁现象的基石。在后续章节中，我们将看到这些方程如何被离散化，并转化为可由计算机求解的代数系统。