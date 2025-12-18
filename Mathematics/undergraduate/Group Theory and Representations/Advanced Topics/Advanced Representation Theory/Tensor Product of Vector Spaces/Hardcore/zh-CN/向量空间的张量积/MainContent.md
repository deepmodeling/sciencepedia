## 引言
在数学和物理学的广阔天地中，我们经常需要将简单的系统组合成更复杂的整体。向量[空间的笛卡尔积](@entry_id:276174)提供了一种直接的组合方式，但在许多情况下，这种方式不足以捕捉系统间丰富的相互作用和结构。[向量空间](@entry_id:151108)的张量积应运而生，它是一种更精妙、更强大的构造，为现代科学的多个分支提供了统一而深刻的语言。从描述量子系统中粒子纠缠的神秘现象，到构造[群表示](@entry_id:156757)和分析拓扑空间的几何结构，张量积无处不在。

本文旨在系统地揭开[向量空间](@entry_id:151108)[张量积](@entry_id:140694)的神秘面纱。我们首先会遇到一个核心问题：为什么我们需要一种超越简单笛卡尔积的构造？本文将通过三个章节，引导读者从基本原理走向前沿应用。在“原理与机制”一章中，我们将深入探讨张量积的严格定义、泛性质、基的构造，以及简单张量与纠缠张量这一关键区别。接着，在“应用与跨学科联系”一章中，我们将见证这些抽象概念如何在高等线性代数、[群表示论](@entry_id:141930)、量子力学和代数拓扑学等领域大放异彩。最后，“动手实践”部分将提供精选的练习，帮助读者巩固所学，将理论知识转化为解决问题的能力。通过本次学习，你将掌握一个强大的数学工具，它将为你深入理解现代科学的诸多核心概念铺平道路。

## 原理与机制

在介绍性章节之后，我们现在深入探讨[向量空间](@entry_id:151108)[张量积](@entry_id:140694)的构造、核心性质与基本机制。[张量积](@entry_id:140694)是一种从现有[向量空间](@entry_id:151108)构建新[向量空间](@entry_id:151108)的强大方法，其重要性远远超出了简单的集合论构造，为线性代数、量子力学、微分几何和[群表示论](@entry_id:141930)等众多领域提供了统一的语言和强大的工具。

### 定义张量积：超越[笛卡尔积](@entry_id:154642)

我们熟悉的组合两个[向量空间](@entry_id:151108) $V$ 和 $W$（在同一域 $\mathbb{F}$ 上）的方法是构造它们的**笛卡尔积（Cartesian product）** $V \times W$。这个集合由所有[有序对](@entry_id:269702) $(v, w)$ 组成，其中 $v \in V$ 且 $w \in W$。通过分量式的加法和[标量乘法](@entry_id:155971)，即 $(v_1, w_1) + (v_2, w_2) = (v_1+v_2, w_1+w_2)$ 和 $c(v,w) = (cv, cw)$，$V \times W$ 本身也构成了一个[向量空间](@entry_id:151108)。

然而，在许多数学和物理情境中，我们需要一种不同的、更精妙的组合方式，它能捕捉到两个空间元素之间更丰富的相互作用。这就是张量积 $V \otimes W$ 发挥作用的地方。从概念上讲，我们从笛卡尔积 $V \times W$ 出发，通过一个**[典范映射](@entry_id:266266)（canonical map）** $\phi: V \times W \to V \otimes W$ 将一对向量 $(v, w)$ 映射到一个新的对象，记作 $v \otimes w$，称为**简单张量（simple tensor）**。

一个至关重要的初始观察是，这个[典范映射](@entry_id:266266) $\phi$ 本身**不是一个线性变换**。线性变换必须同时满足可加性（$T(u_1+u_2) = T(u_1)+T(u_2)$）和齐次性（$T(cu) = cT(u)$）。让我们来检验一下 $\phi(v,w) = v \otimes w$ 是否满足这些条件，其中我们将定义域 $V \times W$ 视为一个[向量空间](@entry_id:151108)。

