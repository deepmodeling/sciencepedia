## 引言
在现代数学与理论物理的宏伟蓝图中，向量丛、[联络与曲率](@entry_id:158520)不仅是核心语言，更是连接不同分支的深邃桥梁。从描述[弯曲时空](@entry_id:159822)的几何结构到刻画基本粒子相互作用的[规范场](@entry_id:159627)，这些概念无处不在，为我们理解自然的内在对称性与拓扑结构提供了强有力的数学框架。然而，对于初学者而言，这些抽象概念之间的逻辑关系、它们的几何直观以及它们在不同领域中的具体应用往往构成了一道难以逾越的知识鸿沟。本文旨在系统性地填补这一鸿沟，为读者提供一条从基本原理到前沿应用的清晰学习路径。

在接下来的内容中，我们将分三个章节展开探讨。在**“原理与机制”**一章中，我们将奠定理论基础，从向量丛的定义出发，详细阐述联络如何作为[微分](@entry_id:158718)工具被引入，以及曲率如何量化空间的弯曲。随后，在**“应用与跨学科联系”**一章中，我们将展示这些理论的强大威力，探索它们在黎曼几何、代数拓扑（通过陈-韦伊理论）以及[几何分析](@entry_id:157700)与物理学（如[杨-米尔斯理论](@entry_id:137401)）中的深刻应用。最后，**“动手实践”**部分将通过一系列精心设计的计算练习，帮助读者将抽象理论转化为具体的解题技能。通过这一学习旅程，读者将不仅掌握向量丛理论的精髓，更能体会到其作为现代几何学基石的深刻意义与广泛影响。

## 原理与机制

本章旨在系统性地阐述向量丛、[联络与曲率](@entry_id:158520)的核心原理与机制。我们将从向量丛的基本定义出发，探讨其局部与全局的结构特性。随后，我们将引入联络作为在[丛的截面](@entry_id:195261)上进行微积分的工具，并揭示曲率作为联络的内在属性，它量化了[平行输运的路径依赖性](@entry_id:204826)。最后，我们将介绍[主丛](@entry_id:160029)的框架，为理解这些几何概念提供一个更深刻且统一的视角。

### 向量丛的概念：局部平凡与全局扭转

在现代几何学中，向量丛是一个核心概念，它将[流形](@entry_id:153038)上的每一点与一个[向量空间](@entry_id:151108)联系起来，并要求这种联系在局部上是“平滑”的。这种结构允许我们在弯曲的空间上一致地讨论向量、张量等依赖于点的线性对象。

#### 形式化定义与[局部平凡化](@entry_id:267993)

一个光滑的 **$k$ 秩实向量丛** (smooth rank-$k$ real vector bundle) 由一个三元组 $(\pi, E, M)$ 构成，其中 $E$（总空间）和 $M$（基空间）是[光滑流形](@entry_id:160799)，$\pi: E \to M$ 是一个光滑的满射（称为投影）。此结构需满足以下核心条件：

1.  对于 $M$ 中的每一点 $x$，其[原像](@entry_id:150899) $E_x := \pi^{-1}(x)$（称为在 $x$ 点的 **纤维**）被赋予一个 $k$ 维实[向量空间](@entry_id:151108)的结构。
2.  **[局部平凡性](@entry_id:160325)** (local triviality)：对于 $M$ 上的任意一点 $x$，存在一个包含 $x$ 的[开邻域](@entry_id:268496) $U$ 和一个微分同胚 $\varphi: \pi^{-1}(U) \to U \times \mathbb{R}^k$，这个映射被称为 **[局部平凡化](@entry_id:267993)** (local trivialization)。它不仅是一个[光滑映射](@entry_id:203730)，还必须满足两个[兼容性条件](@entry_id:201103)：
    *   $\varphi$ 覆盖了 $U$ 上的[恒等映射](@entry_id:634191)，即若 $\varphi(p) = (x, v)$，则 $\pi(p) = x$。
    *   对于 $U$ 中的每一点 $x$，$\varphi$ 在纤维 $E_x$ 上的限制 $\varphi_x: E_x \to \{x\} \times \mathbb{R}^k \cong \mathbb{R}^k$ 是一个[向量空间](@entry_id:151108)的[线性同构](@entry_id:270529)。

