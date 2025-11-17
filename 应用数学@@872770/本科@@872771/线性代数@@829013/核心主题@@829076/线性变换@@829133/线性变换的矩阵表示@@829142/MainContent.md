## 引言
在线性代数中，[线性变换](@entry_id:149133)是连接不同[向量空间的基](@entry_id:191509)础，但其抽象的函数形式不利于直接的数值计算。为了将这些强大的代数概念应用于[计算机图形学](@entry_id:148077)、物理学或数据科学等实际问题中，我们需要一种工具来将它们具体化并进行操作。这个核心工具就是矩阵，它为我们提供了一座连接抽象理论与具体计算的桥梁。

本文旨在系统性地阐明如何为任意一个线性变换找到其唯一的[矩阵表示](@entry_id:146025)。通过本文，你将全面掌握这一关键技术。在“原理与机制”一章，我们将深入探讨构建变换矩阵的核心步骤、复合变换与矩阵乘法的关系，以及不同基下的矩阵表示如何通过相似性联系起来。随后，在“应用与跨学科联系”一章，我们将领略这一概念在几何变换、微[积分算子](@entry_id:262332)、物理模型等多个[交叉](@entry_id:147634)学科中的强大应用。最后，“动手实践”部分将通过精选习题，帮助你巩固和检验学习成果。

让我们开始这段旅程，揭示如何将一个抽象的变换“编码”到一个矩阵中，并释放其在科学与工程计算中的全部潜力。

## 原理与机制

在线性代数的研究中，我们已经了解线性变换是连接两个[向量空间的基](@entry_id:191509)本结构。然而，线性变换作为一种抽象的函数，其本身不便于进行具体的数值计算。为了将这些抽象的代数概念应用于实际问题，例如计算机图形学中的几何变换、物理学中的算子运算，或是数据科学中的[数据转换](@entry_id:170268)，我们需要一种能够将它们“具象化”的工具。这个工具就是**矩阵**。

本章的核心任务是建立[线性变换](@entry_id:149133)与矩阵之间的精确联系。我们将阐明，一旦为[定义域和陪域](@entry_id:159300)[向量空间](@entry_id:151108)选定一组基，任何[线性变换](@entry_id:149133)都可以用一个唯一的矩阵来表示。这个矩阵不仅封装了变换的全部信息，还使得我们可以利用成熟的矩阵运算（如[矩阵乘法](@entry_id:156035)和求逆）来分析和计算线性变换，从而实现从抽象理论到具体计算的跨越。

### 核心构造方法：如何构建变换矩阵

将一个抽象的[线性变换](@entry_id:149133) $T: V \to W$ 转化为一个具体的矩阵，其过程系统而直接。这里的关键在于，一个[线性变换](@entry_id:149133)的全部行为，完全由它如何作用于定义域 $V$ 的一组[基向量](@entry_id:199546)所决定。一旦我们知道[基向量](@entry_id:199546)的“像”（images），我们就能通过线性组合，确定空间中任何一个向量的像。

设 $V$ 是一个 $n$ 维[向量空间](@entry_id:151108)，其基为 $\mathcal{B} = \{\mathbf{v}_1, \mathbf{v}_2, \dots, \mathbf{v}_n\}$。设 $W$ 是一个 $m$ 维[向量空间](@entry_id:151108)，其基为 $\mathcal{C} = \{\mathbf{w}_1, \mathbf{w}_2, \dots, \mathbf{w}_m\}$。我们希望找到一个 $m \times n$ 的矩阵，记作 $[T]_{\mathcal{B}}^{\mathcal{C}}$，它代表了在基 $\mathcal{B}$ 和 $\mathcal{C}$ 下的[线性变换](@entry_id:149133) $T$。

构造这个矩阵的步骤如下：

1.  **施加变换**：将变换 $T$ 依次施加于定义域 $V$ 的每一个[基向量](@entry_id:199546) $\mathbf{v}_j$（其中 $j=1, 2, \dots, n$），得到一系列位于陪域 $W$ 中的向量 $T(\mathbf{v}_j)$。

