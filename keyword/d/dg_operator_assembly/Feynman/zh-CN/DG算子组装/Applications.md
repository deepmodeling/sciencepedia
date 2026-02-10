## 应用与跨学科联系

在上一章中，我们从基本组件开始，细致地组装了间断 Galerkin (DG) 算子。我们看到了如何通过[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)、[求积法则](@keyword=quadrature_rules|lang=zh-CN|style=Feynman)以及在单元边界充当守门人的关键[数值通量](@keyword=numerical_fluxes|lang=zh-CN|style=Feynman)来构建它。您可能会觉得这纯粹是一项数学练习，一个构建复杂矩阵的游戏。但事实远非如此。DG 算子的真正魅力不在于其静态形式，而在于其独特的结构让我们能够*做什么*。

就像一位钟表大师组装齿轮和弹簧，不仅仅是为了欣赏机械结构，而是为了制造一个测量时间的设备一样，我们现在将看到组装好的 DG 算子如何成为科学发现和工程创新的强大引擎。我们会发现，我们融入其设计的那些特性——其局部性、其复合性、其对不连续性的处理——正是解决现代科学中一些最棘手问题的关键。本章是一次探索算子影响范围的旅程，从超级计算机的核心到人工智能的前沿。

### 可能性的艺术：高性能计算

科学中一个反复出现的主题是，一个绝妙的想法的好坏取决于我们执行它的能力。高阶 DG 方法就是一个完美的例子；它们承诺了卓越的精度，但一个幼稚的实现会在计算上造成灾难。应用算子的成本会随着多项式阶数（$p$）和空间维度（$d$）的增加而迅速增长，以至于即使是中等规模的问题也变得难以处理。那么，DG 方法是如何被用来模拟从[湍流](@keyword=turbulent_flow|lang=zh-CN|style=Feynman)到[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)合并等一切事物的呢？答案在于利用算子的结构。

第一个秘密是**局部性**。根据设计，DG 算子的构造分为两部分：“体”项和“面”项。通常计算最密集的部分——体项的计算——*仅*依赖于单个单元内的数据。这意味着我们可以同时[计算网格](@keyword=computational_mesh|lang=zh-CN|style=Feynman)中所有单元的体项贡献，而无需它们之间进行通信。这种通常被称为“易于并行”的特性，与现代超级计算机完美匹配，后者利用成千上万甚至数百万个并行工作的处理器核心的力量。唯一需要的通信是面项，其中一个单元需要与其直接邻居交换少量数据——其边界上的解值 [@problem_id:3407824]。这种最小化的、局部的通信模式使 DG 方法具有非凡的[可扩展性](@keyword=scalability|lang=zh-CN|style=Feynman)。

第二个，也可能是更深刻的秘密，是一种被称为**[和因子分解](@keyword=sum_factorization|lang=zh-CN|style=Feynman)**的算法杰作。在一个三维单元上天真地应用 DG 算子将涉及一个复杂度约为 $O(p^6)$ 的矩阵向量乘积。这是一个计算噩梦。然而，对于我们经常使用的[张量积](@keyword=tensor_product|lang=zh-CN|style=Feynman)单元（如砖块或立方体），高维算子可以被“分解”为一系列简单的一维操作。想象一下被要求在三维网格的每个点上计算一个函数。[和因子分解](@keyword=sum_factorization|lang=zh-CN|style=Feynman)允许我们沿着每个坐标方向执行一系列简单操作——首先沿着所有的 x-线，然后是 y-线，最后是 z-线——而不是进行一次巨大的计算。这种视角的简单改变将计算成本从不可能的 $O(p^{2d})$ 转换为更易于管理的 $O(d p^{d+1})$ [@problem_id:3407955]。

这种避免了构造完整单元矩阵的“无矩阵”方法具有深远的实际意义。使用性能模型，我们可以预测哪种策略——显式矩阵组装或无矩阵[和因子分解](@keyword=sum_factorization|lang=zh-CN|style=Feynman)——在给定的计算机上更快。对于低阶多项式，老式矩阵的开销可能是可以接受的。但是，当我们为了利用[高阶精度](@keyword=higher_order_accuracy|lang=zh-CN|style=Feynman)的力量而增加多项式阶数时，会有一个明显的“交叉点”，此时[无矩阵方法](@keyword=matrix_free_methods|lang=zh-CN|style=Feynman)卓越的伸缩性将决定性地胜出。这个交叉点甚至取决于硬件；图形处理器（GPU）以其巨大的并行性，通常比传统 CPU 更早地偏爱[无矩阵方法](@keyword=matrix_free_methods|lang=zh-CN|style=Feynman) [@problem-id:3422374]。DG 算子的结构决定了算法，而算法又必须根据其运行的硬件进行调整。

