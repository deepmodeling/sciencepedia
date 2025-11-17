## 引言
在动力系统的研究中，我们常常面对形如 $\mathbf{x}'(t) = A(t)\mathbf{x}(t)$ 的[线性微分方程组](@entry_id:155297)，它描述了从物理[振动](@entry_id:267781)到种群动态等众多现象的演化。仅仅找到一个特解是不够的，我们的目标是掌握系统的完整行为，即找到一个能够描述所有可能初始状态的通解。然而，如何系统地构建并表达这个通解，从而揭示系统内在的结构与行为模式，是一个核心的理论挑战。

本文旨在深入探讨解决这一问题的关键工具——[基本矩阵](@entry_id:275638)解。这一强大的数学概念不仅统一了线性系统的求解方法，还为理解系统的几何与定性行为提供了深刻的洞见。通过本文的学习，您将掌握：

- **第一章：原理与机制**，将详细介绍[基本矩阵](@entry_id:275638)的定义、充要条件及其关键性质。我们将探索朗斯基行列式如何检验解的[线性无关](@entry_id:148207)性，并通过[刘维尔公式](@entry_id:267034)揭示其深刻的内在规律。此外，本章还将引出[状态转移矩阵](@entry_id:269075)和矩阵指数这两个核心概念，它们是分析和[求解线性系统](@entry_id:146035)的基石。

- **第二章：应用与[交叉](@entry_id:147634)学科联系**，将展示[基本矩阵](@entry_id:275638)理论如何跨越学科界限，应用于经典力学、[电路分析](@entry_id:261116)、控制理论和[几何分析](@entry_id:157700)等多个领域。您将看到，这一抽象的数学工具如何具体地描述[机械振动](@entry_id:167420)、电路响应以及相空间中轨迹的演化。

- **第三章：动手实践**，将通过一系列精心设计的计算练习，引导您亲手构建[基本矩阵](@entry_id:275638)，处理具有不同实[特征值](@entry_id:154894)、[共轭复特征值](@entry_id:152797)和重根[特征值](@entry_id:154894)的系统，从而将理论知识转化为解决实际问题的能力。

本文将带领您从基本定义出发，逐步深入其理论核心与广泛应用，最终让您能够自信地运用[基本矩阵](@entry_id:275638)来分析和解决各类[线性动力系统](@entry_id:150282)问题。

## 原理与机制

在研究形如 $\mathbf{x}'(t) = A(t)\mathbf{x}(t)$ 的[线性动力系统](@entry_id:150282)时，我们不仅关心寻找单个特解，更希望能够描述系统的完整行为，即找到能够涵盖所有可能初始状态的通解。[基本矩阵](@entry_id:275638)（Fundamental Matrix）正是实现这一目标的核心理论工具。它将系统的多个[线性无关解](@entry_id:185441)整合为一个统一的矩阵形式，从而为分析和[求解线性系统](@entry_id:146035)提供了强大的框架。

### [基本矩阵](@entry_id:275638)的定义与条件

对于一个 $n$ 维[线性齐次微分方程](@entry_id:165420)组 $\mathbf{x}' = A(t)\mathbf{x}$，其解空间构成一个 $n$ 维[线性空间](@entry_id:151108)。这意味着我们可以找到 $n$ 个线性无关的解向量 $\mathbf{x}^{(1)}(t), \mathbf{x}^{(2)}(t), \dots, \mathbf{x}^{(n)}(t)$，它们构成该解空间的一组基。系统的任何解都可以表示为这组基的线性组合。

我们将这 $n$ 个解向量作为列，构成一个 $n \times n$ 的矩阵 $\Phi(t)$：
$$
\Phi(t) = \begin{pmatrix} |  |   | \\ \mathbf{x}^{(1)}(t)  \mathbf{x}^{(2)}(t)  \cdots  \mathbf{x}^{(n)}(t) \\ |  |   | \end{pmatrix}
$$
这个矩阵 $\Phi(t)$ 被称为系统的 **[基本矩阵](@entry_id:275638)**，当且仅当它满足以下两个关键条件：

1.  **矩阵[微分方程](@entry_id:264184)**：$\Phi(t)$ 本身是矩阵形式的[微分方程](@entry_id:264184) $\Phi'(t) = A(t)\Phi(t)$ 的一个解。这等价于说它的每一列都是原向量[微分方程](@entry_id:264184)的一个解。

