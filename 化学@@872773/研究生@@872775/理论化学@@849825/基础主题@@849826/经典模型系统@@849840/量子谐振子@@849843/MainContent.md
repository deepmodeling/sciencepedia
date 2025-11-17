## 引言
量子谐振子 (Quantum Harmonic Oscillator, QHO) 是现代物理学与[理论化学](@entry_id:199050)中最重要的基石模型之一。作为少数几个可以精确求解的量子力学体系，它不仅是理论教学中的典范，更是理解从[化学键](@entry_id:138216)[振动](@entry_id:267781)到[量子场论](@entry_id:138177)等众多复杂物理现象的出发点。然而，QH[O模](@entry_id:186318)型的真正威力并不仅仅在于其数学上的简洁性，更在于它作为一种强大近似方法的普适性。对于研究生水平的学习者而言，关键的挑战在于理解如何将这个理想化的模型应用和扩展到真实的、复杂的化学与物理系统中，从而弥合理论与实践之间的鸿沟。

本文旨在系统性地引导读者完成这一认知飞跃。首先，在“原理与机制”一章中，我们将深入其核心的数学框架，特别是强大的代数方法，以揭示其量子化的本质。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章，我们将展示该模型如何作为分析工具，被广泛应用于[分子光谱学](@entry_id:148164)、[统计热力学](@entry_id:147111)和[开放量子系统](@entry_id:138632)等前沿领域。最后，“动手实践”部分将提供具体问题，帮助读者巩固所学，将理论知识转化为解决实际问题的能力。我们的探索将从量子谐振子最根本的物理原理和数学表述开始，为后续更广泛的应用奠定坚实的基础。

## 原理与机制

本章深入探讨量子谐振子的核心原理与机制。在前一章介绍其在[物理化学](@entry_id:145220)中的广泛应用背景之后，我们现在转向其精确的数学表述和求解方法。我们将从经典力学过渡到量子力学，建立[量子谐振子](@entry_id:140678)的[哈密顿算符](@entry_id:144286)，并重点介绍解决其量子行为的强大代数方法。通过这种方法，我们将推导出其分立的能谱和对应的本征态。此外，我们还将探讨这些[量子态](@entry_id:146142)的基本性质，如宇称和[不确定性关系](@entry_id:186128)，并进一步介绍相空间中的[准概率分布](@entry_id:203668)，以及在[量子化学](@entry_id:140193)和量子光学中至关重要的[相干态](@entry_id:154533)。

### 从经典到量子：[正则量子化](@entry_id:148501)

[量子谐振子](@entry_id:140678)理论的起点是其经典力学对应物。一个质量为 $m$、角频率为 $\omega$ 的一维[经典谐振子](@entry_id:153404)，其[哈密顿量](@entry_id:172864) $H$ 是动能与[势能](@entry_id:748988)之和：

$H = \frac{p^2}{2m} + \frac{1}{2}m\omega^2x^2$

其中，$x$ 是位移，$p$ 是动量。在哈密顿力学中，系统的动力学由正则变量 $x$ 和 $p$ 的[泊松括号](@entry_id:151133) $\{x, p\} = 1$ 决定。

过渡到量子力学，我们采用 **[正则量子化](@entry_id:148501)** 的方法。这一过程的核心思想是将经典物理量（可观测量）提升为在[希尔伯特空间](@entry_id:261193) $\mathcal{H}$ 上作用的算符，并将泊松括号与算符的对易子联系起来。[Paul Dirac](@entry_id:155530) 提出的对应规则是：

$\\{f, g\\} \mapsto \frac{1}{i\hbar}[\hat{f}, \hat{g}]$

其中 $\hat{f}$ 和 $\hat{g}$ 是对应于经典[可观测量](@entry_id:267133) $f$ 和 $g$ 的[量子算符](@entry_id:137703)，$\hbar$ 是[约化普朗克常数](@entry_id:275910)。将此规则应用于正则变量 $x$ 和 $p$，我们得到量子力学中最基本的 **[正则对易关系](@entry_id:185041) (Canonical Commutation Relation, CCR)**：

$[\hat{x}, \hat{p}] = i\hbar \hat{I}$

