## 引言
在量子力学的宏伟殿堂中，[本征值](@entry_id:154894)与本征矢是连接抽象数学形式与具体物理现实的核心支柱。它们不仅是理论的基石，更是我们理解和预测微观世界行为的根本工具。初看起来，这一概念可能显得数学化且难以捉摸，但它所解决的，正是量子理论最核心的问题：当我们测量一个物理量时，会得到什么结果？系统又将如何演化？本征理论为这些问题提供了精确而深刻的答案。

本文旨在系统地揭开[本征值](@entry_id:154894)与本征矢的神秘面纱，展示其在量子力学及更广阔科学领域中的强大威力。我们将通过三个章节的探索，带领读者从基本原理走向前沿应用：

*   在**“原理与机制”**一章中，我们将深入量子力学的形式体系，阐明[本征值方程](@entry_id:192306)作为基本假设的物理意义，探讨厄米算符与幺正算符的关键性质，并揭示简并、对易性与对称性之间的内在联系。
*   在**“应用与交叉学科联系”**一章中，我们将走出纯粹的量子世界，探索本征分析如何在化学、工程学、数据科学乃至经济学中作为一种统一的语言，用于揭示[振动](@entry_id:267781)模式、[数据结构](@entry_id:262134)和系统[稳态](@entry_id:182458)等多样化问题背后的本质规律。
*   最后，在**“动手实践”**部分，我们将通过一系列精心设计的计算练习，引导你亲手求解[本征问题](@entry_id:748835)，将抽象的理论知识转化为具体的分析技能。

通过本次学习，您将掌握一个不仅能解释量子现象，更能洞察各类复杂系统内在秩序的强大思维工具。

## 原理与机制

在量子力学的形式体系中，物理系统的状态由[希尔伯特空间](@entry_id:261193)中的矢量描述，而可观测的物理量则由作用于该空间上的算符表示。[本征值](@entry_id:154894)与本征矢量的概念，是连接这两个抽象数学实体与具体物理实在（即测量结果）的核心桥梁。本章将深入探讨[本征值方程](@entry_id:192306)的原理，阐明其在量子测量、系统演化以及[对称性分析](@entry_id:174795)中的关键机制。

### [本征值方程](@entry_id:192306)：一个基本假设

量子力学的一个核心假设是，对于代表某个可观测量 $Q$ 的算符 $\hat{Q}$，其一系列特殊的[量子态](@entry_id:146142)，称为**[本征态](@entry_id:149904) (eigenstates)**，在该算符作用下保持其方向不变，仅被乘以一个标量因子。这个关系用**[本征值方程](@entry_id:192306) (eigenvalue equation)** 来表达：

$$
\hat{Q}|\psi\rangle = q|\psi\rangle
$$

在这里，$|\psi\rangle$ 是算符 $\hat{Q}$ 的一个**本征矢 (eigenvector)** 或本征态，$q$ 是一个标量，称为与本征态 $|\psi\rangle$ 对应的**[本征值](@entry_id:154894) (eigenvalue)**。从物理上看，本征态代表了这样一种特殊状态：在该状态下，可观测量 $Q$ 具有一个确定的、无涨落的值。

这个方程的直接物理意义通过**测量假设**得以体现：

1.  对一个物理系统测量[可观测量](@entry_id:267133) $Q$，唯一可能得到的测量结果必然是算符 $\hat{Q}$ 的某个[本征值](@entry_id:154894)。
2.  如果在测量瞬时，系统的状态恰好是 $\hat{Q}$ 的一个本征态 $|\psi_n\rangle$，其对应的[本征值](@entry_id:154894)为 $q_n$，那么对 $Q$ 的测量将以 100% 的概率得到结果 $q_n$。该状态被称为 $Q$ 的**定态**。

然而，一个系统通常处于多个[本征态](@entry_id:149904)的**叠加态 (superposition state)**。若系统状态为 $|\phi\rangle$，它可以展开为算符 $\hat{Q}$ 的一组完备正交的[本征态](@entry_id:149904) $|\psi_n\rangle$ 的线性组合：

