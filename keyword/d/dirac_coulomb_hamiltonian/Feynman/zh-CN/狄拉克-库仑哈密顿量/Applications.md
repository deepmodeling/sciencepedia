## 应用与跨学科联系

我们花了一些时间来欣赏[狄拉克方程](@keyword=dirac_equation|lang=zh-CN|style=Feynman)应用于原子时那奇异而优美的架构。我们已经看到了它鲜明的棱角和高耸的拱门。但建筑是用来居住的，理论是用来*使用*的。所以，现在我们不禁要问：这个宏伟的结构能做什么？它打开了哪些门？正如我们将看到的，[狄拉克-库仑哈密顿量](@keyword=dirac_coulomb_hamiltonian|lang=zh-CN|style=Feynman)正是理解周期表下半部分的关键，在那个世界里，我们熟悉的量子力学规则开始弯曲，一个更深层、更统一的现实展现在我们面前。

### 初战告捷：原子的精细结构

狄拉克理论最初也是最优雅的胜利之一，在于它解释了氢原子光谱中一个微妙的谜题。非[相对论量子力学](@keyword=relativistic_quantum_mechanics|lang=zh-CN|style=Feynman)预测，某些电子能级应该是完全简并的——也就是说，具有完全相同的能量。然而，精密的实验表明这并不完全正确。例如，人们发现 $2p$ 能级分裂成两个间距非常近的能级。这种“精细结构”分裂曾是一个谜。物理学家试图通过手动添加修正项来“修复”薛定谔方程——一项用于质量随速度变化的[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)效应，另一项用于电子自旋与其轨道之间一种奇特的相互作用。奇迹般地，这些补丁奏效了。

但狄拉克方程不需要任何补丁[@problem_id:2464125]。它与生俱来就是完备的。你看，自旋不是附加到狄拉克方程上的东西，它被编织进了方程的结构之中。对电子作为四分量旋量的[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)性描述，自动包含了它的磁矩以及该磁矩与其自身绕[核运动](@keyword=nuclear_motion|lang=zh-CN|style=Feynman)所产生的[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)相互作用的方式——我们称之为自旋-轨道耦合。当你求解氢原子的狄拉克方程时，[精细结构分裂](@keyword=fine_structure_splitting|lang=zh-CN|style=Feynman)会自然而然地出现，这是量子力学与狭义相对论统一的直接结果。曾经的一系列临时修正，如今变成了一个单一、深刻而优美的结论。

### 驯服猛兽：[多电子问题](@keyword=many_electron_problem|lang=zh-CN|style=Feynman)

最初的胜利令人振奋，但这只是在最简单的原子中。当我们有两个或更多电子时会发生什么？在这里，我们遇到了一个可怕的问题。包含了电子间[库仑排斥](@keyword=coulomb_repulsion|lang=zh-CN|style=Feynman)的朴素[狄拉克-库仑哈密顿量](@keyword=dirac_coulomb_hamiltonian|lang=zh-CN|style=Feynman)有一个致命缺陷，它“无下界”。为了感受这一点，想象你正在一片地景中寻找最低点。现在想象这片地景包含一个神奇的、无限深的洞。你寻找“最低[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)”的努力将不可避免地导致你掉进这个洞里，能量无休止地骤降。

未投影的[狄拉克-库仑哈密顿量](@keyword=dirac_coulomb_hamiltonian|lang=zh-CN|style=Feynman)就有这样一个洞。我们解释为[正电子](@keyword=positron|lang=zh-CN|style=Feynman)的[负能解](@keyword=negative_energy_solutions|lang=zh-CN|style=Feynman)，创造了这个无底洞。对多电子原子进行的变分计算，在试图寻找最低能态时，会允许一个电子掉入这个负能海，而另一个电子飞向无穷远，导致一个荒谬的、无限负的能量[@problem_id:2774011]。这种病症，有时被称为“连续谱溶解”或“[Brown-Ravenhall病](@keyword=brown_ravenhall_disease|lang=zh-CN|style=Feynman)”，似乎预示着该理论任何实际应用的末日。

解决方案与问题本身一样深刻。我们必须做出一个选择。我们是在描述一个稳定的电子系统，还是在描述更为复杂的量子电动力学（QED）世界，在那个世界里电子-[正电子](@keyword=positron|lang=zh-CN|style=Feynman)对可以从真空中产生？对于化学而言，答案是明确的。我们关心的是原子和分子的稳定电子结构。因此，我们将麻烦的负能态“投影掉”，创建一个只在正能电子态空间内起作用的哈密顿量。这就是**[无对近似](@keyword=no_pair_approximation|lang=zh-CN|style=Feynman)**。这不仅仅是一个数学技巧，它是一个物理宣言。我们正在构建一个关于电子的稳定理论，并通过这样做，我们驯服了这头猛兽。这个无对[狄拉克-库仑哈密顿量](@keyword=dirac_coulomb_hamiltonian|lang=zh-CN|style=Feynman)是有下界的，为整个[相对论量子化学](@keyword=relativistic_quantum_chemistry|lang=zh-CN|style=Feynman)领域提供了坚实的基础。