### 求解物理上难以处理的问题

DG 算子不仅仅是一个需要高效计算的对象；它是我们描述和求解支配物理世界的方程的主要工具。其独特的结构再次证明是无价之宝。

许多现实世界现象涉及在截然不同的时间尺度上发生的过程的混合。考虑河流中污染物的输运：水的[整体流](@keyword=bulk_flow|lang=zh-CN|style=Feynman)动（[对流](@keyword=convection|lang=zh-CN|style=Feynman)）以一种速度发生，而污染物的缓慢分子扩散（[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)）则以另一种速度发生。在[数值模拟](@keyword=numerical_simulation|lang=zh-CN|style=Feynman)中，快速的扩散过程会迫使[显式时间步进](@keyword=explicit_time_stepping|lang=zh-CN|style=Feynman)格式采取极其微小的步长，使得模拟时间长得令人望而却步。我们组装 DG 算子的方式提供了一个优雅的解决方案。我们自然地为[对流](@keyword=convection|lang=zh-CN|style=Feynman)部分（$K$）和刚性[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)部分（$S$）构建了独立的算子。这种分离使我们能够使用强大的**隐式-显式 (IMEX) [时间步进格式](@keyword=time_stepping_schemes|lang=zh-CN|style=Feynman)**。我们显式地处理非刚性的[对流](@keyword=convection|lang=zh-CN|style=Feynman)部分（这在计算上很便宜），而隐式地处理刚性的[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)部分（这消除了严苛的时间步长限制）。我们两全其美：一个既稳定又高效、同时尊重物理多尺度性质的模拟 [@problem_id:3391592]。

此外，一个好的数值方法必须尊重其模拟系统的基本平衡态。[地球物理学](@keyword=geophysics|lang=zh-CN|style=Feynman)中的一个经典例子是“静湖”状态。一个在重力作用下表面平坦的湖泊，即使湖底凹凸不平，也应保持完全静止。令人惊讶的是，许多数值格式很难捕捉到这个简单的事实；它们常常产生虚假的、非物理的流动。DG 算子组装的灵活性使我们能够设计一种**良态平衡格式**。通过精心离散化[压力梯度](@keyword=pressure_gradient|lang=zh-CN|style=Feynman)和来自湖床地形的[引力源](@keyword=sources_of_gravity|lang=zh-CN|style=Feynman)项，我们可以确保它们在离散意义上完美抵消，就像在现实中一样。这使得格式能够以[机器精度](@keyword=unit_roundoff|lang=zh-CN|style=Feynman)保持静湖状态，这对于精确模拟在一个巨大的、稳定的水体之上的微小扰动（如微小的涟漪或海啸波）至关重要 [@problem_id:3377741]。

当然，世界本质上是[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)的。为了[求解非线性方程](@keyword=solving_nonlinear_equations|lang=zh-CN|style=Feynman)，黄金标准是 Newton 法，它需要在每一步对问题进行线性化。这种线性化涉及一个称为[雅可比矩阵](@keyword=jacobian|lang=zh-CN|style=Feynman)的巨大的导数矩阵。对于大问题，构造和存储这个雅可比矩阵通常是不可能的。在这里，DG 方法的无矩阵哲学再次提供了一条前进的道路。使用**无雅可比的 [Newton-Krylov](@keyword=newton_krylov|lang=zh-CN|style=Feynman) (JFNK) 方法**，我们可以在不构造[雅可比矩阵](@keyword=jacobian|lang=zh-CN|style=Feynman)的情况下求解线性化系统。我们所需要的只是一种计算雅可比矩阵作用于一个向量的方法。值得注意的是，这个作用可以通过我们现有的 DG 残差算子的简单[有限差分](@keyword=finite_differences|lang=zh-CN|style=Feynman)来近似。这就创造了一种美丽的[共生关系](@keyword=symbiotic_relationships|lang=zh-CN|style=Feynman)：一个最先进的[非线性求解器](@keyword=nonlinear_solvers|lang=zh-CN|style=Feynman)，由我们为高性能计算开发的同样高效的、无矩阵的残差计算代码提供动力 [@problem_-id:3398891]。

### 建立新的联系

