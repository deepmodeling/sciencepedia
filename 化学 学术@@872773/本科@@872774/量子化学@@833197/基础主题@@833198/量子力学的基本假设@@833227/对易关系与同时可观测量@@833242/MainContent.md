## 引言
在经典世界中，测量一个物体的属性，如位置和速度，似乎理所当然可以同时精确进行。然而，在微观的量子领域，这一直觉被彻底颠覆。量子力学的一个基石概念是，物理量由算符表示，而这些算符的运算顺序往往会影响最终结果。这种不[可交换性](@entry_id:263314)是量子世界奇异特性的根源。那么，我们如何量化这种不[可交换性](@entry_id:263314)？又该如何判断哪些物理量是可以同时被精确测量的“相容”属性呢？

本文旨在深入探讨解决这一核心问题的关键工具——[对易关系](@entry_id:136780)。我们将从“原理与机制”一章出发，系统介绍对易子的定义、代数性质，并揭示其与[海森堡不确定性原理](@entry_id:171099)及共同[本征态](@entry_id:149904)之间的深刻联系。接着，在“应用与跨学科联系”一章中，我们将展示这一理论的强大威力，看它如何解释[原子结构](@entry_id:137190)、角动量、分子对称性，乃至指导[量子计算](@entry_id:142712)等前沿科技的设计。最后，通过“动手实践”部分，您将有机会亲手计算和验证这些重要的对易关系，从而巩固所学知识。通过本文的学习，您将掌握从根本上理解和预测微观系统行为的强大分析工具。

## 原理与机制

### 对易子的定义及其代数性质

在量子力学中，可观测的物理量由厄米算符表示。两个算符 $\hat{A}$ 和 $\hat{B}$ 的先后作用顺序可能会影响最终结果，这种不[可交换性](@entry_id:263314)是量子世界与经典世界的根本区别之一。为了量化这种不[可交换性](@entry_id:263314)，我们定义了**对易子**（commutator）。

两个算符 $\hat{A}$ 和 $\hat{B}$ 的对易子定义为：
$$
[\hat{A}, \hat{B}] = \hat{A}\hat{B} - \hat{B}\hat{A}
$$
如果 $[\hat{A}, \hat{B}] = 0$，我们称算符 $\hat{A}$ 和 $\hat{B}$ **对易**（commute）。这意味着它们的作用顺序无关紧要，即 $\hat{A}\hat{B} = \hat{B}\hat{A}$。反之，如果 $[\hat{A}, \hat{B}] \neq 0$，则算符不对易，其作用顺序会影响结果。

对易子具有一些基本的代数性质，这些性质在量子力学的计算中至关重要：
1.  **反对称性**：
    $$
    [\hat{A}, \hat{B}] = -[\hat{B}, \hat{A}]
    $$
2.  **线性性**：对易子对其两个变元都是线性的。例如，对于任意复数 $c_1$ 和 $c_2$：
    $$
    [\hat{A}, c_1\hat{B} + c_2\hat{C}] = c_1[\hat{A}, \hat{B}] + c_2[\hat{A}, \hat{C}]
    $$
3.  **乘积法则（Leibniz 法则）**：
    $$
    [\hat{A}, \hat{B}\hat{C}] = [\hat{A}, \hat{B}]\hat{C} + \hat{B}[\hat{A}, \hat{C}]
    $$
    $$
    [\hat{A}\hat{B}, \hat{C}] = \hat{A}[\hat{B}, \hat{C}] + [\hat{A}, \hat{C}]\hat{B}
    $$
4.  **雅可比恒等式**：
    $$
    [\hat{A}, [\hat{B}, \hat{C}]] + [\hat{B}, [\hat{C}, \hat{A}]] + [\hat{C}, [\hat{A}, \hat{B}]] = 0
    $$

这些性质使得对易子的计算可以系统地进行。例如，考虑一维系统中的位置算符 $\hat{x}$ 和动量算符 $\hat{p}_x$，它们满足**[正则对易关系](@entry_id:185041)** $[\hat{x}, \hat{p}_x] = i\hbar$。这是量子力学中最基本的对易关系之一。基于此，我们可以计算由它们[线性组合](@entry_id:154743)而成的新算符的[对易关系](@entry_id:136780)。

