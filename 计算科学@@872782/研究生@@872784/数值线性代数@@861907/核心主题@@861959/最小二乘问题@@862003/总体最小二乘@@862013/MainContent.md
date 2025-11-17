## 引言

在线性[数据拟合](@entry_id:149007)中，求解形如 $A\boldsymbol{x} \approx \boldsymbol{b}$ 的超定线性方程组是一个基本而普遍的问题。传统上，[普通最小二乘法](@entry_id:137121)（Ordinary Least Squares, OLS）是解决此类问题的首选方法，它通过最小化残差的欧几里得范数 $\min \|A\boldsymbol{x} - \boldsymbol{b}\|_2^2$ 来寻找最优解。然而，OLS的一个核心假设是数据矩阵 $A$（即[自变量](@entry_id:267118)）是精确无误的，所有测量误差都集中在观测向量 $\boldsymbol{b}$（即因变量）上。在物理、工程、生物和经济学等众多科学领域中，这一假设往往过于理想化。

当[自变量](@entry_id:267118)和因变量都不可避免地受到测量噪声污染时，我们面对的是一个更具挑战性的“变量含误差”（Errors-in-Variables, EIV）模型。在此类情景下，使用OLS会导致系统性的估计偏差，即所谓的“[衰减偏误](@entry_id:746571)”，使得估计出的系数[向量的范数](@entry_id:154882)系统性地小于其真实值。为了克服这一根本性缺陷，总体最小二乘（Total Least Squares, TLS）应运而生。TLS承认所有变量中都存在误差，其目标不再是最小化垂直方向的残差，而是最小化数据点到拟合超平面的正交距离，从而提供了一种在统计上更为稳健和无偏的估计方法。

本文旨在系统地介绍总体最小二乘法的理论、应用与实践。我们将从以下三个层面展开：
*   **原理与机制**：首先，我们将深入剖析TLS的数学基础，阐明其与OLS的根本区别，并详细介绍基于奇异值分解（SVD）的核心求解机制及其深刻的几何意义。
*   **应用与跨学科联系**：接着，我们将展示TLS在变量含误差回归、几何拟合、系统辨识等多个领域的广泛应用，并探讨其与主成分分析（PCA）、[核方法](@entry_id:276706)等其他关键理论的内在联系。
*   **动手实践**：最后，通过一系列精心设计的编程练习，您将有机会亲手实现TLS算法，从而将理论知识转化为解决实际问题的能力。

通过本文的学习，您将不仅掌握TLS的基本原理和计算方法，更能深刻理解其在处理含噪数据时的独特优势，并将其应用于您的研究和工程实践中。

## 原理与机制

总最小二乘（Total Least Squares, TLS）是处理线性方程组 $A\boldsymbol{x} \approx \boldsymbol{b}$ 的一种稳健方法，尤其适用于数据矩阵 $A$ 和观测向量 $\boldsymbol{b}$ 都存在测量误差的情况。本节将深入探讨 TLS 的核心原理与机制，从其与普通最小二乘（Ordinary Least Squares, OLS）的根本区别出发，建立其数学模型，阐明基于[奇异值分解](@entry_id:138057)（SVD）的求解方法，并探讨其几何意义与实际应用中的关键考量。

### 从普通最小二乘到[变量含误差模型](@entry_id:186401)

我们首先回顾经典的**普通最小二乘（Ordinary Least Squares, OLS）**方法。OLS 旨在解决模型 $A\boldsymbol{x} = \boldsymbol{b} + \boldsymbol{\varepsilon}$，其中所有的[测量误差](@entry_id:270998)都归于观测向量 $\boldsymbol{b}$。因此，OLS 的目标是寻找一个解 $\boldsymbol{x}_{\mathrm{LS}}$，使得[残差向量](@entry_id:165091) $\boldsymbol{r} = A\boldsymbol{x} - \boldsymbol{b}$ 的欧几里得范数最小化：

