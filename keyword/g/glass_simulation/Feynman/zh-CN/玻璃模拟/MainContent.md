## 引言
虽然晶体完美的重[复晶格](@keyword=complex_lattice|lang=zh-CN|style=Feynman)为固体提供了一个优美而简单的模型，但物质世界的大部分却以一种更为混乱的状态存在：[非晶态固体](@keyword=amorphous_solids|lang=zh-CN|style=Feynman)，即玻璃。这些材料，从窗玻璃到先进的金属合金，都缺乏[长程有序](@keyword=long_range_order|lang=zh-CN|style=Feynman)，而正是[长程有序](@keyword=long_range_order|lang=zh-CN|style=Feynman)使得晶体如此易于进行理论分析。这就提出了一个根本性的挑战：我们如何科学地描述、预测和设计[原子结构](@keyword=atomic_structure|lang=zh-CN|style=Feynman)本质上是无序的材料？本文旨在作为玻璃[模拟计算](@keyword=analog_computing|lang=zh-CN|style=Feynman)世界的指南，这是一种探索这一复杂领域的强大方法。第一部分“原理与机制”将深入探讨玻璃的统计和动态定义，探索玻璃化转变的本质以及模拟这些缓慢、冻结系统时固有的计算困境。接下来，“应用与跨学科联系”部分将展示这些模拟的应用，从设计新材料、解释实验数据，到理解古代文物中的量子效应以及“玻璃态”在整个[物理学中的普适性](@keyword=universality_in_physics|lang=zh-CN|style=Feynman)。

## 原理与机制

要理解什么是玻璃，也许最简单的方法是首先理解它不是什么。想象一个最完美、最理想形式的固体：晶体。在你的脑海中，想象一个巨大的三维原子网格，一支纪律严明的军队，士兵们排成完美的行列，延伸至无穷远。如果你知道一个士兵的位置和行进命令——[晶格矢量](@keyword=lattice_vectors|lang=zh-CN|style=Feynman)——你就知道军队中每一个其他士兵的位置。这就是**长程有序**和**[平移对称性](@keyword=translational_symmetry|lang=zh-CN|style=Feynman)**的本质。这种完美的周期性是物理学家的梦想。这意味着我们可以使用强大的对称性数学工具，如[傅里叶分析](@keyword=fourier_analysis|lang=zh-CN|style=Feynman)，来一次性求解数万亿个原子的集体行为。例如，[晶格](@keyword=crystalline_lattice|lang=zh-CN|style=Feynman)的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)可以被清晰地描述为一组定义明确的波，即**[声子](@keyword=phonon|lang=zh-CN|style=Feynman)**，每个[声子](@keyword=phonon|lang=zh-CN|style=Feynman)都由一个[波矢](@keyword=wavevector|lang=zh-CN|style=Feynman) $\mathbf{k}$ 标记，就像一架调音完美的钢琴的音符一样 [@problem_id:3259378]。

玻璃则完全相反。它不是一支整装待发的军队，而是在一个熙熙攘攘的集市上的人群，突然间被瞬间冻结。人们紧密地挤在一起，每个人都有自己的近邻，但没有总体的模式。朝一个方向走十英尺，景象就不同了。没有重复的晶胞，没有可以把你从一个相同的环境传送到另一个环境的[晶格矢量](@keyword=lattice_vectors|lang=zh-CN|style=Feynman)。这是一种**非晶无序**的状态。它具有**[短程有序](@keyword=short_range_order|lang=zh-CN|style=Feynman)**——原子和人一样，不能相互重叠，并且与最近的邻居有偏好的距离——但它完全缺乏晶体的长程有序。

作为科学家，我们如何描述这样一团乱麻？我们求助于统计学的语言。

### 无序的剖析

