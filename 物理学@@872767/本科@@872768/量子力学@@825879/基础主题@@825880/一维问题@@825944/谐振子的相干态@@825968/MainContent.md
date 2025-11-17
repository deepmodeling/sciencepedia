## 引言
[量子谐振子](@entry_id:140678)是量子力学中少数几个可以精确求解的系统之一，其[能量本征态](@entry_id:152154)（或称数态）构成了理解[量子化能级](@entry_id:140911)的基础。然而，这些[定态](@entry_id:137260)的性质——例如位置和动量[期望值](@entry_id:153208)始终为零——与我们在宏观世界中观察到的[振荡](@entry_id:267781)粒子行为大相径庭。那么，我们如何用量子力学来描述一个像经典粒子一样来回[振荡](@entry_id:267781)的系统，或者一个像[激光](@entry_id:194225)一样具有稳定振幅和相位的[电磁场](@entry_id:265881)呢？这个知识鸿沟正是引入**相干态 (coherent states)** 的初衷。

[相干态](@entry_id:154533)是连接微观量子世界与宏观经典世界的关键桥梁，它们是量子力学中最接近[经典谐振子](@entry_id:153404)的态。本文将系统地引导你深入理解相干态的迷人世界。

*   在**原理和机制**一章中，我们将从第一性原理出发，定义[相干态](@entry_id:154533)为[湮灭算符](@entry_id:165390)的本征态，推导其在数态[基矢](@entry_id:199546)下的展开，并揭示其最小不确定性、[非正交性](@entry_id:192553)以及动力学演化等核心性质。
*   接着，在**应用与跨学科联系**一章中，我们将展示[相干态](@entry_id:154533)如何作为一种强大工具，应用于[量子光学](@entry_id:140582)、原子物理、[精密测量](@entry_id:145551)等前沿领域，并探讨其在构建薛定谔猫态等非经典态中的作用。
*   最后，通过**动手实践**部分，你将有机会通过解决具体问题来巩固所学知识，亲手计算[相干态](@entry_id:154533)的演化和性质，加深对理论的理解。

通过这趟旅程，你将掌握[相干态](@entry_id:154533)的理论精髓，并领略其在现代物理和技术中的广泛应用。

## 原理和机制

在前一章中，我们介绍了[量子谐振子](@entry_id:140678)及其以分立能级为特征的[定态](@entry_id:137260)，即能量本征态或数态 $|n\rangle$。虽然这些定态是求解时间无关薛定谔方程的基础，但它们在某些方面与我们对经典[振子](@entry_id:271549)的直观理解相去甚远。例如，在任何一个[能量本征态](@entry_id:152154)中，位置和动量的[期望值](@entry_id:153208)都为零，即 $\langle n|\hat{x}|n \rangle = 0$ 和 $\langle n|\hat{p}|n \rangle = 0$。这描绘了一幅静态的画面，与一个在[势阱](@entry_id:151413)中来回[振荡](@entry_id:267781)的经典粒子形成鲜明对比。

为了弥合这一差距，并描述像[激光](@entry_id:194225)场这样表现出稳定[振荡](@entry_id:267781)行为的量子系统，我们需要一种新的[量子态](@entry_id:146142)。这些态，被称为**[相干态](@entry_id:154533) (coherent states)**，是量子力学中最接近[经典谐振子](@entry_id:153404)的描述。本章将深入探讨[相干态](@entry_id:154533)的定义、数学结构、独特性质及其迷人的动力学行为。

### 定义[相干态](@entry_id:154533)：[湮灭算符](@entry_id:165390)的[本征态](@entry_id:149904)

我们寻求一种[量子态](@entry_id:146142)，其期望行为能模拟经典[振子](@entry_id:271549)的轨迹。一个富有成效的途径是通过谐振子的[升降算符](@entry_id:197899)来定义这些态。回顾一下，[湮灭算符](@entry_id:165390) $\hat{a}$ 和创造算符 $\hat{a}^\dagger$ 是通过位置算符 $\hat{x}$ 和动量算符 $\hat{p}$ [线性组合](@entry_id:154743)而成的：

$$
\hat{a} = \sqrt{\frac{m\omega}{2\hbar}}\left(\hat{x} + \frac{i}{m\omega}\hat{p}\right)
$$
$$
\hat{a}^\dagger = \sqrt{\frac{m\omega}{2\hbar}}\left(\hat{x} - \frac{i}{m\omega}\hat{p}\right)
$$

