## 引言
在微分几何中，切丛（Tangent Bundle）TM 是构建在任意光滑流形 M 之上的一个基本结构。它不仅仅是将 M 上每一点的切空间简单地汇集在一起，其本身更是一个拥有丰富内在几何和拓扑结构的流形。初学者往往将切丛视为一个抽象的“容器”，而忽略了它作为一个独立研究对象的深刻意义，以及它在连接几何、拓扑与物理学等不同分支中所扮演的关键桥梁角色。本文旨在填补这一认知空白，系统地揭示切丛的内在生命力。

本文将引导读者踏上一段探索切丛TM的旅程。我们将从最基本的定义出发，逐步构建起这个宏伟的几何大厦。
在第一章**“原理与机制”**中，我们将学习如何为切丛赋予光滑流形结构，并介绍在其上定义的核心工具，如向量场的垂直和水平提升、Sasaki度量以及典范辛形式。
随后，在第二章**“应用与跨学科联系”**中，我们将看到这些抽象的结构如何在具体问题中大放异彩，从描述经典力学中的测地流和带电粒子运动，到通过特征类揭示底流形的全局拓扑不变量。
最后，在第三章**“动手实践”**中，读者将有机会通过解决一系列精心挑选的计算问题，将理论知识转化为切实的几何直觉和分析能力。

通过这三个层次的深入探讨，读者将对切丛TM有一个全面而深刻的理解，认识到它不仅是现代几何的基石，更是通往更广阔数学与物理世界的门户。

## 原理与机制

继引言之后，本章旨在深入探讨切丛的内在结构与机制。我们将把切丛本身构建为一个光滑流形，并研究其上由底流形结构诱导而来的各种重要几何对象。这些结构，如垂直和水平提升、Sasaki度量和典范辛形式，不仅对理论研究至关重要，而且在几何分析、理论物理（特别是力学）和拓扑学中有着广泛的应用。

### 作为光滑流形的切丛

从概念上讲，一个 $n$ 维光滑流形 $M$ 的 **切丛**（Tangent Bundle），记作 $TM$，是其所有切空间的不交并集：
$$ TM = \bigsqcup_{p \in M} T_p M $$
$TM$ 中的一个元素是一个偶对 $(p, v)$，其中 $p$ 是 $M$ 上的一个点（称为基点），而 $v$ 是在点 $p$ 的切空间 $T_pM$ 中的一个切向量。有一个自然的 **典范投影**（canonical projection）映射 $\pi: TM \to M$，其定义为 $\pi(p, v) = p$。对于 $M$ 上的任意一点 $p$，原像 $\pi^{-1}(p)$ 正是切空间 $T_pM$，它被称为在点 $p$ 的 **纤维**（fiber）。

为了使 $TM$ 成为一个 $2n$ 维的光滑流形，我们需要为其赋予一个光滑结构。这通过利用 $M$ 上的坐标图册来完成。假设 $(U, \varphi)$ 是 $M$ 上的一个局部坐标图，其中 $\varphi: U \to \mathbb{R}^n$ 是一个同胚映射，其坐标函数为 $(x^1, \dots, x^n)$。在 $U$ 中的任意一点 $p$，其切空间 $T_pM$ 的一组基由坐标向量场 $\{\frac{\partial}{\partial x^1}|_p, \dots, \frac{\partial}{\partial x^n}|_p\}$ 给出。因此，任何切向量 $v \in T_pM$ 都可以唯一地表示为：
$$ v = \sum_{i=1}^n v^i \frac{\partial}{\partial x^i}\bigg|_p $$
其中 $v^i \in \mathbb{R}$ 是 $v$ 在这个基下的分量。

