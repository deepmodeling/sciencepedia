## 引言
无单元伽辽金（Element-free Galerkin, EFG）方法是[计算力学](@entry_id:174464)领域一项革命性的技术，为求解传统有限元法（FEM）难以应对的复杂工程与科学问题提供了强有力的替代方案。当问题涉及[大变形](@entry_id:167243)、[裂纹扩展](@entry_id:749562)或复杂的[几何演化](@entry_id:636861)时，基于网格的方法常常受限于网格畸变和繁琐的重新剖分过程。EFG方法通过摆脱对预定义单元网格的依赖，从根本上解决了这些挑战，为模拟这类复杂物理现象开辟了新的途径。

本文旨在系统性地介绍EFG方法的理论精髓与实践应用。在“原理与机制”一章中，我们将深入剖析其数学基石——移动最小二乘（MLS）近似和伽辽金[弱形式](@entry_id:142897)。接着，在“应用与交叉学科联系”一章中，我们将展示该方法如何在断裂力学、[计算动力学](@entry_id:204520)及多尺度建模等前沿领域中发挥其独特优势。最后，“动手实践”一章提供了一系列精心设计的编程练习，帮助读者将理论知识转化为实践能力。

通过这三个层层递进的章节，读者将全面掌握EFG方法的构建、应用与实现。让我们首先深入其核心，探索构建这一强大数值工具的基本原理与内在机制。

## 原理与机制

本章深入探讨[无单元伽辽金法](@entry_id:166627)（Element-free Galerkin, EFG）的核心构建模块。我们将剖析其两大理论支柱：其一为用于构造形函数的移动最小二乘（Moving Least Squares, MLS）近似，其二为用于建立离散系统的伽辽金方法。通过理解这些基本原理，我们将揭示 EFG 方法的强大功能、内在特性及其在实际应用中需要仔细处理的关键问题。

### 移动最小二乘 (MLS) 近似

无单元伽辽金方法与传统[有限元法](@entry_id:749389)（Finite Element Method, FEM）的一个根本区别在于其近似函数的构造方式。EFG 方法不依赖于预定义的单元网格来构建分片多项式形函数，而是采用一种更为灵活的、基于一组离散节点的纯节点方法，即**移动最小二乘（Moving Least Squares, MLS）近似**。

#### 核心思想：[局部多项式拟合](@entry_id:636664)

MLS 的核心思想是在求解域中的任意一点 $\mathbf{x}$ 附近，用一个低阶多项式来局部地逼近未知函数 $u(\mathbf{x})$。这个过程可以想象成有一个“移动”的窗口，每当我们需要在某点 $\mathbf{x}$ 处评估函数值时，我们就以该点为中心，考察其邻域内的一组节点，并利用这些节点上的信息来“动态地”构建一个最佳的局部多项式近似。

这个局部近似 $u_h(\mathbf{x})$ 通常表示为：
$u_h(\mathbf{x}) = \mathbf{p}^T(\mathbf{x}) \mathbf{a}(\mathbf{x})$

其中，$\mathbf{p}(\mathbf{x})$ 是一个多项式基函数向量。例如，在二维空间中，一个线性基可以表示为 $\mathbf{p}^T(\mathbf{x}) = \begin{pmatrix} 1  x  y \end{pmatrix}$。向量 $\mathbf{a}(\mathbf{x})$ 则是待定的系数向量，其值**依赖于评估点** $\mathbf{x}$ 的位置——这正是“移动”一词的由来。

系数 $\mathbf{a}(\mathbf{x})$ 并非任意的，而是通过最小化一个加权离散 $L_2$ 范数来确定。这个范数（或称泛函）量化了在评估点 $\mathbf{x}$ 的邻域内，局部多项式在各个节点 $\mathbf{x}_I$ 上的取值 $\mathbf{p}^T(\mathbf{x}_I)\mathbf{a}(\mathbf{x})$ 与该节点对应的未知参数 $u_I$ 之间的加权[误差平方和](@entry_id:149299)。

#### MLS 形函数的推导

