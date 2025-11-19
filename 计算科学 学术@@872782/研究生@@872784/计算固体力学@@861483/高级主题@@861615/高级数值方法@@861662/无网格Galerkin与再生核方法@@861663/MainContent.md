## 引言
在计算科学与工程领域，数值方法的发展不断推动着我们理解和预测复杂物理现象的能力。传统的有限单元法（FEM）作为基石，数十年来一直是结构和连续介质力学分析的黄金标准。然而，FEM的威力根植于其对高质量[计算网格](@entry_id:168560)的依赖，而在处理涉及极[大变形](@entry_id:167243)、裂纹扩展或[移动界面](@entry_id:141467)的问题时，网格的生成与维护往往成为计算流程中最棘手、最耗时的瓶颈。为了突破这一局限，计算力学家们开发了一类被称为“[无网格方法](@entry_id:177458)”的创新技术，其中，[无网格伽辽金法](@entry_id:751897)与[再生核](@entry_id:262515)方法便是其中的杰出代表。

本文旨在系统性地介绍这些前沿的数值方法，填补从理论构建到实际应用的知识鸿沟。我们将探讨这些方法如何摆脱网格的束缚，直接利用一组离散节点来构建精确且光滑的近似解。通过本文的学习，读者将深入理解[无网格方法](@entry_id:177458)背后的数学原理，掌握其在解决高级力学问题时的独特优势，并认识到其在实践中面临的挑战与对策。

文章将分为三个核心部分展开。第一章，“原理与机制”，将深入剖析无网格近似的构造核心——[移动最小二乘法](@entry_id:178698)，阐明保证方法收敛性的关键性质，并详细讨论在伽辽金框架下会遇到的边界条件施加、[数值积分](@entry_id:136578)和线性系统求解等关键问题。第二章，“应用与交叉学科联系”，将视野扩展至实际应用，展示[无网格方法](@entry_id:177458)如何巧妙地处理大变形、断裂力学、结构锁死以及[多物理场耦合](@entry_id:171389)等一系列传统方法难以应对的挑战。最后，“动手实践”部分将提供一系列精心设计的编程练习，引导读者亲手实现并验证[无网格方法](@entry_id:177458)的核心算法，将理论知识转化为实践能力。

## 原理与机制

在[计算固体力学](@entry_id:169583)中，[无网格伽辽金法](@entry_id:751897)与[再生核](@entry_id:262515)方法代表了对传统有限单元法（FEM）的重大[范式](@entry_id:161181)转变。[有限元法](@entry_id:749389)的核心在于将求解域剖分为一个**网格（mesh）**，并在每个单元上构建分片[多项式插值](@entry_id:145762)函数。与此不同，[无网格方法](@entry_id:177458)旨在摆脱对显式、高质量[网格生成](@entry_id:149105)的依赖，直接利用一组离散的**节点（nodes）**来构建近似函数。本章旨在深入探讨这些方法背后的基本原理和核心机制，阐明其从函数构造到[伽辽金离散化](@entry_id:172164)，再到实际应用中关键挑战的完整图景。

### 无网格近似的构建：[移动最小二乘法](@entry_id:178698)

[无网格方法](@entry_id:177458)的核心在于其独特的近似函数（或称形函数）的构建方式。**[移动最小二乘法](@entry_id:178698)（Moving Least Squares, MLS）** 是其中最经典和最基础的一种技术。MLS的本质思想是，在求解域中的任意一点 $\boldsymbol{x}$，其近似值 $u_h(\boldsymbol{x})$ 并非由一个全局函数确定，而是通过一个“移动”的[局部多项式拟合](@entry_id:636664)来得到。

具体而言，对于求解域 $\Omega \subset \mathbb{R}^d$ 中的任意目标点 $\boldsymbol{x}$，我们考虑一个局部多项式[基函数](@entry_id:170178)向量 $\boldsymbol{p}(\boldsymbol{x}) \in \mathbb{R}^m$。例如，在二维空间中进行线性近似，该[基向量](@entry_id:199546)为 $\boldsymbol{p}(\boldsymbol{x}) = \begin{pmatrix} 1  x  y \end{pmatrix}^T$。我们假设在点 $\boldsymbol{x}$ 的局部邻域内，近似解可以表示为 $u_h(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x})\boldsymbol{a}(\boldsymbol{x})$，其中 $\boldsymbol{a}(\boldsymbol{x}) \in \mathbb{R}^m$ 是一个待定的、依赖于点 $\boldsymbol{x}$ 的系数向量。

