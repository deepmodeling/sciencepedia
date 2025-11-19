## 引言
[量子谐振子](@entry_id:140678)是量子力学中少数几个可以精确求解，却又具有极其广泛物理应用的基石模型。从[分子振动](@entry_id:140827)到[晶格振动](@entry_id:140970)，再到[电磁场的量子化](@entry_id:155376)，谐振子的概念无处不在。然而，直接求解其对应的定态薛定谔方程，一个[二阶常微分方程](@entry_id:204212)，虽然可行，但过程较为繁琐，且难以直观地揭示系统内在的[代数结构](@entry_id:137052)。本文旨在介绍一种更为深刻且优雅的求解方法——[升降算符](@entry_id:197899)（或称[阶梯算符](@entry_id:199991)）的代数方法，它不仅简化了计算，更提供了一种理解量子化和[粒子统计](@entry_id:145640)的全新视角。

本文将引导读者系统地掌握这一强大工具。在“**原理与机制**”一章中，我们将从位置和[动量算符](@entry_id:151743)出发，定义创生与[湮灭算符](@entry_id:165390)，推导它们的核心[对易关系](@entry_id:136780)，并展示如何利用它们重构[哈密顿量](@entry_id:172864)，从而轻松地得到整个[能谱](@entry_id:181780)和对应的本征态。接着，在“**应用与跨学科联系**”一章中，我们将探讨该方法的实际应用，展示如何计算物理可观测量、解释分子[光谱](@entry_id:185632)的[选择定则](@entry_id:140784)，并一窥其在凝聚态物理和量子光学等前沿领域的深刻影响。最后，“**动手实践**”部分提供了一系列练习，帮助读者将理论知识转化为解决具体问题的能力。通过这一结构化的学习路径，你将深刻理解为何[升降算符](@entry_id:197899)是现代物理学工具箱中不可或缺的一部分。

## 原理与机制

在处理量子谐振子问题时，求解含[二阶导数](@entry_id:144508)的薛定谔方程是一种直接但较为繁琐的方法。一种更优雅且深刻的途径是代数方法，它利用所谓的**[升降算符](@entry_id:197899)**（ladder operators）来揭示系统的内在结构。本章将详细阐述这些算符的定义、性质及其在确定量子谐振子能谱和计算[物理可观测量](@entry_id:154692)方面的核心作用。

### 从位置和动量到[阶梯算符](@entry_id:199991)

对于质量为 $m$、[角频率](@entry_id:261565)为 $\omega$ 的一维谐振子，其位置算符 $\hat{x}$ 和[动量算符](@entry_id:151743) $\hat{p}$ 是系统的基本动力学变量。[升降算符](@entry_id:197899)正是通过这两个算符来定义的。我们引入两个算符，分别称为**[湮灭算符](@entry_id:165390)**（annihilation operator）$\hat{a}$ 和**创生算符**（creation operator）$\hat{a}^\dagger$：

$$ \hat{a} = \sqrt{\frac{m\omega}{2\hbar}}\left(\hat{x} + \frac{i}{m\omega}\hat{p}\right) $$
$$ \hat{a}^\dagger = \sqrt{\frac{m\omega}{2\hbar}}\left(\hat{x} - \frac{i}{m\omega}\hat{p}\right) $$

其中 $\hbar$ 是约化普朗克常数。从定义可以看出，$\hat{a}$ 和 $\hat{a}^\dagger$ 互为[厄米共轭](@entry_id:191215)。这是因为 $\hat{x}$ 和 $\hat{p}$ 都是厄米算符（$\hat{x}^\dagger = \hat{x}, \hat{p}^\dagger = \hat{p}$），而常数因子是实数，虚数单位 $i$ 的共轭是 $-i$。

