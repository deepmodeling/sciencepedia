## 引言
20世纪初，当面对原子和光的奇异行为时，[经典物理学](@keyword=classical_physics|lang=zh-CN|style=Feynman)中那些优雅且可预测的定律开始瓦解。能量以离散的包（即*量子*）存在、电子等粒子展现出波粒二象性等发现，引发了一场深刻的危机。旧的规则被打破，人们迫切需要一种新的数学语言来描述这个奇怪的亚原子现实。本文将探讨量子力学的第一个成功且影响深远的表述：Werner Heisenberg的**[矩阵力学](@keyword=quantum_mechanics_matrices|lang=zh-CN|style=Feynman)**。

这个框架解决了如何表示不再是简单数字的物理量的根本难题。它提出了一个激进的想法：位置、动量和能量等性质最好由称为矩阵的数学对象来描述。我们将穿越这个抽象而强大的世界，揭示支配这种新量子算术的规则。本文的结构旨在帮助你从零开始建立理解。在第一部分**“原理与机制”**中，我们将探讨核心概念，例如为什么[可观测量](@keyword=observables|lang=zh-CN|style=Feynman)必须是厄米矩阵，以及如何从中提取真实世界的测量结果。随后，**“应用与跨学科联系”**将揭示这些思想惊人的应用范围，展示[矩阵力学](@keyword=quantum_mechanics_matrices|lang=zh-CN|style=Feynman)不仅是历史上的一个奇珍，更是从[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)、凝聚态到[时空](@keyword=space_time|lang=zh-CN|style=Feynman)本质等现代前沿领域中充满活力的工作语言。

## 原理与机制

想象一下，你是一位20世纪初的物理学家。你刚刚发现，[经典物理学](@keyword=classical_physics|lang=zh-CN|style=Feynman)平滑、可预测的世界在原子尺度上失效了。能量以离散的包（即*量子*）的形式出现。一个电子似乎既像粒子又像波。旧的规则不再适用，你需要一本新的宇宙说明书。Werner Heisenberg，在灵光一闪间，找到了这样一本说明书。他意识到量子系统的性质——诸如能量、位置和动量——其行为不像普通数字，而更像**矩阵**。这便是**[矩阵力学](@keyword=quantum_mechanics_matrices|lang=zh-CN|style=Feynman)**这个奇异而美丽的世界。

本章将带我们进入那本新的规则手册。我们不会迷失在数学的细节中，而是试图捕捉Heisenberg当年感受到的那种直觉的闪电。我们将提出简单的问题，并发现它们引出了关于现实构造的深刻真理。

### 一种描述现实的奇异新算术

在你周围看到的世界里，一个物体的属性都只是数字。一个球有位置、速度、动能。你可以把它们写下来。但在量子领域，这还不够。一个物理性质，或者我们称之为**可观测量**，不是一个静态的数字，而是一个*动作*，一个过程。而代表动作的数学对象是**算符**。在[矩阵力学](@keyword=quantum_mechanics_matrices|lang=zh-CN|style=Feynman)中，这些算符就是矩阵。

让我们来思考最简单的量子系统。它不是一个球或一颗行星，而是只有两种可能状态的东西。比如电子的[内禀角动量](@keyword=intrinsic_angular_momentum|lang=zh-CN|style=Feynman)，即**自旋**，沿着某个选定轴的测量结果可以是“上”或“下”。这是一个**[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)**，量子信息的[基本单位](@keyword=fundamental_units|lang=zh-CN|style=Feynman)。你可能会认为“上”是`+1`，“下”是`-1`。但量子力学说：“没那么快。” 代表沿不同轴——x、y和z轴——测量自旋的算符，实际上是矩阵！例如，沿y轴的[自旋算符](@keyword=spin_operators|lang=zh-CN|style=Feynman)由这个奇特的小[矩阵表示](@keyword=matrix_representations|lang=zh-CN|style=Feynman)：

$$
\sigma_y = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}
$$

注意那个`i`，-1的平方根！在描述一个非常真实的物理性质的核心之处，竟然出现了虚数。这是我们得到的第一个线索：规则已经改变了。描述现实的对象不再只是简单的实数。

