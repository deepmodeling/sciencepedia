## 引言
[激子](@keyword=excitons|lang=zh-CN|style=Feynman)，作为固态物质中由电子与空穴构成的基本[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)，是理解[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)与光相互作用的核心概念。然而，将其仅仅看作一个简单的束缚对，远不足以揭示其背后丰富而深刻的物理内涵。为了真正掌握激子的本质，我们必须回答一系列更深层次的问题：它的行为遵循哪些基本法则？它如何根据所处的环境改变其“形态”？它又是如何从单个粒子的行为演化出复杂的集体现象，并在[光电子学](@keyword=optoelectronics|lang=zh-CN|style=Feynman)、能源科学乃至量子技术中扮演关键角色的？

本文旨在系统性地构建一幅关于[激子](@keyword=excitons|lang=zh-CN|style=Feynman)的完整物理图像。我们将从第一章“原理与机制”开始，通过“固态氢原子”这一优雅的类比，深入探讨决定[激子](@keyword=excitons|lang=zh-CN|style=Feynman)基本属性的物理因素，并介绍其Wannier-Mott和Frenkel两种主要类型，以及其内部[自旋结构](@keyword=spin_structures|lang=zh-CN|style=Feynman)和[多体相互作用](@keyword=many_body_interaction|lang=zh-CN|style=Feynman)。接着，在第二章“应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系”中，我们将走出理论的殿堂，探索激子在OLED、太阳能电池、量子点和[谷电子学](@keyword=valleytronics|lang=zh-CN|style=Feynman)等前沿科技中的实际应用，揭示它如何连接起物理、化学与[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)。最后，在第三章“动手实践”中，您将通过解决具体问题，将理论知识应用于实际计算，从而加深对激子物理的理解。

现在，让我们开始这趟旅程，首先深入激子的内部，探索其行为的法则与其精妙的舞蹈机制。

## 原理与机制

在上一章中，我们邂逅了激子——固态物质中一种令人着迷的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)。但这仅仅是一个开始。为了真正地理解[激子](@keyword=excitons|lang=zh-CN|style=Feynman)的本质，我们必须深入其内部，探索其行为的法则，并欣赏它与周围世界互动的精妙舞蹈。这趟旅程，我们将像物理学家那样，从最简单的模型出发，一步步地构建起一幅完整而生动的[激子](@keyword=excitons|lang=zh-CN|style=Feynman)图像。

### “固态氢原子”：一个优雅的类比

想象一下，当一束[光子](@keyword=photon|lang=zh-CN|style=Feynman)射入一块[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)材料时会发生什么？如果[光子](@keyword=photon|lang=zh-CN|style=Feynman)的能量恰到好处，它会“踢”出一个电子，使其从被束缚的价带（valence band）跃迁到可以自由移动的[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)（conduction band）。这个电子带负电，而在它离开的价带中，留下了一个带正电的“[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)”，我们称之为**空穴** (hole)。

现在，我们有了一个负电子和一个正空穴。在真空中，它们会像磁铁的两极一样相互吸引，遵循[库仑定律](@keyword=coulomb_s_law|lang=zh-CN|style=Feynman)。但在固体的世界里，事情变得更有趣了。它们仍然相互吸引，但它们并非身处空无一物的舞台，而是[沉浸](@keyword=immersion|lang=zh-CN|style=Feynman)在一个由无数原子构成的“海洋”中。尽管如此，这个[电子和空穴](@keyword=electrons_and_holes|lang=zh-CN|style=Feynman)仍然有可能撇开周围的喧嚣，形成一个束缚对——这，就是**激子** (exciton)。

理解[激子](@keyword=excitons|lang=zh-CN|style=Feynman)最直观的方式，就是将它想象成一个“固态的氢原子”。在氢原子中，一个电子围绕着一个质子旋转。在[激子](@keyword=excitons|lang=zh-CN|style=Feynman)中，一个电子围绕着一个空穴“旋转”。这个类比异常强大，因为它让我们能够运用关于原子物理的直觉。但正如所有好的物理模型一样，关键在于理解它与现实的差异，以及这些差异所揭示的深刻物理。

与真空中简单的氢原子相比，[激子](@keyword=excitons|lang=zh-CN|style=Feynman)这个“固态氢原子”被它所处的环境深刻地重塑了。主要体现在两个方面 [@problem_id:2821578]：

