## 引言
在我们熟悉的三维世界里，粒子的行为遵循一套公认的规则。例如，金属中的电子被理解为独立的实体，尽管存在复杂的相互作用，它们在很大程度上仍保持其完整性。但是，当我们把这个世界限制在一条直线上时，会发生什么呢？我们从三维经验中建立的直觉将会被颠覆，一个奇异而崭新的现实随之显现。这是一维物理学的领域，在这里，处于“交通堵塞”状态的粒子无法再相互避让，从而导致量子行为的彻底重塑。本文要解决的核心问题是，我们标准的物理模型——如Landau的[费米液体理论](@keyword=fermi_liquid_theory|lang=zh-CN|style=Feynman)——在这种受限的几何结构中如何失效，以及全新的集体现象如何涌现。

本文将分两部分引导您探索这个迷人的领域。首先，在“原理与机制”部分，我们将探讨主导[一维系统](@keyword=one_dimensional_systems|lang=zh-CN|style=Feynman)的基本概念，从单个杂质的巨大影响到被称为朝永-[Luttinger液体](@keyword=luttinger_liquid|lang=zh-CN|style=Feynman)的集体[物质状态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)。我们将揭示一个电子“瓦解”、完美序不复存在的世界背后的理论基础。随后，“应用与跨学科联系”一章将证明，这并非仅仅是理论上的幻想。我们将审视这些现象在真实[量子材料](@keyword=quantum_materials|lang=zh-CN|style=Feynman)中惊人的实验证据，观察它们在可测量性质中留下的印记，并发现它们与[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学、[拓扑物质](@keyword=topological_matter|lang=zh-CN|style=Feynman)和先进计算物理学之间出人意料的联系。准备好进入一个规则迥异、我们所熟知的电子不复存在的世界吧。

## 原理与机制

想象一个被限制在一条直线上的世界。不是一个平面，也不是三维空间，而是一个被局限在一条窄线上的宇宙。这不仅仅是一个几何上的奇特设定；在这个领域里，基本物理定律的展现方式截然不同。在我们熟悉的三维世界里，粒子就像宏大舞厅里的舞者——他们可以相互绕行、侧步避让、避免碰撞。而在一个维度中，他们就像高峰时段挤在单车道隧道里的通勤者。没有“绕行”可言，只有“通过”或“返回”。这条简单的规则——**不可穿越规则**——是解开[一维系统](@keyword=one_dimensional_systems|lang=zh-CN|style=Feynman)奇异而美妙物理学的钥匙。

### 一维交通堵塞：一个无法超越的世界

让我们从最基本的量子相互作用开始：单个粒子遇到一个势垒。在三维空间中，一个低能粒子接近一个小障碍物时，很可能会绕过它。你可以把它想象成大池塘中的水波遇到一根小柱子；水波轻易地绕过它，继续前进。障碍物几乎没有产生影响，散射很弱。

在一维空间中，情况则完全相反。想象一下，沿着一根细线，将一个量子粒子（一个[波包](@keyword=wave_packets|lang=zh-CN|style=Feynman)）射向一个小缺陷或杂质。由于粒子无法绕过势垒，它只有两个选择：透射过去或被反射回来。量子力学中一个非凡的结果是，在极低能量下，一维空间中的粒子几乎**必然**会被**任何**势垒反射，无论这个势垒多么小或多么弱。波没有足够的能量来有效地隧穿，并且由于没有其他路径可选，它只能返回。与之形成对比的是三维情况，在三维中[低能散射](@keyword=low_energy_scattering|lang=zh-CN|style=Feynman)是各向同性的，并由单一参数——**[散射长度](@keyword=scattering_length|lang=zh-CN|style=Feynman)**——来描述，它代表了靶的有效尺寸。但在二维中，对于一个通用势垒，低能[透射概率](@keyword=transmission_probability|lang=zh-CN|style=Feynman) $T$ 会骤降至零，而反射概率 $R$ 则趋近于一 [@problem_id:2117203]。这种“交通堵塞”是完全的。对障碍物的这种极端敏感性是第一个迹象，表明[一维系统](@keyword=one_dimensional_systems|lang=zh-CN|style=Feynman)是完全不同的一类事物。

### 箱中波与环上波

这种受限的几何结构对波（包括粒子的量子波函数）的存在方式产生了深远的影响。如果我们将一个粒子限制在长度为 $L$ 的一维线段上，就像两端固定的吉他弦一样，我们就施加了**[固定边界条件](@keyword=clamped_boundary_conditions|lang=zh-CN|style=Feynman)**。[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)必须在两端为零。这个约束只允许形成一组离散的[驻波](@keyword=standing_waves|lang=zh-CN|style=Feynman)，其波长 $\lambda$ 必须恰好能容纳在箱子中：$\lambda_n = 2L/n$，其中 $n$ 是一个正整数。

我们也可以想象我们的一维宇宙是一个闭环，就像一条项链。这施加了**周期性边界条件**，即[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在环的起点和终点必须有相同的值，$\psi(x) = \psi(x+L)$。这允许*行进*波在环[上循环](@keyword=cocycles|lang=zh-CN|style=Feynman)，其允许的波长为 $\lambda_m = L/|m|$，其中 $m$ 是任意非零整数。请注意，对于相同的波长范围，这两种情况允许的模式（或[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)）数量可能不同。例如，在周期性情况下，对于每个波长，都有两种不同的模式，分别对应顺时针和逆时针传播的波，这是驻波情况中所没有的自由度 [@problem_id:1960001]。这种“态的计数”不仅仅是学术练习；它是理解从热物体颜色（[黑体辐射](@keyword=blackbody_radiation|lang=zh-CN|style=Feynman)）到固体[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)等一切事物的基础。

### 原子链：[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的交响乐

让我们将我们的一维世界从单个粒子构建成一个集体。想象一条由弹簧连接的原子链——一个一维晶体的简单模型。当这些原子[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)时，它们的运动以波的形式沿着链传播，这些波被称为**[声子](@keyword=phonons|lang=zh-CN|style=Feynman)**，即声音的量子粒子。

如果所有原子都具有相同的质量 $M$，那么情况就相对简单。振动频率形成一个连续的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)，称为**[声学支](@keyword=acoustic_branch|lang=zh-CN|style=Feynman)**，因为在长波长下它描述的是普通[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)。但是，如果我们让这条链变得更有趣，让两种不同质量 $m_1$ 和 $m_2$ 的原子交替[排列](@keyword=permutation|lang=zh-CN|style=Feynman)呢？突然之间，[色散关系](@keyword=dispersion_relations|lang=zh-CN|style=Feynman)——即频率 $\omega$ 和波矢 $k$ 之间的关系——分裂成两个截然不同的分支。较低的那个仍然是[声学支](@keyword=acoustic_branch|lang=zh-CN|style=Feynman)，其中相邻的原子同步运动。但出现了一个新的、频率更高的分支：**[光学支](@keyword=optical_branch|lang=zh-CN|style=Feynman)**。在这里，一个晶胞中的两种不同原子做反向运动。这些模式可以被光激发，因此得名。

这两种原子的存在使晶体的重复[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)尺寸增加了一倍。如果我们神奇地将质量调至相等，$m_1 = m_2 = M$，就会发生一件有趣的事情。[声学支](@keyword=acoustic_branch|lang=zh-CN|style=Feynman)和[光学支](@keyword=optical_branch|lang=zh-CN|style=Feynman)之间的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)在新的、更小的布里渊区边缘闭合，[色散关系](@keyword=dispersion_relations|lang=zh-CN|style=Feynman)折叠回晶格间距为一半的简单[单原子链](@keyword=monoatomic_chain|lang=zh-CN|style=Feynman)的色散关系。这是一个绝佳的例子，说明了对称性如何决定一个系统的基本模式 [@problem_id:1795255]。曾经的两种不同原子变成了一种，物理学也反映了这种潜在的统一性。

