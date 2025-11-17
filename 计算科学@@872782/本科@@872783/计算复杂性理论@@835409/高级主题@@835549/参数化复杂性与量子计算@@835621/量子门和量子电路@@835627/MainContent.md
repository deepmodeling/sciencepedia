## 引言
[量子计算](@entry_id:142712)正引领着一场信息处理的革命，其核心在于一套与[经典计算](@entry_id:136968)截然不同的基本构件：[量子门](@entry_id:143510)与量子电路。与依赖比特和[逻辑门](@entry_id:142135)的[经典计算](@entry_id:136968)机不同，[量子计算](@entry_id:142712)机利用量子力学的奇特现象——如叠加与纠缠——来开启前所未有的计算能力。然而，如何精确地驾驭这些量子效应来解决实际问题，是计算科学面临的一大挑战与知识鸿沟。本文旨在系统性地揭开[量子计算](@entry_id:142712)的底层逻辑，为读者搭建起从基本原理到前沿应用的完整知识框架。

在接下来的内容中，你将踏上一段深入的探索之旅。首先，在“**原理与机制**”一章，我们将从[量子比特](@entry_id:137928)的数学描述出发，深入剖析[量子门](@entry_id:143510)作为幺正[变换的核](@entry_id:149509)心性质，并介绍构成所有[量子计算](@entry_id:142712)基础的关键门类型。随后，在“**应用与跨学科连接**”一章，我们将展示这些抽象的门和电路如何在[量子算法](@entry_id:147346)、[物理模拟](@entry_id:144318)、[化学计算](@entry_id:155220)乃至计算机工程中发挥其强大威力。最后，“**动手实践**”部分将提供具体的计算问题，让你亲手应用所学知识，巩固对量子电路演化的理解。通过这三个章节的层层递进，你将掌握构建和理解[量子计算](@entry_id:142712)程序所需的核心工具。

## 原理与机制

与经典计算依赖于比特和[逻辑门](@entry_id:142135)来处理信息类似，[量子计算](@entry_id:142712)也建立在相应的基本单元之上：**[量子比特](@entry_id:137928)（qubits）** 和 **量子门（quantum gates）**。然而，量子力学的独特原理——叠加、纠缠和干涉——赋予了这些基本单元远超经典同行的强大能力。本章将深入探讨量子门与量子电路的核心工作原理与机制，从单个[量子比特](@entry_id:137928)的表示和操作，延伸到[多量子比特系统](@entry_id:142942)的构建，并最终阐明实现[通用量子计算](@entry_id:137200)的理论基石。

### 量子系统的[状态空间](@entry_id:177074)

在进入[量子门](@entry_id:143510)操作的细节之前，我们必须首先理解其操作对象——[量子比特](@entry_id:137928)的状态——是如何被数学描述的。

一个**[量子比特](@entry_id:137928)**是量子信息的[基本单位](@entry_id:148878)。与只能处于 $0$ 或 $1$ 两种状态之一的经典比特不同，一个[量子比特](@entry_id:137928)可以处于 $0$ 和 $1$ 的**线性叠加（linear superposition）**态。在数学上，单[量子比特](@entry_id:137928)的状态被描述为二维[复向量空间](@entry_id:264355)中的一个单位向量。这个[向量空间](@entry_id:151108)被称为**[希尔伯特空间](@entry_id:261193)（Hilbert space）**，记作 $\mathcal{H}$。我们通常选用一组[标准正交基](@entry_id:147779)，称为**计算[基矢](@entry_id:199546)（computational basis）**，记作 $|0\rangle$ 和 $|1\rangle$。它们分别对应经典比特的 $0$ 和 $1$ 状态，其[向量表示](@entry_id:166424)为：
$$
|0\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad |1\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}
$$
一个任意的单[量子比特](@entry_id:137928)状态 $|\psi\rangle$ 都可以写成这两个[基矢](@entry_id:199546)的[线性组合](@entry_id:154743)：
$$
|\psi\rangle = \alpha|0\rangle + \beta|1\rangle = \begin{pmatrix} \alpha \\ \beta \end{pmatrix}
$$
其中，$\alpha$ 和 $\beta$ 是复数，称为**概率幅（probability amplitudes）**。它们必须满足[归一化条件](@entry_id:156486) $|\alpha|^2 + |\beta|^2 = 1$，这源于量子测量的概率诠释：当我们测量这个[量子比特](@entry_id:137928)时，得到结果 $0$ 的概率是 $|\alpha|^2$，得到结果 $1$ 的概率是 $|\beta|^2$。

