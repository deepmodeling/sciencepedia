## 引言
在量子世界中，复合系统无处不在——从原子内电子的[轨道运动](@entry_id:162856)与自身旋转的结合，到[原子核](@entry_id:167902)内质子与中子的相互作用。理解这些复合系统的关键，在于掌握如何将其各个组成部分的角动量正确地“相加”。然而，这并非简单的标量求和，而是一个深刻的量子力学问题。描述复合系统存在两种自然但截然不同的视角：一种是分别描述每个子系统的“非[耦合表象](@entry_id:136812)”，另一种是描述系统整体总角动量的“[耦合表象](@entry_id:136812)”。当子系统间存在依赖于[总角动量](@entry_id:155748)的相互作用时（例如[自旋-轨道耦合](@entry_id:143520)），后者变得至关重要。本文旨在系统地解决在这两种表象之间进行转换的核心问题，其答案就蕴含在被称为Clebsch-Gordan系数的数学工具之中。

本文将分为三个部分，引导您全面掌握这一概念。在“原理与机制”一章中，我们将深入探讨[角动量耦合](@entry_id:145967)的物理动机，定义耦合与非[耦合表象](@entry_id:136812)，推导支配[角动量相加](@entry_id:145967)的[选择定则](@entry_id:140784)，并详细介绍Clebsch-Gordan系数的定义、性质及计算方法。接下来，在“应用与跨学科联系”一章中，我们将展示这些系数如何在原子物理（精细结构、[塞曼效应](@entry_id:154144)）、分子物理（核[自旋统计](@entry_id:161373)）乃至粒子物理（[同位旋对称性](@entry_id:146063)）等多个前沿领域中发挥关键作用，并最终将其与更为普适的[维格纳-埃卡特定理](@entry_id:144878)联系起来。最后，“实践练习”部分将提供一系列具体问题，帮助您巩固理论知识并将其付诸实践。通过本次学习，您将能够熟练运用Clebsch-Gordan系数来分析和解决复杂的[量子多体问题](@entry_id:146763)。

## 原理与机制

在量子力学中，当我们将两个或多个独立的系统组合成一个复合系统时，一个核心任务是理解各个子系统的角动量如何耦合成一个[总角动量](@entry_id:155748)。这个过程不仅是数学上的综合，更深刻地反映了粒子间相互作用的物理实在，例如原子中电子的[轨道角动量与自旋角动量](@entry_id:167026)的耦合（自旋-轨道耦合），或电子[总角动量](@entry_id:155748)与[原子核](@entry_id:167902)自旋的耦合（[超精细结构](@entry_id:158349)）。本章将深入探讨角动量相加的原理与机制，并引入描述这一过程的关键数学工具——Clebsch-Gordan系数。

### 角动量耦合的挑战：两套[基矢](@entry_id:199546)

考虑一个由两个子系统组成的复合系统，它们各自拥有[角动量算符](@entry_id:153013) $\hat{\mathbf{J}}_1$ 和 $\hat{\mathbf{J}}_2$。这两个算符分别作用于各自的[希尔伯特空间](@entry_id:261193)，并且相互对易，即 $[\hat{J}_{1\alpha}, \hat{J}_{2\beta}] = 0$。描述这个复合系统的状态有两种自然的方式，对应两套不同的[基矢](@entry_id:199546)。

第一种是**非[耦合表象](@entry_id:136812)**（uncoupled representation）。在这套表象中，我们选择一组对每个子系统都完备的[对易算符](@entry_id:149529)集。通常，这组算符是 $\{\hat{\mathbf{J}}_1^2, \hat{J}_{1z}, \hat{\mathbf{J}}_2^2, \hat{J}_{2z}\}$。它们的共同[本征态](@entry_id:149904)是两个子系统[本征态](@entry_id:149904)的简单直积，记作 $|j_1, m_1\rangle |j_2, m_2\rangle$ 或简写为 $|j_1, m_1; j_2, m_2\rangle$。这里，$j_1$ 和 $j_2$ 是角动量大小的量子数，$m_1$ 和 $m_2$ 是它们在 $z$ 轴上投影的量子数。这套[基矢](@entry_id:199546)的优点是物理图像清晰：它精确地描述了每个子系统各自的角动量状态。

