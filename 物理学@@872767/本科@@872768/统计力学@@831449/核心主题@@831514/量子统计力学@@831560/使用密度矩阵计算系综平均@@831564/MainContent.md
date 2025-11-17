## 引言
在量子世界中，一个孤立系统的行为可以通过态矢量 $|\psi\rangle$ 来完美描述。然而，当我们转向更现实的宏观系统——那些与环境不断交换能量和信息，或者我们对其初始状态只有统计性知识的系统时，单一态矢量的描述便显得力不从心。这种从理想孤立系统到现实[统计系综](@entry_id:149738)的跨越，正是量子力学与[统计力](@entry_id:194984)学交汇处的核心挑战，也是[密度矩阵](@entry_id:139892)理论应运而生的背景。

为了弥合这一知识鸿沟，本文将系统介绍**密度矩阵**这一强大工具，它推广了[量子态](@entry_id:146142)的概念，为我们提供了理解和计算[量子系综](@entry_id:136263)统计性质的统一语言。通过学习本文，您将能够：

*   在第一章“**原理与机制**”中，掌握[密度矩阵](@entry_id:139892)的数学定义、基本性质及其动力学演化规律，并学会使用它来计算可观测量的系综平均值，这是整个理论的基石。
*   在第二章“**应用与跨学科联系**”中，探索密度矩阵如何在凝聚态物理、[量子计算](@entry_id:142712)、光学等多个前沿领域中大放异彩，从计算材料热容到解释[量子退相干](@entry_id:145210)，领略其强大的实践价值。
*   在第三章“**动手实践**”中，通过解决一系列具体问题，巩固所学知识，将抽象的理论框架应用于实际的物理情景，深化对核心概念的理解。

本系列文章将引导您从基本概念出发，逐步深入，最终不仅能熟练运用密度矩阵进行计算，更能领会其作为连接微观量子规则与宏观物理现象的桥梁所蕴含的深刻物理思想。现在，让我们从密度矩阵的基本原理开始，踏上这段探索之旅。

## 原理与机制

在量子力学的框架下，一个[孤立系统](@entry_id:159201)的状态由一个[希尔伯特空间](@entry_id:261193)中的态矢量 $|\psi\rangle$ 完美描述。然而，在[统计力](@entry_id:194984)学中，我们通常处理的是与环境有相互作用的宏观系统，或者我们对系统的知识并不完备。在这些情况下，单一的态矢量不足以描述系统的全部统计特性。为了解决这个问题，我们引入一个更强大、更普适的数学工具——**密度矩阵 (density matrix)** 或**[密度算符](@entry_id:138151) (density operator)**，记作 $\hat{\rho}$。本章将系统地阐述密度矩阵的定义、基本性质、其在计算系综平均中的核心作用、[时间演化](@entry_id:153943)规律，以及在描述复合系统和[热平衡](@entry_id:141693)态时的应用。

### [密度矩阵](@entry_id:139892)：[量子态](@entry_id:146142)的统计描述

想象一个量子系统的**系综 (ensemble)**，它由大量以相同方式制备的系统副本组成。然而，由于制备过程的[统计不确定性](@entry_id:267672)，这些副本不一定处于完全相同的[量子态](@entry_id:146142)。系综中的一部分系统（比如，比例为 $p_1$）可能处于[纯态](@entry_id:141688) $|\psi_1\rangle$，另一部分（比例为 $p_2$）处于纯态 $|\psi_2\rangle$，以此类推。每个 $p_i$ 是找到一个随机选取的系统处于 $|\psi_i\rangle$ 态的经典概率，且满足[归一化条件](@entry_id:156486) $\sum_i p_i = 1$。

#### 定义与构造

