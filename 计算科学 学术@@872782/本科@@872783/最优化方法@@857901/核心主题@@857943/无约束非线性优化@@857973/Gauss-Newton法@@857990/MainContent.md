## 引言
在科学研究与工程实践中，我们经常需要从充满噪声的观测数据中提取有意义的信息，这通常归结为找到一个能最佳拟[合数](@entry_id:263553)据的数学模型。当模型与待求参数之间的关系为[非线性](@entry_id:637147)时，我们就面临着一[类核](@entry_id:178267)心的优化挑战：[非线性](@entry_id:637147)最小二乘问题。直接求解这类问题往往非常困难，因为它需要解决复杂的非线性方程组。

高斯-牛顿法（Gauss-Newton Method）为此提供了一个优雅而强大的迭代解决方案。它巧妙地回避了直接处理[非线性](@entry_id:637147)的困难，通过在每一步都用一个简单的线性模型来逼近复杂的[非线性系统](@entry_id:168347)，从而将问题转化为我们熟知且易于处理的线性代数问题。这种“化繁为简”的思想使其成为[数据拟合](@entry_id:149007)、[参数估计](@entry_id:139349)和[系统辨识](@entry_id:201290)等领域应用最广泛的算法之一。

本文将带领您深入探索高斯-[牛顿法](@entry_id:140116)的世界。在“原理与机制”一章中，我们将从第一性原理出发，推导其迭代公式，阐明雅可比矩阵的核心作用，并将其与牛顿法、最速下降法等经典优化算法进行比较，以揭示其内在联系与本质。随后，在“应用与跨学科联系”一章中，我们将穿越物理、生物、工程和计算机科学等多个领域，通过一系列真实案例展示该方法如何解决从GPS定位到[神经网](@entry_id:276355)络训练等实际问题。最后，通过“动手实践”部分提供的编程练习，您将有机会亲手实现并感受高斯-[牛顿法](@entry_id:140116)的威力与精妙之处。

## 原理与机制

### 核心思想：[非线性](@entry_id:637147)问题的线性化

高斯-牛顿法是一种用于求解[非线性](@entry_id:637147)[最小二乘问题](@entry_id:164198)的[迭代算法](@entry_id:160288)。这类问题的核心目标是找到一组参数 $\boldsymbol{\beta}$，使得一系列[非线性模型](@entry_id:276864)预测值与观测数据之间的[残差平方和](@entry_id:174395)最小。具体而言，给定 $m$ 个数据点 $(t_i, y_i)$ 和一个依赖于 $n$ 个参数 $\boldsymbol{\beta} = (\beta_1, \dots, \beta_n)^T$ 的[非线性模型](@entry_id:276864)函数 $f(t; \boldsymbol{\beta})$，我们定义第 $i$ 个残差为：

$r_i(\boldsymbol{\beta}) = y_i - f(t_i; \boldsymbol{\beta})$

目标函数是所有这些残差的平方和，记为 $S(\boldsymbol{\beta})$：

$S(\boldsymbol{\beta}) = \sum_{i=1}^{m} [r_i(\boldsymbol{\beta})]^2 = \mathbf{r}(\boldsymbol{\beta})^T \mathbf{r}(\boldsymbol{\beta})$

其中 $\mathbf{r}(\boldsymbol{\beta})$ 是一个由所有残差组成的 $m$ 维列向量。由于 $r_i(\boldsymbol{\beta})$ 的[非线性](@entry_id:637147)特性，直接求解方程 $\nabla S(\boldsymbol{\beta}) = \mathbf{0}$ 以找到最小值通常非常困难。

高斯-牛顿法的核心思想是，在每次迭代中，不用直接处理这个复杂的[非线性](@entry_id:637147)目标函数，而是用一个更简单的[局部线性](@entry_id:266981)模型来近似它。具体来说，在当前参数的估计值 $\boldsymbol{\beta}_k$ 附近，我们通过一阶[泰勒展开](@entry_id:145057)来线性化残差向量 $\mathbf{r}(\boldsymbol{\beta})$。设 $\boldsymbol{\Delta}$ 是从 $\boldsymbol{\beta}_k$ 到下一个估计值 $\boldsymbol{\beta}_{k+1}$ 的更新步长，即 $\boldsymbol{\beta}_{k+1} = \boldsymbol{\beta}_k + \boldsymbol{\Delta}$。那么，新的残差向量可以近似为：

