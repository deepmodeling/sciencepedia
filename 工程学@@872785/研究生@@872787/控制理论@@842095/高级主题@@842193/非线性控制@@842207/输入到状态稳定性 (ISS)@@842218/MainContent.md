## 引言
在复杂的现实世界中，几乎所有工程和物理系统本质上都是[非线性](@entry_id:637147)的，并且持续受到外部扰动或控制输入的影响。传统的[稳定性理论](@entry_id:149957)，如针对无输入系统的[渐近稳定性](@entry_id:149743)，往往无法保证系统在面对这些外部影响时的鲁棒性，甚至一个微小的[持续扰动](@entry_id:197989)也可能导致系统崩溃。为了弥补这一关键的理论空白，输入到状态稳定性（Input-to-State Stability, ISS）理论应运而生，它已成为现代[非线性](@entry_id:637147)控制理论的基石。

ISS提供了一个强大而严谨的数学框架，用以精确刻画系统状态如何同时受到初始条件和外部输入的双重影响。它不仅推广了经典稳定性概念，更重要的是为分析和设计在不确定环境下可靠工作的控制系统提供了定量工具。本文旨在为读者提供一份关于ISS理论的系统性指南，从核心原理到前沿应用，层层递进，深入浅出。

为此，本文组织为三个核心章节。在“**原理与机制**”中，我们将从ISS的严格数学定义出发，揭示其与经典稳定性的深刻联系，并详细介绍作为其核心分析工具的ISS-[李雅普诺夫方法](@entry_id:635639)。接下来，在“**应用与[交叉](@entry_id:147634)学科联系**”中，我们将展示ISS理论的广泛影响力，探讨它如何为[鲁棒控制](@entry_id:260994)、网络化系统、[模型预测控制](@entry_id:146965)乃至混杂和[无穷维系统](@entry_id:170904)提供统一的分析语言。最后，通过“**动手实践**”中的一系列引导性练习，读者将有机会亲手应用所学知识，解决具体的[稳定性分析](@entry_id:144077)问题，从而将理论内化为技能。让我们首先进入第一章，探索ISS的基本原理。

## 原理与机制

引言部分介绍了在存在外部扰动或控制输入时分析[非线性系统稳定性](@entry_id:178090)的必要性。本章将深入探讨输入到状态稳定性（Input-to-State Stability, ISS）的核心原理和关键机制。我们将从其形式化定义出发，揭示它与经典稳定性概念的联系与区别，然后介绍作为其核心分析工具的[Lyapunov方法](@entry_id:635639)，最后讨论ISS理论的一些重要扩展。

### 输入到状态稳定性的核心定义

考虑一个由常微分方程描述的[非线性](@entry_id:637147)控制系统：
$$
\dot{x} = f(x, u)
$$
其中 $x \in \mathbb{R}^{n}$ 是系统状态，而 $u \in \mathbb{R}^{m}$ 是外部输入。为了确保解的[适定性](@entry_id:148590)，我们通常假设向量场 $f$ 在 $(x, u)$ 上是连续的，并且关于 $x$ 是局部Lipschitz的。

输入到状态稳定性（**Input-to-State Stability, ISS**）为我们提供了一个精确的数学框架，用以刻画系统状态如何同时受到初始[状态和](@entry_id:193625)外部输入的影响。在形式上，一个系统被称为ISS，如果其状态范数 $|x(t)|$ 的演化可以被一个由两部分组成的界限所约束：一部分描述了初始条件影响的衰减过程，另一部分则刻画了输入幅值对状态的持续影响。

为了精确表述，我们需要引入几类特殊的**比较函数**：

*   **$\mathcal{K}$[类函数](@entry_id:146970)**：一个[连续函数](@entry_id:137361) $\alpha: [0, \infty) \to [0, \infty)$ 被称为 $\mathcal{K}$ 类函数，如果它是严格递增的且 $\alpha(0)=0$。
*   **$\mathcal{K}_{\infty}$[类函数](@entry_id:146970)**：如果一个 $\mathcal{K}$ [类函数](@entry_id:146970) $\alpha$ 还满足当 $r \to \infty$ 时 $\alpha(r) \to \infty$，则称其为 $\mathcal{K}_{\infty}$ [类函数](@entry_id:146970)。
*   **$\mathcal{KL}$[类函数](@entry_id:146970)**：一个函数 $\beta: [0, \infty) \times [0, \infty) \to [0, \infty)$ 被称为 $\mathcal{KL}$ [类函数](@entry_id:146970)，如果对于每个固定的时间 $t \ge 0$，映射 $\beta(\cdot, t)$ 是一个 $\mathcal{K}$ [类函数](@entry_id:146970)；而对于每个固定的 $s > 0$，映射 $\beta(s, \cdot)$ 是递减的，并且当 $t \to \infty$ 时，$\beta(s, t) \to 0$。

