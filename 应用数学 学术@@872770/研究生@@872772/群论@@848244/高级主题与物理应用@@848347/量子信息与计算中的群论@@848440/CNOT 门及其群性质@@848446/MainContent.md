## 引言
在[量子计算](@entry_id:142712)的宏伟蓝图中，受控非门（CNOT）不仅是一个基础的双[量子比特](@entry_id:137928)[逻辑门](@entry_id:142135)，更是构建复杂量子算法和理解[多体量子系统](@entry_id:161678)动力学的基石。尽管其作用机制——“当控制比特为1时翻转目标比特”——看似简单，但其背后蕴含的深刻数学结构和物理意义远超于此。当前，我们面临的挑战不仅在于物理上实现高保真度的[量子门](@entry_id:143510)，更在于从根本上理解这些门如何组合、演化，以及它们构成的代数系统具有何种计算能力。本文旨在填补这一认知空白，通过群论这一强有力的数学工具，揭示[CNOT门](@entry_id:180955)隐藏的对称性、周期性及其在更广阔物理图景中的角色。

为实现这一目标，本文将引导读者踏上一段从基础原理到前沿应用的探索之旅。在“原理与机制”一章中，我们将首先剖析[CNOT门](@entry_id:180955)的线性算符本质和泡利分解，进而揭示其产生[量子纠缠](@entry_id:136576)的核心机制，并系统性地研究其作为[克利福德群](@entry_id:140930)成员以及与其他门生成的有限群的代数性质。随后的“应用与跨学科联系”一章将展示这些抽象理论的强大威力，探讨[CNOT门](@entry_id:180955)如何在量子电路合成、量子纠错、[资源理论](@entry_id:142789)乃至与[辫群](@entry_id:142941)和拓扑量子计算的深刻联系中发挥关键作用。最后，在“动手实践”部分，我们提供了一系列精心设计的练习，旨在通过具体计算加深对CNOT门群属性的理解。通过这三个章节的层层深入，读者将对[CNOT门](@entry_id:180955)建立一个全面而深刻的认识，领会其作为连接量子信息、抽象代数与数学物理的关键枢纽的重要意义。

## 原理与机制

本章在前一章介绍性概述的基础上，深入探讨受控非门（CNOT）的数学原理和物理机制。我们将从其作为线性算符的基本定义出发，分析其在不同基下的表示，并揭示其产生[量子纠缠](@entry_id:136576)的核心能力。随后，我们将转向更为抽象但功能强大的群论视角，研究由[CNOT门](@entry_id:180955)与其他基本[量子门](@entry_id:143510)生成的[代数结构](@entry_id:137052)，并阐明这些结构在[量子计算](@entry_id:142712)，特别是量子纠错和[算法分析](@entry_id:264228)中的深刻意义。

### 受控非门作为线性算符

在量子力学中，[量子门](@entry_id:143510)是对[量子比特](@entry_id:137928)状态进行操作的幺正变换。[受控非门](@entry_id:180955)是理解[多量子比特系统](@entry_id:142942)动力学和相互作用的基石。

#### 定义与矩阵表示

**受控非门（Controlled-NOT, CNOT）** 是一种双[量子比特](@entry_id:137928)门，它包含一个 **控制比特** (control qubit) 和一个 **目标比特** (target qubit)。其作用规则非常直观：如果控制比特处于 $|1\rangle$ 态，则目标比特的状态翻转（应用一个泡利 $X$ 门）；如果控制比特处于 $|0\rangle$ 态，则目标比特保持不变。其作用可以用如下映射表示：
$$
\text{CNOT} |c, t\rangle = |c, t \oplus c\rangle
$$
其中 $c, t \in \{0, 1\}$，$\oplus$ 表示模2加法。

在标准的计算基 $\{|00\rangle, |01\rangle, |10\rangle, |11\rangle\}$ 中，CNOT 门（以第一比特为控制，第二比特为目标）的幺[正矩阵](@entry_id:149490) $U_{CNOT}$ 为：
$$
U_{CNOT} = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0 \end{pmatrix}
$$
矩阵的前两行和前两列构成的单位矩阵表示当控制比特为 $|0\rangle$ 时（即在 $|00\rangle$ 和 $|01\rangle$ 构成的[子空间](@entry_id:150286)），目标比特不变。后两行和后两列构成的泡利 $X$ 矩阵形式表示当控制比特为 $|1\rangle$ 时（即在 $|10\rangle$ 和 $|11\rangle$ 构成的[子空间](@entry_id:150286)），目标比特的状态发生翻转（$|10\rangle \leftrightarrow |11\rangle$）。由于 $U_{CNOT}^2 = I$，[CNOT门](@entry_id:180955)是自身的逆，这是一个在[电路设计](@entry_id:261622)中非常有用的性质。

