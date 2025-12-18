## 引言
在计算热工和空气动力学领域，能量方程是与质量和动量守恒并列的三大基本控制方程之一，对于准确预测涉及密度变化的流动（即[可压缩流](@entry_id:747589)）中的温度、压力和热流至关重要。然而，能量方程并非以单一形式存在；它可以被表述为总能方程、内能方程、温度方程，并且每种形式又可分为守恒型与非守恒型。为特定物理问题选择不恰当的方程形式，可能导致模拟结果的严重失真，甚至得出完全非物理的解。因此，理解不同表述的物理内涵、数学特性及其适用边界，是进行高保真度[计算模拟](@entry_id:146373)的关键，也是许多工程师和研究人员面临的知识难点。

本篇文章旨在系统性地剖析[可压缩能量方程](@entry_id:1122757)的各种表述形式，为读者构建一个清晰的理论与应用框架。
- 在第一章**“原理与机制”**中，我们将从最基本的[热力学第一定律](@entry_id:146485)和雷诺输运定理出发，严谨推导能量方程的积分与微分形式。我们将详细拆解方程中的各项物理机制，并辨析守恒型与非守恒型、总能与内能方程在不同流动条件下的优劣。
- 第二章**“应用与交叉学科联系”**将理论付诸实践，通过气体动力学、[湍流](@entry_id:151300)、燃烧学乃至天体物理学中的具体实例，展示能量方程如何与其他物理定律耦合，共同描绘出复杂流动的全貌，并探讨其对数值求解器架构的深刻影响。
- 最后，在**“动手实践”**部分，读者将通过一系列精心设计的练习，从推导激波关系到验证数值格式精度，亲手应用所学知识，加深对核心概念的理解。

通过本章的学习，您将能够自信地为您的[计算模型](@entry_id:637456)选择最合适的能量方程形式，从而显著提升仿真结果的准确性和可靠性。

## 原理与机制

本章深入探讨[可压缩流能量方程](@entry_id:188548)的各种表述形式、其物理基础以及在计算建模中的应用。我们将从最基本的[热力学第一定律](@entry_id:146485)和控制体分析出发，推导出[能量方程的积分形式](@entry_id:750702)和[微分形式](@entry_id:146747)。随后，我们将详细剖析方程中的关键物理机制，包括压力功、[粘性耗散](@entry_id:143708)和[热传导](@entry_id:143509)，并阐明它们在[能量转换](@entry_id:165656)过程中的作用。最后，我们将讨论不同方程形式（例如，守恒形式与[非守恒形式](@entry_id:1128837)，总能与内能）的优缺点，以及它们在特定流动区域（如激波或[低马赫数流](@entry_id:1127481)）中的适用性，并介绍解决极端条件下数值挑战的高级方法。

### [能量守恒的积分形式](@entry_id:202417)

[流体动力](@entry_id:750449)学中守恒定律的建立，通常始于一个有限大小、空间固定的区域，即**控制体 (Control Volume, CV)**。能量守恒的表述也不例外。其基础是热力学第一定律，它描述了一个封闭**系统（System）**（即固定质量的流体）的总能量变化率。对于一个系统，其总能量 $E_{\mathrm{sys}}$ 的变化率等于外界对系统加热的净速率 $\dot{Q}$ 减去系统对外界做功的净速率 $\dot{W}$：
$$ \frac{\mathrm{d}E_{\mathrm{sys}}}{\mathrm{d}t} = \dot{Q} - \dot{W} $$

