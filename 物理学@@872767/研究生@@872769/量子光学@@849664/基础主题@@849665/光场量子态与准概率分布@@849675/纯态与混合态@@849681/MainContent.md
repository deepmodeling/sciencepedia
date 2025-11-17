## 引言
在量子世界中，一个系统的状态是我们对其进行描述和预测的基石。在理想情况下，一个完全孤立的量子系统可以由一个被称为“态矢量”的数学对象完美描述，这种状态即为**[纯态](@entry_id:141688)**。然而，现实世界中的量子系统并非孤岛，它们不可避免地与周围环境相互作用，或者我们对它们的制备过程仅有不完全的统计知识。在这些更为普遍的情境下，单一的态矢量不再足以描绘系统的全部面貌，从而引出了**混合态**的概念。区分纯态与[混合态](@entry_id:141568)不仅是理论上的必要，更是理解[量子退相干](@entry_id:145210)、[量子测量](@entry_id:272490)以及[量子信息处理](@entry_id:158111)等核心问题的关键。

本文旨在系统性地阐明[纯态](@entry_id:141688)与[混合态](@entry_id:141568)的本质区别。我们将引入一个更为普适的数学框架——[密度算符](@entry_id:138151)，来统一描述这两种状态，并揭示它们在物理性质上的深刻差异。

## 原理与机制

在量子力学中，一个孤立系统的状态可以用希尔伯特空间中的一个矢量（态矢量）$|\psi\rangle$ 来完全描述。这种由单一态矢量描述的态被称为**纯态 (pure state)**。然而，在许多现实情境中，我们可能无法用一个单一的态矢量来描述系统。例如，系统可能与环境发生了纠缠，或者我们对系统的制备过程只有不完全的经典统计知识。在这些情况下，我们需要一个更普适的数学工具来描述[量子态](@entry_id:146142)——**[密度算符](@entry_id:138151) (density operator)** 或**密度矩阵 (density matrix)**，用符号 $\rho$ 表示。能够用[密度算符](@entry_id:138151)描述，但无法用单一态矢量描述的态，被称为**[混合态](@entry_id:141568) (mixed state)**。本章将深入探讨纯态与混合态的根本区别、它们的数学表述、物理起源以及实验上的区分方法。

### [密度算符](@entry_id:138151)：[量子态](@entry_id:146142)的通用语言

为了理解[混合态](@entry_id:141568)的概念，我们首先将纯态也用[密度算符](@entry_id:138151)的语言来表述。对于一个处于[纯态](@entry_id:141688) $|\psi\rangle$ 的系统，其[密度算符](@entry_id:138151)定义为该态到自身的[投影算符](@entry_id:154142)：
$$
\rho = |\psi\rangle\langle\psi|
$$
这个算符包含了态矢量 $|\psi\rangle$ 的所有信息。例如，任意一个可观测量 $A$ 在该态下的[期望值](@entry_id:153208)可以写作 $\langle A \rangle = \langle\psi|A|\psi\rangle$。利用迹（Trace）的循环不变性（$\text{Tr}(XYZ) = \text{Tr}(ZXY)$），我们也可以用[密度算符](@entry_id:138151)计算这个[期望值](@entry_id:153208)：
$$
\langle A \rangle = \text{Tr}(\rho A)
$$
这种通过迹运算计算[期望值](@entry_id:153208)的方式对于所有[量子态](@entry_id:146142)（包括纯态和[混合态](@entry_id:141568)）都是通用的。

