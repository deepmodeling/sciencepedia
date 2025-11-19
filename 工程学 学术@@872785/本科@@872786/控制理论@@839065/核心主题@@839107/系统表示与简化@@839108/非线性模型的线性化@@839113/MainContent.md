## 引言
现实世界中的绝大多数物理、生物和工程系统，其动态行为本质上都是[非线性](@entry_id:637147)的。这些由复杂的非线性方程描述的系统，给直接分析和控制带来了巨大的挑战。为了应对这一难题，控制理论提供了一种基础而极其强大的工具——线性化。它允许我们用更简单、更易于理解的线性模型来近似复杂系统在特定运行状态下的局部行为，从而架起一座连接[非线性](@entry_id:637147)现实与成熟线性理论的桥梁。本文旨在系统地阐述线性化技术，解决如何将强大的线性分析与设计方法应用于实际[非线性系统](@entry_id:168347)的问题。

在接下来的内容中，你将首先深入学习“原理与机制”一章，掌握线性化的数学基础，即[泰勒级数展开](@entry_id:138468)和雅可比矩阵的计算，并理解如何围绕[平衡点](@entry_id:272705)构建线性状态空间模型。接着，在“应用与跨学科联系”一章中，你将看到线性化如何在工程、生物、经济乃至计算科学等多个领域中发挥关键作用。最后，通过“动手实践”部分的具体问题，你将有机会亲手应用所学知识，巩固对线性化过程的理解。让我们从深入探讨线性化的基本原理与数学机制开始。

## 原理与机制

在深入探讨[控制系统设计](@entry_id:273663)的复杂性之前，我们必须掌握一项基本而强大的技术：线性化。自然界和工程领域中的绝大多数系统，从天体运行的[轨道](@entry_id:137151)到[化学反应](@entry_id:146973)的进程，本质上都是[非线性](@entry_id:637147)的。它们的动态行为由复杂的[非线性微分方程](@entry_id:175929)描述，这使得精确分析和[控制器设计](@entry_id:274982)变得异常困难。然而，在许多实际应用中，我们常常只关心系统在某个特定工作点附近的动态特性。这正是线性化发挥关键作用的地方。

线性化的核心思想是用一个线性模型来近似一个非线性系统在某个特定[工作点](@entry_id:173374)（或轨迹）附近的局部行为。这种近似的威力在于，它为我们打开了[线性系统理论](@entry_id:172825)的宝库。一旦我们将系统近似为线性时不变（LTI）模型，我们就可以利用一系列成熟而强大的工具，例如通过分析[系统矩阵](@entry_id:172230)的[特征值](@entry_id:154894)来判断稳定性、使用[传递函数](@entry_id:273897)进行[频域分析](@entry_id:265642)，以及应用[极点配置](@entry_id:155523)、[线性二次调节器](@entry_id:267871)（LQR）等标准化方法来设计控制器。

从概念上讲，线性化类似于用一条[切线](@entry_id:268870)来近似一条曲线在某一点附近的形状。只要我们离[切点](@entry_id:172885)足够近，[切线](@entry_id:268870)就是曲线的一个极佳的局部近似。本章将系统地阐述线性化的基本原理、数学机制及其在[系统分析](@entry_id:263805)与控制设计中的核心应用。

### 数学基础：[泰勒级数展开](@entry_id:138468)

线性化的数学基石是函数的[泰勒级数展开](@entry_id:138468)。让我们从一个单变量函数 $y = f(x)$ 开始回顾。在任意点 $x_0$ 附近，只要函数 $f(x)$ 足够光滑（即具有足够高阶的导数），我们就可以将其展开为[泰勒级数](@entry_id:147154)：

$f(x) = f(x_0) + f'(x_0)(x - x_0) + \frac{f''(x_0)}{2!}(x - x_0)^2 + \dots$

如果我们只保留到一阶项，就得到了 $f(x)$ 在 $x_0$ 点的**线性近似**：