### 电子集体：独行侠的瓦解

现在我们加入固态世界中最重要的角色：电子。在典型的三维金属中，电子尽管彼此相互作用，但其行为却出人意料地简单。Landau的**[费米液体理论](@keyword=fermi_liquid_theory|lang=zh-CN|style=Feynman)**告诉我们，金属中的电子就像一个“自由”粒子，只是质量被修正了，并且寿命非常长。这种**[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)**是一个独行侠，携带着它的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)（$e$）和自旋（$\frac{1}{2}$）作为一个不可分割的整体。这个图像在三维空间中取得了令人难以置信的成功。

在一维空间中，这个图像完全被打破。“不可穿越规则”卷土重来。一维导线中的电子受到如此严格的限制，以至于它们不能再被视为独立的。任何一个电子的运动都会立即影响所有其他电子。集体性占据了主导地位。单个[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的概念本身就失效了。取而代之的是，系统的低能激发是电子流体的电荷密度和自旋密度的集体波状[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。取代了一维[费米液体](@keyword=fermi_liquid|lang=zh-CN|style=Feynman)的这种新物态被称为**朝永-[Luttinger液体](@keyword=luttinger_liquid|lang=zh-CN|style=Feynman)**（TLL）。

因为[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)图像是无效的，所以像[随机相近似](@keyword=random_phase_approximation_(rpa)|lang=zh-CN|style=Feynman)（RPA）这样建立在准[粒子-空穴激发](@keyword=particle_hole_excitations|lang=zh-CN|style=Feynman)思想上的标准理论工具，在一维中会得出定性上错误的结论 [@problem_id:3008847]。我们需要新的方法，例如针对某些自旋模型的精确**[Jordan-Wigner变换](@keyword=jordan_wigner_transformation|lang=zh-CN|style=Feynman)** [@problem_id:2994900] 或强大的场论技巧**[玻色化](@keyword=bosonization|lang=zh-CN|style=Feynman)** [@problem_id:3021851]。

### 分裂的电子：[自旋-电荷分离](@keyword=spin_charge_separation|lang=zh-CN|style=Feynman)的奇迹

这里我们来到了一维物理学中最奇异和最著名的现象：**[自旋-电荷分离](@keyword=spin_charge_separation|lang=zh-CN|style=Feynman)**。由于基本激发是[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)和自旋的集体波，事实证明电子的这两个属性可以*独立*传播。

想象一排手拉手的人，代表导线中的电子。每个人都有一个“[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)”（他们的位置）和一个“自旋”（比如他们是面朝前还是面朝后）。如果一个人离开队伍（制造一个空穴），他后面的每个人都向前移动一步来填补空缺。这个扰动——[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)的移动——是一个沿着队伍传播的集体波。这就是一个**空穴子**（holon），一种携带[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)但没有自旋的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)。

现在，想象队伍中的一个人转过身。为了传达这个变化，他可以拍一下他的邻居，然后邻居也转过身再拍下一个邻居，依此类推。一个“转身”的波沿着队伍传播，但没有人实际改变他们的位置。这就是一个**自旋子**（spinon），一种携带自旋但[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为零的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)。

在朝永-[Luttinger液体](@keyword=luttinger_liquid|lang=zh-CN|style=Feynman)中，发生的情况正是如此。如果你向一维导线中注入一个电子，它会分解成一个空穴子和一个自旋子 [@problem_id:3017361]。这两种新粒子随后以不同的速度沿线传播，[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)波的速度为 $v_c$，[自旋波](@keyword=spin_waves|lang=zh-CN|style=Feynman)的速度为 $v_s$。我们所知的电子，在这个世界里无法作为稳定的粒子存在。这个非凡的预言，源于像**Hubbard模型** [@problem_id:3019521] 等模型的精确数学解，已在准一维材料的实验中得到证实，是集体量子效应强大力量的惊人证明。

### 当电流停止时：一维的奇特绝缘体

相互作用的独特 interplay 也会导致奇怪的绝缘态。考虑一个每个原子上有一个电子的[一维链](@keyword=one_dimensional_chains|lang=zh-CN|style=Feynman)。直观上看，这个“半满”[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)应该是一个金属。但在**一维**中，它可以通过两种截然不同的机制轻易地变成绝缘体 [@problem_id:1789886]。

1.  **佩尔斯绝缘体 (Peierls Insulator)：**当电子与[晶格振动](@keyword=crystal_lattice_vibrations|lang=zh-CN|style=Feynman)（[声子](@keyword=phonons|lang=zh-CN|style=Feynman)）相互作用时，就会发生这种情况。[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)会发现，通过交替形成短键和长键（[二聚化](@keyword=dimerization|lang=zh-CN|style=Feynman)）来发生畸变，在能量上是有利的。这种[周期倍增](@keyword=period_doubling|lang=zh-CN|style=Feynman)在[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)处打开了一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，从而阻止了电子的流动。在这种状态下，[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)和自旋激发都是有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的——产生任何一种激发都需要能量。

2.  **莫特绝缘体 (Mott Insulator)：**这是一种纯粹的[电子效应](@keyword=electronic_effects|lang=zh-CN|style=Feynman)。如果同一原子上两个电子之间的排斥作用 ($U$) 很强，每个电子就会“卡”在自己的原子上。跳到相邻位点需要克服这个巨大的能量代价，从而产生一个双占据位点。这就打开了一个**[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)**，$\Delta_c > 0$，从而系统变成了绝缘体。这就是莫特绝缘体。但自旋呢？电子被局域化了，但它们的自旋仍然可以相互作用。实际上，低能物理表现为一条相互作用的自旋链，它可以有[无能](@keyword=anergy|lang=zh-CN|style=Feynman)隙的激发。这就导致了一维[莫特绝缘体](@keyword=mott_insulators|lang=zh-CN|style=Feynman)的标志性特征：有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)[部分和](@keyword=partial_sums|lang=zh-CN|style=Feynman)[无能](@keyword=anergy|lang=zh-CN|style=Feynman)隙的自旋部分（$\Delta_s = 0$）。这是[自旋-电荷分离](@keyword=spin_charge_separation|lang=zh-CN|style=Feynman)直接而深刻的结果。[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)流被冻结，但自旋信息的“流”仍然可以[自由流](@keyword=free_streaming|lang=zh-CN|style=Feynman)动。这个[莫特能隙](@keyword=mott_gap|lang=zh-CN|style=Feynman)是由一种称为**U过程散射**（umklapp scattering）的特殊[相干散射](@keyword=coherent_scattering|lang=zh-CN|style=Feynman)过程引起的，这种过程只在像半满这样的整数填充下才可能发生 [@problem_id:3021851]。

