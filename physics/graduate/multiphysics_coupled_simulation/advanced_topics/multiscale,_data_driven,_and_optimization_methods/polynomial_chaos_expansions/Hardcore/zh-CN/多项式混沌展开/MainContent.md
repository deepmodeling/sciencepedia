## 引言
在现代科学与工程领域，从多物理场耦合仿真到金融建模，不确定性无处不在。量化这些不确定性对模型输出的影响，对于评估系统性能、进行风险分析和做出可靠决策至关重要。然而，传统的采样方法，如蒙特卡洛模拟，往往需要成千上万次模型评估，对于计算密集型模型而言，其成本高昂得令人望而却步。因此，学术界和工业界迫切需要一种更高效、更系统化的不确定性量化（UQ）框架。

多项式混沌展开（Polynomial Chaos Expansions, PCE）正是为应对这一挑战而生的一种强大技术。它提供了一种优雅的谱方法，能以极高的效率将模型的不确定性传播过程转化为一个可分析的数学结构。本文旨在为读者提供一个关于PCE的全面而深入的指南。我们将从基本原理出发，逐步深入到高级应用和前沿研究。

在接下来的内容中，我们将通过三个核心章节来构建您的知识体系：首先，在“原理与机制”一章中，我们将奠定坚实的数学基础，详细阐述PCE的谱表示、基函数构建以及系数计算的核心方法。接着，在“应用与交叉学科联系”一章中，我们将通过一系列真实世界的案例，展示PCE如何在计算电磁学、控制工程、数据同化等多个领域中发挥作用，凸显其作为跨学科桥梁的价值。最后，通过“动手实践”部分，您将有机会亲手实现PCE的关键算法，将理论知识转化为解决实际问题的能力。

现在，让我们从第一章开始，深入探索PCE的数学核心，揭示其如何将随机性编码为一组确定的多项式系数。

## 原理与机制

本章深入探讨了多项式混沌展开（Polynomial Chaos Expansions, PCE）的基本原理和核心机制。我们将从其数学基础出发，系统地阐述如何构建和应用这一强大的不确定性量化工具。我们将探讨如何处理复杂的输入、如何实际计算展开系数，以及如何从展开式中高效地提取有价值的统计信息。最后，我们还将介绍一些高级技术，以应对物理模型中出现的更复杂挑战。

### 基本表示：广义多项式混沌展开

不确定性量化领域的一个核心任务是表征一个物理系统的输出如何响应其输入参数中的随机性。假设一个模型的输出量，我们称之为感兴趣的量（Quantity of Interest, QoI），记作 $Y$，它是随机输入向量 $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$ 的函数。广义多项式混沌展开（gPCE）的基本思想是将这个随机输出 $Y(\boldsymbol{\xi})$ 表示为一个谱展开，其基函数由与输入随机变量 $\boldsymbol{\xi}$ 的概率分布相适应的正交多项式构成。

为了精确地定义这一展开，我们首先需要一个合适的函数空间。我们考虑所有关于 $\boldsymbol{\xi}$ 的概率测度 $\mu$ 平方可积的函数构成的希尔伯特空间，记作 $L^2(\mu)$。这个空间中的任何函数 $f(\boldsymbol{\xi})$ 都满足 $\int |f(\boldsymbol{\xi})|^2 d\mu(\boldsymbol{\xi})  \infty$。该空间配备了一个内积，定义为两个函数乘[积的期望](@entry_id:190023)值：
$$
\langle f, g \rangle = \mathbb{E}[f(\boldsymbol{\xi})g(\boldsymbol{\xi})] = \int_{\mathbb{R}^d} f(\boldsymbol{\xi})g(\boldsymbol{\xi}) d\mu(\boldsymbol{\xi})
$$

在 $L^2(\mu)$ 空间中，我们可以构建一组多元正交多项式基函数 $\{\psi_{\alpha}(\boldsymbol{\xi})\}_{\alpha \in \mathcal{A}}$，其中 $\mathcal{A}$ 是一个可数的多元索引集（例如 $\mathbb{N}_0^d$）。这组基函数满足**正交归一性**（orthonormality）条件：
$$
\langle \psi_{\alpha}, \psi_{\beta} \rangle = \delta_{\alpha\beta}
$$
其中 $\delta_{\alpha\beta}$ 是克罗内克（Kronecker）符号。根据惯例，零阶多项式是一个常数，$\psi_{\boldsymbol{0}}(\boldsymbol{\xi}) \equiv 1$，这要求概率测度是归一化的，即 $\int d\mu(\boldsymbol{\xi}) = 1$。正交归一性条件也意味着所有高阶（$\alpha \neq \boldsymbol{0}$）基多项式的均值为零，因为 $\mathbb{E}[\psi_{\alpha}] = \langle \psi_{\alpha}, 1 \rangle = \langle \psi_{\alpha}, \psi_{\boldsymbol{0}} \rangle = 0$。