- **可加性检验**：
对于 $V \times W$ 中的两个任意元素 $(v_1, w_1)$ 和 $(v_2, w_2)$，它们的和是 $(v_1+v_2, w_1+w_2)$。应用映射 $\phi$，我们得到：
$$
\phi((v_1, w_1) + (v_2, w_2)) = \phi(v_1+v_2, w_1+w_2) = (v_1+v_2) \otimes (w_1+w_2)
$$
张量积的一个基本性质是它对每个分量都是线性的（即**[双线性](@entry_id:146819)**），因此我们可以展开上式：
$$
(v_1+v_2) \otimes (w_1+w_2) = v_1 \otimes w_1 + v_1 \otimes w_2 + v_2 \otimes w_1 + v_2 \otimes w_2
$$
另一方面，线性变换所要求的可加性结果是：
$$
\phi(v_1, w_1) + \phi(v_2, w_2) = v_1 \otimes w_1 + v_2 \otimes w_2
$$
显然，这两个结果通常不相等。它们的差值为 $v_1 \otimes w_2 + v_2 \otimes w_1$，只要 $V$ 和 $W$ 的维数都大于等于2，这个差值通常不为零。因此，$\phi$ 不满足可加性。

- **齐次性检验**：
对于一个标量 $c \in \mathbb{F}$ 和一个元素 $(v,w) \in V \times W$，我们有：
$$
\phi(c(v,w)) = \phi(cv, cw) = (cv) \otimes (cw)
$$
利用[张量积](@entry_id:140694)的双线性性质，我们可以将标量从每个分量中提出：
$$
(cv) \otimes (cw) = c(v \otimes (cw)) = c(c(v \otimes w)) = c^2 (v \otimes w)
$$
而[线性变换](@entry_id:149133)所要求的齐次性结果是：
$$
c \phi(v,w) = c(v \otimes w)
$$
除非对于所有标量 $c$ 都有 $c^2=c$（这在大多数域中是不成立的），否则 $\phi$ 不满足齐次性。

由于[典范映射](@entry_id:266266) $\phi$ 既不是可加的，也不是齐次的，它不是一个线性变换。它不满足线性，这恰恰是[张量积](@entry_id:140694)设计的核心特征。$\phi$ 所满足的性质是**双线性（bilinearity）**：对于固定的 $w$，映射 $v \mapsto v \otimes w$ 是线性的；对于固定的 $v$，映射 $w \mapsto v \otimes w$ 也是线性的。正是这种性质，而非完全线性，使得[张量积](@entry_id:140694)成为一个如此有用的构造。

### [泛性质](@entry_id:145831)：[张量积](@entry_id:140694)的本质特征

我们如何严格地定义张量积空间 $V \otimes W$ 及其运算呢？最强大和抽象的方法是通过它的**泛性质（universal property）**。这个性质不仅唯一定义了[张量积](@entry_id:140694)空间（在同构意义下），而且揭示了它的根本目的：将双线性问题转化为线性问题。

**[张量积的泛性质](@entry_id:150937)**：给定域 $\mathbb{F}$ 上的两个[向量空间](@entry_id:151108) $V$ 和 $W$，它们的[张量积](@entry_id:140694)是一个[向量空间](@entry_id:151108) $V \otimes W$ 与一个[双线性映射](@entry_id:186502) $\phi: V \times W \to V \otimes W$ 的组合，该组合满足以下条件：对于任何[向量空间](@entry_id:151108) $Z$ 和任何[双线性映射](@entry_id:186502) $B: V \times W \to Z$，都存在一个**唯一的[线性映射](@entry_id:185132)** $\tilde{B}: V \otimes W \to Z$，使得 $B = \tilde{B} \circ \phi$。

这个性质可以用[交换图](@entry_id:747516)来形象地表示，但其核心思想是：任何从 $V \times W$ 出发的[双线性映射](@entry_id:186502) $B$ 都可以“分解”为两步：首先通过典范[双线性映射](@entry_id:186502) $\phi$ 进入[张量积](@entry_id:140694)空间 $V \otimes W$，然后通过一个**[线性映射](@entry_id:185132)** $\tilde{B}$ 到达最终的目标空间 $Z$。

这意味着 $V \otimes W$ 是“最一般”的[双线性映射](@entry_id:186502)的接收空间。它将关于向量对 $(v, w)$ 的[双线性](@entry_id:146819)计算，转化为关于张量 $v \otimes w$ 的线性计算。由于[线性映射](@entry_id:185132)的理论非常成熟和强大，这种转化极具价值。

