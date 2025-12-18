## 引言
在现代计算科学与工程中，不确定性无处不在——从材料属性的微小变化到环境条件的随机波动。准确量化这些不确定性对系统性能的影响，即不确定性量化（UQ），对于设计可靠、稳健的系统至关重要。然而，诸如蒙特卡罗模拟等传统方法往往需要巨大的计算成本，尤其是在处理复杂模型时。[多项式混沌展开](@entry_id:162793)（Polynomial Chaos Expansion, PCE）作为一种先进的[谱方法](@entry_id:141737)，为这一挑战提供了高效且深刻的解决方案，它不仅能预测不确定性的传播，还能揭示其背后的关键驱动因素。

本文旨在系统性地介绍通过[多项式混沌](@entry_id:196964)进行[不确定性量化](@entry_id:138597)的理论与实践。通过学习本文，读者将能够掌握从基本原理到高级应用的完整知识体系。

我们将分三个章节展开：第一章“原理与机制”将深入剖析PCE的数学基础，解释如何用[正交多项式](@entry_id:146918)构建代理模型并计算其系数。第二章“应用与跨学科联系”将通过一系列来自[结构力学](@entry_id:276699)、电子工程、气候科学等领域的实例，展示PCE在解决实际问题中的强大能力和广泛适用性。最后，在第三章“动手实践”中，您将通过具体的计算练习，将理论知识转化为解决问题的实践技能。让我们一同开启探索PCE世界的旅程，学习如何驾驭不确定性。

## 原理与机制

本章旨在深入探讨[多项式混沌展开](@entry_id:162793) (Polynomial Chaos Expansion, PCE) 的核心原理与关键机制。在上一章介绍其基本概念和应用背景之后，我们将系统性地剖析 PCE 作为一种[不确定性量化](@entry_id:138597)工具的数学基础、实施策略、强大功能及其固有的局限性。我们将从不确定性的数学表示出发，逐步构建起一个完整而严谨的 PCE 理论框架。

### 基础：使用[正交多项式](@entry_id:146918)表示不确定性

[多项式混沌展开](@entry_id:162793)的核心思想，是将一个依赖于随机输入向量 $\boldsymbol{\xi} \in \mathbb{R}^d$ 的模型输出（或称关心量，Quantity of Interest, QoI）$Y(\boldsymbol{\xi})$ 表示为一个谱展开。这个展开是基于一组特殊的多项式[基函数](@entry_id:170178) $\{\Psi_{\alpha}(\boldsymbol{\xi})\}$ 构建的：

$Y(\boldsymbol{\xi}) \approx \widehat{Y}(\boldsymbol{\xi}) = \sum_{\alpha \in \mathcal{A}} c_{\alpha} \Psi_{\alpha}(\boldsymbol{\xi})$

在此表达式中，$\mathcal{A}$ 是一个有限的多[指标集](@entry_id:268489) (multi-index set)，$c_{\alpha}$ 是确定性的展开系数，而 $\Psi_{\alpha}(\boldsymbol{\xi})$ 则是关于[随机变量](@entry_id:195330) $\boldsymbol{\xi}$ 的多元多项式。多指标 $\alpha = (\alpha_1, \dots, \alpha_d)$ 是一个非负整数向量，用于标识每个[基函数](@entry_id:170178)。

这些[基函数](@entry_id:170178)并非任意选取，而是必须满足相对于输入[随机变量](@entry_id:195330)的[概率测度](@entry_id:190821)的 **正交性 (orthogonality)**。更具体地说，我们需要定义一个带权重的[内积](@entry_id:158127)。对于两个关于 $\boldsymbol{\xi}$ 的函数 $f$ 和 $g$，其[内积](@entry_id:158127)定义为它们乘积的数学期望：

$\langle f, g \rangle = \mathbb{E}[f(\boldsymbol{\xi})g(\boldsymbol{\xi})] = \int_{\mathcal{S}_{\boldsymbol{\xi}}} f(\boldsymbol{\xi})g(\boldsymbol{\xi})\rho(\boldsymbol{\xi}) d\boldsymbol{\xi}$

