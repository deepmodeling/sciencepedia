## 引言
在微分几何的世界中，对[曲面](@entry_id:267450)的研究分为两个相互关联的视角：内在几何与外在几何。前者关注[曲面](@entry_id:267450)自身的度量属性，如同一个二维生物只能感知其所在的世界；而后者则研究[曲面](@entry_id:267450)如何嵌入到更高维度的空间（如我们熟悉的三维空间）中并呈现出不同的弯曲形态。本文将从内在几何转向外在几何，解决一个核心问题：我们如何精确地描述和量化一个[曲面](@entry_id:267450)在空间中的弯曲方式？

为了回答这个问题，我们将引入一个强大而优雅的数学工具——**[Weingarten映射](@entry_id:271773)**，也称为[形状算子](@entry_id:264703)。这个工具构成了理解外在曲率的基石。在接下来的内容中，您将踏上一段从基本原理到前沿应用的探索之旅。第一章“**原理与机制**”将详细阐述[Weingarten映射](@entry_id:271773)的定义，揭示其与主曲率、[高斯曲率](@entry_id:149725)和[平均曲率](@entry_id:162147)的深刻联系。第二章“**应用与跨学科联系**”将展示这一理论工具如何超越纯数学，在物理学、工程学和[材料科学](@entry_id:152226)等领域中发挥关键作用。最后，在“**动手实践**”部分，您将通过具体的计算练习，将抽象的理论转化为解决实际问题的能力。这趟旅程将为您揭示隐藏在[曲面](@entry_id:267450)形态背后的数学结构。

## 原理与机制

继前一章对[曲面](@entry_id:267450)的内在几何（由[第一基本形式](@entry_id:274022)决定）进行探讨之后，我们现在将目光转向其外在几何，即[曲面](@entry_id:267450)如何嵌入到周围的三维欧几里得空间 $\mathbb{R}^3$ 中并发生弯曲。理解这种弯曲的核心在于一个关键的数学工具——**Weingarten 映射**（Weingarten map），也常被称为**形状算子**（shape operator）。本章将系统地阐述 Weingarten 映射的定义、性质及其在量化[曲面](@entry_id:267450)弯曲中的核心作用。

### 外在曲率的定义：形状算子（Weingarten 映射）

想象一个光滑[曲面](@entry_id:267450) $S \subset \mathbb{R}^3$。在[曲面](@entry_id:267450)上任意一点 $p$，都存在一个与之相切的平面，称为**切平面** $T_pS$。为了描述[曲面](@entry_id:267450)在 $p$ 点附近的弯曲情况，一个直观的方法是考察该点[法向量](@entry_id:264185)的变化。我们可以在 $p$ 点附近为[曲面](@entry_id:267450)选择一个光滑的[单位法向量](@entry_id:178851)场 $\mathbf{n}$，它在每一点都与切平面正交。

当我们沿着[曲面](@entry_id:267450)上某一切方向 $\mathbf{v} \in T_pS$ 移动时，[单位法向量](@entry_id:178851) $\mathbf{n}$ 也会随之改变。这种变化的速率由[方向导数](@entry_id:189133) $\nabla_{\mathbf{v}}\mathbf{n}$ 给出。一个至关重要的事实是，这个导数向量 $\nabla_{\mathbf{v}}\mathbf{n}$ 本身也位于[切平面](@entry_id:136914) $T_pS$ 中。我们可以通过一个简单的论证来证明这一点：由于 $\mathbf{n}$ 是[单位向量](@entry_id:165907)，$\langle \mathbf{n}, \mathbf{n} \rangle = 1$。对这个等式沿着方向 $\mathbf{v}$求导，根据[乘法法则](@entry_id:144424)得到：
$$
\nabla_{\mathbf{v}}\langle \mathbf{n}, \mathbf{n} \rangle = \langle \nabla_{\mathbf{v}}\mathbf{n}, \mathbf{n} \rangle + \langle \mathbf{n}, \nabla_{\mathbf{v}}\mathbf{n} \rangle = 2\langle \nabla_{\mathbf{v}}\mathbf{n}, \mathbf{n} \rangle = 0
$$
这表明向量 $\nabla_{\mathbf{v}}\mathbf{n}$ 与 $\mathbf{n}$ 正交。由于 $T_pS$ 正是 $\mathbb{R}^3$ 中与 $\mathbf{n}(p)$ 正交的二维[子空间](@entry_id:150286)，因此 $\nabla_{\mathbf{v}}\mathbf{n}$ 必然属于 $T_pS$。