为了使这个抽象的性质变得具体，让我们看一个例子。假设 $V$ 和 $W$ 是实[向量空间](@entry_id:151108)，其基分别为 $\{e_1, e_2\}$ 和 $\{f_1, f_2\}$。考虑一个[双线性映射](@entry_id:186502) $B: V \times W \to \mathbb{R}$，其在[基向量](@entry_id:199546)上的取值已给定。根据[泛性质](@entry_id:145831)，存在一个唯一的[线性映射](@entry_id:185132) $\tilde{B}: V \otimes W \to \mathbb{R}$，满足 $\tilde{B}(v \otimes w) = B(v, w)$。现在，如果我们想计算 $\tilde{B}$ 在一个简单张量 $t = (e_1 + 2e_2) \otimes (3f_1 - f_2)$ 上的值，我们不必直接处理 $\tilde{B}$。我们可以利用定义关系回到更熟悉的[双线性映射](@entry_id:186502) $B$：
$$
\tilde{B}(t) = \tilde{B}((e_1 + 2e_2) \otimes (3f_1 - f_2)) = B(e_1 + 2e_2, 3f_1 - f_2)
$$
由于 $B$ 是[双线性](@entry_id:146819)的，我们可以像展开代数表达式一样展开它：
$$
\begin{align*}
B(e_1 + 2e_2, 3f_1 - f_2)  = B(e_1, 3f_1 - f_2) + 2B(e_2, 3f_1 - f_2) \\
 = 3B(e_1, f_1) - B(e_1, f_2) + 6B(e_2, f_1) - 2B(e_2, f_2)
\end{align*}
$$
一旦我们知道了 $B$ 在基上的值，我们就可以计算出 $\tilde{B}(t)$ 的确切值。这个例子完美地展示了[泛性质](@entry_id:145831)的实际应用：对张量空间的线性操作可以通过其对应的[双线性映射](@entry_id:186502)来理解和计算。

### 构造张量积：[基与维数](@entry_id:166269)

泛性质虽然严谨，但比较抽象。一个更具建设性的方法是通过基来构造[张量积](@entry_id:140694)空间。如果[向量空间](@entry_id:151108) $V$ 有一个基 $\{v_i\}_{i=1}^n$，[向量空间](@entry_id:151108) $W$ 有一个基 $\{w_j\}_{j=1}^m$，那么张量积空间 $V \otimes W$ 的一个基可以由所有可能的形式为 $v_i \otimes w_j$ 的简单张量构成。

这个基共有 $n \times m$ 个元素。因此，张量积空间的维数是其构成空间维数的乘积：
$$
\dim(V \otimes W) = \dim(V) \cdot \dim(W)
$$
这个维数公式是张量积的一个基本且重要的结果。

$V \otimes W$ 中的一个**一般元素（general element）**或**一般张量（general tensor）**是这些基张量的[线性组合](@entry_id:154743)，形式为：
$$
T = \sum_{i=1}^n \sum_{j=1}^m C_{ij} (v_i \otimes w_j)
$$
其中 $C_{ij}$ 是域 $\mathbb{F}$ 中的标量系数。

### 简单张量 vs. 纠缠张量：一个关键区别

初学者常常有一个误解，认为 $V \otimes W$ 中的每一个元素都可以写成 $v \otimes w$ 的形式。**这是错误的**，并且理解这一点对于掌握[张量积](@entry_id:140694)至关重要。

我们称可以表示为单个向量 $v \in V$ 和单个向量 $w \in W$ 的张量积 $v \otimes w$ 的元素为**简单张量（simple tensor）**（或**纯张量**，**可分解张量**）。那些不能以这种形式表示的张量，即必须表示为多个简单张量之和的元素，被称为**非简单张量（non-simple tensor）**或**纠缠张量（entangled tensor）**。这个术语来源于量子力学，其中它描述了[多粒子系统](@entry_id:192694)的[纠缠态](@entry_id:152310)。

如何判断一个给定的张量是否是简单的？我们可以通过其在基 $\{v_i \otimes w_j\}$下的系数 $C_{ij}$ 来判断。将这些系数[排列](@entry_id:136432)成一个矩阵 $C$，其中第 $i$ 行第 $j$ 列的元素是 $C_{ij}$。如果一个张量 $T$ 是简单的，即 $T = u \otimes z$，其中 $u = \sum_i a_i v_i$ 且 $z = \sum_j b_j w_j$，那么：
$$
T = (\sum_i a_i v_i) \otimes (\sum_j b_j w_j) = \sum_{i,j} (a_i b_j) (v_i \otimes w_j)
$$
因此，系数矩阵的元素为 $C_{ij} = a_i b_j$。这样的矩阵是由一个列向量 $(a_i)$ 和一个行向量 $(b_j)$ 的外积构成的，其**秩（rank）**必然为1（除非是零张量）。反之，如果[系数矩阵](@entry_id:151473)的秩为1，那么该张量就是简单的。

