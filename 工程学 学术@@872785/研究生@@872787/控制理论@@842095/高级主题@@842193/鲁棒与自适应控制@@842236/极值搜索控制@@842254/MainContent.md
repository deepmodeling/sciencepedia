## 引言
在现代工程与科学领域，[实时优化](@entry_id:169327)是一个无处不在的挑战：如何在线调整系统参数，以使其性能指标达到最优？当系统的精确数学模型未知或随时间变化时，传统[基于模型的优化](@entry_id:635801)方法便捉襟见肘。极值搜寻控制（Extremum Seeking Control, ESC）正是为解决这一难题而生的一种强大、优雅的无模型[自适应控制](@entry_id:262887)策略。它能够在不依赖先验知识的情况下，通过巧妙的“试探”与反馈，自主地“爬山”或“下谷”，将系统驱动至最优[工作点](@entry_id:173374)。

本文旨在系统性地剖析极值搜寻控制。我们将从其根本机制出发，逐步深入到其高级应用与理论前沿。
*   在 **“原理与机制”** 章节中，您将学习到ESC如何通过引入高频[抖动信号](@entry_id:177752)并结合[同步解调](@entry_id:270620)技术，来估计未知函数的梯度，并理解其稳定性、收敛性以及多变量扩展的核心思想。
*   接下来，在 **“应用与交叉学科联系”** 章节中，我们将展示ESC在太阳能跟踪、[非线性振子](@entry_id:266739)控制等工程问题中的实际应用，探讨其与牛顿法、安[全控制](@entry_id:275827)等高级[范式](@entry_id:161181)的集成，并探索其与[演化生物学](@entry_id:145480)等领域的深刻联系。
*   最后，通过 **“动手实践”** 环节，您将有机会通过解决具体问题，将理论知识转化为实际的分析与设计能力。

通过本次学习，您将全面掌握极值搜寻控制这一强大的[在线优化](@entry_id:636729)工具，为解决复杂的未知[系统优化](@entry_id:262181)问题奠定坚实的理论与实践基础。

## 原理与机制

在“引言”章节中，我们介绍了[极值](@entry_id:145933)搜寻控制（Extremum Seeking Control, ESC）作为一种无模型[实时优化](@entry_id:169327)方法的概念。本章将深入探讨其核心工作原理与基本机制，从其[梯度估计](@entry_id:164549)算法的基础出发，逐步揭示其稳定性、收敛性以及在更复杂场景下的扩展。

### [梯度估计](@entry_id:164549)的基本机制：[抖动](@entry_id:200248)与解调

[极值](@entry_id:145933)搜寻控制最精妙之处在于，它能够在不依赖被控对象数学模型的情况下，估计出未知[非线性映射](@entry_id:272931) $J(u)$ 的梯度信息。这一机制是整个方法的核心，其原理可以通过对一个典型的单输入单输出（SISO）系统进行分析来阐明。

考虑一个待优化的未知静态[非线性映射](@entry_id:272931) $y(t) = J(u(t))$，其中 $u$ 是输入，$y$ 是输出。我们的目标是调整一个参数 $\theta(t)$，使其收敛到 $J(u)$ 的一个[极值](@entry_id:145933)点 $u^\star$。为实现这一目标，ESC采用了一种“探测-估计”策略。控制器并不直接将估计值 $\theta(t)$ 作为系统输入，而是在其上叠加一个小的、高频的周期性扰动信号，即**[抖动信号](@entry_id:177752)**（dither signal）。一个典型的选择是[正弦信号](@entry_id:196767)，此时系统输入为：
$u(t) = \theta(t) + a\sin(\omega t)$
其中，$a > 0$ 是[抖动](@entry_id:200248)幅值，$\omega > 0$ 是[抖动](@entry_id:200248)频率。这里我们做出一个关键的**时间尺度分离**（time-scale separation）假设：[抖动](@entry_id:200248)频率 $\omega$ 远大于系统其他动态（即 $\theta(t)$ 的变化速率）的特征频率。