为了将这个基于系统的定律应用于基于空间的控制体，我们使用**[雷诺输运定理](@entry_id:191217) (Reynolds Transport Theorem, RTT)**。RTT 为任意[广延性质](@entry_id:145410) $B$（其对应的比性质为 $b$）建立了系统变化率与控制体内变化率及跨越**控制面 (Control Surface, CS)** 的通量之间的关系。对于固定的控制体，RTT 的形式为：
$$ \frac{\mathrm{d}B_{\mathrm{sys}}}{\mathrm{d}t} = \frac{\mathrm{d}}{\mathrm{d}t}\int_{\mathrm{CV}}\rho b \,\mathrm{d}V + \oint_{\mathrm{CS}}\rho b (\mathbf{V}\cdot\mathbf{n})\,\mathrm{d}A $$
其中，$\rho$ 是密度，$\mathbf{V}$ 是[流体速度](@entry_id:267320)，$\mathbf{n}$ 是指向控制体外部的[单位法向量](@entry_id:178851)。右边的第一项表示控制体内性质 $B$ 的**累积率**，第二项表示通过控制面的净**通量率**。

将能量作为我们的[广延性质](@entry_id:145410)，即 $B_{\mathrm{sys}} = E_{\mathrm{sys}}$，对应的比性质为单位质量的总能量 $e_t = u + \frac{1}{2}|\mathbf{V}|^{2} + gz$，其中 $u$ 是比内能，$|\mathbf{V}|^{2}/2$ 是比动能，$gz$ 是比势能。应用 RTT，热力学第一定律的左侧变为：
$$ \frac{\mathrm{d}E_{\mathrm{sys}}}{\mathrm{d}t} = \frac{\mathrm{d}}{\mathrm{d}t}\int_{\mathrm{CV}}\rho e_t \,\mathrm{d}V + \oint_{\mathrm{CS}}\rho e_t (\mathbf{V}\cdot\mathbf{n})\,\mathrm{d}A $$

现在我们来分析热力学第一定律的右侧项 $\dot{Q} - \dot{W}$。
1.  **热量[传递率](@entry_id:756124) ($\dot{Q}$)**：热量可以通过控制体表面传入。若 $q''_{w}$ 是指向控制体内部的壁面热通量，则总加热率为 $\dot{Q} = \int_{S_{w}} q''_{w}\,\mathrm{d}A$，其中 $S_w$ 是发生热交换的壁面。
2.  **做功速率 ($\dot{W}$)**：系统对外界做功包括多种形式。**轴功 ($\dot{W}_{\mathrm{sh}}$)** 是通过[旋转轴](@entry_id:187094)等机械装置传递的功率。此外，当流体穿过控制面时，它需要对周围的流体做功以“推开”空间，这被称为**流动功 (Flow Work)**。单位[质量流](@entry_id:143424)体所做的流动功为 $p/\rho$（$p$ 为压力）。因此，在整个控制面上由压力引起的做功速率为 $\oint_{\mathrm{CS}}p(\mathbf{V}\cdot\mathbf{n})\,\mathrm{d}A$。此外，粘性应力也会在控制面上做功。

将所有项组合起来，并将流动功移到方程左侧，我们得到：
$$ \frac{\mathrm{d}}{\mathrm{d}t}\int_{\mathrm{CV}}\rho e_t \,\mathrm{d}V + \oint_{\mathrm{CS}}\rho e_t (\mathbf{V}\cdot\mathbf{n})\,\mathrm{d}A + \oint_{\mathrm{CS}}p(\mathbf{V}\cdot\mathbf{n})\,\mathrm{d}A = \int_{S_{w}} q''_{w}\,\mathrm{d}A - \dot{W}_{\mathrm{sh}} $$
注意到左侧的两个[面积分](@entry_id:275394)可以合并。利用密度 $\rho$，我们可以将压力项写为 $\oint_{\mathrm{CS}}\rho (p/\rho)(\mathbf{V}\cdot\mathbf{n})\,\mathrm{d}A$。合并后的通量项变为：
$$ \oint_{\mathrm{CS}}\rho \left(e_t + \frac{p}{\rho}\right) (\mathbf{V}\cdot\mathbf{n})\,\mathrm{d}A $$
我们定义**比焓 (specific enthalpy)** 为 $h \equiv u + p/\rho$。因此，$e_t + p/\rho = (u+p/\rho) + \frac{1}{2}|\mathbf{V}|^2 + gz = h + \frac{1}{2}|\mathbf{V}|^2 + gz$。这个组合量被称为**比[总焓](@entry_id:197863) (specific total enthalpy)**。