对于最简单的情况，即 $V$ 和 $W$ 都是二维空间（$\dim(V)=\dim(W)=2$），一个一般张量 $T$ 可以写成：
$$
T = a(v_1 \otimes w_1) + b(v_1 \otimes w_2) + c(v_2 \otimes w_1) + d(v_2 \otimes w_2)
$$
其系数矩阵为 $C = \begin{pmatrix} a  b \\ c  d \end{pmatrix}$。该张量是简单的当且仅当矩阵 $C$ 的秩为1，这等价于其[行列式](@entry_id:142978)为零：
$$
ad - bc = 0
$$
这个简洁的代数条件为我们提供了一个实用的判据。例如，给定张量 $T = \frac{1}{2} (v_1 \otimes w_1) + \frac{1}{3} (v_1 \otimes w_2) + \frac{1}{4} (v_2 \otimes w_1) + k (v_2 \otimes w_2)$，我们可以通过设置其系数[矩阵的[行列](@entry_id:148198)式](@entry_id:142978)为零来找到使其成为简单张量的 $k$ 值。这里 $a = 1/2, b = 1/3, c = 1/4, d = k$。因此，我们要求：
$$
\left(\frac{1}{2}\right)k - \left(\frac{1}{3}\right)\left(\frac{1}{4}\right) = 0 \quad \implies \quad \frac{k}{2} = \frac{1}{12} \quad \implies \quad k = \frac{1}{6}
$$
当 $k=1/6$ 时，该张量是简单的；对于任何其他值，$k \ne 1/6$，它都是一个纠缠张量。

### 关键同构与应用

张量积的真正威力在于它与其他线性代数概念之间建立的深刻联系，这些联系通常以**[典范同构](@entry_id:202335)（canonical isomorphisms）**的形式出现。

#### 与标量域的张量积

一个基本的同构关系是[向量空间](@entry_id:151108) $V$ 与其基域 $\mathbb{F}$ 的张量积。对于域 $\mathbb{F}$ 上的任何[向量空间](@entry_id:151108) $V$，我们有：
$$
\mathbb{F} \otimes_{\mathbb{F}} V \cong V
$$
这里的下标 $\mathbb{F}$ 强调了[张量积](@entry_id:140694)是在域 $\mathbb{F}$ 上定义的。这个同构关系是典范的，意味着它不依赖于任何基的选择。这个同构由映射 $\phi: \mathbb{F} \otimes V \to V$ 给出，其定义为：
$$
\phi(c \otimes v) = cv
$$
这里的 $cv$ 就是 $V$ 中向量 $v$ 与标量 $c$ 的标准标量乘法。这个映射本质上是说，与一个标量进行[张量积](@entry_id:140694)运算，等同于将该标量“吸收”到向量中。我们可以验证这个映射是良定义的（满足张量积的平衡条件）并且是线性的、双射的。它的逆映射是 $\psi: V \to \mathbb{F} \otimes V$，定义为 $\psi(v) = 1 \otimes v$。

#### 张量作为线性映射

[张量积](@entry_id:140694)为我们提供了一种看待[线性映射](@entry_id:185132)的全新视角。考虑从 $V$ 到 $W$ 的所有线性映射组成的空间，记为 $\text{Hom}(V, W)$ 或 $\mathcal{L}(V, W)$。这个空间与[张量积](@entry_id:140694)空间 $V^* \otimes W$ 之间存在一个[典范同构](@entry_id:202335)，其中 $V^*$ 是 $V$ 的**[对偶空间](@entry_id:146945)（dual space）**（即从 $V$到 $\mathbb{F}$ 的所有[线性泛函](@entry_id:276136)组成的空间）。
$$
\text{Hom}(V, W) \cong V^* \otimes W
$$
这个同构关系如下建立：一个简单张量 $\alpha \otimes w \in V^* \otimes W$（其中 $\alpha \in V^*$ 是一个[线性泛函](@entry_id:276136)，$w \in W$ 是一个向量）对应于一个线性映射 $T: V \to W$，其定义为：
$$
T(v) = \alpha(v)w
$$
由于 $\alpha(v)$ 是一个标量，这个映射的输出确实在 $W$ 中。这个映射 $T$ 的秩为1（除非 $\alpha$ 或 $w$ 为零）。任何一个从 $V$ 到 $W$ 的线性映射都可以表示为这样一些秩为1的映射之和，这对应于 $V^* \otimes W$ 中的一个一般张量。

