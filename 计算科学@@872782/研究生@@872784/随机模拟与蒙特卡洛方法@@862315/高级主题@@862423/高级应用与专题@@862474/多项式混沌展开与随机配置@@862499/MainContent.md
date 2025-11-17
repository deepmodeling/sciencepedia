## 引言
在现代科学与工程计算中，模型输入参数、[初始条件](@entry_id:152863)或边界条件中存在的不确定性是不可避免的。这些不确定性会传播通过模型，导致其输出结果也具有随机性。准确地量化和管理这种不确定性对于模型的可靠性验证、风险评估和[稳健设计](@entry_id:269442)至关重要。[多项式混沌展开](@entry_id:162793)（Polynomial Chaos Expansions, PCE）和随机配置（Stochastic Collocation, SC）方法是解决这一挑战的两种强大且应用广泛的计算技术。然而，深入理解其背后的数学原理并有效地将其应用于实际问题，对许多研究人员和工程师而言仍是一个知识缺口。

本文旨在系统性地填补这一缺口，为读者提供关于PCE和SC方法的全面指南。我们将从数学基础出发，逐步深入到高级应用和实践挑战。通过本文的学习，您将能够：
- 在第一章“原理与机制”中，掌握构建PCE和SC所需的希尔伯特空间框架、[广义多项式混沌](@entry_id:749788)基的[构造原理](@entry_id:141667)，以及计算展开系数的侵入式与非侵入式方法。
- 在第二章“应用与跨学科联系”中，探索这些方法在求解随机微分方程、进行[灵敏度分析](@entry_id:147555)、处理高维问题以及加速贝叶斯推断等多样化场景中的实际应用。
- 在第三章“动手实践”中，通过一系列精心设计的计算练习，将理论知识转化为解决具体问题的能力，加深对混叠效应、多维插值等关键概念的理解。

本文将引导您穿越[不确定性量化](@entry_id:138597)的复杂景观，从基本概念无缝过渡到前沿应用，最终使您具备在自己的领域中自信地运用PCE和SC方法的能力。

## 原理与机制

本章旨在深入探讨[多项式混沌展开](@entry_id:162793)（Polynomial Chaos Expansions, PCE）与随机配置（Stochastic Collocation, SC）方法背后的核心科学原理与数学机制。我们将从[希尔伯特空间](@entry_id:261193)（Hilbert space）的视角出发，系统地构建[广义多项式混沌](@entry_id:749788)（generalized Polynomial Chaos, gPC）基，探讨其系数的计算方法，并分析这些方法在实际应用中的性能、优势与局限性。

### 用于[不确定性量化](@entry_id:138597)的希尔伯特空间框架

在[不确定性量化](@entry_id:138597)中，我们关注一个物理或数学模型的响应 $u$，它依赖于一个随机输入向量 $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$。这个随机响应本身是一个[随机变量](@entry_id:195330)，其统计特性（如均值、[方差](@entry_id:200758)）是我们希望确定的。[多项式混沌](@entry_id:196964)方法的基本思想是将这个随机响应 $u(\boldsymbol{\xi})$ 表示为一组关于输入[随机变量](@entry_id:195330) $\boldsymbol{\xi}$ 的正交多项式基的[无穷级数](@entry_id:143366)。

