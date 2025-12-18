## 引言
在现代[微分几何](@entry_id:145818)与理论物理中，[张量场](@entry_id:190170)是一个处于核心地位的基石性概念。当我们从平坦的[欧氏空间](@entry_id:138052)迈向弯曲的[光滑流形](@entry_id:160799)时，描述如电磁场、时空度量或材料应力等物理和几何量的传统方法便遇到了挑战。简单地为向量或矩阵的每个分量赋予空间依赖性已不再足够，因为这样的描述会依赖于任意选择的[局部坐标系](@entry_id:751394)，从而丧失物理定律应有的客观性。[张量场](@entry_id:190170)正是为了解决这一根本问题而生，它提供了一种内在的、坐标无关的语言来刻画流形上的局部结构。

本文旨在系统性地介绍流形上[张量场](@entry_id:190170)的理论及其应用。我们将从最基本的定义出发，逐步构建起完整的理论框架，并展示其在多个前沿学科中的强大威力。读者将通过本文的学习，掌握在弯曲空间中进行微积分和物理建模的核心工具。

文章的结构分为三个主要部分。在第一章 **“原理与机制”** 中，我们将严格定义[张量场](@entry_id:190170)，探讨其代数运算与[坐标变换](@entry_id:172727)法则，并深入剖析两种关键的[微分](@entry_id:158422)工具——[李导数](@entry_id:171745)与[协变导数](@entry_id:152476)。我们还将看到，[黎曼度量](@entry_id:754359)和辛形式等基本几何结构，本质上就是特定类型的[张量场](@entry_id:190170)。随后的第二章 **“应用与跨学科联系”** 将理论付诸实践，展示[张量场](@entry_id:190170)如何在[哈密顿力学](@entry_id:146202)、广义相对论、[几何分析](@entry_id:157700)乃至工程学中扮演不可或缺的角色。最后的第三章 **“动手实践”** 则提供了一系列具体的计算问题，帮助读者巩固理论知识，将抽象概念转化为切实的计算技能。

## 原理与机制

在对光滑[流形上的微积分](@entry_id:270207)有基本了解之后，我们现在转向一个核心概念：[张量场](@entry_id:190170)。[张量场](@entry_id:190170)是向量场和[余向量](@entry_id:157727)场（或[1-形式](@entry_id:270392)）概念的推广，为在流形上描述几何结构（如距离、角度、体积）和物理场（如电磁场、[引力场](@entry_id:169425)）提供了统一而强大的语言。本章将系统地阐述[张量场](@entry_id:190170)的定义、它们的基本运算、[微分](@entry_id:158422)方法，并展示它们如何定义流形上最重要的几何结构。

### [张量场](@entry_id:190170)的定义与坐标表示

从根本上说，一个张量是在某一点上的一个[多重线性代数](@entry_id:199321)对象。设 $M$ 是一个 $n$ 维[光滑流形](@entry_id:160799)，对于其上任意一点 $p \in M$，我们有[切空间](@entry_id:199137) $T_pM$ 和其[对偶空间](@entry_id:146945)，即[余切空间](@entry_id:270516) $T_p^*M$。

一个在点 $p$ 的 **$(r,s)$ 型张量** (tensor of type $(r,s)$) 是[张量积](@entry_id:140694)空间 $T_p^{(r,s)}M = (\otimes^r T_pM) \otimes (\otimes^s T_p^*M)$ 中的一个元素。这里，$r$ 称为张量的 **逆变阶** (contravariant rank)，$s$ 称为 **协变阶** (covariant rank)。根据这个定义：
-   一个 $(1,0)$ 型张量就是[切空间](@entry_id:199137) $T_pM$ 中的一个[切向量](@entry_id:265494)。
-   一个 $(0,1)$ 型张量就是[余切空间](@entry_id:270516) $T_p^*M$ 中的一个[余向量](@entry_id:157727)（或[1-形式](@entry_id:270392)）。
-   一个 $(0,0)$ 型张量是一个标量，即一个实数。
-   一个 $(0,2)$ 型张量是一个[双线性形式](@entry_id:746794) $T_p: T_pM \times T_pM \to \mathbb{R}$。

