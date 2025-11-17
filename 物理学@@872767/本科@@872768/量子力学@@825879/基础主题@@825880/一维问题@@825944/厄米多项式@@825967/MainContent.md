## 引言
埃尔米特多项式是量子力学数学工具箱中的一块关键基石，对于理解物理学中最基本、最重要的可解模型之一——量子谐振子——至关重要。尽管许多学生在学习中会遇到这些多项式，但往往只将其视为薛定谔方程的既定解，而未能深入探究其物理必然性、数学结构以及如何将这些抽象概念转化为可计算的物理预测。本文旨在填补这一知识鸿沟，系统地揭示埃尔米特多项式的来龙去脉及其在物理世界中的深刻印记。

在接下来的内容中，我们将分步展开探索之旅。首先，在“**原理与机制**”一章中，我们将从量子谐振子的薛定谔方程出发，揭示埃尔米特多项式是如何作为物理约束下的必然解而出现的。我们将系统学习其高效的生成方法，如罗德里格斯公式和生成函数，并深入剖析其递推关系、宇称性和正交性等关键数学性质。随后，在“**应用与交叉学科联系**”一章中，我们将展示如何运用这些原理来计算[波函数](@entry_id:147440)节点、[期望值](@entry_id:153208)和跃迁概率等可观测量，并将其应用扩展到[量子化学](@entry_id:140193)、[量子光学](@entry_id:140582)等交叉学科领域，展现其广泛的适用性。最后，通过“**动手实践**”部分提供的具体问题，您将有机会亲手应用所学知识，巩固并深化理解。让我们从这些多项式的起源开始，探寻它们是如何精确描绘微观粒子世界的。

## 原理与机制

本章将深入探讨埃尔米特多项式的核心原理与机制。作为[量子谐振子](@entry_id:140678)问题的数学基石，这些多项式不仅是抽象的数学对象，更是描述微观粒子行为的关键。我们将从它们在薛定谔方程中的起源开始，系统地介绍其生成方法、基本数学性质，并最终将其与可观测的物理现象联系起来。

### 埃尔米特多项式：量子谐振子解的必然选择

在上一章中，我们介绍了一维量子谐振子的定态薛定谔方程。通过引入无量纲坐标 $\xi = x \sqrt{m\omega/\hbar}$ 和无量纲能量 $\epsilon = 2E/(\hbar\omega)$，方程可以被简化为一种更普适的形式：
$$ \frac{d^2\psi}{d\xi^2} = (\xi^2 - \epsilon)\psi(\xi) $$

为了求解该方程，物理学家们考察了其在 $\xi \to \pm\infty$ 时的渐进行为。当 $\xi$ 极大时，$\xi^2$ 项远大于 $\epsilon$，方程近似为 $\frac{d^2\psi}{d\xi^2} \approx \xi^2\psi(\xi)$。这个方程的渐进解形式为 $\exp(-\xi^2/2)$，这保证了[波函数](@entry_id:147440)在无穷远处迅速衰减为零，满足物理上对束缚态[波函数](@entry_id:147440)可归一化的要求。

