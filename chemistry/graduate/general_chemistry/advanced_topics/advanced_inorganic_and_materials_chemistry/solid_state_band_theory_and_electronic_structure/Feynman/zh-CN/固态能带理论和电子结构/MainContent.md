## 引言
固态物质的宏观电学和光学性质，如[金属的导电性](@keyword=electrical_conductivity_of_metals|lang=zh-CN|style=Feynman)、绝缘体的透明性以及[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)的光电响应，都源于其内部微观的电子结构。然而，简单地将孤立原子的电子能级理论应用于由海量原子构成的晶体是远远不够的。当原子聚集在一起时，它们的电子行为如何发生根本性的改变？这便是固态能带理论所要解答的核心问题，它为我们理解和设计[功能材料](@keyword=functional_materials|lang=zh-CN|style=Feynman)提供了统一而强大的理论框架。

本文旨在系统性地揭示电子在晶体周期性势场中的行为规律。我们将穿越理论的深邃与应用的广阔，理解从[原子轨道](@keyword=atomic_orbitals|lang=zh-CN|style=Feynman)到宏观[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的[演化过程](@keyword=evolutionary_process|lang=zh-CN|style=Feynman)，并探究这一过程如何决定了材料的命运。在学习过程中，你将首先掌握[能带理论](@keyword=electronic_band_theory|lang=zh-CN|style=Feynman)的核心概念，包括[布洛赫定理](@keyword=bloch_s_theorem|lang=zh-CN|style=Feynman)、[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)与[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的形成、费米面以及有效[质量的起源](@keyword=origin_of_mass|lang=zh-CN|style=Feynman)。接着，你将看到这些理论如何应用于解释和预测现实世界中的现象，例如[半导体掺杂](@keyword=semiconductor_doping|lang=zh-CN|style=Feynman)、[应变工程](@keyword=strain_engineering|lang=zh-CN|style=Feynman)、材料的光学特性，乃至[高温超导](@keyword=high_temperature_superconductivity|lang=zh-CN|style=Feynman)等前沿课题。最后，通过动手实践，你将有机会亲自推导[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)论中的关键模型。

让我们从第一章“原理与机制”开始，深入探索电子在晶体这座“繁华都市”中必须遵循的量子交通规则。

## 原理与机制

在上一章中，我们发现固态物质并非原子的杂乱堆砌，而是一种被称为晶体的、美妙而有序的结构。现在，让我们换一个视角，想象自己化身为一个电子，即将踏上一场穿越晶体内部的冒险。它的旅程将遵循怎样的规则？这并非一片空旷的太空，而是一个由原子核和其它电子构成的“繁华都市”。

### 舞台：[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)及其周期性势场

这场冒险的舞台，最核心的特征就是它的完美周期性。晶体就像一幅可以无限延伸的壁纸图案，无论你朝哪个方向平移特定的距离，看到的景象都和原来一模一样。这种完美的重[复性](@keyword=renaturation|lang=zh-CN|style=Feynman)，是解锁固态物理奥秘的钥匙。

物理学家将这种周期性用一个叫做“[布拉菲晶格](@keyword=bravais_lattices|lang=zh-CN|style=Feynman) (Bravais lattice)”的数学框架来描述，它好比是搭建城市的脚手架。而在脚手架的每一个节点上，我们都放置一个相同的“装饰”，这个装饰可以是一个原子，也可以是多个原子组成的团簇，我们称之为“基元 (basis)”。脚手架加上装饰，就构成了一个真实的[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)。[@problem_id:2955792]

对于在晶体中运动的电子而言，它感受到的不是空无一物的空间，而是一个周期性变化的势能景观，充满了由原子核构成的“山丘”和电子云分布形成的“山谷”。我们可以通过将所有原子的势能相加，来构建这个总的[势能函数](@keyword=potential_energy_function|lang=zh-CN|style=Feynman) $V(\mathbf{r})$。这个势能景观最重要的特性，正是它的周期性。如果我们把电子的位置 $\mathbf{r}$ 移动一个[晶格矢量](@keyword=lattice_vectors|lang=zh-CN|style=Feynman) $\mathbf{R}$（即从一个“脚手架”节点移动到另一个），它感受到的势能是完全相同的：

$$V(\mathbf{r} + \mathbf{R}) = V(\mathbf{r})$$

这个简单的方程，是所有能带理论的基石。它意味着，电子面对的不是一片混乱，而是一个极具规律的、重复的世界。

### 量子世界的交通规则：布洛赫定理

那么，作为量子波的电子，在这样周期性的[势能景观](@keyword=potential_energy_landscape|lang=zh-CN|style=Feynman)中，其[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)会是什么样子呢？答案就是凝聚态物理中最核心的定理之一——布洛赫定理 (Bloch's theorem)。这可以被看作是电子在晶体中必须遵守的“交通规则”，而它正是[平移对称性](@keyword=translational_symmetry|lang=zh-CN|style=Feynman)的直接产物。[@problem_id:2955797]

直觉上，电子的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)本身并不能是严格周期性的。因为一个严格周期的波，在所有位置的概率都一样，意味着它没有净的动量，电子就被“困”住了。但我们知道，金属中的电子是可以自由移动形成电流的。那么，解决方案是什么呢？

想象一下，你正走在一个非常长的、装饰华丽的走廊里，墙壁、天花板和地毯上的图案都在不断重复。你的“状态”，并不仅仅取决于你在某一个重复图案中的具体位置，还取决于你沿着走廊整体前进了多远。

[布洛赫定理](@keyword=bloch_s_theorem|lang=zh-CN|style=Feynman)完美地描述了这一点。它指出，电子在晶体中的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman) $\psi_{\mathbf{k}}(\mathbf{r})$ 具有一种特殊的形式：

$$\psi_{\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} u_{\mathbf{k}}(\mathbf{r})$$

这个美妙的公式由两部分构成：

*   $e^{i\mathbf{k}\cdot\mathbf{r}}$ 部分是一个平面波，就像在真空中自由飞翔的电子一样。它描述了电子的整体长程运动。这里的矢量 $\mathbf{k}$ 被称为**晶体动量**，是电子在晶体中一种新的、适应了[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)环境的“[准动量](@keyword=crystal_momentum|lang=zh-CN|style=Feynman)”。

*   $u_{\mathbf{k}}(\mathbf{r})$ 部分则是一个与[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)具有**相同周期性**的函数。它描述了电子的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在每一个晶胞内部，为了适应原子势能而进行的复杂“扭动”和“舞蹈”。

这正是[布洛赫定理](@keyword=bloch_s_theorem|lang=zh-CN|style=Feynman)的精妙之处：电子的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)是一种混合体，既有自由电子的“行进”特性，又保留了被原子束缚的“局域”特征。一个简单的数学形式，却蕴含了固态中电子行为的所有丰富性。

