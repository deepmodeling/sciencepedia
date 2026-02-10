## 引言
在入门物理学的理想世界里，电子被视为孤立、独立的粒子进行运动。然而，在真实的材料世界中，一个电子从来都不是真正孤独的。它在一个由其他电子构成的密集海洋中穿行，它们之间的相互排斥创造了一场复杂的集体之舞。这种环境从根本上改变了电子的身份，为其披上了一层相互作用的云，从而改变了它的性质。[多体物理学](@keyword=many_body_physics_2|lang=zh-CN|style=Feynman)的核心挑战是理解和描述这些“缀饰”粒子，正是它们主导着金属、绝缘体和[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)的行为。在这个缀饰过程中，原始的裸电子有多少成分得以保留？

本文通过探讨[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)（用$Z$表示）来回答这个问题。这个单一而强大的数字为[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的[相干性](@keyword=coherence|lang=zh-CN|style=Feynman)提供了定量度量，并将相互作用的微观量子世界与宏观、可测量的[材料性质](@keyword=material_properties|lang=zh-CN|style=Feynman)联系起来。本文的结构旨在引导读者从基本概念走向其在现实世界中的应用。第一章“原理与机制”将阐释[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)的物理意义、其与[谱函数](@keyword=spectral_function|lang=zh-CN|style=Feynman)的关系，以及其与电子有效质量的深刻联系。接下来的“应用与跨学科联系”一章将展示这一理论概念如何应用于理解[重费米子材料](@keyword=heavy_fermion_materials|lang=zh-CN|style=Feynman)和[金属-绝缘体相变](@keyword=metal_insulator_transition|lang=zh-CN|style=Feynman)等现象，如何通过实验进行测量，以及它在不同物理学领域的惊人普适性。

## 原理与机制

想象一下，你正试图穿过一个异常拥挤的房间。你无法直接前进，必须推开身边的人，他们会推回来，其他人为了让他们通过也必须移动，于是一圈扰动在你周围[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)开来。从远处看，观察者看到的不仅仅是*你*在移动，而是一个更复杂的实体：你，加上你周围人群的漩涡式运动。这个新的复合体——这个“缀饰”版的你——比你在空房间里移动时要迟缓得多。从某种意义上说，它更重了。

这对于我们向金属中注入一个电子时发生的情况，是一个惊人贴切的类比。金属是无数其他电子的海洋，所有电子都相互排斥。一个孤立的电子不可能不受干扰地行进。它的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)会推开其他电子，而其他电子的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)也会反作用于它。这个电子以及它所携带的关联运动云构成了一个新的实体——**[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)**。它是相互作用电子低能世界中的基本角色。但是在这个缀饰版本中，还剩下多少原始“裸”电子的成分呢？这个问题的答案就在于一个单一而强大的数字：**[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)**，用$Z$表示。

### [准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)及其幽灵

在量子力学的简洁世界里，一个动量为$\mathbf{k}$的单一自由电子具有确定的能量$\epsilon_{\mathbf{k}}$。如果我们要将其存在绘制在能量-动量图上，它会表现为一个无限尖锐的峰。但在拥挤的金属中，电子的身份因相互作用而“破碎”。

完整的图像由一个称为**谱函数**的工具$A(\mathbf{k}, \omega)$来捕捉，它告诉我们找到一个动量为$\mathbf{k}$、能量为$\omega$的激发的概率。对于我们金属中的电子，谱函数揭示了一个引人入胜的故事。原始电子身份的一部分以一个相干、尖锐的峰的形式存活下来，看起来很像一个自由粒子，但能量有所修正。这就是[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)。关键在于，这个峰的总概率，或称“权重”，不再是$1$。它恰好就是[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)$Z$。

那么，电子的其余部分去哪儿了？剩余的[谱权重](@keyword=spectral_weight|lang=zh-CN|style=Feynman)，等于$1-Z$，被涂抹成一个位于更高能量处的宽阔、无特征的连续谱，通常被称为**非相干背景**。这个背景代表了我们的粒子激起的周围电子海中所有杂乱、复杂的激发。电子的本质被分裂了：一部[分形](@keyword=fractal|lang=zh-CN|style=Feynman)成了相干的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，其余部分则消融成一团多体激发的“幽灵”云 [@3013284] [@2985552]。

这赋予了$Z$深刻的物理意义：它是[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)相干性的度量。它是增加一个裸电子所创建的态与相互作用系统的真实[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)态之间的交叠或“相似度”[@2862023] [@3013284]。从数学上讲，如果$|\Psi_{N}\rangle$是$N$个[电子的基态](@keyword=ground_state_of_electrons|lang=zh-CN|style=Feynman)，而$|\Psi_{N+1, \mathbf{k}}\rangle$是包含一个动量为$\mathbf{k}$的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的真实$(N+1)$粒子态，那么[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)就是它们交叠的平方：

