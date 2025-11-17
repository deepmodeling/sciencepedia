## 引言
在量子世界中，一个孤立系统的状态通常由态矢量完美描述。然而，当我们面对由大量粒子组成的[统计系综](@entry_id:149738)，或者只关注一个与环境相互作用的复杂系统的一部[分时](@entry_id:274419)，态矢量的描述便显得力不从心。我们对系统的知识往往是不完整的，这种不确定性需要一个更强大的数学语言来刻画。[密度算符](@entry_id:138151)正是为解决这一根本问题而生，它为所有[量子态](@entry_id:146142)——无论是确定的纯态还是不确定的混合态——提供了一个统一而优雅的框架。

本文旨在系统性地介绍[密度算符](@entry_id:138151)的理论与应用。我们将从第一章“原理与机制”开始，详细阐述[密度算符](@entry_id:138151)的定义、必须满足的数学性质，以及如何利用它计算物理量的[期望值](@entry_id:153208)和区分[纯态](@entry_id:141688)与[混合态](@entry_id:141568)。随后，在第二章“应用与交叉学科联系”中，我们将展示[密度算符](@entry_id:138151)如何成为连接量子力学、[统计力](@entry_id:194984)学和量子信息等领域的桥梁，解释热平衡、量子噪声和纠缠等关键概念。最后，在“动手实践”部分，我们将通过一系列具体问题，巩固并应用所学知识。通过本次学习，读者将掌握使用[密度算符](@entry_id:138151)分析和理解复杂量子系统的核心技能。

## 原理与机制

在量子力学的基础框架中，一个孤立系统的状态由[希尔伯特空间](@entry_id:261193)中的一个态矢量 $|\psi\rangle$ 完美描述。然而，在[统计力](@entry_id:194984)学和更广泛的物理情境中，我们常常无法获得关于系统的完全信息。我们可能面对的是一个处于不同纯态的粒子组成的系综，或者我们只对一个与环境发生纠缠的更大系统的一部分感兴趣。在这些情况下，单一的态矢量已不足以刻画系统的物理状态。为了应对这一挑战，我们引入一个更强大、更普适的数学工具——**[密度算符](@entry_id:138151)**（或称密度矩阵），记作 $\rho$。本章将系统阐述[密度算符](@entry_id:138151)的核心原理、数学性质及其背后的深刻物理机制。

### [密度算符](@entry_id:138151)的构建

[密度算符](@entry_id:138151)为描述一般[量子态](@entry_id:146142)提供了统一的语言，无论是纯态还是[混合态](@entry_id:141568)。

对于一个确定处于[纯态](@entry_id:141688) $|\psi\rangle$ 的系统，其[密度算符](@entry_id:138151)定义为该态到自身的投影算符：
$$
\rho = |\psi\rangle\langle\psi|
$$
这看起来似乎只是对原有表述的重写，但它为推广到更复杂的情况奠定了基础。

当一个系统并非处于单一的[纯态](@entry_id:141688)，而是以一定的经典[概率分布](@entry_id:146404)在一系列[纯态](@entry_id:141688)上时，我们称之为**混合态** (mixed state)。例如，考虑一个系综，其中有比例为 $p_1$ 的粒子处于态 $|\psi_1\rangle$，比例为 $p_2$ 的粒子处于态 $|\psi_2\rangle$，以此类推，其中 $\sum_j p_j = 1$。描述这样一个系综的[密度算符](@entry_id:138151)是各个纯态[投影算符](@entry_id:154142)的加权平均：
$$
\rho = \sum_j p_j |\psi_j\rangle\langle\psi_j|
$$
这里的 $p_j$ 是描述我们知识不完备性的经典概率。它反映了系统在被制备时，有多大的可能性处于 $|\psi_j\rangle$ 这个特定的[量子态](@entry_id:146142)上。

