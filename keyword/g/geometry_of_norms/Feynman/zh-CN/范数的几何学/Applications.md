## 应用与跨学科联系

两点之间最短的路径是什么？当然是直线。但这个看似简单的真理背后隐藏着一个深刻的假设：我们都同意如何测量“长度”以及什么构成“直线”。如果我们能选择自己的尺子呢？如果我们能通过设计一种新的测量距离的方式——一种新的*范数*——来更深刻地理解世界或解决看似不可能复杂的问题呢？在上一章中，我们探讨了范数及其相关[单位球](@keyword=unit_ball|lang=zh-CN|style=Feynman)的形式属性。现在，我们将踏上一段旅程，看看这些抽象的几何思想如何变为现实，重塑从金融、机器学习到物理学基本定律的各个领域。我们将发现，范数单位球的形状不仅仅是一个数学上的奇趣之物；它是一个强大的工具，一种能揭示隐藏的简单性并解锁优雅解决方案的视角选择。

### 稀疏性的几何学：为何“角”是关键

想象一下，你正试图从极少数的测量数据中重建一个信号——比如一幅图像或一段音乐。这似乎是一项不可能的任务，就像试图用一千个方程解出一百万个变量。然而，这就是*[压缩感知](@keyword=compressive_sensing|lang=zh-CN|style=Feynman)*的魔力所在，它之所以能奏效，是因为大多数真实世界的信号都是*稀疏的*；它们只需少数几个重要的信息片段就能描述。挑战在于，如何在一片零的海洋中找到那几个重要的片段。

[范数的几何](@keyword=geometry_of_norms|lang=zh-CN|style=Feynman)学如何帮助我们呢？这个问题可以被构建为找到一个向量$\boldsymbol{x}$，它既满足我们的测量条件$A\boldsymbol{x}=\boldsymbol{b}$，又拥有最少的非零项。直接计算非零项在计算上是一场噩梦。相反，我们可以寻找具有最小“尺寸”或范数的解。但用哪种范数呢？如果我们使用熟悉的欧几里得$\ell_2$范数，我们要求的是离原点最近的解向量。从几何上看，我们正在膨胀一个完美的圆形球体，直到它刚好接触到所有可能解构成的平面（或[超平面](@keyword=hyperplanes|lang=zh-CN|style=Feynman)）。因为球体是光滑的，这个接触点可以位于任何地方，通常导致一个*稠密*的解，其中几乎每个分量都是非零的。

当我们把尺子换成$\ell_1$范数时，突破就来临了，其定义为$\|\boldsymbol{x}\|_1 = \sum_i |x_i|$。$\ell_1$范数的单位球不是一个圆形的球体，而是一个“[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)[多胞体](@keyword=polytopes|lang=zh-CN|style=Feynman)”——二维的菱形，三维的八面体，以此类推。它最显著的特征是其尖锐的角，这些角恰好位于坐标轴上。当我们膨胀这个形状直到它接触到解平面时，它极有可能在其中一个角上首次接触。位于角上的点，其许多坐标都等于零。因此，仅仅通过最小化$\ell_1$范数，我们自然而然地被引导到了我们所寻找的[稀疏解](@keyword=sparse_solutions|lang=zh-CN|style=Feynman)！这个优美的几何直觉是[压缩感知](@keyword=compressive_sensing|lang=zh-CN|style=Feynman)和许多现代[数据科学](@keyword=data_science|lang=zh-CN|style=Feynman)技术能够奏效的核心所在。[@problem_id:2449537]

同样的原理也延伸到了机器学习中。在[支持向量机](@keyword=support_vector_machines|lang=zh-CN|style=Feynman)（SVM）中，目标是找到一个能最好地分离两[类数](@keyword=class_number|lang=zh-CN|style=Feynman)据的[超平面](@keyword=hyperplanes|lang=zh-CN|style=Feynman)。“最好”的分隔器是那个与最近数据点有最大“间隔”或距离的分隔器。传统上，这个距离是用欧几里得$\ell_2$范数来测量的。但如果我们受[压缩感知](@keyword=compressive_sensing|lang=zh-CN|style=Feynman)的启发，考虑一个使用$\ell_1$范数的变体呢？最大化这种新型间隔等价于一个偏爱*稀疏*权重向量$\boldsymbol{w}$的优化问题。一个稀疏的$\boldsymbol{w}$意味着分类决策仅依赖于少数几个输入特征。这不仅使模型更高效，而且更具[可解释性](@keyword=interpretability|lang=zh-CN|style=Feynman)，因为它告诉我们哪些特征是真正重要的。再一次，$\ell_1$范数的“尖角”几何充当了一个强大的选择原则。[@problem_id:2449588]