为了严谨地定义这一展开，我们首先需要一个合适的数学框架。假设模型响应 $u(\boldsymbol{\xi})$ 是一个**平方可积**（square-integrable）的[随机变量](@entry_id:195330)，即其二阶矩有限：$\mathbb{E}[u(\boldsymbol{\xi})^2]  \infty$。这类[随机变量](@entry_id:195330)构成的集合形成了一个希尔伯特空间，记为 $L^2(\Omega, \mathcal{F}, \mathbb{P})$，其中 $(\Omega, \mathcal{F}, \mathbb{P})$ 是底层的[概率空间](@entry_id:201477)。在这个空间中，任意两个[随机变量](@entry_id:195330) $f(\boldsymbol{\xi})$ 和 $g(\boldsymbol{\xi})$ 的**[内积](@entry_id:158127)**（inner product）被自然地定义为其[乘积的期望值](@entry_id:201037)：
$$
\langle f, g \rangle = \mathbb{E}[f(\boldsymbol{\xi})g(\boldsymbol{\xi})] = \int_{\Gamma} f(\boldsymbol{x})g(\boldsymbol{x}) \rho(\boldsymbol{x}) d\boldsymbol{x}
$$
这里，$\boldsymbol{\xi}$ 的值域为 $\Gamma \subseteq \mathbb{R}^d$，其[联合概率密度函数](@entry_id:267139)（PDF）为 $\rho(\boldsymbol{x})$。我们的目标是为这个[希尔伯特空间](@entry_id:261193)找到一组**标准正交基**（orthonormal basis）$\{\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})\}_{\boldsymbol{\alpha} \in \mathbb{N}_0^d}$，使得任何平方可积的函数 $u(\boldsymbol{\xi})$ 都可以唯一地展开为：
$$
u(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathbb{N}_0^d} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})
$$
其中 $c_{\boldsymbol{\alpha}}$ 是展开系数，$\boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_d)$ 是一个多重指标。根据[希尔伯特空间](@entry_id:261193)中的正交投影理论，这些系数可以通过将 $u(\boldsymbol{\xi})$ 与相应的[基函数](@entry_id:170178)做[内积](@entry_id:158127)来获得：
$$
c_{\boldsymbol{\alpha}} = \langle u, \Psi_{\boldsymbol{\alpha}} \rangle = \mathbb{E}[u(\boldsymbol{\xi}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]
$$
该级数在 $L^2$ 范数下收敛，这意味着[均方误差](@entry_id:175403)随着截断项数的增加而趋于零。

### 构建标准正交基：维纳-[阿斯基方案](@entry_id:187960)

构建上述展开的关键在于选择一组“好”的[基函数](@entry_id:170178) $\{\Psi_{\boldsymbol{\alpha}}\}$。一个自然且强大的选择是使用[正交多项式](@entry_id:146918)。Cameron-Martin 定理表明，对于高斯[随机变量](@entry_id:195330)，使用埃尔米特（Hermite）多项式可以构成一个完备的正交基。这一思想被推广为**[广义多项式混沌](@entry_id:749788)**（gPC）理论，其核心原则是：[基函数](@entry_id:170178)的选择应与输入[随机变量](@entry_id:195330)的[概率分布](@entry_id:146404)相匹配。[@problem_id:3330080]

#### 单变量[正交多项式](@entry_id:146918)

对于一个单变量随机输入 $\xi_i$，其概率密度函数为 $\rho_i(x_i)$，我们寻找一组多项式 $\{\psi_n^{(i)}(x_i)\}_{n \ge 0}$，使其在该[分布](@entry_id:182848)的[加权内积](@entry_id:163877)下是正交的：
$$
\langle \psi_m^{(i)}, \psi_n^{(i)} \rangle = \int_{\Gamma_i} \psi_m^{(i)}(x_i) \psi_n^{(i)}(x_i) \rho_i(x_i) dx_i = \gamma_n \delta_{mn}
$$
其中 $\gamma_n$ 是一个正常数，$\delta_{mn}$ 是克罗内克（Kronecker）符号。这种匹配关系被系统地总结在所谓的**维纳-阿斯基（Wiener-Askey）多项式体系**中。该体系为一些常见的连续和[离散分布](@entry_id:193344)指定了相应的[经典正交多项式](@entry_id:192726)族。[@problem_id:3330067]

以下是几个最重要的对应关系：
- **[高斯分布](@entry_id:154414)** ($\mathcal{N}(0,1)$)：对应的正交多项式是**埃尔米特（Hermite）多项式** ($He_n(x)$)，其权重函数为 $w(x) = \exp(-x^2/2)$。
- **[均匀分布](@entry_id:194597)** ($\mathrm{Uniform}(-1,1)$)：对应的[正交多项式](@entry_id:146918)是**勒让德（Legendre）多项式** ($P_n(x)$)，其权重函数为 $w(x) = 1$。
- **伽玛[分布](@entry_id:182848)** ($\mathrm{Gamma}(k, \theta)$)：对应的[正交多项式](@entry_id:146918)是**拉盖尔（Laguerre）多项式** ($L_n^{(\alpha)}(x)$)，其权重函数为 $w(x) = x^{\alpha}\exp(-x)$。
- **贝塔分布** ($\mathrm{Beta}(a,b)$)：对应的[正交多项式](@entry_id:146918)是**雅可比（Jacobi）多项式** ($P_n^{(\alpha, \beta)}(x)$)，其权重函数为 $w(x) = (1-x)^{\alpha}(1+x)^{\beta}$。

例如，对于一个在 $[-1,1]$ 上[均匀分布](@entry_id:194597)的[随机变量](@entry_id:195330)，其PDF为 $\rho(x) = 1/2$。我们选择的基是[勒让德多项式](@entry_id:141510)。标准勒让德多项式在权重 $w(x)=1$ 下正交。为了得到[标准正交基](@entry_id:147779)，我们需要对它们进行归一化。[勒让德多项式的正交性](@entry_id:264861)关系是：
$$
\int_{-1}^{1} P_m(x) P_n(x) dx = \frac{2}{2n+1} \delta_{mn}
$$
因此，对应的**标准正交[勒让德多项式](@entry_id:141510)**为 $\widetilde{P}_n(x) = \sqrt{\frac{2n+1}{2}} P_n(x)$，它们满足 $\int_{-1}^{1} \widetilde{P}_m(x) \widetilde{P}_n(x) dx = \delta_{mn}$。在gPC的框架下，我们使用与PDF成比例的权重函数，即 $w(x)=1/2$，[内积](@entry_id:158127)为 $\frac{1}{2}\int_{-1}^{1}f(x)g(x)dx$。此时，[标准正交基](@entry_id:147779)为 $\psi_n(x) = \sqrt{2n+1} P_n(x)$，因为 $\frac{1}{2}\int_{-1}^{1} (\sqrt{2n+1}P_n(x))^2 dx = 1$。例如，3次标准正交勒让德多项式是 $\psi_3(x) = \sqrt{7}P_3(x) = \sqrt{7} \cdot \frac{1}{2}(5x^3 - 3x)$。[@problem_id:3330142]

#### 张量积构造多维基

当输入随机向量 $\boldsymbol{\xi}=(\xi_1, \dots, \xi_d)$ 的各个分量相互**独立**时，其[联合概率密度函数](@entry_id:267139)是各边缘PDF的乘积：$\rho(\boldsymbol{\xi}) = \prod_{i=1}^d \rho_i(\xi_i)$。在这种情况下，多维[标准正交基](@entry_id:147779)可以通过对单维标准正交基进行**[张量积](@entry_id:140694)**（tensor product）来构造。[@problem_id:3330080]

给定每个维度 $i$ 的单维标准正交多项式族 $\{\psi_n^{(i)}\}_{n \ge 0}$，多维[基函数](@entry_id:170178) $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$ 定义为：
$$
\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{i=1}^d \psi_{\alpha_i}^{(i)}(\xi_i)
$$
其中 $\boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_d)$ 是多重指标。由于各分量的独立性，这组多维多项式基在[联合概率](@entry_id:266356)测度下是标准正交的：
$$
\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \mathbb{E}[\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})] = \int_{\Gamma} \left(\prod_{i=1}^d \psi_{\alpha_i}^{(i)}(x_i)\right) \left(\prod_{i=1}^d \psi_{\beta_i}^{(i)}(x_i)\right) \left(\prod_{i=1}^d \rho_i(x_i)\right) d\boldsymbol{x}
$$
$$
= \prod_{i=1}^d \left( \int_{\Gamma_i} \psi_{\alpha_i}^{(i)}(x_i) \psi_{\beta_i}^{(i)}(x_i) \rho_i(x_i) dx_i \right) = \prod_{i=1}^d \delta_{\alpha_i \beta_i} = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}
$$
这种构造的简洁性和有效性是gPC方法在处理具有独立输入的不确定性问题时如此强大的原因之一。

