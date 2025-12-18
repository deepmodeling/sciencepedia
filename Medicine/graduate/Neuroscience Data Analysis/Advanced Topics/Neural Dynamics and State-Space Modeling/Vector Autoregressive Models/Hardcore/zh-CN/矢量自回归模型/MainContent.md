## 引言
在神经科学、经济学和生物学等众多领域，我们面临的系统通常由多个相互作用的变量随时间演化构成。理解这些复杂系统内部的动态交互机制，是科学研究的核心挑战之一。向量自回归 (VAR) 模型为解决这一问题提供了强大而灵活的统计框架，它能够同时捕捉多个时间序列变量内部及其相互之间的动态依赖关系。然而，从原始的多元时间序列数据中准确地推断出有意义的连接模式、预测系统未来的行为，并区分真正的因果影响与虚假的相关性，需要对 VAR 模型的原理、应用和局限有深刻的理解。

本文旨在为读者提供一份关于 VAR 模型的全面指南。在接下来的内容中，我们将首先在“原理与机制”一章中深入探讨 VAR 模型的数学基础、稳定性条件以及格兰杰因果等核心解释工具。随后，“应用与跨学科连接”一章将通过丰富的案例展示 VAR 模型如何被用于推断功能网络、处理实验数据以及应对非平稳和高维等复杂情况。最后，“动手实践”部分将提供具体的练习，帮助读者巩固关键概念。通过这一结构化的学习路径，读者将能够系统地掌握使用 VAR 模型分析复杂动态系统的理论知识和实践技能。

## 原理与机制

本章旨在深入阐述向量自回归 (VAR) 模型的数学原理、核心机制及其在[神经科学数据分析](@entry_id:1128665)中的应用。我们将从模型的基本结构出发，逐步探讨其动态特性、稳定性条件，并最终介绍用于解释复杂神经系统动力学的关键工具，如[脉冲响应函数](@entry_id:1126431)和格兰杰因果分析。

### 向量自回归模型的结构

#### VAR(p) 过程的形式化定义

向量自回归（VAR）模型是单变量自回归（AR）模型到多维时间序列的直接扩展。它为分析多个相互作用的时间序列变量（例如，来自不同脑区的神经活动信号）提供了一个强大而灵活的框架。

一个 $k$ 维的 $p$ 阶向量[自回归过程](@entry_id:264527)，记作 **VAR(p)**，由以下方程组定义 ：
$$
\mathbf{y}_t = \mathbf{c} + A_1 \mathbf{y}_{t-1} + A_2 \mathbf{y}_{t-2} + \dots + A_p \mathbf{y}_{t-p} + \boldsymbol{\varepsilon}_t
$$
其中：
- $\mathbf{y}_t = (y_{1,t}, y_{2,t}, \dots, y_{k,t})'$ 是一个 $k \times 1$ 的向量，表示在时间点 $t$ 观测到的 $k$ 个变量的值。在神经科学背景下，这可能代表 $k$ 个不同皮层区域的[局部场电位](@entry_id:1127395)（LFP）功率或功能性[磁共振成像](@entry_id:153995)（fMRI）信号。
- $\mathbf{c}$ 是一个 $k \times 1$ 的常数向量，称为截距项，它决定了过程的长期均值。
- $A_i$ 是一个 $k \times k$ 的[系数矩阵](@entry_id:151473)，用于描述时间点 $t-i$ 的观测值 $\mathbf{y}_{t-i}$ 对当前值 $\mathbf{y}_t$ 的线性影响。这些矩阵捕捉了系统的动态特性。
- $\boldsymbol{\varepsilon}_t$ 是一个 $k \times 1$ 的向量，称为**新息**（innovation）或**扰动**（shock）。它是一个零均值的[白噪声过程](@entry_id:146877)，满足 $\mathbb{E}[\boldsymbol{\varepsilon}_t] = \mathbf{0}$ 且对于所有 $s \neq t$，$\mathbb{E}[\boldsymbol{\varepsilon}_t \boldsymbol{\varepsilon}_s'] = \mathbf{0}$。新息的同期协方差矩阵为 $\mathbb{E}[\boldsymbol{\varepsilon}_t \boldsymbol{\varepsilon}_t'] = \boldsymbol{\Sigma}_{\varepsilon}$，通常假设其为[正定矩阵](@entry_id:155546)。

