## 引言
在[分子生物学](@entry_id:140331)和合成生物学的世界里，随机性不是例外，而是规则。即使是遗传上完全相同的细胞，在相同的环境中也会表现出显著的个体差异，这种现象被称为“噪声”。理解和控制这种噪声对于揭示生命过程的基本原理以及设计可靠的生物系统至关重要。虽然化学主方程（CME）为描述这些[随机过程](@entry_id:268487)提供了精确的数学框架，但其固有的复杂性使得直接求解几乎成为不可能完成的任务，这构成了一个显著的知识鸿沟。

为了跨越这一鸿沟，科学家们发展了多种近似方法，其中[线性噪声近似](@entry_id:190628)（LNA）尤为突出。本文旨在全面深入地探讨 LNA。我们将引导您完成一个系统的学习路径，从其第一性原理到前沿应用。在“原理与机制”一章中，您将学习 LNA 是如何从 CME 中通过体系大小展开推导出来的，并理解其背后的数学假设和物理直觉。接下来的“应用与跨学科联系”一章将展示 LNA 作为分析和设计工具的强大功能，涵盖从解构[基因表达噪声](@entry_id:160943)到指导合成生物学回路设计，再到其在[参数推断](@entry_id:753157)和生态学中的应用。最后，通过“动手实践”部分，您将有机会将理论知识应用于具体问题，从而巩固对 [LNA](@entry_id:150014) 的掌握。这篇文章将为您装备一个强大的理论框架，用以分析和驾驭复杂生物系统中的随机世界。

## 原理与机制

本章旨在深入探讨[线性噪声近似](@entry_id:190628) (Linear Noise Approximation, [LNA](@entry_id:150014)) 的理论基础和核心机制。我们将从化学主方程 (Chemical Master Equation, CME) 出发，系统地推导出 [LNA](@entry_id:150014)，阐明其背后的数学近似，并通过具体的生物化学网络实例，展示如何应用 [LNA](@entry_id:150014) 来量化和分析随机性。最后，我们将严格审视 [LNA](@entry_id:150014) 的[适用范围](@entry_id:636189)及其在特定条件下的失效模式。

### 化学主方程：[随机动力学](@entry_id:187867)的基石

在深入研究近似方法之前，我们必须首先建立一个精确描述随机生化反应网络的数学框架。对于一个在恒定体积和温度下充分混合的系统，其状态由各种分子物质的拷贝数向量 $\boldsymbol{n} \in \mathbb{N}^N$ 完全描述，其中 $N$ 是物质的种[类数](@entry_id:156164)。系统通过一系列（共 $R$ 个）化学反应通道进行演化。每个反应 $r$ 都由一个化学计量变化向量 $\boldsymbol{\nu}_r \in \mathbb{Z}^N$ 和一个**[倾向函数](@entry_id:181123) (propensity function)** $a_r(\boldsymbol{n})$ 来定义。当反应 $r$ 发生一次时，系统状态从 $\boldsymbol{n}$ 跳转到 $\boldsymbol{n} + \boldsymbol{\nu}_r$。

[倾向函数](@entry_id:181123) $a_r(\boldsymbol{n})$ 的物理意义至关重要：在给定当前状态为 $\boldsymbol{n}$ 的条件下，反应 $r$ 在下一个无穷小时间间隔 $(t, t+dt]$ 内发生一次的概率为 $a_r(\boldsymbol{n})dt + o(dt)$。这个定义是建立[随机动力学](@entry_id:187867)模型的出发点。

为了描述系统状态的概率分布 $P(\boldsymbol{n}, t)$ 如何随时间演化，我们考虑在时间间隔 $dt$ 内进出状态 $\boldsymbol{n}$ 的[概率流](@entry_id:907649)。一个状态 $\boldsymbol{n}$ 的概率会因为任何一个反应 $r$ 的发生而减少，其总流出速率为 $\sum_{r=1}^R a_r(\boldsymbol{n})P(\boldsymbol{n}, t)$。同时，概率会从其他状态流入 $\boldsymbol{n}$。能够通过一次反应 $r$ 跳转到状态 $\boldsymbol{n}$ 的前驱状态必然是 $\boldsymbol{n} - \boldsymbol{\nu}_r$。因此，从所有前驱状态流入的总速率为 $\sum_{r=1}^R a_r(\boldsymbol{n}-\boldsymbol{\nu}_r)P(\boldsymbol{n}-\boldsymbol{\nu}_r, t)$。

