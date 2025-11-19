## 引言
在计算科学与工程领域，尤其是在[计算流体动力学](@entry_id:147500)（CFD）中，[偏微分方程](@entry_id:141332)（PDEs）通过[空间离散化](@entry_id:172158)后，往往会转化为大规模的常微分方程（ODEs）系统。如何高效、稳定且准确地对这些ODE系统进行[时间积分](@entry_id:267413)，是决定数值模拟成败的关键。[线性多步法](@entry_id:139528)（Linear Multistep Methods, LMMs）作为一类经典且功能强大的[时间积分方法](@entry_id:136323)，为此提供了坚实的理论框架和丰富的实践工具。然而，面对众多LMM（如Adams法、BDF法）以及显式与隐式之分，如何根据问题的物理特性（如刚性）和精度要求做出正确选择，构成了一个核心的知识挑战。

本文旨在系统性地剖析[线性多步法](@entry_id:139528)的公式化、理论基础及其在复杂问题中的应用。我们将从“原理与机制”一章开始，深入探讨LMM的一般形式、两大族系（Adams与BDF）的[构造原理](@entry_id:141667)，并详细阐述收敛性、稳定性和精度背后的数学理论，包括关键的Dahlquist定理。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些理论如何通过线方法应用于CFD，分析谱特性如何决定稳定性，并探讨IMEX等高级格式在多物理场问题中的威力。最后，“实践练习”部分将提供具体问题，帮助读者将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，读者将能够全面掌握[线性多步法](@entry_id:139528)的精髓，并具备在科学研究和工程实践中灵活应用这些方法的能力。

## 原理与机制

在通过数值方法求解由[偏微分方程](@entry_id:141332)（例如，[流体动力学](@entry_id:136788)中的[Navier-Stokes方程](@entry_id:161487)）通过[空间离散化](@entry_id:172158)（如有限差分、有限体积或有限元方法）产生的[常微分方程](@entry_id:147024)（ODE）系统时，[时间积分方法](@entry_id:136323)的选择至关重要。这些[常微分方程](@entry_id:147024)系统通常形式为 $\frac{d\boldsymbol{y}}{dt} = \boldsymbol{f}(\boldsymbol{y}, t)$，其中 $\boldsymbol{y}(t) \in \mathbb{R}^m$ 是包含所有空间自由度的解向量，$m$ 通常非常大。[线性多步法](@entry_id:139528)（Linear Multistep Methods, LMMs）为求解这类问题提供了一个经典且强大的框架。本章旨在系统地阐述[线性多步法](@entry_id:139528)的基本原理、关键机制及其在计算流体动力学（CFD）中的应用背景。

### [线性多步法](@entry_id:139528)的一般形式

[线性多步法](@entry_id:139528)通过利用先前若干个时间步的解信息来近似当前时间步的解。一个通用的 $k$ 步[线性多步法](@entry_id:139528)可以表示为：

$$
\sum_{j=0}^{k} \alpha_j \boldsymbol{y}_{n-j} = h \sum_{j=0}^{k} \beta_j \boldsymbol{f}_{n-j}
$$

其中：
- $\boldsymbol{y}_{n-j}$ 是在时间点 $t_{n-j} = t_0 + (n-j)h$ 处对真实解 $\boldsymbol{y}(t_{n-j})$ 的数值近似。
- $h$ 是固定的时间步长。
- $\boldsymbol{f}_{n-j}$ 是对导数项 $\boldsymbol{f}(\boldsymbol{y}(t_{n-j}), t_{n-j})$ 的近似，通常计算为 $\boldsymbol{f}(\boldsymbol{y}_{n-j}, t_{n-j})$。
- $\alpha_j$ 和 $\beta_j$ 是定义特定方法的[实数系](@entry_id:157774)数。为确保唯一性，通常进行归一化处理，例如 $\alpha_0=1$。

为了求解新的解 $\boldsymbol{y}_n$，我们将上式重排，把包含 $\boldsymbol{y}_n$ 的项移到等式左边，而已知历史信息的项移到右边：

$$
\alpha_0 \boldsymbol{y}_n - h \beta_0 \boldsymbol{f}(\boldsymbol{y}_n, t_n) = - \sum_{j=1}^{k} \alpha_j \boldsymbol{y}_{n-j} + h \sum_{j=1}^{k} \beta_j \boldsymbol{f}_{n-j}
$$

这个方程揭示了显式和隐式方法之间的根本区别 [@problem_id:3340811]。

