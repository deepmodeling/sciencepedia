## 引言
逆问题——从结果反推原因——是贯穿于现代科学与工程计算的核心挑战。无论是从模糊的太[空图](@entry_id:275064)像中恢复清晰的星系结构，还是根据地面震动数据推断地球内部的构造，我们都在试图解决这类问题。然而，许多[逆问题](@entry_id:143129)本质上是“不适定的”（ill-posed）：观测数据中的微小噪声就可能导致解的巨大偏差，使得传统的求解方法失效。这构成了从不[完美数](@entry_id:636981)据中提取有意义信息的根本障碍。

本文旨在系统地介绍“正则化”这一强大思想框架，它是克服[不适定性](@entry_id:635673)、从含噪数据中获得稳定可靠解的关键。通过学习本文，你将掌握[正则化方法](@entry_id:150559)的核心原理及其在不同领域的应用之道。

- 在“**原理与机制**”一章中，我们将深入[逆问题](@entry_id:143129)的数学核心，揭示其[不适定性](@entry_id:635673)的根源。你将学习经典的[Tikhonov正则化](@entry_id:140094)如何通过引入[先验信息](@entry_id:753750)来稳定求解过程，以及现代的[稀疏正则化](@entry_id:755137)（如[LASSO](@entry_id:751223)）如何帮助我们找到结构更简洁的解。
- 接着，在“**应用与[交叉](@entry_id:147634)学科联系**”一章中，我们将跨越学科边界，探索正则化在信号处理、医学成像、计算金融乃至社会科学等领域的真实应用案例，让你直观感受这些数学工具的强大威力。
- 最后，在“**动手实践**”部分，你将有机会通过具体的编程练习，亲手构建和求解正则化模型，将理论知识转化为解决实际问题的能力。

现在，让我们一同启程，深入探索正则化的世界，学习如何驾驭数据中的不确定性。

## 原理与机制

在“引言”章节中，我们已经了解了[逆问题](@entry_id:143129)的普遍性及其在科学和工程中的核心地位。本章将深入探讨[逆问题](@entry_id:143129)的数学原理，特别是其内在的不稳定性，并系统地阐述“正则化”这一关键思想，它是从充满噪声和不确定性的数据中提取可靠信息的根本机制。我们将从经典的[Tikhonov正则化](@entry_id:140094)出发，逐步扩展到促进稀疏性的现代方法，并最终探讨一些前沿的正则化策略及其在贝叶斯推断框架下的统一解释。

### [逆问题](@entry_id:143129)的[不适定性](@entry_id:635673)

许多逆问题可以被形式化为一个线性方程系统。在离散形式下，这通常表示为：

$$
\mathbf{y} = \mathbf{A}\mathbf{x}_{\text{true}} + \mathbf{e}
$$

其中，$\mathbf{y} \in \mathbb{R}^{m}$ 是我们观测到的数据向量，$\mathbf{A} \in \mathbb{R}^{m \times n}$ 是描述物理过程或测量手段的正向模型矩阵，$\mathbf{x}_{\text{true}} \in \mathbb{R}^{n}$ 是我们希望恢复的未知参数向量（例如，图像的像素值、地下介质的属性等），而 $\mathbf{e} \in \mathbb{R}^{m}$ 代表测量噪声。

一个看似直接的求解方法是最小化数据与模型预测之间的[残差平方和](@entry_id:174395)，即**[最小二乘法](@entry_id:137100)** (Least Squares, LS)：

$$
\mathbf{x}_{\text{LS}} = \arg\min_{\mathbf{x} \in \mathbb{R}^{n}} \|\mathbf{A}\mathbf{x} - \mathbf{y}\|_{2}^{2}
$$

当矩阵 $\mathbf{A}$ 列满秩时，[最小二乘解](@entry_id:152054)由其[伪逆](@entry_id:140762) $\mathbf{A}^{\dagger} = (\mathbf{A}^{\top}\mathbf{A})^{-1}\mathbf{A}^{\top}$ 给出：$\mathbf{x}_{\text{LS}} = \mathbf{A}^{\dagger}\mathbf{y}$。然而，这个解往往是不可靠的。问题根源在于许多逆问题本质上是**不适定的** (ill-posed)。一个适定的 (well-posed) 问题应满足三个条件：解存在、解唯一、解稳定。对于[逆问题](@entry_id:143129)，最常被违反的是**稳定性**，即解对数据的微小扰动（如噪声）异常敏感。

