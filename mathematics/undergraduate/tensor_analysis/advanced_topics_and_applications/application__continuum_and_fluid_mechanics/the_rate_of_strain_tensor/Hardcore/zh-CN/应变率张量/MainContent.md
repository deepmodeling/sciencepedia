## 引言
在连续介质力学中，精确描述流体或固体等可变形体的运动是理解其行为的核心。一个微小物质元的运动可以分解为平移、刚性旋转和变形的复杂组合。虽然速度梯度张量包含了所有这些信息，但为了深入分析材料的内在响应，我们必须将纯粹的变形从旋转中分离出来。本文旨在解决这一关键问题，重点介绍**应变率张量 (rate-of-strain tensor)**——一个专门用于量化物质变形速率的强大数学工具。

本文将带领读者系统地掌握应变率张量。在第一章“**原理和机制**”中，我们将从速度梯度张量的分解入手，详细阐述应变率张量的定义、计算方法及其分量的物理意义，并探讨其作为客观量度的重要性。接下来的“**应用与跨学科联系**”一章将展示该张量如何作为连接运动学与动力学的桥梁，在流体力学、材料科学和计算科学等多个领域中发挥关键作用。最后，通过“**动手实践**”环节，您将有机会通过解决具体问题来巩固和应用所学知识，从而将理论真正内化为实践能力。

## 原理和机制

在连续介质力学中，理解一个可变形体（例如流体或固体）的运动是核心任务之一。一个微小物质元的运动可以被分解为平移、旋转和变形。速度梯度张量捕捉了所有这些局部运动信息，而本章的重点——**应变率张量 (rate-of-strain tensor)**——是专门用来量化物质变形速率的工具。它在流体力学、材料科学和固体力学中扮演着至关重要的角色，因为它将运动学（运动的描述）与动力学（力的作用）联系起来。

### 速度梯度张量的分解

为了精确地描述流体微团的局部运动，我们首先引入**速度梯度张量 (velocity gradient tensor)**，记为 $\mathbf{L}$。给定一个速度场 $\vec{v}(\vec{x})$，该张量的分量在笛卡尔坐标系中定义为 $L_{ij} = \frac{\partial v_i}{\partial x_j}$。这个二阶张量完整地描述了在某点附近，速度是如何随空间位置变化的。

然而，速度梯度张量本身混合了两种截然不同的物理过程：物体的变形和物体的刚性旋转。为了将它们分离开来，我们可以利用任何方阵都可以唯一地分解为一个对称部分和一个反对称（或称斜对称）部分之和的数学原理。

我们将速度梯度张量 $\mathbf{L}$ 分解为：
$$ \mathbf{L} = \mathbf{D} + \mathbf{W} $$
其中：
*   **应变率张量 (Rate-of-Strain Tensor)** $\mathbf{D}$ 是 $\mathbf{L}$ 的对称部分：
    $$ \mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T) $$
    它的分量形式为 $D_{ij} = \frac{1}{2} \left( \frac{\partial v_i}{\partial x_j} + \frac{\partial v_j}{\partial x_i} \right)$。这个张量描述了物质微团体积和形状的改变速率，即**变形**的速率。由于其定义，应变率张量必然是对称的，即 $D_{ij} = D_{ji}$。

*   **自旋张量 (Spin Tensor)** 或**涡量张量 (Vorticity Tensor)** $\mathbf{W}$ 是 $\mathbf{L}$ 的反对称部分：
    $$ \mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T) $$
    它的分量形式为 $W_{ij} = \frac{1}{2} \left( \frac{\partial v_i}{\partial x_j} - \frac{\partial v_j}{\partial x_i} \right)$。这个张量描述了物质微团的**刚性旋转**速率，而与其形状改变无关。

通过这种分解，我们成功地将复杂的局部运动分离为纯变形（由 $\mathbf{D}$ 描述）和纯旋转（由 $\mathbf{W}$ 描述）。

### 应变率张量的计算与物理诠释

掌握应变率张量的定义后，我们可以通过一个具体的速度场来计算其分量。考虑一个三维流场，其速度由 $\vec{v}(x,y,z) = (axy)\hat{i} + (byz)\hat{j} + (czx)\hat{k}$ 给出，其中 $a, b, c$ 是常数 [@problem_id:1555477]。

