## 引言
从[有界算子](@entry_id:264879)到更为普遍且应用广泛的[无界算子](@entry_id:144655)，伴随算子的概念经历了深刻的演变，成为现代泛函分析的基石。对于[微分算子](@entry_id:140145)等核心[无界算子](@entry_id:144655)而言，其伴随算子的精确定义和性质是理解量子力学、[偏微分方程](@entry_id:141332)和谱理论的关键。与定义在整个希尔伯特空间上的[有界算子](@entry_id:264879)不同，[无界算子](@entry_id:144655)通常只定义在一个稠密的[子空间](@entry_id:150286)上，这使得伴随算子的构建变得更为精细和复杂，尤其是在处理定义域和边界条件时。本文旨在系统地阐明这一过渡，填补从简单情况到复杂现实的理论鸿沟。

通过本文的学习，读者将深入理解稠密定义[无界算子](@entry_id:144655)的伴随算子的理论框架。**原理与机制**一章将奠定理论基础，详细阐述伴随算子的定义、稠密定义域的重要性、闭性等基本性质，并区分对称与自伴这两个核心概念。**应用与跨学科联系**一章将展示该理论如何在量子力学、[偏微分方程](@entry_id:141332)和[随机分析](@entry_id:188809)等领域发挥关键作用，揭示抽象数学与具体科学问题的深刻联系。最后，**动手实践**部分提供了一系列精心设计的问题，帮助读者将理论知识应用于具体算例，巩固理解。让我们首先从第一性原理出发，严格构建稠密定义[无界算子](@entry_id:144655)的[伴随算子](@entry_id:140236)。

## 原理与机制

在从[有界算子](@entry_id:264879)过渡到更广泛且应用更丰富的[无界算子](@entry_id:144655)领域时，伴随算子的概念变得更加精细和微妙。对于定义在整个[希尔伯特空间](@entry_id:261193)上的[有界线性算子](@entry_id:180446) $A$，其伴随算子 $A^*$ 可以唯一地通过关系式 $\langle Ax, y \rangle = \langle x, A^*y \rangle$ 对所有 $x, y \in H$ 来定义。然而，对于[无界算子](@entry_id:144655)，其定义域 $D(T)$ 是[希尔伯特空间](@entry_id:261193) $H$ 的一个真[子空间](@entry_id:150286)，这引入了新的复杂性。本章旨在系统地阐述稠密定义[无界算子](@entry_id:144655)的伴随算子的核心原理和关键机制。

### 伴随算子的定义与稠密定义域

我们首先构建[无界算子](@entry_id:144655)伴随的严格定义。令 $T$ 是一个在[希尔伯特空间](@entry_id:261193) $H$ 中定义的[线性算子](@entry_id:149003)，其定义域为 $D(T)$。我们希望寻找一个算子 $T^*$ 及其定义域 $D(T^*)$，使得对于所有 $x \in D(T)$ 和 $y \in D(T^*)$，以下关系成立：
$$
\langle Tx, y \rangle = \langle x, T^*y \rangle
$$
为此，我们考虑一个给定的 $y \in H$。我们可以定义一个作用于 $D(T)$ 上的[线性泛函](@entry_id:276136) $L_y$：
$$
L_y(x) = \langle Tx, y \rangle, \quad x \in D(T)
$$
如果这个泛函 $L_y$ 在 $D(T)$ 上是连续的（即有界的），那么根据[里斯表示定理](@entry_id:140012)的一个推广，存在一个唯一的向量 $z \in H$，使得 $L_y(x) = \langle x, z \rangle$ 对于所有 $x \in D(T)$ 均成立。这就引出了[伴随算子](@entry_id:140236)的正式定义：

**定义（伴随算子）**：令 $T$ 为在[希尔伯特空间](@entry_id:261193) $H$ 中定义域为 $D(T)$ 的线性算子。其**[伴随算子](@entry_id:140236) (adjoint operator)** $T^*$ 的定义域 $D(T^*)$ 由所有满足以下条件的向量 $y \in H$ 构成：存在一个向量 $z \in H$ 使得对于所有 $x \in D(T)$，都有 $\langle Tx, y \rangle = \langle x, z \rangle$。
对于每个这样的 $y \in D(T^*)$，如果 $D(T)$ 在 $H$ 中是稠密的，则向量 $z$ 是唯一的。我们定义 $T^*y = z$。