### 物理现实的试金石：[厄米算符](@keyword=hermitian_operators|lang=zh-CN|style=Feynman)

这就引出了一个关键问题。如果我们的[可观测量](@keyword=observables|lang=zh-CN|style=Feynman)是充满复数的矩阵，我们如何得到在实验室实验中看到的普通的、*实数*的结果？物理学家测量到的能量是`2.5`[电子伏特](@keyword=electron_volt|lang=zh-CN|style=Feynman)，而不是`2.5 + 3i`电子伏特！

必须有一个约束，一个规则来确保测量的结果是实数。这个规则确实存在。代表[物理可观测量](@keyword=physical_observables|lang=zh-CN|style=Feynman)的矩阵必须具有一个特殊性质：它们必须是**厄米(Hermitian)**矩阵。

这是什么意思呢？如果一个矩阵$\hat{A}$等于其自身的**共轭转置**（记作$\hat{A}^{\dagger}$），那么它就是厄米矩阵。要求得共轭转置，你首先要[交换矩阵](@keyword=commuting_matrices|lang=zh-CN|style=Feynman)的行和列（转置），然后对每个元素取复共轭。所以，条件是$\hat{A} = \hat{A}^{\dagger}$。

我们来看看`problem 7650`里的[泡利自旋矩阵](@keyword=pauli_spin_matrices|lang=zh-CN|style=Feynman)$\sigma_y$。它是[厄米矩阵](@keyword=hermitian_matrix|lang=zh-CN|style=Feynman)吗？
首先，我们取它的转置：
$$
\sigma_y^T = \begin{pmatrix} 0 & i \\ -i & 0 \end{pmatrix}
$$
现在，我们对每个元素取[复共轭](@keyword=complex_conjugation|lang=zh-CN|style=Feynman)（将`i`替换为`-i`）：
$$
(\sigma_y^T)^* = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}
$$
看！我们得到了[原始矩](@keyword=raw_moments|lang=zh-CN|style=Feynman)阵，所以$\sigma_y^{\dagger} = \sigma_y$。它*是*厄米矩阵。这个简单的检验是通往物理现实的大门。任何通过此检验的矩阵*都可能*代表你可以测量的东西。任何未通过的矩阵则不能。例如，在一个简单的练习中，我们给定几个矩阵，只有满足这个条件的矩阵，比如$B = \begin{pmatrix} 1 & 1-i \\ 1+i & 0 \end{pmatrix}$，才能对应一个物理可观测量[@problem_id:2101347]。对角元素必须是实数，而非对角元素$B_{12}$必须是$B_{21}$的复共轭，这些条件都满足了。

这个性质是如此基础，以至于如果我们要用其他已知矩阵构建一个哈密顿量（能量算符），我们必须以保持[厄米性](@keyword=hermiticity|lang=zh-CN|style=Feynman)的方式来构建它，这反过来又对我们可以使用的数值系数施加了严格的限制关系[@problem_id:1372071]。这不仅仅是一个数学游戏；这是关于物理世界结构的深刻陈述。这里有一个美妙的联系：虽然[时间演化算符](@keyword=time_evolving_operators|lang=zh-CN|style=Feynman)必须是**幺正的**（保持态矢量的长度不变），但这些演化的生成元——像能量这样的[可观测量](@keyword=observables|lang=zh-CN|style=Feynman)——结果是[厄米算符](@keyword=hermitian_operators|lang=zh-CN|style=Feynman)[@problem_id:17339]。

### 寻找答案：[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)和本征态

所以，我们已经确定[可观测量](@keyword=observables|lang=zh-CN|style=Feynman)是[厄米矩阵](@keyword=hermitian_matrix|lang=zh-CN|style=Feynman)。很好。但是数字——实际的测量结果——在哪里呢？

它们隐藏在矩阵内部，提取它们的方法是解**[本征值方程](@keyword=eigenvalue_equations|lang=zh-CN|style=Feynman)**：

$$
\hat{A} | \psi \rangle = \lambda | \psi \rangle
$$

