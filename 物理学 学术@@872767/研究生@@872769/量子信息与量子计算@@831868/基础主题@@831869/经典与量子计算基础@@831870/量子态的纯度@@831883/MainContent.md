## 引言
在量子世界中，一个系统的状态可以完美确知（[纯态](@entry_id:141688)），也可能因为与环境的纠缠或经典不确定性而处于多种可能性的混合中（[混合态](@entry_id:141568)）。然而，如何用一个简单的标量来精确衡量一个[量子态](@entry_id:146142)“纯”或“混合”的程度？这正是**[量子态纯度](@entry_id:153596)（Purity of a Quantum State）**这一核心概念所要解决的问题。纯度不仅为我们提供了一个数学上的度量，更是一把解锁量子现象本质的钥匙，它将[量子纠缠](@entry_id:136576)、[退相干](@entry_id:145157)以及[量子测量](@entry_id:272490)等基本过程联系在一起。

本文将系统性地探索[量子态纯度](@entry_id:153596)的理论与应用。在第一章**“原理和机制”**中，我们将深入其数学定义 $\gamma = \text{Tr}(\rho^2)$，探讨其几何直观（布洛赫球），并阐明它如何区分经典混合与[量子纠缠](@entry_id:136576)。接下来的第二章**“应用与[交叉](@entry_id:147634)学科联系”**将展示纯度作为一个强大的分析工具，在[量子计算](@entry_id:142712)、凝聚态物理、乃至[黑洞](@entry_id:158571)[信息佯谬](@entry_id:190166)和宇宙学等前沿领域中的广泛应用。最后，通过**“动手实践”**环节，读者将有机会通过具体计算来巩固所学知识。

通过这三个章节的学习，读者将全面掌握纯度的概念，理解其在理论分析和实验表征中的重要作用，并洞悉其如何成为连接不同物理分支的桥梁。

## 原理和机制

在量子力学中，一个系统的状态可以用一个态矢量 $|\psi\rangle$（对于**纯态**）或更普遍地用一个**[密度算符](@entry_id:138151)** $\rho$（对于**混合态**）来描述。虽然[密度算符](@entry_id:138151)提供了完整的状态信息，但通常需要一个简单的标量来量化状态的“纯度”或“混合度”。这个量就是**纯度（Purity）**，它在量子信息、[量子计算](@entry_id:142712)和[开放量子系统](@entry_id:138632)中扮演着核心角色。本章旨在深入探讨纯度的基本原理、计算方法及其在各种物理情境中的关键作用机制。

### 纯度的定义与基本性质

一个量子系统的状态由[密度算符](@entry_id:138151) $\rho$ 描述，该算符是作用于系统希尔伯特空间 $\mathcal{H}$ 的一个厄米、正半定且迹为1的算符。该系统的**纯度** $\gamma$ 定义为[密度算符](@entry_id:138151)平方的迹：

$$
\gamma = \text{Tr}(\rho^2)
$$

为了理解这个定义的内涵，我们可以考虑 $\rho$ 的[谱分解](@entry_id:173707)。由于 $\rho$ 是[厄米算符](@entry_id:153410)，它可以被[对角化](@entry_id:147016)：

$$
\rho = \sum_{i=1}^{d} \lambda_i |\phi_i\rangle\langle\phi_i|
$$

其中 $\{|\phi_i\rangle\}$ 是[希尔伯特空间](@entry_id:261193)的一组[标准正交基](@entry_id:147779)（$\rho$ 的本征矢量），$\lambda_i$ 是对应的实数[本征值](@entry_id:154894)， $d = \dim(\mathcal{H})$ 是[希尔伯特空间](@entry_id:261193)的维度。由于 $\rho$ 是正半定的且迹为1，其[本征值](@entry_id:154894)满足 $\lambda_i \ge 0$ 和 $\sum_{i=1}^{d} \lambda_i = 1$。因此，[本征值](@entry_id:154894) $\lambda_i$ 可以被解释为系统处于纯态 $|\phi_i\rangle$ 的概率。

