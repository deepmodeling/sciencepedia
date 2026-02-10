## 引言
虽然[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)——一种[无摩擦流动](@keyword=frictionless_flow|lang=zh-CN|style=Feynman)的液体——的概念本身已是量子世界的一大奇迹，但某些[物态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)将这一边界推向了更为奇异的领域。如果流体的组分粒子不仅仅是无阻力地流动，而是被锁定在一场永恒、[同步](@keyword=entrainment|lang=zh-CN|style=Feynman)的舞蹈中，从而赋予整个系统一种内禀的旋转或“手性”，那会怎样？这就是[手性超流体](@keyword=chiral_superfluid|lang=zh-CN|style=Feynman)的现实——一种挑战我们对对称性和拓扑序理解的物态。与传统[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)中配对粒子处于静止状态不同，[手性超流体](@keyword=chiral_superfluid|lang=zh-CN|style=Feynman)拥有一种隐藏的、具有宏观效应的微观角动量。本文深入探讨了这种迷人的[量子液体](@keyword=quantum_liquids|lang=zh-CN|style=Feynman)，旨在回答当时间反演对称性在一个相干[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)中被打破时会发生什么这一根本问题。

我们的探索始于“原理与机制”一章，在其中我们将解构手性的量子力学核心，探索[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)如何形成并带有内建的角动量。我们将审视这种内禀旋转的深远影响，从基本对称性的自发破缺到决定系统边缘行为的丰富拓扑结构的出现。随后，“应用与跨学科联系”一章将探讨这种隐藏秩序的可观测效应。我们将看到这场‘量子华尔兹’如何表现为反常[输运现象](@keyword=transport_phenomena|lang=zh-CN|style=Feynman)，为难以捉摸且可应用于[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的马约拉纳费米子提供温床，并为宇宙学和高能粒子物理学的概念创造出卓越的桌面模拟系统。准备进入一个微观世界的定律与宇宙结构遥相呼应的世界吧。

## 原理与机制

想象一个满是舞者的舞厅。在通常的舞蹈中，舞伴们可能会旋转，但平均而言，整个舞厅没有净的旋转感。现在，想象一种奇特的华尔兹，每一对舞伴不仅一起旋转，而且还以一个巨大的、协调的圆圈轨道运动，全部按顺时针方向。整个舞厅，作为一个集体，现在有了一个可观的、旋转的角动量。这就是**[手性超流体](@keyword=chiral_superfluid|lang=zh-CN|style=Feynman)**的本质。与它们更常规的同类（其中配对粒子满足于静止状态）不同，[手性超流体](@keyword=chiral_superfluid|lang=zh-CN|style=Feynman)中的配对永远处于运动之中，以一种具有确定手性或**螺旋性**的舞蹈束缚在一起。

这种内禀的微观旋转是孕育出奇异而美丽的物理现象森林的种子。它打破了基本对称性，催生了自身即是[反粒子](@keyword=antiparticles|lang=zh-CN|style=Feynman)的奇异粒子，并用非平庸的拓扑结构描绘了量子真空的构造。现在，让我们来探索支配这种迷人[物态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)的原理和机制。

### 手性的核心：起舞的配对

在量子世界中，像电子或氦-3原子这样的粒子可以形成束缚对，称为**库珀对**，从而形成[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)或超导态。在最简单的情况下，即我们熟悉的**s波**配对，两个[粒子自旋](@keyword=particle_spin|lang=zh-CN|style=Feynman)相反，它们的相对运动携带零[轨道角动量](@keyword=orbital_angular_momentum_(oam)|lang=zh-CN|style=Feynman)。它们是平静的一对。

[手性超流体](@keyword=chiral_superfluid|lang=zh-CN|style=Feynman)则由更具冒险精神的配对构成。考虑其范例——**手性p波**态。“p波”告诉我们，配对具有一个单位（$l=1$）的[轨道角动量](@keyword=orbital_angular_momentum_(oam)|lang=zh-CN|style=Feynman)，就像原子[p轨道](@keyword=p_orbitals|lang=zh-CN|style=Feynman)中的电子一样。“手性”部分则告诉我们，所有这些配对都朝着同一个方向运动。这被编码在配对的[量子力学波函数](@keyword=quantum_mechanics_wavefunctions|lang=zh-CN|style=Feynman)中，在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中，其形式为：
$$
\Delta(\mathbf{k}) \propto k_x + i k_y
$$
这里，$\mathbf{k} = (k_x, k_y)$ 是两个粒子的相对动量。乍一看，这只是一个抽象的公式。但让我们更仔细地审视它。使用极坐标，$k_x = k \cos\phi_k$ 和 $k_y = k \sin\phi_k$，它变成 $\Delta(\mathbf{k}) \propto k e^{i\phi_k}$。当动量矢量 $\mathbf{k}$ 旋转一整圈时，项 $e^{i\phi_k}$ 的相位会缠绕 $2\pi$。这种“缠绕”正是角动量的标志。

在量子力学中，轨道角动量的z分量算符是 $\hat{L}_z = -i\hbar \frac{\partial}{\partial \phi_k}$。当我们“询问”[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)它的角动量是多少时会发生什么？我们将算符作用于其[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)：
$$
\hat{L}_z (k e^{i\phi_k}) = -i\hbar \frac{\partial}{\partial \phi_k} (k e^{i\phi_k}) = -i\hbar (k \cdot i e^{i\phi_k}) = \hbar (k e^{i\phi_k})
$$
[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)原封不动地返回，只是乘以了一个常数：$\hbar$。这正是本征态的定义。在此状态下的每一个[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)都处于确定的角动量态，其值恰好为$\hbar$，即角动量的基本量子。它们都以相同的方式旋转 [@problem_id:1236892] [@problem_id:1201774]。

这个原理可以推广。一个假设的**[手性d波](@keyword=chiral_d_wave|lang=zh-CN|style=Feynman)**[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)，其配对[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的缠绕速度是两倍，$\Delta(\mathbf{k}) \propto (k_x + i k_y)^2 \propto e^{i2\phi_k}$，其配对将各自携带 $2\hbar$ 的角动量。当材料中数以万亿计的配对将其微观角动量对齐时，它们会在[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)本身中产生一个宏观角动量 [@problem_id:218857]。这个物体，即使静止不动，也在量子层面上自发地、永恒地旋转。

### 一个破缺的世界：时间、空间与相位

一个优选旋转方向的出现，意味着超流体本身的对称性低于支配它的物理定律。这是一个深刻的概念，称为**[自发对称性破缺](@keyword=spontaneous_symmetry_breaking|lang=zh-CN|style=Feynman)**。

传统的[s波](@keyword=s_waves|lang=zh-CN|style=Feynman)[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)只打破一种对称性：与粒子数守恒相关的**[U(1)规范对称性](@keyword=u(1)_gauge_symmetry|lang=zh-CN|style=Feynman)**。这就是超流体中“超”的由来。但我们的手性流体更具颠覆性。

首先，通过为其内部旋转选择一个轴（例如z轴），它打破了**旋转对称性**。[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)内部的空间不再是各向同性的；存在一个特殊的方向。

其次，也是更根本的，它打破了**[时间反演对称性](@keyword=time_reversal_symmetry|lang=zh-CN|style=Feynman)（TRS）**。想象一下，拍摄一部关于轨道配对的电影，然后倒着播放。你会看到配对向相反的方向运行。用我们的配对[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)语言来说，时间倒流对应于取[复共轭](@keyword=complex_conjugation|lang=zh-CN|style=Feynman)：$(k_x + i k_y)^* = k_x - i k_y$。这描述了一个角动量为 $-\hbar$ 的状态。由于这与我们开始的状态在物理上是不同的，所以该系统在时间反演下是不对称的。这是罕见且引人注目的。大多数物质状态，从水到铁磁体，如果你把时钟倒转，在微观层面上看起来是一样的。[手性超流体](@keyword=chiral_superfluid|lang=zh-CN|style=Feynman)则不然。

根据**[戈德斯通定理](@keyword=goldstone_s_theorem|lang=zh-CN|style=Feynman)**，每一个被自发破缺的连续对称性都会产生一种新型的集体无质量激发——**[戈德斯通模](@keyword=goldstone_modes|lang=zh-CN|style=Feynman)**。这些是新的有序状态中的“涟漪”。[手性超流体](@keyword=chiral_superfluid|lang=zh-CN|style=Feynman)丰富的[对称性破缺模式](@keyword=symmetry_breaking_pattern|lang=zh-CN|style=Feynman)导致了这些模式相应地变得丰富。一个经典的现实世界例子是[超流氦-3](@keyword=superfluid_helium_3|lang=zh-CN|style=Feynman)的A相，它是由[氦原子](@keyword=helium_atom|lang=zh-CN|style=Feynman)形成的手性[p波超流体](@keyword=p_wave_superfluid|lang=zh-CN|style=Feynman)。其正常态具有自旋旋转对称性、轨道[旋转对称](@keyword=rotational_symmetry|lang=zh-CN|style=Feynman)性和相移对称性 ($G = SO(3)_S \times SO(3)_L \times U(1)_N$)。手性的A相将此对称性破缺至一个更小、更复杂的[子群](@keyword=subgroup|lang=zh-CN|style=Feynman) $H$。破缺对称性的数量，即$\dim(G) - \dim(H)$，决定了不同[戈德斯通模](@keyword=goldstone_modes|lang=zh-CN|style=Feynman)的数量。对于氦-3A，仔细计算表明，恰好有五种这样的模式，每一种都是在超流体中传播的独特类型的“[声波](@keyword=acoustic_waves|lang=zh-CN|style=Feynman)”或“自旋波” [@problem_id:1145990]。

### 拓扑之魂：边缘（与涡旋）上的生命

[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)（使其成为[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)）和破缺的[时间反演对称性](@keyword=time_reversal_symmetry|lang=zh-CN|style=Feynman)的组合，通常预示着深层[拓扑性质](@keyword=topological_property|lang=zh-CN|style=Feynman)的存在。拓扑学是研究在连续变形下保持不变的性质的数学分支。一个咖啡杯和一个甜甜圈在拓扑上是相同的，因为它们都有一个孔。

在凝聚态物质中，这个“孔”是一个[拓扑不变量](@keyword=topological_invariants|lang=zh-CN|style=Feynman)，一个像**陈数**一样的整数，它刻画了动量空间中[量子波函数](@keyword=quantum_wavefunction|lang=zh-CN|style=Feynman)的全局结构。材料体内的非零陈数是一个深刻的论断。它通过一个称为**[体-边对应](@keyword=bulk_edge_correspondence|lang=zh-CN|style=Feynman)**的原理，保证了在其边缘必定会发生非同寻常的事情。系统不能就此停止；它的边界必须承载[无能](@keyword=anergy|lang=zh-CN|style=Feynman)隙的激发。

对于二维[手性超流体](@keyword=chiral_superfluid|lang=zh-CN|style=Feynman)，这表现为**手性边缘模**：局域在样品边界的类粒子态。由于体的Chirality，这些态被禁止掉头。它们只能沿着边缘朝一个方向传播，就像单行道上的汽车一样 [@problem_id:1270812]。这些模式的能量与其沿边缘的动量成正比，$E \propto k_y$，从而导致在单一方向上的无质量、类光传播。

当我们考虑的不是外边缘，而是*内*边缘时，故事变得更加引人入胜。量子**涡旋**是[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)中的一个旋转漩涡，在漩涡中心超流体密度降为零。这个核心实际上是材料内部的一个圆柱形边界。拓扑学在这里要求什么呢？它要求在涡旋核心中存在一个特殊的、孤立的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)。并且值得注意的是，这个态的能量恰好为零，并受到体拓扑的保护 [@problem_id:250551]。

这个零能态并非普通粒子。它是一个**马约拉纳费米子**的实现——一种在1930年代首次被假设的奇异粒子，其自身即是其[反粒子](@keyword=antiparticles|lang=zh-CN|style=Feynman)。电子和正电子是不同的，但两个马约拉纳费米子可以组合成一个常规[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)，或者从一个常规[费米子](@keyword=fermion|lang=zh-CN|style=Feynman)中“分裂”出来。它们的奇异性质，特别是[非阿贝尔统计](@keyword=non_abelian_statistics|lang=zh-CN|style=Feynman)（交换它们会以非平凡的方式改变系统状态），使它们成为构建稳健的[拓扑量子计算](@keyword=topological_quantum_computing|lang=zh-CN|style=Feynman)机的主要候选者。因此，[手性超流体](@keyword=chiral_superfluid|lang=zh-CN|style=Feynman)是基础物理学的游乐场，是未来粒子的潜在孵化器。

### 隐藏秩序的可观测回响

这些理论思想虽然优美，但若没有实验结果的支撑将是空洞的。我们如何看到这种隐藏的手性舞蹈所带来的效应呢？

首先，宏观角动量应该直接显现出来。永恒的内部运动会产生一个自发的**[质量流](@keyword=mass_flow|lang=zh-CN|style=Feynman)**，沿着样品的边缘流动，即使在没有任何外加电压或力的情况下也是如此。这是[时间反演对称性](@keyword=time_reversal_symmetry|lang=zh-CN|style=Feynman)破缺的直接物理后果 [@problem_id:220085]。

其次，配对的独特性质影响了超流体如何响应其环境。
- **对无序的敏感性**：传统的[s波](@keyword=s_waves|lang=zh-CN|style=Feynman)[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)以对非磁性杂质的强大鲁棒性而闻名，这一事实被称为**[安德森定理](@keyword=anderson_s_theorem|lang=zh-CN|style=Feynman)**。手性[p波超流体](@keyword=p_wave_superfluid|lang=zh-CN|style=Feynman)没有这样的保护。因为配对[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)具有方向依赖的相位（$e^{i\phi_k}$），一个散射粒子的杂质可以轻易地破坏配对精密的相干关系，从而将其拆散。这意味着*任何*类型的杂质都充当了强有力的配对破坏者，抑制了超流体转变温度 [@problem_id:1219024]。
- **低能激发**：用少量热量探测系统，会揭示出另一个特征。与具有“硬”[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)的传统[超流体](@keyword=superfluids|lang=zh-CN|style=Feynman)不同，手性[p波超流体](@keyword=p_wave_superfluid|lang=zh-CN|style=Feynman)具有“软”[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。它的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)在两个点（费米球的“两极”）上消失，允许以任意低的能量创建激发。这导致[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)**[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)**在零能量附近随能量线性增长，$N(E) \propto E$ [@problem_id:1236851]。这种行为直接影响了可测量的量，如低温下的[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)。

最后，最深刻的标志在于其拓扑响应。系统对外部场（如[电磁场](@keyword=electromagnetic_field|lang=zh-CN|style=Feynman)）的反应是量子化的。其有效的低能理论包含一个特殊部分，称为**[陈-西蒙斯项](@keyword=chern_simons_term|lang=zh-CN|style=Feynman)**。该项的系数，或称“能级”，是一个量子化的拓扑数。对于手性[p波超流体](@keyword=p_wave_superfluid|lang=zh-CN|style=Feynman)，这个能级预计为 $k=1/2$ [@problem_id:1177394]。这种半整数的量子化是其底层马约拉纳物理学明确无误的指纹。这是物理学统一性的一个惊人例子，宏观属性（如霍尔[电导率](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)）揭示了系统组分粒子最根本和最奇异的本质。配对之舞在整个物理定律的结构中回响。