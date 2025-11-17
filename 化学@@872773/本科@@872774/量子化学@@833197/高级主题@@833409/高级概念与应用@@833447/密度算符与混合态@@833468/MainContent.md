## 引言
在量子力学的世界里，态矢量 $|\psi\rangle$ 是我们描述孤立、理想系统状态的基石。然而，现实中的量子系统很少如此纯粹：我们可能无法完美制备一个系统，或者我们只对一个更大纠缠系统的一部分感兴趣。在这些常见情况下，单一态矢量的描述力将捉襟见肘。为了弥合这一理论与现实之间的鸿沟，我们需要一个更强大、更普适的工具——[密度算符](@entry_id:138151)（density operator）。[密度算符](@entry_id:138151)不仅能够优雅地囊括纯态，还能精确描述由经典概率混合而成的“[混合态](@entry_id:141568)”，使其成为现代量子科学中不可或缺的语言。

本文将系统地引导你掌握[密度算符](@entry_id:138151)的核心概念。在“原理与机制”一章中，我们将深入其数学形式，探讨其基本性质，并学习如何用它来计算物理量和区分不同类型的[量子态](@entry_id:146142)。随后的“应用与[交叉](@entry_id:147634)学科联系”一章将展示[密度算符](@entry_id:138151)如何在[量子统计力学](@entry_id:140244)、[量子化学](@entry_id:140193)和[量子信息](@entry_id:137721)等前沿领域中发挥关键作用，连接抽象理论与具体问题。最后，通过“动手实践”部分，你将有机会应用所学知识解决实际问题，巩固理解。

现在，让我们一同开启探索之旅，首先从[密度算符](@entry_id:138151)的基本原理与机制出发，揭示其超越传统态矢量描述的强大能力。

## 原理与机制

在本章中，我们将深入探讨[密度算符](@entry_id:138151)（density operator）的形式主义，这是一个功能强大的数学工具，它扩展了我们描述量子系统的能力，超越了单一态矢量（state vector）的局限。我们将阐明为何以及何时需要使用[密度算符](@entry_id:138151)，定义其数学属性，并探索其在计算可观测量、理解[量子纠缠](@entry_id:136576)和描述[系统动力学](@entry_id:136288)中的核心作用。

### 超越态矢量：为何需要[密度算符](@entry_id:138151)？

在量子力学的基础学习中，我们习惯于用一个态矢量 $|\psi\rangle$ 来完整描述一个孤立的、制备完好的量子系统。这种描述被称为**[纯态](@entry_id:141688) (pure state)**。然而，在现实的物理和化学情境中，这种理想化的描述往往是不够的。主要原因有两个：

1.  **[统计不确定性](@entry_id:267672)**：我们可能无法完美地将一个系统制备在单一的纯态 $|\psi\rangle$ 上。更常见的情况是，我们得到的是一个**系综 (ensemble)**，其中一部分系统处于状态 $|\psi_1\rangle$，另一部分处于 $|\psi_2\rangle$，以此类推，每个状态都带有一个经典的概率 $p_i$。例如，一个样品可能包含自旋向上的粒子和自旋向下的粒子，两者按一定比例混合。这种由于我们对系统制备过程的知识不完备而产生的统计混合，无法用单一的态矢量来描述。这种状态被称为**混合态 (mixed state)**。

2.  **[量子纠缠](@entry_id:136576)与子系统**：即使一个复合系统（例如，一个由两个粒子A和B组成的系统）本身处于一个[纯态](@entry_id:141688) $|\Psi_{AB}\rangle$，如果我们只对其中一个子系统（例如，粒子A）进行测量和描述，我们通常会发现粒子A本身并不处于一个纯态。这是量子纠缠的深刻后果：关于子系统A的所有信息都无法脱离子系统B而独立定义。当我们“忽略”或“平均掉”子系统B的自由度时，对A的描述自然地呈现为混合态。

为了统一处理纯态和混合态，并为描述量子子系统提供一个严谨的框架，我们需要引入[密度算符](@entry_id:138151)。

### [密度算符](@entry_id:138151)的数学形式

[密度算符](@entry_id:138151)，通常记为 $\hat{\rho}$，为我们提供了一种普遍的语言来描述任何[量子态](@entry_id:146142)。

#### [纯态](@entry_id:141688)

