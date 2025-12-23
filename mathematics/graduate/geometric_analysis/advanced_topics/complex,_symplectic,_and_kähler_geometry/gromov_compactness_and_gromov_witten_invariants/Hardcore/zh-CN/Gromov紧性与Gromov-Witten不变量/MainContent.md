## 引言
[Gromov-Witten不变量](@entry_id:160953)是现代[辛几何](@entry_id:160783)与代数几何中的核心工具，它为“计数”[辛流形](@entry_id:161608)中[伪全纯曲线](@entry_id:201654)这一古老问题提供了坚实的数学框架。经典计数几何虽然直观，但在处理退化和奇异情况时常常面临严格性的挑战。[Gromov-Witten理论](@entry_id:190829)通过引入强大的几何分析技术，不仅解决了这些难题，还揭示了深刻的[代数结构](@entry_id:137052)和跨学科联系。本文旨在系统介绍这一理论的核心思想与应用。

在接下来的内容中，读者将深入学习[Gromov-Witten理论](@entry_id:190829)的三个层面。首先，在“原理与机制”一章，我们将剖析该理论的分析基础，从[J-全纯曲线](@entry_id:184507)出发，重点阐述作为理论基石的[Gromov紧性定理](@entry_id:201615)，并详细介绍[稳定映射](@entry_id:634781)[模空间](@entry_id:159780)和[虚拟基本类](@entry_id:182358)的构造，这是定义[不变量](@entry_id:148850)的关键。其次，在“应用与交叉学科联系”一章，我们将展示这些抽象原理如何转化为强大的计算工具，用于解决经典计数几何问题，催生量子(上)同调这一全新[代数结构](@entry_id:137052)，并建立与Floer理论及[数学物理](@entry_id:265403)的联系。最后，在“动手实践”部分，通过具体问题加深对理论核心概念的理解。

## 原理与机制

在“引言”章节中，我们初步了解了[Gromov-Witten不变量](@entry_id:160953)作为枚举几何中计数问题的现代表述。本章将深入探讨这些[不变量](@entry_id:148850)得以严格定义的数学原理与核心机制。我们将从[J-全纯曲线](@entry_id:184507)的分析基础出发，建立[Gromov紧性定理](@entry_id:201615)这一基石，进而研究[稳定映射](@entry_id:634781)模空间的精细结构，并最终引出[虚拟基本类](@entry_id:182358)的概念，完成对[Gromov-Witten不变量](@entry_id:160953)的构造。

### [J-全纯曲线](@entry_id:184507)的分析基础

[Gromov-Witten理论](@entry_id:190829)的核心研究对象是**[J-全纯曲线](@entry_id:184507)**（J-holomorphic curves），即从一个[黎曼曲面](@entry_id:178613)到几乎复流形的映射。理解这些曲线的性质，是构建整个理论的第一步。

#### 驯顺与相容的几乎[复结构](@entry_id:269128)

设 $(M, \omega)$ 是一个 $2n$ 维的[辛流形](@entry_id:161608)，其中 $\omega$ 是一个闭的、非退化的2-形式。一个**几乎[复结构](@entry_id:269128)**（almost complex structure）是切丛上的一个自同态 $J: TM \to TM$，满足 $J^2 = -\mathrm{Id}$。它在每一点的切空间上定义了一个复结构。

几乎[复结构](@entry_id:269128) $J$ 与[辛形式](@entry_id:165896) $\omega$ 之间的关系至关重要，主要分为两种：

1.  **$\omega$-驯顺性**（$\omega$-tameness）：如果对于任意非零[切向量](@entry_id:265494) $v \in TM$，都有 $\omega(v, Jv) > 0$，则称 $J$ 是**$\omega$-驯顺的**。这个条件意味着由 $g_J(u, v) = \frac{1}{2}(\omega(u, Jv) - \omega(v, Ju))$ 定义的[对称双线性形式](@entry_id:148281)是一个[黎曼度量](@entry_id:754359)，且 $J$ 是一个[正交变换](@entry_id:155650)。换言之，$(M, J, g_J)$ 成为一个殆Hermite[流形](@entry_id:153038)。

