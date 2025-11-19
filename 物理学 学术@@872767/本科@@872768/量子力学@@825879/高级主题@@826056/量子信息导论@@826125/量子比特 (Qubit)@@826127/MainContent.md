## 引言
在数字时代的基石——经典计算中，信息由比特（bit）承载，其状态非0即1。然而，随着我们探索物质世界的更深层次，一个全新的计算[范式](@entry_id:161181)正在崛起：[量子计算](@entry_id:142712)。其基本[信息单位](@entry_id:262428)，即**[量子比特](@entry_id:137928)**（qubit），遵循着奇异而强大的量子力学法则，预示着一场信息处理能力的革命。[量子比特](@entry_id:137928)与经典比特的根本区别在于，它能够利用量子叠加和纠缠等现象，开启了解决特定复杂问题的可能性，这些问题对于当今最强大的超级计算机而言也遥不可及。

然而，从抽象的[量子理论](@entry_id:145435)到功能强大的量子设备，其中存在着巨大的知识鸿沟。一个[量子比特](@entry_id:137928)究竟是什么？它是如何被描述、操控和测量的？这些微观粒子的奇特性质如何转化为在计算、通信和传感领域的颠覆性应用？本文旨在系统性地回答这些问题，为读者铺设一条从基础原理到前沿应用的清晰路径。

在接下来的内容中，我们将分三个核心部分展开探索：
-   在 **“原理与机制”** 一章中，我们将深入[量子比特](@entry_id:137928)的数学心脏，揭示其[状态表示](@entry_id:141201)、叠加、测量、演化以及多比特系统中的纠缠等核心概念。
-   接着，在 **“应用与交叉学科联系”** 一章中，我们将把理论付诸实践，探讨[量子比特](@entry_id:137928)在[囚禁离子](@entry_id:171044)、超导电路等物理系统中的实现，并展示其在[量子算法](@entry_id:147346)、量子通信和精密测量等领域的强大应用。
-   最后，通过一系列 **“动手实践”**，您将有机会运用所学知识解决具体问题，加深对[量子比特](@entry_id:137928)操控与测量的理解。

让我们首先步入第一章，从量子信息的最小载体——[量子比特](@entry_id:137928)的定义与基本原理开始，正式开启我们的量子探索之旅。

## 原理与机制

在本章中，我们将深入探讨[量子计算](@entry_id:142712)的基本构成单元——[量子比特](@entry_id:137928)（qubit）的核心原理与机制。我们将从其数学描述出发，逐步揭示[量子叠加](@entry_id:137914)、测量、演化以及多比特系统中的纠缠等关键概念。这些原理不仅是量子力学的基石，也构成了[量子信息处理](@entry_id:158111)与计算的理论基础。

### [量子比特](@entry_id:137928)：量子信息的载体

经典计算机的基本单位是比特（bit），它只能处于 $0$ 或 $1$ 两种状态之一。与之相对，[量子计算](@entry_id:142712)的[基本单位](@entry_id:148878)是**[量子比特](@entry_id:137928)**（qubit），其[状态空间](@entry_id:177074)要丰富得多。一个[量子比特](@entry_id:137928)的状态由一个二维[复希尔伯特空间](@entry_id:185216)（$\mathbb{C}^2$）中的[单位向量](@entry_id:165907)来描述。

为了描述这个空间中的任意向量，我们需要一个**基底**（basis）。在[量子计算](@entry_id:142712)中，最常用的基底是**计算基底**，由两个正交的态向量 $|0\rangle$ 和 $|1\rangle$ 构成。在[矩阵表示](@entry_id:146025)中，它们通常写为：
$$
|0\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad |1\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}
$$
这两个[基向量](@entry_id:199546)类似于经典比特的两个状态。然而，[量子比特](@entry_id:137928)的真正威力在于它可以处于这两个[基态](@entry_id:150928)的**线性叠加**（linear superposition）中。一个[量子比特](@entry_id:137928)的普遍状态 $|\psi\rangle$ 可以写作：
$$
|\psi\rangle = \alpha|0\rangle + \beta|1\rangle
$$
其中，$\alpha$ 和 $\beta$ 是复数，被称为**概率振幅**（probability amplitudes）。为了确保概率的合理解释，这些振幅必须满足**[归一化条件](@entry_id:156486)**：
$$
|\alpha|^2 + |\beta|^2 = 1
$$
这个条件意味着状态向量 $|\psi\rangle$ 的范数（长度）为1。