有了这个正交归一基，任何属于 $L^2(\mu)$ 空间的随机输出 $Y(\boldsymbol{\xi})$ 都可以唯一地表示为以下级数形式，该级数在 $L^2(\mu)$ 范数下收敛：
$$
Y(\boldsymbol{\xi}) = \sum_{\alpha \in \mathcal{A}} c_{\alpha} \psi_{\alpha}(\boldsymbol{\xi})
$$
展开式的系数 $c_{\alpha}$ 的唯一性是由基函数的正交归一性保证的。为了确定某个特定的系数 $c_{\beta}$，我们可以利用**投影原理**，即将 $Y$ 与相应的基函数 $\psi_{\beta}$ 做内积：
$$
\langle Y, \psi_{\beta} \rangle = \left\langle \sum_{\alpha \in \mathcal{A}} c_{\alpha} \psi_{\alpha}, \psi_{\beta} \right\rangle = \sum_{\alpha \in \mathcal{A}} c_{\alpha} \langle \psi_{\alpha}, \psi_{\beta} \rangle = \sum_{\alpha \in \mathcal{A}} c_{\alpha} \delta_{\alpha\beta} = c_{\beta}
$$
因此，每个系数都是 $Y$ 在相应基函数上的投影：
$$
c_{\alpha} = \langle Y, \psi_{\alpha} \rangle = \mathbb{E}[Y(\boldsymbol{\xi})\psi_{\alpha}(\boldsymbol{\xi})]
$$
这个简洁而强大的框架是 gPCE 理论的基石，它将一个可能复杂的模型响应的随机性，编码到一组确定的系数 $c_{\alpha}$ 中。[@problem_id:3411038]

### 构建基函数：维纳-阿斯基方案

gPCE 的一个核心优势在于其基函数的选择不是任意的，而是与输入随机变量的概率分布“量身定制”的。这种对应关系通过所谓的**维纳-阿斯基多项式体系**（Wiener-Askey scheme）来系统化。该体系为符合特定分布类型的随机变量，指定了相应的正交多项式族。关键在于，这些经典正交多项式的权重函数，正好与特定概率分布的概率密度函数（PDF）相对应。

当输入向量 $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$ 的分量是相互独立的随机变量时，其联合 PDF 是边缘 PDF 的乘积，$w(\boldsymbol{\xi}) = \prod_{i=1}^d w_i(\xi_i)$。此时，多元正交基函数 $\psi_{\alpha}(\boldsymbol{\xi})$ 可以方便地构造为一维正交多项式 $\psi_{\alpha_i}^{(i)}(\xi_i)$ 的张量积：
$$
\psi_{\alpha}(\boldsymbol{\xi}) = \prod_{i=1}^d \psi_{\alpha_i}^{(i)}(\xi_i)
$$
其中，每个一维多项式族 $\{\psi_k^{(i)}\}_{k=0}^\infty$ 都是关于其对应输入 $\xi_i$ 的概率密度函数 $w_i(\xi_i)$ 正交的。

以下是维纳-阿斯基方案中两个最常见的例子：
1.  **高斯随机变量**：如果输入 $\xi_i$ 服从标准正态分布 $\mathcal{N}(0,1)$，其 PDF 为 $w_i(x) = \frac{1}{\sqrt{2\pi}} \exp(-x^2/2)$。与之对应的正交多项式是**概率论者赫米特多项式**（Probabilists' Hermite polynomials），记作 $He_k(x)$。
2.  **均匀随机变量**：如果输入 $\xi_i$ 服从标准均匀分布 $\text{Uniform}(-1,1)$，其 PDF 为 $w_i(x) = 1/2$，支撑域为 $[-1, 1]$。与之对应的正交多项式是**勒让德多项式**（Legendre polynomials），记作 $P_k(x)$。