借助这些比较函数，我们可以给出ISS的严格定义。系统 $\dot{x} = f(x, u)$ 被认为是**输入到状态稳定的**，如果存在一个 $\mathcal{KL}$ [类函数](@entry_id:146970) $\beta$ 和一个 $\mathcal{K}$ 类函数 $\gamma$，使得对于任意初始状态 $x(0) = x_0$ 和任意**可测且局部本质有界**的输入 $u(t)$，系统的解 $x(t)$ 对所有 $t \ge 0$ 存在，并满足如下不等式：
$$
|x(t)| \le \beta(|x_0|, t) + \gamma\left(\operatorname{ess\,sup}_{0 \le \tau \le t} |u(\tau)|\right)
$$
这里，$\operatorname{ess\,sup}_{0 \le \tau \le t} |u(\tau)|$ 表示输入 $u$ 在时间区间 $[0, t]$ 上的**[本质上确界](@entry_id:186689)**范数，通常记为 $\|u\|_{L_{\infty}(0,t)}$。[@problem_id:2712852]

我们来剖析这个核心不等式：

1.  **瞬态项 $\beta(|x_0|, t)$**：这一项描述了系统响应中源于初始条件 $x_0$ 的部分。由于 $\beta$ 是一个 $\mathcal{KL}$ [类函数](@entry_id:146970)，对于任意给定的初始状态大小 $|x_0|$，当时间 $t \to \infty$ 时，$\beta(|x_0|, t)$ 将衰减至零。这表明[初始条件](@entry_id:152863)的影响会随着时间的推移而消失。

2.  **渐近增益项 $\gamma(\lVert u\rVert_{L_{\infty}(0,t)})$**：这一项量化了输入对状态的持续影响。函数 $\gamma$ 被称为系统的**渐近增益**。由于 $\gamma$ 是一个 $\mathcal{K}$ 类函数，它满足 $\gamma(0)=0$，并且随其[自变量](@entry_id:267118)的增大而增大。这意味着，如果输入信号的幅值很小（即 $\lVert u\rVert_{L_{\infty}(0,t)}$ 很小），那么状态最终将被限制在一个靠近原点的小邻域内。特别地，如果输入为零，此项也为零。

值得注意的是，ISS的定义要求对可测输入成立。对于这类输入，在[测度为零](@entry_id:137864)的时间点集上可能出现无穷大的“尖峰”。使用**[本质上确界](@entry_id:186689)**（essential supremum）范数而非普通上确界（supremum）是至关重要的，因为它能忽略这些不影响系统积分轨迹的[零测集](@entry_id:157694)上的病态行为，从而使得对输入大小的衡量更加鲁棒和切合实际。[@problem_id:2712852]

### 与经典稳定性的关系：鲁棒性的视角

ISS的一个优美之处在于它自然地推广了经典的稳定性概念。考虑当系统不受任何外部输入影响，即 $u(t) \equiv 0$ 的情况。此时，输入的[本质上确界](@entry_id:186689)范数为零，即 $\lVert u\rVert_{L_{\infty}(0,t)} = 0$。由于增益函数 $\gamma$ 是 $\mathcal{K}$ [类函数](@entry_id:146970)，我们有 $\gamma(0)=0$。因此，ISS不等式退化为：
$$
|x(t)| \le \beta(|x_0|, t)
$$
这个不等式正是**全局[渐近稳定](@entry_id:168077)（Global Asymptotic Stability, GAS）**的现代定义。$\mathcal{KL}$ [类函数](@entry_id:146970) $\beta$ 的性质同时保证了[Lyapunov稳定性](@entry_id:147734)和全局吸引性。因此，一个直接的结论是：**如果一个系统是ISS的，那么其无输入（$u \equiv 0$）时的系统 $\dot{x} = f(x, 0)$ 必然是全局[渐近稳定](@entry_id:168077)的**。[@problem_id:2713219]

