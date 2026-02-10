## 引言
[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的曙光预示着技术的重塑，但构建这样一台革命性的机器并不仅仅是软件上的挑战——它从根本上说是一个[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)问题。虽然[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)、叠加和纠缠等抽象概念定义了[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的逻辑，但这些思想必须在物理系统中得以实现。核心的知识鸿沟在于，如何将理论量子力学的世界与实际、复杂的真实材料世界联系起来。我们如何能在原子层面寻找、设计和控制物质，以可靠地承载和操控脆弱的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)？本文将探索[量子材料](@keyword=quantum_materials|lang=zh-CN|style=Feynman)的领域，为理解这一技术前沿提供必要的知识。第一章 **“原理与机制”** 深入探讨了赋予材料量子特性的基本物理学，从电子的内禀自旋到[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中电子的集体行为。随后的 **“应用与跨学科联系”** 章节将探讨如何利用这些原理，不仅构建[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机，还发展先进的[光电子学](@keyword=optoelectronics|lang=zh-CN|style=Feynman)、医学成像工具和新一代的[计算设计](@keyword=computational_design|lang=zh-CN|style=Feynman)材料。我们的旅程从量子世界的基本构成单元开始，探索自然本身如何为一种新型计算机提供了完美的要素。

## 原理与机制

想象一下，你想构建一种新型计算机。它不是那种仅仅能更快处理数字的机器，而是一种在奇特而美妙的量子世界法则下运行的计算机。为此，你需要一种新型的“比特”：**[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)**（qubit）。一个经典比特是一个简单的开关，要么是开（1），要么是关（0）。而一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，则可以处于0、1，或者——这正是其魔力所在——同时处于两者的一种微妙的**叠加态**。但是，我们在自然界中哪里能找到如此奇妙的开关呢？答案不在于从零开始构建新东西，而在于倾听物质本身的量子低语。

### 两能级戏法：电子的内禀自旋

大自然慷慨地为我们提供了一个近乎完美的、现成的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)：电子。每个电子都拥有一个称为**自旋**的内禀、不可改变的属性。你可以谨慎地将其想象成电子像一个微小的、旋转的带电小球。这种自旋是一种角动量，但它纯粹是量子力学性质的。

当我们想要描述像电子这样的粒子的自旋时，量子力学告诉我们，有两个我们关心的数字。第一个是**[自旋量子数](@keyword=spin_quantum_number|lang=zh-CN|style=Feynman)** $s$，它告诉我们粒子所具有的自旋*总量*。对于宇宙中任何地方的任何电子，这个数字都是固定的：$s = \frac{1}{2}$。这是它身份的一部分。第二个数字是**[自旋磁量子数](@keyword=ms_quantum_number|lang=zh-CN|style=Feynman)** $m_s$，它告诉我们自旋的取向，或者说沿着我们选择的轴（我们称之为 $z$ 轴）的投影。对于一个 $s = \frac{1}{2}$ 的粒子，量子力学的规则只允许这个投影有两个可能的值：$m_s = +\frac{1}{2}$（“自旋向上”）和 $m_s = -\frac{1}{2}$（“自旋向下”）。

就是这样！一个完美的双能级系统。我们的0和1。电子自旋的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)可以写作 $\lvert s, m_s \rangle$。完整的描述涉及到两个算符的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)：[总自旋](@keyword=total_spin|lang=zh-CN|style=Feynman)平方算符 $\hat{S}^2$，它测量自旋的大小；以及 $z$ 分量算符 $\hat{S}_z$，它测量其投影。它们的作用定义如下：
$$ \hat{S}^2\lvert s,m_s\rangle = s(s+1)\hbar^2 \lvert s,m_s\rangle $$
$$ \hat{S}_z\lvert s,m_s\rangle = m_s\hbar \lvert s,m_s\rangle $$
对于我们的电子，这些方程证实了其总自旋大小总是与 $s=\frac{1}{2}$ 相关联，而其沿我们测量轴的状态可以是两个离散选项之一，即“自旋向上”态 $\lvert \frac{1}{2}, +\frac{1}{2} \rangle$ 或“自旋向下”态 $\lvert \frac{1}{2}, -\frac{1}{2} \rangle$ [@problem_id:2469521]。这就是最基本的构建模块。

### 唤醒[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)：与[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的对话

拥有一个[两能级系统](@keyword=two_level_system|lang=zh-CN|style=Feynman)是一回事；控制它则是另一回事。在自然状态下，电子的“向上”和“向下”[自旋态](@keyword=spin_states|lang=zh-CN|style=Feynman)具有相同的能量。为了使它们有用，我们需要让它们变得不同。我们需要“唤醒”它们。

