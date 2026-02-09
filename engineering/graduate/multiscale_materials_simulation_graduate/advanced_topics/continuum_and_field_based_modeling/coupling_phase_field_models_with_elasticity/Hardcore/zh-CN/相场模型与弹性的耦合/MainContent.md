## 引言
在材料科学与工程领域，微观结构是决定材料宏观性能的关键。相场模型作为一种强大的介观尺度模拟工具，能够生动地描述相变和微观结构的复杂演化过程。然而，在许多固态系统中，相变常常伴随着晶格参数的变化，从而产生显著的内应力。这些弹性效应能够深刻地影响相变的驱动力、动力学路径和最终的结构形貌。因此，若要准确预测和设计高性能材料，简单地考虑化学驱动力是远远不够的，必须将相场模型与弹性力学进行耦合。

本文旨在系统性地介绍耦合相场模型与弹性力学的核心理论与实践。通过学习本文，读者将能够理解弹性效应如何从根本上融入相场模型的热力学与动力学框架，并掌握其在解决前沿材料问题中的应用。

文章将分为三个主要部分展开：第一部分，“原理与机制”，将深入剖析耦合的物理基础，从本征应变的概念出发，构建严谨的热力学和力学框架。第二部分，“应用与交叉学科联系”，将通过一系列实例展示该耦合模型在固态相变、断裂力学、薄膜技术等领域的强大应用价值。最后，在“动手实践”部分，我们将引导读者思考如何将理论转化为计算实践，解决具体的建模与求解问题。现在，让我们从探究耦合模型的核心原理与机制开始。

## 原理与机制

在上一章引言的基础上，本章深入探讨将相场模型与弹性力学耦合所需的核心原理与关键机制。我们将从引入核心概念“本征应变”开始，系统地构建一个将微观晶格变化与宏观力学行为联系起来的热力学和力学框架。随后，我们将阐明这种耦合如何产生内应力、驱动界面演化，并最终决定材料在介观尺度上的微观结构形貌。本章旨在为读者提供一个坚实、自洽的理论基础，以便理解和应用耦合了弹性的相场模型。

### 弹性耦合的核心：本征应变

在固态相变过程中，材料内部的微观结构变化，如成分变化或晶体结构转变，通常会伴随着晶格参数的改变。如果我们将一小块正在发生相变的材料从其周围的基体中“切”出来，它会自由变形到一个新的、无应力的形状和尺寸。这种理想化的、无约束下的变形，就是**本征应变（eigenstrain）**或**无应力转变应变（stress-free transformation strain）**，我们用符号 $\boldsymbol{\varepsilon}^{0}$ 表示。

在连续介质力学框架下，材料的总应变 $\boldsymbol{\varepsilon}$ 被认为是可加性分解的。它由两部分构成：一部分是材料为了适应本征应变和外部约束而产生的**弹性应变（elastic strain）** $\boldsymbol{\varepsilon}^{\mathrm{el}}$，另一部分就是本征应变 $\boldsymbol{\varepsilon}^{0}$ 本身。

$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{\mathrm{el}} + \boldsymbol{\varepsilon}^{0}
$$

这两种应变具有截然不同的物理意义 [@problem_id:3799014]。**本征应变** $\boldsymbol{\varepsilon}^{0}$ 是由材料内部状态（如相场序参量 $\phi$）决定的“理想”或“目标”应变。它本身不直接产生应力。相反，**弹性应变** $\boldsymbol{\varepsilon}^{\mathrm{el}} = \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{0}$ 代表了实际总应变 $\boldsymbol{\varepsilon}$ 与理想本征应变 $\boldsymbol{\varepsilon}^{0}$ 之间的“失配”或“不匹配”。正是这种失配使得晶格发生弹性畸变，从而产生内应力并储存弹性能。根据胡克定律，柯西应力张量 $\boldsymbol{\sigma}$ 与弹性应变成正比：

$$
\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}^{\mathrm{el}} = \mathbb{C} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{0})
$$

其中 $\mathbb{C}$ 是四阶弹性刚度张量。