为了精确理解这种不稳定性，我们可以借助**[奇异值分解](@entry_id:138057)** (Singular Value Decomposition, SVD) 来分析矩阵 $\mathbf{A}$。任何矩阵 $\mathbf{A}$ 都可以分解为 $\mathbf{A} = \mathbf{U}\mathbf{\Sigma}\mathbf{V}^{\top}$，其中 $\mathbf{U}$ 和 $\mathbf{V}$ 是正交矩阵，$\mathbf{\Sigma}$ 是一个[对角矩阵](@entry_id:637782)，其对角线上的元素 $\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_n > 0$ 称为[奇异值](@entry_id:152907)。[最小二乘解](@entry_id:152054)的误差可以表示为：

$$
\mathbf{x}_{\text{LS}} - \mathbf{x}_{\text{true}} = \mathbf{A}^{\dagger}\mathbf{e} = (\mathbf{V}\mathbf{\Sigma}^{\dagger}\mathbf{U}^{\top})\mathbf{e} = \sum_{i=1}^{n} \frac{\mathbf{u}_{i}^{\top}\mathbf{e}}{\sigma_{i}} \mathbf{v}_{i}
$$

其中 $\mathbf{u}_i$ 和 $\mathbf{v}_i$ 分别是 $\mathbf{U}$ 和 $\mathbf{V}$ 的列向量（左、[右奇异向量](@entry_id:754365)）。这个表达式揭示了问题的核心：如果存在很小的[奇异值](@entry_id:152907) ($\sigma_i \to 0$)，它们在分母上的出现将极大地放大噪声向量 $\mathbf{e}$ 在对应[奇异向量](@entry_id:143538)方向上的分量。即使噪声 $\mathbf{e}$ 的范数很小，其在某些方向上的投影 $\mathbf{u}_{i}^{\top}\mathbf{e}$ 也可能非零，导致解的误差 $\mathbf{x}_{\text{LS}} - \mathbf{x}_{\text{true}}$ 变得非常大，使得解完全被噪声淹没。

一个矩阵的**条件数** (condition number)，定义为 $\kappa_{2}(\mathbf{A}) = \sigma_{\max}(\mathbf{A}) / \sigma_{\min}(\mathbf{A})$，量化了这种不稳定性。一个巨大的条件数意味着 $\sigma_{\min}$ 相对于 $\sigma_{\max}$ 非常小，表明该问题是**病态的** (ill-conditioned)。在这种情况下，[最小二乘解](@entry_id:152054)对噪声极其敏感，迫切需要正则化来稳定求解过程 [@problem_id:2405393]。

更糟糕的是，直接求解[最小二乘问题](@entry_id:164198)的标准方法是构建并求解**正规方程** (normal equations)：$\mathbf{A}^{\top}\mathbf{A}\mathbf{x} = \mathbf{A}^{\top}\mathbf{y}$。虽然在数学上等价，但在数值计算上这会进一步恶化问题。矩阵 $\mathbf{A}^{\top}\mathbf{A}$ 的[条件数](@entry_id:145150)是原[矩阵条件数](@entry_id:142689)的平方，即 $\kappa_{2}(\mathbf{A}^{\top}\mathbf{A}) = \kappa_{2}(\mathbf{A})^{2}$。这意味着，即便是中等病态的问题，在形成正规方程后也会变得极其病态，这使得正则化的需求在实践中更为迫切 [@problem_id:2405393]。

### [Tikhonov正则化](@entry_id:140094)：经典的稳定化方法

为了克服[不适定性](@entry_id:635673)，我们需要向问题中引入额外的信息或约束，这就是**正则化** (regularization) 的思想。最常用和最经典的[正则化方法](@entry_id:150559)是**[Tikhonov正则化](@entry_id:140094)** (也称岭回归，Ridge Regression)。它通过在最小二乘[目标函数](@entry_id:267263)中增加一个惩罚项来实现，该惩罚项惩罚解向量 $\mathbf{x}$ 的大小：

$$
J(\mathbf{x}) = \|\mathbf{A}\mathbf{x} - \mathbf{y}\|_{2}^{2} + \alpha^{2}\|\mathbf{x}\|_{2}^{2}
$$