将这个代数概念推广到整个流形，我们便得到了 **[张量场](@entry_id:190170)** (tensor field) 的概念。一个 $(r,s)$ 型[张量场](@entry_id:190170) $T$ 是流形 $M$ 上的一个光滑[截面](@entry_id:154995) (smooth section)，它为每一点 $p \in M$ 指定一个该点的 $(r,s)$ 型张量 $T_p$。也就是说，$T$ 是[张量丛](@entry_id:203012) $T^{(r,s)}M = \bigsqcup_{p \in M} T_p^{(r,s)}M$ 的一个光滑[截面](@entry_id:154995)。

“光滑”这一要求至关重要。一个[截面](@entry_id:154995) $T$ 被认为是光滑的，当且仅当在任何[局部坐标](@entry_id:181200)卡 $(U, x^i)$ 中，它的分量函数都是光滑的 ($C^\infty$)。更精确地说，正如  中所阐明的，一个[截面](@entry_id:154995)的光滑性是一个局部性质。如果对于流形上的每一点，都存在一个包含该点的[局部平凡化](@entry_id:267993)邻域，使得该[截面](@entry_id:154995)在其中的分量函数是光滑的，那么这个[截面](@entry_id:154995)就是光滑的。由于不同[坐标卡](@entry_id:262338)之间的过渡函数是光滑的，因此在一个坐标系下分量是光滑的，在任何其他坐标系下也必然是光滑的。

为了进行具体计算，我们必须在局部坐标中表示[张量场](@entry_id:190170)。在一个[坐标邻域](@entry_id:276525) $U$ 中，点 $p$ 的坐标为 $(x^1, \dots, x^n)$。[切空间](@entry_id:199137) $T_pM$ 有一组自然基底 $\{\partial_1, \dots, \partial_n\}$，其中 $\partial_i = \frac{\partial}{\partial x^i}$。其[对偶空间](@entry_id:146945) $T_p^*M$ 相应地有一组对偶基底 $\{dx^1, \dots, dx^n\}$，满足 $dx^j(\partial_i) = \delta^j_i$（Kronecker delta）。于是，任意一个 $(r,s)$ 型[张量场](@entry_id:190170) $T$ 可以在该邻域中表示为其分量和基底[张量积](@entry_id:140694)的[线性组合](@entry_id:154743)：
$$
T(x) = T^{i_1 \dots i_r}_{\quad j_1 \dots j_s}(x) \ (\partial_{i_1} \otimes \dots \otimes \partial_{i_r}) \otimes (dx^{j_1} \otimes \dots \otimes dx^{j_s})
$$
此处我们使用了爱因斯坦求和约定，即成对出现的同名上下指标表示对该指标从 $1$ 到 $n$ 求和。函数 $T^{i_1 \dots i_r}_{\quad j_1 \dots j_s}(x)$ 就是 $T$ 在该坐标系下的 **分量** (components)。

