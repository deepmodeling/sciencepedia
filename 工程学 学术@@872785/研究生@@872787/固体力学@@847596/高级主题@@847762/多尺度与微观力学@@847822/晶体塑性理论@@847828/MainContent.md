## 引言
[晶体塑性](@entry_id:141273)理论是[固体力学](@entry_id:164042)与[材料科学](@entry_id:152226)领域中的一个核心理论，它旨在建立一个从微观[晶体结构](@entry_id:140373)出发，以预测材料宏观力学响应的定量框架。金属等晶体材料在受力时表现出的复杂行为，如屈服、加工硬化、各向异性等，其根源都深植于其微观结构中[位错](@entry_id:157482)的运动与演化。然而，如何在[连续介质力学](@entry_id:155125)的宏观描述与[位错滑移](@entry_id:275474)的离散微观物理之间建立一座坚实的桥梁，是理解和设计先进工程材料所面临的关键挑战。本文旨在系统地解决这一问题，为读者提供一个关于[晶体塑性](@entry_id:141273)理论的全面而深入的理解。

在接下来的内容中，我们将分步构建[晶体塑性](@entry_id:141273)理论的完整图景。**第一章：原理与机制** 将深入探讨理论的基石，从定义塑性变形的基本单元——[晶体学滑移](@entry_id:196486)系开始，详细阐述驱动滑移的[Schmid定律](@entry_id:160968)、描述大变形[运动学](@entry_id:173318)的[乘法分解](@entry_id:199514)框架，以及建立滑移率和硬化演化的[本构模型](@entry_id:174726)。**第二章：应用与跨学科联系** 将展示该理论的强大威力，探讨如何利用它进行从单晶到多晶体的多尺度建模，解释[霍尔-佩奇效应](@entry_id:144956)、织构演化和[循环加载](@entry_id:181502)等关键材料现象，并介绍其在前沿领域的拓展。最后，**第三章：动手实践** 将通过具体的计算练习，引导读者亲手应用所学知识，计算分[切应力](@entry_id:137139)、求解滑移速率，并实现本构模型的[数值积分](@entry_id:136578)，从而将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，读者将能够掌握[晶体塑性](@entry_id:141273)理论的精髓，并领会其在现代材料研究与工程设计中的重要作用。

## 原理与机制

[晶体塑性](@entry_id:141273)理论旨在建立一个连接微观[晶体结构](@entry_id:140373)与宏观力学行为的预测性框架。其核心在于，金属等晶体材料的不可恢复变形（即塑性变形）主要是由晶体内部特定[晶面](@entry_id:166481)和[晶向](@entry_id:137393)上[位错](@entry_id:157482)的滑移所介导的。本章将系统地阐述[晶体塑性](@entry_id:141273)理论的基本原理与核心机制，从定义塑性变形的基本单元——滑移系开始，逐步建立起描述其激活的力学准则、变形运动学、以及控制其演化的本构关系。

### [晶体学滑移](@entry_id:196486)：塑性变形的根源

晶体材料的塑性变形并非在任意方向上均匀发生，而是局域在特定的[晶体学](@entry_id:140656)平面和方向上。这种局域化的剪切变形被称为**滑移（slip）**。一个滑移由一个**[滑移面](@entry_id:158709)（slip plane）**和一个位于该平面内的**滑移方向（slip direction）**共同定义，二者构成一个**滑移系（slip system）**。

从物理上看，滑移之所以发生在特定的[晶体学](@entry_id:140656)平面和方向上，是因为它遵循[能量最小化](@entry_id:147698)原则。[位错](@entry_id:157482)的滑移本质上是原子键的断裂和重组过程。这一过程在原子[排列](@entry_id:136432)最紧密的晶面上以及沿着原子最密排的方向上遇到的阻力最小。因此，滑移倾向于发生在具有最高原子[面密度](@entry_id:161889)（planar atomic density）的晶面上，并沿着具有最高原子[线密度](@entry_id:158735)（linear atomic density）的方向进行。滑移方向也对应于定义完美[位错](@entry_id:157482)的**伯格斯矢量（Burgers vector）** $\boldsymbol{b}$ 的方向，它代表了[晶格](@entry_id:196752)中最短的平移矢量。[@problem_id:2628543]

