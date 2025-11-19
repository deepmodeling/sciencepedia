## 引言
[量子信息论](@entry_id:141608)是融合了量子力学与信息科学的一门革命性[交叉](@entry_id:147634)学科，它从根本上改变了我们对计算、通信和信息本质的理解。在经典世界中，信息由确定的比特（0或1）承载；然而，在微观的量子领域，信息遵循着截然不同的、甚至违反直觉的规则。这门学科旨在解答一个核心问题：我们如何利用叠加和纠缠等量子特性来处理和传输信息，从而实现超越经典能力的任务？本文正是为了填补从抽象量子原理到具体信息处理应用之间的知识鸿沟而设计，旨在为读者构建一个坚实的量子信息论知识框架。

在接下来的内容中，您将踏上一段系统性的学习之旅。第一章 **“原理与机制”** 将为您揭示量子信息的基本构件——[量子比特](@entry_id:137928)，深入剖析叠加、测量、[量子门](@entry_id:143510)以及“鬼魅般”的量子纠缠。第二章 **“应用与[交叉](@entry_id:147634)学科联系”** 将展示这些原理如何转化为强大的应用，从颠覆性的[量子算法](@entry_id:147346)和无法破解的量子密码，到其在[热力学](@entry_id:141121)和凝聚态物理等领域催生的新洞见。最后，在 **“动手实践”** 部分，您将有机会通过具体问题，将理论知识应用于实践，巩固对核心概念的理解。现在，让我们从构建量子信息世界的基础开始。

## 原理与机制

与依赖于明确的0或1状态的经典比特不同，量子信息的基本单位——**[量子比特](@entry_id:137928) (qubit)** ——存在于一个更丰富、更复杂的现实中。本章旨在阐述支配[量子比特](@entry_id:137928)行为的核心原理，并剖析其用于信息处理的关键机制。我们将从单个[量子比特](@entry_id:137928)的表示法开始，逐步过渡到[多量子比特系统](@entry_id:142942)、量子纠缠的非凡特性，并最终建立一个通用框架来描述[量子态](@entry_id:146142)及其演化，即使在存在噪声的情况下也是如此。

### [量子比特](@entry_id:137928)：信息的新基石

#### 态矢量与叠加

[量子信息](@entry_id:137721)的核心是**叠加原理 (superposition principle)**。一个[量子比特](@entry_id:137928)的状态不是非0即1，而是可以同时是0和1的某种组合。我们使用一种称为**态矢量**的数学对象来描述这种状态，并采用物理学家 Paul Dirac 引入的**[狄拉克符号](@entry_id:154811) (Dirac notation)** 或“bra-ket”符号来书写。

一个[量子比特](@entry_id:137928)的状态 $|\psi\rangle$ (读作 "ket psi") 是一个位于二维[复向量空间](@entry_id:264355)（称为**[希尔伯特空间](@entry_id:261193)**）中的矢量。这个空间由两个特殊的态矢量——**计算[基矢](@entry_id:199546) (computational basis states)** $|0\rangle$ 和 $|1\rangle$——张成。它们分别对应经典比特的0和1。在矩阵表示中，它们是正交的单位矢量：

$$
|0\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad |1\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}
$$

根据叠加原理，任何[量子比特](@entry_id:137928)的态都可以写成这两个[基矢](@entry_id:199546)的线性组合：

$$
|\psi\rangle = \alpha|0\rangle + \beta|1\rangle
$$

这里的系数 $\alpha$ 和 $\beta$ 被称为**概率幅 (probability amplitudes)**，它们是复数。这些概率幅并非任意，它们必须满足**[归一化条件](@entry_id:156486) (normalization condition)**：

$$
|\alpha|^2 + |\beta|^2 = 1
$$

这个条件确保了当我们测量[量子比特](@entry_id:137928)时，其结果为0或1的总概率为1。[概率幅](@entry_id:150609)的模平方 $|\alpha|^2$ 和 $|\beta|^2$ 分别代表了测量时发现[量子比特](@entry_id:137928)处于$|0\rangle$态或$|1\rangle$态的概率。

