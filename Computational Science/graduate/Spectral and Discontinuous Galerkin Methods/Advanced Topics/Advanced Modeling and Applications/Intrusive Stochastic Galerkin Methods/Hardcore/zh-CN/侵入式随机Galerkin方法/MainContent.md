## 引言
在科学与工程领域，[偏微分方程](@entry_id:141332)（PDE）是描述物理现象的核心工具。然而，模型参数、边界条件或几何形状中固有的不确定性，常常限制了预测的可靠性。如何系统性地量化这些不确定性对[系统响应](@entry_id:264152)的影响，是现代计算科学面临的关键挑战。侵入式随机Galerkin（SG）方法为此提供了一个严谨而强大的数学框架，它并非通过重复采样来探索不确定性空间，而是将不确定性直接嵌入到控制方程的结构中，将一个随机PDE转化为一个可求解的、更大的[确定性系统](@entry_id:174558)。

本文旨在全面解析侵入式SG方法。通过学习，读者将能够理解其背后的[谱方法](@entry_id:141737)思想，并掌握其在实践中的应用与挑战。我们将分三个核心部分展开探讨：

在“原理与机制”一章中，我们将深入其数学基础，从[广义多项式混沌](@entry_id:749788)（gPC）展开如何表示不确定性，到[Galerkin投影](@entry_id:145611)如何构建耦合的确定性[方程组](@entry_id:193238)。

接着，在“应用与跨学科联系”一章中，我们将理论联系实际，探索该方法在[流体动力学](@entry_id:136788)、固体力学和计算科学等领域的具体应用，展示其解决真实世界问题的能力。

最后，在“动手实践”部分，我们将通过一系列引导性练习，巩固关键概念，并为读者提供将理论应用于计算实践的初步经验。

## 原理与机制

侵入式随机[Galerkin方法](@entry_id:260906)（Intrusive Stochastic Galerkin, SG）是一种功能强大的[范式](@entry_id:161181)，用于求解具有不确定性参数的[偏微分方程](@entry_id:141332)（PDE）。其核心思想是将不确定性直接融入控制方程的数学结构中，从而将一个[随机偏微分方程](@entry_id:188292)转化为一个等效的、更大的确定性[方程组](@entry_id:193238)。本章将详细阐述该方法的基本原理和核心机制，从[广义多项式混沌](@entry_id:749788)（gPC）表示法的基础，到[Galerkin投影](@entry_id:145611)的实施，再到所得系统的结构、挑战和局限性。

### [广义多项式混沌](@entry_id:749788)展开：不确定性的[谱表示](@entry_id:153219)

侵入式方法的基础是**[广义多项式混沌](@entry_id:749788)（Generalized Polynomial Chaos, gPC）展开**。其精髓在于，一个具有[有限方差](@entry_id:269687)的[随机变量](@entry_id:195330)或[随机过程](@entry_id:159502)，可以被谱展开为一个定义在标准[随机变量](@entry_id:195330)上的正交多项式级数。

假设我们研究的系统依赖于一个随机向量 $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d) \in \mathbb{R}^d$，其[联合概率密度函数](@entry_id:267139)（PDF）为 $\rho(\boldsymbol{\xi})$。任何一个依赖于 $\boldsymbol{\xi}$ 且平方可积的随机量 $Y(\boldsymbol{\xi})$ 都可以表示为：
$$
Y(\boldsymbol{\xi}) = \sum_{\alpha \in \mathbb{N}_0^d} y_{\alpha} \Psi_{\alpha}(\boldsymbol{\xi})
$$
其中 $\{y_{\alpha}\}$ 是确定性的展开系数，$\{\Psi_{\alpha}(\boldsymbol{\xi})\}$ 是一组多变量[正交多项式](@entry_id:146918)[基函数](@entry_id:170178)。这些[基函数](@entry_id:170178)相对于由 $\rho(\boldsymbol{\xi})$ 定义的[加权内积](@entry_id:163877)是正交的：
$$
\langle \Psi_{\alpha}, \Psi_{\beta} \rangle_{\rho} := \mathbb{E}[\Psi_{\alpha}(\boldsymbol{\xi}) \Psi_{\beta}(\boldsymbol{\xi})] = \int_{\mathbb{R}^d} \Psi_{\alpha}(\boldsymbol{\xi}) \Psi_{\beta}(\boldsymbol{\xi}) \rho(\boldsymbol{\xi}) \, d\boldsymbol{\xi} = \delta_{\alpha\beta}
$$
这里 $\delta_{\alpha\beta}$ 是Kronecker delta符号，$\mathbb{E}[\cdot]$ 表示数学期望。