- **显式（Explicit）方法**：如果系数 $\beta_0=0$，则 $\boldsymbol{f}(\boldsymbol{y}_n, t_n)$ 项从方程中消失。在 $\alpha_0 \neq 0$ 的标准条件下，我们可以直接求解 $\boldsymbol{y}_n$：
  $$
  \boldsymbol{y}_n = \frac{1}{\alpha_0} \left( - \sum_{j=1}^{k} \alpha_j \boldsymbol{y}_{n-j} + h \sum_{j=1}^{k} \beta_j \boldsymbol{f}_{n-j} \right)
  $$
  此公式完全由已知的过去值 $\{ \boldsymbol{y}_{n-j} \}_{j=1}^k$ 和 $\{ \boldsymbol{f}_{n-j} \}_{j=1}^k$ 构成，计算成本低廉。因此，当且仅当 $\beta_0 = 0$ 时，方法是显式的。

- **隐式（Implicit）方法**：如果系数 $\beta_0 \neq 0$，则待求解的 $\boldsymbol{y}_n$ 同时出现在线性项 $\alpha_0 \boldsymbol{y}_n$ 和（通常是）[非线性](@entry_id:637147)的 $\boldsymbol{f}(\boldsymbol{y}_n, t_n)$ 项中。这构成了一个关于 $\boldsymbol{y}_n$ 的[代数方程](@entry_id:272665)组，通常需要通过迭代方法（如[牛顿法](@entry_id:140116)）求解，计算成本较高。即使 $\boldsymbol{f}$ 是线性的（例如 $\boldsymbol{f}(\boldsymbol{y}) = A\boldsymbol{y}$），求解也需要解一个线性系统 $(\alpha_0 I - h \beta_0 A)\boldsymbol{y}_n = \dots$，这仍然超出了“直接计算”的范畴。

### LMM的两大族系：[构造原理](@entry_id:141667)

[线性多步法](@entry_id:139528)通常通过两种不同的策略导出：基于积分的Adams法和基于[微分](@entry_id:158718)的[后向差分](@entry_id:637618)格式（BDF）。

#### Adams方法：基于积分的构造

Adams方法源于对常微分方程积分形式的逼近：
$$
\boldsymbol{y}(t_{n+1}) = \boldsymbol{y}(t_n) + \int_{t_n}^{t_{n+1}} \boldsymbol{f}(\boldsymbol{y}(t), t) \, dt
$$
其核心思想是用一个多项式 $P(t)$ 来近似积分项中的函数 $\boldsymbol{f}$，然后精确地积分该多项式。

- **[Adams-Bashforth](@entry_id:168783) (AB) 方法**：这是显式Adams方法族。它通过历史数据点 $\{ (t_{n-j}, \boldsymbol{f}_{n-j}) \}_{j=0}^{k-1}$ 来构造一个[插值多项式](@entry_id:750764)。例如，要构造三步[Adams-Bashforth](@entry_id:168783) (AB3) 方法，我们用一个二次多项式 $P_2(t)$ 插值于点 $(t_n, \boldsymbol{f}_n)$、$(t_{n-1}, \boldsymbol{f}_{n-1})$ 和 $(t_{n-2}, \boldsymbol{f}_{n-2})$ [@problem_id:3340866]。通过在 $[t_n, t_{n+1}]$ 区间上积分这个多项式，可以推导出更新公式：
  $$
  \boldsymbol{y}_{n+1} = \boldsymbol{y}_n + \int_{t_n}^{t_{n+1}} P_2(t) \, dt = \boldsymbol{y}_n + h \left( \frac{23}{12}\boldsymbol{f}_n - \frac{16}{12}\boldsymbol{f}_{n-1} + \frac{5}{12}\boldsymbol{f}_{n-2} \right)
  $$
  这里的系数 $(\beta_1, \beta_2, \beta_3)$ (注意索引与通用公式的差异) 是通过对[拉格朗日基多项式](@entry_id:168175)进行积分得到的。由于插值点不包含未知的 $t_{n+1}$，所以此方法是显式的。

