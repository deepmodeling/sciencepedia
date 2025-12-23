## 引言
在量子力学的世界里，一个核心问题是如何将描述微观粒子行为的抽象[波函数](@entry_id:147440)与我们在实验室中实际测量的物理量（如能量、动量或偶极矩）联系起来。这一理论与现实之间的鸿沟正是通过算符、[可观测量](@entry_id:267133)与[期望值](@entry_id:153208)的概念来填补的。这些概念构成了整个[量子化学](@entry_id:140193)的数学基石，然而，其形式化的定义和严格的数学要求常常成为初学者的障碍。本文旨在系统地扫清这些障碍，清晰地揭示这一核心框架的内在逻辑和强大功用。

在接下来的内容中，我们将分三步深入探索。在“原理与机制”一章，我们将建立算符和[期望值](@entry_id:153208)的基本形式体系，阐明其数学属性为何是确保物理实在性的关键。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章，我们将看到这些抽象原理如何化为计算化学家的有力工具，被用来预测[分子能量](@entry_id:190933)、解读[光谱](@entry_id:185632)数据，并与[统计力](@entry_id:194984)学等领域建立联系。最后，通过“动手实践”环节，你将有机会亲自将这些理论应用于具体问题，将知识转化为技能。

让我们首先从构建这一理论大厦的基石——[可观测量](@entry_id:267133)与算符的基本原理及其内在机制——开始。

## 原理与机制

在量子力学的形式体系中，可观测的物理量与数学算符之间存在着深刻的联系。本章旨在系统阐述这些基本原理，从算符的定义到其在预测测量结果中的核心作用，再到这些预测如何随[时间演化](@entry_id:153943)。我们将探讨[量子力学算符](@entry_id:149409)必须满足的严格数学要求，如何构建这些算符，以及如何利用它们计算[期望值](@entry_id:153208)和不确定性，这些都是连接量子理论与实验现实的桥梁。

### 可观测量与算符：量子对应关系

量子力学的一个核心假设是，每一个经典力学中可测量的物理量（例如能量、动量、位置），在量子力学中都对应一个线性**算符**（operator）。对系统进行一次物理测量，其结果必然是该算符的一个**[本征值](@entry_id:154894)**（eigenvalue）。

#### 算符的[厄米性](@entry_id:141899)要求

物理测量的结果必须是实数。为了保证这一点，代表可观测量的[量子算符](@entry_id:137703)必须是**[厄米算符](@entry_id:153410)**（Hermitian operator）。一个算符 $\hat{A}$ 被称为[厄米算符](@entry_id:153410)，如果它等于其自身的**[厄米共轭](@entry_id:191215)**（或称伴随算符） $\hat{A}^\dagger$。在[狄拉克符号](@entry_id:154811)中，对于[希尔伯特空间](@entry_id:261193)中的任意两个态 $|\psi\rangle$ 和 $|\phi\rangle$，[厄米算符](@entry_id:153410)满足如下关系：
$$
\langle \phi | \hat{A} \psi \rangle = \langle \hat{A} \phi | \psi \rangle
$$
从这个定义出发，我们可以证明[厄米算符](@entry_id:153410)的[期望值](@entry_id:153208)总是实数。一个物理量的[期望值](@entry_id:153208) $\langle \hat{A} \rangle$ 是大量重复测量的平均结果，因此它也必须是实数。对于一个处于归一化态 $|\psi\rangle$ 的系统，其[期望值](@entry_id:153208)的定义为 $\langle \hat{A} \rangle = \langle \psi | \hat{A} | \psi \rangle$。为了检验其是否为实数，我们计算它的[复共轭](@entry_id:174690)：
$$
\langle \hat{A} \rangle^* = \langle \psi | \hat{A} | \psi \rangle^* = \langle \hat{A} \psi | \psi \rangle
$$
由于 $\hat{A}$ 是[厄米算符](@entry_id:153410)，我们可以应用其定义，得到 $\langle \hat{A} \psi | \psi \rangle = \langle \psi | \hat{A} | \psi \rangle$。因此，我们证明了：
$$
\langle \hat{A} \rangle^* = \langle \hat{A} \rangle
$$
一个与其[复共轭](@entry_id:174690)相等的数必然是实数。这个特性是算符能够代表物理可观测量的基本前提 。