本征应变与相场变量 $\phi$ 之间的关系（即耦合函数 $\boldsymbol{\varepsilon}^{0}(\phi)$）是模型的关键本构关系。最简单和最常见的形式之一是线性耦合。例如，考虑一个由于成分变化导致晶格常数 $a$ 发生变化的场景。若晶格常数与序参量 $\phi$ 呈线性关系，$a(\phi) = a_{\mathrm{ref}}(1+\chi \phi)$，其中 $a_{\mathrm{ref}}$ 是参考晶格常数，$\chi$ 是耦合系数（通常称为化学膨胀系数）。对于各向同性材料，这会导致一个纯体积的、各向同性的本征应变 [@problem_id:3798987]：

$$
\boldsymbol{\varepsilon}^{0}(\phi) = \frac{a(\phi) - a_{\mathrm{ref}}}{a_{\mathrm{ref}}} \mathbf{I} = (\chi \phi) \mathbf{I}
$$

其中 $\mathbf{I}$ 是二阶单位张量。这种形式描述了当 $\phi$ 从 $0$ 变为 $1$ 时，材料在所有方向上都希望均匀膨胀或收缩的趋势。更一般地，对于具有特定晶体对称性的相变（例如从立方相到四方相），本征应变张量 $\boldsymbol{\varepsilon}^{0}$ 将具有更复杂的非对角形式，以反映相变的剪切分量。

### 弹性能与热力学框架

将弹性效应纳入相场模型的总自由能中，需要一个严谨的热力学框架。对于一个经历相变的可变形固体，其亥姆霍兹自由能密度 $\psi$ 通常包含化学能、梯度能和弹性能三个部分。总自由能 $F$ 是在整个系统体积 $\Omega$ 上的积分：

$$
F[\phi, \mathbf{u}] = \int_{\Omega} \left( f_{\mathrm{chem}}(\phi) + \frac{\kappa}{2} |\nabla \phi|^2 + \psi_{\mathrm{el}}(\phi, \boldsymbol{\varepsilon}(\mathbf{u})) \right) dV
$$

其中 $\mathbf{u}$ 是位移场，总应变 $\boldsymbol{\varepsilon}$ 由位移场的梯度导出，$\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^{\top})$。

弹性能密度 $\psi_{\mathrm{el}}$ 的表达式必须与热力学第二定律和材料稳定性原理相符 [@problem_id:3799018]。热力学稳定性要求，在任何给定的内部状态（固定的 $\phi$）下，亥姆霍兹自由能必须有下界，并且在平衡态处达到严格的局部最小值。对于弹性体，无应力状态（即 $\boldsymbol{\varepsilon}^{\mathrm{el}}=\mathbf{0}$，或 $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^0$）是其能量最低的平衡态。因此，弹性能密度必须是弹性应变 $\boldsymbol{\varepsilon}^{\mathrm{el}}$ 的一个正定二次型函数。这确保了任何偏离无应力状态的弹性变形都会增加系统的能量。其标准形式为：

$$
\psi_{\mathrm{el}} = \frac{1}{2} \boldsymbol{\varepsilon}^{\mathrm{el}} : \mathbb{C} : \boldsymbol{\varepsilon}^{\mathrm{el}} = \frac{1}{2} (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{0}) : \mathbb{C} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{0})
$$

**正定性**要求对于任何非零的对称张量 $\mathbf{E}$，二次型 $\mathbf{E} : \mathbb{C} : \mathbf{E}$ 必须大于零。这对弹性刚度张量 $\mathbb{C}$ 施加了严格的数学约束。例如，对于各向同性材料，其弹性行为由拉梅参数 $\lambda$ 和 $\mu$（或等价地，体弹模量 $K$ 和剪切模量 $\mu$）描述。正定性条件等价于要求剪切模量和体弹模量均为正值 [@problem_id:3799018]：

$$
\mu > 0 \quad \text{和} \quad K = \lambda + \frac{2}{3}\mu > 0
$$

这些条件保证了材料在受到剪切或静水压力时能够抵抗变形并储存能量，从而维持力学稳定性。如果这些条件不满足，材料将会在微小的扰动下无限变形，这是非物理的。

### 机械平衡及其力学后果