2.  **寻找坐标**：对于每一个得到的向量 $T(\mathbf{v}_j)$，我们将其表示为陪域基 $\mathcal{C}$ 中[基向量](@entry_id:199546)的线性组合。也就是说，我们要找到一组唯一的标量系数 $a_{1j}, a_{2j}, \dots, a_{mj}$，使得：
    $T(\mathbf{v}_j) = a_{1j}\mathbf{w}_1 + a_{2j}\mathbf{w}_2 + \dots + a_{mj}\mathbf{w}_m$

3.  **构建列向量**：这组标量系数构成了向量 $T(\mathbf{v}_j)$ 在基 $\mathcal{C}$下的**[坐标向量](@entry_id:153319)**，记作 $[T(\mathbf{v}_j)]_{\mathcal{C}}$。我们将这个[坐标向量](@entry_id:153319)写成一个列向量：
    $[T(\mathbf{v}_j)]_{\mathcal{C}} = \begin{pmatrix} a_{1j} \\ a_{2j} \\ \vdots \\ a_{mj} \end{pmatrix}$

4.  **组合成矩阵**：将这 $n$ 个列向量按顺序[排列](@entry_id:136432)，就构成了我们所寻求的 $m \times n$ 矩阵 $[T]_{\mathcal{B}}^{\mathcal{C}}$。其第 $j$ 列就是 $T(\mathbf{v}_j)$ 在基 $\mathcal{C}$ 下的[坐标向量](@entry_id:153319)：
    $[T]_{\mathcal{B}}^{\mathcal{C}} = \begin{pmatrix} |  |   | \\ [T(\mathbf{v}_1)]_{\mathcal{C}}  [T(\mathbf{v}_2)]_{\mathcal{C}}  \dots  [T(\mathbf{v}_n)]_{\mathcal{C}} \\ |  |   | \end{pmatrix}$

这个过程是构建所有[变换矩阵](@entry_id:151616)的基石。让我们通过几个例子来深入理解它。

**例1：从输入基到输出基的直接映射**

考虑一个物理场景，其中一个二维各向异性材料对外部场的响应由一个[线性变换](@entry_id:149133) $T: \mathbb{R}^2 \to \mathbb{R}^2$ 描述。输入场向量最好用材料[主轴](@entry_id:172691)对应的基 $\mathcal{B} = \{\mathbf{b}_1, \mathbf{b}_2\}$ 来描述，其中 $\mathbf{b}_1 = (1, 1)$，$\mathbf{b}_2 = (1, -1)$。而输出的响应向量则在实验室的标准[坐标系](@entry_id:156346)（标准基 $\mathcal{E} = \{\mathbf{e}_1, \mathbf{e}_2\}$）下测量。实验测得：
- $T(\mathbf{b}_1) = (5, 2)$
- $T(\mathbf{b}_2) = (1, 0)$

要找到将输入向量的 $\mathcal{B}$-坐标 映射到输出向量的 $\mathcal{E}$-坐标 的矩阵 $[T]_{\mathcal{B}}^{\mathcal{E}}$，我们只需遵循上述步骤。
1.  变换后的向量已知：$T(\mathbf{b}_1) = (5, 2)$ 和 $T(\mathbf{b}_2) = (1, 0)$。
2.  这些向量在标准基 $\mathcal{E}$ 下的坐标是它们自身。即 $[T(\mathbf{b}_1)]_{\mathcal{E}} = \begin{pmatrix} 5 \\ 2 \end{pmatrix}$ 和 $[T(\mathbf{b}_2)]_{\mathcal{E}} = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$。
3.  将这些[坐标向量](@entry_id:153319)作为列，我们立即得到[变换矩阵](@entry_id:151616)：
    $[T]_{\mathcal{B}}^{\mathcal{E}} = \begin{pmatrix} 5  1 \\ 2  0 \end{pmatrix}$
这个矩阵完美地捕捉了变换的本质：它直接告诉我们定义域的[基向量](@entry_id:199546)会被映射到哪里 [@problem_id:1377732]。

