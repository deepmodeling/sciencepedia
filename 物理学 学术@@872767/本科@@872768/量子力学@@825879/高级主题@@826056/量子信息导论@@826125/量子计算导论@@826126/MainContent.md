## 引言
[量子计算](@entry_id:142712)代表了计算科学领域的一场革命，它利用量子力学的奇特规则来处理信息，有望解决当今最强大的经典计算机也无法企及的难题。从[药物设计](@entry_id:140420)到[材料科学](@entry_id:152226)，再到金融建模，其颠覆性潜力正在引发各界的广泛关注。然而，要理解[量子计算](@entry_id:142712)的力量，我们必须首先跨越经典直觉，进入一个由叠加、纠缠和概率主导的全新世界。本文旨在弥合经典计算与[量子计算](@entry_id:142712)之间的概念鸿沟，为读者系统地构建起对这一前沿领域的理解。

在接下来的内容中，我们将分三步探索[量子计算](@entry_id:142712)。我们首先将在“原理与机制”一章中，从最基本的[量子比特](@entry_id:137928)（qubit）出发，建立起描述和操控量子系统的数学语言。接着，在“应用与跨学科联系”一章中，我们将看到这些原理如何催生出强大的[量子算法](@entry_id:147346)，并与物理学、化学等多个学科产生深刻的联系。最后，通过“动手实践”环节，你将有机会亲手应用所学知识，解决具体的[量子计算](@entry_id:142712)问题，从而巩固你的理解。

## 原理与机制

本章将深入探讨[量子计算](@entry_id:142712)的核心原理与基本机制。在前一章介绍背景之后，我们将从最基本的构成单元——[量子比特](@entry_id:137928)（qubit）开始，系统地建立描述和操控[量子信息](@entry_id:137721)的数学框架。我们将探索量子[态的叠加](@entry_id:273993)、测量过程的概率性，以及定义[量子操作](@entry_id:145906)的[酉性](@entry_id:138773)（unitarity）原则。随后，我们将转向[多量子比特系统](@entry_id:142942)，阐明张量积的数学结构，并介绍如何通过量子门（quantum gate）来创建纠缠（entanglement）这一关键的量子资源。最后，本章将讨论几个根本性的量子定理，并引入[密度算符](@entry_id:138151)（density operator）作为描述真实、[开放量子系统](@entry_id:138632)的更通用工具，为理解量子纠错和量子算法的实际挑战奠定基础。

### [量子比特](@entry_id:137928)：量子信息的基本单元

[经典计算](@entry_id:136968)的[基本单位](@entry_id:148878)是比特（bit），它可以处于 $0$ 或 $1$ 两种状态之一。[量子计算](@entry_id:142712)则建立在一个更为丰富的概念之上：**[量子比特](@entry_id:137928)**（qubit）。

#### 单一[量子比特](@entry_id:137928)的状态空间

一个[量子比特](@entry_id:137928)的状态由一个二维[复向量空间](@entry_id:264355) $\mathbb{C}^2$ 中的[单位向量](@entry_id:165907)描述。如同经典比特有两个基本状态，[量子比特](@entry_id:137928)也有一组标准[基矢](@entry_id:199546)，称为**计算[基矢](@entry_id:199546)**（computational basis），记作 $|0\rangle$ 和 $|1\rangle$。它们在[向量空间](@entry_id:151108)中对应于[标准正交基](@entry_id:147779)：

$$
|0\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad |1\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}
$$

量子力学最引人注目的特性之一是**[叠加原理](@entry_id:144649)**（superposition principle）。与只能取 $0$ 或 $1$ 的经典比特不同，一个[量子比特](@entry_id:137928)可以处于 $|0\rangle$ 和 $|1\rangle$ 的线性组合状态。一个任意的单[量子比特](@entry_id:137928)纯态（pure state）$|\psi\rangle$ 可以写为：

$$
|\psi\rangle = \alpha |0\rangle + \beta |1\rangle
$$