然而，反过来的结论是否成立？即，一个无输入时GAS的系统，在受到外部输入时是否总能保持某种形式的稳定性？答案是否定的，而这正是ISS概念强大之处的体现。GAS本身并不保证系统在面对外部扰动时的鲁棒性。

考虑以下这个简单的一维[非线性系统](@entry_id:168347)：[@problem_id:2722269]
$$
\dot{x} = -x + x^2 u(t)
$$
首先，考察其内部稳定性。当输入 $u(t) \equiv 0$ 时，系统简化为 $\dot{x} = -x$。这是一个线性[稳定系统](@entry_id:180404)，其原点是全局指数稳定的，因此也是GAS的。我们可以使用Lyapunov函数 $V(x) = \frac{1}{2}x^2$ 来验证这一点，其导数 $\dot{V} = x\dot{x} = x(-x) = -x^2$ 是负定的。

现在，我们引入一个非常小的、恒定的正输入，例如 $u(t) \equiv \bar{u}$，其中 $\bar{u} > 0$。系统变为：
$$
\dot{x} = -x + \bar{u}x^2 = x(\bar{u}x - 1)
$$
这个系统除了在 $x=0$ 处有一个[平衡点](@entry_id:272705)外，还在 $x = 1/\bar{u}$ 处有另一个[平衡点](@entry_id:272705)。通过[相线](@entry_id:269561)分析可知，$x=0$ 是局部稳定的，而 $x=1/\bar{u}$ 是不稳定的。任何初始状态 $x_0 > 1/\bar{u}$ 都会导致 $\dot{x} > 0$，状态将持续增大。通过求解该[微分方程](@entry_id:264184)，可以发现对于任何 $x_0 > 1/\bar{u}$，解将在有限时间 $T(x_0, \bar{u}) = \ln\left(\frac{x_0\bar{u}}{x_0\bar{u} - 1}\right)$ 内趋于无穷，即发生**有限时间逃逸**。

这个例子生动地说明了，即使一个系统在没有输入时是全局[渐近稳定](@entry_id:168077)的，一个任意小的、持续存在的输入也可能导致系统的全局稳定性被完全破坏，甚至使某些状态轨迹在有限时间内发散。GAS概念本身无法预见或刻画这种脆弱性。而ISS框架正是为了解决这个问题而设计的。一个ISS系统，根据其定义，必须对任意有界输入保持状态有界。因此，上述系统不可能是ISS的。这一结论可以通过后续将要介绍的ISS-Lyapunov理论得到严格的证明。

### ISS的Lyapunov理论

正如[Lyapunov直接法](@entry_id:267103)是分析经典稳定性的基石一样，ISS理论也建立在坚实的Lyapunov基础之上。它使得我们无需直接求解微分方程，即可判断系统是否ISS。

#### ISS-Lyapunov函数

这一理论的核心是**ISS-[Lyapunov函数](@entry_id:273986)**的概念。一个连续可微的、正定且径向无界的函数 $V(x)$ 被称为系统 $\dot{x}=f(x,u)$ 的一个ISS-Lyapunov函数，如果存在 $\mathcal{K}_{\infty}$ 类函数 $\underline{\alpha}, \overline{\alpha}, \alpha$ 和一个 $\mathcal{K}$ 类函数 $\sigma$，使得以下两个条件成立：

1.  **[范数等价](@entry_id:137561)性**:
    $$
    \underline{\alpha}(|x|) \le V(x) \le \overline{\alpha}(|x|)
    $$

2.  **[耗散不等式](@entry_id:188634)**:
    $$
    \frac{\partial V}{\partial x} f(x,u) \le -\alpha(|x|) + \sigma(|u|)
    $$

第一个条件确保了[Lyapunov函数](@entry_id:273986) $V(x)$ 的“大小”与状态范数 $|x|$ 的“大小”是相当的。第二个条件，即[耗散不等式](@entry_id:188634)，是ISS-Lyapunov理论的精髓。它表明，[Lyapunov函数](@entry_id:273986) $V$ 沿系统轨线的变化率 $\dot{V}$ 受到两个部分的制约：

*   一个**耗散项** $-\alpha(|x|)$，它使系统趋于稳定。当状态范数 $|x|$ 较大时，该项是一个较大的负数，强力地“拉低”$V$ 的值。
*   一个**激励项** $\sigma(|u|)$，它由外部输入引起，可能“推高”$V$ 的值。