- **[Adams-Moulton](@entry_id:164339) (AM) 方法**：这是隐式Adams方法族。其构造方式与AB方法类似，但用于插值 $\boldsymbol{f}$ 的多项式也包含了未来的点 $(t_{n+1}, \boldsymbol{f}_{n+1})$。例如，三阶[Adams-Moulton](@entry_id:164339) (AM3) 方法使用通过 $(t_{n+1}, \boldsymbol{f}_{n+1})$、$(t_n, \boldsymbol{f}_n)$ 和 $(t_{n-1}, \boldsymbol{f}_{n-1})$ 的二次多项式 [@problem_id:3340813]。这导致了一个[隐式方程](@entry_id:177636)，因为 $\boldsymbol{f}_{n+1}$ 依赖于待求的 $\boldsymbol{y}_{n+1}$。

#### [后向差分公式](@entry_id:175714) (BDF)：基于[微分](@entry_id:158718)的构造

[BDF方法](@entry_id:176038)采用不同的策略。它直接近似[微分算子](@entry_id:140145) $y'$。其核心思想是：用一个多项式 $P(t)$ 插值于历史解点和当前解点 $\{ (t_{n-j}, \boldsymbol{y}_{n-j}) \}_{j=0}^k$，然后强制要求该多项式在最新时间点 $t_n$ 的导数等于 $\boldsymbol{f}_n$：
$$
P'(t_n) = \boldsymbol{f}_n
$$
由于插值点中包含了待求的 $\boldsymbol{y}_n$，且 $\boldsymbol{f}_n = \boldsymbol{f}(\boldsymbol{y}_n, t_n)$，因此所有非平凡的[BDF方法](@entry_id:176038)都是隐式的。

例如，要构造4步[后向差分公式](@entry_id:175714)（BDF4），我们需要找到一个唯一的4次多项式 $P(t)$，它穿过五个点 $(\boldsymbol{y}_n, \boldsymbol{y}_{n-1}, \boldsymbol{y}_{n-2}, \boldsymbol{y}_{n-3}, \boldsymbol{y}_{n-4})$，然后设置 $P'(t_n) = \boldsymbol{f}_n$ [@problem_id:3340803]。这个过程会产生一个形如 $\alpha_0 \boldsymbol{y}_n + \alpha_1 \boldsymbol{y}_{n-1} + \dots + \alpha_4 \boldsymbol{y}_{n-4} = h \beta_0 \boldsymbol{f}_n$ 的关系式。对于[BDF方法](@entry_id:176038)，$\beta_0$ 是唯一的非零 $\beta$ 系数。对于BDF4，归一化后的系数为：
$$
25\boldsymbol{y}_n - 48\boldsymbol{y}_{n-1} + 36\boldsymbol{y}_{n-2} - 16\boldsymbol{y}_{n-3} + 3\boldsymbol{y}_{n-4} = 12h \boldsymbol{f}_n
$$

### LMM的理论基础：收敛性、稳定性和精度

一个数值方法的价值取决于它是否收敛，即当步长 $h \to 0$ 时，数值解是否趋近于真实的[微分方程](@entry_id:264184)解。对于LMM，收敛性由两个核心属性决定：相容性（consistency）和[零稳定性](@entry_id:178549)（zero-stability）。

#### 相容性与精度阶

**相容性**直观上意味着离散格式在 $h \to 0$ 的极限情况下能够还原为原始的[微分方程](@entry_id:264184)。更形式化地，我们通过**[局部截断误差](@entry_id:147703) (Local Truncation Error, LTE)** 来衡量。LTE是在将真实解 $y(t)$ 代入数值格式时产生的残差。对于在 $t_{n+1}$ 处的格式 $\sum_{j=0}^{k} \alpha_j y_{n+1-j} = h \sum_{j=0}^{k} \beta_j f_{n+1-j}$，LTE $\tau_{n+1}$ 定义为 [@problem_id:3340813]：
$$
\tau_{n+1} = \sum_{j=0}^{k} \alpha_j y(t_{n+1-j}) - h \sum_{j=0}^{k} \beta_j y'(t_{n+1-j})
$$
如果当 $h \to 0$ 时，$\frac{\tau_{n+1}}{h} \to 0$，则称该方法是相容的。

方法的**精度阶 (order of accuracy)** $p$ 是一个整数，它量化了LTE随 $h$ 减小的速率。如果 $\tau_{n+1} = \mathcal{O}(h^{p+1})$，则称该方法具有 $p$ 阶精度。为了确定[精度阶](@entry_id:145189)，我们可以通过泰勒展开，或者更方便地，测试该方法对多项式解 $y(t)=t^m$ 的精确性 [@problem_id:3340853]。一个方法具有 $p$ 阶精度的充要条件是它对所有次数不高于 $p$ 的多项式都是精确的。这引出了一系列关于系数 $\alpha_j$ 和 $\beta_j$ 的代数条件。
- $m=0$: $\sum_{j=0}^k \alpha_j = 0$
- $m=1, \dots, p$: $\sum_{j=0}^k \alpha_j j^m = m \sum_{j=0}^k \beta_j j^{m-1}$ (在使用特定索引形式时)

