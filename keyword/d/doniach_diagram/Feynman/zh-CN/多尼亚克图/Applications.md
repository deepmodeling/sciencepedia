## 应用与跨学科联系

我们已经花了一些时间构建了一个相当精美的智力机器——[多尼亚克图](@keyword=doniach_diagram|lang=zh-CN|style=Feynman)。我们已经看到它如何源于一场在金属心脏地带的量子层面发生的巨大斗争，这场斗争在两种对立的力量之间展开：巡游电子渴望屏蔽和安抚局域磁矩（[近藤效应](@keyword=kondo_effect|lang=zh-CN|style=Feynman)），以及这些磁矩倾向于利用相同的电子作为信使，在它们之间密谋建立集体磁有序（[RKKY相互作用](@keyword=rkky_interaction|lang=zh-CN|style=Feynman)）。

但是，物理学家不会仅仅满足于一个美丽的理论。一个理论，无论多么优雅，都必须面对实验的审判。这个图，这[张量](@keyword=tensor|lang=zh-CN|style=Feynman)子趋势的抽象地图，真的能描述我们握在手中、连接到电压表、并在低温恒温器中冷却的真实金属和磁体的世界吗？答案是响亮的*是*。[多尼亚克图](@keyword=doniach_diagram|lang=zh-CN|style=Feynman)不仅仅是一个理论上的奇珍；它是现代量子世界探索者的实用指南，是[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)不可或缺的工具，也是理解物理学中一些最深奥现象（包括非常规超导之谜）的门户。现在，让我们驾驭这个引擎，看看它能做些什么。

### 物理学家作为材料侦探

想象一下，你拿到了一块新合成的金属晶体。它看起来闪闪发光，就像任何普通金属一样。但你的同事怀疑它可能有些特别，是一种“重费米子”材料。你将如何证实这一点？你需要成为一名侦探，寻找其内部上演的量子戏剧留下的线索。[多尼亚克图](@keyword=doniach_diagram|lang=zh-CN|style=Feynman)恰好告诉你该寻找什么。

第一个、也是最引人注目的线索是材料的[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)。如果内部的电子确实“很重”，它们就会行动迟缓。需要不成比例的能量——即热量——才能使它们移动并提高材料的温度。这通过[低温比热](@keyword=low_temperature_specific_heat|lang=zh-CN|style=Feynman) $C = \gamma T$ 中的[Sommerfeld系数](@keyword=sommerfeld_coefficient|lang=zh-CN|style=Feynman) $\gamma$ 来测量。对于像铜这样的普通金属，$\gamma$ 非常小。而对于重费米子，它可以大上数百甚至数千倍。通过测量 $\gamma$，我们可以直接估算[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman) $m^*$。发现一个 $m^*$ 达到裸电子质量千倍的数值，几乎可以肯定你偶然发现了一个[重费米子系统](@keyword=heavy_fermion_systems_2|lang=zh-CN|style=Feynman) [@problem_id:3018902]。你正在看到的是近藤效应为电子穿上一层厚厚的[量子关联](@keyword=quantum_correlations|lang=zh-CN|style=Feynman)“外衣”的直接后果。

另一个线索来自磁性。如果[近藤效应](@keyword=kondo_effect|lang=zh-CN|style=Feynman)获胜（$T_K > T_{\mathrm{RKKY}}$），[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)就会被屏蔽。在低温下，材料应该不具有磁性。其磁化率不会像自由磁体那样随冷却而发散（[居里定律](@keyword=curie_s_law|lang=zh-CN|style=Feynman)），而是会趋于一个大的常数值，这种行为被称为[泡利顺磁性](@keyword=pauli_paramagnetism|lang=zh-CN|style=Feynman)，但强度要大得多！这种增强的[磁化率](@keyword=susceptibility|lang=zh-CN|style=Feynman) $\chi$ 与增强的比热系数 $\gamma$ 之比给出了一个称为Wilson比的[无量纲数](@keyword=dimensionless_numbers|lang=zh-CN|style=Feynman) $R_W$。对于一个由[近藤物理](@keyword=kondo_physics|lang=zh-CN|style=Feynman)主导的[重费米液体](@keyword=heavy_fermi_liquid|lang=zh-CN|style=Feynman)，理论预测 $R_W \approx 2$。找到一个接近此值的结果，就像DNA匹配一样，确认了其底层物理的身份 [@problem_id:3018902]。