ISS-Lyapunov条件直观地表达了一个“拉锯战”：只要状态 $|x|$ 足够大，使得耗散项 $-\alpha(|x|)$ 能够压制住由输入 $|u|$ 产生的激励项 $\sigma(|u|)$，那么 $V$ 的值就会下降，从而状态 $x$ 会被[拉回](@entry_id:160816)到一个更小的区域。具体来说，当 $\alpha(|x|) > \sigma(|u|)$ 时，$\dot{V}$ 必为负。这等价于，只要 $|x| > \alpha^{-1}(\sigma(|u|))$，状态范数就会减小。这正是ISS性质的体现：状态最终会进入一个由输入幅值决定的邻域内。[@problem_id:2712878]

回到之前的例子 $\dot{x} = -x + x^2 u$。我们再次考察候选[Lyapunov函数](@entry_id:273986) $V(x) = \frac{1}{2}x^2$。其沿轨线的导数为：
$$
\dot{V} = x \cdot (-x + x^2 u) = -x^2 + x^3 u
$$
为了满足ISS-Lyapunov[耗散不等式](@entry_id:188634)，我们需要找到函数 $\alpha$ 和 $\sigma$ 使得 $-x^2 + x^3 u \le -\alpha(|x|) + \sigma(|u|)$。然而，对于任何固定的正输入 $u = \bar{u} > 0$，当 $x$ 变得很大时，$x^3 \bar{u}$ 这一项是正的，并且比 $-x^2$ 的阶数更高。这意味着当 $x > 1/\bar{u}$ 时，$\dot{V} = x^2(\bar{u}x - 1) > 0$。Lyapunov函数的值会增加，而不是减少。因此，我们无法找到所需的耗散项 $-\alpha(|x|)$ 来“镇压”输入效应。该系统不存在ISS-[Lyapunov函数](@entry_id:273986)，这从Lyapunov理论的层面解释了它为何不是ISS的。[@problem_id:2722269]

#### [Lyapunov函数的构造](@entry_id:177727)与ISS界定的推导

**正向[Lyapunov定理](@entry_id:191619)**指出，如果一个系统存在ISS-[Lyapunov函数](@entry_id:273986)，那么该系统就是ISS的。从ISS-Lyapunov不等式推导出最终的ISS界定 $|x(t)| \le \beta(|x_0|, t) + \gamma(\|u\|_{L_{\infty}(0,t)})$ 的过程，清晰地揭示了各比较函数的作用。[@problem_id:2712878]

1.  从 $\dot{V} \le -\alpha(|x|) + \sigma(|u|)$ 出发，利用[范数等价](@entry_id:137561)性 $V \le \overline{\alpha}(|x|)$ (即 $|x| \ge \overline{\alpha}^{-1}(V)$)，可得到一个关于 $V$ 本身的[微分不等式](@entry_id:137452)：$\dot{V} \le -\alpha(\overline{\alpha}^{-1}(V)) + \sigma(\|u\|_{L_{\infty}})$.
2.  通过求解或使用比较引理分析这个标量[微分不等式](@entry_id:137452)，可以得到一个关于 $V(t)$ 的界定，其形式为 $V(x(t)) \le \beta_V(V(x_0), t) + \gamma_V(\|u\|_{L_{\infty}})$. 这里的 $\beta_V$ 和 $\gamma_V$ 的具体形式依赖于 $\alpha, \overline{\alpha}$ 和 $\sigma$。
3.  最后，再次使用[范数等价](@entry_id:137561)性，即 $\underline{\alpha}(|x|) \le V(x)$ 和 $V(x_0) \le \overline{\alpha}(|x_0|)$，将关于 $V$ 的界定转化回关于 $|x|$ 的界定，最终得到ISS的标准形式。

这个过程阐明了：$\underline{\alpha}$ 和 $\overline{\alpha}$ 负责在状态范数和Lyapunov函数值之间建立桥梁；$\alpha$ 决定了系统的内在耗散率，从而影响瞬态衰减函数 $\beta$；而 $\sigma$ 则决定了输入的影响程度，从而影响渐近增益函数 $\gamma$。

让我们通过一个具体的例子来固化这一过程。假设一个系统存在一个[Lyapunov函数](@entry_id:273986) $V(x)$ 满足如下二次型不等式：[@problem_id:2722262]
*   $c_1|x|^2 \le V(x) \le c_2|x|^2$
*   $\dot{V} \le -2\lambda V + \mu |d|^2$

