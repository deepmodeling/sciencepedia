## 引言
晶体[材料的力学性能](@entry_id:158743)，尤其是其抵抗永久变形的能力，是决定其工程应用的关键。然而，一个长期困扰[材料科学](@entry_id:152226)家的谜题是：为何真实金属的屈服强度会比基于完美[晶格](@entry_id:196752)计算出的[理论强度](@entry_id:189300)低上几个[数量级](@entry_id:264888)？这一巨大差异暗示了材料的塑性变形并非通过原子面的整体刚性滑移发生，而是由一种更为精巧的微观机制主导。答案就隐藏在晶体中普遍存在的线缺陷——[位错](@entry_id:157482)之中。[位错](@entry_id:157482)作为[晶格](@entry_id:196752)中的一维不完整性，其运动主导了材料的[塑性流动](@entry_id:201346)、[断裂韧性](@entry_id:157609)乃至微观结构的演化，是连接原子尺度缺陷与宏观力学行为的核心桥梁。

本文旨在系统性地剖析[刃位错](@entry_id:191098)与螺[位错](@entry_id:157482)这两种基本[位错](@entry_id:157482)类型的物理本质。通过学习本文，您将深入理解[材料科学](@entry_id:152226)中的核心概念，并掌握分析其行为的理论工具。在**“原理与机制”**一章中，我们将从[位错](@entry_id:157482)的几何定义（伯格斯矢量）出发，推导其周围的弹性应[力场](@entry_id:147325)和能量，并阐明驱动其运动的皮克-科勒力，区分滑移与攀移这两种基本运动模式。随后，在**“应用与交叉学科联系”**一章中，我们将展示这些基本原理如何解释宏观的塑性现象，如[Orowan方程](@entry_id:272833)描述的应变率、[Frank-Read源](@entry_id:193057)导致的[位错增殖](@entry_id:201761)、以及加工硬化和[固溶强化](@entry_id:137856)等[强化机制](@entry_id:158922)，并将其概念延伸至晶界、[相变](@entry_id:147324)乃至[软物质物理](@entry_id:145473)等更广阔的领域。最后，**“动手实践”**部分将提供具体的计算问题，帮助您巩固和应用所学知识。

## 原理与机制

在引言章节中，我们确立了晶体中的[位错](@entry_id:157482)是理解[材料力学](@entry_id:201885)行为的关键。本章将深入探讨[位错](@entry_id:157482)的基本原理和主导其行为的机制。我们将从[位错](@entry_id:157482)的几何定义出发，发展到其弹性场理论，并最终解释[位错](@entry_id:157482)如何在外加应力下运动，从而导致塑性变形。

### 塑性变形的根源：[位错](@entry_id:157482)的存在

[完美晶体](@entry_id:138314)的理论[剪切强度](@entry_id:754762)，即同时剪切整个原子面所需的应力，相当之高。例如，弗伦克尔（Frenkel）提出的一个简化模型估计，理论[剪切强度](@entry_id:754762) $ \tau_{th} $ 大约是[剪切模量](@entry_id:167228) $ G $ 的一个分数，其表达式为 $ \tau_{th} = \frac{G b}{2 \pi a} $，其中 $ b $ 是滑移方向上的原子间距，$ a $ 是[滑移面](@entry_id:158709)间距。对于大多数金属，假设 $ a \approx b $，[理论强度](@entry_id:189300)大约为 $ \tau_{th} \approx G / (2\pi) $。然而，实验测得的实际[屈服强度](@entry_id:162154) $ \tau_y $ 却比这个理论值低了几个[数量级](@entry_id:264888)。

考虑一个典型的金属，其剪切模量 $ G = 75.0 \, \text{GPa} $，而实验测得的[屈服强度](@entry_id:162154)仅为 $ \tau_y = 15.0 \, \text{MPa} $。[理论强度](@entry_id:189300)与实验强度的比值可以估算为：
$$ \frac{\tau_{th}}{\tau_y} \approx \frac{G / (2\pi)}{\tau_y} = \frac{75.0 \times 10^9 \, \text{Pa}}{2\pi \times 15.0 \times 10^6 \, \text{Pa}} \approx 796 $$
[@problem_id:1311809]