这个局部系数向量 $\boldsymbol{a}(\boldsymbol{x})$ 的确定，是通过最小化一个加权的离散二乘范数来实现的。该范数衡量了局部多项式在邻近节点 $\boldsymbol{x}_I$ 上的值 $\boldsymbol{p}^T(\boldsymbol{x}_I)\boldsymbol{a}(\boldsymbol{x})$ 与这些节点上的参数值 $u_I$ 之间的加权[误差平方和](@entry_id:149299)。这个过程定义了一个泛函 $J(\boldsymbol{a}; \boldsymbol{x})$ [@problem_id:3581093]：
$$
J(\boldsymbol{a}; \boldsymbol{x}) = \sum_{I=1}^N w_I(\boldsymbol{x}) \left[ \boldsymbol{p}^T(\boldsymbol{x}_I)\boldsymbol{a}(\boldsymbol{x}) - u_I \right]^2
$$
其中，$N$ 是节点总数，$u_I$ 是与节点 $\boldsymbol{x}_I$ 相关联的待求参数（通常是位移），而 $w_I(\boldsymbol{x})$ 是一个**权函数（weight function）**或**[窗函数](@entry_id:139733)（window function）**。该函数衡量了节点 $\boldsymbol{x}_I$ 对目标点 $\boldsymbol{x}$ 的影响程度，通常具有[紧支集](@entry_id:276214)（compact support），即当 $\boldsymbol{x}$ 与 $\boldsymbol{x}_I$ 的距离超出某个[影响域](@entry_id:175298)时，$w_I(\boldsymbol{x})=0$。

为了使 $J$ 最小化，我们令其对 $\boldsymbol{a}(\boldsymbol{x})$ 的偏导数为零，即 $\nabla_{\boldsymbol{a}} J(\boldsymbol{a}; \boldsymbol{x}) = \boldsymbol{0}$。这导出了如下的**法方程（normal equations）**：
$$
\boldsymbol{M}(\boldsymbol{x}) \boldsymbol{a}(\boldsymbol{x}) = \boldsymbol{B}(\boldsymbol{x}) \boldsymbol{u}
$$
或者更具体地写作：
$$
\left( \sum_{I=1}^N w_I(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I) \boldsymbol{p}^T(\boldsymbol{x}_I) \right) \boldsymbol{a}(\boldsymbol{x}) = \sum_{I=1}^N w_I(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I) u_I
$$
这里，$\boldsymbol{M}(\boldsymbol{x}) \in \mathbb{R}^{m \times m}$ 被称为**[矩量](@entry_id:152982)矩阵（moment matrix）**。只要 $\boldsymbol{M}(\boldsymbol{x})$ 是非奇异的，我们就可以解出 $\boldsymbol{a}(\boldsymbol{x})$：
$$
\boldsymbol{a}(\boldsymbol{x}) = \boldsymbol{M}^{-1}(\boldsymbol{x}) \left( \sum_{I=1}^N w_I(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I) u_I \right)
$$
$\boldsymbol{M}(\boldsymbol{x})$ 的[可逆性](@entry_id:143146)是至关重要的，它要求在点 $\boldsymbol{x}$ 的[影响域](@entry_id:175298)内必须有足够多的、呈非退化[几何分布](@entry_id:154371)的节点，以确保[基向量](@entry_id:199546)的加权集合 $\{\boldsymbol{p}(\boldsymbol{x}_I)\}_{I \in \mathcal{N}(\boldsymbol{x})}$ 能够张成整个 $\mathbb{R}^m$ 空间 [@problem_id:3581093]。

将 $\boldsymbol{a}(\boldsymbol{x})$ 的表达式代回到 $u_h(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x})\boldsymbol{a}(\boldsymbol{x})$ 中，并重新整理，我们可以得到一个熟悉的形式：
$$
u_h(\boldsymbol{x}) = \sum_{I=1}^N N_I(\boldsymbol{x}) u_I
$$
其中，$N_I(\boldsymbol{x})$ 就是我们所求的MLS形函数：
$$
N_I(\boldsymbol{x}) = \boldsymbol{p}^T(\boldsymbol{x}) \boldsymbol{M}^{-1}(\boldsymbol{x}) \boldsymbol{p}(\boldsymbol{x}_I) w_I(\boldsymbol{x})
$$
这些形函数是复杂的[有理函数](@entry_id:154279)，它们的性质直接继承自多项式基 $\boldsymbol{p}(\boldsymbol{x})$ 和权函数 $w_I(\boldsymbol{x})$。

