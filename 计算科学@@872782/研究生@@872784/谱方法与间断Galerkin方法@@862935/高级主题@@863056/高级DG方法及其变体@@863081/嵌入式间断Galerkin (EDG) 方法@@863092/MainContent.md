## 引言
在现代科学与工程计算领域，对复杂物理现象进行高保真模拟的需求日益增长，这推动了对高效、稳健且灵活的数值方法的不懈追求。嵌入式间断伽辽金（Embedded Discontinuous Galerkin, EDG）方法正是在这一背景下应运而生的一种先进有限元技术。作为混合间断伽辽金（HDG）方法的一个重要变体，EDG通过一种巧妙的设计，成功地在传统连续Galerkin（CG）方法的计算效率与间断Galerkin（DG）方法的局部守恒性和灵活性之间取得了精妙的平衡。

本文旨在系统性地解决高性能数值方法中的一个核心挑战：如何在保证[高阶精度](@entry_id:750325)的同时，构建一个计算上易于处理的代数系统。[EDG方法](@entry_id:748800)通过其独特的“嵌入式”思想，即利用一个全局连续的迹变量来耦合不连续的单元内部解，为这一问题提供了优雅的解决方案。在接下来的章节中，读者将深入学习[EDG方法](@entry_id:748800)的内在逻辑和强大功能。首先，在“原理与机制”一章中，我们将剖析[EDG方法](@entry_id:748800)的基本公式、[代数结构](@entry_id:137052)以及[静态凝聚](@entry_id:176722)等核心技术。接着，在“应用与跨学科[交叉](@entry_id:147634)”一章中，我们将展示该方法在[流体力学](@entry_id:136788)、[固体力学](@entry_id:164042)、波动物理等多个前沿领域的广泛适用性。最后，“实践练习”部分将提供一系列精心设计的问题，帮助您将理论知识转化为解决实际问题的能力。

## 原理与机制

本章深入探讨嵌入式间断Galerkin（Embedded Discontinuous Galerkin, EDG）方法的核心原理与运作机制。作为一种混合间断Galerkin（Hybridizable Discontinuous Galerkin, HDG）方法的变体，[EDG方法](@entry_id:748800)通过在网格骨架上引入一个全局连续的迹变量，巧妙地平衡了局部守恒性、[计算效率](@entry_id:270255)和与传统连续Galerkin（Continuous Galerkin, CG）方法的联系。我们将从基本公式入手，逐步揭示其[代数结构](@entry_id:137052)、计算优势以及理论特性。

### 杂交概念与EDG公式

为了阐明[EDG方法](@entry_id:748800)的基本构造，我们考虑一个典型的二阶椭圆模型问题，即泊松方程或[扩散方程](@entry_id:170713)，定义在有界Lipschitz区域 $\Omega \subset \mathbb{R}^d$ 上：
$$
-\nabla \cdot (\kappa \nabla u) = f \quad \text{in } \Omega, \qquad u=g \quad \text{on } \partial \Omega
$$
其中，[扩散](@entry_id:141445)系数 $\kappa(\boldsymbol x)$ 是一致正定且有界的，$f \in L^2(\Omega)$ 是[源项](@entry_id:269111)，$g$ 是[Dirichlet边界条件](@entry_id:142800)。

[EDG方法](@entry_id:748800)的第一步是将这个[二阶偏微分方程](@entry_id:175326)重写为一个一阶系统。我们引入一个表示通量的变量 $\boldsymbol{q} := -\kappa \nabla u$。这样，原问题就等价于求解 $(u, \boldsymbol{q})$ 使得：
$$
\kappa^{-1}\boldsymbol{q} + \nabla u = 0 \quad \text{in } \Omega
$$
$$
\nabla \cdot \boldsymbol{q} = f \quad \text{in } \Omega
$$

