## 引言
[光与物质的相互作用](@keyword=interaction_of_light_and_matter|lang=zh-CN|style=Feynman)是基础性的，它决定了从宝石的颜色到智能手机屏幕功能的一切。这些现象的核心是一个关键的量子过程：[电子带间跃迁](@keyword=electronic_interband_transitions|lang=zh-CN|style=Feynman)，即电子通过吸收一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)从一个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)跃迁到另一个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)。但是，为什么硅是一种差劲的光源，而砷化镓（Gallium Arsenide）却为我们的LED提供动力？为什么金是黄色的，而大多数其他金属都是银色的？回答这些问题需要我们进入晶体中电子的量子世界。

本文将揭示这场量子之舞的规则。在第一章“原理与机制”中，我们将探讨支配这些跃迁的基本法则，包括能量、动量的作用，以及[直接带隙与间接带隙](@keyword=direct_vs_indirect_gap|lang=zh-CN|style=Feynman)的关键区别。随后，在“应用与[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)学科联系”中，我们将见证这些原理如何通过[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)的视[角解](@keyword=corner_solution|lang=zh-CN|style=Feynman)释[金的颜色](@keyword=color_of_gold|lang=zh-CN|style=Feynman)，如何促成[相变存储器](@keyword=phase_change_memory|lang=zh-CN|style=Feynman)等技术，以及如何在石墨烯（graphene）和新兴的[谷电子学](@keyword=valleytronics|lang=zh-CN|style=Feynman)（valleytronics）等先进材料领域开辟新前沿。

## 原理与机制

想象一下，你正试图把一个球扔给站在楼梯上的朋友。为了能成功接住球，一些简单的事情必须成立。首先，你必须用足够的能量扔球，才能让球到达你朋友所在的台阶。其次，同样重要的是，你的朋友必须*在*那个台阶上，而且那个台阶不能已经有别人占了！在晶体内部的电子量子世界里，吸收光粒子——[光子](@keyword=photon|lang=zh-CN|style=Feynman)——的规则惊人地相似。这个简单的类比揭开了为何某些材料发光璀璨，而另一些则透明或不透明的全部故事。

### 两条基本法则：能量和占据

让我们从支配电子与光相互作用的两条最基本规则开始。

首先，**能量必须守恒**。当一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)撞击一个电子时，它可以将电子踢到更高的能级。这只有在[光子能量](@keyword=photon_energy|lang=zh-CN|style=Feynman) $E_{\text{photon}} = \hbar\omega$（其中 $\hbar$ 是[约化普朗克常数](@keyword=reduced_planck_constant|lang=zh-CN|style=Feynman)，$\omega$ 是光的角频率）恰好等于电子初末态能量差时才可能发生：$E_{final} - E_{initial} = \hbar\omega$。不多也不少。

其次，必须遵守**[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)**。该原理是量子世界不动产的终极法则：没有两个电子可以同时占据完全相同的状态。这意味着，要想让我们的电子发生跃迁，其目的地——最终的能量状态——必须是空的且可用的。

这两条规则完美地解释了一个基本现象。为什么在绝对零度下，一个完美的[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)对低能量光是透明的，而金属却不透明并会吸收它？让我们看看它们的电子“阶梯”，即**能带结构**。在[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)中，电子完全填满了一个称为**[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)**的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)。与[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)相隔一个巨大能量“[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)” $E_g$ 的，是一个称为**导带**的完全空的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)。如果一个能量小于[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)（$E_{\text{photon}} \lt E_g$）的[光子](@keyword=photon|lang=zh-CN|style=Feynman)到来，它没有足够的能量将一个电子从填满的价带踢过[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)到达空的导带。因此，这样的**[带间跃迁](@keyword=interband_transitions|lang=zh-CN|style=Feynman)**（在[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)之间的跳跃）是被禁止的。那么，在价带*内部*进行一次较小的跳跃呢？那将是**[带内跃迁](@keyword=intraband_transition|lang=zh-CN|style=Feynman)**。这时，能量可能刚好，但泡利原理介入了：所有邻近的状态都已被其他电子占据。目的地已满。由于没有可行的移动，电子干脆忽略了[光子](@keyword=photon|lang=zh-CN|style=Feynman)，光便穿透过去。[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)是透明的。

