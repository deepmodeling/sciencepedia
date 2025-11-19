## 引言
在量子世界中，我们关注的系统很少是孤立的单个粒子。从构成原子的电子与[原子核](@entry_id:167902)，到组成物质的基本粒子夸克，再到[量子计算](@entry_id:142712)机中的多个[量子比特](@entry_id:137928)，我们必须处理由多个部分构成的复合系统。描述这些系统的核心挑战之一在于如何有效地处理各个组分的角动量（包括[轨道角动量](@entry_id:191303)和自旋角动量）以及它们之间的相互作用。为解决这一问题，量子力学提供了两种强大而互补的描述框架：非[耦合表象](@entry_id:136812)和[耦合表象](@entry_id:136812)。

本文旨在系统性地阐明这两种表象的物理思想和数学结构，并展示它们在解决实际物理问题中的威力。读者将通过本文的学习，掌握从一种表象转换到另一种表象的关键技术，并理解为何恰当地选择表象是简化问题、揭示物理本质的核心步骤。

在“**原理和机制**”一章中，我们将深入探讨非耦合与[耦合表象](@entry_id:136812)的定义，阐明它们各自对应的力学量完[全集](@entry_id:264200)，并通过[角动量相加](@entry_id:145967)法则和克莱布希-高登(Clebsch-Gordan)系数建立起两者之间的精确联系。接着，在“**应用与交叉学科联系**”一章，我们将展示这一理论框架如何应用于原子物理中的精细结构、粒子物理中的[强子谱学](@entry_id:155019)，以及[量子信息科学](@entry_id:150091)中的[逻辑门设计](@entry_id:165034)等前沿领域，揭示其广泛的适用性。最后，在“**动手实践**”部分，读者将有机会通过解决具体问题，将理论知识转化为解决实际物理场景的实践能力。

## 原理和机制

在量子力学中，当我们从描述单个粒子转向描述由多个组分构成的复合系统时，我们必须扩展我们的数学框架。例如，一个原子中的多个电子，或者一个氢原子中的质子和电子，都构成了[复合量子系统](@entry_id:193313)。描述这些系统的关键在于如何处理各个组分的角动量。本章将详细阐述描述复合系统角动量的两种基本绘景：非耦合绘景和耦合绘景，并探讨它们之间的关系以及各自在物理应用中的重要性。

### 复合系统与表象选择

考虑一个由两个子系统组成的量子系统，每个子系统都具有明确定义的角动量。例如，这可以是两个粒子的轨道角动量，也可以是它们的自旋角动量，或者是[轨道](@entry_id:137151)与自旋的组合。令第一个子系统的[角动量算符](@entry_id:153013)为 $\mathbf{J}_1$，第二个子系统的[角动量算符](@entry_id:153013)为 $\mathbf{J}_2$。描述整个系统的希尔伯特空间是两个子系统希尔伯特空间的张量积，即 $\mathcal{H} = \mathcal{H}_1 \otimes \mathcal{H}_2$。

为了描述这个复合系统中的状态，我们需要为这个[张量积](@entry_id:140694)空间选择一组完备的[基矢](@entry_id:199546)。在处理角动量问题时，有两种特别重要且物理意义清晰的[基矢](@entry_id:199546)选择，它们被称为 **非[耦合表象](@entry_id:136812)（uncoupled basis）** 和 **[耦合表象](@entry_id:136812)（coupled basis）**。选择哪种表象取决于我们所研究的物理问题，特别是系统中[哈密顿量](@entry_id:172864)的对称性。

### 非[耦合表象](@entry_id:136812)：独立子系统的描述

最直观的描述方式是分别指定每个子系统的状态。非[耦合表象](@entry_id:136812)正是基于这种思想。假设子系统1的状态由量子数 $j_1$ 和 $m_1$ 描述，其本征态为 $|j_1, m_1\rangle$，满足 $J_1^2 |j_1, m_1\rangle = j_1(j_1+1)\hbar^2 |j_1, m_1\rangle$ 和 $J_{1z} |j_1, m_1\rangle = m_1\hbar |j_1, m_1\rangle$。同样，子系统2的状态为 $|j_2, m_2\rangle$。

非[耦合表象](@entry_id:136812)的[基矢](@entry_id:199546)是这两个独立本征态的简单[张量积](@entry_id:140694)（或[直积](@entry_id:143046)）：
$$ |j_1, m_1; j_2, m_2\rangle \equiv |j_1, m_1\rangle \otimes |j_2, m_2\rangle $$