[希尔伯特空间](@entry_id:261193)的二维性意味着任何一组由两个**线性无关**的向量构成的集合都可以作为其基底。例如，考虑集合 $S_D = \left\{ \begin{pmatrix} 1 \\ 1 \end{pmatrix}, \begin{pmatrix} 1 \\ -1 \end{pmatrix} \right\}$。我们可以通过计算由这两个向量构成的矩阵的行列式来检验它们的[线性无关](@entry_id:148207)性：
$$
\det \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix} = (1)(-1) - (1)(1) = -2 \neq 0
$$
由于[行列式](@entry_id:142978)不为零，这两个向量是线性无关的，因此它们可以构成 $\mathbb{C}^2$ 空间的一个有效基底。相比之下，一个只包含单个向量的集合无法张成整个二维空间，而一个包含三个或更多向量的集合在二维空间中必然是线性相关的 [@problem_id:1385934]。

### 量子测量与概率

[量子比特](@entry_id:137928)的叠加态在被**测量**（measurement）之前是不可知的。根据量子力学的基本公设，测量一个处于 $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$ 状态的[量子比特](@entry_id:137928)时，其状态会“坍缩”到计算基底的一个[基态](@entry_id:150928)上。

具体来说，测量结果为 $|0\rangle$ 的概率是 $|\alpha|^2$，测量结果为 $|1\rangle$ 的概率是 $|\beta|^2$。这就是著名的**[玻恩定则](@entry_id:154470)**（Born rule）。[归一化条件](@entry_id:156486)确保了总概率为 $1$。

[玻恩定则](@entry_id:154470)可以推广到对任意一组正交归一基底 $\{|m_1\rangle, |m_2\rangle\}$ 的测量。对于一个处于 $|\psi\rangle$ 态的[量子比特](@entry_id:137928)，测量得到结果 $|m_i\rangle$ 的概率 $P(m_i)$ 为：
$$
P(m_i) = |\langle m_i | \psi \rangle|^2
$$
这里的 $\langle m_i |$ 是 $|m_i\rangle$ 的[厄米共轭](@entry_id:191215)（即[转置](@entry_id:142115)共轭），称为“bra”向量，而 $\langle m_i | \psi \rangle$ 是两个态向量的[内积](@entry_id:158127)。

让我们通过一个实例来理解这一过程 [@problem_id:1385925]。假设一个[量子比特](@entry_id:137928)处于状态 $|\psi\rangle = \frac{1}{\sqrt{5}}|0\rangle + \frac{2}{\sqrt{5}}e^{i\pi/3}|1\rangle$，我们想知道测量得到状态 $|m\rangle = \frac{1}{\sqrt{2}}(|0\rangle - i|1\rangle)$ 的概率。

首先，我们计算[内积](@entry_id:158127) $\langle m | \psi \rangle$。$|m\rangle$ 对应的 bra 向量是 $\langle m| = \frac{1}{\sqrt{2}}(\langle 0| + i\langle 1|)$。
$$
\langle m | \psi \rangle = \left( \frac{1}{\sqrt{2}}(\langle 0| + i\langle 1|) \right) \left( \frac{1}{\sqrt{5}}|0\rangle + \frac{2}{\sqrt{5}}e^{i\pi/3}|1\rangle \right)
$$
利用基[向量的正交性](@entry_id:274719)（$\langle i|j \rangle = \delta_{ij}$），我们得到：
$$
\langle m | \psi \rangle = \frac{1}{\sqrt{10}} \left( 1 \cdot 1 + i \cdot 2e^{i\pi/3} \right) = \frac{1}{\sqrt{10}} (1 - \sqrt{3} + i)
$$
根据[玻恩定则](@entry_id:154470)，概率是这个复数[内积](@entry_id:158127)的模平方：
$$
P(m) = |\langle m | \psi \rangle|^2 = \frac{1}{10} \left| (1 - \sqrt{3}) + i \right|^2 = \frac{1}{10} \left( (1-\sqrt{3})^2 + 1^2 \right) = \frac{5 - 2\sqrt{3}}{10}
$$
这个计算过程体现了量子测量的核心数学框架：通过向量[内积](@entry_id:158127)计算概率振幅，再取其模平方得到概率。

