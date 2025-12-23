## 引言
[量子计算](@entry_id:142712)承诺通过利用量子力学现象来彻底改变我们处理复杂问题的方式。但这种变革力量并非凭空而来，它的核心在于一套精确而独特的计算指令——量子门与[量子线路](@entry_id:151866)。它们是构建量子算法、运行量子模拟的基石，如同经典计算机中的逻辑门与电路一样，是连接抽象理论与实际计算的桥梁。

然而，从理解[量子比特](@entry_id:137928)的叠加与纠缠到真正构建一个有用的量子程序，存在一个关键的知识鸿沟：我们究竟如何精确地操控这些[量子态](@entry_id:146142)，并让它们以可控的方式相互作用来执行计算？

本文旨在系统性地解答这一问题。在**“原理与机制”**一章中，我们将深入探讨[量子操作](@entry_id:145906)必须遵循的[幺正性](@entry_id:138773)与线性等基本原则，并详细介绍包括[泡利门](@entry_id:139600)、[阿达玛门](@entry_id:146898)和CNOT门在内的基本量子门，揭示它们如何构建[量子线路](@entry_id:151866)并产生纠缠。接着，在**“应用与[交叉](@entry_id:147634)学科联系”**一章中，我们将展示这些[量子线路](@entry_id:151866)如何构成强大的[量子算法](@entry_id:147346)、模拟复杂的物理与化学系统，并为量子纠错等前沿技术提供支持，突显其在多个科学领域的广泛影响。最后，通过**“动手实践”**部分，你将有机会将理论付诸实践，通过具体练习来巩固对[量子态](@entry_id:146142)操控和线路构建的理解。

让我们首先深入[量子计算](@entry_id:142712)的核心，探索那些驱动一切的普适原理与基础构件。

## 原理与机制

与遵循[布尔逻辑](@entry_id:143377)确定性规则的经典计算不同，[量子计算](@entry_id:142712)的运作基于量子力学的独特原理。这些原理不仅赋予了[量子计算](@entry_id:142712)潜在的强大能力，也引入了一套全新的操作规则和限制。本章将深入探讨驱动量子门和[量子线路](@entry_id:151866)的基本原理与核心机制，从[量子操作](@entry_id:145906)的普适约束到构建复杂[量子算法](@entry_id:147346)的具体工具。

### [量子操作](@entry_id:145906)的基本原则

[量子计算](@entry_id:142712)中的每一个操作，无论是作用于单个[量子比特](@entry_id:137928)还是多个[量子比特](@entry_id:137928)，都必须遵循量子力学的基本公设。这些公设中最关键的两个是幺正性（Unitarity）和线性（Linearity）。它们共同构成了[量子信息处理](@entry_id:158111)的基石，并导致了一些与经典直觉截然不同的结论。

#### 幺正性与可逆性

量子系统的[时间演化](@entry_id:153943)由薛定谔方程描述，其解是一个幺正算符。在[量子计算](@entry_id:142712)的门模型中，这意味着任何[量子逻辑门](@entry_id:142100)都必须由一个**幺[正矩阵](@entry_id:149490)** $U$ 来表示。一个矩阵 $U$ 被称为幺正的，如果其[共轭转置](@entry_id:147909) $U^\dagger$ 同时也是它的[逆矩阵](@entry_id:140380)，即 $U^\dagger U = U U^\dagger = I$，其中 $I$ 是单位矩阵。

这个看似纯粹的数学要求，对[量子计算](@entry_id:142712)的性质有着深远的影响。最直接的推论是，所有由[量子门](@entry_id:143510)组成的计算过程本质上都是**可逆的**。假设一个量子门 $U$ 将一个初始状态 $|\psi\rangle$ 演化为一个末态 $|\psi'\rangle = U|\psi\rangle$。由于 $U$ 是幺正的，我们总可以找到另一个[量子门](@entry_id:143510)，即 $U^\dagger$，作用于末态上，从而完美地恢复初始状态：

$$
U^\dagger |\psi'\rangle = U^\dagger (U|\psi\rangle) = (U^\dagger U)|\psi\rangle = I|\psi\rangle = |\psi\rangle
$$