既然对于每一个切向量 $\mathbf{v} \in T_pS$，向量 $\nabla_{\mathbf{v}}\mathbf{n}$ 都是 $T_pS$ 中的一个确定向量，这便定义了一个从切平面到其自身的线性映射。我们将其定义为 **Weingarten 映射** $W_p: T_pS \to T_pS$，其表达式为：
$$
W_p(\mathbf{v}) = - \nabla_{\mathbf{v}} \mathbf{n}
$$
这里的负号是一个数学约定，它使得标[准球](@entry_id:169696)面（向外指向法向量）的曲率为正，符合我们的几何直观。Weingarten 映射 $W_p$ 捕捉了在 $p$ 点沿不同方向移动时[法向量](@entry_id:264185)变化的全部信息，因此它完美地刻画了[曲面](@entry_id:267450)在该点的外在弯曲形态，故而得名“[形状算子](@entry_id:264703)”。

Weingarten 映射的定义直接依赖于[法向量场](@entry_id:268853)的选择。如果我们反转[曲面](@entry_id:267450)的定向，即用[法向量场](@entry_id:268853) $\mathbf{n}' = -\mathbf{n}$ 替代原来的 $\mathbf{n}$，那么新的 Weingarten 映射 $W'$ 将会如何变化？根据导数的线性性质，我们有 $d\mathbf{n}' = d(-\mathbf{n}) = -d\mathbf{n}$。因此，新的 Weingarten 映射 $W'$ 满足：
$$
W'(\mathbf{v}) = -d\mathbf{n}'(\mathbf{v}) = -(-d\mathbf{n}(\mathbf{v})) = d\mathbf{n}(\mathbf{v}) = -W(\mathbf{v})
$$
这意味着 $W' = -W$。也就是说，反转[曲面](@entry_id:267450)的定向会使 Weingarten 映射、所有[主曲率](@entry_id:270598)以及平均曲率都变号，而[高斯曲率](@entry_id:149725)保持不变 [@problem_id:1510685]。

### Weingarten 映射的矩阵表示

为了进行具体计算，我们需要在选定的基底下将 Weingarten 映射表示为矩阵。设[曲面](@entry_id:267450)由[参数化](@entry_id:272587) $\mathbf{r}(u, v)$ 给出，则在任意一点，切平面由基底 $\{\mathbf{r}_u, \mathbf{r}_v\}$ 张成，其中 $\mathbf{r}_u = \frac{\partial \mathbf{r}}{\partial u}$，$\mathbf{r}_v = \frac{\partial \mathbf{r}}{\partial v}$。

根据 Weingarten 映射的定义，我们可以计算它在[基向量](@entry_id:199546)上的作用：$W(\mathbf{r}_u) = -\mathbf{n}_u$ 和 $W(\mathbf{r}_v) = -\mathbf{n}_v$。由于 $W(\mathbf{r}_u)$ 和 $W(\mathbf{r}_v)$ 都是切向量，它们可以表示为基底 $\{\mathbf{r}_u, \mathbf{r}_v\}$ 的[线性组合](@entry_id:154743)。这些关系式被称为 **Weingarten 方程** [@problem_id:1510681]：
$$
\begin{align*}
-\mathbf{n}_u = W^1_1 \mathbf{r}_u + W^2_1 \mathbf{r}_v \\
-\mathbf{n}_v = W^1_2 \mathbf{r}_u + W^2_2 \mathbf{r}_v
\end{align*}
$$
系数 $W^i_j$ 构成了 Weingarten 映射在基底 $\{\mathbf{r}_u, \mathbf{r}_v\}$ 下的矩阵 $[W]$：
$$
[W] = \begin{pmatrix} W^1_1  W^1_2 \\ W^2_1  W^2_2 \end{pmatrix}
$$
这些系数可以通过[求解线性方程组](@entry_id:169069)得到，但更系统的方法是利用[曲面](@entry_id:267450)的[第一和第二基本形式](@entry_id:192112)。[第一基本形式](@entry_id:274022)的矩阵 $G = (g_{ij})$ 和[第二基本形式](@entry_id:161454)的矩阵 $B = (b_{ij})$ 分别由以下[内积](@entry_id:158127)定义：
$$
g_{ij} = \langle \mathbf{r}_i, \mathbf{r}_j \rangle, \quad b_{ij} = \langle -\mathbf{n}_i, \mathbf{r}_j \rangle = \langle \mathbf{n}, \mathbf{r}_{ij} \rangle
$$
其中 $i,j$ 可取 $u$ 或 $v$。可以证明，Weingarten 映射的矩阵 $[W]$ 与这两个基本形式的矩阵之间存在一个优美的关系：
$$
[W] = G^{-1}B = \begin{pmatrix} g_{11}  g_{12} \\ g_{21}  g_{22} \end{pmatrix}^{-1} \begin{pmatrix} b_{11}  b_{12} \\ b_{21}  b_{22} \end{pmatrix}
$$
在一个特殊的点或对于一个特殊的参数化，如果[切向量](@entry_id:265494)基底 $\{\mathbf{r}_u, \mathbf{r}_v\}$ 是标准正交的，那么[第一基本形式](@entry_id:274022)的矩阵就是单位矩阵 $G=I$。在这种情况下，Weingarten 映射的矩阵就直接等于第二基本形式的矩阵，即 $[W] = B$ [@problem_id:1510655]。