其中，$\alpha$ 和 $\beta$ 是复数，称为**概率幅**（probability amplitudes）。这些[概率幅](@entry_id:150609)必须满足[归一化条件](@entry_id:156486) $|\alpha|^2 + |\beta|^2 = 1$，这确保了[量子态](@entry_id:146142)作为概率解释的[自洽性](@entry_id:160889)。这意味着[量子比特](@entry_id:137928)的状态向量位于一个单位球面上，这个球面在 $\mathbb{C}^2$ 中被称为布洛赫球（Bloch sphere），为[量子态](@entry_id:146142)提供了一个直观的几何图像。

#### 测量与[玻恩定则](@entry_id:154470)

尽管[量子比特](@entry_id:137928)可以存在于无限多个叠加态中，但当我们对其进行测量时，其状态会“坍缩”（collapse）到我们所选的测量[基矢](@entry_id:199546)之一。最常见的测量是在计算[基矢](@entry_id:199546) $\lbrace|0\rangle, |1\rangle\rbrace$ 中进行的。根据**[玻恩定则](@entry_id:154470)**（Born's rule），对于处于状态 $|\psi\rangle = \alpha|0\rangle + \beta|1\rangle$ 的[量子比特](@entry_id:137928)，测量结果为 $|0\rangle$ 的概率是 $|\alpha|^2$，测量结果为 $|1\rangle$ 的概率是 $|\beta|^2$。[归一化条件](@entry_id:156486)确保了总概率为 $1$。

测量[基矢](@entry_id:199546)的选择并非仅限于计算[基矢](@entry_id:199546)。任何一组正交归一的[基矢](@entry_id:199546)都可以用作测量基。例如，**哈达玛基**（Hadamard basis），也称X基，由以下两个态构成：

$$
|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle + |1\rangle), \quad |-\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)
$$

一个[量子态](@entry_id:146142) $|\psi\rangle$ 在某个测量[基矢](@entry_id:199546) $|\phi\rangle$ 上被测得的概率由它们[内积](@entry_id:158127)的模平方给出 [@problem_id:1368624] [@problem_id:1368597]：

$$
P(\phi) = |\langle \phi | \psi \rangle|^2
$$

这里 $\langle \phi |$ 是 $|\phi\rangle$ 的共轭转置，称为“bra”向量。例如，对于一个处在 $|\psi\rangle = \frac{3}{5}|0\rangle + \frac{4}{5}|1\rangle$ 态的[量子比特](@entry_id:137928)，我们测量其处于 $|+\rangle$ 态的概率。首先计算[内积](@entry_id:158127)（即概率幅）：

$$
\langle + | \psi \rangle = \left( \frac{1}{\sqrt{2}}(\langle 0| + \langle 1|) \right) \left( \frac{3}{5}|0\rangle + \frac{4}{5}|1\rangle \right) = \frac{1}{\sqrt{2}} \left( \frac{3}{5}\langle 0|0\rangle + \frac{4}{5}\langle 1|1\rangle \right) = \frac{1}{\sqrt{2}} \left( \frac{3}{5} + \frac{4}{5} \right) = \frac{7}{5\sqrt{2}}
$$

因此，测得 $|+\rangle$ 的概率为 $P(+) = |\frac{7}{5\sqrt{2}}|^2 = \frac{49}{50}$。

这个原理揭示了一个深刻的事实：仅通过在单一[基矢](@entry_id:199546)下重复测量，无法完全确定一个未知的[量子态](@entry_id:146142)。例如，在计算[基矢](@entry_id:199546)下测量只能得到 $|\alpha|^2$ 和 $|\beta|^2$ 的值，但无法确定 $\alpha$ 和 $\beta$ 之间的[相对相位](@entry_id:148120)。为了完整地重构一个[量子态](@entry_id:146142)（这一过程称为**[量子态](@entry_id:146142)层析**，quantum state tomography），必须在多个非共线的[基矢](@entry_id:199546)下进行测量 [@problem_id:1368619]。例如，通过结合在计算[基矢](@entry_id:199546)、哈达玛基和另一个称为圆形基（Y基）的[基矢](@entry_id:199546) $\lbrace \frac{1}{\sqrt{2}}(|0\rangle + i|1\rangle), \frac{1}{\sqrt{2}}(|0\rangle - i|1\rangle) \rbrace$ 下的测量结果，就可以唯一地确定[概率幅](@entry_id:150609) $\alpha$ 和 $\beta$，包括它们的相对相位。