#### 权函数的选择与影响

权函数的选择对MLS近似的性质有决定性影响，特别是其光滑性 [@problem_id:3581121]。为了保证矩量矩阵 $\boldsymbol{M}(\boldsymbol{x})$ 的正定性，权函数必须是**非负的**（$w(r) \ge 0$）。为了使最终的[刚度矩阵](@entry_id:178659)稀疏以提高[计算效率](@entry_id:270255)，权函数通常具有**[紧支集](@entry_id:276214)**。

此外，MLS形函数的[光滑性](@entry_id:634843)直接由权函数的[光滑性](@entry_id:634843)决定。如果权函数是 $C^k$ 连续的，那么只要矩量矩阵处处非奇异，所生成的MLS形函数也将是 $C^k$ 连续的。这对求解高阶[偏微分方程](@entry_id:141332)至关重要。例如，在需要 $H^1$ 协调性的标准弹性问题中，形函数至少需要是 $C^0$ 连续的，这意味着权函数也至少需要是 $C^0$ 的。

常见的权函数选择包括：
- **高斯函数**：$w(r) = \exp(-\alpha r^2)$。它无限阶光滑（$C^\infty$），但没有[紧支集](@entry_id:276214)（全局支撑），除非进行人为截断，否则会导致稠密的刚度矩阵。
- **[三次样条](@entry_id:140033)函数**：如 $w(r) = (1-r)^3(1+3r)$ 对于 $r \in [0,1]$。该函数在 $r=1$ 处的前[二阶导数](@entry_id:144508)均为零，因此是 $C^2$ 连续的。
- **四次[样条](@entry_id:143749)函数**：如 $w(r) = (1-r)^4(1+4r)$ 对于 $r \in [0,1]$。该函数在 $r=1$ 处的前三阶导数均为零，因此是 $C^3$ 连续的 [@problem_id:3581121]。

更高的[光滑性](@entry_id:634843)意味着形函数的导数也更平滑，这在计算应力和应变时可能是有利的。

### [再生核](@entry_id:262515)颗粒法（RKPM）

**[再生核](@entry_id:262515)颗粒法（Reproducing Kernel Particle Method, RKPM）** 可以被看作是MLS的一个更形式化和普适化的框架 [@problem_id:3581101]。RKPM从一个**[核函数](@entry_id:145324)（kernel function）**出发，通过一个修正过程来强制其满足[多项式再生](@entry_id:753580)条件。修正后的[核函数](@entry_id:145324)即为最终的形函数。这种方法确保了近似在构造上就满足特定的**再生属性（reproducing properties）**，从而保证了[伽辽金离散化](@entry_id:172164)的一致性。MLS可以被视为RKPM在特定选择下的一个特例。

### 无网格形函数的关键性质

为了在固体力学的伽辽金框架下获得稳定且收敛的解，无网格形函数必须具备一系列关键性质。这些性质确保了近似的[运动学](@entry_id:173318)许可性、一致性和物理保真度 [@problem_id:3581165]。

1.  **单位分解性（Partition of Unity, POU）**：形函数之和必须恒为1，即 $\sum_I N_I(\boldsymbol{x}) = 1$。这是通过在多项式基 $\boldsymbol{p}(\boldsymbol{x})$ 中包含常数项（即0阶完备性）来实现的。物理上，单位分解性确保了近似能够精确表示刚体平移。当施加一个常数[位移场](@entry_id:141476)时，应变和[应变能](@entry_id:162699)必须为零，POU是实现这一点的根本保证。

2.  **[多项式再生](@entry_id:753580)性（Polynomial Reproduction）**：为了保证收敛性，近似必须能够精确地再生更高阶的多项式场。对于二阶弹性问题，至少需要**线性再生性**，即能够精确表示任何仿射场 $\boldsymbol{u}(\boldsymbol{x}) = \boldsymbol{c} + \boldsymbol{A}\boldsymbol{x}$。
    - 当 $\boldsymbol{A}$ 是反对称矩阵时，这代表了**[刚体转动](@entry_id:191086)**。精确再生确保了[刚体转动](@entry_id:191086)不会产生虚假的[应变能](@entry_id:162699)。
    - 当 $\boldsymbol{A}$ 是对称矩阵时，这代表了**常应变状态**。精确再生确保了方法能够无误地捕捉最简单的变形模式。
    满足线性再生性是方法通过**线性片检验（linear patch test）**的充分条件，而通过片检验是保证[收敛的必要条件](@entry_id:157681) [@problem_id:3581118]。