**例2：[微积分中的线性](@entry_id:276708)算子**

[线性变换](@entry_id:149133)的概念远不止于几何向量。微积分中的**[微分](@entry_id:158718)**和**积分**算子也是线性的。
考虑[微分算子](@entry_id:140145) $D: \mathbb{P}_2 \to \mathbb{P}_1$，它将一个次数不超过2的多项式 $p(t) = c_0 + c_1t + c_2t^2$ 映射到其导数 $p'(t) = c_1 + 2c_2t$。我们可以在标准单项式基 $\mathcal{B} = \{1, t, t^2\}$ 和 $\mathcal{C} = \{1, t\}$ 下找到它的[矩阵表示](@entry_id:146025)。
1.  对 $\mathcal{B}$ 中的[基向量](@entry_id:199546)求导：
    $D(1) = 0$
    $D(t) = 1$
    $D(t^2) = 2t$
2.  在 $\mathcal{C}$ 基下表示这些结果：
    $0 = 0 \cdot 1 + 0 \cdot t \implies [D(1)]_{\mathcal{C}} = \begin{pmatrix} 0 \\ 0 \end{pmatrix}$
    $1 = 1 \cdot 1 + 0 \cdot t \implies [D(t)]_{\mathcal{C}} = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$
    $2t = 0 \cdot 1 + 2 \cdot t \implies [D(t^2)]_{\mathcal{C}} = \begin{pmatrix} 0 \\ 2 \end{pmatrix}$
3.  组合成矩阵：
    $[D]_{\mathcal{B}}^{\mathcal{C}} = \begin{pmatrix} 0  1  0 \\ 0  0  2 \end{pmatrix}$
这个矩阵使得我们可以用矩阵乘法来执行[微分](@entry_id:158718)运算 [@problem_id:1377749]。

同样，我们可以为积分算子 $I: \mathbb{P}_1 \to \mathbb{P}_2$ 定义为 $I(p(x)) = \int_0^x p(t) dt$ 找到矩阵表示。这次我们使用非标准基 $\mathcal{B} = \{1+x, 1-x\}$ 作为定义域基，标准基 $\mathcal{C} = \{1, x, x^2\}$ 作为陪域基。
1.  对 $\mathcal{B}$ 中的[基向量](@entry_id:199546)积分：
    $I(1+x) = \int_0^x (1+t) dt = x + \frac{1}{2}x^2$
    $I(1-x) = \int_0^x (1-t) dt = x - \frac{1}{2}x^2$
2.  在 $\mathcal{C}$ 基下表示这些结果：
    $x + \frac{1}{2}x^2 = 0 \cdot 1 + 1 \cdot x + \frac{1}{2} \cdot x^2 \implies [I(1+x)]_{\mathcal{C}} = \begin{pmatrix} 0 \\ 1 \\ \frac{1}{2} \end{pmatrix}$
    $x - \frac{1}{2}x^2 = 0 \cdot 1 + 1 \cdot x - \frac{1}{2} \cdot x^2 \implies [I(1-x)]_{\mathcal{C}} = \begin{pmatrix} 0 \\ 1 \\ -\frac{1}{2} \end{pmatrix}$
3.  组合成矩阵：
    $[I]_{\mathcal{B}}^{\mathcal{C}} = \begin{pmatrix} 0  0 \\ 1  1 \\ \frac{1}{2}  -\frac{1}{2} \end{pmatrix}$
这个例子强调了，即使基是非标准的，构造方法依然完全相同 [@problem_id:1377766]。

**例3：在非标准基之间转换**

当[定义域和陪域](@entry_id:159300)都使用非标准基时，挑战性会增加，但这更能体现该方法的普适性。考虑线性变换 $L: \mathbb{P}_2 \to \mathbb{P}_1$，定义为 $L(p(x)) = (p(1) - p(0))x + p'(0)$。我们希望找到它在基 $\mathcal{B} = \{1, x-1, (x-1)^2\}$（对于 $\mathbb{P}_2$）和 $\mathcal{C} = \{1+x, 1-x\}$（对于 $\mathbb{P}_1$）下的矩阵。