$f(x) \approx f(x_0) + f'(x_0)(x - x_0)$

这个近似在几何上就是函数在点 $(x_0, f(x_0))$ 处的[切线](@entry_id:268870)。

现在，我们将这个思想推广到控制系统中的多变量向量函数。考虑一个由[状态方程](@entry_id:274378)和输出方程描述的非线性系统：

$$
\begin{aligned}
\dot{\mathbf{x}} = f(\mathbf{x}, \mathbf{u}) \\
\mathbf{y} = h(\mathbf{x}, \mathbf{u})
\end{aligned}
$$

其中，$\mathbf{x} \in \mathbb{R}^n$ 是[状态向量](@entry_id:154607)，$\mathbf{u} \in \mathbb{R}^m$ 是输入向量，$\mathbf{y} \in \mathbb{R}^p$ 是输出向量。函数 $f$ 和 $h$ 是描述系统动态和量测的（通常是）[非线性](@entry_id:637147)向量函数。

为了在某个标称[工作点](@entry_id:173374) $(\mathbf{x}^\star, \mathbf{u}^\star)$ 附近分析系统，我们定义**微扰变量**（perturbation variables）：

$$
\begin{aligned}
\delta \mathbf{x}(t) = \mathbf{x}(t) - \mathbf{x}^\star \\
\delta \mathbf{u}(t) = \mathbf{u}(t) - \mathbf{u}^\star \\
\delta \mathbf{y}(t) = \mathbf{y}(t) - \mathbf{y}^\star
\end{aligned}
$$

其中，$\mathbf{y}^\star = h(\mathbf{x}^\star, \mathbf{u}^\star)$ 是对应于工作点 $(\mathbf{x}^\star, \mathbf{u}^\star)$ 的标称输出。

假设函数 $f$ 和 $h$ 在 $(\mathbf{x}^\star, \mathbf{u}^\star)$ 附近是连续可微的（即属于 $C^1$ 类），我们可以对它们进行一阶[泰勒展开](@entry_id:145057)。对于状态方程：

$\dot{\mathbf{x}} = \frac{d}{dt}(\mathbf{x}^\star + \delta \mathbf{x}) = \dot{\delta \mathbf{x}}$ (因为 $\mathbf{x}^\star$ 是一个常数点)

$f(\mathbf{x}, \mathbf{u}) = f(\mathbf{x}^\star + \delta \mathbf{x}, \mathbf{u}^\star + \delta \mathbf{u}) \approx f(\mathbf{x}^\star, \mathbf{u}^\star) + \left.\frac{\partial f}{\partial \mathbf{x}}\right|_{(\mathbf{x}^\star, \mathbf{u}^\star)} \delta \mathbf{x} + \left.\frac{\partial f}{\partial \mathbf{u}}\right|_{(\mathbf{x}^\star, \mathbf{u}^\star)} \delta \mathbf{u}$

这里的导数是**[雅可比矩阵](@entry_id:264467)**（Jacobian matrices）：

$$
A = \left.\frac{\partial f}{\partial \mathbf{x}}\right|_{(\mathbf{x}^\star, \mathbf{u}^\star)} \quad \text{和} \quad B = \left.\frac{\partial f}{\partial \mathbf{u}}\right|_{(\mathbf{x}^\star, \mathbf{u}^\star)}
$$

$A$ 是一个 $n \times n$ 的矩阵，其元素 $(i,j)$ 为 $\frac{\partial f_i}{\partial x_j}$ 在 $(\mathbf{x}^\star, \mathbf{u}^\star)$ 处的值。类似地，$B$ 是一个 $n \times m$ 的矩阵。

将这些组合起来，我们得到状态方程的**仿射近似**（affine approximation）：

$\dot{\delta \mathbf{x}} \approx f(\mathbf{x}^\star, \mathbf{u}^\star) + A \delta \mathbf{x} + B \delta \mathbf{u}$

