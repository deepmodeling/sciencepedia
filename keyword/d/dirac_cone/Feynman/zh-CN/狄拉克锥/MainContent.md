## 引言
在材料科学的世界里，电子的行为受一套称为能带结构的规则支配。数十年来，我们的理解一直局限于一种简单的抛物线关系，即电子的能量与其动量之间呈抛物线关系，这将其描述为具有有效质量的传统粒子。然而，石墨烯等材料的发现揭示了一种对这一常规的颠覆性突破：一种尖锐的锥形能量景观，其中电子突然表现得仿佛完全没有质量，在固体内部模拟了[狭义相对论](@keyword=special_relativity_theory|lang=zh-CN|style=Feynman)的物理学。这一特征被称为狄拉克锥，它代表了[凝聚态物理学](@keyword=condensed_matter_physics|lang=zh-CN|style=Feynman)的一次范式转变，开启了大量奇特的量子现象。

本文将深入探讨狄拉克锥的迷人世界。第一部分“**原理与机制**”将揭示这种独特性带结构的根本起源，探索[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)对称性与拓扑学如何共同作用，创造出这些无质量的[相对论性粒子](@keyword=relativistic_particle|lang=zh-CN|style=Feynman)，并赋予它们手性和非平凡[贝里相位](@keyword=berry_s_phase|lang=zh-CN|style=Feynman)等奇特性质。随后，“**应用与跨学科联系**”部分将带领读者遍览其影响的广阔图景：从通过石墨烯革新电子学、在[拓扑绝缘体](@keyword=topological_insulators|lang=zh-CN|style=Feynman)中定义新的[物态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)，到通过“[转角电子学](@keyword=twistronics|lang=zh-CN|style=Feynman)”创造新的物理学，甚至出现在[量子自旋液体](@keyword=quantum_spin_liquids|lang=zh-CN|style=Feynman)的抽象领域中。

## 原理与机制

想象一个电子在广阔、空旷的真[空中运动](@keyword=aerial_locomotion|lang=zh-CN|style=Feynman)。它的世界很简单：其能量完全是动能，随动量的平方而增长。现在，将同一个电子置于晶体内部。突然间，它的世界发生了变化。它不再处于真空中，而是身处一个优美有序的景观之中——一个由原子核构成的重[复图](@keyword=complex_graph|lang=zh-CN|style=Feynman)案，这些原子核施加着一张复杂的力网。电子作为一种波，并不仅仅是冲破这片景观，而是与之共振。这种共振产生了一种宏伟的结构，由允许和禁止的能级构成，这一现象我们称之为**能带结构**。它是晶体独特的“乐谱”，几乎决定了材料的所有[电子性质](@keyword=electronic_properties|lang=zh-CN|style=Feynman)。

几十年来，我们对这些“乐谱”的理解一直被一个熟悉的主题所主导。在我们所知的大多数材料中，如硅，能带边缘附近的电子——那些从事所有有趣工作的电子——行为方式极其简单。它们的能量仍然依赖于动量，但仍遵循传统的方式：呈抛物线状。能量-动量关系的形式为 $E \propto |\mathbf{k}|^2$，其中 $\mathbf{k}$ 是[晶格动量](@keyword=quasimomentum|lang=zh-CN|style=Feynman)。这仿佛电子仍然是一个[自由粒子](@keyword=the_free_particle|lang=zh-CN|style=Feynman)，只是其质量被晶体环境神奇地改变了。我们称之为**有效质量**。在这个“抛物线”世界里，电子的行为很像一个台球；推它一下，它就会加速。在二维世界中，这些电子的可用能态密度是恒定的，就像一个平坦的运动场 [@problem_id:4284971]。这曾是那个令人安心、类似经典物理的图景。

但事实证明，大自然的想象力远不止于此。

### 平坦世界，激进几何

狄拉克锥的故事始于一种像铅笔芯中的石墨一样普通的材料：一种名为**石墨烯**的单原子厚度的碳片。石墨烯之所以如此特殊，在于其原子排列方式。碳原子形成一个完美的二维蜂窝状[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)。这不仅仅是又一个简单的网格。仔细观察会发现一个关键特征：该[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)是**二分的**。它可以被分为两个相互穿插的三角形子[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)，我们可以标记为 A 和 B。子[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman) A 上的每个原子都被来自子[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman) B 的三个邻居包围，反之亦然 [@problem_id:3019519]。