求解 $\min_{\mathbf{x}} J(\mathbf{x})$ 的过程在两个相互矛盾的目标之间寻求平衡：
1.  **数据保真项** $\|\mathbf{A}\mathbf{x} - \mathbf{y}\|_{2}^{2}$：确保解能够很好地拟合观测数据。
2.  **正则化项** $\|\mathbf{x}\|_{2}^{2}$：体现了我们对解的先验信念，即一个“好”的解应该具有较小的范数（更“简单”或更“平滑”）。

**[正则化参数](@entry_id:162917)** $\alpha \ge 0$ 控制着这种平衡。当 $\alpha \to 0$ 时，我们回到不稳定的[最小二乘解](@entry_id:152054)；当 $\alpha \to \infty$ 时，数据保真项被忽略，解趋向于 $\mathbf{x}=\mathbf{0}$。选择一个合适的 $\alpha$ 是[正则化方法](@entry_id:150559)应用中的核心挑战，它体现了**偏差-方差权衡** (bias-variance tradeoff)：较大的 $\alpha$ 会引入更大的系统性偏差（因为解被强行拉向零），但能有效抑制由噪声引起的[方差](@entry_id:200758)。

[Tikhonov正则化](@entry_id:140094)问题的解可以通过求解 $\nabla J(\mathbf{x}) = 0$ 得到，其闭式解为：

$$
\mathbf{x}_{\alpha} = (\mathbf{A}^{\top}\mathbf{A} + \alpha^{2}\mathbf{I})^{-1}\mathbf{A}^{\top}\mathbf{y}
$$

再次利用SVD分析，我们可以更清晰地看到[Tikhonov正则化](@entry_id:140094)的作用机制。解可以表示为：

$$
\mathbf{x}_{\alpha} = \sum_{i=1}^{n} \left( \frac{\sigma_{i}^{2}}{\sigma_{i}^{2} + \alpha^{2}} \right) \frac{\mathbf{u}_{i}^{\top}\mathbf{y}}{\sigma_{i}} \mathbf{v}_{i}
$$

这里的 $\frac{\sigma_{i}^{2}}{\sigma_{i}^{2} + \alpha^{2}}$ 称为**滤波因子** (filter factors)。对比无正则化的[最小二乘解](@entry_id:152054)，我们可以发现：
- 对于大的奇异值 ($\sigma_i \gg \alpha$)，滤波因子接近1，解在这些方向上的分量几乎不受影响。
- 对于小的奇异值 ($\sigma_i \lesssim \alpha$)，滤波因子远小于1，有效地抑制了这些不稳定分量，从而控制了噪声的放大 [@problem_id:2405393]。

通过这种方式，[Tikhonov正则化](@entry_id:140094)以引入微小偏差为代价，换取了解的稳定性。当矩阵 $\mathbf{A}$ 的[条件数](@entry_id:145150)很大（意味着存在许多小奇异值）时，通常需要一个相对较大的 $\alpha$ 来有效抑制噪声。

### Tikhonov方法的推广与稳健实现

标准的[Tikhonov正则化](@entry_id:140094)可以被推广，以适应更复杂的先验知识和数据特性。一个更通用的[目标函数](@entry_id:267263)形式是：

$$
J(\mathbf{x}) = \| \mathbf{W} (\mathbf{A}\mathbf{x} - \mathbf{y}) \|_{2}^{2} + \lambda^{2} \| \mathbf{L}\mathbf{x} \|_{2}^{2}
$$

这个形式引入了两个重要的扩展 [@problem_id:2405396]：

1.  **加权矩阵** $\mathbf{W}$：通常是一个[对角矩阵](@entry_id:637782)，用于数据保真项。如果我们的测量数据具有不同的可靠性或噪声水平（即[异方差性](@entry_id:136378)），我们可以为更可靠的测量（噪声[方差](@entry_id:200758)小）分配更大的权重，为不可靠的测量（如离群点）分配更小的权重。这使得模型能够更关注高质量的数据 [@problem_id:2405396, @problem_id:2405416]。