首先，我们计算速度梯度张量 $\mathbf{L}$ 的所有分量：
$$
\mathbf{L} = \nabla\vec{v} =
\begin{pmatrix}
\frac{\partial v_x}{\partial x} & \frac{\partial v_x}{\partial y} & \frac{\partial v_x}{\partial z} \\
\frac{\partial v_y}{\partial x} & \frac{\partial v_y}{\partial y} & \frac{\partial v_y}{\partial z} \\
\frac{\partial v_z}{\partial x} & \frac{\partial v_z}{\partial y} & \frac{\partial v_z}{\partial z}
\end{pmatrix}
=
\begin{pmatrix}
ay & ax & 0 \\
0 & bz & by \\
cz & 0 & cx
\end{pmatrix}
$$

然后，根据定义 $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T)$，我们计算应变率张量 $\mathbf{D}$：
$$
\mathbf{D} = \frac{1}{2} \left(
\begin{pmatrix}
ay & ax & 0 \\
0 & bz & by \\
cz & 0 & cx
\end{pmatrix}
+
\begin{pmatrix}
ay & 0 & cz \\
ax & bz & 0 \\
0 & by & cx
\end{pmatrix}
\right)
=
\begin{pmatrix}
ay & \frac{1}{2}ax & \frac{1}{2}cz \\
\frac{1}{2}ax & bz & \frac{1}{2}by \\
\frac{1}{2}cz & \frac{1}{2}by & cx
\end{pmatrix}
$$
这个矩阵明确给出了流场中任意一点 $(x, y, z)$ 的变形速率。但这些分量的物理意义是什么？

#### 对角分量：法向应变率

应变率张量 $\mathbf{D}$ 的对角分量 $D_{11}, D_{22}, D_{33}$ 被称为**法向应变率 (normal strain rates)**。$D_{ii}$（无爱因斯坦求和约定）表示沿着 $x_i$ 轴方向的单位长度物质线的拉伸或压缩速率。

*   如果 $D_{ii} > 0$，表示物质线在该方向上正在被拉伸。
*   如果 $D_{ii} < 0$，表示物质线在该方向上正在被压缩。
*   如果 $D_{ii} = 0$，表示物质线在该方向上没有长度变化率。

例如，在聚合物薄膜的制造过程中，材料片被拉伸，这个过程可以建模为一种纯拉伸流。考虑一个二维速度场 $\vec{v}(x, y) = (\alpha x)\hat{i} + (\beta y)\hat{j}$，其中 $\alpha$ 和 $\beta$ 是正常数 [@problem_id:1555447]。对于该流场，$v_x = \alpha x$，$v_y = \beta y$。$D_{11}$ 分量的计算如下：
$$ D_{11} = \frac{1}{2} \left( \frac{\partial v_x}{\partial x} + \frac{\partial v_x}{\partial x} \right) = \frac{\partial v_x}{\partial x} = \frac{\partial (\alpha x)}{\partial x} = \alpha $$
这里的常数 $\alpha$ 直接量化了 $x$ 方向上每单位长度的拉伸速率。同样，可以计算出 $D_{22} = \beta$，代表 $y$ 方向的拉伸速率。

#### 非对角分量：剪切应变率

$\mathbf{D}$ 的非对角分量 $D_{ij}$ ($i \neq j$) 被称为**剪切应变率 (shear strain rates)**。$2D_{ij}$ 度量了最初沿着 $x_i$ 和 $x_j$ 轴的两条物质线之间夹角变小的速率。也就是说，它描述了流体微团形状的角变形速率。

考虑一个简单的平面剪切流 $\vec{v} = (\gamma y)\hat{i}$，其中 $\gamma$ 是剪切率 [@problem_id:1555484]。这个速度场描述了流体层之间相互滑动的场景，比如在两个平行板之间的流动。我们计算其应变率张量的分量：
$$ D_{12} = D_{21} = \frac{1}{2} \left( \frac{\partial v_x}{\partial y} + \frac{\partial v_y}{\partial x} \right) = \frac{1}{2} (\gamma + 0) = \frac{\gamma}{2} $$
所有其他分量均为零。这个结果表明，在简单剪切流中，变形完全由剪切应变率描述。可以进一步证明，对于最初分别沿 $x$ 轴和 $y$ 轴的两条相互垂直的物质线，它们之间的夹角 $\theta$ 的变化率在初始时刻 $t=0$ 为 $\frac{d\theta}{dt} = -\gamma = -2D_{12}$。负号表示夹角正在从 $\pi/2$ 减小，这正是剪切变形的特征。