3.  **连续性（Continuity）**：对于基于[虚功原理](@entry_id:138749)的二阶弹性问题，其弱形式要求[位移场](@entry_id:141476)属于索博列夫空间 $H^1(\Omega)$。这意味着[位移场](@entry_id:141476)本身是平方可积的，其[一阶导数](@entry_id:749425)（应变）也是平方可积的。为了保证离散近似解 $u_h$ 属于 $H^1(\Omega)$，一个充分条件是形函数 $N_I(\boldsymbol{x})$ 至少是全局 $C^0$ 连续的。正如前述，这可以通过选择至少 $C^0$ 连续的权函数来实现。

4.  **梯度的有界性（Bounded Gradients）**：为了保证数值解的稳定性和刚度矩阵的良态性，形函数的梯度必须是适当有界的。通常要求，对于节点 $I$，其形函数梯度的范数满足 $\Vert \nabla N_I \Vert_{L^\infty(\omega_I)} \le C/h_I$，其中 $h_I$ 是局部节点间距，$\omega_I$ 是其支集。这个条件防止了在节点[分布](@entry_id:182848)不规则时出现虚假的、非物理的[应变集中](@entry_id:187026)。

### [无网格伽辽金法](@entry_id:751897)

具备了上述性质的形函数后，我们便可以将其应用于标准的伽辽金弱形式中。对于小应变线弹性问题，其弱形式为：寻找位移场 $\boldsymbol{u}$，使其对于所有容许的[虚位移](@entry_id:168781)（[检验函数](@entry_id:166589)）$\boldsymbol{v}$ 均满足：
$$
\int_\Omega \boldsymbol{\sigma}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, d\Omega = \int_\Omega \boldsymbol{f} \cdot \boldsymbol{v} \, d\Omega + \int_{\Gamma_t} \boldsymbol{t} \cdot \boldsymbol{v} \, d\Gamma
$$
在[无网格伽辽金法](@entry_id:751897)中，我们用无网格近似 $u_h(\boldsymbol{x}) = \sum_I N_I(\boldsymbol{x}) \boldsymbol{d}_I$ 和 $v_h(\boldsymbol{x}) = \sum_I N_I(\boldsymbol{x}) \boldsymbol{c}_I$ 来代替连续的场量 $\boldsymbol{u}$ 和 $\boldsymbol{v}$。其中 $\boldsymbol{d}_I$ 和 $\boldsymbol{c}_I$ 是节点上的位移参数矢量。由于[检验函数](@entry_id:166589)的任意性，这将导出一个线性代数方程组 $\boldsymbol{K}\boldsymbol{d} = \boldsymbol{F}$，其中 $\boldsymbol{K}$ 是刚度矩阵，$\boldsymbol{F}$ 是[载荷向量](@entry_id:635284) [@problem_id:3581101]。

#### 片检验（Patch Test）

**片检验**是验证数值方法一致性的基本标准。其核心思想是：如果一个问题的精确解是某个低阶多项式，那么数值方法应该能够精确地、无误差地重现这个解。

- **线性片检验**：设置一个边界条件，使其对应的精确解为一个线性[位移场](@entry_id:141476) $\boldsymbol{u}(\boldsymbol{x}) = \boldsymbol{a} + \boldsymbol{B}\boldsymbol{x}$（即常应变/应[力场](@entry_id:147325)）。一个[离散化方法](@entry_id:272547)若要精确通过该检验，其数值解必须与该线性场完全相等。
- **二次片检验**：类似地，检验方法能否精确重现一个二次多项式[位移场](@entry_id:141476)。

为了精确通过一个 $m$ 阶的片检验，[离散化方法](@entry_id:272547)必须满足两个核心条件 [@problem_id:3581118]：
1.  **$m$ 阶完备性**：近似空间必须能够精确表示所有次数不高于 $m$ 的多项式。这要求形函数具有 $m$ 阶[多项式再生](@entry_id:753580)性，并且此性质必须在整个求解域（包括边界附近）都成立。
2.  **精确积分**：弱形式中的所有积分项（例如，$\int \boldsymbol{\varepsilon}(v_h) : \mathbb{C} : \boldsymbol{\varepsilon}(u_h) d\Omega$）必须被精确计算。任何数值积分方案的精度都必须足以精确计算由该 $m$ 阶多项式解所产生的被积函数。