2.  **$\omega$-相容性**（$\omega$-compatibility）：如果 $J$ 不仅是 $\omega$-驯顺的，并且还保持 $\omega$ 不变，即对任意 $u, v \in TM$ 都有 $\omega(Ju, Jv) = \omega(u, v)$，则称 $J$ 是**$\omega$-相容的**。在这种情况下，由 $g_J(u, v) = \omega(u, Jv)$ 定义的[双线性形式](@entry_id:746794) $g_J$ 不仅正定，而且是对称的，从而构成一个[黎曼度量](@entry_id:754359)。

显然，任何 $\omega$-相容的 $J$ 都是 $\omega$-驯顺的，但反之不然。驯顺性是一个比相容性更弱的条件。例如，在标准辛空间 $(\mathbb{R}^4, \omega_0 = dx_1 \wedge dy_1 + dx_2 \wedge dy_2)$ 中，标准[复结构](@entry_id:269128) $J_0$（定义为 $J_0(\partial_{x_i}) = \partial_{y_i}, J_0(\partial_{y_i}) = -\partial_{x_i}$）是 $\omega_0$-相容的。但如果我们考虑一个新的辛形式 $\omega' = dx_1 \wedge dy_1 + 2 dx_2 \wedge dy_2$，那么 $J_0$ 仍然是 $\omega'$-相容的。然而，对于形式 $\omega_\varepsilon = dx_1 \wedge dy_1 + dx_2 \wedge dy_2 + \varepsilon(dx_1 \wedge dy_2 + dy_1 \wedge dx_2)$（其中 $\varepsilon \in \mathbb{R} \setminus \{0, \pm 1\}$），可以验证 $J_0$ 是 $\omega_\varepsilon$-驯顺的，但不再是 $\omega_\varepsilon$-相容的，因为 $(J_0)^*\omega_\varepsilon \neq \omega_\varepsilon$。

[Gromov-Witten理论](@entry_id:190829)的一个深刻之处在于，其核心的紧性定理（见下文）仅仅要求 $J$ 是 $\omega$-驯顺的。这个条件的灵活性至关重要，因为它保证了由理论产生的[不变量](@entry_id:148850)确实是[辛流形](@entry_id:161608) $(M, \omega)$ 的[不变量](@entry_id:148850)，而不依赖于某个特定的相容的 $J$ 的选择。事实上，给定[辛流形](@entry_id:161608) $(M, \omega)$，其上所有 $\omega$-驯顺的几乎[复结构](@entry_id:269128)组成的空间是可缩的。

#### [J-全纯曲线](@entry_id:184507)方程与能量

给定一个闭[黎曼曲面](@entry_id:178613) $(\Sigma, j)$ 和一个殆[复流形](@entry_id:159076) $(M, J)$，一个[光滑映射](@entry_id:203730) $u: \Sigma \to M$ 被称为 **(J,j)-全纯**或简称**J-全纯**，如果它的[微分](@entry_id:158718) $du: T\Sigma \to TM$ 与复结构相容，即满足**Cauchy-Riemann方程**:
$$ du \circ j = J \circ du $$
这等价于说 $u$ 的**反全纯[微分](@entry_id:158718)** $\bar{\partial}_J u := \frac{1}{2}(du + J \circ du \circ j)$ 为零。

对于一个驯顺的几乎复结构 $J$，我们可以定义一个黎曼度量 $g_J(v, w) = \omega(v, Jw)$。利用这个度量，我们可以定义映射 $u$ 的**能量**（energy）：
$$ E(u) = \frac{1}{2} \int_\Sigma |du|^2 d\mathrm{vol}_\Sigma $$
其中 $|du|^2$ 是关于 $(\Sigma, j)$ 和 $(M, J, g_J)$ 的度量计算的[微分](@entry_id:158718)能量密度。一个关键的计算表明，如果 $u$ 是J-全纯的，那么它的能量恰好等于其像对辛[形式的积分](@entry_id:158607)，即**辛面积**（symplectic area）：
$$ E(u) = \int_\Sigma u^*\omega $$
这个等式将一个分析量（能量）与一个几何/拓扑量（辛面积）联系起来。

