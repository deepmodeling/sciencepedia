## 引言
在探索[线性变换](@entry_id:149133)及其在物理、工程与数据科学中的广泛应用时，[特征值与特征向量](@entry_id:748836)是两个居于核心地位的基石概念。一个[线性变换](@entry_id:149133)通常会改变向量的大小和方向，但对于任何变换，总存在一些特殊的“不变”方向。理解这些方向以及变换在这些方向上的作用，是揭示系统内在属性、预测其长期行为的关键。然而，从复杂的矩阵表示中直接提取这些信息往往是一项挑战，这正是[特征值分析](@entry_id:273168)所要解决的核心问题。

本文将系统地引导读者掌握[特征值与特征向量](@entry_id:748836)的理论与实践。第一部分“原理与机制”将深入探讨其定义、计算方法以及对称矩阵的[谱分解](@entry_id:173707)理论。第二部分“应用与交叉学科联系”将视野扩展至实际问题，展示特征分析如何在[连续介质力学](@entry_id:155125)、[振动分析](@entry_id:146266)、动力系统乃至数据科学中扮演关键角色。最后，“动手实践”部分将通过精心设计的练习，帮助读者将理论知识转化为解决实际问题的能力。

## 原理与机制

在对[线性变换](@entry_id:149133)及其在[张量分析](@entry_id:161423)中的应用的探索中，[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)的概念处于核心地位。它们揭示了变换固有的、不随[坐标系](@entry_id:156346)选择而改变的深刻属性。一个线性变换作用于一个向量时，通常会同时改变其大小和方向。然而，对于任何给定的线性变换，都存在一些特殊的非[零向量](@entry_id:156189)，当变换作用于它们时，其方向保持不变（或恰好反向），仅在长度上进行缩放。这些特殊的向量就是**[特征向量](@entry_id:151813)**（eigenvectors），而对应的缩放因子就是**[特征值](@entry_id:154894)**（eigenvalues）。

这个看似简单的代数关系 $A\mathbf{v} = \lambda\mathbf{v}$，是理解众多物理和工程现象的关键。其中，$A$ 是代表线性变换的方阵，$\mathbf{v}$ 是[特征向量](@entry_id:151813)，$\lambda$ 是对应的标量[特征值](@entry_id:154894)。[特征向量](@entry_id:151813)定义了变换作用下保持不变的“方向”或“轴线”，而[特征值](@entry_id:154894)则量化了在这些方向上的拉伸或压缩程度。例如，在三维空间中，一个刚体绕某根轴的旋转可以由一个旋转矩阵 $R$ 描述。对于沿[旋转轴](@entry_id:187094)方向的任意向量 $\mathbf{v}$，旋转对其没有影响，即 $R\mathbf{v} = \mathbf{v}$。这表明，[旋转轴](@entry_id:187094)本身就是[旋转矩阵](@entry_id:140302) $R$ 对应于[特征值](@entry_id:154894) $\lambda = 1$ 的[特征向量](@entry_id:151813)所张成的空间 [@problem_id:1509077]。同样，在[离散动力系统](@entry_id:154936) $x_{k+1} = A x_k$ 中，[特征向量](@entry_id:151813)代表了系统的“模态”——那些演化行为极其简单的初始状态，其方向在每一步迭代中都保持不变，仅被[特征值](@entry_id:154894)所缩放 [@problem_id:1509080]。

本章将系统地阐述[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)的基本原理、计算方法及其在[张量分析](@entry_id:161423)中的核心机制，特别是针对在物理科学中无处不在的对称张量。

### [特征方程](@entry_id:265849)：求解[特征值](@entry_id:154894)