值得注意的是，湮灭算符 $\hat{a}$ 本身并非厄米算符。任何非厄米算符都可以分解为其厄米和反厄米部分，类似于将复数分解为实部和虚部。对于算符 $\hat{a}$，我们可以定义其厄米部分 $\hat{X}$ 和 $\hat{Y}$ 如下：
$$ \hat{a} = \hat{X} + i\hat{Y} $$
其中 $\hat{X} = \frac{1}{2}(\hat{a} + \hat{a}^\dagger)$ 和 $\hat{Y} = \frac{1}{2i}(\hat{a} - \hat{a}^\dagger)$。将 $\hat{a}$ 和 $\hat{a}^\dagger$ 的定义代入，我们发现这两个部分与位置和动量算符直接相关 [@problem_id:1377478]：
$$ \hat{X} = \frac{1}{2} \left( \sqrt{\frac{m\omega}{2\hbar}}\left(\hat{x} + \frac{i}{m\omega}\hat{p}\right) + \sqrt{\frac{m\omega}{2\hbar}}\left(\hat{x} - \frac{i}{m\omega}\hat{p}\right) \right) = \sqrt{\frac{m\omega}{2\hbar}}\hat{x} $$
$$ \hat{Y} = \frac{1}{2i} \left( \sqrt{\frac{m\omega}{2\hbar}}\left(\hat{x} + \frac{i}{m\omega}\hat{p}\right) - \sqrt{\frac{m\omega}{2\hbar}}\left(\hat{x} - \frac{i}{m\omega}\hat{p}\right) \right) = \sqrt{\frac{m\omega}{2\hbar}}\frac{\hat{p}}{m\omega} $$

这些算符代数的核心在于它们的对易关系。利用位置和动量的基本对易关系 $[\hat{x}, \hat{p}] = i\hbar$，我们可以推导出 $\hat{a}$ 和 $\hat{a}^\dagger$ 之间的[对易关系](@entry_id:136780)：
$$ [\hat{a}, \hat{a}^\dagger] = \hat{a}\hat{a}^\dagger - \hat{a}^\dagger\hat{a} $$
$$ = \frac{m\omega}{2\hbar} \left[ \left(\hat{x} + \frac{i}{m\omega}\hat{p}\right), \left(\hat{x} - \frac{i}{m\omega}\hat{p}\right) \right] $$
$$ = \frac{m\omega}{2\hbar} \left( [\hat{x}, \hat{x}] - \frac{i}{m\omega}[\hat{x}, \hat{p}] + \frac{i}{m\omega}[\hat{p}, \hat{x}] - \left(\frac{i}{m\omega}\right)^2[\hat{p}, \hat{p}] \right) $$
由于 $[\hat{x}, \hat{x}]=0$, $[\hat{p}, \hat{p}]=0$ 且 $[\hat{p}, \hat{x}] = -[\hat{x}, \hat{p}] = -i\hbar$，上式简化为：
$$ [\hat{a}, \hat{a}^\dagger] = \frac{m\omega}{2\hbar} \left( - \frac{i}{m\omega}(i\hbar) + \frac{i}{m\omega}(-i\hbar) \right) = \frac{m\omega}{2\hbar} \left( \frac{\hbar}{m\omega} + \frac{\hbar}{m\omega} \right) = 1 $$
这个极其简洁的**[正则对易关系](@entry_id:185041)**（canonical commutation relation），$[\hat{a}, \hat{a}^\dagger] = 1$，是整个代数方法的基础，它不依赖于 $m$ 或 $\omega$，体现了深刻的普遍性。

### 数算符与态的量子化