在相场演化的每个瞬间，材料的力学场（位移、应变和应力）被认为处于**机械平衡状态**。这意味着在给定相场分布 $\phi(\mathbf{x})$ 的情况下，力学场会瞬时调整以最小化弹性能，满足平衡方程 $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$（在没有体力的情况下）。这个平衡过程是理解弹性效应如何体现的关键。

#### 应变协调性与内应力的起源

内应力的产生与一个深刻的几何概念——**应变协调性（strain compatibility）**——紧密相关 [@problem_id:3799062]。在连续介质中，总应变场 $\boldsymbol{\varepsilon}(\mathbf{x})$ 是由一个连续、单值的位移场 $\mathbf{u}(\mathbf{x})$ 导出的。这个几何约束意味着 $\boldsymbol{\varepsilon}(\mathbf{x})$ 的六个分量不是独立的，它们必须满足一组偏微分方程，即圣维南协调性条件。我们可以用一个算子 $\operatorname{inc}$ 来表示这个条件，$\operatorname{inc}\boldsymbol{\varepsilon} = \mathbf{0}$ 意味着应变场是协调的。

现在考虑应变分解 $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{\mathrm{el}} + \boldsymbol{\varepsilon}^{0}$。由于 $\operatorname{inc}$ 是一个线性算子，我们有：

$$
\operatorname{inc}\boldsymbol{\varepsilon} = \operatorname{inc}\boldsymbol{\varepsilon}^{\mathrm{el}} + \operatorname{inc}\boldsymbol{\varepsilon}^{0} = \mathbf{0}
$$

这导致一个至关重要的关系：

$$
\operatorname{inc}\boldsymbol{\varepsilon}^{\mathrm{el}} = -\operatorname{inc}\boldsymbol{\varepsilon}^{0}
$$

这个方程的物理意义是：如果本征应变场 $\boldsymbol{\varepsilon}^{0}(\mathbf{x})$ 在空间上是不均匀的，它自身很可能是不协调的（即 $\operatorname{inc}\boldsymbol{\varepsilon}^{0} \neq \mathbf{0}$）。例如，想象一个由不同尺寸的砖块砌成的墙，砖块间的缝隙是不可避免的。为了维持材料的连续性（即一个协调的总应变场 $\boldsymbol{\varepsilon}$），弹性应变场 $\boldsymbol{\varepsilon}^{\mathrm{el}}$ 必须产生一个与之大小相等、符号相反的“不协调性”。一个不协调的弹性应变场必然是一个非零的场，从而导致非零的内应力场 $\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\varepsilon}^{\mathrm{el}}$。因此，**不均匀的本征应变场是内应力的根源**。

#### 边界条件的极端情况

我们可以通过两个假想的极端边界条件来具体理解弹性能的储存机制 [@problem_id:3798987]。考虑一个发生均匀相变（$\phi$ 在整个体积内恒定）的物体，其本征应变为 $\boldsymbol{\varepsilon}^0 = \epsilon_0 \mathbf{I}$。

1.  **完全夹持（Clamped）边界条件**：假设物体被刚性夹具固定，不允许任何宏观变形，即总应变 $\boldsymbol{\varepsilon} = \mathbf{0}$。在这种情况下，弹性应变为 $\boldsymbol{\varepsilon}^{\mathrm{el}} = \mathbf{0} - \boldsymbol{\varepsilon}^0 = -\epsilon_0 \mathbf{I}$。物体内部试图膨胀但被阻止，从而产生一个压应力。对于各向同性材料，这个应力是一个静水压应力 $\boldsymbol{\sigma} = -3K \epsilon_0 \mathbf{I}$，其中 $K$ 是体弹模量。相应的弹性能密度为 $\psi_{\mathrm{el}} = \frac{9}{2} K \epsilon_0^2$。

2.  **无约束（Traction-free）边界条件**：假设物体完全自由，不受任何外力。由于本征应变是均匀的，物体可以通过一个均匀的变形来完全适应它。总应变将恰好等于本征应变，$\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^0$。这意味着弹性应变 $\boldsymbol{\varepsilon}^{\mathrm{el}} = \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^0 = \mathbf{0}$。因此，系统内部的应力为零，储存的弹性能也为零 [@problem_id:3799062]。