2.  **正则化算子** $\mathbf{L}$：允许我们对解的特定属性施加惩罚，而不仅仅是其范数。常见的选择包括：
    *   $\mathbf{L} = \mathbf{I}$ ([单位矩阵](@entry_id:156724))：即标准[Tikhonov正则化](@entry_id:140094)，惩罚解的能量。
    *   $\mathbf{L} = \mathbf{D}$ (差分算子)：惩罚解的梯度范数，例如 $\| \mathbf{D}\mathbf{x} \|_{2}^{2} = \sum_i (x_{i+1}-x_i)^2$。这会促使解变得**平滑**，因为相邻元素之间的剧烈变化会受到惩罚 [@problem_id:2405396, @problem_id:2449137]。
    *   更复杂的算子：在特定应用中，$\mathbf{L}$ 可以是基于物理定律的[微分算子](@entry_id:140145)。例如，在[流体动力学](@entry_id:136788)速度场重建中，可以同时惩罚场的拉普拉斯算子（促进平滑）和散度（促进[不可压缩性](@entry_id:274914)），形成一个组合的正则化项 [@problem_id:2405416]。

这个广义Tikhonov问题的解同样可以通过求解其正规方程获得：

$$
(\mathbf{A}^{\top} \mathbf{W}^2 \mathbf{A} + \lambda^2 \mathbf{L}^{\top} \mathbf{L}) \mathbf{x} = \mathbf{A}^{\top} \mathbf{W}^2 \mathbf{y}
$$

然而，正如前面所讨论的，直接构建和求解正规方程可能会因为条件数的平方效应而导致数值不稳定。一种更稳健的数值实现方法是**增广系统法** (augmented system method)。注意到广义Tikhonov[目标函数](@entry_id:267263)可以重写为单个[最小二乘问题](@entry_id:164198)：

$$
J(\mathbf{x}) = \left\| \begin{pmatrix} \mathbf{W}\mathbf{A} \\ \lambda \mathbf{L} \end{pmatrix} \mathbf{x} - \begin{pmatrix} \mathbf{W}\mathbf{y} \\ \mathbf{0} \end{pmatrix} \right\|_{2}^{2}
$$

令[增广矩阵](@entry_id:150523) $\mathbf{C} = \begin{pmatrix} \mathbf{W}\mathbf{A} \\ \lambda \mathbf{L} \end{pmatrix}$ 和增广向量 $\mathbf{d} = \begin{pmatrix} \mathbf{W}\mathbf{y} \\ \mathbf{0} \end{pmatrix}$，问题就变成了求解 $\min_{\mathbf{x}} \| \mathbf{C}\mathbf{x} - \mathbf{d} \|_{2}^{2}$。这个标准的最小二乘问题可以通过对 $\mathbf{C}$ 进行**[QR分解](@entry_id:139154)**来稳定地求解，而无需计算 $\mathbf{C}^{\top}\mathbf{C}$，从而避免了[条件数](@entry_id:145150)的平方，提高了[数值精度](@entry_id:173145)和稳定性 [@problem_id:2430326]。

### [稀疏性](@entry_id:136793)促进：$L_1$正则化及其超越

Tikhonov类型的 $L_2$ 正则化倾向于产生所有分量都非零的平滑解。然而，在许多现代应用中，如[压缩感知](@entry_id:197903)、[图像处理](@entry_id:276975)和[生物信息学](@entry_id:146759)，我们有理由相信真实解是**稀疏的** (sparse)，即解向量 $\mathbf{x}$ 的大多数元素都为零。

度量[稀疏性](@entry_id:136793)的最直接方式是**$L_0$“范数”**，$\|\mathbf{x}\|_0$，它计算向量中非零元素的个数。因此，一个自然的[稀疏正则化](@entry_id:755137)问题是：

$$
\min_{\mathbf{x}} \frac{1}{2} \|\mathbf{A}\mathbf{x} - \mathbf{y}\|_{2}^{2} + \lambda \|\mathbf{x}\|_0
$$

不幸的是，由于 $\|\mathbf{x}\|_0$ 的离散和非[凸性](@entry_id:138568)质，求解这个问题是一个[NP难](@entry_id:264825)的组合优化问题（等价于“[最佳子集选择](@entry_id:637833)”），对于实际规模的问题是不可行的 [@problem_id:2405415]。

一个关键的突破是使用**$L_1$范数**，$\|\mathbf{x}\|_1 = \sum_i |x_i|$，作为 $L_0$“范数”的凸近似。由此产生的[优化问题](@entry_id:266749)，通常称为**LASSO** (Least Absolute Shrinkage and Selection Operator) 或[基追踪](@entry_id:200728)[去噪](@entry_id:165626)，是凸的，因此在计算上是可行的：

