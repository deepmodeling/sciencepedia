## 引言
自P. W. Anderson首次提出以来，[共振价键](@entry_id:145823)（Resonating Valence Bond, RVB）态的概念已成为凝聚态物理学，特别是强[关联电子系统](@entry_id:144460)研究中的一块基石。它提供了一种超越传统朗道对称性破缺理论的全新[范式](@entry_id:161181)，用以理解那些即使在绝对零度下也拒绝任何经典有序的奇异物质相。然而，这些高度纠缠的[量子态](@entry_id:146142)的内在机理，以及它们如何与[高温超导](@entry_id:143123)等重大物理问题联系起来，构成了该领域的一个核心知识挑战。本文旨在系统性地剖析[RVB理论](@entry_id:144395)，带领读者从基本原理走向前沿应用。

在接下来的内容中，我们将分三步深入探索RVB的世界。首先，在“原理与机制”一章中，我们将奠定理论基础，从[RVB态](@entry_id:144977)的定义出发，辨析其与[价键固体](@entry_id:138121)的区别，并引入[部分子构造](@entry_id:143905)、演生[规范场](@entry_id:159627)等强大的形式化工具，揭示其[拓扑序](@entry_id:147345)和分数化激发等深刻物理内涵。随后，在“应用与跨学科联系”一章中，我们将展示RVB思想的强大生命力，探讨其如何作为[量子自旋液体](@entry_id:136269)理论的核心，并被应用于解释[铜氧化物](@entry_id:142665)[高温超导](@entry_id:143123)的复杂机理，同时揭示其与[量子信息](@entry_id:137721)、[统计力](@entry_id:194984)学等领域的深刻联系。最后，在“动手实践”部分，我们提供了一系列精心设计的计算练习，旨在通过亲手计算将抽象的理论概念转化为具体的物理直觉，巩固读者对[RVB态](@entry_id:144977)的理解。

## 原理与机制

本章旨在深入探讨[共振价键](@entry_id:145823)（Resonating Valence Bond, RVB）态的内在原理与物理机制。我们将从其基本定义出发，阐明其作为量子自spin液体候选态的物理动机，然后引入描述和分类这些奇异[物态](@entry_id:139436)的强大理论框架，最终揭示其最引人入胜的特性——拓扑序和分数化激发。

### [共振价键态](@entry_id:144977)的定义与辨析

一个[RVB态](@entry_id:144977)的核心思想是，系统的[基态](@entry_id:150928)并非由某种静态的、破缺对称性的序所描述，而是由大量简并或[近简并](@entry_id:172107)的**自旋单态（spin-singlet）**组态的宏观[量子叠加](@entry_id:137914)而成。在自旋-$\frac{1}{2}$系统中，最基本的构筑单元是连接两个格点的**价键（valence bond）**，即一个自旋单态对：
$$
\ket{s_{ij}} = \frac{1}{\sqrt{2}} \left( \ket{\uparrow_i \downarrow_j} - \ket{\downarrow_i \uparrow_j} \right)
$$
其中，$\ket{\uparrow_i \downarrow_j}$表示$i$格点上的自旋向上，$j$格点上的自旋向下。一个**价键覆盖（valence bond covering）** $\mathcal{C}$ 是将[晶格](@entry_id:196752)上所有$N$个自旋两两配对成不相交的单态价键的一种方式，其对应的[量子态](@entry_id:146142)为 $\ket{\mathcal{C}} = \prod_{(i,j) \in \mathcal{C}} \ket{s_{ij}}$。

一个**RVB[自旋液体](@entry_id:147892)（RVB spin liquid）**的[波函数](@entry_id:147440)正是这些不同价键覆盖的线性叠加 [@problem_id:3013846]：
$$
\ket{\mathrm{RVB}} = \sum_{\mathcal{C}} A_{\mathcal{C}} \ket{\mathcal{C}}
$$
其中，$A_{\mathcal{C}}$是复数振幅。[RVB态](@entry_id:144977)的关键特征在于，这些振幅$A_{\mathcal{C}}$的选取方式必须使得整个[波函数](@entry_id:147440)$\ket{\mathrm{RVB}}$保持[哈密顿量](@entry_id:172864)的所有对称性，包括[晶格](@entry_id:196752)的平移、旋转和反演对称性。这意味着，在一个理想的RVB液体中，价键是动态“共振”的，没有任何一个特定的覆盖模式被优先选择。

