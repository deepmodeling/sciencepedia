## 引言
超导性表现为一种完美的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，其定义特征是完全排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，即所谓的迈斯纳效应。然而，自然界常常在这种绝对之间找到折衷。对于一大类被称为[第二类超导体](@keyword=type_ii_superconductors_2|lang=zh-CN|style=Feynman)的材料而言，暴露在[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中并不会导致其完全失效，而是会形成一种新的、复杂的[物相](@keyword=phases_of_matter|lang=zh-CN|style=Feynman)。本文旨在探讨这些材料如何通过允许[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)以一种高度有序、量子化的方式进入，从而与[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)“达成休战”这一引人入胜的问题。其结果便是[阿布里科索夫涡旋晶格](@keyword=abrikosov_vortex_lattice|lang=zh-CN|style=Feynman)——一个由量子漩涡构成的美妙的微观晶体。在接下来的章节中，我们将探讨支配这一现象的基本物理学及其深远影响。“原理与机制”一章将揭示为何这些涡旋必须存在，它们如何被量子化，以及为何它们会[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成特定的三角图案。随后的“应用与跨学科联系”一章将展示这一曾被视为问题的特性，如何转变为现代技术的基石和基础科学发现的强大工具。

## 原理与机制

### 伟大的折衷：为何涡旋必须存在

想象你是一块[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)。你最核心的特征，你的身份认同，就是对[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)强迫症般的憎恨。当[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)靠近时，你会在表面产生完美的、反向流动的电流来将其完全排出——这便是著名的**[迈斯纳效应](@keyword=the_meissner_effect|lang=zh-CN|style=Feynman)**。这是一个原则问题。对于某一类被称为**[第一类超导体](@keyword=type_i_superconductor_2|lang=zh-CN|style=Feynman)**的材料来说，这是唯一的途径。它们以英勇的固执维持着其内部完美的无场状态，直到外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)变得过强，达到一个称为**[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)临界场** $H_c$ 的值。此时，它们再也无法抵抗，彻底屈服，让[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)涌入，同时自身变回普通的正常金属。这是一个一阶的、全有或全无的[相变](@keyword=phase_transition|lang=zh-CN|style=Feynman)。

但自然界往往比“全有或全无”更为微妙。它钟爱一种好的折衷。这就引出了另一类更常见的材料：**[第二类超导体](@keyword=type_ii_superconductors_2|lang=zh-CN|style=Feynman)**。它们有何不同？答案在于两种支配[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)生命的基本长度尺度之间的奇妙竞争。

第一种是**[相干长度](@keyword=healing_length|lang=zh-CN|style=Feynman)**，用 $\xi$ 表示。可以把它想象成超导电性的“愈合距离”。如果你以某种方式迫使一个区域变为非超导态（正常态），$\xi$ 就是超导态恢复其全部强度所需的[最小距离](@keyword=minimum_distance|lang=zh-CN|style=Feynman)。它是库珀对[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的特征尺寸，是超导态的本质所在。

第二种是**[磁穿透深度](@keyword=magnetic_penetration_depth|lang=zh-CN|style=Feynman)**，$\lambda$。这是外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)能够穿透到[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)内，在被屏蔽[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)完全抵消之前所能达到的特征距离。

现在，考虑一个正常区域（充满[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)）和超导区域（没有[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)）之间的界面。创建这堵墙是有能量成本的，即**[表面能](@keyword=surface_energy|lang=zh-CN|style=Feynman)**。这个能量是两种对立趋势之间斗争的结果 [@problem_id:3021315]。一方面，你会损失一些[凝聚能](@keyword=condensation_energy|lang=zh-CN|style=Feynman)——即你最初通过成为[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)而获得的能量——因为在墙附近一个尺寸为 $\xi$ 的区域内，超导序必须被抑制。这是一个正的能量贡献，一种能量上的惩罚。另一方面，通过允许[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)存在于墙的一侧，你节省了试图排斥它所要花费的能量。这种节省发生在长度尺度 $\lambda$ 上，带来一个负的能量贡献。

这场斗争的胜负由无量纲的**[金兹堡-朗道参数](@keyword=ginzburg_landau_parameter|lang=zh-CN|style=Feynman)** $\kappa = \lambda/\xi$ 决定。

-   如果 $\kappa < 1/\sqrt{2}$，[相干长度](@keyword=healing_length|lang=zh-CN|style=Feynman) $\xi$ 相对较大。抑制超导电性的成本很高，超过了让[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)进入所带来的好处。[表面能](@keyword=surface_energy|lang=zh-CN|style=Feynman)为正。创建这样的墙在能量上是不利的。这就是[第一类超导体](@keyword=type_i_superconductor_2|lang=zh-CN|style=Feynman)的世界。它们不惜一切代价避免内部墙的存在。

-   如果 $\kappa > 1/\sqrt{2}$，穿透深度 $\lambda$ 相对较大。在这个更大的距离上管理[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)所获得的能量增益胜出。[表面能](@keyword=surface_energy|lang=zh-CN|style=Feynman)变为*负值*。这是一个惊人的结果！这意味着[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)实际上可以通过在正常区域和超导区域之间创建界面来*降低*其总能量。[@problem_id:3021315]

具有负[表面能](@keyword=surface_energy|lang=zh-CN|style=Feynman)的材料就是[第二类超导体](@keyword=type_ii_superconductors_2|lang=zh-CN|style=Feynman)。面对外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，它不只是顽固地抵抗，而是达成了一笔交易。它允许[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)进入，但方式非常特殊且高度受控。它创建了一个微小的正常态通道网络，让[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)得以通过，而材料的其余部分则愉快地保持超导状态。例如，一种[相干长度](@keyword=healing_length|lang=zh-CN|style=Feynman)为 $\xi(0) = 150 \text{ nm}$、穿透深度为 $\lambda(0) = 50 \text{ nm}$ 的材料，其 $\kappa = 1/3 < 1/\sqrt{2}$，使其成为[第一类超导体](@keyword=type_i_superconductor_2|lang=zh-CN|style=Feynman)。在中等[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)下，它会简单地排出所有磁通，表现出完美的迈斯纳态 [@problem_id:2978571]。但如果这两个长度反过来，它就会拥抱一种新的排布方式。这种经过精妙协商而形成的新状态被称为**混合态**。这些捕获[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的通道就是著名的**[阿布里科索夫涡旋](@keyword=abrikosov_vortices|lang=zh-CN|style=Feynman)**。

### 量子漩涡

那么，涡旋究竟*是*什么？它是凝聚态物理学中最优雅的结构之一。其核心是一个细长的核，半径约为[相干长度](@keyword=healing_length|lang=zh-CN|style=Feynman) $\xi$，在这里材料基本处于正常态。这就是磁力线穿过的通道。但这个正常核不仅仅是一个被动的管道，它是一场量子飓风的风眼。

在核的周围，一股[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)永恒地环绕着，就像一个微小的、无摩擦的漩涡。这个电流涡旋有两个作用。首先，它将[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)限制在核内，将其与周围的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)主体屏蔽开来。其次，更深刻的是，它是量子力学序参量 $\psi$ 中一个拓扑缺陷的物理表现。序参量是一个复数，$\psi = |\psi| e^{i\theta}$，当你绕着涡旋核走一整圈时，其相位 $\theta$ 必须改变 $2\pi$ 的整数倍。这是保证[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)[单值性](@keyword=monodromy|lang=zh-CN|style=Feynman)的一个基本要求，也是量子力学的基石。

这种相位缠绕带来一个惊人的结果：陷在涡旋核内的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)不能取任意值，它是**量子化**的。单个涡旋中的总磁通量总是**[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)** $\Phi_0 = h/(2e)$ 的整数倍，其中 $h$ 是普朗克常数，$e$ 是电子[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。对于最低能量态，每个涡旋恰好携带一个[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)。[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)并非像水流过管道那样流过[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)，而是被迫以离散的、相同的包裹形式进入。混合态是量子力学在宏观尺度上的微观体现。[@problem_id:2992391]

### 有序的人群：涡旋[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)

现在，当我们增加外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)时会发生什么？[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)必须容纳更多的磁通量，于是它让更多的涡旋进入。这些涡旋会像无序的气体一样四处漂移吗？不。记住每个涡旋都是一个环形电流，会产生[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。携带同向磁通的涡旋——它们都是如此——会相互排斥。

两个相距为 $r$ 的平行涡旋之间的相互作用能是一种排斥力，其作用范围的特征距离是[穿透深度](@keyword=penetration_depth|lang=zh-CN|style=Feynman) $\lambda$ [@problem_id:3002009]。更精确的计算表明，这个能量与 $K_0(r/\lambda)$ 成正比，其中 $K_0$ 是描述衰减排斥势的[修正贝塞尔函数](@keyword=modified_bessel_functions|lang=zh-CN|style=Feynman)。

面对这种相互排斥，一大群涡旋的最低能量排布方式是什么？它们会像任何有理智、保持社交距离的人群一样：形成一个规则的、周期性的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。这种由磁通线组成的、卓越的自组织[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)就是**[阿布里科索夫涡旋晶格](@keyword=abrikosov_vortex_lattice|lang=zh-CN|style=Feynman)**。

这个系统的美妙之处在于其可调性。材料内部的平均[磁感应强度](@keyword=magnetic_flux_density|lang=zh-CN|style=Feynman) $B$ 就是单位面积内的涡旋数 $n_v$ 乘以每个涡旋的磁通量：$B = n_v \Phi_0$。这个极其简单的关系式具有深远的影响。它意味着涡旋[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的密度与外加[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)成正比。通过转动磁体的旋钮，我们可以极其精确地控制这个[量子晶体](@keyword=quantum_crystals|lang=zh-CN|style=Feynman)的间距。对于自然界所偏爱的三角[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，相邻涡旋之间的距离 $a_v$ 由以下简单公式给出 [@problem_id:1215942] [@problem_id:3002009]：
$$
a_v = \left(\frac{2 \Phi_0}{B \sqrt{3}}\right)^{1/2}
$$
随着[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $B$ 的增加，涡旋被越挤越近。当 $B$ 接近**[上临界场](@keyword=upper_critical_field|lang=zh-CN|style=Feynman)** $H_{c2}$（超导性最终被破坏的场强）时，涡旋间的距离变得与[相干长度](@keyword=healing_length|lang=zh-CN|style=Feynman) $\xi$ 本身相当。此时，涡旋的正常核基本上重叠在一起，整个材料变为正常态 [@problem_id:3002009]。

### 几何问题：为何是三角形？

我们已经确定涡旋会形成[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)。但会是哪种[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)呢？方形网格看起来简单直观。六角形（或三角形）[排列](@keyword=permutation|lang=zh-CN|style=Feynman)是另一种密集堆积的明显选择。自然界是如何选择的呢？

这个由 Alexei Abrikosov 在其获得诺贝尔奖的工作中发现的答案，是[理论物理学](@keyword=theoretical_physics|lang=zh-CN|style=Feynman)的杰作。在接近[上临界场](@keyword=upper_critical_field|lang=zh-CN|style=Feynman) $H_{c2}$ 时，超导[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman) $\psi$ 很小。在此极限下，控制 $\psi$ 的[金兹堡-朗道方程](@keyword=ginzburg_landau_equation|lang=zh-CN|style=Feynman)得到简化，其在数学上变得与[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中带电粒子的薛定谔方程相同 [@problem_id:2992391]。此时 $\psi$ 的允许解就是著名的**朗道能级**。

为了使系统在尽可能高的场强下“开启”超导，它必须采取能量最低的状态，这对应于**[最低朗道能级](@keyword=lowest_landau_level|lang=zh-CN|style=Feynman) (LLL)**。LLL最奇怪的特征之一是其巨大的简并性：有大量的不同[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)都具有完全相同的能量。Abrikosov 的天才之处在于，他意识到可以利用这些简并态的线性组合来构建一个空间上周期性的[序参量](@keyword=order_parameter|lang=zh-CN|style=Feynman) $\psi$——也就是一个涡旋[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)！[@problem_id:3002041]

然而，这仍然没有告诉我们哪种[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)几何结构最好，因为在这种近似水平上，方形和三角[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)具有相同的能量。我们需要一个决胜因素。这个决胜因素来自我们最初忽略的 G-L 能量中的非线性 $|\psi|^4$ 项。为了使总[能量最小化](@keyword=energy_minimization|lang=zh-CN|style=Feynman)，系统必须选择能使 $|\psi|^2$ 的空间变化最小的晶格结构，从而保持超导密度尽可能均匀。这由**阿布里科索夫参数**来描述：
$$
\beta_A = \frac{\langle |\psi|^4 \rangle}{\langle |\psi|^2 \rangle^2}
$$
其中尖括号表示在[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的一个[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)上进[行空间](@keyword=row_space|lang=zh-CN|style=Feynman)平均。系统会自发地选择 $\beta_A$ 值最低的几何结构。精细的计算表明，对于方形[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，$\beta_A \approx 1.18$，而对于三角[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，$\beta_A \approx 1.16$ [@problem_id:3002041]。正是这种微小、微妙的能量差异，迫使涡旋海结晶成三角图案。这是一个绝佳的对称性破缺的例子，其中底层的各向同性物理定律产生了一个具有特定、有序几何结构的状态。

### 涡旋晶体的弹性生命

这个涡旋[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)不仅仅是一个漂亮的图案。它是一个物理实体，一种有其自身力学性能的物质。它可以被压缩、剪切和弯曲。实际上，它是一个[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中的弹性固体。

[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)抵抗均匀压缩的能力由其**体模量** $K$ 来描述。将涡旋挤压在一起会增加它们的相互排斥力，从而提高能量。这赋予了[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)抗压缩的刚度，可以直接从系统的[自由能计算](@keyword=free_energy_calculations|lang=zh-CN|style=Feynman)得出 [@problem_id:266475]。

更美妙的是，[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)抵抗剪切的能力——其**[剪切模量](@keyword=shear_modulus|lang=zh-CN|style=Feynman)** $C_{66}$——与它当初形成三角形状的原因直接相关！如果你试图剪切三角[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，你会使其变形，改变[晶格矢量](@keyword=lattice_vectors|lang=zh-CN|style=Feynman)之间的角度。这种畸变使[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)偏离了完美的三角几何结构，这不可避免地会增加阿布里科索夫参数 $\beta_A$ 的值。$\beta_A$ 的增加对应于系统自由能的增加。这个能量成本*就是*弹性剪切能。[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)会努力维持其能量最优的三角形状，从而赋予其抗剪切的刚性 [@problem_id:114945]。

随着我们增加[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)接近 $H_{c2}$，[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)在最终“熔化”成正常态之前开始“软化”。不同的弹性模量以不同的速率衰减。依赖于微妙的 $|\psi|^4$ 能量项的[剪切模量](@keyword=shear_modulus|lang=zh-CN|style=Feynman) $C_{66}$ 特别脆弱。它随着 $(1-B/H_{c2})^2$ 而消失。相比之下，磁通线本身抵抗弯曲的内在能力（**倾斜模量**）衰减得更慢，为 $(1-B/H_{c2})$。[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)对均匀压缩的抵抗力最为稳固，并一直保持有限值直到最后 [@problem_id:3002022]。这种复杂的行为揭示了[阿布里科索夫晶格](@keyword=abrikosov_lattice|lang=zh-CN|style=Feynman)不仅仅是一种单一的状态，而是通往一个丰富的“[涡旋物质](@keyword=vortex_matter|lang=zh-CN|style=Feynman)”世界的大门，这个世界拥有固态、液态甚至玻璃态等相，所有这些都由量子力学、拓扑学和[统计物理学](@keyword=statistical_physics|lang=zh-CN|style=Feynman)之间微妙的相互作用所支配。