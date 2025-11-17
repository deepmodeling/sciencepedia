## 引言
在使用[谱方法](@entry_id:141737)和间断伽辽金（DG）等现代数值技术[求解偏微分方程](@entry_id:138485)（PDEs）时，我们致力于将无限维的连续问题转化为有限维的代数系统。这一转化的核心产物是一系列结构化的矩阵，其中质量矩阵、刚度矩阵和[对流矩阵](@entry_id:747848)构成了整个离散框架的基石。它们不仅是计算过程中的中间步骤，更是连接连续物理定律与离散[数值算法](@entry_id:752770)的关键桥梁。

然而，从抽象的[伽辽金投影](@entry_id:145611)原理到理解这些矩阵的具体形态、内在属性及其物理意义，存在一个概念上的飞跃。许多学习者知道这些矩阵的存在，但可能不完全清楚它们为何具有特定的代数性质（如对称性、正定性），这些性质又如何影响数值格式的稳定性与精度，以及它们在不同学科问题中扮演的统一角色。

本文旨在填补这一知识鸿沟。在接下来的章节中，我们将系统地探索这些核心矩阵。第一章“原理与机制”将深入其定义，揭示其代数性质与物理内涵，并阐述它们如何从[弱形式](@entry_id:142897)中产生及组装。第二章“应用与交叉学科联系”将展示这些矩阵在[计算流体力学](@entry_id:747620)、电磁学、[最优控制](@entry_id:138479)乃至数据科学等多个领域的实际应用，突显其普适性。最后，第三章“动手实践”将通过具体计算和分析问题，帮助读者将理论知识转化为实践技能。

## 原理与机制

在上一章中，我们介绍了利用伽辽金方法将[偏微分方程](@entry_id:141332)（PDEs）转化为[代数方程](@entry_id:272665)组的基本思想。这一转化的核心在于选择合适的[基函数](@entry_id:170178)，并将原方程的解投影到这些[基函数](@entry_id:170178)张成的[有限维空间](@entry_id:151571)上。这个过程自然而然地引出了一系列具有深刻物理和数学意义的矩阵，它们是[谱方法](@entry_id:141737)和间断伽辽金（DG）方法的核心构件。本章将深入探讨这些关键矩阵——[质量矩阵](@entry_id:177093)、刚度矩阵和[对流矩阵](@entry_id:747848)——的原理、性质及其在构建数值格式中的作用。

### 局部单元矩阵：基本定义与性质

在深入研究复杂的多单元（multi-element）问题之前，我们首先在一个孤立的计算单元（或称“元”，element）$K$ 上考察这些矩阵的“局部”形式。假设我们使用一组[局部基](@entry_id:151573)函数 $\{\phi_i\}_{i=1}^N$ 来近似单元 $K$ 上的解。这些矩阵的定义源于对控制方程中不同项进行伽辽金[弱形式](@entry_id:142897)积分。

#### 形式化定义

考虑一个位于 $\mathbb{R}^d$ 中的计算单元 $K$。对于定义在 $K$ 上的任意两个[基函数](@entry_id:170178) $\phi_i$ 和 $\phi_j$，我们定义以下三个核心的局部单元矩阵：

1.  **[质量矩阵](@entry_id:177093) (Mass Matrix)** $M$：其元素 $M_{ij}$ 定义为两个[基函数](@entry_id:170178)的 $L^2(K)$ [内积](@entry_id:158127)。它代表了系统中与时间导数或零阶项相关的“惯性”或“容量”。
    $$
    M_{ij} = \int_K \phi_i(x) \phi_j(x) \, dx
    $$

2.  **刚度矩阵 (Stiffness Matrix)** $K$：其元素 $K_{ij}$ 定义为两个[基函数](@entry_id:170178)梯度的[点积](@entry_id:149019)在 $K$ 上的积分。它通常来源于[扩散](@entry_id:141445)项（如拉普拉斯算子），代表了系统中与空间[二阶导数](@entry_id:144508)相关的物理过程，如[热传导](@entry_id:147831)或动量粘性[扩散](@entry_id:141445)。
    $$
    K_{ij} = \int_K \nabla \phi_i(x) \cdot \nabla \phi_j(x) \, dx
    $$