$$
|\phi\rangle = \sum_n c_n |\psi_n\rangle
$$

其中 $c_n = \langle\psi_n|\phi\rangle$ 是将状态 $|\phi\rangle$ 投影到[本征态](@entry_id:149904) $|\psi_n\rangle$ 上的复数振幅。根据**玻恩法则 (Born rule)**，此时测量可观测量 $Q$ 得到结果 $q_n$ 的概率 $P(q_n)$ 为：

$$
P(q_n) = |\langle\psi_n|\phi\rangle|^2 = |c_n|^2
$$

所有概率之和为1，即 $\sum_n |c_n|^2 = 1$，这要求态矢量 $|\phi\rangle$ 是归一化的，即 $\langle\phi|\phi\rangle = 1$。

让我们通过一个具体的例子来阐明这些原理。考虑一个[量子比特](@entry_id:137928)，其计算[基矢](@entry_id:199546)为正交归一的 $\{|0\rangle, |1\rangle\}$。一个可观测量由泡利-Z算符 $\hat{Z}$ 表示，其定义为 $\hat{Z}|0\rangle = +1|0\rangle$ 和 $\hat{Z}|1\rangle = -1|1\rangle$。这表明 $|0\rangle$ 和 $|1\rangle$ 是 $\hat{Z}$ 的[本征态](@entry_id:149904)，对应的[本征值](@entry_id:154894)分别为 $+1$ 和 $-1$。因此，对该可观测量的一次测量，可能的结果只能是 $+1$ 或 $-1$。

现在，假设系统被制备在状态 $|\psi\rangle = C(2|0\rangle - |1\rangle)$，其中 $C$ 是一个正的实数[归一化常数](@entry_id:752675) [@problem_id:2089980]。首先，我们根据[归一化条件](@entry_id:156486) $\langle\psi|\psi\rangle = 1$ 来确定 $C$。
$$
\langle\psi|\psi\rangle = |C|^2 (2\langle 0| - \langle 1|)(2|0\rangle - |1\rangle) = |C|^2 (4\langle 0|0\rangle - 2\langle 0|1\rangle - 2\langle 1|0\rangle + \langle 1|1\rangle) = 5|C|^2 = 1
$$
由此解得 $C = 1/\sqrt{5}$。归一化后的状态是 $|\psi\rangle = \frac{1}{\sqrt{5}}(2|0\rangle - |1\rangle)$。

根据玻恩法则，测量 $\hat{Z}$ 得到[本征值](@entry_id:154894) $+1$ (对应本征态 $|0\rangle$) 的概率为：
$$
P(+1) = |\langle 0|\psi\rangle|^2 = \left| \frac{1}{\sqrt{5}} \langle 0|(2|0\rangle - |1\rangle) \right|^2 = \left| \frac{2}{\sqrt{5}} \right|^2 = \frac{4}{5}
$$
同样，得到[本征值](@entry_id:154894) $-1$ (对应本征态 $|1\rangle$) 的概率为：
$$
P(-1) = |\langle 1|\psi\rangle|^2 = \left| \frac{1}{\sqrt{5}} \langle 1|(2|0\rangle - |1\rangle) \right|^2 = \left| -\frac{1}{\sqrt{5}} \right|^2 = \frac{1}{5}
$$
这清晰地展示了量子测量的概率性本质，它源于系统状态相对于测量算符的本征基的叠加。

### [本征值](@entry_id:154894)与本征矢的数学性质

为了应用[本征值方程](@entry_id:192306)，我们需要掌握如何求解它以及其解具有的普适性质。对于在[有限维向量空间](@entry_id:265491)中用[矩阵表示](@entry_id:146025)的算符，求解过程是明确的。[本征值方程](@entry_id:192306) $\hat{Q}|\psi\rangle = q|\psi\rangle$ 可以写成矩阵形式 $Q \mathbf{v} = q \mathbf{v}$，即 $(Q - qI)\mathbf{v} = 0$，其中 $I$ 是[单位矩阵](@entry_id:156724)。这个方程有非零解 $\mathbf{v}$ 的充要条件是系数矩阵的[行列式](@entry_id:142978)为零：