$$
\min_{\mathbf{x}} \frac{1}{2} \|\mathbf{A}\mathbf{x} - \mathbf{y}\|_{2}^{2} + \lambda \|\mathbf{x}\|_1
$$

$L_1$范数之所以能促进[稀疏性](@entry_id:136793)，是因为其在坐标轴上具有“尖角”。这使得在优化过程中，解的许多分量会精确地收缩到零。与此相反，$L_2$范数的“球”是光滑的，它只会将系数拉向零，但通常不会使其恰好等于零。

当应用于解的梯度时，$L_1$正则化产生了强大的**总变差** (Total Variation, TV) [正则化方法](@entry_id:150559)。对比两种对梯度进行正则化的方法 [@problem_id:2449137]：
- **$L_2$梯度正则化** ($\min \| \mathbf{D}\mathbf{x} \|_{2}^{2}$): 惩罚梯度的大值，产生整体**平滑**的解。
- **$L_1$梯度正则化** ($\min \| \mathbf{D}\mathbf{x} \|_{1}$): 促进梯度稀疏，即许多位置的梯度 $(D\mathbf{x})_i = x_{i+1}-x_i$ 精确为零。这导致解是**分段常数**的，或称“块状” (blocky)。这种性质在需要保留边缘和重建具有清晰边界的对象的应用中（如地质断层成像或[医学图像分割](@entry_id:636215)）非常理想 [@problem_id:2449137]。

稀疏性的概念还可以进一步推广到**结构化稀疏**。例如，在某些问题中，我们期望系数以组的形式出现或消失。**组稀疏** (Group Sparsity) 正则化，使用混合的 $L_{2,1}$ 范数，可以实现这一目标：

$$
R(\mathbf{x}) = \sum_{g=1}^{G} \| \mathbf{x}_{G_g} \|_{2}
$$

其中，$\mathbf{x}$ 的索引被划分为不相交的组 $G_g$。这个正则化项对每个组的 $L_2$ 范数求和。由于外层的 $L_1$ 结构，它会促使某些组的 $L_2$ 范数整体变为零，从而实现整个组的系数同时被置为零的效果 [@problem_id:2405391]。

### 前沿正则化策略与观点

正则化的思想框架极具扩展性，允许研究人员设计出适应各种复杂先验知识的正则化项。

**[非凸正则化](@entry_id:636532)**：虽然 $L_1$ 范数是强大的凸代理，但它也存在一些局限，比如对大系数会引入不可忽略的偏差。为了更好地逼近 $L_0$“范数”，研究人员提出了**非凸** (non-convex) 的惩罚函数，例如 $L_p$“范数” $\|x\|_p^p = \sum_i |x_i|^p$，其中 $0 < p < 1$。与 $L_1$ 范数相比，$L_p$ 惩罚对小系数施加更大的[边际成本](@entry_id:144599)（更强地推向零），而对大系数施加更小的[边际成本](@entry_id:144599)（减少偏差）。理论和实践都表明，$L_p$ 正则化能够以更少的测量数据恢复更稀疏的信号 [@problem_id:2405374]。然而，这种优势的代价是计算上的挑战：[目标函数](@entry_id:267263)变为非凸，可能存在多个局部极小值，使得找到[全局最优解](@entry_id:175747)变得困难 [@problem_id:2405374]。

**在机器学习中的应用**：正则化思想在现代机器学习中无处不在。例如，**[神经网络剪枝](@entry_id:637127)** (neural network pruning) 可以被看作是一个 $L_0$ 正则化问题，其目标是在保持数据拟合能力的同时，找到一个拥有最少非零权重（即连接）的“稀疏”网络。虽然直接求解是[NP难](@entry_id:264825)的，但这个框架启发了许多实用算法，如基于 $L_1$ 松弛的方法，或直接处理非凸问题的**[迭代硬阈值算法](@entry_id:750514)** (Iterative Hard Thresholding, IHT)，后者可被视为在稀疏约束集上的[投影梯度下降](@entry_id:637587) [@problem_id:2405415]。

**拓扑正则化**：正则化甚至可以用来编码关于解的几何或拓扑结构的先验知识。例如，在二值[图像分割](@entry_id:263141)问题中，我们可能希望前景物体是单个连通的区域，而不是分散的碎片。这可以通过直接惩罚前景区域的**[连通分量](@entry_id:141881)数量**来实现。在拓扑学中，[连通分量](@entry_id:141881)的数量由**零阶[贝蒂数](@entry_id:153109)** ($\beta_0$) 给出，因此，将 $\beta_0(\{x | u(x)=1\})$ 作为正则化项，可以直接实现这一目标，这超越了基于范数的传统正则化范畴 [@problem_id:2405420]。