寻找一个矩阵 $A$ 的[特征值与特征向量](@entry_id:748836)的第一步，是从其定义方程 $A\mathbf{v} = \lambda\mathbf{v}$ 出发。为了求解这个方程，我们将其改写为：
$$
A\mathbf{v} - \lambda\mathbf{v} = \mathbf{0}
$$
引入单位矩阵 $I$，我们可以将上式写成一个[齐次线性方程组](@entry_id:153432)：
$$
(A - \lambda I)\mathbf{v} = \mathbf{0}
$$
我们寻找的是非零的[特征向量](@entry_id:151813) $\mathbf{v}$。根据线性代数的基本定理，一个[齐次线性方程组](@entry_id:153432)拥有非零解的充分必要条件是其[系数矩阵](@entry_id:151473)为奇异矩阵，即该[矩阵的行列式](@entry_id:148198)为零。因此，我们得到求解[特征值](@entry_id:154894)的关键方程：
$$
\det(A - \lambda I) = 0
$$
这个方程被称为矩阵 $A$ 的**特征方程**（characteristic equation）。$\det(A - \lambda I)$ 是一个关于 $\lambda$ 的多项式，称为**[特征多项式](@entry_id:150909)**（characteristic polynomial）。[特征多项式的根](@entry_id:270910)就是矩阵 $A$ 的所有[特征值](@entry_id:154894)。

对于一个 $n \times n$ 的矩阵，[特征多项式](@entry_id:150909)是 $\lambda$ 的 $n$ 次多项式，因此根据[代数基本定理](@entry_id:152321)，它在[复数域](@entry_id:153768)内恰好有 $n$ 个根（计入[重数](@entry_id:136466)）。这意味着任何 $n \times n$ 矩阵都有 $n$ 个[特征值](@entry_id:154894)。

在某些特殊情况下，[特征值](@entry_id:154894)的计算异常简单。例如，考虑一个[对角矩阵](@entry_id:637782)。在[连续介质力学](@entry_id:155125)中，如果我们选择坐标轴与应变的[主轴](@entry_id:172691)对齐，[应变张量](@entry_id:193332)的[矩阵表示](@entry_id:146025)就呈[对角形式](@entry_id:264850)。对于这样的[对角矩阵](@entry_id:637782) [@problem_id:1509096]：
$$
\boldsymbol{\epsilon} = \begin{pmatrix}
\epsilon_{11} & 0 & 0 \\
0 & \epsilon_{22} & 0 \\
0 & 0 & \epsilon_{33}
\end{pmatrix}
$$
其特征方程为：
$$
\det(\boldsymbol{\epsilon} - \lambda \boldsymbol{I}) = \det\begin{pmatrix}
\epsilon_{11} - \lambda & 0 & 0 \\
0 & \epsilon_{22} - \lambda & 0 \\
0 & 0 & \epsilon_{33} - \lambda
\end{pmatrix} = (\epsilon_{11} - \lambda)(\epsilon_{22} - \lambda)(\epsilon_{33} - \lambda) = 0
$$
显而易见，[特征值](@entry_id:154894)就是矩阵对角线上的元素：$\lambda_1 = \epsilon_{11}$, $\lambda_2 = \epsilon_{22}$, $\lambda_3 = \epsilon_{33}$。这在物理上意味着[主应变](@entry_id:197797)就是[应变张量](@entry_id:193332)的[特征值](@entry_id:154894)。

特征多项式的系数也蕴含着关于矩阵的重要信息。对于一个 $n \times n$ 矩阵 $A$，其[特征多项式](@entry_id:150909) $p(\lambda) = \det(A - \lambda I)$ 可以写成 $p(\lambda) = (-1)^n \lambda^n + (-1)^{n-1} \operatorname{tr}(A) \lambda^{n-1} + \dots + \det(A)$。通过[韦达定理](@entry_id:150627)，我们可以建立[特征值](@entry_id:154894)与[矩阵不变量](@entry_id:195012)（如[迹和行列式](@entry_id:149685)）之间的关系：
*   **[特征值](@entry_id:154894)之和等于矩阵的迹**：$\sum_{i=1}^{n} \lambda_i = \operatorname{tr}(A) = \sum_{i=1}^{n} A_{ii}$
*   **[特征值](@entry_id:154894)之积等于[矩阵的行列式](@entry_id:148198)**：$\prod_{i=1}^{n} \lambda_i = \det(A)$