这个性质可以推广到由多个[量子门](@entry_id:143510) $U_1, U_2, \dots, U_n$ 组成的整个[量子线路](@entry_id:151866)。整个线路的总操作可以表示为矩阵乘积 $U_{\text{total}} = U_n \dots U_2 U_1$。由于幺[正矩阵](@entry_id:149490)的乘积仍然是幺正的，所以 $U_{\text{total}}$ 也是一个幺正算符。因此，整个计算过程可以通过应用其逆操作 $U_{\text{total}}^\dagger = U_1^\dagger U_2^\dagger \dots U_n^\dagger$ 来精确地倒转。

这种固有的可逆性是[量子计算](@entry_id:142712)与[经典计算](@entry_id:136968)的一个根本区别。例如，一个经典的“或”门（OR gate）是不可逆的。如果一个OR门的输出是1，我们无法唯一地确定其输入是 (0, 1), (1, 0) 还是 (1, 1)。信息在操作过程中丢失了。而在[量子计算](@entry_id:142712)中，[幺正演化](@entry_id:145020)保证了[信息守恒](@entry_id:634303)；不同的初始状态在经过任何[量子线路](@entry_id:151866)后，绝不会被映射到完全相同的末态 。这种可逆性是设计[量子算法](@entry_id:147346)时必须考虑的一个核心特征。

#### 线性与不可克隆原理

量子力学的另一个基石是**[线性原理](@entry_id:170988)**。这意味着[量子门](@entry_id:143510)对于量子态的叠加是线性作用的。对于任意一个[量子算符](@entry_id:137703) $U$，以及任意两个[量子态](@entry_id:146142) $|\psi_1\rangle$ 和 $|\psi_2\rangle$ 的线性叠加 $c_1|\psi_1\rangle + c_2|\psi_2\rangle$，其作用结果为：

$$
U(c_1|\psi_1\rangle + c_2|\psi_2\rangle) = c_1 U|\psi_1\rangle + c_2 U|\psi_2\rangle
$$

这个原理保证了量子系统在[演化过程](@entry_id:175749)中，叠加态的各个分量是独立演化的。然而，[线性原理](@entry_id:170988)也带来了一个深刻的限制——**不可克隆原理**（No-Cloning Theorem）。该原理指出，不存在一个通用的量子门，能够精确复制一个任意的、未知的[量子态](@entry_id:146142)。

我们可以通过一个思想实验来证明这一点 。假设存在一个理想的克隆门 $U_C$，它的功能是将一个任意的输入[量子比特](@entry_id:137928) $|\psi\rangle$ 和一个处于标准“空白”态 $|0\rangle$ 的辅助比特作为输入，输出两个都处于 $|\psi\rangle$ 态的[量子比特](@entry_id:137928)。其数学表达式为 $U_C (|\psi\rangle \otimes |0\rangle) = |\psi\rangle \otimes |\psi\rangle$。

由于 $U_C$ 必须是一个线性算符，它的行为完全由其在[基态](@entry_id:150928)上的作用决定。对于计算[基态](@entry_id:150928) $|0\rangle$ 和 $|1\rangle$，这个克隆操作应该是：
$U_C(|0\rangle|0\rangle) = |0\rangle|0\rangle$
$U_C(|1\rangle|0\rangle) = |1\rangle|1\rangle$

现在，让我们考虑一个需要被克隆的叠加态，例如 $|\phi\rangle = \sqrt{\frac{1}{3}}|0\rangle + \sqrt{\frac{2}{3}}|1\rangle$。根据[线性原理](@entry_id:170988)，克隆门作用于输入态 $|\phi\rangle|0\rangle$ 的结果 $|\Psi_A\rangle$ 应该是：

$$
|\Psi_A\rangle = U_C(\left(\sqrt{\frac{1}{3}}|0\rangle + \sqrt{\frac{2}{3}}|1\rangle\right)|0\rangle) = \sqrt{\frac{1}{3}}U_C(|0\rangle|0\rangle) + \sqrt{\frac{2}{3}}U_C(|1\rangle|0\rangle) = \sqrt{\frac{1}{3}}|00\rangle + \sqrt{\frac{2}{3}}|11\rangle
$$

