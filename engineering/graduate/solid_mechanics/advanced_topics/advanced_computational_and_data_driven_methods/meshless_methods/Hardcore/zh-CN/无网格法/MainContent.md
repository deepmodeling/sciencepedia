## 引言
在计算力学领域，有限元方法(FEM)长期以来占据主导地位。然而，当面对涉及剧烈几何变化、移动边界或自发不连续性（如裂纹扩展）的问题时，其对高质量网格的依赖往往成为一个巨大的瓶颈，需要复杂的网格重划分技术。为了克服这些局限，一系列被称为“无网格方法”的数值技术应运而生，它们将离散化的核心从“单元”转向了灵活的“节点”，为模拟此前难以处理的物理现象开辟了新途径。

本文旨在系统地介绍无网格方法的核心思想与前沿应用。我们将首先解决其根本的知识体系：这些方法是如何在没有网格连接性的情况下构建出精确且收敛的数值近似的？

为回答这一问题，文章将分为三个章节展开。在“原理与机制”中，我们将深入剖析移动最小二乘(MLS)近似的数学构造、性质及其在无单元伽辽金(EFG)法中的应用，并探讨数值积分、边界条件施加等关键实现挑战。随后，在“应用与跨学科交叉”中，我们将展示无网格方法如何在断裂力学、大变形分析、多物理场耦合以及与机器学习的交叉中展现其独特优势。最后，“动手实践”部分将提供一系列编程练习，帮助您将理论知识转化为实际的计算能力。

现在，让我们从构建无网格方法大厦的基石——其基本原理与核心机制——开始我们的探索之旅。

## 原理与机制

本章旨在深入阐述无网格方法的核心原理与基本机制。在前一章介绍其背景与动机的基础上，我们将系统地剖析这些方法如何摆脱传统网格的束缚来构建数值近似，并探讨由此引发的一系列独特的理论和实践问题。我们将从近似函数的构建出发，逐步推导至离散控制方程的形成，最后讨论其稳定性与精度的关键影响因素。

### 无网格近似的核心思想

与依赖于预定义、拓扑连接的单元网格的**有限元方法 (FEM)** 不同，**无网格方法 (Meshless Methods)** 的基石在于仅通过一组离散节点（或称为“节点云”）来构建整个问题域的近似函数。这种范式的转变是深刻的，它将数值离散化的核心从“单元划分”转移到了“节点影响”。

在无网格方法中，每个节点 $\boldsymbol{x}_I$ 都关联着一个**影响域 (influence domain)**，这通常是一个以该节点为中心的几何区域（如圆形或矩形）。某点 $\boldsymbol{x}$ 处的场变量值，是由所有影响域覆盖该点的节点上的信息加权平均得到的。因此，节点间的**连接性 (connectivity)** 不再由共享单元边界的显式拓扑关系定义，而是由影响域相互重叠的隐式几何关系决定。如果节点 $I$ 和节点 $J$ 的影响域存在重叠，那么在最终的离散系统中，它们之间就可能存在耦合关系。这种灵活的、基于影响域的近似构造方式，正是无网格方法能够便捷处理大变形、裂纹扩展等涉及剧烈拓扑变化的物理问题的根源 [@problem_id:2661988]。

### 移动最小二乘 (MLS) 近似

在众多无网格近似方案中，**移动最小二乘法 (Moving Least Squares, MLS)** 是应用最广泛、理论最成熟的技术之一，尤其在**无单元伽辽金法 (Element-Free Galerkin, EFG)** 中扮演着核心角色。

#### 局部加权最小二乘拟合

MLS 的核心思想是：在求解域内任意一点 $\boldsymbol{x}$ 处，其场函数值 $u(\boldsymbol{x})$ 的近似值 $u^h(\boldsymbol{x})$ 不是直接通过插值得到，而是通过一个局部的、加权的最小二乘拟合来构造。具体而言，我们首先假设在点 $\boldsymbol{x}$ 的邻域内，近似函数 $u^h$ 可以表示为一个低阶多项式，其形式为 $u^h(\boldsymbol{y}; \boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{y})\boldsymbol{a}(\boldsymbol{x})$。其中，$\boldsymbol{p}(\boldsymbol{y})$ 是一个包含 $m$ 个多项式基函数的向量（例如，在二维线性基情况下，$\boldsymbol{p}^T(\boldsymbol{y}) = \begin{pmatrix} 1  y_1  y_2 \end{pmatrix}$），而 $\boldsymbol{a}(\boldsymbol{x})$ 是依赖于评估点 $\boldsymbol{x}$ 的待定系数向量 [@problem_id:2661992]。

