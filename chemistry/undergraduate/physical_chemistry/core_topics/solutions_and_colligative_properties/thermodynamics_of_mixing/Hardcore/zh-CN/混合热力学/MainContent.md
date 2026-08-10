## 引言
混合是自然界最基本的[物理化学](@keyword=physical_chemistry|lang=zh-CN|style=Feynman)过程之一，它控制着从[合金形成](@keyword=alloy_formation|lang=zh-CN|style=Feynman)到生命活动等众多现象。然而，为什么有些物质可以无限互溶，而另一些却会分层？这种行为背后的驱动力是什么？本文旨在系统地回答这些问题，深入剖析混合过程的[热力学原理](@keyword=thermodynamic_principles|lang=zh-CN|style=Feynman)。我们将首先从最简单的[理想混合](@keyword=ideal_mixing|lang=zh-CN|style=Feynman)模型出发，揭示熵在其中的核心作用；然后，通过引入分子间相互作用，过渡到更贴近现实的非[理想溶液模型](@keyword=ideal_solution_model|lang=zh-CN|style=Feynman)，并解释相分离等复杂现象。通过本文的学习，读者将能够理解混合过程中的能量与无序之争，并掌握分析真实世界体系相稳定性的基本工具。文章将通过“原理与机制”、“应用与跨学科联系”以及“动手实践”三个章节，层层递进地引导你从理论基础走向实际应用，全面掌握混合[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)的精髓。

## 原理与机制

混合过程是自然界和工业生产中普遍存在的现象，从大气中气体的[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)到[高分子](@keyword=macromolecules|lang=zh-CN|style=Feynman)合金的制备，都涉及不同组分在[分子尺](@keyword=molecular_ruler|lang=zh-CN|style=Feynman)度上的相互渗透。本章旨在深入探讨混合过程背后的[热力学原理](@keyword=thermodynamic_principles|lang=zh-CN|style=Feynman)与机制。我们将从最简单的[理想混合](@keyword=ideal_mixing|lang=zh-CN|style=Feynman)模型出发，揭示熵在自发混合过程中的核心驱动作用，然后引入[正规溶液模型](@keyword=regular_solution_model|lang=zh-CN|style=Feynman)来描述非理想性，并最终探讨相分离、[临界溶解温度](@keyword=critical_solution_temperature|lang=zh-CN|style=Feynman)等更为复杂的现象。

### [理想混合](@keyword=ideal_mixing|lang=zh-CN|style=Feynman)：熵驱动力

为何两种能够相互溶解的物质在接触时会自发地混合？答案深植于[热力学第二定律](@keyword=second_law_of_thermodynamics|lang=zh-CN|style=Feynman)。在一个孤立系统中，任何自发过程都会朝着熵增加的方向进行。混合过程极大地增加了系统的无序度，从而导致熵的增加，这是混合的主要驱动力。

#### 混合熵的统计学起源

我们可以通过一个思想实验来量化混合过程中的熵变。考虑将几种不同的理想气体在恒温恒压下混合。在混合之前，每种气体 $i$ 占据其各自的体积 $V_i$。混合后，所有气体均匀地[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)在总体积 $V = \sum_i V_i$ 中。从每一种组分的角度来看，混合过程等效于一次[等温膨胀](@keyword=isothermal_expansion|lang=zh-CN|style=Feynman)，其体积从初始的分体积 $V_i$ 扩大到最终的总体积 $V$。对于 $n_i$ 摩尔的[理想气体](@keyword=perfect_gases|lang=zh-CN|style=Feynman)，这个过程的熵变为：
$$ \Delta S_i = n_i R \ln\left(\frac{V}{V_i}\right) $$
其中 $R$ 是[理想气体](@keyword=perfect_gases|lang=zh-CN|style=Feynman)常数。

由于理想气体在恒温恒压下混合时，其分体积之比等于其摩尔分数之比，即 $V_i/V = n_i/n_{total} = x_i$，其中 $x_i$ 是组分 $i$ 的摩尔分数。因此，我们可以将上式重写为：
$$ \Delta S_i = n_i R \ln\left(\frac{1}{x_i}\right) = -n_i R \ln x_i $$