同样，对于输出方程：

$\mathbf{y} = \mathbf{y}^\star + \delta \mathbf{y} = h(\mathbf{x}^\star + \delta \mathbf{x}, \mathbf{u}^\star + \delta \mathbf{u}) \approx h(\mathbf{x}^\star, \mathbf{u}^\star) + \left.\frac{\partial h}{\partial \mathbf{x}}\right|_{(\mathbf{x}^\star, \mathbf{u}^\star)} \delta \mathbf{x} + \left.\frac{\partial h}{\partial \mathbf{u}}\right|_{(\mathbf{x}^\star, \mathbf{u}^\star)} \delta \mathbf{u}$

由于我们定义了 $\mathbf{y}^\star = h(\mathbf{x}^\star, \mathbf{u}^\star)$，方程简化为：

$\delta \mathbf{y} \approx C \delta \mathbf{x} + D \delta \mathbf{u}$

其中，雅可比矩阵 $C$ 和 $D$ 定义为：

$$
C = \left.\frac{\partial h}{\partial \mathbf{x}}\right|_{(\mathbf{x}^\star, \mathbf{u}^\star)} \quad \text{和} \quad D = \left.\frac{\partial h}{\partial \mathbf{u}}\right|_{(\mathbf{x}^\star, \mathbf{u}^\star)}
$$

矩阵 $D$ 被称为**直接馈通矩阵**（direct feedthrough matrix），因为它直接将输入微扰 $\delta \mathbf{u}$ 映射到输出微扰 $\delta \mathbf{y}$。线性化模型是否存在直接馈通，完全取决于函数 $h$ 在工作点处对 $\mathbf{u}$ 的[偏导数](@entry_id:146280)是否为零。值得注意的是，即使 $h$ 是 $\mathbf{u}$ 的一个复杂[非线性](@entry_id:637147)函数，只要它在 $\mathbf{u}^\star$ 处的偏导数为零（例如，在[局部极值](@entry_id:144991)点），线性化模型中的 $D$ 矩阵就会是零矩阵 [@problem_id:2720606]。

### 围绕[平衡点](@entry_id:272705)的线性化

在控制理论中，最重要也最常见的线性化是围绕**[平衡点](@entry_id:272705)**（equilibrium point）进行的。一个[平衡点](@entry_id:272705) $(\mathbf{x}^\star, \mathbf{u}^\star)$ 是指在常数输入 $\mathbf{u}(t) = \mathbf{u}^\star$ 的作用下，系统状态能够保持不变的点。从数学上讲，这意味着状态的时间导数为零，即 $\dot{\mathbf{x}} = 0$。因此，[平衡点](@entry_id:272705)必须满足[代数方程](@entry_id:272665)：

$$
f(\mathbf{x}^\star, \mathbf{u}^\star) = \mathbf{0}
$$

这个条件至关重要 [@problem_id:2720600]。当我们将系统围绕一个[平衡点](@entry_id:272705)进行线性化时，之前导出的[仿射模型](@entry_id:143914)中的常数项 $f(\mathbf{x}^\star, \mathbf{u}^\star)$ 就等于零。这使得微扰动态方程变成一个真正的**[线性时不变](@entry_id:276287)（LTI）系统**，而不是[仿射系统](@entry_id:634107)：

$$
\begin{aligned}
\dot{\delta \mathbf{x}} = A \delta \mathbf{x} + B \delta \mathbf{u} \\
\delta \mathbf{y} = C \delta \mathbf{x} + D \delta \mathbf{u}
\end{aligned}
$$

这个标准的LTI[状态空间模型](@entry_id:137993)是后续进行稳定性分析、[控制器设计](@entry_id:274982)和系统辨识的出发点。

**示例：一个[非线性系统的线性化](@entry_id:275116)**