#### 布洛赫球：一种几何直观

虽然概率幅 $\alpha$ 和 $\beta$ 是复数，但我们可以用一种巧妙的方式将[量子比特](@entry_id:137928)的状态可视化。由于归一化和一个[全局相位](@entry_id:147947)的自由度，一个纯态[量子比特](@entry_id:137928)的状态可以用一个三维单位球面上的点来唯一表示，这个球面被称为**布洛赫球 (Bloch sphere)**。

一个任意的单[量子比特](@entry_id:137928)态 $|\psi\rangle$ 可以用两个实数角 $\theta$ (极角) 和 $\phi$ (方位角) 来参数化 [@problem_id:1633805]：

$$
|\psi\rangle = \cos\left(\frac{\theta}{2}\right)|0\rangle + e^{i\phi}\sin\left(\frac{\theta}{2}\right)|1\rangle
$$

其中 $0 \le \theta \le \pi$ 且 $0 \le \phi  2\pi$。在这个表示中：
-   布洛赫球的“北极”($\theta=0$) 对应于 $|0\rangle$ 态。
-   “南极”($\theta=\pi$) 对应于 $|1\rangle$ 态。
-   所有其他的点都代表 $|0\rangle$ 和 $|1\rangle$ 的叠加态。例如，一个非常重要的状态，被称为**加态** ($|+\rangle$)，位于球的赤道上（$\theta=\pi/2$, $\phi=0$），其表达式为 $|\psi\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$ [@problem_id:1633815]。

重要的是，两个互为正交的态在布洛赫球上表现为两个相对的点。例如，与 $|+\rangle$ 正交的 $|-\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)$ 位于赤道的另一端。[相对相位](@entry_id:148120) $e^{i\phi}$ 是[量子计算](@entry_id:142712)中一个至关重要的资源，它在经典计算中没有对应物。

### 观测量子世界：测量与期望

#### [玻恩定则](@entry_id:154470)与态坍缩

[量子比特](@entry_id:137928)的叠加态在其被测量之前一直保持。**[量子测量](@entry_id:272490) (quantum measurement)** 是一个将量子不确定性转化为经典确定性结果的过程。根据量子力学的基本公理，测量会不可逆地改变[量子态](@entry_id:146142)。

