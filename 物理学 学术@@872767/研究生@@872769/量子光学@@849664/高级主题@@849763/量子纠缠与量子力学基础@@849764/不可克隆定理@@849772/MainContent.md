## 引言
在经典世界里，复制信息是一项司空见惯且微不足道的操作。然而，当我们进入由量子力学主宰的微观领域时，这一直观的动作却遇到了一个根本性的障碍：一个任意的、未知的[量子态](@entry_id:146142)是无法被完美复制的。这便是著名的“[不可克隆定理](@entry_id:146200)”，它是量子信息论的基石之一，深刻地揭示了量子信息与经典信息的本质区别。这一定理并非量子世界的缺陷，而是其内在规律的体现，它为量子技术开启了独特的可能性，尤其是在信息安全领域。

本文旨在系统地剖析[不可克隆定理](@entry_id:146200)。我们将从其最基本的原理出发，揭示为何复制在量子世界中是被禁止的，并探讨这一“禁令”所带来的一系列深远推论。读者将通过本文学习到：

- 在**第一章：原理与机制**中，我们将深入探讨[不可克隆定理](@entry_id:146200)的严格数学证明，理解它如何根植于[量子力学的线性](@entry_id:146991)与幺正性公理。我们还将探索相关的“禁行”定理，如不可区分和不可删除定理，并研究在完美克隆不可能的情况下，我们能做到的最佳近似——[最优量子克隆](@entry_id:195904)。

- 在**第二章：应用与跨学科联系**中，我们将展示[不可克隆定理](@entry_id:146200)如何从一个理论约束转变为一项强大的应用工具。我们将看到它如何保障[量子密钥分发](@entry_id:138070)（QKD）的[绝对安全](@entry_id:262916)，如何重塑量子纠错码的设计[范式](@entry_id:161181)，并探索其在[黑洞信息悖论](@entry_id:140140)、[量子达尔文主义](@entry_id:148606)等基础物理前沿问题中的深刻启示。

- 在**第三章：动手实践**中，读者将通过一系列精心设计的问题，将理论知识付诸实践，计算近似克隆的保真度，分析窃听策略，并探索克隆在更高维度系统中的限制，从而巩固对这一定理的理解。

通过这三个层面的学习，我们将共同揭示[不可克隆定理](@entry_id:146200)如何不仅划定了[量子信息处理](@entry_id:158111)的边界，更指明了通往下一代[量子技术](@entry_id:142946)的独特道路。

## 原理与机制

量子力学的基本公理，特别是其线性和幺正性，对信息处理施加了深刻的限制。这些限制并非缺陷，而是量子世界与经典世界之间根本差异的体现。本章将深入探讨这些原理，从著名的[不可克隆定理](@entry_id:146200)开始，揭示其背后的机制、相关推论以及在近似操作领域中的可能性。

### 基本禁令：[不可克隆定理](@entry_id:146200)

在[经典计算](@entry_id:136968)中，复制信息是一个微不足道的操作。我们可以读取一个比特的值（0或1），然后将该值写入任意数量的其他比特。然而，在量子世界中，一个任意的未知[量子态](@entry_id:146142)是无法被完美复制的。这便是**[不可克隆定理](@entry_id:146200)（No-cloning Theorem）**。

该定理的正式表述是：不存在一个幺正算符 $U$ 和一个固定的初始辅助粒子（ancilla）态 $|A_0\rangle$，能够对任意输入的[量子比特](@entry_id:137928)态 $|\psi\rangle$ 和一个标准“空白”态 $|s\rangle$ 实现如下转换：
$$ U (|\psi\rangle \otimes |s\rangle \otimes |A_0\rangle) = |\psi\rangle \otimes |\psi\rangle \otimes |A'\rangle $$
其中 $|A'\rangle$ 是辅助粒子演化后的末态。通常，我们可以简化这个表述，忽略辅助粒子，并假设空白态为 $|0\rangle$，即一个理想的克隆操作应满足：
$$ U (|\psi\rangle \otimes |0\rangle) = |\psi\rangle \otimes |\psi\rangle $$
对于任意的 $|\psi\rangle$。接下来，我们将通过两种不同的论证方式证明这样的通用克隆操作是不可能存在的。

#### 证明一：与[线性原理](@entry_id:170988)的矛盾