这启发我们为 $\pi^{-1}(U) \subset TM$ 上的一个点 $(p, v)$ 定义一个局部坐标系。该点的坐标可以由 $p$ 的坐标 $(x^1(p), \dots, x^n(p))$ 和 $v$ 的分量 $(v^1, \dots, v^n)$ 共同确定。这样，我们便得到了一个映射 $\Phi: \pi^{-1}(U) \to \mathbb{R}^n \times \mathbb{R}^n$，其定义为：
$$ \Phi(p, v) = (x^1(p), \dots, x^n(p), v^1, \dots, v^n) $$
这组坐标 $(x^1, \dots, x^n, v^1, \dots, v^n)$ 称为 $TM$ 上由 $M$ 的坐标图 $(U, \varphi)$ 诱导的 **自然坐标**（natural coordinates）。通过这种方式，$\pi^{-1}(U)$ 就同胚于 $U$ 在坐标下的像 $\varphi(U)$ 与 $\mathbb{R}^n$ 的笛卡尔积，即 $\pi^{-1}(U) \cong \varphi(U) \times \mathbb{R}^n$。这种结构被称为 **局部平凡化**（local trivialization），它表明切丛在局部上看起来像一个直积空间。

当两个坐标图 $(U, x^i)$ 和 $(\tilde{U}, \tilde{x}^j)$ 在 $M$ 上重叠时，我们需要检验 $TM$ 上诱导的坐标变换是否光滑。设一个点 $p \in U \cap \tilde{U}$。同一个切向量 $v \in T_pM$ 在两个坐标系下有不同的分量表示：
$$ v = \sum_i v^i \frac{\partial}{\partial x^i} = \sum_j \tilde{v}^j \frac{\partial}{\partial \tilde{x}^j} $$
根据链式法则，坐标基向量的变换关系为 $\frac{\partial}{\partial x^i} = \sum_j \frac{\partial \tilde{x}^j}{\partial x^i} \frac{\partial}{\partial \tilde{x}^j}$。由此可得新旧坐标分量的变换关系：
$$ \tilde{v}^j = \sum_i \frac{\partial \tilde{x}^j}{\partial x^i} v^i $$
这个关系式表明，切向量的分量是根据坐标变换的 **雅可比矩阵**（Jacobian matrix） $J = (\frac{\partial \tilde{x}^j}{\partial x^i})$ 进行线性变换的。

因此，在重叠区域 $\pi^{-1}(U \cap \tilde{U})$ 上，$TM$ 的坐标变换函数为：
$$ (\tilde{x}^1, \dots, \tilde{x}^n, \tilde{v}^1, \dots, \tilde{v}^n) = (\tilde{x}^1(x), \dots, \tilde{x}^n(x), \sum_i \frac{\partial \tilde{x}^1}{\partial x^i}v^i, \dots, \sum_i \frac{\partial \tilde{x}^n}{\partial x^i}v^i) $$
由于 $M$ 是光滑流形，坐标变换 $\tilde{x}(x)$ 是光滑的，其雅可比矩阵的元素（偏导数）也是光滑函数。因此，上述 $TM$ 上的坐标变换也是光滑的。这证实了 $TM$ 确实是一个 $2n$ 维的光滑流形。向量分量的变换规则是理解切丛上各种计算的基础 [@problem_id:1067057]。

一个经典且富有启发性的例子是2维球面 $S^2$ 的切丛 $TS^2$。我们可以使用两个球极投影坐标图覆盖 $S^2$。从北极 $N=(0,0,1)$ 投影得到坐标 $(u,v)$，从南极 $S=(0,0,-1)$ 投影得到坐标 $(U,V)$。在两个坐标图的重叠区域 $S^2 \setminus \{N,S\}$ 上，坐标变换函数 $\tau(u,v)=(U,V)$ 可以被显式计算出来，结果为 $\tau(u,v) = (\frac{u}{u^2+v^2}, \frac{v}{u^2+v^2})$。$TS^2$ 的转移函数就是这个坐标变换的雅可比矩阵。通过直接计算，可以得到该雅可比矩阵的[行列式](@entry_id:142978)为 $-\frac{1}{(u^2+v^2)^2}$ [@problem_id:3004547]。这个非平凡的转移函数清晰地表明了 $TS^2$ 虽然局部看起来像 $\mathbb{R}^4$，但其整体结构是扭曲的，不是一个简单的直积空间 $S^2 \times \mathbb{R}^2$。对 $TS^2$ 上不同坐标系下的切向量分量进行变换，本质上就是应用这个雅可比矩阵 [@problem_id:1066949]。

