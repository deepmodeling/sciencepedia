## 引言
在微分几何中，[切丛](@entry_id:161294)（Tangent Bundle）TM 是构建在任意光滑流形 M 之上的一个基本结构。它不仅仅是将 M 上每一点的[切空间](@entry_id:199137)简单地汇集在一起，其本身更是一个拥有丰富内在几何和拓扑结构的[流形](@entry_id:153038)。初学者往往将切丛视为一个抽象的“容器”，而忽略了它作为一个独立研究对象的深刻意义，以及它在连接几何、拓扑与物理学等不同分支中所扮演的关键桥梁角色。本文旨在填补这一认知空白，系统地揭示切丛的内在生命力。

本文将引导读者踏上一段探索切丛TM的旅程。我们将从最基本的定义出发，逐步构建起这个宏伟的几何大厦。
在第一章**“原理与机制”**中，我们将学习如何为切丛赋予[光滑流形](@entry_id:160799)结构，并介绍在其上定义的核心工具，如向量场的垂[直和](@entry_id:156782)[水平提升](@entry_id:160651)、[Sasaki度量](@entry_id:160971)以及[典范辛形式](@entry_id:180641)。
随后，在第二章**“应用与跨学科联系”**中，我们将看到这些抽象的结构如何在具体问题中大放异彩，从描述经典力学中的[测地流](@entry_id:270369)和[带电粒子运动](@entry_id:262424)，到通过特征类揭示底[流形](@entry_id:153038)的全局拓扑不变量。
最后，在第三章**“动手实践”**中，读者将有机会通过解决一系列精心挑选的计算问题，将理论知识转化为切实的几何直觉和分析能力。

通过这三个层次的深入探讨，读者将对[切丛](@entry_id:161294)TM有一个全面而深刻的理解，认识到它不仅是现代几何的基石，更是通往更广阔数学与物理世界的门户。

## 原理与机制

继引言之后，本章旨在深入探讨[切丛](@entry_id:161294)的内在结构与机制。我们将把[切丛](@entry_id:161294)本身构建为一个[光滑流形](@entry_id:160799)，并研究其上由底[流形](@entry_id:153038)结构诱导而来的各种重要几何对象。这些结构，如垂[直和](@entry_id:156782)[水平提升](@entry_id:160651)、[Sasaki度量](@entry_id:160971)和[典范辛形式](@entry_id:180641)，不仅对理论研究至关重要，而且在几何分析、理论物理（特别是力学）和拓扑学中有着广泛的应用。

### 作为[光滑流形](@entry_id:160799)的[切丛](@entry_id:161294)

从概念上讲，一个 $n$ 维[光滑流形](@entry_id:160799) $M$ 的 **[切丛](@entry_id:161294)**（Tangent Bundle），记作 $TM$，是其所有切空间的不交并集：
$$ TM = \bigsqcup_{p \in M} T_p M $$
$TM$ 中的一个元素是一个偶对 $(p, v)$，其中 $p$ 是 $M$ 上的一个点（称为基点），而 $v$ 是在点 $p$ 的[切空间](@entry_id:199137) $T_pM$ 中的一个[切向量](@entry_id:265494)。有一个自然的 **典范投影**（canonical projection）映射 $\pi: TM \to M$，其定义为 $\pi(p, v) = p$。对于 $M$ 上的任意一点 $p$，[原像](@entry_id:150899) $\pi^{-1}(p)$ 正是切空间 $T_pM$，它被称为在点 $p$ 的 **纤维**（fiber）。

为了使 $TM$ 成为一个 $2n$ 维的[光滑流形](@entry_id:160799)，我们需要为其赋予一个[光滑结构](@entry_id:159394)。这通过利用 $M$ 上的[坐标图](@entry_id:156506)册来完成。假设 $(U, \varphi)$ 是 $M$ 上的一个[局部坐标](@entry_id:181200)图，其中 $\varphi: U \to \mathbb{R}^n$ 是一个同胚映射，其坐标函数为 $(x^1, \dots, x^n)$。在 $U$ 中的任意一点 $p$，其切空间 $T_pM$ 的一组基由[坐标向量](@entry_id:153319)场 $\{\frac{\partial}{\partial x^1}|_p, \dots, \frac{\partial}{\partial x^n}|_p\}$ 给出。因此，任何切向量 $v \in T_pM$ 都可以唯一地表示为：
$$ v = \sum_{i=1}^n v^i \frac{\partial}{\partial x^i}\bigg|_p $$
其中 $v^i \in \mathbb{R}$ 是 $v$ 在这个基下的分量。

