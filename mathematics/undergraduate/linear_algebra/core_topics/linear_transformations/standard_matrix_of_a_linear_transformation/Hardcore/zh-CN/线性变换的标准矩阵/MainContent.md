## 引言
在线性代数中，线性变换描述了向量空间中保持结构的基本运动，但其抽象定义往往不便于直接计算。为了量化和操控这些变换，我们需要一种具体的代数工具。那么，我们如何将一个抽象的线性变换——无论是通过几何描述还是代数法则定义——转化为一个可以进行计算和分析的实体呢？答案就在于它的标准矩阵表示，这是连接抽象概念与具体计算的桥梁。

本文旨在系统性地阐明标准矩阵的理论与实践。我们首先在“原理和机制”一章中，深入探讨标准矩阵的构建法则，揭示其如何捕捉线性变换的全部信息。接着，在“应用与交叉学科联系”一章中，我们将展示标准矩阵在计算机图形学、量子计算、动力系统等众多领域的强大应用，凸显线性代数的普适性。最后，通过“动手实践”部分的精选习题，你将有机会亲手应用所学知识，巩固理解。通过这三个层次的学习，你将全面掌握将线性变换从抽象概念转化为强大计算工具的核心技能。

## 原理和机制

在线性代数的研究中，我们致力于搭建抽象概念与具体计算之间的桥梁。线性变换，作为一种保持向量加法和标量乘法运算的特殊函数，描述了向量空间中一种基本的结构保持性运动。然而，为了对这些变换进行量化分析、组合和计算，我们需要一种更具体的代数表示。本章的核心任务就是阐述如何将一个线性变换——无论其定义多么抽象或几何化——精确地“翻译”成一个我们熟悉的工具：矩阵。这种表示法，即**标准矩阵 (standard matrix)**，是连接线性变换的几何直觉与矩阵代数强大计算能力的纽带。

### 核心原理：基向量的变换

一个线性变换的本质特征是什么？我们是否需要知道空间中每一个向量如何变换，才能完全掌握这个变换？答案是否定的。事实上，一个线性变换的全部信息都浓缩在它对定义域 (domain) 中一小组特殊的向量——基向量——的作用上。