为了具体理解这一构建过程，让我们考察一个由自旋-1/2粒子组成的系综。假设系综中一半的粒子处于z轴方向自旋向上态 $|+z\rangle$，另一半处于x轴方向自旋向上态 $|+x\rangle$ [@problem_id:1988209]。在 $S_z$ 表象下，我们有：
$$
|+z\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad |+x\rangle = \frac{1}{\sqrt{2}} (|+z\rangle + |-z\rangle) = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ 1 \end{pmatrix}
$$
根据[混合态](@entry_id:141568)的定义，该系综的[密度算符](@entry_id:138151)为：
$$
\rho = \frac{1}{2} |+z\rangle\langle+z| + \frac{1}{2} |+x\rangle\langle+x|
$$
将各个[投影算符](@entry_id:154142)的矩阵形式代入计算：
$$
|+z\rangle\langle+z| = \begin{pmatrix} 1 \\ 0 \end{pmatrix} \begin{pmatrix} 1  0 \end{pmatrix} = \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix}
$$
$$
|+x\rangle\langle+x| = \left(\frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix}\right) \left(\frac{1}{\sqrt{2}}\begin{pmatrix} 1  1 \end{pmatrix}\right) = \frac{1}{2}\begin{pmatrix} 1  1 \\ 1  1 \end{pmatrix}
$$
于是，[密度矩阵](@entry_id:139892)为：
$$
\rho = \frac{1}{2} \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix} + \frac{1}{2} \left( \frac{1}{2}\begin{pmatrix} 1  1 \\ 1  1 \end{pmatrix} \right) = \begin{pmatrix} \frac{1}{2}  0 \\ 0  0 \end{pmatrix} + \begin{pmatrix} \frac{1}{4}  \frac{1}{4} \\ \frac{1}{4}  \frac{1}{4} \end{pmatrix} = \begin{pmatrix} \frac{3}{4}  \frac{1}{4} \\ \frac{1}{4}  \frac{1}{4} \end{pmatrix}
$$
这个 $2 \times 2$ 的矩阵 $\rho$ 包含了描述该混合态系综所需的全部信息。

### [密度算符](@entry_id:138151)的基本数学性质

任何一个合法的、代表物理状态的[密度算符](@entry_id:138151) $\rho$ 都必须满足三个基本性质：[厄米性](@entry_id:141899)、归一化和[半正定性](@entry_id:147720)。

#### [厄米性](@entry_id:141899) (Hermiticity)
[密度算符](@entry_id:138151)必须是[厄米算符](@entry_id:153410)，即它等于其自身的[厄米共轭](@entry_id:191215)：
$$
\rho = \rho^\dagger
$$
这个性质保证了[物理可观测量](@entry_id:154692)（由[厄米算符](@entry_id:153410)表示）的[期望值](@entry_id:153208)是实数。从定义 $\rho = \sum_j p_j |\psi_j\rangle\langle\psi_j|$ 出发，由于概率 $p_j$ 是实数，且 $(|\psi_j\rangle\langle\psi_j|)^\dagger = |\psi_j\rangle\langle\psi_j|$，所以 $\rho$ 的[厄米性](@entry_id:141899)是自洽的。在矩阵表示中，这意味着 $\rho_{mn} = \rho_{nm}^*$。

#### 归一化 (Normalization)
[密度算符](@entry_id:138151)的迹（trace）必须为1：
$$
\text{Tr}(\rho) = 1
$$
迹是在任何完备正交基下对角元素之和，它与基的选择无关。这个条件是量子版的概率归一化，即在所有可能的状态中找到系统的总概率为1。利用[迹的线性](@entry_id:199170)性质和 $|\psi_j\rangle$ 的归一性 ($\langle\psi_j|\psi_j\rangle=1$)，我们可以验证：
$$
\text{Tr}(\rho) = \text{Tr}\left(\sum_j p_j |\psi_j\rangle\langle\psi_j|\right) = \sum_j p_j \text{Tr}(|\psi_j\rangle\langle\psi_j|) = \sum_j p_j \langle\psi_j|\psi_j\rangle = \sum_j p_j = 1
$$
在实际问题中，[归一化条件](@entry_id:156486)常被用来确定密度矩阵中的未知常数。例如，若一个[密度算符](@entry_id:138151)被给出为 $\rho = N M$，其中 $M$ 是一个给定的厄米矩阵而 $N$ 是一个待定常数，则通过施加迹为1的条件即可求解 $N$ [@problem_id:1988229]。对于矩阵 $M = \begin{pmatrix} 5  2i  1-i \\ -2i  3  1 \\ 1+i  1  4 \end{pmatrix}$，其迹为 $\text{Tr}(M) = 5+3+4=12$。因此，为了满足 $\text{Tr}(\rho) = N \cdot \text{Tr}(M) = 1$，必须有 $N = \frac{1}{12}$。