2.  **[线性无关](@entry_id:148207)性**：$\Phi(t)$ 的列向量在所研究的区间 $I$ 上是[线性无关](@entry_id:148207)的。这保证了这些解构成了整个[解空间](@entry_id:200470)的一组基。在实践中，这一条件等价于矩阵 $\Phi(t)$ 在区间 $I$ 内的每一点都是可逆的，即其[行列式](@entry_id:142978)（称为 **[朗斯基行列式](@entry_id:149814) (Wronskian)**）$W(t) = \det(\Phi(t))$ 在 $I$ 内恒不为零。

为了具体理解这两个条件，让我们考察一个系统 $ \mathbf{x}' = A\mathbf{x} $，其中 $ A = \begin{pmatrix} 1  -1 \\ 2  4 \end{pmatrix} $。假设有一个候选矩阵 $\Phi(t) = \begin{pmatrix} \exp(2t)  \exp(3t) \\ -\exp(2t)  \exp(3t) \end{pmatrix}$ [@problem_id:1715972]。

首先，我们检验第一个条件：$\Phi'(t) = A\Phi(t)$。
该矩阵的导数为 $\Phi'(t) = \begin{pmatrix} 2\exp(2t)  3\exp(3t) \\ -2\exp(2t)  3\exp(3t) \end{pmatrix}$。
而 $A\Phi(t)$ 的计算结果为：
$$
A\Phi(t) = \begin{pmatrix} 1  -1 \\ 2  4 \end{pmatrix} \begin{pmatrix} \exp(2t)  \exp(3t) \\ -\exp(2t)  \exp(3t) \end{pmatrix} = \begin{pmatrix} 2\exp(2t)  0 \\ -2\exp(2t)  6\exp(3t) \end{pmatrix}
$$
通过比较，我们发现 $\Phi'(t) \neq A\Phi(t)$。具体来说，虽然第一列满足 $A\mathbf{x}^{(1)} = (\mathbf{x}^{(1)})'$，但第二列不满足。因此，该矩阵不是此系统的[基本矩阵](@entry_id:275638)，因为它没有完全满足矩阵[微分方程](@entry_id:264184)。

接着，我们检验第二个条件，即线性无关性。我们计算其[朗斯基行列式](@entry_id:149814)：
$$
\det(\Phi(t)) = \exp(2t)\exp(3t) - \exp(3t)(-\exp(2t)) = 2\exp(5t)
$$
由于指数函数恒为正，$\det(\Phi(t))$ 对于所有 $t$ 都不为零。因此，尽管它的列向量是线性无关的，但由于它不满足第一个条件，它仍然不是该系统的[基本矩阵](@entry_id:275638)。

线性无关性的要求至关重要。如果[基本矩阵](@entry_id:275638)的列向量是[线性相关](@entry_id:185830)的，它们就无法张成完整的 $n$ 维[解空间](@entry_id:200470)。这意味着我们无法通过它们的线性组合来表示所有可能的初始状态。例如，考虑一个二维系统，其两个解为 $\mathbf{u}(t) = \begin{pmatrix} 1 \\ 2 \end{pmatrix} \exp(3t)$ 和 $\mathbf{v}(t) = \begin{pmatrix} -2 \\ -4 \end{pmatrix} \exp(3t)$ [@problem_id:1715966]。不难发现，$\mathbf{v}(t) = -2\mathbf{u}(t)$，它们是[线性相关](@entry_id:185830)的。因此，任意线性组合 $\mathbf{x}(t) = c_1\mathbf{u}(t) + c_2\mathbf{v}(t) = (c_1 - 2c_2)\mathbf{u}(t)$ 始终位于由向量 $\begin{pmatrix} 1 \\ 2 \end{pmatrix}$ 张成的直线上。对于任何不在这条直线上的初始条件 $\mathbf{x}(0) = \mathbf{x}_0$，我们都无法找到合适的常数 $c_1, c_2$ 来满足它。因此，这样一组线性相关的解不足以构成通解。

