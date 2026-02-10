## 引言
硅是现代世界的基石，是我们雕刻信息时代的元素。几十年来，我们对硅的理解是基于其宏观、经典的特性。然而，随着电子设备缩小到原子尺度，我们必须面对材料更深层次的量子力学性质。在这个尺度上，一个迷人且至关重要的特征浮现出来：硅的[电子结构](@keyword=electronic_structure|lang=zh-CN|style=Feynman)中存在多个“能谷”，这是电子的一种隐藏的量子身份，对器件的性能和功能有着深远的影响。

这种能谷自由度不再是一个微不足道的学术细节；它已成为前沿电子学物理中的核心角色。然而，它的起源和控制机制可能显得深奥。本文旨在揭开能谷分裂现象的神秘面纱，解答这些能谷是什么、为什么它们固有的能量均等性（简并）在现实世界的器件中被打破，以及这种分裂如何从一个物理上的复杂问题转变为一个强大的工程工具等基本问题。

为了引导您穿越这片量子景观，我们的探索分为两部分。在第一章**原理与机制**中，我们将揭示完美[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中[能谷简并](@keyword=valley_degeneracy|lang=zh-CN|style=Feynman)的起源，并考察打破这种对称性并产生关键能量分裂的三种主要机制——[量子限制](@keyword=quantum_confinement|lang=zh-CN|style=Feynman)、机械应变和[界面物理学](@keyword=interface_physics|lang=zh-CN|style=Feynman)。随后，在**应用与跨学科联系**中，我们将看到这些基础物理学在实践中的应用，揭示对能谷分裂的深刻理解如何促成了从日常[压力传感器](@keyword=pressure_transducer|lang=zh-CN|style=Feynman)和高速处理器到[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)操控以及对硅基[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的追求等技术。

## 原理与机制

想象一下，你是一个电子，不是在真空中飞驰，而是在硅芯片密集、晶体化的景观中穿行。你的世界不是一个空旷的舞台，而是一个由硅原子构成的、[排列](@keyword=permutation|lang=zh-CN|style=Feynman)惊人有序、不断重复的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。这种周期性[排列](@keyword=permutation|lang=zh-CN|style=Feynman)是理解后续一切的关键。它决定了你运动的规则、你的能量，并最终决定了你在量子世界中的身份。

### 多重世界：能谷的起源

在量子领域，电子是一种波，其“动量”由[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman) $\mathbf{k}$ 描述。对于自由空间中的自由电子，能量 $E$ 与动量 $\mathbf{p} = \hbar\mathbf{k}$ 之间的关系很简单：$E = p^2 / (2m_e) = \hbar^2 k^2 / (2m_e)$。最低能量态是静止态，动量为零（$\mathbf{k}=\mathbf{0}$）。但在晶体内部，原子[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的周期性势场深刻地改变了这一图景。根据**[布洛赫定理](@keyword=bloch_s_theorem|lang=zh-CN|style=Feynman) (Bloch's theorem)**，电子的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)是一个平面波，被一个与[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)本身具有相同周期性的函数所[调制](@keyword=modulation|lang=zh-CN|style=Feynman)。这导致了一种更为复杂和有趣的能量-动量关系，即**[能带结构](@keyword=e_k_diagram|lang=zh-CN|style=Feynman)**。

可以将[能带结构](@keyword=e_k_diagram|lang=zh-CN|style=Feynman)看作是晶体中电子允许能量态的一幅地形图。对于**导带**（能够自由移动并承载电流的电子所在[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)）中的电子，我们最感兴趣的是能量最低点。凭直觉，我们可能[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)这个最低点位于[图的中心](@keyword=center_of_a_graph|lang=zh-CN|style=Feynman)，即 $\mathbf{k}=\mathbf{0}$ 处。但在硅中，大自然设计了一种更有趣的[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)电子的最低能量点并不在中心，而是沿着[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)图的主轴，在[第一布里渊区](@keyword=first_brillouin_zone|lang=zh-CN|style=Feynman)边缘附近，分布在六个等效的位置 [@problem_id:3023548]。

这六个能量口袋就是物理学家所说的**能谷 (valleys)**。它们之所以被称为能谷，原因很简单：在一张能量图上，它们确实是电子可以舒适栖息的最低“海拔”位置。由于[硅晶体](@keyword=silicon_crystals|lang=zh-CN|style=Feynman)的立方对称性，这六个能谷在物理上是相同的，并且具有完全相同的能量。这是一种**简并 (degeneracy)**——多个[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)具有相同的能量。这六个能谷中的每一个都代表了电子可以栖息的一个独特的“世界”。这种[能谷简并](@keyword=valley_degeneracy|lang=zh-CN|style=Feynman)度为 $g_v=6$，是硅电子结构的一个基本属性。它在概念上不同于**自旋简并 (spin degeneracy)**，即我们熟悉的由于电子的内禀自旋可以指向“上”或“下”而产生的两重简并 ($g_s=2$)。因此，在体硅中，任何低能电子态都是 $g_v \times g_s = 6 \times 2 = 12$ 重简并的，这是由[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)对称性和量子力学共同作用产生的非凡[多重性](@keyword=multiplicity|lang=zh-CN|style=Feynman) [@problem_id:3023548] [@problem_id:3011924]。

### 打破对称性：限制与应变

然而，这种完美的六重[能谷简并](@keyword=valley_degeneracy|lang=zh-CN|style=Feynman)是理想、无限大[硅晶体](@keyword=silicon_crystals|lang=zh-CN|style=Feynman)的一个特征。一旦我们制造出任何有用的东西，比如现代晶体管，我们便开始打破这些对称性，故事也变得更加有趣。

现代晶体管的核心是一个纳米尺度的区域，电子被限制在一个极薄的二维层中。假设这个层是沿着 $(001)$ 晶面形成的，这意味着电子可以在 $x-y$ 平面内自由移动，但在 $z$ 方向上被紧紧“挤压”。这种挤压是一种[量子限制](@keyword=quantum_confinement|lang=zh-CN|style=Feynman)，就像盒子中的粒子一样。这种限制需要能量代价，而这个能量代价关键取决于电子在限制方向上的质量。

此时，晶体景观的另一个微妙之处显现出来：能谷中电子的**[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman) (effective mass)**是各向异性的。它并非在所有方向上都相同。对于硅能谷中的电子，当沿着能谷轴向运动时，其质量较重（$m_l$，纵向质量）；而当垂直于轴向运动时，其质量较轻（$m_t$，横向质量）。

当我们沿 $z$ 轴限制电子时，沿该轴指向的两个能谷（“z-能谷”）呈现出它们的重纵向质量 $m_l$。而位于 $x-y$ 平面内的四个能谷（“x-y-能谷”）则呈现出它们的轻横向质量 $m_t$。由于对较轻的粒子来说，限制能量更高，因此四个 x-y-能谷被推到比两个 z-能谷高得多的能量位置。仅凭这种限制就打破了六重简并，将其分裂成一个较低的两重简并群和一个较高的四重简并群。我们的低能世界现在从六个能谷缩小到了只有两个 [@problem_id:3011924]。

工程师可以利用**机械应变 (mechanical strain)**进一步推动这种分裂。通过在[晶格间距](@keyword=lattice_spacing|lang=zh-CN|style=Feynman)稍大的材料，如硅锗 (SiGe) 上生长薄硅层，硅被拉伸。这种双轴[拉伸应变](@keyword=extensional_strain|lang=zh-CN|style=Feynman)打破了晶体的立方对称性。根据**[形变势理论](@keyword=deformation_potential_theory|lang=zh-CN|style=Feynman) (deformation potential theory)**，这种应变改变了[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman)，进一步降低了两个 z-能谷的能量，同时提高了四个 x-y-能谷的能量 [@problem_id:2980811] [@problem_id:1091993] [@problem_id:3011924]。能谷的能量位移取决于应变张量 $\epsilon$ 如何与能谷轴向 $\hat{n}_\nu$ 对齐，遵循关系式 $\Delta E_\nu = \Xi_d \mathrm{Tr}(\epsilon) + \Xi_u (\hat{n}_\nu \cdot \epsilon \cdot \hat{n}_\nu - \frac{1}{3}\mathrm{Tr}(\epsilon))$，其中 $\Xi_d$ 和 $\Xi_u$ 是形变势常数 [@problem_id:2980811]。第一项是所有能谷共有的静水压力位移，而第二项无迹项则负责引起分裂。这种[应变工程](@keyword=strain_engineering|lang=zh-CN|style=Feynman)稳固地将两个 z-能谷隔离为低能区的唯一参与者。

### 关键边界：界面如何产生能谷分裂

我们现在只剩下两个简并的能谷态。一个对应于动量沿 $+z$ 方向 ($+\mathbf{k}_0$) 的电子波，另一个对应于动量沿 $-z$ 方向 ($-\mathbf{k}_0$) 的电子波。在完美、无限重复的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中，这两个态将各自独立存在。

但我们的二维电子系统并非无限；它受限于一个**界面 (interface)**，例如[硅晶体](@keyword=silicon_crystals|lang=zh-CN|style=Feynman)与二氧化硅 ($\text{SiO}_2$) 层之间的边界。这个界面是对硅[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)完美[周期性势场](@keyword=periodic_potential|lang=zh-CN|style=Feynman)的一个突然的、原子尺度的扰动。它从根本上打破了沿 $z$ 方向的[平移对称性](@keyword=translational_symmetry|lang=zh-CN|style=Feynman) [@problem_id:3011924] [@problem_id:3011960]。

这种对称性的破坏产生了一个深远的影响：它使得两个能谷态可以耦合。把界面想象成一种特殊类型的镜子。一个动量为 $+\mathbf{k}_0$、朝界面运动的电子波，可能被界面处的陡峭[势场](@keyword=potential_field|lang=zh-CN|style=Feynman)散射，使其方向反转，成为一个动量为 $-\mathbf{k}_0$ 的波。一个连接这两个不同能谷的过程，即**[谷间散射](@keyword=intervalley_scattering|lang=zh-CN|style=Feynman) (intervalley scattering)**，现在成为可能。

在量子力学中，每当两个[简并态](@keyword=degenerate_states|lang=zh-CN|style=Feynman)发生耦合时，简并就会被解除。这些[态混合](@keyword=state_mixing|lang=zh-CN|style=Feynman)形成一对新的本征态：一个对称组合 $(\Psi_{+\mathbf{k}_0} + \Psi_{-\mathbf{k}_0})$ 和一个反对称组合 $(\Psi_{+\mathbf{k}_0} - \Psi_{-\mathbf{k}_0})$，它们现在具有不同的能量。这两个新态之间的能量差就是著名的**能谷分裂 (valley splitting)**，通常表示为 $\Delta_v$ 或 $E_{VS}$ [@problem_id:3011924] [@problem_id:90608]。这与两个相同的[耦合摆](@keyword=coupled_pendulums|lang=zh-CN|style=Feynman)锤直接类似，它们不再独立摆动，而是以两种频率略有不同的“[简正模](@keyword=normal_modes|lang=zh-CN|style=Feynman)式”一起[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。

这种能谷分裂的大小关键取决于界面的*尖锐度*。要将电子的动量从 $+\mathbf{k}_0$ 翻转到 $-\mathbf{k}_0$，需要一个大小为 $2k_0$ 的大动量“踢”。根据傅里叶分析原理，一个势只有在空间中变化非常迅速时，才能提供大的动量踢。一个在单个原子距离内变化的原子级尖锐界面，富含高频傅里叶分量，因此可以为强谷间耦合提供必要的动量踢。相反，一个平滑、缓变的界面则不能，并将导致可忽略的能谷分裂 [@problem_id:3011960]。这就是为什么界面势的简单模型，无论是作为德尔塔函数还是尖锐[指数函数](@keyword=exponential_function|lang=zh-CN|style=Feynman)，都能成功捕捉这一现象的本质：分裂能与电子[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在尖锐边界处的大小直接相关 [@problem_id:97157] [@problem_id:90608]。

这种对界面的极端敏感性具有巨大的实际意义。真实世界的界面从来都不是完美平坦的；它们有原子尺度的台阶和粗糙度。这种无序意味着能谷分裂在芯片上可能存在不可预测的变化，甚至在一个量子点与其邻近[量子点](@keyword=quantum_dots|lang=zh-CN|style=Feynman)之间也不同，这为构建大规模[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机带来了重大挑战 [@problem_id:3011960]。这也解释了为什么能谷分裂是可调的。通过施加更强的垂直电场，我们可以将电子的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)更紧地挤压在界面上，增加其与尖锐势的重叠，从而增强能谷分裂 [@problem_id:3011924]。

### 观察分裂：窥探量子世界

这整个能级分裂再分裂的图景似乎像是理论上的幻想。我们如何确定它是真实的呢？物理学家设计了一种称为**磁谱学 (magnetospectroscopy)** 的精巧方法来直接测量能谷分裂。

实验依赖于能谷态与电子自旋在[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中的相互作用。让我们考虑分裂后的两个能谷态：一个较低能量态（我们称之为 $v_-$）和一个较高能量态（$v_+$），它们之间的能量差为能谷分裂能 $\Delta_v$。在这些轨道态的每一个中，电子的自旋可以指向上或向下。

当我们施加一个外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $B$ 时，自旋简并因**[塞曼效应](@keyword=zeeman_effect|lang=zh-CN|style=Feynman) (Zeeman effect)**而解除。自旋向上态的能量增加 $+\frac{1}{2}g\mu_B B$，而自旋向下态的能量减少 $-\frac{1}{2}g\mu_B B$，其中 $g$ 是电子的 g 因子，$\mu_B$ 是[玻尔磁子](@keyword=bohr_magneton|lang=zh-CN|style=Feynman)。

现在我们有四个能级，它们的能量随着[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)而变化。一个美妙的现象发生了：*较低*能谷态的自旋向上态，其能量从 $0$ 开始并随 $B$ 升高，最终将与*较高*能谷态的自旋向下态发生[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)，后者的能量从 $\Delta_v$ 开始并随 $B$ 下降。

能量分别为：
$E(v_-, \uparrow) = +\frac{1}{2}g\mu_B B$
$E(v_+, \downarrow) = \Delta_v - \frac{1}{2}g\mu_B B$

当这两个能量相等时，[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)发生。一个简单的代数运算表明，这发生在特定的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $B_c$ 处，此时：
$$g \mu_B B_c = \Delta_v$$
通过精确测量观察到[能级交叉](@keyword=level_crossing|lang=zh-CN|style=Feynman)时的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，物理学家可以直接确定能谷分裂能 $\Delta_v$！[@problem_id:3011976]。这种实验技术为我们的理论图景提供了惊人的证实，并为表征可能驱动未来计算机的硅量子点提供了重要工具。同样的基本原理——局域势混合了能谷态——也解释了硅中[施主杂质](@keyword=donor_impurities|lang=zh-CN|style=Feynman)能级的分裂，即所谓的**[谷-轨道分裂](@keyword=valley_orbit_splitting|lang=zh-CN|style=Feynman) (valley-orbit splitting)**，这一现象由杂质位置的四面体对称性决定 [@problem_id:2995770] [@problem_id:469377]。从晶体管到杂质，从理论到实验，这种原理的统一性揭示了固态量子力学深刻而相互关联的美。