### [量子操作](@entry_id:145906)：门与演化

对[量子比特](@entry_id:137928)的操控是通过**量子门**（quantum gates）实现的，这在数学上对应于对其状态向量进行[线性变换](@entry_id:149133)。

#### [单量子比特门](@entry_id:146489)与[酉性](@entry_id:138773)

一个封闭量子系统的演化是可逆的，这意味着信息不会丢失。在数学上，这一物理要求体现在所有量子门都必须由**酉矩阵**（unitary matrix）$U$ 来表示。一个矩阵 $U$ 是酉矩阵，当且仅当它的[共轭转置](@entry_id:147909) $U^\dagger$ 等于它的[逆矩阵](@entry_id:140380)，即：

$$
U^\dagger U = U U^\dagger = I
$$

其中 $I$ 是[单位矩阵](@entry_id:156724)。[酉变换](@entry_id:152599)的一个重要性质是它保持向量的[内积](@entry_id:158127)（以及范数），这意味着它将有效的[量子态](@entry_id:146142)（[单位向量](@entry_id:165907)）映射到有效的[量子态](@entry_id:146142)，并保持了不同态之间的相对“角度”。

一个 $2 \times 2$ 矩阵是[酉矩阵](@entry_id:138978)的等价条件是它的列（或行）向量构成一个正交归一基。这个性质为验证或构建量子门提供了实用的方法。例如，考虑一个由以下矩阵描述的通用单比特门 [@problem_id:1368617]：

$$
G = \frac{1}{2} \begin{pmatrix} 1+i  \beta \\ \sqrt{2}  1-i \end{pmatrix}
$$

为了使 $G$ 成为一个有效的[量子门](@entry_id:143510)，它必须是酉矩阵。我们可以通过要求它的两个列向量 $c_1$ 和 $c_2$ 相互正交且范数为 $1$ 来确定未知的复数 $\beta$。通过计算 $c_1^\dagger c_2 = 0$ 和 $\|c_2\|^2 = 1$，可以解得 $\beta = -\sqrt{2}$。

常见的单比特门包括：
- **泡利-X门 (Pauli-X gate)**：$X = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$，作用是翻转[量子比特](@entry_id:137928)的状态（$|0\rangle \leftrightarrow |1\rangle$），相当于经典计算中的NO[T门](@entry_id:138474)。
- **哈达玛门 (Hadamard gate)**：$H = \frac{1}{\sqrt{2}} \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}$，作用是创建等权叠加态，例如 $H|0\rangle = |+\rangle$ 和 $H|1\rangle = |-\rangle$。

#### [多量子比特系统](@entry_id:142942)与受控门

当我们将多个[量子比特](@entry_id:137928)组合成一个系统时，其状态空间是各个子系统[状态空间](@entry_id:177074)的**[张量积](@entry_id:140694)**（tensor product）。例如，一个[双量子比特系统](@entry_id:203437)的[状态空间](@entry_id:177074)是 $\mathbb{C}^2 \otimes \mathbb{C}^2 \cong \mathbb{C}^4$。其计算[基矢](@entry_id:199546)由单个[量子比特](@entry_id:137928)的[基矢](@entry_id:199546)张量积而成：$|00\rangle \equiv |0\rangle \otimes |0\rangle$, $|01\rangle \equiv |0\rangle \otimes |1\rangle$, $|10\rangle \equiv |1\rangle \otimes |0\rangle$, $|11\rangle \equiv |1\rangle \otimes |1\rangle$。

[多量子比特门](@entry_id:139015)是作用于这个更大状态空间的[酉矩阵](@entry_id:138978)。其中最重要的是**受控门**（controlled gates），它们是产生和操控量子纠缠的关键。
- **[受控非门](@entry_id:180955) (CNOT)**：这是一个双比特门，其中一个[量子比特](@entry_id:137928)是**控制比特**，另一个是**目标比特**。只有当控制比特为 $|1\rangle$ 时，目标比特的状态才会被翻转（应用X门）。
- **[Toffoli门](@entry_id:137725) (CCNOT)**：这是一个三比特门，拥有两个控制比特和一个目标比特。只有当两个控制比特都处于 $|1\rangle$ 状态时，目标比特才会被翻转。

