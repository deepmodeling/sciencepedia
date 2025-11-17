## 引言
[量子计算](@entry_id:142712)代表了信息处理领域的一场革命，它承诺利用[亚原子粒子](@entry_id:142492)奇异的物理行为来解决当今最强大的超级计算机也无法企及的问题。与依赖于明确的0或1状态的经典计算不同，[量子计算](@entry_id:142712)进入了一个由叠加和纠缠主导的概率性领域，开启了计算能力呈指数级增长的可能性。然而，驾驭这种力量需要我们采用一套全新的语言和思维方式，这正是经典计算机在模拟复杂量子系统或破解[现代密码学](@entry_id:274529)等任务上遇到瓶颈的根本原因。本文旨在为您揭开[量子计算](@entry_id:142712)的神秘面纱，系统地引导您掌握其核心概念。

本文将分为三个核心部分。在“原理与机制”中，我们将深入量子世界的基本构件，学习[量子比特](@entry_id:137928)、量子门和测量的数学语言。接着，在“应用与跨学科联系”中，我们将探索这些原理如何转化为强大的[量子算法](@entry_id:147346)（如Grover搜索）和通信协议（如[量子隐形传态](@entry_id:144485)），并揭示其与物理、化学、金融等领域的深刻联系。最后，在“动手实践”部分，您将有机会通过解决具体问题来巩固所学知识。

我们的探索之旅将从构建[量子计算](@entry_id:142712)的理论基石开始。要理解并最终利用[量子计算](@entry_id:142712)机的巨大潜力，我们必须首先掌握支配其行为的基本原理。

## 原理与机制

继前一章对[量子计算](@entry_id:142712)的基本背景和前景进行介绍之后，本章将深入探讨其数学和物理基础。我们将从单个[量子比特](@entry_id:137928)的表示法开始，逐步构建起描述[量子演化](@entry_id:198246)、测量以及多体系统的理论框架。这些原理和机制是理解[量子算法](@entry_id:147346)和[量子技术](@entry_id:142946)威力的核心。

### 量子系统的状态：[量子比特](@entry_id:137928)

经典计算机的基本单位是比特，它只能处于 $0$ 或 $1$ 两种状态之一。而[量子计算](@entry_id:142712)的[基本单位](@entry_id:148878)是**[量子比特](@entry_id:137928) (qubit)**，它的[状态空间](@entry_id:177074)要广阔得多。

#### [状态向量](@entry_id:154607)

从数学上看，一个[量子比特](@entry_id:137928)的状态由一个二维[复向量空间](@entry_id:264355) $\mathbb{C}^2$ 中的单位向量来描述。这个向量被称为**[状态向量](@entry_id:154607)**。我们选取一组标准正交基，称为**计算[基态](@entry_id:150928) (computational basis states)**，记作 $|0\rangle$ 和 $|1\rangle$。它们对应于经典比特的两个状态，并用列[向量表示](@entry_id:166424)为：
$$
|0\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad |1\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}
$$
与经典比特不同，[量子比特](@entry_id:137928)可以处于这两个[基态](@entry_id:150928)的**叠加 (superposition)** 状态。一个任意的单[量子比特](@entry_id:137928)纯态 $|\psi\rangle$ 都可以写成这两个[基态](@entry_id:150928)的[线性组合](@entry_id:154743)：
$$
|\psi\rangle = \alpha |0\rangle + \beta |1\rangle
$$
这里的系数 $\alpha$ 和 $\beta$ 是复数，被称为**概率幅 (probability amplitudes)**。

#### 归一化与概率幅

状态向量的一个核心要求是它必须是[单位向量](@entry_id:165907)，即其范数为 $1$。这意味着[概率幅](@entry_id:150609)必须满足**[归一化条件](@entry_id:156486)**：
$$
|\alpha|^2 + |\beta|^2 = 1
$$
这个条件源于量子测量的概率解释，我们稍后会详细讨论。简而言之，$|\alpha|^2$ 是在测量时发现[量子比特](@entry_id:137928)处于 $|0\rangle$ 态的概率，$|\beta|^2$ 则是发现其处于 $|1\rangle$ 态的概率。这两个[互斥事件](@entry_id:265118)的概率之和必须为 $1$。