当我们将多个[量子比特](@entry_id:137928)组合成一个系统，例如一个**量子寄存器（quantum register）**时，系统的状态空间维度会呈指数级增长。一个包含 $n$ 个[量子比特](@entry_id:137928)的系统的希尔伯特空间是通过将单个[量子比特](@entry_id:137928)的希尔伯特空间进行**[张量积](@entry_id:140694)（tensor product）**运算得到的，记作 $\mathcal{H}^{\otimes n}$。[张量积](@entry_id:140694)空间的维度是各[子空间](@entry_id:150286)维度的乘积。由于单个[量子比特](@entry_id:137928)的空间维度是 $2$，一个 $n$ [量子比特](@entry_id:137928)系统的状态空间维度就是 $2^n$。

例如，一个由10个[量子比特](@entry_id:137928)组成的量子寄存器，其[状态空间](@entry_id:177074)将是一个维度为 $2^{10} = 1024$ 的[复向量空间](@entry_id:264355)。这意味着要完整地描述这样一个系统的状态，我们需要 $1024$ 个复数（概率幅）[@problem_id:1440405]。这种[状态空间](@entry_id:177074)随[量子比特](@entry_id:137928)数量指数级增长的特性，正是[量子计算](@entry_id:142712)巨大潜力的来源之一，因为它允许[量子计算](@entry_id:142712)机在单个计算步骤中并行处理海量的信息。

### [量子门](@entry_id:143510)：幺正变换与基本性质

[量子计算](@entry_id:142712)通过施加一系列**量子门**来演化[量子比特](@entry_id:137928)的状态。在数学上，一个作用于 $n$ 个[量子比特](@entry_id:137928)的量子门是一个 $2^n \times 2^n$ 的**幺[正矩阵](@entry_id:149490)（unitary matrix）** $U$。当一个门 $U$ 作用于[量子态](@entry_id:146142) $|\psi\rangle$ 时，系统的新状态 $|\psi'\rangle$ 就是矩阵与向量的乘积：$|\psi'\rangle = U|\psi\rangle$。

幺正性是量子门最根本的属性。一个矩阵 $U$ 是幺正的，当且仅当它的共轭转置 $U^\dagger$（也称为厄米伴随）同时也是它的逆矩阵，即：
$$
U^\dagger U = U U^\dagger = I
$$
其中 $I$ 是单位矩阵。这个属性带来了两个至关重要的物理推论：

#### [可逆性](@entry_id:143146)

幺正变换是可逆的。如果一个[量子门](@entry_id:143510) $U$ 将状态 $|\psi\rangle$ 演化为 $|\psi'\rangle$，我们总能通过施加另一个[量子门](@entry_id:143510) $U^\dagger$ 将系统完美地恢复到初始状态：
$$
U^\dagger |\psi'\rangle = U^\dagger (U |\psi\rangle) = (U^\dagger U) |\psi\rangle = I |\psi\rangle = |\psi\rangle
$$
这意味着任何由量子门构成的[量子计算](@entry_id:142712)过程在根本上都是**可逆的**。与某些[经典逻辑](@entry_id:264911)门（如[或门](@entry_id:168617) OR、[与非门](@entry_id:151508) NAND）不同，量子门操作不会丢失信息。每个输出状态都唯一地对应一个输入状态 [@problem_id:1429333]。整个量子电路的总操作 $U_{\text{total}} = U_k \dots U_2 U_1$ 也是一个幺[正矩阵](@entry_id:149490)，其逆操作就是 $U_{\text{total}}^\dagger = U_1^\dagger U_2^\dagger \dots U_k^\dagger$。

#### 线性

作为矩阵，量子门的操作自然是线性的。这意味着量子门作用于一个叠加态时，其效果等于分别作用于叠加态的每个分量，然后将结果再按原有的系数叠加起来。即对于任意状态 $|\psi_1\rangle$、 $|\psi_2\rangle$ 和复数 $c_1$、$c_2$：
$$
U(c_1|\psi_1\rangle + c_2|\psi_2\rangle) = c_1 U|\psi_1\rangle + c_2 U|\psi_2\rangle
$$
线性是量子力学的一条基本准则，它导致了一个深刻的结论：**“无克隆定理”（No-Cloning Theorem）**。该定理指出，不存在一个通用的[量子操作](@entry_id:145906)，可以精确地复制一个任意未知的[量子态](@entry_id:146142)。

