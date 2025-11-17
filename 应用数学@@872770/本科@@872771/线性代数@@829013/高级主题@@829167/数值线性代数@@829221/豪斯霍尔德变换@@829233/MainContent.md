## 引言
豪斯霍尔德（Householder）变换是线性代数中一个基础而强大的工具，它在几何上代表了一种简单的镜像反射，但在计算领域却扮演着至关重要的角色。从理论到实践，理解[豪斯霍尔德变换](@entry_id:168808)意味着跨越从直观的几何概念到高效、稳健的[数值算法](@entry_id:752770)之间的鸿沟。许多学习者仅将其视为一个固定的代数公式，而未能充分认识到它作为解决复杂计算问题的通用方法的强大潜力。

本文旨在系统性地揭示[豪斯霍尔德变换](@entry_id:168808)的理论深度与应用广度。我们将超越表面公式，深入探讨其内在机制和关键性质，并展示它如何成为现代[科学计算](@entry_id:143987)的支柱之一。

在接下来的内容中，读者将首先在“**原理与机制**”一章中学习其定义、核心代数性质（如对称性与正交性）以及如何为特定任务构造反射。随后，“**应用与跨学科联系**”一章将展示该变换在QR分解、[最小二乘问题](@entry_id:164198)、[特征值计算](@entry_id:145559)等核心算法中的应用，并探索其在计算机图形学、数据科学和几何学中的角色。最后，“**动手实践**”部分将提供具体问题，帮助读者巩固所学知识。

## 原理与机制

在本章中，我们将深入探讨[豪斯霍尔德变换](@entry_id:168808)（Householder transformation）的核心原理与机制。作为一种基本的线性变换，[豪斯霍尔德变换](@entry_id:168808)在几何上对应于[向量空间](@entry_id:151108)中关于一个[超平面](@entry_id:268044)的镜像反射。我们将从其几何直觉出发，建立其[代数表示](@entry_id:143783)，系统地研究其关键性质，并最终展示如何利用这些性质来解决[数值线性代数](@entry_id:144418)中的核心问题。

### [豪斯霍尔德反射](@entry_id:637383)的定义

从几何角度看，一个[反射变换](@entry_id:175518)由定义反射“[镜面](@entry_id:148117)”的[超平面](@entry_id:268044)唯一确定。在 $n$ 维欧几里得空间 $\mathbb{R}^n$ 中，任何一个通过原点的[超平面](@entry_id:268044)都可以由其唯一的法向量（normal vector）$\boldsymbol{v}$ 来定义。[豪斯霍尔德变换](@entry_id:168808)正是利用这个法向量来构建一个矩阵，该矩阵能将空间中的任意向量关于这个[超平面](@entry_id:268044)进行反射。

要理解其构造，最直观的方式是借助**[正交投影](@entry_id:144168)**（orthogonal projection）的概念。对于任意非[零向量](@entry_id:156189) $\boldsymbol{v} \in \mathbb{R}^n$，我们可以定义一个[投影矩阵](@entry_id:154479) $P_{\boldsymbol{v}}$，它能将任意向量 $\boldsymbol{x}$ 投影到由 $\boldsymbol{v}$ 张成的[线性子空间](@entry_id:151815)（即一条直线）上。这个[投影矩阵](@entry_id:154479)由向量 $\boldsymbol{v}$ 的外积给出：

$$
P_{\boldsymbol{v}} = \frac{\boldsymbol{v}\boldsymbol{v}^T}{\boldsymbol{v}^T\boldsymbol{v}}
$$

其中，$\boldsymbol{v}^T\boldsymbol{v}$ 是 $\boldsymbol{v}$ 与自身的[内积](@entry_id:158127)，即其欧几里得范数的平方 $\|\boldsymbol{v}\|_2^2$，这是一个标量。而 $\boldsymbol{v}\boldsymbol{v}^T$ 是一个 $n \times n$ 的矩阵，称为外积。因此，$P_{\boldsymbol{v}}\boldsymbol{x}$ 就是向量 $\boldsymbol{x}$ 在 $\boldsymbol{v}$方向上的[正交投影](@entry_id:144168)分量。