这个接近800倍的巨大差异有力地证明，真实晶体中的塑性变形并非通过原子面的整体刚性滑移来实现。相反，它通过一种称为**[位错](@entry_id:157482)**（dislocation）的线缺陷的运动来发生。[位错](@entry_id:157482)的移动只需在局部区域断裂和重组原子键，因此所需的应力远低于[理论强度](@entry_id:189300)。理解[位错](@entry_id:157482)的性质是理解[材料塑性](@entry_id:186852)行为的核心。

### [位错](@entry_id:157482)的几何描述：[伯格斯矢量](@entry_id:160637)

[位错](@entry_id:157482)在数学上被描述为一个[晶格](@entry_id:196752)的[拓扑缺陷](@entry_id:138787)。为了精确地量化[位错](@entry_id:157482)所引入的[晶格](@entry_id:196752)畸变，我们使用**伯格斯矢量**（Burgers vector）$ \mathbf{b} $。这个矢量可以通过一个称为**[伯格斯回路](@entry_id:192374)**（Burgers circuit）的几何构建过程来确定。

想象在一个完美的、无缺陷的参考[晶格](@entry_id:196752)中，我们从一个原子位置开始，沿着[晶格矢量](@entry_id:161583)行走，最终形成一个闭合的回路。例如，我们可以走“右5步，上5步，左5步，下5步”，最终会回到起点。现在，在包含一条[位错](@entry_id:157482)线的真实晶体中，我们尝试复制完全相同的行走序列。由于[位错](@entry_id:157482)的存在，[晶格](@entry_id:196752)不再是完美的，这个回路将不再闭合。从终点指向起点的矢量，即所谓的**闭合失效矢量**（closure failure vector），被定义为该[位错](@entry_id:157482)的伯格斯矢量 $ \mathbf{b} $ [@problem_id:2816726]。

[伯格斯矢量](@entry_id:160637) $ \mathbf{b} $ 是[位错](@entry_id:157482)的一个内在属性，具有以下几个关键特征：

1.  **[拓扑不变性](@entry_id:181048)**：只要[伯格斯回路](@entry_id:192374)包围的是同一条[位错](@entry_id:157482)线，无论回路的形状或大小如何改变，所得到的伯格斯矢量 $ \mathbf{b} $ 始终是相同的。它是一个表征[位错](@entry_id:157482)[拓扑性质](@entry_id:141605)的量，不会因为回路路径的连续变形而改变。因此，认为[伯格斯矢量](@entry_id:160637)的大小与回路半径成正比是错误的 [@problem_id:2816726]。

2.  **守恒性**：在一个孤立的晶体中，[位错](@entry_id:157482)线不能凭空消失或终止于晶体内部；它必须形成一个闭合的环，或终止于晶体的自由表面、晶界或其他缺陷处。沿着一条[位错](@entry_id:157482)线，其伯格斯矢量是守恒的。

3.  **符号约定**：[伯格斯矢量](@entry_id:160637)的方向取决于两个约定：[位错](@entry_id:157482)线的**指向**（line sense）$ \boldsymbol{\xi} $ 和[伯格斯回路](@entry_id:192374)的环绕方向。一个常用的约定是“右手法则/终点到起点”（FS/RH）。首先，确定[位错](@entry_id:157482)线的指向 $ \boldsymbol{\xi} $。然后，用右手拇指指向 $ \boldsymbol{\xi} $ 的方向，四指弯曲的方向即为[伯格斯回路](@entry_id:192374)的环绕方向（例如，逆时针）。按照这个方向构建回路后，从终点（Finish）到起点（Start）的矢量即为 $ \mathbf{b} $。如果反转回路的环绕方向（例如，改为顺时针），得到的伯格斯矢量将反号 [@problem_id:2816726]。

在连续介质理论中，[伯格斯矢量](@entry_id:160637)也可以通过对[位错](@entry_id:157482)线周围的弹性畸变张量 $ \boldsymbol{\beta}^{\mathrm{e}} $ 进行线积分来定义：$ \mathbf{b} = -\oint_{C} \boldsymbol{\beta}^{\mathrm{e}} \cdot d\mathbf{l} $。这个积分的结果同样具有[拓扑不变性](@entry_id:181048) [@problem_id:2816726]。