现在，设想一个更复杂的情形：一个量子系统有 $p_1$ 的概率处于[纯态](@entry_id:141688) $|\psi_1\rangle$，有 $p_2$ 的概率处于纯态 $|\psi_2\rangle$，以此类推，其中 $\sum_i p_i = 1$。这描述了一个**[统计系综](@entry_id:149738) (statistical ensemble)**。这其中的不确定性是经典的，源于我们对制备过程的无知。这个系综的整体[量子态](@entry_id:146142)，即[混合态](@entry_id:141568)，由其[密度算符](@entry_id:138151)描述，它是各个纯[态[密](@entry_id:147894)度算符](@entry_id:138151)的加权平均：
$$
\rho = \sum_i p_i |\psi_i\rangle\langle\psi_i|
$$
这个表达式是[量子态](@entry_id:146142)最普适的描述。无论是纯态还是混合态，其[密度算符](@entry_id:138151)都必须满足三个基本性质：
1.  **[厄米性](@entry_id:141899) (Hermiticity)**: $\rho = \rho^\dagger$。这保证了可观测量的[期望值](@entry_id:153208)为实数。
2.  **归一化 (Unit Trace)**: $\text{Tr}(\rho) = 1$。这反映了所有可能性的总概率为1。
3.  **正半定性 (Positive-semidefiniteness)**: 对于任意的态矢量 $|\phi\rangle$，$\langle\phi|\rho|\phi\rangle \ge 0$。这意味着 $\rho$ 的所有[本征值](@entry_id:154894)都必须是非负的。

正半定性条件对[密度算符](@entry_id:138151)的形式施加了强大的约束。例如，考虑一个由实参数 $a$ 描述的二维系统（[量子比特](@entry_id:137928)）的状态 $\rho = \frac{1}{2}(I + a \sigma_z)$，其中 $I$ 是[单位矩阵](@entry_id:156724)，$\sigma_z$ 是泡利[Z矩阵](@entry_id:178741)。为了使 $\rho$ 是一个合法的物理状态，它的[本征值](@entry_id:154894)必须非负。该[密度矩阵](@entry_id:139892)是对角的，其[本征值](@entry_id:154894)为 $\frac{1+a}{2}$ 和 $\frac{1-a}{2}$。正半定性要求 $\frac{1+a}{2} \ge 0$ 和 $\frac{1-a}{2} \ge 0$，这等价于 $-1 \le a \le 1$。

[密度算符](@entry_id:138151)的强大之处在于，它封装了对一个量子系统进行任何可能测量所能获得的全部统计信息。如果两种截然不同的制备过程产生了相同的[密度矩阵](@entry_id:139892)，那么这两个系综在实验上是完全无法区分的。考虑一个例子，过程A制备了一个系综，其中粒子有 $p$ 的概率自旋沿z轴向上 ($|+z\rangle$)，有 $1-p$ 的概率自旋向下 ( $|-z\rangle$ )。其密度矩阵为 $\rho_A = p |+z\rangle\langle+z| + (1-p)|-z\rangle\langle-z|$。过程B制备了另一个系综，其中粒子有 $p$ 的概率自旋沿x轴向上 ($|+x\rangle$)，有 $1-p$ 的概率自旋向下 ($|-x\rangle$)。其密度矩阵为 $\rho_B = p |+x\rangle\langle+x| + (1-p)|-x\rangle\langle-x|$。当 $p=0.5$ 时，尽管制备基底完全不同，但计算表明 $\rho_A = \rho_B = \frac{1}{2}I$，其中 $I$ 是单位矩阵。这个态被称为**[最大混合态](@entry_id:137775) (maximally mixed state)**，它代表了我们对系统状态的“最大无知”。由于它们的[密度矩阵](@entry_id:139892)相同，这两种制备方法产生的系综是物理上不可区分的。

### 度量混合度：纯度与布洛赫球

[纯态](@entry_id:141688)和[混合态](@entry_id:141568)之间的一个关键区别在于**[量子相干性](@entry_id:143031) (quantum coherence)** 的存在。在纯态叠加 $|\psi\rangle = c_1 |\phi_1\rangle + c_2 |\phi_2\rangle$ 中，系数 $c_1$ 和 $c_2$ 之间的相对相位是固定的，这导致了干涉效应。而在[混合态](@entry_id:141568) $\rho = p_1 |\phi_1\rangle\langle\phi_1| + p_2 |\phi_2\rangle\langle\phi_2|$ 中，不存在确定的相位关系，相干性丢失了。

