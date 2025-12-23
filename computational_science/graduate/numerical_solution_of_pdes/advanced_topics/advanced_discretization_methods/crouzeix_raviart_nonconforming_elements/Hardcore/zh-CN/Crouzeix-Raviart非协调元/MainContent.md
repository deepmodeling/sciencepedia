## 引言
在求解[偏微分方程的数值方法](@entry_id:143514)中，有限元法（FEM）是一种极其强大和通用的工具。传统有限元分析通常依赖于**协调单元**，其构造的[函数空间](@entry_id:143478)是精确解所在空间的[子空间](@entry_id:150286)，保证了全局的连续性。然而，这种严格的连续性要求在处理某些特定问题，如不可压缩流体或接触问题时，可能导致数值不稳定或实现复杂。这促使研究者们探索更为灵活的离散化方案，即**[非协调有限元法](@entry_id:752621)**。

本文旨在深入剖析非[协调有限元](@entry_id:170866)中最具代表性和基础性的例子——**Crouzeix-Raviart (CR)单元**。我们将系统地揭示其理论基础与实践价值，填补从标准协调方法到高级非协调与间断方法的知识鸿沟。通过学习本文，读者将全面掌握CR单元的核心思想、数学原理及其在多个科学与工程领域的独特应用。

文章将分为三个主要部分展开：
- 在“**原理与机制**”一章中，我们将详细定义CR单元，阐明其基于边自由度的独特构造，并探讨其背后的数学框架，包括[破碎Sobolev空间](@entry_id:746989)、跳跃算子以及保证收敛性的关键——膜片检验（patch test）。
- 随后的“**应用与[交叉](@entry_id:147634)学科联系**”一章将展示CR单元的实践威力，重点探讨其如何有效解决[流体力学](@entry_id:136788)中的[Stokes方程](@entry_id:196346)稳定性问题、[固体力学](@entry_id:164042)中的[体积锁定](@entry_id:172606)现象，以及在波传播问题中展现出的独特计算优势。
- 最后，在“**动手实践**”部分，我们将通过一系列精心设计的计算练习，引导读者从理论走向实践，亲手构建[基函数](@entry_id:170178)、组装刚度矩阵，并验证方法的关键性质。

现在，让我们从CR单元的基本定义和数学原理开始，踏上探索非[协调有限元](@entry_id:170866)世界的旅程。

## 原理与机制

在[偏微分方程](@entry_id:141332)的[有限元分析](@entry_id:138109)中，选择合适的[函数空间](@entry_id:143478)是构建准确高效数值方法的基石。传统上，我们偏好使用**[协调有限元](@entry_id:170866) (conforming finite elements)**，其[函数空间](@entry_id:143478)是连续问题解空间（如 $H^1(\Omega)$）的[子空间](@entry_id:150286)。然而，放宽对函数全局连续性的严格要求，可以催生出一类同样强大且在特定问题中更具优势的**非[协调有限元](@entry_id:170866) (nonconforming finite elements)**。本章将深入探讨其中最著名和最基础的例子——Crouzeix-Raviart (CR) 非协调单元。

### Crouzeix-Raviart单元的定义与自由度

为了理解CR单元的核心思想，我们首先在二维[三角剖分](@entry_id:272253)上进行定义，并将其与标准的协调 $\mathbb{P}_1$ 单元进行对比。

考虑一个二维区域 $\Omega$ 上的形状规则的三角形剖分 $\mathcal{T}_h$。标准的**协调线性元 (conforming linear element)**，或称Lagrange $\mathbb{P}_1$ 单元，其函数空间由在整个区域 $\Omega$ 上连续的分片线性函数构成。一个函数若在每个单元 $T \in \mathcal{T}_h$ 上是线性的，并且在所有网格顶点处的值是唯一确定的，那么它在整个区域上就是连续的。因此，这类单元的**自由度 (degrees of freedom, DoFs)** 自然地选为函数在网格顶点处的值。全局连续性保证了该有限元空间是 $H^1(\Omega)$ 的一个[子空间](@entry_id:150286)，这是其“协调”名称的由来。

相比之下，**Crouzeix-Raviart (CR) 单元**虽然同样在每个三角形 $T$ 上采用线性多项式（即，其局部函数空间为 $\mathbb{P}_1(T)$），但它采用了更弱的连续性约束。CR单元的自由度并非定义在顶点上，而是定义在**每条边的中点 (edge midpoints)**。一个二维线性函数 $p(x,y) = ax+by+c$ 由三个非共线的点上的值唯一确定，而一个非退化三角形的三条边中点恰好满足此条件。