描述这样一个统计混合系综的[密度算符](@entry_id:138151)被定义为所有可能[纯态](@entry_id:141688)的投影算符的加权平均：
$$
\hat{\rho} = \sum_i p_i |\psi_i\rangle\langle\psi_i|
$$
其中 $|\psi_i\rangle\langle\psi_i|$ 是对应于[纯态](@entry_id:141688) $|\psi_i\rangle$ 的[投影算符](@entry_id:154142)。如果系综中所有系统都处于同一个纯态 $|\psi\rangle$（即某个 $p_k = 1$ 而所有其他的 $p_j = 0$），则[密度算符](@entry_id:138151)简化为 $\hat{\rho} = |\psi\rangle\langle\psi|$，这种情况被称为**纯态 (pure state)**。如果多个 $p_i$ 大于零，则系统处于**混合态 (mixed state)**，它表示了我们对系统确切[量子态](@entry_id:146142)的经典不确定性。

例如，考虑一个由自旋-1/2粒子组成的系综，其中 $p_1 = 3/4$ 的粒子处于z方向的自旋向上态 $|+\rangle_z$，而 $p_2 = 1/4$ 的粒子处于自旋向下态 $|-\rangle_z$。这个系综的密度矩阵就是：
$$
\hat{\rho} = \frac{3}{4} |+\rangle_z\langle+|_z + \frac{1}{4} |-\rangle_z\langle-|_z
$$
在以 $|+\rangle_z$ 和 $|-\rangle_z$ 为[基矢](@entry_id:199546)的表象中，这个密度矩阵可以写成一个 $2 \times 2$ 的矩阵 [@problem_id:1963261]：
$$
\rho = \begin{pmatrix} 3/4  0 \\ 0  1/4 \end{pmatrix}
$$
对角元素 $\rho_{nn}$ 直接给出了在系综中找到粒子处于对应[基态](@entry_id:150928) $|n\rangle$ 的概率。

#### 密度矩阵的基本性质

并非任意一个矩阵都可以成为一个物理上合法的密度矩阵。一个算符 $\hat{\rho}$ 要成为有效的[密度算符](@entry_id:138151)，必须满足三个基本性质 [@problem_id:1963299]：

1.  **[厄米性](@entry_id:141899) (Hermiticity)**: $\hat{\rho} = \hat{\rho}^\dagger$。[密度算符](@entry_id:138151)必须是厄米算符。这一性质保证了所有可观测量的[期望值](@entry_id:153208)都是实数，这与物理测量结果相符。

2.  **单位迹 (Unit Trace)**: $\mathrm{Tr}(\hat{\rho}) = 1$。[算符的迹](@entry_id:185149)（对角元素之和）必须为1。这反映了总概率必须归一化，即在所有可能的状态中找到系统的概率之和为1。$\mathrm{Tr}(\hat{\rho}) = \sum_i p_i \mathrm{Tr}(|\psi_i\rangle\langle\psi_i|) = \sum_i p_i \langle\psi_i|\psi_i\rangle = \sum_i p_i = 1$。

3.  **[正定性](@entry_id:149643) (Positivity)**: $\hat{\rho}$ 是一个半正定算符。这意味着对于任意的态矢量 $|\phi\rangle$，都有 $\langle\phi|\hat{\rho}|\phi\rangle \ge 0$。这个性质等价于[密度算符](@entry_id:138151)的所有[本征值](@entry_id:154894) $\lambda_i$ 都必须是非负的（$\lambda_i \ge 0$）。这些[本征值](@entry_id:154894)可以被解释为系统处于 $\hat{\rho}$ 相应本征态的概率，因此它们不能是负数。

作为一个例子，让我们检验矩阵 $\hat{\rho} = \frac{1}{4} \begin{pmatrix} 1  3i \\ -3i  3 \end{pmatrix}$ 是否是一个合法的[密度矩阵](@entry_id:139892)。
首先，计算其共轭转置：$\hat{\rho}^\dagger = \frac{1}{4} \begin{pmatrix} 1  \overline{(-3i)} \\ \overline{(3i)}  3 \end{pmatrix} = \frac{1}{4} \begin{pmatrix} 1  3i \\ -3i  3 \end{pmatrix} = \hat{\rho}$。因此，**[厄米性](@entry_id:141899)**成立。
其次，计算其迹：$\mathrm{Tr}(\hat{\rho}) = \frac{1}{4}(1 + 3) = 1$。因此，**单位迹**条件也成立。
最后，检验**[正定性](@entry_id:149643)**。对于一个 $2 \times 2$ 厄米矩阵，如果其[行列式](@entry_id:142978)为负，则两个[本征值](@entry_id:154894)必然一正一负。该[矩阵的行列式](@entry_id:148198)为 $\det(\hat{\rho}) = (\frac{1}{4})^2 (1 \cdot 3 - (3i)(-3i)) = \frac{1}{16}(3 - 9) = -\frac{3}{8}$。由于[行列式](@entry_id:142978)为负，该矩阵有一个负[本征值](@entry_id:154894)，因此不满足正定性。所以，尽管这个矩阵满足前两个条件，但它不是一个物理上允许的密度矩阵 [@problem_id:1963299]。