这个看似微不足道的[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)几何细节，却带来了革命性的后果。当我们求解石墨烯中允许的电子能量时，我们发现了惊人的结果。导带（电子存在的区域）和价带（电子来源的区域）之间不像半导体那样存在[带隙](@keyword=band_gap|lang=zh-CN|style=Feynman)，也不像典型金属那样广泛重叠。相反，它们在晶体动量空间中的六个特殊点——即其六边形[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)的角上——完美地接触。

在这些接触点，能量景观的形状不是平缓的抛物线形碗状，而是一个尖锐、完美的锥形。这就是**狄拉克锥**。

在这些点附近，能量 $E$ 与动量 $\mathbf{q}$（从锥顶点测量）之间的关系不再是抛物线形的，而是线性的：

$$
E(\mathbf{q}) = \pm \hbar v_F |\mathbf{q}|
$$

这是狄拉克锥的决定性标志 [@problem_id:4262548] [@problem_id:4284971]。正号描述上方的“导带”锥，负号描述下方的“价带”锥，它们在一个零能量的单一点——**狄拉克点**——相遇。

### 锥上生活：相对论的模仿者

这种线性能量-动量关系是对此前常规的颠覆性突破。事实上，对于物理学家来说，它应该看起来异常熟悉。这正是一个[静止质量](@keyword=rest_mass|lang=zh-CN|style=Feynman)为零、以恒定速度运动的粒子（如光子）的能量-动量关系。在石墨烯中，靠近[狄拉克点](@keyword=dirac_points|lang=zh-CN|style=Feynman)的电子表现得就像无质量的[相对论性粒子](@keyword=relativistic_particle|lang=zh-CN|style=Feynman)。

从某种意义上说，它们是模仿者，在固体内部模拟着[狭义相对论](@keyword=special_relativity_theory|lang=zh-CN|style=Feynman)的物理学。它们的“光速”并非[真空中的光速](@keyword=speed_of_light_in_a_vacuum|lang=zh-CN|style=Feynman)，而是一个小得多且依赖于材料的常数，称为**[费米速度](@keyword=fermi_velocity|lang=zh-CN|style=Feynman)**，$v_F$。在石墨烯中，该速度约为 $10^6 \, \mathrm{m/s}$——一个虽快但可控的速度，约为真空中光速的 1/300 [@problem_id:4262548]。

生活在锥上会带来一些奇特的后果：

-   **恒定速率**：与硅中的电子不同，硅中电子的速率会随着能量的增加而加快，而狄拉克电子始终以相同的速率 $v_F$ 运动。更多的能量只会改变其运动方向，而不会改变其速率 [@problem_id:4284971]。
-   **零有效质量**：固定的有效质量这一在半导体物理学中至关重要的概念，在此完全消失。这些准粒子的“[静止质量](@keyword=rest_mass|lang=zh-CN|style=Feynman)”为零。
-   **消失的[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)**：可用[态密度](@keyword=density_of_states|lang=zh-CN|style=Feynman)不是恒定的。它在锥的顶点处为零，并随能量线性增长，$D(E) \propto |E|$ [@problem_id:4270579]。这意味着在狄拉克点处没有可占据的态，这导致了诸如**[双极性场效应](@keyword=ambipolar_field_effect|lang=zh-CN|style=Feynman)**等现象，即人们可以利用电场将载流子从类电子无缝地调谐到类空穴，并经过一个完全[电中性](@keyword=charge_neutrality|lang=zh-CN|style=Feynman)的状态 [@problem_id:4262548]。

这种独特的行为与[磷烯](@keyword=phosphorene|lang=zh-CN|style=Feynman)等其他[二维材料](@keyword=2d_materials|lang=zh-CN|style=Feynman)形成鲜明对比，后者具有传统的[带隙](@keyword=band_gap|lang=zh-CN|style=Feynman)和各向异性、抛物线形的能带——这提醒我们狄拉克锥是多么的特殊 [@problem_id:4293772]。

