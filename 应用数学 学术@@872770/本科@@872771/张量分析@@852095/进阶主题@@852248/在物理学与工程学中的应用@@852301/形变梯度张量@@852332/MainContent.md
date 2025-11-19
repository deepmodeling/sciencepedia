## 引言
在探索物质世界如何响应外力而改变形状时，连续介质力学提供了一套强大的理论框架。无论是桥梁的承重、橡胶的拉伸，还是生物组织的生长，其核心都在于如何精确地描述和量化材料的变形。然而，变形过程往往是复杂的，涉及拉伸、压缩、剪切和旋转的组合，这为建立普适的力学模型带来了挑战。变形梯度张量正是为了解决这一核心问题而引入的根本性数学工具。

本篇文章将带您深入理解变形梯度张量这一核心概念。您将学习到：

*   在“原理与机制”一章中，我们将从第一性原理出发，定义变形梯度张量，阐释其如何捕捉局部变形的几何信息，并介绍极分解、应变张量等关键衍生概念。
*   在“应用与跨学科联系”一章中，我们将展示变形梯度张量如何作为一种通用语言，应用于固体力学、[流体力学](@entry_id:136788)、[材料科学](@entry_id:152226)和生物力学等多个领域，将抽象理论与实际问题联系起来。
*   最后，在“动手实践”部分，您将通过具体的计算练习，巩固对变形梯度张量及其应用的掌握。

通过这三个章节的学习，您将能够构建起一个关于[材料变形](@entry_id:169356)的完整知识体系，为后续学习更高级的本构理论和计算力学打下坚实的基础。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，理解物体的变形是描述其力学行为的核心。变形梯度张量是量化这种变形的根本工具。本章将系统地阐述变形梯度张量的定义、物理解释、数学性质及其在应变分析中的核心作用。

### 变形梯度张量的定义

想象一个连续体，它在初始时刻占据空间中的一个区域，我们称之为**参考构型**（reference configuration）。物体中的每个物质点在参考构型中的位置可以用位置向量 $\mathbf{X}$ 表示。当物体受力变形后，它会移动到一个新的空间区域，我们称之为**当前构型**（current configuration）。同一个物质点在当前构型中的位置则由位置向量 $\mathbf{x}$ 描述。

因此，变形过程可以被数学地描述为一个从参考构型到当前构型的映射关系：$\mathbf{x} = \boldsymbol{\chi}(\mathbf{X})$。这个函数 $\boldsymbol{\chi}$ 包含了物体如何从其初始状态移动到最终状态的全部信息。

**变形梯度张量**（deformation gradient tensor），记作 $\mathbf{F}$，是这个映射函数 $\boldsymbol{\chi}$ 相对于参考构型坐标 $\mathbf{X}$ 的梯度。在笛卡尔坐标系中，其分量形式定义为：

$$
F_{ij} = \frac{\partial x_i}{\partial X_j}
$$

这里，$x_i$ 是当前构型中的坐标分量，$X_j$ 是参考构型中的坐标分量。$\mathbf{F}$ 是一个二阶张量，它捕捉了在物[质点](@entry_id:186768) $\mathbf{X}$ 附近，变形是如何发生的。

变形梯度张量的一个关键作用是，它将参考构型中的一个无穷小向量 $d\mathbf{X}$ 线性地映射到当前构型中的对应向量 $d\mathbf{x}$：

$$
d\mathbf{x} = \mathbf{F} d\mathbf{X}
$$

这表明 $\mathbf{F}$ 描述了材料线的局部拉伸和旋转。

为了具体理解，我们来看一个例子。考虑一个均匀变形，其映射函数为：
$x_1 = (2 - \alpha)X_1 + \beta X_2$
$x_2 = \beta X_1 + (2 + \alpha)X_2$
$x_3 = \gamma X_3$

其中 $\alpha, \beta, \gamma$ 是表征变形的无量纲常数。根据定义，我们可以计算出 $\mathbf{F}$ 的各个分量 [@problem_id:1547241]：