这个对比清晰地表明，弹性能的储存并非来自本征应变本身，而是来自系统的几何约束（包括内部的协调性约束和外部的边界约束）阻止了本征应变的自由实现。

#### 相干界面处的力学条件

在两相材料中，界面是典型的本征应变不均匀区域。对于**相干界面（coherent interface）**，两侧的晶格保持完美的连续性，没有位错等缺陷。这意味着穿过界面的位移场 $\mathbf{u}$ 必须是连续的。此外，根据牛顿第三定律，界面两侧的力必须平衡，这导致**牵引力连续（traction continuity）**条件。在一个 sharp-interface 图像中，这些条件表示为跳跃条件 $[[\mathbf{u}]] = \mathbf{0}$ 和 $[[\boldsymbol{\sigma} \cdot \mathbf{n}]] = \mathbf{0}$，其中 $\mathbf{n}$ 是界面法向量。在相场模型中，界面是弥散的，这些条件是自动满足的。例如，机械平衡方程 $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$ 在整个区域（包括界面）都成立，这自然就保证了牵引力的连续性 [@problem_id:3799054]。

### 反馈回路：弹性如何驱动相演化

到目前为止，我们讨论了相场如何通过本征应变影响力学场。然而，这是一个双向耦合：力学场反过来也会影响相场的演化。这种反馈是驱动微观结构形成的关键。

在非守恒（Allen-Cahn）动力学中，相场演化由变分导数驱动：$\partial\phi/\partial t \propto -\delta F/\delta \phi$。$\delta F/\delta \phi$ 是总自由能的变分导数，可以被视为相变的“热力学驱动力”。我们可以将这个驱动力分解为化学部分和弹性部分。弹性对相演化的驱动力 $g_{\mathrm{el}}$ 定义为：

$$
g_{\mathrm{el}} = -\frac{\delta F_{\mathrm{el}}}{\delta \phi}
$$

其中 $F_{\mathrm{el}} = \int \psi_{\mathrm{el}} dV$ 是总弹性能。计算这个变分导数需要小心，因为它涉及到对 $\phi$ 的显式和隐式依赖（通过位移场 $\mathbf{u}$）。然而，一个基于虚功原理的重要结果（类似于 Hellmann-Feynman 定理）表明，在机械平衡条件下，由 $\mathbf{u}$ 对 $\phi$ 的隐式依赖产生的项恰好为零 [@problem_id:3799014]。因此，我们可以通过仅对 $\psi_{\mathrm{el}}$ 中 $\phi$ 的显式依赖项求导来得到驱动力：

$$
g_{\mathrm{el}} = \boldsymbol{\sigma} : \frac{\partial \boldsymbol{\varepsilon}^{0}}{\partial \phi} - \frac{1}{2} (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{0}) : \frac{\partial \mathbb{C}}{\partial \phi} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{0})
$$

这个表达式有两个主要的物理贡献 [@problem_id:3799014]：
1.  **$\boldsymbol{\sigma} : \partial\boldsymbol{\varepsilon}^{0}/\partial\phi$**：这一项被称为**化学应力（chemical stress）**项或**结构应力（structural stress）**项。它代表了在当前应力状态 $\boldsymbol{\sigma}$ 下，材料发生微小相变（即 $\phi$ 发生微小变化，导致本征应变变化 $\partial\boldsymbol{\varepsilon}^{0}/\partial\phi$）时所做的机械功。如果这个功是正的（例如，在压应力下发生体积缩小的相变），它将促进相变，从而降低系统总能量。
2.  **$-\frac{1}{2} \boldsymbol{\varepsilon}^{\mathrm{el}} : (\partial\mathbb{C}/\partial\phi) : \boldsymbol{\varepsilon}^{\mathrm{el}}$**：这一项仅在弹性常数依赖于相场变量 $\phi$ 时（即**弹性非均匀性**）出现。它描述了在给定的弹性应变下，系统倾向于转变为弹性更“软”或更“硬”的相的趋势，以进一步降低储存的弹性能。