这些系数 $\boldsymbol{a}(\boldsymbol{x})$ 并非全局常数，而是通过最小化一个加权残差泛函 $J(\boldsymbol{x})$ 来确定的。该泛函量化了局部多项式在邻近节点 $\boldsymbol{x}_I$ 处的值与这些节点对应的虚拟参数 $d_I$ 之间的加权平方误差之和：
$$
J(\boldsymbol{x}) = \sum_{I=1}^{N} w_I(\boldsymbol{x}) [u^h(\boldsymbol{x}_I; \boldsymbol{x}) - d_I]^2 = \sum_{I=1}^{N} w_I(\boldsymbol{x}) [\boldsymbol{p}^T(\boldsymbol{x}_I)\boldsymbol{a}(\boldsymbol{x}) - d_I]^2
$$
其中，$w_I(\boldsymbol{x})$ 是与节点 $\boldsymbol{x}_I$ 关联的**权函数 (weight function)**，它在以 $\boldsymbol{x}_I$ 为中心的紧支集外为零，并随着点 $\boldsymbol{x}$ 远离节点 $\boldsymbol{x}_I$ 而单调递减。

#### MLS 形函数的推导

为了使 $J(\boldsymbol{x})$ 最小，其关于系数向量 $\boldsymbol{a}(\boldsymbol{x})$ 的梯度必须为零，即 $\frac{\partial J}{\partial \boldsymbol{a}} = \boldsymbol{0}$。这导出了如下的**法方程 (normal equations)**：
$$
\boldsymbol{A}(\boldsymbol{x}) \boldsymbol{a}(\boldsymbol{x}) = \boldsymbol{B}(\boldsymbol{x}) \boldsymbol{d}
$$
其中，$\boldsymbol{A}(\boldsymbol{x})$ 是所谓的**矩量矩阵 (moment matrix)**，定义为：
$$
\boldsymbol{A}(\boldsymbol{x}) = \sum_{I=1}^{N} w_I(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I) \boldsymbol{p}^T(\boldsymbol{x}_I)
$$
矩阵 $\boldsymbol{B}(\boldsymbol{x})$ 和向量 $\boldsymbol{d}$ 的形式分别为 $\boldsymbol{B}(\boldsymbol{x}) = \left[ w_1(\boldsymbol{x})\boldsymbol{p}(\boldsymbol{x}_1), w_2(\boldsymbol{x})\boldsymbol{p}(\boldsymbol{x}_2), \dots \right]$ 和 $\boldsymbol{d} = \left[ d_1, d_2, \dots \right]^T$。

只要矩量矩阵 $\boldsymbol{A}(\boldsymbol{x})$ 可逆，我们就可以解得系数向量 $\boldsymbol{a}(\boldsymbol{x}) = \boldsymbol{A}^{-1}(\boldsymbol{x}) \boldsymbol{B}(\boldsymbol{x}) \boldsymbol{d}$。将此解代入点 $\boldsymbol{x}$ 处的近似表达式 $u^h(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x})\boldsymbol{a}(\boldsymbol{x})$，我们得到：
$$
u^h(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) \boldsymbol{A}^{-1}(\boldsymbol{x}) \sum_{I=1}^{N} w_I(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I) d_I
$$
通过重新整理，我们可以将近似函数写成我们熟悉的伽辽金形式 $u^h(\boldsymbol{x}) = \sum_{I=1}^{N} N_I(\boldsymbol{x}) d_I$，其中 $N_I(\boldsymbol{x})$ 就是 MLS **形函数 (shape function)**：
$$
N_I(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) \boldsymbol{A}^{-1}(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I) w_I(\boldsymbol{x})
$$
这个表达式是 MLS 近似的核心。它明确显示，形函数 $N_I(\boldsymbol{x})$ 是一个由多项式基、权函数以及所有邻近节点几何信息（通过矩量矩阵 $\boldsymbol{A}(\boldsymbol{x})$ 体现）共同决定的复杂有理函数（多项式的比值）[@problem_id:2661992]。

#### 多项式完备性与一致性

一个数值方法若要收敛，其近似函数必须能够精确地再现至少常数场。更进一步，为了达到最优的收敛率，它应该能够精确再现更高阶的多项式场。这个性质被称为**多项式完备性 (polynomial completeness)** 或**多项式再生性 (polynomial reproduction)**，是保证方法**一致性 (consistency)** 的关键。