$$
\min_{\boldsymbol{x}} \|\boldsymbol{r}\|_2^2 = \min_{\boldsymbol{x}} \|A\boldsymbol{x} - \boldsymbol{b}\|_2^2
$$

从几何上看，OLS 的解是将向量 $\boldsymbol{b}$ 正交投影到由矩阵 $A$ 的列向量张成的[子空间](@entry_id:150286) $\mathcal{R}(A)$ 上。这个投影点即为 $A\boldsymbol{x}_{\mathrm{LS}}$。这意味着 OLS 最小化的是数据点 $(a_i, b_i)$ 到拟合超平面在 **垂直方向** 上的距离平方和，其中 $a_i$ 是 $A$ 的行向量，即假设所有 $a_i$ 都是精确无误的 [@problem_id:1362205]。这个假设在许多科学和工程应用中并不成立。

当数据矩阵 $A$ 和观测向量 $\boldsymbol{b}$ 都受到[噪声污染](@entry_id:188797)时，我们面临的是一个所谓的**变量含误差（Errors-in-Variables, EIV）**模型。在这种情境下，真实的（但未知的）无噪声数据 $A_{\star}$ 和 $\boldsymbol{b}_{\star}$ 之间存在一个精确的[线性关系](@entry_id:267880) $A_{\star}\boldsymbol{x}_{\star} = \boldsymbol{b}_{\star}$。我们观测到的是它们的含噪版本 $A = A_{\star} + E$ 和 $\boldsymbol{b} = \boldsymbol{b}_{\star} + \boldsymbol{e}$，其中 $E$ 和 $\boldsymbol{e}$ 是[测量误差](@entry_id:270998)。

如果在 EIV 模型中仍然使用 OLS，会导致系统性的估计偏差。具体而言，当 $A$ 中的误差与 $A_{\star}$ 无关且期望为零时，OLS 估计量 $\boldsymbol{x}_{\mathrm{LS}}$ 会表现出**[衰减偏误](@entry_id:746571)（attenuation bias）**。也就是说，在大样本极限下，估计出的系数[向量的范数](@entry_id:154882)会系统性地小于真实系数向量 $\boldsymbol{x}_{\star}$ 的范数，即估计值会朝零点“收缩”[@problem_id:3590963]。例如，在一个简单的标量模型 $b_i \approx x a_i$ 中，若 $a_i$ 含有零均值误差，OLS 估计量 $x_{\mathrm{OLS}} = \frac{\sum a_i b_i}{\sum a_i^2}$ 在概率上收敛于 $x_{\star} \frac{\mathrm{Var}(a_{\star})}{\mathrm{Var}(a_{\star}) + \mathrm{Var}(e_a)}$，其中 $e_a$ 是 $a$ 中的误差。这个因子总是小于1，从而导致了对 $x_{\star}$ 的低估。

为了克服这一问题，我们需要一种能够同时考虑 $A$ 和 $\boldsymbol{b}$ 中误差的方法。**总最小二乘（Total Least Squares, TLS）**正是为此而生。与 OLS 最小化垂直误差不同，TLS 的几何目标是最小化每个数据点到拟合超平面的**正交距离（perpendicular distance）**的平方和 [@problem_id:1362205] [@problem_id:3234673]。这种方法隐含地假设 $A$ 和 $\boldsymbol{b}$ 中的误差是同性的，即在所有维度上的[测量误差](@entry_id:270998)具有相似的统计特性。

### 总[最小二乘问题](@entry_id:164198)的数学表述

总[最小二乘问题](@entry_id:164198)的核心思想是：寻找对原始数据矩阵 $A$ 和向量 $\boldsymbol{b}$ 的最小扰动 $(\Delta A, \Delta \boldsymbol{b})$，使得被扰动后的系统 $(A+\Delta A)\boldsymbol{x} = \boldsymbol{b}+\Delta \boldsymbol{b}$ 变得相容（即有解）。“最小扰动”通常通过**[弗罗贝尼乌斯范数](@entry_id:143384)（Frobenius norm）**来量化。