综合流入和流出项，我们可以写出[概率守恒](@entry_id:149166)的[微分](@entry_id:158422)方程，即**化学主方程 (Chemical Master Equation, CME)** ：
$$
\frac{d}{dt}P(\boldsymbol{n},t) = \sum_{r=1}^R \Big[ a_r(\boldsymbol{n}-\boldsymbol{\nu}_r) P(\boldsymbol{n}-\boldsymbol{\nu}_r,t) - a_r(\boldsymbol{n}) P(\boldsymbol{n},t) \Big]
$$
此方程约定，如果[状态向量](@entry_id:154607) $\boldsymbol{n}-\boldsymbol{\nu}_r$ 的任何分量为负，则该项为零，因为分子拷贝数不能为负。CME 本质上是描述系统状态在[离散状态空间](@entry_id:146672)上进行[连续时间马尔可夫链](@entry_id:267837) (Continuous-Time Markov Chain, CTMC) 演化的 Kolmogorov 前向方程。

CME 的有效性依赖于一系列关键的物理假设 ：
1.  **充分混合假设**：系统在空间上是均匀的，没有浓度梯度，因此状态完全由分子总数描述。
2.  **马尔可夫假设**：反应的未来演化仅依赖于当前状态，而与系统的历史无关。这意味着反应是瞬时完成的，没有时间延迟。
3.  **基本反应事件**：在无穷小时间间隔 $dt$ 内，发生多于一次反应的概率是高阶小量 $o(dt)$。
4.  **内禀噪声**：系统中的所有随机性都源于化学反应事件本身固有的随机时机，不考虑温度波动等外部来源的噪声。

CME 为[随机化学动力学](@entry_id:185805)提供了精确的描述，但它通常是一个高维的、耦合的常微分方程组，除了极少数简单情况外，很难获得解析解。这正是 [LNA](@entry_id:150014) 等近似方法发挥作用的舞台。

### 体系大小展开：从微观到宏观的桥梁

[线性噪声近似](@entry_id:190628)的核心思想是通过**体系大小展开 (system-size expansion)**，在体系大小（如体积）$\Omega$ 很大但有限的极限下，对 CME 进行系统性的近似。这一方法由 van Kampen 提出，其关键在于将分子拷贝数 $\boldsymbol{n}(t)$ 分解为一个宏观的、确定性的部分和一个随机的、较小的涨落部分 。

我们将分子拷贝数 $\boldsymbol{n}$（一个广延量）与浓度 $\boldsymbol{x}$（一个强度量）联系起来，即 $\boldsymbol{x} = \boldsymbol{n}/\Omega$。van Kampen 的核心** ansatz ([拟设](@entry_id:184384))** 如下：
$$
\boldsymbol{n}(t) = \Omega \boldsymbol{x}(t) + \sqrt{\Omega} \boldsymbol{\xi}(t)
$$
这里，$\boldsymbol{x}(t)$ 是满足确定性宏观速率方程的浓度向量，而 $\boldsymbol{\xi}(t)$ 是一个量级为 $\mathcal{O}(1)$ 的新[随机变量](@entry_id:195330)，描述了围绕宏观轨迹的涨落。

这个[拟设](@entry_id:184384)的合理性根植于对反应事件统计特性的分析。对于一个在体积 $\Omega$ 中发生的化学反应，其[倾向函数](@entry_id:181123) $a_r(\boldsymbol{n})$ 通常与体系大小 $\Omega$ 成正比。例如，一个[一级反应](@entry_id:136907) $A \to \dots$，其[倾向函数](@entry_id:181123)为 $a(n_A) = c n_A = c (\Omega x_A)$，是 $\mathcal{O}(\Omega)$。对于一个[二级反应](@entry_id:139599) $A+B \to \dots$，其[倾向函数](@entry_id:181123)为 $a(n_A, n_B) = c \frac{n_A n_B}{\Omega} = c \frac{(\Omega x_A)(\Omega x_B)}{\Omega} = c \Omega x_A x_B$，其量级也是 $\mathcal{O}(\Omega)$。为了保持宏观描述的一致性，我们必须恰当地调整微观[速率常数](@entry_id:140362) $c$ 的标度，以确保所有基本反应的[倾向函数](@entry_id:181123)在写成浓度形式时，其[主导项](@entry_id:167418)都与 $\Omega$ 成线性关系 。总的来说，我们可以写出 $a_r(\boldsymbol{n}) \approx \Omega f_r(\boldsymbol{x})$，其中 $f_r(\boldsymbol{x})$ 是宏观[反应速率](@entry_id:185114)函数。