这组[基矢](@entry_id:199546)是四个相互[对易算符](@entry_id:149529) $J_1^2, J_{1z}, J_2^2, J_{2z}$ 的共同本征矢。这四个算符构成了一组 **力学量完全集（Complete Set of Commuting Observables, CSCO）**。因此，在这个表象中，每个子系统的角动量大小和其在z轴上的投影都是确定的。

该表象非常适用于描述两个子系统之间没有相互作用，或者相互作用非常弱以至于可以忽略的情况。在这种情况下，我们可以独立地测量或讨论每个子系统的角动量状态。

非[耦合表象](@entry_id:136812)中状态的总数是每个子系统状态数的乘积。对于给定的 $j_1$ 和 $j_2$，[磁量子数](@entry_id:145584) $m_1$ 可以取 $2j_1+1$ 个值，$m_2$ 可以取 $2j_2+1$ 个值。因此，非[耦合表象](@entry_id:136812)的总维度（即状态总数）为：
$$ N_{unc} = (2j_1+1)(2j_2+1) $$

例如，考虑一个由核自旋为 $s_N=1$ 的[氘核](@entry_id:161402)和一个自旋为 $s_e=1/2$ 的电子组成的氘[原子模型](@entry_id:137207) [@problem_id:1351486]。在非[耦合表象](@entry_id:136812)中，总的自旋状态数是 $N_{unc} = (2s_N+1)(2s_e+1) = (2 \cdot 1 + 1)(2 \cdot 1/2 + 1) = 3 \times 2 = 6$。这六个状态分别是 $|1, 1; 1/2, 1/2\rangle, |1, 1; 1/2, -1/2\rangle, |1, 0; 1/2, 1/2\rangle, \dots, |1, -1; 1/2, -1/2\rangle$。

### [耦合表象](@entry_id:136812)：将系统视为一个整体

在许[多物理场](@entry_id:164478)景中，子系统之间存在不可忽略的相互作用。例如，原子中的[自旋-轨道耦合](@entry_id:143520)或氢原子中的[超精细相互作用](@entry_id:137748)。这些相互作用通常依赖于子系统角动量的相对取向，而不仅仅是它们各自的独立状态。在这种情况下，单个子系统的角动量通常不再是[守恒量](@entry_id:150267)，因为它们会通过相互作用交换角动量。然而，如果系统是孤立的，其 **[总角动量](@entry_id:155748)** $\mathbf{J} = \mathbf{J}_1 + \mathbf{J}_2$ 仍然是守恒的。

这就引出了[耦合表象](@entry_id:136812)。在[耦合表象](@entry_id:136812)中，我们寻找的是[总角动量算符](@entry_id:149439) $J^2 = (\mathbf{J}_1 + \mathbf{J}_2)^2$ 和其z分量 $J_z = J_{1z} + J_{2z}$ 的共同本征态。这些状态记为 $|J, M\rangle$，其中 $J$ 是[总角动量量子数](@entry_id:164948)，$M$ 是总磁量子数。

这组耦合[基矢](@entry_id:199546)是另一组力学量完全集 $J^2, J_z, J_1^2, J_2^2$ 的共同本征矢。请注意，算符 $J_{1z}$ 和 $J_{2z}$ 通常与 $J^2$ 不对易，因此在[耦合表象](@entry_id:136812)中，单个子系统的z分量角动量通常是不确定的。

对于给定的 $j_1$ 和 $j_2$，[总角动量量子数](@entry_id:164948) $J$ 的可能取值由[角动量加法](@entry_id:138983)法则给出。$J$ 的取值范围是从 $|j_1 - j_2|$ 到 $j_1 + j_2$，每次增加一个整数：
$$ J \in \{ |j_1 - j_2|, |j_1 - j_2| + 1, \dots, j_1 + j_2 \} $$

对于每一个给定的 $J$ 值，总[磁量子数](@entry_id:145584) $M$ 像往常一样，可以取 $2J+1$ 个值，从 $-J$ 到 $+J$。

一个至关重要的原则是 **状态数守恒**：从一个表象变换到另一个表象，希尔伯特空间的维度必须保持不变。这意味着[耦合表象](@entry_id:136812)中所有可能状态的总数必须等于非[耦合表象](@entry_id:136812)中的状态总数。
$$ \sum_{J=|j_1-j_2|}^{j_1+j_2} (2J+1) = (2j_1+1)(2j_2+1) $$