利用[升降算符](@entry_id:197899)，我们可以重新表达谐振子的[哈密顿算符](@entry_id:144286) $\hat{H} = \frac{\hat{p}^2}{2m} + \frac{1}{2}m\omega^2\hat{x}^2$。首先，我们将 $\hat{x}$ 和 $\hat{p}$ 用 $\hat{a}$ 和 $\hat{a}^\dagger$ 表示：
$$ \hat{x} = \sqrt{\frac{\hbar}{2m\omega}}(\hat{a} + \hat{a}^\dagger) $$
$$ \hat{p} = i\sqrt{\frac{m\omega\hbar}{2}}(\hat{a}^\dagger - \hat{a}) $$
将这些表达式代入[哈密顿算符](@entry_id:144286)并利用 $[\hat{a}, \hat{a}^\dagger] = 1$，经过一番代数运算，可得一个极为优美的形式：
$$ \hat{H} = \hbar\omega \left(\hat{a}^\dagger\hat{a} + \frac{1}{2}\right) $$
这个形式的[哈密顿算符](@entry_id:144286)启发我们定义一个核心算符——**数算符**（number operator）$\hat{N}$：
$$ \hat{N} = \hat{a}^\dagger\hat{a} $$
于是[哈密顿算符](@entry_id:144286)变为 $\hat{H} = \hbar\omega (\hat{N} + \frac{1}{2})$。这意味着 $\hat{H}$ 和 $\hat{N}$ 的[本征态](@entry_id:149904)是相同的。如果我们找到 $\hat{N}$ 的本征态 $|n\rangle$ 及其[本征值](@entry_id:154894) $n$，即 $\hat{N}|n\rangle = n|n\rangle$，那么该态也是能量本征态，其能量为 $E_n = \hbar\omega(n + \frac{1}{2})$。

数算符的[本征值](@entry_id:154894) $n$ 必须是非负的。这个结论源于[希尔伯特空间](@entry_id:261193)[内积](@entry_id:158127)的基本性质。对于任意一个归一化的[量子态](@entry_id:146142) $|\psi\rangle$，数算符的[期望值](@entry_id:153208)可以写为：
$$ \langle\psi|\hat{N}|\psi\rangle = \langle\psi|\hat{a}^\dagger\hat{a}|\psi\rangle $$
根据[厄米共轭](@entry_id:191215)的定义，这等价于：
$$ \langle\hat{a}\psi|\hat{a}\psi\rangle = ||\hat{a}|\psi\rangle||^2 $$
这是一个态矢量 $\hat{a}|\psi\rangle$ 的模方。在希尔伯特空间中，任何矢量的模方都必须是非负的，即 $||\hat{a}|\psi\rangle||^2 \ge 0$。因此，$\langle\psi|\hat{N}|\psi\rangle \ge 0$。对于 $\hat{N}$ 的一个本征态 $|n\rangle$，其[期望值](@entry_id:153208)为 $\langle n|\hat{N}|n\rangle = \langle n|n|n\rangle = n\langle n|n\rangle = n$。结合这两个结果，我们得出结论：数算符的任何[本征值](@entry_id:154894) $n$ 都必须满足 $n \ge 0$。这从根本上排除了具有负量子数的物理态，如 $|-1\rangle$ [@problem_id:1377504]。

### 能量本征态的阶梯

创生和湮灭算符的名称源于它们对能量本征态的作用。为了探究这一点，我们计算它们与[哈密顿算符](@entry_id:144286)的对易子 [@problem_id:2120052]：
$$ [\hat{H}, \hat{a}] = [\hbar\omega (\hat{a}^\dagger\hat{a} + \frac{1}{2}), \hat{a}] = \hbar\omega[\hat{a}^\dagger\hat{a}, \hat{a}] = \hbar\omega(\hat{a}^\dagger[\hat{a}, \hat{a}] + [\hat{a}^\dagger, \hat{a}]\hat{a}) = \hbar\omega(0 - 1 \cdot \hat{a}) = -\hbar\omega\hat{a} $$
$$ [\hat{H}, \hat{a}^\dagger] = [\hbar\omega (\hat{a}^\dagger\hat{a} + \frac{1}{2}), \hat{a}^\dagger] = \hbar\omega[\hat{a}^\dagger\hat{a}, \hat{a}^\dagger] = \hbar\omega(\hat{a}^\dagger[\hat{a}, \hat{a}^\dagger] + [\hat{a}^\dagger, \hat{a}^\dagger]\hat{a}) = \hbar\omega(\hat{a}^\dagger \cdot 1 + 0) = \hbar\omega\hat{a}^\dagger $$
这两个关系式 $\hat{H}\hat{a} = \hat{a}(\hat{H} - \hbar\omega)$ 和 $\hat{H}\hat{a}^\dagger = \hat{a}^\dagger(\hat{H} + \hbar\omega)$ 是理解能谱结构的关键。

