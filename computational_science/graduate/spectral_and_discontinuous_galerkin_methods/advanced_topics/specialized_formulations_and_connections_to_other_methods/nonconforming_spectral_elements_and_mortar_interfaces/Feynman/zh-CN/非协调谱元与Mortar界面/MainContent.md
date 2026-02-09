## 引言
在高阶数值模拟领域，谱元法因其卓越的精度而备受青睐。然而，为了高效地模拟具有复杂几何或多尺度物理现象的问题，我们常常需要在计算区域内使用尺寸或多项式阶次不尽相同的网格，即[非协调网格](@keyword=non_conforming_meshes|lang=zh-CN|style=Feynman)。这种灵活性带来了新的挑战：在这些不匹配的网格单元边界上，传统的连续性假设被打破，我们如何才能在保证数值解的稳定与精确的同时，将它们“无缝”地粘合起来？本文旨在系统性地解答这一问题，核心工具便是“[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)”（Mortar Method）——一种强大而优雅的数学框架，用于在非协调界面上施加[弱形式](@keyword=weak_formulation|lang=zh-CN|style=Feynman)的连续性约束。

本文将分为三个部分，带领读者全面掌握这一关键技术。在“原理与机制”一章中，我们将深入剖析非协调性的本质，并详细拆解[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)作为[弱耦合](@keyword=weak_coupling|lang=zh-CN|style=Feynman)方式的工作原理，包括其核心的$L^2$投影、拉格朗日乘子以及稳定性考量。接着，在“应用与[交叉](@keyword=chiasmata|lang=zh-CN|style=Feynman)学科联系”一章中，我们将展示[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)如何在[高性能计算](@keyword=high_performance_computing|lang=zh-CN|style=Feynman)、[流体力学](@keyword=fluid_dynamics|lang=zh-CN|style=Feynman)和计算机图形学等前沿领域中发挥作用，解决实际工程与科学问题。最后，通过“动手实践”部分提供的具体计算练习，读者将有机会亲手实现和分析砂浆耦合系统，将理论知识转化为实践能力。让我们一同开启这段探索之旅，揭开非协调谱元与砂浆界面背后的数学之美与工程智慧。

## 原理与机制

在上一章中，我们领略了非协调谱元法的魅力——它赋予了我们在复杂几何与多物理场问题中进行精细模拟的自由。但是，这种自由并非没有代价。当我们允许网格单元在尺寸（$h$）、多项式阶次（$p$）甚至节点[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)上彼此“失配”时，我们便打破了传统有限元方法赖以生存的基石：**全局连续性**。函数在单元边界上不再严丝合缝，而是可能出现“跳跃”。那么，我们该如何驾驭这种不连续性，既享受网格剖分的自由，又能保证数值解的稳定和精确呢？这便是“[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)”（Mortar Method）登场的舞台。它是一种巧妙的数学艺术，用于在失配的界面上“抹上”一层数学的砂浆，将本已分离的单元重新牢固地粘合在一起。

本章将深入这些核心原理，像剥洋葱一样层层揭开其背后的机制。我们将从“为什么需要非协调”这个问题出发，探索[不连续性](@keyword=discontinuity|lang=zh-CN|style=Feynman)的本质，然后详细拆解[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)是如何作为一种“弱”连接方式工作的，并最终将其置于更广阔的数值方法图景中，揭示其内在的美与统一性。

### [协调网格](@keyword=conforming_mesh|lang=zh-CN|style=Feynman)的“束缚”与“自由”

想象一下用标准的乐高积木搭建模型。每一块积木都完美契合，连接处天衣无缝。这就是**[协调网格](@keyword=conforming_mesh|lang=zh-CN|style=Feynman)（Conforming Mesh）**的世界。在数学上，这意味着整个计算区域上的离散[函数空间](@keyword=function_spaces|lang=zh-CN|style=Feynman)是**$H^1$协调**的——任何一个离散函数在整个区域内都是连续的，它的“跳跃”为零。这种协调性是美好而简单的，它保证了[变分形式](@keyword=variational_formulation|lang=zh-CN|style=Feynman)的直接适用性，并且易于实现。