然而，当子系统之间存在相互作用时，非[耦合表象](@entry_id:136812)往往不再是最便利的选择。许多物理相互作用的[哈密顿量](@entry_id:172864)依赖于系统的**[总角动量](@entry_id:155748)** $\hat{\mathbf{J}} = \hat{\mathbf{J}}_1 + \hat{\mathbf{J}}_2$。例如，[超精细相互作用](@entry_id:137748)的能量正比于 $\mathbf{I} \cdot \mathbf{J}$，其中 $\mathbf{I}$ 是核自旋角动量，$\mathbf{J}$ 是电子[总角动量](@entry_id:155748) [@problem_id:1358328]。这样的[哈密顿量](@entry_id:172864)通常与 $\hat{\mathbf{J}}_1^2$ 和 $\hat{\mathbf{J}}_2^2$ 对易，但也与总角动量平方算符 $\hat{\mathbf{J}}^2$ 和其 $z$ 分量 $\hat{J}_z$ 对易。然而，$\hat{\mathbf{J}}^2$ 通常与 $\hat{J}_{1z}$ 和 $\hat{J}_{2z}$ 不对易。这意味着，系统的[能量本征态](@entry_id:152154)（定态）通常不是[非耦合基](@entry_id:156676)矢，而是在[总角动量](@entry_id:155748)确定的表象下具有确定值的态。

这就引出了第二种描述方式：**[耦合表象](@entry_id:136812)**（coupled representation）。这套表象的[基矢](@entry_id:199546)是[总角动量算符](@entry_id:149439)集 $\{\hat{\mathbf{J}}^2, \hat{J}_z, \hat{\mathbf{J}}_1^2, \hat{\mathbf{J}}_2^2\}$ 的共同本征态，记作 $|j, m\rangle$（其中 $j_1, j_2$ 通常是隐含的）。这些态具有确定的[总角动量量子数](@entry_id:164948) $j$ 和总磁量子数 $m$ [@problem_id:1358330]。在[耦合表象](@entry_id:136812)中，描述依赖于[总角动量](@entry_id:155748)的相互作用变得简单，因为[哈密顿量](@entry_id:172864)矩阵是（或近似是）对角的。

我们的核心任务，便是建立这两套完备正交基之间的变换关系。这一变换的系数，就是Clebsch-Gordan系数。

### [角动量相加](@entry_id:145967)的[选择定则](@entry_id:140784)

在将[非耦合基](@entry_id:156676)矢与耦合[基矢](@entry_id:199546)联系起来之前，我们首先需要确定，给定 $j_1$ 和 $j_2$，[总角动量量子数](@entry_id:164948) $j$ 和 $m$ 可以取哪些值。这由两条基本的**选择定则**所支配。

第一条定则涉及[磁量子数](@entry_id:145584)。总角动量的 $z$ 分量算符就是子系统 $z$ 分量算符之和：$\hat{J}_z = \hat{J}_{1z} + \hat{J}_{2z}$。让我们将此算符作用于一个[非耦合基](@entry_id:156676)矢 $|j_1, m_1; j_2, m_2\rangle$：
$$ \hat{J}_z |j_1, m_1; j_2, m_2\rangle = (\hat{J}_{1z} + \hat{J}_{2z}) |j_1, m_1; j_2, m_2\rangle = (\hbar m_1 + \hbar m_2) |j_1, m_1; j_2, m_2\rangle = \hbar(m_1 + m_2) |j_1, m_1; j_2, m_2\rangle $$
这表明，非耦合态 $|j_1, m_1; j_2, m_2\rangle$ 本身就是 $\hat{J}_z$ 的本征态，其[本征值](@entry_id:154894)为 $\hbar(m_1 + m_2)$。另一方面，根据定义，耦合态 $|j, m\rangle$ 也是 $\hat{J}_z$ 的本征态，[本征值](@entry_id:154894)为 $\hbar m$。由于耦合态可以表示为非耦合态的[线性组合](@entry_id:154743)，一个具有确定 $m$ 值的耦合态，只能由那些具有相同 $\hat{J}_z$ [本征值](@entry_id:154894)的非耦合态叠加而成。因此，我们得到了第一条至关重要的[选择定则](@entry_id:140784) [@problem_id:1358295]：
$$ m = m_1 + m_2 $$
任何不满足这个条件的Clebsch-Gordan系数都必定为零。