这个经过扰动的输入 $u(t)$ 被施加到[非线性映射](@entry_id:272931) $J$ 上，产生输出 $y(t) = J(\theta(t) + a\sin(\omega t))$。由于 $a$ 通常被取得很小，我们可以利用[泰勒级数](@entry_id:147154)在慢变的 $\theta(t)$ 附近展开 $J(u(t))$：
$y(t) = J(\theta(t) + a\sin(\omega t)) \approx J(\theta(t)) + J'(\theta(t)) \cdot a\sin(\omega t) + \frac{1}{2}J''(\theta(t)) \cdot (a\sin(\omega t))^2 + \dots$

输出信号 $y(t)$ 中现在包含了关于 $J$ 在 $\theta(t)$ 点的各阶导数的信息，这些信息被调制在[抖动](@entry_id:200248)频率 $\omega$ 的各[次谐波](@entry_id:171489)上。为了提取我们最感兴趣的梯度信息 $J'(\theta(t))$，ESC采用了**[同步解调](@entry_id:270620)**（synchronous demodulation）技术。具体来说，我们将输出信号 $y(t)$ 与一个和[抖动信号](@entry_id:177752)同步的参考信号（例如，[抖动信号](@entry_id:177752)自身）相乘，得到解调信号 $s(t)$：
$s(t) = y(t)\sin(\omega t) \approx J(\theta(t))\sin(\omega t) + a J'(\theta(t))\sin^2(\omega t) + \dots$

接下来，我们对[解调](@entry_id:260584)信号 $s(t)$ 进行**低通滤波**（Low-Pass Filtering, LPF）。在[时间尺度分离](@entry_id:149780)的假设下，低通滤波器可以被设计为滤除所有频率不为零的交流（AC）分量，仅保留直流（DC）分量。这在数学上等价于对信号在一个[抖动](@entry_id:200248)周期 $T=2\pi/\omega$ 内进行时间平均。我们利用基本的三角函数积分性质：$\langle\sin(\omega t)\rangle = 0$ 以及 $\langle\sin^2(\omega t)\rangle = \frac{1}{2}$。对 $s(t)$ 的各项取平均，我们得到滤波器的输出 $\eta(t)$：
$\eta(t) \approx \langle s(t) \rangle = J(\theta(t))\langle\sin(\omega t)\rangle + a J'(\theta(t))\langle\sin^2(\omega t)\rangle + \dots = \frac{a}{2}J'(\theta(t))$

这个结果是惊人的：通过“[抖动](@entry_id:200248)-[解调](@entry_id:260584)-滤波”这一系列操作，我们得到了一个与未知函数 $J(u)$ 在当前操作点 $\theta(t)$ 的梯度 $J'(\theta(t))$ 成正比的信号。这个信号就是ESC赖以工作的[梯度估计](@entry_id:164549)。

最后一步是构建**[自适应律](@entry_id:276528)**（adaptation law）来更新参数 $\theta(t)$。如果我们希望最小化 $J(u)$，我们应该让 $\theta(t)$ 沿着负梯度方向移动，即执行**[梯度下降](@entry_id:145942)**。因此，[自适应律](@entry_id:276528)可以设计为：
$\dot{\theta}(t) = -k \eta(t) = -k \frac{a}{2}J'(\theta(t))$
其中 $k > 0$ 是自适应增益。这条公式描述了ESC系统的**平均化系统**（averaged system）的动态，它表明，在平均意义下，参数 $\theta(t)$ 的演化等价于对[目标函数](@entry_id:267263) $J$ 执行的连续时间梯度下降算法 [@problem_id:2706356] [@problem_id:2706330]。