#### [半正定性](@entry_id:147720) (Positive Semidefiniteness)
对于任意一个归一化的态矢量 $|\phi\rangle$，用[密度算符](@entry_id:138151) $\rho$ 计算出的在该态的概率必须是非负的：
$$
P(|\phi\rangle) = \langle\phi|\rho|\phi\rangle \ge 0
$$
这个性质被称为[半正定性](@entry_id:147720)。对于一个[厄米算符](@entry_id:153410)，它等价于其所有[本征值](@entry_id:154894) $\lambda_i$ 均为非负数，即 $\lambda_i \ge 0$。这是因为 $\langle\phi|\rho|\phi\rangle$ 的最小值（根据[瑞利-里兹变分原理](@entry_id:185834)）等于 $\rho$ 的最小[本征值](@entry_id:154894)。如果最小[本征值](@entry_id:154894)为负，那么就存在一个态 $|\phi\rangle$ 使得找到系统的概率为负，这在物理上是荒谬的。

因此，一个给定的厄米、迹为1的矩阵，如果它拥有任何负的[本征值](@entry_id:154894)，就不能成为一个合法的密度矩阵 [@problem_id:1988237]。考虑一个矩阵 $\rho = \begin{pmatrix} 0.5  1 \\ 1  0.5 \end{pmatrix}$。它显然是厄米的，且迹为 $0.5+0.5=1$。然而，它的[特征方程](@entry_id:265849)为 $(0.5-\lambda)^2 - 1 = 0$，解得[本征值](@entry_id:154894)为 $\lambda_1 = 1.5$ 和 $\lambda_2 = -0.5$。由于存在一个负[本征值](@entry_id:154894)，这个矩阵不是一个合法的[密度算符](@entry_id:138151)。它预测在对应于 $\lambda_2$ 的本征态 $|\psi_2\rangle = \frac{1}{\sqrt{2}}(|0\rangle-|1\rangle)$ 上找到系统的“概率”为 -0.5，这违背了概率的基本公理。

### 使用[密度算符](@entry_id:138151)：计算与表征

[密度算符](@entry_id:138151)不仅是一个理论构造，更是一个强大的计算工具。

#### 计算物理量的[期望值](@entry_id:153208)
对于由[厄米算符](@entry_id:153410) $A$ 代表的[物理可观测量](@entry_id:154692)，其在由[密度算符](@entry_id:138151) $\rho$ 描述的系综中的[期望值](@entry_id:153208)（或平均测量值）由以下公式给出：
$$
\langle A \rangle = \text{Tr}(\rho A)
$$
这个公式是纯态[期望值](@entry_id:153208)公式 $\langle A \rangle = \langle\psi|A|\psi\rangle$ 的直接推广。对于[纯态](@entry_id:141688) $\rho=|\psi\rangle\langle\psi|$，$\text{Tr}(|\psi\rangle\langle\psi| A) = \langle\psi|A|\psi\rangle$。对于[混合态](@entry_id:141568)，它正确地计算了系综的统计平均值：
$$
\langle A \rangle = \text{Tr}\left(\sum_j p_j |\psi_j\rangle\langle\psi_j| A\right) = \sum_j p_j \text{Tr}(|\psi_j\rangle\langle\psi_j| A) = \sum_j p_j \langle\psi_j|A|\psi_j\rangle
$$
这正是对每个子系综的量子[期望值](@entry_id:153208)进行经典概率加权平均的结果。