有了投影的概念，[豪斯霍尔德反射](@entry_id:637383)的几何意义就变得清晰了。为了将向量 $\boldsymbol{x}$ 关于垂直于 $\boldsymbol{v}$ 的超平面进行反射，我们首先需要找到从 $\boldsymbol{x}$ 到达该[超平面](@entry_id:268044)的路径，这条路径正好是 $\boldsymbol{x}$ 在 $\boldsymbol{v}$ 方向上的投影，即 $P_{\boldsymbol{v}}\boldsymbol{x}$。从 $\boldsymbol{x}$ 的末端减去这个投影向量，我们就到达了反射[超平面](@entry_id:268044)上的一点。为了完成反射，我们需要再减去一次相同的投影向量，从而到达超平面的“另一侧”。因此，反射后的向量 $H\boldsymbol{x}$ 就是 $\boldsymbol{x} - 2P_{\boldsymbol{v}}\boldsymbol{x}$。

由此，我们可以将[豪斯霍尔德矩阵](@entry_id:155018) $H$ 表示为与单位矩阵 $I$ 和[投影矩阵](@entry_id:154479) $P_{\boldsymbol{v}}$ 的[线性组合](@entry_id:154743) [@problem_id:1366969]：

$$
H = I - 2P_{\boldsymbol{v}} = I - 2 \frac{\boldsymbol{v}\boldsymbol{v}^T}{\boldsymbol{v}^T\boldsymbol{v}}
$$

这就是[豪斯霍尔德矩阵](@entry_id:155018)的权威定义。它完全由一个非零向量 $\boldsymbol{v}$ 决定。

为了将这个抽象的定义具体化，让我们看一个在 $\mathbb{R}^2$ 中的例子。假设我们希望构建一个由向量 $\boldsymbol{v} = \begin{pmatrix} 2 \\ -1 \end{pmatrix}$ 定义的[豪斯霍尔德矩阵](@entry_id:155018) [@problem_id:1367012]。

首先，我们计算定义中的两个关键部分：
[内积](@entry_id:158127)：$\boldsymbol{v}^T\boldsymbol{v} = 2^2 + (-1)^2 = 5$。
外积：$\boldsymbol{v}\boldsymbol{v}^T = \begin{pmatrix} 2 \\ -1 \end{pmatrix} \begin{pmatrix} 2 & -1 \end{pmatrix} = \begin{pmatrix} 4 & -2 \\ -2 & 1 \end{pmatrix}$。

接下来，我们将这些值代入豪斯霍尔德公式：
$$
H = I - 2 \frac{\boldsymbol{v}\boldsymbol{v}^T}{\boldsymbol{v}^T\boldsymbol{v}} = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} - \frac{2}{5} \begin{pmatrix} 4 & -2 \\ -2 & 1 \end{pmatrix} = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} - \begin{pmatrix} \frac{8}{5} & -\frac{4}{5} \\ -\frac{4}{5} & \frac{2}{5} \end{pmatrix} = \begin{pmatrix} -\frac{3}{5} & \frac{4}{5} \\ \frac{4}{5} & \frac{3}{5} \end{pmatrix}
$$
这个 $2 \times 2$ 矩阵 $H$ 就代表了关于与向量 $\boldsymbol{v} = (2, -1)^T$ 垂直的直线（即直线 $y = 2x$）的反射。

这个公式同样适用于我们熟悉的几何变换。例如，考虑在 $\mathbb{R}^2$ 中关于 $x_1$ 轴的反射。这个反射的“镜面”是 $x_1$ 轴，其[法向量](@entry_id:264185)是[标准基向量](@entry_id:152417) $\boldsymbol{e}_2 = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$。使用这个向量作为我们的 $\boldsymbol{v}$，我们得到 [@problem_id:1366945]：
$\boldsymbol{v}^T\boldsymbol{v} = 1$ 且 $\boldsymbol{v}\boldsymbol{v}^T = \begin{pmatrix} 0 \\ 1 \end{pmatrix} \begin{pmatrix} 0 & 1 \end{pmatrix} = \begin{pmatrix} 0 & 0 \\ 0 & 1 \end{pmatrix}$。
因此，
$$
H = I - 2 \frac{\boldsymbol{v}\boldsymbol{v}^T}{\boldsymbol{v}^T\boldsymbol{v}} = \begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} - 2 \begin{pmatrix} 0 & 0 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}
$$
这个矩阵正是将任意向量 $\begin{pmatrix} x_1 \\ x_2 \end{pmatrix}$ 映射到 $\begin{pmatrix} x_1 \\ -x_2 \end{pmatrix}$ 的标准反射矩阵，这验证了我们定义的普适性。

