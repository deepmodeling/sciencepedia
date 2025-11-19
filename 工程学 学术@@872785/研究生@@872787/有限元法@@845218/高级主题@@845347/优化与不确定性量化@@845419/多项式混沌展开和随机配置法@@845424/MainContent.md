## 引言
在现代计算科学与工程中，许多模型的输入参数——如材料属性、边界条件或外部载荷——都存在固有的不确定性。传统的确定性模型无法捕捉这些不确定性对系统响应的影响，从而限制了预测的可靠性。因此，如何有效地量化和传播模型中的不确定性，已成为一个核心的科学挑战。[多项式混沌展开](@entry_id:162793) (Polynomial Chaos Expansions, PCE) 和随机配置 (Stochastic Collocation, SC) 方法为此提供了强大而严谨的数学框架，它们能够将不确定性直接融入数学模型，并高效地计算出系统响应的统计特性。

本文旨在系统性地介绍PCE和SC方法，解决从理论到实践的知识鸿沟，帮助读者全面掌握这些先进的[不确定性量化](@entry_id:138597)技术。我们首先将在**原理与机制**一章中，深入探讨这两种方法的核心数学原理，包括如何用[随机变量](@entry_id:195330)建模不确定性、[广义多项式混沌](@entry_id:749788)展开的构建、以及计算展开系数的侵入式与非侵入式策略。随后，在**应用与交叉学科联系**一章中，我们将展示这些理论如何在解决[随机偏微分方程](@entry_id:188292)、[结构动力学](@entry_id:172684)、乃至金融和计算机科学等多样化领域的实际问题中发挥作用。最后，**动手实践**部分将通过具体的数值练习，巩固关键概念，如处理随机场、管理高维复杂性以及避免计算陷阱。

## 原理与机制

本章深入探讨[多项式混沌展开](@entry_id:162793) (Polynomial Chaos Expansions, PCE) 和随机配置 (Stochastic Collocation, SC) 方法的核心原理与底层机制。我们将从不确定性的[数学建模](@entry_id:262517)开始，逐步建立[广义多项式混沌](@entry_id:749788) (generalized Polynomial Chaos, gPC) 的概念框架。随后，我们将阐述计算 gPC 系数的两种主要方法——[侵入式随机伽辽金法](@entry_id:750793) (Stochastic Galerkin, SG) 和非侵入式[随机配置法](@entry_id:174778) (Stochastic Collocation, SC)，并对它们进行比较。最后，本章将介绍 gPC 在后处理分析中的强大应用，如[全局敏感性分析](@entry_id:171355)，并讨论一些高级主题，包括高维问题中的截断策略和处理非光滑问题的多单元方法。

### 不确定性的[随机变量](@entry_id:195330)建模

在对包含不确定性的物理系统进行建模时，第一步是将不确定性[参数形式](@entry_id:176887)化为[概率空间](@entry_id:201477) $(\Omega, \mathcal{F}, \mathbb{P})$ 上的[随机变量](@entry_id:195330)。假设一个系统依赖于 $s$ 个不确定参数，我们可以用一个随机向量 $\boldsymbol{\xi}(\omega) = (\xi_1(\omega), \dots, \xi_s(\omega)): \Omega \to \mathbb{R}^s$ 来表示它们。这个向量的[概率分布](@entry_id:146404)是后续所有分析的基础。处理这些不确定性输入的策略很大程度上取决于其分量是相互独立还是相关 [@problem_id:2589455]。

#### [独立随机变量](@entry_id:273896)

当输入[随机变量](@entry_id:195330) $\xi_1, \dots, \xi_s$ 相互独立时，情况最为简单。此时，它们的[联合概率](@entry_id:266356)测度 $\mathbb{P}_{\boldsymbol{\xi}}$ 是各个分量边缘测度 $\mathbb{P}_i$ 的[张量积](@entry_id:140694)，即 $\mathbb{P}_{\boldsymbol{\xi}} = \bigotimes_{i=1}^s \mathbb{P}_i$。这种可分离的结构是 gPC 和 SC 方法高效应用的关键。它允许我们将多变量问题分解为一系列单变量问题的组合。

