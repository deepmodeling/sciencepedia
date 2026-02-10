## 应用与跨学科联系

现在我们已经熟悉了[电子哈密顿量](@keyword=electronic_hamiltonian|lang=zh-CN|style=Feynman)的机制——它的动能项，它那错综复杂的库仑吸引和排斥网络——你可能会有一种……孤立感。到目前为止，我们一直在讨论处于完美、寂静真空中的分子，不受宇宙其他部分的影响。这是物理学家的天堂，却是化学家或生物学家的荒漠！真实世界是一个充满各种场、拥挤的溶剂分子和巨大重[复结构](@keyword=complex_structure|lang=zh-CN|style=Feynman)的美妙而混乱的地方。

[电子哈密顿量](@keyword=electronic_hamiltonian|lang=zh-CN|style=Feynman)真正的力量和美妙之处并不在于其原始、理想化的形式，而在于其令人难以置信的适应性。它不是僵化的教条，而是一种灵活的语言。通过仔细地添加新的项——为其语法结构添加新的“从句”——我们可以教会它描述一系列惊人的真实世界现象。把基础哈密顿量想象成汽车的底盘。这是一个很好的开始，但要越野、在雨中航行或承载重物，你需要添加特殊的轮胎、雨刮器和强大的发动机。在本章中，我们将探讨如何为我们的哈密顿量添加这些“功能”，将其从一个理论上的好奇之物转变为一个强大的工具，将量子力学与几乎所有物理科学分支联系起来。

### 响应环境：电场和磁场中的分子