$$
\mathbf{F} = \begin{pmatrix}
\frac{\partial x_1}{\partial X_1} & \frac{\partial x_1}{\partial X_2} & \frac{\partial x_1}{\partial X_3} \\
\frac{\partial x_2}{\partial X_1} & \frac{\partial x_2}{\partial X_2} & \frac{\partial x_2}{\partial X_3} \\
\frac{\partial x_3}{\partial X_1} & \frac{\partial x_3}{\partial X_2} & \frac{\partial x_3}{\partial X_3}
\end{pmatrix}
=
\begin{pmatrix}
2-\alpha & \beta & 0 \\
\beta & 2+\alpha & 0 \\
0 & 0 & \gamma
\end{pmatrix}
$$

在这个例子中，因为映射函数是 $\mathbf{X}$ 的线性函数，所以计算出的 $\mathbf{F}$ 是一个常数矩阵，它不随物[质点](@entry_id:186768)的位置 $\mathbf{X}$ 而改变。这种变形被称为**均匀变形**（homogeneous deformation）。

然而，并非所有变形都是均匀的。如果 $\mathbf{F}$ 的值依赖于物[质点](@entry_id:186768)在参考构型中的位置 $\mathbf{X}$，那么这种变形就被称为**非均匀变形**（inhomogeneous deformation）。例如，考虑以下映射 [@problem_id:1547242]：

$$
x_1 = \alpha X_1 + \beta X_2 \\
x_2 = -\beta X_1 + \alpha X_2 \\
x_3 = X_3 + \gamma X_1 X_2
$$

这里的 $x_3$ 包含了 $X_1$ 和 $X_2$ 的乘积项，这是一个[非线性](@entry_id:637147)项。我们来计算 $\mathbf{F}$ 的一个分量，$F_{32}$：

$$
F_{32} = \frac{\partial x_3}{\partial X_2} = \frac{\partial}{\partial X_2}(X_3 + \gamma X_1 X_2) = \gamma X_1
$$

由于 $F_{32}$ 的值依赖于坐标 $X_1$，所以变形梯度张量 $\mathbf{F}$ 在物体的不同点是不同的。因此，这是一个非均匀变形。

### 变形梯度的物理解释

变形梯度张量 $\mathbf{F}$ 不仅仅是一个数学构造，它的不同数学属性直接对应着清晰的物理意义。

#### 体积变化

$\mathbf{F}$ 的[行列式](@entry_id:142978)，通常记为 $J = \det(\mathbf{F})$，具有重要的物理解释。它描述了变形过程中材料微元的局部体积变化率。一个在参考构型中体积为 $dV_0$ 的微元，在变形后其体积 $dV$ 为：

$$
dV = J dV_0
$$

因此，$J$ 是当前构型体积与参考构型体积之比。物理上，物质不能被压缩到零体积或负体积，所以必须始终满足 $J \gt 0$。如果在一个变形过程中 $J=1$，则称该变形为**[等容变形](@entry_id:196451)**（isochoric deformation），意味着物体的[体积保持](@entry_id:141001)不变。

例如，对于一个由以下映射描述的均匀变形 [@problem_id:1547239]：
$x_1 = \alpha X_1 + \beta X_2$
$x_2 = \gamma X_2 - \delta X_3$
$x_3 = \epsilon X_3$

其变形梯度张量为一个[上三角矩阵](@entry_id:150931)：

$$
\mathbf{F} = \begin{pmatrix}
\alpha & \beta & 0 \\
0 & \gamma & -\delta \\
0 & 0 & \epsilon
\end{pmatrix}
$$

其[行列式](@entry_id:142978)就是对角元素的乘积，$J = \det(\mathbf{F}) = \alpha \gamma \epsilon$。如果给定常数值 $\alpha = 1.50, \gamma = 1.10, \epsilon = 0.80$，则体积比为 $J = 1.50 \times 1.10 \times 0.80 = 1.32$。这意味着该变形使材料的局部[体积膨胀](@entry_id:144241)到其初始体积的1.32倍。

#### 描述拉伸、剪切与旋转

$\mathbf{F}$ 的分量直接与材料的局部几何变化相关。其对角分量（如 $F_{11}, F_{22}$）主要与沿坐标轴方向的**拉伸**（stretch）有关，而非对角分量（如 $F_{12}, F_{21}$）则与不同方向之间的**剪切**（shear）有关。

一个典型的例子是**简单剪切**（simple shear）。考虑以下变形 [@problem_id:1547277]：

$$
x_1 = X_1 \\
x_2 = X_2 + \gamma X_3 \\
x_3 = X_3
$$

