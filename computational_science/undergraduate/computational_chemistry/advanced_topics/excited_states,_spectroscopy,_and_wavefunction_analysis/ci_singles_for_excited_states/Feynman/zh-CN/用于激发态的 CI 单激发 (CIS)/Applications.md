## 应用与跨学科连接

现在，我们已经搭建好了我们精美的理论机器 —— [单组态相互作用](@keyword=configuration_interaction_singles|lang=zh-CN|style=Feynman) (CIS) 方法。我们理解了它的构造和工作原理。但是，一位真正的物理学家或化学家绝不会满足于理论本身；我们必须用它来向真实世界提问。这台机器能做些什么呢？它[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)我们去哪里？在本章中，我们将开启一段激动人心的旅程，去探索 CIS 理论在广阔的科学领域中的强大威力与深远影响。你会发现，这个看似简单的想法，如同一把钥匙，能打开从化学、物理到[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)，乃至未来计算科学的大门。

### 光与色的语言：[光谱学](@keyword=spectroscopy|lang=zh-CN|style=Feynman)与[光化学](@keyword=photochemistry|lang=zh-CN|style=Feynman)

我们周围的世界充满了色彩，而这一切都源于分子如何与光相互作用。CIS 最直接、最核心的应用，就是作为翻译，将分子内部电子世界的量子语言，翻译成我们能够观测到的光谱语言 —— 即颜色、[光吸收](@keyword=optical_absorption|lang=zh-CN|style=Feynman)和荧光。

#### 我们是“亮的”还是“暗的”？光的吸收规则