### [量子比特](@entry_id:137928)的可视化与操控

#### [布洛赫球面](@entry_id:138823)

虽然[量子比特](@entry_id:137928)的状态由复数描述，但我们可以通过一个巧妙的几何工具——**[布洛赫球面](@entry_id:138823)**（Bloch sphere）——来直观地表示任意单个[量子比特](@entry_id:137928)的[纯态](@entry_id:141688)。任何归一化的单比特状态 $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$ 都可以（忽略一个[全局相位](@entry_id:147947)）被[参数化](@entry_id:272587)为：
$$
|\psi\rangle = \cos(\frac{\theta}{2})|0\rangle + e^{i\phi}\sin(\frac{\theta}{2})|1\rangle
$$
其中 $\theta \in [0, \pi]$ 是极角，$\phi \in [0, 2\pi)$ 是[方位角](@entry_id:164011)。这个状态可以映射到三维[单位球](@entry_id:142558)面上的一点，其[笛卡尔坐标](@entry_id:167698)为 $(\sin\theta\cos\phi, \sin\theta\sin\phi, \cos\theta)$。

在这个表示中：
-   $|0\rangle$ 态对应于北极点 ($\theta=0$)。
-   $|1\rangle$ 态对应于南极点 ($\theta=\pi$)。
-   所有赤道上的点代表 $|0\rangle$ 和 $|1\rangle$ 的等权重叠加态。例如，指向x轴正方向的点 ($\theta=\pi/2, \phi=0$) 对应于 $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle)$，而指向y轴负方向的点 ($\theta=\pi/2, \phi=3\pi/2$) 对应于状态 $|\psi\rangle = \frac{1}{\sqrt{2}}(|0\rangle - i|1\rangle)$ [@problem_id:2114319]。

[布洛赫球面](@entry_id:138823)为思考单比特操作提供了强大的直观工具，因为所有的单比特量子门操作都对应于球面上[状态向量](@entry_id:154607)的旋转。

#### 量子门

对[量子比特](@entry_id:137928)状态的操控是通过**量子门**（quantum gates）实现的，它们在数学上由**[酉矩阵](@entry_id:138978)**（unitary matrices）$U$ 表示。[酉矩阵](@entry_id:138978)的性质是 $U^\dagger U = UU^\dagger = I$（其中 $I$ 是[单位矩阵](@entry_id:156724)），这保证了[量子态](@entry_id:146142)在演化过程中始终保持归一化。当一个门 $U$ 作用于状态 $|\psi\rangle$ 时，新的状态是 $|\psi'\rangle = U|\psi\rangle$。

一些基本的单比特[量子门](@entry_id:143510)包括：
-   **泡利-X门 (Pauli-X gate)**：相当于[经典逻辑](@entry_id:264911)中的非门（NOT gate），$X = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$。它将 $|0\rangle$ 翻转为 $|1\rangle$，反之亦然。在[布洛赫球面](@entry_id:138823)上，它对应于围绕x轴旋转 $\pi$ 弧度。
-   **哈达玛门 (Hadamard gate)**：$H = \frac{1}{\sqrt{2}}\begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}$。它能创造叠加态，例如 $H|0\rangle = |+\rangle$ 和 $H|1\rangle = |-\rangle$。
-   **[相位门](@entry_id:143669) (Phase gate)**：$S = \begin{pmatrix} 1  0 \\ 0  i \end{pmatrix}$。它保持 $|0\rangle$ 不变，但给 $|1\rangle$ 增加一个 $i$ 的相位。

当多个量子门依次作用于一个[量子比特](@entry_id:137928)时，其总效果由这些门的矩阵乘积给出。重要的是，矩阵相乘的顺序[与门](@entry_id:166291)作用的时间顺序相反。例如，如果一个[量子比特](@entry_id:137928)先通过 $X$ 门，然后通过 $S$ 门，最后通过 $H$ 门，那么等效的单一[酉变换](@entry_id:152599) $U$ 是 $U = HSX$ [@problem_id:2114338]。