设想我们构造了两个新的可观测量算符 $\hat{Q} = 4\hat{x} - 7\hat{p}_x$ 和 $\hat{R} = 2\hat{x} + 3\hat{p}_x$。利用对易子的[双线性性](@entry_id:146819)质，我们可以计算 $[\hat{Q}, \hat{R}]$ [@problem_id:1358633]：
$$
\begin{align}
[\hat{Q}, \hat{R}]  = [4\hat{x} - 7\hat{p}_x, 2\hat{x} + 3\hat{p}_x] \\
 = [4\hat{x}, 2\hat{x}] + [4\hat{x}, 3\hat{p}_x] + [-7\hat{p}_x, 2\hat{x}] + [-7\hat{p}_x, 3\hat{p}_x] \\
 = 8[\hat{x}, \hat{x}] + 12[\hat{x}, \hat{p}_x] - 14[\hat{p}_x, \hat{x}] - 21[\hat{p}_x, \hat{p}_x]
\end{align}
$$
由于任何算符与自身的对易子为零（例如 $[\hat{x}, \hat{x}] = 0$），并利用反对称性 $[\hat{p}_x, \hat{x}] = -[\hat{x}, \hat{p}_x] = -i\hbar$，上式可简化为：
$$
[\hat{Q}, \hat{R}] = 12(i\hbar) - 14(-i\hbar) = (12+14)i\hbar = 26i\hbar
$$
这个结果表明，即使是由对易的算符（$\hat{x}$ 和 $\hat{x}$）和不对易的算符（$\hat{x}$ 和 $\hat{p}_x$）线性组合而成的新算符，它们之间通常也是不对易的。