#### [布洛赫球面](@entry_id:138823)表示

尽管状态向量在二维复空间 $\mathbb{C}^2$ 中，它实际上只有两个实数自由度（两个复数有四个实数参数，但[归一化条件](@entry_id:156486)和[全局相位](@entry_id:147947)无关性各减少一个自由度）。这使得我们可以将任意单[量子比特](@entry_id:137928)纯态 $|\psi\rangle$ 几何化地表示在一个三维单位球面上，这个球面被称为**[布洛赫球面](@entry_id:138823) (Bloch sphere)**。

状态向量 $|\psi\rangle = \alpha |0\rangle + \beta |1\rangle$ 可以用两个角度 $\theta$ 和 $\phi$ 来参数化：
$$
|\psi\rangle = \cos\left(\frac{\theta}{2}\right)|0\rangle + \exp(i\phi)\sin\left(\frac{\theta}{2}\right)|1\rangle
$$
其中 $0 \le \theta \le \pi$ 是极角，$0 \le \phi  2\pi$ 是方位角。例如，北极点 ($\theta=0$) 对应 $|0\rangle$ 态，南极点 ($\theta=\pi$) 对应 $|1\rangle$ 态。所有其他的叠加态则[分布](@entry_id:182848)在球面上。举例来说，一个由角度 $\theta = \frac{\pi}{3}$ 和 $\phi = \frac{\pi}{2}$ 描述的[量子比特](@entry_id:137928) [@problem_id:2098725]，其状态向量为：
$$
|\psi\rangle = \cos\left(\frac{\pi}{6}\right)|0\rangle + \exp\left(i\frac{\pi}{2}\right)\sin\left(\frac{\pi}{6}\right)|1\rangle = \frac{\sqrt{3}}{2}|0\rangle + \frac{i}{2}|1\rangle
$$
这个状态在[向量表示](@entry_id:166424)中为 $\begin{pmatrix} \frac{\sqrt{3}}{2} \\ \frac{i}{2} \end{pmatrix}$。[布洛赫球面](@entry_id:138823)为我们提供了一个直观理解单[量子比特](@entry_id:137928)状态及其变换的有力工具。

### [量子测量](@entry_id:272490)：提取信息

[量子态](@entry_id:146142)本身是无法直接观测的。我们能从量子系统中提取信息的唯一方式就是通过**测量 (measurement)**。然而，[量子测量](@entry_id:272490)有着与经典测量截然不同的特性。

#### [玻恩定则](@entry_id:154470)

量子力学的核心公设之一是**[玻恩定则](@entry_id:154470) (Born rule)**，它将[状态向量](@entry_id:154607)的数学描述与可观测的实验结果联系起来。该定则指出，当对处于状态 $|\psi\rangle$ 的系统进行测量，以确定它是否处于另一个状态 $|\phi\rangle$ 时，得到肯定结果的概率 $P(\phi)$ 等于两个状态向量[内积](@entry_id:158127)的模平方：
$$
P(\phi) = |\langle \phi | \psi \rangle|^2
$$
这里的 $\langle \phi |$ 是 $|\phi\rangle$ 的[共轭转置](@entry_id:147909)，称为“bra”向量。例如，对于一个处于任意状态 $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$ 的[量子比特](@entry_id:137928)，其被测量到处于 $|0\rangle$ 态的概率是 $P(0) = |\langle 0 | \psi \rangle|^2 = |\alpha|^2$，测量到处于 $|1\rangle$ 态的概率是 $P(1) = |\langle 1 | \psi \rangle|^2 = |\beta|^2$。这与我们之前提到的[归一化条件](@entry_id:156486)相吻合。

#### 不同基下的测量