为了形式化地推导 MLS 形函数，我们从定义加权最小二乘泛函 $J(\mathbf{a}, \mathbf{x})$ 开始。对于给定的评估点 $\mathbf{x}$，我们寻求系数向量 $\mathbf{a}(\mathbf{x})$ 以最小化：
$J(\mathbf{a}, \mathbf{x}) = \sum_{I=1}^{N} w_I(\mathbf{x}) \left( \mathbf{p}^T(\mathbf{x}_I) \mathbf{a}(\mathbf{x}) - u_I \right)^2$

这里，$N$ 是[影响点](@entry_id:170700) $\mathbf{x}$ 的节点总数，$u_I$ 是与节点 $\mathbf{x}_I$ 相关联的待求参数（自由度），而 $w_I(\mathbf{x}) = w(\Vert\mathbf{x} - \mathbf{x}_I\Vert)$ 是一个**权函数**，其值随着节点 $\mathbf{x}_I$ 与评估点 $\mathbf{x}$ 之间距离的增加而减小。权函数通常具有[紧支集](@entry_id:276214)，意味着只有 $\mathbf{x}$ 附近的节点才会对该点的近似产生影响。

为了最小化 $J$，我们令其关于系数向量 $\mathbf{a}(\mathbf{x})$ 的[偏导数](@entry_id:146280)为零：
$\frac{\partial J}{\partial \mathbf{a}} = \mathbf{0}$

这导出了如下的**法方程**：
$\left( \sum_{I=1}^{N} w_I(\mathbf{x}) \mathbf{p}(\mathbf{x}_I) \mathbf{p}^T(\mathbf{x}_I) \right) \mathbf{a}(\mathbf{x}) = \sum_{I=1}^{N} w_I(\mathbf{x}) \mathbf{p}(\mathbf{x}_I) u_I$

我们可以将此方程写成更紧凑的矩阵形式：
$\mathbf{A}(\mathbf{x}) \mathbf{a}(\mathbf{x}) = \mathbf{B}(\mathbf{x}) \mathbf{u}$

其中：
- $\mathbf{A}(\mathbf{x}) = \sum_{I=1}^{N} w_I(\mathbf{x}) \mathbf{p}(\mathbf{x}_I) \mathbf{p}^T(\mathbf{x}_I)$ 被称为**矩量矩阵（moment matrix）**。
- $\mathbf{B}(\mathbf{x})$ 是一个矩阵，其第 $I$ 列为 $w_I(\mathbf{x}) \mathbf{p}(\mathbf{x}_I)$。
- $\mathbf{u}$ 是包含所有节点参数 $u_I$ 的向量。

只要矩量矩阵 $\mathbf{A}(\mathbf{x})$ 是非奇异的（这要求影响节点不能处于退化的几何位置上，例如，对于线性基，节点不能共线），我们就可以解出系数向量：
$\mathbf{a}(\mathbf{x}) = \mathbf{A}^{-1}(\mathbf{x}) \mathbf{B}(\mathbf{x}) \mathbf{u}$

最后，将此解代回到局部近似表达式 $u_h(\mathbf{x}) = \mathbf{p}^T(\mathbf{x}) \mathbf{a}(\mathbf{x})$ 中，我们得到：
$u_h(\mathbf{x}) = \mathbf{p}^T(\mathbf{x}) \mathbf{A}^{-1}(\mathbf{x}) \mathbf{B}(\mathbf{x}) \mathbf{u} = \sum_{I=1}^{N} \phi_I(\mathbf{x}) u_I$

通过比较，我们便可以识别出与节点 $I$ 相关联的 MLS 形函数 $\phi_I(\mathbf{x})$：
$\phi_I(\mathbf{x}) = \mathbf{p}^T(\mathbf{x}) \left( \sum_{J=1}^{N} w_J(\mathbf{x}) \mathbf{p}(\mathbf{x}_J) \mathbf{p}^T(\mathbf{x}_J) \right)^{-1} w_I(\mathbf{x}) \mathbf{p}(\mathbf{x}_I)$

这个表达式是 MLS 近似的核心。它表明，形函数 $\phi_I(\mathbf{x})$ 是一个复杂的[有理函数](@entry_id:154279)，其形式取决于评估点 $\mathbf{x}$、所有影响节点的几何位置 $\mathbf{x}_J$、多项式基 $\mathbf{p}(\cdot)$ 以及权函数 $w(\cdot)$。

#### 示例：一维线性形函数

