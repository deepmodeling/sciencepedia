## 引言
在量子力学的世界里，物理系统的状态由[希尔伯特空间](@entry_id:261193)中抽象的态矢量来描述。然而，为了将这些数学实体与可测量的物理现实联系起来，我们需要一个强大的工具来量化不同状态之间的关系、相似性与可区分性。[内积](@entry_id:158127)与正交性正是扮演这一关键角色的数学支柱，它们是将抽象的[量子理论](@entry_id:145435)转化为具体预测和计算的桥梁。

本文旨在解决一个核心问题：我们如何利用[内积](@entry_id:158127)这一概念，为量子[态的叠加](@entry_id:273993)、测量和演化建立一个坚实且自洽的数学框架？缺乏对[内积](@entry_id:158127)和正交性的深刻理解，量子力学的许多基本公理，如波恩诠释和算符的性质，将变得难以捉摸。

为了系统地构建这一理解，本文将分三步展开。首先，在“原理与机制”一章中，我们将深入探讨[内积](@entry_id:158127)的定义、[狄拉克符号](@entry_id:154811)的运用，并阐明正交性与归一化如何共同构成描述[量子态](@entry_id:146142)的“[坐标系](@entry_id:156346)”。接着，在“应用与跨学科联系”一章中，我们将展示这些概念如何从解释原子轨道的[基本对称性](@entry_id:161256)，延伸到驱动现代[量子化学](@entry_id:140193)计算、[数值分析](@entry_id:142637)乃至数据科学的核心算法。最后，通过“动手实践”部分，您将有机会运用所学知识解决具体的[量子化学](@entry_id:140193)问题，从而巩固和深化您的理解。让我们首先从构建这个理论框架的基础——[内积](@entry_id:158127)的原理与机制开始。

## 原理与机制

在量子力学的数学框架中，系统的状态由[希尔伯特空间](@entry_id:261193)中的矢量来描述。为了从这些抽象的矢量中提取[可观测量](@entry_id:267133)和概率等物理信息，我们需要一个定义明确的数学工具来衡量不同状态矢量之间的关系。这个工具就是**[内积](@entry_id:158127)**（inner product）。本章将深入探讨[内积](@entry_id:158127)的定义、性质及其在构建量子理论中的核心作用，特别是**正交性**（orthogonality）和**归一化**（normalization）的概念。

### 量子力学中的[内积](@entry_id:158127)

在量子力学中，我们使用由 Paul Dirac 引入的优雅的**[狄拉克符号](@entry_id:154811)**（Dirac notation）或称**bra-ket符号**来表示[量子态](@entry_id:146142)及其相互关系。一个[量子态](@entry_id:146142)被表示为一个**[右矢](@entry_id:152965)**（ket） $|\psi\rangle$。每个[右矢](@entry_id:152965)都有一个与之对应的**左矢**（bra），记作 $\langle\psi|$，它是[右矢](@entry_id:152965)的[厄米共轭](@entry_id:191215)（Hermitian conjugate）。

左矢和[右矢](@entry_id:152965)的组合，形如 $\langle\phi|\psi\rangle$，便构成了一个**[内积](@entry_id:158127)**。这个[内积](@entry_id:158127)是一个复数，它编码了 $|\psi\rangle$ 态在 $|\phi\rangle$ 态上的投影信息。我们可以将其视为矢量[点积](@entry_id:149019)在复矢量空间中的推广。[内积](@entry_id:158127)具有以下基本性质：

1.  **[共轭对称性](@entry_id:144131)**（Conjugate symmetry）：$\langle\phi|\psi\rangle = (\langle\psi|\phi\rangle)^*$，其中 $*$ 表示[复共轭](@entry_id:174690)。
2.  **对[右矢](@entry_id:152965)的线性**（Linearity in the ket）：$\langle\phi| (c_1|\psi_1\rangle + c_2|\psi_2\rangle) = c_1\langle\phi|\psi_1\rangle + c_2\langle\phi|\psi_2\rangle$。
3.  **对左矢的[反线性](@entry_id:268590)**（Antilinearity in the bra）：$\langle(c_1\phi_1 + c_2\phi_2)| \psi\rangle = c_1^*\langle\phi_1|\psi\rangle + c_2^*\langle\phi_2|\psi\rangle$。
4.  **正定性**（Positive-definiteness）：一个态与自身的[内积](@entry_id:158127)，即其范数（norm）的平方，是实数且非负：$\langle\psi|\psi\rangle \ge 0$。只有对于[零矢量](@entry_id:155273)，$\langle\psi|\psi\rangle$ 才为零。