对于一个处于归一化[纯态](@entry_id:141688) $|\psi\rangle$ 的系统，其[密度算符](@entry_id:138151)定义为该态到自身的投影算符：
$$
\hat{\rho} = |\psi\rangle\langle\psi|
$$
这是一个非常简洁的定义。要在某个特定的基底下得到其[矩阵表示](@entry_id:146025)，我们只需计算其[矩阵元](@entry_id:186505)。例如，在一个由正交归一[基矢](@entry_id:199546) $\{|\phi_n\rangle\}$ 张成的[希尔伯特空间](@entry_id:261193)中，[密度矩阵](@entry_id:139892)的元素 $\rho_{mn}$ 为：
$$
\rho_{mn} = \langle\phi_m|\hat{\rho}|\phi_n\rangle = \langle\phi_m|\psi\rangle\langle\psi|\phi_n\rangle
$$
若将态矢量 $|\psi\rangle$ 在此基底下展开为 $|\psi\rangle = \sum_k c_k |\phi_k\rangle$，其中 $c_k = \langle\phi_k|\psi\rangle$，那么[矩阵元](@entry_id:186505)就是 $\rho_{mn} = c_m c_n^*$。

作为一个具体的例子，考虑一个[双原子分子](@entry_id:148655)中的电子，其状态可以用两个[原子轨道](@entry_id:140819) $|\phi_A\rangle$ 和 $|\phi_B\rangle$ 的线性组合来近似。假设电子被制备在[纯态](@entry_id:141688) $|\psi\rangle = \frac{1}{\sqrt{6}} \left( (1+i)|\phi_A\rangle + 2|\phi_B\rangle \right)$ [@problem_id:1404025]。在这个 $\{|\phi_A\rangle, |\phi_B\rangle\}$ 基底下，我们有 $c_A = \frac{1+i}{\sqrt{6}}$ 和 $c_B = \frac{2}{\sqrt{6}}$。[密度矩阵](@entry_id:139892)的元素可以如下计算：
$$
\rho_{AA} = c_A c_A^* = \left(\frac{1+i}{\sqrt{6}}\right)\left(\frac{1-i}{\sqrt{6}}\right) = \frac{1^2 - i^2}{6} = \frac{2}{6} = \frac{1}{3}
$$
$$
\rho_{BB} = c_B c_B^* = \left(\frac{2}{\sqrt{6}}\right)\left(\frac{2}{\sqrt{6}}\right) = \frac{4}{6} = \frac{2}{3}
$$
$$
\rho_{AB} = c_A c_B^* = \left(\frac{1+i}{\sqrt{6}}\right)\left(\frac{2}{\sqrt{6}}\right) = \frac{2(1+i)}{6} = \frac{1+i}{3}
$$
$$
\rho_{BA} = c_B c_A^* = \left(\frac{2}{\sqrt{6}}\right)\left(\frac{1-i}{\sqrt{6}}\right) = \frac{2(1-i)}{6} = \frac{1-i}{3}
$$
因此，该[纯态](@entry_id:141688)的[密度矩阵](@entry_id:139892)为：
$$
\rho = \begin{pmatrix} \frac{1}{3} & \frac{1+i}{3} \\ \frac{1-i}{3} & \frac{2}{3} \end{pmatrix}
$$

#### 混合态

对于一个[混合态](@entry_id:141568)，系统以经典概率 $p_i$ 处于一系列（不必正交的）纯态 $|\psi_i\rangle$。其[密度算符](@entry_id:138151)是这些纯态[投影算符](@entry_id:154142)的加权平均：
$$
\hat{\rho} = \sum_i p_i |\psi_i\rangle\langle\psi_i|
$$
其中，概率 $p_i$ 必须满足 $p_i \ge 0$ 和 $\sum_i p_i = 1$。这个表达式优雅地将经典概率（$p_i$）与[量子态](@entry_id:146142)（$|\psi_i\rangle$）融合在一起。

考虑一个自旋1/2粒子的系综，由于制备装置的不完善，导致 $60\%$ 的粒子处于z轴方向的自旋向上态 $|\uparrow_z\rangle$，而另外 $40\%$ 的粒子处于x轴方向的自旋向上态 $|\uparrow_x\rangle$ [@problem_id:1403976]。这是一个典型的[混合态](@entry_id:141568)。其[密度算符](@entry_id:138151)为：
$$
\hat{\rho} = 0.6 \, |\uparrow_z\rangle\langle\uparrow_z| + 0.4 \, |\uparrow_x\rangle\langle\uparrow_x|
$$
为了在标准的z基底 $\{|\uparrow_z\rangle, |\downarrow_z\rangle\}$ 中写出其矩阵表示，我们需要将所有态用该基底表达。我们知道 $|\uparrow_z\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ 和 $|\uparrow_x\rangle = \frac{1}{\sqrt{2}}(|\uparrow_z\rangle + |\downarrow_z\rangle) = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix}$。对应的[投影矩阵](@entry_id:154479)是：
$$
|\uparrow_z\rangle\langle\uparrow_z| = \begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix}, \quad |\uparrow_x\rangle\langle\uparrow_x| = \frac{1}{2}\begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}
$$
将它们代入 $\hat{\rho}$ 的表达式中：
$$
\hat{\rho} = 0.6 \begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix} + 0.4 \cdot \frac{1}{2} \begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix} = \begin{pmatrix} 0.6 & 0 \\ 0 & 0 \end{pmatrix} + \begin{pmatrix} 0.2 & 0.2 \\ 0.2 & 0.2 \end{pmatrix} = \begin{pmatrix} 0.8 & 0.2 \\ 0.2 & 0.2 \end{pmatrix} = \begin{pmatrix} \frac{4}{5} & \frac{1}{5} \\ \frac{1}{5} & \frac{1}{5} \end{pmatrix}
$$
这就是描述该混合系综的密度矩阵。