最终，我们得到[可压缩流](@entry_id:747589)动的**能量守恒[积分方程](@entry_id:138643)** ：
$$ \frac{\mathrm{d}}{\mathrm{d}t}\int_{\mathrm{CV}}\rho\left(u+\frac{|\mathbf{V}|^{2}}{2}+gz\right)\mathrm{d}V + \oint_{\mathrm{CS}}\rho\left(h+\frac{|\mathbf{V}|^{2}}{2}+gz\right)(\mathbf{V}\cdot\mathbf{n})\,\mathrm{d}A = \int_{S_{w}} q''_{w}\,\mathrm{d}A - \dot{W}_{\mathrm{sh}} $$
这个方程是所有[可压缩能量方程](@entry_id:1122757)推导的物理基础。它表明，控制体内总能量的变化率等于通过边界的净能量输入（以热量和功的形式）与通过质量流动的净能量输运之和。

### 能量方程的微分形式

虽然积分形式在宏观分析中非常有用，但对于计算流体力学 (CFD) 中需要求解局部流场的问题，我们通常需要其[微分形式](@entry_id:146747)。通过应用[高斯散度定理](@entry_id:188065)，我们可以将积分方程转换为[偏微分](@entry_id:194612)方程 (PDE)。

#### 守恒型总能方程

从积分形式出发，假设被积函数足够光滑，并且[积分方程](@entry_id:138643)对任意控制体都成立，我们可以得到其对应的[微分形式](@entry_id:146747)。忽略重力效应和轴功，能量方程的**守恒型 (conservative form)** 或**散度型 (divergence form)** 如下：
$$ \frac{\partial (\rho E)}{\partial t} + \nabla \cdot ((\rho E + p) \mathbf{u}) = \nabla \cdot (\boldsymbol{\tau} \cdot \mathbf{u}) - \nabla \cdot \mathbf{q} + S_E $$
其中，$E = e + \frac{1}{2}|\mathbf{u}|^2$ 是不含势能的比总能，$\boldsymbol{\tau}$ 是[粘性应力](@entry_id:261328)张量，$\mathbf{q}$ 是热[通量矢量](@entry_id:273577)，$S_E$ 是单位体积的能量源项（例如，化学反应放热）。

这个方程与[质量守恒](@entry_id:204015)方程和动量守恒方程一起，构成了完整的**[可压缩Navier-Stokes](@entry_id:747591)方程组** ：
1.  **质量守恒（[连续性方程](@entry_id:195013)）**:
    $$ \frac{\partial \rho}{\partial t} + \nabla\cdot(\rho \mathbf{u}) = 0 $$
2.  **[动量守恒](@entry_id:149964)**:
    $$ \frac{\partial (\rho \mathbf{u})}{\partial t} + \nabla\cdot(\rho \mathbf{u} \otimes \mathbf{u} + p\mathbf{I}) = \nabla \cdot \boldsymbol{\tau} + \rho \mathbf{b} $$
3.  **总能守恒**:
    $$ \frac{\partial (\rho E)}{\partial t} + \nabla \cdot ((\rho E + p) \mathbf{u}) = \nabla \cdot (\boldsymbol{\tau} \cdot \mathbf{u} - \mathbf{q}) + \rho \mathbf{b} \cdot \mathbf{u} $$
在这里，$\mathbf{b}$ 是单位质量的体积力。这组方程是高度耦合的：压力 $p$ 出现在动量和能量方程中，而速度 $\mathbf{u}$ 出现在所有方程中。此外，物性参数（如粘度 $\mu$ 和热导率 $k$）和状态方程（如[理想气体定律](@entry_id:146757) $p=\rho R T$）通过温度 $T$ 建立了能量方程与其他方程之间更深层次的联系。

#### 非守恒型内能方程

