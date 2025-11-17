## 引言
对称矩阵，以其简洁的 $A^T = A$ 形式，是线性代数中最优雅也最重要的一类对象之一。从描述物理系统中的[应力与应变](@entry_id:137374)，到数据科学中的协[方差](@entry_id:200758)结构，它们无处不在。然而，一个核心问题随之而来：我们如何才能深刻理解一个对称[线性变换](@entry_id:149133)的内在作用机理？是否存在一个“自然”的[坐标系](@entry_id:156346)，能将其复杂的、多变量耦合的作用，简化为一系列独立、清晰的[缩放变换](@entry_id:166413)？

[对称矩阵](@entry_id:143130)的谱定理（Spectral Theorem for Symmetric Matrices）为这个问题提供了完美的答案。它不仅是线性代数课程中的一个理论高峰，更是连接抽象数学与具体应用的坚实桥梁。该定理揭示了[对称矩阵](@entry_id:143130)深刻的几何结构，并提供了一个强大的“解耦”工具，这个工具在从量子力学到机器学习的众多领域中都至关重要。

本文将带领您系统地探索谱定理。在“**原则与机理**”一章中，我们将揭示该定理的核心论断，并深入其背后的数学原理，理解为何对称性保证了[正交对角化](@entry_id:149411)的可能性。接着，在“**应用与跨学科联系**”一章中，我们将跨越学科界限，见证[谱定理](@entry_id:136620)如何在几何学、物理学、工程学和现代数据科学等领域大放异彩，成为解决实际问题的关键工具。最后，在“**动手实践**”部分，您将通过具体的计算练习，将理论知识转化为解决问题的实用技能。

## 原则与机理

在本章中，我们将深入探讨[实对称矩阵](@entry_id:192806)的一项核心性质，这一性质在线性代数及其应用中占据着至关重要的地位。这项被称为谱定理的结论，不仅揭示了对称矩阵深刻的几何结构，也为从量子力学到数据科学等众多领域提供了强大的分析工具。我们将系统地阐述该定理背后的基本原则与作用机理。

### 对称矩阵与[正交对角化](@entry_id:149411)

我们首先从一个核心的等价关系开始。在线性代数中，一个实方阵 $A$ 被称为**可[对角化](@entry_id:147016)**的，如果存在一个可逆矩阵 $P$ 和一个[对角矩阵](@entry_id:637782) $D$，使得 $A = PDP^{-1}$。这一过程的几何意义在于，它为[向量空间](@entry_id:151108) $\mathbb{R}^n$ 找到了一组由 $A$ 的[特征向量](@entry_id:151813)构成的基。在此基下，[线性变换](@entry_id:149133) $A$ 的作用变得异常简单，仅仅是对[基向量](@entry_id:199546)进行缩放。

一个更强的概念是**[正交对角化](@entry_id:149411)**。一个实方阵 $A$ 被称为可[正交对角化](@entry_id:149411)的，如果存在一个**[正交矩阵](@entry_id:169220)** $P$（即满足 $P^T P = I$，或等价地 $P^{-1} = P^T$）和一个对角矩阵 $D$，使得 $A = PDP^T$。这里的关键在于，用于[对角化](@entry_id:147016)的基不仅是[特征向量](@entry_id:151813)，而且是一个**标准正交基**。这意味着[基向量](@entry_id:199546)之间不仅线性无关，还两两正交且长度为1。

那么，哪些矩阵拥有如此优美的性质呢？谱定理给出了一个简洁而深刻的回答：

**一个实方阵 $A$ 是可[正交对角化](@entry_id:149411)的，当且仅当它是[对称矩阵](@entry_id:143130)。**

[对称矩阵](@entry_id:143130)是指满足 $A^T = A$ 的矩阵。这个“当且仅当”的论断包含两个方面：

1.  如果一个矩阵 $A$ 可以被[正交对角化](@entry_id:149411)为 $A = PDP^T$，那么它必定是对称的。这个方向的证明非常直接。由于 $D$ 是[对角矩阵](@entry_id:637782)，所以 $D^T = D$。我们对表达式进行[转置](@entry_id:142115)：
    $A^T = (PDP^T)^T = (P^T)^T D^T P^T = PDP^T = A$
    这证明了可[正交对角化](@entry_id:149411)的矩阵必然是对称的。