### 风险与稳定性的几何学

除了寻找[稀疏解](@keyword=sparse_solutions|lang=zh-CN|style=Feynman)，范数还提供了一种通用的语言来定义安全和稳定的边界。在许多物理和经济系统中，一个状态可以表示为高维空间中的一个点。范数可以测量该状态的“压力”或“风险”，而该范数的单位球可以定义一个“安全”区域。

在固[体力](@keyword=body_forces|lang=zh-CN|style=Feynman)学中，当材料受到力时，会产生内部应力，这可以用一个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)来描述。应力状态可以看作是多维[张量](@keyword=tensor|lang=zh-CN|style=Feynman)空间中的一个点。对于许多金属来说，材料开始永久变形（屈服）的条件由[von Mises准则](@keyword=von_mises_criterion|lang=zh-CN|style=Feynman)描述。该准则指出，当应力张量的偏量部分达到一个临界大小时，就会发生屈服。这个大小是通过[Frobenius范数](@keyword=frobenius_norm|lang=zh-CN|style=Feynman)来测量的，它是欧几里得范数到矩阵的推广。从几何上看，安全的弹性区域是一个高维球面。预测[材料行为](@keyword=material_behavior|lang=zh-CN|style=Feynman)的过程包括计算应力状态及其范数，实际上就是在检查状态向量是否已移出这个安全球体之外。[@problem_id:2678303]

类似的概念也适用于[鲁棒控制理论](@keyword=robust_control_theory|lang=zh-CN|style=Feynman)，该理论为飞机或化工厂等必须在存在不确定性的情况下保持稳定的系统设计控制器。一个系统的稳定性可能会受到未建模动态或扰动$\Delta$的威胁。问题是：能使系统失稳的“最小”扰动是什么？“最小”是通过[矩阵范数](@keyword=matrix_norms|lang=zh-CN|style=Feynman)来衡量的。事实证明，对于一个简单的（非结构化）不确定性，系统的脆弱性直接由其[传递函数矩阵](@keyword=transfer_function_matrix|lang=zh-CN|style=Feynman)$M$的最大奇异值决定。最危险的、范数最小的扰动是一个由对应于这个最大[奇异值](@keyword=singular_values|lang=zh-CN|style=Feynman)的奇异向量构成的[秩一矩阵](@keyword=rank_one_matrix|lang=zh-CN|style=Feynman)。从几何上看，[奇异向量](@keyword=singular_vectors|lang=zh-CN|style=Feynman)定义了系统$M$提供最大放大的输入和输出方向。最坏情况的扰动完美地利用了这一点，形成一个[反馈回路](@keyword=feedback_loop|lang=zh-CN|style=Feynman)，将系统推向不稳定。[线性算子](@keyword=linear_operators|lang=zh-CN|style=Feynman)本身的几何结构揭示了它的阿喀琉斯之踵。[@problem_id:2750621]

这种量化脆弱性的思想延伸到了经济学。考虑一个银行间相互借贷的网络。对一家银行的冲击，比如一笔突然的损失，如何通过系统级联并引发危机？我们可以用一个矩阵$L$来建模，其中$L_{ij}$代表银行$i$给银行$j$的贷款。一个简单的线性模型显示，冲击的放大由矩阵$L$的范数决定。使用[无穷范数](@keyword=infinity_norm_2|lang=zh-CN|style=Feynman)$\|\cdot\|_\infty$，它对应于最大绝对行和，可以提供一个特别清晰的洞见。$L$的[无穷范数](@keyword=infinity_norm_2|lang=zh-CN|style=Feynman)代表了任何单一银行对网络其余部分的最大风险暴露。如果这个值太高，系统就不稳定，冲击将被放大。因此，[矩阵范数](@keyword=matrix_norms|lang=zh-CN|style=Feynman)这个抽象概念提供了一个具体的[系统性风险](@keyword=systemic_risk|lang=zh-CN|style=Feynman)度量，将整个金融系统的稳定性与其联系最紧密的成员的行为联系起来。[@problem_id:2449549]

