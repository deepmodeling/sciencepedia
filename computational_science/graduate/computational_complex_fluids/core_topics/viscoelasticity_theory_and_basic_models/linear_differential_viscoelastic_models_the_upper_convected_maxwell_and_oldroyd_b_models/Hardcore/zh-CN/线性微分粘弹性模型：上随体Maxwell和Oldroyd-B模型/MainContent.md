## 引言
在[计算复杂流体](@entry_id:1122778)领域，理解和模拟[聚合物溶液](@entry_id:145399)等非牛顿流体的行为至关重要。上随转 Maxwell (UCM) 模型和 Oldroyd-B 模型是这一领域的基石，为从简单的[牛顿流体](@entry_id:263796)描述过渡到复杂的[粘弹性](@entry_id:148045)行为提供了第一个理论阶梯。这些模型的核心挑战在于如何将直观的一维弹簧-粘壶力学概念，推广到能够准确描述三维[流体变形](@entry_id:271538)与应力响应的、符合物理[客观性原理](@entry_id:185412)的张量方程。本文旨在系统性地阐述这些基础模型的理论、应用与局限。

在接下来的章节中，读者将踏上一段从基本原理到前沿应用的探索之旅。在“**原则与机理**”一章中，我们将从微观的胡克哑铃模型出发，构建 UCM 和 Oldroyd-B [本构方程](@entry_id:138559)，并深入分析它们在简单剪切和拉伸流中的预测行为及其固有的物理缺陷。随后，在“**应用与交叉学科联系**”一章中，我们将展示这些模型如何解释魏森伯格效应等宏观现象，如何与实验[流变学](@entry_id:138671)数据相结合，并探讨它们在[计算流变学](@entry_id:747633)和粘弹性相分离等交叉领域中的角色。最后，通过“**动手实践**”中的具体问题，读者将有机会亲手应用所学知识，巩固对模型力学行为的理解。

## 原则与机理

在本章中，我们将深入探讨线性[微分](@entry_id:158422)[粘弹性本构模型](@entry_id:265825)，重点关注上随转 Maxwell (UCM) 模型和 Oldroyd-B 模型。这些模型是[计算复杂流体](@entry_id:1122778)领域的基石，为理解和模拟聚合物溶液及熔体的流动行为提供了基础框架。我们将从基本物理原则出发，构建这些[本构关系](@entry_id:186508)，分析它们在典型流场中的预测，并探讨其固有的局限性以及在[数值模拟](@entry_id:146043)中带来的挑战。

### 从一维粘弹性到张量框架

理解粘弹性最直观的起点是一维力学模型。想象一个由线弹性弹簧和线性[粘性阻尼](@entry_id:168972)器（或称粘壶）串联组成的单元，这便是经典的 **Maxwell 元件**。当施加应力 $\sigma$ 时，弹簧产生与应变成正比的响应，而阻尼器产生与应变率成正比的响应。对于串联系统，总[应变率](@entry_id:154778) $\dot{\gamma}$ 是弹簧[应变率](@entry_id:154778) $\dot{\gamma}_s$ 和阻尼器应变率 $\dot{\gamma}_d$ 的和，而应力在两个元件上是相同的。

根据这些基本关系，弹簧的[应力-应变关系](@entry_id:274093)为 $\sigma = G \gamma_s$，其中 $G$ 是弹性模量，其应变率为 $\dot{\gamma}_s = \frac{1}{G}\dot{\sigma}$。阻尼器的应力-[应变率](@entry_id:154778)关系为 $\sigma = \eta_p \dot{\gamma}_d$，其中 $\eta_p$ 是[聚合物粘度](@entry_id:186823)，其应变率为 $\dot{\gamma}_d = \frac{1}{\eta_p}\sigma$。将两者相加得到总应变率：
$$ \dot{\gamma} = \dot{\gamma}_s + \dot{\gamma}_d = \frac{1}{G}\dot{\sigma} + \frac{1}{\eta_p}\sigma $$
整理后，我们得到关于[应力演化](@entry_id:1132517)的[微分](@entry_id:158422)方程，即**标量 Maxwell 模型**：
$$ \sigma + \lambda \dot{\sigma} = \eta_p \dot{\gamma} $$
这里，我们定义了一个关键的材料参数，**弛豫时间** $\lambda = \eta_p / G$，它代表了材料从弹性主导响应过渡到粘性主导响应的[特征时间尺度](@entry_id:276738)。