利用这个[谱分解](@entry_id:173707)，纯度可以表示为[本征值](@entry_id:154894)的平方和：

$$
\gamma = \text{Tr}(\rho^2) = \text{Tr}\left( \left(\sum_i \lambda_i |\phi_i\rangle\langle\phi_i|\right) \left(\sum_j \lambda_j |\phi_j\rangle\langle\phi_j|\right) \right) = \text{Tr}\left( \sum_{i,j} \lambda_i \lambda_j |\phi_i\rangle\langle\phi_i|\phi_j\rangle\langle\phi_j| \right)
$$

由于[基矢](@entry_id:199546)量的正交性 $\langle\phi_i|\phi_j\rangle = \delta_{ij}$，上式简化为：

$$
\gamma = \text{Tr}\left( \sum_i \lambda_i^2 |\phi_i\rangle\langle\phi_i| \right) = \sum_i \lambda_i^2 \text{Tr}(|\phi_i\rangle\langle\phi_i|) = \sum_{i=1}^{d} \lambda_i^2
$$

这个表达式揭示了纯度的本质：它是对[本征值分布](@entry_id:194746)“尖锐度”的度量。

#### 纯度的界限

纯度的取值范围是有界的。利用柯西-[施瓦茨不等式](@entry_id:202153)，我们可以推导出其上下界。考虑两个 $d$ 维向量 $\vec{u} = (1, 1, \dots, 1)$ 和 $\vec{v} = (\lambda_1, \lambda_2, \dots, \lambda_d)$。柯西-施瓦茨不等式指出 $(\vec{u} \cdot \vec{v})^2 \le |\vec{u}|^2 |\vec{v}|^2$，即：

$$
\left(\sum_{i=1}^{d} 1 \cdot \lambda_i\right)^2 \le \left(\sum_{i=1}^{d} 1^2\right) \left(\sum_{i=1}^{d} \lambda_i^2\right)
$$

利用 $\sum \lambda_i = 1$ 和 $\sum \lambda_i^2 = \gamma$，我们得到：

$$
1^2 \le d \cdot \gamma \implies \gamma \ge \frac{1}{d}
$$

另一方面，由于 $\lambda_i \in [0, 1]$，我们有 $\lambda_i^2 \le \lambda_i$。因此：

$$
\gamma = \sum_{i=1}^{d} \lambda_i^2 \le \sum_{i=1}^{d} \lambda_i = 1
$$

综上所述，纯度的取值范围为 $\frac{1}{d} \le \gamma \le 1$ [@problem_id:1988239]。

*   **最大纯度 $(\gamma = 1)$**：当且仅当一个[本征值](@entry_id:154894)为1，其余所有[本征值](@entry_id:154894)均为0时，$\gamma = 1^2 + 0^2 + \dots = 1$。这对应于**[纯态](@entry_id:141688)**，其[密度算符](@entry_id:138151)为投影算符 $\rho = |\psi\rangle\langle\psi|$，满足 $\rho^2 = \rho$。
*   **最小纯度 $(\gamma = 1/d)$**：当且仅当所有[本征值](@entry_id:154894)都相等，即 $\lambda_i = 1/d$ 对所有 $i$ 成立时，达到下界。此时 $\gamma = \sum_{i=1}^d (1/d)^2 = d \cdot (1/d^2) = 1/d$。这对应于**[最大混合态](@entry_id:137775)**，其[密度算符](@entry_id:138151)为 $\rho = \frac{1}{d}I$，其中 $I$ 是单位算符。该状态在任何基下都表现出完全的随机性 [@problem_id:2088988]。