如果我们想知道处于 $|\psi\rangle$ 态的[量子比特](@entry_id:137928)在测量时是否会得到某个特定的目标态 $|\chi\rangle$，其概率由**[玻恩定则](@entry_id:154470) (Born's rule)** 给出 [@problem_id:1633805]：

$$
P(\text{outcome is } |\chi\rangle) = |\langle\chi|\psi\rangle|^2
$$

这里的 $\langle\chi|$ (读作 "bra chi") 是 $|\chi\rangle$ 的[共轭转置](@entry_id:147909)，而 $\langle\chi|\psi\rangle$ 是两个态矢量之间的**[内积](@entry_id:158127) (inner product)**。如果测量结果确实是 $|\chi\rangle$，那么测量之后，[量子比特](@entry_id:137928)的状态就**坍缩 (collapse)** 到了 $|\chi\rangle$。

例如，假设一个[量子比特](@entry_id:137928)被制备在由 $\theta = \pi/3$ 和 $\phi = \pi/2$ 定义的状态 $|\psi\rangle = \cos(\pi/6)|0\rangle + i\sin(\pi/6)|1\rangle = \frac{\sqrt{3}}{2}|0\rangle + \frac{i}{2}|1\rangle$。如果我们想测量它是否处于目标态 $|\chi\rangle = \frac{1}{\sqrt{5}}(|0\rangle + 2i|1\rangle)$，我们首先计算[内积](@entry_id:158127)：

$$
\langle\chi|\psi\rangle = \left( \frac{1}{\sqrt{5}}(\langle0| - 2i\langle1|) \right) \left( \frac{\sqrt{3}}{2}|0\rangle + \frac{i}{2}|1\rangle \right) = \frac{1}{\sqrt{5}} \left( \frac{\sqrt{3}}{2} + (-2i)\left(\frac{i}{2}\right) \right) = \frac{1}{\sqrt{5}}\left(\frac{\sqrt{3}}{2} + 1\right)
$$

因此，测量得到 $|\chi\rangle$ 的概率为 $P = |\langle\chi|\psi\rangle|^2 = \frac{1}{5}(\frac{\sqrt{3}}{2} + 1)^2 = \frac{7+4\sqrt{3}}{20}$ [@problem_id:1633805]。

在计算基上的标准测量是一个特例，它回答了“[量子比特](@entry_id:137928)是处于$|0\rangle$态还是$|1\rangle$态？”这个问题。在这种情况下，得到0的概率是 $|\langle0|\psi\rangle|^2=|\alpha|^2$，得到1的概率是 $|\langle1|\psi\rangle|^2=|\beta|^2$。重要的是，这个过程是不可逆的，并且会丢失关于原始[概率幅](@entry_id:150609)之间相对相位 $e^{i\phi}$ 的信息。一个假想的设备如果试图通过测量大量相同[量子比特](@entry_id:137928)的副本来“克隆”一个未知的[量子态](@entry_id:146142) $|\psi\rangle = \frac{1}{\sqrt{2}}(|0\rangle + e^{i\phi}|1\rangle)$，它只能确定概率 $|\alpha|^2=1/2$ 和 $|\beta|^2=1/2$。如果它基于此重建一个相位为零的态 $|\psi_{rec}\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle)$，那么重建态与原始态之间的**保真度 (fidelity)** $F = |\langle\psi|\psi_{rec}\rangle|^2$ 将是 $F = \cos^2(\phi/2)$ [@problem_id:1633811]。这表明，除非原始相位 $\phi$ 恰好为0，否则信息将丢失，这从根本上揭示了**量子[不可克隆定理](@entry_id:146200) (no-cloning theorem)** 的一个方面：我们无法完美地复制一个未知的[量子态](@entry_id:146142)。

#### [可观测量](@entry_id:267133)之[期望值](@entry_id:153208)

除了投影到特定状态外，我们通常更关心某个物理量（称为**可观测量 (observable)**）的平均值。在量子力学中，每个可观测量都由一个**厄米算符 (Hermitian operator)** $M$ (即 $M=M^\dagger$，其中 $M^\dagger$ 是 $M$ 的共轭转置) 来表示。

对于处于 $|\psi\rangle$ 态的系统，[可观测量](@entry_id:267133) $M$ 的**[期望值](@entry_id:153208) (expectation value)** 定义为：

$$
\langle M \rangle = \langle\psi|M|\psi\rangle
$$

这个值代表了在大量相同制备的[量子态](@entry_id:146142)上测量 $M$ 所得到的平均结果。例如，一个重要的[可观测量](@entry_id:267133)是泡利-Z算符 $\sigma_z$，它描述了[量子比特](@entry_id:137928)沿z轴的“自旋”投影。它的[期望值](@entry_id:153208) $\langle\sigma_z\rangle$ 告诉我们[量子比特](@entry_id:137928)更倾向于 $|0\rangle$ 态 (此时 $\langle\sigma_z\rangle = +1$) 还是 $|1\rangle$ 态 (此时 $\langle\sigma_z\rangle = -1$)。对于一般态 $|\psi\rangle=\alpha|0\rangle+\beta|1\rangle$，[期望值](@entry_id:153208)为 $\langle\sigma_z\rangle = |\alpha|^2 - |\beta|^2$ [@problem_id:1633769]。这个计算展示了[期望值](@entry_id:153208)是如何从概率幅中提取出平均物理信息的。

### [量子操作](@entry_id:145906)的语言：门和矩阵

