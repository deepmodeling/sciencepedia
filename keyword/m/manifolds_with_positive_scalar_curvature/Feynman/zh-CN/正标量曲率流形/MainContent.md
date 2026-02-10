## 引言
是什么基本规则支配着空间的形态？任何抽象的形状或“[流形](@keyword=manifold|lang=zh-CN|style=Feynman)”都能被赋予一种像球面那样平均来看是正弯曲的几何结构吗？还是说某些形状内在地抗拒这种结构？这个[微分几何](@keyword=differential_geometry|lang=zh-CN|style=Feynman)中的核心问题——研究具有[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)（PSC）的[流形](@keyword=manifold|lang=zh-CN|style=Feynman)——正处于拓扑学、分析学和物理学一个非凡的[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)点上。它挑战我们去理解一个空间的整体“形状”与其所能支撑的局部“弯曲”之间深刻而又常常出人意料的相互作用。

几十年来，数学家们一直在寻求对哪些[流形](@keyword=manifold|lang=zh-CN|style=Feynman)承认PSC度量进行分类，这项探索揭示了关于宇宙可能存在的几何形式的深邃真理。本文将引领读者探索这一研究的全景，梳理其涌现出的关键原理、强大技术以及惊人应用。我们将首先探讨支配PSC的核心“原理与机制”，从[Yamabe问题](@keyword=yamabe_problem|lang=zh-CN|style=Feynman)的共形观点到[自旋几何](@keyword=spin_geometry|lang=zh-CN|style=Feynman)的强大障碍定理，再到几何手术的构造艺术。随后，我们将开启一段“应用与跨学科联系”的旅程，发现这个看似抽象的几何条件如何对爱因斯坦的广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)、弦理论乃至[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学产生深远影响。读毕本文，读者将对为何[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的研究是现代几何学的基石，同时也是理解现实构造的重要工具有一个全面的认识。

## 原理与机制

想象你是一位宇宙雕塑家，你的材料是[时空](@keyword=space_time|lang=zh-CN|style=Feynman)本身。然而，你的工具并不允许你随心所欲地雕刻任何形状。几何学的法则本身就对哪些形式是可能的、哪些是被禁止的施加了深刻的限制。研究具有**[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)**的[流形](@keyword=manifold|lang=zh-CN|style=Feynman)正是这样一种探索：一场理解哪些形状，即“[流形](@keyword=manifold|lang=zh-CN|style=Feynman)”，可以被赋予一种在每一点上平均都是正弯曲的几何结构（像球面那样）的旅程。

在我们对这个宏大问题进行介绍之后，现在让我们深入探讨支配空间形状（其拓扑）与其所能支撑的几何结构（其度量）之间迷人相互作用的原理和机制。我们将看到数学家们如何发展出强大的工具，这些工具不仅能回答“是”或“否”，还能揭示几何、分析和拓扑之间深刻而美丽的统一性。

### 共形观点：放大镜下的宇宙

操控几何最自然的方式之一是拉伸它。想象你有一张画在橡胶薄膜上的地图。你可以拉伸和收缩薄膜的不同部分，这会改变距离和面积，但不会改变相交线之间的角度。这种变换被称为**共形变换**。如果你最初的度量（测量距离的规则）是$g$，一个与之共形相关的度量形如$\tilde{g} = u^{\frac{4}{n-2}}g$，其中$u$是空间中某个正函数，$n$是维度（$n \ge 3$）。函数$u$的作用就像一个放大倍率随点变化的放大镜。

一个深刻的问题，即**[Yamabe问题](@keyword=yamabe_problem|lang=zh-CN|style=Feynman)**（由Hidehiko Yamabe提出），问道：在闭[流形](@keyword=manifold|lang=zh-CN|style=Feynman)上任意给定的共形度量族中，我们是否总能找到一个在某种意义上“最好”的度量？经过包括Neil Trudinger、[Thierry Aubin](@keyword=thierry_aubin|lang=zh-CN|style=Feynman)和[Richard Schoen](@keyword=richard_schoen|lang=zh-CN|style=Feynman)在内的数学家们几十年的努力，答案是肯定的。对于任何一个起始度量，你总能找到一个具有*常*标量曲率的共形“亲戚”。

这简直不可思议。就好像无论你最初的橡胶薄膜的曲率如何褶皱和不均匀，你总能以恰当的方式拉伸它，使得“[平均曲率](@keyword=mean_curvature|lang=zh-CN|style=Feynman)”在每一点都相同。这个[常曲率](@keyword=constant_curvature|lang=zh-CN|style=Feynman)的符号——正、负或零——是整个共形族的指纹。

这为我们提供了一个强大的工具。要判断一个[流形](@keyword=manifold|lang=zh-CN|style=Feynman) $M$ 是否能具有任何[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)（PSC）度量，我们可以考察在每个共形族中能达到的“最佳”[常标量曲率](@keyword=constant_scalar_curvature|lang=zh-CN|style=Feynman)，然后取遍所有可能的共形族后的[上确界](@keyword=least_upper_bound|lang=zh-CN|style=Feynman)。这个数是该[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的一个基本拓扑不变量，称为**[Yamabe不变量](@keyword=yamabe_invariant|lang=zh-CN|style=Feynman)**或**sigma[不变量](@keyword=invariant|lang=zh-CN|style=Feynman)**，记作 $\sigma(M)$。核心结果异常简洁：一个[流形](@keyword=manifold|lang=zh-CN|style=Feynman) $M$ 承认[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)度量，当且仅当其[Yamabe不变量](@keyword=yamabe_invariant|lang=zh-CN|style=Feynman)为正，即 $\sigma(M) > 0$。[@problem_id:3005238] [@problem_id:3005242]

然而，这种方法有一个局限性。解决[Yamabe问题](@keyword=yamabe_problem|lang=zh-CN|style=Feynman)的[共形因子](@keyword=conformal_factor|lang=zh-CN|style=Feynman)$u$是一个遍及整个[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的全局方程的解。这意味着你不能仅仅通过一个局部的共形微调来修[复流形](@keyword=complex_manifolds|lang=zh-CN|style=Feynman)上曲率为负的某个“丑陋”的小块区域。这种改变的涟漪效应会波及各处。这是由于其底层的[椭圆方程](@keyword=equation_of_an_ellipse|lang=zh-CN|style=Feynman)所具有的强[唯一延拓](@keyword=unique_extension|lang=zh-CN|style=Feynman)原理所致；你根本无法将改变限制在一个小区域内。[@problem_id:3035429] [共形变换](@keyword=conformal_transformations|lang=zh-CN|style=Feynman)是一个全局工具，而非局部手术刀。

### “行不通”定理：拓扑路障

如果[Yamabe不变量](@keyword=yamabe_invariant|lang=zh-CN|style=Feynman)是守门人，那么[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的什么性质可能会将大门关上，确保 $\sigma(M) \le 0$？答案见于现[代数学](@keyword=algebra|lang=zh-CN|style=Feynman)中一些最令人惊叹的结果，它们就像“行不通”定理。这些定理揭示了[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的底层拓扑——其基本形状——可以成为[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的刚性障碍。

其中一个最优雅的障碍适用于一类称为**[自旋流形](@keyword=spin_manifolds|lang=zh-CN|style=Feynman)**的特殊[流形](@keyword=manifold|lang=zh-CN|style=Feynman)。粗略地说，这些空间上可以一致地定义“旋量”，物理学家用[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)来描述像电子这样的粒子。在这类[流形](@keyword=manifold|lang=zh-CN|style=Feynman)上，存在一个称为**Dirac算子**的基本算子$D$，可以被看作是[拉普拉斯算子](@keyword=divergence_of_the_gradient|lang=zh-CN|style=Feynman)的一种“平方根”。

神奇之处在于伟大的法国数学家André Lichnerowicz发现的一个公式。对于任何[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)场$\psi$，**[Lichnerowicz公式](@keyword=lichnerowicz_formula|lang=zh-CN|style=Feynman)**表明：

$$D^2 \psi = \nabla^*\nabla \psi + \frac{1}{4} R_g \psi$$

这里，$\nabla^*\nabla$ 是一个恒非负的项（就像速度的平方），而 $R_g$ 是我们的[标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman)。现在，我们来玩一个游戏。假设我们的[流形](@keyword=manifold|lang=zh-CN|style=Feynman)*确实*有一个具有[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的度量，因此 $R_g > 0$ 处处成立。如果我们寻找一个“调和旋量”，即满足 $D\psi = 0$ 的特殊状态 $\psi$，会发生什么？

如果 $D\psi=0$，那么自然有 $D^2\psi=0$。让我们在整个[流形](@keyword=manifold|lang=zh-CN|style=Feynman)上对[Lichnerowicz公式](@keyword=lichnerowicz_formula|lang=zh-CN|style=Feynman)进行积分。经过一些分部积分后，该方程基本上说的是：

$$0 = ( \text{一个来自}\ \nabla\psi\ \text{的非负项} ) + ( \text{一个包含}\ \frac{1}{4}R_g|\psi|^2\ \text{的积分项} )$$

因为我们假设 $R_g > 0$，第二项是一堆正数的和，也必须是非负的。两个非负数之和为零的唯一可能是两者都为零。为了使第二项为零，[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)场 $\psi$ 必须处处为零。[@problem_id:1027182]

因此，结论是无可避免的：**一个具有[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的[自旋流形](@keyword=spin_manifolds|lang=zh-CN|style=Feynman)不能有任何非平凡的调和旋量。**

这又如何？关键在于此。传奇的**Atiyah-Singer[指数定理](@keyword=index_theorems|lang=zh-CN|style=Feynman)**指出，独立调和旋量解的数量（Dirac算子的指数）是一个纯粹的拓扑不变量——一个只依赖于[流形](@keyword=manifold|lang=zh-CN|style=Feynman)形状而不依赖于度量的数。这个数被称为**Â-亏格**，记作 $\hat{A}(M)$。

我们刚刚见证了数学推理的一个奇迹。
1.  **几何学：** 假设 $R_g > 0$。
2.  **分析学：** [Lichnerowicz公式](@keyword=lichnerowicz_formula|lang=zh-CN|style=Feynman)意味着不存在非平凡的调和旋量。
3.  **拓扑学：** Atiyah-Singer定理继而迫使[拓扑不变量](@keyword=topological_invariants|lang=zh-CN|style=Feynman)为零：$\hat{A}(M) = 0$。

因此，如果一个[自旋流形](@keyword=spin_manifolds|lang=zh-CN|style=Feynman)的Â-亏格非零，那么它就绝对、断然地被禁止承认任何[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的度量。例如，被称为**[K3曲面](@keyword=k3_surface|lang=zh-CN|style=Feynman)**的复[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)是一个[自旋流形](@keyword=spin_manifolds|lang=zh-CN|style=Feynman)，其Â-亏格可以计算出为 $2$。因此，我们可以确定，无论你如何尝试弯曲或塑造它，你永远无法使一个[K3曲面](@keyword=k3_surface|lang=zh-CN|style=Feynman)处处都具有[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)。[@problem_id:3035397]

这只是这类障碍中的一个。更高级的理论，如针对4维[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的**[Seiberg-Witten理论](@keyword=seiberg_witten_theory|lang=zh-CN|style=Feynman)**[@problem_id:1021741]和针对具有复杂[基本群](@keyword=fundamental_group|lang=zh-CN|style=Feynman)[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的**Rosenberg指数**[@problem_id:3005242]，提供了更深刻、更微妙的障碍。空间的形状确实会进行反抗。

### 手术的艺术：用正曲率进行构造

虽然某些形状被禁止，但许多其他形状是被允许的。我们如何在这些[流形](@keyword=manifold|lang=zh-CN|style=Feynman)上构造PSC度量？Mikhail Gromov和H. Blaine Lawson Jr.提供了一种革命性的技术：**几何手术**。

想象你有一个已经具有PSC度量的[流形](@keyword=manifold|lang=zh-CN|style=Feynman) $M$。其思想是切掉 $M$ 的一部分，然后粘进一个新的部分来创造一个新的[流形](@keyword=manifold|lang=zh-CN|style=Feynman) $M'$。问题是，我们能否在施行这个手术后，使得新[流形](@keyword=manifold|lang=zh-CN|style=Feynman) $M'$ 也具有PSC度量？**[Gromov-Lawson手术](@keyword=gromov_lawson_surgery|lang=zh-CN|style=Feynman)定理**给出的答案是响亮的“是”，但有一个关键条件：手术必须在**[余维数](@keyword=codimension|lang=zh-CN|style=Feynman)至少为3**的情况下进行。

让我们来解释一下。手术通常涉及移除一个加厚的球面 $S^p \times D^q$ 并粘入一个“柄” $D^{p+1} \times S^{q-1}$。这里的“[余维数](@keyword=codimension|lang=zh-CN|style=Feynman)”是$q$。该定理说，如果$q \ge 3$，那么这个保持PSC的技巧是可行的。为什么是3这个神奇的数字？[@problem_id:3002802]

原因非常具有几何性，可以通过检查粘合发生的“颈部”区域来理解。颈部的度量可以被建模为一个扭曲乘积 $dr^2 + a(r)^2 g_{S^p} + b(r)^2 g_{S^{q-1}}$。其[标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman)公式包含三类项：$S^p$ 球面的[内蕴曲率](@keyword=intrinsic_curvature|lang=zh-CN|style=Feynman)、$S^{q-1}$ 球面的内蕴曲率，以及与颈部“弯曲”相关的项（扭曲函数$a(r)$和$b(r)$的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)）。维度为$k$的球面的[内蕴曲率](@keyword=intrinsic_curvature|lang=zh-CN|style=Feynman)大约是$k(k-1)$。

因此，来自$S^{q-1}$因子的内蕴曲率项与$(q-1)(q-2)$成正比。
*   如果[余维数](@keyword=codimension|lang=zh-CN|style=Feynman)$q \ge 3$，那么$q-1 \ge 2$，项$(q-1)(q-2)$严格为正。该项以$1/b(r)^2$的方式缩放，意味着当我们将颈部做得非常细时，它会成为一个巨大的[正曲率](@keyword=positive_curvature|lang=zh-CN|style=Feynman)来源。这个正的“缓冲”可以用来压倒由弯曲引入的任何[负曲率](@keyword=negative_curvature|lang=zh-CN|style=Feynman)。
*   但如果[余维数](@keyword=codimension|lang=zh-CN|style=Feynman)是$q=2$（一个圆周$S^1$）或$q=1$（两个点$S^0$），因子$(q-1)(q-2)$就为零！$S^1$和$S^0$的[内蕴曲率](@keyword=intrinsic_curvature|lang=zh-CN|style=Feynman)为零。这个起着决定性作用的[正曲率](@keyword=positive_curvature|lang=zh-CN|style=Feynman)缓冲消失了。来自弯曲的负项可能占主导地位，通常就不可能维持[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)了。[@problem_id:3035458]

这表明手术的成功并非魔术，而是[球面几何](@keyword=sphere_geometry|lang=zh-CN|style=Feynman)的直接结果。与全局的[共形方法](@keyword=conformal_method|lang=zh-CN|style=Feynman)不同，手术是一种**局部**操作。构造出的度量可以在手术位置的任意小邻域之外与原始度量完全相同。[@problem_id:3035429]

低[余维数](@keyword=codimension|lang=zh-CN|style=Feynman)手术的失败也与Schoen和Yau开创的另一系列障碍有关。他们证明了PSC[流形](@keyword=manifold|lang=zh-CN|style=Feynman)不能包含某些类型的稳定“极小曲面”（肥[皂膜](@keyword=soap_film|lang=zh-CN|style=Feynman)的高维类似物）。事实证明，在余维1和2中进行的手术恰恰是那种倾向于产生这些被禁止的[极小曲面](@keyword=minimal_surfaces|lang=zh-CN|style=Feynman)的操作，为它们的失败提供了另一个更全局性的原因。[@problem_id:3033326]

### 一个更丰富的宇宙：超越简单的“是”或“否”

标量曲率的全貌远比一个简单的存在性“是/否”问题丰富得多。例如，[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)条件比更强的**正Ricci曲率**条件要灵活得多。对于一个[3-流形](@keyword=3_manifolds|lang=zh-CN|style=Feynman)，正[Ricci曲率](@keyword=ricci_curvature|lang=zh-CN|style=Feynman)迫使该[流形](@keyword=manifold|lang=zh-CN|style=Feynman)成为一个“球面[空间形式](@keyword=space_forms|lang=zh-CN|style=Feynman)”（一个球面或其商空间），其[基本群](@keyword=fundamental_group|lang=zh-CN|style=Feynman)是有限的。[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)是否也如此呢？

答案是否定的。考虑[流形](@keyword=manifold|lang=zh-CN|style=Feynman) $S^2 \times S^1$，即一个球面和一个圆的乘积。我们可以通过取 $S^2$ 上的[常曲率度量](@keyword=constant_curvature_metrics|lang=zh-CN|style=Feynman)和 $S^1$ 上的平直度量的乘积，来赋予它一个具有[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的度量。球面的正曲率足以使[总曲率](@keyword=total_curvature|lang=zh-CN|style=Feynman)为正。然而，$S^2 \times S^1$ 的基本群是无限的整数群 $\mathbb{Z}$。因此，这里我们有一个具有[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的[流形](@keyword=manifold|lang=zh-CN|style=Feynman)，它在拓扑上与球面非常不同。[@problem_id:2978484] 利用手术，我们可以将这个对象附加到任何其他PSC[流形](@keyword=manifold|lang=zh-CN|style=Feynman)上，以创建具有无限基本群的更复杂的例子。[@problem_id:2978484]

最终的问题可能是：如果一个[流形](@keyword=manifold|lang=zh-CN|style=Feynman)*确实*承认PSC度量，那么有多少种呢？它们都是连通的吗？你能通过一条PSC度量路径将任何PSC度量[连续形变](@keyword=continuous_deformation|lang=zh-CN|style=Feynman)为任何其他PSC度量吗？答案惊人地是否定的。源于与代数拓扑学分支[K-理论](@keyword=k_theory|lang=zh-CN|style=Feynman)的深刻联系，一些结果表明，对于某些[流形](@keyword=manifold|lang=zh-CN|style=Feynman)，所有PSC度量的空间是不连通的。它由一些独立的“岛屿”组成。例如，在8-球面上 $S^8$，恰好存在两个[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)度量的岛屿。一个岛屿上的度量永远无法形变到另一个岛屿上的度量，而不在形变过程中的某个地方违反正弯曲的条件。[@problem_id:932782]

从一个简单的几何问题——这个形状能否被正向弯曲？——我们穿越了[全局分析](@keyword=global_analysis|lang=zh-CN|style=Feynman)、[算子理论](@keyword=operator_theory|lang=zh-CN|style=Feynman)和代数拓扑，揭示了一个拥有惊人复杂性和深刻联系的宇宙。对[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的探索证明了数学揭示支配空间构造的隐藏而刚性规则的力量。