形式上，给定 $A \in \mathbb{R}^{m \times n}$ 和 $\boldsymbol{b} \in \mathbb{R}^{m}$，TLS 问题被表述为一个约束优化问题：

$$
\min_{\Delta A, \Delta \boldsymbol{b}, \boldsymbol{x}} \|[\Delta A \ \ \Delta \boldsymbol{b}]\|_F^2 \quad \text{subject to} \quad (A+\Delta A)\boldsymbol{x} = \boldsymbol{b}+\Delta \boldsymbol{b}
$$

其中 $[\Delta A \ \ \Delta \boldsymbol{b}] \in \mathbb{R}^{m \times (n+1)}$ 是由 $\Delta A$ 和 $\Delta \boldsymbol{b}$ 水平拼接而成的增广扰动矩阵。

选择[弗罗贝尼乌斯范数](@entry_id:143384)作为[目标函数](@entry_id:267263)并非随意的，它有深刻的统计和几何依据 [@problem_id:3599768]：

1.  **与最大似然估计的联系**：如果我们假设[增广矩阵](@entry_id:150523) $[A \ \ \boldsymbol{b}]$ 的所有 $m \times (n+1)$ 个元素的测量误差是[独立同分布](@entry_id:169067)（i.i.d.）的零均值高斯[随机变量](@entry_id:195330)，且[方差](@entry_id:200758)均为 $\sigma^2$，那么求解该 EIV 模型的**[最大似然估计](@entry_id:142509)（Maximum Likelihood Estimator, MLE）**等价于最小化负[对数似然函数](@entry_id:168593)。这个负[对数似然函数](@entry_id:168593)正比于 $\|[\Delta A \ \ \Delta \boldsymbol{b}]\|_F^2$。因此，TLS 在这种[标准误差](@entry_id:635378)假设下是最优的[统计估计](@entry_id:270031)方法 [@problem_id:3599768, A]。

2.  **[几何不变性](@entry_id:637068)**：一个理想的度量方法应该对[坐标系](@entry_id:156346)的旋转不敏感。[弗罗贝尼乌斯范数](@entry_id:143384)具有**[酉不变性](@entry_id:198984)（unitarily invariant）**，特别是对左乘一个[正交矩阵](@entry_id:169220) $Q$ 保持不变，即 $\|Q M\|_F = \|M\|_F$。这意味着，如果我们对测量空间（$\mathbb{R}^m$）进行旋转或反射，扰动的“大小”度量不会改变。这一要求，结合误差各向同性的假设，自然地导向了[弗罗贝尼乌斯范数](@entry_id:143384) [@problem_id:3599768, B]。

3.  **作为广义模型的特例**：如果误差不是各向同性的，例如，不同变量的测量误差具有不同的[方差](@entry_id:200758)或相关性，其[协方差矩阵](@entry_id:139155)为 $\Sigma$，则更一般的 MLE [目标函数](@entry_id:267263)是最小化一个加权范数，即[马氏距离](@entry_id:269828)的平方 $\| \Sigma^{-1/2} \mathrm{vec}([\Delta A \ \ \Delta \boldsymbol{b}]) \|_2^2$。标准的 TLS [目标函数](@entry_id:267263)可以看作是当[误差协方差](@entry_id:194780)为 $\Sigma = \sigma^2 I$ 时的特例 [@problem_id:3599768, D]。例如，若 $A$ 中各元素的[误差方差](@entry_id:636041)为 $\sigma_A^2$，$\boldsymbol{b}$ 中各元素的[误差方差](@entry_id:636041)为 $\sigma_{\boldsymbol{b}}^2$，则恰当的目标函数是最小化 $\frac{\|\Delta A\|_F^2}{\sigma_A^2} + \frac{\|\Delta \boldsymbol{b}\|_2^2}{\sigma_{\boldsymbol{b}}^2}$。只有当 $\sigma_A^2 = \sigma_{\boldsymbol{b}}^2$ 时，这才会简化为标准的 TLS 目标函数 [@problem_id:3599768, F]。