守恒型方程对于正确捕捉激波等不连续现象至关重要。然而，为了更好地理解其中的物理机制，我们常常推导**非守恒型 (non-conservative form)** 的**内能方程**。通过从总能方程中减去动能方程（由[动量方程](@entry_id:197225)与速度 $\mathbf{u}$ 点乘得到），可以得到以下形式 ：
$$ \rho \frac{De}{Dt} = -p(\nabla \cdot \mathbf{u}) + \boldsymbol{\tau} : \nabla\mathbf{u} - \nabla \cdot \mathbf{q} + S_E $$
其中，$D/Dt \equiv \partial/\partial t + \mathbf{u}\cdot\nabla$ 是**物质导数**，表示随流体微团移动的变化率。这个方程清晰地分离了改变内能的几个关键物理机制，我们将在下一节详细讨论。

### 能量传递机制的剖析

内能方程 $\rho De/Dt = -p(\nabla \cdot \mathbf{u}) + \boldsymbol{\tau} : \nabla\mathbf{u} - \nabla \cdot \mathbf{q} + S_E$ 为我们提供了一个理想的框架来分析能量是如何在不同形式之间转换的。

#### 压力-膨胀功：可逆的机械功转换

方程中的第一项，$-p(\nabla \cdot \mathbf{u})$，代表了由流体体积变化所做的**压力-膨胀功**。速度场的散度 $\nabla \cdot \mathbf{u}$ 描述了流体微团体积的膨胀率。

*   当流体被**压缩**时，$\nabla \cdot \mathbf{u}  0$，导致 $-p(\nabla \cdot \mathbf{u}) > 0$。这意味着外界对流体做正功，其内能增加，温度升高。这就是所谓的**压缩生热**。
*   当流体**膨胀**时，$\nabla \cdot \mathbf{u} > 0$，导致 $-p(\nabla \cdot \mathbf{u})  0$。这意味着流体对外界做功，其内能减少，温度降低。这就是所谓的**膨胀致冷**。

这个过程在理想情况下是**可逆的**。通过吉布斯关系 $T ds = de + p dv$（其中 $s$ 是比熵，$v=1/\rho$ 是比容）和连续性方程，我们可以推导出熵的[输运方程](@entry_id:174281)。在这个推导过程中，压力-膨胀功项 $-p(\nabla \cdot \mathbf{u})$ 与 $de$ 和 $dv$ 中的相应项完全抵消，表明在光滑、无粘、绝热的流动中，该项本身不产生熵 。它仅仅是机械能和内能之间的一种可逆转换方式。

#### [粘性耗散](@entry_id:143708)：不可逆的能量转换

方程中的第二项，$\Phi = \boldsymbol{\tau} : \nabla\mathbf{u}$，被称为**粘性耗散函数**。它描述了由于流体内速度梯度（即剪切和拉伸）和[粘性应力](@entry_id:261328)而产生的[能量转换](@entry_id:165656)。

[粘性耗散](@entry_id:143708)的本质是将宏观的机械能（动能）不可逆地转化为微观的内能（热）。这是[摩擦生热](@entry_id:201286)在流体中的体现。对于[牛顿流体](@entry_id:263796)，[粘性应力](@entry_id:261328)张量 $\boldsymbol{\tau}$ 是应变率张量 $\mathbf{D}=\tfrac{1}{2}(\nabla\mathbf{u}+\nabla\mathbf{u}^{\mathsf{T}})$ 的线性函数。[粘性耗散](@entry_id:143708)函数可以写成 ：
$$ \Phi = 2\mu \mathbf{D}:\mathbf{D} + \lambda (\nabla\cdot\mathbf{u})^2 $$
其中 $\mu$ 是[剪切粘度](@entry_id:141046)，$\lambda$ 是[第二粘度](@entry_id:189253)系数。根据[热力学](@entry_id:172368)第二定律，这个过程必须是[耗散性](@entry_id:162959)的，即总是增加内能。这意味着 $\Phi$ 必须始终非负。为了保证这一点，流体的粘性系数必须满足一定的物理约束条件，即 $\mu \ge 0$ 和 $\lambda + \frac{2}{3}\mu \ge 0$。这个过程是完全**不可逆的**，并且是熵的一个主要来源。

