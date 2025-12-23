## 引言
在使用[谱方法](@entry_id:141737)或间断伽辽金（DG）等[高阶方法](@entry_id:165413)对[偏微分方程](@entry_id:141332)进行空间离散后，我们面临着求解一个极大规模常微分方程（ODE）组的挑战。显式[龙格-库塔](@entry_id:140452)（RK）方法是推进这些系统随时间演化的标准工具，但其传统实现方式会消耗巨大的内存资源，成为大规模高精度模拟的主要瓶颈。为了解决这一关键问题，**低存储龙格-库塔（low-storage Runge-Kutta, LSRK）格式**应运而生，它通过精巧的[算法设计](@entry_id:634229)，在不牺牲精度和稳定性的前提下，将内存占用降至最低。

本文将系统地引导您掌握LSRK格式的理论与实践。我们将从基本原理出发，逐步深入到其在复杂科学计算中的高级应用。在**“原理与机制”**一章中，您将学习LSRK格式的[代数结构](@entry_id:137052)、内存节省的数学基础以及其精度与稳定性是如何被设计的。随后，**“应用与跨学科联系”**一章将展示这些方法在[流体动力学](@entry_id:136788)、计算电磁学等领域的实际效用，并探讨其与间断[伽辽金法](@entry_id:749698)（DG）等先进空间离散技术的深度融合。最后，通过**“动手实践”**部分提供的一系列挑战，您将有机会亲手实现和验证LSRK格式，将理论知识转化为解决实际问题的能力。让我们首先深入其核心，探究LSRK格式的原理与机制。

## 原理与机制

在通过[谱方法](@entry_id:141737)或间断伽辽金 (DG) 方法对[偏微分方程](@entry_id:141332)进行空间离散后，我们通常得到一个大规模[常微分方程](@entry_id:147024) (ODE) 组。[显式时间积分](@entry_id:165797)方案，特别是龙格-库塔 (Runge-Kutta, RK) 方法，是推进这些[半离散系统](@entry_id:754680)在时间上求解的常用工具。然而，传统 RK 方法的直接实现可能需要巨大的内存，这在求解高阶方法产生的大自由度问题时尤其具有挑战性。本章将深入探讨**低存储龙格-库塔 (low-storage [Runge-Kutta](@entry_id:140452), LSRK) 格式**的原理与机制，这类方法经过专门设计，旨在显著减少内存占用的同时保持[高阶精度](@entry_id:750325)和稳定性。

### [高阶方法](@entry_id:165413)的内存需求

为了理解低存储格式的必要性，我们首先要量化传统显式[龙格-库塔方法](@entry_id:144251)的内存成本。一个标准的 $s$ 阶显式[龙格-库塔方法](@entry_id:144251)，用于求解 ODE 系统 $\frac{d\boldsymbol{u}}{dt} = \mathcal{L}(\boldsymbol{u})$，其形式如下：

$$
\boldsymbol{k}_i = \mathcal{L} \left( \boldsymbol{u}^n + \Delta t \sum_{j=1}^{i-1} a_{ij} \boldsymbol{k}_j \right), \quad i=1, \dots, s
$$

$$
\boldsymbol{u}^{n+1} = \boldsymbol{u}^n + \Delta t \sum_{i=1}^{s} b_i \boldsymbol{k}_i
$$

其中 $\boldsymbol{u}^n \in \mathbb{R}^{N}$ 是在时间 $t^n$ 的解向量，$\boldsymbol{k}_i \in \mathbb{R}^{N}$ 是第 $i$ 个**阶段导数 (stage derivative)**，$N$ 是系统的总自由度。在标准的实现中，为了计算最终的解 $\boldsymbol{u}^{n+1}$，必须在整个时间步长内保留初始状态 $\boldsymbol{u}^n$ 以及所有的阶段导数 $\boldsymbol{k}_1, \dots, \boldsymbol{k}_s$。

因此，所需的总存储量（以长度为 $N$ 的向量数组数量计）为：
- 1 个数组用于存储初始解 $\boldsymbol{u}^n$。
- $s$ 个数组用于存储 $s$ 个阶段导数 $\boldsymbol{k}_i$。