#### 算符分解：泡利基

任何作用于 $n$ [量子比特](@entry_id:137928)系统的线性算符都可以表示为 **[泡利算符](@entry_id:144061)串（Pauli strings）** 的线性组合。对于一个[双量子比特系统](@entry_id:203437)，其算符空间由 $4 \times 4 = 16$ 个形如 $\sigma_i \otimes \sigma_j$ 的算符张成一个[正交基](@entry_id:264024)，其中 $i,j \in \{0, x, y, z\}$，$\sigma_0=I$ 为[单位矩阵](@entry_id:156724)，$\sigma_x, \sigma_y, \sigma_z$ 为标准的泡利矩阵。

一个算符 $U$ 在这个基下的展开式为：
$$
U = \sum_{i,j \in \{0,x,y,z\}} c_{ij} (\sigma_i \otimes \sigma_j)
$$
系数 $c_{ij}$ 可以通过[希尔伯特-施密特内积](@entry_id:190429) $\langle A, B \rangle = \text{Tr}(A^\dagger B)$ 来计算。由于泡利算符串构成了正交基，且 $\text{Tr}((\sigma_i \otimes \sigma_j)^\dagger (\sigma_k \otimes \sigma_l)) = 4 \delta_{ik}\delta_{jl}$，我们可以得到展开系数的计算公式：
$$
c_{ij} = \frac{1}{4} \text{Tr}\left( (\sigma_i \otimes \sigma_j)^\dagger U \right)
$$
由于[泡利矩阵](@entry_id:139493)都是[厄米矩阵](@entry_id:155147)，$(\sigma_i \otimes \sigma_j)^\dagger = \sigma_i \otimes \sigma_j$。

让我们以一个具体的例子来揭示[CNOT门](@entry_id:180955)的内在结构 [@problem_id:803032]。考虑计算CNOT门在泡利基中对应于 $\sigma_z \otimes \sigma_x$ 的系数 $c_{zx}$。根据公式：
$$
c_{zx} = \frac{1}{4} \text{Tr}\left( (\sigma_z \otimes \sigma_x) U_{CNOT} \right)
$$
我们需要计算矩阵 $(\sigma_z \otimes \sigma_x) U_{CNOT}$ 的迹。首先，我们分析算符 $\sigma_z \otimes \sigma_x$ 对计算[基矢](@entry_id:199546)的作用：
- $(\sigma_z \otimes \sigma_x) |00\rangle = (\sigma_z|0\rangle) \otimes (\sigma_x|0\rangle) = |0\rangle \otimes |1\rangle = |01\rangle$
- $(\sigma_z \otimes \sigma_x) |01\rangle = (\sigma_z|0\rangle) \otimes (\sigma_x|1\rangle) = |0\rangle \otimes |0\rangle = |00\rangle$
- $(\sigma_z \otimes \sigma_x) |10\rangle = (\sigma_z|1\rangle) \otimes (\sigma_x|0\rangle) = -|1\rangle \otimes |1\rangle = -|11\rangle$
- $(\sigma_z \otimes \sigma_x) |11\rangle = (\sigma_z|1\rangle) \otimes (\sigma_x|1\rangle) = -|1\rangle \otimes |0\rangle = -|10\rangle$

现在我们可以计算迹，即对角[线元](@entry_id:196833)素之和 $\sum_k \langle k | (\sigma_z \otimes \sigma_x) U_{CNOT} | k \rangle$：
- $\langle 00 | (\sigma_z \otimes \sigma_x) U_{CNOT} | 00 \rangle = \langle 00 | (\sigma_z \otimes \sigma_x) | 00 \rangle = \langle 00 | 01 \rangle = 0$
- $\langle 01 | (\sigma_z \otimes \sigma_x) U_{CNOT} | 01 \rangle = \langle 01 | (\sigma_z \otimes \sigma_x) | 01 \rangle = \langle 01 | 00 \rangle = 0$
- $\langle 10 | (\sigma_z \otimes \sigma_x) U_{CNOT} | 10 \rangle = \langle 10 | (\sigma_z \otimes \sigma_x) | 11 \rangle = \langle 10 | (-|10\rangle) = -1$
- $\langle 11 | (\sigma_z \otimes \sigma_x) U_{CNOT} | 11 \rangle = \langle 11 | (\sigma_z \otimes \sigma_x) | 10 \rangle = \langle 11 | (-|11\rangle) = -1$