测量并不局限于计算基。我们可以在任何一组[正交基](@entry_id:264024)下进行测量。一个重要的例子是**哈达玛基 (Hadamard basis)**，由以下两个状态构成：
$$
|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle), \quad |-\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)
$$
假设一个[量子比特](@entry_id:137928)被制备在状态 $|\psi\rangle = \frac{3}{5}|0\rangle + \frac{4}{5}|1\rangle$ [@problem_id:1368624]。要在哈达玛基下测量它，我们需要计算其与 $|+\rangle$ 和 $|-\rangle$ 的[内积](@entry_id:158127)。例如，测量到 $|+\rangle$ 态的概率为：
$$
P(+) = |\langle + | \psi \rangle|^2 = \left| \left( \frac{1}{\sqrt{2}}(\langle 0| + \langle 1|) \right) \left( \frac{3}{5}|0\rangle + \frac{4}{5}|1\rangle \right) \right|^2
$$
利用[基态](@entry_id:150928)的正交性 $\langle i|j \rangle = \delta_{ij}$，我们得到：
$$
P(+) = \left| \frac{1}{\sqrt{2}}\left(\frac{3}{5} + \frac{4}{5}\right) \right|^2 = \left| \frac{7}{5\sqrt{2}} \right|^2 = \frac{49}{50}
$$
这意味着，尽管该状态在计算基下有明确的[概率分布](@entry_id:146404)（$P(0)=\frac{9}{25}, P(1)=\frac{16}{25}$），但在哈达玛基下它有着完全不同的[概率分布](@entry_id:146404)。

通过在不同基下对大量全同制备的[量子比特](@entry_id:137928)进行测量，我们可以反推出[量子态](@entry_id:146142)的概率幅，这一过程称为**[量子态](@entry_id:146142)层析 (quantum state tomography)**。例如，通过结合在计算基、哈达玛基和另一个称为“圆极化基”下的测量概率，可以唯一确定一个[量子比特](@entry_id:137928)的[状态向量](@entry_id:154607)，包括其[复数相位](@entry_id:173474) [@problem_id:1368619]。

一个关键的推论是，测量行为是具有破坏性的。在测量之后，[量子态](@entry_id:146142)会**坍缩 (collapse)** 到测量结果所对应的[本征态](@entry_id:149904)上。例如，如果对状态 $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$ 进行计算基测量并得到结果 $0$，那么测量后该[量子比特](@entry_id:137928)的状态就变成了 $|0\rangle$。原始的叠加信息就丢失了。

### [量子演化](@entry_id:198246)：门和算子

如果不对[量子比特](@entry_id:137928)进行测量，其状态会如何随时间演化？根据量子力学，一个封闭量子系统的演化由一个**[酉算子](@entry_id:151194) (unitary operator)** $U$ 描述。如果系统初始状态为 $|\psi\rangle$，演化后的状态为 $|\psi'\rangle = U|\psi\rangle$。

#### 酉性作为核心原则

在矩阵表示中，[量子演化](@entry_id:198246)由**酉矩阵 (unitary matrix)** 描述。一个矩阵 $U$ 是酉矩阵，如果其共轭转置 $U^\dagger$ 等于其[逆矩阵](@entry_id:140380)，即：
$$
U^\dagger U = U U^\dagger = I
$$
其中 $I$ 是[单位矩阵](@entry_id:156724)。[酉变换](@entry_id:152599)的一个重要性质是它保持[向量的范数](@entry_id:154882)（长度）不变。对于任意状态 $|\psi\rangle$，演化后状态的范数 $\| |\psi'\rangle \| = \| U|\psi\rangle \| = \sqrt{\langle\psi|U^\dagger U|\psi\rangle} = \sqrt{\langle\psi|\psi\rangle} = \| |\psi\rangle \| = 1$。这保证了[量子态](@entry_id:146142)在演化后仍然是归一化的，从而保证了总[概率守恒](@entry_id:149166)。这个要求是物理实在性的基本体现。

因此，任何一个合法的[量子操作](@entry_id:145906)或“门”都必须由一个[酉矩阵](@entry_id:138978)来表示。例如，考虑一个由参数 $\beta$ 决定的矩阵 $G$ [@problem_id:1368617]：
$$
G = \frac{1}{2} \begin{pmatrix} 1+i  \beta \\ \sqrt{2}  1-i \end{pmatrix}
$$
为了使 $G$ 成为一个合法的[量子门](@entry_id:143510)，它必须是[酉矩阵](@entry_id:138978)。[酉矩阵](@entry_id:138978)的列向量必须构成一组[标准正交基](@entry_id:147779)。通过强制要求其列向量相互正交且范数为1，可以解出未知参数 $\beta$ 的值。计算表明，只有当 $\beta = -\sqrt{2}$ 时，该矩阵才满足酉性条件。

