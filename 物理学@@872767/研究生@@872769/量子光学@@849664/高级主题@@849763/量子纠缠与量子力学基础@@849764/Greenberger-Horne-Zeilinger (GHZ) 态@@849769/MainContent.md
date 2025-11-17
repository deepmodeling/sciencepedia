## 引言
[量子纠缠](@entry_id:136576)是量子力学的基石之一，它描述了多个粒子之间超越经典物理想象的深刻关联。然而，当我们从熟悉的双粒子纠缠走向[多体系统](@entry_id:144006)时，一个更为丰富和复杂的纠缠世界便展现在眼前。在探索这个前沿领域时，格林伯格-霍恩-蔡林格（Greenberger-Horne-Zeilinger, GHZ）态扮演着至关重要的角色，它被视为[多体纠缠](@entry_id:142544)最极致、最纯粹的范例。理解[GHZ态](@entry_id:182114)不仅是掌握[量子信息科学](@entry_id:150091)的关键，也为我们提供了一个独特的窗口，以最尖锐的方式审视量子力学与我们日常直觉的根本冲突。

本文旨在系统性地剖析[GHZ态](@entry_id:182114)，填补从抽象理论到实际应用的认知鸿沟。我们将带领读者深入探索这个奇特[量子态](@entry_id:146142)的全貌。文章分为三个核心部分：

在“原理与机制”一章中，我们将从[GHZ态](@entry_id:182114)的数学定义出发，揭示其不可分性与“全或无”的纠缠结构。我们将探讨如何在[量子线路](@entry_id:151866)上生成[GHZ态](@entry_id:182114)，并深入分析其与[局域实在论](@entry_id:144981)的戏剧[性冲突](@entry_id:152298)，即著名的GHZ悖论。同时，我们也将讨论其固有的脆弱性——对环境噪声的极端敏感。

接着，在“应用与跨学科联系”一章中，我们将展示[GHZ态](@entry_id:182114)如何从一个理论奇迹转变为一种强大的资源。我们将探索其在量子通信、[分布式量子计算](@entry_id:153256)、超精密[量子计量学](@entry_id:138980)以及[量子纠错码](@entry_id:266787)中的核心作用，并揭示其与凝聚态物理、相对论等基础学科的深刻联系。

最后，“动手实践”部分将通过一系列精心设计的问题，引导读者亲手计算和验证[GHZ态](@entry_id:182114)的关键性质，将理论知识转化为可操作的技能。通过这一结构化的学习路径，我们希望能为读者揭开[GHZ态](@entry_id:182114)的神秘面纱，领略其在推动量子科技革命中的核心力量。

## 原理与机制

在深入探讨[多体量子系统](@entry_id:161678)的复杂性时，某些特定的[纠缠态](@entry_id:152310)因其独特的结构和[非局域关联](@entry_id:180194)而成为理论与实验研究的基石。其中，Greenberger-Horne-Zeilinger (GHZ) 态是[多体纠缠](@entry_id:142544)最极致、最纯粹的体现之一。本章旨在系统阐述 GHZ 态的核心原理及其相关机制，从其数学定义出发，逐步揭示其生成方法、纠缠结构、非局域特性以及在噪声环境下的演化规律。

### GHZ 态的定义与不[可分性](@entry_id:143854)

一个 $N$ [量子比特](@entry_id:137928)系统的 GHZ 态，在其[标准形式](@entry_id:153058)下，是两个宏观上截然不同的状态的等权重叠加。这两个状态分别是所有[量子比特](@entry_id:137928)都处于 $|0\rangle$ 态和所有[量子比特](@entry_id:137928)都处于 $|1\rangle$ 态。其数学表达式为：

$$
|\text{GHZ}_N\rangle = \frac{1}{\sqrt{2}} \left( |0\rangle^{\otimes N} + |1\rangle^{\otimes N} \right) = \frac{1}{\sqrt{2}} (|00\dots0\rangle + |11\dots1\rangle)
$$