然而，流体流动是三维的，其应力状态由一个[二阶张量](@entry_id:199780) $\boldsymbol{\tau}$ 描述。如何将一维的 Maxwell 模型推广到三维张量形式？一个幼稚的推广可能是简单地将标量替换为张量，并将时间导数替换为[随体导数](@entry_id:204621) $D/Dt$：
$$ \boldsymbol{\tau} + \lambda \frac{D\boldsymbol{\tau}}{Dt} = 2\eta_p \boldsymbol{D} $$
其中 $\boldsymbol{D}$ 是[形变率张量](@entry_id:184787)，即[速度梯度](@entry_id:261686) $\nabla\boldsymbol{v}$ 的对称部分。然而，这个“朴素”的推广存在一个致命缺陷：它不满足**[物质坐标系无关性原理](@entry_id:188784)**（或称**[客观性原理](@entry_id:185412)**）。该原理要求[本构方程](@entry_id:138559)在任何[刚体运动](@entry_id:144691)（如平移和旋转）的叠加下形式不变。[随体导数](@entry_id:204621) $D\boldsymbol{\tau}/Dt$ 并非一个客观的时间导数；在一个旋转的坐标系中观察时，即使流体本身没有发生形变，它也会预测出非零的应力变化。

为了满足[客观性原理](@entry_id:185412)，我们必须使用**[客观时间导数](@entry_id:1129024)**。有多种客观导数，但对于源于微观结构（如聚合物哑铃模型的仿射形变）的**逆变应力张量** $\boldsymbol{\tau}$，其输运规律自然地导出了**上随[转导](@entry_id:139819)数** (Upper-Convected Derivative)，记为 $\overset{\triangledown}{\boldsymbol{\tau}}$：
$$ \overset{\triangledown}{\boldsymbol{\tau}} = \frac{D\boldsymbol{\tau}}{Dt} - (\nabla\boldsymbol{v}) \cdot \boldsymbol{\tau} - \boldsymbol{\tau} \cdot (\nabla\boldsymbol{v})^{\top} $$
通过将朴[素模型](@entry_id:155161)中的[随体导数](@entry_id:204621)替换为上随转导数，我们得到了**上随转 Maxwell (UCM) 模型**：
$$ \boldsymbol{\tau} + \lambda \overset{\triangledown}{\boldsymbol{\tau}} = 2\eta_p \boldsymbol{D} $$
这个模型是客观的，并且在小形变极限下能正确地恢复到标量 Maxwell 模型的形式。其他客观导数，如[共旋导数](@entry_id:203813)或下随[转导](@entry_id:139819)数，虽然也满足[客观性原理](@entry_id:185412)，但它们对应于不同的微观结构或张量特性，与仿射形变的逆变[应力张量](@entry_id:148973)的物理背景不符。

### [运动学分解](@entry_id:751020)：形变与旋转的角色

为了更深入地理解本构模型中的各项，我们需要考察流动的基本运动学。任意一点的局部流动都可以通过[速度梯度张量](@entry_id:270928) $\boldsymbol{L} = \nabla\boldsymbol{v}$ 来描述。这个张量可以唯一地分解为一个对称[部分和](@entry_id:162077)一个反对称部分：
$$ \boldsymbol{L} = \boldsymbol{D} + \boldsymbol{W} $$
其中，**[形变率张量](@entry_id:184787)** $\boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^{\top})$ 描述了流体微元的拉伸、压缩和[剪切变形](@entry_id:170920)，是产生应力的根源。而**[涡量张量](@entry_id:189621)**（或称[自旋张量](@entry_id:187346)）$\boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^{\top})$ 描述了流体微元的刚性旋转。