我们可以通过定义量子门对所有计算[基矢](@entry_id:199546)的作用来构建其矩阵表示。例如，对于[Toffoli门](@entry_id:137725)，其作用规则是：
- 如果控制比特为 $|q_1 q_2\rangle \neq |11\rangle$，则 $U|q_1 q_2 q_3\rangle = |q_1 q_2 q_3\rangle$。
- 如果控制比特为 $|11\rangle$，则 $U|11 q_3\rangle = |11 (1-q_3)\rangle$。

按照字典序[排列](@entry_id:136432)[基矢](@entry_id:199546)（$|000\rangle, |001\rangle, \dots, |111\rangle$），[Toffoli门](@entry_id:137725)的 $8 \times 8$ 矩阵表示大部分是对角线为 $1$ 的单位阵，只在最后两行两列形成一个X门块，交换了 $|110\rangle$ 和 $|111\rangle$ 的位置 [@problem_id:1368601]。

$$
\text{CCNOT} = \begin{pmatrix}
1  0  0  0  0  0  0  0\\
0  1  0  0  0  0  0  0\\
0  0  1  0  0  0  0  0\\
0  0  0  1  0  0  0  0\\
0  0  0  0  1  0  0  0\\
0  0  0  0  0  1  0  0\\
0  0  0  0  0  0  0  1\\
0  0  0  0  0  0  1  0
\end{pmatrix}
$$

### 关键量子现象及其推论

[叠加原理](@entry_id:144649)和[酉演化](@entry_id:145020)共同催生了一些深刻且完全非经典的现象，它们是[量子计算](@entry_id:142712)能力的源泉。

#### 纠缠：超越经典的关联

一个[多量子比特系统](@entry_id:142942)，如果其状态**不能**被写成其各个子系统状态的张量积，那么这个状态就被称为**[纠缠态](@entry_id:152310)**（entangled state）。反之，能够写成张量积形式的状态被称为**可分离态**（separable state）或乘积态。

考虑一个一般的双[量子比特](@entry_id:137928)态：$|\psi\rangle = \alpha|00\rangle + \beta|01\rangle + \gamma|10\rangle + \delta|11\rangle$。如果这个态是可分离的，即 $|\psi\rangle = (a|0\rangle + b|1\rangle) \otimes (c|0\rangle + d|1\rangle)$，展开后我们得到：

$$
|\psi\rangle = ac|00\rangle + ad|01\rangle + bc|10\rangle + bd|11\rangle
$$

通过比较系数，我们发现 $\alpha = ac, \beta = ad, \gamma = bc, \delta = bd$。这些系数之间存在一个特定关系：$\alpha\delta = (ac)(bd) = abcd$ 并且 $\beta\gamma = (ad)(bc) = abcd$。因此，一个双[量子比特](@entry_id:137928)[纯态](@entry_id:141688)是可分离的，当且仅当其系数满足**可分离性判据**：

$$
\alpha\delta = \beta\gamma
$$

如果 $\alpha\delta \neq \beta\gamma$，则该态必然是纠缠的 [@problem_id:1368621]。例如，著名的贝尔态（Bell state）$|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$，其系数为 $\alpha=\frac{1}{\sqrt{2}}, \beta=0, \gamma=0, \delta=\frac{1}{\sqrt{2}}$。这里 $\alpha\delta = \frac{1}{2}$ 而 $\beta\gamma = 0$，因此它是一个[纠缠态](@entry_id:152310)。纠缠意味着对其中一个[量子比特](@entry_id:137928)的测量结果会瞬间影响到另一个[量子比特](@entry_id:137928)的测量概率，无论它们相隔多远，这种关联是经典物理无法解释的。

#### [不可克隆定理](@entry_id:146200)

[量子信息](@entry_id:137721)的一个根本限制是**[不可克隆定理](@entry_id:146200)**（No-Cloning Theorem），它指出：不可能创建一个设备，能够完美地复制一个任意的、未知的[量子态](@entry_id:146142)。