这些关系为验证[特征值计算](@entry_id:145559)的正确性提供了有力的工具，并且深化了我们对这些[矩阵不变量](@entry_id:195012)的理解 [@problem_id:1509127]。

### 特征空间：求解[特征向量](@entry_id:151813)

一旦通过求解[特征方程](@entry_id:265849)找到了一个[特征值](@entry_id:154894) $\lambda$，下一步就是找出所有与之对应的[特征向量](@entry_id:151813)。这些[特征向量](@entry_id:151813)是[齐次线性方程组](@entry_id:153432) $(A - \lambda I)\mathbf{v} = \mathbf{0}$ 的所有非零解。

所有对应于同一个[特征值](@entry_id:154894) $\lambda$ 的[特征向量](@entry_id:151813)，再加上零向量，构成一个[向量空间](@entry_id:151108)。这个空间是矩阵 $(A - \lambda I)$ 的**[零空间](@entry_id:171336)**（null space）或**核**（kernel），我们称之为对应于 $\lambda$ 的**特征空间**（eigenspace），记作 $E_\lambda$。因此，$E_\lambda = \ker(A - \lambda I)$。特征空间是一个[子空间](@entry_id:150286)，这意味着任何属于 $E_\lambda$ 的向量的[线性组合](@entry_id:154743)仍然属于 $E_\lambda$。要描述一个特征空间，我们通常需要找到它的一组基。

求解过程即为求解一个具体的[齐次线性方程组](@entry_id:153432)。例如，考虑矩阵 $A = \begin{pmatrix} 5 & -1 & 1 \\ 3 & 1 & -5 \\ 6 & -6 & 2 \end{pmatrix}$，已知其一个[特征值](@entry_id:154894)为 $\lambda = -4$ [@problem_id:1509080]。为了找到对应的特征空间 $E_{-4}$，我们求解 $(A - (-4)I)\mathbf{v} = (A+4I)\mathbf{v} = \mathbf{0}$：
$$
A+4I=\begin{pmatrix} 9 & -1 & 1 \\ 3 & 5 & -5 \\ 6 & -6 & 6 \end{pmatrix}
$$
令 $\mathbf{v} = (x, y, z)^T$，我们得到[方程组](@entry_id:193238)：
$$
\begin{cases}
9x-y+z=0 \\
3x+5y-5z=0 \\
6x-6y+6z=0
\end{cases}
$$
通过[高斯消元法](@entry_id:153590)或简单的代数代换，可以解得该[方程组](@entry_id:193238)的通解为 $t(0, 1, 1)^T$，其中 $t$ 是任意非零实数。因此，[特征空间](@entry_id:638014) $E_{-4}$ 是由向量 $\begin{pmatrix} 0 \\ 1 \\ 1 \end{pmatrix}$ 张成的一维[子空间](@entry_id:150286)，这个向量就是 $E_{-4}$ 的一个基。

与[特征值](@entry_id:154894)相关的两个重要概念是**[代数重数](@entry_id:154240)**（algebraic multiplicity）和**[几何重数](@entry_id:155584)**（geometric multiplicity）。
*   **[代数重数](@entry_id:154240)**是[特征值](@entry_id:154894) $\lambda$ 作为特征多项式[根的重数](@entry_id:635479)。
*   **[几何重数](@entry_id:155584)**是对应[特征空间](@entry_id:638014) $E_\lambda$ 的维数，即 $\dim(E_\lambda)$。它表示[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)的最大数量。