-   对于 $\mathbf{b}_1 = 1$：$L(1) = (1-1)x + 0 = 0$。我们需要将 $0$ 表示为 $\mathcal{C}$ 的线性组合：$0 = c_1(1+x) + c_2(1-x)$，显然 $c_1=0, c_2=0$。所以第一列是 $\begin{pmatrix} 0 \\ 0 \end{pmatrix}$。
-   对于 $\mathbf{b}_2 = x-1$：$L(x-1) = (0 - (-1))x + 1 = 1+x$。这恰好是 $\mathcal{C}$ 的第一个[基向量](@entry_id:199546)，所以 $1+x = 1 \cdot (1+x) + 0 \cdot (1-x)$。第二列是 $\begin{pmatrix} 1 \\ 0 \end{pmatrix}$。
-   对于 $\mathbf{b}_3 = (x-1)^2$：$L((x-1)^2) = (0-1)x + (-2) = -x-2$。我们需要求解 $-x-2 = c_1(1+x) + c_2(1-x) = (c_1+c_2) + (c_1-c_2)x$。通过匹配系数，我们得到[方程组](@entry_id:193238) $c_1+c_2 = -2$ 和 $c_1-c_2 = -1$，解得 $c_1 = -3/2$，$c_2 = -1/2$。第三列是 $\begin{pmatrix} -3/2 \\ -1/2 \end{pmatrix}$。

将这些列组合起来，得到最终的变换矩阵：
$[L]_{\mathcal{B}}^{\mathcal{C}} = \begin{pmatrix} 0  1  -\frac{3}{2} \\ 0  0  -\frac{1}{2} \end{pmatrix}$
这个例子全面地展示了如何处理抽象空间和非标准基 [@problem_id:1377756]。

最后，最简单的变换——零变换 $Z: V \to W$，它将每个向量映射到零向量，其[矩阵表示](@entry_id:146025)是什么？对于任何定义域[基向量](@entry_id:199546) $\mathbf{v}_j$，$Z(\mathbf{v}_j) = \mathbf{0}_W$。而零向量在任何基下的坐标都是零。因此，零变换的矩阵表示总是**[零矩阵](@entry_id:155836)** [@problem_id:1377753]。

### 复合变换的矩阵表示

在实践中，我们常常需要将多个[线性变换](@entry_id:149133)接连施加，形成一个**复合变换**。例如，在计算机图形学中，一个对象的动画可能需要先旋转，再缩放，最后平移。如果 $T_1: U \to V$ 和 $T_2: V \to W$ 是两个[线性变换](@entry_id:149133)，它们的复合变换 $T = T_2 \circ T_1$ 是一个从 $U$ 到 $W$ 的新线性变换。

[矩阵表示](@entry_id:146025)的一个强大之处在于，它将复合变换的抽象概念转化为具体的**[矩阵乘法](@entry_id:156035)**。若 $\mathcal{B}, \mathcal{C}, \mathcal{D}$ 分别是 $U, V, W$ 的基，则复合变换 $T$ 的矩阵表示满足以下优雅的定理：
$[T_2 \circ T_1]_{\mathcal{B}}^{\mathcal{D}} = [T_2]_{\mathcal{C}}^{\mathcal{D}} [T_1]_{\mathcal{B}}^{\mathcal{C}}$

这里的矩阵乘法顺序至关重要：变换施加的顺序是从右到左（先 $T_1$ 后 $T_2$），而矩阵相乘的顺序也是从右到左。同时，内侧的基（这里是 $\mathcal{C}$）必须匹配。

**例1：几何[变换的复合](@entry_id:149828)**

