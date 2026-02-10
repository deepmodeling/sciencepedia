## 引言
光与[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)之间的相互作用是现代[光电子学](@keyword=optoelectronics|lang=zh-CN|style=Feynman)的引擎，从我们手中的发光显示屏到为世界供电的[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)板，无不如此。然而，其基本原理似乎深奥难懂：为什么硅芯片对某些光是透明的，而一块金属却是不透明的？我们如何能精确地设计一种材料来发射特定颜色的光？本文通过全面概述[半导体的光学性质](@keyword=optical_properties_of_semiconductors|lang=zh-CN|style=Feynman)来回答这些问题。我们首先将在“**原理与机制**”一章中深入量子世界，揭示[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)、[动量守恒](@keyword=conservation_of_momentum|lang=zh-CN|style=Feynman)的基本规则，以及激子等电子-空穴相互作用的关键作用。随后，“**应用与跨学科联系**”一章将把理论与实践联系起来，展示这些原理如何被用来创造LED、激光器、太阳能电池和[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)，以及这些知识如何将物理学与化学、工程学和计算科学联系起来。读完本文，您将不仅理解当光遇到[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)时会发生*什么*，还会理解*为什么*会发生，以及我们如何控制它。

## 原理与机制

要理解[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)如何与光相互作用，就必须踏上一段深入晶体量子世界的旅程。是什么决定了光是穿过、被吸收，还是被反射？答案并非单一属性，而是能量、动量和量子规则之间美妙的相互作用，这些规则支配着电子在固体刚性、重[复结构](@keyword=complex_structure|lang=zh-CN|style=Feynman)中的生命。让我们层层揭开这个引人入胜的故事。

### 巨大的鸿沟：电子的[量子跃迁](@keyword=quantum_jumps|lang=zh-CN|style=Feynman)

想象一下，你有两种材料。一种是像银一样的金属薄片，另一种是像硅一样的纯[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)芯片，并已冷却到接近绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)。你用一束昏暗的红光照射两者。银片闪闪发光，反射部分光并吸收其余部分，呈现不透明状态。然而，硅却是完全透明的；光线仿佛穿过空气一样通过了它。为什么会有如此巨大的差异？

秘密在于电子在这些材料中的[排列](@keyword=permutation|lang=zh-CN|style=Feynman)方式。在固体中，电子不能随意拥有任何能量。它被限制在特定的能量“楼层”上，即**[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)**。在绝对零度的[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)中，我们关心两个楼层：一个较低的楼层，即**价带**，完全被电子填满；另一个高得多的楼层，即**导带**，完全是空的。它们之间是一个巨大、空旷的楼梯间——一个[能量间隙](@keyword=energy_gap|lang=zh-CN|style=Feynman)，或称**[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)**（$E_g$），任何电子都不允许存在于此。

电子要吸收一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)，必须利用[光子](@keyword=photon|lang=zh-CN|style=Feynman)的能量跃迁到一个空的、能量更高的状态。在我们的[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)中，那束昏暗红光的[光子](@keyword=photon|lang=zh-CN|style=Feynman)根本没有足够的能量将电子从已满的[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)一直提升到空的[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)。这是一种**[带间跃迁](@keyword=interband_transitions|lang=zh-CN|style=Feynman)**，只有在[光子能量](@keyword=photon_energy|lang=zh-CN|style=Feynman) $\hbar\omega$ 大于[带隙能量](@keyword=bandgap_energy|lang=zh-CN|style=Feynman) $E_g$ 时才可能发生。但是，电子难道不能只吸收[光子](@keyword=photon|lang=zh-CN|style=Feynman)并在其自身的价带内移动到一个稍高的位置吗？**[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)**禁止这样做！该原理指出，没有两个电子可以占据相同的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。由于[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)已经完全填满，附近每个“座位”都已被占据。电子根本无处可去。由于没有可行的跃迁，低能量[光子](@keyword=photon|lang=zh-CN|style=Feynman)便不受阻碍地通过，材料因此是透明的 [@problem_id:1784042]。