#### [单量子比特门](@entry_id:146489)

[单量子比特门](@entry_id:146489)是对单个[量子比特](@entry_id:137928)进行操作的[酉变换](@entry_id:152599)，由 $2 \times 2$ 的酉矩阵表示。一些常见的例子包括：
- **泡利-X门 (Pauli-X gate)**，相当于经典计算中的NO[T门](@entry_id:138474)：$X = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$。
- **泡利-Z门 (Pauli-Z gate)**，它给 $|1\rangle$ 态引入一个相位翻转：$Z = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$。
- **哈达玛门 (Hadamard gate)**，它创造和消除叠加态：$H = \frac{1}{\sqrt{2}}\begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}$。它将 $|0\rangle$ 变为 $|+\rangle$，将 $|1\rangle$ 变为 $|-\rangle$。

#### 门的组合

一系列[量子门](@entry_id:143510)相继作用于一个量子系统，其总效果由这些门矩阵的乘积来描述。一个重要的规则是，矩阵相乘的顺序与门作用的顺序相反。如果门 $G_1, G_2, G_3$ 依次作用在一个状态上，那么总的变换算子是 $U_{total} = G_3 G_2 G_1$。

例如，考虑一个操作序列：首先是哈达玛门 $H$，然后是一个[参数化](@entry_id:272587)的旋转门 $D(\theta)$，最后是泡利-Z门 $Z$ [@problem_id:1368599]。代表整个序列的单一矩阵 $U_{total}$ 就是这三个矩阵的乘积：
$$
U_{total} = Z \cdot D(\theta) \cdot H
$$
通过执行矩阵乘法，我们可以得到一个单独的 $2 \times 2$ 矩阵，它等效于这三个门顺序作用的净效应。这种将复杂操作序列合成为单个[酉矩阵](@entry_id:138978)的能力，是量子算法设计和分析的基础。

### [多量子比特系统](@entry_id:142942)与纠缠

现实中的[量子计算](@entry_id:142712)机需要处理多个[量子比特](@entry_id:137928)。描述多体系统的数学语言是**[张量积](@entry_id:140694) (tensor product)**。

#### [张量积](@entry_id:140694)

一个由 $n$ 个[量子比特](@entry_id:137928)组成的系统，其状态空间是 $n$ 个 $\mathbb{C}^2$ 空间的[张量积](@entry_id:140694)，即 $\mathbb{C}^2 \otimes \mathbb{C}^2 \otimes \dots \otimes \mathbb{C}^2$，这是一个 $2^n$ 维的[复向量空间](@entry_id:264355)。

例如，一个[双量子比特系统](@entry_id:203437)的计算[基态](@entry_id:150928)由两个单[量子比特](@entry_id:137928)[基态](@entry_id:150928)的[张量积](@entry_id:140694)构成：
$|00\rangle = |0\rangle \otimes |0\rangle$, $|01\rangle = |0\rangle \otimes |1\rangle$, $|10\rangle = |1\rangle \otimes |0\rangle$, $|11\rangle = |1\rangle \otimes |1\rangle$。
一个任意的双[量子比特](@entry_id:137928)态是这四个[基态](@entry_id:150928)的线性组合：
$$
|\psi\rangle = \alpha|00\rangle + \beta|01\rangle + \gamma|10\rangle + \delta|11\rangle
$$
其中 $|\alpha|^2 + |\beta|^2 + |\gamma|^2 + |\delta|^2 = 1$。

#### [多量子比特门](@entry_id:139015)

作用于多个[量子比特](@entry_id:137928)的门由 $2^n \times 2^n$ 的酉[矩阵表示](@entry_id:146025)。最重要的[多量子比特门](@entry_id:139015)之一是**[受控非门](@entry_id:180955) (Controlled-NOT, CNOT)**，这是一个双[量子比特](@entry_id:137928)门。它有一个控制[量子比特](@entry_id:137928)和一个目标[量子比特](@entry_id:137928)。如果控制位是 $|1\rangle$，它就翻转目标位（施加一个X门）；如果控制位是 $|0\rangle$，它什么也不做。