当[量子态](@entry_id:146142)用连续的[波函数](@entry_id:147440)（如位置空间中的 $\psi(x)$）表示时，[内积](@entry_id:158127)通常定义为积分形式。对于一维系统，两个态 $|\phi\rangle$ 和 $|\psi\rangle$（分别对应[波函数](@entry_id:147440) $\phi(x)$ 和 $\psi(x)$）的[内积](@entry_id:158127)为：
$$
\langle\phi|\psi\rangle = \int_{-\infty}^{\infty} \phi^*(x) \psi(x) dx
$$
这里 $\phi^*(x)$ 是 $\phi(x)$ 的[复共轭](@entry_id:174690)。这个积分遍及所有可能的空间。

### 正交性与归一化：构建量子[坐标系](@entry_id:156346)

[内积](@entry_id:158127)的两个最重要应用是定义态的归一化和态间的正交性。这两个概念共同构成了**正交归一性**（orthonormality），它是构建任何量子力学计算框架的基石。

#### 归一化

根据量子力学的波恩诠释（Born rule），$|\psi(x)|^2 dx$ 代表了在位置 $x$ 到 $x+dx$ 区间内发现粒子的概率。因此，在全空间中找到粒子的总概率必须为 1。这要求态矢量必须被**归一化**（normalized），即其与自身的[内积](@entry_id:158127)必须等于 1：
$$
\langle\psi|\psi\rangle = \int \psi^*(x) \psi(x) dx = 1
$$
一个满足此条件的态称为归一化态。

在实际应用中，我们常常将一个任意态 $|\psi\rangle$ 表示为一组[基态](@entry_id:150928) $|\phi_n\rangle$ 的线性组合：$|\psi\rangle = \sum_n c_n |\phi_n\rangle$。如果[基态](@entry_id:150928)是正交归一的，那么[归一化条件](@entry_id:156486) $\langle\psi|\psi\rangle=1$ 会对展开系数 $c_n$ 施加一个重要约束。例如，考虑一个由两个正交归一[基态](@entry_id:150928) $|\phi_1\rangle$ 和 $|\phi_2\rangle$ 构成的系统中，一个态被描述为 $|\psi\rangle = c_1 |\phi_1\rangle + c_2 |\phi_2\rangle$。其[归一化条件](@entry_id:156486)计算如下：
$$
\langle\psi|\psi\rangle = \langle(c_1\phi_1 + c_2\phi_2)|(c_1\phi_1 + c_2\phi_2)\rangle = |c_1|^2\langle\phi_1|\phi_1\rangle + |c_2|^2\langle\phi_2|\phi_2\rangle + c_1^*c_2\langle\phi_1|\phi_2\rangle + c_2^*c_1\langle\phi_2|\phi_1\rangle
$$
由于[基态](@entry_id:150928)是正交归一的（$\langle\phi_i|\phi_j\rangle = \delta_{ij}$），交叉项为零，对角项为 1。因此，[归一化条件](@entry_id:156486)简化为：
$$
|c_1|^2 + |c_2|^2 = 1
$$
这个结果具有深刻的物理意义：$|c_n|^2$ 是在测量中发现系统处于 $|\phi_n\rangle$ 态的概率，所有这些[互斥事件](@entry_id:265118)的概率之和必须为 1。[@problem_id:1374326]

#### 正交性