全局的CR有限元空间 $V_h^{\mathrm{CR}}$ 是通过要求共享公共内部边的相邻单元函数在该边的中点处取值相同来“粘合”的。对于一条内部边 $E$，其两侧的函数 $v_h^+$ 和 $v_h^-$ 在 $E$ 的中点 $m_E$ 处必须相等，即 $v_h^+(m_E) = v_h^-(m_E)$。对于带齐次[Dirichlet边界条件](@entry_id:142800)的边值问题，则要求所有边界边中点上的函数值为零  。

这种中点连续性并不足以保证函数在整条边上都连续。因此，CR空间中的函数在单元边界上通常是间断的，这意味着 $V_h^{\mathrm{CR}}$ **不是** $H^1(\Omega)$ 的[子空间](@entry_id:150286)，这正是其“非协调”的本质 。

一个重要且等价的定义方式是利用积分。对于一个在边 $E$ 上呈线性的函数 $p(s)$，其在中点 $m_E$ 的值等于它在这条边上的平均值，即 $p(m_E) = \frac{1}{|E|} \int_E p(s) \, \mathrm{d}s$。因此，中点连续性条件 $v_h^+(m_E) = v_h^-(m_E)$ 等价于两个迹的积分平均值相等：
$$
\frac{1}{|E|} \int_E v_h^+(s) \, \mathrm{d}s = \frac{1}{|E|} \int_E v_h^-(s) \, \mathrm{d}s
$$
这又等价于函数在边 $E$ 上的**跳跃 (jump)** 的积分为零。如果我们定义内部边 $E$ 上的跳跃为 $[v_h]_E = v_h^+ - v_h^-$，那么连续性条件可以优雅地写作：
$$
\int_E [v_h]_E \, \mathrm{d}s = 0
$$
综上，带有齐次[Dirichlet边界条件](@entry_id:142800)的二维CR空间可以被精确定义为  ：
$$
V_h^{\mathrm{CR}} = \left\{ v_h \in L^2(\Omega) \,\middle|\, \forall T \in \mathcal{T}_h, v_h|_T \in \mathbb{P}_1(T); \; \forall E \in \mathcal{E}_h^i, \int_E [v_h]_E \, \mathrm{d}s = 0; \; \forall E \in \mathcal{E}_h^b, \int_E v_h \, \mathrm{d}s = 0 \right\}
$$
其中 $\mathcal{E}_h^i$ 和 $\mathcal{E}_h^b$ 分别代表内部[边集](@entry_id:267160)和边界[边集](@entry_id:267160)。

### 非协调分析的数学框架

为了更严谨地分析像CR单元这样的[非协调方法](@entry_id:165221)，我们需要引入一些特定的数学工具。

首先是**[破碎Sobolev空间](@entry_id:746989) (broken Sobolev space)** 的概念。它由所有在剖分的每个单元 $K$ 上都属于标准Sobolev空间 $H^1(K)$ 的 $L^2(\Omega)$ 函数构成，记作 $H^1(\mathcal{T}_h)$：
$$
H^1(\mathcal{T}_h) := \{ v \in L^2(\Omega) : v|_K \in H^1(K) \text{ for all } K \in \mathcal{T}_h \}
$$
这个空间允许函数在单元边界上存在间断。CR空间 $V_h^{\mathrm{CR}}$ 正是 $H^1(\mathcal{T}_h)$ 的一个[子空间](@entry_id:150286)。

其次，我们需要精确定义跨单元边界的**迹 (trace)** 和**跳跃 (jump)**。对于 $v \in H^1(\mathcal{T}_h)$，其在每个单元 $K$ 上的限制 $v|_K$ 都在 $H^1(K)$ 中。根据[迹定理](@entry_id:203967)，我们可以定义 $v|_K$ 在 $K$ 的边界 $\partial K$ 上的迹。对于一条内部边 $e = \partial K^+ \cap \partial K^-$，我们可以得到两个迹：来自 $K^+$ 的 $v^+$ 和来自 $K^-$ 的 $v^-$。假设我们为每条边 $e$ 固定一个法向量 $\boldsymbol{n}_e$（例如，从 $K^+$ 指向 $K^-$），则函数 $v$ 在 $e$ 上的（标量）跳跃定义为：
$$
\llbracket v \rrbracket := v^+ - v^-
$$
利用这个记号，CR单元的连续性条件就是要求函数在所有内部边上的跳跃的积分为零 。

### 推广与结构性质