一个关键的事实是，湮灭算符 $\hat{a}$ 不是厄米算符 ($\hat{a} \neq \hat{a}^\dagger$)。这意味着它的[本征值](@entry_id:154894)不一定是实数，并且它的本征态（如果存在）不一定相互正交。正是这一特性为我们打开了一扇通往新物理的窗户。

我们将**[相干态](@entry_id:154533)** $|\alpha\rangle$ 定义为湮灭算符 $\hat{a}$ 的右本征态，其对应的[本征值](@entry_id:154894)为一个复数 $\alpha$。[@problem_id:2922375]

$$
\hat{a} |\alpha\rangle = \alpha |\alpha\rangle
$$

这个定义是构建[相干态](@entry_id:154533)理论的基石。复数 $\alpha$ 可以写成 $\alpha = |\alpha|e^{i\delta}$，它包含了描述经典[振荡](@entry_id:267781)的两个关键参数：振幅和相位，这一点我们稍后会看到。由于 $\hat{a}$ 是非厄米的，其[本征态](@entry_id:149904) $|\alpha\rangle$ 和左本征态 $\langle\alpha|$（即 $\langle\alpha|\hat{a}^\dagger = \alpha^*\langle\alpha|$）的行为将展现出一些与厄米算符本征态截然不同的特性。

### [相干态](@entry_id:154533)的结构：数态的叠加

为了更好地理解[相干态](@entry_id:154533)的物理内容，我们可以在[量子谐振子](@entry_id:140678)更熟悉的能量本征态（或数态）$\{ |n\rangle \}$ [基矢](@entry_id:199546)上展开它。数态构成了完备正交归一的[基矢](@entry_id:199546)。因此，任何[相干态](@entry_id:154533) $|\alpha\rangle$ 都可以写成它们的线性叠加：

$$
|\alpha\rangle = \sum_{n=0}^{\infty} c_n |n\rangle
$$

其中 $c_n = \langle n|\alpha\rangle$ 是我们希望确定的展开系数。将定义式 $\hat{a}|\alpha\rangle = \alpha|\alpha\rangle$ 应用于这个展开式，我们得到：

$$
\hat{a} \left( \sum_{n=0}^{\infty} c_n |n\rangle \right) = \alpha \left( \sum_{n=0}^{\infty} c_n |n\rangle \right)
$$

利用湮灭算符对数态的作用规则 $\hat{a}|n\rangle = \sqrt{n}|n-1\rangle$（对于 $n \ge 1$）和 $\hat{a}|0\rangle = 0$，上式左边变为：

$$
\sum_{n=1}^{\infty} c_n \sqrt{n} |n-1\rangle = \sum_{n=0}^{\infty} \alpha c_n |n\rangle
$$

为了比较系数，我们对左边的求和变元进行替换，令 $k = n-1$。这样，求和就从 $k=0$ 开始：

$$
\sum_{k=0}^{\infty} c_{k+1} \sqrt{k+1} |k\rangle = \sum_{n=0}^{\infty} \alpha c_n |n\rangle
$$

由于数态 $\{|n\rangle\}$ 是正交的，我们可以逐项比较各项的系数，得到关于系数 $c_n$ 的递推关系：

$$
c_{n+1} \sqrt{n+1} = \alpha c_n \quad \implies \quad c_{n+1} = \frac{\alpha}{\sqrt{n+1}} c_n
$$

通过迭代求解这个递推关系，我们可以将任意系数 $c_n$ 用 $c_0$ 表示：

$$
c_n = \frac{\alpha^n}{\sqrt{n!}} c_0
$$

剩下的系数 $c_0$ 由[归一化条件](@entry_id:156486) $\langle\alpha|\alpha\rangle = 1$ 确定。

$$
\langle\alpha|\alpha\rangle = \sum_{n=0}^{\infty} |c_n|^2 = |c_0|^2 \sum_{n=0}^{\infty} \frac{|\alpha|^{2n}}{n!} = 1
$$

我们认出上式中的求和是[指数函数](@entry_id:161417)的泰勒级数展开 $\sum_{k=0}^{\infty} \frac{x^k}{k!} = \exp(x)$。因此，$|c_0|^2 \exp(|\alpha|^2) = 1$。选择一个方便的相位约定，令 $c_0$ 为实数且为正，我们得到 $c_0 = \exp(-|\alpha|^2/2)$。代回 $c_n$ 的表达式，我们最终得到[相干态](@entry_id:154533)在数态[基矢](@entry_id:199546)下的完整形式：[@problem_id:2922375]