这个定义捕捉了一个关键思想：在局部上，任何向量丛都“看起来”像一个平凡的 **积丛** (product bundle) $M \times \mathbb{R}^k$。一个向量丛被称为 **平凡的** (trivial)，当且仅当存在一个 **全局平凡化**，即一个定义在整个 $E$ 上的向量丛同构 $\Phi: E \to M \times \mathbb{R}^k$ [@problem_id:3037042]。然而，许多重要的向量丛并非平凡的。例如，[二维球面](@entry_id:269890) $S^2$ 的[切丛](@entry_id:161294) $TS^2$ 就是一个非平凡的向量丛，这与著名的“[毛球定理](@entry_id:151079)”有关，即无法在球面上梳理出一个处处非零的光滑向量场。

#### 黏合构造：[转移函数](@entry_id:273897)

向量丛的“全局扭转”特性，正是通过描述这些[局部平凡化](@entry_id:267993)在重叠区域如何“黏合”来编码的。假设我们有一个覆盖 $M$ 的开集族 $\{U_\alpha\}$，以及相应的[局部平凡化](@entry_id:267993)映射 $\varphi_\alpha: \pi^{-1}(U_\alpha) \to U_\alpha \times \mathbb{R}^k$。

在任意两个开集的非空交集 $U_\alpha \cap U_\beta$ 上，我们可以考虑复合映射 $\varphi_\beta \circ \varphi_\alpha^{-1}$。这个映射是一个从 $(U_\alpha \cap U_\beta) \times \mathbb{R}^k$ 到自身的[微分同胚](@entry_id:147249)：
$$ \varphi_\beta \circ \varphi_\alpha^{-1}: (x, v) \mapsto (x, g_{\alpha\beta}(x)v) $$
这里 $x \in U_\alpha \cap U_\beta$，$v \in \mathbb{R}^k$。由于 $\varphi_\alpha$ 和 $\varphi_\beta$ 在每个纤维上都是线性的，所以对于固定的 $x$，$v \mapsto g_{\alpha\beta}(x)v$ 必须是一个线性变换。因此，$g_{\alpha\beta}(x)$ 是一个可逆的 $k \times k$ 矩阵。这样，我们就得到了一族[光滑映射](@entry_id:203730) $g_{\alpha\beta}: U_\alpha \cap U_\beta \to \mathrm{GL}(k, \mathbb{R})$，它们被称为 **[转移函数](@entry_id:273897)** (transition functions)。

这些[转移函数](@entry_id:273897)必须满足[一致性条件](@entry_id:637057)。在三重重叠区域 $U_\alpha \cap U_\beta \cap U_\gamma$ 上，从 $\alpha$-平凡化变换到 $\gamma$-平凡化，既可以直接进行，也可以通过 $\beta$-平凡化作中介。这两种方式必须给出相同的结果，即 $(\varphi_\gamma \circ \varphi_\beta^{-1}) \circ (\varphi_\beta \circ \varphi_\alpha^{-1}) = \varphi_\gamma \circ \varphi_\alpha^{-1}$。这在[转移函数](@entry_id:273897)上表现为 **上链条件** (cocycle condition) [@problem_id:3037070]：
$$ g_{\alpha\gamma}(x) = g_{\beta\gamma}(x) g_{\alpha\beta}(x) \quad \text{或等价地} \quad g_{\alpha\beta}(x) g_{\beta\gamma}(x) g_{\gamma\alpha}(x) = \mathrm{Id} $$
（具体形式取决于坐标或标架的变换约定）。此外，显然有 $g_{\alpha\alpha} = \mathrm{Id}$ 和 $g_{\beta\alpha} = g_{\alpha\beta}^{-1}$。