例如，在一个多物理场耦合仿真中，如果一个不确定参数由标准正态变量 $\xi_1$ 描述，另一个由标准均匀变量 $\xi_2$ 描述，那么构建 gPCE 的正确基函数将是赫米特多项式与勒让德多项式的张量积。内积的定义直接使用相应的 PDF 作为权重函数，这确保了所选基函数的正交性。[@problem_id:3523231]

### 处理复杂输入

在许多实际工程和科学问题中，不确定输入并非总是独立的或具有简单的分布。PCE 框架可以通过一些预处理步骤来优雅地处理这些复杂情况。

#### 关联输入：纳塔夫变换

标准 gPCE 框架依赖于输入变量的独立性来构建张量积基函数。当输入变量 $\boldsymbol{\Xi}$ 是相互关联的，即其协方差矩阵 $\boldsymbol{\Sigma}$ 非对角时，直接应用张量积基是错误的。**纳塔夫变换**（Nataf transformation）是一种将关联随机向量 $\boldsymbol{\Xi}$ 转换为一组独立标准随机向量 $\mathbf{Z}$ 的标准方法。

对于输入向量 $\boldsymbol{\Xi}$ 服从多元高斯分布 $\mathcal{N}(\mathbf{0}, \boldsymbol{\Sigma})$ 的重要特例，纳塔夫变换简化为一个线性的“白化”或“去相关”变换。因为对于高斯变量，不相关等价于独立，我们的目标是找到一个矩阵 $\mathbf{A}$ 使得 $\mathbf{Z} = \mathbf{A}\boldsymbol{\Xi}$ 的协方差矩阵为单位矩阵 $\mathbf{I}$。这可以通过多种矩阵分解实现：

1.  **Cholesky 分解**：由于协方差矩阵 $\boldsymbol{\Sigma}$ 是对称正定的，它可以唯一地分解为 $\boldsymbol{\Sigma} = \mathbf{L}\mathbf{L}^\top$，其中 $\mathbf{L}$ 是一个下三角矩阵。选择变换矩阵为 $\mathbf{A} = \mathbf{L}^{-1}$，我们得到 $\mathbf{Z} = \mathbf{L}^{-1}\boldsymbol{\Xi}$，它服从标准正态分布 $\mathcal{N}(\mathbf{0}, \mathbf{I})$。

2.  **特征值分解**：我们也可以使用 $\boldsymbol{\Sigma}$ 的谱分解 $\boldsymbol{\Sigma} = \mathbf{V}\boldsymbol{\Lambda}\mathbf{V}^\top$，其中 $\mathbf{V}$ 是由特征向量构成的正交矩阵，$\boldsymbol{\Lambda}$ 是由正特征值构成的对角矩阵。选择变换矩阵为 $\mathbf{A} = \boldsymbol{\Lambda}^{-1/2}\mathbf{V}^\top$，我们得到 $\mathbf{Z} = \boldsymbol{\Lambda}^{-1/2}\mathbf{V}^\top\boldsymbol{\Xi}$，它同样服从 $\mathcal{N}(\mathbf{0}, \mathbf{I})$。

一旦将原始的关联输入 $\boldsymbol{\Xi}$ 转换为了独立的标准正态输入 $\mathbf{Z}$，我们就可以在新的 $\mathbf{Z}$ 空间中安全地构建 PCE，此时应使用赫米特多项式基。模型的响应现在被视为 $\mathbf{Z}$ 的函数，即 $Q(\boldsymbol{\Xi}) = Q(\mathbf{A}^{-1}\mathbf{Z}) = \tilde{Q}(\mathbf{Z})$。[@problem_id:3341898]

#### 空间分布输入：卡尔亨-洛伊展开

当不确定性不是由少数几个标量参数引起，而是由一个随机场（例如，在空间上随机变化的材料属性 $\epsilon(\mathbf{r}, \omega)$）引起时，我们面临着一个无限维的随机输入空间。直接对随机场进行参数化是不可行的。**卡尔亨-洛伊（Karhunen-Loève, K-L）展开**为此提供了一个最优的降维工具。