考虑一个由以下方程描述的非线性系统 [@problem_id:2865858]：
$$
\begin{aligned}
\dot{x}_{1} = -3x_{1} + x_{2}^{3} + u \cos(x_{1}) \\
\dot{x}_{2} = \tanh(x_{1}) - x_{2} + u \\
y = x_{1} + \exp(x_{2})u
\end{aligned}
$$

首先，我们需要验证 $(x^\star, u^\star) = ([0, 0]^\top, 0)$ 是否为一个[平衡点](@entry_id:272705)。代入[状态方程](@entry_id:274378)：
$\dot{x}_1 = -3(0) + 0^3 + 0 \cdot \cos(0) = 0$
$\dot{x}_2 = \tanh(0) - 0 + 0 = 0$
由于 $f(x^\star, u^\star) = \mathbf{0}$，该点确实是一个[平衡点](@entry_id:272705)。对应的标称输出为 $y^\star = 0 + \exp(0) \cdot 0 = 0$。

接下来，我们计算雅可比矩阵 $A, B, C, D$ 在该点的值。
$f(x, u) = \begin{pmatrix} -3x_{1} + x_{2}^{3} + u \cos(x_{1}) \\ \tanh(x_{1}) - x_{2} + u \end{pmatrix}$

$A = \left.\frac{\partial f}{\partial x}\right|_{(0,0,0)} = \left.\begin{pmatrix} -3 - u\sin(x_1) & 3x_2^2 \\ \text{sech}^2(x_1) & -1 \end{pmatrix}\right|_{(0,0,0)} = \begin{pmatrix} -3 & 0 \\ 1 & -1 \end{pmatrix}$

$B = \left.\frac{\partial f}{\partial u}\right|_{(0,0,0)} = \left.\begin{pmatrix} \cos(x_1) \\ 1 \end{pmatrix}\right|_{(0,0,0)} = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$

$C = \left.\frac{\partial h}{\partial x}\right|_{(0,0,0)} = \left.\begin{pmatrix} 1 & u\exp(x_2) \end{pmatrix}\right|_{(0,0,0)} = \begin{pmatrix} 1 & 0 \end{pmatrix}$

$D = \left.\frac{\partial h}{\partial u}\right|_{(0,0,0)} = \left.\exp(x_2)\right|_{(0,0,0)} = 1$

因此，描述系统在原点附近行为的线性化模型为：
$$
\begin{aligned}
\dot{\delta x} = \begin{pmatrix} -3 & 0 \\ 1 & -1 \end{pmatrix} \delta x + \begin{pmatrix} 1 \\ 1 \end{pmatrix} \delta u \\
\delta y = \begin{pmatrix} 1 & 0 \end{pmatrix} \delta x + 1 \cdot \delta u
\end{aligned}
$$

### 线性化模型的应用

一旦获得了LTI模型，我们就可以利用它进行深入的分析和设计。

#### 稳定性分析

根据 **Hartman-Grobman 定理**，在一个**[双曲平衡点](@entry_id:165723)**（hyperbolic equilibrium point）的邻域内，非线性系统的动态行为在拓扑上等价于其线性化系统的动态行为。[双曲平衡点](@entry_id:165723)是指其线性化[系统矩阵](@entry_id:172230) $A$ 的所有[特征值](@entry_id:154894)都没有零实部。

这意味着，我们可以通过检查矩阵 $A$ 的[特征值](@entry_id:154894)来判断非线性系统在该[平衡点](@entry_id:272705)局部的稳定性：
- 如果所有[特征值](@entry_id:154894)的实部都为负，则该[平衡点](@entry_id:272705)是**局部渐近稳定**的。
- 如果至少有一个[特征值](@entry_id:154894)的实部为正，则该[平衡点](@entry_id:272705)是**不稳定**的。
- 如果[特征值](@entry_id:154894)中既有正实部也有负实部，则该[平衡点](@entry_id:272705)是一个**[鞍点](@entry_id:142576)**。

