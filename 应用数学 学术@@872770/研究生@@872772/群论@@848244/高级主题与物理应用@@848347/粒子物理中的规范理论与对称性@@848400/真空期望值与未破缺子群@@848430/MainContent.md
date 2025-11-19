## 引言
对称性是现代物理学的基石，它不仅赋予物理定律以优美的形式，也深刻地决定了守恒律和基本相互作用的本质。然而，我们所观测到的宇宙在很大程度上呈现出一种“破缺”的对称性，这与理论所预言的完美对称性形成了鲜明对比。如何调和理论的内在对称性与现象的不对称性？自发对称性破缺（Spontaneous Symmetry Breaking, SSB）机制为此提供了一个强有力的解释框架。其核心思想在于，即使一个系统的基本动力学规律（如[拉格朗日量](@entry_id:174593)）在一个对称群 G 下保持不变，其能量最低的[基态](@entry_id:150928)（或真空态）却可能不具备这种对称性。当系统“选择”了其中一个特定的[基态](@entry_id:150928)时，对称性便被自发地破坏了。

本文旨在系统性地解决一个核心问题：当[自发对称性破缺](@entry_id:140964)发生时，我们如何精确地确定剩余的对称性，即所谓的“[未破缺子群](@entry_id:204152)”？理解这一过程对于揭示粒子[质量的起源](@entry_id:161752)、预测新粒子的存在以及构建更宏大的统一理论至关重要。

在接下来的内容中，我们将分三步深入探索这一主题。在“原理与机制”一章中，我们将建立理论基础，阐明[真空期望值](@entry_id:146340)（VEV）的概念，并介绍如何运用李代数的方法来判别哪些对称性被保留、哪些被破缺。接着，在“应用与跨学科关联”一章中，我们将展示这些原理在粒子物理标准模型、大统一理论（GUTs）、凝聚态物理乃至宇宙学中的具体应用，领略其强大的解释力和普适性。最后，在“动手实践”部分，我们将通过一系列精心设计的练习，帮助你将理论知识转化为解决实际问题的能力。

## 原理与机制

在物理学中，对称性的概念至关重要，它支配着[基本相互作用](@entry_id:749649)的结构和[守恒定律](@entry_id:269268)的起源。然而，我们观察到的世界在许多方面并不表现出理论所描述的完美对称性。[自发对称性破缺](@entry_id:140964)（Spontaneous Symmetry Breaking, SSB）的机制为我们提供了一个深刻的框架，以调和理论的内在对称性与现象的不对称性。这一机制的核心思想是，尽管描述一个物理系统的基本定律（例如，其[拉格朗日量](@entry_id:174593)或[哈密顿量](@entry_id:172864)）在一个特定的对称群 $G$ 下保持不变，但系统的[基态](@entry_id:150928)或真空态却不具备这种对称性。本章旨在深入探讨自发对称性破缺的基本原理，阐明确定剩余对称性的方法，并揭示其在粒子物理和凝聚态物理中的深远影响。

### 自发对称性破缺与[真空期望值](@entry_id:146340)

自发对称性破缺的[典范模型](@entry_id:198268)是一个[复标量场](@entry_id:159799) $\Phi$，其[势能](@entry_id:748988)由以下形式给出：
$$
V(\Phi) = -\mu^2 (\Phi^\dagger \Phi) + \lambda (\Phi^\dagger \Phi)^2
$$
其中 $\mu^2$ 和 $\lambda$ 是正实数。该势能在复平面上形似一顶“墨西哥帽”，其在 $\Phi=0$ 处有一个局域极大值，而在一个圆周上达到最小值。这个[势能](@entry_id:748988) $V(\Phi)$ 在全局 $U(1)$ 相位变换 $\Phi \to e^{i\alpha}\Phi$ 下是完全不变的。然而，系统的[基态](@entry_id:150928)（真空态）并非对称的 $\Phi=0$ 状态，因为该点能量并非最低。