例如，在一个系综中，有 $\frac{3}{4}$ 的粒子处于态 $|\psi_1\rangle = |\uparrow_z\rangle$，$\frac{1}{4}$ 的粒子处于态 $|\psi_2\rangle = \frac{1}{\sqrt{2}}(|\uparrow_z\rangle + |\downarrow_z\rangle)$。我们要计算自旋z分量的平均值，其算符为 $\hat{\sigma}_z = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$ [@problem_id:1988277]。首先构建[密度矩阵](@entry_id:139892)：
$$
\rho = \frac{3}{4} \begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix} + \frac{1}{4} \left( \frac{1}{2} \begin{pmatrix} 1  1 \\ 1  1 \end{pmatrix} \right) = \begin{pmatrix} \frac{7}{8}  \frac{1}{8} \\ \frac{1}{8}  \frac{1}{8} \end{pmatrix}
$$
然后计算[期望值](@entry_id:153208)：
$$
\langle \hat{\sigma}_z \rangle = \text{Tr}(\rho \hat{\sigma}_z) = \text{Tr}\left( \begin{pmatrix} \frac{7}{8}  \frac{1}{8} \\ \frac{1}{8}  \frac{1}{8} \end{pmatrix} \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix} \right) = \text{Tr}\begin{pmatrix} \frac{7}{8}  -\frac{1}{8} \\ \frac{1}{8}  -\frac{1}{8} \end{pmatrix} = \frac{7}{8} - \frac{1}{8} = \frac{6}{8} = \frac{3}{4}
$$
这个结果清晰地展示了[密度算符](@entry_id:138151)在处理混合系综时的威力。

#### 纯度：量化态的混合程度
我们如何判断一个由 $\rho$ 描述的态是[纯态](@entry_id:141688)还是[混合态](@entry_id:141568)？一个简单而有效的度量是**纯度** (purity)，定义为 $\gamma = \text{Tr}(\rho^2)$。

-   如果系统处于**[纯态](@entry_id:141688)**，$\rho = |\psi\rangle\langle\psi|$，那么 $\rho^2 = (|\psi\rangle\langle\psi|)(|\psi\rangle\langle\psi|) = |\psi\rangle\langle\psi| = \rho$。因此，$\gamma = \text{Tr}(\rho^2) = \text{Tr}(\rho) = 1$。
-   如果系统处于**混合态**，可以证明 $\gamma = \text{Tr}(\rho^2)  1$。在其本征基下，$\rho = \sum_i \lambda_i |i\rangle\langle i|$，其中 $\sum_i \lambda_i = 1$ 且 $0 \le \lambda_i \le 1$。那么 $\rho^2 = \sum_i \lambda_i^2 |i\rangle\langle i|$，其迹为 $\gamma = \sum_i \lambda_i^2$。由于 $\lambda_i^2 \le \lambda_i$，所以 $\sum_i \lambda_i^2 \le \sum_i \lambda_i = 1$。等号仅在某个 $\lambda_i=1$ 而其余都为0时成立，这恰恰是[纯态](@entry_id:141688)的条件。

对于一个 $d$ 维系统，纯度的最小值为 $\frac{1}{d}$，对应于**[最大混合态](@entry_id:137775)** (maximally mixed state)，即 $\rho = \frac{1}{d} I$，其中 $I$ 是[单位矩阵](@entry_id:156724)。

考察之前的一个例子，$\rho = \begin{pmatrix} 7/8  1/8 \\ 1/8  1/8 \end{pmatrix}$ [@problem_id:1988267]。我们可以计算它的纯度来判断其混合程度：
$$
\rho^2 = \begin{pmatrix} \frac{7}{8}  \frac{1}{8} \\ \frac{1}{8}  \frac{1}{8} \end{pmatrix} \begin{pmatrix} \frac{7}{8}  \frac{1}{8} \\ \frac{1}{8}  \frac{1}{8} \end{pmatrix} = \begin{pmatrix} (\frac{7}{8})^2+(\frac{1}{8})^2  (\frac{7}{8})(\frac{1}{8})+(\frac{1}{8})(\frac{1}{8}) \\ (\frac{1}{8})(\frac{7}{8})+(\frac{1}{8})(\frac{1}{8})  (\frac{1}{8})^2+(\frac{1}{8})^2 \end{pmatrix} = \begin{pmatrix} \frac{50}{64}  \frac{8}{64} \\ \frac{8}{64}  \frac{2}{64} \end{pmatrix}
$$
纯度为 $\gamma = \text{Tr}(\rho^2) = \frac{50}{64} + \frac{2}{64} = \frac{52}{64} = \frac{13}{16}$。因为 $\gamma  1$，所以该态是一个混合态。

### 复合系统与[约化密度算符](@entry_id:190449)