### 优化的几何学：寻找“最直”的路径

可变几何最深刻的应用也许是在[数值优化](@keyword=numerical_optimization|lang=zh-CN|style=Feynman)领域。当我们试图找到一个函数的最小值时，最直观的方法是最速下降法：从你当前的位置，沿着函数下降最快的方向迈出一小步。但哪个方向是“最陡峭”的呢？我们被欧几里得世界塑造的直觉会大声告诉我们，它必定是与梯度相反的方向，即$-\nabla f(\boldsymbol{x})$。

但这仅在我们的尺子是标准欧几里得范数时才成立。如果我们决定用一个不同的范数来测量长度，比如说由一个[正定矩阵](@keyword=positive_definite_matrix|lang=zh-CN|style=Feynman)$P$定义的范数$\|\boldsymbol{d}\|_P = \sqrt{\boldsymbol{d}^T P \boldsymbol{d}}$，那么最速下降的方向就完全改变了。它不再是$-\nabla f(\boldsymbol{x})$，而是$-P^{-1}\nabla f(\boldsymbol{x})$。[@problem_id:2221541] 这是一个革命性的思想。它意味着我们可以改变我们空间的几何结构，使通往最小值的路径变得更加直接。这就是*预处理*的精髓，这项技术可以将一个曲折困难的优化问题转变为一个极其简单的问题。

[共轭梯度](@keyword=conjugate_gradient|lang=zh-CN|style=Feynman)（CG）方法为这一原理提供了一个惊人的例证。当用于求解[线性系统](@keyword=linear_systems|lang=zh-CN|style=Feynman)$A\boldsymbol{x}=\boldsymbol{b}$时，这等价于最小化二次函数$f(\boldsymbol{x}) = \frac{1}{2}\boldsymbol{x}^T A \boldsymbol{x} - \boldsymbol{b}^T \boldsymbol{x}$，CG方法可以被看作是在一种[特殊几何](@keyword=special_geometry|lang=zh-CN|style=Feynman)中的[最速下降法](@keyword=method_of_steepest_descents|lang=zh-CN|style=Feynman)。这种几何是由矩阵$A$本身通过$A$-范数定义的。在这个量身定制的世界里，函数$f(\boldsymbol{x})$的水平集是完美的球面，CG所走的路径是一条直线——一条[测地线](@keyword=geodesic_path|lang=zh-CN|style=Feynman)——直达最小值。与此同时，标准的[最速下降法](@keyword=method_of_steepest_descents|lang=zh-CN|style=Feynman)，固守其欧几里得视角，看到的是扭曲的[椭球](@keyword=ellipsoid|lang=zh-CN|style=Feynman)形水平集，并被迫走一条低效的、之字形的路径。在金融领域，如果$A$是资产收益的[协方差矩阵](@keyword=covariance_matrix|lang=zh-CN|style=Feynman)，这有一个优美的解释：CG对投资组合进行连续调整，这些调整在风险方面是不相关的，从而有效地消除了误差源，而不会抵消先前的进展。[@problem_id:2382850]

### 驯服[维度灾难](@keyword=curse_of_dimensionality|lang=zh-CN|style=Feynman)

在我们这个大数据时代，我们不断面临着在极高维空间中的问题。在这里，[范数的几何](@keyword=geometry_of_norms|lang=zh-CN|style=Feynman)学既提供了诊断工具，也创造了计算奇迹。