我们可以通过位移场 $\mathbf{u} = \mathbf{x} - \mathbf{X}$ 来直观理解这个变形。位移分量为 $u_1=0$, $u_2=\gamma X_3$, $u_3=0$。这表明，所有初始位于 $X_3 = \text{常数}$ 平面上的物[质点](@entry_id:186768)，在变形后都沿 $x_2$ 方向平移了相同的距离 $\gamma X_3$。离 $X_3=0$ 平面越远，平移的距离越大，就像一叠扑克牌的滑动。

该变形的变形梯度张量为：

$$
\mathbf{F} = \begin{pmatrix}
1 & 0 & 0 \\
0 & 1 & \gamma \\
0 & 0 & 1
\end{pmatrix}
$$

这里的非对角项 $F_{23} = \gamma$ 精确地量化了这种剪切效应。值得注意的是，$\det(\mathbf{F}) = 1$，说明简单剪切是一种[等容变形](@entry_id:196451)。

### 变形梯度的性质与运算

变形梯度张量作为一个数学对象，遵循[张量代数](@entry_id:161671)的一系列运算法则，这些运算在[连续介质力学](@entry_id:155125)中具有明确的物理对应。

#### 逆变形梯度

既然 $\mathbf{F}$ 将参考构型映射到当前构型，那么只要变形是可逆的（即 $J \gt 0$），就必然存在一个**逆映射** $\mathbf{X} = \boldsymbol{\chi}^{-1}(\mathbf{x})$，它将当前构型中的点映射回其在参考构型中的原始位置。这个逆映射的梯度被称为**[逆变](@entry_id:192290)形梯度张量**（inverse deformation gradient tensor），记为 $\mathbf{F}^{-1}$：

$$
(\mathbf{F}^{-1})_{ij} = \frac{\partial X_i}{\partial x_j}
$$

从数学上看，$\mathbf{F}^{-1}$ 就是 $\mathbf{F}$ 的矩阵逆。例如，对于一个非均匀变形 [@problem_id:1547269]：
$x_1 = X_1 + \alpha X_2$
$x_2 = X_2 + \beta X_1^{2}$
$x_3 = \gamma X_3$

其变形梯度张量为：

$$
\mathbf{F} = \begin{pmatrix}
1 & \alpha & 0 \\
2\beta X_{1} & 1 & 0 \\
0 & 0 & \gamma
\end{pmatrix}
$$

只要 $\det(\mathbf{F}) = \gamma(1 - 2\alpha\beta X_1) \neq 0$，我们就可以求出其逆矩阵：

$$
\mathbf{F}^{-1} = \begin{pmatrix}
\frac{1}{1-2\alpha\beta X_{1}} & -\frac{\alpha}{1-2\alpha\beta X_{1}} & 0 \\
-\frac{2\beta X_{1}}{1-2\alpha\beta X_{1}} & \frac{1}{1-2\alpha\beta X_{1}} & 0 \\
0 & 0 & \frac{1}{\gamma}
\end{pmatrix}
$$

#### 复合变形

当一个物体经历一系列连续的变形时，总的变形梯度可以通过链式法则得到。假设物体首先经历变形 $\boldsymbol{\chi}_1$，从参考构型 $\mathbf{X}$ 到[中间构型](@entry_id:193000) $\mathbf{x}'$，其变形梯度为 $\mathbf{F}_1$。接着，它再经历变形 $\boldsymbol{\chi}_2$，从[中间构型](@entry_id:193000) $\mathbf{x}'$ 到最终构型 $\mathbf{x}$，其变形梯度为 $\mathbf{F}_2$。

那么，从初始构型 $\mathbf{X}$ 到最终构型 $\mathbf{x}$ 的总变形梯度 $\mathbf{F}$ 是这两个变形梯度的乘积：

$$
\mathbf{F} = \mathbf{F}_2 \mathbf{F}_1
$$

注意，矩阵乘法不满足[交换律](@entry_id:141214)，因此变形的顺序至关重要。先发生的变形对应的张量（$\mathbf{F}_1$）在右边。