定义中**稠密定义域 (densely defined domain)** 的要求至关重要，它保证了 $T^*y$ 的唯一性，从而使 $T^*$ 成为一个适定 (well-defined) 的算子。若 $D(T)$ 不是稠密的，则 $D(T)$ 的正交补 $D(T)^\perp$ 中包含非零向量。如果 $\langle Tx, y \rangle = \langle x, z \rangle$ 对所有 $x \in D(T)$ 成立，那么对于任意 $z_0 \in D(T)^\perp$，我们也有：
$$
\langle x, z + z_0 \rangle = \langle x, z \rangle + \langle x, z_0 \rangle = \langle x, z \rangle
$$
因为 $x \in D(T)$ 且 $z_0 \in D(T)^\perp$ 意味着 $\langle x, z_0 \rangle = 0$。这意味着如果 $z$ 是 $y$ 的一个伴随像，那么 $z$ 加上 $D(T)^\perp$ 中的任意向量都是 $y$ 的伴随像，导致 $T^*y$ 不是一个唯一的向量，而是一个仿射[子空间](@entry_id:150286)。

为了具体理解这一点，我们可以考察一个定义在非[稠密子空间](@entry_id:261392)上的简单算子 [@problem_id:1885431]。考虑希尔伯特空间 $H = \mathbb{C}^2$，以及[恒等算子](@entry_id:204623) $Tf=f$，其定义域 $D(T)$ 是由向量 $(1,1)$ 生成的一维[子空间](@entry_id:150286)，即 $D(T) = \{ (\lambda, \lambda) \mid \lambda \in \mathbb{C} \}$。这个定义域在 $\mathbb{C}^2$ 中显然不是稠密的。对于任意 $y = (y_1, y_2) \in \mathbb{C}^2$，我们寻找所有满足 $\langle Tx, y \rangle = \langle x, z \rangle$ 的 $z=(z_1, z_2)$。对于任意 $x=(\lambda, \lambda) \in D(T)$，该条件变为：
$$
\langle (\lambda, \lambda), (y_1, y_2) \rangle = \langle (\lambda, \lambda), (z_1, z_2) \rangle
$$
$$
\lambda \overline{y_1} + \lambda \overline{y_2} = \lambda \overline{z_1} + \lambda \overline{z_2}
$$
由于此式对所有 $\lambda \in \mathbb{C}$ 成立，我们必须有 $\overline{y_1} + \overline{y_2} = \overline{z_1} + \overline{z_2}$，取共轭后得到 $y_1 + y_2 = z_1 + z_2$。这意味着满足条件的 $z$ 并不是一个点，而是满足 $z_1 + z_2 = \text{const}$ 的一条直线。因此，伴随算子是多值的。这个例子清晰地表明，为了确保伴随算子是一个从向量到向量的唯一映射，即一个真正的算子，我们必须要求原[算子的定义域](@entry_id:152686)在[希尔伯特空间](@entry_id:261193)中是稠密的。

### 计算[伴随算子](@entry_id:140236)：技巧与实例

计算伴随算子 $T^*$ 的核心任务是，对于给定的 $y \in D(T^*)$，找出它的像 $T^*y$ 的表达式，并确定 $D(T^*)$ 的具体形式。这个过程通常遵循一个通用策略：从[内积](@entry_id:158127) $\langle Tx, y \rangle$ 出发，通过代数或分析的变换（如[分部求和](@entry_id:185335)或[分部积分](@entry_id:136350)），将算子 $T$ 的作用从 $x$ “移动”到 $y$ 上，最终得到 $\langle x, z \rangle$ 的形式。在这个过程中出现的 $z$ 就是 $T^*y$，而使得整个变换合法且边界项消失的对 $y$ 的约束条件，则定义了 $D(T^*)$。

#### 实例：序列空间上的差分算子

