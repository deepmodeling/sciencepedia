## 引言
在电磁理论中，引入[标量势](@entry_id:276177) $\phi$ 与矢量势 $\mathbf{A}$ 是求解麦克斯韦方程组的一种强大技巧，它能自动满足其中两个[齐次方程](@entry_id:163650)。然而，这种表示方法也带来了一个固有的自由度——[规范不变性](@entry_id:137857)，即存在无穷多组不同的势 $(\phi, \mathbf{A})$ 可以描述完全相同的物理电场和磁场。这种不唯一性给理论分析和数值求解带来了挑战：我们应该选择哪一组势？

为了解决这一问题，必须施加一个额外的数学约束，即“[规范条件](@entry_id:749730)”或“[规范固定](@entry_id:142821)”。本文将深入探讨两种最基本且应用最广泛的规范选择：[洛伦兹规范](@entry_id:153650)和[库仑规范](@entry_id:273044)。我们将系统地剖析它们背后的物理原理，比较它们各自的优势与局限，并展示它们如何在现代[计算电磁学](@entry_id:265339)中发挥关键作用。

在接下来的内容中，读者将首先在“原理与机制”一章中学习两种规范的数学定义、它们如何解耦麦克斯韦方程，以及规范变换的本质。随后，在“应用与跨学科联系”一章中，我们将通过理论物理和[计算电磁学](@entry_id:265339)中的具体实例，展示如何根据问题特性（如相对论效应、[准静态近似](@entry_id:264812)）战略性地选择规范。最后，“动手实践”部分将提供具体的编程练习，帮助读者将理论知识转化为解决实际问题的能力。通过这趟旅程，您将深刻理解规范选择为何不仅是数学上的便利，更是优化物理建模与数值仿真的核心策略。

## 原理与机制

在电磁学领域，标量势 $\phi$ 和矢量势 $\mathbf{A}$ 的引入极大地简化了[麦克斯韦方程组](@entry_id:150940)的求解。通过定义 $\mathbf{B} = \nabla \times \mathbf{A}$ 和 $\mathbf{E} = -\nabla \phi - \frac{\partial \mathbf{A}}{\partial t}$，[磁场](@entry_id:153296)的高斯定律 $\nabla \cdot \mathbf{B} = 0$ 和[法拉第感应定律](@entry_id:146175) $\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$ 自动得到满足。然而，这种表示方式引入了一个新的自由度，即[规范不变性](@entry_id:137857)。本章将深入探讨这一原理，并详细阐述两种最常用的规范选择——[洛伦兹规范](@entry_id:153650)和[库仑规范](@entry_id:273044)——的内在机制及其在[计算电磁学](@entry_id:265339)中的深刻影响。

### [规范不变性](@entry_id:137857)原理