### 核心代数性质

[豪斯霍尔德矩阵](@entry_id:155018)拥有一系列优美的代数性质，这些性质不仅深刻地反映了其几何本质，也使其成为数值计算中极为强大和可靠的工具。

#### 对称性 (Symmetry)

[豪斯霍尔德矩阵](@entry_id:155018)总是**对称的**，即 $H = H^T$。我们可以通过对其定义式求转置来证明这一点 [@problem_id:18003]：
$$
H^T = \left(I - 2 \frac{\boldsymbol{v}\boldsymbol{v}^T}{\boldsymbol{v}^T\boldsymbol{v}}\right)^T = I^T - 2 \left(\frac{\boldsymbol{v}\boldsymbol{v}^T}{\boldsymbol{v}^T\boldsymbol{v}}\right)^T
$$
由于单位矩阵是对称的（$I^T = I$），且标量因子 $\frac{2}{\boldsymbol{v}^T\boldsymbol{v}}$ 不受[转置](@entry_id:142115)影响，我们只需关注外积矩阵 $(\boldsymbol{v}\boldsymbol{v}^T)^T$。根据矩阵[转置的性质](@entry_id:148302)，$(\boldsymbol{v}\boldsymbol{v}^T)^T = (\boldsymbol{v}^T)^T \boldsymbol{v}^T = \boldsymbol{v}\boldsymbol{v}^T$。因此，外积矩阵本身就是对称的。
所以，
$$
H^T = I - 2 \frac{\boldsymbol{v}\boldsymbol{v}^T}{\boldsymbol{v}^T\boldsymbol{v}} = H
$$
证明完毕。这意味着 $H$ 与其[转置](@entry_id:142115)完全相同。

#### 正交性与保范性 (Orthogonality and Norm-Preservation)

[豪斯霍尔德矩阵](@entry_id:155018)最重要的性质之一是它是**[正交矩阵](@entry_id:169220)**（orthogonal matrix），即 $H^T H = I$。由于我们已经证明 $H$ 是对称的（$H^T = H$），证明其正交性等价于证明 $H^2 = I$。这个性质也被称为**对合性**（involutory），意味着连续两次应用相同的反射会使任何向量返回其初始位置，这完全符合几何直觉。

让我们来证明 $H^2 = I$。再次使用 $H = I - 2P_{\boldsymbol{v}}$ 的形式，其中 $P_{\boldsymbol{v}} = \frac{\boldsymbol{v}\boldsymbol{v}^T}{\boldsymbol{v}^T\boldsymbol{v}}$。一个关键的事实是[投影矩阵](@entry_id:154479)具有[幂等性](@entry_id:190768)（idempotent），即 $P_{\boldsymbol{v}}^2 = P_{\boldsymbol{v}}$。
$$
P_{\boldsymbol{v}}^2 = \left(\frac{\boldsymbol{v}\boldsymbol{v}^T}{\boldsymbol{v}^T\boldsymbol{v}}\right) \left(\frac{\boldsymbol{v}\boldsymbol{v}^T}{\boldsymbol{v}^T\boldsymbol{v}}\right) = \frac{\boldsymbol{v}(\boldsymbol{v}^T\boldsymbol{v})\boldsymbol{v}^T}{(\boldsymbol{v}^T\boldsymbol{v})^2} = \frac{(\boldsymbol{v}^T\boldsymbol{v})\boldsymbol{v}\boldsymbol{v}^T}{(\boldsymbol{v}^T\boldsymbol{v})^2} = \frac{\boldsymbol{v}\boldsymbol{v}^T}{\boldsymbol{v}^T\boldsymbol{v}} = P_{\boldsymbol{v}}
$$
现在我们可以计算 $H^2$：
$$
H^2 = (I - 2P_{\boldsymbol{v}})^2 = I^2 - 4P_{\boldsymbol{v}} + 4P_{\boldsymbol{v}}^2 = I - 4P_{\boldsymbol{v}} + 4P_{\boldsymbol{v}} = I
$$
这就证明了 $H$ 是正交且对合的。