这种保持对称性的特性是[RVB态](@entry_id:144977)与另一种相关的物态——**[价键固体](@entry_id:138121)（Valence Bond Solid, [VBS](@entry_id:138121)）**的根本区别。在一个[VBS](@entry_id:138121)态中，波[函数的振幅](@entry_id:160674)$|A_{\mathcal{C}}|^2$会集中在某一个或少数几个通过对称性操作相互关联的价键覆盖模式上。这导致系统自发地选择一个静态的、晶体化的价键[排列](@entry_id:136432)方式，从而破缺了[晶格](@entry_id:196752)的某些对称性（如平移或[旋转对称](@entry_id:137077)性）。

这种对称性上的差异直接体现在物理可观测量上。首先，由于RVB和[VBS](@entry_id:138121)态都是由自旋单态构成的，它们都保持了全局自旋旋转对称性（$SU(2)$对称性），因此任何局域的自旋[期望值](@entry_id:153208)都为零，即 $\langle \mathbf{S}_i \rangle = \mathbf{0}$。然而，它们的二聚子（dimer）关联行为则截然不同。定义二聚子算符 $B_{ij} = \frac{1}{4} - \mathbf{S}_i \cdot \mathbf{S}_j$，它能够投影出键$(i,j)$上的单态分量。在[VBS](@entry_id:138121)相中，由于存在长程的价键序，二聚子-二聚子关联函数 $C_{BB}(\mathbf{r}) = \langle B_{0}B_{\mathbf{r}} \rangle - \langle B_0 \rangle \langle B_{\mathbf{r}} \rangle$ 在$|\mathbf{r}| \to \infty$时会趋于一个非零常数。这在倒空间中表现为，其对应的[结构因子](@entry_id:158623) $D(\mathbf{q})$ 会在与破缺对称性相关的布拉格波矢处出现尖锐的**布拉格峰（Bragg peaks）**。相反，在一个（短程）RVB液体中，由于不存在任何长程序，所有局域关联函数都会在长距离下衰减至零，因此$D(\mathbf{q})$是一个光滑的函数，没有任何布拉格峰 [@problem_id:3013846]。

值得注意的是，构成[RVB态](@entry_id:144977)的价键覆盖[基矢](@entry_id:199546) $\ket{\mathcal{C}}$ 并[非正交基](@entry_id:154908)。例如，在一个四格点的环上，两种不同的近邻价键覆盖$\ket{\mathcal{C}_1} = \ket{s_{12}}\ket{s_{34}}$和$\ket{\mathcal{C}_2} = \ket{s_{23}}\ket{s_{41}}$的交叠是$\langle \mathcal{C}_1 | \mathcal{C}_2 \rangle = 1/2 \neq 0$。这个[非正交性](@entry_id:192553)是[RVB理论](@entry_id:144395)的一个基本且重要的技术特点，它使得[波函数](@entry_id:147440)的归一化和各种[期望值](@entry_id:153208)的计算变得非常复杂 [@problem_id:3013846]。

### 物理动机：阻挫与[共振能量](@entry_id:147349)增益

为何[RVB态](@entry_id:144977)会成为某些[量子磁性](@entry_id:145792)系统（特别是阻挫反铁磁体）的有力[基态](@entry_id:150928)候选者？答案在于量子力学中的一个基本原理：当系统存在多个[近简并](@entry_id:172107)的态时，它们之间的混合（或共振）可以显著地降低系统能量。