张量作为一个几何对象，其本身是独立于坐标系选择的。这意味着，当我们在另一个坐标系 $(y^\alpha)$ 中观察同一个[张量场](@entry_id:190170)时，其分量会以一种特定的方式变换。假设坐标变换是 $y^\alpha = y^\alpha(x^1, \dots, x^n)$，其 Jacobian 矩阵为 $J^\alpha_i = \frac{\partial y^\alpha}{\partial x^i}$，逆 Jacobian 矩阵为 $K^i_\beta = \frac{\partial x^i}{\partial y^\beta}$。根据[链式法则](@entry_id:190743)，基底[向量和余向量](@entry_id:181128)的变换关系为：
$$
\partial_i = \frac{\partial y^\alpha}{\partial x^i} \frac{\partial}{\partial y^\alpha} = J^\alpha_i \frac{\partial}{\partial y^\alpha}
$$
$$
dx^j = \frac{\partial x^j}{\partial y^\beta} dy^\beta = K^j_\beta dy^\beta
$$
将这些关系代入张量的表达式，并要求张量本身不变，我们就可以推导出其分量的变换法则 。在新的 $y$-坐标系中，张量的分量 $T'^{\alpha_1 \dots \alpha_r}_{\quad \beta_1 \dots \beta_s}$ 与旧的 $x$-坐标系中的分量 $T^{i_1 \dots i_r}_{\quad j_1 \dots j_s}$ 之间的关系为：
$$
T'^{\alpha_1 \dots \alpha_r}_{\quad \beta_1 \dots \beta_s} = J^{\alpha_1}_{i_1} \dots J^{\alpha_r}_{i_r} \ K^{j_1}_{\beta_1} \dots K^{j_s}_{\beta_s} \ T^{i_1 \dots i_r}_{\quad j_1 \dots j_s}
$$
这个变换法则精确地定义了张量的本质。每一个上指标（逆变指标）都与一个 Jacobian 矩阵 $J$ 相乘，而每一个下指标（协变指标）都与一个逆 Jacobian 矩阵 $K$ 相乘。这解释了为何这些指标分别被称为 **逆变的** (contravariant) 和 **协变的** (covariant)。

### [张量场](@entry_id:190170)的基本运算

除了标准的线性运算（加法和标量乘法）外，[张量场](@entry_id:190170)还支持一些特有的运算，这些运算是其在几何与物理中应用的基础。

#### [张量积](@entry_id:140694)与缩并

两个[张量场](@entry_id:190170)可以进行 **[张量积](@entry_id:140694)** (tensor product) 运算。例如，一个 $(r,s)$ 型[张量场](@entry_id:190170) $T$ 和一个 $(p,q)$ 型[张量场](@entry_id:190170) $S$ 的[张量积](@entry_id:140694) $T \otimes S$ 是一个 $(r+p, s+q)$ 型[张量场](@entry_id:190170)。在局部坐标中，其分量就是分量的简单乘积：$(T \otimes S)^{i_1 \dots i_{r+p}}_{\quad j_1 \dots j_{s+q}} = T^{i_1 \dots i_r}_{\quad j_1 \dots j_s} S^{i_{r+1} \dots i_{r+p}}_{\quad j_{s+1} \dots j_{s+q}}$。

**缩并** (contraction) 是一个降低张量阶数的操作。它选取一个逆变指标和一个[协变](@entry_id:634097)指标，然后对它们求和（在[基底层](@entry_id:920664)面，相当于将一个向量输入到一个[余向量](@entry_id:157727)中）。例如，对一个 $(1,1)$ 型张量 $T = T^i_j \partial_i \otimes dx^j$ 进行缩并，得到一个[标量场](@entry_id:151443)（$(0,0)$ 型张量） $C(T) = T^i_i$。

#### 映照下的[张量变换](@entry_id:183453)：[前推与拉回](@entry_id:181877)

当存在一个[光滑映射](@entry_id:203730) $F: M \to N$ 时，我们自然会问：$M$ 上的[张量场](@entry_id:190170)与 $N$ 上的[张量场](@entry_id:190170)之间如何关联？这引出了前推和拉回的概念，其定义深刻地揭示了逆变与协变指标的内在差异 。

对于一个 $M$ 上的向量场 $X \in \mathfrak{X}(M)$，我们可以定义其 **前推** (pushforward)。在每一点 $p \in M$，切映射 $dF_p: T_pM \to T_{F(p)}N$ 将向量 $X_p$ 映为 $dF_p(X_p) \in T_{F(p)}N$。这样得到的对象 $(F_*X)_p = dF_p(X_p)$ 是一个沿着 $F$ 的向量场。然而，除非 $F$ 是一个微分同胚，否则 $F_*X$ 通常不是 $N$ 上的一个良定义的向量场。如果 $F$ 不是满射，那么[像空间](@entry_id:918062)之外的点没有对应的向量；如果 $F$ 不是[单射](@entry_id:183792)，那么一个点可能会被赋予多个不同的向量，导致定义不明确。

