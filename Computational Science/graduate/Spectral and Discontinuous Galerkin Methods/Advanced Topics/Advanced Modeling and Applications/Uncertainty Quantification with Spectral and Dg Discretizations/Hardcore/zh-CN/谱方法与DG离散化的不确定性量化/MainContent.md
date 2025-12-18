## 引言
在现代科学与工程计算中，[偏微分方程](@entry_id:141332)（PDEs）是模拟复杂物理现象的基石。然而，实际系统总是伴随着各种不确定性，这些不确定性可能源于材料属性的变异、边界条件的[测量误差](@entry_id:270998)或几何形状的制造公差。准确量化这些输入不确定性如何传播并影响模型预测的输出，即不确定性量化（UQ），对于做出可靠的设计决策和风险评估至关重要。本文旨在系统性地介绍一个强大而灵活的框架，用于解决这一挑战：将高效的谱随机方法与灵活的不连续伽辽金（DG）[空间离散化](@entry_id:172158)相结合。

本文的核心问题是，如何构建一个数学上严谨且计算上可行的方案，以处理由随机参数驱动的PDEs。我们将展示如何将一个复杂的随机PDE问题，转化为一个（可能非常大的）确定性耦合代数系统，并探讨其求解策略。

为实现这一目标，本文将引导读者逐步深入该领域的核心。在第一章“原理与机制”中，我们将奠定理论基础，详细介绍如何使用[Karhunen-Loève展开](@entry_id:751050)和[广义多项式混沌](@entry_id:749788)（gPC）来表示不确定性输入和解，并推导侵入式随机伽辽金方法以及最终系统的[代数结构](@entry_id:137052)。随后，在第二章“应用与交叉学科联系”中，我们将通过[流体动力学](@entry_id:136788)、几何[不确定性分析](@entry_id:149482)和[非线性](@entry_id:637147)[双曲系统](@entry_id:260647)等一系列应用案例，展示该框架在解决真实世界问题中的强大威力与灵活性。最后，在第三章“动手实践”中，我们提供了一系列精心设计的编程练习，帮助读者将理论知识转化为实践技能，亲手构建和分析UQ模型。通过这一从理论到应用再到实践的完整学习路径，读者将全面掌握使用谱方法和[DG离散化](@entry_id:748366)进行[不确定性量化](@entry_id:138597)的核心技术。

## 原理与机制

在为[偏微分方程](@entry_id:141332)（PDEs）进行不确定性量化（UQ）时，我们的核心目标是理解和预测输入参数中的随机性如何传播到系统解。本章深入探讨了实现这一目标的基本原理和机制，重点关注随机输入的[谱表示](@entry_id:153219)方法以及与不连续伽辽金（DG）[空间离散化](@entry_id:172158)方法的结合。我们将从随机性的建模开始，逐步构建一个完整的计算框架，并探讨其理论基础和实现细节。

### 不确定性的表示：从[随机变量](@entry_id:195330)到[随机场](@entry_id:177952)

在对受不确定性影响的物理系统进行建模时，首要任务是以数学上严谨且计算上可行的方式来描述这种不确定性。通常，不确定性源于模型参数，例如材料属性、边界条件或源项。

#### 参数化不确定性

最直接的方法是将不确定性归因于一个或多个[随机变量](@entry_id:195330)。假设一个PD[E模](@entry_id:160271)型依赖于一个参数向量 $\boldsymbol{\xi}(\omega) = (\xi_1(\omega), \dots, \xi_{d_{\xi}}(\omega))$，其中 $\omega$ 是底层[概率空间](@entry_id:201477) $(\Omega, \mathcal{F}, \mathbb{P})$ 中的一个事件。这里的 $\boldsymbol{\xi}$ 是一个有限维随机向量，其分量可以是独立的，也可以是相关的。例如，一个[扩散](@entry_id:141445)系数 $a$ 可以表示为参数的函数 $a(x, \omega) = \mathcal{A}(x, \boldsymbol{\xi}(\omega))$ 。