考虑一个存在**[几何阻挫](@entry_id:145579)（frustration）**的系统，例如方格子上同时存在近邻$J_1 > 0$和次近邻$J_2 > 0$反铁磁相互作用的$J_1-J_2$[海森堡模型](@entry_id:139958)。当$J_2$足够大时（例如 $J_2/J_1 \sim 0.5$），它会与$J_1$所偏好的简单棋盘状奈尔（Néel）反铁磁序相竞争。这种竞争使得单一的经典自旋构型不再是能量最优的，而是导致了大量不同的短程自旋单态构型（即价键覆盖）成为能量相近的候选态。阻挫为价键的“共振”创造了理想的舞台 [@problem_id:3013898]。

反铁磁交换相互作用本身提供了驱动这种共振的机制。考虑一个四格点方块上的两个价键覆盖态，$\ket{h} = \ket{s_{12}}\ket{s_{34}}$ 和 $\ket{v} = \ket{s_{23}}\ket{s_{41}}$。[海森堡哈密顿量](@entry_id:146333) $H = J \sum_{\langle i j \rangle} \mathbf{S}_i \cdot \mathbf{S}_j$ 作用在其中一个态上，例如$\ket{h}$，可以将其转变为另一个态$\ket{v}$。这是因为像$\mathbf{S}_2 \cdot \mathbf{S}_3$这样的交换项可以“打断”$(1,2)$和$(3,4)$上的单态，并重新组合成$(2,3)$和$(1,4)$上的单态。这意味着[哈密顿量](@entry_id:172864)在$\ket{h}$和$\ket{v}$这两个[基矢](@entry_id:199546)之间存在非对角的[矩阵元](@entry_id:186505) $\langle h | H | v \rangle \neq 0$。

根据量子力学的[微扰理论](@entry_id:138766)或变分原理，这种非[对角矩阵](@entry_id:637782)元的存在会导致[能级排斥](@entry_id:137654)。通过形成一个对称的叠加态，例如 $\ket{\psi} \propto (\ket{h} + \ket{v})$，系统的变分能量可以被降低。这个能量的降低量被称为**共振能（resonance energy）**。正是这种通过量子涨落获得的能量增益，使得[RVB态](@entry_id:144977)在能量上有可能胜过经典的有序态。同时，这种价键的持续动态涨落天然地破坏了任何静态长程[磁序](@entry_id:161845)的形成，从而导致了一个没有磁矩的量子无序[基态](@entry_id:150928)——即[量子自旋液体](@entry_id:136269) [@problem_id:3013898]。

### 形式化方法：[部分子构造](@entry_id:143905)与平均场理论

为了对[RVB态](@entry_id:144977)进行更系统和定量的研究，P. W. Anderson引入了**[部分子](@entry_id:160627)（parton）**或**奴隶粒子（slave-particle）**的方法。其思想是将基本[自旋算符](@entry_id:155419)分解为更基本的“[部分子](@entry_id:160627)”算符。在费米型部分子表述（也称Abrikosov[费米子](@entry_id:146235)）中，自旋-$\frac{1}{2}$算符被写作一对[费米子算符](@entry_id:149120)的二次型：
$$
\mathbf{S}_{i} = \frac{1}{2} \sum_{\alpha, \beta} f_{i\alpha}^{\dagger} \boldsymbol{\sigma}_{\alpha\beta} f_{i\beta}
$$
其中，$f_{i\sigma}^{\dagger}$ 和 $f_{i\sigma}$ 是在格点$i$上产生和湮灭自旋为$\sigma$的费米型[部分子](@entry_id:160627)（称为**[自旋子](@entry_id:140415)(spinon)**）的算符，$\boldsymbol{\sigma}$是[泡利矩阵](@entry_id:139493)。