值得注意的是，TLS 并不具备**[尺度不变性](@entry_id:180291)**。如果将矩阵 $A$ 的某一列乘以一个常数（例如，改变物理单位），TLS 的解通常会发生改变。因此，在应用 TLS 之前，对数据进行适当的[预处理](@entry_id:141204)和标准化是至关重要的实践步骤 [@problem_id:3599768, E]。

### 基于奇异值分解的求解机制

TLS 问题的求解与矩阵的低秩逼近理论密切相关。约束条件 $(A+\Delta A)\boldsymbol{x} = \boldsymbol{b}+\Delta \boldsymbol{b}$ 可以重写为一个齐次方程：

$$
[A+\Delta A \ \ \boldsymbol{b}+\Delta \boldsymbol{b}] \begin{pmatrix} \boldsymbol{x} \\ -1 \end{pmatrix} = \boldsymbol{0}
$$

令[增广矩阵](@entry_id:150523) $C = [A \ \ \boldsymbol{b}]$ 和增广扰动 $\Delta C = [\Delta A \ \ \Delta \boldsymbol{b}]$，上述条件意味着矩阵 $C+\Delta C$ 是[秩亏](@entry_id:754065)的，因为它存在一个非零的零空间向量 $\begin{pmatrix} \boldsymbol{x} \\ -1 \end{pmatrix}$。因此，TLS 问题等价于：在所有使 $C+\Delta C$ [秩亏](@entry_id:754065)的扰动 $\Delta C$ 中，寻找一个具有最小[弗罗贝尼乌斯范数](@entry_id:143384)的扰动 [@problem_id:3583050] [@problem_id:3592284]。

这个问题的答案由 **Eckart-Young-Mirsky 定理** 给出。该定理指出，对于一个矩阵 $C$，其在[弗罗贝尼乌斯范数](@entry_id:143384)意义下的最佳 $k$ 秩逼近，是通过其**奇异值分解（Singular Value Decomposition, SVD）**将最小的那些奇异值置零得到的。在我们的场景中，$C \in \mathbb{R}^{m \times (n+1)}$ 通常是满秩的（秩为 $n+1$）。要使其[秩亏](@entry_id:754065)（秩最多为 $n$），我们需要找到最佳的秩 $n$ 逼近。

设 $C$ 的 SVD 为 $C = U\Sigma V^T$，其中[奇异值](@entry_id:152907)按降序[排列](@entry_id:136432) $\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_{n+1} > 0$。最小的扰动 $\Delta C$ 是 $\Delta C = -\sigma_{n+1}\boldsymbol{u}_{n+1}\boldsymbol{v}_{n+1}^T$，其中 $\boldsymbol{u}_{n+1}$ 和 $\boldsymbol{v}_{n+1}$ 分别是对应于最小奇异值 $\sigma_{n+1}$ 的左、[右奇异向量](@entry_id:754365)。这个扰动的范数是 $\|\Delta C\|_F = \sigma_{n+1}$。

被扰动后的矩阵 $C' = C + \Delta C$ 的零空间由向量 $\boldsymbol{v}_{n+1}$ 张成。因此，我们必须有：

$$
\begin{pmatrix} \boldsymbol{x}_{\mathrm{TLS}} \\ -1 \end{pmatrix} = k \cdot \boldsymbol{v}_{n+1}
$$

对于某个非零标量 $k$。将[右奇异向量](@entry_id:754365) $\boldsymbol{v}_{n+1} \in \mathbb{R}^{n+1}$ 分块为 $\boldsymbol{v}_{n+1} = \begin{pmatrix} \hat{\boldsymbol{v}} \\ v_b \end{pmatrix}$，其中 $\hat{\boldsymbol{v}} \in \mathbb{R}^n$ 是前 $n$ 个分量，$v_b \in \mathbb{R}$ 是最后一个分量。通过比较向量的最后分量，我们得到 $-1 = k \cdot v_b$。