我们不再问“每个原子在哪里？”，而是问：“如果我站在一个原子上，在距离 $r$ 处其他原子的平均密度是多少？” 答案由一个优美的函数给出，称为**对关联函数**，或 $g(r)$。对于一个完美的晶体，$g(r)$ 将是一系列无限尖锐的峰，对应于精确[晶格](@keyword=crystalline_lattice|lang=zh-CN|style=Feynman)距离上分立的邻居壳层。对于液体，它显示出最近邻的突出第一峰，随后是一系列更小、更宽的鼓包，这些鼓包很快消失，直到在远距离处 $g(r)$ 变得平坦，趋近于1，表明原子完全不相关，就像在随机气体中一样 [@problem_id:2463798]。

玻璃作为一种冻结的液体，其 $g(r)$ 看起来很像液体，但有一个能说明问题的转折。因为原子被更刚性地锁定在原位，所以峰比在热液体中更尖锐、更清晰。在许多简单的玻璃中，出现了一个显著的特征：在液体中是单个宽鼓包的第二个峰，在玻璃化时通常会分裂成两个不同的子峰 [@problem_id:2463798]。这种微妙的分裂是原子受挫局域堆积的指纹，是一个结构特征，告诉我们我们正在观察的不再是流体，而是[非晶态固体](@keyword=amorphous_solids|lang=zh-CN|style=Feynman)。

我们也可以在“[倒易空间](@keyword=reciprocal_space_2|lang=zh-CN|style=Feynman)”中观察这种结构，就像[X射线](@keyword=x_ray|lang=zh-CN|style=Feynman)或中子束那样。这给了我们**[静态结构因子](@keyword=static_structure_factor|lang=zh-CN|style=Feynman)**，$S(k)$，它本质上是原子位置的[傅里叶变换](@keyword=fourier_transform|lang=zh-CN|style=Feynman)。对于晶体，其完美的周期性产生了一个由尖锐、明亮的斑点——**布拉格峰**——组成的图案，这是长程有序的明确标志。对于玻璃，我们只看到宽阔、弥散的环或“晕”，这是其[短程有序](@keyword=short_range_order|lang=zh-CN|style=Feynman)的回声，但也是其缺乏周期性的明确证明 [@problem_id:3259378]。因此，玻璃的模拟是一次数值旅程，进入一个没有晶体简化对称性的世界，一个我们只能通过统计方法，一次一个原子地探索的世界。

### 大减速：液体如何变成玻璃

那么，我们如何制造玻璃呢？我们不是一个原子一个原子地构建它；我们诱使液体变成玻璃。这个过程称为**淬火**——将液体快速冷却，使其原子没有时间找到它们应有的、有序的晶体位置。它们被卡住了。

想象一下，一场音乐会后，一群人试图通过几个狭窄的门离开体育场。在高温（高能量）下，每个人都移动得很快且随机，通过门的流量是稳定的。这是液体状态。随着温度下降，人们移动得更加迟缓。他们需要更长的时间才能挪过邻居，找到通往出口的路径。在某个点，随着密度增加和移动减慢，人群就堵塞了。每个人都被邻居困住，只能在原地挪动，但无法朝着门口取得任何显著进展。人群已经“玻璃化”了。

这个堵塞点就是**[玻璃化转变温度](@keyword=glass_transition_temperature|lang=zh-CN|style=Feynman)**，或 $T_g$。在模拟和实验中，我们可以清楚地发现它。当我们冷却液体时，其体积或势能等性质以平滑、线性的方式减少。但就在 $T_g$ 处，斜率突然改变 [@problem_id:1760070] [@problem_id:1307761]。材料变得更硬，对温度变化的响应更小，因为它的大部分原子运动已被冻结。