现在，考虑一个金属。其定义性特征是有一个仅被部分填充的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)。在零温下，最高占据能级被称为**[费米能](@keyword=fermi_energy|lang=zh-CN|style=Feynman)** $E_F$。就在这个能级之上，*同一[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)内*有大量未被占据的状态。当一个低能量[光子](@keyword=photon|lang=zh-CN|style=Feynman)到来时，一个刚好在[费米能](@keyword=fermi_energy|lang=zh-CN|style=Feynman)下方的电子可以轻易找到一个空态跃迁过去，同时满足[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)和泡利原理。这些[带内跃迁](@keyword=intraband_transition|lang=zh-CN|style=Feynman)很容易发生，因此[光子](@keyword=photon|lang=zh-CN|style=Feynman)被吸收。这就是为什么金属不透明且有光泽——它们在很宽的能量范围内高效反射光 [@problem_id:1784042]。

### 晶体的运动法则：[垂直跃迁](@keyword=vertical_transitions|lang=zh-CN|style=Feynman)

到目前为止，我们的规则似乎很简单。但当我们考虑到电子生活在晶体奇妙的周期性和对称环境中时，就会出现一个美妙的微妙之处。在这个世界里，电子具有一种称为**晶体动量**的属性，用矢量 $\mathbf{k}$ 表示。它不同于真空中自由粒子的动量，但在晶体内部，它的行为类似于动量，并且也必须守恒。

所以，我们有第三条规则：**晶体动量必须守恒**。当一个初始动量为 $\mathbf{k}_{i}$ 的电子吸收一个动量为 $\mathbf{k}_{\text{photon}}$ 的[光子](@keyword=photon|lang=zh-CN|style=Feynman)时，它的最终动量必须为 $\mathbf{k}_{f} = \mathbf{k}_{i} + \mathbf{k}_{\text{photon}}$。

这似乎让事情变得复杂，但一个绝妙的简化随之而来。让我们问问：可见光的[光子](@keyword=photon|lang=zh-CN|style=Feynman)究竟携带多少动量？[光子](@keyword=photon|lang=zh-CN|style=Feynman)的动量与其波长 $\lambda$ 相关。晶体中典型的[晶格常数](@keyword=lattice_constant|lang=zh-CN|style=Feynman)——原子间距——约为 $a \approx 0.5$ 纳米。这决定了晶体“动量空间”的尺度，其大小约为 $\pi/a$。可见光[光子](@keyword=photon|lang=zh-CN|style=Feynman)的波长约为 $\lambda \approx 500$ 纳米。因此，其动量大约比晶体动量空间的尺度小1000倍 [@problem_id:2982257]。在电子世界的尺度上，来自[光子](@keyword=photon|lang=zh-CN|style=Feynman)的动量“踢”动完全可以忽略不计！

这引导我们得出一个强大而优雅的近似：我们可以设定 $\mathbf{k}_{\text{photon}} \approx \mathbf{0}$。动量守恒规则于是戏剧性地简化为 $\mathbf{k}_{f} \approx \mathbf{k}_{i}$。这就是著名的**[垂直跃迁](@keyword=vertical_transitions|lang=zh-CN|style=Feynman)规则**。如果我们将电子的能级对[晶体动量](@keyword=crystal_momentum|lang=zh-CN|style=Feynman)作图（$E$-$\mathbf{k}$ 图），一次[光学跃迁](@keyword=optical_transitions|lang=zh-CN|style=Feynman)就对应于一个电子垂直向上跳跃，其水平位置（$\mathbf{k}$）没有变化。

### 两种跃迁的故事：直接与间接