其中 $\hat{I}$ 是单位算符。相应地，[量子谐振子](@entry_id:140678)的[哈密顿算符](@entry_id:144286) $\hat{H}$ 形式上与经典[哈密顿量](@entry_id:172864)相似：

$\hat{H} = \frac{\hat{p}^2}{2m} + \frac{1}{2}m\omega^2\hat{x}^2$

然而，这个看似简单的推广背后隐藏着深刻的数学结构。一个关键的数学事实是，满足 CCR 的算符 $\hat{x}$ 和 $\hat{p}$ 必须是 **无界算符**。这意味着它们不能在整个希尔伯特空间 $\mathcal{H}$ 上都有定义，而只能定义在一个稠密的[子空间](@entry_id:150286)（称为定义域）上。为了确保这些算符对应于[物理可观测量](@entry_id:154692)（其测量结果必须是实数）并且能够生成物理变换（如[时间演化](@entry_id:153943)），它们必须是 **自伴算符**。

为了严格地建立一个满足 CCR 的唯一（在[酉等价](@entry_id:197898)意义下）的自伴算符 $\hat{x}$ 和 $\hat{p}$ 的表示，我们需要诉诸于 CCR 的指数形式，即 **外尔关系 (Weyl relations)**。**[Stone-von Neumann 定理](@entry_id:189284)** 保证了，在一个可分的[复希尔伯特空间](@entry_id:185216)上，外尔关系的任何强连续、不可约表示都[酉等价](@entry_id:197898)于标准的薛定谔表示。这个严格的数学框架确保了量子谐振子[哈密顿算符](@entry_id:144286) $\hat{H}$ 的谱和动力学是唯一且良定义的 [@problem_id:2918148]。尽管这些数学细节对于研究生水平的理论化学家至关重要，但在接下来的讨论中，我们将主要聚焦于由这些关系所产生的[代数结构](@entry_id:137052)及其物理推论。

### 代数方法：[升降算符](@entry_id:197899)

虽然可以通过在坐标表象中求解[哈密顿算符](@entry_id:144286)的[本征值问题](@entry_id:142153)（一个[二阶常微分方程](@entry_id:204212)，即定态薛定谔方程）来找到量子谐振子的[能谱](@entry_id:181780)，但一种更深刻、更普适的方法是 **代数方法**。这种方法完全在算符的框架内进行，避免了求解微分方程。

第一步是引入无量纲的算符以简化代数运算。我们通过系统的固有参数 $m$, $\omega$, $\hbar$ 来定义特征长度和动量标度 [@problem_id:2918094]：

$x_0 = \sqrt{\frac{\hbar}{m\omega}}$,  $p_0 = \sqrt{m\hbar\omega}$

注意 $x_0 p_0 = \hbar$。然后我们定义无量纲的坐标和动量算符 $\hat{X}$ 和 $\hat{P}$ [@problem_id:2918133]：

$\hat{X} = \frac{\hat{x}}{x_0} = \sqrt{\frac{m\omega}{\hbar}}\hat{x}$

$\hat{P} = \frac{\hat{p}}{p_0} = \frac{1}{\sqrt{m\hbar\omega}}\hat{p}$

通过这些新算符，[哈密顿算符](@entry_id:144286)变为一个对称的形式：

$\hat{H} = \frac{\hbar\omega}{2}(\hat{P}^2 + \hat{X}^2)$

而[正则对易关系](@entry_id:185041)也简化为：

$[\hat{X}, \hat{P}] = \frac{1}{x_0 p_0}[\hat{x}, \hat{p}] = \frac{1}{\hbar}(i\hbar) = i$

接下来，我们引入两个新的非[厄米算符](@entry_id:153410)，**湮灭算符 (annihilation operator)** $\hat{a}$ 和 **[产生算符](@entry_id:191512) (creation operator)** $\hat{a}^\dagger$：

$\hat{a} = \frac{1}{\sqrt{2}}(\hat{X} + i\hat{P})$

$\hat{a}^\dagger = \frac{1}{\sqrt{2}}(\hat{X} - i\hat{P})$

这里 $\hat{a}^\dagger$ 是 $\hat{a}$ 的[厄米共轭](@entry_id:191215)。请注意，在 $\hat{a}$ 的定义中，$\hat{P}$ 前的因子 $i$ 的选择至关重要。这个相位的选择是为了得到一个最简洁的对易关系。我们可以直接计算 $[\hat{a}, \hat{a}^\dagger]$ [@problem_id:2918094] [@problem_id:2918133]：

