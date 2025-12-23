## 引言
在现代科学与工程计算中，模型参数、边界条件与几何形状的不确定性无处不在，准确量化这些不确定性对模型预测结果的影响至关重要。传统方法如[蒙特卡洛模拟](@entry_id:193493)虽然通用，但往往需要巨大的计算成本才能获得收敛的统计结果，这在求解复杂[偏微分方程](@entry_id:141332)（PDE）等大规模问题时尤其突出。[多项式混沌](@entry_id:196964)（Polynomial Chaos, PC）与随机伽辽金（Stochastic Galerkin, SG）方法应运而生，为解决这一难题提供了高效的谱方法框架。

本文旨在系统性地介绍这一强大的不确定性量化工具。通过本文的学习，读者将能够深入理解[随机变量](@entry_id:195330)的[谱表示](@entry_id:153219)思想，并掌握如何将一个随机PDE转化为一个确定性的、可求解的大型系统。文章将分为三个核心部分：在“原理与机制”一章中，我们将奠定该方法的数学基础，从[希尔伯特空间](@entry_id:261193)的概念到[广义多项式混沌](@entry_id:749788)的构建；接着，在“应用与交叉学科联系”一章中，我们将探索该方法在[固体力学](@entry_id:164042)、[流体力学](@entry_id:136788)、[地球科学](@entry_id:749876)乃至机器学习等前沿领域的广泛应用；最后，通过“动手实践”部分，读者将有机会亲手实现相关算法，将理论知识转化为实践能力。让我们首先从其核心的数学原理开始探索。

## 原理与机制

本章深入探讨[多项式混沌](@entry_id:196964)（Polynomial Chaos, PC）和随机伽辽金（Stochastic Galerkin, SG）方法的核心原理与运作机制。我们将从[随机变量](@entry_id:195330)的希尔伯特空间表示法入手，逐步构建起一个完整的理论框架，用以理解和应用这些强大的[不确定性量化](@entry_id:138597)工具。

### [随机变量](@entry_id:195330)的希尔伯特空间与[谱表示](@entry_id:153219)

随机伽辽金方法的基础，是将不确定性问题置于一个严谨的泛函分析框架中。考虑一个由样本空间 $\Omega$、$\sigma$-代数 $\mathcal{F}$ 和概率测度 $\mathbb{P}$ 构成的[概率空间](@entry_id:201477) $(\Omega, \mathcal{F}, \mathbb{P})$。我们关注的是所有平方可积的实值[随机变量](@entry_id:195330)构成的集合，这一集合在定义了合适的[内积](@entry_id:158127)后，便构成了一个[希尔伯特空间](@entry_id:261193)，记为 $L^2(\Omega)$。该空间中的[内积](@entry_id:158127)定义为两个[随机变量乘积的期望](@entry_id:262447)值：
$$
\langle X, Y \rangle = \mathbb{E}[XY] = \int_{\Omega} X(\omega)Y(\omega) \, d\mathbb{P}(\omega)
$$
这自然地导出了范数 $\|X\|_{L^2} = \sqrt{\mathbb{E}[X^2]}$。

[多项式混沌](@entry_id:196964)的核心思想，正是将 $L^2(\Omega)$ 中的一个[随机变量](@entry_id:195330) $u(\xi)$ （例如，一个[随机偏微分方程](@entry_id:188292)的解），通过一组[正交基](@entry_id:264024)函数 $\{\Psi_\alpha\}_{\alpha=0}^\infty$ 进行**[谱表示](@entry_id:153219)（spectral representation）**：
$$
u(\xi) = \sum_{\alpha=0}^{\infty} u_\alpha \Psi_\alpha(\xi)
$$
其中，$u_\alpha$ 是确定性的展开系数，而 $\xi$ 是驱动系统不确定性的一个或一组基础[随机变量](@entry_id:195330)。为了使这种表示唯一且收敛，[基函数](@entry_id:170178)系 $\{\Psi_\alpha\}$ 必须是**完备的（complete）**。一个[基函数](@entry_id:170178)系是完备的，意味着它的所有有限线性组合张成的空间在 $L^2(\Omega)$ 中是稠密的。换言之，任何一个平方可积的[随机变量](@entry_id:195330)都可以通过这个[基函数](@entry_id:170178)系以任意精度逼近。