例如，在一个简单的一维问题中，假设我们用两个谱元 $[-1, 0]$ 和 $[0, 1]$ 拼接。即便左单元使用4阶多项式，右单元使用2阶，我们依然可以轻松实现协调连接 [@problem_id:3403332]。为什么？因为它们的界面仅仅是一个点：$x=0$。两个单元都在这个点上拥有一个节点，我们只需强制这两个节点上的函数值相等，即可实现连续性。在这种情况下，总的自由度就是两个单元自由度之和减去1（因为一个约束合并了两个自由度）。

然而，现实世界的物理问题远比这复杂。想象一下模拟飞机机翼周围的空气流动。在靠近机翼表面的[边界层](@keyword=boundary_layer|lang=zh-CN|style=Feynman)，流场变量梯度极大，变化剧烈，我们需要极高的分辨率来捕捉这些细节。而在远离机翼的区域，流场则平缓得多。如果我们坚持使用全局统一的精细网格，无疑会在[远场区](@keyword=far_zone|lang=zh-CN|style=Feynman)域浪费大量的计算资源。

为了效率，我们渴望**自适应性（Adaptivity）**——在需要的地方加密网格，在不需要的地方使用粗疏网格。这种需求催生了两种主要的[网格加密](@keyword=mesh_refinement|lang=zh-CN|style=Feynman)策略：
- **$h$-自适应**：减小单元的尺寸。
- **$p$-自适应**：提高单元内多项式的阶次。

当我们采用这些策略时，完美的乐高世界便不复存在。一个大单元旁边可能会紧邻着两个或多个小单元，一个[高阶单元](@keyword=higher_order_elements|lang=zh-CN|style=Feynman)旁边可能是个低阶单元。这种“失配”打破了网格的协调性，我们进入了**[非协调网格](@keyword=non_conforming_meshes|lang=zh-CN|style=Feynman)（Nonconforming Mesh）**的世界。这虽然带来了挑战，但也赋予了我们前所未有的模拟自由。

### 失配的剖析：什么是[非协调网格](@keyword=non_conforming_meshes|lang=zh-CN|style=Feynman)？

“非协调”或“不连续”究竟意味着什么？让我们来解剖一个典型的失配界面。当两个单元的离散函数空间无法在共享界面上实现逐点匹配时，非协调性就产生了。这主要源于以下三种情况 [@problem_id:3403313]：

- **几何非协调 (Geometric Nonconformity)**：这是最直观的一种失配。当一个大单元的边与两个或更多小单元的边对齐时，小单元共享的顶点会落在大单元边的内部。这个无处连接的节点被称为**[悬挂节点](@keyword=dangling_nodes|lang=zh-CN|style=Feynman) (Hanging Node)** [@problem_id:3403318]。这就像试图将一块大砖和两块小砖砌在一起，中间必然会出现一条无法对齐的缝。

- **多项式次数非协调 ($p$-Nonconformity)**：即使单元在几何上是匹配的（一条边对一条边），但如果它们内部使用的[多项式逼近](@keyword=polynomial_approximation|lang=zh-CN|style=Feynman)阶次不同，例如左边是5阶，右边是3阶，那么它们在界面上的迹[函数空间](@keyword=function_spaces|lang=zh-CN|style=Feynman)也不同。左边的迹函数是一个5次多项式，而右边是一个3次多项式。一个5次多项式通常无法被一个3次多项式完美表示，因此无法保证在界面上处处相等。

- **节点非协调 (Nodal Nonconformity)**：这是更微妙的一种情况。谱元法通常使用一系列特定的节点（如[Gauss-Lobatto-Legendre节点](@keyword=gauss_lobatto_legendre_nodes|lang=zh-CN|style=Feynman)）来定义单元上的[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)。这些节点的位置取决于多项式的阶次。即使两个相邻单元的多项式阶次相同，如果它们使用的节点类型不同（例如，一个用Gauss-Lobatto节点，另一个用Gauss节点），或者由于$p$-非协调导致节点[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)不匹配，那么除了共有的顶点外，它们在界面内部的节点也无法一一对应。