那么金属呢？金属的能量结构就像一个巨大的、只被部分填满的楼层。那里有大量的已占据态，但就在这片电子海洋的表面——[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)——存在着无数能量稍高的空态。即使是低能量[光子](@keyword=photon|lang=zh-CN|style=Feynman)，也足以推动靠近海洋顶部的电子跳入一个[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)。这个过程称为**[带内跃迁](@keyword=intraband_transition|lang=zh-CN|style=Feynman)**，它能轻易地吸收[光子](@keyword=photon|lang=zh-CN|style=Feynman)的能量。这就是为什么金属对几乎任何能量的光都是不透明的 [@problem_id:1784042]。

这种根本差异——是否存在可被光触及的[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)——是第一条也是最重要的原理。[光子](@keyword=photon|lang=zh-CN|style=Feynman)是否被吸收直接影响材料的宏观光学性质，如其**[折射率](@keyword=refractive_index|lang=zh-CN|style=Feynman)**（$n$）和**[消光系数](@keyword=extinction_coefficient|lang=zh-CN|style=Feynman)**（$k$），这两者决定了光在材料内部如何弯曲和衰减。这两个数值又决定了我们肉眼所见：被反射的光的比例，即**[反射率](@keyword=reflectance|lang=zh-CN|style=Feynman)**（$R$），由[Fresnel公式](@keyword=fresnel_formulae|lang=zh-CN|style=Feynman)给出，对于垂直入射 [@problem_id:1792244]：

$$R = \frac{(n-1)^2 + k^2}{(n+1)^2 + k^2}$$

对于我们的透明[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)，$k$ 几乎为零，而对于能吸收光的金属，它则很大。

### 游戏规则：动量与对称性的故事

因此，要让[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)吸收光，[光子](@keyword=photon|lang=zh-CN|style=Feynman)必须有足够的能量（$\hbar\omega > E_g$）。但在物理学中，能量只是故事的一半；还有动量。当电子吸收[光子](@keyword=photon|lang=zh-CN|style=Feynman)时，系统的[总动量](@keyword=total_linear_momentum|lang=zh-CN|style=Feynman)必须守恒。这引出了一条极其简单却又意义深远的规则。

我们来做一个快速比较。晶体中电子的“动量”并非简单的质量乘以速度。它是一个称为**[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)动量**的量子概念，用波矢 $\vec{k}$ 表示，描述电子的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在周期性[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中的行为。电子可能的 $\vec{k}$ 值范围由“动量空间”中一个称为**[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)**的区域定义。对于一个典型晶体，该区的宽度约为 $\frac{\pi}{a}$，其中 $a$ 是[晶格常数](@keyword=lattice_constant|lang=zh-CN|style=Feynman)（原子间距），大约为0.5纳米。那么，可见光[光子](@keyword=photon|lang=zh-CN|style=Feynman)的动量是多少？[光子](@keyword=photon|lang=zh-CN|style=Feynman)的动量是 $\frac{2\pi}{\lambda}$，其中 $\lambda$ 是其波长，约为550纳米。

如果你计算一下比值，会发现[光子](@keyword=photon|lang=zh-CN|style=Feynman)的动量与电子世界的尺度相比完全是微不足道的——大约是 $\frac{2a}{\lambda} \approx 0.002$ [@problem_id:1784080]。这意味着当电子吸收[光子](@keyword=photon|lang=zh-CN|style=Feynman)时，它获得了大量能量，但几乎没有获得动量。这就像一个静止站立的人接住一个乒乓球；他吸收了球的能量，但几乎不会被撞离原地。

这对我们绘制[能带图](@keyword=energy_band_diagram|lang=zh-CN|style=Feynman)有巨大影响。由于电子的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)动量 $\vec{k}$ 在吸收过程中几乎不变，因此跃迁在能量对动量（$E$-$\vec{k}$）图上必须是一条**竖直线**。这被称为**直接跃迁**，而那些[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)最低点恰好位于价带最高点正上方的材料，被称为具有**直接带隙**。这些材料，如砷化镓（GaAs），在吸收和发射光方面非常高效。