具体来说，如果 $T: V \to W$ 的[矩阵表示](@entry_id:146025)在基 $\{e_i\}$ 和 $\{f_j\}$ 下为 $A = (A_{ji})$，那么与 $T$ 对应的张量 $\tau_T \in V^* \otimes W$ 可以表示为：
$$
\tau_T = \sum_{i,j} A_{ji} (e^i \otimes f_j)
$$
其中 $\{e^i\}$ 是 $\{e_i\}$ 的对偶基。这表明，[线性映射](@entry_id:185132)的矩阵元素就是其对应张量在线性泛函和目标空间向量的基张量下的分量。

#### 迹作为[张量缩并](@entry_id:193373)

这一思想在研究从一个空间到其自身的[线性算子](@entry_id:149003)（即**自同态**）时尤为深刻。在这种情况下，$W=V$，我们有同构 $\text{Hom}(V, V) \cong V^* \otimes V$。我们可以定义一个称为**缩并（contraction）**的映射 $\mathcal{C}: V^* \otimes V \to \mathbb{F}$，它在简单张量上的作用是：
$$
\mathcal{C}(\alpha \otimes v) = \alpha(v)
$$
即，将线性泛函作用于其配对的向量上。这个映射可以通过线性扩展到整个 $V^* \otimes V$ 空间。

一个优美的结果是，算子 $T \in \text{Hom}(V,V)$ 的**迹（trace）**可以通过这个缩并操作得到。如果 $\tau_T \in V^* \otimes V$ 是与 $T$ 对应的张量，那么：
$$
\text{Tr}(T) = \mathcal{C}(\tau_T)
$$
让我们来验证这一点。如果 $T$ 的矩阵是 $A=(A_{ji})$，那么对应的张量是 $\tau_T = \sum_{i,j} A_{ji} (e^i \otimes e_j)$。应用缩并映射：
$$
\mathcal{C}(\tau_T) = \sum_{i,j} A_{ji} \mathcal{C}(e^i \otimes e_j) = \sum_{i,j} A_{ji} e^i(e_j) = \sum_{i,j} A_{ji} \delta^i_j = \sum_i A_{ii}
$$
这正是矩阵 $A$ 的迹的定义。因此，[张量缩并](@entry_id:193373)为迹提供了一个不依赖于基的、内在的定义。

### 高级结构与应用

#### 对称与[反对称张量](@entry_id:199349)

当我们考虑一个[向量空间](@entry_id:151108)与自身的[张量积](@entry_id:140694) $V \otimes V$ 时，会出现额外的结构。我们可以将这个[空间分解](@entry_id:755142)为两个重要的[子空间](@entry_id:150286)。

- **[对称张量](@entry_id:148092)空间（Symmetric Tensors）** $\text{Sym}^2(V)$，由形如 $v \otimes w + w \otimes v$ 的张量张成。这些张量在交换其分量时保持不变。
- **[反对称张量](@entry_id:199349)空间（Anti-symmetric Tensors）** $\Lambda^2(V)$，由形如 $v \otimes w - w \otimes v$ 的张量张成。这些张量在交换其分量时会变号。

对于特征不为2的域，张量平方空间可以分解为这两个[子空间](@entry_id:150286)[直和](@entry_id:156782)：
$$
V \otimes V = \text{Sym}^2(V) \oplus \Lambda^2(V)
$$
如果 $\dim(V) = n$，那么这些[子空间](@entry_id:150286)的维数由组[合数](@entry_id:263553)给出：
$$
\dim(\text{Sym}^2(V)) = \binom{n+1}{2} = \frac{n(n+1)}{2}
$$
$$
\dim(\Lambda^2(V)) = \binom{n}{2} = \frac{n(n-1)}{2}
$$
我们可以验证维数是相容的：$\frac{n(n+1)}{2} + \frac{n(n-1)}{2} = \frac{n^2+n+n^2-n}{2} = n^2 = \dim(V \otimes V)$。

这个分解在物理学中有直接的应用。在量子力学中，由两个全同**[玻色子](@entry_id:138266)（bosons）**（如[光子](@entry_id:145192)）组成的系统的态空间由[对称张量](@entry_id:148092)空间 $\text{Sym}^2(V)$ 描述，而由两个全同**[费米子](@entry_id:146235)（fermions）**（如电子）组成的系统的态空间则由[反对称张量](@entry_id:199349)空间 $\Lambda^2(V)$ 描述，其中 $V$ 是单粒子态空间。例如，如果一个双[玻色子](@entry_id:138266)系统的态空间维数为21，我们可以推断出单粒[子空间](@entry_id:150286)的维数 $n$，然后计算出相应的双[费米子](@entry_id:146235)系统的态空间维数。
$$
\frac{n(n+1)}{2} = 21 \implies n^2+n-42=0 \implies (n+7)(n-6)=0
$$
由于维数必须是正数，我们得到 $n=6$。因此，对应的[费米子](@entry_id:146235)系统的态空间维数为：
$$
\dim(\Lambda^2(V)) = \frac{6(6-1)}{2} = 15
$$