考虑一个三维空间中的变换 $T: \mathbb{R}^3 \to \mathbb{R}^3$，它由两步构成：首先将向量沿 $xy$-平面对称（变换 $F$），然后将结果向量的长度均匀放大7倍（变换 $G$）。即 $T = G \circ F$。
在标准基下：
-   $F$ 将 $(x, y, z)$ 变为 $(x, y, -z)$，其矩阵为 $[F] = \begin{pmatrix} 1  0  0 \\ 0  1  0 \\ 0  0  -1 \end{pmatrix}$。
-   $G$ 将 $(x, y, z)$ 变为 $(7x, 7y, 7z)$，其矩阵为 $[G] = \begin{pmatrix} 7  0  0 \\ 0  7  0 \\ 0  0  7 \end{pmatrix}$。
复合变换 $T$ 的矩阵就是这两个矩阵的乘积：
$[T] = [G][F] = \begin{pmatrix} 7  0  0 \\ 0  7  0 \\ 0  0  7 \end{pmatrix} \begin{pmatrix} 1  0  0 \\ 0  1  0 \\ 0  0  -1 \end{pmatrix} = \begin{pmatrix} 7  0  0 \\ 0  7  0 \\ 0  0  -7 \end{pmatrix}$
这个结果直观地告诉我们，整个过程就是将 $x, y$ 坐标放大7倍，并将 $z$ 坐标反向后再放大7倍 [@problem_id:1377775]。

另一个几何例子是先将 $\mathbb{R}^3$ 中的向量[正交投影](@entry_id:144168)到 $xy$-平面（变换 $P$），然后绕 $z$ 轴逆时针旋转角度 $\theta$（变换 $R_z(\theta)$）。
-   [投影矩阵](@entry_id:154479)为 $[P] = \begin{pmatrix} 1  0  0 \\ 0  1  0 \\ 0  0  0 \end{pmatrix}$。
-   [旋转矩阵](@entry_id:140302)为 $[R_z(\theta)] = \begin{pmatrix} \cos\theta  -\sin\theta  0 \\ \sin\theta  \cos\theta  0 \\ 0  0  1 \end{pmatrix}$。
复合变换 $T = R_z(\theta) \circ P$ 的矩阵为：
$[T] = [R_z(\theta)][P] = \begin{pmatrix} \cos\theta  -\sin\theta  0 \\ \sin\theta  \cos\theta  0 \\ 0  0  1 \end{pmatrix} \begin{pmatrix} 1  0  0 \\ 0  1  0 \\ 0  0  0 \end{pmatrix} = \begin{pmatrix} \cos\theta  -\sin\theta  0 \\ \sin\theta  \cos\theta  0 \\ 0  0  0 \end{pmatrix}$
这个矩阵清晰地显示，任何向量的 $z$ 分量都将变为0，而其 $x, y$ 分量则经历一次二维旋转 [@problem_id:1377785]。

**例2：抽象空间的复合变换**

复合规则同样适用于更抽象的空间。考虑一个从 $\mathbb{R}^3$ 到 $\mathbb{P}_1(\mathbb{R})$ 的复合变换 $T = T_2 \circ T_1$。
-   $T_1: \mathbb{R}^3 \to \mathbb{P}_2(\mathbb{R})$ 定义为 $T_1(a, b, c) = (a - b) + (b - c)x + (c - a)x^2$。
-   $T_2: \mathbb{P}_2(\mathbb{R}) \to \mathbb{P}_1(\mathbb{R})$ 定义为 $T_2(p(x)) = p(1) + p'(0)x$。

我们可以直接计算复合变换作用在定义域[基向量](@entry_id:199546)上的效果来求得最终矩阵。例如，在 $\mathbb{R}^3$ 的基 $\mathcal{B} = \{(1, 1, 0), (0, 1, 1), (1, 0, 1)\}$ 和 $\mathbb{P}_1$ 的基 $\mathcal{C} = \{1+x, 1-x\}$ 下，我们可以对 $\mathcal{B}$ 中的每个向量 $\mathbf{v}_i$ 计算 $T(\mathbf{v}_i) = T_2(T_1(\mathbf{v}_i))$，然后找到结果在 $\mathcal{C}$ 下的坐标。这个过程虽然涉及多个步骤，但最终仍归结为我们最初的核心构造方法 [@problem_id:1377729]。

