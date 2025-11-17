## 引言
巴丁-库珀-施里弗（Bardeen-Cooper-Schrieffer, BCS）理论是[凝聚态物理学](@entry_id:140205)的一座丰碑，它首次从微观层面成功解释了常规超[导电性](@entry_id:137481)这一[宏观量子现象](@entry_id:144018)。其核心在于揭示了电子如何在[晶格](@entry_id:196752)媒介下配对形成库珀对，并进而凝聚成一个具有[能隙](@entry_id:191975)的全新[基态](@entry_id:150928)。超导能隙的存在不仅是理论的直接推论，更是理解[超导体](@entry_id:191025)几乎所有独特性质——从零电阻到[迈斯纳效应](@entry_id:273600)——的关键。然而，从抽象的理论构建到与纷繁复杂的实验现象建立联系，需要一个系统性的知识桥梁。本文旨在填补这一鸿沟，为读者提供一个关于BCS理论及其核心概念——[超导能隙](@entry_id:145058)——的全面而深入的图景。

在接下来的内容中，我们将踏上一段从基础到前沿的探索之旅。第一章**“原理与机制”**将从根源出发，详细阐述[电子-声子相互作用](@entry_id:140708)如何产生吸[引力](@entry_id:175476)，[库珀不稳定性](@entry_id:145007)如何引发配对，并最终构建[BCS基态](@entry_id:136275)与[能隙](@entry_id:191975)的完整理论图像，同时也会触及超越[弱耦合](@entry_id:140994)近似的[Eliashberg理论](@entry_id:144676)。第二章**“应用与交叉学科联系”**将视野转向真实世界，展示超导能隙如何在宏观输运、[热力学性质](@entry_id:146047)以及各类先进谱学（如隧穿谱、ARPES、NMR）中被精确探测，并探讨BCS思想在量子器件、[纳米结构](@entry_id:148157)乃至非常规超导研究中的广泛应用和扩展。最后，第三章**“动手实践”**提供了一系列精心设计的计算练习，旨在通过实践加深对[能隙](@entry_id:191975)、相干长度等核心概念的理解。通过这一结构化的学习路径，读者将能够系统地掌握BCS理论的精髓，并具备将其应用于解决前沿物理问题的能力。

## 原理与机制

本章旨在深入阐述传统超[导电性](@entry_id:137481)的基本原理与核心机制。我们将从导致电子配对的吸[引力](@entry_id:175476)根源出发，逐步构建巴丁-库珀-施里弗（Bardeen-Cooper-Schrieffer, BCS）理论的完整框架。内容将涵盖[库珀不稳定性](@entry_id:145007)、[BCS基态](@entry_id:136275)的形成、[超导能隙](@entry_id:145058)的出现、[准粒子激发](@entry_id:138475)谱的特性，以及[超导相变](@entry_id:141757)的[热力学特征](@entry_id:185212)。此外，我们还将探讨杂质对超[导电性](@entry_id:137481)的影响，并最终介绍超越BCS理论的强耦合 Eliashberg 理论，以提供一个更为全面和精确的物理图像。

### 吸[引力](@entry_id:175476)的来源：[电子-声子相互作用](@entry_id:140708)

在真空中，两个电子因带有同种[电荷](@entry_id:275494)而相互排斥。然而，在固体金属中，电子并非存在于真空中，而是运动于一个由带正电的离子实构成的可形变[晶格](@entry_id:196752)背景中。这种[晶格](@entry_id:196752)的动力学行为从根本上改变了电子间的有效相互作用。

一个运动的电子会通过库仑力吸引其周围的正离子，导致[晶格](@entry_id:196752)发生局部畸变，形成一个短暂的、局域化的正[电荷密度](@entry_id:144672)增强区域。这个正[电荷](@entry_id:275494)区域可以吸引第二个电子。如果第二个电子在[晶格](@entry_id:196752)弛豫回平衡位置之前经过该区域，它将感受到一个有效的吸[引力](@entry_id:175476)。这个过程可以被形象地理解为：第一个电子“犁开”[晶格](@entry_id:196752)，留下一道“沟”，第二个电子则被这道“沟”所吸引。

