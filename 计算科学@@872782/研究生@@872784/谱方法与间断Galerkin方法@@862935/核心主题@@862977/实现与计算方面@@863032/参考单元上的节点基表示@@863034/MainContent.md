## 引言
在[高阶数值方法](@entry_id:142601)（如谱方法和[间断Galerkin方法](@entry_id:748369)）中，通过在计算单元上使用高次多项式来逼近解是实现高精度的关键。为了高效、系统地处理这一过程，尤其是在面对复杂几何时，通常会在标准的“[参考单元](@entry_id:168425)”上定义这些多项式。然而，如何选择和构建一个既直观又便于计算的[基函数](@entry_id:170178)来表示这些多项式，是开发稳健数值格式的核心问题。本文旨在填补这一知识空白，系统阐述参考单元上[节点基](@entry_id:752522)表示的完整图景。在接下来的内容中，读者将首先在“原理与机制”一章中学习[节点基](@entry_id:752522)的基本构造，包括[拉格朗日多项式](@entry_id:142463)和[节点选择](@entry_id:637104)的重要性。随后，“应用与交叉学科联系”一章将展示这些原理如何在[微分算子](@entry_id:140145)构造、[间断Galerkin方法](@entry_id:748369)以及处理复杂几何与[非线性](@entry_id:637147)问题中发挥关键作用。最后，“动手实践”部分将提供具体的计算练习，帮助读者巩固所学知识。

## 原理与机制

在谱方法和间断Galerkin (DG)方法中，为了获得[高阶精度](@entry_id:750325)，解在计算域的每个单元上被表示为高次多项式。为了系统地处理复杂的几何形状和简化计算，这些多项式通常定义在几个标准的**参考单元 (reference elements)** 上。通过可逆的[几何映射](@entry_id:749852)，参考单元上的计算可以被转换到物理空间中的任意单元上。本章将深入探讨在这些[参考单元](@entry_id:168425)上构建和使用**[节点基](@entry_id:752522) (nodal basis)** 的核心原理与机制。

### 基础：[参考单元](@entry_id:168425)与多项式空间

在[数值分析](@entry_id:142637)中，[参考单元](@entry_id:168425)是一个简单的、[标准化](@entry_id:637219)的几何域，我们在此之上定义[基函数](@entry_id:170178)。所有的计算，如[微分](@entry_id:158718)和积分，都在这个参考单元上执行。

最常见的一维[参考单元](@entry_id:168425)是[闭区间](@entry_id:136474) $\hat{K}_{1D} = [-1,1]$。对于更高维度 $d \in \mathbb{N}$，主要有两种类型的[参考单元](@entry_id:168425)：[超立方体](@entry_id:273913)和单纯形。

- **参考超立方体 (Reference Hypercube)**：$d$ 维参考[超立方体](@entry_id:273913) $\hat{K}_{\square}$ 是通过一维参考区间的[张量积](@entry_id:140694)构造的，定义为 $\hat{K}_{\square} = [-1,1]^d$。例如，在二维情况下，它是一个边长为2的正方形 $[-1,1]^2$；在三维情况下，它是一个立方体 $[-1,1]^3$。

- **参考单纯形 (Reference Simplex)**：$d$ 维标准参考单纯形 $\hat{K}_{\triangle}$ 定义为 $\hat{K}_{\triangle} = \{\boldsymbol{r} \in \mathbb{R}^d : r_i \ge 0 \text{ 对所有 } i, \sum_{i=1}^d r_i \le 1\}$。在二维情况下，它是一个由顶点 $(0,0)$, $(1,0)$ 和 $(0,1)$ 构成的直角三角形；在三维情况下，它是一个四面体。

在这些[参考单元](@entry_id:168425)上，我们定义[多项式空间](@entry_id:144410)来逼近解。多项式由单项式 $r_1^{i_1} r_2^{i_2} \cdots r_d^{i_d}$ 的线性组合构成，其中 $i_j$ 是非负整数。根据对指数 $i_j$ 的约束方式，我们定义了两种主要的多项式空间 [@problem_id:3402576]：

- **$Q^N$ 空间 (Tensor-Product Polynomials)**：这个空间通常定义在超立方体 $\hat{K}_{\square}$ 上。它由所有在每个变量中的次数都不超过 $N$ 的多项式组成。也就是说，对于每个单项式 $r_1^{i_1} \cdots r_d^{i_d}$，其指数必须满足 $0 \le i_j \le N$ 对所有的 $j=1,\dots,d$。由于每个变量的指数可以独立地从 $0$ 到 $N$ 取值，共有 $N+1$ 种选择，因此 $d$ 维空间 $Q^N(\hat{K}_{\square})$ 的维度是 $\dim Q^N(\hat{K}_{\square}) = (N+1)^d$。

