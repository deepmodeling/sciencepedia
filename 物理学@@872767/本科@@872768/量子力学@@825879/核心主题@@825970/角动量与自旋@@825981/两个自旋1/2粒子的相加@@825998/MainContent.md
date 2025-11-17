## 引言
从单个自旋1/2粒子的量子特性出发，我们自然会问：当两个这样的粒子构成一个系统时，会发生什么？这个问题并非简单的数量叠加，而是通往理解量子多体世界复杂性的门户。两个自旋1/2粒子系统的行为是理解原子结构、材料磁性乃至[量子纠缠](@entry_id:136576)等深刻概念的基础。然而，如何从单个粒子的独立状态过渡到描述整个系统的集体行为，并揭示其独特的量子特性，构成了量子力学中的一个核心挑战。本文旨在系统性地解决这一问题。在“原理与机制”一章中，我们将构建描述双粒子系统的数学框架，推导出关键的单态和[三重态](@entry_id:156705)，并探讨它们的对称性和纠缠特性。随后的“应用与跨学科联系”一章将展示这些抽象概念如何在原子物理、[凝聚态物质](@entry_id:747660)和[量子信息](@entry_id:137721)等多个领域中发挥关键作用。最后，“动手实践”部分将通过具体问题，帮助读者巩固和应用所学知识。现在，让我们首先深入探讨构建这个复合系统的基本原理和内在机制。

## 原理与机制

在理解了单个自旋1/2粒子的量子行为之后，我们自然会进一步探究由两个此类粒子组成的复合系统。两个自旋1/2粒子的相互作用和耦合是量子力学中的一个基本模型，它不仅是理解多体系统（如原子、分子和固体）中磁性现象的基石，也为[量子信息](@entry_id:137721)和[量子计算](@entry_id:142712)等前沿领域提供了核心概念，如量子纠缠。本章将系统地阐述两个自旋1/2粒子总自旋的叠加原理及其背后的关键机制。

### 复合系统的态空间与表象

一个自旋1/2粒子的状态可以用一个二维[复向量空间](@entry_id:264355)（[希尔伯特空间](@entry_id:261193)）来描述，其标准[基矢](@entry_id:199546)为自旋向上态 $|\uparrow\rangle$ 和自旋向下态 $|\downarrow\rangle$。这两个态是自旋z分量算符 $S_z$ 的[本征态](@entry_id:149904)，[本征值](@entry_id:154894)分别为 $+\frac{\hbar}{2}$ 和 $-\frac{\hbar}{2}$。

当系统包含两个可区分的粒子（标记为1和2）时，其总的希尔伯特空间是两个子系统[希尔伯特空间](@entry_id:261193)的**张量积**。因此，描述这个双[粒子系统](@entry_id:180557)的态空间是四维的。最自然的一组[基矢](@entry_id:199546)是由单个粒子基矢的[张量积](@entry_id:140694)构成的，我们称之为**非[耦合表象](@entry_id:136812)**（或乘积[基矢](@entry_id:199546)）：
$$
|\uparrow\uparrow\rangle \equiv |\uparrow\rangle_1 \otimes |\uparrow\rangle_2
$$
$$
|\uparrow\downarrow\rangle \equiv |\uparrow\rangle_1 \otimes |\downarrow\rangle_2
$$
$$
|\downarrow\uparrow\rangle \equiv |\downarrow\rangle_1 \otimes |\uparrow\rangle_2
$$
$$
|\downarrow\downarrow\rangle \equiv |\downarrow\rangle_1 \otimes |\downarrow\rangle_2
$$
其中，例如 $|\uparrow\downarrow\rangle$ 表示粒子1处于自旋向上态，而粒子2处于自旋向下态。在这个表象中，每个粒子的自旋z分量 $S_{1z}$ 和 $S_{2z}$ 都是确定的。

### 总自旋与[耦合表象](@entry_id:136812)

