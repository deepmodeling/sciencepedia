## 引言
晶体材料的塑性变形，即在外力作用下发生的不可恢复的形状改变，其微观根源在于[晶格缺陷](@entry_id:270099)——[位错](@entry_id:157482)的运动。理解是什么力驱动这些一维缺陷在晶体中穿行，是掌握和预测[材料力学](@entry_id:201885)行为的基石。然而，如何将工程师施加的宏观应力与作用在单个原子尺度缺陷上的力精确地联系起来，构成了[材料力学](@entry_id:201885)中的一个核心问题。本文旨在系统地解答这一问题，为读者构建一个从宏观应力到微观[位错动力学](@entry_id:748548)的完整理论桥梁。

本文分为三个核心部分。在“原理与机制”一章中，我们将从普适的[构型力](@entry_id:188113)概念出发，严格推导著名的[Peach-Koehler力](@entry_id:157620)公式，并深入剖析其物理内涵、矢量性质及其与经典[Schmid定律](@entry_id:160968)的关系。随后，在“应用与跨学科联系”一章，我们将展示该理论的强大威力，通过一系列实例说明它如何被用于解释[位错相互作用](@entry_id:181480)、多种[强化机制](@entry_id:158922)、薄膜工程乃至[疲劳失效](@entry_id:202922)等复杂现象。最后，“动手实践”部分将提供具体的计算问题，帮助读者将理论知识转化为解决实际问题的能力。通过这一学习路径，读者将能够深刻理解驱动[晶体塑性](@entry_id:141273)的根本力学原理。

## 原理与机制

在引言中，我们了解了[位错](@entry_id:157482)作为[晶体塑性](@entry_id:141273)变形基本载体的重要性。本章将深入探讨驱动位错运动的力学原理。我们将从“[构型力](@entry_id:188113)”这一普适概念出发，系统地推导和诠释著名的 **Peach–Koehler 力** (Peach–Koehler force)，并阐明它如何成为连接宏观应力状态与微观[位错](@entry_id:157482)行为的关键桥梁。此外，我们还将讨论在真实材料中，如何综合考虑多种应力来源和非弹性阻力，以准确预测[位错](@entry_id:157482)的动态行为，并明确经典理论的适用边界。

### [位错](@entry_id:157482)上的[构型力](@entry_id:188113)概念

在连续介质力学中，点、[线或](@entry_id:170208)[面缺陷](@entry_id:161449)（如空洞、[位错](@entry_id:157482)、裂纹）的存在会改变固体的能量状态。当这些缺陷在材料内部移动或改变形状时，系统的总[势能](@entry_id:748988)（包括[弹性应变能](@entry_id:202243)和外力所做的功的负值）会发生变化。为了描述这种能量变化驱动的“运动趋势”，物理学家引入了**[构型力](@entry_id:188113)** (configurational force) 的概念。

[构型力](@entry_id:188113)并非作用在真实物质[质点](@entry_id:186768)上的牛顿力，而是作用在缺陷本身“构型”上的一种[广义力](@entry_id:169699)。它在[热力学](@entry_id:141121)上与系统自由能对缺陷位置的负梯度共轭。根据**[虚功原理](@entry_id:138749)** (principle of virtual work)，我们可以为[构型力](@entry_id:188113)下一个精确的定义：对于一个缺陷的任意微小虚拟位移 $\delta\mathbf{a}$，如果系统的总[势能](@entry_id:748988)变化为 $\delta\mathcal{U}$，那么作用在该缺陷上的总[构型力](@entry_id:188113) $\mathbf{F}_{\text{config}}$ 所做的[虚功](@entry_id:176403)为 $\mathbf{F}_{\text{config}} \cdot \delta\mathbf{a} = -\delta\mathcal{U}$ [@problem_id:2907452]。这个定义是普适的，它为我们定量分析作用在[位错](@entry_id:157482)等缺陷上的驱动力提供了坚实的理论基础 [@problem_id:2907429]。对于一条[位错](@entry_id:157482)线，我们更关心的是沿其长度[分布](@entry_id:182848)的力密度，即单位长度[位错](@entry_id:157482)线上的[构型力](@entry_id:188113) $\mathbf{f}$。