与此相反，对于 $N$ 上的[协变张量](@entry_id:634493)场，我们可以定义一个总是良定义的 **拉回** (pullback)。以一个 $N$ 上的[余向量](@entry_id:157727)场（即 $(0,1)$ 型[张量场](@entry_id:190170)）$\alpha \in \mathfrak{X}^*(N)$ 为例，其拉回 $F^*\alpha$ 是 $M$ 上的一个[余向量](@entry_id:157727)场。其定义方式非常自然：在任意点 $p \in M$，要确定 $(F^*\alpha)_p$ 对向量 $v \in T_pM$ 的作用，我们首先将 $v$ “前推”到 $T_{F(p)}N$ 中，得到 $dF_p(v)$，然后让 $\alpha$ 在 $F(p)$ 点的值作用于这个新向量：
$$
(F^*\alpha)_p(v) := \alpha_{F(p)}(dF_p(v))
$$
这个定义可以推广到任意 $(0,s)$ 型[张量场](@entry_id:190170) $\beta$：
$$
(F^*\beta)_p(v_1, \dots, v_s) := \beta_{F(p)}(dF_p(v_1), \dots, dF_p(v_s)) \quad \text{for } v_i \in T_pM
$$
这个操作之所以总是可行的，是因为[协变张量](@entry_id:634493)是以向量为“输入”的，而切映射 $dF_p$ 恰好提供了从 $T_pM$ 到 $T_{F(p)}N$ 的输入通道。

然而，对于[逆变张量](@entry_id:636697)（如向量场），不存在一个规范的拉回操作。尝试定义一个向量场 $Y$ 在 $N$ 上的拉回，需要在每点 $p \in M$ 从 $Y_{F(p)} \in T_{F(p)}N$ 构造一个向量 $(F^*Y)_p \in T_pM$。这需要一个从 $T_{F(p)}N$ 到 $T_pM$ 的“逆向”映射。除非 $F$ 是一个[局部微分同胚](@entry_id:203529)，否则 $dF_p$ 不可逆，这样一个规范的逆向映射一般不存在。这正是[协变与逆变](@entry_id:189600)张量在几何运算中的一个根本区别。

### [张量场](@entry_id:190170)的[微分](@entry_id:158422)

在欧氏空间中，我们可以通过对向量场的分量求[偏导数](@entry_id:146280)来描述其变化。但在弯曲的流形上，由于[基向量](@entry_id:199546)本身随位置变化，仅仅对分量求导数得到的结果不再是张量的分量。这一困难催生了两种重要的、概念上不同的[张量场](@entry_id:190170)[微分](@entry_id:158422)方法：[Lie 导数](@entry_id:171745)和[协变导数](@entry_id:152476)。

#### [Lie 导数](@entry_id:171745)

**[Lie 导数](@entry_id:171745)** (Lie derivative) $\mathcal{L}_X T$ 衡量了[张量场](@entry_id:190170) $T$ 沿着向量场 $X$ 的流（flow）的无穷小变化。它是一个完全内在的、不依赖于任何附加结构（如度量或联络）的导数。

