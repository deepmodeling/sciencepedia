## 引言
[非线性系统](@entry_id:168347)无处不在，从机器人的运动到[化学反应](@entry_id:146973)的进程，再到流行病的传播，它们的动态行为往往复杂且难以预测。与线性系统不同，我们无法简单地应用叠加原理来分析或控制它们。然而，在工程与科学实践中，我们常常更关心系统在特定工作状态（如稳定飞行或[稳态](@entry_id:182458)生产）附近的表现。这为我们提供了一个关键的切入点：利用线性化技术，将一个棘手的[非线性](@entry_id:637147)问题转化为一个我们拥有成熟理论工具的线性问题。线性化不仅是一种数学近似，更是一种深刻的工程思想，是驾驭复杂性的基石。

本文旨在系统性地介绍非线性[模型的线性化](@entry_id:751300)方法，解决如何对复杂的非线性系统进行局部分析与控制这一核心问题。通过本文的学习，你将掌握从基本原理到高级应用的完整知识体系。

- 在 **“原理与机制”** 一章中，我们将深入探讨线性化的数学基础，学习如何通过[泰勒展开](@entry_id:145057)和雅可比矩阵，围绕[平衡点](@entry_id:272705)推导出线性近似模型，并分析其有效性与局限性。
- 在 **“应用与交叉学科联系”** 一章中，我们将展示线性化如何在[控制系统设计](@entry_id:273663)、状态估计（如[扩展卡尔曼滤波器](@entry_id:199333)）、机器人学、航空航天乃至生命科学等多个领域中发挥关键作用，连接理论与实践。
- 最后，在 **“动手实践”** 部分，你将通过一系列精心设计的计算和分析练习，巩固所学知识，将理论应用于具体问题。

让我们从线性化的基本原理开始，揭开分析[非线性](@entry_id:637147)世界的强大工具。

## 原理与机制

在对非线性系统进行分析与控制时，我们面临的主要挑战源于其固有的复杂性。与线性系统不同，[非线性系统](@entry_id:168347)的行为无法简单地通过[叠加原理](@entry_id:144649)来预测。然而，在许多工程应用中，我们常常关注系统在某个特定工作状态附近的动态行为。幸运的是，光滑的[非线性](@entry_id:637147)函数在局部上可以被线性函数很好地近似。这一深刻的数学思想构成了**线性化 (linearization)** 的基石，它是一种强大而基础的技术，允许我们将丰富的[线性系统理论](@entry_id:172825)工具应用于分析[非线性](@entry_id:637147)现象的局部特性。本章旨在深入探讨线性化的基本原理、实施机制、[适用范围](@entry_id:636189)及其在更高级概念中的扩展。

### 基本原理：通过[泰勒展开](@entry_id:145057)进行线性化

线性化的核心思想是利用函数在一点的一阶[泰勒展开](@entry_id:145057)来近似该函数在该点邻域内的行为。对于一个由[常微分方程](@entry_id:147024)描述的非[线性动力系统](@entry_id:150282)，其通用状态空间形式为：

$$
\begin{align*}
\dot{x} = f(x, u) \\
y = h(x, u)
\end{align*}
$$

其中，$x \in \mathbb{R}^n$ 是[状态向量](@entry_id:154607)，$u \in \mathbb{R}^m$ 是输入向量，$y \in \mathbb{R}^p$ 是输出向量。函数 $f: \mathbb{R}^n \times \mathbb{R}^m \to \mathbb{R}^n$ 和 $h: \mathbb{R}^n \times \mathbb{R}^m \to \mathbb{R}^p$ 分别描述了系统的状态动态和输出映射，我们假设它们是连续可微的（至少是 $C^1$ 类函数）。

#### 工作点的概念

我们不能在任意一点上随意进行线性化。为了得到一个具有明确物理意义且数学上简洁的[线性模型](@entry_id:178302)，我们需要围绕一个**[工作点](@entry_id:173374) (operating point)** 或**[平衡点](@entry_id:272705) (equilibrium point)** 进行展开。一个时间不变的[工作点](@entry_id:173374) $(x^\star, u^\star)$ 被定义为一个常数状态 $x^\star$ 和常数输入 $u^\star$ 的组合，在该输入下，系统状态不再随时间变化。从数学上讲，这意味着状态的时间导数为零 [@problem_id:2720600]。