其中，$|0\rangle^{\otimes N}$ 是 $N$ 个[量子比特](@entry_id:137928)的张量积 $|0\rangle \otimes |0\rangle \otimes \dots \otimes |0\rangle$ 的简写。此状态最引人注目的特性是其 **真正的[多体纠缠](@entry_id:142544)** (genuine multipartite entanglement)。这意味着它无法被分解为系统中任何一部分与其余部分之间的双边纠缠，更不能被写成各个独立[量子比特](@entry_id:137928)状态的乘积。

一个可以写成其组成部分[张量积](@entry_id:140694)的[量子态](@entry_id:146142)被称为 **[可分态](@entry_id:142281) (separable state)** 或 **乘积态 (product state)**。对于一个三比特系统，一个[可分态](@entry_id:142281)的形式为 $|\Psi_{\text{prod}}\rangle = |\psi_1\rangle \otimes |\psi_2\rangle \otimes |\psi_3\rangle$，其中 $|\psi_k\rangle = a_k |0\rangle + b_k |1\rangle$ 是第 $k$ 个[量子比特](@entry_id:137928)的独立状态。GHZ 态的本质属性在于它不属于此类。

我们可以通过反证法来严格证明这一点。假设一个三比特 GHZ 态是可分的，即：

$$
\frac{1}{\sqrt{2}}(|000\rangle + |111\rangle) = (a_1 |0\rangle + b_1 |1\rangle) \otimes (a_2 |0\rangle + b_2 |1\rangle) \otimes (a_3 |0\rangle + b_3 |1\rangle)
$$

展开右侧的张量积，我们得到一个包含全部八个计算[基矢](@entry_id:199546) $|000\rangle, |001\rangle, \dots, |111\rangle$ 的线性组合。通过逐一比较等式两侧各个[基矢](@entry_id:199546)的系数，我们可以得到一组方程。例如，比较 $|000\rangle$ 和 $|111\rangle$ 的系数，我们有：

$$
a_1 a_2 a_3 = \frac{1}{\sqrt{2}}
$$
$$
b_1 b_2 b_3 = \frac{1}{\sqrt{2}}
$$

这两个方程立即告诉我们，所有的系数 $a_k$ 和 $b_k$ (对于 $k=1, 2, 3$) 都必须是非零的。然而，当我们考察 GHZ 态中并未出现的[基矢](@entry_id:199546)，例如 $|001\rangle$，其系数必须为零。对于乘积态而言，$|001\rangle$ 的系数是 $a_1 a_2 b_3$。因此，我们必须满足：

$$
a_1 a_2 b_3 = 0
$$

这就产生了一个不可调和的矛盾。一方面，为了匹配 $|000\rangle$ 和 $|111\rangle$ 分量的存在，所有 $a_k$ 和 $b_k$ 都不能为零。另一方面，为了使 $|001\rangle$ 分量消失，至少有一个因子（$a_1$, $a_2$ 或 $b_3$）必须为零。这两个条件无法同时满足，从而证明了我们的初始假设——GHZ 态是可分的——是错误的。因此，GHZ 态是真正纠缠的，它的属性不能归结为各个独立[量子比特](@entry_id:137928)的属性集合 [@problem_id:1651676]。

### GHZ 态的生成与推广

既然 GHZ 态具有如此独特的性质，一个自然的问题是：如何在[量子计算](@entry_id:142712)机或实验装置中制备这样的状态？一个标准的[量子线路](@entry_id:151866)提供了一种系统性的方法。对于三比特系统，我们可以从初始态 $|000\rangle$ 开始。

1.  对第一个[量子比特](@entry_id:137928)施加一个 **Hadamard 门 (H)**。Hadamard 门将 $|0\rangle$ 变为 $\frac{1}{\sqrt{2}}(|0\rangle+|1\rangle)$。此时，系统状态变为 $\frac{1}{\sqrt{2}}(|000\rangle+|100\rangle)$。

2.  接着，以第一个[量子比特](@entry_id:137928)为 **控制比特**，第二个[量子比特](@entry_id:137928)为 **目标比特**，施加一个 **[受控非门](@entry_id:180955) (CNOT)**。CNOT 门的作用是当控制比特为 $|1\rangle$ 时，翻转目标比特。施加 CNOT$_{1,2}$ 后，状态演变为 $\frac{1}{\sqrt{2}}(|000\rangle+|110\rangle)$。