让我们通过两个例子来验证这一点。
1.  考虑一个原子，其中一个电子处于p轨道 ($l_1=1$)，另一个电子处于d轨道 ($l_2=2$) [@problem_id:2087704]。根据[角动量加法](@entry_id:138983)法则，总[轨道角动量量子数](@entry_id:167573) $L$ 的可能取值为：
    $$ L \in \{ |1-2|, |1-2|+1, \dots, 1+2 \} = \{ 1, 2, 3 \} $$
    在非[耦合表象](@entry_id:136812)中，状态总数为 $(2l_1+1)(2l_2+1) = (3)(5) = 15$。在[耦合表象](@entry_id:136812)中，状态总数为 $\sum_L (2L+1) = (2\cdot1+1) + (2\cdot2+1) + (2\cdot3+1) = 3 + 5 + 7 = 15$。两者完全一致。

2.  回到[氘](@entry_id:194706)原子的例子，其中 $s_N=1, s_e=1/2$ [@problem_id:1351486]。总自旋量子数 $F$ 的可能取值为：
    $$ F \in \{ |1-1/2|, 1+1/2 \} = \{ 1/2, 3/2 \} $$
    [耦合表象](@entry_id:136812)中的状态总数为 $(2 \cdot 1/2 + 1) + (2 \cdot 3/2 + 1) = 2 + 4 = 6$。这与我们在非[耦合表象](@entry_id:136812)中计算得到的6个状态完全匹配。

### 关联两个表象：[Clebsch-Gordan系数](@entry_id:142551)

既然非[耦合表象](@entry_id:136812)和[耦合表象](@entry_id:136812)都是同一个[希尔伯特空间](@entry_id:261193)中的完备正交基，它们之间必然可以通过一个幺正变换联系起来。这个变换将一个耦合态 $|J, M\rangle$ 展开为非耦合态 $|j_1, m_1; j_2, m_2\rangle$ 的[线性组合](@entry_id:154743)：

$$ |J, M\rangle = \sum_{m_1, m_2} \langle j_1, m_1; j_2, m_2 | J, M \rangle |j_1, m_1; j_2, m_2\rangle $$

这里的展开系数 $\langle j_1, m_1; j_2, m_2 | J, M \rangle$ 被称为 **[Clebsch-Gordan系数](@entry_id:142551) (CG系数)**。这些系数是实数（通过[相角](@entry_id:274491)约定），并且只有在 $M = m_1 + m_2$ 时才不为零。这个条件反映了[总角动量](@entry_id:155748)z分量是各个分量之和的事实。

CG系数的具体数值可以通过使用[升降算符](@entry_id:197899)或递归关系来计算，并且在许多参考书中都有表格可查。让我们以最重要和最常见的例子——两个自旋1/2粒子的耦合——来手动构建这些系数。

考虑两个自旋1/2粒子（例如，两个电子），$j_1=s_1=1/2, j_2=s_2=1/2$。[总自旋](@entry_id:153335) $S$ 的可能取值为 $|1/2-1/2|, \dots, 1/2+1/2$，即 $S=0$（**自旋单态**）和 $S=1$（**自旋三重态**）。[非耦合基](@entry_id:156676)矢为 $\{|\uparrow\uparrow\rangle, |\uparrow\downarrow\rangle, |\downarrow\uparrow\rangle, |\downarrow\downarrow\rangle\}$，其中 $|\uparrow\rangle$ 代表 $m_s=+1/2$, $|\downarrow\rangle$ 代表 $m_s=-1/2$。

1.  **[最高权](@entry_id:202808)重态（Stretched State）**：我们从总自旋和其投影都取最大值的状态开始，即三重态中的 $|S=1, M=1\rangle$。要得到 $M=1$，唯一的可能是 $m_1=1/2$ 和 $m_2=1/2$。因此，这个耦合态直接对应于一个非耦合态 [@problem_id:2087695]：
    $$ |1, 1\rangle = |\uparrow\uparrow\rangle $$
    这说明了“拉伸”态（$J=j_1+j_2, M=J$）总是一个简单的乘积态，其CG系数为1。