在二维或三维空间中，单元间的界面是一条[线或](@keyword=wired_or|lang=zh-CN|style=Feynman)一个面，拥有无限多的点。上述任何一种失配都意味着我们无法再通过简单地等同界面上的节点值来强制实现连续性。其根本后果是，拼装起来的全局离散[函数空间](@keyword=function_spaces|lang=zh-CN|style=Feynman)不再是$H^1(\Omega)$的[子空间](@keyword=subspace|lang=zh-CN|style=Feynman)，函数在界面上产生了“跳跃”，传统的变分原理似乎失效了。

### [砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)的妥协艺术

面对这个“破碎”的[函数空间](@keyword=function_spaces|lang=zh-CN|style=Feynman)，我们该何去何从？是花费巨大代价去构造复杂的过渡单元以恢复协调性，还是有更聪明的办法？[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)提供了一种优雅的妥协方案。它的核心思想是：**既然无法保证在界面上“处处相等”（强连续性），那我们就退而求其次，要求它们在“平均意义上”相等（弱连续性）。**

让我们通过一个模型问题——泊松方程——来理解这个思想 [@problem_id:3403320]。假设我们要解$-\Delta u = f$。其标准的弱形式要求在整个区域上积分。当区域被分解成互不重叠的[子域](@keyword=subfield|lang=zh-CN|style=Feynman)$\Omega_k$后，我们可以先在每个子域内进行分部积分。这会产生一系列边界积分项。对于内部界面$\Gamma$，相邻的两个单元$\Omega^+$和$\Omega^-$都会贡献一个边界项。为了将它们重新耦合起来，[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)引入了一个全新的数学实体：定义在界面$\Gamma$上的**砂浆空间 (Mortar Space)** $M_h(\Gamma)$，它通常也是一个多项式空间。

弱连续性条件被表述为一个积分约束：对于任意一个取自砂浆空间的“[检验函数](@keyword=test_functions|lang=zh-CN|style=Feynman)”$\mu_h \in M_h(\Gamma)$，函数在界面上的跳跃值$[u_h] = u_h|_{+} - u_h|_{-}$必须与其正交。
$$
\int_{\Gamma} [u_h] \, \mu_h \, \mathrm{d}s = 0, \quad \forall \mu_h \in M_h(\Gamma)
$$
这个公式是什么意思？如果取$\mu_h=1$（假设[常数函数](@keyword=constant_function|lang=zh-CN|style=Feynman)在$M_h(\Gamma)$中），这个条件就意味着函数在界面上跳跃的积分为零，即平均跳跃为零。如果$M_h(\Gamma)$包含更高阶的多项式，这个条件就意味着跳跃对这些高阶“矩”的正交，这是一个更强的约束。

为了在[变分问题](@keyword=variational_problems|lang=zh-CN|style=Feynman)中施加这个约束，我们引入了**拉格朗日乘子 (Lagrange Multiplier)** $\lambda_h \in M_h(\Gamma)$。这个乘子本身也成了我们要求解的未知量之一，它在物理上通常可以解释为穿过界面的通量（例如热流或应力）[@problem_id:3403320]。最终，我们得到一个所谓的**[鞍点问题](@keyword=saddle_point_problems|lang=zh-CN|style=Feynman) (Saddle-Point Problem)** [@problem_id:3403365]，需要同时求解原始变量$u_h$和乘子变量$\lambda_h$。这种方法虽然增加了未知量，但它为连接完全不同的[离散空间](@keyword=discrete_space|lang=zh-CN|style=Feynman)提供了一个坚实而灵活的数学框架。

### 细节是魔鬼：让[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)运转起来

抽象的原理固然优美，但要让[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)在计算机中高效运转，还需解决一系列关键的实现问题。

#### 代数之核：$L^2$[投影算子](@keyword=projection_operators|lang=zh-CN|style=Feynman)

[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)的核心操作是将一个单元在界面上的迹函数“投影”到另一个单元的迹[函数空间](@keyword=function_spaces|lang=zh-CN|style=Feynman)（或者一个中立的砂浆空间）上。这个操作在代数上是如何实现的呢？