这启发我们为 $\pi^{-1}(U) \subset TM$ 上的一个点 $(p, v)$ 定义一个局部坐标系。该点的坐标可以由 $p$ 的坐标 $(x^1(p), \dots, x^n(p))$ 和 $v$ 的分量 $(v^1, \dots, v^n)$ 共同确定。这样，我们便得到了一个映射 $\Phi: \pi^{-1}(U) \to \mathbb{R}^n \times \mathbb{R}^n$，其定义为：
$$ \Phi(p, v) = (x^1(p), \dots, x^n(p), v^1, \dots, v^n) $$
这组坐标 $(x^1, \dots, x^n, v^1, \dots, v^n)$ 称为 $TM$ 上由 $M$ 的[坐标图](@entry_id:156506) $(U, \varphi)$ 诱导的 **自然坐标**（natural coordinates）。通过这种方式，$\pi^{-1}(U)$ 就同胚于 $U$ 在坐标下的像 $\varphi(U)$ 与 $\mathbb{R}^n$ 的[笛卡尔积](@entry_id:154642)，即 $\pi^{-1}(U) \cong \varphi(U) \times \mathbb{R}^n$。这种结构被称为 **[局部平凡化](@entry_id:267993)**（local trivialization），它表明[切丛](@entry_id:161294)在局部上看起来像一个直[积空间](@entry_id:151693)。

当两个[坐标图](@entry_id:156506) $(U, x^i)$ 和 $(\tilde{U}, \tilde{x}^j)$ 在 $M$ 上重叠时，我们需要检验 $TM$ 上诱导的[坐标变换](@entry_id:172727)是否光滑。设一个点 $p \in U \cap \tilde{U}$。同一个[切向量](@entry_id:265494) $v \in T_pM$ 在两个[坐标系](@entry_id:156346)下有不同的分量表示：
$$ v = \sum_i v^i \frac{\partial}{\partial x^i} = \sum_j \tilde{v}^j \frac{\partial}{\partial \tilde{x}^j} $$
根据链式法则，[坐标基](@entry_id:270149)向量的变换关系为 $\frac{\partial}{\partial x^i} = \sum_j \frac{\partial \tilde{x}^j}{\partial x^i} \frac{\partial}{\partial \tilde{x}^j}$。由此可得新旧坐标分量的变换关系：
$$ \tilde{v}^j = \sum_i \frac{\partial \tilde{x}^j}{\partial x^i} v^i $$
这个关系式表明，切向量的分量是根据坐标变换的 **[雅可比矩阵](@entry_id:264467)**（Jacobian matrix） $J = (\frac{\partial \tilde{x}^j}{\partial x^i})$ 进行[线性变换](@entry_id:149133)的。

因此，在重叠区域 $\pi^{-1}(U \cap \tilde{U})$ 上，$TM$ 的[坐标变换](@entry_id:172727)函数为：
$$ (\tilde{x}^1, \dots, \tilde{x}^n, \tilde{v}^1, \dots, \tilde{v}^n) = (\tilde{x}^1(x), \dots, \tilde{x}^n(x), \sum_i \frac{\partial \tilde{x}^1}{\partial x^i}v^i, \dots, \sum_i \frac{\partial \tilde{x}^n}{\partial x^i}v^i) $$
由于 $M$ 是光滑流形，[坐标变换](@entry_id:172727) $\tilde{x}(x)$ 是光滑的，其[雅可比矩阵](@entry_id:264467)的元素（偏导数）也是光滑函数。因此，上述 $TM$ 上的坐标变换也是光滑的。这证实了 $TM$ 确实是一个 $2n$ 维的光滑流形。向量分量的变换规则是理解切丛上各种计算的基础 [@problem_id:1067057]。

