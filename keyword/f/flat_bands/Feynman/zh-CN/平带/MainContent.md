## 引言
在[晶体固体](@keyword=crystalline_solids|lang=zh-CN|style=Feynman)的量子世界中，电子并非完全自由地运动。它们被允许的能量被限制在称为[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的特定范围内，这些[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)决定了材料的电子性质。通常，这些[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)是弯曲的，意味着电子的能量随其动量而变化。但如果一个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)是完全平坦的呢？在这种奇异的情景下，能量变得与动量无关，这从根本上改变了电子的行为，实际上使它们陷入静止。本文探讨了[淬灭](@keyword=quenching|lang=zh-CN|style=Feynman)这种电子动能所带来的深远后果，这一知识领域填补了简单[能带理论](@keyword=electronic_band_theory|lang=zh-CN|style=Feynman)与[强关联物理](@keyword=strongly_correlated_physics|lang=zh-CN|style=Feynman)复杂领域之间的空白。

首先，在“原理与机制”部分，我们将剖析这些静态电子波的构造，定义它们的零群速度和无限大[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)。我们将探索特定的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)几何结构，如Kagome[晶格和](@keyword=lattice_sums|lang=zh-CN|style=Feynman)[Lieb晶格](@keyword=lieb_lattice|lang=zh-CN|style=Feynman)，如何利用[相消干涉](@keyword=destructive_interference|lang=zh-CN|style=Feynman)来束缚电子并产生这些[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)。随后，“应用与跨学科联系”部分将揭示为何这些体系如此激动人心。通过抑制动能，我们放大了[电子-电子相互作用](@keyword=electron_electron_interactions|lang=zh-CN|style=Feynman)的效应，为[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)铁磁性和高温超导等奇异物态搭建了舞台，并揭示了其与[计算化学](@keyword=computational_chemistry|lang=zh-CN|style=Feynman)、[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)等领域之间出人意料的联系。

## 原理与机制

想象一个电子在晶体完美的有序原子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中移动。它不像是在光滑地板上滚动的弹珠，而是一个量子力学波，是量子场中的一个涟漪，在穿过重复的原子阵列时会发生衍射和干涉。这些电子波被允许的能量不是连续的，而是形成了独特的**[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)**。对于我们所熟知的大多数材料——我们电线中的铜，芯片中的硅——这些[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)都有明确的形状。电子的能量 $E$ 随着其[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)动量 $\vec{k}$ 的变化而变化。这种关系 $E(\vec{k})$ 被称为色散关系。你可以把它想象成电子在其中穿行的一个由山丘和山谷构成的景观。陡峭的斜坡意味着电子移动得快；平缓的斜坡则意味着它移动得慢。但如果我们在这一景观中发现了一个完全、绝对平坦的地方呢？

### 静态波的剖析

让我们想象一下这种奇异的情景。我们有一个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)，其中能量 $E(\vec{k})$ 只是一个常数，我们称之为 $E_0$，完全独立于电子的动量 $\vec{k}$。这就是**完美平带**的定义。这对电子本身意味着什么？其后果既简单又深刻。

首先，让我们问问电子移动的速度有多快。在波动力学中，[波包](@keyword=wave_packets|lang=zh-CN|style=Feynman)的速度不是由其[相速度](@keyword=phase_velocity|lang=zh-CN|style=Feynman)给出，而是由其**[群速度](@keyword=group_velocity|lang=zh-CN|style=Feynman)** $\vec{v}_g$ 给出。这个量告诉我们能量如何随[动量变化](@keyword=change_in_momentum|lang=zh-CN|style=Feynman)，这个概念应该感觉很直观——它就是[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman)的斜率。其公式非常简洁：$\vec{v}_g = \frac{1}{\hbar} \nabla_{\vec{k}} E(\vec{k})$，其中 $\hbar$ 是约化普朗克常数，$\nabla_{\vec{k}}$ 是对动量的梯度。如果[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)是平坦的，$E(\vec{k})$ 是一个常数，所以它的梯度处处为零。这意味着[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)中电子的群速度恒等于零 [@problem_id:1814088]。电子无处可去。它是一种本质上静止的波。

当我们考虑电子的质量时，事情变得更加奇怪。在晶体中，电子的行为并不像它拥有通常的静止质量。相反，它有一个**有效质量** $m^*$，描述了它如何响应力。如果你推一个电子，它会加速多少？这取决于[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的曲率，由能量对动量的二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)给出。[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)通过关系式 $(m^*)^{-1} \propto \frac{\partial^2 E}{\partial k^2}$ 定义。对于一个正常的弯曲能带，这会得到一个有限的质量。但对于[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)来说，曲率为零。这意味着有效质量的倒数为零，这只能说明一件事：**有效质量是无限大**的！