考虑两种简单的流场可以清晰地揭示 $\boldsymbol{D}$ 和 $\boldsymbol{W}$ 的物理意义。在纯[刚体](@entry_id:1131033)旋转流场 $\boldsymbol{v} = \boldsymbol{\Omega} \times \boldsymbol{r}$ 中，我们发现 $\boldsymbol{D} = \boldsymbol{0}$ 而 $\boldsymbol{L} = \boldsymbol{W}$，这证实了 $\boldsymbol{W}$ 编码了旋转。相反，在纯[拉伸流](@entry_id:198535)场中，$\boldsymbol{W} = \boldsymbol{0}$ 而 $\boldsymbol{L} = \boldsymbol{D}$。对于平面 Couette [剪切流](@entry_id:266817) $\boldsymbol{v} = (\dot{\gamma}y, 0, 0)$，我们得到非零的 $\boldsymbol{D}$ 和 $\boldsymbol{W}$，表明[简单剪切流](@entry_id:1131665)是[拉伸与旋转](@entry_id:150197)的结合。

在 UCM 这样的[粘弹性模型](@entry_id:175352)中，$\boldsymbol{D}$ 和 $\boldsymbol{W}$ 的角色被明确区分开来。[形变率张量](@entry_id:184787) $\boldsymbol{D}$ 出现在本构方程的右端，作为产生聚合物应力的**源项** ($2\eta_p \boldsymbol{D}$)。这符合物理直觉：只有当材料发生形变时，才会产生弹性应力。而[涡量张量](@entry_id:189621) $\boldsymbol{W}$（作为 $\boldsymbol{L}$ 的一部分）则出现在上随[转导](@entry_id:139819)数的项中，它的作用是确保应力张量 $\boldsymbol{\tau}$ 随着流体微元一起被正确地旋转和平流，从而保证了模型的客观性。因此，在纯[刚体](@entry_id:1131033)旋转中，由于 $\boldsymbol{D}=\boldsymbol{0}$，UCM 模型不会从静止状态产生任何弹性应力。

### Oldroyd-B 模型：引入溶剂贡献

许多聚合物体系，尤其是稀溶液，可以被看作是粘弹性聚合物溶解在[牛顿流体](@entry_id:263796)（溶剂）中。**Oldroyd-B 模型**正是对这种体系的理想化描述。它假设总的[偏应力张量](@entry_id:267642) $\boldsymbol{\sigma}'$ 是牛顿溶剂贡献 $\boldsymbol{\tau}_s$ 和聚合物贡献 $\boldsymbol{\tau}_p$ 的简单叠加（并联）：
$$ \boldsymbol{\sigma}' = \boldsymbol{\tau}_s + \boldsymbol{\tau}_p $$
其中，溶剂的贡献遵循[牛顿流体](@entry_id:263796)本构，即 $\boldsymbol{\tau}_s = 2\eta_s\boldsymbol{D}$，$\eta_s$ 是[溶剂粘度](@entry_id:264247)。聚合物的贡献则由 UCM 模型描述，$\boldsymbol{\tau}_p + \lambda \overset{\triangledown}{\boldsymbol{\tau}}_p = 2\eta_p \boldsymbol{D}$。因此，Oldroyd-B 模型可以写作一个方程组：
$$ \boldsymbol{\sigma} = -p\boldsymbol{I} + \boldsymbol{\tau}_s + \boldsymbol{\tau}_p $$
$$ \boldsymbol{\tau}_s = 2\eta_s\boldsymbol{D} $$
$$ \boldsymbol{\tau}_p + \lambda \overset{\triangledown}{\boldsymbol{\tau}}_p = 2\eta_p \boldsymbol{D} $$
其中 $p$ 是压力，$\boldsymbol{I}$ 是单位张量。这个模型继承了 UCM 模型的客观性，并增加了一个纯粘性的耗散通道。 

### 微观结构基础：胡克哑铃模型

UCM 和 Oldroyd-B 模型不仅仅是唯象的数学构造，它们也可以从简化的微观物理模型——**胡克哑铃模型**——中推导出来。该模型将一个聚合物链简化为两个由无质量的线弹性（胡克）弹簧连接的珠子。珠子在溶剂中运动，受到流体拖曳力、弹簧的恢复力以及由热搅动引起的布朗力的作用。