3.  **[对流矩阵](@entry_id:747848) (Convection Matrix)** $C$：其元素 $C_{ij}$ 来自于[对流](@entry_id:141806)项的离散。给定一个[速度场](@entry_id:271461) $\boldsymbol{a}$，它定义为：
    $$
    C_{ij} = \int_K \phi_i(x) (\boldsymbol{a} \cdot \nabla \phi_j(x)) \, dx
    $$
    该矩阵描述了由速度场 $\boldsymbol{a}$ 引起的物理量的输运。

#### 内在代数性质

这些矩阵不仅是离散化过程的产物，其代数性质也深刻反映了它们所代表的物理算子的特性 [@problem_id:3398519]。

**质量矩阵 $M$** 的性质非常优良。首先，由于标量函数乘法的交换律（$\phi_i \phi_j = \phi_j \phi_i$），其定义显然是对称的，即 $M_{ij} = M_{ji}$ 或 $M = M^T$。其次，对于任意非[零向量](@entry_id:156189) $\boldsymbol{v}$，我们可以构建函数 $u_h = \sum_j v_j \phi_j$。由于[基函数](@entry_id:170178)是[线性无关](@entry_id:148207)的，$u_h$ 必为非零函数。此时，二次型 $\boldsymbol{v}^T M \boldsymbol{v}$ 等于：
$$
\boldsymbol{v}^T M \boldsymbol{v} = \sum_{i,j} v_i M_{ij} v_j = \int_K \left( \sum_i v_i \phi_i \right) \left( \sum_j v_j \phi_j \right) \, dx = \int_K (u_h)^2 \, dx = \|u_h\|_{L^2(K)}^2 > 0
$$
这意味着[质量矩阵](@entry_id:177093)是**[对称正定](@entry_id:145886) (Symmetric Positive Definite, SPD)** 的。这一性质保证了与质量矩阵相关的线性系统的良定性。

**刚度矩阵 $K$** 同样具有对称性，因为梯度[点积](@entry_id:149019)满足交换律（$\nabla\phi_i \cdot \nabla\phi_j = \nabla\phi_j \cdot \nabla\phi_i$）。然而，在正定性方面有所不同。其二次型为：
$$
\boldsymbol{v}^T K \boldsymbol{v} = \int_K |\nabla u_h|^2 \, dx = \|\nabla u_h\|_{L^2(K)}^2 \ge 0
$$
该值总是非负的，因此[刚度矩阵](@entry_id:178659)是**对称半正定 (Symmetric Positive Semidefinite)** 的。它不是严格正定的，因为当 $u_h$ 为一个非零[常数函数](@entry_id:152060)时，其梯度为零，导致二次型为零。因此，刚度[矩阵的零空间](@entry_id:152429)（nullspace）包含了所有可以由[基函数](@entry_id:170178)表示的常数函数。这与物理直觉相符：对于一个纯[扩散](@entry_id:141445)问题，若没有边界热流，整个物体的温度可以整体升高或降低（即加上一个常数）而不改变其内部的温度梯度。