这种相互作用的核心在于**[延迟效应](@entry_id:199612) (retardation effect)**。[晶格](@entry_id:196752)的响应速度远慢于电子的运动速度。当第一个电子离开后，它所引起的[晶格](@entry_id:196752)畸变（即正[电荷](@entry_id:275494)富集）会持续一小段时间。正是在这段时间内，第二个电子感受到了由第一个电子“遗留”下来的吸引作用。

在量子力学框架下，[晶格](@entry_id:196752)的[振动](@entry_id:267781)被量子化为**[声子](@entry_id:140728) (phonons)**。电子与[晶格](@entry_id:196752)的相互作用表现为[电子发射](@entry_id:143393)或吸收一个虚[声子](@entry_id:140728)。一个[电子发射](@entry_id:143393)虚[声子](@entry_id:140728)，另一个电子吸收该虚[声子](@entry_id:140728)，从而实现两者之间的动量和能量交换。这种通过交换虚[声子](@entry_id:140728)介导的有效[电子-电子相互作用](@entry_id:139900)可以通过[二阶微扰理论](@entry_id:192858)进行计算。对于交换动量为 $\mathbf{q}$、能量为 $\omega$ 的过程，其有效相互作用势 $V_{\text{eff}}(\mathbf{q},\omega)$ 可以表示为 [@problem_id:2802524]：

$$
V_{\text{eff}}^{R}(\mathbf{q},\omega) = |g_{\mathbf{q}}|^{2}\ D^{R}(\mathbf{q},\omega) = |g_{\mathbf{q}}|^{2}\ \frac{2\omega_{\mathbf{q}}}{(\omega + i0^{+})^{2} - \omega_{\mathbf{q}}^{2}}
$$

这里，$g_{\mathbf{q}}$ 是[电子-声子相互作用](@entry_id:140708)矩阵元，$\omega_{\mathbf{q}}$ 是动量为 $\mathbf{q}$ 的[声子](@entry_id:140728)的频率，$D^{R}(\mathbf{q},\omega)$ 是延迟[声子](@entry_id:140728)[传播子](@entry_id:139558)。该势的实部决定了相互作用是吸引还是排斥：

$$
\text{Re}\left[V_{\text{eff}}^{R}(\mathbf{q},\omega)\right] = |g_{\mathbf{q}}|^2 \frac{2\omega_{\mathbf{q}}}{\omega^2 - \omega_{\mathbf{q}}^2}
$$

一个吸引相互作用对应于 $\text{Re}[V_{\text{eff}}^{R}]  0$。由于 $|g_{\mathbf{q}}|^2$ 和 $\omega_{\mathbf{q}}$ 均为正，吸引条件等价于分母为负，即 $\omega^2 - \omega_{\mathbf{q}}^2  0$。这导出了一个至关重要的结论：

$$
|\omega|  \omega_{\mathbf{q}}
$$

这意味着，只有当两个电子之间交换的能量（频率）$|\omega|$ 小于所交换[声子](@entry_id:140728)的能量 $\omega_{\mathbf{q}}$ 时，这种由[声子](@entry_id:140728)介导的相互作用才是吸引的。对于高能量交换过程 ($|\omega| > \omega_{\mathbf{q}}$)，相互作用是排斥的。这种[延迟效应](@entry_id:199612)使得瞬时排斥的[库仑力](@entry_id:174598)在特定能量尺度下，可以被[晶格](@entry_id:196752)的“过筛选”效应所克服，从而产生净吸[引力](@entry_id:175476)。正是这种[声子](@entry_id:140728)介导的吸[引力](@entry_id:175476)，为电子配对和超[导电性](@entry_id:137481)的形成奠定了基础。

### [库珀不稳定性](@entry_id:145007)：[费米海](@entry_id:136725)中的配对

在三维真空中，一个任意弱的短程吸引势不足以束缚两个粒子形成稳定的束缚态。然而，在金属的[费米海](@entry_id:136725)（Fermi sea）背景下，情况发生了戏剧性的变化。这一深刻的见解源于 Leon Cooper 在1956年提出的**[库珀问题](@entry_id:161364) (Cooper problem)** [@problem_id:2802588]。