接下来，我们将求解域 $\Omega$ 剖分成一个由单元 $K$ 组成的网格 $\mathcal{T}_h$。与标准DG方法类似，我们在每个单元 $K$ 内部寻找近似解 $(u_h, \boldsymbol{q}_h)$，这些解在单元之间可以是间断的。我们在每个单元 $K$上对上述[一阶系统](@entry_id:147467)进行[弱形式](@entry_id:142897)化。将第一个方程乘以一个向量测试函数 $\boldsymbol{v}$，第二个方程乘以一个标量测试函数 $w$，然后在单元 $K$ 上积分，并通过[分部积分](@entry_id:136350)（散度定理），我们得到：
$$
(\kappa^{-1}\boldsymbol{q}_h, \boldsymbol{v})_K - (u_h, \nabla \cdot \boldsymbol{v})_K + \langle u_h, \boldsymbol{v} \cdot \boldsymbol{n} \rangle_{\partial K} = 0
$$
$$
-(\boldsymbol{q}_h, \nabla w)_K + \langle \boldsymbol{q}_h \cdot \boldsymbol{n}, w \rangle_{\partial K} = (f,w)_K
$$
其中 $(\cdot,\cdot)_K$ 表示在单元 $K$ 上的 $L^2$ [内积](@entry_id:158127)，$\langle \cdot, \cdot \rangle_{\partial K}$ 表示在单元边界 $\partial K$ 上的 $L^2$ [内积](@entry_id:158127)，$\boldsymbol{n}$ 是 $\partial K$ 上的单位外法向向量。

**杂交（Hybridization）** 的核心思想是引入一个新的未知量，即定义在网格骨架（所有单元面的集合 $\mathcal{E}_h$）上的 **迹变量** $\widehat{u}_h$。这个变量旨在逼近解 $u$ 在单元边界上的迹。引入 $\widehat{u}_h$ 后，我们用它来代替[弱形式](@entry_id:142897)中的边界项 $u_h$。同时，法向通量 $\boldsymbol{q}_h \cdot \boldsymbol{n}$ 也被一个 **[数值通量](@entry_id:752791)** $\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n}$ 所取代。

对于[EDG方法](@entry_id:748800)，这些数值通量的选择如下 [@problem_id:3383206]：
1.  解的迹由迹变量直接代替：$u|_{\partial K} \to \widehat{u}_h$。
2.  法向通量的[数值通量](@entry_id:752791)采用Lax-Friedrichs形式，并包含一个稳定化项：$\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n} := \boldsymbol{q}_h \cdot \boldsymbol{n} - \tau(u_h - \widehat{u}_h)$。

这里的 $\tau > 0$ 是一个逐面定义的 **稳定化参数**，它惩罚单元内部解 $u_h$ 与骨架上的迹变量 $\widehat{u}_h$ 之间的不匹配。将这些[数值通量](@entry_id:752791)代入局部[弱形式](@entry_id:142897)，我们得到[EDG方法](@entry_id:748800)的局部方程：对于每个单元 $K \in \mathcal{T}_h$，寻找 $(u_h, \boldsymbol{q}_h)$ 使得对于所有来自相应多项式空间的测试函数 $(w, \boldsymbol{v})$，以下方程成立：
$$
(\kappa^{-1}\boldsymbol{q}_h, \boldsymbol{v})_K - (u_h, \nabla \cdot \boldsymbol{v})_K + \langle \widehat{u}_h, \boldsymbol{v} \cdot \boldsymbol{n} \rangle_{\partial K} = 0
$$
$$
-(\boldsymbol{q}_h, \nabla w)_K + \langle \boldsymbol{q}_h \cdot \boldsymbol{n} - \tau(u_h - \widehat{u}_h), w \rangle_{\partial K} = (f,w)_K
$$
这些方程定义了每个单元内的局部解 $(u_h, \boldsymbol{q}_h)$ 如何依赖于定义在其边界 $\partial K$ 上的迹变量 $\widehat{u}_h$。

### 连续[迹空间](@entry_id:756085)：“嵌入式”的本质

[EDG方法](@entry_id:748800)与其他[HDG方法](@entry_id:170956)的根本区别在于对迹变量 $\widehat{u}_h$ 所属[函数空间](@entry_id:143478)的选择。EDG的“嵌入式”特性正体现在这里 [@problem_id:3383263]。