3.  最后，再次以第一个[量子比特](@entry_id:137928)为控制比特，第三个[量子比特](@entry_id:137928)为目标比特，施加第二个 CNOT 门 (CNOT$_{1,3}$)。状态最终变为 $\frac{1}{\sqrt{2}}(|000\rangle+|111\rangle)$，这正是标准的三比特 GHZ 态。

这个流程可以自然地推广到 $N$ 个[量子比特](@entry_id:137928)。

更有趣的是，我们可以通过修改这个基本线路来生成更广义的 GHZ 型态。例如，考虑一个非对称的实系数 GHZ 态：

$$
|\psi_{\text{target}}\rangle = \sqrt{\frac{1}{N+1}}|000\rangle + \sqrt{\frac{N}{N+1}}|111\rangle
$$

其中 $N$ 是一个正实数。为了生成这个状态，我们可以将初始的 Hadamard 门替换为一个绕 y 轴的旋转门 $R_y(\theta)$。该门的作用是 $R_y(\theta)|0\rangle = \cos(\frac{\theta}{2})|0\rangle + \sin(\frac{\theta}{2})|1\rangle$。将此门作用于第一个[量子比特](@entry_id:137928)，然后依次施加 CNOT$_{1,2}$ 和 CNOT$_{1,3}$，得到的最终状态将是：

$$
|\psi_{\text{out}}\rangle = \cos(\tfrac{\theta}{2})|000\rangle + \sin(\tfrac{\theta}{2})|111\rangle
$$

通过将这个输出态与我们的目标态进行比较，可以得到系数之间的关系：$\cos(\frac{\theta}{2}) = \sqrt{\frac{1}{N+1}}$ 和 $\sin(\frac{\theta}{2}) = \sqrt{\frac{N}{N+1}}$。由此可以解出所需的旋转角 $\theta$。两式相除得到 $\tan(\frac{\theta}{2}) = \sqrt{N}$，因此，旋转角为 $\theta = 2\arctan(\sqrt{N})$。这个例子展示了通过精确控制单比特操作，我们可以灵活地制备出具有特定振幅[分布](@entry_id:182848)的广义 GHZ 态 [@problem_id:755304]。

### GHZ 纠缠的结构特征

GHZ 态的纠缠结构非常特殊，通常被称为“全或无”式的纠缠。这与另一类重要的三体[纠缠态](@entry_id:152310)——W 态（例如 $|W\rangle = \frac{1}{\sqrt{3}}(|100\rangle + |010\rangle + |001\rangle)$）——形成鲜明对比。

#### 局域性质与[约化密度矩阵](@entry_id:146315)

要理解一个多体系统中单个子系统的状态，我们需要计算其 **[约化密度矩阵](@entry_id:146315) (reduced density matrix)**。这是通过对系统中其余部分进行求迹 (trace out) 操作得到的。对于一个处于 GHZ 态的三比特系统 $\rho_{123} = |\text{GHZ}\rangle\langle\text{GHZ}|$，如果我们只关心第一个[量子比特](@entry_id:137928)，我们需要对第二和第三个[量子比特](@entry_id:137928)求迹：

$$
\rho_1 = \text{Tr}_{23}(\rho_{123}) = \frac{1}{2} \text{Tr}_{23} \left( (|000\rangle + |111\rangle)(\langle000| + \langle111|) \right)
$$

计算结果为：

$$
\rho_1^{\text{GHZ}} = \frac{1}{2}(|0\rangle\langle0| + |1\rangle\langle1|) = \frac{1}{2} I
$$

这是一个 **[完全混合态](@entry_id:139247) (maximally mixed state)**。它的密度矩阵正比于[单位矩阵](@entry_id:156724) $I$，表示测量该[量子比特](@entry_id:137928)时得到 $|0\rangle$ 和 $|1\rangle$ 的概率完全相等，且不存在任何确定的相位信息。这反映了一个深刻的事实：尽管整个 GHZ 系统处于一个[纯态](@entry_id:141688)，但其任何单个组成部分都处于最无序、最不确定的状态。