对合性质在动态系统中表现得非常有趣。例如，考虑一个粒子的位置由递归关系 $\boldsymbol{p}_n = H \boldsymbol{p}_{n-1}$ 描述，其中 $H$ 是一个[豪斯霍尔德矩阵](@entry_id:155018)。我们想知道在第99步时粒子的位置 $\boldsymbol{p}_{99}$。由于 $\boldsymbol{p}_n = H^n \boldsymbol{p}_0$ 且 $H^2=I$，我们可以推断 $H^n$ 的规律：当 $n$ 为偶数时，$H^n = (H^2)^{n/2} = I^{n/2} = I$；当 $n$ 为奇数时，$H^n = H H^{n-1} = H I = H$。因为99是奇数，所以 $\boldsymbol{p}_{99} = H \boldsymbol{p}_0$ [@problem_id:1366983]。我们无需进行99次矩阵乘法，只需一次即可。

正交性的一个直接且至关重要的推论是[豪斯霍尔德变换](@entry_id:168808)**保持向量的[欧几里得范数](@entry_id:172687)**（即长度），这种变换称为**[等距同构](@entry_id:273188)**（isometry）。对于任意向量 $\boldsymbol{u}$，其变换后向量 $H\boldsymbol{u}$ 的范数平方为：
$$
\|H\boldsymbol{u}\|_2^2 = (H\boldsymbol{u})^T (H\boldsymbol{u}) = \boldsymbol{u}^T H^T H \boldsymbol{u} = \boldsymbol{u}^T I \boldsymbol{u} = \boldsymbol{u}^T \boldsymbol{u} = \|\boldsymbol{u}\|_2^2
$$
因此，$\|H\boldsymbol{u}\|_2 = \|\boldsymbol{u}\|_2$。这意味着经过[豪斯霍尔德反射](@entry_id:637383)后，向量的长度保持不变 [@problem_id:1366989]。这一性质是[豪斯霍尔德变换](@entry_id:168808)在数值算法中保持数值稳定性的基石，因为它不会放大计算过程中产生的[舍入误差](@entry_id:162651)。

### 几何解释：特征空间

要从根本上理解一个[线性变换](@entry_id:149133)，分析其**[特征向量](@entry_id:151813)**（eigenvectors）和**[特征值](@entry_id:154894)**（eigenvalues）是必不可少的。[豪斯霍尔德矩阵](@entry_id:155018)的特征结构完美地揭示了其反射的几何本质。

首先，让我们考察定义反射超平面的法向量 $\boldsymbol{v}$ 本身在变换下的行为。我们将 $H$ 应用于 $\boldsymbol{v}$ [@problem_id:17994]：
$$
H\boldsymbol{v} = \left(I - 2 \frac{\boldsymbol{v}\boldsymbol{v}^T}{\boldsymbol{v}^T\boldsymbol{v}}\right) \boldsymbol{v} = I\boldsymbol{v} - 2 \frac{\boldsymbol{v}(\boldsymbol{v}^T\boldsymbol{v})}{\boldsymbol{v}^T\boldsymbol{v}} = \boldsymbol{v} - 2\boldsymbol{v} = -\boldsymbol{v}
$$
这个结果表明 $H\boldsymbol{v} = (-1)\boldsymbol{v}$。这意味着，法向量 $\boldsymbol{v}$ 是 $H$ 的一个[特征向量](@entry_id:151813)，其对应的[特征值](@entry_id:154894)为 $\lambda = -1$。这在几何上是完全合理的：垂直于镜面的向量在反射后方向会完全反转。