同样，乘积法则是处理算符乘积的对易关系时的有力工具。为了更好地理解其应用，我们可以考虑一个具体场景 [@problem_id:1358610]。令算符 $\hat{A}$, $\hat{B}$, $\hat{C}$ 分别定义为 $\hat{A}f(x) = \alpha x f(x)$, $\hat{B}f(x) = \frac{d}{dx}f(x)$, $\hat{C}f(x) = x^2 f(x)$。我们来计算 $[\hat{A}, \hat{B}\hat{C}]$ 作用在任意函数 $f(x)$ 上的结果。根据定义：
$$
[\hat{A}, \hat{B}\hat{C}]f = (\hat{A}\hat{B}\hat{C} - \hat{B}\hat{C}\hat{A})f
$$
分别计算两项：
$$
\hat{A}\hat{B}\hat{C}f = \hat{A}\hat{B}(x^2 f) = \hat{A}\left(\frac{d}{dx}(x^2f)\right) = \hat{A}(2xf + x^2 f') = \alpha x (2xf + x^2 f') = 2\alpha x^2 f + \alpha x^3 f'
$$
$$
\hat{B}\hat{C}\hat{A}f = \hat{B}\hat{C}(\alpha x f) = \hat{B}(x^2 \cdot \alpha x f) = \hat{B}(\alpha x^3 f) = \alpha \frac{d}{dx}(x^3 f) = \alpha(3x^2 f + x^3 f') = 3\alpha x^2 f + \alpha x^3 f'
$$
两者相减得到：
$$
[\hat{A}, \hat{B}\hat{C}]f = (2\alpha x^2 f + \alpha x^3 f') - (3\alpha x^2 f + \alpha x^3 f') = -\alpha x^2 f(x)
$$
这验证了对易子的复杂结构，并展示了如何通过作用于一个任意函数来确定算符的[等价关系](@entry_id:138275)。

### 对易关系与不确定性原理

[对易子的物理意义](@entry_id:150090)远不止于代数运算。它与量子力学的一个核心概念——**[不确定性原理](@entry_id:141278)**——紧密相连。对于任意两个[厄米算符](@entry_id:153410) $\hat{A}$ 和 $\hat{B}$，它们所对应的物理量在任何[量子态](@entry_id:146142)上的测量[标准差](@entry_id:153618) $\Delta A$ 和 $\Delta B$ 必须满足**[广义不确定性关系](@entry_id:156492)**：
$$
(\Delta A)^2 (\Delta B)^2 \ge \left| \frac{1}{2i} \langle [\hat{A}, \hat{B}] \rangle \right|^2
$$
其中 $\langle \cdot \rangle$ 表示在给定[量子态](@entry_id:146142)下的[期望值](@entry_id:153208)。

这个关系式揭示了一个深刻的物理原理：
**如果两个可观测量对应的算符对易，即 $[\hat{A}, \hat{B}] = 0$，那么[不确定性关系](@entry_id:186128)的右侧为零。这意味着原则上可以找到一个[量子态](@entry_id:146142)，使得这两个物理量可以被同时、无限精确地测量。** 我们称这样的物理量为**可同时观测的**（simultaneously observable）。

反之，如果两个算符不对易，$[\hat{A}, \hat{B}] \neq 0$，那么在任何状态下，同时精确测量这两个物理量是不可能的。它们的[测量精度](@entry_id:271560)乘积存在一个由对易子决定的非零下限。最著名的例子就是位置和动量，由于 $[\hat{x}, \hat{p}_x] = i\hbar \neq 0$，导致了[海森堡不确定性原理](@entry_id:171099) $\Delta x \Delta p_x \ge \hbar/2$。

我们可以通过具体的例子来理解这个原理的应用 [@problem_id:2105766]。考虑以下几对物理量：
*   **位置 ($\hat{x}$) 与动能 ($\hat{K} = \frac{\hat{p}^2}{2m}$)**：
    我们需要计算 $[\hat{x}, \hat{K}]$。利用[乘积法则](@entry_id:158393)：
    $$
    [\hat{x}, \hat{p}^2] = [\hat{x}, \hat{p}]\hat{p} + \hat{p}[\hat{x}, \hat{p}] = (i\hbar)\hat{p} + \hat{p}(i\hbar) = 2i\hbar\hat{p}
    $$
    因此，
    $$
    [\hat{x}, \hat{K}] = \frac{1}{2m}[\hat{x}, \hat{p}^2] = \frac{i\hbar}{m}\hat{p} \neq 0
    $$
    由于对易子不为零，位置和动能无法被同时精确测量。直观上，确定一个粒子的精确位置会使其[波函数局域化](@entry_id:190191)，而一个局域化的波包必然是不同动量本征[态的叠加](@entry_id:273993)，从而导致动量（及动能）的不确定性。

*   **[自由粒子](@entry_id:148748)的能量 ($\hat{H}_{\text{free}} = \frac{\hat{p}^2}{2m}$) 与宇称 ($\hat{\Pi}$)**：
    [宇称算符](@entry_id:148434)的作用是空间反演，$\hat{\Pi} f(x) = f(-x)$。它对位置和动量算符的作用是 $\hat{\Pi}\hat{x}\hat{\Pi}^{-1} = -\hat{x}$ 和 $\hat{\Pi}\hat{p}\hat{\Pi}^{-1} = -\hat{p}$。因此，[宇称算符](@entry_id:148434)作用在动量的平方上时：
    $$
    \hat{\Pi}\hat{p}^2\hat{\Pi}^{-1} = (\hat{\Pi}\hat{p}\hat{\Pi}^{-1})(\hat{\Pi}\hat{p}\hat{\Pi}^{-1}) = (-\hat{p})(-\hat{p}) = \hat{p}^2
    $$
    这意味着 $\hat{\Pi}\hat{p}^2 = \hat{p}^2\hat{\Pi}$，所以 $[\hat{\Pi}, \hat{p}^2] = 0$。进而，
    $$
    [\hat{H}_{\text{free}}, \hat{\Pi}] = \left[\frac{\hat{p}^2}{2m}, \hat{\Pi}\right] = \frac{1}{2m}[\hat{p}^2, \hat{\Pi}] = 0
    $$
    由于自由粒子[哈密顿量](@entry_id:172864)与[宇称算符](@entry_id:148434)对易，这两个物理量是可同时观测的。这意味着[自由粒子](@entry_id:148748)的[能量本征态](@entry_id:152154)可以同时具有确定的宇称（即，它们可以是偶函数或奇函数）。

### 共同本征态与可对易观测量的测量

[对易算符](@entry_id:149529)与[同时可观测量](@entry_id:268369)之间的联系可以通过**共同[本征态](@entry_id:149904)**（simultaneous eigenstate）的概念进一步加深。

一个[量子态](@entry_id:146142) $|\psi\rangle$ 如果同时是算符 $\hat{A}$ 和 $\hat{B}$ 的[本征态](@entry_id:149904)，即：
$$
\hat{A}|\psi\rangle = a|\psi\rangle \quad \text{和} \quad \hat{B}|\psi\rangle = b|\psi\rangle
$$
其中 $a$ 和 $b$ 分别是对应的[本征值](@entry_id:154894)，那么我们称 $|\psi\rangle$ 是 $\hat{A}$ 和 $\hat{B}$ 的一个共同本征态。当系统处于这样的状态时，对物理量 A 和 B 的测量将确定地得到结果 $a$ 和 $b$。

这里有一个核心定理：**当且仅当两个厄米算符 $\hat{A}$ 和 $\hat{B}$ 对易（$[\hat{A}, \hat{B}] = 0$），它们才存在一个完备的共同本征态[基矢](@entry_id:199546)。**

这意味着，如果两个算符对易，我们总能找到一组[基矢](@entry_id:199546)，其中每个[基矢](@entry_id:199546)都同时是这两个算符的[本征态](@entry_id:149904)。任何一个[量子态](@entry_id:146142)都可以表示为这组[基矢](@entry_id:199546)的[线性组合](@entry_id:154743)。

一个清晰的例子是[刚性转子模型](@entry_id:153240)，例如模拟一个甲基的内部转动 [@problem_id:1358596]。其角动量 z 分量算符为 $\hat{L}_z = -i\hbar \frac{d}{d\phi}$，动能（[哈密顿量](@entry_id:172864)）算符为 $\hat{H} = -\frac{\hbar^2}{2I} \frac{d^2}{d\phi^2}$。我们可以发现 $\hat{L}_z^2 = (-i\hbar \frac{d}{d\phi})^2 = -\hbar^2 \frac{d^2}{d\phi^2}$，所以[哈密顿量](@entry_id:172864)可以写成 $\hat{H} = \frac{\hat{L}_z^2}{2I}$。由于 $\hat{H}$ 只是 $\hat{L}_z$ 的函数，它们必然对易：
$$
[\hat{H}, \hat{L}_z] = \left[\frac{\hat{L}_z^2}{2I}, \hat{L}_z\right] = 0
$$
因为算符对易，它们拥有共同的[本征态](@entry_id:149904)。如果系统被制备在 $\hat{L}_z$ 的一个[本征态](@entry_id:149904) $\psi_k$ 上，满足 $\hat{L}_z\psi_k = \hbar k \psi_k$，那么这个态也必定是 $\hat{H}$ 的本征态：
$$
\hat{H}\psi_k = \frac{\hat{L}_z^2}{2I} \psi_k = \frac{1}{2I} \hat{L}_z (\hbar k \psi_k) = \frac{\hbar k}{2I} (\hat{L}_z \psi_k) = \frac{\hbar k}{2I} (\hbar k \psi_k) = \frac{\hbar^2 k^2}{2I} \psi_k
$$
因此，对这个态进行能量测量，得到的结果是确定的值 $\frac{\hbar^2 k^2}{2I}$，而不是一个[概率分布](@entry_id:146404)。

反之，如果实验发现一个系统状态对于两个物理量 $Q_1$ 和 $Q_2$ 总能给出确定的测量值，这强烈暗示了这两个物理量对应的算符是对易的 [@problem_id:1358588]。假设一个态 $\Psi$ 是算符 $\hat{Q}_1$ 和 $\hat{Q}_2$ 的共同本征态，那么测量 $Q_1$ 和 $Q_2$ 的[方差](@entry_id:200758)均为零，即 $\Delta Q_1 = 0$ 和 $\Delta Q_2 = 0$。根据[不确定性关系](@entry_id:186128)，这意味着 $\langle [\hat{Q}_1, \hat{Q}_2] \rangle = 0$。如果对易子 $[\hat{Q}_1, \hat{Q}_2]$ 本身是一个常[数乘](@entry_id:155971)以单位算符（即所谓的 c-数），那么它的[期望值](@entry_id:153208)就是这个常数本身。因此，这个对易子算符必须为零。这个推论为我们从实验现象反推算符性质提供了途径。

当两个算符不对易时，情况则完全不同。它们不共享一个完备的本征态[基矢](@entry_id:199546)。一个算符的[本征态](@entry_id:149904)通常是另一个算符的多个本征态的叠加。考虑一个双能级系统，其[哈密顿量](@entry_id:172864) $\hat{H}$ 和另一个可观测量“颜色” $\hat{C}$ 的矩阵表示为 [@problem_id:1358630]：
$$
\hat{H} = E_0 \begin{pmatrix} 3  2 \\ 2  6 \end{pmatrix}, \quad \hat{C} = c_0 \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}
$$
我们可以计算它们的对易子矩阵：
$$
[\hat{H}, \hat{C}] = E_0 c_0 \left[ \begin{pmatrix} 3  2 \\ 2  6 \end{pmatrix}, \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix} \right] = E_0 c_0 \left( \begin{pmatrix} 3  -2 \\ 2  -6 \end{pmatrix} - \begin{pmatrix} 3  2 \\ -2  -6 \end{pmatrix} \right) = E_0 c_0 \begin{pmatrix} 0  -4 \\ 4  0 \end{pmatrix} \neq 0
$$
由于算符不对易，$\hat{H}$ 的[本征态](@entry_id:149904)（能量本征态）不是 $\hat{C}$ 的本征态（颜色[本征态](@entry_id:149904)）。系统的能量最低的态，即[基态](@entry_id:150928) $|\psi_g\rangle$，是 $\hat{H}$ 对应于最小[本征值](@entry_id:154894)的本征矢。通过计算，我们发现 $\hat{H}$ 的[能量本征值](@entry_id:144381)为 $2E_0$ 和 $7E_0$，[基态](@entry_id:150928) $|\psi_g\rangle$ 对应于能量 $2E_0$，其在 $\{|\phi_1\rangle, |\phi_2\rangle\}$ 基下的表示为 $\frac{1}{\sqrt{5}}(-2|\phi_1\rangle + |\phi_2\rangle)$。而颜色算符 $\hat{C}$ 的[本征态](@entry_id:149904)恰好是[基矢](@entry_id:199546) $|\phi_1\rangle$（[本征值](@entry_id:154894) $+c_0$）和 $|\phi_2\rangle$（[本征值](@entry_id:154894) $-c_0$）。
因此，当系统处于[基态](@entry_id:150928) $|\psi_g\rangle$ 时，测量其“颜色”会发生什么？系统状态将“塌缩”到 $\hat{C}$ 的一个[本征态](@entry_id:149904)上。测量结果为 $+c_0$ 的概率由 $|\psi_g\rangle$ 中 $|\phi_1\rangle$ 的分量决定：
$$
P(+c_0) = |\langle \phi_1 | \psi_g \rangle|^2 = \left| \frac{-2}{\sqrt{5}} \right|^2 = \frac{4}{5}
$$
这个例子生动地说明了，对于不对易的物理量，一个量的确定状态必然是另一个量的不确定状态的叠加，测量结果是概率性的。