MLS 近似具有内在的 $m$ 阶完备性，其充要条件是：
1.  近似中采用的多项式基 $\boldsymbol{p}(\boldsymbol{x})$ 必须包含所有直到 $m$ 次的单项式。
2.  在感兴趣的区域内，矩量矩阵 $\boldsymbol{A}(\boldsymbol{x})$ 必须是可逆的。

$\boldsymbol{A}(\boldsymbol{x})$ 的可逆性取决于权函数 $w_I(\boldsymbol{x})$ 在点 $\boldsymbol{x}$ 处的支持域内，是否有足够数量的节点，并且这些节点的几何排布相对于多项式基 $\boldsymbol{p}(\boldsymbol{x})$ 是非退化的。具体来说，对于一个包含 $n_p$ 个基函数的多项式基，支持域内至少需要有 $n_p$ 个节点，并且这些节点不能位于某个 $m$ 次多项式的零集上（例如，对于线性基，节点不能共线）[@problem_id:2661998]。

#### MLS 的非插值特性

与有限元中拉格朗日形函数的一个关键区别是，标准 MLS 形函数不具备**克罗内克 delta (Kronecker delta)** 性质，即 $N_I(\boldsymbol{x}_J) \neq \delta_{IJ}$。这意味着在节点 $\boldsymbol{x}_J$ 处的近似值 $u^h(\boldsymbol{x}_J) = \sum_{I=1}^{N} N_I(\boldsymbol{x}_J) d_I$ 通常不等于该节点的参数 $d_J$。

这个**非插值 (non-interpolatory)** 的特性是 MLS 构造方法的直接产物。MLS 的目标是找到一个“最佳拟合”的多项式，而不是一个穿过所有数据点的多项式。从理论上讲，若要强行使 $N_I(\boldsymbol{x}_J) = \delta_{IJ}$，则要求每个节点的权函数在其自身位置处非零，而在所有其他节点位置处为零。这样的权函数会使得矩量矩阵 $\boldsymbol{A}(\boldsymbol{x})$ 对于任何高于零阶的多项式基都是奇异的，从而彻底破坏了多项式完备性这一关键性质。因此，非插值性是标准 MLS 为获得良好光滑性和高阶一致性所付出的“代价” [@problem_id:2662039]。这个特性也直接导致了在施加本质边界条件时的困难，我们将在稍后讨论。

### 近似方案的实际考量

MLS 近似的性能和稳定性在很大程度上取决于两个关键的人为选择：权函数的形式和其支持域的大小。

#### 权函数

权函数 $w(q)$（其中 $q$ 是点到节点中心的归一化距离）的选择对于 MLS 近似的质量至关重要。一个好的权函数通常需要满足以下条件：
*   **紧支性 (Compact Support)**：权函数仅在一个有限的区域内非零，以保证近似的局部性并产生稀疏的系统矩阵。
*   **非负性与单位中心值**：$w(q) \ge 0$ 且 $w(0) = 1$。
*   **单调递减性**：随着距离增加，权重减小。
*   **足够的光滑性**：权函数的光滑度决定了最终 MLS 形函数的光滑度。

常用的权函数包括具有 $C^1$ 连续性的**三次样条 (cubic spline)** 函数：
$$
w(q) = \begin{cases} 1 - 3q^2 + 2q^3  0 \le q \le 1 \\ 0  q > 1 \end{cases}
$$
以及具有 $C^2$ 连续性的**四次样条 (quartic spline)** 函数：
$$
w(q) = \begin{cases} 1 - 6q^2 + 8q^3 - 3q^4  0 \le q \le 1 \\ 0  q > 1 \end{cases}
$$
此外，**截断高斯 (truncated Gaussian)** 函数也常被使用 [@problem_id:2661979]。

#### 支持域半径：一个关键参数

权函数的支持域半径 $r_s$ 通常与局部节点间距 $h$ 成比例，即 $r_s = \beta h$，其中 $\beta$ 是一个无量纲的缩放因子。参数 $\beta$ 的选择是一个涉及精度、稳定性和计算成本的微妙权衡 [@problem_id:2661990]：

*   **过小的 $\beta$**：如果支持域太小，其内部可能不包含足够数量的节点来保证矩量矩阵 $\boldsymbol{A}(\boldsymbol{x})$ 的非奇异性。这会导致多项式完备性的丧失，甚至在计算中出现除零错误。所需的最小节点数随着多项式基的阶次 $m$ 增加而增加，因此更高阶的近似需要更大的 $\beta$。

