## 引言
在科学与工程领域，从[电磁仿真](@entry_id:748890)到气候模型，不确定性无处不在。材料属性的微小变化、制造[公差](@entry_id:275018)或环境噪声都可能导致模型预测结果产生巨大偏差。量化这些不确定性的影响对于设计可靠、鲁棒的系统至关重要，但传统方法如蒙特卡洛模拟往往计算成本高昂，令人望而却步。

[多项式混沌](@entry_id:196964)展开 (Polynomial Chaos Expansions, PCE) 为应对这一挑战提供了一个高效且严谨的[谱方法](@entry_id:141737)框架。它并非制造混沌，而是将复杂的随机响应分解为一组确定性的[正交多项式](@entry_id:146918)[基函数](@entry_id:170178)之和，从而将一个随机问题转化为一个（或一系列）确定性问题来求解。这种方法不仅极大地提升了[计算效率](@entry_id:270255)，还为深入洞察模型行为提供了独特的视角。

本文将系统地引导您掌握PCE的核心思想与实践。在第一章 **“原理与机制”** 中，我们将深入探讨PCE的数学基础，从[函数空间](@entry_id:143478)理论到[正交基](@entry_id:264024)函数的构建，并介绍计算展开系数的关键方法。接下来的第二章 **“应用与跨学科连接”** 将通过计算电磁学、[多物理场耦合](@entry_id:171389)及数据科学等领域的丰富案例，展示PCE在解决实际问题中的强大威力。最后，在 **“动手实践”** 部分，您将通过编程练习来巩固所学知识，将理论转化为技能。

让我们首先进入第一章，揭示[多项式混沌](@entry_id:196964)展开背后的数学原理与精巧机制。

## 原理与机制

在对不确定性进行量化时，其核心挑战在于如何有效地描述和传播随机性。[多项式混沌](@entry_id:196964)展开 (Polynomial Chaos Expansions, PCE) 为此提供了一个强大而严谨的数学框架。它并非制造“混沌”，而是借鉴了 Norbert Wiener 在研究[随机过程](@entry_id:159502)（布朗运动）时所使用的数学思想，将看似无序的随机响应表示为一组有序的、具有确定性的正交多项式[基函数](@entry_id:170178)的谱展开。本章将深入探讨PCE的基本原理、构建机制及其在[计算电磁学](@entry_id:265339)等领域中的核心应用。

### [函数空间](@entry_id:143478)中的随机性表达

从根本上说，PCE 将一个依赖于随机输入 $\boldsymbol{\xi}$ 的模型输出量 $Y(\boldsymbol{\xi})$ 视为一个定义在概率空间上的函数。为了系统地分析这[类函数](@entry_id:146970)，我们首先需要确定一个合适的数学“舞台”。这个舞台就是[希尔伯特空间](@entry_id:261193) $L^2(\mu)$，它由所有关于概率测度 $\mu$ 平方可积的函数构成。一个函数 $Y$ 属于 $L^2(\mu)$ 空间，意味着其[方差](@entry_id:200758)是有限的，这对于大多数物理和工程问题中的“感兴趣量 (Quantity of Interest, QoI)” 都是一个自然而合理的假设。

在这个空间中，我们可以定义一个[内积](@entry_id:158127)，它为我们提供了衡量函数间“相似度”和进行“投影”操作的工具。对于任意两个函数 $f(\boldsymbol{\xi})$ 和 $g(\boldsymbol{\xi})$，其[内积](@entry_id:158127)定义为它们乘积的数学期望：

$$
\langle f, g \rangle = \mathbb{E}[f(\boldsymbol{\xi})g(\boldsymbol{\xi})] = \int f(\boldsymbol{\xi})g(\boldsymbol{\xi}) \, \mathrm{d}\mu(\boldsymbol{\xi})
$$