不同[晶体结构](@entry_id:140373)由于其原子[排列](@entry_id:136432)方式不同，具有不同的主导滑移系。晶体的[点群对称性](@entry_id:141230)决定了一个[滑移系](@entry_id:136401)族（例如，特定类型的晶面和方向）中包含多少个等效的、可以被激活的独立滑移系。

- **[面心立方](@entry_id:156319)（Face-Centered Cubic, FCC）晶体**：如铝（Al）、铜（Cu）、镍（Ni）等。其最密排面是 $\{111\}$ 族[晶面](@entry_id:166481)，最密排方向是 $\langle 110 \rangle$ 族方向。因此，FCC晶体的主导[滑移系](@entry_id:136401)族是 $\{111\}\langle 110 \rangle$。由于立方晶系的高度对称性，存在4个不等价的 $\{111\}$ [晶面](@entry_id:166481)，每个[晶面](@entry_id:166481)内包含3个不等价的 $\langle 110 \rangle$ 方向，总计 $4 \times 3 = 12$ 个等效[滑移系](@entry_id:136401)。

- **体心立方（Body-Centered Cubic, BCC）晶体**：如铁（Fe）、钨（W）、钼（Mo）等。[BCC晶格](@entry_id:146999)中没有真正的密排面。其最密排方向是连接立方体顶点和体心原子的 $\langle 111 \rangle$ 方向，这也是其[伯格斯矢量](@entry_id:160637)的方向。实验观察和[原子模拟](@entry_id:199973)均表明，BCC金属中的螺[位错核心](@entry_id:201451)结构复杂且非平面化，导致其可以在多个包含 $\langle 111 \rangle$ 方向的晶面上滑移。最常见的滑移面族是 $\{110\}$、$\{112\}$ 和 $\{123\}$。若将这三个面族上所有可能的[滑移系](@entry_id:136401)都考虑在内，BCC晶体可用的滑移系总数非常多（$\{110\}\langle 111 \rangle$ 有12个，$\{112\}\langle 111 \rangle$ 有12个，$\{123\}\langle 111 \rangle$ 有24个，总计48个），这解释了BCC金属良好的塑性。[@problem_id:2628543]

- **密排六方（Hexagonal Close-Packed, HCP）晶体**：如镁（Mg）、钛（Ti）、锌（Zn）等。由于其较低的六方对称性，HCP晶体的滑移行为具有显著的各向异性。其[滑移系](@entry_id:136401)通常被分为几类，激活它们所需的应力也大不相同：
    - **基面滑移（Basal Slip）**：在最密排的基面 $\{0001\}$ 上沿 $\langle 11\bar{2}0 \rangle$ 方向滑移。共存在3个[滑移系](@entry_id:136401)。
    - **柱面滑移（Prismatic Slip）**：在柱面 $\{10\bar{1}0\}$ 上沿 $\langle 11\bar{2}0 \rangle$ 方向滑移。共存在3个滑移系。
    - **锥面滑移（Pyramidal Slip）**：为了协调c轴方向的变形，需要激活具有c轴分量[伯格斯矢量](@entry_id:160637)的[滑移系](@entry_id:136401)。最常见的是在 $\{10\bar{1}1\}$ 锥面上沿 $\langle 11\bar{2}3 \rangle$ 方向的滑移（称为 $\langle c+a \rangle$ 滑移），这类[滑移系](@entry_id:136401)有12个。

[滑移系](@entry_id:136401)的数目和种类对材料的塑性变形能力至关重要。根据[von Mises准则](@entry_id:164472)，为了能够适应任意形状的塑性变形，晶体需要至少5个独立的[滑移系](@entry_id:136401)。FCC晶体拥有12个[滑移系](@entry_id:136401)，远超此要求，因此通常表现出优异的[延展性](@entry_id:160108)。而HCP晶体，尤其是当锥面滑移难以激活时，其有限的滑移系数量会导致其塑性变形能力受限和显著的各向异性。