其中 $c_1, c_2, \lambda, \mu$ 均为正常数，输入为 $d(t)$。设 $r = \|d\|_{\infty}$。我们有[微分不等式](@entry_id:137452) $\dot{V} + 2\lambda V \le \mu r^2$。两边乘以[积分因子](@entry_id:177812) $e^{2\lambda t}$ 得 $\frac{d}{dt}(V e^{2\lambda t}) \le \mu r^2 e^{2\lambda t}$。从 $0$ 到 $t$ 积分，我们得到：
$$
V(t)e^{2\lambda t} - V(0) \le \frac{\mu r^2}{2\lambda}(e^{2\lambda t} - 1)
$$
整理后得到关于 $V(t)$ 的界：
$$
V(t) \le V(0) e^{-2\lambda t} + \frac{\mu r^2}{2\lambda}(1 - e^{-2\lambda t}) \le V(0) e^{-2\lambda t} + \frac{\mu r^2}{2\lambda}
$$
现在，利用[范数等价](@entry_id:137561)性 $c_1|x(t)|^2 \le V(t)$ 和 $V(0) \le c_2|x_0|^2$：
$$
c_1|x(t)|^2 \le c_2|x_0|^2 e^{-2\lambda t} + \frac{\mu r^2}{2\lambda}
$$
两边同除以 $c_1$ 并开方，利用 $\sqrt{A+B} \le \sqrt{A} + \sqrt{B}$，我们得到：
$$
|x(t)| \le \sqrt{\frac{c_2}{c_1}}|x_0|e^{-\lambda t} + \sqrt{\frac{\mu}{2\lambda c_1}}r
$$
这正是ISS界定的形式，其中 $\beta(s,t) = \sqrt{c_2/c_1} s e^{-\lambda t}$ 是一个($\mathcal{KL}$类)指数衰减函数，而渐近增益函数为 $\gamma(r) = \sqrt{\frac{\mu}{2\lambda c_1}}r$。

#### 非光滑系统与Converse定理

Lyapunov理论的适用范围可以扩展到Lyapunov函数 $V$ 仅仅是局部Lipschitz而非连续可微的情形。此时，导数 $\dot{V}$ 被**Dini导数**所替代。例如，上右Dini导数的定义为：[@problem_id:2712850]
$$
D^+V(x; f(x,u)) \triangleq \limsup_{h\to 0^+} \frac{V(x+h f(x,u)) - V(x)}{h}
$$
有了这个推广，ISS-Lyapunov的[耗散不等式](@entry_id:188634)可以写为 $D^+V(x; f(x,u)) \le -\alpha(|x|) + \sigma(|u|)$，这使得该理论能够应用于更广泛的系统，包括那些由[非光滑优化](@entry_id:167581)或切换逻辑产生的系统。

Lyapunov理论的完备性由**Converse [Lyapunov定理](@entry_id:191619)**所保证。该定理指出，对于任何满足温和[正则性条件](@entry_id:166962)的ISS系统，必然存在一个（光滑或非光滑的）ISS-[Lyapunov函数](@entry_id:273986)。[@problem_id:2712917] 这一深刻结果意味着ISS性质与ISS-[Lyapunov函数](@entry_id:273986)的存在性是等价的。它不仅具有理论上的重要性，也启发了通过求解Hamilton-Jacobi不等式来构造控制器和观测器的数值方法。其[构造性证明](@entry_id:157587)通常定义 $V(x)$ 为从状态 $x$ 出发，在所有可能的输入下，沿轨迹累积的某种“代价”的最坏情况（[上确界](@entry_id:140512)），例如：
$$
V(x) = \sup_{u(\cdot)} \int_0^\infty e^{-\lambda \tau} \alpha_c(|\phi(\tau, x, u)|) d\tau
$$
其中 $\phi(\tau, x, u)$ 是系统的解，$\alpha_c$ 是一个选定的[代价函数](@entry_id:138681)。证明的关键在于利用已知的ISS界定来保证该[积分收敛](@entry_id:139742)且 $V$ 具有所需的性质。

### ISS概念的扩展

ISS框架的灵活性和深刻内涵催生了一系列重要的理论扩展，使其能够应对更复杂的系统和稳定性问题。

#### 一致输入到状态稳定性 (Uniform Input-to-State Stability - UISS)

