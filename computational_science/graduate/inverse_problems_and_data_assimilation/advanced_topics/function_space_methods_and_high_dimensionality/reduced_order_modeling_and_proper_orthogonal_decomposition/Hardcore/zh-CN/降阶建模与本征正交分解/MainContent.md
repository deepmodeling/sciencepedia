## 引言
在现代科学与工程领域，从天气预报到飞机设计，高保真度的数值模拟已成为不可或缺的研究工具。然而，这些模型往往涉及数百万甚至数十亿的自由度，导致其计算成本极为高昂。这一“维度诅咒”严重制约了我们在实时控制、多场景优化、以及不确定性量化等关键任务中的探索能力。如何才能在不牺牲过多精度的前提下，构建出能够快速、准确预测复杂系统行为的代理模型？这正是当前计算科学面临的核心挑战之一。

本文旨在系统性地介绍一种强大而优雅的解决方案：基于**本征正交分解（Proper Orthogonal Decomposition, POD）**的**降阶建模（Reduced-Order Modeling, ROM）**。这种方法的核心思想在于，尽管系统状态空间维度极高，其动态行为往往被限制在一个低维的内在结构上。通过从数据中学习并提取这个主导结构，我们可以构建出维度极小但能有效捕捉关键动力学的降阶模型。

为了帮助读者全面掌握这一技术，本文将分为三个核心部分。在**“原理与机制”**一章中，我们将深入探讨POD的数学基础，学习如何从数据快照中提取最优基函数，并通过伽辽金投影构建动力学方程。接下来的**“应用与交叉学科联系”**一章，将展示降阶模型如何在数据同化、优化设计、多物理场耦合以及纯数据驱动分析等多个前沿领域发挥关键作用。最后，在**“动手实践”**一章中，读者将通过具体的编程练习，将理论知识转化为解决实际问题的能力。

通过本次学习，读者不仅将掌握构建降阶模型的具体方法，更将深入理解其背后的数据驱动思想，从而能够将其应用于各自的研究与工程实践中。现在，让我们从探索降阶建模的基石——本征正交分解的原理开始。

## 原理与机制

本章旨在阐述降阶模型（Reduced-Order Models, ROMs）构建背后的核心原理与机制，重点关注作为现代ROMs基石的**本征正交分解**（Proper Orthogonal Decomposition, POD）方法。我们将从降维的基本概念出发，系统地推导POD，并探讨其在构建动力系统降阶模型中的应用。此外，我们还将讨论一系列高级主题与实际应用中的关键考量，包括加权内积、非齐次边界条件的处理、投影方法的选择以及非线性动力学中的稳定性问题。

### 降维引论：线性子空间与非线性流形

许多科学与工程问题涉及的系统状态可以用一个高维向量 $\mathbf{x} \in \mathbb{R}^n$ 来描述，其中 $n$ 可能非常大（例如，有限元离散化后的自由度数量）。尽管状态空间维度很高，但系统的实际动态行为通常被限制在一个低维的子结构上。降阶建模的核心思想便是识别这个低维结构，并将系统动力学投影到其上，从而以远低于原始模型的计算成本进行模拟和分析。

这个低维结构可能是线性的，也可能是非线性的。**线性降维**方法假设数据主要分布在一个低维的**线性子空间**（即一个通过原点的“平面”）附近。而**非线性降维**方法则假设数据分布在一个低维的**光滑流形**（一个局部类似于欧氏空间的弯曲空间）上。

为了理解这两种方法的区别及其适用性，我们考察两种理想化的场景 [@problem_id:3417062]。

**场景1：数据位于非线性流形上**