$$
\det(Q - qI) = 0
$$

这个方程称为**特征方程 (characteristic equation)**，解出的 $q$ 就是算符 $\hat{Q}$ 的所有[本征值](@entry_id:154894)。然后，将每个[本征值](@entry_id:154894) $q$ 代回 $(Q - qI)\mathbf{v} = 0$，即可解出对应的本征矢 $\mathbf{v}$。

#### 厄米算符：可观测量的数学表示

量子力学中，代表物理可观测量（如能量、动量、角动量）的算符必须是**[厄米算符](@entry_id:153410) (Hermitian operators)**。[厄米算符](@entry_id:153410)的定义是它等于其自身的[厄米共轭](@entry_id:191215)，即 $\hat{Q} = \hat{Q}^\dagger$，其中[厄米共轭](@entry_id:191215)（或称随算）是对矩阵进行转置并取复共轭。这个要求并非随意的数学构造，而是确保[量子理论](@entry_id:145435)与物理实在相符的关键。[厄米算符](@entry_id:153410)具有两个至关重要的性质：

1.  **厄米算符的[本征值](@entry_id:154894)是实数。**
    证明：设 $|\psi\rangle$ 是[厄米算符](@entry_id:153410) $\hat{Q}$ 的本征矢，[本征值](@entry_id:154894)为 $q$。那么 $\hat{Q}|\psi\rangle = q|\psi\rangle$。我们用 $\langle\psi|$ 从左边乘以这个方程，得到 $\langle\psi|\hat{Q}|\psi\rangle = q\langle\psi|\psi\rangle$。现在取该方程的复共轭，得到 $\langle\psi|\hat{Q}|\psi\rangle^* = q^*\langle\psi|\psi\rangle^*$。由于 $\langle\psi|\psi\rangle$ 是范数的平方，必为实数，所以 $\langle\psi|\psi\rangle^* = \langle\psi|\psi\rangle$。对于厄米算符，有 $\langle\psi|\hat{Q}|\psi\rangle^* = \langle\psi|\hat{Q}^\dagger|\psi\rangle = \langle\psi|\hat{Q}|\psi\rangle$。因此，我们有 $\langle\psi|\hat{Q}|\psi\rangle = q^*\langle\psi|\psi\rangle$。比较两个表达式，我们发现 $q\langle\psi|\psi\rangle = q^*\langle\psi|\psi\rangle$。由于 $|\psi\rangle$ 是非[零矢量](@entry_id:155273)，$\langle\psi|\psi\rangle \neq 0$，所以必须有 $q = q^*$，这证明了 $q$ 是实数。这个性质是至关重要的，因为它保证了物理测量的结果总是实数。

    作为一个反例，考虑一个非厄米算符，例如 $\hat{O} = \begin{pmatrix} 1  1 \\ -1  1 \end{pmatrix}$ [@problem_id:2089983]。其特征方程为 $(1-\lambda)^2 - (1)(-1) = (1-\lambda)^2 + 1 = 0$，解得[本征值](@entry_id:154894)为 $\lambda = 1 \pm i$。这些复数[本征值](@entry_id:154894)无法对应于任何物理可观测量的一次测量结果。