通过对珠子进行[力平衡](@entry_id:267186)分析，并结合统计力学，可以推导出描述哑铃端到端矢量 $\mathbf{R}$ 的概率分布函数演化的 Fokker-Planck 方程。宏观的聚合物[应力张量](@entry_id:148973) $\boldsymbol{\tau}_p$ 可以通过 Kramers-Giesekus 表达式从哑铃构象的系综平均中得到。这一系列的推导最终表明，胡克哑铃模型在宏观上恰好对应于 UCM 模型。

这个微观模型为宏观参数提供了清晰的物理解释：
- **弛豫时间** $\lambda = \frac{\zeta}{4H}$，其中 $\zeta$ 是珠子的拖曳系数，$H$ 是弹簧的劲度系数。$\lambda$ 反映了弹簧恢复力与[流体阻力](@entry_id:262242)之间的竞争。
- **[聚合物粘度](@entry_id:186823)** $\eta_p = n k_B T \lambda$，其中 $n$ 是哑铃的[数密度](@entry_id:895657)，$k_B$ 是[玻尔兹曼常数](@entry_id:142384)，$T$ 是[绝对温度](@entry_id:144687)。这表明粘度源于聚合物链的[熵弹性](@entry_id:151071)贡献，并与[弛豫时间](@entry_id:191572)成正比。

在[数值模拟](@entry_id:146043)和理论分析中，我们常引入一个无量纲的**构象张量** $\boldsymbol{A}$，它定义为哑铃端到端矢量二阶矩的系综平均，$\boldsymbol{A} = \langle \boldsymbol{q}\boldsymbol{q} \rangle$，其中 $\boldsymbol{q}$ 是被平衡[均方根](@entry_id:263605)长度归一化的端到端矢量。在静止[平衡态](@entry_id:270364)，$\boldsymbol{A}_{eq} = \boldsymbol{I}$。聚合物[应力张量](@entry_id:148973)与构象张量之间存在一个非常重要的关系：
$$ \boldsymbol{\tau}_p = G(\boldsymbol{A} - \boldsymbol{I}) $$
其中 $G$ 是[弹性模量](@entry_id:198862)。这个关系表明，偏离平衡构象 $(\boldsymbol{A} - \boldsymbol{I})$ 直接导致了弹性应力。通过微观推导，可以证明模量 $G$ 既可以从微观参数得到 $G = n k_B T$，也可以从宏观参数得到 $G = \eta_p / \lambda$。这两个表达式是等价的，构成了微观与宏观世界的桥梁。 使用构象张量 $\boldsymbol{A}$，Oldroyd-B 模型的[演化方程](@entry_id:268137)可以写成关于 $\boldsymbol{A}$ 的[输运方程](@entry_id:174281)，这在计算流体力学中是一种非常常见的形式。

### 模型在典型流场中的预测

一个本构模型的价值在于其对流体在不同流动条件下行为的预测能力。

#### [线性粘弹性](@entry_id:181219)（小振幅振荡剪切）

在[小振幅振荡剪切 (SAOS)](@entry_id:196963) 实验中，流体经受一个正弦变化的应变 $\gamma(t) = \gamma_0 \sin(\omega t)$。在这种小形变极限下，UCM 模型中的[非线性](@entry_id:637147)项可以忽略，模型线性化。对于 Oldroyd-B 流体，我们可以推导出其**[复数粘度](@entry_id:192623)** $\eta^*(\omega)$：
$$ \eta^*(\omega) = \eta_s + \frac{\eta_p}{1 + i\omega\lambda} $$
[复数粘度](@entry_id:192623)可以进一步分解为储能模量 $G'(\omega)$ 和耗能模量 $G''(\omega)$：
$$ G'(\omega) = \omega \eta''(\omega) = \frac{\eta_p \lambda \omega^2}{1 + \lambda^2\omega^2} $$
$$ G''(\omega) = \omega \eta'(\omega) = \omega\eta_s + \frac{\eta_p\omega}{1 + \lambda^2\omega^2} $$
其中 $\eta'(\omega)$ 和 $\eta''(\omega)$ 分别是 $\eta^*(\omega)$ 的实部和虚部的[相反数](@entry_id:151709)。$G'$ 代表流体储存的[弹性势能](@entry_id:168893)，而 $G''$ 代表流体耗散的能量。这些表达式可以直接与流变仪的测量结果进行比较，从而确定模型的参数 $\eta_s, \eta_p, \lambda$。