- **$P^N$ 空间 (Total-Degree Polynomials)**：这个空间通常定义在单纯形 $\hat{K}_{\triangle}$ 上。它由所有**总次数 (total degree)** 不超过 $N$ 的多项式组成。一个单项式的总次数定义为其所有指数之和 $\sum_{j=1}^d i_j$。因此，$P^N(\hat{K}_{\triangle})$ 包含了所有满足 $\sum_{j=1}^d i_j \le N$ 的单项式。利用[组合数学](@entry_id:144343)中的“[隔板法](@entry_id:152143)”，可以证明该空间的维度为 $\dim P^N(\hat{K}_{\triangle}) = \binom{N+d}{d}$。

这两种多项式空间的选择与参考单元的几何结构天然匹配。$Q^N$ 空间的张量积结构非常适合超立方体，而 $P^N$ 空间则更自然地适用于单纯形。

### [节点基](@entry_id:752522)：[拉格朗日多项式](@entry_id:142463)

一旦我们选定了多项式空间 $\mathbb{P}_N(\hat{K})$（它可以是 $Q^N$ 或 $P^N$），我们就需要一个基来表示空间中的任意多项式。在众多选择中，**[节点基](@entry_id:752522) (nodal basis)** 因其出色的物理直观性和易于实现插值而备受青睐。

给定参考单元 $\hat{K}$ 上的一个多项式空间 $\mathbb{P}_N(\hat{K})$，其维度为 $N_p = \dim \mathbb{P}_N(\hat{K})$。我们选择 $N_p$ 个不同的点，称为**节点 (nodes)**，记为 $\{\boldsymbol{x}_i\}_{i=1}^{N_p} \subset \hat{K}$。如果唯一一个在所有这些节点上都为零的 $\mathbb{P}_N(\hat{K})$ 多项式是零多项式，那么这个节点集被称为是**单解的 (unisolvent)**。

对于一个单解的节点集，我们可以定义一组与之对应的**[拉格朗日基多项式](@entry_id:168175) (Lagrange basis polynomials)**，记为 $\{\ell_j\}_{j=1}^{N_p} \subset \mathbb{P}_N(\hat{K})$。这组[基函数](@entry_id:170178)的定义非常简洁，它通过**克罗内克 delta (Kronecker delta)** 性质来描述：
$$
\ell_j(\boldsymbol{x}_i) = \delta_{ij} = \begin{cases} 1  \text{若 } i=j \\ 0  \text{若 } i \neq j \end{cases}
$$
这个性质意味着[基函数](@entry_id:170178) $\ell_j$ 在节点 $\boldsymbol{x}_j$ 处取值为1，而在所有其他节点 $\boldsymbol{x}_i$ ($i \neq j$) 处取值为0。

#### 显式构造

[拉格朗日基](@entry_id:751105)的存在性由节点集的单解性保证，其构造方式也十分直接 [@problem_id:3402559]。

在一维参考区间 $[-1,1]$ 上，对于给定的 $N+1$ 个不同节点 $\{x_m\}_{m=0}^N$，[拉格朗日基](@entry_id:751105)函数 $\ell_j(x) \in \mathbb{P}_N([-1,1])$ 的显式乘积形式为：
$$
\ell_j(x) = \prod_{\substack{m=0 \\ m \neq j}}^{N} \frac{x - x_m}{x_j - x_m}
$$
这个公式清晰地展示了 $\ell_j(x)$ 是一个 $N$ 次多项式，并且满足 $\ell_j(x_j)=1$ 和 $\ell_j(x_m)=0$ 对于 $m \neq j$。然而，在数值计算中，直接使用此公式进行求值可[能效](@entry_id:272127)率不高且不稳定。一个更受欢迎的替代方法是**[重心坐标](@entry_id:155488)插值公式 (barycentric interpolation formula)** [@problem_id:3402619]。通过定义一个节点多项式 $L(x) = \prod_{m=0}^N (x-x_m)$ 和重心权重 $w_j = \left(\prod_{m \neq j}(x_j - x_m)\right)^{-1}$，[拉格朗日基](@entry_id:751105)可以写成 $\ell_j(x) = L(x) \frac{w_j}{x-x_j}$。利用恒等式 $\sum_{j=0}^N \ell_j(x) = 1$，我们可以消去 $L(x)$，得到一个有理表达式形式的插值公式，这在计算上更为高效和稳健。