$[\hat{a}, \hat{a}^\dagger] = \frac{1}{2}[(\hat{X} + i\hat{P}), (\hat{X} - i\hat{P})] = \frac{1}{2}([\hat{X}, -i\hat{P}] + [i\hat{P}, \hat{X}]) = \frac{1}{2}(-i[\hat{X}, \hat{P}] - i[\hat{X}, \hat{P}]) = -i[\hat{X}, \hat{P}]$

将 $[\hat{X}, \hat{P}] = i$ 代入，我们得到它们的基本[对易关系](@entry_id:136780)：

$[\hat{a}, \hat{a}^\dagger] = -i(i) = 1$

这种[代数结构](@entry_id:137052)是[玻色子](@entry_id:138266)场的典型特征，因此 $\hat{a}$ 和 $\hat{a}^\dagger$ 也被称为[玻色算符](@entry_id:148361)。

最后，我们将[哈密顿算符](@entry_id:144286)用这些新算符表示。首先，我们反解出 $\hat{X}$ 和 $\hat{P}$：

$\hat{X} = \frac{1}{\sqrt{2}}(\hat{a} + \hat{a}^\dagger)$

$\hat{P} = \frac{1}{i\sqrt{2}}(\hat{a} - \hat{a}^\dagger)$

将它们代入 $\hat{H} = \frac{\hbar\omega}{2}(\hat{X}^2 + \hat{P}^2)$ 中，经过一番代数运算和利用 $[\hat{a}, \hat{a}^\dagger]=1$ (即 $\hat{a}\hat{a}^\dagger = \hat{a}^\dagger\hat{a} + 1$)，可以得到：

$\hat{H} = \frac{\hbar\omega}{2}(\hat{a}^\dagger\hat{a} + \hat{a}\hat{a}^\dagger) = \frac{\hbar\omega}{2}(\hat{a}^\dagger\hat{a} + \hat{a}^\dagger\hat{a} + 1) = \hbar\omega(\hat{a}^\dagger\hat{a} + \frac{1}{2})$

我们定义 **数量算符 (number operator)** $\hat{N} = \hat{a}^\dagger\hat{a}$。这是一个厄米算符，其[本征值](@entry_id:154894)将代表系统中的能量[量子数](@entry_id:145558)。于是，[哈密顿算符](@entry_id:144286)最终写为极其简洁的形式：

$\hat{H} = \hbar\omega(\hat{N} + \frac{1}{2})$

这个表达式揭示了，求解[哈密顿算符](@entry_id:144286) $\hat{H}$ 的[能谱](@entry_id:181780)等价于求解数量算符 $\hat{N}$ 的谱。

### [能谱](@entry_id:181780)和本征态

现在我们利用算符代数来推导 $\hat{N}$ 的[本征值](@entry_id:154894)和本征矢。首先，我们需要 $\hat{N}$ 与 $\hat{a}$ 和 $\hat{a}^\dagger$ 的[对易关系](@entry_id:136780) [@problem_id:2918144]：

$[\hat{N}, \hat{a}] = [\hat{a}^\dagger\hat{a}, \hat{a}] = \hat{a}^\dagger[\hat{a}, \hat{a}] + [\hat{a}^\dagger, \hat{a}]\hat{a} = 0 - \hat{a} = -\hat{a}$

$[\hat{N}, \hat{a}^\dagger] = [\hat{a}^\dagger\hat{a}, \hat{a}^\dagger] = \hat{a}^\dagger[\hat{a}, \hat{a}^\dagger] + [\hat{a}^\dagger, \hat{a}^\dagger]\hat{a} = \hat{a}^\dagger(1) + 0 = \hat{a}^\dagger$

假设 $|n\rangle$ 是 $\hat{N}$ 的一个归一化本征矢，其[本征值](@entry_id:154894)为 $n$，即 $\hat{N}|n\rangle = n|n\rangle$。我们来考察 $\hat{a}|n\rangle$ 和 $\hat{a}^\dagger|n\rangle$ 这两个新态。

