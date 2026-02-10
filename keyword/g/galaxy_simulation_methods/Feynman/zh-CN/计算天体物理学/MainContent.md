## 引言
[模拟宇宙](@keyword=simulating_the_universe|lang=zh-CN|style=Feynman)是现代科学的宏大挑战之一。我们如何将基本物理定律转化为一个能正常运行、不断演化的星系模型，其中包含数十亿颗恒星、广阔的气体云和神秘的暗物质支架？这些数字宇宙不仅仅是计算练习；它们是理解我们在宇宙中位置的不可或缺的实验室，弥合了抽象理论与望远镜带来的丰富数据之间的鸿沟。然而，所涉及的尺度范围之广和复杂性之高构成了一个巨大的障碍，使得直接的第一性原理模拟成为不可能。本文深入探讨了使星系模拟成为可能的巧妙方法。我们将首先在 **原理与机制** 部分探讨核心的计算挑战及其解决方案，重点是[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)与气体动力学的建模。随后，我们将进入多样化的 **应用与跨学科联系** 部分，探索这些模拟如何被用于创建模拟宇宙、检验[宇宙学模型](@keyword=cosmology_models|lang=zh-CN|style=Feynman)，并开创新的科学研究方式。

## 原理与机制

模拟一个星系是一项大胆的尝试：在盒子里构建一个宇宙。想象一下这项任务。你必须精心编排数十亿颗恒星和看不见的暗物[质粒](@keyword=plasmid|lang=zh-CN|style=Feynman)子的[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)华尔兹。你必须捕捉星际气体的[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)生命——广阔的气体云坍缩形成新恒星，然后这些恒星爆炸，用新元素丰富宇宙。我们怎么可能希望在计算机中捕捉到这种宏伟的复杂性？答案不在于蛮力，而在于一系列极其巧妙的原理和机制，这是物理学家近似艺术的证明。

### 两种宇宙流体

我们的虚拟星系由两种根本不同的物质构成。首先是恒星和神秘的暗物质。在星系的巨大尺度上，这些物体很少（如果曾经有过的话）会真正碰撞。它们就像彼此穿过的幽灵，仅通过它们集体的、长程而温和的[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)相互作用。我们称之为一个 **无碰撞** 组分。它们的行为由在位置和速度的六维空间中平滑流动的舞蹈所支配。

然后是气体，即星际介质。它是一种真正的流体，一个 **有碰撞** 组分。气体原子和分子不断相互碰撞。这产生了可以抵抗[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)的压力。气体可以被加热，可以冷却，并且可以以超音速相互撞击，形成壮观的激波。与恒星宁静的华尔兹相比，它是一种远为狂暴和复杂的野兽。[@problem_id:3505149]

这种根本性的划分——无碰撞与有碰撞之间的划分——定义了星系模拟的两大挑战。

### [引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)之舞：驯服无限计算

让我们首先考虑无碰撞组分：恒星和暗物质。它们遵循的唯一规则是[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)。牛顿定律很简单：每个粒子都吸引其他所有粒子。但这种简单性背后隐藏着一个巨大的计算问题。如果你有 $N$ 个粒子，要计算其中一个粒子受到的力，你必须将其他 $N-1$ 个粒子的拉力相加。要对 *所有* $N$ 个粒子都这样做，大约需要 $N \times N$，即 $N^2$ 次计算。

一个中等规模的模拟可能有一百万（$10^6$）个粒子。$N^2$ 将是万亿（$10^{12}$）次计算 *每个时间步*。一个拥有十亿（$10^9$）个粒子的现代模拟将需要难以想象的 $10^{18}$ 次计算。这就是 **$N^2$ 问题**，它使得直接模拟成为不可能。我们必须更聪明一些。

关键的洞见是[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)随距离减弱。一个非常遥远的星团的[合力](@keyword=net_force|lang=zh-CN|style=Feynman)，与位于该星团[质心](@keyword=centroid|lang=zh-CN|style=Feynman)的一个单一、大质量伪粒子的[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)几乎无法区分。想象一下在夜晚看一个遥远的城市；你看到的不是单个的路灯，而是一个单一的、集体的光晕。

这就是 **分层树方法** 背后的原理。像 Barnes-Hut 算法这样的算法构建了一个虚拟的[数据结构](@keyword=data_structures|lang=zh-CN|style=Feynman)，一个“[八叉树](@keyword=octree|lang=zh-CN|style=Feynman)”，它递归地将模拟立方体划分为八个更小的立方体。为了计算一个粒子上的力，代码会“遍历”这棵树。如果它遇到了一个与它的距离相比足够小的遥远立方体（树中的一个“节点”），它就使用简单的单极近似——那个集体的光晕。如果立方体太近，代码就会“打开”它，并查看其更小的组成立方体。这个巧妙的技巧将计算成本从不可能的 $O(N^2)$ 降低到可控的 $O(N \log N)$。[@problem_id:3215910]