反过来，一个深刻的结论是，任何满足上链条件的一族[光滑映射](@entry_id:203730) $\{g_{\alpha\beta}\}$ 都唯一地（在同构意义下）确定了一个向量丛。我们可以将一族不相交的积丛 $U_\alpha \times \mathbb{R}^k$ 沿着它们的边界，使用[转移函数](@entry_id:273897) $g_{\alpha\beta}$ 作为“胶水”来黏合，从而构造出总空间 $E$。

#### 同构与等价

两个秩相同的向量丛 $E$ 和 $E'$ 被认为是 **同构的** (isomorphic)，如果存在一个保持纤维结构和线性结构的微分同胚。在使用[转移函数](@entry_id:273897)描述的框架下，这等价于它们的[转移函数](@entry_id:273897)上链是 **上同调的** (cohomologous)。具体来说，假设 $E$ 和 $E'$ 分别由关于同一开覆盖 $\{U_\alpha\}$ 的[转移函数](@entry_id:273897) $\{g_{\alpha\beta}\}$ 和 $\{g'_{\alpha\beta}\}$ 定义。它们定义同构的丛，当且仅当存在一族[光滑映射](@entry_id:203730) $h_\alpha: U_\alpha \to \mathrm{GL}(k, \mathbb{R})$，使得在每个重叠区域 $U_\alpha \cap U_\beta$ 上，下式成立 [@problem_id:3037070]：
$$ g'_{\alpha\beta}(x) = h_\beta(x) g_{\alpha\beta}(x) h_\alpha(x)^{-1} $$
这可以被理解为在每个[局部平凡化](@entry_id:267993)中进行一次依赖于点的基变换。

### 从旧丛构造新丛

向量丛的理论之所以强大，部分原因在于我们可以像操作[向量空间](@entry_id:151108)一样来操作它们，从而从已知的丛构造出新的丛。这些操作在纤维层面是标准的线性代数运算，而在[转移函数](@entry_id:273897)层面则对应于矩阵的相应运算。

#### 惠特尼和 (Whitney Sum)

给定基空间同为 $M$ 的两个向量丛 $E$ (秩 $r_E$) 和 $F$ (秩 $r_F$)，它们的 **惠特尼和** $E \oplus F$ 是一个在 $M$ 上的新向量丛。其在点 $x$ 的纤维定义为两个原纤维的直和：$(E \oplus F)_x = E_x \oplus F_x$。

如果我们有 $E$ 和 $F$ 的[转移函数](@entry_id:273897) $g^E_{ij}$ 和 $g^F_{ij}$（相对于共同的[开覆盖](@entry_id:140020)），那么 $E \oplus F$ 的[转移函数](@entry_id:273897) $g^{E \oplus F}_{ij}$ 就是由这两个矩阵构成的分[块对角矩阵](@entry_id:145530) [@problem_id:3037026]：
$$ g^{E \oplus F}_{ij}(x) = \begin{pmatrix} g^E_{ij}(x) & 0 \\ 0 & g^F_{ij}(x) \end{pmatrix} $$
这个新矩阵属于 $\mathrm{GL}(r_E+r_F, \mathbb{K})$。因此，惠特尼和的秩是两丛秩之和：$\mathrm{rank}(E \oplus F) = r_E + r_F$。

#### [张量积](@entry_id:140694) (Tensor Product)

同样，我们可以定义 $E$ 和 $F$ 的 **[张量积](@entry_id:140694)丛** $E \otimes F$。其在点 $x$ 的纤维是纤维的[张量积](@entry_id:140694)：$(E \otimes F)_x = E_x \otimes F_x$。

$E \otimes F$ 的[转移函数](@entry_id:273897)由原[转移函数](@entry_id:273897)的 **克罗内克积** (Kronecker product) 给出 [@problem_id:3037026]：
$$ g^{E \otimes F}_{ij}(x) = g^E_{ij}(x) \otimes g^F_{ij}(x) $$
[克罗内克积](@entry_id:182766)是定义在 $\mathrm{GL}(r_E, \mathbb{K}) \times \mathrm{GL}(r_F, \mathbb{K})$ 到 $\mathrm{GL}(r_E r_F, \mathbb{K})$ 的映射。因此，张量积丛的秩是两丛秩之积：$\mathrm{rank}(E \otimes F) = r_E r_F$。

其他重要的构造还包括 **对偶丛** $E^*$（其纤维为 $(E_x)^*$）和 **外幂丛** $\Lambda^p E$（其纤维为 $\Lambda^p(E_x)$），它们在微分形式和几何学中有广泛应用。

### 联络：[微分截面](@entry_id:137333)

[向量丛的截面](@entry_id:270734) (section) 是一个[光滑映射](@entry_id:203730) $s: M \to E$，使得 $\pi \circ s = \mathrm{id}_M$。它为[流形](@entry_id:153038)上的每一点都指定了该点纤维中的一个向量。一个自然的问题是：我们如何对[截面](@entry_id:154995)进行[微分](@entry_id:158718)？

在欧氏空间中，我们可以对[向量值函数](@entry_id:261164)进行分量[微分](@entry_id:158718)。但在一个弯曲的[流形](@entry_id:153038)上，或在一个扭曲的向量丛中，不同点的纤维没有自然的认同方式。因此，简单地对[局部坐标](@entry_id:181200)下的分量函数求导数是没有几何意义的，因为结果会依赖于[局部平凡化](@entry_id:267993)的选择。**联络** (connection) 正是为解决这一问题而引入的附加结构，它提供了一种在丛上进行[微分](@entry_id:158718)的一致性法则。

#### 联络的公理化定义

一个 **线性联络** 是一个 $\mathbb{R}$-线性算子 $\nabla: \Gamma(E) \to \Gamma(T^*M \otimes E)$，它将 $E$ 的一个光滑[截面](@entry_id:154995)映射为 $E$ 值 1-形式（即 $T^*M \otimes E$ 的一个[截面](@entry_id:154995)）。这个算子必须满足如下的 **[莱布尼茨法则](@entry_id:157949)** (Leibniz rule) [@problem_id:3037074]：
$$ \nabla(fs) = df \otimes s + f \nabla s $$
其中 $f \in C^\infty(M)$ 是一个光滑函数，$s \in \Gamma(E)$ 是一个光滑[截面](@entry_id:154995)，$df$ 是 $f$ 的外微分（一个 [1-形式](@entry_id:270392)）。

这个法则是联络定义的核心。它表明 $\nabla$ 不是一个 $C^\infty(M)$-线性的算子（即张量），否则我们将有 $\nabla(fs) = f\nabla s$。$df \otimes s$ 这一项的存在表明 $\nabla$ 是一个一阶微分算子，它同时作用于函数 $f$ 和[截面](@entry_id:154995) $s$。

#### [协变导数](@entry_id:152476)与[局部标架](@entry_id:635789)

尽管 $\nabla s$ 作为 $E$ 值 1-形式包含了关于 $s$ 在所有方向上的变化信息，但通常处理沿特定方向的变化更为方便。给定一个向量场 $X \in \Gamma(TM)$，我们可以定义 $s$ 沿 $X$ 方向的 **协变导数** (covariant derivative)，记为 $\nabla_X s$，通过将 $\nabla s$ 这个 1-形式作用于向量场 $X$ 来得到：
$$ \nabla_X s := \iota_X(\nabla s) \in \Gamma(E) $$
从 $\nabla$ 的公理化定义，我们可以推导出 $\nabla_X$ 的两个关键性质 [@problem_id:3037074]：
1.  **对 $X$ 的 $C^\infty(M)$-线性**：$\nabla_{fX} s = f \nabla_X s$。这意味着 $\nabla_X s$ 在点 $x$ 的值仅依赖于 $X$ 在该点的值 $X_x$，而与 $X$ 在 $x$ 邻域内的行为无关。
2.  **对 $s$ 的[莱布尼茨法则](@entry_id:157949)**：$\nabla_X(fs) = X(f)s + f \nabla_X s$，其中 $X(f) = df(X)$ 是函数 $f$ 沿 $X$ 的[方向导数](@entry_id:189133)。

要在局部进行计算，我们通常选取一个 **[局部标架](@entry_id:635789)** (local frame) $\{e_1, \dots, e_k\}$，它是 $\pi^{-1}(U)$ 上的一组[截面](@entry_id:154995)，使得在 $U$ 的每一点 $x$，$\{e_1(x), \dots, e_k(x)\}$ 构成纤维 $E_x$ 的一组基。联络 $\nabla$ 作用在这些基[截面](@entry_id:154995)上的结果可以用基自身来展开。其系数形成一个矩阵，其元素为 [1-形式](@entry_id:270392)，称为 **联络 1-形式** (connection 1-forms) $\omega^i_j \in \Omega^1(U)$：
$$ \nabla e_j = \sum_{i=1}^k \omega^i_j \otimes e_i $$
现在，考虑一个任意[截面](@entry_id:154995) $s = \sum_j s^j e_j$，其中 $s^j \in C^\infty(U)$ 是分量函数。利用协变[导数的性质](@entry_id:141529)，我们可以推导出其分量的表达式 [@problem_id:3037035]：
\begin{align*} \nabla_X s = \nabla_X \left(\sum_j s^j e_j\right) = \sum_j \nabla_X(s^j e_j) \\ = \sum_j \left( (X s^j) e_j + s^j \nabla_X e_j \right) \\ = \sum_j (X s^j) e_j + \sum_j s^j \left( \sum_i \omega^i_j(X) e_i \right) \\ = \sum_i \left( X(s^i) + \sum_j \omega^i_j(X) s^j \right) e_i \end{align*}
因此，$\nabla_X s$ 在标架 $\{e_i\}$ 下的第 $i$ 个分量 $(\nabla_X s)^i$ 为：
$$ (\nabla_X s)^i = X(s^i) + \sum_{j=1}^k \omega^i_j(X) s^j $$
这个公式至关重要。它表明协变导数由两部分组成：一部分是普通的方向导数 $X(s^i)$，另一部分是修正项 $\sum_j \omega^i_j(X) s^j$，该修正项由[联络形式](@entry_id:263247)决定，弥补了因标架自身在空间中“旋转”而产生的变化。

例如，在 $M=\mathbb{R}^2$ 的平凡丛 $E=\mathbb{R}^2 \times \mathbb{R}^2$ 上，给定[联络形式](@entry_id:263247)矩阵 $\omega = (\omega^i_j)$、向量场 $X$ 和[截面](@entry_id:154995) $s=(s^1, s^2)$，我们可以利用上述公式在任意点计算协变导数的分量 [@problem_id:3037035]。

### [平行输运](@entry_id:160671)、和乐与曲率

联络的引入不仅让我们能够[微分截面](@entry_id:137333)，还引出了一系列深刻的几何概念。

#### [平行输运](@entry_id:160671)

联络提供了一种比较沿路径的不同点上纤维中向量的方法。一个[截面](@entry_id:154995) $s(t)$ 被称为沿着一条光滑曲线 $\gamma: [0,1] \to M$ 是 **平行的** (parallel)，如果它沿该路径的协变导数为零：
$$ \nabla_{\dot{\gamma}(t)} s(t) = 0 $$
这是一个关于[截面](@entry_id:154995)分量的[一阶常微分方程组](@entry_id:635184)。对于给定的初始向量 $v \in E_{\gamma(0)}$，存在唯一的平行[截面](@entry_id:154995) $s(t)$ 使得 $s(0)=v$。这定义了一个[线性同构](@entry_id:270529)映射 $P_\gamma: E_{\gamma(0)} \to E_{\gamma(1)}$，称为沿 $\gamma$ 的 **[平行输运](@entry_id:160671)** (parallel transport) 映射，其中 $P_\gamma(v) = s(1)$。

在[局部标架](@entry_id:635789)中，[平行输运](@entry_id:160671)方程可以写作一个矩阵[微分方程](@entry_id:264184)。令 $S(t)$ 为平行[截面](@entry_id:154995)在标架下的分量列向量，$\Omega(t)$ 为将联络 [1-形式](@entry_id:270392)矩阵 $\omega$ [拉回](@entry_id:160816)到路径上得到的矩阵，即 $\gamma^*\omega = \Omega(t) dt$。[平行输运](@entry_id:160671)方程为 [@problem_id:3037069]：
$$ \frac{dS(t)}{dt} = - \Omega(t) S(t) $$
这个方程的解，即演化算子 $U(t)$ (使得 $S(t) = U(t)S(0)$)，由一个称为 **路径排序指数** (path-ordered exponential) 的[无穷级数](@entry_id:143366)给出：
$$ U(t) = \mathcal{P}\exp\left(-\int_0^t \Omega(\tau)d\tau\right) $$
其中 $\mathcal{P}$ 表示路径排序，因为当不同时刻的矩阵 $\Omega(\tau)$ 不对易时，它们在乘积中的顺序至关重要。在特殊情况下，如果[联络形式](@entry_id:263247)在某个[坐标系](@entry_id:156346)下是常数矩阵 $A_i$，并且路径是直线 $\gamma(t)=x_0+tv$，则 $\Omega(t) = \sum_i v^i A_i$ 是一个常数矩阵。此时，解就简化为标准的[矩阵指数](@entry_id:139347)函数 $\exp(-t \sum_i v^i A_i)$ [@problem_id:3037069]。

#### 和乐群

[平行输运](@entry_id:160671)是依赖于路径的。将一个向量从点 $p$ 出发，沿一条闭合回路 $\gamma$ (即 $\gamma(0) = \gamma(1) = p$) 进行平行输运，返回到 $p$ 点的向量通常与初始向量不同。平行输运映射 $P_\gamma$ 成为一个[自同构](@entry_id:155390) $P_\gamma: E_p \to E_p$。

在点 $p$ 的所有闭合回路上产生的平行输运映射构成的群，称为在该点的 **和乐群** (holonomy group) $\mathrm{Hol}_p(\nabla)$。这个群是 $\mathrm{GL}(E_p)$ 的一个李[子群](@entry_id:146164)，它精确地量化了由联络定义的“弯曲”或“全局扭转”的程度。

#### 曲率：无穷小[和乐](@entry_id:137051)

[和乐群](@entry_id:191471)描述了宏观路径上的几何效应，而 **曲率** (curvature) 则量化了其无穷小对应物。直观上，曲率衡量了当一个向量沿一个无穷小闭回路[平行输运](@entry_id:160671)时发生的转动。

形式上，[曲率算子](@entry_id:198006) $F$ 定义为[协变导数](@entry_id:152476)的不对易性：
$$ F(X, Y)s = \nabla_X \nabla_Y s - \nabla_Y \nabla_X s - \nabla_{[X,Y]} s $$
其中 $X, Y$ 是向量场，$s$ 是[截面](@entry_id:154995)。一个关键的性质是，$F$ 是一个张量，即它在 $X, Y, s$ 中都是 $C^\infty(M)$-线性的。这意味着 $F$ 在一点的值仅依赖于 $X, Y, s$ 在该点的值。因此，我们可以将其视为一个 $\mathrm{End}(E)$-值的 [2-形式](@entry_id:188008)，$F \in \Omega^2(M, \mathrm{End}(E))$。

在[局部标架](@entry_id:635789) $\{e_i\}$ 中，曲率可以表示为一个 2-形式矩阵 $\Omega = (\Omega^i_j)$，其中 $\Omega^i_j \in \Omega^2(U)$。这些 **曲率 [2-形式](@entry_id:188008)** 与联络 [1-形式](@entry_id:270392) $\omega = (\omega^i_j)$ 之间存在一个基本关系，即 **[嘉当第二结构方程](@entry_id:196278)** (Cartan's second structure equation)：
$$ \Omega = d\omega + \omega \wedge \omega $$
这里 $d\omega$ 是对 $\omega$ 的每个[矩阵元](@entry_id:186505)求外微分，而 $\omega \wedge \omega$ 是矩阵乘法与外积的结合。这个方程表明，曲率是[联络形式](@entry_id:263247)的外[协变导数](@entry_id:152476)。

对于一个二维[黎曼曲面](@entry_id:178613)，其[切丛](@entry_id:161294)上有一个特殊的联络——[列维-奇维塔联络](@entry_id:161107)。它的曲率与经典的 **高斯曲率** $K$ 密切相关。通过第一[结构方程](@entry_id:274644) $d\theta^i + \sum_j \omega^i_j \wedge \theta^j = 0$ (其中 $\{\theta^i\}$ 是一个正交[余标架场](@entry_id:183575))，我们可以解出联络 1-形式 $\omega^1_2$。然后，利用第二[结构方程](@entry_id:274644)，我们得到 $\Omega^1_2 = d\omega^1_2$。将此与定义 $\Omega^1_2 = K (\theta^1 \wedge \theta^2)$ 相比较，就可以确定[高斯曲率](@entry_id:149725) $K$ [@problem_id:3037032]。这建立了抽象的[曲率形式](@entry_id:199387)与经典[曲面论](@entry_id:273972)之间的直接联系。

#### [安布罗斯-辛格定理](@entry_id:198517)：曲率生成和乐

[曲率与和乐](@entry_id:186596)之间的深刻联系由 **[安布罗斯-辛格定理](@entry_id:198517)** (Ambrose-Singer theorem) 揭示。该定理指出，和乐群的[李代数](@entry_id:137954) $\mathfrak{hol}_p(\nabla)$，是由所有在[流形](@entry_id:153038)各点 $q$ 的[曲率算子](@entry_id:198006) $F_q(u,v)$，通过[平行输运](@entry_id:160671)[拉回](@entry_id:160816)到点 $p$ 后生成的。更精确地说，$\mathfrak{hol}_p(\nabla)$ 是由集合
$$ \{ P_\gamma^{-1} \circ F_q(u,v) \circ P_\gamma \mid q \in M, u,v \in T_qM, \gamma \text{ is a path from } p \text{ to } q \} $$
所生成的最小[李代数](@entry_id:137954) [@problem_id:3037054]。

这个定理有几个重要的推论：
*   **平坦联络**：如果曲率在整个[流形](@entry_id:153038)上恒为零 ($F \equiv 0$)，那么和乐群的李代数也为零 ($\mathfrak{hol}_p(\nabla) = \{0\}$)。这意味着和乐群是离散的。如果[流形](@entry_id:153038)是单连通的，则和乐群是平凡的，联络是“平坦的” [@problem_id:3037054]。
*   **几何解释**：曲率是和乐的“[无穷小生成元](@entry_id:270424)”。对于一个由向量 $aX$ 和 $bY$ 张成的无穷小平行四边形回路，平行输运产生的旋转角度 $\theta$ 正比于该区域的面积与曲率的乘积：$\theta \approx K(p) \cdot ab$ [@problem_id:3037061]。例如，在平坦的环面 $T^2$上，$K=0$，因此无穷小回路的[和乐](@entry_id:137051)是平凡的。而在半径为 $R$ 的球面 $S^2_R$ 上，$K=1/R^2$，无穷小回路的[和乐](@entry_id:137051)是一个角度为 $ab/R^2$ 的旋转。
*   在特殊情况下，例如曲率是“中心的”，即所有的[曲率算子](@entry_id:198006)都是[单位矩阵](@entry_id:156724)的倍数。它们在[李括号](@entry_id:636461)下是可交换的，因此生成的李代数是一维的阿贝尔代数 $i\mathbb{R} \cdot \mathrm{Id}_{E_p}$，它对应于 $U(1)$ [子群](@entry_id:146164)的和乐 [@problem_id:3037054]。

### [主丛](@entry_id:160029)框架

向量丛的概念可以被推广并统一在一个更抽象的框架中，即[主丛](@entry_id:160029)理论。

#### 主 G-丛

令 $G$ 是一个[李群](@entry_id:137659)。一个 **主 G-丛** (principal G-bundle) 是一个光滑纤维丛 $\pi: P \to M$，其总空间 $P$ 上有一个光滑的、自由的、传递的右 $G$ 作用，并且该作用保持纤维不变（即 $\pi(p \cdot g) = \pi(p)$）。纤维 $P_x = \pi^{-1}(x)$ 本身不是一个[向量空间](@entry_id:151108)，而是与李群 $G$ 同构的空间（作为 $G$-空间）。直观上，可以把 $P$ 的一个元素 $p \in P_x$ 看作是点 $x$ 处的一个“标架”或“[参考系](@entry_id:169232)”。$G$ 的作用 $p \cdot g$ 就代表着对这个[参考系](@entry_id:169232)进行一次变换。

[主丛](@entry_id:160029)的定义也可以通过其[局部平凡化](@entry_id:267993)来刻画，它要求[局部平凡化](@entry_id:267993)映射 $\varphi_\alpha: \pi^{-1}(U_\alpha) \to U_\alpha \times G$ 是 $G$-等变的，即 $\varphi_\alpha(p \cdot g) = (x, hg)$ 如果 $\varphi_\alpha(p) = (x, h)$ [@problem_id:3037066]。

一个典型的例子是秩 $k$ 向量丛 $E$ 的 **[标架丛](@entry_id:187852)** (frame bundle) $F(E)$。其在点 $x$ 的纤维是 $E_x$ 中所有有序基的集合。这个集合上有一个自然的 $\mathrm{GL}(k, \mathbb{R})$ 的右作用（基变换），使得 $F(E)$ 成为一个主 $\mathrm{GL}(k, \mathbb{R})$-丛。

#### 相伴丛

[主丛](@entry_id:160029)的强大之处在于，它们可以作为“母体”来生成各种类型的[纤维丛](@entry_id:159565)，包括向量丛。这个过程被称为 **相伴丛构造** (associated bundle construction)。

给定一个主 $G$-丛 $P \to M$ 和一个 $G$ 在[向量空间](@entry_id:151108) $V$ 上的表示 $\rho: G \to \mathrm{GL}(V)$，我们可以构造一个相伴向量丛 $E = P \times_\rho V$。其总空间是通过对乘积空间 $P \times V$ 取商来定义的。我们在 $P \times V$ 上定义一个右 $G$ 作用：
$$ (p, v) \cdot g = (p \cdot g, \rho(g^{-1})v) $$
相伴丛 $E$ 就是这个作用下的[轨道空间](@entry_id:148658) $E = (P \times V) / G$。其上的一个点是形如 $[p,v]$ 的[等价类](@entry_id:156032)。

这个构造的意义在于，同一个[主丛](@entry_id:160029)，通过选取不同的表示 $\rho$，可以生成不同类型的几何对象。例如，对于切丛的[标架丛](@entry_id:187852) $F(TM)$（一个主 $\mathrm{GL}(n, \mathbb{R})$-丛）：
*   选取 $\mathrm{GL}(n, \mathbb{R})$ 在 $\mathbb{R}^n$ 上的标准表示，我们重构出切丛 $TM$ 本身。
*   选取[对偶表示](@entry_id:146263)，我们得到[余切丛](@entry_id:185138) $T^*M$。
*   选取[张量积表示](@entry_id:143629)，我们得到各种[张量丛](@entry_id:203012)。

因此，[主丛](@entry_id:160029)为各种[张量丛](@entry_id:203012)提供了一个统一的起源。此外，联络的概念在[主丛](@entry_id:160029)框架下有特别简洁的表述（作为李代数值的 [1-形式](@entry_id:270392)），并且[主丛上的联络](@entry_id:159386)可以自然地诱导出其任何相伴[丛上的联络](@entry_id:191877)。这个深刻而优雅的框架是现代[微分几何](@entry_id:145818)的基石。