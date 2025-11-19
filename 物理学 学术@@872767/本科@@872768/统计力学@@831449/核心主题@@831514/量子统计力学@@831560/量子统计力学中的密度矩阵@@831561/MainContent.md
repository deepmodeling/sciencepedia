## 引言
在量子力学的世界里，单个[孤立系统](@entry_id:159201)的行为可以通过一个态矢量 $|\psi\rangle$ 来精确描述，这被称为“纯态”。然而，当我们从单个粒子转向由无数粒子组成的宏观系统，或者当系统不可避免地与环境相互作用时，这种理想化的描述便不再足够。我们常常无法确切知道系统的精确状态，而只能知道它以一定概率处于一系列可能状态中的某一个。如何在一个统一的框架内，既保留[量子叠加](@entry_id:137914)的特性，又容纳这种经典统计的不确定性？这正是[量子统计力学](@entry_id:140244)所面临的核心问题。

为了解决这一难题，物理学家引入了“密度矩阵”这一强大概念。[密度矩阵](@entry_id:139892)不仅是描述混合态的数学工具，更是连接微观量子世界与宏观[热力学](@entry_id:141121)世界的关键桥梁。本文将系统地引导读者掌握[密度矩阵](@entry_id:139892)。在“原理与机制”一章中，我们将学习如何构建密度矩阵，探索其必须满足的基本数学性质，并了解如何用它来计算物理量的[期望值](@entry_id:153208)和区分[纯态](@entry_id:141688)与混合态。随后，在“应用与跨学科连接”一章中，我们将见证密度矩阵在[计算热力学](@entry_id:148023)性质、[量子信息](@entry_id:137721)、多体物理等前沿领域的广泛应用，揭示其作为现代物理学通用语言的强大威力。最后，“动手实践”一章将提供具体的计算问题，帮助读者巩固理论知识，将抽象概念付诸实践。

## 原理与机制

在量子力学的基础框架中，一个[孤立系统](@entry_id:159201)的状态由[希尔伯特空间](@entry_id:261193)中的一个态矢量 $|\psi\rangle$ 完美描述。这种描述适用于“[纯态](@entry_id:141688)”——即我们对系统的[量子态](@entry_id:146142)拥有完全确定的知识。然而，在[统计力](@entry_id:194984)学领域，我们通常处理的是宏观系统，或是与环境有相互作用的系统。在这些情况下，我们往往无法精确知道系统的确切[量子态](@entry_id:146142)。取而代之的是，我们可能知道系统处于一系列可能的[纯态](@entry_id:141688) $|\psi_i\rangle$ 中的某一个，每个纯态出现的概率为 $p_i$。这种不确定性并非源于[量子叠加](@entry_id:137914)，而是源于我们知识的欠缺。这种由多个[纯态](@entry_id:141688)按照经典概率组成的统计混合体，被称为“[混合态](@entry_id:141568)”。为了描述这种更普遍的情况，我们需要引入一个更为强大的数学工具——**[密度矩阵](@entry_id:139892)**（或[密度算符](@entry_id:138151)），记为 $\hat{\rho}$。

### [密度矩阵](@entry_id:139892)的构建：从纯态到[混合态](@entry_id:141568)

[密度算符](@entry_id:138151)的核心思想是将量子态的叠加原理与经典概率的统计平均结合起来。对于一个处于纯态 $|\psi\rangle$ 的系统，其[密度算符](@entry_id:138151)被定义为一个投影算符：
$$
\hat{\rho} = |\psi\rangle\langle\psi|
$$
这个算符包含了关于该纯态的所有信息。

现在，考虑一个[统计系综](@entry_id:149738)，其中系统有 $p_1$ 的概率处于[纯态](@entry_id:141688) $|\psi_1\rangle$，有 $p_2$ 的概率处于纯态 $|\psi_2\rangle$，以此类推，且满足概率[归一化条件](@entry_id:156486) $\sum_i p_i = 1$。描述这个[混合态](@entry_id:141568)的[密度算符](@entry_id:138151)就是这些纯态投影算符的加权平均：
$$
\hat{\rho} = \sum_i p_i |\psi_i\rangle\langle\psi_i|
$$
这个定义是[量子统计力学](@entry_id:140244)的基石。它优雅地将我们对系统状态的经典无知（由概率 $p_i$ 体现）与每个可能状态的量子特性（由态矢量 $|\psi_i\rangle$ 体现）融合在一个统一的数学对象中。