假设 $|E\rangle$ 是一个能量为 $E$ 的本征态，即 $\hat{H}|E\rangle = E|E\rangle$。现在我们将 $\hat{H}$ 作用在 $\hat{a}|E\rangle$ 上：
$$ \hat{H}(\hat{a}|E\rangle) = \hat{a}(\hat{H} - \hbar\omega)|E\rangle = \hat{a}(E - \hbar\omega)|E\rangle = (E - \hbar\omega)(\hat{a}|E\rangle) $$
这表明，如果 $\hat{a}|E\rangle$ 不是[零矢量](@entry_id:155273)，它就是哈密顿的一个新本征态，其能量为 $E - \hbar\omega$。因此，$\hat{a}$ 将一个能量本征态“湮灭”为一个能量更低的态，能量恰好减少了一个量子 $\hbar\omega$。

同理，对于 $\hat{a}^\dagger|E\rangle$：
$$ \hat{H}(\hat{a}^\dagger|E\rangle) = \hat{a}^\dagger(\hat{H} + \hbar\omega)|E\rangle = \hat{a}^\dagger(E + \hbar\omega)|E\rangle = (E + \hbar\omega)(\hat{a}^\dagger|E\rangle) $$
$\hat{a}^\dagger$ 将能量本征态“创生”为一个能量更高的态，能量增加了 $\hbar\omega$。

这种性质解释了为何它们被称为**[阶梯算符](@entry_id:199991)**：$\hat{a}$ 扮演着**降算符**（lowering operator）的角色，使系统在等间距的能量“阶梯”上向下移动一步；而 $\hat{a}^\dagger$ 是**升算符**（raising operator），使系统向上移动一步。这直接证明了量子谐振子的能级是等距[分布](@entry_id:182848)的，间距为 $\hbar\omega$ [@problem_id:2120052]。

### 构建谐振子[能谱](@entry_id:181780)

既然能量阶梯是存在的，它必须有一个最低的“梯级”，否则能量可以无限降低，系统将是不稳定的。这个最低能量态，即**[基态](@entry_id:150928)**（ground state），记为 $|0\rangle$。根据定义，[基态](@entry_id:150928)不能再被降低，这意味着湮灭算符作用于其上必须得到[零矢量](@entry_id:155273)：
$$ \hat{a}|0\rangle = 0 $$
这个条件是定义[基态](@entry_id:150928)的核心。利用这个条件，我们可以立即计算出基态能量，即**[零点能](@entry_id:142176)**（zero-point energy）[@problem_id:1377461]。将[哈密顿算符](@entry_id:144286)作用于 $|0\rangle$：
$$ \hat{H}|0\rangle = \hbar\omega \left(\hat{a}^\dagger\hat{a} + \frac{1}{2}\right)|0\rangle = \hbar\omega (\hat{a}^\dagger(\hat{a}|0\rangle) + \frac{1}{2}|0\rangle) = \hbar\omega(0 + \frac{1}{2}|0\rangle) = \frac{1}{2}\hbar\omega |0\rangle $$
因此，基态能量为 $E_0 = \frac{1}{2}\hbar\omega$。同时，我们也可以确认[基态](@entry_id:150928)是数算符[本征值](@entry_id:154894)为0的态：$\hat{N}|0\rangle = \hat{a}^\dagger\hat{a}|0\rangle = 0$。