$$
\dot{x} = f(x^\star, u^\star) = 0
$$

这个条件至关重要。它确保了当我们分析系统对微小扰动的响应时，系统本身没有一个内在的“漂移”或恒定的变化趋势。满足此条件的点 $(x^\star, u^\star)$ 构成了系统的[稳态](@entry_id:182458)。相应的[稳态](@entry_id:182458)输出则自然地定义为 $y^\star = h(x^\star, u^\star)$。

#### 线性化模型的推导

为了研究系统在[平衡点](@entry_id:272705) $(x^\star, u^\star)$ 附近的动态，我们引入**扰动变量 (perturbation variables)**，它们表示系统的当前状态、输入和输出与相应平衡值的偏差：

$$
\begin{align*}
\delta x(t) = x(t) - x^\star \\
\delta u(t) = u(t) - u^\star \\
\delta y(t) = y(t) - y^\star
\end{align*}
$$

由于 $x^\star$ 是一个常数向量，我们有 $\dot{x}(t) = \frac{d}{dt}(x^\star + \delta x(t)) = \dot{\delta x}(t)$。将这些关系代入原始的状态方程，得到：

$$
\dot{\delta x} = f(x^\star + \delta x, u^\star + \delta u)
$$

现在，我们在[平衡点](@entry_id:272705) $(x^\star, u^\star)$ 处对函数 $f$ 进行一阶泰勒展开。由于 $f$ 是 $C^1$ 函数，这种展开是有效的：

$$
f(x, u) \approx f(x^\star, u^\star) + \left.\frac{\partial f}{\partial x}\right|_{(x^\star, u^\star)}(x - x^\star) + \left.\frac{\partial f}{\partial u}\right|_{(x^\star, u^\star)}(u - u^\star)
$$

将扰动变量代入，并利用[平衡点](@entry_id:272705)定义 $f(x^\star, u^\star) = 0$，我们得到扰动状态的近似动态方程 [@problem_id:2909775]：

$$
\dot{\delta x} \approx A \delta x + B \delta u
$$

其中，矩阵 $A$ 和 $B$ 是函数 $f$ 对状态 $x$ 和输入 $u$ 的**雅可比矩阵 (Jacobian matrices)**，并在[平衡点](@entry_id:272705)处求值：

$$
A = \left.\frac{\partial f}{\partial x}\right|_{(x^\star, u^\star)}, \qquad B = \left.\frac{\partial f}{\partial u}\right|_{(x^\star, u^\star)}
$$

通过完全相同的过程，我们可以对输出方程 $y = h(x, u)$ 进行线性化。从 $\delta y = y - y^\star = h(x^\star + \delta x, u^\star + \delta u) - h(x^\star, u^\star)$ 出发，[泰勒展开](@entry_id:145057)给出：

$$
h(x^\star + \delta x, u^\star + \delta u) \approx h(x^\star, u^\star) + \left.\frac{\partial h}{\partial x}\right|_{(x^\star, u^\star)}\delta x + \left.\frac{\partial h}{\partial u}\right|_{(x^\star, u^\star)}\delta u
$$

因此，扰动输出方程为：

$$
\delta y \approx C \delta x + D \delta u
$$

其中，$C$ 和 $D$ 同样是在[平衡点](@entry_id:272705)处求值的[雅可比矩阵](@entry_id:264467)：

$$
C = \left.\frac{\partial h}{\partial x}\right|_{(x^\star, u^\star)}, \qquad D = \left.\frac{\partial h}{\partial u}\right|_{(x^\star, u^\star)}
$$

最终，我们得到了描述扰动变量动态的**[线性时不变 (LTI) 系统](@entry_id:178866)**：

$$
\begin{align*}
\dot{\delta x} = A \delta x + B \delta u \\
\delta y = C \delta x + D \delta u
\end{align*}
$$

这个[线性模型](@entry_id:178302)是分析和控制原始[非线性系统](@entry_id:168347)在[平衡点](@entry_id:272705)附近行为的出发点。它是一个近似模型，其有效性取决于扰动 $(\delta x, \delta u)$ 的“小”程度。

### 雅可比矩阵的计算机制