但是，如果导带的最低点*不*与价带的最高点对齐呢？这就是**[间接带隙](@keyword=indirect_bandgap|lang=zh-CN|style=Feynman)**材料（如硅）的情况。要让电子完成跃迁，它不仅需要[光子](@keyword=photon|lang=zh-CN|style=Feynman)的能量，还需要一个显著的动量“踢”，以使其从[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)的一个点到达另一个点。它通过与一个**[声子](@keyword=phonons|lang=zh-CN|style=Feynman)**——晶格振动的量子——同时相互作用来获得这个动量踢。这种[三体](@keyword=trisomy|lang=zh-CN|style=Feynman)探戈（电子、[光子](@keyword=photon|lang=zh-CN|style=Feynman)、[声子](@keyword=phonons|lang=zh-CN|style=Feynman)）的事件发生概率要低得多，这就是为什么硅的[发光效率](@keyword=luminous_efficacy|lang=zh-CN|style=Feynman)远低于GaAs，这一事实对制造硅基激光器具有深远的影响。

仿佛这些规则还不够，还有一个更微妙、根植于对称性的复杂层次。即使在[直接带隙](@keyword=direct_bandgap|lang=zh-CN|style=Feynman)材料中，如果价带和[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)具有相同的宇称（一种[量子力学对称性](@keyword=quantum_mechanics_symmetry|lang=zh-CN|style=Feynman)），跃迁也可能是**光学禁戒**的。支配[光与物质相互作用](@keyword=light_matter_interaction|lang=zh-CN|style=Feynman)的偶极算符具有[奇宇称](@keyword=odd_parity|lang=zh-CN|style=Feynman)，因此要使[跃迁概率](@keyword=transition_probability|lang=zh-CN|style=Feynman)不为零，初始态和最终态必须具有*相反*的宇称。如果它们不具备相反宇称，那么带边的跃迁就是禁戒的，尽管对于偏离绝对最小值/最大值的电子来说，这种跃迁可以变得弱允许 [@problem_id:2814808]。看来，大自然有一本丰富而详细的规则手册！

### 改变规则：掺杂、无序与挑战

[完美晶体](@keyword=perfect_crystal|lang=zh-CN|style=Feynman)的世界是优雅的，但真实世界的材料通常更混乱——也更有趣。我们可以有意地引入“缺陷”来调整[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)的性质，这个过程称为**掺杂**。

通过添加极少量的杂质原子，我们可以产生一群**自由载流子**——[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)中的电子（n型掺杂）或[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)中的“空穴”（[p型掺杂](@keyword=p_type_doping|lang=zh-CN|style=Feynman)）。这些自由载流子不束缚于任何特定原子，并能在晶体中移动。它们的行为很像金属中的电子，形成一个能与光相互作用的“等离子体”。对于低能量[光子](@keyword=photon|lang=zh-CN|style=Feynman)（例如红外光），这些自由载流子可以使[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)变得高度反射，这种现象称为等离子体反射。通过测量这种反射率最小的频率，我们甚至可以计算出我们添加的自由载流子的数量 [@problem_id:1779139]。

