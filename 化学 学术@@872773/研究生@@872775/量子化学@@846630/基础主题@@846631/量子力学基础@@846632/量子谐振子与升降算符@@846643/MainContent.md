## 引言
量子谐振子（Quantum Harmonic Oscillator, QHO）不仅是量子力学中最基本、最重要的[精确可解模型](@entry_id:142243)之一，也是连接理论与实验的桥梁，其应用遍及从化学到物理的多个分支。传统上，我们通过求解定态薛定谔方程来获得其能级和[波函数](@entry_id:147440)，但这往往掩盖了其背后深刻的[代数结构](@entry_id:137052)。本文旨在填补这一认知空白，引导读者超越[微分方程](@entry_id:264184)的视角，深入掌握一种更为优雅且强大的工具——[阶梯算符](@entry_id:199991)代数方法。

通过本文的学习，您将不仅理解[量子谐振子](@entry_id:140678)的基本解，更能领会其形式主义的威力。在“原理与机制”一章中，我们将从[正则对易关系](@entry_id:185041)出发，引入并构建[阶梯算符](@entry_id:199991)，展示如何纯粹通过代数运算推导出完整的[能谱](@entry_id:181780)和[本征态](@entry_id:149904)。接下来，在“应用与跨学科联系”一章中，我们将看到这一模型如何成为解释分子振动[光谱](@entry_id:185632)、分析多原子体系[简正模](@entry_id:139640)、乃至描述量子化光场和光物质相互作用的基石。最后，通过“动手实践”部分的精选问题，您将有机会亲手运用这些算符技巧，解决具体物理问题，从而巩固和深化您的理解。让我们一同开启这场探索之旅，揭示隐藏在谐振子问题背后的数学之美及其在现代科学中的广泛回响。

## 原理与机制

量子谐振子 (Quantum Harmonic Oscillator, QHO) 模型是量子力学中的一个基石。它不仅精确地描述了许多物理系统（如[分子振动](@entry_id:140827)、[晶格振动](@entry_id:140970)或[电磁场的量子化](@entry_id:155376)模式），而且其求解方法本身也引入了量子力学中一些最深刻、最强大的数学工具。在本章中，我们将系统地探讨量子谐振子的基本原理和求解机制，重点关注一种不直接求解薛定谔[微分方程](@entry_id:264184)，而是利用算符代数的方法。

### 从经典到量子的跃迁：[对易关系](@entry_id:136780)的引入

