## 引言
[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)，即物质从一种状态到另一种状态的剧烈转变，很大程度上可以通过强大的[Landau-Ginzburg-Wilson理论](@keyword=landau_ginzburg_wilson_theory|lang=zh-CN|style=Feynman)来理解。该框架通过对相的破缺对称性进行分类，成功地描述了从水沸腾到传统磁性等各种现象。然而，在量子领域出现了一个危机：某些材料在具有根本不相容序的态之间表现出[连续相变](@keyword=continuous_phase_transitions|lang=zh-CN|style=Feynman)，例如Néel相和价键固相（Valence-Bond-Solid）——这种[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)被标准[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)明确禁戒。这个难题表明我们传统理解的失效，并要求一个新的理论基础。

本文介绍[退禁闭量子临界性](@keyword=deconfined_quantum_criticality|lang=zh-CN|style=Feynman)（DQCP），这是一个正面应对这一挑战的革命性理论。通过摒弃传统的序参量图像，DQCP提出在[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，基本粒子本身会溶解或分数化，揭示出一个由涌现粒子和涌现力组成的隐藏世界。我们将首先探讨DQCP的核心“原理与机制”，解析自旋子[分数化](@keyword=fractionalization|lang=zh-CN|style=Feynman)、[涌现规范场](@keyword=emergent_gauge_fields|lang=zh-CN|style=Feynman)以及竞争序之间深刻的对偶性等概念。随后，“应用与跨学科联系”一章将展示这些思想的深远影响，说明DQCP如何为理解[量子材料](@keyword=quantum_materials|lang=zh-CN|style=Feynman)、[拓扑物质](@keyword=topological_matter|lang=zh-CN|style=Feynman)乃至非传统超导电性提供了一个新的视角。

## 原理与机制

想象一下站在一个边界上。一边是一个完美有序的王国，一块磁性晶体，其中每个原子自旋都与其邻居的自旋方向相反，形成一种被称为**Néel序**的刚性棋盘格图案。另一边是另一个同样有序的领域，但性质完全不同。在这里，自旋配对成了惰性的、非磁性的双子，称为单重态，形成一种键的晶体图案——**[价键固体](@keyword=valence_bond_solid|lang=zh-CN|style=Feynman)（VBS）**。我们的直觉，乃至整个20世纪的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)理论框架都告诉我们，跨越这样的边界必然是一个剧烈的、不连续的事件。这就像试图将棋盘平滑地变形为一堵砖墙；如果不把东西打碎重来，你是不可能做到的。

### 一场禁戒的有序之舞

由Landau、Ginzburg和Wilson发展的、备受推崇的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)理论建立在**序参量**的概念之上。序参量是捕捉相的破缺对称性本质的数学对象——对于Néel磁体的自旋方向，是一个三分量矢量 $\mathbf{N}$；对于VBS的键图案，是一个二分量对象 $\mathbf{\Phi}$。Landau的框架告诉我们，要写下这两种序在[晶体对称性](@keyword=crystal_symmetry|lang=zh-CN|style=Feynman)支配下所有可能的相互作用方式。最简单、最强大的[相互作用项](@keyword=interaction_terms|lang=zh-CN|style=Feynman)耦合了它们大小的平方：$\lambda |\mathbf{N}|^2 |\mathbf{\Phi}|^2$。

如果[耦合系数](@keyword=coupling_coefficient|lang=zh-CN|style=Feynman) $\lambda$ 为正，这两种序会相互排斥；它们是竞争对手。系统将选择其中一种，它们之间的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)将是突然的一阶跃变。一个[连续相变](@keyword=continuous_phase_transitions|lang=zh-CN|style=Feynman)，即两种序在同一点上平稳地消失，需要精细调节多个参数才能到达一个特殊的“[多临界点](@keyword=multicritical_points|lang=zh-CN|style=Feynman)”。然而，无论是在看似合理的量子磁体的[计算机模拟](@keyword=computer_simulation|lang=zh-CN|style=Feynman)中，还是在理论模型中，我们都看到了诱人的证据，表明通过只调节*一个*参数，这种“禁戒”的[连续相变](@keyword=continuous_phase_transitions|lang=zh-CN|style=Feynman)就可能发生[@problem_id:2999163] [@problem_id:3012187]。这不仅仅是一个小难题；这是一场危机。它表明序参量 $\mathbf{N}$ 和 $\mathbf{\Phi}$ 并非这个临界舞台上的基本角色。真相必定更深邃、更奇特。

### 分裂自旋：内在世界