也许最戏剧性的证据来自于测量材料冷却时的电阻率。在普通金属中，电阻率随冷却而下降，因为原子晶格振动减少，导致[电子散射](@keyword=electron_scattering|lang=zh-CN|style=Feynman)减少。但在许多[重费米子化合物](@keyword=heavy_fermion_compounds|lang=zh-CN|style=Feynman)中，发生了奇怪的事情。当从室温冷却它们时，电阻率反而*增加*了！就好像材料越冷，[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)越“差”。这种反直觉的行为是[局域磁矩](@keyword=local_magnetic_moment|lang=zh-CN|style=Feynman)作为独立的、[非相干散射](@keyword=incoherent_scattering|lang=zh-CN|style=Feynman)中心的标志。随着温度下降，来自每个格点的近藤散射变得更强。然后，在一个特征“相干温度” $T^*$ 处，[电阻率](@keyword=electrical_resistivity|lang=zh-CN|style=Feynman)达到峰值并突然骤降。这个峰值并非缺陷的标志；它是一种[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)的优美体现。它标志着电子停止在单个、孤立的磁矩上散射，并开始作为一个单一的、相干的[量子流体](@keyword=quantum_fluids|lang=zh-CN|style=Feynman)——一个[重费米液体](@keyword=heavy_fermi_liquid|lang=zh-CN|style=Feynman)——集体运动的时刻 [@problem_id:3018916]。这种[相干态](@keyword=coherent_states|lang=zh-CN|style=Feynman)的形成最终使得电阻率下降，在最低温下遵循[费米液体](@keyword=fermi_liquid|lang=zh-CN|style=Feynman)的 $T^2$ 定律，但带有一个巨大的前因子，反映了载流子巨大的有效质量。

### 用挤压调控量子宇宙

[多尼亚克图](@keyword=doniach_diagram|lang=zh-CN|style=Feynman)是一张带有控制轴的地图，该控制轴是[无量纲参数](@keyword=nondimensional_parameters|lang=zh-CN|style=Feynman) $J\rho_0$。这就提出了一个诱人的问题：作为实验者，我们能否物理地“转动”一个真实材料的“旋钮”，并观察它在这张地图上移动？值得注意的是，我们可以。实现这一目标最强大的工具之一是静水压力。

挤压晶体会使原子彼此靠得更近。这通常会增加局域 $f$-电子轨道与巡游[传导电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)之间的重叠。结果是更强的杂化，这是驱动近藤交换 $J_K$ 的微观引擎。因此，增加压力通常会增加 $J_K$，并将材料在[多尼亚克图](@keyword=doniach_diagram|lang=zh-CN|style=Feynman)上向右推动 [@problem_id:3018920]。

这一原理引出了一项优美的实验检验。自然界为我们提供了两个非常适合这项研究的元素家族：铈（Ce），带有一个 $f$-电子；和镱（Yb），带有一个 $f$-*空穴*。在某种意义上，它们是粒子-空穴的伙伴。对于常压下通常是[反铁磁体](@keyword=antiferromagnets|lang=zh-CN|style=Feynman)的铈（Ce）基化合物，施加压力会增强 $J_K$，加强近藤效应，并能系统地破坏磁有序，将材料转变为[重费米液体](@keyword=heavy_fermi_liquid|lang=zh-CN|style=Feynman)。你可以亲眼看到磁有序温度 $T_N$ 下降，并在一个[临界压力](@keyword=critical_pressure|lang=zh-CN|style=Feynman) $p_c$ 处消失。

令人惊讶的是，对于许多镱（Yb）基化合物，情况恰恰相反！施加压力会驱使它们*趋向*磁性。这种美丽的非对称性是我们微观理解的惊人证实。在镱中，压力的主要作用是使已填满的 $f^{14}$ 壳层更加稳定，这增加了产生一个空穴的能量成本，从而有效地将 $f$-空穴能级*推离*费米能。这种效应可以压倒杂化的增强，导致 $J_K$ 净*减少*，并将系统在[多尼亚克图](@keyword=doniach_diagram|lang=zh-CN|style=Feynman)上向左移动，朝向由RKKY主导的磁性状态 [@problem_id:3018920]。