这种有限维[参数化](@entry_id:272587)是许多UQ方法的基础。当随机输入 $\xi_i$ 是相互独立的标准[高斯变量](@entry_id:276673)时（即 $\xi_i \sim \mathcal{N}(0,1)$），建模和计算会大大简化。然而，在许多实际应用中，输入变量是相关的。例如，它们可能服从一个[联合高斯](@entry_id:636452)[分布](@entry_id:182848) $\boldsymbol{\xi} \sim \mathcal{N}(\boldsymbol{0}, \Sigma)$，其中[协方差矩阵](@entry_id:139155) $\Sigma$ 不是单位阵。在这种情况下，直接使用以原始坐标 $\xi_i$ 构建的[张量积](@entry_id:140694)[基函数](@entry_id:170178)将不再具有正交性。一个标准的技术是通过[线性变换](@entry_id:149133)来解耦这些变量。由于 $\Sigma$ 是[对称正定](@entry_id:145886)的，我们可以找到一个矩阵 $L$（例如，通过[Cholesky分解](@entry_id:147066) $\Sigma = LL^\top$）使得变换后的向量 $\boldsymbol{\eta} = L^{-1}\boldsymbol{\xi}$ 的分量是独立的标准[高斯变量](@entry_id:276673)。然后，我们可以在新的 $\boldsymbol{\eta}$ [坐标系](@entry_id:156346)下构建正交基，从而恢复随机[伽辽金投影](@entry_id:145611)中的正交性 。

#### Karhunen-Loève 展开

当不确定性表现为空间变化的随机场（例如，非均匀材料中的[扩散](@entry_id:141445)系数 $a(x,\omega)$）时，我们需要一种更强大的表示方法。**Karhunen-Loève (KL) 展开** 为表示二阶[随机场](@entry_id:177952)提供了一种最优的谱分解方法。

考虑一个零均值随机场 $g(x,\omega)$（如果均值非零，我们可以通过减去均值 $\bar{g}(x) = \mathbb{E}[g(x,\cdot)]$ 来中心化）。其性质由[协方差核](@entry_id:266561) $C(x,y) = \mathbb{E}[g(x,\omega)g(y,\omega)]$ 完全确定。这个核函数定义了一个积分算子，即**协[方差](@entry_id:200758)算子** $T_C$:
$$
(T_C \varphi)(x) = \int_D C(x,y)\,\varphi(y)\,dy
$$
在有界域 $D$ 上，如果 $C(x,y)$ 是平方可积的，则 $T_C$ 是一个[Hilbert-Schmidt算子](@entry_id:271274)，因此是紧的。由于 $C(x,y)$ 的对称性和[半正定性](@entry_id:147720)，该算子是自伴且半正定的。根据[希尔伯特空间](@entry_id:261193)上的[紧自伴算子](@entry_id:147701)[谱理论](@entry_id:275351)，存在一列非负[特征值](@entry_id:154894) $\{\lambda_n\}_{n\ge 1}$（按降序[排列](@entry_id:136432)）和对应的 $L^2(D)$ 中标准正交的特征函数 $\{\phi_n(x)\}_{n\ge 1}$，满足特征问题  :
$$
\int_D C(x,y)\,\phi_n(y)\,dy = \lambda_n\,\phi_n(x)
$$
[KL展开](@entry_id:751050)将随机场 $g(x,\omega)$ 表示为这些[特征函数](@entry_id:186820)的[线性组合](@entry_id:154743)，其系数是随机的：
$$
g(x,\omega) = \sum_{n=1}^\infty \sqrt{\lambda_n}\,\phi_n(x)\,\xi_n(\omega)
$$
这里的[随机变量](@entry_id:195330) $\xi_n(\omega) = \frac{1}{\sqrt{\lambda_n}} \int_D g(x,\omega)\phi_n(x)dx$ 具有零均值和单位[方差](@entry_id:200758)，并且是**不相关**的，即 $\mathbb{E}[\xi_n \xi_m] = \delta_{nm}$。这是一个普适的性质。特别地，如果原始随机场 $g(x,\omega)$ 是一个高斯场，那么 $\xi_n$ 也是[联合高斯分布的](@entry_id:636452)，不相关性此时等价于**独立性**。因此，对于高斯场，[KL展开](@entry_id:751050)将其分解为一组确定性空间模式和一组独立的标准高斯[随机变量](@entry_id:195330) 。对于非高斯场，$\xi_n$ 虽然不相关，但可能仍然是相依的 。