系统的总**[混合熵](@keyword=mixing_entropy|lang=zh-CN|style=Feynman) (entropy of mixing)**, $\Delta S_{mix}$，是所有组分[熵变](@keyword=entropy_change|lang=zh-CN|style=Feynman)的总和：
$$ \Delta S_{mix} = \sum_i \Delta S_i = -R \sum_i n_i \ln x_i $$

如果我们关心的是单位摩尔量的[混合熵](@keyword=mixing_entropy|lang=zh-CN|style=Feynman)，即**摩尔[混合熵](@keyword=mixing_entropy|lang=zh-CN|style=Feynman) ($\Delta \bar{S}_{mix}$)**，我们只需将总[混合熵](@keyword=mixing_entropy|lang=zh-CN|style=Feynman)除以总摩尔数 $n_{total}$：
$$ \Delta \bar{S}_{mix} = \frac{\Delta S_{mix}}{n_{total}} = -R \sum_i x_i \ln x_i $$

这个公式具有普适性，它不仅适用于[理想气体](@keyword=perfect_gases|lang=zh-CN|style=Feynman)，也适用于**理想溶液 (ideal solution)**，即那些混合时[分子间相互作用](@keyword=molecular_interactions|lang=zh-CN|style=Feynman)力没有变化的液体或固体混合物。例如，一个由氧气、氦气和氮气组成的用于深海潜水的三元气体混合物（Trimix），其摩尔[混合熵](@keyword=mixing_entropy|lang=zh-CN|style=Feynman)就可以用这个公式精确描述 [@problem_id:2025803]。由于[摩尔分数](@keyword=mole_fraction|lang=zh-CN|style=Feynman) $x_i$ 恒小于1，其对数 $\ln x_i$ 恒为负，因此 $\Delta S_{mix}$ 总是正值。这从[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)上证明了，只要分子间没有特殊的排斥作用，混合总是一个[熵增](@keyword=entropy_generation|lang=zh-CN|style=Feynman)的、自发有利的过程。

#### [吉布斯佯谬](@keyword=gibbs_paradox|lang=zh-CN|style=Feynman)与粒子的可区分性

混合熵的统计学本质引出了一个经典的思想实验——**[吉布斯佯谬](@keyword=gibbs_paradox|lang=zh-CN|style=Feynman) (Gibbs Paradox)**。假设我们有一个被隔板分为两半的容器，两边装着相同种类、相同温度和压力的[理想气体](@keyword=perfect_gases|lang=zh-CN|style=Feynman)。当我们移除隔板时，宏观上没有任何变化发生——压力、温度和密度处处相等。直觉和实验都告诉我们，这个过程没有[熵变](@keyword=entropy_change|lang=zh-CN|style=Feynman)。然而，如果我们机械地套用[混合熵](@keyword=mixing_entropy|lang=zh-CN|style=Feynman)公式，将左右两边的气体视为两个“组分”，我们会计算出一个正的[熵变](@keyword=entropy_change|lang=zh-CN|style=Feynman)。

这个佯谬的解决关键在于**粒子的可区分性 (distinguishability)** [@problem_id:2025819]。[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)和[统计力学中的熵](@keyword=entropy_in_statistical_mechanics|lang=zh-CN|style=Feynman)变，与系统微观状态数的改变有关。只有当混合的粒子是可区分的（例如，不同种类的分子，甚至是同位素原子），移除隔板后，每种粒子才真正获得了新的空间构型，从而增加了系统的总微观状态数，导致[熵增](@keyword=entropy_generation|lang=zh-CN|style=Feynman)。如果两边的气体粒子是完全不可区分的，那么移除隔板前后，系统的总微观状态数并没有改变。因此，混合两种相同的理想气体，其 $\Delta S_{mix} = 0$。这个看似微妙的区别，是理解混合熵物理意义的基石。

#### 化学势：混合的[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)判据