### Peach–Koehler 公式的推导

现在，我们将运用上述[虚功原理](@entry_id:138749)推导作用在单位长度[位错](@entry_id:157482)线上的[构型力](@entry_id:188113)，即 Peach–Koehler 力。

考虑一段长度为 $dl$ 的笔直[位错](@entry_id:157482)线段，其方向由[单位切向量](@entry_id:262985) $\boldsymbol{\xi}$ 描述，其[晶格错配](@entry_id:196802)的特征由**[伯格斯矢量](@entry_id:160637)** (Burgers vector) $\mathbf{b}$ 给出。这段[位错](@entry_id:157482)线位于一个承受均匀**柯西[应力张量](@entry_id:148973)** (Cauchy stress tensor) $\boldsymbol{\sigma}$ 的弹性体中。

设想这段[位错](@entry_id:157482)线段发生了一个微小的刚性虚拟位移 $\delta\mathbf{x}$。在这一过程中，[位错](@entry_id:157482)线扫过一个带状的微小面积，其面积矢量为 $d\mathbf{A} = (\boldsymbol{\xi} \, dl) \times \delta\mathbf{x}$。[位错](@entry_id:157482)的移动意味着在这个新扫过的面上，一侧的材料相对于另一侧发生了量值为 $\mathbf{b}$ 的滑移。外部应[力场](@entry_id:147325) $\boldsymbol{\sigma}$ 在这个新产生的滑移面上做了功。根据柯西牵引定理，在法向为 $\mathbf{n}$ 的面上，牵[引力](@entry_id:175476)矢量为 $\mathbf{t}_{\text{trac}} = \boldsymbol{\sigma} \cdot \mathbf{n}$。因此，在[面积元](@entry_id:263205) $d\mathbf{A}$ 上，应[力场](@entry_id:147325)做的功 $\delta W$ 为牵[引力](@entry_id:175476)与位移 $\mathbf{b}$ 的[点积](@entry_id:149019)：

$$
\delta W = (\boldsymbol{\sigma} \cdot d\mathbf{A}) \cdot \mathbf{b}
$$

由于柯西应力张量在线弹性理论中是对称的（$\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$），我们可以利用张量恒等式 $(\boldsymbol{\sigma} \cdot \mathbf{u}) \cdot \mathbf{v} = \mathbf{u} \cdot (\boldsymbol{\sigma}^T \cdot \mathbf{v})$，将上式改写为：

$$
\delta W = d\mathbf{A} \cdot (\boldsymbol{\sigma} \cdot \mathbf{b})
$$

这个表达式揭示了矢量 $\boldsymbol{\sigma} \cdot \mathbf{b}$ 的深刻物理意义。它并非一个作用在某个物理平面上的真实牵[引力](@entry_id:175476)，而是一个**[功共轭](@entry_id:194957)矢量** (work-conjugate vector)。它的物理含义是：当[位错](@entry_id:157482)扫过一个单位法向为 $\mathbf{n}$ 的微元面积时，应[力场](@entry_id:147325)对外做的功等于 $(\boldsymbol{\sigma} \cdot \mathbf{b}) \cdot \mathbf{n}$ [@problem_id:2907511]。

将 $d\mathbf{A}$ 的表达式代入功的计算式中：

$$
\delta W = ((\boldsymbol{\xi} \, dl) \times \delta\mathbf{x}) \cdot (\boldsymbol{\sigma} \cdot \mathbf{b})
$$

利用[标量三重积](@entry_id:177480)的轮换性质 $(\mathbf{A} \times \mathbf{B}) \cdot \mathbf{C} = (\mathbf{C} \times \mathbf{A}) \cdot \mathbf{B}$，我们可以得到：

$$
\delta W = ((\boldsymbol{\sigma} \cdot \mathbf{b}) \times (\boldsymbol{\xi} \, dl)) \cdot \delta\mathbf{x}
$$