我们可以通过一个思想实验来证明这一点 [@problem_id:1440368]。假设存在一个“克隆”门 $U_C$，它的功能是接收一个待克隆态 $|\psi\rangle$ 和一个初始为空白的[辅助量子比特](@entry_id:144604) $|0\rangle$，并输出两个处于 $|\psi\rangle$ 状态的[量子比特](@entry_id:137928)。即 $U_C (|\psi\rangle \otimes |0\rangle) = |\psi\rangle \otimes |\psi\rangle$。

根据线性，这个门的行为完全由它在[基矢](@entry_id:199546)上的作用决定：
1.  $U_C(|0\rangle|0\rangle) = |0\rangle|0\rangle$
2.  $U_C(|1\rangle|0\rangle) = |1\rangle|1\rangle$

现在，让我们尝试克隆一个叠加态，例如 $|\phi\rangle = \sqrt{\frac{1}{3}}|0\rangle + \sqrt{\frac{2}{3}}|1\rangle$。一方面，根据[线性原理](@entry_id:170988)，输出态应该是：
$$
|\Psi_A\rangle = U_C(|\phi\rangle|0\rangle) = U_C\left(\sqrt{\frac{1}{3}}|00\rangle + \sqrt{\frac{2}{3}}|10\rangle\right) = \sqrt{\frac{1}{3}}U_C(|00\rangle) + \sqrt{\frac{2}{3}}U_C(|10\rangle) = \sqrt{\frac{1}{3}}|00\rangle + \sqrt{\frac{2}{3}}|11\rangle
$$
另一方面，理想的克隆输出应该是 $|\phi\rangle|\phi\rangle$：
$$
|\Psi_B\rangle = |\phi\rangle|\phi\rangle = \left(\sqrt{\frac{1}{3}}|0\rangle + \sqrt{\frac{2}{3}}|1\rangle\right) \otimes \left(\sqrt{\frac{1}{3}}|0\rangle + \sqrt{\frac{2}{3}}|1\rangle\right) = \frac{1}{3}|00\rangle + \frac{\sqrt{2}}{3}|01\rangle + \frac{\sqrt{2}}{3}|10\rangle + \frac{2}{3}|11\rangle
$$
显然，$|\Psi_A\rangle \neq |\Psi_B\rangle$。这两个状态不仅不等，甚至不是简单的[全局相位](@entry_id:147947)差异。这表明，一个遵循量子力学[线性原理](@entry_id:170988)的操作无法实现对任意[量子态](@entry_id:146142)的完美克隆。

### 关键量子门举例

如同[经典计算](@entry_id:136968)中的与、或、[非门](@entry_id:169439)，[量子计算](@entry_id:142712)也有一套构建模块。下面介绍一些最重要和最常用的[量子门](@entry_id:143510)。

#### [单量子比特门](@entry_id:146489)

这些门作用于单个[量子比特](@entry_id:137928)，由 $2 \times 2$ 的幺正矩阵表示。

*   **[泡利门](@entry_id:139600)（Pauli Gates）**: 泡利-X、Y、Z门是[量子计算](@entry_id:142712)的基石，可以视为量子世界中对经典比特翻转操作的推广。
    *   **泡利-X门**（或**比特翻转门**）：$X = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$。它将 $|0\rangle$ 变为 $|1\rangle$，将 $|1\rangle$ 变为 $|0\rangle$。
    *   **泡利-Z门**（或**相位翻转门**）：$Z = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$。它保持 $|0\rangle$ 不变，但将 $|1\rangle$ 变为 $-|1\rangle$，引入一个负号的相位。
    *   **泡利-Y门**：$Y = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}$。它的作用是比特翻转和相位翻转的结合。例如，我们可以计算它对[基矢](@entry_id:199546)的作用 [@problem_id:1440387]：
        $$
        Y|0\rangle = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix} \begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} 0 \\ i \end{pmatrix} = i|1\rangle
        $$
        $$
        Y|1\rangle = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix} \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \begin{pmatrix} -i \\ 0 \end{pmatrix} = -i|0\rangle
        $$