库珀考虑的是在零温下，在一个被电子完全填充至[费米能](@entry_id:143977) $\epsilon_{\mathrm{F}}$ 的费米海之上，加入两个额外的电子。假设这两个电子之间存在一个微弱的吸引相互作用 $-|V|$，且该作用仅当两个电子的能量都处于费米面上方一个很薄的能量壳层 $[\epsilon_{\mathrm{F}}, \epsilon_{\mathrm{F}} + \hbar\omega_{\mathrm{D}}]$ 内时才非零。这里的 $\hbar\omega_{\mathrm{D}}$ 通常对应于德拜能量，即晶格振动的最大能量。

解决这个问题的关键在于**[泡利不相容原理](@entry_id:141850) (Pauli exclusion principle)**。由于[费米海](@entry_id:136725)内部的所有态都已被占据，这两个额外的电子在相互散射时，其末态只能是费米能以上的空态。这个限制极大地压缩了可用的相空间，并从根本上改变了问题的性质。

为了最大化利用这个受限的相空间，能量最低的配对态是总动量为零的态。这意味着两个电子的动量相反，$(\mathbf{k}, -\mathbf{k})$。为了使总[波函数](@entry_id:147440)反对称，如果空间[波函数](@entry_id:147440)是对称的（$s$-波配对），则自旋部分必须是反对称的，即**自旋单态 (spin-singlet)** $\frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle)$。

通过求解这两个电子的薛定谔方程，可以发现，即使吸引作用 $|V|$ 任意微弱，系统也总能形成一个束缚态，其能量低于两个电子分别占据[费米能](@entry_id:143977)时的总能量 $2\epsilon_{\mathrm{F}}$。这个束缚态就是**库珀对 (Cooper pair)**。束缚能 $\Delta_B$ 的大小由下式给出：

$$
\Delta_B = E_{\text{bound}} - 2\epsilon_{\mathrm{F}} \approx -2\hbar\omega_{\mathrm{D}}\exp\left(-\frac{2}{N(0)|V|}\right)
$$

其中，$N(0)$ 是[费米能级](@entry_id:143215)处的**单[自旋态](@entry_id:149436)密度**。这个结果有两个非凡的特征：
1.  **不稳定性**：只要存在任意微弱的吸[引力](@entry_id:175476) ($|V| > 0$)，束缚态就一定形成 ($\Delta_B  0$)。这表明，一个充满电子的[费米面](@entry_id:137798)在面对吸引相互作用时是内禀不稳定的，它会自发地通过形成库珀对来降低系统总能量。
2.  **非解析性 (Non-analyticity)**：束缚能对相互作用强度 $|V|$ 的依赖关系是指数形式的，无法在 $|V|=0$ 处进行[泰勒展开](@entry_id:145057)。这预示着超[导电性](@entry_id:137481)是一种[非微扰现象](@entry_id:149275)，不能通过对正常金属态的简单微扰来描述。

从更现代的观点看，[库珀不稳定性](@entry_id:145007)可以从**粒子-粒子[阶梯图](@entry_id:263049) (particle-particle ladder diagrams)** 的求和中得到解释 [@problem_id:2802563]。重复的吸引相互作用形成一个几何级数，其和（T-矩阵）的分母中包含一项所谓的**库珀气泡图 (Cooper bubble)** $\Pi(\Omega)$。在零温极限下，由于[费米面](@entry_id:137798)的存在，这个气泡图的实部在总能量 $\Omega \to 0$ 时会呈对数发散。这种发散保证了对于任何 $|V| > 0$，T-矩阵总会在某个负能量处出现极点，这个极点就对应于库珀对束缚态。在**[重整化群](@entry_id:147717) (renormalization group, RG)** 的语言中，这种对数发散意味着吸引相互作用是一个“边缘攸关”的[耦合常数](@entry_id:747980)，它会在低能标下流向强耦合，最终导致费米液[基态](@entry_id:150928)失稳，形成新的凝聚态。