为了更深刻地理解[厄米性](@entry_id:141899)的重要性，我们可以考察一个非[厄米算符](@entry_id:153410)的例子。考虑一个在环上运动的粒子，其状态由角度 $\phi \in [0, 2\pi]$ 的函数描述。让我们研究算符 $\hat{A} = \frac{d}{d\phi}$。通过[分部积分](@entry_id:136350)可以证明，它的伴随算符是 $\hat{A}^\dagger = -\frac{d}{d\phi} = -\hat{A}$。由于 $\hat{A}^\dagger \neq \hat{A}$，这个算符不是[厄米算符](@entry_id:153410)，而是**反厄米算符**。它的本征方程为 $\frac{d}{d\phi}\psi(\phi) = \lambda \psi(\phi)$，在[周期性边界条件](@entry_id:147809) $\psi(0) = \psi(2\pi)$ 下，其[本征值](@entry_id:154894)为纯虚数 $\lambda_m = im$（其中 $m$ 为整数），对应的本征函数为 $e^{im\phi}$ 。由于[本征值](@entry_id:154894)为虚数，$\hat{A}$ 本身不能代表一个物理可观测量。然而，这恰恰解释了为什么[角动量算符](@entry_id:153013) $\hat{L}_z$ 在位置表示中写作 $-i\hbar \frac{d}{d\phi}$。因子 $-i$ 的引入确保了整个算符是厄米的：$(\hat{L}_z)^\dagger = (-i\hbar \hat{A})^\dagger = (i\hbar) \hat{A}^\dagger = (i\hbar)(-\hat{A}) = -i\hbar\hat{A} = \hat{L}_z$。

#### [量子算符](@entry_id:137703)的构建

构建[量子算符](@entry_id:137703)的通用方法是**对应原理**（correspondence principle）。我们从物理量的经典表达式开始，将其中的位置坐标（如 $x, y, z$）和动量分量（如 $p_x, p_y, p_z$）替换为相应的[量子算符](@entry_id:137703)。在位置表象中，这种替换规则如下：
- 位置算符：$\hat{x} = x$, $\hat{y} = y$, $\hat{z} = z$ （即乘以相应的坐标）
- [动量算符](@entry_id:151743)：$\hat{p}_x = -i\hbar \frac{\partial}{\partial x}$, $\hat{p}_y = -i\hbar \frac{\partial}{\partial y}$, $\hat{p}_z = -i\hbar \frac{\partial}{\partial z}$

让我们以一个具体的例子来说明。考虑一个三维空间中运动的粒子，其沿 $y$ 轴的动能的经典表达式为 $T_y = \frac{p_y^2}{2m}$。为了得到相应的[量子算符](@entry_id:137703) $\hat{T}_y$，我们首先将 $p_y$ 替换为 $\hat{p}_y$：
$$
\hat{T}_y = \frac{\hat{p}_y^2}{2m}
$$
然后，我们将 $\hat{p}_y$ 的具体形式代入，并计算其平方：
$$
\hat{p}_y^2 = \left(-i\hbar \frac{\partial}{\partial y}\right)^2 = (-i\hbar)^2 \frac{\partial^2}{\partial y^2} = -\hbar^2 \frac{\partial^2}{\partial y^2}
$$
因此，沿 $y$ 轴的[动能算符](@entry_id:265633)为 ：
$$
\hat{T}_y = -\frac{\hbar^2}{2m} \frac{\partial^2}{\partial y^2}
$$
这个过程是构建[哈密顿算符](@entry_id:144286)（总能量算符）$\hat{H} = \hat{T} + \hat{V}$ 的基础，其中 $\hat{T}$ 是总[动能算符](@entry_id:265633)，$\hat{V}$ 是[势能](@entry_id:748988)算符。

#### 算符的排序问题

当一个经典可观测量是两个或多个物理量的乘积时，量子化过程会出现一个微妙的问题，即**算符排序问题**（operator ordering problem）。经典物理中，量的乘积是可交换的（例如 $p_x x = x p_x$）。然而，在量子力学中，算符的乘积通常是不可交换的。例如，位置算符 $\hat{x}$ 和[动量算符](@entry_id:151743) $\hat{p}_x$ 的**对易子**（commutator）不为零：$[\hat{x}, \hat{p}_x] = \hat{x}\hat{p}_x - \hat{p}_x\hat{x} = i\hbar$。