2.  如果一个矩阵 $A$ 是对称的，那么它一定可以被[正交对角化](@entry_id:149411)。这个方向的证明更为深刻，构成了本章后续讨论的核心。

这个定理为我们提供了一个无需计算[特征值](@entry_id:154894)或[特征向量](@entry_id:151813)，就能直接判断矩阵是否可被[正交对角化](@entry_id:149411)的强大准则 [@problem_id:1390331]。例如，给定以下矩阵：
$M_A = \begin{pmatrix} 3  & -7 \\ -7 & 1 \end{pmatrix}$, $M_B = \begin{pmatrix} 1  & 4 \\ 0  & 2 \end{pmatrix}$, $M_C = \begin{pmatrix} 5  & 0 \\ 0  & -9 \end{pmatrix}$
我们只需检查其对称性。$M_A$ 是对称的，因为 $(M_A)_{12} = (M_A)_{21} = -7$。$M_C$ 是一个[对角矩阵](@entry_id:637782)，而所有[对角矩阵](@entry_id:637782)都是对称的。因此，$M_A$ 和 $M_C$ 保证是可[正交对角化](@entry_id:149411)的。相反，$M_B$ 不是对称的，因此它不能被[正交对角化](@entry_id:149411)。

这个[等价关系](@entry_id:138275)的重要性也体现在其[逆否命题](@entry_id:265332)上。如果一个矩阵 $A$ 已知拥有一组覆盖整个空间的相互正交的[特征向量](@entry_id:151813)，那么它必须是对称的 [@problem_id:1390342]。例如，若矩阵 $A = \begin{pmatrix} 3 & x \\ y & 5 \end{pmatrix}$ 拥有两个正交的[特征向量](@entry_id:151813) $\mathbf{v}_1 = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$ 和 $\mathbf{v}_2 = \begin{pmatrix} -2 \\ 1 \end{pmatrix}$（它们的[点积](@entry_id:149019)为 $1(-2) + 2(1) = 0$），那么[谱定理](@entry_id:136620)的逆向论断告诉我们 $A$ 必须是对称的。这意味着它的非对角元素必须相等，即 $x = y$。这一关系，结合[特征向量](@entry_id:151813)的定义 $A\mathbf{v} = \lambda\mathbf{v}$，足以确定未知参数 $x$ 和 $y$ 的值。

### [对称矩阵](@entry_id:143130)的核心性质

为了理解为何所有对称矩阵都能被[正交对角化](@entry_id:149411)，我们需要探究它们所具备的几个基本而关键的性质。这些性质共同构成了谱定理的基石。

#### 性质 1：实[特征值](@entry_id:154894)

**一个[实对称矩阵](@entry_id:192806)的所有[特征值](@entry_id:154894)都是实数。**

对于一般的实矩阵，[特征值](@entry_id:154894)可以是复数。例如，旋转矩阵 $\begin{pmatrix} 0  & -1 \\ 1  & 0 \end{pmatrix}$ 的[特征值](@entry_id:154894)为 $\pm i$。然而，对称性排除了这种可能性。虽然严格的证明需要使用复数共轭，但其结论是坚实的：我们无需担心在[对角化](@entry_id:147016)过程中会遇到复数。

我们可以通过一个具体的例子来验证这一点。在[材料科学](@entry_id:152226)中，一个点的应变状态可以用一个 $2 \times 2$ 的[对称矩阵](@entry_id:143130)——应变张量来描述。其[特征值](@entry_id:154894)被称为[主应变](@entry_id:197797)，物理上代表了该点的最大和最小拉伸或压缩。考虑应变张量 [@problem_id:1390373]：
$$
S = \begin{pmatrix} 5  & 3 \\ 3  & 1 \end{pmatrix}
$$
它的特征方程是 $\det(S - \lambda I) = 0$，即 $(5 - \lambda)(1 - \lambda) - 9 = \lambda^2 - 6\lambda - 4 = 0$。根据二次公式，[特征值](@entry_id:154894)为：
$$
\lambda = \frac{6 \pm \sqrt{36 - 4(-4)}}{2} = 3 \pm \sqrt{13}
$$
正如理论所预言，这两个[特征值](@entry_id:154894) $3 - \sqrt{13}$ 和 $3 + \sqrt{13}$ 都是实数。

#### 性质 2：正交的[特征向量](@entry_id:151813)

