## 引言
在线性代数和[张量分析](@entry_id:161423)的广阔领域中，存在一个核心概念，它优雅地连接了不同[向量空间](@entry_id:151108)之间的[线性变换](@entry_id:149133)以及它们各自的对偶测量工具——这就是**[拉回](@entry_id:160816)（Pullback）**。与将向量从一个空间“推向”另一个空间的正向映射相反，[拉回](@entry_id:160816)提供了一种系统性的方法，将作用于目标空间的线性泛函（即“测量”）“[拉回](@entry_id:160816)”到源空间。然而，这种“逆向”操作的本质、其深刻的[代数结构](@entry_id:137052)及其在不同科学领域中的统一作用，往往是初学者面临的知识鸿沟。本文旨在填补这一鸿沟，为读者提供一个关于[拉回](@entry_id:160816)的全面视角。我们将分三步深入探讨：首先，在**「原理与机制」**一章中，我们将从第一性原理出发，建立[拉回](@entry_id:160816)的严格定义，揭示其作为对偶映射的[逆变性](@entry_id:192290)质，并推导其简洁的[矩阵表示](@entry_id:146025)。接着，在**「应用与跨学科联系」**一章中，我们将展示[拉回](@entry_id:160816)如何超越抽象理论，成为连接微分几何、物理学和计算科学等领域的强大桥梁。最后，通过**「动手实践」**中的具体问题，读者将有机会将理论付诸实践，巩固所学。让我们从[拉回](@entry_id:160816)最基本的原理和机制开始，踏上这段探索之旅。

## 原理与机制

在理解了[向量空间](@entry_id:151108)与对偶空间的基本概念之后，我们现在探讨一个核心的构造，它将不同[向量空间](@entry_id:151108)之间的线性映射与它们各自的对偶空间联系起来。这个构造被称为**[拉回](@entry_id:160816) (pullback)**。[拉回](@entry_id:160816)是[张量分析](@entry_id:161423)和微分几何中一个无处不在的概念，它提供了一种系统的方式，将在一个空间上定义的测量（即[线性泛函](@entry_id:276136)）“传送”到另一个空间上。本章将深入探讨[拉回](@entry_id:160816)的定义、核心代数性质、[矩阵表示](@entry_id:146025)及其在几何语境下的深刻含义。

### [拉回](@entry_id:160816)的定义：从[线性泛函](@entry_id:276136)到对偶空间

想象我们有两个[向量空间](@entry_id:151108)，$V$ 和 $W$，以及一个连接它们的线性映射 $T: V \to W$。这个映射将 $V$ 中的向量转换为 $W$ 中的向量。现在，假设在目标空间 $W$ 上有一个“测量工具”，它是一个[线性泛函](@entry_id:276136) $\alpha \in W^*$。这个泛函 $\alpha$ 作用于 $W$ 中的任意向量并给出一个标量值。一个很自然的问题是：我们能否利用已有的 $T$ 和 $\alpha$ 来构造一个在源空间 $V$ 上的新测量工具？

答案是肯定的，而这个构造正是[拉回](@entry_id:160816)的核心思想。对于 $V$ 中的任意一个向量 $v$，我们可以先用 $T$ 将其映射到 $W$ 中，得到向量 $T(v)$。由于 $T(v)$ 是 $W$ 中的一个向量，我们可以用泛函 $\alpha$ 来测量它，得到一个标量值 $\alpha(T(v))$。这个过程为 $V$ 中的每一个向量 $v$ 都赋予了一个明确的标量。

因此，我们可以定义一个从 $V$ 到其标量域 $\mathbb{R}$ 的新映射，记为 $T^*\alpha$。它的定义如下：
对于任意 $v \in V$，
$$
(T^*\alpha)(v) := \alpha(T(v))
$$

这个新映射 $T^*\alpha$ 被称为 **$\alpha$ 在映射 $T$ 下的[拉回](@entry_id:160816)** (the pullback of $\alpha$ by $T$)。本质上，它是一个复合映射 $\alpha \circ T$。