这种表示方法极大地扩展了[希尔伯特空间](@entry_id:261193)。原本每个格点只有两个状态（$\uparrow$ 或 $\downarrow$），现在却有四个状态：真空$\ket{0}_i$、单占据$\ket{\uparrow}_i$、$\ket{\downarrow}_i$和双占据$\ket{\uparrow\downarrow}_i$。为了确保我们描述的是物理的自旋系统，必须施加一个严格的**单占据约束（single-occupancy constraint）**在每个格点上：
$$
\sum_{\sigma} f_{i\sigma}^{\dagger} f_{i\sigma} = 1
$$
这个约束意味着每个格点上必须且只能有一个自旋子。

在部分子表述下，海森堡相互作用 $\mathbf{S}_i \cdot \mathbf{S}_j$ 变成了一个关于$f$算符的四次项。我们可以采用**平均场近似（mean-field approximation）**，通过Hubbard-Stratonovich变换将其[解耦](@entry_id:637294)成一个自旋子的二次型[哈密顿量](@entry_id:172864)。这通常会引入两个平均场参数：描述自旋子在格点间跃迁的**跃迁振幅** $\chi_{ij} = \langle \sum_{\sigma} f_{i\sigma}^\dagger f_{j\sigma} \rangle$，以及描述自旋子配对的**配对振幅** $\Delta_{ij} = \langle f_{i\uparrow}f_{j\downarrow} - f_{i\downarrow}f_{j\uparrow} \rangle$。这样得到的[平均场哈密顿量](@entry_id:751814)描述了在一个由$\chi_{ij}$和$\Delta_{ij}$决定的背景“[能带结构](@entry_id:139379)”中运动和配对的“自由”自旋子。

然而，平均场理论的[基态](@entry_id:150928)（一个BCS类型的[波函数](@entry_id:147440) $\ket{\mathrm{BCS}}$）本身并不满足单占据约束，因为它包含了真空和双占据的组态。为了获得一个物理上有意义的[自旋波函数](@entry_id:190161)，我们必须将$\ket{\mathrm{BCS}}$投影回物理的、单占据的[希尔伯特空间](@entry_id:261193)。这个操作通过**[Gutzwiller投影](@entry_id:141781)算符（Gutzwiller projector）** $\mathcal{P}_G$ 来实现 [@problem_id:3013863]：
$$
\ket{\Psi_{\mathrm{RVB}}} = \mathcal{P}_G \ket{\mathrm{BCS}}, \quad \text{with} \quad \mathcal{P}_G = \prod_i (1 - n_{i\uparrow}n_{i\downarrow})
$$
其中 $n_{i\sigma} = f_{i\sigma}^\dagger f_{i\sigma}$ 是[粒子数算符](@entry_id:153568)。算符 $(1 - n_{i\uparrow}n_{i\downarrow})$ 的作用是：当格点$i$上没有双占据时（$n_{i\uparrow}n_{i\downarrow}=0$），它等于单位算符；当存在双占据时（$n_{i\uparrow}n_{i\downarrow}=1$），它等于零，从而将该组态从[波函数](@entry_id:147440)中“投影”掉。这个[投影算符](@entry_id:154142)是厄米的（$\mathcal{P}_G^\dagger = \mathcal{P}_G$）和幂等的（$\mathcal{P}_G^2 = \mathcal{P}_G$），但它不是幺正的，因此投影操作会改变波[函数的范数](@entry_id:275551)。[Gutzwiller投影](@entry_id:141781)可以被看作是在[哈密顿量](@entry_id:172864)中引入无穷大在位排斥$U \to \infty$的严格实现，因为 $\mathcal{P}_G$ 等价于算符 $\exp(-g \sum_i n_{i\uparrow}n_{i\downarrow})$ 在 $g \to \infty$ 时的极限 [@problem_id:3013863]。

### 演生规范结构与物态分类

[部分子](@entry_id:160627)分解和单占据约束的引入，不仅为构造[变分波函数](@entry_id:144043)提供了便利，更揭示了[RVB态](@entry_id:144977)深层次的结构——**演生规范场（emergent gauge field）**。