接下来，我们考虑那些位于反射超平面内的向量。根据定义，这些向量 $\boldsymbol{u}$ 都与[法向量](@entry_id:264185) $\boldsymbol{v}$ 正交，即它们的[内积](@entry_id:158127)为零：$\boldsymbol{v}^T\boldsymbol{u} = 0$。现在我们将 $H$ 应用于这样的向量 $\boldsymbol{u}$ [@problem_id:1366949]：
$$
H\boldsymbol{u} = \left(I - 2 \frac{\boldsymbol{v}\boldsymbol{v}^T}{\boldsymbol{v}^T\boldsymbol{v}}\right) \boldsymbol{u} = I\boldsymbol{u} - 2 \frac{\boldsymbol{v}(\boldsymbol{v}^T\boldsymbol{u})}{\boldsymbol{v}^T\boldsymbol{v}} = \boldsymbol{u} - 2 \frac{\boldsymbol{v}(0)}{\boldsymbol{v}^T\boldsymbol{v}} = \boldsymbol{u}
$$
这个结果表明 $H\boldsymbol{u} = (1)\boldsymbol{u}$。这意味着，任何位于反射[超平面](@entry_id:268044)内的向量都是 $H$ 的[特征向量](@entry_id:151813)，其对应的[特征值](@entry_id:154894)为 $\lambda = 1$。这些向量在反射中保持不变，它们是变换的**[不动点](@entry_id:156394)**（fixed points）。

在 $n$ 维空间中，与向量 $\boldsymbol{v}$ 正交的[子空间](@entry_id:150286)（即反射超平面）的维度是 $n-1$。因此，我们可以找到 $n-1$ 个线性无关的[特征向量](@entry_id:151813)，它们都对应于[特征值](@entry_id:154894) $1$。

综上所述，一个在 $\mathbb{R}^n$ 中的[豪斯霍尔德矩阵](@entry_id:155018) $H$ 拥有一个等于 $-1$ 的[特征值](@entry_id:154894)（其特征空间由[法向量](@entry_id:264185) $\boldsymbol{v}$ 张成），以及 $n-1$ 个等于 $1$ 的[特征值](@entry_id:154894)（其特征空间就是反射[超平面](@entry_id:268044)本身）。这个完整的特征谱系简洁而深刻地描述了[豪斯霍尔德反射](@entry_id:637383)的全部几何行为。

### 为特定任务构造反射

[豪斯霍尔德变换](@entry_id:168808)的强大之处不仅在于其优雅的性质，更在于我们可以精确地构造它来完成特定的几何任务。其中最常见和最有用的任务是：给定两个长度相等但方向不同的向量 $\boldsymbol{x}$ 和 $\boldsymbol{y}$，找到一个[豪斯霍尔德反射](@entry_id:637383) $H$ 能将 $\boldsymbol{x}$ 映射到 $\boldsymbol{y}$，即 $H\boldsymbol{x} = \boldsymbol{y}$。

由于[豪斯霍尔德变换](@entry_id:168808)是[等距同构](@entry_id:273188)，一个必要条件是 $\|\boldsymbol{x}\|_2 = \|\boldsymbol{y}\|_2$。假设这个条件成立，我们如何找到定义该反射的[法向量](@entry_id:264185) $\boldsymbol{v}$ 呢？

从几何上看，将 $\boldsymbol{x}$ 反射到 $\boldsymbol{y}$ 的[超平面](@entry_id:268044)必须是连接向量 $\boldsymbol{x}$ 和 $\boldsymbol{y}$ 端点的线段的垂直平分面。这个平面的法向量方向与向量 $\boldsymbol{x}-\boldsymbol{y}$ 的方向相同。因此，一个自然的选择是令 $\boldsymbol{v} = \boldsymbol{x} - \boldsymbol{y}$。