举一个具体的例子，假设一个实验设备产生一束自旋-1/2粒子。由于制备过程不完美，粒子束是一个[统计系综](@entry_id:149738)：其中60%的粒子处于z轴方向的自旋向上态 $|+Z\rangle$，其余40%处于x轴方向的自旋向上态 $|+X\rangle$ [@problem_id:1999444]。为了构建该系综的密度矩阵，我们首先需要写出这两个纯态的[密度算符](@entry_id:138151)，并按照其概率进行加权求和。

在以 $|+Z\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ 和 $|-Z\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$ 为[基矢](@entry_id:199546)的标准z基中，我们有：
- $|+Z\rangle$ 态的[投影算符](@entry_id:154142)为 $|+Z\rangle\langle+Z| \leftrightarrow \begin{pmatrix} 1  & 0 \\ 0  & 0 \end{pmatrix}$。
- $|+X\rangle$ 态可以表示为 $|+X\rangle = \frac{1}{\sqrt{2}}(|+Z\rangle + |-Z\rangle)$，其投影算符为 $|+X\rangle\langle+X| \leftrightarrow \frac{1}{2} \begin{pmatrix} 1  & 1 \\ 1  & 1 \end{pmatrix}$。

根据[混合态](@entry_id:141568)的定义，该粒子束的[密度矩阵](@entry_id:139892) $\hat{\rho}$ 为：
$$
\hat{\rho} = 0.6 \, |+Z\rangle\langle+Z| + 0.4 \, |+X\rangle\langle+X|
$$
将其转换为矩阵形式：
$$
\hat{\rho} \leftrightarrow 0.6 \begin{pmatrix} 1  & 0 \\ 0  & 0 \end{pmatrix} + 0.4 \left( \frac{1}{2} \begin{pmatrix} 1  & 1 \\ 1  & 1 \end{pmatrix} \right) = \begin{pmatrix} 0.6  & 0 \\ 0  & 0 \end{pmatrix} + \begin{pmatrix} 0.2  & 0.2 \\ 0.2  & 0.2 \end{pmatrix} = \begin{pmatrix} 0.8  & 0.2 \\ 0.2  & 0.2 \end{pmatrix}
$$
这个 $2 \times 2$ 矩阵 $\begin{pmatrix} \frac{4}{5}  & \frac{1}{5} \\ \frac{1}{5}  & \frac{1}{5} \end{pmatrix}$ 就是该自旋系综的完整描述。

### [密度矩阵](@entry_id:139892)的基本性质

任何一个代表物理[量子态](@entry_id:146142)的[密度矩阵](@entry_id:139892)，无论它是纯态还是[混合态](@entry_id:141568)，都必须满足三个基本性质。这三个性质确保了从密度矩阵中提取的物理预测（如测量概率和[期望值](@entry_id:153208)）是自洽且有意义的。

1.  **[厄米性](@entry_id:141899) (Hermiticity)**: $\hat{\rho} = \hat{\rho}^\dagger$。密度矩阵必须是厄米算符，即它等于其自身的[共轭转置](@entry_id:147909)。这个性质保证了[可观测量](@entry_id:267133)的[期望值](@entry_id:153208)是实数。

2.  **单位迹 (Unit Trace)**: $\text{Tr}(\hat{\rho}) = 1$。[矩阵的迹](@entry_id:139694)（对角线元素之和）必须为1。这个性质是概率[归一化条件](@entry_id:156486)的直接体现。因为密度矩阵的对角线元素 $\rho_{nn} = \langle n | \hat{\rho} | n \rangle$ 代表在[基态](@entry_id:150928) $|n\rangle$ 上找到系统的概率，所有可能结果的概率之和必须为1。在某些情况下，一个算符可能满足[厄米性](@entry_id:141899)，但迹不为1。这时，只要其迹为正，我们就可以通过归一化得到一个合法的[密度矩阵](@entry_id:139892)。例如，给定一个厄米矩阵 $\hat{M}(x) = \begin{pmatrix} 2  & ix \\ -ix  & 1 \end{pmatrix}$，它的迹是 $\text{Tr}(\hat{M}(x)) = 3$。为了得到一个物理态，我们必须将其归一化，定义 $\hat{\rho}(x) = \frac{1}{\text{Tr}(\hat{M}(x))} \hat{M}(x) = \frac{1}{3} \hat{M}(x)$，这样处理后 $\text{Tr}(\hat{\rho}(x)) = 1$ 就得到了满足 [@problem_id:1999490]。