我们必须验证 $T^*\alpha$ 确实是一个线性泛函，即 $T^*\alpha \in V^*$。设 $v_1, v_2 \in V$ 且 $c_1, c_2$ 为标量，我们利用 $T$ 和 $\alpha$ 的线性性质：
$$
\begin{align}
(T^*\alpha)(c_1 v_1 + c_2 v_2)  = \alpha(T(c_1 v_1 + c_2 v_2))  \text{(根据定义)} \\
 = \alpha(c_1 T(v_1) + c_2 T(v_2))  \text{(因为 } T \text{ 是线性的)} \\
 = c_1 \alpha(T(v_1)) + c_2 \alpha(T(v_2))  \text{(因为 } \alpha \text{ 是线性的)} \\
 = c_1 (T^*\alpha)(v_1) + c_2 (T^*\alpha)(v_2)  \text{(根据定义)}
\end{align}
$$
这证明了 $T^*\alpha$ 确实是 $V$ 上的一个[线性泛函](@entry_id:276136)。因此，[拉回](@entry_id:160816)操作本身可以被看作一个映射，它接收 $W^*$ 中的泛函，并生成 $V^*$ 中的泛函。这个映射被称为**[拉回](@entry_id:160816)映射** (pullback map) 或**对偶映射** (dual map)，记为 $T^*: W^* \to V^*$。注意，它的方向与原映射 $T: V \to W$ 相反，这是一个至关重要的特征。

为了具体理解这个定义，让我们看一个简单的例子。设 $V = W = \mathbb{R}^2$。考虑一个线性变换 $T(x, y) = (3x - 2y, x + 4y)$ 和一个[线性泛函](@entry_id:276136) $\alpha(w_1, w_2) = 5w_1 - w_2$。如果我们想计算[拉回](@entry_id:160816)泛函 $T^*\alpha$ 在向量 $v = (2, -3)$ 上的值，我们只需遵循定义即可：
$$
(T^*\alpha)(v) = \alpha(T(v))
$$
首先，计算 $T(v)$：
$$
T(2, -3) = (3(2) - 2(-3), 2 + 4(-3)) = (6+6, 2-12) = (12, -10)
$$
然后，将结果代入 $\alpha$：
$$
\alpha(12, -10) = 5(12) - (-10) = 60 + 10 = 70
$$
因此，$(T^*\alpha)(2, -3) = 70$。[@problem_id:1533747]

这个定义也适用于更抽象的[向量空间](@entry_id:151108)。例如，设 $V$ 是次数不超过2的实系数多项式空间 $P_2(\mathbb{R})$，$W = \mathbb{R}^3$。考虑一个[线性映射](@entry_id:185132) $T(p(x)) = \begin{pmatrix} p(0) \\ p'(0) \\ p(1) \end{pmatrix}$ 和一个线性泛函 $g(\mathbf{w}) = 2w_1 - w_2 + 3w_3$。要计算 $g$ 的[拉回](@entry_id:160816) $T^*g$ 在多项式 $q(x) = 4 - 2x + 5x^2$ 上的值，我们同样遵循复合映射的步骤。首先，应用 $T$：
$$
T(q(x)) = \begin{pmatrix} q(0) \\ q'(0) \\ q(1) \end{pmatrix} = \begin{pmatrix} 4 \\ -2 \\ 7 \end{pmatrix}
$$
然后，应用 $g$：
$$
(T^*g)(q(x)) = g(T(q(x))) = g\left(\begin{pmatrix} 4 \\ -2 \\ 7 \end{pmatrix}\right) = 2(4) - (-2) + 3(7) = 31
$$
这个例子 [@problem_id:1508866] 展示了[拉回](@entry_id:160816)定义的普适性，它优雅地连接了不同性质的空间（如多项式空间和欧几里得空间）以及其上的操作（如求值和求导）。

### [拉回](@entry_id:160816)的代数性质