考虑一个由两个可观测量 $A$ 和 $B$ 的乘积构成的经典量 $A \times B$。如果对应的算符 $\hat{A}$ 和 $\hat{B}$ 对易（即 $[\hat{A}, \hat{B}]=0$），那么乘积算符 $\hat{A}\hat{B}$ 仍然是厄米的，可以明确地代表这个可观测量。然而，如果 $[\hat{A}, \hat{B}] \neq 0$，情况就变得复杂了。乘积算符 $\hat{A}\hat{B}$ 一般不再是厄米的，因为：
$$
(\hat{A}\hat{B})^\dagger = \hat{B}^\dagger \hat{A}^\dagger = \hat{B}\hat{A}
$$
只有当 $\hat{A}\hat{B} = \hat{B}\hat{A}$ 时，$(\hat{A}\hat{B})^\dagger = \hat{A}\hat{B}$ 才成立。因此，如果算符不对易，$\hat{A}\hat{B}$ 不能作为一个有效的可观测量算符 。

为了解决这个问题，我们需要构建一个厄米的算符组合。最常见的选择是采用**对称化乘积**：
$$
\hat{O}_{AB} = \frac{1}{2}(\hat{A}\hat{B} + \hat{B}\hat{A})
$$
这个组合确保了无论 $\hat{A}$ 和 $\hat{B}$ 是否对易，结果算符总是厄米的。这种对称化方法（也称为外尔对应）是在从经典表述过渡到量子表述时确保物理一致性的标准程序之一 。

### [期望值](@entry_id:153208)：连接理论与测量

一旦我们为[可观测量](@entry_id:267133)建立了算符，下一步就是利用它来做出可与实验比较的预测。在量子力学中，对于一个处于特定状态的系统，单次测量的结果是概率性的。我们能精确预测的是大量重复测量的平均值，这个平均值被称为**[期望值](@entry_id:153208)**（expectation value）。

#### 定义与计算

对于一个处于归一化[量子态](@entry_id:146142) $|\psi\rangle$（即 $\langle \psi | \psi \rangle = 1$）的系统，可观测量 $A$ 的[期望值](@entry_id:153208) $\langle \hat{A} \rangle$ 定义为：
$$
\langle \hat{A} \rangle = \langle \psi | \hat{A} | \psi \rangle
$$
在位置表象中，如果系统的状态由[波函数](@entry_id:147440) $\psi(\vec{r})$ 描述，这个表达式等价于一个积分：
$$
\langle \hat{A} \rangle = \int \psi^*(\vec{r}) \hat{A} \psi(\vec{r}) d\tau
$$
其中积分遍及所有空间。需要强调的是，这个表达式在数学上是良定义的，前提是态 $|\psi\rangle$ 必须位于算符 $\hat{A}$ 的**定义域**（domain）内。如果 $|\psi\rangle$ 不在 $\hat{A}$ 的定义域中，那么 $\hat{A}|\psi\rangle$ 就没有意义，[期望值](@entry_id:153208)也就无法计算。因此，一个算符的完整定义不仅包括其作用规则，还包括其作用的[函数空间](@entry_id:143478) 。

#### 概率诠释与投影算符

[期望值](@entry_id:153208)的概念与量子力学的概率特性密切相关。我们可以通过**投影算符**（projection operator）来揭示这种联系。对于一个归一化的[本征态](@entry_id:149904) $|\psi_n\rangle$，其对应的[投影算符](@entry_id:154142)定义为 $\hat{P}_n = |\psi_n\rangle\langle\psi_n|$。这个算符的作用是将任意态投影到 $|\psi_n\rangle$ 的方向上。

现在，让我们计算一个处于任意归一化态 $|\Phi\rangle$ 的系统，其投影算符 $\hat{P}_n$ 的[期望值](@entry_id:153208) ：
$$
\langle \hat{P}_n \rangle = \langle \Phi | \hat{P}_n | \Phi \rangle = \langle \Phi | (|\psi_n\rangle\langle\psi_n|) | \Phi \rangle
$$
利用[内积](@entry_id:158127)的[结合律](@entry_id:151180)，我们可以重新组合上式：
$$
\langle \hat{P}_n \rangle = (\langle \Phi | \psi_n \rangle) (\langle \psi_n | \Phi \rangle)
$$
由于 $\langle \Phi | \psi_n \rangle = \langle \psi_n | \Phi \rangle^*$，上式可以写为：
$$
\langle \hat{P}_n \rangle = |\langle \psi_n | \Phi \rangle|^2
$$
这个结果具有非凡的物理意义。它表明，[投影算符](@entry_id:154142) $\hat{P}_n$ 的[期望值](@entry_id:153208)，等于在态 $|\Phi\rangle$ 中找到系统处于态 $|\psi_n\rangle$ 的**概率**。这正是量子力学的**玻恩法则**（Born's rule）。因此，[期望值](@entry_id:153208)的计算蕴含了[量子测量](@entry_id:272490)的概率诠释。

