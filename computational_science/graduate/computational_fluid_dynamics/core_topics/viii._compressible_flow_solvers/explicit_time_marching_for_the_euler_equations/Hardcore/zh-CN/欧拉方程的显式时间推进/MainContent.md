## 引言
在计算流体力学（CFD）领域，欧拉方程是模拟无粘可压缩流动的基石，对于理解航空航天、天体物理乃至工程设计中的高速流动现象至关重要。然而，这些非线性双曲守恒律方程的解析解极为有限，特别是在存在激波和接触间断等复杂结构时，数值求解成为不可或缺的工具。其中的核心挑战在于如何设计出既能精确捕捉这些间断，又能保持数值稳定和计算效率的算法。显式时间推进方法因其实现简单和易于并行而广受欢迎，但其背后蕴含着深刻的数学原理和精巧的算法设计。

本文旨在系统性地剖析求解欧拉方程的显式时间推进框架。读者将从第一性原理出发，逐步构建一套完整而强大的数值求解体系。在“原理与机制”一章中，我们将奠定理论基础，从欧拉方程的守恒形式与双曲特性讲起，深入有限体积法、CFL稳定性条件、数值通量构造，并最终实现高阶MUSCL-SSP格式。随后，在“应用与跨学科联系”一章中，我们将展示如何将这些核心原理应用于解决更复杂的实际问题，例如弯曲网格上的几何守恒律、基于特征的边界条件、以及在多物理场耦合中的扩展。最后，“动手实践”部分将提供具体的计算练习，帮助读者将理论知识转化为实践能力。

让我们首先进入第一章，深入探讨这些强大算法的底层原理与核心机制。

## 原理与机制

本章旨在深入探讨求解可压缩欧拉方程的显式时间推进方法的根本原理与核心机制。我们将从欧拉方程的守恒形式出发，系统地建立描述流体运动的数学框架。随后，我们将阐明双曲系统的特性，特别是信息传播速度的概念，这对于理解显式格式的稳定性至关重要。在此基础上，我们将构建有限体积法的基本框架，并详细讨论数值通量的构造，从简单的耗散格式到复杂的近似黎曼求解器。为了超越一阶精度，我们将引入实现高分辨率的 MUSCL 重构与 TVD (总变差递减) 限制器。最后，我们将讨论保证高阶时间积分器稳定性的强稳定性保持 (SSP) 方法，并综合分析整个数值格式的收敛阶。

### 欧拉方程的守恒形式

无粘可压缩流动的控制方程是欧拉方程，它以积分形式表达了质量、动量和能量三大基本物理量的守恒定律。对于一维流动，其守恒形式的偏微分方程组可以写为：

$$
\frac{\partial \boldsymbol{U}}{\partial t} + \frac{\partial \boldsymbol{F}(\boldsymbol{U})}{\partial x} = \boldsymbol{0}
$$

其中，$t$ 是时间，$x$ 是空间坐标。$\boldsymbol{U}$ 是守恒变量矢量，$\boldsymbol{F}(\boldsymbol{U})$ 是相应的通量矢量。对于量热完全气体（calorically perfect gas），它们的具体形式为：

$$
\boldsymbol{U} = \begin{pmatrix} \rho \\ \rho u \\ E \end{pmatrix}, \qquad \boldsymbol{F}(\boldsymbol{U}) = \begin{pmatrix} \rho u \\ \rho u^2 + p \\ u(E+p) \end{pmatrix}
$$

这里的变量分别代表：$\rho$ 为流体密度，$u$ 为流体速度，$p$ 为热力学压力，$E$ 为单位体积的总能量。这三个守恒变量与流体的三个基本守恒定律一一对应：

1.  **质量守恒**：$\boldsymbol{U}$ 的第一个分量 $\rho$ 是单位体积的质量。其通量 $\rho u$ 代表单位时间内通过单位面积的质量流量。