这个方程看起来很抽象，但其思想却非常直观。把算符矩阵$\hat{A}$想象成一个动作，比如“测量沿y轴的自旋”。大多数时候，当这个动作作用于一个任意的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)矢量$|\psi\rangle$时，它会把它变成一个完全不同的矢量。但对于某些特殊的状态，称为**本征态**，$\hat{A}$的作用仅仅是将该状态乘以一个数$\lambda$进行缩放。这个态在抽象空间中的“方向”保持不变。这个特殊的数$\lambda$被称为**[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)**。

奇迹就在这里：**[厄米算符](@keyword=hermitian_operators|lang=zh-CN|style=Feynman)的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)总是实数。**这是一个数学事实，也是整个结构能够成立的原因。对一个可观测量$\hat{A}$进行测量的所有可能结果的集合，恰好就是它的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)集合。

让我们用我们的老朋友$\sigma_y$矩阵来看看这个过程[@problem_id:7650]。为了找到它的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)，我们解特征方程$\det(\sigma_y - \lambda I) = 0$，其中$I$是[单位矩阵](@keyword=identity_matrix|lang=zh-CN|style=Feynman)。
$$
\det \begin{pmatrix} -\lambda & -i \\ i & -\lambda \end{pmatrix} = (-\lambda)(-\lambda) - (-i)(i) = \lambda^2 - 1 = 0
$$
解是$\lambda = 1$和$\lambda = -1$。这些是你在沿y轴测量[电子自旋](@keyword=electron_spin|lang=zh-CN|style=Feynman)时*唯一*可能得到的值（在我们使用的单位下）。它们是实数，正如所承诺的那样！

### 系统的状态与跃迁之舞

我们有了可观测量（[厄米矩阵](@keyword=hermitian_matrix|lang=zh-CN|style=Feynman)）和可能的结果（它们的实数[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)）。但是系统本身呢？在我们测量它之前，它的*状态*是什么？

在[矩阵力学](@keyword=quantum_mechanics_matrices|lang=zh-CN|style=Feynman)中，系统的状态由一个矢量描述——一个我们称为**[右矢](@keyword=bra_vector|lang=zh-CN|style=Feynman)(ket)**的列矩阵，写作$|\psi\rangle$。对于我们的二能级[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)系统，我们可以定义一个基。一个常见的选择是沿z轴有确定自旋的态构成的基，我们称之为$|0\rangle$和$|1\rangle$。
$$
|0\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad |1\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}
$$
[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)的任意状态是这些[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)的[线性组合](@keyword=linear_combinations|lang=zh-CN|style=Feynman)：$|\psi\rangle = c_0 |0\rangle + c_1 |1\rangle$。复系数$c_0$和$c_1$告诉我们态$|\psi\rangle$中含有多少“成分”的$|0\rangle$和$|1\rangle$。它们的模长的平方，$|c_0|^2$和$|c_1|^2$，分别给出了测量系统处于$|0\rangle$或$|1\rangle$态的*概率*。

现在我们可以看到算符对一个态*做*了什么。让我们将$\sigma_y$算符作用于态$|0\rangle$ [@problem_id:1385835]：
$$
\sigma_y |0\rangle = \begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix} \begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} (0)(1) + (-i)(0) \\ (i)(1) + (0)(0) \end{pmatrix} = \begin{pmatrix} 0 \\ i \end{pmatrix} = i \begin{pmatrix} 0 \\ 1 \end{pmatrix} = i|1\rangle
$$
算符$\sigma_y$将态从$|0\rangle$翻转到了$|1\rangle$（并乘以了$i$）。在量子力学中，我们常常想知道在算符$\hat{O}$的影响下，从某个初态$|\psi_i\rangle$跃迁到某个末态$|\psi_f\rangle$的概率幅。这由“矩阵元”$\langle \psi_f | \hat{O} | \psi_i \rangle$给出。**左矢(bra)** $\langle \psi_f |$是[右矢](@keyword=bra_vector|lang=zh-CN|style=Feynman)$|\psi_f\rangle$的[共轭转置](@keyword=conjugate_transpose|lang=zh-CN|style=Feynman)。在我们的例子中，$\sigma_y$导致从$|0\rangle$到$|1\rangle$跃迁的概率幅是$\langle 1 | \sigma_y | 0 \rangle$。利用我们上面的结果，可得 $\langle 1 | (i|1\rangle) = i \langle 1|1 \rangle = i$，因为态$|1\rangle$是归一化的（$\langle 1|1 \rangle = 1$）。这个跃迁的概率是[概率幅](@keyword=probability_amplitude|lang=zh-CN|style=Feynman)的模长平方：$|i|^2 = 1$。跃迁是必然发生的！