在[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)中，计算分子的性质涉及到求解薛定谔方程，这是一个极其复杂的问题。[Hartree-Fock方法](@keyword=hartree_fock_method|lang=zh-CN|style=Feynman)是寻找近似解的一种迭代过程。在[分子几何优化](@keyword=molecular_geometry_optimization|lang=zh-CN|style=Feynman)的每一步，都必须确保电子[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)完全收敛。如果做不到这一点，就会导致作用在原子上的力不正确，优化失败。我们如何检查这种收敛性呢？一个关键条件，[Brillouin定理](@keyword=brillouin_s_theorem|lang=zh-CN|style=Feynman)，可以表示为一个称为Fock矩阵的矩阵的占据-虚拟块$\mathbf{F}_{\mathrm{ov}}$的消失。这个块的[Frobenius范数](@keyword=frobenius_norm|lang=zh-CN|style=Feynman)$\|\mathbf{F}_{\mathrm{ov}}\|_{\mathrm{F}}$，可以作为一个简单的标量诊断工具。如果这个范数不接近于零，就意味着电子态不是[稳态](@keyword=steady_state_2|lang=zh-CN|style=Feynman)，计算出的力是不可靠的。这个范数在[计算化学](@keyword=computational_chemistry|lang=zh-CN|style=Feynman)的高维机器中充当了关键的质量控制仪表。[@problem_id:2877962]

一个更惊人的结果来自随机线性代数。假设你需要分析一个巨大的矩阵$A$。这项任务在计算上可能是望而却步的。令人震惊的Johnson-Lindenstrauss (JL) 引理提出了一条出路。它本质上说，你可以用一个*随机*矩阵将一组点从高维空间投影到一个维度低得多的空间中，并且以高概率，点之间的距离几乎会完美地保持不变。这意味着数据的几何结构得以保留。在随机奇异值分解（rSVD）的背景下，我们可以通过将矩阵$A$乘以一个[随机矩阵](@keyword=stochastic_matrix|lang=zh-CN|style=Feynman)$\Omega$来创建一个更小的“草图”，形成$Y = A\Omega$。因为[随机投影](@keyword=random_projections|lang=zh-CN|style=Feynman)的作用近似于[等距](@keyword=isometry|lang=zh-CN|style=Feynman)映射，所以$A$的[列空间](@keyword=image_of_a_linear_transformation|lang=zh-CN|style=Feynman)的主要几何特征被捕捉在小得多的矩阵$Y$的[列空间](@keyword=image_of_a_linear_transformation|lang=zh-CN|style=Feynman)中。所有后续昂贵的计算都可以在$Y$上执行，从而带来巨大的速度提升。这是一个由几何原理引导的随机性提供强大计算工具的案例。[@problem_id:2196138]

### 最后的疆域：[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)世界上的函数

到目前为止，我们的向量都生活在平坦的空间$\mathbb{R}^n$中。但几何和范数的原理可以被推向其最终的结论：为生活在曲[流形](@keyword=manifold|lang=zh-CN|style=Feynman)上的函数定义范数。在广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)等领域，宇宙是一个弯曲的[时空流形](@keyword=spacetime_manifold|lang=zh-CN|style=Feynman)。我们如何测量这样一个舞台上的函数或场的“大小”或“光滑度”？

这就是黎曼[流形上的[Sobolev空](@keyword=sobolev_spaces_on_manifolds|lang=zh-CN|style=Feynman)间](@article_id:317877)的领域。其思想是通过对函数及其[导数](@keyword=derivative|lang=zh-CN|style=Feynman)进行积分来构建一个范数，就像我们在平坦空间中所做的那样。但要使这个定义坐标无关且有意义，我们必须做出两个关键的替换。首先，依赖于坐标的普通[偏导数](@keyword=partial_derivatives|lang=zh-CN|style=Feynman)必须被尊重空间曲率的*[协变导数](@keyword=covariant_derivative|lang=zh-CN|style=Feynman)*所取代。其次，标准的[勒贝格积分](@keyword=lebesgue_integration|lang=zh-CN|style=Feynman)测度$dx$必须被[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的内蕴体[积测度](@keyword=product_measures|lang=zh-CN|style=Feynman)$d\mathrm{vol}_g$所取代。最终得到的[Sobolev范数](@keyword=sobolev_norm|lang=zh-CN|style=Feynman)是一个真正的[几何不变量](@keyword=geometric_invariants|lang=zh-CN|style=Feynman)，它以一种与任何观察者[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)无关的方式测量函数的属性。在[紧流形](@keyword=compact_manifold|lang=zh-CN|style=Feynman)上，这些空间具有与它们的欧几里得对应物非常相似的[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)性质，构成了现代几何分析和数学物理的基石。[@problem_id:3033615] 这代表了分析与几何的终极统一，证明了一个简单思想的力量：为你希望测量的世界选择正确的尺子。