[KL展开](@entry_id:751050)的一个关键优势是其**最优性**。在所有使用 $N$ 个[基函数](@entry_id:170178)进行的展开中，截断的[KL展开](@entry_id:751050)能够最小化均方截断误差。该误差恰好等于被忽略的[特征值](@entry_id:154894)之和 ：
$$
\mathbb{E}\left[\left\|g - \sum_{n=1}^N \sqrt{\lambda_n}\,\phi_n\,\xi_n\right\|_{L^2(D)}^2\right] = \sum_{n=N+1}^\infty \lambda_n
$$
这使得[KL展开](@entry_id:751050)成为[降维](@entry_id:142982)的理想工具：通过保留具有最大[特征值](@entry_id:154894)的模态，我们可以用少数几个[随机变量](@entry_id:195330) $\xi_n$ 来捕捉随机场的主要变异性。

在特殊情况下，例如当[协方差核](@entry_id:266561)是平移不变的（即 $C(x,y) = k(x-y)$）且域是周期性的时候，协[方差](@entry_id:200758)算子的特征函数就是傅里叶模态，而[特征值](@entry_id:154894)则是[核函数](@entry_id:145324) $k$ 的傅里叶系数 。

### 解的[谱表示](@entry_id:153219)：[广义多项式混沌](@entry_id:749788)

一旦我们将输入不确定性表示为由随机向量 $\boldsymbol{\xi}$ 驱动，我们就可以假设问题的解 $u(x, \boldsymbol{\xi})$ 同样依赖于这个向量。**[广义多项式混沌 (gPC)](@entry_id:749789)** 的思想是将解 $u(x, \boldsymbol{\xi})$ 展开为一组关于 $\boldsymbol{\xi}$ 的正交多项式基。

一个关键的原则是，多项式基的选择必须与 $\boldsymbol{\xi}$ 的概率测度相匹配，以确保正交性。这种对应关系被称为 **Wiener-Askey 方案**。具体而言，对于一个由概率密度函数 (PDF) $\rho(\xi)$ 定义的[随机变量](@entry_id:195330) $\xi$，我们寻找一个多项式族 $\{\Psi_k(\xi)\}$，使得它们在由 $\rho(\xi)$ 加权的[内积](@entry_id:158127)下是正交的：
$$
\mathbb{E}[\Psi_j \Psi_k] = \int \Psi_j(\xi) \Psi_k(\xi) \rho(\xi) d\xi = C_k \delta_{jk}
$$
这正是标准正交多项式的定义，其中权重函数就是[随机变量](@entry_id:195330)的PDF 。以下是一些重要的对应关系：

*   如果 $\xi$ 服从 **$[-1, 1]$ 上的[均匀分布](@entry_id:194597)**，其PDF为 $\rho(\xi) = 1/2$。对应的[正交多项式](@entry_id:146918)是**勒让德 (Legendre) 多项式**。
*   如果 $\xi$ 服从 **标准[高斯分布](@entry_id:154414) $\mathcal{N}(0,1)$**，其PDF为 $\rho(\xi) = (2\pi)^{-1/2}\exp(-\xi^2/2)$。对应的[正交多项式](@entry_id:146918)是**概率论者的埃尔米特 (Hermite) 多项式** $\mathrm{He}_k(\xi)$。
*   如果 $\xi$ 服从 **Gamma[分布](@entry_id:182848) $\mathrm{Gamma}(k, \theta)$**，其PDF为 $\rho(x) \propto x^{k-1}\exp(-x/\theta)$。对应的[正交多项式](@entry_id:146918)是通过变量代换 $y=x/\theta$ 得到的**广义拉盖尔 (Laguerre) 多项式** $L_n^{(k-1)}(x/\theta)$。

对于由 $d_{\xi}$ 个[独立随机变量](@entry_id:273896)组成的向量 $\boldsymbol{\xi}$，多维gPC基可以通过[张量积](@entry_id:140694)构造，即 $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{i=1}^{d_{\xi}} \Psi_{\alpha_i}(\xi_i)$，其中 $\boldsymbol{\alpha}$ 是一个多重指标。

于是，我们可以将随机解 $u(x, \boldsymbol{\xi})$ 近似地表示为一个截断的gPC展开：
$$
u(x, \boldsymbol{\xi}) \approx u_P(x, \boldsymbol{\xi}) = \sum_{|\boldsymbol{\alpha}| \le p} u_{\boldsymbol{\alpha}}(x) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})
$$
其中 $p$ 是多项式的最高总阶数，$u_{\boldsymbol{\alpha}}(x)$ 是确定性的空间依赖系数场。