对于一个二阶随机场（即均值和协方差有界），K-L 展开将其表示为一组确定性空间模式 $\phi_n(\mathbf{r})$ 和一组不相关随机变量 $\xi_n(\omega)$ 的线性组合。具体来说，它将随机场分解为其均值场 $m(\mathbf{r})$ 和一个零均值波动的和：
$$
\epsilon(\mathbf{r}, \omega) = m(\mathbf{r}) + \sum_{n=1}^{\infty} \sqrt{\lambda_n} \phi_n(\mathbf{r}) \xi_n(\omega)
$$
这里的空间模式 $\phi_n(\mathbf{r})$ 和标量 $\lambda_n$ 是通过求解一个积分特征值问题得到的，该问题的核是随机场的协方差函数 $C(\mathbf{r}, \mathbf{r}')$：
$$
\int_D C(\mathbf{r}, \mathbf{r}') \phi_n(\mathbf{r}') d\mathbf{r}' = \lambda_n \phi_n(\mathbf{r})
$$
通过 K-L 展开，原始的无限维随机场被表示为一组可数的、不相关的（通常被归一化为正交归一的）随机变量 $\xi_n$。然后，我们可以截断这个级数，只保留最重要的少数几个模式（即对应较大特征值 $\lambda_n$ 的模式），从而实现有效的降维。这些随机变量 $\xi_n$ 接着就可以作为有限维 gPCE 的输入。K-L 展开与 gPCE 的结合，构成了一个从随机场建模到不确定性传播的强大工作流。[@problem_id:3341904]

### 实际实现：截断与系数估计

理论上的 PCE 是一个无穷级数。在计算中，我们必须将其截断为一个有限和，并确定展开式中的未知系数。

#### 有限近似：截断方案

截断 PCE 级数意味着选择一个有限的多元索引集 $\mathcal{A}_p \subset \mathbb{N}_0^d$，其中 $p$ 是一个控制展开式丰富度的参数，通常是多项式的最高阶数。最常见的截断方案有两种：

1.  **总阶数（Total-Degree, TD）截断**：此方案包含所有总阶数不超过 $p$ 的多项式。总阶数定义为多元索引各分量之和。其索引集为：
    $$
    \mathcal{A}_p^{\mathrm{TD}} = \left\{ \alpha \in \mathbb{N}_0^d : \sum_{j=1}^d \alpha_j \le p \right\}
    $$
    此集合的大小（即 PCE 中的项数）为 $M = |\mathcal{A}_p^{\mathrm{TD}}| = \binom{d+p}{p}$。这个数字随着维度 $d$ 的增加而急剧增长，这种现象被称为“维数灾难”。

2.  **双曲交叉（Hyperbolic-Cross, HC）截断**：为了缓解维数灾难，可以使用双曲交叉截断。其背后的假设是，高阶交互项（即多个变量同时具有高阶多项式）的贡献通常较小，可以被忽略。一个典型的 HC 索引集定义为：
    $$
    \mathcal{A}_p^{\mathrm{HC}} = \left\{ \alpha \in \mathbb{N}_0^d : \prod_{j=1}^d (\alpha_j + 1) \le p+1 \right\}
    $$
    这个集合的形状在索引空间中呈双曲线状，它优先包含那些涉及少数变量的高阶项，同时舍弃了许多涉及多变量的高阶交互项。其项数 $|\mathcal{A}_p^{\mathrm{HC}}|$ 的增长速度远慢于 TD 截断，大致为 $O(p (\log p)^{d-1})$，从而在许多高维问题中显著减少了计算负担。[@problem_id:3341902]

#### 计算系数：侵入式与非侵入式方法

确定 PCE 系数 $c_{\alpha}$ 主要有两种策略：

**侵入式方法（Stochastic Galerkin Methods）**
侵入式方法的核心思想是将 PCE 形式的解直接代入控制方程（例如，一组偏微分方程）。然后，利用伽辽金投影，即要求方程的残差与 PCE 基函数的子空间正交。这会产生一个庞大的、耦合的确定性方程组，其未知数是所有 PCE 的系数场。求解这个耦合系统可以一次性得到所有系数。这种方法的优点是通常具有很高的精度和效率，特别是对于低维问题。然而，它需要对现有的确定性求解器代码进行深度修改（即“侵入”），以组装和求解这个新的、更大的耦合系统，这在实践中可能非常困难。[@problem_id:3523236]

**非侵入式方法（Non-Intrusive Methods）**
非侵入式方法将原始的确定性求解器视为一个“黑箱”，只需在选定的一组输入样本点 $\boldsymbol{\xi}^{(n)}$ 上运行它，得到相应的输出 $Y(\boldsymbol{\xi}^{(n)})$。然后，利用这些输入-输出对来推断 PCE 系数。这种方法无需修改求解器代码，因此具有极大的灵活性和易用性。主要有两种非侵入式技术：

1.  **基于投影的求积（Projection via Quadrature）**：此方法直接使用系数的投影公式 $c_{\alpha} = \mathbb{E}[Y\psi_{\alpha}]$。公式中的期望（一个高维积分）通过数值求积来近似。为了获得高精度，通常使用高斯求积（Gauss quadrature），它能用较少的点精确地积分多项式。然而，为了精确计算一个 $d$ 维问题中所有阶数最高为 $p$ 的 PCE 系数，通常需要一个张量积求积网格。这种网格的点数会随维度 $d$ 指数增长，即 $N \approx (p+1)^d$，再次导致“维数灾难”。[@problem_id:3341911]

2.  **基于回归的最小二乘（Regression via Least-Squares）**：此方法将问题转化为一个线性回归问题。通过在 $N$ 个样本点上评估 PCE，我们得到一个线性系统 $\mathbf{y} \approx \boldsymbol{\Psi}\mathbf{c}$，其中 $\mathbf{y}$ 是模型在样本点上的输出向量，$\boldsymbol{\Psi}$ 是在这些点上评估的基多项式构成的设计矩阵，$\mathbf{c}$ 是待求的系数向量。通过求解最小二乘问题 $\min_{\mathbf{c}} \|\boldsymbol{\Psi}\mathbf{c} - \mathbf{y}\|_2^2$ 来估计系数。为了得到一个稳定且唯一的解，样本数量 $N$ 必须至少等于未知系数的数量 $M$，通常建议使用过采样，例如 $N \ge 2M$。由于 $M$（例如，对于 TD 截断是 $\binom{d+p}{p}$）随维度 $d$ 的增长是多项式的，远慢于张量积求积的指数增长，因此最小二乘回归法在高维问题中通常比求积法需要更少的模型评估次数，从而在一定程度上缓解了维数灾难。[@problem_id:3341911] [@problem_id:3523236]

### 利用展开式：为不确定性量化进行后处理

一旦 PCE 系数被确定，我们就获得了一个关于模型响应的廉价且可解析的代理模型。PCE 的巨大威力在于，许多重要的统计量和敏感度信息可以几乎无额外成本地从这些系数中直接推导出来。

#### 统计矩

由于基函数的正交归一性，计算输出 $Y$ 的统计矩变得非常简单。

*   **均值（Mean）**：$Y$ 的均值就是其 PCE 的零阶系数，因为所有高阶基函数的期望均为零。
    $$
    \mathbb{E}[Y] = \mathbb{E}\left[\sum_{\alpha} c_{\alpha} \psi_{\alpha}\right] = \sum_{\alpha} c_{\alpha} \mathbb{E}[\psi_{\alpha}] = c_{\boldsymbol{0}}\mathbb{E}[\psi_{\boldsymbol{0}}] = c_{\boldsymbol{0}}
    $$

*   **方差（Variance）**：$Y$ 的方差是所有高阶（非零阶）系数的平方和。这源于方差的定义 $\mathrm{Var}(Y) = \mathbb{E}[Y^2] - (\mathbb{E}[Y])^2$ 和基函数的正交归一性。
    $$
    \mathrm{Var}(Y) = \left(\sum_{\alpha} c_{\alpha}^2\right) - c_{\boldsymbol{0}}^2 = \sum_{\alpha \neq \boldsymbol{0}} c_{\alpha}^2
    $$
    这个结果也被称为帕塞瓦尔定理（Parseval's theorem）在 PCE 背景下的体现。例如，对于一个二阶展开式 $Y(\xi) = c_0 \psi_0 + c_1 \psi_1 + c_2 \psi_2$，其均值为 $c_0$，方差为 $c_1^2 + c_2^2$。这种直接从系数计算矩的能力，是 PCE 相较于传统的蒙特卡洛采样的主要优势之一。[@problem_id:2589461]

#### 敏感度分析：索博尔指数

PCE 的方差分解特性使其成为进行全局敏感度分析（Global Sensitivity Analysis, GSA）的理想工具。**索博尔指数**（Sobol' indices）是一种基于方差的 GSA 度量，它量化了单个输入或一组输入对总输出方差的贡献。

PCE 结构允许我们通过对系数进行分组求和来解析地计算索博尔指数。

*   **一阶索博尔指数 ($S_i$)**：它衡量了输入变量 $\xi_i$ 单独对总方差的贡献。在 PCE 中，这对应于那些只依赖于 $\xi_i$ 的基函数所贡献的方差部分。
    $$
    S_i = \frac{\mathrm{Var}(\mathbb{E}[Y \mid \xi_i])}{\mathrm{Var}(Y)} = \frac{\sum_{\alpha \in \mathcal{A}_i} c_{\alpha}^2}{\sum_{\beta \neq \boldsymbol{0}} c_{\beta}^2}
    $$
    其中 $\mathcal{A}_i$ 是只与 $\xi_i$ 相关的多项式索引集（即，$\alpha_i > 0$ 且对所有 $j \neq i$ 有 $\alpha_j=0$）。

*   **总效应索博尔指数 ($T_i$)**：它衡量了输入变量 $\xi_i$ 通过其自身以及与其他变量的所有交互作用对总方差的贡献。这对应于 PCE 中所有涉及 $\xi_i$ 的项（即 $\alpha_i > 0$）所贡献的方差。
    $$
    T_i = \frac{\mathbb{E}(\mathrm{Var}[Y \mid \boldsymbol{\xi}_{-i}])}{\mathrm{Var}(Y)} = \frac{\sum_{\alpha \in \mathcal{A}_{\sim i}} c_{\alpha}^2}{\sum_{\beta \neq \boldsymbol{0}} c_{\beta}^2}
    $$
    其中 $\boldsymbol{\xi}_{-i}$ 表示除 $\xi_i$ 以外的所有输入，$\mathcal{A}_{\sim i}$ 是所有满足 $\alpha_i > 0$ 的索引集。

从 PCE 系数计算索博尔指数的这种能力，使得 GSA 成为 PCE 工作流中一个简单且高效的后处理步骤。[@problem_id:3341860]

### 高级主题：处理非光滑性与多单元 PCE

标准 PCE 在模型响应 $Y(\boldsymbol{\xi})$ 作为 $\boldsymbol{\xi}$ 的函数是光滑（例如，解析）时，表现出谱收敛性（即误差随多项式阶数指数下降）。然而，许多物理系统在特定参数阈值处会发生**状态转变**（regime change），导致其响应函数出现不光滑（例如，导数不连续的“扭结”）甚至不连续。一个典型的例子是电磁波导中的传播模式，当介电常数等参数越过一个临界值时，模式会从传播状态突变为衰减状态，这会导致传播常数的大小在其导数上不连续。[@problem_id:3341868]

当用全局多项式去逼近这种非光滑函数时，PCE 会遭遇类似于傅里叶级数中的**吉布斯现象**（Gibbs phenomenon）：在不光滑点附近出现伪振荡，且收敛速度从谱收敛退化为缓慢的代数收敛。

**多单元多项式混沌展开**（Multi-Element PCE, ME-PCE）是为解决这一问题而设计的先进技术。其核心思想类似于有限元方法（FEM）：不是用一个高阶多项式来逼近整个定义域，而是将随机输入参数的支撑域划分为多个不重叠的“单元”（elements）。关键在于，划分的边界要与函数不光滑的位置对齐。

这样，在每个单元内部，函数都是光滑的。我们可以在每个单元上独立地构建一个**局部 PCE**。这个局部 PCE 使用的是针对该单元上的**条件概率测度**而正交的多项式基。整个函数则被表示为这些分段多项式展开的集合，通过指示函数拼接在一起：
$$
Y(\boldsymbol{\xi}) \approx \sum_{i=1}^{M} \left( \sum_{k=0}^{P_i} c_{i,k} \Psi_{i,k}(\boldsymbol{\xi}) \right) \mathbb{I}_{\mathcal{D}_i}(\boldsymbol{\xi})
$$
其中 $\mathcal{D}_i$ 是第 $i$ 个单元，$\mathbb{I}_{\mathcal{D}_i}$ 是其指示函数，$\{\Psi_{i,k}\}$ 是在 $\mathcal{D}_i$ 上关于条件测度正交的局部基。通过将不光滑性隔离在单元边界上，ME-PCE 可以在每个光滑的单元内恢复快速的谱收敛，从而以远低于标准全局 PCE 的计算成本获得高精度近似。[@problem_id:3341868]