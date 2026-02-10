## 引言
[密度泛函理论](@keyword=density_functional_theory_2|lang=zh-CN|style=Feynman)（DFT）是现代[计算科学](@keyword=computational_science|lang=zh-CN|style=Feynman)的支柱，它使我们能够根据[量子力学](@keyword=quantum_mechanics|lang=zh-CN|style=Feynman)的基本定律预测分子和材料的性质。其成功在于将无数[电子](@keyword=electrons|lang=zh-CN|style=Feynman)之间复杂的相互作用简化为单一的量：[电子密度](@keyword=electron_density|lang=zh-CN|style=Feynman)。然而，尽管功能强大，标准的 DFT 近似却存在一个关键盲点。它们本质上是“[近视](@keyword=myopia|lang=zh-CN|style=Feynman)”的，无法“看到”被称为[范德华力](@keyword=van_der_waals_forces|lang=zh-CN|style=Feynman)的微弱、长程吸引作用。这一疏漏使得它们无法描述从气体[冷凝](@keyword=condensation|lang=zh-CN|style=Feynman)到 DNA [结构完整性](@keyword=structural_integrity|lang=zh-CN|style=Feynman)等广泛现象。本文旨在解决[计算理论](@keyword=theory_of_computation|lang=zh-CN|style=Feynman)中的这一根本性空白。

以下章节将[引导](@keyword=bootstrapping|lang=zh-CN|style=Feynman)您了解这个引人入胜的问题及其解决方案。首先，在“原理与机制”部分，我们将深入探讨[范德华力](@keyword=van_der_waals_forces|lang=zh-CN|style=Feynman)的量子起源，精确解释为何局域 DFT 会失效，并介绍为解决此问题而发展的两个主要理论框架：实用的经验性校正和严谨的[非局域泛函](@keyword=nonlocal_functionals|lang=zh-CN|style=Feynman)。随后，在“应用与跨学科联系”部分，我们将探讨这些校正的深远影响，展示精确模拟这种“弱”相互作用对于设计新材料、理解生物过程以及将[量子理论](@keyword=quantum_theory|lang=zh-CN|style=Feynman)与真实世界实验联系起来是何等重要。

## 原理与机制

想象一下，您正试图描述两个身处独立[隔音](@keyword=noise_isolation|lang=zh-CN|style=Feynman)房间里的人的行为。您可以完美地测量每个房间内发生的一切——他们的动作、[心率](@keyword=heart_rate|lang=zh-CN|style=Feynman)、写下的东西。但如果您将整个理论建立在这些*局域*观测之上，您会得出他们永远无法互动的结论。如果您发现他们一直在通过微弱地[振动](@keyword=vibrational_motion|lang=zh-CN|style=Feynman)地板来传递纸条——这是一种根本上*非局域*的联系——您会感到困惑不已。简而言之，这就是几十年来[计算科学](@keyword=computational_science|lang=zh-CN|style=Feynman)家在试图理解所有[化学键](@keyword=chemical_bonds|lang=zh-CN|style=Feynman)中最温和的一种——[范德华力](@keyword=van_der_waals_forces|lang=zh-CN|style=Feynman)时所面临的巨大难题。

### 量子世界中的幽灵：[缺失](@keyword=deletion|lang=zh-CN|style=Feynman)的吸[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)

在我们自下而上模拟宇宙的探索中，[密度泛函理论](@keyword=density_functional_theory_2|lang=zh-CN|style=Feynman)（DFT）是我们最强大的工具之一。它允许我们基于一个基本量来计算分子和材料的性质：[电子](@keyword=electrons|lang=zh-CN|style=Feynman)的[分布](@keyword=generalized_functions|lang=zh-CN|style=Feynman)，即[电子密度](@keyword=electron_density|lang=zh-CN|style=Feynman) $n(\mathbf{r})$。DFT 的高明之处在于，它用一个基于这个更简单的、[弥散](@keyword=dispersion|lang=zh-CN|style=Feynman)的[电荷](@keyword=electrical_charge|lang=zh-CN|style=Feynman)云的理论，取代了每个[电子](@keyword=electrons|lang=zh-CN|style=Feynman)极其复杂的舞蹈。

