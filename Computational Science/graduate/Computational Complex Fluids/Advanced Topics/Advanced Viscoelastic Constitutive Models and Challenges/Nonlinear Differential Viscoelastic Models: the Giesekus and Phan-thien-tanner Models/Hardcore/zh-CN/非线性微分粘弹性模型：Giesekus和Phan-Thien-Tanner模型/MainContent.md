## 引言
复杂流体，如聚合物熔体和溶液，在工业加工中常见的强流场下表现出复杂的[非线性](@entry_id:637147)行为，这超出了[线性粘弹性](@entry_id:181219)模型的预测能力。[剪切致稀](@entry_id:150203)、[法向应力](@entry_id:260622)效应和拉伸[硬化](@entry_id:177483)等现象对过程控制和产品质量至关重要，但如何用严谨的数学模型来描述这些行为，是流变学和计算流体科学中的一个核心挑战。本文旨在深入剖析两类应用最广泛的[非线性](@entry_id:637147)[微分](@entry_id:158422)[粘弹性模型](@entry_id:175352)——Giesekus模型和Phan-Thien-Tanner (PTT)模型，为理解和应用这些强大的工具提供一个清晰的框架。

我们将分三个章节展开：在“原理与机制”中，我们将探究这些模型背后的物理起源和数学构造，揭示它们如何从微观结构出发捕捉宏观[非线性响应](@entry_id:188175)；在“应用与跨学科连接”中，我们将展示这些理论如何与实验流变学和[计算模拟](@entry_id:146373)相结合，成为连接理论与实践的桥梁；最后，通过“动手实践”，您将有机会应用所学知识来分析和解决具体问题。通过这一结构化的学习路径，读者将能够掌握从微观物理洞察到宏观流变预测，再到工程应用的全过程。

## 原理与机制

在对[复杂流体](@entry_id:198415)进行建模时，[线性粘弹性](@entry_id:181219)模型，如上随体Maxwell (UCM) 模型，为描述小形变和短时行为提供了基础框架。然而，[聚合物熔体](@entry_id:192068)和溶液在工业加工中常见的强流场下会表现出丰富的[非线性](@entry_id:637147)现象，例如剪切致稀、[法向应力差](@entry_id:199507)以及[拉伸粘度](@entry_id:1124791)的[应变硬化](@entry_id:1132472)。为了捕捉这些复杂的[流变学](@entry_id:138671)响应，必须引入[非线性](@entry_id:637147)[微分](@entry_id:158422)[粘弹性本构模型](@entry_id:265825)。本章将深入探讨两类应用最广泛的非线性模型——Giesekus模型和Phan-Thien-Tanner (PTT) 模型——的物理原理、数学构造及其流变学预测。

### [本构模型](@entry_id:174726)构建的指导原则

在从线性框架扩展到[非线性](@entry_id:637147)领域时，任何一个严谨的本构模型都必须遵循几个基本物理和数学原则，以确保其有效性和物理实在性。

首先是 **物质[坐标无关性](@entry_id:159715) (Material Frame Indifference)** 原理。该原理要求本构方程的形式不应依赖于观察者的参考系。对于一个描述流体内部微结构（如[聚合物链构象](@entry_id:173977)）演化的张量，这意味着其时间导数必须是“客观的”。对于由柔性聚合物链哑铃状微结构构成的流体，物理上恰当的[客观时间导数](@entry_id:1129024)是 **[上随体导数](@entry_id:756365) (upper-convected derivative)**。对于任意[二阶张量](@entry_id:199780) $\boldsymbol{T}$，其[上随体导数](@entry_id:756365)定义为：
$$
\overset{\nabla}{\boldsymbol{T}} = \frac{\mathrm{D}\boldsymbol{T}}{\mathrm{D}t} - \boldsymbol{L}\cdot\boldsymbol{T} - \boldsymbol{T}\cdot\boldsymbol{L}^{\mathrm{T}}
$$
其中 $\frac{\mathrm{D}}{\mathrm{D}t}$ 是物质导数，$\boldsymbol{L} = \boldsymbol{\nabla}\boldsymbol{v}$ 是[速度梯度张量](@entry_id:270928)。这个选择根植于[聚合物动力学](@entry_id:146985)理论，它正确地描述了嵌入在宏观形变流场中的微观结构单元的拉伸和旋转。