将这些对角元相加，得到迹为 $0 + 0 - 1 - 1 = -2$。因此，系数 $c_{zx} = \frac{1}{4}(-2) = -\frac{1}{2}$。通过类似计算，可以得到[CNOT门](@entry_id:180955)的完整泡利分解：
$$
U_{CNOT} = \frac{1}{2} (I \otimes I + Z \otimes I + I \otimes X - Z \otimes X)
$$
这个分解形式清晰地表明，[CNOT门](@entry_id:180955)的行为可以理解为四种基本物理过程的叠加：全局的单位演化、控制比特的相位翻转、目标比特的比特翻转，以及一种受控的比特-相位联合翻转。

### [受控非门](@entry_id:180955)与[量子纠缠](@entry_id:136576)

CNOT门最著名的特性是其产生和操控[量子纠缠](@entry_id:136576)的能力。一个 **[纠缠态](@entry_id:152310)** 是指一个[多体量子系统](@entry_id:161678)的状态，它不能被写成其各个子系统状态的[张量积](@entry_id:140694)。

#### 纠缠的产生与贝尔基下的作用

CNOT门是构建[纠缠态](@entry_id:152310)最直接的工具。考虑一个初始处于可分离态 $|+\rangle|0\rangle$ 的[双量子比特系统](@entry_id:203437)，其中 $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$。该初始态可以展开为：
$$
|\psi_{in}\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle) \otimes |0\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |10\rangle)
$$
将CNOT门作用于此态上，利用其线性性质：
$$
U_{CNOT}|\psi_{in}\rangle = \frac{1}{\sqrt{2}}(U_{CNOT}|00\rangle + U_{CNOT}|10\rangle) = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)
$$
最终得到的态 $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$ 是著名的 **贝尔态** 之一。这个态是最大纠缠态，无法写成两个单比特态的乘积，展示了CNOT门如何将一个[经典关联](@entry_id:136367)的输入态（两个比特都可能是0或1，但它们是独立的）转化为一个具有深刻[量子关联](@entry_id:136327)的输出态。

[贝尔态](@entry_id:140749)本身构成了一个双[量子比特](@entry_id:137928)希尔伯特空间的[正交基](@entry_id:264024)，即 **贝尔基**。研究[CNOT门](@entry_id:180955)在贝尔基下的表示，能为我们提供其操控纠缠态的深入见解 [@problem_id:802985]。例如，我们可以计算CNOT在两个贝尔态 $|\Phi^+\rangle$ 和 $|\Psi^+\rangle = \frac{1}{\sqrt{2}}(|01\rangle + |10\rangle)$ 之间的矩阵元 $M = \langle \Phi^+ | U_{CNOT} | \Psi^+ \rangle$。
$$
\begin{align*}
M & = \left( \frac{1}{\sqrt{2}}(\langle 00| + \langle 11|) \right) U_{CNOT} \left( \frac{1}{\sqrt{2}}(|01\rangle + |10\rangle) \right) \\
 &= \frac{1}{2} \left( \langle 00|U_{CNOT}|01\rangle + \langle 00|U_{CNOT}|10\rangle + \langle 11|U_{CNOT}|01\rangle + \langle 11|U_{CNOT}|10\rangle \right) \\
 &= \frac{1}{2} \left( \langle 00|01\rangle + \langle 00|11\rangle + \langle 11|01\rangle + \langle 11|11\rangle \right) \\
 &= \frac{1}{2} (0 + 0 + 0 + 1) = \frac{1}{2}
\end{align*}
$$
这个非零的矩阵元表明[CNOT门](@entry_id:180955)可以诱导不同类型的[纠缠态](@entry_id:152310)之间的跃迁。实际上，CNOT门在贝尔基下的矩阵表示是对角的（在适当调整相位后），这意味着[贝尔态](@entry_id:140749)是CNOT算符的本征态。这一性质在[量子隐形传态](@entry_id:144485)和[超密编码](@entry_id:137220)等量子通信协议中至关重要。

#### [量化纠缠](@entry_id:144669)：并发度