还存在其他方法，比如 **粒子-网格（PM）** 方案，它将[质量分布](@keyword=mass_distribution|lang=zh-CN|style=Feynman)到一个网格上，并使用强大的快速傅里叶变换（FFT）一次性求解各处的[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)。这对于捕捉大尺度的、平滑的[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)分量非常高效，但无法捕捉近距离接触的精细细节。最先进的解决方案通常是混合的 **Tree-PM** 方法，它使用 PM 方法处理长程力，使用树方法处理短程、精细的相互作用，从而兼得两者的优点。[@problem_id:3505150]

然而，还有另一个微妙之处。我们的模拟“粒子”不是单个恒星；它们是“宏观粒子”，每个代表成千上万或数百万颗真实恒星。如果两个这样的庞然大物偶然相遇并彼此非常靠近，会发生什么？真实的 $1/r^2$ 力定律会导致一个巨大的、剧烈的加速度，将它们以一种两个由数百万颗恒星组成的弥散云团绝不会有的方式散射开。这种人为的散射被称为 **双体弛豫**，它会破坏我们模拟一个平滑、[无碰撞系统](@keyword=collisionless_systems|lang=zh-CN|style=Feynman)的尝试。

解决方案是另一个优美的物理推理：**[引力软化](@keyword=gravitational_softening|lang=zh-CN|style=Feynman)**。我们在非常小的距离上稍微改变牛顿定律。我们可能使用像 $-G m_1 m_2 / \sqrt{r^2 + \epsilon^2}$ 这样的势，而不是 $-G m_1 m_2 / r$。这里，$\epsilon$ 是微小的“[软化长度](@keyword=softening_length|lang=zh-CN|style=Feynman)”。对于远大于 $\epsilon$ 的距离 $r$，公式与牛顿定律完全相同。但对于 $r  \epsilon$，势能变得平坦，力不再发散到无穷大。这就像在微观尺度上模糊[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)，以防止我们巨大的宏观粒子发生不真实的刀锋般相遇。这确保了我们的模拟正确地模拟了真实星系的平滑、集体的[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)。[@problem_id:3535179]

### 宇宙漩涡：模拟气体

现在来看气体。它不仅感受[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)；它还会[反作用](@keyword=backreaction|lang=zh-CN|style=Feynman)。它有压力、温度，并遵循复杂的[流体动力学](@keyword=fluid_dynamics|lang=zh-CN|style=Feynman)定律。模拟它主要有两种哲学方法。

第一种是 **拉格朗日** 方法，以 **[光滑粒子流体动力学](@keyword=smoothed_particle_hydrodynamics_2|lang=zh-CN|style=Feynman)（SPH）** 为代表。想象流体是一系列相互作用的“斑点”或粒子，每个都携带固定的质量和诸如温度等其他属性。这些粒子随流而动。这种方法是天然自适应的——气体在哪里聚集，粒子就在哪里聚集，从而自动提高分辨率。因为粒子间的力被构造成完全对称的，SPH 能够完美地守恒动量和角动量。然而，其经典形式在捕捉尖锐激波方面存在困难，并且难以模拟需要流体混合的情况，比如在剪切层上。[@problem_id:3505149] [@problem_id:3475499]

第二种是 **欧拉** 方法，它使用一个网格或 **栅格**。想象一个固定的棋盘覆盖在星系上，你测量气体（密度、速度）流过每个单元格时的属性。这种方法，特别是当使用现代的 **Godunov 型** 格式（在单元格界面求解[黎曼问题](@keyword=riemann_problem|lang=zh-CN|style=Feynman)）时，在捕捉激波和混合方面非常出色。然而，它也有自己的挑战。当一个旋转的气体盘穿过一个固定的笛卡尔网格时，将气体从一个单元格平流到另一个单元格时产生的小[数值误差](@keyword=numerical_errors|lang=zh-CN|style=Feynman)会累积起来，并人为地耗尽其角动量，这对于形成一个真实的星系来说是灾难性的。[@problem_id:3505149]