在微小时间间隔 $\Delta t$ 内，反应 $r$ 发生的次数可以近似为一个泊松[随机变量](@entry_id:195330)，其均值和方差均为 $a_r(\boldsymbol{n})\Delta t$。因此，[状态向量](@entry_id:154607) $\boldsymbol{n}$ 的总增量 $\Delta \boldsymbol{n}$ 的条件均值（漂移）和协方差（扩散）分别为：
$$
\mathbb{E}[\Delta \boldsymbol{n} | \boldsymbol{n}] = \sum_{r=1}^R \boldsymbol{\nu}_r a_r(\boldsymbol{n}) \Delta t = \mathcal{O}(\Omega \Delta t)
$$
$$
\text{Cov}[\Delta \boldsymbol{n} | \boldsymbol{n}] = \sum_{r=1}^R \boldsymbol{\nu}_r \boldsymbol{\nu}_r^\top a_r(\boldsymbol{n}) \Delta t = \mathcal{O}(\Omega \Delta t)
$$
由于方差的量级为 $\mathcal{O}(\Omega \Delta t)$，标准差的量级就是 $\mathcal{O}(\sqrt{\Omega} \sqrt{\Delta t})$。这表明，分子拷贝数的涨落幅度与 $\sqrt{\Omega}$ 成正比，这为 van Kampen 拟设中的 $\sqrt{\Omega}\boldsymbol{\xi}(t)$ 项提供了有力的支持 。这个展开实际上是在小参数 $\Omega^{-1/2}$ 下进行的。

### [LNA](@entry_id:150014) 方程的推导

将体系大小展开的拟设代入 CME，并将[倾向函数](@entry_id:181123) $a_r(\boldsymbol{n})$ 在宏观部分 $\Omega\boldsymbol{x}$ 附近进行[泰勒展开](@entry_id:145057)，然后按照 $\Omega$ 的幂次收集各项，我们就能得到一个方程层级。

#### 宏观动力学：[主导项](@entry_id:167418)

展开后的最高阶项（量级为 $\mathcal{O}(\Omega)$）必须相互抵消，这给出了描述浓度向量 $\boldsymbol{x}(t)$ 演化的确定性**宏观[速率方程](@entry_id:198152) (macroscopic rate equations)**：
$$
\frac{d\boldsymbol{x}}{dt} = \sum_{r=1}^R \boldsymbol{\nu}_r f_r(\boldsymbol{x}) \equiv \boldsymbol{F}(\boldsymbol{x})
$$
这里的 $\boldsymbol{\nu}_r$ 是化学计量向量。需要注意的是，在从分子数 $\boldsymbol{n}$ 转换到浓度 $\boldsymbol{x}$ 时，[化学计量矩阵](@entry_id:275342) $S$ 本身保持不变（其元素为整数），但单次反应在浓度空间中产生的“跳跃”幅度为 $\boldsymbol{\nu}_r/\Omega$，量级为 $\mathcal{O}(1/\Omega)$ 。宏观速率方程可以更紧凑地写为 $\frac{d\boldsymbol{x}}{dt} = S \boldsymbol{f}(\boldsymbol{x})$，其中 $S$ 是 $N \times R$ 的[化学计量矩阵](@entry_id:275342)，$\boldsymbol{f}(\boldsymbol{x})$ 是 $R \times 1$ 的宏观速率向量。

例如，考虑一个简单的 mRNA 合成与降解模型（组成性基因表达）：
1.  转录: $\emptyset \xrightarrow{k_m} M$
2.  降解: $M \xrightarrow{\gamma_m} \emptyset$

其宏观[速率方程](@entry_id:198152)为 ：
$$
\frac{dx_m}{dt} = k_m - \gamma_m x_m
$$
其中 $k_m$ 是单位体积的生产速率（单位：浓度/时间），$\gamma_m$ 是一阶降解[速率常数](@entry_id:140362)（单位：1/时间）。

#### 涨落动力学：次[主导项](@entry_id:167418)