**一个[实对称矩阵](@entry_id:192806)的对应于不同[特征值](@entry_id:154894)的[特征向量](@entry_id:151813)是相互正交的。**

这是[谱定理](@entry_id:136620)最核心的几何性质。假设 $\lambda_1$ 和 $\lambda_2$ 是[对称矩阵](@entry_id:143130) $A$ 的两个不同[特征值](@entry_id:154894)，对应的[特征向量](@entry_id:151813)分别为 $\mathbf{v}_1$ 和 $\mathbf{v_2}$。即 $A\mathbf{v}_1 = \lambda_1 \mathbf{v}_1$ 和 $A\mathbf{v}_2 = \lambda_2 \mathbf{v}_2$。

我们来考察标量 $\mathbf{v}_1^T A \mathbf{v}_2$。我们可以从两种方式计算它：
$$
\mathbf{v}_1^T (A \mathbf{v}_2) = \mathbf{v}_1^T (\lambda_2 \mathbf{v}_2) = \lambda_2 (\mathbf{v}_1^T \mathbf{v}_2)
$$
另一方面，利用矩阵[转置的性质](@entry_id:148302) $(XY)^T = Y^T X^T$ 和 $A$ 的对称性 $A^T=A$，我们得到：
$$
\mathbf{v}_1^T A \mathbf{v}_2 = (A^T \mathbf{v}_1)^T \mathbf{v}_2 = (A \mathbf{v}_1)^T \mathbf{v}_2 = (\lambda_1 \mathbf{v}_1)^T \mathbf{v}_2 = \lambda_1 (\mathbf{v}_1^T \mathbf{v}_2)
$$
比较两种计算结果，我们有 $\lambda_2 (\mathbf{v}_1^T \mathbf{v}_2) = \lambda_1 (\mathbf{v}_1^T \mathbf{v}_2)$，即 $(\lambda_1 - \lambda_2)(\mathbf{v}_1^T \mathbf{v}_2) = 0$。由于我们假设了 $\lambda_1 \neq \lambda_2$，因此唯一的可能性就是 $\mathbf{v}_1^T \mathbf{v}_2 = 0$。这正是向量 $\mathbf{v}_1$ 和 $\mathbf{v}_2$ 正交的定义。

以矩阵 $A = \begin{pmatrix} 6  & -2  & -1 \\ -2  & 6  & -1 \\ -1  & -1  & 5 \end{pmatrix}$ 为例 [@problem_id:1390363]，我们可以找到它的三个[特征值](@entry_id:154894)分别为 $3, 6, 8$。对应的[特征向量](@entry_id:151813)分别是 $\mathbf{v}_1 = \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}$, $\mathbf{v}_2 = \begin{pmatrix} 1 \\ 1 \\ -2 \end{pmatrix}$ 和 $\mathbf{v}_3 = \begin{pmatrix} 1 \\ -1 \\ 0 \end{pmatrix}$。我们可以轻易验证它们之间的正交性：
$\mathbf{v}_1 \cdot \mathbf{v}_2 = 1(1)+1(1)+1(-2)=0$
$\mathbf{v}_1 \cdot \mathbf{v}_3 = 1(1)+1(-1)+1(0)=0$
$\mathbf{v}_2 \cdot \mathbf{v}_3 = 1(1)+1(-1)+(-2)(0)=0$
它们构成了一个[正交基](@entry_id:264024)。

重要的是要认识到，这种正交性是**对称性**的直接产物。对于一个[非对称矩阵](@entry_id:153254)，即使它拥有不同的实[特征值](@entry_id:154894)，其[特征向量](@entry_id:151813)也通常不是正交的 [@problem_id:1390369]。例如，矩阵 $A = \begin{pmatrix} 1  & 1 \\ -2  & 4 \end{pmatrix}$ 有两个实[特征值](@entry_id:154894) $\lambda_1 = 2$ 和 $\lambda_2 = 3$，但其对应的[特征向量](@entry_id:151813) $\mathbf{v}_1 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$ 和 $\mathbf{v}_2 = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$ 的[点积](@entry_id:149019)为 $3$，显然不正交。

#### 性质 3：不变的[子空间](@entry_id:150286)

在构建完整的正交[特征基](@entry_id:151409)时，我们需要处理[特征值](@entry_id:154894)有重根（即[特征空间](@entry_id:638014)维度大于1）的情况。此时，一个更微妙的性质——[不变子空间](@entry_id:152829)——变得至关重要。