2.  **[厄米算符](@entry_id:153410)对应于不同[本征值](@entry_id:154894)的本征矢是正交的。**
    证明：设 $|\psi_1\rangle$ 和 $|\psi_2\rangle$ 是[厄米算符](@entry_id:153410) $\hat{Q}$ 的本征矢，对应不同的[本征值](@entry_id:154894) $q_1$ 和 $q_2$ ($q_1 \neq q_2$) 。我们有 $\hat{Q}|\psi_1\rangle = q_1|\psi_1\rangle$ 和 $\hat{Q}|\psi_2\rangle = q_2|\psi_2\rangle$。用 $\langle\psi_2|$ 左乘第一个方程，得到 $\langle\psi_2|\hat{Q}|\psi_1\rangle = q_1\langle\psi_2|\psi_1\rangle$。利用 $\hat{Q}$ 的[厄米性](@entry_id:141899)，我们也可以计算 $\langle\psi_2|\hat{Q}|\psi_1\rangle = \langle\hat{Q}\psi_2|\psi_1\rangle = (q_2\langle\psi_2|)|\psi_1\rangle = q_2^*\langle\psi_2|\psi_1\rangle$。由于 $q_2$ 是实数，$q_2^* = q_2$。因此我们得到 $q_1\langle\psi_2|\psi_1\rangle = q_2\langle\psi_2|\psi_1\rangle$，即 $(q_1-q_2)\langle\psi_2|\psi_1\rangle = 0$。因为我们假设 $q_1 \neq q_2$，所以必然有 $\langle\psi_2|\psi_1\rangle = 0$，这证明了两个本征矢是正交的。这个性质保证了我们可以构建一个由相互正交的[本征态](@entry_id:149904)组成的基底，这对于展开任意态和应用玻恩法则至关重要 [@problem_id:1360132]。

#### 幺正算符：演化与变换的描述

另一类重要的算符是**幺正算符 (Unitary operators)**，定义为满足 $\hat{U}^\dagger \hat{U} = \hat{U} \hat{U}^\dagger = \hat{I}$ 的算符。幺正算符在量子力学中扮演着描述系统状态演化（[时间演化算符](@entry_id:196774)）或对称性变换的角色。它们的一个关键特性是保范性，即如果 $|\psi'\rangle = \hat{U}|\psi\rangle$，那么 $\langle\psi'|\psi'\rangle = \langle\psi|\hat{U}^\dagger \hat{U}|\psi\rangle = \langle\psi|\psi\rangle$。这意味着变换或演化过程保持了总概率为1。

幺正算符的[本征值](@entry_id:154894)具有一个独特的性质：

-   **幺正算符的[本征值](@entry_id:154894)是模为1的复数。**
    证明：设 $|\psi\rangle$ 是幺正算符 $\hat{U}$ 的本征矢，[本征值](@entry_id:154894)为 $\lambda$。从 $\hat{U}|\psi\rangle = \lambda|\psi\rangle$，我们有 $\langle\psi|\hat{U}^\dagger = \lambda^*\langle\psi|$。将这两者结合，我们得到 $\langle\psi|\hat{U}^\dagger \hat{U}|\psi\rangle = (\lambda^*\langle\psi|)(\lambda|\psi\rangle) = |\lambda|^2 \langle\psi|\psi\rangle$。由于 $\hat{U}^\dagger \hat{U} = \hat{I}$，左边等于 $\langle\psi|\hat{I}|\psi\rangle = \langle\psi|\psi\rangle$。因此，我们有 $\langle\psi|\psi\rangle = |\lambda|^2 \langle\psi|\psi\rangle$。由于 $\langle\psi|\psi\rangle \neq 0$，我们必须有 $|\lambda|^2=1$，这意味着 $\lambda$ 是一个模为1的复数，可以写成 $e^{i\theta}$ 的形式。

    此外，如果 $|\psi\rangle$ 是 $\hat{U}$ 的[本征值](@entry_id:154894)为 $\lambda$ 的本征态，那么它也是其[厄米共轭](@entry_id:191215) $\hat{U}^\dagger$ 的[本征态](@entry_id:149904)。从 $\hat{U}|\psi\rangle = \lambda|\psi\rangle$ 出发，用 $\hat{U}^\dagger$ 作用于两侧，得到 $\hat{U}^\dagger \hat{U}|\psi\rangle = \lambda \hat{U}^\dagger|\psi\rangle$，即 $|\psi\rangle = \lambda \hat{U}^\dagger|\psi\rangle$。因此，$\hat{U}^\dagger|\psi\rangle = \lambda^{-1}|\psi\rangle$。由于 $|\lambda|=1$，我们有 $\lambda^{-1} = \lambda^*$。所以，$\hat{U}^\dagger|\psi\rangle = \lambda^*|\psi\rangle$。这一特性在分析由幺正算符构成的[复合算符](@entry_id:152160)时非常有用 [@problem_id:2089987]。