总计需要 $s+1$ 个长度为 $N$ 的向量的存储空间 。对于 DG 或谱方法，自由度 $N$ 可能非常大（例如，$N = N_e (p+1)^d$，其中 $N_e$ 是单元数，$p$ 是多项式次数，$d$ 是空间维度）。当使用高阶 ($p$ 较大) 或高阶段数 ($s$ 较大) 的方法时，$s+1$ 个向量的存储需求可能变得过高，甚至超出计算硬件的内存容量。

低存储格式通过一种巧妙的代数重构，旨在仅使用固定数量（通常是 2 或 3 个）的寄存器（即长度为 $N$ 的工作数组）来完成整个时间步的更新。以最节省内存的**双寄存器 (two-register)** 或 "$2N$" 方案为例，它在整个步骤中仅使用两个长度为 $N$ 的向量。我们可以计算这种低存储方案与传统方案的内存使用量之比 $\chi(s)$ ：

$$
\chi(s) = \frac{\text{低存储方案内存}}{\text{传统方案内存}} = \frac{2N}{(s+1)N} = \frac{2}{s+1}
$$

这个简单的比率揭示了 LSRK 格式的巨大优势。例如，对于一个五阶方法（$s=5$），传统实现需要 $6N$ 的存储，而 $2N$ 的 LSRK 格式仅需 $2N$ 的存储，内存占用减少到原来的三分之一。这种显著的内存节省使得在内存受限的硬件上进行大规模、高精度的模拟成为可能。

### 低存储龙格-库塔格式的结构

LSRK 格式的核心思想是通过**原地 (in-place)** 更新来重用工作数组，从而避免存储所有的中间阶段导数。下面我们介绍两种最常见的 LSRK 变体 。

#### 双寄存器 (2N) 格式

双寄存器格式是最节省内存的变体，它仅使用两个长度为 $N$ 的数组：一个**解寄存器 (solution register)** $\boldsymbol{q}$ 和一个**残差寄存器 (residual register)** $\boldsymbol{r}$。一个典型的时间步更新流程如下：

首先，初始化解寄存器为当前时间步的初值，$\boldsymbol{q}^{(0)} = \boldsymbol{u}^n$，残差寄存器为零，$\boldsymbol{r}^{(0)} = \boldsymbol{0}$。然后，对于每个阶段 $i=1, \dots, s$，执行以下更新 ：

1.  **更新残差寄存器**: $\boldsymbol{r}^{(i)} = a_i \boldsymbol{r}^{(i-1)} + \Delta t \mathcal{L}(\boldsymbol{q}^{(i-1)})$
2.  **更新解寄存器**: $\boldsymbol{q}^{(i)} = \boldsymbol{q}^{(i-1)} + b_i \boldsymbol{r}^{(i)}$

在最后一个阶段后，$\boldsymbol{q}^{(s)}$ 即为新的解 $\boldsymbol{u}^{n+1}$。在这个过程中，$\boldsymbol{r}$ 寄存器累积了先前阶段残差的加权和，而 $\boldsymbol{q}$ 寄存器则被逐步、原地更新。注意，由于 $\boldsymbol{q}^{(0)}$ 在第一个阶段就被覆盖，初始解 $\boldsymbol{u}^n$ 不被保留。

这种格式的一个重要特性是**守恒性**。如果空间算子 $\mathcal{L}$ 是守恒的（即某个线性泛函 $L$ 作用于其上为零，$L(\mathcal{L}(\boldsymbol{v}))=0$），那么该 LSRK 格式也是守恒的。这是因为每个阶段的更新都是对先前守恒状态的增量修正，而这些增量最终都源于 $\mathcal{L}$ 的求值 。

通过展开递归关系，我们可以看到最终的解更新 $\boldsymbol{u}^{n+1} - \boldsymbol{u}^n$ 是如何由各个阶段的“裸”残差 $\boldsymbol{k}_j := \Delta t \mathcal{L}(\boldsymbol{q}^{(j-1)})$ 构成的 。总更新量可以表示为：

$$
\boldsymbol{u}^{n+1} - \boldsymbol{u}^n = \sum_{i=1}^{s} (\boldsymbol{q}^{(i)} - \boldsymbol{q}^{(i-1)}) = \sum_{i=1}^{s} b_i \boldsymbol{r}^{(i)}
$$

而 $\boldsymbol{r}^{(i)}$ 本身是 $\boldsymbol{k}_1, \dots, \boldsymbol{k}_i$ 的线性组合。例如，对于 $s=4$ 的情况，$\boldsymbol{k}_1$ 对总更新的贡献系数为：