### 景观的形成：[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)与[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)

既然我们知道了电子[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的形式，那么它们所对应的能量又是怎样的呢？求解薛定谔方程后，我们惊奇地发现，并非所有能量都是允许的！[周期性势场](@keyword=periodic_potential|lang=zh-CN|style=Feynman)将连续的能量谱梳理成了分立的“能量域”，我们称之为**[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman) (energy bands)**，而[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)之间则存在电子无法涉足的**[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) (band gaps)**。

理解[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)与[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的形成，有两种非常好的思路，它们就像从山的两侧攀登，最终在顶峰相遇。

**“近自由电子”的观点：** 让我们从一个极端开始，想象晶体中的势场非常微弱。一个近乎自由的电子高速穿行。当它的波长恰好满足[布拉格衍射](@keyword=bragg_diffraction|lang=zh-CN|style=Feynman)条件时，会发生什么呢？这就像光波在光栅上发生衍射一样。

在动量空间中一个叫做“布里渊区边界”的特殊位置（例如在一维情况下 $k = \pi/a$），向右运动的电子波 $e^{ikx}$ 和向左运动的电子波 $e^{-ikx}$ 具有完全相同的能量。微弱的[周期性势场](@keyword=periodic_potential|lang=zh-CN|style=Feynman)会将这两个状态耦合起来，电子仿佛站在了一个十字路口，无法决定是向左还是向右。量子力学的解决方案是，电子形成两种不同的驻波。一种驻波将电子[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)更多地聚集在原子核附近，与正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的吸引作用更强，因此能量更低；另一种[驻波](@keyword=standing_waves|lang=zh-CN|style=Feynman)则将电子[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)聚集在原子之间，能量更高。[@problem_id:2955812]

就这样，一个[能量简并](@keyword=energy_degeneracy|lang=zh-CN|style=Feynman)点被劈开，形成了一个宽度为 $2|V_G|$ 的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)！$V_G$ 是周期性势场的傅里叶分量，它的大小决定了[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的宽度。这就是[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的来源，是[量子干涉](@keyword=quantum_interference|lang=zh-CN|style=Feynman)在晶体世界中上演的杰作。

**“紧束缚”的观点：** 现在我们从另一个极端出发。想象原子彼此相距很远，每个原子都拥有自己独立的、离散的[原子能级](@keyword=atomic_energy_levels|lang=zh-CN|style=Feynman)。

当我们把这些原子逐渐拉近，一个原子上的电子的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)会开始与邻近原子的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)发生重叠。这意味着，一个原子上的电子有机会“隧穿”或“跳跃”到旁边的原子上。这种跳跃的可能性，使得原本尖锐的[原子能级](@keyword=atomic_energy_levels|lang=zh-CN|style=Feynman)展宽成了一个能量范围，也就是[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)。原子间的[波函数重叠](@keyword=wavefunction_overlap|lang=zh-CN|style=Feynman)越多，电子越容易在晶体中“旅行”，[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)也就越宽。[@problem_id:2955794]

在这种观点下，我们可以用原子的轨道 $\phi(x-na)$ 作为“积木”，通过线性组合来构建整个晶体的电子[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)。通过赋予这些积木合适的相位因子 $e^{ikna}$，我们就能构造出满足布洛赫定理的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)。这里的[晶体动量](@keyword=crystal_momentum|lang=zh-CN|style=Feynman) $\mathbf{k}$ 控制着不同原子轨道之间的相对相位，决定了它们在电子传播时是[相长干涉](@keyword=constructive_interference|lang=zh-CN|style=Feynman)还是[相消干涉](@keyword=destructive_interference|lang=zh-CN|style=Feynman)。