[密度算符](@entry_id:138151)的一个极为重要的应用是描述一个更大量子系统的一部分。考虑一个由子系统 A 和 B 组成的复合系统 AB。即使整个系统 AB 处于一个纯态 $|\Psi\rangle_{AB}$，如果我们只对子系统 A 进行测量，我们通常不能用一个纯态来描述 A。

要获得子系统 A 的状态描述，我们需要通过对子系统 B 的自由度求**[偏迹](@entry_id:146482)** (partial trace) 来得到 A 的**[约化密度算符](@entry_id:190449)** (reduced density operator) $\rho_A$：
$$
\rho_A = \text{Tr}_B(\rho_{AB})
$$
其中 $\rho_{AB} = |\Psi\rangle_{AB}\langle\Psi|_{AB}$ 是整个系统的[密度算符](@entry_id:138151)。

这一过程揭示了[量子纠缠](@entry_id:136576)的一个深刻后果：**纠缠导致局域混合性**。当子系统 A 和 B 纠缠时，即使整个系统是[纯态](@entry_id:141688)，描述单个子系统的[约化密度算符](@entry_id:190449)通常是混合态。

一个经典的例子是处于[贝尔态](@entry_id:140749)的两个纠缠的[量子比特](@entry_id:137928) [@problem_id:1988251]。设系统处于态 $|\Psi\rangle = \frac{1}{\sqrt{2}}(|00\rangle + |11\rangle)$，其中 $|ij\rangle \equiv |i\rangle_A \otimes |j\rangle_B$。整个系统的[密度算符](@entry_id:138151)是：
$$
\rho_{AB} = \frac{1}{2}(|00\rangle + |11\rangle)(\langle 00| + \langle 11|) = \frac{1}{2}(|00\rangle\langle 00| + |00\rangle\langle 11| + |11\rangle\langle 00| + |11\rangle\langle 11|)
$$
对子系统 B 求[偏迹](@entry_id:146482)，我们需要计算 $\text{Tr}_B(\rho_{AB}) = \sum_k \langle k|_B \rho_{AB} |k\rangle_B$。由于[交叉](@entry_id:147634)项如 $|00\rangle\langle 11|$ 的[偏迹](@entry_id:146482)为零（因为它们包含 $\langle 0|1\rangle_B=0$ 这样的[内积](@entry_id:158127)），只有对角项有贡献：
$$
\rho_A = \frac{1}{2} \text{Tr}_B(|00\rangle\langle 00|) + \frac{1}{2} \text{Tr}_B(|11\rangle\langle 11|)
$$
$$
= \frac{1}{2} \left( |0\rangle_A\langle 0|_A \langle 0|0\rangle_B + |1\rangle_A\langle 1|_A \langle 1|1\rangle_B \right) = \frac{1}{2} (|0\rangle_A\langle 0|_A + |1\rangle_A\langle 1|_A)
$$
在 A 的基 $\{|0\rangle_A, |1\rangle_A\}$ 中，$\rho_A$ 的[矩阵表示](@entry_id:146025)为：
$$
\rho_A = \frac{1}{2} \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} = \frac{1}{2}I
$$
这是一个[最大混合态](@entry_id:137775)！这意味着，尽管我们对整个 AB 系统的状态有完全的了解（它是一个[纯态](@entry_id:141688)），但对于只关心子系统 A 的观察者来说，A 的状态是完全随机的。任何对 A 的测量，无论在哪个基下，得到向上和向下结果的概率都是 50%。这就是量子纠缠的奇特之处，信息并非局域地存在于子系统中，而是存在于系统之间的关联中。

### 动力学与物理解释

[密度算符](@entry_id:138151)不仅能描述静态的系综，还能描述其随时间的演化。

#### 刘维-冯诺依曼方程与定态
对于一个由时间无关的[哈密顿量](@entry_id:172864) $H$ 描述的孤立系统，[密度算符](@entry_id:138151) $\rho(t)$ 的[时间演化](@entry_id:153943)遵循**刘维-冯诺依曼方程** (Liouville-von Neumann equation)：
$$
i\hbar \frac{d\rho}{dt} = [H, \rho]
$$
这个方程是薛定谔方程在[密度算符](@entry_id:138151)语言下的形式。其形式解为 $\rho(t) = U(t)\rho(0)U^\dagger(t)$，其中 $U(t) = \exp(-iHt/\hbar)$ 是[时间演化算符](@entry_id:196774)。