**计算示例**
考虑一个[量子比特](@entry_id:137928)（qubit, $d=2$），其密度矩阵在计算基 $\{|0\rangle, |1\rangle\}$ 下表示为 [@problem_id:1988267]：
$$
\rho = \begin{pmatrix} \frac{7}{8}  \frac{1}{8} \\ \frac{1}{8}  \frac{1}{8} \end{pmatrix}
$$
为了计算其纯度，我们首先计算 $\rho^2$：
$$
\rho^2 = \begin{pmatrix} \frac{7}{8}  \frac{1}{8} \\ \frac{1}{8}  \frac{1}{8} \end{pmatrix} \begin{pmatrix} \frac{7}{8}  \frac{1}{8} \\ \frac{1}{8}  \frac{1}{8} \end{pmatrix} = \begin{pmatrix} (\frac{7}{8})^2 + (\frac{1}{8})^2  \frac{7}{8}\frac{1}{8} + \frac{1}{8}\frac{1}{8} \\ \frac{1}{8}\frac{7}{8} + \frac{1}{8}\frac{1}{8}  (\frac{1}{8})^2 + (\frac{1}{8})^2 \end{pmatrix} = \begin{pmatrix} \frac{50}{64}  \frac{8}{64} \\ \frac{8}{64}  \frac{2}{64} \end{pmatrix}
$$
纯度是 $\rho^2$ 的迹：
$$
\gamma = \text{Tr}(\rho^2) = \frac{50}{64} + \frac{2}{64} = \frac{52}{64} = \frac{13}{16}
$$
由于 $1/2  13/16  1$，这个状态是一个[混合态](@entry_id:141568)，既不是纯态也不是[最大混合态](@entry_id:137775)。

### 单[量子比特](@entry_id:137928)的纯度：布洛赫球视角

对于一个单[量子比特](@entry_id:137928)系统，纯度有一个优美的几何解释。任何单比特密度矩阵都可以用**[布洛赫矢量](@entry_id:144181)** $\vec{r} = (r_x, r_y, r_z)$ 表示：

$$
\rho = \frac{1}{2}(I + \vec{r} \cdot \vec{\sigma})
$$

