## 引言
在宏观世界中，一杯静置的水或一室平静的空气似乎是稳定和不变的。然而，在微观尺度下，这是一个由无数粒子组成的、永不停歇的混沌世界，它们以惊人的速度进行着复杂的运动。我们日常感知的温度，正是这场微观狂欢激烈程度的宏观体现。这引出了一个根本性的问题：在这片看似无序的混沌背后，是否存在着普适的物理规律？我们能否精确描述在特定温度下，粒子能量和速度的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)，并借此预测物质的行为？

本文旨在系统地回答这些问题，深入剖析[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的基石——[玻尔兹曼统计](@keyword=boltzmann_statistics|lang=zh-CN|style=Feynman)与麦克斯韦-玻尔兹曼分布。我们将带领读者踏上一段从基本原理到前沿应用的探索之旅。
*   在**“原理与机制”**一章中，我们将揭示玻尔兹曼的革命性思想，理解粒子状态概率如何由能量决定，并推导出描述[粒子速率分布](@keyword=particle_speed_distribution|lang=zh-CN|style=Feynman)的麦克斯韦-[玻尔兹曼公式](@keyword=boltzmann_s_formula|lang=zh-CN|style=Feynman)，同时探讨其引出的深刻概念，如熵、[吉布斯佯谬](@keyword=gibbs_paradox|lang=zh-CN|style=Feynman)和[时间之箭](@keyword=arrow_of_time|lang=zh-CN|style=Feynman)。
*   在**“应用与[交叉](@keyword=chiasmata|lang=zh-CN|style=Feynman)学科联系”**一章中，我们将展示这些经典理论如何在现代计算材料科学中焕发新生，成为验证[分子动力学模拟](@keyword=molecular_dynamics_simulations|lang=zh-CN|style=Feynman)、预测材料[热导率](@keyword=thermal_conductivity|lang=zh-CN|style=Feynman)与[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)系数、以及理解[化学反应动力学](@keyword=chemical_reaction_kinetics|lang=zh-CN|style=Feynman)的强大工具。
*   最后，在**“动手实践”**部分，我们提供了一系列精心设计的问题，帮助读者将理论知识转化为解决实际问题的能力。

现在，就让我们戴上那副“微观眼镜”，深入这个由原子与分子构成的狂舞世界，去探寻支配这一切的优雅而深刻的统计法则。

## 原理与机制

想象一下，你正凝视着一杯静置的水，或者房间里看似静止的空气。从宏观上看，一切都平静而稳定。但如果你能戴上一副“微观眼镜”，你将看到一幅截然不同的景象：一个由无数原子和分子组成的、永不停歇的狂舞世界。这些微小粒子以惊人的速度四处飞驰、碰撞、旋转和[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。那么，我们日常感知的“温度”究竟是什么？它不是某个特定分子的属性，而是这场集体狂欢激烈程度的体现。

然而，这场狂欢并非毫无章法。并非所有粒子都以相同的速度运动。有些粒子懒洋洋地晃动，有些则像出膛的子弹一样飞驰。那么，是否存在一个普适的规则，能够描述在给定温度下，粒子速度的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)情况？又是什么样的基本原理，在背[后支配](@keyword=postdominance|lang=zh-CN|style=Feynman)着这片看似混沌的微观世界？答案就隐藏在[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的基石——[玻尔兹曼统计](@keyword=boltzmann_statistics|lang=zh-CN|style=Feynman)与[麦克斯韦-玻尔兹曼分布](@keyword=maxwell_boltzmann_distribution|lang=zh-CN|style=Feynman)之中。

### 玻尔兹曼的宏伟构想：万能钥匙

要理解粒子的行为，我们首先需要一个框架。在[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学中，这个框架被称为**系综 (ensemble)**。想象一个我们感兴趣的系统——比如一块晶体或一盒气体——它并非完全孤立，而是与一个巨大且温度恒定的“热库”接触，可以自由[交换能](@keyword=exchange_energy|lang=zh-CN|style=Feynman)量。这个系统与[热库](@keyword=thermal_reservoir|lang=zh-CN|style=Feynman)的组合，被称为**[正则系综](@keyword=nvt_ensemble|lang=zh-CN|style=Feynman) (canonical ensemble)**，它描述了在一个恒定温度 $T$、体积 $V$ 和粒子数 $N$ 下的系统。[@problem_id:3435462]

现在，关键问题来了：在任何一个瞬间，这个系统处于其无数个可能的**微观状态**（即每个粒子确切的位置和动量构成的特定组合）中的哪一个呢？伟大的物理学家[路德维希·玻尔兹曼](@keyword=ludwig_boltzmann|lang=zh-CN|style=Feynman)给出了一个惊人而简洁的回答。他提出，系统处于能量为 $E_i$ 的特定微观状态 $i$ 的概率 $P_i$ 与一个简单的因子成正比，这个因子就是大名鼎鼎的**[玻尔兹曼因子](@keyword=boltzmann_factor|lang=zh-CN|style=Feynman) (Boltzmann factor)**：

$$
P_i \propto \exp(-\beta E_i)
$$

其中，$\beta = 1/(k_B T)$，$k_B$ 是玻尔兹曼常数，一个连接微观能量与宏观温度的桥梁。这个公式是[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的核心，是解开热现象之谜的万能钥匙。它告诉我们，在[热平衡](@keyword=thermal_equilibrium|lang=zh-CN|style=Feynman)中，能量越高的状态，其出现的概率呈指数级下降。这就像一场宇宙级别的“彩票游戏”，能量越高的“奖券”虽然存在，但“中奖”的几率却微乎其微。

为了将这个正比关系变成等式，我们需要对所有可能的状态进行求和，得到一个归一化常数，即**[配分函数](@keyword=sum_of_states|lang=zh-CN|style=Feynman) (partition function)** $Z = \sum_i \exp(-\beta E_i)$。这个 $Z$ 看似只是一个数学工具，实则蕴含了系统的所有[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)信息，从自由能到熵，一切都可以从它推导出来。

### 从整体到部分：[麦克斯韦-玻尔兹曼分布](@keyword=maxwell_boltzmann_distribution|lang=zh-CN|style=Feynman)的诞生

玻尔兹曼的构想给了我们描述整个系统的方法，但我们更常关心的是单个粒子的行为。如何从整体的[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)中，提炼出单个粒子的速度[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)呢？

这里的关键在于系统[哈密顿量](@keyword=hamiltonian_function|lang=zh-CN|style=Feynman)（即总能量表达式）的结构。对于一团[理想气体](@keyword=perfect_gases|lang=zh-CN|style=Feynman)，其总能量 $H$ 是所有粒子动能的总和（如果存在外场，还包括[势能](@keyword=energy_potential|lang=zh-CN|style=Feynman)）。重要的是，一个粒子的动能 $\frac{\mathbf{p}_i^2}{2m}$ 只取决于它自身的动量 $\mathbf{p}_i$，而与其他粒子的状态无关。物理学家称这种性质为**可分离性 (separability)**。[@problem_id:3435462]

这种可分离性带来了巨大的简化。它意味着，单个粒子的动量（或速度）[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)，可以从总的[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)中独立出来。更令人惊讶的是，即使粒子处于一个复杂的外部[势场](@keyword=potential_fields|lang=zh-CN|style=Feynman) $U(\mathbf{r})$ 中（例如晶体中的原子受到周期性[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)的作用），其速度[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)的**形式**也完全不受这个势场的影响！只要动能和[势能](@keyword=energy_potential|lang=zh-CN|style=Feynman)是可分离的，速度的统计规律就保持不变。这是一个极其深刻且并非显而易见的结论。[@problem_id:3435462]

那么，这个[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)具体是什么样的呢？对于速度的单个分量，比如 $v_x$，其能量是 $\frac{1}{2} m v_x^2$。根据玻尔兹曼因子，其[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)必然正比于 $\exp(-\frac{m v_x^2}{2 k_B T})$。这是一个以零为中心的正态分布（或称高斯分布，“[钟形曲线](@keyword=bell_curve|lang=zh-CN|style=Feynman)”）。$v_y$ 和 $v_z$ 分量也遵循完全相同的规律。

因此，一个粒子具有特定速度矢量 $\mathbf{v} = (v_x, v_y, v_z)$ 的概率，就是一个三维的正态分布。[@problem_id:3435482] 但在很多情况下，我们更关心的是速率 $v = |\mathbf{v}| = \sqrt{v_x^2 + v_y^2 + v_z^2}$，而不关心其方向。要得到速率的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)，我们需要在[速度空间](@keyword=velocity_space|lang=zh-CN|style=Feynman)中思考。所有对应于同一个速率 $v$ 的[速度矢量](@keyword=velocity_vector|lang=zh-CN|style=Feynman)，构成了一个半径为 $v$ 的球面。这个球面的表面积是 $4\pi v^2$。

因此，**[麦克斯韦-玻尔兹曼速率分布](@keyword=maxwell_boltzmann_speed_distribution|lang=zh-CN|style=Feynman) (Maxwell-Boltzmann speed distribution)** $P(v)$ 的最终形式，是两个因素竞争的结果：
1.  **相空间体积因子**：随着速率 $v$ 的增加，可供选择的速度方向越来越多，这个“可能性”的增长与球面积 $4\pi v^2$ 成正比。
2.  **玻尔兹曼能量惩罚因子**：随着速率 $v$ 的增加，动能 $\frac{1}{2}mv^2$ 变大，其概率被玻尔兹曼因子 $\exp(-\frac{mv^2}{2k_BT})$ 指数级地抑制。

综合起来，我们得到：

$$
P(v) = 4\pi \left(\frac{m}{2\pi k_B T}\right)^{3/2} v^2 \exp\left(-\frac{m v^2}{2 k_B T}\right)
$$

这个[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)曲线从零点开始，上升到一个峰值，即**[最概然速率](@keyword=most_probable_speed|lang=zh-CN|style=Feynman) (most probable speed)** $v_{\text{mp}} = \sqrt{\frac{2 k_B T}{m}}$，然后逐渐下降，拖着一条长长的“尾巴”延伸到高能区域。[@problem_id:3435482] 这条尾巴，看似不起眼，却蕴含着驱动世界变化的力量。

### 长尾的力量：驱动世界[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)的引擎

麦克斯韦-玻尔兹曼分布告诉我们，在任何温度下，总有一小部分粒子的能量远高于平均值。它们就是[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)曲线中那条长长的**高能尾 (high-energy tail)** 上的“幸运儿”。尽管数量稀少，但它们的存在是许多物理和化学过程的关键。

一个绝佳的例子是[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)中的[原子扩散](@keyword=atomic_diffusion|lang=zh-CN|style=Feynman)或[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)。想象一个吸附在材料表面的原子，它想到达邻近的一个吸附位，但两者之间存在一个能量壁垒，即**活化能 (activation energy)** $\Delta E^\ddagger$。[@problem_id:3435508] 处于平均能量的原子根本无法“翻越”这座山峰。

谁能完成这个壮举呢？正是那些来自[麦克斯韦-玻尔兹曼分布](@keyword=maxwell_boltzmann_distribution|lang=zh-CN|style=Feynman)高能尾部的粒子。它们偶然获得了足够的动能，足以克服能量壁垒，完成一次成功的“跃迁”。一个反应的速率，本质上正比于找到这样一个高能粒子的概率。根据[玻尔兹曼统计](@keyword=boltzmann_statistics|lang=zh-CN|style=Feynman)，这个概率与 $\exp(-\Delta G^\ddagger / k_B T)$ 成正比（其中 $\Delta G^\ddagger$ 是包含熵效应的[自由能垒](@keyword=free_energy_barrier|lang=zh-CN|style=Feynman)）。这正是化学中著名的阿伦尼乌斯公式的微观起源。[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)的“长尾”虽然稀疏，却是驱动世界[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)和物质输运的真正引擎。[@problem_id:3435508]

### [时间之箭](@keyword=arrow_of_time|lang=zh-CN|style=Feynman)与[稳态](@keyword=steady_states|lang=zh-CN|style=Feynman)

至此，我们描述的都是系统处于热平衡时的“静态”画面。但如果系统一开始不处于平衡态呢？比如，我们向一盒冷气体中注入一束高能粒子。系统将如何演化？直觉告诉我们，通过不断的碰撞，能量会逐渐重新分配，最终整个系统会达到一个新的、均匀的温度。

这个过程可以用**[玻尔兹曼输运方程](@keyword=boltzmann_transport_equation|lang=zh-CN|style=Feynman) (Boltzmann Transport Equation, BTE)** 来精确描述。这个方程刻画了[粒子分布函数](@keyword=particle_distribution_function|lang=zh-CN|style=Feynman) $f(\mathbf{r}, \mathbf{p}, t)$ 如何因粒子的自由运动（流逝项）和相互碰撞（碰撞项）而随[时间演化](@keyword=time_evolution|lang=zh-CN|style=Feynman)。[@problem_id:3435459]

那么，演化的终点是什么？当系统[达到平衡](@keyword=equilibration|lang=zh-CN|style=Feynman)时，[分布函数](@keyword=distribution_function|lang=zh-CN|style=Feynman)将不再随时间改变，即达到一个**[稳态](@keyword=steady_states|lang=zh-CN|style=Feynman) (stationary state)**。在没有外部驱动的情况下，这意味着BTE中的碰撞项必须为零。碰撞项为零的条件是什么？那就是对于任何一种碰撞过程及其逆过程，两者的发生速率必须完全相等。这个条件被称为**细致平衡原理 (principle of detailed balance)**。

玻尔兹曼证明了一个深刻的定理（[H定理](@keyword=h_theorem|lang=zh-CN|style=Feynman)）：唯一能够满足所有可能碰撞的[细致平衡条件](@keyword=detailed_balance_condition|lang=zh-CN|style=Feynman)的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)，就是麦克斯韦-玻尔兹曼分布。换句话说，无论初始状态如何混乱，只要粒子可以自由碰撞[交换能](@keyword=exchange_energy|lang=zh-CN|style=Feynman)量，它们最终的宿命就是达到麦克斯韦-玻尔兹曼分布。这个[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)是[热力学平衡](@keyword=thermodynamic_equilibrium|lang=zh-CN|style=Feynman)的唯一“[不动点](@keyword=fixed_point|lang=zh-CN|style=Feynman)”。它将微观世界的动力学与宏观世界中不可逆的时间之箭，以及[熵增原理](@keyword=principle_of_increasing_entropy|lang=zh-CN|style=Feynman)紧密地联系在了一起。[@problem_id:3435459]

### 数不可数之物：熵与[吉布斯佯谬](@keyword=gibbs_paradox|lang=zh-CN|style=Feynman)

[玻尔兹曼统计](@keyword=boltzmann_statistics|lang=zh-CN|style=Feynman)不仅给出了速度[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)，还为“熵”这一神秘概念提供了坚实的微观基础。玻尔兹曼的墓碑上刻着他最著名的公式：$S = k_B \ln W$，其中 $S$ 是熵，$W$ (或 $\Omega$) 是对应于某一[宏观态](@keyword=macrostates|lang=zh-CN|style=Feynman)的[微观态](@keyword=microstates|lang=zh-CN|style=Feynman)总数。熵是系统无序度的量度，或者说是我们对系统微观状态“无知”程度的量度。

然而，早期经典[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学在应用这一理念时，遇到了一个著名的难题——**[吉布斯佯谬](@keyword=gibbs_paradox|lang=zh-CN|style=Feynman) (Gibbs paradox)**。想象一个被隔板分开的盒子，两边装着**不同**的理想气体，温度和压强相同。抽掉隔板，气体混合，熵增加。这很自然，因为系统变得更无序了。但如果两边装的是**相同**的气体，抽掉隔板后，宏观上什么也没发生，但根据早期理论计算，熵竟然也增加了！[@problem_id:3435464] [@problem_id:3435491]

这个佯谬的根源在于我们对“相同”的理解。在经典世界里，我们可以想象给每个粒子贴上独一无二的标签。但在微观世界，同种类的粒子是**绝对不可区分的 (indistinguishable)**。交换两个电子或两个氧分子的位置，你得到的微观[状态和](@keyword=sum_of_states|lang=zh-CN|style=Feynman)原来是完全同一个状态。经典统计因为错误地将这些不可区分的状态当作不同状态来计数，从而高估了微观状态的数量。

解决方案是在[配分函数](@keyword=sum_of_states|lang=zh-CN|style=Feynman)中引入一个修正因子 $1/N!$，$N$ 是粒子数。这个因子恰好消除了因粒子可标记性而导致的重复计数。引入这个因子后，[熵变](@keyword=entropy_change|lang=zh-CN|style=Feynman)成了一个**广延量 (extensive property)**，即系统的熵恰好等于其各部分熵的总和。[吉布斯佯谬](@keyword=gibbs_paradox|lang=zh-CN|style=Feynman)也迎刃而解：混合相同气体时，计算出的[熵变](@keyword=entropy_change|lang=zh-CN|style=Feynman)为零，与物理现实相符。[@problem_id:3435464] [@problem_id:3435491] 值得注意的是，这个对热力学性质至关重要的修正，并不会改变单个粒子的麦克斯韦-玻尔兹曼速度[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)，因为它处理的是集体计数的宏观问题，而非单粒子动力学。更深层次的探讨还会涉及**遍历性 (ergodicity)** 等概念，它们是连接微观动力学长[时间平均与系综平均](@keyword=time_average_vs_ensemble_average|lang=zh-CN|style=Feynman)的桥梁。[@problem_id:3435455]

### 超越理想：原子的真实世界

麦克斯韦-玻尔兹曼分布是为[理想气体](@keyword=perfect_gases|lang=zh-CN|style=Feynman)——即忽略相互作用的质点——量身定做的。但真实世界中的原子和分子之间既有排斥力（当它们靠得太近时），也有吸[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)（在较远距离上）。这些相互作用如何改变理想气体的行为？

答案可以通过**[维里展开](@keyword=virial_expansion|lang=zh-CN|style=Feynman) (virial expansion)** 来系统地给出。它将真实气体的状态方程（联系压强 $p$、体积 $V$ 和温度 $T$ 的方程）展开成密度的[幂级数](@keyword=power_series|lang=zh-CN|style=Feynman)：

$$
\frac{p}{k_B T} = n + B_2(T) n^2 + B_3(T) n^3 + \cdots
$$

其中 $n=N/V$ 是粒子[数密度](@keyword=number_density|lang=zh-CN|style=Feynman)。第一项 $n$ 就是理想气体定律。而**第二维里系数 (second virial coefficient)** $B_2(T)$ 则是最重要的修正项，它精确地反映了成对粒子间相互作用的影响。[@problem_id:3435501]

$B_2(T)$ 的正负和大小，直观地揭示了相互作用的本质：
-   **排斥力占主导**：粒子像微小的硬球，互相占据空间，形成“[排除体积](@keyword=excluded_volume|lang=zh-CN|style=Feynman)”。这使得粒子活动空间变小，碰撞更频繁，从而使压强**高于**[理想气体](@keyword=perfect_gases|lang=zh-CN|style=Feynman)。这种效应贡献一个正的 $B_2(T)$。[@problem_id:3435466]
-   **吸[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)占主导**：粒子间存在吸[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)，使得它们倾向于短暂地“粘”在一起，形成瞬时二聚体。这会减弱它们对容器壁的冲击，使压强**低于**理想气体。这种效应贡献一个负的 $B_2(T)$。[@problem_id:3435466]

在高温下，粒子的动能足以克服吸[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)，排斥效应占主导，$B_2(T)$ 为正。在低温下，吸[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)变得重要，$B_2(T)$ 可能变为负。存在一个特殊的温度，称为**玻义耳温度 (Boyle temperature)** $T_B$，此时 $B_2(T_B)=0$，吸引和排斥效应恰好相互抵消，真实气体在相当大的密度范围内表现得最像理想气体。[@problem_id:3435466]

### 量子世界中的经典心脏

[玻尔兹曼统计](@keyword=boltzmann_statistics|lang=zh-CN|style=Feynman)和麦克斯韦-玻尔兹曼分布是经典物理的杰作，但它们的影响力一直延伸到现代[计算材料科学](@keyword=computational_materials_science|lang=zh-CN|style=Feynman)的量子世界。在许多**[第一性原理分子动力学](@keyword=ab_initio_molecular_dynamics|lang=zh-CN|style=Feynman) (ab initio molecular dynamics)** 模拟中，虽然我们用量子力学来精确处理电子的行为，但质量大得多的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的运动，通常仍然可以用[牛顿力学](@keyword=newtonian_mechanics|lang=zh-CN|style=Feynman)来描述。

那么，如何在一个模拟开始时，赋予这些[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)符合特定温度的初始运动呢？标准做法就是从麦克斯韦-玻尔兹曼分布中随机抽样，为每个[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)赋予一个初始速度。这是连接理论与实践、启动复杂模拟的关键一步。[@problem_id:3435450]

然而，我们必须始终保持清醒。当温度足够低或[振动频率](@keyword=vibrational_frequencies|lang=zh-CN|style=Feynman)足够高时，原子的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)（在晶体中称为**[声子](@keyword=phonon|lang=zh-CN|style=Feynman) (phonon)**）会显示出其量子本性。它们的能量不再是连续分布的，而是量子化的，其统计规律由**[玻色-爱因斯坦统计](@keyword=bose_einstein_statistics|lang=zh-CN|style=Feynman)**描述，而非经典的[麦克斯韦-玻尔兹曼统计](@keyword=boltzmann_statistics|lang=zh-CN|style=Feynman)。我们可以定义一个修正因子，来衡量系统偏离经典行为的程度，判断量子效应在多大程度上是重要的。[@problem_id:3435450]

这最终揭示了一幅和谐而统一的物理图景：尽管我们的世界在最深层次上是量子的，但源于19世纪的经典[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学思想，仍然为我们理解温度、能量[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)和[热平衡](@keyword=thermal_equilibrium|lang=zh-CN|style=Feynman)提供了强大而优美的语言。[麦克斯韦-玻尔兹曼分布](@keyword=maxwell_boltzmann_distribution|lang=zh-CN|style=Feynman)，作为这套语言的核心词汇，至今仍是我们在原子尺度上思考和模拟物质世界的基石。