那么，何种条件下我们能保证一个正交多项式基是完备的呢？这取决于基础[随机变量](@entry_id:195330) $\xi$ 的[概率测度](@entry_id:190821)。

*   **[紧支集](@entry_id:276214)测度**：若[随机变量](@entry_id:195330) $\xi$ 的概率测度支撑在一个紧区间（如[均匀分布](@entry_id:194597)）上，根据 [Stone-Weierstrass 定理](@entry_id:146002)，多项式函数集在[连续函数空间](@entry_id:150395)中是稠密的，而[连续函数空间](@entry_id:150395)又在相应的 $L^2$ 空间中是稠密的。因此，通过对单项式基 $\{1, \xi, \xi^2, \dots\}$ 进行格拉姆-施密特（Gram-Schmidt）正交化得到的正交多项式基是完备的 。

*   **全实线测度**：对于支撑在整个实轴上的测度，如[高斯测度](@entry_id:749747)，情况更为复杂。此时，多项式[基的完备性](@entry_id:196285)与所谓的 Hamburger 矩问题（Hamburger moment problem）的确定性相关。Carleman 条件为此提供了一个充分判据。对于[高斯测度](@entry_id:749747)，该条件成立，这意味着相应的厄米特（Hermite）多项式基是完备的 。这构成了最初由 Norbert Wiener 提出的经典[多项式混沌](@entry_id:196964)理论的基础。

*   **[离散测度](@entry_id:183686)**：如果 $\xi$ 的[分布](@entry_id:182848)由有限个（$N$个）具有正概率的点支撑，那么 $L^2(\Omega)$ 空间实际上同构于一个 $N$ 维[向量空间](@entry_id:151108)。此时，一个由 $N$ 个线性无关的多项式（例如，从 $0$ 次到 $N-1$ 次）构成的集合就足以张成整个空间，因此是完备的 。

需要强调的是，**正交性（orthogonality）**与**完备性（completeness）**是两个不同的概念。一个[正交集](@entry_id:268255)可能是不完备的。例如，在 $[-1,1]$ 上的勒让德（Legendre）多项式构成一个完备正交基，但如果我们只取其中的偶数阶多项式，这个[子集](@entry_id:261956)虽然仍然是正交的，但它无法表示任何非零的[奇函数](@entry_id:173259)，因此是不完备的 。

### [广义多项式混沌](@entry_id:749788)与[Wiener-Askey格式](@entry_id:174054)

Wiener 的原始工作主要针对高斯随机输入，采用厄米特多项式作为基。然而，在工程和科学问题中，不确定性来源多种多样，远不止高斯分布。**[广义多项式混沌](@entry_id:749788)（generalized Polynomial Chaos, gPC）**将这一思想推广到由更广泛的[概率分布](@entry_id:146404)驱动的系统。

gPC 的核心原则是：为匹配输入[随机变量](@entry_id:195330) $\xi$ 的特定[概率密度函数](@entry_id:140610) $\rho(\xi)$，选择一个与之对应的[正交多项式](@entry_id:146918)族 $\{\psi_n(\xi)\}$。具体而言，这个多项式族必须满足关于权重函数 $\rho(\xi)$ 的[正交关系](@entry_id:145540)：
$$
\langle \psi_m, \psi_n \rangle = \int \psi_m(\xi) \psi_n(\xi) \rho(\xi) \, d\xi = C_n \delta_{mn}
$$
其中 $C_n$ 是一个[归一化常数](@entry_id:752675)，$\delta_{mn}$ 是克罗内克（Kronecker）符号。这种“量身定制”的[基函数](@entry_id:170178)选择，极大地提升了谱展开的收敛速度。