典范投影 $\pi: TM \to M$ 是一个光滑映射。其在 $TM$ 上一点 $u=(p,v)$ 的微分（或前推） $d\pi_u: T_u(TM) \to T_pM$ 将 $TM$ 的切向量（即 $T(TM)$ 中的元素）映射回 $M$ 的切向量。在自然坐标 $(x^i, v^i)$ 下，$T_u(TM)$ 的基是 $\{\frac{\partial}{\partial x^i}|_u, \frac{\partial}{\partial v^i}|_u\}$。由于 $\pi$ 的坐标表示为 $\pi(x^1, \dots, v^n) = (x^1, \dots, x^n)$，它的微分作用在基向量上为：
$$ d\pi_u\left(\frac{\partial}{\partial x^i}\bigg|_u\right) = \frac{\partial}{\partial x^i}\bigg|_p, \quad d\pi_u\left(\frac{\partial}{\partial v^i}\bigg|_u\right) = 0 $$
这意味着 $d\pi$ "保留"了基点方向的运动分量，而"遗忘"了纤维方向的运动分量 [@problem_id:1066910]。

### 切丛上的向量场：提升

流形 $M$ 上的几何结构可以被“提升”到其切丛 $TM$ 上。向量场的提升是其中最基本的操作，它提供了研究 $TM$ 几何的强大工具。$T_u(TM)$ 的切向量可以被分解为与纤维相切的“垂直”部分和与纤维“正交”的“水平”部分。

#### 垂直提升

对于 $TM$ 上的一点 $u=(p,v)$，其所在纤维 $T_pM$ 本身是一个向量空间，因此也是一个光滑子流形。在 $u$ 点沿纤维方向的切向量构成了 $T_u(TM)$ 的一个子空间，称为 **垂直子空间**（vertical subspace），记为 $V_u(TM)$。从微分的角度看，垂直子空间正是微分映射 $d\pi_u$ 的核：
$$ V_u(TM) = \ker(d\pi_u) = \text{span}\left\{\frac{\partial}{\partial v^1}\bigg|_u, \dots, \frac{\partial}{\partial v^n}\bigg|_u\right\} $$
$V_u(TM)$ 中的向量称为 **垂直向量**。

给定 $M$ 上的一个向量场 $X$，我们可以定义其在 $TM$ 上的 **垂直提升**（vertical lift）$X^V$。$X^V$ 是 $TM$ 上的一个向量场，在每一点 $u=(p,v)$，$X^V_u$ 都是一个垂直向量。具体而言，$X^V_u$ 可以被看作是 $X_p$ 在纤维 $T_pM$ 中的平行移动。在自然坐标中，如果 $X = \sum_i X^i(x) \frac{\partial}{\partial x^i}$，则其垂直提升的坐标表达式为：
$$ X^V = \sum_i X^i(x) \frac{\partial}{\partial v^i} $$
这个定义非常直观：$X$ 在 $M$ 上的 $i$-分量被用作 $X^V$ 在 $TM$ 上的 $v^i$-方向（即纤维方向）的分量。垂直提升的向量场只在纤维方向上作用，因此它对只依赖于基点坐标的函数（即从 $M$ 提升到 $TM$ 的函数）的作用为零。例如，考虑 $M$ 上的一个向量场 $X = y \frac{\partial}{\partial x} - x \frac{\partial}{\partial y}$，其垂直提升为 $X^V = y \frac{\partial}{\partial v_x} - x \frac{\partial}{\partial v_y}$。我们可以计算它对 $TM$ 上函数的作用，比如 $F = \alpha v_x^2 + \beta v_y^2 - \gamma (x v_y - y v_x)$，通过应用链式法则即可得到 $X^V(F)$ 的值 [@problem_id:1067031]。

#### 水平提升

为了定义一个与垂直子空间互补的 **水平子空间**（horizontal subspace）$H_u(TM)$，使得 $T_u(TM) = H_u(TM) \oplus V_u(TM)$，我们需要额外的结构。这个结构由 $M$ 上的一个 **仿射联络**（affine connection） $\nabla$ 提供。联络本质上定义了如何在流形上对向量场进行微分，并允许我们比较邻近点上的切向量，从而定义了“平行移动”的概念。

一旦有了联络，水平子空间 $H_u(TM)$ 就被定义为那些在投影到 $M$ 上时“保持水平”的切向量所构成的空间。利用这个水平/垂直分解，任何 $M$ 上的向量场 $X$ 都可以被唯一地提升为一个在 $TM$ 上处处水平的向量场，称为 **水平提升**（horizontal lift），记作 $X^H$。