### 隐藏的转折：[赝自旋](@keyword=pseudospin|lang=zh-CN|style=Feynman)与手性

故事变得更加奇特。线性的色散关系只是故事的一半。另一半在于最初引发这一切的双子晶格结构。由于电子的[波函数](@keyword=wave_functions|lang=zh-CN|style=Feynman)必须同时分布在 A 和 B 两个子[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)上，它获得了一个新的内部自由度。这不是电子的内禀自旋，而是一种“赝”自旋，描述了电子“偏好”停留在哪个子[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)上。我们将这种双分量性质称为**[赝自旋](@keyword=pseudospin|lang=zh-CN|style=Feynman)** [@problem_id:2805103]。

在狄拉克锥中，这种赝自旋并不独立于电子的运动。它被牢固地锁定在动量方向上。这种性质被称为**手性**，或[螺旋性](@keyword=helicity|lang=zh-CN|style=Feynman)。一个向右运动的电子，其赝自旋相对于其动量有特定的取向；而一个向左运动的电子则具有相反的取向。它们就像具有确定螺纹的螺丝。

这种手性不仅仅是一个有趣的细节；它是石墨烯一些最引人注目的电子特性的根源。为了让一个电子向后散射，它必须完全反转其动量。但由于手性的存在，这也需要翻转其赝自旋。一个平滑、缓慢变化的势——比如来自远处杂质的势——无法提供翻转这种赝自旋所需的急剧冲击。因此，**背散射被强烈抑制**。

其最终表现形式是**克莱因隧穿**。在普通的量子世界里，如果你向一个非常高且宽的能垒发射一个电子，它几乎肯定会被反射。但是一个手性的狄拉克电子，当它迎面撞上一个势垒时，无论势垒有多高多宽，它都将以 100% 的概率穿过 [@problem_id:4284971]。就好像势垒变得透明了一样。这些无质量的手性粒子根本无法用传统手段加以约束。

### 最深的秘密：对称性与拓扑学

狄拉克锥究竟为何存在？它们是碳化学中的偶然现象吗？答案是响亮的“不”。它们的存在是物理学中一个深刻原理最美丽的例证之一：物理性质受到对称性和拓扑学的保护。

[狄拉克点](@keyword=dirac_points|lang=zh-CN|style=Feynman)处的二重简并并非偶然。它受到蜂窝状[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)对称性的严格保障。具体来说，在[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)的 $K$ 点，时间反演对称性与三重[旋转对称](@keyword=rotational_symmetry|lang=zh-CN|style=Feynman)性的结合迫使两条能带在此处相遇。作为对称性的数学语言，群论表明，此处的电子态必须属于一个二维[不可约表示](@keyword=symmetry_species|lang=zh-CN|style=Feynman)，从而保证了简并的存在 [@problem_id:5297044]。一旦破坏这种对称性，就有可能摧毁狄拉克锥。

比对称性更深层次的是拓扑学。如果我们在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中沿着一个环绕[狄拉克点](@keyword=dirac_points|lang=zh-CN|style=Feynman)的封闭路径移动一个电子的动量，其[量子波函数](@keyword=quantum_wavefunction|lang=zh-CN|style=Feynman)会获得一个额外的相位因子。这并非通常由时间流逝产生的动力学相位，而是一种称为**贝里相位**的几何相位。对于环绕狄拉克锥的路径，这个相位恰好是 $\pi$ [@problem_id:3022810]。

这个 $\pi$ [贝里相位](@keyword=berry_s_phase|lang=zh-CN|style=Feynman)是一个[拓扑不变量](@keyword=topological_invariants|lang=zh-CN|style=Feynman)。它是一个稳健、量子化的性质，就像甜甜圈上的孔洞数量一样，不能通过微小的形变来改变。它是狄拉克锥非[平凡拓扑](@keyword=trivial_topology|lang=zh-CN|style=Feynman)的决定性标志，并且具有可直接观测的后果，其中最著名的是**[半整数量子霍尔效应](@keyword=half_integer_quantum_hall_effect|lang=zh-CN|style=Feynman)**。当石墨烯被置于强磁场中时，其电导率会以阶梯状的方式量子化，而这些台阶与传统体系相比，奇特地偏移了半个整数。这个“半台阶”正是对 $\pi$ [贝里相位](@keyword=berry_s_phase|lang=zh-CN|style=Feynman)的直接测量，也是对石墨烯电子[拓扑性质](@keyword=topological_property|lang=zh-CN|style=Feynman)的优美证实 [@problem_id:3022810]。

