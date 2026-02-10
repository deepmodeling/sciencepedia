## 引言
量子物质领域充满了各种[涌现现象](@keyword=emergent_phenomena|lang=zh-CN|style=Feynman)，其集体行为常常不符合简单的直觉。其中最深刻的现象之一是超[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)，即某些材料在[零电阻](@keyword=zero_resistance|lang=zh-CN|style=Feynman)下导电的能力。几十年来，Bardeen-Cooper-Schrieffer (BCS) 理论为此提供了一个优美而完整的解释，将此效应归因于电子通过[晶格振动](@keyword=crystal_lattice_vibrations|lang=zh-CN|style=Feynman)介导的引力进行配对。然而，新一类[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)，特别是铁基化合物的发现，提出了一个谜题：它们的性质无法用常规机制来解释。这造成了一个重大的知识空白，并引发了一个问题：电子配对如何可能产生于本应阻止其配对的力——即它们之间的相互排斥力？

本文将探讨这一悖论的优雅解决方案：$s^{\pm}$波配对态。我们将深入探讨这种非常规机制的核心，揭示排斥力本身如何被用来创造一个稳固的超导态。在第一章**原理与机制**中，我们将剖析[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的物理学，将$s^{\pm}$波态与其常规的$s^{++}$波和非常规的$d$波对应物进行对比，并审视其符号改变性质的确凿实验证据。随后，在**应用与跨学科联系**中，我们将拓宽视野，探讨[费米子配对](@keyword=fermionic_pairing|lang=zh-CN|style=Feynman)这一基本概念如何成为一个普适的主题，出现在人工设计的量子材料、[超冷原子气体](@keyword=ultracold_atomic_gases|lang=zh-CN|style=Feynman)以及中子星内部的极端环境等各种背景中。

## 原理与机制

介绍了非常规超导的谜题之后，现在让我们深入探讨其背后的运作机制。要真正领略$s^{\pm}$-wave态的精妙之美，我们必须首先了解它所脱离的世界——常规超导的世界。这是一个关于吸引、排斥、对称性和量子奇异性的故事，其中一个悖论的解决常常为另一个更深奥的悖论打开了大门。

### 正统图像：[声子](@keyword=phonons|lang=zh-CN|style=Feynman)介导之舞

所有超导现象的核心都存在一个奇特而美妙的实体：**[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)**。您知道，电子是[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)，是量子世界中固执的个人主义者。[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)禁止任意两个电子占据相同的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。这种孤僻的特性使得它们难以以集体、协调的方式运动。但如果两个电子能联合起来形成一个[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)——一种更合群、喜欢与其同类占据相同状态的粒子，情况会怎样呢？这样一个电子对的集合体便可以像单一的[量子流体](@keyword=quantum_fluids|lang=zh-CN|style=Feynman)一样流动，且没有电阻。

为了实现这一点，电子对的总[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)（即其空间部分和自旋部分的乘积）在交换两个电子时必须是反对称的。让我们考虑最简单的情况：一个相对轨道角动量为零的电子对，即所谓的**s波**态。在空间上，这就像两个舞者在一个紧密的圆圈中一起旋转，始终保持相同的距离。它们[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的空间部分是对称的。那么，为了满足泡利原理，它们的自旋部分必须是反对称的。对于两个自旋为1/2的电子来说，这意味着它们必须形成一个**自旋单态**，其中它们的自旋方向相反，总自旋为零 [@problem_id:1124462]。

但这引出了一个问题：为什么两个通过库仑力相互激烈排斥的电子会想要配对呢？在[常规超导体](@keyword=conventional_superconductors|lang=zh-CN|style=Feynman)中，答案在于电子游弋于其中的正离子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。想象一个电子飞速穿过这个[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。它会把较重的带正电的离子吸引过来，产生一个瞬时的涟漪，一个正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的局部集中区——可以看作是一种“尾迹”。稍后经过的第二个电子就会被这个带正电的尾迹所吸引。这有点像两个人躺在一个软床垫上；一个人造成的凹陷会使另一个人滚向他。这种由晶格振动（即**[声子](@keyword=phonons|lang=zh-CN|style=Feynman)**）介导的间接、延迟的吸引力，正是束缚常规[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的“胶水”。

当然，电子之间直接的库仑排斥并不会就此消失。这是一场[声子介导的吸引](@keyword=phonon_mediated_attraction|lang=zh-CN|style=Feynman)力与裸[静电排斥](@keyword=electrostatic_repulsion|lang=zh-CN|style=Feynman)力之间的持续战斗。谁会获胜呢？胜利者由一种微妙的时间效应，或者用物理学的术语来说，**延迟效应**所决定。[声子](@keyword=phonons|lang=zh-CN|style=Feynman)吸引是一个缓慢、低能量的过程，其作用时间尺度与[晶格振动](@keyword=crystal_lattice_vibrations|lang=zh-CN|style=Feynman)的特征时间尺度相当。而库仑排斥则几乎是瞬时的。金属中的高能电子会非常迅速地对其产生屏蔽，从而有效地削弱了它在[声子](@keyword=phonons|lang=zh-CN|style=Feynman)胶水起作用的低能量尺度上的影响。这种被屏蔽的、较弱的排斥力被称为**[库仑赝势](@keyword=coulomb_pseudopotential|lang=zh-CN|style=Feynman)**，记为$\mu_{*}$。如果来自[声子](@keyword=phonons|lang=zh-CN|style=Feynman)的无量纲吸引耦合$\lambda$强于这种剩余的排斥力，即$\lambda > \mu_{*}$，超[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)就会出现[@problem_id:2818841]。这一优美的见解解释了为何大多数普通金属尽管电子间普遍存在排斥力，却仍能成为[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)。在很长一段时间里，这就是故事的全部。

### 非常规革命：源于排斥的配对

然而，自然界充满了惊喜。在像[重费米子化合物](@keyword=heavy_fermion_compounds|lang=zh-CN|style=Feynman)和[铁基超导体](@keyword=iron_based_superconductors|lang=zh-CN|style=Feynman)这样的材料中，[声子](@keyword=phonons|lang=zh-CN|style=Feynman)似乎太弱了，无法解释观测到的超导现象。配对的胶水必定是别的什么，一种强得多的东西。主要的“嫌疑犯”正是本应阻止配对的力：电子之间的排斥力本身！

排斥力究竟是如何产生束缚对的？这似乎就像两个敌人通过互相争吵而成为挚友一样不太可能。这个悖论的解决方案是现代物理学中最优雅的思想之一：可以通过调整电子对的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)结构来“避开”排斥力。

想象一种即将成为反铁磁体的材料。在这种状态下，[电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)倾向于以“上-下-上-下”交替的模式[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。即使材料没有完全有序化，它也会充满这种自旋模式的强大而长寿命的涨落——**反铁磁[自旋涨落](@keyword=spin_fluctuations|lang=zh-CN|style=Feynman)**。这些涨落充当了电子之间相互作用的有效媒介。两个电子可以交换一个[自旋涨落](@keyword=spin_fluctuations|lang=zh-CN|style=Feynman)，就像两个滑冰者在冰冻的池塘上通过来回投掷一个重球来“相互作用”。这种相互作用本质上是排斥性的。而且至关重要的是，它并非均匀的；对于连接具有特定动量转移$\mathbf{Q}$（对应于反铁磁模式）的电子的散射过程，这种作用尤为强烈[@problem_id:3018867]。

诀窍就在这里。虽然一个均匀的排斥“势”永远无法束缚一个电子对，但一个结构化的、依赖于动量的势却可以。库珀对可以形成一种巧妙地最小化这种排斥的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。它通过确保其[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在被排斥力连接的动量区域具有不同的符号来实现这一点。如果排斥相互作用主要在动量态$\mathbf{k}$和$\mathbf{k}+\mathbf{Q}$之间散射电子，那么如果超导能隙函数$\Delta(\mathbf{k})$满足条件$\Delta(\mathbf{k}) \approx -\Delta(\mathbf{k}+\mathbf{Q})$，系统就可以获得能量。通过这种方式，电子对将其自身[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成在排斥力最强的地方恰好具有节点或符号改变，从而有效地避开了它。就像两个互相不喜欢的人决定住在不同的城市一样，库珀对通过占据其抽象动量空间世界中具有相反“相位”的区域，来最小化其排斥性的“社交能量”。

### 对称性大观园：从$s^{++}$和$d$到$s^{\pm}$

这种通过排斥实现配对的原理开启了一个全新的可能[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)对称性的“大观园”，每种对称性都是[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)为避免排斥而扭曲自身的不同方式。

*   **常规[s波](@keyword=s_waves|lang=zh-CN|style=Feynman) ($s^{++}$):** 这是[声子](@keyword=phonons|lang=zh-CN|style=Feynman)机制中常见的情况。[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)由净吸引力驱动，因此它在费米面上的任何地方都具有相同的符号（比如说，‘+’）。它既稳固又简单。一个重要的推论，如**[Anderson定理](@keyword=anderson_s_theorem|lang=zh-CN|style=Feynman)**所阐明的，是这种态在很大程度上不受非磁性杂质的影响。杂质将电子从费米面上的一个点散射到另一个点，但由于[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)处处相同，电子对不会被破坏[@problem_id:1809304]。

*   **d波:** 这是非常规世界中的明星，发现于高温[铜氧化物超导体](@keyword=cuprate_superconductors|lang=zh-CN|style=Feynman)中。[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)具有“四叶草”形状，由一个类似$\Delta_d(\mathbf{k}) \propto \big(\cos(k_x a) - \cos(k_y a)\big)$的函数描述，其中$a$是晶格常数[@problem_id:248094] [@problem_id:1152912]。它沿着一个晶轴为正，沿着另一个晶轴为负。[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)必须沿着对角线穿过零点——这些被称为**节点**。这种符号改变发生在*单个费米面内部*。因此，$d$波超导对非磁性杂质非常敏感，因为杂质可以将一个电子对从‘+’瓣散射到‘-’瓣，从而破坏相干性。

*   **s±波:** 现在我们来到了我们的主题。$s^{\pm}$-wave态是多种思想的巧妙综合。从某种意义上说，它是一个“[s波](@keyword=s_waves|lang=zh-CN|style=Feynman)”态，因为它的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)在[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)的任何一个部分上都具有完全的s波对称性（*无节点*）。但像$d$波一样，它也是一个**符号改变**态。它是如何做到这一点的呢？诀窍在于它存在于具有多个不连通的费米面的材料中——例如，动量空间区域中心的一个小[电子口袋](@keyword=electron_pockets|lang=zh-CN|style=Feynman)和靠近角落的其他口袋。$s^{\pm}$态的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)在一组口袋上是全开放且为正的，而在另一组口袋上是全开放但为负的。

其机制正是我们讨论过的[自旋涨落](@keyword=spin_fluctuations|lang=zh-CN|style=Feynman)胶水。在像[铁基超导体](@keyword=iron_based_superconductors|lang=zh-CN|style=Feynman)这样的材料中，最强的反铁磁涨落恰好对应一个动量矢量$\mathbf{Q}$，该矢量完美地连接了中心的“正[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)”口袋和角落的“负[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)”口袋[@problem_id:1161239]。因此，系统采用了一个*在*费米面之间改变符号的s波[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，完美地利用了排斥相互作用来形成库珀对，同时避免了在$d$波态中会有害的节点。这是一个完美的折衷：名义上是s波，但其核心却隐藏着一个非常规的转折。

### 确凿证据：当场捕捉相位

[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)符号改变的想法很优美，但它是真实的吗？我们怎么可能“看到”一个[量子力学波函数](@keyword=quantum_mechanics_wavefunctions|lang=zh-CN|style=Feynman)的符号呢？答案在于量子物理学另一个优美的部分：**干涉**。

通过制造一种称为[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)（SQUID）的特殊装置，物理学家可以创建一个包含两个约瑟夫森结（[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)之间的弱连接）的闭合环路。SQUID能够承载的总[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)取决于通过两个结的路径之间的[量子干涉](@keyword=quantum_interference|lang=zh-CN|style=Feynman)，而这种干涉对穿过环路的任何磁通量都极其敏感。

现在，想象我们用一种符号改变的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)（如$d$波或$s^{\pm}$-wave材料）构建一个SQUID。如果我们巧妙地调整晶体取向，使得一个结探测到[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)为正的区域，而另一个结探测到[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)为负的区域，就会发生一些非同寻常的事情。第二个结的行为就好像它相对于第一个结具有一个内在的、固有的$\pi$ 弧度（$180^{\circ}$）的相移。

这个“$\pi$-结”完全改变了[干涉图样](@keyword=interference_pattern|lang=zh-CN|style=Feynman)。对于一个常规的$s^{++}$ [SQUID](@keyword=squid|lang=zh-CN|style=Feynman)，最大[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)出现在零磁通量处。而对于我们的$s^{\pm}$ [SQUID](@keyword=squid|lang=zh-CN|style=Feynman)，来自内在$\pi$-相移的相消干涉导致[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)在零[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)处*最小*。整个[干涉图样](@keyword=interference_pattern|lang=zh-CN|style=Feynman)发生了平移[@problem_id:2994155]。

一个更引人注目的演示是创建一个包含奇数个此类$\pi$-结的环。这样一个环是“受挫的”——不可能同时满足所有结的相位偏好。为了解决这种挫折，系统会自发地产生自己的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，以恰好等于磁通量量子一半的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)穿过环，即$\Phi_0/2 = h/(4e)$。这是一个[宏观量子现象](@keyword=macroscopic_quantum_phenomena|lang=zh-CN|style=Feynman)，一个完全由超导[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman)复杂、符号改变的性质所创造的微型[永磁体](@keyword=permanent_magnets|lang=zh-CN|style=Feynman)。在对几类材料的实验中观测到这种自发的半磁通量子，为符号改变[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的真实性提供了确凿的“铁证”，将一个优美的理论思想变成了坚实的实验事实[@problem_id:2994155]。