一个绝妙的折衷方案是 **移动网格有限体积（MMFV）** 方法。在这里，网格不是固定的，而是一个动态的镶嵌（像一个 [Voronoi 图](@keyword=voronoi_diagram|lang=zh-CN|style=Feynman)），其网格点被设计为随局部流体流动而移动。这使得该方法成为准拉格朗日的，极大地减少了[平流](@keyword=advection|lang=zh-CN|style=Feynman)误差并改善了[角动量守恒](@keyword=angular_momentum_conservation|lang=zh-CN|style=Feynman)，同时保留了 Godunov 格式出色的激波捕捉能力。它代表了两种哲学思想的有力融合。[@problem_id:3475499]

所有用于模拟气体动力学的显式方法都受到一个严格的速度限制，即 **[Courant-Friedrichs-Lewy (CFL) 条件](@keyword=courant_friedrichs_lewy_(cfl)_condition|lang=zh-CN|style=Feynman)**。直观地说，它指出模拟的时间步长 $\Delta t$ 必须足够短，以至于信息（如声波或流体本身）没有时间传播超过一个网格单元。最大速度通常是[流体速度](@keyword=fluid_velocity|lang=zh-CN|style=Feynman)加上声速，即 $|v| + c_s$。在星系模拟中，气体可以被激波加热到数百万度（高 $c_s$），或者以极高的速度落入[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)（高 $|v|$），而这一切都由极小的网格单元来解析。这种组合常常迫使时间步长变得非常短，使得气体动力学成为整个模拟的主要计算瓶颈。[@problem_id:2383717]

### 看不见的宇宙：[次网格物理](@keyword=subgrid_physics|lang=zh-CN|style=Feynman)的必要性

在这里，我们触及了现代[计算天体物理学](@keyword=computational_astrophysics|lang=zh-CN|style=Feynman)最深刻的方面之一。无论我们的计算机多么强大，我们都永远无法解析所有事物。一个典型的高分辨率星系模拟可能具有约 50 秒差距的空间分辨率，即单元格大小 $\Delta x$。这是一个巨大的体积，是我们太阳系体积的一百万亿倍以上。一颗恒星、一次超新星爆发、坍缩形成恒星的[分子云](@keyword=molecular_clouds|lang=zh-CN|style=Feynman)核——所有这些都比我们单个最小的网格单元要小得多。

那么，恒星在我们的模拟中是如何形成的呢？如果任其自然，一个分辨率为 50 pc 的模拟永远不会形成一颗恒星。气体云变得对[引力坍缩](@keyword=gravitational_collapse|lang=zh-CN|style=Feynman)不稳定的物理尺度，即 **[金斯长度](@keyword=jeans_length|lang=zh-CN|style=Feynman)**（$\lambda_J$），取决于其温度和密度。对于一个典型的冷而致密的[分子云](@keyword=molecular_clouds|lang=zh-CN|style=Feynman)，[金斯长度](@keyword=jeans_length|lang=zh-CN|style=Feynman)可能只有几秒差距。由于这个尺度远小于我们的网格单元（$\lambda_J \ll \Delta x$），模拟会人为地平滑密度并提供虚假的压力支持，从而阻止物理坍缩的发生。[@problem_id:3491943]

这似乎是一个无法逾越的障碍。但解决方案既务实又强大：**[次网格模型](@keyword=subgrid_models|lang=zh-CN|style=Feynman)**。[次网格模型](@keyword=subgrid_models|lang=zh-CN|style=Feynman)是一个“配方”，一个基于物理的规则，它将我们 *能够* 在一个网格单元中解析的属性与我们知道必须在未解析尺度上发生的物理过程联系起来。

例如，一个 **恒星形成配方** 可能会说：“如果一个单元格中的平均气体密度高于某个阈值，并且气体足够冷，那么就在一个与局部自由落体时间相关的时间尺度内，将该气体的一部分转化为一个‘恒星粒子’。” 这个‘恒星粒子’不是一颗单独的恒星，而是代表由该气体诞生的整个恒星族群。[@problem_id:3491943]

一旦恒星粒子诞生，我们就需要另一个用于 **[恒星反馈](@keyword=stellar_feedback|lang=zh-CN|style=Feynman)** 的[次网格模型](@keyword=subgrid_models|lang=zh-CN|style=Feynman)。我们知道该族群中的[大质量恒星](@keyword=massive_stars|lang=zh-CN|style=Feynman)会以[超新星](@keyword=supernovae|lang=zh-CN|style=Feynman)的形式爆炸。我们无法解析错综复杂的[冲击波](@keyword=blast_wave|lang=zh-CN|style=Feynman)。更糟糕的是，如果我们简单地将超新星的能量（$10^{51}$ 尔格）作为纯热量注入到那个 50 秒差距的致密单元格中，代码的冷却程序会发现这种极热、致密的气体，并在它有机会做任何机械功之前，立即将所有能量辐射掉。这就是臭名昭著的 **过度冷却问题**。