### 铸造工具：[计算化学](@keyword=computational_chemistry|lang=zh-CN|style=Feynman)家的武器库

有了稳定的哈密顿量，我们终于可以构建研究现实世界的工具了。正是在这里，狄拉克-库仑模型与计算科学这一强大的智力引擎联系起来。

研究分子的最强大工具之一是**[密度泛函理论 (DFT)](@keyword=density_functional_theory_dft|lang=zh-CN|style=Feynman)**，它巧妙地将问题重新表述为关注电子密度，而不是极其复杂的[多电子波函数](@keyword=many_electron_wavefunction|lang=zh-CN|style=Feynman)。但这个想法能[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)化吗？答案是肯定的。只要我们使用稳定的无对哈密顿量，DFT的基础支柱——Hohenberg-[Kohn定理](@keyword=kohn_s_theorem|lang=zh-CN|style=Feynman)，就可以推广到[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)领域[@problem_id:2464791]。这就产生了**[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)DFT**，这是现代计算化学真正的“主力军”。在其最完整的形式中，它甚至扩展了我们对“密度”的概念：对于[磁场](@keyword=magnetic_field|lang=zh-CN|style=Feynman)中的系统，基本变量不仅仅是标量电荷密度，而是整个[时空](@keyword=space_time|lang=zh-CN|style=Feynman)[四维流](@keyword=four_current|lang=zh-CN|style=Feynman)密度 $j^{\mu}(\mathbf r)$ [@problem_id:2920645]。

对于要求最高精度的问​​题，化学家会求助于所谓的“[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)方法”，如**[耦合簇](@keyword=coupled_cluster|lang=zh-CN|style=Feynman) (CC) 理论**。在[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)框架下实现这些方法是一个引人入胜的挑战[@problem_id:2632837]。我们熟悉的[自旋轨道](@keyword=spin_orbitals|lang=zh-CN|style=Feynman)语言被四分量旋量所取代。由于[自旋-轨道耦合](@keyword=l_s_coupling|lang=zh-CN|style=Feynman)现在是问题的内在部分，自旋不再是一个“[好量子数](@keyword=good_quantum_numbers|lang=zh-CN|style=Feynman)”；我们不能再谈论纯粹的[单重态和三重态](@keyword=singlet_and_triplet_states|lang=zh-CN|style=Feynman)。数学机制必须被重建以处理复数，因为旋量以及对它们的积分通常是复数值的。然而，聪明的物理学家和程序员已经找到了使其易于处理的方法，例如，通过利用潜在的时间反演对称性（[Kramers对](@keyword=kramers_pair|lang=zh-CN|style=Feynman)称性）来削减[计算成本](@keyword=computational_cost|lang=zh-CN|style=Feynman)。

完整的四分量处理在计算上仍然非常昂贵。这催生了一系列极具创造性的近似方法。像**[零阶正则近似](@keyword=zeroth_order_regular_approximation|lang=zh-CN|style=Feynman) (ZORA)** 和 **精确二分量 (X2C)** 方法等技术，试图将[狄拉克旋量](@keyword=dirac_spinors|lang=zh-CN|style=Feynman)中大的电子分量与小的正电子分量“解耦”，从而产生一个更易于处理的二分量哈密顿量[@problem_id:2891921]。这些方法本身就是一门艺术，但它们伴随着一个至关重要的微妙之处。当你改变哈密顿量时，你也在改变你所描绘的现实“图像”。要获得一个物理性质的正确答案，你还必须变换你用来测量它的算符（“尺子”）。这就是**图像变换修正**，一个重要的细节，它提醒我们在[理论物理学](@keyword=theoretical_physics|lang=zh-CN|style=Feynman)中[逻辑一致性](@keyword=consistency_of_logic|lang=zh-CN|style=Feynman)的必要性[@problem_id:2888165]。

### 见证[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)世界：化学与[光谱学](@keyword=spectroscopy|lang=zh-CN|style=Feynman)

现在我们有了工具。我们能看到什么？