考虑一个先进行简单剪切，再进行[单轴拉伸](@entry_id:188287)的例子 [@problem_id:1547274]。
1.  简单剪切：$x'_1 = X_1 + kX_2, x'_2 = X_2, x'_3 = X_3$。其变形梯度为 $\mathbf{F}_1 = \begin{pmatrix} 1 & k & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}$。
2.  [单轴拉伸](@entry_id:188287)：$x_1 = x'_1, x_2 = \lambda x'_2, x_3 = x'_3$。其变形梯度为 $\mathbf{F}_2 = \begin{pmatrix} 1 & 0 & 0 \\ 0 & \lambda & 0 \\ 0 & 0 & 1 \end{pmatrix}$。

总的变形梯度为：

$$
\mathbf{F} = \mathbf{F}_2 \mathbf{F}_1 = \begin{pmatrix} 1 & 0 & 0 \\ 0 & \lambda & 0 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & k & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} = \begin{pmatrix} 1 & k & 0 \\ 0 & \lambda & 0 \\ 0 & 0 & 1 \end{pmatrix}
$$

### 从变形梯度到应变张量

变形梯度 $\mathbf{F}$ 本身包含了材料的拉伸（变形）和刚体旋转信息。在[材料科学](@entry_id:152226)和[固体力学](@entry_id:164042)中，我们通常更关心那些能够引起[内力](@entry_id:167605)（应力）的纯粹的形状和尺寸变化，即**应变**（strain）。因此，需要从 $\mathbf{F}$ 中提取出不包含刚体旋转的量。

#### 右柯西-格林变形张量

**右柯西-格林变形张量**（Right Cauchy-Green deformation tensor），记作 $\mathbf{C}$，是定义应变的一个核心工具。它被定义为：

$$
\mathbf{C} = \mathbf{F}^T \mathbf{F}
$$

其中 $\mathbf{F}^T$ 是 $\mathbf{F}$ 的转置。$\mathbf{C}$ 是一个[对称张量](@entry_id:148092)。它的物理意义在于测量材料纤维长度的平方变化。考虑参考构型中的一个微元向量 $d\mathbf{X}$，其长度的平方为 $dS^2 = d\mathbf{X} \cdot d\mathbf{X}$。变形后，该向量变为 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$，其长度的平方为 $ds^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F} d\mathbf{X})^T (\mathbf{F} d\mathbf{X}) = d\mathbf{X}^T \mathbf{F}^T \mathbf{F} d\mathbf{X} = d\mathbf{X}^T \mathbf{C} d\mathbf{X}$。

可见，$\mathbf{C}$ 完全描述了所有方向上材料纤维长度的平方是如何变化的。如果变形只是一个刚体旋转，$\mathbf{F}$ 就是一个[旋转张量](@entry_id:191990) $\mathbf{R}$，此时 $\mathbf{C} = \mathbf{R}^T \mathbf{R} = \mathbf{I}$（单位张量），说明没有长度变化。因此，$\mathbf{C}$ 天然地滤除了刚体旋转的影响。

对于前面提到的简单[剪切变形](@entry_id:170920) [@problem_id:1547222]，我们有 $\mathbf{F} = \begin{pmatrix} 1 & \gamma & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}$。其对应的[右柯西-格林张量](@entry_id:174156)为：

$$
\mathbf{C} = \mathbf{F}^T \mathbf{F} = \begin{pmatrix} 1 & 0 & 0 \\ \gamma & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & \gamma & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} = \begin{pmatrix} 1 & \gamma & 0 \\ \gamma & 1+\gamma^2 & 0 \\ 0 & 0 & 1 \end{pmatrix}
$$

#### [格林-拉格朗日应变张量](@entry_id:187745)

从 $\mathbf{C}$ 出发，我们可以定义一个直接度量应变的张量。**[格林-拉格朗日应变张量](@entry_id:187745)**（Green-Lagrange strain tensor），记作 $\mathbf{E}$，定义为：

$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^T \mathbf{F} - \mathbf{I})
$$

这个张量直接量化了长度平方的改变量。具体来说，$ds^2 - dS^2 = 2 d\mathbf{X}^T \mathbf{E} d\mathbf{X}$。如果没有任何变形（$\mathbf{F}=\mathbf{I}$），则 $\mathbf{E}=\mathbf{0}$。重要的是，对于任何刚体旋转，$\mathbf{E}$ 也为零，因此它是一个纯粹的[应变度量](@entry_id:755495)。

