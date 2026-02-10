## 应用与学科[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)

现在我们已经掌握了传感单个电子[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的基本原理，让我们踏上一段旅程，看看这个想法将引向何方。你可能会认为这样精细的业务仅限于低温物理实验室的纯净、受控环境。但事实远非如此。探测并响应单个[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)存在的能力是一条金线，它穿梭于一幅惊人现象的织锦之中，从将为量子革命提供动力的电路，到你自己大脑中生命的火花。我们即将发现，大自然以其无穷的创造力，是[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)传感的大师工匠，而我们作为它的学生，正在学习为宏大和平凡的目的构建我们自己的设备。

### 聆听量子低语：通往[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的大门

让我们首先冒险前往量子世界的严寒前沿。我们这个时代的巨大挑战是构建一台[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机。存在许多巧妙的方案来存储[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)，即“[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)（qubit）”，其中之一是利用囚禁在称为[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)的微小[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)笼中的单个电子的内禀自旋。自旋可以是“上”或“下”，代表量子零或一。这是一种保持量子信息的绝佳方式，但一个棘手的问题出现了：你如何*读取*它？单个电子的自旋是一个幽灵般的磁学量，太弱以至于无法直接探测。

解决方案是一种优美的量子柔术：你不测量自旋，而是让自旋决定另一个更实在的粒子——一个[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)——是否被允许移动。这就是[自旋-电荷转换](@keyword=spin_to_charge_conversion|lang=zh-CN|style=Feynman)的艺术。

一个优雅的策略涉及一个外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，它使自旋向上态的能量与自旋向下态略有不同。想象[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)是一个内部有一个电子的小房间，旁边是一个巨大的电子库——一个熙熙攘攘的费米海。我们可以使用电门来调节这个房间的“地板”高度。为了读出，我们将门电压脉冲到一个巧妙的位置：自旋向上态的能级被推到刚好高于电子库的海平面，而自旋向下态则安全地保持在水下。会发生什么呢？如果电子是自旋向上，它会发现自己处于一个能量上不稳定的位置，并会隧穿到库中。如果它是自旋向下，它就被卡住了；它可以隧穿到的态已经被占据了。所以，“自旋向上”导致量子点的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)变化（从一个电子变为零），而“自旋向下”则没有变化。

另一个更微妙的方案，在所谓的[泡利自旋阻塞](@keyword=pauli_spin_blockade|lang=zh-CN|style=Feynman)（Pauli spin blockade）中使用两个相邻的量子点[@problem_id:3012031]。在这里，*两个*电子的自旋状态决定了它们的移动能力。[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)，那个量子力学的严厉法则，禁止两个具有相同自旋的电子（[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)）占据相同的轨道[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。一对具有相反自旋的电子（单重态）则没有这样的限制。通过调节量子点间的能级，我们可以创造一种情况，即单重态对可以愉快地从(1,1)构型（每个点一个电子）跳到(0,2)构型（两个电子在同一个点），但[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)对则被阻塞。再一次，自旋态被映射到了[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)态上——在这种情况下，是[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的*位置*。

在这两种情况下，最后一步都是相同的：我们需要一个对单个电子[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的存在与否极其敏感的探测器。这就是像[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)接触 (QPC) 这样的设备发挥作用的地方。QPC是[二维电子气](@keyword=2d_electron_gas|lang=zh-CN|style=Feynman)中的一个微小缩窄，其狭窄程度使得电子的波动性变得至关重要。它的[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)是量子化的，以 $2e^2/h$ 的离散步长增加。步数，也就是[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)，对静电环境非常敏感。如果一个电子从我们附近的[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)隧穿出去，QPC处的[静电势](@keyword=electrostatics_potential|lang=zh-CN|style=Feynman)会改变，其[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)就会跳变。

然而，这种探测的魔力需要精巧的操控[@problem_id:2976834]。QPC只有在偏置于其两个[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)平台之间的陡峭上升区时才是一个好的传感器。在平台的平坦部分，其[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)被锁定且对小扰动不敏感——这就像试图用一个只能以千克为单位读数的秤来称量一根羽毛。但在上升区，它最为敏感，单个电子从[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)离开引起的微小电势变化会导致QPC电流发生巨大的、可测量的变化。当我们扫描控制[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)和QPC的门电压时，我们看到量子点的充电事件在二维图中显示为清晰的线条。但这些线条只有在QPC被调谐到其敏感的上升区之一时，才在[跨导](@keyword=transconductance|lang=zh-CN|style=Feynman)信号中“可见”。这是被测量的量子系统与进行测量的量子设备之间的一场优美舞蹈。当然，整个过程都是与时间赛跑。[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)必须在脆弱的自旋弛豫到其相反状态之前被读出，而传感器必须足够快和安静，以便在[单电子隧穿](@keyword=single_electron_tunneling|lang=zh-CN|style=Feynman)事件被[热噪声](@keyword=johnson_nyquist_noise|lang=zh-CN|style=Feynman)淹没之前捕捉到它[@problem_id:3012031]。

### 生命的火花：生物世界中的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)传感

为了避免认为这种不可思议的灵敏度纯粹是人类发明的领域，让我们将目光转向内在，转向生命自身的机制。你的每一个思想、每一个感觉、每一次心跳都由在你神经系统中传播的电信号所调控。这些信号是由大自然自己的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)传感纳米机器产生的：[电压门控离子通道](@keyword=voltage_gated_ion_channels|lang=zh-CN|style=Feynman)。

这些通道是蛋白质工程的奇迹，镶嵌在每个[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)的[细胞膜](@keyword=plasma_membrane|lang=zh-CN|style=Feynman)中。它们具有双重特性。蛋白质的一部分作为[电压传感](@keyword=voltage_sensing|lang=zh-CN|style=Feynman)器，拥有带电的氨基酸[残基](@keyword=residue|lang=zh-CN|style=Feynman)，能感受到穿过[细胞膜](@keyword=plasma_membrane|lang=zh-CN|style=Feynman)的电场。当神经冲动期间膜电压变化时，这些带电片段被物理地推或拉，从而扭曲蛋白质的形状。这个运动就是[门控电流](@keyword=gating_current|lang=zh-CN|style=Feynman)，一个在主要事件之前出现的微小电脉冲[@problem_id:2741250]。它是守门人移动[重心](@keyword=center_of_gravity|lang=zh-CN|style=Feynman)时的低语。

这个运动与通道的第二部分——孔道——机械耦合。[电压传感](@keyword=voltage_sensing|lang=zh-CN|style=Feynman)器的运动拉开了通道中央孔道上的一个门，允许大量离子（$\text{Na}^+$、$\text{K}^+$ 或 $\text{Ca}^{2+}$）在电化学梯度的驱动下冲过[细胞膜](@keyword=plasma_membrane|lang=zh-CN|style=Feynman)。这股离子流的洪流就是[神经冲动](@keyword=nerve_impulse|lang=zh-CN|style=Feynman)本身。通过巧妙地用特定毒素阻断孔道，[生物物理学](@keyword=biological_physics|lang=zh-CN|style=Feynman)家能够分离并测量微小的[门控电流](@keyword=gating_current|lang=zh-CN|style=Feynman)，从而证明传感器的运动是孔道打开之前一个独特的、先行的步骤。他们实际上将传感与行动分开了。

然而，大自然并不满足于一种一刀切的设备。进化提供了一个丰富的工具包来调整这些生物电荷传感器。[辅助蛋白](@keyword=accessory_proteins|lang=zh-CN|style=Feynman)亚基可以与主通道结合，巧妙地改变[电压传感](@keyword=voltage_sensing|lang=zh-CN|style=Feynman)器运动的[自由能形貌](@keyword=free_energy_landscape|lang=zh-CN|style=Feynman)。例如，通过稳定传感器的“激活”状态，一个亚基可以改变通道可能打开的电压，或者通过降低构象变化的能垒，它可以极大地加快通道的开放动力学[@problem_id:2587784]。

这种调节的后果是深远的。在突触前末梢，[神经递质](@keyword=neurotransmitter|lang=zh-CN|style=Feynman)的释放是由钙离子[内流](@keyword=internal_flow|lang=zh-CN|style=Feynman)触发的，其关系是高度非线性的——释放量可以与钙离子浓度的四次方成正比！由[辅助亚基](@keyword=auxiliary_subunits|lang=zh-CN|style=Feynman)带来的一个适度变化——使通道打开得快一点，电压低一点——不仅仅是增加了一点点钙[离子电流](@keyword=ionic_currents|lang=zh-CN|style=Feynman)；它可以将由此产生的[神经递质释放](@keyword=neurotransmitter_release|lang=zh-CN|style=Feynman)放大几个[数量级](@keyword=powers_of_ten|lang=zh-CN|style=Feynman)。这就是生命如何利用经过亿万年精炼的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)传感基本物理原理，来构建一个不仅稳健而且可精细调节且具有可塑性的神经系统。

### 机器中的幽灵：我们电子产品中的缺陷

到目前为止，我们已经看到[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)传感是我们设计的强大工具和自然采用的精妙机制。但有时，[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)传感是机器中的幽灵——一个困扰我们最先进技术的不良副作用。这一点在构成我们数字世界基石的硅芯片中表现得最为明显。

现代计算机中数十亿个晶体管中的每一个都是[金属-氧化物-半导体场效应晶体管](@keyword=mosfet|lang=zh-CN|style=Feynman) ([MOSFET](@keyword=mosfet|lang=zh-CN|style=Feynman))。它通过向栅极电极施加电压来吸引[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)载流子到硅的表面，从而创建一个导电通道。理想的晶体管是一个完美的开关。但现实世界是复杂的。硅晶体和二氧化硅绝缘层之间的界面永远不会完美。它布满了原子尺度的缺陷——悬挂键、杂质和结构不完美——这些缺陷充当“界面陷阱”。

这些陷阱实际上是不受欢迎的[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)，其能级位于硅的[带隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)内。当晶体管被打开和关闭时，界面处的电场发生变化，[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)扫过这些[陷阱态](@keyword=trap_states|lang=zh-CN|style=Feynman)。这些陷阱充当了无意的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)传感器[@problem_id:2815834]。例如，一个类受主陷阱在空着时是中性的。当正栅极电压升高表面电势以打开晶体管时，[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)上升到陷阱能级之上，陷阱捕获一个电子，变为负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。

这个被捕获的负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)与我们施加的正栅极电压相抗衡。为了创建导电通道，栅极现在必须吸引足够的正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，既要形成通道，又要补偿新捕获的负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。结果是晶体管需要更高的电压才能打开——其阈值电压发生了偏移。此外，在开关过程中陷阱的持续充电和放电构成了一个额外的[寄生电容](@keyword=parasitic_capacitance|lang=zh-CN|style=Feynman)，这使得晶体管成为一个“漏电”的、效率较低的开关，降低了其亚阈值斜率。我们利用于量子读出的完全相同的原理——[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)响应局部电势而改变其状态——却成了器件工程师必须不断与之斗争的持续性缺陷来源。