$$
|\alpha\rangle = \exp\left(-\frac{|\alpha|^2}{2}\right) \sum_{n=0}^{\infty} \frac{\alpha^n}{\sqrt{n!}} |n\rangle
$$

这个展开式揭示了相干态的深刻结构：它是一个包含了所有数态的无限叠加。一个处于[相干态](@entry_id:154533)的[振子](@entry_id:271549)被测量时，可能发现它处于任何一个能级 $|n\rangle$。在能级 $|n\rangle$ 上发现它的概率 $P(n)$ 是：

$$
P(n) = |\langle n|\alpha\rangle|^2 = |c_n|^2 = \exp(-|\alpha|^2) \frac{|\alpha|^{2n}}{n!}
$$

这正是**[泊松分布](@entry_id:147769) (Poisson distribution)** 的形式，其平均值为 $\lambda = |\alpha|^2$。这为复数参数 $\alpha$ 提供了清晰的物理解释：$|\alpha|^2$ 是在[相干态](@entry_id:154533)中测量到的[平均能量](@entry_id:145892)量子数（或粒子数）。我们可以通过直接计算数算符 $\hat{N} = \hat{a}^\dagger\hat{a}$ 的[期望值](@entry_id:153208)来验证这一点：

$$
\langle \hat{N} \rangle = \langle\alpha|\hat{a}^\dagger\hat{a}|\alpha\rangle = \langle\alpha|\hat{a}^\dagger(\alpha|\alpha\rangle) = \alpha \langle\alpha|\hat{a}^\dagger|\alpha\rangle = \alpha (\alpha^* \langle\alpha|\alpha\rangle) = |\alpha|^2
$$

因此，参数 $\alpha$ 的模平方直接对应于[振子](@entry_id:271549)的[平均激发能](@entry_id:160327)级。

### 相干态的性质：[非正交性](@entry_id:192553)与过完备性

正如之前提到的，相干态是作为非[厄米算符](@entry_id:153410) $\hat{a}$ 的本征态出现的，这导致它们形成一个在几何上非常独特的态集合。我们可以通过计算两个不同相干态 $|\alpha\rangle$ 和 $|\beta\rangle$ 的[内积](@entry_id:158127)来探究这一点。利用它们的数态展开式：

$$
\langle\beta|\alpha\rangle = \left( \exp\left(-\frac{|\beta|^2}{2}\right) \sum_{m=0}^{\infty} \frac{(\beta^*)^m}{\sqrt{m!}} \langle m| \right) \left( \exp\left(-\frac{|\alpha|^2}{2}\right) \sum_{n=0}^{\infty} \frac{\alpha^n}{\sqrt{n!}} |n\rangle \right)
$$

利用数态的正交归一性 $\langle m|n\rangle = \delta_{mn}$，双[重求和](@entry_id:275405)简化为单一求和：

$$
\langle\beta|\alpha\rangle = \exp\left(-\frac{|\alpha|^2}{2} - \frac{|\beta|^2}{2}\right) \sum_{n=0}^{\infty} \frac{(\beta^*\alpha)^n}{n!}
$$

再次利用[指数函数](@entry_id:161417)的[级数展开](@entry_id:142878)，我们得到一个优美的[封闭形式](@entry_id:272960)：

$$
\langle\beta|\alpha\rangle = \exp\left(-\frac{1}{2}|\alpha|^2 - \frac{1}{2}|\beta|^2 + \beta^*\alpha\right)
$$

这个结果的模平方同样简洁：[@problem_id:2105943] [@problem_id:1378222]

$$
|\langle\beta|\alpha\rangle|^2 = \left| \exp\left(-\frac{1}{2}|\alpha|^2 - \frac{1}{2}|\beta|^2 + \beta^*\alpha\right) \right|^2 = \exp\left(-|\alpha|^2 - |\beta|^2 + 2\text{Re}(\beta^*\alpha)\right) = \exp\left(-|\alpha-\beta|^2\right)
$$

这个公式揭示了[相干态](@entry_id:154533)的两个基本性质：