虽然熵是混合的根本驱动力，但在恒温恒压条件下，描述系统平衡和自发方向的更直接的物理量是**[吉布斯自由能](@keyword=gibbs_free_energy|lang=zh-CN|style=Feynman) ($G$)**。而对于多组分系统，我们使用**化学势 ($\mu_i$)**，即偏摩尔[吉布斯自由能](@keyword=gibbs_free_energy|lang=zh-CN|style=Feynman)，来判断物质转移和[相变](@keyword=phase_change|lang=zh-CN|style=Feynman)的趋势。

当一种纯净的物质 $i$（例如，在压力为 $P$ 的纯氧气罐中的氧气）被引入到一个混合物中（例如，一个[总压](@keyword=stagnation_pressure|lang=zh-CN|style=Feynman)也为 $P$ 的氮氧混合气穹顶），其化学势会发生变化 [@problem_id:2025800]。对于[理想气体](@keyword=perfect_gases|lang=zh-CN|style=Feynman)或[理想溶液](@keyword=ideal_solutions|lang=zh-CN|style=Feynman)中的组分 $i$，其化学势 $\mu_i$ 与其在[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman)时的化学势 $\mu_i^*$（在相同温度和[总压](@keyword=stagnation_pressure|lang=zh-CN|style=Feynman)下）之间的关系为：
$$ \mu_i = \mu_i^* + RT \ln x_i $$

因此，组分 $i$ 从[纯态](@keyword=pure_states|lang=zh-CN|style=Feynman)到[混合态](@keyword=mixed_states|lang=zh-CN|style=Feynman)的化学势变化为：
$$ \Delta \mu_i = \mu_i - \mu_i^* = RT \ln x_i $$

由于 $x_i  1$，$\ln x_i$ 为负，所以 $\Delta \mu_i$ 总是负值。这表明，一个纯组分进入混合物中，其化学势会降低。物质总是自发地从高化学势区域流向低化学势区域，因此，纯组分自发地“溶解”或“[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)”到混合物中，直到整个系统达到均匀的化学势为止。化学势的降低是混合过程自发性的最终[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)判据。

#### [理想溶液](@keyword=ideal_solutions|lang=zh-CN|style=Feynman)的[吉布斯混合自由能](@keyword=gibbs_energy_of_mixing|lang=zh-CN|style=Feynman)

对于理想溶液，混合过程中的分子间相互作用能没有变化，因此其**[混合焓](@keyword=mixing_enthalpy|lang=zh-CN|style=Feynman) ($\Delta H_{mix}$)** 为零。结合我们已经得到的混合熵表达式，我们可以写出理想溶液的**[吉布斯混合自由能](@keyword=gibbs_energy_of_mixing|lang=zh-CN|style=Feynman) ($\Delta G_{mix}$)**：
$$ \Delta G_{mix} = \Delta H_{mix} - T\Delta S_{mix} = 0 - T(-R \sum_i n_i \ln x_i) = RT \sum_i n_i \ln x_i $$

相应的，摩尔[吉布斯混合自由能](@keyword=gibbs_energy_of_mixing|lang=zh-CN|style=Feynman)为：
$$ \Delta g_{mix} = RT \sum_i x_i \ln x_i $$

由于 $x_i  1$，$\Delta g_{mix}$ 对于任何非纯组分的混合物总是负值。$\Delta g_{mix}$ 对组成的曲线是一个向下凹的平滑曲线，其最低点在组分均匀混合时达到 [@problem_id:2025845]。这意味着对于[理想溶液](@keyword=ideal_solutions|lang=zh-CN|style=Feynman)，组分在任何比例下都可以自发混合，系统不存在相分离的趋势。

### [非理想溶液](@keyword=non_ideal_solutions|lang=zh-CN|style=Feynman)：[正规溶液模型](@keyword=regular_solution_model|lang=zh-CN|style=Feynman)

[理想溶液模型](@keyword=ideal_solution_model|lang=zh-CN|style=Feynman)是一个有力的理论起点，但它假设混合前后分子间的相互作用能不变（$\Delta H_{mix} = 0$），这在现实世界中很少成立。混合两种不同的液体，如水和乙醇，会因[氢键](@keyword=hydrogen_bonding|lang=zh-CN|style=Feynman)的形成和破坏而释放或吸收热量。为了描述这类**[非理想溶液](@keyword=non_ideal_solutions|lang=zh-CN|style=Feynman)**，我们需要更完善的模型。