### 选择正确的视角：[对角化](@keyword=diagonalization|lang=zh-CN|style=Feynman)

我们写下矩阵和矢量的方式取决于我们选择的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)（比如我们的$|0\rangle$和$|1\rangle$）。这就像是选择用街道地址还是GPS坐标来描述一个位置。物理现实是相同的，但你写下的数字是不同的。

有没有一个“最好”的[基矢](@keyword=basis_vector|lang=zh-CN|style=Feynman)可以使用呢？对于一个给定的系统，最自然的基几乎总是其**哈密顿**算符$\hat{H}$（总能量算符）的[本征基](@keyword=eigenvector_basis|lang=zh-CN|style=Feynman)。为什么？因为在这个基中，[哈密顿矩阵](@keyword=hamiltonian_matrix|lang=zh-CN|style=Feynman)变得异常简单：它是**对角**的。所有非对角元素都为零，而对角元素就是系统的[能量本征值](@keyword=energy_eigenvalues|lang=zh-CN|style=Feynman)。

想象一个[二能级系统](@keyword=two_level_systems|lang=zh-CN|style=Feynman)，其中初始的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)$|\psi_1\rangle$和$|\psi_2\rangle$（或许代表一个电子处于两个[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)之一）相互耦合。其哈密顿量可能看起来像这样[@problem_id:2084026]：
$$
H = \begin{pmatrix} E_0 + \delta & V \\ V & E_0 - \delta \end{pmatrix}
$$
非对角项$V$是一个“耦合”，导致系统在$|\psi_1\rangle$和$|\psi_2\rangle$之间[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)。这些不是“定态”，因为它们的能量没有明确定义。但是如果我们解出这个矩阵的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)，我们就能找到系统的真实、确定的能级。如果我们然后用它*自己的本征矢量*所构成的基来写哈密顿量，表示形式会完全改变。新的矩阵，我们称之为$H'$，将是对角的：
$$
H' = \begin{pmatrix} E_a & 0 \\ 0 & E_b \end{pmatrix}
$$
其中$E_a$和$E_b$是我们找到的[能量本征值](@keyword=energy_eigenvalues|lang=zh-CN|style=Feynman)。在这个特殊的基中，没有耦合。一个能量为$E_a$的态将永远保持能量为$E_a$（在没有其他微扰的情况下）。这个寻找[本征基](@keyword=eigenvector_basis|lang=zh-CN|style=Feynman)以使算符[矩阵对角化](@keyword=a_=_pdp^_1|lang=zh-CN|style=Feynman)的过程被称为**[对角化](@keyword=diagonalization|lang=zh-CN|style=Feynman)**，它是量子物理学家工具箱中最强大的工具之一。

### 超越矩阵：从离散到连续

到目前为止，我们一直在玩一些小巧的$2 \times 2$矩阵。但是，对于一个可以在一条直线上任意位置的粒子呢？它的位置不是两种状态之一，而是一个连续的变量。[矩阵力学](@keyword=quantum_mechanics_matrices|lang=zh-CN|style=Feynman)如何处理这种情况？

答案是矩阵变成了无穷维的。行和列的索引，之前是像1和2这样的离散数字，现在变成了像位置$x$这样的连续变量。对矩阵元的求和变成了积分。态矢量不再是一列数字，而是一个连续的函数，即著名的**[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)**$\psi(x)$。