这是最引人入胜的部分：对于给定的材料，$T_g$ 的值不是一个固定的、普适的常数。它取决于你的冷却速度！如果你更慢地冷却液体，你就给了原子更多的时间来重新[排列](@keyword=permutation|lang=zh-CN|style=Feynman)和挤过通往出口的道路。系统可以在更低的温度下保持流体状态，然后才最终堵塞。较慢的冷却速率会导致较低的玻璃化转变温度 [@problem_id:1317695]。这种对**冷却速率**的依赖性是最终的证明，表明[玻璃化转变](@keyword=glass_transition|lang=zh-CN|style=Feynman)不是像[凝固](@keyword=solidification|lang=zh-CN|style=Feynman)或沸腾那样的真正[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)[相变](@keyword=phase_change|lang=zh-CN|style=Feynman)，而是一种**动力学现象**。玻璃是一种脱离了平衡的物质。

### [凝固](@keyword=solidification|lang=zh-CN|style=Feynman)于时间的舞蹈：动力学与[结构冻结](@keyword=structural_arrest|lang=zh-CN|style=Feynman)

要真正欣赏玻璃态，我们必须观察原子的舞蹈。在计算机模拟中，我们可以追踪每一个粒子的运动。一个强大的工具是**[均方位移](@keyword=mean_squared_displacement_2|lang=zh-CN|style=Feynman)**（MSD），它测量粒子在时间 $t$ 内从其起始点移动的平均平方距离。

在液体中，一个原子不断地与它的邻居挤来挤去，但最终它会挣脱并漫游开去。平均而言，MSD随时间线性增长：$\text{MSD}(t) \propto t$。这是**[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)**的标志，是表征流体状态的粒子[随机行走](@keyword=random_walk|lang=zh-CN|style=Feynman)。