DG 算子所体现的原理是如此基础，以至于它们的影响现在正远远超出传统模拟的范畴，与其他科学和数学领域建立起新的联系。

物理学最美的方面之一是发现表面上不相关的现象之间隐藏的统一性。在数值方法的世界里也存在类似的统一性。从表面上看，间断 Galerkin 方法似乎与它们的近亲——从一开始就强制连续性的连续 Galerkin [谱元法 (SEM)](@keyword=spectral_element_methods_(sem)|lang=zh-CN|style=Feynman)——大相径庭。然而，如果恰当地选择成分——特别是，使用位于 Gauss-Lobatto 求积点上的[节点基](@keyword=nodal_basis|lang=zh-CN|style=Feynman)——这两种方法在代数上变得完全相同。从[弱形式](@keyword=weak_formulation|lang=zh-CN|style=Feynman)[体积分](@keyword=volume_integration|lang=zh-CN|style=Feynman)和[中心通量](@keyword=central_flux|lang=zh-CN|style=Feynman)面项精心组装而成的 DG 算子，与全局组装的 SEM 算子产生的结果完全一致 [@problem_id:3385289]。这是一个深刻的启示，表明不同的逻辑链和不同的哲学出发点可以通向相同的本质真理。

现代 DG 求解器的速度使其能够用于曾经无法想象的应用中，例如创建**[降阶模型](@keyword=reduced_order_models|lang=zh-CN|style=Feynman) (ROMs)**。想象一下，为了找到一个最优的翼型，需要对机翼上的气流进行数千次模拟。即使是快速的 DG 求解器也太慢了。ROM 通过首先运行几次高保真度的 DG 模拟来“学习”系统的最主要行为，并将它们捕捉到一小组“降阶基”函数中，从而解决了这个问题。然后，巨大的 DG 算子被投影到这个微小的基上，产生一个求解速度极快的微型系统。使其变得实用的关键在于能够将昂贵的离线计算与廉价的在线查询分开。如果问题的物理参数以简单的“仿射”方式出现在控制方程中，我们就可以离线完成所有繁重的投影工作。对于更复杂的非仿射依赖关系，一种称为**[经验插值法](@keyword=empirical_interpolation_method|lang=zh-CN|style=Feynman) (EIM)** 的巧妙技术可用于恢复近似的仿射结构，从而恢复离线-在线的效率 [@problem_id:3412142] [@problem_id:3383619]。这使我们能够构建“数字孪生”——能够在实时中模拟的物理系统的虚拟副本。

也许最令人兴奋的新前沿是经典[数值分析](@keyword=numerical_analysis|lang=zh-CN|style=Feynman)与现代机器学习的[交叉](@keyword=chiasmata|lang=zh-CN|style=Feynman)。**物理启发的[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络 ([PINNs](@keyword=pinns|lang=zh-CN|style=Feynman))** 试图通过训练一个[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络来满足控制方程，从而求解偏微分方程。然而，基本的 PINNs 常常在稳定性和准确性方面遇到困难，因为它们缺乏像 DG 这样方法中内建的数学严谨性。一个绝妙的新想法是通过使用 DG 残差本身作为[损失函数](@keyword=loss_functions|lang=zh-CN|style=Feynman)，将这种严谨性注入到 PINN 中。我们不仅仅要求网络在几个点上满足[偏微分方程](@keyword=partial_differential_equation|lang=zh-CN|style=Feynman)，而是要求其输出函数满足完整的 DG [弱形式](@keyword=weak_formulation|lang=zh-CN|style=Feynman)——包括那些保证稳定性和守恒性的精心设计的[数值通量](@keyword=numerical_fluxes|lang=zh-CN|style=Feynman)和惩罚项。这种被称为 DG-PINN 或变分 PINN (vPINN) 的强大综合，可以利用 DG 的全部理论体系，例如在损失函数中使用 mortar 方法来处理具有[悬挂节点](@keyword=dangling_nodes|lang=zh-CN|style=Feynman)的复杂[非协调网格](@keyword=non_conforming_meshes|lang=zh-CN|style=Feynman) [@problem_id:3408372]。DG 算子组装的深刻原理正在为构建下一代稳健、可靠且具有物理意识的人工智能提供数学支架。

从处理器的核心到物理定律的结构，再到机器学习的逻辑，DG 算子远不止是一个单纯的矩阵。其内部架构——局部性、张量积结构和基于组件的设计——是开启广阔应用领域的钥匙，揭示了纯数学、物理学和计算机科学之间深刻而美丽的统一。