我们可以通过反证法来证明这一点 [@problem_id:1368640]。假设存在这样一个“[量子克隆](@entry_id:138347)机”，它由一个酉算符 $U$ 描述。这个机器接收一个待克隆的态 $|\psi\rangle$ 和一个处于“空白”态（如 $|0\rangle$）的辅助比特，输出两个都处于 $|\psi\rangle$ 态的[量子比特](@entry_id:137928)。其数学表达式为：

$$
U (|\psi\rangle \otimes |0\rangle) = |\psi\rangle \otimes |\psi\rangle
$$

现在，我们用两个不同的非正交态 $|\psi_A\rangle$ 和 $|\psi_B\rangle$ 来测试这台机器。根据[酉演化](@entry_id:145020)的线性性质，它必须保持任意两个初态的[内积](@entry_id:158127)。初始状态的[内积](@entry_id:158127)为：

$$
\langle \Phi_{in, A} | \Phi_{in, B} \rangle = (\langle \psi_A | \otimes \langle 0 |) (|\psi_B\rangle \otimes |0\rangle) = \langle \psi_A | \psi_B \rangle \langle 0 | 0 \rangle = \langle \psi_A | \psi_B \rangle
$$

而克隆后输出状态的[内积](@entry_id:158127)为：

$$
\langle \Phi_{out, A} | \Phi_{out, B} \rangle = (\langle \psi_A | \otimes \langle \psi_A |) (|\psi_B\rangle \otimes |\psi_B\rangle) = \langle \psi_A | \psi_B \rangle \langle \psi_A | \psi_B \rangle = (\langle \psi_A | \psi_B \rangle)^2
$$

由于[酉演化](@entry_id:145020)必须保持[内积](@entry_id:158127)，我们必须有 $\langle \psi_A | \psi_B \rangle = (\langle \psi_A | \psi_B \rangle)^2$。设 $x = \langle \psi_A | \psi_B \rangle$，方程 $x = x^2$ 的解只有 $x=0$ 或 $x=1$。这意味着，克隆机只能完美克隆一组正交的态（$x=0$）或者相同的态（$x=1$）。对于任意一个未知的、非正交的[量子态](@entry_id:146142)，这个等式不成立，从而导致矛盾。这证明了[通用量子克隆机](@entry_id:146760)是不可能存在的。

#### 非正交态的不可区分性

[不可克隆定理](@entry_id:146200)背后是一个更普适的原理：非正交的[量子态](@entry_id:146142)无法被任何单次测量完美地区分开。如果我们可以完美区分两个非正交态，我们就可以通过确定输入态的身份然后制备一个相同的态来绕过[不可克隆定理](@entry_id:146200)。

假设发送者以等概率发送两个非正交态 $|\psi_A\rangle$ 或 $|\psi_B\rangle$ 之一。接收者希望通过一次测量来判断收到的是哪个态。无论接收者设计多么巧妙的测量方案，总会存在一个最小的平均[错误概率](@entry_id:267618)。这个极限被称为**[Helstrom界](@entry_id:142767)**。对于等概率发送的两个[纯态](@entry_id:141688)，最小错误概率为 [@problem_id:1368666]：

$$
P_{\text{err}}^{\text{min}} = \frac{1}{2} \left( 1 - \sqrt{1 - |\langle \psi_A | \psi_B \rangle|^2} \right)
$$

这个概率只在 $|\langle \psi_A | \psi_B \rangle| = 0$（即态正交）时为零，并且随着态的重叠度 $|\langle \psi_A | \psi_B \rangle|$ 的增加而增加。这为[量子密码学](@entry_id:144827)的安全性提供了理论基础。

### 真实量子系统的描述

到目前为止，我们主要讨论的是封闭系统中的[纯态](@entry_id:141688)。然而，真实的量子系统总是与环境发生相互作用，并且我们可能只对一个更[大系统](@entry_id:166848)的一部分感兴趣。为了处理这些更现实的情景，我们需要引入**[密度算符](@entry_id:138151)**（density operator） formalism。

#### [混合态](@entry_id:141568)与[密度算符](@entry_id:138151)