考虑希尔伯特空间 $\ell^2(\mathbb{Z})$，以及定义在有限支撑序列（即只有有限个非零项的序列）构成的[稠密子空间](@entry_id:261392) $\mathcal{D}$ 上的[前向差分](@entry_id:173829)算子 $T$：
$$
(Tx)_n = x_{n+1} - x_n
$$
我们来计算其伴随 $T^*$ [@problem_id:1885393]。对于任意 $x \in \mathcal{D}$ 和 $y \in \ell^2(\mathbb{Z})$，我们有：
$$
\langle Tx, y \rangle = \sum_{n=-\infty}^{\infty} (x_{n+1} - x_n) \overline{y_n} = \sum_{n=-\infty}^{\infty} x_{n+1} \overline{y_n} - \sum_{n=-\infty}^{\infty} x_n \overline{y_n}
$$
由于 $x$ 是有限支撑的，这些和都是有限和，我们可以安全地重排索引。在第一个和式中，令 $m = n+1$，则 $n = m-1$，和式变为 $\sum_{m=-\infty}^{\infty} x_m \overline{y_{m-1}}$。代回原式：
$$
\langle Tx, y \rangle = \sum_{n=-\infty}^{\infty} x_n \overline{y_{n-1}} - \sum_{n=-\infty}^{\infty} x_n \overline{y_n} = \sum_{n=-\infty}^{\infty} x_n \overline{(y_{n-1} - y_n)} = \langle x, z \rangle
$$
其中 $z$ 是一个序列，其第 $n$ 项为 $z_n = y_{n-1} - y_n$。这个表达式定义了[伴随算子](@entry_id:140236)的作用：$(T^*y)_n = y_{n-1} - y_n$，即负的[后向差分](@entry_id:637618)算子。为了确定 $D(T^*)$，我们需要检查对于哪些 $y \in \ell^2(\mathbb{Z})$，所得到的 $z$ 仍然属于 $\ell^2(\mathbb{Z})$。由于 $z$ 是 $y$ 的一个移位与 $y$ 本身的差，而[移位算子](@entry_id:273531)在 $\ell^2(\mathbb{Z})$ 上是有界的，所以对于任何 $y \in \ell^2(\mathbb{Z})$，$z$ 都属于 $\ell^2(\mathbb{Z})$。因此，$D(T^*) = \ell^2(\mathbb{Z})$。

#### 实例：函数空间上的微分算子

[微分算子](@entry_id:140145)是[无界算子](@entry_id:144655)中最重要的例子，其[伴随算子](@entry_id:140236)的计算是理解量子力学和[偏微分方程](@entry_id:141332)的关键。考虑 $H = L^2([0,1])$ 上的[微分算子](@entry_id:140145) $Tf = \frac{df}{dx}$，其定义域 $D(T)$ 是所有在 $[0,1]$ 上连续可微且满足边界条件 $f(1)=0$ 的函数构成的[稠密子空间](@entry_id:261392) [@problem_id:1885452]。

对于 $f \in D(T)$ 和一个足够光滑的函数 $g \in H$，我们使用[分部积分法](@entry_id:136350)：
$$
\langle Tf, g \rangle = \int_0^1 f'(x) \overline{g(x)} \,dx = \left[f(x) \overline{g(x)}\right]_0^1 - \int_0^1 f(x) \overline{g'(x)} \,dx
$$
这个过程要求 $g$ 是绝对连续的，且其导数 $g'$ 是平方可积的。边界项为 $f(1)\overline{g(1)} - f(0)\overline{g(0)}$。根据 $D(T)$ 的定义，我们知道 $f(1)=0$，因此边界项简化为 $-f(0)\overline{g(0)}$。
为了使 $\langle Tf, g \rangle$ 能被写成 $\langle f, h \rangle$ 的形式，即 $\int_0^1 f(x) \overline{h(x)} \,dx$，边界项 $-f(0)\overline{g(0)}$ 必须对所有 $f \in D(T)$ 都为零。由于 $D(T)$ 中包含在 $x=0$ 处取任意值的函数（例如 $f(x) = c(x-1)$），要保证边界项消失，唯一的可能是要求 $\overline{g(0)}=0$，即 $g(0)=0$。