相变的稳定性不仅取决于驱动力的符号，还取决于自由能形貌的曲率。弹性能对总自由能形貌的贡献可以通过计算能量对 $\phi$ 的二阶导数来量化。在一个简单的均匀夹持系统中，若本征应变与 $\phi$ 呈线性关系 $\boldsymbol{\varepsilon}^0_{ij} = \alpha \phi A_{ij}$，则弹性能对能量曲率的贡献（单位体积）为 $\alpha^2 A_{ij}C_{ijkl}A_{kl}$ [@problem_id:3798986]。这是一个正值，意味着弹性效应总是倾向于“钉扎”相场，增加相变的能量势垒，从而起到稳定作用。

### 介观形貌与组织形成：长程弹性相互作用

弹性相互作用最显著的特征是其**长程性**，这使其在决定介观尺度（远大于原子尺度）的微观结构形貌方面扮演着至关重要的角色。

#### Khachaturyan 微观弹性理论

为了分析弹性对大尺度结构形成的影响，直接处理耦合的 $\phi$ 和 $\mathbf{u}$ 场非常复杂。**Khachaturyan 微观弹性理论**提供了一个强大的数学工具，它通过在**傅里叶空间**中求解机械平衡方程，将位移场 $\mathbf{u}$ 的贡献精确地“积分掉” [@problem_id:3799052] [@problem_id:3799003]。

其核心思想是，在傅里叶空间中，机械平衡方程 $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$ 变成一个关于位移傅里叶系数 $\hat{\mathbf{u}}(\mathbf{k})$ 的代数方程。求解这个方程可以将 $\hat{\mathbf{u}}(\mathbf{k})$ 表示为本征应变傅里叶系数 $\hat{\boldsymbol{\varepsilon}}^0(\mathbf{k})$ 的函数，而后者又与相场傅里叶系数 $\hat{\phi}(\mathbf{k})$ 直接相关。将这个解代回弹性能表达式，最终得到的弹性能完全用相场变量 $\phi$ 表示：

$$
F_{\mathrm{el}}[\phi] = \frac{1}{2} \int \hat{\phi}(\mathbf{k}) B(\hat{\mathbf{k}}) \hat{\phi}(-\mathbf{k}) \frac{d\mathbf{k}}{(2\pi)^3}
$$

这里的 $B(\hat{\mathbf{k}})$ 是一个仅依赖于波矢方向 $\hat{\mathbf{k}} = \mathbf{k}/|\mathbf{k}|$ 而不依赖其大小的**弹性核函数**。在实空间中，这种傅里叶空间中的乘积形式对应于一个卷积积分，代表了一种**长程相互作用**。该相互作用势在实空间中通常随距离 $r$ 按 $1/r^3$ 的规律衰减，类似于偶极-偶极相互作用 [@problem_id:3799052]。这与梯度能所代表的短程相互作用（仅限于近邻）形成鲜明对比。

#### 弹性各向异性的作用

弹性核函数 $B(\hat{\mathbf{k}})$ 的方向依赖性是理解微观结构择优取向的关键。这个方向依赖性源于晶体**弹性刚度张量 $\mathbb{C}$ 的各向异性** [@problem_id:3799003]。

-   对于一个**弹性各向同性**的材料，如果其本征应变也是各向同性的（纯体积膨胀），那么弹性核 $B(\hat{\mathbf{k}})$ 是一个与方向无关的常数 $\lambda$。在这种情况下，弹性效应会抑制相分离（因为它总是一个正的能量惩罚项），但不会导致任何特定的结构取向 [@problem_id:3799052]。
-   对于一个**弹性各向异性**的材料（如大多数晶体），$\mathbb{C}$ 在不同晶向上的值不同。这导致 $B(\hat{\mathbf{k}})$ 的值依赖于波矢 $\mathbf{k}$ 的方向。通常，在某些“软”的晶体学方向上，$B(\hat{\mathbf{k}})$ 的值会达到最小。

#### 调幅分解与定向粗化

在发生调幅分解（spinodal decomposition）的合金中，这种弹性各向异性效应表现得尤为突出。线性稳定性分析表明，成分波的增长率 $\omega(\mathbf{k})$ 包含弹性核的贡献 [@problem_id:3799052]：