线性化过程的核心是计算 $A, B, C, D$ 这四个雅可比矩阵。这本质上是一个多元微积分的练习，但其中蕴含着对系统结构的深刻洞察。

#### 直接计算

最直接的方法是逐项计算[偏导数](@entry_id:146280)。考虑一个具体的[非线性系统](@entry_id:168347) [@problem_id:2909775]：

$$
\begin{aligned}
\dot{x}_{1} = -2 x_{1} + \sin(x_{2}) + u \\
\dot{x}_{2} = x_{1}^{2} - x_{2} + u^{3} \\
y = x_{1} + x_{2}^{2}
\end{aligned}
$$

系统在原点 $(x_e, u_e) = ((0,0)^\top, 0)$ 处有一个[平衡点](@entry_id:272705)。我们来计算雅可比矩阵：

$A = \left.\frac{\partial f}{\partial x}\right|_{(0,0)} = \left.\begin{pmatrix} \frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} \\ \frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2} \end{pmatrix}\right|_{(0,0)} = \left.\begin{pmatrix} -2 & \cos(x_2) \\ 2x_1 & -1 \end{pmatrix}\right|_{(0,0)} = \begin{pmatrix} -2 & 1 \\ 0 & -1 \end{pmatrix}$

$B = \left.\frac{\partial f}{\partial u}\right|_{(0,0)} = \left.\begin{pmatrix} \frac{\partial f_1}{\partial u} \\ \frac{\partial f_2}{\partial u} \end{pmatrix}\right|_{(0,0)} = \left.\begin{pmatrix} 1 \\ 3u^2 \end{pmatrix}\right|_{(0,0)} = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$

$C = \left.\frac{\partial h}{\partial x}\right|_{(0,0)} = \left.\begin{pmatrix} \frac{\partial h}{\partial x_1} & \frac{\partial h}{\partial x_2} \end{pmatrix}\right|_{(0,0)} = \left.\begin{pmatrix} 1 & 2x_2 \end{pmatrix}\right|_{(0,0)} = \begin{pmatrix} 1 & 0 \end{pmatrix}$

$D = \left.\frac{\partial h}{\partial u}\right|_{(0,0)} = \left.\frac{\partial}{\partial u}(x_1 + x_2^2)\right|_{(0,0)} = 0$

于是，在原点附近的线性化模型为：

$$
\begin{aligned}
\dot{\delta x} = \begin{pmatrix} -2 & 1 \\ 0 & -1 \end{pmatrix} \delta x + \begin{pmatrix} 1 \\ 0 \end{pmatrix} \delta u \\
\delta y = \begin{pmatrix} 1 & 0 \end{pmatrix} \delta x
\end{aligned}
$$

#### 复合函数与[链式法则](@entry_id:190743)

在更复杂的系统中，输入或状态可能通过一个或多个静态[非线性](@entry_id:637147)函数影响系统动态。在这种情况下，必须正确应用**链式法则**。例如，考虑一个形如 $\dot{x} = f(x, \phi(u))$ 的系统，其中 $\phi$ 是一个静态[非线性映射](@entry_id:272931) [@problem_id:2720562]。输入矩阵 $B$ 的计算需要对复合函数 $g(u) = f(x^\star, \phi(u))$ 关于 $u$ 求导。

设 $v = \phi(u)$，则根据[链式法则](@entry_id:190743)：

$$
B = \left.\frac{d}{du} f(x^\star, \phi(u))\right|_{u=u^\star} = \left.\frac{\partial f}{\partial v}\right|_{(x^\star, v^\star)} \cdot \left.\frac{d\phi}{du}\right|_{u=u^\star}
$$

其中 $v^\star = \phi(u^\star)$。这表明 $B$ 矩阵是两个灵敏度的乘积：系统动态对中间变量 $v$ 的灵敏度，以及中间变量 $v$ 对实际输入 $u$ 的灵敏度。忽略这种结构会导致错误的[线性模型](@entry_id:178302)。

#### 直接馈通项 (D) 的物理意义

矩阵 $D$ 被称为**直接馈通 (direct feedthrough)** 或**前馈**矩阵。它描述了输入 $u$ 对输出 $y$ 的瞬时、代数效应。当 $D \ne 0$ 时，输入的变化会立刻反映在输出上，而无需通过系统状态的动态演化。