当我们将分子从安静的真空中取出，并将其置于外场中时，会发生什么？宇宙中充满了[电场和磁场](@keyword=electric_and_magnetic_fields|lang=zh-CN|style=Feynman)，而分子作为[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的集合，必须对此作出响应。我们描述这种响应的方式非常简单：我们只需在哈密顿量中增加一个新的势能项。

想象一下将一个分子置于均匀电场 $\mathbf{E}$ 中。这个场会试图将正电的原子核向一个方向拉，而将负电的电子向另一个方向拉。这种相互作用具有相关的势能。在[经典物理学](@keyword=classical_physics|lang=zh-CN|style=Feynman)中，偶极矩 $\boldsymbol{\mu}$ 在电场中的能量是 $-\boldsymbol{\mu} \cdot \mathbf{E}$。在量子世界里，我们只需将其转化为一个算符。分子的总偶极矩有一部分来自固定的原子核，另一部分是来自可移动电子的算符部分。所以，我们在哈密顿量中增加一个类似 $-\mathbf{E} \cdot (\hat{\boldsymbol{\mu}}_e + \boldsymbol{\mu}_N)$ 的项 [@problem_id:2822971]。电子现在感受到这个新的势，它们的位置会发生轻微移动，扭曲它们的概率云。这种扭曲改变了分子的能量和[感应偶极矩](@keyword=induced_dipole_moment|lang=zh-CN|style=Feynman)，这种现象我们称之为[极化率](@keyword=polarizability|lang=zh-CN|style=Feynman)。通过研究能级随场的变化（[斯塔克效应](@keyword=stark_effect|lang=zh-CN|style=Feynman)），我们可以以极高的精度探测分子的[电子结构](@keyword=electronic_structure|lang=zh-CN|style=Feynman)。

对于外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $\mathbf{B}$，情况大致相同。电子不仅仅是一个[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)；它还是一个微小的自旋磁体，其轨道运动也会产生磁矩。哈密顿量必须被教会这些磁性性质。[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)主要引入两个新项 [@problem_id:2465196]。第一个，通常称为塞曼项，将场 $\mathbf{B}$ 直接与电子的轨道和自旋角动量算符耦合。这个项负责能级的分裂，这一现象是两项最强大的科学分析技术的基石：[核磁共振](@keyword=nuclear_magnetic_resonance|lang=zh-CN|style=Feynman)（NMR）[光谱学](@keyword=spectroscopy|lang=zh-CN|style=Feynman)，它描绘了分子中原子的化学环境；以及[电子顺磁共振](@keyword=electron_paramagnetic_resonance|lang=zh-CN|style=Feynman)（EPR）[光谱学](@keyword=spectroscopy|lang=zh-CN|style=Feynman)。第二个项与 $B^2$ 成正比，它引起了[抗磁性](@keyword=diamagnetism|lang=zh-CN|style=Feynman)，即所有物质普遍具有的对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的微弱排斥性。

在这两种情况下，原理是相同的。哈密顿量就像我们的能量账本。如果出现新的相互作用，我们只需将其添加到账本中。然后，薛定谔方程会告诉我们系统如何重新[排列](@keyword=permutation|lang=zh-CN|style=Feynman)自身以适应这个新的现实。

### 添加更精细的细节：[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)的作用

我们的标准哈密顿量是非[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)性的；它对Einstein的宇宙一无所知。在许多情况下，特别是对于轻元素，这是一个完全可以接受的近似。但现实是[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)性的，有时这些微妙的效应变得至关重要。其中最重要的之一是[自旋-轨道耦合](@keyword=l_s_coupling|lang=zh-CN|style=Feynman)。

一个电子在原子核和其他电子的电场中运动时，从它自己的角度来看，会把这个场体验为一个[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。这个内部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)随后与电子自身的内禀[自旋磁矩](@keyword=spin_magnetic_moment|lang=zh-CN|style=Feynman)相互作用。这种自我相互作用被称为自旋-轨道耦合。为了解释它，我们必须在哈密顿量中再增加一个新项，一个明确地将电子的[自旋算符](@keyword=spin_operators|lang=zh-CN|style=Feynman) $\mathbf{S}$ 与其轨道角动量算符 $\mathbf{L}$ 耦合的项。这种耦合不仅仅是一个单一的项；它包括与核场的主要单电子相互作用，也包括更微妙的双[电子项](@keyword=electronic_terms|lang=zh-CN|style=Feynman)，其中一个电子的运动产生的场会影响另一个电子的自旋 [@problem_id:2464225]。

这种效应可能看起来很深奥，但它具有深远的化学后果。它导致了原子光谱线的[精细结构分裂](@keyword=fine_structure_splitting|lang=zh-CN|style=Feynman)。在含有重原子的分子中，电子的运动速度可以达到光速的一个可观比例，[自旋-轨道耦合](@keyword=l_s_coupling|lang=zh-CN|style=Feynman)效应巨大，甚至可以决定分子的几何构型和反应性。即使在有机分子中，它也为“自旋禁戒”过程提供了一条途径，例如在[单重态和三重态](@keyword=singlet_and_triplet_states|lang=zh-CN|style=Feynman)电子态之间切换，这是许多[光化学反应](@keyword=photochemical_reactions|lang=zh-CN|style=Feynman)中的关键步骤，也是磷光等现象的基础。

### 驯服野兽：计算近似的艺术

如果你一直跟读到这里，你会意识到“完整”的哈密顿量是一个极其复杂的对象。对于像苯（$\mathrm{C}_6\mathrm{H}_6$）这样的简单分子，我们有42个电子！用一个包含所有42个电子位置的哈密顿量来求解薛定谔方程在计算上是不可能的，而且幸运的是，也是不必要的。[计算化学](@keyword=computational_chemistry|lang=zh-CN|style=Feynman)的艺术不仅仅在于原始的计算能力，更在于做出明智的近似。

第一个也是最重要的近似是[芯-价分离](@keyword=core_valence_separation|lang=zh-CN|style=Feynman)。考虑氢化铍 $\mathrm{BeH}_2$。铍原子有四个电子：两个在深层的 $1s$ 芯层轨道，两个在 $2s$ 价层轨道。$1s$ 电子被极紧地束缚在原子核上，处于一个狭小、紧凑的空间区域。激发它们所需的能量与典型的化学键能相比是巨大的。当Be原子与两个氢原子形成键时，是价电子在做所有的工作——重新[排列](@keyword=permutation|lang=zh-CN|style=Feynman)自己以形成[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)。芯层电子在很大程度上是惰性的旁观者 [@problem_id:2464248]。

这种物理洞察力带来了一个绝妙的计算捷径：有效芯势（ECP）或赝势。我们不再处理裸核强大的、奇异的吸引力以及与惰性芯电子的复杂相互作用，而是用一个只作用于价电子的、更平滑的单一有效势来取代整个原子实。这有两个巨大的好处。首先，它极大地减少了我们需要显式处理的电子数量。其次，它移除了靠近原子核的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)中尖锐、快速变化的部分，这在数学上是很难描述的。现代的ECP是复杂的算符，通常对价电子的不同角动量（$s, p, d, \dots$）有不同的势，并且其构建是为了确保赝原子具有与真实原子相同的化学性质 [@problem_id:2887798]。对于重元素，像质量-速度修正甚至[自旋-轨道耦合](@keyword=l_s_coupling|lang=zh-CN|style=Feynman)这样的[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)效应可以被隐式地“折叠”到ECP的构建中，为我们提供了一种计算上廉价的方式来处理这些原本具有挑战性的物理效应。

### 一种适用于所有科学的语言：跨学科的哈密顿量

[电子哈密顿量](@keyword=electronic_hamiltonian|lang=zh-CN|style=Feynman)的最终力量体现在它能够超越物理和化学的界限，为理解所有形式的物质提供一种语言。