2.  **应用下降算符**：我们可以通过对 $|1, 1\rangle$ 应用总自旋下降算符 $S_{-} = S_{1-} + S_{2-}$ 来生成三重态中的其他成员。作用在耦合态上：
    $$ S_-|S, M\rangle = \hbar\sqrt{S(S+1) - M(M-1)} |S, M-1\rangle $$
    $$ S_-|1, 1\rangle = \hbar\sqrt{1(2) - 1(0)} |1, 0\rangle = \hbar\sqrt{2} |1, 0\rangle $$
    现在，将 $S_-$ 作用在非耦合态 $|\uparrow\uparrow\rangle$ 上：
    $$ (S_{1-} + S_{2-})|\uparrow\uparrow\rangle = S_{1-}|\uparrow\uparrow\rangle + S_{2-}|\uparrow\uparrow\rangle = \hbar|\downarrow\uparrow\rangle + \hbar|\uparrow\downarrow\rangle $$
    比较两边的结果，我们得到 $|S=1, M=0\rangle$ 的表达式 [@problem_id:2087721]：
    $$ |1, 0\rangle = \frac{1}{\sqrt{2}} (|\uparrow\downarrow\rangle + |\downarrow\uparrow\rangle) $$
    这个表达式告诉我们，如果在 $|1, 0\rangle$ 态上测量单个粒子的自旋z分量，我们有 $1/(\sqrt{2})^2 = 1/2$ 的概率发现粒子1自旋向上而粒子2自旋向下，也有 $1/2$ 的概率发现粒子1自旋向下而粒子2自旋向上。这里 $1/\sqrt{2}$ 就是相应的CG系数 $\langle 1/2, 1/2; 1/2, -1/2 | 1, 0 \rangle$ [@problem_id:2087666]。

3.  **其他状态**：再次应用下降算符可以得到 $|1, -1\rangle = |\downarrow\downarrow\rangle$。最后，单态 $|S=0, M=0\rangle$ 必须与 $|1, 0\rangle$ 正交，并且归一化。这唯一地确定了它的形式（在标准[相角](@entry_id:274491)约定下）：
    $$ |0, 0\rangle = \frac{1}{\sqrt{2}} (|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle) $$

值得注意的是，除了两个“拉伸”态 $|1, 1\rangle$ 和 $|1, -1\rangle$ 之外，耦合态 $|1, 0\rangle$ 和 $|0, 0\rangle$ 都无法写成单个[非耦合基](@entry_id:156676)矢（即乘积态）的形式。它们是两个[非耦合基](@entry_id:156676)矢的线性叠加。这种无法分解为单个乘积态的特性正是量子力学中 **纠缠** 的标志。因此，耦合过程通常会产生[纠缠态](@entry_id:152310) [@problem_id:2087696]。

### 物理应用与算符表示

选择哪种表象最方便，取决于我们想要对角化（即寻找其本征态）的[哈密顿量](@entry_id:172864)。

#### [泡利不相容原理](@entry_id:141850)与[自旋对称性](@entry_id:197993)

对于全同[费米子](@entry_id:146235)（如电子）系统，[泡利不相容原理](@entry_id:141850)要求总[波函数](@entry_id:147440)（空间部分与自旋部分的乘积）在交换任意两个粒子时必须是反对称的 [@problem_id:2087722]。
$$ \Psi(1, 2) = \Psi_{\text{spatial}}(r_1, r_2) \chi_{\text{spin}}(s_1, s_2) = -\Psi(2, 1) $$
如果空间[波函数](@entry_id:147440) $\Psi_{\text{spatial}}$ 是对称的（例如，两个电子处于相同的[轨道](@entry_id:137151)态），那么[自旋波函数](@entry_id:190161) $\chi_{\text{spin}}$ 必须是反对称的，以满足总[波函数](@entry_id:147440)的反对称性。对于两个自旋1/2的粒子，反对称的自旋态正是自旋单态 $|S=0, M=0\rangle$。反之，如果空间[波函数](@entry_id:147440)是反对称的，自旋部分就必须是[三重态](@entry_id:156705)中的一个（它们都是对称的）。因此，总自旋[量子数](@entry_id:145558) $S$ 直接与[交换对称性](@entry_id:151892)联系在一起。

#### [相互作用哈密顿量](@entry_id:181720)