#### [单量子比特门](@entry_id:146489)：泡利算符与阿达马门

正如经典计算机使用[逻辑门](@entry_id:142135)（如与、或、非）来处理比特一样，[量子计算](@entry_id:142712)机使用**量子门 (quantum gates)** 来操纵[量子比特](@entry_id:137928)。[量子门](@entry_id:143510)是对[量子比特](@entry_id:137928)态矢量进行的数学变换。由于[量子态](@entry_id:146142)的演化必须保持归一化（即[概率守恒](@entry_id:149166)），所有[量子门](@entry_id:143510)都必须是**幺正算符 (unitary operators)**。一个算符 $U$ 是幺正的，如果它的[厄米共轭](@entry_id:191215) $U^\dagger$ 也是它的逆，即 $UU^\dagger = U^\dagger U = I$ (其中 $I$ 是[单位矩阵](@entry_id:156724))。

[单量子比特门](@entry_id:146489)是用 $2 \times 2$ 的幺正[矩阵表示](@entry_id:146025)的。一些最基本的门包括：
-   **[泡利算符](@entry_id:144061) (Pauli operators)**：$\sigma_x, \sigma_y, \sigma_z$。它们是[量子信息论](@entry_id:141608)的基石。
    $$
    \sigma_x = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}, \quad \sigma_y = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}, \quad \sigma_z = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}
    $$
    $\sigma_x$ 门也被称为比特翻转门（NO[T门](@entry_id:138474)），$\sigma_z$ 是相位翻转门。这些算符具有重要的代数关系。例如，它们互不对易但反对易。例如，通过直接的矩阵乘法，可以验证 $\sigma_y\sigma_z = -\sigma_z\sigma_y$ [@problem_id:1633780]。这意味着它们的**[反交换](@entry_id:186708)子 (anti-commutator)** $\{\sigma_y, \sigma_z\} = \sigma_y\sigma_z + \sigma_z\sigma_y$ 为[零矩阵](@entry_id:155836)。这种[非对易性](@entry_id:153545)是量子力学与经典物理的根本区别之一。

-   **阿达马门 (Hadamard gate)**：$H$ 门是产生叠加态的关键。
    $$
    H = \frac{1}{\sqrt{2}}\begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}
    $$
    它将计算[基矢](@entry_id:199546)变换为均匀叠加态：$H|0\rangle = |+\rangle$ 和 $H|1\rangle = |-\rangle$。

量子算法通常由一系列相继作用的[量子门](@entry_id:143510)构成。如果一个门 $U_1$ 先作用，然后是 $U_2$，那么总操作由矩阵乘积 $U_2 U_1$ 描述。例如，如果一个初始处于 $|+\rangle$ 态的[量子比特](@entry_id:137928)先经过一个泡利-Z门，再经过一个阿达马门，其最终状态 $| \psi_f \rangle$ 将是 $H(Z|+\rangle) = |1\rangle$ [@problem_id:1633815]。这个例子说明了门操作的顺序至关重要。

#### [多量子比特系统](@entry_id:142942)与张量积

当处理多个[量子比特](@entry_id:137928)时，我们需要一种新的数学工具来组合它们的希尔伯特空间。这个工具就是**[张量积](@entry_id:140694) (tensor product)**，用符号 $\otimes$ 表示。一个由两个[量子比特](@entry_id:137928)组成的系统的[状态空间](@entry_id:177074)是它们各自空间的[张量积](@entry_id:140694)。如果第一个[量子比特](@entry_id:137928)处于 $|a\rangle$ 态，第二个处于 $|b\rangle$ 态，那么这个两[量子比特](@entry_id:137928)系统的联合状态就是 $|a\rangle \otimes |b\rangle$，通常简写为 $|ab\rangle$。

两[量子比特](@entry_id:137928)系统的计算[基矢](@entry_id:199546)由四个态构成：$\{|00\rangle, |01\rangle, |10\rangle, |11\rangle\}$。一个普遍的两[量子比特](@entry_id:137928)态是这四个[基矢](@entry_id:199546)的叠加。