这两种观点——从几乎自由的电子出发，看它如何被[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)“卡住”形成能隙；以及从被束缚的电子出发，看它如何通过“跳跃”[形成能](@keyword=formation_energy|lang=zh-CN|style=Feynman)带——是同一枚硬币的两面。它们都指向了同一个深刻的结论：晶体中电子的能量不是连续的，而是分布在一个个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)上。

### 居民：填充[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)

我们已经描绘出了晶体中允许电子存在的[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman)。现在，我们需要把宇宙中的电子“居民”安置进去。根据[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)，每个[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)最多只能容纳两个自旋相反的电子。

在绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman) $(T=0)$ 时，电子们会从最低的能级开始，一层一层地向上填充，直到所有电子都找到自己的位置。这个被占据的最高能级，就是**[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman) ($E_F$)**。它就像我们能量景观中的“海平面”，海平面以下是被电子占据的“[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)”，海平面以上则是空无一人的“天空”。[@problem_id:2955765]

费米能级的位置，决定了一种材料的电学本性：

*   **金属 (Metals)：** 如果[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)恰好落在一个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的中间，那么“海平面”附近就有大量的空态。只需施加一个很小的电场，就能轻易地将“海平面”附近的[电子激发](@keyword=electronic_promotion|lang=zh-CN|style=Feynman)到更高的空态中，形成电流。这就是金属导电的原因。

*   **绝缘体与[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman) (Insulators and Semiconductors)：** 如果一个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)被完全填满，而[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)正好位于它与下一个空[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)之间的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)中，那么情况就大不相同了。要想让电子导电，必须提供足够大的能量（至少等于[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)宽度），才能将它从被填满的“[价带](@keyword=valence_band|lang=zh-CN|style=Feynman)”激发到空无一物的“[导带](@keyword=conduction_band|lang=zh-CN|style=Feynman)”上。如果[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)很大，材料就是绝缘体；如果[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)较小，它就是[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)。

在金属中，“[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)”在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中的“海岸线”被称为**费米面 (Fermi surface)**。它是由所有满足 $E(\mathbf{k}) = E_F$ 的 $\mathbf{k}$ 点构成的[等能面](@keyword=constant_energy_surface|lang=zh-CN|style=Feynman)。

你可能会觉得这很抽象，但[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)是描述金属最重要的物理概念！几乎所有在低温下发生的有趣现象——[电导](@keyword=electrical_conductance|lang=zh-CN|style=Feynman)、[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)、磁性——都只与费米面附近的电子有关。那些深藏在“[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)”内部的电子，由于周围的状态都已被占据，被[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)“冻结”住了，无法参与到这些低能量的物理过程中。[@problem_id:2955765]