DFT 的主力近似方法，即**[局域密度近似](@keyword=local_density_approximation|lang=zh-CN|style=Feynman)（LDA）**和**[广义梯度近似](@keyword=generalized_gradient_approximation|lang=zh-CN|style=Feynman)（GGA）**，遵循一个极其简单的原理。为了计算分子中某一点的能量，它们*仅仅*关注该点的[电子密度](@keyword=electron_density|lang=zh-CN|style=Feynman)（在 LDA 中）或[密度](@keyword=density|lang=zh-CN|style=Feynman)及其陡峭程度（其[梯度](@keyword=gradient|lang=zh-CN|style=Feynman)，在 GGA 中）[@problem_id:2088815]。这就像我们只通过观察各自的房间来观察那两个人一样。

对于原子间剧烈争夺和共享[电子](@keyword=electrons|lang=zh-CN|style=Feynman)的强[化学键](@keyword=chemical_bonds|lang=zh-CN|style=Feynman)，这种局域图像的效果惊人地好。但当我们模拟一些更精细的体系时会发生什么呢？考虑两个高贵而孤傲的氩原子相互漂移靠近，或者想象一个氩原子漂浮在一张巨大而平靜的[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)片上[@problem_id:1977558]。实验告诉我们，在更强的排斥力将它们推开之前，存在一种微弱但不可否认的吸引性“[粘性](@keyword=viscosity|lang=zh-CN|style=Feynman)”会将它们拉到一起。然而，当我们用 LDA 或 GGA 计算时，它们给出的结果却很奇怪：原子之间几乎感觉不到任何吸[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)！它们只是在靠得太近时相互排斥[@problem_id:1363356]。这种理论，尽管功能强大，却对那种能使液体凝聚、让壁虎粘在墙上的力视而不见。它错过了机器中的一个幽灵。

### 瞬时偶极的舞蹈

这一失败的原因是深远的。[范德华力](@keyword=van_der_waals_forces|lang=zh-CN|style=Feynman)——或者更具体地说，[伦敦色散力](@keyword=london_dispersion_forces|lang=zh-CN|style=Feynman)——就是我们局域观察者错过的“地板[振动](@keyword=vibrational_motion|lang=zh-CN|style=Feynman)”式相互作用。它并非源于任何静态或永久的东西，而是源于[电子](@keyword=electrons|lang=zh-CN|style=Feynman)永不停息的量子[抖动](@keyword=dithering|lang=zh-CN|style=Feynman)。

即使在像氩这样完全球形[对称](@keyword=symmetry|lang=zh-CN|style=Feynman)且[电中性](@keyword=electroneutrality|lang=zh-CN|style=Feynman)的原子中，[电子](@keyword=electrons|lang=zh-CN|style=Feynman)云也不是一个静态的绒球，而是一个翻滚、涨落的量子实体。在一个极短暂的瞬间，[电子](@keyword=electrons|lang=zh-CN|style=Feynman)可能恰好聚集在[原子核](@keyword=nucleus|lang=zh-CN|style=Feynman)的一侧。这会产生一个稍纵即逝的**瞬时偶极**：一个存在时间仅为一瞬间的微小磁体。这个微小、闪烁的场延伸到空间中，影响邻近原子的[电子](@keyword=electrons|lang=zh-CN|style=Feynman)云，诱使其发生[同步](@keyword=synchronization|lang=zh-CN|style=Feynman)涨落——形成一个**[感应偶极](@keyword=induced_dipole|lang=zh-CN|style=Feynman)**。这两个临时偶极现在以完美的关联性共舞，并相互吸引。这种瞬时偶极的协同舞蹈，即一种**非局域[电子](@keyword=electrons|lang=zh-CN|style=Feynman)相关效应**，正是[色散力](@keyword=dispersion_forces|lang=zh-CN|style=Feynman)的起源[@problem_id:1977558]。

