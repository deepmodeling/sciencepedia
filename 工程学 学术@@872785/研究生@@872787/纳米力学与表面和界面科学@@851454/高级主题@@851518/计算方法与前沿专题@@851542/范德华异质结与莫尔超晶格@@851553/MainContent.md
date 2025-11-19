## 引言
二维材料的出现彻底改变了[材料科学](@entry_id:152226)的面貌，而通过范德华力将这些原子级薄层堆叠起来，构建所谓的**[范德华异质结](@entry_id:142819)**，则开启了一个全新的研究[范式](@entry_id:161181)。在这些异质结中，当层与层之间存在微小的[晶格失配](@entry_id:196802)或扭转角时，一种名为**莫尔超晶格**的长周期性图案便会涌现。这种莫尔图案不仅仅是几何上的[干涉条纹](@entry_id:176719)，它更是一个深刻影响材料基本属性的物理实体，为按需设计和调控材料的电子、光学、力学乃至[拓扑性质](@entry_id:141605)提供了前所未有的可能性。

然而，要充分利用莫尔超晶格这一强大平台，我们必须首先回答一系列根本性问题：莫尔超晶格的结构是如何形成的？驱动其变化的物理机制是什么？这些微观结构的变化又是如何转化为宏观可观测的物性调控的？本文旨在系统性地解决这一知识鸿沟，为读者构建一个关于[范德华异质结](@entry_id:142819)与莫尔[超晶格](@entry_id:200197)物理学的坚实理论框架。

在接下来的内容中，我们将分三部分展开深入探讨。在“**原理与机制**”一章中，我们将从莫尔图案的几何描述出发，剖析层间[范德华相互作用](@entry_id:168429)的能量学，并建立描述其力学弛豫的连续介质模型，揭示结构重构的核心机制。随后，在“**应用与[交叉](@entry_id:147634)学科联系**”一章中，我们将展示这些基本原理如何在[纳米力学](@entry_id:185346)、电子与光电学、量子模拟以及[热输运](@entry_id:198424)等多个前沿领域中催生出新颖的应用和物理现象。最后，“**动手实践**”部分将通过具体的计算问题，帮助读者将理论知识应用于实际分析中，从而加深对畴壁宽度、层间作用势构建等核心概念的理解。通过这一系列的学习，读者将能够全面掌握莫尔物理的核心，并洞悉其在未来量子材料设计中的巨大潜力。

## 原理与机制

继引言之后，本章旨在深入阐述构成[范德华异质结](@entry_id:142819)和莫尔超晶格物理学的基本原理与核心机制。我们将从莫尔图案的几何描述开始，然后探讨驱动这些系统行为的能量学，建立描述其力学弛豫的连续介质模型，并最终分析结构重构的关键机制及其物理后果。

### 莫尔[超晶格](@entry_id:200197)的几何框架

当两个具有相似[晶格结构](@entry_id:145664)的二维晶体堆叠在一起，并存在微小的[晶格失配](@entry_id:196802)或扭转角时，一种名为**莫尔[超晶格](@entry_id:200197)**的长周期性图案便会涌现。这种图案本质上是两种原子[晶格](@entry_id:196752)周期性势场的几何干涉效应。

理解莫尔周期性的最直观方式之一是通过[倒易空间](@entry_id:754151)。考虑一个由[石墨烯](@entry_id:143512)（G）和[六方氮化硼](@entry_id:198061)（hBN）组成的[异质结](@entry_id:196407)。两种材料都具有六角[晶格](@entry_id:196752)，但晶格常数略有不同。莫尔超晶格的周期性由一个新的倒易格矢 $\mathbf{q}$ 描述，它等于两层材料中几乎共线的原始倒易格矢 $\mathbf{G}_{\mathrm{G}}$ 和 $\mathbf{G}_{\mathrm{hBN}}$ 之差。对于一个由扭转角 $\theta$ 和相对[晶格失配](@entry_id:196802) $\delta = (a_{\mathrm{hBN}} - a_{\mathrm{G}})/a_{\mathrm{G}}$ 共同决定的系统，莫尔[超晶格](@entry_id:200197)的倒易格矢大小 $q = |\mathbf{q}|$ 近似为 $q \approx G_{\mathrm{G}} \sqrt{\delta^2 + \theta^2}$，其中 $G_{\mathrm{G}}$ 是石墨烯的倒易格矢大小。由于实空间周期 $L$ 与[倒易空间](@entry_id:754151)周期 $q$ 的关系为 $L = 4\pi/(q\sqrt{3})$（对于六角[晶格](@entry_id:196752)），我们可以推导出莫尔周期长度的著名近似关系 [@problem_id:2796945]：