### [位错](@entry_id:157482)的基本类型

根据伯格斯矢量 $ \mathbf{b} $ 和[位错](@entry_id:157482)线指向 $ \boldsymbol{\xi} $ 之间的相对取向，[位错](@entry_id:157482)可以被分为三种[基本类](@entry_id:158335)型。

#### 螺[位错](@entry_id:157482)（Screw Dislocation）

当[伯格斯矢量](@entry_id:160637) $ \mathbf{b} $ 与[位错](@entry_id:157482)线指向 $ \boldsymbol{\xi} $ **平行**（$ \mathbf{b} \parallel \boldsymbol{\xi} $）时，该[位错](@entry_id:157482)被称为**螺[位错](@entry_id:157482)**。螺[位错](@entry_id:157482)的几何形态可以想象为将一个[完美晶体](@entry_id:138314)沿某平面切开，然后将切口一侧相对于另一侧沿着平行于切口前沿（即[位错](@entry_id:157482)线）的方向滑动一个[伯格斯矢量](@entry_id:160637)的距离，最后再将原子重新键合。这使得晶体中的原子面围绕[位错](@entry_id:157482)线形成一个螺旋形的坡道，类似于螺旋楼梯。对于沿 $ z $ 轴的螺[位错](@entry_id:157482)，其[伯格斯矢量](@entry_id:160637)必然平行于 $ z $ 轴 [@problem_id:2816726]。

#### [刃位错](@entry_id:191098)（Edge Dislocation）

当[伯格斯矢量](@entry_id:160637) $ \mathbf{b} $ 与[位错](@entry_id:157482)线指向 $ \boldsymbol{\xi} $ **垂直**（$ \mathbf{b} \perp \boldsymbol{\xi} $）时，该[位错](@entry_id:157482)被称为**刃位错**。刃位错最直观的图像是在[晶格](@entry_id:196752)中插入或移出一个**额外半原子面**（extra half-plane），而[位错](@entry_id:157482)线就是这个半原子面的终止边界。这个额外半原子面在[位错](@entry_id:157482)线的一侧造成挤压，而在另一侧造成拉伸。

[刃位错](@entry_id:191098)的符号（正或负）与其几何结构相关。在一个[右手坐标系](@entry_id:166669)中，我们可以通过 $ \boldsymbol{\xi} $ 和 $ \mathbf{b} $ 的叉乘来确定额外半原子面的位置。滑移面是包含 $ \boldsymbol{\xi} $ 和 $ \mathbf{b} $ 的平面。向量 $ \boldsymbol{\xi} \times \mathbf{b} $ 的方向指向包含额外半原子面的那个半空间 [@problem_id:2880192]。例如，考虑一个[位错](@entry_id:157482)线沿 $ z $ 轴（$ \boldsymbol{\xi} = \hat{z} $），滑移面为 $ xz $ 平面的刃位错。
*   如果其伯格斯矢量为 $ \mathbf{b} = b\hat{x} $ (其中 $ b>0 $)，则 $ \boldsymbol{\xi} \times \mathbf{b} = \hat{z} \times (b\hat{x}) = b\hat{y} $。这表明额外半原子面位于滑移面上方的 $ y>0 $ 区域。
*   如果伯格斯矢量为 $ \mathbf{b} = -b\hat{x} $，则 $ \boldsymbol{\xi} \times \mathbf{b} = \hat{z} \times (-b\hat{x}) = -b\hat{y} $。这表明额外半原子面位于滑移面下方的 $ y0 $ 区域。

#### [混合位错](@entry_id:191088)（Mixed Dislocation）