[拉回](@entry_id:160816)操作不仅仅是一个定义，它还拥有一套丰富的[代数结构](@entry_id:137052)，这些结构对于理论推导和实际计算都至关重要。

首先，[拉回](@entry_id:160816)映射 $T^*: W^* \to V^*$ 本身是一个线性映射。这意味着对于任意 $\alpha_1, \alpha_2 \in W^*$ 和标量 $c_1, c_2$，我们有：
$$
T^*(c_1 \alpha_1 + c_2 \alpha_2) = c_1 T^*(\alpha_1) + c_2 T^*(\alpha_2)
$$
证明这一点需要展示左右两边的泛函在作用于任意向量 $v \in V$ 时得到相同的结果：
$$
\begin{align}
(T^*(c_1 \alpha_1 + c_2 \alpha_2))(v)  = (c_1 \alpha_1 + c_2 \alpha_2)(T(v)) \\
 = c_1 \alpha_1(T(v)) + c_2 \alpha_2(T(v)) \\
 = c_1 (T^*\alpha_1)(v) + c_2 (T^*\alpha_2)(v) \\
 = (c_1 T^*\alpha_1 + c_2 T^*\alpha_2)(v)
\end{align}
$$
由于这对所有 $v \in V$ 都成立，所以两个泛函相等。

其次，[拉回](@entry_id:160816)操作在处理映射相加时也表现出线性。如果我们有两个从 $V$ 到 $W$ 的线性映射 $S$ 和 $T$，它们的和 $(S+T)$ 定义为 $(S+T)(v) = S(v) + T(v)$。那么，对于任意 $\alpha \in W^*$，其在 $(S+T)$ 下的[拉回](@entry_id:160816)是什么呢？我们可以通过定义来推导：
$$
\begin{align}
((S+T)^*\alpha)(v)  = \alpha((S+T)(v))  \text{(拉回定义)} \\
 = \alpha(S(v) + T(v))  \text{(映射加法定义)} \\
 = \alpha(S(v)) + \alpha(T(v))  \text{(}\alpha \text{ 的线性)} \\
 = (S^*\alpha)(v) + (T^*\alpha)(v)  \text{(拉回定义)} \\
 = (S^*\alpha + T^*\alpha)(v)  \text{(泛函加法定义)}
\end{align}
$$
由于这对所有 $v \in V$ 成立，我们得出结论：
$$
(S+T)^*\alpha = S^*\alpha + T^*\alpha
$$
这个性质 [@problem_id:1533715] 表明，[拉回](@entry_id:160816)操作在映射层面是可加的。

最重要的代数性质，也是“[拉回](@entry_id:160816)”这一术语“反向”意味的来源，是它处理映射复合的方式。假设我们有三个[向量空间](@entry_id:151108)和两个[线性映射](@entry_id:185132) $T: U \to V$ 和 $S: V \to W$。我们可以复合它们得到 $S \circ T: U \to W$。现在，取一个泛函 $\omega \in W^*$，我们可以计算其在复合映射 $S \circ T$ 下的[拉回](@entry_id:160816) $(S \circ T)^*\omega$。这个新的泛函在 $U^*$ 中。另一方面，我们可以分步进行[拉回](@entry_id:160816)：首先将 $\omega$ 从 $W^*$ [拉回](@entry_id:160816)到 $V^*$，得到 $S^*\omega \in V^*$；然后，再将这个新的泛函从 $V^*$ [拉回](@entry_id:160816)到 $U^*$，得到 $T^*(S^*\omega) \in U^*$。一个惊人而优美的结果是，这两种方式得到的结果是相同的。这就是**[拉回](@entry_id:160816)的[逆变](@entry_id:192290)（contravariant）性质**：
$$
(S \circ T)^* = T^* \circ S^*
$$
注意，映射复合的顺序被颠倒了。让我们来证明它。对于任意 $u \in U$：
$$
\begin{align}
((S \circ T)^*\omega)(u)  = \omega((S \circ T)(u))  \text{(定义)} \\
 = \omega(S(T(u)))  \text{(复合定义)}