$$
\text{Coefficient of } \boldsymbol{k}_1 = b_1 + a_2 b_2 + a_2 a_3 b_3 + a_2 a_3 a_4 b_4
$$

这表明，通过适当地选择系数 $\{a_i\}$ 和 $\{b_i\}$，LSRK 格式可以精确地重现任何标准显式 RK 方法的[代数结构](@entry_id:137052)，从而达到相同的精度和稳定性。

#### 三寄存器 (3N) 格式

三寄存器格式牺牲了少量内存以换取更大的代数灵活性，使得更多种类的 RK 方法可以被表示为低存储形式。它使用三个寄存器：

-   $\boldsymbol{u}$: 当前演化的阶段解。
-   $\boldsymbol{u}^n$: 时间步开始时的“冻结”解。
-   $\boldsymbol{w}$: 一个工作数组，通常用于存储阶段导数 $\mathcal{L}(\boldsymbol{u})$。

一个通用的阶段更[新形式](@entry_id:199611)如下：对于 $i=1, \dots, s$：

1.  **计算阶段导数**: $\boldsymbol{w} \leftarrow \mathcal{L}(\boldsymbol{u})$
2.  **更新解**: $\boldsymbol{u} \leftarrow \alpha_i \boldsymbol{u} + \beta_i \boldsymbol{u}^n + \gamma_i \Delta t \boldsymbol{w}$

这里，系数 $\alpha_i, \beta_i, \gamma_i$ 被选择以匹配目标 RK 方法的 Butcher 表。由于需要在更新时同时访问 $\boldsymbol{u}$, $\boldsymbol{u}^n$ 和 $\boldsymbol{w}$，该方法需要三个寄存器。

值得注意的是，无论算子 $\mathcal{L}$ 是线性的还是[非线性](@entry_id:637147)的，这些 LSRK 格式都同样适用，因为在每个阶段，$\mathcal{L}$ 总是作用于最新计算出的解向量 。

### 从第一性原理构建：精度和稳定性

LSRK 格式的系数 $\{a_i, b_i\}$ 等并非随意选择，它们必须满足特定的**[精度阶](@entry_id:145189)条件 (order conditions)**。我们可以通过将 LSRK 格式应用于线性标量测试方程 $\frac{dy}{dt} = \lambda y$ 来推导这些条件 。

考虑一个简单的双寄存器、两阶段格式，其更新规则为：
$$
w_1 = a_1 w_0 + \lambda y^n, \quad y_1 = y^n + b_1 h w_1
$$
$$
w_2 = a_2 w_1 + \lambda y_1, \quad y^{n+1} = y_1 + b_2 h w_2
$$
其中 $w_0=0$，$h$ 是时间步长，$z = h\lambda$。通过逐步代换，我们可以将 $y^{n+1}$ 表示为 $y^n$ 的倍数：

$w_1 = \lambda y^n$ （注意 $a_1$ 因为 $w_0=0$ 而不起作用）

$y_1 = y^n + b_1 h (\lambda y^n) = (1 + b_1 z) y^n$

$w_2 = a_2(\lambda y^n) + \lambda(y^n(1+b_1 z)) = \lambda y^n (a_2 + 1 + b_1 z)$

$y^{n+1} = y_1 + b_2 h w_2 = y^n(1+b_1 z) + b_2 z y^n (a_2+1+b_1 z)$

整理后得到 $y^{n+1} = R(z) y^n$，其中**稳定性多项式 (stability polynomial)** $R(z)$ 为：
$$
R(z) = 1 + (b_1 + b_2 + a_2 b_2)z + b_1 b_2 z^2
$$

为了使该格式达到**二阶精度**，其稳定性多项式 $R(z)$ 的[泰勒展开](@entry_id:145057)必须与精确解的指数函数 $\exp(z) = 1 + z + \frac{1}{2}z^2 + \mathcal{O}(z^3)$ 在 $z=0$ 处的展开匹配至 $z^2$ 项。比较系数可得阶条件：
1.  $z^1$ 的系数: $b_1 + b_2 + a_2 b_2 = 1$
2.  $z^2$ 的系数: $b_1 b_2 = \frac{1}{2}$

