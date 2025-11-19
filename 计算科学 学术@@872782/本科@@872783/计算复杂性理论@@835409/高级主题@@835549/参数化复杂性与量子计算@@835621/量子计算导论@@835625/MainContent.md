## 引言
随着摩尔定律趋近其物理极限，[经典计算](@entry_id:136968)机在处理某些特定类型的复杂问题时开始显现其固有的局限性。在这一背景下，[量子计算](@entry_id:142712)作为一种革命性的计算[范式](@entry_id:161181)应运而生，它利用量子力学的奇特规则——如叠加和纠缠——来处理信息，有望解决[经典计算](@entry_id:136968)无法企及的难题。然而，[量子计算](@entry_id:142712)的世界充满了反直觉的概念和复杂的数学，令许多初学者望而却步。本文旨在系统地揭开[量子计算](@entry_id:142712)的神秘面纱，为读者搭建一座从基本原理到前沿应用的坚实桥梁。

本文将带领读者踏上一场结构化的学习之旅。我们将分为三个核心章节来逐步深入这个激动人心的领域：

1.  **原理与机制**：我们将从[量子计算](@entry_id:142712)的原子单元——[量子比特](@entry_id:137928)（qubit）出发，建立描述其状态、演化和相互作用的数学框架。您将学习到叠加、纠缠、量子门以及[量子线路](@entry_id:151866)等核心概念，为理解量子算法奠定理论基础。

2.  **应用与跨学科交叉**：在掌握了基本原理后，我们将探索[量子计算](@entry_id:142712)如何在[算法设计](@entry_id:634229)、信息安全、物理模拟和[计算化学](@entry_id:143039)等领域大放异彩。通过分析Shor算法、[Grover算法](@entry_id:139156)和[量子密钥分发](@entry_id:138070)等实例，您将领会到[量子计算](@entry_id:142712)的实际威力及其对其他科学领域的深远影响。

3.  **动手实践**：理论学习需要通过实践来巩固。本章提供了一系列精心设计的编程练习，引导您亲手构建和分析简单的量子电路，将抽象的理论知识转化为具体的计算技能。

通过这三个章节的循序渐进的学习，您将不仅理解[量子计算](@entry_id:142712)“是什么”和“为什么”强大，还将初步掌握“如何”应用它。现在，让我们从构建量子世界的第一块基石开始，深入其核心的原理与机制。

## 原理与机制

继前一章对[量子计算](@entry_id:142712)的宏观介绍之后，本章将深入探讨其核心的数学原理与物理机制。我们将从[量子计算](@entry_id:142712)的基本单元——[量子比特](@entry_id:137928)（qubit）开始，系统地构建描述其状态、演化和相互作用的理论框架。理解这些基本原理是掌握量子[算法设计与分析](@entry_id:746357)，并最终领会[量子计算](@entry_id:142712)强大能力的关键。

### [量子态](@entry_id:146142)：[量子比特](@entry_id:137928)与希尔伯特空间

经典计算建立在比特（bit）之上，一个比特的状态非0即1。而[量子计算](@entry_id:142712)则采用**[量子比特](@entry_id:137928)**（**qubit**）作为其基本信息单元。[量子比特](@entry_id:137928)的独特之处在于其能够处于一种**叠加态**（**superposition**），即同时是0和1的线性组合。

#### [状态向量](@entry_id:154607)表示

在数学上，一个孤立的单[量子比特](@entry_id:137928)系统状态由一个二维[复希尔伯特空间](@entry_id:185216)（complex Hilbert space）中的向量描述。这个向量被称为**[状态向量](@entry_id:154607)**，通常用[狄拉克符号](@entry_id:154811)（Dirac notation）记为 $|\psi\rangle$。我们选取一组标准正交基，称为**计算[基态](@entry_id:150928)**（computational basis states），记为 $|0\rangle$ 和 $|1\rangle$。它们分别对应于经典比特的0和1。在[向量表示](@entry_id:166424)中，它们是：

$$
|0\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad |1\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}
$$