### 计算展开系数：侵入式与非侵入式方法

构建了[基函数](@entry_id:170178)后，下一个核心任务是计算展开系数 $\{c_{\boldsymbol{\alpha}}\}$。计算这些系数的方法主要分为两大类：**侵入式（intrusive）** 和 **非侵入式（non-intrusive）**。

#### 侵入式方法：随机[伽辽金投影](@entry_id:145611)

侵入式方法直接从模型的控制方程入手。假设模型由一个参数化的算子方程描述，例如一个线性系统 $A(\boldsymbol{\xi}) u(\boldsymbol{\xi}) = f(\boldsymbol{\xi})$。我们将 $A(\boldsymbol{\xi})$、$f(\boldsymbol{\xi})$ 和未知的解 $u(\boldsymbol{\xi})$ 全部用gPC级数来表示：
$$
A(\boldsymbol{\xi}) = \sum_{\ell} A_{\ell} \psi_{\ell}(\boldsymbol{\xi}), \quad f(\boldsymbol{\xi}) = \sum_{m} f_{m} \psi_{m}(\boldsymbol{\xi}), \quad u(\boldsymbol{\xi}) \approx \widehat{u}(\boldsymbol{\xi}) = \sum_{j} u_{j} \psi_{j}(\boldsymbol{\xi})
$$
其中 $A_{\ell}$ 是系数矩阵，$f_m$ 和 $u_j$ 是系数向量。然后，我们将这些展开式代入原方程，并利用**伽辽金（Galerkin）**方法，要求残差 $A(\boldsymbol{\xi})\widehat{u}(\boldsymbol{\xi}) - f(\boldsymbol{\xi})$ 与每个[基函数](@entry_id:170178) $\psi_i(\boldsymbol{\xi})$ 在 $L^2$ [内积](@entry_id:158127)下正交。[@problem_id:3330129]