线性化模型中是否存在直接馈通，取决于输出函数 $h(x, u)$ 在[工作点](@entry_id:173374)处对输入 $u$ 的[偏导数](@entry_id:146280)是否为零 [@problem_id:2720606]。即，当且仅当 $D = \left.\frac{\partial h}{\partial u}\right|_{(x^\star, u^\star)} = 0$ 时，线性化模型没有直接馈通。

值得注意的是，$\left.\frac{\partial h}{\partial u}\right|_{(x^\star, u^\star)} = 0$ 并不意味着函数 $h$ 在全局上与 $u$ 无关。例如，若 $h(u) = u^2$ 且工作点为 $u^\star = 0$，则 $D = \left.2u\right|_{u=0} = 0$。尽管 $h$ 显然依赖于 $u$，但在该特定工作点，输出对输入的**一阶灵敏度**为零，因为该点是函数的[驻点](@entry_id:136617)。

### 线性近似的局部有效性与分析

线性化模型本质上是一个局部近似。理解这个近似的质量和其有效的范围，对于可靠地应用线性化至关重要。

#### 数学基础与[误差界](@entry_id:139888)定

线性化模型的存在性和误差特性取决于[非线性](@entry_id:637147)函数 $f$ 和 $h$ 的光滑性。

- **存在性**: [雅可比矩阵](@entry_id:264467)的存在性，即 $f$ 和 $h$ 的弗雷歇导数 (Fréchet derivative) 的存在性，是进行线性化的基本前提。一个充分条件是 $f$ 和 $h$ 在[工作点](@entry_id:173374)的一个邻域内是**连续可微的 ($C^1$)** [@problem_id:2720583]。在此条件下，[泰勒展开](@entry_id:145057)的余项 $r(\delta x, \delta u)$ 是关于扰动范数 $\|(\delta x, \delta u)\|$ 的高阶无穷小，记作 $o(\|(\delta x, \delta u)\|)$。这意味着当扰动趋于零时，误差比扰动本身更快地趋于零。

- **误差阶数**: 如果我们要求更强的[误差界](@entry_id:139888)定，例如一个二次界 $\mathcal{O}(\|(\delta x, \delta u)\|^2)$，则需要更强的光滑性条件。如果 $f$ 和 $h$ 是**二次连续可微的 ($C^2$)**，[泰勒定理](@entry_id:144253)保证了[余项](@entry_id:159839)可以被扰动范数的平方所约束。这对于某些[鲁棒控制](@entry_id:260994)和估计问题的严格分析至关重要 [@problem_id:2720583]。

#### 定义有效区域

“小扰动”这个概念虽然直观，但在工程上不够精确。我们可以量化地定义一个**有效区域 (region of validity)**，在该区域内，[线性模型](@entry_id:178302)是“足够好”的近似。一种实用的方法是要求[非线性](@entry_id:637147)余项的大小相对于线性项的大小保持在一个可接受的比例之下 [@problem_id:2720579]。

考虑[自治系统](@entry_id:173841) $\dot{x} = f(x)$，其线性化为 $\dot{\tilde{x}} = A \tilde{x} + r(\tilde{x})$。我们可以定义[线性模型](@entry_id:178302)的主导性条件为：

$$
\|r(\tilde{x})\| \le \varepsilon \|A \tilde{x}\|
$$

其中 $\varepsilon \in (0,1)$ 是一个小的容差。如果我们知道[余项](@entry_id:159839) $r(\tilde{x})$ 的二次[上界](@entry_id:274738)，例如 $\|r(\tilde{x})\| \le \frac{1}{2} \tilde{x}^\top H \tilde{x}$（其中 $H$ 是一个[半正定矩阵](@entry_id:155134)，其大小与 $f$ 的[二阶导数](@entry_id:144508)相关），并且知道 $A$ 的最小奇异值 $\sigma_{\min}(A)$（它给出了 $\|A\tilde{x}\|$ 的下界），我们就可以导出一个保证上述条件成立的扰动半径 $r$：

$$
r \le \frac{2 \varepsilon \sigma_{\min}(A)}{\lambda_{\max}(H)}
$$

