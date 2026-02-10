## 引言
在固体的量子世界中，材料通常被分为电子无法流动的绝缘体或电子可以自由移动的金属。在这两种为人熟知的状态之间，存在一个奇特而迷人的前沿领域：[拓扑半金属](@keyword=topological_semimetals|lang=zh-CN|style=Feynman)的王国。这些材料既不完全是金属，也不完全是绝缘体；相反，它们的电子[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)以[孤立点](@keyword=isolated_point|lang=zh-CN|style=Feynman)或线的形式接触，这种接触方式因对称性和拓扑学的深层原理而异常稳固。这种独特的[电子结构](@keyword=electronic_structure|lang=zh-CN|style=Feynman)赋予了它们奇异的性质，将普通的晶体变成了桌面宇宙，在其中电子的行为可以像来自时间之初的奇异粒子。

本文旨在回答围绕这些材料的基本问题：是什么让它们具有“拓扑”性？为什么这一概念彻底改变了凝聚态物理学？我们将揭开支配其存在的原理的神秘面纱，并探索由此产生的惊人后果。通过两个核心部分的导航，您将对这个前沿领域获得全面的理解。我们的旅程始于这些材料背后的基本理论，然后转向它们的具体表现和深远影响。

首先，在“原理与机制”部分，我们将深入理论核心，探索[晶体对称性](@keyword=crystal_symmetry|lang=zh-CN|style=Feynman)如何创造出从 [Dirac 点](@keyword=dirac_points|lang=zh-CN|style=Feynman)到节线的各种[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)接触。我们将揭示 Weyl 点作为[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中拓扑磁单极子的本质，并了解这如何导致它们最著名的特征之一：受保护的表面[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)。然后，在“应用与跨学科联系”部分，我们将理论与现实联系起来。我们将看到[实验物理学](@keyword=experimental_physics|lang=zh-CN|style=Feynman)家如何“拍摄”这些幽灵般的电子态，并见证它们奇特的量子行为。我们还将探讨它们的独特性质（如[手性反常](@keyword=axial_anomaly|lang=zh-CN|style=Feynman)）如何可能推动新一代电子和[能量收集](@keyword=energy_harvesting|lang=zh-CN|style=Feynman)设备的发展，以及这些材料如何与粒子物理学和宇宙学建立起惊人的联系。

## 原理与机制

好了，让我们着手深入探讨[拓扑半金属](@keyword=topological_semimetals|lang=zh-CN|style=Feynman)运作的核心。我们听说它们奇特而美妙，但*为什么*会这样？答案，如同物理学中许多深刻的真理一样，在于对称性与几何学之间美妙的相互作用。但这里的几何结构并非晶体本身，而是电子动量这个奇特、抽象的世界——布里渊区的几何结构。

### [能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)接触的“动物园”：点、线与对称性

想象一下晶体中电子允许的能级，我们称之为[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)。在绝缘体中，最高填充[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)（价带）与最低空[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)（导带）之间被一个[禁带](@keyword=forbidden_zone|lang=zh-CN|style=Feynman)隔开。在普通金属中，某个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)仅被部分填充，因此电子只需微小的推动就能自由移动。[半金属](@keyword=half_metal|lang=zh-CN|style=Feynman)是介于两者之间的一种特殊情况：价带和导带刚好*接触*。在这些接触点，没有[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。

现在，有趣的问题来了：它们*如何*接触？在电子动量的三维空间中，这种接触可以以不同方式发生。

-   它们可能在孤立的、离散的点上接触，就像两座山峰在云中轻吻。这些是 **Dirac** 和 **Weyl [半金属](@keyword=half_metal|lang=zh-CN|style=Feynman)**。
-   它们可能沿着一条连续的一维曲线接触，形成一个完整的环或接触线，就像一道山脊。这些是**[节线半金属](@keyword=nodal_line_semimetals|lang=zh-CN|style=Feynman)** (nodal-line semimetals) [@problem_id:1827877]。

你可能会认为，让两个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)接触是一种精巧的平衡之举。你说得对！对于三维空间中的一个普遍的双[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)系统，通常需要满足三个独立的数学条件才能强制产生简并。这就像要将三个独立的旋钮精确地调到零才能点亮一盏灯。在一个三维参数空间（即我们的动量空间，分量为 $k_x, k_y, k_z$）中，这种精细调节通常只会发生在孤立点上。这就是为什么点状接触在某种意义上是“最自然”或最普遍的一种。它们具有所谓的**3的余维 (codimension of 3)**。