[Lie 导数](@entry_id:171745)的核心性质是它在[张量代数](@entry_id:161671)上是一个导子，即满足针对[张量积](@entry_id:140694)的 Leibniz 法则：$\mathcal{L}_X(A \otimes B) = (\mathcal{L}_X A) \otimes B + A \otimes (\mathcal{L}_X B)$。基于此以及它在[标量场](@entry_id:151443)（$ \mathcal{L}_X f = X(f) $）和向量场（$ \mathcal{L}_X Y = [X,Y] $，[Lie 括号](@entry_id:636461)）上的定义，我们可以推导出 [Lie 导数](@entry_id:171745)作用于任意 $(r,s)$ 型[张量场](@entry_id:190170) $T$ 的分量表达式 。在局部坐标中，$(\mathcal{L}_X T)$ 的分量为：
$$
(\mathcal{L}_{X}T)^{i_{1}\cdots i_{r}}_{\quad j_{1}\cdots j_{s}} = X^{k}\partial_{k}T^{i_{1}\cdots i_{r}}_{\quad j_{1}\cdots j_{s}} - \sum_{p=1}^{r}T^{i_{1}\cdots \alpha \cdots i_{r}}_{\quad j_{1}\cdots j_{s}}\partial_{\alpha}X^{i_{p}} + \sum_{q=1}^{s}T^{i_{1}\cdots i_{r}}_{\quad j_{1}\cdots \beta \cdots j_{s}}\partial_{j_{q}}X^{\beta}
$$
其中，在第一个和式中，求和指标 $\alpha$ 替代了第 $p$ 个逆变指标 $i_p$ 的位置；在第二个和式中，求和指标 $\beta$ 替代了第 $q$ 个[协变](@entry_id:634097)指标 $j_q$ 的位置。这个公式的结构清晰地揭示了 [Lie 导数](@entry_id:171745)的构成：第一项是沿 $X$ 的[方向导数](@entry_id:189133)，后面两项则是由于[坐标基](@entry_id:270149)底本身被 $X$ 的流拖拽而产生的“修正项”，这些修正项涉及向量场 $X$ 分量的梯度。

#### [仿射联络](@entry_id:160152)与[协变导数](@entry_id:152476)

**[协变导数](@entry_id:152476)** (covariant derivative) 是另一种[微分](@entry_id:158422)[张量场](@entry_id:190170)的方式，它通过引入一个称为 **[仿射联络](@entry_id:160152)** (affine connection) 的附加结构 $\nabla$ 来实现。联络的目的是定义一种“平行移动”向量的方式，从而可以比较相邻点上的向量。

一个[仿射联络](@entry_id:160152) $\nabla$ 是一个映射 $\nabla: \mathfrak{X}(M) \times \mathfrak{X}(M) \to \mathfrak{X}(M)$，记为 $(X,Y) \mapsto \nabla_X Y$，它满足以下公理 ：
1.  对第一个参数 $X$ 是 $C^\infty(M)$-线性的：$\nabla_{fX_1+gX_2}Y = f\nabla_{X_1}Y + g\nabla_{X_2}Y$。
2.  对第二个参数 $Y$ 是 $\mathbb{R}$-线性的：$\nabla_X(aY_1+bY_2) = a\nabla_X Y_1 + b\nabla_X Y_2$。
3.  对第二个参数 $Y$ 满足 Leibniz 法则：$\nabla_X(fY) = (X[f])Y + f\nabla_X Y$。

值得注意的是，第二个参数的 Leibniz 法则中出现了导数项 $X[f]$，这意味着 $\nabla_X$ 作为一个算子不是 $C^\infty(M)$-线性的。因此，联络本身 **不是** 一个张量。我们可以用一组称为 **Christoffel 符号** (Christoffel symbols) 的函数 $\Gamma^k_{ij}$ 来描述联络在局部坐标中的行为，其定义为 $\nabla_{\partial_i}\partial_j = \Gamma^k_{ij}\partial_k$。Christoffel 符号不是张量分量，它们在坐标变换下的变换法则非常复杂，包含一个非齐次的二阶导数项。

一个经典的例子可以明确说明这一点 。考虑一个从[笛卡尔坐标](@entry_id:167698) $(x^1, x^2)$ 到一个[曲线坐标](@entry_id:178535) $(u,v)$ 的变换。在平坦的[欧氏空间](@entry_id:138052)中，[笛卡尔坐标](@entry_id:167698)下的 Christoffel 符号 $\Gamma^k_{ij}$ 均为零。如果 $\Gamma^k_{ij}$ 是一个 $(1,2)$ 型张量的分量，那么在新坐标系中它们也应为零。然而，直接从新坐标系的度量计算出的 Christoffel 符号 $\bar{\Gamma}^k_{ij}$ 却不为零。例如，对于变换 $x^1=u^2-v^2, x^2=2uv$，我们发现 $\bar{\Gamma}^1_{11} = \frac{u}{u^2+v^2}$，这与[张量变换](@entry_id:183453)预测的零值有明确的偏差。这个偏差 $\bar{\Gamma}^1_{11} - 0$ [直接证明](@entry_id:141172)了 Christoffel 符号的非张量性。