作用在[多量子比特系统](@entry_id:142942)上的门同样通过[张量积](@entry_id:140694)来构建。如果我们要对第一个[量子比特](@entry_id:137928)应用阿达马门 $H$，同时对第二个[量子比特](@entry_id:137928)什么都不做（即应用单位门 $I$），那么整个操作就是 $H \otimes I$ [@problem_id:1633792]。当这个组合门作用于初始态 $|00\rangle$ 时，结果是：
$$
(H \otimes I)|00\rangle = (H|0\rangle) \otimes (I|0\rangle) = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle) \otimes |0\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |10\rangle)
$$
这个结果是一个**纠缠态 (entangled state)** 的前奏。

#### 纠缠门：CNOT算符

虽然单比特门和它们的张量积很有用，但[量子计算](@entry_id:142712)的真正威力来自于能够创建和操纵[量子比特](@entry_id:137928)之间关联的门。这类门中最著名的是**受控非门 (Controlled-NOT or CNOT)**。

[CNOT门](@entry_id:180955)是一个两[量子比特](@entry_id:137928)门。它有一个**控制[量子比特](@entry_id:137928) (control qubit)** 和一个**目标[量子比特](@entry_id:137928) (target qubit)**。它的作用是：如果控制[量子比特](@entry_id:137928)是 $|1\rangle$，它就翻转（应用NOT或 $\sigma_x$）目标[量子比特](@entry_id:137928)；如果控制[量子比特](@entry_id:137928)是 $|0\rangle$，它就不做任何操作。以第一个[量子比特](@entry_id:137928)为控制，第二个为目标，其在计算[基矢](@entry_id:199546)上的作用为：
-   CNOT$|00\rangle = |00\rangle$
-   CNOT$|01\rangle = |01\rangle$
-   CNOT$|10\rangle = |11\rangle$
-   CNOT$|11\rangle = |10\rangle$

在 $\{|00\rangle, |01\rangle, |10\rangle, |11\rangle\}$ [基矢](@entry_id:199546)下，它的[矩阵表示](@entry_id:146025)为：
$$
\text{CNOT} = \begin{pmatrix} 1  0  0  0 \\ 0  1  0  0 \\ 0  0  0  1 \\ 0  0  1  0 \end{pmatrix}
$$
CNOT门，结合[单量子比特门](@entry_id:146489)，构成了**[通用量子计算](@entry_id:137200) (universal quantum computation)** 的基础，意味着任何量子算法都可以由这些门组合而成。

### [量子纠缠](@entry_id:136576)：“鬼魅般的超距作用”

#### 可分离态与纠缠态

爱因斯坦曾将**量子纠缠 (quantum entanglement)** 著名地称为“[鬼魅般的超距作用](@entry_id:143486)”。它是指两个或多个[量子比特](@entry_id:137928)的状态以一种无法独立描述的方式关联在一起。

如果一个两[量子比特](@entry_id:137928)系统的状态可以写成两个单[量子比特](@entry_id:137928)状态的张量积，即 $|\psi\rangle = |\psi_A\rangle \otimes |\psi_B\rangle$，那么这个状态被称为**可分离的 (separable)**。这意味着对第一个[量子比特](@entry_id:137928)的测量结果与第二个[量子比特](@entry_id:137928)无关。

然而，存在大量无法这样分解的状态，它们被称为**[纠缠态](@entry_id:152310)**。最著名的例子是**贝尔态 (Bell states)**。例如，**$|\Phi^+\rangle$ 贝尔态**可以这样创建：从 $|00\rangle$ 开始，对第一个[量子比特](@entry_id:137928)应用阿达马门，然后应用一个以第一个[量子比特](@entry_id:137928)为控制的[CNOT门](@entry_id:180955)。
1.  初始态：$|00\rangle$
2.  应用 $H \otimes I$：$\frac{1}{\sqrt{2}}(|00\rangle + |10\rangle)$
3.  应用 CNOT：CNOT$\left(\frac{1}{\sqrt{2}}(|00\rangle + |10\rangle)\right) = \frac{1}{\sqrt{2}}(\text{CNOT}|00\rangle + \text{CNOT}|10\rangle) = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$