#### [基函数](@entry_id:170178)的选择：Wiener-Askey框架

为了确保gPC展开具有最佳的收敛性质（即所谓的谱收敛），[基函数](@entry_id:170178)的选择至关重要。**Wiener-Askey多项式框架**为不同类型的[概率分布](@entry_id:146404)指定了相应的最优[正交多项式](@entry_id:146918)族。关键在于，多项式族的正交性权重函数必须与[随机变量](@entry_id:195330)的概率密度函数相匹配。最常见的对应关系包括：

*   **[高斯分布](@entry_id:154414)** ($\mathcal{N}(0,1)$)：对应**概率论者的[Hermite多项式](@entry_id:153594)**，其权重函数为 $\frac{1}{\sqrt{2\pi}} \exp(-x^2/2)$。
*   **[均匀分布](@entry_id:194597)** ($\mathrm{Uniform}(-1,1)$)：对应**[Legendre多项式](@entry_id:141510)**，其权重函数为 $\frac{1}{2}$。
*   **Gamma[分布](@entry_id:182848)**：对应**[广义Laguerre多项式](@entry_id:180857)**。
*   **Beta[分布](@entry_id:182848)**：对应**[Jacobi多项式](@entry_id:197425)**。

当随机向量 $\boldsymbol{\xi}$ 的分量相互独立时，其联合PDF是边际PDF的乘积，即 $\rho(\boldsymbol{\xi}) = \prod_{i=1}^d \rho_i(\xi_i)$。在这种情况下，多变量gPC[基函数](@entry_id:170178)可以方便地通过[张量积](@entry_id:140694)构建，即 $\Psi_{\alpha}(\boldsymbol{\xi}) = \prod_{i=1}^d \psi_{\alpha_i}^{(i)}(\xi_i)$，其中 $\{\psi_n^{(i)}\}$ 是与[边际分布](@entry_id:264862) $\rho_i$ 相应的单变量正交多项式族。

例如，考虑一个三维随机向量 $\boldsymbol{\xi} = (\xi_1, \xi_2, \xi_3)$，其分量[相互独立](@entry_id:273670)，[分布](@entry_id:182848)分别为[标准正态分布](@entry_id:184509) $\xi_1 \sim \mathcal{N}(0,1)$、[均匀分布](@entry_id:194597) $\xi_2 \sim \mathrm{Uniform}(-1,1)$ 和Gamma[分布](@entry_id:182848) $\xi_3 \sim \mathrm{Gamma}(k=2, \theta=1)$。为了构建一个关于联合PDF $\rho(\boldsymbol{\xi}) = \rho_1(\xi_1)\rho_2(\xi_2)\rho_3(\xi_3)$ 的[标准正交基](@entry_id:147779)，我们需要为每个分量选择匹配的多项式族并进行适当的归一化 。

