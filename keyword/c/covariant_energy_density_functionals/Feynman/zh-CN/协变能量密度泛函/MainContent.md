## 引言
[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)是由质子和中子组成的致密系统，长期以来，物理学家一直在寻求一种统一的描述性理论来解释它，这是一个巨大的挑战。虽然非相对论模型已取得成功，但它们常常依赖于唯象的附加项，并且难以解释像核[自旋-轨道力](@keyword=spin_orbit_force|lang=zh-CN|style=Feynman)巨大强度这样的基本性质。协变[能量密度泛函](@keyword=energy_density_functional|lang=zh-CN|style=Feynman) (CEDFs) 提供了一个更深层次的解决方案，它基于[狭义相对论](@keyword=special_relativity_theory|lang=zh-CN|style=Feynman)的原理从头开始构建理论。这种方法将[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)视为在强大的、自生产生场中运动的[相对论性粒子](@keyword=relativistic_particle|lang=zh-CN|style=Feynman)，提供了一个框架，其中许多复杂的核性质是自然产生的，而不是人为引入的。

本文全面概述了CEDF框架。我们将首先深入探讨其核心的**原理与机制**，探索相对论[协变](@keyword=covariation|lang=zh-CN|style=Feynman)性如何塑造该理论，解释[自旋-轨道力](@keyword=spin_orbit_force|lang=zh-CN|style=Feynman)的起源，并通过对称性破缺融入配对和形变等关键的[多体效应](@keyword=many_body_effects|lang=zh-CN|style=Feynman)。随后，**应用与跨学科联系**部分将展示该理论的预测能力，说明一个单一、一致的框架如何能够描述整个核物理版图，从单个[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的性质到[中子星](@keyword=neutron_star|lang=zh-CN|style=Feynman)和[超新星](@keyword=supernovae|lang=zh-CN|style=Feynman)的极端环境。

## 原理与机制

要理解[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)，我们必须首先选择我们的语言。几十年来，物理学家将[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)描述为一堆小台球——质子和中子——通过被 painstakingly 编目和[参数化](@keyword=parametrization|lang=zh-CN|style=Feynman)的力相互作用。这种非相对论的图景，体现在像[Skyrme泛函](@keyword=skyrme_functional|lang=zh-CN|style=Feynman)这样的模型中，取得了显著的成功。然而，它留下了一些悬而未决的深层问题。为什么[自旋-轨道力](@keyword=spin_orbit_force|lang=zh-CN|style=Feynman)（它使[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)的自旋与其[轨道运动](@keyword=orbital_motion|lang=zh-CN|style=Feynman)对齐）在[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)中异常强大，而在原子中对电子却很微弱？为什么[富中子核](@keyword=neutron_rich_nuclei|lang=zh-CN|style=Feynman)的某些性质表现出它们特有的行为？

协变[能量密度泛函](@keyword=energy_density_functional|lang=zh-CN|style=Feynman)方法提供了一种不同且更深邃的语言。它始于一个大胆的前提：要真正理解[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)，我们必须将其构成部分——[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)——描述为完全受[狄拉克方程](@keyword=dirac_equation|lang=zh-CN|style=Feynman)支配的相对论粒子，而不仅仅是简单的台球。这并不是因为[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)以接近光速的速度运动——它们没有。而是因为束缚它们的力是如此巨大，以至于可以与[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)自身的[静止质量](@keyword=rest_mass|lang=zh-CN|style=Feynman)能量相媲美。在这种情况下，爱因斯坦相对论中所体现的时空基本对称性不仅仅是高能领域的好奇心；它们是故事的关键部分。

### 一个自束缚世界的相对论舞台

与原子中的电子在[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)提供的中心外部势中舞蹈不同，[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)*创造*了它们表演的舞台。[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)是一个**自束缚**系统。这对[密度泛函理论](@keyword=density_functional_theory|lang=zh-CN|style=Feynman) (DFT) 提出了一个挑战，因为其最初的公式——[Hohenberg-Kohn定理](@keyword=hohenberg_kohn_theorems|lang=zh-CN|style=Feynman)——依赖于一个外部势。解决方案非常优雅：我们为[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的*内禀*密度，即从其自身[质心](@keyword=centroid|lang=zh-CN|style=Feynman)看到的密度，重新构建了理论。这使我们能够定义一个普适的[能量泛函](@keyword=energy_functional|lang=zh-CN|style=Feynman)和相应的[Kohn-Sham方案](@keyword=kohn_sham_scheme|lang=zh-CN|style=Feynman)，为将DFT应用于没有外部锚点的系统提供了严格的基础 [@problem_id:3554404]。

在实践中，这意味着我们的平均场计算必须将[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)局域化，否则它会散布在整个空间中。这通常通过添加一个弱约束来完成，该约束将[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的[质心](@keyword=centroid|lang=zh-CN|style=Feynman)“钉”在原点。必须认识到，这是一种计算工具；基本理论仍然是平移不变的 [@problem_id:3554404]。

舞台已经搭好，那么我们[能量泛函](@keyword=energy_functional|lang=zh-CN|style=Feynman)的构建块是什么呢？由于我们的理论是相对论性的，能量密度必须是一个**[洛伦兹标量](@keyword=lorentz_scalar|lang=zh-CN|style=Feynman)**——它对所有惯性观察者来说必须看起来一样。这是一个强大的约束。它规定我们不能随意添加任何我们喜欢的项。构建块必须以非常特定的方式由[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)的狄拉克波函数 $\psi$ 构建。通过要求在[洛伦兹变换](@keyword=the_lorentz_transformation|lang=zh-CN|style=Feynman)、宇称（[镜像对称](@keyword=mirror_symmetry|lang=zh-CN|style=Feynman)）和时间反演下不变，一小组优雅的基本密度应运而生。这些是自然界对称性所允许的基本成分 [@problem_id:3554408]。其中最重要的包括：

-   **[标量密度](@keyword=scalar_density|lang=zh-CN|style=Feynman)** $\rho_S(\mathbf{r}) = \sum_i \bar{\psi}_i(\mathbf{r})\psi_i(\mathbf{r})$，这是一个真正的[洛伦兹标量](@keyword=lorentz_scalar|lang=zh-CN|style=Feynman)。
-   **重子[四维流](@keyword=four_current|lang=zh-CN|style=Feynman)** $j^\mu(\mathbf{r}) = \sum_i \bar{\psi}_i(\mathbf{r})\gamma^\mu\psi_i(\mathbf{r})$，它像一个[四维矢量](@keyword=4_vectors|lang=zh-CN|style=Feynman)一样变换。它的类时分量 $j^0$ 是我们熟悉的[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)[数密度](@keyword=number_density|lang=zh-CN|style=Feynman) $\rho_B(\mathbf{r}) = \sum_i \psi_i^\dagger(\mathbf{r})\psi_i(\mathbf{r})$。
-   **[张量密度](@keyword=tensor_density|lang=zh-CN|style=Feynman)**，它捕捉了更复杂的[自旋结构](@keyword=spin_structures|lang=zh-CN|style=Feynman)。

为了区分质子和中子，我们还引入了它们的**同位旋矢量**对应项，这些对应项对[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)的同位旋（即它是质子还是中子）敏感 [@problem_id:3554443]。对于静态的偶偶核，在平均场水平上，其他可能的[双线性](@keyword=bilinearity|lang=zh-CN|style=Feynman)项，如[赝标量](@keyword=pseudoscalar|lang=zh-CN|style=Feynman)和轴矢量密度，其[期望值](@keyword=expectation_values|lang=zh-CN|style=Feynman)为零，不直接产生贡献 [@problem_id:3554408]。理论本身告诉我们应该保留什么，丢弃什么。

### 自洽之舞

该框架的核心思想是一支优美的、自我调节的舞蹈。[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)通过它们的集体存在，产生了强大的平均场。这些场反过来又决定了[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)的行为方式。这是一个完美的反馈循环，一种**自洽**的状态。

想象一下[标量密度](@keyword=scalar_density|lang=zh-CN|style=Feynman) $\rho_S$ 作为强大吸引性**[标量场](@keyword=scalar_fields|lang=zh-CN|style=Feynman)** $S(\mathbf{r})$ 的源。同时，重子密度 $\rho_B$ 作为强大排斥性**矢量场** $V(\mathbf{r})$ 的源。因此，在[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)中运动的[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)沐浴在这两个相反的场中。它的运动不再由自由的狄拉克方程描述，而是由一个包含这些势的修正方程描述 [@problem_id:3554405]：

$$
\left[ \boldsymbol{\alpha}\cdot\mathbf{p} + \beta\left(m + S(\mathbf{r})\right) + V(\mathbf{r}) \right] \psi_i(\mathbf{r}) = \epsilon_i \psi_i(\mathbf{r})
$$

这是我们相对论核系统的[Kohn-Sham方程](@keyword=kohn–sham_equations|lang=zh-CN|style=Feynman)。注意这两个场的作用。矢量势 $V(\mathbf{r})$ 的作用就像[电势](@keyword=electric_potential|lang=zh-CN|style=Feynman)一样，改变了[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)的能量 $\epsilon_i$。然而，标量势 $S(\mathbf{r})$ 的作用更为深刻。它通过 $\beta$ 矩阵与质量项耦合。在[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)内部，[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)的行为就好像它有一个“有效质量” $m^* = m + S(\mathbf{r})$。由于标量场是强吸引的（$S$ 是大的负值），[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)的有效质量显著降低，约为其自由空间质量的 $0.6$ 到 $0.7$ 倍！这种相对论效应是该理论的基石。

整个这种结构是协变泛函与像Skyrme类型的非相对论泛函的区别所在。[Skyrme泛函](@keyword=skyrme_functional|lang=zh-CN|style=Feynman)是建立在尊重伽利略[不变性](@keyword=invariance|lang=zh-CN|style=Feynman)而非[洛伦兹不变性](@keyword=lorentz_invariance|lang=zh-CN|style=Feynman)的密度之上的，其方程是类薛定谔的 [@problem_id:3554399]。

### 自然之美：[自旋-轨道力](@keyword=spin_orbit_force|lang=zh-CN|style=Feynman)

在这里，我们见证了[协变](@keyword=covariation|lang=zh-CN|style=Feynman)方法最令人惊叹的胜利之一。几十年来，[自旋-轨道相互作用](@keyword=spin_orbit_interaction|lang=zh-CN|style=Feynman)——解释[核物理](@keyword=nuclear_physics|lang=zh-CN|style=Feynman)“幻数”的关键因素——必须通过人为的方式添加到非相对论模型中，其强度是唯象地固定的。它是一个已知的特征，但其起源却很模糊。

在相对论框架中，[自旋-轨道力](@keyword=spin_orbit_force|lang=zh-CN|style=Feynman)是*自动*产生的，是强[标量场](@keyword=scalar_fields|lang=zh-CN|style=Feynman)和矢量场存在下狄拉克方程的直接且不可避免的后果。通过对上述[狄拉克方程](@keyword=dirac_equation|lang=zh-CN|style=Feynman)进行仔细的非相对论简化，一个新项出现在有效的薛定谔方程中。该项的形式恰好是自旋-[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)势的形式，其强度与矢量场和[标量场](@keyword=scalar_fields|lang=zh-CN|style=Feynman)之*差*的梯度成正比：

$$
U_{\mathrm{SO}} \propto \frac{1}{r} \frac{d}{dr} \left( V(\mathbf{r}) - S(\mathbf{r}) \right)
$$

在[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)内部，$V$ 是大的[排斥势](@keyword=repulsive_potential|lang=zh-CN|style=Feynman)（数百 MeV），而 $S$ 是大的吸引势（数百 MeV）。它们的差值是巨大的，自然地解释了观测到的核[自旋-轨道力](@keyword=spin_orbit_force|lang=zh-CN|style=Feynman)的强度。它不是人为加入的，而是自然得出的。这种深刻的联系有力地证明了相对论描述的正确性。此外，它还提供了预测能力。通过理解矢量势的[同位旋](@keyword=isotopic_spin|lang=zh-CN|style=Feynman)矢量部分在[富中子核](@keyword=neutron_rich_nuclei|lang=zh-CN|style=Feynman)中的演化，我们可以预测当中子[自旋-轨道分裂](@keyword=spin_orbit_splitting|lang=zh-CN|style=Feynman)随着我们接近[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)存在的极限时如何变化，以及这种演化如何与诸如**[对称能](@keyword=symmetry_energy|lang=zh-CN|style=Feynman)斜率** $L$ [@problem_id:3554432] 等体性质联系起来。

### 精雕细琢：现代泛函与破缺对称性

[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)通过介子交换相互作用的简单图景仅仅是个开始。现代的高精度泛函承认，相互作用本身会受到周围核介质的修正。耦合强度不再是常数，而是依赖于局域[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)密度。这引入了一个奇妙而微妙的[多体效应](@keyword=many_body_effects|lang=zh-CN|style=Feynman)：**[重排能](@keyword=rearrangement_energy|lang=zh-CN|style=Feynman)**。当向系统中添加一个[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)时，你不仅添加了它自身的能量，还轻微地改变了密度，这反过来又改变了*所有*其他[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)的相互作用能。这种反馈，或称重排项，对于[核物质](@keyword=nuclear_matter|lang=zh-CN|style=Feynman)和有限核的[热力学一致性](@keyword=thermodynamic_consistency|lang=zh-CN|style=Feynman)描述至关重要 [@problem_id:3555154]。

那么，作为任何相对论理论基础的负能态之海——[狄拉克海](@keyword=hole_theory|lang=zh-CN|style=Feynman)——又该如何处理呢？对其贡献的幼稚计算会导致必须[重整化](@keyword=renormalization|lang=zh-CN|style=Feynman)的无限能量。实际的CEDF计算采用**无海近似**，其中[真空极化](@keyword=vacuum_polarization|lang=zh-CN|style=Feynman)的效应不被显式计算。相反，它们被隐式地吸收到泛函的耦合参数中，这些参数是通过拟合实验数据得到的。这是一个理论上合理的程序，其合理性由[有效场论](@keyword=effective_field_theory|lang=zh-CN|style=Feynman)的原理所证明：真空的短程效应可以被编码到有效理论的局域[相互作用项](@keyword=interaction_terms|lang=zh-CN|style=Feynman)中。这种近似对于描述核结构是稳健的，但在超越平均场近似或进入极端密度时需要仔细重新审视 [@problem_id:3554467]。

最后，[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)不仅仅是独立粒子的静态集合。它表现出丰富的集体行为，如转动和超流性。这些现象在DFT中通过**[自发对称性破缺](@keyword=spontaneous_symmetry_breaking|lang=zh-CN|style=Feynman)**的概念得到了优雅的描述。

-   **形变：** 虽然底层的泛函是球对称的，但对于大多数[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)来说，能量最低的解并非如此。平均场呈现出形变的形状（像一个足球或一个铁饼），自发地打破了转动对称性。
-   **配对：** 在[开壳层原子核](@keyword=open_shell_nuclei|lang=zh-CN|style=Feynman)中，[核子](@keyword=nucleon|lang=zh-CN|style=Feynman)形成相关的“库珀对”，这是一种类似于金属中超导的现象。为了描述这一点，我们使用**相对论Hartree-Bogoliubov (RHB)** 框架，其中[基态](@keyword=ground_state|lang=zh-CN|style=Feynman)是不同[粒子数态](@keyword=number_states|lang=zh-CN|style=Feynman)的叠加。这打破了与粒子数守恒相关的全局对称性 [@problem_id:3554463]。这样一个系统的基本激发不再是粒子和空穴，而是**[准粒子](@keyword=quasiparticle|lang=zh-CN|style=Feynman)**，它们是两者的混合。RHB方程提供了对平均场和配对场的统一描述 [@problem_id:3554463]。

这些破缺的对称性并非理论的缺陷。它们正是理论用来描述[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)涌现的、集体的生命的语言。通过允许这些基本定律的对称性被解所打破，我们得以接触到[核多体问题](@keyword=nuclear_many_body_problem|lang=zh-CN|style=Feynman)丰富而复杂的现实。为了与测量具有良[好量子数](@keyword=good_quantum_numbers|lang=zh-CN|style=Feynman)态的实验数据进行比较，这些对称性可以通过强大的群论**投影技术**来恢复 [@problem_id:3554459]。这个两步过程——打破对称性以捕捉本质物理，然后恢复它以与观测联系起来——是协变[能量密度泛函](@keyword=energy_density_functional|lang=zh-CN|style=Feynman)现代应用的核心。