一个更复杂的例子是**受控-受控-[非门](@entry_id:169439) (CCNOT or Toffoli gate)**，这是一个[三量子比特](@entry_id:146257)门 [@problem_id:1368601]。它有两个控制位和一个目标位。只有当两个控制位都处于 $|1\rangle$ 态时，目标位才会被翻转。这个门在 $8 \times 8$ 的希尔伯特空间中作用，其矩阵表示在一个按[字典序](@entry_id:143032)[排列](@entry_id:136432)的基 $\{|000\rangle, |001\rangle, \dots, |111\rangle\}$ 中，大部分是对角元为1的[单位矩阵](@entry_id:156724)，只在对应于 $|110\rangle$ 和 $|111\rangle$ 的[子空间](@entry_id:150286)中表现为一个X门，即交换这两个[基向量](@entry_id:199546)。

#### 纠缠：量子关联

在[多量子比特系统](@entry_id:142942)中，会出现一种纯粹的量子现象，即**量子纠缠 (quantum entanglement)**。

一个多[量子比特](@entry_id:137928)态如果可以被写成其各个子系统（单个[量子比特](@entry_id:137928)）状态的张量积，则称该状态为**可分离态 (separable state)** 或乘积态。例如，$|\psi\rangle = |\phi_A\rangle \otimes |\phi_B\rangle$。这样的状态中，对一个[量子比特](@entry_id:137928)的测量不会影响另一个[量子比特](@entry_id:137928)的测量结果。

然而，许多状态无法这样分解，这些状态被称为**纠缠态 (entangled states)**。对于一个一般的双[量子比特](@entry_id:137928)态 $|\psi\rangle = \alpha|00\rangle + \beta|01\rangle + \gamma|10\rangle + \delta|11\rangle$，它是可分离的当且仅当其系数满足条件 [@problem_id:1368621]：
$$
\alpha\delta = \beta\gamma
$$
如果 $\alpha\delta \neq \beta\gamma$，则该状态是纠缠的。例如，状态 $|\psi_B\rangle = \frac{1}{\sqrt{3}} ( |00\rangle + |01\rangle + |10\rangle )$ 的系数为 $\alpha=1/\sqrt{3}, \beta=1/\sqrt{3}, \gamma=1/\sqrt{3}, \delta=0$。这里 $\alpha\delta=0$ 而 $\beta\gamma=1/3$，因此该状态是纠缠的。

最著名的[纠缠态](@entry_id:152310)之一是贝尔态 $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$。在这个状态中，对第一个[量子比特](@entry_id:137928)的测量结果会瞬间决定第二个[量子比特](@entry_id:137928)的测量结果，无论它们相隔多远。例如，如果第一个测得为 $|0\rangle$，第二个必然是 $|0\rangle$；如果第一个是 $|1\rangle$，第二个必然是 $|1\rangle$。这种“幽灵般的[超距作用](@entry_id:264202)”（爱因斯坦语）是量子力学最深刻和反直觉的特征之一，也是[量子计算](@entry_id:142712)和[量子通信](@entry_id:138989)的关键资源。

### 高级原理与“禁令”定理

量子力学的[酉性](@entry_id:138773)和线性结构导致了一些深刻的限制性原理，它们规定了哪些事情在量子世界中是“不可能”完成的。

#### [不可克隆定理](@entry_id:146200)

一个最著名的结果是**[不可克隆定理](@entry_id:146200) (no-cloning theorem)**，它指出我们不可能创造一个完美的、通用的设备来复制一个任意未知的[量子态](@entry_id:146142)。

我们可以通过反证法来理解这一点 [@problem_id:1368640]。假设存在一个通用的[量子克隆](@entry_id:138347)机，它由一个[酉算子](@entry_id:151194) $U$ 描述。这个机器取一个待克隆的状态 $|\psi\rangle$ 和一个处于“空白”状态（如 $|0\rangle$）的[辅助量子比特](@entry_id:144604)作为输入，输出两个都处于 $|\psi\rangle$ 状态的[量子比特](@entry_id:137928)。其操作可以写成：
$$
U (|\psi\rangle \otimes |0\rangle) = |\psi\rangle \otimes |\psi\rangle
$$
现在，考虑用两个不同的非正交状态 $|\psi_A\rangle$ 和 $|\psi_B\rangle$ 来测试这个克隆机。根据假设，我们有：
$U (|\psi_A\rangle \otimes |0\rangle) = |\psi_A\rangle \otimes |\psi_A\rangle$
$U (|\psi_B\rangle \otimes |0\rangle) = |\psi_B\rangle \otimes |\psi_B\rangle$