#### [正规溶液模型](@keyword=regular_solution_model|lang=zh-CN|style=Feynman)的提出

**[正规溶液模型](@keyword=regular_solution_model|lang=zh-CN|style=Feynman) (Regular Solution Model)** 是对[理想溶液模型](@keyword=ideal_solution_model|lang=zh-CN|style=Feynman)最简单的、也是最重要的一步修正 [@problem_id:2002490]。它基于两个核心假设：
1.  [混合熵](@keyword=mixing_entropy|lang=zh-CN|style=Feynman)与[理想溶液](@keyword=ideal_solutions|lang=zh-CN|style=Feynman)完全相同，即 $\Delta S_{mix} = -R \sum n_i \ln x_i$。这等同于假设尽管分子间存在相互作用能的差异，但它们在空间上仍然是完全随机混合的。
2.  [混合焓](@keyword=mixing_enthalpy|lang=zh-CN|style=Feynman)不为零，对于一个二元体系（组分A和B），其摩尔[混合焓](@keyword=mixing_enthalpy|lang=zh-CN|style=Feynman)由一个简单的表达式给出：$\Delta H_{mix, m} = \Omega x_A x_B$。

这里的 $\Omega$ 是一个关键参数，称为**[相互作用参数](@keyword=interaction_parameters|lang=zh-CN|style=Feynman)**，它量化了混合过程中的能量变化。

#### [相互作用参数](@keyword=interaction_parameters|lang=zh-CN|style=Feynman)的微观解释

这个唯象的[混合焓](@keyword=mixing_enthalpy|lang=zh-CN|style=Feynman)表达式背后有其深刻的物理根源，可以通过一个简化的**准化学[格点模型](@keyword=lattice_models|lang=zh-CN|style=Feynman) (quasi-chemical lattice model)** 来理解 [@problem_id:2025821]。想象一个固体或液体由一个规则的[晶格](@keyword=crystalline_lattice|lang=zh-CN|style=Feynman)构成，每个格点被一个A原子或B原子占据。系统的总能量由最近邻原子对之间的[相互作用能](@keyword=interaction_energy|lang=zh-CN|style=Feynman)决定，我们分别用 $\epsilon_{AA}$、$\epsilon_{BB}$ 和 $\epsilon_{AB}$ 表示A-A、B-B和A-B对的相互作用能。

通过统计随机混合状态下各类原子对的数量，并与混合前纯组分的状态进行比较，可以推导出[混合焓](@keyword=mixing_enthalpy|lang=zh-CN|style=Feynman)为：
$$ \Delta H_{mix, m} = N_A z \left( \epsilon_{AB} - \frac{\epsilon_{AA} + \epsilon_{BB}}{2} \right) x_A x_B $$
其中 $N_A$ 是[阿伏伽德罗常数](@keyword=avogadro_s_constant|lang=zh-CN|style=Feynman)，$z$ 是[晶格](@keyword=crystalline_lattice|lang=zh-CN|style=Feynman)的配位数（一个原子周围的最近邻[原子数](@keyword=atomicity|lang=zh-CN|style=Feynman)）。

将括号内的项与相互作用参数 $\Omega$ 对应起来，我们得到：
$$ \Omega = N_A z \left( \epsilon_{AB} - \frac{\epsilon_{AA} + \epsilon_{BB}}{2} \right) $$

这个关系揭示了 $\Omega$ 的物理意义：
-   如果 $\Omega > 0$，意味着异类分子间的[相互作用能](@keyword=interaction_energy|lang=zh-CN|style=Feynman) $\epsilon_{AB}$ 不如（即能量更高）同类分子间相互作用能的平均值。分子倾向于与同类聚集，混合是[吸热过程](@keyword=endothermic_process|lang=zh-CN|style=Feynman)。这对应于“物以类聚”的情况。
-   如果 $\Omega  0$，意味着异类分子间的相互作用 $\epsilon_{AB}$ 更强。混合是[放热过程](@keyword=exothermic_process|lang=zh-CN|style=Feynman)，系统倾向于形成A-B对。
-   如果 $\Omega = 0$，则退化为[理想溶液](@keyword=ideal_solutions|lang=zh-CN|style=Feynman)的情况。