### [基变换](@entry_id:189626)与矩阵的相似性

到目前为止，我们都假设基是固定的。但一个核心问题是：如果为同一个[向量空间](@entry_id:151108)选择不同的基，同一个[线性变换的矩阵表示](@entry_id:162822)会如何变化？这在实践中非常重要，因为某些基（如[特征向量](@entry_id:151813)组成的基）可以极大地简化变换的矩阵。

考虑一个[线性算子](@entry_id:149003) $T: V \to V$。假设它在“旧”基 $\mathcal{E}$ 下的矩阵是 $[T]_{\mathcal{E}}$，在“新”基 $\mathcal{B}$ 下的矩阵是 $[T]_{\mathcal{B}}$。这两个矩阵之间存在一个深刻的联系，该联系由**[基变换矩阵](@entry_id:184480)** $P$ 建立。

**[基变换矩阵](@entry_id:184480)** $P_{\mathcal{B} \to \mathcal{E}}$ 是一个其列由新基 $\mathcal{B}$ 的向量在旧基 $\mathcal{E}$ 下的坐标构成的矩阵。它的作用是将一个向量的“新”坐标转换为“旧”坐标：$[\mathbf{v}]_{\mathcal{E}} = P_{\mathcal{B} \to \mathcal{E}} [\mathbf{v}]_{\mathcal{B}}$。相应地，$P^{-1}$ 则执行相反的操作。

我们可以推导出 $[T]_{\mathcal{B}}$ 和 $[T]_{\mathcal{E}}$ 之间的关系：
$[T]_{\mathcal{B}} = P^{-1} [T]_{\mathcal{E}} P$
这个关系被称为**[相似变换](@entry_id:152935)**。如果两个矩阵 $A$ 和 $B$ 存在一个可逆矩阵 $P$ 使得 $B = P^{-1}AP$，则称 $A$ 和 $B$ **相似**。因此，同一个线性算子在不同基下的矩阵彼此相似。

**例1：从标准基到非标准基**

给定一个变换 $T(x, y) = (x + 2y, 3x + 4y)$，其在标准基 $\mathcal{E}$ 下的矩阵是 $[T]_{\mathcal{E}} = \begin{pmatrix} 1  2 \\ 3  4 \end{pmatrix}$。我们想找到它在一个新基 $\mathcal{B} = \{(1, 1), (1, -1)\}$ 下的矩阵 $[T]_{\mathcal{B}}$。
[基变换矩阵](@entry_id:184480) $P = P_{\mathcal{B} \to \mathcal{E}}$ 的列是 $\mathcal{B}$ 的[基向量](@entry_id:199546)：$P = \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}$。
我们计算其[逆矩阵](@entry_id:140380) $P^{-1} = \frac{1}{-2} \begin{pmatrix} -1  -1 \\ -1  1 \end{pmatrix} = \begin{pmatrix} 1/2  1/2 \\ 1/2  -1/2 \end{pmatrix}$。
现在，我们可以通过相似变换计算新矩阵：
$[T]_{\mathcal{B}} = P^{-1} [T]_{\mathcal{E}} P = \begin{pmatrix} 1/2  1/2 \\ 1/2  -1/2 \end{pmatrix} \begin{pmatrix} 1  2 \\ 3  4 \end{pmatrix} \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}$
执行[矩阵乘法](@entry_id:156035)后，我们将得到 $T$ 在新基 $\mathcal{B}$ 下的表示。一个重要的[不变量](@entry_id:148850)是矩阵的迹（对角线元素之和）：[相似矩阵](@entry_id:155833)的迹相等。对于 $[T]_{\mathcal{E}}$，迹是 $1+4=5$，因此我们知道 $[T]_{\mathcal{B}}$ 的迹也必须是5 [@problem_id:1377774]。

**例2：从特殊基到标准基**