### 驱动力与激活准则：[Schmid定律](@entry_id:160968)

当一个晶体承受外部载荷时，内部会产生一个应[力场](@entry_id:147325)，由**柯西应力张量（Cauchy stress tensor）** $\boldsymbol{\sigma}$ 描述。这个宏观应力如何在微观的滑移系上产生驱动力，从而引发塑性滑移呢？答案是**分[切应力](@entry_id:137139)（resolved shear stress）**。

对于一个由单位滑移方向矢量 $\boldsymbol{s}^{\alpha}$ 和单位[滑移面](@entry_id:158709)法向矢量 $\boldsymbol{m}^{\alpha}$ 定义的[滑移系](@entry_id:136401) $\alpha$（其中 $\boldsymbol{s}^{\alpha} \cdot \boldsymbol{m}^{\alpha} = 0$），作用在该滑移面上的牵[引力](@entry_id:175476)矢量为 $\boldsymbol{t}(\boldsymbol{m}^{\alpha}) = \boldsymbol{\sigma} \cdot \boldsymbol{m}^{\alpha}$。分[切应力](@entry_id:137139) $\tau^{\alpha}$ 定义为这个牵[引力](@entry_id:175476)矢量在滑移方向上的分量：
$$ \tau^{\alpha} = \boldsymbol{t}(\boldsymbol{m}^{\alpha}) \cdot \boldsymbol{s}^{\alpha} = (\boldsymbol{\sigma} \cdot \boldsymbol{m}^{\alpha}) \cdot \boldsymbol{s}^{\alpha} $$
这个标量值 $\tau^{\alpha}$ 代表了作用在滑移系 $\alpha$ 上、促使[位错](@entry_id:157482)沿滑移方向运动的有效[剪切应力](@entry_id:137139)。

为了在张量运算中更方便地处理，我们引入**Schmid张量（Schmid tensor）**，定义为滑移方向和[滑移面](@entry_id:158709)法向的并矢：
$$ \mathbf{S}^{\alpha} = \mathbf{s}^{\alpha} \otimes \mathbf{m}^{\alpha} $$
利用张量[双点积](@entry_id:748648)的定义 $\mathbf{A} : \mathbf{B} = \operatorname{tr}(\mathbf{A}^{\mathsf{T}} \mathbf{B})$，分切应力可以简洁地表示为[应力张量](@entry_id:148973)与Schmid张量的[双点积](@entry_id:748648)：[@problem_id:2628513]
$$ \tau^{\alpha} = \boldsymbol{\sigma} : \mathbf{S}^{\alpha} $$
Schmid张量具有一些重要的性质。首先，由于 $\boldsymbol{s}^{\alpha}$ 与 $\boldsymbol{m}^{\alpha}$ 正交，它的迹为零：$\operatorname{tr}(\mathbf{S}^{\alpha}) = \boldsymbol{s}^{\alpha} \cdot \boldsymbol{m}^{\alpha} = 0$。这意味着分[切应力](@entry_id:137139)不受静水压力的影响，因为[静水压力](@entry_id:275365)部分 $\boldsymbol{\sigma}_p = p\mathbf{I}$ 与Schmid张量的[双点积](@entry_id:748648)为 $p\mathbf{I} : \mathbf{S}^{\alpha} = p \operatorname{tr}(\mathbf{S}^{\alpha}) = 0$。这解释了为何金属的塑性变形在很大程度上是体积不变的。其次，Schmid张量通常是非对称的，即 $(\mathbf{S}^{\alpha})^{\mathsf{T}} = \mathbf{m}^{\alpha} \otimes \mathbf{s}^{\alpha} \neq \mathbf{S}^{\alpha}$。然而，由于柯西应力张量 $\boldsymbol{\sigma}$ 是对称的，分切应力只取决于Schmid[张量的对称部分](@entry_id:182434)，因为一个[对称张量](@entry_id:148092)与一个[反对称张量](@entry_id:199349)的[双点积](@entry_id:748648)恒为零。即 $\tau^{\alpha} = \boldsymbol{\sigma} : \operatorname{sym}(\mathbf{S}^{\alpha})$。[@problem_id:2628513]