### [本征空间](@entry_id:147356)与简并

当一个[本征值](@entry_id:154894)对应不止一个线性无关的本征矢时，我们称这个[本征值](@entry_id:154894)是**简并的 (degenerate)**。属于同一个[本征值](@entry_id:154894) $q$ 的所有本征矢，连同[零矢量](@entry_id:155273)一起，构成一个[向量子空间](@entry_id:151815)，称为对应于[本征值](@entry_id:154894) $q$ 的**[本征空间](@entry_id:147356) (eigenspace)**。

[本征空间](@entry_id:147356)的一个关键性质是，其中任何矢量的线性组合仍然是该[本征空间](@entry_id:147356)中的矢量。这意味着，如果 $|\psi_1\rangle$ 和 $|\psi_2\rangle$ 都是算符 $\hat{Q}$ 对应于[本征值](@entry_id:154894) $q_0$ 的[本征态](@entry_id:149904)，那么它们的任意[线性组合](@entry_id:154743) $|\psi\rangle = c_1|\psi_1\rangle + c_2|\psi_2\rangle$ 也将是 $\hat{Q}$ 的[本征态](@entry_id:149904)，且具有相同的[本征值](@entry_id:154894) $q_0$ [@problem_id:2089972]。
$$
\hat{Q}|\psi\rangle = \hat{Q}(c_1|\psi_1\rangle + c_2|\psi_2\rangle) = c_1\hat{Q}|\psi_1\rangle + c_2\hat{Q}|\psi_2\rangle = c_1 q_0 |\psi_1\rangle + c_2 q_0 |\psi_2\rangle = q_0(c_1|\psi_1\rangle + c_2|\psi_2\rangle) = q_0|\psi\rangle
$$
更进一步，如果一个态是 $\hat{Q}$ 的[本征态](@entry_id:149904)，它也将是任何 $\hat{Q}$ 的函数（例如多项式）所构成的算符 $\hat{S} = f(\hat{Q})$ 的[本征态](@entry_id:149904)。例如，对于 $\hat{S} = \alpha_0 \hat{I} + \alpha_1 \hat{Q} + \alpha_2 \hat{Q}^2$，作用在 $|\psi\rangle$ 上会得到：
$$
\hat{S}|\psi\rangle = (\alpha_0 + \alpha_1 q_0 + \alpha_2 q_0^2)|\psi\rangle
$$
其[本征值](@entry_id:154894)为 $f(q_0) = \alpha_0 + \alpha_1 q_0 + \alpha_2 q_0^2$。

简并现象在物理世界中很常见。一个经典的例子是自由粒子。一个向右传播的平面波 $\psi_+(x) = C_1 e^{ikx}$ 是[动量算符](@entry_id:151743) $\hat{p}_x = -i\hbar\frac{d}{dx}$ 的本征态，其[本征值](@entry_id:154894)为 $+\hbar k$。一个向左传播的平面波 $\psi_-(x) = C_2 e^{-ikx}$ 也是 $\hat{p}_x$ 的本征态，[本征值](@entry_id:154894)为 $-\hbar k$。现在考虑一个由这两者叠加而成的态 $\psi(x) = C_1 e^{ikx} + C_2 e^{-ikx}$ [@problem_id:2089951]。由于它混合了两个具有不同动量[本征值](@entry_id:154894)的态，因此它本身不再是动量算符的本征态。