与单变量 AR 模型（$y_t = c + \sum_{i=1}^p \phi_i y_{t-i} + \varepsilon_t$）的关键区别在于，VAR 模型中的系数 $A_i$ 是矩阵而非标量。这使得 VAR 模型不仅能捕捉每个变量自身的历史对其现在的影响（**自回归效应**），还能捕捉一个变量的历史对另一个变量的现在的影响（**交叉滞后效应**）。正是这些交叉滞后项，使得 VAR 模型成为研究[神经信号](@entry_id:153963)之间有向[交互作用](@entry_id:164533)的有力工具。

#### 动态展开：自回归与交叉滞后效应

为了更清晰地理解 VAR 模型如何编码动态交互，我们来看一个具体的例子。考虑一个由两个[神经信号](@entry_id:153963) $y_{1,t}$ 和 $y_{2,t}$ 组成的均值为零的二元 VAR(2) 模型 。其向量形式为：
$$
\mathbf{y}_t = A_1 \mathbf{y}_{t-1} + A_2 \mathbf{y}_{t-2} + \boldsymbol{\varepsilon}_t
$$
其中 $\mathbf{y}_t = \begin{pmatrix} y_{1,t} \\ y_{2,t} \end{pmatrix}$，系数矩阵为：
$$
A_1 = \begin{pmatrix} a_{11}^{(1)} & a_{12}^{(1)} \\ a_{21}^{(1)} & a_{22}^{(1)} \end{pmatrix}, \quad A_2 = \begin{pmatrix} a_{11}^{(2)} & a_{12}^{(2)} \\ a_{21}^{(2)} & a_{22}^{(2)} \end{pmatrix}
$$
通过执行[矩阵乘法](@entry_id:156035)，我们可以将这个紧凑的向量方程展开为两个标量方程：
$$
y_{1,t} = a_{11}^{(1)}y_{1,t-1} + a_{12}^{(1)}y_{2,t-1} + a_{11}^{(2)}y_{1,t-2} + a_{12}^{(2)}y_{2,t-2} + \varepsilon_{1,t}
$$
$$
y_{2,t} = a_{21}^{(1)}y_{1,t-1} + a_{22}^{(1)}y_{2,t-1} + a_{21}^{(2)}y_{1,t-2} + a_{22}^{(2)}y_{2,t-2} + \varepsilon_{2,t}
$$
在第一个方程中，项 $a_{11}^{(1)}y_{1,t-1}$ 和 $a_{11}^{(2)}y_{1,t-2}$ 描述了信号 $y_1$ 自身的过去对其现在的影响，这些由对[角系数](@entry_id:149598) $a_{11}^{(1)}$ 和 $a_{11}^{(2)}$ 加权。而项 $a_{12}^{(1)}y_{2,t-1}$ 和 $a_{12}^{(2)}y_{2,t-2}$ 则描述了信号 $y_2$ 的过去对信号 $y_1$ 现在的影响，这些交叉滞后效应由非对角系数 $a_{12}^{(1)}$ 和 $a_{12}^{(2)}$ 编码。同理，在第二个方程中，系数 $a_{21}^{(1)}$ 和 $a_{21}^{(2)}$ 编码了从 $y_1$ 到 $y_2$ 的交叉滞后影响。

因此，在 VAR 框架下，所有编码交叉滞后（即信道间）影响的系数都位于系数矩阵 $A_i$ 的**非对角线**位置。具体而言，系数 $a_{ij}^{(p)}$ 量化了变量 $j$ 在 $p$ 个时间步之前的值 ($y_{j, t-p}$) 对变量 $i$ 当前值 ($y_{i, t}$) 的线性影响。

#### 使用[滞后算子](@entry_id:266398)的紧凑表示

为了方便理论推导，使用**[滞后算子](@entry_id:266398)**（lag operator）$L$ 来表示 VAR 模型非常有用。[滞后算子](@entry_id:266398)作用于一个时间序列，将其时间索引向后移动一个单位，即 $L\mathbf{y}_t = \mathbf{y}_{t-1}$。其幂次则表示多次移位，例如 $L^k \mathbf{y}_t = \mathbf{y}_{t-k}$ 。