1.  对于 $\xi_1 \sim \mathcal{N}(0,1)$，PDF为 $\rho_1(x) = \frac{1}{\sqrt{2\pi}} \exp(-x^2/2)$。我们选择概率论者的[Hermite多项式](@entry_id:153594) $\mathrm{He}_n(x)$，其[正交关系](@entry_id:145540)为 $\mathbb{E}[\mathrm{He}_n \mathrm{He}_m] = n! \delta_{nm}$。[标准正交基函数](@entry_id:193867)为 $\psi_n^{(H)}(x) = \mathrm{He}_n(x) / \sqrt{n!}$。
2.  对于 $\xi_2 \sim \mathrm{Uniform}(-1,1)$，PDF为 $\rho_2(x) = 1/2$。我们选择Legendre多项式 $P_n(x)$，其在权重为1下的[正交关系](@entry_id:145540)为 $\int_{-1}^1 P_n P_m dx = \frac{2}{2n+1}\delta_{nm}$。因此，相对于 $\rho_2$ 的[内积](@entry_id:158127)，$\langle P_n, P_m \rangle_{\rho_2} = \frac{1}{2n+1}\delta_{nm}$。[标准正交基函数](@entry_id:193867)为 $\psi_n^{(L)}(x) = \sqrt{2n+1} P_n(x)$。
3.  对于 $\xi_3 \sim \mathrm{Gamma}(2,1)$，PDF为 $\rho_3(x) = x \exp(-x)$。这对应于参数为 $\alpha=1$ 的[广义Laguerre多项式](@entry_id:180857) $L_n^{(1)}(x)$，其[正交关系](@entry_id:145540)为 $\int_0^\infty L_n^{(1)} L_m^{(1)} x^1 e^{-x} dx = (n+1) \delta_{nm}$。[标准正交基函数](@entry_id:193867)为 $\psi_n^{(\mathrm{Lag})}(x) = L_n^{(1)}(x) / \sqrt{n+1}$。

最终，多变量标准正交基由这些单变量基的[张量积](@entry_id:140694)构成：$\Psi_{\alpha}(\boldsymbol{\xi}) = \psi_{\alpha_1}^{(H)}(\xi_1) \psi_{\alpha_2}^{(L)}(\xi_2) \psi_{\alpha_3}^{(\mathrm{Lag})}(\xi_3)$。

#### 截断与维数灾难

在实际计算中，无限级数必须被截断为有限项。一个常见的截断策略是**总阶数（total-degree）截断**，即保留所有多项式总阶数不超过 $p$ 的[基函数](@entry_id:170178)。其多重[指标集](@entry_id:268489)定义为：
$$
\mathcal{A}_p = \{\alpha \in \mathbb{N}_0^d : |\alpha|_1 = \sum_{i=1}^d \alpha_i \le p\}
$$
这个集合中[基函数](@entry_id:170178)的数量，即gPC展开的项数（或称随机模式的数量），可以通过[组合数学](@entry_id:144343)中的“[隔板法](@entry_id:152143)”推导得出 。其基数（cardinality）为：
$$
P = |\mathcal{A}_p| = \binom{p+d}{d} = \frac{(p+d)!}{p!d!}
$$
这个公式揭示了gPC方法的一个核心挑战。当随机维数 $d$ 很高时，即使多项式阶数 $p$ 不大，[基函数](@entry_id:170178)的数量 $P$ 也会迅速增长。对于固定的 $p$ 和 $d \gg 1$， $P$ 的增长趋势为 $\mathcal{O}(d^p)$。这种关于维数的幂次增长，虽然优于张量积截断（其[基数](@entry_id:754020)为 $(p+1)^d$）的[指数增长](@entry_id:141869)，但仍然构成了所谓的**[维数灾难](@entry_id:143920)（curse of dimensionality）**。这意味着对于高维不确定性问题，gPC展开的模式数量会变得异常庞大，给计算带来巨大压力。

### 侵入式[Galerkin投影](@entry_id:145611)原理

侵入式方法的核心在于将gPC展开直接代入到控制方程中，并利用[Galerkin方法](@entry_id:260906)来求解未知的gPC系数。

考虑一个一般的含参数PDE：
$$
\mathcal{L}(x, \boldsymbol{\xi}; u) = f(x)
$$
其中 $\mathcal{L}$ 是一个微分算子，其系数可能依赖于随机参数 $\boldsymbol{\xi}$， $u(x, \boldsymbol{\xi})$ 是待求的随机解。侵入式SG方法假设解和所有不确定的输入参数都可以用截断的gPC[级数表示](@entry_id:175860)：
$$
u(x, \boldsymbol{\xi}) \approx u_p(x, \boldsymbol{\xi}) = \sum_{j=0}^{P-1} u_j(x) \Psi_j(\boldsymbol{\xi})
$$
$$
k(x, \boldsymbol{\xi}) \approx k_R(x, \boldsymbol{\xi}) = \sum_{r=0}^{R-1} k_r(x) \Psi_r(\boldsymbol{\xi})
$$
这里，$u_j(x)$ 是待求的确定性系数场（或称模式），$k_r(x)$ 是已知的输入系数的gPC模式。