然而，让我们考察[动能算符](@entry_id:265633) $\hat{T} = \frac{\hat{p}_x^2}{2m} = -\frac{\hbar^2}{2m} \frac{d^2}{dx^2}$。
$$
\hat{T} e^{ikx} = -\frac{\hbar^2}{2m} (ik)^2 e^{ikx} = \frac{\hbar^2 k^2}{2m} e^{ikx}
$$
$$
\hat{T} e^{-ikx} = -\frac{\hbar^2}{2m} (-ik)^2 e^{-ikx} = \frac{\hbar^2 k^2}{2m} e^{-ikx}
$$
两个动量本征态虽然动量相反，但它们对应于**相同**的动能[本征值](@entry_id:154894) $E_k = \frac{\hbar^2 k^2}{2m}$。这意味着动能[本征值](@entry_id:154894)是简并的（至少是二重简并）。因此，它们的任意线性组合 $\psi(x)$ 都是[动能算符](@entry_id:265633)的本征态，具有相同的[本征值](@entry_id:154894) $E_k$：
$$
\hat{T}\psi(x) = \hat{T}(C_1 e^{ikx} + C_2 e^{-ikx}) = C_1 (\hat{T}e^{ikx}) + C_2 (\hat{T}e^{-ikx}) = \frac{\hbar^2 k^2}{2m} (C_1 e^{ikx} + C_2 e^{-ikx}) = E_k \psi(x)
$$
这个例子深刻地揭示了简并的物理意义：一个系统可以处于不同的状态（例如，向左或向右运动），但仍然拥有完全相同的某个物理量的值（例如，动能）。

### 对易性、[对称性与守恒律](@entry_id:160300)

本征态理论的威力在考察多个可观测量时表现得淋漓尽致。一个基本定理指出：**两个[厄米算符](@entry_id:153410) $\hat{A}$ 和 $\hat{B}$ 拥有一组共同的完备本征基的充要条件是它们相互对易（commute）**，即它们的对易子为零：

$$
[\hat{A}, \hat{B}] \equiv \hat{A}\hat{B} - \hat{B}\hat{A} = 0
$$

如果两个算符对易，就意味着存在一组[基矢](@entry_id:199546)，其中每个[基矢](@entry_id:199546)都是 $\hat{A}$ 和 $\hat{B}$ 的共同本征态。这在物理上意味着，可以制备一个系统状态，使得对 $A$ 和 $B$ 的测量都将得到确定的值。

反之，如果两个算符不对易，例如自旋的 $x$ 分量和 $z$ 分量的算符 $\hat{S}_x$ 和 $\hat{S}_z$，它们通常不具有共同的[本征态](@entry_id:149904)。一个 $\hat{S}_z$ 的[本征态](@entry_id:149904)（例如自旋向上态 $|\chi_+\rangle$）在 $\hat{S}_x$ 的作用下，会转变为一个不同的状态，而不再是 $\hat{S}_x$ 的[本征态](@entry_id:149904) [@problem_id:2089999]。这就是著名的**不确定性原理**的数学根源：如果两个可观测量不对易，就不可能同时精确地知道它们的值。

对易关系与系统的**对称性 (symmetries)** 紧密相连。根据[诺特定理](@entry_id:145690)的思想，在量子力学中，如果一个系统的[哈密顿量](@entry_id:172864) $\hat{H}$ 与某个算符 $\hat{Q}$ 对易，即 $[\hat{H}, \hat{Q}]=0$，那么 $\hat{Q}$ 所对应的物理量就是一个**守恒量 (conserved quantity)**。