从[基态](@entry_id:150928)出发，我们可以通过重复应用创生算符 $\hat{a}^\dagger$ 来构建整个能谱。第一[激发态](@entry_id:261453) $|1\rangle$ 是通过将 $\hat{a}^\dagger$ 作用于 $|0\rangle$ 得到的，其能量为 $E_1 = E_0 + \hbar\omega = \frac{3}{2}\hbar\omega$。第 $n$ 个[激发态](@entry_id:261453) $|n\rangle$ 是通过将 $\hat{a}^\dagger$ 连续作用 $n$ 次于 $|0\rangle$ 构建的，其能量为 $E_n = (n + \frac{1}{2})\hbar\omega$。

为了得到归一化的本征态，我们需要确定算符作用后的系数。我们已知 $\hat{N}|n\rangle = n|n\rangle$。考虑态 $\hat{a}^\dagger|n\rangle$ 的模方：
$$ ||\hat{a}^\dagger|n\rangle||^2 = \langle n|\hat{a}\hat{a}^\dagger|n\rangle $$
利用[对易关系](@entry_id:136780) $[\hat{a}, \hat{a}^\dagger]=1 \implies \hat{a}\hat{a}^\dagger = \hat{a}^\dagger\hat{a} + 1 = \hat{N} + 1$，我们得到：
$$ \langle n|\hat{N}+1|n\rangle = (n+1)\langle n|n\rangle = n+1 $$
因此，$\hat{a}^\dagger|n\rangle$ 的模是 $\sqrt{n+1}$。这意味着，如果 $|n\rangle$ 是归一化的，那么归一化的 $|n+1\rangle$ 态与 $\hat{a}^\dagger|n\rangle$ 的关系是：
$$ \hat{a}^\dagger|n\rangle = \sqrt{n+1}|n+1\rangle $$
类似地，可以推导出湮灭算符的作用：
$$ \hat{a}|n\rangle = \sqrt{n}|n-1\rangle $$
这些关系式是进行具体计算的基础。例如，它们表明 $|n\rangle$ 不仅是 $\hat{N}$ 的本征态，也是算符 $\hat{a}\hat{a}^\dagger$ 的本征态，其[本征值](@entry_id:154894)为 $n+1$ [@problem_id:1377479]，并且是任何形如 $c_1\hat{a}^\dagger\hat{a} + c_2\hat{a}\hat{a}^\dagger$ 的算符的本征态，[本征值](@entry_id:154894)为 $c_1n + c_2(n+1)$ [@problem_id:1377463]。

利用这些关系，我们可以从归一化的[基态](@entry_id:150928) $|0\rangle$ 生成任意归一化的[激发态](@entry_id:261453) $|n\rangle$ [@problem_id:1377509]：
$$ |1\rangle = \frac{1}{\sqrt{1}}\hat{a}^\dagger|0\rangle $$
$$ |2\rangle = \frac{1}{\sqrt{2}}\hat{a}^\dagger|1\rangle = \frac{1}{\sqrt{2}\sqrt{1}}(\hat{a}^\dagger)^2|0\rangle $$
以此类推，可以得到一般公式：
$$ |n\rangle = \frac{1}{\sqrt{n!}}(\hat{a}^\dagger)^n|0\rangle $$
这表明，整个谐振子的希尔伯特空间可以由[基态](@entry_id:150928)和创生算符完全构建出来。

最后，代数方法还可以与位置表象（[波函数](@entry_id:147440)）联系起来。[基态](@entry_id:150928)条件 $\hat{a}|0\rangle=0$ 在位置表象中变为一个关于[基态](@entry_id:150928)[波函数](@entry_id:147440) $\psi_0(x) = \langle x|0\rangle$ 的[一阶微分方程](@entry_id:173139) [@problem_id:1377517]。将 $\hat{x} \to x$ 和 $\hat{p} \to -i\hbar\frac{d}{dx}$ 代入 $\hat{a}$ 的定义：
$$ \sqrt{\frac{m\omega}{2\hbar}}\left(x + \frac{i}{m\omega}(-i\hbar\frac{d}{dx})\right)\psi_0(x) = 0 $$
$$ \left(x + \frac{\hbar}{m\omega}\frac{d}{dx}\right)\psi_0(x) = 0 $$
整理可得：
$$ \frac{d\psi_0(x)}{dx} = -\frac{m\omega}{\hbar}x \cdot \psi_0(x) $$
这是一个变量可分离的[微分方程](@entry_id:264184)，其解是一个高斯函数，这正是我们通过求解薛定谔方程所得到的[基态](@entry_id:150928)[波函数](@entry_id:147440)。

