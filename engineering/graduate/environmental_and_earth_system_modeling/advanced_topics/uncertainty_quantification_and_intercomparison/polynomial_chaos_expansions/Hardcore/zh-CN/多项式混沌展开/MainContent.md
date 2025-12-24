## 引言
在环境与地球[系统建模](@entry_id:197208)等众多科学与工程领域，准确量化模型预测的不确定性至关重要。传统方法如[蒙特卡洛模拟](@entry_id:193493)虽然通用，但在面对计算成本高昂的模型时往往效率低下。多项式混沌展开（Polynomial Chaos Expansions, PCE）作为一种先进的[谱方法](@entry_id:141737)，为这一挑战提供了强大而优雅的解决方案。它不仅能够高效地传播输入参数的不确定性，还能深入揭示不确定性的来源，并构建可被即时评估的代理模型，从而解决了传统方法在效率和深度分析上的知识缺口。本文旨在系统性地介绍PCE的理论与实践。在“原理与机制”一章中，我们将深入其数学核心，学习如何构建PCE并利用其进行不确定性量化。随后，在“应用与跨学科连接”中，我们将探索PCE在[灵敏度分析](@entry_id:147555)、代理建模、优化等任务中的广泛应用，并揭示其与降维、[降阶建模](@entry_id:177038)等前沿技术的联系。最后，“实践练习”部分将通过具体问题，帮助您巩固所学知识，将理论应用于实践。

## 原理与机制

本章旨在深入探讨[多项式混沌](@entry_id:196964)展开（Polynomial Chaos Expansions, PCE）的基本原理与核心机制。我们将从其数学基础出发，系统地阐述如何构建并应用PCE进行不确定性量化，并讨论其在面对高维、输入相关性和非光滑响应等复杂问题时的收敛特性、挑战与高级对策。

### 希尔伯特空间视角下的多项式混沌

在最根本的层面上，[广义多项式混沌](@entry_id:749788)展开是一种将[随机系统](@entry_id:187663)响应在特定函数空间中进行[谱表示](@entry_id:153219)的方法。理解这一视角是掌握PCE精髓的关键。

**将模型响应视为[随机变量](@entry_id:195330)**

考虑一个由随机输入向量 $\boldsymbol{\xi} \in \mathbb{R}^d$ 驱动的数学或[计算模型](@entry_id:637456)。其标量输出，我们记为 $Y(\boldsymbol{\xi})$，本身就是一个[随机变量](@entry_id:195330)。为了对 $Y$ 的不确定性进行分析，我们需要一个能够系统地描述其统计特性的数学框架。PCE正是提供了这样一种框架，它将 $Y(\boldsymbol{\xi})$ 表达为一系列关于输入[随机变量](@entry_id:195330) $\boldsymbol{\xi}$ 的[正交多项式](@entry_id:146918)的加权和。

**$L^2$ 空间与[内积](@entry_id:750660)**

PCE理论的数学舞台是**希尔伯特空间** $L^2(\Omega, \mathcal{F}, \mathbb{P}_\xi)$，它由所有关于[概率测度](@entry_id:190821) $\mathbb{P}_\xi$ **平方可积**的[随机变量](@entry_id:195330)构成。这意味着对于空间中的任何一个元素 $Y$，其二阶矩都是有限的，即 $\mathbb{E}[Y(\boldsymbol{\xi})^2]  \infty$ 。

在这个空间中，两个[随机变量](@entry_id:195330) $f(\boldsymbol{\xi})$ 和 $g(\boldsymbol{\xi})$ 的**[内积](@entry_id:750660)**被定义为它们[乘积的期望值](@entry_id:201037)：
$$
\langle f, g \rangle = \mathbb{E}[f(\boldsymbol{\xi})g(\boldsymbol{\xi})]
$$
如果输入变量 $\boldsymbol{\xi}$ 具有[联合概率密度函数](@entry_id:267139)（PDF）$\rho(\boldsymbol{\xi})$，那么这个[内积](@entry_id:750660)可以写成一个加权积分的形式：
$$
\langle f, g \rangle = \int_{\mathcal{S}_\xi} f(\boldsymbol{\xi})g(\boldsymbol{\xi})\rho(\boldsymbol{\xi}) d\boldsymbol{\xi}
$$
其中 $\mathcal{S}_\xi$ 是 $\boldsymbol{\xi}$ 的支撑集 。这个[内积](@entry_id:750660)结构赋予了 $L^2$ 空间几何特性，使得我们可以讨论诸如正交性、投影和收敛等概念。