这导致了一个关于未知系数向量 $\{u_j\}$ 的庞大的、耦合的确定性[线性系统](@entry_id:147850) $G \mathbf{u} = \mathbf{b}$。该系统的全局矩阵 $G$ 的一个标量元素 $[G]_{(i,a),(j,b)}$ (对应于第 $i$ 个[基函数](@entry_id:170178)的第 $a$ 个方程分量和第 $j$ 个未知系数向量的第 $b$ 个分量) 可以表示为：
$$
[G]_{(i,a),(j,b)} = \sum_{\ell=0}^{L} \langle \psi_{i} \psi_{\ell} \psi_{j} \rangle [A_{\ell}]_{ab}
$$
其中 $\langle \psi_{i} \psi_{\ell} \psi_{j} \rangle = \mathbb{E}[\psi_i \psi_{\ell} \psi_j]$ 是所谓的**[三重积](@entry_id:162942)（triple-product）**。侵入式方法的主要优点是，如果适用，它通常能以较少的计算量得到高度准确的系数。其主要缺点是需要深入修改模型的求解器代码以集成随机维度，这在实践中可能非常困难或不可行。

#### 非侵入式方法：[谱投影](@entry_id:265201)与配置

与侵入式方法不同，非侵入式方法将模型求解器视为一个**黑箱**，仅通过在随机空间中选择一些点进行采样评估来计算系数。

##### [谱投影](@entry_id:265201)与数值积分

最直接的非侵入式方法是利用[正交投影](@entry_id:144168)公式 $c_{\boldsymbol{\alpha}} = \mathbb{E}[u(\boldsymbol{\xi})\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]$。这个[期望值](@entry_id:153208)是一个[高维积分](@entry_id:143557)，除了极少数简单情况外，通常无法解析计算。因此，我们必须依赖**数值积分（numerical quadrature）**。[@problem_id:3330123]

对于与正交多项式相关的权重函数，最高效的[数值积分方法](@entry_id:141406)是**高斯积分（Gaussian quadrature）**。一个单维的 $N$ 点[高斯积分法](@entry_id:178260)则对于次数最高为 $2N-1$ 的多项式是**精确**的。[@problem_id:3330137] 这一非凡的精度源于其节点被巧妙地选为第 $N$ 阶[正交多项式](@entry_id:146918)的根。