其中 $I$ 是 $2 \times 2$ 单位矩阵，$\vec{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$ 是[泡利矩阵](@entry_id:139493)矢量。[布洛赫矢量](@entry_id:144181) $\vec{r}$ 的长度 $|\vec{r}| = \sqrt{r_x^2 + r_y^2 + r_z^2}$ 限定在单位球内，即 $|\vec{r}| \le 1$。

我们可以将纯度 $\gamma$ 直接用[布洛赫矢量](@entry_id:144181) $\vec{r}$ 的分量表示 [@problem_id:1988508]。为此，我们计算 $\rho^2$：
$$
\rho^2 = \frac{1}{4}(I + \vec{r} \cdot \vec{\sigma})^2 = \frac{1}{4}(I^2 + 2(\vec{r} \cdot \vec{\sigma}) + (\vec{r} \cdot \vec{\sigma})^2)
$$
利用泡利矩阵的关键恒等式 $(\vec{r} \cdot \vec{\sigma})^2 = |\vec{r}|^2 I$，上式变为：
$$
\rho^2 = \frac{1}{4}((1 + |\vec{r}|^2)I + 2(\vec{r} \cdot \vec{\sigma}))
$$
取迹，并利用 $\text{Tr}(I) = 2$ 和 $\text{Tr}(\sigma_k) = 0$ 的性质，我们得到：
$$
\gamma = \text{Tr}(\rho^2) = \frac{1}{4}((1 + |\vec{r}|^2)\text{Tr}(I) + 2\text{Tr}(\vec{r} \cdot \vec{\sigma})) = \frac{1}{4}((1 + |\vec{r}|^2) \cdot 2 + 0)
$$
最终得到纯度与[布洛赫矢量](@entry_id:144181)长度的直接关系：
$$
\gamma = \frac{1}{2}(1 + |\vec{r}|^2)
$$
这个公式提供了一个强大的几何直观：
*   **[纯态](@entry_id:141688)**对应于布洛赫球的**表面**，其上 $|\vec{r}| = 1$，因此 $\gamma = \frac{1}{2}(1 + 1) = 1$。对于一个[纯态](@entry_id:141688)，其[密度矩阵](@entry_id:139892)元素必须满足特定条件，例如对于矩阵 $\rho = \begin{pmatrix} a  b \\ b^*  1-a \end{pmatrix}$，纯度为1的条件是 $|b|^2 = a(1-a)$ [@problem_id:1190217]。
*   **[混合态](@entry_id:141568)**对应于布洛赫球的**内部**，其中 $|\vec{r}|  1$，因此 $\gamma  1$。
*   **[最大混合态](@entry_id:137775)**对应于布洛赫球的**中心**，其中 $\vec{r} = \vec{0}$，因此 $|\vec{r}| = 0$，纯度达到最小值 $\gamma = \frac{1}{2}(1 + 0) = 1/2$。

此外，[布洛赫矢量](@entry_id:144181)的分量具有明确的物理意义：它们是相应泡利算符的[期望值](@entry_id:153208)，$r_k = \langle \sigma_k \rangle = \text{Tr}(\rho \sigma_k)$。这些[期望值](@entry_id:153208)又可以直接与测量结果的概率联系起来。例如，在 $\sigma_k$ 的本征基下测量，得到 $+1$ 结果的概率为 $p_k$，则 $\langle \sigma_k \rangle = p_k \cdot (+1) + (1-p_k) \cdot (-1) = 2p_k - 1$。因此，纯度可以直接通过实验测量的概率 $p_x, p_y, p_z$ 来确定 [@problem_id:112487]：
$$
\gamma = \frac{1 + (2p_x-1)^2 + (2p_y-1)^2 + (2p_z-1)^2}{2}
$$

### 纯度、混合与纠缠

[量子态](@entry_id:146142)的混合性主要来源于两个截然不同的物理过程：经典（非相干）混合和[量子纠缠](@entry_id:136576)。纯度是区分和量化这两种效应的有力工具。

#### 非相干混合

当一个系统以概率 $p_i$ 处于一系列状态 $\rho_i$ 时，其整体描述由这些状态的经典加权平均给出，即 $\rho = \sum_i p_i \rho_i$。这种混合总是导致纯度的降低（或不变）。

考虑一个由两个[纯态](@entry_id:141688) $\rho_1=|\psi_1\rangle\langle\psi_1|$ 和 $\rho_2=|\psi_2\rangle\langle\psi_2|$ 以概率 $p$ 和 $1-p$ 混合而成的[量子比特](@entry_id:137928)态 $\rho_{mix} = p\rho_1 + (1-p)\rho_2$。设这两个纯态在布洛赫球上的对应矢量 $\vec{r}_1$ 和 $\vec{r}_2$ 之间的夹角为 $\theta$。[混合态](@entry_id:141568)的[布洛赫矢量](@entry_id:144181)为 $\vec{r}_{mix} = p\vec{r}_1 + (1-p)\vec{r}_2$。其纯度为 [@problem_id:112615]：
$$
\gamma_{mix} = \frac{1}{2}(1 + |\vec{r}_{mix}|^2) = 1 - p(1-p)(1 - \cos\theta)
$$
这个结果非常直观：
*   如果两个态相同 ($\theta=0$)，混合后仍为该纯态，$\gamma_{mix}=1$。
*   如果两个态正交 ($\theta=\pi$)，例如 $|0\rangle$ 和 $|1\rangle$，混合导致的纯度损失最大。
*   混合的概率越接近均等 ($p=1/2$)，纯度损失也越大。

例如，一个系统有 $50\%$ 的概率处于 $|0\rangle$ 态，有 $50\%$ 的概率处于 $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle)$ 态。这两个态在布洛赫球上是正交的（$\vec{r}_z \cdot \vec{r}_x = 0$, $\theta=\pi/2$）。由此产生的混合态 $\rho = \frac{1}{2}|0\rangle\langle0| + \frac{1}{2}|+\rangle\langle+|$ 的纯度为 $\gamma = 1 - \frac{1}{2}(1-\frac{1}{2})(1-0) = \frac{3}{4}$ [@problem_id:2110632]。