### 在计算[可观测量](@entry_id:267133)中的应用

[升降算符](@entry_id:197899)方法的最大优势在于计算可观量的矩阵元和[期望值](@entry_id:153208)。由于物理算符（如位置 $\hat{x}$、动量 $\hat{p}$ 及其任意次幂）都可以用 $\hat{a}$ 和 $\hat{a}^\dagger$ 表示，复杂的积分运算就转化为了纯粹的代数运算。

作为一个例子，我们来计算非[对角矩阵](@entry_id:637782)元 $\langle n+1 | \hat{x}^3 | n \rangle$ [@problem_id:1377477]。首先，我们将 $\hat{x}^3$ 表示为[升降算符](@entry_id:197899)的形式：
$$ \hat{x}^3 = \left(\sqrt{\frac{\hbar}{2m\omega}}(\hat{a} + \hat{a}^\dagger)\right)^3 = \left(\frac{\hbar}{2m\omega}\right)^{3/2} (\hat{a} + \hat{a}^\dagger)^3 $$
展开 $(\hat{a} + \hat{a}^\dagger)^3$ 会得到8个算符乘积项。然而，在计算 $\langle n+1 | \dots | n \rangle$ 时，我们只需要考虑那些能将[量子数](@entry_id:145558)从 $n$ 变为 $n+1$ 的项。一个 $\hat{a}^\dagger$ 算符使 $n$ 增加1，一个 $\hat{a}$ 算符使 $n$ 减少1。因此，只有那些包含两个 $\hat{a}^\dagger$ 和一个 $\hat{a}$ 的项才能对该矩阵元有非零贡献。这些项是：$\hat{a}(\hat{a}^\dagger)^2$、$\hat{a}^\dagger\hat{a}\hat{a}^\dagger$ 和 $(\hat{a}^\dagger)^2\hat{a}$。我们逐一计算它们的作用：

1.  $\langle n+1 | \hat{a}(\hat{a}^\dagger)^2 | n \rangle$:
    $(\hat{a}^\dagger)^2|n\rangle = \hat{a}^\dagger(\sqrt{n+1}|n+1\rangle) = \sqrt{n+1}\sqrt{n+2}|n+2\rangle$
    $\hat{a}(\hat{a}^\dagger)^2|n\rangle = \sqrt{n+1}\sqrt{n+2}\hat{a}|n+2\rangle = \sqrt{n+1}\sqrt{n+2}\sqrt{n+2}|n+1\rangle = (n+2)\sqrt{n+1}|n+1\rangle$
    所以，$\langle n+1 | \hat{a}(\hat{a}^\dagger)^2 | n \rangle = (n+2)\sqrt{n+1}$。

2.  $\langle n+1 | \hat{a}^\dagger\hat{a}\hat{a}^\dagger | n \rangle$:
    $\hat{a}^\dagger|n\rangle = \sqrt{n+1}|n+1\rangle$
    $\hat{a}\hat{a}^\dagger|n\rangle = \sqrt{n+1}\hat{a}|n+1\rangle = (n+1)|n\rangle$
    $\hat{a}^\dagger\hat{a}\hat{a}^\dagger|n\rangle = (n+1)\hat{a}^\dagger|n\rangle = (n+1)\sqrt{n+1}|n+1\rangle$
    所以，$\langle n+1 | \hat{a}^\dagger\hat{a}\hat{a}^\dagger | n \rangle = (n+1)\sqrt{n+1}$。