### 实际应用中的挑战与对策

在将[无网格伽辽金法](@entry_id:751897)付诸实践时，会遇到几个与传统[有限元法](@entry_id:749389)显著不同的关键挑战。

#### 1. 本质边界条件（[狄利克雷边界条件](@entry_id:173524)）的施加

一个标准的MLS或RKPM形函数不具备**克罗内克-德尔塔（Kronecker-delta）**性质，即 $N_I(\boldsymbol{x}_J) \neq \delta_{IJ}$ [@problem_id:3581267]。这是因为MLS近似是一个“最佳拟合”，而非“插值”。在节点 $\boldsymbol{x}_J$ 处的近似值 $u_h(\boldsymbol{x}_J)$ 是其邻近所有节点参数 $u_I$ 的加权平均，通常不等于节点参数 $u_J$ 本身 [@problem_id:3581267, @problem_id:3581101]。

这个性质的缺失意味着我们不能像在标准[有限元法](@entry_id:749389)中那样，通过直接设置节点参数值来强加[本质边界条件](@entry_id:173524)。例如，在边界节点 $\boldsymbol{x}_J$ 上施加位移 $\bar{\boldsymbol{u}}$，简单地令 $\boldsymbol{d}_J = \bar{\boldsymbol{u}}$ 并不能保证 $u_h(\boldsymbol{x}_J) = \bar{\boldsymbol{u}}$。因此，必须采用**[弱形式](@entry_id:142897)**的方法来施加这类边界条件。常见的方法包括 [@problem_id:3581267]：

- **罚函数法（Penalty Method）**：在变分泛函中增加一个罚项，如 $\frac{\alpha}{2} \int_{\Gamma_D} (\boldsymbol{u}_h - \bar{\boldsymbol{u}})^2 ds$。当罚因子 $\alpha$ 趋于无穷大时，约束被精确满足。然而，有限的 $\alpha$ 会引入 $O(\alpha^{-1})$ 的[一致性误差](@entry_id:747725)，而过大的 $\alpha$ 则会导致刚度矩阵的**病态（ill-conditioning）**。

- **[拉格朗日乘子法](@entry_id:176596)（Lagrange Multiplier Method）**：引入一个[拉格朗日乘子](@entry_id:142696)场（代表边界上的反力）作为附加的未知量。该方法可以精确满足边界条件，但会产生一个更大规模的**[鞍点](@entry_id:142576)（saddle-point）**问题。所得的[线性系统](@entry_id:147850)是**对称不定**的，并且要求乘[子空间](@entry_id:150286)和位移空间之间满足特定的相容性条件（如[LBB条件](@entry_id:746626)）以保证稳定性。

- **Nitsche法（Nitsche's Method）**：通过在[弱形式](@entry_id:142897)中引入对称且一致的边界积分项来施加约束。它不引入新的未知量，能够保持系统的对称性和正定性（对于对称正定问题），并在稳定化参数选取合适时达到最优[收敛率](@entry_id:146534)。这是一种在保持系统性质和施加精度之间取得良好平衡的流行方法。

#### 2. 数值积分

MLS/RKPM形函数是复杂的有理函数，因此[弱形式](@entry_id:142897)中的积分几乎无法解析计算，必须依赖**数值积分（numerical quadrature）**。通常的做法是在背景上铺设一个与节点[分布](@entry_id:182848)无关的**积分网格（integration grid）**，然后在每个网格单元内使用[高斯积分](@entry_id:187139)等标准方法。

- **积分精度**：为了不让[积分误差](@entry_id:171351)“污染”由近似阶数决定的收敛精度，[数值积分](@entry_id:136578)的阶次必须足够高。假设近似空间能再生 $p$ 阶多项式，应变场则能再生 $p-1$ 阶多项式。对于[常系数](@entry_id:269842)弹性问题，[弱形式](@entry_id:142897)中的刚度项被积函数 $\boldsymbol{\varepsilon}(v_h)^T \boldsymbol{C} \boldsymbol{\varepsilon}(u_h)$ 表现为 $2(p-1)$ 阶多项式。因此，为确保片检验通过和最优收敛，[高斯积分](@entry_id:187139)的精度至少需要能够精确积分 $2(p-1)$ 阶多项式 [@problem_id:3581256]。总的离散误差由近似误差（[收敛阶](@entry_id:146394)为 $O(h^p)$）和[积分误差](@entry_id:171351)（收敛阶与积分阶次相关）共同决定，最终的[收敛速度](@entry_id:636873)受限于两者中较慢的一方 [@problem_id:3581096]。