然而，我们所期望的“理想”克隆结果 $|\Psi_B\rangle$ 应该是 $|\phi\rangle|\phi\rangle$：

$$
|\Psi_B\rangle = \left(\sqrt{\frac{1}{3}}|0\rangle + \sqrt{\frac{2}{3}}|1\rangle\right) \otimes \left(\sqrt{\frac{1}{3}}|0\rangle + \sqrt{\frac{2}{3}}|1\rangle\right) = \frac{1}{3}|00\rangle + \frac{\sqrt{2}}{3}|01\rangle + \frac{\sqrt{2}}{3}|10\rangle + \frac{2}{3}|11\rangle
$$

显然，[线性原理](@entry_id:170988)所预测的实际输出 $|\Psi_A\rangle$ 与我们期望的理想输出 $|\Psi_B\rangle$ 是完全不同的状态。$|\Psi_A\rangle$ 是一个[纠缠态](@entry_id:152310)，而 $|\Psi_B\rangle$ 是一个可分离态。它们之间的保真度 $F = |\langle \Psi_A | \Psi_B \rangle|^2$ 远小于1，具体计算为 $\frac{9 + 4\sqrt{2}}{27}$ 。这个矛盾证明了，一个能够完美克隆[基态](@entry_id:150928)的线性算符，无法完美克隆它们的叠加态。因此，通用的[量子克隆](@entry_id:138347)机是不可能存在的。

### [单量子比特门](@entry_id:146489)：基本操作单元

正如经典计算机的逻辑门是处理比特的基本单元，量子门是操控[量子比特](@entry_id:137928)的基本工具。一个[单量子比特门](@entry_id:146489)在数学上表示为一个 $2 \times 2$ 的幺[正矩阵](@entry_id:149490)，作用于表示[量子比特](@entry_id:137928)状态的二维[复向量](@entry_id:192851)上。

#### [泡利门](@entry_id:139600) (Pauli Gates)

[泡利门](@entry_id:139600)是最基础的一组[单量子比特门](@entry_id:146489)，它们构成了描述[量子比特](@entry_id:137928)操作的重要基石。

**泡利-X 门 (Pauli-X Gate):** 也称为比特翻转门，是经典 NOT 门的量子对应。它的矩阵表示为：
$$ X = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix} $$
它将 $|0\rangle$ 翻转为 $|1\rangle$，将 $|1\rangle$ 翻转为 $|0\rangle$。

**泡利-Z 门 (Pauli-Z Gate):** 也称为相位翻转门。它的矩阵表示为：
$$ Z = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix} $$
它保持 $|0\rangle$ 不变，但给 $|1\rangle$ 附加一个 $-1$ 的相位因子，即 $Z|1\rangle = -|1\rangle$。这个相位变化虽然在计算基下测量时不可见，但在叠加态中却至关重要。

**泡利-Y 门 (Pauli-Y Gate):** 这个门可以看作是同时进行比特翻转和相位翻转。其[矩阵表示](@entry_id:146025)为：
$$ Y = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix} $$
通过[矩阵乘法](@entry_id:156035)，我们可以确定它对[基态](@entry_id:150928)的作用 ：
$Y|0\rangle = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}\begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} 0 \\ i \end{pmatrix} = i|1\rangle$
$Y|1\rangle = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}\begin{pmatrix} 0 \\ 1 \end{pmatrix} = \begin{pmatrix} -i \\ 0 \end{pmatrix} = -i|0\rangle$
它将 $|0\rangle$ 映射到 $i|1\rangle$，将 $|1\rangle$ 映射到 $-i|0\rangle$。

#### [阿达玛门](@entry_id:146898) (Hadamard Gate)

[阿达玛门](@entry_id:146898)（H门）在[量子计算](@entry_id:142712)中扮演着核心角色，因为它是创造**等量叠加态**的最基本工具。其矩阵表示为：
$$ H = \frac{1}{\sqrt{2}}\begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix} $$
当 H 门作用于计算[基态](@entry_id:150928)时：
$H|0\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$，通常记为 $|+\rangle$ 态。
$H|1\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)$，通常记为 $|-\rangle$ 态。
H 门可以被看作是在不同基之间的转换器。例如，它将 Z-基（$|0\rangle, |1\rangle$）上的状态转换为 X-基（$|+\rangle, |-\rangle$）上的状态。由于几乎所有[量子算法](@entry_id:147346)都利用了叠加性，H 门是构建[量子线路](@entry_id:151866)不可或缺的组件。