其次是 **[线性响应](@entry_id:146180)一致性 (Linear-Response Consistency)**。一个有效的[非线性模型](@entry_id:276864)，在其[非线性](@entry_id:637147)参数趋于零或在小形变极限下，必须能够退化为公认的[线性粘弹性](@entry_id:181219)模型，即 UCM 模型。UCM 模型的[标准形式](@entry_id:153058)为：
$$
\lambda\overset{\nabla}{\boldsymbol{\tau}} + \boldsymbol{\tau} = 2\eta_p\boldsymbol{D}
$$
其中 $\boldsymbol{\tau}$ 是聚合物贡献的附加应力张量，$\lambda$ 是松弛时间，$\eta_p$ 是[聚合物粘度](@entry_id:186823)，$\boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^{\mathrm{T}})$ 是形变速率张量。这一要求确保了模型在小应变或低应变率下的行为是正确的，并且新引入的[非线性](@entry_id:637147)项是高阶效应。

最后，[非线性](@entry_id:637147)项的引入必须具有合理的 **微观结构起源和[热力学](@entry_id:172368)相容性**。[非线性](@entry_id:637147)项并非随意添加，它们通常反映了对理想化微观模型（如胡克哑铃模型）的修正，并且必须保证在任何物理可及的流动条件下，[熵产](@entry_id:141771)率非负。

### Giesekus模型：各向异性曳力

Giesekus模型是解释聚合物溶液和熔体流变行为最成功的模型之一。它通过引入一个二次应力项来扩展 UCM 模型，其[标准形式](@entry_id:153058)为：
$$
\boldsymbol{\tau} + \lambda\overset{\nabla}{\boldsymbol{\tau}} + \alpha\frac{\lambda}{\eta_p}\boldsymbol{\tau}\cdot\boldsymbol{\tau} = 2\eta_p\boldsymbol{D}
$$
这里的 $\alpha$ 是一个无量纲的 **各向异性参数** 或 **迁移率参数**。

#### 物理起源

Giesekus模型的物理基础源于对聚合物链在溶液中所受[流体动力](@entry_id:750449)曳力的更精确描述。在线性的胡克哑铃模型中，构成哑铃的珠子被假设为在各向同性的介质中运动，其所受曳力与速度成正比且与方向无关。然而，当聚合物链被拉伸和取向时，它自身会扰动周围的溶剂场，导致珠子感受到的流体动力曳力变得 **各向异性 (anisotropic)**。也就是说，沿着[聚合物链取向](@entry_id:158341)方向的运动受到的阻力与垂直于该方向的运动受到的阻力不同。

这种构象依赖的、各向异性的曳力（或等效地，各向异性的迁移率张量）在宏观本构方程中最终表现为与应力张量二次方 ($\boldsymbol{\tau}\cdot\boldsymbol{\tau}$) 成正比的[非线性](@entry_id:637147)项。此项本质上是一个耗散项，因为它源于曳力，会增加系统的熵产。为了保证模型的物理实在性，即迁移率张量在任何构象下都必须是正定的，[热力学分析](@entry_id:142723)要求各向异性参数 $\alpha$ 必须在以下范围内：
$$
0 \le \alpha \le 1
$$
当 $\alpha=0$ 时，模型退化为 UCM 模型。

#### 流变学预测：非零的第二[法向应力差](@entry_id:199507)

Giesekus模型的一个关键成功之处在于它能够预测一个非零且通常为负的 **第二法向应力差 ($N_2$)**，这与实验观察结果相符。我们可以通过分析[稳态](@entry_id:139253)[简单剪切流](@entry_id:1131665)来揭示这一点。考虑速度场为 $\boldsymbol{v} = (\dot{\gamma}y, 0, 0)$，其中 $\dot{\gamma}$ 是恒定的剪切速率。

在[稳态](@entry_id:139253)和均匀流动的假设下，Giesekus方程的各个分量可以写成一组[代数方程](@entry_id:272665)。通过在小剪切速率（即小[魏森贝格数](@entry_id:262025) $\mathrm{Wi} = \lambda\dot{\gamma}$）下进行摄动展开，可以求解应力分量的最低阶表达式。 

