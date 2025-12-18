## 引言
在[数值求解偏微分方程](@entry_id:634353)（PDEs）的广阔领域中，传统方法如有限元法（FEM）和[有限差分法](@entry_id:147158)（FDM）长期占据主导地位，但它们对高质量网格的依赖，在面对几何形状复杂、动态演化或存在自由边界的问题时，往往成为计算的瓶颈。[无网格方法](@entry_id:177458)（Meshfree Methods）应运而生，它摆脱了对预定义网格剖分的束缚，直接从一系列离散节点出发构建数值近似，为解决上述挑战提供了革命性的新[范式](@entry_id:161181)。

本文旨在系统性地介绍[无网格方法](@entry_id:177458)的核心思想与应用实践。通过学习本文，读者将深入理解这一强大计算工具的内在机理和广阔的应用前景。文章结构如下：
- **第一章：原理与机制** 将深入探讨支撑[无网格方法](@entry_id:177458)的基础理论。我们将从节点[分布](@entry_id:182848)的几何量化（如填充距离和分离距离）讲起，阐明[多项式再生](@entry_id:753580)（一致性）与稳定性如何共同确保方法的收敛性。接着，将详细介绍两种主流的近似构造技术：[移动最小二乘法](@entry_id:178698)（MLS）和[径向基函数](@entry_id:754004)（RBF）法，并分析它们在伽辽金[弱形式](@entry_id:142897)和强形式配点法中的不同角色。
- **第二章：应用与[交叉](@entry_id:147634)学科联系** 将展示这些理论在实践中的威力。通过求解椭圆、抛物线和双曲型等各类方程，我们将看到[无网格方法](@entry_id:177458)如何处理复杂几何、时变问题和[对流](@entry_id:141806)主导现象。更进一步，本章还将探索其在前沿[交叉](@entry_id:147634)学科中的应用，包括[曲面](@entry_id:267450)上的PDE、非局部与分数阶算子，并揭示其与机器学习中[高斯过程回归](@entry_id:276025)的深刻联系。
- **第三章：动手实践** 将通过一系列精心设计的计算练习，帮助读者将理论知识转化为实践技能，巩固对核心概念的理解。

让我们首先从[无网格方法](@entry_id:177458)最根本的构建模块——其近似理论的原理与机制开始。

## 原理与机制

在[偏微分方程](@entry_id:141332)的数值求解领域，[无网格方法](@entry_id:177458)（Meshfree Methods）提供了一套不依赖于传统网格剖分的强大而灵活的离散化框架。与有限元方法（Finite Element Method, FEM）中形函数（shape functions）的定义和性质严格依赖于单元的几何形状与连通性不同，[无网格方法](@entry_id:177458)直接从散布于求解域内的一组节点（或称为粒子）出发，构建近似函数。这种构造的灵活性使得[无网格方法](@entry_id:177458)在处理大变形、[裂纹扩展](@entry_id:749562)、[自由表面流](@entry_id:265322)等涉及复杂或动态变化的几何域问题时，展现出独特的优势。本章将深入探讨支撑这些方法的核心原理与关键机制，从[近似理论](@entry_id:138536)的基础出发，逐步构建起对主流[无网格方法](@entry_id:177458)及其应用的系统性理解。

### 无网格近似的基本概念

[无网格方法](@entry_id:177458)的核心在于如何仅根据一组离散节点 $\mathcal{X} = \{\boldsymbol{x}_i\}_{i=1}^N \subset \Omega$ 及其对应的节点值来构造一个定义在整个域 $\Omega$ 上的[连续函数](@entry_id:137361)。这个过程的质量与可靠性，取决于节点[分布](@entry_id:182848)的几何特性以及近似构造本身所满足的数学性质。

#### 节点[分布](@entry_id:182848)的几何刻画

为了对[无网格方法](@entry_id:177458)的收敛性和稳定性进行严谨的[数学分析](@entry_id:139664)，我们需要定量地描述节点集的[分布](@entry_id:182848)质量。三个核心几何参数被引入 ：

1.  **填充距离 (Fill Distance)** $h$：填充距离 $h_{X,\Omega}$ 是衡量节点集 $X$ 对区域 $\Omega$ 覆盖程度的指标。它被定义为在 $\Omega$ 中可以放入的最大空心球的半径，其数学表达式为：
    $$
    h = h_{X,\Omega} = \sup_{\boldsymbol{x} \in \Omega} \min_{1 \le i \le N} \|\boldsymbol{x} - \boldsymbol{x}_i\|_2
    $$
    直观上，$h$ 扮演了传统网格方法中“网格尺寸”的角色。一个数值方案要收敛，其基本要求是当节点数量 $N \to \infty$ 时，填充距离 $h \to 0$。在[误差分析](@entry_id:142477)中，近似误差通常表示为 $h$ 的[幂函数](@entry_id:166538)，例如 $O(h^k)$。