这个“[垂直跃迁](@keyword=vertical_transitions|lang=zh-CN|style=Feynman)”规则迫使我们将[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)分为两个截然不同的家族，它们具有迥异的光学性质。

在**[直接带隙半导体](@keyword=direct_gap_semiconductor|lang=zh-CN|style=Feynman)**中，如砷化镓（Gallium Arsenide, GaAs），填充的价带顶（[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)顶，VBM）和空的导带底（导带底，CBM）出现在[晶体动量](@keyword=crystal_momentum|lang=zh-CN|style=Feynman)的相同值处，通常在 $\mathbf{k}=\mathbf{0}$。这非常方便！一个处于VBM的电子可以吸收一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)并垂直向上直接跳到CBM，完美地满足我们所有的规则。这是一个简单的、直接的双体相互作用过程（电子和[光子](@keyword=photon|lang=zh-CN|style=Feynman)），这使其成为一个高概率的，或称**一阶**过程。反之亦然：一个在CBM的电子可以轻易地落回价带，发射一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)。这就是为什么[直接带隙半导体](@keyword=direct_gap_semiconductor|lang=zh-CN|style=Feynman)是优良的发光体，并构成了我们的LED和[激光二极管](@keyword=laser_diode|lang=zh-CN|style=Feynman)的基础 [@problem_id:2484959] [@problem_id:3002201]。

在**间接带隙[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)**中，如硅（Silicon, Si），情况就没那么配合了。VBM和CBM位于*不同*的晶体动量值处。一个在[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)顶的电子不能直接垂直跳到导带底；那会违反[垂直跃迁](@keyword=vertical_transitions|lang=zh-CN|style=Feynman)规则。为了进行能量最低的跃迁，电子需要从[光子](@keyword=photon|lang=zh-CN|style=Feynman)那里获得能量，*并*显著改变其动量。由于[光子](@keyword=photon|lang=zh-CN|style=Feynman)无法提供所需的动量，电子需要第三方的帮助：一个**[声子](@keyword=phonons|lang=zh-CN|style=Feynman)**，也就是[晶格振动](@keyword=crystal_lattice_vibrations|lang=zh-CN|style=Feynman)的量子。

可以把它想象成一个三体碰撞：电子吸收[光子](@keyword=photon|lang=zh-CN|style=Feynman)获得能量，同时吸收或发射一个[声子](@keyword=phonons|lang=zh-CN|style=Feynman)以提供所需的动量“踢”动（$\mathbf{k}_{f} \approx \mathbf{k}_{i} \pm \mathbf{k}_{\text{phonon}}$）。因为这是一个更复杂的**二阶**事件，它发生的可能性要小得多。这种根本性的低效率正是为什么硅——电子工业无可争议的冠军——在制造激光器方面是一种非常差的材料。它可以（在[声子](@keyword=phonons|lang=zh-CN|style=Feynman)的帮助下）吸收光，但在发光方面却非常糟糕 [@problem_id:2484959] [@problem_id:3002201]。

### 细节条款：对称性、自旋和束缚对

[能量和动量守恒](@keyword=conservation_of_energy_and_momentum|lang=zh-CN|style=Feynman)是大的法则，但正如物理学中常有的那样，总有一些引人入胜的细节。

**对称性规则**：宇宙偏爱对称性，并用它来决定哪些过程是允许的，哪些是禁止的。电子的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)（其[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)）具有一定的对称性，与之相互作用的光场也一样。一个跃迁只有在初态、末态和相互作用本身的对称性以群论的数学语言所规定的方式相匹配时，才是“允许的”。要使跃迁发生，这些对称性的乘积必须包含“全对称”表示。这一深刻的原理意味着，即使能量和动量都守恒，一个跃迁仍可能仅仅因为它具有“错误”的形状而被禁止 [@problem_id:2914657]。