通过追踪像Ce基化合物这样的材料，并在用压力调控它时，我们可以在地图上画出一条路径。我们可以观察到反铁磁[Néel温度](@keyword=néel_temperature|lang=zh-CN|style=Feynman) $T_N$ 先是上升，形成一个特征性的“穹顶”，然后随着[近藤屏蔽](@keyword=kondo_screening|lang=zh-CN|style=Feynman)开始压倒[RKKY相互作用](@keyword=rkky_interaction|lang=zh-CN|style=Feynman)而骤降至零。就在磁性消失的[临界压力](@keyword=critical_pressure|lang=zh-CN|style=Feynman) $p_c$ 处，系统进入一个奇异的新领域：量子临界点（QCP）。在这里，由[比热](@keyword=specific_heat|lang=zh-CN|style=Feynman)系数 $\gamma$ 测量的[准粒子有效质量](@keyword=quasiparticle_effective_mass|lang=zh-CN|style=Feynman)达到一个巨大的峰值，然后在另一侧再次下降。这个峰值是系统发出的呼喊，宣告它正处于最大量子涨落的状态，在两种根本不同的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)之间的刀刃上保持平衡 [@problem_id:3018928]。

### 边缘生活：[量子临界性](@keyword=quantum_criticality|lang=zh-CN|style=Feynman)的奇异世界

[量子临界点](@keyword=quantum_critical_point|lang=zh-CN|style=Feynman)不仅仅是相图上的一条边界线。在这里，我们对金属的传统理解会崩溃。在这里，磁性与重液体之间的[量子涨落](@keyword=quantum_fluctuations|lang=zh-CN|style=Feynman)如此强烈和长程，以至于稳定、长寿命的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)电子这一概念本身就不再有效。系统进入一种“[非费米液体](@keyword=non_fermi_liquids|lang=zh-CN|style=Feynman)”状态，其性质由临界现象的普适定律支配，但这是在一个量子的、零温的环境中。

其效应可以是戏剧性的。一个最深刻的观点是“近藤崩坏”的概念，即费米面——动量空间中已占据电子态的海洋——可以在QCP处突然重构。在[重费米液体](@keyword=heavy_fermi_liquid|lang=zh-CN|style=Feynman)中，根据[Luttinger定理](@keyword=luttinger_s_theorem|lang=zh-CN|style=Feynman)，f-电子是电子海洋的一部分，导致一个“大”费米面。在磁性状态下，它们是局域化的，只留下一个由[传导电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)组成的“小”[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)。在QCP处，系统可能会从一种构型跳到另一种。载流子本性的这种剧烈变化将表现为[霍尔系数](@keyword=hall_coefficient|lang=zh-CN|style=Feynman)（一个有效计算载流子数量的物理量）的突然、急剧跳变。在通过[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)或压力调控材料穿过QCP时观察到这样的跳变，是这种深刻的[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)重构的有力标志 [@problem_id:3018895]。

其他[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)量也以各自的方式宣告着与QCP的接近。[Grüneisen参数](@keyword=grüneisen_parameter|lang=zh-CN|style=Feynman) $\Gamma$ 是衡量挤压材料时其温度变化程度的指标——一种热-力学耦合。在普通材料中，它是一个行为良好的数字。但理论预测，当一个系统接近QCP时，这个参数应该会发散，以对调控参数的无限灵敏度“大声疾呼”。这种发散遵循特定的[幂律](@keyword=power_laws|lang=zh-CN|style=Feynman)，已得到实验证实，并成为[量子临界性](@keyword=quantum_criticality|lang=zh-CN|style=Feynman)的一个普适[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)指纹，直接反映了支配QCP附近物理现象的底层标度定律 [@problem_id:3018941]。

### 从混沌到有序：非常规超导的诞生

在量子临界点的涨落[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)中会涌现出什么？通常是某种完全出乎意料且美丽的东西：一种新的有序形式。在许多[重费米子材料](@keyword=heavy_fermion_materials|lang=zh-CN|style=Feynman)中，人们发现一个非常规超导的穹顶拱跨在反铁磁QCP之上。这并非巧合。这是现代物理学中最激动人心的前沿之一，它将磁性世界与超导世界联系起来。

为了实现超导，电子必须形成“[Cooper对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)”。这需要某种“胶水”将它们粘合在一起。在[常规超导体](@keyword=conventional_superconductors|lang=zh-CN|style=Feynman)中，这种胶水由晶格振动（[声子](@keyword=phonons|lang=zh-CN|style=Feynman)）提供。但在反铁磁QCP附近，系统充满了另一种[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)：量子自旋涨落。这些是被刚刚抑制的磁有序留下的短暂、幽灵般的残余。