$\mathbf{r}(\boldsymbol{\beta}_k + \boldsymbol{\Delta}) \approx \mathbf{r}(\boldsymbol{\beta}_k) + \mathbf{J}(\boldsymbol{\beta}_k) \boldsymbol{\Delta}$

这里，$\mathbf{J}(\boldsymbol{\beta}_k)$ 是[残差向量](@entry_id:165091) $\mathbf{r}$ 在点 $\boldsymbol{\beta}_k$ 处关于参数 $\boldsymbol{\beta}$ 的雅可比矩阵。该矩阵的第 $i$ 行第 $j$ 列的元素为 $(J)_{ij} = \frac{\partial r_i}{\partial \beta_j}$。这个线性近似将原始的[非线性](@entry_id:637147)最小二乘问题，转化为了一个关于步长 $\boldsymbol{\Delta}$ 的 **线性最小二乘问题** [@problem_id:2214258]。

### 高斯-牛顿更新步的推导

在得到[残差向量](@entry_id:165091)的线性近似后，我们将其代入目标函数 $S(\boldsymbol{\beta})$，从而得到一个关于更新步 $\boldsymbol{\Delta}$ 的二次近似模型 $S_L(\boldsymbol{\Delta})$：

$S_L(\boldsymbol{\Delta}) = \|\mathbf{r}(\boldsymbol{\beta}_k) + \mathbf{J}(\boldsymbol{\beta}_k) \boldsymbol{\Delta}\|^2_2 = (\mathbf{r}_k + \mathbf{J}_k \boldsymbol{\Delta})^T (\mathbf{r}_k + \mathbf{J}_k \boldsymbol{\Delta})$

为了方便，我们使用简写 $\mathbf{r}_k = \mathbf{r}(\boldsymbol{\beta}_k)$ 和 $\mathbf{J}_k = \mathbf{J}(\boldsymbol{\beta}_k)$。展开上式可得：

$S_L(\boldsymbol{\Delta}) = \mathbf{r}_k^T \mathbf{r}_k + 2\boldsymbol{\Delta}^T \mathbf{J}_k^T \mathbf{r}_k + \boldsymbol{\Delta}^T \mathbf{J}_k^T \mathbf{J}_k \boldsymbol{\Delta}$

我们的目标是找到一个 $\boldsymbol{\Delta}$，使得这个二次模型 $S_L(\boldsymbol{\Delta})$ 最小。为了求极值，我们将 $S_L(\boldsymbol{\Delta})$ 对 $\boldsymbol{\Delta}$ 求梯度并令其为零：

$\nabla_{\boldsymbol{\Delta}} S_L(\boldsymbol{\Delta}) = 2\mathbf{J}_k^T \mathbf{r}_k + 2\mathbf{J}_k^T \mathbf{J}_k \boldsymbol{\Delta} = \mathbf{0}$

整理后，我们得到一个关于 $\boldsymbol{\Delta}$ 的[线性方程组](@entry_id:148943)，这被称为 **正规方程 (Normal Equations)**：

$(\mathbf{J}_k^T \mathbf{J}_k) \boldsymbol{\Delta} = -\mathbf{J}_k^T \mathbf{r}_k$

假设矩阵 $\mathbf{J}_k^T \mathbf{J}_k$ 是可逆的（这通常要求雅可比矩阵 $\mathbf{J}_k$ 是列满秩的），我们可以解出唯一的更新步长 $\boldsymbol{\Delta}_k$ [@problem_id:2214285]：

$\boldsymbol{\Delta}_k = -(\mathbf{J}_k^T \mathbf{J}_k)^{-1} \mathbf{J}_k^T \mathbf{r}_k$

这样，高斯-牛顿法的迭代更新规则就是：

$\boldsymbol{\beta}_{k+1} = \boldsymbol{\beta}_k + \boldsymbol{\Delta}_k = \boldsymbol{\beta}_k - (\mathbf{J}_k^T \mathbf{J}_k)^{-1} \mathbf{J}_k^T \mathbf{r}_k$

整个算法的流程就是：从一个初始猜测 $\boldsymbol{\beta}_0$ 开始，在每一步计算当前的残差向量 $\mathbf{r}_k$ 和雅可比矩阵 $\mathbf{J}_k$，然后求解正规方程得到更新步 $\boldsymbol{\Delta}_k$，并用它来更新参数，直到满足某个[收敛准则](@entry_id:158093)为止。

### [雅可比矩阵](@entry_id:264467)：线性化的核心