例如，考虑一个[倒立摆模型](@entry_id:176720)，其[平衡点](@entry_id:272705)之一在垂直向上位置 $x_1=\pi$ 处。对此系统在该不稳定平衡点进行线性化，会得到一个状态矩阵 $A$，其[特征值](@entry_id:154894)之一具有正实部，从而在数学上证实了该[平衡点](@entry_id:272705)的不稳定性 [@problem_id:1590141]。这为设计一个使摆稳定在这一位置的控制器提供了基础。

然而，线性化分析有其局限性。如果矩阵 $A$ 存在任何具有零实部的[特征值](@entry_id:154894)（例如，纯虚数[特征值](@entry_id:154894)），该[平衡点](@entry_id:272705)就不是双曲的。在这种情况下，Hartman-Grobman 定理不适用，线性化模型无法确定[非线性系统的稳定性](@entry_id:264568)。高阶[非线性](@entry_id:637147)项可能会使系统稳定、不稳定，或产生[极限环](@entry_id:274544)。例如，在一个具有纯虚数[特征值](@entry_id:154894)的[生态模型](@entry_id:186101)中，我们不能仅从线性化就断定物种是共存还是会灭绝 [@problem_id:2167263]。

#### [控制器设计](@entry_id:274982)与[系统分析](@entry_id:263805)

线性化模型是设计局部控制器的基础。例如，我们可以使用[极点配置技术](@entry_id:270184)设计一个[状态反馈控制器](@entry_id:203349) $\delta u = -K \delta x$，使得闭环系统矩阵 $(A-BK)$ 的[特征值](@entry_id:154894)都位于复平面的左半部分，从而稳定原始的非线性系统在该[平衡点](@entry_id:272705)附近。

此外，线性化模型使我们能够计算**[传递函数](@entry_id:273897)**，将系统与[频域分析](@entry_id:265642)工具连接起来。对于微扰变量，从输入 $\delta U(s)$ 到输出 $\delta Y(s)$ 的[传递函数](@entry_id:273897)为：

$G(s) = C(sI - A)^{-1}B + D$

对于之前示例中的系统 [@problem_id:2865858]，其[传递函数](@entry_id:273897)可以计算为 $G(s) = \frac{s+4}{s+3}$。这个[传递函数](@entry_id:273897)描述了当输入以特定频率[振荡](@entry_id:267781)时，系统输出的响应特性，这对于设计[PID控制器](@entry_id:268708)等经典控制器至关重要。

线性化同样适用于其他系统属性的分析，如**能观性**（observability）。能观性决定了我们是否能通过测量系统输出来唯一地确定系统的内部状态。对于[LTI系统](@entry_id:271946)，这可以通过能观性[矩阵的秩](@entry_id:155507)来判断。然而，对于[非线性系统](@entry_id:168347)，能观性可能是状态依赖的。通过在不同点进行线性化，我们可以研究能观性如何随系统状态变化。例如，对于一个通过测量其角度的正弦值 $y=\sin(x_1)$ 来观测的摆，线性化分析表明，当摆接近水平位置（$x_1=\pi/2$）时，系统会失去能观性。这是因为在这些点，$\sin(x_1)$ 函数的斜率为零，导致输出对角度的微小变化不敏感 [@problem_id:2720575]。

### 超越[平衡点](@entry_id:272705)的线性化

虽然围绕[平衡点](@entry_id:272705)的线性化是最常见的，但线性化技术本身更为通用。

有时，我们需要在一个并非[平衡点](@entry_id:272705)的任意点 $(x_0, u_0)$ 进行线性化。在这种情况下，$f(x_0, u_0)$ 通常不为零。[仿射模型](@entry_id:143914)变为：

$\dot{\delta x} \approx A \delta x + B \delta u + e$

其中 $e = f(x_0, u_0)$ 是一个非零的常数向量，代表一个恒定的“漂移”或“偏置”项 [@problem_id:1590122]。这种模型在某些分析中可能有用，但由于这个常数项的存在，它不像标准的LTI模型那样便于进行[控制器设计](@entry_id:274982)。