### 对易子在动力学与对称性中的应用

对易子的重要性不仅限于静态的[测量问题](@entry_id:189139)，它在理解量子系统的动力学演化和对称性方面也扮演着核心角色。

#### [守恒量](@entry_id:150267)与[运动常数](@entry_id:150267)

在量子力学中，一个物理量被称为**[守恒量](@entry_id:150267)**（或**运动常数**），如果其[期望值](@entry_id:153208)不随时间改变。对于一个本身不显含时间的算符 $\hat{O}$，其[期望值](@entry_id:153208) $\langle \hat{O} \rangle$ 的[时间演化](@entry_id:153943)由以下方程描述（[海森堡绘景](@entry_id:141162)）：
$$
\frac{d}{dt} \langle \hat{O} \rangle = \frac{i}{\hbar} \langle [\hat{H}, \hat{O}] \rangle
$$
从这个方程可以立即得出一个至关重要的结论：
**一个不显含时间的物理量是守恒量，当且仅当其对应的算符与系统的[哈密顿量](@entry_id:172864) $\hat{H}$ 对易。**
$$
[\hat{H}, \hat{O}] = 0 \quad \iff \quad \frac{d}{dt} \langle \hat{O} \rangle = 0
$$
这为我们从[哈密顿量](@entry_id:172864)的形式识别守恒量提供了一个强大的判据。例如，在一个二维[各向同性谐振子](@entry_id:190656)系统中，其[哈密顿量](@entry_id:172864)为 $\hat{H} = \frac{\hat{p}_x^2 + \hat{p}_y^2}{2m} + \frac{1}{2} k (\hat{x}^2 + \hat{y}^2)$ [@problem_id:1358646]。我们可以检验哪些物理量是守恒的：
*   $y$ 方向的动量 $\hat{p}_y$：$[\hat{H}, \hat{p}_y] = [\frac{1}{2}k\hat{y}^2, \hat{p}_y] = i\hbar k\hat{y} \neq 0$。因此 $\hat{p}_y$ 不守恒。
*   $z$ 方向的角动量 $\hat{L}_z = \hat{x}\hat{p}_y - \hat{y}\hat{p}_x$：由于[势能](@entry_id:748988) $V \propto (x^2+y^2)$ 是转动不变的，我们可以证明 $[\hat{H}, \hat{L}_z] = 0$。因此，$\hat{L}_z$ 是一个[守恒量](@entry_id:150267)。
*   $x$ 方向的能量 $\hat{H}_x = \frac{\hat{p}_x^2}{2m} + \frac{1}{2}k\hat{x}^2$：由于[哈密顿量](@entry_id:172864)可以分离变量 $\hat{H} = \hat{H}_x + \hat{H}_y$，且 $x$ 和 $y$ 的自由度是独立的（即 $x$ 相关的算符与 $y$ 相关的算符对易），我们有 $[\hat{H}, \hat{H}_x] = [\hat{H}_x + \hat{H}_y, \hat{H}_x] = [\hat{H}_y, \hat{H}_x] = 0$。因此 $\hat{H}_x$ 也是一个[守恒量](@entry_id:150267)。这揭示了该系统一个特殊的对称性。