让我们计算一个具体例子中的应变分量 [@problem_id:1547291]。考虑映射：
$x_1 = (1+\alpha) X_1$
$x_2 = X_2 + \beta X_1$
$x_3 = X_3$

首先计算 $\mathbf{F}$：

$$
\mathbf{F} = \begin{pmatrix} 1+\alpha & 0 & 0 \\ \beta & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}
$$

然后计算 $\mathbf{C}=\mathbf{F}^T\mathbf{F}$：

$$
\mathbf{C} = \begin{pmatrix} 1+\alpha & \beta & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 1+\alpha & 0 & 0 \\ \beta & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} = \begin{pmatrix} (1+\alpha)^2 + \beta^2 & \beta & 0 \\ \beta & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}
$$

最后，计算[格林-拉格朗日应变张量](@entry_id:187745)的 $E_{11}$ 分量：

$$
E_{11} = \frac{1}{2}(C_{11} - 1) = \frac{1}{2}((1+\alpha)^2 + \beta^2 - 1) = \frac{1}{2}(1 + 2\alpha + \alpha^2 + \beta^2 - 1) = \alpha + \frac{\alpha^2 + \beta^2}{2}
$$

这个结果显示了 $\mathbf{E}$ 如何捕捉由拉伸（$\alpha$）和剪切（$\beta$）共同贡献的[非线性](@entry_id:637147)应变效应。

### 极分解：旋转与拉伸的分离

虽然 $\mathbf{C}$ 和 $\mathbf{E}$ 成功地滤除了旋转，但它们本身并没有显式地告诉我们变形中的旋转部分是什么。**极分解**（Polar Decomposition）定理提供了一个优雅的解决方案，它能将任何可逆的变形梯度 $\mathbf{F}$ 分解为一个纯旋转和一个纯拉伸的组合。

**右极分解**（Right Polar Decomposition）将 $\mathbf{F}$ 写成：

$$
\mathbf{F} = \mathbf{R} \mathbf{U}
$$

其中：
-   $\mathbf{R}$ 是一个**[旋转张量](@entry_id:191990)**（rotation tensor），它是一个正交矩阵（$\mathbf{R}^T \mathbf{R} = \mathbf{I}$）且[行列式](@entry_id:142978)为+1（$\det(\mathbf{R}) = 1$），代表了变形中的刚体旋转部分。
-   $\mathbf{U}$ 是**右[拉伸张量](@entry_id:193200)**（right stretch tensor），它是一个对称（$\mathbf{U}^T=\mathbf{U}$）且正定（所有[特征值](@entry_id:154894)都为正）的张量，代表了纯粹的拉伸或挤压变形。

这个分解的物理解释是：任何一个局部变形，都可以看作是先对参考构型进行一次纯拉伸（由 $\mathbf{U}$ 描述），然后再对拉伸后的构型进行一次刚体旋转（由 $\mathbf{R}$ 描述）。