考虑一个线性变换 $T: \mathbb{R}^n \to \mathbb{R}^m$。我们知道，$\mathbb{R}^n$ 中的任何向量 $\mathbf{x}$ 都可以唯一地表示为其标准基向量 $\mathbf{e}_1, \mathbf{e}_2, \dots, \mathbf{e}_n$ 的线性组合。这里的 $\mathbf{e}_j$ 是一个分量中第 $j$ 个为 $1$、其余均为 $0$ 的向量。具体来说，如果 $\mathbf{x} = \begin{pmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{pmatrix}$，那么：
$$
\mathbf{x} = x_1\mathbf{e}_1 + x_2\mathbf{e}_2 + \dots + x_n\mathbf{e}_n
$$
现在，我们将变换 $T$ 应用于向量 $\mathbf{x}$。根据线性变换的定义（保持加法和标量乘法），我们可以得到：
$$
\begin{align*}
T(\mathbf{x})  = T(x_1\mathbf{e}_1 + x_2\mathbf{e}_2 + \dots + x_n\mathbf{e}_n) \\
 = T(x_1\mathbf{e}_1) + T(x_2\mathbf{e}_2) + \dots + T(x_n\mathbf{e}_n) \\
 = x_1T(\mathbf{e}_1) + x_2T(\mathbf{e}_2) + \dots + x_nT(\mathbf{e}_n)
\end{align*}
$$
这个等式揭示了一个至关重要的事实：只要我们知道了每个标准基向量的像 $T(\mathbf{e}_1), T(\mathbf{e}_2), \dots, T(\mathbf{e}_n)$，我们就可以通过简单的线性组合计算出**任何**向量 $\mathbf{x}$ 的像 $T(\mathbf{x})$。基向量的像完全决定了整个线性变换。

### 标准矩阵的构建

上述的核心原理不仅提供了理论上的洞见，更指明了构造线性变换矩阵表示的具体方法。我们的目标是找到一个矩阵 $A$，使得对于任意 $\mathbf{x} \in \mathbb{R}^n$，都有 $T(\mathbf{x}) = A\mathbf{x}$ 成立。

让我们回顾矩阵向量乘法的定义。如果 $A$ 是一个 $m \times n$ 矩阵，其列向量为 $\mathbf{a}_1, \mathbf{a}_2, \dots, \mathbf{a}_n$，而 $\mathbf{x}$ 是 $\mathbb{R}^n$ 中的一个列向量，那么它们的乘积 $A\mathbf{x}$ 定义为 $A$ 的列的线性组合，其中系数是 $\mathbf{x}$ 的分量：
$$
A\mathbf{x} = x_1\mathbf{a}_1 + x_2\mathbf{a}_2 + \dots + x_n\mathbf{a}_n
$$
将这个表达式与我们从线性性质推导出的 $T(\mathbf{x}) = x_1T(\mathbf{e}_1) + x_2T(\mathbf{e}_2) + \dots + x_nT(\mathbf{e}_n)$ 进行比较，一个惊人地简洁的结论跃然纸上：如果我们令矩阵 $A$ 的第 $j$ 列就是向量 $T(\mathbf{e}_j)$，即 $\mathbf{a}_j = T(\mathbf{e}_j)$，那么这两个表达式就完全等价了。

由此，我们得到了**标准矩阵**的正式定义：对于一个线性变换 $T: \mathbb{R}^n \to \mathbb{R}^m$，其标准矩阵 $A$ 是一个 $m \times n$ 矩阵，它的列由标准基向量在 $T$ 下的像构成：
$$
A = \begin{pmatrix} |  |   | \\ T(\mathbf{e}_1)  T(\mathbf{e}_2)  \dots  T(\mathbf{e}_n) \\ |  |   | \end{pmatrix}
$$
这个构造方法是寻找任何线性变换标准矩阵的基石。

让我们通过一个具体的几何例子来理解这个构建过程。考虑一个在二维图形应用中用于产生特效的变换 $T: \mathbb{R}^2 \to \mathbb{R}^2$ [@problem_id:1374106]。该变换保持水平轴上的点不变，并将垂直基向量 $\mathbf{e}_2 = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$ 映射到向量 $\mathbf{e}_2 + 3\mathbf{e}_1$。

1.  **求 $T(\mathbf{e}_1)$**：变换保持水平轴上的点不变，因此标准基向量 $\mathbf{e}_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ 被映射到其自身。所以，$T(\mathbf{e}_1) = \mathbf{e}_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$。这是标准矩阵的第一列。

2.  **求 $T(\mathbf{e}_2)$**：根据问题描述，$T(\mathbf{e}_2) = \mathbf{e}_2 + 3\mathbf{e}_1 = \begin{pmatrix} 0 \\ 1 \end{pmatrix} + 3\begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} 3 \\ 1 \end{pmatrix}$。这是标准矩阵的第二列。

3.  **构建矩阵**：将这两个列向量组合起来，我们得到该剪切变换的标准矩阵：
    $$
    A = \begin{pmatrix} 1  3 \\ 0  1 \end{pmatrix}
    $$
这个矩阵完美地捕捉了变换的几何行为。例如，作用于一个点 $\begin{pmatrix} x \\ y \end{pmatrix}$，结果是 $A\begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} x+3y \\ y \end{pmatrix}$，这正是一个水平剪切。

### 从变换法则推导矩阵

并非所有线性变换都直接以其对基向量的作用来定义。更多时候，它们以一个通用的代数公式或几何描述给出。在这种情况下，我们的任务就是运用这个法则来找出标准基向量的像。

**利用线性性质**

有时，变换的作用是针对一组非标准的向量给出的。这时，我们需要利用线性性质来求解标准基向量的像。例如，假设一个线性变换 $T: \mathbb{R}^2 \to \mathbb{R}^2$ 满足 $T(1, 0) = (1, 2)$ 且 $T(0, 2) = (-4, 2)$ [@problem_id:1365124]。

-   $T(\mathbf{e}_1) = T(1,0)$ 已经直接给出，即 $\begin{pmatrix} 1 \\ 2 \end{pmatrix}$。
-   $T(\mathbf{e}_2) = T(0,1)$ 需要通过已知的 $T(0,2)$ 来推导。注意到 $(0,2) = 2(0,1) = 2\mathbf{e}_2$。利用 $T$ 的齐次性（标量乘法性质）：
    $$
    T(0,2) = T(2\mathbf{e}_2) = 2T(\mathbf{e}_2)
    $$
    因此，
    $$
    T(\mathbf{e}_2) = \frac{1}{2}T(0,2) = \frac{1}{2}\begin{pmatrix} -4 \\ 2 \end{pmatrix} = \begin{pmatrix} -2 \\ 1 \end{pmatrix}
    $$
