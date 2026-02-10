## 引言
在广阔而复杂的晶体材料世界中，数十亿电子彼此相互作用，并与周期性[排列](@keyword=permutation|lang=zh-CN|style=Feynman)的原子阵列相互作用，从而产生了定义我们技术世界的各种性质，从[电导率](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)到磁性。我们如何为这种量子混沌带来秩序？答案就在于[费米学](@keyword=fermiology|lang=zh-CN|style=Feynman)（Fermiology），即对一个基础而又抽象的概念——[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)（Fermi surface）的研究。本文旨在解决从支配单个电子的微观规则，到对其集体行为形成预测性理解这一挑战。我们将首先深入探讨“原理与机制”，探索什么是费米面，[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)如何塑造其复杂的形状，以及支配其存在的量子规则。随后，在“应用与跨学科联系”部分，我们将揭示科学家如何通过实验绘制这个无形的表面，并利用它来预测和理解物理学中一些最深刻的现象，包括超导电性和奇异[拓扑材料](@keyword=topological_materials|lang=zh-CN|style=Feynman)的涌现。

## 原理与机制

### 动量空间中的电子海

想象一下晶体内部的电子。它们受制于奇妙的量子力学定律，其中最重要的一条是**[泡利不相容原理](@keyword=pauli_exclusion_principle|lang=zh-CN|style=Feynman)**。该原理告诉我们，没有两个电子可以占据完全相同的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。从某种意义上说，它们是极度独立的个体。在绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)，当所有热骚动都停止时，这些电子并非静止不动。相反，它们会逐个填充到最低的[可用能](@keyword=available_energy|lang=zh-CN|style=Feynman)态中，就像将水倒入容器一样。

现在，让我们进入一个更抽象但极其强大的视角。我们不再考虑电子的位置，而是考虑它的动量。在晶体中，这更精确地称为**晶体动量**，用矢量$\hbar\mathbf{k}$表示。所有可能动量矢量的空间就是我们所说的**[k空间](@keyword=k_space|lang=zh-CN|style=Feynman)**，或称倒易空间。它像是一张地图，描绘了电子所有可能的直线运动。在这个空间中，每个点$\mathbf{k}$代表一个具有特定动量和能量$\varepsilon(\mathbf{k})$的态。

当我们在绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)下向晶体中添加电子时，它们会从最低能量处（通常在中心$\mathbf{k}=0$处）开始，向外填充k空间中的可用态。这就在[k空间](@keyword=k_space|lang=zh-CN|style=Feynman)中形成了一个被称为**[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)**的已占据态区域。这个“海”的“表面”，即分隔已填充态与空态的边界，是一个极其重要的对象：**[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)**。[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)上的每个态都具有相同的能量，即**费米能**$E_F$。它是浩瀚、沉寂的电子海洋的海岸线。