例如，考虑一个[椭圆抛物面](@entry_id:268068) $S$，其[参数化](@entry_id:272587)为 $\mathbf{x}(u,v) = (u, v, au^2+bv^2)$。我们可以通过直接计算来确定 Weingarten 映射作用在一个[基向量](@entry_id:199546)上的结果。首先计算切向量 $\mathbf{x}_u = (1, 0, 2au)$ 和[单位法向量](@entry_id:178851) $\mathbf{n}$。然后，我们计算[法向量](@entry_id:264185)对 $u$ 的偏导数 $\frac{\partial \mathbf{n}}{\partial u}$。根据定义，$W_p(\mathbf{x}_u) = - \frac{\partial \mathbf{n}}{\partial u}$。这是一个直接但通常比较繁琐的计算，它会给出一个依赖于 $(u_0, v_0)$ 的具体向量，该向量位于点 $p$ 的[切平面](@entry_id:136914)内 [@problem_id:1510648]。

### [特征值与特征向量](@entry_id:748836)：[主曲率](@entry_id:270598)与[主方向](@entry_id:276187)

Weingarten 映射 $W_p$ 是一个定义在二维[内积空间](@entry_id:271570)（[切平面](@entry_id:136914) $T_pS$）上的[线性算子](@entry_id:149003)。一个深刻的性质是，它是**自伴**（self-adjoint）的，也即对称的。这意味着对于任意两个切向量 $\mathbf{u}, \mathbf{v} \in T_pS$，都满足：
$$
\langle W_p(\mathbf{u}), \mathbf{v} \rangle = \langle \mathbf{u}, W_p(\mathbf{v}) \rangle
$$
这里的[内积](@entry_id:158127) $\langle \cdot, \cdot \rangle$ 是由[第一基本形式](@entry_id:274022)定义的。根据线性代数中的[谱定理](@entry_id:136620)，任何自伴算子都存在一个由标准正交的[特征向量](@entry_id:151813)构成的基底，并且其[特征值](@entry_id:154894)都是实数。

Weingarten 映射的[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)具有非凡的几何意义。为了理解这一点，我们首先引入**[法曲率](@entry_id:270966)**（normal curvature）的概念。对于切平面中的一个[单位向量](@entry_id:165907) $\mathbf{v}$，它定义了一个方向。包含 $\mathbf{v}$ 和法向量 $\mathbf{n}$ 的平面与[曲面](@entry_id:267450)相交，形成一条[平面曲线](@entry_id:271353)，称为**法截线**。这条法截线在点 $p$ 的曲率（带符号）就是[曲面](@entry_id:267450)在该方向的[法曲率](@entry_id:270966)，记为 $k_n(\mathbf{v})$。

[法曲率](@entry_id:270966)与 Weingarten 映射之间存在一个基本关系 [@problem_id:1510670]：
$$
k_n(\mathbf{v}) = \langle W_p(\mathbf{v}), \mathbf{v} \rangle
$$
这个公式也被称为**[欧拉曲率公式](@entry_id:637477)**。它表明，在给定点 $p$，沿任何方向的[法曲率](@entry_id:270966)都可以通过[形状算子](@entry_id:264703) $W_p$ 计算得到。