### 系综平均与可观测量

[密度矩阵形式体系](@entry_id:183082)的核心优势在于它提供了一个计算任意可观测量系综平均值（或[期望值](@entry_id:153208)）的统一方法。

#### [期望值](@entry_id:153208)的计算

对于一个由[密度算符](@entry_id:138151) $\hat{\rho}$ 描述的系综，一个[可观测量](@entry_id:267133)（由[厄米算符](@entry_id:153410) $\hat{A}$ 表示）的[期望值](@entry_id:153208) $\langle \hat{A} \rangle$ 由下式给出：
$$
\langle \hat{A} \rangle = \mathrm{Tr}(\hat{\rho} \hat{A})
$$
这个公式是[量子统计力学](@entry_id:140244)的基石。我们可以通过将[密度算符](@entry_id:138151)的定义代入来理解其含义：
$$
\langle \hat{A} \rangle = \mathrm{Tr}\left( \left( \sum_i p_i |\psi_i\rangle\langle\psi_i| \right) \hat{A} \right) = \sum_i p_i \mathrm{Tr}(|\psi_i\rangle\langle\psi_i| \hat{A}) = \sum_i p_i \langle\psi_i| \hat{A} |\psi_i\rangle
$$
这表明，系综平均值正是每个[纯态](@entry_id:141688) $|\psi_i\rangle$ 中可观测量[期望值](@entry_id:153208) $\langle\psi_i|\hat{A}|\psi_i\rangle$ 的经典概率加权平均。

让我们应用这个公式。考虑前述的自旋系综 [@problem_id:1963261]，我们想要计算沿与z轴成 $\theta$ 角的 $\hat{n}$ 方向的自旋分量的平均值。该[可观测量](@entry_id:267133)算符为 $\hat{S}_n = \frac{\hbar}{2} \begin{pmatrix} \cos\theta  \sin\theta \\ \sin\theta  -\cos\theta \end{pmatrix}$。[期望值](@entry_id:153208)为：
$$
\langle \hat{S}_n \rangle = \mathrm{Tr}(\hat{\rho} \hat{S}_n) = \mathrm{Tr}\left( \begin{pmatrix} 3/4  0 \\ 0  1/4 \end{pmatrix} \frac{\hbar}{2} \begin{pmatrix} \cos\theta  \sin\theta \\ \sin\theta  -\cos\theta \end{pmatrix} \right)
$$
$$
\langle \hat{S}_n \rangle = \mathrm{Tr}\left( \frac{\hbar}{2} \begin{pmatrix} (3/4)\cos\theta  (3/4)\sin\theta \\ (1/4)\sin\theta  -(1/4)\cos\theta \end{pmatrix} \right) = \frac{\hbar}{2} \left( \frac{3}{4}\cos\theta - \frac{1}{4}\cos\theta \right) = \frac{\hbar}{4}\cos\theta
$$
特别地，对于系统的能量平均值，我们计算[哈密顿算符](@entry_id:144286) $\hat{H}$ 的[期望值](@entry_id:153208) $\langle E \rangle = \mathrm{Tr}(\hat{\rho} \hat{H})$。如果密度矩阵是在能量本征[基矢](@entry_id:199546)下对角的，即 $\rho_{mn} = p_m \delta_{mn}$，且[哈密顿量](@entry_id:172864)也是对角的 $H_{nn} = E_n$，那么计算就变得非常简单：$\langle E \rangle = \sum_n \rho_{nn} H_{nn} = \sum_n p_n E_n$ [@problem_id:1963263]。