我们看到的第一件事是，[重元素](@keyword=heavy_elements|lang=zh-CN|style=Feynman)的性质完全由[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)主导。为什么金是黄色的，而银是白色的？为什么汞在室温下是液体？答案就在[狄拉克方程](@keyword=dirac_equation|lang=zh-CN|style=Feynman)中。对于像金 ($Z=79$) 这样的重原子，[内层电子](@keyword=core_electrons|lang=zh-CN|style=Feynman)以光速的很大一部分在运动。它们的[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)性质量增加导致它们的轨道收缩。内层轨道的这种收缩更有效地屏蔽了核[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，使得外层价轨道（尤其是 $6s$）也被拉得更近。金中价层 $s$ 轨道的这种[相对论性收缩](@keyword=relativistic_contraction|lang=zh-CN|style=Feynman)使其稳定化，改变了轨道之间的[能隙](@keyword=electronic_band_gap|lang=zh-CN|style=Feynman)。它吸收蓝光，反射黄光。在汞中同样效应创造了一个异常稳定的价层电子壳层，使得汞原子之间的键非常弱，以至于它在 $-39^{\circ}C$ 就熔化了。[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)甚至改变了分子对电场的响应，改变了其[永久电偶极矩](@keyword=permanent_electric_dipole_moment|lang=zh-CN|style=Feynman)和[极化率](@keyword=polarizability|lang=zh-CN|style=Feynman)[@problem_id:2888165]。

接下来，我们找到了一种新的语言来描述含有重原子的分子。在非[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)理论中，我们通过轨道角动量投影 ($\Lambda$) 和自旋角动量投影 ($\Sigma$) 到核间轴上来对[双原子分子的电子态](@keyword=electronic_states_of_diatomic_molecules|lang=zh-CN|style=Feynman)进行分类。但[狄拉克方程](@keyword=dirac_equation|lang=zh-CN|style=Feynman)告诉我们，[自旋-轨道耦合](@keyword=l_s_coupling|lang=zh-CN|style=Feynman)混合了这些量。它们不再分别守恒。唯一保持为[好量子数](@keyword=good_quantum_numbers|lang=zh-CN|style=Feynman)的是*总*[电子角动量](@keyword=electronic_angular_momentum|lang=zh-CN|style=Feynman)的投影，$\Omega = \Lambda + \Sigma$ [@problem_id:2787530]。这种从基于 $\Lambda$ 和 $\Sigma$（洪德情况(a)或(b)）的描述转变为基于 $\Omega$（洪德情况(c)）的描述，并非品味问题，而是问题对称性的根本改变，是[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)强加给我们的。

也许最引人注目的后果体现在我们从这些分子中看到的光。在非[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)世界中，控制光吸收和发射的电偶极算符是与自旋无关的。这导致了严格的选择定则 $\Delta S = 0$。不同[自旋态](@keyword=spin_states|lang=zh-CN|style=Feynman)之间的跃迁（例如，[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)到[单重态](@keyword=singlet_state|lang=zh-CN|style=Feynman)）是“禁戒”的。这就是为什么一些材料可以吸收光并“卡”在激发的[三重态](@keyword=triplet_state|lang=zh-CN|style=Feynman)中，以[磷光](@keyword=phosphorescence|lang=zh-CN|style=Feynman)的形式缓慢释放能量。

但在[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)世界中，这个规则被打破了。由于[自旋-轨道耦合](@keyword=l_s_coupling|lang=zh-CN|style=Feynman)将单重态和三重态的特征混合到电子态中，一个我们可能*称之为*三重态的态实际上混入了一点单重态的成分，反之亦然。这种“借来”的特征足以使[禁戒跃迁](@keyword=forbidden_transitions|lang=zh-CN|style=Feynman)变得弱允许[@problem_id:2920677]。对于重元素，这种效应可能非常强，以至于允许和禁戒之间的区别变得模糊。一个全新的“系间窜越”[光谱学](@keyword=spectroscopy|lang=zh-CN|style=Feynman)世界就此打开，让我们能够以其他方式无法实现的方式探测分子的电子结构。

从氢原子中[谱线](@keyword=spectral_line|lang=zh-CN|style=Feynman)的微妙分裂，到[金的颜色](@keyword=color_of_gold|lang=zh-CN|style=Feynman)和磷光屏的发光，[狄拉克-库仑哈密顿量](@keyword=dirac_coulomb_hamiltonian|lang=zh-CN|style=Feynman)为我们的量子世界提供了一个更深层、更统一、最终也更真实的描述。它证明了基本原理的力量，以及当伟大思想——量子力学和[狭义相对论](@keyword=special_relativity_theory|lang=zh-CN|style=Feynman)——汇集在一起时所产生的意想不到的美。