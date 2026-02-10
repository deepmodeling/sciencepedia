## 应用与跨学科联系

在我们之前的讨论中，我们探索了李群及其表示的优雅框架。可以说，我们学习了词汇——群、代数以及它们可以用[矩阵表示](@keyword=matrix_representations|lang=zh-CN|style=Feynman)的各种方式的定义。但是学一套字母是一回事，用它写诗则完全是另一回事。现在，我们进入应用领域，看看这种优美的数学语言如何不仅仅是一种抽象的游戏，而是物理世界的真正语法。我们将发现，*对称性决定相互作用*这一深刻论断，正是通过表示论的机制得以实现的。

### [粒子物理学](@keyword=particle_physics|lang=zh-CN|style=Feynman)：标准模型的架构蓝图

[李群表示](@keyword=lie_groups_representation|lang=zh-CN|style=Feynman)的原理在[粒子物理学](@keyword=particle_physics|lang=zh-CN|style=Feynman)的[标准模型](@keyword=standard_model|lang=zh-CN|style=Feynman)中展现得最为耀眼。该模型是我们对基本粒子和力最成功的描述，它并非一堆杂乱无章的实体的集合，而是一座基于特定[对称群](@keyword=symmetry_groups|lang=zh-CN|style=Feynman)$SU(3) \times SU(2) \times U(1)$基础之上，令人惊叹的建筑。我们观察到的粒子，从深层次上讲，不过是这个群的[不可约表示](@keyword=irreducible_representations|lang=zh-CN|style=Feynman)。

想想夸克。它们有三种“颜色”（红、绿、蓝），但这并非视觉意义上的颜色，而是[量子色动力学](@keyword=quantum_chromodynamics|lang=zh-CN|style=Feynman)（QCD）的$SU(3)$群的3维[基本表示](@keyword=fundamental_representation|lang=zh-CN|style=Feynman)的态的标签。夸克*就是*[基本表示](@keyword=fundamental_representation|lang=zh-CN|style=Feynman)。而[胶子](@keyword=gluons|lang=zh-CN|style=Feynman)——传递强力并将夸克束缚成质子和中子的粒子——则属于另一类。它们属于8维的*[伴随表示](@keyword=adjoint_representation|lang=zh-CN|style=Feynman)*。这不是一个随意的选择；[伴随表示](@keyword=adjoint_representation|lang=zh-CN|style=Feynman)之所以特殊，是因为它描述了群自身的结构。生成元本身在这个表示下变换，这意味着胶子携带它们所传递的力的“荷”，使它们能够相互作用。

这带来了一个优美的见解。粒子如何相互作用？费曼图中代表基本相互作用的顶点，在数学上由可以从相互作用粒子的表示构建出来的[不变张量](@keyword=invariant_tensors|lang=zh-CN|style=Feynman)来描述。例如，三个[胶子](@keyword=gluons|lang=zh-CN|style=Feynman)之间的相互作用由[李代数](@keyword=lie_algebras|lang=zh-CN|style=Feynman)的[结构常数](@keyword=structure_constants|lang=zh-CN|style=Feynman)$f^{abc}$决定。另一种可能的三[胶子相互作用](@keyword=gluon_interactions|lang=zh-CN|style=Feynman)类型与另一个[不变张量](@keyword=invariant_tensors|lang=zh-CN|style=Feynman)，即全对称的$d^{abc}$符号有关。一位物理学家可能会问：对于一个给定的群，三个[伴随表示](@keyword=adjoint_representation|lang=zh-CN|style=Feynman)的粒子有多少种独立的相互作用方式？这等价于询问[伴随表示](@keyword=adjoint_representation|lang=zh-CN|style=Feynman)与自身的三个张量积中有多少个单态表示。对于群$SU(4)$这个有启发性的例子，人们发现正好有两个这样的[不变量](@keyword=invariant|lang=zh-CN|style=Feynman)，对应于这些基本的$f$和$d$结构[@problem_id:660035] [@problem_id:846079]。相互作用的规则本身就编码在[张量积](@keyword=tensor_product|lang=zh-CN|style=Feynman)的分解之中。

要在这类理论中进行任何实际计算——比如说，预测一个粒子的[衰变率](@keyword=decay_rate|lang=zh-CN|style=Feynman)——我们需要一个一致的“度量衡”。这由[卡西米尔不变量](@keyword=casimir_invariants|lang=zh-CN|style=Feynman)和邓金指数等量提供，它们是每个表示的独特指纹。通过建立一个约定，例如，任何$SU(N)$群的[基本表示](@keyword=fundamental_representation|lang=zh-CN|style=Feynman)的邓金指数为$T_F = 1/2$，物理学家们创造了一个通用标准。从这个简单的约定和已知的基本卡西米尔算符的值，可以优雅地导出[归一化](@keyword=normalization|lang=zh-CN|style=Feynman)，展示了理论内部深刻的一致性[@problem_id:749319]。计算更复杂表示的这些指数，比如两个基本粒子[反对称张量](@keyword=antisymmetric_tensor|lang=zh-CN|style=Feynman)积的表示[@problem_id:185213]，是构建和检验新模型的关键一步。

### [超越标准模型](@keyword=beyond_the_standard_model|lang=zh-CN|style=Feynman)：寻求统一的简洁性

物理学家们梦想着统一——即看似不同的自然力是单一、更宏伟的力在低能量下的表现，这个力由一个更大的单李群所支配。在一个[大统一理论](@keyword=grand_unified_theory|lang=zh-CN|style=Feynman)（GUT）中，标准模型的[对称群](@keyword=symmetry_groups|lang=zh-CN|style=Feynman)$SU(3) \times SU(2) \times U(1)$将只是一个更大得多的群的[子群](@keyword=subgroup|lang=zh-CN|style=Feynman)，也许是$SU(5)$、$SO(10)$或更奇特的群。