**[对流矩阵](@entry_id:747848) $C$** 的性质则更为复杂。它通常是**非对称的**。为了理解其非对称性的来源，我们考察其对称部分，即 $C_{ij} + C_{ji}$：
$$
C_{ij} + C_{ji} = \int_K \left( \phi_i (\boldsymbol{a} \cdot \nabla \phi_j) + \phi_j (\boldsymbol{a} \cdot \nabla \phi_i) \right) dx
$$
对于常数速度场 $\boldsymbol{a}$，被积函数可以写作 $\nabla \cdot (\phi_i \phi_j \boldsymbol{a})$。利用散度定理（或[分部积分](@entry_id:136350)），该[体积分](@entry_id:171119)可以转化为一个边积分：
$$
C_{ij} + C_{ji} = \int_{\partial K} (\boldsymbol{a} \cdot \boldsymbol{n}) \phi_i \phi_j \, ds
$$
其中 $\boldsymbol{n}$ 是单元边界 $\partial K$ 上的单位外法向量。这个边界项通常不为零，因此 $C$ 不是对称的，也不是斜对称的。它的非对称性是平流输运这一物理过程（由一阶空间导数描述）非自伴（non-self-adjoint）特性的直接体现。仅在特殊情况下，如[速度场](@entry_id:271461) $\boldsymbol{a}=\boldsymbol{0}$ 或所有[基函数](@entry_id:170178)在边界上的值为零时，该边界项消失，此时[对流矩阵](@entry_id:747848)才变为**斜对称 (skew-symmetric)**，即 $C = -C^T$ [@problem_id:3398519]。对于一维情形，$K=[x_L, x_R]$，这个边界积分简化为在两个端点的取值之差：$a(\phi_i(x_R)\phi_j(x_R) - \phi_i(x_L)\phi_j(x_L))$。

### [PDE离散化](@entry_id:175821)中的矩阵角色

这些抽象的矩阵定义如何与具体的PDE求解联系起来？答案在于伽辽金方法。通过一个典型的[对流扩散方程](@entry_id:152018)，我们可以清晰地看到这些矩阵是如何从[弱形式](@entry_id:142897)中自然产生的。

考虑一维[对流扩散方程](@entry_id:152018) [@problem_id:3398524]：
$$
\frac{\partial u}{\partial t} + a \frac{\partial u}{\partial x} - \nu \frac{\partial^2 u}{\partial x^2} = f(x,t)
$$
伽辽金方法的第一步是构建[弱形式](@entry_id:142897)：将方程乘以一个检验函数 (test function) $v(x)$，然后在求解域上（例如，一个单元 $[-1,1]$）积分：
$$
\int_{-1}^{1} \frac{\partial u}{\partial t} v \, dx + \int_{-1}^{1} a \frac{\partial u}{\partial x} v \, dx - \int_{-1}^{1} \nu \frac{\partial^2 u}{\partial x^2} v \, dx = \int_{-1}^{1} f v \, dx
$$
为了处理[二阶导数](@entry_id:144508)项并降低对解的光滑性要求，我们对[扩散](@entry_id:141445)项进行[分部积分](@entry_id:136350)：
$$
- \int_{-1}^{1} \nu \frac{\partial^2 u}{\partial x^2} v \, dx = \nu \int_{-1}^{1} \frac{\partial u}{\partial x} \frac{\partial v}{\partial x} \, dx - \left[ \nu \frac{\partial u}{\partial x} v \right]_{-1}^{1}
$$
假设边界项（方括号中的项）可以得到适当处理（例如，通过边界条件或在[DG方法](@entry_id:748369)中的数值通量），弱形式变为：
$$
\int_{-1}^{1} \frac{\partial u}{\partial t} v \, dx + a \int_{-1}^{1} \frac{\partial u}{\partial x} v \, dx + \nu \int_{-1}^{1} \frac{\partial u}{\partial x} \frac{\partial v}{\partial x} \, dx = \int_{-1}^{1} f v \, dx
$$
第二步是引入[基函数](@entry_id:170178)展开。我们将待求的数值解 $u(x,t)$ 表示为一组含时系数 $u_j(t)$ 与空间[基函数](@entry_id:170178) $\phi_j(x)$ 的[线性组合](@entry_id:154743)：$u(x,t) = \sum_j u_j(t) \phi_j(x)$。同时，我们选择[基函数](@entry_id:170178)本身作为[检验函数](@entry_id:166589)，即 $v(x) = \phi_i(x)$。将这些代入[弱形式](@entry_id:142897)，得到一个关于系数 $u_j$ 的[常微分方程组](@entry_id:266774) (ODE)：
$$
\sum_j \left( \int_{-1}^{1} \phi_i \phi_j \, dx \right) \frac{d u_j}{dt} + \sum_j \left( a \int_{-1}^{1} \phi_i \frac{d \phi_j}{dx} \, dx \right) u_j + \sum_j \left( \nu \int_{-1}^{1} \frac{d \phi_i}{dx} \frac{d \phi_j}{dx} \, dx \right) u_j = \int_{-1}^{1} f \phi_i \, dx
$$
通过识别各项的积分形式，我们发现这正是一个[矩阵方程](@entry_id:203695)：
$$
M \frac{d\boldsymbol{u}}{dt} + (aC + \nu K) \boldsymbol{u} = \boldsymbol{f}
$$
其中 $\boldsymbol{u}(t)$ 是包含系数 $u_j(t)$ 的向量，而矩阵 $M, C, K$ 的元素恰好是我们之前定义的质量、[对流](@entry_id:141806)和刚度矩阵。例如，若使用[勒让德多项式](@entry_id:141510) $\phi_0=1, \phi_1=x, \phi_2=\frac{3x^2-1}{2}$ 作为[基函数](@entry_id:170178)，我们可以直接计算出矩阵 $(aC+\nu K)$ 的任意元素。例如，$(aC+\nu K)_{12}$ 的计算涉及 $\phi_1, \phi_2$ 及其导数的积分，最终结果为 $2a$ [@problem_id:3398524]。这个过程清晰地揭示了：
*   **质量矩阵 $M$** 乘以时间导数项 $\dot{\boldsymbol{u}}$，体现了系统的“惯性”。
*   **[刚度矩阵](@entry_id:178659) $K$** 来自于二阶[扩散算子](@entry_id:136699)，描述了物理量的[扩散](@entry_id:141445)或平滑效应。
*   **[对流矩阵](@entry_id:747848) $C$** 来自于一阶[对流](@entry_id:141806)算子，描述了物理量的输运。