$\hat{N}(\hat{a}|n\rangle) = ([\hat{N}, \hat{a}] + \hat{a}\hat{N})|n\rangle = (-\hat{a} + \hat{a}n)|n\rangle = (n-1)(\hat{a}|n\rangle)$

$\hat{N}(\hat{a}^\dagger|n\rangle) = ([\hat{N}, \hat{a}^\dagger] + \hat{a}^\dagger\hat{N})|n\rangle = (\hat{a}^\dagger + \hat{a}^\dagger n)|n\rangle = (n+1)(\hat{a}^\dagger|n\rangle)$

这表明，如果 $\hat{a}|n\rangle$ 和 $\hat{a}^\dagger|n\rangle$ 不是[零矢量](@entry_id:155273)，那么它们分别是 $\hat{N}$ 的[本征值](@entry_id:154894)为 $n-1$ 和 $n+1$ 的本征矢。因此，$\hat{a}$ 和 $\hat{a}^\dagger$ 的作用是在一个由整数间隔的[本征值](@entry_id:154894)组成的“阶梯”上降低或升高一个态。这正是它们被称为 **[升降算符](@entry_id:197899) (ladder operators)** 的原因。

物理上，任何系统的[哈密顿量](@entry_id:172864)都必须有能量下界。由于 $\hat{H}$ 与 $\hat{N}$ 是线性关系，$\hat{N}$ 的谱也必须有下界。我们考察任意态 $|\psi\rangle$ 中 $\hat{N}$ 的[期望值](@entry_id:153208)：

$\langle\psi|\hat{N}|\psi\rangle = \langle\psi|\hat{a}^\dagger\hat{a}|\psi\rangle = \langle\hat{a}\psi|\hat{a}\psi\rangle = \|\hat{a}|\psi\rangle\|^2 \ge 0$

由于希尔伯特空间中任何矢量的范数平方都是非负的，所以 $\hat{N}$ 的[期望值](@entry_id:153208)总是非负的。对于[本征态](@entry_id:149904) $|n\rangle$，这意味着 $n = \langle n|\hat{N}|n\rangle \ge 0$。因此，$\hat{N}$ 的所有[本征值](@entry_id:154894)必须是非负的。

这个下界的存在意味着，通过反复应用降低算符 $\hat{a}$ 所产生的[本征值](@entry_id:154894)阶梯必须在某处终止。否则，我们可以得到任意小的、甚至是负的[本征值](@entry_id:154894)，这与 $n \ge 0$ 的结论相矛盾。终止的条件是存在一个最低的态，即 **[基态](@entry_id:150928) (ground state)**，我们记为 $|0\rangle$，它被湮灭算符 $\hat{a}$ 化为[零矢量](@entry_id:155273)：

$\hat{a}|0\rangle = 0$

这个态的[本征值](@entry_id:154894) $n_0$ 可以通过 $\hat{N}$ 的作用得到：

$\hat{N}|0\rangle = \hat{a}^\dagger\hat{a}|0\rangle = \hat{a}^\dagger(0) = 0$

因此，[基态](@entry_id:150928)的能量[量子数](@entry_id:145558)是 $0$。

所有其他的[本征态](@entry_id:149904)，即 **[激发态](@entry_id:261453) (excited states)**，都可以通过对[基态](@entry_id:150928)反复应用[产生算符](@entry_id:191512) $\hat{a}^\dagger$ 来构建：

$|1\rangle \propto \hat{a}^\dagger|0\rangle$ ([本征值](@entry_id:154894)为 1)
$|2\rangle \propto (\hat{a}^\dagger)^2|0\rangle$ ([本征值](@entry_id:154894)为 2)
...
$|n\rangle \propto (\hat{a}^\dagger)^n|0\rangle$ ([本征值](@entry_id:154894)为 n)

因此，数量算符 $\hat{N}$ 的谱就是所有非负整数：$\{0, 1, 2, ...\}$。相应地，量子谐振子的能量谱是分立的，其[能量本征值](@entry_id:144381) $E_n$ 为：

$E_n = \hbar\omega(n + \frac{1}{2}), \quad n = 0, 1, 2, ...$