当系统模型本身随时间变化时，即 $\dot{x} = f(t, x, u)$，稳定性是否依赖于系统启动的时刻 $t_0$ 就成了一个关键问题。**一致ISS (UISS)** 要求稳定性行为不依赖于初始时刻。形式上，系统被称为UISS，如果存在**单个**不依赖于初始时刻 $t_0$ 的 $\mathcal{KL}$ 类函数 $\beta$ 和 $\mathcal{K}$ 类函数 $\gamma$，使得对任意初始时刻 $t_0 \ge 0$，任意初始状态 $x_0$ 和任意输入 $u$，解满足：[@problem_id:2712861]
$$
|x(t)| \le \beta(|x_0|, t-t_0) + \gamma\left(\sup_{s \ge t_0}|u(s)|\right)
$$
这里的关键在于，函数 $\beta$ 的第二个变量是**流逝时间** $t-t_0$，而非[绝对时间](@entry_id:265046) $t$。这保证了无论系统何时启动，其[初始条件](@entry_id:152863)的衰减速率都是相同的，体现了“一致性”。如果 $\beta$ 函数依赖于 $t_0$（记为 $\beta_{t_0}$），则稳定性是“非一致的”。

#### 积分输入到状态稳定性 (Integral Input-to-State Stability - iISS)

iISS是一个比ISS更弱的稳定性概念，它关注的是[状态和](@entry_id:193625)输入的**积分**行为。一个系统被称为iISS，如果存在 $\mathcal{K}_\infty$ [类函数](@entry_id:146970) $\alpha, \sigma, \mu, \rho$，使得对所有 $t \ge 0$ 成立：[@problem_id:2712901]
$$
\int_0^t \alpha(|x(\tau)|) d\tau \le \sigma(|x_0|) + \mu\left(\int_0^t \rho(|u(\tau)|) d\tau\right)
$$
这个不等式表明，状态的累积“能量”（左侧积分）被初始状态的效应以及输入累积“能量”（右侧积分）所约束。

ISS与iISS的关键区别在于对输入范数的依赖：ISS依赖于输入的 $L_\infty$ 范数（幅值），而iISS依赖于输入的 $L_1$ 型范数（积分）。这导致了根本性的行为差异：**ISS是比iISS更强的性质**。任何ISS系统都是iISS的，但反之不然。一个重要后果是，iISS不保证有界输入产生有界状态（BIBS性质）。例如，一个恒定的非零输入 $u(t) \equiv c$ 是有界的，但其积分 $\int_0^t \rho(c)d\tau = \rho(c) \cdot t$ 会随时间线性增长。iISS不等式允许状态的积分也随之增长，这可能对应于状态本身无界增长（尽管增长速度可能很慢）。而ISS系统则必须在这种情况下保持状态有界。

#### 输入到输出稳定性 (Input-to-Output Stability - IOS)

在许多应用中，我们关心的不是整个系统状态的稳定性，而是某个特定**输出** $y = h(x)$ 的稳定性。**输入到输出稳定性 (IOS)** 正是为此而生。一个带输出的系统被称为IOS，如果存在 $\beta \in \mathcal{KL}$ 和 $\gamma \in \mathcal{K}$，使得输出 $y(t)$ 满足：[@problem_id:2714043]
$$
|y(t)| \le \beta(|x_0|, t) + \gamma(\|u\|_\infty)
$$
这个定义与ISS的定义在结构上完全相同，只是将考察对象从状态 $x$ 换成了输出 $y$。IOS允许系统内部存在不稳定动态（即系统不是ISS的），只要这些不稳定的“模式”在输出端是不可见的。

一个典型的例子是系统：
$$
\begin{aligned}
\dot{x}_1 = -x_1 + u \\
\dot{x}_2 = x_2
\end{aligned}
$$
其状态 $x_2(t) = x_2(0)e^t$ 是不稳定的，因此整个系统不是ISS。然而，如果我们只关心输出 $y = x_1$，那么由于 $x_1$ 子系统本身是ISS的，其解满足 $|x_1(t)| \le |x_1(0)|e^{-t} + \|u\|_\infty (1-e^{-t})$。这个界符合IOS的定义。因此，该系统对于输出 $y=x_1$ 是IOS的，但对于全状态 $x=(x_1, x_2)$ 不是ISS的。这个概念在研究系统的[零动态](@entry_id:177017)、[观测器设计](@entry_id:263404)以及模块化控制中扮演着至关重要的角色。