\end{align}
$$
而另一方面：
$$
\begin{align}
(T^* \circ S^*)(\omega)(u)  = (T^*(S^*\omega))(u)  \text{(复合定义)} \\
 = (S^*\omega)(T(u))  \text{(T 的拉回定义)} \\
 = \omega(S(T(u)))  \text{(S 的拉回定义)}
\end{align}
$$
两边的结果完全相同，因此该恒等式成立。

我们可以通过一个具体的计算来验证这个恒等式 [@problem_id:1533753]。设 $U = \mathbb{R}^2, V = \mathbb{R}^3, W = \mathbb{R}^2$，并定义映射 $T(x,y) = (x-2y, 3x+y, y)$ 和 $S(a,b,c) = (a+b, 2b-c)$，以及泛函 $\omega(p,q) = 4p - q$。
首先计算复合映射 $S \circ T$：
$$
(S \circ T)(x,y) = S(x-2y, 3x+y, y) = ((x-2y)+(3x+y), 2(3x+y)-y) = (4x-y, 6x+y)
$$
然后计算其[拉回](@entry_id:160816)：
$$
((S \circ T)^*\omega)(x,y) = \omega(4x-y, 6x+y) = 4(4x-y) - (6x+y) = 16x-4y-6x-y = 10x-5y
$$
现在，我们分步计算 $T^* \circ S^*$。首先计算 $S^*\omega$。对于 $v=(a,b,c) \in V$：
$$
(S^*\omega)(a,b,c) = \omega(S(a,b,c)) = \omega(a+b, 2b-c) = 4(a+b)-(2b-c) = 4a+2b+c
$$
令 $\eta = S^*\omega$，则 $\eta(a,b,c) = 4a+2b+c$。现在计算 $T^*\eta = T^*(S^*\omega)$。对于 $u=(x,y) \in U$：
$$
(T^*\eta)(x,y) = \eta(T(x,y)) = \eta(x-2y, 3x+y, y) = 4(x-2y)+2(3x+y)+y = 4x-8y+6x+2y+y = 10x-5y
$$
两种计算方法得到了完全相同的结果 $10x - 5y$，有力地证实了 $(S \circ T)^* = T^* \circ S^*$ 这一核心性质。

### [拉回](@entry_id:160816)的[矩阵表示](@entry_id:146025)

当我们在[有限维向量空间](@entry_id:265491)中工作时，[线性映射](@entry_id:185132)可以用矩阵来表示。[拉回](@entry_id:160816)映射也有一个非常简洁和强大的矩阵表示。

假设 $V$ 和 $W$ 是[有限维向量空间](@entry_id:265491)，分别具有基 $\{e_1, \dots, e_m\}$ 和 $\{f_1, \dots, f_n\}$。设 $T: V \to W$ 是一个[线性映射](@entry_id:185132)，其[矩阵表示](@entry_id:146025)为 $A$，其中 $A$ 的第 $j$ 列是 $T(e_j)$ 在基 $\{f_k\}$ 下的坐标。即 $T(e_j) = \sum_{k=1}^n A_{kj} f_k$。

现在考虑[对偶空间](@entry_id:146945) $V^*$ 和 $W^*$，它们分别具有对偶基 $\{\epsilon^1, \dots, \epsilon^m\}$ 和 $\{\phi^1, \dots, \phi^n\}$，其定义为 $\epsilon^i(e_j) = \delta^i_j$ 和 $\phi^k(f_l) = \delta^k_l$。[拉回](@entry_id:160816)映射 $T^*: W^* \to V^*$ 是一个线性映射，因此它也应该有一个矩阵表示。这个矩阵是什么呢？

结论是：**如果 $T$ 的矩阵是 $A$，那么 $T^*$ 相对于对偶基的矩阵是 $A$ 的转置 $A^T$**。

