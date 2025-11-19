## 引言
在量子力学的奇妙世界中，“相位”是一个核心却又常常引起困惑的概念。一个[量子态](@entry_id:146142)的数学描述中包含相位因子，但并非所有相位都对应着可观测的物理现实。这种微妙的区别构成了量子理论的基石之一，并引出了一个根本性问题：我们如何区分一个仅仅是数学冗余的相位，与一个蕴含着深刻[物理信息](@entry_id:152556)、能够驱动量子现象的相位？这正是[全局相位](@entry_id:147947)与相对相位之争的核心。

本文旨在系统性地剖析这一关键[二分法](@entry_id:140816)。我们将带领读者穿越[量子相位](@entry_id:197087)的迷雾，从基本原理出发，直至前沿应用。
*   在**“原理与机制”**一章中，我们将严格定义[全局相位](@entry_id:147947)和[相对相位](@entry_id:148120)，阐明为何前者不可观测，而后者却是量子干涉、动力学演化和可观测量[期望值](@entry_id:153208)的决定性因素。我们还将探讨[超选择定则](@entry_id:203866)如何为相干叠加划定边界。
*   接下来，在**“应用与跨学科连接”**一章中，我们将展示相对相位这一概念如何在量子光学、化学、[材料科学](@entry_id:152226)和[量子信息](@entry_id:137721)等多个领域中大放异彩，从经典的双缝干涉到现代的[拓扑物质](@entry_id:161097)和[量子算法](@entry_id:147346)。
*   最后，**“动手实践”**部分将通过具体的计算问题，让您亲身体验如何操控和测量相对相位，巩固您对这一核心概念的理解。

通过本次学习，您将掌握区分并应用两种相位的关[键能](@entry_id:142761)力，深刻理解它们在构建我们对微观世界认知中的不同角色。

## 原理与机制

在量子力学的数学框架中，一个物理系统的状态由希尔伯特空间中的一个矢量来描述，这个矢量通常被称为态矢量，并用[狄拉克符号](@entry_id:154811) $|\psi\rangle$ 表示。然而，一个关键的微妙之处在于，态矢量本身并非物理实体。相反，它是一个数学工具，用于计算[可观测量](@entry_id:267133)的测量概率和[期望值](@entry_id:153208)。这种区别引出了量子力学中一个核心且深刻的概念：相位的角色。本章中，我们将系统地剖析两种类型的相位——[全局相位](@entry_id:147947)和相对相位，并阐明它们在量子现象中截然不同的作用。

### [量子态](@entry_id:146142)矢的相位模糊性：[全局相位](@entry_id:147947)

根据量子力学的基本假设，所有关于一个系统的[物理信息](@entry_id:152556)都蕴含在其态矢量 $|\psi\rangle$ 中。然而，态矢与物理现实之间的联系并非一一对应。具体来说，如果两个态矢量 $|\psi\rangle$ 和 $|\phi\rangle$ 仅相差一个模为1的复数因子，即 $|\phi\rangle = e^{i\alpha}|\psi\rangle$，其中 $\alpha$ 是一个任意实数，那么这两个态矢量描述的是完全相同的物理状态。

要理解为什么会这样，我们必须考察量子力学如何从态矢量中提取可观测的预测。物理预测通常有两种形式：测量概率和可观测量的[期望值](@entry_id:153208)。

1.  **测量概率**：在一个量子系统中，如果我们测量某个物理量，系统将坍缩到该物理量算符的一个本征态 $|\chi\rangle$。系统处于 $|\psi\rangle$ 状态时，测量得到结果 $|\chi\rangle$ 的概率由[玻恩定则](@entry_id:154470)给出，即 $P = |\langle \chi | \psi \rangle|^2$。如果我们用 $e^{i\alpha}|\psi\rangle$ 来描述这个状态，概率变为 $|\langle \chi | e^{i\alpha}\psi \rangle|^2 = |e^{i\alpha}\langle \chi | \psi \rangle|^2 = |e^{i\alpha}|^2 |\langle \chi | \psi \rangle|^2$。由于 $|e^{i\alpha}| = 1$，这个概率与原来的完全相同。