我们从一维[经典谐振子](@entry_id:153404)的[哈密顿量](@entry_id:172864)开始：
$$
H = \frac{p^2}{2m} + \frac{1}{2}m\omega^2x^2
$$
其中 $m$ 是质量，$p$ 是动量，$x$ 是位移，$\omega$ 是[振动](@entry_id:267781)的角频率。从经典力学过渡到量子力学最直接的方法（即所谓的**[正则量子化](@entry_id:148501)**）是将物理量（如 $x$ 和 $p$）提升为在希尔伯特空间上作用的算符 $\hat{x}$ 和 $\hat{p}$。同时，经典力学中的泊松括号 $\{f, g\}$ 被量子力学中的对易子 $[\hat{f}, \hat{g}]$ 所取代，其间的对应关系由狄拉克提出：
$$
\{\cdot, \cdot\} \mapsto \frac{1}{i\hbar}[\cdot, \cdot]
$$
对于[正则坐标](@entry_id:175654) $x$ 和动量 $p$，它们的[泊松括号](@entry_id:151133)为 $\{x, p\} = 1$。将其量子化后，我们得到了量子力学中最基本的关系之一——**[正则对易关系](@entry_id:185041) (Canonical Commutation Relation, CCR)**：
$$
[\hat{x}, \hat{p}] = i\hbar
$$
这个简单的关系背后蕴含着深刻的数学结构。由于位置和动量在物理上可以取任意实数值，它们的算符 $\hat{x}$ 和 $\hat{p}$ 必须是**无界算符 (unbounded operators)**。无界算符不能定义在整个希尔伯特空间上，而只能定义在一个稠密的[子空间](@entry_id:150286)（称为定义域）上。为了保证[量子理论](@entry_id:145435)的物理实在性和唯一性，我们需要更严格的数学条件。具体而言，[物理可观测量](@entry_id:154692)对应的算符必须是**自伴的 (self-adjoint)**，而不仅仅是对称的。根据[斯通定理](@entry_id:262301) (Stone's theorem)，只有自伴算符才能生成一个强连续的[单参数酉群](@entry_id:270459)，这些[酉群](@entry_id:138602)对应着如时间演化、空间平移等基本物理变换。

为了唯一地（在[酉等价](@entry_id:197898)的意义下）确定满足 CCR 的 $\hat{x}$ 和 $\hat{p}$ 算符，我们需要考虑它们的指数形式，即**外尔关系 (Weyl relations)**。斯通-冯·诺依曼定理 (Stone-von Neumann theorem) 保证了，在一个可分的[复希尔伯特空间](@entry_id:185216)上，外尔关系的任何强连续[不可约表示](@entry_id:263310)都[酉等价](@entry_id:197898)于标准的薛定谔表示。这些严格的数学要求确保了[量子谐振子](@entry_id:140678)[哈密顿量](@entry_id:172864)的明确定义和其动力学的唯一性，并为我们接下来将要介绍的代数方法提供了坚实的理论基础 [@problem_id:2918148]。

### 代数方法：[哈密顿量](@entry_id:172864)的[因子分解](@entry_id:150389)

直接求解[量子谐振子](@entry_id:140678)的定态薛定谔方程是一个涉及[二阶常微分方程](@entry_id:204212)的标准问题，其解为厄米多项式。然而，有一种更优雅、更具洞察力的代数方法，它完全避开了求解微分方程的过程。该方法的核心思想是对[哈密顿算符](@entry_id:144286)进行“[因子分解](@entry_id:150389)”。

为了简化代数运算，我们首先引入一组**无量纲算符**。我们定义新的无量纲位置算符 $\hat{X}$ 和动量算符 $\hat{P}$：
$$
\hat{x} = \alpha \hat{X}, \qquad \hat{p} = \beta \hat{P}
$$
其中 $\alpha$ 和 $\beta$ 是具有适当量纲的标度常数。我们的目标是使[哈密顿量](@entry_id:172864)正比于 $\hat{X}^2 + \hat{P}^2$，并且[对易关系](@entry_id:136780)保持最简洁的无量纲形式。
将上述代换带入[哈密顿量](@entry_id:172864)，我们得到：
$$
\hat{H} = \frac{\beta^2}{2m}\hat{P}^2 + \frac{1}{2}m\omega^2\alpha^2\hat{X}^2
$$
为了让 $\hat{P}^2$ 和 $\hat{X}^2$ 的系数相等，我们要求 $\frac{\beta^2}{2m} = \frac{1}{2}m\omega^2\alpha^2$，即 $\beta = m\omega\alpha$。
接下来，我们考察[对易关系](@entry_id:136780)：
$$
[\hat{x}, \hat{p}] = [\alpha \hat{X}, \beta \hat{P}] = \alpha\beta[\hat{X}, \hat{P}] = i\hbar
$$
为了得到最简洁的无量纲[对易关系](@entry_id:136780) $[\hat{X}, \hat{P}] = i$，我们必须要求 $\alpha\beta = \hbar$。联立两个关于 $\alpha$ 和 $\beta$ 的方程，我们解得：
$$
\alpha = \sqrt{\frac{\hbar}{m\omega}}, \qquad \beta = \sqrt{m\hbar\omega}
$$
于是，无量纲算符与原始算符的关系为：
$$
\hat{X} = \sqrt{\frac{m\omega}{\hbar}}\hat{x}, \qquad \hat{P} = \frac{1}{\sqrt{m\hbar\omega}}\hat{p}
$$
此时，[哈密顿量](@entry_id:172864)可以优美地写成 [@problem_id:2918133]：
$$
\hat{H} = \frac{\hbar\omega}{2}(\hat{X}^2 + \hat{P}^2)
$$
这种无量纲化处理将一个依赖于具体系统参数（$m$ 和 $\omega$）的问题，转化为了一个普适的[代数结构](@entry_id:137052)问题，极大地简化了后续分析。

### [阶梯算符](@entry_id:199991)的引入

代数方法的核心飞跃在于引入**[阶梯算符](@entry_id:199991) (ladder operators)**，也称为**产生和[湮灭算符](@entry_id:165390) (creation and annihilation operators)**。它们是无量纲算符 $\hat{X}$ 和 $\hat{P}$ 的线性组合。我们定义**[湮灭算符](@entry_id:165390)** $\hat{a}$ 和**[产生算符](@entry_id:191512)** $\hat{a}^\dagger$ 如下：
$$
\hat{a} = \frac{1}{\sqrt{2}}(\hat{X} + i\hat{P})
$$
$$
\hat{a}^\dagger = \frac{1}{\sqrt{2}}(\hat{X} - i\hat{P})
$$
注意 $\hat{a}^\dagger$ 确实是 $\hat{a}$ 的[厄米共轭](@entry_id:191215)，因为 $\hat{X}$ 和 $\hat{P}$ 都是[厄米算符](@entry_id:153410)。

这里 $\hat{X}$ 和 $\hat{P}$ 之间的[相对相位](@entry_id:148120)因子 $i = \exp(i\pi/2)$ 并非随意选择。这个选择是至关重要的，它确保了 $\hat{a}$ 和 $\hat{a}^\dagger$ 具有最简洁和最强大的代数性质。我们可以从一个更普遍的定义出发来理解这一点，形如 $\hat{a} \propto \hat{X} + \exp(i\phi)\hat{P}$。通过计算 $[\hat{a}, \hat{a}^\dagger]$ 并要求其结果为一个简单的实数（按惯例取 1），可以证明相对相位 $\phi$ 必须是 $\pi/2$。这个相位的符号直接与[正则对易关系](@entry_id:185041) $[\hat{x}, \hat{p}] = +i\hbar$ 中的符号相关联。如果符号相反，所需的相位也会随之改变 [@problem_id:2918094]。

有了上述定义，我们可以直接计算 $\hat{a}$ 和 $\hat{a}^\dagger$ 的对易子：
$$
[\hat{a}, \hat{a}^\dagger] = \frac{1}{2}[ \hat{X} + i\hat{P}, \hat{X} - i\hat{P} ] = \frac{1}{2} ( -i[\hat{X}, \hat{P}] + i[\hat{P}, \hat{X}] ) = \frac{1}{2} ( -i[\hat{X}, \hat{P}] - i[\hat{X}, \hat{P}] ) = -i[\hat{X}, \hat{P}]
$$
代入 $[\hat{X}, \hat{P}] = i$，我们得到它们的基本[对易关系](@entry_id:136780)：
$$
[\hat{a}, \hat{a}^\dagger] = -i(i) = 1
$$

### [哈密顿量](@entry_id:172864)与数算符

现在，我们可以用[阶梯算符](@entry_id:199991)来重新表达[哈密顿量](@entry_id:172864)。首先，我们将 $\hat{X}$ 和 $\hat{P}$ 用 $\hat{a}$ 和 $\hat{a}^\dagger$ 表示：
$$
\hat{X} = \frac{1}{\sqrt{2}}(\hat{a} + \hat{a}^\dagger), \qquad \hat{P} = \frac{1}{i\sqrt{2}}(\hat{a} - \hat{a}^\dagger)
$$
将它们代入 $H = \frac{\hbar\omega}{2}(\hat{X}^2 + \hat{P}^2)$：
$$
\hat{H} = \frac{\hbar\omega}{2} \left[ \frac{1}{2}(\hat{a} + \hat{a}^\dagger)^2 - \frac{1}{2}(\hat{a} - \hat{a}^\dagger)^2 \right] = \frac{\hbar\omega}{4} [ (\hat{a}^2 + \hat{a}\hat{a}^\dagger + \hat{a}^\dagger\hat{a} + (\hat{a}^\dagger)^2) - (\hat{a}^2 - \hat{a}\hat{a}^\dagger - \hat{a}^\dagger\hat{a} + (\hat{a}^\dagger)^2) ]
$$
$$
\hat{H} = \frac{\hbar\omega}{4} [ 2(\hat{a}\hat{a}^\dagger + \hat{a}^\dagger\hat{a}) ] = \frac{\hbar\omega}{2} (\hat{a}\hat{a}^\dagger + \hat{a}^\dagger\hat{a})
$$
利用[对易关系](@entry_id:136780) $\hat{a}\hat{a}^\dagger = \hat{a}^\dagger\hat{a} + 1$，我们可以将[哈密顿量](@entry_id:172864)整理成**正常序 (normal-ordered)** 形式（即所有[产生算符](@entry_id:191512)都在湮灭算符的左边）：
$$
\hat{H} = \frac{\hbar\omega}{2} ( (\hat{a}^\dagger\hat{a} + 1) + \hat{a}^\dagger\hat{a} ) = \hbar\omega \left( \hat{a}^\dagger\hat{a} + \frac{1}{2} \right)
$$
这个结果是代数方法的核心。它表明谐振子的能量只依赖于算符组合 $\hat{a}^\dagger\hat{a}$。我们定义**数算符 (number operator)** $\hat{N} = \hat{a}^\dagger\hat{a}$，则[哈密顿量](@entry_id:172864)可以简洁地写为：
$$
\hat{H} = \hbar\omega \left( \hat{N} + \frac{1}{2} \right)
$$
寻找[哈密顿量](@entry_id:172864)的能谱问题，现在被完全转化为寻找数算符 $\hat{N}$ 的本征谱问题。

### 代数方法求解能谱

现在我们利用算符的代数性质来确定 $\hat{H}$ 的能谱 [@problem_id:2918123] [@problem_id:2918144]。

1.  **[阶梯算符](@entry_id:199991)的作用**：首先，我们考察[阶梯算符](@entry_id:199991)与[哈密顿量](@entry_id:172864)的[对易关系](@entry_id:136780)。
    $$
    [\hat{H}, \hat{a}] = [\hbar\omega(\hat{N} + 1/2), \hat{a}] = \hbar\omega[\hat{a}^\dagger\hat{a}, \hat{a}] = \hbar\omega(\hat{a}^\dagger[\hat{a}, \hat{a}] + [\hat{a}^\dagger, \hat{a}]\hat{a}) = \hbar\omega(-\hat{a}) = -\hbar\omega\hat{a}
    $$
    $$
    [\hat{H}, \hat{a}^\dagger] = [\hbar\omega(\hat{N} + 1/2), \hat{a}^\dagger] = \hbar\omega[\hat{a}^\dagger\hat{a}, \hat{a}^\dagger] = \hbar\omega(\hat{a}^\dagger[\hat{a}, \hat{a}^\dagger] + [\hat{a}^\dagger, \hat{a}^\dagger]\hat{a}) = \hbar\omega(\hat{a}^\dagger) = +\hbar\omega\hat{a}^\dagger
    $$
    假设 $|E\rangle$ 是 $\hat{H}$ 的一个[能量本征态](@entry_id:152154)，其[本征值](@entry_id:154894)为 $E$，即 $\hat{H}|E\rangle = E|E\rangle$。那么，我们考察 $\hat{a}|E\rangle$ 这个态的能量：
    $$
    \hat{H}(\hat{a}|E\rangle) = (\hat{a}\hat{H} + [\hat{H}, \hat{a}])|E\rangle = \hat{a}(E|E\rangle) - \hbar\omega\hat{a}|E\rangle = (E - \hbar\omega)(\hat{a}|E\rangle)
    $$
    类似地，对于 $\hat{a}^\dagger|E\rangle$：
    $$
    \hat{H}(\hat{a}^\dagger|E\rangle) = (\hat{a}^\dagger\hat{H} + [\hat{H}, \hat{a}^\dagger])|E\rangle = \hat{a}^\dagger(E|E\rangle) + \hbar\omega\hat{a}^\dagger|E\rangle = (E + \hbar\omega)(\hat{a}^\dagger|E\rangle)
    $$
    这表明，如果 $\hat{a}|E\rangle$ 和 $\hat{a}^\dagger|E\rangle$ 不是[零矢量](@entry_id:155273)，它们就分别是能量为 $E-\hbar\omega$ 和 $E+\hbar\omega$ 的新[本征态](@entry_id:149904)。因此，$\hat{a}$ 将能量降低一个量子 $\hbar\omega$，而 $\hat{a}^\dagger$ 将能量升高一个量子 $\hbar\omega$。这正是它们“[阶梯算符](@entry_id:199991)”名称的由来。

2.  **[基态](@entry_id:150928)的存在和能量**：物理系统的能量必须有下界。让我们考察任意归一化态 $|\psi\rangle$ 的[能量期望值](@entry_id:174035)：
    $$
    \langle\psi|\hat{H}|\psi\rangle = \hbar\omega \langle\psi|\hat{a}^\dagger\hat{a} + \frac{1}{2}|\psi\rangle = \hbar\omega \langle\psi|\hat{a}^\dagger\hat{a}|\psi\rangle + \frac{\hbar\omega}{2}
    $$
    由于 $\langle\psi|\hat{a}^\dagger\hat{a}|\psi\rangle = \langle \hat{a}\psi|\hat{a}\psi\rangle = \|\hat{a}|\psi\rangle\|^2 \ge 0$，我们得出结论：
    $$
    \langle\psi|\hat{H}|\psi\rangle \ge \frac{\hbar\omega}{2}
    $$
    所有[能量本征值](@entry_id:144381)都必须不小于 $\frac{\hbar\omega}{2}$。既然存在能量下界，那么从任意一个[能量本征态](@entry_id:152154)出发，连续作用降低算符 $\hat{a}$ 的过程必须在某一步终止。否则，我们将得到能量无限低的本征态，这与能量有下界相矛盾。
    这个终止过程意味着，必然存在一个能量最低的**[基态](@entry_id:150928)**（我们记作 $|0\rangle$），它被[湮灭算符](@entry_id:165390) $\hat{a}$ 湮灭：
    $$
    \hat{a}|0\rangle = 0
    $$
    这个[基态](@entry_id:150928)的能量可以通过[哈密顿量](@entry_id:172864)作用于它来计算：
    $$
    \hat{H}|0\rangle = \hbar\omega\left(\hat{a}^\dagger\hat{a} + \frac{1}{2}\right)|0\rangle = \hbar\omega\left(\hat{a}^\dagger(0) + \frac{1}{2}|0\rangle\right) = \frac{\hbar\omega}{2}|0\rangle
    $$
    因此，[基态能量](@entry_id:263704)为 $E_0 = \frac{\hbar\omega}{2}$，这也被称为**零点能 (zero-point energy)**。

3.  **[能谱](@entry_id:181780)的离散结构**：从[基态](@entry_id:150928) $|0\rangle$ 出发，我们可以通过连续作用[产生算符](@entry_id:191512) $\hat{a}^\dagger$ 来构建一个[能量本征态](@entry_id:152154)的阶梯。
    $$
    |1\rangle \propto \hat{a}^\dagger|0\rangle, \quad E_1 = E_0 + \hbar\omega = \frac{3}{2}\hbar\omega
    $$
    $$
    |2\rangle \propto \hat{a}^\dagger|1\rangle \propto (\hat{a}^\dagger)^2|0\rangle, \quad E_2 = E_1 + \hbar\omega = \frac{5}{2}\hbar\omega
    $$
    一般地，第 $n$ 个[激发态](@entry_id:261453) $|n\rangle$ 可以通过对[基态](@entry_id:150928)作用 $n$ 次[产生算符](@entry_id:191512)得到，其能量为：
    $$
    E_n = \left(n + \frac{1}{2}\right)\hbar\omega, \quad n = 0, 1, 2, \dots
    $$
    数算符 $\hat{N}$ 作用在 $|n\rangle$ 上的[本征值](@entry_id:154894)为 $n$，即 $\hat{N}|n\rangle = n|n\rangle$。这些态构成了整个系统的完备正交基。至此，我们完全通过代数方法确定了量子谐振子的[能谱](@entry_id:181780)：它是离散的、等间距的，并且有下界。

### 连接到[波函数](@entry_id:147440)：位置表象

代数方法非常强大，但我们通常也希望了解这些[能量本征态](@entry_id:152154)在位置空间中的具体形式，即[波函数](@entry_id:147440) $\psi_n(x) = \langle x|n \rangle$。

#### [基态](@entry_id:150928)[波函数](@entry_id:147440)

我们可以通过求解[基态](@entry_id:150928)条件 $\hat{a}|0\rangle = 0$ 在位置表象中的形式来找到[基态](@entry_id:150928)[波函数](@entry_id:147440) $\psi_0(x)$ [@problem_id:2918061]。首先，我们将 $\hat{a}$ 算符用位置表象表示，将 $\hat{x}$ 替换为 $x$，将 $\hat{p}$ 替换为 $-i\hbar\frac{d}{dx}$：
$$
\hat{a} = \sqrt{\frac{m\omega}{2\hbar}}\left(x + \frac{i}{m\omega}(-i\hbar\frac{d}{dx})\right) = \sqrt{\frac{m\omega}{2\hbar}}\left(x + \frac{\hbar}{m\omega}\frac{d}{dx}\right)
$$
于是，$\langle x|\hat{a}|0\rangle = 0$ 变成一个[一阶微分方程](@entry_id:173139)：
$$
\left(x + \frac{\hbar}{m\omega}\frac{d}{dx}\right)\psi_0(x) = 0
$$
这是一个可分离变量的方程，其解为：
$$
\psi_0(x) = C \exp\left(-\frac{m\omega}{2\hbar}x^2\right)
$$
这是一个高斯函数。通过[归一化条件](@entry_id:156486) $\int_{-\infty}^{\infty}|\psi_0(x)|^2dx = 1$，我们可以确定[归一化常数](@entry_id:752675) $C$，得到归一化的[基态](@entry_id:150928)[波函数](@entry_id:147440)：
$$
\psi_0(x) = \left(\frac{m\omega}{\pi\hbar}\right)^{1/4} \exp\left(-\frac{m\omega}{2\hbar}x^2\right)
$$

#### [激发态](@entry_id:261453)与厄米多项式

[激发态](@entry_id:261453)[波函数](@entry_id:147440)可以通过对[基态](@entry_id:150928)[波函数](@entry_id:147440)重复作用[产生算符](@entry_id:191512) $\hat{a}^\dagger$ 来获得。在位置表象中，$\hat{a}^\dagger$ 是一个[微分](@entry_id:158718)算符：
$$
\hat{a}^\dagger = \sqrt{\frac{m\omega}{2\hbar}}\left(x - \frac{\hbar}{m\omega}\frac{d}{dx}\right)
$$
由于 $\psi_n(x) \propto (\hat{a}^\dagger)^n \psi_0(x)$，我们可以看到，每次作用 $\hat{a}^\dagger$ 都会在原来的[高斯函数](@entry_id:261394)前产生一个多项式因子，并且多项式的阶数增加一。因此，第 $n$ 个[激发态](@entry_id:261453)的[波函数](@entry_id:147440)具有以下形式 [@problem_id:2918102]：
$$
\psi_n(x) = N_n H_n(\xi) \exp(-\xi^2/2)
$$
其中 $\xi = \sqrt{\frac{m\omega}{\hbar}}x$ 是无量纲坐标，$N_n$ 是[归一化常数](@entry_id:752675)，而 $H_n(\xi)$ 是一个 $n$ 次多项式，称为**厄米多项式 (Hermite polynomial)**。

我们可以从 $\hat{a}^\dagger$ 的算符形式直接导出一个产生这些多项式的封闭表达式，即**罗德里格斯公式 (Rodrigues' formula)** [@problem_id:2918057]。通过一个巧妙的算符恒等式变换，可以证明：
$$
\left(\xi - \frac{d}{d\xi}\right)^n \exp(-\xi^2/2) = (-1)^n \exp(\xi^2/2) \frac{d^n}{d\xi^n} \exp(-\xi^2)
$$
由此，我们可以将厄米多项式定义为（忽略归一化）：
$$
H_n(\xi) = (-1)^n \exp(\xi^2) \frac{d^n}{d\xi^n} \exp(-\xi^2)
$$
这个公式提供了一种从高斯函数出发，通过重复求导来构造任意阶厄米多项式的系统方法，完美地将代数构造 $(\hat{a}^\dagger)^n|0\rangle$ 与解析解联系起来。

### 形式主义的应用

[阶梯算符](@entry_id:199991)形式主义的威力在于它能极大地简化对[物理可观测量](@entry_id:154692)的计算。

#### 可观测量的矩阵元

计算诸如位置和动量在不同能级之间的跃迁矩阵元，在[光谱学](@entry_id:141940)中至关重要。利用[阶梯算符](@entry_id:199991)，这项工作变得异常简单。我们将 $\hat{x}$ 和 $\hat{p}$ 用 $\hat{a}$ 和 $\hat{a}^\dagger$ 表示：
$$
\hat{x} = \sqrt{\frac{\hbar}{2m\omega}}(\hat{a} + \hat{a}^\dagger)
$$
$$
\hat{p} = i\sqrt{\frac{m\hbar\omega}{2}}(\hat{a}^\dagger - \hat{a})
$$
要计算矩阵元 $\langle n|\hat{x}|\ell\rangle$，我们利用[阶梯算符](@entry_id:199991)对能量本征态的作用关系（经过归一化）：
$$
\hat{a}|n\rangle = \sqrt{n}|n-1\rangle, \qquad \hat{a}^\dagger|n\rangle = \sqrt{n+1}|n+1\rangle
$$
于是，
$$
\langle n|\hat{x}|\ell\rangle = \sqrt{\frac{\hbar}{2m\omega}} \langle n|(\hat{a} + \hat{a}^\dagger)|\ell\rangle = \sqrt{\frac{\hbar}{2m\omega}} (\sqrt{\ell}\langle n|\ell-1\rangle + \sqrt{\ell+1}\langle n|\ell+1\rangle)
$$
由于态的正交性 $\langle n|k\rangle = \delta_{nk}$，上式给出：
$$
\langle n|\hat{x}|\ell\rangle = \sqrt{\frac{\hbar}{2m\omega}} (\sqrt{\ell}\delta_{n, \ell-1} + \sqrt{\ell+1}\delta_{n, \ell+1})
$$
同理，对于动量算符：
$$
\langle n|\hat{p}|\ell\rangle = i\sqrt{\frac{m\hbar\omega}{2}} (\sqrt{\ell+1}\delta_{n, \ell+1} - \sqrt{\ell}\delta_{n, \ell-1})
$$
这些结果 [@problem_id:2918122] 表明，位置和[动量算符](@entry_id:151743)只在相邻能级之间（即 $\ell = n \pm 1$）有非[零矩阵](@entry_id:155836)元。这直接导出了谐振子的**选择定则** $\Delta n = \pm 1$，即在[偶极近似](@entry_id:152759)下，光与[谐振子](@entry_id:155622)的相互作用只会引起相邻能级间的跃迁。

#### [期望值](@entry_id:153208)与维里定理

计算[可观测量](@entry_id:267133)在某个能级上的[期望值](@entry_id:153208)也同样简单。例如，我们计算 $\langle n|\hat{x}^2|n\rangle$ [@problem_id:2918066]。
$$
\hat{x}^2 = \frac{\hbar}{2m\omega}(\hat{a} + \hat{a}^\dagger)^2 = \frac{\hbar}{2m\omega}(\hat{a}^2 + \hat{a}\hat{a}^\dagger + \hat{a}^\dagger\hat{a} + (\hat{a}^\dagger)^2)
$$
在计算[期望值](@entry_id:153208) $\langle n|...|n\rangle$ 时，任何不等数量的产生和[湮灭算符](@entry_id:165390)的项（如 $\hat{a}^2$ 和 $(\hat{a}^\dagger)^2$）都会因态的正交性而贡献为零。因此我们只需考虑包含相同数量 $\hat{a}$ 和 $\hat{a}^\dagger$ 的项。
$$
\langle n|\hat{x}^2|n\rangle = \frac{\hbar}{2m\omega}\langle n|\hat{a}\hat{a}^\dagger + \hat{a}^\dagger\hat{a}|n\rangle = \frac{\hbar}{2m\omega}\langle n|2\hat{a}^\dagger\hat{a} + 1|n\rangle = \frac{\hbar}{2m\omega}(2n+1)
$$
类似地，
$$
\langle n|\hat{p}^2|n\rangle = -\frac{m\hbar\omega}{2}\langle n|(\hat{a}^\dagger - \hat{a})^2|n\rangle = \frac{m\hbar\omega}{2}\langle n|\hat{a}\hat{a}^\dagger + \hat{a}^\dagger\hat{a}|n\rangle = \frac{m\hbar\omega}{2}(2n+1)
$$
利用这些结果，我们可以验证[量子谐振子](@entry_id:140678)的**[维里定理](@entry_id:146441) (Virial Theorem)**。体系的[平均动能](@entry_id:146353) $\langle T \rangle$ 和平均势能 $\langle V \rangle$ 分别为：
$$
\langle T \rangle = \frac{\langle p^2 \rangle}{2m} = \frac{1}{2m} \frac{m\hbar\omega}{2}(2n+1) = \frac{\hbar\omega}{2}\left(n+\frac{1}{2}\right) = \frac{1}{2}E_n
$$
$$
\langle V \rangle = \frac{1}{2}m\omega^2\langle x^2 \rangle = \frac{1}{2}m\omega^2 \frac{\hbar}{2m\omega}(2n+1) = \frac{\hbar\omega}{2}\left(n+\frac{1}{2}\right) = \frac{1}{2}E_n
$$
我们得到了一个漂亮的结果：对于量子谐振子的任意一个[能量本征态](@entry_id:152154)，其[平均动能](@entry_id:146353)等于平均势能，且都等于总能量的一半。这不仅是理论自洽性的有力证明，也深刻揭示了束缚态中能量的分配规律。

本章我们通过引入和运用[阶梯算符](@entry_id:199991)，系统地解决了[量子谐振子](@entry_id:140678)问题。这种代数方法不仅展示了量子力学形式上的优雅，也为处理更复杂的[量子场论](@entry_id:138177)问题提供了基本[范式](@entry_id:161181)。