**[广义多项式混沌](@entry_id:749788)展开 (gPC)**

有了[希尔伯特空间](@entry_id:261193)的框架，PCE的定义就变得非常清晰。假设我们有一组多元多项式基函数 $\{ \Psi_\alpha(\boldsymbol{\xi}) \}_{\alpha \in \mathbb{N}_0^d}$，它们构成了 $L^2$ 空间的一个**完全正交规范基**（Complete Orthonormal Basis, CONB）。这意味着这组基函数不仅是完备的（即它们的[线性组合](@entry_id:154743)可以逼近空间中的任何元素），而且满足**正交规范性条件**：
$$
\langle \Psi_\alpha, \Psi_\beta \rangle = \mathbb{E}[\Psi_\alpha(\boldsymbol{\xi})\Psi_\beta(\boldsymbol{\xi})] = \delta_{\alpha\beta}
$$
其中 $\delta_{\alpha\beta}$ 是克罗内克（Kronecker）符号 。

根据希尔伯特空间的基本理论，任何平方可积的响应 $Y(\boldsymbol{\xi})$ 都可以唯一地展开为这组基函数的[无穷级数](@entry_id:143366)，这便是[广义多项式混沌](@entry_id:749788)展开 ：
$$
Y(\boldsymbol{\xi}) = \sum_{\alpha \in \mathbb{N}_0^d} c_\alpha \Psi_\alpha(\boldsymbol{\xi})
$$
这里的 $c_\alpha$ 是展开系数，$\alpha$ 是一个多指标（multi-index）。

**[均方收敛](@entry_id:137545)性**

上述[无穷级数的收敛](@entry_id:157904)性是在 $L^2$ 空间的范数意义下定义的，即**[均方收敛](@entry_id:137545)**（mean-square convergence）。这意味着，如果我们用一个有限项的截断和 $Y_p(\boldsymbol{\xi}) = \sum_{|\alpha| \le p} c_\alpha \Psi_\alpha(\boldsymbol{\xi})$ 来近似 $Y(\boldsymbol{\xi})$，那么当截断阶数 $p \to \infty$ 时，近似误差的平方的[期望值](@entry_id:150961)将趋于零 ：
$$
\lim_{p \to \infty} \mathbb{E}\left[ \left( Y(\boldsymbol{\xi}) - \sum_{|\alpha| \le p} c_\alpha \Psi_\alpha(\boldsymbol{\xi}) \right)^2 \right] = 0
$$
这种[收敛模式](@entry_id:189917)是PCE理论的基石，它保证了在统计意义上，我们的多项式近似会越来越接近真实的模型响应。

### 构建PCE的关键要素

要实际构建一个PCE，我们需要确定两个关键要素：合适的正交多项式基，以及计算相应展开系数的方法。

#### 正交多项式基

PCE的核心在于“正交性”。选择与输入[随机变量](@entry_id:195330)的概率分布相匹配的[正交多项式](@entry_id:146918)基至关重要。

**Askey-Wiener 族**

幸运的是，对于许多常见的概率分布，相应的[正交多项式](@entry_id:146918)族是已知的。这些关系构成了所谓的**Askey-Wiener族**。例如：
-   如果输入 $\xi$ 是一个**标准正态**[随机变量](@entry_id:195330)（$\xi \sim \mathcal{N}(0,1)$），则对应的正交多项式是**[Hermite多项式](@entry_id:153594)** 。
-   如果输入 $\xi$ 是一个在 $[-1,1]$ 上的**均匀**[随机变量](@entry_id:195330)（$\xi \sim \mathcal{U}[-1,1]$），则对应的[正交多项式](@entry_id:146918)是**[Legendre多项式](@entry_id:141510)** 。
-   其他分布，如Gamma、Beta和[泊松分布](@entry_id:147769)，也分别对应着Laguerre、Jacobi和[Charlier多项式](@entry_id:183055)。

当模型有多个**独立**的随机输入 $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$ 时，多元[正交基](@entry_id:264024)函数 $\Psi_\alpha(\boldsymbol{\xi})$ 通常可以通过相应的一元正交多项式 $\psi_{\alpha_k}(\xi_k)$ 的[张量积](@entry_id:140694)来构建：
$$
\Psi_\alpha(\boldsymbol{\xi}) = \prod_{k=1}^d \psi_{\alpha_k}(\xi_k)
$$

#### 计算展开系数