2.  **[期望值](@entry_id:153208)**：一个由[厄米算符](@entry_id:153410) $\hat{O}$ 表示的可观测量，其在状态 $|\psi\rangle$ 中的[期望值](@entry_id:153208)被定义为 $\langle \hat{O} \rangle = \langle \psi | \hat{O} | \psi \rangle$。对于状态 $e^{i\alpha}|\psi\rangle$，[期望值](@entry_id:153208)变为：
    $$
    \langle \hat{O} \rangle' = \langle e^{i\alpha}\psi | \hat{O} | e^{i\alpha}\psi \rangle = \langle \psi | (e^{-i\alpha}) \hat{O} (e^{i\alpha}) | \psi \rangle
    $$
    由于 $e^{i\alpha}$ 是一个标量，它可以与算符 $\hat{O}$ 对易，因此：
    $$
    \langle \hat{O} \rangle' = e^{-i\alpha} e^{i\alpha} \langle \psi | \hat{O} | \psi \rangle = \langle \psi | \hat{O} | \psi \rangle = \langle \hat{O} \rangle
    $$
    同样，[期望值](@entry_id:153208)保持不变。

因为所有可能的测量结果的[概率分布](@entry_id:146404)都保持不变，所以我们说这两个态矢量是**物理上不可区分的**。这个因子 $e^{i\alpha}$ 被称为**[全局相位](@entry_id:147947) (global phase)**。它是一个整体上乘以整个态矢量的相位因子，不具有任何可观测的物理效应。

例如，考虑一个二维希尔伯特空间中的几个态矢量 [@problem_id:2096223] [@problem_id:2096227]：
*   $|\psi_I\rangle = \frac{1}{2}|0\rangle + \frac{\sqrt{3}}{2}|1\rangle$
*   $|\psi_{II}\rangle = -\frac{1}{2}|0\rangle - \frac{\sqrt{3}}{2}|1\rangle = -1 \cdot |\psi_I\rangle = e^{i\pi} |\psi_I\rangle$
*   $|\psi_{IV}\rangle = \frac{i}{2}|0\rangle + \frac{i\sqrt{3}}{2}|1\rangle = i \cdot |\psi_I\rangle = e^{i\pi/2} |\psi_I\rangle$

尽管 $|\psi_I\rangle$、$|\psi_{II}\rangle$ 和 $|\psi_{IV}\rangle$ 在数学上是不同的矢量，但它们之间仅相差一个[全局相位](@entry_id:147947)因子（分别为 $e^{i\pi}$ 和 $e^{i\pi/2}$）。因此，它们代表了完全相同的物理状态。任何实验都无法区分一个处于 $|\psi_I\rangle$ 状态的系统和一个处于 $|\psi_{IV}\rangle$ 状态的系统。

### [相对相位](@entry_id:148120)的物理意义

[全局相位](@entry_id:147947)的不[可观测性](@entry_id:152062)引出了一个更深层次的问题：相位在量子力学中是否总是无关紧要的？答案是否定的，这引导我们进入**[相对相位](@entry_id:148120) (relative phase)** 的概念，它是[量子叠加](@entry_id:137914)和干涉现象的核心。