2.  **动量守恒**：$\boldsymbol{U}$ 的第二个分量 $\rho u$ 是单位体积的动量。其通量 $\rho u^2 + p$ 由两部分组成：第一部分 $\rho u^2 = (\rho u)u$ 代表动量自身的对流输运；第二部分 $p$ 代表作用在控制体表面上的压力（单位面积上的法向力）。这直接体现了牛顿第二定律，即流体微元的动量变化率等于作用在其上的压力梯度力。[@problem_id:3317378]

3.  **能量守恒**：$\boldsymbol{U}$ 的第三个分量 $E$ 是单位体积的总能量，它由内部能量和动能两部分组成，即 $E = \rho e + \frac{1}{2}\rho u^2$，其中 $e$ 是单位质量的内能（比内能）。其通量 $u(E+p)$ 同样可以分解为两部分：$uE$ 表示总能量的对流输运，而 $up$ 则代表压力在控制体表面所做的功，即压强功（pressure work）的通量。[@problem_id:3317378]

为了使方程组封闭，还需要一个状态方程 (Equation of State, EOS) 来关联热力学变量。对于量热完全气体，压力 $p$、密度 $\rho$ 和比内能 $e$ 之间的关系为 $p = (\gamma - 1)\rho e$，其中 $\gamma$ 是比热比。利用总能量的定义，我们可以将压力表示为守恒变量的函数：

$$
p = (\gamma - 1) \left(E - \frac{1}{2}\rho u^2\right) = (\gamma-1)\left(E - \frac{1}{2}\frac{(\rho u)^2}{\rho}\right)
$$

值得注意的是，压力 $p$ 并非一个独立的守恒量，而是由守恒变量 $\boldsymbol{U}$ 决定的一个状态量。欧拉方程组是一个非线性、强耦合的系统，因为通量 $\boldsymbol{F}$ 中的每一项都依赖于守恒变量 $\boldsymbol{U}$ 的多个分量。[@problem_id:3317378]

对于二维或三维流动，该方程组可以自然地推广。例如，在二维笛卡尔坐标系 $(x,y)$ 中，方程变为：

$$
\frac{\partial \boldsymbol{U}}{\partial t} + \frac{\partial \boldsymbol{F}(\boldsymbol{U})}{\partial x} + \frac{\partial \boldsymbol{G}(\boldsymbol{U})}{\partial y} = \boldsymbol{0}
$$

其中守恒变量和通量矢量扩展为：

$$
\boldsymbol{U} = \begin{pmatrix} \rho \\ \rho u \\ \rho v \\ E \end{pmatrix}, \quad \boldsymbol{F}(\boldsymbol{U}) = \begin{pmatrix} \rho u \\ \rho u^2 + p \\ \rho uv \\ u(E+p) \end{pmatrix}, \quad \boldsymbol{G}(\boldsymbol{U}) = \begin{pmatrix} \rho v \\ \rho uv \\ \rho v^2 + p \\ v(E+p) \end{pmatrix}
$$

这里，$u$ 和 $v$ 分别是 $x$ 和 $y$ 方向的速度分量，总能量密度 $E = \rho e + \frac{1}{2}\rho (u^2+v^2)$。[@problem_id:3317311]

### 双曲性与特征速度

欧拉方程组属于一类被称为 **双曲型偏微分方程** 的系统。这一数学属性至关重要，因为它决定了信息在流场中是如何传播的。对于形如 $\partial_t \boldsymbol{U} + \partial_x \boldsymbol{F}(\boldsymbol{U}) = \boldsymbol{0}$ 的方程，我们可以写出其准线性形式：

$$
\frac{\partial \boldsymbol{U}}{\partial t} + \boldsymbol{A}(\boldsymbol{U}) \frac{\partial \boldsymbol{U}}{\partial x} = \boldsymbol{0}
$$

其中 $\boldsymbol{A}(\boldsymbol{U}) = \frac{\partial \boldsymbol{F}}{\partial \boldsymbol{U}}$ 是 **通量雅可比矩阵** (flux Jacobian matrix)。一个系统是双曲的，如果对于任意物理上允许的状态 $\boldsymbol{U}$，矩阵 $\boldsymbol{A}(\boldsymbol{U})$ 都具有实数特征值和一组完备的线性无关的特征向量。