最终得到的态 $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$ 就是一个最大[纠缠态](@entry_id:152310)。在这个状态下，如果你测量第一个[量子比特](@entry_id:137928)得到0，你就能瞬间确定第二个[量子比特](@entry_id:137928)也必定是0，反之亦然，无论它们相距多远。这种完美的关联是经典世界中不存在的。

#### 识别纠缠：[施密特分解](@entry_id:145934)

我们如何严格地判断一个给定的[纯态](@entry_id:141688) $|\psi\rangle = \sum_{j,k} C_{jk} |j\rangle_A |k\rangle_B$ 是否纠缠？**[施密特分解](@entry_id:145934) (Schmidt decomposition)** 提供了一个强大的工具。任何两体[纯态](@entry_id:141688)都可以被写成一种特殊的形式：
$$
|\psi\rangle = \sum_k \lambda_k |u_k\rangle_A |v_k\rangle_B
$$
其中 $\{|u_k\rangle_A\}$ 和 $\{|v_k\rangle_B\}$ 分别是子系统A和B的正交基，$\lambda_k$ 是称为**[施密特系数](@entry_id:137823) (Schmidt coefficients)** 的非负实数，且满足 $\sum_k \lambda_k^2=1$。

非零[施密特系数](@entry_id:137823)的数量被称为**[施密特数](@entry_id:141441) (Schmidt number)**。这是衡量纠缠的直接指标：
-   如果[施密特数](@entry_id:141441)为1，态是可分离的。
-   如果[施密特数](@entry_id:141441)大于1，态是纠缠的。

要计算[施密特数](@entry_id:141441)，我们可以构建系数矩阵 $C$ (其元素为 $C_{jk}$)，然后计算 $C^\dagger C$ 的[特征值](@entry_id:154894)。这些[特征值](@entry_id:154894)的平方根就是[施密特系数](@entry_id:137823)。例如，对于态 $|\psi\rangle = \frac{1}{\sqrt{3}}|00\rangle + i\sqrt{\frac{2}{3}}|11\rangle$ [@problem_id:1633756]，其[系数矩阵](@entry_id:151473)为 $C = \begin{pmatrix} 1/\sqrt{3}  0 \\ 0  i\sqrt{2/3} \end{pmatrix}$。我们发现 $C^\dagger C = \begin{pmatrix} 1/3  0 \\ 0  2/3 \end{pmatrix}$。这个矩阵有两个非零[特征值](@entry_id:154894)（1/3和2/3），因此有两个非零[施密特系数](@entry_id:137823)。[施密特数](@entry_id:141441)为2，这意味着该态是纠缠的。

### 描述现实：[纯态](@entry_id:141688)、[混合态](@entry_id:141568)与密度矩阵

#### 从经典不确定性到混合态

到目前为止，我们都假设[量子比特](@entry_id:137928)处于一个明确的**[纯态](@entry_id:141688) (pure state)**，可以用一个唯一的态矢量 $|\psi\rangle$ 来描述。然而，在现实世界中，我们常常缺乏关于系统的完整信息。例如，一个有缺陷的设备可能以 $p_1$ 的概率制备出 $|\psi_1\rangle$ 态，以 $p_2$ 的概率制备出 $|\psi_2\rangle$ 态，等等。这种由经典概率混合而成的[量子态](@entry_id:146142)被称为**[混合态](@entry_id:141568) (mixed state)**。

