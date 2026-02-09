## 引言
在微分几何的探索中，当我们掌握了切丛与向量场的概念后，目光自然会投向它们的对偶结构。正如向量空间的对偶空间揭示了其内在的代数特性，切丛的对偶——余切丛，以及在其上定义的1-形式，为我们理解积分理论、经典力学乃至现代物理学提供了不可或缺的语言和工具。本文旨在深入探讨这些对偶对象的核心变换行为——拉回（pullback），它描述了1-形式如何在光滑映射下从一个流形“传递”到另一个流形。本文旨在解决如何以一种与坐标无关的、内在的方式来理解和计算这种变换，并揭示其背后深刻的几何与物理意义。

通过本文的学习，你将全面掌握余切丛与1-形式的理论框架及其应用。在第一部分“原理与机制”中，我们将从基本定义出发，建立余切空间、余切丛和光滑1-形式的严格概念，并详细阐述拉回的定义、代数性质及坐标表示。接着，在“应用与跨学科联系”部分，我们将展示这些抽象工具的巨大威力，探讨它们如何统一地描述曲线积分、定义黎曼流形上的梯度场、构建哈密顿力学的相空间，并揭示流形的拓扑不变量。最后，通过“动手实践”环节，你将通过具体计算来巩固和深化对拉回运算的理解。让我们首先进入第一章，探究其背后的基本原理与机制。

## 原理与机制

在对光滑流形上的切丛和向量场进行了研究之后，我们自然会转向其对偶结构。正如线性代数中向量空间的对偶空间揭示了其深刻的结构特性一样，切丛的对偶——余切丛——以及作用于其上的1-形式，为我们理解微分几何、积分理论乃至理论物理提供了至关重要的语言和工具。本章将系统地阐述余切丛的定义、其作为向量丛的结构，并深入探讨1-形式及其在光滑映射下的核心变换行为——拉回（pullback）。

### 余切空间：切空间的对偶

我们从单点上的构造开始。给定一个光滑流形 $M$ 和其上一点 $p$，我们已经熟悉了在该点的**切空间** $T_pM$。可以将 $T_pM$ 中的一个元素（一个切向量）视为一个作用于 $M$ 上光滑函数代数 $C^\infty(M)$ 的**导子**（derivation），它是一个线性映射 $X: C^\infty(M) \to \mathbb{R}$，并满足莱布尼兹法则 [@problem_id:3069017]。

基于此，我们定义在点 $p$ 的**余切空间** (cotangent space)，记作 $T_p^*M$，它正是切空间 $T_pM$ 的对偶向量空间。

**定义 (余切空间)**. 对于流形 $M$ 上的任意一点 $p$，其余切空间 $T_p^*M$ 是 $T_pM$ 的对偶空间，即由所有从 $T_pM$ 到 $\mathbb{R}$ 的线性映射（或称线性泛函）构成的向量空间：
$$ T_p^*M := \operatorname{Hom}_{\mathbb{R}}(T_pM, \mathbb{R}) $$

$T_p^*M$ 中的元素被称为**余切向量** (cotangent vector)、**余向量** (covector) 或**在点 $p$ 的1-形式** (1-form at $p$) [@problem_id:3069024]。如果 $\alpha \in T_p^*M$ 是一个余向量，$v \in T_pM$ 是一个切向量，则 $\alpha$ 对 $v$ 的作用记为 $\alpha(v)$ 或 $\langle \alpha, v \rangle$，其结果是一个实数。这种配对关系 $\langle \cdot, \cdot \rangle: T_p^*M \times T_pM \to \mathbb{R}$ 是双线性的。

一个自然而重要的问题是：切空间 $T_pM$ 和其对偶空间 $T_p^*M$ 是否“相同”？从有限维向量空间的角度看，它们具有相同的维度，因此它们是同构的。然而，在流形的光滑结构自身提供的框架内，并不存在一个**典范的**（canonical）同构。也就是说，我们无法在不引入额外结构（如黎曼度量）的情况下，以一种与坐标选取无关的自然方式来认同这两个空间 [@problem_id:3069024]。选择一个黎曼度量 $g_p$ 会诱导出一个特定的同构（音乐同构），但这依赖于度量的选择。

