## 应用与跨学科联系

在我们上次的讨论中，我们揭示了费米面这个优美而抽象的概念——金属内部电子海洋的“海岸线”。这是一个诞生于量子力学奇特规则和[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)的概念。你可能会认为这只是一个数学上的奇观，是物理学家局限于黑板上的白日梦。但事实远非如此。

费米面不仅仅是一个概念；它是材料电子灵魂的核心蓝图。它的形状、它的曲折和它的转折，决定了我们可以看到、测量以及最重要的是可以利用的各种实在属性。从金属导电的方式，到你电脑里的磁性存储器，再到[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中电阻的奇迹般消失，费米面都是指挥整场演出的隐藏指挥家。本章的任务是离开抽象的[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)，看看费米面如何在我们的世界中，在广阔的科学技术领域里展现其存在。

### 看见不可见之物：如何为抽象概念拍照

在我们领会[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)的*作用*之前，我们必须回答一个简单的问题：我们怎么知道它就在那里？我们如何为一个存在于抽象[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)而非真实空间中的物体拍照？事实证明，物理学家们以其特有的独创性，开发出了两台非凡的“相机”。

第一种技术是一种依赖[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的优美的量子戏法。当我们将金属置于强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中时，费米面上的电子被迫进入螺旋状轨道。但量子力学坚持认为这些轨道并非任意的；它们必须是量子化的，意味着只允许特定面积的轨道存在。当我们缓慢增加[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)时，这些被称为[朗道能级](@keyword=landau_levels|lang=zh-CN|style=Feynman)的量子化轨道会扩张并扫过费米能。每当一个能级穿过[费米能](@keyword=fermi_energy|lang=zh-CN|style=Feynman)时，它都会在材料的性质上引起微小而周期性的摆动，例如其[磁化率](@keyword=susceptibility|lang=zh-CN|style=Feynman)或电阻。这些就是量子[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，以德哈斯-范阿尔芬 (dHvA) 和舒布尼科夫-德哈斯 (SdH) 效应等名称为人所知。

由 Lars Onsager 揭示的深刻联系是，这些[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)相对于逆[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $1/B$ 的*频率*，与垂直于[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)[截面](@keyword=cross_section_2|lang=zh-CN|style=Feynman)积成正比 [@problem_id:56975]。这就像我们用一束“光”（[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)）穿过[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)，并测量其阴影的大小。通过旋转材料并从各个角度测量[振荡频率](@keyword=oscillation_frequency|lang=zh-CN|style=Feynman)，我们可以构建一个完整的三维模型，就像医院的 CT 扫描仪使用来自不同方向的 X 射线来重建器官图像一样 [@problem_id:2810690]。这是我们首次获得关于费米面复杂且常常出人意料的形状的具体视觉证据。

第二台“相机”更为直接，称为[角分辨光电子能谱](@keyword=arpes|lang=zh-CN|style=Feynman)，即 [ARPES](@keyword=arpes|lang=zh-CN|style=Feynman)。其概念原理非常简单：我们用高能[光子](@keyword=photon|lang=zh-CN|style=Feynman)照射材料，将一个电子完全敲出。然后我们扮演一个宇宙级的捕手，测量被逐出电子的动能和它飞出的角度。利用[能量和动量守恒](@keyword=conservation_of_energy_and_momentum|lang=zh-CN|style=Feynman)定律，我们可以反向推算出电子在被撞击前在晶体*内部*的确切能量和动量。通过对所有不同角度重复此过程，我们可以 painstakingly地绘制出材料的[电子能带结构](@keyword=electronic_band_structure|lang=zh-CN|style=Feynman)——电子景观的“地形图”。费米面就是我们在这片景观与费米能级相交处追踪出的[等高线](@keyword=level_curves|lang=zh-CN|style=Feynman) [@problem_id:2952752]。

### 指挥棒：主导电子的流动

也许金属最基本的属性就是其导电能力。这一日常现象完全由[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)边缘的电子所主导。当你施加电压时，你提供了一个温和的推动力，但只有费米面上的电子才有邻近的空态可以移动进去。它们是可移动的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)载流子。

因此，费米面的形状对材料如何导电有着直接而深远的影响。[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)上特定点的电子速度取决于该点[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的陡峭程度。晶体的各向异性——即在不同方向上具有不同特性的属性——直接反映在其费米面的形状上。例如，如果一种材料沿一个轴的导电性优于另一个轴，那是因为其费미面上的电子在该方向上的[平均速度](@keyword=mean_velocity|lang=zh-CN|style=Feynman)更高。通过像 [ARPES](@keyword=arpes|lang=zh-CN|style=Feynman) 这样的技术，我们可以同时测量费米面的位置和那里的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)斜率，从而使我们能够从第一性原理预测和理解材料的[各向异性电导率](@keyword=anisotropic_conductivity|lang=zh-CN|style=Feynman) [@problem_id:2952752]。动量空间中的抽象几何形状直接映射到你可以在实验室中测量的 tangible 电阻值。

### 隐藏的握手：自旋电子学与 RKKY 相互作用

一种材料的[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)能影响另一种材料吗，即使它们没有接触？答案是肯定的，而且这正是现代[数据存储](@keyword=data_storage|lang=zh-CN|style=Feynman)技术的核心。考虑一个由两个磁性层夹着一个薄的非磁性金属间隔层构成的“三明治”结构，比如用铜层隔开的铁层。你可能[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)这两个铁层在磁性上是独立的。但值得注意的是，它们的磁取向变得耦合——它们倾向于彼此平行或反平行[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。更奇怪的是，随着铜间隔层厚度的改变，这种首选的[排列](@keyword=permutation|lang=zh-CN|style=Feynman)方式会在平行和反平行之间[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。

这种被称为层间[交换耦合](@keyword=exchange_coupling|lang=zh-CN|style=Feynman)的现象是由铜间隔层的费米海所介导的。第一个铁层的磁性扰动了铜中[导电电子](@keyword=conduction_electrons|lang=zh-CN|style=Feynman)的自旋。这种扰动不仅仅停留在界面处；它以一种长程的[自旋密度波](@keyword=spin_density_wave_2|lang=zh-CN|style=Feynman)纹，即[自旋密度波](@keyword=spin_density_wave_2|lang=zh-CN|style=Feynman)的形式在金属中传播。这就是著名的 [Ruderman-Kittel-Kasuya-Yosida](@keyword=ruderman_kittel_kasuya_yosida|lang=zh-CN|style=Feynman) (RKKY) 相互作用。这个波纹的波长不是任意的；它由铜费米面的“卡尺”——即沿三明治方向横跨费米面的极值距离——所设定。

当第二个铁层被放置在一定距离时，它会感受到这种[自旋波](@keyword=spin_waves|lang=zh-CN|style=Feynman)纹。如果它位于“波峰”上，它会平行[排列](@keyword=permutation|lang=zh-CN|style=Feynman)；如果位于“波谷”中，则会反平行[排列](@keyword=permutation|lang=zh-CN|style=Feynman) [@problem_id:2820688]。通过精确设计间隔层的厚度，我们可以将磁性层锁定在反铁磁状态。施加外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)可以迫使它们对齐，从而急剧改变器件的电阻。这就是巨[磁阻](@keyword=reluctance|lang=zh-CN|style=Feynman) (GMR) 效应，其发现获得了 2007 年诺贝尔物理学奖，并促成了硬盘驱动器的小型化。你存储的每一比特数据都是通过一种简单金属的费米面传递的这种“隐藏握手”的见证。

### 超[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)的摇篮

[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)不仅是单电子现象的舞台；它更是物理学中最神秘、最美丽的集体现象之一——超[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)——诞生的摇篮。在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，电子形成配对（库珀对），可以毫无阻力地穿过[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。

这种配对并非一个简单的事件。它由一种[吸引相互作用](@keyword=attractive_interactions|lang=zh-CN|style=Feynman)介导，配对形成了一个新的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，其特征是一个“超导能隙” $\Delta$。这个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)是打破一个配对的能量惩罚；它排斥费米能附近的单电子激发。在最简单的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，这个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)在费米面上的任何地方都是均匀的。但在广阔而激动人心的“非规”[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)世界里，例如高温铜氧化物和铁基材料，[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的大小会随着你在费米面上的移动而急剧变化，即 $\Delta(\mathbf{k})$ [@problem_id:2802582]。

ARPES 再次成为我们洞察这个世界的窗口。当一种材料变成超导态时，ARPES 显示电子[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)不再穿过[费米能](@keyword=fermi_energy|lang=zh-CN|style=Feynman)。相反，它会向自身“弯回”，打开一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。这个有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)在[费米动量](@keyword=fermi_momentum|lang=zh-CN|style=Feynman)处的最小能量直接给出了超导能隙的大小 $|\Delta(\mathbf{k})|$。通过在整个[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)上绘制这个最小能量，我们可以描绘出[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)各向异性的完整图像 [@problem_id:2802582]。

这张图掌握着[配对机制](@keyword=pairing_mechanisms|lang=zh-CN|style=Feynman)本身的秘密。例如，在许多[铁基超导体](@keyword=iron_based_superconductors|lang=zh-CN|style=Feynman)中，[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)由不同的“口袋”组成——[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)中心的小空穴型表面和角落的电子型表面 [@problem_id:2810668]。[ARPES](@keyword=arpes|lang=zh-CN|style=Feynman) 可能会显示在所有这些口袋上都有一个完整的、无节点的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。但这并未揭示全部真相。另一种技术，[非弹性中子散射](@keyword=inelastic_neutron_scattering|lang=zh-CN|style=Feynman)，可以探测到一种称为“[自旋共振](@keyword=spin_resonance|lang=zh-CN|style=Feynman)”的集体自旋激发。理论告诉我们，这种在这些材料中作为关键特征的共振，只有当[超导能隙](@keyword=superconducting_gap|lang=zh-CN|style=Feynman)在空穴口袋上的*符号*与[电子口袋](@keyword=electron_pockets|lang=zh-CN|style=Feynman)上的符号相反时才能存在。这是一种所谓的 $s_{\pm}$ 配对态 [@problem_id:2996879]。在这里我们看到了多种技术的完美结合：[ARPES](@keyword=arpes|lang=zh-CN|style=Feynman) 绘制了[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)的几何形状和[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的大小，而中子散射提供了关于其相位的关键信息，使我们能够破译[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)复杂的、符号变化的本质。

### 跨越地平线：奇异世界中的[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)

[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)概念的力量如此之大，以至于它甚至延伸到一些最奇异、相互作用最强的[物质状态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)，在这些状态中，“电子”本身的概念都开始变得模糊。

物理学中一个著名的难题涉及欠掺杂的[铜氧化物](@keyword=cuprates|lang=zh-CN|style=Feynman)高温超导体。在它们的“[赝能隙](@keyword=pseudogap|lang=zh-CN|style=Feynman)”相中，ARPES 测量显示出的是不连续的“[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)”，而不是闭合的费米[等高线](@keyword=level_curves|lang=zh-CN|style=Feynman)。然而，在高[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中的量子[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)实验却探测到对应于小的、*闭合的*费米口袋的信号。这两者怎么可能都是真的呢？答案在于理解我们的“相机”告诉了我们什么。一个可信的模型表明，一个真正的、闭合的口袋确实存在，但口袋“背面”（在所谓的反节点区域）的[准粒子寿命](@keyword=quasiparticle_lifetime|lang=zh-CN|style=Feynman)极短且非相干，以至于它们的谱特征在 ARPES 中完全被冲刷掉了。ARPES 只看到了口袋的相干“正面”，表现为[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)。而对闭合轨道路径而非局域[相干性](@keyword=coherence|lang=zh-CN|style=Feynman)敏感的量子[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，仍然可以探测到完整的、闭合的口袋 [@problem_id:2994211, @problem_id:2994211]。这教给我们一个微妙但至关重要的教训：我们测量到的东西取决于我们提出的问题。

也许这个概念力量最惊人的展示来自于[分数量子霍尔效应 (FQHE)](@keyword=fractional_quantum_hall_effect_(fqhe)|lang=zh-CN|style=Feynman)。在极洁净的二维电子气中，在极低温度和巨大[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)下，电子间的相互排斥变得至关重要。系统进入一种新的、奇异的液体状态。由 Jainendra Jain 提出的[复合费米子理论](@keyword=composite_fermion_theory|lang=zh-CN|style=Feynman)假设，我们可以通过想象每个电子捕获偶数个[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)并成为一种新的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)——复合费米子——来理解这个复杂、[强相互作用](@keyword=strong_nuclear_force|lang=zh-CN|style=Feynman)的系统。这团复合费米子随后的行为非常像一团[弱相互作用](@keyword=weak_nuclear_force|lang=zh-CN|style=Feynman)的粒子。令人惊奇的是，在填充因子 $\nu=1/2$ 附近，这些[复合费米子](@keyword=composite_fermion|lang=zh-CN|style=Feynman)形成了它们自己的[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)和自己明确的费米面。而且我们可以“看到”它！实验探测到了在*有效*[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中呈周期性的[舒布尼科夫-德哈斯振荡](@keyword=shubnikov_de_haas_oscillations|lang=zh-CN|style=Feynman)，其频率给出了复合费米子费米面的面积，与预测完全一致 [@problem_id:2976547]。费米面的概念如凤凰涅槃般从[强相互作用](@keyword=strong_nuclear_force|lang=zh-CN|style=Feynman)的漩涡中重生，证明了其深刻的统一力量。

### 设计师的画架

我们回到了起点。我们从学习如何“看”到[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)开始。然后我们探索了它的形状如何决定材料的电学、磁学和超导性质。这些知识的最终目标是将观察转化为创造。我们能成为“[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)工程师”吗？

这是现代[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)的前沿。非规[超导理论](@keyword=superconductivity_theory|lang=zh-CN|style=Feynman)表明，为了实现高的临界温度 ($T_c$)，我们可能需要一个具有特定形状的费米面——例如，一个具有良好“嵌套” (nesting) 特性的[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)，这种特性可以增强被认为在许多这类系统中粘合库珀对的排斥性[自旋涨落](@keyword=spin_fluctuations|lang=zh-CN|style=Feynman)相互作用 [@problem_id:2869559]。有了这些知识，我们可以使用计算方法来预测哪些化学成分和[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)可能产生具有所需几何形状的费米面。然后，实验家们可以在实验室里着手工作，尝试合成这些预测的材料。

费米面，曾经是一个纯粹的理论构造，如今已成为设计师画架上的实用蓝图。它将量子力学最深邃的规则与我们时代最先进的技术联系在一起，并继续指引着我们去发现和发明将塑造我们未来的材料。