一个经典且富有启发性的例子是2维球面 $S^2$ 的切丛 $TS^2$。我们可以使用两个球极投影[坐标图](@entry_id:156506)覆盖 $S^2$。从北极 $N=(0,0,1)$ 投影得到坐标 $(u,v)$，从南极 $S=(0,0,-1)$ 投影得到坐标 $(U,V)$。在两个[坐标图](@entry_id:156506)的重叠区域 $S^2 \setminus \{N,S\}$ 上，坐标变换函数 $\tau(u,v)=(U,V)$ 可以被显式计算出来，结果为 $\tau(u,v) = (\frac{u}{u^2+v^2}, \frac{v}{u^2+v^2})$。$TS^2$ 的[转移函数](@entry_id:273897)就是这个[坐标变换](@entry_id:172727)的雅可比矩阵。通过直接计算，可以得到该雅可比[矩阵的[行列](@entry_id:148198)式](@entry_id:142978)为 $-\frac{1}{(u^2+v^2)^2}$ [@problem_id:3004547]。这个非平凡的[转移函数](@entry_id:273897)清晰地表明了 $TS^2$ 虽然局部看起来像 $\mathbb{R}^4$，但其整体结构是扭曲的，不是一个简单的直积空间 $S^2 \times \mathbb{R}^2$。对 $TS^2$ 上不同[坐标系](@entry_id:156346)下的[切向量](@entry_id:265494)分量进行变换，本质上就是应用这个雅可比矩阵 [@problem_id:1066949]。

典范投影 $\pi: TM \to M$ 是一个[光滑映射](@entry_id:203730)。其在 $TM$ 上一点 $u=(p,v)$ 的[微分](@entry_id:158718)（或[前推](@entry_id:158718)） $d\pi_u: T_u(TM) \to T_pM$ 将 $TM$ 的[切向量](@entry_id:265494)（即 $T(TM)$ 中的元素）映射回 $M$ 的[切向量](@entry_id:265494)。在自然坐标 $(x^i, v^i)$ 下，$T_u(TM)$ 的基是 $\{\frac{\partial}{\partial x^i}|_u, \frac{\partial}{\partial v^i}|_u\}$。由于 $\pi$ 的坐标表示为 $\pi(x^1, \dots, v^n) = (x^1, \dots, x^n)$，它的[微分](@entry_id:158718)作用在[基向量](@entry_id:199546)上为：
$$ d\pi_u\left(\frac{\partial}{\partial x^i}\bigg|_u\right) = \frac{\partial}{\partial x^i}\bigg|_p, \quad d\pi_u\left(\frac{\partial}{\partial v^i}\bigg|_u\right) = 0 $$
这意味着 $d\pi$ "保留"了基点方向的运动分量，而"遗忘"了纤维方向的运动分量 [@problem_id:1066910]。

### [切丛](@entry_id:161294)上的向量场：提升

[流形](@entry_id:153038) $M$ 上的几何结构可以被“提升”到其切丛 $TM$ 上。向量场的提升是其中最基本的操作，它提供了研究 $TM$ 几何的强大工具。$T_u(TM)$ 的[切向量](@entry_id:265494)可以被分解为与纤维相切的“垂直”部分和与纤维“正交”的“水平”部分。

#### 垂直提升

对于 $TM$ 上的一点 $u=(p,v)$，其所在纤维 $T_pM$ 本身是一个[向量空间](@entry_id:151108)，因此也是一个光滑子流形。在 $u$ 点沿纤维方向的[切向量](@entry_id:265494)构成了 $T_u(TM)$ 的一个[子空间](@entry_id:150286)，称为 **垂直[子空间](@entry_id:150286)**（vertical subspace），记为 $V_u(TM)$。从[微分](@entry_id:158718)的角度看，垂直[子空间](@entry_id:150286)正是[微分](@entry_id:158718)映射 $d\pi_u$ 的核：
$$ V_u(TM) = \ker(d\pi_u) = \text{span}\left\{\frac{\partial}{\partial v^1}\bigg|_u, \dots, \frac{\partial}{\partial v^n}\bigg|_u\right\} $$
$V_u(TM)$ 中的向量称为 **垂直向量**。