这个[方程组](@entry_id:193238)有三个未知数和两个方程，存在一族解。一个方便的选择是 $a_2 = -1/2$, $b_2 = 1$，由此可得 $b_1 = 1/2$。将阶条件代入 $R(z)$ 的一般表达式，我们发现任何满足这些条件的二阶格式都具有相同的稳定性多项式：

$$
R(z) = 1 + z + \frac{1}{2}z^2
$$

这恰好是标准二阶 RK 方法的稳定性多项式。这个过程展示了如何从基本原理出发，通过匹配[泰勒级数](@entry_id:147154)来设计一个满足特定精度要求的低存储格式。

### 高级主题与应用

LSRK 格式不仅是[内存优化](@entry_id:751872)的工具，它们还与其他重要的数值方法概念紧密相连，并在实际应用中展现出强大的适应性。

#### [强稳定性保持 (SSP)](@entry_id:755538) 格式

在求解包含激波或不连续的 hyperbolic 守恒律时，数值方法必须保持解的某些物理特性，例如[单调性](@entry_id:143760)或总变差不增 (TVD)。**强稳定性保持 (Strong Stability Preserving, SSP)** 方法是一类旨在保持这些性质的[高阶时间积分](@entry_id:750308)格式。

一个显式 RK 方法若能被写成一系列**前向欧拉步 (forward Euler steps)** 的**[凸组合](@entry_id:635830) (convex combination)**，则该方法是 SSP 的 。由 Shu 和 Osher 发展的理论表明，一个 $s$ 阶方法的每个阶段 $\boldsymbol{u}^{(i)}$ 都可以表示为：

$$
\boldsymbol{u}^{(i)} = \sum_{k=0}^{i-1}\alpha_{ik}\,\boldsymbol{u}^{(k)} + \sum_{k=0}^{i-1}\beta_{ik}\Big(\boldsymbol{u}^{(k)}+\frac{\Delta t}{C}\,\mathcal{L}(\boldsymbol{u}^{(k)})\Big)
$$

其中系数 $\alpha_{ik} \ge 0$, $\beta_{ik} \ge 0$，且对于每个阶段 $i$ 都有 $\sum_{k=0}^{i-1}(\alpha_{ik}+\beta_{ik})=1$。如果[前向欧拉法](@entry_id:141238)在时间步长 $\Delta t \le \Delta t_{\mathrm{FE}}$ 时是保持性质的，那么该 SSP-RK 方法在时间步长 $\Delta t \le C \cdot \Delta t_{\mathrm{FE}}$ 时也将保持该性质。这里的 $C$ 被称为**SSP 系数**。

许多流行的 LSRK 格式被设计为 SSP 的。一个经典的例子是三阶三步 SSP-RK 方法，它可以用低存储形式实现，其阶段更新如下 ：
- 阶段 1: $\boldsymbol{u}^{(1)} = \boldsymbol{u}^{n} + \Delta t\,\mathcal{L}(\boldsymbol{u}^{n})$
- 阶段 2: $\boldsymbol{u}^{(2)} = \frac{3}{4}\,\boldsymbol{u}^{n} + \frac{1}{4}\,\big(\boldsymbol{u}^{(1)} + \Delta t\,\mathcal{L}(\boldsymbol{u}^{(1)})\big)$
- 阶段 3: $\boldsymbol{u}^{n+1} = \frac{1}{3}\,\boldsymbol{u}^{n} + \frac{2}{3}\,\big(\boldsymbol{u}^{(2)} + \Delta t\,\mathcal{L}(\boldsymbol{u}^{(2)})\big)$

这个格式可以被证明是一个[凸组合](@entry_id:635830)，并且是一个高效的 SSP 时间积分器。

#### 实际应用中的稳定性分析

将 LSRK 方法应用于实际问题（如 DG 离散）时，必须确保数值稳定性。这要求将 RK 方法的稳定性域与空间离散算子 $\mathcal{L}$ 的谱（[特征值分布](@entry_id:194746)）相匹配。