为了量化一个态的混合程度，我们引入**纯度 (purity)** 的概念，定义为 $\gamma = \text{Tr}(\rho^2)$。
对于一个[纯态](@entry_id:141688) $\rho = |\psi\rangle\langle\psi|$，我们有 $\rho^2 = (|\psi\rangle\langle\psi|)(|\psi\rangle\langle\psi|) = |\psi\rangle(\langle\psi|\psi\rangle)\langle\psi| = |\psi\rangle\langle\psi| = \rho$。因此，纯[态的纯度](@entry_id:185476)为 $\gamma = \text{Tr}(\rho) = 1$。可以证明，对于任何混合态，其纯度都满足 $\gamma  1$。纯度的最小值取决于希尔伯特空间的维度 $d$，对于[最大混合态](@entry_id:137775) $\rho = \frac{1}{d}I$，其纯度为 $\gamma = \text{Tr}((\frac{1}{d}I)^2) = \frac{1}{d^2}\text{Tr}(I) = \frac{d}{d^2} = \frac{1}{d}$。

对于一个[量子比特](@entry_id:137928)（$d=2$），其状态可以用一个三维实向量 $\vec{r}$（称为**布洛赫向量 (Bloch vector)**）进行几何可视化，其密度矩阵可以写为：
$$
\rho = \frac{1}{2}(I + \vec{r} \cdot \vec{\sigma})
$$
其中 $\vec{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$ 是[泡利矩阵](@entry_id:139493)向量。利用泡利矩阵的性质 $(\vec{r}\cdot\vec{\sigma})^2 = |\vec{r}|^2 I$，我们可以将纯度直接与布洛赫向量的模长 $|\vec{r}|$ 联系起来。
$$
\rho^2 = \frac{1}{4}(I + 2\vec{r}\cdot\vec{\sigma} + (\vec{r}\cdot\vec{\sigma})^2) = \frac{1}{4}((1+|\vec{r}|^2)I + 2\vec{r}\cdot\vec{\sigma})
$$
取迹后，利用 $\text{Tr}(I)=2$ 和 $\text{Tr}(\sigma_i)=0$，我们得到一个优美的关系：
$$
\gamma = \text{Tr}(\rho^2) = \frac{1}{4}( (1+|\vec{r}|^2)\text{Tr}(I) ) = \frac{1+|\vec{r}|^2}{2}
$$
这个公式揭示了深刻的几何图像。如前所述，密度矩阵的正半定性要求其[本征值](@entry_id:154894) $\lambda_\pm = \frac{1}{2}(1 \pm |\vec{r}|)$ 非负，这等价于 $|\vec{r}| \le 1$。因此，所有合法的单[量子比特](@entry_id:137928)态都对应于三维空间中一个半径为1的实心球内的点，这个球被称为**布洛赫球 (Bloch ball)**。
-   **纯态**：纯[态的纯度](@entry_id:185476) $\gamma = 1$，这意味着 $\frac{1+|\vec{r}|^2}{2} = 1$，即 $|\vec{r}|=1$。因此，所有纯态都位于**布洛赫球的表面**，这个球面被称为**布洛赫球层 (Bloch sphere)**。
-   **混合态**：混合[态的纯度](@entry_id:185476) $\gamma  1$，这意味着 $|\vec{r}|  1$。因此，所有[混合态](@entry_id:141568)都位于**布洛赫球的内部**。
-   **[最大混合态](@entry_id:137775)**：当 $\vec{r} = \vec{0}$ 时，我们得到 $\rho = \frac{1}{2}I$，其纯度达到最小值 $\gamma = 1/2$。这对应于**布洛赫球的球心**。

### 纯态与[混合态](@entry_id:141568)的操作区分

尽管[纯态](@entry_id:141688)和混合态在数学上和概念上有所不同，但在实验上区分它们需要仔细设计测量方案。一个常见的误区是认为只要测量某个可观测量的[期望值](@entry_id:153208)就能区分它们。事实并非如此。例如，考虑纯态 $|+\rangle = \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle)$ 和[最大混合态](@entry_id:137775) $\rho_M = \frac{1}{2}I$。对这两个态测量 $\sigma_z$ 的[期望值](@entry_id:153208)，我们得到 $\langle\sigma_z\rangle_P = \langle+|\sigma_z|+\rangle = 0$ 和 $\langle\sigma_z\rangle_M = \text{Tr}(\frac{1}{2}I \sigma_z) = 0$。[期望值](@entry_id:153208)完全相同。