#### 变形与旋转的区分：刚体旋转

应变率张量的一个关键特性是它只捕捉变形。对于一个不发生形状或体积改变的运动，其应变率张量应为零。一个典型的例子是**刚体旋转 (rigid-body rotation)**。

考虑一个在微机电系统（MEMS）陀螺仪中的旋转盘，它以恒定角速度 $\omega$ 绕 $z$ 轴旋转 [@problem_id:1555454]。其速度场为 $\vec{v} = (-\omega y)\hat{i} + (\omega x)\hat{j}$。我们来计算其应变率张量：
$$ L_{12} = \frac{\partial v_x}{\partial y} = -\omega, \quad L_{21} = \frac{\partial v_y}{\partial x} = \omega $$
所有其他速度梯度分量都为零。因此，速度梯度张量为：
$$ \mathbf{L} = \begin{pmatrix} 0 & -\omega & 0 \\ \omega & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix} $$
这是一个纯反对称矩阵。现在计算应变率张量 $\mathbf{D}$：
$$ \mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T) = \frac{1}{2} \left( \begin{pmatrix} 0 & -\omega & 0 \\ \omega & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix} + \begin{pmatrix} 0 & \omega & 0 \\ -\omega & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix} \right) = \begin{pmatrix} 0 & 0 & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix} $$
结果是零张量。这有力地证明了刚体旋转是一种无变形的运动。尽管流体中的粒子在移动并且有非零的速度梯度，但它们的形状和大小没有改变，因此应变率为零。所有的运动信息都包含在自旋张量 $\mathbf{W} = \mathbf{L}$ 中。

### 张量不变量及其物理意义

应变率张量的某些组合在坐标系旋转下保持不变，这些量被称为张量不变量，它们通常具有深刻的物理意义。

#### 第一不变量：体积应变率

应变率张量的迹 (trace)，即对角元素之和，是其第一不变量。
$$ \text{tr}(\mathbf{D}) = D_{11} + D_{22} + D_{33} $$
利用 $D_{ii} = \frac{\partial v_i}{\partial x_i}$ （此处不求和），我们得到：
$$ \text{tr}(\mathbf{D}) = \frac{\partial v_x}{\partial x} + \frac{\partial v_y}{\partial y} + \frac{\partial v_z}{\partial z} = \nabla \cdot \vec{v} $$
这正是速度场的散度。它的物理意义是**体积应变率 (volumetric strain rate)**，即单位体积的物质微团的体积膨胀或收缩的速率 [@problem_id:1555472]。

*   如果 $\nabla \cdot \vec{v} > 0$，流体在该点膨胀。
*   如果 $\nabla \cdot \vec{v} < 0$，流体在该点压缩。
*   如果 $\nabla \cdot \vec{v} = 0$，流体的体积保持不变，这种流动被称为**不可压缩流 (incompressible flow)**。

对于势流，如果速度势 $\phi$ 满足拉普拉斯方程 $\nabla^2\phi = 0$，那么流场是无散的，即 $\nabla \cdot \vec{v} = \nabla \cdot (\nabla \phi) = \nabla^2\phi = 0$。这意味着应变率张量的迹为零，流动是不可压缩的 [@problem_id:1555465]。在一些复杂流动分析中，不可压缩性和无剪切应变的条件可以用来约束流动参数 [@problem_id:1555492]。

### 主应变率与主方向

由于应变率张量 $\mathbf{D}$ 是一个实对称张量，它具有一个非常重要的数学性质：它总是可以被对角化。这意味着我们可以找到一个特殊的正交坐标系，在这个坐标系中，应变率张量只有对角分量。

*   $\mathbf{D}$ 的**特征值 (eigenvalues)** 被称为**主应变率 (principal strain rates)**。它们代表了物质微团在三个相互垂直方向上的最大和最小拉伸/压缩率。在这些方向上，变形是纯粹的拉伸或压缩，没有剪切。