这种表示法的美妙之处在于，它可以让我们方便地计算解的[统计矩](@entry_id:268545)。假设gPC基是标准正交的，即 $\mathbb{E}[\Psi_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\beta}}] = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$，并且[常数函数](@entry_id:152060)由 $\Psi_{\boldsymbol{0}}=1$ 表示。那么，解的**期望（均值）**就是零阶系数 ：
$$
\mathbb{E}[u(x, \boldsymbol{\xi})] = \mathbb{E}\left[\sum_{\boldsymbol{\alpha}} u_{\boldsymbol{\alpha}}(x) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})\right] = \sum_{\boldsymbol{\alpha}} u_{\boldsymbol{\alpha}}(x) \mathbb{E}[\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})] = u_{\boldsymbol{0}}(x)
$$
类似地，解的**[方差](@entry_id:200758)**可以由高阶系数的范数之和得到。例如，空间积分[方差](@entry_id:200758)为 ：
$$
\operatorname{Var}[u] = \mathbb{E}\left[ \|u - \mathbb{E}[u]\|_{L^2(D)}^2 \right] = \sum_{|\boldsymbol{\alpha}| > 0} \|u_{\boldsymbol{\alpha}}\|_{L^2(D)}^2
$$
这个性质表明，gPC展开不仅是一种近似，更是一种将随机解分解为均值和围绕均值的各阶脉动的[方差分解](@entry_id:272134)。

### 侵入式随机伽辽金方法

有了不确定性输入和解的[谱表示](@entry_id:153219)之后，接下来的问题是如何确定系数场 $u_{\boldsymbol{\alpha}}(x)$。**侵入式随机伽辽金方法**通过将gPC展开式代入原始PDE，并利用[伽辽金投影](@entry_id:145611)原理来实现这一目标。

考虑一个一般的随机PDE，例如[椭圆问题](@entry_id:146817) $-\nabla \cdot (a(x, \boldsymbol{\xi}) \nabla u) = f(x)$。我们将近似解 $u_P(x, \boldsymbol{\xi})$ 代入方程，得到一个残差。伽辽金方法要求该残差与gPC基中的每一个[基函数](@entry_id:170178) $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$（对于 $|\boldsymbol{\alpha}| \le p$）在期望意义下正交 ：
$$
\mathbb{E}\left[ \left( -\nabla \cdot (a(x, \boldsymbol{\xi}) \nabla u_P) - f(x) \right) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \right] = 0
$$
通过交换期望和[微分算子](@entry_id:140145)的顺序，并代入 $u_P$ 和 $a$ 的gPC展开，我们得到一个关于未知系数场 $\{u_{\boldsymbol{\beta}}(x)\}$ 的确定性PDE耦合系统。例如，对于上述[椭圆问题](@entry_id:146817)，该系统具有以下形式 ：
$$
-\sum_{|\boldsymbol{\beta}| \le p} \nabla \cdot \left( \widehat{a}_{\boldsymbol{\alpha}\boldsymbol{\beta}}(x) \nabla u_{\boldsymbol{\beta}}(x) \right) = f(x) \delta_{\boldsymbol{\alpha}\boldsymbol{0}}, \quad \forall \boldsymbol{\alpha} \text{ with } |\boldsymbol{\alpha}| \le p
$$
这里的耦合来自于**随机[耦合系数](@entry_id:273384)** $\widehat{a}_{\boldsymbol{\alpha}\boldsymbol{\beta}}(x) = \mathbb{E}[a(x, \boldsymbol{\xi}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})]$。这些系数本质上是gPC[基函数](@entry_id:170178)的[三重积](@entry_id:162942)积分，它们决定了不同随机模态 $u_{\boldsymbol{\beta}}$ 之间的相互作用。

如果[扩散](@entry_id:141445)系数 $a(x, \boldsymbol{\xi})$ 对参数 $\boldsymbol{\xi}$ 是仿射依赖的，例如 $a(x, \boldsymbol{\xi}) = a_0(x) + \sum_{k=1}^{d_{\xi}} a_k(x) \xi_k$，并且我们使用与标准[高斯变量](@entry_id:276673) $\xi_k$ 对应的[埃尔米特多项式](@entry_id:153594)基，那么[耦合系数](@entry_id:273384)具有[稀疏结构](@entry_id:755138)。利用[埃尔米特多项式](@entry_id:153594)的[三项递推关系](@entry_id:176845)，可以推导出 $\widehat{a}_{\boldsymbol{\alpha}\boldsymbol{\beta}}(x)$ 的精确表达式 ：
$$
\widehat{a}_{\boldsymbol{\alpha}\boldsymbol{\beta}}(x) = a_{0}(x)\,\delta_{\boldsymbol{\alpha}\boldsymbol{\beta}} + \sum_{k=1}^{d_{\xi}} a_{k}(x) \left( \sqrt{\alpha_k+1}\,\delta_{\boldsymbol{\beta}, \boldsymbol{\alpha}+e_k} + \sqrt{\alpha_k}\,\delta_{\boldsymbol{\beta}, \boldsymbol{\alpha}-e_k} \right)
$$
其中 $e_k$ 是第 $k$ 个方向上的单位多重指标。这个表达式表明，对于仿射依赖，第 $\boldsymbol{\alpha}$ 个方程仅与具有相邻多重指标的模态 $u_{\boldsymbol{\beta}}$ 耦合，这导致了一个稀疏的耦合结构。