考虑一个由两个正交基矢 $|a\rangle$ 和 $|b\rangle$ 张成的系统中一个更普遍的叠加态：
$$
|\psi\rangle = c_a |a\rangle + c_b |b\rangle
$$
其中 $c_a$ 和 $c_b$ 是复数系数。我们可以将它们写成极坐标形式：$c_a = |c_a|e^{i\phi_a}$ 和 $c_b = |c_b|e^{i\phi_b}$。于是，态矢量变为：
$$
|\psi\rangle = |c_a|e^{i\phi_a} |a\rangle + |c_b|e^{i\phi_b} |b\rangle
$$
利用[全局相位](@entry_id:147947)的自由度，我们可以将整个态矢量乘以 $e^{-i\phi_a}$ 而不改变其物理内容。这样做可以消除第一个系数的相位：
$$
|\psi'\rangle = e^{-i\phi_a}|\psi\rangle = |c_a| |a\rangle + |c_b|e^{i(\phi_b - \phi_a)} |b\rangle
$$
现在，状态 $|\psi'\rangle$ 在物理上等价于 $|\psi\rangle$。然而，我们注意到，虽然 $\phi_a$ 被消除了，但两个[基矢](@entry_id:199546)系数之间的相位差 $\theta = \phi_b - \phi_a$ 仍然存在。这个相位差，即**相对相位**，无法通过乘以一个[全局相位](@entry_id:147947)因子来消除。事实证明，正是这个[相对相位](@entry_id:148120)，而非每个系数的绝对相位，蕴含了至关重要的物理信息。

### 观测相对相位的后果

与[全局相位](@entry_id:147947)不同，[相对相位](@entry_id:148120)是可观测的，并且是许多关键量子效应（如干涉、[量子隧穿](@entry_id:142867)和[量子计算](@entry_id:142712)中的算法）的根源。下面我们将通过几个例子来展示[相对相位](@entry_id:148120)的物理后果。

#### 不同基下的测量结果

[相对相位](@entry_id:148120)的影响在改变测量基时会戏剧性地显现出来。假设物理学家Alice和Bob正在研究一个双能级量子系统（[量子比特](@entry_id:137928)） [@problem_id:2096265]。Alice可以制备以下两种状态之一：
*   状态A: $|\Psi_A\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$
*   状态B: $|\Psi_B\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle) = \frac{1}{\sqrt{2}}(|0\rangle + e^{i\pi}|1\rangle)$

这两个状态的唯一区别是 $|1\rangle$ 分量前的相对相位：状态A中为0，状态B中为 $\pi$。如果我们在计算基 $\{|0\rangle, |1\rangle\}$ 中测量这两个状态，我们会发现对于两个状态，测量结果为 $|0\rangle$ 和 $|1\rangle$ 的概率都是 $|\frac{1}{\sqrt{2}}|^2 = \frac{1}{2}$。基于此测量，这两个状态似乎是无法区分的。

然而，如果Bob选择在另一个称为Hadamard基的基中进行测量，情况则完全不同。Hadamard基的[基矢](@entry_id:199546)定义为：
*   $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$
*   $|-\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)$

现在我们计算Bob的测量概率。
对于Alice制备的状态A，即 $|\Psi_A\rangle = |+\rangle$：
*   Bob测得 $|+\rangle$ 的概率: $P(+|A) = |\langle + | \Psi_A \rangle|^2 = |\langle + | + \rangle|^2 = 1^2 = 1$
*   Bob测得 $|-\rangle$ 的概率: $P(-|A) = |\langle - | \Psi_A \rangle|^2 = |\langle - | + \rangle|^2 = 0^2 = 0$

对于Alice制备的状态B，即 $|\Psi_B\rangle = |-\rangle$：
*   Bob测得 $|+\rangle$ 的概率: $P(+|B) = |\langle + | \Psi_B \rangle|^2 = |\langle + | - \rangle|^2 = 0^2 = 0$
*   Bob测得 $|-\rangle$ 的概率: $P(-|B) = |\langle - | \Psi_B \rangle|^2 = |\langle - | - \rangle|^2 = 1^2 = 1$

结果是惊人的：通过在Hadamard基中测量，Bob可以完美地确定Alice制备的是状态A还是状态B。一个简单的相对相位符号（$+$或$-$）的改变，导致了在特定测量下确定性的、完全相反的结果。这清晰地证明了[相对相位](@entry_id:148120)是一个可观测的、真实的物理属性。

#### [量子干涉](@entry_id:139127)