#### 纯度与[冯·诺依曼熵](@entry_id:143216)

[密度矩阵](@entry_id:139892)不仅能计算[期望值](@entry_id:153208)，还能量化我们对系统状态知识的缺乏程度，或者说状态的“混合程度”。

**纯度 (Purity)** 是衡量混合程度的一个简单指标，定义为 $\gamma = \mathrm{Tr}(\hat{\rho}^2)$。对于一个 $d$ 维系统，纯度的取值范围是 $1/d \le \gamma \le 1$。
*   如果系统处于纯态 $\hat{\rho} = |\psi\rangle\langle\psi|$，则 $\hat{\rho}^2 = |\psi\rangle\langle\psi|\psi\rangle\langle\psi| = |\psi\rangle\langle\psi| = \hat{\rho}$。因此，$\gamma = \mathrm{Tr}(\hat{\rho}^2) = \mathrm{Tr}(\hat{\rho}) = 1$。纯[态的纯度](@entry_id:185476)总是1。
*   如果系统处于[混合态](@entry_id:141568)，其纯度将小于1。最小纯度 $1/d$ 对应于**[最大混合态](@entry_id:137775) (maximally mixed state)** $\hat{\rho} = \frac{1}{d} I$，其中 $I$ 是单位矩阵。

例如，一个与温度为 $T$ 的[热库](@entry_id:143608)平衡的自旋-1/2系统，其纯度可以计算出来，并依赖于温度。当温度趋于零时，系统趋于[基态](@entry_id:150928)（一个纯态），纯度趋于1。当温度非常高时，两个能级的布居概率趋于相等，系统趋于[最大混合态](@entry_id:137775)，纯度趋于 $1/2$ [@problem_id:1963264]。

一个更基本、信息论意义更强的度量是**[冯·诺依曼熵](@entry_id:143216) (von Neumann entropy)**，定义为：
$$
S = -k_B \mathrm{Tr}(\hat{\rho} \ln \hat{\rho})
$$
其中 $k_B$ 是玻尔兹曼常数。如果 $\hat{\rho}$ 的[本征值](@entry_id:154894)为 $\lambda_i$，则熵可以表示为 $S = -k_B \sum_i \lambda_i \ln \lambda_i$，这在形式上与香農信息熵非常相似。[冯·诺依曼熵](@entry_id:143216)量化了与[量子态](@entry_id:146142)相关的[统计不确定性](@entry_id:267672)。

对于任何纯态 $\hat{\rho} = |\psi\rangle\langle\psi|$，其[本征值](@entry_id:154894)谱由一个 1 和 $d-1$ 个 0 组成。因此，其熵为 $S = -k_B (1 \cdot \ln(1) + (d-1) \cdot 0 \cdot \ln(0)) = 0$，这里我们使用了极限 $\lim_{x\to 0^+} x \ln x = 0$。[纯态](@entry_id:141688)的熵为零，这与它代表了关于系统的完备知识（没有不确定性）这一事实相符 [@problem_id:1963272]。对于[混合态](@entry_id:141568)，$S > 0$。

### [密度矩阵](@entry_id:139892)的动力学与对称性

#### [时间演化](@entry_id:153943)：刘维-[冯·诺依曼方程](@entry_id:153472)