关键在于，电子的自旋也赋予了它一个**磁矩** $\vec{\mu}$，使其行为像一个微观的指南针。这个磁矩通过一个称为[旋磁比](@keyword=gyromagnetic_ratio|lang=zh-CN|style=Feynman)的常数 $\gamma$ 与其[自旋角动量](@keyword=spin_angular_momentum|lang=zh-CN|style=Feynman) $\vec{S}$ 成正比：$\vec{\mu} = \gamma \vec{S}$。现在我们有了把手！我们可以利用外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $\vec{B}$ 与这个磁矩对话。

当我们将电子置于[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中时，[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)会对磁矩施加力矩，系统的能量会根据其取向而改变。这种相互作用由简洁而优雅的**塞曼哈密顿量**描述：$H = -\vec{\mu} \cdot \vec{B}$。如果我们将[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)沿 $z$ 轴方向[排列](@keyword=permutation|lang=zh-CN|style=Feynman)，[自旋态](@keyword=spin_states|lang=zh-CN|style=Feynman)的能量就变成 $E = -\gamma B m_s \hbar$。突然之间，我们的两个状态，$m_s = +\frac{1}{2}$ 和 $m_s = -\frac{1}{2}$，能量不再相同。[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)将它们分开了。

想象我们有两种假设的材料，一种由自旋为1/2的粒子构成，另一种由自旋为1的粒子构成，但具有相同的[旋磁比](@keyword=gyromagnetic_ratio|lang=zh-CN|style=Feynman)。在相同的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中，自旋为1的粒子的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)（最低能量）深度将是自旋为1/2粒子的两倍 [@problem_id:1981731]。这个简单的思想实验揭示了一个深刻的真理：我们[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的能量景观是我们可以设计的，既可以通过选择粒子（其内禀自旋 $s$），也可以通过施加外部场。自旋向上和自旋向下态之间的能量差 $\Delta E$ 定义了我们[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的[自然频率](@keyword=natural_frequency|lang=zh-CN|style=Feynman) $\omega = \Delta E / \hbar$，这也是我们用于将其从0翻转到1所需的光的频率。

### 原子的磁性灵魂：打造[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的家园

一个孤立的电子是一个很好的理论出发点，但实际上，我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)存在于材料内部，作为[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的原子的一部分。在这里，事情变得更加有趣。一个原子的磁性不是由单个电子决定的，而是由其所有电子的集体舞蹈决定的。电子的[总轨道角动量](@keyword=total_orbital_angular_momentum|lang=zh-CN|style=Feynman)（$L$）和[总自旋角动量](@keyword=total_spin_angular_momentum|lang=zh-CN|style=Feynman)（$S$）结合起来，形成一个**总角动量**，由[量子数](@keyword=quantum_numbers|lang=zh-CN|style=Feynman) $J$ 标记。这个数字决定了整个原子是否像一个小磁铁一样活动。

这种组合的规则（称为**洪德规则**）是量子力学创造复杂秩序的一个壮观例子。考虑在其p轨道上有电子的原子。单个p电子（$p^1$ 构型）会形成一个有磁性的原子。但两个p电子（$p^2$）呢？你可能会认为两个磁铁会形成一个更大的磁铁。但量子力学不这么认为。为了最小化它们的能量，两个电子会以一种非常特殊的方式[排列](@keyword=permutation|lang=zh-CN|style=Feynman)它们的自旋和轨道，导致[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的 $J=0$ [@problem_id:1792728]。这个原子是“磁性静默的”，是[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中的一个幽灵。

这非常有用！为了构建一个[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机，我们可能会选择一个具有良好自旋的客体原子（如氮）作为我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，并将其置于由磁性静默的原子组成的主体晶体中（如金刚石中的碳，形成著名的NV[色心](@keyword=color_centers|lang=zh-CN|style=Feynman)）。这个静默的主体提供了一个安静、稳定的环境，保护我们[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)脆弱的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)免受不必要的磁性“喋喋不休”的干扰。

### 电子在晶体中的生命：[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)、[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)和[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)

当我们将原子[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成一个完美的、重复的晶体时，电子的世界发生了巨大变化。电子不再处于一个单一、明确的能级，而是看到一个由原子核构成的周期性景观。其允许的能量被“涂抹”成广阔的大陆，称为**[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)**，这些[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)被禁止的海洋——**[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)**——所分隔。

电子可以从一个被填满的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)（**价带**）激发到一个空的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)（**导带**），留下一个**空穴**——即电子的缺失，它巧妙地表现得像一个正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)粒子。当电子回落时，它可以以[光子](@keyword=photon|lang=zh-CN|style=Feynman)的形式释放其能量。这就是LED背后的原理。但这个过程的效率严重依赖于晶体的[能带结构](@keyword=e_k_diagram|lang=zh-CN|style=Feynman)。

在**直接带隙**[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)（如砷化镓）中，导带的最低点在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中正好位于价带的最高点之上。电子可以简单地掉下来，释放一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)，一切顺利。而在**[间接带隙](@keyword=indirect_bandgap|lang=zh-CN|style=Feynman)**[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)（如硅）中，这两点是错位的。为了让电子下落，它不仅要释放一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)，还必须从晶格振动（即一个**[声子](@keyword=phonons|lang=zh-CN|style=Feynman)**）中获得一个动量“踢”。这种[三体](@keyword=trisomy|lang=zh-CN|style=Feynman)探戈的发生几率要小得多，使得[发光效率](@keyword=luminous_efficacy|lang=zh-CN|style=Feynman)极差 [@problem_id:1771550]。这就是为什么你的电脑硅芯片不会发光，也是设计用于光控量子器件的材料时的一个关键考量。