在最一般的情况下，伯格斯矢量 $ \mathbf{b} $ 与[位错](@entry_id:157482)线指向 $ \boldsymbol{\xi} $ 既不平行也不垂直。这种[位错](@entry_id:157482)被称为**[混合位错](@entry_id:191088)**。任何一段[混合位错](@entry_id:191088)都可以被分解为一个螺分量 $ \mathbf{b}_s $ 和一个刃分量 $ \mathbf{b}_e $，它们分别平行和垂直于[位错](@entry_id:157482)线指向 $ \boldsymbol{\xi} $：
$$ \mathbf{b} = \mathbf{b}_s + \mathbf{b}_e $$
其中，
$$ \mathbf{b}_s = (\mathbf{b} \cdot \boldsymbol{\xi}) \boldsymbol{\xi} $$
$$ \mathbf{b}_e = \mathbf{b} - \mathbf{b}_s = \boldsymbol{\xi} \times (\mathbf{b} \times \boldsymbol{\xi}) $$
[位错](@entry_id:157482)的**特征角**（character angle）$ \theta $ 定义为 $ \mathbf{b} $ 和 $ \boldsymbol{\xi} $ 之间的夹角，可以通过它们的[点积](@entry_id:149019)计算：
$$ \cos(\theta) = \frac{\mathbf{b} \cdot \boldsymbol{\xi}}{|\mathbf{b}| |\boldsymbol{\xi}|} $$
纯螺[位错](@entry_id:157482)的 $ \theta = 0^\circ $ 或 $ 180^\circ $，而纯[刃位错](@entry_id:191098)的 $ \theta = 90^\circ $。

例如，考虑一个面心立方（FCC）晶体中的[位错](@entry_id:157482)，其伯格斯矢量为 $ \mathbf{b} = \frac{a}{2}(1, -1, 0) $，线指向为 $ \boldsymbol{\xi} = \frac{1}{\sqrt{14}}(1, 2, -3) $。我们可以计算其特征角来确定其混合程度。首先计算[点积](@entry_id:149019)和模：
$$ \mathbf{b} \cdot \boldsymbol{\xi} = \frac{a}{2\sqrt{14}} (1 \cdot 1 + (-1) \cdot 2 + 0 \cdot (-3)) = -\frac{a}{2\sqrt{14}} $$
$$ |\mathbf{b}| = \frac{a}{2} \sqrt{1^2 + (-1)^2 + 0^2} = \frac{a\sqrt{2}}{2} $$
$$ |\boldsymbol{\xi}| = 1 $$
因此，特征角的余弦为：
$$ \cos(\theta) = \frac{-a / (2\sqrt{14})}{ (a\sqrt{2}/2) \cdot 1 } = -\frac{1}{\sqrt{28}} \approx -0.189 $$
计算出的角度为 $ \theta = \arccos(-0.189) \approx 100.9^\circ $ [@problem_id:2880215]。这个角度不接近 $ 0^\circ $ 或 $ 90^\circ $，表明这是一个具有显著刃分量和螺分量的[混合位错](@entry_id:191088)。

### [位错的弹性场](@entry_id:203330)与能量

[位错](@entry_id:157482)作为[晶格缺陷](@entry_id:270099)，会在其周围产生一个长程的**弹性应[力场](@entry_id:147325)**和**应变场**。这些场是理解[位错](@entry_id:157482)之间以及[位错](@entry_id:157482)与其他缺陷相互作用的基础。

#### [位错核心](@entry_id:201451)

在线性弹性理论的框架下，[位错](@entry_id:157482)线本身是一个[奇点](@entry_id:137764)，理论预测在 $ r \to 0 $ 处应力和应变会趋于无穷大。这显然是不符合物理实际的，因为在原子尺度上，[晶格](@entry_id:196752)的离散性和[原子间作用力](@entry_id:158182)的[非线性](@entry_id:637147)会起主导作用。因此，我们引入了**[位错核心](@entry_id:201451)**（dislocation core）的概念，它指的是[位错](@entry_id:157482)线周围一个半径为 $ r_c $ 的小区域。在这个区域内，应变非常大（例如，[位移梯度](@entry_id:165352) $ b/r $ 的量级为1），[线性弹性](@entry_id:166983)理论失效 [@problem_id:2816718]。

核心半径 $ r_c $ 并不是一个精确定义的物理量，而是一个用于正则化理论的[截断半径](@entry_id:136708)，其[数量级](@entry_id:264888)通常为几个伯格斯矢量的大小（$ r_c \sim b $）。选择不同的 $ r_c $ 会改变弹性储能和核心[储能](@entry_id:264866)的划分，但不会影响远离核心的长程弹性场 [@problem_id:2816718]。