这个结果是量子力学的核心成果之一。它揭示了[谐振子](@entry_id:155622)的能量是量子化的，只能取一系列离散值。最低的能量并非零，而是 $E_0 = \frac{1}{2}\hbar\omega$，这被称为 **零点能 (zero-point energy)**。[零点能](@entry_id:142176)的存在是海森堡不确定性原理的直接体现。假设一个能量为零的态 $|\psi\rangle$ 存在，即 $H|\psi\rangle = 0$，这将导致 $\hat{N}|\psi\rangle = -\frac{1}{2}|\psi\rangle$。然而，这会推导出矛盾 $\langle\psi|\hat{N}|\psi\rangle = \|\hat{a}|\psi\rangle\|^2 = -\frac{1}{2}\langle\psi|\psi\rangle  0$，这在数学上是不可能的 [@problem_id:2112608]。因此，任何束缚在[谐振子势](@entry_id:750179)阱中的粒子都不能静止，必须保持最小的[振动能](@entry_id:157909)量。

归一化的能量本征态 $|n\rangle$（也称为 **[福克态](@entry_id:155105) (Fock states)** 或数量态）可以通过以下方式构建：

$|n\rangle = \frac{1}{\sqrt{n!}}(\hat{a}^\dagger)^n|0\rangle$

对于这些归一化的态，[升降算符](@entry_id:197899)的作用为 [@problem_id:2112618]：

$\hat{a}|n\rangle = \sqrt{n}|n-1\rangle$

$\hat{a}^\dagger|n\rangle = \sqrt{n+1}|n+1\rangle$

这些关系解释了算符名称的物理意义：$\hat{a}^\dagger$ 从真空或较低能级“产生”一个能量量子，将系统提升到下一个能级；而 $\hat{a}$ 则“湮灭”一个能量量子，使系统下降一个能级。

### 定态的性质

#### 宇称

除了能量，量子谐振子的定态还具有明确的对称性。[哈密顿算符](@entry_id:144286)中的[势能](@entry_id:748988)项 $V(x) = \frac{1}{2}m\omega^2x^2$ 是一个关于坐标原点偶对称的函数，即 $V(-x) = V(x)$。动能项中的[二阶导数](@entry_id:144508) $\frac{d^2}{dx^2}$ 也不受 $x \to -x$ 变换的影响。因此，整个[哈密顿算符](@entry_id:144286)与 **[宇称算符](@entry_id:148434)** $\hat{\Pi}$（其作用为 $\hat{\Pi} \psi(x) = \psi(-x)$）是对易的，即 $[\hat{H}, \hat{\Pi}] = 0$。

一个基本定理指出，如果两个算符对易，它们就存在共同的本征函数。对于一维束缚态问题，能谱是非简并的。这意味着对于每个[能量本征值](@entry_id:144381) $E_n$，只存在一个（在相因子意义下）唯一的本征函数 $\psi_n(x)$。由于 $\hat{H}\psi_n(x) = E_n\psi_n(x)$，那么 $\hat{H}\psi_n(-x) = E_n\psi_n(-x)$ 也成立。因为非简并性，$\psi_n(-x)$ 必须与 $\psi_n(x)$ [线性相关](@entry_id:185830)，即 $\psi_n(-x) = c\psi_n(x)$。应用两次宇称操作可知 $c^2=1$，因此 $c=\pm 1$。

这证明了量子谐振子的所有能量本征态都具有确定的宇称：它们要么是[偶函数](@entry_id:163605)（宇称+1），要么是奇函数（宇称-1）。具体而言，[基态](@entry_id:150928) $(n=0)$ 是一个无节点的函数，必须是[偶函数](@entry_id:163605)。第一[激发态](@entry_id:261453) $(n=1)$ 有一个节点，该节点必须在原点，因此是[奇函数](@entry_id:173259)。可以推广得出，第 $n$ 个本征态的宇称是 $(-1)^n$ [@problem_id:2820608]。

#### [不确定性关系](@entry_id:186128)

利用[升降算符](@entry_id:197899)，我们可以方便地计算坐标和动量的[期望值](@entry_id:153208)和不确定度。对于任意[能量本征态](@entry_id:152154) $|n\rangle$：

$\langle n|\hat{x}|n\rangle = \sqrt{\frac{\hbar}{2m\omega}}\langle n|(\hat{a} + \hat{a}^\dagger)|n\rangle = 0$
$\langle n|\hat{p}|n\rangle = i\sqrt{\frac{\hbar m\omega}{2}}\langle n|(\hat{a}^\dagger - \hat{a})|n\rangle = 0$