具体而言，对于依赖于[独立随机变量](@entry_id:273896)的量 $Q(\boldsymbol{\xi})$，其期望的计算（即在 $L^2$ 空间中的[内积](@entry_id:158127)）可以分解为：
$$
\mathbb{E}[g(\boldsymbol{\xi})h(\boldsymbol{\xi})] = \int_{\mathbb{R}^s} g(\mathbf{x})h(\mathbf{x}) \prod_{i=1}^s d\mathbb{P}_i(x_i)
$$
这种分解使得我们可以通过张量积来构建多变量[正交多项式](@entry_id:146918)[基函数](@entry_id:170178)。如果 $\psi_{\alpha_i}^{(i)}$ 是关于测度 $\mathbb{P}_i$ 的一维[正交多项式](@entry_id:146918)，那么 $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{i=1}^s \psi_{\alpha_i}^{(i)}(\xi_i)$ 就构成了关于联合测度 $\mathbb{P}_{\boldsymbol{\xi}}$ 的多维正交基。同样，随机配置方法中的多维求积或插值网格（例如[张量积网格](@entry_id:755861)或[稀疏网格](@entry_id:139655)）也可以从一维求积规则（如高斯求积）构造而来 [@problem_id:2589455]。

#### [相关随机变量](@entry_id:200386)

当输入变量 $\boldsymbol{\xi}$ 的分量之间存在相关性时，其[联合概率密度函数](@entry_id:267139) $p_{\boldsymbol{\xi}}(\mathbf{x})$ 不再是边缘密度函数的乘积。直接使用为[独立变量](@entry_id:267118)设计的张量积基（例如，在相关[高斯变量](@entry_id:276673)中使用单变量 Hermite 多项式的乘积）将导致[基函数](@entry_id:170178)失去正交性，从而使 gPC 的理论基础和计算优势失效 [@problem_id:2589455]。例如，对于两个相关的零均值[高斯变量](@entry_id:276673) $\xi_1$ 和 $\xi_2$，其[相关系数](@entry_id:147037)为 $\rho \neq 0$，[基函数](@entry_id:170178) $H_1(\xi_1) = \xi_1$ 和 $H_1(\xi_2) = \xi_2$ 的[内积](@entry_id:158127)为 $\mathbb{E}[\xi_1 \xi_2] = \text{Cov}(\xi_1, \xi_2) = \rho \neq 0$，破坏了正交性。

处理相关性主要有两种策略：

1.  **等概率变换 (Isoprobabilistic Transform)**：寻找一个可测变换 $T: \mathbb{R}^s \to \mathbb{R}^s$，将一组易于处理的[独立随机变量](@entry_id:273896) $\boldsymbol{\eta}$（例如标准正态分布）映射到目标相关变量 $\boldsymbol{\xi}$，使得 $\boldsymbol{\xi} = T(\boldsymbol{\eta})$ 在[分布](@entry_id:182848)上成立。常用的变换包括 Rosenblatt 变换和 Nataf 变换。通过这种方式，原始问题 $Q(\boldsymbol{\xi})$ 被转化为 $Q(T(\boldsymbol{\eta}))$，变成了一个关于[独立变量](@entry_id:267118) $\boldsymbol{\eta}$ 的问题。随后，我们可以在 $\boldsymbol{\eta}$ 空间中构建标准的 gPC 展开和配置网格。进行计算时，只需将 $\boldsymbol{\eta}$ 空间的[配置点](@entry_id:169000)通过 $T$ 映射回 $\boldsymbol{\xi}$ 空间，然后送入原始的确定性求解器 [@problem_id:2589455]。

2.  **构建相关[基函数](@entry_id:170178)**：另一种方法是直接针[对相关](@entry_id:203353)的联合概率测度 $\mathbb{P}_{\boldsymbol{\xi}}$ 构建一个多变量正交多项式基 $\{\Phi_k(\boldsymbol{\xi})\}$。这可以通过对一组[基函数](@entry_id:170178)（如多项式单项式）应用 Gram-Schmidt [正交化](@entry_id:149208)过程来实现，其[内积](@entry_id:158127)定义为 $\langle \phi, \psi \rangle = \int_{\mathbb{R}^s} \phi(\mathbf{x})\psi(\mathbf{x}) p_{\boldsymbol{\xi}}(\mathbf{x}) d\mathbf{x}$。相应地，[数值积分](@entry_id:136578)和配置也必须使用针对此特定加权测度设计的求积规则。这种方法虽然原理上可行，但在实践中可能更具挑战性 [@problem_id:2589455]。

### [广义多项式混沌 (gPC)](@entry_id:749789) 展开