任何单[量子比特](@entry_id:137928)的[纯态](@entry_id:141688) $|\psi\rangle$ 都可以表示为这两个[基态](@entry_id:150928)的线性组合：

$$
|\psi\rangle = \alpha|0\rangle + \beta|1\rangle = \begin{pmatrix} \alpha \\ \beta \end{pmatrix}
$$

这里的系数 $\alpha$ 和 $\beta$ 是复数，被称为**概率振幅**（probability amplitudes）。它们不仅编码了状态的信息，还决定了测量结果的概率。

#### 归一化公设

量子力学的一个基本公设要求，任何有效的[量子态](@entry_id:146142)向量必须是归一化的。这意味着状态[向量的范数](@entry_id:154882)（norm）必须为1。对于单[量子比特](@entry_id:137928)态 $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$，[归一化条件](@entry_id:156486)具体表现为概率振幅的模平方和必须等于1：

$$
|\alpha|^2 + |\beta|^2 = 1
$$

这个条件源于[量子测量](@entry_id:272490)的概率解释（即**[玻恩定则](@entry_id:154470)**，Born rule）：当我们对处于 $|\psi\rangle$ 态的[量子比特](@entry_id:137928)在计算基下进行测量时，得到结果0的概率是 $|\alpha|^2$，得到结果1的概率是 $|\beta|^2$。由于测量结果必然是0或1之一，总概率必须为1。

因此，并非任何二维[复向量](@entry_id:192851)都能代表一个物理上有效的[量子比特](@entry_id:137928)状态。例如，我们需要检验一个给定的向量是否满足[归一化条件](@entry_id:156486)和维度要求 [@problem_id:1429332]。考虑向量 $|\psi_A\rangle = \begin{pmatrix} 3/5 \\ (4/5)i \end{pmatrix}$。我们计算其系数的模平方和：

$$
\left|\frac{3}{5}\right|^2 + \left|\frac{4}{5}i\right|^2 = \frac{9}{25} + \frac{16}{25} = 1
$$

由于结果为1，且该向量是二维的，所以 $|\psi_A\rangle$ 是一个有效的单[量子比特](@entry_id:137928)态。然而，对于向量 $|\psi_B\rangle = \begin{pmatrix} 1/\sqrt{2} \\ i \end{pmatrix}$，其模平方和为：

$$
\left|\frac{1}{\sqrt{2}}\right|^2 + |i|^2 = \frac{1}{2} + 1 = \frac{3}{2} \neq 1
$$

因此，它不是一个有效的[量子态](@entry_id:146142)。同样，一个具有三个分量的向量，即使其范数为1，也不能描述一个单[量子比特](@entry_id:137928)，因为它属于一个三维空间（描述的是一个**qutrit**）。

#### 状态的归一化

在[量子算法](@entry_id:147346)的中间步骤中，我们常常会得到一个未归一化的[状态向量](@entry_id:154607)。幸运的是，任何非零向量 $|\psi_{un}\rangle$ 都可以通过乘以一个正实数**归一化常数** $N$ 来转换为一个有效的、归一化的[状态向量](@entry_id:154607) $|\psi\rangle = N |\psi_{un}\rangle$ [@problem_id:1429357]。这个常数 $N$ 的值等于 $|\psi_{un}\rangle$ 范数的倒数：

$$
N = \frac{1}{\sqrt{\langle\psi_{un}|\psi_{un}\rangle}}
$$

其中，[内积](@entry_id:158127) $\langle\psi_{un}|\psi_{un}\rangle$ 是向量中所有概率振幅的模平方之和。例如，假设一个[双量子比特系统](@entry_id:203437)经过一系列操作后处于一个未归一化的状态：

$$
|\psi_{un}\rangle = (1+i)|00\rangle + (2-i)|01\rangle - 2i|10\rangle + 3|11\rangle
$$

其范数的平方为：

$$
\langle\psi_{un}|\psi_{un}\rangle = |1+i|^2 + |2-i|^2 + |-2i|^2 + |3|^2 = (1^2+1^2) + (2^2+(-1)^2) + ((-2)^2) + 3^2 = 2 + 5 + 4 + 9 = 20
$$