1.  **[非正交性](@entry_id:192553) (Non-orthogonality)**：只要 $\alpha \neq \beta$，[内积](@entry_id:158127) $\langle\beta|\alpha\rangle$ 就永远不为零。这意味着任意两个不同的[相干态](@entry_id:154533)都不是正交的。这与厄米算符（如[哈密顿算符](@entry_id:144286) $\hat{H}$ 或位置算符 $\hat{x}$）的本征态形成鲜明对比，后者的不同本征态总是相互正交的。从物理上讲，这意味着我们永远无法通过一次测量完美地区分两个不同的[相干态](@entry_id:154533)。

2.  **[线性无关](@entry_id:148207)性 (Linear Independence)**：对于 $\alpha \neq \beta$，我们总是有 $|\langle\beta|\alpha\rangle|^2  1$。根据柯西-施瓦茨不等式，两个归一化向量的[内积](@entry_id:158127)模平方等于1的充要条件是它们线性相关（即一个向量是另一个的复数倍）。因此，任意两个不同的[相干态](@entry_id:154533)都是线性无关的。[@problem_id:1378222]

这两个性质共同指向一个更深层次的概念：**过完备性 (overcompleteness)**。[相干态](@entry_id:154533)的集合 $\{|\alpha\rangle\}$ 覆盖了整个谐振子的[希尔伯特空间](@entry_id:261193)，但它们不是一个[基矢](@entry_id:199546)，因为它们不是线性无关的最小集合。它们是“冗余的”，向量比构成[基矢](@entry_id:199546)所必需的要多。尽管如此，这种过完备性在量子光学的理论形式中非常有用，因为它允许将任意态分解为[相干态](@entry_id:154533)的积分。

### 相干态的动力学：经典对应

相干态最引人注目的特性在于其[时间演化](@entry_id:153943)行为。它们在[谐振子势](@entry_id:750179)阱中的运动完美地再现了我们对经典[振荡](@entry_id:267781)粒子的期望，从而为[量子-经典对应](@entry_id:155778)原理提供了最清晰的例证之一。

#### [时间演化](@entry_id:153943)

让我们考察一个初始状态为相干态 $|\Psi(0)\rangle = |\alpha\rangle$ 的系统。其随时间的演化由薛定谔方程决定，形式解为 $|\Psi(t)\rangle = \exp(-i\hat{H}t/\hbar)|\Psi(0)\rangle$。对于谐振子[哈密顿量](@entry_id:172864) $\hat{H} = \hbar\omega(\hat{a}^\dagger\hat{a} + 1/2)$，我们可以通过分析[湮灭算符](@entry_id:165390)在[海森堡绘景](@entry_id:141162)中的演化来巧妙地确定 $|\Psi(t)\rangle$ 的形式。

[海森堡绘景](@entry_id:141162)中的[湮灭算符](@entry_id:165390) $\hat{a}_H(t)$ 定义为 $\hat{a}_H(t) = e^{i\hat{H}t/\hbar} \hat{a} e^{-i\hat{H}t/\hbar}$。其运动方程为：

$$
\frac{d}{dt}\hat{a}_H(t) = \frac{i}{\hbar}[\hat{H}, \hat{a}_H(t)]
$$

我们可以方便地在[薛定谔绘景](@entry_id:144112)中计算对易子 $[\hat{H}, \hat{a}] = \hbar\omega[\hat{a}^\dagger\hat{a}, \hat{a}] = -\hbar\omega\hat{a}$。因此，$\hat{a}_H(t)$ 的[运动方程](@entry_id:170720)变为一个简单的[一阶微分方程](@entry_id:173139)：

$$
\frac{d}{dt}\hat{a}_H(t) = -i\omega \hat{a}_H(t)
$$

该方程的解为 $\hat{a}_H(t) = \hat{a}_H(0)e^{-i\omega t} = \hat{a}e^{-i\omega t}$。现在，我们让湮灭算符 $\hat{a}$ 作用于[时间演化](@entry_id:153943)后的态 $|\Psi(t)\rangle$：

$$
\hat{a}|\Psi(t)\rangle = \hat{a}e^{-i\hat{H}t/\hbar}|\alpha\rangle = (e^{-i\hat{H}t/\hbar}e^{i\hat{H}t/\hbar}) \hat{a} e^{-i\hat{H}t/\hbar}|\alpha\rangle = e^{-i\hat{H}t/\hbar} \hat{a}_H(t) |\alpha\rangle
$$

将 $\hat{a}_H(t)$ 的解代入，并利用 $|\alpha\rangle$ 是 $\hat{a}$ 的本征态这一事实：