其中，$\rho(\boldsymbol{\xi})$ 是 $\boldsymbol{\xi}$ 的[联合概率密度函数](@entry_id:267139) (PDF)，$\mathcal{S}_{\boldsymbol{\xi}}$ 是其支撑集。

PCE 所用的[基函数](@entry_id:170178) $\{\Psi_{\alpha}\}$ 必须是关于这个[内积](@entry_id:158127) **标准正交的 (orthonormal)**。这意味着任意两个[基函数](@entry_id:170178)的内積满足如下关系 ：

$\langle \Psi_{\alpha}, \Psi_{\beta} \rangle = \mathbb{E}[\Psi_{\alpha}(\boldsymbol{\xi})\Psi_{\beta}(\boldsymbol{\xi})] = \delta_{\alpha\beta}$

其中 $\delta_{\alpha\beta}$ 是克罗内克 (Kronecker) delta，当多指标 $\alpha = \beta$ 时为 $1$，否则为 $0$。这个条件蕴含了两层意思：
1.  **正交性**：当 $\alpha \neq \beta$ 时，$\langle \Psi_{\alpha}, \Psi_{\beta} \rangle = 0$。
2.  **归一性**：对于任意 $\alpha$，$\langle \Psi_{\alpha}, \Psi_{\alpha} \rangle = \|\Psi_{\alpha}\|^2 = 1$。

通常，第零阶多项式 $\Psi_{\boldsymbol{0}}$ (对应于多指标 $\boldsymbol{0}=(0,\dots,0)$) 是一个常数，且根据归一性要求，$\Psi_{\boldsymbol{0}}=1$。这种[标准正交性](@entry_id:267887)是 PCE 方法高效性和诸多优良性质的基石，我们将在后续章节中反复看到它的威力。

### Wiener-Askey 框架：选择合适的多项式

[基函数](@entry_id:170178)的选择并非随意，而是与输入[随机变量](@entry_id:195330)的[概率分布](@entry_id:146404)紧密相关。**Wiener-Askey 框架** 为此提供了经典的指导，它为一系列常见的[概率分布](@entry_id:146404)指定了相应的[正交多项式](@entry_id:146918)族。当输入变量是[相互独立](@entry_id:273670)的，即 $\rho(\boldsymbol{\xi}) = \prod_{i=1}^d \rho_i(\xi_i)$ 时，多元[正交多项式](@entry_id:146918)可以方便地通过一元[正交多项式](@entry_id:146918)的张量积构造出来：$\Psi_{\alpha}(\boldsymbol{\xi}) = \prod_{i=1}^d \psi_{\alpha_i}^{(i)}(\xi_i)$。

Wiener-Askey 框架中的一些关键配对包括 ：
-   **高斯分布 (Gaussian)** $\longleftrightarrow$ **Hermite 多项式**
-   **[均匀分布](@entry_id:194597) (Uniform)** $\longleftrightarrow$ **Legendre 多项式**
-   **Gamma [分布](@entry_id:182848)** $\longleftrightarrow$ **Laguerre 多项式**
-   **Beta [分布](@entry_id:182848)** $\longleftrightarrow$ **Jacobi 多项式**

然而，在实际工程问题中，输入参数的[分布](@entry_id:182848)可能不属于上述经典类型，例如[对数正态分布](@entry_id:261888) (lognormal distribution)，它常用于描述必须为正值的物理量（如材料的[杨氏模量](@entry_id:140430)）。此时，我们可以借助 **同概率变换 (isoprobabilistic transform)** 的思想。其核心是将非经典[分布](@entry_id:182848)的[随机变量](@entry_id:195330)映射到一个具有已知[正交多项式](@entry_id:146918)的经典[分布](@entry_id:182848)变量上。