在高维情况下，构造方法取决于单元的类型 [@problem_id:3402559]。

- **张量积单元**：在参考正方形 $[-1,1]^2$ 上，对于一个由一维节点集 $\{x_i\}_{i=0}^N$ 和 $\{y_j\}_{j=0}^M$ 构成的[张量积网格](@entry_id:755861)，二维[拉格朗日基](@entry_id:751105)函数可以通过一维基的简单**[张量积](@entry_id:140694) (tensor product)** 得到：
$$
L_{ij}(\xi, \eta) = \ell_i(\xi) \ell_j(\eta) = \left( \prod_{\substack{k=0 \\ k \neq i}}^{N} \frac{\xi - x_k}{x_i - x_k} \right) \left( \prod_{\substack{l=0 \\ l \neq j}}^{M} \frac{\eta - y_l}{y_j - y_l} \right)
$$
这个[基函数](@entry_id:170178)在节点 $(x_i, y_j)$ 处为1，在所有其他网格点 $(x_{i'}, y_{j'})$ 处为0。

- **单纯形单元**：在参考单纯形上，尤其是对于低阶多项式，**[重心坐标](@entry_id:155488) (barycentric coordinates)** 提供了一种优雅的构造方式。例如，在顶点为 $v_1=(0,0), v_2=(1,0), v_3=(0,1)$ 的二维参考三角形上，与这三个顶点相关联的线性[拉格朗日基](@entry_id:751105)函数（即 $P^1$ 空间）正是该点的[重心坐标](@entry_id:155488)：
$$
\phi_1(x,y) = 1 - x - y, \quad \phi_2(x,y) = x, \quad \phi_3(x,y) = y
$$
可以验证，$\phi_1$ 在 $v_1$ 处为1，在 $v_2, v_3$ 处为0，其他[基函数](@entry_id:170178)也类似。

### 节点插值算子

[拉格朗日基](@entry_id:751105)的优美之处在于它使得插值变得异常简单。给定一个定义在 $\hat{K}$ 上的[连续函数](@entry_id:137361) $f \in C^0(\hat{K})$，我们可以定义一个**插值算子 (interpolation operator)** $I_N: C^0(\hat{K}) \to \mathbb{P}_N(\hat{K})$，它将函数 $f$ 映射到其在节点集上的多项式插值。这个[插值多项式](@entry_id:750764) $I_N f$ 可以显式地写为 [@problem_id:3402622]：
$$
(I_N f)(\boldsymbol{x}) = \sum_{j=1}^{N_p} f(\boldsymbol{x}_j) \ell_j(\boldsymbol{x})
$$
这意味着[插值多项式](@entry_id:750764)在基 $\{\ell_j\}$ 下的展开系数恰好就是函数 $f$ 在节点上的采样值 $f(\boldsymbol{x}_j)$。

这个算子具有几个关键性质 [@problem_id:3402622]：

1.  **插值性 (Interpolation Property)**：根据构造，$(I_N f)(\boldsymbol{x}_i) = \sum_{j=1}^{N_p} f(\boldsymbol{x}_j) \ell_j(\boldsymbol{x}_i) = \sum_{j=1}^{N_p} f(\boldsymbolx_j) \delta_{ji} = f(\boldsymbol{x}_i)$。即插值多项式在所有节点上都与原函数的值完全吻合。

2.  **[多项式再生](@entry_id:753580)性 (Polynomial Reproduction)**：如果待插值的函数 $p$ 本身就是 $\mathbb{P}_N(\hat{K})$ 空间中的一个多项式，那么其插值结果就是它自身，即 $I_N p = p$。这是因为 $I_N p$ 和 $p$ 都是 $\mathbb{P}_N(\hat{K})$ 中的多项式，并且它们在 $N_p$ 个单解节点上的值相同，因此它们必须是同一个多项式。

3.  **投影性 (Projection Property)**：$I_N$ 是一个投影算子，满足 $I_N^2 = I_N$。这是再生性的直接推论。对于任意函数 $f \in C^0(\hat{K})$，$I_N f$ 是一个 $\mathbb{P}_N(\hat{K})$ 中的多项式。对其再次应用 $I_N$，根据再生性，我们得到 $I_N(I_N f) = I_N f$。