### 物理态的判据：[密度矩阵](@entry_id:139892)的三个基本性质

并非任何一个矩阵都可以代表一个物理上可能的[量子态](@entry_id:146142)。一个算符 $\hat{\rho}$ 要成为一个合法的[密度算符](@entry_id:138151)，它必须满足以下三个基本条件：

1.  **[厄米性](@entry_id:141899) (Hermiticity)**: $\hat{\rho} = \hat{\rho}^\dagger$。这意味着密度矩阵等于其共轭转置，$\rho_{mn} = \rho_{nm}^*$。这个性质保证了所有[可观测量](@entry_id:267133)的[期望值](@entry_id:153208)都是实数。

2.  **单位迹 (Unit Trace)**: $\operatorname{Tr}(\hat{\rho}) = 1$。矩阵的迹（对角元素之和）必须为1。这对应于总概率归一化，即在所有可能的结果中找到系统的总概率为1。

3.  **正半定性 (Positive Semi-definiteness)**: $\hat{\rho} \ge 0$。这意味着对于任意态矢量 $|\phi\rangle$，$\langle\phi|\hat{\rho}|\phi\rangle \ge 0$。这等价于要求[密度矩阵](@entry_id:139892)的所有[本征值](@entry_id:154894) $\lambda_k$ 都必须是非负的，$\lambda_k \ge 0$。这个条件保证了任何测量结果的概率都是非负的。

我们可以通过检验一个给定的矩阵是否满足这三个条件来判断它是否能描述一个真实的物理状态 [@problem_id:1404013]。例如，考虑矩阵 $\rho = \begin{pmatrix} \frac{1}{2} & \frac{i}{\sqrt{3}} \\ -\frac{i}{\sqrt{3}} & \frac{1}{2} \end{pmatrix}$。
- **[厄米性](@entry_id:141899)**: 矩阵的[共轭转置](@entry_id:147909)为 $(\rho^\dagger)_{12} = \rho_{21}^* = (-\frac{i}{\sqrt{3}})^* = \frac{i}{\sqrt{3}} = \rho_{12}$，对角元为实数。所以，该矩阵是厄米矩阵。
- **单位迹**: $\operatorname{Tr}(\rho) = \frac{1}{2} + \frac{1}{2} = 1$。迹为1的条件也满足。
- **正半定性**: 我们需要计算其[本征值](@entry_id:154894)。本征方程为 $\det(\rho - \lambda I) = 0$：
$$
\det\begin{pmatrix} \frac{1}{2}-\lambda & \frac{i}{\sqrt{3}} \\ -\frac{i}{\sqrt{3}} & \frac{1}{2}-\lambda \end{pmatrix} = \left(\frac{1}{2}-\lambda\right)^2 - \left(\frac{i}{\sqrt{3}}\right)\left(-\frac{i}{\sqrt{3}}\right) = \left(\frac{1}{2}-\lambda\right)^2 - \frac{1}{3} = 0
$$
解得 $\lambda = \frac{1}{2} \pm \frac{1}{\sqrt{3}}$。由于 $\sqrt{3} \approx 1.732$，所以 $\frac{1}{\sqrt{3}} \approx 0.577 > \frac{1}{2}$。这意味着其中一个[本征值](@entry_id:154894) $\lambda_{-} = \frac{1}{2} - \frac{1}{\sqrt{3}}$ 是负数。因此，该矩阵不是正半定的，不能代表一个物理[量子态](@entry_id:146142)。

### 纯度：区分纯态与混合态

如何量化一个态的“混合程度”？一个非常有用的度量是**纯度 (purity)** $\mathcal{P}$，定义为[密度算符](@entry_id:138151)平方的迹：
$$
\mathcal{P} = \operatorname{Tr}(\hat{\rho}^2)
$$
对于一个纯态 $\hat{\rho} = |\psi\rangle\langle\psi|$ (其中 $\langle\psi|\psi\rangle = 1$)，我们有：
$$
\hat{\rho}^2 = (|\psi\rangle\langle\psi|)(|\psi\rangle\langle\psi|) = |\psi\rangle(\langle\psi|\psi\rangle)\langle\psi| = |\psi\rangle\langle\psi| = \hat{\rho}
$$
因此，纯态的[密度算符](@entry_id:138151)是幂等的。其纯度为 $\mathcal{P}_{\text{pure}} = \operatorname{Tr}(\hat{\rho}^2) = \operatorname{Tr}(\hat{\rho}) = 1$。