- **积分稳定性：[沙漏模式](@entry_id:174855)**：为了追求极致的[计算效率](@entry_id:270255)，研究者们提出了**节[点积](@entry_id:149019)分（nodal integration）**，即直接在每个节点上进行单[点积](@entry_id:149019)分来近似整个域的积分。这种方法极大地简化了计算，但它是一种严重的**欠积分（under-integration）**方案。其致命缺陷是无法感知那些在节点处应变为零、但在节点之间存在变形的高频变形模式。这些非[刚体运动](@entry_id:193355)模式由于在离散计算中不产生[应变能](@entry_id:162699)，被称为**虚假[零能模式](@entry_id:172472)（spurious zero-energy modes）**或**[沙漏模式](@entry_id:174855)（hourglass modes）** [@problem_id:3581157]。这些模式的存在使得刚度矩阵出现额外的零[特征值](@entry_id:154894)，导致其[秩亏](@entry_id:754065)，系统无法求解。因此，使用节[点积](@entry_id:149019)分必须配合额外的**稳定化（stabilization）**技术来抑制[沙漏模式](@entry_id:174855)。

#### 3. 线性系统的条件数

求解最终的线性方程组 $\boldsymbol{K}\boldsymbol{d} = \boldsymbol{F}$ 是计算的核心。[无网格方法](@entry_id:177458)生成的刚度矩阵 $\boldsymbol{K}$ 常常是病态的，即其**条件数**非常大，这给迭代求解器带来了巨大挑战。病态主要来源于两个方面 [@problem_id:3581229]：

1.  **[矩量](@entry_id:152982)矩阵的近奇异性**：当某个点 $\boldsymbol{x}$ 的邻域内节点数量不足或[分布](@entry_id:182848)不佳时，其矩量矩阵 $\boldsymbol{M}(\boldsymbol{x})$ 会变得近奇异。由于形函数的构造依赖于 $\boldsymbol{M}^{-1}(\boldsymbol{x})$，这会导致形函数及其导数出现剧烈[振荡](@entry_id:267781)和巨大的数值，从而使刚度矩阵中不同行/列的元素尺度差异极大，导致病态。

2.  **形函数支集的过度重叠**：当权函数的[影响域](@entry_id:175298)半径 $h$ 相对节点间距 $\Delta x$ 过大时，相邻节点的形函数会变得非常相似，因为它们是基于几乎相同的邻近节点集构造的。这导致了形函数（及其梯度）之间的**近似[线性相关](@entry_id:185830)**。在线性代数中，[基向量](@entry_id:199546)的线性相关性是导致[格拉姆矩阵](@entry_id:203297)（Gram matrix，如[刚度矩阵](@entry_id:178659)）奇[异或](@entry_id:172120)病态的直接原因，表现为[刚度矩阵](@entry_id:178659)出现非常小的[特征值](@entry_id:154894)。

为了解决[病态问题](@entry_id:137067)，**[预处理](@entry_id:141204)（preconditioning）**技术至关重要。常用的预处理器包括：
- **[对角缩放](@entry_id:748382)（Diagonal Scaling）**：也称雅可比预处理。通过将刚度矩阵的对角元缩放为1，可以有效地平衡矩阵行和列的尺度，对缓解由矩量矩阵病态引起的尺度差异问题有一定效果。
- **不完全分解（Incomplete Factorization）**：如[不完全Cholesky分解](@entry_id:750589)（IC）。这类方法利用刚度矩阵的稀疏性（源于权函数的[紧支集](@entry_id:276214)），构造一个易于求解的稀疏矩阵来逼近原矩阵。它能极大地改善[特征值](@entry_id:154894)的[分布](@entry_id:182848)，使预处理后的系统[条件数](@entry_id:145150)显著降低，是求解[大型稀疏线性系统](@entry_id:137968)的有力工具。

综上所述，[无网格伽辽金法](@entry_id:751897)虽然摆脱了[网格生成](@entry_id:149105)的束缚，但在理论和实践层面引入了一系列新的挑战。理解并妥善处理这些机制，是成功应用[无网格方法](@entry_id:177458)的关键。