假设我们要将“精细”边（fine side）的迹函数$u_f$投影到“粗糙”边（coarse side）的[迹空间](@keyword=trace_spaces|lang=zh-CN|style=Feynman)$V_h^{\mathrm{coarse}}$上，得到$u_c$。根据弱连续性定义，我们要求投影误差$u_c - u_f$与粗糙边[迹空间](@keyword=trace_spaces|lang=zh-CN|style=Feynman)中的任何函数$v_c$都$L^2$正交：
$$
\int_{\Gamma} (u_c - u_f) v_c \, \mathrm{d}\Gamma = 0, \quad \forall v_c \in V_h^{\mathrm{coarse}}
$$
将$u_c$和$u_f$分别用各自空间的[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)展开，并代入上式，经过一番推导，我们就能得到一个纯粹的线性代数关系 [@problem_id:3403347]：
$$
\mathbf{u}_c = \mathbf{P} \, \mathbf{u}_f
$$
这里的$\mathbf{u}_c$和$\mathbf{u}_f$是函数在各自基底下展开的系数向量。$\mathbf{P}$就是大名鼎鼎的**[投影算子](@keyword=projection_operators|lang=zh-CN|style=Feynman) (Projection Operator)**，它可以表示为：
$$
\mathbf{P} = \mathbf{M}_c^{-1} \mathbf{B}
$$
其中，$\mathbf{M}_c$是粗糙边[迹空间](@keyword=trace_spaces|lang=zh-CN|style=Feynman)的**[质量矩阵](@keyword=mass_matrix|lang=zh-CN|style=Feynman)**（即[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)之间的[内积](@keyword=interior_product|lang=zh-CN|style=Feynman)矩阵），而$\mathbf{B}$是连接两个空间的**耦合[质量矩阵](@keyword=mass_matrix|lang=zh-CN|style=Feynman)**（即粗糙边[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)与精细边[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)的[内积](@keyword=interior_product|lang=zh-CN|style=Feynman)矩阵）。这个投影算子是[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)的计算核心，它将高维信息（来自$u_f$）以一种保持关键积分性质的方式“压缩”到低维空间（生成$u_c$）。

#### 基底的选择：[节点基](@keyword=nodal_basis|lang=zh-CN|style=Feynman) vs. 模式基

构造砂浆空间$M_h(\Gamma)$时，选择什么样的[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)至关重要，这直接影响到计算的效率和精度 [@problem_id:3403364]。两种主流选择是：

1.  **模式基 (Modal Basis)**：通常选用**[勒让德多项式](@keyword=legendre_polynomials|lang=zh-CN|style=Feynman) (Legendre Polynomials)** $\{P_k\}$。它们在区间$[-1, 1]$上是$L^2$正交的。对于平直界面，这意味着[质量矩阵](@keyword=mass_matrix|lang=zh-CN|style=Feynman)$\mathbf{M}_c$是一个对角阵！这是一个巨大的优势，因为[对角矩阵](@keyword=diagonal_matrix|lang=zh-CN|style=Feynman)的[逆矩阵](@keyword=matrix_inverse|lang=zh-CN|style=Feynman)求解易如反掌，使得投影计算极其高效。

2.  **[节点基](@keyword=nodal_basis|lang=zh-CN|style=Feynman) (Nodal Basis)**：通常选用与Gauss-Lobatto-Legendre (GLL)节点相关联的**[拉格朗日多项式](@keyword=lagrange_polynomials|lang=zh-CN|style=Feynman) (Lagrange Polynomials)**。这套[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)不具备$L^2$正交性，导致在精确积分下，[质量矩阵](@keyword=mass_matrix|lang=zh-CN|style=Feynman)$\mathbf{M}_c$是稠密的，并且随着多项式阶次$p$的增加，其条件数会快速恶化（按$\mathcal{O}(p^2)$增长），给求解带来困难。