想想这意味着什么。要加速一个质量无限大的物体，你需要无限大的力。[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)中的电子是终极的顽固物体。你可以用电场推它，但它根本不会动。这种深刻的惯性是**空间局域化**的标志。尽管底层的电子态（[布洛赫波](@keyword=bloch_waves|lang=zh-CN|style=Feynman)）遍布整个晶体，但电子本身却被钉住，困在原地。

所以，平带是[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)的集合，它们共同作用，创造出具有无限惯性的固定电子。这听起来像是理论家白日梦里的东西。自然界怎么可能构建出这样的东西？事实证明，答案不在于某种奇异的力，而在于几何学的简单之美。

### 利用几何结构束缚电子的艺术

为了理解[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)如何能够束缚电子，我们可以使用一个简单而强大的图景，称为**[紧束缚模型](@keyword=tight_binding_model|lang=zh-CN|style=Feynman)**。想象电子存在于原子上，并有一定概率“跃迁”到相邻的原子上。电子的能量取决于它能采取的所有可能路径。有时，不同路径的量子力学波会相加（[相长干涉](@keyword=constructive_interference|lang=zh-CN|style=Feynman)），有时它们会抵消（相消干涉）。[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)正是诞生于一次完美的[相消干涉](@keyword=destructive_interference|lang=zh-CN|style=Feynman)。