这正是 LDA 和 GGA 失效的原因。从其构造上讲，它们对这些长程相关是“盲目”的。它们的数学形式只考虑单一点的[密度](@keyword=density|lang=zh-CN|style=Feynman) $n(\mathbf{r})$ 及其紧邻的[周围](@keyword=entourages|lang=zh-CN|style=Feynman)环境 $\nabla n(\mathbf{r})$，因此无法知道*这里*的[密度涨落](@keyword=density_fluctuations|lang=zh-CN|style=Feynman)与遥远的*那里*的涨落是相关的[@problem_id:2480419]。对于两个[电子](@keyword=electrons|lang=zh-CN|style=Feynman)云不重叠的原子，半局域[泛函](@keyword=functional|lang=zh-CN|style=Feynman)只看到两个独立的系统，其计算出的[相互作用能](@keyword=interaction_energy|lang=zh-CN|style=Feynman)为零。然而，真实的[相互作用能](@keyword=interaction_energy|lang=zh-CN|style=Feynman)却随着距离 $R$ 的增加而优雅地[衰减](@keyword=attenuation|lang=zh-CN|style=Feynman)，形式为 $-C_6/R^6$。这是一种[幂律](@keyword=power_laws|lang=zh-CN|style=Feynman)，是[长程力](@keyword=long_range_forces|lang=zh-CN|style=Feynman)的标志，而局域理论永远无法产生这种形式。[二阶微扰理论](@keyword=second_order_perturbation_theory|lang=zh-CN|style=Feynman)证明，两个基态原子间的这种相互作用总是吸引的，因为它是一个带有总负号的正项之和[@problem_id:2942361]。

### 务实的补丁：将力加回去

如果你的理论中缺少一种力，最直接的解决方案就是手动将其加回去。这正是被称为 **[DFT-D](@keyword=dft_d|lang=zh-CN|style=Feynman)**（带[色散校正](@keyword=dispersion_correction|lang=zh-CN|style=Feynman)的 DFT）系列方法背后绝妙而务实的思想[@problem_id:1363406]。

该方法很简单：我们采用标准的 DFT 计算（它能基本正确地处理短程物理），然后附加一个额外的能量项，该项明确地模拟[缺失](@keyword=deletion|lang=zh-CN|style=Feynman)的[色散力](@keyword=dispersion_forces|lang=zh-CN|style=Feynman)。这个项通常是所有原子对的总和，具有我们熟悉的形式：

$$
E_{\text{disp}} = - \sum_{A<B} \frac{C_6^{AB}}{R_{AB}^6}
$$

在这里，$R_{AB}$ 是原子 A 和 B 之间的距离，$C_6^{AB}$ 是描述它们[相互作用强度](@keyword=interaction_strength|lang=zh-CN|style=Feynman)的系数。但一个新问题立刻出现：当原子非常接近时（$R_{AB} \to 0$），这个公式会[发散](@keyword=divergence|lang=zh-CN|style=Feynman)；而在这些短距离下，基础的 DFT [泛函](@keyword=functional|lang=zh-CN|style=Feynman)已经在尝试描述[电子](@keyword=electrons|lang=zh-CN|style=Feynman)相关。添加完整的[色散](@keyword=dispersion|lang=zh-CN|style=Feynman)项会“重[复计](@keyword=double_counting|lang=zh-CN|style=Feynman)算”吸引作用。

解决方案是使用一个**[阻尼](@keyword=damping|lang=zh-CN|style=Feynman)函数** $f_{\text{damp}}(R_{AB})$。校正后的能量表达式变为：

$$
E_{\text{disp}} = - \sum_{A<B} f_{\text{damp}}(R_{AB}) \frac{C_6^{AB}}{R_{AB}^6}
$$