这个平均化系统的稳定性直接与 $J(u)$ 的局部曲率相关。在一个[平衡点](@entry_id:272705) $\theta^\star$ 附近（$J'(\theta^\star)=0$），我们可以对平均化系统进行线性化，得到误差动态 $\dot{\tilde{\theta}} \approx -(\frac{ka}{2}J''(\theta^\star))\tilde{\theta}$，其中 $\tilde{\theta} = \theta - \theta^\star$。对于最小化问题，我们寻求的[极值](@entry_id:145933)点满足 $J''(\theta^\star) > 0$。由于 $k, a$ 均为正，线性化系统的系数 $-(\frac{ka}{2}J''(\theta^\star))$ 为负，这意味着[平衡点](@entry_id:272705)是局部指数稳定的。反之，如果目标是最大化 $J(u)$，我们需要实现**梯度上升**，此时[自适应律](@entry_id:276528)应为 $\dot{\theta}(t) = +k \eta(t)$。这种情况下，系统会稳定在满足 $J''(\theta^\star)  0$ 的局部[最大值点](@entry_id:634610) [@problem_id:2706288]。

### 平均化系统的深入分析：偏差与收敛

上一节的推导揭示了ESC的核心思想，但它依赖于一阶近似。为了更精确地理解ESC的行为，我们需要考察高阶项的影响。这涉及到收敛的**偏差**（bias）和**收敛速率**（convergence rate）两个关键性能指标。

#### [稳态](@entry_id:182458)偏差

让我们将[泰勒展开](@entry_id:145057)式推进到更高阶。如果我们考虑 $J$ 的三阶导数，解调信号的平均值将包含更高阶的项。具体而言，平均化后的[梯度估计](@entry_id:164549)信号为 [@problem_id:2706323]：
$\eta(\theta) = \frac{a}{2}J'(\theta) + \frac{a^3}{16}J'''(\theta) + \mathcal{O}(a^5)$

注意，由于 $\langle\sin^n(\omega t)\rangle=0$ 对所有奇数 $n$ 成立，所以平均化信号中只含有 $a$ 的奇次幂项。

现在，考虑最小化问题的平均化系统 $\dot{\bar{\theta}} = -k \eta(\bar{\theta})$。其[平衡点](@entry_id:272705) $\bar{\theta}_{\mathrm{eq}}$ 由 $\eta(\bar{\theta}_{\mathrm{eq}}) = 0$ 决定，即：
$\frac{a}{2}J'(\bar{\theta}_{\mathrm{eq}}) + \frac{a^3}{16}J'''(\bar{\theta}_{\mathrm{eq}}) + \mathcal{O}(a^5) = 0$

