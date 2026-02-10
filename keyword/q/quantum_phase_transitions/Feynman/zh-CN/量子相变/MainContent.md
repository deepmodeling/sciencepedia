## 引言
[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)定义了我们周围的世界，从水结成冰到铁产生磁性。几个世纪以来，这些转变一直被理解为能量与温度驱动的热混沌之间的一场斗争。但是，如果我们将温度完全从等式中移除，让一个量子系统处于绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)，会发生什么呢？在这个极寒的领域，热涨落消失了，但宇宙远非静止。一种由量子力学内禀不确定性本身驱动的、不同类型的变化成为可能。

本文旨在探讨量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman) (QPTs) 这一迷人现象，它重塑了我们对物质[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的理解。我们将探索即使在零温下，调控[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)或压力等参数如何能在两个相互竞争的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)之间引发剧烈的转变。您将了解到支配这个奇异新世界的基本概念。

首先，在“原理与机制”一章中，我们将揭示[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)的物理学，介绍作为基石的[横向场](@keyword=transverse_field|lang=zh-CN|style=Feynman)伊辛模型，并阐明将量子行为与更高维度中的经典统计联系起来的深刻的量子-经典映射。随后，“应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系”一章将展示这些理论思想如何为理解真实世界的现象提供了关键的蓝图，从奇异磁体和[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的行为，到利用[超冷原子](@keyword=ultracold_atoms|lang=zh-CN|style=Feynman)和光进行的革命性实验。

## 原理与机制

想象一下你正在冷却一壶水。当温度达到零[摄氏度](@keyword=celsius|lang=zh-CN|style=Feynman)时，一个壮观的转变发生了：混乱、翻滚的液态水分子锁定成一个刚性、美丽的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。我们称之为[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)。几个世纪以来，这是我们所知道的唯一一种[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)，它们都由热能的嘈杂舞蹈所驱动。斗争总是在偏爱有序的能量和偏爱混沌的熵之间进行。当你降低温度时，能量获胜，一个全新的、更有序的相就诞生了。

但是，如果你一直降温到底呢？在可能的最低温度——绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)，$T=0$ 时，会发生什么？在这一点上，所有的热运动都停止了。不再有混沌，不再有热晃动。从经典角度看，一个原子将完全静止。你可能认为这就是故事的结局，一种完美、冻结的宁静状态。但你错了。宇宙在其量子核心，从未真正静止过。

### 一种新的寒冷：量子领域的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)

即使在绝对零度，[海森堡不确定性原理](@keyword=heisenberg_s_uncertainty_principle|lang=zh-CN|style=Feynman)依然主宰一切。你无法同时以完美的精度知道一个粒子的位置和动量。这不是我们仪器的局限，而是自然界的一个基本属性。这种内在的不确定性产生了**[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)**。一个粒子，即使在其最低能量状态，也在不断地探测其周围环境，存在于一种幽灵般的可能性叠加态中。

正是这些[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)，而非热涨落，能够驱动一种全新的、奇异的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)：**量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)** (QPT)。我们不是调节温度，而是调节一种不同的参数——[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)、压力或者化学物质的浓度。这个参数改变了游戏的基本规则，改变了支配系统的量子哈密顿量。量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)是两个相互竞争的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)之间的斗争，是系统以其最低可能能量状态[排列](@keyword=permutation|lang=zh-CN|style=Feynman)自身的两种不同方式之间的斗争。