现在，让我们考虑 $k_n(\mathbf{v})$ 在所有单位方向 $\mathbf{v}$ 上的[极值](@entry_id:145933)问题。根据瑞利商的性质，二次型 $\langle W_p(\mathbf{v}), \mathbf{v} \rangle$ 的[极值](@entry_id:145933)恰好在 $\mathbf{v}$ 是 $W_p$ 的[特征向量](@entry_id:151813)时取到，并且极值的大小就是对应的[特征值](@entry_id:154894)。因此，我们得出结论 [@problem_id:1510665] [@problem_id:1510698]：
- Weingarten 映射的**[特征向量](@entry_id:151813)**所指出的方向，是[法曲率](@entry_id:270966)取极大值和极小值的方向。这些方向被称为**[主方向](@entry_id:276187)**（principal directions）。
- Weingarten 映射的**[特征值](@entry_id:154894)**，就是对应主方向上的[法曲率](@entry_id:270966)，它们被称为**主曲率**（principal curvatures），通常记为 $k_1$ 和 $k_2$。

因为 $W_p$ 是自伴的，如果两个[主曲率](@entry_id:270598) $k_1$ 和 $k_2$ 不相等，那么对应的两个主方向必定是正交的 [@problem_id:1510677]。这意味着在[曲面](@entry_id:267450)的每一点（除非是[脐点](@entry_id:260926)，即 $k_1=k_2$ 的点），都存在两个相互垂直的方向，[曲面](@entry_id:267450)在其中一个方向上弯曲得最厉害，在另一个方向上弯曲得最平缓。

例如，对于由 $z = \frac{1}{2}(\alpha x^2 + \beta y^2)$ 定义的[曲面](@entry_id:267450)，在原点 $(0,0,0)$ 处，切平面是 $xy$ 平面，Weingarten 映射的矩阵恰好是对角阵 $\begin{pmatrix} \alpha  0 \\ 0  \beta \end{pmatrix}$。因此，[主曲率](@entry_id:270598)直接就是 $k_1 = \alpha$ 和 $k_2 = \beta$，主方向就是 $x$ 轴和 $y$ 轴方向 [@problem_id:1510657]。对于更复杂的[曲面](@entry_id:267450)，如[双曲抛物面](@entry_id:275753)（马鞍面）$z=uv$，在原点的[主方向](@entry_id:276187)则可能是沿对角线方向，如 $\vec{w}_1 = (1, 1, 0)$ 和 $\vec{w}_2 = (1, -1, 0)$ [@problem_id:1510677]。

### 曲率[不变量](@entry_id:148850)：高斯曲率与[平均曲率](@entry_id:162147)

尽管 Weingarten 映射本身依赖于[坐标基](@entry_id:270149)底的选择，但它的某些属性是内在的、不随[坐标变换](@entry_id:172727)而改变的。最重要的两个[不变量](@entry_id:148850)是它的[行列式](@entry_id:142978)和迹。这两个量定义了[曲面](@entry_id:267450)几何中两个最核心的曲率度量。

- **[高斯曲率](@entry_id:149725)**（Gaussian curvature）$K$ 定义为 Weingarten 映射的[行列式](@entry_id:142978)：
  $$
  K = \det(W_p)
  $$
- **[平均曲率](@entry_id:162147)**（mean curvature）$H$ 定义为 Weingarten 映射的迹的一半：
  $$
  H = \frac{1}{2}\text{tr}(W_p)
  $$

由于[行列式](@entry_id:142978)是[特征值](@entry_id:154894)的乘积，迹是[特征值](@entry_id:154894)的和，这两个曲率也可以用主曲率表示：
$$
K = k_1 k_2, \quad H = \frac{1}{2}(k_1 + k_2)
$$
这种表示方式提供了对[高斯曲率](@entry_id:149725)和[平均曲率](@entry_id:162147)的直观理解。[高斯曲率](@entry_id:149725) $K$ 的符号决定了[曲面](@entry_id:267450)的局部形状：$K > 0$ 表示局部是凸起的（如球面），$K  0$ 表示局部是鞍形的（如双曲抛物面），$K=0$ 表示至少有一个主方向是平的（如圆柱面）。[平均曲率](@entry_id:162147) $H$ 则衡量了[曲面](@entry_id:267450)在一点附近的“平均弯曲程度”。$H=0$ 的[曲面](@entry_id:267450)称为**[极小曲面](@entry_id:157732)**，肥皂膜就是其物理实现。