另一个重要的应用是**量测[模型的线性化](@entry_id:751300)**。在许多导航和滤波问题（如[扩展卡尔曼滤波器](@entry_id:199333) EKF）中，我们需要一个描述传感器测量值如何依赖于系统状态的[线性模型](@entry_id:178302)。例如，一个自主车测量其到原点信标的距离，其量测函数为 $y = \sqrt{p_x^2 + p_y^2}$，其中 $(p_x, p_y)$ 是车辆的位置。这是一个[非线性](@entry_id:637147)函数。我们可以将其围绕一个标称位置 $(p_{x,0}, p_{y,0})$ 进行线性化，得到一个在局部有效的线性量测方程 [@problem_id:1590143]。

### 线性化的局限性与有效性范围

最后，我们必须深刻理解线性化是一个**近似**，其有效性是有条件的。

#### 定性局限

如前所述，对于非[双曲平衡点](@entry_id:165723)，线性化在[稳定性分析](@entry_id:144077)方面是无效的。[非线性](@entry_id:637147)项的行为决定了系统的最终命运。

#### 定量局限：“小邻域”有多小？

线性化的有效性仅限于工作点的一个“小邻域”内。但是，“小”是一个相对概念。其大小取决于系统[非线性](@entry_id:637147)的强度以及我们对模型精度的要求。

我们可以通过考察[泰勒展开](@entry_id:145057)中的高阶项来量化[线性化误差](@entry_id:751298)。[线性化误差](@entry_id:751298) $E(x) = f(x) - f_{\text{lin}}(x)$ 主要由二阶及更高阶的项主导。对于一个足够光滑的函数，在[工作点](@entry_id:173374)附近，这个误差的大小约等于二阶项。我们可以推导出形如 $\Vert f(x) - f_{\text{lin}}(x) \Vert \le C \Vert x-x^\star \Vert^2$ 的[误差界](@entry_id:139888)，其中 $C$ 是一个依赖于函数[二阶导数](@entry_id:144508)的常数 [@problem_id:2720592]。这个界表明，误差随着偏离工作点的距离的平方而增长。通过这个[误差界](@entry_id:139888)，我们可以估算出，要将[线性化误差](@entry_id:751298)保持在某个给定的容差 $\tau$ 之内，系统状态必须保持在以 $x^\star$ 为中心、半径为 $r \approx \sqrt{\tau/C}$ 的球形区域内。这为“小邻域”提供了一个具体的、可计算的度量。

#### 实践局限与更广阔的视野

在某些应用中，系统的运行范围远远超出了任何单个[平衡点](@entry_id:272705)的小邻域。例如，一架进行特技飞行的无人机，其姿态和速度会在一个非常大的范围内剧烈变化 [@problem_id:1575287]。在这种情况下，基于单一工作点（如悬停）的线性化控制器在远离该点时性能会急剧下降。

这揭示了雅可比线性化的根本局限性：它是一种**局部**方法。为了解决这个问题，[控制工程](@entry_id:149859)师发展了更先进的技术，例如**[增益调度](@entry_id:272589)**（Gain Scheduling），即在多个工作点进行线性化并设计相应的控制器，然后根据系统当前状态在这些控制器之间进行平滑切换。另一种更强大的技术是**[反馈线性化](@entry_id:163432)**（Feedback Linearization），它通过一个[非线性](@entry_id:637147)的[状态反馈](@entry_id:151441)来精确抵消系统的[非线性](@entry_id:637147)，从而在更广阔的状态空间区域内得到一个等效的[线性系统](@entry_id:147850)。这些高级主题虽然超出了本章的范围，但它们的存在突显了理解基础线性化及其局限性的重要性，因为它是通向更复杂、更强大的[非线性](@entry_id:637147)控制世界的垫脚石。