**Wiener-Askey 格式**系统地建立了多种经典[概率分布](@entry_id:146404)与其对应的[正交多项式](@entry_id:146918)族之间的联系。下表总结了其中几个最重要的对应关系 ：

| 随机输入[分布](@entry_id:182848) | 支撑集 | 权重函数 $\rho(\xi)$ | 正交多项式族 |
| :--- | :--- | :--- | :--- |
| 高斯（Gaussian） | $(-\infty, \infty)$ | $\frac{1}{\sqrt{2\pi}} \exp(-\xi^2/2)$ | 概率论者厄米特（Hermite）多项式 |
| 均匀（Uniform） | $[-1, 1]$ | $\frac{1}{2}$ | 勒让德（Legendre）多项式 |
| $\Gamma$ [分布](@entry_id:182848) | $[0, \infty)$ | $\xi^{\alpha} \exp(-\xi)$ | 广义拉盖尔（Laguerre）多项式 |
| $\beta$ [分布](@entry_id:182848) | $[-1, 1]$ | $(1-\xi)^{\alpha}(1+\xi)^{\beta}$ | 雅可比（Jacobi）多项式 |

例如，若输入 $\xi$ 服从标准正态分布，我们应选择概率论者厄米特多项式 $He_n(\xi)$ 作为基。若 $\xi$ 服从 $[-1,1]$ 上的[均匀分布](@entry_id:194597)，则应选择勒让德多项式 $P_n(\xi)$。对于伽马（Gamma）[分布](@entry_id:182848) $\Gamma(k, \theta)$，其[概率密度函数](@entry_id:140610)形式为 $\rho(\xi) \propto \xi^{k-1} \exp(-\xi/\theta)$，通过变量代换 $x = \xi/\theta$ 和参数匹配 $\alpha = k-1$，可知应选用广义拉盖尔（Laguerre）多项式 $L_n^{(k-1)}(\xi/\theta)$ 。

### [多项式混沌展开](@entry_id:162793) (PCE)

一旦选定了合适的归一化[正交基](@entry_id:264024) $\{\Psi_\alpha\}$（即 $\mathbb{E}[\Psi_\alpha \Psi_\beta] = \delta_{\alpha\beta}$），我们就可以将一个依赖于[随机变量](@entry_id:195330) $\xi$ 的目标量 $u(\xi)$ （例如，某个物理量或模型输出）表示为**[多项式混沌展开](@entry_id:162793)（Polynomial Chaos Expansion, PCE）**：
$$
u(\xi) = \sum_{\alpha \in \mathcal{A}} u_\alpha \Psi_\alpha(\xi)
$$
在实际计算中，这个和通常被截断到一个有限的多重[指标集](@entry_id:268489) $\mathcal{A}$。

系数 $u_\alpha$ 的计算是该方法的核心步骤之一。利用基[函数的正交性](@entry_id:160337)，我们可以通过**$L^2$-[正交投影](@entry_id:144168)**来确定每个系数：
$$
u_\alpha = \langle u(\xi), \Psi_\alpha(\xi) \rangle = \mathbb{E}[u(\xi) \Psi_\alpha(\xi)] = \int u(\xi) \Psi_\alpha(\xi) \rho(\xi) \, d\xi
$$
这意味着，第 $\alpha$ 个 PCE 系数是目标量 $u(\xi)$ 在[基函数](@entry_id:170178) $\Psi_\alpha(\xi)$ 上的投影。

对于多维随机输入 $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$，我们使用多重指标 $\boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_d)$。一个常用的截断策略是**总阶数截断（total-degree truncation）**，即保留所有满足 $|\boldsymbol{\alpha}| = \sum_{j=1}^d \alpha_j \le p$ 的多项式，其中 $p$ 是展开的最大阶数 。

**示例：计算PCE系数**