因此，归一化常数 $N = \frac{1}{\sqrt{20}} = \frac{1}{2\sqrt{5}}$。物理上有效的[量子态](@entry_id:146142)应为 $|\psi\rangle = \frac{1}{2\sqrt{5}} \left( (1+i)|00\rangle + (2-i)|01\rangle - 2i|10\rangle + 3|11\rangle \right)$。

### [多量子比特系统](@entry_id:142942)与纠缠

当量子系统由多个[量子比特](@entry_id:137928)组成时，其复杂性呈指数级增长，这也是[量子计算](@entry_id:142712)强大潜力的根源。

#### 复合系统：张量积

描述一个由 $n$ 个[量子比特](@entry_id:137928)组成的复合系统的状态空间，是通过取单个[量子比特](@entry_id:137928)[状态空间](@entry_id:177074)的**张量积**（**tensor product**）得到的。一个单[量子比特](@entry_id:137928)生活在 $2$ 维的[希尔伯特空间](@entry_id:261193)中，而一个 $n$ [量子比特](@entry_id:137928)系统则生活在一个 $2^n$ 维的希尔伯特空间中。

例如，一个[双量子比特系统](@entry_id:203437)的计算[基态](@entry_id:150928)由两个单[量子比特](@entry_id:137928)[基态](@entry_id:150928)的张量积构成：$|q_1 q_0\rangle = |q_1\rangle \otimes |q_0\rangle$。这四个[基态](@entry_id:150928)是 $|00\rangle, |01\rangle, |10\rangle, |11\rangle$，它们构成了 $4$ 维[希尔伯特空间](@entry_id:261193)的一组标准正交基。

状态空间的维数随[量子比特](@entry_id:137928)数 $n$ 呈[指数增长](@entry_id:141869)（$2^n$），这对[经典计算](@entry_id:136968)机模拟量子系统构成了巨大挑战 [@problem_id:1429317]。为了在[经典计算](@entry_id:136968)机上精确模拟一个 $n$ [量子比特](@entry_id:137928)的系统，我们需要存储 $2^n$ 个复数（概率振幅）。如果每个复数需要 $2B$ 字节（例如，实部和虚部分别用一个 $B$ 字节的浮点数表示），那么总共需要的内存为 $2B \times 2^n$ 字节。假设一台经典计算机有 $M$ 字节的可用内存，那么它可以模拟的最大[量子比特](@entry_id:137928)数 $n_{\text{max}}$ 必须满足：

$$
2B \cdot 2^{n_{\text{max}}} \leq M \quad \implies \quad n_{\text{max}} \leq \log_2\left(\frac{M}{2B}\right)
$$

由于 $n_{\text{max}}$ 必须是整数，我们得到：

$$
n_{\text{max}} = \left\lfloor \log_2\left(\frac{M}{2B}\right) \right\rfloor
$$

这个结果清楚地表明，经典模拟所需的内存资源随[量子比特](@entry_id:137928)数线性增加而指数爆炸。即使拥有TB级（约 $10^{12}$ 字节）内存的超级计算机，在 $B=8$ 的情况下，也只能模拟大约 $n_{\text{max}} = \lfloor \log_2(10^{12}/16) \rfloor \approx 36$ 个[量子比特](@entry_id:137928)。这从一个侧面揭示了建造物理[量子计算](@entry_id:142712)机的必要性。

#### [可分态与纠缠态](@entry_id:153112)

[多量子比特系统](@entry_id:142942)的状态可以分为两类。如果一个复合系统的状态可以写成其各个子系统状态的[张量积](@entry_id:140694)，则称该状态为**[可分态](@entry_id:142281)**（**separable state**）或**乘积态**（**product state**）。例如，如果第一个[量子比特](@entry_id:137928)处于 $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle)$ 态，第二个[量子比特](@entry_id:137928)处于 $|-\rangle = \frac{1}{\sqrt{2}}(|0\rangle-|1\rangle)$ 态，那么这个[双量子比特系统](@entry_id:203437)的联合状态就是一个[可分态](@entry_id:142281) [@problem_id:1429374]：