相对相位最直观的体现是在干涉现象中。想象一个粒子，如[双缝实验](@entry_id:155892)中的电子，其状态是两个空间局域[波包](@entry_id:154698)的叠加，一个在左边 ($\psi_L(x)$)，一个在右边 ($\psi_R(x)$)。其总的态函数可以写为：
$$
\Psi(x) = \frac{1}{\sqrt{N}} \left( \psi_L(x) + e^{i\theta} \psi_R(x) \right)
$$
其中 $e^{i\theta}$ 是相对相位因子，$N$ 是[归一化常数](@entry_id:752675)。

根据[玻恩定则](@entry_id:154470)，在位置 $x$ 找到该粒子的概率密度是 $P(x) = |\Psi(x)|^2$。我们来展开这个表达式：
$$
P(x) = \frac{1}{N} \left( \psi_L^*(x) + e^{-i\theta} \psi_R^*(x) \right) \left( \psi_L(x) + e^{i\theta} \psi_R(x) \right)
$$
$$
P(x) = \frac{1}{N} \left( |\psi_L(x)|^2 + |\psi_R(x)|^2 + e^{i\theta}\psi_L^*(x)\psi_R(x) + e^{-i\theta}\psi_L(x)\psi_R^*(x) \right)
$$
最后两项被称为**干涉项**。如果[波函数](@entry_id:147440) $\psi_L(x)$ 和 $\psi_R(x)$ 是实函数（这在许多简化模型中是常见情况），则干涉项可以简化为：
$$
P(x) = \frac{1}{N} \left( \psi_L(x)^2 + \psi_R(x)^2 + 2\psi_L(x)\psi_R(x)\cos\theta \right)
$$
这个结果非常重要。它表明，在两个[波包](@entry_id:154698)重叠的区域，找到粒子的概率不仅仅是两个独立概率之和（$|\psi_L|^2 + |\psi_R|^2$），还包含一个依赖于[相对相位](@entry_id:148120) $\theta$ 的[振荡](@entry_id:267781)项。

*   如果 $\theta = 0$，则 $\cos\theta=1$，干涉项为正，导致**相长干涉**，概率密度增大。
*   如果 $\theta = \pi$，则 $\cos\theta=-1$，干涉项为负，导致**相消干涉**，概率密度减小。
*   对于其他值的 $\theta$，干涉程度介于两者之间。

例如，在一个对称[双势阱](@entry_id:171252)模型中 [@problem_id:2096258]，如果两个[高斯波包](@entry_id:151158)的中心分别位于 $-a$ 和 $+a$，那么在中心点 $x=0$ 处，$\psi_L(0) = \psi_R(0)$。此时的概率密度正比于 $(1+\cos\theta)$。这意味着通过调控相对相位 $\theta$，我们可以控制粒子出现在两个[势阱](@entry_id:151413)中间的概率，这是一个可直接测量的物理效应。

#### 可观测量[期望值](@entry_id:153208)

相对相位也直接影响物理量的[期望值](@entry_id:153208)。考虑一个自旋-1/2的粒子，其状态是自旋向上 $|+\rangle$ 和自旋向下 $|-\rangle$ 的叠加。假设我们制备了两个状态，它们仅在[相对相位](@entry_id:148120)上有所不同 [@problem_id:2096269]：
$$
|\psi_A\rangle = \frac{1}{\sqrt{2}}(|+\rangle + e^{i\pi/3}|-\rangle)
$$
$$
|\psi_B\rangle = \frac{1}{\sqrt{2}}(|+\rangle + e^{-i\pi/3}|-\rangle)
$$
我们来计算沿y方向的自旋分量 $S_y$ 的[期望值](@entry_id:153208)。$S_y$ 算符在 $\{|+\rangle, |-\rangle\}$ 基下的矩阵表示为 $\frac{\hbar}{2} \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}$。

对于状态 $|\psi_A\rangle$，其[期望值](@entry_id:153208) $\langle S_y \rangle_A = \langle \psi_A|S_y|\psi_A \rangle$ 的计算结果为 $\frac{\hbar}{2}\sin(\pi/3) = \frac{\hbar\sqrt{3}}{4}$。
对于状态 $|\psi_B\rangle$，其[期望值](@entry_id:153208) $\langle S_y \rangle_B = \langle \psi_B|S_y|\psi_B \rangle$ 的计算结果为 $\frac{\hbar}{2}\sin(-\pi/3) = -\frac{\hbar\sqrt{3}}{4}$。