当系统随时间演化时，其密度矩阵也随之演化。如果系统由一个不含时的[哈密顿算符](@entry_id:144286) $\hat{H}$ 描述，单个纯态的[时间演化](@entry_id:153943)由薛定谔方程给出：$|\psi(t)\rangle = U(t) |\psi(0)\rangle$，其中 $U(t) = \exp(-i\hat{H}t/\hbar)$ 是[时间演化算符](@entry_id:196774)。由此，我们可以推导出[密度矩阵的演化](@entry_id:185083)规律：
$$
\hat{\rho}(t) = \sum_i p_i |\psi_i(t)\rangle\langle\psi_i(t)| = \sum_i p_i U(t) |\psi_i(0)\rangle\langle\psi_i(0)| U(t)^\dagger = U(t) \hat{\rho}(0) U(t)^\dagger
$$
对上式关于时间 $t$求导，可以得到[密度矩阵](@entry_id:139892)的[运动方程](@entry_id:170720)，即**刘维-[冯·诺依曼方程](@entry_id:153472) (Liouville-von Neumann equation)**：
$$
i\hbar \frac{d\hat{\rho}}{dt} = [\hat{H}, \hat{\rho}]
$$
这个方程是量子版本的经典刘维定理。一个重要的推论是，如果[密度矩阵](@entry_id:139892)与[哈密顿量](@entry_id:172864)对易（$[\hat{H}, \hat{\rho}] = 0$），则 $\frac{d\hat{\rho}}{dt} = 0$，密度矩阵不随时间变化，系统处于一个**定态 (stationary state)**。热平衡态就是一个典型的例子。

在计算[可观测量](@entry_id:267133)[期望值的时间演化](@entry_id:153265)时，我们有两种等价的图像。在薛定谔图像中，算符不变，密度矩阵演化：$\langle \hat{A} \rangle(t) = \mathrm{Tr}(\hat{\rho}(t) \hat{A})$。在海森堡图像中，密度矩阵不变，算符演化：$\langle \hat{A} \rangle(t) = \mathrm{Tr}(\hat{\rho}(0) \hat{A}(t))$，其中 $\hat{A}(t) = U(t)^\dagger \hat{A} U(t)$。

考虑一个自旋在z方向[磁场](@entry_id:153296)中进动的例子，[哈密顿量](@entry_id:172864)为 $H = \omega_0 S_z$ [@problem_id:1963275]。我们想计算 $\langle S_x \rangle(t)$。使用海森堡图像，我们需要计算 $S_x(t)$。其[运动方程](@entry_id:170720)为 $\frac{dS_x}{dt} = \frac{i}{\hbar}[H, S_x] = \frac{i\omega_0}{\hbar}[S_z, S_x] = -\omega_0 S_y$。这是一个耦合的微分方程组，其解为 $S_x(t) = S_x(0)\cos(\omega_0 t) - S_y(0)\sin(\omega_0 t)$。因此，[期望值](@entry_id:153208)为：
$$
\langle S_x \rangle(t) = \langle S_x(0) \rangle \cos(\omega_0 t) - \langle S_y(0) \rangle \sin(\omega_0 t)
$$
这描述了自旋[期望值](@entry_id:153208)矢量在xy平面上的进动。

#### [对称性与守恒律](@entry_id:160300)

[密度矩阵形式体系](@entry_id:183082)为利用对称性进行物理推断提供了优雅的工具。如果一个系统的制备过程具有某种对称性，那么描述该系统的[密度矩阵](@entry_id:139892)也必须具有这种对称性。如果对称性由一个幺正算符 $U$ 代表，那么状态的对称性意味着 $\hat{\rho}$ 在该变换下不变，即 $\hat{\rho} = U\hat{\rho}U^\dagger$，或者等价地 $[\hat{\rho}, U] = 0$。

这一对称性可以对可观测量的[期望值](@entry_id:153208)施加很强的约束。假设我们想测量一个可观测量 $\hat{A}$，而它在对称变换 $U$ 下会反号，即 $U^\dagger \hat{A} U = -\hat{A}$（或者说 $\hat{A}$ 与 $U$ [反对易](@entry_id:186708)）。那么它的[期望值](@entry_id:153208)必然为零。证明如下 [@problem_id:1963286]：
$$
\langle \hat{A} \rangle = \mathrm{Tr}(\hat{\rho} \hat{A})
$$
利用迹的循环[不变性](@entry_id:140168)和态的对称性 $\hat{\rho} = U\hat{\rho}U^\dagger$：
$$
\langle \hat{A} \rangle = \mathrm{Tr}(U \hat{\rho} U^\dagger \hat{A}) = \mathrm{Tr}(\hat{\rho} U^\dagger \hat{A} U)
$$
现在使用算符 $\hat{A}$ 的变换性质 $U^\dagger \hat{A} U = -\hat{A}$：
$$
\langle \hat{A} \rangle = \mathrm{Tr}(\hat{\rho} (-\hat{A})) = - \mathrm{Tr}(\hat{\rho} \hat{A}) = -\langle \hat{A} \rangle
$$
唯一满足 $\langle \hat{A} \rangle = -\langle \hat{A} \rangle$ 的数就是零。因此，$\langle \hat{A} \rangle = 0$。