真正的区别在于[相干性](@entry_id:268953)，它体现在不同测量基下的测量结果[统计分布](@entry_id:182030)中。

一种区分方法是**选择合适的测量基**。假设一位科学家Alice面临一个任务：判断一个设备是持续制备纯态 $|-\rangle = \frac{1}{\sqrt{2}}(|0\rangle - |1\rangle)$（模式P），还是制备一个 $|0\rangle$ 和 $|1\rangle$ 的50/50经典[混合态](@entry_id:141568)（模式M），即[最大混合态](@entry_id:137775) $\frac{1}{2}I$。
-   如果在计算基 $\{|0\rangle, |1\rangle\}$ 中进行测量，对于模式P，得到 $|0\rangle$ 和 $|1\rangle$ 的概率都是 $|\frac{1}{\sqrt{2}}|^2=0.5$。对于模式M，根据定义，概率也是0.5。因此，在这个基下，两种模式的测量统计完全相同，无法区分。
-   然而，如果Alice在哈达玛基 $\{|+\rangle, |-\rangle\}$ 中进行测量，情况就大不相同了。对于模式P，系统本就处于[纯态](@entry_id:141688) $|-\rangle$，所以每次测量都会确定性地得到结果 $|-\rangle$，概率为1。对于模式M，由于 $\rho_M = \frac{1}{2}I$，在任何正交基下测量，得到各个结果的概率都是均等的0.5。因此，在哈达玛基下测量，会得到 $|+\rangle$ 和 $|-\rangle$ 各一半的概率。通过比较测量结果的统计分布，Alice可以明确地分辨出这两种状态。

另一种方法是**比较测量结果的[方差](@entry_id:200758)**。[方差](@entry_id:200758) $\text{Var}(A) = \langle A^2 \rangle - \langle A \rangle^2$ 度量了测量结果的离散程度。再次考虑[纯态](@entry_id:141688) $|+\rangle$ 和[最大混合态](@entry_id:137775) $\frac{1}{2}I$。我们测量 $\sigma_x$ 算符。
-   对于[纯态](@entry_id:141688) $|+\rangle$，它是 $\sigma_x$ 的本征态，[本征值](@entry_id:154894)为+1。因此，每次测量 $\sigma_x$ 都会确定性地得到+1。[期望值](@entry_id:153208) $\langle\sigma_x\rangle_P = 1$，[方差](@entry_id:200758) $\text{Var}_P(\sigma_x) = \langle\sigma_x^2\rangle_P - \langle\sigma_x\rangle_P^2 = \langle I \rangle_P - 1^2 = 1 - 1 = 0$。[方差](@entry_id:200758)为零意味着测量结果没有任何不确定性。
-   对于[最大混合态](@entry_id:137775) $\rho_M = \frac{1}{2}I$，[期望值](@entry_id:153208) $\langle\sigma_x\rangle_M = \text{Tr}(\frac{1}{2}I\sigma_x) = 0$。[方差](@entry_id:200758) $\text{Var}_M(\sigma_x) = \langle\sigma_x^2\rangle_M - \langle\sigma_x\rangle_M^2 = \text{Tr}(\frac{1}{2}I^2) - 0^2 = 1$。[方差](@entry_id:200758)为1（对于[泡利算符](@entry_id:144061)是最大可能值）意味着测量结果是完全随机的（+1和-1各一半概率）。
通过测量 $\sigma_x$ 的[方差](@entry_id:200758)，我们可以毫不含糊地区分这两种状态。

### 混合态的动力学与起源

既然我们理解了纯态和混合态的区别，一个自然的问题是：[混合态](@entry_id:141568)从何而来？以及它们的混合程度会如何随时间演化？