在实验中，我们可以通过控制[量子门](@entry_id:143510)的参数并测量最终状态的[概率分布](@entry_id:146404)来反推系统的未知属性。例如，通过施加一个哈达玛门和一个相位可变的[相位门](@entry_id:143669) $P(\phi) = \begin{pmatrix} 1  0 \\ 0  e^{i\phi} \end{pmatrix}$，并测量最终在 $|+\rangle$ 态上的概率，我们可以根据测量结果反解出相位角 $\phi$ 的值 [@problem_id:2114314]。

### [可观测量](@entry_id:267133)与[期望值](@entry_id:153208)

在量子力学中，可测量的物理量，如自旋、能量或位置，被称为**[可观测量](@entry_id:267133)**（observables），并由**[厄米算符](@entry_id:153410)**（Hermitian operators）表示。[厄米算符](@entry_id:153410)的性质是 $A^\dagger = A$。

[可观测量](@entry_id:267133)的**本征态**（eigenstates）和**[本征值](@entry_id:154894)**（eigenvalues）具有特殊的物理意义。如果一个系统处于某个可观测量 $A$ 的本征态 $|\lambda\rangle$ 上，满足 $A|\lambda\rangle = \lambda|\lambda\rangle$，那么对该系统测量 $A$ 将以 $100\%$ 的概率得到其对应的[本征值](@entry_id:154894) $\lambda$。

对于一个处于任意状态 $|\psi\rangle$ 的系统，对可观测量 $A$ 进行单次测量的结果是其[本征值](@entry_id:154894)之一，但如果我们对大量相同制备的系统进行测量，所得到结果的平均值被称为**[期望值](@entry_id:153208)**（expectation value），记作 $\langle A \rangle$。其计算公式为：
$$
\langle A \rangle = \langle \psi | A | \psi \rangle
$$
让我们考虑一个由泡利矩阵 $\sigma_x$ 和 $\sigma_z$ 构成的[可观测量](@entry_id:267133) $S_\theta = \cos\theta \sigma_z + \sin\theta \sigma_x$ [@problem_id:2114335]。假设系统被制备在 $S_\alpha$ 的一个[本征值](@entry_id:154894)为 $+1$ 的[本征态](@entry_id:149904) $|\psi_\alpha\rangle$ 上，然后我们测量另一个可观测量 $S_\beta$。该测量的[期望值](@entry_id:153208) $\langle S_\beta \rangle$ 是多少？

通过求解本征方程，可以发现 $S_\alpha$ 对应于[本征值](@entry_id:154894) $+1$ 的本征态是 $|\psi_\alpha\rangle = \cos(\alpha/2)|0\rangle + \sin(\alpha/2)|1\rangle$。然后，我们计算[期望值](@entry_id:153208)：
$$
\langle S_\beta \rangle = \langle \psi_\alpha | S_\beta | \psi_\alpha \rangle = \langle \psi_\alpha | (\cos\beta \sigma_z + \sin\beta \sigma_x) | \psi_\alpha \rangle
$$
经过一番代数运算，我们得到一个非常简洁和深刻的结果：
$$
\langle S_\beta \rangle = \cos\alpha \cos\beta + \sin\alpha \sin\beta = \cos(\alpha - \beta)
$$
这个结果在[布洛赫球面](@entry_id:138823)上有一个优美的几何解释：[期望值](@entry_id:153208)等于两个[可观测量](@entry_id:267133)对应方向之间的夹角的余弦。这也暗示了一个重要的事实：由于 $\sigma_x$ 和 $\sigma_z$ 不对易（即 $\sigma_x \sigma_z \neq \sigma_z \sigma_x$），一个[量子态](@entry_id:146142)无法同时是它们两者的确定[本征态](@entry_id:149904)，这构成了[量子不确定性](@entry_id:156130)原理的一个例子。

### [多量子比特系统](@entry_id:142942)与[量子纠缠](@entry_id:136576)

当系统包含多个[量子比特](@entry_id:137928)时，其状态空间是各个子系统[希尔伯特空间](@entry_id:261193)的**张量积**（tensor product）。例如，一个双比特系统的状态空间是 $\mathbb{C}^2 \otimes \mathbb{C}^2$，这是一个四维空间 $\mathbb{C}^4$。其计算基底由四个状态构成：$|00\rangle, |01\rangle, |10\rangle, |11\rangle$，其中 $|ab\rangle$ 是 $|a\rangle \otimes |b\rangle$ 的简写。