#### 弹性应[力场](@entry_id:147325)

在线性弹性理论的[适用范围](@entry_id:636189)（$ r  r_c $）内，可以精确求解[位错](@entry_id:157482)的应[力场](@entry_id:147325)。这些应[力场](@entry_id:147325)的一个共同特征是它们都随着与[位错](@entry_id:157482)线距离 $ r $ 的增大而以 $ 1/r $ 的规律衰减。

对于沿 $ z $ 轴的**螺[位错](@entry_id:157482)**（$ \mathbf{b} = b\hat{z} $），其应[力场](@entry_id:147325)是纯剪切的。在以[位错](@entry_id:157482)线为原点的[笛卡尔坐标系](@entry_id:169789)中，非零的应力分量为 [@problem_id:2816762]：
$$ \sigma_{xz} = -\frac{\mu b}{2\pi} \frac{y}{x^2 + y^2} $$
$$ \sigma_{yz} = \frac{\mu b}{2\pi} \frac{x}{x^2 + y^2} $$
其中 $ \mu $ 是剪切模量。

对于沿 $ z $ 轴的**[刃位错](@entry_id:191098)**（$ \mathbf{b} = b\hat{x} $），其应[力场](@entry_id:147325)更为复杂，同时包含[剪切应力](@entry_id:137139)和[正应力](@entry_id:260622) [@problem_id:2816727]：
$$ \sigma_{xx} = -\frac{\mu b}{2\pi(1-\nu)} \frac{y(3x^2 + y^2)}{(x^2 + y^2)^2} $$
$$ \sigma_{yy} = \frac{\mu b}{2\pi(1-\nu)} \frac{y(x^2 - y^2)}{(x^2 + y^2)^2} $$
$$ \sigma_{xy} = \frac{\mu b}{2\pi(1-\nu)} \frac{x(x^2 - y^2)}{(x^2 + y^2)^2} $$
其中 $ \nu $ 是[泊松比](@entry_id:158876)。$ \sigma_{xx} $ 和 $ \sigma_{yy} $ 分量的存在表明，在刃位错周围存在着**压缩区**（额外半原子面所在的一侧）和**拉伸区**（额外半原子面缺失的一侧）。这些正应力场对于[刃位错](@entry_id:191098)与溶质原子、析出相等缺陷的相互作用至关重要。

#### 弹性能

[位错](@entry_id:157482)的应[力场](@entry_id:147325)在晶体中储存了弹性能。单位长度[位错](@entry_id:157482)线的弹性能 $ E/L $ 可以通过对[应变能密度](@entry_id:200085) $ w = \frac{1}{2} \sigma_{ij}\varepsilon_{ij} $ 在[位错核心](@entry_id:201451)外部的区域进行积分得到。对于一条螺[位错](@entry_id:157482)，其单位长度的弹性能为 [@problem_id:2816692]：
$$ \frac{E}{L} = \frac{\mu b^2}{4\pi} \ln\left(\frac{R}{r_c}\right) $$
其中 $ R $ 是一个外部[截断半径](@entry_id:136708)，代表晶体尺寸或与其他[位错](@entry_id:157482)的平均距离。刃位错的能量表达式形式类似，只是系数中包含了[泊松比](@entry_id:158876) $ \nu $，变为 $ \frac{\mu b^2}{4\pi(1-\nu)} \ln\left(\frac{R}{r_c}\right) $。

这个对数形式的能量表达式揭示了两个重要事实：
1.  [位错](@entry_id:157482)的能量与 $ b^2 $ 成正比。这构成了**弗兰克能量准则**（Frank's energy criterion）的基础，即[位错](@entry_id:157482)反应（如分解或合并）在能量上有利的条件是产物的 $ \sum b^2 $ 小于反应物的 $ \sum b^2 $。
2.  能量对 $ \ln(r_c) $ 的依赖性证实了核心区域的重要性。如果没有核心截断（即 $ r_c \to 0 $），能量将发散至无穷大，这再次说明了线性弹性理论在[位错](@entry_id:157482)线处的失效 [@problem_id:2816718]。