从上述推导中可以看出，雅可比矩阵 $\mathbf{J}$ 是高斯-牛顿法的核心构件，它捕捉了模型残差对参数变化的局部敏感度。计算[雅可比矩阵](@entry_id:264467)是应用该方法的关键一步。我们通过几个例子来说明其计算过程。

**示例 1：[酶动力学](@entry_id:145769)模型**

在生物化学中，米氏方程（[Michaelis-Menten](@entry_id:145978) equation）常用于描述酶促[反应速率](@entry_id:139813) $v$ 与[底物浓度](@entry_id:143093) $[S]$ 之间的关系 [@problem_id:2214264]：

$f([S]; V_{\max}, K_m) = \frac{V_{\max} [S]}{K_m + [S]}$

这里的参数是 $\boldsymbol{\beta} = (V_{\max}, K_m)^T$。对于一个给定的数据点 $([S]_i, v_i)$，残差函数为 $r_i(V_{\max}, K_m) = v_i - f([S]_i; V_{\max}, K_m)$。[雅可比矩阵](@entry_id:264467)的元素需要计算残差对每个参数的偏导数：

$\frac{\partial r_i}{\partial V_{\max}} = - \frac{\partial f}{\partial V_{\max}} = - \frac{[S]_i}{K_m + [S]_i}$

$\frac{\partial r_i}{\partial K_m} = - \frac{\partial f}{\partial K_m} = - \left( - \frac{V_{\max} [S]_i}{(K_m + [S]_i)^2} \right) = \frac{V_{\max} [S]_i}{(K_m + [S]_i)^2}$

对于每个数据点，我们都可以计算出雅可比矩阵的一行。将所有数据点对应的行堆叠起来，就构成了完整的雅可比矩阵 $\mathbf{J}$。

**示例 2：正弦模型**

另一个常见的应用场景是拟合[振荡](@entry_id:267781)数据，例如使用正弦模型 $f(x; a, \omega) = a \sin(\omega x)$ [@problem_id:2214289]。参数是幅值 $a$ 和角频率 $\omega$，即 $\boldsymbol{\beta} = (a, \omega)^T$。残差函数为 $r_i(a, \omega) = y_i - a \sin(\omega x_i)$。其对参数的偏导数为：

$\frac{\partial r_i}{\partial a} = - \sin(\omega x_i)$

$\frac{\partial r_i}{\partial \omega} = - a x_i \cos(\omega x_i)$

通过这些具体的例子可以看出，雅可比矩阵的计算是直接的，只需要具备基本的微积分知识。在每次迭代中，都需要使用当前的[参数估计](@entry_id:139349)值 $\boldsymbol{\beta}_k$ 来计算[雅可比矩阵](@entry_id:264467) $\mathbf{J}_k$ 和[残差向量](@entry_id:165091) $\mathbf{r}_k$，然后才能求解更新步长。

### 与其他[优化方法](@entry_id:164468)的关系

为了更深刻地理解高斯-牛顿法，将其与其他经典的[优化算法](@entry_id:147840)进行比较是非常有益的。

#### 与[牛顿法](@entry_id:140116)的关系：一种近似

高斯-[牛顿法](@entry_id:140116)可以被看作是用于优化[目标函数](@entry_id:267263) $S(\boldsymbol{\beta})$ 的牛顿法的一个近似。标准的牛顿法通过求解以下方程来计算更新步长 $\boldsymbol{\Delta}$：

$\mathbf{H}_S(\boldsymbol{\beta}_k) \boldsymbol{\Delta} = -\nabla S(\boldsymbol{\beta}_k)$

其中 $\nabla S(\boldsymbol{\beta})$ 是 $S(\boldsymbol{\beta})$ 的梯度，$\mathbf{H}_S(\boldsymbol{\beta})$ 是其[海森矩阵](@entry_id:139140)（Hessian matrix）。我们来计算这两项。首先是梯度：

$\nabla S(\boldsymbol{\beta}) = \nabla (\mathbf{r}^T \mathbf{r}) = 2 \mathbf{J}^T \mathbf{r}$

其次是[海森矩阵](@entry_id:139140)，对梯度再次求导可得：

$\mathbf{H}_S(\boldsymbol{\beta}) = \frac{\partial}{\partial \boldsymbol{\beta}^T} (2 \mathbf{J}^T \mathbf{r}) = 2 \mathbf{J}^T \mathbf{J} + 2 \sum_{i=1}^{m} r_i(\boldsymbol{\beta}) \mathbf{H}_{r_i}(\boldsymbol{\beta})$