3.  $\langle n+1 | (\hat{a}^\dagger)^2\hat{a} | n \rangle$:
    $\hat{a}|n\rangle = \sqrt{n}|n-1\rangle$
    $(\hat{a}^\dagger)^2\hat{a}|n\rangle = \sqrt{n}(\hat{a}^\dagger)^2|n-1\rangle = \sqrt{n}(\sqrt{n}\sqrt{n+1}|n+1\rangle) = n\sqrt{n+1}|n+1\rangle$
    所以，$\langle n+1 | (\hat{a}^\dagger)^2\hat{a} | n \rangle = n\sqrt{n+1}$。

将这三项贡献相加，得到 $\langle n+1 | (\hat{a}+\hat{a}^\dagger)^3 | n \rangle = \sqrt{n+1}((n+2)+(n+1)+n) = 3(n+1)\sqrt{n+1}$。最后，乘上系数，我们得到最终结果：
$$ \langle n+1 | \hat{x}^3 | n \rangle = \left(\frac{\hbar}{2m\omega}\right)^{3/2} \cdot 3(n+1)\sqrt{n+1} $$
这个过程展示了代数方法的威力：它将一个原本需要计算含高斯函数和厄米多项式的复杂积分问题，转化为了遵循简单规则的算符操作。这种方法不仅简化了计算，也为理解选择定则（selection rules）等[光谱学](@entry_id:141940)概念提供了清晰的物理图像。例如，从这个计算中我们看到，$\hat{x}^3$ 算符可以导致 $\Delta n = \pm 1, \pm 3$ 的跃迁。

同样地，计算算符的[期望值](@entry_id:153208)也变得非常直接。例如，对于一个由[升降算符](@entry_id:197899)构成的[厄米算符](@entry_id:153410) $\hat{M} = \hat{G}^\dagger \hat{G}$，其中 $\hat{G} = c_1 \hat{a} + i c_2 \hat{a}^\dagger$（$c_1, c_2$为实常数），其在第一[激发态](@entry_id:261453) $|1\rangle$ 的[期望值](@entry_id:153208) $\langle 1|\hat{M}|1\rangle$ 可以通过代数方法轻松求得 [@problem_id:1377507]。首先展开 $\hat{M}$：
$$ \hat{M} = (c_1 \hat{a}^\dagger - i c_2 \hat{a})(c_1 \hat{a} + i c_2 \hat{a}^\dagger) = c_1^2 \hat{a}^\dagger\hat{a} + c_2^2 \hat{a}\hat{a}^\dagger + i c_1 c_2 (\hat{a}^\dagger\hat{a}^\dagger - \hat{a}\hat{a}) $$
计算[期望值](@entry_id:153208)时，$\langle 1|\hat{a}^\dagger\hat{a}^\dagger|1\rangle$ 和 $\langle 1|\hat{a}\hat{a}|1\rangle$ 由于量子数不匹配而为零。我们只需计算对角项：
$$ \langle 1|\hat{M}|1\rangle = c_1^2 \langle 1|\hat{a}^\dagger\hat{a}|1\rangle + c_2^2 \langle 1|\hat{a}\hat{a}^\dagger|1\rangle $$
由于 $\hat{a}^\dagger\hat{a}|1\rangle = \hat{N}|1\rangle = 1|1\rangle$ 且 $\hat{a}\hat{a}^\dagger|1\rangle = (\hat{N}+1)|1\rangle = 2|1\rangle$，我们得到：
$$ \langle 1|\hat{M}|1\rangle = c_1^2 (1) + c_2^2 (2) = c_1^2 + 2c_2^2 $$
这个结果再次展示了代数方法的简洁与高效。

总之，[升降算符](@entry_id:197899)不仅提供了一种求解量子谐振子问题的强大数学工具，更重要的是，它揭示了[能谱](@entry_id:181780)的内在[代数结构](@entry_id:137052)，为[量子场论](@entry_id:138177)等更高级的理论奠定了基础。