这个[阻尼](@keyword=damping|lang=zh-CN|style=Feynman)函数就像一个外交调解员。它的设计使其在短距离时几乎为零，告诉[色散校正](@keyword=dispersion_correction|lang=zh-CN|style=Feynman)项保持“安静”，让主要的 DFT [泛函](@keyword=functional|lang=zh-CN|style=Feynman)发挥作用。随着原子分开，[阻尼](@keyword=damping|lang=zh-CN|style=Feynman)[函数平滑](@keyword=function_smoothing|lang=zh-CN|style=Feynman)地增加到 1，让 $R^{-6}$ 项接管并正确描述长程物理[@problem_id:2942361]。这是一个补丁，一种经验性修正，但却非常有效，它彻底改变了 DFT 在分子和生物系统中的准确性。

### 更复杂的对话：从原子对到群体

然而，这种成对图像仍然是一种近似。两个原子间的“对话”可以被第三个原子“偷听”并影响。对成对图像的主要校正是**[三体](@keyword=trisomy|lang=zh-CN|style=Feynman)相互作用**，即 Axilrod-Teller-Muto (ATM) 力[@problem_id:170760]。它揭示了三个原子的[色散能](@keyword=dispersion_energy|lang=zh-CN|style=Feynman)并不仅仅是三对原子（A-B、B-C 和 A-C）能量的总和，还有一个额外的项，取决于它们形成的三角形的几何形状。对于共线的三个原子，这个[三体](@keyword=trisomy|lang=zh-CN|style=Feynman)项是排斥的，削弱了总吸[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)；对于等边三角形，它则是吸引的，增强了总吸[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)。

这仅仅是个开始。在致密系统中，比如表面上的分子，情况就变成了集[体效应](@keyword=body_effect|lang=zh-CN|style=Feynman)的故事。当一个分子的[电子](@keyword=electrons|lang=zh-CN|style=Feynman)云在金属表面附近涨落时，它不仅仅是在与一个原子对话，而是在与整个[离域电子](@keyword=delocalized_electrons|lang=zh-CN|style=Feynman)的海洋对话。这个[电子](@keyword=electrons|lang=zh-CN|style=Feynman)海洋可以集体响应来**屏蔽**这种相互作用，从而有效地削弱它。这就像试图在一个嘈杂拥挤的房间里进行私人谈话——信息会被减弱。像 [DFT-D](@keyword=dft_d|lang=zh-CN|style=Feynman) 这样的简单成对模型，其参数来自自由原子，会错过这种[屏蔽效应](@keyword=electron_shielding|lang=zh-CN|style=Feynman)，因此常常显著高估分子在金属表面的[吸附](@keyword=adsorption|lang=zh-CN|style=Feynman)强度[@problem_id:2455173]。这催生了更复杂的模型，这些模型根据局域[电子](@keyword=electrons|lang=zh-CN|style=Feynman)环境调整相互作用，例如根据[电子密度](@keyword=electron_density|lang=zh-CN|style=Feynman)缩放原子性质的 Tkatchenko-Scheffler (TS) 方案，或者通过将原子建模为[耦合振子](@keyword=coupled_oscillators|lang=zh-CN|style=Feynman)来明确计算集体[屏蔽效应](@keyword=electron_shielding|lang=zh-CN|style=Feynman)的[多体色散](@keyword=many_body_dispersion|lang=zh-CN|style=Feynman)（MBD）方法[@problem_id:2768270]。

### 走向统一描述：[非局域泛函](@keyword=nonlocal_functionals|lang=zh-CN|style=Feynman)的兴起

尽管经验性校正很有用，但终极目标是建立一个[色散能](@keyword=dispersion_energy|lang=zh-CN|style=Feynman)从[第一性原理](@keyword=ab_initio|lang=zh-CN|style=Feynman)自然产生的理论。这种渴望催生了**[范德华密度泛函](@keyword=vdw_df|lang=zh-CN|style=Feynman)（vdW-DF）**的发展[@problem_id:2480419]。这是一类新的[泛函](@keyword=functional|lang=zh-CN|style=Feynman)，它们摒弃了严格的局域世界观。它们在能量表达式中包含一个真正的非局域项，通常形式如下：