2.  **分离距离 (Separation Distance)** $q$：分离距离 $q_X$ 衡量节点之间相互分离的最小程度。它通常定义为所有不同节点对之间距离的一半：
    $$
    q = q_X = \frac{1}{2} \min_{i \ne j} \|\boldsymbol{x}_i - \boldsymbol{x}_j\|_2
    $$
    这个量也被称为节点集 $X$ 的**堆积半径 (packing radius)**。分离距离对于保证数值方案的**稳定性**至关重要。如果两个节点过于接近（$q$ 相对于 $h$ 过小），那么以它们为中心构造的[基函数](@entry_id:170178)会变得近似线性相关，导致离散化后得到的[线性系统](@entry_id:147850)矩阵出现严重的病态（ill-conditioned），使得数值解对微小扰动异常敏感。

3.  **网格比 (Mesh Ratio)** $\rho$：网格比 $\rho$ 是一个无量纲参数，定义为填充距离与分离距离之比：
    $$
    \rho = \frac{h}{q}
    $$
    它综合反映了节点[分布](@entry_id:182848)的均匀性。一个理想的节点集应是在密集覆盖区域（$h$ 小）的同时，节点之间又不过分拥挤（$q$ 不能太小）。如果在一系列加密的节点集中，网格比 $\rho$ 始终被一个与 $N$ 无关的常数所界定，我们就称这样的节点集是**准均匀的 (quasi-uniform)**。准[均匀性](@entry_id:152612)是建立稳健的误差估计和保证数值方法[稳定收敛](@entry_id:199422)的关键条件 。

#### [一致性与收敛性](@entry_id:747723)：[多项式再生](@entry_id:753580)

一个[数值近似](@entry_id:161970)方案要能够收敛到真实解，它必须至少能精确地表示一些简单的函数。在[无网格方法](@entry_id:177458)中，这个基本要求被形式化为**[多项式再生](@entry_id:753580)（Polynomial Reproduction）**或**多项式一致性 (polynomial consistency)**。

一个无网格近似算子 $\Pi_h$，它将一个[连续函数](@entry_id:137361) $u$ 映射到一个近似函数 $\Pi_h u$，如果对于次数不超过 $m$ 的任意多项式 $p \in \mathbb{P}_m$，都能满足 $\Pi_h p = p$，那么我们说该算子具有 **$m$ 阶[多项式再生](@entry_id:753580)能力** 。

[多项式再生](@entry_id:753580)是一致性的体现。它的重要性在于，结合稳定性和节点集的正则性，它直接决定了近似的[收敛阶](@entry_id:146394)。考虑一个[光滑函数](@entry_id:267124) $u \in C^{m+1}(\Omega)$，根据[泰勒定理](@entry_id:144253)，在任意点 $\boldsymbol{x}$ 附近， $u$ 可以展开为一个 $m$ 阶多项式 $T_m[u]$ 和一个余项 $R_{m+1}[u]$ 之和，其中[余项](@entry_id:159839)的大小为 $O(h^{m+1})$。如果我们用一个具有 $m$ 阶再生能力的算子 $\Pi_h$ 来近似 $u$，那么误差为：
$$
u - \Pi_h u = (T_m + R_{m+1}) - \Pi_h(T_m + R_{m+1}) = T_m + R_{m+1} - \Pi_h T_m - \Pi_h R_{m+1}
$$
由于 $\Pi_h$ 再生 $m$ 阶多项式，$\Pi_h T_m = T_m$，因此误差简化为：
$$
u - \Pi_h u = R_{m+1} - \Pi_h R_{m+1}
$$
取范数后得到 $\|u - \Pi_h u\| \le \|R_{m+1}\| + \|\Pi_h R_{m+1}\| \le (1 + \|\Pi_h\|) \|R_{m+1}\|$。如果算子 $\Pi_h$ 是**稳定**的，即其[算子范数](@entry_id:752960) $\|\Pi_h\|$ 有界，那么[误差范数](@entry_id:176398)将主要由泰勒余项决定，即 $\|u - \Pi_h u\| = O(h^{m+1})$。