对于一个[混合态](@entry_id:141568)，情况则有所不同。可以证明，对于任何混合态，其纯度总是小于1。$1/d \le \mathcal{P}_{\text{mixed}} \lt 1$，其中 $d$ 是[希尔伯特空间](@entry_id:261193)的维度。纯度的最小值 $1/d$ 对应于**[最大混合态](@entry_id:137775)**，即所有[基态](@entry_id:150928)以均等概率混合，例如 $\hat{\rho} = \frac{1}{d}I$，其中 $I$ 是单位矩阵。

这个差异是一个区分[纯态](@entry_id:141688)和混合态的实用判据。例如，考虑一个自旋系综，其中75%的粒子处于自旋向上态 $|+\rangle_z$，25%处于自旋向下态 $|-\rangle_z$ [@problem_id:1404015]。其[密度矩阵](@entry_id:139892)是[对角化](@entry_id:147016)的：
$$
\hat{\rho} = 0.75 |+\rangle_z\langle+| + 0.25 |-\rangle_z\langle-| = \begin{pmatrix} 0.75 & 0 \\ 0 & 0.25 \end{pmatrix} = \begin{pmatrix} \frac{3}{4} & 0 \\ 0 & \frac{1}{4} \end{pmatrix}
$$
其平方为 $\hat{\rho}^2 = \begin{pmatrix} (3/4)^2 & 0 \\ 0 & (1/4)^2 \end{pmatrix} = \begin{pmatrix} 9/16 & 0 \\ 0 & 1/16 \end{pmatrix}$。
纯度为 $\mathcal{P} = \operatorname{Tr}(\hat{\rho}^2) = \frac{9}{16} + \frac{1}{16} = \frac{10}{16} = \frac{5}{8}$。由于 $\mathcal{P} = 5/8  1$，我们确认这是一个混合态。

纯度的概念深刻地揭示了量子相干叠加与经典统计混合的根本区别 [@problem_id:1404021]。考虑两种制备[量子比特](@entry_id:137928)的方案：
- **方案A**：制备一个纯的[相干叠加](@entry_id:170209)态 $|\psi_A\rangle = \frac{1}{\sqrt{2}}(|\alpha\rangle + |\beta\rangle)$。这是一个纯态，其[密度算符](@entry_id:138151) $\rho_A = |\psi_A\rangle\langle\psi_A|$，纯度 $\mathcal{P}_A = \operatorname{Tr}(\rho_A^2)=1$。
- **方案B**：制备一个统计混合态，其中 $50\%$ 的粒子在 $|\alpha\rangle$ 态，$50\%$ 在 $|\beta\rangle$ 态。其[密度算符](@entry_id:138151)为 $\rho_B = \frac{1}{2}|\alpha\rangle\langle\alpha| + \frac{1}{2}|\beta\rangle\langle\beta|$。在 $\{|\alpha\rangle, |\beta\rangle\}$ 基底下，$\rho_B = \frac{1}{2}I = \begin{pmatrix} 1/2  0 \\ 0  1/2 \end{pmatrix}$。这是一个[最大混合态](@entry_id:137775)。其纯度 $\mathcal{P}_B = \operatorname{Tr}(\rho_B^2) = \operatorname{Tr}(\frac{1}{4}I^2) = \frac{1}{4}\operatorname{Tr}(I) = \frac{1}{4} \cdot 2 = \frac{1}{2}$。

尽管方案A和B在某些测量下（例如在 $\{|\alpha\rangle, |\beta\rangle\}$ 基底下测量布居数）可能给出相同的结果（都是50/50的概率），但它们是本质上不同的状态。方案A的[纯态](@entry_id:141688)具有量子相 coherent 性，而方案B的[混合态](@entry_id:141568)则完全没有。纯度 $\mathcal{P}_A=1$ 和 $\mathcal{P}_B=1/2$ 清晰地反映了这一差异。

### [密度算符](@entry_id:138151)的应用：计算可观测量的[期望值](@entry_id:153208)

[密度算符](@entry_id:138151)最重要的用途之一是计算[可观测量](@entry_id:267133) $\hat{A}$ 的系综平均值（[期望值](@entry_id:153208)）。其通用公式为：
$$
\langle \hat{A} \rangle = \operatorname{Tr}(\hat{\rho}\hat{A})
$$
这个公式统一了纯态和混合态。对于纯态 $\hat{\rho} = |\psi\rangle\langle\psi|$，该公式回退到我们熟悉的形式：$\operatorname{Tr}(|\psi\rangle\langle\psi|\hat{A}) = \langle\psi|\hat{A}|\psi\rangle$（利用迹的循环[不变性](@entry_id:140168) $\operatorname{Tr}(ABC)=\operatorname{Tr}(CAB)$）。