这是因为 $\hat{a}$ 和 $\hat{a}^\dagger$ 总是将 $|n\rangle$ 变为与之正交的态。

对于[基态](@entry_id:150928) $|0\rangle$，我们可以计算 $\langle\hat{x}^2\rangle$ 和 $\langle\hat{p}^2\rangle$：

$\langle 0|\hat{x}^2|0\rangle = \frac{\hbar}{2m\omega}\langle 0|(\hat{a} + \hat{a}^\dagger)^2|0\rangle = \frac{\hbar}{2m\omega}\langle 0|(\hat{a}\hat{a}^\dagger)|0\rangle = \frac{\hbar}{2m\omega}\langle 0|1|0\rangle = \frac{\hbar}{2m\omega}$

$\langle 0|\hat{p}^2|0\rangle = -\frac{\hbar m\omega}{2}\langle 0|(\hat{a}^\dagger - \hat{a})^2|0\rangle = -\frac{\hbar m\omega}{2}\langle 0|(-\hat{a}^\dagger\hat{a})|0\rangle = \frac{\hbar m\omega}{2}\langle 0|1|0\rangle = \frac{\hbar m\omega}{2}$

因此，[基态](@entry_id:150928)的不确定度为：

$\Delta x_0 = \sqrt{\langle 0|\hat{x}^2|0\rangle - \langle 0|\hat{x}|0\rangle^2} = \sqrt{\frac{\hbar}{2m\omega}}$

$\Delta p_0 = \sqrt{\langle 0|\hat{p}^2|0\rangle - \langle 0|\hat{p}|0\rangle^2} = \sqrt{\frac{\hbar m\omega}{2}}$

其不确定度乘积为：

$\Delta x_0 \Delta p_0 = \sqrt{\frac{\hbar}{2m\omega}} \sqrt{\frac{\hbar m\omega}{2}} = \frac{\hbar}{2}$

这个结果达到了海森堡不确定性原理 $\Delta x \Delta p \ge \frac{\hbar}{2}$ 的下限。因此，[量子谐振子](@entry_id:140678)的[基态](@entry_id:150928)是一个 **最小不确定度态**。

对于一个叠加态，例如 $|\psi\rangle = \frac{1}{\sqrt{3}}|0\rangle + \sqrt{\frac{2}{3}}|1\rangle$，我们可以用同样的方法计算不确定度乘积，结果会严格大于 $\frac{\hbar}{2}$ [@problem_id:2112632]。这表明[激发态](@entry_id:261453)和它们的叠加态通常具有比[基态](@entry_id:150928)更大的不确定性。

### 超越[定态](@entry_id:137260)：相干态与相空间

[福克态](@entry_id:155105) $|n\rangle$ 是量子化的[能量本征态](@entry_id:152154)，它们在某些方面表现出强烈的非经典行为（例如，位置和动量的[期望值](@entry_id:153208)始终为零）。然而，在许多应用中，尤其是在描述[激光](@entry_id:194225)场或分子的宏观[振动](@entry_id:267781)时，我们需要一种更接近经典描述的[量子态](@entry_id:146142)。

#### [相干态](@entry_id:154533)

**[相干态](@entry_id:154533) (coherent states)** $|\alpha\rangle$ 正是这样一类态。它们有几个等价的定义，其中之一是作为湮灭算符 $\hat{a}$ 的本征态，其[本征值](@entry_id:154894)为一个复数 $\alpha \in \mathbb{C}$ [@problem_id:2820537]：

$\hat{a}|\alpha\rangle = \alpha|\alpha\rangle$

由于 $\hat{a}$ 不是厄米算符，其[本征值](@entry_id:154894) $\alpha$ 可以是复数，且不同[本征值](@entry_id:154894)对应的本征矢通常不是正交的。

相干态可以通过对真空态 $|0\rangle$ 应用一个特定的酉算符——**位移算符 $D(\alpha)$**——来构造：

$|\alpha\rangle = D(\alpha)|0\rangle$,  其中 $D(\alpha) = \exp(\alpha\hat{a}^\dagger - \alpha^*\hat{a})$