量子力学的一个核心公设是**[线性原理](@entry_id:170988)**：一个算符作用于态的叠加，等于该算符分别作用于各个态之后的叠加。我们将证明，一个假设的[通用量子克隆机](@entry_id:146760)的定义与[量子力学的线性](@entry_id:146991)原理直接冲突。

让我们考虑一个假想的“通用量子复印机”（UQC），它被设计用来执行上述的克隆操作。我们以一个叠加态作为输入来检验其有效性，例如 $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$。输入系统的完整状态为 $|+\rangle \otimes |0\rangle$。我们可以通过两种方式预测输出状态 [@problem_id:1429354]。

**方法A：直接应用克隆定义**
如果我们假设克隆机的定义对叠加态 $|+\rangle$ 本身成立，那么输出就应该是两份 $|+\rangle$ 的拷贝：
$$ |\Psi_A\rangle = |+\rangle \otimes |+\rangle = \left( \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle) \right) \otimes \left( \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle) \right) $$
$$ |\Psi_A\rangle = \frac{1}{2}(|00\rangle + |01\rangle + |10\rangle + |11\rangle) $$
这是一个可分离态，表示两个[量子比特](@entry_id:137928)都独立地处于 $|+\rangle$ 态。

**方法B：应用[线性原理](@entry_id:170988)**
如果我们假设克隆算符 $U$ 必须遵守[线性原理](@entry_id:170988)，我们首先要将输入态写成基[态的叠加](@entry_id:273993)形式，然后将 $U$ 分别作用于每一项：
$$ |\Psi_B\rangle = U(|+\rangle \otimes |0\rangle) = U \left( \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle) \otimes |0\rangle \right) $$
$$ |\Psi_B\rangle = \frac{1}{\sqrt{2}} U(|0\rangle \otimes |0\rangle) + \frac{1}{\sqrt{2}} U(|1\rangle \otimes |0\rangle) $$
根据克隆机的定义，它必须能完美克隆[基态](@entry_id:150928) $|0\rangle$ 和 $|1\rangle$：
$$ U(|0\rangle \otimes |0\rangle) = |00\rangle $$
$$ U(|1\rangle \otimes |0\rangle) = |11\rangle $$
将此代入上式，我们得到：
$$ |\Psi_B\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle) $$
这个结果是一个最大纠缠的[贝尔态](@entry_id:140749)。

显然， $|\Psi_A\rangle \neq |\Psi_B\rangle$。两种合理的假设——通用克隆机的存在性与[量子力学的线性](@entry_id:146991)原理——导出了相互矛盾的结论。由于[线性原理](@entry_id:170988)是量子力学不可动摇的基石，我们必须放弃[通用量子克隆机](@entry_id:146760)存在的可能性。这个简单的例子揭示了[不可克隆定理](@entry_id:146200)的本质：克隆操作本质上是一个**[非线性](@entry_id:637147)**的过程，因为它试图将一个线性叠加态的演化（产生纠缠）和一个整体的复制（产生可分离态）强行等同起来。

#### 证明二：与幺正性的矛盾

量子系统的演化由**幺正算符**描述。幺正性的一个基本推论是它保持了[量子态](@entry_id:146142)之间的**[内积](@entry_id:158127)**。即对于任意两个态 $|\Phi_1\rangle$ 和 $|\Phi_2\rangle$，以及任意幺正算符 $U$，它们演化后的[内积](@entry_id:158127)不变：$\langle \Phi_1 | \Phi_2 \rangle = \langle U\Phi_1 | U\Phi_2 \rangle$。我们可以利用这一性质来提供一个更普适的证明。

假设存在一个幺正的克隆算符 $U$。我们选取两个不同的、非正交的单[量子比特](@entry_id:137928)态 $|\psi_A\rangle$ 和 $|\psi_B\rangle$ [@problem_id:1368640]。这意味着它们的[内积](@entry_id:158127) $\langle\psi_A|\psi_B\rangle$ 不为零也不为一。

初始时，我们有两个系统，一个待克隆的[量子比特](@entry_id:137928)和另一个处于空白态 $|0\rangle$ 的[量子比特](@entry_id:137928)。对应于 $|\psi_A\rangle$ 和 $|\psi_B\rangle$ 的两个初始态分别是：
$$ |\Phi_{in, A}\rangle = |\psi_A\rangle \otimes |0\rangle $$
$$ |\Phi_{in, B}\rangle = |\psi_B\rangle \otimes |0\rangle $$
这两个初始态的[内积](@entry_id:158127)为：
$$ \langle \Phi_{in, A} | \Phi_{in, B} \rangle = (\langle \psi_A| \otimes \langle 0|) (|\psi_B\rangle \otimes |0\rangle) = \langle \psi_A | \psi_B \rangle \langle 0 | 0 \rangle = \langle \psi_A | \psi_B \rangle $$

