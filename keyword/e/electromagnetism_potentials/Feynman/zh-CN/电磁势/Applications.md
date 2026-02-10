## 应用与跨学科联系

在我们之前的讨论中，我们介绍了[电磁势](@keyword=electromagnetic_potentials|lang=zh-CN|style=Feynman)$\phi$和$\vec{A}$，以及奇特的[规范不变性](@keyword=gauge_invariance|lang=zh-CN|style=Feynman)原理。我们看到，虽然势决定了[电场和磁场](@keyword=electric_and_magnetic_fields|lang=zh-CN|style=Feynman)，但它们本身并不是唯一的；我们可以用某些方式变换它们而不改变任何物理场。这可能会让你留下一个挥之不去的问题：如果势只是一种数学技巧，一种我们可以随意改变的计算脚手架，为什么它们在现代物理学中如此核心？

答案是，它们远不止是一种技巧。它们代表了关于相互作用本质的深刻真理。物理定律不应依赖于我们局域的观点——即局域的“规范”——这一原理，最终被证明正是像[电磁力](@keyword=electromagnetic_forces|lang=zh-CN|style=Feynman)这样的力*必须存在*的原因。这种思想，即要求一种局域对称性就必须引入一个“补偿”或“联络”场，或许是二十世纪物理学最深刻的洞见之一[@problem_id:1872250]。势就是这个联络场。

在本章中，我们将踏上一段旅程，见证这一思想所带来的惊人后果。我们将看到势如何从经典力学中的一种便利，演变为量子世界中的物理实在，它们如何在外来材料中协调数百万电子的集体行为，以及它们如何构成我们用以描述时空结构本身的语言。

### [经典动力学](@keyword=classical_dynamics|lang=zh-CN|style=Feynman)的新语言

早在其量子重要性被理解之前，势就在 Lagrange 和 Hamilton 对经典力学的优雅重构中证明了其价值。我们可以用单一的标量——拉格朗日量 $L$ 或哈密顿量 $H$——来描述一个系统的整个动力学，而无需与力作斗争。在这种语言中，势不是事后的补充，而是一个基本的组成部分。

包含[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)的规则非常简单，这个方法被称为“[最小耦合](@keyword=minimal_coupling|lang=zh-CN|style=Feynman)”。要找到[带电粒子的哈密顿量](@keyword=hamiltonian_for_a_charged_particle|lang=zh-CN|style=Feynman)，你只需取自由粒子的哈密顿量$\frac{\vec{p}^2}{2m}$，然后简单地将动量$\vec{p}$替换为组合$\vec{p} - q\vec{A}$，并加上势能$q\phi$。例如，如果你想描述一个与光波相互作用的带电粒子，比如一个被激光晃动的电子，这正是你的起点。光波由其势来描述，而哈密顿量则成为它们相互作用上演的舞台[@problem_id:2045060]。

$$H = \frac{1}{2m}(\vec{p}-q\vec{A})^{2} + q\phi$$

这种形式体系揭示了隐藏的真理。考虑一个带电粒子处于一个均匀[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)随时间缓慢增加的区域，$B(t) = B_0 t$。这样的场可以由矢量势$\vec{A} = \frac{1}{2}B_0 t (-y, x, 0)$来描述。这里发生了一件有趣的事情。机械角动量 $m(x\dot{y} - y\dot{x})$ *不*守恒。一个增强的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)会产生一个环形电场，使粒子加速或减速。然而，[拉格朗日形式体系](@keyword=lagrangian_formalism|lang=zh-CN|style=Feynman)告诉我们，另一个量*是*守恒的：正则角动量 $p_\theta$。这个量是熟悉的机械角动量和一个涉及矢量势本身的项的组合[@problem_id:2086349]。势重新定义了我们所说的[守恒量](@keyword=conserved_quantity|lang=zh-CN|style=Feynman)，为我们提供了一个更基本的视角，即使在场发生变化时也成立。

### 量子世界的裁决：势是真实的

在经典力学中，人们仍然可以争辩说，势只是一个聪明的记账工具。量子革命粉碎了这种观点。决定性的一击来自一个非凡的思想实验，后来在实验室得到证实，即[阿哈罗诺夫-玻姆效应](@keyword=aharonov_bohm_effect|lang=zh-CN|style=Feynman)。