更一般地，对于两个任意（可能已是混合）态 $\rho_1$ 和 $\rho_2$ 的等权重混合 $\rho = \frac{1}{2}(\rho_1 + \rho_2)$，其纯度可以表示为 [@problem_id:710748]：
$$
\gamma = \text{Tr}(\rho^2) = \frac{1}{4}\text{Tr}(\rho_1^2 + \rho_2^2 + \rho_1\rho_2 + \rho_2\rho_1) = \frac{\gamma_1 + \gamma_2 + 2C_{12}}{4}
$$
其中 $\gamma_1, \gamma_2$ 是原始[态的纯度](@entry_id:185476)，而 $C_{12} = \text{Tr}(\rho_1\rho_2)$ 是两个[密度算符](@entry_id:138151)的[希尔伯特-施密特内积](@entry_id:190429)，它量化了两个态的“重叠”程度。

#### 纯度与量子纠缠

[量子纠缠](@entry_id:136576)是[多体系统](@entry_id:144006)的一个纯粹的量子特性，它也导致子系统的混合性。考虑一个处于纯态 $|\Psi\rangle_{AB}$ 的二体系统 $AB$。除非 $|\Psi\rangle_{AB}$ 是一个乘积态，否则其子系统 $A$ 或 $B$ 的状态必然是[混合态](@entry_id:141568)。子系统 $A$ 的状态由**[约化密度算符](@entry_id:190449)** $\rho_A = \text{Tr}_B(|\Psi\rangle_{AB}\langle\Psi|_{AB})$ 描述，其中 $\text{Tr}_B$ 表示对子系统 $B$ 的自由度求[偏迹](@entry_id:146482)。

子系统 $A$ 的纯度 $\gamma_A = \text{Tr}(\rho_A^2)$ 直接量化了 $A$ 与 $B$ 之间的纠缠程度。

利用**[施密特分解](@entry_id:145934)**，任何二体纯态都可以写成 $|\Psi\rangle_{AB} = \sum_i \lambda_i |u_i\rangle_A |v_i\rangle_B$，其中 $\{|u_i\rangle_A\}$ 和 $\{|v_i\rangle_B\}$ 分别是子系统 $A$ 和 $B$ 的标准正交基，$\lambda_i \ge 0$ 是[施密特系数](@entry_id:137823)，满足 $\sum_i \lambda_i^2 = 1$。子系统 $A$ 的[约化密度算符](@entry_id:190449)为[对角形式](@entry_id:264850)：
$$
\rho_A = \sum_i \lambda_i^2 |u_i\rangle_A\langle u_i|_A
$$
其纯度因此为 [@problem_id:943618]：
$$
\gamma_A = \text{Tr}(\rho_A^2) = \sum_i (\lambda_i^2)^2
$$
这个表达式是连接纠缠和子系统纯度的桥梁。[施密特系数](@entry_id:137823)[分布](@entry_id:182848)越均匀，纠缠程度越高，子系统的纯度就越低。

*   **无纠缠（乘积态）**：只有一个[施密特系数](@entry_id:137823)为1（例如 $\lambda_1=1$），其余为0。此时 $\gamma_A = 1^2 = 1$，子系统 $A$ 处于纯态。
*   **最大纠缠**：对于 $d \times d$ 系统，当所有 $d$ 个[施密特系数](@entry_id:137823)都相等，即 $\lambda_i = 1/\sqrt{d}$ 时，纠缠达到最大。此时，$\rho_A = \sum_i (1/d)|u_i\rangle_A\langle u_i|_A = \frac{1}{d}I_A$，子系统处于[最大混合态](@entry_id:137775)，其纯度为最小值 $\gamma_A = \sum_i (1/d)^2 = d \cdot (1/d^2) = 1/d$ [@problem_id:112595]。