此外，这条[对易关系](@entry_id:136780)还有一个重要推论：如果 $\hat{H}$ 的一个[能量本征值](@entry_id:144381) $E$ 是**非简并的**，那么该能量本征态也必然是与 $\hat{H}$ 对易的任何算符 $\hat{Q}$ 的[本征态](@entry_id:149904)。这是因为，如果 $|\psi_E\rangle$ 是能量为 $E$ 的[本征态](@entry_id:149904)，那么 $\hat{H}|\psi_E\rangle = E|\psi_E\rangle$。现在用 $\hat{Q}$ 作用于此状态，我们有 $\hat{Q}|\psi_E\rangle$。考察 $\hat{H}$ 对这个新状态的作用：
$$
\hat{H}(\hat{Q}|\psi_E\rangle) = \hat{H}\hat{Q}|\psi_E\rangle = \hat{Q}\hat{H}|\psi_E\rangle = \hat{Q}(E|\psi_E\rangle) = E(\hat{Q}|\psi_E\rangle)
$$
这表明 $\hat{Q}|\psi_E\rangle$ 这个状态也是能量为 $E$ 的本征态。由于我们假设 $E$ 是非简并的，这意味着所有对应于 $E$ 的[本征态](@entry_id:149904)必须是 $|\psi_E\rangle$ 的常数倍。因此，$\hat{Q}|\psi_E\rangle$ 必须与 $|\psi_E\rangle$ 成正比，即 $\hat{Q}|\psi_E\rangle = q|\psi_E\rangle$。这证明了 $|\psi_E\rangle$ 也是 $\hat{Q}$ 的本征态。

一个富有启发性的例子是考虑一个具有[轴对称](@entry_id:173333)性的[势场](@entry_id:143025)，例如 $V(x,y,z) = K \frac{z^2}{x^2+y^2+z^2} = K\cos^2\theta$ [@problem_id:2089981]。该势场绕 $z$ 轴旋转时保持不变，这意味着系统[哈密顿量](@entry_id:172864) $\hat{H}$ 与绕 $z$ 轴旋转的生成元，即角动量的 $z$ 分量算符 $\hat{L}_z$，是对易的：$[\hat{H}, \hat{L}_z]=0$。然而，该势场不具有完全的球对称性，因此 $\hat{H}$ 与总角动量平方算符 $\hat{L}^2$ 不对易：$[\hat{H}, \hat{L}^2] \neq 0$。根据上述定理，如果测量发现系统处于一个非简并的能量本征态，那么该状态也必然是 $\hat{L}_z$ 的[本征态](@entry_id:149904)。因此，紧接着对 $L_z$ 的测量将得到一个确定的值。但对 $L^2$ 的测量则不一定，因为能量本征态不一定是 $\hat{L}^2$ 的本征态。

### 在时间演化与[连续谱](@entry_id:155477)中的应用

#### [哈密顿量](@entry_id:172864)的[本征态](@entry_id:149904)：定态

在所有可观测量中，[哈密顿量](@entry_id:172864) $\hat{H}$ 的地位最为特殊，因为它决定了系统的**时间演化**。$\hat{H}$ 的[本征态](@entry_id:149904)被称为**[定态](@entry_id:137260) (stationary states)**，其[能量本征值](@entry_id:144381) $E_n$ 对应于系统可能具有的确定能量。如果一个系统在 $t=0$ 时处于一个能量本征态 $|\psi_n(0)\rangle$，那么在任意稍后时刻 $t$，其状态由薛定谔方程的解给出：

$$
|\psi_n(t)\rangle = e^{-iE_n t/\hbar} |\psi_n(0)\rangle
$$

这个表达式揭示了定态的本质：随着时间的流逝，状态矢量仅仅获得一个随时间变化的**相位因子 (phase factor)**。其模长和方向（在[希尔伯特空间](@entry_id:261193)中）保持不变。因此，对于处于[定态](@entry_id:137260)的系统，任何可观测量的[期望值](@entry_id:153208)都是不随时间改变的，$\langle\hat{Q}\rangle(t) = \langle\psi_n(t)|\hat{Q}|\psi_n(t)\rangle = \langle\psi_n(0)|\hat{Q}|\psi_n(0)\rangle$。

#### 一般态的[时间演化](@entry_id:153943)：量子动力学

然而，一个系统通常不处于定态，而是多个[能量本征态](@entry_id:152154)的叠加态。设初始状态为 $|\psi(0)\rangle = \sum_n c_n |\psi_n(0)\rangle$。由于薛定谔方程是线性的，系统的后续状态就是每个定态独立演化后的线性叠加：