对于[混合态](@entry_id:141568) $\hat{\rho} = \sum_i p_i |\psi_i\rangle\langle\psi_i|$，[期望值](@entry_id:153208)变为：
$$
\langle \hat{A} \rangle = \operatorname{Tr}\left(\sum_i p_i |\psi_i\rangle\langle\psi_i|\hat{A}\right) = \sum_i p_i \operatorname{Tr}(|\psi_i\rangle\langle\psi_i|\hat{A}) = \sum_i p_i \langle\psi_i|\hat{A}|\psi_i\rangle
$$
这正是对每个子系综的量子[期望值](@entry_id:153208)进行经典概率加权平均，完全符合我们的物理直觉。

例如，考虑一个由[无限深势阱](@entry_id:140940)中的粒子组成的系综，其中 $50\%$ 处于[基态](@entry_id:150928) ($n=1$)，$50\%$ 处于第一[激发态](@entry_id:261453) ($n=2$) [@problem_id:1403974]。单个粒子的[能量本征值](@entry_id:144381)为 $E_n = \frac{n^2 h^2}{8mL^2}$。该系综的[平均能量](@entry_id:145892) $\langle E \rangle$ 可以通过[期望值](@entry_id:153208)公式计算：
$$
\langle E \rangle = p_1 E_1 + p_2 E_2 = \frac{1}{2} E_1 + \frac{1}{2} E_2 = \frac{1}{2}\left(\frac{1^2 h^2}{8mL^2}\right) + \frac{1}{2}\left(\frac{2^2 h^2}{8mL^2}\right) = \frac{h^2}{16mL^2} + \frac{4h^2}{16mL^2} = \frac{5h^2}{16mL^2}
$$

#### 对角元与非对角元：布居与相干

密度矩阵的元素具有明确的物理意义。在一个给定的正交基 $\{|n\rangle\}$ 中：
- **对角元素 $\rho_{nn} = \langle n|\hat{\rho}|n \rangle$** 代表在系综中找到系统处于态 $|n\rangle$ 的**概率**，也称为**布居数 (population)**。由于 $\operatorname{Tr}(\hat{\rho})=1$，我们有 $\sum_n \rho_{nn} = 1$。
- **非对角元素 $\rho_{nm} = \langle n|\hat{\rho}|m \rangle$ ($n \neq m$)** 代表不同[基态](@entry_id:150928) $|n\rangle$ 和 $|m\rangle$ 之间的**量子相干性 (quantum coherence)**。这些复数值编码了系综中各个纯态分量在 $|n\rangle$ 和 $|m\rangle$ 之间的相对相位信息。如果所有非对角元素都为零，则密度矩阵在该基底下是退相干的。

非对角元素的存在与否直接关系到某些物理量的测量结果。考虑一个在z基底 $\{|0\rangle, |1\rangle\}$ 下表示的[密度矩阵](@entry_id:139892) $\hat{\rho} = \begin{pmatrix} \rho_{00}  \rho_{01} \\ \rho_{10}  \rho_{11} \end{pmatrix}$。如果我们想测量x方向的[自旋极化](@entry_id:164038)，对应的算符是[泡利矩阵](@entry_id:139493) $\hat{\sigma}_x = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$。其[期望值](@entry_id:153208)为 [@problem_id:1403981]：
$$
\langle \hat{\sigma}_x \rangle = \operatorname{Tr}(\hat{\rho}\hat{\sigma}_x) = \operatorname{Tr}\left(\begin{pmatrix} \rho_{00}  \rho_{01} \\ \rho_{10}  \rho_{11} \end{pmatrix}\begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}\right) = \operatorname{Tr}\begin{pmatrix} \rho_{01}  \rho_{00} \\ \rho_{11}  \rho_{10} \end{pmatrix} = \rho_{01} + \rho_{10}
$$
由于 $\rho$ 是[厄米矩阵](@entry_id:155147)，$\rho_{10} = \rho_{01}^*$，所以 $\langle \hat{\sigma}_x \rangle = \rho_{01} + \rho_{01}^* = 2\text{Re}(\rho_{01})$。类似地，可以证明 $\langle \hat{\sigma}_y \rangle = 2\text{Im}(\rho_{01})$ 以及 $\langle \hat{\sigma}_z \rangle = \rho_{00} - \rho_{11}$。