想象一个无限长的细[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)——一个线圈。电流流过它，在[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)*内部*产生强[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，但在其*外部*绝对没有[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。现在，假设我们发射电子，让它们的路径从螺线管的两侧通过，但从不穿过它。由于电子只在[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)为零的区域行进，它们受到的经典洛伦兹力为零。你会[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)对它们的运动没有任何影响。

但量子力学有不同看法。虽然[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)$\vec{B}$在[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)外部为零，但矢量势$\vec{A}$不为零。它围绕任何包围[螺线管](@keyword=solenoid|lang=zh-CN|style=Feynman)的闭合回路的线积分等于内部的磁通量$\Phi$。一个由[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)描述的量子粒子对其[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的相位很敏感。当电子从A点行进到B点时，它的相位会改变，其中一部分变化是由于其路径上的矢量势引起的。

当来自两条路径的电子波重新汇合干涉时，它们最终的[相位差](@keyword=phase_difference|lang=zh-CN|style=Feynman)包含一个取决于它们所包围磁通量的项，即使它们从未接触过[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)！这个[阿哈罗诺夫-玻姆相](@keyword=aharonov_bohm_phase|lang=zh-CN|style=Feynman)移是一个纯粹的量子力学效应，由下式给出：

$$ \Delta\varphi = \frac{q}{\hbar} \oint \vec{A} \cdot d\vec{l} = \frac{q\Phi}{\hbar} $$

这是一个惊人的结果[@problem_id:2466075] [@problem_id:1517351]。它证明了带电粒子可以被一个在相应[力场](@keyword=force_field|lang=zh-CN|style=Feynman)不存在的区域中的势所影响。势不仅仅是一种数学上的便利；它们具有直接、可观测的物理后果。它们和场本身一样真实。

这个效应也为我们提供了一种新的、更深刻的方式来思考势。在数学中，[微分几何](@keyword=differential_geometry|lang=zh-CN|style=Feynman)领域谈到“联络”。联络是一个规则，告诉你如何沿着一条路径“[平行输运](@keyword=vector_transport_on_curved_space|lang=zh-CN|style=Feynman)”一个矢量或其他几何对象。矢量势$\vec{A}$正是[波函数相位](@keyword=wavefunction_phase|lang=zh-CN|style=Feynman)的这样一种联络。它告诉电子的相位如何从一点演化到下一点。围绕一个闭合回路获得的[阿哈罗诺夫-玻姆相](@keyword=aharonov_bohm_phase|lang=zh-CN|style=Feynman)位是这种联络的“[和乐](@keyword=holonomy|lang=zh-CN|style=Feynman)性”——从[波函数相位](@keyword=wavefunction_phase|lang=zh-CN|style=Feynman)的角度看，衡量空间“弯曲”程度的量度[@problem_id:1517351]。

这也阐明了规范不变性的作用。如果我们进行一次[规范变换](@keyword=gauge_transformations|lang=zh-CN|style=Feynman)，[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)本身会获得一个局域的相位因子[@problem_id:2103413]。任何单一点的相位本身没有物理意义。但是，干涉实验中两条路径之间的相位*差*是规范不变的，因此是物理上可观测的。

### 物质的集体之舞

势作为支配相位的联络这一概念，不仅仅是针对单个粒子的深奥概念。它是理解材料中一些最壮观的集体现象的关键，在这些现象中，数以万亿计的电子以完美的协同方式行动。

#### 超导性

在[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)中，电子形成配对（库珀对）并凝聚成一个单一的、宏观的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)，由一个复数序参量$\psi(\mathbf{r})$描述，这可以被认为是“整个材料的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)”[@problem_id:2826158]。超导性的一个关键特征是迈斯纳效应：[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)被完全排出[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)内部。这是如何发生的？答案在于一个巧妙的规范选择。

[库珀对](@keyword=cooper_pairs|lang=zh-CN|style=Feynman)的超流$\mathbf{J}_s$和矢量势$\mathbf{A}$之间的关系通常是复杂的。然而，我们可以利用我们的规范自由度来极大地简化它。通过选择所谓的伦敦规范，其中$\nabla \cdot \mathbf{A} = 0$，这种关系变得惊人地简单：超流就直接正比于矢量势！

$$ \mathbf{J}_s = -\frac{n_s (2e)^2}{m^*} \mathbf{A} $$

将这个简单的本构关系与[麦克斯韦方程组](@keyword=maxwell_s_equations|lang=zh-CN|style=Feynman)结合，立即表明任何[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)只能穿透到[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)内部一个很小的距离（[伦敦穿透深度](@keyword=london_penetration_depth|lang=zh-CN|style=Feynman)）就会衰减到零。令人费解的迈斯纳效应从一个由势形式体系和一个明智的规范选择所实现的简单描述中自然而然地涌现出来[@problem_id:1818570]。

#### “动量空间”[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)

[规范理论](@keyword=gauge_theory|lang=zh-CN|style=Feynman)的数学结构是如此强大和基础，以至于它在完全不同的背景下重现。其中最美的例子之一是在[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)内电子的运动中。

晶体中电子的状态由其[布洛赫波函数](@keyword=bloch_wave_function|lang=zh-CN|style=Feynman)描述，这取决于它的动量$\vec{k}$。事实证明，这个[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)在*动量空间*中的几何特性创造了一个与[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)完美类比的结构。存在一个“[贝里联络](@keyword=berry_connection|lang=zh-CN|style=Feynman)”$\mathcal{A}_n(\vec{k})$，其作用就像一个矢量势，还有一个“[贝里曲率](@keyword=berry_curvature|lang=zh-CN|style=Feynman)”$\Omega_n(\vec{k})$，其作用就像一个[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)。

这不仅仅是一个形式上的类比。这个动量空间的“[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)”会产生一个真实的力。电子的速度被一个看起来就像洛伦兹力的额外项所修正，称为[反常速度](@keyword=anomalous_velocity|lang=zh-CN|style=Feynman)：$\dot{\vec{r}}_{\text{anomalous}} \propto \dot{\vec{k}} \times \Omega_n(\vec{k})$。这个项是造成现实世界现象的原因，比如[反常霍尔效应](@keyword=anomalous_hall_effect|lang=zh-CN|style=Feynman)，即即使没有外部[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，电压也会出现在垂直于电流的方向上[@problem_id:1809525]。就好像电子正在穿过一个[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)，但这个“场”是由晶体[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的[量子几何](@keyword=quantum_geometry|lang=zh-CN|style=Feynman)编织而成的。

### [时空](@keyword=space_time|lang=zh-CN|style=Feynman)的结构与[力的统一](@keyword=unification_of_forces|lang=zh-CN|style=Feynman)

我们来到了最宏大的舞台：宇宙本身。[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)中的[规范不变性](@keyword=gauge_invariance|lang=zh-CN|style=Feynman)与爱因斯坦广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中的[广义协变性原理](@keyword=principle_of_general_covariance|lang=zh-CN|style=Feynman)之间的深刻类比，揭示了势最深层的作用。

让我们回顾一下这个逻辑[@problem_id:1872250]：
1. 在[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)中，我们要求我们的物理定律在带电粒子[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)的*局域*相位旋转下保持不变。
2. 为了实现这一点，我们被迫引入一个“联络”场——[电磁势](@keyword=electromagnetic_potentials|lang=zh-CN|style=Feynman)$A_\mu$——来补偿局域变换。这个场是[电磁力](@keyword=electromagnetic_forces|lang=zh-CN|style=Feynman)的媒介。

现在，考虑引力：
1. 在广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中，我们要求我们的物理定律在我们的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)的*局域*改变下保持不变。我们希望物理定律无论我们如何标记[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中的点都是相同的。
2. 为了实现这一点，我们被迫引入一个“联络”场——从度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman)$g_{\mu\nu}$导出的克里斯托费尔联络——它告诉我们如何在[弯曲时空](@keyword=curved_spacetime|lang=zh-CN|style=Feynman)中比较不同点的矢量和[张量](@keyword=tensor|lang=zh-CN|style=Feynman)。这个场是引力的媒介。

模式是完全相同的。**局域对称性要求一个[规范场](@keyword=gauge_fields|lang=zh-CN|style=Feynman)。** 势是局域对称性的语言。它们不仅仅是理论的附加物；它们是其最基本原理的必然结果。

这种统一的几何观点使我们能够写下无缝融合[电磁学](@keyword=electricity_and_magnetism|lang=zh-CN|style=Feynman)和引力的方程。例如，一个在弯曲的、无源[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中传播的电磁波的方程，直接将矢量势$A_a$与[时空](@keyword=space_time|lang=zh-CN|style=Feynman)本身的曲率（由里奇张量$R_{ac}$表示）耦合起来[@problem_id:1032450]。

$$ \nabla_b \nabla^b A_a - R_{ac} A^c = 0 $$

看着这个方程，你可以看到整个故事。势$A_a$不仅仅是存在*于*[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中；它的动力学与[时空](@keyword=space_time|lang=zh-CN|style=Feynman)自身的几何结构交织在一起。从一个简单的计算工具，[电磁势](@keyword=electromagnetic_potentials|lang=zh-CN|style=Feynman)被提升为我们描述宇宙的一个基本组成部分，这证明了在我们的物理定律中寻求更深层次对称性的力量和美丽。