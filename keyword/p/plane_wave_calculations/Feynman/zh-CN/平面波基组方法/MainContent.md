## 引言
理解材料的性质需要为其电子求解量子力学的薛定谔方程，而对于块状体系来说，这是一项极其复杂的任务。[密度泛函理论](@keyword=density_functional_theory|lang=zh-CN|style=Feynman) (DFT) 通过关注电子密度提供了一条切实可行的途径，但一个根本性问题依然存在：我们应该使用何种数学语言来描述这种密度？“[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)”的选择至关重要，而对于晶体中无限重复的原[子模](@keyword=submodule|lang=zh-CN|style=Feynman)式，有一种方法因其简洁和强大而脱颖而出：[平面波基组](@keyword=plane_wave_basis_sets|lang=zh-CN|style=Feynman)。本文旨在填补一个知识鸿沟：从仅仅知道存在不同[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)，到理解为何[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)特别适用于周期性体系，以及如何使其在实际计算中变得可行。

本文将引导您了解使该方法如此稳健的基本概念。在“原理与机制”一节中，我们将探讨[布洛赫定理](@keyword=bloch_s_theorem|lang=zh-CN|style=Feynman)如何使[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)成为晶体的自然选择，单一的[能量截断](@keyword=energy_cutoff|lang=zh-CN|style=Feynman)参数如何实现系统性改进，以及赝势这一巧妙概念如何克服一个看似致命的缺陷。随后，在“应用与跨学科联系”一节中，我们将超越固态物理的范畴，探究这些相同的思想如何被用于计算力、预测分子结构、模拟[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)，甚至在光子学领域控制光的行为。

## 原理与机制

要理解材料的世界——从我们电脑芯片中的硅到净化环境的催化剂——我们需要了解电子在其中的行为。薛定谔方程主宰着这种行为，但要为一个拳头大小、其电子数量比我们银河系中恒星还多的金属块求解该方程，是一项不可能完成的任务。密度泛函理论 (DFT) 为我们提供了一个强大的替代方案，它将问题重塑为关于电子密度的问题，而电子密度是一个简单得多的量。然而，即便有了这种简化，我们仍面临一个根本性问题：如何用数学来描述电子错综复杂的运动？ 这就是**[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)**概念发挥作用的地方。

### 两种哲学的博弈：从原子构建还是从空间雕刻？

想象一下，你想创造一个完美的和弦。一种方法是将各种乐器的声音——小提琴、大提琴、长笛——叠加在一起，每种乐器都贡献其独特的音色。另一种方法是从一块“白噪声”开始，对其进行雕琢，削去不需要的频率，直到只剩下你想要的和弦。这两种方法反映了[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)中构建[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)的两种主要哲学。