最重要的余向量例子之一是光滑函数的**微分**。给定一个光滑函数 $f \in C^\infty(M)$，它在点 $p$ 的微分 $df_p$ 定义为一个作用于切向量 $X_p \in T_pM$ 的线性泛函：
$$ df_p(X_p) := X_p(f) $$
根据导子的定义，这个映射对于 $X_p$ 显然是线性的，因此 $df_p$ 确实是 $T_p^*M$ 的一个元素。这澄清了一个常见的误解：$df_p$ 是一个余向量，而不是一个切向量 [@problem_id:3069024]。

### 余切丛及其光滑结构

正如我们将所有切空间“捆绑”在一起构成切丛 $TM$ 一样，我们也可以将所有余切空间集结起来，形成**余切丛** (cotangent bundle) $T^*M$。

**定义 (余切丛)**. 流形 $M$ 的余切丛 $T^*M$ 是其所有余切空间的无交并集：
$$ T^*M = \bigsqcup_{p \in M} T_p^*M $$
与之相伴的还有一个典范的**投影映射** $\pi: T^*M \to M$，它将任何余向量 $\alpha_p \in T_p^*M$ 映射到其基点 $p$，即 $\pi(\alpha_p) = p$。

然而，$T^*M$ 不仅仅是一个集合，它本身就是一个 $2n$ 维的光滑流形（其中 $n = \dim M$），并且是一个秩为 $n$ 的**光滑向量丛**。这意味着 $T^*M$ 局部上看起来像一个乘积空间 $U \times \mathbb{R}^n$ [@problem_id:3069055]。这个结构是通过 $M$ 上的光滑图卡（charts）来构建的。

假设 $(U, x)$ 是 $M$ 上的一个局部坐标图，其中 $x = (x^1, \dots, x^n)$。在 $U$ 中的每一点 $p$，坐标向量场 $\{\frac{\partial}{\partial x^1}|_p, \dots, \frac{\partial}{\partial x^n}|_p\}$ 构成了 $T_pM$ 的一组基。其对偶基 $\{dx^1|_p, \dots, dx^n|_p\}$ 则构成了 $T_p^*M$ 的一组基，其定义满足 $dx^i|_p(\frac{\partial}{\partial x^j}|_p) = \delta^i_j$。

任何余向量 $\alpha_p \in T_p^*M$ 都可以唯一地表示为这个对偶基的线性组合：
$$ \alpha_p = \sum_{i=1}^n \xi_i \, dx^i|_p $$
其中系数 $(\xi_1, \dots, \xi_n) \in \mathbb{R}^n$ 是 $\alpha_p$ 在该基下的分量。这些分量可以通过将 $\alpha_p$ 作用于 $T_pM$ 的基向量来确定 [@problem_id:3069026]：
$$ \xi_j = \alpha_p\left(\frac{\partial}{\partial x^j}\bigg|_p\right) $$
这就在 $\pi^{-1}(U)$ 上建立了一套局部坐标。一个点 $\alpha_p \in \pi^{-1}(U)$ 的坐标可以表示为 $(x^1(p), \dots, x^n(p), \xi_1, \dots, \xi_n) \in \mathbb{R}^{2n}$。这个构造给出了一个**局部平凡化** (local trivialization) $\Phi_U: \pi^{-1}(U) \to U \times \mathbb{R}^n$，它是一个保持纤维的微分同胚，并且在每个纤维上都是线性同构 [@problem_id:3069055]。