由于 $U$ 是[酉算子](@entry_id:151194)，它必须保持任意两个状态向量的[内积](@entry_id:158127)不变。因此，输入态的[内积](@entry_id:158127)必须等于输出态的[内积](@entry_id:158127)。
输入态的[内积](@entry_id:158127)是：
$$
\langle \text{in}_A | \text{in}_B \rangle = (\langle\psi_A| \otimes \langle 0|) (|\psi_B\rangle \otimes |0\rangle) = \langle\psi_A|\psi_B\rangle \langle 0|0\rangle = \langle\psi_A|\psi_B\rangle
$$
输出态的[内积](@entry_id:158127)是：
$$
\langle \text{out}_A | \text{out}_B \rangle = (\langle\psi_A| \otimes \langle\psi_A|) (|\psi_B\rangle \otimes |\psi_B\rangle) = \langle\psi_A|\psi_B\rangle \langle\psi_A|\psi_B\rangle = (\langle\psi_A|\psi_B\rangle)^2
$$
要使[内积](@entry_id:158127)保持不变，必须有 $\langle\psi_A|\psi_B\rangle = (\langle\psi_A|\psi_B\rangle)^2$。这个方程只有在 $\langle\psi_A|\psi_B\rangle = 0$（状态正交）或 $\langle\psi_A|\psi_B\rangle = 1$（状态相同）时才成立。因此，不存在一个能够克隆任意非正交状态的通用[酉算子](@entry_id:151194)。这一定理对[量子密码学](@entry_id:144827)和量子纠错具有深远的影响。

#### 可区分性的极限

[不可克隆定理](@entry_id:146200)与另一个密切相关的事实有关：非正交的[量子态](@entry_id:146142)无法通过任何单次测量被完美地区分。

考虑一个情景，发送者Alice以等概率发送两个状态中的一个：$|\psi_A\rangle = |0\rangle$ 或 $|\psi_B\rangle = \cos(\alpha)|0\rangle + \sin(\alpha)|1\rangle$，其中 $0  \alpha  \pi/2$ [@problem_id:1368666]。接收者Bob的目标是通过一次测量来确定收到的是哪个状态。Bob能做的最好的事情是设计一个测量，使得他猜错的平均概率最小。可以证明，这个最小的平均错误概率（也称为 Helstrom 界）为：
$$
P_{\text{err}}^{\min} = \frac{1}{2} \left( 1 - \sqrt{1 - |\langle\psi_A|\psi_B\rangle|^2} \right)
$$
在这个例子中，$\langle\psi_A|\psi_B\rangle = \cos(\alpha)$，所以最小[错误概率](@entry_id:267618)为 $\frac{1-\sin(\alpha)}{2}$。只要 $\alpha \neq \pi/2$（即只要两个状态不正交），这个[错误概率](@entry_id:267618)就严格大于零。只有当状态相互正交时，才能被完美地区分。

### 开放系统与混合态

到目前为止，我们主要讨论的是与外界完全隔离的“封闭”量子系统，它们的状态由[纯态](@entry_id:141688)向量 $|\psi\rangle$ 描述。然而，在现实世界中，任何量子系统都不可避免地会与环境发生相互作用，这种相互作用被称为**[退相干](@entry_id:145157) (decoherence)**。为了描述这些更现实的“开放”系统，我们需要引入更广义的工具。

#### [密度矩阵](@entry_id:139892)

描述一个量子系统最通用的方式是使用**密度矩阵 (density matrix)** 或[密度算符](@entry_id:138151)，通常记作 $\rho$。对于一个处于纯态 $|\psi\rangle$ 的系统，其密度矩阵是 $\rho = |\psi\rangle\langle\psi|$。