*   **[阿达玛门](@entry_id:146898)（Hadamard Gate）**: $H = \frac{1}{\sqrt{2}}\begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}$。这是[量子计算](@entry_id:142712)中最重要的门之一。它的核心功能是创建等概率的叠加态。当它作用于计算[基矢](@entry_id:199546)上时：
    $$
    H|0\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)
    $$
    $$
    H|1\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)
    $$
    可以看到，它将一个确定的[基态](@entry_id:150928)转换为了一个不确定的叠加态，这是开启[量子并行性](@entry_id:137267)的关键一步。

*   **[相位门](@entry_id:143669)（Phase Gates）**:
    *   **S门** (或 $\sqrt{Z}$ 门): $S = \begin{pmatrix} 1  0 \\ 0  i \end{pmatrix}$。它给 $|1\rangle$ 态引入一个 $i$ 的相位。
    *   **[T门](@entry_id:138474)**: $T = \begin{pmatrix} 1  0 \\ 0  \exp(i\pi/4) \end{pmatrix}$。它给 $|1\rangle$ 态引入一个 $\exp(i\pi/4)$ 的相位。这个门在[通用量子计算](@entry_id:137200)中扮演着至关重要的角色，我们将在稍后讨论。

#### [多量子比特门](@entry_id:139015)

[多量子比特门](@entry_id:139015)是实现[量子比特](@entry_id:137928)间相互作用和**量子纠缠（quantum entanglement）**的关键。

*   **[张量积表示](@entry_id:143629)**: 当多个独立的门同时作用于不同的[量子比特](@entry_id:137928)时，整个系统的操作由各个门矩阵的张量积给出。例如，考虑一个[双量子比特系统](@entry_id:203437)，我们希望对第一个[量子比特](@entry_id:137928)施加泡利-X门，同时对第二个[量子比特](@entry_id:137928)施加[阿达玛门](@entry_id:146898)。如果我们的状态向量[基矢](@entry_id:199546)顺序是 $\{|00\rangle, |01\rangle, |10\rangle, |11\rangle\}$，其中约定记法为 $|q_2q_1\rangle$（$q_2$ 代表第二个[量子比特](@entry_id:137928)），那么总的操作矩阵 $U$ 是 $H \otimes X$。其计算过程如下 [@problem_id:1440375]：
    $$
    U = H \otimes X = \frac{1}{\sqrt{2}}\begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix} \otimes \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix} = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \cdot X  1 \cdot X \\ 1 \cdot X  -1 \cdot X \end{pmatrix} = \frac{1}{\sqrt{2}}\begin{pmatrix} 0  1  0  1 \\ 1  0  1  0 \\ 0  1  0  -1 \\ 1  0  -1  0 \end{pmatrix}
    $$
    这个 $4 \times 4$ 的矩阵描述了这一并行操作对整个[双量子比特系统](@entry_id:203437)的影响。

*   **受控门（Controlled Gates）**: 这是一类极其重要的双[量子比特](@entry_id:137928)门，其操作依赖于一个“控制”[量子比特](@entry_id:137928)的状态来决定是否对另一个“目标”[量子比特](@entry_id:137928)施加操作。
    *   **受控非门（CNOT Gate）**: [CNOT门](@entry_id:180955)是其中最著名的例子。它有一个控制比特和一个目标比特。如果控制比特是 $|1\rangle$，它就对目标比特施加一个X门（比特翻转）；如果控制比特是 $|0\rangle$，它什么也不做。其作用可以总结为：CNOT$|c\rangle|t\rangle = |c\rangle|t \oplus c\rangle$，其中 $\oplus$ 是模2加法。
    *   **受控Z门（CZ Gate）**: 类似地，CZ门在控制比特为 $|1\rangle$ 时对目标比特施加一个Z门（相位翻转）。让我们分析它对四个计算[基矢](@entry_id:199546)的作用 [@problem_id:1440400]。设第一个[量子比特](@entry_id:137928)为控制比特，第二个为目标比特：
        *   $CZ|00\rangle$: 控制位为 $|0\rangle$，无操作，结果为 $|00\rangle$。
        *   $CZ|01\rangle$: 控制位为 $|0\rangle$，无操作，结果为 $|01\rangle$。
        *   $CZ|10\rangle$: 控制位为 $|1\rangle$，对目标 $|0\rangle$ 施加Z门。因为 $Z|0\rangle = |0\rangle$，所以结果仍是 $|10\rangle$。
        *   $CZ|11\rangle$: 控制位为 $|1\rangle$，对目标 $|1\rangle$ 施加Z门。因为 $Z|1\rangle = -|1\rangle$，所以结果变为 $-|11\rangle$。
        因此，CZ门的独特之处在于它仅给 $|11\rangle$ 状态引入一个-1的相位，而保持其他[基态](@entry_id:150928)不变。这种“条件相位”是构建许多[量子算法](@entry_id:147346)的核心机制。