**如果 $W$ 是对称矩阵 $A$ 的一个不变子空间（即对任意 $\mathbf{w} \in W$，都有 $A\mathbf{w} \in W$），那么它的正交补 $W^{\perp}$ 也是 $A$ 的一个[不变子空间](@entry_id:152829)。**

一个特别重要的例子是：如果 $\mathbf{v}$ 是 $A$ 的一个[特征向量](@entry_id:151813)，那么由 $\mathbf{v}$ 张成的[子空间](@entry_id:150286) $W=\text{span}\{\mathbf{v}\}$ 是一个不变子空间。因此，它的[正交补](@entry_id:149922) $W^{\perp}$（即所有与 $\mathbf{v}$ 正交的向量构成的集合）也必须是 $A$ 的一个[不变子空间](@entry_id:152829)。

证明如下：令 $\mathbf{w} \in W^{\perp}$，这意味着 $\mathbf{w}^T \mathbf{v} = 0$。我们需要证明 $A\mathbf{w}$ 也在 $W^{\perp}$ 中，即 $(A\mathbf{w})^T \mathbf{v} = 0$。利用 $A$ 的对称性：
$$
(A\mathbf{w})^T \mathbf{v} = \mathbf{w}^T A^T \mathbf{v} = \mathbf{w}^T A \mathbf{v}
$$
因为 $\mathbf{v}$ 是[特征向量](@entry_id:151813)，有 $A\mathbf{v} = \lambda\mathbf{v}$。代入上式：
$$
\mathbf{w}^T (\lambda \mathbf{v}) = \lambda (\mathbf{w}^T \mathbf{v}) = \lambda (0) = 0
$$
这证明了 $A\mathbf{w}$ 与 $\mathbf{v}$ 正交，即 $A\mathbf{w} \in W^{\perp}$ [@problem_id:1390316]。

这个性质保证了我们可以通过一个迭代过程找到完整的[正交基](@entry_id:264024)。我们首先找到一个[特征向量](@entry_id:151813) $\mathbf{u}_1$。然后，我们可以将注意力限制在与 $\mathbf{u}_1$ 正交的[子空间](@entry_id:150286)中，并在这个更低维度的空间里寻找下一个[特征向量](@entry_id:151813) $\mathbf{u}_2$。由于该[子空间](@entry_id:150286)是 $A$-不变的，我们保证能找到这样的向量。如此往复，直到构建出整个标准正交基。

### [谱分解](@entry_id:173707)：构造与诠释

结合以上性质，我们现在可以清晰地描述如何将一个[对称矩阵](@entry_id:143130) $A$ 分解。这个分解形式被称为**[谱分解](@entry_id:173707)**（Spectral Decomposition），它深刻地揭示了矩阵 $A$ 的作用方式。

假设 $A$ 是一个 $n \times n$ 的[实对称矩阵](@entry_id:192806)。根据我们已建立的性质，我们知道：
1.  $A$ 拥有 $n$ 个实[特征值](@entry_id:154894)（计入[重数](@entry_id:136466)），记为 $\lambda_1, \lambda_2, \dots, \lambda_n$。
2.  我们可以找到一个对应的[标准正交基](@entry_id:147779) $\{\mathbf{u}_1, \mathbf{u}_2, \dots, \mathbf{u}_n\}$，其中每个 $\mathbf{u}_i$ 都是 $A$ 的[特征向量](@entry_id:151813)，满足 $A\mathbf{u}_i = \lambda_i \mathbf{u}_i$。