这些特征值，记为 $\lambda_k$，代表了流场中信息传播的 **特征速度**。要推导这些特征速度，直接对 $\boldsymbol{F}$ 求 $\boldsymbol{U}$ 的偏导数在代数上较为繁琐。一个更系统的方法是引入原始变量 (primitive variables) $\boldsymbol{V} = (\rho, u, p)^{\mathsf{T}}$，并利用链式法则。通量雅可比矩阵可以表示为 $\boldsymbol{A} = (\partial \boldsymbol{F} / \partial \boldsymbol{V}) (\partial \boldsymbol{U} / \partial \boldsymbol{V})^{-1}$。通过计算，可以得到一个更简洁的矩阵，其特征值与 $\boldsymbol{A}$ 相同。

经过严谨的推导，对于一维欧拉方程，可以证明通量雅可比矩阵 $\boldsymbol{A}(\boldsymbol{U})$ 的三个特征值为：

$$
\lambda_1 = u - c, \qquad \lambda_2 = u, \qquad \lambda_3 = u + c
$$

其中 $c = \sqrt{\gamma p / \rho}$ 是当地的 **声速** (speed of sound)。[@problem_id:3317332] 这些特征值都是实数，并且只要声速 $c \neq 0$（即压力 $p>0$ 且密度 $\rho>0$），它们就是互不相同的。在这种情况下，系统被称为 **严格双曲的** (strictly hyperbolic)。

这三个特征速度具有明确的物理意义：
- $\lambda_2 = u$：对应于随流体自身运动的信息传播。熵的变化和接触间断（密度和温度有跳跃，但压力和速度连续）都以局部流速 $u$ 传播。
- $\lambda_{1,3} = u \pm c$：对应于声波的传播。这些是压力和密度的扰动，它们以相对于流体运动的速度 $\pm c$ 传播。换言之，它们在静止坐标系下的传播速度是 $u+c$（顺流）和 $u-c$（逆流）。[@problem_id:3317378]

理解特征速度是设计稳定数值方法的基石。任何局部扰动都会沿着这些特征方向传播，形成一个所谓的“依赖域”。

### 有限体积法与显式时间推进

**有限体积法** (Finite Volume Method) 是求解守恒律方程的一种非常自然且强大的数值方法。其基本思想不是在网格点上近似微分方程，而是在一系列不重叠的控制体（或称为“单元”）上严格满足积分形式的守恒定律。

考虑一维空间中的一个单元格 $[x_{i-1/2}, x_{i+1/2}]$，其宽度为 $\Delta x_i = x_{i+1/2} - x_{i-1/2}$。将欧拉方程在该单元格上积分，并应用散度定理，可得：

$$
\frac{d}{dt} \int_{x_{i-1/2}}^{x_{i+1/2}} \boldsymbol{U}(x,t) dx + \boldsymbol{F}(\boldsymbol{U}(x_{i+1/2},t)) - \boldsymbol{F}(\boldsymbol{U}(x_{i-1/2},t)) = \boldsymbol{0}
$$

定义单元 $i$ 内的平均守恒量为 $\boldsymbol{U}_i(t) = \frac{1}{\Delta x_i} \int_{x_{i-1/2}}^{x_{i+1/2}} \boldsymbol{U}(x,t) dx$，上式变为：

$$
\frac{d \boldsymbol{U}_i}{dt} = -\frac{1}{\Delta x_i} \left( \boldsymbol{F}_{i+1/2} - \boldsymbol{F}_{i-1/2} \right)
$$

这里的 $\boldsymbol{F}_{i\pm1/2}$ 是在单元格边界 $x_{i\pm1/2}$ 上的瞬时通量。然而，由于 $\boldsymbol{U}_i$ 是单元平均值，在单元边界上的值是未知的。数值方法的核心挑战就在于如何近似这个通量。我们用一个 **数值通量** (numerical flux) 函数 $\hat{\boldsymbol{F}}$ 来代替它，该函数依赖于界面两侧的状态（例如，来自单元 $i$ 和 $i+1$ 的信息）。这样，我们就得到了一个常微分方程组（ODE），称为半离散格式：