**[Schmid定律](@entry_id:160968)（Schmid's law）**是[晶体塑性](@entry_id:141273)理论的基石，它提出了滑移的激活准则：当某个[滑移系](@entry_id:136401)上的分[切应力](@entry_id:137139) $\tau^{\alpha}$ 的[绝对值](@entry_id:147688)达到一个临界值时，该[滑移系](@entry_id:136401)便开始滑移。这个临界值被称为**临界分切应力（critical resolved shear stress, CRSS）**，记为 $\tau_{c}^{\alpha}$。$\tau_{c}^{\alpha}$ 是一个材料参数，反映了[晶格](@entry_id:196752)对[位错运动](@entry_id:143448)的本征阻力，它会随着材料的[硬化](@entry_id:177483)而增加。

对于理想的率无关塑性模型，[Schmid定律](@entry_id:160968)可以用一套Kuhn-Tucker[互补条件](@entry_id:747558)来精确表述：[@problem_id:2628492]
$$ |\tau^{\alpha}| \le \tau_{c}^{\alpha}, \quad \dot{\gamma}^{\alpha} \ge 0, \quad \dot{\gamma}^{\alpha} \left( |\tau^{\alpha}| - \tau_{c}^{\alpha} \right) = 0 $$
其中 $\dot{\gamma}^{\alpha}$ 是滑移系 $\alpha$ 上的滑移率。这组条件意味着：
- 如果 $|\tau^{\alpha}|  \tau_{c}^{\alpha}$，则滑移系处于非激活（弹性）状态，滑移率为零（$\dot{\gamma}^{\alpha} = 0$）。
- 如果[滑移系](@entry_id:136401)被激活（$\dot{\gamma}^{\alpha} > 0$），则分[切应力](@entry_id:137139)必须等于临界分切应力（$|\tau^{\alpha}| = \tau_{c}^{\alpha}$）。

### [大变形](@entry_id:167243)[运动学](@entry_id:173318)：[乘法分解](@entry_id:199514)

当材料经历大变形时，我们需要一个能够清晰区分弹性变形（可恢复的[晶格](@entry_id:196752)畸变）和塑性变形（不可恢复的滑移）的[运动学](@entry_id:173318)框架。由Lee等人提出的**变形梯度的[乘法分解](@entry_id:199514)（multiplicative decomposition of the deformation gradient）**为此提供了理论基础。

总的变形梯度 $\boldsymbol{F}$ 将材料从初始的参考构型映射到当前的变形构型。[乘法分解](@entry_id:199514)引入了一个概念性的、无应力的**[中间构型](@entry_id:193000)（intermediate configuration）**，并将总变形分解为两步：
$$ \boldsymbol{F} = \boldsymbol{F}^{e} \boldsymbol{F}^{p} $$
其中：
- **塑性变形梯度 $\boldsymbol{F}^{p}$**：描述了从参考构型到[中间构型](@entry_id:193000)的映射。它代表了由[位错滑移](@entry_id:275474)累积产生的纯塑性变形。这个过程重排了材料点，但保持了[晶格](@entry_id:196752)的局部取向和间距不变，因此是“[晶格](@entry_id:196752)不变”的变形。[位错滑移](@entry_id:275474)是剪切过程，不改变体积，因此塑性变形是保体积的，即 $\det(\boldsymbol{F}^{p}) = 1$。[@problem_id:2628512]
- **弹性变形梯度 $\boldsymbol{F}^{e}$**：描述了从[中间构型](@entry_id:193000)到当前构型的映射。它代表了[晶格](@entry_id:196752)的弹性畸变（拉伸和剪切）以及[刚体转动](@entry_id:191086)。这部分变形是可恢复的，其对应的机械功以弹性应变能的形式储存在材料中。