#### 不确定性与统计分布

[期望值](@entry_id:153208)描述了测量结果的平均趋势，但它没有告诉我们测量结果的分散程度。这种分散程度由**不确定性**（uncertainty）来量化，其严格定义为测量结果[分布](@entry_id:182848)的标准差，记为 $\Delta A$。

不确定性的平方，即[方差](@entry_id:200758) $(\Delta A)^2$，定义为偏差平方的[期望值](@entry_id:153208)：
$$
(\Delta A)^2 = \langle (\hat{A} - \langle \hat{A} \rangle)^2 \rangle
$$
其中 $\langle \hat{A} \rangle$ 是一个标量。展开平方项并利用[期望值](@entry_id:153208)的线性性质，我们可以得到一个更实用的计算公式 ：
$$
\begin{align}
(\Delta A)^2 = \langle \hat{A}^2 - 2\hat{A}\langle \hat{A} \rangle + \langle \hat{A} \rangle^2 \rangle \\
= \langle \hat{A}^2 \rangle - 2\langle \hat{A} \rangle\langle \hat{A} \rangle + \langle \hat{A} \rangle^2 \\
= \langle \hat{A}^2 \rangle - \langle \hat{A} \rangle^2
\end{align}
$$
因此，不确定性为：
$$
\Delta A = \sqrt{\langle \hat{A}^2 \rangle - \langle \hat{A} \rangle^2}
$$
这个公式是计算任何可观测量不确定性的基础，也是推导著名的[海森堡不确定性原理](@entry_id:171099)的出发点。此外，通过柯西-[施瓦茨不等式](@entry_id:202153)，我们可以得到[期望值](@entry_id:153208)大小的一个上界：$|\langle \psi|\hat{A}|\psi\rangle| \le ||\psi|| \cdot ||\hat{A}\psi||$。对于归一化态 $||\psi||=1$，这简化为 $|\langle \hat{A} \rangle| \le ||\hat{A}\psi||$ 。

### [时间演化](@entry_id:153943)与运动常量

量子系统的[状态和](@entry_id:193625)可观测量的[期望值](@entry_id:153208)通常会随[时间演化](@entry_id:153943)。理解这种演化是[量子动力学](@entry_id:138183)的核心。

#### [定态](@entry_id:137260)

一类特别重要的[量子态](@entry_id:146142)是**[定态](@entry_id:137260)**（stationary state）。[定态](@entry_id:137260)是体系[哈密顿算符](@entry_id:144286) $\hat{H}$ 的本征态，满足本征方程 $\hat{H}|\psi_n\rangle = E_n |\psi_n\rangle$，其中 $E_n$ 是体系的[能量本征值](@entry_id:144381)。

[定态](@entry_id:137260)之所以被称为“[定态](@entry_id:137260)”，是因为对于一个处于定态的系统，任何不显含时间的物理量 $\hat{A}$ 的[期望值](@entry_id:153208)都是恒定不变的。我们可以从两个角度理解这一点 。
首先，从[薛定谔绘景](@entry_id:144112)来看，[定态](@entry_id:137260)的[时间演化](@entry_id:153943)非常简单。如果系统在 $t=0$ 时处于 $|\psi_n\rangle$，那么在任意时刻 $t$，其状态为：
$$
|\psi_n(t)\rangle = e^{-iE_nt/\hbar} |\psi_n(0)\rangle
$$
状态矢量仅仅获得了一个随时间变化的[全局相位](@entry_id:147947)因子。在计算[期望值](@entry_id:153208)时，这个相位因子会被抵消：
$$
\langle \hat{A} \rangle(t) = \langle \psi_n(t) | \hat{A} | \psi_n(t) \rangle = \langle \psi_n(0) | e^{iE_nt/\hbar} \hat{A} e^{-iE_nt/\hbar} | \psi_n(0) \rangle = \langle \psi_n(0) | \hat{A} | \psi_n(0) \rangle = \text{常数}
$$
其次，从[埃伦费斯特定理](@entry_id:151868)（Ehrenfest's theorem）的角度看，对于一个不显含时间的算符 $\hat{A}$，其[期望值](@entry_id:153208)的时间导数为：
$$
\frac{d\langle \hat{A} \rangle}{dt} = \frac{i}{\hbar} \langle [\hat{H}, \hat{A}] \rangle
$$
当系统处于[定态](@entry_id:137260) $|\psi_n\rangle$ 时，对易子的[期望值](@entry_id:153208)为：
$$
\langle \psi_n | [\hat{H}, \hat{A}] | \psi_n \rangle = \langle \psi_n | \hat{H}\hat{A} | \psi_n \rangle - \langle \psi_n | \hat{A}\hat{H} | \psi_n \rangle = E_n \langle \psi_n | \hat{A} | \psi_n \rangle - E_n \langle \psi_n | \hat{A} | \psi_n \rangle = 0
$$
因此，$\frac{d\langle \hat{A} \rangle}{dt} = 0$。值得注意的是，这个结论成立，并不要求 $[\hat{H}, \hat{A}]=0$。只要系统处于[哈密顿算符](@entry_id:144286)的一个本征态，任何可观测量的[期望值](@entry_id:153208)都是恒定的。这个概念可以推广到简并能级：任何处于同一简并能级[子空间](@entry_id:150286)内的态的[线性组合](@entry_id:154743)，其[时间演化](@entry_id:153943)也只携带一个共同的相位因子，因此也是定态 。