这个结果揭示了一个深刻的联系：
- 对角元素（布居数之差）决定了与基底对易的[可观测量](@entry_id:267133)（如 $\hat{\sigma}_z$）的[期望值](@entry_id:153208)。
- 非对角元素（相干项）决定了那些会引起[基态](@entry_id:150928)之间跃迁的[可观测量](@entry_id:267133)（如 $\hat{\sigma}_x, \hat{\sigma}_y$）的[期望值](@entry_id:153208)。如果一个[密度矩阵](@entry_id:139892)在某个基底下是对角的，那么在该基底下所有非对角的算符的[期望值](@entry_id:153208)都将为零。

### [量子态](@entry_id:146142)的完备描述

[密度算符](@entry_id:138151)的一个惊人之处在于，它包含了关于一个量子系统所有可能通过测量获得的信息。这意味着，如果两个通过完全不同的物理过程制备的系综，恰好具有相同的[密度算符](@entry_id:138151)，那么它们在**任何**物理测量下都是不可区分的。

一个经典的例子可以说明这一点 [@problem_id:1403954]。考虑两个系综：
- **系综 A**：$50\%$ 的粒子处于 $|+\rangle_z$ 态，$50\%$ 处于 $|-\rangle_z$ 态。
- **系综 B**：$50\%$ 的粒子处于 $|+\rangle_x$ 态，$50\%$ 处于 $|-\rangle_x$ 态。

我们来计算它们的[密度矩阵](@entry_id:139892)。
对于系综 A：
$$
\hat{\rho}_A = \frac{1}{2}|+\rangle_z\langle+|_z + \frac{1}{2}|-\rangle_z\langle-|_z = \frac{1}{2}\begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix} + \frac{1}{2}\begin{pmatrix} 0  0 \\ 0  1 \end{pmatrix} = \frac{1}{2}\begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} = \frac{1}{2}I
$$
对于系综 B，我们先将x基底的投影算符用z基底表示：
$|+\rangle_x\langle+|_x = \frac{1}{2}(|+\rangle_z + |-\rangle_z)(\langle+|_z + \langle-|_z) = \frac{1}{2}(|+\rangle_z\langle+|_z + |-\rangle_z\langle-|_z + |+\rangle_z\langle-|_z + |-\rangle_z\langle+|_z)$
$|-\rangle_x\langle-|_x = \frac{1}{2}(|+\rangle_z - |-\rangle_z)(\langle+|_z - \langle-|_z) = \frac{1}{2}(|+\rangle_z\langle+|_z + |-\rangle_z\langle-|_z - |+\rangle_z\langle-|_z - |-\rangle_z\langle+|_z)$
将两者相加，非对角项（相干项）恰好抵消：
$$
\hat{\rho}_B = \frac{1}{2}(|+\rangle_x\langle+|_x) + \frac{1}{2}(|-\rangle_x\langle-|_x) = \frac{1}{2}(|+\rangle_z\langle+|_z + |-\rangle_z\langle-|_z) = \frac{1}{2}I
$$
两个系综的密度矩阵完全相同！这意味着，尽管它们的制备历史截然不同，但没有任何实验手段可以区分它们。对任何[可观测量](@entry_id:267133) $\hat{O}$，它们的[期望值](@entry_id:153208)都是一样的：$\langle \hat{O} \rangle_A = \operatorname{Tr}(\frac{1}{2}I\hat{O}) = \frac{1}{2}\operatorname{Tr}(\hat{O})$ 和 $\langle \hat{O} \rangle_B = \operatorname{Tr}(\frac{1}{2}I\hat{O}) = \frac{1}{2}\operatorname{Tr}(\hat{O})$。这强有力地证明了[密度算符](@entry_id:138151)是[量子态](@entry_id:146142)的最终、最完备的描述符，任何在此之外的“隐藏信息”（如每个粒子的具体来源）都是物理上不可观测的。

### 子系统与纠缠：[约化密度算符](@entry_id:190449)

[密度算符](@entry_id:138151)在处理复合系统的子系统时显示出其不可或缺的价值。当一个复合系统 AB 处于[纠缠态](@entry_id:152310)时，即使整个系统处于纯态 $|\Psi_{AB}\rangle$，其子系统 A 或 B 通常都处于混合态。为了描述子系统A的状态，我们需要引入**[约化密度算符](@entry_id:190449) (reduced density operator)** $\hat{\rho}_A$。