$$
\frac{d \boldsymbol{U}_i}{dt} = \mathcal{L}(\boldsymbol{U})_i := -\frac{1}{\Delta x_i} \left( \hat{\boldsymbol{F}}_{i+1/2} - \hat{\boldsymbol{F}}_{i-1/2} \right)
$$

其中 $\hat{\boldsymbol{F}}_{i+1/2}$ 是数值通量，通常是界面左右两侧状态 $\boldsymbol{U}_i$ 和 $\boldsymbol{U}_{i+1}$ 的函数，即 $\hat{\boldsymbol{F}}_{i+1/2} = \hat{\boldsymbol{F}}(\boldsymbol{U}_i, \boldsymbol{U}_{i+1})$。

接下来，我们需要对这个 ODE 系统进行时间积分。最简单的方法是 **前向欧拉法** (Forward Euler method)，这是一个显式方法：

$$
\frac{\boldsymbol{U}_i^{n+1} - \boldsymbol{U}_i^n}{\Delta t} = \mathcal{L}(\boldsymbol{U}^n)_i
$$

整理后得到全离散的更新格式：

$$
\boldsymbol{U}_i^{n+1} = \boldsymbol{U}_i^n - \frac{\Delta t}{\Delta x_i} \left( \hat{\boldsymbol{F}}_{i+1/2}^n - \hat{\boldsymbol{F}}_{i-1/2}^n \right)
$$

其中上标 $n$ 表示时间层 $t^n = n \Delta t$。这种一次性使用所有空间方向通量进行更新的方法称为 **非分裂格式** (unsplit scheme)。[@problem_id:3317311]

#### 显式格式的稳定性：CFL 条件

显式时间推进方法的一个主要限制是其 **条件稳定性** (conditional stability)。这意味着时间步长 $\Delta t$ 不能任意选取，它受到空间步长 $\Delta x$ 和物理问题特性的制约。这个限制就是著名的 **Courant-Friedrichs-Lewy (CFL) 条件**。

其物理直觉是：在一个时间步 $\Delta t$ 内，位于某一点的物理信息所能传播的最远距离，不能超出该点在数值计算中所依赖的网格范围（即数值依赖域）。对于我们的一阶有限体积格式，一个单元的更新依赖于其相邻单元。因此，从一个单元边界传出的最快的物理信号，在一个时间步内不应传播超过一个单元的宽度。

我们已经知道，欧拉方程中最快的信号传播速度是 $\max(|\lambda|) = |u| + c$。因此，物理影响区域的传播速度为 $|u|+c$。在一个时间步 $\Delta t$ 内，该信号传播的距离为 $(|u|+c)\Delta t$。为了保证数值稳定性，这个距离必须小于空间步长 $\Delta x$。这便导出了 CFL 条件：

$$
(|u|+c) \frac{\Delta t}{\Delta x} \le 1
$$

在实践中，我们会引入一个小于 1 的安全因子，称为 CFL 数或 Courant 数，记为 $\sigma_{\text{CFL}}$。因此，稳定的时间步长必须满足：

$$
\Delta t \le \sigma_{\text{CFL}} \frac{\Delta x}{\max_{\text{domain}}(|u|+c)}
$$

其中最大值需要在整个计算域中寻找。[@problem_id:3317378]

为了更严格地理解稳定性，我们可以进行 **冯·诺依曼稳定性分析** (von Neumann stability analysis)。虽然欧拉方程是非线性的，但我们可以通过分析其线性化模型来获得关键洞察。考虑一个简化的线性声波系统，用一阶迎风格式和前向欧拉法离散。通过寻找形如 $\boldsymbol{q}_j^n = \hat{\boldsymbol{q}}^n e^{i\theta j}$ 的傅里叶模态解，我们可以推导出 **放大因子** (amplification factor) $G(\theta; \sigma)$，它描述了单个模态在一个时间步内的振幅变化。对于与特征速度 $+c$ 相关的右行波，其放大因子为：