#### [稳态](@entry_id:139253)[简单剪切流](@entry_id:1131665)

在[稳态](@entry_id:139253)[简单剪切流](@entry_id:1131665) $\boldsymbol{v} = (\dot{\gamma}y, 0, 0)$ 中，Oldroyd-B 模型预测了几个标志性的行为。通过求解[稳态](@entry_id:139253)的[本构方程](@entry_id:138559)，我们得到：
- **剪切粘度** $\eta(\dot{\gamma}) = \frac{\sigma_{xy}}{\dot{\gamma}} = \eta_s + \eta_p$。粘度是一个常数，不随剪切率 $\dot{\gamma}$ 变化。这被称为**牛顿平台**，模型无法预测真实聚合物溶液中常见的**[剪切稀化](@entry_id:150203)**现象。
- **第一[法向应力差](@entry_id:199507)** $N_1(\dot{\gamma}) = \sigma_{xx} - \sigma_{yy} = 2\eta_p\lambda\dot{\gamma}^2$。模型成功预测了非零的法向应力，这是粘弹性流体的一个关键特征（如 Weissenberg 效应）。$N_1$ 是正值且与剪切率的平方成正比。
- **第二法向应力差** $N_2(\dot{\gamma}) = \sigma_{yy} - \sigma_{zz} = 0$。模型预测 $N_2$ 恒为零。然而，实验表明大多数聚合物溶液的 $N_2$ 是一个小的负值。这是该模型的另一个显著缺陷。

#### [稳态](@entry_id:139253)[单轴拉伸](@entry_id:188287)流

在[稳态](@entry_id:139253)[单轴拉伸](@entry_id:188287)流 $\nabla\boldsymbol{v} = \mathrm{diag}(\dot{\varepsilon}, -\dot{\varepsilon}/2, -\dot{\varepsilon}/2)$ 中，Oldroyd-B 模型揭示了一个更为戏剧性的特性。求解[稳态](@entry_id:139253)本构方程可得**[拉伸粘度](@entry_id:1124791)** $\eta_E$：
$$ \eta_E(\dot{\varepsilon}) = \frac{\sigma_{xx} - \sigma_{yy}}{\dot{\varepsilon}} = 3\eta_s + \frac{3\eta_p}{(1-2\lambda\dot{\varepsilon})(1+\lambda\dot{\varepsilon})} $$
这个表达式显示，当拉伸率 $\dot{\varepsilon}$ 接近一个临界值 $\dot{\varepsilon}_c = 1/(2\lambda)$ 时，分母趋于零，导致[拉伸粘度](@entry_id:1124791) $\eta_E$ 发散至无穷大。这被称为**拉伸灾变** (extensional catastrophe)。从微观角度看，这对应于胡克哑铃在线性弹簧力作用下被无限拉长的**卷曲-拉伸转变**。这个无物理的[奇点](@entry_id:266699)是 Oldroyd-B 模型最严重的缺陷之一，并对[数值模拟](@entry_id:146043)构成了巨大挑战。

### 关键[无量纲数](@entry_id:260863)：Weissenberg 数与 Deborah 数

在分析[粘弹性流动](@entry_id:1133840)时，两个关键的[无量纲数](@entry_id:260863)——**Weissenberg 数** ($Wi$) 和 **Deborah 数** ($De$)——至关重要。虽然它们有时被混用，但其物理意义有明确的区别。

通过对本构方程进行无量纲化，我们发现：
- **Weissenberg 数** $Wi = \lambda \mathcal{G}$，其中 $\mathcal{G}$ 是特征剪切率（如 $U/L$ 或 $\dot{\gamma}$）。$Wi$ 比较了材料的弛豫时间与[流体变形](@entry_id:271538)过程的时间尺度。它衡量了流动中[非线性弹性](@entry_id:185743)的重要性。当 $Wi \ll 1$ 时，流动接近[牛顿流体](@entry_id:263796)；当 $Wi \gtrsim 1$ 时，弹性效应显著。例如，第一法向应力差 $N_1$ 就正比于 $Wi^2$。
- **Deborah 数** $De = \lambda / T_{proc}$，其中 $T_{proc}$ 是流动过程的[特征时间尺度](@entry_id:276738)（如[振荡周期](@entry_id:271387)或外部条件变化的时间）。$De$ 比较了材料的弛豫时间与流动非[稳态](@entry_id:139253)性的时间尺度。它衡量了流动的“类固”或“类液”程度。