只要 $v_b \neq 0$（这是有唯一有限解的条件），我们就可以解出 $k = -1/v_b$。代入前 $n$ 个分量，我们得到 TLS 解：

$$
\boldsymbol{x}_{\mathrm{TLS}} = -\frac{1}{v_b}\hat{\boldsymbol{v}}
$$

这个公式构成了 TLS 的核心计算机制 [@problem_id:2203385] [@problem_id:3583050, A]。它明确地将 TLS 解与[增广矩阵](@entry_id:150523) $[A \ \ \boldsymbol{b}]$ 的整体结构（通过其 SVD）联系起来，这与 OLS 解 $\boldsymbol{x}_{\mathrm{LS}} = A^+\boldsymbol{b}$ 形成了鲜明对比，后者仅依赖于 $A$ 的[伪逆](@entry_id:140762)作用于 $\boldsymbol{b}$ [@problem_id:3592284, A, D]。

在特殊情况下，即当原始系统 $A\boldsymbol{x} \approx \boldsymbol{b}$ 无需扰动就相容时（即 $\boldsymbol{b} \in \mathcal{R}(A)$），最小扰动为零，$\sigma_{n+1}=0$。此时，OLS 和 TLS 的解是相同的，都等于精确解 $A^+\boldsymbol{b}$ [@problem_id:3592284, E]。

如果出现 $v_b=0$ 的退化情况，这意味着向量 $\boldsymbol{v}_{n+1}$ 的最后一个分量为零。此时，无法通过缩放 $\boldsymbol{v}_{n+1}$ 使其最后一个分量为 $-1$，因此 TLS 问题没有有限解。这种情况在几何上对应于最佳拟合[超平面](@entry_id:268044)“垂直”于某些自变量坐标轴的情况。此时，最小的[秩亏](@entry_id:754065)扰动仅作用于矩阵 $A$，即 $\Delta \boldsymbol{b} = \boldsymbol{0}$ [@problem_id:3583050, D]。

### 几何解释：[正交回归](@entry_id:753009)

TLS 的求解过程虽然是代数的，但其几何意义却非常直观。它等价于**[正交回归](@entry_id:753009)（Orthogonal Regression）**，即寻找一个 $n$ 维空间中的超平面，使得数据点到该超平面的正交距离的平方和最小。

对于一个由[单位法向量](@entry_id:178851) $\boldsymbol{n}$ 和标量 $d$ 定义的[超平面](@entry_id:268044) $\boldsymbol{n}^T\boldsymbol{z} + d = 0$，一个点 $\boldsymbol{z}_i$ 到它的正交距离的平方是 $(\boldsymbol{n}^T\boldsymbol{z}_i + d)^2$。如果我们有一组数据点 $\{\boldsymbol{z}_i\}_{i=1}^m \subset \mathbb{R}^{n+1}$，TLS 的目标是最小化 $\sum_{i=1}^m (\boldsymbol{n}^T\boldsymbol{z}_i + d)^2$，约束条件是 $\|\boldsymbol{n}\|=1$。

可以证明，最优的[超平面](@entry_id:268044)必须穿过数据点的**质心（centroid）** $\boldsymbol{\mu} = \frac{1}{m}\sum \boldsymbol{z}_i$。这意味着我们可以先对数据进行中心化，即考虑 $\boldsymbol{y}_i = \boldsymbol{z}_i - \boldsymbol{\mu}$，然后寻找一个穿过原点的[超平面](@entry_id:268044) $\boldsymbol{n}^T\boldsymbol{y}=0$ 来最小化 $\sum (\boldsymbol{n}^T\boldsymbol{y}_i)^2$。令 $Y$ 是一个以 $\boldsymbol{y}_i^T$ 为行的 $m \times (n+1)$ 矩阵，这个[目标函数](@entry_id:267263)可以写成 $\|Y\boldsymbol{n}\|_2^2$。