这个基本原理——**一致性 (再生性) + 稳定性 $\Rightarrow$ 收敛性**——是贯穿所有数值分析的黄金法则。它清楚地表明，仅仅拥有[多项式再生](@entry_id:753580)能力是不够的；必须同时保证近似算子的稳定性，才能获得可靠的收敛结果  。

### 构造无网格近似的主要方法

基于上述理论基础，发展出了多种构造无网格形函数的方法。其中，[移动最小二乘法](@entry_id:178698)和[径向基函数](@entry_id:754004)法是最为重要的两类。

#### [移动最小二乘法](@entry_id:178698) (Moving Least Squares, MLS)

MLS方法不是试图找到一个全局函数来拟合所有数据点，而是在每个评估点 $\boldsymbol{x}$ 处，动态地构造一个局部最佳的[多项式拟合](@entry_id:178856)。

给定一组节点 $\{\boldsymbol{x}_i\}$ 及其对应的参数 $\{u_i\}$，在任意评估点 $\boldsymbol{x}$ 处，我们寻找一个局部多项式 $p(\boldsymbol{y}) = \boldsymbol{p}^T(\boldsymbol{y}) \boldsymbol{a}(\boldsymbol{x})$（其中 $\boldsymbol{p}(\boldsymbol{y})$ 是多项式[基函数](@entry_id:170178)向量，$\boldsymbol{a}(\boldsymbol{x})$ 是待求的系数向量），使得这个多项式在 $\boldsymbol{x}$ 的邻域内与节点数据 $\{u_i\}$ 的加权平方误差最小。这个误差泛函定义为 ：
$$
J(\boldsymbol{a}; \boldsymbol{x}) = \sum_{i=1}^N w_i(\boldsymbol{x}) \left( \boldsymbol{p}^T(\boldsymbol{x}_i) \boldsymbol{a}(\boldsymbol{x}) - u_i \right)^2
$$
这里，$w_i(\boldsymbol{x}) = w(\|\boldsymbol{x}-\boldsymbol{x}_i\|)$ 是一个以 $\boldsymbol{x}$ 为中心、具有[紧支集](@entry_id:276214)的非负**权函数**。权函数定义了“局部”的范围，只有落在其支集内的节点才会对 $\boldsymbol{x}$ 点的近似有贡献。

通过对 $J$ 关于系数 $\boldsymbol{a}(\boldsymbol{x})$求导并令其为零，我们得到一个[线性方程组](@entry_id:148943)，即[正规方程](@entry_id:142238)：
$$
A(\boldsymbol{x}) \boldsymbol{a}(\boldsymbol{x}) = B(\boldsymbol{x}) \boldsymbol{u}
$$
其中矩阵 $A(\boldsymbol{x})$ 和 $B(\boldsymbol{x})$ 的定义为：
$$
A(\boldsymbol{x}) = \sum_{j=1}^N w_j(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_j) \boldsymbol{p}^T(\boldsymbol{x}_j)
$$
$$
B(\boldsymbol{x})_{ki} = w_i(\boldsymbol{x}) p_k(\boldsymbol{x}_i)
$$
矩阵 $A(\boldsymbol{x})$ 被称为**矩量矩阵 (moment matrix)**。如果 $A(\boldsymbol{x})$ 可逆，我们就可以解出系数 $\boldsymbol{a}(\boldsymbol{x})$，并得到在 $\boldsymbol{x}$ 点的近似值 $u^h(\boldsymbol{x})$：
$$
u^h(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) \boldsymbol{a}(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) A^{-1}(\boldsymbol{x}) B(\boldsymbol{x}) \boldsymbol{u}
$$
将上式写成 $u^h(\boldsymbol{x}) = \sum_{i=1}^N N_i(\boldsymbol{x}) u_i$ 的形式，我们便得到了 MLS 形函数 $N_i(\boldsymbol{x})$ 的表达式 ：
$$
N_i(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) A^{-1}(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_i) w_i(\boldsymbol{x})
$$

MLS近似具有以下几个关键特性：