经过假设的幺正克隆算符 $U$ 作用后，末态分别为：
$$ |\Phi_{out, A}\rangle = |\psi_A\rangle \otimes |\psi_A\rangle $$
$$ |\Phi_{out, B}\rangle = |\psi_B\rangle \otimes |\psi_B\rangle $$
这两个末态的[内积](@entry_id:158127)为：
$$ \langle \Phi_{out, A} | \Phi_{out, B} \rangle = (\langle \psi_A| \otimes \langle \psi_A|) (|\psi_B\rangle \otimes |\psi_B\rangle) = \langle \psi_A | \psi_B \rangle \langle \psi_A | \psi_B \rangle = (\langle \psi_A | \psi_B \rangle)^2 $$

由于 $U$ 是幺正的，初末态的[内积](@entry_id:158127)必须相等：
$$ \langle \psi_A | \psi_B \rangle = (\langle \psi_A | \psi_B \rangle)^2 $$
令 $x = \langle \psi_A | \psi_B \rangle$，方程变为 $x = x^2$，其解为 $x=0$ 或 $x=1$。
- $x = 0$ 意味着 $\langle \psi_A | \psi_B \rangle = 0$，即两个态是**正交**的。
- $x = 1$ 意味着 $|\psi_A\rangle$ 和 $|\psi_B\rangle$ 是同一个态（在忽略[全局相位](@entry_id:147947)的情况下）。

这表明，一个幺正的克隆过程最多只能完美克隆一组相互正交的特定[基态](@entry_id:150928)，而不能克隆任意的、非正交的[量子态](@entry_id:146142)。由于一个希尔伯特空间充满了无穷多个非正交的态，一个能够克隆“任意”未知态的“通用”克隆机因此是不可能存在的。

### 更广泛的推论与相关的“禁行”定理

[不可克隆定理](@entry_id:146200)的影响远不止于复制信息本身。它是[量子信息论](@entry_id:141608)中一系列“禁行”（no-go）定理的基石，这些定理共同描绘了量子世界中信息处理的边界。

#### 不可区分非正交态

[不可克隆定理](@entry_id:146200)的一个直接且深刻的推论是，我们无法完美地区分两个非正交的[量子态](@entry_id:146142)。这也被称为**不可区分定理（no-distinguishing theorem）**。其逻辑联系非常直接：如果存在一个设备可以确定性地、无差错地区分两个非正交态 $|\psi_1\rangle$ 和 $|\psi_2\rangle$，那么我们就可以构建一个完美的克隆机。具体方法是：首先使用该设备测量输入态，确定它是 $|\psi_1\rangle$ 还是 $|\psi_2\rangle$；然后根据测量结果，使用标准设备制备出任意多份该状态的拷贝。由于克隆是禁止的，因此完美的区分也必然是被禁止的。

我们可以通过[广义测量](@entry_id:154280)（[POVM](@entry_id:138770)）的形式来更严格地证明这一点 [@problem_id:2095912]。一个用于区分两个态的测量过程可以由一组测量算符 $\{E_1, E_2\}$ 描述，它们满足[完备性关系](@entry_id:139077) $E_1 + E_2 = I$，且均为正半定算符。如果输入态为 $|\psi\rangle$，得到结果 $i$ 的概率为 $P(i|\psi) = \langle\psi|E_i|\psi\rangle$。

完美无误的区分要求：
1.  如果输入是 $|\psi_1\rangle$，必须以 $100\%$ 的概率得到结果1： $P(1|\psi_1) = \langle\psi_1|E_1|\psi_1\rangle = 1$。
2.  如果输入是 $|\psi_2\rangle$，必须以 $100\%$ 的概率得到结果2： $P(2|\psi_2) = \langle\psi_2|E_2|\psi_2\rangle = 1$。

由于 $E_1+E_2=I$，第一个条件等价于 $\langle\psi_1|E_2|\psi_1\rangle = 0$。因为 $E_2$ 是正算符，这进一步要求 $E_2|\psi_1\rangle=0$。同理，第二个条件要求 $E_1|\psi_2\rangle=0$。