### 全离散化：结合不[连续伽辽金方法](@entry_id:747805)

为了得到一个可计算的数值模型，我们还需要对上述耦合PDE系统进行[空间离散化](@entry_id:172158)。**[不连续伽辽金 (DG)](@entry_id:748482) 方法**由于其局部守恒性、对复杂几何和非结构网格的适应性以及对[hp-自适应](@entry_id:750398)的灵活性，是进行[空间离散化](@entry_id:172158)的一个有力工具。

#### 耦合[DG弱形式](@entry_id:748377)

我们首先为单个PDE（例如，[双曲守恒律](@entry_id:147752) $u_t + \nabla \cdot \boldsymbol{f}(u; \xi) = 0$）建立[DG弱形式](@entry_id:748377)。在每个网格单元 $K$上，我们将方程乘以一个检验函数 $v_h$，然后分部积分，并将边界上的物理通量替换为**数值通量** $\hat{\boldsymbol{f}}$ 。将此过程与随机[伽辽金投影](@entry_id:145611)相结合，我们得到一个全离散的弱形式，它必须对每个单元 $K$、每个空间[基函数](@entry_id:170178) $v_h$ 和每个随机[基函数](@entry_id:170178) $\Psi_{\ell}$ 都成立 ：
$$
\int_{K}\mathbb{E}\left[ u_{t} v_h \Psi_\ell \right] d\boldsymbol x - \int_{K}\mathbb{E}\left[ \boldsymbol f(u; \xi) \cdot \nabla v_h \Psi_\ell \right] d\boldsymbol x + \int_{\partial K}\mathbb{E}\left[ \hat{\boldsymbol f} \cdot \boldsymbol n_K v_h \Psi_\ell \right] ds = 0
$$

#### 最终的代数系统

将空间近似（例如，$u_{\boldsymbol{\alpha}}(x) = \sum_i (u_{\boldsymbol{\alpha},h})_i \phi_i(x)$，其中 $\{\phi_i\}$ 是DG空间[基函数](@entry_id:170178)）代入耦合PDE系统，最终会得到一个庞大的线性代数系统 $\mathcal{A} U = F$。理解这个全局矩阵 $\mathcal{A}$ 的结构至关重要。

我们可以将总的近似空间看作是空间DG空间 $V_h$ 和随机gPC空间 $S_p$ 的**[张量积](@entry_id:140694)空间** $V_h \otimes S_p$。该空间的维度是 $\dim(V_h \otimes S_p) = N_s \times N_{\xi}$，其中 $N_s$ 是空间自由度数量，而 $N_{\xi} = \binom{d_{\xi}+p}{p}$ 是随机自由度数量 。全局自由度向量 $U$ 可以通过一种系统的方式[排列](@entry_id:136432)，例如，以随机模态指标 $\boldsymbol{\alpha}$ 为慢变索引，空间指标 $i$ 为快变索引 。

全局算子 $\mathcal{A}$ 具有优雅的**Kronecker积**结构。对于仿射依赖的[扩散](@entry_id:141445)系数 $a(x, \boldsymbol{\xi}) = \sum_{m=0}^M a_m(x) \Psi_m(\boldsymbol{\xi})$，全局矩阵可以表示为 ：
$$
\mathcal{A} = \sum_{m=0}^{M} G_{m} \otimes K_{m}
$$
这里，$K_m$ 是与确定性空间场 $a_m(x)$ 相关的空间DG[刚度矩阵](@entry_id:178659)，其元素为 $(K_m)_{ij} = B_{a_m}(\phi_j, \phi_i)$。$G_m$ 是随机[耦合矩阵](@entry_id:191757)，其元素为 $(G_m)_{\boldsymbol{\alpha}\boldsymbol{\beta}} = \mathbb{E}[\Psi_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\beta}} \Psi_m]$。这种结构清晰地分离了空间和随机维度的贡献，对于设计高效的求解器（如利用张量结构）至关重要。