一个系统如果可能以概率 $p_i$ 处于纯态 $|\psi_i\rangle$，那么它的状态是一个**混合态 (mixed state)**，其[密度矩阵](@entry_id:139892)是这些纯[态密度](@entry_id:147894)矩阵的加权平均：
$$
\rho = \sum_i p_i |\psi_i\rangle\langle\psi_i|
$$
一个关键的区分标准是 $\text{Tr}(\rho^2)$。对于纯态，$\text{Tr}(\rho^2) = 1$；对于任何混合态，$\text{Tr}(\rho^2)  1$。

#### 部分迹与子系统

当一个复合系统（例如，一个纠缠的双[量子比特](@entry_id:137928)对）处于一个纯态时，其子系统的状态通常是[混合态](@entry_id:141568)。为了得到子系统的状态，我们需要对复合系统的[密度矩阵](@entry_id:139892)执行一个叫做**部分迹 (partial trace)** 的操作。

例如，考虑一个处于纯态 $|\psi\rangle_{AB}$ 的AB复合系统。子系统A的状态由其**[约化密度矩阵](@entry_id:146315) (reduced density matrix)** $\rho_A$ 描述，其定义为对系统B的自由度求迹：
$$
\rho_A = \text{Tr}_B(\rho_{AB}) = \text{Tr}_B(|\psi\rangle_{AB}\langle\psi|_{AB})
$$
考虑一个纠缠态 $|\psi\rangle_{AB} = \sqrt{p} |01\rangle - i\sqrt{1-p} |10\rangle$，其中 $0  p  1$ [@problem_id:1368631]。通过计算部分迹，我们发现子系统A的[约化密度矩阵](@entry_id:146315)为：
$$
\rho_A = p|0\rangle\langle 0| + (1-p)|1\rangle\langle 1| = \begin{pmatrix} p  0 \\ 0  1-p \end{pmatrix}
$$
这是一个对角矩阵，表示A系统以概率 $p$ 处于 $|0\rangle$ 态，以概率 $1-p$ 处于 $|1\rangle$ 态。我们可以计算它的“混合度”，例如使用**线性熵 (linear entropy)** $S_L = 1 - \text{Tr}(\rho^2)$。对于这个 $\rho_A$，我们得到 $S_{L,A} = 1 - (p^2 + (1-p)^2) = 2p(1-p)$。只要 $p$ 不为 $0$ 或 $1$（即只要原始态是纠缠的），线性熵就大于零，表明子系统A处于[混合态](@entry_id:141568)。这是一个普遍的结论：**纠缠的[纯态](@entry_id:141688)的子系统必然是[混合态](@entry_id:141568)**。

#### 量子通道

对[开放量子系统](@entry_id:138632)演化的最通用描述是**量子通道 (quantum channel)** 或[量子操作](@entry_id:145906)。一个量子通道 $\mathcal{E}$ 是一个将密度矩阵映到[密度矩阵](@entry_id:139892)的线性映射。一个非常有用的表示是**[算子和表示](@entry_id:140073) (operator-sum representation, OSR)**：
$$
\mathcal{E}(\rho) = \sum_k E_k \rho E_k^\dagger
$$
这里的 $\{E_k\}$ 是一组算子，称为**克劳斯算子 (Kraus operators)**。为了使这个映射描述一个物理过程，它必须保持迹不变，即 $\text{Tr}(\mathcal{E}(\rho)) = \text{Tr}(\rho)$。这个要求等价于克劳斯算子满足**[完备性关系](@entry_id:139077)**：
$$
\sum_k E_k^\dagger E_k = I
$$
通过实验表征一个噪声过程，我们可以利用这些物理约束来确定描述该过程的克劳斯算子的参数 [@problem_id:1368614]。

本章介绍的原理——[状态向量](@entry_id:154607)、[酉演化](@entry_id:145020)、[量子测量](@entry_id:272490)、[张量积](@entry_id:140694)和纠缠——构成了[量子计算](@entry_id:142712)的基石。这些概念虽然抽象，但它们共同描绘了一幅与我们日常经验截然不同的现实图景，并为一种全新的计算[范式](@entry_id:161181)打开了大门。在后续章节中，我们将看到如何利用这些原理来构建强大的[量子算法](@entry_id:147346)。