考虑一个依赖于二维标准[高斯随机向量](@entry_id:635820) $\boldsymbol{\xi}=(\xi_1, \xi_2)$ 的量 $u(\boldsymbol{\xi}) = \exp(\lambda \xi_1 + \mu \xi_2)$。我们希望找到其PCE展开中对应于多重指标 $\boldsymbol{\alpha}=(2,1)$ 的系数 $u_{(2,1)}$。

根据 Wiener-Askey 格式，我们应使用厄米特多项式。归一化的二维[基函数](@entry_id:170178)是张量积形式 $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \psi_{\alpha_1}(\xi_1)\psi_{\alpha_2}(\xi_2)$，其中 $\psi_k(x) = He_k(x)/\sqrt{k!}$。我们需要的[基函数](@entry_id:170178)是：
$$
\Psi_{(2,1)}(\boldsymbol{\xi}) = \psi_2(\xi_1) \psi_1(\xi_2) = \frac{1}{\sqrt{2!}}(\xi_1^2 - 1) \cdot \frac{1}{\sqrt{1!}}\xi_2 = \frac{1}{\sqrt{2}}(\xi_1^2 - 1)\xi_2
$$
系数 $u_{(2,1)}$ 通过投影计算得出：
$$
u_{(2,1)} = \mathbb{E}[u(\boldsymbol{\xi}) \Psi_{(2,1)}(\boldsymbol{\xi})] = \mathbb{E}\left[ \exp(\lambda \xi_1 + \mu \xi_2) \frac{1}{\sqrt{2}}(\xi_1^2 - 1)\xi_2 \right]
$$
由于 $\xi_1$ 和 $\xi_2$ 是独立的，期望可以分解为两个一维积分的乘积。通过在[高斯测度](@entry_id:749747)下完成平方并利用高斯分布的矩性质，可以求得这两个积分，最终得到 ：
$$
u_{(2,1)} = \frac{\lambda^2 \mu}{\sqrt{2}} \exp\left(\frac{\lambda^2 + \mu^2}{2}\right)
$$
这个例子清晰地展示了从定义出发计算PCE系数的完整过程。

### 独立性的关键作用：[张量积](@entry_id:140694)基

当处理多维随机输入 $\boldsymbol{\xi}=(\xi_1, \dots, \xi_d)$ 时，输入变量之间的统计**独立性（independence）**是一个至关重要的性质。它极大地简化了正交基的构造和后续计算。

如果所有输入变量 $\xi_j$ 都是[相互独立](@entry_id:273670)的，那么它们的[联合概率密度函数](@entry_id:267139)（PDF）可以分解为边缘密度函数的乘积：$\rho(\boldsymbol{\xi}) = \prod_{j=1}^d \rho_j(\xi_j)$。这一性质使得 $L^2_\rho$ 空间具有**[张量积](@entry_id:140694)结构（tensor-product structure）**。

这意味着，我们可以为每个独立的变量 $\xi_j$ 分别选择一个与之边缘[分布](@entry_id:182848) $\rho_j$ 相匹配的一维[正交多项式](@entry_id:146918)基 $\{\phi_k^{(j)}\}_{k \ge 0}$，然后通过简单的张量积来构造多维[基函数](@entry_id:170178)：
$$
\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{j=1}^d \phi_{\alpha_j}^{(j)}(\xi_j)
$$
由于独立性使得多维[内积](@entry_id:158127)积分可以分解为一维积分的乘积，因此这个[张量积](@entry_id:140694)基自动地在联合测度下是正交的 ：
$$
\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle_\rho = \prod_{j=1}^d \int \phi_{\alpha_j}^{(j)}(\xi_j) \phi_{\beta_j}^{(j)}(\xi_j) \rho_j(\xi_j) d\xi_j = \prod_{j=1}^d \delta_{\alpha_j \beta_j} = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}
$$
这个性质是[多项式混沌](@entry_id:196964)方法在实际中如此高效和流行的根本原因之一。

### 依赖输入变量的处理