尽管非[耦合表象](@entry_id:136812)很直观，但在许多物理情境中，粒子间的相互作用取决于它们的**[总自旋](@entry_id:153335)**，而不是各自独立的自旋。[总自旋](@entry_id:153335)矢量算符定义为各[粒子自旋](@entry_id:142910)算符之和：
$$
\vec{S} = \vec{S}_1 + \vec{S}_2
$$
与角动量叠加的一般理论类似，描述系统的更方便的表象通常是总[自旋算符](@entry_id:155419) $\vec{S}^2$ 及其z分量 $S_z = S_{1z} + S_{2z}$ 的共同本征态。这组[基矢](@entry_id:199546)被称为**[耦合表象](@entry_id:136812)**，记作 $|S, m_S\rangle$，其中 $S$ 是总自旋[量子数](@entry_id:145558)，$m_S$ 是总[磁量子数](@entry_id:145584)。$\vec{S}^2$ 和 $S_z$ 的[本征值](@entry_id:154894)分别为 $S(S+1)\hbar^2$ 和 $m_S\hbar$。

对于两个自旋1/2粒子（$s_1 = 1/2, s_2 = 1/2$），总[自旋量子数](@entry_id:142550) $S$ 可以取的值为 $s_1+s_2 = 1$ 和 $|s_1-s_2| = 0$。

#### 三重态 (S=1)

当 $S=1$ 时，总磁量子数 $m_S$ 可以取 $-1, 0, 1$ 三个值。这三个态构成了**三重态**[流形](@entry_id:153038)。我们可以通过以下步骤构建它们：

1.  **最大 $m_S$ 态**：总磁量子数 $m_S$ 的最大值只能由各个粒子 $m_{s1}$ 和 $m_{s2}$ 的最大值相加得到，即 $m_S = m_{s1} + m_{s2} = 1/2 + 1/2 = 1$。这对应于[非耦合基](@entry_id:156676)矢中的 $|\uparrow\uparrow\rangle$。因此，这个态必定是[耦合表象](@entry_id:136812)中的 $|1, 1\rangle$ 态：
    $$
    |1, 1\rangle = |\uparrow\uparrow\rangle
    $$
    这个简单的等式具有深刻的物理意义。如果一次测量发现一个双自旋系统的[总自旋](@entry_id:153335)为 $S=1$ 且 $m_S=1$，那么系统必然塌缩到处在这个 $|1, 1\rangle$ 态。由于 $|1, 1\rangle$ 就是 $|\uparrow\uparrow\rangle$，这意味着两个粒子的自旋都必定是向上的。因此，紧接着对粒子1的 $S_{1z}$ 进行测量，将确定性地得到结果 $+\frac{\hbar}{2}$ [@problem_id:2080784]。

2.  **构造 $m_S=0$ 和 $m_S=-1$ 态**：我们可以利用总自旋**降算符** $S_- = S_{1-} + S_{2-}$ 从 $|1, 1\rangle$ 态生成三重态中的其他成员。降算符作用于耦合[基矢](@entry_id:199546)的规则是 $S_-|S, m_S\rangle = \hbar\sqrt{S(S+1) - m_S(m_S-1)}|S, m_S-1\rangle$。
    将 $S_-$ 作用于 $|1, 1\rangle$：
    $$
    S_-|1, 1\rangle = \hbar\sqrt{1(2) - 1(0)}|1, 0\rangle = \sqrt{2}\hbar|1, 0\rangle
    $$
    我们也可以在非[耦合表象](@entry_id:136812)中计算 $S_-$ 的作用，利用 $S_{i-}|\uparrow\rangle_i = \hbar|\downarrow\rangle_i$ 和 $S_{i-}|\downarrow\rangle_i = 0$：
    $$
    S_-|\uparrow\uparrow\rangle = (S_{1-} + S_{2-})|\uparrow\rangle_1|\uparrow\rangle_2 = \hbar(|\downarrow\rangle_1|\uparrow\rangle_2 + |\uparrow\rangle_1|\downarrow\rangle_2) = \hbar(|\downarrow\uparrow\rangle + |\uparrow\downarrow\rangle)
    $$
    比较上述两式，经过归一化后，我们得到 $|1, 0\rangle$ 态的表达式 [@problem_id:2080783]：
    $$
    |1, 0\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle + |\downarrow\uparrow\rangle)
    $$