以一个服从[对数正态分布](@entry_id:261888)的杨氏模量 $E$ 为例，根据其定义，$\ln E$ 服从[高斯分布](@entry_id:154414)，即 $\ln E \sim \mathcal{N}(\mu_g, \sigma_g^2)$。我们可以定义一个标准正态[随机变量](@entry_id:195330) $\xi \sim \mathcal{N}(0,1)$，并建立如下映射关系：

$\xi = \frac{\ln E - \mu_g}{\sigma_g} \quad \iff \quad E(\xi) = \exp(\mu_g + \sigma_g \xi)$

通过这个变换，我们将原始模型 $Y(E)$ 转化为了一个以标准正态变量为输入的新模型 $Y(E(\xi))$。此时，我们就可以根据 Wiener-Askey 框架，选用 Hermite 多项式[基函数](@entry_id:170178) $\{\Psi_{\alpha}(\xi)\}$ 来构建 PCE。对于更复杂的多维相关非[高斯变量](@entry_id:276673)，可以采用 Nataf 变换等方法将其转化为相关的标准[高斯变量](@entry_id:276673)，再通过线性变换解耦，最终回到基于独立标准[高斯变量](@entry_id:276673)和 Hermite 多项式的 PCE 框架上来 。

### 计算 PCE 系数：投影与最优性

确定了合适的[基函数](@entry_id:170178)后，下一步是计算展开式中的系数 $\{c_{\alpha}\}$。从数学上看，PCE 是将模型输出 $Y(\boldsymbol{\xi})$ 在 $L^2$ 空间中投影到由[基函数](@entry_id:170178) $\{\Psi_{\alpha}\}_{\alpha \in \mathcal{A}}$ 张成的多项式[子空间](@entry_id:150286)上。为了找到最优的系数，我们要求投影误差 $e = Y - \widehat{Y}$ 与该[子空间](@entry_id:150286)中的任何函数都正交。这等价于要求误差与每一个[基函数](@entry_id:170178)都正交：

$\langle Y - \sum_{\alpha \in \mathcal{A}} c_{\alpha} \Psi_{\alpha}, \Psi_{\beta} \rangle = 0, \quad \forall \beta \in \mathcal{A}$

利用[内积](@entry_id:158127)的线性性质，上式可整理为一个[线性方程组](@entry_id:148943)，即“正规方程 (normal equations)”：

$\sum_{\alpha \in \mathcal{A}} c_{\alpha} \langle \Psi_{\alpha}, \Psi_{\beta} \rangle = \langle Y, \Psi_{\beta} \rangle, \quad \forall \beta \in \mathcal A$

这是一个形式为 $Gc=f$ 的线性系统，其中 $G$ 是 Gram 矩阵，其元素为 $G_{\beta\alpha} = \langle \Psi_{\alpha}, \Psi_{\beta} \rangle$。

此时，**[基函数](@entry_id:170178)的[标准正交性](@entry_id:267887)**极大地简化了这个问题 。由于 $\langle \Psi_{\alpha}, \Psi_{\beta} \rangle = \delta_{\alpha\beta}$，Gram 矩阵 $G$ 变成了单位矩阵。[正规方程](@entry_id:142238)因此解耦，每个系数都可以独立地通过简单的投影积分直接计算：

$c_{\beta} = \langle Y, \Psi_{\beta} \rangle = \mathbb{E}[Y(\boldsymbol{\xi})\Psi_{\beta}(\boldsymbol{\xi})]$

这一简洁的公式是 PCE 方法的核心。它表明，在标准正交基下，PCE 系数就是模型输出与对应[基函数](@entry_id:170178)乘[积的期望](@entry_id:190023)。这种投影得到的 PCE 近似 $\widehat{Y}$ 是在所有由该[基函数](@entry_id:170178)构成的多项式中，对原始函数 $Y$ 的 **最佳均方逼近 (best mean-square approximation)**。换言之，它使得 $L^2$ [误差范数](@entry_id:176398) $\|e\|_{L^2} = \|Y - \widehat{Y}\|_{L^2}$ 最小化。如果[基函数](@entry_id:170178)只是正交但未归一化，即 $\langle \Psi_{\alpha}, \Psi_{\beta} \rangle = h_{\alpha}\delta_{\alpha\beta}$，系数的计算公式会略有调整：$c_{\beta} = \langle Y, \Psi_{\beta} \rangle / h_{\beta}$。如果[基函数](@entry_id:170178)非正交，则必须求解一个完全耦合 (fully coupled) 的[线性方程组](@entry_id:148943) 。