*   **[多项式再生](@entry_id:753580)**：如果多项式基 $\boldsymbol{p}$ 包含了所有次数不超过 $m$ 的多项式，并且矩量矩阵 $A(\boldsymbol{x})$ 处处可逆，那么MLS近似就具有 $m$ 阶再生能力。一个特别重要的推论是，如果[基函数](@entry_id:170178)包含常数1，那么形函数就构成**单位分解 (partition of unity)**，即 $\sum_{i=1}^N N_i(\boldsymbol{x}) = 1$  。
*   **非插值性**：标准的MLS形函数不具备**克罗内克-德尔[塔性质](@entry_id:273153) (Kronecker-delta property)**，即 $N_i(\boldsymbol{x}_j) \neq \delta_{ij}$ 。这意味着近似函数 $u^h(\boldsymbol{x})$ 通常不穿过节点值，即 $u^h(\boldsymbol{x}_j) \neq u_j$。这是因为MLS是最小二乘“拟合”而非“插值”。这一特性给施加本质（Dirichlet）边界条件带来了困难，通常需要借助[拉格朗日乘子法](@entry_id:176596)、罚函数法或修正形函数等特殊技术来处理。
*   **[可逆性](@entry_id:143146)条件**：MLS近似的良定性依赖于矩量矩阵 $A(\boldsymbol{x})$ 的[可逆性](@entry_id:143146)。这要求在权函数 $w$ 的支集内，必须有足够多的、呈“良好”几何分布的节点，使得局部节点集对于所选的多项式基 $\boldsymbol{p}$ 是**单解的 (unisolvent)**。单解性意味着唯一能让所选空间中的多项式在所有这些节点上为零的多项式就是零多项式。如果节点不足或[分布](@entry_id:182848)不当（例如，在二维线性基下，三个节点共线），$A(\boldsymbol{x})$ 就会奇异，导致形函数无定义  。
*   **[标度不变性](@entry_id:180291)**：MLS形函数对于权函数的整体缩放是不变的。若将所有权函数值 $w_i(\boldsymbol{x})$ 乘以一个共同的正常数 $c(\boldsymbol{x})$，得到的形函数 $N_i(\boldsymbol{x})$ 保持不变。这是因为在[最小二乘问题](@entry_id:164198)中，起作用的是权重的相对大小，而非[绝对值](@entry_id:147688) 。

#### [径向基函数](@entry_id:754004)法 (Radial Basis Function, RBF)

RBF是另一大类强大的无网格近似工具。其核心思想是用以各个节点为中心、呈[径向对称](@entry_id:141658)的函数之[线性组合](@entry_id:154743)来构造近似。一个基本的RBF[插值函数](@entry_id:262791)形式如下：
$$
s(\boldsymbol{x}) = \sum_{j=1}^N c_j \phi(\|\boldsymbol{x} - \boldsymbol{x}_j\|)
$$
其中 $\phi: [0, \infty) \to \mathbb{R}$ 是一个一维的**[径向基函数](@entry_id:754004)**，$\|\cdot\|$ 是欧氏范数，$c_j$ 是待定系数。通过在所有节点上施加插值条件 $s(\boldsymbol{x}_i) = u_i$，我们得到一个线性方程组 $A \boldsymbol{c} = \boldsymbol{u}$，其中插值矩阵 $A_{ij} = \phi(\|\boldsymbol{x}_i - \boldsymbol{x}_j\|)$。

RBF方法的一个神奇之处在于其插值[矩阵的可逆性](@entry_id:204560)。对于一大类被称为**严格正定 (strictly positive definite)** 的RBF，只要所有插值节点 $\boldsymbol{x}_i$ 是互不相同的，插值矩阵 $A$ 就保证是**[对称正定](@entry_id:145886)**的，因此必然可逆 。一个函数 $\phi$ 被称为严格正定的，如果对于任意一组不同的点 $\{\boldsymbol{x}_i\}_{i=1}^N$ 和任意非零系数向量 $\boldsymbol{c} \in \mathbb{R}^N \setminus \{0\}$，二次型都严格为正：
$$
\sum_{i=1}^N \sum_{j=1}^N c_i c_j \phi(\|\boldsymbol{x}_i - \boldsymbol{x}_j\|) = \boldsymbol{c}^T A \boldsymbol{c} > 0
$$
严格正定性保证了无论节点如何[分布](@entry_id:182848)（只要互不相同），总能唯一地确定插值系数。常见的光滑（$C^\infty$）正定RBF包括高斯函数 $\phi(r) = \exp(-(\varepsilon r)^2)$ 和逆多二次函数 $\phi(r) = (1+(\varepsilon r)^2)^{-1/2}$。