态矢量不足以描述[混合态](@entry_id:141568)。为此，我们引入一个更通用的工具：**[密度矩阵](@entry_id:139892) (density matrix)** (或[密度算符](@entry_id:138151)) $\rho$。
-   对于一个[纯态](@entry_id:141688) $|\psi\rangle$，其[密度矩阵](@entry_id:139892)定义为 $\rho = |\psi\rangle\langle\psi|$。
-   对于一个混合态，它是各个纯态密度矩阵的加权平均：$\rho = \sum_i p_i |\psi_i\rangle\langle\psi_i|$。

例如，一个设备以75%的概率产生 $|0\rangle$，25%的概率产生 $|1\rangle$，其产生的系综（ensemble）由密度矩阵描述 [@problem_id:1633770]：
$$
\rho = 0.75 |0\rangle\langle0| + 0.25 |1\rangle\langle1| = \begin{pmatrix} 0.75  0 \\ 0  0.25 \end{pmatrix}
$$

#### 纠缠作为[混合态](@entry_id:141568)的来源

令人惊讶的是，经典不确定性并不是混合态的唯一来源。即使整个复合系统处于一个纯态，其子系统也可能处于混合态。这种情况当且仅当复合系统是[纠缠态](@entry_id:152310)时发生。

要描述一个子系统A的状态，我们需要从整个系统AB的[密度矩阵](@entry_id:139892) $\rho_{AB}$ 出发，然后“忽略”或“追踪掉”子系统B的自由度。这个过程称为**[偏迹](@entry_id:146482) (partial trace)**，记作 $\rho_A = \text{Tr}_B(\rho_{AB})$。

考虑之前提到的[贝尔态](@entry_id:140749) $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$。这是一个纯态。其联合密度矩阵为 $\rho_{AB} = |\Phi^+\rangle\langle\Phi^+|$。如果我们只对第一个[量子比特](@entry_id:137928)A感兴趣，我们计算其**[约化密度矩阵](@entry_id:146315) (reduced density matrix)** $\rho_A$ [@problem_id:1633793]：
$$
\rho_A = \text{Tr}_B(\rho_{AB}) = \frac{1}{2}|0\rangle_A\langle0|_A + \frac{1}{2}|1\rangle_A\langle1|_A = \frac{1}{2}\begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} = \frac{1}{2}I
$$
这个结果是单[量子比特](@entry_id:137928)的**[最大混合态](@entry_id:137775) (maximally mixed state)**。它意味着，尽管整个两比特系统处于一个完全确定的[纯态](@entry_id:141688)，但单独观察其中一个[量子比特](@entry_id:137928)，它看起来就像一个完全随机的经典比特，有一半概率是0，一半概率是1。纠缠将信息编码在[量子比特](@entry_id:137928)之间的关联中，而不是单个[量子比特](@entry_id:137928)本身。

#### 量化信息与纯度：熵与纯度

我们可以量化一个态的混合程度。
-   **纯度 (Purity)**：定义为 $\gamma = \text{Tr}(\rho^2)$。对于[纯态](@entry_id:141688)，$\gamma=1$。对于任何混合态，$\gamma  1$。对于一个d维系统，最小纯度为$1/d$（对应[最大混合态](@entry_id:137775)）。对于前面提到的[混合态](@entry_id:141568) $\rho = \begin{pmatrix} 0.75  0 \\ 0  0.25 \end{pmatrix}$，其纯度为 $\gamma = \text{Tr}(\rho^2) = 0.75^2 + 0.25^2 = 0.625$ [@problem_id:1633770]。

-   **[冯·诺依曼熵](@entry_id:143216) (Von Neumann Entropy)**：这是香农熵的[量子模拟](@entry_id:145469)，衡量了我们对[量子态](@entry_id:146142)的不确定性。它定义为 $S(\rho) = -\text{Tr}(\rho \ln \rho)$。对于纯态，$S(\rho)=0$。对于混合态，$S(\rho)  0$。这个量可以通过[密度矩阵的特征值](@entry_id:204442) $\lambda_i$ 计算：$S(\rho) = -\sum_i \lambda_i \ln \lambda_i$。
    对于一个以50%概率为$|0\rangle$和50%概率为$|1\rangle$的[最大混合态](@entry_id:137775)，其[密度矩阵](@entry_id:139892)为 $\rho = \frac{1}{2}I$，[特征值](@entry_id:154894)为 $1/2, 1/2$。其[冯·诺依曼熵](@entry_id:143216)为 $S = -(\frac{1}{2}\ln\frac{1}{2} + \frac{1}{2}\ln\frac{1}{2}) = \ln 2$ [@problem_id:1633795] [@problem_id:1633793]。这是一个[量子比特](@entry_id:137928)能拥有的最大熵，代表了信息的完全缺失。