为了更具体地理解上述推导，我们考虑一个简单的一维算例。设有两个节点，分别位于 $x_1=0$ 和 $x_2=1$。我们采用线性多项式基 $\mathbf{p}(x) = \begin{pmatrix} 1 \\ x \end{pmatrix}$。为了简化，假设权函数在整个域上为常数，即 $w_1(x) = w_2(x) = 1$。在这种特殊情况下，[矩量](@entry_id:152982)矩阵 $\mathbf{A}$ 变为一个常数矩阵：
$\mathbf{A} = \mathbf{p}(x_1)\mathbf{p}^T(x_1) + \mathbf{p}(x_2)\mathbf{p}^T(x_2) = \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix} + \begin{pmatrix} 1  1 \\ 1  1 \end{pmatrix} = \begin{pmatrix} 2  1 \\ 1  1 \end{pmatrix}$

其逆矩阵为 $\mathbf{A}^{-1} = \begin{pmatrix} 1  -1 \\ -1  2 \end{pmatrix}$。
形函数向量 $\mathbf{\phi}^T(x) = \begin{pmatrix} \phi_1(x)  \phi_2(x) \end{pmatrix}$ 可以通过下式计算：
$\mathbf{\phi}^T(x) = \mathbf{p}^T(x) \mathbf{A}^{-1} \begin{pmatrix} \mathbf{p}(x_1)  \mathbf{p}(x_2) \end{pmatrix}^T = \begin{pmatrix} 1  x \end{pmatrix} \begin{pmatrix} 1  -1 \\ -1  2 \end{pmatrix} \begin{pmatrix} 1  1 \\ 0  1 \end{pmatrix} = \begin{pmatrix} 1-x  x \end{pmatrix}$

因此，我们得到 $\phi_1(x) = 1-x$ 和 $\phi_2(x) = x$。这恰好是标准[有限元法](@entry_id:749389)中的一维线性[拉格朗日形函数](@entry_id:635448)。这个结果揭示了一个重要的联系：在某些高度简化的条件下，MLS 近似可以退化为我们熟悉的形式。然而，一旦权函数变得非均匀（例如，采用更实际的高斯型或[样条](@entry_id:143749)型权函数），形函数就会变成复杂的[有理函数](@entry_id:154279)，不再是简单的多项式。

### MLS 近似的关键特性

MLS 近似所产生的形函数具有一些与传统有限元形函数截然不同的关键特性，这些特性决定了 EFG 方法的优势与挑战。

#### 权函数的角色

权函数 $w(r)$ 在 MLS 中扮演着至关重要的角色，它定义了近似的“局部”性质。理想的权函数应具有**[紧支集](@entry_id:276214)（compact support）**，即当距离 $r$ 超过某个支持半径 $\rho$ 时，权函数值为零。这意味着在评估点 $\mathbf{x}$ 处的近似只受其 $\rho$-邻域内的节点影响，这保证了最终[系统矩阵](@entry_id:172230)的[稀疏性](@entry_id:136793)。

权函数的**光滑度**也至关重要。一个重要的结论是，MLS 形函数会继承权函数的光滑度。如果权函数在其支集内部是 $C^k$ 连续的，那么所产生的 MLS 形函数 $\phi_I(\mathbf{x})$ 也是 $C^k$ 连续的（只要邻域内的节点集不发生突变）。这使得 EFG 方法能够轻易构建高阶连续的近似，这在分析要求解具有高阶光滑度的物理问题（如壳体和板问题）时非常有利。

实践中常用的权函数包括：
- **[三次样条](@entry_id:140033)函数**：$w(r) = \begin{cases} \frac{2}{3} - 4r^2 + 4r^3  & \text{if } r \le 0.5 \\ \frac{4}{3} - 4r + 4r^2 - \frac{4}{3}r^3  & \text{if } 0.5 < r \le 1 \\ 0  & \text{if } r > 1 \end{cases}$
- **四次[样条](@entry_id:143749)函数**：$w(r) = \begin{cases} 1 - 6r^2 + 8r^3 - 3r^4  & \text{if } r \le 1 \\ 0  & \text{if } r > 1 \end{cases}$
- **截断高斯函数**：$w(r) = \begin{cases} \exp(-\alpha r^2) - \exp(-\alpha)  & \text{if } r \le 1 \\ 0  & \text{if } r > 1 \end{cases}$