#### [热传导](@entry_id:143509)

方程中的第三项，$-\nabla \cdot \mathbf{q}$，代表了由**[热传导](@entry_id:143509)**引起的内能变化。热通量矢量 $\mathbf{q}$ 描述了单位时间通过单位面积的热量流动。散度的负号表示，当热量从一个区域流出时（$\nabla \cdot \mathbf{q} > 0$），该区域的内能会减少。

根据**[傅里叶热传导定律](@entry_id:138911)**，热通量与温度梯度成正比，方向相反 ：
$$ \mathbf{q} = -k \nabla T $$
其中 $k$ 是**[热导](@entry_id:189019)率**。将此代入能量方程，[热传导](@entry_id:143509)项变为 $\nabla \cdot (k \nabla T)$。如果热导率 $k$ 是常数，该项简化为 $k \nabla^2 T$（一个线性的拉普拉斯项）。然而，在许多实际应用中，$k$ 是温度 $T$ 的函数。在这种情况下，必须使用[乘积法则](@entry_id:158393)展开：
$$ \nabla \cdot (k(T) \nabla T) = k(T) \nabla^2 T + (\nabla k) \cdot (\nabla T) $$
这使得能量方程成为一个[非线性](@entry_id:637147)的[扩散方程](@entry_id:170713)，增加了求解的复杂性。

#### 数值方法中的能量通量分解

在基于[有限体积法 (FVM)](@entry_id:749403) 的[CFD求解器](@entry_id:747244)中，我们需要计算通过每个控制单元边界（“面”）的通量。[总能量方程](@entry_id:1133263)的[通量矢量](@entry_id:273577) $\mathbf{F}_E$ 可以被精确地分解为对流、压力功、粘性功和[热传导](@entry_id:143509)四个部分。对于一个面积为 $A_f$，法向量为 $\mathbf{n}_f$ 的面，离开控制体的总[能量通量](@entry_id:266056)为 ：
$$ F_{E,f} = \left[ (\rho E)_f (\mathbf{u}_f \cdot \mathbf{n}_f) + p_f (\mathbf{u}_f \cdot \mathbf{n}_f) - ((\boldsymbol{\tau} \cdot \mathbf{u})_f \cdot \mathbf{n}_f) + (\mathbf{q}_f \cdot \mathbf{n}_f) \right] A_f $$
其中，$(\rho E)_f (\mathbf{u}_f \cdot \mathbf{n}_f)$ 是**[对流通量](@entry_id:158187)**，$p_f (\mathbf{u}_f \cdot \mathbf{n}_f)$ 是**压力功通量**，$- ((\boldsymbol{\tau} \cdot \mathbf{u})_f \cdot \mathbf{n}_f)$ 是**粘性功通量**，而 $(\mathbf{q}_f \cdot \mathbf{n}_f)$ 是**[热传导](@entry_id:143509)通量**。这种分解对于设计精确和稳定的数值格式至关重要。

### 选择正确的能量方程形式

不同的能量方程形式在不同的物理场景和数值算法中有各自的优势和局限性。

#### 守恒型 vs. 非守恒型：激波与光滑流

对于光滑、连续的流场，守恒型和非守恒型方程在数学上是等价的，因为从前者到后者的推导依赖于可以处处为零的[连续性方程](@entry_id:195013) 。然而，当流场中出现**激波**等不连续现象时，这种等价性便不复存在。

物理上，守恒定律的积分形式是最根本的。只有守恒型（散度型）的[微分](@entry_id:158422)方程才能在包含不连续的“[弱解](@entry_id:161732)”意义下，正确地代表其积分形式。在数值上，这意味着只有[离散守恒](@entry_id:1123819)型方程的有限体积格式才能保证在网格间传递的能量是守恒的，从而正确地计算出激波两侧应满足的**朗金-雨果尼厄跳跃关系 (Rankine-Hugoniot jump conditions)**。使用非守恒型方程求解激波问题，即使网格加密到无限，也会收敛到一个物理上不正确的错误解 。