应力分量的展开形式为：
- 剪切应力: $\tau_{12} = \eta_p\dot{\gamma} + \mathcal{O}(\dot{\gamma}^3)$
- [法向应力](@entry_id:260622): $\tau_{11} = c_{11}\dot{\gamma}^2 + \mathcal{O}(\dot{\gamma}^4)$, $\tau_{22} = c_{22}\dot{\gamma}^2 + \mathcal{O}(\dot{\gamma}^4)$, $\tau_{33}=0$

将这些展开式代入Giesekus方程的分量形式，并收集 $\mathcal{O}(\dot{\gamma}^2)$ 的项，经过推导可得：
$$
\tau_{11} \approx (2-\alpha)\lambda\eta_p\dot{\gamma}^2
$$
$$
\tau_{22} \approx -\alpha\lambda\eta_p\dot{\gamma}^2
$$
$$
\tau_{33} = 0
$$

第一法向应力差 $N_1 = \tau_{11} - \tau_{22}$ 和第二[法向应力差](@entry_id:199507) $N_2 = \tau_{22} - \tau_{33}$ 的领先阶表达式为：
$$
N_1 = [(2-\alpha) - (-\alpha)]\lambda\eta_p\dot{\gamma}^2 = 2\lambda\eta_p\dot{\gamma}^2
$$
$$
N_2 = -\alpha\lambda\eta_p\dot{\gamma}^2 - 0 = -\alpha\lambda\eta_p\dot{\gamma}^2
$$
这个结果非常重要。首先，它表明 $N_2$ 不为零，并且由于 $\alpha \gt 0$， $N_2$ 是负值，这与许多[聚合物流体](@entry_id:1129919)的实验数据定性一致。其次，我们可以计算这两个法向应力差的比值：
$$
\frac{N_2}{N_1} = \frac{-\alpha\lambda\eta_p\dot{\gamma}^2}{2\lambda\eta_p\dot{\gamma}^2} = -\frac{\alpha}{2}
$$
这个简洁的关系式直接将一个宏观可测量的流变学量（法向应力差之比）与模型的微观物理参数 $\alpha$ 联系起来，为通过实验数据确定模型参数提供了直接途径。

### [Phan-Thien-Tanner模型](@entry_id:1129555)：应力依赖的松弛

Phan-Thien-Tanner (PTT) 模型提供了另一种引入[非线性](@entry_id:637147)的物理途径。与 Giesekus模型修改曳力项不同，PTT模型假设[应力松弛](@entry_id:159905)过程本身受到聚合物链伸展状态的影响。其通用形式为：
$$
f(\mathrm{tr}\,\boldsymbol{\tau})\boldsymbol{\tau} + \lambda\overset{\nabla}{\boldsymbol{\tau}} = 2\eta_p\boldsymbol{D}
$$
其中 $f$ 是一个依赖于应力张量迹 $\mathrm{tr}\,\boldsymbol{\tau}$ 的标量函数，$\mathrm{tr}\,\boldsymbol{\tau}$ 反映了聚合物链的平均伸展程度。

#### 物理起源

PTT模型的微观起源通常从[聚合物网络](@entry_id:191902)理论中寻找解释。在高浓度体系中，聚合物链相互缠结形成一个瞬时网络。当[流体变形](@entry_id:271538)时，网络节点（缠结点）会随之运动。然而，在强流场下，链段可能会从缠结点滑脱，或者缠结点自身可能解开并重新形成，这个过程称为 **网络滑移 (network slip)** 或构象释放。

这种滑移机制意味着聚合物链的松弛速率会随着其伸展程度的增加而加快。PTT模型通过引入函数 $f(\mathrm{tr}\,\boldsymbol{\tau})$ 来唯象地描述这一效应。为了与线性响应一致，$f$ 必须满足在应力趋于零时 $f \to 1$。常见的 $f$ 函数形式包括：
- **线性 PTT 模型**: $f(\mathrm{tr}\,\boldsymbol{\tau}) = 1 + \epsilon \frac{\lambda}{\eta_p} \mathrm{tr}\,\boldsymbol{\tau}$
- **指数 PTT 模型**: $f(\mathrm{tr}\,\boldsymbol{\tau}) = \exp\left(\epsilon \frac{\lambda}{\eta_p} \mathrm{tr}\,\boldsymbol{\tau}\right)$

这里的 $\epsilon$ 是一个无量纲参数，表征了应力对松弛速率的影响强度。[热力学稳定性](@entry_id:142877)和流变学稳定性（如剪切应力随剪切速率单调增加）通常要求 $\epsilon \ge 0$。