将这些展开式代入原PDE，得到一个依赖于 $\boldsymbol{\xi}$ 的残差方程：
$$
\text{Res}(x, \boldsymbol{\xi}) = \mathcal{L}(x, \boldsymbol{\xi}; u_p) - f(x) \neq 0
$$
[Galerkin原理](@entry_id:167636)要求这个残差与gPC基空间中的每一个[基函数](@entry_id:170178)都正交。这意味着对于每一个测试函数 $\Psi_i(\boldsymbol{\xi})$（其中 $i=0, 1, \dots, P-1$），其[加权内积](@entry_id:163877)（即数学期望）为零：
$$
\langle \text{Res}(x, \boldsymbol{\xi}), \Psi_i(\boldsymbol{\xi}) \rangle_{\rho} = \mathbb{E}[\text{Res}(x, \boldsymbol{\xi}) \Psi_i(\boldsymbol{\xi})] = 0
$$
这个过程将一个随机PDE转化为了一个包含 $P$ 个耦合的确定性PDE的系统，其未知量为系数场 $\{u_j(x)\}_{j=0}^{P-1}$。

#### 耦合系统的结构

以一个线性[椭圆问题](@entry_id:146817)为例，可以更清晰地看到所得系统的结构 。考虑随机[扩散](@entry_id:141445)问题：
$$
- \nabla \cdot (k(x, \boldsymbol{\xi}) \nabla u(x, \boldsymbol{\xi})) = f(x)
$$
经过空间弱形式和随机[Galerkin投影](@entry_id:145611)后，对于每个测试模式 $\Psi_i$，我们得到一个耦合的确定性弱形式方程：
$$
\sum_{j=0}^{P-1} \mathbb{E}[\Psi_i \Psi_j k(x, \boldsymbol{\xi})] \int_D \nabla u_j(x) \cdot \nabla v(x) \, dx = \mathbb{E}[\Psi_i] \int_D f(x) v(x) \, dx
$$
代入 $k(x, \boldsymbol{\xi})$ 的gPC展开 $k(x, \boldsymbol{\xi}) = \sum_{r=0}^{R-1} k_r(x) \Psi_r(\boldsymbol{\xi})$，左侧的耦合项变为：
$$
\sum_{j=0}^{P-1} \sum_{r=0}^{R-1} \mathbb{E}[\Psi_i \Psi_j \Psi_r] \int_D k_r(x) \nabla u_j(x) \cdot \nabla v(x) \, dx
$$
这里的核心是**三乘积期望** $T_{ijr} := \mathbb{E}[\Psi_i \Psi_j \Psi_r]$。这些标量值决定了不同随机模式 $u_j$ 之间的耦合强度。在经过空间有限元离散后，整个系统可以写成一个巨大的块矩阵方程。若 $U_j$ 是模式 $u_j(x)$ 的有限元系数向量，$K^{(r)}$ 是由 $k_r(x)$ 产生的确定性刚度矩阵，则第 $i$ 个块方程的形式为：
$$
\sum_{j=0}^{P-1} \left( \sum_{r=0}^{R-1} T_{ijr} K^{(r)} \right) U_j = \delta_{i0} F
$$
其中 $F$ 是确定性[载荷向量](@entry_id:635284)，$\delta_{i0}$ 源于 $\mathbb{E}[\Psi_i]=\delta_{i0}$（假设 $\Psi_0=1$）。这表明，对于确定性源项，驱动力仅作用于平均场模式（$i=0$）。

### 随机Galerkin系统的性质与实例

#### 具体实现：一个简单的[扩散](@entry_id:141445)问题