有趣的是，工程师们发现了一个“捷径”：如果使用与GLL[节点基](@keyword=nodal_basis|lang=zh-CN|style=Feynman)完全对应的GLL[求积公式](@keyword=quadrature_rules|lang=zh-CN|style=Feynman)来近似计算质量矩阵的积分，由于[拉格朗日基](@keyword=lagrange_basis|lang=zh-CN|style=Feynman)函数在节点上的取值特性（只在一个节点上为1，其余为0），算出来的[质量矩阵](@keyword=mass_matrix|lang=zh-CN|style=Feynman)竟然也是对角阵！这种技术被称为**[质量集中](@keyword=mass_lumping|lang=zh-CN|style=Feynman) (Mass Lumping)**。它虽然引入了[积分误差](@keyword=integration_error|lang=zh-CN|style=Feynman)（因为GLL求积对两个$p$阶多项式之积并非精确），但换来了巨大的计算便利，成为一种非常流行的实用选择。

#### 稳定性的“暗礁”：inf-sup条件

引入[拉格朗日乘子](@keyword=lagrange_multipliers|lang=zh-CN|style=Feynman)虽然巧妙，但也暗藏风险。[鞍点问题](@keyword=saddle_point_problems|lang=zh-CN|style=Feynman)的稳定性不再是自动保证的，它需要满足一个深刻的数学条件——**Babuška-Brezzi (inf-sup) 条件**。我们不必深究其数学细节，但可以用一个直观的例子来理解其精神 [@problem_id:3403330]。

inf-sup条件本质上要求乘[子空间](@keyword=subspace|lang=zh-CN|style=Feynman)$\Lambda_h$（砂浆空间）和[迹空间](@keyword=trace_spaces|lang=zh-CN|style=Feynman)$V_h|_\Gamma$之间必须“兼容”或“势均力敌”。乘[子空间](@keyword=subspace|lang=zh-CN|style=Feynman)不能“过于强大”。如果乘[子空间](@keyword=subspace|lang=zh-CN|style=Feynman)$\Lambda_h$的维度过大，或者说它包含了太多高频信息，以至于[迹空间](@keyword=trace_spaces|lang=zh-CN|style=Feynman)$V_h|_\Gamma$完全“看不见”，那么灾难就会发生。

想象一下，[迹空间](@keyword=trace_spaces|lang=zh-CN|style=Feynman)$V_h|_\Gamma$由1次多项式（直线）构成，而我们奢侈地选择了2次[多项式空间](@keyword=pspace|lang=zh-CN|style=Feynman)作为乘[子空间](@keyword=subspace|lang=zh-CN|style=Feynman)$\Lambda_h$。问题来了：是否存在一个非零的2次多项式$\lambda(s)$，它与所有的1次多项式$v(s)$都$L^2$正交？即$\int_{-1}^1 \lambda(s)v(s)ds = 0$。答案是肯定的！这个多项式正是（除去常数因子）第二个[勒让德多项式](@keyword=legendre_polynomials|lang=zh-CN|style=Feynman)$P_2(s) = \frac{1}{2}(3s^2-1)$，它本身就与所有低阶勒让德多项式（包括$P_0=1$和$P_1=s$）正交。

这个$P_2(s)$就是所谓的**[伪模式](@keyword=spurious_modes|lang=zh-CN|style=Feynman) (Spurious Mode)**。在数值求解中，这个模式可以被任意放大而不会受到弱连续性条件的任何惩罚，因为它对于[迹空间](@keyword=trace_spaces|lang=zh-CN|style=Feynman)来说是“隐形”的。这会导致解中出现剧烈的、非物理的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，从而破坏整个计算的稳定性。因此，选择合适的砂浆空间维度是保证[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)成功的关键一步，通常要求其维度不超过（或经过精心设计以匹配）较弱一侧的[迹空间](@keyword=trace_spaces|lang=zh-CN|style=Feynman)维度。

### 拥抱现实世界：弯曲几何

到目前为止，我们的讨论大多局限在平直的界面上。但真实的工程问题充满了曲线和[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)。[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)如何适应这些复杂的几何呢？答案是**[等参映射](@keyword=isoparametric_mapping|lang=zh-CN|style=Feynman) (Isoparametric Mapping)** [@problem_id:3403359]。

这个思想非常优雅：我们用来逼近未知解的高阶多项式[基函数](@keyword=basis_function|lang=zh-CN|style=Feynman)，同样可以用来描述和逼近几何本身。我们将一个简单的参考单元（如正方形$[-1, 1]^2$）通过一个高阶[多项式映射](@keyword=polynomial_maps|lang=zh-CN|style=Feynman)，将其“弯曲”成物理空间中复杂的形状。