$$
G(\theta; \sigma) = 1 - \sigma(1 - e^{-i\theta})
$$

其中 $\sigma = c \Delta t / \Delta x$ 是该模式的 Courant 数。稳定性的要求是 $|G(\theta; \sigma)| \le 1$ 对所有波数 $\theta$ 成立。通过计算可得，这个条件等价于 $0 \le \sigma \le 1$。这为 CFL 条件提供了坚实的数学基础，表明 Courant 数必须小于等于 1 才能保证稳定。[@problem_id:3317331]

### 数值通量的构造

数值通量 $\hat{\boldsymbol{F}}$ 的设计是有限体积方法的核心。一个好的数值通量应该：
1.  **相容性** (Consistent)：当左右状态相同时，$\hat{\boldsymbol{F}}(\boldsymbol{U}, \boldsymbol{U}) = \boldsymbol{F}(\boldsymbol{U})$。
2.  **稳定性** (Stable)：能够引入适量的数值耗散，以抑制非物理振荡并稳定计算。
3.  **精确性** (Accurate)：尽可能减少数值耗散，以精确捕捉流动的物理特征。

数值通量的构造通常基于在单元界面上求解或近似求解一个 **黎曼问题** (Riemann problem)。黎曼问题是一个具有特定初值的柯西问题，其初值由两个常数状态（即我们的 $\boldsymbol{U}_L = \boldsymbol{U}_i$ 和 $\boldsymbol{U}_R = \boldsymbol{U}_{i+1}$）在界面处拼接而成。其自相似解包含了一系列波（激波、稀疏波、接触间断），这些波以不同的特征速度从界面处传播开来。

#### 鲁萨诺夫通量 (Rusanov Flux)

最简单的数值通量之一是 **鲁萨诺夫通量**，也称为局部 Lax-Friedrichs 通量。它的思想是在物理通量的平均值基础上，添加一个与状态差成正比的数值耗散项。其形式为：

$$
\hat{\boldsymbol{F}}(\boldsymbol{U}_L, \boldsymbol{U}_R) = \frac{1}{2}\left( \boldsymbol{F}(\boldsymbol{U}_L) + \boldsymbol{F}(\boldsymbol{U}_R) \right) - \frac{s_{\max}}{2} \left( \boldsymbol{U}_R - \boldsymbol{U}_L \right)
$$

这里的 $s_{\max}$ 是界面处信号传播速度的最大估计值。为了确保所有波都被稳定地处理，它必须大于等于界面左右两侧所有特征速度的绝对值。对于欧拉方程，一个安全且常用的选择是：

$$
s_{\max} = \max(|u_L| + c_L, |u_R| + c_R)
$$

鲁萨诺夫通量非常鲁棒，易于实现，并且能够保证解的正定性（在适当的 CFL 约束下）。然而，它的数值耗散相对较大，可能会过度抹平接触间断等精细结构。这种方法可以自然地推广到多维，例如在二维情况下，我们分别在 $x$ 和 $y$ 方向上使用各自的法向速度和最大波速来构造 $\hat{\boldsymbol{F}}$ 和 $\hat{\boldsymbol{G}}$。[@problem_id:3317311]

#### 近似黎曼求解器 (Approximate Riemann Solvers)

为了提高精度，研究者们开发了更复杂的通量，它们更精确地模拟了黎曼问题的波结构。

- **戈杜诺夫通量 (Godunov Flux)**：这是理论上的“黄金标准”。它通过求解界面上的 **精确黎曼问题** 来得到界面处的真实状态 $\boldsymbol{U}^*$，然后用物理通量 $\boldsymbol{F}(\boldsymbol{U}^*)$ 作为数值通量。戈杜诺夫方法能够完美地捕捉所有波族，并自动满足熵条件，因此具有极低的数值耗散。但其缺点是计算成本非常高，因为它需要在每个界面的每个时间步都进行一次迭代求解。[@problem_id:3317363]