给定 $M$ 上的一个向量场 $X$，我们可以定义其在 $TM$ 上的 **垂直提升**（vertical lift）$X^V$。$X^V$ 是 $TM$ 上的一个向量场，在每一点 $u=(p,v)$，$X^V_u$ 都是一个垂直向量。具体而言，$X^V_u$ 可以被看作是 $X_p$ 在纤维 $T_pM$ 中的平行移动。在自然坐标中，如果 $X = \sum_i X^i(x) \frac{\partial}{\partial x^i}$，则其垂直提升的坐标表达式为：
$$ X^V = \sum_i X^i(x) \frac{\partial}{\partial v^i} $$
这个定义非常直观：$X$ 在 $M$ 上的 $i$-分量被用作 $X^V$ 在 $TM$ 上的 $v^i$-方向（即纤维方向）的分量。垂直提升的向量场只在纤维方向上作用，因此它对只依赖于基点坐标的函数（即从 $M$ 提升到 $TM$ 的函数）的作用为零。例如，考虑 $M$ 上的一个向量场 $X = y \frac{\partial}{\partial x} - x \frac{\partial}{\partial y}$，其垂直提升为 $X^V = y \frac{\partial}{\partial v_x} - x \frac{\partial}{\partial v_y}$。我们可以计算它对 $TM$ 上函数的作用，比如 $F = \alpha v_x^2 + \beta v_y^2 - \gamma (x v_y - y v_x)$，通过应用链式法则即可得到 $X^V(F)$ 的值 [@problem_id:1067031]。

#### [水平提升](@entry_id:160651)

为了定义一个与垂直[子空间](@entry_id:150286)互补的 **水平[子空间](@entry_id:150286)**（horizontal subspace）$H_u(TM)$，使得 $T_u(TM) = H_u(TM) \oplus V_u(TM)$，我们需要额外的结构。这个结构由 $M$ 上的一个 **[仿射联络](@entry_id:160152)**（affine connection） $\nabla$ 提供。联络本质上定义了如何在[流形](@entry_id:153038)上对向量场进行[微分](@entry_id:158718)，并允许我们比较邻近点上的切向量，从而定义了“平行移动”的概念。

一旦有了联络，水平[子空间](@entry_id:150286) $H_u(TM)$ 就被定义为那些在投影到 $M$ 上时“保持水平”的[切向量](@entry_id:265494)所构成的空间。利用这个水平/垂直分解，任何 $M$ 上的向量场 $X$ 都可以被唯一地提升为一个在 $TM$ 上处处水平的向量场，称为 **[水平提升](@entry_id:160651)**（horizontal lift），记作 $X^H$。

如果联络 $\nabla$ 的克氏符（Christoffel symbols）为 $\Gamma^k_{ij}$，则 $X = \sum_i X^i(x) \frac{\partial}{\partial x^i}$ 的[水平提升](@entry_id:160651)在自然坐标下的表达式为：
$$ X^H = \sum_i X^i(x) \frac{\partial}{\partial x^i} - \sum_{i,j,k} v^j \Gamma^k_{ij}(x) X^i(x) \frac{\partial}{\partial v^k} $$
这个表达式的第一部分 $X^i \frac{\partial}{\partial x^i}$ 确保了 $d\pi(X^H) = X$。第二部分是一个修正项，它是一个垂直向量，其作用是抵消掉沿 $X$ 方向移动时 $v$ 的“非水平”变化，从而确保 $X^H$ 保持在水平[子空间](@entry_id:150286)中。例如，在具有标[准圆](@entry_id:175119)度量的 $S^2$ 上，我们可以计算其 Levi-Civita 联络的克氏符，然后用上述公式得到方位角向量场 $\partial_\phi$ 的[水平提升](@entry_id:160651) $X^H$ 的具体坐标表达式，并用它来计算特定点上的作用 [@problem_id:1067084]。

#### 完全提升