利用[滞后算子](@entry_id:266398)，VAR(p) 方程可以重写为：
$$
\mathbf{y}_t = A_1 L \mathbf{y}_t + A_2 L^2 \mathbf{y}_t + \dots + A_p L^p \mathbf{y}_t + \mathbf{c} + \boldsymbol{\varepsilon}_t
$$
将所有包含 $\mathbf{y}_t$ 的项移到左边：
$$
(I_k - A_1 L - A_2 L^2 - \dots - A_p L^p) \mathbf{y}_t = \mathbf{c} + \boldsymbol{\varepsilon}_t
$$
其中 $I_k$ 是 $k \times k$ 的[单位矩阵](@entry_id:156724)。括号内的部分是一个以[滞后算子](@entry_id:266398) $L$ 为变量、矩阵为系数的多项式，称为**矩阵滞后多项式**，记为 $A(L)$：
$$
A(L) = I_k - A_1 L - A_2 L^2 - \dots - A_p L^p
$$
于是，VAR(p) 过程可以非常简洁地表示为：
$$
A(L) \mathbf{y}_t = \mathbf{c} + \boldsymbol{\varepsilon}_t
$$
这种表示法在推导模型的稳定性和[脉冲响应函数](@entry_id:1126431)时至关重要。

### 新息过程

#### 新息的角色与性质

新息项 $\boldsymbol{\varepsilon}_t$ 在 VAR 模型中扮演着核心角色。从预测的角度看，$\boldsymbol{\varepsilon}_t$ 是基于过程过去所有信息对 $\mathbf{y}_t$ 进行最佳[线性预测](@entry_id:180569)后产生的**一步[预测误差](@entry_id:753692)** 。即，$\boldsymbol{\varepsilon}_t = \mathbf{y}_t - \mathbb{E}[\mathbf{y}_t | \mathbf{y}_{t-1}, \mathbf{y}_{t-2}, \dots]$。