其中 $\mathbf{H}_{r_i}$ 是第 $i$ 个残差函数 $r_i$ 的海森矩阵。

将梯度和[海森矩阵](@entry_id:139140)代入牛顿法方程，得到：

$\left( 2 \mathbf{J}_k^T \mathbf{J}_k + 2 \sum_{i=1}^{m} r_{i,k} \mathbf{H}_{r_i,k} \right) \boldsymbol{\Delta} = -2 \mathbf{J}_k^T \mathbf{r}_k$

与高斯-[牛顿法](@entry_id:140116)的正规方程 $(\mathbf{J}_k^T \mathbf{J}_k) \boldsymbol{\Delta} = -\mathbf{J}_k^T \mathbf{r}_k$ 相比，可以看出，高斯-[牛顿法](@entry_id:140116)实际上是**忽略了**海森矩阵中的第二项 $2 \sum r_i \mathbf{H}_{r_i}$。这个被忽略的项包含了残差函数的[二阶导数](@entry_id:144508)（曲率）信息 [@problem_id:2214277]。

这种近似的合理性基于两个常见场景：
1.  **小残差问题**：当模型能够很好地拟合数据时，在最优点附近，残差 $r_i$ 的值会非常小。因此，包含 $r_i$ 的那一项对海森矩阵的贡献也可以忽略不计。
2.  **近似线性问题**：如果模型函数 $f$ 本身接近线性，那么其[二阶导数](@entry_id:144508)（即 $\mathbf{H}_{r_i}$ 的元素）会很小，使得被忽略的项同样很小。

因此，高斯-[牛顿法](@entry_id:140116)可以被视为[牛顿法](@entry_id:140116)的一种简化，它通过只使用一阶导数（[雅可比矩阵](@entry_id:264467)）来构建对海森矩阵的近似，从而避免了计算和存储复杂的[二阶导数](@entry_id:144508)。

#### 与最速下降法的比较

[最速下降法](@entry_id:140448)是另一种基本的优化算法，它沿着目标函数下降最快的方向（负梯度方向）进行搜索。对于[目标函数](@entry_id:267263) $S(\boldsymbol{\beta})$，其负梯度方向为：

$\mathbf{p}_{SD} = -\nabla S(\boldsymbol{\beta}) = -2 \mathbf{J}^T \mathbf{r}$

高斯-[牛顿法](@entry_id:140116)的搜索方向则是 $\mathbf{p}_{GN} = -(\mathbf{J}^T \mathbf{J})^{-1} \mathbf{J}^T \mathbf{r}$。可以看出，高斯-牛顿方向是通过一个矩阵 $(\mathbf{J}^T \mathbf{J})^{-1}$ 对最速下降方向进行了“修正”或“缩放”。这个矩阵 $(\mathbf{J}^T \mathbf{J})$ 是对[海森矩阵](@entry_id:139140)的近似，因此它包含了关于[目标函数](@entry_id:267263)曲率的二阶信息。这使得高斯-牛顿法通常比[最速下降法](@entry_id:140448)收敛得更快，因为它不仅仅考虑了梯度的方向，还考虑了函数表面的形状，从而能够走出更有效率的步伐 [@problem_id:2214239]。

#### 特殊情况：线性最小二乘

高斯-牛顿法与[线性最小二乘法](@entry_id:165427)之间存在一个深刻而优美的联系。考虑一个[线性模型](@entry_id:178302) $\mathbf{y} \approx \mathbf{X}\boldsymbol{\beta}$，其中 $\mathbf{X}$ 是 $m \times n$ 的[设计矩阵](@entry_id:165826)。[残差向量](@entry_id:165091)为 $\mathbf{r}(\boldsymbol{\beta}) = \mathbf{y} - \mathbf{X}\boldsymbol{\beta}$。

对于这个[线性模型](@entry_id:178302)，残差向量对参数 $\boldsymbol{\beta}$ 的[雅可比矩阵](@entry_id:264467)是一个常数矩阵：

$\mathbf{J} = \frac{\partial}{\partial \boldsymbol{\beta}^T} (\mathbf{y} - \mathbf{X}\boldsymbol{\beta}) = -\mathbf{X}$

现在，我们将这个[雅可比矩阵](@entry_id:264467)代入高斯-牛顿的更新公式中。假设我们从任意一个初始猜测 $\boldsymbol{\beta}_0$ 开始：