让我们来证明这个结论。设 $T^*$ 的矩阵为 $B$。$B$ 的第 $k$ 列应该是 $T^*(\phi^k)$ 在基 $\{\epsilon^i\}$ 下的坐标。也就是说，$T^*(\phi^k) = \sum_{i=1}^m B_{ik} \epsilon^i$。为了确定系数 $B_{jk}$，我们让这个泛函作用在[基向量](@entry_id:199546) $e_j$ 上：
$$
(T^*(\phi^k))(e_j) = \left(\sum_{i=1}^m B_{ik} \epsilon^i\right)(e_j) = \sum_{i=1}^m B_{ik} \epsilon^i(e_j) = \sum_{i=1}^m B_{ik} \delta^i_j = B_{jk}
$$
另一方面，根据[拉回](@entry_id:160816)的定义：
$$
(T^*(\phi^k))(e_j) = \phi^k(T(e_j)) = \phi^k\left(\sum_{l=1}^n A_{lj} f_l\right) = \sum_{l=1}^n A_{lj} \phi^k(f_l) = \sum_{l=1}^n A_{lj} \delta^k_l = A_{kj}
$$
比较两个结果，我们得到 $B_{jk} = A_{kj}$。这正是[矩阵转置](@entry_id:155858)的定义，即 $B = A^T$。

例如，考虑一个从 $\mathbb{R}^3$到 $\mathbb{R}^2$ 的映射 $T$，定义在标准基上为 $T(e_1) = f_1$, $T(e_2) = 2f_1 + 3f_2$, $T(e_3) = -f_2$。$T$ 的矩阵 $A$ 的列是这些像的坐标：
$$
A = \begin{pmatrix} 1   2   0 \\ 0   3   -1 \end{pmatrix}
$$
根据我们的理论，[拉回](@entry_id:160816)映射 $T^*: (\mathbb{R}^2)^* \to (\mathbb{R}^3)^*$ 的矩阵应该是 $A^T$。
$$
A^T = \begin{pmatrix} 1   0 \\ 2   3 \\ 0   -1 \end{pmatrix}
$$
我们可以直接计算来验证。$T^*$ 的第一列是 $T^*(\phi^1)$ 的坐标。
$$
(T^*\phi^1)(e_1) = \phi^1(T(e_1)) = \phi^1(f_1) = 1 \\
(T^*\phi^1)(e_2) = \phi^1(T(e_2)) = \phi^1(2f_1+3f_2) = 2 \\
(T^*\phi^1)(e_3) = \phi^1(T(e_3)) = \phi^1(-f_2) = 0
$$
所以 $T^*(\phi^1) = 1\epsilon^1 + 2\epsilon^2 + 0\epsilon^3$，其[坐标向量](@entry_id:153319)是 $(1, 2, 0)^T$，正是 $A^T$ 的第一列。同样地，对于 $T^*(\phi^2)$:
$$
(T^*\phi^2)(e_1) = \phi^2(T(e_1)) = \phi^2(f_1) = 0 \\
(T^*\phi^2)(e_2) = \phi^2(T(e_2)) = \phi^2(2f_1+3f_2) = 3 \\
(T^*\phi^2)(e_3) = \phi^2(T(e_3)) = \phi^2(-f_2) = -1
$$
所以 $T^*(\phi^2) = 0\epsilon^1 + 3\epsilon^2 - 1\epsilon^3$，其[坐标向量](@entry_id:153319)是 $(0, 3, -1)^T$，正是 $A^T$ 的第二列。这证实了 $[T^*] = [T]^T$ 的结论 [@problem_id:1533719]。这个关系式在计算上极为有用，例如，它直接告诉我们[拉回](@entry_id:160816)映射的像空间 $\text{Im}(T^*)$ (在对偶基下的表示)就是原映射矩阵 $A$ 的行空间 [@problem_id:1533726]。

### [拉回](@entry_id:160816)与[向量空间](@entry_id:151108)的几何结构

[拉回](@entry_id:160816)操作不仅是代数上的构造，它还深刻地反映了原[线性映射](@entry_id:185132) $T$ 的几何性质，如核 (kernel) 与像 (image)。