最小化 $\|Y\boldsymbol{n}\|_2^2$ 在约束 $\|\boldsymbol{n}\|=1$ 下是一个经典的[瑞利商](@entry_id:137794)问题。其解 $\boldsymbol{n}$ 是中心化[数据协方差](@entry_id:748192)矩阵 $Y^T Y$ 对应于**[最小特征值](@entry_id:177333)**的[特征向量](@entry_id:151813)。根据 SVD 的性质，这等价于中心化数据矩阵 $Y$ 对应于**最小奇异值**的[右奇异向量](@entry_id:754365) [@problem_id:3234673, A]。这个向量 $\boldsymbol{n}$ 定义了数据[方差](@entry_id:200758)最小的方向，因此拟合的超平面正是与数据[分布](@entry_id:182848)中最不显著的主成分方向正交的平面。最小的距离平方和等于该最小[奇异值](@entry_id:152907)的平方，即 $\sigma_{min}^2(Y)$ [@problem_id:3234673, C]。

让我们通过一个例子来阐明 TLS 作为[正交回归](@entry_id:753009)的优越性。考虑一个三维空间中的数据云，其真实点[分布](@entry_id:182848)在一个平面 $2x-y-z=0$ 上，但观测到的 $(x,y,z)$ 坐标都受到了独立的、[方差](@entry_id:200758)为1的噪声干扰。在这种 EIV 模型下，OLS 通过最小化 $z$ 方向的残差（即 $z - (px+qy)$）得到的拟合平面，其[法向量](@entry_id:264185)会偏离真实法向量 $(2, -1, -1)$，因为 OLS 无法解释 $x$ 和 $y$ 中的误差。然而，TLS 通过最小化到平面的正交距离，能够正确地识别出数据中由各向同性噪声引入的最小[方差](@entry_id:200758)方向。可以证明，当噪声协[方差](@entry_id:200758)为 $\sigma^2 I$ 时，[数据协方差](@entry_id:748192)矩阵 $\Sigma$ 的[最小特征值](@entry_id:177333)对应的[特征向量](@entry_id:151813)恰好是真实平面的[法向量](@entry_id:264185)。因此，TLS 能够在这种理想的 EIV 场景下无偏地恢复出真实的底层关系，而 OLS 则不能 [@problem_id:3599783]。

### 实践考量与扩展

#### [仿射模型](@entry_id:143914)的拟合：截距问题

标准的 TLS 公式 $A\boldsymbol{x} \approx \boldsymbol{b}$ 对应于一个穿过原点的[超平面](@entry_id:268044)。然而，在大多数应用中，我们需要拟合一个包含截距项的**[仿射模型](@entry_id:143914)（affine model）**：$b_i \approx \boldsymbol{a}_i^T\boldsymbol{\beta} + \beta_0$。有两种正确的方法来处理这个截距项 $\beta_0$ [@problem_id:3599792]。

1.  **数据中心化**：这是最常见的方法。首先，计算数据矩阵 $A$ 各列的均值（得到向量 $\bar{\boldsymbol{a}}$）和向量 $\boldsymbol{b}$ 的均值 $\bar{b}$。然后，对数据进行中心化处理，得到 $A_c = A - \mathbf{1}\bar{\boldsymbol{a}}^T$ 和 $\boldsymbol{b}_c = \boldsymbol{b} - \bar{b}\mathbf{1}$。可以证明，原始的[仿射模型](@entry_id:143914)等价于中心化数据的一个齐次模型 $\boldsymbol{b}_c \approx A_c \boldsymbol{\beta}$ [@problem_id:3599792, A]。我们对 $(A_c, \boldsymbol{b}_c)$ 应用标准的 TLS 算法来求解斜率向量 $\boldsymbol{\beta}$。一旦求得 $\hat{\boldsymbol{\beta}}$，截距项就可以通过确保拟合平面穿过数据[质心](@entry_id:265015) $(\bar{\boldsymbol{a}}, \bar{b})$ 来恢复：

    $$
    \hat{\beta}_0 = \bar{b} - \bar{\boldsymbol{a}}^T \hat{\boldsymbol{\beta}}
    $$