$$
|\psi\rangle = |+\rangle \otimes |-\rangle = \frac{1}{2}(|0\rangle+|1\rangle) \otimes (|0\rangle-|1\rangle) = \frac{1}{2}(|00\rangle - |01\rangle + |10\rangle - |11\rangle)
$$

对于[可分态](@entry_id:142281)，对一个子系统的测量不会影响另一个子系统的状态，它们的测量结果在统计上是独立的。

然而，量子力学允许存在更奇特的状态，它们无法表示为子系统状态的张量积。这类状态被称为**纠缠态**（**entangled state**）。纠缠是量子力学最深刻、最反直觉的特性之一，也是[量子计算](@entry_id:142712)和[量子通信](@entry_id:138989)中一种宝贵的资源。在[纠缠态](@entry_id:152310)中，即使各个[量子比特](@entry_id:137928)在空间上相距遥远，它们仍然构成一个不可分割的整体。对其中一个[量子比特](@entry_id:137928)的测量结果会瞬间影响到另一个[量子比特](@entry_id:137928)的可能状态，这种关联性超越了经典物理的解释范畴。最著名的[纠缠态](@entry_id:152310)是[贝尔态](@entry_id:140749)（Bell states），例如 $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle+|11\rangle)$。

#### 纠缠的量度

由于纠缠是一种资源，量化其程度变得十分重要。对于一个由 $a|00\rangle+b|01\rangle+c|10\rangle+d|11\rangle$ 定义的双[量子比特](@entry_id:137928)纯态，一个常用的[纠缠度量](@entry_id:139894)是**并发度**（**concurrence**），其计算公式为 $C(|\phi\rangle) = 2|ad-bc|$ [@problem_id:1429367]。并发度的取值范围为0到1，其中 $C=0$ 表示该状态是[可分态](@entry_id:142281)，而 $C=1$ 表示最大纠缠态。

量子门操作可以产生和改变纠缠。例如，将一个受控非门（CNOT gate）作用于状态 $|\psi_{in}\rangle = \frac{1}{2}(|00\rangle + i|01\rangle - i|10\rangle + |11\rangle)$。该门的作用是当控制位为1时翻转目标位。经过运算，末态为 $|\psi_{out}\rangle = \frac{1}{2}(|00\rangle + i|01\rangle + |10\rangle - i|11\rangle)$。其系数为 $a=1/2, b=i/2, c=1/2, d=-i/2$。计算其并发度：

$$
C = 2|ad-bc| = 2\left|\left(\frac{1}{2}\right)\left(-\frac{i}{2}\right) - \left(\frac{i}{2}\right)\left(\frac{1}{2}\right)\right| = 2\left|-\frac{i}{4} - \frac{i}{4}\right| = 2\left|-\frac{i}{2}\right| = 2 \cdot \frac{1}{2} = 1
$$

结果为1，表明输出态是一个最大纠缠态。

### 量子动力学：门与线路

[量子态](@entry_id:146142)的演化，即[量子计算](@entry_id:142712)的过程，是通过一系列**[量子门](@entry_id:143510)**（**quantum gates**）操作实现的。

#### 么正性与[可逆性原理](@entry_id:175078)

一个孤立量子系统的状态演化由**薛定谔方程**描述，其结果是，任何[量子门](@entry_id:143510)操作在数学上都必须对应一个**么正变换**（**unitary transformation**）。一个矩阵 $U$ 是么正的，如果其[共轭转置](@entry_id:147909) $U^\dagger$（也称为[埃尔米特伴随](@entry_id:187630)）同时也是它的[逆矩阵](@entry_id:140380)，即：

$$
U^\dagger U = U U^\dagger = I
$$

其中 $I$ 是单位矩阵。

