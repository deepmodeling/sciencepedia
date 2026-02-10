## 引言
虽然我们体验到的大多数物理属性（如体积或速度）是连续的，但量子世界通常遵循一套不同的规则，倾向于离散、不可分割的“包”。其中一个最令人惊叹的例子就是[磁通量子化](@keyword=flux_quantization|lang=zh-CN|style=Feynman)——在这种现象中，穿过[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)只能以某个[基本单位](@keyword=fundamental_units|lang=zh-CN|style=Feynman)的整数倍存在。这种效应将量子力学奇特的颗粒性带到了我们可以直接测量和利用的尺度，弥合了微观世界与宏观世界之间的鸿沟。但是，像磁力这样的经典力，为何以及如何会遵循如此严格的量子定律呢？

本文将揭开磁通量子的奥秘。首先，在“原理与机制”一章中，我们将探讨这一现象的理论基础，深入研究电子库珀对的作用以及[量子力学波函数](@keyword=quantum_mechanics_wavefunctions|lang=zh-CN|style=Feynman)，后者的完整性要求磁通必须量子化。我们将看到这一原理如何通过观测得到直接验证。随后，“应用与跨学科联系”一章将揭示这个看似抽象的概念如何成为[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)传感器等强大技术背后的引擎，并为物理学家研究先进材料的性质、统一量子物理学的不同领域提供了深刻的视角。

## 原理与机制

想象一下你有一个水桶，正在往里装水。你可以加入一升、一毫升，甚至一滴水。水的量似乎可以无限分割；它是一个连续量。在几乎整个历史上，我们都以同样的方式看待物理属性。但量子世界有一个有趣的习惯，就是把我们的连续[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)变成离散的、颗粒状的现实。事实证明，对于一类特殊的材料——[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)——[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)的行为不像水，而更像沙子。它只能以离散、不可分割的“包”存在。这就是**[磁通量子化](@keyword=flux_quantization|lang=zh-CN|style=Feynman)**现象，是量子力学在宏观尺度上的一次惊人而直接的展示。

### 经典世界中的量子规则

让我们为这场量子戏剧布置舞台。我们的舞台是一个简单的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)，一个由在冷却到临界温度以下时电阻为零的材料制成的[圆环](@keyword=annulus|lang=zh-CN|style=Feynman)。在这种状态下，会发生一件非凡的事情。通常各自奔波的电子决定配对。这些被称为**库珀对**的电子对是我们故事中的主角。一个[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)是两个电子组成的松散束缚对，这意味着它的总[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)不是我们熟悉的元[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $-e$，而是其两倍，即 $q = -2e$。这个看似微小的细节却有着深远的影响。

现在，如果我们试图让一个[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)穿过我们超导[圆环](@keyword=annulus|lang=zh-CN|style=Feynman)的孔，我们会发现我们不能随心所欲地施加任意大小的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)。磁通量，即穿过孔洞的磁感线的总和，是受限制的。它必须是一个基本磁通包——**[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)**（记为 $\Phi_0$）的整数倍。这个规则简单而绝对：

$$ \Phi = n \Phi_0 \quad (n = 0, 1, 2, \ldots) $$

这不是一个建议；这是[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)必须遵守的自然法则。这个基本包的值由自然界最重要的两个常数决定：量子理论的基石——普朗克常数 $h$，以及我们[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $2e$。磁通量子的表达式为：

$$ \Phi_0 = \frac{h}{2e} $$

将已知的 $h$ 和 $e$ 的值代入，我们便能得到这个磁性量子的具体数值 [@problem_id:1778084]。这是一个极其微小的量：大约为 $2.068 \times 10^{-15}$ 韦伯。为了对此有一个直观的感受，考虑一个半径仅为5微米的微观环。要捕获单个磁通量子，你只需要施加大约 $26.3$ 微特斯拉的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) [@problem_id:1781836]。这是一个很弱的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，大约是指南针所依赖的地球[磁场强度](@keyword=magnetic_field_intensity|lang=zh-CN|style=Feynman)的一半。因此，尽管量子本身很微小，但其效应完全在我们的测量和控制能力范围之内。

### 必须首尾相接的波