#### [复化](@entry_id:260775)：标量域的扩张

[张量积](@entry_id:140694)还提供了一种改变[向量空间](@entry_id:151108)基域的系统方法，这一过程称为**[标量扩张](@entry_id:150588)（extension of scalars）**。一个重要的例子是**[复化](@entry_id:260775)（complexification）**，即将一个实[向量空间](@entry_id:151108) $V$ 转化为一个[复向量空间](@entry_id:264355)。

这通过构造张量积 $V_\mathbb{C} = V \otimes_\mathbb{R} \mathbb{C}$ 来实现。这个新空间自然地成为一个[复向量空间](@entry_id:264355)，其[标量乘法](@entry_id:155971)定义如下：对于任意复数 $z \in \mathbb{C}$ 和简单张量 $v \otimes c \in V_\mathbb{C}$（其中 $v \in V, c \in \mathbb{C}$），我们定义：
$$
z \cdot (v \otimes c) = v \otimes (zc)
$$
这个运算通过线性扩展到 $V_\mathbb{C}$ 中的所有张量。

类似地，任何作用于实[向量空间](@entry_id:151108) $V$ 的线性算子 $T: V \to V$ 都可以被“[复化](@entry_id:260775)”为一个作用于 $V_\mathbb{C}$ 的线性算子 $T_\mathbb{C}: V_\mathbb{C} \to V_\mathbb{C}$，定义为 $T_\mathbb{C} = T \otimes I$，其中 $I$ 是 $\mathbb{C}$ 上的[恒等映射](@entry_id:634191)。它在简单张量上的作用是：
$$
T_\mathbb{C}(v \otimes c) = T(v) \otimes c
$$
这个构造非常强大。例如，一个实线性算子 $T$ 可能没有任何实[特征值](@entry_id:154894)（例如，在 $\mathbb{R}^2$ 中的旋转）。然而，根据[代数基本定理](@entry_id:152321)，其[复化](@entry_id:260775)算子 $T_\mathbb{C}$ 作为有限维[复向量空间](@entry_id:264355)上的算子，**必定**至少有一个[复特征值](@entry_id:156384) $\lambda \in \mathbb{C}$ 和对应的[特征向量](@entry_id:151813) $u \in V_\mathbb{C}$。

我们可以进一步分析这个结果的含义。任何 $u \in V_\mathbb{C}$ 都可以唯一地写成 $u = v_1 \otimes 1 + v_2 \otimes i$ 的形式，其中 $v_1, v_2 \in V$。设[复特征值](@entry_id:156384) $\lambda = \alpha + i\beta$，其中 $\alpha, \beta \in \mathbb{R}$。[特征值方程](@entry_id:192306) $T_\mathbb{C}(u) = \lambda u$ 可以展开为：
$$
\text{左边： } T_\mathbb{C}(v_1 \otimes 1 + v_2 \otimes i) = T(v_1) \otimes 1 + T(v_2) \otimes i
$$
$$
\text{右边： } (\alpha + i\beta) \cdot (v_1 \otimes 1 + v_2 \otimes i) = (\alpha v_1 - \beta v_2) \otimes 1 + (\beta v_1 + \alpha v_2) \otimes i
$$
通过比较 $\otimes 1$ 和 $\otimes i$ 的系数，我们得到一个关于原始实算子 $T$ 和实向量 $v_1, v_2$ 的耦合[方程组](@entry_id:193238)：
$$
\begin{cases}
T(v_1) = \alpha v_1 - \beta v_2 \\
T(v_2) = \beta v_1 + \alpha v_2
\end{cases}
$$
这揭示了一个深刻的结构：即使 $T$ 没有一维的不变子空间（实[特征向量](@entry_id:151813)），它也总是在一个由 $v_1, v_2$ 张成的二维[子空间](@entry_id:150286)上表现出特定的行为（一个缩放和一个旋转的组合）。[张量积](@entry_id:140694)的[复化](@entry_id:260775)工具使我们能够发现和理解实[向量空间](@entry_id:151108)中这种更复杂的“类特征”行为。