么正性的一个直接且至关重要的推论是，所有[量子计算](@entry_id:142712)本质上都是**可逆的**（**reversible**）[@problem_id:1429333]。如果一个[量子态](@entry_id:146142) $|\psi\rangle$ 经过门 $U$ 演化为 $|\psi'\rangle = U|\psi\rangle$，我们总能通过施加 $U^\dagger$ 门来精确地恢复初始状态：

$$
U^\dagger |\psi'\rangle = U^\dagger (U|\psi\rangle) = (U^\dagger U)|\psi\rangle = I|\psi\rangle = |\psi\rangle
$$

由多个[量子门](@entry_id:143510) $U_1, U_2, \dots, U_n$ 组成的整个[量子线路](@entry_id:151866)，其总的变换 $U_{tot} = U_n \dots U_2 U_1$ 也是一个么正变换。因此，整个计算过程可以通过依次施加 $U_1^\dagger, U_2^\dagger, \dots, U_n^\dagger$ 来逆转。这与许多经典的逻辑门（如[与门](@entry_id:166291)AND、[或门](@entry_id:168617)OR）形成鲜明对比，后者会丢失输入信息，因而是不可逆的。

#### 常用量子门

**[单量子比特门](@entry_id:146489)**作用于单个[量子比特](@entry_id:137928)，在数学上由 $2 \times 2$ 的么正矩阵表示。一个极其重要的单比特门是**哈达玛门**（**Hadamard gate**），其[矩阵表示](@entry_id:146025)为：

$$
H = \frac{1}{\sqrt{2}}\begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}
$$

哈达玛门的作用是将计算[基态](@entry_id:150928)转换为均匀的叠加态：$H|0\rangle = \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle) \equiv |+\rangle$ 和 $H|1\rangle = \frac{1}{\sqrt{2}}(|0\rangle-|1\rangle) \equiv |-\rangle$。它是构建量子算法中叠加性的关键工具。

**[多量子比特门](@entry_id:139015)**用于在多个[量子比特](@entry_id:137928)之间建立关联，这是产生纠缠和执行复杂计算所必需的。最经典的双[量子比特](@entry_id:137928)门是**受控非门**（**Controlled-NOT** 或 **CNOT**）。它有两个输入：一个**控制[量子比特](@entry_id:137928)**和一个**目标[量子比特](@entry_id:137928)**。其逻辑是：如果控制比特是 $|1\rangle$，则对目标比特执行一个[非门](@entry_id:169439)（$X$ 门，即翻转 $|0\rangle \leftrightarrow |1\rangle$）；如果控制比特是 $|0\rangle$，则目标比特保持不变。

CNOT门的[矩阵表示](@entry_id:146025)取决于哪个[量子比特](@entry_id:137928)是控制位，以及计算基的排序约定。在标准基 $\{|00\rangle, |01\rangle, |10\rangle, |11\rangle\}$（其中第一个[量子比特](@entry_id:137928)是控制位，第二个是目标位）下，[CNOT门](@entry_id:180955)的作用是 $|10\rangle \leftrightarrow |11\rangle$，其矩阵为：

$$
\text{CNOT} = \begin{pmatrix} 1  0  0  0 \\ 0  1  0  0 \\ 0  0  0  1 \\ 0  0  1  0 \end{pmatrix}
$$

如果我们改变控制位和目标位，矩阵也会随之改变。例如，如果第二个[量子比特](@entry_id:137928)是控制位，第一个是目标位，在基 $\{|q_1 q_0\rangle\}$ 下，该门的作用是 $|01\rangle \leftrightarrow |11\rangle$。而在基约定为 $\{|q_0 q_1\rangle\}$ 的情况下，则是第二个[量子比特](@entry_id:137928)（左边的数字）控制第一个[量子比特](@entry_id:137928)（右边的数字），此时门的作用是 $|10\rangle \leftrightarrow |11\rangle$ [@problem_id:1429330]。理解如何根据门在[基向量](@entry_id:199546)上的作用来构建其[矩阵表示](@entry_id:146025)，是至关重要的技能。

#### 构建[量子线路](@entry_id:151866)