当输入变量**相关（dependent）**时，情况变得复杂。[联合密度函数](@entry_id:263624)不再能分解，张量积结构也随之消失。此时，如果仍然天真地使用由边缘[分布](@entry_id:182848)构成的张量积多项式基，这个基在联合测度下将**不再正交** 。例如，对于相关的 $(\xi_1, \xi_2)$，即使 $\mathbb{E}[\phi_1^{(1)}(\xi_1)]=0$ 且 $\mathbb{E}[\phi_1^{(2)}(\xi_2)]=0$，它们的协[方差](@entry_id:200758) $\mathbb{E}[\phi_1^{(1)}(\xi_1)\phi_1^{(2)}(\xi_2)]$ 通常不为零，这导致了[基函数](@entry_id:170178)的[交叉](@entry_id:147634)[内积](@entry_id:158127)不为零，正交性被破坏 。

面[对相关](@entry_id:203353)输入，必须构造一个直接在联合测度 $\rho(\boldsymbol{\xi})$ 下正交的多项式基。一个直接的构造性方法是**多维[格拉姆-施密特正交化](@entry_id:143035)** 。该过程如下：
1.  选择一个基础的多项式基，通常是按总阶数排序的多元单项式基，如 $\{1, \xi_1, \xi_2, \xi_1^2, \xi_1\xi_2, \xi_2^2, \dots\}$。
2.  应用格拉姆-施密特算法，对这个单项式基进行[正交化](@entry_id:149208)。此过程中的所有[内积](@entry_id:158127)都必须在联合测度 $\rho(\boldsymbol{\xi})$ 下计算。
3.  每一步都进行归一化，得到最终的归一化正交基 $\{\Psi_\alpha\}$。

这个过程在理论上是完备的，但在实践中需要计算所有必要的高阶混合矩 $\mathbb{E}[\xi_1^i \xi_2^j \dots]$，这可能非常困难。在数值上，这个过程等价于构造单项式的矩矩阵（Gram matrix）$G_{ij} = \langle m_i, m_j \rangle_\rho$，然后对其进行 Cholesky 分解 $G=LL^\top$，最终的[正交多项式](@entry_id:146918)可以通过 $L^{-\top}$ 变换从单项式基得到 。

### 随机伽辽金方法求解偏微分方程

现在我们将 PCE 应用于求解带有随机参数的[偏微分方程](@entry_id:141332)（PDE），这就是**随机伽辽金（Stochastic Galerkin, SG）**方法。考虑一个模型问题，如随机[扩散方程](@entry_id:170713) ：
$$
-\nabla \cdot (a(x, \xi) \nabla u(x, \xi)) = f(x)
$$
其中[扩散](@entry_id:141445)系数 $a(x,\xi)$ 和解 $u(x,\xi)$ 都依赖于[随机变量](@entry_id:195330) $\xi$。

SG 方法的步骤如下：
1.  **展开**：将随机系数 $a(x, \xi)$ 和未知的解 $u(x, \xi)$ 都表示为 PCE 形式：
    $$
    a(x, \xi) = \sum_{k=0}^{K} a_k(x) \psi_k(\xi), \quad u(x, \xi) = \sum_{\alpha=0}^{P} u_\alpha(x) \Psi_\alpha(\xi)
    $$
    注意，这里的系数 $a_k(x)$ 和 $u_\alpha(x)$ 现在是空间变量 $x$ 的函数。

2.  **代入**：将这些展开式代入原始 PDE 中。

3.  **[伽辽金投影](@entry_id:145611)**：将所得的残差方程投影到每一个[基函数](@entry_id:170178) $\Psi_\beta(\xi)$ 上。这通过在随机空间中取[内积](@entry_id:158127)（即取期望）来实现。对于每一个 $\beta = 0, \dots, P$，我们得到一个方程：
    $$
    \mathbb{E}\left[ \left( -\nabla \cdot \left( \sum_{k, \alpha} a_k(x) u_\alpha(x) \psi_k(\xi) \Psi_\alpha(\xi) \right) - f(x) \right) \Psi_\beta(\xi) \right] = 0
    $$