#### [对称性与简并](@entry_id:177833)

守恒量通常与系统的**对称性**有关。如果一个变换（如平移、旋转、反演）使系统的[哈密顿量](@entry_id:172864)保持不变，我们就说系统具有相应的对称性。代表该变换的算符 $\hat{S}$ 将与[哈密顿量](@entry_id:172864)对易，$[\hat{H}, \hat{S}]=0$。

对易关系在这里揭示了能级**简并**（degeneracy）的一个深刻来源。简[并指](@entry_id:276731)的是多个[线性无关](@entry_id:148207)的[量子态](@entry_id:146142)拥有完全相同的能量。考虑一个对称性算符 $\hat{S}$，它与 $\hat{H}$ 对易。假设 $|\psi\rangle$ 是一个[能量本征态](@entry_id:152154)，$\hat{H}|\psi\rangle = E|\psi\rangle$。现在我们将 $\hat{S}$ 作用于 $|\psi\rangle$ 上，得到新态 $|\phi\rangle = \hat{S}|\psi\rangle$。这个新态的能量是多少？
$$
\hat{H}|\phi\rangle = \hat{H}(\hat{S}|\psi\rangle) = \hat{S}(\hat{H}|\psi\rangle) = \hat{S}(E|\psi\rangle) = E(\hat{S}|\psi\rangle) = E|\phi\rangle
$$
这表明 $|\phi\rangle$ 也是一个能量为 $E$ 的[本征态](@entry_id:149904)。现在，如果原始态 $|\psi\rangle$ 碰巧不是对称算符 $\hat{S}$ 的本征态，那么 $|\phi\rangle$ 将是一个与 $|\psi\rangle$ 线性无关的新态。这就意味着存在[能量简并](@entry_id:203091)。