费米面的形状直接由能带结构 $E(\mathbf{k})$ 决定，它反过来也决定了金属的宏观性质。例如，一个在某些方向上更“伸展”的费米面，会导致该方向上的[电导率](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)更高。

### 精妙的细节与动力学

让我们再深入探索一下[能带结构](@keyword=e_k_diagram|lang=zh-CN|style=Feynman)，会发现更多奇妙的细节。

**有效质量 (Effective Mass):** 晶体中的电子在受力时，它的响应行为与在真空中的自由电子完全不同。它的加速度不再由其本身的质量 $m_e$ 决定，而是由它所在[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的**曲率**决定。我们将这种效应打包成一个概念，叫做“有效质量” $m^*$。定义为：

$$(m^*)^{-1}_{ij} = \frac{1}{\hbar^2}\frac{\partial^2 E(\mathbf{k})}{\partial k_i \partial k_j}$$
 
这个公式告诉我们，[有效质量张量](@keyword=effective_mass_tensor|lang=zh-CN|style=Feynman)的逆正比于[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman) $E(\mathbf{k})$ 的曲率（由二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)描述）。[@problem_id:2955803]

*   一个弯曲得很厉害的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)（像一个很深的“山谷”），对应着很小的有效质量。这意味着电子非常“敏捷”，很容易被加速。
*   一个平坦的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)，对应着巨大的有效质量。这意味着电子非常“笨重”，几乎无法移动。
*   最惊人的是，在[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的顶部附近，能量对 $\mathbf{k}$ 的二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)是负的，这导致了**负的有效质量**！这意味着，如果你朝一个方向推它，它会朝相反的方向加速。这听起来很荒谬，但它正是[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)中“空穴”概念的物理根源。一个空穴，本质上就是在满带顶部附近行为怪异的电子的集体表现。

**态密度与[范霍夫奇点](@keyword=van_hove_singularity|lang=zh-CN|style=Feynman) (Density of States & van Hove Singularities):** 在给定的能量附近，有多少个可用的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)？这个量被称为态密度 (DOS)。它通常不是一个平滑的函数。每当能带结构 $E(\mathbf{k})$ 在某个 $\mathbf{k}$ 点变得“平坦”时（即能量的梯度 $\nabla_{\mathbf{k}} E(\mathbf{k}) = \mathbf{0}$），[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)就会出现尖锐的峰或[拐点](@keyword=inflection_points|lang=zh-CN|style=Feynman)，这些特征被称为**[范霍夫奇点](@keyword=van_hove_singularity|lang=zh-CN|style=Feynman)**。这又是一个几何（[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的曲率和拓扑）与[物理可观测量](@keyword=physical_observables|lang=zh-CN|style=Feynman)（态密度）之间的深刻联系。[@problem_id:2955831]

**光学性质：直接与间接[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman) (Direct vs. Indirect Gaps):** 光是如何与[能带结构](@keyword=e_k_diagram|lang=zh-CN|style=Feynman)相互作用的呢？最常见的过程是，一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)被吸收，将一个电子从被填满的价带“踢”到空的导带。

这个过程必须同时满足[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)和动量守恒。可见光[光子](@keyword=photon|lang=zh-CN|style=Feynman)的能量很高，但与晶体中的电子相比，它的动量几乎可以忽略不计。因此，这个跃迁在 $\mathbf{k}$ 空间中必须是“垂直”的，即电子的[晶体动量](@keyword=crystal_momentum|lang=zh-CN|style=Feynman) $\mathbf{k}$ 几乎不发生改变。

*   如果价带的顶端和导带的底端位于**同一个 $\mathbf{k}$ 值**，这种材料就具有**直接[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)**。[光子](@keyword=photon|lang=zh-CN|style=Feynman)的吸收和发射过程非常高效，因为一步就能完成。这类材料（如砷化镓 GaAs）是制造 LED 和激光器的理想选择。[@problem_id:2955770]

*   如果价带顶和导带底位于**不同的 $\mathbf{k}$ 值**，材料就具有**间接[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)**。电子在跃迁时，不仅需要吸收一个[光子](@keyword=photon|lang=zh-CN|style=Feynman)来获得能量，还需要[晶格振动](@keyword=crystal_lattice_vibrations|lang=zh-CN|style=Feynman)（[声子](@keyword=phonons|lang=zh-CN|style=Feynman)）的帮助来补足动量差。这是一个两步过程，发生的概率要低得多。因此，这类材料的光吸收和发射效率很低。这就是为什么硅 (Si)，一种间接[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)，是制造计算机芯片的王者，却不适合用来做激光器。[@problem_id:2955770]