当两个坐标图 $(U, x)$ 和 $(V, y)$ 重叠时，我们需要考察余向量分量的变换法则。设在 $x$ 坐标系下分量为 $\xi_i$，在 $y$ 坐标系下分量为 $\eta_j$。利用基向量的变换法则 $\frac{\partial}{\partial y^j} = \sum_i \frac{\partial x^i}{\partial y^j} \frac{\partial}{\partial x^i}$ 和 $\eta_j = \alpha_p(\frac{\partial}{\partial y^j}|_p)$，我们得到：
$$ \eta_j = \alpha_p\left(\sum_{i=1}^n \frac{\partial x^i}{\partial y^j}(p) \frac{\partial}{\partial x^i}\bigg|_p\right) = \sum_{i=1}^n \frac{\partial x^i}{\partial y^j}(p) \, \alpha_p\left(\frac{\partial}{\partial x^i}\bigg|_p\right) = \sum_{i=1}^n \xi_i \frac{\partial x^i}{\partial y^j}(p) $$
这个变换法则称为**协变** (covariant) 变换法则 [@problem_id:3069026]。它与切向量分量的**逆变** (contravariant) 变换法则 $\tilde{v}^j = \sum_i v^i \frac{\partial y^j}{\partial x^i}$ 正好相反。这两种互补的变换法则是至关重要的，它们保证了余向量与向量的配对 $\alpha(v) = \sum_i \xi_i v^i$ 是一个不依赖于坐标系选择的标量（几何不变量）。例如，通过计算可以验证，在一个坐标系下算出的值 $\sum_i \xi_i v^i$ 和在另一个坐标系下算出的值 $\sum_j \eta_j \tilde{v}^j$ 是完全相等的 [@problem_id:3069051]。

### 光滑1-形式

全局上，一个**光滑1-形式** (smooth 1-form) 是余切丛的一个光滑截面。

**定义 (光滑1-形式)**. 流形 $M$ 上的一个光滑1-形式 $\alpha$ 是一个光滑映射 $\alpha: M \to T^*M$，使得对于所有 $p \in M$，$\pi \circ \alpha(p) = p$。

这个定义意味着，一个1-形式 $\alpha$ 为流形上的每一点 $p$ 都指定了一个余向量 $\alpha_p \in T_p^*M$，并且这种指定是“光滑的”。“光滑”的确切含义是，当在局部坐标 $(U, x)$ 中将 $\alpha$ 写成 $\alpha = \sum_{i=1}^n a_i(x) dx^i$ 时，所有的系数函数 $a_i: U \to \mathbb{R}$ 都是光滑函数 [@problem_id:3069025]。

还有一个等价的判别光滑性的方法：一个1-形式 $\alpha$ 是光滑的，当且仅当对于 $M$ 上的任何光滑向量场 $X$，由 $p \mapsto \alpha_p(X_p)$ 定义的函数 $M \to \mathbb{R}$ 是一个光滑函数 [@problem_id:3069025]。

### 1-形式的拉回

1-形式的一个核心特性是它们可以通过光滑映射“拉回”。与将切向量沿映射方向“前推”不同，1-形式是“逆着”映射方向从目标流形“拉回”到源流形。

#### 微分（前推）

为了定义拉回，我们首先需要定义光滑映射的**微分** (differential) 或**前推** (pushforward)。设 $F: M \to N$ 是一个光滑映射。在每一点 $p \in M$，它诱导了一个从 $T_pM$ 到 $T_{F(p)}N$ 的线性映射 $dF_p$。

**定义 (微分/前推)**. 设 $F: M \to N$ 是光滑映射，$p \in M$，$X_p \in T_pM$。$X_p$ 的前推 $dF_p(X_p)$ 是 $T_{F(p)}N$ 中的一个切向量，其定义为：对于任意光滑函数 $g \in C^\infty(N)$，
$$ (dF_p(X_p))(g) := X_p(g \circ F) $$
这个定义非常自然：$dF_p(X_p)$ 在 $F(p)$ 点对函数 $g$ 的“作用”，就是原始向量 $X_p$ 在 $p$ 点对复合函数 $g \circ F$ 的作用。这是链式法则在导子层面上的体现 [@problem_id:3069017]。

#### 拉回的定义与性质

有了前推的概念，我们现在可以定义1-形式的拉回。