当计算界面上的积[分时](@keyword=time_sharing|lang=zh-CN|style=Feynman)，例如$\int_\Gamma u v \, ds$，我们需要通过变量替换，将其[拉回](@keyword=pullback|lang=zh-CN|style=Feynman)到一维的参考界面$\hat{\Gamma} = [-1, 1]$上进行计算。根据微分几何，物理界面上的微元[弧长](@keyword=length_of_a_curve|lang=zh-CN|style=Feynman)$ds$与参考界面上的微元$d\eta$之间存在一个换算因子，这个因子就是映射的**雅可比 (Jacobian)**——具体来说，是界面切向量的模长。
$$
\int_{\Gamma} u v \, ds = \int_{-1}^{1} (u \circ \mathbf{x}_f)(\eta) \, (v \circ \mathbf{x}_f)(\eta) \, \left\| \frac{\partial \mathbf{x}_f}{\partial \eta}(\eta) \right\| \, d\eta
$$
这里$\mathbf{x}_f(\eta)$是从参考边到物理边的映射。对于弯曲界面，这个[雅可比因子](@keyword=jacobian_factor|lang=zh-CN|style=Feynman)$\left\| \partial \mathbf{x}_f / \partial \eta \right\|$不再是常数，而是随着$\eta$变化的函数。

这个看似简单的改变，却带来了一个深刻的后果。还记得勒让德多项式在平直界面上的完美正交性吗？当乘以一个非恒定的雅可比权重后，这种正交性便荡然无存 [@problem_id:3403364]。这意味着，即使在模式基下，弯曲界面上的[质量矩阵](@keyword=mass_matrix|lang=zh-CN|style=Feynman)也不再是对角阵。这是科学给我们的又一堂“天下没有免费的午餐”的课。为了处理复杂几何，我们牺牲了部分代数上的简洁性。

### 殊途同归：与其他方法的联系

[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)的思想并非孤立存在，它与[数值分析](@keyword=numerical_analysis|lang=zh-CN|style=Feynman)领域的另一大主流方法——**间断Galerkin法 (Discontinuous Galerkin, DG)**——有着深刻的内在联系。DG方法从一开始就允许函数在所有单元边界上是不连续的，并通过精心设计的**数值通量 (Numerical Flux)** 来重新建立单元间的耦合。

如果我们仔细考察一种[DG方法](@keyword=dg_methods|lang=zh-CN|style=Feynman)——对称内部罚函数法(SIPG)，并将其与一种被称为“稳定化[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)”的变体进行比较，会发现惊人的一致性 [@problem_id:3403372]。两种方法的界面耦合项都可以写成三个部分的和：两个与通量相关的[交叉](@keyword=chiasmata|lang=zh-CN|style=Feynman)项，以及一个惩[罚函数](@keyword=penalty_function|lang=zh-CN|style=Feynman)跳跃的项。
- DG方法的惩罚项是$\int_\Gamma \sigma [u][v] \, ds$。
- 稳定化[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)的惩罚项是$\int_\Gamma \tau \Pi([u]) \Pi([v]) \, ds$，其中$\Pi$是到砂浆空间的投影。

可以证明，如果选择砂浆空间与DG的[迹空间](@keyword=trace_spaces|lang=zh-CN|style=Feynman)完全相同（此时投影算子$\Pi$变为[恒等算子](@keyword=identity_operator|lang=zh-CN|style=Feynman)），并且令罚参数相等（$\sigma = \tau$），那么这两种方法在界面上的数学表达将变得**完[全等](@keyword=congruences|lang=zh-CN|style=Feynman)价**！

这一发现揭示了自然规律的某种统一性：不同的方法，从不同的哲学出发（[砂浆法](@keyword=mortar_methods|lang=zh-CN|style=Feynman)试图“修复”不连续性，DG法“拥抱”不连续性），最终为了达到稳定和精确的耦合，殊途同归，发展出了形式上几乎一致的数学结构。理解了这一点，我们便不再将它们看作是孤立的技巧，而是通往高效数值模拟这一共同目标的不同路径。