gPC 的核心思想是将一个随机输出量（或[随机场](@entry_id:177952)）$Q(\boldsymbol{\xi})$，假设其[方差](@entry_id:200758)有限（即 $Q \in L^2(\Gamma, \rho)$），表示为一个在其输入[随机变量](@entry_id:195330) $\boldsymbol{\xi}$ 的正交多项式基 $\{\Psi_{\boldsymbol{\alpha}}\}$ 上的谱展开式：
$$
Q(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathbb{N}_0^d} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})
$$
其中 $\boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_d)$ 是多重指标，$c_{\boldsymbol{\alpha}}$ 是展开系数。

#### 正交性的中心作用

**正交性** (orthogonality) 是 gPC 方法的基石。这里的正交性是针对由 $\boldsymbol{\xi}$ 的[概率密度函数](@entry_id:140610) $\rho(\boldsymbol{\xi})$ 加权的 $L^2$ [内积](@entry_id:158127)而言的。对于任意两个[基函数](@entry_id:170178) $\Psi_{\boldsymbol{\alpha}}$ 和 $\Psi_{\boldsymbol{\beta}}$，它们的[内积](@entry_id:158127)定义为[期望值](@entry_id:153208)：
$$
\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \mathbb{E}[\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})\Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})] = \int_{\Gamma} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})\Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})\rho(\boldsymbol{\xi}) d\boldsymbol{\xi}
$$
如果基是**标准正交** (orthonormal) 的，那么 $\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$，其中 $\delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$ 是 Kronecker delta。

[标准正交性](@entry_id:267887)极大地简化了系数的计算。为了找到最佳的 $L^2$ 逼近，我们将 $Q(\boldsymbol{\xi})$ 投影到由[基函数](@entry_id:170178)张成的[子空间](@entry_id:150286)上。这要求逼近误差 $e = Q - \sum c_{\boldsymbol{\alpha}}\Psi_{\boldsymbol{\alpha}}$ 与该[子空间](@entry_id:150286)中的任何[基函数](@entry_id:170178) $\Psi_{\boldsymbol{\beta}}$ 正交，即 $\langle e, \Psi_{\boldsymbol{\beta}} \rangle = 0$。这导出了所谓的**[正规方程](@entry_id:142238)** (normal equations)。如果基是标准正交的，正规方程的 Gram 矩阵就是[单位矩阵](@entry_id:156724)，系数可以直接通过投影得到 [@problem_id:2589508]：
$$
c_{\boldsymbol{\alpha}} = \langle Q(\boldsymbol{\xi}), \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \rangle = \mathbb{E}[Q(\boldsymbol{\xi})\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]
$$
如果基只满足正交性而非标准正交，即 $\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\alpha}} \rangle = h_{\boldsymbol{\alpha}} \neq 1$，则系数公式变为 $c_{\boldsymbol{\alpha}} = \mathbb{E}[Q(\boldsymbol{\xi})\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})] / h_{\boldsymbol{\alpha}}$。如果基不是正交的，则必须求解一个全耦合的[线性系统](@entry_id:147850) $Gc=f$ 来获得系数，计算成本显著增加 [@problem_id:2589508]。

#### Askey 族多项式与 gPC

Wiener 最初提出的[多项式混沌](@entry_id:196964)仅使用 Hermite 多项式来表示高斯[随机过程](@entry_id:159502)。gPC 将此思想推广，根据输入[随机变量](@entry_id:195330)的[分布](@entry_id:182848)类型，从 Askey 族正交多项式中选择最合适的基。例如：
-   **Hermite 多项式** 对应 **高斯**[分布](@entry_id:182848)。
-   **Legendre 多项式** 对应 **均匀**[分布](@entry_id:182848)。
-   **Laguerre 多项式** 对应 **指数**或 **Gamma** [分布](@entry_id:182848)。
-   **Jacobi 多项式** 对应 **Beta** [分布](@entry_id:182848)。

选择与输入测度相匹配的正交多项式基，可以确保 gPC 展开的谱收敛性（即对于光滑的参数到解映射，误差随多项式阶数呈指数下降）。

