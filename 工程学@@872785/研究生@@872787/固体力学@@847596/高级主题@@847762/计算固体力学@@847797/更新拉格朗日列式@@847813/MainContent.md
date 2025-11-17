## 引言
在现代工程与科学领域，精确模拟材料和结构在经历大变形、大转动时的力学行为至关重要。传统的线性分析方法在这种[非线性](@entry_id:637147)场景下已不再适用，这催生了以[有限元法](@entry_id:749389)为基础的多种[非线性](@entry_id:637147)分析框架。其中，如何选择合适的参考构型来描述运动和计算平衡，是区分不同数值列式法（如全量拉格朗日法与更新拉格朗日法）的关键。更新拉格朗日（Updated Lagrangian, UL）列式法通过一个不断更新的参考构型，为处理一类特定的复杂问题（如材料历史依赖性、接触和几何失稳）提供了强大而自然的框架，但其背后的力学原理和计算细节对许多研究者而言仍是一个挑战。

本文旨在系统性地剖析更新拉格朗日列式法的理论精髓与实践应用。读者将通过本文的学习，建立一个从基本概念到高级应用的完整知识体系。文章将分为三个核心部分：首先，在“原理和机制”一章中，我们将深入探讨UL列式法的基本思想、增量运动学、[客观应力率](@entry_id:199282)以及控制方程的推导，为后续内容奠定坚实的理论基础。接着，在“应用与跨学科联系”一章中，我们将展示该理论如何转化为强大的计算工具，应用于[弹塑性](@entry_id:193198)、[接触力学](@entry_id:177379)、[结构稳定性](@entry_id:147935)等前沿问题。最后，“动手实践”部分将提供具体的思考题，帮助读者巩固对关键概念的理解和应用能力。通过这一结构化的学习路径，本文将引导您全面掌握更新拉格朗日这一[非线性固体力学](@entry_id:171757)的核心方法。

## 原理和机制

本章深入探讨更新拉格朗日（Updated Lagrangian, UL）列式法的核心原理与力学机制。我们将从其基本思想出发，逐步建立描述增量运动的[运动学](@entry_id:173318)框架，探索适用于该框架下的应力率和[应变率](@entry_id:154778)，并最终推导其控制方程的[弱形式](@entry_id:142897)及其线性化，为有限元方法的实现奠定理论基础。

### 核心思想：一个移动的参考[坐标系](@entry_id:156346)

在[非线性](@entry_id:637147)连续介质力学中，为了求解一个随[时间演化](@entry_id:153943)的问题，我们通常将其离散为一系列增量步。如何描述和计算每个增量步的力学行为，是不同数值列式法的核心区别。更新拉格朗日列式法的根本特征在于其参考构型的选择。

与始终采用初始未变形构型 $\Omega_0$作为唯一参考的“全量拉格朗日”（Total Lagrangian, TL）列式法不同，更新拉格朗日法采用一种“移动”或“更新”的参考构型。具体来说，对于从时间 $t_n$ 到 $t_{n+1}$ 的任意一个分析步，UL列式法将该增量步开始时的构型 $\Omega_n$ 作为求解该步的参考构型 [@problem_id:2709110]。构型 $\Omega_n$ 在上一步计算中是未知的，但在当前步开始时是已知的。

这种策略具有几个显著优点。首先，由于参考构型 $\Omega_n$ 与待求解的当前构型 $\Omega_{n+1}$ 在几何上“接近”，因此基于该参考构型的运动学量（如[位移梯度](@entry_id:165352)）通常是小量，这为问题的线性化带来了便利。其次，对于材料历史依赖性较弱或经历极端变形（如金属成型或流体）的问题，初始构型可能变得不再重要，甚至会因网格严重畸变而导致数值困难。在这些情况下，始终基于当前最新构型进行计算显得更为自然和稳健。

### 增量[运动学](@entry_id:173318)

为了精确描述UL列式法中的变形，我们必须仔细定义各个构型之间的映射关系。设物[质点](@entry_id:186768)在初始构型 $\mathcal{B}_0$ 中的位置为 $\mathbf{X}$，在 $t_n$ 时刻构型 $\mathcal{B}_n$ 中的位置为 $\mathbf{x}_n$，在 $t_{n+1}$ 时刻构型 $\mathcal{B}_{n+1}$ 中的位置为 $\mathbf{x}_{n+1}$。