#### 理论保证：稳定性和收敛性

一个数值方法的可靠性取决于其稳定性和收敛性。对于随机伽辽金DG方法，要保证最终的代数系统是对称正定的，并且近似解能[均方收敛](@entry_id:137545)到真解，需要满足一系列充分条件 ：

1.  **随机PDE的[适定性](@entry_id:148590)**：首先，对于几乎每一个随机参数的实现 $\omega$，原始PDE必须是适定的。对于[椭圆问题](@entry_id:146817)，这要求[扩散](@entry_id:141445)系数 $a(x, \omega)$ 是一致有界和椭圆的，即存在确定性常数 $a_{\min}, a_{\max}$ 使得 $0  a_{\min} \le a(x, \omega) \le a_{\max}  \infty$ 几乎必然成立。在此条件下，[Lax-Milgram定理](@entry_id:137966)保证了[解的存在唯一性](@entry_id:177406)，并且解的能量范数是一致有界的，从而保证解属于Bochner空间 $L^2(\Omega; H_0^1(D))$ 。

2.  **[数值方法的稳定性](@entry_id:165924)**：上述[一致椭圆性](@entry_id:194714)和有界性条件也保证了随机[伽辽金算子](@entry_id:636484)的矫顽性和连续性，这对于方法的稳定性和收敛性至关重要。此外，DG方法中的罚参数必须足够大，以确保空间离散算子本身的[矫顽性](@entry_id:159399)，这个罚参数的大小通常依赖于 $a_{\max}$ 。

3.  **近似空间的属性**：为了保证收敛性，多项式基 $\{\Psi_{\boldsymbol{\alpha}}\}$ 必须在 $L^2(\Gamma, \rho)$ 空间中是稠密的。一个充分条件是，由 $\rho$ 定义的测度的所有矩都是有限的 。

### 非侵入式方法：随机配置

与需要修改[PDE求解器](@entry_id:753289)的侵入式方法相反，**非侵入式方法**将确定性求解器视为一个“黑箱”。**随机配置 (Stochastic Collocation)** 是其中最流行的一种。

其基本思想非常简单 ：
1.  在[参数空间](@entry_id:178581) $\Gamma$ 中选取一组**[配置点](@entry_id:169000)** $\{\boldsymbol{\xi}^{(j)}\}_{j=1}^M$。
2.  对每一个[配置点](@entry_id:169000) $\boldsymbol{\xi}^{(j)}$，独立地求解一次确定性PDE，得到解的样本 $u(x, \boldsymbol{\xi}^{(j)})$。
3.  利用这些解的样本，通过**多项式插值**或**伪[谱投影](@entry_id:265201)**（基于求积）来重构整个gPC展开 $u_P(x, \boldsymbol{\xi})$。

如果[配置点](@entry_id:169000)的数量 $M$ 等于gPC空间的维度 $N=|\mathcal{A}_p|$，并且这些点对于多项式空间 $\Pi_p$ 是**单值对应的 (unisolvent)**，那么存在唯一的插值多项式。这个插值过程对于本身就在 $\Pi_p$ 空间内的函数是精确的 。

非侵入式方法的主要优点是易于实现，因为它们可以复用现有的、高度优化的确定性求解器。每个[配置点](@entry_id:169000)的求解是完全解耦的，可以实现完美的[并行化](@entry_id:753104)。然而，对于某些问题，为了达到与侵入式方法相同的精度，可能需要更多的确定性求解次数。

特别地，当使用基于[高斯求积](@entry_id:146011)点的配置方案时，插值和伪[谱投影](@entry_id:265201)变得紧密相关。如果使用一个对最高 $2p$ 次多项式精确的求积法则，那么通过该求积计算的gPC系数对于任何次数不超过 $p$ 的函数都是精确的 。

总之，本章概述的原理和机制——从[KL展开](@entry_id:751050)对输入的[降维](@entry_id:142982)，到gPC对解的[谱表示](@entry_id:153219)，再到侵入式伽辽金和非侵入式配置方法的求解策略，以及与DG[空间离散化](@entry_id:172158)的结合——共同构成了一个强大而灵活的框架，用于在复杂的PDE模型中进行前向[不确定性传播](@entry_id:146574)分析。