在某些情况下，向量组的线性相关性可能不那么明显。例如，考虑向量函数 $\mathbf{x}^{(1)}(t) = \begin{pmatrix} t^3 \\ t^2 |t| \end{pmatrix}$ 和 $\mathbf{x}^{(2)}(t) = \begin{pmatrix} t^2 \\ t|t| \end{pmatrix}$ [@problem_id:1715931]。尽管它们的表达式看起来不同，但我们注意到对于所有实数 $t$，都有 $\mathbf{x}^{(1)}(t) = t \cdot \mathbf{x}^{(2)}(t)$。这是一个更微妙的线性相关形式。其[朗斯基行列式](@entry_id:149814) $W(t) = t^3(t|t|) - t^2(t^2|t|) = t^4|t| - t^4|t| = 0$ 对所有 $t$ 都成立。由于朗斯基行列式恒为零，这两个向量函数在任何时刻都是线性相关的，因此它们不能构成任何区间上的基本解集。

### [基本矩阵](@entry_id:275638)的关键性质

#### [朗斯基行列式](@entry_id:149814)与[刘维尔公式](@entry_id:267034)

前面我们看到，通过计算 $W(t) = \det(\Phi(t))$ 可以检验解的[线性无关](@entry_id:148207)性。一个深刻的结论是，我们无需在每个点上都计算 $W(t)$。**[刘维尔公式](@entry_id:267034) (Liouville's Formula)** 指出，对于一个满足 $\Phi'(t) = A(t)\Phi(t)$ 的矩阵，其[行列式](@entry_id:142978)满足以下[一阶微分方程](@entry_id:173139)：
$$
\frac{d}{dt}W(t) = \text{tr}(A(t)) W(t)
$$
其中 $\text{tr}(A(t))$ 是矩阵 $A(t)$ 的迹（主对角[线元](@entry_id:196833)素之和）。该方程的解为：
$$
W(t) = W(t_0) \exp\left(\int_{t_0}^t \text{tr}(A(s))\,ds\right)
$$
这个公式的意义非凡：对于一个[线性系统](@entry_id:147850)的解矩阵，其朗斯基行列式要么在区间 $I$ 内恒等于零，要么在 $I$ 内处处不为零。这取决于它在任意一点 $t_0$ 的值 $W(t_0)$ 是否为零。因此，要验证一组解是否线性无关，我们只需在任意一个方便的时刻（如 $t=0$）计算其[行列式](@entry_id:142978)即可。

例如，考虑一个[常系数](@entry_id:269842)系统 $\dot{\mathbf{x}} = A\mathbf{x}$，其中 $A = \begin{pmatrix} 1  2 \\ 2  1 \end{pmatrix}$ [@problem_id:1715907]。对于这个系统，$\text{tr}(A) = 1+1=2$。假设我们找到了一个[基本矩阵](@entry_id:275638) $\Phi(t)$，其初始值为 $\Phi(0) = \begin{pmatrix} 2  0 \\ 1  3 \end{pmatrix}$。根据[刘维尔公式](@entry_id:267034)（对于常数 $A$，公式简化为 $W(t) = W(0) \exp(t \cdot \text{tr}(A))$），我们可以直接计算任意时刻 $t$ 的[行列式](@entry_id:142978)值。
首先，$W(0) = \det(\Phi(0)) = (2)(3) - (0)(1) = 6$。
因此，对于任意 $t$，$\det(\Phi(t)) = 6 \exp(2t)$。
如果我们想知道 $t = \ln(5)$ 时的[行列式](@entry_id:142978)值，只需代入：
$$
\det(\Phi(\ln(5))) = 6 \exp(2\ln(5)) = 6 \exp(\ln(5^2)) = 6 \cdot 25 = 150
$$
这个过程完全不需要求解 $\Phi(t)$ 的具体表达式，展示了[刘维尔公式](@entry_id:267034)的强大威力。

#### [基本矩阵](@entry_id:275638)的非唯一性

一个系统的[基本矩阵](@entry_id:275638)不是唯一的。事实上，存在无穷多个[基本矩阵](@entry_id:275638)。如果 $\Phi_1(t)$ 是一个[基本矩阵](@entry_id:275638)，那么它的列向量构成了系统[解空间](@entry_id:200470)的一组基。我们可以对这组基进行任何可逆的[线性变换](@entry_id:149133)，得到一组新的基。在矩阵语言中，这意味着如果 $C$ 是一个任意的常数可逆矩阵，那么 $\Phi_2(t) = \Phi_1(t)C$ 也是该系统的一个[基本矩阵](@entry_id:275638)。

我们可以验证这一点：
1.  **[微分方程](@entry_id:264184)**：$(\Phi_1(t)C)' = \Phi_1'(t)C = (A(t)\Phi_1(t))C = A(t)(\Phi_1(t)C)$。所以 $\Phi_2(t)$ 满足矩阵[微分方程](@entry_id:264184)。
2.  **线性无关性**：$\det(\Phi_2(t)) = \det(\Phi_1(t)C) = \det(\Phi_1(t))\det(C)$。因为 $\Phi_1(t)$ 是[基本矩阵](@entry_id:275638)，$\det(\Phi_1(t)) \neq 0$。又因为 $C$ 是[可逆矩阵](@entry_id:171829)，$\det(C) \neq 0$。因此 $\det(\Phi_2(t)) \neq 0$。

反过来，如果 $\Phi_1(t)$ 和 $\Phi_2(t)$ 是同一系统的两个[基本矩阵](@entry_id:275638)，它们之间必然通过一个常数可逆矩阵 $C$ 相关联，即 $\Phi_2(t) = \Phi_1(t)C$。要找到这个矩阵 $C$，我们可以利用 $\Phi_1(t)$ 的可逆性：$C = \Phi_1^{-1}(t)\Phi_2(t)$。由于 $C$ 是常数矩阵，这个乘积在任何时刻 $t$ 的值都应该相同。因此，我们可以在一个方便的时刻（如 $t=0$）进行计算：$C = \Phi_1^{-1}(0)\Phi_2(0)$ [@problem_id:1715924]。

例如，对于系统 $\mathbf{x}' = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}\mathbf{x}$，已知两个[基本矩阵](@entry_id:275638)：
$$
\Phi_1(t) = \begin{pmatrix} \cos(t)  \sin(t) \\ \sin(t)  -\cos(t) \end{pmatrix}, \quad \Phi_2(t) = \begin{pmatrix} \cos(t)+\sin(t)  \cos(t)-\sin(t) \\ \sin(t)-\cos(t)  \sin(t)+\cos(t) \end{pmatrix}
$$
在 $t=0$ 时，$\Phi_1(0) = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$ 且 $\Phi_2(0) = \begin{pmatrix} 1  1 \\ -1  1 \end{pmatrix}$。
$\Phi_1(0)$ 的逆是它自身，即 $\Phi_1^{-1}(0) = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$。
因此，
$$
C = \Phi_1^{-1}(0)\Phi_2(0) = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix} \begin{pmatrix} 1  1 \\ -1  1 \end{pmatrix} = \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}
$$
这个常数矩阵 $C$ 揭示了两组基底之间的[线性变换](@entry_id:149133)关系。