[拉伸张量](@entry_id:193200) $\mathbf{U}$ 与[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 密切相关。由 $\mathbf{F}=\mathbf{R}\mathbf{U}$ 和 $\mathbf{C}=\mathbf{F}^T\mathbf{F}$ 可得：
$\mathbf{C} = (\mathbf{R}\mathbf{U})^T(\mathbf{R}\mathbf{U}) = \mathbf{U}^T\mathbf{R}^T\mathbf{R}\mathbf{U} = \mathbf{U}^T\mathbf{I}\mathbf{U} = \mathbf{U}^2$
因此，右[拉伸张量](@entry_id:193200) $\mathbf{U}$ 是[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 的唯一的正定平方根，即 $\mathbf{U} = \sqrt{\mathbf{C}}$。

$\mathbf{U}$ 的[特征值](@entry_id:154894)被称为**主拉伸**（principal stretches），记为 $\lambda_i$，它们表示了在三个相互正交的方向上材料纤维的最大、最小和中间拉伸率。$\mathbf{U}$ 的[特征向量](@entry_id:151813)则定义了这些**主拉伸方向**（principal stretch directions）在参考构型中的朝向。

我们通过一个二维变形的例子来演示极分解的计算过程 [@problem_id:1547220]。考虑映射 $x_1 = 2X_1 - X_2, x_2 = X_1 + 3X_2$。
1.  计算变形梯度 $\mathbf{F}$：
    $$
    \mathbf{F} = \begin{pmatrix} 2 & -1 \\ 1 & 3 \end{pmatrix}
    $$
2.  计算[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$：
    $$
    \mathbf{C} = \mathbf{F}^T \mathbf{F} = \begin{pmatrix} 2 & 1 \\ -1 & 3 \end{pmatrix} \begin{pmatrix} 2 & -1 \\ 1 & 3 \end{pmatrix} = \begin{pmatrix} 5 & 1 \\ 1 & 10 \end{pmatrix}
    $$
3.  计算 $\mathbf{C}$ 的[特征值](@entry_id:154894) $\mu$。它们是 $\mathbf{U}^2$ 的[特征值](@entry_id:154894)，而主拉伸 $\lambda$ 是 $\mathbf{U}$ 的[特征值](@entry_id:154894)，所以 $\mu = \lambda^2$。特征方程为 $\det(\mathbf{C} - \mu\mathbf{I}) = (5-\mu)(10-\mu) - 1 = \mu^2 - 15\mu + 49 = 0$。解得 $\mu_{1,2} = \frac{15 \pm \sqrt{29}}{2}$。
4.  因此，最大和最小主拉伸分别为：
    $$
    \lambda_1 = \sqrt{\frac{15 + \sqrt{29}}{2}}, \quad \lambda_2 = \sqrt{\frac{15 - \sqrt{29}}{2}}
    $$
5.  为了找到[旋转张量](@entry_id:191990) $\mathbf{R}$，我们可以利用 $\mathbf{U} = \mathbf{R}^T \mathbf{F}$ 并且 $\mathbf{U}$ 是对称的这一性质。设二维[旋转张量](@entry_id:191990)为 $\mathbf{R} = \begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix}$。则
    $$
    \mathbf{U} = \mathbf{R}^T\mathbf{F} = \begin{pmatrix} \cos\theta & \sin\theta \\ -\sin\theta & \cos\theta \end{pmatrix} \begin{pmatrix} 2 & -1 \\ 1 & 3 \end{pmatrix} = \begin{pmatrix} 2\cos\theta + \sin\theta & -\cos\theta + 3\sin\theta \\ -2\sin\theta + \cos\theta & \sin\theta + 3\cos\theta \end{pmatrix}
    $$
    由于 $\mathbf{U}$ 是对称的，其非对角元必须相等：$-\cos\theta + 3\sin\theta = -2\sin\theta + \cos\theta$，这给出 $\tan\theta = \frac{2}{5}$。由此可得 $\cos\theta = \frac{5}{\sqrt{29}}$ 和 $\sin\theta = \frac{2}{\sqrt{29}}$。二维[旋转张量](@entry_id:191990)的迹为 $\operatorname{tr}(\mathbf{R}) = 2\cos\theta = \frac{10}{\sqrt{29}}$。

### 高等主题：材料框架无关性

在建立材料本构关系（即应力与应变之间的关系）时，一个必须遵守的基本物理原理是**材料框架无关性**（principle of material frame-indifference），也称为**客观性**（objectivity）。该原理指出，材料的本构响应（例如其内部储存的[应变能](@entry_id:162699)）不应依赖于观察者（或[坐标系](@entry_id:156346)）的[刚体运动](@entry_id:193355)。

换言之，如果在当前构型上叠加一个任意的刚体旋转 $\mathbf{Q}$，材料的应力或[应变能](@entry_id:162699)不应发生改变。经过这种叠加旋转后，新的变形梯度变为 $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$。如果[应变能密度函数](@entry_id:755490)为 $W(\mathbf{F})$，那么[客观性原理](@entry_id:185412)要求：

$$
W(\mathbf{F}) = W(\mathbf{F}^*) = W(\mathbf{Q}\mathbf{F})
$$

此等式必须对所有[旋转张量](@entry_id:191990) $\mathbf{Q}$ 成立。这一要求极大地限制了[应变能函数](@entry_id:178435) $W$ 的可能形式。一个自然的结果是，$W$ 只能通过那些在叠加旋转下保持不变的量来依赖于 $\mathbf{F}$。

我们来考察[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 在叠加旋转下的变化：

$$
\mathbf{C}^* = (\mathbf{F}^*)^T \mathbf{F}^* = (\mathbf{Q}\mathbf{F})^T (\mathbf{Q}\mathbf{F}) = \mathbf{F}^T \mathbf{Q}^T \mathbf{Q} \mathbf{F} = \mathbf{F}^T \mathbf{I} \mathbf{F} = \mathbf{F}^T \mathbf{F} = \mathbf{C}
$$

可见，$\mathbf{C}$ 在这种变换下是不变的。因此，对于一个**各向同性**（isotropic）材料，其[应变能函数](@entry_id:178435)必须只能是 $\mathbf{C}$ 的函数，即 $W(\mathbf{F}) = \hat{W}(\mathbf{C})$。更进一步，由于旋转 $\mathbf{C}$ 的[坐标系](@entry_id:156346)也不应改变能量，$\hat{W}$ 最终必须是 $\mathbf{C}$ 的[标量不变量](@entry_id:193787)的函数。

对于**各向异性**（anisotropic）材料，比如具有特定纤维方向的[复合材料](@entry_id:139856)，情况类似。其[应变能函数](@entry_id:178435)必须是 $\mathbf{C}$ 和描述材料内部结构的张量（例如代表纤维方向的[单位向量](@entry_id:165907) $\mathbf{a}_0$）的联合[不变量](@entry_id:148850)的函数。

考虑一个为横观[各向同性材料](@entry_id:170678)提出的[应变能函数](@entry_id:178435)模型 [@problem_id:1547259]。其客观性可以通过将其完全用一组标准[不变量](@entry_id:148850)来表达而得到验证。这些[不变量](@entry_id:148850)包括：
$I_1 = \operatorname{tr}(\mathbf{C})$
$I_2 = \frac{1}{2}[(\operatorname{tr}\mathbf{C})^2 - \operatorname{tr}(\mathbf{C}^2)]$
$I_3 = \det(\mathbf{C})$
$I_4 = \mathbf{a}_0^T \mathbf{C} \mathbf{a}_0$
$I_5 = \mathbf{a}_0^T \mathbf{C}^2 \mathbf{a}_0$

假设一个[应变能函数](@entry_id:178435)形式为：
$W = c_1 \operatorname{tr}(\mathbf{F}^T\mathbf{F}) + c_2 \operatorname{tr}((\mathbf{F}\mathbf{F}^T)(\mathbf{F}\mathbf{a}_0 \otimes \mathbf{F}\mathbf{a}_0)) + c_3 \det(\mathbf{F})^2 (\mathbf{a}_0^T \mathbf{C}^{-1} \mathbf{a}_0)$

我们可以逐项将其转换为[不变量](@entry_id:148850)形式：
-   第一项：$\operatorname{tr}(\mathbf{F}^T\mathbf{F}) = \operatorname{tr}(\mathbf{C}) = I_1$。
-   第二项：利用迹的性质，可化为 $(\mathbf{F}\mathbf{a}_0)^T (\mathbf{F}\mathbf{F}^T) (\mathbf{F}\mathbf{a}_0) = \mathbf{a}_0^T \mathbf{F}^T \mathbf{F} \mathbf{F}^T \mathbf{F} \mathbf{a}_0 = \mathbf{a}_0^T \mathbf{C}^2 \mathbf{a}_0 = I_5$。
-   第三项：利用 $\det(\mathbf{F})^2 = \det(\mathbf{C}) = I_3$，以及三维张量的[Cayley-Hamilton定理](@entry_id:150551) $\mathbf{C}^{-1} = \frac{1}{I_3}(\mathbf{C}^2 - I_1\mathbf{C} + I_2\mathbf{I})$，可以推导出 $\mathbf{a}_0^T \mathbf{C}^{-1} \mathbf{a}_0 = \frac{1}{I_3}(I_5 - I_1 I_4 + I_2)$。因此，第三项变为 $c_3 I_3 \cdot \frac{1}{I_3}(I_5 - I_1 I_4 + I_2) = c_3(I_2 - I_1 I_4 + I_5)$。

将所有项合并，得到 $W = c_1 I_1 + c_2 I_5 + c_3(I_2 - I_1 I_4 + I_5) = c_1 I_1 + c_3 I_2 - c_3 I_1 I_4 + (c_2+c_3)I_5$。由于整个表达式完全由客观[不变量](@entry_id:148850)构成，该本构模型满足材料框架无关性原理。这一过程充分展示了变形梯度及其衍生量在构建严谨物理模型中的基础性地位。