### 构建量子电路

一个**量子电路**是将一系列[量子门](@entry_id:143510)按时间顺序[排列](@entry_id:136432)，作用于一组[量子比特](@entry_id:137928)上的计算模型。通过精心设计门的序列，我们可以实现特定的计算任务或制备出有价值的[量子态](@entry_id:146142)。

一个经典的例子是**贝尔态（Bell state）的制备**。贝尔态是四种最简单的双[量子比特](@entry_id:137928)纠缠态。其中一种，记为 $|\Phi^+\rangle$，定义为：
$$
|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)
$$
这个状态的特点是，两个[量子比特](@entry_id:137928)的测量结果总是相关的：要么都得到0，要么都得到1，但无法在测量前预测是哪一种。要从初始的 $|00\rangle$ 态制备出 $|\Phi^+\rangle$，我们只需要一个[阿达玛门](@entry_id:146898)和一个[CNOT门](@entry_id:180955) [@problem_id:1440392]。

电路的构建步骤如下：
1.  **初始化**: 系统处于 $|00\rangle$ 态。
2.  **创建叠加**: 对第一个[量子比特](@entry_id:137928)施加一个[阿达玛门](@entry_id:146898)（H）。系统状态变为：
    $$
    (H \otimes I)|00\rangle = (H|0\rangle) \otimes |0\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle) \otimes |0\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |10\rangle)
    $$
3.  **产生纠缠**: 接下来，施加一个[CNOT门](@entry_id:180955)，以第一个[量子比特](@entry_id:137928)为控制，第二个为目标。我们对上一步得到的叠加态施加这个门：
    $$
    \text{CNOT}\left(\frac{1}{\sqrt{2}}(|00\rangle + |10\rangle)\right) = \frac{1}{\sqrt{2}}(\text{CNOT}|00\rangle + \text{CNOT}|10\rangle)
    $$
    根据CNOT的定义：
    *   对于 $|00\rangle$ 项，控制位是 $|0\rangle$，目标位不变，结果是 $|00\rangle$。
    *   对于 $|10\rangle$ 项，控制位是 $|1\rangle$，目标位 $|0\rangle$ 翻转为 $|1\rangle$，结果是 $|11\rangle$。
    将这两部分组合起来，最终状态即为：
    $$
    \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle) = |\Phi^+\rangle
    $$
这个简单的两步电路，完美地展示了量子电路如何利用叠加和受控操作来创造出经典世界中不存在的纠缠关联。

### [通用量子计算](@entry_id:137200)原理

一个自然而然的问题是：是否存在一个有限的“门集”，通过组合其中的门，可以构建出任何可能的[量子计算](@entry_id:142712)？答案是肯定的，这样的门集被称为**[通用量子门集](@entry_id:136517)（universal quantum gate set）**。通用性意味着，任何 $n$ [量子比特](@entry_id:137928)的幺正变换 $U$ 都可以通过该门集中的门以任意精度来近似。

并非任何门集都是通用的。例如，只包含泡利-X门和泡利-Z门的集合就不是通用的 [@problem_id:1440399]。考虑一个初始态 $|\psi_{in}\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$。无论我们施加多少次X门或Z门，我们都无法将这个状态变成 $|0\rangle$。这是因为X门和Z门只能交换或改变[概率幅](@entry_id:150609)的符号，但不能改变它们的[绝对值](@entry_id:147688)。初始态中 $|0\rangle$ 和 $|1\rangle$ 的概率幅[绝对值](@entry_id:147688)都是 $\frac{1}{\sqrt{2}}$，而目标态 $|0\rangle$ 中它们的[概率幅](@entry_id:150609)[绝对值](@entry_id:147688)分别是 $1$ 和 $0$。由于这些门无法改变[概率幅](@entry_id:150609)的模，所以无法实现这一转变。