材料的储存能（亥姆霍兹自由能 $\Psi$）仅与弹性变形有关。为了满足[客观性原理](@entry_id:185412)（即能量不应随[刚体转动](@entry_id:191086)而改变），自由能必须是弹性应变度量的函数，通常选择**弹性[右柯西-格林张量](@entry_id:174156)（elastic right Cauchy-Green tensor）** $\boldsymbol{C}^{e} = (\boldsymbol{F}^{e})^{\mathsf{T}} \boldsymbol{F}^{e}$。

在率形式下，总的速度梯度 $\boldsymbol{L} = \dot{\boldsymbol{F}} \boldsymbol{F}^{-1}$ 可以分解为弹性部分和塑性部分的贡献。关键是定义在[中间构型](@entry_id:193000)中的**塑性速度梯度 $\boldsymbol{L}^{p}$**：
$$ \boldsymbol{L}^{p} = \dot{\boldsymbol{F}}^{p} (\boldsymbol{F}^{p})^{-1} = \sum_{\alpha} \dot{\gamma}^{\alpha} \boldsymbol{s}^{\alpha} \otimes \boldsymbol{m}^{\alpha} = \sum_{\alpha} \dot{\gamma}^{\alpha} \boldsymbol{S}^{\alpha} $$
这个方程是[晶体塑性](@entry_id:141273)理论的**[流动法则](@entry_id:177163)（flow rule）**的核心，它将宏观塑性变形率与所有滑移系上微观滑移率 $\dot{\gamma}^{\alpha}$ 的总和联系起来。由于 $\operatorname{tr}(\boldsymbol{S}^{\alpha}) = 0$，我们得到 $\operatorname{tr}(\boldsymbol{L}^{p}) = 0$，通过[雅可比公式](@entry_id:142453) $\frac{d}{dt}(\det \boldsymbol{F}^{p}) = (\det \boldsymbol{F}^{p}) \operatorname{tr}(\boldsymbol{L}^{p})$，这[直接证明](@entry_id:141172)了塑性流动的保体积特性。[@problem_id:2628512]

进一步，总速度梯度 $\boldsymbol{L}$ 可以分解为对称部分**变形率张量 $\boldsymbol{D}$** 和反对称部分**[涡量张量](@entry_id:189621)（或[自旋张量](@entry_id:187346)） $\boldsymbol{W}$**。[晶格](@entry_id:196752)的转动由**[晶格](@entry_id:196752)涡量 $\boldsymbol{W}^{e}$** 描述，它与材料的宏观涡量 $\boldsymbol{W}$ 和[塑性流动](@entry_id:201346)引起的**塑性[涡量](@entry_id:142747) $\boldsymbol{W}^{p}$** 相关联。一个精确的运动学关系将这些量联系起来，它对于正确追踪[晶格](@entry_id:196752)取向的演化至关重要，尤其是在模拟织构发展等问题中。[@problem_id:2628532]

### 本构模型：流动与硬化

为了使[晶体塑性](@entry_id:141273)理论成为一个完整的预测工具，我们需要为两个核心内部变量的演化指定[本构方程](@entry_id:138559)：滑移率 $\dot{\gamma}^{\alpha}$（[流动法则](@entry_id:177163)）和滑移阻力 $g^{\alpha}$（[硬化](@entry_id:177483)法则）。这里的 $g^{\alpha}$ 是临界分[切应力](@entry_id:137139) $\tau_{c}^{\alpha}$ 的一个更通用的表示，代表了[滑移系](@entry_id:136401) $\alpha$ 的当前强度。

#### 流动法则：黏塑性与[热激活](@entry_id:201301)

理想的率无关模型（[Schmid定律](@entry_id:160968)）是一种简化，它假设滑移的发生与加载速率无关。然而，在现实中，材料的塑性行为通常表现出对**[应变率](@entry_id:154778)**和**温度**的依赖性。这可以通过**黏塑性（viscoplastic）**模型来描述。