现在，我们来计算这两个态的[内积](@entry_id:158127)：
$$ \langle\psi_1|\psi_2\rangle = \langle\psi_1|I|\psi_2\rangle = \langle\psi_1|(E_1+E_2)|\psi_2\rangle = \langle\psi_1|E_1|\psi_2\rangle + \langle\psi_1|E_2|\psi_2\rangle $$
由于 $E_1|\psi_2\rangle=0$，第一项为零。由于 $E_2|\psi_1\rangle=0$，其[厄米共轭](@entry_id:191215) $\langle\psi_1|E_2^\dagger = \langle\psi_1|E_2$ 也为零，因此第二项也为零。
最终我们得到：
$$ \langle\psi_1|\psi_2\rangle = 0 $$
这个结果表明，只有当两个态是正交的时候，才可能被确定性地区分。对于任何非正交态（例如 $|\psi_1\rangle = |0\rangle$ 和 $|\psi_2\rangle = \frac{\sqrt{3}}{2}|0\rangle + \frac{1}{2}|1\rangle$），它们的[内积](@entry_id:158127)不为零，因此任何物理设备都无法保证 $100\%$ 准确地区分它们。

#### 不可删除定理

[量子力学的线性](@entry_id:146991)也禁止了克隆的时间反演过程——**通用量子删除（no-deleting theorem）**。该定理指出，不存在一个通用操作可以将两份相同的任意未知[量子态](@entry_id:146142) $|\psi\rangle|\psi\rangle$ 转换为一个 $|\psi\rangle$ 和一个标准空白态 $|0\rangle$。即 $|\psi\rangle|\psi\rangle \to |\psi\rangle|0\rangle$ 这样的转换对于任意 $|\psi\rangle$ 是不可能实现的。

与[不可克隆定理](@entry_id:146200)类似，我们可以通过一个简单的例子来揭示其与[线性原理](@entry_id:170988)的冲突 [@problem_id:159139]。考虑一个假设的线性机器，它被设计用来完美删除计算[基态](@entry_id:150928)：
1.  $U (|0\rangle|0\rangle) = |0\rangle|0\rangle$
2.  $U (|1\rangle|1\rangle) = |1\rangle|0\rangle$

现在，我们将两份叠加态 $|\phi\rangle = a|0\rangle + b|1\rangle$ （其中 $|a|^2+|b|^2=1$）输入该机器。输入态为：
$$ |\Psi_{in}\rangle = |\phi\rangle \otimes |\phi\rangle = a^2|00\rangle + ab(|01\rangle+|10\rangle) + b^2|11\rangle $$
由于机器是线性的，我们只需将 $U$ 作用于[基态展开](@entry_id:190117)的每一项。为了使 $U$ 在整个希尔伯特空间上是幺正的，我们需要定义它在正交补空间上的行为，一个自然的选择是 $U|01\rangle = |01\rangle$ 和 $U|10\rangle = |11\rangle$。则输出态为：
$$ |\Psi_{out}\rangle = U|\Psi_{in}\rangle = a^2|00\rangle + ab|01\rangle + ab|11\rangle + b^2|10\rangle $$
整理后得到：
$$ |\Psi_{out}\rangle = |0\rangle \otimes (a^2|0\rangle + ab|1\rangle) + |1\rangle \otimes (b^2|0\rangle + ab|1\rangle) $$
这个输出态是纠缠的。第一个[量子比特](@entry_id:137928)的最终状态是一个[混合态](@entry_id:141568)，其[约化密度矩阵](@entry_id:146315) $\rho_1$ 并非纯态 $|\phi\rangle\langle\phi|$。例如，当输入态为 $|\phi\rangle = \frac{1}{\sqrt{3}}|0\rangle + \sqrt{\frac{2}{3}}|1\rangle$ 时，可以计算出第一个[量子比特](@entry_id:137928)的末态纯度 $P = \text{Tr}(\rho_1^2) = \frac{77}{81}$，它显著小于1。这表明，原始[量子比特](@entry_id:137928)的状态被破坏了，并没有像预期的那样被“保留”下来。因此，一个通用的删除操作是不可能的。

#### 不可能实现的通用非门