$\hat{\rho}_A$ 是通过对复合系统的总[密度算符](@entry_id:138151) $\hat{\rho}_{AB}$ 求关于子系统B自由度的**[偏迹](@entry_id:146482) (partial trace)** 得到的：
$$
\hat{\rho}_A = \operatorname{Tr}_B(\hat{\rho}_{AB})
$$
[偏迹](@entry_id:146482) $\operatorname{Tr}_B$ 的操作可以理解为“平均掉”或“忽略”B系统的所有可能性。具体而言，如果 $\{|b_j\rangle\}$ 是B系统的一组正交归一基，那么[偏迹](@entry_id:146482)操作定义为：
$$
\hat{\rho}_A = \sum_j \langle b_j | \hat{\rho}_{AB} | b_j \rangle
$$
其中 $\langle b_j | \cdot | b_j \rangle$ 是作用在B系统希尔伯特空间上的[内积](@entry_id:158127)，其结果仍然是A系统上的一个算符。

考虑一个由两个自旋1/2粒子组成的系统，处于纯的[纠缠态](@entry_id:152310) $|\Psi\rangle = \sqrt{\frac{2}{3}}|\alpha_1\alpha_2\rangle + \sqrt{\frac{1}{3}}|\beta_1\beta_2\rangle$ [@problem_id:1403993]。
首先，构建整个系统的[密度算符](@entry_id:138151) $\hat{\rho}_{12} = |\Psi\rangle\langle\Psi|$:
$$
\hat{\rho}_{12} = \left(\sqrt{\frac{2}{3}}|\alpha_1\alpha_2\rangle + \sqrt{\frac{1}{3}}|\beta_1\beta_2\rangle\right)\left(\sqrt{\frac{2}{3}}\langle\alpha_1\alpha_2| + \sqrt{\frac{1}{3}}\langle\beta_1\beta_2|\right) \\
= \frac{2}{3}|\alpha_1\alpha_2\rangle\langle\alpha_1\alpha_2| + \frac{1}{3}|\beta_1\beta_2\rangle\langle\beta_1\beta_2| + \frac{\sqrt{2}}{3}|\alpha_1\alpha_2\rangle\langle\beta_1\beta_2| + \frac{\sqrt{2}}{3}|\beta_1\beta_2\rangle\langle\alpha_1\alpha_2|
$$
现在，我们通过对粒子2的自由度求[偏迹](@entry_id:146482)来找到粒子1的[约化密度算符](@entry_id:190449) $\hat{\rho}_1$。粒子2的[基矢](@entry_id:199546)是 $\{|\alpha_2\rangle, |\beta_2\rangle\}$。
$$
\hat{\rho}_1 = \operatorname{Tr}_2(\hat{\rho}_{12}) = \langle\alpha_2|\hat{\rho}_{12}|\alpha_2\rangle + \langle\beta_2|\hat{\rho}_{12}|\beta_2\rangle
$$
利用[基矢](@entry_id:199546)的正交性（例如 $\langle\alpha_2|\beta_2\rangle=0, \langle\alpha_2|\alpha_2\rangle=1$），我们逐项计算：
$\langle\alpha_2| \left( \frac{2}{3}|\alpha_1\alpha_2\rangle\langle\alpha_1\alpha_2| \right) |\alpha_2\rangle = \frac{2}{3}|\alpha_1\rangle\langle\alpha_1|$
$\langle\beta_2| \left( \frac{1}{3}|\beta_1\beta_2\rangle\langle\beta_1\beta_2| \right) |\beta_2\rangle = \frac{1}{3}|\beta_1\rangle\langle\beta_1|$
所有交叉项（如 $\langle\alpha_2| (|\alpha_1\alpha_2\rangle\langle\beta_1\beta_2|) |\alpha_2\rangle$）都因 $\langle\alpha_2||\beta_1\beta_2\rangle = |\beta_1\rangle\langle\alpha_2|\beta_2\rangle=0$ 而消失。
因此，粒子1的[约化密度算符](@entry_id:190449)为：
$$
\hat{\rho}_1 = \frac{2}{3}|\alpha_1\rangle\langle\alpha_1| + \frac{1}{3}|\beta_1\rangle\langle\beta_1| = \begin{pmatrix} 2/3  0 \\ 0  1/3 \end{pmatrix}
$$
这是一个[对角矩阵](@entry_id:637782)，代表一个[混合态](@entry_id:141568)！尽管整个系统是纯态，但子系统1却处于一个有 $2/3$ 概率为自旋向上，$1/3$ 概率为自旋向下的混合态。这就是纠缠的本质：信息存在于粒子间的关联中，而不是单个粒子上。