- **Roe 通量**：这是一种非常流行的近似黎曼求解器。它的核心思想是通过一个特殊平均状态（Roe 平均）构造一个常数矩阵 $\hat{\boldsymbol{A}}(\boldsymbol{U}_L, \boldsymbol{U}_R)$，使得通量差被精确线性化，即 $\boldsymbol{F}(\boldsymbol{U}_R) - \boldsymbol{F}(\boldsymbol{U}_L) = \hat{\boldsymbol{A}}(\boldsymbol{U}_R - \boldsymbol{U}_L)$。然后，通过对 $\hat{\boldsymbol{A}}$ 进行特征分解，将状态差 $\boldsymbol{U}_R - \boldsymbol{U}_L$ 分解到三个特征波上，并根据每个波的传播方向（特征值的符号）进行迎风处理。Roe 格式能精确解析孤立的激波和接触间断，精度很高。然而，它也存在一些著名的问题，比如在跨音速稀疏波附近可能产生非物理的“膨胀激波”（需要熵修正来解决），并且不能保证密度和压力的正定性。[@problem_id:3317363]

- **HLLC 通量**：这是 HLL (Harten-Lax-van Leer) 格式的改进版。HLL 格式假设黎曼问题的解只包含两个最快的波（一个左行，一个右行），中间是一个常数状态。这种简化使其非常鲁棒，但会严重抹平中间的接触间断。HLLC (Harten-Lax-van Leer-Contact) 格式通过在两个声波之间重新引入被 HLL 忽略的接触间断波，修正了这一缺陷。它构造了一个包含两个“星区”状态和一个接触波的三波模型。这使得 HLLC 能够像 Godunov 和 Roe 格式一样精确解析接触间断，同时它又比 Roe 格式计算成本更低，因为它只需要估计波速，而不需要完整的特征向量分解。[@problem_id:3317363]

### 实现高阶精度：MUSCL 重构

上述使用单元平均值 $\boldsymbol{U}_i$ 和 $\boldsymbol{U}_{i+1}$ 作为黎曼问题输入的格式，在空间上最多只有一阶精度。为了获得更高阶的精度，我们可以采用 **MUSCL (Monotonic Upstream-centered Schemes for Conservation Laws)** 方法。

MUSCL 的核心思想是，在每个单元内部，不再假设物理量是常数，而是用一个更高阶的多项式（通常是线性函数）来重构其分布。然后，用这个重构多项式在单元边界处的值 $\boldsymbol{U}_{i+1/2}^L$ 和 $\boldsymbol{U}_{i+1/2}^R$ 作为黎曼求解器的输入。

对于单元 $i$，一个线性的重构可以表示为：

$$
\boldsymbol{U}(x) = \boldsymbol{U}_i + \boldsymbol{\sigma}_i (x - x_i), \quad \text{for } x \in [x_{i-1/2}, x_{i+1/2}]
$$

其中 $\boldsymbol{\sigma}_i$ 是单元内的斜率。这个斜率需要被小心地选择。一个简单的中心差分斜率会导致在激波等间断附近产生严重的非物理振荡（吉布斯现象）。为了避免这种情况，MUSCL 引入了 **斜率限制器** (slope limiter) 的概念。

限制器的作用是根据数据的局部光滑度来调整斜率 $\boldsymbol{\sigma}_i$。一个关键的工具是连续斜率的比值：

$$
r_i = \frac{\boldsymbol{U}_{i+1} - \boldsymbol{U}_i}{\boldsymbol{U}_i - \boldsymbol{U}_{i-1}}
$$

这个比值 $r_i$ 可以作为一个局部光滑度探测器：[@problem_id:3317335]
- 如果 $r_i \approx 1$，说明数据局部是线性的（光滑的）。
- 如果 $r_i$ 远离 1 但为正，说明数据是单调的。
- 如果 $r_i \le 0$，说明在 $\boldsymbol{U}_i$ 处存在一个局部极值。

斜率限制器是一个函数 $\phi(r)$，它将一个未经限制的斜率（例如，由中心或后向差分计算）乘以一个修正因子，以获得最终使用的斜率。例如，一个常见的重构形式是：