要得到一条接触点构成的*线*——一个一维物体——我们需要余维为2。这意味着只需要满足两个条件。这怎么可能呢？只有当某个基本原理替我们自动将其中一个隐喻性的“旋钮”保持在零位，自动满足其中一个条件时，才可能实现。这个原理就是**对称性**。例如，如果一个晶体具有[镜面](@keyword=mirror_plane|lang=zh-CN|style=Feynman)对称性，那么[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中[镜面](@keyword=mirror_plane|lang=zh-CN|style=Feynman)上的[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)可以根据它们的镜面[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)来标记。如果两个[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)具有不同的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)，晶体的对称性会禁止它们混合。这就消除了避免交叉的一个条件，只剩下两个。在三个变量（$k_x, k_y, k_z$）中求解两个方程，通常会得到一条线——于是，一条受对称性保护的[节线](@keyword=nodal_lines|lang=zh-CN|style=Feynman)就诞生了 [@problem_id:3007282]。

### 问题的核心：Weyl 点和 [Dirac 点](@keyword=dirac_points|lang=zh-CN|style=Feynman)

让我们聚焦于那些点状接触。事实证明，它们主要有两种类型，由它们的简并度——在接触点处具有相同能量的电子态数量——来区分。

最基本的构筑单元是一个称为 **Weyl 点**的二重简并点。在这个点附近，电子的行为就像粒子物理学中首次构想的无质量 Weyl [费米子](@keyword=fermion|lang=zh-CN|style=Feynman)。这些是奇特的“手性”粒子，要么是左手的，要么是右手的。拥有这些粒子的材料就是 **Weyl 半金属**。

另一类是称为 **Dirac 点**的四重简并点，这里的电子行为像无质量的 [Dirac 费米子](@keyword=dirac_fermions|lang=zh-CN|style=Feynman)。这与石墨烯中的情况类似，但我们这里谈论的是它们在 **[Dirac 半金属](@keyword=dirac_semimetals|lang=zh-CN|style=Feynman)**中的三维表亲。

那么它们之间有什么关系呢？事实证明，Dirac 点并非那么基本。它可以被理解为两个具有相反“手性”（或手征性）的 Weyl 点恰好重叠在一起，其简并性受到晶体对称性的保护和强制 [@problem_id:2870328]。将它们锁在一起的关键对称性是**[时间反演对称性](@keyword=time_reversal_symmetry|lang=zh-CN|style=Feynman) (T)** 和**空间反演对称性 (P)**。[时间反演对称性](@keyword=time_reversal_symmetry|lang=zh-CN|style=Feynman)意味着如果你让时间倒流，物理定律看起来是一样的。空间反演对称性意味着如果你通过晶体的[中心点](@keyword=medoid|lang=zh-CN|style=Feynman)观察，晶体看起来是一样的。

如果一种材料同时具有 T 和 P 对称性，那么在动量 $\mathbf{k}$ 处具有一手性的 Weyl 点，必然在同一点 $\mathbf{k}$ 处与另一个相反手性的 Weyl 点共存。它们被钉在一起，形成一个四重简并的 [Dirac 点](@keyword=dirac_points|lang=zh-CN|style=Feynman)。