#### 辛形式的闭性条件

至此，我们可能会问，为什么辛形式 $\omega$ 必须是闭的，即 $d\omega = 0$？这个条件是[Gromov-Witten理论](@entry_id:190829)的基石。原因在于，只有当 $d\omega=0$ 时，辛面积 $\int_\Sigma u^*\omega$ 才是一个**[同伦不变量](@entry_id:151920)**，它仅依赖于映射 $u$ 所代表的同调类 $A = u_*[\Sigma] \in H_2(M; \mathbb{Z})$。

具体来说，如果 $u_0, u_1: \Sigma \to M$ 是两个同伦的映射，即存在一个同伦 $F: \Sigma \times [0,1] \to M$ 连接它们，那么根据[Stokes定理](@entry_id:146491)：
$$ \int_\Sigma u_1^*\omega - \int_\Sigma u_0^*\omega = \int_{\Sigma \times [0,1]} F^*(d\omega) $$
如果 $d\omega = 0$，则右侧为零，这意味着辛面积 $\int_\Sigma u^*\omega = \langle [\omega], A \rangle$ 是一个拓扑量，其中 $[\omega] \in H^2(M; \mathbb{R})$ 是 $\omega$ 的De Rham[上同调类](@entry_id:263961)。

这个性质至关重要。它为所有代表同一同调类 $A$ 的[J-全纯曲线](@entry_id:184507)提供了一个统一的**先验能量界**（a priori energy bound）。正如我们将在下一节看到的，这个能量界是证明[模空间](@entry_id:159780)紧性的关键。如果 $d\omega \neq 0$，能量将不再是拓扑量，无法获得统一的能量界，紧性论证将失败，[Gromov-Witten不变量](@entry_id:160953)也无从谈起。

### 模空间的紧性：Gromov定理

拥有了[J-全纯曲线](@entry_id:184507)的定义和先验能量界，我们现在可以研究由这些曲线构成的**[模空间](@entry_id:159780)**（moduli space）的性质。一个自然的愿望是，在给定拓扑不变量（如同调类）下，[J-全纯曲线](@entry_id:184507)的集合应该是一个“行为良好”的空间，特别是[紧空间](@entry_id:155073)。

#### 气泡化现象

然而，一个由光滑[J-全纯曲线](@entry_id:184507)组成的序列，即使能量一致有界，其极限也未必是一条光滑的[J-全纯曲线](@entry_id:184507)。一个典型的[退化现象](@entry_id:183258)是**气泡化**（bubbling）。

考虑从[黎曼球面](@entry_id:148483) $\mathbb{CP}^1$ 到自身的度为 $d \ge 2$ 的[全纯映射](@entry_id:264170)序列。我们可以构造一个序列 $u_\lambda: \mathbb{CP}^1 \to \mathbb{CP}^1$，使得当参数 $\lambda \to 0$ 时，映射序列在一个点（比如“北极”）附近发生剧烈变化。在极限中，原始映射收敛到一个度数较低（例如 $d-1$）的映射，而“丢失”的能量和度数则集中在一个点上，形成一个新的度为1的球面映射，像一个从[主曲线](@entry_id:161549)上“吹”出的气泡。通过适当的坐标缩放（rescaling），我们可以清晰地看到这个气泡映射。

这个例子揭示了[能量守恒](@entry_id:140514)和量子化的本质。在极限过程中，总能量（等于总度数）是守恒的。如果一个序列 $u_k$ 的能量为 $E$，其极限由一个基本部分 $u_\text{base}$ 和若干气泡 $u_{\text{bubble}, i}$ 组成，那么总能量等于各部分能量之和：$E = E(u_\text{base}) + \sum_i E(u_{\text{bubble}, i})$。每个分量的能量（辛面积）都对应于一个非负的拓扑量。例如，在 $\mathbb{CP}^1$ 的例子中，气泡的能量恰好为1，对应其度数为1。