-   **可分离态 (Separable States)**：如果一个多比特系统的状态可以写成其各个子系统状态的张量积，例如 $|\Psi\rangle = |\psi_A\rangle \otimes |\psi_B\rangle$，那么这个状态是可分离的。这类状态中的[量子比特](@entry_id:137928)之间没有[量子关联](@entry_id:136327)。

-   **[纠缠态](@entry_id:152310) (Entangled States)**：任何不可分离的态都称为**纠缠态**。纠缠是量子力学最奇特、也最强大的特性之一。处于[纠缠态](@entry_id:152310)的两个或多个[量子比特](@entry_id:137928)，无论相隔多远，它们的状态都是内在关联的。

最著名的纠缠态是**[贝尔态](@entry_id:140749)**（Bell states），例如：
$$
|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)
$$
$$
|\Psi^-\rangle = \frac{1}{\sqrt{2}}(|01\rangle - |10\rangle)
$$
这些状态无法被分解为两个单比特状态的[张量积](@entry_id:140694)。对于一个纯的双比特态 $|\Psi\rangle = c_{00}|00\rangle + c_{01}|01\rangle + c_{10}|10\rangle + c_{11}|11\rangle$，一个判断其是否可分离的必要条件是 $c_{00}c_{11} - c_{01}c_{10} = 0$。对于[贝尔态](@entry_id:140749) $|\Psi^-\rangle$，我们有 $c_{01}=1/\sqrt{2}, c_{10}=-1/\sqrt{2}$，而其他系数为零，因此 $c_{00}c_{11} - c_{01}c_{10} = 0 - (1/\sqrt{2})(-1/\sqrt{2}) = 1/2 \neq 0$，表明它是纠缠的 [@problem_id:1385930]。

纠缠的深刻含义在于对其中一个[量子比特](@entry_id:137928)的测量会瞬间影响到另一个[量子比特](@entry_id:137928)的状态。考虑处于[贝尔态](@entry_id:140749) $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$ 的两个[量子比特](@entry_id:137928)。如果我们测量第一个[量子比特](@entry_id:137928)并得到结果 $|0\rangle$，整个系统的状态会立即坍缩到 $|00\rangle$，这意味着第二个[量子比特](@entry_id:137928)的状态必然是 $|0\rangle$。这种超越空间的关联性，即爱因斯坦所说的“[鬼魅般的超距作用](@entry_id:143486)”，是[量子信息处理](@entry_id:158111)中许多强大应用（如[量子隐形传态](@entry_id:144485)和[超密编码](@entry_id:137220)）的基础 [@problem_id:2114315]。

### 基本原理与局限性

#### [不可克隆定理](@entry_id:146200)

量子力学的一个基本限制是**[不可克隆定理](@entry_id:146200)**（No-Cloning Theorem），它指出不可能创建一个设备，能够完美复制一个任意未知的[量子态](@entry_id:146142)。

我们可以通过一个思想实验来证明这一点 [@problem_id:2114322]。假设存在一个通用的克隆门 $U_{clone}$，可以将任意态 $|\psi\rangle$ 和一个初始态为 $|0\rangle$ 的辅助比特转换为两个 $|\psi\rangle$ 的副本：$U_{clone}(|\psi\rangle \otimes |0\rangle) = |\psi\rangle \otimes |\psi\rangle$。

[量子演化](@entry_id:198246)必须是酉的，而[酉变换](@entry_id:152599)保持[内积](@entry_id:158127)不变。考虑两个不同的初始态 $|I_A\rangle = |\psi_A\rangle \otimes |0\rangle$ 和 $|I_B\rangle = |\psi_B\rangle \otimes |0\rangle$。它们的[内积](@entry_id:158127)是 $\langle I_A | I_B \rangle = \langle \psi_A | \psi_B \rangle$。
经过克隆门后，末态分别是 $|F_A\rangle = |\psi_A\rangle \otimes |\psi_A\rangle$ 和 $|F_B\rangle = |\psi_B\rangle \otimes |\psi_B\rangle$。它们的[内积](@entry_id:158127)是 $\langle F_A | F_B \rangle = \langle \psi_A | \psi_B \rangle \langle \psi_A | \psi_B \rangle = (\langle \psi_A | \psi_B \rangle)^2$。