总变形梯度 $\mathbf{F}_n$ 描述了从初始构型 $\mathcal{B}_0$ 到 $t_n$ 时刻构型 $\mathcal{B}_n$ 的映射：$\mathbf{F}_n = \partial \mathbf{x}_n / \partial \mathbf{X}$。
在UL列式法中，我们关注的核心是描述从 $t_n$ 到 $t_{n+1}$ 这一步的运动。该运动可以由一个**增量变形梯度**（incremental deformation gradient）$\mathbf{f}_{n+1}$ 来刻画，它定义为当前位置 $\mathbf{x}_{n+1}$ 相对于[参考位](@entry_id:754187)置 $\mathbf{x}_n$ 的梯度 [@problem_id:2709075]：
$$ \mathbf{f}_{n+1} = \frac{\partial \mathbf{x}_{n+1}}{\partial \mathbf{x}_n} $$
这里的梯度运算是针对构型 $\mathcal{B}_n$ 的坐标进行的。

总变形和增量变形之间的关系可以通过[链式法则](@entry_id:190743)联系起来。从 $\mathcal{B}_0$ 到 $\mathcal{B}_{n+1}$ 的总变形梯度 $\mathbf{F}_{n+1}$ 可以看作是先从 $\mathcal{B}_0$ 映射到 $\mathcal{B}_n$，再从 $\mathcal{B}_n$ 映射到 $\mathcal{B}_{n+1}$ 的复合映射。因此，我们得到总变形梯度的**乘法更新法则**：
$$ \mathbf{F}_{n+1} = \frac{\partial \mathbf{x}_{n+1}}{\partial \mathbf{X}} = \frac{\partial \mathbf{x}_{n+1}}{\partial \mathbf{x}_n} \frac{\partial \mathbf{x}_n}{\partial \mathbf{X}} = \mathbf{f}_{n+1} \mathbf{F}_n $$
这个[乘法分解](@entry_id:199514)是有限变形理论的基石，它清晰地展示了总变形是如何通过一系列增量步累积起来的 [@problem_id:2709075]。

由于UL列式法的所有计算都在当前构型上进行，采用定义在空间构型上的[应变度量](@entry_id:755495)就显得尤为自然。**[欧拉-阿尔曼西应变张量](@entry_id:194948)**（Euler-Almansi strain tensor）$\mathbf{e}$ 就是这样一个例子。它定义为：
$$ \mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{b}^{-1}) $$
其中 $\mathbf{I}$ 是单位张量，$\mathbf{b} = \mathbf{F}\mathbf{F}^T$ 是左柯西-格林变形张量（Finger张量）。[欧拉-阿尔曼西应变](@entry_id:187104) $\mathbf{e}$ 与定义在物质构型上的[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})$ 之间存在一个推前（push-forward）变换关系：$\mathbf{e} = \mathbf{F}^{-T} \mathbf{E} \mathbf{F}^{-1}$ [@problem_id:2709088]。

在UL增量分析中，$\mathbf{e}$ 的一个重要特性是其线性化形式。对于一个微小的增量位移 $\delta\mathbf{u}$，其增量[欧拉-阿尔曼西应变](@entry_id:187104)近似等于该[位移场](@entry_id:141476)的[无穷小应变张量](@entry_id:167211) [@problem_id:2709088]：
$$ \delta\mathbf{e} \approx \frac{1}{2}(\nabla(\delta\mathbf{u}) + \nabla(\delta\mathbf{u})^T) $$
这使得它在增量迭代求解的框架下非常易于使用。

### [运动学](@entry_id:173318)率与[客观应力率](@entry_id:199282)

在UL列式法中，我们经常需要处理与时间相关的变化率，例如材料的本构关系通常以率形式给出。**[空间速度梯度](@entry_id:187198)**（spatial velocity gradient）$\mathbf{l}$ 是描述当前构型中[速度场](@entry_id:271461) $\mathbf{v}$ 空间变化的中心量，定义为 $\mathbf{l} = \nabla_{\mathbf{x}}\mathbf{v}$。

速度梯度 $\mathbf{l}$ 可以唯一地分解为一个对称部分和一个反对称部分：
$$ \mathbf{l} = \mathbf{d} + \mathbf{w} $$
其中，**变形率张量**（rate of deformation tensor）或伸长率张量（stretching tensor）$\mathbf{d} = \frac{1}{2}(\mathbf{l} + \mathbf{l}^T)$ 描述了材料微元的拉伸和剪切变形速率。**[自旋张量](@entry_id:187346)**（spin tensor）$\mathbf{w} = \frac{1}{2}(\mathbf{l} - \mathbf{l}^T)$ 描述了材料微元的[刚体转动](@entry_id:191086)速率 [@problem_id:2709057]。