部分子表示 $\mathbf{S}_{i} = \frac{1}{2} f_{i\alpha}^{\dagger} \boldsymbol{\sigma}_{\alpha\beta} f_{i\beta}$ 具有一个局域的 $U(1)$ **规范冗余性（gauge redundancy）**，即在变换 $f_{i\sigma} \to e^{i\theta_i} f_{i\sigma}$ 下，物理的[自旋算符](@entry_id:155419) $\mathbf{S}_i$ 保持不变。在[路径积分表述](@entry_id:145051)中，为了强制实施单占据约束 $\sum_{\sigma} f_{i\sigma}^{\dagger} f_{i\sigma} = 1$，我们需要引入一个随时间和空间变化的拉格朗日乘子场 $a_0(i, \tau)$。这个场的作用如同一个[电势](@entry_id:267554)，与自旋子密度耦合。类似地，平均场[解耦](@entry_id:637294)时引入的跃迁和配对振幅 $\chi_{ij}$ 和 $\Delta_{ij}$ 都是复数，它们的相位同样具有[规范自由度](@entry_id:160491)。这些相位涨落可以被看作是连接格点的演生矢量势 $a_{ij}(\tau)$。综合来看，这些自由度构成了一个完整的、动力学的 $U(1)$ 演生[规范场](@entry_id:159627) $a_{\mu} = (a_0, \mathbf{a})$，它与作为“物质场”的[自旋子](@entry_id:140415)发生[最小耦合](@entry_id:148226) [@problem_id:3013820]。在低能长波极限下，该系统的[有效作用量](@entry_id:145780)可以写成一个规范场与[狄拉克费米子](@entry_id:161484)（代表低能[自旋子](@entry_id:140415)）耦合的形式，并需要通过Villain形式等方法来正确处理[规范场](@entry_id:159627)的紧致性 [@problem_id:3013820]。

这种演生规范结构的存在意味着，即便两个[RVB态](@entry_id:144977)具有完全相同的物理对称性（如[晶格](@entry_id:196752)对称性），它们仍然可能是完全不同的物理相。对这些物态进行分类的强大工具是**投影[对称群](@entry_id:146083)（Projective Symmetry Group, PSG）**理论 [@problem_id:3013878]。PSG的核心思想是研究物理[对称操作](@entry_id:143398)（如平移$T_x$）如何在部分子的希尔伯特空间中被“实现”。一个物理[对称操作](@entry_id:143398) $g$ 作用在[平均场哈密顿量](@entry_id:751814)上，其效果必须等价于一个[规范变换](@entry_id:176521) $G_g$。因此，PSG的元素是成对的 $(g, G_g)$。这些对的组合必须满足与物理[对称群](@entry_id:146083) $\mathcal{G}$ 一致的[群代数](@entry_id:145139)关系，但这种满足关系是“投影”的，即只要求在模掉一个**不变[规范群](@entry_id:144761)（Invariant Gauge Group, IGG）**元素的意义下成立。例如，$(g_1, G_{g_1})$和$(g_2, G_{g_2})$的复合会产生一个因子 $\eta(g_1, g_2)$，它属于IGG。这些因子系的非等价选择（不能通过规范变换消除）就对应着不同的PSG，从而分类了不同的[自旋液体](@entry_id:147892)相 [@problem_id:3013878]。

作为一个具体的例子，方格子上的一种常见RVB平均场ansatz具有 $d_{x^2-y^2}$ 对称性的配对振幅（$\Delta_{i,i+\hat{x}}=\Delta, \Delta_{i,i+\hat{y}}=-\Delta$）。通过将[平均场哈密顿量](@entry_id:751814)作[傅里叶变换](@entry_id:142120)并在Nambu空间中对角化，可以得到自旋子的[准粒子色散](@entry_id:161746)关系 [@problem_id:3013882]：
$$
E_{\mathbf{k}} = \sqrt{\left( \lambda - \frac{3J\chi}{4}(\cos(k_x) + \cos(k_y)) \right)^2 + \left( \frac{3J\Delta}{4}(\cos(k_x) - \cos(k_y)) \right)^2}
$$
其中 $\chi$ 和 $\Delta$ 是平均场参数，$\lambda$ 是化学势。这个[色散关系](@entry_id:140395)在布里渊区的某些点（[狄拉克点](@entry_id:276156)）上可以为零，形成[无能](@entry_id:201612)隙的激发。这种态被称为 $U(1)$ 狄拉克[自旋液体](@entry_id:147892)，是[RVB理论](@entry_id:144395)中一类重要的无能隙[自旋液体](@entry_id:147892)。