$\boldsymbol{\Delta}_0 = -((-\mathbf{X})^T(-\mathbf{X}))^{-1} (-\mathbf{X})^T (\mathbf{y} - \mathbf{X}\boldsymbol{\beta}_0)$
$\boldsymbol{\Delta}_0 = -(\mathbf{X}^T\mathbf{X})^{-1} (-\mathbf{X}^T) (\mathbf{y} - \mathbf{X}\boldsymbol{\beta}_0)$
$\boldsymbol{\Delta}_0 = (\mathbf{X}^T\mathbf{X})^{-1} \mathbf{X}^T (\mathbf{y} - \mathbf{X}\boldsymbol{\beta}_0)$
$\boldsymbol{\Delta}_0 = (\mathbf{X}^T\mathbf{X})^{-1} \mathbf{X}^T \mathbf{y} - (\mathbf{X}^T\mathbf{X})^{-1} \mathbf{X}^T \mathbf{X} \boldsymbol{\beta}_0$
$\boldsymbol{\Delta}_0 = (\mathbf{X}^T\mathbf{X})^{-1} \mathbf{X}^T \mathbf{y} - \boldsymbol{\beta}_0$

那么，下一步的迭代结果为：

$\boldsymbol{\beta}_1 = \boldsymbol{\beta}_0 + \boldsymbol{\Delta}_0 = \boldsymbol{\beta}_0 + ((\mathbf{X}^T\mathbf{X})^{-1} \mathbf{X}^T \mathbf{y} - \boldsymbol{\beta}_0) = (\mathbf{X}^T\mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}$

这个结果正是线性[最小二乘问题](@entry_id:164198)的解析解，即普通最小二乘（OLS）估计量。这意味着，当高斯-[牛顿法](@entry_id:140116)应用于一个线性模型时，它能在**一次迭代**内直接收敛到精确解，无论初始猜测是什么 [@problem_id:2214238]。这一特性完美地展示了高斯-[牛顿法](@entry_id:140116)是如何将线性最小二乘的求解思想推广到[非线性](@entry_id:637147)领域的。

### 与[求根问题](@entry_id:174994)的联系

高斯-[牛顿法](@entry_id:140116)不仅与[优化问题](@entry_id:266749)相关，还与[非线性方程组](@entry_id:178110)的[求根问题](@entry_id:174994)密切相关。考虑一个有 $n$ 个方程和 $n$ 个未知数的[非线性方程组](@entry_id:178110) $\mathbf{F}(\mathbf{x}) = \mathbf{0}$，其中 $\mathbf{F}: \mathbb{R}^n \to \mathbb{R}^n$。

我们可以将[求根问题](@entry_id:174994)重新表述为一个最小二乘[优化问题](@entry_id:266749)，即寻找一个 $\mathbf{x}$ 来最小化残差的范数平方：$\min_{\mathbf{x}} \frac{1}{2} \|\mathbf{F}(\mathbf{x})\|_2^2$。这个问题现在完全符合高斯-牛顿法的框架，其中残差向量就是 $\mathbf{F}(\mathbf{x})$ 本身。

在这种情况下，残差的[雅可比矩阵](@entry_id:264467)就是函数 $\mathbf{F}(\mathbf{x})$ 的[雅可比矩阵](@entry_id:264467) $\mathbf{J}_F(\mathbf{x})$。高斯-[牛顿法](@entry_id:140116)的更新步长 $\mathbf{p}_k$ 由[正规方程](@entry_id:142238)给出：

$(\mathbf{J}_F(\mathbf{x}_k)^T \mathbf{J}_F(\mathbf{x}_k)) \mathbf{p}_k = -\mathbf{J}_F(\mathbf{x}_k)^T \mathbf{F}(\mathbf{x}_k)$

由于系统是“方的”（$m=n$），[雅可比矩阵](@entry_id:264467) $\mathbf{J}_F$ 是一个方阵。如果 $\mathbf{J}_F$ 在 $\mathbf{x}_k$ 处非奇异（可逆），我们可以对上式两边同时左乘其转置的[逆矩阵](@entry_id:140380) $((\mathbf{J}_F^T)^{-1})$：

$\mathbf{J}_F(\mathbf{x}_k) \mathbf{p}_k = -\mathbf{F}(\mathbf{x}_k)$

这恰好是用于求解 $\mathbf{F}(\mathbf{x}) = \mathbf{0}$ 的标准**牛顿-拉夫逊法**（[Newton-Raphson](@entry_id:177436) method）的[更新方程](@entry_id:264802)。因此，对于方程数和未知数个数相等的[非线性系统](@entry_id:168347)，高斯-牛顿法与牛顿-拉夫逊法是等价的 [@problem_id:3232734]。这也进一步解释了为何高斯-牛顿法有时被称为一种“类牛顿”方法。