如果两个不同的[量子态](@entry_id:146142) $|\psi\rangle$ 和 $|\phi\rangle$ 的[内积](@entry_id:158127)为零，我们称它们是**正交的**（orthogonal）：
$$
\langle\psi|\phi\rangle = 0
$$
正交性在量子意义上表示这两个态是完全“可区分”或“[互斥](@entry_id:752349)”的。如果一个系统处于 $|\psi\rangle$ 态，那么测量其是否处于与之正交的 $|\phi\rangle$ 态的概率将为零。

我们可以利用[正交性条件](@entry_id:168905)来确定描述[量子态](@entry_id:146142)的未知参数。例如，在一个由三个正交归一[基矢](@entry_id:199546) $\{|e_1\rangle, |e_2\rangle, |e_3\rangle\}$ 张成的希尔伯特空间中，考虑两个态：
$$
|\psi\rangle = i|e_1\rangle + |e_2\rangle + |e_3\rangle
$$
$$
|\phi(\alpha)\rangle = 3|e_1\rangle + i\alpha|e_2\rangle + 5i|e_3\rangle
$$
其中 $\alpha$ 是一个实数。要使这两个态正交，它们的[内积](@entry_id:158127)必须为零。为此，我们首先求出 $|\psi\rangle$ 对应的左矢 $\langle\psi|$，通过对其系数进行[复共轭](@entry_id:174690)得到 $\langle\psi| = -i\langle e_1| + \langle e_2| + \langle e_3|$。然后计算[内积](@entry_id:158127)：
$$
\langle\psi|\phi(\alpha)\rangle = (-i)(3)\langle e_1|e_1\rangle + (1)(i\alpha)\langle e_2|e_2\rangle + (1)(5i)\langle e_3|e_3\rangle
$$
利用[基矢](@entry_id:199546)的正交归一性 $\langle e_i|e_j\rangle = \delta_{ij}$，上式简化为：
$$
\langle\psi|\phi(\alpha)\rangle = -3i + i\alpha + 5i = i(\alpha + 2)
$$
令此[内积](@entry_id:158127)为零，即 $i(\alpha+2)=0$，我们得到 $\alpha = -2$。这个结果表明，只有当参数 $\alpha$ 取特定值时，这两个态才在量子力学意义上[相互独立](@entry_id:273670)。[@problem_id:1374314]

#### 正交归一[基组](@entry_id:160309)

在实践中，使用一套**正交归一的**（orthonormal）[基函数](@entry_id:170178)或[基矢](@entry_id:199546)来描述系统极为方便。一个[基组](@entry_id:160309) $\{\phi_n\}$ 若满足以下条件，则称其为正交归一的：
$$
\langle\phi_n|\phi_m\rangle = \delta_{nm}
$$
这里的 $\delta_{nm}$ 是**[克罗内克δ函数](@entry_id:272741)**（Kronecker delta），当 $n=m$ 时其值为 1（归一化），当 $n \neq m$ 时其值为 0（正交性）。

例如，考虑在区间 $[0, 2]$ 上的两个实值函数 $\psi_1(x) = A$ 和 $\psi_2(x) = B(x-1)$。为了使它们构成一个正交归一集，我们必须同时满足正交性和[归一化条件](@entry_id:156486)。
首先，检验正交性：
$$
\langle\psi_1|\psi_2\rangle = \int_0^2 A \cdot B(x-1) dx = AB \left[ \frac{x^2}{2} - x \right]_0^2 = AB(2-2) = 0
$$
可见，这两个函数对于任意常数 $A$ 和 $B$ 都是正交的。
接下来，我们施加[归一化条件](@entry_id:156486)。对于 $\psi_1(x)$：
$$
\langle\psi_1|\psi_1\rangle = \int_0^2 A^2 dx = 2A^2 = 1 \implies A = \frac{1}{\sqrt{2}}
$$
对于 $\psi_2(x)$：
$$
\langle\psi_2|\psi_2\rangle = \int_0^2 B^2(x-1)^2 dx = B^2 \left[ \frac{(x-1)^3}{3} \right]_0^2 = B^2 \left(\frac{1}{3} - (-\frac{1}{3})\right) = \frac{2B^2}{3} = 1 \implies B = \sqrt{\frac{3}{2}}
$$
通过强制执行正交归一条件，我们唯一地确定了这两个[基函数](@entry_id:170178)的归一化常数。[@problem_id:1374295]