在方程层级中的次[主导项](@entry_id:167418)（量级为 $\mathcal{O}(\sqrt{\Omega})$）描述了涨落变量 $\boldsymbol{\xi}(t)$ 的动力学。这些项构成了一个线性的**[福克-普朗克方程](@entry_id:140155) (Fokker-Planck equation)**，该方程等价于一个线性的**[随机微分方程](@entry_id:146618) (Stochastic Differential Equation, SDE)**，这便是[线性噪声近似](@entry_id:190628)的核心方程：
$$
d\boldsymbol{\xi}(t) = J(\boldsymbol{x}(t)) \boldsymbol{\xi}(t) dt + \sqrt{D(\boldsymbol{x}(t))} d\boldsymbol{W}(t)
$$
其中：
-   $J(\boldsymbol{x}(t))$ 是宏观[速率方程](@entry_id:198152)在确定性轨迹 $\boldsymbol{x}(t)$ 上的**[雅可比矩阵](@entry_id:178326) (Jacobian matrix)**，$J_{ij} = \frac{\partial F_i}{\partial x_j}$。它描述了一个线性的恢复力，将涨落拉回到零点。
-   $D(\boldsymbol{x}(t))$ 是**[扩散矩阵](@entry_id:182965) (diffusion matrix)**，它量化了随机噪声的强度。其形式为 $D = S \cdot \text{diag}(\boldsymbol{f}(\boldsymbol{x})) \cdot S^\top$。此[扩散矩阵](@entry_id:182965) $D$ 的量级为 $\mathcal{O}(1)$。与之相关，描述浓度 $\boldsymbol{x}$ 的[扩散矩阵](@entry_id:182965)量级为 $\mathcal{O}(1/\Omega)$ 。
-   $d\boldsymbol{W}(t)$ 是一个多维标准[维纳过程](@entry_id:137696)（[高斯白噪声](@entry_id:749762)）的增量。

这个方程描述的涨落过程是[高斯过程](@entry_id:182192)，这源于两个核心近似 ：
1.  **动力学线性化**：通过[泰勒展开](@entry_id:145057)并将漂移项截断至关于 $\boldsymbol{\xi}$ 的线性项，我们将[非线性](@entry_id:637147)的动力学在确定性轨迹附近线性化了。
2.  **噪声扩散近似**：底层的离散[跳跃过程](@entry_id:180953)（[泊松过程之和](@entry_id:261287)）在大量事件的极限下，根据[泛函中心极限定理](@entry_id:182006)，可以用连续的[高斯白噪声](@entry_id:749762)来近似。

一个[线性系统](@entry_id:147850)由高斯噪声驱动，其解必然是[高斯过程](@entry_id:182192)。因此，[LNA](@entry_id:150014) 预测涨落 $\boldsymbol{\xi}(t)$ 服从高斯分布。需要注意的是，这要求初始涨落 $\boldsymbol{\xi}(0)$ 也是高斯分布的（或是一个常数，即退化的高斯分布）。

### [稳态](@entry_id:139253)涨落与 Ornstein-Uhlenbeck 过程

在许多应用中，我们更关心系统在达到宏观[稳态](@entry_id:139253) $\boldsymbol{x}^*$（即 $\boldsymbol{F}(\boldsymbol{x}^*) = 0$）后的长时间行为。如果这个不动点是[渐近稳定](@entry_id:168077)的（即[雅可比矩阵](@entry_id:178326) $J(\boldsymbol{x}^*)$ 的所有特征值的实部都为负），那么确定性轨迹 $\boldsymbol{x}(t)$ 将会收敛到 $\boldsymbol{x}^*$。

在这种情况下，LNA 方程中的时变系数 $J(\boldsymbol{x}(t))$ 和 $D(\boldsymbol{x}(t))$ 可以用它们在不动点处的常数值 $J(\boldsymbol{x}^*)$ 和 $D(\boldsymbol{x}^*)$ 来近似。这样，SDE 就简化为一个具有[常系数](@entry_id:269842)的线性 SDE ：
$$
d\boldsymbol{\xi}(t) = J \boldsymbol{\xi}(t) dt + \sqrt{D} d\boldsymbol{W}(t)
$$
这个方程定义了一个**Ornstein-Uhlenbeck (OU) 过程**。由于 $J$ 是一个[稳定矩阵](@entry_id:180808)，这个 OU 过程存在唯一的[稳态分布](@entry_id:149079)。这个[稳态分布](@entry_id:149079)是一个均值为零的多元高斯分布 $\mathcal{N}(0, \Sigma)$。

其[稳态](@entry_id:139253)协方差矩阵 $\Sigma$ 是通过求解一个**连续时间代数[李雅普诺夫方程](@entry_id:156397) (continuous-time algebraic Lyapunov equation)** 得到的：
$$
J\Sigma + \Sigma J^\top + D = 0
$$
这个方程为我们提供了一个强大的代数工具，可以直接计算系统在[稳态](@entry_id:139253)下的噪声大小（方差）和不同组分之间的[噪声相关](@entry_id:1128753)性（协方差），而无需模拟[随机轨迹](@entry_id:755474)。