其中 $\lambda_{\max}(H)$ 是 $H$ 的最大[特征值](@entry_id:154894)。这个结果为“局部”提供了一个具体的、可计算的范围，是连接理论与实践的重要桥梁。

#### 线性化与局部可观测性

线性化的威力体现在它可以将[线性系统理论](@entry_id:172825)的各种概念（如[可控性](@entry_id:148402)、可观测性）应用于非线性系统的局部分析。一个系统的**可观测性 (observability)** 关系到我们能否通过测量输出 $y$ 来唯一确定系统的内部状态 $x$。对于非线性系统，[可观测性](@entry_id:152062)可能依赖于系统所处的状态。

考虑一个倒立摆，其角度 $x_1$ 的测量是通过一个[非线性](@entry_id:637147)传感器 $y = \sin(x_1)$ 实现的 [@problem_id:2720575]。该系统的输出雅可比矩阵 $C(\hat{x})$ 在任意估计点 $\hat{x} = (\hat{x}_1, \hat{x}_2)^\top$ 处为 $C(\hat{x}) = \begin{pmatrix} \cos(\hat{x}_1) & 0 \end{pmatrix}$。

为了分析局部可观测性，我们构造线性化系统的[可观测性矩阵](@entry_id:165052) $\mathcal{O}(\hat{x}) = \begin{pmatrix} C(\hat{x}) \\ C(\hat{x})A(\hat{x}) \end{pmatrix}$。计算表明，该矩阵的行列式为 $\det(\mathcal{O}(\hat{x})) = \cos^2(\hat{x}_1)$。

当 $\det(\mathcal{O}(\hat{x})) = 0$ 时，线性化系统失去[可观测性](@entry_id:152062)。这发生在 $\cos(\hat{x}_1) = 0$，即 $\hat{x}_1 = \frac{\pi}{2} + k\pi$（摆处于水平位置）。物理直觉与此完全吻合：在这些点，$\sin(x_1)$ 函数达到其极值，其斜率为零。因此，输出 $y$ 对角度 $x_1$ 的微小变化变得一阶不敏感，使得我们无法从输出的微小变化中推断出状态的微小变化，从而导致局部可观测性的丧失。

### 超越[平衡点](@entry_id:272705)：线性化的局限与扩展

尽管线性化功能强大，但其应用范围是有限的。当系统行为不能由其一阶近似主导时，或当关注的对象不是一个固定的[平衡点](@entry_id:272705)时，我们需要更精细的工具。

#### 非[双曲平衡点](@entry_id:165723)：线性化失效之时

**Lyapunov 间接法**（或称线性化原理）指出：如果一个[非线性系统](@entry_id:168347)在[平衡点](@entry_id:272705)处的线性化矩阵 $A$ 的所有[特征值](@entry_id:154894)都具有非零实部（即[平衡点](@entry_id:272705)是**双曲的 (hyperbolic)**），那么[非线性系统](@entry_id:168347)在该[平衡点](@entry_id:272705)附近的[局部稳定性](@entry_id:751408)与线性化系统完全相同。

然而，当矩阵 $A$ 存在一个或多个[特征值](@entry_id:154894)的实部为零时，[平衡点](@entry_id:272705)是**非双曲的 (non-hyperbolic)**，此时线性化方法失效。稳定性将由被忽略的**高阶[非线性](@entry_id:637147)项**决定。

考虑一个平面系统 [@problem_id:2720587]：
$$
\begin{aligned}
\dot{x} = -y - \alpha x (x^2+y^2) \\
\dot{y} = x - \alpha y (x^2+y^2)
\end{aligned}
$$
其在原点的线性化矩阵为 $A = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix}$，[特征值](@entry_id:154894)为 $\pm i$。这是一个典型的非双曲情况。线性化模型预示着一个中性稳定的中心，但我们无法断定原始[非线性系统](@entry_id:168347)的行为。通过分析极坐标下的径向动态，可以精确地得到 $\dot{r} = -\alpha r^3$。这表明，当 $\alpha > 0$ 时，三次项是耗散的，系统实际上是局部[渐近稳定](@entry_id:168077)的（螺线汇点）；当 $\alpha  0$ 时，三次项是反耗散的，系统是局部不稳定的（螺线源）。线性化完全忽略了决定系统命运的关键三次项。