### 利用[基本矩阵](@entry_id:275638)[求解初值问题](@entry_id:170405)

[基本矩阵](@entry_id:275638)最直接的应用是[求解初值问题](@entry_id:170405)（IVP）。给定系统 $\mathbf{x}' = A(t)\mathbf{x}$ 和初始条件 $\mathbf{x}(t_0) = \mathbf{x}_0$，其通解可以写作
$$
\mathbf{x}(t) = \Phi(t)\mathbf{c}
$$
其中 $\Phi(t)$ 是任意一个[基本矩阵](@entry_id:275638)，$\mathbf{c}$ 是一个待定的常数向量。将[初始条件](@entry_id:152863)代入：
$$
\mathbf{x}(t_0) = \Phi(t_0)\mathbf{c} = \mathbf{x}_0
$$
由于 $\Phi(t_0)$ 是可逆的，我们可以解出 $\mathbf{c}$：
$$
\mathbf{c} = \Phi^{-1}(t_0)\mathbf{x}_0
$$
将此 $\mathbf{c}$ [回代](@entry_id:146909)到通解表达式中，我们便得到了初值问题的唯一解：
$$
\mathbf{x}(t) = \Phi(t)\Phi^{-1}(t_0)\mathbf{x}_0
$$
这个公式优雅地给出了任意时刻 $t$ 的状态如何由初始状态 $\mathbf{x}_0$ 决定。