许多重要的物理相互作用依赖于[总角动量](@entry_id:155748)。一个典型的例子是两个自旋之间的相互作用，其[哈密顿量](@entry_id:172864)形式为 $H_{int} \propto \mathbf{S}_1 \cdot \mathbf{S}_2$。这出现在氢原子的[超精细结构](@entry_id:158349) [@problem_id:2087703] 或[量子点](@entry_id:143385)中电子的交换相互作用 [@problem_id:2087668] 中。

为了分析这个算符，我们可以利用一个关键的恒等式，它来自于对总[自旋算符](@entry_id:155419)平方的展开 $S^2 = (\mathbf{S}_1 + \mathbf{S}_2)^2 = S_1^2 + S_2^2 + 2\mathbf{S}_1 \cdot \mathbf{S}_2$。由此可得：
$$ \mathbf{S}_1 \cdot \mathbf{S}_2 = \frac{1}{2} (S^2 - S_1^2 - S_2^2) $$
这个形式的巨大优势在于，算符的右边只包含各个角动量大小的平方。由于耦合态 $|S, M_S\rangle$ 是 $S^2$, $S_1^2$, $S_2^2$ 的共同本征态，这意味着 $\mathbf{S}_1 \cdot \mathbf{S}_2$ 算符在 **[耦合表象](@entry_id:136812)中是对角的**。

它的[本征值](@entry_id:154894)（即[对角矩阵](@entry_id:637782)元）可以立即读出。对于两个自旋1/2的粒子 ($s_1=s_2=1/2, S_1^2 \to \frac{3}{4}\hbar^2, S_2^2 \to \frac{3}{4}\hbar^2$):
- 对于[三重态](@entry_id:156705) ($S=1, S^2 \to 2\hbar^2$):
  $$ \langle \mathbf{S}_1 \cdot \mathbf{S}_2 \rangle_{\text{triplet}} = \frac{1}{2} (2\hbar^2 - \frac{3}{4}\hbar^2 - \frac{3}{4}\hbar^2) = \frac{1}{4}\hbar^2 $$
- 对于单态 ($S=0, S^2 \to 0$):
  $$ \langle \mathbf{S}_1 \cdot \mathbf{S}_2 \rangle_{\text{singlet}} = \frac{1}{2} (0 - \frac{3}{4}\hbar^2 - \frac{3}{4}\hbar^2) = -\frac{3}{4}\hbar^2 $$
因此，耦合[基矢](@entry_id:199546)是这种[相互作用哈密顿量](@entry_id:181720)的[本征态](@entry_id:149904)，[耦合表象](@entry_id:136812)是研究这类问题的“自然”语言。

#### 不同表象中的算符矩阵

选择的表象不仅决定了状态向量的表示，也决定了算符的[矩阵表示](@entry_id:146025)。

- 在[耦合表象](@entry_id:136812)中对角的算符（如 $\mathbf{S}_1 \cdot \mathbf{S}_2$），在非[耦合表象](@entry_id:136812)中通常不是对角的。我们可以通过将其展开为分量形式来验证这一点：
  $$ \mathbf{S}_1 \cdot \mathbf{S}_2 = S_{1z}S_{2z} + \frac{1}{2}(S_{1+}S_{2-} + S_{1-}S_{2+}) $$
  $S_{1z}S_{2z}$ 项在[非耦合基](@entry_id:156676)矢 $\{|\uparrow\uparrow\rangle, |\uparrow\downarrow\rangle, |\downarrow\uparrow\rangle, |\downarrow\downarrow\rangle\}$ 中是对角的。然而，flip-flop项 $S_{1+}S_{2-}$ 和 $S_{1-}S_{2+}$ 是非对角的，它们会引起态之间的跃迁。例如，它可以将 $|\downarrow\uparrow\rangle$ 变换为 $|\uparrow\downarrow\rangle$。计算[矩阵元](@entry_id:186505) $\langle \uparrow\downarrow | \mathbf{S}_1 \cdot \mathbf{S}_2 | \downarrow\uparrow \rangle$ 会得到一个非零值 [@problem_id:2087668]，这表明 $\mathbf{S}_1 \cdot \mathbf{S}_2$ 在此基底下存在非对角元，它混合了 $|\uparrow\downarrow\rangle$ 和 $|\downarrow\uparrow\rangle$ 这两个状态。