一旦定义了向量场的[协变导数](@entry_id:152476)，就可以通过要求其满足 Leibniz 法则并与缩并运算可交换，将其唯一地推广到任意 $(r,s)$ 型[张量场](@entry_id:190170)上。

### [张量场](@entry_id:190170)定义的几何结构

[张量场](@entry_id:190170)的真正威力在于它们能够为流形赋予丰富的几何结构。最重要的例子包括度量张量、联络和[辛形式](@entry_id:165896)。

#### 度量张量与(伪)[黎曼流形](@entry_id:261160)

一个 **(伪)[黎曼度量](@entry_id:754359)** ((pseudo-)Riemannian metric) $g$ 是一个光滑、对称、非退化的 $(0,2)$ 型[张量场](@entry_id:190170) 。
-   **对称性** 意味着 $g(X,Y) = g(Y,X)$。
-   **非退化性** 意味着，如果在某点 $p$，对于所有 $Y \in T_pM$ 都有 $g_p(X,Y)=0$，那么必有 $X=0$。
如果 $g_p(X,X) > 0$ 对所有非[零向量](@entry_id:156189) $X \in T_pM$ 成立，则称该度量是正定的，流形 $(M,g)$ 称为 **[黎曼流形](@entry_id:261160)** (Riemannian manifold)。如果 $g_p$ 只是非退化但非正定（即存在 $X$ 使得 $g_p(X,X)$ 可以为负或零），则称其为 **[伪黎曼度量](@entry_id:185204)** (pseudo-Riemannian metric)，流形 $(M,g)$ 称为[伪黎曼流形](@entry_id:184750)。广义相对论中的时空就是[洛伦兹流形](@entry_id:162024)，一种重要的[伪黎曼流形](@entry_id:184750)。

度量张量 $g$ 在每一点的切空间上定义了一个[内积](@entry_id:750660)（或伪[内积](@entry_id:750660)），从而使我们能够测量向量的长度和它们之间的角度。非退化性保证了所谓的 **[音乐同构](@entry_id:199976)** (musical isomorphisms) ：
-   **降号** (flat) 映射 $\flat: TM \to T^*M$，定义为 $X^\flat = g(X, \cdot)$。
-   **升号** (sharp) 映射 $\sharp: T^*M \to TM$，是 $\flat$ 的逆映射，$\alpha^\sharp = g^{-1}(\alpha, \cdot)$。
这些同构在哈密顿和拉格朗日力学中扮演着核心角色，它们在切丛和余切丛之间建立了联系。此外，在[黎曼流形](@entry_id:261160)中，每一点的单位切球面 $S_p = \{v \in T_pM : g_p(v,v)=1\}$ 是一个[紧集](@entry_id:147575)，这是许多分析和拓扑结论的基础 。

#### Levi-Civita 联络

引入度量张量后，便可以从中确定一个唯一的、与度量结构“兼容”的“自然”联络。这就是 **[黎曼几何基本定理](@entry_id:189185)** (Fundamental Theorem of Riemannian Geometry)  。该定理指出，在任何一个(伪)[黎曼流形](@entry_id:261160) $(M,g)$上，存在唯一一个[仿射联络](@entry_id:160152) $\nabla$，它同时满足以下两个条件：
1.  **无挠** (Torsion-free): $T^\nabla(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y] = 0$。在[局部坐标](@entry_id:181200)中，这等价于 Christoffel 符号对其下指标是对称的，即 $\Gamma^k_{ij} = \Gamma^k_{ji}$ 。
2.  **度量兼容** (Metric-compatible): $\nabla g = 0$。这意味着在[协变导数](@entry_id:152476)下度量张量是“常数”。这一性质的一个重要推论是，沿任意曲线的平行移动保持向量的[内积](@entry_id:750660)、长度和角度不变 。