我们可以通过计算[第一和第二基本形式](@entry_id:192112)的系数，来得到 $K$ 和 $H$ 的一般表达式：
$$
K = \frac{LN - M^2}{EG - F^2}, \quad H = \frac{EN - 2FM + GL}{2(EG - F^2)}
$$
其中 $E, F, G$ 是[第一基本形式](@entry_id:274022)的系数，$L, M, N$ 是[第二基本形式](@entry_id:161454)的系数。利用这些公式，我们可以为具体的[参数化曲面](@entry_id:181980)计算其高斯曲率和[平均曲率](@entry_id:162147) [@problem_id:1510693]。

值得一提的是，高斯的天才发现——**[绝妙定理](@entry_id:159067)**（Theorema Egregium）——表明，尽管 $W_p$, $H$, $k_1, k_2$ 都是外在量（依赖于[曲面](@entry_id:267450)在 $\mathbb{R}^3$ 中的嵌入方式），但它们的组合 $K = k_1 k_2$ 竟然是一个内在量，它完全由[第一基本形式](@entry_id:274022)（即[曲面](@entry_id:267450)上的距离测量）确定。这意味着生活在[曲面](@entry_id:267450)内的二维生物无需参考外部空间就能测量出[高斯曲率](@entry_id:149725)。

### 高等专题：Codazzi-Mainardi 方程

我们可能会问：是否任意给定一个[第一基本形式](@entry_id:274022)（度量张量 $g_{ij}$）和一个对称的[第二基本形式](@entry_id:161454)（张量 $b_{ij}$），我们总能找到一个嵌入在 $\mathbb{R}^3$ 中的[曲面](@entry_id:267450)，使其具有这两个基本形式？答案是否定的。这两个形式必须满足一定的[相容性条件](@entry_id:637057)，这些条件被称为 **Codazzi-Mainardi 方程**。

这些方程本质上是对 Weingarten 映射（或第二基本形式）的[协变导数](@entry_id:152476)施加的约束。使用张量记法，并引入 Levi-Civita 联络的[协变导数](@entry_id:152476) $\nabla$，Weingarten 映射可以看作一个 (1,1)-张量 $W^i_j = g^{ik}b_{kj}$。Codazzi-Mainardi 方程可以简洁地表述为：
$$
\nabla_j W^i_k - \nabla_k W^i_j = 0
$$
或者等价地，第二基本形式的协变导数具有对称性：$\nabla_k b_{ij} = \nabla_j b_{ik}$。

这个方程的几何意义是，Weingarten 映射的变化方式必须与[曲面](@entry_id:267450)的内在几何（由 $g_{ij}$ 及其 Christoffel 符号 $\Gamma^i_{jk}$ 决定）相容。如果这个条件不满足，那么就不存在一个光滑的嵌入能同时实现给定的[第一和第二基本形式](@entry_id:192112)。

我们可以通过一个假设的例子来理解这一点 [@problem_id:1510659]。考虑一个由极坐标 $(r, \theta)$ 参数化的[二维流形](@entry_id:188198)，其度量为 $g_{rr}=1, g_{\theta\theta}=r^2$（即平坦的 $\mathbb{R}^2$）。假设我们虚构了一个第二基本形式，其分量为 $\tilde{K}_{rr}=0, \tilde{K}_{\theta\theta}=0, \tilde{K}_{r\theta} = A r^3$。通过计算，可以发现对应的张量 $C^i_{jk} = \nabla_j \tilde{W}^i_k - \nabla_k \tilde{W}^i_j$ 的分量 $C^r_{r\theta}$ 并不为零，而是等于 $4Ar^2$。由于 Codazzi-Mainardi 方程没有被满足，我们可以断定，在三维[欧几里得空间](@entry_id:138052)中，不存在任何[曲面](@entry_id:267450)同时具有平面度量和这样一个假设的[第二基本形式](@entry_id:161454)。这彰显了 Codazzi-Mainardi 方程作为[曲面](@entry_id:267450)存在性“[可积性](@entry_id:142415)条件”的深刻作用，它与[高斯方程](@entry_id:192573)一起构成了[曲面论](@entry_id:273972)的基本方程。