**定义 (拉回)**. 设 $F: M \to N$ 是光滑映射，$\alpha$ 是 $N$ 上的一个1-形式。$\alpha$ 沿 $F$ 的**拉回** (pullback) $F^*\alpha$ 是 $M$ 上的一个1-形式，其在点 $p \in M$ 对切向量 $X_p \in T_pM$ 的作用定义为：
$$ (F^*\alpha)_p(X_p) := \alpha_{F(p)}(dF_p(X_p)) $$
这个定义的直观意义是：要想知道拉回形式 $(F^*\alpha)_p$ 如何作用于向量 $X_p$，我们先把 $X_p$ “前推”到目标流形 $N$ 中，得到向量 $dF_p(X_p) \in T_{F(p)}N$，然后再让原始的1-形式 $\alpha$ 在 $F(p)$ 点作用于这个前推后的向量 [@problem_id:3069017] [@problem_id:3069024]。

拉回具有重要的**函子性** (functoriality)。如果 $G: P \to N$ 和 $F: N \to M$ 是光滑映射，那么复合映射的拉回等于拉回的复合，但顺序相反：
$$ (F \circ G)^* = G^* \circ F^* $$
这是链式法则 $d(F \circ G)_r = dF_{G(r)} \circ dG_r$ 的直接推论 [@problem_id:3069024]。

#### 坐标下的拉回

拉回的抽象定义在局部坐标下有一个非常具体和有用的表达式。假设 $F: M \to N$ 在局部坐标 $x$ 和 $y$ 下由 $y^i = F^i(x)$ 给出，而 $N$ 上的1-形式 $\alpha$ 表示为 $\alpha = \sum_i \alpha_i(y) dy^i$。我们想计算 $M$ 上的拉回形式 $F^*\alpha = \sum_k (F^*\alpha)_k(x) dx^k$ 的分量 $(F^*\alpha)_k(x)$。

根据定义和分量的求法：
$$ (F^*\alpha)_k(x) = (F^*\alpha)_x\left(\frac{\partial}{\partial x^k}\right) = \alpha_{F(x)}\left(dF_x\left(\frac{\partial}{\partial x^k}\right)\right) $$
利用链式法则，我们知道 $dF_x(\frac{\partial}{\partial x^k}) = \sum_i \frac{\partial F^i}{\partial x^k}(x) \frac{\partial}{\partial y^i}$。代入上式并利用 $\alpha_{F(x)}$ 的线性和 $\alpha_{F(x)}(\frac{\partial}{\partial y^i}) = \alpha_i(F(x))$，我们得到：
$$ (F^*\alpha)_k(x) = \sum_{i=1}^n \alpha_i(F(x)) \frac{\partial F^i}{\partial x^k}(x) $$
这个公式是进行具体计算的基石 [@problem_id:3069035]。

#### 拉回与外微分的交换性

拉回运算与外微分 $d$ 有着优美的关系。对于任何光滑函数 $f \in C^\infty(N)$，我们有：
$$ F^*(df) = d(f \circ F) $$
这个性质表明，先对函数求微分再拉回，与先将函数拉回（通过复合）再求微分的结果是相同的。这本质上就是链式法则的另一种表述。通过在局部坐标中进行直接计算，可以轻松验证这一恒等式 [@problem_id:3069030]。

### 应用与几何解释

#### 到子流形的限制

一个特别重要且直观的拉回应用是处理嵌入子流形。设 $S \subset M$ 是一个嵌入子流形，其包含映射为 $i: S \hookrightarrow M$。对于 $M$ 上的任意1-形式 $\alpha$，其拉回 $i^*\alpha$ 是 $S$ 上的一个1-形式，通常称为 $\alpha$ **在 $S$ 上的限制** [@problem_id:3069036]。