#### [相位门](@entry_id:143669) (S and T Gates)

除了泡利-Z门引入的 $180^\circ$（$\pi$ [弧度](@entry_id:171693)）相位，我们还需要更精细的相位控制。

**S 门 (Phase Gate):** S 门引入一个 $90^\circ$（$\pi/2$ [弧度](@entry_id:171693)）的相位。它是 Z 门的平方根，即 $S^2 = Z$。其矩阵为：
$$ S = \begin{pmatrix} 1  0 \\ 0  i \end{pmatrix} $$

**T 门 ($\pi/8$ Gate):** T 门提供更精细的 $45^\circ$（$\pi/4$ [弧度](@entry_id:171693)）相位旋转，是 S 门的平方根。其矩阵为：
$$ T = \begin{pmatrix} 1  0 \\ 0  \exp(\frac{i\pi}{4}) \end{pmatrix} $$
T 门在实现[通用量子计算](@entry_id:137200)中具有特殊地位，我们将在后续章节进一步探讨。

### [多量子比特系统](@entry_id:142942)与纠缠

真实世界的[量子计算](@entry_id:142712)很少只涉及单个[量子比特](@entry_id:137928)。为了解决有意义的问题，我们需要处理由多个[量子比特](@entry_id:137928)组成的系统。

#### 多[量子比特](@entry_id:137928)态与门操作

一个由 $n$ 个[量子比特](@entry_id:137928)组成的系统的[状态空间](@entry_id:177074)维度为 $2^n$。其状态由各个[量子比特](@entry_id:137928)状态的**[张量积](@entry_id:140694)**（$\otimes$）来描述。例如，一个[双量子比特系统](@entry_id:203437)的计算[基矢](@entry_id:199546)为 $|00\rangle, |01\rangle, |10\rangle, |11\rangle$。

当一个单比特门作用于多比特系统中的某一个[量子比特](@entry_id:137928)时，它在整个系统上的作用由该门的矩阵与作用于其他[量子比特](@entry_id:137928)的[单位矩阵](@entry_id:156724) $I$ 的张量积给出。例如，将 H 门作用于一个[三量子比特](@entry_id:146257)系统的第二个比特上，其总操作为 $I \otimes H \otimes I$。

如果将同一个门（如 H 门）同时应用于所有[量子比特](@entry_id:137928)，其总操作为 $H^{\otimes n} = H \otimes H \otimes \dots \otimes H$。例如，将三个 H 门并行作用于初始态 $|101\rangle$ 上，末态为 $(H|1\rangle) \otimes (H|0\rangle) \otimes (H|1\rangle)$ 。展开后，这将产生一个包含所有 $2^3=8$ 个计算[基矢](@entry_id:199546)的均匀叠加态，但每个[基矢](@entry_id:199546)前有特定的正负相位。

#### 受控门与纠缠的产生

为了让[量子比特](@entry_id:137928)之间能够相互作用，我们需要**受控门**。这类门有一个或多个“控制”[量子比特](@entry_id:137928)和一个或多个“目标”[量子比特](@entry_id:137928)。只有当所有控制[量子比特](@entry_id:137928)都处于特定状态（通常是 $|1\rangle$）时，目标[量子比特](@entry_id:137928)上才会执行一个特定的操作。

**受控非门 (CNOT Gate):** CNOT 门是最著名的双比特门。它有一个控制比特和一个目标比特。如果控制比特是 $|0\rangle$，目标比特保持不变；如果控制比特是 $|1\rangle$，目标比特执行一个 X 操作（比特翻转）。其作用可以总结为：CNOT$|c, t\rangle = |c, t \oplus c\rangle$，其中 $\oplus$ 表示模2加法。