考虑一个非零泛函 $\alpha \in W^*$ 和一个线性映射 $T: V \to W$。如果 $\alpha$ 的[拉回](@entry_id:160816)是零泛函，即 $T^*\alpha = 0$，这意味着什么？根据定义，对于所有 $v \in V$，我们有 $(T^*\alpha)(v) = \alpha(T(v)) = 0$。这个等式告诉我们，映射 $T$ 的整个像空间 $\text{Im}(T) = \{T(v) \mid v \in V\}$ 都被泛函 $\alpha$ 映射到了零。换句话说，$\text{Im}(T)$ 中的每一个向量都在 $\alpha$ 的核 $\text{ker}(\alpha)$ 中。因此，我们得到了一个重要的结论：**如果 $T^*\alpha = 0$ 且 $\alpha \neq 0$，则 $\text{Im}(T) \subseteq \text{ker}(\alpha)$** [@problem_id:1533741]。这为我们提供了一个通过[拉回](@entry_id:160816)来探测映射像空间的方法。

这个关系可以被推广。一个关键的结果是，[拉回](@entry_id:160816)映射的像空间与原映射的核空间之间存在一种称为“歼灭”(annihilation) 的对偶关系。一个[子空间](@entry_id:150286) $S \subseteq V$ 的**歼灭子** (annihilator) $S^o$ 是 $V^*$ 中的一个[子空间](@entry_id:150286)，由所有在 $S$ 上为零的[线性泛函](@entry_id:276136)组成：$S^o = \{ \phi \in V^* \mid \phi(s) = 0 \text{ for all } s \in S \}$。一个基础性的定理（此处不作证明）指出：
$$
\text{Im}(T^*) = (\text{ker}(T))^o
$$
这说明，$T^*$ 的像恰好由那些能够“歼灭” $T$ 的核的泛函组成。

这种对偶关系最显著的体现是在映射的[单射性](@entry_id:147722) (injectivity) 与满射性 (surjectivity) 上。我们有以下重要定理：

1.  **$T$ 是满射的 (surjective) 当且仅当 $T^*$ 是[单射](@entry_id:183792)的 (injective)。**
2.  **$T$ 是[单射](@entry_id:183792)的 (injective) 当且仅当 $T^*$ 是满射的 (surjective)。**

让我们证明第一条。
($\Rightarrow$) 假设 $T$ 是满射的。要证明 $T^*$ 是[单射](@entry_id:183792)的，我们只需证明其核为零，即若 $T^*\alpha = 0$，则必有 $\alpha = 0$。如果 $T^*\alpha=0$，那么对所有 $v \in V$，都有 $\alpha(T(v)) = 0$。因为 $T$ 是满射的，对于 $W$ 中任意一个向量 $w$，都存在一个 $v \in V$ 使得 $T(v) = w$。因此，对于任意 $w \in W$，都有 $\alpha(w)=0$。这意味着 $\alpha$ 是零泛函。故 $T^*$ 是[单射](@entry_id:183792)的。
($\Leftarrow$) 证明反向需要更深入的工具，但直观上，如果 $T^*$ 是[单射](@entry_id:183792)的，它就不会“丢失信息”，这意味着原映射 $T$ 必须“覆盖”整个目标空间。

我们可以用一个例子来感受这一点 [@problem_id:1533711]。考虑从[多项式空间](@entry_id:144410) $V=P_2(\mathbb{R})$ 到 $W=\mathbb{R}^2$ 的映射 $T(p) = (p(0), p(1))$。这个映射是满射的，因为对于任意一对值 $(u,v) \in \mathbb{R}^2$，我们总能找到一个多项式（例如一次多项式 $p(t) = u + (v-u)t$）使得 $p(0)=u$ 且 $p(1)=v$。根据定理，$T^*$ 应该是单射的。我们可以计算一个具体泛函 $\omega(u,v) = 3u-v$ 的[拉回](@entry_id:160816) $T^*\omega$。对于任意多项式 $p(t) = a_0+a_1 t + a_2 t^2$：
$$
(T^*\omega)(p) = \omega(T(p)) = \omega(p(0), p(1)) = 3p(0) - p(1) = 3a_0 - (a_0+a_1+a_2) = 2a_0 - a_1 - a_2
$$
得到的[拉回](@entry_id:160816) $T^*\omega$ 是一个作用于[多项式系数](@entry_id:262287)的非零泛函。