这个算符的作用是将真空态在相空间中“位移”到一个由复数 $\alpha$ 所指定的位置。利用 Baker-Campbell-Hausdorff (BCH) 公式，我们可以将位移算符分解，并得到[相干态](@entry_id:154533)在[福克态](@entry_id:155105)[基矢](@entry_id:199546)下的展开式：

$|\alpha\rangle = \exp(-\frac{1}{2}|\alpha|^2) \sum_{n=0}^{\infty} \frac{\alpha^n}{\sqrt{n!}}|n\rangle$

这个表达式表明，相干态是无限个数量[态的叠加](@entry_id:273993)。找到粒子处于能级 $n$ 的概率 $P(n) = |\langle n|\alpha\rangle|^2$ 是一个泊松分布：

$P(n) = \exp(-|\alpha|^2) \frac{(|\alpha|^2)^n}{n!}$

其平均能量量子数 $\langle\hat{N}\rangle = |\alpha|^2$。当 $\langle\hat{N}\rangle \gg 1$ 时，相干态的行为非常接近于[经典谐振子](@entry_id:153404)。例如，在相干态 $|\alpha\rangle$ 中，坐标和动量的[期望值](@entry_id:153208)随时间演化，其轨迹与[经典谐振子](@entry_id:153404)的运动完全一致。

#### [维格纳函数](@entry_id:153092)

为了更直观地理解[量子态](@entry_id:146142)与经典描述的联系，我们可以使用 **[维格纳函数](@entry_id:153092) (Wigner function)** $W(x,p)$，它是一个在[经典相空间](@entry_id:195767) $(x,p)$ 中定义的[准概率分布](@entry_id:203668)。对于一个由[波函数](@entry_id:147440) $\psi(x)$ 描述的纯态，[维格纳函数](@entry_id:153092)定义为 [@problem_id:2820547]：

$W(x,p) = \frac{1}{\pi\hbar} \int_{-\infty}^{\infty} dy \, \psi^*(x+y) \psi(x-y) \exp\left(\frac{2ipy}{\hbar}\right)$

[维格纳函数](@entry_id:153092)是实值的，但可能取负值，因此被称为“准”[概率分布](@entry_id:146404)。

对于[量子谐振子](@entry_id:140678)的[基态](@entry_id:150928) $|0\rangle$，其[维格纳函数](@entry_id:153092)是一个以相空间原点为中心的二维高斯函数：

$W_0(x,p) = \frac{1}{\pi\hbar} \exp\left(-\frac{m\omega}{\hbar} x^2 - \frac{p^2}{m\omega\hbar}\right)$

这个[分布](@entry_id:182848)清晰地展示了[基态](@entry_id:150928)在相空间中的不确定性：粒子最可能在原点附近被找到，且动量也接近于零，但两者都存在一个由 $\hbar$ 决定的扩展范围。

对于一个相干态 $|\alpha\rangle$，其经典对应物是在相空间中以 $(x_0, p_0)$ 为中心的[振子](@entry_id:271549)。我们可以将复数 $\alpha$ 与经典振幅和相位联系起来，即 $x_0 = \sqrt{\frac{2\hbar}{m\omega}}\text{Re}(\alpha)$ 和 $p_0 = \sqrt{2\hbar m\omega}\text{Im}(\alpha)$。计算该[相干态](@entry_id:154533)的[维格纳函数](@entry_id:153092)，我们得到 [@problem_id:2820547]：

$W_{\alpha}(x,p) = \frac{1}{\pi\hbar} \exp\left(-\frac{m\omega}{\hbar}(x-x_0)^2 - \frac{(p-p_0)^2}{m\omega\hbar}\right)$

这个结果非常优雅：相干态的[维格纳函数](@entry_id:153092)仅仅是[基态](@entry_id:150928)的[维格纳函数](@entry_id:153092)在相空间中平移到经典轨迹点 $(x_0, p_0)$ 的结果。它是一个与[基态](@entry_id:150928)形状相同的最小不确定度[高斯波包](@entry_id:151158)，其中心随时间演化，完美地描绘了一个经典的[振荡](@entry_id:267781)轨迹。这为我们将相干态视为最经典的[量子态](@entry_id:146142)提供了有力的图像。