**定理：如果存在一个与[哈密顿量](@entry_id:172864)对易的对称性算符 $\hat{S}$，并且某个[能量本征态](@entry_id:152154) $|\psi\rangle$ 不是 $\hat{S}$ 的本征态，那么该能级必然是简并的。**

一个很好的例子是二维[势场](@entry_id:143025) $V(x,y)$ 具有[交换对称性](@entry_id:151892)，即 $V(x,y)=V(y,x)$ [@problem_id:1358603]。定义[交换算符](@entry_id:156554) $S$ 为 $S f(x,y) = f(y,x)$。可以验证 $[\hat{H}, S] = 0$。假设我们发现一个[能量本征态](@entry_id:152154) $\psi(x, y) = A(x + 2y) \exp(-\beta(x^2+y^2))$，它显然不具有[交换对称性](@entry_id:151892)（即 $S\psi \neq c\psi$）。根据上述理论，态 $\phi = S\psi$ 必定是另一个与 $\psi$ 简并的能量本征态。
$$
\phi(x,y) = S\psi(x,y) = \psi(y,x) = A(y + 2x) \exp(-\beta(y^2+x^2))
$$
这个新态 $\phi(x,y)$ 与 $\psi(x,y)$ 线性无关，但拥有完全相同的能量 $E$。因此，对称性直接导致了能级的简并。