反向操作同样重要。假设我们知道一个算子 $T$ 在某个特殊基 $\mathcal{B} = \{\mathbf{v}_1, \mathbf{v}_2, \mathbf{v}_3\}$ 下的矩阵 $[T]_{\mathcal{B}}$ 是一个简单的对角矩阵 $D$，这意味着 $\mathcal{B}$ 是由 $T$ 的[特征向量](@entry_id:151813)组成的基。
例如，设 $\mathcal{B} = \{\begin{pmatrix} 1 \\ 0 \\ 1 \end{pmatrix}, \begin{pmatrix} -1 \\ 1 \\ 0 \end{pmatrix}, \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}\}$，且 $[T]_{\mathcal{B}} = D = \begin{pmatrix} 2  0  0 \\ 0  -1  0 \\ 0  0  3 \end{pmatrix}$。
我们想找到 $T$ 在标准基 $\mathcal{E}$ 下的矩阵 $[T]_{\mathcal{E}}$。
[相似变换](@entry_id:152935)公式可以重写为：$[T]_{\mathcal{E}} = P [T]_{\mathcal{B}} P^{-1}$。
[基变换矩阵](@entry_id:184480) $P$ 的列是 $\mathcal{B}$ 中的向量：$P = \begin{pmatrix} 1  -1  1 \\ 0  1  1 \\ 1  0  1 \end{pmatrix}$。
在计算出 $P^{-1}$ 后，我们就可以通过矩阵乘法 $P D P^{-1}$ 来重建[标准矩阵](@entry_id:151240) $[T]_{\mathcal{E}}$。这个过程揭示了对角化的深刻意义：它是在寻找一个能让[变换矩阵](@entry_id:151616)变得最简单的“理想”[坐标系](@entry_id:156346)（基）[@problem_id:1377759]。

### 高级主题：[对偶变换](@entry_id:137576)及其矩阵

每个[向量空间](@entry_id:151108) $V$ 都有一个与之关联的**[对偶空间](@entry_id:146945)** $V^*$，它由从 $V$ 到其标量域的所有线性函数（称为**线性泛函**）组成。如果 $T: V \to W$ 是一个[线性变换](@entry_id:149133)，那么它自然地诱导出一个**[对偶变换](@entry_id:137576)**（或**转置变换**）$T^*: W^* \to V^*$。其定义为，对于 $W^*$ 中的任何线性泛函 $f$，$T^*(f)$ 是 $V^*$ 中一个新的线性泛函，它作用于 $V$ 中向量 $\mathbf{v}$ 的方式是：$(T^*f)(\mathbf{v}) = f(T(\mathbf{v}))$。

这个抽象的定义在选择基后有一个非常简洁的矩阵表示。设 $[T]_{\mathcal{B}}^{\mathcal{C}} = A$ 是 $T$ 在基 $\mathcal{B}$ (for $V$) 和 $\mathcal{C}$ (for $W$)下的矩阵。设 $\mathcal{B}^*$ 和 $\mathcal{C}^*$ 是对应的对偶基。那么，[对偶变换](@entry_id:137576) $T^*$ 的矩阵 $[T^*]_{\mathcal{C}^*}^{\mathcal{B}^*}$ 与原矩阵 $A$ 的关系是：
$[T^*]_{\mathcal{C}^*}^{\mathcal{B}^*} = A^T$
即[对偶变换](@entry_id:137576)的矩阵就是原变换矩阵的**[转置](@entry_id:142115)**。

例如，如果一个变换 $T: \mathbb{P}_1 \to \mathbb{R}^3$ 在某组基下的[矩阵表示](@entry_id:146025)为 $A = \begin{pmatrix} 2  1 \\ 0  -1 \\ 1  3 \end{pmatrix}$，那么其[对偶变换](@entry_id:137576) $T^*: (\mathbb{R}^3)^* \to (\mathbb{P}_1)^*$ 在对应对偶基下的矩阵就是 $A^T = \begin{pmatrix} 2  0  1 \\ 1  -1  3 \end{pmatrix}$ [@problem_id:1377795]。这一性质揭示了线性变换与其对偶之间深刻的对称性，是线性代数中许多理论结果的基础。