$$
|\psi(t)\rangle = \sum_n c_n |\psi_n(t)\rangle = \sum_n c_n e^{-iE_n t/\hbar} |\psi_n(0)\rangle
$$

此时，不同能量本征态分量之间的**相对相位**会随时间变化，导致系统的可观测量[期望值](@entry_id:153208)发生[振荡](@entry_id:267781)，展现出非平庸的量子动力学。

一个经典的例子是[二能级系统](@entry_id:138452)中的[拉比振荡](@entry_id:137940)。考虑一个[哈密顿量](@entry_id:172864)为 $\hat{H} = \begin{pmatrix} E_0  \Delta \\ \Delta  E_0 \end{pmatrix}$ 的系统，其[基矢](@entry_id:199546)为 $|1\rangle$ 和 $|2\rangle$ [@problem_id:2089962]。如果系统在 $t=0$ 时被制备在状态 $|\psi(0)\rangle = |1\rangle$，这个状态并不是 $\hat{H}$ 的本征态。为了求解其[时间演化](@entry_id:153943)，我们必须首先求解 $\hat{H}$ 的[本征问题](@entry_id:748835)，得到能量本征态（它们是 $|1\rangle$ 和 $|2\rangle$ 的叠加态）和对应的[能量本征值](@entry_id:144381)。然后将初始态 $|1\rangle$ 在这个能量本征基下展开，让每个分量随时间独立演化，最后再将它们叠加起来得到 $|\psi(t)\rangle$。通过计算 $|\langle 2|\psi(t)\rangle|^2$，可以得到在时刻 $t$ 测量到系统处于 $|2\rangle$ 态的概率 $P_2(t)$。这个概率会随时间[振荡](@entry_id:267781)，其形式为 $P_2(t) = \sin^2(\Delta t/\hbar)$。这种从一个状态到另一个[状态的周期性](@entry_id:193569)概率转移是量子系统动力学的基本特征。

#### 连续谱：超越希尔伯特空间

我们至今讨论的都是具有**[离散谱](@entry_id:150970) (discrete spectrum)** 的算符，即它们的[本征值](@entry_id:154894)是一系列孤立的点。然而，诸如位置算符 $\hat{x}$ 和动量算符 $\hat{p}_x$ 等基本算符，其[本征值](@entry_id:154894)可以取任何实数，构成**连续谱 (continuous spectrum)**。

以一维位置算符为例，其[本征值方程](@entry_id:192306)为 $\hat{x}\psi_{x_0}(x) = x_0 \psi_{x_0}(x)$，即 $x\psi_{x_0}(x) = x_0\psi_{x_0}(x)$。这个方程的解 $\psi_{x_0}(x)$ 必须在所有 $x \neq x_0$ 的点上为零，这正是**狄拉克 $\delta$ 函数 (Dirac delta function)** $\delta(x-x_0)$ 的定义。然而，$\delta$ 函数并不是一个常规函数，而是一个[分布](@entry_id:182848)。它不属于物理态所在的[希尔伯特空间](@entry_id:261193) $L^2(\mathbb{R})$，因为它不是平方可积的。尝试对其进行归一化会发现其范数积分 $\int |\delta(x-x_0)|^2 dx$ 是发散的 [@problem_id:2090005]。

这意味着，一个粒子被精确局域在空间某一点 $x_0$ 的态，虽然在概念上很有用，但并非一个物理上可实现的态。这些非归一化的[本征函数](@entry_id:154705)被称为“广义本征函数”，它们构成了所谓的**[装备希尔伯特空间](@entry_id:141353) (Rigged Hilbert Space)** 的一部分。在实践中，任何物理上可实现的粒子状态都由一个归一化的**[波包](@entry_id:154698) (wave packet)** 描述，该波包可以看作是这些[连续谱](@entry_id:155477)本征函数（如平面波或位置本征函数）的叠加。这些广义本征函数提供了一个强大的数学框架，用于处理[连续谱](@entry_id:155477)问题，并构成了我们理解散射、隧道效应等现象的基础。