这个定义至关重要，因为它将概率论中的期望运算与泛函分析中的[内积](@entry_id:158127)概念联系在一起。正是这个[内积](@entry_id:158127)结构，使得我们能够将一个复杂的随机响应分解到一组更简单的[基函数](@entry_id:170178)上。

### [广义多项式混沌](@entry_id:749788)展开 (gPCE)

[广义多项式混沌](@entry_id:749788)展开 (gPCE) 的核心思想是，任何属于 $L^2(\mu)$ 空间的函数 $Y(\boldsymbol{\xi})$ 都可以表示为一组在该空间内正交的多项式[基函数](@entry_id:170178) $\Psi_{\alpha}(\boldsymbol{\xi})$ 的无穷级数。在实际计算中，我们通常采用一个截断的有限项和来近似 $Y(\boldsymbol{\xi})$：

$$
Y(\boldsymbol{\xi}) \approx \sum_{\alpha \in \mathcal{A}} c_{\alpha} \Psi_{\alpha}(\boldsymbol{\xi})
$$

其中，$\alpha$ 是一个多重指标 (multi-index)，$\mathcal{A}$ 是一个有限的多重[指标集](@entry_id:268489)合，而 $c_{\alpha}$ 则是展开系数。

这个展开式的基石是[基函数](@entry_id:170178) $\Psi_{\alpha}$ 的**正交性**。具体来说，我们要求这组多项式基是**标准正交 (orthonormal)** 的，即满足如下条件 ：

$$
\langle \Psi_{\alpha}, \Psi_{\beta} \rangle = \mathbb{E}[\Psi_{\alpha}(\boldsymbol{\xi})\Psi_{\beta}(\boldsymbol{\xi})] = \delta_{\alpha\beta}
$$

这里 $\delta_{\alpha\beta}$ 是克罗内克 δ 符号，当多重指标 $\alpha = \beta$ 时为1，否则为0。这个看似简单的性质是PCE所有强大功能的基础。它保证了展开系数 $c_{\alpha}$ 的唯一性，并且提供了一种直接的计算方法。为了求解特定系数 $c_{\beta}$，我们可以将展开式两边与[基函数](@entry_id:170178) $\Psi_{\beta}$ 作[内积](@entry_id:158127)：

$$
\langle Y, \Psi_{\beta} \rangle = \left\langle \sum_{\alpha \in \mathcal{A}} c_{\alpha} \Psi_{\alpha}, \Psi_{\beta} \right\rangle = \sum_{\alpha \in \mathcal{A}} c_{\alpha} \langle \Psi_{\alpha}, \Psi_{\beta} \rangle = \sum_{\alpha \in \mathcal{A}} c_{\alpha} \delta_{\alpha\beta} = c_{\beta}
$$

因此，每个系数都是原始函数 $Y$ 在相应[基函数](@entry_id:170178)上的正交投影：

$$
c_{\alpha} = \langle Y, \Psi_{\alpha} \rangle = \mathbb{E}[Y(\boldsymbol{\xi})\Psi_{\alpha}(\boldsymbol{\xi})]
$$

按照惯例，零阶多项式[基函数](@entry_id:170178) $\Psi_{\mathbf{0}}$ 是一个常数。为了满足[归一化条件](@entry_id:156486) $\langle \Psi_{\mathbf{0}}, \Psi_{\mathbf{0}} \rangle = 1$，我们取 $\Psi_{\mathbf{0}}(\boldsymbol{\xi}) \equiv 1$。因此，所有[高阶基函数](@entry_id:165641)（$\alpha \neq \mathbf{0}$）都必须与 $\Psi_{\mathbf{0}}$ 正交，这意味着它们的均值为零：$\mathbb{E}[\Psi_{\alpha}] = \langle \Psi_{\alpha}, 1 \rangle = \langle \Psi_{\alpha}, \Psi_{\mathbf{0}} \rangle = 0$。

### 选择合适的[基函数](@entry_id:170178)：Wiener-Askey 框架