在宇宙大爆炸后不久的极高能量下，这种宏大的对称性是显现的。但随着宇宙冷却，对称性“破缺”了。一个关键问题随之而来：如果我们有一组粒子，它们构成了GUT群的一个单一、优雅的不可约表示，那么在对称性破缺后它们会是什么样子？答案在于**分支规则**，它告诉我们一个群$G$的表示如何分解为一个[子群](@keyword=subgroup|lang=zh-CN|style=Feynman)$H$的表示之和。

例如，可以考虑一个基于$SU(4)$的假想理论。如果这个对称性破缺到我们熟悉的强力$SU(3)$对称性，那么$SU(4)$的15个规范玻色子（处于其[伴随表示](@keyword=adjoint_representation|lang=zh-CN|style=Feynman)中）在我们看来会是怎样的？分支规则的数学给出了一个明确的答案：它们分裂成一个8维表示（$SU(3)$的[胶子](@keyword=gluons|lang=zh-CN|style=Feynman)）、一个基本的3维表示、其[反粒子](@keyword=antiparticles|lang=zh-CN|style=Feynman)[共轭表示](@keyword=conjugate_representation|lang=zh-CN|style=Feynman)和一个单态[@problem_id:625425]。这是一个非凡的预言：一个统一的多重态破碎成了一系列熟悉的粒子外加新的、未被发现的粒子。研究这些分支规则，无论是从$SU(4)$到$Sp(4)$[@problem_id:846116]还是从$SO(5)$到$SO(4)$[@problem_id:761613]，是推导任何提出的统一理论的低能预言的主要工具。破缺后出现的[不可约表示的数量](@keyword=number_of_irreducible_representations|lang=zh-CN|style=Feynman)告诉我们应该去寻找多么丰富的新粒子谱。

### 最远的边疆：弦理论与[时空](@keyword=space_time|lang=zh-CN|style=Feynman)

[表示论](@keyword=representation_theory|lang=zh-CN|style=Feynman)的力量延伸到了理论物理的最前沿。在寻求万有理论的过程中，[弦理论](@keyword=string_theory|lang=zh-CN|style=Feynman)假定基本实体不是点状粒子，而是微小的、[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)的弦。所涉及的对称性极其庞大。其中最引人入胜的是例外[李群](@keyword=lie_groups|lang=zh-CN|style=Feynman)$E_8$。其最小的非[平凡表示](@keyword=trivial_representation|lang=zh-CN|style=Feynman)是伴随表示，维数为248。

从事弦理论研究的物理学家们使用我们讨论过的相同工具，但规模更为宏大。他们会问这样的问题：当我们将两个这样的248维对象组合时会发生什么？[张量积](@keyword=tensor_product|lang=zh-CN|style=Feynman)$248 \otimes 248$分解为对称和反对称部分，而这些部分又会分裂成$E_8$的其他不可约表示。这些产生的[表示的维数](@keyword=dimension_of_representation|lang=zh-CN|style=Feynman)，例如在对称部分中找到的1、3875和27000维不可约表示，暗示了在这样一个奇异世界中可能存在的复合粒子和相互作用[@problem_id:621560]。我们甚至能够提出并回答这样的问题，就证明了这种数学语言的力量和普适性。

离我们更近一些，[李群](@keyword=lie_groups|lang=zh-CN|style=Feynman)描述了[时空](@keyword=space_time|lang=zh-CN|style=Feynman)本身的对称性。旋转群$SO(3)$（在量子力学中你称其表示为角动量）和[狭义相对论](@keyword=special_relativity_theory|lang=zh-CN|style=Feynman)的[洛伦兹群](@keyword=lorentz_group|lang=zh-CN|style=Feynman)$SO(1,3)$都是[李群](@keyword=lie_groups|lang=zh-CN|style=Feynman)。它们的[不可约表示](@keyword=irreducible_representations|lang=zh-CN|style=Feynman)根据粒子的内禀自旋来对粒子进行分类，而自旋是一个根本性的量子力学属性。

### 在其他科学中的回响

故事并未在基础物理学中结束。表示论的回响遍布整个科学领域。

在**凝聚态物理学**中，[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)的对称性决定了在其中运动的电子的行为，从而导致[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)的形成。这些对称性的表示方式决定了材料的电子和磁性，从绝缘体到[超导体](@keyword=superconductor|lang=zh-CN|style=Feynman)。

在**[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)**中，分子的形状由一个[对称群](@keyword=symmetry_groups|lang=zh-CN|style=Feynman)描述。[表示论](@keyword=representation_theory|lang=zh-CN|style=Feynman)是理解[分子振动](@keyword=molecular_vibrations|lang=zh-CN|style=Feynman)模式（决定其红外光谱）和其[电子轨道](@keyword=electron_orbitals|lang=zh-CN|style=Feynman)（支配其化学反应性）的基本工具。理解一个表示如何分解，能让化学家预测哪些[光谱跃迁](@keyword=spectroscopic_transitions|lang=zh-CN|style=Feynman)是允许的，哪些是禁戒的。

从原子核的中心到晶体的结构，从宇宙的黎明到[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)的形成，[李群表示](@keyword=lie_groups_representation|lang=zh-CN|style=Feynman)论提供了一条统一的线索。它揭示了自然并非一堆互不相干的事实的无序堆砌，而是一幅由对称性之线编织而成的壮丽织锦，通过理解它的模式，我们离理解整体更近了一步。