如果 $U_{clone}$ 是酉的，那么必须有 $|\langle I_A | I_B \rangle|^2 = |\langle F_A | F_B \rangle|^2$，这意味着 $|\langle \psi_A | \psi_B \rangle|^2 = |\langle \psi_A | \psi_B \rangle|^4$。这个方程只在 $|\langle \psi_A | \psi_B \rangle|$ 为 $0$ 或 $1$ 时成立，即当两个态是正交的或完全相同时。但对于任意非正交、非相同的态，这个等式不成立。因此，一个能克隆任意态的普适[酉变换](@entry_id:152599)是不存在的。这一定理深刻地揭示了量子信息与经典信息的根本区别。

#### 真实世界中的[量子态](@entry_id:146142)：退相干

到目前为止，我们讨论的都是[孤立系统](@entry_id:159201)中的[纯态](@entry_id:141688)和[酉演化](@entry_id:145020)。然而，在现实世界中，任何量子系统都不可避免地与其环境发生相互作用。这种相互作用会导致[量子态](@entry_id:146142)的**退相干**（decoherence），这是实现可靠[量子计算](@entry_id:142712)的主要障碍。

为了描述这种[开放量子系统](@entry_id:138632)，我们需要使用**密度矩阵**（density matrix）$\rho$ 的形式化语言。对于[纯态](@entry_id:141688) $|\psi\rangle$，[密度矩阵](@entry_id:139892)定义为 $\rho = |\psi\rangle\langle\psi|$。而对于一个可能处于多个纯态 $|\psi_i\rangle$（概率为 $p_i$）的[统计系综](@entry_id:149738)，其状态是**[混合态](@entry_id:141568)**（mixed state），[密度矩阵](@entry_id:139892)为 $\rho = \sum_i p_i |\psi_i\rangle\langle\psi_i|$。

与环境的相互作用（噪声）通常不是[酉演化](@entry_id:145020)，而是通过一个更广义的映射——**[量子操作](@entry_id:145906)**或**量子通道**——来描述。一个常用的描述方法是**[克劳斯算符和表示](@entry_id:146609)**（Kraus operator-sum representation），其中末态[密度矩阵](@entry_id:139892) $\rho_{\text{final}}$ 由初态 $\rho_{\text{initial}}$ 给出：
$$
\rho_{\text{final}} = \mathcal{E}(\rho_{\text{initial}}) = \sum_k E_k \rho_{\text{initial}} E_k^\dagger
$$
其中 $E_k$ 是[克劳斯算符](@entry_id:144882)，满足[完备性关系](@entry_id:139077) $\sum_k E_k^\dagger E_k = I$。

一个典型的例子是**[相位阻尼](@entry_id:147888)通道**（phase-damping channel），它描述了[量子比特](@entry_id:137928)因与环境相互作用而损失其相位信息的过程 [@problem_id:2114303]。对于一个初始处于 $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle)$ 态的[量子比特](@entry_id:137928)，其初始密度矩阵为 $\rho_{\text{initial}} = \frac{1}{2}\begin{pmatrix} 1  1 \\ 1  1 \end{pmatrix}$。经过一个由[克劳斯算符](@entry_id:144882) $E_0 = \begin{pmatrix} 1  0 \\ 0  \sqrt{1-p} \end{pmatrix}$ 和 $E_1 = \begin{pmatrix} 0  0 \\ 0  \sqrt{p} \end{pmatrix}$ 描述的[相位阻尼](@entry_id:147888)通道后，最终的密度矩阵变为：
$$
\rho_{\text{final}} = \frac{1}{2}\begin{pmatrix} 1  \sqrt{1-p} \\ \sqrt{1-p}  1 \end{pmatrix}
$$
我们可以看到，[密度矩阵](@entry_id:139892)的对角元素（布居数）保持不变，但非对角元素（相干项）被一个因子 $\sqrt{1-p}$ 所抑制。当[退相干](@entry_id:145157)强度 $p$ 增加时，相干项趋于零，量子叠加的特性逐渐消失，系统行为越来越趋向于经典。理解和对抗[退相干](@entry_id:145157)是[量子技术](@entry_id:142946)走向实用的核心挑战。