[量子算法](@entry_id:147346)可以被可视化为**[量子线路](@entry_id:151866)**（**quantum circuit**），其中[量子比特](@entry_id:137928)（通常表示为水平线）按顺序通过一系列[量子门](@entry_id:143510)。

一个典型的例子是制备贝尔态 $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$ 的线路 [@problem_id:1429337]。该过程从初始态 $|00\rangle$ 开始：
1.  对第一个[量子比特](@entry_id:137928)施加一个哈达玛门 $H$。这个操作在[双量子比特系统](@entry_id:203437)上由算符 $H \otimes I$ 表示。
    $$
    (H \otimes I)|00\rangle = (H|0\rangle) \otimes (I|0\rangle) = \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle) \otimes |0\rangle = \frac{1}{\sqrt{2}}(|00\rangle+|10\rangle)
    $$
2.  接着，施加一个CNOT门，以第一个[量子比特](@entry_id:137928)为控制位，第二个为目标位。
    $$
    \text{CNOT}\left(\frac{1}{\sqrt{2}}(|00\rangle+|10\rangle)\right) = \frac{1}{\sqrt{2}}(\text{CNOT}|00\rangle + \text{CNOT}|10\rangle) = \frac{1}{\sqrt{2}}(|00\rangle+|11\rangle)
    $$
这个简单的两步过程，将一个完全可分的初始态 $|00\rangle$ 转换为了一个最大[纠缠态](@entry_id:152310)，展示了[量子门](@entry_id:143510)产生纠缠的强大能力。

在更复杂的算法（如[Deutsch-Jozsa算法](@entry_id:143224)或Grover[搜索算法](@entry_id:272182)）中，一个关键构件是**[量子谕示](@entry_id:145592)**（**quantum oracle**）[@problem_id:1429313]。谕示是一个“黑箱”[量子门](@entry_id:143510) $U_f$，它以某种方式编码了一个经典函数 $f: \{0,1\}^n \to \{0,1\}^m$ 的信息。标准的谕示定义为对计算[基态](@entry_id:150928)的作用：

$$
U_f |x\rangle|y\rangle = |x\rangle|y \oplus f(x)\rangle
$$

其中 $\oplus$ 表示[按位异或](@entry_id:269594)。输入寄存器 $|x\rangle$ 保持不变，而函数值 $f(x)$ 被“计算”并加到辅助寄存器 $|y\rangle$ 上。通过巧妙地制备输入态（例如使用哈达玛门），[量子算法](@entry_id:147346)可以利用[量子并行性](@entry_id:137267)，通过一次调用谕示来评估关于函数 $f$ 的全局属性，而经典算法则需要多次调用。

### 基本原理与推论

量子力学的数学形式主义导致了一些深刻的、非经典的推论，这些推论塑造了[量子信息处理](@entry_id:158111)的边界和可能性。

#### [不可克隆定理](@entry_id:146200)

一个最著名的结果是**[不可克隆定理](@entry_id:146200)**（**no-cloning theorem**），它指出：**不可能制造一台通用设备，能够完美复制一个任意的、未知的[量子态](@entry_id:146142)**。这与经典世界形成鲜明对比，在经典世界里，我们可以轻易地读取和复制任何信息。

该定理的证明优雅地展示了量子力学基本原理的力量 [@problem_id:1429349]。假设存在这样一个[通用量子克隆机](@entry_id:146760)，其作用由一个么正算符 $U_{clone}$ 描述。它取一个待克隆的未知态 $|\psi\rangle$ 和一个处于标准“空白”态 $|b\rangle$ 的粒子作为输入，输出两个都处于 $|\psi\rangle$ 态的粒子：

$$
U_{clone}(|\psi\rangle \otimes |b\rangle) = |\psi\rangle \otimes |\psi\rangle
$$

现在，我们用量子力学的**[线性原理](@entry_id:170988)**来检验这个假设。考虑两个正交的状态 $|\psi_1\rangle$ 和 $|\psi_2\rangle$，并构造它们的叠加态 $|\phi\rangle = \frac{1}{\sqrt{2}}(|\psi_1\rangle + |\psi_2\rangle)$。