$L \approx \frac{a_{\mathrm{G}}}{\sqrt{\delta^2+\theta^2}}$

其中 $a_{\mathrm{G}}$ 是石墨烯的[晶格常数](@entry_id:158935)。这个关系式清晰地表明，当失配 $\delta$ 和扭转角 $\theta$ 都很小时，莫尔周期 $L$ 会远大于原子晶格常数 $a_{\mathrm{G}}$。例如，对于[晶格常数](@entry_id:158935) $a_{\mathrm{G}}=0.246\,\mathrm{nm}$ 的石墨烯和 $a_{\mathrm{hBN}}=0.250\,\mathrm{nm}$ 的[六方氮化硼](@entry_id:198061)，其固有失配 $\delta \approx 0.0163$。如果实验测得的莫尔周期为 $L=13.4\,\mathrm{nm}$，利用上述公式可以反推出两层之间的扭转角约为 $\theta \approx 0.49^\circ$。[@problem_id:2796945]

为了更深入地描述莫尔超晶格的内部结构，我们引入**连续介质位移场** $\boldsymbol{\Delta}(\mathbf{r})$ 的概念。这个矢量场描述了在空间位置 $\mathbf{r}$ 处，顶层[晶格](@entry_id:196752)相对于底层[晶格](@entry_id:196752)的局域相对平移。对于由小角度扭转 $\theta$ 和均匀双轴应变 $e$（等价于[晶格失配](@entry_id:196802) $\delta$）引起的莫尔图案，位移场可以近似为位置 $\mathbf{r}$ 的线性函数 [@problem_id:2796931]：

$\boldsymbol{\Delta}(\mathbf{r}) = \left[ \mathbf{I} - \mathcal{R}(-\theta)(\mathbf{I}+e\mathbf{I}) \right] \mathbf{r} = \mathbf{M}\mathbf{r}$

这里，$\mathbf{I}$ 是[单位矩阵](@entry_id:156724)，$\mathcal{R}(-\theta)$ 是旋转矩阵，$\mathbf{M}$ 被称为“失配矩阵”。$\boldsymbol{\Delta}(\mathbf{r})$ 的空间变化描述了层间堆叠序的连续演化。例如，$\boldsymbol{\Delta}(\mathbf{r}) = \mathbf{0}$ （模上底层[晶格](@entry_id:196752)的任意格矢）对应于高对称的**AA堆叠**，而 $\boldsymbol{\Delta}(\mathbf{r})$ 等于[连接子](@entry_id:177005)[晶格](@entry_id:196752)的[基矢](@entry_id:199546)量 $\boldsymbol{\tau}$ 或 $-\boldsymbol{\tau}$ 时，则分别对应于**AB堆叠**和**BA堆叠**。随着位置 $\mathbf{r}$ 在莫尔晶胞内变化，$\boldsymbol{\Delta}(\mathbf{r})$ 会平滑地扫过所有可能的层间堆叠构型。