此外，一个穿过这个晶体景观的电子感觉不像一个自由粒子。来自[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)离子的持续推拉使其表现得好像具有不同的质量，即**[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)**（$m^*$）。这不是一个戏法；这是一个深刻的简化。所有复杂的相互作用都被打包到这一个参数中，使我们能以一种优美简洁的方式描述电子的运动。

### 量子囚笼的艺术：捕获[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)

为了构建一个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，我们不能让我们的电子在整个晶体中自由漫游。我们需要捕获它，将它固定住以便我们能与它对话。这就是**[量子限制](@keyword=quantum_confinement|lang=zh-CN|style=Feynman)**的艺术。通过构建纳米尺度的结构，我们可以创造“量子囚笼”或[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)。

最简单的例子是**量子点**，一个微小的[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)斑点，它小到像一个人工原子。我们可以将其建模为一个盒子中的电子——或者更准确地说，是一个抛物线[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)中的电子。就像吉他弦只能以特定频率[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)一样，一个被限制的电子也只能拥有特定的、量子化的能级。这些能级的间距取决于[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)的陡峭程度，以及至关重要的，电子的有效质量，其中[基态能量](@keyword=ground_state_energy_2|lang=zh-CN|style=Feynman)的标度关系为 $E_1 \propto 1/\sqrt{m^*}$ [@problem_id:1805816]。较轻的电子更“分散”，具有更高的限制能。这给了我们另一个可以调节的旋钮：通过选择具有不同有效质量的材料，我们可以直接设计我们人造原子的[能谱](@keyword=energy_spectrum|lang=zh-CN|style=Feynman)。