一个被广泛应用的黏[塑性流动法则](@entry_id:189597)是**[幂律](@entry_id:143404)（power-law）**形式：[@problem_id:2628526]
$$ \dot{\gamma}^{\alpha} = \dot{\gamma}_{0} \left| \frac{\tau^{\alpha}}{g^{\alpha}} \right|^{1/m} \mathrm{sgn}(\tau^{\alpha}) $$
- $\dot{\gamma}_{0}$ 是一个参考滑移率，具有 $\mathrm{s}^{-1}$ 的量纲。
- $g^{\alpha}$ 是[滑移系](@entry_id:136401) $\alpha$ 的当前滑移阻力或强度，具有应力量纲。
- $m$ 是**率敏感性指数（rate-sensitivity exponent）**，一个无量纲的正常数。$m$ 值越小，材料行为越接近率无关（即[应力-应变曲线](@entry_id:159459)在不同[应变率](@entry_id:154778)下差异很小）。当 $m \to 0$ 时，该[模型收敛](@entry_id:634433)于率无关的[Schmid定律](@entry_id:160968)。
- $\mathrm{sgn}(\tau^{\alpha})$ 函数确保滑移的方向与分切应力的方向一致。

这种形式的法则属于**过应力（overstress）**模型，意味着理论上任何非零的 $\tau^{\alpha}$ 都会导致非零的滑移率。然而，当 $|\tau^{\alpha}| \ll g^{\alpha}$ 且 $m$ 很小时，滑移率极小，可以忽略不计。只有当 $|\tau^{\alpha}|$ 接近或超过 $g^{\alpha}$ 时，滑移才变得显著。该[幂律](@entry_id:143404)形式保证了[塑性耗散](@entry_id:201273) $\mathcal{D}_{p} = \sum_{\alpha} \tau^{\alpha} \dot{\gamma}^{\alpha}$ 恒为非负，满足热力学第二定律的要求。[@problem_id:2628526]

这种对率和温度的依赖性有其深刻的物理根源，即**[热激活](@entry_id:201301)（thermal activation）**过程。[位错](@entry_id:157482)的运动需要克服一系列障碍物，这些障碍物根据其作用范围可分为两类：[@problem_id:2628507]
1.  **长程障碍物**：如其他[位错](@entry_id:157482)或[晶界](@entry_id:196965)，它们产生的应[力场](@entry_id:147325)范围较大，对温度不敏感。克服它们需要足够的机械外力。这部分贡献构成了**非热（athermal）**阻力，记为 $\tau_{\mathrm{a}}^{\alpha}$。
2.  **短程障碍物**：如Peierls势垒、杂质原子、空位等，它们的作用范围仅为几个原子间距。[位错](@entry_id:157482)可以在热能的帮助下（即原子的热[振动](@entry_id:267781)）以一定的概率“跳过”这些障碍。

因此，总的分切应力 $\tau^{\alpha}$ 可以看作由非热[部分和](@entry_id:162077)**热（thermal）**部分 $\tau_{\mathrm{t}}^{\alpha}$ 组成。真正驱动[热激活过程](@entry_id:274558)的有效应力是 $\tau_{\mathrm{eff}}^{\alpha} = |\tau^{\alpha}| - \tau_{\mathrm{a}}^{\alpha}$。根据过渡态理论，一个[热激活过程](@entry_id:274558)的发生频率遵循**阿伦尼乌斯（Arrhenius）**关系，其速率正比于 $\exp(-\Delta G / (k_B T))$，其中 $\Delta G$ 是激活能， $k_B$ 是[玻尔兹曼常数](@entry_id:142384)，$T$ 是绝对温度。