显然，$\langle S_y \rangle_A$ 和 $\langle S_y \rangle_B$ 不仅不同，而且符号相反。这意味着如果我们对大量按方法A制备的粒子测量y方向自旋，我们会得到一个正的平均值；而对于按方法B制备的粒子，我们会得到一个负的平均值。这再次证明了相对相位是一个具有直接物理后果的参数。

#### [密度矩阵表象](@entry_id:183082)

描述相对相位的更形式化、更强大的工具是**[密度矩阵](@entry_id:139892)** $\rho$。对于一个[纯态](@entry_id:141688) $|\psi\rangle$，其[密度算符](@entry_id:138151)定义为投影算符 $\rho = |\psi\rangle\langle\psi|$。对于一个一般的[量子比特](@entry_id:137928)态 $|\psi\rangle = c_0|0\rangle + c_1|1\rangle$，其[密度矩阵](@entry_id:139892)为：
$$
\rho = \begin{pmatrix} \langle 0|\psi\rangle\langle\psi|0\rangle  \langle 0|\psi\rangle\langle\psi|1\rangle \\ \langle 1|\psi\rangle\langle\psi|0\rangle  \langle 1|\psi\rangle\langle\psi|1\rangle \end{pmatrix} = \begin{pmatrix} c_0 c_0^*  c_0 c_1^* \\ c_1 c_0^*  c_1 c_1^* \end{pmatrix} = \begin{pmatrix} |c_0|^2  c_0 c_1^* \\ c_1 c_0^*  |c_1|^2 \end{pmatrix}
$$
观察这个矩阵的结构：
*   **对角元素**：$\rho_{00} = |c_0|^2$ 和 $\rho_{11} = |c_1|^2$ 分别是在计算基中测得 $|0\rangle$ 和 $|1\rangle$ 的概率。它们被称为**布居数 (populations)**，是实数且不含相位信息。
*   **非对角元素**：$\rho_{01} = c_0 c_1^*$ 和 $\rho_{10} = c_1 c_0^*$ 被称为**相干项 (coherences)**。它们包含了[基态](@entry_id:150928)之间叠加的全部信息，尤其是[相对相位](@entry_id:148120)。

如果我们设 $c_0 = a_0$ (实数) 并通过[全局相位](@entry_id:147947)选择将 $c_1$ 写为 $c_1 = a_1 e^{i\delta}$，其中 $\delta$ 是相对相位 [@problem_id:2096204]，那么非对角元素变为：
$$
\rho_{10} = c_1 c_0^* = (a_1 e^{i\delta})(a_0) = a_0 a_1 e^{i\delta} = a_0 a_1 (\cos\delta + i\sin\delta)
$$
可见，$\rho_{10}$ 的相位就是[相对相位](@entry_id:148120) $\delta$。实际上，我们可以通过测量 $\rho_{10}$ 的实部和虚部来确定 $\delta$，其比值为 $\frac{\text{Im}(\rho_{10})}{\text{Re}(\rho_{10})} = \tan\delta$。[密度矩阵](@entry_id:139892)的非对角元素是否为零，是判断一个系统是否存在量子相干性（即有效的叠加）的判据。

### [相对相位](@entry_id:148120)的动力学：[量子拍](@entry_id:155286)

到目前为止，我们讨论的都是静态的[相对相位](@entry_id:148120)。然而，[相对相位](@entry_id:148120)最引人入胜的特性之一是它如何随[时间演化](@entry_id:153943)，从而驱动量子系统的动力学。