例如，如果一个自旋-1/2系综的制备过程对于绕z轴旋转 $\pi$ [弧度](@entry_id:171693)是不变的，那么 $\langle S_x \rangle$ 和 $\langle S_y \rangle$ 都必须为零，因为 $S_x$ 和 $S_y$ 在这个变换下都会反号 [@problem_id:1963286]。这种基于对称性的论证无需知道[密度矩阵](@entry_id:139892)的具体形式，显示了其强大的威力。

### [多体系统](@entry_id:144006)与[约化密度矩阵](@entry_id:146315)

当处理由多个子系统组成的复合系统时，[密度矩阵形式体系](@entry_id:183082)显示出其不可或缺的价值，特别是在处理[量子纠缠](@entry_id:136576)时。

#### 描述子系统

考虑一个由A和B两个子系统组成的 bipartite 系统，其总[希尔伯特空间](@entry_id:261193)为张量积 $\mathcal{H} = \mathcal{H}_A \otimes \mathcal{H}_B$。整个系统由[密度矩阵](@entry_id:139892) $\hat{\rho}_{AB}$ 描述。如果我们只对子系统A进行测量，而对子系统B的状态不感兴趣或无法测量，我们如何描述A的状态？

答案是**[约化密度矩阵](@entry_id:146315) (reduced density matrix)** $\hat{\rho}_A$。它是通过在子系统B的自由度上对总密度矩阵 $\hat{\rho}_{AB}$ 求**部分迹 (partial trace)** 得到的：
$$
\hat{\rho}_A = \mathrm{Tr}_B(\hat{\rho}_{AB})
$$
$\mathrm{Tr}_B$ 意味着在子系统B的任意一组[完备基](@entry_id:143908)矢上求迹。[约化密度矩阵](@entry_id:146315) $\hat{\rho}_A$ 包含了所有仅通过在子系统A上进行局部测量所能获得的全部信息。一个惊人的事实是，即使整个系统 $\hat{\rho}_{AB}$ 处于一个[纯态](@entry_id:141688)，其子系统 $\hat{\rho}_A$ 也可能处于一个[混合态](@entry_id:141568)。这正是**[量子纠缠](@entry_id:136576) (quantum entanglement)** 的标志。

对于一个只作用于子系统A的局部可观测量 $\hat{O}_A$（在总空间中表示为 $\hat{O} = \hat{O}_A \otimes I_B$），其[期望值](@entry_id:153208)可以完全由[约化密度矩阵](@entry_id:146315)计算，而无需关心整个系统的状态 [@problem_id:1963293]：
$$
\langle \hat{O}_A \rangle = \mathrm{Tr}_{AB}(\hat{\rho}_{AB} (\hat{O}_A \otimes I_B)) = \mathrm{Tr}_A(\hat{\rho}_A \hat{O}_A)
$$
这个公式是处理[开放量子系统](@entry_id:138632)和量子信息理论的基础。