对于一个与外界完全隔离的**封闭量子系统**，其时间演化由薛定谔方程决定，是幺正的 (unitary)。[密度算符](@entry_id:138151)的演化遵循**冯·诺伊曼方程** $\frac{d\rho}{dt} = -\frac{i}{\hbar}[H, \rho]$，其解为 $\rho(t) = U(t)\rho(0)U^\dagger(t)$，其中 $U(t) = \exp(-iHt/\hbar)$ 是[时间演化算符](@entry_id:196774)。在这种[幺正演化](@entry_id:145020)下，一个[态的纯度](@entry_id:185476)是**守恒**的。
$$
\gamma(t) = \text{Tr}(\rho(t)^2) = \text{Tr}(U(t)\rho(0)U^\dagger(t)U(t)\rho(0)U^\dagger(t))
$$
利用 $U^\dagger U = I$ 和迹的循环不变性，上式变为：
$$
\gamma(t) = \text{Tr}(U(t)\rho(0)^2 U^\dagger(t)) = \text{Tr}(\rho(0)^2 U^\dagger(t)U(t)) = \text{Tr}(\rho(0)^2) = \gamma(0)
$$
这意味着一个孤立系统如果初始是纯态，它将永远保持纯态；如果初始是[混合态](@entry_id:141568)，它的混合程度（纯度）将保持不变。

那么，混合态的出现以及纯态向混合态的转变，必然涉及到**[开放量子系统](@entry_id:138632)**，即系统与外部世界（环境）的相互作用。混合态主要有两大来源：

1.  **测量引起的退相干**：[量子测量](@entry_id:272490)过程是纯态转变为混合态的一个典型机制。假设一个系统处于[纯态](@entry_id:141688) $|\psi\rangle = \frac{3}{5}|\uparrow\rangle + \frac{4}{5}|\downarrow\rangle$。这个[态的纯度](@entry_id:185476)为1。现在，我们对该系统进行一次 $S_z$ 的投影测量。根据[玻恩定则](@entry_id:154470)，测量结果为 $|\uparrow\rangle$ 的概率是 $p_\uparrow = (3/5)^2 = 9/25$，结果为 $|\downarrow\rangle$ 的概率是 $p_\downarrow = (4/5)^2 = 16/25$。如果一个观察者进行了测量但**不知道**具体是哪个结果，那么从他的视角来看，测量后的系综只能被描述为一个[混合态](@entry_id:141568)：
    $$
    \rho_{\text{final}} = p_\uparrow |\uparrow\rangle\langle\uparrow| + p_\downarrow |\downarrow\rangle\langle\downarrow| = \frac{9}{25}|\uparrow\rangle\langle\uparrow| + \frac{16}{25}|\downarrow\rangle\langle\downarrow|
    $$
    这个末[态的纯度](@entry_id:185476)为 $\text{Tr}(\rho_{\text{final}}^2) = (9/25)^2 + (16/25)^2 = 337/625$，远小于1。初始的[相干叠加](@entry_id:170209)态 $|\psi\rangle$ 在测量后（且结果未知时）退化为了一个非相干的经典统计混合物。这个过程被称为**退相干 (decoherence)**。

2.  **与环境的纠缠和部分迹**：这是混合态最普遍的来源。任何现实的量子系统 A 都不可避免地与周围的环境 B 发生相互作用并产生**[量子纠缠](@entry_id:136576) (quantum entanglement)**。即使整个“系统+环境”的复合系统 AB 处于一个巨大的[纯态](@entry_id:141688) $|\Psi_{AB}\rangle$ 中，如果我们只对子系统 A 感兴趣（因为我们无法测量整个宇宙），那么 A 的状态通常是混合态。描述子系统 A 状态的数学工具是**[约化密度矩阵](@entry_id:146315) (reduced density matrix)**，通过对环境 B 的自由度求**部分迹 (partial trace)** 得到：
    $$
    \rho_A = \text{Tr}_B(|\Psi_{AB}\rangle\langle\Psi_{AB}|)
    $$
    只要 $|\Psi_{AB}\rangle$ 是一个[纠缠态](@entry_id:152310)，那么 $\rho_A$ 就必然是一个[混合态](@entry_id:141568)。这揭示了一个深刻的观点：一个局域观察者看到的“混合”或“经典随机性”，其根源可能在于该系统与外部世界的量子纠缠。