现在，我们构建一个[正交矩阵](@entry_id:169220) $P$，其列向量就是这些标准[正交特征向量](@entry_id:155522)：
$$
P = \begin{pmatrix} |  & |   & | \\ \mathbf{u}_1  & \mathbf{u}_2  & \cdots  & \mathbf{u}_n \\ |  & |   & | \end{pmatrix}
$$
同时，构建一个对角矩阵 $D$，其对角线元素是对应的[特征值](@entry_id:154894)：
$$
D = \begin{pmatrix} \lambda_1  & 0  & \cdots  & 0 \\ 0  & \lambda_2  & \cdots  & 0 \\ \vdots  & \vdots  & \ddots  & \vdots \\ 0  & 0  & \cdots  & \lambda_n \end{pmatrix}
$$
根据矩阵乘法和[特征向量](@entry_id:151813)的定义，我们有：
$$
AP = A \begin{pmatrix} \mathbf{u}_1  & \cdots  & \mathbf{u}_n \end{pmatrix} = \begin{pmatrix} A\mathbf{u}_1  & \cdots  & A\mathbf{u}_n \end{pmatrix} = \begin{pmatrix} \lambda_1\mathbf{u}_1  & \cdots  & \lambda_n\mathbf{u}_n \end{pmatrix} = PD
$$
由于 $P$ 是[正交矩阵](@entry_id:169220)，有 $P^{-1} = P^T$，所以我们可以从右侧乘以 $P^T$ 得到：
$$
A = PDP^T
$$
这就是[谱定理](@entry_id:136620)的核心方程。但我们可以进一步将其展开，以获得更具启发性的形式。将 $P$ 写成列向量形式， $P^T$ 便是行向量形式：
$$
A = \begin{pmatrix} \mathbf{u}_1  & \cdots  & \mathbf{u}_n \end{pmatrix} \begin{pmatrix} \lambda_1   &  &  \\  & \ddots  &  \\   &  & \lambda_n \end{pmatrix} \begin{pmatrix} —  \mathbf{u}_1^T  — \\  \vdots  \\ —  \mathbf{u}_n^T  — \end{pmatrix}
= \sum_{i=1}^n \lambda_i \mathbf{u}_i \mathbf{u}_i^T
$$
这个和式就是谱分解。它告诉我们，**任何[对称矩阵](@entry_id:143130) $A$ 都可以表示为其[特征值](@entry_id:154894)加权的、指向其标准[正交特征向量](@entry_id:155522)方向的秩-1[投影矩阵](@entry_id:154479)之和**。

这里的每一项 $\mathbf{u}_i \mathbf{u}_i^T$ 都是一个**[投影矩阵](@entry_id:154479)**。它是一个 $n \times n$ 的矩阵，当它作用于任意向量 $\mathbf{x}$ 上时，结果是 $\mathbf{x}$ 在 $\mathbf{u}_i$ 方向上的投影，即 $(\mathbf{x} \cdot \mathbf{u}_i)\mathbf{u}_i$。因此，谱分解的几何意义是：一个[对称变换](@entry_id:144406) $A$ 对任意向量 $\mathbf{x}$ 的作用，可以分解为三步：
1.  将 $\mathbf{x}$ 分别投影到各个正交的特征方向 $\mathbf{u}_i$ 上。
2.  将每个投影分量沿其方向缩放相应的[特征值](@entry_id:154894) $\lambda_i$ 倍。
3.  将所有缩放后的分量相加。

这个分解在信号处理和机器学习中极其重要 [@problem_id:1390344]。例如，给定一个[对称矩阵](@entry_id:143130) $A = \begin{pmatrix} 5 & -2 \\ -2 & 8 \end{pmatrix}$ 和一组[正交特征向量](@entry_id:155522) $\mathbf{v}_1 = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$ 和 $\mathbf{v}_2 = \begin{pmatrix} -1 \\ 2 \end{pmatrix}$，我们可以将 $A$ 写成 $A = c_1 \mathbf{v}_1 \mathbf{v}_1^T + c_2 \mathbf{v}_2 \mathbf{v}_2^T$ 的形式。通过计算可以发现，系数 $c_i$ 与[特征值](@entry_id:154894) $\lambda_i$ 直接相关，具体关系为 $c_i = \lambda_i / \|\mathbf{v}_i\|^2$。

这些[投影矩阵](@entry_id:154479) $\mathbf{u}_i \mathbf{u}_i^T$ 还有一个美妙的性质，它们构成了一个“[单位分解](@entry_id:150115)”：
$$
I = \sum_{i=1}^n \mathbf{u}_i \mathbf{u}_i^T
$$
这表示单位矩阵可以被分解为到所有相互正交的一维特征空间上的投影之和。如果某个[特征值](@entry_id:154894) $\lambda_k$ 有重根，比如其[特征空间](@entry_id:638014) $E_k$ 是多维的，那么到这个[子空间](@entry_id:150286)的[投影矩阵](@entry_id:154479) $P_k$ 就是构成该[子空间](@entry_id:150286)的一组[标准正交基](@entry_id:147779)向量 $\{\mathbf{u}_{k_1}, \mathbf{u}_{k_2}, \dots\}$ 的投影之和：$P_k = \sum_j \mathbf{u}_{k_j} \mathbf{u}_{k_j}^T$ [@problem_id:1390312]。