3.  **正半定性 (Positive Semi-definiteness)**: $\hat{\rho} \ge 0$。这意味着[密度矩阵](@entry_id:139892)的所有[本征值](@entry_id:154894) $\lambda_i$ 都必须是非负的，即 $\lambda_i \ge 0$。这个性质的物理意义至关重要：它保证了任何测量的概率都不会是负数。对于任意一个纯态 $|\phi\rangle$，系统被发现处于该状态的概率是 $\langle\phi|\hat{\rho}|\phi\rangle$。正半定性保证了这个值为非负。由于[密度矩阵的本征值](@entry_id:204442)可以被看作是在其本征基下的[概率分布](@entry_id:146404)，因此它们也必须是非负的。

仅仅满足[厄米性](@entry_id:141899)和单位迹是不够的。考虑一个矩阵 $\hat{\rho}_{\text{prop}} = \begin{pmatrix} 0.9  & 0.4 \\ 0.4  & 0.1 \end{pmatrix}$ [@problem_id:1999466]。它显然是厄米矩阵，并且其迹 $\text{Tr}(\hat{\rho}_{\text{prop}}) = 0.9 + 0.1 = 1$。然而，它并非一个合法的密度矩阵。要验证这一点，我们需要计算它的[本征值](@entry_id:154894)。[本征值方程](@entry_id:192306)为 $\lambda^2 - \text{Tr}(\hat{\rho})\lambda + \det(\hat{\rho}) = 0$。这里，$\det(\hat{\rho}_{\text{prop}}) = (0.9)(0.1) - (0.4)(0.4) = 0.09 - 0.16 = -0.07$。因此，[本征值](@entry_id:154894)为 $\lambda = \frac{1 \pm \sqrt{1^2 - 4(-0.07)}}{2} = \frac{1 \pm \sqrt{1.28}}{2}$。其中一个[本征值](@entry_id:154894)约为 $\frac{1 - 1.131}{2} \approx -0.0657$，是负数。这意味着这个矩阵不满足正半定性，因此不能代表任何物理上可实现的[量子态](@entry_id:146142)。

### [期望值](@entry_id:153208)计算与矩阵元的物理诠释

密度矩阵的一个核心用途是计算任意可观测量 $\hat{A}$ 的系综平均[期望值](@entry_id:153208)。这个[期望值](@entry_id:153208)由以下公式给出：
$$
\langle \hat{A} \rangle = \text{Tr}(\hat{\rho} \hat{A})
$$
这个公式的优雅之处在于它提供了一个不依赖于特定表象的普适计算方法。为了理解其内在逻辑，我们可以回到[混合态](@entry_id:141568)的定义。[期望值](@entry_id:153208)是各个纯态[期望值](@entry_id:153208)的统计平均：
$$
\langle \hat{A} \rangle = \sum_i p_i \langle \psi_i | \hat{A} | \psi_i \rangle
$$
利用迹的循环[不变性](@entry_id:140168) ($\text{Tr}(XYZ) = \text{Tr}(ZXY)$)，我们可以证明这与迹公式等价：
$$
\text{Tr}(\hat{\rho} \hat{A}) = \text{Tr}\left(\left(\sum_i p_i |\psi_i\rangle\langle\psi_i|\right) \hat{A}\right) = \sum_i p_i \text{Tr}(|\psi_i\rangle\langle\psi_i| \hat{A}) = \sum_i p_i \text{Tr}(\langle\psi_i| \hat{A} |\psi_i\rangle) = \sum_i p_i \langle \psi_i | \hat{A} | \psi_i \rangle
$$
在任意一组[正交基](@entry_id:264024) $\{|n\rangle\}$ 中，迹可以被展开为[矩阵元](@entry_id:186505)素之和：
$$
\langle \hat{A} \rangle = \text{Tr}(\hat{\rho} \hat{A}) = \sum_n \langle n | \hat{\rho} \hat{A} | n \rangle = \sum_{n,m} \langle n | \hat{\rho} | m \rangle \langle m | \hat{A} | n \rangle = \sum_{n,m} \rho_{nm} A_{mn}
$$
其中 $\rho_{nm} = \langle n | \hat{\rho} | m \rangle$ 和 $A_{mn} = \langle m | \hat{A} | n \rangle$ 分别是 $\hat{\rho}$ 和 $\hat{A}$ 在该基下的[矩阵元](@entry_id:186505)。这个表达式在实际计算中非常有用 [@problem_id:1999448]。