### 应用实例

让我们通过两个具体的例子来展示 [LNA](@entry_id:150014) 的完整分析流程。

#### 实例一：线性级联反应

考虑一个[反应网络](@entry_id:203526)，其中物质 X 被产生，然后降解或转化为物质 Y，Y 再降解 。
-   $\varnothing \xrightarrow{k_{x}\Omega} X$
-   $X \xrightarrow{d_{x}} \varnothing$
-   $X \xrightarrow{k_{c}} Y$
-   $Y \xrightarrow{d_{y}} \varnothing$

1.  **宏观方程与[稳态](@entry_id:139253)**：
    $$
    \frac{d\phi_X}{dt} = k_x - (d_x + k_c) \phi_X \\
    \frac{d\phi_Y}{dt} = k_c \phi_X - d_y \phi_Y
    $$
    稳态解为 $\phi_X^* = \frac{k_x}{d_x + k_c}$ 和 $\phi_Y^* = \frac{k_c k_x}{d_y(d_x + k_c)}$。

2.  **[雅可比矩阵](@entry_id:178326)和[扩散矩阵](@entry_id:182965)**：
    $$
    J = \begin{pmatrix} -(d_x + k_c) & 0 \\ k_c & -d_y \end{pmatrix}, \quad
    D = \begin{pmatrix} 2k_x & -\frac{k_c k_x}{d_x+k_c} \\ -\frac{k_c k_x}{d_x+k_c} & \frac{2k_c k_x}{d_x+k_c} \end{pmatrix}
    $$

3.  **求解[李雅普诺夫方程](@entry_id:156397)**：通过求解 $J\Sigma + \Sigma J^\top + D = 0$，可以得到[协方差矩阵](@entry_id:139155) $\Sigma$ 的各个元素。例如，可以算出 $\Sigma_{YY} = \frac{k_c k_x}{d_y(d_x+k_c)} = \phi_Y^*$。

4.  **计算分子数方差**：根据 LNA 拟设，分子数的方差与浓度涨落的方差关系为 $\text{Var}(n_Y) = \Omega \Sigma_{YY}$。因此，我们得到一个简洁的结果：
    $$
    \text{Var}(n_Y) = \Omega \frac{k_c k_x}{d_y(d_x+k_c)} = \mathbb{E}[n_Y]
    $$
    在这个特定的[线性系统](@entry_id:147850)中，Y 的分子数分布遵循泊松分布，其 Fano 因子（方差/均值）为 1。

#### 实例二：两阶段[基因表达模型](@entry_id:178501)

现在考虑一个更经典的生物学模型：mRNA (M) 和蛋白质 (P) 的产生与降解 。
-   转录: $\varnothing \xrightarrow{k_m} M$
-   mRNA 降解: $M \xrightarrow{\gamma_m} \varnothing$
-   翻译: $M \xrightarrow{k_p} M + P$
-   [蛋白质降解](@entry_id:187883): $P \xrightarrow{\gamma_p} \varnothing$

通过与前例完全相同的步骤，我们可以计算出[雅可比矩阵](@entry_id:178326) $A$（在 [LNA](@entry_id:150014) 文献中常用 $A$ 代替 $J$）、[扩散矩阵](@entry_id:182965) $D$，并求解[李雅普诺夫方程](@entry_id:156397)。最终，我们可以得到蛋白质拷贝数 $n_P$ 的**法诺因子 (Fano factor)** $F_P = \text{Var}(n_P) / \mathbb{E}[n_P]$，这是一个衡量噪声相对大小的无量纲量。计算结果为：
$$
F_P = 1 + \frac{k_p}{\gamma_m + \gamma_p}
$$
这个著名的结果揭示了蛋白质噪声的两个来源：“1”代表蛋白质产生和降解的泊松过程所产生的内禀噪声，而第二项 $\frac{k_p}{\gamma_m + \gamma_p}$ 则代表了上游 mRNA 分子数涨落传递到下游所造成的**外源噪声 (extrinsic noise)**（在此模型中，mRNA 涨落对蛋白质而言是“外源”的）。这一结果清晰地展示了 [LNA](@entry_id:150014) 如何能够提供关于[噪声传播](@entry_id:266175)和组成的深刻见解。

### LNA 的适用性与局限性