$$
\boldsymbol{U}_{i+1/2}^L = \boldsymbol{U}_i + \frac{1}{2} \phi(r_i) (\boldsymbol{U}_i - \boldsymbol{U}_{i-1})
$$

限制器函数 $\phi(r)$ 的设计目标是：在光滑区域（$r_i \approx 1$），$\phi(r_i) \approx 1$，以保持高阶精度；在极值点附近（$r_i \le 0$），$\phi(r_i) \to 0$，将格式降为一阶以避免产生新的振荡。

为了保证格式的非振荡性，我们通常要求它满足 **总变差递减 (TVD)** 条件。Harten 和 Sweby 的研究表明，对于标量守恒律，只要限制器函数 $\phi(r)$ 位于一个特定的区域内，即满足：

$$
0 \le \phi(r) \le \min(2, 2r) \quad \text{for } r > 0, \quad \text{and} \quad \phi(r) = 0 \quad \text{for } r \le 0
$$

并且满足适当的 CFL 条件，那么整个 MUSCL 格式就是 TVD 的。常见的限制器如 minmod、superbee、van Leer 等都满足这些条件。对于欧拉方程这样的方程组，限制过程通常需要在 **特征变量** (characteristic variables) 上逐分量进行，以确保每个物理波的非振荡性。[@problem_id:3317335]

### 高阶时间积分：强稳定性保持 (SSP) 方法

采用高阶空间离散（如 MUSCL）后，为了在整体上获得高阶精度，时间积分也必须是高阶的。然而，标准的高阶龙格-库塔 (Runge-Kutta, RK) 方法，如经典的四阶 RK 方法，可能会破坏由 TVD 限制器精心保证的非振荡性质。

**强稳定性保持 (Strong Stability Preserving, SSP)** 方法是一类专门为此设计的显式时间积分格式。它们的核心特性是：一个 SSP-RK 方法的每一步都可以表示为一系列 **前向欧拉步骤的凸组合** (convex combination of Forward Euler steps)。

让我们考虑一个抽象的半离散系统 $\frac{d\boldsymbol{U}}{dt} = \mathcal{L}(\boldsymbol{U})$。假设我们已知前向欧拉法在时间步长 $\Delta t \le \Delta t_{\text{FE}}$ 时是稳定的（例如，是 TVD 的或保正的）。一个 $s$ 阶的 SSP-RK 方法在 Shu-Osher 形式下可以写成：

$$
\boldsymbol{U}^{(i)} = \sum_{j=0}^{i-1} \alpha_{ij} \left( \boldsymbol{U}^{(j)} + \frac{\beta_{ij}}{\alpha_{ij}} \Delta t \mathcal{L}(\boldsymbol{U}^{(j)}) \right), \quad \text{for } 1 \le i \le s
$$

其中系数 $\alpha_{ij} \ge 0$, $\beta_{ij} \ge 0$ 且 $\sum_{j=0}^{i-1} \alpha_{ij} = 1$。括号内的项正是一个步长为 $(\beta_{ij}/\alpha_{ij})\Delta t$ 的前向欧拉步骤。整个表达式是一个凸组合。由于 TVD 等性质在凸组合下是封闭的，只要保证每个前向欧拉步骤都稳定，即 $(\beta_{ij}/\alpha_{ij})\Delta t \le \Delta t_{\text{FE}}$，那么整个 SSP-RK 方法也将保持稳定性。

为了满足所有阶段的所有项的这个条件，全局时间步长 $\Delta t$ 必须满足：

$$
\Delta t \le c \cdot \Delta t_{\text{FE}}, \quad \text{where} \quad c = \min_{i,j: \beta_{ij}>0} \frac{\alpha_{ij}}{\beta_{ij}}
$$

这个系数 $c$ 被称为 **SSP 系数**。它量化了 SSP 方法相对于前向欧拉法在保持稳定性方面的效率。[@problem_id:3317325]

一个经典的例子是二阶 SSPRK(2,2) 方法：
1.  $\boldsymbol{U}^{(1)} = \boldsymbol{U}^n + \Delta t \mathcal{L}(\boldsymbol{U}^n)$
2.  $\boldsymbol{U}^{n+1} = \frac{1}{2}\boldsymbol{U}^n + \frac{1}{2}\left( \boldsymbol{U}^{(1)} + \Delta t \mathcal{L}(\boldsymbol{U}^{(1)}) \right)$