#### 总能 vs. 内能：低马赫数问题

在**[低马赫数](@entry_id:1127478) ($M \to 0$)** 流动中，流体的动能远小于其内能（$|\mathbf{u}|^2/2 \ll e$）。在这种情况下，总能 $E = e + |\mathbf{u}|^2/2$ 的大小主要由内能 $e$ 决定。如果求解守恒的总能方程，我们得到的 $\rho E$ 在数值上与 $\rho e$ 非常接近。为了计算压力，我们必须从一个大数中减去一个与之相近的大数来恢复内能：$e = E - |\mathbf{u}|^2/2$。这个过程会产生严重的**数值相消 (subtractive cancellation)** 错误，导致计算出的温度和压力出现巨大误差甚至变为负值 。

在这种情况下，直接求解内能方程或温度方程会更加稳健和精确，因为它直接追踪内能或温度的变化，避免了这种病态的减法操作。

#### 温度基方程

在许多工程问题中，我们最终关心的是温度场，而且流体的物性（如 $\mu$ 和 $k$）通常表示为温度的函数。因此，将能量方程转换为以温度 $T$ 为求解变量的形式非常方便。这可以通过链式法则，并引入**定容比热 ($c_v$)** 和**定[压比](@entry_id:137698)热 ($c_p$)** 来实现 。

*   从内能方程出发，利用 $de \approx c_v dT$，可以得到一个关于 $DT/Dt$ 的方程，其形式为：
    $$ \rho c_v \frac{DT}{Dt} = -T\left(\frac{\partial p}{\partial T}\right)_v \nabla\cdot\mathbf{u} + \Phi - \nabla\cdot\mathbf{q} + S_E $$
*   从焓方程（可由内能方程推导）出发，利用 $dh \approx c_p dT$，可以得到：
    $$ \rho c_p \frac{DT}{Dt} = \rho T\left(\frac{\partial v}{\partial T}\right)_p \frac{Dp}{Dt} + \Phi - \nabla\cdot\mathbf{q} + S_E $$

对于量热完全理想气体，这些方程简化为我们更熟悉的形式 ：
$$ \rho c_v \frac{DT}{Dt} = -p\nabla\cdot\mathbf{u} + \dots \quad \text{和} \quad \rho c_p \frac{DT}{Dt} = \frac{Dp}{Dt} + \dots $$
这些方程清楚地展示了机械效应（如压缩和压力变化）与热效应（如耗散和传导）是如何耦合在一起决定温度演化的。

#### 高级专题：高[马赫数](@entry_id:274014)流动的双能格式

与[低马赫数](@entry_id:1127478)问题相对，**高[马赫数](@entry_id:274014) ($M \gg 1$)** 流动也存在数值挑战。此时，动能远大于内能。求解守恒的总能方程时，即使是微小的数值误差也可能导致计算出的内能 $e = E - |\mathbf{u}|^2/2$ 为负，从而得到非物理的[负压](@entry_id:161198)力。

为了解决这个问题，发展出了一种称为**双能（或混合）格式 (dual-energy/hybrid formulation)** 的先进数值方法 。其核心思想是：
1.  始终求解**守恒的总能方程**，以保证正确的激波捕捉和全局能量守恒。
2.  同时，并行求解一个**非守恒的内能方程**。由于内能方程的源项（如粘性耗散）通常是正的，因此更容易设计出保证 $\rho e$ 始终为正的数值格式。
3.  根据流场情况动态选择使用哪个能量值来计算压力。在一个判断准则（例如，当内能与总能之比 $e/E$ 低于某个阈值时）的指导下，在可能出现[负压](@entry_id:161198)力的“刚性”区域，使用由内能方程得到的、保证为正的内能来计算压力。在其他“安全”区域，则将内能同步到由守恒总能计算出的值，以维持长期的一致性。

通过这种方式，双能格式巧妙地结合了两种方法的优点，既保证了数值解的物理真实性（压力为正），又维持了对激波等不连续现象至关重要的能量守恒性。