根据线性代数的理论，一个[特征值](@entry_id:154894)的[几何重数](@entry_id:155584)总是小于或等于其[代数重数](@entry_id:154240)。我们可以通过计算矩阵 $A-\lambda I$ 的秩来确定[几何重数](@entry_id:155584)。根据秩-零度定理，$\dim(E_\lambda) = \dim(\ker(A - \lambda I)) = n - \operatorname{rank}(A - \lambda I)$，其中 $n$ 是矩阵的维数。

例如，对于矩阵 $S = \begin{pmatrix} 2 & 2 & -1 \\ 2 & 5 & -2 \\ -1 & -2 & 2 \end{pmatrix}$ 和[特征值](@entry_id:154894) $\lambda=1$ [@problem_id:1509103]，我们计算 $S-I$：
$$
S-I=\begin{pmatrix} 1 & 2 & -1 \\ 2 & 4 & -2 \\ -1 & -2 & 1 \end{pmatrix}
$$
观察可知，第二行是第一行的 2 倍，第三行是第一行的 -1 倍。这意味着该矩阵的秩为 1。因此，$\lambda=1$ 的[几何重数](@entry_id:155584)为 $\dim(E_1) = 3 - \operatorname{rank}(S - I) = 3 - 1 = 2$。这意味着存在两个[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)都对应于[特征值](@entry_id:154894) $\lambda=1$。

### 对称性的角色：[对称矩阵](@entry_id:143130)的特征属性

在物理和工程领域，我们遇到的大多数张量（如应力张量、[应变张量](@entry_id:193332)、惯性张量）都是对称的。在[矩阵表示](@entry_id:146025)中，这意味着矩阵等于其转置，即 $A = A^T$。[对称矩阵](@entry_id:143130)拥有一系列优美而强大的性质，这使得它们的特征分析尤为重要和简洁。

最重要的两个性质是：
1.  **实数[特征值](@entry_id:154894)**：一个[实对称矩阵](@entry_id:192806)的所有[特征值](@entry_id:154894)都是实数。这保证了在物理世界中，诸如主应力、[主应变](@entry_id:197797)、转动惯量等量总是实数，这与我们的物理直觉相符。
2.  **[正交特征向量](@entry_id:155522)**：对应于**不同**[特征值](@entry_id:154894)的[特征向量](@entry_id:151813)是相互正交的。

我们可以证明第二条性质。假设 $\lambda_1$ 和 $\lambda_2$ 是对称矩阵 $A$ 的两个不同[特征值](@entry_id:154894)（$\lambda_1 \neq \lambda_2$），对应的[特征向量](@entry_id:151813)分别为 $\mathbf{v}_1$ 和 $\mathbf{v}_2$。我们有：
$$
A\mathbf{v}_1 = \lambda_1 \mathbf{v}_1 \quad \text{和} \quad A\mathbf{v}_2 = \lambda_2 \mathbf{v}_2
$$
考虑[标量积](@entry_id:138996) $(\lambda_1 \mathbf{v}_1) \cdot \mathbf{v}_2$。利用矩阵乘积与[点积](@entry_id:149019)的关系 $(A\mathbf{x}) \cdot \mathbf{y} = \mathbf{x} \cdot (A^T \mathbf{y})$，我们得到：
$$
\lambda_1 (\mathbf{v}_1 \cdot \mathbf{v}_2) = (A\mathbf{v}_1) \cdot \mathbf{v}_2 = \mathbf{v}_1 \cdot (A^T \mathbf{v}_2)
$$
由于 $A$ 是对称的（$A^T=A$），上式变为：
$$
\lambda_1 (\mathbf{v}_1 \cdot \mathbf{v}_2) = \mathbf{v}_1 \cdot (A\mathbf{v}_2) = \mathbf{v}_1 \cdot (\lambda_2 \mathbf{v}_2) = \lambda_2 (\mathbf{v}_1 \cdot \mathbf{v}_2)
$$
整理后得到：
$$
(\lambda_1 - \lambda_2)(\mathbf{v}_1 \cdot \mathbf{v}_2) = 0
$$
因为我们假设了 $\lambda_1 \neq \lambda_2$，所以必然有 $\mathbf{v}_1 \cdot \mathbf{v}_2 = 0$。这证明了[特征向量](@entry_id:151813)是正交的 [@problem_id:1509104]。