与此相反，如果我们对 W 态的第一个[量子比特](@entry_id:137928)计算[约化密度矩阵](@entry_id:146315)，会得到 $\rho_1^{W} = \frac{2}{3}|0\rangle\langle0| + \frac{1}{3}|1\rangle\langle1|$。这是一个[混合态](@entry_id:141568)，但不是[完全混合态](@entry_id:139247)。GHZ 态和 W 态的这种差异，体现在它们[约化密度矩阵](@entry_id:146315)的不同上，可以通过 **[迹距离](@entry_id:142668) (trace distance)** 来量化，它衡量了两个[量子态](@entry_id:146142)的可区分性。GHZ 和 W 态的单比特[约化密度矩阵](@entry_id:146315)之间的[迹距离](@entry_id:142668)不为零（具体为 $\frac{1}{6}$），表明它们在局域上是可区分的 [@problem_id:142060]。

#### 纠缠的分类与变换

这种结构上的差异意味着 GHZ 态和 W 态属于不同的 **纠缠类别**。在[量子信息](@entry_id:137721)理论中，如果两个状态可以通过 **[局域操作和经典通信](@entry_id:136398) (LOCC)** 相互转化，它们就被认为是等价的。GHZ 态和 W 态是不能通过 LOCC 相互转化的，它们代表了三比特系统中两种最基本的、不可约的纠缠形式。

我们可以通过 **[施密特分解](@entry_id:145934) (Schmidt decomposition)** 来更深入地理解这一点。将一个三体态 $|\Psi\rangle_{ABC}$ 视为一个由 A 和 (BC) 组成的二体系统，我们可以找到一组[正交基](@entry_id:264024)，将其写成 $|\Psi\rangle_{ABC} = \sum_i c_i |i\rangle_A |i\rangle_{BC}$。系数 $c_i$ 称为[施密特系数](@entry_id:137823)，它们的大小反映了 A 与 BC 之间的纠缠程度。对于 GHZ 态，分解是：

$$
|\text{GHZ}\rangle = \frac{1}{\sqrt{2}}|0\rangle_A |00\rangle_{BC} + \frac{1}{\sqrt{2}}|1\rangle_A |11\rangle_{BC}
$$

其[施密特系数](@entry_id:137823)为 $\{\frac{1}{\sqrt{2}}, \frac{1}{\sqrt{2}}\}$。而对于 W 态，分解后得到的[施密特系数](@entry_id:137823)为 $\{\frac{\sqrt{2}}{\sqrt{3}}, \frac{1}{\sqrt{3}}\}$。在 LOCC 操作下，最大的[施密特系数](@entry_id:137823) $c_{\max}$ 是一个不会增加的量（称为[纠缠单调](@entry_id:136743)子），由于 $c_{\max, \text{W}} = \frac{\sqrt{2}}{\sqrt{3}} > c_{\max, \text{GHZ}} = \frac{1}{\sqrt{2}}$，这直接证明了从 GHZ 态通过 LOCC 无法制备出 W 态 [@problem_id:2112333]。

#### 关联函数分析

描述 GHZ 态的另一种强大语言是 **关联函数 (correlation functions)**。单比特的性质由局域[布洛赫矢量](@entry_id:144181) $\vec{r}^{(k)}$ 描述，其分量为[泡利算符](@entry_id:144061)的[期望值](@entry_id:153208) $r_i^{(k)} = \text{Tr}(\rho \, \sigma_i^{(k)})$。对于 GHZ 态，由于其单比特[约化密度矩阵](@entry_id:146315)是[完全混合态](@entry_id:139247)，所有的局域[布洛赫矢量](@entry_id:144181)均为[零矢量](@entry_id:155273)：$\vec{r}^{(k)} = \vec{0}$。这意味着在任何方向上测量单个[量子比特](@entry_id:137928)，得到向上或向下自旋的概率都是 $1/2$。