### 自旋的秘密生活

到目前为止，我们几乎忽略了电子的一个内在属性：自旋。它重要吗？哦，它至关重要，并且引出了全新的物理。

一个关键的效应是**自旋-轨道耦合 (Spin-Orbit Coupling, SOC)**。这是一个源于[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)的效应。简单来说，一个在原子核电场中高速运动的电子，在它自己的[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)里会感受到一个[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。这个内部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)会与电子自身的磁矩（即自旋）相互作用。这个相互作用的哈密顿量形式如下：

$$H_{\mathrm{SO}}=\frac{\hbar}{4 m_e^2 c^2} (\nabla V \times \mathbf{p}) \cdot \boldsymbol{\sigma}$$

这里 $\nabla V$ 是电[势能的梯度](@keyword=gradient_of_potential_energy|lang=zh-CN|style=Feynman)（电场），$\mathbf{p}$ 是动量，而 $\boldsymbol{\sigma}$ 是代表自旋的[泡利矩阵](@keyword=pauli_matrices|lang=zh-CN|style=Feynman)。[@problem_id:2955772]

对称性再次扮演了主角：

*   如果晶体具有**反演对称性**（即存在一个中心点，将整个晶体进[行空间](@keyword=row_space|lang=zh-CN|style=Feynman)反演后保持不变），那么在任何一个 $\mathbf{k}$ 点，自旋向上和自旋向下的电子能量都严格相等。[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)是双重自旋简并的。[@problem_id:2955772]

*   如果晶体**缺少[反演对称性](@keyword=inversion_symmetry|lang=zh-CN|style=Feynman)**，这种简并就会被解除！在同一个 $\mathbf{k}$ 点，自旋向上和向下的电子将具有不同的能量，[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)会分裂成两条。这正是“自旋电子学”领域的基石，它旨在利用电子的自旋属性来存储和处理信息。[@problem_id:2955772]

*   然而，即使没有[反演对称性](@keyword=inversion_symmetry|lang=zh-CN|style=Feynman)，**时间反演对称性**依然提供了一层保护。它保证了 $E(\mathbf{k}, \uparrow) = E(-\mathbf{k}, \downarrow)$ 的关系。更重要的是，在[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)中的一些特殊高对称点（被称为[时间反演](@keyword=time_reversal_2|lang=zh-CN|style=Feynman)不变动量点），[能量本征态](@keyword=energy_eigenstates|lang=zh-CN|style=Feynman)仍然必须是至少双重简并的，这被称为[克拉默斯简并](@keyword=kramers__degeneracy|lang=zh-CN|style=Feynman) (Kramers degeneracy)。[@problem_id:2955772]

### 章节小结

我们看到了一套多么令人惊叹的、层层递进的物理原理。从一个简单而优雅的周期性势场假设出发，结合量子力学和对称性的基本规则，我们就推导出了固态物质中那丰富多彩、有时甚至匪夷所思的电子行为世界。

不过，在整个过程中，我们其实耍了一点“小聪明”。我们一直将电子当作是在一个固定的背景[势场](@keyword=potential_field|lang=zh-CN|style=Feynman)中独立运动的粒子。但实际上，电子之间会相互排斥。当我们考虑这些复杂的相互作用时，我们这幅美丽的单粒子图像会崩溃吗？

一个名为**[卢廷格定理](@keyword=luttinger_s_theorem|lang=zh-CN|style=Feynman) (Luttinger's theorem)** 的深刻结果给了我们一个预告。令人惊讶的是，对于一大类被称为“[费米液体](@keyword=fermi_liquid|lang=zh-CN|style=Feynman)”的材料，我们最重要的结果之一——费米面的体积——居然**不受**这些复杂相互作用的影响！它只由电子的总数（或密度）唯一确定。[@problem_id:2955773]

这暗示着，我们的单粒子图像虽然是一种简化，但它建立在一个非常坚实的基础之上。真实的、相互作用的电子，其行为在很多方面就像是继承了我们简单[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)论中电子属性的“[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)”。但要深入探索这个充满相互作用的奇妙世界，就是我们下一章的故事了。