第二条定则，即著名的**三角不等式**，限制了[总角动量量子数](@entry_id:164948) $j$ 的可能取值。对于给定的 $j_1$ 和 $j_2$，[量子数](@entry_id:145558) $j$ 只能取以下范围内的值：
$$ |j_1 - j_2| \le j \le j_1 + j_2 $$
并且 $j$ 的取值以整数为步长，即 $j = |j_1 - j_2|, |j_1 - j_2| + 1, \dots, j_1 + j_2$。这个规则可以直观地理解为量子化的“矢量相加”法则。

例如，在一个氘原子的简化模型中，[原子核](@entry_id:167902)由一个质子（自旋 $s_p = 1/2$）和一个中子（自旋 $s_n = 1/2$）组成。它们耦合形成的总核自旋 $I$ 的可能取值为 $|1/2 - 1/2|, \dots, 1/2 + 1/2$，即 $I \in \{0, 1\}$。如果原子处于一个[激发态](@entry_id:261453)，电子的[轨道角动量](@entry_id:191303)为 $l=1$，[电子自旋](@entry_id:137016)为 $s_e=1/2$，则电子的[总角动量](@entry_id:155748) $J$ 的可能取值为 $|1 - 1/2|, \dots, 1 + 1/2$，即 $J \in \{1/2, 3/2\}$。最终，原子的总角动量 $F$ 由核自旋 $I$ 和电子总角动量 $J$ 耦合而成。将所有可能的 $(I, J)$ 组合进行耦合，我们可以得到所有可能的 $F$ 值 [@problem_id:1358294]：
- 若 $I=0, J=1/2 \implies F=1/2$
- 若 $I=0, J=3/2 \implies F=3/2$
- 若 $I=1, J=1/2 \implies F \in \{1/2, 3/2\}$
- 若 $I=1, J=3/2 \implies F \in \{1/2, 3/2, 5/2\}$
综合所有情况，该原子[总角动量量子数](@entry_id:164948) $F$ 的所有可能测量值是 $\{1/2, 3/2, 5/2\}$。

一个重要的原则是，从非[耦合表象](@entry_id:136812)到[耦合表象](@entry_id:136812)的变换是**幺正变换**，它保持了希尔伯特空间的维度。[非耦合基](@entry_id:156676)矢的总数为 $(2j_1+1)(2j_2+1)$。在[耦合表象](@entry_id:136812)中，对于每个可能的 $j$ 值，都有 $(2j+1)$ 个简并的 $m$ 态（从 $-j$ 到 $+j$）。态数的守恒要求所有可能 $j$ 值的简并度之和等于[非耦合基](@entry_id:156676)矢的总数：
$$ \sum_{j=|j_1-j_2|}^{j_1+j_2} (2j+1) = (2j_1+1)(2j_2+1) $$
我们可以用一个例子来验证。当耦合 $j_1=1$ 和 $j_2=3/2$ 时，可能的 $J$ 值为 $1/2, 3/2, 5/2$。耦合态的总数是 $(2 \cdot 1/2 + 1) + (2 \cdot 3/2 + 1) + (2 \cdot 5/2 + 1) = 2 + 4 + 6 = 12$。这与非耦合态的总数 $(2 \cdot 1 + 1)(2 \cdot 3/2 + 1) = 3 \cdot 4 = 12$ 完全一致，验证了态数守恒原则 [@problem_id:1358312]。

### Clebsch-Gordan系数：变换矩阵

有了选择定则，我们现在可以正式定义联系这两个表象的**Clebsch-Gordan系数**（简称CGCs）。它们是幺正[变换矩阵](@entry_id:151616)的[矩阵元](@entry_id:186505)，定义为耦合[基矢](@entry_id:199546)在[非耦合基](@entry_id:156676)矢上的展开系数 [@problem_id:2760430]：
$$ |j, m\rangle = \sum_{m_1, m_2} |j_1, m_1; j_2, m_2\rangle \langle j_1, m_1; j_2, m_2 | j, m \rangle $$
这里的系数 $\langle j_1, m_1; j_2, m_2 | j, m \rangle$ 就是Clebsch-Gordan系数。由于 $m=m_1+m_2$ 的选择定则，求和实际上只对满足 $m_1+m_2=m$ 的项进行。