$$
E_{c}^{\text{nl}}[n] = \frac{1}{2} \iint n(\mathbf{r}) \, \Phi(\mathbf{r}, \mathbf{r}') \, n(\mathbf{r}') \, d\mathbf{r} \, d\mathbf{r}'
$$

这个方程完美地表达了其背后的物理。它表明，[非局域相关](@keyword=nonlocal_correlation|lang=zh-CN|style=Feynman)能 $E_{c}^{\text{nl}}$ 是通过对空间中所有点对 $\mathbf{r}$ 和 $\mathbf{r}'$ 进行积分得到的。$\mathbf{r}$ 点的[密度](@keyword=density|lang=zh-CN|style=Feynman)通过一个**[核函数](@keyword=kernel_function|lang=zh-CN|style=Feynman)** $\Phi(\mathbf{r}, \mathbf{r}')$ 与 $\mathbf{r}'$ 点的[密度](@keyword=density|lang=zh-CN|style=Feynman)联系起来，这个[核函数](@keyword=kernel_function|lang=zh-CN|style=Feynman)在我们之前的比喻中扮演了“地板”的角色，传递着相关的涨落。与 [DFT-D](@keyword=dft_d|lang=zh-CN|style=Feynman) 方法不同，这不是一个计算后的补丁，而是[泛函](@keyword=functional|lang=zh-CN|style=Feynman)的一个组成部分。[色散](@keyword=dispersion|lang=zh-CN|style=Feynman)相互作用是自洽计算的，它会反过来影响最终的[电子密度](@keyword=electron_density|lang=zh-CN|style=Feynman)本身。

这种方法的力量在于其[普适性](@keyword=universality|lang=zh-CN|style=Feynman)。[核函数](@keyword=kernel_function|lang=zh-CN|style=Feynman) $\Phi$ 是基于基本物理设计的，而不是针对特定原子类型拟合的。它内在地包含了[多体效应](@keyword=many_body_effects|lang=zh-CN|style=Feynman)，并能自动响应[电子](@keyword=electrons|lang=zh-CN|style=Feynman)环境。这使其能够无缝地描述从原子对到表面分子，再到像石墨这样的层状材料的结合等各种情况。例如，两个原子间的相互作用按 $R^{-6}$ 规律[衰减](@keyword=attenuation|lang=zh-CN|style=Feynman)，而两个大的[平行平面](@keyword=parallel_planes|lang=zh-CN|style=Feynman)（如[石墨烯](@keyword=graphene|lang=zh-CN|style=Feynman)层）间的相互作用则按 $d^{-4}$ [衰减](@keyword=attenuation|lang=zh-CN|style=Feynman)，其中 $d$ 是层间距。vdW-DF 方法能够正确地捕捉到这种[标度律](@keyword=scaling_laws|lang=zh-CN|style=Feynman)的变化，这是简单的成对模型无法实现的壮举 [@problem_id:2768235], [@problem_id:2768270]。

对全空间计算这个双重积分似乎在计算上是不可能的。然而，一个巧妙的数学重构使得其计算成本能够随体系大小近似[线性增长](@keyword=linear_growth|lang=zh-CN|style=Feynman)，这要归功于[快速傅里叶变换](@keyword=fast_fourier_transform|lang=zh-CN|style=Feynman)（FFT）的魔力[@problem_id:2768235]。这一[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)上的突破使得这些强大的[第一性原理方法](@keyword=ab_initio_methods|lang=zh-CN|style=Feynman)成为前沿[材料发现](@keyword=materials_discovery|lang=zh-CN|style=Feynman)的实用工具。我们理论中[缺失](@keyword=deletion|lang=zh-CN|style=Feynman)的那个“幽灵”不仅被找到了，而且被以一种优雅而严谨的方式描述，统一了强[化学键](@keyword=chemical_bonds|lang=zh-CN|style=Feynman)的世界和维系我们世界存在的温和而普遍的力。