### 有[能隙](@entry_id:191975)[RVB态](@entry_id:144977)的[拓扑序](@entry_id:147345)：$Z_2$[自旋液体](@entry_id:147892)

除了无能隙的 $U(1)$ [自旋液体](@entry_id:147892)，[RVB理论](@entry_id:144395)同样可以描述具有**[拓扑序](@entry_id:147345)（topological order）**的有[能隙](@entry_id:191975)[自旋液体](@entry_id:147892)。其中最著名和最简单的例子是 **$Z_2$[自旋液体](@entry_id:147892)**。

从 $U(1)$ [规范理论](@entry_id:142992)出发，一个 $Z_2$ [自旋液体](@entry_id:147892)可以通过**[希格斯机制](@entry_id:144416)（Higgs mechanism）**产生。如果自旋子发生配对并形成一个具有非零[期望值](@entry_id:153208)的凝聚体，即 $\langle \Delta_{ij} \rangle \neq 0$，那么这个凝聚场就会“希格斯”掉原来的 $U(1)$ [规范场](@entry_id:159627)。由于配对算符 $\Delta_{ij}$ 是由两个[费米子](@entry_id:146235)构成的，它在 $U(1)$ [规范变换](@entry_id:176521)下携带的[电荷](@entry_id:275494)为 $q=2$。一个[电荷](@entry_id:275494)为2的标量场的凝聚，并不能完全破缺 $U(1)$ 对称性，而是会留下一个离散的 $\mathbb{Z}_2$ [子群](@entry_id:146164)。这是因为变换 $\theta = \pi$ 满足 $e^{i2\theta}=1$，从而使凝聚体保持不变 [@problem_id:3013902]。因此，低能下的[有效理论](@entry_id:155490)从一个 $U(1)$ 规范理论变成了一个 $\mathbb{Z}_2$ 规范理论，系统进入了一个有[能隙](@entry_id:191975)的拓扑相。

$Z_2$[自旋液体](@entry_id:147892)具有独特的[元激发](@entry_id:140859)。除了被希格斯机制赋予了[能隙](@entry_id:191975)的自旋子（现在携带 $\mathbb{Z}_2$ 规范荷）外，还存在一种称为**维[相子](@entry_id:145875)（vison）**的[拓扑激发](@entry_id:157702)。维[相子](@entry_id:145875)是[希格斯场](@entry_id:160081)的涡旋，它携带了 $\mathbb{Z}_2$ 规范理论中的[磁通量](@entry_id:268943)。一个基本维[相子](@entry_id:145875)所携带的磁通量恰好为 $\pi$ [@problem_id:3013902]。由于在涡旋核心处，凝聚场必须为零，这会带来[凝聚能](@entry_id:195476)的损失，因此维[相子](@entry_id:145875)也是有[能隙](@entry_id:191975)的激发。

$Z_2$[自旋液体](@entry_id:147892)的拓扑性质体现在其激发之间的奇异**[编织统计](@entry_id:147187)（braiding statistics）**上。当一个自旋子绕一个维[相子](@entry_id:145875)绝热地运动一圈时，它的[波函数](@entry_id:147440)会拾取一个阿哈罗诺夫-玻姆（Aharonov-Bohm）相位。这个相位等于自旋子的[电荷](@entry_id:275494)（$q=1$）乘以维[相子](@entry_id:145875)的磁通量（$\Phi=\pi$），即 $\gamma = 1 \times \pi = \pi$。这对应于一个 $(-1)$ 的相位因子 [@problem_id:3013832]。计算一个[自旋子](@entry_id:140415)环绕维[相子](@entry_id:145875)的[威尔逊圈](@entry_id:146516)（Wilson loop）的值，会直接得到 $W(C) = \exp(i\pi) = -1$ [@problem_id:3013902]。这意味着[自旋子](@entry_id:140415)和维[相子](@entry_id:145875)之间存在**半[任意子](@entry_id:143753)（semionic）**的互易统计关系：它们不是[玻色子](@entry_id:138266)也不是[费米子](@entry_id:146235)，交换两者会导致[波函数](@entry_id:147440)改变符号。