你可能会问，既然所有这些电子都以有限的动量（[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)上的任何点的动量大小为$p_F = \hbar k_F$）飞驰，为什么一块金属不会自发地从桌子上飞走？这个明显的悖论有一个植根于对称性的优美解答。对于处于$\mathbf{k}$态的每一个电子，都存在一个能量完全相同、位于$-\mathbf{k}$的[对应态](@keyword=corresponding_states|lang=zh-CN|style=Feynman)。这是**[时间反演对称性](@keyword=time_reversal_symmetry|lang=zh-CN|style=Feynman)**的一个深刻推论：在没有[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的情况下，如果你把物理过程的影片倒着放，基本物理定律同样适用。这种对称性确保了如果一个态$\mathbf{k}$是费米海的一部分，那么它的反向态$-\mathbf{k}$也是。当你把所有动量矢量相加时，它们会成对抵消。整个费米海的*平均*动量恰好为零，即使[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)上的每个电子都不是静止的[@problem_id:2988974]。这片海是完全平静的，不携带任何净电流。

### 晶体的影响：布里渊区

到目前为止，我们想象的电子处于一个均匀、空旷的空间中，这导致了一个简单的球形费米海。但真实的晶体绝非空旷。它是由原子核构成的高度有序、周期性[排列](@keyword=permutation|lang=zh-CN|style=Feynman)的结构——[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。这种周期性背景对于电子的量子波来说，就像一个精密的衍射光栅。

这种相互作用从根本上重构了k空间。电子波只有在特定波长下才能无散射地传播；而对于其他波长，它们会经历强烈的[布拉格反射](@keyword=bragg_reflection|lang=zh-CN|style=Feynman)。这把连续的[k空间](@keyword=k_space|lang=zh-CN|style=Feynman)“切割”成了一系列重复的区域，称为**布里渊区**。

有一种非常直观的方法可以构建其中最重要的一个，即[第一布里渊区](@keyword=first_brillouin_zone|lang=zh-CN|style=Feynman)。首先，我们将晶体的正空间[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)映射到k空间中，创建所谓的**[倒易晶格](@keyword=reciprocal_lattice|lang=zh-CN|style=Feynman)**。这个新[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)由点构成，每个点$\mathbf{G}$代表一个能引起[布拉格反射](@keyword=bragg_reflection|lang=zh-CN|style=Feynman)的矢量。[k空间](@keyword=k_space|lang=zh-CN|style=Feynman)的中心，$\mathbf{k}=0$，被称为$\Gamma$点。要找到[第一布里渊区](@keyword=first_brillouin_zone|lang=zh-CN|style=Feynman)，你只需找到[k空间](@keyword=k_space|lang=zh-CN|style=Feynman)中比其他任何倒易格点都更靠近$\Gamma$点的区域。从几何上看，你可以通过从$\Gamma$点向其所有相邻的倒易格点画线，然后构建这些线段的垂直平分面来实现。这些平面所包围的最小体积就是[第一布里渊区](@keyword=first_brillouin_zone|lang=zh-CN|style=Feynman)[@problem_id:2810706]。这些边界平面正是[布拉格反射](@keyword=bragg_reflection|lang=zh-CN|style=Feynman)最强的位置。

你可以把布里渊区想象成一个形状独特的容器，用来容纳我们的[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)。容器的形状完全由[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的对称性决定。对于二维的简单[正方晶格](@keyword=square_lattice|lang=zh-CN|style=Feynman)，布里渊区是一个正方形；对于像铝这样的真实三维材料，它具有[面心立方](@keyword=face_centered_cubic|lang=zh-CN|style=Feynman)（FCC）结构，其[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)是一个美丽的多面体，称为截角八面体。

### 形形色色的[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)：口袋和怪物

当不断扩张的[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)表面碰到[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)的坚硬“壁垒”时会发生什么？动量处于[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)边界的电子会经历[布拉格反射](@keyword=bragg_reflection|lang=zh-CN|style=Feynman)，这意味着它的波会与自身干涉形成[驻波](@keyword=standing_waves|lang=zh-CN|style=Feynman)。这种相互作用打开了一个**[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)**。自由电子的简单、连续的能量-动量关系被打破，[能谱](@keyword=energy_spectrum|lang=zh-CN|style=Feynman)分裂成不同的**[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)**。

这对费米面的影响是巨大的。[自由电子模型](@keyword=free_electron_model_2|lang=zh-CN|style=Feynman)的简单球体被扭曲、弯折，并以复杂的方式重新连接。在许多金属中，自由电子球实际上比[第一布里渊区](@keyword=first_brillouin_zone|lang=zh-CN|style=Feynman)更大。为了理解真实的费米面，我们使用一种巧妙的记账方法，称为**[Harrison构造](@keyword=harrison_construction|lang=zh-CN|style=Feynman)法**：我们将球体“溢出”布里渊区边界的部分“折叠”回[第一布里渊区](@keyword=first_brillouin_zone|lang=zh-CN|style=Feynman)内。

以铝为例。它是一种FCC金属，每个原子有三个价电子。它的自由电子球非常大，以至于远超出了[第一布里渊区](@keyword=first_brillouin_zone|lang=zh-CN|style=Feynman)。当我们执行折叠过程时，一个奇妙的新图像出现了[@problem_id:2971146]。
- 中心区域费米面的主要部分不再是一个完整的球体。它在接触[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)边界的地方出现了缺失，看起来像一个带有孔洞的、膨胀的圆角立方体。这些*未占据*态的区域，看起来像是已填充的海洋中的气泡，其行为在各方面都像带正电的粒子。我们称之为**空穴口袋**。它们就像在[费米能](@keyword=fermi_energy|lang=zh-CN|style=Feynman)的海平面确定后留下的岛屿。
- 球体溢出到邻近[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)的部[分形](@keyword=fractal|lang=zh-CN|style=Feynman)成了新的、不连续的表面。这些是*已占据*态的小块区域，呈透镜形状，就像在高海拔山谷中形成的水坑。我们称之为**[电子口袋](@keyword=electron_pockets|lang=zh-CN|style=Feynman)**。

铝以及大多数金属的最终[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)不是一个简单的球体，而是一个复杂的、通常很美丽的“怪物”，它是由具有电子和空穴两种特性的复杂表面集合而成。其精确形状可以通过**[紧束缚模型](@keyword=tight_binding_model|lang=zh-CN|style=Feynman)**[@problem_id:121178]等模型计算出来，是材料的独特指纹。

此外，这种拓扑结构并非总是固定的。如果我们挤压材料（施加压力）或增减电子（掺杂），我们实际上是在改变“海平面”（[费米能](@keyword=fermi_energy|lang=zh-CN|style=Feynman)）或[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman)的“地形”。在某些[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，费米面会发生突发的[拓扑变化](@keyword=topological_changes|lang=zh-CN|style=Feynman)——一个半岛可能与大陆相连，或者一个岛屿可能沉没在波浪之下。这就是**利弗席兹[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)**（Lifshitz transition）[@problem_id:121178] [@problem_id:56963]，一种[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的真实[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)，可以极大地改变材料的性质。

### 探测无形之物：量子[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)

这一切都是一幅优美的理论图景。但我们究竟如何才能“看到”这些存在于抽象[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中的复杂形状呢？由Lars Onsager发现的关键在于施加一个强大而均匀的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)$\mathbf{B}$。

在[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中，电子被迫沿圆形（或更普遍的，环形）路径运动。在半经典图像中，[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)上的电子同样受到约束。它的动量矢量$\mathbf{k}$将在[k空间](@keyword=k_space|lang=zh-CN|style=Feynman)中描绘出一个闭合环路。这个环路就是等能量的费米面与垂直于[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的平面的交线。

接下里是量子魔法的时刻。就像原子的能级一样，这些回旋轨道也是量子化的！并非任何轨道都是允许的。**Onsager-Lifshitz[量子化条件](@keyword=quantization_conditions|lang=zh-CN|style=Feynman)**指出，一个允许的轨道在[k空间](@keyword=k_space|lang=zh-CN|style=Feynman)中所包围的面积$A$必须满足一个简单的规则：
$$ A_n = \frac{2\pi e B}{\hbar} (n + \gamma) $$
其中$n$是整数，$e$是元[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，$\hbar$是[约化普朗克常数](@keyword=reduced_planck_constant|lang=zh-CN|style=Feynman)，$\gamma$是一个包含微妙但重要[物理信息](@keyword=physical_information|lang=zh-CN|style=Feynman)的相位因子，其中包括被称为**[贝里相位](@keyword=berry_s_phase|lang=zh-CN|style=Feynman)**（Berry phase）的电子路径几何信息[@problem_id:2818251]。

这是一个惊人的结果。一个几何属性——动量空间中的面积——被直接量子化了。对于给定的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，[k空间](@keyword=k_space|lang=zh-CN|style=Feynman)中允许的电子态被限制在一系列同心圆柱（在三维中）上，这些圆柱被称为**朗道管**。这些管的[横截面](@keyword=cross_section|lang=zh-CN|style=Feynman)积由[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)决定。

随着我们增加[磁场强度](@keyword=magnetic_field_intensity|lang=zh-CN|style=Feynman)，这些管的半径会增大。它们会逐一扫过材料固定的费米面。每当一个朗道管的边缘穿过[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)时，系统的总能量就会发生突变，导致材料的宏观性质（如电阻或磁化强度）发生微小的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。

### 费米面的交响乐

通过测量这些[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，我们可以聆听费米面的交响乐。让我们考虑磁化强度的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，这一现象被称为**德哈斯-范阿尔芬（dHvA）效应**。关键的洞见是，[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的周期性不是针对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)$B$，而是针对其倒数$1/B$。给定[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的*频率*$F$与[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)垂直于[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)方向的**极端[截面](@keyword=cross_section_2|lang=zh-CN|style=Feynman)积**$A_{ext}$成正比：
$$ F = \frac{\hbar}{2\pi e} A_{ext} $$
这为我们提供了通往k空间几何的直接途径！例如，如果我们的[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)形状像一个波纹状的圆柱体，施加沿轴线的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)将揭示两个极端[截面](@keyword=cross_section_2|lang=zh-CN|style=Feynman)积：一个小的“颈部”面积和一个大的“腹部”面积。dHvA测量将显示出两种不同频率的叠加[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，从而使我们能够测量颈部和腹部的大小[@problem_id:2812611]。通过旋转[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)并在每个角度测量频率组合，我们可以进行一种量子层析成像，painstakingly 重建出费米面的完整三维形状。

但信号中还有更多的音乐。这些[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的*振幅*也携带着宝贵的信息。当我们升高温度时，热致弥散会导致[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)衰减。振幅衰减的速率由朗道管之间的间距决定，而这个间距又取决于电子的**[回旋质量](@keyword=cyclotron_mass|lang=zh-CN|style=Feynman)**$m_c$。通过仔细测量不同温度下的振幅，我们可以使用**[Lifshitz-Kosevich公式](@keyword=lifshitz_kosevich_formula|lang=zh-CN|style=Feynman)**来确定该特定极端轨道上电子的$m_c$ [@problem_id:2980361]。

这个[回旋质量](@keyword=cyclotron_mass|lang=zh-CN|style=Feynman)不是真空中自由电子的质量。它是一个**有效质量**，一个概括了电子如何与[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)相互作用的数字。而物理学的统一性再次展现其魅力，这个动态定义的质量与[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)本身的几何形状相关联：
$$ m_c = \frac{\hbar^2}{2\pi} \left( \frac{\partial A}{\partial E} \right)_{E=E_F} $$
质量与轨道面积随能量变化的快慢成正比。能量景观中“平坦”的区域对应于重的质量，而“陡峭”的区域则对应于轻的质量。通过分析dHvA交响乐——它的频率和振幅——我们不仅可以绘制[费米海](@keyword=fermi_sea|lang=zh-CN|style=Feynman)的地理图，还可以“称量”生活在其海岸上的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的重量。

### 现代前沿：重构与涌现

[费米学](@keyword=fermiology|lang=zh-CN|style=Feynman)远非物理学中一个已经完结的篇章。它是探索最奇异、最复杂的量子物质形态的重要工具。在许多现代材料中，电子不只是被动地响应静态的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。它们会[自组织](@keyword=self_organization|lang=zh-CN|style=Feynman)成新的集体[物态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)，例如磁性或超导电性。这些新的有序模式本身可以充当一个新的、有效的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，深刻地改变电子结构。

考虑一种变为反铁磁性的材料。[电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)以交替的向上-向下模式[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。这种新的自旋周期性（可能不同于底层的原子周期性）会创建一个新的、更小的布里渊区（“磁布里渊区”）。原始的[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)在这个新区域的边界处被折叠、切割和重新缝合，从而形成一个完全**重构的费米面**[@problem_id:2810766]。一个简单、大的[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)可以分裂成小口袋，或者它的某些部分可能被完全破坏（打开[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)）。

这种重构可[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)来惊人的后果。例如，如果在这种材料中出现超[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)，[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)所感受到的有效超导能隙将取决于它在*重构*表面上的位置。对于一个常规的s波[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)来说，它应该具有均匀、无节点的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)，但它可能会出现“意外”的节点——[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)消失的点——这些点恰好位于重构的费米口袋与旧的磁布里渊区边界相交的地方[@problem_id:2810766]。理解费米面的形状和拓扑结构成为解开这些复杂的、共存的量子序的关键。

费米面的几何形状甚至在正空间中留下了它的印记。金属中的单个杂质不仅仅是造成一个局部扰动；它会在电子电荷密度中激发出随距离衰减的涟漪。这些**[弗里德尔振荡](@keyword=friedel_oscillations|lang=zh-CN|style=Feynman)**的波长和模式由费米面的尺寸决定[@problem_id:670912]。从一个非常直接的意义上说，[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)的形状支配着电子在正空间中形成的模式。因此，费米面不仅仅是一个理论构想；它是协调晶体材料丰富而往往出人意料的电子生活的根本实体。