值得强调的是，尽管 $I_N$ 是一个投影算子，但它通常不是 $L^2$ **[正交投影](@entry_id:144168) ($L^2$-orthogonal projection)**。$L^2$ 投影的定义要求其误差 $f - P_N f$ 与投影空间 $\mathbb{P}_N(\hat{K})$ 中的所有多项式都正交。然而，对于节点插值算子 $I_N$，其误差 $f - I_N f$ 一般不具有此正交性 [@problem_id:3402622]。这是一个区分节点插值和[Galerkin投影](@entry_id:145611)的关键点。

[拉格朗日基](@entry_id:751105)的存在性、节点集的单解性以及描述从任意基系数到节点值的变换的**广义[范德蒙矩阵](@entry_id:147747) (generalized Vandermonde matrix)** 的[可逆性](@entry_id:143146)，这三者是等价的 [@problem_id:3402622]。

### 节点集的选择：稳定性与精度

虽然任何单解的节点集都可以定义一组[拉格朗日基](@entry_id:751105)，但节点集的选择对插值的**稳定性 (stability)** 和精度有巨大影响。一个糟糕的[节点选择](@entry_id:637104)会导致随着多项式次数 $N$ 的增加，插值多项式在节点之间产生剧烈的[振荡](@entry_id:267781)，这种现象被称为**龙格现象 (Runge phenomenon)**。

为了量化插值的稳定性，我们引入**勒贝格函数 (Lebesgue function)** $\Lambda_N(\boldsymbol{x})$ 和**[勒贝格常数](@entry_id:196241) (Lebesgue constant)** $\|\Lambda_N\|_{\infty}$ [@problem_id:3402608] [@problem_id:3402622]：
$$
\Lambda_N(\boldsymbol{x}) = \sum_{j=1}^{N_p} |\ell_j(\boldsymbol{x})|, \qquad \|\Lambda_N\|_{\infty} = \max_{\boldsymbol{x} \in \hat{K}} \Lambda_N(\boldsymbol{x})
$$
[勒贝格常数](@entry_id:196241)是插值算子 $I_N$ 在[无穷范数](@entry_id:637586)下的[算子范数](@entry_id:752960)，即 $\|I_N\|_{C^0 \to C^0} = \|\Lambda_N\|_{\infty}$。它给出了[插值误差](@entry_id:139425)相对于最佳[多项式逼近](@entry_id:137391)误差的放大因子。一个缓慢增长的[勒贝格常数](@entry_id:196241)是保证插值过程稳定和收敛的关键。

在一维区间 $[-1,1]$ 上，三种常见的节点集表现出截然不同的行为 [@problem_id:3402572] [@problem_id:3402608]：

- **[等距节点](@entry_id:168260) (Equispaced Nodes)**：虽然直观，但这是最差的选择。其[勒贝格常数](@entry_id:196241)随 $N$ **指数增长** ($\|\Lambda_N\|_{\infty} \sim 2^N$)，导致灾难性的龙格现象。

- **高斯-勒让德节点 (Gauss-Legendre, GL)**：这些节点是 $(N+1)$ 阶勒让德多项式 $P_{N+1}(x)$ 的根。它们[分布](@entry_id:182848)在[开区间](@entry_id:157577) $(-1,1)$ 内，不包含端点。其[勒贝格常数](@entry_id:196241)随 $N$ **对数增长** ($\|\Lambda_N\|_{\infty} \sim \frac{2}{\pi} \log N$)，这种缓慢的增长保证了高阶插值的稳定性。

- **[高斯-洛巴托-勒让德节点](@entry_id:165096) ([Gauss-Lobatto-Legendre](@entry_id:749736), GLL)**：这些节点包括端点 $\pm 1$ 以及 $N$ 阶勒让德多项式导数 $P'_N(x)$ 的根。因为包含单元边界上的点，GLL节点在[谱元法](@entry_id:755171)中被广泛用于保证单元间的 $C^0$ 连续性。其[勒贝格常数](@entry_id:196241)也随 $N$ **对数增长** ($\|\Lambda_N\|_{\infty} \sim \frac{2}{\pi} \log N$)。

从线性代数的角度看，节点集的质量也反映在以某个正交多项式（如[勒让德多项式](@entry_id:141510)）为基底的[范德蒙矩阵](@entry_id:147747) $V$ 的**[条件数](@entry_id:145150) (condition number)** $\kappa(V)$ 上 [@problem_id:3402596]。条件数衡量了输入数据（节点值）的微小扰动对输出（[多项式系数](@entry_id:262287)）的影响。对于[等距节点](@entry_id:168260)，$\kappa(V)$ 随 $N$ 指数增长，而对于GL和GLL节点，$\kappa(V)$ 仅以温和的多项式速率增长（对于正交勒让德基，$\kappa(V) = \Theta(N^{1/2})$）。这再次证实了高斯型节点在数值稳定性方面的巨大优势。