#### [变换的生成元](@entry_id:172031)与[阶梯算符](@entry_id:199991)

对易关系还揭示了算符在更抽象层面上的作用——作为**[变换的生成元](@entry_id:172031)**。例如，[动量算符](@entry_id:151743) $\hat{p}_x$ 是空间平移的生成元。考虑一个无穷小空间平移 $\epsilon$，其变换算符为 $\hat{T}(\epsilon) = \exp(-i\epsilon \hat{p}_x / \hbar) \approx \hat{I} - i\epsilon \hat{p}_x / \hbar$。一个依赖于位置的算符 $\hat{A} = f(\hat{x})$ 在此变换下的变化可以由对易子给出 [@problem_id:1358604]：
$$
\delta \hat{A} \approx \frac{i\epsilon}{\hbar} [\hat{p}_x, f(\hat{x})]
$$
利用[对易关系](@entry_id:136780) $[\hat{p}_x, f(\hat{x})] = -i\hbar f'(\hat{x})$（其中 $f'$ 是函数 $f$ 对其变量的导数），我们得到：
$$
\delta \hat{A} \approx \frac{i\epsilon}{\hbar} (-i\hbar f'(\hat{x})) = \epsilon f'(\hat{x})
$$
这正是函数 $f(x)$ 在平移 $\epsilon$ 后的一阶变化 $f(x+\epsilon) - f(x) \approx \epsilon f'(x)$ 的算符版本。因此，[正则对易关系](@entry_id:185041) $[\hat{x}, \hat{p}_x]=i\hbar$ 蕴含了动量是位置的[共轭变量](@entry_id:147843)，它生成了空间平移。

最后，[对易关系](@entry_id:136780)的[代数结构](@entry_id:137052)可以用来解决一些重要的物理问题，最典型的例子就是量子谐振子。通过定义**产生**和**湮灭算符**（$\hat{a}^\dagger$ 和 $\hat{a}$），可以得到它们与[哈密顿量](@entry_id:172864) $\hat{H}$ 的[对易关系](@entry_id:136780)，例如 $[\hat{H}, \hat{a}] = -\hbar\omega\hat{a}$ [@problem_id:1358589]。这个关系式有一个惊人的推论。假设 $\psi$ 是能量为 $E$ 的本征态，即 $\hat{H}\psi = E\psi$。那么新态 $\phi = \hat{a}\psi$ 的能量是：
$$
\hat{H}\phi = \hat{H}\hat{a}\psi = (\hat{a}\hat{H} + [\hat{H}, \hat{a}])\psi = (\hat{a}\hat{H} - \hbar\omega\hat{a})\psi = \hat{a}(E\psi) - \hbar\omega(\hat{a}\psi) = (E - \hbar\omega)\hat{a}\psi = (E - \hbar\omega)\phi
$$
只要 $\phi$ 不是[零态](@entry_id:154996)，它就是能量为 $E - \hbar\omega$ 的新本征态。这表明湮灭算符 $\hat{a}$ 的作用就像一个“阶梯”，将系统“降低”一个能量量子 $\hbar\omega$。同理，[产生算符](@entry_id:191512) $\hat{a}^\dagger$ 会将能量“升高”一个量子。这种纯代数的方法，完全基于对易关系，不仅能推导出谐振子的分立等间距能谱，还极大地简化了相关物理量的计算，展示了[对易关系](@entry_id:136780)在量子理论中的强大威力。