考虑一个二维数据集，其中数据点 $\mathbf{x}(\theta) = [\cos\theta, \sin\theta]^T$ 由参数 $\theta$ 在 $0, 2\pi)$ 上[均匀分布生成。显然，所有数据点都精确地位于 $\mathbb{R}^2$ 中的单位圆上，这是一个一维的光滑流形。如果我们选择一个最优的一维非线性模型——即单位圆本身——来表示这些数据，那么每个数据点到模型的距离都为零，重构误差的期望值为零。

然而，如果我们试图用一个一维的**线性**子空间（即一条穿过原点的直线）来逼近这些数据，情况就不同了。为了找到最优的线性子空间，我们需要进行本征正交分解（POD）。首先计算数据集的协方差矩阵 $\Sigma$。由于数据已中心化（均值为零），我们有：
$$
\Sigma = \mathbb{E}[\mathbf{x}\mathbf{x}^T] = \mathbb{E}\left[\begin{pmatrix} \cos^2\theta & \cos\theta\sin\theta \\ \cos\theta\sin\theta & \sin^2\theta \end{pmatrix}\right] = \begin{pmatrix} 1/2 & 0 \\ 0 & 1/2 \end{pmatrix}
$$
该协方差矩阵的特征值为 $\lambda_1 = \lambda_2 = 1/2$。任何一维子空间都是最优的POD子空间。选择任意一条直线（例如 $x_1$ 轴）作为我们的模型，其平均重构误差的平方等于被舍弃的特征值之和，此处为 $\lambda_2 = 1/2$。这个非零的误差源于线性模型无法捕捉数据的内在曲率。

**场景2：数据位于线性子空间上**

现在考虑一个由线性生成模型产生的数据集：$\mathbf{x} = A \mathbf{z}$，其中 $\mathbf{z} \in \mathbb{R}^p$ 是一个标准正态分布的随机向量，而 $A \in \mathbb{R}^{n \times p}$ 是一个列满秩矩阵（$p \lt n$）。这个数据集中的所有点都精确地位于由矩阵 $A$ 的列向量张成的 $p$ 维线性子空间 $\mathrm{range}(A)$ 中。

在这种情况下，一个 $p$ 维的POD模型将完美地识别出这个子空间，其重构误差为零。由于线性模型已经可以完美地表示数据，任何更复杂的 $p$ 维非线性流形模型都无法进一步减小误差。

这两个场景揭示了一个核心原则：当数据具有显著的非线性结构时，线性方法（如POD）可能是次优的；而当数据内在结构为线性时，POD则是最优且最高效的选择。在许多物理问题中，尽管存在非线性动力学，但在很大程度上，解的演化仍可被一个主导的线性子空间很好地近似。因此，POD成为了构建降阶模型最广泛和最成功的方法之一。

### 本征正交分解(POD)：最优线性子空间

POD提供了一种系统性的方法，用于从一系列高维数据（称为**快照**）中提取最优的线性子空间。

#### 优化问题

假设我们有一组 $m$ 个数据快照 $\{\mathbf{u}_k\}_{k=1}^m$，其中每个快照 $\mathbf{u}_k \in \mathbb{R}^n$ 是系统在不同时刻或不同参数下的状态。我们将这些快照排列成一个**快照矩阵** $\mathbf{X} = [\mathbf{u}_1, \mathbf{u}_2, \ldots, \mathbf{u}_m] \in \mathbb{R}^{n \times m}$。

POD的目标是寻找一个 $r$ 维的正交基 $\{\boldsymbol{\phi}_i\}_{i=1}^r$（其中 $\boldsymbol{\phi}_i^T \boldsymbol{\phi}_j = \delta_{ij}$），使得所有快照投影到这个基所张成的子空间上的平均重构误差最小。对于单个快照 $\mathbf{u}_k$，其投影为 $\mathrm{proj}(\mathbf{u}_k) = \sum_{i=1}^r (\mathbf{u}_k^T \boldsymbol{\phi}_i) \boldsymbol{\phi}_i$。我们要最小化的目标函数是：
$$
\min_{\{\boldsymbol{\phi}_i\}_{i=1}^r} \sum_{k=1}^m \|\mathbf{u}_k - \mathrm{proj}(\mathbf{u}_k)\|_2^2
$$
根据勾股定理，最小化重构误差等价于最大化投影的能量。因此，优化问题可以重述为 [@problem_id:2679843]：
$$
\max_{\{\boldsymbol{\phi}_i\}_{i=1}^r \text{ s.t. } \boldsymbol{\phi}_i^T\boldsymbol{\phi}_j=\delta_{ij}} \sum_{k=1}^m \sum_{i=1}^r (\mathbf{u}_k^T \boldsymbol{\phi}_i)^2 = \max \sum_{i=1}^r \boldsymbol{\phi}_i^T \left( \sum_{k=1}^m \mathbf{u}_k \mathbf{u}_k^T \right) \boldsymbol{\phi}_i
$$
括号中的项是空间相关性矩阵 $\mathbf{C} = \mathbf{X}\mathbf{X}^T$。

#### 通过奇异值分解(SVD)求解

上述优化问题是一个经典的瑞利商最大化问题。其解由空间相关性矩阵 $\mathbf{C} = \mathbf{X}\mathbf{X}^T$ 的前 $r$ 个（即特征值最大的）特征向量给出。这些特征向量正是我们所寻求的最优POD基 $\{\boldsymbol{\phi}_i\}_{i=1}^r$。

在实践中，直接计算和分解巨大的 $n \times n$ 矩阵 $\mathbf{C}$ 可能成本高昂。一种更高效且数值稳定的方法是利用**奇异值分解**（Singular Value Decomposition, SVD）。快照矩阵 $\mathbf{X}$ 的SVD形式为：
$$
\mathbf{X} = \mathbf{U} \mathbf{\Sigma} \mathbf{V}^T
$$
其中：
- $\mathbf{U} \in \mathbb{R}^{n \times n}$ 是一个正交矩阵，其列向量 $\{\mathbf{u}_i\}$ 称为**左奇异向量**。
- $\mathbf{V} \in \mathbb{R}^{m \times m}$ 是一个正交矩阵，其列向量 $\{\mathbf{v}_i\}$ 称为**右奇异向量**。
- $\mathbf{\Sigma} \in \mathbb{R}^{n \times m}$ 是一个对角矩阵，其对角线上的元素 $\sigma_1 \ge \sigma_2 \ge \dots \ge 0$ 称为**奇异值**。

将SVD代入空间相关性矩阵 $\mathbf{C}$ 的表达式中，我们发现：
$$
\mathbf{C} = \mathbf{X}\mathbf{X}^T = (\mathbf{U}\mathbf{\Sigma}\mathbf{V}^T)(\mathbf{U}\mathbf{\Sigma}\mathbf{V}^T)^T = \mathbf{U}(\mathbf{\Sigma}\mathbf{\Sigma}^T)\mathbf{U}^T
$$
这正是 $\mathbf{C}$ 的特征值分解形式。因此，最优的POD基向量（即 $\mathbf{C}$ 的特征向量）就是快照矩阵 $\mathbf{X}$ 的**左奇异向量**（即 $\mathbf{U}$ 的列）。我们选择 $\mathbf{U}$ 的前 $r$ 列作为我们的 $r$ 维POD基。

SVD的各个组成部分在ROM中具有明确的物理解释 [@problem_id:2679843]：
- **左奇异向量** $\mathbf{U}$ 的列构成了最优的空间基函数，称为**POD模式**。
- **奇异值** $\mathbf{\Sigma}$ 的对角元素 $\sigma_i$ 量化了每个POD模式的重要性。$\sigma_i^2$ 正比于第 $i$ 个模式在快照集合中捕获的**能量**或**方差**。
- **右奇异向量** $\mathbf{V}$ 的列与时间演化相关。通过投影 $\mathbf{U}^T \mathbf{X} = \mathbf{\Sigma}\mathbf{V}^T$，我们可以看到，每个快照的模态系数（即时间依赖的振幅）是由 $\mathbf{\Sigma}\mathbf{V}^T$ 的列给出的，而非仅仅是 $\mathbf{V}^T$。

#### 能量、方差与截断

POD的一个核心优势是它提供了一种基于能量的层次化表示。快照集的总能量（或方差），以平方Frobenius范数度量，等于所有奇异值的平方和 [@problem_id:3417047]：
$$
\|\mathbf{X}\|_F^2 = \sum_{i,j} X_{ij}^2 = \mathrm{tr}(\mathbf{X}^T\mathbf{X}) = \sum_{i=1}^{\min(n,m)} \sigma_i^2
$$
由前 $r$ 个POD模式捕获的能量为 $\sum_{i=1}^r \sigma_i^2$。因此，由 $r$ 维POD子空间捕获的能量分数由下式给出：
$$
\mathcal{E}(r) = \frac{\sum_{i=1}^r \sigma_i^2}{\sum_{i=1}^{\min(n,m)} \sigma_i^2}
$$
这个公式为选择ROM的维度 $r$ 提供了一个自然的、基于物理的准则。我们可以预设一个能量捕获阈值 $\tau$（例如 $\tau = 0.999$），然后选择满足 $\mathcal{E}(r) \ge \tau$ 的最小整数 $r$。

例如，假设一个系统的奇异值谱为 $\{50, 20, 10, 5, 2, 1, \dots\}$。总能量是所有奇异值平方的总和 $50^2 + 20^2 + 10^2 + 5^2 + \dots = 2500 + 400 + 100 + 25 + \dots = 3025 + \dots$。如果我们希望捕获至少 $99.5\%$ 的能量，我们需要计算累积能量。假设总能量为 $3030.3$，目标能量为 $0.995 \times 3030.3 \approx 3015.15$。
- $r=1$: 能量 $= 2500$
- $r=2$: 能量 $= 2500 + 400 = 2900$
- $r=3$: 能量 $= 2900 + 100 = 3000$
- $r=4$: 能量 $= 3000 + 25 = 3025$
由于 $3025 > 3015.15$，我们选择的最小维度是 $r=4$ [@problem_id:3417047]。

#### 压缩的优势

POD不仅提供了最优的基，还带来了显著的数据压缩效益，这是ROMs的一个主要动机。存储完整的快照矩阵 $U \in \mathbb{R}^{N \times K}$ 需要的内存与 $N \times K$ 成正比。而存储一个 $r$ 维的ROM，我们需要存储基矩阵 $\Phi \in \mathbb{R}^{N \times r}$ 和系数矩阵 $A \in \mathbb{R}^{r \times K}$。所需的内存与 $N \times r + r \times K = r(N+K)$ 成正比。

当 $r \ll N$ 且 $r \ll K$ 时，这种节省是巨大的。分数内存缩减 $\rho$ 可以表示为 [@problem_id:3265878]：
$$
\rho = 1 - \frac{\text{ROM内存}}{\text{快照内存}} = 1 - \frac{r(N+K)}{NK} = 1 - r\left(\frac{1}{K} + \frac{1}{N}\right)
$$
例如，对于一个具有 $N=20000$ 个空间点和 $K=500$ 个时间步的模拟，若我们构建一个 $r=50$ 的ROM，内存缩减率约为 $\rho = 1 - 50(\frac{1}{500} + \frac{1}{20000}) \approx 0.8975$，即节省了近 $90\%$ 的存储空间。

### 基于POD构建降阶模型(ROM)

拥有了最优基 $\{\boldsymbol{\phi}_i\}_{i=1}^r$ 之后，下一步是确定这些基的系数 $a_i(t)$ 如何随时间演化。这通过将原始系统的控制方程投影到POD子空间上来实现。

#### Galerkin投影

假设原始系统的控制方程（例如，一个偏微分方程的半离散化形式）可以写成：
$$
\frac{d\mathbf{u}}{dt} = \mathcal{F}(\mathbf{u}, t)
$$
我们用POD展开式 $\mathbf{u}(t) \approx \mathbf{u}_r(t) = \sum_{j=1}^r a_j(t)\boldsymbol{\phi}_j$ 来近似解 $\mathbf{u}(t)$。将此近似代入方程，会产生一个**残差** $\mathcal{R}(\mathbf{u}_r) = \frac{d\mathbf{u}_r}{dt} - \mathcal{F}(\mathbf{u}_r, t)$，它通常不为零。

**Galerkin投影**的核心思想是要求这个残差与降阶子空间中的所有基函数**正交** [@problem_id:2432068]。即，对于每个 $i=1, \dots, r$：
$$
\langle \mathcal{R}(\mathbf{u}_r), \boldsymbol{\phi}_i \rangle = 0
$$
这里的 $\langle \cdot, \cdot \rangle$ 是一个适当选择的内积（通常是标准的欧氏内积）。这个正交性条件背后的根本原因在于，它是在降阶子空间 $V_r = \mathrm{span}\{\boldsymbol{\phi}_1, \dots, \boldsymbol{\phi}_r\}$ 上强制执行原始方程的**弱形式**。如果原始方程的弱形式是 $\langle \frac{d\mathbf{u}}{dt}, \mathbf{v} \rangle = \langle \mathcal{F}(\mathbf{u},t), \mathbf{v} \rangle$ 对所有测试函数 $\mathbf{v}$ 成立，那么Galerkin方法就是要求这个等式对所有在子空间 $V_r$ 内的测试函数成立。

施加这个条件会产生一个关于系数 $\mathbf{a}(t)=[a_1(t), \dots, a_r(t)]^T$ 的 $r$ 维常微分方程组（ODE），其形式通常为：
$$
\mathbf{M}_r \frac{d\mathbf{a}}{dt} = \mathbf{F}_r(\mathbf{a}, t)
$$
其中 $\mathbf{M}_r$ 是降阶质量矩阵，$\mathbf{F}_r$ 是降阶后的算子。这个ODE系统就是我们的降阶模型，其维度 $r$ 远小于原始系统的维度 $n$。对于对称正定问题，Galerkin投影不仅提供了封闭的系数方程，还被证明能在能量范数下给出最优的近似解。

#### 投影的示例解析

让我们通过一个具体的例子来理解Galerkin投影的计算过程 [@problem_id:2432132]。假设我们的向量空间是 $\mathbb{R}^3$，并赋予了一个由对称正定矩阵 $M$ 定义的加权内积 $\langle \mathbf{u}, \mathbf{w} \rangle_M = \mathbf{u}^T M \mathbf{w}$。
$$
M = \begin{pmatrix} 2 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 3 \end{pmatrix}, \quad \boldsymbol{\phi}_1 = \begin{pmatrix} 1 \\ 2 \\ 0 \end{pmatrix}, \quad \boldsymbol{\phi}_2 = \begin{pmatrix} 0 \\ 1 \\ 2 \end{pmatrix}
$$
我们要将一个全阶状态向量 $\mathbf{x} = [3, -2, 4]^T$ 投影到这个子空间上。投影后的向量 $\widehat{\mathbf{x}} \in \mathcal{U}$ 可以写成 $\widehat{\mathbf{x}} = c_1 \boldsymbol{\phi}_1 + c_2 \boldsymbol{\phi}_2$。Galerkin投影的定义要求误差向量 $\mathbf{x} - \widehat{\mathbf{x}}$ 与子空间 $\mathcal{U}$ 中的所有向量（即与基向量 $\boldsymbol{\phi}_1$ 和 $\boldsymbol{\phi}_2$）在 $M$-内积下正交。
这给出了一个关于系数 $c_1, c_2$ 的 $2 \times 2$ 线性方程组（格拉姆系统）：
$$
\begin{pmatrix}
\langle \boldsymbol{\phi}_1, \boldsymbol{\phi}_1 \rangle_M & \langle \boldsymbol{\phi}_1, \boldsymbol{\phi}_2 \rangle_M \\
\langle \boldsymbol{\phi}_2, \boldsymbol{\phi}_1 \rangle_M & \langle \boldsymbol{\phi}_2, \boldsymbol{\phi}_2 \rangle_M
\end{pmatrix}
\begin{pmatrix} c_1 \\ c_2 \end{pmatrix}
=
\begin{pmatrix}
\langle \mathbf{x}, \boldsymbol{\phi}_1 \rangle_M \\
\langle \mathbf{x}, \boldsymbol{\phi}_2 \rangle_M
\end{pmatrix}
$$
通过计算所有必要的 $M$-内积，例如 $\langle \boldsymbol{\phi}_1, \boldsymbol{\phi}_1 \rangle_M = \boldsymbol{\phi}_1^T M \boldsymbol{\phi}_1 = 6$ 以及 $\langle \mathbf{x}, \boldsymbol{\phi}_1 \rangle_M = \mathbf{x}^T M \boldsymbol{\phi}_1 = 2$，我们可以建立并求解这个系统，得到系数 $c_1 = -9/37$ 和 $c_2 = 64/37$。最终的投影向量为：
$$
\widehat{\mathbf{x}} = -\frac{9}{37}\boldsymbol{\phi}_1 + \frac{64}{37}\boldsymbol{\phi}_2 = \begin{pmatrix} -9/37 \\ 46/37 \\ 128/37 \end{pmatrix}
$$
这个过程精确地展示了如何通过求解一个小的线性系统来计算投影系数，这是构建ROM动力学方程的核心步骤。

### 高级主题与实践考量

标准的POD-Galerkin框架在许多应用中非常有效，但解决更复杂的问题通常需要一些扩展和改进。

#### 内积的角色：加权POD

到目前为止，我们默认使用了标准的欧氏内积。然而，物理系统的“能量”或重要性度量往往与特定的范数相关。例如，在结构力学或流体动力学中，动能由质量矩阵 $\mathbf{M}$ 定义，即 $E_{kin} = \frac{1}{2} \mathbf{u}^T \mathbf{M} \mathbf{u} = \frac{1}{2}\|\mathbf{u}\|_M^2$。

如果我们希望我们的ROM基能最优地捕获这种物理能量，而不是欧氏范数下的方差，我们就需要使用由 $\mathbf{M}$ 定义的加权内积来执行POD [@problem_id:2679843] [@problem_id:3417054]。这可以通过对一个加权的快照矩阵进行标准SVD来实现。具体来说，如果我们想在 $\mathbf{M}$-范数下优化，我们可以对 $\mathbf{M}^{1/2}\mathbf{X}$ 进行SVD，其中 $\mathbf{M}^{1/2}$ 是 $\mathbf{M}$ 的矩阵平方根。如果 $\mathbf{M}^{1/2}\mathbf{X} = \tilde{\mathbf{U}}\tilde{\mathbf{\Sigma}}\tilde{\mathbf{V}}^T$，那么最优的 $\mathbf{M}$-正交基由 $\mathbf{\Phi} = \mathbf{M}^{-1/2}\tilde{\mathbf{U}}_r$ 给出。

选择正确的内积至关重要。例如，在一个数据同化问题中，如果背景误差协方差的逆 $B^{-1}$ 与质量矩阵 $M$ 成正比（即 $B^{-1} = \alpha M$），这意味着先验不确定性是以物理能量范数来度量的。在这种情况下，使用 $\mathbf{M}$-加权的POD来生成基，可以确保ROM最能代表那些在物理和统计上都最重要的动态模式，从而提高数据同化系统的稳定性和准确性 [@problem_id:3417054]。

通常，欧氏POD和加权POD会产生不同的基。只有当加权矩阵是单位矩阵的标量倍（$M=cI$）时，两者才会生成相同的子空间 [@problem_id:3417054]。

#### 处理非齐次边界条件

标准的POD-Galerkin方法要求基函数满足齐次（零）边界条件。当原始问题具有非齐次（非零）边界条件时，例如 $u(\mathbf{x},t) = g(\mathbf{x},t)$ 在边界上，我们需要一个预处理步骤 [@problem_id:3417040]。

常用的方法是**提升函数法**（lifting function method）。我们将解 $u$ 分解为两部分：
$$
u(\mathbf{x},t) = v(\mathbf{x},t) + w(\mathbf{x},t)
$$
其中 $w(\mathbf{x},t)$ 是一个“提升函数”，它满足原始的非齐次边界条件，即 $w = g$ 在边界上。而 $v(\mathbf{x},t)$ 是一个新的待求解场，它现在满足齐次边界条件 $v=0$。

我们将这个分解代入原始的控制方程（例如，$\partial_t u = \mathcal{L}u + s$），得到一个关于 $v$ 的新方程：
$$
\partial_t v = \mathcal{L}v + \left( s + \mathcal{L}w - \partial_t w \right)
$$
注意，提升函数 $w$ 及其导数现在变成了新的源项。现在，我们可以对满足齐次边界条件的场 $v$ 应用标准的POD-Galerkin流程：
1.  从全阶模拟中收集 $u$ 的快照，并减去相应的提升函数 $w$ 得到 $v$ 的快照。
2.  对 $v$ 的快照进行POD，得到一组满足齐次边界条件的基函数 $\{\boldsymbol{\phi}_i\}$。
3.  将 $v$ 的新控制方程投影到POD基上，得到关于其系数 $\mathbf{a}(t)$ 的ROM。降阶算子 $A_{ij} = \langle \boldsymbol{\phi}_i, \mathcal{L}\boldsymbol{\phi}_j \rangle$ 不受提升函数影响，但降阶源项 $b_i$ 会包含来自 $s, \mathcal{L}w, \partial_t w$ 的贡献 [@problem_id:3417040]。
4.  求解ROM得到 $\mathbf{a}(t)$，然后重构近似解 $v_r(t) = \sum a_i(t)\boldsymbol{\phi}_i$。
5.  最后，通过加上提升函数来获得满足原始非齐次边界条件的最终解：$u_r(t) = v_r(t) + w(t)$。

#### 投影方法的变体：Galerkin与Petrov-Galerkin

Galerkin投影要求残差与**试验空间**（trial space，即POD基张成的空间）正交。这是一个自然的选择，但并非唯一。更广泛的**Petrov-Galerkin**方法允许**测试空间**（test space）与试验空间不同。

一个重要的Petrov-Galerkin变体是**最小二乘Petrov-Galerkin**（Least-Squares Petrov-Galerkin, LSPG）方法 [@problem_id:3417077]。对于一个离散时间演化方程 $x_{k+1} = A x_k$，LSPG-ROM在每一步都寻找能最小化下一步状态残差的模态系数 $a_{k+1}$。具体来说，它求解：
$$
a_{k+1} = \arg\min_{z \in \mathbb{R}^r} \| U_r z - A U_r a_k \|_M^2
$$
其中 $U_r$ 是POD基矩阵，$M$ 是一个SPD权重矩阵。这会导出一个不同于标准Galerkin的降阶演化算子。

- **Galerkin ROM算子**: $A_r^{\mathrm{G}} = U_r^T A U_r$ (假设 $U_r^T U_r = I_r$)
- **LSPG ROM算子**: $A_r^{\mathrm{LSPG}} = (U_r^T M U_r)^{-1} (U_r^T M A U_r)$

这两种方法在特定条件下是等价的。例如，当LSPG中的权重矩阵 $M$ 是单位矩阵时，LSPG就退化为标准Galerkin方法 [@problem_id:3417077]。另一个重要的等价条件是，当POD子空间对于全阶算子 $A$ 是**不变的**（即 $A$ 将该子空间映射到其自身，满足 $A U_r = U_r B$）。在这种情况下，无论权重矩阵 $M$ 如何选择，LSPG和Galerkin都会产生完全相同的降阶动力学 [@problem_id:3417077]。然而，在一般情况下，这两种方法会产生不同的ROM，从而在数据同化等应用中可能导致不同的结果。

#### 非线性动力学中的挑战：稳定性与闭合

当将POD-Galerkin方法应用于具有强非线性的系统，如流体动力学中的Navier-Stokes方程时，一个严重的问题是模型的**长期不稳定性**。这通常表现为能量的无界增长，即所谓的**能量漂移**（energy drift）[@problem_id:3417043]。

这种不稳定性的根源在于截断。在完整的物理系统中（如湍流），能量通过非线性相互作用从大尺度（能量注入尺度）级联到小尺度（耗散尺度）。这是一个保持总能量守恒（在无粘、无外力情况下）但将能量重新分配的过程。标准的Galerkin ROM只考虑了POD基内部的（resolved-resolved）相互作用，这些相互作用同样是保能的。然而，它完全忽略了从已解析尺度到被截断的未解析尺度之间的能量传递。由于这个物理上存在的能量流出通道在模型中被切断，能量会在已解析的模式中不切实际地累积，最终导致模型发散。

为了解决这个问题，需要引入**闭合模型**（closure model）。闭合模型的目标是模拟被截断模式对已解析模式的平均影响，特别是它们所造成的能量耗散。一种常见的方法是**涡粘性模型**（eddy-viscosity model），它在ROM方程中增加一个额外的耗散项，形式通常为 $-\nu_e(t) D \mathbf{a}(t)$，其中 $\nu_e$ 是“涡粘性系数”，$D$ 是一个对称半正定的耗散矩阵。

闭合项的参数（如 $\nu_e$）通常是未知的，需要进行标定。在数据驱动的背景下，我们可以利用可用的数据来动态调整这些参数。例如，我们可以计算由数据揭示的“真实”能量变化率 $R^{\text{data}}$，并将其与未闭合ROM预测的能量变化率 $R(t)$ 进行比较。然后，我们可以选择 $\nu_e(t)$ 以弥合这一差距，即求解 [@problem_id:3417043]：
$$
\nu_e(t) = \frac{R(t) - R^{\text{data}}(t)}{\mathbf{a}(t)^T D \mathbf{a}(t)}
$$
这种方法确保了ROM在能量上与观测数据保持一致，从而显著提高了其长期稳定性和物理保真度。