让我们用一个极其简单却又含义深远的模型来具体说明这一点：**[横向场](@keyword=transverse_field|lang=zh-CN|style=Feynman)[伊辛模型](@keyword=ising_model|lang=zh-CN|style=Feynman)** (TFIM)。想象一条由微小的量子磁体（或称自旋）组成的[一维链](@keyword=one_dimensional_chains|lang=zh-CN|style=Feynman)，这些自旋可以指向“上”或“下”。规则很简单：
1. 每个自旋都希望与它的邻居对齐。这种[相互作用强度](@keyword=interaction_strength|lang=zh-CN|style=Feynman)为 $J$，它倾向于一个有序的铁[磁基态](@keyword=magnetic_ground_states|lang=zh-CN|style=Feynman)，其中所有自旋都指向同一个方向（例如，全部向上）。
2. 我们施加一个外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，不是在上下方向，而是在横向（侧向）方向。这个强度为 $g$ 的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)试图翻转自旋，倾向于一个“量子顺磁”[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)，其中每个自旋都处于上*和*下的[量子叠加](@keyword=quantum_superposition|lang=zh-CN|style=Feynman)态中。

系统的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)由这两种力量的竞争决定，由比值 $g/J$ 捕捉 [@problem_id:1998412]。当 $g$ 非常小时，邻近相互作用 $J$ 占主导，[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)是一个简单的铁磁体。当 $g$ 非常大时，[横向场](@keyword=transverse_field|lang=zh-CN|style=Feynman)获胜，[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)是一个顺磁体。在这个比值的一个精确的临界值 $(g/J)_c$ 处，系统经历一次量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)。在这个**量子临界点**，系统无法决定选择哪个[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)，而最有趣的物理现象正是在这里展开。

### 量子-经典联系：时间的障眼法

我们该如何着手分析一个系统在这样一个[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)猖獗的[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)上的行为呢？在这里，我们遇到了现代物理学中最优美、最强大的思想之一，这是 [Richard Feynman](@keyword=richard_feynman|lang=zh-CN|style=Feynman) 首次充分认识到的一套“魔术”：**量子-经典映射**。

想想我们[自旋链](@keyword=spin_chain|lang=zh-CN|style=Feynman)中的量子涨落。在[横向场](@keyword=transverse_field|lang=zh-CN|style=Feynman)的影响下，单个自旋并不仅仅是静止的；它的方向在*时间*中涨落。这个单一量子自旋随时间演化的历史，看起来有点像一排经典的、可以随时翻转的自旋。现在，如果我们考虑整条[量子自旋链](@keyword=quantum_spin_chain|lang=zh-CN|style=Feynman)呢？它在时间中的演化创造了一个二维的“世界面”。惊人的洞见是，包含我们[一维量子系统](@keyword=one_dimensional_quantum_systems|lang=zh-CN|style=Feynman)在 $T=0$ 时所有信息的量子配分函数，可以被形式上证明与一个处于有限温度下的二维*经典*伊辛模型的配分函数相同！[@problem_id:1998412]

这就是量子-经典映射。一个 $d$ 维系统中的量子涨落可以在数学上换成一个 $(d+1)$ 维经典系统中的[热涨落](@keyword=thermal_fluctuations|lang=zh-CN|style=Feynman)。这个额外的维度不是空间维度，而是**虚时间**维度。它是一个数学构造，但其后果却是非常真实的。这一发现揭示了自然法则中一种深刻而出人意料的统一性：绝对零度下量子力学的奇异、概率性世界，其背后竟由与更高维度中经典系统统计性晃动相同的普适原理所支配。

### 临界边缘的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)：动力学[临界指数](@keyword=critical_exponents|lang=zh-CN|style=Feynman)