经过整理，我们得到一个关于确定性系数函数 $\{u_\alpha(x)\}$ 的**[耦合偏微分方程组](@entry_id:198181)**：
$$
-\sum_{k=0}^{K} \sum_{\alpha=0}^{P} C_{k\alpha\beta} \nabla \cdot (a_k(x) \nabla u_\alpha(x)) = f(x) \delta_{0\beta}, \quad \text{for } \beta = 0, \dots, P
$$
这个系统将一个随机 PDE 转化为了一个规模更大的确定性 PDE 系统。

### 伽辽金张量的结构与计算

上述耦合系统中的**耦合机制**完全由**三阶张量（triple-product tensor）** $C_{k\alpha\beta}$ 决定，其定义为：
$$
C_{k\alpha\beta} = \mathbb{E}[\psi_k \Psi_\alpha \Psi_\beta] = \int \psi_k(\xi) \Psi_\alpha(\xi) \Psi_\beta(\xi) \rho(\xi) d\xi
$$
这些张量的值决定了不同 PCE 模态 $u_\alpha$ 之间的相互作用强度。

在输入变量独立且[基函数](@entry_id:170178)为[经典正交多项式](@entry_id:192726)（如厄米特、[勒让德多项式](@entry_id:141510)）的情况下，这些三阶张量具有高度的**稀疏性**。这种稀疏性源于[经典正交多项式](@entry_id:192726)的[三项递推关系](@entry_id:176845)。我们可以通过[生成函数](@entry_id:146702)等方法推导出这些张量的解析表达式和**[选择定则](@entry_id:140784)（selection rules）**。例如，对于归一化的厄米特多项式，三阶张量 $\mathbb{E}[\Psi_m \Psi_n \Psi_p]$ 非零的充分必要条件是 ：
1.  **奇偶性**：$m+n+p$ 必须为偶数。
2.  **三角不等式**：$m, n, p$ 必须满足三角不等式，即任意两个之和不小于第三个。

满足这些条件时，其值可以解析计算，例如 $\mathbb{E}[\Psi_1 \Psi_1 \Psi_2] = \sqrt{2}$ 。这种[稀疏性](@entry_id:136793)使得最终的伽辽金系统矩阵呈现出块对角或块带状结构，这对于计算效率至关重要 。

对于包含**[非线性](@entry_id:637147)项**的 PDE，例如反应项 $r(u, \xi) = \sum_q c_q(\xi) u^q$，[伽辽金投影](@entry_id:145611)会产生更复杂的耦合结构。$u^q$ 这一项在 PCE 展开后，会导致PCE系数的**卷积**。投影后的[非线性](@entry_id:637147)项会包含更高阶的耦合张量，形如 ：
$$
T_{p, i_1, \dots, i_q, m} = \mathbb{E}[\psi_p \psi_{i_1} \dots \psi_{i_q} \psi_m]
$$
这些[高阶张量](@entry_id:200122)通常比三阶张量要稠密得多，使得[非线性](@entry_id:637147)问题的计算成本显著增加。

### 数值实现与后处理

#### 求积、[混叠误差](@entry_id:637691)与[去混叠](@entry_id:748248)
在实践中，计算伽辽金张量（如三阶张量）和投影所需的积分通常采用[数值求积](@entry_id:136578)法，如**[高斯求积](@entry_id:146011)（Gauss Quadrature）**。然而，使用有限点数的求积法则会引入**[混叠误差](@entry_id:637691)（aliasing error）**。

考虑对一个[非线性](@entry_id:637147)项 $u_p^m$ 进行投影，其中 $u_p$ 是 $p$ 阶PCE。被积函数是一个最高阶数为 $p \cdot m + p = p(m+1)$ 的多项式。如果[求积法则](@entry_id:753909)的精度不足以精确积分这个多项式，高阶多项式分量的能量就会被错误地“混叠”到我们计算的低阶系数上，导致结果失真 。