有效应力通过做功来降低激活能垒 $\Delta G$。一个典型的[热激活](@entry_id:201301)流动法则形式如下：[@problem_id:2628507]
$$ \dot{\gamma}^{\alpha} = \dot{\gamma}_{0}^{\alpha} \exp\left\{ -\frac{\Delta G^{\alpha}(\tau_{\mathrm{eff}}^{\alpha})}{k_B T} \right\} $$
其中激活能 $\Delta G^{\alpha}$ 是有效应力 $\tau_{\mathrm{eff}}^{\alpha}$ 的单调递减函数。一个常用的函数形式为：
$$ \Delta G^{\alpha} = \Delta F_{0}^{\alpha} \left[ 1 - \left( \frac{\tau_{\mathrm{eff}}^{\alpha}}{\hat{\tau}^{\alpha}} \right)^{p} \right]^{q} $$
这里 $\Delta F_{0}^{\alpha}$ 是没有外力辅助时的总能量势垒，$\hat{\tau}^{\alpha}$ 是克服障碍所需的纯机械应力，p和q是拟合参数。当 $\tau_{\mathrm{eff}}^{\alpha} \ge \hat{\tau}^{\alpha}$ 时，能量势垒消失，滑移不再需要[热激活](@entry_id:201301)。

#### [硬化](@entry_id:177483)法则：[位错](@entry_id:157482)的相互作用

材料在塑性变形过程中通常会变得越来越难以变形，这种现象称为**加工硬化（work hardening）**或**应变硬化（strain hardening）**。在[晶体塑性](@entry_id:141273)理论中，这表现为滑移阻力 $g^{\alpha}$ 随着塑性滑移的累积而增加。硬化的微观根源是位错密度的增加以及[位错](@entry_id:157482)之间的相互作用。

一个被广泛采用的唯象**[硬化](@entry_id:177483)法则（hardening law）**将 $g^{\alpha}$ 的演化率与所有[滑移系](@entry_id:136401)上的滑移率幅度关联起来：[@problem_id:2628517]
$$ \dot{g}^{\alpha} = \sum_{\beta} h_{\alpha\beta} |\dot{\gamma}^{\beta}| $$
- $h_{\alpha\beta}$ 是**硬化模量矩阵**。
- 对角项 $h_{\alpha\alpha}$ 描述了**自[硬化](@entry_id:177483)（self-hardening）**，即[滑移系](@entry_id:136401) $\alpha$ 上的滑移活动导致其自身阻力的增加。
- 非对角项 $h_{\alpha\beta} (\alpha \neq \beta)$ 描述了**潜[硬化](@entry_id:177483)（latent hardening）**，即滑移系 $\beta$ 上的滑移活动导致了滑移系 $\alpha$ 阻力的增加。这是因为不同滑移系上的[位错](@entry_id:157482)会相互交割、形成[位错](@entry_id:157482)锁（jogs）或森林，成为彼此运动的障碍。
- 由于[硬化](@entry_id:177483)是滑移量的累积效应，与滑移方向无关，因此法则中采用滑移率的[绝对值](@entry_id:147688) $|\dot{\gamma}^{\beta}|$。为保证材料不发生软化，所有 $h_{\alpha\beta}$ 均需为非负值。

例如，对于一个双[滑移系](@entry_id:136401)晶体，其硬化矩阵为 $\boldsymbol{h}=\begin{pmatrix}100  50 \\ 20  100\end{pmatrix}\,\mathrm{MPa}$。若滑移率分别为 $\dot{\gamma}^{1}=1\times 10^{-3}\,\mathrm{s}^{-1}$ 和 $\dot{\gamma}^{2}=-2\times 10^{-3}\,\mathrm{s}^{-1}$，则[滑移系](@entry_id:136401)1的[硬化](@entry_id:177483)率为：
$$ \dot{g}^{1} = h_{11}|\dot{\gamma}^{1}| + h_{12}|\dot{\gamma}^{2}| = (100\,\mathrm{MPa})(10^{-3}\,\mathrm{s}^{-1}) + (50\,\mathrm{MPa})(2\times 10^{-3}\,\mathrm{s}^{-1}) = 0.2\,\mathrm{MPa/s} $$
[@problem_id:2628517]