Crouzeix-Raviart单元的思想具有很好的普适性，可以自然地推广到三维空间。在三维区域 $\Omega$ 的四面体剖分 $\mathcal{T}_h$ 上，$\mathbb{P}_1$ CR单元同样由分片线性函数构成。一个四面体有4个面，一个线性函数 $p(x,y,z)$ 由4个自由度确定。因此，三维CR单元的自由度被定义为函数在**四个三角面 (faces)** 上的积分平均值。

全局空间是通过要求函数在内部公共面 $F$ 上的积分平均值连续来构建的。这同样等价于函数在面上的跳跃积分为零，即 $\int_F \llbracket v_h \rrbracket \, ds = 0$。同样地，对于线性函数而言，面上的积分平均值等于其在面的**[重心](@entry_id:273519) (barycenter)** 处的函数值。因此，三维CR单元的连续性条件也可以等价地描述为函数在所有内部面的重心处连续 。

回到二维情形，我们来考察CR空间 $V_h^{\mathrm{CR}}$ 的结构性质。由于自由度与网格的边一一对应，并且边界边上的自由度在[齐次边界条件](@entry_id:750371)下被置零，因此空间的**维数**等于内部边的数量：
$$
\dim V_h^{\mathrm{CR}} = |\mathcal{E}_h^{\mathrm{int}}|
$$
我们可以为每条内部边 $e \in \mathcal{E}_h^{\mathrm{int}}$ 构建一个**典则[基函数](@entry_id:170178) (canonical basis function)** $\varphi_e \in V_h^{\mathrm{CR}}$。该[基函数](@entry_id:170178)定义为在其对应的边 $e$ 的中点处取值为1，而在所有其他边的中点处取值为0。

考察[基函数](@entry_id:170178) $\varphi_e$ 的**支集 (support)**，即函数非零的区域。考虑任意一个不与边 $e$ 相邻的三角形 $T'$。$\varphi_e$ 在 $T'$ 的三条边的中点处的值均为0。由于一个线性函数在三个非[共线点](@entry_id:174222)上为零，则它必定在该三角形上恒为零。因此，$\varphi_e$ 仅在与边 $e$ 直接相邻的两个三角形上非零。这意味着[基函数](@entry_id:170178) $\varphi_e$ 的支集是共享边 $e$ 的那两个三角形的并集 。这种高度局部的支集特性在构建稀疏的[全局刚度矩阵](@entry_id:138630)时至关重要。

### [局部基](@entry_id:151573)函数与插值

为了更深入地理解CR单元，我们可以在一个参考三角形上显式地构造出其[局部基](@entry_id:151573)函数。利用**[重心坐标](@entry_id:155488) (barycentric coordinates)** $\lambda_1, \lambda_2, \lambda_3$ 是一个非常有效的工具。在一个三角形 $T$ 上，其顶点为 $\boldsymbol{x}_1, \boldsymbol{x}_2, \boldsymbol{x}_3$，[重心坐标](@entry_id:155488) $\lambda_i$ 是一个线性函数，满足 $\lambda_i(\boldsymbol{x}_j) = \delta_{ij}$ 并且 $\sum_i \lambda_i = 1$。

设 $e_i$ 是与顶点 $\boldsymbol{x}_i$ 相对的边。我们希望构造一组[基函数](@entry_id:170178) $\{\varphi_1, \varphi_2, \varphi_3\} \subset \mathbb{P}_1(T)$，它们关于边平均值自由度是对偶的，即 $\frac{1}{|e_j|} \int_{e_j} \varphi_i \, ds = \delta_{ij}$。通过计算[重心坐标](@entry_id:155488)在各条边上的积分，可以推导出这组[基函数](@entry_id:170178)具有非常简洁的形式 ：
$$
\varphi_i = 1 - 2\lambda_i, \quad i=1,2,3
$$
基于这些[基函数](@entry_id:170178)，我们可以定义一个**Crouzeix-Raviart插值算子** $\mathcal{I}_{\mathrm{CR}}$。对于一个足够光滑的函数 $u$，其插值 $\mathcal{I}_{\mathrm{CR}}u \in \mathbb{P}_1(T)$ 被定义为与 $u$ 具有相同边平均值的唯一线性函数。

一个至关重要的性质是，该插值算子能够**精确再现**线性多项式。也就是说，如果 $p$ 本身就是一个线性函数，那么 $\mathcal{I}_{\mathrm{CR}}p = p$。这个性质可以通过证明 $p - \mathcal{I}_{\mathrm{CR}}p$ 在三条边上的平均值均为零，进而推断出这个线性函数在三个顶点处的值也必为零，从而证明它恒等于零 。这个性质，在更广泛的意义上被称为**通过线性修补检验 (passing the linear patch test)**，是[非协调元](@entry_id:752549)能够收敛的根本保证。它确保了当网格尺寸趋于零时，即使单元之间不完全连续，方法也能够在常数场和线性场的情况下给出精确解，这是任何有效的有限元方法必须满足的最低要求。