以上述三阶 SSP-RK 方法为例 ，我们可以推导出其稳定性多项式为：
$$
R(z) = 1 + z + \frac{1}{2}z^2 + \frac{1}{6}z^3
$$
对于一个[耗散系统](@entry_id:151564)，算子 $\mathcal{L}$ 的[特征值](@entry_id:154894) $\lambda$ 位于复平面的左半部分。稳定性的保守要求是，对于所有相关的 $z = \lambda \Delta t$，必须有 $|R(z)| \le 1$。为了确定沿负实轴的稳定性边界，我们求解 $R(-r) = -1$，其中 $r = |\lambda| \Delta t > 0$：
$$
1 - r + \frac{1}{2}r^2 - \frac{1}{6}r^3 = -1 \quad \implies \quad r^3 - 3r^2 + 6r - 12 = 0
$$
该方程的实根约为 $r_s \approx 2.513$。这定义了该方法在负实轴上的稳定区间为 $[-2.513, 0]$。

对于 DG 方法，算子 $\mathcal{L}$ 的谱半径 $\rho = \max|\lambda|$ 通常有已知的界。例如，对于一维线性[平流方程](@entry_id:144869)，使用 $p$ 次多项式和[迎风格式](@entry_id:756374)，谱半径的界为 $\rho \approx (2p+1)a/h$，其中 $a$ 是波速，$h$ 是单元尺寸。为了保证稳定性，我们必须选择时间步长 $\Delta t$ 使得所有 $\lambda \Delta t$ 都在稳定域内。一个保守的稳定性条件是：
$$
\rho \Delta t \le r_s \quad \implies \quad \Delta t \le \frac{r_s}{\rho}
$$
通过这个过程，我们可以为给定的 DG 离散和 LSRK 方法计算出一个具体的、稳定的最大时间步长。

#### 隐式-显式 (IMEX) 低存储格式

当待解的 ODE 系统包含不同时间尺度的项（即刚性问题）时，纯显式方法会受到极其严格的[时间步长限制](@entry_id:756010)。一个常见的策略是将系统分裂为非刚性部分 $F(u)$ 和刚性部分 $G(u)$：
$$
\frac{du}{dt} = F(u) + G(u)
$$
并采用**隐式-显式 (IMEX)** 方法，即对 $F(u)$ 采用显式处理，对 $G(u)$ 采用隐式处理。低存储的思想可以扩展到 IMEX 框架 。

我们可以构建一个 IMEX-LSRK 格式，其中显式部分 $F(u)$ 采用双寄存器低存储形式，而隐式部分 $G(u)$ 采用一种高效的**对角隐式[龙格-库塔](@entry_id:140452) (Diagonally Implicit [Runge-Kutta](@entry_id:140452), DIRK)** 格式。在这种格式中，每个阶段的隐式求解都形如 $U^{(i)} - \gamma \Delta t G(U^{(i)}) = \text{已知右端项}$，这通常比全隐式方法更容易求解。

以最简单的单步 IMEX 格式（IMEX-Euler）为例，它将前向欧拉用于 $F(u)$，后向欧拉用于 $G(u)$：
$$
u^{n+1} = u^n + \Delta t F(u^n) + \Delta t G(u^{n+1})
$$
将其应用于线性测试方程 $u' = \lambda_f u + \lambda_g u$，并定义 $z_f = \Delta t \lambda_f$ 和 $z_g = \Delta t \lambda_g$，我们可以得到其放大因子 $R(z_f, z_g)$：
$$
u^{n+1}(1 - z_g) = u^n(1 + z_f) \quad \implies \quad R(z_f, z_g) = \frac{1 + z_f}{1 - z_g}
$$
这个[放大因子](@entry_id:144315)清晰地展示了 IMEX 方法的特点：稳定性受显式部分 $z_f$ 的限制（需要 $|1+z_f| \le |1-z_g|$），而对刚性部分 $z_g$ 则是 A-稳定的（对于 $\text{Re}(z_g) \le 0$ 稳定）。

#### 与其他数值组件的交互

在复杂的科学计算代码中，[时间积分](@entry_id:267413)器很少孤立存在。它需要与各种其他数值组件，如**[保正限制器](@entry_id:753610) (positivity-preserving limiters)** 或人为耗散机制，进行交互。LSRK 格式的阶段性结构使得在每个阶段应用这些操作成为可能。然而，这种交互会给格式的系数和允许的时间步长带来额外的约束 。例如，为了在每个 LSRK 阶段都保持解的非负性，可能需要对系数 $a_i, b_i$ 施加非负性等条件，并可能导致比仅考虑线性稳定性时更严格的[时间步长限制](@entry_id:756010)。设计一个鲁棒的数值方案需要仔细考虑所有这些组件之间的协同作用。