### 实现策略：侵入式与非侵入式方法

计算 PCE 系数的关键在于求解投影积分 $\mathbb{E}[Y(\boldsymbol{\xi})\Psi_{\beta}(\boldsymbol{\xi})]$。实践中主要有两大类方法：侵入式方法和非侵入式方法。

#### 侵入式与非侵入式方法的权衡

**侵入式随机 Galerkin 方法 (Intrusive Stochastic Galerkin Method)** 将 PCE 表达式直接代入模型的控制方程（如有限元法的[方程组](@entry_id:193238)）。然后，利用 Galerkin 投影原理，要求方程的残差与 PCE [基函数](@entry_id:170178)在随机空间中正交。这会产生一个规模更大的、耦合的确定性[方程组](@entry_id:193238)，其未知量是 PCE 系数场（例如，每个节点位移的 PCE 系数）。
-   **优点**：理论上，如果积分精确计算，它能直接求得在所选多项式空间中的 $L^2$ 最优解，精度较高。
-   **缺点**：该方法是“侵入式”的，因为它需要对现有确定性求解器的源代码进行深度修改，以组装和求解新的大型耦合系统。对于复杂的“祖传代码”(legacy codes)，这在工程上往往不切实际或成本过高 。

**非侵入式方法 (Non-intrusive Methods)** 将确定性求解器视为一个“黑箱”，仅通过多次调用它来获取模型在特定输入参数下的响应。
-   **优点**：无需修改求解器代码，实现简单，通用性强。此外，由于每次模型评估都是独立的，该过程是“易于并行的 (embarrassingly parallel)”，非常适合在现代[并行计算](@entry_id:139241)平台上高效执行 。
-   **缺点**：其精度依赖于[采样策略](@entry_id:188482)，会引入额外的采样或[积分误差](@entry_id:171351)。

非侵入式方法中最常用的是[随机配置法](@entry_id:174778)和回归法。我们将重点介绍基于[数值积分](@entry_id:136578)的[随机配置法](@entry_id:174778)。

#### 非侵入式[随机配置法](@entry_id:174778)：一个计算实例

[随机配置法](@entry_id:174778) (Stochastic Collocation) 使用[数值积分](@entry_id:136578)（正交）来近似系数积分 $c_{\beta} = \mathbb{E}[Y(\boldsymbol{\xi})\Psi_{\beta}(\boldsymbol{\xi})]$。例如，对于单变量 $\xi$，积分可写为：

$c_{\beta} = \int Y(\xi)\Psi_{\beta}(\xi)\rho(\xi)d\xi \approx \sum_{i=1}^{N} Y(\xi_i)\Psi_{\beta}(\xi_i) w_i$

其中，$\{\xi_i, w_i\}$ 是与权重函数 $\rho(\xi)$ 相应的 $N$ 点数值积分的节点和权重。例如，对于服从[均匀分布](@entry_id:194597)的 $\xi$，应使用 Gauss-Legendre 正交；对于高斯分布，则使用 Gauss-Hermite 正交。

让我们通过一个实例来理解这个过程 。考虑一个一维弹性杆，其[杨氏模量](@entry_id:140430) $E(\xi) = E_0(1+\beta\xi)$ 存在不确定性，其中 $\xi \sim \mathcal{U}(-1,1)$，$\beta=\frac{1}{5}$。我们关心的量是归一化的杆端位移 $Q(\xi) = \frac{1}{1+\beta\xi}$。我们希望使用3点 Gauss-Legendre 正交来计算其 PCE 的二阶系数 $c_2$。[基函数](@entry_id:170178)为标准化的 Legendre 多项式 $\psi_2(\xi) = \frac{\sqrt{5}}{2}(3\xi^2-1)$。
系数的精确表达式为（对于 $\mathcal{U}(-1,1)$，$\rho(\xi) = 1/2$）：