[样条](@entry_id:143749)函数在计算上更高效，而高斯函数形式更简单。选择哪种权函数以及其支持域的大小，是影响 EFG 方法计算成本和精度的重要因素。支持域越大，参与计算的节点越多，单个评估点的计算量越大，但近似可能更稳定。

#### [多项式完备性](@entry_id:177462) (再生性质)

MLS 近似最核心的性质是其**[多项式完备性](@entry_id:177462)（polynomial completeness）**，或称**再生性质（reproducing property）**。如果 MLS 近似采用了 $m$ 阶多项式基 $\mathcal{P}_m$，并且矩量矩阵处处非奇异，那么所生成的形函数就具有 $m$ 阶完备性。这意味着，这组形函数可以精确地再生（或重构）任何次数不高于 $m$ 的多项式。形式上，对于任意 $p(\mathbf{x}) \in \mathcal{P}_m$，下式恒成立：
$\sum_{I=1}^{N} \phi_I(\mathbf{x}) p(\mathbf{x}_I) = p(\mathbf{x})$

这个性质是保证近似精度的理论基石。例如，零阶完备性 ($m=0$) 对应于再生[常数函数](@entry_id:152060)的能力，即 $\sum_I \phi_I(\mathbf{x}) = 1$，这被称为**[单位分解](@entry_id:150115)（partition of unity）** 性质。一阶完备性 ($m=1$) 则保证了对线性场的精确再生。

完备性的阶数直接决定了数值方法的[收敛率](@entry_id:146534)。对于一个具有 $m$ 阶完备性的方法，在求解一个光滑解的椭圆[边值问题](@entry_id:1121801)时，其近似解在[能量范数](@entry_id:274966)（如 $H^1$ 范数）下的[误差收敛](@entry_id:137755)阶约为 $O(h^m)$，在 $L^2$ 范数下的[误差收敛](@entry_id:137755)阶约为 $O(h^{m+1})$，其中 $h$ 是节点的特征间距。因此，通过提高 MLS 基函数的阶数，原则上可以实现更高的[收敛率](@entry_id:146534)。

#### 克罗内克 Delta (Kronecker Delta) 性质的缺失

与标准有限元形函数的一个显著区别是，标准 MLS 形函数**不具备克罗内克 Delta（Kronecker Delta）性质**。也就是说，在一般情况下：
$\phi_I(\mathbf{x}_J) \neq \delta_{IJ}$
其中 $\delta_{IJ}$ 是克罗内克符号（当 $I=J$ 时为 1，否则为 0）。这意味着，在节点 $\mathbf{x}_J$ 处的近似值 $u_h(\mathbf{x}_J) = \sum_I \phi_I(\mathbf{x}_J) u_I$ 并非直接等于该节点的参数 $u_J$，而是其邻域内所有节点参数的加权平均。因此，MLS 是一种**近似**方法，而非**插值**方法。

这个特性带来了深远的影响，其中最重要的一点是关于**[本质边界条件](@entry_id:173524)（[狄利克雷边界条件](@entry_id:173524)）的施加**。在有限元中，由于 $\phi_I(\mathbf{x}_J) = \delta_{IJ}$，我们可以通过直接将边界节点的自由度 $u_J$ 设为给定值 $\bar{u}$ 来强行施加边界条件。但在 EFG 方法中，这样做并不能保证在[边界点](@entry_id:176493) $\mathbf{x}_J$ 处的解满足 $u_h(\mathbf{x}_J) = \bar{u}$。

因此，EFG 方法必须采用特殊的策略来施加[本质边界条件](@entry_id:173524)。常用的方法包括[罚函数法](@entry_id:636090)（penalty method）、[拉格朗日乘子法](@entry_id:176596)（Lagrange multipliers）或 Nitsche 法等。这些方法通过在[变分方程](@entry_id:635018)中引入附加项来[弱形式](@entry_id:142897)地施加边界约束，是 EFG 方法实施中的一个关键技术环节。

### 从近似到离散化：伽辽金框架

构建了形函数之后，下一步就是利用它们将连续的[偏微分](@entry_id:194612)方程（PDE）转化为离散的代数方程组。EFG 方法的名字昭示了它采用的是[伽辽金法](@entry_id:749698)。