为了更精确地描述纠缠的程度，我们可以引入一个度量，例如 **并发度（Concurrence）**。对于一个纯的双[量子比特](@entry_id:137928)态 $|\psi\rangle$，其并发度定义为 $C(|\psi\rangle) = \sqrt{2(1 - \text{Tr}(\rho_A^2))}$，其中 $\rho_A = \text{Tr}_B(|\psi\rangle\langle\psi|)$ 是对系统B进行部分迹运算后得到的A系统的[约化密度矩阵](@entry_id:146315)。并发度取值范围从0（可分离态）到1（最大[纠缠态](@entry_id:152310)）。

我们可以通过一个“分数阶”[CNOT门](@entry_id:180955)来考察纠缠是如何逐渐产生的 [@problem_id:803011]。考虑一个由参数 $\alpha$ 控制的广义[CNOT门](@entry_id:180955) $U(\alpha) = \exp(i\alpha U_{CNOT})$。由于 $U_{CNOT}^2 = I$，根据[欧拉公式](@entry_id:176440)，其矩阵形式可以简化为 $U(\alpha) = \cos(\alpha)I + i\sin(\alpha)U_{CNOT}$。

将此门作用于初始态 $|\psi_{in}\rangle = |+\rangle|0\rangle = \frac{1}{\sqrt{2}}(|00\rangle+|10\rangle)$：
$$
\begin{align*}
|\psi_{out}\rangle & = U(\alpha) \frac{1}{\sqrt{2}}(|00\rangle+|10\rangle) \\
 &= \frac{1}{\sqrt{2}} \left[ (\cos\alpha + i\sin\alpha)|00\rangle + (\cos\alpha|10\rangle + i\sin\alpha|11\rangle) \right]
\end{align*}
$$
计算A系统的[约化密度矩阵](@entry_id:146315) $\rho_A$，我们得到：
$$
\rho_A = \frac{1}{2} \begin{pmatrix} 1 & \cos\alpha e^{i\alpha} \\ \cos\alpha e^{-i\alpha} & 1 \end{pmatrix}
$$
其迹的平方为 $\text{Tr}(\rho_A^2) = \frac{1}{2} + \frac{1}{2}\cos^2\alpha$。代入并发度公式：
$$
C = \sqrt{2(1 - \text{Tr}(\rho_A^2))} = \sqrt{2(1 - \frac{1}{2} - \frac{1}{2}\cos^2\alpha)} = \sqrt{1 - \cos^2\alpha} = |\sin\alpha|
$$
这个优美的结果表明，通过[调节参数](@entry_id:756220) $\alpha$ 从 $0$ 到 $\pi/2$，我们可以精确地控制输出态的纠缠度，从 $0$ 平滑地增加到 $1$。例如，当 $\alpha = \pi/6$ 时，并发度为 $\sin(\pi/6) = 1/2$。这说明CNOT门不仅仅是一个二元的“开关”，其作用强度可以被连续地调节，从而生成任意指定纠缠度的[量子态](@entry_id:146142)。

### 受控非门的群论性质

将[量子门](@entry_id:143510)视为抽象群的元素，为我们分析量子电路的计算能力、设计量子算法以及构建[量子纠错码](@entry_id:266787)提供了强大的数学框架。

#### [克利福德群](@entry_id:140930)与泡利算符的演化

在[海森堡绘景](@entry_id:141162)中，系统的状态不变，而算符（可观测量）随时间演化。一个算符 $A$ 在幺正变换 $U$ 下的演化由共轭运算 $A' = U A U^\dagger$ 描述。一类特别重要的量子门是 **[克利福德群](@entry_id:140930)（Clifford group）** 的成员，它们能将[泡利群](@entry_id:136414) $G_n$（由 $n$-比特[泡利算符](@entry_id:144061)串和相位因子 $\{\pm 1, \pm i\}$ 构成的群）映射到自身。[CNOT门](@entry_id:180955)正是二比特[克利福德群](@entry_id:140930)的一个核心成员。

这一性质意味着，用[CNOT门](@entry_id:180955)共轭一个泡利串，结果仍然是一个泡利串（可能带有相位）。这个特性使得仅包含[克利福德门](@entry_id:137923)的量子电路可以被经典计算机高效地模拟（[Gottesman-Knill定理](@entry_id:141100)），并且在[量子纠错](@entry_id:139596)中扮演着核心角色，因为它们能将简单的[泡利错误](@entry_id:146391)映射为其他[泡利错误](@entry_id:146391)，从而便于诊断和修正。