由于变换是幺正的，[逆变](@entry_id:192290)换关系同样成立：
$$ |j_1, m_1; j_2, m_2\rangle = \sum_{j, m} |j, m\rangle \langle j, m | j_1, m_1; j_2, m_2 \rangle $$
由于[基矢](@entry_id:199546)的正交归一性，CGCs也满足相应的[正交关系](@entry_id:145540)。特别地，由于任何一个[非耦合基](@entry_id:156676)矢 $|j_1, m_1; j_2, m_2\rangle$ 都是归一化的，我们可以对其范数进行计算：
$$ \langle j_1, m_1; j_2, m_2 | j_1, m_1; j_2, m_2 \rangle = 1 $$
将上述展开式代入，并利用耦合[基矢](@entry_id:199546) $|j, m\rangle$ 的正交性 $\langle j, m | j', m' \rangle = \delta_{jj'} \delta_{mm'}$，我们得到一个重要的求和规则 [@problem_id:1358280]：
$$ \sum_{j=|j_1-j_2|}^{j_1+j_2} |\langle j, m_1+m_2 | j_1, m_1; j_2, m_2 \rangle|^2 = 1 $$
这个关系式的物理解释是：一个处于特定非耦合态 $|j_1, m_1; j_2, m_2\rangle$ 的系统，当测量其总角动量 $j$ 时，测量结果必然是某个允许的 $j$ 值，所有可能结果的概率之和为1。而 $|\langle j, m_1+m_2 | j_1, m_1; j_2, m_2 \rangle|^2$ 正是测得总角动量为 $j$ 的概率。

值得注意的是，CGCs的定义存在一个相位模糊性。为了消除这种模糊性并[标准化](@entry_id:637219)所有计算，物理学界普遍采用**Condon-Shortley相约定**。该约定规定：
1.  所有的Clebsch-Gordan系数都是实数。
2.  对于最大总角动量 $j = j_1+j_2$ 的“拉伸态”（stretched state），其系数为正一。即，耦合两个[最高权](@entry_id:202808)重态 $|j_1, m_1=j_1\rangle$ 和 $|j_2, m_2=j_2\rangle$ 时，得到的总角动量最高权重态 $|j=j_1+j_2, m=j_1+j_2\rangle$ 的系数为+1：
    $$ \langle j_1, j_1; j_2, j_2 | j_1+j_2, j_1+j_2 \rangle = +1 $$
这个约定，结合[升降算符](@entry_id:197899)的[递推关系](@entry_id:189264)，可以唯一地确定所有CGCs的数值和符号 [@problem_id:2760430]。

### Clebsch-Gordan系数的计算与应用

#### 具体计算：两个自旋1/2粒子的耦合

掌握了基本原理，我们来看一个最基本也最重要的例子：耦合两个自旋1/2的粒子。设 $j_1=s_1=1/2$, $j_2=s_2=1/2$。可能的总[自旋量子数](@entry_id:142550) $j$ 为 $|1/2-1/2|=0$ 和 $1/2+1/2=1$。因此，我们得到一个**自旋单态**（$j=0$，非简并）和一个**自旋三重态**（$j=1$，三重简并）。让我们用[升降算符法](@entry_id:185152)推导它们的态函数。我们将自旋向上态 $|s=1/2, m_s=1/2\rangle$ 记为 $|\uparrow\rangle$，自旋向下态 $|s=1/2, m_s=-1/2\rangle$ 记为 $|\downarrow\rangle$。

1.  **[最高权](@entry_id:202808)重态**：总[磁量子数](@entry_id:145584) $m$ 的最大值为 $m=m_1+m_2 = 1/2+1/2=1$。这个态只能对应于 $j=1$，因此它是耦合态 $|j=1, m=1\rangle$。根据[Condon-Shortley约定](@entry_id:269147)，它与非耦合态的关系是：
    $$ |j=1, m=1\rangle = |\uparrow\uparrow\rangle $$