#### [正规溶液](@keyword=regular_solution|lang=zh-CN|style=Feynman)的[吉布斯混合自由能](@keyword=gibbs_energy_of_mixing|lang=zh-CN|style=Feynman)

结合[正规溶液](@keyword=regular_solution|lang=zh-CN|style=Feynman)的两个假设，我们可以立即写出其摩尔[吉布斯混合自由能](@keyword=gibbs_energy_of_mixing|lang=zh-CN|style=Feynman)的完整表达式 [@problem_id:2002490]：
$$ \Delta G_{mix, m} = \Delta H_{mix, m} - T\Delta S_{mix, m} = \Omega x_A x_B + RT(x_A \ln x_A + x_B \ln x_B) $$

这个方程是理解[非理想溶液](@keyword=non_ideal_solutions|lang=zh-CN|style=Feynman)行为的核心。它包含两项：一项是代表能量效应的**焓项** ($\Omega x_A x_B$)，另一项是代表无序效应的**熵项** ($-T\Delta S_{mix, m}$)。这两项的相互竞争，决定了混合物的最终行为。

### 相稳定性与互溶间隙

对于[正规溶液](@keyword=regular_solution|lang=zh-CN|style=Feynman)，混合是否自发以及混合物是否稳定，取决于焓项和熵项的相对大小。

#### 焓与熵的竞争

[吉布斯混合自由能](@keyword=gibbs_energy_of_mixing|lang=zh-CN|style=Feynman)对温度的依赖关系可以通过[吉布斯-亥姆霍兹方程](@keyword=gibbs_helmholtz_equation|lang=zh-CN|style=Feynman)得到 [@problem_id:2012877]：
$$ \left(\frac{\partial \Delta G_{mix}}{\partial T}\right)_{P, x} = -\Delta S_{mix} $$
由于[混合熵](@keyword=mixing_entropy|lang=zh-CN|style=Feynman) $\Delta S_{mix}$ 对于随机混合总是正的，所以 $\Delta G_{mix}$ 随温度升高而降低。这意味着，升高温度总是有利于熵项，从而有利于混合。

当 $\Omega > 0$（吸热混合）时，焓项为正，不利于混合；而熵项 $-T\Delta S_{mix}$ 总是为负，有利于混合。
-   在**高温**下，$-T\Delta S_{mix}$ 项的[绝对值](@keyword=absolute_value|lang=zh-CN|style=Feynman)很大，主导了 $\Delta G_{mix}$，使其为负，因此混合物是均匀稳定的。
-   在**低温**下，$T$ 较小，正的焓项 $\Omega x_A x_B$ 可能在某些组成范围内超过熵项的贡献，导致 $\Delta G_{mix}$ 曲线的形状发生改变，从而引发相分离。

#### 亚稳与不稳：旋节线分解

一个均匀的单[相混合](@keyword=phase_mixing|lang=zh-CN|style=Feynman)物要保持稳定，不仅要求其 $\Delta G_{mix}$ 为负，还要求其对任何微小的组成涨落都是稳定的。这在图形上表现为 $\Delta G_{mix}$ vs. $x_A$ 曲线必须是向上凹的。其数学条件是[吉布斯混合自由能](@keyword=gibbs_energy_of_mixing|lang=zh-CN|style=Feynman)对组成的[二阶导数](@keyword=second_derivative|lang=zh-CN|style=Feynman)大于零：
$$ \frac{d^2\Delta G_{mix}}{dx_A^2} > 0 $$

当系统条件（如温度）变化，使得曲线在某些区域变为向下凹（$\frac{d^2\Delta G_{mix}}{dx_A^2}  0$）时，该区域内的均相就变得**不稳定 (unstable)**，会通过**旋节线分解 (spinodal decomposition)** 自发地分离成两个不同的相。不稳定区与稳定区之间的边界被称为**旋节线 (spinodal curve)**，其定义为 [@problem_id:2025785]：
$$ \frac{d^2\Delta G_{mix}}{dx_A^2} = 0 $$