然而，GHZ 态的奇特之处在于其多体关联。对于[三体](@entry_id:265960) GHZ 态，一个显著的特点是任意两个[量子比特](@entry_id:137928)之间的 z 方向[自旋测量](@entry_id:196098)结果总是相同的，这体现为二体关联函数 $\langle\sigma_z^{(a)} \otimes \sigma_z^{(b)}\rangle=1$。与之形成鲜明对比的是，在 x 或 y 方向上，相应的二体关联函数均为零，即 $\langle\sigma_x^{(a)} \otimes \sigma_x^{(b)}\rangle = 0$ 和 $\langle\sigma_y^{(a)} \otimes \sigma_y^{(b)}\rangle = 0$。GHZ 态真正的[非局域性](@entry_id:140165)体现在更高级别的关联上，例如三体关联：
$$
\langle\sigma_x^{(1)} \otimes \sigma_x^{(2)} \otimes \sigma_x^{(3)}\rangle = 1
$$
$$
\langle\sigma_x^{(1)} \otimes \sigma_y^{(2)} \otimes \sigma_y^{(3)}\rangle = -1
$$
$$
\langle\sigma_y^{(1)} \otimes \sigma_x^{(2)} \otimes \sigma_y^{(3)}\rangle = -1
$$
$$
\langle\sigma_y^{(1)} \otimes \sigma_y^{(2)} \otimes \sigma_x^{(3)}\rangle = -1
$$
这些结果表明，尽管单个[量子比特](@entry_id:137928)的行为完全随机，并且某些二体关联不存在，但所有三个[量子比特](@entry_id:137928)的测量结果组合起来却表现出完美的、确定性的关联或反关联。这种“无局域性质但有完美[非局域关联](@entry_id:180194)”的特性，是 GHZ 态的核心特征之一，并直接导致了下一节将要讨论的 GHZ 悖论 [@problem_id:744526]。

### GHZ 态与[局域实在论](@entry_id:144981)的冲突

GHZ 态最深刻的意义在于它为检验量子力学与 **[局域实在论](@entry_id:144981) (local realism)** 的基本冲突提供了一个比[贝尔不等式](@entry_id:156237)更直接、更具戏剧性的舞台。[局域实在论](@entry_id:144981)假设物理对象的属性是客观存在的（实在论），且不受远处事件瞬时影响（局域性）。

#### GHZ 悖论：“没有不等式的[非局域性](@entry_id:140165)”

考虑一个由 Alice、Bob 和 Carol 共享的三比特 GHZ 态。他们各自可以在 x 或 y 方向上测量其[量子比特](@entry_id:137928)的自旋。根据量子力学，这些测量算符（$\sigma_x, \sigma_y$）的[乘积的期望值](@entry_id:201037)可以通过计算 $\langle\text{GHZ}|O|\text{GHZ}\rangle$ 得到，其中 $O$ 是对应于测量组合的张量积算符。

我们来分析两种测量设置：
1.  Alice 测量 $\sigma_x$，Bob 和 Carol 测量 $\sigma_y$。对应的算符是 $O_1 = \sigma_x^{(1)} \otimes \sigma_y^{(2)} \otimes \sigma_y^{(3)}$。
2.  Alice、Bob 和 Carol 都测量 $\sigma_x$。对应的算符是 $O_2 = \sigma_x^{(1)} \otimes \sigma_x^{(2)} \otimes \sigma_x^{(3)}$。

通过直接计算可知，GHZ 态是这两个算符的本征态：

$$
O_1 |\text{GHZ}\rangle = -|\text{GHZ}\rangle
$$
$$
O_2 |\text{GHZ}\rangle = +|\text{GHZ}\rangle
$$

这意味着，在第一种设置下，三次测量结果的乘积总是 $-1$。在第二种设置下，三次测量结果的乘积总是 $+1$ [@problem_id:2130470]。

现在我们从[局域实在论](@entry_id:144981)的角度来看这个问题。该理论假设每个[量子比特](@entry_id:137928)在测量前就已经拥有了在 x 和 y 方向上的确定自旋值，我们分别记为 $m_x^{(k)}$ 和 $m_y^{(k)}$ (其值为 $+1$ 或 $-1$)。那么，上述实验结果可以写成：

1.  $m_x^{(1)} m_y^{(2)} m_y^{(3)} = -1$
2.  $m_x^{(1)} m_x^{(2)} m_x^{(3)} = +1$