一旦确定了[正交基](@entry_id:264024) $\{ \Psi_\alpha \}$，展开系数 $c_\alpha$ 就可以通过将模型响应 $Y$ **[正交投影](@entry_id:144168)**到每个基函数 $\Psi_\alpha$ 上来计算。利用基的正交规范性，我们可以推导出系数的计算公式 ：
$$
\langle Y, \Psi_\alpha \rangle = \left\langle \sum_{\beta} c_\beta \Psi_\beta, \Psi_\alpha \right\rangle = \sum_{\beta} c_\beta \langle \Psi_\beta, \Psi_\alpha \rangle = \sum_{\beta} c_\beta \delta_{\beta\alpha} = c_\alpha
$$
因此，系数由以下[内积](@entry_id:750660)给出：
$$
c_\alpha = \langle Y, \Psi_\alpha \rangle = \mathbb{E}[Y(\boldsymbol{\xi})\Psi_\alpha(\boldsymbol{\xi})] = \int_{\mathcal{S}_\xi} Y(\boldsymbol{\xi})\Psi_\alpha(\boldsymbol{\xi})\rho(\boldsymbol{\xi}) d\boldsymbol{\xi}
$$
这个积分通常通过数值方法（如[高斯求积法](@entry_id:146011)）进行计算，这构成了[非侵入式PCE](@entry_id:638059)方法的基础。

**示例：一阶PCE的构建**

让我们通过一个具体的例子来演示这个过程 。考虑一个简化的集水区径流模型 $Q(\xi) = \frac{1}{1+\alpha\xi}$，其中不确定性输入 $\xi$ 是一个服从 $\mathcal{U}[-1,1]$ 分布的[随机变量](@entry_id:195330)。我们的任务是构建其一阶PCE。

1.  **选择基函数**：由于输入是均匀分布，我们选择[Legendre多项式](@entry_id:141510)。其概率密度函数为 $\rho(x) = \frac{1}{2}$ 对于 $x \in [-1,1]$。我们需要构建在此[概率测度](@entry_id:190821)下正交规范的基。标准Legendre多项式 $P_n(x)$ 满足 $\int_{-1}^1 P_n(x)P_m(x)dx = \frac{2}{2n+1}\delta_{nm}$。我们的[内积](@entry_id:750660)是 $\mathbb{E}[fg] = \frac{1}{2}\int_{-1}^1 f(x)g(x)dx$。因此，正交规范的基 $\psi_n(x)$ 与 $P_n(x)$ 的关系是 $\psi_n(x) = \sqrt{2n+1}P_n(x)$。对于一阶展开，我们需要：
    *   $\psi_0(x) = \sqrt{1}P_0(x) = 1$
    *   $\psi_1(x) = \sqrt{3}P_1(x) = \sqrt{3}x$

2.  **计算系数**：我们使用[投影公式](@entry_id:152164)计算 $c_0$ 和 $c_1$。
    *   **计算 $c_0$**：
        $$
        c_0 = \mathbb{E}[Q(\xi)\psi_0(\xi)] = \mathbb{E}\left[\frac{1}{1+\alpha\xi}\right] = \int_{-1}^{1} \frac{1}{1+\alpha x} \cdot \frac{1}{2} dx = \frac{1}{2\alpha} \ln\left(\frac{1+\alpha}{1-\alpha}\right)
        $$
    *   **计算 $c_1$**：
        $$
        c_1 = \mathbb{E}[Q(\xi)\psi_1(\xi)] = \mathbb{E}\left[\frac{\sqrt{3}\xi}{1+\alpha\xi}\right] = \frac{\sqrt{3}}{2} \int_{-1}^{1} \frac{x}{1+\alpha x} dx
        $$
        通过代数变换 $\frac{x}{1+\alpha x} = \frac{1}{\alpha}(1 - \frac{1}{1+\alpha x})$，积分可得：
        $$
        c_1 = \sqrt{3}\frac{1}{2\alpha^2}\left(2\alpha - \ln\left(\frac{1+\alpha}{1-\alpha}\right)\right)
        $$
这样，我们就得到了模型响应 $Q(\xi)$ 的一阶PCE近似：$Q(\xi) \approx c_0 \psi_0(\xi) + c_1 \psi_1(\xi)$。

### PCE的核心优势：[不确定性量化](@entry_id:138597)

PCE最引人注目的优点之一是，一旦展开系数被计算出来，模型响应的关键[统计矩](@entry_id:268545)（如均值和方差）就可以被几乎无成本地解析获得。

**均值与方差的计算**