为了更具体地理解上述过程，我们考虑一个一维随机[扩散](@entry_id:141445)问题 。设[扩散](@entry_id:141445)系数为 $a(x, \xi) = \bar{a} + \sigma \sqrt{2}\sin(\pi x) \xi$，其中 $\xi \sim \mathcal{N}(0,1)$。我们用单个空间[基函数](@entry_id:170178) $v_1(x) = \sqrt{2}\sin(\pi x)$ 和一阶gPC展开（[基函数](@entry_id:170178)为 $\Psi_0=1, \Psi_1=\xi$）来近似解 $u(x,\xi) \approx (u_0\Psi_0(\xi) + u_1\Psi_1(\xi))v_1(x)$。

经过空间和随机[Galerkin投影](@entry_id:145611)后，我们得到一个关于系数 $(u_0, u_1)$ 的 $2 \times 2$ 线性方程组：
$$
\begin{pmatrix} \pi^2 \bar{a} & \frac{4\sqrt{2}\pi}{3} \sigma \\ \frac{4\sqrt{2}\pi}{3} \sigma & \pi^2 \bar{a} \end{pmatrix} \begin{pmatrix} u_0 \\ u_1 \end{pmatrix} = \begin{pmatrix} \frac{2\sqrt{2}}{\pi} \\ 0 \end{pmatrix}
$$
这个简单的例子清晰地展示了侵入式方法的核心特征：
1.  **耦合性**：[系统矩阵](@entry_id:172230)的非对角线项（源于 $\mathbb{E}[\xi \cdot \text{operator}]$）耦合了平均场模式 $u_0$ 和一阶随机模式 $u_1$。
2.  **确定性**：最终求解的是一个确定性的代数系统。
3.  **直接性**：一旦解出 $(u_0, u_1)$，我们就获得了gPC系数，从而可以直接构造解的近似、计算其[统计矩](@entry_id:268545)（例如，均值 $\mathbb{E}[u] = u_0$，[方差](@entry_id:200758) $\text{Var}[u] = u_1^2 \text{Var}[\Psi_1] = u_1^2$）。

#### 系统矩阵的稀疏性

尽管SG系统是耦合的，但其耦合结构通常是高度稀疏的。三乘积期望 $T_{ijr} = \mathbb{E}[\Psi_i \Psi_j \Psi_r]$ 具有重要的**选择定则（selection rules）**。例如，对于[Hermite多项式](@entry_id:153594)，当且仅当 $i,j,r$ 满足三角不等式（即任意两个之和大于等于第三个）且 $i+j+r$ 为偶数时，$T_{ijr}$ 才非零。

考虑一个[扩散](@entry_id:141445)系数为二阶gPC展开 $a(z) = a_0\Psi_0 + a_1\Psi_1 + a_2\Psi_2$ 的情况 。如果解用三阶gPC展开近似，所得的 $4 \times 4$ [耦合矩阵](@entry_id:191757) $C$ 的[稀疏性](@entry_id:136793)就由三乘积 $\mathbb{E}[\Psi_i \Psi_k \Psi_j]$（其中 $k \in \{0,1,2\}$）的非零性决定。利用选择定则可以发现，该矩阵并非全满的。例如，$C_{03}$ 项依赖于 $\mathbb{E}[\Psi_0 \Psi_k \Psi_3]$，其中 $k \in \{0,1,2\}$。根据[三角不等式](@entry_id:143750)，$k$ 必须大于等于 $|3-0|=3$，这与 $k$ 的取值范围矛盾，因此 $C_{03}=0$。这种稀疏性对于开发高效的求解器至关重要。

对于具有[仿射参数](@entry_id:260625)依赖性（$k = k_0 + \sum \xi_m k_m$）的更一般情况，系统矩阵可以表示为Kronecker[积之和](@entry_id:266697)，例如 $\sum_{k=0}^d K_k \otimes G_k$  。由于[经典正交多项式](@entry_id:192726)的[三项递推关系](@entry_id:176845)，矩阵 $G_k$ (其元素为 $\mathbb{E}[\xi_k \Psi_\alpha \Psi_\beta]$) 具有极稀疏的结构（例如，每个模式仅与其“邻近”[模式耦合](@entry_id:752088)），这使得利用Krylov[子空间](@entry_id:150286)等迭代方法求解大型SG系统成为可能。