1.  **屏蔽的相互作用 (Screened Interaction)**：[电子和空穴](@keyword=electrons_and_holes|lang=zh-CN|style=Feynman)之间的库仑吸引力被[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)原子“稀释”或屏蔽了。这就像在水中观察物体，光线会发生折射一样。这种[屏蔽效应](@keyword=screening_effect|lang=zh-CN|style=Feynman)由材料的**[介电常数](@keyword=permittivity|lang=zh-CN|style=Feynman)** ($\varepsilon_r$) 描述。$\varepsilon_r$ 越大，屏蔽越强，电子和空穴之间的吸引力就越弱。

2.  **重塑的惯性 (Remodeled Inertia)**：在[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中运动的[电子和空穴](@keyword=electrons_and_holes|lang=zh-CN|style=Feynman)，其行为并不像在真空中那样自由。它们与周期性排布的原子相互作用，使得它们的惯性（质量）发生了改变。我们用**[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)** ($m_e^*$ 和 $m_h^*$) 来描述这种变化。一个电子或空穴的[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)可能比其在真空中的质量大得多，也可能小得多，这取决于[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)[势场](@keyword=potential_field|lang=zh-CN|style=Feynman)的具体“地形”。

这两个因素——[介电常数](@keyword=permittivity|lang=zh-CN|style=Feynman)和[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)——共同决定了一个[激子](@keyword=excitons|lang=zh-CN|style=Feynman)的两个最基本属性：它的**[玻尔半径](@keyword=bohr_radius|lang=zh-CN|style=Feynman)** ($a_X$)，即电子与空穴之间的平均距离；以及它的**结合能** ($E_b$)，即拆散这个[电子-空穴对](@keyword=electron_hole_pair|lang=zh-CN|style=Feynman)所需的能量。从氢原子的模型出发，我们可以推断出它们的标度关系 [@problem_id:2821578]：

$$
E_b \propto \frac{\mu}{\varepsilon_r^2} \quad \text{以及} \quad a_X \propto \frac{\varepsilon_r}{\mu}
$$

其中 $\mu$ 是由电子和空穴有效质量决定的**[折合质量](@keyword=reduced_mass|lang=zh-CN|style=Feynman)** ($\frac{1}{\mu} = \frac{1}{m_e^*} + \frac{1}{m_h^*}$)。这个简单的关系蕴含着丰富的物理：一个具有强屏蔽 ($\varepsilon_r$ 大) 和轻[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman) ($\mu$ 小) 的材料，会形成一个空间上延展很广 ($a_X$ 大)、束缚很弱 ($E_b$ 小) 的[激子](@keyword=excitons|lang=zh-CN|style=Feynman)。

这个理论最美妙的验证之一，来自于材料的光学吸收谱。为了将电子从[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)激发到导带，[光子](@keyword=photon|lang=zh-CN|style=Feynman)通常需要提供至少等于**[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)** ($E_g$) 的能量。但由于激子是一个能量比自由[电子-空穴对](@keyword=electron_hole_pair|lang=zh-CN|style=Feynman)更低的稳定束缚态，形成[激子](@keyword=excitons|lang=zh-CN|style=Feynman)所需的光子能量实际上略低于[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，其值为 $E_g - E_b$。因此，在许多[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)的吸收谱中，我们可以在[带隙能量](@keyword=bandgap_energy|lang=zh-CN|style=Feynman)之下观察到一个尖锐的吸收峰，这正是激子存在的“吸烟枪”证据 [@problem_id:1775136]。

### 激子的两种风味：Wannier-Mott与Frenkel

基于这个“固态氢原子”模型，我们可以将[激子](@keyword=excitons|lang=zh-CN|style=Feynman)大致分为两种截然不同的“风味”，这取决于其尺寸相对于晶格常数 $a$ 的大小 [@problem_id:2987958]。

#### [Wannier-Mott激子](@keyword=wannier_mott_exciton|lang=zh-CN|style=Feynman)

当[激子](@keyword=excitons|lang=zh-CN|style=Feynman)的[玻尔半径](@keyword=bohr_radius|lang=zh-CN|style=Feynman)远大于晶格常数 ($a_X \gg a$) 时，我们称之为**[Wannier-Mott激子](@keyword=wannier_mott_exciton|lang=zh-CN|style=Feynman)**。这正是我们刚才讨论的“巨型氢原子”模型最适用的情况。这种[激子](@keyword=excitons|lang=zh-CN|style=Feynman)是弱束缚的，其[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)延展到成百上千个原子之上。电子和空穴之间的距离很大，以至于它们感受到的仅仅是[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)屏蔽后的、平滑的平均势场。这在典型的共价[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)中非常常见，例如砷化镓 (GaAs) 或硅 (Si)，这些材料通常具有较大的[介电常数](@keyword=permittivity|lang=zh-CN|style=Feynman)和较小的[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)。在砷化镓中，一个[激子](@keyword=excitons|lang=zh-CN|style=Feynman)的半径可以达到约 $12$ 纳米，是晶格常数（约 $0.57$ 纳米）的二十多倍！[@problem_id:2987958]

#### [Frenkel激子](@keyword=frenkel_exciton|lang=zh-CN|style=Feynman)

与[Wannier-Mott激子](@keyword=wannier_mott_exciton|lang=zh-CN|style=Feynman)相对的是**[Frenkel激子](@keyword=frenkel_exciton|lang=zh-CN|style=Feynman)**。当电子和空穴被紧紧地束缚在一起，其尺寸与单个原子或分子相当，甚至更小 ($a_X \lesssim a$) 时，就形成了[Frenkel激子](@keyword=frenkel_exciton|lang=zh-CN|style=Feynman)。你可以把它想象成一个被激发了的原子或分子，坐落在由其他[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)原子或分子组成的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中。这种激子常见于分子晶体（如蒽）或稀有气体固体（如固态氪）中，这些材料的电子被紧密地束缚在原子或分子内部，且[介电屏蔽](@keyword=dielectric_shielding|lang=zh-CN|style=Feynman)效应很弱。

对于[Frenkel激子](@keyword=frenkel_exciton|lang=zh-CN|style=Feynman)，“固态氢原子”的类比就不那么贴切了。一个更好的模型是**[紧束缚模型](@keyword=tight_binding_model|lang=zh-CN|style=Feynman)** (tight-binding model) [@problem_id:2988004]。在这个模型中，[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)是局域在单个格点（原子或分子）上的。然而，由于[量子力学中的隧穿效应](@keyword=tunneling_in_quantum_mechanics|lang=zh-CN|style=Feynman)，这个局域的激发可以“跳跃”到相邻的格点上。这种从一个格点到另一个格点的相干跳跃，使得[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)不再静止于一点，而是在整个晶体中以波的形式传播。这种传播的[激子](@keyword=excitons|lang=zh-CN|style=Feynman)波，就像在[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中传播的电子波一样，也具有自己的能量-动量关系，即**[能带色散](@keyword=energy_band_dispersion|lang=zh-CN|style=Feynman)**。对于一个简单的一维分子链，其能量可以表示为：

$$
E(k) = E_0 + 2J \cos(ka)
$$

其中 $E_0$ 是单个分子的激发能，$J$ 是相邻分子间的[转移积分](@keyword=transfer_integral|lang=zh-CN|style=Feynman)（描述跳跃的难易程度），$k$ 是波矢，$a$ 是[晶格常数](@keyword=lattice_constant|lang=zh-CN|style=Feynman) [@problem_id:2988004]。这揭示了一个深刻的统一性：无论是延展的[Wannier-Mott激子](@keyword=wannier_mott_exciton|lang=zh-CN|style=Feynman)还是局域的[Frenkel激子](@keyword=frenkel_exciton|lang=zh-CN|style=Feynman)，它们都是在固体中传播的波包，是波粒二象性的完美体现。

### [激子](@keyword=excitons|lang=zh-CN|style=Feynman)的内心世界：自旋与交换

[激子](@keyword=excitons|lang=zh-CN|style=Feynman)不仅仅是一个简单的[电荷复合](@keyword=charge_recombination|lang=zh-CN|style=Feynman)体，它还拥有丰富的“内心世界”，其中最重要的是**自旋** (spin)。电子和空穴都是自旋为 $1/2$ 的[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)。根据角动量[叠加原理](@keyword=principle_of_superposition|lang=zh-CN|style=Feynman)，一个电子和一个空穴的自旋可以有两种组合方式：它们的自旋反平行，[总自旋](@keyword=total_spin|lang=zh-CN|style=Feynman)为 $S=0$（**单重态**）；或者它们的自旋平行，总自旋为 $S=1$（**[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)**）。

这个小小的自旋差异，却对激子的光学性质产生了巨大的影响。在最简单的情况下，只有当电子和空穴的自旋反平行 ($S=0$) 时，它们才能高效地复合，并以[光子](@keyword=photon|lang=zh-CN|style=Feynman)的形式释放能量。我们称这种可以与光直接相互作用的[激子](@keyword=excitons|lang=zh-CN|style=Feynman)为**亮激子** (bright exciton)。而总自旋为 $S=1$ 的三种状态，由于[自旋选择定则](@keyword=spin_selection_rules|lang=zh-CN|style=Feynman)的限制，不能直接衰变成[光子](@keyword=photon|lang=zh-CN|style=Feynman)，因此被称为**暗[激子](@keyword=excitons|lang=zh-CN|style=Feynman)** (dark exciton) [@problem_id:1775152]。这个“亮”与“暗”的区别，对于设计[发光二极管](@keyword=light_emitting_diodes|lang=zh-CN|style=Feynman)（LED）、激光器和量子光源等光电器件至关重要，因为只有亮激子才能有效发光。

那么，是什么决定了亮[激子](@keyword=excitons|lang=zh-CN|style=Feynman)和暗激子之间的能量差异呢？答案是一种纯粹的量子力学效应——**交换相互作用** (exchange interaction) [@problem_id:2988007]。这种相互作用的根源在于电子的不可区分性（[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)）。它不是经典的[库仑力](@keyword=coulomb_force|lang=zh-CN|style=Feynman)，而是一种修正，源于考虑两个电子（一个在导带，一个在[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)）[波函数反对称性](@keyword=wavefunction_antisymmetry|lang=zh-CN|style=Feynman)时出现的额外能量项。

令人惊奇的是，这种[交换相互作用](@keyword=exchange_interaction|lang=zh-CN|style=Feynman)可以进一步分为两个部分，它们的物理起源和效应截然不同 [@problem_id:2988007]：

-   **短程交换作用**：这是一种“接触”式的相互作用，只在[电子和空穴](@keyword=electrons_and_holes|lang=zh-CN|style=Feynman)的[波函数重叠](@keyword=wavefunction_overlap|lang=zh-CN|style=Feynman)时才显著，也就是说，当它们位于同一个晶体[原胞](@keyword=primitive_unit_cell|lang=zh-CN|style=Feynman)内时。这种相互作用对自旋非常敏感，它正是导致亮激子（[单重态](@keyword=singlet_state|lang=zh-CN|style=Feynman)）和暗激子（[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)）之间产生能量分裂的主要原因 [@problem_id:2821553]。

-   **长程交换作用**：这部分更加奇特。它是一种非局域的相互作用，其大小和符号竟然取决于激子运动的**方向**！你可以把它想象成[激子](@keyword=excitons|lang=zh-CN|style=Feynman)自身的跃迁[电偶极矩](@keyword=electric_dipole_moment|lang=zh-CN|style=Feynman)产生了一个[宏观电场](@keyword=macroscopic_electric_field|lang=zh-CN|style=Feynman)，这个电场反过来又作用于激子本身。这种奇异的自相互作用导致了亮激子根据其运动方向（相对于其极化方向）分裂成**纵向[激子](@keyword=excitons|lang=zh-CN|style=Feynman)** (longitudinal exciton) 和**横向激子** (transverse exciton)，它们之间存在能量差，即**纵横分裂** (longitudinal-transverse splitting)。

### 激子的社交生活：从个体到群体

单个激子的行为已经足够有趣，但当许多激子聚集在一起时，一幅更加丰富多彩的社会图景便展现在我们面前。

#### [复合玻色子](@keyword=composite_bosons|lang=zh-CN|style=Feynman)与[激子](@keyword=excitons|lang=zh-CN|style=Feynman)分子

首先，一个惊人的事实是，在密度较低时，由两个[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)（[电子和空穴](@keyword=electrons_and_holes|lang=zh-CN|style=Feynman)）组成的激子，其整体行为就像一个**[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)** (boson) [@problem_id:1775159]。这个近似之所以成立，是因为当[激子](@keyword=excitons|lang=zh-CN|style=Feynman)相距很远时，交换一个[激子](@keyword=excitons|lang=zh-CN|style=Feynman)和另一个[激子](@keyword=excitons|lang=zh-CN|style=Feynman)，等效于交换两对[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)，其[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的总符号不变，这正是[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)的特征。然而，这只是一个近似。当[激子](@keyword=excitons|lang=zh-CN|style=Feynman)密度增加，它们之间的平均距离近到可以与自身的[玻尔半径](@keyword=bohr_radius|lang=zh-CN|style=Feynman)相比拟时，[激子](@keyword=excitons|lang=zh-CN|style=Feynman)内部的[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)“个性”就会显现出来。一个[激子](@keyword=excitons|lang=zh-CN|style=Feynman)中的电子会开始“排斥”另一个激子中的电子（[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)），[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)近似就失效了 [@problem_id:2821566]。

在这种低密度、类似气体的状态下，激子之间可以像原子形成分子一样，相互结合形成更复杂的复合物：

-   **三子** (Trion)：最简单的[激子](@keyword=excitons|lang=zh-CN|style=Feynman)“分子”是一个激子与一个额外的自由电荷（电子或空穴）结合形成的带电[三体复合](@keyword=three_body_recombination|lang=zh-CN|style=Feynman)物。例如，一个由两个电子和一个空穴组成的带负电的三子 ($X^-$) [@problem_id:1775145]，或一个由一个电子和两个空穴组成的带正电的三子 ($X^+$)。它们可以被看作是[激子](@keyword=excitons|lang=zh-CN|style=Feynman)世界里的“[氢分子离子](@keyword=hydrogen_molecule_ion|lang=zh-CN|style=Feynman)”($H_2^+$)。
-   **双激子** (Biexciton)：两个中性的[激子](@keyword=excitons|lang=zh-CN|style=Feynman)也可以相互吸引，形成一个稳定的四体束缚态，即双激子。这可以被视为[激子](@keyword=excitons|lang=zh-CN|style=Feynman)世界里的“氢分子”($H_2$)。将它们束缚在一起的力，包括源于[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)交换的短程吸引力，以及类似于中性[原子间作用力](@keyword=forces_on_atoms|lang=zh-CN|style=Feynman)的长程范德瓦尔斯力 [@problem_id:2988047]。

#### [莫特相变](@keyword=mott_transition|lang=zh-CN|style=Feynman)：从气体到等离子体

随着激子密度不断增加，[激子](@keyword=excitons|lang=zh-CN|style=Feynman)“气体”最终会经历一场剧烈的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)。当[激子](@keyword=excitons|lang=zh-CN|style=Feynman)之间的距离近到一定程度时，它们之间的[库仑屏蔽](@keyword=coulomb_screening|lang=zh-CN|style=Feynman)效应会变得极强，以至于任何一个[电子-空穴对](@keyword=electron_hole_pair|lang=zh-CN|style=Feynman)都无法再维持束缚状态。整个系统会从一个由中性[激子](@keyword=excitons|lang=zh-CN|style=Feynman)构成的绝缘“气体”，转变成一个由自由电子和空穴组成的导电“等离子体”。这个从绝缘态到金属态的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)，被称为**[莫特相变](@keyword=mott_transition|lang=zh-CN|style=Feynman)** (Mott transition) [@problem_id:121845]。这为我们描绘了激子存在的上限，也展示了[多体相互作用](@keyword=many_body_interaction|lang=zh-CN|style=Feynman)如何催生出全新的物质状态。

### 激子与环境：盛装舞步

最后，我们必须认识到，激子并非生活在真空中，它深深地[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)在[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的怀抱里。它与环境的互动，为自己“穿上”了各种华丽的“外衣”，从而变成了新的、更为复杂的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)。

#### 激子-[极化子](@keyword=polarons|lang=zh-CN|style=Feynman)

[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)并非静止不动，而是时刻在[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，这些[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)量子就是**[声子](@keyword=phonons|lang=zh-CN|style=Feynman)** (phonon)。激子作为一种[电荷分布](@keyword=charge_distribution|lang=zh-CN|style=Feynman)，会使其周围的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)发生畸变（极化），就像一个保龄球落在蹦床上会使其凹陷一样。当[激子](@keyword=excitons|lang=zh-CN|style=Feynman)在[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中移动时，它会拖着这个[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)畸变的“云团”一起前进。这种由[激子](@keyword=excitons|lang=zh-CN|style=Feynman)和伴随它的[声子](@keyword=phonons|lang=zh-CN|style=Feynman)云共同构成的“盛装”[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，被称为**激子-[极化子](@keyword=polarons|lang=zh-CN|style=Feynman)** (exciton-polaron) [@problem_id:2987999]。

与[声子](@keyword=phonons|lang=zh-CN|style=Feynman)的耦合会带来显著的后果。首先，这团[声子](@keyword=phonons|lang=zh-CN|style=Feynman)“外衣”增加了[激子](@keyword=excitons|lang=zh-CN|style=Feynman)运动的“拖累”，使其有效质量变大 [@problem_id:99433]。在[强耦合](@keyword=strong_coupling|lang=zh-CN|style=Feynman)的情况下，这种拖累效应会变得极其严重，以至于激子完全被自己造成的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)畸变“卡住”，无法移动，形成**[自陷](@keyword=self_trapping|lang=zh-CN|style=Feynman)激子** (self-trapped exciton)。这可以看作是一场竞赛：是保持离域状态以降低动能更有利，还是通过局域化让[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)为自己创造一个[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)以降低势能更有利 [@problem_id:2988009]。

#### [激子-极化激元](@keyword=exciton_polaritons|lang=zh-CN|style=Feynman)

如果我们将容纳[激子](@keyword=excitons|lang=zh-CN|style=Feynman)的[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)材料放置在一个由两面镜子构成的[光学微腔](@keyword=optical_microcavity|lang=zh-CN|style=Feynman)中，一个更加奇妙的[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)将会诞生。[激子](@keyword=excitons|lang=zh-CN|style=Feynman)可以吸收一个腔内[光子](@keyword=photon|lang=zh-CN|style=Feynman)，然后又将其重新发射出来；这个[光子](@keyword=photon|lang=zh-CN|style=Feynman)可以在腔内来回反射，并再次被[激子](@keyword=excitons|lang=zh-CN|style=Feynman)吸收。这种在[激子](@keyword=excitons|lang=zh-CN|style=Feynman)和[光子](@keyword=photon|lang=zh-CN|style=Feynman)之间快速、可逆的能量交换，使得我们再也无法清晰地分辨哪个是[激子](@keyword=excitons|lang=zh-CN|style=Feynman)，哪个是[光子](@keyword=photon|lang=zh-CN|style=Feynman)。它们混合成了一种全新的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)——**[激子-极化激元](@keyword=exciton_polaritons|lang=zh-CN|style=Feynman)** (exciton-polariton) [@problem_id:2987941]。

这种[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)一半是“物质”（激子成分），一半是“光”（[光子](@keyword=photon|lang=zh-CN|style=Feynman)成分）。这种光与物质的强耦合，最显著的标志是在共振时出现**[拉比分裂](@keyword=rabi_splitting|lang=zh-CN|style=Feynman)** (Rabi splitting)：原本简并的[激子](@keyword=excitons|lang=zh-CN|style=Feynman)和[光子](@keyword=photon|lang=zh-CN|style=Feynman)能级会相互“推开”，形成两个新的、能量分离的[极化激元](@keyword=polaritons|lang=zh-CN|style=Feynman)能级。这些极化激元继承了[光子](@keyword=photon|lang=zh-CN|style=Feynman)的极轻有效质量 [@problem_id:99476] 和激子的强相互作用特性，使它们成为在较高温度下实现玻色-爱因斯坦凝聚等[宏观量子现象](@keyword=macroscopic_quantum_phenomena|lang=zh-CN|style=Feynman)的理想平台。

从一个简单的类比，到复杂的内部结构、社会行为和与环境的互动，我们对[激子](@keyword=excitons|lang=zh-CN|style=Feynman)的探索之旅揭示了凝聚态物理学中令人惊叹的丰富性和统一性。[激子](@keyword=excitons|lang=zh-CN|style=Feynman)不仅仅是一个理论模型，它是一个活跃的、多姿多彩的实体，连接着量子力学、光学和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)的多个领域，并持续为未来的技术创新提供着源源不断的灵感。