3.  再次应用降算符于 $|1, 0\rangle$ 可以得到 $|1, -1\rangle$ 态：
    $$
    S_-|1, 0\rangle = \hbar\sqrt{1(2) - 0(-1)}|1, -1\rangle = \sqrt{2}\hbar|1, -1\rangle
    $$
    在非[耦合表象](@entry_id:136812)中：
    $$
    S_-\left(\frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle + |\downarrow\uparrow\rangle)\right) = \frac{\hbar}{\sqrt{2}}(|\downarrow\downarrow\rangle + |\downarrow\downarrow\rangle) = \sqrt{2}\hbar|\downarrow\downarrow\rangle
    $$
    因此，我们得到：
    $$
    |1, -1\rangle = |\downarrow\downarrow\rangle
    $$

#### 单态 (S=0)

当 $S=0$ 时，总磁量子数 $m_S$ 只能为0。这个 $|0, 0\rangle$ 态必须与所有[三重态](@entry_id:156705)正交，特别是与 $|1, 0\rangle$ 正交。在由 $|\uparrow\downarrow\rangle$ 和 $|\downarrow\uparrow\rangle$ 张成的 $m_S=0$ [子空间](@entry_id:150286)中，与对称组合 $|1, 0\rangle$ 正交的态必然是反对称组合：
$$
|0, 0\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle)
$$
这个态被称为**单态**。至此，我们构建了完整的耦合[基矢](@entry_id:199546)：
*   **[三重态](@entry_id:156705) (S=1)**:
    $$
    |1, 1\rangle = |\uparrow\uparrow\rangle
    $$
    $$
    |1, 0\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle + |\downarrow\uparrow\rangle)
    $$
    $$
    |1, -1\rangle = |\downarrow\downarrow\rangle
    $$
*   **单态 (S=0)**:
    $$
    |0, 0\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle)
    $$
这组态构成了描述两个自旋1/2[粒子系统](@entry_id:180557)的[耦合表象](@entry_id:136812)。

### 单态与三重态的物理性质

单态和[三重态](@entry_id:156705)不仅仅是数学上的构造，它们拥有截然不同的物理性质，这使得它们的区分在物理学中至关重要。

#### [交换对称性](@entry_id:151892)与[泡利不相容原理](@entry_id:141850)

考虑交换两个粒子的算符 $P_{12}$。当它作用于[基矢](@entry_id:199546)时，$P_{12}|\psi_1\rangle|\psi_2\rangle = |\psi_2\rangle|\psi_1\rangle$。我们可以检验它在耦合[基矢](@entry_id:199546)上的作用：
*   对于三重态：
    $P_{12}|1, 1\rangle = P_{12}|\uparrow\uparrow\rangle = |\uparrow\uparrow\rangle = +|1, 1\rangle$
    $P_{12}|1, 0\rangle = P_{12}\frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle + |\downarrow\uparrow\rangle) = \frac{1}{\sqrt{2}}(|\downarrow\uparrow\rangle + |\uparrow\downarrow\rangle) = +|1, 0\rangle$
    $P_{12}|1, -1\rangle = P_{12}|\downarrow\downarrow\rangle = |\downarrow\downarrow\rangle = +|1, -1\rangle$
    所有三重态在[粒子交换](@entry_id:154910)下都是**对称**的。

*   对于单态：
    $P_{12}|0, 0\rangle = P_{12}\frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle) = \frac{1}{\sqrt{2}}(|\downarrow\uparrow\rangle - |\uparrow\downarrow\rangle) = -|0, 0\rangle$
    单态在[粒子交换](@entry_id:154910)下是**反对称**的。