### [内积](@entry_id:158127)的应用

[内积](@entry_id:158127)是量子力学计算的“瑞士军刀”，它被用于计算概率幅、[期望值](@entry_id:153208)以及各种矩阵元。

#### 投影与展开系数

如果一个完备的正交归一[基组](@entry_id:160309) $\{|\phi_n\rangle\}$ 已知，那么[希尔伯特空间](@entry_id:261193)中的任何态 $|\psi\rangle$ 都可以唯一地表示为这些[基矢](@entry_id:199546)的[线性组合](@entry_id:154743)：
$$
|\psi\rangle = \sum_n c_n |\phi_n\rangle
$$
其中 $c_n$ 是复数展开系数。[内积](@entry_id:158127)提供了一种计算这些系数的直接方法。我们将上式两边与某个特定的[基矢](@entry_id:199546) $\langle\phi_m|$ 作[内积](@entry_id:158127)：
$$
\langle\phi_m|\psi\rangle = \langle\phi_m| \left( \sum_n c_n |\phi_n\rangle \right) = \sum_n c_n \langle\phi_m|\phi_n\rangle
$$
利用[基组](@entry_id:160309)的正交归一性 $\langle\phi_m|\phi_n\rangle = \delta_{mn}$，右边的求和中只有 $n=m$ 的项存活下来：
$$
\langle\phi_m|\psi\rangle = \sum_n c_n \delta_{mn} = c_m
$$
因此，展开系数 $c_m$ 就是态 $|\psi\rangle$ 在[基矢](@entry_id:199546) $|\phi_m\rangle$ 上的**投影**（projection）。这个过程类似于在经典力学中通过[点积](@entry_id:149019)求一个矢量在某个坐标轴上的分量。

例如，要确定一个任意的试探波函数 $\psi_{trial}(x)$ 中包含了多少“成分”的[基态](@entry_id:150928) $\phi_1(x)$，我们只需计算它们的[内积](@entry_id:158127) $c_1 = \langle\phi_1|\psi_{trial}\rangle$。对于一个被限制在 $x \in [0, L]$ 区域内的粒子，其[基态](@entry_id:150928)为 $\phi_1(x) = \sqrt{\frac{2}{L}} \sin(\frac{\pi x}{L})$。如果我们使用一个抛物线形的[试探函数](@entry_id:756165) $\psi_{trial}(x) = N x (L-x)$，那么[基态](@entry_id:150928)的贡献由以下积分给出：
$$
c_1 = \int_0^L \phi_1^*(x) \psi_{trial}(x) dx = \int_0^L \left( \sqrt{\frac{2}{L}} \sin\left(\frac{\pi x}{L}\right) \right) (N x(L-x)) dx
$$
通过计算这个积分，我们就能量化[试探函数](@entry_id:756165)与真实[基态](@entry_id:150928)的“相似度”。[@problem_id:1374292]

#### [期望值](@entry_id:153208)