#### 运动常量

与[定态](@entry_id:137260)的概念相对应，我们还可以问：在什么条件下，一个[可观测量](@entry_id:267133) $\hat{A}$ 的[期望值](@entry_id:153208)对于*任何*[量子态](@entry_id:146142)（而不仅仅是[定态](@entry_id:137260)）都是恒定不变的？这样的可观测量被称为**运动常量**（constant of motion）或**守恒量**。

从[埃伦费斯特定理](@entry_id:151868) $\frac{d\langle \hat{A} \rangle}{dt} = \frac{i}{\hbar} \langle [\hat{H}, \hat{A}] \rangle$ 可以看出，要使[期望值](@entry_id:153208)的时间导数对任意态都为零，唯一的可能是对易子算符本身为零，即：
$$
[\hat{H}, \hat{A}] = 0
$$
这个条件——算符与[哈密顿算符](@entry_id:144286)对易——是该算符所代表的物理量守恒的充分必要条件。在更普适的[密度矩阵](@entry_id:139892)形式中，这一结论同样成立 。例如，如果体系不受外力矩作用，其[角动量算符](@entry_id:153013)与[哈密顿算符](@entry_id:144286)对易，因此[角动量守恒](@entry_id:156798)。

#### 时间演化的绘景

描述量子动力学存在多种等价的数学框架，或称“绘景”。最常用的是**[薛定谔绘景](@entry_id:144112)**（Schrödinger picture）和**[海森堡绘景](@entry_id:141162)**（Heisenberg picture）。
- 在**[薛定谔绘景](@entry_id:144112)**中，系统的状态矢量 $|\psi_S(t)\rangle$ 随时间演化（$|\psi_S(t)\rangle = U(t)|\psi(0)\rangle$，其中 $U(t)$ 是[时间演化算符](@entry_id:196774)），而算符 $\hat{A}_S$ 通常是固定的。
- 在**[海森堡绘景](@entry_id:141162)**中，状态矢量 $|\psi_H\rangle$ 固定为其初始状态 $|\psi(0)\rangle$，而算符 $\hat{A}_H(t)$ 则随[时间演化](@entry_id:153943)，其演化规则为 $\hat{A}_H(t) = U^\dagger(t) \hat{A}_S U(t)$。

这两种绘景只是描述同一物理实在的不同方式，所有可测量的物理预言必须在两种绘景中完全相同。例如，[期望值](@entry_id:153208)在[海森堡绘景](@entry_id:141162)中计算为：
$$
\langle \hat{A} \rangle_H(t) = \langle \psi_H | \hat{A}_H(t) | \psi_H \rangle = \langle \psi(0) | U^\dagger(t) \hat{A}_S U(t) | \psi(0) \rangle = \langle \psi_S(t) | \hat{A}_S | \psi_S(t) \rangle = \langle \hat{A} \rangle_S(t)
$$
可见，计算结果与绘景的选择无关。同样地，[方差](@entry_id:200758) $(\Delta A)^2 = \langle A^2 \rangle - \langle A \rangle^2$ 以及不确定性 $\Delta A$ 也都是与绘景无关的。进一步地，连[不确定性原理](@entry_id:141278)本身也与绘景无关。这是因为算符之间的对易关系也以一种协变的方式进行变换：$[\hat{A}_H(t), \hat{B}_H(t)] = U^\dagger(t)[\hat{A}_S, \hat{B}_S]U(t)$。因此，[不确定性关系](@entry_id:186128)的下限 $\frac{1}{2}|\langle[\hat{A},\hat{B}]\rangle|$ 在所有绘景中都保持不变 。