作为一种近似方法，理解 [LNA](@entry_id:150014) 的有效性边界至关重要。

#### 一般有效性条件

[LNA](@entry_id:150014) 的有效性基于以下几个核心条件 ：
1.  **大体系极限**：$\Omega$ 必须足够大，使得 $\Omega^{-1/2}$ 是一个真正的小参数。这意味着所有物种的平均分子数都应该很大。
2.  **宏观稳定性**：系统应围绕一个[渐近稳定](@entry_id:168077)的不动点或[极限环](@entry_id:274544)进行涨落。[LNA](@entry_id:150014) 描述的是对微小扰动的线性响应，因此需要一个稳定的[参考态](@entry_id:151465)。
3.  **远离边界和[分岔点](@entry_id:187394)**：涨落的幅度（量级为 $\sqrt{\Omega}$）必须远小于平均分子数（量级为 $\Omega$），以确保系统状态不会频繁触及物理边界（如分子数为零），也不会探索到动力学发生质变的区域（如分岔点）。

#### 在[多稳态](@entry_id:180390)系统中的局域性

如果一个系统的宏观动力学具有多个稳定的不动点（即存在**[多稳态](@entry_id:180390) (multistability)**），[LNA](@entry_id:150014) 只能在单个吸引盆内部提供局域的、高斯型的涨落描述。它无法捕捉由大的、罕见的涨落驱动的、跨越势垒在不同[稳态](@entry_id:139253)之间切换的动力学。因此，[LNA](@entry_id:150014) 预测的单峰高斯分布不能代表全局的、通常是多峰的[稳态分布](@entry_id:149079) 。

#### 失效模式一：临界慢化

当系统参数接近一个**分岔点**（例如鞍结分岔或霍普夫分岔）时，[LNA](@entry_id:150014) 会失效 。在分岔点附近，[雅可比矩阵](@entry_id:178326) $J$ 的一个或多个特征值的实部趋于零。这对应于**临界慢化 (critical slowing down)**，即系统沿某个特定方向（由相应[特征向量](@entry_id:151813)定义）的[弛豫时间](@entry_id:191572)变得极长。

从[李雅普诺夫方程](@entry_id:156397)的解可以看出，协方差矩阵 $\Sigma$ 的元素通常与特征值的倒数成比例。因此，当某个特征值 $\lambda_{\min} \to 0$ 时，沿该方向的涨落方差会发散，其量级为 $\mathcal{O}(1/|\lambda_{\min}|)$。这种发散的方差意味着涨落变得非常大，从而使得忽略动力学中的[非线性](@entry_id:637147)项这一核心假设失效。此时，需要更高阶的展开或[重整化群](@entry_id:147717)等更复杂的理论来描述非高斯的、异常的涨落。值得注意的是，如果噪声在慢化方向上的投影恰好为零，这种发散可能会被抑制 。

#### 失效模式二：低拷贝数物种

LNA 的一个更根本的局限性在于处理那些分子数本身不随体系大小 $\Omega$ 变化的物种，例如细胞中通常只有一个或两个拷贝的基因 。对于这类物种，体系大小展开的拟设从根本上就是不成立的。

考虑一个由两状态启动子驱动的[基因表达模型](@entry_id:178501)。启动子在活性 ($G^*$) 和非活性 ($G$) 状态之间切换，其总拷贝数为 1。
-   **慢切换机制**：如果启动子切换的速率 ($k_{\text{on}}, k_{\text{off}}$) 远小于 mRNA 和蛋白质的降解速率，系统会在长时间内分别处于“转录开启”和“转录关闭”两种宏观状态。这会导致下游 mRNA 和蛋白质的分布呈现双峰或多峰形态，这显然不能被 [LNA](@entry_id:150014) 的单峰高斯分布所描述。
-   **快切换机制**：反之，如果启动子切换非常快，我们可以**绝热地消除 (adiabatically eliminate)** 启动子状态变量，用一个有效的平均转录速率来代替。此时，如果下游的 mRNA 和蛋白质分子数足够大，LNA 就可以应用于这个简化后的系统 。

对于慢切换等含有离散、低拷贝数动态的系统，一个有效的补救措施是采用**[混合模型](@entry_id:266571) (hybrid models)**。这类模型将系统的离散、低拷贝数部分（如启动子状态）用精确的随机模拟方法（如 Gillespie 算法）处理，而将高拷贝数部分（如蛋白质）的动力学用 LNA 或确定性方程来近似，从而在保证精度的同时提高计算效率 。