$$
Z_{\mathbf{k}} = |\langle \Psi_{N+1, \mathbf{k}} | c_{\mathbf{k}}^{\dagger} | \Psi_{N} \rangle|^2
$$

其中$c_{\mathbf{k}}^{\dagger}$是产生裸电子的算符。根据这个定义，$Z$必须是一个介于$0$和$1$之间的数。对于一个无相互作用的系统，[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)就是裸电子，所以$Z=1$。随着相互作用变强，缀饰云变得更加庞大，与裸电子的交叠随之缩小。因此，$Z$从$1$开始减小，量化了电子的身份在多大程度上被“溶解”在群体之中。

### 人群的负担：[质量重整化](@keyword=mass_renormalization|lang=zh-CN|style=Feynman)

被一群其他粒子缀饰最直接的后果就是你会变得更重。我们的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)也是如此。其[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)$m^*$大于裸电子的质量$m$。这种质量增强与[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)之间的关系是该理论最优雅的成果之一。

在许多重要情况下，例如在维度非常高的系统或只有局域相互作用的系统中，这种联系异常简洁：有效质量与[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)成反比 [@2983237] [@2833041]。

$$
\frac{m^*}{m} = \frac{1}{Z}
$$

这在直觉上非常有道理。一个小的$Z$意味着[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)主要由迟缓的缀饰云构成，只剩下很少的“裸电子”特性。它负担沉重，因此具有很大的[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)。$Z=0.01$的值意味着[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)比自由电子重$100$倍！在更一般的情况下，当相互作用也依赖于动量时，关系会稍微复杂一些，但基本趋势依然存在 [@2833041]。

这一原理在**[莫特转变](@keyword=mott_transition|lang=zh-CN|style=Feynman)**中得到了最戏剧性的体现。[莫特转变](@keyword=mott_transition|lang=zh-CN|style=Feynman)是一种强[电子-电子排斥](@keyword=electron_electron_repulsion|lang=zh-CN|style=Feynman)能将本应是金属的物质转变为绝缘体的现象。在所谓的Brinkman–Rice图像中，随着在位排斥能$U$的增加，电子之间变得越来越“相互排斥”，导致缀饰云越来越重。这会驱动[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)$Z$连续地趋向于零。根据我们的公式，有效质量$m^*$必然发散至无穷大！[@2974458] [@2974447]。在临界[相互作用强度](@keyword=interaction_strength|lang=zh-CN|style=Feynman)$U_c$处，$Z$达到零，[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)变得无限重，然后被卡住。电子被局域化，相干运动停止，金属变成了绝缘体。

### [准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的指纹

[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)这个抽象概念不仅仅是理论家的幻想；它在材料的性质上留下了具体、可测量的指纹。

*   **[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)：** 想想加热一种物质需要多少能量。一群非常重的粒子比一群轻的粒子更难“晃动”。在低温下，电子对比热的贡献由$C_v = \gamma T$给出，其中[索末菲系数](@keyword=sommerfeld_coefficient|lang=zh-CN|style=Feynman)$\gamma$与[有效质量](@keyword=effective_mass|lang=zh-CN|style=Feynman)成正比，即$\gamma \propto m^*$。由于$m^* \propto 1/Z$，我们发现$\gamma \propto 1/Z$。这为$Z$提供了一个直接的实验探针。的确，有一类引人入胜的材料被称为**重费米子体系**——其中的一个关键例子是[近藤晶格](@keyword=kondo_lattice|lang=zh-CN|style=Feynman)材料，其实测的$\gamma$值可以比普通金属大数百甚至数千倍。这直接表明这些材料中的[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)异常重，对应着一个非常小的[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)$Z \ll 1$ [@2833041]。

*   **[动量分布](@keyword=momentum_distribution|lang=zh-CN|style=Feynman)：** 在绝对零度的无[相互作用费米子](@keyword=interacting_fermions|lang=zh-CN|style=Feynman)气体中，所有动量低于一个尖锐的**[费米动量](@keyword=fermi_momentum|lang=zh-CN|style=Feynman)**$k_F$的态都被占据，而所有高于它的态都是空的。这在[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)上，动量占据数函数$n(\mathbf{k})$会出现一个幅度为$1$的尖锐阶梯状下降。相互作用改变了这一点。缀饰云导致一些电子即使在[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)下也被散射到$|\mathbf{k}| > k_F$的态上。结果是，费米面上的尖锐阶梯被削弱为一个较小的不连续。这个跳跃的幅度不再是$1$，而恰好等于[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)$Z$！[@3013284, @2985552, @2974458]。在像角分辨光电子能谱（ARPES）这样的测量中看到这个跳跃，就是看到了费米液体的实际作用，而跳跃的大小就是对$Z$的直接测量。