[密度矩阵](@entry_id:139892)的矩阵元本身也具有深刻的物理意义：
- **对角元 $\rho_{nn}$**: $\rho_{nn} = \langle n | \hat{\rho} | n \rangle$ 代表在系综中随机选取一个系统，测量发现在[基态](@entry_id:150928) $|n\rangle$ 的概率。因此，对角元被称为**布居数 (populations)**。
- **非对角元 $\rho_{nm}$ ($n \neq m$)**: 非对角元 $\rho_{nm}$ 描述了[基态](@entry_id:150928) $|n\rangle$ 和 $|m\rangle$ 之间的**量子相干性 (quantum coherence)**。如果一个[密度矩阵](@entry_id:139892)在某个基下（例如能量本征基）的非对角元不为零，这直接意味着系统状态包含了该基底下不同态的量子叠加 [@problem_id:1959542]。一个仅由能量本征态构成的统计混合系综，其密度矩阵在能量本征基下是纯对角的，所有非对角元均为零。反之，任何非零的非对角元都标志着能量本征态之间存在[相干叠加](@entry_id:170209)，系统并未处于一个稳定的能量本征态混合中。

### [纯态](@entry_id:141688)与混合态的甄别：纯度

一个关键问题是：给定一个[密度矩阵](@entry_id:139892) $\hat{\rho}$，我们如何判断它描述的是一个纯态还是一个[混合态](@entry_id:141568)？
一个看似简单的例子可以揭示其中的微妙之处。考虑两个实验：
- **实验室A**：制备一个统计[混合态](@entry_id:141568)，其中50%的粒子处于 $|+X\rangle$ 态，50%处于 $|-X\rangle$ 态。
- **实验室B**：制备一个[纯态](@entry_id:141688)，所有粒子都处于 $|+Z\rangle$ 态。

实验室A的[密度矩阵](@entry_id:139892)为 $\hat{\rho}_A = \frac{1}{2}|+X\rangle\langle+X| + \frac{1}{2}|-X\rangle\langle-X| = \frac{1}{2} I = \begin{pmatrix} 1/2  & 0 \\ 0  & 1/2 \end{pmatrix}$。
实验室B的[密度矩阵](@entry_id:139892)为 $\hat{\rho}_B = |+Z\rangle\langle+Z| = \begin{pmatrix} 1  & 0 \\ 0  & 0 \end{pmatrix}$。
这两个[密度矩阵](@entry_id:139892)截然不同，代表着完全不同的物理状态。前者是完全无极化的混合态，后者是一个确定的[纯态](@entry_id:141688)。

一个量化这种差异的指标是**纯度 (purity)**，定义为 $P = \text{Tr}(\hat{\rho}^2)$。
- 对于一个**[纯态](@entry_id:141688)** $\hat{\rho} = |\psi\rangle\langle\psi|$，由于[投影算符](@entry_id:154142)的[幂等性](@entry_id:190768) $\hat{\rho}^2 = (|\psi\rangle\langle\psi|)(|\psi\rangle\langle\psi|) = |\psi\rangle\langle\psi| = \hat{\rho}$，其纯度为 $P = \text{Tr}(\hat{\rho}^2) = \text{Tr}(\hat{\rho}) = 1$。
- 对于一个**混合态**，其纯度总是小于1。如果 $\hat{\rho}$ 的[本征值](@entry_id:154894)为 $\lambda_i$（即概率），那么 $\text{Tr}(\hat{\rho}^2) = \sum_i \lambda_i^2$。由于 $\sum_i \lambda_i = 1$ 且 $0 \le \lambda_i \le 1$，我们可以证明 $\sum_i \lambda_i^2 \le (\sum_i \lambda_i)^2 = 1$，除非只有一个 $\lambda_i=1$（[纯态](@entry_id:141688)情况）。

回到上面的例子 [@problem_id:1999477]：
- 实验室A的纯度为 $\text{Tr}(\hat{\rho}_A^2) = \text{Tr}(\frac{1}{4}I^2) = \frac{1}{4}\text{Tr}(I) = \frac{1}{4} \times 2 = \frac{1}{2}$。因为 $P  1$，它是一个混合态。
- 实验室B的纯度为 $\text{Tr}(\hat{\rho}_B^2) = \text{Tr}(\hat{\rho}_B) = 1$。因为 $P = 1$，它是一个纯态。