变形率[张量的迹](@entry_id:190669)与体积变化率直接相关。变形梯度的[行列式](@entry_id:142978) $J = \det \mathbf{F}$ 代表了体积的变化率，其[物质时间导数](@entry_id:190892)满足一个重要的运动学恒等式 [@problem_id:2709057]：
$$ \dot{J} = J \cdot \mathrm{tr}(\mathbf{l}) = J \cdot \mathrm{tr}(\mathbf{d}) $$
这表明，材料的体积变化率完全由变形率[张量的迹](@entry_id:190669)（即[速度场](@entry_id:271461)的散度）决定。

在构建本构关系时，一个至关重要的原则是**[物质客观性原理](@entry_id:191727)**（Principle of Material Frame-Indifference），即材料的本构响应不应依赖于观察者。这意味着[本构方程](@entry_id:138559)中使用的所有量都必须是“客观的”。然而，柯西应力 $\boldsymbol{\sigma}$ 的标准[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$ 并不是一个[客观率](@entry_id:198692)，因为它会受到观察者刚性转动的影响。

为了解决这个问题，我们需要引入**[客观应力率](@entry_id:199282)**（objective stress rates）。这些应力率通过修正 $\dot{\boldsymbol{\sigma}}$ 来消除[刚体转动](@entry_id:191086)的影响。**Jaumann率**（或称 co-rotational rate）是其中最常用的一种，其定义为 [@problem_id:2709097]：
$$ \boldsymbol{\sigma}^{\nabla} = \dot{\boldsymbol{\sigma}} - \mathbf{w}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{w} $$
这里的修正项 $\mathbf{w}\boldsymbol{\sigma} - \boldsymbol{\sigma}\mathbf{w}$ 恰好抵消了在叠加[刚体转动](@entry_id:191086)时 $\dot{\boldsymbol{\sigma}}$ 中出现的非客观项，从而使得 $\boldsymbol{\sigma}^{\nabla}$ 成为一个客观张量 [@problem_id:2709097] [@problem_id:2709057]。

另一个重要的[客观率](@entry_id:198692)是**[Truesdell率](@entry_id:181014)**。它与Jaumann率的关系为 [@problem_id:2709106]：
$$ \overset{\circ}{\boldsymbol{\sigma}} = \boldsymbol{\sigma}^{\nabla} - (\mathbf{d}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{d}) + (\mathrm{tr}\mathbf{d})\boldsymbol{\sigma} $$
可以看出，两者在一般情况下并不相同。对于一个从势函数（[应变能](@entry_id:162699)）导出的[超弹性材料](@entry_id:190241)，其率形式的本构关系与[Truesdell率](@entry_id:181014)（或等价地，[Kirchhoff应力](@entry_id:751039)的Oldroyd率）天然相容，保证了路径无关性。然而，如果使用一个简单的率形式本构（即所谓的“[亚弹性](@entry_id:204371)”模型），例如将Jaumann率与一个常数弹性模量张量相关联，可能会在某些变形路径（如大[剪切变形](@entry_id:170920)）下产生非物理的应力[振荡](@entry_id:267781)，这正是因为这种本构关系通常是不可积的，即不存在一个对应的[应变能函数](@entry_id:178435) [@problem_id:2709106]。因此，在可能的情况下，使用基于[超弹性](@entry_id:159356)的本构模型是更可靠的选择。

### 应力度量及其变换

在有限变形框架中，存在多种应力度量，它们定义在不同的构型上。UL列式法要求我们能够在不同构型之间自如地转换这些度量。
- **柯西应力 (Cauchy Stress)** $\boldsymbol{\sigma}$：定义在当前构型上的真实应力，表示单位当前面积上的力。
- **第二类[皮奥拉-基尔霍夫应力](@entry_id:173629) (Second Piola-Kirchhoff Stress)** $\mathbf{S}$：定义在参考构型上的一个对称应力度量，它与[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$ 能量共轭。
- **[基尔霍夫应力](@entry_id:751039) (Kirchhoff Stress)** $\boldsymbol{\tau}$：定义为 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$，在处理大变形塑性和体积[不可压缩性](@entry_id:274914)时非常有用。

这些[应力张量](@entry_id:148973)之间的转换关系源于跨越变形后和参考构型面元的牵引力平衡。最核心的转换公式将第二类PK应力 $\mathbf{S}$ 和柯西应力 $\boldsymbol{\sigma}$ 联系起来 [@problem_id:2609697]：
$$ \boldsymbol{\sigma} = J^{-1} \mathbf{F} \mathbf{S} \mathbf{F}^T $$
$$ \mathbf{S} = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T} $$

这些变换可以被形式化地定义为**推前（push-forward）**和**[拉回](@entry_id:160816)（pull-back）**操作。将一个定义在参考构型上的张量（如$\mathbf{S}$）映射到当前构型（得到$\boldsymbol{\sigma}$）的过程是推前操作。反之，将一个定义在当前构型上的张量映射到参考构型是[拉回](@entry_id:160816)操作 [@problem_id:2709066]。这些操作的力学意义在于，它们通过变形梯度 $\mathbf{F}$ 和[雅可比行列式](@entry_id:137120) $J$ 准确地计入了微元面积的大小和方向的变化，从而保证了力学等效性 [@problem_id:2709066]。在UL的增量步中，这些变换将上一时刻的应力状态或通过本构律计算出的（相对于$t_n$构型的）应力增量，正确地转换到当前构型$t_{n+1}$中，以用于平衡方程的求解。

### 控制方程：虚功原理及其线性化

UL列式法的基础是建立在当前构型 $\Omega_t$ 上的平衡方程。在忽略[惯性力](@entry_id:169104)的准静态情况下，[局部平衡](@entry_id:156295)方程为：
$$ \nabla_{\mathbf{x}} \cdot \boldsymbol{\sigma} + \rho \mathbf{b} = \mathbf{0} $$
其中 $\rho$ 是当前密度，$\mathbf{b}$ 是单位质量的[体力](@entry_id:174230)。

利用虚功原理，我们可以将上述强形式的[微分方程](@entry_id:264184)转化为一个等价的积分弱形式。通过将平衡方程与任意满足[位移边界条件](@entry_id:203261)的[虚位移](@entry_id:168781)场 $\delta\mathbf{u}$ 做[点积](@entry_id:149019)并在当前体积上积分，再利用[高斯散度定理](@entry_id:188065)，可以得到 [@problem_id:2609717]：
$$ \int_{\Omega_t} \boldsymbol{\sigma} : \delta \mathbf{d} \, dv = \int_{\Omega_t} \rho\mathbf{b} \cdot \delta\mathbf{u} \, dv + \int_{\partial\Omega_t^t} \bar{\mathbf{t}} \cdot \delta\mathbf{u} \, da $$
其中 $\delta\mathbf{d}$ 是虚变形率张量，即虚[位移梯度](@entry_id:165352)的对称部分。这个方程即为UL列式法中的**[虚功原理](@entry_id:138749)**。它明确指出了在空间构型描述中，柯西应力 $\boldsymbol{\sigma}$ 与变形率张量 $\mathbf{d}$ 是能量共轭的。

在[有限元分析](@entry_id:138109)中，上述[非线性方程](@entry_id:145852)通常通过牛顿-拉夫逊（[Newton-Raphson](@entry_id:177436)）等[迭代法](@entry_id:194857)求解。这需要对[虚功](@entry_id:176403)方程进行**一致性线性化**（consistent linearization），以得到**[切线刚度矩阵](@entry_id:170852)**。对[内虚功](@entry_id:172278)项 $\int \boldsymbol{\sigma} : \delta\mathbf{d} \, dv$ 关于增量位移 $\Delta\mathbf{u}$ 进行线性化，会产生两个部分：

1.  **[材料刚度](@entry_id:158390) (Material Stiffness)**：源于应力对应变的本构响应，即应力增量与应变增量之间的关系，由材料的[切线](@entry_id:268870)模量张量决定。
2.  **[几何刚度](@entry_id:172820) (Geometric Stiffness)** 或 **初应力刚度 (Initial Stress Stiffness)**：这一部分不依赖于材料的本构模量，而是纯粹由当前存在的应力状态 $\boldsymbol{\sigma}$ 以及增量变形的几何效应（转动和拉伸）引起 [@problem_id:2709084]。

[几何刚度](@entry_id:172820)项来源于将更新构型中的内力项[拉回](@entry_id:160816)到当前参考构型并进行线性化的过程。它本质上是对应力张量的推前操作和积分域变化进行线性化的结果。其最终的双线性形式为 [@problem_id:2709084]：
$$ K_{\text{geo}}(\boldsymbol{\eta}, \Delta\mathbf{u}) = \int_{\Omega} \mathrm{tr}(\boldsymbol{\sigma} (\nabla\boldsymbol{\eta})^T \nabla(\Delta\mathbf{u})) \, dv $$
其中 $\boldsymbol{\eta}$ 是测试函数（[虚位移](@entry_id:168781)）。这一项描述了现有应[力场](@entry_id:147325)对结构增量刚度的贡献，对于分析结构失稳（如屈曲）等问题至关重要，是所有[非线性固体力学](@entry_id:171757)分析的核心组成部分。