让我们通过一个实例来验证[CNOT门](@entry_id:180955)的克利福德特性 [@problem_id:802984]。考虑共轭算符 $X \otimes Y$。对于以第一比特为控制、第二比特为目标的CNOT门 ($U_{12}$)，其对[泡利算符](@entry_id:144061)的变换规则为：$X_1 \to X_1$，$Z_1 \to Z_1 Z_2$，$X_2 \to X_1 X_2$，$Z_2 \to Z_2$。利用这些规则，我们可以分解并变换算符 $X \otimes Y = X_1 Y_2$:
$$
\begin{align*}
A' & = U_{12} (X_1 Y_2) U_{12}^\dagger \\
   & = (U_{12} X_1 U_{12}^\dagger) (U_{12} Y_2 U_{12}^\dagger) \\
   & = X_1 \cdot U_{12} (i X_2 Z_2) U_{12}^\dagger \\
   & = i X_1 (U_{12} X_2 U_{12}^\dagger) (U_{12} Z_2 U_{12}^\dagger) \\
   & = i X_1 (X_1 X_2) Z_2 \\
   & = i (X_1^2 X_2 Z_2) = i (I_1 X_2 Z_2) \\
   & = I \otimes (i XZ) = I \otimes Y
\end{align*}
$$
结果表明，$U_{CNOT} (X \otimes Y) U_{CNOT}^\dagger = I \otimes Y$。一个泡利串被映射到了另一个泡利串，这清晰地证明了CNOT是[克利福德群](@entry_id:140930)的一员。

#### 由量子门生成的群

在[矩阵乘法](@entry_id:156035)下，一个或多个量子门可以生成一个群。这个群的 **阶（order）**，即群中不同元素的数量，反映了该门集所能产生的不同操作的丰富程度。研究这些[有限群的结构](@entry_id:137958)，是理解[量子计算](@entry_id:142712)基本单元能力的关键。

一个经典的例子是研究由[CNOT门](@entry_id:180955)和[SWAP门](@entry_id:147789)生成的群 $G = \langle U_{CNOT}, U_{SWAP} \rangle$ [@problem_id:802931]。[SWAP门](@entry_id:147789)的作用是交换两个[量子比特](@entry_id:137928)的状态，其矩阵为：
$$
U_{SWAP} = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}
$$
我们可以将这些门视为对计算[基矢](@entry_id:199546) $\{|00\rangle, |01\rangle, |10\rangle, |11\rangle\}$ 的[置换](@entry_id:136432)。若将[基矢](@entry_id:199546)索引为 $\{0, 1, 2, 3\}$，则CNOT的作用是[置换](@entry_id:136432) $(2, 3)$，SWAP的作用是[置换](@entry_id:136432) $(1, 2)$。这两者生成的群 $G$ 作用在[子空间](@entry_id:150286) $\text{span}\{|01\rangle, |10\rangle, |11\rangle\}$ 上，同构于3个元素的对称群 $S_3$。$S_3$ 的阶为 $3! = 6$。$G$ 的完整阶数也是6（包含单位元）。$S_3$ 的 **中心（center）**，即与所有群元素对易的元素集合，是平凡的，只包含单位元。因此，群 $G$ 的中心阶为1，这意味着除了单位操作外，不存在任何一个由CNOT和SWAP组合出的操作可以与所有其他操作对易。

另一个重要的例子是CNOT与对角门的组合 [@problem_id:802880] [@problem_id:802971]。考虑由CNOT（记为 $C$）和受控Z门（CZ，记为 $Z_{ctrl}$）生成的群 $G = \langle C, Z_{ctrl} \rangle$。这两个门都是对合的，即 $C^2 = I, Z_{ctrl}^2 = I$。它们的乘积 $P = C \cdot Z_{ctrl}$ 的阶决定了群的结构。计算表明 $(C \cdot Z_{ctrl})^4 = I$，并且没有更小的正整数幂次为单位矩阵。这两个对合及其乘积的阶满足关系 $s^2=t^2=(st)^4=I$，这正是8阶 **[二面体群](@entry_id:143875)** $D_4$（或记为$D_8$）的定义。因此，该[群的阶](@entry_id:137115)为8。将CZ门替换为另一个对角门 $Z \otimes Z$ 也会生成一个同构的群，其阶同样为8。这表明CNOT门与不同类型的[相位门](@entry_id:143669)组合倾向于生成具有相似结构的[二面体群](@entry_id:143875)。

#### 对易关系与[表示论](@entry_id:137998)

量子门之间的对易性是量子电路设计和优化的核心问题。两个算符的 **对易子** $[A, B] = AB - BA$ 度量了它们不可交换的程度。