在控制设计中，这种失效尤为关键。对于系统 $\dot{x}_1 = x_2, \dot{x}_2 = -x_1^3 + u$ [@problem_id:2721954]，其在原点的线性化为 $\dot{x}_1=x_2, \dot{x}_2=0$，是一个具有两个零[特征值](@entry_id:154894)的双重[积分器](@entry_id:261578)。任何基于这个（不完全的）线性模型的[控制器设计](@entry_id:274982)都可[能效](@entry_id:272127)果不佳或完全失败。正确的控制策略必须利用[非线性](@entry_id:637147)信息，例如，通过构造一个包含“能量”项 $\frac{1}{4}x_1^4$ 的**控制 Lyapunov 函数 (Control Lyapunov Function, CLF)**，来明确地利用 $-x_1^3$ 这一稳定化项。

#### 围绕轨[迹的线性](@entry_id:199170)化：周期轨道

线性化的思想还可以从[固定点](@entry_id:156394)扩展到围绕一条参考轨迹。一个特别重要的例子是**[周期轨道](@entry_id:275117) (periodic orbit)** 或**极限环 (limit cycle)**。对于一个周期为 $T_0$ 的[轨道](@entry_id:137151) $\Gamma$，我们无法定义一个固定的[平衡点](@entry_id:272705)。取而代之，我们引入**[庞加莱映射](@entry_id:269710) (Poincaré map)** 的概念。

我们选择一个与[轨道](@entry_id:137151)横向相交的[截面](@entry_id:154995) $\Sigma$。从 $\Sigma$ 上的一个点 $x_k$ 出发，系统轨迹将在一段时间后首次返回并与 $\Sigma$ 相交于一个新的点 $x_{k+1}$。这个从 $x_k$到 $x_{k+1}$ 的映射 $P: \Sigma \to \Sigma$ 就是[庞加莱映射](@entry_id:269710)。周期轨道 $\Gamma$ 与 $\Sigma$ 的交点 $x^\star$ 成为该映射的一个**[不动点](@entry_id:156394)**，即 $P(x^\star) = x^\star$。

[轨道](@entry_id:137151)的稳定性问题现在转化为[不动点](@entry_id:156394) $x^\star$ 对于离散映射 $P$ 的稳定性问题。我们可以像对[连续系统](@entry_id:178397)[平衡点](@entry_id:272705)那样，对映射 $P$ 在其[不动点](@entry_id:156394) $x^\star$ 处进行线性化 [@problem_id:2720593]：

$$
\delta x_{k+1} \approx DP(x^\star) \delta x_k
$$

其中 $DP(x^\star)$ 是[庞加莱映射](@entry_id:269710)在[不动点](@entry_id:156394)处的[雅可比矩阵](@entry_id:264467)。[轨道](@entry_id:137151) $\Gamma$ 的横向稳定性由矩阵 $DP(x^\star)$ 的[特征值](@entry_id:154894)（称为**[弗洛凯乘子](@entry_id:265040) (Floquet multipliers)**）决定。如果所有乘子的模都小于1，则[轨道](@entry_id:137151)是渐近稳定的。

例如，对于一个在[圆柱坐标系](@entry_id:266798)下描述的系统，其解表现为一个半径为 $r_0$、[角速度](@entry_id:192539)为 $\omega_0$ 的稳定旋转，同时在径向和 $z$ 轴方向上指数衰减。其[周期轨道](@entry_id:275117) $\Gamma$ 的庞加莱[映射的线性化](@entry_id:276268)雅可比矩阵可以被计算出来，其[特征值](@entry_id:154894)为 $e^{-k_r T_0}$ 和 $e^{-k_z T_0}$。因为 $k_r, k_z, T_0$ 均为正，这两个乘子的模都小于1，从而证明了该[周期轨道](@entry_id:275117)是指数稳定的 [@problem_id:2720593]。

总之，线性化是探索[非线性](@entry_id:637147)世界的一扇窗。尽管它的视野是局部的，但通过深刻理解其原理、机制、局限和扩展，我们能够将线性系统的严谨性和系统性方法应用于广泛而复杂的[非线性](@entry_id:637147)问题中。