### [位错](@entry_id:157482)的运动

[位错](@entry_id:157482)的运动是塑性变形的微观机制。施加在晶体上的外部应力会对[位错](@entry_id:157482)线产生一个力，驱动其运动。

#### 皮克-科勒力

作用在单位长度[位错](@entry_id:157482)线上的力 $ \mathbf{f} $ 由**皮克-科勒（Peach-Koehler）公式**给出：
$$ \mathbf{f} = (\boldsymbol{\sigma} \cdot \mathbf{b}) \times \boldsymbol{\xi} $$
其中 $ \boldsymbol{\sigma} $ 是作用在[位错](@entry_id:157482)位置处的应力张量（可以是外加应力，也可以是其他缺陷产生的[内应力](@entry_id:193721)）。这个力是一个**[构型力](@entry_id:188113)**（configurational force），它描述了当[位错](@entry_id:157482)移动时系统总能量的变化率。力 $ \mathbf{f} $ 的方向总是垂直于[位错](@entry_id:157482)线 $ \boldsymbol{\xi} $ [@problem_id:2768871]。

#### 滑移与攀移

[位错](@entry_id:157482)的运动可以分为两种基本模式：滑移和攀移 [@problem_id:2816731]。

1.  **滑移（Glide）**：这是[位错](@entry_id:157482)线在其**[滑移面](@entry_id:158709)**（slip plane）内的运动。[滑移面](@entry_id:158709)是由[伯格斯矢量](@entry_id:160637) $ \mathbf{b} $ 和[位错](@entry_id:157482)线指向 $ \boldsymbol{\xi} $ 共同定义的平面。滑移是一种**守恒运动**，因为它只涉及原子键的局部断裂和重新组合，不改变晶体中的原子总数。驱动滑移的力是皮克-科勒力在滑移面内的分量，它源于作用在滑移系上的**分解剪应力**（resolved shear stress）。滑移是低温下[金属塑性](@entry_id:176585)变形的主要方式，因为它不需要长程的[原子扩散](@entry_id:159939)。

2.  **攀移（Climb）**：这专指**刃位错**垂直于其滑移面的运动。攀移是一种**非守恒运动**，因为它要求额外半原子面的收缩或伸长。这只能通过原子尺度的物质输运来实现：
    *   **正攀移**（positive climb）：额外半原子面缩短，需要向[位错核心](@entry_id:201451)发射空位或吸收间隙原子。
    *   **负攀移**（negative climb）：额外半原子面伸长，需要吸收空位或发射间隙原子。
    由于攀移依赖于[点缺陷](@entry_id:136257)（空位或间隙原子）的[扩散](@entry_id:141445)，它是一个**[热激活过程](@entry_id:274558)**，通常只在高温下才变得显著。驱动攀移的力是皮克-科勒力中垂直于滑移面的分量，它源于作用在额外半原子面上的正应力分量 [@problem_id:2816731] [@problem_id:2768871]。例如，对于伯格斯矢量为 $ b\hat{x} $ 的刃位错，沿 $ x $ 方向的[正应力](@entry_id:260622) $ \sigma_{xx} $ 会产生一个攀移力。