**从真空到烧杯：** 大多数[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)不是在真空中发生，而是在溶液中。周围的溶剂分子不断地撞击和电极化溶质。我们的哈密顿量如何解释这个由数万亿分子组成的复杂环境？一种强大的方法是[可极化连续介质模型](@keyword=polarizable_continuum_model|lang=zh-CN|style=Feynman)（PCM）。我们用一个包围在溶质[空腔](@keyword=hohlraum|lang=zh-CN|style=Feynman)周围的连续介电介质来代替显式的溶剂分子。溶质自身的[电荷分布](@keyword=charge_distribution|lang=zh-CN|style=Feynman)会极化这个介质，介质反过来会产生一个“[反应场](@keyword=reaction_field|lang=zh-CN|style=Feynman)”作用回溶质。这个[反应场](@keyword=reaction_field|lang=zh-CN|style=Feynman)作为一个新的一电子势被添加到哈密顿量中。因为[反应场](@keyword=reaction_field|lang=zh-CN|style=Feynman)依赖于电子密度，而电子密度又依赖于薛定谔方程的解，所以这个问题必须自洽地求解，直到电子云和溶剂的极化彼此达到平衡 [@problem_id:2465191]。这使我们能够计算分子在真实环境中的性质，这是连接理论与实验的关键一步。

**生命的尺度：** 我们如何才能模拟一个酶，一个由数千个原子组成的蛋白质，其中[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)发生在一个微小的[活性位点](@keyword=active_site|lang=zh-CN|style=Feynman)？用量子力学处理整个系统是不可能的。在这里，我们看到了量子世界和经典世界在所谓的QM/MM（[量子力学/分子力学](@keyword=quantum_mechanics_molecular_mechanics|lang=zh-CN|style=Feynman)）方法中的完美结合。我们对系统进行划分。小的、化学活跃的区域——酶的“业务端”——用完整的量子[电子哈密顿量](@keyword=electronic_hamiltonian|lang=zh-CN|style=Feynman)（$\hat{H}_{\text{QM}}$）处理。广阔的蛋白质和周围水分子的其余部分则使用更简单的经典力学定律来处理，如同带有静[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的球和弹簧（$U_{\text{MM}}$）。然后，这两个区域通过一个描述它们静电和[范德华相互作用](@keyword=van_der_waals_interactions|lang=zh-CN|style=Feynman)的相互作用项（$\hat{V}_{\text{QM/MM}}$）耦合起来 [@problem_id:2872877]。这种混合方法使我们能够将昂贵的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)能力精确地集中在需要的地方，从而使得模拟真实生物环境中的[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)成为可能。

**有序的材料世界：** 一个分子是有限的；而一个晶体，实际上是无限的。我们如何为[晶体固体](@keyword=crystalline_solids|lang=zh-CN|style=Feynman)写一个哈密顿量？我们利用晶体的周期性。我们定义一个包含一组原子的晶胞，然后想象它在所有方向上无限重复。哈密顿量因此不仅必须包括[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)内粒子之间的相互作用，还必须包括每个粒子与整个[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中所有其他粒子的所有周期性镜像之间的相互作用。这导致了必须使用像[Ewald求和](@keyword=ewald_summation|lang=zh-CN|style=Feynman)这样的数学技术小心处理的无限求和 [@problem_id:2475257]。这种周期性哈密顿量是所有现代固态物理学和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)的起点，使我们能够计算[固体的能带结构](@keyword=band_structure_of_solids|lang=zh-CN|style=Feynman)，从而决定它是金属、绝缘体还是[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)。

**超导之舞：** 即使是完美、静态晶体的哈密顿量也是一种理想化。固体中的真实原子在不断[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。这些量子化的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)被称为[声子](@keyword=phonons|lang=zh-CN|style=Feynman)。当我们的电子与这些[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)相互作用时会发生什么？我们必须再次扩充我们的哈密顿量，为[声子](@keyword=phonons|lang=zh-CN|style=Feynman)场本身的能量添加项，以及一个描述电子吸收或发射[声子](@keyword=phonons|lang=zh-CN|style=Feynman)的关键的[电子-声子耦合](@keyword=electron_phonon_coupling|lang=zh-CN|style=Feynman)项 [@problem_id:2464246]。这种相互作用是有限温度下电阻的起源。但在适当的条件下，它可以做一些神奇的事情。一个电子可以使[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)畸变（发射一个[声子](@keyword=phonons|lang=zh-CN|style=Feynman)），而远处的第二个电子可以被这个畸变所吸引（吸收该[声子](@keyword=phonons|lang=zh-CN|style=Feynman)）。这在两个电子之间产生了一种有效的、间接的吸引力，克服了它们之间的[库仑排斥](@keyword=coulomb_repulsion|lang=zh-CN|style=Feynman)。这种[声子介导的吸引](@keyword=phonon_mediated_attraction|lang=zh-CN|style=Feynman)力将电子束缚成“[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)”，然后它们可以无阻力地穿过[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。哈密顿量，一旦扩展到包含[声子](@keyword=phonons|lang=zh-CN|style=Feynman)，就包含了常规超导性的秘密。

从单个分子对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的响应，到引起超导性的电子与[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)的集体交响乐，[电子哈密顿量](@keyword=electronic_hamiltonian|lang=zh-CN|style=Feynman)证明了自己是一个普适且极其优美的理论框架。它是原子和分子量子世界的[主方程](@keyword=master_equation|lang=zh-CN|style=Feynman)，是一个通过独创性和洞察力，让我们能够将物理学的基本定律与我们周围看到的复杂而宏伟的现实联系起来的工具。