在计算gPC系数 $c_{\boldsymbol{\alpha}}$ 时，被积函数是 $u(\boldsymbol{\xi})\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$。如果我们对 $u(\boldsymbol{\xi})$ 进行一个 $p$ 阶的总次数截断，那么为了精确计算所有 $|{\boldsymbol{\alpha}}| \le p$ 的系数，我们需要精确地计算形如 $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})\Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})$ (其中$|{\boldsymbol{\beta}}| \le p$) 的多项式乘积的积分。这些乘积的最高次数在任一维度上可达 $2p$。为了确保[高斯积分](@entry_id:187139)的精确性，单维积分法则的次数必须满足 $2n-1 \ge 2p$，其中 $n$ 是该维度的积分点数。这导出了一个关键的条件：$n \ge p+1$。即，为了无混淆地计算一个 $p$ 阶PCE的系数，每个维度至少需要 $p+1$ 个[高斯积分](@entry_id:187139)点。[@problem_id:3330137]

对于 $d$ 维问题，我们使用[张量积](@entry_id:140694)[高斯积分法](@entry_id:178260)则。系数的近似值 $\widehat{c}_{\boldsymbol{\alpha}}$ 由下式给出：
$$
\widehat{c}_{\boldsymbol{\alpha}} = \sum_{j_1=1}^{n} \dots \sum_{j_d=1}^{n} u(\xi_1^{(j_1)}, \dots, \xi_d^{(j_d)}) \prod_{k=1}^{d} \left( w_k^{(j_k)} \psi_{\alpha_k}^{(k)}(\xi_k^{(j_k)}) \right)
$$
其中 $(\xi_k^{(j_k)}, w_k^{(j_k)})$ 是第 $k$ 维的 $n$ 点高斯[积分节点和权重](@entry_id:146264)。[@problem_id:3330123]

##### 随机配置及其与投影的等价性

**随机配置（Stochastic Collocation）** 提供了另一种非侵入式的视角。其核心思想是在随机空间中选择一个节点集 $\mathcal{X}$，在这些点上评估模型 $u(\boldsymbol{x})$，然后构造一个多项式 $I_{\mathcal{X}}[u]$ 来**插值**这些评估值。这个[插值多项式](@entry_id:750764)本身就是对真实函数 $u(\boldsymbol{\xi})$ 的一个代理模型。[@problem_id:3330060]

一个自然的选择是使用**多元拉格朗日（Lagrange）多项式**作为插值基。对于一个张量积节点网格 $\mathcal{X}$，[插值多项式](@entry_id:750764)可以写为：
$$
I_{\mathcal{X}}[u](\boldsymbol{\xi}) = \sum_{\boldsymbol{x} \in \mathcal{X}} u(\boldsymbol{x}) L_{\boldsymbol{x}}(\boldsymbol{\xi})
$$
其中 $L_{\boldsymbol{x}}(\boldsymbol{\xi})$ 是在节点 $\boldsymbol{x}$ 取值为1，在所有其他节点上取值为0的多元[拉格朗日基多项式](@entry_id:168175)。

[谱投影](@entry_id:265201)和随机配置之间存在一个深刻而优美的联系。当随机配置的节点集 $\mathcal{X}$ 恰好是用于[谱投影](@entry_id:265201)的张量积[高斯积分](@entry_id:187139)节点集时，通过数值积分得到的PCE近似多项式与通过[拉格朗日插值](@entry_id:167052)得到的配置多项式是**完全相同的**。[@problem_id:3330060] 这种等价性源于高斯积分点上的**离散正交性**。具体来说，对于一个与gPC基和积分法则匹配的[张量积](@entry_id:140694)多项式空间，PCE[基函数](@entry_id:170178)在该积分点集上满足加权离散[正交关系](@entry_id:145540)。这确保了从节点值到PCE系数的变换是一个保范变换（[等距同构](@entry_id:273188)），反之亦然。[@problem_id:3330060] 因此，非侵入式[谱投影](@entry_id:265201)和随机配置可以被看作是同一枚硬币的两个面：一个在谱空间（系数）中操作，另一个在物理空间（节点值）中操作。

### 实践考量：收敛性、维度与局限性

在将PCE和SC方法应用于实际问题时，必须考虑其计算成本、收敛行为和内在局限性。

#### [维度灾难](@entry_id:143920)与截断策略