$c_2 = \langle Q(\xi), \psi_2(\xi) \rangle = \frac{1}{2}\int_{-1}^{1} \frac{1}{1+\frac{1}{5}\xi} \cdot \frac{\sqrt{5}}{2}(3\xi^2-1) d\xi$

使用给定的三点 Gauss-Legendre 节点 $\{\xi_1=0, \xi_2=\sqrt{3/5}, \xi_3=-\sqrt{3/5}\}$ 和权重 $\{w_1=8/9, w_2=5/9, w_3=5/9\}$，我们近似这个积分为：

$c_2 \approx \frac{1}{2} \sum_{i=1}^3 w_i Q(\xi_i) \psi_2(\xi_i)$

通过在每个节点 $\xi_i$ 上调用“黑箱”求解器（这里是简单的函数求值 $Q(\xi_i)$），并计算出 $\psi_2(\xi_i)$ 的值，然后加权求和，最终可以得到 $c_2$ 的近似值。经过计算，结果为 $c_2 \approx \frac{2\sqrt{5}}{183}$。这个例子清晰地展示了非侵入式方法的工作流程：通过在精心选择的采样点处运行确定性模型，然后对结果进行后处理来获得 PCE 系数。

值得注意的是，若要精确计算一个最高次数为 $p$ 的 PCE 系数，我们需要确保[数值积分](@entry_id:136578)能够精确地计算 $Y(\xi)\Psi_{\beta}(\xi)$ 的积分。如果 $Y(\xi)$ 本身是一个次数不超过 $p$ 的多项式，那么被积函数 $Y(\xi)\Psi_{\beta}(\xi)$ 的次数最高为 $2p$。因此，所选的[数值积分](@entry_id:136578)规则必须对所有次数不超过 $2p$ 的多项式都是精确的 。

#### [维数灾难](@entry_id:143920)

两种方法都面临着“[维数灾难](@entry_id:143920)”(curse of dimensionality) 的挑战，但其表现形式不同 。
-   对于 **侵入式 Galerkin 方法**，成本取决于 PCE [基函数](@entry_id:170178)的数量。对于 $d$ 个维度的 $p$ 阶总次数截断，[基函数](@entry_id:170178)数量为 $\binom{p+d}{d}$。这个数量随维度 $d$ 以多项式 $O(d^p)$ 的速度增长，这是一种[组合爆炸](@entry_id:272935)。
-   对于 **非侵入式[张量积](@entry_id:140694)[配置法](@entry_id:142690)**，成本取决于采样点的总数。如果每个维度使用 $q$ 个点，总点数即为 $q^d$，随维度 $d$ [指数增长](@entry_id:141869)。这种增长速度远快于[多项式增长](@entry_id:177086)，使得高维问题（例如 $d>10$）的计算成本迅速变得无法承受。[稀疏网格](@entry_id:139655) (sparse grids) 等技术可以缓解但无法根除这一问题。

因此，侵入式方法在低维时可能更精确，但非侵入式方法因其实现简单和易于并行，在实践中（特别是对于已有的大型程序）应用更广，并且是应对中高维问题时各种高级方法（如稀疏 PCE）的基础。

### 利用 PCE 代理模型：为获得洞见进行后处理

一旦 PCE 系数 $\{c_\alpha\}$ 被计算出来，我们就得到了一个原始复杂模型的廉价 **代理模型 (surrogate model)**, $\widehat{Y}(\boldsymbol{\xi}) = \sum c_\alpha \Psi_\alpha(\boldsymbol{\xi})$。对这个代理模型的任何操作都极为迅速，无需再次运行昂贵的原始模型。这使得我们可以高效地执行各种[不确定性量化](@entry_id:138597)任务。

#### 计算[统计矩](@entry_id:268545)