这个对称性对于**全同粒子**（如两个电子）系统具有决定性意义。根据**[泡利不相容原理](@entry_id:141850)**，两个全同[费米子](@entry_id:146235)（如电子）的总[波函数](@entry_id:147440)（包括空间部分和自旋部分）在交换两个粒子时必须是反对称的。
$$
\Psi_{\text{total}}(1, 2) = \Psi_{\text{space}}(\vec{r}_1, \vec{r}_2) \chi_{\text{spin}}(s_1, s_2)
$$
$$
P_{12}\Psi_{\text{total}} = (P_{12}\Psi_{\text{space}})(P_{12}\chi_{\text{spin}}) = -\Psi_{\text{total}}
$$
这意味着，如果空间[波函数](@entry_id:147440) $\Psi_{\text{space}}$ 是对称的，那么[自旋波函数](@entry_id:190161) $\chi_{\text{spin}}$ 必须是反对称的（即单态）。反之，如果空间[波函数](@entry_id:147440)是反对称的，[自旋波函数](@entry_id:190161)必须是对称的（即[三重态](@entry_id:156705)）。

一个典型的例子是：考虑两个被限制在[一维无限深势阱](@entry_id:271157)中的相同[费米子](@entry_id:146235)。如果它们的空间[波函数](@entry_id:147440)是对称的，例如两个粒子都处于同一个单粒子能级上，比如 $\Psi_{\text{space}}(x_1, x_2) = \psi_2(x_1)\psi_2(x_2)$，那么为了满足总[波函数](@entry_id:147440)的[反对称性](@entry_id:261893)，它们的自旋部分必须处于反对称的单态（$S=0$） [@problem_id:2080752]。这解释了为什么在原子和分子中，占据相同空间[轨道](@entry_id:137151)的两个电子的自旋总是相反的。

#### 纠缠与[非定域性](@entry_id:140165)

单态和三重态中的 $|1,0\rangle$ 态有一个根本的区别：它们无法被写成两个独立单粒子态的张量积。一个不能写成 $|\psi\rangle = |\chi\rangle_1 \otimes |\chi\rangle_2$ 形式的态被称为**量子纠缠态**。

一个可分离态（非纠缠态）的一般形式为：
$$
|\psi_{\text{sep}}\rangle = (a|\uparrow\rangle + b|\downarrow\rangle) \otimes (c|\uparrow\rangle + d|\downarrow\rangle) = ac|\uparrow\uparrow\rangle + ad|\uparrow\downarrow\rangle + bc|\downarrow\uparrow\rangle + bd|\downarrow\downarrow\rangle
$$
对于一个任意态 $|\psi\rangle = \alpha_{\uparrow\uparrow}|\uparrow\uparrow\rangle + \alpha_{\uparrow\downarrow}|\uparrow\downarrow\rangle + \alpha_{\downarrow\uparrow}|\downarrow\uparrow\rangle + \alpha_{\downarrow\downarrow}|\downarrow\downarrow\rangle$，它是可分离的当且仅当其系数满足 $\alpha_{\uparrow\uparrow}\alpha_{\downarrow\downarrow} - \alpha_{\uparrow\downarrow}\alpha_{\downarrow\uparrow} = 0$。

我们可以检验单态 $|0, 0\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle)$。其系数为 $\alpha_{\uparrow\uparrow}=0, \alpha_{\downarrow\downarrow}=0, \alpha_{\uparrow\downarrow}=1/\sqrt{2}, \alpha_{\downarrow\uparrow}=-1/\sqrt{2}$。
$$
\alpha_{\uparrow\uparrow}\alpha_{\downarrow\downarrow} - \alpha_{\uparrow\downarrow}\alpha_{\downarrow\uparrow} = (0)(0) - (\frac{1}{\sqrt{2}})(-\frac{1}{\sqrt{2}}) = \frac{1}{2} \neq 0
$$
因此，单态是纠缠态 [@problem_id:2080798]。类似地，可以证明 $|1,0\rangle$ 也是[纠缠态](@entry_id:152310)，而 $|1,1\rangle$ 和 $|1,-1\rangle$ 是可分离态。