CNOT 门的一个关键用途是**产生纠缠**。纠缠是量子力学最独特的现象之一，指一个[多体系统](@entry_id:144006)的状态无法表示为其各子系统状态的乘积。[纠缠态](@entry_id:152310)中的[量子比特](@entry_id:137928)即使在空间上相隔遥远，其测量结果也会表现出强烈的关联性。

一个标准的产生纠缠态的线路是作用于 $|00\rangle$ 态上的 H 门和 CNOT 门 。
1.  首先，对第一个[量子比特](@entry_id:137928)应用 H 门：
    $(H \otimes I)|00\rangle = (H|0\rangle) \otimes |0\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle) \otimes |0\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |10\rangle)$。
    此时系统处于一个可分离的叠加态。

2.  接着，应用一个以第一个比特为控制、第二个比特为目标的 CNOT 门：
    $\text{CNOT}_{1,2} \left( \frac{1}{\sqrt{2}}(|00\rangle + |10\rangle) \right) = \frac{1}{\sqrt{2}}(\text{CNOT}_{1,2}|00\rangle + \text{CNOT}_{1,2}|10\rangle)$
    根据 CNOT 的定义，$\text{CNOT}_{1,2}|00\rangle = |00\rangle$ (控制位为0)，而 $\text{CNOT}_{1,2}|10\rangle = |11\rangle$ (控制位为1，目标位翻转)。
    因此，最终状态为：
    $$ |\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle) $$
    这个著名的状态被称为**贝尔态**（Bell state），它是一个最大[纠缠态](@entry_id:152310)。无论测量哪个[量子比特](@entry_id:137928)，结果都是随机的（0或1的概率各为0.5），但一旦测量了一个，另一个的状态就瞬间确定为相同的结果。

**受控-Z 门 (CZ Gate):** 另一个重要的受控门是 CZ 门。它在控制比特为 $|1\rangle$ 时，对目标比特施加一个 Z 门。它的作用是保持 $|00\rangle, |01\rangle, |10\rangle$ 不变，但将 $|11\rangle$ 变为 $-|11\rangle$ 。有趣的是，CZ 门和 CNOT 门是等价的，可以通过在 CNOT 门的目标比特前后各加一个 H 门来构造出 CZ 门：$CZ_{1,2} = (I \otimes H) \cdot CNOT_{1,2} \cdot (I \otimes H)$ 。这种门之间的等价关系在[量子线路](@entry_id:151866)的优化和不同量子硬件平台的编译中非常重要。

### [量子线路](@entry_id:151866)与通用性

将一系列[量子门](@entry_id:143510)按时间顺序[排列](@entry_id:136432)，作用于一组[量子比特](@entry_id:137928)上，就构成了一个**[量子线路](@entry_id:151866)**。分析[量子线路](@entry_id:151866)的目标通常是追踪一个初始态的演化，并计算在最终状态下测量得到特定结果的概率。

例如，考虑一个[双量子比特系统](@entry_id:203437)，初始态为 $|00\rangle$。依次施加以下操作：(1) 对第一个比特施加 H 门；(2) 施加一个 CNOT 门（第一个比特为控制）；(3) 对第一个比特施加 Y 门。我们可以逐步计算系统的状态演化 ：
1.  初始态：$|\psi_0\rangle = |00\rangle$
2.  施加 H 门后：$|\psi_1\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |10\rangle)$
3.  施加 CNOT 门后：$|\psi_2\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$ （即贝尔态）
4.  施加 Y 门后：$|\psi_3\rangle = (Y \otimes I)|\psi_2\rangle = \frac{1}{\sqrt{2}}(Y|0\rangle \otimes |0\rangle + Y|1\rangle \otimes |1\rangle) = \frac{i}{\sqrt{2}}(|10\rangle - |01\rangle)$

此时，如果我们测量第二个[量子比特](@entry_id:137928)，得到结果为 $|1\rangle$ 的概率是多少？我们需要看末态中所有第二个比特为 $|1\rangle$ 的分量。这些分量是 $|01\rangle$ 和 $|11\rangle$。在 $|\psi_3\rangle$ 中，$|01\rangle$ 的振幅是 $-\frac{i}{\sqrt{2}}$，$|11\rangle$ 的振幅是 $0$。根据[玻恩定则](@entry_id:154470)，概率是振幅模的平方和：$P(q_2=1) = |-\frac{i}{\sqrt{2}}|^2 + |0|^2 = \frac{1}{2}$。