**自旋守恒**：电子还有一个称为自旋的内禀量子属性。吸收一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)会翻转电子的自旋吗？通常不会。光波的电场与电子的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)相互作用，影响其轨道运动，但并不直接与自旋“对话”。这引出了另一条[选择定则](@keyword=selection_rules|lang=zh-CN|style=Feynman)：$\Delta S_z = 0$，自旋是守恒的。即使光是[圆偏振](@keyword=circular_polarization|lang=zh-CN|style=Feynman)的并携带角动量，该角动量通常也会转移到电子的*轨道*运动上，而不是其自旋。用光来翻转电子的自旋通常需要一种更微妙的效应，称为**[自旋-轨道耦合](@keyword=l_s_coupling|lang=zh-CN|style=Feynman)**，这是一种将电子运动与其自旋联系起来的[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)现象，在许多现代材料中很重要，但它不是光的**一阶**效应 [@problem_id:3015268]。

**激子**：当电子跃迁到导带后，它在价带中留下一个“空穴”——一个带净正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的点。是什么阻止这个带负电的电子和带正电的空穴相互吸引呢？什么也阻止不了！它们可以形成一个[束缚态](@keyword=bound_states|lang=zh-CN|style=Feynman)，一种在晶体内部运行的量子“氢原子”。这个束缚的电子-空穴对是一种新的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，称为**[激子](@keyword=excitons|lang=zh-CN|style=Feynman)**。形成激子所需的能量比创造一个完全自由的[电子和空穴](@keyword=electrons_and_holes|lang=zh-CN|style=Feynman)要稍微少一些，因为在束缚它们的过程中释放了一些能量。因此，当你观察一个真实[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)的吸收光谱时，你经常会看到一个尖锐的吸收峰出现在能量*略低于*主直接带隙的地方。这个峰是[激子](@keyword=excitons|lang=zh-CN|style=Feynman)形成的标志，是多体物理在材料光学性质中体现的一个美丽例子 [@problem_id:2799066]。

### 调控内部之光：[Burstein-Moss效应](@keyword=burstein_moss_effect|lang=zh-CN|style=Feynman)

理解这些规则不仅仅是学术练习；它使我们能够设计[材料的光学性质](@keyword=optical_properties_of_materials|lang=zh-CN|style=Feynman)。一个完美的例子是**Burstein-Moss位移**。

想象一下，我们取一个[直接带隙半导体](@keyword=direct_gap_semiconductor|lang=zh-CN|style=Feynman)，并对其进行重“掺杂”，添加大量的额外电子。这些电子将开始填充曾经空置的导带底部，形成一个深电子池，直至一个新的[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)。现在，当我们用能量等于[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的光照射时会发生什么？[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)中的一个电子试图进行其通常的[垂直跃迁](@keyword=vertical_transitions|lang=zh-CN|style=Feynman)到导带底。但它做不到！[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)说“拒绝访问”——那个状态已经被占据了。

为了被吸收，[光子](@keyword=photon|lang=zh-CN|style=Feynman)必须具有*更高*的能量，足以将电子从[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)一直提升到费米能级*上方*的一个空态。最低能量的[允许跃迁](@keyword=allowed_transitions|lang=zh-CN|style=Feynman)不再是[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) $E_g$，而是一个更高的能量，该能量取决于导带的填充程度。表观光学[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)已移动到更高的能量——它被“蓝移”了。[吸收边](@keyword=absorption_edge|lang=zh-CN|style=Feynman)能量的这种增加就是Burstein-Moss位移 [@problem_id:3008366]。这种效应不仅仅是一个奇观；它是[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)和触摸屏中使用的[透明导电氧化物](@keyword=transparent_conducting_oxides|lang=zh-CN|style=Feynman)（TCO）背后的原理。通过对材料进行重掺杂，使其表观[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)被推到可见光范围之外，我们可以使其在导电的同时对可见光保持透明。

从几条简单的量子规则出发，一个丰富而复杂的图景浮现出来，它不仅解释了我们周围的世界，也给了我们设计世界的工具。由能量、动量和对称性法则支配的电子与[光子](@keyword=photon|lang=zh-CN|style=Feynman)之舞，是光学世界的引擎。