基于此，我们可以合理地假设方程的完整解具有以下形式：
$$ \psi(\xi) = H(\xi) \exp(-\frac{1}{2}\xi^2) $$
其中 $H(\xi)$ 是一个关于 $\xi$ 的待定函数。将此形式代入无量纲薛定谔方程，经过一番[微分](@entry_id:158718)和化简，我们可以得到一个完全描述 $H(\xi)$ 的[微分方程](@entry_id:264184)：
$$ \frac{d^2H}{d\xi^2} - 2\xi \frac{dH}{d\xi} + (\epsilon - 1)H(\xi) = 0 $$
这个方程被称为**[埃尔米特微分方程](@entry_id:153368) (Hermite's differential equation)**。为了使物理[波函数](@entry_id:147440) $\psi(\xi)$ 在整个空间内行为良好（即不发散），$H(\xi)$ 必须是一个有限阶的多项式，而非[无穷级数](@entry_id:143366)。这一要求导致了能量的量子化：只有当常数 $(\epsilon - 1)$ 取特定的离散值时，方程的解才是多项式。这些特定的值被证明是 $2n$，其中 $n$ 是一个非负整数 ($n=0, 1, 2, \dots$)。

因此，我们得到了[能量量子化](@entry_id:137825)的条件：
$$ \epsilon - 1 = 2n \quad \Rightarrow \quad \epsilon = 2n + 1 $$
将 $\epsilon$ 的定义代回，便可得到我们所熟知的量子谐振子能级公式 $E_n = (n + \frac{1}{2})\hbar\omega$。对于每一个量子数 $n$，都有一个对应的多项式解，我们称之为**埃尔米特多项式**，记作 $H_n(\xi)$。

让我们通过两个例子来具体感受这种对应关系。

首先，考虑系统的**[基态](@entry_id:150928)**，即 $n=0$ 的情况 [@problem_id:2096771]。此时，$\epsilon = 2(0)+1 = 1$，[埃尔米特方程](@entry_id:196615)变为：
$$ \frac{d^2H_0}{d\xi^2} - 2\xi \frac{dH_0}{d\xi} = 0 $$
这是一个可以求解的二阶微分方程。令 $G(\xi) = dH_0/d\xi$，方程变为 $dG/d\xi - 2\xi G = 0$，这是一个[一阶线性微分方程](@entry_id:164869)，其解为 $G(\xi) = C_1 \exp(\xi^2)$。再次积分得到 $H_0(\xi) = C_1 \int \exp(\xi^2) d\xi + C_2$。由于我们要求 $H_0(\xi)$ 是一个多项式，这迫使积分项的系数必须为零，即 $C_1=0$。因此，$H_0(\xi) = C_2$，即一个常数。按照物理学中的约定，我们通常选择 $H_0(\xi) = 1$。

现在，我们反过来验证一个更复杂的例子 [@problem_id:2096791]。假设我们提出了一个[波函数](@entry_id:147440)，其多项式部分为 $P(\xi) = 8\xi^3 - 12\xi$。这个多项式是否能描述一个有效的[量子谐振子](@entry_id:140678)定态？如果是，它对应于哪个能级？我们可以通过将其代入[埃尔米特方程](@entry_id:196615)来进行检验。该多项式 $P(\xi)$ 实际上就是 $H_3(\xi)$。我们需要验证它是否满足 $H_3'' - 2\xi H_3' + ( \epsilon - 1)H_3 = 0$。
首先计算其一阶和[二阶导数](@entry_id:144508)：
$P'(\xi) = 24\xi^2 - 12$
$P''(\xi) = 48\xi$
代入方程左边：
$$ (48\xi) - 2\xi(24\xi^2 - 12) + (\epsilon - 1)(8\xi^3 - 12\xi) $$
$$ = 48\xi - 48\xi^3 + 24\xi + (\epsilon - 1)(8\xi^3 - 12\xi) $$
$$ = -48\xi^3 + 72\xi + (\epsilon - 1)(8\xi^3 - 12\xi) $$
为了使上式对所有 $\xi$ 都恒等于零，不同次幂项的系数必须分别相加为零。
对于 $\xi^3$ 项：$-48 + 8(\epsilon - 1) = 0 \Rightarrow 8(\epsilon - 1) = 48 \Rightarrow \epsilon - 1 = 6 \Rightarrow \epsilon = 7$。
对于 $\xi$ 项：$72 - 12(\epsilon - 1) = 0 \Rightarrow 12(\epsilon - 1) = 72 \Rightarrow \epsilon - 1 = 6 \Rightarrow \epsilon = 7$。
两个条件给出了一致的结果 $\epsilon=7$。根据 $\epsilon = 2n+1$ 的关系，我们得到 $2n+1=7$，即 $n=3$。这证实了多项式 $8\xi^3 - 12\xi$ 确实是量子谐振子的第三[激发态](@entry_id:261453)（$n=3$）的解，并且它只在能量为 $\epsilon=7$ 时才成立。这个过程清晰地揭示了[波函数](@entry_id:147440)的特定形式与能量的特定值之间存在着一一对应的锁定关系。

### 埃尔米特多项式的系统生成方法

逐个求解微分方程来寻找 $H_n(\xi)$ 是非常繁琐的。幸运的是，数学家们已经发展出几种更高效、更系统的生成方法。

#### 罗德里格斯公式

**罗德里格斯公式 (Rodrigues' formula)** 提供了一个直接计算任意阶 $H_n(\xi)$ 的紧凑表达式：
$$ H_n(\xi) = (-1)^n \exp(\xi^2) \frac{d^n}{d\xi^n} \exp(-\xi^2) $$

这个公式虽然看起来复杂，但操作起来却非常直接。让我们用它来计算 $H_2(\xi)$ [@problem_id:2096800]。根据公式，当 $n=2$ 时：
$$ H_2(\xi) = (-1)^2 \exp(\xi^2) \frac{d^2}{d\xi^2} \exp(-\xi^2) $$
我们只需计算 $\exp(-\xi^2)$ 的[二阶导数](@entry_id:144508)。
一阶导数：$\frac{d}{d\xi}\exp(-\xi^2) = -2\xi \exp(-\xi^2)$。
[二阶导数](@entry_id:144508)：$\frac{d^2}{d\xi^2}\exp(-\xi^2) = \frac{d}{d\xi}(-2\xi \exp(-\xi^2)) = -2\exp(-\xi^2) + (-2\xi)(-2\xi \exp(-\xi^2)) = (4\xi^2 - 2)\exp(-\xi^2)$。
代回原式：
$$ H_2(\xi) = \exp(\xi^2) \left[ (4\xi^2 - 2)\exp(-\xi^2) \right] = 4\xi^2 - 2 $$
这正是 $n=2$ 的埃尔米特多项式。

#### 生成函数

另一种极其强大的工具是**[生成函数](@entry_id:146702) (generating function)**。它将所有阶的埃尔米特多项式编码在一个单一的函数 $G(\xi, t)$ 中：
$$ G(\xi, t) = \exp(2\xi t - t^2) = \sum_{n=0}^{\infty} H_n(\xi) \frac{t^n}{n!} $$
这里的 $t$ 是一个辅助变量，没有直接的物理意义。$H_n(\xi)$ 恰好是这个函数对 $t$ 进行泰勒展开时 $t^n/n!$ 项的系数。这意味着，我们可以通过对 $G(\xi, t)$ 在 $t=0$ 附近做[级数展开](@entry_id:142878)来一次性“提取”出各个阶的埃尔米特多项式。

让我们用这个方法来找出前三个埃尔米特多项式 $H_0, H_1, H_2$ [@problem_id:1371790]。我们将[生成函数](@entry_id:146702)写成两个[指数函数](@entry_id:161417)之积，并分别对它们进行泰勒展开：
$$ G(\xi, t) = \exp(2\xi t) \exp(-t^2) $$
$$ \exp(2\xi t) = 1 + (2\xi t) + \frac{(2\xi t)^2}{2!} + \dots = 1 + 2\xi t + 2\xi^2 t^2 + O(t^3) $$
$$ \exp(-t^2) = 1 + (-t^2) + \frac{(-t^2)^2}{2!} + \dots = 1 - t^2 + O(t^4) $$
将两者相乘，并收集 $t$ 的同次幂项（我们只需要到 $t^2$ 项）：
$$ G(\xi, t) = (1 + 2\xi t + 2\xi^2 t^2 + \dots)(1 - t^2 + \dots) $$
$$ = 1 \cdot 1 + (2\xi t) \cdot 1 + (2\xi^2 t^2) \cdot 1 + 1 \cdot (-t^2) + \dots $$
$$ = 1 + (2\xi)t + (2\xi^2 - 1)t^2 + O(t^3) $$
现在，我们将此结果与[生成函数](@entry_id:146702)的定义 $\sum H_n(\xi) \frac{t^n}{n!}$ 进行比较：
$t^0$ 项: $\frac{H_0(\xi)}{0!} = 1 \Rightarrow H_0(\xi) = 1$
$t^1$ 项: $\frac{H_1(\xi)}{1!} = 2\xi \Rightarrow H_1(\xi) = 2\xi$
$t^2$ 项: $\frac{H_2(\xi)}{2!} = 2\xi^2 - 1 \Rightarrow H_2(\xi) = 2(2\xi^2 - 1) = 4\xi^2 - 2$
这与我们之前得到的结果完全一致，展示了[生成函数](@entry_id:146702)的威力。

#### 递推关系

埃尔米特多项式之间还存在着紧密的联系，可以通过**[递推关系](@entry_id:189264) (recursion relations)** 来描述。其中最常用的是：
$$ H_{n+1}(\xi) = 2\xi H_n(\xi) - 2n H_{n-1}(\xi) $$
这个关系式表明，只要我们知道任意两个连续的埃尔米特多项式，就可以通过纯代数运算，无需再进行[微分](@entry_id:158718)或积分，就能得到更高阶的多项式。

例如，已知 $H_1(\xi) = 2\xi$ 和 $H_2(\xi) = 4\xi^2 - 2$，我们可以用[递推关系](@entry_id:189264)计算 $H_3(\xi)$ [@problem_id:2096790]。令 $n=2$：
$$ H_3(\xi) = 2\xi H_2(\xi) - 2(2) H_1(\xi) $$
$$ = 2\xi (4\xi^2 - 2) - 4 (2\xi) $$
$$ = 8\xi^3 - 4\xi - 8\xi = 8\xi^3 - 12\xi $$
这个结果与我们之前在验证薛定谔方程时所用的多项式完全相同。这个[递推关系](@entry_id:189264)在理论推导和数值计算中都极其有用。

### 基本性质及其物理意义

埃尔米特多项式拥有一系列优美的数学性质，这些性质直接转化为了[量子谐振子](@entry_id:140678)[波函数](@entry_id:147440)的物理特性。

#### 宇称性

埃尔米特多项式具有明确的**宇称性 (parity)**，即在[自变量](@entry_id:267118)变号时，函数或者不变，或者变号：
$$ H_n(-\xi) = (-1)^n H_n(\xi) $$
这意味着，当 $n$ 是偶数时，$H_n(\xi)$ 是一个[偶函数](@entry_id:163605)；当 $n$ 是奇数时，$H_n(\xi)$ 是一个奇函数。这个性质可以从生成函数简洁地证明 [@problem_id:2096788]。考虑 $G(-\xi, -t)$：
$$ G(-\xi, -t) = \exp(2(-\xi)(-t) - (-t)^2) = \exp(2\xi t - t^2) = G(\xi, t) $$
将其展开为级数：
$$ \sum_{n=0}^{\infty} H_n(-\xi) \frac{(-t)^n}{n!} = \sum_{n=0}^{\infty} H_n(\xi) \frac{t^n}{n!} $$
$$ \sum_{n=0}^{\infty} (-1)^n H_n(-\xi) \frac{t^n}{n!} = \sum_{n=0}^{\infty} H_n(\xi) \frac{t^n}{n!} $$
比较两侧 $t^n$ 的系数，我们立即得到 $H_n(\xi) = (-1)^n H_n(-\xi)$，这等价于 $H_n(-\xi) = (-1)^n H_n(\xi)$。
由于谐振子[波函数](@entry_id:147440) $\psi_n(\xi) = N_n H_n(\xi) \exp(-\xi^2/2)$ 中的高斯因子 $\exp(-\xi^2/2)$ 是[偶函数](@entry_id:163605)，因此[波函数](@entry_id:147440) $\psi_n(\xi)$ 的宇称性完全由 $H_n(\xi)$ 决定。这意味着谐振子的第 $n$ 个能级的[波函数](@entry_id:147440)具有 $(-1)^n$ 的宇称。这一对称性在计算跃迁概率和[期望值](@entry_id:153208)时非常重要，因为它常常能让许多复杂的积分直接等于零。

#### 正交性与权重函数

埃尔米特多项式最重要的性质之一是**正交性 (orthogonality)**。但这种正交性并非简单的 $\int H_m(\xi) H_n(\xi) d\xi = 0$，而是需要一个特定的**权重函数 (weight function)**，即我们在[波函数](@entry_id:147440)中看到的高斯因子 $\exp(-\xi^2)$。完整的[正交关系](@entry_id:145540)是：
$$ \int_{-\infty}^{\infty} H_m(\xi) H_n(\xi) \exp(-\xi^2) d\xi = 0, \quad \text{for } m \neq n $$
当 $m=n$ 时，这个积分给出了[归一化常数](@entry_id:752675)的大小：
$$ \int_{-\infty}^{\infty} [H_n(\xi)]^2 \exp(-\xi^2) d\xi = 2^n n! \sqrt{\pi} $$
这个[正交关系](@entry_id:145540)是量子力学中一个基本原理的体现：一个[厄米算符](@entry_id:153410)（如此处的[哈密顿量](@entry_id:172864)）的不同[本征值](@entry_id:154894)的本征函数是相互正交的。正是埃尔米特多项式的[加权正交性](@entry_id:168186)，保证了不同能级的谐振子[波函数](@entry_id:147440) $\psi_m(x)$ 和 $\psi_n(x)$ 相互正交。

权重函数 $\exp(-\xi^2)$ 的作用是至关重要的。如果缺少它，正交性将不复存在。让我们通过一个例子来理解这一点 [@problem_id:2096747]。考虑不含权重函数的积分 $\int_{-\infty}^{\infty} H_0(\xi) H_2(\xi) d\xi$。我们知道 $H_0(\xi)=1$ 和 $H_2(\xi)=4\xi^2-2$。
$$ I = \int_{-\infty}^{\infty} 1 \cdot (4\xi^2 - 2) d\xi = \lim_{A\to\infty} \int_{-A}^{A} (4\xi^2 - 2) d\xi $$
$$ = \lim_{A\to\infty} \left[ \frac{4}{3}\xi^3 - 2\xi \right]_{-A}^{A} = \lim_{A\to\infty} 2 \left( \frac{4}{3}A^3 - 2A \right) $$
显然，当 $A \to \infty$ 时，这个积分发散到无穷大，而不是零。这清晰地表明，如果没有高斯权重函数来抑制多项式在无穷远处趋于无穷大的行为，埃尔米特多项式本身并不构成一个[正交集](@entry_id:268255)。

### 物理应用

现在我们将这些数学工具和性质应用于解决具体的物理问题。

#### [波函数](@entry_id:147440)与节点

完整的谐振子[定态](@entry_id:137260)[波函数](@entry_id:147440)为 $\psi_n(x) = N_n H_n(\alpha x) \exp(-\frac{1}{2}\alpha^2 x^2)$，其中 $\alpha = \sqrt{m\omega/\hbar}$ 负责将物理坐标 $x$ 转换为无量纲坐标 $\xi = \alpha x$。[波函数](@entry_id:147440)的**节点 (nodes)** 是指在有限位置处[波函数](@entry_id:147440)值为零的点，这些点上发现粒子的概率密度为零。

由于归一化常数 $N_n$ 和指数因子 $\exp(-\frac{1}{2}\alpha^2 x^2)$ 永远不为零，$\psi_n(x)$ 的节点完全由埃尔米特[多项式的根](@entry_id:154615)决定，即满足 $H_n(\alpha x)=0$ 的位置。
例如，让我们找出 $n=2$ [激发态](@entry_id:261453)的节点 [@problem_id:2096783]。该态的[波函数](@entry_id:147440)涉及 $H_2(\xi) = 4\xi^2 - 2$。节点位置满足：
$$ H_2(\alpha x) = 4(\alpha x)^2 - 2 = 0 $$
解这个方程，我们得到 $(\alpha x)^2 = 1/2$，所以 $\alpha x = \pm 1/\sqrt{2}$。将 $x$ 解出来：
$$ x = \pm \frac{1}{\sqrt{2}\alpha} = \pm \frac{1}{\sqrt{2}} \sqrt{\frac{\hbar}{m\omega}} = \pm \sqrt{\frac{\hbar}{2m\omega}} $$
这表明，处于第二[激发态](@entry_id:261453)的粒子，在 $x = \pm \sqrt{\hbar/(2m\omega)}$ 这两个对称的位置上永远不会被发现。一般地，$H_n(\xi)$ 是一个 $n$ 次多项式，它有 $n$ 个实根，这意味着第 $n$ 个[激发态](@entry_id:261453)的[波函数](@entry_id:147440)有 $n$ 个节点。

#### [升降算符](@entry_id:197899)

除了[递推关系](@entry_id:189264)，埃尔米特多项式还与量子谐振子的**[升降算符](@entry_id:197899) (ladder operators)** 密切相关。在无量纲坐标下，**[产生算符](@entry_id:191512)** $\hat{a}^\dagger$ 和**[湮灭算符](@entry_id:165390)** $\hat{a}$ 定义为：
$$ \hat{a}^\dagger = \frac{1}{\sqrt{2}}\left(\xi - \frac{d}{d\xi}\right), \quad \hat{a} = \frac{1}{\sqrt{2}}\left(\xi + \frac{d}{d\xi}\right) $$
它们的作用是使系统在能级阶梯上“上升”或“下降”：$\hat{a}^\dagger \psi_n \propto \psi_{n+1}$ 且 $\hat{a} \psi_n \propto \psi_{n-1}$。
让我们看看[产生算符](@entry_id:191512)作用在[基态](@entry_id:150928)[波函数](@entry_id:147440) $\psi_0(\xi) = N_0 \exp(-\xi^2/2)$ 上的效果 [@problem_id:2096766]。
$$ \hat{a}^\dagger \psi_0(\xi) = \frac{1}{\sqrt{2}}\left(\xi - \frac{d}{d\xi}\right) \left(N_0 \exp(-\frac{\xi^2}{2})\right) $$
$$ = \frac{N_0}{\sqrt{2}}\left(\xi \exp(-\frac{\xi^2}{2}) - (-\xi)\exp(-\frac{\xi^2}{2})\right) $$
$$ = \frac{N_0}{\sqrt{2}}\left(2\xi \exp(-\frac{\xi^2}{2})\right) = \sqrt{2} N_0 \xi \exp(-\frac{\xi^2}{2}) $$
我们注意到结果中的 $\xi$ 因子。由于 $H_1(\xi) = 2\xi$，上式可以写成 $\frac{\sqrt{2}N_0}{2} (2\xi) \exp(-\xi^2/2) \propto H_1(\xi)\exp(-\xi^2/2)$。这表明，[产生算符](@entry_id:191512)作用于[基态](@entry_id:150928)[波函数](@entry_id:147440)，确实生成了与第一[激发态](@entry_id:261453)[波函数](@entry_id:147440) $\psi_1$ 成比例的新函数。这个过程在多项式层面，相当于将 $H_0=1$ 变成了 $H_1 \propto \xi$。

#### 叠加态中的[期望值](@entry_id:153208)

最后，让我们看一个综合性的例子，计算一个处于叠加态的粒子的物理量[期望值](@entry_id:153208) [@problem_id:2096782]。假设一个粒子在 $t=0$ 时刻的状态由[基态](@entry_id:150928)和第一[激发态](@entry_id:261453)的等权重叠加而成：
$$ \Psi(x) = \frac{1}{\sqrt{2}}(\psi_0(x) + \psi_1(x)) $$
我们来计算该状态下粒子位置的[期望值](@entry_id:153208) $\langle x \rangle$。
$$ \langle x \rangle = \int_{-\infty}^{\infty} \Psi^*(x) x \Psi(x) dx $$
由于[波函数](@entry_id:147440)是实函数，$\Psi^* = \Psi$。展开积分：
$$ \langle x \rangle = \frac{1}{2} \int_{-\infty}^{\infty} (\psi_0 + \psi_1) x (\psi_0 + \psi_1) dx $$
$$ = \frac{1}{2} \left( \int \psi_0 x \psi_0 dx + \int \psi_1 x \psi_1 dx + \int \psi_0 x \psi_1 dx + \int \psi_1 x \psi_0 dx \right) $$
这里，宇称性显示出它的威力。$\psi_0$ 是偶函数，$\psi_1$ 是奇函数，$x$ 是奇函数。因此，第一个积分的被积函数 $\psi_0 \cdot x \cdot \psi_0$ 是[奇函数](@entry_id:173259)，在对称区间 $(-\infty, \infty)$ 上的积分为零。同理，第二个积分的被积函数 $\psi_1 \cdot x \cdot \psi_1$ 也是[奇函数](@entry_id:173259)，其积分也为零。
这样，[期望值](@entry_id:153208)就只剩下交叉项：
$$ \langle x \rangle = \frac{1}{2} (0 + 0 + 2 \int_{-\infty}^{\infty} \psi_0(x) x \psi_1(x) dx) = \int_{-\infty}^{\infty} \psi_0(x) x \psi_1(x) dx $$
代入 $\psi_0$ 和 $\psi_1$ 的具体形式 $\psi_0(x) = N_0 H_0(\alpha x) \exp(-\frac{1}{2}\alpha^2x^2)$ 和 $\psi_1(x) = N_1 H_1(\alpha x) \exp(-\frac{1}{2}\alpha^2x^2)$，其中 $H_0=1, H_1=2\alpha x$：
$$ \langle x \rangle = \int_{-\infty}^{\infty} N_0 \exp(-\frac{\alpha^2x^2}{2}) \cdot x \cdot N_1 (2\alpha x) \exp(-\frac{\alpha^2x^2}{2}) dx $$
$$ = 2\alpha N_0 N_1 \int_{-\infty}^{\infty} x^2 \exp(-\alpha^2 x^2) dx $$
这是一个标准的[高斯积分](@entry_id:187139)，$\int_{-\infty}^{\infty} x^2 \exp(-\beta x^2)dx = \frac{\sqrt{\pi}}{2\beta^{3/2}}$。令 $\beta = \alpha^2$，我们得到积分值为 $\frac{\sqrt{\pi}}{2\alpha^3}$。
$$ \langle x \rangle = 2\alpha N_0 N_1 \frac{\sqrt{\pi}}{2\alpha^3} = \frac{N_0 N_1 \sqrt{\pi}}{\alpha^2} $$
代入[归一化常数](@entry_id:752675) $N_0 = (\frac{\alpha}{\sqrt{\pi}})^{1/2}$ 和 $N_1 = (\frac{\alpha}{2\sqrt{\pi}})^{1/2}$，得到：
$$ \langle x \rangle = \frac{1}{\alpha^2} \left(\frac{\alpha^2}{2\pi}\right)^{1/2} \sqrt{\pi} = \frac{1}{\alpha^2} \frac{\alpha}{\sqrt{2\pi}} \sqrt{\pi} = \frac{1}{\sqrt{2}\alpha} $$
这个非零结果表明，尽管该叠加态由两个期望位置为零的[定态](@entry_id:137260)构成，但其自身的期望位置并不为零。这是一个典型的[量子干涉](@entry_id:139127)效应，其具体的计算过程充分展示了如何联合运用埃尔米特多项式的具体形式、宇称性以及正交性等概念来预测物理系统的行为。