但是，如果我们打破其中一个对称性会发生什么？如果我们打破空间[反演对称性](@keyword=inversion_symmetry|lang=zh-CN|style=Feynman)（通过使用一个没有对称中心的晶体）或时间反演对称性（例如，通过使材料具有磁性），我们就消除了将两个 Weyl 点粘合在一起的胶水。[Dirac 点](@keyword=dirac_points|lang=zh-CN|style=Feynman)变得不稳定，分裂成一对 Weyl 点，在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中彼此分开 [@problem_id:1827852]。四重简并被解除，我们得到的是二重简并的 Weyl 点。从 [Dirac 半金属](@keyword=dirac_semimetals|lang=zh-CN|style=Feynman)到 Weyl [半金属](@keyword=half_metal|lang=zh-CN|style=Feynman)的这种转变，完美地展示了对称性如何决定物质的基本属性。

### [动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)：Weyl 节点的拓扑学

这就是我们名字中“拓扑”部分的由来。这有点抽象，但与我们熟悉的东西——[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)——的类比却异常有力。

在量子力学中，[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的相位是不可观测的，我们可以自由地在局部改变它。这被称为**规范自由度**。这种自由度带来了深远的影响。与晶体中电子[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)相关的是一个称为**[贝里联络](@keyword=berry_connection|lang=zh-CN|style=Feynman)**的数学对象，其作用就像[电磁学中的矢势](@keyword=vector_potential_electromagnetism|lang=zh-CN|style=Feynman)。与矢势一样，[贝里联络](@keyword=berry_connection|lang=zh-CN|style=Feynman)本身是依赖于规范的；它不是一个直接的[物理可观测量](@keyword=physical_observables|lang=zh-CN|style=Feynman) [@problem_id:2532792]。

然而，如果我们对动量空间中的这个[贝里联络](@keyword=berry_connection|lang=zh-CN|style=Feynman)取“旋度”，我们会得到一个称为**[贝里曲率](@keyword=berry_curvature|lang=zh-CN|style=Feynman)** $\mathbf{\Omega}_n(\mathbf{k})$ 的新量。就像[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $\mathbf{B}$ 是矢势 $\mathbf{A}$ 的旋度一样，[贝里曲率](@keyword=berry_curvature|lang=zh-CN|style=Feynman)是规范*不变的*。它是[能带结构](@keyword=e_k_diagram|lang=zh-CN|style=Feynman)的一个真实的、物理的属性。你可以把它想象成一个生活在抽象[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中的有效磁场。

那么，Weyl 点有什么特别之处呢？它们充当了这种贝里曲率的**[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)**——源或汇！Weyl 点是[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中的一个点，贝里曲率场线从该点向外辐射（源）或向内汇聚（汇）。穿过包围 Weyl 点的表面的这个“[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)”的总通量被量子化为一个整数。这个整数，$+1$ 或 $-1$，就是 Weyl 点的**手性**，其基本的[拓扑荷](@keyword=topological_charge|lang=zh-CN|style=Feynman) [@problem_id:2870328]。

这个图像引出了一个被称为 **Nielsen-Ninomiya 定理**的强力约束。[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)是周期性的，因此是一个闭合空间（就像甜甜圈的表面）。就像在一块磁铁上不能只有一个磁北极而没有磁南极一样，在闭合的布里渊区中也不能有净磁单极子荷。总通量必须为零。这意味着一个晶体中所有 Weyl 点的手性之和必须为零 [@problem_id:1827866]。Weyl 点*必须*成对出现，且手性相反。这不仅仅是一个建议；这是一个深刻的拓扑定律。一个拥有两个 $(+1)$ 节点和一个 $(-1)$ 节点的材料是根本不允许存在的。这种[拓扑荷](@keyword=topological_charge|lang=zh-CN|style=Feynman)守恒也意味着两个相[同手性](@keyword=homochirality|lang=zh-CN|style=Feynman)的 Weyl 点不能简单地相遇并消失；它们受到[拓扑保护](@keyword=topological_protection|lang=zh-CN|style=Feynman)，不会湮灭 [@problem_id:1122835]。

由于 [Dirac 点](@keyword=dirac_points|lang=zh-CN|style=Feynman)只是一个 $(+1)$ 和一个 $(-1)$ 的 Weyl 点重合在一起，其净手性为零，这与该规则是一致的 [@problem_id:2870328]。

同样值得注意的是，围绕 Weyl 点的能量[色散](@keyword=frequency_dispersion|lang=zh-CN|style=Feynman)锥的倾斜度可以变化。在 **I 型** Weyl 半金属中，锥体是直立的，在 Weyl 点能量处，费米面收缩为一个点。但在 **II 型**半金属中，锥体极度倾斜，以至于翻倒。这导致即使在 Weyl 点的能量处，也存在着在节点处接触的[电子和空穴](@keyword=electrons_and_holes|lang=zh-CN|style=Feynman)态的口袋共存的情况 [@problem_id:1827824]。这种倾斜也对物理性质产生深远影响，例如材料对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的响应。

### 不容错辨的特征：受保护的[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)

好，我们现在知道了在晶体体材料内部隐藏着这些迷人的拓扑荷。我们如何才能希望能看到它们呢？这就需要另一个深刻的原理，即**[体-边对应](@keyword=bulk_edge_correspondence|lang=zh-CN|style=Feynman)**。它指出，如果材料的体态具有非平庸的拓扑性质，其表面*必须*承载着无法独立存在的[奇异金属](@keyword=strange_metals|lang=zh-CN|style=Feynman)态。

对于 Weyl 半金属，其体态具有这些分离的贝里曲率[磁单极子](@keyword=magnetic_monopoles|lang=zh-CN|style=Feynman)（+1和-1）。[体-边对应](@keyword=bulk_edge_correspondence|lang=zh-CN|style=Feynman)要求这些点必须在[晶体表面](@keyword=crystal_surface|lang=zh-CN|style=Feynman)上连接起来。其结果是该领域最引人注目的预测之一：**[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)**。

与普通金属表面上形成闭合环路的态不同，Weyl [半金属](@keyword=half_metal|lang=zh-CN|style=Feynman)的表面态形成开放的弧线。一条弧线从表面布里渊区上一个手性的 Weyl 点的投影处开始，穿过表面布里渊区，终止于一个相反手性的 Weyl 点的投影处 [@problem_id:1827857]。它们就像[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中的一座桥梁，连接着源和汇。

“拓扑保护”部分意味着这些弧线异常坚固。你无法通过小的扰动来消除它们。想象一下你有一个显示出这些[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)的样品。现在，你在上面沉积一层薄薄的普通、非磁性的污垢（一种绝缘体）。对于一个平庸的金属，这很可能会破坏[表面态](@keyword=surface_states|lang=zh-CN|style=Feynman)并打开一个[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。但对于 Weyl 半金属，这些弧线仍然存在！它们的存在是由体态的[拓扑性质](@keyword=topological_property|lang=zh-CN|style=Feynman)保证的，而非表面的具体[化学成分](@keyword=chemical_composition|lang=zh-CN|style=Feynman)。这种稳定性是告诉实验物理学家他们发现的是 Weyl 半金属，而不仅仅是某种乏味的、平庸金属的确凿证据 [@problem_id:1827857]。

这些奇特的[能带结构](@keyword=e_k_diagram|lang=zh-CN|style=Feynman)也引出了独特的物理性质。例如，I 型 Weyl 节点附近的可用电子态数量不是随能量线性增长，而是二次增长（$g(E) \propto E^2$），这是三维线性锥状色散关系的直接结果 [@problem_id:103668]。这个微妙的特征，连同[费米弧](@keyword=fermi_arcs|lang=zh-CN|style=Feynman)和其他现象（如[手性反常](@keyword=axial_anomaly|lang=zh-CN|style=Feynman)），使得这些材料不仅是理论上的好奇之物，更是一个发现新物理和潜在新型电子器件的活跃平台。