2.  **[增广矩阵](@entry_id:150523)法**：另一种方法是将模型写成 $\boldsymbol{b} \approx [A \ \ \mathbf{1}] \begin{pmatrix} \boldsymbol{\beta} \\ \beta_0 \end{pmatrix}$。这里，我们显式地将一个全为1的列向量加入到数据矩阵中，其对应的系数就是截距 $\beta_0$。然而，关键在于，这个全为1的列代表了一个没有误差的、确定的回归量。因此，我们必须使用一种**混合 OLS-TLS** 或 **带精确列的 TLS** 算法，在求解过程中不允许扰动这个全为1的列。理论上可以证明，这种方法与数据中心化方法得到的斜率 $\hat{\boldsymbol{\beta}}$ 和截距 $\hat{\beta}_0$ 是完全等价的 [@problem_id:3599792, B]。

需要特别警惕的是，如果天真地将全1列加入 $A$ 中，然后应用标准的 TLS 算法（允许所有列被扰动），将会得到错误的结果。因为算法可能会发现，通过扰动这个“1”列可以更有效地减小整体误差，从而导致拟合出一个不再具有明确截距意义的模型 [@problem_id:3599792, C]。

#### 数值实现：SVD 与正规方程

从计算角度看，求解 TLS 的核心是找到[增广矩阵](@entry_id:150523) $C = [A \ \ \boldsymbol{b}]$ 的最小奇异值及其对应的[右奇异向量](@entry_id:754365)。实现这一目标有两种主要途径 [@problem_id:3599805]：

1.  **直接 SVD 法**：直接对 $m \times (n+1)$ 的矩阵 $C$ 应用数值稳定的 SVD 算法（如基于 Golub-Kahan [双对角化](@entry_id:746789)的算法）。这是目前最受推荐的、最稳健的方法。

2.  **[正规方程](@entry_id:142238)法**：利用 $C^T C$ 的[特征向量](@entry_id:151813)就是 $C$ 的[右奇异向量](@entry_id:754365)这一关系，转而求解 $(n+1) \times (n+1)$ 的[对称矩阵](@entry_id:143130) $C^T C$ 的[特征值问题](@entry_id:142153)。具体来说，我们寻找 $C^T C$ 的[最小特征值](@entry_id:177333) $\lambda_{min} = \sigma_{n+1}^2$ 及其对应的[特征向量](@entry_id:151813) $\boldsymbol{v}_{n+1}$。

虽然在精确算术中，这两种方法是等价的，但在有限精度的[浮点运算](@entry_id:749454)中，它们的数值稳定性却有天壤之别。问题出在**显式地计算[交叉](@entry_id:147634)乘积矩阵 $C^T C$** 这一步。这个操作会使问题的条件数平方，即 $\kappa_2(C^T C) = (\kappa_2(C))^2$。如果原始矩阵 $C$ 是病态的（即[条件数](@entry_id:145150) $\kappa_2(C)$ 很大），那么 $C^T C$ 将会是极度病态的。在计算 $C^T C$ 的过程中，与小奇异值相关的信息可能会因为舍入误差而被“淹没”，导致计算出的最小特征值和[特征向量](@entry_id:151813)严重失真。

相比之下，直接对 $C$ 进行 SVD 的现代算法具有**[后向稳定性](@entry_id:140758)（backward stability）**，它们避免了条件数的平方，从而在面对[病态问题](@entry_id:137067)时能提供远为精确和可靠的结果。因此，在高质量的数值软件实现中，总是优先选择直接 SVD 法来求解总最小二乘问题 [@problem_id:3599805, A]。