现在我们来验证这个选择是否正确。我们想证明，如果取 $\boldsymbol{v} = \boldsymbol{x} - \boldsymbol{y}$（其中 $\boldsymbol{x} \neq \boldsymbol{y}$），则 $H_{\boldsymbol{v}}\boldsymbol{x} = \boldsymbol{y}$ [@problem_id:1366972]。
根据定义，$H_{\boldsymbol{v}}\boldsymbol{x} = \boldsymbol{x} - 2 \frac{\boldsymbol{v}^T\boldsymbol{x}}{\boldsymbol{v}^T\boldsymbol{v}} \boldsymbol{v}$。我们代入 $\boldsymbol{v} = \boldsymbol{x} - \boldsymbol{y}$：
$$
\boldsymbol{v}^T\boldsymbol{x} = (\boldsymbol{x}-\boldsymbol{y})^T\boldsymbol{x} = \boldsymbol{x}^T\boldsymbol{x} - \boldsymbol{y}^T\boldsymbol{x} = \|\boldsymbol{x}\|_2^2 - \boldsymbol{y}^T\boldsymbol{x}
$$
$$
\boldsymbol{v}^T\boldsymbol{v} = (\boldsymbol{x}-\boldsymbol{y})^T(\boldsymbol{x}-\boldsymbol{y}) = \boldsymbol{x}^T\boldsymbol{x} - \boldsymbol{y}^T\boldsymbol{x} - \boldsymbol{x}^T\boldsymbol{y} + \boldsymbol{y}^T\boldsymbol{y}
$$
因为 $\boldsymbol{x}^T\boldsymbol{y} = \boldsymbol{y}^T\boldsymbol{x}$ 且 $\|\boldsymbol{x}\|_2^2 = \|\boldsymbol{y}\|_2^2$，上式变为：
$$
\boldsymbol{v}^T\boldsymbol{v} = 2\|\boldsymbol{x}\|_2^2 - 2\boldsymbol{y}^T\boldsymbol{x} = 2(\|\boldsymbol{x}\|_2^2 - \boldsymbol{y}^T\boldsymbol{x})
$$
于是，比值 $\frac{\boldsymbol{v}^T\boldsymbol{x}}{\boldsymbol{v}^T\boldsymbol{v}}$ 惊人地简化了：
$$
\frac{\boldsymbol{v}^T\boldsymbol{x}}{\boldsymbol{v}^T\boldsymbol{v}} = \frac{\|\boldsymbol{x}\|_2^2 - \boldsymbol{y}^T\boldsymbol{x}}{2(\|\boldsymbol{x}\|_2^2 - \boldsymbol{y}^T\boldsymbol{x})} = \frac{1}{2}
$$
将这个结果代回 $H_{\boldsymbol{v}}\boldsymbol{x}$ 的表达式：
$$
H_{\boldsymbol{v}}\boldsymbol{x} = \boldsymbol{x} - 2\left(\frac{1}{2}\right)\boldsymbol{v} = \boldsymbol{x} - \boldsymbol{v} = \boldsymbol{x} - (\boldsymbol{x} - \boldsymbol{y}) = \boldsymbol{y}
$$
这证明了我们的猜想：向量 $\boldsymbol{v} = \boldsymbol{x} - \boldsymbol{y}$ 确实定义了将 $\boldsymbol{x}$ 映射到 $\boldsymbol{y}$ 的[豪斯霍尔德反射](@entry_id:637383)。

这一结论是[数值线性代数](@entry_id:144418)中许多重要算法的基石，例如**QR分解**。在[QR分解](@entry_id:139154)中，一个核心步骤是将给定向量 $\boldsymbol{x}$ 变换为一个沿着某个坐标轴的向量，例如 $y = \sigma \boldsymbol{e}_1$，其中 $\boldsymbol{e}_1$ 是第一个[标准基向量](@entry_id:152417)，$\sigma = \pm \|\boldsymbol{x}\|_2$。通过选择 $\boldsymbol{v} = \boldsymbol{x} - \sigma \boldsymbol{e}_1$，我们可以构造一个[豪斯霍尔德矩阵](@entry_id:155018)，它能将 $\boldsymbol{x}$ 中的特定元素“清零”，从而逐步将一个矩阵转化为上三角形式。

最后，值得一提的是，[豪斯霍尔德变换](@entry_id:168808)的组合也具有明确的几何结构。例如，考虑一个由 $H_1$ 和 $H_2$ 构成的复合变换 $M = H_2 H_1 H_2$。由于 $H_2$ 是其自身的逆，这个表达式是 $H_1$ 的一个共轭变换。可以证明，这个复合变换本身也是一个[豪斯霍尔德反射](@entry_id:637383)，其[法向量](@entry_id:264185)是原法向量 $v_1$ 经过 $H_2$ 反射后的结果，即 $\boldsymbol{v}_3 = H_2 \boldsymbol{v}_1$ [@problem_id:1366991]。这揭示了[反射变换](@entry_id:175518)群的深刻[代数结构](@entry_id:137052)，也为更高级的[几何算法](@entry_id:175693)和理论提供了基础。