除了垂直和[水平提升](@entry_id:160651)，还有一种称为 **完全提升**（complete lift）或 **切向提升**（tangent lift）的构造，记为 $X^C$。如果 $X$ 在 $M$ 上生成一个流 $\phi_t$，那么 $X^C$ 就是这个流在 $TM$ 上的[微分](@entry_id:158718) $d\phi_t$ 所生成的向量场。在坐标中，它的表达式是：
$$ X^C = \sum_i X^i(x) \frac{\partial}{\partial x^i} + \sum_{i,j} v^j \frac{\partial X^i}{\partial x^j}(x) \frac{\partial}{\partial v^i} $$
这个定义不依赖于联络，是一种更具代数性质的构造。我们可以看到，完全提升同时包含了基点和纤维方向的分量。事实上，借助联络，完全提升可以被分解为水平和垂直部分之和：$X^C = X^H + (\nabla_v X)^V$。例如，对于 $\mathbb{R}^2$ 上的向量场 $X = y^2 \frac{\partial}{\partial x} + x \frac{\partial}{\partial y}$，我们可以通过上述公式直接计算其完全提升 $X^C$ 的表达式，并进一步研究其性质 [@problem_id:1067012]。

### 切丛上的典范结构

切丛 $TM$ 不仅仅是一个[光滑流形](@entry_id:160799)，它还从底[流形](@entry_id:153038) $(M,g)$ 继承了一系列丰富的几何结构。

#### 刘维尔向量场

在任何[切丛](@entry_id:161294)上，都存在一个典范的 **刘维尔向量场**（Liouville vector field），通常记为 $Z$。在自然坐标中，它的表达式非常简单：
$$ Z = \sum_i v^i \frac{\partial}{\partial v^i} $$
这个向量场在每一点 $u=(p,v)$ 都指向从纤维原点 $0_p$ 到 $v$ 的方向。因此，$Z$ 生成了沿纤维的伸缩变换 $t \mapsto (p, e^t v)$。刘维尔向量场在[辛几何](@entry_id:160783)和[哈密顿力学](@entry_id:146202)中扮演着核心角色，它与[测地流](@entry_id:270369)密切相关。例如，动能函数 $E = \frac{1}{2}g_{ij}v^i v^j$ 关于 $Z$ 的作用 $Z(E) = \sum_k v^k \frac{\partial E}{\partial v^k} = g_{ij}v^i v^j = 2E$ [@problem_id:1067033]。

#### Sasaki 度量

如果 $(M,g)$ 是一个[黎曼流形](@entry_id:261160)，我们可以利用水平/垂直分解在 $TM$ 上定义一个自然的黎曼度量，称为 **Sasaki 度量** $g_S$。其定义如下：对于 $M$ 上的任意两个向量场 $X, Y$，它们的提升在 $TM$ 上的度量关系为：
1.  $g_S(X^H, Y^H) = g(X, Y) \circ \pi$
2.  $g_S(X^V, Y^V) = g(X, Y) \circ \pi$
3.  $g_S(X^H, Y^V) = 0$

这一定义表明，水平[子空间](@entry_id:150286)和垂直[子空间](@entry_id:150286)在 Sasaki 度量下是相互正交的。并且，[水平提升](@entry_id:160651)和垂直提升都是[等距嵌入](@entry_id:152303)（在纤维方向上）。这使得 $TM$ 本身也成为了一个黎曼流形。由于黎曼联络（Levi-Civita联络）对于平坦空间（如 $\mathbb{R}^n$ 或[平坦环面](@entry_id:261129) $T^n$）的克氏符为零，此时[水平提升](@entry_id:160651) $X^H$ 就简化为 $X^i \frac{\partial}{\partial x^i}$。在这种情况下，计算 Sasaki 范数变得尤为简单。例如，对于一个由 $W = A \cdot X^H + B \cdot Y^V$ 构成的向量场，其 Sasaki 范数的平方为 $\|W\|_{g_S}^2 = A^2 g(X,X) + B^2 g(Y,Y)$ [@problem_id:1067037]。

#### [典范辛形式](@entry_id:180641)