#### 流变学预测：零值的第二法向应力差

与 Giesekus模型相比，PTT模型在预测[法向应力](@entry_id:260622)方面表现出显著差异。我们同样考虑线性 PTT 模型在[稳态](@entry_id:139253)[简单剪切流](@entry_id:1131665)中的小剪切速率极限。

在 $\mathcal{O}(\dot{\gamma})$ 阶，PTT模型与 Giesekus和 UCM 模型一样，给出 $\tau_{12}^{(1)} = \eta_p \dot{\gamma}$，并且 $\mathrm{tr}\,\boldsymbol{\tau}^{(1)} = 0$。在分析 $\mathcal{O}(\dot{\gamma}^2)$ 阶的项时，PTT模型的[非线性](@entry_id:637147)项 $(\epsilon \frac{\lambda}{\eta_p} \mathrm{tr}\,\boldsymbol{\tau})\boldsymbol{\tau}$ 变为 $(\epsilon \frac{\lambda}{\eta_p} \mathrm{tr}\,\boldsymbol{\tau}^{(2)})\boldsymbol{\tau}^{(1)}$，这比 $\boldsymbol{\tau}^{(2)}$ 是更高阶的项。因此，在 $\mathcal{O}(\dot{\gamma}^2)$ 阶，PTT模型的方程简化为与 UCM 模型完全相同的形式：
$$
\boldsymbol{\tau}^{(2)} + \lambda\overset{\nabla}{\boldsymbol{\tau}}^{(1)} = \boldsymbol{0}
$$
求解可得：
$$
\tau_{11} \approx 2\lambda\eta_p\dot{\gamma}^2
$$
$$
\tau_{22} \approx 0
$$
$$
\tau_{33} = 0
$$
因此，线性PTT模型在小剪切速率下的[法向应力差](@entry_id:199507)预测为：
$$
N_1 = 2\lambda\eta_p\dot{\gamma}^2
$$
$$
N_2 = 0
$$
这个结果表明，至少在其最简单的形式下，PTT模型无法像 Giesekus模型那样预测出非零的 $N_2$。这是一个关键的区别，意味着这两种模型捕捉了不同的[物理非线性](@entry_id:276205)机制。

### 对比分析与极限行为

Giesekus模型和PTT模型代表了构建[非线性](@entry_id:637147)[微分](@entry_id:158422)[本构方程](@entry_id:138559)的两种不同哲学：
- **Giesekus模型**：通过引入 **各向异性耗散**（曳力）来产生[非线性](@entry_id:637147)，其[非线性](@entry_id:637147)项是张量二次型 ($\boldsymbol{\tau}\cdot\boldsymbol{\tau}$)。
- **PTT模型**：通过引入 **各向同性、依赖于应力大小的松弛机制** 来产生[非线性](@entry_id:637147)，其[非线性](@entry_id:637147)项是标量函数乘以应力张量 ($f(\mathrm{tr}\,\boldsymbol{\tau})\boldsymbol{\tau}$)。

尽管它们的物理起源和数学结构不同，导致了在预测 $N_2$ 等[流变性](@entry_id:152243)质上的差异，但这两个模型共享一个重要的共同点：它们都是对 UCM 模型的系统性扩展。在小形变极限下（$\mathrm{Wi} \to 0$），两种模型的[非线性](@entry_id:637147)项都比线性项高阶，因此它们都自然地退化为 UCM 模型。 这不仅是模型构建的一个一致性检验，也意味着在小应变下，这些复杂的[非线性](@entry_id:637147)效应是观察不到的，这符合物理直觉。

在实际应用中，选择哪种模型取决于所研究的特定聚合物体系及其关键的[流变学](@entry_id:138671)特征。如果实验数据明确显示存在显著的第二法向应力差，Giesekus模型可能是更合适的选择。如果体系的主要[非线性](@entry_id:637147)行为是强烈的剪切致稀和拉伸[硬化](@entry_id:177483)，而 $N_2$ 相对不重要，那么 PTT模型（特别是其指数形式）可能更受青睐，因为它通常能更好地拟合这些行为。在[计算流体力学](@entry_id:747620)模拟中，这两种模型及其变体为预测和理解复杂几何构型中的[非牛顿流动](@entry_id:275095)提供了强大而灵活的工具。