*   $\mathbf{D}$ 的**特征向量 (eigenvectors)** 定义了这些特殊方向，被称为**主应变方向 (principal directions of strain)**。它们构成了变形的“自然”坐标系。

寻找主应变率和主方向是标准的特征值问题。例如，对于一个二维流场，其在某点的应变率张量为 [@problem_id:1555430]：
$$ \mathbf{D} = \begin{pmatrix} 1 & 3 \\ 3 & 1 \end{pmatrix} \text{ s}^{-1} $$
我们通过求解特征方程 $\det(\mathbf{D} - \lambda \mathbf{I}) = 0$ 来寻找主应变率 $\lambda$：
$$ (1-\lambda)^2 - 3^2 = 0 \implies 1-\lambda = \pm 3 $$
解得两个主应变率 $\lambda_1 = 4 \text{ s}^{-1}$（最大拉伸率）和 $\lambda_2 = -2 \text{ s}^{-1}$（最大压缩率）。

然后，通过求解 $(\mathbf{D} - \lambda \mathbf{I})\vec{n} = \vec{0}$，我们可以找到对应的主方向 $\vec{n}$。对于另一个例子，如果张量为 [@problem_id:1555499]：
$$ \mathbf{D} = \begin{pmatrix} 4 & -2 \\ -2 & 7 \end{pmatrix} $$
其特征值为 $\lambda_1 = 3$ 和 $\lambda_2 = 8$。对应的单位特征向量（主方向）可以计算出来，它们是正交的，指明了纯拉伸的方向。

### 应变率张量的客观性

在连续介质力学中，一个重要的概念是**客观性 (objectivity)**。一个客观的张量所描述的物理量不应该依赖于观察者的运动状态（特指不依赖于叠加的刚性旋转）。应变率张量正是一个客观的张量，这使它成为一个真正衡量材料内在变形的工具。

我们可以通过一个思想实验来证明这一点 [@problem_id:1555493]。假设我们有一个基础流场 $\vec{v}(\vec{x})$，其速度梯度为 $\mathbf{L}$，应变率张量为 $\mathbf{D}$。现在，我们从一个以角速度 $\boldsymbol{\Omega}$ 旋转的参考系来观察这个流动。这等效于在原速度场上叠加一个刚体旋转速度 $\boldsymbol{\Omega} \times \vec{x}$。新的速度场为 $\vec{v}^* = \vec{v} + \boldsymbol{\Omega} \times \vec{x}$。

新速度场的梯度为 $\mathbf{L}^* = \nabla\vec{v}^* = \nabla\vec{v} + \nabla(\boldsymbol{\Omega} \times \vec{x})$。我们已经知道 $\nabla\vec{v} = \mathbf{L}$，并且刚体旋转的梯度是一个反对称张量，我们记为 $\mathbf{R}$。所以 $\mathbf{L}^* = \mathbf{L} + \mathbf{R}$。

现在计算新的应变率张量 $\mathbf{D}^*$：
$$ \mathbf{D}^* = \frac{1}{2}(\mathbf{L}^* + (\mathbf{L}^*)^T) = \frac{1}{2}((\mathbf{L} + \mathbf{R}) + (\mathbf{L} + \mathbf{R})^T) = \frac{1}{2}(\mathbf{L} + \mathbf{R} + \mathbf{L}^T + \mathbf{R}^T) $$
由于 $\mathbf{L}^T$ 是 $\mathbf{L}$ 的转置，而 $\mathbf{R}$ 是反对称的（即 $\mathbf{R}^T = -\mathbf{R}$），上式变为：
$$ \mathbf{D}^* = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T) + \frac{1}{2}(\mathbf{R} + \mathbf{R}^T) = \mathbf{D} + \frac{1}{2}(\mathbf{R} - \mathbf{R}) = \mathbf{D} + \mathbf{0} = \mathbf{D} $$
这个结果表明，叠加一个刚体旋转完全不影响应变率张量的计算结果。因此，应变率张量是客观的，它测量的变形是独立于观察者旋转状态的内在物理属性。相比之下，速度梯度张量 $\mathbf{L}$ 本身不是客观的，因为它会随着观察者的旋转而改变。这正是我们将 $\mathbf{L}$ 分解为 $\mathbf{D}$ 和 $\mathbf{W}$ 的根本物理动机之一。