例如，对于[三量子比特](@entry_id:146257)的[GHZ态](@entry_id:182114) $|\text{GHZ}\rangle = \frac{1}{\sqrt{2}}(|000\rangle + |111\rangle)$，任何一个单比特的[约化密度矩阵](@entry_id:146315)都是 $\rho_A = \frac{1}{2}(|0\rangle\langle0| + |1\rangle\langle1|) = \frac{1}{2}I$，其纯度为 $1/2$。而对于[W态](@entry_id:180654) $|W\rangle = \frac{1}{\sqrt{3}}(|100\rangle + |010\rangle + |001\rangle)$，单比特的[约化密度矩阵](@entry_id:146315)为 $\rho_A = \frac{2}{3}|0\rangle\langle0| + \frac{1}{3}|1\rangle\langle1|$，其纯度为 $\gamma_A = (\frac{2}{3})^2 + (\frac{1}{3})^2 = \frac{5}{9}$ [@problem_id:112613]。这表明不同的[多体纠缠](@entry_id:142544)结构会导致子系统具有不同程度的混合性 [@problem_id:943427]。

### 纯度在量子动力学中的演化

#### [幺正演化](@entry_id:145020)

对于一个与外界隔离的封闭量子系统，其时间演化由一个幺正算符 $U$ 描述：$\rho(t) = U \rho(0) U^\dagger$。在这种情况下，系统的纯度是守恒的。这是因为迹的循环不变性 [@problem_id:1419413]：
$$
\gamma(t) = \text{Tr}(\rho(t)^2) = \text{Tr}((U\rho U^\dagger)(U\rho U^\dagger)) = \text{Tr}(U\rho^2 U^\dagger) = \text{Tr}(\rho^2 U^\dagger U) = \text{Tr}(\rho^2) = \gamma(0)
$$
因此，[幺正演化](@entry_id:145020)（例如由系统[哈密顿量](@entry_id:172864)驱动的演化）不会改变[态的纯度](@entry_id:185476)。纯态将始终保持[纯态](@entry_id:141688)，混合态的混合程度也保持不变。

#### 非[幺正演化](@entry_id:145020)与[退相干](@entry_id:145157)

当一个量子[系统与环境](@entry_id:142270)发生相互作用时，它就变成了一个[开放量子系统](@entry_id:138632)，其演化不再是幺正的。这种相互作用通常会导致**退相干**，即系统量子相干性的丢失，表现为纯度的降低。这种演化可以用**量子信道**（Quantum Channel）或**[克劳斯算符](@entry_id:144882)（Kraus operators）**来描述：
$$
\rho_{out} = \mathcal{E}(\rho_{in}) = \sum_k E_k \rho_{in} E_k^\dagger
$$
其中[克劳斯算符](@entry_id:144882)满足 $\sum_k E_k^\dagger E_k = I$。

**示例1：[振幅阻尼信道](@entry_id:141880)（Amplitude Damping）**
这个信道模拟了[能量弛豫](@entry_id:136820)过程，例如一个[激发态](@entry_id:261453)原子通过发射[光子](@entry_id:145192)回到[基态](@entry_id:150928)。对于一个初始处于 $|+\rangle$ 态的[量子比特](@entry_id:137928)，其密度矩阵为 $\rho_{in} = \frac{1}{2}\begin{pmatrix} 1  1 \\ 1  1 \end{pmatrix}$。经过衰减概率为 $\gamma$ 的[振幅阻尼信道](@entry_id:141880)后，其纯度会下降。演化后的纯度为 $P(t) = 1 - \frac{\gamma}{2} + \frac{\gamma^2}{2}$ [@problem_id:112516]。当 $\gamma$ 从0增加到1时，纯度从1单调下降到 $1/2$。

**示例2：[相位阻尼](@entry_id:147888)/退相（Phase Dephasing）**
这个过程描述了系统相位信息的丢失，而没有能量交换。它主要影响[密度矩阵](@entry_id:139892)的非对角元素（相干项）。例如，一个初始处于 $|+\rangle$ 态的[量子比特](@entry_id:137928)，在速率为 $\Gamma$ 的[纯退相干](@entry_id:204036)过程中，其非对角元素按指数衰减 $\rho_{01}(t) = \rho_{01}(0) e^{-2\Gamma t}$。其纯度随时间的演化为 [@problem_id:112517]：
$$
P(t) = \frac{1 + e^{-4\Gamma t}}{2}
$$
当 $t \to \infty$ 时，[相干性](@entry_id:268953)完全丢失，纯度从1下降到 $1/2$，系统趋向于一个对角混合态。