一个极其重要的情况是当初始[密度算符](@entry_id:138151)与[哈密顿量](@entry_id:172864)对易时，即 $[\rho(0), H] = 0$。在这种情况下：
$$
\frac{d\rho}{dt} = \frac{1}{i\hbar}[H, \rho(0)] = 0
$$
这意味着[密度算符](@entry_id:138151)不随时间演化，$\rho(t) = \rho(0)$。这样的状态被称为**定态** (stationary state)。对于一个处于定态的系统，任何物理量 $A$ 的[期望值](@entry_id:153208)都将是恒定的 [@problem_id:1988274]：
$$
\langle A \rangle(t) = \text{Tr}(\rho(t)A) = \text{Tr}(\rho(0)A) = \langle A \rangle(0) = \text{常数}
$$
注意，这个结论与 $A$ 是否与 $H$ 对易无关。[统计力](@entry_id:194984)学中的平衡态系综，如微正则系综、[正则系综](@entry_id:142391)和[巨正则系综](@entry_id:141562)，其[密度算符](@entry_id:138151)都是[哈密顿量](@entry_id:172864) $H$ 的函数，因此都与 $H$ 对易，描述的正是平衡定态。

#### 相干性：非对角元的物理意义
[密度矩阵](@entry_id:139892)的元素不仅包含概率信息，还编码了量子相干性。为了看清这一点，我们在系统的能量本征基 $\{|E_n\rangle\}$ 中展开[密度矩阵](@entry_id:139892)，其矩阵元为 $\rho_{mn} = \langle E_m|\rho|E_n\rangle$。

-   **对角元 $\rho_{nn}$**：代表了系统处于[能量本征态](@entry_id:152154) $|E_n\rangle$ 的**布居数** (population) 或经典概率。由于 $\text{Tr}(\rho)=1$，我们有 $\sum_n \rho_{nn} = 1$。如果[密度矩阵](@entry_id:139892)是对角的，即 $\rho_{mn}=0$ 当 $m \neq n$ 时，那么系统就是一个[能量本征态](@entry_id:152154)的经典统计混合，没有任何量子干涉效应。

-   **非对角元 $\rho_{mn}$ ($m \neq n$)**：被称为**相干项** (coherences)。它们的存在意味着系统不仅仅是能量本征态的经典混合，而是处于这些态的**量子[相干叠加](@entry_id:170209)**之中。非对角元的大小和[相位编码](@entry_id:753388)了不同[能量本征态](@entry_id:152154)之间的确定性相位关系。

非对角元的存在与否直接决定了系统的动力学行为 [@problem_id:1988268]。在刘维-冯诺依曼方程下，[矩阵元](@entry_id:186505)随时间演化为：
$$
\rho_{mn}(t) = \langle E_m|U(t)\rho(0)U^\dagger(t)|E_n\rangle = \rho_{mn}(0) \exp\left(-\frac{i}{\hbar}(E_m-E_n)t\right)
$$
可见，对角元 $\rho_{nn}(t) = \rho_{nn}(0)$ 是不随时间变化的，而**非对角元则以对应能量差的频率进行[振荡](@entry_id:267781)**。

这种[振荡](@entry_id:267781)会传递到物理量的[期望值](@entry_id:153208)上。一个[可观测量](@entry_id:267133) $A$ 的[期望值](@entry_id:153208)为：
$$
\langle A \rangle(t) = \text{Tr}(\rho(t)A) = \sum_{m,n} \rho_{nm}(t)A_{mn} = \sum_{m,n} \rho_{nm}(0) A_{mn} \exp\left(-\frac{i}{\hbar}(E_n-E_m)t\right)
$$
如果一个可观测量 $A$ 与[哈密顿量](@entry_id:172864) $H$ 对易（$[A,H]=0$），那么它在能量基下是对角的（$A_{mn} \propto \delta_{mn}$），其[期望值](@entry_id:153208)将不随时间变化。然而，如果 $A$ 与 $H$ 不对易，它在能量基下将有非对角元。此时，如果系统本身也存在相干性（$\rho_{nm}(0) \neq 0$），那么 $\langle A \rangle(t)$ 将会随时间演化，通常表现为[振荡](@entry_id:267781)行为。因此，**非对角相干项是那些与[哈密顿量](@entry_id:172864)不对易的[可观测量](@entry_id:267133)产生[时间演化](@entry_id:153943)的根源**。