对于[正规溶液模型](@keyword=regular_solution_model|lang=zh-CN|style=Feynman)，该条件给出：
$$ \frac{RT}{x_A(1-x_A)} - 2\Omega = 0 $$

#### [上临界溶解温度](@keyword=upper_critical_solution_temperature|lang=zh-CN|style=Feynman) (Upper Critical Solution Temperature, UCST)

上式可以解出温度 $T$ 作为组成 $x_A$ 的函数，该函数描绘了[相图](@keyword=phase_portrait|lang=zh-CN|style=Feynman)上的旋节线。这条线的最高点被称为**[上临界溶解温度](@keyword=upper_critical_solution_temperature|lang=zh-CN|style=Feynman) (Upper Critical Solution Temperature, UCST)**，记为 $T_c$。通过数学分析可以发现，这个最高点出现在 $x_A=0.5$ 的对称组成处，其温度为 [@problem_id:2025785]：
$$ T_c = \frac{\Omega}{2R} $$

在 $T > T_c$ 时，$\Delta G_{mix}$ 曲线在所有组成范围内都是向上凹的，两种组分完全互溶。在 $T  T_c$ 时，$\Delta G_{mix}$ 曲线中间部分会向下凹，出现一个**互溶间隙 (miscibility gap)**。对于一个总组成落在此间隙内的混合物，它将不再稳定。

#### 两相平衡与[公切线构造](@keyword=common_tangent_construction_2|lang=zh-CN|style=Feynman)

当一个总组成位于互溶间隙内的混合物达到平衡时，它会分离成两个具有确定组成的液相（或固相），我们称之为 $\alpha$ 相和 $\beta$ 相。这两个平衡相的组成，可以通过在 $\Delta G_{mix}$ 曲线上做**[公切线构造](@keyword=common_tangent_construction_2|lang=zh-CN|style=Feynman) (common tangent construction)** 来确定 [@problem_id:2025787]。

公[切线](@keyword=tangent_line|lang=zh-CN|style=Feynman)的物理意义是，[切点](@keyword=point_of_tangency|lang=zh-CN|style=Feynman)所对应的两个相 $(\alpha, \beta)$ 中，组分A的化学势彼此相等 ($\mu_A^\alpha = \mu_A^\beta$)，同时组分B的化学势也彼此相等 ($\mu_B^\alpha = \mu_B^\beta$)。这是[多相平衡](@keyword=heterogeneous_equilibrium|lang=zh-CN|style=Feynman)的基本[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)条件。在 $\Delta G_{mix}$ 图上，公[切线](@keyword=tangent_line|lang=zh-CN|style=Feynman)与曲线相切的两个点的横坐标，$x_A^\alpha$ 和 $x_A^\beta$，就代表了在该温度下共存的两相的平衡组成。例如，对于一个在 $300 \, \text{K}$ 时 $\Omega = 6500 \, \text{J/mol}$ 的体系，通过求解化学势相等的条件，可以精确计算出共存两相的组成为 $x_A=0.123$ 和 $x_A=0.877$ [@problem_id:2025787]。

所有这些平衡组成点 $(T, x_A)$ 构成的边界线称为**[双节线](@keyword=binodal_curve|lang=zh-CN|style=Feynman) (binodal curve)** 或[溶解度](@keyword=solubility|lang=zh-CN|style=Feynman)曲线，它包围着两[相共存](@keyword=phase_coexistence|lang=zh-CN|style=Feynman)的区域。

### 高级主题：下[临界溶解温度](@keyword=critical_solution_temperature|lang=zh-CN|style=Feynman) (LCST)

[正规溶液模型](@keyword=regular_solution_model|lang=zh-CN|style=Feynman)成功地解释了许多体系“加热促溶”的 UCST 行为。然而，自然界中也存在一类与之相反的奇特现象：某些液体对在低温下完全互溶，加热到一定温度后反而会发生相分离。这种行为的特征温度被称为**下[临界溶解温度](@keyword=critical_solution_temperature|lang=zh-CN|style=Feynman) (Lower Critical Solution Temperature, LCST)**。典型的例子是水和一些聚合物（如聚环氧乙烷）或有机胺的混合物。