如果我们对[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)进行重度掺杂会发生什么？在这里，[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)再次以一种美妙而违反直觉的方式发挥作用。如果我们在导带底部塞入足够多的电子（重度n型掺杂），它们会填满所有可用的能态，直到某个能量——[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)现在位于[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)*内部*。被[光子](@keyword=photon|lang=zh-CN|style=Feynman)从[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)激发的新电子不能再落在[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)底部；那里已经满了！它必须跳到费米能级*之上*的未占据态。这有效地增加了吸收所需的能量。吸收边移动到更高的能量（“[蓝移](@keyword=blueshift|lang=zh-CN|style=Feynman)”），使材料对它本应吸收的光变得透明。这种显著的现象被称为**Burstein-Moss位移** [@problem_id:1320323]。通过填充最低能态，我们设计出了一个更大的“光学”[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。

无意的混乱，或称**无序**，也会改变规则。在像玻璃这样的**非晶**材料中，没有完美的、重复的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。这种长程有序的缺失对[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)产生了深远的影响。无序状态不会形成清晰、明确的带边，而是创造了大量局域化的能态，这些能态从[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)中“拖尾”而出，延伸到[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)中。这些被称为**[Urbach尾](@keyword=urbach_tail|lang=zh-CN|style=Feynman)**。这些尾态充当了垫脚石，使材料能够吸收能量*小于*理想[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的[光子](@keyword=photon|lang=zh-CN|style=Feynman)。这就是为什么[非晶硅](@keyword=amorphous_silicon|lang=zh-CN|style=Feynman)的[吸收边](@keyword=absorption_edge|lang=zh-CN|style=Feynman)是一个平缓的斜坡，而不是其晶体对应物中看到的陡峭悬崖 [@problem_id:1322640]。

### 跃迁之外：电子与空穴之舞

到目前为止，我们一直将光激发描绘成一次单向旅程：一个电子吸收一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)，被提升到[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)，在价带中留下一个**空穴**（即电子的缺失）。我们假设它们随后各奔东西。但电[子带](@keyword=miniband|lang=zh-CN|style=Feynman)负电，而空穴表现得像一个正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。异性相吸！

如果它们并没有真正自由，而是形成一个束缚对，在晶体中漂移时相互环绕呢？这个束缚的电子-空穴对是一个新实体，一个称为**激子**的**[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)**。[激子](@keyword=excitons|lang=zh-CN|style=Feynman)就像一个生活在[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)内部的微小、短暂的氢原子。电子扮演电子的角色，空穴扮演质子的角色，而晶体本身则充当它们存在的真空。静电吸引力被周围的原子“屏蔽”或削弱了，而且这些粒子的有效质量也不同于自由电子的质量。

这个简单而美妙的想法，超越了“独立粒子”图像，彻底重塑了我们对吸收边的理解 [@problem_id:3008361]。创建一个束缚的激子所需的能量比创建一个必须被撕开的自由[电子和空穴](@keyword=electrons_and_holes|lang=zh-CN|style=Feynman)要*少*一点。能量差就是**[激子束缚能](@keyword=exciton_binding_energy|lang=zh-CN|style=Feynman)**。这意味着我们应该看到吸收不是在[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $E_g$ 处开始，而是在一个稍低的能量 $E_g - E_{binding}$ 处开始。的确，在高质量[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)的低温[吸收光谱](@keyword=absorption_spectrum|lang=zh-CN|style=Feynman)中，我们在主吸收边正下方看到了一系列尖锐、清晰的峰。这些是激子在其[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)（$n=1$）和[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)（$n=2, 3, ...$）被创造出来的指纹 [@problem_id:1808468]。

完整的理论，由**Bethe-Salpeter方程**概括，提供了一幅完整而统一的图景。它表明，库仑吸引力做了两件事。首先，它将一部分吸收强度，或称**[振子强度](@keyword=oscillator_strength|lang=zh-CN|style=Feynman)**，从[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)上方的自由粒子态连续区中拉出，并将其集中到[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)下方的尖锐、强烈的激子峰中。其次，即使在能量高于[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)、电子和空穴自由的情况下，它们之间挥之不去的吸引力也使它们更有可能在彼此附近被发现。这种**Sommerfeld增强**效应提升了在带边及带边以上区域的[吸收概率](@keyword=absorption_probability|lang=zh-CN|style=Feynman)。结果是一次戏剧性的转变：[独立粒子模型](@keyword=independent_particle_model|lang=zh-CN|style=Feynman)中简单的、斜坡状的吸收起始被一个由尖锐峰值和其后增强的连续区组成的新景象所取代 [@problem_id:2996684] [@problem_id:3008361]。这才是[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)中光吸收的真实面貌——一个由光、电子和[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)本身之间的量子之舞所产生的丰富而动态的过程。