-   将结果组合成标准矩阵：
    $$
    A = \begin{pmatrix} 1  -2 \\ 2  1 \end{pmatrix}
    $$

**从几何定义出发**

许多重要的线性变换源于几何操作，如旋转、反射和投影。为它们找到标准矩阵的方法同样是考察它们对标准基向量的作用。

考虑一个二维正交投影变换 $T_2$，它将任意向量投影到直线 $y=x$ 上 [@problem_id:13980]。这条直线由向量 $\mathbf{u} = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ 张成。向量 $\mathbf{v}$ 到由 $\mathbf{u}$ 张成的直线上的正交投影公式为：
$$
\text{proj}_{\mathbf{u}} \mathbf{v} = \frac{\mathbf{v} \cdot \mathbf{u}}{\|\mathbf{u}\|^2} \mathbf{u}
$$
其中 $\|\mathbf{u}\|^2 = 1^2 + 1^2 = 2$。

-   对 $\mathbf{e}_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ 进行投影：
    $$
    T_2(\mathbf{e}_1) = \frac{\begin{pmatrix} 1 \\ 0 \end{pmatrix} \cdot \begin{pmatrix} 1 \\ 1 \end{pmatrix}}{2} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \frac{1}{2}\begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 1/2 \\ 1/2 \end{pmatrix}
    $$
-   对 $\mathbf{e}_2 = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$ 进行投影：
    $$
    T_2(\mathbf{e}_2) = \frac{\begin{pmatrix} 0 \\ 1 \end{pmatrix} \cdot \begin{pmatrix} 1 \\ 1 \end{pmatrix}}{2} \begin{pmatrix} 1 \\ 1 \end{pmatrix} = \frac{1}{2}\begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} 1/2 \\ 1/2 \end{pmatrix}
    $$
因此，$T_2$ 的标准矩阵为 $A_2 = \begin{pmatrix} 1/2  1/2 \\ 1/2  1/2 \end{pmatrix}$。

### 复合变换的矩阵

现实中的许多过程是多个连续操作的结果，在线性代数中，这对应于**复合变换 (composite transformations)**。如果 $T_1: \mathbb{R}^n \to \mathbb{R}^k$ 和 $T_2: \mathbb{R}^k \to \mathbb{R}^m$ 是线性变换，那么它们的复合 $T = T_2 \circ T_1$ (先应用 $T_1$，再应用 $T_2$) 也是一个线性变换，其定义为 $T(\mathbf{x}) = T_2(T_1(\mathbf{x}))$。

复合变换的标准矩阵有一个优雅的性质：它等于其构成变换的标准矩阵的乘积。若 $A_1$ 和 $A_2$ 分别是 $T_1$ 和 $T_2$ 的标准矩阵，则复合变换 $T$ 的标准矩阵 $A$ 为：
$$
A = A_2 A_1
$$
**注意**：矩阵乘法的顺序与变换复合的顺序是“相反”的。$T_1$ 先作用，所以其矩阵 $A_1$ 在乘积的右侧，直接与向量 $\mathbf{x}$ 相邻。

我们可以通过两种等价的方法来求复合变换的矩阵。

**方法一：矩阵乘积**

延续上文的例子 [@problem_id:13980]，假设在投影 $T_2$ 之前，我们首先对向量进行一次关于 x 轴的反射 $T_1$。$T_1$ 将 $(x,y)$ 映射到 $(x,-y)$，其标准矩阵为 $A_1 = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$。那么复合变换 $T = T_2 \circ T_1$（先反射，后投影）的标准矩阵 $A$ 就是 $A_2 A_1$：
$$
A = A_2 A_1 = \begin{pmatrix} 1/2  1/2 \\ 1/2  1/2 \end{pmatrix} \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix} = \begin{pmatrix} 1/2  -1/2 \\ 1/2  -1/2 \end{pmatrix}
$$

**方法二：依次变换基向量**