例如，我们可以考察标准[CNOT门](@entry_id:180955) $U_{CNOT_{12}}$（第一位控制第二位）和反向[CNOT门](@entry_id:180955) $U_{CNOT_{21}}$（第二位控制第一位）之间的[对易关系](@entry_id:136780) [@problem_id:802920]。$U_{CNOT_{21}}$ 可以通过 $U_{SWAP} U_{CNOT_{12}} U_{SWAP}$ 构建。它们的矩阵形式分别为：
$$
U \equiv U_{CNOT_{12}}=\begin{pmatrix} 1&0&0&0\\0&1&0&0\\0&0&0&1\\0&0&1&0 \end{pmatrix}, \quad V \equiv U_{CNOT_{21}}=\begin{pmatrix} 1&0&0&0\\0&0&0&1\\0&0&1&0\\0&1&0&0 \end{pmatrix}
$$
直接计算它们的对易子 $[U, V]$ 得到：
$$
[U,V] = UV-VU = \begin{pmatrix} 0&0&0&0\\ 0&0&-1&1\\ 0&1&0&-1\\ 0&-1&1&0 \end{pmatrix}
$$
这个非零的结果直观地表明了这两种CNOT门是不可交换的，在量子电路中它们的顺序至关重要。我们可以用 **[弗罗贝尼乌斯范数](@entry_id:143384)** $||M||_F = \sqrt{\text{Tr}(M^\dagger M)}$ 来量化这种[非对易性](@entry_id:153545)的大小。对于上述对易子矩阵，其范数为 $\sqrt{6}$。

更进一步，我们可以研究由 $C=U_{CNOT_{12}}$ 和 $R=U_{CNOT_{21}}$ 生成的群 $G = \langle C, R \rangle$ 的代数性质，特别是它的 **[交换子代数](@entry_id:143966)（commutant algebra）** $G'$ [@problem_id:802944]。$G'$ 是所有与 $G$ 中每个元素都对易的 $4 \times 4$ 矩阵构成的集合。$G'$ 是一个[复向量空间](@entry_id:264355)，其维度反映了 $G$ 的对称性结构。

根据[表示论](@entry_id:137998)，一个群的表示的[交换子代数](@entry_id:143966)的维度，等于该[表示分解](@entry_id:139061)为不可约表示（irreps）后，各[不可约表示](@entry_id:263310)出现次数（multiplicity）的平方和，即 $\dim(G') = \sum_i m_i^2$（这源于[舒尔引理](@entry_id:136779)）。
$C$ 和 $R$ 作为[置换](@entry_id:136432)，分别作用为 $(2,3)$ 和 $(1,3)$，它们在[基矢](@entry_id:199546) $\{|01\rangle, |10\rangle, |11\rangle\}$ 上生成了 $S_3$ 群。而[基矢](@entry_id:199546) $|00\rangle$ 在这两个操作下保持不变。因此，$\mathbb{C}^4$ 上的这个表示可以分解为：
$$
\mathbb{C}^4 \cong V_{triv_1} \oplus V_{S_3}
$$
其中 $V_{triv_1}$ 是由 $|00\rangle$ 张成的一维[平凡表示](@entry_id:141357)。而作用在 $V_{S_3}=\text{span}\{|01\rangle, |10\rangle, |11\rangle\}$ 上的三维[置换表示](@entry_id:142960)本身可以进一步分解为一个一维[平凡表示](@entry_id:141357)（由向量 $|01\rangle+|10\rangle+|11\rangle$ 张成）和一个二维的标准不可约表示。
因此，$\mathbb{C}^4$ 上的表示最终分解为：
$$
\mathbb{C}^4 \cong \mathbf{1} \oplus \mathbf{1} \oplus \mathbf{2}
$$
这里，$\mathbf{1}$ 代表一维平凡[不可约表示](@entry_id:263310)，$\mathbf{2}$ 代表二维标准不可约表示。在这个分解中，一维不可约表示的出现次数 $m_1 = 2$，二维不可约表示的出现次数 $m_2 = 1$。
根据[舒尔引理](@entry_id:136779)的推论，[交换子代数](@entry_id:143966)的维度为：
$$
\dim(G') = m_1^2 + m_2^2 = 2^2 + 1^2 = 5
$$
这个维度为5的结果，揭示了与CNOT和反向[CNOT门](@entry_id:180955)同时对易的算符构成的[线性空间](@entry_id:151108)的结构，为理解由这些基本门构成的更复杂量子系统的对称性和[守恒量](@entry_id:150267)提供了深刻的数学工具。