莫尔[超晶格](@entry_id:200197)的周期性可以通过位移场的定义来确定。当空间位置平移一个莫尔格矢 $\mathbf{A}_i$ 时，局域堆叠序必须复现，这意味着位移场的变化量等于底层[晶格](@entry_id:196752)的一个格矢 $\mathbf{a}_i$。即 $\boldsymbol{\Delta}(\mathbf{r} + \mathbf{A}_i) - \boldsymbol{\Delta}(\mathbf{r}) = \mathbf{a}_i$。利用 $\boldsymbol{\Delta}(\mathbf{r})$ 的[线性形式](@entry_id:276136)，我们得到 $\mathbf{M}\mathbf{A}_i = \mathbf{a}_i$，这意味着莫尔格矢由 $\mathbf{A}_i = \mathbf{M}^{-1}\mathbf{a}_i$ 给出。通过计算，可以得到失配矩阵 $\mathbf{M}$ 在小角度和小编应近似下为 $\mathbf{M} \approx -e\mathbf{I} - \theta\mathbf{S}$（其中 $\mathbf{S}$ 是[旋转生成元](@entry_id:154292)），其[逆矩阵](@entry_id:140380)的模量与 $\sqrt{e^2+\theta^2}$ 成反比。最终，我们从这个连续介质框架中同样推导出莫尔[晶格常数](@entry_id:158935) $L_m$ [@problem_id:2796931]：

$L_{m} = |\mathbf{A}_i| = \frac{|\mathbf{a}_i|}{|\det(\mathbf{M})|^{1/2}} \approx \frac{a}{\sqrt{e^{2}+\theta^{2}}}$

这与之前从[倒易空间](@entry_id:754151)得到的结论完全一致，展示了不同理论视角的统一性。

### 层间[范德华相互作用](@entry_id:168429)的能量学

莫尔超晶格的几何结构决定了其潜在的物理性质，而这些性质的涌现则根植于层间相互作用的能量学。最主要的相互作用力是**范德华（van der Waals, vdW）力**。

描述vdW相互作用存在两种主要理论方法：微观的**成对势加和方法**（如[Lennard-Jones势](@entry_id:143105)）和宏观的**连续介质理论**（[Lifshitz理论](@entry_id:188943)）。[@problem_id:2796929]
- **Lennard-Jones (L-J) 方法**将材料视为离散原子的集合，总相互作用能通过对所有原子对的 $C_6/r^6$ 型吸引势和短程[排斥势](@entry_id:185622)求和得到。这种方法本质上是**可加的**，即忽略了[多体效应](@entry_id:173569)（如屏蔽），并且未考虑**电磁[延迟效应](@entry_id:199612)**（即光速的有限性）。它在亚纳米至几纳米的极小间距下是合理的近似，此时原子尺度的[晶格](@entry_id:196752)堆叠效应显著，且非延迟近似成立。对于两个二维原子层，通过积分可以得到非延迟区的相互作用能密度随间距 $d$ 按 $d^{-4}$ 规律衰减。
- **Lifshitz 理论**则将材料视为具有频率依赖介电函数 $\varepsilon(i\xi)$ 的连续介质。它通过宏观[量子电动力学](@entry_id:150740)和涨落-耗散定理计算相互作用能。该理论天然地包含了**非可加性**（如[金属中的屏蔽](@entry_id:146568)效应）和**[延迟效应](@entry_id:199612)**。对于[二维材料](@entry_id:142244)，它在大于原子间距的尺度上均有效。在非延迟极限下，它同样预测能量密度按 $d^{-4}$ 衰减；而在[延迟效应](@entry_id:199612)显著的大间距下（通常大于几十纳米），衰减规律会过渡到 $d^{-5}$。

由于[Lifshitz理论](@entry_id:188943)的普适性和精确性，在研究莫尔[超晶格](@entry_id:200197)这种宏观[周期结构](@entry_id:753351)时，连续介质的观点更为恰当。在这一框架下，描述层间相互作用的核心物理量是**广义[堆垛层错能](@entry_id:145736)（Generalized Stacking Fault Energy, GSFE）**，记为 $U(\boldsymbol{\Delta})$。