### 不完美的序：涨落的主宰

在我们的三维世界里，我们习惯于看到材料在低温下进入完美有序的状态——钻石的完美[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，铁磁体的对齐磁矩。这被称为**[长程序](@keyword=long_range_order|lang=zh-CN|style=Feynman)**。在一维空间中，这种完美的序通常是不可能的。

**[Mermin-Wagner定理](@keyword=mermin_wagner_theorem|lang=zh-CN|style=Feynman)**指出，对于具有[连续对称性](@keyword=continuous_symmetry|lang=zh-CN|style=Feynman)（如磁体中自旋的[旋转对称](@keyword=rotational_symmetry|lang=zh-CN|style=Feynman)性）的系统，一维的[热涨落](@keyword=thermal_fluctuations|lang=zh-CN|style=Feynman)非常强大，以至于在任何高于绝对零度的温度下都会破坏任何[长程序](@keyword=long_range_order|lang=zh-CN|style=Feynman)。即使在零温下，量子涨落也能起到同样的作用。

那么，[一维系统](@keyword=one_dimensional_systems|lang=zh-CN|style=Feynman)会陷入混乱吗？不。它会进入一种更微妙的状态：**[准长程序](@keyword=quasi_long_range_order|lang=zh-CN|style=Feynman)**。想象一条由磁罗盘组成的线。在三维铁磁体中，所有的指针都指向北方。在一维链中，当你沿着线移动时，指针大致指向同一方向，但它们会缓慢地随机漂移。两个指针方向之间的关联不是指数衰减的（如在[无序系统](@keyword=disordered_systems|lang=zh-CN|style=Feynman)中），而是随距离呈缓慢的[幂律衰减](@keyword=power_law_decay|lang=zh-CN|style=Feynman)。这种[幂律衰减](@keyword=power_law_decay|lang=zh-CN|style=Feynman)是朝永-[Luttinger液体](@keyword=luttinger_liquid|lang=zh-CN|style=Feynman)的标志。例如，在一维相互作用的[玻色子](@keyword=boson|lang=zh-CN|style=Feynman)气体中，预示[超流性](@keyword=superfluidity|lang=zh-CN|style=Feynman)的关联函数并非常数，而是按 $G(x) \propto |x|^{-\eta}$ 衰减，其中指数 $\eta$ 直接取决于[相互作用强度](@keyword=interaction_strength|lang=zh-CN|style=Feynman) [@problem_id:1200383]。完美的序消失了，但它的一种美丽的、标度不变的残余存活了下来，这是线上一维生存的直接结果。