这一正交性具有深刻的物理意义。它意味着[对称张量](@entry_id:148092)的[特征向量](@entry_id:151813)构成了一组正交的**[主轴](@entry_id:172691)**（principal axes）。在这些[主轴](@entry_id:172691)方向上，张量所描述的物理效应是“纯粹”的。例如，对于应变张量，主轴方向是纯拉伸或压缩而没有剪切应变的方向 [@problem_id:1509089]。通过找到这些主轴（即[特征向量](@entry_id:151813)），我们可以极大地简化对物理系统状态的描述和分析。

### 对角化与谱分解

[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)的一个核心应用是**[矩阵对角化](@entry_id:138930)**（matrix diagonalization）。如果一个 $n \times n$ 矩阵 $A$ 有 $n$ 个[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)（这在[几何重数](@entry_id:155584)等于[代数重数](@entry_id:154240)时成立），我们就可以将其对角化。具体来说，我们可以找到一个可逆矩阵 $P$ 和一个对角矩阵 $D$，使得：
$$
A = PDP^{-1}
$$
其中，$D$ 是一个对角线上元素为 $A$ 的[特征值](@entry_id:154894) $\lambda_1, \lambda_2, \dots, \lambda_n$ 的[对角矩阵](@entry_id:637782)，而 $P$ 的列向量是与这些[特征值](@entry_id:154894)[一一对应](@entry_id:143935)的[特征向量](@entry_id:151813)。

这个分解非常有用。例如，计算矩阵的高次幂变得非常简单：$A^k = (PDP^{-1})^k = PD(P^{-1}P)D(P^{-1}\dots)DP^{-1} = PD^kP^{-1}$。计算对角矩阵的幂次只需将其对角线元素取幂即可。

让我们通过一个例子来构造这个分解 [@problem_id:1509121]。考虑矩阵 $A = \begin{pmatrix} 5 & -2 \\ -2 & 2 \end{pmatrix}$。
1.  **求[特征值](@entry_id:154894)**：$\det(A-\lambda I) = (5-\lambda)(2-\lambda)-4 = \lambda^2 - 7\lambda + 6 = (\lambda-6)(\lambda-1)=0$。[特征值](@entry_id:154894)为 $\lambda_1=6, \lambda_2=1$。
2.  **求[特征向量](@entry_id:151813)**：
    *   对于 $\lambda_1=6$，解 $(A-6I)\mathbf{v}=0$ 得 $\begin{pmatrix} -1 & -2 \\ -2 & -4 \end{pmatrix}\mathbf{v}=0$，[特征向量](@entry_id:151813)可取 $\mathbf{v}_1 = \begin{pmatrix} 2 \\ -1 \end{pmatrix}$。
    *   对于 $\lambda_2=1$，解 $(A-I)\mathbf{v}=0$ 得 $\begin{pmatrix} 4 & -2 \\ -2 & 1 \end{pmatrix}\mathbf{v}=0$，[特征向量](@entry_id:151813)可取 $\mathbf{v}_2 = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$。
3.  **构造 P 和 D**：将[特征值](@entry_id:154894)按降序[排列](@entry_id:136432)在 $D$ 的对角线上，并将对应的[特征向量](@entry_id:151813)作为 $P$ 的列。
    $$
    D = \begin{pmatrix} 6 & 0 \\ 0 & 1 \end{pmatrix}, \quad P = \begin{pmatrix} 2 & 1 \\ -1 & 2 \end{pmatrix}
    $$