### [BCS基态](@entry_id:136275)与超导能隙

[库珀问题](@entry_id:161364)揭示了费米海对形成单个电子对的不稳定性。[BCS理论](@entry_id:144185)则将这一思想推广到宏观数量的电子，构建了一个描述超导[基态](@entry_id:150928)的完整[多体理论](@entry_id:169452)。

该理论的核心是**简化的BCS[哈密顿量](@entry_id:172864) (reduced BCS Hamiltonian)** [@problem_id:2802602]，它包含了电子的动能项和只保留了导致[库珀配对](@entry_id:195218)的关键相互作用项：

$$
H_{\text{BCS}}=\sum_{\mathbf{k}\sigma}\xi_{\mathbf{k}}\, c_{\mathbf{k}\sigma}^{\dagger}c_{\mathbf{k}\sigma}-\sum_{\mathbf{k}\mathbf{k'}}V_{\mathbf{k}\mathbf{k'}}\, c_{\mathbf{k}\uparrow}^{\dagger}c_{-\mathbf{k}\downarrow}^{\dagger}\, c_{-\mathbf{k'}\downarrow}c_{\mathbf{k'}\uparrow}
$$

这里，$\xi_{\mathbf{k}}=\varepsilon_{\mathbf{k}}-\mu$ 是相对于化学势 $\mu$ 的[单粒子能量](@entry_id:160812)，$c_{\mathbf{k}\sigma}^{\dagger}$ 和 $c_{\mathbf{k}\sigma}$ 是电子的产生和湮灭算符。第二项描述了一个动量为 $(\mathbf{k'}\uparrow, -\mathbf{k'}\downarrow)$ 的[库珀对](@entry_id:143370)被散射到 $(\mathbf{k}\uparrow, -\mathbf{k}\downarrow)$ 状态的过程，其中 $V_{\mathbf{k}\mathbf{k'}}$ 是吸引相互作用矩阵元（约定 $V_{\mathbf{k}\mathbf{k'}} \ge 0$）。

为了求解这个多体[哈密顿量](@entry_id:172864)，BCS理论采用了**[平均场近似](@entry_id:144121) (mean-field approximation)**。其核心思想是，由于存在大量的库珀对，我们可以将[四费米子相互作用](@entry_id:184227)项线性化，用其平均值来代替。这引入了一个关键概念——**超导序参量 (superconducting order parameter)**，通常用 $\Delta_{\mathbf{k}}$ 表示 [@problem_id:2802577]：

$$
\Delta_{\mathbf{k}} \equiv -\sum_{\mathbf{k}'} V_{\mathbf{k}\mathbf{k}'}\, \langle c_{-\mathbf{k}'\downarrow}c_{\mathbf{k}'\uparrow} \rangle
$$

序参量 $\Delta_{\mathbf{k}}$ 本质上是[库珀对](@entry_id:143370)[湮灭算符](@entry_id:165390)的宏观系综平均值。一个非零的 $\Delta_{\mathbf{k}}$ 意味着[库珀对](@entry_id:143370)发生了宏观凝聚。从对称性的角度看，$\Delta_{\mathbf{k}}$ 的出现标志着系统 U(1) 规范对称性的**自发破缺 (spontaneous symmetry breaking)**。在与粒子数守恒相关的全局 U(1) [规范变换](@entry_id:176521) $c_{\mathbf{k}\sigma} \to e^{i\phi}c_{\mathbf{k}\sigma}$ 下，序参量的变换行为是 $\Delta_{\mathbf{k}} \to e^{2i\phi}\Delta_{\mathbf{k}}$。这意味着超导态选择了一个特定的宏观相位，破坏了原[哈密顿量](@entry_id:172864)的对称性。