我们为[离散变量](@entry_id:263628)选择以下[多项式空间](@entry_id:144410) [@problem_id:3383208]：
*   **单元内部标量场 $u_h$**：属于分片[多项式空间](@entry_id:144410) $V_h^k = \{ v \in L^2(\Omega) : v|_K \in P^k(K) \ \forall K \in \mathcal{T}_h \}$。
*   **单元内部向量场 $\boldsymbol{q}_h$**：属于分片[多项式空间](@entry_id:144410) $\boldsymbol{W}_h^k = \{ \boldsymbol{w} \in [L^2(\Omega)]^d : \boldsymbol{w}|_K \in [P^k(K)]^d \ \forall K \in \mathcal{T}_h \}$。
*   **骨架迹变量 $\widehat{u}_h$**：属于一个在整个网格骨架 $\mathcal{E}_h$ 上 **全局连续** 的分片[多项式空间](@entry_id:144410) $\widehat{V}_h^k = \{ \widehat{v} \in C^0(\mathcal{E}_h) : \widehat{v}|_F \in P^k(F) \ \forall F \in \mathcal{E}_h \}$。

这里 $P^k(K)$ 表示在单元 $K$ 上次数最高为 $k$ 的[多项式空间](@entry_id:144410)。关键在于 $\widehat{V}_h^k \subset C^0(\mathcal{E}_h)$ 的要求。这意味着迹变量 $\widehat{u}_h$ 在相邻单元共享的顶点和边上是单值的。相比之下，标准的[HDG方法](@entry_id:170956)允许 $\widehat{u}_h$ 在单元面的边界处不连续。

这个连续性要求是[EDG方法](@entry_id:748800)设计的核心动机 [@problem_id:3383229]。它使得全局耦合系统的结构变得类似于标准连续Galerkin（CG）方法。在CG方法中，全局未知数（通常是节点值）定义了一个全局 $C^0$ 的函数，其稀疏矩阵的邻接关系直接反映了网格的拓扑结构。在EDG中，通过[静态凝聚](@entry_id:176722)消去所有单元内部的自由度后，剩下的全局未知数恰好是定义在连续[迹空间](@entry_id:756085) $\widehat{V}_h^k$ 上的自由度。由于这个空间的连续性，其自由度（例如，在网格顶点和边上的值）也具有与CG方法类似的局部连接性。因此，EDG的全局[系统矩阵](@entry_id:172230)具有与CG方法相似的稀疏模式和规模，这使得求解更为高效。从这个角度看，[EDG方法](@entry_id:748800)可以被视为一种 **$H^1$-嵌入的[混合方法](@entry_id:163463)**：它将间断的单元内部解通过一个全局 $H^1$ 共形的[迹空间](@entry_id:756085)“粘合”在一起 [@problem_id:3383263]。

### [全局系统组装](@entry_id:749932)与[静态凝聚](@entry_id:176722)

局部方程建立了单元内部解 $(u_h, \boldsymbol{q}_h)$ 与迹变量 $\widehat{u}_h$ 之间的关系。为了求解全局唯一的 $\widehat{u}_h$，我们需要一个全局耦合方程。这个方程源于物理上的通量[守恒定律](@entry_id:269268)，即在没有内部源或汇的情况下，流入一个界面的通量必须等于流出的通量。

在EDG框架中，这通过要求数值通量 $\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n}$ 在内部界面上是连续的（弱形式意义下）来实现。具体而言，对于所有属于[迹空间](@entry_id:756085)（且在Dirichlet边界上为零）的测试函数 $\mu$，数值通量在整个网格骨架上的积分和为零 [@problem_id:3383206]：
$$
\sum_{K \in \mathcal{T}_h} \langle \widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n}, \mu \rangle_{\partial K \setminus \partial\Omega} = 0
$$
将[数值通量](@entry_id:752791)的定义 $\widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n} = \boldsymbol{q}_h \cdot \boldsymbol{n} - \tau(u_h - \widehat{u}_h)$ 代入，就得到了一个只涉及 $(u_h, \boldsymbol{q}_h)$ 和 $\widehat{u}_h$ 的全局方程。