2.  **应用降算符**：现在我们应用总降算符 $\hat{J}_- = \hat{S}_{1-} + \hat{S}_{2-}$ 来得到 $m=0$ 的态。
    作用于耦合态：
    $$ \hat{J}_- |1, 1\rangle = \hbar\sqrt{1(1+1) - 1(1-1)} |1, 0\rangle = \hbar\sqrt{2} |1, 0\rangle $$
    作用于非耦合态：
    $$ (\hat{S}_{1-} + \hat{S}_{2-}) |\uparrow\uparrow\rangle = (\hat{S}_{1-}|\uparrow\rangle_1)|\uparrow\rangle_2 + |\uparrow\rangle_1(\hat{S}_{2-}|\uparrow\rangle_2) = (\hbar|\downarrow\rangle_1)|\uparrow\rangle_2 + |\uparrow\rangle_1(\hbar|\downarrow\rangle_2) = \hbar (|\downarrow\uparrow\rangle + |\uparrow\downarrow\rangle) $$
    比较两式，我们得到三重态中的 $m=0$ 态：
    $$ |j=1, m=0\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle + |\downarrow\uparrow\rangle) $$

3.  **构造正交态**：总磁量子数 $m=0$ 也可以由 $m_1=1/2, m_2=-1/2$ 和 $m_1=-1/2, m_2=1/2$ 组合而成，所以 $m=0$ 的[子空间](@entry_id:150286)是二维的。除了上面得到的 $|j=1, m=0\rangle$ 态，还必须存在另一个与它正交的态，这个态就是单态 $|j=0, m=0\rangle$。通过正交性要求 $\langle 1, 0 | 0, 0 \rangle = 0$，我们可以唯一确定单态的组合方式。对于一般形式 $a|\uparrow\downarrow\rangle + b|\downarrow\uparrow\rangle$，正交条件给出 $\frac{1}{\sqrt{2}}(a^*+b^*)=0$。选择实系数并归一化，我们得到 [@problem_id:2084397]：
    $$ |j=0, m=0\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle) $$
    这个反对称组合就是著名的贝尔态之一，是[量子纠缠](@entry_id:136576)的典型例子。

#### 应用1：预测测量结果

CGCs的直接应用是计算在不同表象间进行测量时的概率。假设一个系统被制备在非耦合态 $|L=1, M_L=1\rangle |S=1/2, M_S=-1/2\rangle$。现在我们要测量其[总角动量](@entry_id:155748) $J$。可能的结果是 $J=1/2$ 或 $J=3/2$。测得 $J=1/2$ 的概率是多少？ [@problem_id:2084365]

为此，我们需要将这个非耦合态用耦合[基矢](@entry_id:199546) $|J, M_J\rangle$ 展开。这相当于进行逆向变换。通过求解上述两个自旋1/2粒子耦合的[线性方程组](@entry_id:148943)，我们可以反解出：
$$ |\uparrow\downarrow\rangle = \frac{1}{\sqrt{2}}(|1, 0\rangle + |0, 0\rangle) $$
$$ |\downarrow\uparrow\rangle = \frac{1}{\sqrt{2}}(|1, 0\rangle - |0, 0\rangle) $$
对于 $L=1, S=1/2$ 的情况，通过类似的[升降算符法](@entry_id:185152)可以推导出：
$$ |L=1, M_L=1; S=1/2, M_S=-1/2\rangle = \sqrt{\frac{1}{3}}|J=3/2, M_J=1/2\rangle - \sqrt{\frac{2}{3}}|J=1/2, M_J=1/2\rangle $$
根据量子力学的测量公设，测量总角动量得到 $J=1/2$ 的概率就是其展开系数的模平方：
$$ P(J=1/2) = \left|-\sqrt{\frac{2}{3}}\right|^2 = \frac{2}{3} $$
同样，测得 $J=3/2$ 的概率为 $|\sqrt{1/3}|^2 = 1/3$。两者之和为1，符合概率解释。

#### 应用2：[能谱](@entry_id:181780)与动力学

CGCs的物理意义在处理相互作用和时间演化时表现得最为深刻。