与这些光滑RBF相关的一个重要概念是**形参数 (shape parameter)** $\varepsilon$。它控制着[基函数](@entry_id:170178)的“形状”：$\varepsilon$ 越小，[基函数](@entry_id:170178)越“平坦”；$\varepsilon$ 越大，[基函数](@entry_id:170178)越“尖锐”。形参数的选择对RBF方法的性能有巨大影响，并带来了一个著名的**权衡原则 (trade-off principle)** ：
*   **精度**：对于[光滑函数](@entry_id:267124)，使用更平坦的[基函数](@entry_id:170178)（减小 $\varepsilon$）可以获得更高的精度。在极限情况下（即“平坦极限” $\varepsilon \to 0$），光滑RBF插值可以达到谱精度（误差衰减速度快于任何多项式阶）。
*   **稳定性**：然而，当 $\varepsilon \to 0$ 时，不同节点上的[基函数](@entry_id:170178)变得越来越相似，导致插值矩阵 $A$ 趋近于一个秩为1的矩阵（所有元素都接近 $\phi(0)$），其条件数会以超乎想象的速度（如指数级）增长。这使得在标准浮点数精度下，数值求解变得极其不稳定。

有趣的是，在平坦极限 $\varepsilon \to 0$ 时，RBF[插值函数](@entry_id:262791)会收敛于一个特定的**[多项式插值](@entry_id:145762)函数** 。这一深刻的理论联系催生了现代的稳定算法（如RBF-QR），这些算法通过构造一个等价的、良态的基（如[正交多项式](@entry_id:146918)基）来绕过直接求解病态RBF系统的困难，从而在享受平坦RBF高精度的同时，保持数值稳定。

### 在[偏微分方程](@entry_id:141332)求解中的应用

构造了形函数之后，下一步就是将其应用于[求解PDE](@entry_id:138485)。主流的应用方式分为基于[弱形式](@entry_id:142897)的[伽辽金法](@entry_id:749698)和基于强形式的配点法。

#### [弱形式](@entry_id:142897)方法：伽辽金框架

在弱形式（或[变分形式](@entry_id:166033)）方法中，我们将PDE转化为一个[积分方程](@entry_id:138643)。以一个标准的椭圆[边值问题](@entry_id:193901)为例，我们寻找满足[本质边界条件](@entry_id:173524)的函数 $u$，使得对于所有满足[齐次边界条件](@entry_id:750371)的[检验函数](@entry_id:166589) $v$，某个积分等式（弱形式）成立。

**[无网格伽辽金法](@entry_id:751897) (Element-Free Galerkin, EFG)** 和 **[再生核](@entry_id:262515)粒子法 (Reproducing Kernel Particle Method, RKPM)** 是此类方法的杰出代表 。它们的核心思想是：

1.  **近似空间**：使用MLS（在EFG中）或[再生核](@entry_id:262515)（在RKPM中）构造的形函数 $\{\psi_I\}$ 来构建离散的[试探函数](@entry_id:756165)空间和[检验函数](@entry_id:166589)空间。即 $u_h(\boldsymbol{x}) = \sum_I \psi_I(\boldsymbol{x}) u_I$ 和 $v_h(\boldsymbol{x}) = \sum_I \psi_I(\boldsymbol{x}) v_I$。
2.  **离散系统**：将这些近似表达式代入PDE的[弱形式](@entry_id:142897)，通过选取一组基检验函数（例如 $v_h = \psi_J$），得到一个关于节点未知数 $\{u_I\}$ 的[线性方程组](@entry_id:148943) $K\boldsymbol{u} = \boldsymbol{f}$。
3.  **数值积分**：由于形函数 $\psi_I$ 通常是复杂的[有理函数](@entry_id:154279)，弱形式中的积分（如 $\int_\Omega \nabla \psi_I \cdot \nabla \psi_J \, d\Omega$）无法解析计算。因此，必须采用数值积分。一个标准做法是引入一个独立的**背景网格 (background mesh)**，它仅用于划分积分区域，而不用于定义形函数的连通性。在每个背景单元上，采用[高斯求积](@entry_id:146011)等标准方法进行数值积分。这是“无网格”方法通常需要一个“网格”用于积分的微妙之处。

#### 强形式方法：配点法

强形式方法直接在离散点上强制PDE及其边界条件成立。这类方法因其概念简单、易于实现而广受欢迎。

**Kansa方法** 是一种经典的基于全局RBF的强形式配点法 。其步骤如下：
1.  **近似**：用全局RBF展开式 $u_h(\boldsymbol{x}) = \sum_{j=1}^N \alpha_j \phi(\|\boldsymbol{x}-\boldsymbol{x}_j\|)$ 来近似解。
2.  **配点**：选取一组配点（通常与RB[F中心](@entry_id:149090)点重合），包括 $N_I$ 个内部点和 $N_B$ 个[边界点](@entry_id:176493)。
3.  **强制方程**：在内部配点上，要求 $L u_h = f$；在边界配点上，要求 $B u_h = g$。这会形成一个 $N \times N$ 的[线性系统](@entry_id:147850) $A\boldsymbol{\alpha} = \boldsymbol{b}$，用以求解系数 $\boldsymbol{\alpha}$。