### 参考单元与[坐标变换](@entry_id:172727)

在实际计算中，直接在各种形状和大小的物理单元上定义[基函数](@entry_id:170178)和进行积分是非常繁琐的。因此，一个[标准化](@entry_id:637219)的做法是引入**[参考单元](@entry_id:168425) (reference element)** $\hat{K}$（例如，一维的 $[-1,1]$ 或二维的 $[-1,1]^2$），所有的计算都在这个统一的单元上进行。然后，通过一个[坐标映射](@entry_id:747874) $F: \hat{K} \to K$，将结果变换到物理单元 $K$ 上。

这个过程对单元矩阵有直接影响 [@problem_id:3398540]。设[仿射映射](@entry_id:746332)为 $x = F(\xi) = J\xi + x_0$，其中 $J$ 是常数雅可比矩阵。根据多元微[积分的变量替换](@entry_id:178219)法则，我们有：
*   体积元变换：$dx = \det(J) d\xi$
*   梯度变换：$\nabla_x = J^{-T} \nabla_\xi$

将这些变换规则应用于矩阵定义，我们可以推导出物理单元上的矩阵与[参考单元](@entry_id:168425)上的矩阵之间的关系：

*   **[质量矩阵](@entry_id:177093)**：
    $$
    M^K_{ij} = \int_K \phi_i \phi_j \, dx = \int_{\hat{K}} \hat{\phi}_i \hat{\phi}_j (\det(J) \, d\xi) = \det(J) M^{\hat{K}}_{ij}
    $$
    质量矩阵与单元的“体积”成正比，这符合物理直觉。