一个量子系统可能不处于一个确定的纯态 $|\psi\rangle$，而是以概率 $p_i$ 处于一系列[纯态](@entry_id:141688) $|\psi_i\rangle$ 中的某一个。这种状态的集合被称为**混合态**（mixed state），它由[密度算符](@entry_id:138151) $\rho$ 描述：

$$
\rho = \sum_i p_i |\psi_i\rangle\langle\psi_i|
$$

其中 $p_i$ 是经典概率，满足 $\sum_i p_i = 1$。纯态 $|\psi\rangle$ 是其特殊情况，其[密度算符](@entry_id:138151)为 $\rho = |\psi\rangle\langle\psi|$。一个[密度算符](@entry_id:138151) $\rho$ 必须满足三个性质：
1.  它是厄米（Hermitian）的：$\rho = \rho^\dagger$。
2.  它是半正定的：$\langle \phi | \rho | \phi \rangle \ge 0$ 对任意 $|\phi\rangle$ 成立。
3.  它的迹（trace）为1：$\mathrm{Tr}(\rho) = 1$。

如果一个系统的状态由 $\rho$ 描述，那么测量得到某个结果 $|\phi\rangle$ 的概率由 $P(\phi) = \langle\phi|\rho|\phi\rangle = \mathrm{Tr}(\rho |\phi\rangle\langle\phi|)$ 给出 [@problem_id:2098729]。

#### 子系统与部分迹

[密度算符](@entry_id:138151)的强大之处在于它能描述一个更大纠缠系统的一部分。即使一个复合系统AB处于一个[纯态](@entry_id:141688) $|\psi_{AB}\rangle$，其子系统A或B通常也必须用混合态来描述。子系统A的状态由其**[约化密度算符](@entry_id:190449)**（reduced density operator）$\rho_A$ 给出，它是通过对复合系统的[密度算符](@entry_id:138151) $\rho_{AB} = |\psi_{AB}\rangle\langle\psi_{AB}|$ 关于子系统B进行**部分迹**（partial trace）运算得到的：

$$
\rho_A = \mathrm{Tr}_B(\rho_{AB}) = \sum_j {}_B\langle j | \rho_{AB} | j \rangle_B
$$

其中 $\lbrace |j\rangle_B \rbrace$ 是子系统B的任意一组[标准正交基](@entry_id:147779)。

例如，考虑一个处于纯[纠缠态](@entry_id:152310) $|\psi\rangle = \alpha|00\rangle + \beta|11\rangle$ 的双比特系统 [@problem_id:2098711]。其总[密度算符](@entry_id:138151)为 $\rho = (|\psi\rangle\langle\psi|)$。对B系统进行部分迹运算，我们得到A系统的[约化密度算符](@entry_id:190449)：

$$
\rho_A = |\alpha|^2 |0\rangle_A\langle 0|_A + |\beta|^2 |1\rangle_A\langle 1|_A = \begin{pmatrix} |\alpha|^2  0 \\ 0  |\beta|^2 \end{pmatrix}
$$

除非 $|\alpha|$ 或 $|\beta|$ 有一个为1（此时系统是可分离的），否则 $\rho_A$ 是一个[对角矩阵](@entry_id:637782)，代表一个混合态。这意味着，尽管整个系统的信息是完整的（纯态），但对于只能访问子系统A的观察者来说，该子系统表现为一个概率混合。**纠缠是子系统呈现混合态的根源**。

#### 量子通道与退相干

真实量子[系统与环境](@entry_id:142270)的相互作用（噪声）会导致[量子信息](@entry_id:137721)的损失，这一过程称为**[退相干](@entry_id:145157)**（decoherence）。这种演化不再能用单一的[酉矩阵](@entry_id:138978)来描述，而是用一种更广义的映射——**量子通道**（quantum channel）来刻画。

一个量子通道 $\mathcal{E}$ 的作用可以通过**[算符和表示](@entry_id:140073)**（operator-sum representation）来描述，它将输入[密度算符](@entry_id:138151) $\rho_{in}$ 映射到输出[密度算符](@entry_id:138151) $\rho_{out}$：

$$
\rho_{out} = \mathcal{E}(\rho_{in}) = \sum_k E_k \rho_{in} E_k^\dagger
$$