作为一个具体的计算例子，考虑一个线指向 $ \boldsymbol{\xi} = \mathbf{e}_z $，[伯格斯矢量](@entry_id:160637) $ \mathbf{b} = b\mathbf{e}_x $，滑移面法向 $ \mathbf{n} = \mathbf{e}_y $ 的[刃位错](@entry_id:191098)。滑移方向为 $ \mathbf{s} = \mathbf{n} \times \boldsymbol{\xi} = \mathbf{e}_y \times \mathbf{e}_z = \mathbf{e}_x $。在[应力张量](@entry_id:148973) $ \boldsymbol{\sigma} $ 作用下，皮克-科勒力为：
$$ \mathbf{f} = (\boldsymbol{\sigma} \cdot (b\mathbf{e}_x)) \times \mathbf{e}_z = (\sigma_{xx} b \mathbf{e}_x + \sigma_{yx} b \mathbf{e}_y + \sigma_{zx} b \mathbf{e}_z) \times \mathbf{e}_z $$
$$ \mathbf{f} = \sigma_{xx} b (\mathbf{e}_x \times \mathbf{e}_z) + \sigma_{yx} b (\mathbf{e}_y \times \mathbf{e}_z) = -\sigma_{xx} b \mathbf{e}_y + \sigma_{yx} b \mathbf{e}_x $$
滑移力（沿 $ \mathbf{s}=\mathbf{e}_x $ 方向）的大小为 $ f_{\text{glide}} = \mathbf{f} \cdot \mathbf{s} = \sigma_{yx} b $，它由剪应力 $ \sigma_{yx} $ 驱动。攀移力（沿 $ \mathbf{n}=\mathbf{e}_y $ 方向）的大小为 $ f_{\text{climb}} = \mathbf{f} \cdot \mathbf{n} = -\sigma_{xx} b $，它由正应力 $ \sigma_{xx} $ 驱动 [@problem_id:2768871] [@problem_id:2816731]。

### [位错](@entry_id:157482)反应：分解与[堆垛层错](@entry_id:138255)

[位错](@entry_id:157482)不仅会运动，还会相互作用并发生反应。一个重要的例子是**[位错](@entry_id:157482)分解**（dislocation dissociation）。根据弗兰克能量准则，如果一条[位错](@entry_id:157482)能够分解成两条或多条总能量更低的[位错](@entry_id:157482)，这个反应在能量上是有利的。

在[面心立方](@entry_id:156319)（FCC）晶体中，一个常见的例子是滑移面（如(111)面）上的完美[位错](@entry_id:157482)分解为两个**肖克利不全[位错](@entry_id:157482)**（Shockley partial dislocations）。例如，一个伯格斯矢量为 $ \mathbf{b} = \frac{a}{2}[1\bar{1}0] $ 的完美[位错](@entry_id:157482)可以分解为：
$$ \frac{a}{2}[1\bar{1}0] \rightarrow \frac{a}{6}[2\bar{1}\bar{1}] + \frac{a}{6}[1\bar{2}1] $$
[@problem_id:2880162]

这个反应满足两个基本条件：
1.  **伯格斯矢量守恒**：产物[伯格斯矢量](@entry_id:160637)的矢量和等于反应物伯格斯矢量。
    $ \frac{a}{6}(2+1, -1-2, -1+1) = \frac{a}{6}(3, -3, 0) = \frac{a}{2}[1\bar{1}0] $。
2.  **能量降低**：产物能量之和小于反应物能量。对于FCC晶体，完美[位错](@entry_id:157482) $ \frac{a}{2}\langle 110 \rangle $ 的能量正比于 $ |\mathbf{b}|^2 = (\frac{a}{2})^2(1^2+1^2) = \frac{a^2}{2} $。肖克利不全[位错](@entry_id:157482) $ \frac{a}{6}\langle 112 \rangle $ 的能量正比于 $ |\mathbf{b}|^2 = (\frac{a}{6})^2(1^2+1^2+2^2) = \frac{a^2}{6} $。产物总能量正比于 $ \frac{a^2}{6} + \frac{a^2}{6} = \frac{a^2}{3} $。由于 $ \frac{a^2}{3}  \frac{a^2}{2} $，该分解在能量上是有利的。

这两个肖克利不全[位错](@entry_id:157482)是滑[移位](@entry_id:145848)错，它们在(111)滑移面上相互排斥，并以一个平衡距离分开。它们之间夹着一个**[堆垛层错](@entry_id:138255)**（stacking fault）区域，这是一个局部晶体堆垛顺序发生错误的平[面缺陷](@entry_id:161449)（例如，从...ABCABC...变为...AB|CABC...）。[堆垛层错](@entry_id:138255)具有一定的能量，它提供的吸[引力](@entry_id:175476)与两个不全[位错](@entry_id:157482)之间的排斥力相平衡，从而决定了分解后[位错](@entry_id:157482)的宽度。[位错](@entry_id:157482)的分解对材料的塑性行为有深远影响，例如影响[交滑移](@entry_id:195437)的难易程度和[加工硬化](@entry_id:160669)行为。