例如，考虑一个系统，其[基本矩阵](@entry_id:275638)为 $\Phi(t) = \begin{pmatrix} \exp(t)  \exp(-2t) \\ \exp(t)  -\exp(-2t) \end{pmatrix}$，初始条件为 $\mathbf{x}(0) = \begin{pmatrix} 3 \\ 1 \end{pmatrix}$ [@problem_id:1715909]。
首先，我们计算 $\Phi(0) = \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}$。
然后，我们求解方程 $\Phi(0)\mathbf{c} = \mathbf{x}(0)$ 来确定常数向量 $\mathbf{c} = \begin{pmatrix} c_1 \\ c_2 \end{pmatrix}$：
$$
\begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix} \begin{pmatrix} c_1 \\ c_2 \end{pmatrix} = \begin{pmatrix} 3 \\ 1 \end{pmatrix}
$$
解这个线性方程组得到 $c_1 = 2$ 和 $c_2 = 1$，所以 $\mathbf{c} = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$。
最后，将 $\mathbf{c}$ 代入通解公式：
$$
\mathbf{x}(t) = \Phi(t)\mathbf{c} = \begin{pmatrix} \exp(t)  \exp(-2t) \\ \exp(t)  -\exp(-2t) \end{pmatrix} \begin{pmatrix} 2 \\ 1 \end{pmatrix} = \begin{pmatrix} 2\exp(t) + \exp(-2t) \\ 2\exp(t) - \exp(-2t) \end{pmatrix}
$$
这就是满足给定初始条件的[特解](@entry_id:149080)。

### [状态转移矩阵](@entry_id:269075)与矩阵指数

#### [状态转移矩阵](@entry_id:269075)的定义与性质

在上述[求解初值问题](@entry_id:170405)的公式 $\mathbf{x}(t) = \Phi(t)\Phi^{-1}(t_0)\mathbf{x}_0$ 中，矩阵乘积 $\Phi(t)\Phi^{-1}(t_0)$ 扮演了一个特殊角色。我们将其定义为 **[状态转移矩阵](@entry_id:269075) (State Transition Matrix)**，记作 $\Phi(t, t_0)$。
$$
\Phi(t, t_0) := \Phi(t)\Phi^{-1}(t_0)
$$
顾名思义，[状态转移矩阵](@entry_id:269075)将系统在时刻 $t_0$ 的状态 $\mathbf{x}(t_0)$ “转移” 到时刻 $t$ 的状态 $\mathbf{x}(t)$：
$$
\mathbf{x}(t) = \Phi(t, t_0)\mathbf{x}(t_0)
$$
值得注意的是，尽管[基本矩阵](@entry_id:275638) $\Phi(t)$ 不是唯一的，但[状态转移矩阵](@entry_id:269075) $\Phi(t, t_0)$ 是唯一确定的。这是因为如果我们用另一个[基本矩阵](@entry_id:275638) $\tilde{\Phi}(t) = \Phi(t)C$ 来计算，会得到相同的结果：
$$
\tilde{\Phi}(t)\tilde{\Phi}^{-1}(t_0) = (\Phi(t)C)((\Phi(t_0)C)^{-1}) = (\Phi(t)C)(C^{-1}\Phi^{-1}(t_0)) = \Phi(t)I\Phi^{-1}(t_0) = \Phi(t, t_0)
$$
[状态转移矩阵](@entry_id:269075)是满足矩阵[微分方程](@entry_id:264184) $\frac{d}{dt}\Phi(t, t_0) = A(t)\Phi(t, t_0)$ 且[初始条件](@entry_id:152863)为 $\Phi(t_0, t_0) = I$（单位矩阵）的唯一矩阵。

一个特别重要的[基本矩阵](@entry_id:275638)是**[主基本矩阵](@entry_id:163277) (Principal Fundamental Matrix)**，通常记为 $\Psi(t)$，它是在 $t_0=0$ 处等于单位矩阵的[基本矩阵](@entry_id:275638)，即 $\Psi(0)=I$。由任意[基本矩阵](@entry_id:275638) $\Phi(t)$，我们可以构造出[主基本矩阵](@entry_id:163277) [@problem_id:1715961]：
$$
\Psi(t) = \Phi(t)\Phi^{-1}(0)
$$
若使用[主基本矩阵](@entry_id:163277)，则[状态转移矩阵](@entry_id:269075)可以更简洁地表示为 $\Phi(t, t_0) = \Psi(t)\Psi^{-1}(t_0)$。

[状态转移矩阵](@entry_id:269075)最重要的性质是**[半群性质](@entry_id:271012) (Semigroup Property)**：
$$
\Phi(t_2, t_0) = \Phi(t_2, t_1)\Phi(t_1, t_0) \quad \text{for any } t_0, t_1, t_2
$$
这个性质的直观意义是，将系统从 $t_0$ 演化到 $t_2$，等同于先从 $t_0$ 演化到 $t_1$，再从 $t_1$ 演化到 $t_2$。这个性质即使在[时变系统](@entry_id:175653)（$A(t)$ 依赖于时间）中也成立 [@problem_id:1715916]。