### 用光作画：观察[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)移动

除了计算和生物学，[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)传感技术还为材料的动态世界提供了一个窗口，特别是那些与可再生能源相关的材料。考虑一个[染料敏化太阳能电池](@keyword=dye_sensitized_solar_cells|lang=zh-CN|style=Feynman)，它依赖于一个分子（染料）吸收太阳光并向像二氧化钛（$\text{TiO}_2$）这样的[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)注入一个电子。为了优化这些设备，我们迫切希望*观察*到这种电荷转移的发生。

一种强大的技术是泵浦-探测[紫外光电子能谱](@keyword=ultraviolet_photoelectron_spectroscopy|lang=zh-CN|style=Feynman) (UPS)[@problem_id:2508749]。在这个实验中，一个飞秒级的“泵浦”[激光脉冲](@keyword=laser_pulses|lang=zh-CN|style=Feynman)，调谐到染料的吸收频率，照射到样品上。这个脉冲提供的能量刚好足以将染料中的一个电子从其[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)（HOMO）激发到[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)（LUMO）。这就是“[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)”。在短暂的时间之后——也许只有几十飞秒——一个“探测”紫外脉冲到达。这个高能脉冲有足够的能量将电子完全从材料中踢出。然后我们测量这些逃逸的光电子的动能。