一方面，如果直接克隆 $|\phi\rangle$，根据克隆机的定义，我们应该得到：

$$
U_{clone}(|\phi\rangle \otimes |b\rangle) = |\phi\rangle \otimes |\phi\rangle = \frac{1}{2}(|\psi_1\rangle + |\psi_2\rangle) \otimes (|\psi_1\rangle + |\psi_2\rangle) = \frac{1}{2}(|\psi_1\psi_1\rangle + |\psi_1\psi_2\rangle + |\psi_2\psi_1\rangle + |\psi_2\psi_2\rangle)
$$

另一方面，由于 $U_{clone}$ 是一个线性算符，我们可以先将输入态展开，再应用克隆机：

$$
U_{clone}(|\phi\rangle \otimes |b\rangle) = U_{clone}\left(\frac{1}{\sqrt{2}}(|\psi_1\rangle \otimes |b\rangle + |\psi_2\rangle \otimes |b\rangle)\right) = \frac{1}{\sqrt{2}}(U_{clone}(|\psi_1\rangle \otimes |b\rangle) + U_{clone}(|\psi_2\rangle \otimes |b\rangle))
$$

根据克隆机的定义，这等于：

$$
\frac{1}{\sqrt{2}}(|\psi_1\rangle \otimes |\psi_1\rangle + |\psi_2\rangle \otimes |\psi_2\rangle)
$$

比较两种方法得到的结果，它们显然是不相等的。第一种方法的结果包含了交叉项 $|\psi_1\psi_2\rangle$ 和 $|\psi_2\psi_1\rangle$，而第二种方法没有。这个矛盾证明了，满足[线性原理](@entry_id:170988)的么正变换不可能实现对任意未知态的完美克隆。

#### [量子计算](@entry_id:142712)的能力：[计算复杂性](@entry_id:204275)一瞥

[不可克隆定理](@entry_id:146200)似乎是一个限制，但[量子计算](@entry_id:142712)的真正力量在于其处理信息的方式。在[计算复杂性理论](@entry_id:272163)的框架下，我们可以更精确地讨论这种力量。

- **P (Polynomial time)**：包含所有可以由经典计算机在[多项式时间](@entry_id:263297)内解决的[判定问题](@entry_id:636780)。
- **BQP (Bounded-error Quantum Polynomial time)**：包含所有可以由[量子计算](@entry_id:142712)机在[多项式时间](@entry_id:263297)内解决，且[错误概率](@entry_id:267618)有界的[判定问题](@entry_id:636780)。

目前已严格证明的关系是 **P $\subseteq$ BQP** [@problem_id:1429311]。这意味着，任何[经典计算](@entry_id:136968)机能有效解决的问题（例如，在[P类](@entry_id:262479)中的`NetworkFlow`问题），[量子计算](@entry_id:142712)机也同样能有效解决。因此，原则上，我们可以为`NetworkFlow`问题设计一个多项式时间的[量子算法](@entry_id:147346)。

然而，计算理论界普遍猜测（但尚未证明）**P $\neq$ BQP**，即存在一些问题在BQP中但不在P中。最著名的候选问题是**[整数分解](@entry_id:138448)**（`IntegerFactorization`），Shor算法证明了它在BQP中。如果这个猜测成立，那么[量子计算](@entry_id:142712)机将能够有效解决经典计算机无法解决的问题，从而带来计算能力的飞跃。理解BQP与P以及其他复杂性类（如NP和[PSPACE](@entry_id:144410)）之间的关系，是[量子计算](@entry_id:142712)理论研究的核心课题。

本章我们从[量子比特](@entry_id:137928)的定义出发，逐步建立了多比特系统、[量子门](@entry_id:143510)、[量子线路](@entry_id:151866)以及纠缠等核心概念的数学描述。我们还探讨了么正性、可逆性和[不可克隆定理](@entry_id:146200)等基本原理。这些构成了理解后续章节中具体量子算法和协议的坚实基础。