PCE 的“广义”之处在于，它不局限于某一特定的多项式族，而是根据输入[随机变量](@entry_id:195330) $\boldsymbol{\xi}$ 的[概率分布](@entry_id:146404)来“量身定制”正交基函数。这种对应关系被称为 **Wiener-Askey 框架**。其基本原则是：选择的多项式族必须在由输入变量的概率密度函数 (PDF) 定义的[加权内积](@entry_id:163877)下是正交的。

换言之，如果输入变量 $\xi$ 的 PDF 是 $w(\xi)$，那么相应的多项式族 $\{P_n(\xi)\}$ 必须满足正交性关系：
$$
\int P_m(\xi) P_n(\xi) w(\xi) \,d\xi = 0, \quad m \neq n
$$
这恰好与我们定义的[内积](@entry_id:158127) $\langle f,g \rangle = \int fg \, w(\xi)d\xi$ 相吻合。下表总结了一些经典连续分布及其对应的正交多项式族：

| [分布](@entry_id:182848) (Distribution) | 支撑集 (Support) | 权重函数 $w(\xi)$ (PDF) | [正交多项式](@entry_id:146918) (Orthogonal Polynomials) |
|---|---|---|---|
| 高斯 (Gaussian) | $(-\infty, \infty)$ | $\frac{1}{\sqrt{2\pi}} \exp(-\xi^2/2)$ | Hermite |
| 均匀 (Uniform) | $[-1, 1]$ | $1/2$ | Legendre |
| Gamma | $[0, \infty)$ | $\frac{\xi^{a-1}\exp(-\xi)}{\Gamma(a)}$ | Laguerre |
| Beta | $[-1, 1]$ | $(1-\xi)^a (1+\xi)^b$ | Jacobi |

例如，在一个耦合的[多物理场仿真](@entry_id:145294)中，若模型的不确定性来自一个服从标准正态分布 $\mathcal{N}(0,1)$ 的[杨氏模量](@entry_id:140430)和一个服从 $[-1,1]$ 上标准[均匀分布](@entry_id:194597)的无量纲[耦合参数](@entry_id:747983)，那么构建PCE[基函数](@entry_id:170178)时，我们应分别选用 Hermite 多项式和 Legendre 多项式 。

### 处理高维问题：[张量积](@entry_id:140694)与截断

实际问题中的不确定性往往来源于多个独立的随机源，甚至来源于随机场。

#### 从[随机场](@entry_id:177952)到[随机变量](@entry_id:195330)：Karhunen-Loève 展开