在[环面几何](@entry_id:636287)上，这种拓扑性质有一个非常直观的图像。环面上的所有二聚[子覆盖](@entry_id:151408)可以根据其穿过某个非平庸圈（例如沿x方向）的二聚子数目的奇偶性 $p \in \{0, 1\}$，被划分为不同的**拓扑扇区（topological sectors）**。一个维[相子](@entry_id:145875)算符可以被定义为在该圈上插入一个$\pi$[磁通](@entry_id:191239)，其作用是对穿过该圈的每个二聚子赋予一个 $(-1)$ 的符号。当这个算符作用在一个特定拓扑扇区 $p$ 的[RVB态](@entry_id:144977) $\ket{\Psi_p}$ 上时，由于该扇区中所有组态穿过该圈的二聚子数目的奇偶性都是 $p$，因此整个[波函数](@entry_id:147440)会获得一个统一的相位因子 $(-1)^p$ [@problem_id:3013901]。这表明这些[RVB态](@entry_id:144977)是维[相子](@entry_id:145875)圈算符的本征态，[本征值](@entry_id:154894)直接反映了其拓扑扇区。

最后，一个二维[拓扑序](@entry_id:147345)最明确的定量标志是**[拓扑纠缠熵](@entry_id:145064)（Topological Entanglement Entropy, TEE）**，记为 $\gamma$。一个二维有[能隙](@entry_id:191975)系统的[纠缠熵](@entry_id:140818) $S(X)$ 满足所谓的“[面积定律](@entry_id:145931)”，$S(X) = \alpha |\partial X| - \gamma + \dots$，其中第一项与边界长度 $|\partial X|$ 成正比，而 $\gamma$ 是一个不依赖于区域形状和大小的[普适常数](@entry_id:165600)。通过Kitaev-Preskill或Levin-Wen提出的特定区域组合减法，可以精确地分离出这个普适项：$\gamma = -[S(A)+S(B)+S(C)-S(AB)-S(BC)-S(CA)+S(ABC)]$ [@problem_id:3013821]。理论指出，$\gamma = \ln \mathcal{D}$，其中 $\mathcal{D}$ 是该拓扑相中所有任意子[准粒子](@entry_id:136584)的**总[量子维度](@entry_id:146936)（total quantum dimension）**，定义为 $\mathcal{D} = \sqrt{\sum_a d_a^2}$ ($d_a$是[任意子](@entry_id:143753)$a$的[量子维度](@entry_id:146936))。对于$Z_2$[自旋液体](@entry_id:147892)，存在四种类型的[任意子](@entry_id:143753)（真空$1$、[自旋子](@entry_id:140415)$e$、维[相子](@entry_id:145875)$m$和它们的复合物$\epsilon$），它们的[量子维度](@entry_id:146936)都是1。因此，总[量子维度](@entry_id:146936)为 $\mathcal{D} = \sqrt{1^2+1^2+1^2+1^2} = 2$。这给出了$Z_2$[拓扑序](@entry_id:147345)的一个标志性结果：
$$
\gamma = \ln(2)
$$
这个非零的[拓扑纠缠熵](@entry_id:145064)是$Z_2$ [RVB态](@entry_id:144977)长程[量子纠缠](@entry_id:136576)的直接证据，也是其作为一种拓扑[物态](@entry_id:139436)的决定性特征 [@problem_id:3013821]。