这种方法更侧重于变换的几何过程，它直接计算复合变换对标准基向量的作用。
对于 $T = T_2 \circ T_1$：
-   $T(\mathbf{e}_1) = T_2(T_1(\mathbf{e}_1)) = T_2\left(\begin{pmatrix} 1 \\ 0 \end{pmatrix}\right) = \begin{pmatrix} 1/2 \\ 1/2 \end{pmatrix}$
-   $T(\mathbf{e}_2) = T_2(T_1(\mathbf{e}_2)) = T_2\left(\begin{pmatrix} 0 \\ -1 \end{pmatrix}\right) = \frac{\begin{pmatrix} 0 \\ -1 \end{pmatrix} \cdot \begin{pmatrix} 1 \\ 1 \end{pmatrix}}{2}\begin{pmatrix} 1 \\ 1 \end{pmatrix} = -\frac{1}{2}\begin{pmatrix} 1 \\ 1 \end{pmatrix} = \begin{pmatrix} -1/2 \\ -1/2 \end{pmatrix}$
将这两个结果作为列向量，我们得到与方法一完全相同的矩阵 $A = \begin{pmatrix} 1/2  -1/2 \\ 1/2  -1/2 \end{pmatrix}$。

复合变换的思想在更高维度和不同维度空间之间的变换中同样适用。
-   **三维空间中的复合变换** [@problem_id:1377785]：一个变换 $T: \mathbb{R}^3 \to \mathbb{R}^3$ 先将向量正交投影到 $xy$-平面（变换 $P$），然后将结果绕 $z$-轴逆时针旋转 $\theta$ 角（变换 $R_z$）。则 $T = R_z \circ P$。它们的标准矩阵分别为：
    $$
    A_P = \begin{pmatrix} 1  0  0 \\ 0  1  0 \\ 0  0  0 \end{pmatrix}, \quad A_{R_z} = \begin{pmatrix} \cos\theta  -\sin\theta  0 \\ \sin\theta  \cos\theta  0 \\ 0  0  1 \end{pmatrix}
    $$
    复合矩阵为 $A = A_{R_z} A_P = \begin{pmatrix} \cos\theta  -\sin\theta  0 \\ \sin\theta  \cos\theta  0 \\ 0  0  0 \end{pmatrix}$。
-   **不同维度间的复合变换** [@problem_id:1390576]：一个变换 $T: \mathbb{R}^2 \to \mathbb{R}^3$ 先将 $\mathbb{R}^2$ 中的向量逆时针旋转 $\theta$ 角（$R_\theta: \mathbb{R}^2 \to \mathbb{R}^2$），然后通过一个嵌入变换 $E: \mathbb{R}^2 \to \mathbb{R}^3$ 将其映射到三维空间。其中 $E(v_1, v_2) = (v_1 - v_2, v_1 + v_2, 2v_2)$。
    $R_\theta$ 的标准矩阵是 $A_{R_\theta} = \begin{pmatrix} \cos\theta  -\sin\theta \\ \sin\theta  \cos\theta \end{pmatrix}$。
    $E$ 的标准矩阵 $A_E$ 通过计算 $E(\mathbf{e}_1)$ 和 $E(\mathbf{e}_2)$ 得到：$E(1,0)=(1,1,0)$，$E(0,1)=(-1,1,2)$。所以 $A_E = \begin{pmatrix} 1  -1 \\ 1  1 \\ 0  2 \end{pmatrix}$。
    复合变换 $T=E \circ R_\theta$ 的标准矩阵是 $3 \times 2$ 矩阵 $A = A_E A_{R_\theta}$：
    $$
    A = \begin{pmatrix} 1  -1 \\ 1  1 \\ 0  2 \end{pmatrix} \begin{pmatrix} \cos\theta  -\sin\theta \\ \sin\theta  \cos\theta \end{pmatrix} = \begin{pmatrix} \cos\theta - \sin\theta  -\cos\theta - \sin\theta \\ \cos\theta + \sin\theta  \cos\theta - \sin\theta \\ 2\sin\theta  2\cos\theta \end{pmatrix}
    $$

### 超越欧几里得空间：一般向量空间

标准矩阵的思想可以推广到任何有限维向量空间，例如多项式空间或矩阵空间。关键在于为定义域和到达域 (codomain) 都指定一个**有序基 (ordered basis)**。