### 收敛特性与局限性

尽管高斯-[牛顿法](@entry_id:140116)原理清晰且应用广泛，但理解其收敛特性和潜在的局限性至关重要。

#### 局部[收敛性分析](@entry_id:151547)

高斯-牛顿法的局部收敛速度与问题的残差大小直接相关 [@problem_id:3232760]。

1.  **零残差问题 (Small-Residual Problems)**：如果模型能够完美拟合数据，使得在最优点 $\boldsymbol{\beta}^*$ 处，残差向量 $\mathbf{r}(\boldsymbol{\beta}^*) = \mathbf{0}$，那么前面提到的被忽略的海森矩阵项 $2 \sum r_i \mathbf{H}_{r_i}$ 在最优点处为零。在这种情况下，高斯-[牛顿法](@entry_id:140116)所用的近似海森矩阵在最优点处与真实海森矩阵完全一致。因此，该方法的局部收敛行为与真正的[牛顿法](@entry_id:140116)相同，具有**二次收敛**速度。二次收敛意味着每次迭代后，解的有效数字位数大约会翻倍，收敛非常迅速。

2.  **大残差问题 (Large-Residual Problems)**：如果模型无法完美拟[合数](@entry_id:263553)据（这在现实中非常普遍），则在最优点 $\boldsymbol{\beta}^*$ 处，残差 $\mathbf{r}(\boldsymbol{\beta}^*) \neq \mathbf{0}$。此时，被忽略的海森矩阵项不为零，高斯-牛顿法的[海森近似](@entry_id:171462)是有偏的。这种偏差导致算法的收敛速度从二次退化为**[线性收敛](@entry_id:163614)**。[线性收敛](@entry_id:163614)意味着每次迭代只减少一个固定比例的误差，其收敛速度可能远慢于二次收敛。[线性收敛](@entry_id:163614)的速率与最优点处残差的大小成正比；残差越大，收敛越慢 [@problem_id:3232734]。

#### 方法的失效模式

纯粹的高斯-[牛顿法](@entry_id:140116)并非总是可靠的，它在某些情况下可能会表现不佳甚至失效。

1.  **雅可比矩阵的[秩亏](@entry_id:754065)**：算法要求矩阵 $\mathbf{J}^T \mathbf{J}$ 是可逆的。这需要[雅可比矩阵](@entry_id:264467) $\mathbf{J}$ 是列满秩的。如果参数之间存在[共线性](@entry_id:270224)，或者模型对某些参数不敏感，$\mathbf{J}$ 就可能变成[秩亏](@entry_id:754065)的，导致 $\mathbf{J}^T \mathbf{J}$ 不可逆或病态。此时，更新步长无法确定或数值上极不稳定。

2.  **收敛性无保证**：高斯-[牛顿法](@entry_id:140116)只保证在最优点附近且满足特定条件时才收敛。如果初始猜测 $\boldsymbol{\beta}_0$ 离最优点太远，迭代过程可能不收敛。更新步长可能过大，导致新的参数点处的目标函数值反而增加（“步子迈得太大”）。

3.  **[振荡](@entry_id:267781)或发散行为**：在某些高度[非线性](@entry_id:637147)的问题中，即使每一步的计算都正确，迭代序列也可能陷入[振荡](@entry_id:267781)或直接发散。一个经典的例子是拟合一个简单的反正切函数 [@problem_id:2214263]。考虑将模型 $g(t; x) = \arctan(xt)$ 拟合到数据点 $(t_1, y_1) = (1, 0)$。其迭代函数为 $x_{k+1} = x_k - (1 + x_k^2) \arctan(x_k)$。虽然最优解显然是 $x=0$，但如果从一个特定的初始点（例如 $x_0 \approx 1.392$）开始，算法会进入一个稳定的2-周期，在 $x_0$ 和 $-x_0$ 之间无限[振荡](@entry_id:267781)，永远无法收敛到真正的最小值。

这些局限性催生了更稳健的改进算法，如**莱文伯格-马夸特方法（Levenberg-Marquardt algorithm）**和**[信赖域方法](@entry_id:138393)（Trust-Region methods）**。这些方法通过在每一步中引入阻尼项或限制步长的大小，来改善高斯-[牛顿法](@entry_id:140116)在[病态问题](@entry_id:137067)和远离最优点时的收敛性能，我们将在后续章节中详细探讨。