但是，*为什么*呢？为什么磁通必须量子化？答案在于物质的波动性，这是量子力学的基本原理。在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，数以亿计的库珀对并不像一群混乱的乌合之众。相反，它们凝聚成一个单一、统一的状态，表现得像一个巨大的实体。这种集体行为由一个单一的**[宏观波函数](@keyword=macroscopic_wavefunction|lang=zh-CN|style=Feynman)**描述，通常写作 $\Psi(\mathbf{r}) = \sqrt{\rho_s} \exp(i\theta(\mathbf{r}))$，其中 $\rho_s$ 代表[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的密度，$\theta(\mathbf{r})$ 是它们的集体量子相位。

现在，想象一个沿着圆形吉他弦传播的波。为了使波稳定且不发生相消干涉，它在绕行一整圈后必须完美平滑地连接回其起点。它可以有一个、两个或任意整数个波长正好容纳在圆周内。但它不能有，比如说，2.5个波长，因为这样一来波的终点将无法与起点匹配，从而产生一个“扭结”。

超导[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的相位 $\theta$ 必须遵守同样的规则。当我们沿着环内材料绕孔洞一周并回到起点时，[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)必须恢复其原始值。这被称为**[单值性](@keyword=monodromy|lang=zh-CN|style=Feynman)条件**。要实现这一点，其相位的总变化量只能是 $2\pi$ 的整数倍 [@problem_id:1785396] [@problem_id:1235055]。

$$ \oint d\theta = 2\pi n $$

关键的联系在于：[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)会改变带电粒子[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的相位。这种联系是通过一个称为**磁[矢势](@keyword=vector_potential|lang=zh-CN|style=Feynman)** $\mathbf{A}$ 的概念建立的，这是一个更深层次的场，[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman) $\mathbf{B}$ 由它导出。在没有电流的[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)内部，[波函数相位](@keyword=wavefunction_phase|lang=zh-CN|style=Feynman)的变化与这个[矢势](@keyword=vector_potential|lang=zh-CN|style=Feynman)成正比。因此，环路累积的总相位变化与环路内捕获的总[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi$ 成正比。

当我们结合这两个事实——总相位变化必须是 $2\pi$ 的整数倍，且该相位变化由磁通量决定——我们便得出一个非凡的结论。[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman) $\Phi$ 不能再取任意值。它被限制在那些能让[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)完美“首尾相接”的值上。这一约束在数学上直接导出了量子化规则：$\Phi = n \frac{h}{q}$。由于我们的载流子是[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为 $q=2e$ 的[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)，我们精确地得到 $\Phi = n \frac{h}{2e}$ [@problem_id:1085731]。电子配对不仅仅是一个偶然特征；它从根本上决定了[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)的大小。

### 观测量子：[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)与涡旋[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)

这一切似乎是美妙的理论物理，但我们如何知道它是真的呢？我们真的能“看到”这些量子吗？答案是肯定的，通过一些有史以来最精巧的设备。

完成这项任务的首选工具是**SQUID**，即[超导量子干涉仪](@keyword=superconducting_quantum_interference_devices|lang=zh-CN|style=Feynman)。其核心是一个（或两个）连接到一些电子设备的[超导环](@keyword=superconducting_ring|lang=zh-CN|style=Feynman)。它被设计成一个极其灵敏的磁力计。其工作原理是[磁通量子化](@keyword=flux_quantization|lang=zh-CN|style=Feynman)的直接结果。当穿过其环路的[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)增加时，SQUID两端的电压会上下[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。每一次完整的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，即输出信号中的每一次“摆动”，都对应着[磁通量](@keyword=magnetic_flux|lang=zh-CN|style=Feynman)变化了*恰好一个*[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman) $\Phi_0$。

想象一个实验：一位物理学家小心地增加穿过一个环路面积为 $1.00 \text{ mm}^2$ 的SQUID的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。他们观察到，当[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)仅增加103.5纳特斯拉时，电压输出恰好完成了50次完整的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。根据这些数据，他们可以通过简单的计算，实验性地确定磁通量子的值。结果与理论值 $h/(2e)$ 惊人地精确吻合 [@problem_id:1806334]。[SQUID](@keyword=squid|lang=zh-CN|style=Feynman)本质上是一个用于计算[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)的设备，为量子化本身以及库珀对的 $2e$ [电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)提供了无可辩驳的证据。

当我们从单个环转向一大片**[第二类超导体](@keyword=type_ii_superconductors_2|lang=zh-CN|style=Feynman)**时，故事变得更加直观。与它们的第一类“表亲”不同（[第一类超导体](@keyword=type_i_superconductor_2|lang=zh-CN|style=Feynman)会完全排斥[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)直到某一[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)），[第二类超导体](@keyword=type_ii_superconductors_2|lang=zh-CN|style=Feynman)有一个迷人的[中间相](@keyword=intermediate_phases|lang=zh-CN|style=Feynman)。当外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)足够强时，它们允许[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)穿透，但只能以一种高度结构化、量子化的方式。[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)以微小的圆柱形磁通丝组成的密集阵列穿透材料，这些磁通丝被称为**[阿布里科索夫涡旋](@keyword=abrikosov_vortices|lang=zh-CN|style=Feynman)**。

这些涡旋中的每一个都是一个微观的量子漩涡。在它的核心，超[导电性](@keyword=electrical_conductivity|lang=zh-CN|style=Feynman)被局部破坏，但围绕这个核心的是一股环绕的[超电流](@keyword=supercurrent|lang=zh-CN|style=Feynman)，将磁感线限制在其中。而最美妙的部分是什么？每一个涡旋都携带*恰好一个量子*的磁通量，即 $\Phi_0$。

你在材料内部测得的平均[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)就是这些涡旋的密度——单位面积的涡旋数量——乘以 $\Phi_0$ [@problem_id:1775644]。对于一个0.85特斯拉的相当大的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，你会发现在每平方米内竟挤满了 $4.11 \times 10^{14}$ 个涡旋！这些涡旋会自行[排列](@keyword=permutation|lang=zh-CN|style=Feynman)成规则的三角形或正方形[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)，形成一个“涡旋晶体”，其间距取决于[磁场强度](@keyword=magnetic_field_intensity|lang=zh-CN|style=Feynman) [@problem_id:1828352]。在这种状态下，磁性的量子本质不再被隐藏；它以一种惊人的、周期性的图案在整个材料中显露无遗。

### 两种量子的故事

那么，$\Phi_0 = h/(2e)$ 这个值是像光速一样的普适自然常数吗？答案是否定的，其原因极具启发性。磁通量子不是普适的，因为量子凝聚体的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)不是普适的。

让我们来做一个思想实验。假设我们发现了一种奇特的新型[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)，其中的载流子不是[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)，而是某种[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为 $qe$ 的其他[玻色子](@keyword=boson|lang=zh-CN|style=Feynman) [@problem_id:1778112]。如果我们回溯我们的推导，我们会发现[单值性](@keyword=monodromy|lang=zh-CN|style=Feynman)条件现在将导出一个大小为 $\Phi_b = h/(qe)$ 的磁通量子。量子的大小与载流子的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)成反比。这不仅仅是一个理论游戏；它突显了其中起作用的基本原理。

这个想法在一个完全不同但相关的量子现象中得以体现：**[量子霍尔效应](@keyword=quantum_hall_effect|lang=zh-CN|style=Feynman)**。这种效应发生在置于强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)和极低温度下的二维电子片中。在这里，载流子是单个电子，[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为 $e$。其物理过程导致了量子化的性质，在这个背景下也出现了一个自然的磁通单位。但由于载流子是单个电子，相关的[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)是：

$$ \Phi_{QHE} = \frac{h}{e} $$

这个与单个电子相关的[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)，恰好是与[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)相关的超导[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)的*两倍大* [@problem_id:1820493]。这是大自然最优雅的体现。我们有两个截然不同、蔚为壮观的[宏观量子现象](@keyword=macroscopic_quantum_phenomena|lang=zh-CN|style=Feynman)。两者都受制于相同的[量子力学基](@keyword=quantum_mechanics_basis|lang=zh-CN|style=Feynman)本规则和相同的[基本常数](@keyword=fundamental_constants|lang=zh-CN|style=Feynman) $h$ 和 $e$。然而，因为一个涉及电子对，另一个涉及单个电子，它们表现出两种不同的“基本”[磁通量子](@keyword=magnetic_flux_quantum|lang=zh-CN|style=Feynman)。这是一个美妙的证明，说明在物理学中，理解原理就是一切；具体的答案源于将这些原理应用于舞台上独特的“演员”。