$U(\boldsymbol{\Delta})$ 定义为，在保持层间距和层内[晶格](@entry_id:196752)恒定的情况下，将一层相对于另一层刚性平移一个面内[位移矢量](@entry_id:262782) $\boldsymbol{\Delta}$ 所引起的体系总能量变化量（单位面积）。[@problem_id:2796943] 这是一个[势能面](@entry_id:147441)，它完全由两层晶体的[原子结构](@entry_id:137190)和化学性质决定，与莫尔周期无关。计算 $U(\boldsymbol{\Delta})$ 的标准[第一性原理方法](@entry_id:268553)（如密度泛函理论，DFT）涉及以下步骤：
1.  构建一个包含两层晶体和足够真空层的超胞。
2.  对于一系列离散的位移 $\boldsymbol{\Delta}$，进行刚性平移操作，即**不进行任何离子位置弛豫**。
3.  对每个固定的原子构型进行单点能计算，得到总能量 $E_{\mathrm{bilayer}}(\boldsymbol{\Delta})$。
4.  将能量变化量除以超胞面积 $A$。有两种等效的定义方式 [@problem_id:2796943]：
    -   相对定义：$U(\boldsymbol{\Delta}) = [E_{\mathrm{bilayer}}(\boldsymbol{\Delta}) - E_{\mathrm{bilayer}}(\boldsymbol{\Delta}_{\mathrm{ref}})]/A$，其中 $\boldsymbol{\Delta}_{\mathrm{ref}}$ 是一个参考堆叠构型（通常是能量最低点）。
    -   绝对定义（[相互作用能](@entry_id:264333)）：$U(\boldsymbol{\Delta}) = [E_{\mathrm{bilayer}}(\boldsymbol{\Delta}) - E_{\mathrm{mono},1} - E_{\mathrm{mono},2}]/A$，其中 $E_{\mathrm{mono},i}$ 是在相同计算条件下单个孤立层的能量。

$U(\boldsymbol{\Delta})$ 的周期性和形状编码了层间相互作用的所有信息。对于六角[晶格](@entry_id:196752)，其最低阶[傅里叶级数](@entry_id:139455)近似形式可以写作 [@problem_id:2796930]：

$U(\boldsymbol{\Delta}) = U_{0} + 2 V \sum_{j=1}^{3} \cos(\mathbf{G}_{j}\cdot \boldsymbol{\Delta})$

其中 $\mathbf{G}_j$ 是底层[晶格](@entry_id:196752)最短的三个对称相关的倒易格矢，$V$ 是能量起伏的振幅。这个[势能面](@entry_id:147441)包含了能量极小值点（如AB/BA堆叠）和极大值点（如AA堆叠）。例如，AA堆叠对应 $\boldsymbol{\Delta}_{\mathrm{AA}}=\mathbf{0}$，其能量为 $U(\boldsymbol{\Delta}_{\mathrm{AA}}) = U_0 + 6V$。AB堆叠对应 $\mathbf{G}_j \cdot \boldsymbol{\Delta}_{\mathrm{AB}} = 2\pi/3$，其能量为 $U(\boldsymbol{\Delta}_{\mathrm{AB}}) = U_0 - 3V$。因此，AA和AB堆叠之间的能量差为 $\Delta U = U(\boldsymbol{\Delta}_{\mathrm{AA}}) - U(\boldsymbol{\Delta}_{\mathrm{AB}}) = 9V$。这个能量差 $\Delta U$ 是一个正值（对于大多数vdW材料），量化了不同堆叠方式的能量优劣，构成了驱动后续力学弛豫和结构重构的根本动力。例如，若 $V=2.137\times 10^{-2}\,\mathrm{J\,m^{-2}}$，则驱动力大小为 $\Delta U \approx 0.1923\,\mathrm{J\,m^{-2}}$。[@problem_id:2796930]

### 莫尔弛豫的连续介质模型

建立了莫尔几何框架和层间相互作用的能量学基础后，我们现在可以将它们结合起来，构建一个描述莫尔超[晶格力学](@entry_id:189426)行为的连续介质模型。