一个分子是否能吸收特定颜色的光，取决于从[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)到某个[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的跃迁是否“被允许”。在量子世界里，“允许”与否由一个称为**跃迁偶极矩** ($\vec{\mu}_{0k}$) 的量决定。它的数值大小直接关系到光谱[谱线](@keyword=spectral_line|lang=zh-CN|style=Feynman)的强度。如果 $\vec{\mu}_{0k}$ 很大，跃迁就很强，我们称之为“亮的” (bright) 跃迁；如果它接近于零，跃迁就很弱或被禁止，我们称之为“暗的” (dark) 跃迁。

CIS 方法的优美之处在于，它为我们提供了一个直接计算[跃迁偶极矩](@keyword=transition_dipole_moment|lang=zh-CN|style=Feynman)的“配方”。它告诉我们，从[基态](@keyword=basis_states|lang=zh-CN|style=Feynman) $|\Psi_0\rangle$ 到一个 CIS [激发态](@keyword=excited_state|lang=zh-CN|style=Feynman) $|\Psi_k\rangle$ 的[跃迁偶极矩](@keyword=transition_dipole_moment|lang=zh-CN|style=Feynman)，本质上是构成这个[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的所有单电子“跳跃”(从占据轨道 $i$ 到虚拟轨道 $a$) 的贡献的总和，并由相应的 CIS 系数 $c_{ia}^k$ 加权 [@problem_id:2452229]：
$$
\vec{\mu}_{0\rightarrow k} = \sqrt{2} \sum_{ia} c_{ia}^k \langle \phi_a | \hat{\boldsymbol{\mu}} | \phi_i \rangle
$$
这里的 $\langle \phi_a | \hat{\boldsymbol{\mu}} | \phi_i \rangle$ 就是单个电子从轨道 $\phi_i$ “跳”到轨道 $\phi_a$ 时所产生的[跃迁偶极矩](@keyword=transition_dipole_moment|lang=zh-CN|style=Feynman)。这个公式是连接理论计算和实验观测的核心桥梁。一旦我们知道了跃迁偶极矩和跃迁能量 $\Delta E_{0k}$，我们甚至可以估算[分子发光](@keyword=molecular_luminescence|lang=zh-CN|style=Feynman)（例如荧光）的速率，即爱因斯坦 $A$ 系数，它与 $|\vec{\mu}_{0k}|^2$ 和 $\Delta E_{0k}^3$ 成正比 [@problem_id:2452213]。这使得我们不仅能预测分子的颜色，还能预测它们的[发光效率](@keyword=luminous_efficacy|lang=zh-CN|style=Feynman)和寿命——这对于设计荧光探针和激光材料至关重要。

#### 重叠的逻辑：为何有些跃迁很微弱？

为什么有些跃迁是亮的，而另一些是暗的呢？上面的公式给了我们数学上的答案，但物理直觉又在哪里？让我们以甲醛分子为例。计算表明，它的最低能量[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)，即 $n \to \pi^*$ 跃迁，具有非常小的吸收强度 [@problem_id:2452245]。

这里的奥秘藏在轨道的“空间地理学”之中。$n$ 轨道是一个[非键轨道](@keyword=non_bonding_orbitals|lang=zh-CN|style=Feynman)，电子云主要蜷缩在氧原子周围。而 $\pi^*$ 轨道是一个[反键轨道](@keyword=antibonding_orbitals|lang=zh-CN|style=Feynman)，它的电子云分布在碳和氧原子上，并且像一个“8”字形，两边的相位是相反的。当我们要计算跃迁偶极矩积分 $\langle \pi^* | \hat{\boldsymbol{r}} | n \rangle$ 时，我们实际上是在考察这两个轨道在空间中“加权”的重叠情况。由于 $n$ 轨道高度定域在氧原子附近，而 $\pi^*$ 轨道在这一区域恰好有一个节点（相位改变的地方），导致积分在空间中的正负贡献几乎完全抵消了。就像你在挖一个坑，同时又把挖出的土填回旁边的另一个坑，最终什么也没发生。这种空间上的正交性和相位的抵消，使得整个跃迁偶"矩"非常小，因此跃迁也就非常“暗”。这个例子美妙地展示了，抽象的量子力学规则如何通过直观的[轨道图](@keyword=orbital_diagrams|lang=zh-CN|style=Feynman)像，与分子的具体化学特性联系起来。

#### 从分析到设计：解密复杂的分子世界

CIS 的威力远不止于简单的有机分子。在[无机化学](@keyword=inorganic_chemistry|lang=zh-CN|style=Feynman)和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)中，过渡金属配合物的光物理性质是研究的核心。这些分子的[电子跃迁](@keyword=electronic_transitions|lang=zh-CN|style=Feynman)类型非常丰富，包括金属中心 ($d-d$) 跃迁 (MC)、配体中心 ($\pi-\pi^*$) 跃迁 (LC) 以及电荷转移 (CT) 跃迁。如何区分它们呢？

CIS 计算就像一台功能强大的分析仪器。通过分析 CIS 计算的输出，我们可以为[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)“画像”[@problem_id:2452228]。一种强大的技术是分析**[自然跃迁轨道](@keyword=natural_transition_orbitals|lang=zh-CN|style=Feynman) (NTO)** [@problem_id:2452205]。一个复杂的激发过程，可能在数学上表现为许许多多 canonical 轨道的跃迁组合。NTO 分析通过一个聪明的数学技巧（[奇异值分解](@keyword=singular_value_decomposition_(svd)|lang=zh-CN|style=Feynman)），将这个复杂的过程提炼成一个简洁明了的故事：一个电子从一个“空穴 (hole)” NTO 跑到了一个“粒子 (particle)” NTO。

这样一来，分类就变得易如反掌 [@problem_id:2452228]：
-   如果空穴和粒子 NTO 都定域在金属上，这就是一个 MC 跃迁。
-   如果它们都定域在配体上，这就是一个 LC 跃迁。
-   如果空穴在金属上，粒子在配体上，这就是一个金属到配体的[电荷转移](@keyword=charge_transfer|lang=zh-CN|style=Feynman) (MLCT) 跃迁。
-   反之，则为[配体到金属的电荷转移](@keyword=ligand_to_metal_charge_transfer|lang=zh-CN|style=Feynman) (LMCT) 跃迁。

这种分析能力使得我们能够理解为什么某些[配合物](@keyword=coordination_compound|lang=zh-CN|style=Feynman)是优良的光敏剂（如 MLCT 态），而另一些则在受激后迅速失活（如 MC 态），为设计新型[太阳能电池](@keyword=solar_cells|lang=zh-CN|style=Feynman)、发光二极管 ([OLED](@keyword=oleds|lang=zh-CN|style=Feynman)) 和[光催化剂](@keyword=photocatalyst|lang=zh-CN|style=Feynman)提供了坚实的理论指导。

### 超越光谱：[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的结构与动力学

CIS 不仅能告诉我们光谱的“长相”，还能帮助我们探索[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)的“地形”，揭示分子在吸收[光子](@keyword=photon|lang=zh-CN|style=Feynman)后可能经历的奇妙旅程。

#### 探索[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)：寻找通往[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的“逃生通道”

分子在[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)不会永远停留。它们最终会通过发光或非辐射过程回到[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。在光化学中，最重要、最迅速的[非辐射衰变](@keyword=non_radiative_decay|lang=zh-CN|style=Feynman)通道之一，就是通过所谓的**[锥形交叉](@keyword=conical_intersections|lang=zh-CN|style=Feynman) (Conical Intersection, CoIn)**。这是一种[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)上的[特殊几何](@keyword=special_geometry|lang=zh-CN|style=Feynman)构型，在这一点上，两个电子态（例如 $S_1$ 和 $S_2$，或 $S_1$ 和 $S_0$）发生简并，就像一个漏斗，为分子提供了一条从高能量[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)快速“泄流”到低能量态的捷径。

寻找这些转瞬即逝的“漏斗”是[光化学](@keyword=photochemistry|lang=zh-CN|style=Feynman)研究的圣杯。借助 CIS 提供的[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)能量和能量梯度（即[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)上的“坡度”），我们可以通过[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)系统地寻找[锥形交叉](@keyword=conical_intersections|lang=zh-CN|style=Feynman)点 [@problem_id:2452190]。一种常见的方法是构造一个目标函数，它同时最小化两个态的[平均能量](@keyword=average_energy|lang=zh-CN|style=Feynman)和它们之间的能量差。通过这种方式，我们能够“迫使”[分子结构](@keyword=molecular_structure|lang=zh-CN|style=Feynman)走向一个既能量较低又满足简并条件的几何构型。这使得 CIS 成为研究[光化学反应](@keyword=photochemical_reactions|lang=zh-CN|style=Feynman)机理、理解光合作用中的[能量传递](@keyword=energy_transfer|lang=zh-CN|style=Feynman)以及设计光开关分子的一个重要理论工具。

#### 不同寻常的态：Rydberg 态与计算的艺术

我们通常关注的[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)，如 $n \to \pi^*$ 或 $\pi \to \pi^*$，被称为**价[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)** (valence states)，因为电子仍然停留在分子的成键区域内。然而，还有一类非常不同的[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)——**Rydberg 态**。在 Rydberg 态中，电子被激发到一个非常“蓬松”、空间范围巨大的轨道上，远离分子核的束缚，就像一颗行星被抛到了太阳系的边缘。

描述 Rydberg 态对计算方法提出了特殊的要求 [@problem_id:2452184]。标准的[基组函数](@keyword=basis_set_functions|lang=zh-CN|style=Feynman)是为描述成键区域的电子而设计的，它们在远离原子核的地方衰减得很快。如果你用这样的[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)去计算 Rydberg 态，就像用砖块去搭建一朵云彩，结果必然是灾难性的。计算出的 Rydberg 态能量会被严重高估，甚至完全无法得到正确的态。为了正确描述这些“弥散”的 Rydberg 轨道，我们必须在[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)中加入所谓的**[弥散函数](@keyword=diffuse_functions|lang=zh-CN|style=Feynman) (diffuse functions)** ——这些函数在空间中衰减得非常缓慢。

这个例子深刻地提醒我们，计算化学不是一个“黑箱”操作。理论方法的成功，离不开对物理现象的深刻理解和对计算工具的正确运用。有趣的是，加入[弥散函数](@keyword=diffuse_functions|lang=zh-CN|style=Feynman)有时会戏剧性地改变[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的能量排序，使得原本能量较高的 Rydberg 态“掉”下来，甚至成为最低[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)。这在解释某些分子的光化学行为时至关重要。

### 物理的统一性：CIS 作为一种普适思想

到目前为止，我们看到的都是 CIS 在分子[电子激发](@keyword=electronic_promotion|lang=zh-CN|style=Feynman)中的应用。但 CIS 背后的核心思想——在一个简单的[参考态](@keyword=reference_state|lang=zh-CN|style=Feynman)基础上，通过混合“单激发”组态来描述系统的真实状态——是一种非常普适的物理思想。它可以被应用到完全不同的物理系统中，揭示出自然界深层次的统一性与和谐之美。

#### 集体激发：材料中的[激子](@keyword=excitons|lang=zh-CN|style=Feynman)

想象一下，我们有两个相同的分子（一个二聚体），它们靠得很近但相互作用很弱。每个分子都可以独立地发生[电子激发](@keyword=electronic_promotion|lang=zh-CN|style=Feynman)。但是，当它们组成一个整体时，一个分子上的激发会“感受”到另一个分子的存在。它们会通过库仑相互作用发生耦合。

在这个体系中，我们可以借鉴 CIS 的思想，将局域在单个分子上的[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)（例如 $|1^*\rangle$ 和 $|2^*\rangle$）作为我们的“单激发”基底。通过求解这个二能级体系的[哈密顿矩阵](@keyword=hamiltonian_matrix|lang=zh-CN|style=Feynman)，我们会发现，系统的本征态不再是局域的 $|1^*\rangle$ 或 $|2^*\rangle$，而是它们的对称和反对称线性组合 [@problem_id:2452227]：
$$
|\Psi_{\pm}\rangle = \frac{1}{\sqrt{2}} (|1^*\rangle \pm |2^*\rangle)
$$
这两个新的态被称为**[激子](@keyword=excitons|lang=zh-CN|style=Feynman)态 (excitonic states)**。它们的能量会发生分裂，并且它们的光学性质（亮或暗）取决于原来两个分子[跃迁偶极矩](@keyword=transition_dipole_moment|lang=zh-CN|style=Feynman)的相对朝向。这种将局域激发耦合形成[离域](@keyword=delocalization|lang=zh-CN|style=Feynman)的集体激发的思想，是凝聚态物理和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)的基石。它解释了光合作用中光能如何高效地在[叶绿素](@keyword=chlorophyll|lang=zh-CN|style=Feynman)分子网络中传递，也指导着我们设计[有机太阳能电池](@keyword=organic_solar_cells|lang=zh-CN|style=Feynman)和 OLED 器件。

#### 原子的舞蹈：[声子](@keyword=phonons|lang=zh-CN|style=Feynman)的类比

CIS 的思想甚至可以超越电子的世界。在一个完美的晶体中，原子的集体[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)可以被量子化，形成一种[准粒子](@keyword=quasiparticles|lang=zh-CN|style=Feynman)，我们称之为**[声子](@keyword=phonons|lang=zh-CN|style=Feynman) (phonon)**。每个[声子](@keyword=phonons|lang=zh-CN|style=Feynman)都对应一个特定的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)模式（正规模），就像分子轨道一样，它们是谐振近似下晶格振动的[本征态](@keyword=eigenstates|lang=zh-CN|style=Feynman)。

我们可以将“没有[声子](@keyword=phonons|lang=zh-CN|style=Feynman)”的[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)看作是我们的“[参考态](@keyword=reference_state|lang=zh-CN|style=Feynman)”，而“包含一个[声子](@keyword=phonons|lang=zh-CN|style=Feynman)”的态看作是“单激发”态。在一个完美的、谐振的晶体中，不同的[声子模式](@keyword=phonon_modes|lang=zh-CN|style=Feynman)之间不会相互作用。但是，如果晶体中存在缺陷，或者我们考虑非谐效应（原子间的相互作用力不是完美的弹簧），这些“完美”的[声子](@keyword=phonons|lang=zh-CN|style=Feynman)态就会发生耦合。

我们可以构建一个类似于 CIS 的模型，称为**[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)[组态相互作用](@keyword=configuration_interaction|lang=zh-CN|style=Feynman) (VCI)**，在这个模型中，[哈密顿矩阵](@keyword=hamiltonian_matrix|lang=zh-CN|style=Feynman)的非对角元就代表了由缺陷或非谐性引起的[声子](@keyword=phonons|lang=zh-CN|style=Feynman)之间的散射 [@problem_id:2452204]。这种类比的美妙之处在于，它揭示了不同物理领域背后共同的数学结构：无论是电子在分子中的激发，还是晶格振动在固体中的传播，处理它们相互作用的基本方法论是相通的。

#### 窥见量子时代：[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)与[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)

最令人兴奋的连接之一，也许是 CIS 与前沿的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的联系。让我们考虑一个最简单的化学系统：两个电子占据一个轨道。它的最低能量单激发（从轨道 $i$ 到 $a$）包含两种可能：激发自旋向上的电子，或激发自旋向下的电子。这构成了一个二维的 CIS 空间。

现在，让我们进行一个大胆的映射：将这两种激发分别对应于一个[双量子比特系统](@keyword=two_qubit_system|lang=zh-CN|style=Feynman)的两个[基态](@keyword=basis_states|lang=zh-CN|style=Feynman) $|10\rangle$ 和 $|01\rangle$ [@problem_id:2452222]。在这种对应关系下，描述电子相互作用的 CIS 哈密顿矩阵，摇身一变成为了一个作用在这两个[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)上的算符。这个哈密顿矩阵的非对角元（即交换积分 $K_{ia}$）耦合了 $|10\rangle$ 和 $|01\rangle$ 这两个态。

这意味着什么呢？这意味着，如果我们让这个系统随时间演化，一个初始处于 $|10\rangle$（一个可分离的直积态）的[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)，会演化成 $|10\rangle$ 和 $|01\rangle$ 的叠加态。而一个这样的叠加态，在[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)语言中，就是一个**纠缠态 (entangled state)**！因此，描述一个简单化学激发过程的哈密顿量，从[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的角度看，就是一个可以产生纠缠的**[量子门](@keyword=quantum_computing_gates|lang=zh-CN|style=Feynman)**。这个深刻的联系展示了量子力学作为一种通用语言的惊人力量，它统一了[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)的微观世界和未来[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的逻辑核心。

### 认识局限与超越

像任何科学理论一样，CIS 有其辉煌的适用范围，也有其固有的局限性。认识这些局限，不仅能让我们更明智地使用这个工具，也指引了通往更精确理论的道路。

CIS 最根本的近似在于它只考虑了单激发组态。对于许多[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)，这已经足够好了。但有些[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)天生就具有显著的“双激发”甚至更高阶的激发特征。例如，一个[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的真实[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)可能是单激发和双激发的混合体 [@problem_id:1387137]。在这种情况下，CIS 就像一个戴着“单激发滤镜”的观察者，它只能“看到”[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)中单激发的部分，而完全忽略了双激发的部分。这会导致对跃迁强度的错误预测，因为它错误地将所有的“亮度”都归因于单激发成分。

为了克服这个问题，我们需要更强大的理论，例如**[运动方程耦合簇](@keyword=eom_cc|lang=zh-CN|style=Feynman) ([EOM-CC](@keyword=eom_cc|lang=zh-CN|style=Feynman))** 方法。与 CIS 相比，[EOM-CC](@keyword=eom_cc|lang=zh-CN|style=Feynman) 的高明之处在于它提供了一种“平衡的”方式来描述[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)和[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)的电子相关效应 [@problem_id:2464089]。CIS 的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)（HF [波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)）是完全不相关的，而[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)只包含了最基本的单激发混合，这两者之间存在明显的不平衡。而 [EOM-CC](@keyword=eom_cc|lang=zh-CN|style=Feynman) 方法首先用一个指数算符 $e^T$ 为[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)“穿上”一身华丽的“电子相关外衣”，然后再用一个线性算符 $R_k$ 在这个高度相关的[参考态](@keyword=reference_state|lang=zh-CN|style=Feynman)上构造[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)。由于[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)和所有[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)都共享了同一件“外衣”，它们所包含的动力学相关能得到了更公平、更平衡的处理。

然而，这并不意味着 CIS 毫无用处。恰恰相反，科学的智慧往往体现在如何巧妙地改造和扩展现有理论。例如，要计算能量极高的 **X 射线[吸收光谱](@keyword=absorption_spectrum|lang=zh-CN|style=Feynman) (XAS)**，标准的 CIS 会因为“变分崩溃”而彻底失败。但是，通过引入**核心-价态分离 (CVS)** 近似，并使用为[核心空穴](@keyword=core_hole|lang=zh-CN|style=Feynman)态特殊优化的轨道，我们可以成功地将 CIS 方法应用于这个极具挑战性的领域，准确预测材料的 X 射线吸收谱 [@problem_id:2452240]。

### 结论

从预测分子的颜色，到设计高效的[发光材料](@keyword=light_emitting_materials|lang=zh-CN|style=Feynman)；从揭示光合作用的奥秘，到探索晶体中[声子](@keyword=phonons|lang=zh-CN|style=Feynman)的散射；甚至到与[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的未来遥相呼应——我们看到，CIS 作为一个看似简单的理论，其思想的触角延伸到了科学的各个角落。它完美地体现了物理学之美：一个核心概念，通过类比、推广和巧妙的改造，能够解释看似毫不相关的现象，展现出自然法则背后深刻的统一性。CIS 是我们探索[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)世界的第一步，但这一步，已经带领我们看到了无比壮丽的风景。