### 态的描述 vs. 态的制备

最后，我们必须强调一个[密度算符](@entry_id:138151)理论中至关重要的概念：[密度算符](@entry_id:138151) $\rho$ 描述的是一个[量子态](@entry_id:146142)本身所包含的、所有可通过实验测量获取的信息，但它并不唯一对应于一种特定的制备历史。换言之，**多种不同的物理制备过程可以产生完全相同的[密度算符](@entry_id:138151)**。一旦两个系综被证明具有相同的[密度算符](@entry_id:138151)，那么通过任何[量子测量](@entry_id:272490)都无法将它们区分开来。

这个“多对一”的映射关系是[量子统计力学](@entry_id:140244)的一个核心特征。让我们来看一个惊人的例子 [@problem_id:1988253]。考虑两个不同的自旋-1/2粒子系综：
- **系综 A**：50% 的粒子处于 $|{\uparrow_z}\rangle$ 态，50% 处于 $|{\downarrow_z}\rangle$ 态。
- **系综 B**：50% 的粒子处于 $|{\uparrow_x}\rangle$ 态，50% 处于 $|{\downarrow_x}\rangle$ 态。

直觉上，这两个系综似乎完全不同。然而，它们的[密度算符](@entry_id:138151)却是相同的。
对于系综 A：
$$
\rho_A = \frac{1}{2}|\uparrow_z\rangle\langle\uparrow_z| + \frac{1}{2}|\downarrow_z\rangle\langle\downarrow_z| = \frac{1}{2}\begin{pmatrix} 1  0 \\ 0  0 \end{pmatrix} + \frac{1}{2}\begin{pmatrix} 0  0 \\ 0  1 \end{pmatrix} = \frac{1}{2}\begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} = \frac{1}{2}I
$$
对于系综 B，利用 $|{\uparrow_x}\rangle\langle{\uparrow_x}| + |{\downarrow_x}\rangle\langle{\downarrow_x}| = I$（因为它们构成一个[完备基](@entry_id:143908)），我们得到：
$$
\rho_B = \frac{1}{2}|\uparrow_x\rangle\langle\uparrow_x| + \frac{1}{2}|\downarrow_x\rangle\langle\downarrow_x| = \frac{1}{2} (|\uparrow_x\rangle\langle\uparrow_x| + |\downarrow_x\rangle\langle\downarrow_x|) = \frac{1}{2}I
$$
两个系综的[密度算符](@entry_id:138151)完全相同，都是[最大混合态](@entry_id:137775)。这意味着，尽管它们的制备过程（一个在z基上混合，一个在x基上混合）截然不同，但最终的统计状态在物理上是不可区分的。测量任何方向的自旋分量，其[期望值](@entry_id:153208)都为零。

更令人惊讶的是，这还不是得到[最大混合态](@entry_id:137775)的全部方式。我们之前已经看到两种完全不同的物理情景也导向了同样的结果：
1.  对一个处于特定纯态的粒子进行一次投影测量（例如测量 $S_x$），但不对测量结果进行记录或筛选，最终留下的系综状态也是[最大混合态](@entry_id:137775) [@problem_id:1988212]。
2.  一个处于纠缠[贝尔态](@entry_id:140749) $|\Psi^+\rangle$ 的双粒子系统，如果我们只观察其中一个粒子，它的[约化密度算符](@entry_id:190449)也是[最大混合态](@entry_id:137775) [@problem_id:1988251]。

综上所述，一个经典概率混合物、一个测量导致的[退相干](@entry_id:145157)态、一个纠缠系统的子系统，这三种来源迥异的物理过程，都可以产生同一个数学对象——[最大混合态](@entry_id:137775)[密度算符](@entry_id:138151)。这深刻地揭示了[密度算符](@entry_id:138151)作为一种“知识状态”的本质：它封装了我们对一个系统通过测量所能知道的一切，而抹去了那些无法通过操作区分的、关于其“真实”来源的细节。