根据[构型力](@entry_id:188113)的定义，这段[位错](@entry_id:157482)线段上的总[构型力](@entry_id:188113) $\mathbf{F} = \mathbf{f} \, dl$ 在虚拟位移 $\delta\mathbf{x}$ 中所做的功为 $\delta W_{\text{force}} = \mathbf{F} \cdot \delta\mathbf{x} = (\mathbf{f} \, dl) \cdot \delta\mathbf{x}$。由于外力做功等于系统势能的减少，即 $\delta W = -\delta\mathcal{U}$，我们有 $\delta W = \delta W_{\text{force}}$。比较两个功的表达式：

$$
((\mathbf{f} \, dl) \cdot \delta\mathbf{x}) = ((\boldsymbol{\sigma} \cdot \mathbf{b}) \times (\boldsymbol{\xi} \, dl)) \cdot \delta\mathbf{x}
$$

由于虚拟位移 $\delta\mathbf{x}$ 是任意的，因此我们可以得到单位长度[位错](@entry_id:157482)线上的[构型力](@entry_id:188113) $\mathbf{f}$ 的表达式：

$$
\mathbf{f} = (\boldsymbol{\sigma} \cdot \mathbf{b}) \times \boldsymbol{\xi}
$$

这就是著名的 **Peach–Koehler 公式**。它精确地描述了外部应[力场](@entry_id:147325)如何转化为驱动[位错运动](@entry_id:143448)的线力密度。值得强调的是，尽管我们从一个特定的[虚功](@entry_id:176403)论证出发，但通过其他更复杂的理论途径，如基于 **Eshelby [能量动量张量](@entry_id:150076)** (Eshelby energy-momentum tensor) 的积分方法，也能殊途同归地得到完全相同的表达式，这彰显了其在连续介质[弹性理论](@entry_id:184142)框架下的普适性和深刻性 [@problem_id:2907429]。

### Peach–Koehler 力的性质与诠释

Peach–Koehler 公式不仅是一个数学表达式，更蕴含了丰富的物理内容。

#### 矢量性质与[不变性](@entry_id:140168)

首先，Peach–Koehler 力 $\mathbf{f}$ 是一个矢量。由于它是一个叉积的产物，其方向遵循[右手定则](@entry_id:156766)，并且**始终垂直于[位错](@entry_id:157482)线切向 $\boldsymbol{\xi}$**，即 $\mathbf{f} \cdot \boldsymbol{\xi} = 0$。这意味着作用在直[位错](@entry_id:157482)段上的力只能驱动其在垂直于自身的方向上运动，而不能使其沿着线方向伸长或缩短。

其次，公式的结构决定了其在描述约定改变时的变换性质。[位错](@entry_id:157482)的物理实体是唯一的，但其数学描述（$\mathbf{b}$ 和 $\boldsymbol{\xi}$ 的方向）存在约定。根据 FS/RH (Finish-Start/Right-Hand) 约定，如果我们将[位错](@entry_id:157482)线的指向反向（$\boldsymbol{\xi} \to -\boldsymbol{\xi}$），那么为了保持对同一物理缺陷的描述，伯格斯矢量也必须反向（$\mathbf{b} \to -\mathbf{b}$）。让我们考察 Peach–Koehler 力在这种变换下的行为 [@problem_id:2907513]：