纠缠的物理含义是，即使两个粒子在空间上相距甚远，对其中一个粒子的测量结果也会瞬间影响另一个粒子的状态。这种关联无法用经典物理来解释。单态在这方面表现得最为极致。一个关键性质是单态具有**[旋转不变性](@entry_id:137644)**，即它在任何基底下都保持相同的形式：
$$
|0, 0\rangle = \frac{1}{\sqrt{2}}(|\uparrow_n\downarrow_n\rangle - |\downarrow_n\uparrow_n\rangle)
$$
其中 $|\uparrow_n\rangle$ 和 $|\downarrow_n\rangle$ 是沿任意方向 $\hat{n}$ 的自旋本征态。这导致了完美的**反关联**。如果两个粒子处于单态，当一个观察者（Alice）测量粒子1沿任意轴 $\hat{n}$ 的自旋得到 $+\frac{\hbar}{2}$ 时，系统状态会塌缩，使得另一个观察者（Bob）测量粒子2沿同一轴 $\hat{n}$ 的自旋将确定性地得到 $-\frac{\hbar}{2}$ [@problem_id:2080787]。

与单态的标量性质不同，[三重态](@entry_id:156705)作为一个整体在旋转下表现为一个矢量。例如，一个两个自旋都指向x轴正方向的态 $|\rightarrow\rightarrow\rangle = \frac{1}{2}(|\uparrow\uparrow\rangle + |\uparrow\downarrow\rangle + |\downarrow\uparrow\rangle + |\downarrow\downarrow\rangle)$，可以被证明是三重态的一个线性叠加，不含任何单态分量 [@problem_id:2080764]：
$$
|\rightarrow\rightarrow\rangle = \frac{1}{2}|1, 1\rangle + \frac{1}{\sqrt{2}}|1, 0\rangle + \frac{1}{2}|1, -1\rangle
$$
这表明，虽然 $|\rightarrow\rightarrow\rangle$ 是一个乘积态，但它代表了一个总自旋为1的系统，只是其自旋指向x轴而非z轴。

### 物理系统中的应用

单态和[三重态](@entry_id:156705)的概念在描述真实物理系统时至关重要，特别是当存在自旋依赖的相互作用时。

#### [海森堡交换相互作用](@entry_id:156535)

两个相邻电子（例如在[磁性材料](@entry_id:137953)或双量子点中）之间的相互作用通常可以用**[海森堡哈密顿量](@entry_id:146333)**来描述：
$$
H = J \vec{S}_1 \cdot \vec{S}_2
$$
其中 $J$ 是[交换耦合](@entry_id:154848)常数。为了找到该[哈密顿量](@entry_id:172864)的[本征态](@entry_id:149904)和本征能量，我们可以利用一个关键的算符恒等式。从 $\vec{S}^2 = (\vec{S}_1 + \vec{S}_2)^2 = \vec{S}_1^2 + \vec{S}_2^2 + 2\vec{S}_1 \cdot \vec{S}_2$ 出发，可得：
$$
\vec{S}_1 \cdot \vec{S}_2 = \frac{1}{2}(\vec{S}^2 - \vec{S}_1^2 - \vec{S}_2^2)
$$
由于单态和[三重态](@entry_id:156705)是 $\vec{S}^2$, $\vec{S}_1^2$ 和 $\vec{S}_2^2$ 的共同本征态，它们也必然是[海森堡哈密顿量](@entry_id:146333)的本征态。
对于自旋1/2粒子，$\vec{S}_i^2$ 的[本征值](@entry_id:154894)为 $s(s+1)\hbar^2 = \frac{1}{2}(\frac{1}{2}+1)\hbar^2 = \frac{3}{4}\hbar^2$。

*   对于**单态** ($S=0$)：
    $\vec{S}^2$ 的[本征值](@entry_id:154894)为 $0(0+1)\hbar^2 = 0$。因此，$\vec{S}_1 \cdot \vec{S}_2$ 的[本征值](@entry_id:154894)为 $\frac{1}{2}(0 - \frac{3}{4}\hbar^2 - \frac{3}{4}\hbar^2) = -\frac{3}{4}\hbar^2$。
    单态能量为 $E_S = -\frac{3}{4}J\hbar^2$ [@problem_id:2080766]。