一个系统的态矢量的时间演化由薛定谔方程支配。对于一个具有不随时变的[哈密顿算符](@entry_id:144286) $\hat{H}$ 的系统，如果初始状态是能量本征态 $|E_n\rangle$（即 $\hat{H}|E_n\rangle = E_n|E_n\rangle$），那么其时间演化非常简单：
$$
|E_n(t)\rangle = e^{-iE_n t/\hbar} |E_n(0)\rangle
$$
这是一个**[定态](@entry_id:137260) (stationary state)**。注意，时间演化仅仅引入了一个时间依赖的**[全局相位](@entry_id:147947)**。由于[全局相位](@entry_id:147947)不可观测，定态的所有物理属性（如[概率密度](@entry_id:175496)、[期望值](@entry_id:153208)）都不会随时间改变。

然而，如果系统初始处于两个（或多个）能量本征态的叠加态，情况就完全不同了。考虑初始状态 [@problem_id:2096221]：
$$
|\Psi(0)\rangle = c_1|E_1\rangle + c_2|E_2\rangle
$$
根据薛定谔方程的线性特性，时间演化后的状态是各个本征态独立演化的叠加：
$$
|\Psi(t)\rangle = c_1 e^{-iE_1 t/\hbar} |E_1\rangle + c_2 e^{-iE_2 t/\hbar} |E_2\rangle
$$
为了看清[相对相位](@entry_id:148120)的演化，我们提取一个共同的相位因子 $e^{-iE_1 t/\hbar}$ 作为[全局相位](@entry_id:147947)：
$$
|\Psi(t)\rangle = e^{-iE_1 t/\hbar} \left( c_1 |E_1\rangle + c_2 e^{-i(E_2 - E_1)t/\hbar} |E_2\rangle \right)
$$
现在，物理上等价的态矢（括号内的部分）清楚地显示，两个[能量本征态](@entry_id:152154)之间的**相对相位随[时间演化](@entry_id:153943)**，其值为 $\theta(t) = \theta(0) - (E_2 - E_1)t/\hbar$。这个时间依赖的[相对相位](@entry_id:148120)导致了可观测量的[振荡](@entry_id:267781)，这种现象通常被称为**[量子拍](@entry_id:155286) (quantum beats)**。

[振荡](@entry_id:267781)的角频率由能量差决定：
$$
\omega = \frac{E_2 - E_1}{\hbar}
$$
由于我们已经知道[期望值](@entry_id:153208)和干涉图样依赖于[相对相位](@entry_id:148120)，现在这个相位随时间变化，这些[可观测量](@entry_id:267133)也将以频率 $\omega$ [振荡](@entry_id:267781)。例如，一个[可观测量](@entry_id:267133) $\hat{X}$ 的[期望值](@entry_id:153208)可能会表现出类似 $\langle \hat{X} \rangle_t = A\cos(\omega t + \phi_0)$ 的行为 [@problem_id:2096221]。

这个原理在各种物理系统中都有体现：
*   在一个[一维无限深势阱](@entry_id:271157)中，处于[基态](@entry_id:150928) $|\psi_1\rangle$ 和第一[激发态](@entry_id:261453) $|\psi_2\rangle$ 叠加的粒子，其概率密度 $|\Psi(x,t)|^2$ 会以频率 $\omega=(E_2-E_1)/\hbar$ 在阱内来回“晃动” [@problem_id:2096259]。经过一段时间 $T = \frac{2\pi}{\omega} = \frac{2\pi\hbar}{E_2-E_1}$ 后，[相对相位](@entry_id:148120)演化了 $2\pi$，[概率密度](@entry_id:175496)将首次完全恢复到初始时刻的形状，这个时间被称为**复振周期 (revival time)**。
*   在[量子谐振子](@entry_id:140678)中，处于[基态](@entry_id:150928)和第二[激发态](@entry_id:261453)叠加的电子，其位置平方的[期望值](@entry_id:153208) $\langle x^2 \rangle$ (与[波包](@entry_id:154698)宽度有关) 会以频率 $f = \omega/(2\pi) = (E_2-E_0)/(h)$ [振荡](@entry_id:267781) [@problem_id:2096252]。

### 叠加的边界：[超选择定则](@entry_id:203866)