[内积](@entry_id:158127)是计算物理可观测量平均值（即**[期望值](@entry_id:153208)**）的核心。对于一个由算符 $\hat{A}$ 代表的[可观测量](@entry_id:267133)，在态 $|\Psi\rangle$ 中的[期望值](@entry_id:153208)由下式给出：
$$
\langle A \rangle = \langle\Psi|\hat{A}|\Psi\rangle = \int \Psi^*(x) \hat{A} \Psi(x) dx
$$
如果态 $|\Psi\rangle$ 是一个叠加态，例如 $|\Psi\rangle = c_1|\psi_1\rangle + c_2|\psi_2\rangle$，其中 $|\psi_1\rangle$ 和 $|\psi_2\rangle$ 是正交归一的[基态](@entry_id:150928)，那么[期望值](@entry_id:153208)的计算会展开为：
$$
\langle A \rangle = |c_1|^2 \langle\psi_1|\hat{A}|\psi_1\rangle + |c_2|^2 \langle\psi_2|\hat{A}|\psi_2\rangle + c_1^*c_2 \langle\psi_1|\hat{A}|\psi_2\rangle + c_2^*c_1 \langle\psi_2|\hat{A}|\psi_1\rangle
$$
这个表达式揭示了[期望值](@entry_id:153208)的构成：它不仅包含每个[基态](@entry_id:150928)自身的[期望值](@entry_id:153208)（对角项，如 $\langle\psi_1|\hat{A}|\psi_1\rangle$），还包含不同[基态](@entry_id:150928)之间的**干涉项**（非对角项，如 $\langle\psi_1|\hat{A}|\psi_2\rangle$）。这些非对角项，也称为**矩阵元**，是量子干涉效应的数学体现。例如，对于一个处于叠加态 $\Psi(x) = \frac{1}{\sqrt{5}} \psi_1(x) + \frac{2}{\sqrt{5}} \psi_2(x)$ 的一维[箱中粒子](@entry_id:140940)，其[位置期望值](@entry_id:171721) $\langle x \rangle$ 的计算就必须包含对角矩阵元 $\langle\psi_1|\hat{x}|\psi_1\rangle$、$\langle\psi_2|\hat{x}|\psi_2\rangle$ 和非[对角矩阵](@entry_id:637782)元 $\langle\psi_1|\hat{x}|\psi_2\rangle$。[@problem_id:1374282]

#### 对称性的利用

在计算[内积](@entry_id:158127)（特别是积分形式）时，利用函数的对称性可以极大地简化工作。一个关键的法则是：**在一个对称区间（如 $[-L, L]$）上，任何奇函数（odd function, $f(-x)=-f(x)$）的积分都为零。**

这个性质源于奇函数在原点两侧的贡献相互抵消。由此可以推导出更广泛的规则：
*   奇函数 $\times$ 奇函数 = 偶函数
*   偶函数 $\times$ 偶函数 = [偶函数](@entry_id:163605)
*   奇函数 $\times$ 偶函数 = [奇函数](@entry_id:173259)

因此，在一个对称区间上，任意[偶函数](@entry_id:163605)与任意奇函数的[内积](@entry_id:158127)必定为零，因为它们的乘积是一个[奇函数](@entry_id:173259)。例如，考虑在区间 $[-\pi, \pi]$ 上的两个函数 $\Psi_A(x) = N_A(1+x)$ 和 $\Psi_B(x) = N_B(\cos(x)+\sin(x))$。它们的[内积](@entry_id:158127)包含四个积分项：
$$
\langle \Psi_A|\Psi_B\rangle \propto \int_{-\pi}^{\pi} (\cos x + \sin x + x\cos x + x\sin x) dx
$$
在这里，$\sin x$ 和 $x\cos x$ 都是奇函数，因此它们在 $[-\pi, \pi]$ 上的积分为零。我们只需计算[偶函数](@entry_id:163605)部分 $\cos x$ 和 $x\sin x$ 的积分，从而大大简化了计算。[@problem_id:1374329]

### [内积](@entry_id:158127)与厄米算符

[内积](@entry_id:158127)与代表[物理可观测量](@entry_id:154692)的**[厄米算符](@entry_id:153410)**（Hermitian operators）之间存在着深刻的联系。

#### [厄米算符](@entry_id:153410)的定义

一个算符 $\hat{A}$ 被称为厄米算符，如果对于其定义域内的任意两个态 $|\phi\rangle$ 和 $|\psi\rangle$，它都满足以下条件：
$$
\langle\phi|\hat{A}|\psi\rangle = \langle\hat{A}\phi|\psi\rangle
$$
这个定义意味着算符 $\hat{A}$ 可以“作用”在[右矢](@entry_id:152965)上，也可以将其“[厄米共轭](@entry_id:191215)” $\hat{A}^\dagger$（对于厄米算符，$\hat{A}^\dagger = \hat{A}$）作用在左矢上，而[内积](@entry_id:158127)的结果不变。用积分形式表达，这个条件等价于：
$$
\int f^*(x) [\hat{A} g(x)] dx = \int [\hat{A} f(x)]^* g(x) dx
$$
这个性质保证了[厄米算符](@entry_id:153410)的[本征值](@entry_id:154894)为实数，这与[物理可观测量](@entry_id:154692)必须是实数的要求相符。[@problem_id:1374296]