以高斯[随机变量](@entry_id:195330)为例，我们可以具体构建其[正交基](@entry_id:264024)。假设 $\xi \sim \mathcal{N}(0,1)$，常用的基是概率论学家的 Hermite 多项式 $\{\psi_n(\xi)\}$，它们关于标准[高斯测度](@entry_id:749747)是标准正交的。例如，前三阶标准[正交多项式](@entry_id:146918)为 $\psi_0(\xi) = 1$, $\psi_1(\xi) = \xi$, 和 $\psi_2(\xi) = \frac{\xi^2 - 1}{\sqrt{2}}$ [@problem_id:2589461]。另一个约定是物理学家的 Hermite 多项式 $H_n(y)$，它们关于权重 $\exp(-y^2)$ 正交。例如，$H_0(y)=1, H_1(y)=2y, H_2(y)=4y^2-2, H_3(y)=8y^3-12y$。它们对应的范数可以通过[正交关系](@entry_id:145540) $\int_{-\infty}^{\infty} [H_n(y)]^2 \exp(-y^2) dy = \sqrt{\pi} 2^n n!$ 来计算 [@problem_id:2589427]。

### 从 gPC 系数中提取[统计矩](@entry_id:268545)

gPC 展开的一个核心优势在于，一旦获得了系数 $\{c_{\boldsymbol{\alpha}}\}$，就可以极其高效地计算出原随机量 $Q(\boldsymbol{\xi})$ 的各种[统计矩](@entry_id:268545)。

#### 均值和[方差](@entry_id:200758)

利用基[函数的正交性](@entry_id:160337)，我们可以直接从 gPC 系数中解析地得到均值（期望）和[方差](@entry_id:200758)。假设使用[标准正交基](@entry_id:147779) $\{\Psi_{\boldsymbol{\alpha}}\}$，且 $\Psi_{\boldsymbol{0}} = 1$。

**均值** $\mathbb{E}[Q]$ 的计算如下：
$$
\mathbb{E}[Q] = \mathbb{E}\left[ \sum_{\boldsymbol{\alpha}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \right] = \sum_{\boldsymbol{\alpha}} c_{\boldsymbol{\alpha}} \mathbb{E}[\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]
$$
由于 $\mathbb{E}[\Psi_{\boldsymbol{\alpha}}] = \langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{0}} \rangle = \delta_{\boldsymbol{\alpha}0}$，上式简化为：
$$
\mathbb{E}[Q] = c_{\boldsymbol{0}}
$$
即 gPC 展开的零阶系数就是随机量的均值。

**[方差](@entry_id:200758)** $\text{Var}[Q]$ 的计算如下：
$$
\text{Var}[Q] = \mathbb{E}[(Q - \mathbb{E}[Q])^2] = \mathbb{E}\left[ \left( \sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \right)^2 \right]
$$
展开平方项并利用[基函数](@entry_id:170178)的[标准正交性](@entry_id:267887)：
$$
\text{Var}[Q] = \sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} \sum_{\boldsymbol{\beta} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}} c_{\boldsymbol{\beta}} \mathbb{E}[\Psi_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\beta}}] = \sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} \sum_{\boldsymbol{\beta} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}} c_{\boldsymbol{\beta}} \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}} = \sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}}^2
$$
[方差](@entry_id:200758)等于所有非零阶 gPC 系数的平方和。这一结果是希尔伯特空间中 Parseval 恒等式的直接体现 [@problem_id:2589461] [@problem_id:2589508]。例如，对于一个二阶展开 $Q(\xi) = u_0 \psi_0(\xi) + u_1 \psi_1(\xi) + u_2 \psi_2(\xi)$，其均值为 $u_0$，[方差](@entry_id:200758)为 $u_1^2 + u_2^2$ [@problem_id:2589461]。

### 计算 gPC 系数的方法

计算 gPC 系数是整个 UQ 过程中的核心计算任务。主要有两种途径：侵入式和非侵入式。

#### 侵入式方法：[随机伽辽金法](@entry_id:178148) (SG)

**[随机伽辽金法](@entry_id:178148)**是一种**侵入式** (intrusive) 方法，它直接在[随机微分方程](@entry_id:146618)的弱形式层面进行操作。其核心思想是将解和不确定系数都表示为 gPC 展开，然后将这些展开式代入控制方程的[弱形式](@entry_id:142897)中。接着，通过对随机空间进行[伽辽金投影](@entry_id:145611)（即要求残差与 gPC 基中的每个多项式都正交），从而导出一个大规模、全耦合的确定性[方程组](@entry_id:193238)，该[方程组](@entry_id:193238)的解就是 gPC 系数。