#### [Gromov紧性定理](@entry_id:201615)与[稳定映射](@entry_id:634781)

Gromov的革命性工作在于，他证明了气泡化是唯一的退化方式。通过允许定义域[黎曼曲面](@entry_id:178613)自身发生退化（形成**节点**，即两个点粘合在一起），并允许在节点上附着气泡球面，[J-全纯曲线](@entry_id:184507)的[模空间](@entry_id:159780)可以被[紧化](@entry_id:150518)。

**[Gromov紧性定理](@entry_id:201615)**：设 $(M, \omega)$ 是一个闭[辛流形](@entry_id:161608)， $J$ 是一个 $\omega$-驯顺的几乎[复结构](@entry_id:269128)。给定亏格 $g$，标记点数 $k$ 和同调类 $A \in H_2(M; \mathbb{Z})$，任何一列亏格为 $g$、带 $k$ 个标记点的[J-全纯曲线](@entry_id:184507)，其同调类为 $A$（因此能量有界），都存在一个子列，在Gromov拓扑下收敛到一个**[稳定映射](@entry_id:634781)**（stable map）。

这个定理是整个[Gromov-Witten理论](@entry_id:190829)的基石。它保证了我们研究的[模空间](@entry_id:159780) $\overline{\mathcal{M}}_{g,k}(A;J)$ 是一个紧空间，从而可以在其上进行积分来定义[不变量](@entry_id:148850)。

### [稳定映射](@entry_id:634781)[模空间](@entry_id:159780)的结构

[Gromov紧性定理](@entry_id:201615)告诉我们，研究[J-全纯曲线](@entry_id:184507)的正确对象是[稳定映射](@entry_id:634781)。现在我们来精确定义这些对象以及它们构成的[模空间](@entry_id:159780)。

#### [稳定映射](@entry_id:634781)的定义

一个亏格为 $g$、带 $k$ 个标记点的**[稳定映射](@entry_id:634781)**是一个等价类 $[(C, \mathbf{z}, u)]$，其中：
1.  **定义域**：$C$ 是一个连通的、至多有节点的[黎曼曲面](@entry_id:178613)，其算术亏格为 $g$。
2.  **标记点**：$\mathbf{z} = (z_1, \dots, z_k)$ 是 $C$ 的光滑点上的 $k$ 个有序的不同点。
3.  **映射**：$u: C \to M$ 是一个[连续映射](@entry_id:153855)，在 $C$ 的每个不可约分支上都是J-全纯的，并且其推出的同调类为 $A$，即 $u_*[C] = A$。