对于[对称矩阵](@entry_id:143130)，[对角化](@entry_id:147016)过程更加优美。由于我们总能找到一组 $n$ 个相互正交的[特征向量](@entry_id:151813)，我们可以将它们归一化，构成一个**[正交矩阵](@entry_id:169220)** $Q$（满足 $Q^T Q = I$，即 $Q^{-1} = Q^T$）。这样，[对角化公式](@entry_id:204557)就变成了：
$$
A = QDQ^T
$$
这就是著名的**谱定理**（Spectral Theorem）。它表明任何[对称矩阵](@entry_id:143130)都可以通过一个旋转（由 $Q^T$ 代表）变换到一个纯粹拉伸/压缩（由 $D$ 代表）的状态，然后再旋转回去（由 $Q$ 代表）。

[谱定理](@entry_id:136620)还可以写成一种极其深刻的形式，称为**谱分解**（spectral decomposition）或**主轴分解**（principal axis decomposition）。如果 $Q$ 的列是标准[正交特征向量](@entry_id:155522) $\mathbf{n}_1, \dots, \mathbf{n}_n$，则：
$$
A = \sum_{i=1}^{n} \lambda_i (\mathbf{n}_i \otimes \mathbf{n}_i)
$$
这里，$\mathbf{n}_i \otimes \mathbf{n}_i$ （在[矩阵表示](@entry_id:146025)中为 $\mathbf{n}_i \mathbf{n}_i^T$）是一个**投影算子**，它将任意[向量投影](@entry_id:147046)到由 $\mathbf{n}_i$ 定义的主轴方向上。因此，谱分解的物理图像是：对称张量 $A$ 的作用，等价于将一个向量分别投影到各个正交的主轴上，然后将每个投影分量按其对应的[特征值](@entry_id:154894)进行缩放，最后将所有结果向量相加。

这个分解形式在理论分析中非常强大。例如，考虑一个由应力张量 $\sigma$ 的[主方向](@entry_id:276187) $\mathbf{n}_i$ 构成的“权重张量” $W = \sum_i \alpha_i (\mathbf{n}_i \otimes \mathbf{n}_i)$。要计算 $D = \operatorname{Tr}(W\sigma)$ [@problem_id:1509083]，我们可以利用谱分解和[张量积](@entry_id:140694)的性质。由于 $\sigma = \sum_j \lambda_j (\mathbf{n}_j \otimes \mathbf{n}_j)$ 且主方向是标准正交的（即 $\mathbf{n}_i \cdot \mathbf{n}_j = \delta_{ij}$），我们有：
$$
W\sigma = \left( \sum_{i} \alpha_i (\mathbf{n}_i \otimes \mathbf{n}_i) \right) \left( \sum_{j} \lambda_j (\mathbf{n}_j \otimes \mathbf{n}_j) \right) = \sum_{i} \alpha_i \lambda_i (\mathbf{n}_i \otimes \mathbf{n}_i)
$$
取其迹，并利用 $\operatorname{Tr}(\mathbf{n}_i \otimes \mathbf{n}_i) = \mathbf{n}_i \cdot \mathbf{n}_i = 1$，得到：
$$
D = \operatorname{Tr}(W\sigma) = \sum_{i=1}^{n} \alpha_i \lambda_i
$$
这个简洁的结果表明，最终的标量 $D$ 是[主应力](@entry_id:176761)（[特征值](@entry_id:154894)）的一个加权和，而无需显式计算[特征向量](@entry_id:151813)。这充分展示了谱分解的威力。

### 超越实数[特征值](@entry_id:154894)：[复特征值](@entry_id:156384)的情形

虽然[对称矩阵的特征值](@entry_id:152966)总是实数，但一般非对称的实矩阵可能拥有复数[特征值](@entry_id:154894)。当[特征方程](@entry_id:265849)的根为复数时会发生什么？