同时，通过对称性，我们也应该能推断出另外两个与第一个设置类似的方程：$m_y^{(1)} m_x^{(2)} m_y^{(3)} = -1$ 和 $m_y^{(1)} m_y^{(2)} m_x^{(3)} = -1$。

现在我们将这三个“-1”方程相乘：
$$
(m_y^{(1)} m_x^{(2)} m_y^{(3)}) \cdot (m_y^{(1)} m_y^{(2)} m_x^{(3)}) \cdot (m_x^{(1)} m_y^{(2)} m_y^{(3)}) = (-1)^3 = -1
$$
由于每个 $m$ 值都是 $+1$ 或 $-1$，它们的平方 $(m_i^{(k)})^2$ 总是 $+1$。整理上式，我们得到：
$$
(m_x^{(1)} m_x^{(2)} m_x^{(3)}) \cdot (m_y^{(1)})^2 (m_y^{(2)})^2 (m_y^{(3)})^2 = m_x^{(1)} m_x^{(2)} m_x^{(3)} = -1
$$
这个结论与我们从第二种实验设置中得到的 $m_x^{(1)} m_x^{(2)} m_x^{(3)} = +1$ 直接矛盾。这种非统计性的、确定性的矛盾被称为 GHZ 悖论，它以前所未有的清晰度揭示了量子力学的预言与任何[局域实在论](@entry_id:144981)理论都无法兼容。

#### Mermin 不等式及其违背

GHZ 悖论可以被推广到一个不等式框架中，即 Mermin 不等式。对于三比特系统，Mermin 算符定义为：

$$
M = \sigma_x^{(1)}\sigma_y^{(2)}\sigma_y^{(3)} + \sigma_y^{(1)}\sigma_x^{(2)}\sigma_y^{(3)} + \sigma_y^{(1)}\sigma_y^{(2)}\sigma_x^{(3)} - \sigma_x^{(1)}\sigma_x^{(2)}\sigma_x^{(3)}
$$

任何[局域隐变量理论](@entry_id:203716)都预测，该算符的[期望值](@entry_id:153208) $\langle M \rangle$ 的[绝对值](@entry_id:147688)不会超过 2，即 $|\langle M \rangle| \le 2$。

然而，量子力学的预测是什么呢？我们可以计算 $M$ 在一个广义 GHZ 态 $|\Psi(\phi)\rangle = \frac{1}{\sqrt{2}} (|000\rangle + e^{i\phi} |111\rangle)$ 上的[期望值](@entry_id:153208)。通过计算每个乘积项的[期望值](@entry_id:153208)，我们发现：

$$
\langle\Psi(\phi)| \sigma_x^{(1)}\sigma_y^{(2)}\sigma_y^{(3)} |\Psi(\phi)\rangle = -\cos\phi
$$
$$
\langle\Psi(\phi)| \sigma_x^{(1)}\sigma_x^{(2)}\sigma_x^{(3)} |\Psi(\phi)\rangle = \cos\phi
$$

由于对称性，前三项的[期望值](@entry_id:153208)均为 $-\cos\phi$。因此，总的[期望值](@entry_id:153208)为：

$$
\langle M \rangle = 3(-\cos\phi) - (\cos\phi) = -4\cos\phi
$$

其[绝对值](@entry_id:147688)为 $|\langle M \rangle| = 4|\cos\phi|$。当相位 $\phi=0$ 时（即标准 GHZ 态），这个[期望值](@entry_id:153208)的[绝对值](@entry_id:147688)达到最大值 4，这是[局域实在论](@entry_id:144981)极限 2 的两倍。这种巨大的违背是[量子非局域性](@entry_id:143788)最强有力的证据之一 [@problem_id:755211]。

### GHZ 态的动力学与脆弱性

尽管 GHZ 态在理论上非常强大，但在现实世界中，它们对环境噪声极其敏感，这种特性被称为 **脆弱性 (fragility)**。

#### [退相干](@entry_id:145157)效应