#### 特殊相互作用的熵-焓效应

LCST 现象无法用简单的[正规溶液模型](@keyword=regular_solution_model|lang=zh-CN|style=Feynman)（其中 $\Omega$ 为正且不依赖于温度）来解释。其根源在于混合物中存在着强烈的、具有[方向性](@keyword=directivity|lang=zh-CN|style=Feynman)的**特殊相互作用**，例如[氢键](@keyword=hydrogen_bonding|lang=zh-CN|style=Feynman) [@problem_id:2025810]。

在这种体系中，混合过程往往是**放热的 ($\Delta H_{mix}  0$)**。例如，水分子和另一种分子的极性基团之间形成新的[氢键](@keyword=hydrogen_bonding|lang=zh-CN|style=Feynman)，会释放能量。从焓的角度看，这有利于混合。然而，这些新形成的、有序的[氢键](@keyword=hydrogen_bonding|lang=zh-CN|style=Feynman)结构（如[溶剂笼](@keyword=solvent_cage|lang=zh-CN|style=Feynman)）会束缚分子的运动，使得系统的**熵**相比于随机混合状态大大降低。这个额外的熵减小量，被称为**[超额熵](@keyword=excess_entropy|lang=zh-CN|style=Feynman) ($\Delta S_{mix}^E$)**，其值为负且[绝对值](@keyword=absolute_value|lang=zh-CN|style=Feynman)很大。

因此，总的[吉布斯混合自由能](@keyword=gibbs_energy_of_mixing|lang=zh-CN|style=Feynman)可以写成：
$$ \Delta G_{mix} = \Delta H_{mix} - T(\Delta S_{ideal} + \Delta S_{mix}^E) $$
在这里，$\Delta H_{mix}$ 和 $\Delta S_{mix}^E$ 都是负值。

#### LCST的[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)模型与计算

这种行为的[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)竞争关系如下：
-   在**低温**下，焓项 $\Delta H_{mix}$ (负值) 占主导，使得 $\Delta G_{mix}$ 为负，体系均匀混合。
-   在**高温**下，熵项中的 $-T\Delta S_{mix}^E$ (其中 $\Delta S_{mix}^E$ 为负) 变为一个大的正值，它会压倒有利的焓项和[理想混合](@keyword=ideal_mixing|lang=zh-CN|style=Feynman)熵项，最终导致 $\Delta G_{mix}$ 曲线出现向下凹的区域，引发相分离。

为了模拟这种行为，我们可以让相互作用参数 $\Omega$ 依赖于温度，例如写成 $\Omega(T) = H_p - T S_p$，其中 $H_p$ 代表与特殊相互作用相关的焓参数（通常为负），$S_p$ 代表相关的非[组合熵](@keyword=combinatorial_entropy|lang=zh-CN|style=Feynman)参数（通常也为负）[@problem_id:2025810]。此时[吉布斯混合自由能](@keyword=gibbs_energy_of_mixing|lang=zh-CN|style=Feynman)为：
$$ \Delta G_{mix} = x_A x_B (H_p - T S_p) + RT(x_A \ln x_A + x_B \ln x_B) $$

同样应用相稳定性的判据 $\frac{d^2\Delta G_{mix}}{dx_A^2} = 0$，并在[对称点](@keyword=point_of_symmetry|lang=zh-CN|style=Feynman) $x_A = 0.5$ 处求解，我们可以得到 LCST 的表达式：
$$ T_c = \frac{H_p}{S_p + 2R} $$

利用给定的参数，如 $H_p = -13.50 \, \text{kJ/mol}$ 和 $S_p = -50.00 \, \mathrm{J/(mol\cdot K)}$，可以计算出该体系的 LCST 约为 $131 \, ^{\circ}\text{C}$ [@problem_id:2025810]。这个结果清晰地展示了，通过对[正规溶液模型](@keyword=regular_solution_model|lang=zh-CN|style=Feynman)进行合理的扩展，使其包含与特殊相互作用相关的焓和熵效应，我们能够定量地理解和预测如 LCST 这样更为复杂的[相行为](@keyword=phase_behavior|lang=zh-CN|style=Feynman)。