势 $(\phi, \mathbf{A})$ 的引入并非唯一。考虑一个任意的、足够光滑的标量函数 $\chi(\mathbf{r}, t)$，我们可以对势进行如下变换：
$$
\mathbf{A}' = \mathbf{A} + \nabla \chi, \qquad \phi' = \phi - \frac{\partial \chi}{\partial t}
$$
这个变换被称为**规范变换**。令人惊讶的是，物理场 $\mathbf{E}$ 和 $\mathbf{B}$ 在此变换下保持不变。我们可以通过直接计算来验证这一点：
$$
\mathbf{B}' = \nabla \times \mathbf{A}' = \nabla \times (\mathbf{A} + \nabla \chi) = \nabla \times \mathbf{A} + \nabla \times (\nabla \chi) = \mathbf{B}
$$
因为任意标量函数的[梯度的旋度](@entry_id:274168)恒为零。同样地，对于[电场](@entry_id:194326)：
$$
\mathbf{E}' = -\nabla \phi' - \frac{\partial \mathbf{A}'}{\partial t} = -\nabla \left(\phi - \frac{\partial \chi}{\partial t}\right) - \frac{\partial}{\partial t}(\mathbf{A} + \nabla \chi) = \left(-\nabla \phi - \frac{\partial \mathbf{A}}{\partial t}\right) + \nabla\left(\frac{\partial \chi}{\partial t}\right) - \frac{\partial}{\partial t}(\nabla \chi) = \mathbf{E}
$$
因为时间和空间[偏导数](@entry_id:146280)的次序可以交换。

这种对于任意函数 $\chi$ 的不变性，被称为**规范不变性**（gauge invariance），它意味着对于给定的物理场，存在无限多组可能的[电磁势](@entry_id:266145)。为了从这个无限大的可能性空间中选择一个确定的、便于求解的势，我们必须施加一个额外的约束条件。这个约束条件就是**[规范条件](@entry_id:749730)**（gauge condition）或**[规范固定](@entry_id:142821)**（gauge fixing）。一个[规范条件](@entry_id:749730)有效地“固定”了自由度，使得势的求解过程变得明确。[@problem_id:3325787]

### [洛伦兹规范](@entry_id:153650)：相对论协变的选择

最著名和最广泛使用的[规范条件](@entry_id:749730)之一是**[洛伦兹规范](@entry_id:153650)**（Lorenz gauge）。它由丹麦物理学家 Ludvig Lorenz 提出，其数学形式为：
$$
\nabla \cdot \mathbf{A} + \frac{1}{c^2} \frac{\partial \phi}{\partial t} = 0
$$
其中 $c = 1/\sqrt{\mu_0\varepsilon_0}$ 是[真空中的光速](@entry_id:272753)。这个看似简单的附加条件，却带来了巨大的理论和计算上的便利。

为了理解其作用，我们将势的定义代入另外两个麦克斯韦方程。由高斯定律 $\nabla \cdot \mathbf{E} = \rho / \varepsilon_0$ 可得：
$$
\nabla \cdot \left(-\nabla \phi - \frac{\partial \mathbf{A}}{\partial t}\right) = \frac{\rho}{\varepsilon_0} \implies \nabla^2 \phi + \frac{\partial}{\partial t}(\nabla \cdot \mathbf{A}) = -\frac{\rho}{\varepsilon_0}
$$
由[安培-麦克斯韦定律](@entry_id:266368) $\nabla \times \mathbf{B} = \mu_0 \mathbf{J} + \mu_0 \varepsilon_0 \frac{\partial \mathbf{E}}{\partial t}$ 可得：
$$
\nabla \times (\nabla \times \mathbf{A}) = \mu_0 \mathbf{J} + \mu_0 \varepsilon_0 \frac{\partial}{\partial t}\left(-\nabla \phi - \frac{\partial \mathbf{A}}{\partial t}\right)
$$
利用矢量恒等式 $\nabla \times (\nabla \times \mathbf{A}) = \nabla(\nabla \cdot \mathbf{A}) - \nabla^2 \mathbf{A}$ 并整理后得到：
$$
(\nabla^2 \mathbf{A} - \frac{1}{c^2}\frac{\partial^2 \mathbf{A}}{\partial t^2}) - \nabla\left(\nabla \cdot \mathbf{A} + \frac{1}{c^2}\frac{\partial \phi}{\partial t}\right) = -\mu_0 \mathbf{J}
$$
在没有施加[规范条件](@entry_id:749730)时，$\phi$ 和 $\mathbf{A}$ 的方程是耦合在一起的，求解非常困难。然而，一旦我们施加[洛伦兹规范](@entry_id:153650)条件，上式括号中的项恰好为零。同时，将 $\nabla \cdot \mathbf{A} = -\frac{1}{c^2} \frac{\partial \phi}{\partial t}$ 代入 $\phi$ 的方程中，我们得到了一组优美、对称且解耦的[方程组](@entry_id:193238)：
$$
\nabla^2 \phi - \frac{1}{c^2}\frac{\partial^2 \phi}{\partial t^2} = -\frac{\rho}{\varepsilon_0}
$$
$$
\nabla^2 \mathbf{A} - \frac{1}{c^2}\frac{\partial^2 \mathbf{A}}{\partial t^2} = -\mu_0 \mathbf{J}
$$
这两者都是标准的**非齐次波方程**。它们表明，在[洛伦兹规范](@entry_id:153650)下，标量势 $\phi$ 由[电荷密度](@entry_id:144672) $\rho$ 驱动，矢量势 $\mathbf{A}$ 由[电流密度](@entry_id:190690) $\mathbf{J}$ 驱动，并且它们都以光速 $c$ 传播。[@problem_id:3325816] [@problem_id:3325858] 这深刻地揭示了电磁相互作用的因果性和[有限传播速度](@entry_id:163808)。

这些波方程的解可以通过**[推迟格林函数](@entry_id:139183)**（[retarded Green's function](@entry_id:139183)）来构造。对于[达朗贝尔算子](@entry_id:275913) $\Box \equiv \nabla^2 - \frac{1}{c^2}\frac{\partial^2}{\partial t^2}$，其[推迟格林函数](@entry_id:139183)为：
$$
G_{\text{ret}}(\mathbf{r}, t) = \frac{\delta(t - |\mathbf{r}|/c)}{4\pi |\mathbf{r}|}
$$
它描述了一个在原点、瞬时发生的[点源](@entry_id:196698)所产生的、以光速向外传播的脉冲。利用这个[格林函数](@entry_id:147802)，任意源[分布](@entry_id:182848)产生的[推迟势](@entry_id:204770)可以通过时空卷积得到。例如，标量势的解为：
$$
\phi(\mathbf{r}, t) = \frac{1}{\varepsilon_0} \int \int G_{\text{ret}}(\mathbf{r}-\mathbf{r}', t-t') \rho(\mathbf{r}', t') \,d^3r' dt' = \int \frac{\rho(\mathbf{r}', t - |\mathbf{r}-\mathbf{r}'|/c)}{4\pi\varepsilon_0 |\mathbf{r}-\mathbf{r}'|} \,d^3r'
$$
这个积分形式明确体现了因果律：在时刻 $t$、位置 $\mathbf{r}$ 的势，是由源在过去某个**推迟时刻** $t' = t - |\mathbf{r}-\mathbf{r}'|/c$ 的状态决定的。[@problem_id:3325816]

[洛伦兹规范](@entry_id:153650)的另一个根本优势在于其**[洛伦兹协变性](@entry_id:161987)**。在[狭义相对论](@entry_id:275552)的四维时空框架中，我们可以定义[四维势](@entry_id:188407) $A^\mu = (\phi/c, \mathbf{A})$ 和[四维电流密度](@entry_id:262568) $J^\mu = (c\rho, \mathbf{J})$。四维[梯度算子](@entry_id:275922)为 $\partial_\mu = (\frac{1}{c}\frac{\partial}{\partial t}, \nabla)$。在这种表示下，[洛伦兹规范](@entry_id:153650)条件可以极其简洁地写成：
$$
\partial_\mu A^\mu = 0
$$
在洛伦兹变换下，$A^\mu$ 作为一个四维矢量进行变换，而 $\partial_\mu$ 作为一个[协变矢量](@entry_id:263917)进行变换。它们的缩并 $\partial_\mu A^\mu$ 是一个[洛伦兹标量](@entry_id:275319)，意味着它在所有惯性参考系中都具有相同的值。因此，如果在一个[参考系](@entry_id:169232)中 $\partial_\mu A^\mu = 0$ 成立，那么它在所有[惯性参考系](@entry_id:276742)中都成立。这种协变性使得[洛伦兹规范](@entry_id:153650)成为[相对论电动力学](@entry_id:160964)中的首选。[@problem_id:3325819]

### [库仑规范](@entry_id:273044)：分离静电与动力学效应

另一个重要的规范选择是**[库仑规范](@entry_id:273044)**（Coulomb gauge），也称为辐射规范或横向规范。其定义为：
$$
\nabla \cdot \mathbf{A} = 0
$$
这个条件同样可以解耦势方程，但方式与[洛伦兹规范](@entry_id:153650)截然不同。将 $\nabla \cdot \mathbf{A} = 0$ 代入之[前推](@entry_id:158718)导的含源[高斯定律](@entry_id:141493)方程，我们得到：
$$
\nabla^2 \phi = -\frac{\rho}{\varepsilon_0}
$$
这正是我们熟悉的**泊松方程**。它表明，在[库仑规范](@entry_id:273044)下，[标量势](@entry_id:276177) $\phi$ 在任意时刻都完全由该时刻的[电荷分布](@entry_id:144400) $\rho$ 决定，其形式与静电学完全相同。解可以写为：
$$
\phi(\mathbf{r}, t) = \int \frac{\rho(\mathbf{r}', t)}{4\pi\varepsilon_0 |\mathbf{r}-\mathbf{r}'|} \,d^3r'
$$
这种“瞬时”的相互作用看似违背了相对论的因果律，但需要强调的是，$\phi$ 和 $\mathbf{A}$ 并非直接[可观测量](@entry_id:267133)。物理场 $\mathbf{E}$ 和 $\mathbf{B}$ 仍然是因果的，因为 $\mathbf{A}$ 的动力学行为补偿了 $\phi$ 的瞬时性。[@problem_id:3325858] [@problem_id:3325784]

相应地，矢量势 $\mathbf{A}$ 的方程变得更加复杂。它由一个包含**横向[电流密度](@entry_id:190690)** $\mathbf{J}_T$ 驱动的波方程决定，其中 $\mathbf{J}_T$ 是总[电流密度](@entry_id:190690) $\mathbf{J}$ 中散度为零的部分。[@problem_id:3325858]

[库仑规范](@entry_id:273044)的一个重要特性是它将场分解为纵向和横向分量。在傅里叶空间（或$\mathbf{k}$空间）中，[梯度算子](@entry_id:275922)变为 $i\mathbf{k}$，[散度算子](@entry_id:265975)变为 $i\mathbf{k}\cdot$。因此，库侖[规范条件](@entry_id:749730) $\nabla \cdot \mathbf{A} = 0$ 在傅里叶空间中等价于**横向条件**：
$$
\mathbf{k} \cdot \tilde{\mathbf{A}}(\mathbf{k}) = 0
$$
这表明矢量势的傅里叶分量总是垂直于波矢 $\mathbf{k}$。任何一个矢量场 $\tilde{\mathbf{V}}$ 都可以被分解为一个平行于 $\mathbf{k}$ 的纵向分量和一个垂直于 $\mathbf{k}$ 的横向分量。[库仑规范](@entry_id:273044)本质上是移除了矢量势的纵向分量。实现这种分解的数学工具是**横向[投影算子](@entry_id:154142)** $P_{ij}(\mathbf{k})$：
$$
P_{ij}(\mathbf{k}) = \delta_{ij} - \frac{k_i k_j}{k^2}
$$
其中 $k=|\mathbf{k}|$。这个算子作用于任意矢量场 $\tilde{\mathbf{V}}$ 将得到其横向分量 $\tilde{\mathbf{V}}^\perp$。[@problem_id:3325825]

与[洛伦兹规范](@entry_id:153650)不同，[库仑规范](@entry_id:273044)不是洛伦兹协变的。在一个[参考系](@entry_id:169232)中满足 $\nabla \cdot \mathbf{A} = 0$ 的势，在经过洛伦兹变换到另一个[参考系](@entry_id:169232)后，通常不再满足此条件。这使得它在处理相对论性问题时较为不便，但在[量子电动力学](@entry_id:150740)和凝聚态物理的某些领域中，由于其清晰地分离了静电效应和[辐射效应](@entry_id:148987)，它仍然非常有用。[@problem_id:3325819]

### [规范变换](@entry_id:176521)与残余自由度

即使在固定了一个规范之后，势的唯一性问题也并未完全解决。我们仍可能存在一定的**残余规范自由度**（residual gauge freedom）。

假设我们已经有了一组满足[洛伦兹规范](@entry_id:153650)的势 $(\mathbf{A}, \phi)$。我们现在问，什么样的[规范函数](@entry_id:749731) $\chi$ 能使得变换后的势 $(\mathbf{A}', \phi')$ 仍然满足[洛伦兹规范](@entry_id:153650)？
$$
\nabla \cdot \mathbf{A}' + \frac{1}{c^2}\frac{\partial \phi'}{\partial t} = \nabla \cdot (\mathbf{A} + \nabla \chi) + \frac{1}{c^2}\frac{\partial}{\partial t}\left(\phi - \frac{\partial \chi}{\partial t}\right) = \left(\nabla \cdot \mathbf{A} + \frac{1}{c^2}\frac{\partial \phi}{\partial t}\right) + \left(\nabla^2 \chi - \frac{1}{c^2}\frac{\partial^2 \chi}{\partial t^2}\right) = 0
$$
由于第一项已经为零，我们发现，为了保持[洛伦兹规范](@entry_id:153650)，[规范函数](@entry_id:749731) $\chi$ 自身必须满足**齐次波方程** $\Box \chi = 0$。[@problem_id:3325787] [@problem_id:3325819]

类似地，对于[库仑规范](@entry_id:273044)，若要保持 $\nabla \cdot \mathbf{A}' = 0$，[规范函数](@entry_id:749731) $\chi$ 必须满足**拉普拉斯方程** $\nabla^2 \chi = 0$。[@problem_id:3325787]

这些残余自由度意味着即使选择了规范，势也不是完全唯一的。然而，在大多数物理问题中，我们还会施加**边界条件**。例如，在处理辐射问题的无界空间中，我们要求势在无穷远处衰减为零。根据波动方程和拉普拉斯方程的唯一性定理，在无界空间中满足齐次方程且在无穷远处为零的解只有[平凡解](@entry_id:155162) $\chi=0$（或一个无关紧要的常数）。因此，在这些物理情境下，[规范条件](@entry_id:749730)与物理边界条件相结合，最终能够唯一地确定[电磁势](@entry_id:266145)。[@problem_id:3325787]

我们也可以从一个规范变换到另一个。例如，如果我们从一组满足[洛伦兹规范](@entry_id:153650)的势 $(\mathbf{A}, \phi)$ 出发，想要得到一组满足[库仑规范](@entry_id:273044)的新势 $(\mathbf{A}', \phi')$，我们需要寻找一个[规范函数](@entry_id:749731) $\chi$ 使得 $\nabla \cdot \mathbf{A}' = \nabla \cdot (\mathbf{A} + \nabla \chi) = 0$。这导出了一个关于 $\chi$ 的泊松方程：
$$
\nabla^2 \chi = -\nabla \cdot \mathbf{A}
$$
求解这个[泊松方程](@entry_id:143763)（在适当的边界条件下），我们就能找到所需的[规范函数](@entry_id:749731) $\chi$，进而完成从[洛伦兹规范](@entry_id:153650)到[库仑规范](@entry_id:273044)的变换。[@problem_id:3325784]

### 在计算电磁学中的意义

规范选择对[计算电磁学](@entry_id:265339)方法的稳定性、效率和实现复杂度有着至关重要的影响。

#### 数值稳定性与寄生模

在有限元方法（FEM）等离散化方案中，一个核心挑战是处理[旋度算子](@entry_id:184984) $\nabla \times$ 的巨大零空间，该零空间由所有[梯度场](@entry_id:264143)构成。如果[变分形式](@entry_id:166033)未能有效控制这个零空间，离散系统中就会出现大量对应于非物理[梯度场](@entry_id:264143)的零或接近零的[特征值](@entry_id:154894)。这些模式被称为**寄生模**（spurious modes），它们会严重污染数值解并破坏代数系统的良态性。

[规范条件](@entry_id:749730)是控制这些寄生模的关键。
- **[洛伦兹规范](@entry_id:153650)**通过耦合 $\mathbf{A}$ 和 $\phi$ 的方程，提供了一种鲁棒的正则化机制。它在整个 $(\mathbf{A}, \phi)$ 系统中引入了与频率相关的耦合项，有效地“提升”了[梯度场](@entry_id:264143)的能量，从而抑制了寄生模。在数学上，这确保了对应的离散算子在一个关键的[子空间](@entry_id:150286)上是强制的（coercive），并且整个[混合格式](@entry_id:167436)满足一个在网格尺寸 $h$ 上一致的 inf-sup 稳定条件（对于固定的 $\omega > 0$）。[@problem_id:3325800]
- **[库仑规范](@entry_id:273044)**则通过[拉格朗日乘子法](@entry_id:176596)强制施加 $\nabla \cdot \mathbf{A} = 0$ 约束，形成一个**[鞍点问题](@entry_id:174221)**。这类问题的数值稳定性是出了名的“脆弱”。即使使用了满足离散 [inf-sup 条件](@entry_id:174538)的兼容有限元空间，整个系统的良态性仍然不理想，因为主算子块（包含 $\nabla \times \nabla \times$ 项）在[梯度场](@entry_id:264143)[子空间](@entry_id:150286)上仍然是奇异的。这使得系统对[离散化误差](@entry_id:748522)和扰动非常敏感，容易产生数值噪声。[@problem_id:3325800]

因此，对于通用目的的有限元求解器，[洛伦兹规范](@entry_id:153650)通常被认为在抑制寄生模和保证数值稳定性方面更为稳健。

#### 代数求解器性能

规范选择直接决定了最终离散[线性系统](@entry_id:147850)的[代数结构](@entry_id:137052)，从而影响迭代求解器的性能。
- **[洛伦兹规范](@entry_id:153650)**下的势方程是[解耦](@entry_id:637294)的亥姆霍兹方程。虽然高频亥姆霍兹方程本身求解难度很大（算子高度不定），但其结构是标准的。我们可以独立地为 $\mathbf{A}$ 和 $\phi$ 的[系统设计](@entry_id:755777)和应用先进的[预条件子](@entry_id:753679)，如多重网格法、域分解法等。这使得它能更好地利用现有的高性能求解器技术。[@problem_id:3325801]
- **[库仑规范](@entry_id:273044)**下的[鞍点](@entry_id:142576)结构对[迭代求解器](@entry_id:136910)极不友好。其[系统矩阵](@entry_id:172230)不定，且[特征值分布](@entry_id:194746)广泛，包含许多接近零的[特征值](@entry_id:154894)。标准的[预条件子](@entry_id:753679)（如[不完全LU分解](@entry_id:163424)）通常效果很差。要高效求解此类系统，必须采用专门为[鞍点问题](@entry_id:174221)设计的**块[预条件子](@entry_id:753679)**（block preconditioners），如Schur补预条件子。这增加了实现的复杂性，且在高频下性能通常不如[洛伦兹规范](@entry_id:153650)下的[解耦](@entry_id:637294)方案。[@problem_id:3325801]

#### 物理定律的执行

[数值离散化](@entry_id:752782)误差可能破坏物理守恒律，例如电荷守恒定律 $\frac{\partial \rho}{\partial t} + \nabla \cdot \mathbf{J} = 0$。如果一个数值方案不能精确地保持这个关系，就可能导致非物理的[电荷](@entry_id:275494)产生或消失。一种常见的补救措施是引入一个**散度修正**或**[散度清理](@entry_id:748607)**步骤。该方法通过求解一个[泊松方程](@entry_id:143763)来计算一个修正势 $\delta\phi$，并用它来调整[电荷密度](@entry_id:144672) $\rho$，从而强制满足[电荷守恒](@entry_id:264158)。这个修正步骤的推导是基于高斯定律的，因此其形式与规范选择无关，可以应用于任何未能精确保持[电荷守恒](@entry_id:264158)的算法中。[@problem_id:3325788]

#### 边界与拓扑问题

- **[材料界面](@entry_id:751731)**：在不同介质的交界处，[电磁场](@entry_id:265881)需满足特定的边界条件。这些条件也会传递到势上。例如，在两种[介电常数](@entry_id:146714)（$\varepsilon_1, \varepsilon_2$）和[磁导率](@entry_id:154559)（$\mu_1, \mu_2$）不同的[材料界面](@entry_id:751731)上，[洛伦兹规范](@entry_id:153650) $\nabla \cdot \mathbf{A} = -i\omega\mu\varepsilon\phi$ 暗示了 $\nabla \cdot \mathbf{A}$ 通常是不连续的，其跳变值为 $[\nabla \cdot \mathbf{A}] = -i\omega(\mu_2\varepsilon_2 - \mu_1\varepsilon_1)\phi$。而[库仑规范](@entry_id:273044)则强制要求 $\nabla \cdot \mathbf{A}$ 在界面两侧均为零，因此其跳变值 $[\nabla \cdot \mathbf{A}]$ 恒为零。这在[边界元法](@entry_id:141290)（BEM）或需要显式处理[界面条件](@entry_id:750725)的有限元法中具有重要意义。[@problem_id:3325804]

- **拓扑约束**：在拓扑非平凡的区域（如环形域）中，规范选择会遇到更深层次的困难。例如，在一个三维环面（torus）上，如果存在穿过环面孔洞的净[磁通量](@entry_id:268943)，那么根据[斯托克斯定理](@entry_id:264534)，就不可能定义一个全球单值且周期性的矢量势 $\mathbf{A}$。这意味着[库仑规范](@entry_id:273044) $\nabla \cdot \mathbf{A} = 0$ 无法在全球范围内被满足。在计算中，必须采用更高级的技术，如引入“扭曲”周期性边界条件，或在[有限元外微分](@entry_id:174585)（FEEC）框架下，显式地为代表拓扑自由度的**上同调[基函数](@entry_id:170178)**（cohomology basis functions）[分配系数](@entry_id:177413)，以正确表示净磁通量。这是一个深刻的例子，说明了物理、拓扑和规范选择之间错综复杂的关系。[@problem_id:3325818]

总之，[洛伦兹规范](@entry_id:153650)和[库仑规范](@entry_id:273044)为我们提供了两种不同的视角和数学工具来处理电磁问题。[洛伦兹规范](@entry_id:153650)因其相对论协变性和在计算中的鲁棒性而受到青睐，尤其是在波传播和高频问题中。[库仑规范](@entry_id:273044)则因其能清晰分离静电和横向[辐射场](@entry_id:164265)，在理论分析和某些[量子场论](@entry_id:138177)应用中占有一席之地。在[计算电磁学](@entry_id:265339)实践中，理解它们各自的优势和缺陷是设计高效、准确和稳定数值算法的关键。