下一个关键步骤是 **[静态凝聚](@entry_id:176722)（static condensation）**，这是一个纯代数过程，它使得[EDG方法](@entry_id:748800)在计算上极具吸[引力](@entry_id:175476) [@problem_id:3383262]。在每个单元 $K$ 上，离散化的局部方程可以写成一个矩阵块系统。令 $x_K$ 为单元 $K$ 内部未知数 $(u_h|_K, \boldsymbol{q}_h|_K)$ 的系数向量，$\lambda_K$ 为迹变量 $\widehat{u}_h$ 在边界 $\partial K$ 上的系数向量。该局部系统可以表示为：
$$
\begin{pmatrix} A_K & B_K \\ B_K^T & D_K \end{pmatrix}
\begin{pmatrix} x_K \\ \lambda_K \end{pmatrix}
=
\begin{pmatrix} b_K \\ g_K \end{pmatrix}
$$
其中矩阵 $A_K$ 代表单元内部未知数之间的相互作用，$B_K$ 和 $B_K^T$ 代表内部未知数与边界迹的耦合，$D_K$ 代表迹未知数之间的直接相互作用。由于单元内部的[基函数](@entry_id:170178)只在 $K$ 上有支撑，它们与其他单元的内部变量是[解耦](@entry_id:637294)的。因此，$A_K$ 对每个单元都是一个可逆的小矩阵。

[静态凝聚](@entry_id:176722)的过程如下：
1.  从第一个块行方程中求解 $x_K$：
    $A_K x_K = b_K - B_K \lambda_K \implies x_K = A_K^{-1} (b_K - B_K \lambda_K)$
2.  将 $x_K$ 的表达式代入第二个块行方程：
    $B_K^T \left( A_K^{-1} (b_K - B_K \lambda_K) \right) + D_K \lambda_K = g_K$
3.  整理后得到一个只含迹变量 $\lambda_K$ 的方程：
    $\left( D_K - B_K^T A_K^{-1} B_K \right) \lambda_K = g_K - B_K^T A_K^{-1} b_K$

矩阵 $S_K = D_K - B_K^T A_K^{-1} B_K$ 被称为 $A_K$ 在该系统中的 **[舒尔补](@entry_id:142780)（Schur complement）**。它代表了将单元内部物理过程凝聚到边界上的等效刚度矩阵。

全局系统是通过将所有单元的[舒尔补](@entry_id:142780)贡献组装起来形成的。令 $\lambda$ 为全局连续迹变量 $\widehat{u}_h$ 的系数向量，而 $\lambda_K = R_K \lambda$ 是通过一个[限制算子](@entry_id:754316) $R_K$ 得到的局部向量。全局系统矩阵 $S$ 就是：
$$
S \lambda = \left( \sum_{K \in \mathcal{T}_h} R_K^T S_K R_K \right) \lambda = \text{RHS}
$$
这个过程的优美之处在于，所有单元内部的未知数 $x_K$ 都可以通过完全并行的局部计算被消去。最终需要求解的全局线性系统 $S \lambda = \text{RHS}$ 的规模仅由迹变量 $\widehat{u}_h$ 的自由度决定。一旦求得全局的 $\lambda$，每个单元的内部解 $x_K$ 也可以通过局部反代并行地恢复出来。对于[扩散](@entry_id:141445)问题，若采用对称的[数值通量](@entry_id:752791)，得到的全局矩阵 $S$ 是[对称正定](@entry_id:145886)的。

### 计算优势与自由度分析

[EDG方法](@entry_id:748800)相对于其他DG变体的主要动机在于其[计算效率](@entry_id:270255)，这直接源于其连续[迹空间](@entry_id:756085)的设定 [@problem_id:3383229]。

**全局自由度（DOF）的显著减少** 是最核心的优势。我们可以具体量化这一优势。考虑一个二维平面上的三角形网格，包含 $N_v$ 个顶点和 $N_e$ 个单元。根据[平面图的欧拉公式](@entry_id:264421)，边的数量 $N_{edges} = N_v + N_e - 1$。我们来比较多项式次数为 $k$ 时不同方法的全局自由度数量 [@problem_id:3383235]：