### [参考单元](@entry_id:168425)上的节点运算

[节点基](@entry_id:752522)表示法的一个主要优点是它简化了在[参考单元](@entry_id:168425)上的各种运算，特别是[微分](@entry_id:158718)和到物理单元的映射。

#### [微分](@entry_id:158718)

任何在 $\mathbb{P}_N(\hat{K})$ 中的多项式 $u_h$ 及其导数 $\nabla u_h$ 仍然是多项式。因此，我们可以在节点上精确地表示导数。在一维情况下，设 $u_h(x) = \sum_{j=0}^N u_j \ell_j(x)$，其中 $u_j = u_h(x_j)$。其导数为 $u_h'(x) = \sum_{j=0}^N u_j \ell_j'(x)$。在节点 $x_i$ 处计算该导数的值，我们得到：
$$
u_h'(x_i) = \sum_{j=0}^N u_j \ell_j'(x_i)
$$
如果我们定义一个**[微分矩阵](@entry_id:149870) (differentiation matrix)** $D$，其元素为 $D_{ij} = \ell_j'(x_i)$，那么节点上的导数值向量 $\boldsymbol{u}' = (u_h'(x_0), \dots, u_h'(x_N))^T$ 可以通过简单的矩阵-向量乘法得到：$\boldsymbol{u}' = D \boldsymbol{u}$。

这个思想可以高效地推广到二维或三维的[张量积](@entry_id:140694)单元上。例如，在参考正方形 $[-1,1]^2$ 上，使用[张量积](@entry_id:140694)基 $\phi_{ij}(\xi,\eta) = \ell_i(\xi)\ell_j(\eta)$。一个函数 $u_h(\xi, \eta) = \sum_{i,j} U_{ij} \phi_{ij}(\xi,\eta)$ 的[偏导数](@entry_id:146280)在节点 $(\xi_p, \eta_q)$ 处的值可以表示为：
$$
\frac{\partial u_h}{\partial \xi}(\xi_p, \eta_q) = \sum_i (D_{\xi})_{pi} U_{iq}, \qquad \frac{\partial u_h}{\partial \eta}(\xi_p, \eta_q) = \sum_j (D_{\eta})_{qj} U_{pj}
$$
其中 $D_{\xi}$ 和 $D_{\eta}$ 是一维[微分矩阵](@entry_id:149870)。如果我们将二维节点值 $U_{ij}$ 按行或按列[向量化](@entry_id:193244)为一个长向量 $\mathbf{u}$，那么二维偏微分算子可以优雅地表示为**克罗内克积 (Kronecker products)** [@problem_id:3402610]。例如，对于按行展开的 lexicographic 排序，偏导算子矩阵为：
$$
\mathcal{D}_{\xi} = D \otimes I, \qquad \mathcal{D}_{\eta} = I \otimes D
$$
其中 $I$ 是[单位矩阵](@entry_id:156724)。这种结构使得多维[微分](@entry_id:158718)运算可以分解为一系列一维运算，极大地提高了计算效率。

#### 到物理单元的映射

为了处理复杂的几何形状，我们定义一个从[参考单元](@entry_id:168425) $\hat{K}$（坐标为 $\boldsymbol{\xi}$）到物理空间中的单元 $K$（坐标为 $\boldsymbol{x}$）的映射 $\boldsymbol{x} = \boldsymbol{F}(\boldsymbol{\xi})$。在**等参 (isoparametric)** 方法中，这个[几何映射](@entry_id:749852)本身也用与解相同的[节点基](@entry_id:752522)来表示。

函数在物理坐标下的梯度 $\nabla_{\boldsymbol{x}} u$ 和在参考坐标下的梯度 $\nabla_{\boldsymbol{\xi}} \hat{u}$（其中 $\hat{u}(\boldsymbol{\xi}) = u(\boldsymbol{x}(\boldsymbol{\xi}))$）通过[多元函数](@entry_id:145643)的链式法则联系起来。其关系式为 [@problem_id:3402600]：
$$
\nabla_{\boldsymbol{x}} u = (J^{-1})^T \nabla_{\boldsymbol{\xi}} \hat{u}
$$
其中 $J$ 是映射 $\boldsymbol{F}$ 的**雅可比矩阵 (Jacobian matrix)**，其元素为 $J_{ij} = \frac{\partial x_i}{\partial \xi_j}$。矩阵 $(J^{-1})^T$ 的元素被称为**度量项 (metric terms)**。