### [Galerkin正交性](@entry_id:173536)与[相容性误差](@entry_id:747725)

最后，我们探讨非协调性对有限元方法核心理论——**[Galerkin正交性](@entry_id:173536) (Galerkin orthogonality)**——的影响。考虑[泊松方程](@entry_id:143763)的[弱形式](@entry_id:142897)：寻找 $u \in H^1_0(\Omega)$ 使得
$$
a(u,v) := \int_{\Omega} \nabla u \cdot \nabla v \, dx = \int_{\Omega} f v \, dx =: \ell(v) \quad \forall v \in H^1_0(\Omega)
$$
CR-[Galerkin方法](@entry_id:260906)则是在破碎空间上寻找 $u_h \in V_h^{\mathrm{CR}}$ 使得
$$
a_h(u_h, v_h) := \sum_{K \in \mathcal{T}_h} \int_{K} \nabla u_h \cdot \nabla v_h \, dx = \ell(v_h) \quad \forall v_h \in V_h^{\mathrm{CR}}
$$
对于协调方法，由于 $V_h \subset H^1_0(\Omega)$，我们可以取连续弱形式中的 $v = v_h \in V_h$，得到 $a(u,v_h) = \ell(v_h)$。将其与离散方程 $a(u_h,v_h) = \ell(v_h)$ 相减，便得到误差 $e=u-u_h$ 与离散空间 $V_h$ 中的任意函数 $v_h$ 在[能量内积](@entry_id:167297) $a(\cdot,\cdot)$ 下正交，即 $a(e,v_h)=0$。

然而，对于CR方法，这个论证过程在第一步就失效了。因为 $V_h^{\mathrm{CR}} \not\subset H^1_0(\Omega)$，我们不能简单地将离散[检验函数](@entry_id:166589) $v_h$ 代入到为 $H^1_0(\Omega)$ 函数定义的连续[弱形式](@entry_id:142897)中 。

为了得到一个有效的误差方程，我们必须从离散误差 $a_h(u-u_h, v_h)$ 出发，并使用[分部积分](@entry_id:136350)。我们有 $a_h(u-u_h, v_h) = a_h(u, v_h) - a_h(u_h, v_h) = a_h(u, v_h) - \ell(v_h)$。对 $a_h(u, v_h)$ 在每个单元上进行分部积分，并利用 $-\Delta u = f$，我们得到：
$$
a_h(u, v_h) = \sum_{K \in \mathcal{T}_h} \int_K \nabla u \cdot \nabla v_h \, dx = \int_{\Omega} f v_h \, dx + \sum_{K \in \mathcal{T}_h} \int_{\partial K} (\nabla u \cdot \boldsymbol{n}_K) v_h \, ds
$$
将边界积分项整理成关于网格边的求和，可以证明一个修正的“正交性”关系：
$$
a_h(u-u_h, v_h) = \sum_{E \in \mathcal{E}_h} \int_E (\nabla u \cdot \boldsymbol{n}_E) \llbracket v_h \rrbracket \, ds \quad \forall v_h \in V_h^{\mathrm{CR}}
$$
这个等式是Strang第二引理的一个实例。它表明，误差与[离散空间](@entry_id:155685)的“正交性”被破坏了，其偏差由右端的项——**[相容性误差](@entry_id:747725) (consistency error)**——来量化。这个误差源于我们用一个不属于原空间的函数去检验原方程。CR方法的[收敛性分析](@entry_id:151547)的关键就在于证明，当网格细化时，这个[相容性误差](@entry_id:747725)项的收敛速度足够快，以至于不会破坏方法的整体[收敛阶](@entry_id:146394)。而这恰恰依赖于CR空间的核心定义，即 $\int_E \llbracket v_h \rrbracket \, ds = 0$，它使得我们可以通过[Poincaré不等式](@entry_id:142086)等工具来控制这些边界积分项 。

总之，Crouzeix-Raviart单元通过牺牲全局连续性换取了结构上的简洁性，并引入了非[协调有限元](@entry_id:170866)分析的一整套核心概念：[破碎Sobolev空间](@entry_id:746989)、跳跃算子、修补检验以及[相容性误差](@entry_id:747725)。它是理解更高级的非协调和间断Galerkin方法的重要起点。