### 瑞利商与[同时对角化](@entry_id:196036)

[谱定理](@entry_id:136620)还引申出一些高级但非常有用的概念，它们在数值计算和理论物理中扮演着重要角色。

#### 瑞利商

对于一个对称矩阵 $A$ 和一个非零向量 $\mathbf{x}$，**瑞利商**（Rayleigh Quotient）定义为：
$$
R_A(\mathbf{x}) = \frac{\mathbf{x}^T A \mathbf{x}}{\mathbf{x}^T \mathbf{x}}
$$
[瑞利商](@entry_id:137794)有一个极其重要的性质，即它的值总被 $A$ 的最小和最大[特征值](@entry_id:154894)所界定：
$$
\lambda_{\min} \le R_A(\mathbf{x}) \le \lambda_{\max}
$$
等号成立当且仅当 $\mathbf{x}$ 是对应于 $\lambda_{\min}$ 或 $\lambda_{\max}$ 的[特征向量](@entry_id:151813)。这个性质将一个复杂的求特征值问题（解高次多项式方程）转化为一个[优化问题](@entry_id:266749)（寻找[瑞利商](@entry_id:137794)的极值）。这在计算大型矩阵的[特征值](@entry_id:154894)时特别有用。

在主成分分析（PCA）等应用中，[瑞利商](@entry_id:137794)可以帮助我们识别数据的主要变化方向 [@problem_id:1390347]。例如，对于一个协方差矩阵 $C$，计算某个测试向量 $\mathbf{v}$ 的瑞利商 $R_C(\mathbf{v})$，其值会落在 $C$ 的[特征值](@entry_id:154894)谱范围内。如果计算出的值恰好等于一个已知的[特征值](@entry_id:154894)，那么这个测试向量 $\mathbf{v}$ 就是该[特征值](@entry_id:154894)对应的一个[特征向量](@entry_id:151813)。

#### [同时对角化](@entry_id:196036)

谱定理是关于单个矩阵的。一个自然的问题是：给定两个对称矩阵 $A$ 和 $B$，是否存在一个**共同的**正交矩阵 $P$，使得 $A$ 和 $B$都能被 $P$ 对角化？即 $A = P D_A P^T$ 且 $B = P D_B P^T$。如果可以，我们称 $A$ 和 $B$ 是**可同时[正交对角化](@entry_id:149411)**的。

这个问题的答案同样非常简洁：
**两个[实对称矩阵](@entry_id:192806) $A$ 和 $B$ 是可同时[正交对角化](@entry_id:149411)的，当且仅当它们是可交换的，即 $AB = BA$。**

这个定理在量子力学中具有基础性的意义。物理观测量由对称（厄米）算符表示，算符的[特征值](@entry_id:154894)是测量可能得到的结果，[特征向量](@entry_id:151813)是测量后系统所处的状态。如果两个算符（矩阵）可交换，它们就拥有一组共同的本征态（[特征向量](@entry_id:151813)）。这意味着对应的两个物理量可以被同时精确测量。

例如，给定两个[对称矩阵](@entry_id:143130) $A$ 和 $B$，其中一个矩阵含有未知参数，如 $B = \begin{pmatrix} 5 & 2 & -1 \\ 2 & \delta & 2 \\ -1 & 2 & 5 \end{pmatrix}$ [@problem_id:1390335]。要使 $A$ 和 $B$ 可[同时对角化](@entry_id:196036)，我们只需找到能使 $AB=BA$ 成立的 $\delta$ 值即可。通过计算矩阵乘积并令其相等，我们就能解出参数 $\delta$。这一条件确保了存在一个共同的[坐标系](@entry_id:156346)（由共享的[特征向量](@entry_id:151813)构成），在该[坐标系](@entry_id:156346)下，两个线性变换都表现为简单的缩放。

本章我们从[谱定理](@entry_id:136620)的核心论断出发，剖析了[对称矩阵](@entry_id:143130)的三个基本性质，并在此基础上构建了其[谱分解](@entry_id:173707)形式，最后探讨了瑞利商和[同时对角化](@entry_id:196036)等相关重要概念。这些原则和机理共同描绘了[对称矩阵](@entry_id:143130)在[线性空间](@entry_id:151108)中优美而简洁的几何行为。