如果联络 $\nabla$ 的克氏符（Christoffel symbols）为 $\Gamma^k_{ij}$，则 $X = \sum_i X^i(x) \frac{\partial}{\partial x^i}$ 的水平提升在自然坐标下的表达式为：
$$ X^H = \sum_i X^i(x) \frac{\partial}{\partial x^i} - \sum_{i,j,k} v^j \Gamma^k_{ij}(x) X^i(x) \frac{\partial}{\partial v^k} $$
这个表达式的第一部分 $X^i \frac{\partial}{\partial x^i}$ 确保了 $d\pi(X^H) = X$。第二部分是一个修正项，它是一个垂直向量，其作用是抵消掉沿 $X$ 方向移动时 $v$ 的“非水平”变化，从而确保 $X^H$ 保持在水平子空间中。例如，在具有标准圆度量的 $S^2$ 上，我们可以计算其 Levi-Civita 联络的克氏符，然后用上述公式得到方位角向量场 $\partial_\phi$ 的水平提升 $X^H$ 的具体坐标表达式，并用它来计算特定点上的作用 [@problem_id:1067084]。

#### 完全提升

除了垂直和水平提升，还有一种称为 **完全提升**（complete lift）或 **切向提升**（tangent lift）的构造，记为 $X^C$。如果 $X$ 在 $M$ 上生成一个流 $\phi_t$，那么 $X^C$ 就是这个流在 $TM$ 上的微分 $d\phi_t$ 所生成的向量场。在坐标中，它的表达式是：
$$ X^C = \sum_i X^i(x) \frac{\partial}{\partial x^i} + \sum_{i,j} v^j \frac{\partial X^i}{\partial x^j}(x) \frac{\partial}{\partial v^i} $$
这个定义不依赖于联络，是一种更具代数性质的构造。我们可以看到，完全提升同时包含了基点和纤维方向的分量。事实上，借助联络，完全提升可以被分解为水平和垂直部分之和：$X^C = X^H + (\nabla_v X)^V$。例如，对于 $\mathbb{R}^2$ 上的向量场 $X = y^2 \frac{\partial}{\partial x} + x \frac{\partial}{\partial y}$，我们可以通过上述公式直接计算其完全提升 $X^C$ 的表达式，并进一步研究其性质 [@problem_id:1067012]。

### 切丛上的典范结构

切丛 $TM$ 不仅仅是一个光滑流形，它还从底流形 $(M,g)$ 继承了一系列丰富的几何结构。

#### 刘维尔向量场

在任何切丛上，都存在一个典范的 **刘维尔向量场**（Liouville vector field），通常记为 $Z$。在自然坐标中，它的表达式非常简单：
$$ Z = \sum_i v^i \frac{\partial}{\partial v^i} $$
这个向量场在每一点 $u=(p,v)$ 都指向从纤维原点 $0_p$ 到 $v$ 的方向。因此，$Z$ 生成了沿纤维的伸缩变换 $t \mapsto (p, e^t v)$。刘维尔向量场在辛几何和哈密顿力学中扮演着核心角色，它与测地流密切相关。例如，动能函数 $E = \frac{1}{2}g_{ij}v^i v^j$ 关于 $Z$ 的作用 $Z(E) = \sum_k v^k \frac{\partial E}{\partial v^k} = g_{ij}v^i v^j = 2E$ [@problem_id:1067033]。

#### Sasaki 度量

如果 $(M,g)$ 是一个黎曼流形，我们可以利用水平/垂直分解在 $TM$ 上定义一个自然的黎曼度量，称为 **Sasaki 度量** $g_S$。其定义如下：对于 $M$ 上的任意两个向量场 $X, Y$，它们的提升在 $TM$ 上的度量关系为：
1.  $g_S(X^H, Y^H) = g(X, Y) \circ \pi$
2.  $g_S(X^V, Y^V) = g(X, Y) \circ \pi$
3.  $g_S(X^H, Y^V) = 0$