但核心思想完全相同！像$\langle \psi_m |\hat{O}| \psi_n \rangle$这样的[矩阵元](@keyword=matrix_elements|lang=zh-CN|style=Feynman)变成了一个积分：
$$
O_{mn} = \int \psi_m^*(x) \hat{O} \psi_n(x) dx
$$
例如，在[量子谐振子](@keyword=quantum_harmonic_oscillator|lang=zh-CN|style=Feynman)（分子振动的模型）中，我们可以计算位置算符平方$\hat{x}^2$在[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)（$n=0$）和第二[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)（$n=2$）之间的矩阵元。这涉及一个看起来很复杂的、包含厄米多项式和高斯函数的积分，但最终，它只给出一个数字，$\frac{\hbar}{\sqrt{2}m\omega}$ [@problem_id:1371765]。这个数字的意义与我们简单的$2 \times 2$矩阵元相同：它量化了一个物理算符在两个态之间的耦合程度。这一认识统一了Heisenberg的[矩阵力学](@keyword=quantum_mechanics_matrices|lang=zh-CN|style=Feynman)和Schrödinger的[波动力学](@keyword=wave_mechanics|lang=zh-CN|style=Feynman)——它们是对同一底层现实的两种不同描述。

这个框架也清晰地解释了为什么有些算符可以代表可观测量，而另一些则不能。一维动量算符是$\hat{p} = -i\hbar \frac{d}{dx}$。那个看起来无害的[微分](@keyword=pushforward|lang=zh-CN|style=Feynman)算符$\frac{d}{dx}$，当作用于在边界处消失的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)时（比如在盒子中），实际上是*反厄米的*[@problem_id:1384441]。这意味着它本身不能代表一个物理可观测量。但是当乘以$-i\hbar$后，得到的[动量算符](@keyword=momentum_operator|lang=zh-CN|style=Feynman)$\hat{p}$*是*厄米的，它的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)（可能的动量）是实数。这个形式体系正确地引导着我们。

### 能级不[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)规则：当能级相互排斥时

让我们以这个矩阵形式体系中最美丽、最不直观的预测之一来结束。考虑一个系统，比如一个分子，其两个能级依赖于某个参数，比如说两个原子之间的距离$R$。在一个简化的“透热”视图中，我们可能有两条能量函数曲线$E_1(R)$和$E_2(R)$，它们在某个距离$R_0$处相交。

[矩阵力学](@keyword=quantum_mechanics_matrices|lang=zh-CN|style=Feynman)怎么说？真实的哈密顿量包含一个非对角耦合项$V$，它混合了这两个态。所以能量矩阵看起来像我们之前的$2 \times 2$例子：
$$
H(R) = \begin{pmatrix} E_1(R) & V \\ V & E_2(R) \end{pmatrix}
$$
真实的能级是这个矩阵的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)。正如我们之前发现的，[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)涉及一个平方根项：$\sqrt{(E_1(R) - E_2(R))^2 + 4V^2}$。这些能量有可能相等吗？要使之发生，平方根内的项必须为零。但是，如果耦合项$V$不为零，那么$4V^2$项总是正的！即使在$E_1 = E_2$的$R_0$点，平方根项也是$\sqrt{4V^2} = 2|V|$。

能级可以靠得很近，但它们永远不能[交叉](@keyword=decussation|lang=zh-CN|style=Feynman)。耦合项$V$迫使它们相互“排斥”。这被称为**[避免交叉](@keyword=avoided_crossings|lang=zh-CN|style=Feynman)**[@problem_id:2678126]。能级之间的最小间隙恰好是$2|V|$。这不是一个小修正；这是系统[能谱](@keyword=energy_spectrum|lang=zh-CN|style=Feynman)性质的根本性改变，完全由一个$2 \times 2$厄米矩阵的数学性质所预测。这一现象对于理解[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)速率、材料中的能量转移以及许多其他量子现象至关重要。这是一个绝佳的例子，说明了[矩阵力学](@keyword=quantum_mechanics_matrices|lang=zh-CN|style=Feynman)简单而严格的规则如何揭示了量子世界深刻且常常令人惊讶的行为。