能量的最小值出现在势能导数为零的位置，即 $\frac{\partial V}{\partial (\Phi^\dagger \Phi)} = 0$，这给出了：
$$
\Phi^\dagger \Phi = \frac{\mu^2}{2\lambda} \equiv v^2
$$
这里的 $v$ 是一个非零实常数，称为**[真空期望值](@entry_id:146340) (Vacuum Expectation Value, VEV)** 的大小。这意味着任何满足 $|\Phi| = v$ 的场构型都是一个[能量简并](@entry_id:203091)的[基态](@entry_id:150928)。当系统演化到其中一个特定的[基态](@entry_id:150928)，例如 $\langle\Phi\rangle = v$（通过相位旋转，我们可以将其选为实数），系统的这种选择就“自发地”破坏了原有的 $U(1)$ 对称性。因为这个特定的真空态 $v$ 在 $\Phi \to e^{i\alpha}\Phi$ （其中 $\alpha \neq 2\pi k$）变换下不再保持不变。

这个过程是理解现代物理学中质量起源和对称性模式的关键。一个标量场获得非零的[真空期望值](@entry_id:146340)，是触发对称性破缺的普遍机制。

### [未破缺子群](@entry_id:204152)与真空[流形](@entry_id:153038)

当一个连续[对称群](@entry_id:146083) $G$ 被自发破缺时，通常并非所有的对称性都消失了。会有一个[子群](@entry_id:146164) $H \subset G$ 保留下来，它由所有那些能够使选定的真空态 $\langle\Phi\rangle$ 保持不变的变换组成。这个[子群](@entry_id:146164) $H$ 被称为**[未破缺子群](@entry_id:204152) (unbroken subgroup)** 或**[稳定子群](@entry_id:137216) (stabilizer subgroup)**。其形式化定义为：
$$
H = \{ h \in G \mid h \langle\Phi\rangle = \langle\Phi\rangle \}
$$
其中 $h \langle\Phi\rangle$ 表示群元 $h$ 对[真空期望值](@entry_id:146340) $\langle\Phi\rangle$ 的作用。

所有可能的简并[基态](@entry_id:150928)构成的集合被称为**真空[流形](@entry_id:153038) (vacuum manifold)** $\mathcal{M}$。由于[哈密顿量](@entry_id:172864)在整个群 $G$ 下是不变的，从任何一个[基态](@entry_id:150928)出发，通过 $G$ 中元素的变换，都可以得到另一个能量完全相同的[基态](@entry_id:150928)。因此，真空[流形](@entry_id:153038)正是所选[基态](@entry_id:150928) $\langle\Phi\rangle$ 在群 $G$ 作用下的**[轨道](@entry_id:137151) (orbit)**：
$$
\mathcal{M} = \{ g \langle\Phi\rangle \mid g \in G \}
$$
根据群论中的[轨道](@entry_id:137151)-稳定子定理，一个元素的[轨道](@entry_id:137151)与它的[稳定子群](@entry_id:137216)的陪集之间存在一一对应关系。对于李群而言，这种对应关系是微分同胚的。因此，真空[流形](@entry_id:153038)在拓扑上等价于**[陪集空间](@entry_id:180459) (coset space)** $G/H$ [@problem_id:2992559]。
$$
\mathcal{M} \cong G/H
$$
真空[流形](@entry_id:153038)的维度 $\dim(\mathcal{M})$ 等于 $\dim(G) - \dim(H)$。这个维度也恰好是理论中出现的**[南部-戈德斯通玻色子](@entry_id:137488) (Nambu-Goldstone bosons)** 的数目。值得强调的是，将真空[流形](@entry_id:153038)等同于[陪集空间](@entry_id:180459) $G/H$ 并不要求 $H$ 是 $G$ 的一个正规子群 [@problem_id:2992559]。

### 确定[对称性破缺模式](@entry_id:191014)

为了确定一个给定的VEV $\langle\Phi\rangle$ 将对称群 $G$ 破缺到哪个[子群](@entry_id:146164) $H$，我们通常从[李代数](@entry_id:137954)的层面入手。一个[李群](@entry_id:137659)的[对称变换](@entry_id:144406)可以由其[李代数](@entry_id:137954)的生成元 $T_a$ 来表示。一个无穷小变换可以写为 $U \approx 1 + i\epsilon^a T_a$。