我们甚至可以捕获更奇特的东西。当一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)撞击[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)时，它可以产生一个电子-空穴对，它们因相互吸引而保持束缚，形成一个类氢[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，称为**激子**。这个[激子](@keyword=excitons|lang=zh-CN|style=Feynman)的自然“尺寸”是其[有效玻尔半径](@keyword=effective_bohr_radius|lang=zh-CN|style=Feynman) $a_B^*$。如果我们将这个[激子](@keyword=excitons|lang=zh-CN|style=Feynman)捕获在一个比其自身尺寸更薄的**[量子阱](@keyword=quantum_wells|lang=zh-CN|style=Feynman)**中会发生什么？这种限制会“压扁”激子，迫使其从三维存在变为二维存在。这种维度的急剧变化增加了其束缚能，使其更加稳定。三维和二维行为之间的转变发生在阱宽 $L$ 变得与激子的[有效玻尔半径](@keyword=effective_bohr_radius|lang=zh-CN|style=Feynman) $a_B^*$ 相当时 [@problem_id:2821522]。这不仅仅是一个奇观；它证明了我们不仅能操纵粒子，还能通过塑造其环境的几何形状来改变其相互作用的本质。

### 不可避免的温暖：热、[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)和量子噪声

不幸的是，我们的量子世界并非孤立。它生活在我们的经典世界中，一个温暖、嘈杂而混乱的地方。[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)最大的敌人是热量，它表现为[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。这些量子化的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，即**[声子](@keyword=phonons|lang=zh-CN|style=Feynman)**，就像一片持续的震颤之海，可以[颠簸](@keyword=thrashing|lang=zh-CN|style=Feynman)我们的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，破坏其叠加态，使其忘记自己的状态。这个过程被称为**[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)**。

为了对抗[退相干](@keyword=decoherence|lang=zh-CN|style=Feynman)，[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机在极低的、接近绝对零度几个分之一的低温下运行。在这些温度下，材料的热学性质变得至关重要。例如，金属的[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)主要有两个部分：一部分来自电子，一部分来自[声子](@keyword=phonons|lang=zh-CN|style=Feynman)。电子部分与温度成正比，$C_e = \gamma T$，而[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)部分则急剧下降，如同 $C_l \propto T^3$ [@problem_id:1774390]。当我们冷却下来时，[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)冻结成几乎完美的寂静，其速度远快于电子。

管理这种[热噪声](@keyword=johnson_nyquist_noise|lang=zh-CN|style=Feynman)是一项重大的工程挑战。考虑一根在低温装置中用作连接的纳米线。在这些低温下，[声子](@keyword=phonons|lang=zh-CN|style=Feynman)像子弹一样弹道式传播，直到撞到表面。在一根纯净的[纳米线](@keyword=nanowires|lang=zh-CN|style=Feynman)中，[声子](@keyword=phonons|lang=zh-CN|style=Feynman)的[平均自由程](@keyword=mean_free_path|lang=zh-CN|style=Feynman)就是线的直径。这意味着[热导率](@keyword=thermal_conductivity|lang=zh-CN|style=Feynman)与直径成正比：$\kappa \propto D$ [@problem_id:1795195]。更细的线是更好的热绝缘体！这个反直觉的结果对于设计能够将脆弱的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)与外界热量隔离开来的支架和布线至关重要。

### 超导革命

最后，我们来到了最引人瞩目的量子材料类别：**[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)**。在某个[临界温度](@keyword=critical_temperature|lang=zh-CN|style=Feynman) $T_c$ 以下，这些材料会经历[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)，进入一个[宏观量子态](@keyword=macroscopic_quantum_state|lang=zh-CN|style=Feynman)。通常相互排斥的电子形成“[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)”，能够以绝对[零电阻](@keyword=zero_resistance|lang=zh-CN|style=Feynman)的方式穿过[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。

但还不止于此。[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)还表现出**迈斯纳效应**：它们会主动地将其内部的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)排斥出去，成为完美的抗磁体。然而，“完美”是一个很强的词。[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)并非在表面瞬间被排斥；它会穿透一个微小的距离，称为**[伦敦穿透深度](@keyword=london_penetration_depth|lang=zh-CN|style=Feynman)** $\lambda$。对于一根半径 $R$ 与 $\lambda$ 相当的细超导线，相当一部分[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)仍然可以进入内部 [@problem_id:1825915]。这个看似不完美之处，实际上是我们利用的一个特性。[超导量子比特](@keyword=superconducting_qubits|lang=zh-CN|style=Feynman)，如广泛使用的“transmon”，本质上是微观电路。它们的[电感](@keyword=inductance|lang=zh-CN|style=Feynman)——形成[振荡器](@keyword=oscillators|lang=zh-CN|style=Feynman)的关键属性——直接来源于[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的动能和储存在这个穿透区域的磁能。我们正是利用这种“不完美”的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)排斥物理来构建[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)。

[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的世界仍然充满了神秘。传统的[超导理论](@keyword=superconductivity_theory|lang=zh-CN|style=Feynman)，即巴丁-库珀-施里弗（BCS）理论，做出了一个坚定的预测：零温下[超导能隙](@keyword=superconducting_gap|lang=zh-CN|style=Feynman)与[临界温度](@keyword=critical_temperature|lang=zh-CN|style=Feynman)之比 $2\Delta(0)/(k_B T_c)$ 应该是一个通用常数，约为3.53。这对于许多传统的低温[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)是成立的。但对于20世纪80年代发现的奇特的**高温[铜氧化物超导体](@keyword=cuprate_superconductors|lang=zh-CN|style=Feynman)**，实验一致发现这个比值要大得多，通常在4到9之间 [@problem_id:1781787]。这告诉我们，[BCS理论](@keyword=bcs_theory|lang=zh-CN|style=Feynman)中简单的电子-[声子](@keyword=phonons|lang=zh-CN|style=Feynman)[配对机制](@keyword=pairing_mechanisms|lang=zh-CN|style=Feynman)并非故事的全部。一种新的、更强大的理论正在发挥作用，暗示着我们尚未完全理解的更深层次的量子现象。正是在探索这些前沿——我们理解中的这些空白——之中，下一代量子材料将会诞生。