*   **[HDG方法](@entry_id:170956)**：迹变量在每个边上是独立的，但在边与边之间不连续。一条边上的 $k$ 次多项式有 $k+1$ 个自由度。因此，总的全局自由度为：
    $N_{HDG} = (k+1) N_{edges} = (k+1)(N_v + N_e - 1)$

*   **[EDG方法](@entry_id:748800)**：迹变量在整个骨架上是连续的。其自由度可以分解为与顶点关联的和与边内部关联的。有 $N_v$ 个顶点，每个顶点贡献1个自由度。每条边有 $k-1$ 个内部自由度（总共 $k+1$ 个自由度，减去两个端点）。总的全局自由度为：
    $N_{EDG} = N_v + (k-1) N_{edges} = N_v + (k-1)(N_v + N_e - 1) = k N_v + (k-1)N_e - k + 1$

*   **CG方法**：全局自由度包括顶点、边内部和单元内部的自由度。其总数为：
    $N_{CG} = N_v + (k-1)N_{edges} + \binom{k-1}{2}N_e = k N_v + \frac{k(k-1)}{2}N_e - k + 1$

通过比较可以发现，$N_{EDG}$ 远小于 $N_{HDG}$，尤其是在 $k$ 和单元数量较大时。$N_{EDG}$ 的规模与 $N_{CG}$ 更加接近，但EDG的优势在于它只耦合了较低维度的骨架变量。

此外，在[静态凝聚](@entry_id:176722)过程中被消去的单元内部自由度的数量也相当可观。例如，在二维情况下，单元内部[标量场](@entry_id:151443) $u_h|_K \in P^k(K)$ 的自由度为 $\frac{(k+1)(k+2)}{2}$，向量场 $\boldsymbol{q}_h|_K \in [P^k(K)]^2$ 的自由度为 $(k+1)(k+2)$ [@problem_id:3383217]。这些大量的自由度被局部处理，无需进入全局求解过程。

值得强调的是，尽管EDG在[代数结构](@entry_id:137052)上与CG有相似之处，但它仍然是一个[DG方法](@entry_id:748369)，并完整地保留了[DG方法](@entry_id:748369)的一个关键优点：**局部守恒性**。通过在局部弱形式中选择测试函数 $w=1$（[常数函数](@entry_id:152060)属于[多项式空间](@entry_id:144410)），可以轻易证明数值通量在每个单元边界上的积分等于单元内部源项的积分，即 $\int_{\partial K} \widehat{\boldsymbol{q}}_h \cdot \boldsymbol{n} \, ds = \int_K f \, dx$ [@problem_id:3383229]。这是许多物理和工程应用中至关重要的性质。

### 稳定化参数的角色及与其他方法的联系

稳定化参数 $\tau$ 在[EDG方法](@entry_id:748800)中扮演着多重角色，理解它有助于我们将EDG置于更广阔的数值方法图景中。

首先，$\tau$ 对于保证方法的 **稳定性和收敛性** 至关重要。对于[扩散](@entry_id:141445)问题，罚项 $\tau(u_h - \widehat{u}_h)$ 必须足够大，以确保离散双线性形式的[矫顽性](@entry_id:159399)（coercivity）。理论分析表明，$\tau$ 的尺度应与[扩散](@entry_id:141445)系数 $\kappa$ 和网格尺寸 $h$ 相关，典型的选择是 $\tau \sim \kappa/h$。对于[对流](@entry_id:141806)占优问题，$\tau$ 的选择则应与[对流](@entry_id:141806)速度相关，如 $\tau \sim |\boldsymbol{\beta} \cdot \boldsymbol{n}|$，以提供必要的上风稳定化 [@problem_id:3383266]。