一个核心且微妙的概念必须首先澄清：GSFE势函数 $U(\boldsymbol{\Delta})$ 的周期性是由原子[晶格](@entry_id:196752)决定的（周期为 $a$），而莫尔图案的[能量景观](@entry_id:147726) $E(\mathbf{r})$ 却呈现出长周期的莫尔周期性（周期为 $L_m$）。这种[尺度分离](@entry_id:270204)的现象是如何产生的呢？[@problem_id:2796900] 其根源在于能量密度函数 $E(\mathbf{r})$ 是一个[复合函数](@entry_id:147347) $E(\mathbf{r}) = U(\boldsymbol{\Delta}(\mathbf{r}))$。如前所述，$U$ 是一个关于其宗量 $\boldsymbol{\Delta}$ 的短[周期函数](@entry_id:139337)，可以展开为傅里叶级数 $\sum U_{\mathbf{G}} \exp(i\mathbf{G}\cdot\boldsymbol{\Delta})$。而 $\boldsymbol{\Delta}(\mathbf{r})$ 是一个随空间位置 $\mathbf{r}$ 缓慢变化的场。将 $\boldsymbol{\Delta}(\mathbf{r}) \approx \mathbf{M}\mathbf{r}$ 代入，空间能量密度变为：

$E(\mathbf{r}) = \sum_{\mathbf{G}} U_{\mathbf{G}} \exp(i\mathbf{G}\cdot(\mathbf{M}\mathbf{r})) = \sum_{\mathbf{G}} U_{\mathbf{G}} \exp(i(\mathbf{M}^{\mathsf{T}}\mathbf{G})\cdot\mathbf{r})$

这表明，$E(\mathbf{r})$ 的空间傅里叶分量的[波矢](@entry_id:178620)不再是原始的 $\mathbf{G}$，而是新的、更小的波矢 $\mathbf{K} = \mathbf{M}^{\mathsf{T}}\mathbf{G}$。这些 $\mathbf{K}$ 正是莫尔超晶格的倒易格矢，其大小与 $\theta$ 和 $\delta$ 成正比，因此对应的[实空间](@entry_id:754128)周期非常长。这样，一个微观周期的[势能函数](@entry_id:200753)通过与一个缓慢变化的[位移场](@entry_id:141476)复合，便“生成”了宏观的莫尔能量景观。

这个莫尔[能量景观](@entry_id:147726)的存在意味着，一个理想的、未弛豫的扭转双层结构并非处于能量最低态。体系会通过层内**[弹性形变](@entry_id:161971)**来尽可能多地处于能量有利的堆叠区域（如AB/BA），从而降低总能量。这一过程被称为**结构重构**或**弛豫**。

描述这一过程的连续介质模型的总[能量泛函](@entry_id:170311) $E$ 由两部分组成：层内弹性应变能和层间堆叠能，对整个二维面积积分 [@problem_id:2796899]：

$E[\mathbf{u}^{(1)}, \mathbf{u}^{(2)}] = \int d^2 r \left\{ \sum_{\alpha=1}^{2} \frac{1}{2} C_{ijkl} \varepsilon_{ij}^{(\alpha)} \varepsilon_{kl}^{(\alpha)} + U[\boldsymbol{\Delta}(\mathbf{r})] \right\}$

- **弹性应变能**: 第一项是两层（$\alpha=1,2$）的弹性应变能密度之和。$C_{ijkl}$ 是[四阶弹性张量](@entry_id:188318)，$\mathbf{u}^{(\alpha)}(\mathbf{r})$ 是第 $\alpha$ 层的面内位移场。至关重要的是，应变张量 $\varepsilon_{ij}^{(\alpha)}$ 必须使用对称化的形式 $\varepsilon_{ij}^{(\alpha)} = \frac{1}{2}(\partial_i u_j^{(\alpha)} + \partial_j u_i^{(\alpha)})$，以确保能量在刚性转动下不变。
- **层间堆叠能**: 第二项是GSFE。这里的局域[位移场](@entry_id:141476) $\boldsymbol{\Delta}(\mathbf{r})$ 现在包含了[弹性形变](@entry_id:161971)的贡献：$\boldsymbol{\Delta}(\mathbf{r}) = \mathbf{b}(\mathbf{r}) + \mathbf{u}^{(1)}(\mathbf{r}) - \mathbf{u}^{(2)}(\mathbf{r})$，其中 $\mathbf{b}(\mathbf{r})$ 代表由扭转和[晶格失配](@entry_id:196802)引起的初始（未弛豫）位移场。