为了完全消除[混叠误差](@entry_id:637691)，即实现**[去混叠](@entry_id:748248)（de-aliasing）**，[高斯求积](@entry_id:146011)的节点数 $N_q$ 必须足够多，以确保其对于最高阶的被积多项式是精确的。一个 $N_q$ 点的[高斯-勒让德求积](@entry_id:138201)法则可以精确积分最高 $2N_q-1$ 次的多项式。因此，我们必须满足：
$$
2N_q - 1 \ge p(m+1)
$$
由此可得，保证零[混叠误差](@entry_id:637691)所需的最少求积节点数为 ：
$$
N_q = \left\lceil \frac{p(m+1) + 1}{2} \right\rceil
$$
例如，对于一个二次[非线性](@entry_id:637147)项（$m=2$），这导致了著名的 "$2p+1$" 法则的近似形式。

#### 后处理：[统计矩](@entry_id:268545)与全局敏感度分析
PCE 的一个巨大优势在于，一旦获得了 PCE 系数 $\{c_{\boldsymbol{\alpha}}\}$，就可以极其廉价地进行后处理，提取关于模型输出的丰富统计信息。

*   **[统计矩](@entry_id:268545)**：输出的均值和[方差](@entry_id:200758)可以直接从系数中得到。由于 $\Psi_{\mathbf{0}}=1$ 且基是正交的，我们有：
    $$
    \mathbb{E}[Q] = c_{\mathbf{0}}
    $$
    $$
    \mathrm{Var}(Q) = \mathbb{E}[ (Q - \mathbb{E}[Q])^2 ] = \mathbb{E}\left[ \left(\sum_{\boldsymbol{\alpha} \neq \mathbf{0}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}\right)^2 \right] = \sum_{\boldsymbol{\alpha} \neq \mathbf{0}} c_{\boldsymbol{\alpha}}^2
    $$
    [方差](@entry_id:200758)就是所有非零阶系数的平方和。

*   **全局敏感度分析（Global Sensitivity Analysis, GSA）**：**Sobol' 指数**是衡量输入变量对输出[方差](@entry_id:200758)贡献的常用指标。利用 PCE 系数，计算 Sobol' 指数变得异常简单 。
    *   **一阶 Sobol' 指数** $S_i$，衡量变量 $\xi_i$ 的独立贡献，等于所有仅依赖于 $\xi_i$ 的[基函数](@entry_id:170178)对应系数的平方和，再除以总[方差](@entry_id:200758)。
    *   **总 Sobol' 指数** $T_i$，衡量变量 $\xi_i$ 的所有贡献（包括其与其他变量的交互作用），等于所有依赖于 $\xi_i$（无论是否还依赖于其他变量）的[基函数](@entry_id:170178)对应系数的平方和，再除以总[方差](@entry_id:200758)。

形式上，若定义 $\mathcal{A}_i = \{\boldsymbol{\alpha} \neq \mathbf{0} \mid \alpha_i > 0, \alpha_{j \neq i}=0\}$ 和 $\mathcal{A}_{T_i} = \{\boldsymbol{\alpha} \mid \alpha_i > 0\}$，则：
$$
S_i = \frac{\sum_{\boldsymbol{\alpha} \in \mathcal{A}_i} c_{\boldsymbol{\alpha}}^2}{\mathrm{Var}(Q)}, \quad T_i = \frac{\sum_{\boldsymbol{\alpha} \in \mathcal{A}_{T_i}} c_{\boldsymbol{\alpha}}^2}{\mathrm{Var}(Q)}
$$
例如，对于一个具体计算出的 PCE 系数集，我们可以通过简单地对相应系数的平方进行加和，来快速评估各个输入参数的重要性 。这种 PCE 与 GSA 的无缝连接是该方法最强大的应用之一。