*   **[刚度矩阵](@entry_id:178659)**：
    $$
    K^K_{ij} = \int_K (\nabla_x \phi_i) \cdot (\nabla_x \phi_j) \, dx = \int_{\hat{K}} (J^{-T} \nabla_\xi \hat{\phi}_i) \cdot (J^{-T} \nabla_\xi \hat{\phi}_j) (\det(J) \, d\xi)
    $$
    这可以写作 $K^K_{ij} = \det(J) \int_{\hat{K}} (\nabla_\xi \hat{\phi}_i)^T (J^{-1}J^{-T}) (\nabla_\xi \hat{\phi}_j) \, d\xi$。矩阵 $G = J^{-1}J^{-T}$ 称为度量张量 (metric tensor)，它描述了坐标变换如何影响长度和角度的度量。这个复杂的表达式表明，刚度矩阵不仅受单元体积的影响，还受到单元形状（拉伸、剪切）的强烈影响。

*   **[对流矩阵](@entry_id:747848)**：
    $$
    C^K_{ij} = \int_K \phi_i (\boldsymbol{a} \cdot \nabla_x \phi_j) \, dx = \det(J) \int_{\hat{K}} \hat{\phi}_i (\hat{\boldsymbol{a}} \cdot \nabla_\xi \hat{\phi}_j) \, d\xi
    $$
    其中，[参考单元](@entry_id:168425)上的等效速度场为 $\hat{\boldsymbol{a}} = J^{-1}\boldsymbol{a}$。

以一维[仿射变换](@entry_id:144885) $x = a\xi + b$ ($a>0$) 为例，[雅可比](@entry_id:264467)为 $J=a$。变换关系急剧简化：$M^K = a M^{\hat{K}}$，而 $K^K = a^{-1} K^{\hat{K}}$。这意味着，当单元尺寸 $a$ 变大时，质量矩阵的元素变大，而[刚度矩阵](@entry_id:178659)的元素变小。刚度与质量之比的缩放因子为 $a^{-2}$ [@problem_id:3398540]，这个比例关系在分析[数值方法的稳定性](@entry_id:165924)和收敛性时至关重要。

### 全局矩阵的组装与结构

到目前为止，我们只讨论了单个单元上的矩阵。一个完整的计算域 $\Omega$ 通常被剖分成许多单元。全局（global）矩阵是通过将所有局部单元矩阵“组装”起来形成的。组装的方式以及最终全局矩阵的结构，极大地依赖于所采用的数值方法，特别是连续伽辽金（CG）方法和间断伽辽金（DG）方法之间的区别。

#### 连续伽辽金 (CG) 方法

在CG方法（如标准[有限元法](@entry_id:749389)或[谱元法](@entry_id:755171)）中，要求解在单元边界上是连续的（$C^0$ 连续）。这是通过让相邻单元共享边界上的节点（自由度）来实现的。在组装过程中，如果一个全局自由度 $i$ 被多个单元共享，那么全局矩阵的第 $i$ 行（或列）的对应元素，就是所有包含该自由度的局部单元矩阵贡献的总和（这一过程常被称为“直接刚度求和”）。

这种组装方式导致全局矩阵是**稀疏的**。矩阵的非零元素 $A_{ij}$ 仅当自由度 $i$ 和 $j$ 属于同一个单元时才可能出现。因此，矩阵的稀疏模式直接反映了网格的拓扑连接关系 [@problem_id:3398549]。

#### 间断伽辽金 (DG) 方法

与CG方法形成鲜明对比的是，[DG方法](@entry_id:748369)允许解在单元边界上存在间断。每个[基函数](@entry_id:170178)都严格地只定义在一个单元内部，其支集（support）不跨越单元边界。这意味着，在[DG方法](@entry_id:748369)中，不同单元的自由度是完全独立的。

这一特性对全局矩阵的结构有决定性影响 [@problem_id:3398550]：

*   **全局质量矩阵**：由于[质量矩阵](@entry_id:177093)的定义 $M_{ij} = \int_\Omega \phi_i \phi_j \, dx$ 只涉及单元内部的积分，而不同单元的[基函数](@entry_id:170178) $\phi_i$ 和 $\phi_j$ 的支集不重叠，因此它们的乘积积分为零。结果是，全局[质量矩阵](@entry_id:177093)是**块对角 (block-diagonal)** 的。每个对角块就是对应单元的局部[质量矩阵](@entry_id:177093)。这是一个至关重要的性质。