$$
\omega(\mathbf{k}) = -M |\mathbf{k}|^2 \left( f''(\phi_0) + \kappa |\mathbf{k}|^2 + B(\hat{\mathbf{k}}) \right)
$$

其中 $M$ 是迁移率，$f''(\phi_0)  0$ 是发生分解的化学驱动力。为了使增长率 $\omega(\mathbf{k})$ 最大化，系统会自发地选择那些使弹性惩罚项 $B(\hat{\mathbf{k}})$ 最小的波矢方向 $\hat{\mathbf{k}}$。因此，新相的析出物（例如，沉淀相）将倾向于沿着这些弹性软方向排列和生长，形成具有特定取向的板状或针状结构。这就是**定向粗化（directional coarsening）**的物理根源。

在一个简化的各向同性模型中，其中 $B(\hat{\mathbf{k}})=\lambda$ 为常数，我们可以清晰地看到化学驱动力（由 $a=f''(\phi_0)$ 表示）、梯度能（$\kappa$）和弹性能（$\lambda$）之间的竞争。只有当化学驱动力足够强以克服弹性能的稳定化效应时（即 $a+\lambda  0$），相分离才会发生。不稳定的波矢范围由一个截止波矢 $k_c$ 界定，其值为 $k_c = \sqrt{-(a+\lambda)/\kappa}$ [@problem_id:3799010]。

### 变分原理与边界条件：形式化框架

最后，我们必须关注整个耦合问题的数学框架，特别是如何处理不同的力学边界条件。这涉及到选择合适的热力学势和变分原理 [@problem_id:3799057]。

在一个等温系统中，平衡态由某个热力学势的最小值（或驻点）给出。该势的选择取决于施加在系统边界上的约束。

1.  **固定位移（狄利克雷）边界条件**：如果系统边界 $\partial\Omega$ 的一部分 $\Gamma_D$ 被施加了固定的位移 $\mathbf{u} = \overline{\mathbf{u}}$，这对应于一个**正则系统（canonical ensemble）**。在这种情况下，我们寻找的平衡态是使系统的**亥姆霍兹自由能 $F[\phi, \mathbf{u}]$** 最小化的解，同时满足位移约束。没有额外的边界功项需要被添加到泛函中。

2.  **固定牵引力（诺伊曼）边界条件**：如果系统边界的一部分 $\Gamma_N$ 被施加了固定的牵引力 $\mathbf{t} = \overline{\mathbf{t}}$，这对应于一个**吉布斯型系统（Gibbs-type ensemble）**。在这种情况下，外力会对系统做功。为了找到平衡态，我们需要最小化一个包含了外力势能的总势能 $\Pi$。这个总势能是亥姆霍兹自由能 $F$ 减去外力所做的功：

    $$
    \Pi[\phi, \mathbf{u}] = F[\phi, \mathbf{u}] - \int_{\Gamma_N} \overline{\mathbf{t}} \cdot \mathbf{u} \, d\Gamma
    $$

    从热力学角度看，从 $F$ 到 $\Pi$ 的转变是一个关于边界共轭变量对（边界位移 $\mathbf{u}|_{\Gamma_N}$ 和边界牵引力 $\mathbf{t}$）的**勒让德变换（Legendre transform）**。

3.  **混合边界条件**：在最一般的情况下，边界同时包含固定位移部分 $\Gamma_D$ 和固定牵引力部分 $\Gamma_N$。相应的变分原理是前两者的结合：我们需要最小化总势能 $\Pi = F[\phi, \mathbf{u}] - \int_{\Gamma_N} \overline{\mathbf{t}} \cdot \mathbf{u} \, d\Gamma$，并在求解过程中强制满足在 $\Gamma_D$ 上的位移约束 $\mathbf{u} = \overline{\mathbf{u}}$。

正确地建立变分框架对于模型的理论自洽性和数值实现（例如，在有限元方法中）都至关重要。它确保了模型的解在物理上是能量最小化的稳定态，并且正确地反映了外部力学环境对相变过程的影响。