反过来，这个观点也意味着任何[混合态](@entry_id:141568)都可以被视为某个更大系统中的[纯态](@entry_id:141688)的一部分。给定任意一个混合态 $\rho_A$，我们总能虚构一个[辅助系统](@entry_id:142219) B，并在这个复合系统 AB 上构造一个纯态 $|\Psi_{AB}\rangle$，使得 $\text{Tr}_B(|\Psi_{AB}\rangle\langle\Psi_{AB}|) = \rho_A$。这个过程被称为**纯化 (purification)**。例如，通过对 $\rho_A$ 进行[谱分解](@entry_id:173707) $\rho_A = \sum_i \lambda_i |u_i\rangle\langle u_i|$，一个标准的纯化形式是 $|\Psi_{AB}\rangle = \sum_i \sqrt{\lambda_i} |u_i\rangle_A |i\rangle_B$，其中 $\{|i\rangle_B\}$ 是[辅助系统](@entry_id:142219)B的一组标准正交基。纯化在[量子信息](@entry_id:137721)理论中是一个极其有力的概念工具。

### 应用实例：非偏振光的滤波

让我们通过一个光学中的具体例子来巩固这些概念。一束**非偏振光 (unpolarized light)** 是[光子](@entry_id:145192)[偏振态](@entry_id:175130)完全随机的统计混合。在量子描述中，这对应于[最大混合态](@entry_id:137775)。在水平/垂直偏振基 $\{|H\rangle, |V\rangle\}$ 中，其[密度矩阵](@entry_id:139892)为：
$$
\rho_{\text{unpolarized}} = \frac{1}{2}(|H\rangle\langle H| + |V\rangle\langle V|) = \frac{1}{2}I
$$
这是一个纯度为 $1/2$ 的混合态。

现在，让这束光通过一个[线性偏振片](@entry_id:195509)，该[偏振片](@entry_id:269119)只允许与水平方向成 $45^\circ$ 角的偏振光通过。这个[偏振态](@entry_id:175130)是 $|45^\circ\rangle = \frac{1}{\sqrt{2}}(|H\rangle + |V\rangle)$。[偏振片](@entry_id:269119)的作用相当于一个量子滤波器，其数学描述是一个[投影算符](@entry_id:154142) $P = |45^\circ\rangle\langle 45^\circ|$。当一个系综 $\rho_{in}$ 通过这个滤波器后，透射出的子系综的状态变为：
$$
\rho_{out} = \frac{P \rho_{in} P^\dagger}{\text{Tr}(P \rho_{in} P^\dagger)}
$$
将 $\rho_{in} = \frac{1}{2}I$ 和 $P^\dagger=P$ 代入，我们得到：
$$
\text{分子： } P(\frac{1}{2}I)P = \frac{1}{2}P^2 = \frac{1}{2}P
$$
$$
\text{分母： } \text{Tr}(P(\frac{1}{2}I)P) = \text{Tr}(\frac{1}{2}P^2) = \frac{1}{2}\text{Tr}(P) = \frac{1}{2} \times 1 = \frac{1}{2}
$$
因此，出射光的状态为：
$$
\rho_{out} = \frac{\frac{1}{2}P}{\frac{1}{2}} = P = |45^\circ\rangle\langle 45^\circ|
$$
这个结果非常直观：最初完全随机的、处于[最大混合态](@entry_id:137775)的[非偏振光](@entry_id:176162)，在通过一个理想的 $45^\circ$ 偏振片后，被“过滤”成了处于 $|45^\circ\rangle$ 的纯态。这个过程清晰地展示了物理相互作用（在此是滤波）如何将一个混合态转变为一个纯态，这本质上是一次选择性的量子测量。