对于一个线性变换 $T: V \to W$，其中 $V$ 的基为 $\mathcal{B} = \{\mathbf{v}_1, \dots, \mathbf{v}_n\}$，$W$ 的基为 $\mathcal{C}$，我们同样可以构造一个矩阵。该矩阵的第 $j$ 列不再是 $T(\mathbf{v}_j)$ 本身，而是 $T(\mathbf{v}_j)$ 在基 $\mathcal{C}$ 下的**坐标向量 (coordinate vector)**，记作 $[T(\mathbf{v}_j)]_{\mathcal{C}}$。这个矩阵被称为 $T$ 相对于基 $\mathcal{B}$ 和 $\mathcal{C}$ 的矩阵表示。

**示例 1：多项式空间** [@problem_id:13923]
考虑从一次多项式空间 $P_1(\mathbb{R})$ 到自身的线性变换 $L(p(t)) = p(t+c) - p(t)$，其中 $c$ 是一个非零常数。我们使用 $P_1$ 的标准基 $\mathcal{B} = \{1, t\}$。
-   对第一个基向量 $p(t)=1$ 作用：$L(1) = 1 - 1 = 0$。这个零多项式在基 $\mathcal{B}$ 下的表示为 $0 \cdot 1 + 0 \cdot t$，因此其坐标向量为 $\begin{pmatrix} 0 \\ 0 \end{pmatrix}$。
-   对第二个基向量 $p(t)=t$ 作用：$L(t) = (t+c) - t = c$。这个常数多项式在基 $\mathcal{B}$ 下的表示为 $c \cdot 1 + 0 \cdot t$，其坐标向量为 $\begin{pmatrix} c \\ 0 \end{pmatrix}$。
-   因此，$L$ 相对于基 $\mathcal{B}$ 的矩阵为 $[L]_{\mathcal{B}} = \begin{pmatrix} 0  c \\ 0  0 \end{pmatrix}$。