让我们看看**Kagome[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)**，这是一种由共角三角形构成的令人惊叹的二维图案，就像传统的日本编织篮图案。如果我们考虑电子在最近邻格点之间跃迁，能量成本为 $-t$，我们会发现一件了不起的事情。存在一种特殊状态，其中电子可以被完美地限制在[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的单个六边形格子内 [@problem_id:436485]。通过将[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在六边形的六个格点上设置为交替符号（+1, -1, +1, -1, +1, -1），就达到了一种精妙的平衡。对于这些格点上的任何一个电子，来自其在六边形上的两个相邻原子的量子“拉力”都完美地相互抵消。电子被困住了。由于这个束缚态是局域的，不与[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的其余部分通信，它的能量不依赖于任何长程波长，也就是说，它与[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)动量 $\vec{k}$ 无关。对于这种特定的几何结构，该平带的能量固定在 $E = \epsilon_0 + 2t$，其中 $\epsilon_0$ 是电子在不发生跃迁时位于原子上的能量 [@problem_id:1138685]。

这种“[几何阻挫](@keyword=geometric_frustration|lang=zh-CN|style=Feynman)”原理并非Kagome[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)所独有。另一个美丽的例子是**[Lieb晶格](@keyword=lieb_lattice|lang=zh-CN|style=Feynman)**，它看起来像一个方形网格，在每条边的中间都有额外的原子 [@problem_id:1210302]。这个[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)每个[原胞](@keyword=primitive_unit_cell|lang=zh-CN|style=Feynman)有三个格点，但它们并不都等价。“角”格点与四个邻居相连，而“边心”格点只与两个邻居相连。这种不平衡是关键。[Lieb晶格](@keyword=lieb_lattice|lang=zh-CN|style=Feynman)中的平带态以一种巧妙的方式构建，使得它们在所有角格点上的振幅都为零。它们只存在于连接较少的边心格点上，这再次导致一种[相消干涉](@keyword=destructive_interference|lang=zh-CN|style=Feynman)，从而局域化电子。在这种情况下，[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)的能量就是它所占据的格点的在位能，$E = \epsilon_B$。

### 一条不平衡的法则

[Lieb晶格](@keyword=lieb_lattice|lang=zh-CN|style=Feynman)的例子指向了一条极其普遍的法则。许多拥有平带的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)可以被归类为**二分[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)**。这意味着我们可以用两种颜色，比如A（红色）和B（蓝色），来为[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)格点着色，使得任何A格点只与B格点相连，反之亦然。方形[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)是二分的；三角形[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)则不是。

现在，如果A格点的数量 $N_A$ 与B格点的数量 $N_B$ 不同呢？假设我们的A格点比B格点多。在电子只从A跃迁到B的[紧束缚模型](@keyword=tight_binding_model|lang=zh-CN|style=Feynman)中，每个B格点只能与一定数量的A格点“配对”。如果存在不平衡，必然会有一些A格点态剩下，没有B格点伙伴可以跃迁过去。这些“未配对”的态就是[零能模式](@keyword=zero_energy_mode|lang=zh-CN|style=Feynman)。它们注定存在于零能量，因为它们无处可去。事实证明，每个原胞中将恰好有 $|N_A - N_B|$ 个这样的态 [@problem_id:1138737]。这些态形成了一个位于零能量的完美平带！这个强大的结果将平带的存在直接与[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)本身的拓扑和连通性联系起来。它给了我们一个设计原则：如果你想要一个[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)，就构建一个在两个子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中格点数量不等的二分[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。

### 静止的后果

我们已经确定，[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)容纳了大量局域化的、固定的电子，它们都处于完全相同的能量上。这种奇特的情况对材料的物理性质有着巨大的影响。

首先，考虑**[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)（DOS）** $g(E)$，它计算在给定能量下可用的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)数量。对于具有[色散](@keyword=frequency_dispersion|lang=zh-CN|style=Feynman)的正常[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)，态分布在一个能量范围内，[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)通常是一个平滑的函数。对于[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)，整个布里渊区中对应于每个可能动量 $\vec{k}$ 的所有态都堆积在单一能量 $E_{\text{flat}}$ 上。这在态密度中产生了一个无限尖锐的峰。在数学上，它的贡献是一个**[狄拉克δ函数](@keyword=dirac_delta_function|lang=zh-CN|style=Feynman)**：$g(E) = \delta(E - E_{\text{flat}})$ [@problem_id:1826683]。无限的态密度是[电子不稳定性](@keyword=electronic_instability|lang=zh-CN|style=Feynman)的温床。在某个精确能量上有如此多的态可供占据，即使是电子之间微弱的相互作用也能产生巨大的影响，比如导致它们自发地有序化为磁性或超导相。

其次，关于[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)呢？一个部分填充了[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的材料通常是金属。[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)附近的电子可以自由移动并携带电流。但如果我们有一个部分填充的*平*带会发生什么？我们有载流子，但它们是局域化的。它们的[群速度](@keyword=group_velocity|lang=zh-CN|style=Feynman)为零，[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)为无穷大。你可能已经猜到，它们不能携带常规电流。这可以通过**[Drude权重](@keyword=drude_weight|lang=zh-CN|style=Feynman)** $D$ 来量化，它衡量了电导率中理想的、无耗散的部分。对于正常金属，$D$ 是正的。对于[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)位于[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)中的系统，[Drude权重](@keyword=drude_weight|lang=zh-CN|style=Feynman)恰好为零 [@problem_id:1199572]。即使它拥有一个部分填充的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)，该系统也是一个绝缘体！

这就是[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)的核心魔力：**动能被淬灭**。电子已经放弃了移动。这种对其通常不息运动的完全抑制改变了游戏规则。在大多数材料中，电子的动能是巨大的，而它们之间的静电排斥只是一个相对较小的修正。但在[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)中，动能项消失了。突然之间，无论电子之间的相互作用多么微弱，都占据了中心舞台。物理学不再是关于单个电子四处跃迁；而是关于许多电子试图最小化其排斥力的集体、关联的舞蹈。这是通往**[强关联电子体系](@keyword=strongly_correlated_electron_systems|lang=zh-CN|style=Feynman)**奇异世界的大门，在那里，[高温超导](@keyword=high_temperature_superconductivity|lang=zh-CN|style=Feynman)和分数[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)等现象可以涌现。

### 脆弱的完美

这些[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)是自然界中一个稳健的特征，还是一个脆弱的理想化？真相一如既往，介于两者之间。我们所讨论的完美平坦性通常依赖于一种完美的抵消，例如，它假设电子只能跃迁到它们的最近邻。

考虑**[烧绿石晶格](@keyword=pyrochlore_lattice|lang=zh-CN|style=Feynman)**，这是一种由共角四面体构成的三维结构。如果只有最近邻跃迁（$t_1$），它会展现出两个完美的[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)。但如果我们允许电子有很小的概率进行稍长一点的跳跃，到达其次近邻（$t_2$）呢？这个微小的改变引入了新的跃迁路径。完美的[相消干涉](@keyword=destructive_interference|lang=zh-CN|style=Feynman)被破坏了。[平带](@keyword=flat_bands|lang=zh-CN|style=Feynman)“活了过来”，并获得了[色散](@keyword=frequency_dispersion|lang=zh-CN|style=Feynman)；它的能量现在依赖于动量 [@problem_id:248045]。完美被打破了。

这告诉我们，完美的平坦性是一个微妙的极限。然而，即使只是“近乎平坦”的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)也能继承其理想化表亲的壮观物理特性。只要动能被强烈抑制，即使不是完全为零，电子之间的相互作用仍然可以占主导地位，并导致大量迷人的物理现象。寻找平带材料的探索，就是寻找那些我们可以刻意将电子动能调低至微弱低语的体系，从而让我们能够听到它们量子关联那微弱而美妙的乐章。