除非 $J'''(\bar{\theta}_{\mathrm{eq}})=0$（这在一般情况下不成立），否则 $J'(\bar{\theta}_{\mathrm{eq}})$ 并不等于零。这意味着ESC的[平衡点](@entry_id:272705)通常会偏离真正的极值点 $u^\star$（其中 $J'(u^\star)=0$）。这个偏离就是[稳态](@entry_id:182458)偏差。我们可以估计这个偏差的大小。设偏差为 $\delta\theta = \bar{\theta}_{\mathrm{eq}} - u^\star$，并假设其很小。在 $u^\star$ 附近，我们有 $J'(\bar{\theta}_{\mathrm{eq}}) \approx J''(u^\star)\delta\theta$ 且 $J'''(\bar{\theta}_{\mathrm{eq}}) \approx J'''(u^\star)$。代入[平衡点](@entry_id:272705)条件，我们得到：
$J''(u^\star)\delta\theta \approx -\frac{a^2}{8}J'''(u^\star)$
$\delta\theta \approx -\frac{a^2}{8} \frac{J'''(u^\star)}{J''(u^\star)}$

这个重要的结果表明，[稳态](@entry_id:182458)偏差的大小与[抖动](@entry_id:200248)幅值 $a$ 的平方成正比，即 $\delta\theta = \mathcal{O}(a^2)$ [@problem_id:2706314]。这是一个[基本权](@entry_id:200855)衡：较大的[抖动](@entry_id:200248)幅值 $a$ 能产生更强的梯度信号（信噪比更高），从而可能加快收敛，但代价是更大的[稳态](@entry_id:182458)偏差。

#### 收敛速率

系统的收敛速率由平均化系统在[平衡点](@entry_id:272705)附近的线性化矩阵的[特征值](@entry_id:154894)决定。对于SISO系统，这个[特征值](@entry_id:154894)（即雅可比行列式）为：
$\frac{d}{d\bar{\theta}}\left(-\frac{ka}{2}J'(\bar{\theta})\right)\bigg|_{\bar{\theta} \approx u^\star} = -\frac{ka}{2}J''(u^\star)$

因此，局部[指数收敛](@entry_id:142080)速率近似为 $\frac{ka}{2}J''(u^\star)$。这个速率与增益 $k$、[抖动](@entry_id:200248)幅值 $a$ 以及目标函数在[极值](@entry_id:145933)点处的曲率 $J''(u^\star)$ 成正比 [@problem_id:2706314]。这符合直觉：更大的增益、更强的探测信号和更“陡峭”的 extremum 都会导致更快的收敛。然而， $k$ 和 $a$ 的选择受到时间尺度分离假设的限制，不能无限增大。

### 实际回路中的考量：相位、滤波器与执行器动态

在理想化的分析之外，实际ESC回路的性能还受到其他动态组件的显著影响。

#### 解调相位的影响

在前面的分析中，我们假设解调信号与[抖动信号](@entry_id:177752)完全同步，即使用 $\sin(\omega t)$ 进行[解调](@entry_id:260584)。如果[解调](@entry_id:260584)信号存在一个[相位偏移](@entry_id:276073) $\varphi$，即 $r(t) = \sin(\omega t + \varphi)$，情况会如何？解调后的[信号平均](@entry_id:270779)值变为：
$\langle aJ'(\theta) \sin(\omega t)\sin(\omega t + \varphi) \rangle = aJ'(\theta) \langle \frac{1}{2}(\cos(-\varphi) - \cos(2\omega t + \varphi)) \rangle = \frac{a \cos\varphi}{2}J'(\theta)$

此时，平均化系统变为 $\dot{\bar{\theta}} = -k \frac{a \cos\varphi}{2}J'(\bar{\theta})$ [@problem_id:2706314]。可见，梯度项的系数现在是 $\cos\varphi$。当 $\varphi=0$ 时，我们得到最大系数。当 $\varphi$ 增加，系数减小。特别地，当 $\varphi = \pi/2$（正交解调），$\cos(\pi/2)=0$，一阶梯度信息完全消失，ESC将失效。因此，精确的相位同步对于ESC的效率至关重要。

#### 动态滤波器的作用

在实际应用中，我们还会遇到其他滤波器。例如，为了消除测量信号中可能存在的直流偏置，常在解调前加入一个**高通滤波器**（High-Pass Filter, HPF），也称为冲刷滤波器（washout filter）。假设HPF的[传递函数](@entry_id:273897)为 $H_{hp}(s)$。这个滤波器会作用于 $y(t)$ 中的[抖动](@entry_id:200248)分量 $aJ'(\theta)\sin(\omega t)$，使其幅值和相位发生改变。滤波后的信号将变为 $aJ'(\theta) |H_{hp}(j\omega)| \sin(\omega t + \angle H_{hp}(j\omega))$。这个新的幅值和相位会传递到最终的平均化动态中，从而改变ESC的有效增益 [@problem_id:2706302]。

#### 执行器动态

同样，如果控制器输出 $\theta(t)+a\sin(\omega t)$ 与实际施加到[非线性映射](@entry_id:272931)的输入 $u(t)$ 之间存在执行器动态 $A(s)$，那么[抖动信号](@entry_id:177752)在到达 $J$ 之前也会被衰减和相移。实际输入端的[抖动](@entry_id:200248)分量将是 $a|A(j\omega)|\sin(\omega t + \angle A(j\omega))$。这相当于在[解调](@entry_id:260584)环节引入了一个等效的、频率相关的[相位偏移](@entry_id:276073)。最终，平均化动态的系数将依赖于执行器在[抖动](@entry_id:200248)频率 $\omega$ 处的[频率响应](@entry_id:183149) $A(j\omega)$ [@problem_id:2706331]。这凸显了在选择[抖动](@entry_id:200248)频率 $\omega$ 时，必须考虑系统中所有相关动态元件的带宽。

### 多变量[极值](@entry_id:145933)搜寻：正交性的力量

将ESC从单变量扩展到多变量情况 $J: \mathbb{R}^m \to \mathbb{R}$，核心挑战在于如何同时并独立地估计梯度向量 $\nabla J(\theta)$ 的所有分量。关键思想在于利用**正交性**（orthogonality）来实现信道[解耦](@entry_id:637294)。

考虑一个二维系统 $\theta = [\theta_1, \theta_2]^\top$。我们在每个输入通道上叠加一个[抖动信号](@entry_id:177752)：
$\theta(t) = \hat{\theta}(t) + d(t) = \begin{pmatrix} \hat{\theta}_1(t) \\ \hat{\theta}_2(t) \end{pmatrix} + \begin{pmatrix} a_1 s_1(t) \\ a_2 s_2(t) \end{pmatrix}$
其中 $s_1(t)$ 和 $s_2(t)$ 是周期性的载波信号。

系统的输出经过一阶泰勒展开后近似为：
$y(t) \approx J(\hat{\theta}) + \frac{\partial J}{\partial \theta_1}(\hat{\theta}) a_1 s_1(t) + \frac{\partial J}{\partial \theta_2}(\hat{\theta}) a_2 s_2(t)$

为了估计第 $i$ 个梯度分量 $\frac{\partial J}{\partial \theta_i}$，我们将 $y(t)$ 与对应的载波 $s_i(t)$ 相乘并进行低通滤波（平均）：
$\eta_i(t) = \langle y(t)s_i(t) \rangle \approx \langle \frac{\partial J}{\partial \theta_1} a_1 s_1 s_i \rangle + \langle \frac{\partial J}{\partial \theta_2} a_2 s_2 s_i \rangle$

要实现解耦，即让 $\eta_i$ 只包含 $\frac{\partial J}{\partial \theta_i}$ 的信息，我们需要[载波](@entry_id:261646)信号满足[正交性条件](@entry_id:168905)：$\langle s_i(t) s_j(t) \rangle = 0$ 对所有 $i \neq j$ 成立。如果同时将载波进行归一化，使得 $\langle s_i^2(t) \rangle = 1$，那么我们就能得到：
$\eta_i(t) \approx a_i \frac{\partial J}{\partial \theta_i}(\hat{\theta})$

有两种常用的方法来构造这样的正交[载波](@entry_id:261646)集合：
1.  **频率分离**：为每个通道选择互不通约（incommensurate）的频率，例如 $s_i(t) = \sqrt{2}\sin(\omega_i t)$，其中 $\omega_i/\omega_j$ 不是有理数。在这种情况下，长期平均 $\langle s_i(t) s_j(t) \rangle = 0$ 对 $i \neq j$ 成立。这种方法可以自然地扩展到任意多维。[@problem_id:2706303] [@problem_id:2706330]
2.  **相位分离**：使用同一频率 $\omega$ 的正交相位的信号，例如对于二维系统，选择 $s_1(t) = \sqrt{2}\sin(\omega t)$ 和 $s_2(t) = \sqrt{2}\cos(\omega t)$。由于 $\langle \sin(\omega t)\cos(\omega t) \rangle = \langle \frac{1}{2}\sin(2\omega t) \rangle = 0$，正交性得以保证。

采用正交载波后，多变量ESC的平均化系统可以写成解耦的[梯度流](@entry_id:635964)形式：
$\dot{\hat{\theta}}_{i,avg}(t) = -k_i \eta_i(t) \approx -k_i a_i \frac{\partial J}{\partial \theta_i}(\hat{\theta})$
或者用矩阵形式表示为 $\dot{\hat{\theta}}_{avg}(t) \approx -K \nabla J(\hat{\theta})$，其中 $K$ 是一个[对角矩阵](@entry_id:637782) $K = \mathrm{diag}(k_1 a_1, k_2 a_2, \dots)$。这表明，多变量ESC在平均意义下等价于一个[对角缩放](@entry_id:748382)的梯度下降（或上升）算法。

### 形式化分析与理论关联

ESC不仅仅是一种[启发式算法](@entry_id:176797)，它的行为可以通过严格的数学理论进行分析和证明，并与其他优化和控制理论分支紧密相连。

#### [李雅普诺夫稳定性](@entry_id:147734)分析

对于特定类型的[目标函数](@entry_id:267263)，我们可以使用李雅普诺夫（Lyapunov）方法来形式化地证明ESC的稳定性。例如，考虑一个严格凸的二次型[目标函数](@entry_id:267263) $J(u) = q(u - \theta^\star)^2 + J_0$ ($q0$)。对于这个问题，平均化动态是精确的[线性系统](@entry_id:147850)，因为所有高阶导数都为零。经过推导，误差 $\tilde{\theta} = \theta - \theta^\star$ 的平均化动态为 [@problem_id:2706363]：
$\dot{\tilde{\theta}}_{avg} = -2kaq \tilde{\theta}_{avg}$

我们可以选择一个[李雅普诺夫函数](@entry_id:273986)候选 $V(\tilde{\theta}) = \frac{1}{2}\tilde{\theta}^2$。它的导数沿着平均系统的轨迹为：
$\dot{V} = \tilde{\theta}\dot{\tilde{\theta}} = \tilde{\theta}(-2kaq\tilde{\theta}) = -2kaq\tilde{\theta}^2 = -4kaqV$

由于 $k,a,q$ 均为正，$\dot{V}$ 是负定的，这证明了系统是全局指数稳定的。此外，这个关系还允许我们进行[控制器设计](@entry_id:274982)。如果我们希望收敛速率至少为 $\sigma$，即要求 $\dot{V} \le -2\sigma V$，那么我们只需满足 $-4kaqV \le -2\sigma V$，这给出增益的下界 $k \ge \frac{\sigma}{2aq}$。对于多变量二次型函数 $J(\theta) = \frac{1}{2}\theta^\top Q \theta$（$Q$ 正定），类似的分析表明，使用正交[抖动](@entry_id:200248)的ESC平均化系统是一个[线性系统](@entry_id:147850) $\dot{\hat{\theta}}_{avg} = -D Q \hat{\theta}$（$D$ 为正定对角阵），可以通过二次型李雅普诺夫函数证明其全局[指数稳定性](@entry_id:169260) [@problem_id:2706303]。

#### 非凸目标与[吸引域](@entry_id:172179)

ESC本质上是一种**局部**[优化方法](@entry_id:164468)。它的行为类似于梯度下降/上升，因此当[目标函数](@entry_id:267263) $J(u)$ 非凸时，系统可能会收敛到任何一个[局部极值](@entry_id:144991)点。最终收敛到哪个极值点，取决于参数的初始值 $\theta(0)$。

以非[凸函数](@entry_id:143075) $J(u) = -(u^2-1)^2$ 为例，该函数在 $u=\pm 1$ 处有两个[全局最大值](@entry_id:174153)，在 $u=0$ 处有一个局部最小值。一个寻求最大值的ESC系统（$\dot{\hat{u}} = k \eta(t)$）的平均化动态为 $\dot{\hat{u}}_{avg} = \frac{ka}{2}J'(\hat{u}_{avg})$。该系统的[平衡点](@entry_id:272705)为 $J'(u)=0$ 的解，即 $u \in \{-1, 0, 1\}$。稳定性分析表明，对应于[最大值点](@entry_id:634610)的 $u=\pm 1$ 是稳定的[平衡点](@entry_id:272705)，而对应于[最小值点](@entry_id:634980)的 $u=0$ 是不稳定的[平衡点](@entry_id:272705)。这个不稳定的[平衡点](@entry_id:272705)成了一个**分离轨迹**（separatrix），它将状态空间划分为不同的**[吸引域](@entry_id:172179)**（basins of attraction）。如果初始值 $\hat{u}(0)  0$，系统将收敛到 $u=1$；如果 $\hat{u}(0)  0$，系统将收敛到 $u=-1$ [@problem_id:2706288]。这清楚地说明了ESC的局部性。

#### 与[随机近似](@entry_id:270652)的联系

当测量信号中存在加性零均值噪声 $y(t) = J(u(t)) + \nu(t)$ 时，ESC的[梯度估计](@entry_id:164549)项会受到一个附加的噪声项干扰。在这种情况下，ESC的[自适应律](@entry_id:276528)在本质上变成了一个**[随机近似](@entry_id:270652)**（stochastic approximation）算法，类似于机器学习中常用的[随机梯度下降](@entry_id:139134)（SGD）。

经典的Robbins-Monro[随机近似](@entry_id:270652)理论指出，要保证算法[几乎必然收敛](@entry_id:265812)到目标点（而不仅仅是在其附近波动），步长（在ESC中对应于增益 $k$）必须随时间递减。具体来说，如果将连续时间ESC离散化，步长序列 $\{\alpha_n\}$ 需要满足条件 $\sum \alpha_n = \infty$ 和 $\sum \alpha_n^2  \infty$。一个典型的选择是 $\alpha_n \propto 1/n$。如果使用固定的增益 $k$，在噪声存在的情况下，[参数估计](@entry_id:139349) $\theta(t)$ 不会收敛到一个点，而是会收敛到一个以[真值](@entry_id:636547)为中心的随机[分布](@entry_id:182848)，其[方差](@entry_id:200758)与增益 $k$ 和噪声强度有关 [@problem_id:2706330]。

#### 时间尺度分离与参数整定

 averaging theory的有效性依赖于严格的时间尺度分离。一个设计良好的ESC系统通常需要满足三个时间尺度的分离 [@problem_id:2706313]：
1.  **最快尺度**：[抖动](@entry_id:200248)频率 $\omega$。
2.  **中间尺度**：低通滤波器的带宽，例如由其极点 $\lambda$ 决定。
3.  **最慢尺度**：自适应增益 $k$ 决定的闭环动态。

即满足 $\omega \gg \lambda \gg k$。这个条件保证了低通滤波器能有效地滤除[抖动](@entry_id:200248)谐波，同时又能足够快地跟踪[梯度估计](@entry_id:164549)值的变化，而参数 $\theta(t)$ 的更新则要足够慢，以使其在 averaging 周期内可被视为常数。

更深入的[奇异摄动](@entry_id:170303)分析表明，为了在[抖动](@entry_id:200248)频率 $\omega \to \infty$ 的极限下保持恒定的收敛性能同时消除[稳态](@entry_id:182458)偏差，控制器参数需要根据 $\omega$ 进行特定比例的调整（scaling）。例如，一种有效的参数整定策略是 $a(\omega) \propto \omega^{-1/2}$， $k(\omega) \propto \omega^{1/2}$ 以及 $\lambda(\omega) \propto \omega^{3/4}$。这种整定确保了有效收敛速率 $\kappa \propto k(\omega)a(\omega)$ 保持不变，而偏差（与 $a^2$ 和 $(\lambda/\omega)^2$ 有关）和时间尺度分离条件都能在极限情况下得到满足 [@problem_id:2706313]。

本章通过层层剖析，揭示了极值搜寻控制从基本原理到理论深度的完整图景。它是一种巧妙地将控制理论与优化思想结合的工程方法，其 elegant 的[梯度估计](@entry_id:164549)算法使其在处理未知[系统优化](@entry_id:262181)问题时显得尤为强大。