#### [线性时不变系统](@entry_id:276591)与矩阵指数

对于**[线性时不变](@entry_id:276287) (Linear Time-Invariant, LTI)** 系统，即矩阵 $A$ 是常数矩阵，情况得到极大简化。在这种情况下，[主基本矩阵](@entry_id:163277) $\Psi(t)$ 有一个非常优雅和强大的形式——**[矩阵指数](@entry_id:139347) (Matrix Exponential)**：
$$
\Psi(t) = \exp(At) = \sum_{k=0}^{\infty} \frac{(At)^k}{k!} = I + At + \frac{A^2 t^2}{2!} + \dots
$$
我们可以验证 $\exp(At)$ 确实是[主基本矩阵](@entry_id:163277)：
1.  **[微分方程](@entry_id:264184)**：$\frac{d}{dt}\exp(At) = \frac{d}{dt}\left(\sum_{k=0}^{\infty} \frac{A^k t^k}{k!}\right) = \sum_{k=1}^{\infty} \frac{A^k t^{k-1}}{(k-1)!} = A \left(\sum_{k=1}^{\infty} \frac{A^{k-1} t^{k-1}}{(k-1)!}\right) = A \exp(At)$。
2.  **初始条件**：$\exp(A \cdot 0) = I$。

因此，对于[LTI系统](@entry_id:271946)，[状态转移矩阵](@entry_id:269075)为 $\Phi(t, t_0) = \exp(A(t-t_0))$。这使得[求解IVP](@entry_id:170405)变得非常直接：
$$
\mathbf{x}(t) = \exp(A(t-t_0))\mathbf{x}(t_0)
$$
计算[矩阵指数](@entry_id:139347) $\exp(At)$ 是解决[LTI系统](@entry_id:271946)的关键。虽然其级数定义在理论上很重要，但在实践中通常使用基于[特征值分解](@entry_id:272091)或[若尔当标准型](@entry_id:155670)的方法。例如，对于一个具有[重特征值](@entry_id:154579)的 $2 \times 2$ 矩阵 $A = \begin{pmatrix} 3  -1 \\ 1  1 \end{pmatrix}$ [@problem_id:1715968]，其[特征值](@entry_id:154894)为 $\lambda=2$（[代数重数](@entry_id:154240)为2）。令 $N = A - 2I = \begin{pmatrix} 1  -1 \\ 1  -1 \end{pmatrix}$，我们发现 $N^2=0$（$N$ 是一个[幂零矩阵](@entry_id:152732)）。由于 $A=2I+N$，并且 $2I$ 与 $N$ 可交换，我们可以写出：
$$
\exp(At) = \exp((2I+N)t) = \exp(2It)\exp(Nt) = \exp(2t)I \cdot \left(I + Nt + \frac{(Nt)^2}{2!} + \dots\right)
$$
因为 $N^2=0$，所有更高次的项也为零，所以 $\exp(Nt) = I+Nt$。因此，
$$
\exp(At) = \exp(2t)(I+Nt) = \exp(2t)\left(\begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} + t\begin{pmatrix} 1  -1 \\ 1  -1 \end{pmatrix}\right) = \exp(2t)\begin{pmatrix} 1+t  -t \\ t  1-t \end{pmatrix}
$$
利用这个[矩阵指数](@entry_id:139347)，我们可以求解任何[初始条件](@entry_id:152863)下的解。例如，若初始状态为 $\mathbf{\psi}(0) = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$，则 $t=4$ 时的解为：
$$
\mathbf{\psi}(4) = \exp(A \cdot 4)\mathbf{\psi}(0) = \exp(8)\begin{pmatrix} 1+4  -4 \\ 4  1-4 \end{pmatrix} \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \exp(8)\begin{pmatrix} -4 \\ -3 \end{pmatrix}
$$
其第一个分量为 $\psi_1(4) = -4\exp(8)$。

总结而言，[基本矩阵](@entry_id:275638)是理解[线性动力系统](@entry_id:150282)解的结构的基石。它不仅提供了构造通解的系统方法，还引出了[状态转移矩阵](@entry_id:269075)这一核心概念，后者描述了系统状态随时间的确定性演化。对于[LTI系统](@entry_id:271946)，这一框架最终归结为优雅而强大的矩阵指数理论。