根据[光电效应](@keyword=the_photoelectric_effect|lang=zh-CN|style=Feynman)，一个被射出电子的动能告诉我们它在材料中被束缚得有多紧。泵浦脉冲后的结果是戏剧性的。首先，我们看到来自染料HOMO的信号“漂白”；因为电子已经被提升到LUMO，它不再在那里可以从HOMO被射出。其次，在电子从LUMO注入到$\text{TiO}_2$后，染料分子作为一个正离子被留下。这层正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)产生一个[表面偶极子](@keyword=surface_dipole|lang=zh-CN|style=Feynman)，改变了材料的功函数，我们将其“感知”为发射电子能量截止点的明显偏移。通过改变泵浦和探测脉冲之间的时间延迟，我们可以创造一个电荷转移过程的定格动画，以惊人的时间分辨率追踪电子的旅程。

一种互补的方法是[电化学阻抗谱 (EIS)](@keyword=electrochemical_impedance_spectroscopy_(eis)|lang=zh-CN|style=Feynman)[@problem_id:1439154]。在这里，我们不是用光脉冲，而是用一个微小的、不同频率的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)电压来“骚扰”材料，并听取电流的响应。材料对我们“唱”回来的方式揭示了丰富的信息。在高频下，我们感知到最快的过程，比如电极表面的本征电荷转移反应。在低频下，我们对较慢的过程变得敏感，比如离子通过聚合物薄膜的[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)。通过分析完整的[阻抗谱](@keyword=impedance_spectroscopy|lang=zh-CN|style=Feynman)，我们可以将一个复杂的电化学系统分解为其组成部分——一个用于[电荷转移](@keyword=charge_transfer|lang=zh-CN|style=Feynman)的电阻，一个用于[双电层](@keyword=electrical_double_layer|lang=zh-CN|style=Feynman)的电容，一个用于扩散的特殊“Warburg”元件——从而获得关于[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)如何在材料内部移动、存储和反应的完整图像。