常识可能会认为，本质上对电子有排斥作用的磁涨落只会拆散电子对。但量子世界是微妙的。由这些[自旋涨落](@keyword=spin_fluctuations|lang=zh-CN|style=Feynman)介导的有效相互作用在表征旧有磁有序的特定动量，即[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman) $Q$ 处，具有强烈的峰值。虽然这种相互作用对于“面对面”的电子是排斥的，但对于以更复杂、非均匀方式[排列](@keyword=permutation|lang=zh-CN|style=Feynman)的一对电子，它可能变得有吸引力。具体来说，它有利于一种配对态，其中Cooper对的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中由 $Q$ 分隔的区域具有相反的符号。这是[非常规超导体](@keyword=unconventional_superconductors|lang=zh-CN|style=Feynman)（如 $d$-波[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)）的标志 [@problem_id:3018867]。这是一个深刻而美丽的讽刺：正是那些标志着一种旧有序消亡的磁涨落，变成了将电子粘合成一种新的、更奇特超导有序的胶水。

### 现实世界是复杂的：环境与无序

到目前为止，我们的旅程都假设晶体是完美的、理想化的。但真实的材料是复杂的。原子的局域环境和缺陷的存在为这个故事增添了新的复杂性——和丰富性。

对于一个 $f$-电子来说，其[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)不仅由自身的自旋和轨道决定，还受到晶体中邻近离子产生的电场的影响。这种[晶体电场](@keyword=crystal_electric_field|lang=zh-CN|style=Feynman)（CEF）可以分裂 $f$-离子的简并能级。这意味着，它可能不再有（比如说）六个可能的状态来参与[近藤效应](@keyword=kondo_effect|lang=zh-CN|style=Feynman)，而可能只有一个由两个态组成的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)二重态，其他态则处于高得多的能量上。有效简并度的这种降低对[近藤温度](@keyword=kondo_temperature|lang=zh-CN|style=Feynman)有戏剧性的、指数级的影响，通常会将其抑制数个[数量级](@keyword=powers_of_ten|lang=zh-CN|style=Feynman)。是整个简并度还是仅[基态简并](@keyword=ground_state_degeneracy|lang=zh-CN|style=Feynman)度起作用，取决于[近藤温度](@keyword=kondo_temperature|lang=zh-CN|style=Feynman)和CEF[能级分裂](@keyword=energy_level_splitting|lang=zh-CN|style=Feynman)之间的竞争，这在某些材料中导致了丰富的、多阶段的屏蔽过程 [@problem_-id:3018926]。这有助于解释为什么含有相同磁性离子的材料会因其[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)不同而具有截然不同的性质。

此外，没有哪个真实晶体是完美的。以缺失原子或杂质形式存在的[淬火无序](@keyword=quenched_disorder|lang=zh-CN|style=Feynman)会产生深远影响，尤其是在QCP附近。无序可能导致并非每个格点都具有相同的[近藤温度](@keyword=kondo_temperature|lang=zh-CN|style=Feynman) $T_K$，而是会产生一个[近藤温度](@keyword=kondo_temperature|lang=zh-CN|style=Feynman)的空间分布。在这种情况下，当冷却材料时，人们不会穿过一个单一的、清晰的边界。相反，人们会发现一个宽泛的温度范围，其中材料的某些区域的磁矩已被屏蔽，而其他区域的则仍然自由。这种“量子[Griffiths相](@keyword=griffiths_phase|lang=zh-CN|style=Feynman)”会使尖锐的QCP变得模糊不清，并导致磁化率和比热在一个很宽的温度范围内表现出反常的幂律行为，这是由无序驱动的[非费米液体](@keyword=non_fermi_liquids|lang=zh-CN|style=Feynman)行为的标志 [@problem_id:3018869]。对于理解许多真实的、不可避免地存在缺陷的[重费米子系统](@keyword=heavy_fermion_systems_2|lang=zh-CN|style=Feynman)而言，这种效应是解开谜题的关键一环。

因此，[多尼亚克图](@keyword=doniach_diagram|lang=zh-CN|style=Feynman)远不止一幅简单的卡通画。它是一个强大的、具有预测性的框架，统一了广泛的现象。它指导着我们的实验，帮助我们解释实验结果，并为发现诞生于相互竞争的量子熔炉中的新的奇异[物质状态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)指明了方向。它证明了量子世界深刻的美丽和内在的联系。