为了更深入地理解[硬化](@entry_id:177483)，我们可以引入基于位错密度演化的物理模型。**Kocks-Mecking模型**是一个经典例子，它描述了[统计存储位错](@entry_id:181754)密度 $\rho$ 的演化，认为其变化率是[位错](@entry_id:157482)**存储**和**动态回复**（湮灭）竞争的结果：[@problem_id:2628533]
$$ \frac{d\rho}{d\varepsilon^p} = k_1 \sqrt{\rho} - k_2 \rho $$
- 存储项 $k_1 \sqrt{\rho}$ 源于位错运动时被障碍物捕获。存储率正比于 $1/\ell$，其中[位错](@entry_id:157482)[平均自由程](@entry_id:139563) $\ell \sim 1/\sqrt{\rho}$。
- 回复项 $-k_2 \rho$ 源于运动中的[位错](@entry_id:157482)发生相遇和湮灭，其概率正比于位错密度的平方（体现在率方程中为线性项）。

滑移阻力 $g$ 则通过著名的**[泰勒关系](@entry_id:161818)（Taylor relation）**与[位错密度](@entry_id:161592)相联系：
$$ g = \alpha \mu b \sqrt{\rho} $$
其中 $\alpha$ 是一个量级为1的无量纲常数，$\mu$ 是剪切模量，$b$ 是伯格斯矢量模。这个关系式描述了克服森林[位错](@entry_id:157482)所需的应力。将这两个方程联立，就构成了一个基于物理机制的[硬化](@entry_id:177483)模型。该模型能够自然地预测硬化的饱和现象：当[位错](@entry_id:157482)的存储和回复[达到平衡](@entry_id:170346)时（$\dot{\rho}=0$），位错密度达到饱和值 $\rho_{\mathrm{sat}}=(k_1/k_2)^2$，硬化停止，流动应力达到饱和值 $g_{\mathrm{sat}} = \alpha \mu b (k_1/k_2)$。[@problem_id:2628533]

### 超越经典：非Schmid效应

[Schmid定律](@entry_id:160968)假设滑移的激活仅取决于分切应力 $\tau^{\alpha}$。然而，大量实验和[原子模拟](@entry_id:199973)表明，在许多情况下，特别是对于BCC金属，其他应力分量也会显著影响滑移的难易程度。这种现象被称为**非Schmid效应（non-Schmid effects）**。[@problem_id:2628495]

非Schmid效应的根源并不在于驱动滑移的[Peach-Koehler力](@entry_id:157620)失效，而在于**临界分切应力 $\tau_c$ 本身会受到其他应力分量的影响**。其物理机制与BCC金属中 $\frac{1}{2}\langle 111 \rangle$ 螺[位错](@entry_id:157482)独特的非平面核心结构密切相关。这个核心并非局限在一个单一的[滑移面](@entry_id:158709)上，而是扩展到几个相交的晶面上。[位错](@entry_id:157482)的运动需要核心结构发生复杂的重构，这一过程的[能量势](@entry_id:748988)垒（Peierls势垒）非常高。

那些不产生滑移驱动力（即非Schmid）的应力分量，虽然不直接推动[位错](@entry_id:157482)平移，但可以作用于[位错核心](@entry_id:201451)，使其发生畸变。这种畸变会改变核心的能量以及运动所需的Peierls势垒高度，从而影响滑移的激活。能够引起非Schmid效应的应力分量包括：
- 作用在滑移面上的**[法向应力](@entry_id:260622) $\sigma_n$**。
- 作用在滑移面上、但垂直于滑移方向的**[剪切应力](@entry_id:137139) $\tau_{\perp}$**。
- 作用在包含滑移方向的其他[晶面](@entry_id:166481)上的**[剪切应力](@entry_id:137139) $\tau'$**。

这些应力的作用导致了BCC金属复杂的塑性行为，例如滑移的“孪生/反孪生”不对称性。为了在模型中考虑这些效应，通常需要修正Schmid激活准则，将这些非Schmid应力分量引入到一个有效分切应力表达式中，例如：[@problem_id:2628495]
$$ \tau + a_1 \sigma_n + a_2 \tau_{\perp} + a_3 \tau' \ge \tau_c $$
其中 $a_i$ 是表征各种非Schmid效应强度的材料常数。理解和量化非Schmid效应对于精确预测BCC金属及其合金的强度和[延性](@entry_id:160108)至关重要。