利用基[函数的正交性](@entry_id:160337)，我们可以轻松推导出均值和方差的表达式 。

*   **均值** $\mathbb{E}[Y]$：
    $$
    \mathbb{E}[Y] = \mathbb{E}\left[\sum_{\alpha} c_\alpha \Psi_\alpha(\boldsymbol{\xi})\right] = \sum_{\alpha} c_\alpha \mathbb{E}[\Psi_\alpha(\boldsymbol{\xi})]
    $$
    由于 $\Psi_0 = 1$ 是常[数基](@entry_id:634389)函数，并且对于所有 $\alpha \neq \mathbf{0}$，$\mathbb{E}[\Psi_\alpha] = \mathbb{E}[\Psi_\alpha \Psi_0] = \langle \Psi_\alpha, \Psi_0 \rangle = 0$。因此，上式简化为：
    $$
    \mathbb{E}[Y] = c_{\mathbf{0}} \mathbb{E}[\Psi_{\mathbf{0}}] = c_{\mathbf{0}}
    $$
    模型响应的均值就是第零阶的PCE系数。

*   **方差** $\text{Var}(Y)$：
    方差定义为 $\text{Var}(Y) = \mathbb{E}[(Y - \mathbb{E}[Y])^2]$。将PCE代入，我们有 $Y - \mathbb{E}[Y] = \sum_{\alpha \neq \mathbf{0}} c_\alpha \Psi_\alpha(\boldsymbol{\xi})$。
    $$
    \text{Var}(Y) = \mathbb{E}\left[ \left(\sum_{\alpha \neq \mathbf{0}} c_\alpha \Psi_\alpha\right) \left(\sum_{\beta \neq \mathbf{0}} c_\beta \Psi_\beta\right) \right] = \sum_{\alpha \neq \mathbf{0}} \sum_{\beta \neq \mathbf{0}} c_\alpha c_\beta \mathbb{E}[\Psi_\alpha \Psi_\beta]
    $$
    再次利用正交性 $\mathbb{E}[\Psi_\alpha \Psi_\beta] = \delta_{\alpha\beta}$，双[重求和](@entry_id:275405)坍缩为：
    $$
    \text{Var}(Y) = \sum_{\alpha \neq \mathbf{0}} c_\alpha^2
    $$
    模型响应的方差是所有非零阶PCE系数的[平方和](@entry_id:161049)。这个公式优雅地将总[方差分解](@entry_id:912477)为各个正交模式的贡献，为[全局敏感性分析](@entry_id:171355)（[Sobol'指数](@entry_id:165435)）提供了直接的计算途径。

*   **示例：从系数计算均值和方差** ：
    假设一个模型响应由二阶PCE给出 $u(\xi) = u_0 \psi_0(\xi) + u_1 \psi_1(\xi) + u_2 \psi_2(\xi)$，其中系数为 $u_0 = 2$, $u_1 = -1$, $u_2 = \frac{1}{2}$。根据上述公式：
    *   均值: $\mathbb{E}[u(\xi)] = u_0 = 2$
    *   方差: $\text{Var}(u(\xi)) = u_1^2 + u_2^2 = (-1)^2 + (\frac{1}{2})^2 = 1 + \frac{1}{4} = \frac{5}{4}$

### PCE的收敛性与局限性

PCE的强大功能依赖于其快速收敛的特性，但这并非无条件的。理解其收敛性要求和局限性对于有效应用该方法至关重要。

#### [谱收敛](@entry_id:142546)性：PCE为何高效

PCE最著名的特性是其**[谱收敛](@entry_id:142546)性**，即对于光滑的函数，其近似误差随多项式阶数 $p$ 的增加呈指数级下降，形式如 $C \exp(-\gamma p)$。这种[收敛速度](@entry_id:636873)远超传统的蒙特卡洛方法（其[误差收敛](@entry_id:137755)速度为 $N^{-1/2}$）。

这种优异性能的根源在于**参数-解映射的光滑性**。如果模型响应 $Y(\boldsymbol{\xi})$ 作为其输入参数 $\boldsymbol{\xi}$ 的函数是**解析**的（即可以[泰勒展开](@entry_id:145057)），并且可以在包含参数实际取值范围的一个[复数域](@entry_id:153768)内进行**全纯延拓**，那么PCE就能实现[谱收敛](@entry_id:142546)。在更严格的数学表述中，这要求在[复数域](@entry_id:153768)内，问题仍然是**一致良定**的（例如，对于一个[偏微分](@entry_id:194612)方程模型，其对应的[双线性形式](@entry_id:746794)在复参[数域](@entry_id:155558)内保持一致强制性）。

#### 收敛性的退化与挑战

当模型响应不光滑时，PCE的[谱收敛](@entry_id:142546)性会丧失。在环境与[地球系统模型](@entry_id:1124096)中，这种非[光滑性](@entry_id:634843)可能源于多种物理过程，如相变、干湿转换、或者结构力学中的接触与屈服等。

考虑一个由于[单边接触](@entry_id:756326)而产生“拐点”（kink）的[响应函数](@entry_id:142629) $R(\xi) = k_s \max(0, \alpha \xi - c)$ 。该函数在 $\xi^\star = c/\alpha$ 点是[连续但不可导](@entry_id:261860)的（$C^0$ 但非 $C^1$）。这种**局部非[解析性](@entry_id:140716)**破坏了全局[谱收敛](@entry_id:142546)的前提。当使用全局光滑的多项式（如Hermite或Legendre）去逼近这样一个带拐点的函数时，会发生以下情况：
*   **[收敛速度](@entry_id:636873)退化**：[收敛速度](@entry_id:636873)从指数级下降为**代数级**（例如 $p^{-k}$），效率大打[折扣](@entry_id:139170)。
*   **[吉布斯现象](@entry_id:138701)**：在[拐点](@entry_id:144929)附近，PCE近似会产生持续的、不会随阶数增加而消失的振荡，类似于[傅里叶级数](@entry_id:139455)在阶跃不连续点附近的行为。

**解决方案：多单元PCE (Multi-element PCE)**

为了克服非光滑性带来的挑战，可以采用**多单元PCE**方法。其核心思想是在输入参数空间中，沿着不连续或不可导的区域进行**[区域分解](@entry_id:165934)**。例如，对于上述接触问题，我们可以在 $\xi^\star$ 点将输入域 $(-\infty, \infty)$ 分割为 $(-\infty, \xi^\star]$ 和 $(\xi^\star, \infty)$ 两个单元。在每个单元内部，函数 $R(\xi)$ 是解析的（在本例中甚至是简单的多项式）。因此，我们可以在每个单元上独立构建一个局部的PCE。由于每个局部函数都是光滑的，[谱收敛](@entry_id:142546)性得以恢复。最终，全局的[统计矩](@entry_id:268545)可以通过对各单元上的结果进行概率加权平均来获得（依据全期望和全方差定律）。

### 高维问题中的PCE：挑战与对策

当模型的不确定性输入源数量 $d$ 很大时，PCE会面临所谓的**[维度灾难](@entry_id:143920)**（Curse of Dimensionality）。

#### 维度灾难

PCE基函数的数量由截断后的多[指标集](@entry_id:268489) $\mathcal{A}$ 的[基数](@entry_id:754020) $|\mathcal{A}|$ 决定。对于一个 $d$ 维问题，即使是中等的多项式阶数 $p$，基函数的总数也可能爆炸式增长，使得计算PCE系数的成本变得无法承受。

#### 截断策略

为了在计算成本和近似精度之间取得平衡，必须明智地选择用于截断PCE级数的多[指标集](@entry_id:268489)。

*   **全阶（Total-Degree, TD）截断**：这是最简单和最常见的截断策略。它包含所有总阶数不超过 $p$ 的多项式：
    $$
    \mathcal{A}_p^{\text{TD}} = \{ \alpha \in \mathbb{N}_0^d : |\alpha|_1 = \sum_{k=1}^d \alpha_k \le p \}
    $$
    其[基数](@entry_id:754020)由组合数公式给出：$|\mathcal{A}_p^{\text{TD}}| = \binom{p+d}{d} \sim \frac{p^d}{d!}$ (对于大的 $p$) 。这种策略是**各向同性**的，即同等对待所有维度的[交互作用](@entry_id:164533)。然而，当 $d$ 很大时，其[基数](@entry_id:754020)增长非常迅速。例如，一个6维问题，4阶TD展开的基函数数量为 $|\mathcal{A}_4^{\text{TD}}| = \binom{4+6}{4} = 210$ 。

*   **双曲交叉（Hyperbolic-Cross, HC）截断**：许多模型中，高阶交互作用的重要性远低于低阶[交互作用](@entry_id:164533)和单个参数的高阶影响。HC截断正是利用了这一点，它包含的多指标满足：
    $$
    \mathcal{A}_p^{\text{HC}} = \{ \alpha \in \mathbb{N}_0^d : \prod_{k=1}^d (\alpha_k + 1) \le p + 1 \}
    $$
    这个集合优先包含那些只有少数几个分量非零的多指标，从而有效地减少了高阶交互项的数量。对于固定的 $d$ 和大的 $p$，其[基数](@entry_id:754020)增长为 $|\mathcal{A}_p^{\text{HC}}| \sim \mathcal{O}(p(\log p)^{d-1})$，远慢于TD集。对于固定的 $p$ 和大的 $d$，其[基数](@entry_id:754020)仅随 $d$ [多项式增长](@entry_id:177086)，而TD集的[基数](@entry_id:754020)则随 $d^p$ 增长 。这使得HC集在高维问题中特别有吸[引力](@entry_id:189550)。

*   **各向异性（Anisotropic）截断**：如果已知某些输入参数比其他参数更重要，我们可以采用加权的截断策略。例如，一个加权TD集定义为：
    $$
    \mathcal{A}_p^{\text{aniso}} = \{ \alpha \in \mathbb{N}_0^d : \boldsymbol{w} \cdot \boldsymbol{\alpha} = \sum_{k=1}^d w_k \alpha_k \le p \}
    $$
    其中权重向量 $\boldsymbol{w}$ 反映了参数的相对重要性（重要参数权重小，允许更高阶展开）。通过为不重要的参数分配较大的权重，可以有效削减PCE基的规模，同时保留对关键参数的足够分辨率 。例如，对于前述的6维问题，如果权重为 $\boldsymbol{w}=(3,2,2,1,1,1)$，总阶数 $p=4$ 的各向异性集[基数](@entry_id:754020)仅为62，远小于各向同性TD集的210。

#### 处理相关输入

标准PCE的构建依赖于输入变量的**[相互独立](@entry_id:273670)性**，这样才能通过[张量积](@entry_id:140694)构建多元[正交基](@entry_id:264024)。然而，在真实世界的环境模型中，输入变量（如降雨和土壤导水率）往往是相关的。

为了在这种情况下使用PCE，需要先通过**等概率变换**（Isoprobabilistic Transform）将相关的物理变量 $\boldsymbol{X}$ 映射到一个[辅助空间](@entry_id:638067)中的独立标准变量 $\boldsymbol{Z}$。然后，在 $\boldsymbol{Z}$ 的空间中构建PCE。两种常见的变换是Nataf变换和Rosenblatt变换。

*   **Nataf变换**：该变换适用于其依赖结构可以用**高斯Copula**描述的输入。它通过两步实现：(1) 使用逆标准正态CDF和各变量的边缘CDF，将每个分量 $X_i$ 映射到一个标准正态变量 $Y_i$；(2) 对生成的相关高斯向量 $\boldsymbol{Y}$ 进行线性[解耦](@entry_id:160890)（如[Cholesky分解](@entry_id:147066)）得到独立的标准正态向量 $\boldsymbol{Z}$。Nataf变换的优点是仅需要边缘分布和变量间的[皮尔逊相关系数](@entry_id:918491)矩阵。其缺点是，高斯Copula的假设可能无法准确捕捉真实世界中的**[尾部相关性](@entry_id:140618)**（即极端事件同时发生的概率），这在风险评估中可能导致严重偏差 , 。

*   **Rosenblatt变换**：这是一种更通用的非参数变换。它通过变量的条件CDF[链式法则](@entry_id:190743)来构造映射：
    $$
    U_1 = F_{X_1}(X_1), \quad U_2 = F_{X_2|X_1}(X_2|X_1), \quad \dots
    $$
    理论上，只要联合CDF已知且连续，Rosenblatt变换就能精确地将任意相关的向量 $\boldsymbol{X}$ 映射为一组[相互独立](@entry_id:273670)的标准均匀变量 $\boldsymbol{U}$，后者可以进一步映射到标准正态变量。其优点是理论上的精确性，不依赖任何Copula假设。缺点是它需要完整的[联合分布](@entry_id:263960)知识（这往往难以获得），并且变换本身依赖于变量的排序 。

通过这些变换，PCE的应用范围被极大地扩展到了具有相关输入的现实问题中。值得注意的是，如果一个模型在变换后的独立变量空间中是多项式形式，那么其PCE展开将是精确的。这意味着从PCE系数计算出的[统计矩](@entry_id:268545)是真实响应的精确矩，而[蒙特卡洛模拟](@entry_id:193493)只能提供这些真实矩的[统计估计](@entry_id:270031) 。