- 反之，在非[耦合表象](@entry_id:136812)中对角的算符（如单个粒子的自旋分量 $S_{2z}$），在[耦合表象](@entry_id:136812)中通常不是对角的。让我们看看 $S_{2z}$ 在耦合[基矢](@entry_id:199546) $\left\{|1,1\rangle, |1,0\rangle, |1,-1\rangle, |0,0\rangle\right\}$ 上的作用 [@problem_id:2087683]：
  $$ S_{2z}|1,0\rangle = S_{2z} \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle + |\downarrow\uparrow\rangle) = \frac{1}{\sqrt{2}} (-\frac{\hbar}{2}|\uparrow\downarrow\rangle + \frac{\hbar}{2}|\downarrow\uparrow\rangle) $$
  这个结果不能表示为 $|1,0\rangle$ 的倍数。实际上，通过重新组合，我们可以发现它与单态 $|0,0\rangle$ 有关：
  $$ S_{2z}|1,0\rangle = -\frac{\hbar}{2} \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle) = -\frac{\hbar}{2}|0,0\rangle $$
  同样可以算出 $S_{2z}|0,0\rangle = -\frac{\hbar}{2}|1,0\rangle$。这意味着 $S_{2z}$ 的矩阵在[耦合表象](@entry_id:136812)中具有非对角元，它混合了 $|1,0\rangle$ 和 $|0,0\rangle$。这清晰地说明了两种表象之间的权衡：[耦合表象](@entry_id:136812)简化了总角动量和相互作用算符，而非[耦合表象](@entry_id:136812)简化了与单个子系统相关的算符。

### 复合系统中的测量

最后，让我们将这些形式化的工具与实际的测量过程联系起来。假设一个系统被制备在某个耦合态，我们随后去测量其中一个子系统的物理量（例如，z方向自旋）。结果的[概率分布](@entry_id:146404)由CG系数的平方决定。

考虑一个由两个自旋1/2粒子组成的系统，被制备在以下归一化的叠加态 [@problem_id:2087696]：
$$ |\psi\rangle = \sqrt{\frac{1}{5}} |J=1, M=1\rangle + \sqrt{\frac{4}{5}} |J=1, M=0\rangle $$

现在，我们同时测量两个粒子的z方向自旋 $S_{1z}$ 和 $S_{2z}$。我们想知道，测量结果为粒子1自旋向上 ($m_{s1}=+1/2$) 而粒子2自旋向下 ($m_{s2}=-1/2$) 的概率是多少？

要回答这个问题，我们需要将态 $|\psi\rangle$ 在非[耦合表象](@entry_id:136812)中展开。测量结果的概率幅就是 $|\psi\rangle$ 在[非耦合基](@entry_id:156676)矢 $|m_{s1}, m_{s2}\rangle = |+1/2, -1/2\rangle$ (即 $|\uparrow\downarrow\rangle$) 上的投影。

首先，我们将 $|\psi\rangle$ 中的耦合态用非耦合态表示：
$$ |1, 1\rangle = |\uparrow\uparrow\rangle $$
$$ |1, 0\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle + |\downarrow\uparrow\rangle) $$

代入 $|\psi\rangle$ 的表达式中：
$$ |\psi\rangle = \sqrt{\frac{1}{5}} |\uparrow\uparrow\rangle + \sqrt{\frac{4}{5}} \left[ \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle + |\downarrow\uparrow\rangle) \right] $$
$$ |\psi\rangle = \sqrt{\frac{1}{5}} |\uparrow\uparrow\rangle + \sqrt{\frac{2}{5}} |\uparrow\downarrow\rangle + \sqrt{\frac{2}{5}} |\downarrow\uparrow\rangle $$

现在，我们可以清晰地看到态 $|\uparrow\downarrow\rangle$ 的[概率幅](@entry_id:150609)是 $\sqrt{2/5}$。根据量子力学的测量公设，得到该结果的概率是概率幅的模平方：
$$ P(m_{s1}=+1/2, m_{s2}=-1/2) = |\langle \uparrow\downarrow | \psi \rangle|^2 = \left| \sqrt{\frac{2}{5}} \right|^2 = \frac{2}{5} $$

这个例子完美地展示了两种表象的协同作用。系统的演化或制备可能在[耦合表象](@entry_id:136812)中更自然地描述，而测量过程通常是在非[耦合表象](@entry_id:136812)中进行的。在它们之间进行转换的能力，正是熟练运用角动量理论的核心技能。