*   对于**[三重态](@entry_id:156705)** ($S=1$)：
    $\vec{S}^2$ 的[本征值](@entry_id:154894)为 $1(1+1)\hbar^2 = 2\hbar^2$。因此，$\vec{S}_1 \cdot \vec{S}_2$ 的[本征值](@entry_id:154894)为 $\frac{1}{2}(2\hbar^2 - \frac{3}{4}\hbar^2 - \frac{3}{4}\hbar^2) = +\frac{1}{4}\hbar^2$。
    三重态能量为 $E_T = +\frac{1}{4}J\hbar^2$。

海森堡相互作用导致单态和[三重态](@entry_id:156705)之间产生能量分裂 $\Delta E = E_T - E_S = J\hbar^2$。如果 $J>0$（反[铁磁耦合](@entry_id:153346)），系统[基态](@entry_id:150928)为单态；如果 $J<0$（[铁磁耦合](@entry_id:153346)），[基态](@entry_id:150928)为三重态。这是理解磁有序现象的基础。

#### 投影算符与量子测量

在实际操作中，我们可能需要将一个任意的双自旋态投影到单态或[三重态](@entry_id:156705)[子空间](@entry_id:150286)上。这可以通过构建**投影算符**来实现。利用 $\vec{S}_1 \cdot \vec{S}_2$ 算符在单态和[三重态](@entry_id:156705)[子空间](@entry_id:150286)上具有不同[本征值](@entry_id:154894)的特性，我们可以构建这样的投影算符。

例如，考虑算符 $P_T = \frac{3}{4}I + \frac{1}{\hbar^2}\vec{S}_1 \cdot \vec{S}_2$。让我们看看它作用在耦合[基矢](@entry_id:199546)上会发生什么：
*   作用于任意三重态 $|1, M\rangle$：
    $$
    P_T |1, M\rangle = \left(\frac{3}{4} + \frac{1}{\hbar^2}\left(\frac{1}{4}\hbar^2\right)\right)|1, M\rangle = ( \frac{3}{4} + \frac{1}{4} )|1, M\rangle = 1 \cdot |1, M\rangle
    $$
*   作用于单态 $|0, 0\rangle$：
    $$
    P_T |0, 0\rangle = \left(\frac{3}{4} + \frac{1}{\hbar^2}\left(-\frac{3}{4}\hbar^2\right)\right)|0, 0\rangle = ( \frac{3}{4} - \frac{3}{4} )|0, 0\rangle = 0 \cdot |0, 0\rangle
    $$
因此，$P_T$ 正是**[三重态](@entry_id:156705)[子空间](@entry_id:150286)的投影算符**。它会保留任意态中的三重态分量，并湮灭其单态分量 [@problem_id:2080755]。类似地，可以构建单态投影算符 $P_S = I - P_T = \frac{1}{4}I - \frac{1}{\hbar^2}\vec{S}_1 \cdot \vec{S}_2$。

这些[投影算符](@entry_id:154142)是分析和测量中的有力工具。根据[玻恩定则](@entry_id:154470)，如果系统处于态 $|\Psi\rangle$，测量其[总自旋](@entry_id:153335)得到单态（$S=0$）的概率为：
$$
P_{\text{singlet}} = \| P_S |\Psi\rangle \|^2 = \langle\Psi| P_S^\dagger P_S |\Psi\rangle = \langle\Psi| P_S |\Psi\rangle = |\langle 0,0 | \Psi \rangle|^2
$$
例如，对于一个给定的态 $|\Psi\rangle = \frac{1}{\sqrt{10}}(|\uparrow\uparrow\rangle + 2i|\uparrow\downarrow\rangle - 2i|\downarrow\uparrow\rangle + |\downarrow\downarrow\rangle)$，我们可以通过计算其与单态的[内积](@entry_id:158127)来求得测量到单态的概率。
$$
\langle 0,0 | \Psi \rangle = \left( \frac{1}{\sqrt{2}}(\langle\uparrow\downarrow| - \langle\downarrow\uparrow|) \right) \left( \frac{1}{\sqrt{10}}(|\uparrow\uparrow\rangle + 2i|\uparrow\downarrow\rangle - 2i|\downarrow\uparrow\rangle + |\downarrow\downarrow\rangle) \right) = \frac{1}{\sqrt{20}}(2i - (-2i)) = \frac{4i}{\sqrt{20}}
$$
概率为 $P_{\text{singlet}} = |\frac{4i}{\sqrt{20}}|^2 = \frac{16}{20} = \frac{4}{5}$ [@problem_id:2080785]。