#### 弱形式与[伽辽金法](@entry_id:749698)

我们以一个标量扩散问题为例来说明这个过程。其强形式为：
$-\nabla \cdot (k \nabla u) = f$

通过与一个任意的检验函数 $v$ 相乘并在求解域 $\Omega$ 上积分，再利用[分部积分](@entry_id:136350)（或高维的散度定理），我们可以得到问题的**[弱形式](@entry_id:142897)**：
$\int_{\Omega} k \nabla v \cdot \nabla u \, d\Omega = \int_{\Omega} v f \, d\Omega + \int_{\Gamma_N} v \bar{t} \, dS$

其中 $\bar{t}$ 是在诺伊曼边界 $\Gamma_N$ 上给定的流量。伽辽金法的核心思想是，用与构造近似解 $u_h$ 相同的基[函数空间](@entry_id:143478)来选取[检验函数](@entry_id:166589) $v$。具体来说，我们将 MLS 近似 $u_h(\mathbf{x}) = \sum_I \phi_I(\mathbf{x}) d_I$ 代入弱形式，并依次令检验函数为每个形函数 $\phi_J(\mathbf{x})$。这会产生一个线性[代数方程](@entry_id:272665)组：
$\mathbf{K} \mathbf{d} = \mathbf{f}$

其中，$\mathbf{d}$ 是待求的节点参数向量，刚度矩阵 $\mathbf{K}$ 和[载荷向量](@entry_id:635284) $\mathbf{f}$ 的分量分别为：
$K_{JI} = \int_{\Omega} k (\nabla \phi_J) \cdot (\nabla \phi_I) \, d\Omega$
$f_J = \int_{\Omega} \phi_J f \, d\Omega + \int_{\Gamma_N} \phi_J \bar{t} \, dS$

#### 积分的挑战：背景单元

上述刚度矩阵和[载荷向量](@entry_id:635284)的表达式中包含了对形函数及其梯度的积分。然而，正如我们已经看到的，MLS 形函数是复杂的[有理函数](@entry_id:154279)，对其进行解析积分几乎是不可能的。这是 EFG 方法面临的一个核心计算挑战。

解决方案是采用**数值积分**。EFG 方法巧妙地将近似的构造（依赖于节点）与积分的执行（依赖于几何剖分）[解耦](@entry_id:160890)。具体做法是在求解域 $\Omega$ 上铺设一个独立的、简单的**背景积分网格（background integration grid）**。这个网格由简单的几何形状（如四边形或三角形）组成，它不影响形函数的定义，仅用于执行[数值积分](@entry_id:136578)。在每个背景单元上，我们可以采用标准的数值求积法则，如**[高斯求积](@entry_id:146011)（Gaussian quadrature）**，来[近似计算](@entry_id:1121073)所需的积分。

这种[解耦](@entry_id:160890)是 EFG 方法灵活性的关键来源：节点的分布可以非常自由，甚至随机，而积分则可以在一个结构化的背景网格上高效进行。

#### 积分准则的精度要求

一个自然的问题是：为了保证整个数值方法的精度，数值积分需要多精确？如果[积分误差](@entry_id:171351)过大，它将“污染”由高质量 MLS 近似所带来的高精度，导致实际[收敛率](@entry_id:146534)达不到理论预期。

这个问题的答案与**补片检验（patch test）** 密切相关。补片检验是验证数值方法是否能精确再现[基本解](@entry_id:184782)（如常数或线性场）的一种测试。为了使一个具有 $m$ 阶完备性的 EFG 方法能够通过 $m$ 阶补片检验，从而保证其理论[收敛率](@entry_id:146534)，所使用的[数值积分法则](@entry_id:175061)必须满足一定的精度要求。

一个被广泛接受的充分条件是：用于[计算刚度](@entry_id:1122809)矩阵的[求积法则](@entry_id:753909)，必须能够精确积分最高次数为 $2(p-1)$ 的多项式，其中 $p$ 是 MLS 近似的完备阶数。例如：
- 对于一维问题，若要保证 $p$ 阶完备性，使用 $n$ 点[高斯-勒让德求积](@entry_id:138201)时，需要满足 $2n-1 \ge 2(p-1)$，即 $n \ge p - 1/2$。由于 $n$ 是整数，所以需要 $n \ge p$ 个积分点。
- 对于二维[四边形单元](@entry_id:176937)，若要保证 $p$ 阶完备性，使用 $m \times m$ 的[高斯点](@entry_id:170251)就足够了，只要 $m \ge p$。