相容性等价于方法至少为1阶精度，这要求 $\rho(1)=0$ 和 $\rho'(1)=\sigma(1)$，其中 $\rho$ 和 $\sigma$ 是下面将要介绍的特征多项式 [@problem_id:3340886]。

#### [零稳定性](@entry_id:178549)与根条件

**[零稳定性](@entry_id:178549)**是LMM的一个内在属性，它保证当 $h \to 0$ 时，数值解不会因为微小的扰动（如[舍入误差](@entry_id:162651)）而发生无界增长。这个概念通过考察方法在求解最简单的ODE $y'=0$ 时的行为来分析。此时，LMM简化为一个齐次差分方程：
$$
\sum_{j=0}^{k} \alpha_j \boldsymbol{y}_{n-j} = \mathbf{0}
$$
这个方程的解的行为由其**第一[特征多项式](@entry_id:150909)** $\rho(\zeta)$ 的根决定 [@problem_id:3340871]：
$$
\rho(\zeta) = \sum_{j=0}^{k} \alpha_j \zeta^{k-j}
$$
为了使解序列 $\{\boldsymbol{y}_n\}$ 有界，$\rho(\zeta)$ 的所有根 $\zeta_i$ 必须满足**Dahlquist根条件** [@problem_id:3340886]：
1.  所有根的模不大于1，即 $|\zeta_i| \le 1$。
2.  任何模为1的根都必须是单根（非[重根](@entry_id:151486)）。

如果存在模大于1的根，解会指数增长；如果存在模为1的[重根](@entry_id:151486)，解会[多项式增长](@entry_id:177086)。任何一种情况都意味着不稳定。重要的是，[零稳定性](@entry_id:178549)仅由 $\alpha_j$ 系数决定，与 $\beta_j$ 系数、步长 $h$ 或具体问题 $\boldsymbol{f}$ 无关。

例如，[BDF方法](@entry_id:176038)族的一个著名性质是，只有当步数 $k \le 6$ 时它们才是零稳定的。对于BDF7，其第一特征多项式 $\rho(\zeta)$ 的根中存在模大于1的根，因此BDF7不是一个可用的方法 [@problem_id:3340884]。

#### 收敛性：[Dahlquist等价定理](@entry_id:634938)

收敛性、相容性和[零稳定性](@entry_id:178549)之间的关系由**[Dahlquist等价定理](@entry_id:634938)**完美地阐述 [@problem_id:3340886]：
> 对于一个满足适当初始条件的[线性多步法](@entry_id:139528)，如果它作用于一个满足[Lipschitz条件](@entry_id:153423)的[常微分方程](@entry_id:147024)[初值问题](@entry_id:144620)，那么该方法是收敛的，当且仅当它是相容的且是零稳定的。

这个定理是[数值分析](@entry_id:142637)的基石。它将复杂的收敛性[问题分解](@entry_id:272624)为两个更易于验证的独立部分：相容性（与精度相关）和[零稳定性](@entry_id:178549)（与稳定性相关）。一个方法即使精度很高（相容），但如果不是零稳定的，其计算结果也将毫无意义。

### [刚性问题](@entry_id:142143)与[绝对稳定性](@entry_id:165194)

在许多[CFD应用](@entry_id:144462)中，尤其是在模拟[粘性流](@entry_id:136330)或[化学反应](@entry_id:146973)时，ODE系统是**刚性的 (stiff)**。这意味着解的不同分量以悬殊的时间尺度演化。对于这类问题，[零稳定性](@entry_id:178549)不足以保证在实际（即有限的）步长 $h$ 下的良好行为。我们需要**[绝对稳定性](@entry_id:165194)**的概念。