在稳态流动中，唯一的流动时间尺度是剪切率的倒数，因此 $T_{proc} \sim 1/\mathcal{G}$，这导致 $De=Wi$。然而，在[非稳态流](@entry_id:269993)动中，两者通常不同。例如，在小振幅振荡剪切中， $De = \lambda\omega$ 控制着线性的、与频率相关的响应（如相角），而 $Wi = \lambda(\gamma_0\omega)$ 控制着与振[幅相](@entry_id:269870)关的[非线性](@entry_id:637147)效应（如法向应力）。只有当 $Wi$ 不可忽略时，[非线性](@entry_id:637147)效应才变得重要。

### 模型的局限性与计算挑战

尽管 Oldroyd-B 模型是理解[粘弹性](@entry_id:148045)的有力工具，但其预测能力有限。正如前面分析所示，它无法描述几个关键的实验现象：
1.  **剪切稀化**：真实[聚合物溶液](@entry_id:145399)的粘度通常随剪切率增加而降低。Oldroyd-B 模型预测粘度恒定。
2.  **非零的第二[法向应力差](@entry_id:199507)**：实验中通常测得 $N_2 < 0$ 且 $|N_2| \ll N_1$。Oldroyd-B 模型预测 $N_2=0$。
3.  **有限的[拉伸粘度](@entry_id:1124791)**：由于聚合物链长度有限，其[拉伸粘度](@entry_id:1124791)虽然会显著增长，但最终会趋于一个平台值。Oldroyd-B 模型预测[拉伸粘度](@entry_id:1124791)在有限的拉伸率下发散。

这些缺陷的根源在于胡克哑铃模型的过度简化：线性的弹簧力（导致无限可拉伸性）和各向同性的流体拖曳假设。

这些物理上的缺陷直接导致了计算上的巨大困难，即所谓的**高 Weissenberg 数难题 (HWNP)**。当模拟包含停[滞点](@entry_id:266621)（局部为强[拉伸流](@entry_id:198535)）的[复杂流动](@entry_id:747569)时，如果局部 $Wi$ 超过临界值（对于[单轴拉伸](@entry_id:188287)是 $1/2$，对于平面拉伸也是 $1/2$），Oldroyd-B 模型预测应力会局部发散。这会在停[滞点](@entry_id:266621)附近形成极度陡峭的应力边界层，任何数值网格都难以解析，从而导致计算发散。

在数值层面，不恰当的离散格式还可能导致构象张量 $\boldsymbol{A}$ 失去其物理上必须满足的[对称正定](@entry_id:145886)性 (Symmetric Positive Definite, SPD)，这也是导致计算失败的常见原因。值得注意的是，失去[正定性](@entry_id:149643)是数值问题，而非连续介质模型本身的物理问题。

为了克服 HWNP，研究者们发展了多种策略。在数值方面，**[对数构象方法](@entry_id:1127422)** (log-conformation representation) 通过求解 $\log\boldsymbol{A}$ 的演化方程，在数学上保证了 $\boldsymbol{A}$ 的正定性，从而显著增强了算法的稳定性。 在物理模型方面，引入更真实的物理机制，如**有限可拉伸性**，是更根本的解决方案。例如，FENE-P (Finitely Extensible Nonlinear Elastic–Peterlin) 模型用一个[非线性](@entry_id:637147)的弹簧力代替了胡克弹簧，使得哑铃的伸长有上限。这消除了[拉伸粘度](@entry_id:1124791)的[奇点](@entry_id:266699)，使应力饱和于一个有限值，从而缓解了应力梯度的陡峭程度，使得在高 Weissenberg 数下的[数值模拟](@entry_id:146043)成为可能。

总之，UCM 和 Oldroyd-B 模型是学习粘弹性流体力学的理想起点。它们简洁、具有微观物理解释，并能捕捉到一些关键的弹性现象。然而，它们的缺陷同样具有启发性，指引着我们向更复杂、更真实的[非线性](@entry_id:637147)本构模型迈进。