### 量子过程与噪声：[算符和表示](@entry_id:140073)

#### 一般[量子操作](@entry_id:145906)

[幺正演化](@entry_id:145020) ($|\psi'\rangle = U|\psi\rangle$ 或 $\rho' = U\rho U^\dagger$) 描述了孤立、完美的量子系统。然而，现实中的量子系统总是与环境相互作用，导致噪声和**退相干 (decoherence)**。我们需要一个更普适的框架来描述这些**量子过程 (quantum processes)** 或**[量子信道](@entry_id:145403) (quantum channels)**。

**[算符和表示](@entry_id:140073) (operator-sum representation)** 提供这样一个框架。任何物理上允许的[量子操作](@entry_id:145906) $\mathcal{E}$ 都可以表示为：
$$
\rho' = \mathcal{E}(\rho) = \sum_k E_k \rho E_k^\dagger
$$
其中 $E_k$ 是一组被称为**[克劳斯算符](@entry_id:144882) (Kraus operators)** 的矩阵。这个形式自动保证了变换是**完全正定的 (completely positive)**，这是物理实在性的一个关键要求。

#### [完备性关系](@entry_id:139077)：[概率守恒](@entry_id:149166)

[量子操作](@entry_id:145906)必须保持总概率为1，这意味着[密度矩阵的迹](@entry_id:145147)必须始终为1（$\text{Tr}(\rho)=1$）。一个量子信道 $\mathcal{E}$ 是**保迹的 (trace-preserving)** 当且仅当它的[克劳斯算符](@entry_id:144882)满足**[完备性关系](@entry_id:139077) (completeness relation)** [@problem_id:1633782]：
$$
\sum_k E_k^\dagger E_k = I
$$
这个关系是验证一个理论模型是否描述了一个有效物理过程的基本检查。例如，考虑一个描述[振幅阻尼](@entry_id:146861)（[能量耗散](@entry_id:147406)）的信道，其[克劳斯算符](@entry_id:144882)为 $E_0 = \begin{pmatrix} 1  0 \\ 0  \sqrt{1-p} \end{pmatrix}$ 和 $E_1 = \begin{pmatrix} 0  \sqrt{p} \\ 0  0 \end{pmatrix}$，其中 $p$ 是发生错误的概率。我们可以验证：
$$
E_0^\dagger E_0 + E_1^\dagger E_1 = \begin{pmatrix} 1  0 \\ 0  1-p \end{pmatrix} + \begin{pmatrix} 0  0 \\ 0  p \end{pmatrix} = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} = I
$$
因此，这组[克劳斯算符](@entry_id:144882)描述了一个有效的、保迹的[量子操作](@entry_id:145906)。相反，如果给定的算符集不满足这个关系，那么它就不代表一个[封闭系统](@entry_id:139565)中发生的完整物理过程 [@problem_id:1633782]。

通过这些原理和机制，我们构建了[量子信息论](@entry_id:141608)的基础。从单个[量子比特](@entry_id:137928)的叠加，到多[量子比特](@entry_id:137928)的纠缠，再到用于描述真实世界系统的[密度矩阵](@entry_id:139892)和[量子操作](@entry_id:145906)，这一系列概念为探索[量子计算](@entry_id:142712)、[量子通信](@entry_id:138989)和[量子传感](@entry_id:138398)的巨大潜力铺平了道路。