一个常见的[噪声模型](@entry_id:752540)是局域、独立的 **[退相干](@entry_id:145157) (dephasing)**。在这种模型下，每个[量子比特](@entry_id:137928)都以一定的速率 $\Gamma$ 经历相位信息的丢失，其动力学可以用 Lindblad 主方程描述。对于一个初始处于 $|\text{GHZ}_N\rangle$ 态的系统，其[密度矩阵](@entry_id:139892) $\rho(t)$ 会随时间演化。我们特别关心的是描述 $|0\dots0\rangle$ 和 $|1\dots1\rangle$ 之间量子相干性的非对角项 $c(t) = \langle 0\dots0|\rho(t)|1\dots1\rangle$。

通过求解[主方程](@entry_id:142959)，可以发现该相干项随时间的演化遵循一个简单的[微分方程](@entry_id:264184)：

$$
\frac{dc}{dt} = -N\Gamma c(t)
$$

这个方程的解为 $c(t) = c(0) \exp(-N\Gamma t)$。由于初始状态是 GHZ 态， $c(0) = 1/2$，所以相干项的幅度为：

$$
|\langle 0\dots0|\rho(t)|1\dots1\rangle| = \frac{1}{2}\exp(-N\Gamma t)
$$

这个结果揭示了一个至关重要的现象：GHZ 态的相干性衰减速率与[量子比特](@entry_id:137928)的数量 $N$ 成正比。这种效应有时被称为 **超退相干 (superdecoherence)**。这意味着随着系统规模的增大，GHZ 态的纠缠会以指数级加速的方式消失。这种对噪声的极端敏感性使得在实验中制备和维持大规模的 GHZ 态成为一项巨大的挑战 [@problem_id:755213]。

#### 测量 induced dynamics

GHZ 态的“全或无”特性也在测量过程中得到体现。考虑一个 $N$ 比特 GHZ 态，如果我们对其中一个[量子比特](@entry_id:137928)（例如第一个）进行投影测量，但我们不知道测量的具体结果，那么剩余 $N-1$ 个[量子比特](@entry_id:137928)会处于一个什么样的状态？

假设我们在任意基 $\{|v_1\rangle, |v_2\rangle\}$ 下测量第一个比特。得到结果 $|v_m\rangle$ 的概率是 $p_m = 1/2$，与测量基的选择无关。如果得到了结果 $|v_m\rangle$，剩余的 $N-1$ 个比特会塌缩到一个新的纯态 $|\psi_m\rangle$。由于我们不知道结果，[剩余系](@entry_id:637054)统的状态是一个混合态 $\rho_{\text{rem}} = \frac{1}{2}|\psi_1\rangle\langle\psi_1| + \frac{1}{2}|\psi_2\rangle\langle\psi_2|$。

现在，如果我们从这剩余的 $N-1$ 个[量子比特](@entry_id:137928)中再挑选任意一个（例如第 $k$ 个），并计算它的[约化密度矩阵](@entry_id:146315) $\rho_k$，我们会发现一个惊人的结果：无论最初对第一个[量子比特](@entry_id:137928)的测量基是什么，$\rho_k$ 总是处于[完全混合态](@entry_id:139247) $\frac{1}{2}I$。这意味着，对于一个对测量结果一无所知的外部观察者来说，[剩余系](@entry_id:637054)统中的任何单个[量子比特](@entry_id:137928)都表现为完全随机。

这个状态的 **[冯·诺依曼熵](@entry_id:143216) (von Neumann entropy)** $S(\rho) = -\text{Tr}(\rho \log_2 \rho)$ 是衡量[量子态](@entry_id:146142)不确定性或混合程度的指标。对于[完全混合态](@entry_id:139247) $\rho_k = \text{diag}(\frac{1}{2}, \frac{1}{2})$，其熵为 $S(\rho_k) = -(\frac{1}{2}\log_2\frac{1}{2} + \frac{1}{2}\log_2\frac{1}{2}) = 1$ 比特。这个最大熵值表明，在对第一个[量子比特](@entry_id:137928)进行测量后（结果未知），任何一个剩余的[量子比特](@entry_id:137928)自身所包含的信息都降为零，其状态变得完全不可预测 [@problem_id:755345]。这再次凸显了 GHZ 态的极端整体性：对其任何局部的扰动都会深刻地、非局域地影响整个系统的关联结构。