作为一个具体的例子，考虑一个[双量子比特系统](@entry_id:203437)，其状态是贝尔态 $|\Phi^+\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$ 和 $|00\rangle$ 态的混合 [@problem_id:1963302]：
$$
\rho_{AB} = \alpha |\Phi^+\rangle\langle\Phi^+| + (1-\alpha) |00\rangle\langle 00|
$$
为了计算只作用于第一个[量子比特](@entry_id:137928)A的泡利Z算符 $\sigma_z^A$ 的[期望值](@entry_id:153208)，我们首先计算A的[约化密度矩阵](@entry_id:146315) $\rho_A = \mathrm{Tr}_B(\rho_{AB})$。经过计算可得：
$$
\rho_A = \begin{pmatrix} 1 - \alpha/2  0 \\ 0  \alpha/2 \end{pmatrix}
$$
然后，我们可以用 $\rho_A$ 来计算[期望值](@entry_id:153208)：
$$
\langle \sigma_z^A \rangle = \mathrm{Tr}_A(\rho_A \sigma_z^A) = \mathrm{Tr}\left( \begin{pmatrix} 1 - \alpha/2  0 \\ 0  \alpha/2 \end{pmatrix} \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix} \right) = (1 - \alpha/2) - \alpha/2 = 1 - \alpha
$$

### [热平衡](@entry_id:141693)态的[密度矩阵](@entry_id:139892)

在[统计力](@entry_id:194984)学中，最重要的一类系综是处于[热平衡](@entry_id:141693)的系统。对于一个与温度为 $T$ 的大热库接触并[达到平衡](@entry_id:170346)的系统（**正则系综, canonical ensemble**），其状态由**正则密度矩阵**描述：
$$
\hat{\rho} = \frac{\exp(-\beta \hat{H})}{Z}
$$
其中 $\beta = 1/(k_B T)$，$k_B$ 是玻尔兹曼常数，$\hat{H}$ 是系统的[哈密顿量](@entry_id:172864)。归一化因子 $Z$ 被称为**[配分函数](@entry_id:193625) (partition function)**，由 $Z = \mathrm{Tr}[\exp(-\beta \hat{H})]$ 给出。这个形式可以由[最大熵原理](@entry_id:142702)导出，即在给定[平均能量](@entry_id:145892) $\langle\hat{H}\rangle$ 的约束下，正则密度矩阵所对应的[冯·诺依曼熵](@entry_id:143216)最大。

在能量本征[基矢](@entry_id:199546) $\{|n\rangle\}$ 中，[哈密顿量](@entry_id:172864)是对角的，$H_{mn} = E_n \delta_{mn}$。因此，正则密度矩阵也是对角的：
$$
\rho_{mn} = \langle m|\hat{\rho}|n\rangle = \frac{1}{Z} \langle m|\exp(-\beta \hat{H})|n\rangle = \frac{\exp(-\beta E_n)}{Z} \delta_{mn}
$$
对角元素 $\rho_{nn} = \frac{\exp(-\beta E_n)}{Z}$ 就是系统处于能量为 $E_n$ 的[本征态](@entry_id:149904)的概率，这正是玻尔兹曼分布。

作为一个典型的例子，我们考虑一个角频率为 $\omega$ 的一维量子谐振子，其能级为 $E_n = \hbar\omega(n+1/2)$。其[配分函数](@entry_id:193625)是一个[几何级数](@entry_id:158490)求和 [@problem_id:1963268]：
$$
Z = \sum_{n=0}^{\infty} \exp(-\beta E_n) = \frac{\exp(-\beta\hbar\omega/2)}{1 - \exp(-\beta\hbar\omega)}
$$
因此，在能量本征[基矢](@entry_id:199546)中，其[密度矩阵](@entry_id:139892)的[矩阵元](@entry_id:186505)为：
$$
\rho_{mn} = \delta_{mn} \frac{\exp(-\beta E_n)}{Z} = \delta_{mn} \left[1 - \exp(-\beta\hbar\omega)\right] \exp(-n\beta\hbar\omega)
$$
这为我们提供了在任意温度下，一个与热库平衡的量子谐振子的完整统计描述。

综上所述，[密度矩阵](@entry_id:139892)是连接量子力学与[统计力](@entry_id:194984)学的桥梁。它不仅推广了[量子态](@entry_id:146142)的概念以包含[统计不确定性](@entry_id:267672)，还提供了一套完备的形式体系来计算可观测量的系综平均、描述[时间演化](@entry_id:153943)、利用对称性以及处理纠缠的子系统，使其成为现代物理学中一个不可或缺的工具。