我们已经看到，相对相位在拥有相同[量子数](@entry_id:145558)（如同种粒子的不同自旋态或同一[势阱](@entry_id:151413)中的不同能级）的态的叠加中扮演着核心角色。这引出了一个终极问题：我们是否可以任意地将任何两个态叠加起来，并讨论它们之间的相对相位？

答案是否定的。在某些情况下，叠加态和其中的[相对相位](@entry_id:148120)是无物理意义的。这由**[超选择定则](@entry_id:203866) (superselection rules)** 所限制。

一个著名的例子是[电荷](@entry_id:275494)[超选择定则](@entry_id:203866)。考虑一个思想实验，物理学家试图制备一个质子态 $|p\rangle$ 和一个中子态 $|n\rangle$ 的叠加态 [@problem_id:2096219]：
$$
|\psi\rangle = c_p |p\rangle + c_n e^{i\theta} |n\rangle
$$
质[子带](@entry_id:154462)[电荷](@entry_id:275494) $+e$，中子[电荷](@entry_id:275494)为0。它们是[电荷](@entry_id:275494)算符 $\hat{Q}$ 的本征态，且[本征值](@entry_id:154894)不同。[超选择定则](@entry_id:203866)指出，**所有物理可观测量 $\hat{O}$ 都必须与[守恒荷](@entry_id:145660)（如此处的[电荷](@entry_id:275494) $\hat{Q}$）的算符对易**，即 $[\hat{O}, \hat{Q}] = 0$。

这个看似抽象的规则有一个强大的推论。对于任意满足该规则的算符 $\hat{O}$，其在不同[电荷](@entry_id:275494)[本征态](@entry_id:149904)之间的[矩阵元](@entry_id:186505)必定为零。我们可以证明这一点：
$$
\langle p | [\hat{O}, \hat{Q}] | n \rangle = \langle p | (\hat{O}\hat{Q} - \hat{Q}\hat{O}) | n \rangle = 0
$$
$$
\langle p | \hat{O} (q_n |n\rangle) - (q_p \langle p|) \hat{O} | n \rangle = (q_n - q_p) \langle p | \hat{O} | n \rangle = 0
$$
由于 $q_n \neq q_p$（0 vs. +e），我们必然得到 $\langle p | \hat{O} | n \rangle = 0$。

现在，我们来计算任意[可观测量](@entry_id:267133) $\hat{O}$ 在这个假想叠加态中的[期望值](@entry_id:153208)：
$$
\langle\psi|\hat{O}|\psi\rangle = |c_p|^2\langle p|\hat{O}|p\rangle + |c_n|^2\langle n|\hat{O}|n\rangle + c_p^*c_n e^{i\theta}\langle p|\hat{O}|n\rangle + c_n^*c_p e^{-i\theta}\langle n|\hat{O}|p\rangle
$$
由于[交叉](@entry_id:147634)项 $\langle p|\hat{O}|n\rangle$ 和 $\langle n|\hat{O}|p\rangle$ 都为零，上式简化为：
$$
\langle\psi|\hat{O}|\psi\rangle = |c_p|^2\langle p|\hat{O}|p\rangle + |c_n|^2\langle n|\hat{O}|n\rangle
$$
这个[期望值](@entry_id:153208)是两个独立状态[期望值](@entry_id:153208)的加权平均，它完全不依赖于[相对相位](@entry_id:148120) $\theta$！这意味着，没有任何物理测量可以揭示或依赖于质子和中子态之间的相对相位。因此，这种叠加（有时被称为“非[相干叠加](@entry_id:170209)”）在物理上与一个经典概率混合是无法区分的，其[相对相位](@entry_id:148120)没有意义。

总结来说，相对相位的概念是量子力学的基石，但它的舞台被[超选择定则](@entry_id:203866)所限制。只有在那些没有被[守恒荷](@entry_id:145660)（如[电荷](@entry_id:275494)、重子数等）的差异所分隔的态之间，[相干叠加](@entry_id:170209)和有意义的相对相位才成为可能，从而展现出量子世界丰富多彩的干涉和动力学行为。