利用基[函数的正交性](@entry_id:160337)，我们可以直接从 PCE 系数解析地计算出模型输出的[统计矩](@entry_id:268545)。
-   **均值 (Mean)**：输出的均值就是第零阶系数，因为所有[高阶基函数](@entry_id:165641)的期望均为零。
    $\mathbb{E}[Y] \approx \mathbb{E}[\widehat{Y}] = \mathbb{E}[c_{\boldsymbol{0}}\Psi_{\boldsymbol{0}} + \sum_{\alpha \ne \boldsymbol{0}} c_{\alpha}\Psi_{\alpha}] = c_{\boldsymbol{0}}\mathbb{E}[\Psi_{\boldsymbol{0}}] = c_{\boldsymbol{0}}$
-   **[方差](@entry_id:200758) (Variance)**：输出的[方差](@entry_id:200758)则是所有非零阶系数的平方和。
    $\mathrm{Var}[Y] \approx \mathrm{Var}[\widehat{Y}] = \mathbb{E}[(\widehat{Y} - c_{\boldsymbol{0}})^2] = \mathbb{E}[(\sum_{\alpha \ne \boldsymbol{0}} c_{\alpha}\Psi_{\alpha})^2] = \sum_{\alpha \ne \boldsymbol{0}, \beta \ne \boldsymbol{0}} c_{\alpha}c_{\beta}\mathbb{E}[\Psi_{\alpha}\Psi_{\beta}] = \sum_{\alpha \ne \boldsymbol{0}} c_{\alpha}^2$

例如，对于一个二阶 PCE $Y(\xi) = u_0\psi_0(\xi) + u_1\psi_1(\xi) + u_2\psi_2(\xi)$，如果系数为 $u_0=2, u_1=-1, u_2=1/2$，那么其均值为 $\mathbb{E}[Y]=u_0=2$，[方差](@entry_id:200758)为 $\mathrm{Var}[Y] = u_1^2 + u_2^2 = (-1)^2 + (1/2)^2 = 5/4$ 。如果 PCE 基底只是正交而非标准正交，即 $\mathbb{E}[\Psi_{\boldsymbol{\alpha}}^2] = \gamma_{\boldsymbol{\alpha}}$，那么[方差](@entry_id:200758)公式需要相应修正为 $\mathrm{Var}[Y] = \sum_{\boldsymbol{\alpha} \ne \boldsymbol{0}} c_{\boldsymbol{\alpha}}^2 \gamma_{\boldsymbol{\alpha}}$ 。

#### 全局敏感度分析

全局敏感度分析 (Global Sensitivity Analysis, GSA) 是 PCE 最强大的应用之一。它旨在量化各个输入变量及其交互作用对输出[方差](@entry_id:200758)的贡献。基于[方差](@entry_id:200758)的 Sobol' 指数是 GSA 的标准度量。PCE 天然地提供了一种函数 ANOVA (Analysis of Variance) 分解，使得 Sobol' 指数可以作为系数计算的“免费”副产品获得，无需额外的模型评估 。

PCE 的总[方差](@entry_id:200758)可以被分解为由单个变量、变量对等引起的贡献。定义一个多指标 $\boldsymbol{\alpha}$ 的支撑集为其非零元素的位置集合, $\mathrm{supp}(\boldsymbol{\alpha}) := \{j \in \{1,\dots,d\} : \alpha_j > 0\}$。
-   **一阶 Sobol' 指数 ($S_i$)**：度量输入 $X_i$ 的“主效应”对总[方差](@entry_id:200758)的贡献。它等于所有仅与 $X_i$ 相关的[基函数](@entry_id:170178)（即 $\mathrm{supp}(\boldsymbol{\alpha})=\{i\}$）的 PCE 系数平方和与总[方差](@entry_id:200758)之比。
    $S_i = \dfrac{\sum_{\boldsymbol{\alpha}:\mathrm{supp}(\boldsymbol{\alpha})=\{i\}} c_{\boldsymbol{\alpha}}^2}{\sum_{\boldsymbol{\beta} \ne \boldsymbol{0}} c_{\boldsymbol{\beta}}^2}$