不满足此要求的“欠积分”可能会导致刚度矩阵奇异，产生[伪零能模式](@entry_id:755267)，从而破坏解的稳定性。

### 高级主题与精细化处理

尽管 MLS 和背景积分构成了 EFG 的基础，但在处理复杂问题时，还需要一些更精细的理论和技术。

#### 复杂几何与边界的处理

当求解域包含凹角、裂纹或孔洞等复杂几何特征时，标准的 MLS 近似可能会失效。问题出在评估点靠近这些凹边界时，其支持域（由权函数定义的邻域）可能会被边界“切掉”，变成非凸的“楔形”区域。

在这种情况下，如果天真地只考虑“可见”的节点（即与评估点连线不穿过求解域外部的节点），那么这些可见节点在空间中的分布将是有偏的，可能集中在某个方向上。这种有偏的分布会导致[矩量](@entry_id:152982)矩阵 $\mathbf{A}(\mathbf{x})$ 变得病态甚至奇异，从而破坏 MLS 的再生条件，导致精度严重下降。

解决此问题的前沿技术包括引入**可见性准则（visibility criterion）** 和**[矩量](@entry_id:152982)校正（moment correction）**。其思想是，首先通过可见性判据剔除被遮挡的、物理上不相关的节点，然后对保留下来的节点权重进行修正，以强制满足再生所需的代数条件（例如，强制修正后的权重一阶矩为零）。这种方法可以恢复在复杂几何边界附近的完备性，是 EFG 方法处理[断裂力学](@entry_id:141480)等问题的关键技术之一。

#### 节点积分的陷阱与稳定化

背景积分网格虽然有效，但引入了与节点集独立的第二套几何实体，增加了实现的复杂性。一个看似更简单、更符合“无网格”精神的替代方案是**直接节点积分（direct nodal integration, DNI）**，即用各节点处被积函数值的加权和来近似整个域上的积分。

然而，对于实[体力](@entry_id:174230)学等问题，简单的节点积分会导致灾难性的后果。其根本原因在于，节点积分对被积函数（特别是[应变能密度](@entry_id:200085)）的采样严重不足。存在这样一种非物理的变形模式：它在所有节点处的应变均为零，但在节点之间却有显著的非零应变。对于这种模式，节点积分计算出的应变能为零，导致[刚度矩阵](@entry_id:178659)出现额外的零特征值（即[秩亏](@entry_id:754065)），这便是所谓的**[伪零能模式](@entry_id:755267)（spurious zero-energy modes）**，它会使数值解完全失稳。

为了克服 DNI 的不稳定性，同时保留其计算上的简便性，研究者们发展了**稳定化一致性节点积分（Stabilized Conforming Nodal Integration, SCNI）** 等高级积分格式。SCNI 的核心思想有两点：
1.  **光滑化梯度**：它不再使用在节点处直接求导得到的梯度 $\nabla\phi_I(\mathbf{x}_J)$，而是通过[散度定理](@entry_id:143110)，将节点邻域（如[沃罗诺伊单元](@entry_id:144746)）内的平均梯度转化为该邻域边界上的积分来计算一个“光滑化”的梯度。这个过程保证了对线性场的精确再生（通过了补片检验）。
2.  **引入稳定项**：仅有光滑化梯度可能导致系统过“软”。因此，SCNI 额外引入一个稳定化项，该项惩罚了原始点态梯度与光滑化梯度之间的差异。这样，任何引起二者显著偏离的[伪零能模式](@entry_id:755267)都会获得一个非零的能量惩罚，从而被抑制，恢复了[刚度矩阵](@entry_id:178659)的满秩和方法的稳定性。

SCNI 及其变体是现代 EFG 方法中实现高效与稳定计算的关键技术之一，它体现了在追求[计算效率](@entry_id:270255)的同时，必须深刻理解并维护方法基本数学性质的重要性。