### 狄拉克材料的宇宙

一旦我们理解了狄拉克锥是基本对称性和拓扑学的结果，我们就可以开始在其他地方寻找它们。而且我们确实找到了很多。

-   **[拓扑绝缘体](@keyword=topological_insulators|lang=zh-CN|style=Feynman)**：这是现代物理学中最令人惊叹的发现之一。它们是一种体态为电绝缘体，但其表面却被迫呈现金属性的材料。为什么？因为其体[能带结构](@keyword=band_structure|lang=zh-CN|style=Feynman)中存在一个拓扑“扭曲”。[拓扑绝缘体](@keyword=topological_insulators|lang=zh-CN|style=Feynman)与真空（或任何普通绝缘体）之间的边界，就像一个[畴壁](@keyword=domain_walls|lang=zh-CN|style=Feynman)，在此处电子性质必须发生变化，从而迫使一个无[带隙](@keyword=band_gap|lang=zh-CN|style=Feynman)态存在。你猜对了，这个态就是一个狄拉克锥 [@problem_id:2532797]。这个表面狄拉克锥的存在由体-边对应关系保证，这是一个将体态拓扑与边缘物理联系起来的深刻原理 [@problem_id:3497727]。

-   **狄拉克和外尔[半金属](@keyword=semimetals|lang=zh-CN|style=Feynman)**：这个概念也可以扩展到三维空间。**[狄拉克半金属](@keyword=dirac_semimetals|lang=zh-CN|style=Feynman)**是可被视为“三维石墨烯”的三维材料。它们拥有三维狄拉克锥，其中四条能带在一个单点相遇。这种高度的简并性受到[晶体对称性](@keyword=crystallographic_symmetry|lang=zh-CN|style=Feynman)、[时间反演对称性](@keyword=time_reversal_symmetry|lang=zh-CN|style=Feynman)和[反演对称性](@keyword=inversion_symmetry|lang=zh-CN|style=Feynman)的共同保护。

如果轻轻地破坏其中一个保护对称性，[狄拉克点](@keyword=dirac_points|lang=zh-CN|style=Feynman)就会分裂。例如，破坏时间反演对称性（如通过施加磁场）会将狄拉克点分裂成一对在[动量空间](@keyword=momentum_space|lang=zh-CN|style=Feynman)中分离的**外尔点**。破坏反演对称性也会使它们在动量空间中分裂 [@problem_id:4312396]。这些外尔点本身也受到[拓扑保护](@keyword=topological_protection|lang=zh-CN|style=Feynman)，并且更为奇特，在动量空间中充当[贝里曲率](@keyword=berry_curvature|lang=zh-CN|style=Feynman)的源和汇。从这个角度看，狄拉克锥是这些更基本的拓扑准粒子的“母体”。

从石墨烯的蜂窝状[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)到[拓扑绝缘体](@keyword=topological_insulators|lang=zh-CN|style=Feynman)的表面，再到外尔[半金属](@keyword=semimetals|lang=zh-CN|style=Feynman)的三维体态，狄拉克锥是一个反复出现的主题。它代表了一类普适的电子行为，其中[晶格](@keyword=crystal_lattices|lang=zh-CN|style=Feynman)的几何结构和[波函数](@keyword=wave_functions|lang=zh-CN|style=Feynman)的[拓扑性质](@keyword=topological_property|lang=zh-CN|style=Feynman)共同作用，创造出违背我们经典直觉的[准粒子](@keyword=quasiparticle|lang=zh-CN|style=Feynman)，它们在晶体内部表现得就像无质量的相对论性物体。始于铅笔痕迹的研究，最终揭示了一个深刻而统一的原理，并持续重新定义着物理学和材料科学的前沿。