*   **全局刚度/[对流矩阵](@entry_id:747848)**：在DG方法中，单元间的耦合不是通过共享自由度，而是通过在单元界面上定义的**数值通量 (numerical flux)** 来实现的。这些通量项将一个单元的解与它紧邻的邻居联系起来。因此，对于一维问题，完整的空间算子（例如，刚度加[对流](@entry_id:141806)）的全局矩阵呈现出**块三对角 (block-tridiagonal)** 结构。每个自由度只与其所在单元以及直接相邻单元的自由度耦合。对于按单元顺序[排列](@entry_id:136432)自由度的方式，一维DG算子的标量半带宽（half-bandwidth）可以精确计算为 $b = 2(p+1) - 1$，其中 $p$ 是多项式阶数 [@problem_id:3398550]。

### [质量矩阵](@entry_id:177093)：集总及其影响

在[DG方法](@entry_id:748369)和某些[谱元法](@entry_id:755171)中，块对角或对角的质量矩阵为[显式时间推进](@entry_id:749180)格式带来了巨大的计算优势。一个非对角的[质量矩阵](@entry_id:177093) $M$ 在求解 $M\dot{\boldsymbol{u}} = \boldsymbol{R}(\boldsymbol{u})$ 时需要进行矩阵求逆，这是一个计算成本高昂的操作。如果 $M$ 是对角的，其[逆矩阵](@entry_id:140380)的计算就变得微不足道（只需对对角元素取倒数）。

一个被称为**质量集总 (mass lumping)** 的技术，可以在使用[节点基](@entry_id:752522)（nodal basis）时，系统地得到一个对角的质量矩阵。其关键在于积分的[数值近似](@entry_id:161970) [@problem_id:3398532] [@problem_id:3398542]。

具体而言，如果在单元上使用与[拉格朗日插值](@entry_id:167052)节点（例如，[Gauss-Lobatto-Legendre](@entry_id:749736), GLL节点）相对应的[基函数](@entry_id:170178) $\{\ell_i(x)\}$，并采用以这些节点为积分点的[求积法则](@entry_id:753909)来计算[质量矩阵](@entry_id:177093)的积分，即：
$$
M_{ij} = \int_K \ell_i \ell_j \, dx \approx \sum_k w_k \ell_i(x_k) \ell_j(x_k)
$$
其中 $\{x_k\}$ 和 $\{w_k\}$ 是求积节点和权重。由于[拉格朗日基](@entry_id:751105)函数具有克罗内克-德尔[塔性质](@entry_id:273153)，即 $\ell_i(x_k) = \delta_{ik}$，上述求和会因为 $\delta_{ik}\delta_{jk}$ 的存在而急剧简化。当 $i \neq j$ 时，求和的每一项都为零；当 $i = j$ 时，只有 $k=i$ 的一项非零。这导致近似后的[质量矩阵](@entry_id:177093) $M^Q$ 是一个[对角矩阵](@entry_id:637782)：
$$
M^Q_{ij} = w_i \delta_{ij}
$$
这个[对角化](@entry_id:147016)是[节点基](@entry_id:752522)与求积点“配置”在一起的代数结果，与求积法则的精度无关。

这种“不精确”的积分方法不仅方便，而且具有深刻的理论支撑。对于线性[对流](@entry_id:141806)问题，使用这种[对角质量矩阵](@entry_id:173002) $M_d$ 的[DG格式](@entry_id:178043)，不仅可以推导出简洁的强形式节点更新公式 [@problem_id:3398542]，而且被证明能够**保持离散守恒性**，并且对于上风（upwind）通量是**能量稳定**的 [@problem_id:3398526]。这些优良的性质使得质量集总成为显式DG方法中一个几乎[标准化](@entry_id:637219)的操作。

### 谱特性与系统刚度