一旦我们有了[约化密度算符](@entry_id:190449) $\hat{\rho}_1$，我们就可以计算任何只作用于粒子1的可观测量的[期望值](@entry_id:153208)。例如，粒子1的z方向自旋角动量 $\hat{S}_{1z}$ 的[期望值](@entry_id:153208)是：
$$
\langle \hat{S}_{1z} \rangle = \operatorname{Tr}_1(\hat{\rho}_1 \hat{S}_{1z}) = \operatorname{Tr}\left[ \left(\frac{2}{3}|\alpha_1\rangle\langle\alpha_1| + \frac{1}{3}|\beta_1\rangle\langle\beta_1|\right) \hat{S}_{1z} \right]
$$
由于 $\hat{S}_{1z}|\alpha_1\rangle = \frac{\hbar}{2}|\alpha_1\rangle$ 和 $\hat{S}_{1z}|\beta_1\rangle = -\frac{\hbar}{2}|\beta_1\rangle$，我们得到：
$$
\langle \hat{S}_{1z} \rangle = \operatorname{Tr}\left[ \frac{2}{3}\frac{\hbar}{2}|\alpha_1\rangle\langle\alpha_1| - \frac{1}{3}\frac{\hbar}{2}|\beta_1\rangle\langle\beta_1| \right] = \frac{2}{3}\frac{\hbar}{2} - \frac{1}{3}\frac{\hbar}{2} = \frac{\hbar}{6}
$$
这个结果与直接在复合系统态上计算 $\langle\Psi|\hat{S}_{1z}|\Psi\rangle$ 的结果完全一致，但[约化密度算符](@entry_id:190449)的方法更为通用和系统化。

### [密度算符](@entry_id:138151)的[时间演化](@entry_id:153943)：刘维尔-[冯·诺依曼方程](@entry_id:153472)

[密度算符](@entry_id:138151)的时间演化由**刘维尔-[冯·诺依曼方程](@entry_id:153472) (Liouville-von Neumann equation)** 描述：
$$
\frac{d\hat{\rho}}{dt} = -\frac{i}{\hbar}[\hat{H}, \hat{\rho}] = -\frac{i}{\hbar}(\hat{H}\hat{\rho} - \hat{\rho}\hat{H})
$$
这个方程是量子力学中的基本动力学方程，等价于薛定谔方程，但其形式更适合于[统计系综](@entry_id:149738)。

对于一个时间无关的[哈密顿量](@entry_id:172864) $\hat{H}$，其形式解为：
$$
\hat{\rho}(t) = \hat{U}(t)\hat{\rho}(0)\hat{U}^\dagger(t)
$$
其中 $\hat{U}(t) = \exp(-i\hat{H}t/\hbar)$ 是[时间演化算符](@entry_id:196774)。

一个极其重要的特例是**定态 (stationary state)**。如果一个系统的初始[密度算符](@entry_id:138151) $\hat{\rho}(0)$ 与[哈密顿量](@entry_id:172864) $\hat{H}$ 对易（commute），即 $[\hat{H}, \hat{\rho}(0)] = 0$，那么：
$$
\frac{d\hat{\rho}}{dt} = -\frac{i}{\hbar}[\hat{H}, \hat{\rho}] = 0
$$
这意味着[密度算符](@entry_id:138151)不随时间变化，$\hat{\rho}(t) = \hat{\rho}(0)$。这样的系统处于平衡状态。

一个常见且重要的[定态](@entry_id:137260)是当系统被制备为[哈密顿量](@entry_id:172864)本征态的统计混合时 [@problem_id:1404022]。假设 $\hat{H}|\psi_n\rangle = E_n|\psi_n\rangle$，初始态为 $\hat{\rho}(0) = \sum_n p_n |\psi_n\rangle\langle\psi_n|$。由于 $\hat{H}$ 和每个[投影算符](@entry_id:154142) $|\psi_n\rangle\langle\psi_n|$ 都对易，所以 $\hat{H}$ 与它们的[线性组合](@entry_id:154743) $\hat{\rho}(0)$ 也对易。因此，这样的系综是[定态](@entry_id:137260)，其布居数 $p_n$ 和为零的相干项将永远保持不变。这解释了为何处于[热平衡](@entry_id:141693)的系统（其状态由玻尔兹曼分布的[能量本征态](@entry_id:152154)混合而成）是稳定的。

如果在[能量本征态](@entry_id:152154)基底下，初始[密度矩阵](@entry_id:139892)存在非对角元素 $\rho_{nm}(0) \neq 0$，那么这些相干项将会随[时间演化](@entry_id:153943)：
$$
\rho_{nm}(t) = \langle\psi_n|\hat{\rho}(t)|\psi_m\rangle = \langle\psi_n|\hat{U}(t)\hat{\rho}(0)\hat{U}^\dagger(t)|\psi_m\rangle = e^{-i(E_n-E_m)t/\hbar} \rho_{nm}(0)
$$
这意味着相干项会以对应能量差的频率 $(E_n - E_m)/\hbar$ 进行[振荡](@entry_id:267781)，而对角项（布居数）$\rho_{nn}(t) = \rho_{nn}(0)$ 保持不变。这种相干[振荡](@entry_id:267781)是量子动力学中许多现象（如[量子拍](@entry_id:155286)）的根源。