这个方法可以被看作是两个前向欧拉步骤的凸组合。它的 SSP 系数 $c=1$，意味着它可以在与前向欧拉法相同的 CFL 约束下保持其稳定性（如 TVD 或保正性）。该方法的 Butcher Tableau 为 $c=[0, 1]^{\mathsf{T}}$, $A = \begin{pmatrix} 0  0 \\ 1  0 \end{pmatrix}$, $b = [1/2, 1/2]^{\mathsf{T}}$。它是一个二阶精度的时间积分方法，广泛用于求解双曲守恒律。[@problem_id:3317326] [@problem_id:3317325]

### 综合讨论：熵稳定性与收敛阶

#### 熵稳定性

TVD 条件是保证一维标量问题非振荡性的强大工具，但在多维问题和方程组上，其理论基础较弱。一个更基本、更物理的稳定性判据是 **熵稳定性** (entropy stability)。根据热力学第二定律，物理上真实的间断（激波）必须产生熵。一个数值格式应该模拟这种行为，即在光滑区域保持熵守恒，在激波处耗散熵。

对于欧拉方程，一个被证明是守恒变量 $\boldsymbol{U}$ 的严格凸函数的数学熵是 $\eta(\boldsymbol{U}) = -\rho s$，其中 $s = \ln(p\rho^{-\gamma})$ 是物理熵。对应的熵通量为 $q(\boldsymbol{U}) = -\rho s u$。一个数值通量 $\hat{\boldsymbol{F}}$ 被认为是半离散熵稳定的，如果它满足一个 Tadmor 型不等式，该不等式保证了在每个界面处数值熵的产生率不小于物理熵的通量差。这个局部条件可以被求和，从而保证在没有边界熵流入的情况下，总的数值熵是单调不减的（对应于物理熵）或单调不增的（对应于数学熵 $\eta$），从而确保了格式收敛到物理上正确的弱解。[@problem_id:3317314]

#### 全局收敛阶

最后，我们将所有部分结合起来，考虑整个数值方法的 **全局收敛阶**。对于采用龙格-库塔时间积分（$p$ 阶）和空间离散（$q$ 阶）的龙格－库塔方法，在时间 $T$ 的全局误差 $E(T)$ 可以被分解为空间误差和时间误差两部分。对于光滑解，误差上界可以表示为：

$$
E(T) \le C_1 \Delta t^p + C_2 \Delta x^q
$$

其中 $C_1$ 和 $C_2$ 是不依赖于步长的常数。总的收敛阶由这两个误差项中较慢的一个决定。

在显式格式中，$\Delta t$ 和 $\Delta x$ 通过 CFL 条件关联。通常我们取 $\Delta t = \text{const} \cdot \Delta x$。在这种情况下，误差变为：

$$
E(T) = O(\Delta x^p + \Delta x^q) = O(\Delta x^{\min(p,q)})
$$

这意味着方法的整体阶数是时间阶和空间阶中较低的那一个。例如，如果我们使用一个四阶空间格式（$q=4$）和一个二阶时间积分器（$p=2$），在固定的 CFL 数下，整体精度将只有二阶。在这种情况下，时间误差是瓶颈。反之，如果 $p>q$，则空间误差是瓶颈，整体阶数为 $q$。[@problem_id:3317377]

为了使空间和时间误差达到平衡，理论上可以选择 $\Delta t \propto \Delta x^{q/p}$。但这在实践中可能不切实际，因为 CFL 条件通常要求 $\Delta t \propto \Delta x$。因此，对于显式方法，通常的做法是选择时间积分器的阶数 $p$ 大于或等于空间格式的阶数 $q$，以确保空间精度不会被时间积分所限制。所有这些分析都建立在格式 **稳定性** 的前提之上，没有稳定性，即使格式是一致的，也无法保证收敛。[@problem_id:3317377]