矩阵的[特征值](@entry_id:154894)[谱分布](@entry_id:158779)决定了其所代表的离散[算子的核](@entry_id:272757)心性质，并直接影响到数值求解的效率，特别是对于[时间演化](@entry_id:153943)问题。对于一个由刚度矩阵 $K$ 和[质量矩阵](@entry_id:177093) $M$ 构成的系统，[广义特征值问题](@entry_id:151614) $K\boldsymbol{c} = \lambda M\boldsymbol{c}$ 的解 $\lambda$ 揭示了系统的模态和相应的时间尺度。算子 $-M^{-1}K$ 的[特征值](@entry_id:154894)谱尤其重要。

以一个一维单元上的[扩散](@entry_id:141445)问题为例，可以分析离散算子[特征值](@entry_id:154894)的标度律 (scaling law) [@problem_id:3398556]。对于一个长度为 $h$ 的单元，使用 $p$ 阶多项式，可以证明 $-M^{-1}K$ 的[最大模](@entry_id:195246)[特征值](@entry_id:154894) $|\lambda|_{\max}$ 的行为近似为：
$$
|\lambda|_{\max} \propto \frac{p^2(p+1)^2}{h^2} \quad \text{(对于标准拉普拉斯算子)}
$$
或
$$
|\lambda|_{\max} \propto \frac{p(p+1)}{h^2} \quad \text{(对于特定的加权拉普拉斯算子)}
$$
在[显式时间积分](@entry_id:165797)格式（如向前[欧拉法](@entry_id:749108)）中，为了保持数值稳定，时间步长 $\Delta t$ 必须小于某个由 $|\lambda|_{\max}$ 决定的阈值，即 $\Delta t \lesssim 1/|\lambda|_{\max}$。这意味着：
$$
\Delta t \lesssim \mathcal{O}\left(\frac{h^2}{p^4}\right) \quad \text{或} \quad \Delta t \lesssim \mathcal{O}\left(\frac{h^2}{p^2}\right)
$$
这个关系定量地描述了谱方法和DG方法中的**刚度 (stiffness)** 问题：随着多项式阶数 $p$ 的增加（$p$-refinement）或网格尺寸 $h$ 的减小（$h$-refinement），系统变得越来越“刚”，要求的时间步长急剧减小，从而增加了计算成本。

### [DG方法](@entry_id:748369)中[刚度矩阵](@entry_id:178659)的推广

最后，值得注意的是，在[DG方法](@entry_id:748369)中处理[扩散](@entry_id:141445)项时，仅仅使用我们最初定义的刚度矩阵 $K$ 是不够的。由于解的间断性，需要引入额外的项来确保格式的稳定性和一致性。

以**[对称内部罚](@entry_id:755719)函数伽辽金 (Symmetric Interior Penalty Galerkin, SIPG)** 方法为例 [@problem_id:3398562]，其用于离散 $-\nu \Delta u$ 的[双线性形式](@entry_id:746794) $a_h(u,v)$ 由三部分构成：
1.  **[体积分](@entry_id:171119)项**：这正是所有单元上标准[刚度矩阵](@entry_id:178659)贡献的总和 $\sum_K \int_K \nu \nabla u \cdot \nabla v \, dx$。
2.  **一致性项**：这些是跨单元界面的积分项，用于将解的值和梯度的平均值与跳跃值耦合起来，以确保在解光滑时格式能收敛到正确的[弱形式](@entry_id:142897)。
3.  **[罚函数](@entry_id:638029)项**：这是一个惩罚解在界面上跳跃的项，形式为 $\sum_F \sigma_F [u][v]$。罚参数 $\sigma_F$ 的大小至关重要，它必须足够大以保证格式的强制性（coercivity）和稳定性。通常其大小与 $\nu p^2/h$ 成正比。

因此，在DG的语境下，“刚度算子”是一个比基本刚度矩阵 $K$ 更复杂的复合算子，它包含了来自单元内部和单元界面的多重贡献。理解这一点对于正确实现和分析[DG方法](@entry_id:748369)至关重要。