**[能谱](@entry_id:181780)结构**：考虑一个由[哈密顿量](@entry_id:172864) $H = \frac{J_c}{\hbar^2} \mathbf{S}_1 \cdot \mathbf{S}_2$ 描述的自旋相互作用系统 [@problem_id:1358317]。我们可以将 $\mathbf{S}_1 \cdot \mathbf{S}_2$ 用总[自旋算符](@entry_id:155419)表示：
$$ \mathbf{S}_1 \cdot \mathbf{S}_2 = \frac{1}{2}(\hat{\mathbf{J}}^2 - \hat{\mathbf{S}}_1^2 - \hat{\mathbf{S}}_2^2) $$
由于耦合态 $|j, m\rangle$ 是 $\hat{\mathbf{J}}^2$, $\hat{\mathbf{S}}_1^2$, $\hat{\mathbf{S}}_2^2$ 的共同[本征态](@entry_id:149904)，它们也是这个[哈密顿量](@entry_id:172864)的本征态（[能量本征态](@entry_id:152154)）。其[能量本征值](@entry_id:144381) $E_j$ 为：
$$ E_j = \frac{J_c}{2\hbar^2} [\hbar^2 j(j+1) - \hbar^2 s_1(s_1+1) - \hbar^2 s_2(s_2+1)] $$
对于两个自旋1/2粒子系统，$s_1=s_2=1/2$。单态（$j=0$）的能量为 $E_S = -3J_c/4$，而[三重态](@entry_id:156705)（$j=1$）的能量为 $E_T = J_c/4$。[哈密顿量](@entry_id:172864)在[耦合表象](@entry_id:136812)中是对角的，但在非[耦合表象](@entry_id:136812)中不是。CGCs正是实现这一[对角化](@entry_id:147016)变换的矩阵。

**[量子动力学](@entry_id:138183)**：现在考虑一个系统在 $t=0$ 时被制备在非耦合态 $|\psi(0)\rangle = |\uparrow\downarrow\rangle$。这个态不是[能量本征态](@entry_id:152154)，而是[能量本征态](@entry_id:152154) $|1, 0\rangle$ 和 $|0, 0\rangle$ 的叠加：
$$ |\psi(0)\rangle = \frac{1}{\sqrt{2}}(|1, 0\rangle + |0, 0\rangle) $$
随时间演化，每个能量本征态会获得一个相位因子 $e^{-iEt/\hbar}$：
$$ |\psi(t)\rangle = \frac{1}{\sqrt{2}} (e^{-iE_T t/\hbar}|1, 0\rangle + e^{-iE_S t/\hbar}|0, 0\rangle) $$
将耦合态用非耦合态展开，我们可以看到系统状态随时间的变化：
$$ |\psi(t)\rangle = \frac{1}{2} [e^{-iE_T t/\hbar}(|\uparrow\downarrow\rangle + |\downarrow\uparrow\rangle) + e^{-iE_S t/\hbar}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle)] $$
$$ |\psi(t)\rangle = \frac{1}{2} (e^{-iE_T t/\hbar} + e^{-iE_S t/\hbar})|\uparrow\downarrow\rangle + \frac{1}{2} (e^{-iE_T t/\hbar} - e^{-iE_S t/\hbar})|\downarrow\uparrow\rangle $$
系统在 $|\uparrow\downarrow\rangle$ 和 $|\downarrow\uparrow\rangle$ 两个状态之间[振荡](@entry_id:267781)。例如，系统演化到状态 $|\downarrow\uparrow\rangle$ 的概率为：
$$ P(|\downarrow\uparrow\rangle, t) = \left|\frac{1}{2} (e^{-iE_T t/\hbar} - e^{-iE_S t/\hbar})\right|^2 = \sin^2\left(\frac{(E_T-E_S)t}{2\hbar}\right) = \sin^2\left(\frac{J_c t}{2\hbar}\right) $$
当 $\frac{J_c t}{2\hbar} = \frac{\pi}{2}$，即 $t = \frac{\pi\hbar}{J_c}$ 时，这个概率首次达到1。这意味着系统完全从 $|\uparrow\downarrow\rangle$ 翻转到了 $|\downarrow\uparrow\rangle$ [@problem_id:1358317]。这种现象，称为[量子拍](@entry_id:155286)或[Rabi振荡](@entry_id:137940)，是初始态在不同[能量本征态](@entry_id:152154)上叠加的直接后果，而Clebsch-Gordan系数正是连接这两个图像的桥梁。

综上所述，Clebsch-Gordan系数不仅是连接不同量子力学表象的数学工具，它们更是理解和量化粒子间相互作用、预测测量结果以及描述系统动力学演化的物理核心。