**贝叶斯视角下的统一**：[正则化方法](@entry_id:150559)有一个深刻的概率解释，它将正则化与[贝叶斯推断](@entry_id:146958)中的**[先验分布](@entry_id:141376)**联系起来。从贝叶斯观点看，求解[逆问题](@entry_id:143129)等同于根据观测数据 $\mathbf{y}$ 来更新我们对未知量 $\mathbf{x}$ 的信念。根据贝叶斯定理，[后验概率](@entry_id:153467) $p(\mathbf{x}|\mathbf{y})$ 正比于[似然](@entry_id:167119) $p(\mathbf{y}|\mathbf{x})$ 和先验 $p(\mathbf{x})$ 的乘积：

$$
p(\mathbf{x}|\mathbf{y}) \propto p(\mathbf{y}|\mathbf{x}) p(\mathbf{x})
$$

寻找后验概率最大的解，即**[最大后验概率](@entry_id:268939)** (Maximum A Posteriori, MAP) 估计，等价于最小化负对数后验概率：

$$
\min_{\mathbf{x}} [ -\ln p(\mathbf{y}|\mathbf{x}) - \ln p(\mathbf{x}) ]
$$

现在，让我们建立联系：
-   假设测量噪声是高斯的，$\mathbf{e} \sim \mathcal{N}(0, \sigma^2 \mathbf{I})$，那么[似然函数](@entry_id:141927) $p(\mathbf{y}|\mathbf{x}) = \mathcal{N}(\mathbf{y}|\mathbf{A}\mathbf{x}, \sigma^2 \mathbf{I})$。其负对数 $-\ln p(\mathbf{y}|\mathbf{x})$ 正比于数据保真项 $\frac{1}{2\sigma^2}\|\mathbf{A}\mathbf{x}-\mathbf{y}\|_2^2$。
-   正则化项对应于[先验分布](@entry_id:141376)的负对数。例如：
    *   Tikhonov ($L_2$) 正则化 $\lambda^2\|\mathbf{L}\mathbf{x}\|_2^2$ 对应于一个[高斯先验](@entry_id:749752) $p(\mathbf{x}) \propto \exp(-\frac{\lambda^2}{2}\|\mathbf{L}\mathbf{x}\|_2^2)$。
    *   LASSO ($L_1$) 正则化 $\lambda\|\mathbf{x}\|_1$ 对应于一个拉普拉斯先验 $p(\mathbf{x}) \propto \exp(-\lambda\|\mathbf{x}\|_1)$。

这个贝叶斯框架不仅为正则化提供了理论基础，还指明了如何设计新的[正则化方法](@entry_id:150559)——即通过构建合适的[先验分布](@entry_id:141376)来表达我们对未知量的信念。一个强大的例子是使用**高斯过程** (Gaussian Process, GP) 作为先验。在高斯过程中，我们直接为[函数空间](@entry_id:143478)赋予一个先验分布，其中任意有限个函数值的集合都服从一个多元高斯分布。这个[分布](@entry_id:182848)由一个[均值函数](@entry_id:264860)和一个[协方差核](@entry_id:266561)函数完全定义。在离散化后，GP先验对应于一个特定的[高斯先验](@entry_id:749752) $\mathcal{N}(\mathbf{0}, K)$，其中协方差矩阵 $K$ 由[核函数](@entry_id:145324)在网格点上的求值得到。在这种情况下，正则化问题自然地从先验定义中产生，而正则化强度和类型则由[核函数](@entry_id:145324)的超参数（如长度尺度和幅度）控制 [@problem_id:2405451]。

综上所述，正则化是解决[逆问题](@entry_id:143129)的核心工具。从经典的Tikhonov方法到现代的稀疏和结构化稀疏方法，再到更高级的非凸、拓扑和[贝叶斯正则化](@entry_id:635494)，其基本原理一脉相承：通过引入关于解的[先验信息](@entry_id:753750)，将不适定的问题转化为一个适定的、可以在计算上求解的问题，从而在数据和先验之间找到一个有意义的[平衡点](@entry_id:272705)。