#### 时间依赖问题与质量矩阵

对于时间依赖问题，如 $\partial_t u + \mathcal{L}(u) = 0$，SG方法会产生一个[常微分方程](@entry_id:147024)（ODE）组 $\mathbf{M} \dot{\mathbf{U}} = \mathbf{R}(\mathbf{U})$，其中 $\mathbf{U}$ 是所有gPC系数的向量。**[质量矩阵](@entry_id:177093)** $\mathbf{M}$ 的结构对[时间积分](@entry_id:267413)方案的效率有重大影响。

一个显著的优点是，如果空间离散（例如，使用模态[间断Galerkin方法](@entry_id:748369)）和随机空间离散都采用标准正交基，则全局质量矩阵将是对角矩阵，甚至是[单位矩阵](@entry_id:156724) 。这是因为质量矩阵的项形如 $\mathbb{E}[\int_D (\phi_i \Psi_k)(\phi_j \Psi_l) d x]$，由于空间和随机[基函数](@entry_id:170178)的双重正交性，该项等于 $\delta_{ij}\delta_{kl}$（在适当归一化后）。一个单位质量矩阵意味着ODE系统是显式的，即 $\dot{\mathbf{U}} = \mathbf{R}(\mathbf{U})$，可以直接使用[显式时间积分](@entry_id:165797)格式（如Runge-Kutta），而无需在每个时间步求解一个[大型线性系统](@entry_id:167283)。

### 挑战与局限性

尽管侵入式SG方法功能强大，但也面临着一些重要的挑战和固有的局限性。

#### [非线性](@entry_id:637147)与闭合问题

当PDE包含[非线性](@entry_id:637147)项时，例如 $u^2$，会产生所谓的**闭合问题（closure problem）** 。如果 $u$ 是一个 $p$ 阶gPC展开，那么 $u^2$ 的展开将包含最高达到 $2p$ 阶的多项式。然而，标准的[Galerkin投影](@entry_id:145611)将这个 $2p$ 阶的多项式投影回原来的 $p$ 阶空间。这个投影过程会丢弃[高阶模](@entry_id:750331)式的信息，从而引入截断误差。为了精确计算[非线性](@entry_id:637147)项的[Galerkin投影](@entry_id:145611)，需要在随机空间中进行数值积分（求积），而为了避免混淆误差（aliasing），求积法则必须能够精确积分最高达到 $3p$ 阶的多项式（因为被积函数包含一个最高 $p$ 阶的测试函数和一个最高 $2p$ 阶的[非线性](@entry_id:637147)项）。

#### 强制性丧失

[Galerkin方法](@entry_id:260906)的数学基础，如[Lax-Milgram定理](@entry_id:137966)，依赖于[双线性形式](@entry_id:746794)的**强制性（coercivity）**。对于[椭圆方程](@entry_id:169190)，这通常与[扩散](@entry_id:141445)系数的正定性相关。一个令人惊讶且重要的事实是：即使对于每一个参数实现，[扩散](@entry_id:141445)系数 $a(\boldsymbol{\xi})$ 都是正的，从而保证确定性问题是良定的，但对应的SG系统却可能丧失强制性。

更糟糕的是，如果 $a(\boldsymbol{\xi})$ 以正概率取负值，SG系统几乎肯定会丧失强制性。考虑一个简单的例子 $a(\xi) = 1 - 2\xi$，其中 $\xi \sim \mathcal{U}(-1,1)$ 。当 $\xi > 1/2$ 时，$a(\xi)$ 为负。尽管其均值 $\mathbb{E}[a(\xi)]=1$ 是正的，但在一阶gPC空间中构造的 $2 \times 2$ SG矩阵的[特征值](@entry_id:154894)之一为负。这意味着SG矩阵是**不定**的，双线性形式不再是强制的。其后果是：[Lax-Milgram定理](@entry_id:137966)不再适用，SG解的存在性和唯一性无法保证，并且标准的[迭代求解器](@entry_id:136910)（如[共轭梯度法](@entry_id:143436)）会失效。这个问题不会随着gPC阶数的增加而消失，反而可能变得更糟，因为更高阶的gPC空间能更精确地“捕捉”到系数为负的区域。