因此，纯度 $\text{Tr}(\hat{\rho}^2)$ 是一个有效的判据：
- $\text{Tr}(\hat{\rho}^2) = 1$ $\iff$ 系统处于纯态。
- $\text{Tr}(\hat{\rho}^2)  1$ $\iff$ 系统处于[混合态](@entry_id:141568)。
对于一个$d$维系统，纯度的取值范围是 $\frac{1}{d} \le \text{Tr}(\hat{\rho}^2) \le 1$。其中，最小纯度 $\frac{1}{d}$ 对应于[最大混合态](@entry_id:137775) $\hat{\rho} = \frac{1}{d}I$。
我们可以应用这个判据来分析一个给定的[量子态](@entry_id:146142)，例如 $\hat{\rho} = \begin{pmatrix} 3/4   i/4 \\ -i/4   1/4 \end{pmatrix}$ [@problem_id:1999480]。计算其平方：
$$
\hat{\rho}^2 = \begin{pmatrix} 3/4   i/4 \\ -i/4   1/4 \end{pmatrix} \begin{pmatrix} 3/4   i/4 \\ -i/4   1/4 \end{pmatrix} = \begin{pmatrix} (9/16) + (1/16)   3i/16 + i/16 \\ -3i/16 - i/16   (1/16) + 1/16 \end{pmatrix} = \begin{pmatrix} 10/16   4i/16 \\ -4i/16   2/16 \end{pmatrix}
$$
其迹为 $\text{Tr}(\hat{\rho}^2) = \frac{10}{16} + \frac{2}{16} = \frac{12}{16} = \frac{3}{4}$。由于纯度 $\frac{3}{4}  1$，该状态是一个混合态。

### 子系统与纠缠：[约化密度矩阵](@entry_id:146315)

当一个量子系统由多个部分组成时（例如，一个由粒子A和粒子B组成的双[粒子系统](@entry_id:180557)），我们常常只对其中一个子系统（比如粒子A）感兴趣。即使整个复合系统 $AB$ 处于一个[纯态](@entry_id:141688) $|\Psi\rangle_{AB}$，我们如何描述子系统A的状态呢？答案是通过**[约化密度矩阵](@entry_id:146315) (reduced density matrix)** $\hat{\rho}_A$。

[约化密度矩阵](@entry_id:146315)是通过在复合系统的总密度矩阵 $\hat{\rho}_{AB}$ 上对我们不感兴趣的子系统（B）的自由度求**[偏迹](@entry_id:146482) (partial trace)** 得到的：
$$
\hat{\rho}_A = \text{Tr}_B(\hat{\rho}_{AB})
$$
具体而言，如果 $\{|b_k\rangle\}$ 是子系统B的一组标准正交基，[偏迹](@entry_id:146482)操作定义为：
$$
\hat{\rho}_A = \sum_k \langle b_k |_B \, \hat{\rho}_{AB} \, |b_k\rangle_B
$$
这个操作可以直观地理解为“平均掉”或“忽略”子系统B的所有信息，只保留与子系统A相关的统计信息。$\hat{\rho}_A$ 包含了所有仅通过测量子系统A就能获得的信息。

一个惊人且深刻的后果是，即使整个系统处于纯态，其子系统也可能处于混合态。这正是**[量子纠缠](@entry_id:136576) (quantum entanglement)** 的一个核心特征。考虑一个由两个[量子比特](@entry_id:137928)组成的复合系统，它处于一个纠缠[纯态](@entry_id:141688) $|\psi\rangle = \frac{1}{\sqrt{5}} (2 |00\rangle + i |11\rangle)$ [@problem_id:1999486]。整个系统的[密度矩阵](@entry_id:139892)是 $\hat{\rho} = |\psi\rangle\langle\psi|$。为了得到子系统A的[约化密度矩阵](@entry_id:146315)，我们对B的自由度求[偏迹](@entry_id:146482)：
$$
\hat{\rho}_A = \text{Tr}_B(|\psi\rangle\langle\psi|) = \frac{1}{5} \text{Tr}_B \left( 4|00\rangle\langle00| - 2i|00\rangle\langle11| + 2i|11\rangle\langle00| + |11\rangle\langle11| \right)
$$
利用[偏迹](@entry_id:146482)的性质 $\text{Tr}_B(|i\rangle_A|j\rangle_B\langle k|_A\langle l|_B) = |i\rangle_A\langle k|_A \delta_{jl}$，我们得到：
$$
\hat{\rho}_A = \frac{1}{5} \left( 4|0\rangle_A\langle0|_A + 1|1\rangle_A\langle1|_A \right) = \begin{pmatrix} 4/5   0 \\ 0   1/5 \end{pmatrix}
$$
尽管整个系统处于纯态，子系统A却处于一个[混合态](@entry_id:141568)，因为它不是一个[投影算符](@entry_id:154142)，其纯度为 $\text{Tr}(\hat{\rho}_A^2) = (4/5)^2 + (1/5)^2 = 17/25  1$。