对于实矩阵 $A$，如果 $\lambda = \alpha + i\beta$（其中 $\beta \neq 0$）是一个[特征值](@entry_id:154894)，其对应的[特征向量](@entry_id:151813) $\mathbf{w}$ 也必然是[复向量](@entry_id:192851)。由于矩阵 $A$ 的元素都是实数，[特征值](@entry_id:154894)的共轭 $\bar{\lambda} = \alpha - i\beta$ 也必然是 $A$ 的一个[特征值](@entry_id:154894)，且其对应的[特征向量](@entry_id:151813)是 $\bar{\mathbf{w}}$。

一个复数[特征值](@entry_id:154894)意味着在实数空间 $\mathbb{R}^n$ 中不存在任何一个方向能在变换 $A$ 的作用下保持不变。那么，它的几何意义是什么呢？答案是**旋转与缩放的复合**。

考虑一个二维平面上的变换 $A$，它有一对[共轭复特征值](@entry_id:152797) $\lambda = \alpha \pm i\beta$ [@problem_id:1509073]。令对应于 $\lambda = \alpha + i\beta$ 的[复特征向量](@entry_id:155846)为 $\mathbf{w} = \mathbf{u} + i\mathbf{v}$，其中 $\mathbf{u}$ 和 $\mathbf{v}$ 是 $\mathbb{R}^2$ 中的实向量。将它们代入特征方程 $A\mathbf{w} = \lambda\mathbf{w}$ 并分离实部和虚部，我们得到：
$$
A\mathbf{u} = \alpha\mathbf{u} - \beta\mathbf{v}
$$
$$
A\mathbf{v} = \beta\mathbf{u} + \alpha\mathbf{v}
$$
向量 $\mathbf{u}$ 和 $\mathbf{v}$ 是线性无关的，它们构成 $\mathbb{R}^2$ 的一个基。在这组基 $\{\mathbf{u}, \mathbf{v}\}$ 下，线性变换 $A$ 的矩阵表示 $C$ 为：
$$
C = \begin{pmatrix} \alpha & \beta \\ -\beta & \alpha \end{pmatrix}
$$
这个矩阵可以被分解为一个[缩放矩阵](@entry_id:188350)和一个[旋转矩阵](@entry_id:140302)的乘积。令 $r = |\lambda| = \sqrt{\alpha^2 + \beta^2}$，并定义角度 $\theta$ 使得 $\cos\theta = \alpha/r$ 和 $\sin\theta = \beta/r$。那么：
$$
C = r \begin{pmatrix} \alpha/r & \beta/r \\ -\beta/r & \alpha/r \end{pmatrix} = r \begin{pmatrix} \cos\theta & \sin\theta \\ -\sin\theta & \cos\theta \end{pmatrix}
$$
这清楚地表明，在 $\{\mathbf{u}, \mathbf{v}\}$ 基所定义的[坐标系](@entry_id:156346)中，变换 $A$ 的作用是先进行一个角度为 $\theta$ 的旋转，然后再进行一个因子为 $r = |\lambda|$ 的缩放。

因此，当我们将变换 $A$ 反复作用于一个初始向量 $\mathbf{v}_0$ 时，所生成的点序列 $\mathbf{v}_k = A^k \mathbf{v}_0$ 的轨迹将是一条螺线。
*   如果 $|\lambda| > 1$，点将沿着一条向外发散的螺线运动。
*   如果 $|\lambda|  1$，点将沿着一条向内收敛的螺线运动，趋向于原点。
*   如果 $|\lambda| = 1$，缩放因子为 1，点将沿着一个固定的椭圆（在标准[坐标系](@entry_id:156346)下）运动。

总之，实数[特征值](@entry_id:154894)对应于沿特定方向的纯粹拉伸或压缩，而复数[特征值](@entry_id:154894)则对应于在某个二维[子空间](@entry_id:150286)内的[旋转和缩放](@entry_id:154036)的组合。这一认识完善了我们对线性变换几何行为的整体理解。