**示例 2：从多项式空间到欧几里得空间** [@problem_id:1390578]
考虑一个更复杂的变换 $T: P_2 \to \mathbb{R}^3$，定义为 $T(p(t)) = (p(0), p'(0), \int_0^1 p(t) dt)$。其中 $P_2$ 是次数不超过2的多项式空间。我们使用 $P_2$ 的标准基 $\mathcal{B} = \{1, t, t^2\}$ 和 $\mathbb{R}^3$ 的标准基 $\mathcal{E}$。
-   $T(1)$: $p(t)=1 \implies p(0)=1, p'(0)=0, \int_0^1 1 dt = 1$。所以 $T(1) = (1,0,1)$。
-   $T(t)$: $p(t)=t \implies p(0)=0, p'(0)=1, \int_0^1 t dt = 1/2$。所以 $T(t) = (0,1,1/2)$。
-   $T(t^2)$: $p(t)=t^2 \implies p(0)=0, p'(0)=0, \int_0^1 t^2 dt = 1/3$。所以 $T(t^2) = (0,0,1/3)$。
由于到达域是 $\mathbb{R}^3$ 且我们使用其标准基，因此这些向量本身就是它们的坐标向量。将它们作为列，我们得到 $T$ 的标准矩阵：
$$
A = \begin{pmatrix} 1  0  0 \\ 0  1  0 \\ 1  1/2  1/3 \end{pmatrix}
$$

### 代数性质与基变换

矩阵表示不仅是计算工具，它还深刻地反映了线性变换的内在属性。

**可逆性**
一个线性变换 $T: \mathbb{R}^n \to \mathbb{R}^n$ 是可逆的，当且仅当它的标准矩阵 $A$ 是可逆矩阵。此外，逆变换 $T^{-1}$ 的标准矩阵恰好是 $A$ 的逆矩阵 $A^{-1}$。这一联系使得我们可以利用矩阵代数的工具来研究和计算逆变换。
例如，如果一个可逆变换 $T$ 的标准矩阵 $A$ 满足多项式方程 $A^2 - 3A + 2I = 0$ (其中 $I$ 是单位矩阵) [@problem_id:1390604]，我们可以通过代数操作找到 $A^{-1}$。
$$
A^2 - 3A + 2I = 0 \implies 2I = 3A - A^2
$$
提取公因子 $A$：
$$
2I = A(3I - A)
$$
根据逆矩阵的定义，如果一个矩阵 $C$ 满足 $AC=I$，则 $C$ 是 $A$ 的逆。从上式我们看到，$\frac{1}{2}(3I-A)$ 这个矩阵与 $A$ 的乘积为 $I$。因此：
$$
A^{-1} = \frac{1}{2}(3I - A)
$$
这表明，变换 $T^{-1}$ 的标准矩阵可以通过 $A$ 的简单线性组合得到，完全无需进行高斯-若尔当消元等标准求逆过程。

**基变换的视角**
一个变换的矩阵表示依赖于基的选择。有时，变换在一个非标准的基下具有更简单的形式。例如，对于一个变换 $T$，如果存在一个基 $\mathcal{B}=\{\mathbf{v}_1, \dots, \mathbf{v}_n\}$ 和一组标量 $\lambda_1, \dots, \lambda_n$ 使得 $T(\mathbf{v}_j) = \lambda_j \mathbf{v}_j$，那么在这个基下，$T$ 的矩阵表示将是一个非常简洁的对角矩阵。

考虑一个变换 $T: \mathbb{R}^2 \to \mathbb{R}^2$，它将向量 $\mathbf{v}_1 = (1,1)$ 映射到 $\alpha\mathbf{v}_1$，将向量 $\mathbf{v}_2 = (1,-1)$ 映射到 $\beta\mathbf{v}_2$ [@problem_id:1390598]。要找到它的标准矩阵 $A$，我们仍然需要计算 $T(\mathbf{e}_1)$ 和 $T(\mathbf{e}_2)$。

关键一步是先用基 $\{\mathbf{v}_1, \mathbf{v}_2\}$ 来表示标准基向量 $\mathbf{e}_1, \mathbf{e}_2$。通过解方程组可得：
$$
\mathbf{e}_1 = \frac{1}{2}(\mathbf{v}_1 + \mathbf{v}_2), \quad \mathbf{e}_2 = \frac{1}{2}(\mathbf{v}_1 - \mathbf{v}_2)
$$
现在利用 $T$ 的线性性质：
$$
\begin{align*}
T(\mathbf{e}_1)  = T\left(\frac{1}{2}(\mathbf{v}_1 + \mathbf{v}_2)\right) = \frac{1}{2}(T(\mathbf{v}_1) + T(\mathbf{v}_2)) = \frac{1}{2}(\alpha\mathbf{v}_1 + \beta\mathbf{v}_2) \\
 = \frac{1}{2}\left(\alpha\begin{pmatrix}1 \\ 1\end{pmatrix} + \beta\begin{pmatrix}1 \\ -1\end{pmatrix}\right) = \begin{pmatrix} (\alpha+\beta)/2 \\ (\alpha-\beta)/2 \end{pmatrix}
\end{align*}
$$
$$
\begin{align*}
T(\mathbf{e}_2)  = T\left(\frac{1}{2}(\mathbf{v}_1 - \mathbf{v}_2)\right) = \frac{1}{2}(T(\mathbf{v}_1) - T(\mathbf{v}_2)) = \frac{1}{2}(\alpha\mathbf{v}_1 - \beta\mathbf{v}_2) \\
 = \frac{1}{2}\left(\alpha\begin{pmatrix}1 \\ 1\end{pmatrix} - \beta\begin{pmatrix}1 \\ -1\end{pmatrix}\right) = \begin{pmatrix} (\alpha-\beta)/2 \\ (\alpha+\beta)/2 \end{pmatrix}
\end{align*}
$$
因此，标准矩阵为：
$$
A = \begin{pmatrix} (\alpha+\beta)/2  (\alpha-\beta)/2 \\ (\alpha-\beta)/2  (\alpha+\beta)/2 \end{pmatrix}
$$
这个例子完美地展示了如何在不同基的描述之间进行转换，这是线性代数中一个更深层次且极为有用的主题。

### 结论

将线性变换与矩阵联系起来是线性代数中最具威力的思想之一。通过遵循一个简单的构造规则——标准矩阵的列就是标准基向量的像——我们可以为任何有限维向量空间之间的线性变换赋予一个具体的、可计算的代数形式。这一工具不仅使我们能够高效地计算变换的结果，更重要的是，它将变换的几何与代数属性（如复合、可逆性）转化为矩阵的相应属性（矩阵乘法、矩阵求逆）。这为我们运用整个矩阵理论的武库来深入探索和理解线性变换的广阔世界打开了大门。