PCE方法的一个核心挑战是**[维度灾难](@entry_id:143920)（curse of dimensionality）**。所需的[基函数](@entry_id:170178)（以及非侵入式方法中的模拟次数）数量会随着维度 $d$ 和多项式阶数 $p$ 的增加而迅速增长。

考虑不同的[基函数](@entry_id:170178)截断策略，其计算成本差异巨大：
- **张量积（Tensor Product, TP）**：包含所有分量次数 $\alpha_i \le p$ 的多项式。[基函数](@entry_id:170178)数量为 $(p+1)^d$，随维度 $d$ [指数增长](@entry_id:141869)。
- **总次数（Total Degree, TD）**：包含所有总次数 $\sum \alpha_i \le p$ 的多项式。[基函数](@entry_id:170178)数量为 $\binom{p+d}{d}$，随维度 $d$ [多项式增长](@entry_id:177086)（阶数为 $p$）。
- **双曲[交叉](@entry_id:147634)（Hyperbolic Cross, HC）**：包含满足 $\prod (\alpha_i+1) \le p+1$ 的多项式，优先考虑低阶[交叉](@entry_id:147634)项。其[基函数](@entry_id:170178)数量增长比总次数截断更慢。

例如，对于一个 $d=6$ 维、 $p=4$ 阶的问题，张量积基需要 $5^6 = 15625$ 项，总次[数基](@entry_id:634389)需要 $\binom{10}{6} = 210$ 项，而双曲[交叉](@entry_id:147634)基仅需 $40$ 项。[@problem_id:3330072] 显然，总次数和双曲[交叉](@entry_id:147634)等稀疏化策略对于缓解[维度灾难](@entry_id:143920)至关重要，使得PCE在更高维度的问题中成为可能。

#### 方法选择：[多项式混沌](@entry_id:196964) vs. 蒙特卡洛

PCE的性能与模型的**光滑性**密切相关。将其与不依赖光滑性的[蒙特卡洛](@entry_id:144354)（Monte Carlo, MC）方法比较，可以揭示其适用范围。[@problem_id:3330097]
- **MC方法**：其[均方根误差](@entry_id:170440)以 $\mathcal{O}(N^{-1/2})$ 的速率收敛，其中 $N$ 是样本数。这个速率与问题维度 $d$ 和模型光滑性无关。
- **PCE方法**：
    - 对于**光滑（例如，解析）**的模型响应，PCE系数会快速衰减，导致误差呈**谱收敛**（即比任何多项式速率都快，如[指数收敛](@entry_id:142080)）。在低维到中等维度下，PCE可以用远少于MC方法的计算成本达到更高的精度。[@problem_id:3330097]
    - 然而，在**高维度**下，即使是稀疏化的PCE，其计算成本也可能因[维度灾难](@entry_id:143920)而变得过高，使得MC方法更具吸[引力](@entry_id:175476)。[@problem_id:3330097]

#### 非光滑性的挑战：[吉布斯现象](@entry_id:138701)

标准PCE方法的一个主要局限性在于处理**非光滑**函数。当模型响应 $u(\boldsymbol{\xi})$ 存在不连续（例如，由激波或阈值效应引起的跳跃）时，其全局[多项式逼近](@entry_id:137391)会表现出**吉布斯（Gibbs）现象**。[@problem_id:3330073]

这具体表现为：
1. 在不连续点附近出现持续的、不会随多项式阶数增加而消失的**[伪振荡](@entry_id:152404)**。
2. 整体收敛速率从谱收敛急剧下降为缓慢的**代数收敛**。例如，对于一个阶跃函数，[均方根误差](@entry_id:170440)的收敛速率仅为 $\mathcal{O}(p^{-1/2})$。[@problem_id:3330073]

这种现象严重破坏了PCE的精度和效率。相比之下，MC方法的收敛性不受模型[光滑性](@entry_id:634843)影响，因此对于具有不连续或低正则性的问题，MC通常是更可靠和稳健的选择。[@problem_id:3330097] 克服[吉布斯现象](@entry_id:138701)是PCE研究中的一个前沿领域，发展出了多元素PCE（multi-element PCE）、重构PCE（reconstruction PCE）等高级技术。