[退相干](@entry_id:145157)对纯度的影响程度，取决于初始态所包含的相干性。例如，一个[量子比特](@entry_id:137928)先绕y轴旋转角度 $\theta$ 产生[相干性](@entry_id:268953)，然后再通过一个[相位阻尼](@entry_id:147888)信道。最终的纯度为 $\mathcal{P} = 1 - \frac{\gamma}{2}\sin^2(\theta)$ [@problem_id:112490]。这表明，只有当初始态存在[相干性](@entry_id:268953)时（$\sin(\theta) \neq 0$），[相位阻尼](@entry_id:147888)才会导致纯度下降。

### 与其他概念的联系

#### 纯度与[冯·诺依曼熵](@entry_id:143216)

**[冯·诺依曼熵](@entry_id:143216)**是另一个量化[量子态](@entry_id:146142)混合程度的重要工具，定义为 $S(\rho) = -\text{Tr}(\rho \ln\rho) = -\sum_i \lambda_i \ln\lambda_i$。它与纯度是互补的度量。两者之间存在单调的反比关系：**纯度越高的态，其[冯·诺依曼熵](@entry_id:143216)越低** [@problem_id:2110597]。
*   纯态：$\gamma=1 \iff S=0$ (无不确定性)。
*   [最大混合态](@entry_id:137775)：$\gamma=1/d \iff S=\ln(d)$ (最大不确定性)。

对于给定的纯度值，可以唯一确定其熵值（反之亦然，在固定维度下）。因此，比较两个[态的纯度](@entry_id:185476)，就等同于比较它们的熵。

#### 相空间中的纯度

在量子光学的语境下，[量子态](@entry_id:146142)可以用相空间中的[准概率分布](@entry_id:203668)来表示，例如**[维格纳函数](@entry_id:153092)** $W(q,p)$。纯度与[维格纳函数](@entry_id:153092)的积分有着直接的联系 [@problem_id:653422]：
$$
\mathcal{P} = 2\pi\hbar \int_{-\infty}^{\infty} dq \int_{-\infty}^{\infty} dp \, [W(q, p)]^2
$$
这个关系表明，[维格纳函数](@entry_id:153092)在相空间中[分布](@entry_id:182848)越“尖锐”或越集中，其纯度就越高。对于[纯态](@entry_id:141688)，[维格纳函数](@entry_id:153092)可以取负值，这正是其非经典性的体现。而对于混合态，[维格纳函数](@entry_id:153092)则趋于平滑和延展。

#### 随机[态的纯度](@entry_id:185476)

在研究复杂[多体系统](@entry_id:144006)时，考虑从整个希尔伯特空间中随机抽取的“典型”纯态的性质，是非常有启发性的。根据[哈尔测度](@entry_id:142417)（Haar measure）随机选择一个二体系统 $A \otimes B$（维度为 $d_A \times d_B$）的[纯态](@entry_id:141688)，其子系统 $A$ 的平均纯度为 [@problem_id:112521]：
$$
\langle\gamma_A\rangle = \frac{d_A + d_B}{d_A d_B + 1}
$$
这个结果（佩奇定理的推论）表明，对于一个大的环境（$d_B \gg d_A$），子系统 $A$ 的状态将非常接近[最大混合态](@entry_id:137775)（$\langle\gamma_A\rangle \approx 1/d_A$）。这为理解[量子热化](@entry_id:144321)和[黑洞信息悖论](@entry_id:140140)等前沿问题提供了深刻的见解。

总之，纯度是一个简单而深刻的概念。它不仅为量化[量子态](@entry_id:146142)的混合性提供了一个可计算的标度，而且将经典混合、量子纠缠和[退相干](@entry_id:145157)等核心物理过程联系在一起，成为探索和理解量子世界不可或缺的工具。