#### [厄米算符](@entry_id:153410)[本征函数的正交性](@entry_id:150712)

厄米算符的一个至关重要的特性是：**属于不同[本征值](@entry_id:154894)的本征函数必定相互正交。**
这是一个可以严格证明的定理，它构成了量子力学的基本公理之一。这个定理在实践中非常有用。如果我们知道两个函数是同一个[厄米算符](@entry_id:153410)（如[哈密顿算符](@entry_id:144286)）的[本征函数](@entry_id:154705)，并且它们对应的能量（[本征值](@entry_id:154894)）不同，那么我们无需计算就可以断定它们的[内积](@entry_id:158127)为零。

例如，假设已知两个函数 $\psi_A(x)$ 和 $\psi_B(x)$ 是某个一维[哈密顿算符](@entry_id:144286)的非简并（即[本征值](@entry_id:154894)不同）的[本征函数](@entry_id:154705)。那么我们就可以直接使用正交条件 $\int_0^L \psi_A(x) \psi_B(x) dx = 0$ 来求解函数形式中的未知参数，而无需知道[哈密顿算符](@entry_id:144286)的具体形式。[@problem_id:1374301]

### 高级主题与推广

#### [完备性关系](@entry_id:139077)与[Parseval定理](@entry_id:139215)

一个正交归一[基组](@entry_id:160309) $\{|\phi_n\rangle\}$ 如果是**完备的**（complete），意味着[希尔伯特空间](@entry_id:261193)中的任何矢量都可以用它来展开。完备性可以用一个称为**[完备性关系](@entry_id:139077)**或**闭合关系**的优美公式来表示：
$$
\sum_n |\phi_n\rangle\langle\phi_n| = \hat{I}
$$
这里，$\hat{I}$ 是单位算符。表达式 $|\phi_n\rangle\langle\phi_n|$ 是一个**[外积](@entry_id:147029)**（outer product），它是一个算符（投影算符）。[完备性关系](@entry_id:139077)表明，将一个态投影到所有[基矢](@entry_id:199546)上再将这些投影加起来，就等于恢复了原态本身。

这个关系有一个重要的推论，即**[Parseval定理](@entry_id:139215)**。一个态的范数平方 $\langle\Psi|\Psi\rangle$ 可以用它在任意一个完备正交归一[基组](@entry_id:160309)中的展开系数来表示：
$$
\langle\Psi|\Psi\rangle = \langle\Psi|\hat{I}|\Psi\rangle = \langle\Psi| \left( \sum_n |\phi_n\rangle\langle\phi_n| \right) |\Psi\rangle = \sum_n \langle\Psi|\phi_n\rangle\langle\phi_n|\Psi\rangle = \sum_n |c_n|^2
$$
这个定理表明，态矢量的“长度”的平方等于其在所有“坐标轴”上分量平方和，这与我们熟悉的欧几里得空间中的毕达哥拉斯定理（勾股定理）异曲同工。这也意味着，无论我们选择哪一套完备正交归一[基组](@entry_id:160309)来计算，一个态的范数都是不变的。[@problem_id:1374332]

#### [非正交基组](@entry_id:190211)与[重叠矩阵](@entry_id:268881)

在[量子化学](@entry_id:140193)的实际计算中，例如在分子[轨道](@entry_id:137151)的[原子轨道线性组合](@entry_id:151829)（LCAO）方法中，我们选择的[基函数](@entry_id:170178)（通常是原子轨道）往往不是正交的。例如，放置在不同原子上的原子轨道在空间中有重叠，它们的[内积](@entry_id:158127)不为零。