$$
\hat{a}|\Psi(t)\rangle = e^{-i\hat{H}t/\hbar} (\hat{a}e^{-i\omega t}) |\alpha\rangle = e^{-i\omega t} e^{-i\hat{H}t/\hbar} (\hat{a}|\alpha\rangle) = e^{-i\omega t} e^{-i\hat{H}t/\hbar} (\alpha|\alpha\rangle) = (\alpha e^{-i\omega t}) |\Psi(t)\rangle
$$

这个优美的结果表明，**一个[相干态](@entry_id:154533)在谐振子势中演化后，仍然是一个[相干态](@entry_id:154533)**。[@problem_id:2918113] 它的[本征值](@entry_id:154894)从 $\alpha$ 变为随时间演化的 $\alpha(t) = \alpha e^{-i\omega t}$。这意味着态 $|\Psi(t)\rangle$ 与相干态 $|\alpha(t)\rangle$ 只相差一个相位因子。通过在数态[基矢](@entry_id:199546)上直接进行演化可以证明，这个完整的演化态是：[@problem_id:2030461]

$$
|\Psi(t)\rangle = e^{-i\omega t/2} |\alpha e^{-i\omega t}\rangle
$$

复数[本征值](@entry_id:154894) $\alpha(t)$ 在复平面上以[角频率](@entry_id:261565) $\omega$ 顺时针旋转。这种确定[性的演化](@entry_id:163338)行为是[相干态](@entry_id:154533)呈现经典性的根源。顺便提一下，由于[能量本征值](@entry_id:144381) $E_n = \hbar\omega(n+1/2)$ 之间的等间距特性，可观测量的[期望值](@entry_id:153208)会以周期 $T=2\pi/\omega$ 恢复。而整个[量子态](@entry_id:146142)[波函数](@entry_id:147440)（包括[全局相位](@entry_id:147947)）的精确恢复，则需要一个两倍的周期，即量子复兴时间 $T_{rev} = 4\pi/\omega$。[@problem_id:2140790]

#### 经典轨迹

现在我们来计算位置和动量[期望值](@entry_id:153208)的演化，看看它们如何体现经典行为。利用 $\hat{x}$ 和 $\hat{p}$ 与[升降算符](@entry_id:197899)的关系，以及 $\langle\Psi(t)|\hat{a}|\Psi(t)\rangle = \alpha(t) = \alpha e^{-i\omega t}$ 和 $\langle\Psi(t)|\hat{a}^\dagger|\Psi(t)\rangle = \alpha^*(t) = \alpha^* e^{i\omega t}$，我们可以计算[期望值](@entry_id:153208)。

[位置期望值](@entry_id:171721)为：
$$
\langle\hat{x}\rangle(t) = \left\langle \sqrt{\frac{\hbar}{2m\omega}}(\hat{a} + \hat{a}^\dagger) \right\rangle(t) = \sqrt{\frac{\hbar}{2m\omega}} (\alpha e^{-i\omega t} + \alpha^* e^{i\omega t})
$$

动量[期望值](@entry_id:153208)为：
$$
\langle\hat{p}\rangle(t) = \left\langle i\sqrt{\frac{\hbar m\omega}{2}}(\hat{a}^\dagger - \hat{a}) \right\rangle(t) = i\sqrt{\frac{\hbar m\omega}{2}} (\alpha^* e^{i\omega t} - \alpha e^{-i\omega t})
$$

为了看到更熟悉的[振荡](@entry_id:267781)形式，我们将初始复数 $\alpha$ 写成极坐标形式 $\alpha = |\alpha|e^{i\delta}$。代入后得到：[@problem_id:2030461]

$$
\langle\hat{x}\rangle(t) = \sqrt{\frac{2\hbar}{m\omega}} |\alpha| \cos(\delta - \omega t)
$$
$$
\langle\hat{p}\rangle(t) = \sqrt{2\hbar m\omega} |\alpha| \sin(\delta - \omega t) = m\omega \sqrt{\frac{2\hbar}{m\omega}} |\alpha| \sin(\delta - \omega t)
$$

这些方程正是质量为 $m$、[角频率](@entry_id:261565)为 $\omega$ 的[经典谐振子](@entry_id:153404)的[运动方程](@entry_id:170720)！期望位置 $\langle\hat{x}\rangle(t)$ 和期望动量 $\langle\hat{p}\rangle(t)$ 遵循正弦和余弦规律，振幅为 $x_{max} = \sqrt{2\hbar/(m\omega)}|\alpha|$，初始相位由 $\delta$ 决定。这清晰地表明，[相干态](@entry_id:154533)[波包](@entry_id:154698)的中心以经典方式在[势阱](@entry_id:151413)中[振荡](@entry_id:267781)。[@problem_id:2918113]