[切丛](@entry_id:161294) $TM$ 还具有一个不依赖于度量的典范 **辛结构**（symplectic structure）。这个结构由 **典范 1-形式**（canonical 1-form）$\Theta$（也称为刘维尔形式或[联络形式](@entry_id:263247)）导出。给定[黎曼度量](@entry_id:754359) $g$，$\Theta$ 在点 $u=(p,v) \in TM$ 对一个向量 $A \in T_u(TM)$ 的作用定义为：
$$ \Theta_u(A) = g_p(v, d\pi_u(A)) $$
在自然坐标中，$\Theta = \sum_{i,j} g_{ij}(x) v^i dx^j$。

**[典范辛形式](@entry_id:180641)**（canonical symplectic form）$\Omega$ 定义为 $\Theta$ 的[外微分](@entry_id:161900)的相反数：$\Omega = -d\Theta$。这个 [2-形式](@entry_id:188008)是非退化的、闭的，因此它将 $TM$ 变成了一个[辛流形](@entry_id:161608)。在物理学中，若将 $M$ 视为位形空间，则 $TM$ 就是相空间，动能 $E$ 就是[哈密顿量](@entry_id:172864)，而[测地线方程](@entry_id:264349)就可以表示为与 $\Omega$ 相关的[哈密顿方程](@entry_id:156213)。

[辛形式](@entry_id:165896) $\Omega$ 与水平/垂直分解有着优美的关系。可以证明：
$$ \Omega(X^V, Y^V) = 0, \quad \Omega(X^H, Y^V) = g(X, Y) \circ \pi $$
值得注意的是，两个[水平提升](@entry_id:160651)的配对 $\Omega(X^H, Y^H)$ 通常不为零，它与底[流形](@entry_id:153038)的[曲率张量](@entry_id:181383) $R$ 有关。以上关系表明，垂直[子空间](@entry_id:150286)是拉格朗日的，而[辛形式](@entry_id:165896)在水平和垂直向量间的配对则能恢复底[流形](@entry_id:153038)的度量。这个性质非常深刻，它将[黎曼几何](@entry_id:160508)（通过 $g$ 和联络定义的 $H, V$）与[辛几何](@entry_id:160783)（通过 $\Omega$）联系在一起。在[庞加莱上半平面](@entry_id:264005) $\mathbb{H}^2$ 这样的具体例子中，我们可以显式计算克氏符和各个提升，并验证这个美妙的公式 [@problem_id:1067080]。

### 二阶切丛与典范对合

最后，我们简要介绍二阶结构。由于 $TM$ 本身是一个光滑流形，我们可以考虑它的[切丛](@entry_id:161294)，即 **二阶[切丛](@entry_id:161294)**（second tangent bundle）$T(TM)$。$T(TM)$ 中的一个元素是 $TM$ 中一条曲线的切向量。如果 $TM$ 的自然坐标为 $(x^i, v^i)$，那么 $T(TM)$ 的自然坐标可以记为 $(x^i, v^i; \dot{x}^i, \dot{v}^i)$。

在 $T(TM)$ 上存在一个非常重要的自然对合（involution），称为 **典范对合**（canonical flip map），记为 $\kappa: T(TM) \to T(TM)$。它的作用是交换基点速度和纤维向量分量：
$$ \kappa: (x^i, v^i; \dot{x}^i, \dot{v}^i) \mapsto (x^i, \dot{x}^i; v^i, \dot{v}^i) $$
这个映射的几何意义与二阶[偏导数的对称性](@entry_id:194790)（Schwarz 定理）密切相关。它在构造高阶[拉格朗日力学](@entry_id:147054)和芬斯勒几何中起着基础性作用。我们可以通过考虑 $TM$ 中一条具体曲线（例如一条螺旋线上的旋转向量场）的[切向量](@entry_id:265494)，来具体计算典范对合的作用 [@problem_id:1066926]。

综上所述，[切丛](@entry_id:161294)不仅是汇集所有切向量的简单集合，它本身就是一个拥有丰富几何结构的[流形](@entry_id:153038)。通过垂直、水平和完全提升，我们可以将底[流形上的分析](@entry_id:637756)问题提升到[切丛](@entry_id:161294)上进行研究。而 Sasaki 度量和[典范辛形式](@entry_id:180641)等内在结构，则为[测地流](@entry_id:270369)、[哈密顿力学](@entry_id:146202)和[几何量子化](@entry_id:159174)等领域提供了坚实的数学框架。