这个现象在贝尔态（如[单重态](@entry_id:154728) $|\Psi\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle)$）中表现得最为极致 [@problem_id:1999464]。对于这个纯的[纠缠态](@entry_id:152310)，子系统A的[约化密度矩阵](@entry_id:146315)为：
$$
\hat{\rho}_A = \text{Tr}_B (|\Psi\rangle\langle\Psi|) = \frac{1}{2} (|\uparrow\rangle_A\langle\uparrow|_A + |\downarrow\rangle_A\langle\downarrow|_A) = \frac{1}{2}I_A
$$
这是一个**[最大混合态](@entry_id:137775)**，其纯度为 $1/2$。这意味着，如果我们只观察其中一个粒子，它的自旋是完全无极化的，向上和向下的概率完全相等。所有的信息都不在单个粒子中，而在于两个粒子之间完美的关联之中。

### [时间演化](@entry_id:153943)与[稳态](@entry_id:182458)：[冯·诺依曼方程](@entry_id:153472)

密度矩阵如何随[时间演化](@entry_id:153943)？对于一个由时间无关的[哈密顿量](@entry_id:172864) $\hat{H}$ 描述的[孤立系统](@entry_id:159201)，密度矩阵 $\hat{\rho}(t)$ 的演化由**[冯·诺依曼方程](@entry_id:153472) (von Neumann equation)** 给出：
$$
i\hbar \frac{d\hat{\rho}(t)}{dt} = [\hat{H}, \hat{\rho}(t)]
$$
其中 $[\hat{H}, \hat{\rho}] = \hat{H}\hat{\rho} - \hat{\rho}\hat{H}$ 是对易子。这个方程是量子力学中的薛定谔方程在[统计系综](@entry_id:149738)层面的推广，也是经典[统计力](@entry_id:194984)学中[刘维尔方程](@entry_id:156422)的量子对应。

一个特别重要的概念是**[稳态](@entry_id:182458) (stationary state)**，即不随[时间演化](@entry_id:153943)的状态。对于这样的状态，$\frac{d\hat{\rho}}{dt} = 0$。根据[冯·诺依曼方程](@entry_id:153472)，这等价于一个简单而深刻的条件 [@problem_id:2014357]：
$$
[\hat{H}, \hat{\rho}] = 0
$$
这个条件既是充分的也是必要的。它表明，一个[量子态](@entry_id:146142)是[稳态](@entry_id:182458)，当且仅当其[密度矩阵](@entry_id:139892)与系统的[哈密顿量](@entry_id:172864)对易。
从物理上看，这意味着[稳态](@entry_id:182458)的[密度矩阵](@entry_id:139892)和[哈密顿量](@entry_id:172864)拥有共同的本征矢。因此，任何在能量本征基下是对角的密度矩阵都描述了一个[稳态](@entry_id:182458)。更普遍地说，任何可以写成[哈密顿量](@entry_id:172864)函数的密度矩阵，即 $\hat{\rho} = f(\hat{H})$，都与 $\hat{H}$ 对易，因此都是[稳态](@entry_id:182458)。

这正是[统计力](@entry_id:194984)学中各种平衡系综（微正则、正则、巨正则）的关键特征。例如，在与温度为 $T$ 的[热库](@entry_id:143608)接触并[达到平衡](@entry_id:170346)的系统中，其状态由正则系综描述，[密度矩阵](@entry_id:139892)为：
$$
\hat{\rho}_{\text{can}} = \frac{1}{Z} \exp(-\beta \hat{H})
$$
其中 $\beta = 1/(k_B T)$，$Z = \text{Tr}(\exp(-\beta \hat{H}))$ 是[配分函数](@entry_id:193625)。由于这个[密度矩阵](@entry_id:139892)是 $\hat{H}$ 的函数，它自然满足 $[\hat{H}, \hat{\rho}_{\text{can}}] = 0$，因此它描述了一个热力学平衡下的[稳态](@entry_id:182458)。