这里的 $E_k$ 被称为**[克劳斯算符](@entry_id:144882)**（Kraus operators），它们描述了[系统与环境](@entry_id:142270)之间可能发生的各种相互作用。它们必须满足[完备性关系](@entry_id:139077) $\sum_k E_k^\dagger E_k = I$，以确保 $\mathrm{Tr}(\rho_{out}) = 1$。

一个典型的[噪声模型](@entry_id:752540)是**[退相干](@entry_id:145157)通道**（dephasing channel），它会随机地引入相[位错](@entry_id:157482)误。例如，一个作用于单比特的[退相干](@entry_id:145157)通道可以由[克劳斯算符](@entry_id:144882) $E_0 = \sqrt{1-p} \cdot I$ 和 $E_1 = \sqrt{p} \cdot Z$ 描述，其中 $p$ 是发生相位翻转（由泡利-Z门引起）的概率。

我们可以用这个工具来分析纠缠如何在噪声环境中衰减 [@problem_id:2098714]。假设一个[贝尔态](@entry_id:140749) $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$ 的第一个[量子比特](@entry_id:137928)经过上述[退相干](@entry_id:145157)通道。初始[密度矩阵](@entry_id:139892)为 $\rho_0 = |\Phi^+\rangle\langle\Phi^+|$。演化后的状态为：

$$
\rho_f = (E_0 \otimes I)\rho_0(E_0^\dagger \otimes I) + (E_1 \otimes I)\rho_0(E_1^\dagger \otimes I)
$$

计算后发现，最终状态是两个贝尔态的混合：$\rho_f = (1-p)|\Phi^+\rangle\langle\Phi^+| + p|\Phi^-\rangle\langle\Phi^-|$。我们可以使用**并发度**（concurrence）$C$ 这一度量来量化这个态的纠缠程度。计算表明，该态的并发度为 $C(\rho_f) = |1-2p|$。当 $p=0$ 时，$C=1$（最大纠缠）；当 $p=0.5$ 时，$C=0$（纠缠完全消失，系统变成[最大混合态](@entry_id:137775)）；当 $p=1$ 时，$C=1$（系统变为另一个最大[纠缠态](@entry_id:152310) $|\Phi^-\rangle$）。这清晰地展示了环境噪声如何逐步侵蚀宝贵的[量子纠缠](@entry_id:136576)资源。

### [量子计算](@entry_id:142712)的能力与局限

最后，我们简要讨论一下构建一个[通用量子计算](@entry_id:137200)机需要什么，以及其能力的边界在哪里。

一个**[通用量子门集](@entry_id:136517)**（universal quantum gate set）是指一个有限的[量子门](@entry_id:143510)集合，通过组合这些门可以以任意精度近似任何可能的[酉变换](@entry_id:152599)。一个常见的[通用门集](@entry_id:191428)是 {[Hadamard门](@entry_id:146898), CNOT门, [T门](@entry_id:138474)}，其中 [T门](@entry_id:138474) ($T = \begin{pmatrix} 1  0 \\ 0  e^{i\pi/4} \end{pmatrix}$) 是一个引入[复数相位](@entry_id:173474)的关键单比特门。

然而，并非所有门集都是通用的。一个门集的能力受到其构成门的数学性质的限制。例如，考虑一个只由实数矩阵表示的量子门构成的“实值量子引擎” [@problem_id:2098749]。由于实矩阵的乘积仍然是实矩阵，这个引擎能实现的任何操作，其最终的等效[酉矩阵](@entry_id:138978)也必须是实数的（最多相差一个[全局相位](@entry_id:147947)）。

这意味着，那些无法通过乘以一个[全局相位](@entry_id:147947)因子 $e^{i\phi}$ 变成实数矩阵的门，是这个引擎永远无法合成的。例如，[相位门](@entry_id:143669) $S = \begin{pmatrix} 1  0 \\ 0  i \end{pmatrix}$ 和 [T门](@entry_id:138474)都含有无法通过[全局相位](@entry_id:147947)消除的“真正”的复数项。因此，它们无法由一个纯实数的门集生成。这个例子说明，为了实现通用的[量子计算](@entry_id:142712)，产生和控制[复数相位](@entry_id:173474)是必不可少的能力。