### [拉回](@entry_id:160816)的应用与推广

[拉回](@entry_id:160816)的概念远远超出了基础线性代数的范畴，它是现代数学中一个统一性的思想。

#### 双重[拉回](@entry_id:160816)与自然性

我们可以对[拉回](@entry_id:160816)映射 $T^*: W^* \to V^*$ 再次进行[拉回](@entry_id:160816)操作，得到一个**双重[拉回](@entry_id:160816)** (double pullback) $(T^*)^*: V^{**} \to W^{**}$，其中 $V^{**}$ 和 $W^{**}$ 分别是 $V$ 和 $W$ 的[双对偶空间](@entry_id:264977)。对于[有限维向量空间](@entry_id:265491)，存在一个特别的**[典范同构](@entry_id:202335)** (canonical isomorphism) $J_V: V \to V^{**}$，它将一个向量 $v \in V$ 映射到其在 $V^{**}$ 中的对应元素——作用于泛函的[求值映射](@entry_id:149774) $\text{ev}_v$，其定义为 $\text{ev}_v(\phi) = \phi(v)$。

在这个[典范同构](@entry_id:202335)的框架下，双重[拉回](@entry_id:160816) $(T^*)^*$ 与原映射 $T$ 之间存在着一个美妙的关系。考虑 $V$ 中的任意向量 $v$。它通过 $J_V$ 对应于 $V^{**}$ 中的 $\text{ev}_v$。然后，$(T^*)^*$ 将 $\text{ev}_v$ 映射到 $W^{**}$ 中的一个元素。这个元素是什么呢？对于任意 $\psi \in W^*$：
$$
((T^*)^*(\text{ev}_v))(\psi) = \text{ev}_v(T^*\psi) = (T^*\psi)(v) = \psi(T(v))
$$
但是，$\psi(T(v))$ 正是 $W^{**}$ 中与向量 $T(v) \in W$ 相关联的[求值映射](@entry_id:149774) $\text{ev}_{T(v)}$ 作用于 $\psi$ 的结果。因此，我们有：
$$
((T^*)^*(\text{ev}_v))(\psi) = \text{ev}_{T(v)}(\psi)
$$
这意味着 $(T^*)^*(\text{ev}_v) = \text{ev}_{T(v)}$。换句话说，在[典范同构](@entry_id:202335)下，双重[拉回](@entry_id:160816) $(T^*)^*$ 的作用等同于原映射 $T$ 本身。这个关系可以表示为 $(T^*)^* \circ J_V = J_W \circ T$，体现了[拉回](@entry_id:160816)构造的**自然性** (naturality) [@problem_id:1533709]。这表明对偶和[拉回](@entry_id:160816)的构造是与[向量空间](@entry_id:151108)结构内在协调的，而非依赖于任意的基选择。

#### 从线性代数到[微分几何](@entry_id:145818)：[1-形式的拉回](@entry_id:263669)

[拉回](@entry_id:160816)最重要的应用之一是在[微分几何](@entry_id:145818)中，它被用来变换[微分形式](@entry_id:146747) (differential forms)。一个**[1-形式](@entry_id:270392)** (1-form) 或**余[切向量](@entry_id:265494)场** (covector field) 实质上是在[流形](@entry_id:153038) (manifold) 的每一点的[切空间](@entry_id:199137) (tangent space) 上都指定了一个线性泛函（余[切向量](@entry_id:265494)）。