这个公式是有限元方法的核心。它允许我们将物理空间中的[微分](@entry_id:158718)运算转换为参考单元上的[微分](@entry_id:158718)运算。具体操作如下：
1.  在[参考单元](@entry_id:168425)上，使用[微分矩阵](@entry_id:149870) $\mathcal{D}_{\xi}, \mathcal{D}_{\eta}$ 等计算参考梯度 $\nabla_{\boldsymbol{\xi}} \hat{u}$ 的节点值。
2.  在每个需要的点（通常是求积点）计算[雅可比矩阵](@entry_id:264467) $J$ 及其逆 $J^{-1}$。
3.  使用上述链式法则，通过[矩阵乘法](@entry_id:156035)得到物理梯度 $\nabla_{\boldsymbol{x}} u$ 的值。

### 与其他基的比较：[模态基](@entry_id:752055)视角

[节点基](@entry_id:752522)并非唯一的选择。另一大类是**[模态基](@entry_id:752055) (modal basis)**，通常由一组按某种规则（如次数）排序的[正交多项式](@entry_id:146918)构成，例如[勒让德多项式](@entry_id:141510)。这两种基在实现上有根本的权衡 [@problem_id:3402599] [@problem_id:3402622]。

关键的比较点之一是**[质量矩阵](@entry_id:177093) (mass matrix)** $M$，其定义为 $M_{ij} = \int_{\hat{K}} \varphi_i(\boldsymbol{x}) \varphi_j(\boldsymbol{x}) d\boldsymbol{x}$。

- 对于**[模态基](@entry_id:752055)**，如果选择了一组 $L^2$-正交的多项式（如[标准化](@entry_id:637219)的勒让德多项式），那么根据定义，其精确积分的[质量矩阵](@entry_id:177093) $M$ 是一个**对角矩阵**（甚至是单位矩阵）。这是一个巨大的计算优势，因为求解形如 $M\boldsymbol{u} = \boldsymbol{f}$ 的线性系统变得非常简单。然而，[模态基](@entry_id:752055)不具备直接的插值性质。将节点上的函数值转换为[模态系数](@entry_id:752057)需要求解一个（可能病态的）范德蒙[线性系统](@entry_id:147850)。

- 对于**[节点基](@entry_id:752522)**，精确积分的质量矩阵 $M$ 通常是**稠密的**。然而，可以通过**质量集总 (mass lumping)** 来获得一个对角的近似质量矩阵。这通常通过数值求积实现，即将求积点与[基函数](@entry_id:170178)节点重合。
    - 如果使用 $(N+1)$ 点的GL节点作为[基函数](@entry_id:170178)节点，并用相同的GL求积规则来计算[质量矩阵](@entry_id:177093)，由于GL求积对于 $2N+1$ 次多项式是精确的，而 $\ell_i \ell_j$ 的次数最多为 $2N$，所以求积是精确的。然而，由于[拉格朗日基](@entry_id:751105)函数非正交，精确的[质量矩阵](@entry_id:177093) $M$ 是稠密的，而通过质量集总得到的对角矩阵 $M^{(Q)}_{ij} = w_i \delta_{ij}$ 是对 $M$ 的一种近似。[@problem_id:3402599]。
    - 如果使用 $(N+1)$ 点的GLL节点，并用GLL求积规则，得到的[对角质量矩阵](@entry_id:173002) $M^{(Q)}$ 只是一个近似，因为GLL求积的精度（最高 $2N-1$ 次）不足以精确积分次数为 $2N$ 的项 $\ell_i \ell_j$ [@problem_id:3402599]。

此外，在从参考单元映射到物理单元时，如果映射是仿射的（雅可比矩阵 $J$ 为常数），正交[模态基](@entry_id:752055)的质量矩阵依然保持对角性，只是被 $J$ 缩放。但如果映射是弯曲的（$J$ 不为常数），质量矩阵就会失去对角性。

总结来说，[节点基](@entry_id:752522)以其插值简单性为代价，换来了稠密的[质量矩阵](@entry_id:177093)（尽管可以被集总）；而[模态基](@entry_id:752055)以其对角的[质量矩阵](@entry_id:177093)为优势，却牺牲了插值的直接性。现代[高阶方法](@entry_id:165413)常常在 nodal 和 modal 表示之间设计快速转换算法，以期兼得两者的优点。