为了解决这个问题，模拟研究者们开发了几种巧妙的反馈配方。一个 **热反馈** 模型可能仍然注入热量，但会暂时禁用该单元格的冷却程序，让热泡有时间膨胀并降低其密度。一个 **动能反馈** 模型则完全绕过热阶段，直接给邻近的气体粒子一个动量“踢”。一个 **机械反馈** 模型更进一步：它使用高分辨率、小尺度模拟的结果来计算一个真实的[超新星遗迹](@keyword=supernova_remnants|lang=zh-CN|style=Feynman)在其[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)阶段结束时 *应该* 具有的总动量，并将该动量直接注入到网格单元中。这些都是近似，都是为了捕捉我们看不见的物理过程的净效应而进行的深思熟虑的尝试。[@problem_id:3537985]

### 现实性的层级

这些将[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)和[流体动力学](@keyword=fluid_dynamics|lang=zh-CN|style=Feynman)与[次网格物理](@keyword=subgrid_physics|lang=zh-CN|style=Feynman)耦合起来的全数值模拟，是我们能构建的最详细的模型。但它们不是唯一的工具。对于不同的问题，我们可以使用不同层次的抽象。在更高层次的抽象上是 **半解析模型（SAMs）**。SAMs 不模拟气体杂乱的[流体动力学](@keyword=fluid_dynamics|lang=zh-CN|style=Feynman)，而是从一个快速的、仅含暗物质的模拟开始，构建宇宙的[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)骨架——一个描述[暗物质晕](@keyword=dark_matter_halos|lang=zh-CN|style=Feynman)如何生长和合并的“[并合](@keyword=coalescence|lang=zh-CN|style=Feynman)树”。然后，它应用一套参数化的解析方程来模拟气体如何在这些晕中冷却、形成星系、转化为恒星，并受到反馈的影响。SAMs 的细节远不如[流体动力学模拟](@keyword=fluid_dynamics_simulation|lang=zh-CN|style=Feynman)，但它们的计算成本低廉，使得天体物理学家能够探索广阔的参数空间，并生成巨大的[模拟星系星表](@keyword=mock_galaxy_catalogs|lang=zh-CN|style=Feynman)，以便与观测进行统计比较。[@problem_id:3486098]

### 成功的衡量标准：分辨率与收敛性

我们如何知道是否可以信任这些具有多层近似的复杂模拟？科学过程的一个关键部分是定义我们的术语和检验我们的结果。在这个领域，我们谈论三种分辨率：
- **空间分辨率**：能够解析流体的最小单元格尺寸（$\Delta x$）或 SPH 平滑长度（$h$）。
- **[质量分辨率](@keyword=mass_resolution|lang=zh-CN|style=Feynman)**：最小粒子元素的质量，它决定了我们能可靠追踪的最轻天体。
- **[时间分辨率](@keyword=temporal_resolution|lang=zh-CN|style=Feynman)**：[积分时间步长](@keyword=integration_time_step|lang=zh-CN|style=Feynman)（$\Delta t$），它必须足够小以满足 CFL 条件和其他物理时间尺度。[@problem_id:3505203]

一个基本的测试是 **收敛性**：如果我们加倍分辨率（从而也加倍计算成本），我们的结果会改变吗？理想情况下，它们不应该改变。如果一个模拟的预测（比如一个星系的总[恒星质量](@keyword=stellar_mass|lang=zh-CN|style=Feynman)）在分辨率增加而 *不改变* 次网格配方的情况下收敛到一个稳定的答案，我们称之为 **强收敛**。这是黄金标准，表明我们的[次网格模型](@keyword=subgrid_models|lang=zh-CN|style=Feynman)在物理上是稳健的。

然而，我们更常发现，为了得到一个与观测相符的一致结果，我们必须在改变分辨率时稍微重新调整我们的次网格参数（如[恒星形成](@keyword=stellar_formation|lang=zh-CN|style=Feynman)效率）。这被称为 **弱收敛**。这是对这些模拟本质的坦诚承认：它们不仅仅是求解第一性原理方程的计算器，而是宇宙的复杂、有效模型，其中已解析物理和参数化物理之间的界线是一个移动的目标。对收敛性的追求是模拟与现实之间的持续对话，推动我们创造出越来越逼真的宇宙画像。[@problem_id:3505203]