体系的平衡构型对应于总能量 $E$ 的最小值。通过对位移场 $\mathbf{u}^{(1)}$ 和 $\mathbf{u}^{(2)}$ 进行变分并令 $\delta E=0$，我们可以导出系统的[欧拉-拉格朗日方程](@entry_id:137827)，即力学平衡方程 [@problem_id:2796899]：

$-\partial_i \sigma^{(1)}_{ij} + \frac{\partial U}{\partial \Delta_j}=0$
$-\partial_i \sigma^{(2)}_{ij} - \frac{\partial U}{\partial \Delta_j}=0$

其中 $\sigma_{ij}^{(\alpha)} = C_{ijkl} \varepsilon_{kl}^{(\alpha)}$ 是第 $\alpha$ 层的柯西[应力张量](@entry_id:148973)。这些方程具有清晰的物理图像：每一层内部[应力的散度](@entry_id:185633)（$\partial_i \sigma_{ij}$，代表来自层内形变的恢复力密度）必须与层间相互作用力密度（$\pm \partial U / \partial \Delta_j$）相平衡。层间作用力在两层之间大小相等、方向相反，符合牛顿第三定律。

### 结构重构的机制与后果

求解上述[平衡方程](@entry_id:172166)揭示了莫尔[超晶格](@entry_id:200197)中丰富的结构重构现象。最引人注目的特征之一是在小扭转角下，体系自发地形成由能量有利的AB和BA堆叠构成的**大面积畴区**，这些畴区由被称为**[孤子](@entry_id:145656)（solitons）**或**畴壁（domain walls）**的狭窄边界隔开。

这种[畴壁](@entry_id:144723)网络的形成是弹性成本与堆叠能量收益之间竞争与平衡的结果。我们可以通过一个标度分析来理解为何在小扭转角 $\theta$ 下这种状态是能量有利的 [@problem_id:2796937]。
- 首先，考虑单个孤子的性质。[孤子](@entry_id:145656)的宽度 $w$ 和线能量（单位长度的能量）$\varepsilon_w$ 由局域的能量平衡决定。在宽度为 $w$ 的[孤子](@entry_id:145656)内部，[晶格](@entry_id:196752)需要适应约等于原子[晶格常数](@entry_id:158935) $a$ 的位移变化，因此产生应变 $\epsilon \sim a/w$。弹性成本密度为 $\sim G\epsilon^2 \sim G(a/w)^2$，其中 $G$ 是[有效弹性模量](@entry_id:181086)。孤子线能量的弹性部分为 $\sim G(a/w)^2 \cdot w = Ga^2/w$。另一方面，孤子区域是高能量的“不良”堆叠区，其堆叠能量成本的线能量为 $\sim \Delta\gamma \cdot w$，其中 $\Delta\gamma$ 是GSFE的起伏幅度。总线能量 $\varepsilon_w \sim Ga^2/w + \Delta\gamma \cdot w$ 在 $w \sim a\sqrt{G/\Delta\gamma}$ 时最小。此时，最小线能量为 $\varepsilon_w \sim a\sqrt{G\Delta\gamma}$。重要的是，[孤子](@entry_id:145656)宽度 $w$ 和线能量 $\varepsilon_w$ 都只依赖于材料的內禀属性（$G, \Delta\gamma, a$），而与莫尔周期 $L$ 或扭转角 $\theta$ 无关。
- 其次，考虑整个[孤子](@entry_id:145656)网络的能量。畴壁网络以莫尔周期 $L \sim a/\theta$ 遍布整个材料。单位面积内的畴壁总长度约为 $1/L$。因此，由[畴壁](@entry_id:144723)网络带来的总能量成本（单位面积）为 $E_{\text{wall}} \sim \varepsilon_w / L \propto \theta$。
- 最后，比较能量得失。形成畴区所获得的能量收益来自于将大部分区域从能量较高的非公度堆叠转变为能量最低的AB/BA堆叠。这个能量收益（单位面积）的大小正比于GSFE的幅度 $\Delta\gamma$，它是一个与 $\theta$ 无关的常数。