另一个被禁止的操作是**“通用非门”（universal-NOT gate）**。这样的门可以将任意输入的单[量子比特](@entry_id:137928)态 $|\psi\rangle$ 转换为其精确的正交态 $|\psi^\perp\rangle$。例如，对于 $|\psi\rangle = a|0\rangle + b|1\rangle$，其正交态为 $|\psi^\perp\rangle = -b^*|0\rangle + a^*|1\rangle$。这种转换同样与[线性原理](@entry_id:170988)相悖。考虑作用于两个不同[态的叠加](@entry_id:273993) $|\Psi\rangle = c_1|\psi_1\rangle + c_2|\psi_2\rangle$。线性要求输出为 $U|\Psi\rangle = c_1 U|\psi_1\rangle + c_2 U|\psi_2\rangle = c_1 |\psi_1^\perp\rangle + c_2 |\psi_2^\perp\rangle$。而通用[非门](@entry_id:169439)的定义则要求输出为 $|\Psi^\perp\rangle$，这两个结果通常是不同的。因此，完美的通用非门也是不存在的。

### 可能的领域：最优近似克隆

“禁行”定理虽然设定了严格的界限，但也激发了一个富有成果的研究领域：既然完美的操作不可能，那么我们能做出的**最佳近似**是什么？这个问题将我们从绝对的“是”与“否”带入一个充满权衡和优化的灰色地带。

**保真度**（Fidelity）是衡量近似克隆质量的核心指标。对于一个输入为[纯态](@entry_id:141688) $|\psi\rangle$ 的克隆过程，其中一个输出克隆品的[约化密度矩阵](@entry_id:146315)为 $\rho_{clone}$，则该克隆品的保真度定义为 $F = \langle\psi|\rho_{clone}|\psi\rangle$。$F=1$ 表示完美克隆，$F  1$ 则表示不完美或近似克隆。

#### 简单克隆器的局限性

让我们考察一个只被设计用来完美克隆计算[基态](@entry_id:150928) $\{|0\rangle, |1\rangle\}$ 的“有限”克隆器 [@problem_id:159239]。其操作由线性扩展的以下规则定义：
$$ U (|0\rangle_1 \otimes |0\rangle_2) = |0\rangle_1 \otimes |0\rangle_2 $$
$$ U (|1\rangle_1 \otimes |0\rangle_2) = |1\rangle_1 \otimes |1\rangle_2 $$
当输入是叠加态 $|\psi\rangle_1 = \frac{1}{\sqrt{2}}(|0\rangle_1 + |1\rangle_1)$ 时，根据[线性原理](@entry_id:170988)，实际输出为：
$$ |\psi_{out}\rangle = \frac{1}{\sqrt{2}} (|0\rangle_1 |0\rangle_2 + |1\rangle_1 |1\rangle_2) $$
这是一个[贝尔态](@entry_id:140749)。而理想的克隆结果应该是：
$$ |\psi_{ideal}\rangle = |\psi\rangle_1 \otimes |\psi\rangle_2 = \frac{1}{2} (|00\rangle + |01\rangle + |10\rangle + |11\rangle) $$
这两个态显然不同。我们可以计算实际输出与理想输出之间的保真度 $F_{total} = |\langle \psi_{ideal} | \psi_{out} \rangle|^2$。计算得到 $\langle \psi_{ideal} | \psi_{out} \rangle = 1/\sqrt{2}$，因此 $F_{total} = 1/2$。这定量地表明，即便是这样一个简单的克隆器，在处理叠加态时，其克隆效果也远非完美。

#### 最优通用[量子克隆](@entry_id:138347)

上述例子引出了一个更普遍的问题：对于任意输入态，能实现的最佳克隆保真度是多少？这一问题的答案取决于克隆的份数以及对输出克隆品的要求。

**1. 对称克隆**

在**通用对称[量子克隆](@entry_id:138347)机（UQCM）**中，所有输出的 $M$ 份克隆品都是不可区分的，因此它们的保真度都相等，记为 $F$。对于一个从 $1$ 份输入到 $M$ 份输出的通用对称克隆过程（以[量子比特](@entry_id:137928)为例），其可实现的最大保真度有一个确定的上限 [@problem_id:159118]：
$$ F_{max} = \frac{2M+1}{3M} $$
这个著名的公式揭示了[量子信息](@entry_id:137721)的基本稀释规律：
-   对于 $1 \to 2$ 克隆，$M=2$，最大保真度为 $F_{max} = 5/6 \approx 0.833$。
-   当克隆份数非常大时 ($M \to \infty$)，保真度的极限为 $F_{max} \to 2/3$。