#### [通用门集](@entry_id:191428)

一个自然的问题是：我们需要多少种不同的[量子门](@entry_id:143510)才能实现任意可能的[量子计算](@entry_id:142712)？正如[经典计算](@entry_id:136968)中的与非门（NAND）是通用的一样，[量子计算](@entry_id:142712)中也存在**[通用门集](@entry_id:191428)**（Universal Gate Set）。一个门集是通用的，意味着通过组合该集合中的门，可以任意精度地逼近任何一个幺正变换。

并非所有门集都是通用的。例如，只包含泡利-X 和泡利-Z 门的集合就不是通用的 。如果我们从 $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle)$ 态开始，无论如何交替应用 X 和 Z 门，我们只能得到有限的几个态，如 $|+\rangle, |-\rangle, -|+\rangle, -|-\rangle$。这些态的振幅分量的[绝对值](@entry_id:147688)始终相等，因此我们永远无法通过这组门得到像 $|0\rangle$ 这样振幅不等的态。

一个被广泛接受的[通用门集](@entry_id:191428)是**{H, S, T, CNOT}**。这组门足以构建任何量子算法。

#### Clifford 门与 T 门的特殊作用

在这个[通用门集](@entry_id:191428)中，{H, S, CNOT} 这组门有一个特殊的名称，它们生成的群被称为**[克利福德群](@entry_id:140930)** (Clifford group)。[克利福德门](@entry_id:137923)有一个重要性质：它们总是将[泡利算符](@entry_id:144061)的乘积映射到泡利算符的乘积（Gottesman-Knill 定理）。一个实际的推论是，任何仅由[克利福德门](@entry_id:137923)和计算[基态](@entry_id:150928)制备、测量的[量子线路](@entry_id:151866)，都可以被经典计算机高效地模拟。这类线路产生的测量概率总是**[二进有理数](@entry_id:148903)**（dyadic rational），即形如 $k/2^n$ 的数。

为了获得超越经典计算的能力，我们需要引入[非克利福德门](@entry_id:137861)。T 门正是这样一个关键角色。将 T 门加入到[克利福德门](@entry_id:137923)集中，就使得该门集具备了真正的[通用量子计算](@entry_id:137200)能力。

T 门之所以特殊，是因为它引入的 $\exp(i\pi/4)$ 相位无法仅通过[克利福德门](@entry_id:137923)产生。通过巧妙地设计线路，这个特殊的相位可以转化为测量概率上的非[二进有理数](@entry_id:148903)，这标志着该计算过程无法被经典方法有效模拟。

考虑一个简单的线路 $U = HTH$，作用于 $|0\rangle$ 态 。
1.  $H|0\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$
2.  $T \left( \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle) \right) = \frac{1}{\sqrt{2}}(|0\rangle + \exp(i\pi/4)|1\rangle)$
3.  $H \left( \frac{1}{\sqrt{2}}(|0\rangle + \exp(i\pi/4)|1\rangle) \right) = \frac{1}{2}((1+\exp(i\pi/4))|0\rangle + (1-\exp(i\pi/4))|1\rangle)$

测量得到 $|1\rangle$ 的概率 $p(1)$ 是其振幅模的平方：
$$ p(1) = \left|\frac{1-\exp(i\pi/4)}{2}\right|^2 = \frac{1}{4} |1 - (\cos(\frac{\pi}{4}) + i\sin(\frac{\pi}{4}))|^2 = \frac{1}{4} \left( (1-\frac{\sqrt{2}}{2})^2 + (-\frac{\sqrt{2}}{2})^2 \right) = \frac{2-\sqrt{2}}{4} $$
由于 $\sqrt{2}$ 是无理数，这个概率不是[二进有理数](@entry_id:148903)。这个简单的例子有力地证明了，T 门是解锁完全[量子计算](@entry_id:142712)能力、超越经典模拟界限的“魔法钥匙”。