一个被广泛接受的[通用门集](@entry_id:191428)是**[克利福德+T门](@entry_id:146439)集（Clifford+T gate set）**。[克利福德门](@entry_id:137923)集包括[阿达玛门](@entry_id:146898)(H)、S门以及CNOT门。[克利福德门](@entry_id:137923)构成的电路虽然功能强大，并且在[经典计算](@entry_id:136968)机上可以被高效地模拟，但它们本身并不足以实现[通用量子计算](@entry_id:137200)。它们所能产生的[量子态](@entry_id:146142)有一个特殊的性质：在计算[基矢](@entry_id:199546)下测量时，得到的各种结果的概率总是**[二进有理数](@entry_id:148903)（dyadic rational）**，即形如 $k/2^n$ 的数。

为了实现真正的通用性，即能够生成具有任意概率幅的[量子态](@entry_id:146142)，我们必须引入一个[非克利福德门](@entry_id:137861)。**[T门](@entry_id:138474)**正是扮演了这个关键角色。通过引入[T门](@entry_id:138474)，我们可以构建出产生非[二进有理数](@entry_id:148903)测量概率的电路。一个最简单的例子是 $HTH$ 电路 [@problem_id:1440413]。将它作用于 $|0\rangle$ 态：
1.  $H|0\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$
2.  $T \left( \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle) \right) = \frac{1}{\sqrt{2}}(|0\rangle + e^{i\pi/4}|1\rangle)$
3.  $H \left( \frac{1}{\sqrt{2}}(|0\rangle + e^{i\pi/4}|1\rangle) \right) = \frac{1}{2}((1+e^{i\pi/4})|0\rangle + (1-e^{i\pi/4})|1\rangle)$
测量得到结果 '1' 的概率为：
$$
p(1) = \left|\frac{1-e^{i\pi/4}}{2}\right|^2 = \frac{1}{4}|1 - (\cos(\pi/4) + i\sin(\pi/4))|^2 = \frac{1}{4}\left((1-\frac{\sqrt{2}}{2})^2 + (-\frac{\sqrt{2}}{2})^2\right) = \frac{2-\sqrt{2}}{4}
$$
由于 $\sqrt{2}$ 是无理数，这个概率不是一个[二进有理数](@entry_id:148903)。这具体地表明，[T门](@entry_id:138474)使得[量子计算](@entry_id:142712)能够探索[希尔伯特空间](@entry_id:261193)中一个比[克利福德电路](@entry_id:141482)所能触及的、更广阔也更丰富的区域。事实上，[Solovay-Kitaev定理](@entry_id:138373)保证了通过组合[克利福德门](@entry_id:137923)和[T门](@entry_id:138474)，可以有效地近似任何幺正变换。

更进一步，通用性的概念可以被更精细地刻画。一个重要的结论是，任何能够产生纠缠的双[量子比特](@entry_id:137928)门，与所有[单量子比特门](@entry_id:146489)组合在一起，就构成了[通用门集](@entry_id:191428)。一个有趣的例子是考虑一个对角矩阵形式的双[量子比特](@entry_id:137928)门 $U_{entangle} = \text{diag}(1, 1, 1, e^{i\alpha})$，其中 $\alpha/\pi$ 是一个无理数 [@problem_id:1440362]。这个门集可以被证明是通用的，但它揭示了“通用性”的两种含义：**精确构造**和**任意精度近似**。由于 $\alpha/\pi$ 是无理数，我们无法通过有限次地使用这个门来精确地构造出像[CNOT门](@entry_id:180955)（其等效的[对角形式](@entry_id:264850)相位为 $\pi$）这样的操作。然而，正是因为 $\alpha/\pi$ 是无理数，通过重复使用 $U_{entangle}$，我们可以生成在 $[0, 2\pi)$ 区间内稠密的相位，从而能够以任意高的精度去**近似**CNOT门以及任何其他的幺正操作。这为构建[量子计算](@entry_id:142712)机提供了一条可行的途径，即我们只需要物理上实现一个“足够好”的纠缠门和任意的单比特旋转，就可以实现通用的[量子计算](@entry_id:142712)能力。