以一个随机[扩散](@entry_id:141445)问题为例，$-\nabla \cdot (k(x, \boldsymbol{\xi}) \nabla u(x, \boldsymbol{\xi})) = f(x)$。我们假设解和系数的 gPC 展开为：
$$
u(x, \boldsymbol{\xi}) = \sum_{j=0}^{P} u_j(x) \Psi_j(\boldsymbol{\xi}), \quad k(x, \boldsymbol{\xi}) = \sum_{r=0}^{R} k_r(x) \Psi_r(\boldsymbol{\xi})
$$
其中 $u_j(x)$ 是待求的确定性系数场。将它们代入[弱形式](@entry_id:142897)，并用每个[基函数](@entry_id:170178) $\Psi_i(\boldsymbol{\xi})$ 作为[检验函数](@entry_id:166589)进行投影，最终经过有限元[空间离散化](@entry_id:172158)后，得到一个关于 nodal coefficient vectors $U_j$ 的大型块状[线性系统](@entry_id:147850) [@problem_id:2590507]：
$$
\sum_{j=0}^{P} \left( \sum_{r=0}^{R} T_{ijr} K^{(r)} \right) U_j = \langle \Psi_i \rangle f^h, \quad \text{for } i = 0, \dots, P
$$
其中 $K^{(r)}$ 是与 $k_r(x)$ 相关的刚度矩阵，$f^h$是[载荷向量](@entry_id:635284)，而 $T_{ijr} = \langle \Psi_i \Psi_j \Psi_r \rangle$ 是[基函数](@entry_id:170178)的[三重积](@entry_id:162942)张量，它将不同的 gPC [模式耦合](@entry_id:752088)在一起。

SG 方法的“侵入性”在于它需要对现有的确定性有限元代码进行深度修改，以组装和求解这个新的、更大的耦合系统。然而，它在数学上极为优雅，且对于某些问题（如线性问题）可能非常高效 [@problem_id:2589495]。

#### 非侵入式方法：[随机配置法](@entry_id:174778) (SC)

与 SG 相反，**[随机配置法](@entry_id:174778)**是一类**非侵入式** (non-intrusive) 方法。它将已有的确定性求解器视为一个“黑箱”，通过在随机参数空间中精心选择的点（称为**[配置点](@entry_id:169000)**或** collocation points**）上多次运行该求解器，然后利用这些“快照”解来重构 gPC 展开。

SC 的核心是将 gPC 系数 $c_{\boldsymbol{\alpha}} = \mathbb{E}[Q(\boldsymbol{\xi})\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]$ 的积分计算问题转化为一个[数值求积](@entry_id:136578)问题。最直接的 SC 形式是**伪[谱[投](@entry_id:265201)影法](@entry_id:144836)** (pseudospectral projection)，它使用[数值求积](@entry_id:136578)（如高斯求积）来近似积分：
$$
c_{\boldsymbol{\alpha}} \approx \sum_{m=1}^{M} w_m Q(\boldsymbol{\xi}^{(m)}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}^{(m)})
$$
其中 $\{\boldsymbol{\xi}^{(m)}\}$是求积节点，$\{w_m\}$ 是对应的权重。要计算这些系数，我们只需：
1.  选择一个合适的求积规则（节点和权重）。
2.  在每个节点 $\boldsymbol{\xi}^{(m)}$ 处，运行一次确定性求解器得到 $Q(\boldsymbol{\xi}^{(m)})$。
3.  通过上述加权和计算每个系数 $c_{\boldsymbol{\alpha}}$。

例如，对于一个依赖于单个[均匀分布](@entry_id:194597)变量 $\xi \in [-1,1]$ 的问题，我们可以使用三点 Gauss-Legendre 求积规则来近似计算二阶 Legendre 多项式 $\psi_2(\xi)$ 的系数 $c_2$ [@problem_id:2589502]。

另一种 SC 的形式是**插值法** (interpolation)。它在[配置点](@entry_id:169000)集 $\{\boldsymbol{\xi}^{(m)}\}$ 上构建一个[多项式插值](@entry_id:145762) $\mathcal{I}[Q](\boldsymbol{\xi})$ 来逼近 $Q(\boldsymbol{\xi})$，使得 $\mathcal{I}[Q](\boldsymbol{\xi}^{(m)}) = Q(\boldsymbol{\xi}^{(m)})$。这个[插值多项式](@entry_id:750764)本身就是 gPC 展开的一个逼近。