### 深入探讨：自伴算符的严格性

在入门级的量子力学课程中，“[厄米算符](@entry_id:153410)”和“自伴算符”通常被当作同义词。然而，在更严格的数学物理中，尤其是在处理像位置和动量这样定义域不是整个希尔伯特空间的**无界算符**时，区分**对称算符**（symmetric operator）和**自伴算符**（self-adjoint operator）至关重要。

一个算符 $\hat{A}$ 是对称的，如果对于其定义域 $\mathcal{D}(\hat{A})$ 内的所有 $|\psi\rangle$ 和 $|\phi\rangle$，都有 $\langle \phi | \hat{A} \psi \rangle = \langle \hat{A} \phi | \psi \rangle$。这等价于说，$\hat{A}$ 的作用包含于其伴随算符 $\hat{A}^\dagger$ 的作用中（$\hat{A} \subset \hat{A}^\dagger$）。而一个算符是自伴的，则要求更为严格：它不仅要是对称的，而且其定义域必须与其伴随算符的定义域完全相同，即 $\hat{A} = \hat{A}^\dagger$ 且 $\mathcal{D}(\hat{A}) = \mathcal{D}(\hat{A}^\dagger)$ 。

为什么物理可观测量必须由自伴算符而不是仅仅对称的算符来表示？这背后有深刻的物理和数学原因 。

1.  **谱定理的唯一性**：[量子测量](@entry_id:272490)的概率解释（玻恩法则）在数学上由**谱定理**（Spectral Theorem）支撑。该定理将算符与其对应的**投影值测量**（Projection-Valued Measure, PVM）联系起来，PVM 本质上是对算符本征谱的推广。关键在于，只有自伴算符才能保证在[实数轴](@entry_id:147286)上存在一个**唯一**的PVM。一个仅仅对称但非自伴的算符，可能没有[自伴扩张](@entry_id:264525)（因而无法定义一个物理上完备的测量过程），或者可能存在多个不同的[自伴扩张](@entry_id:264525)。每一个扩张都对应一个不同的[物理可观测量](@entry_id:154692)，具有不同的本征谱和动力学行为。因此，为了避免物理上的模糊性，我们必须要求算符是自伴的。

2.  **[酉演化](@entry_id:145020)的生成元**：根据**[斯通定理](@entry_id:262301)**（Stone's Theorem），任何连续的[酉变换](@entry_id:152599)群（如[时间演化](@entry_id:153943) $U(t) = e^{-i\hat{H}t/\hbar}$ 或空间平移 $T(x) = e^{-i\hat{p}x/\hbar}$）都有一个唯一的自伴**无穷小生成元**（infinitesimal generator）。例如，[哈密顿算符](@entry_id:144286) $\hat{H}$ 是[时间演化](@entry_id:153943)的生成元，动量算符 $\hat{p}$ 是空间平移的生成元。[酉变换](@entry_id:152599)是保持[量子态](@entry_id:146142)范数和[内积](@entry_id:158127)不变的变换，这对于[概率守恒](@entry_id:149166)至关重要。如果[哈密顿量](@entry_id:172864)仅仅是对称的而非自伴的，那么 $e^{-i\hat{H}t/\hbar}$ 就不能保证在所有时间 $t$ 都构成一个[酉群](@entry_id:138602)，这将导致概率不守恒等灾难性的物理后果。因此，要求[可观测量](@entry_id:267133)（特别是那些作为动力学或对称性生成元的量）是自伴的，是确保[量子理论](@entry_id:145435)内部逻辑自洽性的根本要求。

总之，从构建基本算符到预测其测量值的[统计分布](@entry_id:182030)和时间演化，算符、[可观测量](@entry_id:267133)和[期望值](@entry_id:153208)的概念构成了[计算化学](@entry_id:143039)和量子物理的理论基石。对这些原理的精确理解，特别是[厄米性](@entry_id:141899)和自伴性的严格要求，是应用量子力学解决实际化学问题的前提。