在这种情况下，我们需要引入**[重叠矩阵](@entry_id:268881)**（overlap matrix） $\mathbf{S}$，其[矩阵元](@entry_id:186505)定义为[基函数](@entry_id:170178)间的[内积](@entry_id:158127)：
$$
S_{ik} = \langle\phi_i|\phi_k\rangle
$$
虽然[原子轨道](@entry_id:140819)[基组](@entry_id:160309) $\{\phi_i\}$ 非正交，但我们最终构建的分子[轨道](@entry_id:137151) $\{\psi_j\}$ 必须是正交归一的，即 $\langle\psi_j|\psi_k\rangle = \delta_{jk}$。将LCAO展开式 $\psi_j = \sum_i c_{ij}\phi_i$ 代入这个条件，我们得到：
$$
\langle\psi_j|\psi_k\rangle = \left\langle \sum_i c_{ij}\phi_i \middle| \sum_l c_{lk}\phi_l \right\rangle = \sum_{i,l} c_{ij}^* c_{lk} \langle\phi_i|\phi_l\rangle = \sum_{i,l} c_{ij}^* S_{il} c_{lk} = \delta_{jk}
$$
这个方程可以用矩阵形式简洁地写为：
$$
\mathbf{C}^\dagger \mathbf{S} \mathbf{C} = \mathbf{I}
$$
其中 $\mathbf{C}$ 是由系数 $c_{ij}$ 构成的矩阵，$\mathbf{C}^\dagger$ 是其共轭转置，$\mathbf{I}$ 是单位矩阵。这个广义的正交[归一化条件](@entry_id:156486)是所有基于[非正交基组](@entry_id:190211)的[量子化学](@entry_id:140193)计算方法的核心。[@problem_id:1374289]

#### 连续谱与[狄拉克δ函数](@entry_id:153299)归一化

我们至今讨论的归一化主要针对束缚态，它们的[波函数](@entry_id:147440)在无穷远处趋于零，使得 $\int |\psi|^2 dx$ 是一个有限值。然而，对于能量为正的非束缚态（或[散射态](@entry_id:150968)），例如自由粒子的平面波 $\psi_k(x) = A e^{ikx}$，[波函数](@entry_id:147440)在整个空间中[振荡](@entry_id:267781)而不衰减，导致其范数积分发散。

对于这类构成**连续谱**的态，我们采用一种不同的归一化方案，即**[狄拉克δ函数](@entry_id:153299)归一化**：
$$
\langle\psi_{k'}|\psi_k\rangle = \int_{-\infty}^{\infty} \psi_{k'}^*(x) \psi_k(x) dx = \delta(k - k')
$$
这里的 $\delta(k-k')$ 是**狄拉克δ函数**，它是一个在 $k=k'$ 时为无穷大、在其他地方为零且全域积分为 1 的[广义函数](@entry_id:182848)。这种归一化方案保留了正交性（当 $k \neq k'$ 时[内积](@entry_id:158127)为零），但将[归一化条件](@entry_id:156486)从 1 替换为了一个δ函数。

当一个物理上可实现的、可归一化的[波包](@entry_id:154698) $|\Psi\rangle$ 由这些[连续谱](@entry_id:155477)的[基态](@entry_id:150928)叠加而成时，求和就变成了积分：
$$
|\Psi\rangle = \int g(k) |\psi_k\rangle dk
$$
其中 $g(k)$ 是叠加系数函数。此时，[波包](@entry_id:154698)的[归一化条件](@entry_id:156486) $\langle\Psi|\Psi\rangle=1$ 会转化为对系数函数的约束：
$$
\langle\Psi|\Psi\rangle = \iint g^*(k')g(k) \langle\psi_{k'}|\psi_k\rangle dk' dk = \iint g^*(k')g(k) \delta(k-k') dk' dk = \int |g(k)|^2 dk = 1
$$
这个结果表明，对于[连续谱](@entry_id:155477)，$|g(k)|^2$ 扮演了概率密度的角色，其在整个 $k$ 空间（[动量空间](@entry_id:148936)）的积分必须为 1。[@problem_id:1374291]