这个唯一的联络称为 **Levi-Civita 联络**。它为(伪)黎曼[流形上的微积分](@entry_id:270207)提供了一套完整的工具，包括平行移动、[测地线](@entry_id:269969)（作为“直线”的推广）和曲率（衡量流形弯曲程度）。需要强调的是，尽管 Levi-Civita 联络在[欧氏空间](@entry_id:138052)的[笛卡尔坐标](@entry_id:167698)下其 Christoffel 符号为零，但在一般的弯曲流形上，不存在一个开集上的坐标系能使其所有 Christoffel 符号都为零。这种局部“平坦化”的障碍正是由非零的 **[黎曼曲率张量](@entry_id:160189)** 描述的。

#### 微分形式与[辛流形](@entry_id:161608)

**[微分形式](@entry_id:146747)** (Differential forms) 是一类特别重要的[张量场](@entry_id:190170)——它们是全反对称的[协变张量](@entry_id:634493)场 。一个 $k$-形式是 $\wedge^k T^*M$ 的一个光滑[截面](@entry_id:154995)。[微分形式](@entry_id:146747)代数的核心运算是 **[外积](@entry_id:147029)** (wedge product) $\wedge$，它是一个[双线性](@entry_id:146819)、结合的、满足分次[交换律](@entry_id:141214)（$\alpha \wedge \beta = (-1)^{k\ell} \beta \wedge \alpha$，其中 $\alpha$ 是 $k$-形式，$\beta$ 是 $\ell$-形式）的运算。一个关键性质是，任何 1-形式 $\theta$ 与自身的[外积](@entry_id:147029)为零：$\theta \wedge \theta = 0$ 。

微分形式是定义另一类重要几何结构的基础。一个 **[辛流形](@entry_id:161608)** (symplectic manifold) $(M, \omega)$ 是一个偶数维[光滑流形](@entry_id:160799)，其上装备了一个称为 **[辛形式](@entry_id:165896)** (symplectic form) 的2-形式 $\omega$，该形式满足两个条件 ：
1.  **闭性** (Closed): $d\omega = 0$，其中 $d$ 是外微分算子。
2.  **非退化性** (Non-degenerate): 在每一点 $p \in M$，$\omega_p$ 作为 $T_pM$ 上的[双线性形式](@entry_id:746794)是非退化的。

非退化性在此处的含义与度量张量类似，但后果却截然不同。由于 $\omega$ 是一个[2-形式](@entry_id:188008)，它必然是反对称的，即 $\omega(X,X)=0$。非退化性意味着，如果 $X \neq 0$，则必存在 $Y$ 使得 $\omega(X,Y) \neq 0$。这个条件有几个等价的表述和深刻的推论 ：
-   它等价于映射 $\omega^\flat: TM \to T^*M$（定义为 $X \mapsto i_X\omega = \omega(X, \cdot)$）是一个丛同构。
-   在 $2n$ 维流形上，它等价于 $n$ 次[外积](@entry_id:147029) $\omega^n = \omega \wedge \dots \wedge \omega$ 是一个处处非零的[体积形式](@entry_id:203000)。
-   最重要的推论是，它保证了对于流形上的任意一个光滑函数 $H$（称为 **[哈密顿量](@entry_id:144286)**），都存在一个 **唯一** 的向量场 $X_H$（称为 **哈密顿向量场**），满足方程 $i_{X_H}\omega = dH$。

最后这个性质是辛几何成为经典力学（特别是[哈密顿力学](@entry_id:146202)）的现代理论框架的基石。它在流形的几何结构（由 $\omega$ 定义）和其上的动力学（由 $H$ 和 $X_H$ 描述）之间建立了一座至关重要的桥梁。