设 $\Phi: M \to N$ 是两个[流形](@entry_id:153038)之间的[光滑映射](@entry_id:203730)。在 $M$ 的每一点 $p$，其[微分](@entry_id:158718) $d\Phi_p$ 是一个从 $M$ 在 $p$ 点的[切空间](@entry_id:199137) $T_pM$ 到 $N$ 在 $\Phi(p)$ 点的切空间 $T_{\Phi(p)}N$ 的线性映射。如果 $\alpha$ 是 $N$ 上的一个[1-形式](@entry_id:270392)，那么在每一点 $q \in N$，$\alpha_q$ 是 $T_qN$ 上的一个[线性泛函](@entry_id:276136)。

我们可以定义 $\alpha$ 在 $\Phi$ 下的[拉回](@entry_id:160816) $\Phi^*\alpha$，它将是 $M$ 上的一个新1-形式。其在点 $p \in M$ 的值 $(\Phi^*\alpha)_p$ 是 $T_pM$ 上的一个线性泛函，定义方式与我们之前看到的完全一样：
$$
(\Phi^*\alpha)_p (v) = \alpha_{\Phi(p)}(d\Phi_p(v)) \quad \text{for any } v \in T_pM
$$
这正是[微分](@entry_id:158718)映射 $d\Phi_p$ 的[拉回](@entry_id:160816) $(d\Phi_p)^*$ 作用于 $\alpha_{\Phi(p)}$。

在[局部坐标](@entry_id:181200)中，这个操作变得非常具体。假设 $M$ 有坐标 $(x,y)$，$N$ 有坐标 $(u,v)$，映射 $\Phi$ 由函数 $u(x,y)$ 和 $v(x,y)$ 给出。$N$ 上的一个1-形式可以写成 $\alpha = A(u,v) du + B(u,v) dv$。要计算其[拉回](@entry_id:160816) $\Phi^*\alpha$，我们需要[拉回](@entry_id:160816)系数函数和基1-形式：
$$
\Phi^*\alpha = (\Phi^*A) (\Phi^*du) + (\Phi^*B) (\Phi^*dv)
$$
$\Phi^*A$ 就是将 $u,v$ 替换为 $u(x,y), v(x,y)$，即 $A(u(x,y), v(x,y))$。而基[1-形式的拉回](@entry_id:263669)则通过[全微分](@entry_id:171747)（[链式法则](@entry_id:190743)）计算：
$$
\Phi^*du = d(u \circ \Phi) = \frac{\partial u}{\partial x}dx + \frac{\partial u}{\partial y}dy
$$
$$
\Phi^*dv = d(v \circ \Phi) = \frac{\partial v}{\partial x}dx + \frac{\partial v}{\partial y}dy
$$
例如，考虑一个从 $(x,y)$ 空间到 $(u,v)$ 空间的映射 $\Phi$，由 $u=x\cos(y), v=x\sin(y)$ 定义，以及目标空间上的[1-形式](@entry_id:270392) $\alpha = u^2 du + v^2 dv$。它的[拉回](@entry_id:160816) $\Phi^*\alpha$ 是 [@problem_id:1533733]：
$$
\begin{align}
\Phi^*\alpha  = (x\cos y)^2 d(x\cos y) + (x\sin y)^2 d(x\sin y) \\
 = x^2\cos^2y(\cos y dx - x\sin y dy) + x^2\sin^2y(\sin y dx + x\cos y dy) \\
 = (x^2\cos^3y + x^2\sin^3y)dx + (-x^3\cos^2y\sin y + x^3\sin^2y\cos y)dy
\end{align}
$$
这个过程展示了[拉回](@entry_id:160816)如何将在一个[坐标系](@entry_id:156346)下定义的物理量（如[力场](@entry_id:147325)或梯度场）系统地转换到另一个[坐标系](@entry_id:156346)下，它是广义相对论和经典力学等领域中不可或缺的计算工具。

综上所述，[拉回](@entry_id:160816)是一个深刻且多功能的概念。它从一个简单的复合映射定义出发，展现出丰富的[代数结构](@entry_id:137052)和深刻的几何内涵，并最终成为连接现代数学和物理学不同分支的桥梁。