[绝对稳定性](@entry_id:165194)通过将LMM应用于标准测试方程 $y' = \lambda y$ 来分析，其中 $\lambda$ 是一个复数。将LMM应用于此方程，并设 $z = h\lambda$，可以得到一个关于放大因子 $\xi$ 的特征方程 [@problem_id:3340841]：
$$
\rho(\xi) - z \sigma(\xi) = 0
$$
其中 $\rho(\xi)$ 和 $\sigma(\xi)$ 是LMM的两个特征多项式（注意这里 $\xi$ 的定义可能与零稳定性分析中的 $\zeta$ 有所不同，但本质是研究特征根）。方法的**绝对稳定区域** $\mathcal{A}$ 是复平面上所有 $z$ 值的集合，对于这些 $z$，上述特征方程的所有根 $\xi_i$ 都满足 $|\xi_i| \le 1$ （且模为1的根是单根）。

对于[刚性问题](@entry_id:142143)，我们希望数值方法的绝对稳定区域尽可能大，特别是要包含左半复平面（因为刚性系统的[特征值](@entry_id:154894) $\lambda$ 通常具有大的负实部）。

#### [A-稳定性](@entry_id:144367)与[Dahlquist第二障碍](@entry_id:173749)

一个理想的性质是**[A-稳定性](@entry_id:144367)**，即方法的绝对稳定区域包含整个左半复平面 $\text{Re}(z) \le 0$。这意味着无论问题有多刚硬（即 $\text{Re}(\lambda)$ 有多大的负值），只要步长 $h$ 合理，数值解都会保持稳定。

- **梯形法则 (Trapezoidal Rule)** 是一个典型的[A-稳定方法](@entry_id:746185)。它是二阶[Adams-Moulton方法](@entry_id:144250)，其更新公式为 $\boldsymbol{y}_{n+1} - \boldsymbol{y}_n = \frac{h}{2}(\boldsymbol{f}_{n+1} + \boldsymbol{f}_n)$。其[稳定性函数](@entry_id:178107)为 $R(z) = \frac{1+z/2}{1-z/2}$，绝对稳定区域恰好是整个左半平面 [@problem_id:3340841]。

然而，LMM的[A-稳定性](@entry_id:144367)受到一个根本性的限制，即**[Dahlquist第二障碍](@entry_id:173749)** [@problem_id:3287775]：
> 一个A-稳定的[线性多步法](@entry_id:139528)，其[精度阶](@entry_id:145189) $p$ 不能超过2。

这个定理揭示了LMM在精度和稳定性之间的一个深刻的权衡。你无法同时拥有[A-稳定性](@entry_id:144367)和高于二阶的精度。二阶的梯形法则和BDF2方法都是达到这个界限的例子。这也是为什么高阶的Adams方法（如AM3）都不是A-稳定的原因。

#### [L-稳定性](@entry_id:143644)与[高频耗散](@entry_id:750292)

对于极刚问题，我们甚至可能需要比[A-稳定性](@entry_id:144367)更强的性质。**[L-稳定性](@entry_id:143644)**要求一个方法是A-稳定的，并且其[稳定性函数](@entry_id:178107) $R(z)$ 在 $z \to \infty$ 时趋于零：
$$
\lim_{\text{Re}(z) \to -\infty} |R(z)| = 0
$$
这个性质在CFD中非常有用，因为它意味着对应于极大负实部[特征值](@entry_id:154894)（代表极快衰减的物理模式或高频数值噪声）的解分量会被数值格式迅速地、几乎在一个时间步内完全抑制。

- **BDF2** 方法是L-稳定的。其[稳定性函数](@entry_id:178107)在无穷远处趋于0 [@problem_id:3340812]。这使得[BDF方法](@entry_id:176038)（尤其是BDF1和BDF2）在求解[扩散](@entry_id:141445)主导的[刚性问题](@entry_id:142143)时非常受欢迎，因为它们能有效地耗散掉由高[波数](@entry_id:172452)引起的不稳定性。
- 相比之下，[梯形法则](@entry_id:145375)只是A-稳定的，而不是L-稳定的，因为当 $\text{Re}(z) \to -\infty$ 时，其[稳定性函数](@entry_id:178107) $|R(z)| \to 1$。这意味着它不会衰减最刚硬的分量，可能导致数值解中出现持续的、非物理的[振荡](@entry_id:267781)。

综上所述，[线性多步法](@entry_id:139528)的选择是一个涉及计算成本（显式 vs. 隐式）、精度阶、[零稳定性](@entry_id:178549)、以及针对问题刚性的[绝对稳定性](@entry_id:165194)（[A-稳定性](@entry_id:144367)或[L-稳定性](@entry_id:143644)）的复杂决策过程。理解这些基本原理和机制对于在计算科学与工程中成功应用数值方法至关重要。