*   **电导率：** 在金属中是什么承载着电流？是[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)的相干运动。光学电导率中对应于这种无耗散、相干流动的分量被称为**[德鲁德权重](@keyword=drude_weight|lang=zh-CN|style=Feynman)**。理论模型表明，这个[德鲁德权重](@keyword=drude_weight|lang=zh-CN|style=Feynman)与$Z$成正比 [@2974447]。当我们接近$Z \to 0$的[莫特转变](@keyword=mott_transition|lang=zh-CN|style=Feynman)时，[德鲁德权重](@keyword=drude_weight|lang=zh-CN|style=Feynman)消失。这标志着相干载流子的完全丧失，材料变成绝缘体，无法传导直流电。

### 当[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)消逝时

$Z \to 0$的极限标志着我们所熟悉的金属世界的边缘，在这一点上，[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)概念本身瓦解，系统进入一个**[非费米液体](@keyword=non_fermi_liquids|lang=zh-CN|style=Feynman)**状态。这里发生了什么？

我们已经看到了一条路径：莫特绝缘体，其中[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)变得无限重并被局域化。它们在[谱函数](@keyword=spectral_function|lang=zh-CN|style=Feynman)中的相干峰完全消失，其权重被非相干的[哈伯德带](@keyword=hubbard_bands|lang=zh-CN|style=Feynman)吸收，并且[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)打开，禁止了带电激发 [@2974458] [@3013256]。一个引人入胜的问题出现了：如果*定义*费米面的$n(\mathbf{k})$的跳跃消失了，费米面本身是否也消失了？答案是一个深刻而优美的“不”。**[卢廷格定理](@keyword=luttinger_s_theorem|lang=zh-CN|style=Feynman)**，一个根植于粒子数守恒的强大结果，指出，由费米面包围的体积是一个拓扑不变量，由电子总数固定。即使当$Z$趋于零时，这个体积也保持不变。变化的是费米面的*性质*。在$Z > 0$的[费米液体](@keyword=fermi_liquid|lang=zh-CN|style=Feynman)中，费米面是[格林函数](@keyword=green_s_functions|lang=zh-CN|style=Feynman)中极点的轨迹。当$Z \to 0$时，这可以演变为一个零点的轨迹 [@2998985]。即便边界上激发的性质完全改变，计数仍然是正确的。

[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)还有另一种更奇怪的死亡方式。在一些奇特的材料中，如高温超导[铜氧化物](@keyword=cuprates|lang=zh-CN|style=Feynman)，系统似乎没有一个单一、明确的[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)$Z$。相反，权重变成了能量的函数$Z(\omega)$。一个激发越接近[费米能级](@keyword=fermi_level|lang=zh-CN|style=Feynman)（$\omega=0$），它被缀饰得就越重。这导致了一种**边缘[费米液体](@keyword=fermi_liquid|lang=zh-CN|style=Feynman)**，其中[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)在接近[费米能](@keyword=fermi_energy|lang=zh-CN|style=Feynman)时以对数方式消失：$Z(\omega) \propto 1/\ln(\omega_c/|\omega|)$ [@3007647]。恰在[费米面](@keyword=fermi_surface|lang=zh-CN|style=Feynman)上，[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)已完全失去相干性，但它在离费米面任何有限能量处都“勉强”存在。这是一个摇摇欲坠地处于[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)边缘的宇宙。

最后，我们可以给出一个统一所有这些思想的形式化定义。[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)及其性质由**[自能](@keyword=self_energy|lang=zh-CN|style=Feynman)**$\Sigma(\mathbf{k}, \omega)$决定，它在数学上概括了“人群”的全部效应。[自能](@keyword=self_energy|lang=zh-CN|style=Feynman)的实部$\Sigma'$会修正粒子的能量。一个关键的洞见是，[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)$Z$与[自能](@keyword=self_energy|lang=zh-CN|style=Feynman)随能量变化的快慢直接相关：

$$
Z_{\mathbf{k}} = \frac{1}{1 - \left. \frac{\partial \Sigma'(\mathbf{k}, \omega)}{\partial \omega} \right|_{\omega=0}}
$$

[@2862023] 自能强烈的能量依赖性（一个大的负[导数](@keyword=derivative|lang=zh-CN|style=Feynman)）意味着一个对能量变化非常敏感的重缀饰云。这导致了小的$Z$和大的有效质量，从而将形式化定义与我们关于负重电子的物理图像优雅地联系起来。从一个人在人群中的简单类比出发，[准粒子权重](@keyword=quasiparticle_weight|lang=zh-CN|style=Feynman)的概念得以展开，用以解释电子的质量、金属的[热容](@keyword=thermal_capacitance|lang=zh-CN|style=Feynman)、[电传导](@keyword=electrical_conduction|lang=zh-CN|style=Feynman)的本质，乃至向绝缘体的急剧转变，揭示了量子多粒子世界深刻的统一性与美感。