Kansa方法的一个显著特点是其生成的矩阵 $A$ 通常是**非对称的**，即使原PDE的微分算子是自伴的。例如，矩阵的第 $i$ 行对应于算子 $L$ 作用在以所有节点 $\boldsymbol{x}_j$ 为中心的[基函数](@entry_id:170178)上，并在点 $\boldsymbol{x}_i$ 求值，即 $A_{ij} = (L\phi(\|\cdot - \boldsymbol{x}_j\|))(\boldsymbol{x}_i)$。而 $A_{ji} = (L\phi(\|\cdot - \boldsymbol{x}_i\|))(\boldsymbol{x}_j)$ 通常与 $A_{ij}$ 不相等。也存在构造对称配点矩阵的方法，但这需要更复杂的算子作用方式，例如将算子同时作用于[核函数](@entry_id:145324)的两个变量上，如 $A_{ij} = L^{\boldsymbol{x}} L^{\boldsymbol{y}} \phi(\|\boldsymbol{x}-\boldsymbol{y}\|)|_{\boldsymbol{x}=\boldsymbol{x}_i, \boldsymbol{y}=\boldsymbol{x}_j}$。

另一类重要的强形式方法是**局部[无网格方法](@entry_id:177458)**，如**RBF生成的有限差分 (RBF-FD)**。与全局方法不同，它在每个节点 $\boldsymbol{x}_i$ 处，仅利用其邻近的一个小“计算云”或“模板” (stencil) 上的节点来近似[微分算子](@entry_id:140145)。通过要求近似在多项式空间上精确，可以计算出差分权重。这种方法最终产生的系统矩阵是**稀疏的**，这在计算上是一个巨大的优势。

### 计算考量：系统结构与求解器

选择全局方法还是局部方法，对最终[线性系统](@entry_id:147850)的结构和求解效率有着决定性的影响 。

*   **全局方法**（如Kansa方法）：
    *   **系统结构**：由于使用了全局支撑的[基函数](@entry_id:170178)，每个节点都与其他所有节点相互作用，产生的线性系统矩阵 $A$ 是**稠密的**。
    *   **计算成本**：存储一个[稠密矩阵](@entry_id:174457)需要 $O(N^2)$ 的内存。在使用[迭代法](@entry_id:194857)（如GMRES）求解时，核心的[矩阵向量乘法](@entry_id:140544)操作每次需要 $O(N^2)$ 的计算量。
    *   **求解**：由于矩阵通常是病态的（尤其是在RBF中追求高精度时），迭代求解器可能收敛缓慢甚至停滞。直接求解法（如[LU分解](@entry_id:144767)）虽然稳健，但计算成本高达 $O(N^3)$，限制了可求解问题的规模。

*   **局部方法**（如EFG, RBF-FD）：
    *   **系统结构**：由于每个节点的近似只依赖于其邻近的 $k$ 个节点（其中 $k \ll N$），产生的系统矩阵是**稀疏的**，每行只有 $O(k)$ 个非零元。
    *   **计算成本**：存储稀疏矩阵仅需 $O(kN)$ 的内存。[矩阵向量乘法](@entry_id:140544)的成本也降至 $O(kN)$。
    *   **求解**：[稀疏性](@entry_id:136793)使得这类系统对大规模计算极具吸[引力](@entry_id:175476)。它们适用于高效的[迭代求解器](@entry_id:136910)，尤其是当与强大的预条件子结合时。对于椭圆型PDE产生的[稀疏系统](@entry_id:168473)，**[代数多重网格](@entry_id:140593)法 (Algebraic Multigrid, AMG)** 是一种特别有效的预条件策略，它能够仅根据矩阵的代数信息构造多层次的求解结构，从而实现接近 $O(N)$ 的最优计算复杂度。

综上所述，从全局稠密系统到局部[稀疏系统](@entry_id:168473)的转变，是[无网格方法](@entry_id:177458)从理论探索走向大规模科学与工程计算的关键一步。它用近似构造上的少许复杂性，换来了[计算效率](@entry_id:270255)和问题规模上的巨大飞跃。