这意味着，无论我们制造多少份克隆，都永远无法达到完美的保真度。每一次克隆操作，原始[量子态](@entry_id:146142)中携带的信息都会被不可避免地“稀释”到更大的[希尔伯特空间](@entry_id:261193)中。

**2. 非对称克隆**

如果我们放宽所有克隆品质量必须相同的对称性要求，就可以在不同克隆品的保真度之间进行权衡，这便是**非对称克隆**。例如，在 $1 \to 2$ 的非对称克隆中，我们可以让一个克隆品（$F_1$）的质量更高，代价是另一个克隆品（$F_2$）的质量下降。

这些保真度对 $(F_1, F_2)$ 的取值范围并非任意，而是受限于一个明确的边界。
-   对于**通用克隆**（适用于布洛赫球上所有态），最优保真度边界由方程 $4(F_1^2 + F_2^2 + F_1 F_2) - 8(F_1 + F_2) + 5 = 0$ 描述 [@problem_id:159119]。例如，如果一个克隆器的设计使得 $F_2 = 2/3$，我们可以通过解这个二次方程得到第一个克隆品能达到的最大保真度为 $F_1 = \frac{4 + \sqrt{3}}{6} \approx 0.955$。
-   对于一类特殊的**相位[协变](@entry_id:634097)克隆**（phase-covariant cloner），它专门用于克隆布洛赫球赤道上的态，其保真度边界关系更为简洁 [@problem_id:159241]：$(2F_1 - 1)^2 + (2F_2 - 1)^2 = 1$。这个关系描述了在 $(2F_1-1, 2F_2-1)$ 平面上的一个圆。从这个方程可以解出 $F_2$ 与 $F_1$ 的函数关系：$F_2 = \frac{1}{2} + \sqrt{F_1(1-F_1)}$（假设 $F_1 \ge F_2$）。这个关系的两个极端情况极具启发性：
    -   $(F_1, F_2) = (1, 1/2)$：这对应于将原始[量子比特](@entry_id:137928)完美传输给第一个输出端口，而第二个输出端口则得到一个完全随机的态（其保真度恒为 $1/2$）。
    -   $(F_1, F_2) = (1/2, 1)$：与上一种情况对称。

#### 近似其他禁止操作

近似的思想同样适用于其他“禁行”定理。例如，虽然完美的通用非门不存在，但我们可以构建一个近似的通用非门，并评估其性能。评估其整体性能的一个好方法是计算其保真度在所有可能输入态（整个[布洛赫球面](@entry_id:138823)）上的平均值 $\bar{F}$。对于任意单比特幺正操作 $U$，其作为通用[非门](@entry_id:169439)的最佳平均保真度为 [@problem_id:764773]：
$$ \bar{F}_{max} = \frac{2}{3} $$
这个 $2/3$ 的数值再次出现并非偶然，它与 $1 \to \infty$ 克隆的保真度极限相同，暗示了在量子信息论的约束下，不同任务之间存在深刻的内在联系。

#### 理论基础：对称性原理

最优克隆的这些数值界限并非偶然，它们源于深刻的对称性原理。一个“通用”的克隆机，其克隆质量不应依赖于输入态，这意味着克隆过程必须在态空间的所有旋转下保持[协变](@entry_id:634097)。这个物理要求在数学上体现为克隆变换必须是一个 **SU(2) 互缠算符（intertwiner）**。

具体来说，一个 $1 \to 2$ 的通用对称克隆过程，其输入态 $|\psi\rangle$ 属于自旋-$1/2$表示（$J=1/2$），而两个输出克隆品由于对称性要求，其联合状态必须处于它们的对称[子空间](@entry_id:150286)，该[子空间](@entry_id:150286)对应于自旋-$1$表示（$J=1$）。根据[角动量耦合](@entry_id:145967)规则（Clebsch-Gordan 分解），从 $J=1/2$ 空间到 $J=1$ 空间的映射需要一个[辅助系统](@entry_id:142219)（ancilla）的参与，而这个[辅助系统](@entry_id:142219)本身也必须携带合适的表示。为了满足通用性和对称性的所有约束，可以证明，实现最优 $1 \to 2$ 通用对称克隆所需的[辅助系统](@entry_id:142219)，其希尔伯特空间的最小维度为3 [@problem_id:764758]。这个结论将抽象的对称性要求与克隆机所需的具体物理资源联系在了一起，展示了量子信息论中基本原理的力量。