现在，让我们看看当我们将液体冷却成玻璃态时会发生什么 [@problem_id:1876715]。在非常短的时间内，粒子只是来回[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，被其近邻推拉。这种初始运动在液体或固体中是相同的。但在玻璃中，发生了新的事情。粒子被长时间困住。它的邻居在它周围形成了一个“笼子”，阻止它逃逸。在MSD对时间的图上，这种被困表现为一个长平台。粒子在笼子内嘎嘎作响，但其位移不增长。它被冻结了。

这种现象被称为**[笼蔽效应](@keyword=caging_effect|lang=zh-CN|style=Feynman)**。如果系统是真正的、理想的玻璃，粒子将永远被困住，MSD将停留在这个平台上。平台的高度告诉我们笼子的大小。如果系统是一个非常冷的、粘稠的、刚好在 $T_g$ 以上的[过冷液体](@keyword=supercooled_liquids|lang=zh-CN|style=Feynman)，粒子最终会在很长一段时间后，随着其邻居的缓慢重排而设法逃离其笼子。这次逃逸是[结构弛豫](@keyword=structural_relaxation|lang=zh-CN|style=Feynman)的基本步骤。逃逸所需的平均时间是**[结构弛豫](@keyword=structural_relaxation|lang=zh-CN|style=Feynman)时间**，$\tau_{relax}$。当我们从上方接近玻璃化转变温度时，这个弛豫时间会急剧增加，温度仅下降一点，[弛豫时间](@keyword=relaxation_times|lang=zh-CN|style=Feynman)就会增加许多[数量级](@keyword=order_of_magnitude|lang=zh-CN|style=Feynman)。这就是微观层面上的“大减速”。当这个弛豫时间变得比我们愿意等待的时间更长时，玻璃就形成了。

### 液态过往的记忆：虚构温度与[有效温度](@keyword=effective_temperature|lang=zh-CN|style=Feynman)

室温下的玻璃是一种奇怪的东西。它是一种固体，但其无序结构与平衡晶体不同。它处于非平衡状态，是液体在时间中冻结的一个快照。但这是哪个时刻的快照呢？

这个问题引出了一个优雅的概念——**虚构温度**，$T_f$ [@problem_id:1332211]。玻璃的虚构温度是指，如果其结构与玻璃当前结构相同，该[液体结构](@keyword=structure_of_liquids|lang=zh-CN|style=Feynman)会处于平衡状态的温度。简而言之，你桌上的一块玻璃并不具有20°C下平衡固体的原子[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。相反，它具有在更高温度下（比如500°C）冻结的、混乱的[液体结构](@keyword=structure_of_liquids|lang=zh-CN|style=Feynman)。那个500°C就是它的虚构温度。这是它诞生时炽热液态的记忆。通过较慢冷却生产的玻璃可以在冻结前弛豫到能量更低的类液态，因此其虚构温度会更低。

我们可以将这个想法推向更深层次。在平衡系统中，系统自身的涨落方式与其对外部扰动的响应方式之间存在着美妙的联系——这种关系被称为**涨落-耗散定理**。在非平衡的玻璃中，这种关系被打破了。原子在其笼中自发[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)的方式（涨落）不再与你推它时它屈服的方式（响应）完全一致。

令人惊讶的是，我们可以量化这种破裂。通常会发现，系统涨落时仿佛处于一个温度，而响应时仿佛处于另一个温度！我们可以根据响应与涨落的比率定义一个**[有效温度](@keyword=effective_temperature|lang=zh-CN|style=Feynman)**，$T_{eff}$ [@problem_id:3452637]。对于一个正在[老化](@keyword=burn_in|lang=zh-CN|style=Feynman)的玻璃，这个 $T_{eff}$ 通常高于它所在的室温。就好像系统被困在其高能量、无序的状态中，仍在试图以它曾经作为热液体时的活力来探索其局域能量景观。这个“[有效温度](@keyword=effective_temperature|lang=zh-CN|style=Feynman)”是衡量系统偏离平衡多远的深刻度量，是其热历史的动态回声。

### 模拟者的困境：可能性的艺术

模拟玻璃推动了计算的边界，这主要是因为所涉及的时间尺度范围极其巨大。原子[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)发生在飞秒（$10^{-15}$ s）的尺度上。我们模拟的积分**时间步长** $\Delta t$ 必须更小才能精确捕捉这种运动 [@problem_id:2452082]。过大的时间步长会引入[数值误差](@keyword=numerical_errors|lang=zh-CN|style=Feynman)，人为地阻碍系统的弛豫，使其看起来在比应有温度更高的温度下[玻璃化](@keyword=vitrification|lang=zh-CN|style=Feynman)。

然而，我们想要在 $T_g$ 附近研究的[结构弛豫](@keyword=structural_relaxation|lang=zh-CN|style=Feynman)可能需要微秒、毫秒、秒，甚至更长得多的时间。用飞秒的时间步长模拟一秒的物理时间将需要 $10^{15}$ 次计算步骤——这项任务远超地球上任何计算机的能力。

这导致了模拟者的核心困境：准确性与时间之间的权衡 [@problem_id:2452835]。我们可以构建极其精确的[原子间作用力](@keyword=forces_on_atoms|lang=zh-CN|style=Feynman)模型，甚至使用量子力学（[第一性原理分子动力学](@keyword=ab_initio_molecular_dynamics|lang=zh-CN|style=Feynman)）。但这些模型的计算成本极其高昂。或者，我们可以使用更简单、更便宜的“固定[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)”[力场](@keyword=force_field|lang=zh-CN|style=Feynman)。它们不太准确，但速度快。

对于玻璃模拟，选择是明确的。主要挑战是达到有趣物理现象发生的长时间尺度。一个运行时间仅为几纳秒的极其精确的模拟，如果弛豫时间是微秒，那是毫无用处的。它只会看到原子在笼子里[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。一个不太准确但速度更快，能够运行足够长时间以观察到粒子逃离笼子并流动的模型，其价值要大得多。玻璃模拟的艺术在于选择一个“足够好”以捕捉基本物理特性，但又“足够便宜”以让我们跨越巨大的时间鸿沟的模型，从而让我们能够见证液体凝固成固体，却永远不会成为晶体的缓慢、微妙而美丽的舞蹈。