当 $g(0)=0$ 这个条件满足时，边界项为零，我们得到：
$$
\langle Tf, g \rangle = - \int_0^1 f(x) \overline{g'(x)} \,dx = \int_0^1 f(x) \overline{(-g'(x))} \,dx = \langle f, -g' \rangle
$$
这表明 $T^*g = -g'$。因此，我们确定了伴随算子 $T^*$ 的作用及其定义域：
$$
T^*g = -\frac{dg}{dx}, \quad D(T^*) = \{ g \in H \mid g \text{ is absolutely continuous, } g' \in L^2([0,1]), g(0)=0 \}
$$
这个例子深刻地揭示了一个普遍规律：一个微分算子的[伴随算子](@entry_id:140236)不仅在形式上（通常是符号和阶数）相关，其定义域中的**边界条件**也与原[算子定义域](@entry_id:275586)中的边界条件密切相关，它们是相互“对偶”的，共同确保分部积分后的边界项为零。

### [伴随算子](@entry_id:140236)的基本性质

稠密定义算子的伴随具有一系列优美的代数和拓扑性质，这些性质是泛函分析理论的基石。

#### 伴随算子的闭性

一个极其重要的性质是：**任意稠密定义算子 $T$ 的伴随算子 $T^*$ 必定是一个[闭算子](@entry_id:274252)**。一个算子 $A$ 被称为**[闭算子](@entry_id:274252) (closed operator)**，如果其图像 $\mathrm{Graph}(A) = \{ (x, Ax) \mid x \in D(A) \}$ 是 $H \times H$ 中的一个[闭集](@entry_id:136446)。这等价于：若序列 $\{x_n\} \subset D(A)$ 满足 $x_n \to x$ 且 $Ax_n \to y$，则必有 $x \in D(A)$ 且 $Ax=y$。

这个性质的证明相当直接。假设序列 $\{y_n\} \subset D(T^*)$ 满足 $y_n \to y$ 且 $T^*y_n \to z$。我们需要证明 $y \in D(T^*)$ 且 $T^*y = z$。根据 $T^*$ 的定义，对于任意 $x \in D(T)$ 和任意 $n$，我们有 $\langle Tx, y_n \rangle = \langle x, T^*y_n \rangle$。现在取极限 $n \to \infty$：
$$
\langle Tx, y \rangle = \lim_{n\to\infty} \langle Tx, y_n \rangle = \lim_{n\to\infty} \langle x, T^*y_n \rangle = \langle x, z \rangle
$$
这个等式 $\langle Tx, y \rangle = \langle x, z \rangle$ 对所有 $x \in D(T)$ 都成立，这正是 $y \in D(T^*)$ 且 $T^*y = z$ 的定义。因此，$T^*$ 是[闭算子](@entry_id:274252) [@problem_id:1885413]。

#### 扩张与限制的对偶性

算子之间的包含关系（限制与扩张）在取伴随之后会发生逆转。具体而言，如果 $S$ 和 $T$ 都是稠密定义的算子，且 $S$ 是 $T$ 的一个限制（记作 $S \subseteq T$），即 $D(S) \subseteq D(T)$ 且在 $D(S)$ 上 $S=T$，那么它们的[伴随算子](@entry_id:140236)满足 $T^* \subseteq S^*$ [@problem_id:1885433]。

这个结论的直观理解是，定义伴随算子 $A^*$ 的条件 $\langle Ax, y \rangle = \langle x, z \rangle$ 必须对 *所有* $x \in D(A)$ 成立。当我们将算子从 $T$ 限制到 $S$ 时，定义域变小了 ($D(S) \subset D(T)$)。因此，要求 $\langle Sx, y \rangle = \langle x, z \rangle$ 对所有 $x \in D(S)$ 成立，这是一个比对所有 $x \in D(T)$ 成立更弱的条件。因此，可能会有更多的 $y$ 满足这个较弱的条件，从而导致 $D(T^*)$ 是 $D(S^*)$ 的一个[子集](@entry_id:261956)，即 $T^* \subseteq S^*$。

#### 代数运算的伴随

伴随运算与其他[算子代数](@entry_id:146444)运算（如加法）具有良好的兼容性。一个特别有用的法则是关于一个[无界算子](@entry_id:144655)与一个[有界算子](@entry_id:264879)之和的伴随 [@problem_id:1885432]。如果 $T$ 是一个稠密定义的算子，而 $S$ 是一个在整个[希尔伯特空间](@entry_id:261193) $H$ 上都有定义的[有界算子](@entry_id:264879)，那么算子 $A = S+T$（定义域为 $D(A) = D(T)$）的伴随是：
$$
(S+T)^* = S^* + T^*
$$
并且它们的定义域相同，$D((S+T)^*) = D(T^*)$。这是因为对于 $y \in D(T^*)$：
$$
\langle (S+T)x, y \rangle = \langle Sx, y \rangle + \langle Tx, y \rangle = \langle x, S^*y \rangle + \langle x, T^*y \rangle = \langle x, (S^*+T^*)y \rangle
$$
由于 $S$ 是有界的，$y$ 是否属于 $D((S+T)^*)$ 的判断完全取决于 $\langle Tx, y \rangle$ 是否有界，这与判断 $y$ 是否属于 $D(T^*)$ 的条件完全相同。

#### 核、值域与正交性

[伴随算子](@entry_id:140236)的一个核心性质是它通过正交性将原算子的值域 (range) 和其自身的核 (kernel) 联系起来。对于任意稠密定义的算子 $T$，我们有以下基本恒等式：
$$
(\mathrm{ran}(T))^\perp = \ker(T^*)
$$
这里 $\mathrm{ran}(T) = \{Tx \mid x \in D(T)\}$ 是 $T$ 的值域，$(\cdot)^\perp$ 表示正交补。这个关系说明，一个向量 $y$ 与 $T$ 的整个值域正交，当且仅当这个向量被 $T^*$ 映为零向量。证明如下：
$y \in (\mathrm{ran}(T))^\perp$
$\iff \langle z, y \rangle = 0$ 对所有 $z \in \mathrm{ran}(T)$
$\iff \langle Tx, y \rangle = 0$ 对所有 $x \in D(T)$
$\iff \langle x, T^*y \rangle = 0$ 对所有 $x \in D(T)$ (这要求 $y \in D(T^*)$)
由于 $D(T)$ 是稠密的，最后一个条件等价于 $T^*y = 0$，即 $y \in \ker(T^*)$。
通过取两次[正交补](@entry_id:149922)，可以得到另一个相关的重要结果：$\overline{\mathrm{ran}(T)} = (\ker(T^*))^\perp$。这个定理在求解算子方程和谱理论中扮演着核心角色 [@problem_id:1885427]。

### 对称与[自伴算子](@entry_id:152188)

对称性和自伴性是[无界算子](@entry_id:144655)理论中最重要的概念，尤其是在量子力学中，它们分别对应于物理 observable 的数学形式。

#### [对称算子](@entry_id:272489)

一个稠密定义的算子 $T$ 被称为**对称的 (symmetric)** 或埃尔米特的 (Hermitian)，如果它被其伴随算子所包含，即 $T \subseteq T^*$。这等价于两个条件：
1.  定义域满足 $D(T) \subseteq D(T^*)$。
2.  对于所有 $x \in D(T)$，$Tx = T^*x$。

将这两个条件合并，对称性的一个更实用的判别准则是：
$$
\langle Tx, y \rangle = \langle x, Ty \rangle, \quad \text{for all } x, y \in D(T)
$$
以动量算子 $Tf = -if'$ 为例。如果其定义域为 $D(T) = C_c^\infty((0,1))$，即在 $(0,1)$ 内具有[紧支撑](@entry_id:276214)的无穷可微函数，那么对于任意 $f, g \in D(T)$，分部积分的边界项 $[ -i f(x) \overline{g(x)} ]_0^1$ 会因为 $f$ 和 $g$ 在端点附近为零而消失。因此，$\langle Tf, g \rangle = \langle f, Tg \rangle$ 成立，该算子是对称的 [@problem_id:1885454]。然而，如果我们将定义域改为 $D(T) = \{f \in C^1([0,1]) : f(0)=0\}$，对于 $f, g \in D(T)$，分部积分将产生一个边界项 $-i f(1) \overline{g(1)}$，它通常不为零。因此，在这个定义域下，算子 $T$ 不是对称的 [@problem_id:1885444]。这再次说明了定义域（特别是边界条件）在确定算子性质中的决定性作用。

#### [自伴算子](@entry_id:152188)

对称性 ($T \subseteq T^*$) 是一个理想的性质，但一个更强的性质是**自伴性 (self-adjointness)**。一个[对称算子](@entry_id:272489) $T$ 如果满足 $D(T) = D(T^*)$，则称其为**自伴的 (self-adjoint)**。这意味着 $T=T^*$。

自伴性是一个非常苛刻的条件。许多在物理和数学中自然出现的[对称算子](@entry_id:272489)都不是自伴的。例如，上面提到的动量算子 $Tf = -if'$，当定义域为 $D(T) = C_c^\infty((0,1))$ 时是对称的。它的伴随 $T^*$ 的作用形式同样是 $T^*g = -ig'$，但其定义域 $D(T^*)$ 是 Sobolev 空间 $H^1((0,1))$，即所有导数也属于 $L^2$ 的 $L^2$ 函数，没有任何边界条件 [@problem_id:1885454]。显然，$D(T) = C_c^\infty((0,1))$ 是 $D(T^*) = H^1((0,1))$ 的一个[真子集](@entry_id:152276)。例如，[常数函数](@entry_id:152060) $g(x)=1$ 就在 $D(T^*)$ 中（因为 $g'=0 \in L^2$），但它显然不在 $D(T)$ 中，因为它不满足[紧支撑](@entry_id:276214)条件。因此，这个算子是**对称的，但不是自伴的**。

#### 二次伴随与[算子闭包](@entry_id:261843)

对于一个稠密定义的算子 $T$，其伴随 $T^*$ 是一个[闭算子](@entry_id:274252)。如果我们再取一次伴随，得到 $T^{**} = (T^*)^*$。一个基本定理指出，当 $T$ 是稠密定义时，它的闭包 $\bar{T}$ 存在当且仅当 $D(T^*)$ 也是稠密的。在这种情况下，我们有：
$$
\bar{T} = T^{**}
$$
由于 $T^*$ 是 $T^{**}$ 的伴随，并且 $T^*$ 本身是闭的，这意味着 $T^* = (T^*)^{**} = (T^{**})^*$。
如果 $T$ 本身是闭的，则 $T = \bar{T} = T^{**}$。

对于一个[对称算子](@entry_id:272489) $T$，我们有 $T \subseteq T^*$。取伴随得到 $(T^*)^* \subseteq T^*$，即 $T^{**} \subseteq T^*$。结合 $T \subseteq T^{**}$（因为 $T^{**}$ 是 $T$ 的[闭包](@entry_id:148169)），我们得到了[对称算子](@entry_id:272489)的基本包含关系链：
$$
T \subseteq T^{**} \subseteq T^*
$$
再次考察我们的动量算子例子 $Tf = -if'$，其定义域为 $D(T) = C_c^\infty((0,1))$ [@problem_id:1885398]。
1.  $T$ 的作用为 $-if'$，定义域 $D(T) = C_c^\infty((0,1))$。
2.  我们计算出 $T^*$ 的作用为 $-ig'$，定义域 $D(T^*) = H^1((0,1))$。
3.  $T^{**} = (T^*)^*$ 的作用为 $-if'$。计算 $T^*$ 的伴随时，分部积分的边界项 $[ -i g(x) \overline{f(x)} ]_0^1$ 必须对所有 $g \in D(T^*) = H^1((0,1))$ 消失。这要求 $f$ 必须满足 $f(0)=0$ 和 $f(1)=0$。因此，其定义域为 $D(T^{**}) = H_0^1((0,1))$，即在端点处为零的 $H^1$ [函数空间](@entry_id:143478)。

这清晰地展示了三者之间的严格包含关系：
$$
C_c^\infty((0,1)) \subset H_0^1((0,1)) \subset H^1((0,1))
$$
$$
D(T) \subset D(T^{**}) \subset D(T^*)
$$
$T$ 是对称的，它的[闭包](@entry_id:148169) $\bar{T} = T^{**}$ 也是对称的，但它们都不是自伴的。寻找一个[对称算子](@entry_id:272489)的[自伴扩张](@entry_id:264525)（即找到一个介于 $T$ 和 $T^*$ 之间的[自伴算子](@entry_id:152188)）是谱理论中的一个核心问题，它对于量子系统的[哈密顿量](@entry_id:172864)等物理算子的数学严谨性至关重要。