### 进阶主题：纠缠的严格判据

虽然[行列式](@entry_id:142978)判据对[纯态](@entry_id:141688)很有效，但要处理更一般的情况（混合态）或寻求更形式化的证明，我们需要更强大的工具。**[部分转置](@entry_id:136776)判据**（[Peres-Horodecki判据](@entry_id:146053)）就是其中之一。

一个[量子态](@entry_id:146142)可以用[密度矩阵](@entry_id:139892) $\rho$ 来描述。对于一个纯态 $|\psi\rangle$，其[密度矩阵](@entry_id:139892)为 $\rho = |\psi\rangle\langle\psi|$。对于一个双体系统，我们可以对其中一个子系统（比如粒子B）执行[转置](@entry_id:142115)操作，这被称为**[部分转置](@entry_id:136776)**，记为 $\rho^{T_B}$。该判据指出：如果一个态是可分离的，那么其[部分转置](@entry_id:136776)后的密度矩阵 $\rho^{T_B}$ 必须是半正定的（即所有[本征值](@entry_id:154894)非负）。因此，如果 $\rho^{T_B}$ 存在负[本征值](@entry_id:154894)，那么该态必定是纠缠的。

让我们将此判据应用于单态 $|\psi^-\rangle = \frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle)$。其[密度矩阵](@entry_id:139892)为：
$$
\rho = |\psi^-\rangle\langle\psi^-| = \frac{1}{2}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle)(\langle\uparrow\downarrow| - \langle\downarrow\uparrow|) = \frac{1}{2}(|\uparrow\downarrow\rangle\langle\uparrow\downarrow| - |\uparrow\downarrow\rangle\langle\downarrow\uparrow| - |\downarrow\uparrow\rangle\langle\uparrow\downarrow| + |\downarrow\uparrow\rangle\langle\downarrow\uparrow|)
$$
在[基矢](@entry_id:199546) $\{|\uparrow\uparrow\rangle, |\uparrow\downarrow\rangle, |\downarrow\uparrow\rangle, |\downarrow\downarrow\rangle\}$ 下，其矩阵形式为：
$$
\rho = \frac{1}{2}\begin{pmatrix} 0  & 0 & 0 & 0 \\ 0 & 1 & -1 & 0 \\ 0 & -1 & 1 & 0 \\ 0 & 0 & 0 & 0 \end{pmatrix}
$$
执行对粒子B的[部分转置](@entry_id:136776)操作，我们得到 $\rho^{T_B}$。其矩阵形式为：
$$
\rho^{T_B} = \begin{pmatrix} 0  & 0 & 0 & -1/2 \\ 0 & 1/2 & 0 & 0 \\ 0 & 0 & 1/2 & 0 \\ -1/2 & 0 & 0 & 0 \end{pmatrix}
$$
计算该矩阵的[本征值](@entry_id:154894)，我们发现它们是 $\{\frac{1}{2}, \frac{1}{2}, \frac{1}{2}, -\frac{1}{2}\}$。由于出现了一个负[本征值](@entry_id:154894) $-\frac{1}{2}$，这严格证明了单态是纠缠的 [@problem_id:2080749]。这一方法为识别和[量化纠缠](@entry_id:144669)提供了坚实的数学基础，在[量子信息科学](@entry_id:150091)中具有核心地位。