**[退禁闭量子临界性](@keyword=deconfined_quantum_criticality|lang=zh-CN|style=Feynman)**背后的革命性思想是，在[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，磁体中我们熟悉的激发——称为磁振子的自旋$1$波——不再是基本粒子。相反，它们会**分数化**。自旋$1$的磁振子分解为其组成部分：两个称为**自旋子**的自旋$\frac{1}{2}$[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)。

可以这样想：一个条形磁铁（一个偶极子，自旋$1$）可以看作一个北极和一个南极粘在一起。通常情况下，你无法分离出单个磁极。但如果，在某些极端的量子条件下，你可以呢？在[退禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)[量子临界点](@keyword=quantum_critical_point|lang=zh-CN|style=Feynman)（DQCP），类似的事情发生在自旋本身上。携带正常磁振子一半自旋的自旋子，作为自由实体出现。

分数化这一行为并非没有后果。当[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman) $z_\alpha$（其中$\alpha$可以是‘上’或‘下’）出现时，它们揭示了一种一直以来将它们束缚在一起的隐藏相互作用：一个**[涌现规范场](@keyword=emergent_gauge_fields|lang=zh-CN|style=Feynman)** $a_\mu$。这个场不是我们宇宙中熟悉的[电磁场](@keyword=electromagnetic_field|lang=zh-CN|style=Feynman)；它是一种只存在于量子磁体内部的私有力，只作用于[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)。自旋子在这种涌现场下带“[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)”，而该场的“[光子](@keyword=photon|lang=zh-CN|style=Feynman)”则在它们之间传递力。

整个[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)的复杂戏剧可以被提炼成一个惊人简单而优雅的场论，一种三维[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中的[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)[量子电动力学](@keyword=quantum_electrodynamics|lang=zh-CN|style=Feynman)（$QED_3$）[@problem_id:3012634]：

$$
\mathcal{L}_{\text{critical}} = \sum_{\alpha=1}^{2} |(\partial_{\mu} - i a_{\mu}) z_{\alpha}|^2 + u \left( \sum_{\alpha=1}^{2} |z_{\alpha}|^2 \right)^2 + \frac{1}{2e^2} (\epsilon_{\mu\nu\rho} \partial_{\nu} a_{\rho})^2
$$

这个方程是[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)涌现宇宙的宪法。它描述了两种味的玻色自旋子（$z_\alpha$）通过涌现U(1)[规范场](@keyword=gauge_fields|lang=zh-CN|style=Feynman)（$a_\mu$）相互作用，而[规范场](@keyword=gauge_fields|lang=zh-CN|style=Feynman)的动力学由一个类Maxwell项决定。“[退禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)”一词现在有了精确的含义：在这个[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，自旋子是自由粒子，不受涌现力的约束。

### 现实的对偶性：粒子凝聚 vs. 场冻结

如果[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)是一个[退禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)的世界，那么两边的两个相又是什么呢？用这种新语言来说，Néel序和VBS序被揭示为系统逃离这个[临界状态](@keyword=critical_state|lang=zh-CN|style=Feynman)的两种不同的、*对偶*的方式。它们是同一枚硬币的两面，是涌现宇宙的两种命运。

1.  **Néel相：[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)的凝聚体。** 如果我们将系统调谐到Néel相，[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)本身会发生玻色-爱因斯坦凝聚。它们全部落入同一个[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，建立起一种相干的[长程有序](@keyword=long_range_order|lang=zh-CN|style=Feynman)。在这种自旋子语言中，Néel序参量仅仅是[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)场的复合：$\mathbf{N} \propto z^\dagger \boldsymbol{\sigma} z$ [@problem_id:3012187]。当[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)（$\langle z_\alpha \rangle \neq 0$）凝聚时，它们通过[Anderson-Higgs机制](@keyword=anderson_higgs_mechanism|lang=zh-CN|style=Feynman)赋予涌现[光子质量](@keyword=photon_mass|lang=zh-CN|style=Feynman)。涌现力变为[短程力](@keyword=short_range_forces|lang=zh-CN|style=Feynman)，[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)再次被禁闭成传统的自旋$1$[磁振子](@keyword=magnons|lang=zh-CN|style=Feynman)。VBS序的“幽灵”仍然存在，但其关联性在一个由规范[光子质量](@keyword=photon_mass|lang=zh-CN|style=Feynman)决定的短距离上呈指数衰减[@problem_id:86452]。

2.  **VBS相：[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)的晶体。** VBS相的命运则奇异得多。在这里，[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)保持有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)和无序状态。取而代之的是，系统凝聚了[涌现规范场](@keyword=emergent_gauge_fields|lang=zh-CN|style=Feynman)中的**拓扑缺陷**。在(2+1)维[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中，U(1)规范场的基本点状缺陷是**[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)**——[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中的一个点，规范通量在此处产生或消失。VBS相是这些磁单极子本身凝聚成晶体的状态。这个[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)凝聚体使[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)凝聚体无序（就像[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)一样），并在对偶意义上，它禁闭了自旋子。想象一下，一个[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)和一个反[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)之间的涌现“电”[场线](@keyword=field_lines|lang=zh-CN|style=Feynman)，被凝聚的[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)海洋挤压成一根禁闭管。因此，VBS序参量$\mathbf{\Phi}$正是产生[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)的算符[@problem_id:3012187]。

DQCP是*既非*[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)*也非*[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)凝聚的刀锋[平衡点](@keyword=equilibrium_points|lang=zh-CN|style=Feynman)。它是一锅翻滚的两者混合的量子汤，一个具有最大复杂性和自由度的状态。

### [退禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)的规则

为什么这样一个精妙的状态会存在呢？为什么磁单极子不立即凝聚并禁闭一切？答案在于[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)和磁单极子之间的一场宇宙之战，这场战斗由[重整化群](@keyword=renormalization_group|lang=zh-CN|style=Feynman)的规则所支配。

像磁单极子这样的算符改变系统命运的能力，由其**标度维** $\Delta$ 来衡量。在$d=3$维[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中，如果$\Delta < 3$，算符是**相关的**并且其重要性会增长，将系统驱动到一个新的相中。如果$\Delta > 3$，它是**无关的**并且会逐渐消失。在[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，稳定性要求磁单极子算符是无关的。用[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)“逸度”$\lambda$来微扰系统会将其驱动到VBS相，打开一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)并产生一个有限的关联长度$\xi$，其标度关系为 $\xi \sim \lambda^{-1/(3 - \Delta_M)}$ [@problem_id:52168]，这显示了一个[相关算符](@keyword=relevant_operators|lang=zh-CN|style=Feynman)如何破坏临界性。

[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)会反击。无能隙的带电物质（[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)）的存在会屏蔽[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)并增加它们的标度维。一个著名的大-$N$近似结果表明，带[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)$q$的磁单极子的标度维随自旋子味道数$N$的增加而增长：$\Delta_q \propto N q^2$ [@problem_id:295408]。如果$N$足够大，[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)可以赢得这场战斗，使[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)变得无关，从而稳定[退禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)。

但这里出现了最美妙的转折，一个来自底层[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的信息。方格[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的微观对称性对涌现世界起着强大的“[选择定则](@keyword=selection_rules|lang=zh-CN|style=Feynman)”的作用[@problem_id:3017395]。它们规定了哪些[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)算符是真正允许存在的。对于方格[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)上的自旋$\frac{1}{2}$系统，这些对称性禁戒了最基本的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为$q=1$和$q=2$的[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)。第一个满足所有[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)对称性的[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)是[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为$q=4$的那个！[@problem_id:3012187]。由于磁单极子导致禁闭的能力对于更高[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)会减弱（$\Delta_q \propto q^2$），[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)本身就在[合力](@keyword=net_force|lang=zh-CN|style=Feynman)促成[退禁闭](@keyword=deconfinement|lang=zh-CN|style=Feynman)变得更加可能，即使对于物理上相关的$N=2$个[自旋子](@keyword=spinons|lang=zh-CN|style=Feynman)味道的情况也是如此。

### 更高的统一性

也许这个理论最深刻的结果是在[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)涌现出一个完全意想不到的、更大的对称性。远离[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)时，三分量的Néel矢量$\mathbf{N}$和二分量的VBS序$\mathbf{\Phi}$显然是不同的。但当我们接近DQCP时，它们之间的界限变得模糊。

值得注意的是，有证据表明，在[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，这两个序参量合并成一个单一的五分量“超自旋”矢量$(\mathbf{N}, \mathbf{\Phi})$。该理论发展出一种涌现的**SO(5)对称性**，可以自由地将Néel分量旋转成VBS分量，反之亦然[@problem_id:2999163]。这是一个惊人的发现。这两个看似破坏了完全不相关对称性的相，在[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)被统一到一个单一的、更大的结构中。这就像，用量子显微镜观察棋盘和砖墙之间的边界时，我们发现它们只是同一个更高维物体投下的两个不同阴影，而这个物体只有在[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)的火焰中才可见。这种涌现的统一性是[退禁闭量子临界性](@keyword=deconfined_quantum_criticality|lang=zh-CN|style=Feynman)的最终标志，是量子世界深刻而常常隐藏的美的证明。