-   **高阶 Sobol' 指数 ($S_{\mathfrak{u}}$)**：度量一组变量 $\mathfrak{u} \subseteq \{1,\dots,d\}$ 的纯[交互效应](@entry_id:176776)对总[方差](@entry_id:200758)的贡献。
    $S_{\mathfrak{u}} = \dfrac{\sum_{\boldsymbol{\alpha}:\mathrm{supp}(\boldsymbol{\alpha})=\mathfrak{u}} c_{\boldsymbol{\alpha}}^2}{\sum_{\boldsymbol{\beta} \ne \boldsymbol{0}} c_{\boldsymbol{\beta}}^2}$

-   **总效应 Sobol' 指数 ($S_{T_i}$)**：度量输入 $X_i$ 的主效应及其与其他所有变量的交互效应对总[方差](@entry_id:200758)的全部贡献。它等于所有与 $X_i$ 相关的[基函数](@entry_id:170178)（即 $\alpha_i > 0$）的 PCE 系数平方和与总[方差](@entry_id:200758)之比。
    $S_{T_i} = \dfrac{\sum_{\boldsymbol{\alpha}:\alpha_i>0} c_{\boldsymbol{\alpha}}^2}{\sum_{\boldsymbol{\beta} \ne \boldsymbol{0}} c_{\boldsymbol{\beta}}^2}$

这些公式  突显了 PCE 在 GSA 中的巨大优势。一旦系数 $\{c_\alpha\}$ 计算完成，所有敏感度指数都可以通过对系数进行简单的分组和求和来获得。这与传统的局部敏感度分析方法（如基于[有限差分](@entry_id:167874)的梯度计算）形成鲜明对比，后者只能提供模型在某个特定点附近的行为信息，而无法捕捉全局和[交互效应](@entry_id:176776) 。

### 局限性与前沿课题

尽管 PCE 功能强大，但它也并非万能。其核心假设是模型输出可以被全局光滑的多项式很好地近似。当这个假设不成立时，PCE 的性能会显著下降。

一个典型的例子是当模型响应包含 **[不连续性](@entry_id:144108)** 时，例如在传热问题中由于[相变](@entry_id:147324)引起的温度或热流的跳跃。假设模型输出 $u(\xi)$ 在 $\xi^{\star}$ 处有一个[跳跃间断](@entry_id:139886)。使用全局的 Legendre 多项式（或任何其他光滑的[全局基函数](@entry_id:749917)）来近似这个[不连续函数](@entry_id:143848)，会导致类似于傅里葉级数中的 **[吉布斯现象](@entry_id:138701) (Gibbs phenomenon)** 。

具体表现为：
1.  **收敛速度降低**：对于[光滑函数](@entry_id:267124)，PCE 通常能实现指数级的收敛速度。但对于有间断的函数， $L^2$ 误差的[收敛速度](@entry_id:636873)会降至缓慢的 **代数速率** (algebraic rate)，例如 $O(1/p)$，其中 $p$ 是多项式阶数。
2.  **虚假振荡**：在[间断点](@entry_id:144108) $\xi^{\star}$ 附近，PCE 近似会产生剧烈的、幅值不会随 $p$ 增大而消失的过冲和下冲。这意味着 PCE 无法对[间断函数](@entry_id:143848)实现均匀收敛 (uniform convergence)。

这种现象是全局谱方法逼近[非光滑函数](@entry_id:175189)的固有局限，简单地更换多项式基族（例如用 Hermite 替换 Legendre）并不能解决问题 。为了克服这一困难，研究人员发展了更先进的技术，如多单元 PCE (multi-element PCE)、分段 PCE 或[基函数](@entry_id:170178)增强方法，这些方法通过在随机空间中引入局部化思想来更准确地捕捉不连续行为。这些已成为[不确定性量化](@entry_id:138597)领域的前沿研究课题。