根据拉回的定义，对任意 $p \in S$ 和 $v \in T_pS$，我们有：
$$ (i^*\alpha)_p(v) = \alpha_{i(p)}(di_p(v)) = \alpha_p(v) $$
这里我们用到了 $i(p)=p$ 和 $di_p$ 是切空间 $T_pS$ 到 $T_pM$ 的包含映射。这个结果的几何意义非常清晰：$i^*\alpha$ 就是将 $\alpha$ 的作用域从整个切空间 $T_pM$ 限制到其子空间 $T_pS$ 上。

在适应子流形的局部坐标（“切片坐标”）中，这个操作尤为简单。如果 $M$ 的坐标 $(x^1, \dots, x^m)$ 使得 $S$ 由 $x^{k+1} = \dots = x^m = 0$ 给出，那么对于 $\alpha = \sum_{j=1}^m a_j(x) dx^j$，其限制为：
$$ i^*\alpha = \sum_{j=1}^k a_j(x^1, \dots, x^k, 0, \dots, 0) dx^j $$
所有与法向（$j > k$）相关的分量都消失了，因为在 $S$ 上 $d(x^j \circ i) = d(0) = 0$ [@problem_id:3069036]。

在黎曼几何的背景下，如果 $\alpha$ 是由向量场 $X$ 通过音乐同构产生的1-形式，即 $\alpha = X^\flat = g(X, \cdot)$，那么 $i^*\alpha$ 的作用在 $v \in TS$ 上就是 $g(X,v)$。这等于 $g(X^\top, v)$，其中 $X^\top$ 是 $X$ 沿着 $TS$ 的切向分量。这再次说明，拉回到子流形的过程只保留了与子流形相切的信息 [@problem_id:3069036]。

#### 拉回的消失

拉回运算提供了一个强大的几何工具来判断某些量是否为零。一个非零的1-形式 $\alpha$ 在拉回后可能变为零形式。这种情况的发生有着深刻的几何原因。

从定义 $(F^*\alpha)_p(X_p) = \alpha_{F(p)}(dF_p(X_p))$ 看出，$F^*\alpha$ 在点 $p$ 为零，意味着 $\alpha_{F(p)}$ 在 $dF_p$ 的像空间 $\operatorname{Im}(dF_p) \subseteq T_{F(p)}N$ 上恒为零。也就是说，$\operatorname{Im}(dF_p)$ 必须包含在余向量 $\alpha_{F(p)}$ 的核（kernel）中。

如果对于所有 $p \in M$ 都满足这个条件，那么 $F^*\alpha$ 就是一个零形式。这通常发生在 $F$ 是一个降秩映射时，即 $\operatorname{rank}(dF_p) < \dim N$。以下是一些典型例子 [@problem_id:3069044]：

1.  **嵌入到更高维度**：考虑映射 $F: \mathbb{R}^2 \to \mathbb{R}^3$，$F(x,y) = (x,y,0)$，以及1-形式 $\alpha = dz$。$dF$ 的像空间是 $\mathbb{R}^3$ 中的 $xy$-平面。由于 $dz$ 在任何方向不含 $z$ 分量的向量上都为零，所以 $dz$ 在 $xy$-平面上为零。因此，$F^* (dz) \equiv 0$。

2.  **投影到更低维度子空间**：考虑映射 $F: \mathbb{R}^2 \to \mathbb{R}^2$，$F(x,y) = (x,0)$，以及1-形式 $\alpha = dy$。$dF$ 的像空间是 $x$-轴。由于 $dy$ 在任何方向不含 $y$ 分量的向量上都为零，所以 $dy$ 在 $x$-轴上为零。因此，$F^*(dy) \equiv 0$。

3.  **常值映射**：如果 $F: M \to N$ 是一个常值映射 $F(p) = q_0$，那么 $dF_p$ 是零映射。$dF_p$ 的像只包含零向量。任何1-形式在零向量上都取值为零，因此对于任意 $\alpha$，都有 $F^*\alpha \equiv 0$。

这些例子揭示了拉回运算如何探测和反映光滑映射的几何退化。通过考察一个1-形式的拉回是否为零，我们可以获得关于映射微分的像空间与该1-形式的核之间关系的宝贵信息。