SC 的关键优势在于其**非侵入性**：它不需要修改确定性求解器的源代码，只需一个能够调用它的外部脚本即可。这使得将 UQ 方法应用于复杂的遗留代码成为可能。SC 的挑战在于选择一组高效的[配置点](@entry_id:169000)，以在控制求解器调用次数（即计算成本）的同时，获得足够精确的 gPC 系数 [@problem_id:2589495]。如果 $Q$ 是一个至多 $p$ 阶的多项式，为了精确计算所有系数（其被积函数 $Q\Psi_{\boldsymbol{\alpha}}$ 的阶数最高可达 $2p$），需要一个对至多 $2p$ 阶多项式都精确的求积法则 [@problem_id:2589508]。

### 高级主题与实践考量

#### [全局敏感性分析](@entry_id:171355)：[Sobol指数](@entry_id:156558)

gPC 展开不仅能提供均值和[方差](@entry_id:200758)，还能作为进行**[全局敏感性分析](@entry_id:171355)** (Global Sensitivity Analysis, GSA) 的强大工具。GSA 的目的是量化单个或一组输入变量对输出[方差](@entry_id:200758)的贡献。最常用的度量是 **[Sobol指数](@entry_id:156558)**。

[Sobol指数](@entry_id:156558)基于 ANOVA (Analysis of Variance) 分解，它将函数 $Q(\boldsymbol{\xi})$ 的总[方差](@entry_id:200758) $V$ 分解为由不同输入变量[子集](@entry_id:261956)引起的[方差](@entry_id:200758)之和。利用 gPC 展开的正交性，[ANOVA](@entry_id:275547) 分解与 gPC 展开之间存在直接的对应关系。具体来说，与变量[子集](@entry_id:261956) $A \subseteq \{1, \dots, d\}$ 相关联的部分[方差](@entry_id:200758) $V_U$ (其中 $U \subseteq A$) 可以通过对 gPC 系数进行分组求和得到 [@problem_id:2589462]：
$$
\sum_{\emptyset \neq U \subseteq A} V_U = \sum_{\boldsymbol{\alpha} : \emptyset \neq \text{supp}(\boldsymbol{\alpha}) \subseteq A} c_{\boldsymbol{\alpha}}^2
$$
其中 $\text{supp}(\boldsymbol{\alpha})$ 是多重指标 $\boldsymbol{\alpha}$ 的非零元索引集。

-   **一阶[Sobol指数](@entry_id:156558)** $S_i$ 度量了变量 $\xi_i$ 单独对总[方差](@entry_id:200758)的贡献。
-   **总效应[Sobol指数](@entry_id:156558)** $S_{T,i}$ 度量了变量 $\xi_i$ 单独以及它与其他变量所有[交互作用](@entry_id:176776)共同对总[方差](@entry_id:200758)的贡献。

利用 gPC 系数，这些指数可以无额外模型运行成本地计算出来：
$$
S_i = \frac{\sum_{\boldsymbol{\alpha} \in \mathcal{A}_i} c_{\boldsymbol{\alpha}}^2}{V}, \quad S_{T,i} = \frac{\sum_{\boldsymbol{\alpha} \in \mathcal{A}_{T,i}} c_{\boldsymbol{\alpha}}^2}{V}
$$
其中 $\mathcal{A}_i = \{\boldsymbol{\alpha} | \text{supp}(\boldsymbol{\alpha})=\{i\}\}$，$ \mathcal{A}_{T,i} = \{\boldsymbol{\alpha} | i \in \text{supp}(\boldsymbol{\alpha})\}$，$V = \sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}}^2$。这一特性使 gPC 成为进行高效敏感性分析的“元模型”。

#### gPC 截断策略与[维数灾难](@entry_id:143920)

在实践中，gPC 展开必须截断至有限项。选择哪些多项式[基函数](@entry_id:170178)保留在展开中，即选择一个**多重[指标集](@entry_id:268489)** $\mathcal{A}$，是一个关键决策。最直接的选择是**总阶数 (Total-Degree, TD)** 截断：
$$
\mathcal{A}_p^{\text{TD}} = \{\boldsymbol{\alpha} \in \mathbb{N}_0^d : |\boldsymbol{\alpha}|_1 = \sum_{k=1}^d \alpha_k \le p\}
$$
TD 集的大小，即[基函数](@entry_id:170178)数量，为 $|\mathcal{A}_p^{\text{TD}}| = \binom{p+d}{d}$。当维数 $d$ 增加时，这个数量会以 $d^p$ 的速度爆炸性增长，这就是所谓的**维数灾难** (curse of dimensionality)。