这一定义表明，水平子空间和垂直子空间在 Sasaki 度量下是相互正交的。并且，水平提升和垂直提升都是等距嵌入（在纤维方向上）。这使得 $TM$ 本身也成为了一个黎曼流形。由于黎曼联络（Levi-Civita联络）对于平坦空间（如 $\mathbb{R}^n$ 或平坦环面 $T^n$）的克氏符为零，此时水平提升 $X^H$ 就简化为 $X^i \frac{\partial}{\partial x^i}$。在这种情况下，计算 Sasaki 范数变得尤为简单。例如，对于一个由 $W = A \cdot X^H + B \cdot Y^V$ 构成的向量场，其 Sasaki 范数的平方为 $\|W\|_{g_S}^2 = A^2 g(X,X) + B^2 g(Y,Y)$ [@problem_id:1067037]。

#### 典范辛形式

切丛 $TM$ 还具有一个不依赖于度量的典范 **辛结构**（symplectic structure）。这个结构由 **典范 1-形式**（canonical 1-form）$\Theta$（也称为刘维尔形式或联络形式）导出。给定黎曼度量 $g$，$\Theta$ 在点 $u=(p,v) \in TM$ 对一个向量 $A \in T_u(TM)$ 的作用定义为：
$$ \Theta_u(A) = g_p(v, d\pi_u(A)) $$
在自然坐标中，$\Theta = \sum_{i,j} g_{ij}(x) v^i dx^j$。

**典范辛形式**（canonical symplectic form）$\Omega$ 定义为 $\Theta$ 的外微分的相反数：$\Omega = -d\Theta$。这个 2-形式是非退化的、闭的，因此它将 $TM$ 变成了一个辛流形。在物理学中，若将 $M$ 视为位形空间，则 $TM$ 就是相空间，动能 $E$ 就是哈密顿量，而测地线方程就可以表示为与 $\Omega$ 相关的哈密顿方程。

辛形式 $\Omega$ 与水平/垂直分解有着优美的关系。可以证明：
$$ \Omega(X^V, Y^V) = 0, \quad \Omega(X^H, Y^V) = g(X, Y) \circ \pi $$
值得注意的是，两个水平提升的配对 $\Omega(X^H, Y^H)$ 通常不为零，它与底流形的曲率张量 $R$ 有关。以上关系表明，垂直子空间是拉格朗日的，而辛形式在水平和垂直向量间的配对则能恢复底流形的度量。这个性质非常深刻，它将黎曼几何（通过 $g$ 和联络定义的 $H, V$）与辛几何（通过 $\Omega$）联系在一起。在庞加莱上半平面 $\mathbb{H}^2$ 这样的具体例子中，我们可以显式计算克氏符和各个提升，并验证这个美妙的公式 [@problem_id:1067080]。

### 二阶切丛与典范对合

最后，我们简要介绍二阶结构。由于 $TM$ 本身是一个光滑流形，我们可以考虑它的切丛，即 **二阶切丛**（second tangent bundle）$T(TM)$。$T(TM)$ 中的一个元素是 $TM$ 中一条曲线的切向量。如果 $TM$ 的自然坐标为 $(x^i, v^i)$，那么 $T(TM)$ 的自然坐标可以记为 $(x^i, v^i; \dot{x}^i, \dot{v}^i)$。

在 $T(TM)$ 上存在一个非常重要的自然对合（involution），称为 **典范对合**（canonical flip map），记为 $\kappa: T(TM) \to T(TM)$。它的作用是交换基点速度和纤维向量分量：
$$ \kappa: (x^i, v^i; \dot{x}^i, \dot{v}^i) \mapsto (x^i, \dot{x}^i; v^i, \dot{v}^i) $$
这个映射的几何意义与二阶偏导数的对称性（Schwarz 定理）密切相关。它在构造高阶拉格朗日力学和芬斯勒几何中起着基础性作用。我们可以通过考虑 $TM$ 中一条具体曲线（例如一条螺旋线上的旋转向量场）的切向量，来具体计算典范对合的作用 [@problem_id:1066926]。

综上所述，切丛不仅是汇集所有切向量的简单集合，它本身就是一个拥有丰富几何结构的流形。通过垂直、水平和完全提升，我们可以将底流形上的分析问题提升到切丛上进行研究。而 Sasaki 度量和典范辛形式等内在结构，则为测地流、哈密顿力学和几何量子化等领域提供了坚实的数学框架。