在平均场近似下，BCS[哈密顿量](@entry_id:172864)可以被[对角化](@entry_id:147016)，但这需要引入一种新的[准粒子](@entry_id:136584)——**博戈留波夫[准粒子](@entry_id:136584) (Bogoliubov quasiparticles)**。为了方便处理，我们通常使用**南部-戈尔科夫 (Nambu-Gor'kov) 形式** [@problem_id:2802490]，它将粒子和空穴放在同一个矢量中，$\Psi_{\mathbf{k}} = (c_{\mathbf{k}\uparrow}, c_{-\mathbf{k}\downarrow}^{\dagger})^{T}$。在此表示下，[平均场哈密顿量](@entry_id:751814)矩阵为：

$$
\hat{h}_{\mathbf{k}} = \begin{pmatrix} \xi_{\mathbf{k}}  \Delta_{\mathbf{k}} \\ \Delta_{\mathbf{k}}^{*}  -\xi_{\mathbf{k}} \end{pmatrix} = \xi_{\mathbf{k}}\tau_{z} + \text{Re}(\Delta_{\mathbf{k}})\tau_{x} - \text{Im}(\Delta_{\mathbf{k}})\tau_{y}
$$

其中 $\tau_{x,y,z}$ 是作用于粒子-空穴空间的[泡利矩阵](@entry_id:139493)。非对角项 $\Delta_{\mathbf{k}}$ 直接耦合了动量为 $\mathbf{k}$ 的粒子态和动量为 $-\mathbf{k}$ 的空穴态，这就是**粒子-空穴混合 (particle-hole mixing)** 的数学体现。

[对角化](@entry_id:147016)这个 $2\times 2$ 矩阵，我们得到新的本征能量，即博戈留波夫[准粒子](@entry_id:136584)的激发谱：

$$
E_{\mathbf{k}} = \sqrt{\xi_{\mathbf{k}}^{2} + |\Delta_{\mathbf{k}}|^{2}}
$$

这个[色散关系](@entry_id:140395)是BCS理论最重要的结果之一。它表明，与正常金属中可以在[费米面](@entry_id:137798)附近以任意小能量激发电子-空穴对不同，在超导态中，创造一个最简单的[准粒子激发](@entry_id:138475)需要一个最小的能量。这个最小能量发生在费米面上 ($\xi_{\mathbf{k}} = 0$)，其值为 $|\Delta_{\mathbf{k}}|$。这个能量最小值就是**超导能隙 (superconducting energy gap)**。

[能隙](@entry_id:191975)的存在意味着在能量范围 $|E|  |\Delta|$ 内，不存在任何单粒子[激发态](@entry_id:261453)。这直接导致了超导态的单粒子**[态密度](@entry_id:147894) (density of states, DOS)** 在费米能级附近出现一个硬的[能隙](@entry_id:191975)。对于各向同性的 $s$-波[超导体](@entry_id:191025)（$\Delta_{\mathbf{k}} = \Delta$ 为常数），超导态的[态密度](@entry_id:147894) $N_s(E)$ 表现为：

$$
N_{s}(E) = N(0)\,\frac{|E|}{\sqrt{E^{2}-\Delta^{2}}},\quad \text{for } |E| \ge \Delta
$$

并且在 $|E|  \Delta$ 时，$N_s(E) = 0$。这种在[能隙](@entry_id:191975)边缘发散的“相干峰”是超导态电子谱的一个标志性特征，可以通过[扫描隧道谱](@entry_id:157738)等实验手段直接观测到。

### [热力学性质](@entry_id:146047)与[相变](@entry_id:147324)

超导[序参量](@entry_id:144819)和[能隙](@entry_id:191975)的大小不是一成不变的，而是依赖于温度。随着温度升高，[热激发](@entry_id:275697)会破坏[库珀对](@entry_id:143370)的凝聚，导致[能隙](@entry_id:191975) $\Delta(T)$ 减小。$\Delta(T)$ 的具体行为由有限温度下的BCS[自洽方程](@entry_id:155949)决定。

当温度升高到某个**临界温度 (critical temperature)** $T_c$ 时，[能隙](@entry_id:191975)完全闭合，$\Delta(T_c)=0$，超导态消失，系统恢复到正常金属态。在BCS平均场理论的框架内，可以精确分析 $T_c$ 附近的[相变](@entry_id:147324)行为 [@problem_id:2802500]。

在临界温度 $T_c$ 附近，序参量 $\Delta(T)$ 的行为可以近似表示为：

$$
\Delta(T) \propto \sqrt{1 - \frac{T}{T_c}} \quad \text{as } T \to T_c^{-}
$$

这表明，[序参量](@entry_id:144819)是**连续**地趋向于零的，其均场[临界指数](@entry_id:142071)为 $1/2$。根据埃伦费斯特（Ehrenfest）[相变](@entry_id:147324)分类，这种行为对应于**[二级相变](@entry_id:154877) (second-order phase transition)**。[二级相变](@entry_id:154877)的特征如下：

1.  **自由能**：自由能本身是连续的。
2.  **熵**：作为自由能的[一阶导数](@entry_id:749425)，熵在[相变](@entry_id:147324)点是连续的。这意味着[相变过程](@entry_id:147919)中没有**[潜热](@entry_id:146032) (latent heat)** 的吸收或释放。
3.  **比热**：作为自由能的[二阶导数](@entry_id:144508)，比热在[相变](@entry_id:147324)点表现为一个有限的**跳变 (jump)**。BCS理论预言，在$T_c$处，[电子比热](@entry_id:144099)的跳变 $\Delta C$ 与正常态[电子比热](@entry_id:144099) $C_n$ 的比值是一个[普适常数](@entry_id:165600)，即 $\Delta C / C_n(T_c) \approx 1.43$。这个比热跳变是验证[超导相变](@entry_id:141757)为[二级相变](@entry_id:154877)的一个关键实验证据。

### 杂质的角色：[安德森定理](@entry_id:139654)与对破缺

真实材料中不可避免地存在各种缺陷和杂质，它们对超导电性的影响是一个至关重要的问题。

对于传统的各向同性 $s$-波[超导体](@entry_id:191025)，一个惊人的理论结果是**[安德森定理](@entry_id:139654) (Anderson's theorem)** [@problem_id:2802507]。该定理指出，弱的、非磁性的[杂质散射](@entry_id:267814)不会改变超导[临界温度](@entry_id:146683) $T_c$。

其微观机制相当精妙：[杂质散射](@entry_id:267814)对电子的作用主要体现在两个方面。一方面，它通过[自能修正](@entry_id:754667)使得[准粒子](@entry_id:136584)具有有限的寿命，这倾向于抑制配对。另一方面，在 $s$-波情况下，它通过[顶点修正](@entry_id:146982)增强了有效[配对相互作用](@entry_id:158014)。在基于Nambu-Gor'kov形式主义的严格计算中可以证明，对于时间反演对称的非磁性散射体和各向同性的 $s$-波序参量，这两项修正效应在决定 $T_c$ 的线性化[能隙方程](@entry_id:141924)中**精确抵消**。因此，$T_c$ 对这类杂质“免疫”。

然而，[安德森定理](@entry_id:139654)的[适用范围](@entry_id:636189)是有限的。对于具有**各向异性[配对对称性](@entry_id:139531)**的[超导体](@entry_id:191025)，例如 $d$-波[超导体](@entry_id:191025)（其[序参量](@entry_id:144819)在费米面上会变号），情况则完全不同 [@problem_id:2802498]。在这种情况下，[安德森定理](@entry_id:139654)失效，非磁性杂质会成为强烈的**对破缺 (pair-breaking)** 因子，显著抑制 $T_c$。

其物理根源在于，[杂质散射](@entry_id:267814)使得电子在费米面上的不同动量点之间跃迁。对于 $d$-波[超导体](@entry_id:191025)，电子可能从一个[序参量](@entry_id:144819)为正的区域 $(\Delta(\mathbf{k}) > 0)$ 散射到一个[序参量](@entry_id:144819)为负的区域 $(\Delta(\mathbf{k'})  0)$。[库珀对](@entry_id:143370)[波函数](@entry_id:147440)在[费米面](@entry_id:137798)上经历这种快速的、由散射引起的符号变化，会破坏其[相干性](@entry_id:268953)，从而削弱配对。从数学上看，之前在 $s$-波情况下的精确抵消不复存在，导致 $T_c$ 随着[杂质散射](@entry_id:267814)率 $\Gamma$ 的增加而迅速下降。根据阿布里科索夫-戈尔科夫（Abrikosov-Gor'kov）理论，对于弱散射极限下的 $d$-波[超导体](@entry_id:191025)， $T_c$ 的抑制在领先阶上是线性的：

$$
T_c \approx T_{c0} - \frac{\pi}{4}\Gamma
$$

其中 $T_{c0}$ 是纯净样品中的临界温度。因此，通过研究非磁性杂质对 $T_c$ 的影响，可以作为一种有效的实验手段来判别[超导体](@entry_id:191025)的[配对对称性](@entry_id:139531)是传统的 $s$-波还是非常规的各向异性波。

### 超越BCS：强耦合与[延迟效应](@entry_id:199612)

BCS理论取得了巨大的成功，但它建立在一些简化假设之上，例如[弱耦合](@entry_id:140994)近似和瞬时相互作用。对于许多实际的[强耦合超导体](@entry_id:140567)（如铅、汞等），[BCS理论](@entry_id:144185)的定量预测与实验结果存在偏差。一个更精确的理论是**Migdal-[Eliashberg理论](@entry_id:144676)**，它能够处理强耦合和相互作用的[延迟效应](@entry_id:199612)。

[Eliashberg理论](@entry_id:144676)的核心思想是，[电子-声子相互作用](@entry_id:140708)的能量依赖性不能被忽略。该理论引入了两个依赖于频率（在计算中通常是[松原频率](@entry_id:197724) $i\omega_n$）的函数 [@problem_id:2802509]：

1.  **频率依赖的[能隙](@entry_id:191975)函数 $\Delta(i\omega_n)$**: 描述了不同[能量尺度](@entry_id:196201)下的配对强度。
2.  **[质量重整化](@entry_id:139777)函数 $Z(i\omega_n)$**: 描述了电子因与[声子](@entry_id:140728)云的“拖拽”效应而增加的[有效质量](@entry_id:142879)。

这两个函数通过一组耦合的[非线性](@entry_id:637147)积分方程（即**[Eliashberg方程](@entry_id:147834)**）自洽地确定。方程的输入是两个描述材料基本属性的函数：

*   **[Eliashberg谱函数](@entry_id:140372) $\alpha^2F(\Omega)$**: 这是加权的[声子态密度](@entry_id:199476)，$\Omega$ 是[声子频率](@entry_id:753407)。它包含了[电子-声子相互作用](@entry_id:140708)强度的详细信息，可以从实验（如[中子散射](@entry_id:142835)或隧道谱）中提取。
*   **[库仑赝势](@entry_id:145447) $\mu^*$**: 这是一个唯象参数，用于描述被延迟的[声子](@entry_id:140728)吸引作用所屏蔽后的瞬时电子-电子[库仑排斥](@entry_id:181876)。

[Eliashberg方程](@entry_id:147834)的典型形式如下（在[松原频率](@entry_id:197724)轴上）：

$$
Z(i\omega_{n}) = 1 + \frac{\pi T}{\omega_{n}} \sum_{m} \lambda(n-m) \frac{\omega_{m}}{\sqrt{\omega_{m}^{2}+\Delta^{2}(i\omega_{m})}}
$$

$$
Z(i\omega_{n})\Delta(i\omega_{n}) = \pi T \sum_{m} \left[ \lambda(n-m) - \mu^{\ast}\theta(\omega_{c}-|\omega_{m}|) \right] \frac{\Delta(i\omega_{m})}{\sqrt{\omega_{m}^{2}+\Delta^{2}(i\omega_{m})}}
$$

其中，[相互作用核](@entry_id:193790) $\lambda(n-m)$ 直接由 $\alpha^2F(\Omega)$ 决定。[Eliashberg理论](@entry_id:144676)不仅能更精确地计算 $T_c$，还能解释许多BCS理论无法描述的强耦合效应，例如[能隙](@entry_id:191975)与 $T_c$ 的比值 $2\Delta(0)/k_BT_c$ 会偏离BCS的普适值 $3.53$。它为理解传统超[导电性](@entry_id:137481)提供了一个更为定量和强大的理论框架。