#### 最小不确定性与非展宽波包

相干态的经典特性不仅体现在其[期望值](@entry_id:153208)的轨迹上，还体现在其[波包](@entry_id:154698)的形状稳定性上。为了探究这一点，我们计算位置和动量的不确定性（标准差）。不确定性 $\Delta Q$ 定义为 $\Delta Q = \sqrt{\langle\hat{Q}^2\rangle - \langle\hat{Q}\rangle^2}$。

通过细致的代数运算，利用 $\langle\hat{a}\rangle = \alpha$, $\langle\hat{a}^\dagger\rangle = \alpha^*$, $\langle\hat{a}^2\rangle = \alpha^2$, $\langle\hat{a}^{\dagger 2}\rangle = \alpha^{*2}$, 以及 $[\hat{a}, \hat{a}^\dagger]=1$ 导出的 $\langle\hat{a}\hat{a}^\dagger\rangle = |\alpha|^2+1$ 和 $\langle\hat{a}^\dagger\hat{a}\rangle = |\alpha|^2$，我们可以计算出[方差](@entry_id:200758)：

$$
(\Delta x)^2 = \langle\hat{x}^2\rangle - \langle\hat{x}\rangle^2 = \frac{\hbar}{2m\omega}
$$
$$
(\Delta p)^2 = \langle\hat{p}^2\rangle - \langle\hat{p}\rangle^2 = \frac{\hbar m\omega}{2}
$$

令人惊讶的是，这些[方差](@entry_id:200758)完全不依赖于参数 $\alpha$。这意味着所有[相干态](@entry_id:154533)，无论其[平均能量](@entry_id:145892)或相位如何，都具有完全相同的位置和动量不确定性。实际上，它们与[谐振子基](@entry_id:750178)态 $|0\rangle$（即 $\alpha=0$ 的相干态）的不确定性完全相同。

现在，我们计算不确定性乘积：[@problem_id:2084532] [@problem_id:2139465]

$$
\Delta x \Delta p = \sqrt{\frac{\hbar}{2m\omega}} \cdot \sqrt{\frac{\hbar m\omega}{2}} = \frac{\hbar}{2}
$$

这个结果等于[海森堡不确定性原理](@entry_id:171099)给出的理论最小值 $(\Delta x \Delta p \ge \hbar/2)$。因此，相干态是**最小不确定性态 (minimum uncertainty states)**。

更重要的是，由于这些不确定性不依赖于 $\alpha$，而时间演化只是将 $\alpha$ 替换为 $\alpha(t)=\alpha e^{-i\omega t}$，所以**[相干态](@entry_id:154533)的不确定性在时间演化中保持恒定**。这意味着相干态波包在[势阱](@entry_id:151413)中[振荡](@entry_id:267781)时，其形状和大小（宽度）保持不变。

这种行为与自由空间中的[高斯波包](@entry_id:151158)形成鲜明对比。一个[自由粒子](@entry_id:148748)的[高斯波包](@entry_id:151158)，即使初始时是最小不确定性的，其位置不确定性也必然会随着时间增长，即波包会“展宽”。而对于谐振子势中的[相干态](@entry_id:154533)，[势阱](@entry_id:151413)的“聚焦”效应恰好抵消了[波包](@entry_id:154698)固有的[扩散](@entry_id:141445)趋势，使其成为一个稳定的、**非展宽[波包](@entry_id:154698) (non-spreading wavepacket)**。[@problem_id:2148910]

总结来说，相干态之所以被誉为最“经典”的[量子态](@entry_id:146142)，是因为它们集三个关键特征于一身：
1.  其期望位置和动量精确地遵循经典运动方程。
2.  它们在任何时刻都饱和了海森堡[不确定性关系](@entry_id:186128)，是最小不确定性态。
3.  它们在[演化过程](@entry_id:175749)中保持形状不变，是一个非展宽的稳定[波包](@entry_id:154698)。

这些独特的原理和机制使[相干态](@entry_id:154533)成为连接宏观经典世界和微观量子世界的关键桥梁，并在[量子光学](@entry_id:140582)、量子信息和凝聚态物理等领域扮演着至关重要的角色。