第一种，即**局域原子轨道 (LCAO)** 方法，就像组建一支管弦乐队。它在每个[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的位置上放置熟悉的、类原子的函数（如高斯型或[斯莱特型轨道](@keyword=slater_type_orbitals|lang=zh-CN|style=Feynman)）。对于描述一个漂浮在广阔虚空中的孤立分子而言，这种方法非常直观且高效。当所有活动都发生在原子周围时，何必浪费精力去描述真空呢？这是大多数分子化学的标准选择。[@problem_id:1293558]

第二种哲学，即**[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)**方法，则像雕刻一座雕塑。它使用一组普适的、充满空间的函数——频率不断增加的正弦和余弦函数——这些函数在我们模拟盒子里的任何地方都有定义。对于一个孤立分子，这似乎效率极低。我们把大部分计算精力花在了描述空无一物的空间上。但如果我们的体系不是一个孤立的分子呢？如果它是一个固体晶体，一种原则上用重复的原子模式填充*所有*空间的物质呢？

### 晶体的韵律：布洛赫定理与完美[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)

晶体由其周期性所定义。一个电子在[完美晶体](@keyword=perfect_crystal|lang=zh-CN|style=Feynman)中行进时，看到的是一个无限重复的[势能](@keyword=energy_potential|lang=zh-CN|style=Feynman)景观，就像沿着一条铺设完美的瓷砖走廊望去。物理学告诉我们，在这种情况下会发生一些非凡的事情。薛定谔方程的解，即电子波函数，必须遵守一个被称为**[布洛赫定理](@keyword=bloch_s_theorem|lang=zh-CN|style=Feynman)**的特殊条件。该定理指出，晶体中的波函数 $\psi$ 并非某种任意、混乱的函数。它必须采取平面波 $e^{i\mathbf{k}\cdot\mathbf{r}}$ 的形式，其振幅由一个函数 $u_{\mathbf{k}}(\mathbf{r})$ 调制，而这个函数具有与*[晶格](@keyword=crystalline_lattice|lang=zh-CN|style=Feynman)完全相同的周期性*。

这是一个启示！我们试图描述的波函数本身就是根本上周期性的。那么，为什么不使用本身也具有周期性的[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)呢？这就是[平面波基组](@keyword=plane_wave_basis_sets|lang=zh-CN|style=Feynman)的精妙之处。这些[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)的形式为 $e^{i\mathbf{G}\cdot\mathbf{r}}$，其中 $\mathbf{G}$ 是**倒易点阵**中的一个矢量——这是一个数学构造，是实空间[晶格](@keyword=crystalline_lattice|lang=zh-CN|style=Feynman)的[傅里叶变换](@keyword=fourier_transform|lang=zh-CN|style=Feynman)。这些函数是周期性体系的自然语言。对于像砷化镓 ($\text{GaAs}$) 这样形成完美晶体的材料，[平面波基组](@keyword=plane_wave_basis_sets|lang=zh-CN|style=Feynman)不仅仅是一种选择；它是最简洁、最自然的描述，与问题固有的对称性完美匹配。[@problem_id:1293558]

### [能量截断](@keyword=energy_cutoff|lang=zh-CN|style=Feynman)：实现系统性完美的单一旋钮

当然，我们不能使用无限多个这样的[平面波基](@keyword=plane_wave_basis|lang=zh-CN|style=Feynman)函数。我们需要一种切实可行的方法来创建一个有限的集合。我们如何决定哪些最重要？关键在于看它们的动能。一个[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman) $e^{i\mathbf{G}\cdot\mathbf{r}}$ 的动能与 $|\mathbf{G}|^2$ 成正比。电子波函数的缓慢变化、平滑的特征可以由具有小 $|\mathbf{G}|$ 矢量（低动能）的平面波构建。为了捕捉尖锐、快速[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的特征，我们需要包含具有大 $|\mathbf{G}|$ 矢量（高动能）的平面波。

这引出了平面波方法最美妙的特性之一：我们可以用一个单一的物理参数——**[动能截断](@keyword=kinetic_energy_cutoff|lang=zh-CN|style=Feynman)**，或称 $E_{\text{cut}}$——来控制我们[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)的质量。我们只需包含所有动能小于或等于 $E_{\text{cut}}$ 的平面波。就是这么简单。没有需要设计和测试的、针对特定元素的定制[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)。我们只有一个通用的旋钮。如果我们想要更准确的答案，只需调高 $E_{\text{cut}}$ 的值。这保证了我们的计算是**可系统性改进的**；随着我们增加 $E_{\text{cut}}$，我们计算出的能量保证会越来越接近我们所用理论模型的真实答案。我们[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)中的[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)数量 $N_{\text{pw}}$ 与模拟晶胞的体积和[截断能](@keyword=energy_cutoff|lang=zh-CN|style=Feynman)的关系为 $N_{\text{pw}} \propto V E_{\text{cut}}^{3/2}$。[@problem_id:3431500]

### 魔鬼在细节中：[尖点](@keyword=cusps|lang=zh-CN|style=Feynman)、[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)与[赝势](@keyword=pseudopotentials|lang=zh-CN|style=Feynman)的天才构想

这幅图景似乎近乎完美。但实际上，它有一个陷阱——一个非常严重的陷阱。在原子深处，靠近[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的地方，电子感受到一种极其强烈的、奇异的 ($1/r$) [引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)。为了在这里满足薛定谔方程，波函数必须在[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)处形成一个尖锐的**尖点**。此外，芯层电子，那些紧密束缚于[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的电子，在这个深[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)中剧烈[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。

描述这些尖点和快速[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)将需要具有极高动能的平面波。所需的 $E_{\text{cut}}$ 将会巨大无比，以至于在最快的超级计算机上也需要耗费亿万年的时间。在很长一段时间里，这个“[尖点](@keyword=cusps|lang=zh-CN|style=Feynman)问题”使得[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)方法对于真实材料不切实际。[@problem_id:2460094]

解决方案是一项物理学和计算科学上的天才之举：**赝势**。其核心洞见在于，深层的芯层电子在化学上是惰性的。它们忠于自己的[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)，不参与同其他原子的成键。所有有趣的化学和[材料性质](@keyword=material_properties|lang=zh-CN|style=Feynman)都由外层的**价电子**决定。

因此，我们进行了一次巧妙的替换。我们移除了[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)和芯层电子，用一个“赝原子”来替代它们。这个赝原子由一个平滑、微弱的*赝势*来描述，这个赝势经过精心构建，具有两个关键性质。首先，在一个小的“核心半径”之外，它精确地再现了原始原子的势。其次，它产生的价电子波函数——“赝波函数”——在核心半径之外与真实的全电子波函数完全相同，但在核心半径之内，它们是平滑且无节点的，完全没有了麻烦的尖点和[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。

通过进行这种替换，我们现在的任务是描述一个平滑得多的函数。这可以用一个可控的小 $E_{\text{cut}}$ 来精确地完成。这就是为什么赝势不仅仅是一种便利，而是对任何含原子体系进行实际平面波计算的绝对必需品。相比之下，像[高斯型轨道 (GTOs)](@keyword=gaussian_type_orbitals_(gtos)|lang=zh-CN|style=Feynman) 这样的原子中心[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)，只要付出足够的努力，就能够近似[尖点](@keyword=cusps|lang=zh-CN|style=Feynman)，因为它们的函数已经以[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)为中心，这使得[全电子计算](@keyword=all_electron_calculation|lang=zh-CN|style=Feynman)成为可能，尽管通常非常昂贵。[@problem_id:2460094]

### 公正性的力量：摆脱叠加误差

平面波最深刻的优点之一源于其不偏不倚的性质。[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)由模拟盒子的大小和形状决定，而不是由其中原子的位置决定。它们均匀地填充空间，对每个原子、在任何地方都是相同的。

这带来了一个奇妙的结果。在使用原子中心[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)（如 LCAO）的计算中，常常会出现一种被称为**[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)叠加误差 (BSSE)** 的微妙误差。当两个原子相互靠近时，每个原子都可以“借用”以其邻居为中心的[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)来改善自身的描述。这不是一个物理效应；它是对孤立原子使用不[完备基组](@keyword=complete_basis_set|lang=zh-CN|style=Feynman)所产生的赝象。它会导致人为的能量降低和对原子间[结合能](@keyword=binding_energy|lang=zh-CN|style=Feynman)的高估。

使用[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)，这个问题就消失了。由于[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)在整个[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)内是固定的、均匀的，所以没有“邻近”的函数可以借用。每个原子已经可以访问完全相同的[完备基](@keyword=complete_basis|lang=zh-CN|style=Feynman)函数集。当原子被聚集在一起时发生的任何能量降低都是真实物理和化学相互作用的结果，而不是数学赝象。[@problem_id:3434472] [@problem_id:2464018]

然而，这种公正性是一把双刃剑。如果我们进行一项允许模拟盒子体积变化的计算（例如，为了找到材料的平衡[晶格常数](@keyword=lattice_constant|lang=zh-CN|style=Feynman)），一个固定的 $E_{\text{cut}}$ 会导致我们[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)中的[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)数量发生离散的跳跃。这种不连续性会导致施加在模拟盒子壁上的人为压力，这个误差被称为 **Pulay 应力**。这是[基组不完备性](@keyword=basis_set_incompleteness|lang=zh-CN|style=Feynman)的另一种表现形式，与 BSSE 不同，必须小心处理。[@problem_id:2464018]

### 计算的实践艺术：平衡精度与成本

一次真实的[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)计算是在妥协艺术中的一次实践，需要在追求精度和计算成本的限制之间取得平衡。

除了[能量截断](@keyword=energy_cutoff|lang=zh-CN|style=Feynman) $E_{\text{cut}}$，还有另一个关键参数：**$k$ 点取样**。因为晶体在概念上是无限的，我们无法计算所有地方的性质。布洛赫定理允许我们在一个称为布里渊区的特殊区域内，在一个有限的动量矢量网格——**$k$ 点**——上对[电子结构](@keyword=electronic_structure|lang=zh-CN|style=Feynman)进行取样。这个网格的密度是我们必须调节的另一个旋钮。较粗的网格成本较低，但较细的网格更准确。要精确计算能量、力和应力，需要同时对 $E_{\text{cut}}$ 和 $k$ 点网格进行收敛性测试。目标是找到一组**[帕累托最优](@keyword=pareto_optimality|lang=zh-CN|style=Feynman)**的参数：即满足所需精度目标的计算成本最低的组合。[@problem_id:3440829]

其中的权衡取舍可能十分有趣。考虑一个思想实验：我们取一个小[立方晶胞](@keyword=cubic_unit_cells|lang=zh-CN|style=Feynman)，然后决定通过构建一个在一个方向上长 100 倍的超[原胞](@keyword=primitive_unit_cell|lang=zh-CN|style=Feynman)来模拟一根含 100 个原子的长丝。我们的直觉可能会尖叫，认为这将昂贵 100 倍。但物理原理更为微妙。[晶胞体积](@keyword=crystal_unit_cell_volume|lang=zh-CN|style=Feynman)确实增加了 100 倍，这意味着在相同 $E_{\text{cut}}$ 下所需的[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)数量 $N_{\text{pw}}$ 也增加了 100 倍。然而，由于[晶胞](@keyword=unit_cell|lang=zh-CN|style=Feynman)在实空间中长了 100 倍，其[布里渊区](@keyword=brillouin_zone|lang=zh-CN|style=Feynman)在倒易空间中相应地短了 100 倍。在该方向上所需的 $k$ 点取样密度减少了 100 倍。总计算量，约与 $N_k \times N_{\text{pw}}$ 的乘积成正比，几乎保持不变！[基组](@keyword=basis_set|lang=zh-CN|style=Feynman)规模的巨大增加几乎被所需 $k$ 点数量的减少完美抵消——这是实空间与[倒易空间](@keyword=reciprocal_space_2|lang=zh-CN|style=Feynman)之间对偶性的一个优美例证。[@problem_id:2460288]

其他因素也起作用。模拟像铁这样的[磁性材料](@keyword=magnetic_materials|lang=zh-CN|style=Feynman)需要分别处理自旋向上和自旋向下的电子，这实际上创建了两个并行运行的独立计算，使得存储波函数所需的内存加倍。[@problem_id:2460263] 将[交换相关能](@keyword=exchange_correlation_energy|lang=zh-CN|style=Feynman)的描述从简单的[局域密度近似](@keyword=local_density_approximation|lang=zh-CN|style=Feynman) ([LDA](@keyword=local_density_approximation|lang=zh-CN|style=Feynman)) 改进为更复杂的[广义梯度近似 (GGA)](@keyword=generalized_gradient_approximation_(gga)|lang=zh-CN|style=Feynman)，会增加一个随体系大小线性扩展的少量计算开销，但这个成本通常远小于计算的主要部分，因此为了获得更高的精度，这是一项值得的投资。[@problem_id:2987524]

归根结底，[平面波](@keyword=plane_waves|lang=zh-CN|style=Feynman)计算代表了物理学和计算机科学的一大胜利。通过拥抱晶体的周期性，巧妙地避开棘手的[尖点](@keyword=cusps|lang=zh-CN|style=Feynman)问题，并提供一条简单、系统性的收敛路径，它们为从量子力学的基本定律出发预测材料性质提供了一个稳健而简洁的框架。