其次，$\tau$ 的值揭示了EDG与CG方法之间的深刻联系。罚项可以被看作是[弱形式](@entry_id:142897)下施加约束 $u_h = \widehat{u}_h$ 的一种方式。在极限情况 $\tau \to \infty$ 下，为了使总能量有界，约束 $u_h = \widehat{u}_h$ 必须被强行满足。由于 $\widehat{u}_h$ 是全局连续的，这意味着间断解 $u_h$ 的迹也必须变得连续。此时，EDG解将收敛于CG解 [@problem_id:3383266]。这个极限行为为理解EDG提供了重要的理论视角，但也警示我们，在实际计算中过大的 $\tau$ 会导致全局系统[矩阵的条件数](@entry_id:150947)恶化。

最后，通过一个简单的变换，我们可以揭示EDG与另一种著名的DG方法——[对称内部罚](@entry_id:755719)分Galerkin（Symmetric Interior Penalty Galerkin, SIPG）方法之间的等价关系。考虑一个内部面上的罚项 $\tau |u_h^- - \lambda|^2 + \tau |u_h^+ - \lambda|^2$，其中 $u_h^-$ 和 $u_h^+$ 是来自左右单元的迹。通过对共享的迹变量 $\lambda$ 进行最小化，我们发现最优的 $\lambda = (u_h^- + u_h^+)/2$。将此最优值代回，该罚项等价于 $\frac{\tau}{2}[u_h]^2$，其中 $[u_h] = u_h^- - u_h^+$ 是解的跳跃。而[SIPG方法](@entry_id:754927)的罚项形式为 $\frac{\sigma}{h}[u_h]^2$。通过比较这两个表达式，我们发现在一维均匀网格上，两种方法的罚分机制是等价的，其参数关系为 $\sigma = \frac{\tau h}{2}$ [@problem_id:3383226]。这表明EDG的杂交和稳定化机制可以被视为一种实现内部罚分思想的替代路径。

### 收敛性质

对于实际应用，一个[数值方法的收敛性](@entry_id:635470)质是其可靠性的最终衡量标准。[EDG方法](@entry_id:748800)继承了DG类方法优良的收敛特性。特别地，对于解析解（即在每个单元内足够光滑的解），[EDG方法](@entry_id:748800)能够实现 **谱收敛（spectral convergence）**，也称为[指数收敛](@entry_id:142080)。

谱收敛指的是在固定网格剖分下，当多项式次数 $k \to \infty$ 时，误差以指数形式衰减，即误差 $\sim e^{-\alpha k}$。要达到这种高速收敛，需要满足三个条件 [@problem_id:3383219]：
1.  **一致稳定性**：方法的离散双线性形式的矫顽性和连续性常数必须独立于（或可控地依赖于）多项式次数 $k$。这通常通过恰当地选择稳定化参数来实现。为了抵消高阶多项式在边界上的不良行为（由[逆不等式](@entry_id:750800)揭示），$\tau$ 需要随 $k$ 增长，典型的选择是 $\tau \sim k^2/h$。
2.  **相容性与[Galerkin正交性](@entry_id:173536)**：离散系统必须准确地表示连续问题。在实践中，这意味着积分必须精确计算。由于EDG的[弱形式](@entry_id:142897)中包含多项式乘积（例如，在稳定化项中，两个次数为 $k$ 的多项式相乘得到次数为 $2k$ 的多项式），所使用的[数值积分](@entry_id:136578)（quadrature）法则必须对次数至少为 $2k$ 的多项式精确。如果满足此条件，则可以避免“变分犯罪”（variational crime），保证[Galerkin正交性](@entry_id:173536)成立。
3.  **[最佳逼近性质](@entry_id:166240)**：函数空间必须能够以指数速率逼近解析解。这是[多项式逼近理论](@entry_id:753571)的一个经典结果：对于解析函数，其在 $P_k$ 空间中的最佳逼近误差在 $H^1$ 范数下随 $k$ 呈指数衰减。

当这三个条件同时满足时，根据[Céa引理](@entry_id:165386)或其推广（[Strang引理](@entry_id:168943)），可以证明[EDG方法](@entry_id:748800)的解将以指数速率收敛到真解。这使得[EDG方法](@entry_id:748800)在需要高精度解的科学与工程计算中尤为强大。