*   **过大的 $\beta$**：增加 $\beta$ 会引入更多节点参与局部拟合，通常能改善 $\boldsymbol{A}(\boldsymbol{x})$ 的条件数，使局部近似更稳定。然而，这会带来两个负面影响。首先，它增加了最终全局刚度矩阵的带宽（非零元数量），因为形函数的支持域变大，重叠也随之增多，计算成本显著上升（非零元数量大致与 $\beta^2$ 成正比）。其次，当 $\beta$ 过大时，不同节点的形函数会变得越来越相似，导致全局形函数基的近似线性相关，反而使全局刚度矩阵的条件数恶化，导致数值不稳定。

因此，在实践中，必须为给定的多项式基阶次选择一个“恰到好处”的 $\beta$ 值，以在保证局部近似稳定性和一致性的同时，维持全局系统的良好条件数和可接受的计算成本。

### 从近似到离散：无单元伽辽金 (EFG) 法

构建了 MLS 近似函数后，下一步是利用伽辽金程序将其应用于求解偏微分方程，这就构成了**无单元伽辽金 (EFG) 法**。

#### 组装离散系统

我们以小应变线弹性问题的虚功原理（弱形式）为例：
$$
\int_{\Omega} \boldsymbol{\sigma}(\boldsymbol{u}):\boldsymbol{\varepsilon}(\boldsymbol{v}) d\Omega = \int_{\Omega} \boldsymbol{b}\cdot \boldsymbol{v} d\Omega + \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \boldsymbol{v} d\Gamma
$$
在 EFG 中，我们将试探函数 $\boldsymbol{u}$ 和检验函数 $\boldsymbol{v}$ 都用 MLS 形函数展开：
$$
\boldsymbol{u}^h(\boldsymbol{x}) = \sum_{I=1}^{N} \boldsymbol{\mathcal{N}}_{I}(\boldsymbol{x}) \boldsymbol{d}_{I}, \quad \boldsymbol{v}^h(\boldsymbol{x}) = \sum_{J=1}^{N} \boldsymbol{\mathcal{N}}_{J}(\boldsymbol{x}) \boldsymbol{\delta d}_{J}
$$
其中 $\boldsymbol{d}_I$ 是节点位移参数向量，$\boldsymbol{\mathcal{N}}_{I}(\boldsymbol{x})$ 是一个 $2 \times 2$ 的矩阵形函数（在二维情况下），通常为 $N_I(\boldsymbol{x}) \boldsymbol{I}$。应变张量的离散形式为 $\boldsymbol{\varepsilon}(\boldsymbol{u}^h) = \sum_I \boldsymbol{\mathcal{B}}_I \boldsymbol{d}_I$，其中**应变-位移矩阵** $\boldsymbol{\mathcal{B}}_I$ 由 MLS 形函数的空间导数构成。例如，在二维平面应变问题的 Voigt 表示中：
$$
\boldsymbol{\mathcal{B}}_{I}(\boldsymbol{x}) = \begin{bmatrix} \partial_{x}N_{I}(\boldsymbol{x})  0 \\ 0  \partial_{y}N_{I}(\boldsymbol{x}) \\ \partial_{y}N_{I}(\boldsymbol{x})  \partial_{x}N_{I}(\boldsymbol{x}) \end{bmatrix}
$$
形函数的导数可以通过对 $N_I(\boldsymbol{x})$ 的表达式进行链式法则求导得到，这是一个繁琐但直接的过程 [@problem_id:2662041]。将离散的场代入弱形式，并利用虚位移 $\boldsymbol{\delta d}_J$ 的任意性，我们最终得到一个标准的线性代数方程组 $\boldsymbol{K}\boldsymbol{d} = \boldsymbol{f}$。其中，全局刚度矩阵 $\boldsymbol{K}$ 的 $(I,J)$ 子块由下式给出：
$$
\boldsymbol{K}_{IJ} = \int_{\Omega} \boldsymbol{\mathcal{B}}_{I}^{T} \boldsymbol{C} \boldsymbol{\mathcal{B}}_{J} d\Omega
$$
这里 $\boldsymbol{C}$ 是材料的弹性矩阵。这个表达式构成了 EFG 离散系统的核心 [@problem_id:2662007]。

#### 数值积分的挑战