当不确定性输入是一个随机场（例如，空间上变化的随机[介电常数](@entry_id:146714) $\epsilon(\mathbf{r}, \omega)$）时，其自由度是无限的。为了应用PCE，我们首先需要将其[降维](@entry_id:142982)为一组可数的、不相关的[随机变量](@entry_id:195330)。**Karhunen-Loève (K-L) 展开** 正是实现这一目标的关键工具 。它将一个二阶[随机场](@entry_id:177952)表示为其均值场与一系列空间模态函数的[线性组合](@entry_id:154743)，其系数是一组标准正交的[随机变量](@entry_id:195330) $\{\xi_n\}$。具体来说，给定[随机场](@entry_id:177952)的[协方差函数](@entry_id:265031) $C(\mathbf{r}, \mathbf{r}')$，通过求解如下的 Fredholm 积分[特征值问题](@entry_id:142153)：
$$
\int_D C(\mathbf{r}, \mathbf{r}') \phi_n(\mathbf{r}') \, \mathrm{d}\mathbf{r}' = \lambda_n \phi_n(\mathbf{r})
$$
可以得到一组正交的空间模态 $\phi_n(\mathbf{r})$ 和相应的[特征值](@entry_id:154894) $\lambda_n$。随机场 $\epsilon(\mathbf{r}, \omega)$ 即可展开为：
$$
\epsilon(\mathbf{r}, \omega) = m(\mathbf{r}) + \sum_{n=1}^\infty \sqrt{\lambda_n} \phi_n(\mathbf{r}) \xi_n(\omega)
$$
其中 $m(\mathbf{r})$ 是均值场，$\{\xi_n\}$ 是通过对随机场投影得到的一组不相关、零均值、单位[方差](@entry_id:200758)的[随机变量](@entry_id:195330)。这样，一个无限维的随机场输入就被转化为了一个由可数个标准[随机变量](@entry_id:195330)构成的向量 $\boldsymbol{\xi} = (\xi_1, \xi_2, \dots)$，为后续的PCE处理铺平了道路。

#### [张量积](@entry_id:140694)[基函数](@entry_id:170178)

当输入向量 $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$ 的各分量[相互独立](@entry_id:273670)时，高维PCE[基函数](@entry_id:170178)可以通过一维正交多项式的**[张量积](@entry_id:140694)**构造得到。设与 $\xi_i$ 对应的标准正交多项式族为 $\{\psi_{\alpha_i}^{(i)}\}$，则高维[基函数](@entry_id:170178) $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$ 定义为：

$$
\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{i=1}^d \psi_{\alpha_i}^{(i)}(\xi_i)
$$

由于各分量独立，高维[内积](@entry_id:158127)可以分解为一维[内积](@entry_id:158127)的乘积，从而可以证明，由标准正交的一维[基函数](@entry_id:170178)通过[张量积](@entry_id:140694)构造出的高维[基函数](@entry_id:170178)系仍然是标准正交的 。

#### [维度灾难](@entry_id:143920)与截断策略

即使输入维度 $d$ 是有限的，多项式[基函数](@entry_id:170178)的数量也会随着多项式阶数 $p$ 的增加而迅速增长，这就是所谓的“维度灾难”。因此，必须对无限的PCE级数进行截断，只保留一个有限的多重[指标集](@entry_id:268489) $\mathcal{A}_p$。常见的截断策略包括：

*   **总阶数 (Total-Degree, TD) 截断**: 该策略保留所有总阶数不超过 $p$ 的多项式。总阶数定义为多重指标各分量之和。[指标集](@entry_id:268489)为：
    $$
    \mathcal{A}_p^{\mathrm{TD}} = \left\{ \boldsymbol{\alpha} \in \mathbb{N}_0^d : \sum_{j=1}^d \alpha_j \le p \right\}
    $$
    其[基函数](@entry_id:170178)数量（即展开式中的项数）为 $M = \binom{d+p}{p}$  。

*   **[张量积](@entry_id:140694) (Tensor-Product, TP) 截断**: 也称为全张量截断 (Full Tensor)，它要求每个维度上的多项式阶数都不超过 $p$。[指标集](@entry_id:268489)为：
    $$
    \mathcal{A}_p^{\mathrm{TP}} = \left\{ \boldsymbol{\alpha} \in \mathbb{N}_0^d : \max_{1 \le j \le d} \alpha_j \le p \right\}
    $$
    其[基函数](@entry_id:170178)数量为 $M = (p+1)^d$ 。这个数字在维度 $d$ 较高时会爆炸式增长。

*   **双曲交叉 (Hyperbolic-Cross, HC) 截断**: 许多物理问题中，高阶交互项（即多个变量同时处于高阶多项式中的项）的贡献往往较小。双曲[交叉](@entry_id:147634)截断正是利用这一先验知识，优先保留低阶交互项和单个变量的高阶项。一个常见的定义是  ：
    $$
    \mathcal{A}_p^{\mathrm{HC}} = \left\{ \boldsymbol{\alpha} \in \mathbb{N}_0^d : \prod_{j=1}^d (\alpha_j + 1) \le p+1 \right\}
    $$
    相比于总阶数截断，双曲交叉截断显著减少了[基函数](@entry_id:170178)的数量，尤其是在高维情况下，从而在一定程度上缓解了[维度灾难](@entry_id:143920)。

### 计算PCE系数：侵入式与非侵入式方法

确定了[基函数](@entry_id:170178)和截断集后，下一个核心任务是计算展开系数 $c_{\alpha}$。主要有两种途径：侵入式方法和非侵入式方法。

#### 侵入式方法：随机[伽辽金投影](@entry_id:145611)

侵入式方法需要修改原有的确定性求解器。其核心思想是将待求物理量（如[电场](@entry_id:194326) $\mathbf{E}(\mathbf{x}, \boldsymbol{\xi})$）的PCE形式直接代入到控制方程（如麦克斯韦方程的[变分形式](@entry_id:166033)）中 。

$$
\mathbf{E}(\mathbf{x}, \boldsymbol{\xi}) \approx \sum_{\alpha \in \mathcal{A}} \mathbf{E}_{\alpha}(\mathbf{x}) \Psi_{\alpha}(\boldsymbol{\xi})
$$

然后，利用**[伽辽金投影](@entry_id:145611)**，要求方程的残差与随机空间中的每一个[基函数](@entry_id:170178) $\Psi_{\beta}$ 正交。由于基[函数的正交性](@entry_id:160337)，对[随机变量](@entry_id:195330)的积分（即求期望）可以预先计算，得到一系列确定的[耦合系数](@entry_id:273384)（例如，三阶张量 $C_{\gamma\alpha\beta} = \mathbb{E}[\Psi_{\gamma}\Psi_{\alpha}\Psi_{\beta}]$）。这个过程将一个[随机偏微分方程](@entry_id:188292)转化为了一个针对所有未知系数场 $\mathbf{E}_{\alpha}(\mathbf{x})$ 的、规模更大的确定性耦合[方程组](@entry_id:193238)。这种方法虽然在数学上非常优雅且通常能达到很高的精度，但需要重写大量的求解器代码，实现过程非常复杂。

#### 非侵入式方法：与黑箱求解器协作

非侵入式方法将确定性求解器视为一个“黑箱”，只需通过多次调用求解器获取模型在不同随机输入样本点上的输出即可，无需修改其内部代码。

*   **基于正交投影的求积方法**:
    这种方法直接利用系数的积分表达式 $c_{\alpha} = \mathbb{E}[Y(\boldsymbol{\xi})\Psi_{\alpha}(\boldsymbol{\xi})]$，并通过数值积分（求积）来近似这个[期望值](@entry_id:153208) 。一个 $d$ 维的张量积[高斯求积法](@entry_id:146011)则可以表示为：
    $$
    c_{\alpha} \approx \sum_{j_1=1}^{N_1} \dots \sum_{j_d=1}^{N_d} W_{\boldsymbol{j}} Y(\boldsymbol{\xi}_{\boldsymbol{j}}) \Psi_{\alpha}(\boldsymbol{\xi}_{\boldsymbol{j}})
    $$
    其中 $\boldsymbol{\xi}_{\boldsymbol{j}}$ 是求积节点， $W_{\boldsymbol{j}}$ 是对应的权重。[高斯求积](@entry_id:146011)的优点在于其高效性：一个 $N$ 点的[高斯求积法](@entry_id:146011)则对于最高 $2N-1$ 阶的多项式是精确的。因此，我们可以通过分析被积函数 $Y(\boldsymbol{\xi})\Psi_{\alpha}(\boldsymbol{\xi})$ 的多项式阶数来确定保证积分精确性所需的最小求积点数 。例如，要精确计算 $Y(\xi)=\xi^3$ 对应的三阶勒让德多项式展开系数 $c_3$，被积函数的阶数为 $3+3=6$。我们需要 $2N-1 \ge 6$，即 $N \ge 3.5$，所以至少需要4个[高斯-勒让德求积](@entry_id:138201)点。然而，[张量积求积](@entry_id:145940)方法的总样本点数会随维度 $d$ 指数增长（$N_{total} = N^d$），这使其在高维问题中变得不切实际。

*   **基于回归的最小二乘法**:
    回归方法将系数求解问题转化为一个线性拟合问题。我们首先生成一组随机样本点 $\{\boldsymbol{\xi}^{(n)}\}_{n=1}^N$，并运行确定性求解器得到相应的输出 $\{y_n = Y(\boldsymbol{\xi}^{(n)})\}_{n=1}^N$。然后，我们寻找一组系数 $\mathbf{c} = \{c_{\alpha}\}$，使得PCE在这些样本点上的预测值与真实输出值的均方误差最小 ：
    $$
    \min_{\mathbf{c}} \sum_{n=1}^N \left( y_n - \sum_{\alpha \in \mathcal{A}} c_{\alpha} \Psi_{\alpha}(\boldsymbol{\xi}^{(n)}) \right)^2
    $$
    这是一个标准的线性[最小二乘问题](@entry_id:164198) $\min_{\mathbf{c}} \|\boldsymbol{\Psi}\mathbf{c} - \mathbf{y}\|_2^2$，其中 $\boldsymbol{\Psi}$ 是[设计矩阵](@entry_id:165826)，其元素为 $\Psi_{n\alpha} = \Psi_{\alpha}(\boldsymbol{\xi}^{(n)})$。为了得到一个稳定唯一的解，样本数量 $N$ 必须至少等于未知系数的数量 $M=|\mathcal{A}|$，通常推荐使用[过采样](@entry_id:270705)（如 $N \ge 2M$）。与[张量积求积](@entry_id:145940)相比，[最小二乘法](@entry_id:137100)的样本数量仅需与PCE[基函数](@entry_id:170178)的数量 $M$（例如，对于TD截断是 $\binom{d+p}{p}$）成正比。由于 $M$ 随维度 $d$ 的增长远慢于 $(p+1)^d$，因此基于回归的方法能够极大地缓解维度灾难，在高维问题中更具优势。

### PCE的威力：高效的[不确定性量化](@entry_id:138597)后处理

一旦获得了PCE系数 $\{c_{\alpha}\}$，我们就拥有了一个原始复杂模型的廉价代理模型。利用这个代理模型，各种不确定性量化分析变得异常简单和高效。

#### [统计矩](@entry_id:268545)的即时计算

由于PCE基[函数的正交性](@entry_id:160337)，模型输出的[统计矩](@entry_id:268545)可以直接从展开系数中解析地得到 ：

*   **均值**: 模型的均值就是零阶系数本身。
    $$
    \mu_Y = \mathbb{E}[Y] = \mathbb{E}\left[\sum_{\alpha} c_{\alpha} \Psi_{\alpha}\right] = c_{\mathbf{0}} \mathbb{E}[\Psi_{\mathbf{0}}] = c_{\mathbf{0}}
    $$

*   **[方差](@entry_id:200758)**: 模型的[方差](@entry_id:200758)是所有非零阶系数的平方和。这本质上是[随机变量](@entry_id:195330)空间中的帕萨瓦尔定理 (Parseval's identity)。
    $$
    \sigma_Y^2 = \mathrm{Var}[Y] = \mathbb{E}[(Y - \mu_Y)^2] = \mathbb{E}\left[\left(\sum_{\alpha \neq \mathbf{0}} c_{\alpha} \Psi_{\alpha}\right)^2\right] = \sum_{\alpha \neq \mathbf{0}} c_{\alpha}^2
    $$

#### [全局敏感性分析](@entry_id:171355) (Sobol 指数)

更进一步，PCE的加性[方差分解](@entry_id:272134)结构为[全局敏感性分析](@entry_id:171355)提供了直接的途径。总[方差](@entry_id:200758)可以被精确地分解为来自单个输入变量的贡献（主效应）以及变量之间[交互作用](@entry_id:176776)的贡献。

**Sobol 指数**是衡量输入变量对输出[方差](@entry_id:200758)贡献的常用指标。利用PCE系数，它们可以被轻易计算出来 。一个多重指标 $\boldsymbol{\alpha}$ 的支撑集 $\mathrm{supp}(\boldsymbol{\alpha})$ 定义为所有使得 $\alpha_i > 0$ 的维度 $i$ 的集合。

*   **一阶 Sobol 指数 ($S_i$)**: 量化了输入变量 $\xi_i$ 的主效应（不考虑其与其他变量的交互）对总[方差](@entry_id:200758)的贡献。它等于所有只依赖于 $\xi_i$ 的[基函数](@entry_id:170178)项所贡献的[方差](@entry_id:200758)之和，再除以总[方差](@entry_id:200758)。
    $$
    S_i = \frac{\sum_{\alpha : \mathrm{supp}(\alpha)=\{i\}} c_{\alpha}^2}{\sigma_Y^2}
    $$

*   **总阶 Sobol 指数 ($S_{T_i}$)**: 量化了与输入变量 $\xi_i$ 相关的所有效应（包括其主效应和所有阶的交互效应）对总[方差](@entry_id:200758)的总贡献。它等于所有依赖于 $\xi_i$ 的[基函数](@entry_id:170178)项所贡献的[方差](@entry_id:200758)之和，再除以总[方差](@entry_id:200758)。
    $$
    S_{T_i} = \frac{\sum_{\alpha : i \in \mathrm{supp}(\alpha)} c_{\alpha}^2}{\sigma_Y^2}
    $$

这种通过简单代数运算即可获得全局敏感性指数的能力，是PCE作为不确定性量化工具的一个核心优势。

### 收敛性理论：PCE为何如此高效？

PCE之所以成为一种强大的方法，一个关键原因在于其优异的收敛性质，即**谱收敛 (spectral convergence)**。这意味着当被展开的函数 $Y(\boldsymbol{\xi})$ 足够光滑时，PCE的[截断误差](@entry_id:140949)会随着多项式阶数 $p$ 的增加而以指数速率下降，即误差衰减速度快于任何 $p$ 的多项式次幂（如 $O(p^{-k})$）。

[收敛速度](@entry_id:636873)的理论保证来源于一个深刻的数学结论：如果函数 $Y(\boldsymbol{\xi})$ 作为其参数 $\boldsymbol{\xi}$ 的函数，能够在包含[随机变量](@entry_id:195330)支撑集的复数域的一个区域内进行[解析延拓](@entry_id:147225)，那么其PCE将表现出谱收敛 。

对于由[偏微分方程](@entry_id:141332)（如麦克斯韦方程）定义的模型，这意味着：
1.  方程的系数（如[介电常数](@entry_id:146714) $\epsilon(\boldsymbol{\xi})$）必须是随机参数 $\boldsymbol{\xi}$ 的解析函数。
2.  控制方程的算子在参数的复数邻域内必须保持良定（例如，一致可逆，不出现共振）。

例如，在[电磁仿真](@entry_id:748890)中，如果[介电常数](@entry_id:146714) $\epsilon$ 对 $\boldsymbol{\xi}$ 解析，并且介质本身是有耗的（这能保证算子的一致可逆性），那么PCE就能实现谱收敛。同样，对于无耗介质，只要工作频率能一致地避开所有参数下的本征频率（共振点），也能保证谱收敛 。

反之，如果函数 $Y(\boldsymbol{\xi})$ 的光滑性较差，例如，当[介电常数](@entry_id:146714)是参数 $\boldsymbol{\xi}$ 的一个阶跃函数时，函数在[参数空间](@entry_id:178581)中存在[不连续性](@entry_id:144108)，此时PCE的[收敛速度](@entry_id:636873)将退化为缓慢的代数收敛，并可能出现吉布斯现象。因此，PCE的有效性与其所模拟的物理问题对不确定性参数的依赖关系的光滑程度紧密相关。