根据均方预测中的**[正交性原理](@entry_id:153755)**，[预测误差](@entry_id:753692) $\boldsymbol{\varepsilon}_t$ 与用于预测的过去信息是正交的（即不相关）。由此可得新息过程的几个基本性质：
1.  **零均值**: 如果原始过程 $\mathbf{y}_t$ 是零均值或已经中心化，则 $\mathbb{E}[\boldsymbol{\varepsilon}_t] = \mathbf{0}$。
2.  **序列不相关**: $\boldsymbol{\varepsilon}_t$ 与其自身的任何过去值都不相关，即 $\mathbb{E}[\boldsymbol{\varepsilon}_t \boldsymbol{\varepsilon}_{s}'] = \mathbf{0}$ 对所有 $s \neq t$ 成立。这就是所谓的**[白噪声](@entry_id:145248)**过程。
3.  **有限协方差**: 新息具有一个有限的、正定的同期[协方差矩阵](@entry_id:139155) $\boldsymbol{\Sigma}_{\varepsilon} = \mathbb{E}[\boldsymbol{\varepsilon}_t \boldsymbol{\varepsilon}_t']$。

在实践中，除了这些基本要求，通常还会做出一些额外假设。例如，为了进行最大似然估计和精确的有限样本统计检验，常假设新息服从[多元正态分布](@entry_id:175229)，即 $\boldsymbol{\varepsilon}_t \sim \mathcal{N}(\mathbf{0}, \boldsymbol{\Sigma}_{\varepsilon})$。然而，对于模型参数的普通最小二乘 (OLS) 估计的**一致性**而言，[正态性假设](@entry_id:170614)并非必要条件。只要新息是序列不相关的白噪声，且与作为回归量的过去观测值不相关，OLS 估计量就是一致的 。

#### 新息[协方差矩阵](@entry_id:139155) ($\Sigma_{\varepsilon}$)

新息协方差矩阵 $\boldsymbol{\Sigma}_{\varepsilon}$ 捕捉了在同一时间点 $t$ 上，模型未能被过去信息解释的部分之间的相关性 。其非对角元素 $(\boldsymbol{\Sigma}_{\varepsilon})_{ij}$ 量化了新息分量 $\varepsilon_{i,t}$ 和 $\varepsilon_{j,t}$ 之间的**同期相关性**（contemporaneous correlation）。

重要的是要将这种同期相关性与交叉滞后效应（由 $A_i$ 矩阵的非对角元素编码）区分开来。
- **$A_i$ 的非对角元素**：描述了一个变量的**过去**如何影响另一个变量的**现在**。这是有向、有延迟的动态交互，是格兰杰因果关系的基础。
- **$\boldsymbol{\Sigma}_{\varepsilon}$ 的非对角元素**：描述了在同一时刻，冲击到不同变量的新息之间的相关性。这是一种瞬时关系，可能源于模型未包含的、作用速度快于采样率的共同驱动因素，或变量间的直接瞬时物理联系。

例如，即使系统没有格兰杰因果关系（所有 $A_i$ 矩阵都是对角的），非对角的 $\boldsymbol{\Sigma}_{\varepsilon}$ 仍然意味着系统各部分会同时受到相关的随机扰动。反之，即使新息是完全不相关的（$\boldsymbol{\Sigma}_{\varepsilon}$ 是对角的），非对角的 $A_i$ 矩阵仍然会通过滞后效应在观测序列 $\mathbf{y}_t$ 中产生复杂的同期相关性 。因此，观测数据的同期相关性是由滞后动态和新息相关性共同决定的。

### [模型稳定性](@entry_id:636221)与平稳性

#### 稳定性的概念

一个 VAR 过程的**稳定性**（stability）是一个至关重要的属性。一个稳定的过程是**协方差平稳**的，意味着其均值、方差和协方差不随时间变化。从动态角度看，稳定性保证了系统对冲击的响应是暂时的，不会无限放大。换句话说，任何一次性的扰动（如一次新息冲击）的影响会随着时间的推移而衰减至零。在神经生理学上，这符合生物物理约束，即一个短暂的外部刺激不应导致神经活动无限制地增长 。

#### [伴随矩阵](@entry_id:148203)与稳定性条件

对于一个 VAR(p) 模型，其稳定性由系数矩阵 $\{A_i\}_{i=1}^p$ 完全决定。检验稳定性的标准方法是将其转换为一个等价的 VAR(1) 形式，即**[伴随形式](@entry_id:747524)**（companion form）。

定义一个 $kp \times 1$ 的[状态向量](@entry_id:154607) $S_t = (\mathbf{y}_t', \mathbf{y}_{t-1}', \dots, \mathbf{y}_{t-p+1}')'$。这个增广向量的动态可以表示为一个[一阶差分](@entry_id:275675)方程：
$$
S_t = F S_{t-1} + G \boldsymbol{\varepsilon}_t
$$
其中，$F$ 是 $kp \times kp$ 的**[伴随矩阵](@entry_id:148203)**：
$$
F = \begin{pmatrix}
A_1 & A_2 & \cdots & A_{p-1} & A_p \\
I_k & 0 & \cdots & 0 & 0 \\
0 & I_k & \cdots & 0 & 0 \\
\vdots & \vdots & \ddots & \vdots & \vdots \\
0 & 0 & \cdots & I_k & 0
\end{pmatrix}
$$
而 $G$ 是一个将新息 $\boldsymbol{\varepsilon}_t$ 嵌入[状态空间](@entry_id:160914)的矩阵。

系统的动态行为现在由矩阵 $F$ 的幂次 $F^h$ 控制。为了使过去状态的影响随时间衰减，即 $\lim_{h \to \infty} F^h = 0$，一个标准的线性代数结论是，矩阵 $F$ 的所有**特征值**的模（modulus）必须严格小于 1。

因此，VAR(p) 过程的**稳定性条件**是：其[伴随矩阵](@entry_id:148203) $F$ 的所有特征值的模都严格小于 1 。

这个条件等价于[特征多项式](@entry_id:150909) $\det(I_k - A_1 z - A_2 z^2 - \dots - A_p z^p) = 0$ 的所有复数根 $z$ 的模都严格大于 1。满足稳定性条件的 VAR 过程保证存在一个唯一的、具有绝对可加和脉冲响应序列的因果移动平均表示。

### 关键应用与解释工具

#### [脉冲响应函数](@entry_id:1126431) (IRF)

一旦拟合了稳定的 VAR 模型，一个核心的解释工具就是**[脉冲响应函数](@entry_id:1126431) (IRF)**。IRF 描述了在一个变量上施加一个一次性的、单位大小的冲击后，对系统内所有变量未来路径产生的动态影响。

在数学上，任何稳定的 VAR(p) 过程都可以表示为一个无穷阶的[向量移动平均](@entry_id:139987) (VMA($\infty$)) 过程，也称为其 **Wold 表示**：
$$
\mathbf{y}_t - \boldsymbol{\mu} = \sum_{h=0}^{\infty} \Psi_h \boldsymbol{\varepsilon}_{t-h}
$$
其中 $\boldsymbol{\mu}$ 是过程的均值，而 $\Psi_h$ 是 $k \times k$ 的矩阵序列，即[脉冲响应函数](@entry_id:1126431) 。这些矩阵可以通过 VAR [系数矩阵](@entry_id:151473)递归计算得出：
- $\Psi_0 = I_k$
- $\Psi_h = \sum_{i=1}^{p} A_i \Psi_{h-i}$ 对于 $h \ge 1$（约定当 $h  0$ 时 $\Psi_h = 0$）

$\Psi_h$ 矩阵的第 $(i, j)$ 个元素 $(\Psi_h)_{ij}$ 的解释是：在时间点 $t$ 对第 $j$ 个变量的新息 $\varepsilon_{j,t}$ 施加一个单位冲击，对时间点 $t+h$ 的第 $i$ 个变量的[期望值](@entry_id:150961) $y_{i,t+h}$ 产生的[边际效应](@entry_id:634982)，同时保持所有其他过去、现在和未来的冲击为零。IRF 描绘了冲击在系统中传播和衰减的完整轨迹，为理解[神经回路](@entry_id:169301)的动态响应特性提供了定量描述。

#### 格兰杰因果关系 (Granger Causality)

VAR 模型最著名的应用之一是检验**格兰杰因果关系**。这一概念基于预测，其核心思想是：如果变量 $X$ 的过去值能够帮助预测变量 $Z$ 的未来值，且这种帮助超出了仅使用 $Z$ 自身过去值进行预测所能达到的效果，那么我们称 $X$ 是 $Z$ 的格兰杰原因。

在 VAR 框架内，这个概念可以被精确地形式化 。考虑一个包含两个子系统 $\mathbf{x}_t$ 和 $\mathbf{z}_t$（以及可能存在的其他变量 $\mathbf{w}_t$）的 VAR 模型。我们想检验“$\mathbf{x}$ 不是 $\mathbf{z}$ 的格兰杰原因（以 $\mathbf{w}$ 为条件）”这一零假设。这个[零假设](@entry_id:265441)等价于：
$$
\mathbb{E}[\mathbf{z}_t | \{\mathbf{x}_{s}, \mathbf{z}_{s}, \mathbf{w}_{s}\}_{s  t}] = \mathbb{E}[\mathbf{z}_t | \{\mathbf{z}_{s}, \mathbf{w}_{s}\}_{s  t}]
$$
即在预测 $\mathbf{z}_t$ 时，知道 $\mathbf{x}$ 的过去并不能提供额外的信息。

在 VAR(p) 模型中，这个预测问题转化为对系数矩阵的约束。将每个 $A_{\ell}$ 矩阵按照 $(\mathbf{x}, \mathbf{z}, \mathbf{w})$ 进行分块：
$$
A_{\ell} = \begin{bmatrix} A^{xx}_{\ell}  A^{xz}_{\ell}  A^{xw}_{\ell} \\ A^{zx}_{\ell}  A^{zz}_{\ell}  A^{zw}_{\ell} \\ A^{wx}_{\ell}  A^{wz}_{\ell}  A^{ww}_{\ell} \end{bmatrix}
$$
描述 $\mathbf{z}_t$ 的方程组为：
$$
\mathbf{z}_t = \sum_{\ell=1}^{p} (A^{zx}_{\ell} \mathbf{x}_{t-\ell} + A^{zz}_{\ell} \mathbf{z}_{t-\ell} + A^{zw}_{\ell} \mathbf{w}_{t-\ell}) + \mathbf{u}^z_t
$$
$\mathbf{x}$ 的过去值能否帮助预测 $\mathbf{z}_t$，完全取决于系数块 $A^{zx}_{\ell}$ 是否为零。因此，“$\mathbf{x}$ 不是 $\mathbf{z}$ 的格兰杰原因”的零假设等价于对所有滞后 $\ell=1, \dots, p$，都有 $A^{zx}_{\ell} = \mathbf{0}$。这可以通过标准的统计检验（如 Wald 检验）来评估。

#### 从简约型到结构型 VAR (SVAR)

我们目前讨论的模型被称为**简约型 VAR**（reduced-form VAR），其新息 $\boldsymbol{\varepsilon}_t$ 是[预测误差](@entry_id:753692)，其分量之间可能存在同期相关性（即 $\boldsymbol{\Sigma}_{\varepsilon}$ 非对角）。然而，为了做出更具因果解释力的推断，研究者常常对系统中更“基本”的、[相互独立](@entry_id:273670)的驱动力感兴趣。

**结构型 VAR (SVAR)** 模型旨在揭示这些潜在的驱动力。它通过引入一个额外的矩阵 $B$ 来描述变量间的瞬时因果关系 ：
$$
B \mathbf{y}_t = \mathbf{c} + \sum_{i=1}^p A_i^* \mathbf{y}_{t-i} + u_t
$$
这里的 $u_t$ 是**[结构性冲击](@entry_id:136585)**（structural shocks），关键假设是它们相互正交（不相关），即其协方差矩阵 $\Sigma_u = \mathbb{E}[u_t u_t']$ 是一个对角矩阵。$B$ 矩阵的非对角元素描述了变量间的瞬时影响。

通过对 SVAR 方程左乘 $B^{-1}$，可以得到其对应的简约型 VAR：
$$
\mathbf{y}_t = B^{-1}\mathbf{c} + \sum_{i=1}^p (B^{-1}A_i^*) \mathbf{y}_{t-i} + B^{-1}u_t
$$
比较可知，简约型新息 $\boldsymbol{\varepsilon}_t = B^{-1}u_t$，其[协方差矩阵](@entry_id:139155)为 $\boldsymbol{\Sigma}_{\varepsilon} = B^{-1} \Sigma_u (B^{-1})'$。这个关系 $B \boldsymbol{\Sigma}_{\varepsilon} B' = \Sigma_u$ 是连接可估计的简约型模型和不可直接观测的结[构型模型](@entry_id:747676)的桥梁。

然而，仅从数据中估计出的 $\boldsymbol{\Sigma}_{\varepsilon}$ 不足以唯一确定 $B$ 和 $\Sigma_u$。这就是所谓的 **SVAR 识别问题**。为了唯一地确定[结构性冲击](@entry_id:136585)，必须施加额外的约束，例如，假设 $B$ 是一个下[三角矩阵](@entry_id:636278)（即施加一个递归的瞬时因果顺序，称为 Cholesky 分解）。这些约束应基于具体的理论或先验知识。

### 模型构建中的实践考量

#### 选择模型阶数 (p)

在应用 VAR 模型时，一个关键的实践步骤是选择合适的滞后阶数 $p$。这是一个典型的**偏差-方差权衡**问题：
- 如果 $p$太小，模型可能无法捕捉系统的全部动态，导致模型设定不当和有偏估计。
- 如果 $p$ 太大，模型会包含许多不必要的参数，导致估计方差增大和预测精度下降。

选择 $p$ 的常用方法是使用**信息准则**（information criteria）。这些准则在模型的[拟合优度](@entry_id:176037)（由[似然函数](@entry_id:921601)或残差协方差的行列式度量）和[模型复杂度](@entry_id:145563)（由参数数量度量）之间进行权衡。对于一个包含 $q(p) = k^2 p + k$ 个参数的 $k$ 维 VAR(p) 模型（$k^2p$ 个自[回归系数](@entry_id:634860)和 $k$ 个截距项），常用的[信息准则](@entry_id:635818)包括 ：

- **[赤池信息准则 (AIC)](@entry_id:193149)**:
  $$
  \mathrm{AIC}(p) = \ln|\hat{\Sigma}_p| + \frac{2}{T} q(p)
  $$
- **[贝叶斯信息准则 (BIC)](@entry_id:181959)** 或 **施瓦茨准则 (SC)**:
  $$
  \mathrm{BIC}(p) = \ln|\hat{\Sigma}_p| + \frac{\ln(T)}{T} q(p)
  $$
- **汉南-奎因准则 (HQ)**:
  $$
  \mathrm{HQ}(p) = \ln|\hat{\Sigma}_p| + \frac{2\ln(\ln(T))}{T} q(p)
  $$
其中 $\hat{\Sigma}_p$ 是模型阶数为 $p$ 时的残差[协方差矩阵](@entry_id:139155)的估计，T 是[有效样本量](@entry_id:271661)。

这些准则的惩罚项各不相同。BIC 的惩罚最重，倾向于选择更简约的模型；AIC 的惩罚最轻；HQ 介于两者之间。在实践中，通常会计算一系列候选 $p$ 值的这些准则，并选择使准则值最小的 $p$。