#### 非光滑解与收敛性损失

gPC展开的谱收敛（即误差随 $p$ 指数下降）依赖于解关于随机参数的高度光滑性（理想情况下是解析的）。然而，即使PDE本身是线性和光滑的，我们所关心的**目标量（Quantity of Interest, QoI）**也可能是非光滑的。

考虑一个简单的例子，解 $u(x_0; \xi)$ 线性依赖于 $\xi$，但我们关心的是它是否超过某个阈值 $\theta$，即QoI为指标函数 $Q(\xi) = \mathbf{1}\{u(x_0; \xi) \ge \theta\}$ 。这个QoI是一个关于 $\xi$ 的[阶跃函数](@entry_id:159192)，它在某个点 $\xi^\star$ 处有[跳跃间断](@entry_id:139886)。用全局光滑的多项式基（如Legendre多项式）去逼近这样一个[间断函数](@entry_id:143848)，会产生**[Gibbs现象](@entry_id:138701)**（在间断点附近的[振荡](@entry_id:267781)），并且[收敛率](@entry_id:146534)会从谱收敛退化为缓慢的代数收敛。

一个有效的补救措施是采用**多单元[多项式混沌](@entry_id:196964)（Multi-Element Polynomial Chaos, ME-PC）**。这种方法将[参数空间](@entry_id:178581)划分为多个子域（单元），使得函数在每个子域内是光滑的。对于上述阶跃函数，我们可以在 $\xi^\star$ 处分割参[数域](@entry_id:155558)。在侵入式框架下，这相当于在参数空间上应用**间断Galerkin（DG）**方法，从而在每个光滑[子域](@entry_id:155812)内恢复谱收敛。

### 与非侵入式方法的对比

最后，值得将侵入式SG方法与其主要替代方案——**非侵入式谱方法**（如[随机配置法](@entry_id:174778)，Stochastic Collocation）进行对比。

*   **工作流程与系统结构** ：
    *   **侵入式SG**：求解一个尺寸为 $N_h \times P$ 的大型、耦合的[确定性系统](@entry_id:174558)。需要修改现有的确定性求解器来处理特殊的块耦合结构。
    *   **非侵入式SC**：在[参数空间](@entry_id:178581)中选择一组[配置点](@entry_id:169000)，对每个点求解一个标准的、尺寸为 $N_h$ 的确定性问题。这些求解是完全独立的，可以利用现成的、高度优化的确定性求解器并行执行。

*   **获取统计信息** ：
    *   **侵入式SG**：直接计算出解的gPC系数 $\{u_\alpha\}$。一旦系数已知，任何多项式形式的[统计矩](@entry_id:268545)（如均值、[方差](@entry_id:200758)）或QoI都可以通过对系数进行代数运算来精确计算，无需额外的采样或积分。
    *   **非侵入式SC**：得到的是解在[配置点](@entry_id:169000)上的一系列“快照”。要获得[统计矩](@entry_id:268545)或gPC系数，需要进行后处理，通常是通过数值求积（例如，$\mathbb{E}[u] \approx \sum w_q u(\xi^{(q)})$）或基于最小二乘/投影的回归。

总而言之，侵入式方法通过深入修改控制方程，提供了对解的[谱表示](@entry_id:153219)的直接访问，这在分析和后处理中具有优势。然而，这种“侵入性”也带来了实现上的复杂性，并使其在面对强[非线性](@entry_id:637147)、非[光滑性](@entry_id:634843)或强制性丧失等问题时显得较为脆弱。相比之下，非侵入式方法则以其简单、并行和非侵入的特性，为更广泛的问题提供了一个鲁棒且灵活的替代方案。