为了缓解[维数灾难](@entry_id:143920)，特别是对于那些高阶交互作用较弱的问题，可以使用其他各向异性的截断策略。一个流行的选择是**双曲[交叉](@entry_id:147634) (Hyperbolic-Cross, HC)** [指标集](@entry_id:268489)：
$$
\mathcal{A}_p^{\text{HC}} = \{\boldsymbol{\alpha} \in \mathbb{N}_0^d : \prod_{k=1}^{d}(\alpha_k+1) \le p+1\}
$$
HC 集优先包含那些低阶交互作用的项（即大部分 $\alpha_k$ 为零的项），而舍弃许多高阶[交互作用](@entry_id:176776)的项。对于固定的 $p$，当 $d \to \infty$ 时，HC 集的大小 $|\mathcal{A}_p^{\text{HC}}|$ 仅以 $d^{\lfloor \log_2(p+1) \rfloor}$ 的速度增长，这是一个远低于 TD 集增长速度的[多项式增长](@entry_id:177086)。而对于固定的 $d$，当 $p \to \infty$ 时，HC 集大小的增长速度约为 $\mathcal{O}(p(\log p)^{d-1})$，也远慢于 TD 集的 $\mathcal{O}(p^d)$ [@problem_id:2589489]。选择合适的截断策略是在高维问题中平衡精度和计算成本的关键。

#### 处理非[光滑性](@entry_id:634843)：多单元 gPC

标准（全局）gPC 方法在参数到解的映射 $Q(\boldsymbol{\xi})$ 光滑时表现最佳，能实现谱收敛。然而，如果映射中存在**不连续**或**拐点** (kinks)——例如，由于材料行为的阈值效应——全局[多项式逼近](@entry_id:137391)的收敛会退化到缓慢的代数收敛，并可能产生类似吉布斯现象的[振荡](@entry_id:267781)。

为了解决这个问题，可以采用**多单元[多项式混沌展开](@entry_id:162793) (multi-element PCE, m-PCE)** [@problem_id:2589436]。其思想类似于物理空间中的[有限元法](@entry_id:749389)：将随机[参数空间](@entry_id:178581) $\Gamma$ 分割成多个不相交的“随机单元” $\{\Gamma_k\}$，使得在每个单元内部，$Q(\boldsymbol{\xi})$ 都是光滑的。然后，在每个单元 $\Gamma_k$ 上独立地构建一个局部的 gPC 展开。
$$
Q(\boldsymbol{\xi}) \approx \sum_{k=1}^{K} \mathbb{I}_{\Gamma_k}(\boldsymbol{\xi}) Q_k(\boldsymbol{\xi}) = \sum_{k=1}^{K} \mathbb{I}_{\Gamma_k}(\boldsymbol{\xi}) \left( \sum_{\boldsymbol{\alpha}} c_{\boldsymbol{\alpha}}^{(k)} \psi_{\boldsymbol{\alpha}}^{(k)}(\boldsymbol{\xi}) \right)
$$
其中 $\mathbb{I}_{\Gamma_k}$ 是单元 $\Gamma_k$ 的指示函数，$\{\psi_{\boldsymbol{\alpha}}^{(k)}\}$ 是在 $\Gamma_k$ 上关于[条件概率](@entry_id:151013)测度正交的局部多项式基。

这种分片逼近可以在不连续的界面上精确地捕捉跳跃，从而在每个光滑的子域内恢复谱收敛性。全局[统计矩](@entry_id:268545)，如均值和[方差](@entry_id:200758)，可以通过**[全期望定律](@entry_id:265946)**和**[全方差定律](@entry_id:184705)**，将每个单元上的局部矩根据其概率 $P(\Gamma_k)$ 加权求和得到。例如，$\mathbb{E}[Q] = \sum_k P(\Gamma_k) \mathbb{E}_k[Q]$。m-PCE 的非侵入式实现只需在每个单元 $\Gamma_k$ 内部署独立的随机配置方法即可。重要的是，这种方法本质上是分片不连续的，不需要在单元边界强制施加连续性约束来保证 $L^2$ 收敛 [@problem_id:2589436]。