因此，总能量变化为 $\Delta E_{\text{total}} \approx \Delta\gamma - C \cdot \theta$（$C$为正常数）。当 $\theta$ 足够小时，与 $\theta$ 无关的能量收益项 $\Delta\gamma$ 必然会超过随 $\theta$ 线性减小的能量成本项 $E_{\text{wall}}$。这使得结构重构成为能量上有利的过程，并且由于 $w$ 是常数而 $L \propto 1/\theta$，在小角度下自然满足 $w \ll L$，即形成“宽畴区、窄畴壁”的图像。

结构重构并不仅限于面内位移，它也常常伴随着显著的**面外重构**，即**翘曲（corrugation）**。层间相互作用不仅依赖于横向位移 $\boldsymbol{\Delta}$，也依赖于层间距。能量有利的区域（如AB）倾向于吸引得更近，而能量不利的区域（如AA）则倾向于排斥得更远。这种效应导致二维材料发生面[外形](@entry_id:146590)变，形成与莫尔周期相匹配的高度起伏。翘曲的幅度由材料的**抗弯刚度 $D$** 和**层间粘附能反差 $\Delta U$** 之间的竞争决定 [@problem_id:2796922]。在一个简化的模型中，总能量可以写成弯曲弹性势能 $\frac{1}{2}D\langle(\nabla^2 h)^2\rangle$ 和层间粘附势能 $\frac{1}{2}K\langle(h-h_{\text{pref}})^2\rangle$ 之和，其中 $h(\mathbf{r})$ 是高度场，$h_{\text{pref}}(\mathbf{r})$ 是由粘附能驱动的理想高度场， $K$ 是等效的支撑刚度。通过能量最小化，可以得到[平衡态](@entry_id:168134)的翘曲幅度。例如，对于莫尔周期 $L_m = 14.0\,\mathrm{nm}$、抗弯刚度 $D = 2.4\times 10^{-19}\,\mathrm{J}$、支撑刚度 $K = 1.0\times 10^{19}\,\mathrm{J\,m^{-4}}$ 和粘附能反差 $\Delta U = 5.0\times 10^{-4}\,\mathrm{J\,m^{-2}}$ 的系统，计算出的峰谷高度差（AA与AB区域的高度差）约为 $0.0200\,\mathrm{nm}$ [@problem_id:2796922]，这在实验中是完全可以观测到的。

最后，值得注意的是，莫尔超晶格的结构重构景观是**可调控的**。改变外部环境可以有效改变层间相互作用，从而调控弛豫的程度。一个典型的例子是在[异质结](@entry_id:196407)的层间插入溶剂分子 [@problem_id:2796908]。
- 溶剂层作为一种介电媒质，会**屏蔽**层间的[范德华相互作用](@entry_id:168429)。这种相互作用主要由倏逝[电磁场](@entry_id:265881)介导，其强度随距离指数衰减。因此，厚度为 $t$、[介电常数](@entry_id:146714)为 $\epsilon$ 的溶剂层会使GSFE的振幅 $\Delta U$ 大致按 $\Delta U(\epsilon,t) \propto \epsilon^{-1} \exp(-Gt)$ 的规律减小，其中 $G$ 是莫尔倒易格矢的大小。
- 根据我们之前的分析，[孤子](@entry_id:145656)宽度 $w \propto 1/\sqrt{\Delta U}$。因此，当 $\Delta U$ 减小时，[孤子](@entry_id:145656)宽度 $w$ 会增加，即 $w \propto \epsilon^{1/2} \exp(Gt/2)$。这意味着更强的[介电屏蔽](@entry_id:266074)或更厚的溶剂层会削弱结构重构的驱动力，导致[畴壁](@entry_id:144723)变宽，畴区边界变得模糊。

这一机制的理解不仅加深了我们对莫尔物理的认识，也为通过[环境工程](@entry_id:183863)（如电化学门控、溶剂插层等）来动态调控[二维材料](@entry_id:142244)的力学、电学和光学性质开辟了新的途径。