EFG 方法面临的一个核心挑战是如何对弱形式中的积分进行数值计算。在有限元中，由于形函数是分片多项式，积分可以在每个单元上使用**高斯求积 (Gaussian quadrature)** 精确（或非常精确地）完成。然而，在 EFG 中，被积函数（如 $\boldsymbol{\mathcal{B}}_{I}^{T} \boldsymbol{C} \boldsymbol{\mathcal{B}}_{J}$）是复杂的有理函数。任何多项式求积法则，如高斯求积，都无法精确地计算其积分。

为了解决这个问题，EFG 通常采用一个独立于节点分布的**背景积分网格 (background integration mesh)**。将求解域划分为简单的积分单元（如三角形或四边形），然后在每个积分单元上应用高斯求积。由于积分是不精确的，这在理论上引入了**一致性误差 (consistency error)**，有时被称为“**变分犯罪 (variational crime)**”，即离散方程所对应的变分原理与原始的变分原理不完全等价。这种积分误差的大小取决于背景网格的密度和求积点的数量，并且是 EFG 方法总误差的一个来源 [@problem_id:2661961]。

#### 本质边界条件的挑战

如前所述，MLS 形函数的非插值性使得施加**本质边界条件 (Essential Boundary Conditions, EBCs)**（如狄氏边界条件）成为一个难题。直接在边界节点上强加位移值，即令 $\boldsymbol{d}_I = \boldsymbol{g}(\boldsymbol{x}_I)$，并不能保证近似解在这些点上满足边界条件，即 $\boldsymbol{u}^h(\boldsymbol{x}_I) \neq \boldsymbol{g}(\boldsymbol{x}_I)$。这种不一致的做法会破坏变分原理，导致解的精度严重下降甚至不收敛 [@problem_id:2662039]。

因此，必须采用**弱形式**来施加 EBCs。常用的方法包括：
*   **罚函数法 (Penalty Method)**：通过在弱形式中增加一个罚项 $\int_{\Gamma_u} \alpha (\boldsymbol{u}^h - \boldsymbol{g}) \cdot \boldsymbol{v}^h d\Gamma$ 来近似满足边界条件，其中 $\alpha$ 是一个大的罚参数。这会修正刚度矩阵和力向量 [@problem_id:2662007]。
*   **拉格朗日乘子法 (Lagrange Multiplier Method)**：引入拉格朗日乘子场来精确满足边界约束，但这会增加未知数并产生一个鞍点问题。
*   **Nitsche 法**：一种结合了罚函数和一致性项的方法，能够在不引入额外未知数的情况下稳定地施加边界条件。

### 稳定性与精度考量

无网格方法的稳定性和精度对参数选择和实现细节非常敏感。以下是一些关键的稳定性问题及其诊断方法 [@problem_id:2661967]：

*   **局部秩亏 (Local Rank Deficiency)**：当矩量矩阵 $\boldsymbol{A}(\boldsymbol{x})$ 在某个积分点变得奇异或病态时发生。这通常是由于支持域内节点不足或几何构型退化引起的。实践中，可以通过在积分点处检查 $\boldsymbol{A}(\boldsymbol{x})$ 的秩和条件数来诊断此问题。

*   **零能模式 (Zero-Energy Modes)**：也称为**沙漏模式 (hourglass modes)**，是指离散系统存在非物理的、能量为零的变形模式。这通常由积分不当（如单点求积）引起。诊断方法是计算（约束后）全局刚度矩阵 $\boldsymbol{K}$ 的特征值。如果其零空间（对应于零特征值）的维数超过了物理刚体运动的模态数，则存在零能模式。

*   **边界效应 (Boundary Effects)**：在求解域的边界附近，由于支持域被截断，节点数量减少，容易导致局部秩亏和多项式完备性的丧失。这是标准 MLS 的一个固有缺陷，需要采用特殊技术（如衍射法、特殊边界基函数等）来修正 [@problem_id:2661990]。

*   **动力学问题中的不稳定性**：在显式动力学分析中，空间离散的不稳定性（如由某些参数选择导致的“拉伸不稳定性”）会导致系统总能量无故增长。通过监测一个保守系统在使用保辛时间积分格式下的总能量是否守恒，可以有效地诊断这类问题。

值得强调的是，一些看似直观的“修复”方法往往是错误的。例如，通过**节点积分 (nodal integration)**（即将积分简化为节点值的加权和）虽然可以得到对角的质量矩阵，但用于刚度矩阵时会引入严重的零能模式，反而加剧了不稳定性。同样，仅仅通过**CFL (Courant–Friedrichs–Lewy)** 条件来限制时间步长只能保证时间积分的稳定，无法消除空间离散本身固有的不稳定性。