一个生成元 $T_a$ 被认为是**未破缺的**，如果它作用在真空态上结果为零。这些未破缺的生成元张成了[未破缺子群](@entry_id:204152) $H$ 的[李代数](@entry_id:137954) $\mathfrak{h}$。反之，如果一个生成元作用在真空态上结果非零，它就被称为**破缺的生成元**。

因此，判定一个生成元是否破缺的核心判据是：
$$
T_a \langle\Phi\rangle = 0 \quad \Leftrightarrow \quad T_a \text{ is unbroken}
$$
$$
T_a \langle\Phi\rangle \neq 0 \quad \Leftrightarrow \quad T_a \text{ is broken}
$$
破缺生成元的数量，即 $\dim(G) - \dim(H)$，直接关系到系统低[能谱](@entry_id:181780)中的物理后果。如果 $G$ 是一个全局[对称群](@entry_id:146083)，根据**[戈德斯通定理](@entry_id:142874) (Goldstone's theorem)**，每个破缺的生成元对应一个无质量的标量粒子，即戈德斯通玻色子 [@problem_id:839798] [@problem_id:2992559]。如果 $G$ 是一个局域（规范）[对称群](@entry_id:146083)，根据**[希格斯机制](@entry_id:144416) (Higgs mechanism)**，这些“潜在的”戈德斯通玻色子会被相应的[规范玻色子](@entry_id:200257)“吃掉”，使得后者获得质量。因此，破缺生成元的数目等于有质量的规范玻色子的数目 [@problem_id:782472]。

#### `SO(N)`对称性的破缺

考虑一个具有 $SO(N)$ 对称性的理论，其中一个 $N$ 分量的实[标量场](@entry_id:151443) $\Phi$ 处在 $SO(N)$ 的[基本表示](@entry_id:157678)（矢量表示）下。其[势能](@entry_id:748988) $V(\Phi) = \frac{\lambda}{4} ( \Phi^T \Phi - v^2 )^2$ 促使场获得一个非零VEV。不失一般性，我们可以通过一次 $SO(N)$ 旋转将VEV对准最后一个分量 [@problem_id:839798] [@problem_id:782472]：
$$
\langle\Phi\rangle = \begin{pmatrix} 0 \\ \vdots \\ 0 \\ v \end{pmatrix}
$$
一个 $SO(N)$ 变换 $O$ 保持此VEV不变的条件是 $O \langle\Phi\rangle = \langle\Phi\rangle$。这意味着矩阵 $O$ 的最后一列必须是 $(0, \dots, 0, 1)^T$。由于 $SO(N)$ 矩阵是正交的，其行和列都是单位[正交向量](@entry_id:142226)，这迫使 $O$ 的最后一行也必须是 $(0, \dots, 0, 1)$。因此，这个不变矩阵 $O$ 必然具有如下的分块形式：
$$
O = \begin{pmatrix} O'  0 \\ 0  1 \end{pmatrix}
$$
其中 $O'$ 是一个 $(N-1) \times (N-1)$ 的矩阵。由于 $O$ 属于 $SO(N)$（[行列式](@entry_id:142978)为1），$O'$ 必须属于 $SO(N-1)$。因此，[未破缺子群](@entry_id:204152)是 $H = SO(N-1)$。

[李群](@entry_id:137659) $SO(N)$ 的维度是 $\dim(SO(N)) = \frac{N(N-1)}{2}$。破缺生成元的数量为：
$$
\dim(G) - \dim(H) = \dim(SO(N)) - \dim(SO(N-1)) = \frac{N(N-1)}{2} - \frac{(N-1)(N-2)}{2} = N-1
$$
这意味着在 $SO(N) \to SO(N-1)$ 的破缺模式下，会产生 $N-1$ 个[戈德斯通玻色子](@entry_id:156185)（对于全局对称性）或 $N-1$ 个有质量的规范玻色子（对于局域对称性）。例如，在 $N=4$ 的情况下，当 $SO(4)$ 破缺为 $SO(3)$ 时，会产生 $\dim(SO(4)) - \dim(SO(3)) = 6 - 3 = 3$ 个[戈德斯通玻色子](@entry_id:156185) [@problem_id:839798]。

#### `SU(N)`对称性的破缺

$SU(N)$ 群的破缺模式更为丰富，取决于[标量场](@entry_id:151443)所在的表示以及VEV的具体结构。

考虑一个具有 $SU(3)$ 对称性的理论，其中一个[复标量场](@entry_id:159799) $\Phi$ 处于3维[基本表示](@entry_id:157678)下。我们可以选择VEV为 [@problem_id:839840]：
$$
\langle\Phi\rangle = \begin{pmatrix} 0 \\ 0 \\ v \end{pmatrix}
$$
我们需要检验 $SU(3)$ 的八个生成元 $T_a = \frac{1}{2}\lambda_a$（其中 $\lambda_a$ 是[Gell-Mann矩阵](@entry_id:159244)）哪些会使 $\langle\Phi\rangle$ 为零。
- 生成元 $\lambda_1, \lambda_2, \lambda_3$ 构成了作用于前两个分量的 $SU(2)$ 子代数，它们作用在 $\langle\Phi\rangle$ 上显然为零。因此，$T_1, T_2, T_3$ 是未破缺的。
- 生成元 $\lambda_4, \lambda_5, \lambda_6, \lambda_7$ 会将第三分量与第一或第二分量混合，因此它们作用在 $\langle\Phi\rangle$ 上不为零，是破缺的。
- 对角的生成元 $\lambda_8 = \frac{1}{\sqrt{3}}\text{diag}(1, 1, -2)$ 作用在 $\langle\Phi\rangle$ 上得到一个非[零向量](@entry_id:156189)。因此 $T_8$ 也是破缺的。

综上所述，未破缺的生成元是 $T_1, T_2, T_3$，它们构成了 $SU(2)$ 的李代数。因此，[未破缺子群](@entry_id:204152)是 $H=SU(2)$，其维度为3。破缺生成元的数量为 $\dim(SU(3)) - \dim(SU(2)) = 8 - 3 = 5$。

如果标量场处于伴随表示下，情况则有所不同。例如，考虑一个 $SU(2)$ 理论，其中场 $\Phi = \phi^a T^a$ 处于伴随表示，VEV为 $\langle\Phi\rangle = v T^3$（其中 $T^a = \sigma^a/2$ 是 $SU(2)$ 生成元）[@problem_id:839835]。一个无穷小变换 $U \approx 1 + i\theta^a T^a$ 保持VEV不变的条件是其生成元与VEV对易：
$$
[i\theta^a T^a, v T^3] = 0 \implies i v \theta^a [T^a, T^3] = 0
$$
利用 $SU(2)$ 代数 $[T^a, T^b] = i\epsilon^{abc}T^c$，我们得到 $\theta^a \epsilon^{a3c} T^c = 0$。由于 $\epsilon^{a3c}$ 只在 $a=1, c=2$ 或 $a=2, c=1$ 时非零，这意味着 $\theta^1=0$ 和 $\theta^2=0$。只有 $\theta^3$ 可以是非零的（因为 $[T^3, T^3]=0$）。这表明只有一个生成元 $T^3$ 是未破缺的。这个生成元对应一个 $U(1)$ [子群](@entry_id:146164)。因此，对称性由 $SU(2)$ 破缺为 $U(1)$，维度为1。

更复杂的例子可见于某些大统一理论模型，其中 $SU(3)$ 被一个伴随表示的[标量场](@entry_id:151443)破缺，其VEV的[本征值](@entry_id:154894)为 $\{v, v, -2v\}$ [@problem_id:839910]。这种简并的本征谱结构意味着[未破缺子群](@entry_id:204152)是保持两个简并的[本征向量](@entry_id:151813)构成的[子空间](@entry_id:150286)不变的变换，即 $S(U(2) \times U(1))$。其维度为 $\dim(U(2)) + \dim(U(1)) - 1 = 2^2+1^2-1=4$。因此，真空[流形](@entry_id:153038)的维度（或[戈德斯通玻色子](@entry_id:156185)的数量）为 $\dim(SU(3)) - \dim(S(U(2) \times U(1))) = 8 - 4 = 4$。

#### 应用：[电弱对称性破缺](@entry_id:161363)

标准模型中的[电弱对称性破缺](@entry_id:161363)是这一机制最成功的应用。电弱[规范群](@entry_id:144761)为 $G = SU(2)_L \times U(1)_Y$。希格斯场 $\Phi$ 是一个 $SU(2)_L$ 的[复标量](@entry_id:272141)二重态，其[弱超荷](@entry_id:149263) $Y=1$。通过规范选择，其VEV可以写为 [@problem_id:839786]：
$$
\langle\Phi\rangle = \frac{1}{\sqrt{2}} \begin{pmatrix} 0 \\ v \end{pmatrix}
$$
$SU(2)_L$ 的三个生成元 $T^a = \sigma^a/2$ ($a=1,2,3$) 和 $U(1)_Y$ 的生成元 $Y_{\text{op}}$ 作用在 $\langle\Phi\rangle$ 上。
- $T^1\langle\Phi\rangle$ 和 $T^2\langle\Phi\rangle$ 显然非零，因此 $T^1, T^2$ 是破缺的。
- $T^3\langle\Phi\rangle = \frac{1}{2}\sigma^3 \langle\Phi\rangle = \frac{1}{2\sqrt{2}} \begin{pmatrix} 0 \\ -v \end{pmatrix} \neq 0$。
- $Y_{\text{op}}\langle\Phi\rangle = Y \langle\Phi\rangle = 1 \cdot \langle\Phi\rangle \neq 0$。

乍一看，似乎所有四个生成元都破缺了。然而，关键在于寻找它们的[线性组合](@entry_id:154743)中可能存在的未破缺生成元。考虑[电荷](@entry_id:275494)算符 $Q_{em}$：
$$
Q_{em} = T^3 + \frac{Y_{op}}{2}
$$
让我们检验它是否是未破缺的。由于希格斯[真空期望值](@entry_id:146340)的非零分量（下分量）是 $T^3$ 的[本征值](@entry_id:154894)为 $-1/2$ 的本征态，并且整个二重态的[弱超荷](@entry_id:149263)为 $Y=1$，[电荷](@entry_id:275494)算符 $Q_{em}$ 作用在真空态上得到：
$$
Q_{em}\langle\Phi\rangle = \left(T^3 + \frac{Y}{2}\right) \langle\Phi\rangle = \left(-\frac{1}{2} + \frac{1}{2}\right) \langle\Phi\rangle = 0
$$
这表明 $Q_{em}$ 是一个未破缺的生成元！它生成的[子群](@entry_id:146164)就是电磁[规范群](@entry_id:144761) $U(1)_{em}$。在 $SU(2)_L \times U(1)_Y$ 的总共 $3+1=4$ 个生成元中，有1个是未破缺的，因此有 $4-1=3$ 个是破缺的。这3个破缺的生成元对应于希格斯机制中获得质量的三个[规范玻色子](@entry_id:200257)：$W^+, W^-, Z^0$。而对应于未破缺生成元 $Q_{em}$ 的规范玻色子——[光子](@entry_id:145192)——则保持无质量。

反过来，要求电[磁对称性](@entry_id:186579) $U(1)_{em}$ 不被破坏，可以对承担[对称性破缺](@entry_id:158994)任务的[标量场](@entry_id:151443)属性施加严格的约束。例如，如果一个标量场处于 $SU(2)_L$ 的四重态（[同位旋](@entry_id:199830) $j=3/2$），并且我们要求其 VEV 落在 $T^3=+1/2$ 的分量上时保持[电中性](@entry_id:157680)（即 $Q_{em}=0$），我们就能唯一地确定该[标量场](@entry_id:151443)的[弱超荷](@entry_id:149263) $Y$。由 $Q_{em} = T^3 + Y/2 = 0$，我们得到 $1/2 + Y/2 = 0$，即 $Y=-1$ [@problem_id:839908]。

### 剩余[离散对称性](@entry_id:146994)

在某些情况下，即使连续对称群被完全破缺，也可能留下一个离散的[子群](@entry_id:146164)作为未破缺对称性。

考虑一个 $U(1)$ 规范理论，其中一个[电荷](@entry_id:275494)为 $n$ 的[复标量场](@entry_id:159799) $\phi$ 获得非零VEV $\langle\phi\rangle = v$。一个 $U(1)$ 变换 $\phi \to e^{i n \alpha}\phi$ 保持真空不变的条件是 $e^{i n \alpha} = 1$。这要求 $n\alpha = 2\pi k$ 对于某个整数 $k$ 成立。因此，允许的变换参数为 $\alpha = \frac{2\pi k}{n}$。在 $[0, 2\pi)$ 区间内，这给出了 $n$ 个离散的解：$0, \frac{2\pi}{n}, \frac{4\pi}{n}, \dots, \frac{2\pi(n-1)}{n}$。这些变换构成了一个 $n$ 阶[循环群](@entry_id:138668) $\mathbb{Z}_n$。

如果系统中有多个标量场 $\phi_1, \phi_2, \dots$，它们的[电荷](@entry_id:275494)分别为 $n_1, n_2, \dots$，并且它们都获得了非零VEV，那么剩余的[离散对称性](@entry_id:146994)必须同时满足所有[不变性条件](@entry_id:171412) [@problem_id:839957]：
$$
e^{i n_1 \alpha} = 1, \quad e^{i n_2 \alpha} = 1, \quad \dots
$$
这意味着 $\alpha$ 必须同时是 $2\pi/n_1, 2\pi/n_2, \dots$ 的整数倍。这等价于要求 $\alpha$ 是 $2\pi / \gcd(n_1, n_2, \dots)$ 的整数倍。因此，剩余的离散[对称群](@entry_id:146083)是 $\mathbb{Z}_d$，其中 $d = \gcd(n_1, n_2, \dots)$。

这个概念可以推广到多个 $U(1)$ 群的乘积。例如，在 $G = U(1)_A \times U(1)_B$ 对称群下，有两个[标量场](@entry_id:151443) $\phi_1, \phi_2$，它们的[电荷](@entry_id:275494)向量分别为 $\vec{q}_1 = (n_A, n_B)$ 和 $\vec{q}_2 = (k_A, k_B)$。如果它们都获得VEV，一个变换 $(\alpha, \beta)$ 保持真空不变的条件是 [@problem_id:839788]：
$$
n_A \alpha + n_B \beta = 2\pi m_1
$$
$$
k_A \alpha + k_B \beta = 2\pi m_2
$$
其中 $m_1, m_2$ 是整数。这个[线性方程组的解](@entry_id:150455) $(\alpha, \beta)$ 构成了剩余的[对称群](@entry_id:146083)。如果[电荷](@entry_id:275494)向量[线性无关](@entry_id:148207)，这个群是离散的。其阶数（即不同解的数量，模 $2\pi$）等于[电荷](@entry_id:275494)[矩阵行列式](@entry_id:194066)的[绝对值](@entry_id:147688)：
$$
\text{Order}(H) = \left| \det \begin{pmatrix} n_A  n_B \\ k_A  k_B \end{pmatrix} \right| = |n_A k_B - n_B k_A|
$$
这个结果在[弦理论](@entry_id:145688)和[超越标准模型](@entry_id:161067)的模型构建中具有重要意义，因为这种剩余的[离散对称性](@entry_id:146994)可以用来解释[味物理](@entry_id:148857)中的层级结构或作为暗物质稳定性的来源。

综上所述，通过分析[标量场](@entry_id:151443)的[真空期望值](@entry_id:146340)如何响应[对称群](@entry_id:146083)的变换，我们可以精确地确定[对称性破缺](@entry_id:158994)的模式，识别出未破缺的连续或离散[子群](@entry_id:146164)。这一过程是理解[粒子质量](@entry_id:156313)谱、相互作用结构以及探索新物理现象的基础。