### 更深层的联系：[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的几何学

最后，让我们再退一步，问一个真正深刻的问题。我们已经讨论了传感离散[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。但对于导致整个晶体宏观电极化的分布[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)呢？如何“感知”无限、周期性固体的属性？现代极化理论揭示的答案是物理学中最美的答案之一，它涉及一种既抽象又极其根本的传感形式。

想象一个绝缘晶体被塑造成一个环——一个一维环面。为了探测其内部电学性质，我们不是用尖锐的探针去戳它。相反，我们进行一个思想实验：我们慢慢地将一个[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)量子 $\Phi_0 = h/e$ 穿过环的孔洞[@problem_id:2914634]。对于生活在环上的电子来说，这相当于施加一个“扭曲”边界条件；它们的[量子波函数](@keyword=quantum_wavefunction|lang=zh-CN|style=Feynman)在穿过环时必须获得一个特定的[相移](@keyword=phase_shift|lang=zh-CN|style=Feynman)。

当我们把磁通量从零增加到一个量子时，系统的哈密顿量发生变化，但在最后又回到了一个等效的版本。绝缘体的多体[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)[绝热演化](@keyword=adiabatic_evolution|lang=zh-CN|style=Feynman)。由于它是绝缘体，实际上没有[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)绕环流动。然而，有些东西已经改变了。[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)积累了一个[几何相位](@keyword=geometric_phase|lang=zh-CN|style=Feynman)——一个贝里相位。令人惊讶的是，这个纯粹的量子力学相位与晶体的宏观电极化直接成正比！

在这个图景中，穿过的磁通量作为一种拓扑探针，而[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的几何相位是“感知”到的响应。从一个深刻的意义上说，材料通过其集体[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)如何响应全局[拓扑变化](@keyword=topological_changes|lang=zh-CN|style=Feynman)而扭曲来测量自身的极化。这个想法可以被扩展。如果我们周期性地改变[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)扭曲和材料的另一个参数（比如说，通过周期性格点畸变），系统可以在每个周期内精确地泵浦整数个电子穿过环中的任何切口。这种“[Thouless泵浦](@keyword=thouless_pumping|lang=zh-CN|style=Feynman)”表明，以这种几何方式感知的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)不仅是一种静态属性，而且在其动力学上也是量子化的。它揭示了[物态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)一种隐藏的几何结构，将宏观电学性质与[量子理论](@keyword=quantum_theory|lang=zh-CN|style=Feynman)最微妙、最美丽的方面联系起来。从[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的实际读出到[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的抽象几何，[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)传感原理为我们提供了一种在最根本层面上理解和操控世界的语言。