两个这样的数据 $(C, \mathbf{z}, u)$ 和 $(C', \mathbf{z}', u')$ 被认为是等价的，如果存在一个[双全纯映射](@entry_id:178321) $\psi: C \to C'$，它保持标记点（即 $\psi(z_i) = z'_i$），并且与映射 $u, u'$ 相容（即 $u = u' \circ \psi$）。

**[模空间](@entry_id:159780)** $\overline{\mathcal{M}}_{g,k}(A;J)$ 就是由所有这些[稳定映射](@entry_id:634781)的[等价类](@entry_id:156032)构成的空间。

#### 稳定条件

定义中“稳定”一词具有深刻的含义。为了使[模空间](@entry_id:159780)成为一个行为良好的空间（具体来说，是一个**[轨道](@entry_id:137151)[流形](@entry_id:153038)**，orbifold），我们必须要求每个[稳定映射](@entry_id:634781)的**[自同构群](@entry_id:139672)**（automorphism group）是有限的。[自同构](@entry_id:155390)是指从一个数据 $(C, \mathbf{z}, u)$ 到其自身的等价映射。

无限[自同构群](@entry_id:139672)的出现，恰恰发生在映射 $u$ “遗忘”了定义域的某些几何结构时。这具体表现为：当 $u$ 将 $C$ 的某个不可约分支 $C_i$ 映为 $M$ 中的一个单点时，这个分支被称为**收缩分支**或“鬼”分支。对于这样的分支，任何保持其上特殊点（标记点或节点）的[自同构](@entry_id:155390)都可以平凡地扩展为整个[稳定映射](@entry_id:634781)的[自同构](@entry_id:155390)。

一个[黎曼曲面](@entry_id:178613)的[自同构群](@entry_id:139672)是无限的（连续的）情况非常有限：
-   亏格为0的球面，带有0、1或2个特殊点。
-   亏格为1的环面，带有0个特殊点。

因此，**稳定性条件**要求：对于任何被映射 $u$ 收缩到一点的不可约分支 $C_i$，该分支（作为带有自身特殊点的曲线）必须是**Deligne-Mumford稳定**的。具体来说：
-   任何亏格为0的收缩分支必须至少有3个特殊点（标记点或节点）。
-   任何亏格为1的收缩分支必须至少有1个特殊点。

对于非收缩的分支，由于映射 $u$ 本身非平凡，它会破坏定义域的连续对称性，自动保证了[自同构群](@entry_id:139672)的有限性。

#### 基本态射：[求值映射](@entry_id:149774)与遗忘映射

在[紧化](@entry_id:150518)的模空间 $\overline{\mathcal{M}}_{g,k}(A;J)$ 上，定义了两个极其重要的态射：

1.  **[求值映射](@entry_id:149774)**（evaluation map） $\mathrm{ev}_i: \overline{\mathcal{M}}_{g,k}(A;J) \to M$。它将一个[稳定映射](@entry_id:634781) $[(C, \mathbf{z}, u)]$ 映到第 $i$ 个标记点在目标[流形](@entry_id:153038)中的像：
    $$ \mathrm{ev}_i([(C, \mathbf{z}, u)]) = u(z_i) $$
    这个映射的几何意义是“在第 $i$ 个标记点处的位置”。由于[稳定映射](@entry_id:634781) $u$ 是连续的，且标记点 $z_i$ 位于光滑点上，这个映射是良定义的。

2.  **遗忘映射**（forgetful map） $\mathrm{ft}: \overline{\mathcal{M}}_{g,k}(A;J) \to \overline{\mathcal{M}}_{g,k}$。它“遗忘”了映射 $u$，只保留定义域的代数几何结构。其像空间 $\overline{\mathcal{M}}_{g,k}$ 是**Deligne-Mumford[模空间](@entry_id:159780)**，即亏格为 $g$、带 $k$ 个标记点的稳定[代数曲线](@entry_id:170938)的模空间。这个映射需要一个“稳定化”步骤：如果[稳定映射](@entry_id:634781)的定义域 $(C, \mathbf{z})$ 本身不是Deligne-Mumford稳定的（例如，包含一个只有两个特殊点的球面分支，但映射 $u$ 在其上非恒定），遗忘映射会先将这些不稳定的分支收缩掉。

[Gromov紧性定理](@entry_id:201615)的一个重要推论是，在Gromov拓扑下，这两个映射都是**连续的**。[求值映射](@entry_id:149774)的连续性意味着，当一列[稳定映射](@entry_id:634781)收敛时，它们在标记点处的值也会收敛。遗忘映射的连续性则连接了[J-全纯曲线](@entry_id:184507)的分析世界和[代数曲线](@entry_id:170938)的纯代数世界。这两个映射的连续性是利用模空间来定义[不变量](@entry_id:148850)的先决条件。

### 形变理论与[虚拟基本类](@entry_id:182358)

我们已经知道模空间 $\overline{\mathcal{M}}_{g,k}(A;J)$ 是一个[紧空间](@entry_id:155073)。但它的局部结构是怎样的？它是一个[光滑流形](@entry_id:160799)吗？

#### 线性化Cauchy-Riemann算子

为了研究模空间在一点 $[u]$ 附近的局部结构，我们考察[J-全纯曲线](@entry_id:184507)方程 $\bar{\partial}_J(u)=0$ 的**线性化**。考虑映射 $u$ 的一个微小形变，由一个沿着 $u$ 的向量场 $\xi \in \Gamma(u^*TM)$ 描述。$\bar{\partial}_J$ 在 $u$ 处的线性化 $D_u\bar{\partial}_J$ 作用在 $\xi$ 上，给出：
$$ D_u\bar{\partial}_J(\xi)(X) = \frac{1}{2} \left( \nabla_X \xi + J(\nabla_{jX} \xi) + (\nabla_{\xi} J)(J(du(X))) \right) $$
其中 $\nabla$ 是 $TM$ 上的[Levi-Civita联络](@entry_id:161107)， $X \in T\Sigma$。这个算子是一个作用在 $u^*TM$ [丛的截面](@entry_id:195261)上的**一阶线性椭圆偏[微分算子](@entry_id:140145)**。

#### [Fredholm理论](@entry_id:261771)与期望维数

根据[椭圆算子](@entry_id:181616)理论，$D_u\bar{\partial}_J$ 是一个**[Fredholm算子](@entry_id:268966)**。这意味着它的核（kernel）和余核（cokernel）都是有限维的。这两个空间具有重要的几何意义：
-   $\ker(D_u\bar{\partial}_J)$ 对应于 $u$ 的无穷小形变空间。
-   $\mathrm{coker}(D_u\bar{\partial}_J)$ 对应于形变的**阻碍空间**（obstruction space）。

如果对于一个[J-全纯曲线](@entry_id:184507) $u$，其阻碍空间为零（$\mathrm{coker}(D_u\bar{\partial}_J) = 0$），则称 $u$ 是**正则的**（regular）。在这种情况下，根据[隐函数定理](@entry_id:147247)的无穷维版本，模空间在 $[u]$ 附近是一个维数为 $\dim_{\mathbb{R}}(\ker(D_u\bar{\partial}_J))$ 的[光滑流形](@entry_id:160799)。

[Fredholm算子](@entry_id:268966)的一个重要[不变量](@entry_id:148850)是它的**指标**（index），定义为 $\mathrm{index}(D_u) = \dim(\ker D_u) - \dim(\mathrm{coker} D_u)$。利用[Atiyah-Singer指标定理](@entry_id:144128)，可以计算出该算子的复指标，进而得到[模空间](@entry_id:159780)的**期望维数**或**虚拟维数**（virtual dimension）。其（实的）虚拟维数为：
$$ \mathrm{vdim}_{\mathbb{R}} \overline{\mathcal{M}}_{g,k}(A;J) = (n-3)(2-2g) + 2 \langle c_1(TM), A \rangle + 2k $$
其中 $n$ 是 $M$ 的复维数，$c_1(TM)$ 是 $M$ 切丛的[第一陈类](@entry_id:201400)。例如，对于目标空间 $X=\mathbb{CP}^2$ ($n=2$)，考虑亏格 $g=0$、同调类为 $A=2[\text{line}]$（二次曲线）、标记点数 $k=5$ 的情况，我们可以计算出期望实维数为 $20$。

#### [横截性](@entry_id:158669)问题与[虚拟基本类](@entry_id:182358)

问题在于，并非所有[J-全纯曲线](@entry_id:184507)都是正则的。当存在阻碍时（$\mathrm{coker}(D_u\bar{\partial}_J) \neq 0$），[模空间](@entry_id:159780)的实际维数可能小于期望维数，并且可能不是[光滑流形](@entry_id:160799)，而是具有复杂的奇异性。这种情况在存在多重覆盖曲线时尤为常见。

这意味着我们不能简单地将模空间当作一个普通[流形](@entry_id:153038)来处理。为了解决这个**[横截性](@entry_id:158669)**（transversality）问题，现代几何学家发明了一种强大的工具：**[虚拟基本类](@entry_id:182358)**（virtual fundamental class），记作 $[\overline{\mathcal{M}}_{g,k}(A;J)]^{\mathrm{vir}}$。

这个[虚拟基本类](@entry_id:182358)是一个定义在模空间 $\overline{\mathcal{M}}_{g,k}(A;J)$ 上的有理系数同调类，其维数恰好等于我们之前计算的期望维数。直观上，它通过一种“扰动”的方式来修正模空间，使其“表现得”像一个维数正确的[流形](@entry_id:153038)，即使它本身不是。这个构造是[Gromov-Witten理论](@entry_id:190829)中最深刻和技术性的部分之一。

### [Gromov-Witten不变量](@entry_id:160953)的定义

有了紧的[模空间](@entry_id:159780)和其上的[虚拟基本类](@entry_id:182358)，我们终于可以定义[Gromov-Witten不变量](@entry_id:160953)了。

#### 积分定义

设 $\alpha_1, \dots, \alpha_k \in H^*(M; \mathbb{Q})$ 是目标[流形](@entry_id:153038) $M$ 上的[上同调类](@entry_id:263961)。我们可以利用[求值映射](@entry_id:149774) $\mathrm{ev}_i$ 将这些类[拉回](@entry_id:160816)到[模空间](@entry_id:159780)上，得到 $\mathrm{ev}_i^*(\alpha_i) \in H^*(\overline{\mathcal{M}}_{g,k}(A;J); \mathbb{Q})$。然后，我们将这些[拉回](@entry_id:160816)的类用上同调的上积（cup product）$\cup$ 乘起来。

亏格为 $g$、带 $k$ 个点的**[Gromov-Witten不变量](@entry_id:160953)**定义为这个上同调类在[虚拟基本类](@entry_id:182358)上的积分：
$$ \langle \alpha_1, \dots, \alpha_k \rangle_{g,A} = \int_{[\overline{\mathcal{M}}_{g,k}(A;J)]^{\mathrm{vir}}} \mathrm{ev}_1^*(\alpha_1) \cup \dots \cup \mathrm{ev}_k^*(\alpha_k) $$
这个积分（或者说，[上同调类](@entry_id:263961)在同调类上的配对）是一个有理数。它只有在维数匹配时才可能非零，即上同调类的总次数等于[虚拟基本类](@entry_id:182358)的维数：
$$ \sum_{i=1}^k \deg(\alpha_i) = \mathrm{vdim}_{\mathbb{R}} \overline{\mathcal{M}}_{g,k}(A;J) $$
这个[不变量](@entry_id:148850)在几何上“计数”了亏格为 $g$、同调类为 $A$ 的[J-全纯曲线](@entry_id:184507)，且这些曲线穿过了由上同调类 $\alpha_i$ 的[Poincaré对偶](@entry_id:161676)所代表的闭链。

这个定义也可以等价地表述为：将[虚拟基本类](@entry_id:182358)通过乘积[求值映射](@entry_id:149774) $\mathrm{ev} = (\mathrm{ev}_1, \dots, \mathrm{ev}_k)$ 推前到 $M^k$ 中，然后与[上同调类](@entry_id:263961) $\alpha_1 \boxtimes \dots \boxtimes \alpha_k$ 进行配对。

#### 定向问题

为了使这个“计数”得到一个明确的符号，而不仅仅是[绝对值](@entry_id:147688)，[虚拟基本类](@entry_id:182358)需要被**定向**（oriented）。定向问题在[Gromov-Witten理论](@entry_id:190829)中是一个核心的技术要点。

定向的工具来自于[Fredholm算子](@entry_id:268966)的**[行列式线丛](@entry_id:201038)**（determinant line bundle）。对于线性化算子族 $\{D_u\}$，它们在模空间上构成一个[行列式线丛](@entry_id:201038) $\det(D) = \Lambda^{\mathrm{top}}\ker(D) \otimes (\Lambda^{\mathrm{top}}\mathrm{coker}(D))^*$。这个线丛的一个定向就给出了[模空间](@entry_id:159780)的一个定向。

幸运的是，对于从闭[黎曼曲面](@entry_id:178613)出发的[J-全纯曲线](@entry_id:184507)，线性化算子 $D_u\bar{\partial}_J$ 是**复线性**的。它的核与余核都是[复向量空间](@entry_id:264355)，因此[行列式线丛](@entry_id:201038)是一个复线丛。任何一维[复向量空间](@entry_id:264355)都带有一个典范的实定向（例如，由基 $\{1, i\}$ 给出）。这为我们提供了一个**典范定向**。更重要的是，这个定向系统在节点退化和粘合操作下是**相容的**（coherent）。这种相容性确保了我们可以为整个[紧化](@entry_id:150518)模空间的所有层次（strata）赋予一致的符号，从而得到一个良定义的、带符号的[Gromov-Witten不变量](@entry_id:160953)。

### 正则化理论前沿

[虚拟基本类](@entry_id:182358)的构造是[Gromov-Witten理论](@entry_id:190829)的分析核心。这个构造本身充满了技术上的挑战，催生了多种深刻的数学思想。

#### 分析上的挑战

传统的Banach[流形](@entry_id:153038)框架在处理[模空间](@entry_id:159780)时会遇到一个棘手的问题：由定义域的双全纯[自同构群](@entry_id:139672)构成的重[参数化](@entry_id:272587)群，其在Sobolev映射空间上的作用不是光滑的。这是因为复合函数求导的链式法则会“损失”一个导数，导致映射的无穷小形变理论无法在经典的[流形](@entry_id:153038)框架内完美建立。

#### 不同的[正则化方法](@entry_id:150559)及其一致性

为了克服这些分析上的困难，并严格地构造[虚拟基本类](@entry_id:182358)，几何学家们发展了多种方法：

1.  **Kuranishi结构**：由Fukaya和Ono等人发展的分析方法，它用有限维的“Kuranishi图表”来局部地描述模空间，每个图表由一个[有限维向量空间](@entry_id:265491)中的一个[截面](@entry_id:154995)的[零点集](@entry_id:150020)给出。通过在这些图表上进行相容的扰动，可以构造出[虚拟基本类](@entry_id:182358)。

2.  **解析虚拟循环**：由Li和Tian发展的另一种分析方法，它将 $\bar{\partial}_J$ 算子视为一个无穷维Banach丛中的一个Fredholm[截面](@entry_id:154995)，并通过处理阻碍丛来构造虚拟循环。

3.  **Polyfold理论**：由Hofer, Wysocki和Zehnder发展的更为现代和强大的框架。它引入了**尺度微积分**（scale calculus）和**sc-光滑**等概念，建立了一个可以自然处理导数损失现象的广义“[流形](@entry_id:153038)”——**M-polyfold**。在这个框架下，模空间的正则化问题得到了系统性的解决。

4.  **代数几何方法**：当目标空间 $M$ 是一个光滑射影簇时，[Gromov-Witten不变量](@entry_id:160953)也可以在纯[代数几何](@entry_id:156300)的框架下定义。由Behrend和Fantechi发展的理论，将[模空间](@entry_id:159780)视为一个**Deligne-Mumford叠**（stack），并为其装备一个**完美阻碍理论**（perfect obstruction theory），从而在[代数几何](@entry_id:156300)的Chow群中定义[虚拟基本类](@entry_id:182358)。

一个至关重要的结论是，尽管这些方法的技术路径截然不同，但它们最终殊途同归。在可以进行比较的情况下（即当[辛流形](@entry_id:161608) $M$ 是一个射影簇时），上述所有方法（分析的Kuranishi/Li-Tian/Polyfold方法和代数的Behrend-Fantechi方法）在经过恰当的定向和数据匹配后，会产生相同的[虚拟基本类](@entry_id:182358)，从而定义出完全相同的[Gromov-Witten不变量](@entry_id:160953)。这种跨越分析与代数的一致性，深刻地揭示了[Gromov-Witten不变量](@entry_id:160953)的内在稳健性和数学美感。