在一个我们熟悉的热[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，比如水沸腾时，有一个关键量会发散：关联长度 $\xi$。这是系统各部分相互“交流”的特征距离。在[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，$\xi$ 变为无穷大；每个水分子都知晓其他所有分子的信息。

在量子临界点，则有另一番景象。不仅关联长度 $\xi$ 发散，关联*时间* $\tau$ 也发散。系统的涨落慢得像蜗牛。这两个发散尺度之间的关系是量子[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)的决定性特征之一。我们将其写为：
$$ \tau \sim \xi^z $$
指数 $z$ 被称为**动力学临界指数**。它告诉我们[时空](@keyword=space_time|lang=zh-CN|style=Feynman)本身在[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)是如何构造的。

对于许多系统，比如我们的一维[横向场](@keyword=transverse_field|lang=zh-CN|style=Feynman)伊辛模型，结果是 $z=1$ [@problem_id:1177227]。这意味着时间和空间以相同的方式标度。[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)处的低能激发行为如同相对论性粒子，其能量 $E$ 与动量 $k$ 成正比 ($E \sim k$)。

但大自然比这更有创造力。在其他系统中，我们可以发现 $z=2$ 或 $z=3$，甚至其他值 [@problem_id:2005728] [@problem_id:2985445]。当 $z \neq 1$ 时，[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)呈现出奇异的各向异性。时间和空间不再处于平等地位。这个指数 $z$ 不仅仅是一个数学上的奇特之处；它是临界态的一个基本指纹。

现在我们可以完善我们的量子-经典映射。相应经典系统的“有效”维度不仅仅是 $d+1$，而更普遍地是：
$$ d_{eff} = d + z $$
这是涨落所经历的真实维度，是物理空间维度和时间维度的结合，并由动力学指数 $z$ 加权 [@problem_id:1906286]。

### 维度的力量：打破旧规则

有了[有效维度](@keyword=effective_dimension|lang=zh-CN|style=Feynman) $d_{eff} = d+z$ 的概念，我们可以做出一些惊人的预测。

[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)理论中一个著名的结果是 Mermin-Wagner 定理，该定理指出，在维度 $d \le 2$ 时，具有连续对称性（比如自旋可以在一个圆上指向任何方向）的系统在任何有限温度下都不能有真正的[长程序](@keyword=long_range_order|lang=zh-CN|style=Feynman)。热涨落太强大了，总会破坏秩序。你可能会天真地认为，这个规则对于 $T=0$ 的二维*量子*系统会更加适用，因为那里的[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)处于顶峰。

但考虑一个 $z=2$ 的二维量子转[子模](@keyword=submodule|lang=zh-CN|style=Feynman)型。它的有效经典维度是多少？是 $d_{eff} = d+z = 2+2 = 4$。由于 $4$ 大于[下临界维度](@keyword=lower_critical_dimension|lang=zh-CN|style=Feynman) $2$，Mermin-Wagner 定理被规避了！量子涨落通过为系统提供额外的两个“[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)维度”来探索，实际上帮助稳定了有序相，以抵抗它们自身的破坏倾向。在 $T=0$ 时，从量子虚空中可以奇迹般地诞生出在二维经典对应物中被禁止的长程序 [@problem_id:2005728]。

这个技巧在另一个方向也同样有效。存在一个**[上临界维度](@keyword=upper_critical_dimension|lang=zh-CN|style=Feynman)**，在此维度之上，涨落变得无关紧要，一个非常简单的“平均场”理论变得精确。对于许多经典系统，这个维度是 $d=4$。那么像三维[横向场](@keyword=transverse_field|lang=zh-CN|style=Feynman)[伊辛模型](@keyword=ising_model|lang=zh-CN|style=Feynman)这样的量子系统呢，它有 $z=1$？它的[有效维度](@keyword=effective_dimension|lang=zh-CN|style=Feynman)是 $d_{eff} = 3+1 = 4$。这意味着这个三维量子系统的[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)可以被最简单的[平均场理论](@keyword=mean_field_theory|lang=zh-CN|style=Feynman)完美描述，该理论预测了诸如序参量指数 $\beta = 1/2$ 的临界指数 [@problem_id:1216772] [@problem_id:1116329]。三个空间维度中的狂野[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)的强度恰好与四个维度中的热涨落强度相同，这是一个它们变得可控的阈值。

### 超越[简单图](@keyword=simple_graphs|lang=zh-CN|style=Feynman)景：[奇异金属](@keyword=strange_metals|lang=zh-CN|style=Feynman)与[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)的灵魂

我们建立的框架是强大的，但这仅仅是故事的开始。量子临界点附近是涨落的风暴中心，它能够撕裂我们对物质理解的根基。

在普通金属中，电子尽管相互作用很强，但它们会协同作用，表现得像称为“[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)”的近独立粒子。这就是著名的[费米液体理论](@keyword=fermi_liquid_theory|lang=zh-CN|style=Feynman)，是我们理解金属的基础。但在[量子临界点](@keyword=quantum_critical_point|lang=zh-CN|style=Feynman)附近，临界涨落可能变得如此剧烈，以至于将这些[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)撕成碎片。电子失去了它的身份，溶解成一种奇异的、集体的电子汤。系统变成了**[非费米液体](@keyword=non_fermi_liquids|lang=zh-CN|style=Feynman)**，或称**[奇异金属](@keyword=strange_metals|lang=zh-CN|style=Feynman)**。这种[物质状态](@keyword=states_of_matter|lang=zh-CN|style=Feynman) defies 了我们的常规描述。实验上，我们在一些奇异行为中看到了它的迹象，比如[电子比热](@keyword=electronic_specific_heat|lang=zh-CN|style=Feynman)容除以温度，$C_e/T$，它不是一个常数（如在正常金属中），而是在温度趋于零时呈对数发散（$C_e/T \sim \ln(1/T)$）或幂律发散（$C_e/T \sim T^{-\alpha}$）[@problem_id:2986246] [@problem_id:2985445]。就好像电子的[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)变得无穷大，这是一个[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)图像完全失效的明确信号。

更令人吃惊的事情也可能发生。考虑两种完全不同类型的有序态之间的转变，例如，一个[反铁磁体](@keyword=antiferromagnets|lang=zh-CN|style=Feynman)（具有棋盘状自旋图案）和一个[价键固体](@keyword=valence_bond_solid|lang=zh-CN|style=Feynman)（由配对自旋组成的晶体）。我们标准的[朗道相变理论](@keyword=landau_theory_of_phase_transitions|lang=zh-CN|style=Feynman)，一个世纪以来一直很成功，它预测这两种截然不同的序应该由一个“一级”[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)分开，就像水和油一样——它们在边界处不应该混合。然而，在一些量子材料中，计算机模拟表明它们可以连续地相互转变。

为了解释这一点，物理学家们提出了一个革命性的想法：**[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)[量子临界性](@keyword=quantum_criticality|lang=zh-CN|style=Feynman)**。该理论认为，在[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，磁体的基本组成部分（自旋）会“[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)”或[解禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)，形成新的、携带原始[量子数](@keyword=quantum_numbers|lang=zh-CN|style=Feynman)分数的演生粒子——就像夸克被限制在质子内部，但在极高能量下表现得像[自由粒子](@keyword=the_free_particle|lang=zh-CN|style=Feynman)一样。这些演生粒子通过一种*演生规范力*相互作用，这是一种只存在于[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)的新型“[电磁力](@keyword=electromagnetic_forces|lang=zh-CN|style=Feynman)”[@problem_id:2999163]。这是一个粒子的身份本身都可变的世界，支配它们的力量是从集体舞蹈中诞生的。在这个暮光区，甚至[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)本身的性质也可能改变，例如在一个[连续相变](@keyword=continuous_phase_transitions|lang=zh-CN|style=Feynman)线与突变[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)线交汇的**[三相点](@keyword=triple_point|lang=zh-CN|style=Feynman)**上 [@problem_id:1154189]。

这就是前沿。[量子临界点](@keyword=quantum_critical_point|lang=zh-CN|style=Feynman)不仅仅是绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)的奇观；它们是新粒子、新力量和自然界新组织原则被锻造的熔炉。它们向我们展示，即使在最深的寒冷中，宇宙也充满了创造性的量子能量，将物质塑造成我们才刚刚开始想象的形态。