1.  若只将[伯格斯矢量](@entry_id:160637)反向 ($\mathbf{b} \to -\mathbf{b}$)，力变为 $\mathbf{f}' = (\boldsymbol{\sigma} \cdot (-\mathbf{b})) \times \boldsymbol{\xi} = -(\boldsymbol{\sigma} \cdot \mathbf{b}) \times \boldsymbol{\xi} = -\mathbf{f}$。这意味着一个反[位错](@entry_id:157482)在相同应[力场](@entry_id:147325)中会受到大小相等、方向相反的力。
2.  若只将线矢量反向 ($\boldsymbol{\xi} \to -\boldsymbol{\xi}$)，力变为 $\mathbf{f}'' = (\boldsymbol{\sigma} \cdot \mathbf{b}) \times (-\boldsymbol{\xi}) = -(\boldsymbol{\sigma} \cdot \mathbf{b}) \times \boldsymbol{\xi} = -\mathbf{f}$。
3.  若同时反向 ($\mathbf{b} \to -\mathbf{b}$, $\boldsymbol{\xi} \to -\boldsymbol{\xi}$)，力变为 $\mathbf{f}''' = (\boldsymbol{\sigma} \cdot (-\mathbf{b})) \times (-\boldsymbol{\xi}) = (-1)(-1)((\boldsymbol{\sigma} \cdot \mathbf{b}) \times \boldsymbol{\xi}) = \mathbf{f}$。

第三个结果至关重要：**Peach–Koehler 力对于描述约定的同时改变是不变的**。这保证了计算出的力是一个真实的物理量，不依赖于我们观察和定义[位错](@entry_id:157482)的任意选择。

#### 滑移力与攀移力的分解

由于力 $\mathbf{f}$ 垂直于[位错](@entry_id:157482)线 $\boldsymbol{\xi}$，它位于一个由[位错](@entry_id:157482)线法向构成的平面内。我们可以将这个力分解到两个对[位错运动](@entry_id:143448)至关重要的方向上：

*   **滑移力 (Glide Force)**: 位于**[滑移面](@entry_id:158709)** (slip plane) 内且垂直于[位错](@entry_id:157482)线的力分量。该力驱动[位错](@entry_id:157482)在滑移面上运动，这是一种保守运动，不涉及物质输运。
*   **攀移力 (Climb Force)**: 垂直于[滑移面](@entry_id:158709)的力分量。该力驱动[位错](@entry_id:157482)离开其[滑移面](@entry_id:158709)，这是一种非保守运动，需要通过空位或间隙原子的[扩散](@entry_id:141445)来完成。

对于一条刃型位错，其[伯格斯矢量](@entry_id:160637) $\mathbf{b}$ 垂直于线矢量 $\boldsymbol{\xi}$。滑移面即为包含 $\mathbf{b}$ 和 $\boldsymbol{\xi}$ 的平面，设其法向为 $\mathbf{n}$。此时，作用在滑移方向（平行于 $\mathbf{b}$）上的滑移力大小为 $f_g = b\tau$，其中 $\tau$ 是在[滑移面](@entry_id:158709)上沿滑移方向的**[分解切应力](@entry_id:201022)** (resolved shear stress)。而垂直于[滑移面](@entry_id:158709)的攀移力则与作用在[滑移面](@entry_id:158709)上的[正应力](@entry_id:260622)分量相关 [@problem_id:2907456]。例如，静水压力 $(\boldsymbol{\sigma} = -p\mathbf{I})$ 会对刃型位错产生纯攀移力，大小为 $f_c = pb$，但不会产生滑移力。对于[螺型位错](@entry_id:182908)，由于 $\mathbf{b}$ 平行于 $\boldsymbol{\xi}$，[静水压力](@entry_id:275365)不会产生任何力。

### 作为[Schmid定律](@entry_id:160968)的矢量推广

在[晶体塑性理论](@entry_id:180579)的早期，**Schmid 定律** (Schmid's law) 已经揭示，晶体的滑移启动取决于作用在特定[滑移系](@entry_id:136401)上的[分解切应力](@entry_id:201022) $\tau$ 是否达到临界值 $\tau_c$。这是一个标量判据。Peach–Koehler 力理论则提供了一个更全面、更强大的矢量化框架 [@problem_id:2907470]。

我们可以证明，Peach–Koehler 力在滑移方向上的投影，其大小恰好是伯格斯矢量大小 $b$ 与[分解切应力](@entry_id:201022) $\tau$ 的乘积。考虑一个[滑移系](@entry_id:136401)，其[滑移面](@entry_id:158709)法向为 $\mathbf{n}$，滑移方向为 $\mathbf{s}$，伯格斯矢量 $\mathbf{b} = b\mathbf{s}$。[位错](@entry_id:157482)线 $\boldsymbol{\xi}$ 位于该[滑移面](@entry_id:158709)内。在滑移面内垂直于 $\boldsymbol{\xi}$ 的滑移方向为 $\mathbf{g} = \mathbf{n} \times \boldsymbol{\xi}$。单位长度上的滑移力大小 $f_g$ 为：

$$
f_g = \mathbf{f} \cdot \mathbf{g} = ((\boldsymbol{\sigma} \cdot b\mathbf{s}) \times \boldsymbol{\xi}) \cdot (\mathbf{n} \times \boldsymbol{\xi})
$$

通过[矢量代数](@entry_id:152340)运算，可以证明上式简化为 [@problem_id:2907451]：

$$
f_g = b (\mathbf{n} \cdot (\boldsymbol{\sigma} \cdot \mathbf{s})) = b \tau
$$

其中 $\tau = \mathbf{n} \cdot (\boldsymbol{\sigma} \cdot \mathbf{s})$ 正是 Schmid 定律中的[分解切应力](@entry_id:201022)。对于[单轴拉伸](@entry_id:188287)应力 $\sigma_a$，加载方向与 $\mathbf{n}$ 和 $\mathbf{s}$ 的夹角分别为 $\phi$ 和 $\lambda$，我们有 $\tau = \sigma_a \cos\phi \cos\lambda$，因此滑移力为 $f_g = b \sigma_a \cos\phi \cos\lambda$。这里的 $\cos\phi \cos\lambda$ 就是著名的**施密特因子** (Schmid factor)。

Peach–Koehler 理论的优越性在于：

1.  **统一处理所有[位错](@entry_id:157482)类型**：Schmid 定律通常针对理想的滑移情况，而 Peach–Koehler 公式能精确计算混合型[位错](@entry_id:157482)的受力，正确地包含了其刃分量和螺分量对滑移力的不同贡献 [@problem_id:2907470]。
2.  **解决螺[位错](@entry_id:157482)的模糊性**：对于螺[位错](@entry_id:157482)，由于 $\mathbf{b} \parallel \boldsymbol{\xi}$，它没有唯一的[滑移面](@entry_id:158709)，可以发生**[交滑移](@entry_id:195437)** (cross-slip)。Schmid 定律在此处适用性模糊。而 Peach–Koehler 力是唯一确定的，可以被分解到任何可能的滑移方向上，从而定量比较在不同[滑移面](@entry_id:158709)上（如主滑移面和[交滑移](@entry_id:195437)面）的驱动力大小，为预测[交滑移](@entry_id:195437)行为提供了定量依据 [@problem_id:2907470]。
3.  **包含攀移力**：它自然地包含了攀移力分量，这是 Schmid 定律完全没有涉及的。这使得分析[高温蠕变](@entry_id:189747)等涉及攀移的过程成为可能。

---
#### **应用实例：[混合位错](@entry_id:191088)的[交滑移](@entry_id:195437)趋势分析**
为了具体说明 Peach–Koehler 力的矢量分解应用，我们考虑一个计算实例 [@problem_id:2907436]。

假设一个[混合位错](@entry_id:191088)位于一个由[应力张量](@entry_id:148973) $\boldsymbol{\sigma} = \begin{pmatrix} 100  50  30 \\ 50  -80  40 \\ 30  40  60 \end{pmatrix} \text{MPa}$ 所描述的应[力场](@entry_id:147325)中。其伯格斯矢量为 $\mathbf{b} = b_0(1,0,0)$，线矢量为 $\boldsymbol{\xi} = \frac{1}{\sqrt{2}}(1,1,0)$。主[滑移面](@entry_id:158709)法向为 $\mathbf{n}_1 = (0,0,1)$，一个可能的[交滑移](@entry_id:195437)面法向为 $\mathbf{n}_2 = (0,1,0)$。

1.  **计算 Peach–Koehler 力 $\mathbf{f}$**：
    首先计算 $\boldsymbol{\sigma} \cdot \mathbf{b} = b_0(100, 50, 30)^T$ MPa。
    然后计算叉积 $\mathbf{f} = (\boldsymbol{\sigma} \cdot \mathbf{b}) \times \boldsymbol{\xi}$，得到 $\mathbf{f} = \frac{b_0}{\sqrt{2}}(-30, 30, 50)^T$ (单位 N/m)。

2.  **计算在主[滑移面](@entry_id:158709)上的滑移力 $f_g$**：
    主滑移面内的滑移方向为 $\mathbf{m}_1 = \frac{\mathbf{n}_1 \times \boldsymbol{\xi}}{|\mathbf{n}_1 \times \boldsymbol{\xi}|} = \frac{1}{\sqrt{2}}(-1, 1, 0)^T$。
    将 $\mathbf{f}$ 投影到 $\mathbf{m}_1$ 上：$f_g = \mathbf{f} \cdot \mathbf{m}_1 = 30b_0$。

3.  **计算在[交滑移](@entry_id:195437)面上的滑移力 $f_{cs}$**：
    [交滑移](@entry_id:195437)面内的滑移方向为 $\mathbf{m}_2 = \frac{\mathbf{n}_2 \times \boldsymbol{\xi}}{|\mathbf{n}_2 \times \boldsymbol{\xi}|} = (0, 0, -1)^T$。
    将 $\mathbf{f}$ 投影到 $\mathbf{m}_2$ 上：$f_{cs} = \mathbf{f} \cdot \mathbf{m}_2 = -\frac{50b_0}{\sqrt{2}}$。

4.  **评估[交滑移](@entry_id:195437)趋势**：
    比较两个力的大小，我们计算比值 $R = \frac{|f_{cs}|}{|f_g|} = \frac{50/\sqrt{2}}{30} \approx 1.179$。
    由于 $R > 1$，作用在[交滑移](@entry_id:195437)方向上的驱动力大于主滑移方向上的驱动力，表明从力学角度看，该[位错](@entry_id:157482)有向[交滑移](@entry_id:195437)面运动的趋势。当然，实际发生[交滑移](@entry_id:195437)还需要满足运动学条件（伯格斯矢量必须位于两个平面的交线内），本例中该条件恰好满足。

这个例子清晰地展示了 Peach–Koehler 力的矢量性质如何让我们能够定量分析复杂的位错运动行为。

---

### 实际微观结构中的Peach–Koehler力

#### 应[力场](@entry_id:147325)的叠加

在真实的晶体材料中，[位错](@entry_id:157482)感受到的局部应[力场](@entry_id:147325) $\boldsymbol{\sigma}$ 通常是多个来源的叠加。由于 Peach–Koehler 公式对应力 $\boldsymbol{\sigma}$ 是线性的，总的驱动力也是各项贡献之和 [@problem_id:2907457]：

$$
\mathbf{f}_{\text{total}} = ((\boldsymbol{\sigma}^{\text{ext}} + \boldsymbol{\sigma}^{\text{int}} + \boldsymbol{\sigma}^{\text{self}}) \cdot \mathbf{b}) \times \boldsymbol{\xi} = \mathbf{f}^{\text{ext}} + \mathbf{f}^{\text{int}} + \mathbf{f}^{\text{self}}
$$

*   **外加应力 ($\boldsymbol{\sigma}^{\text{ext}}$)**：由外部宏观载荷产生，通常在微观尺度上可视为均匀。这是驱动塑性变形的主要动力。
*   **[内应力](@entry_id:193721) ($\boldsymbol{\sigma}^{\text{int}}$)**：由材料内部其他缺陷（如其他[位错](@entry_id:157482)、析出相、[晶界](@entry_id:196965)等）产生。例如，[位错塞积](@entry_id:187511)群中的领先[位错](@entry_id:157482)会受到来自后方同号[位错](@entry_id:157482)的排斥力（一种**[背应力](@entry_id:198105)**），这会阻碍其继续运动，是应变硬化的重要来源之一。
*   **自应力 ($\boldsymbol{\sigma}^{\text{self}}$)**：[位错](@entry_id:157482)线自身的应[力场](@entry_id:147325)。对于无限长直[位错](@entry_id:157482)，自应力不会对其自身产生净平移力。但对于**弯曲的[位错](@entry_id:157482)线**，自应力会产生一个指向[曲率中心](@entry_id:270032)的力，其效果类似于一根具有**线张力** (line tension) 的弹性弦，总是试图缩短[位错](@entry_id:157482)线长度，抵抗[位错](@entry_id:157482)弓出。

#### 弹性驱动力与[晶格](@entry_id:196752)阻力

至此我们讨论的 Peach–Koehler 力都是在连续弹性介质模型下得到的**弹性驱动力**。然而，[位错](@entry_id:157482)的运动还必须克服来自离散[晶格](@entry_id:196752)的固有阻力。

最重要的阻力之一是**佩尔斯力** (Peierls force)，它源于[位错](@entry_id:157482)芯在原子点阵中从一个低能位置移动到下一个低能位置时需要克服的能量势垒。这个阻力可以等效为一个临界的[分解切应力](@entry_id:201022)，即**佩尔斯应力** (Peierls stress) $\tau_P$。只有当弹性驱动力对应的[分解切应力](@entry_id:201022) $\tau$ 超过 $\tau_P$ 时，[位错](@entry_id:157482)才能在[晶格](@entry_id:196752)中开始宏观运动。

因此，[位错运动](@entry_id:143448)的判据并非简单的 $f_g > 0$，而是 $\tau = f_g/b > \tau_P$ [@problem_id:2907471]。例如，一个[刃位错](@entry_id:191098)即使受到一个由 $\tau = 60 \text{ MPa}$ 产生的滑移力，但如果其所在[晶格](@entry_id:196752)的佩尔斯应力为 $\tau_P = 75 \text{ MPa}$，该[位错](@entry_id:157482)仍将保持静止。这是区分弹性驱动力与净驱动力的关键。

一旦位错运动起来，它还会受到各种与速度相关的[阻尼力](@entry_id:265706)，如与[声子](@entry_id:140728)和电子的相互作用。在过阻尼情况下，[位错](@entry_id:157482)的[稳态](@entry_id:182458)速度 $v$ 通常与净驱动力成正比，即 $v \propto (f_g - b\tau_P)$。

### 经典公式的适用范围与局限性

经典 Peach–Koehler 公式是一个极为强大和成功的理论工具，但作为教学者和研究者，我们必须清醒地认识到其成立所依赖的假设及其失效的场景 [@problem_id:2907452]。

1.  **小应变[线性弹性](@entry_id:166983)假设**：公式的推导基于小应变假设和线弹性[本构关系](@entry_id:186508)。当材料经历[大变形](@entry_id:167243)或进入[非线性弹性](@entry_id:185743)/[弹塑性](@entry_id:193198)区域时，需要使用有限变形理论和相应的[能量动量张量](@entry_id:150076)，经典公式不再直接适用。

2.  **连续介质与理想化[位错](@entry_id:157482)芯假设**：理论将[位错](@entry_id:157482)芯视为一个数学[奇点](@entry_id:137764)或一个半径可忽略的区域。这忽略了原子尺度上复杂的[位错](@entry_id:157482)芯结构和能量。当[位错](@entry_id:157482)芯的展宽、重构或与杂质原子的交互作用变得重要时（例如在解释[非施密特效应](@entry_id:188957)时），纯粹的连续介质理论就显得不足，必须结合[原子模拟](@entry_id:199973)。

3.  **准静态平衡假设**：推导过程忽略了惯性效应。当[位错](@entry_id:157482)以接近材料中[弹性波](@entry_id:196203)速（如剪切波速）的量级高速运动时，动态效应和能量辐射（[声子](@entry_id:140728)发射）变得不可忽略，需要引入动态[构型力](@entry_id:188113)理论。

4.  **简单柯西介质假设**：理论假设材料的[应变能](@entry_id:162699)仅依赖于应变本身。对于在微纳米尺度上表现出显著尺寸效应的材料，可能需要考虑应变梯度的影响（如[应变梯度塑性理论](@entry_id:172852)），这会在[构型力](@entry_id:188113)表达式中引入额外的高阶项。

综上所述，Peach–Koehler 力理论为我们理解[晶体塑性](@entry_id:141273)变形的力学驱动力提供了基石。它深刻地揭示了宏观应力如何通过[位错](@entry_id:157482)这一媒介转化为微观滑移，并以其矢量形式完美地统一和推广了[Schmid定律](@entry_id:160968)。在后续的学习中，我们将在此基础上，进一步探讨[位错](@entry_id:157482)间的相互作用、[位错](@entry_id:157482)群的集体行为以及更复杂的材料响应。