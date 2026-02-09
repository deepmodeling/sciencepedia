## 引言
在现代光学成像，尤其是在半导体制造领域，精确预测和控制光的行为至关重要。随着光刻技术不断挑战物理极限，简单的相干或非相干成像模型已不足以描述亚波长尺寸下的复杂光学现象。部分相干成像理论，特别是霍普金斯（Hopkins）公式，为此提供了强大而精确的数学框架，成为理解和驾驭现代光学系统的关键。

本文旨在填补基础理论与前沿应用之间的知识鸿沟，系统性地阐明霍普金斯公式的内涵及其在解决实际工程问题中的核心作用。读者将通过本文的学习，循序渐进地掌握部分相干成像的精髓。在“原理与机制”章节，我们将从物理第一性原理出发，推导霍普金斯公式，并深入剖析其核心概念——传递交叉系数（TCC）。随后的“应用与跨学科联系”章节将展示该理论如何成为计算光刻中分辨率增强技术（如OPC和SMO）的基石，并探讨其在光学显微镜等领域的延伸。最后，“动手实践”部分将通过具体问题，帮助读者将理论知识转化为解决实际问题的能力。

本文的探索将从理解部分相干成像的物理基础和数学语言开始，为后续的深入学习奠定坚实的基础。

## 原理与机制

本章旨在深入探讨部分相干成像的物理原理与数学框架，重点介绍霍普金斯（Hopkins）公式。我们将从部分相干光场的基本统计描述出发，推导出在空域和频域中描述成像过程的核心方程，并详细阐述其关键组成部分，如传递交叉系数（TCC）。此外，我们还将讨论该模型的数值实现方法及其局限性，为后续章节中计算光刻技术的应用奠定坚实的理论基础。

### 相干性的统计描述：互强度与交叉光谱密度

为了精确描述部分相干成像，我们必须首先建立一个能够量化光场在空间和时间上相关性的数学语言。对于一个统计平稳的、准单色的标量光场 $E(\mathbf{r}, t)$，其核心统计特性由**互强度（mutual intensity）** $J(\mathbf{r}_1, \mathbf{r}_2)$ 捕获。互强度定义为场在两个不同空间点 $\mathbf{r}_1$ 和 $\mathbf{r}_2$ 处进行系综平均的互相关函数：

$$
J(\mathbf{r}_1, \mathbf{r}_2) = \langle E(\mathbf{r}_1, t) E^*(\mathbf{r}_2, t) \rangle
$$

其中，尖括号 $\langle \cdot \rangle$ 表示对场的所有可能实现进行系综平均。互强度是一个功能强大的工具，它将关于光场的两个关键信息编码在一个函数中 [@problem_id:4130947]。

-   **强度（Intensity）**：当两个空间点重合时，即 $\mathbf{r}_1 = \mathbf{r}_2 = \mathbf{r}$，互强度的对角线元素给出了该点的平均光强度（或辐照度）$I(\mathbf{r})$：
    $$
    I(\mathbf{r}) = J(\mathbf{r}, \mathbf{r}) = \langle |E(\mathbf{r}, t)|^2 \rangle
    $$
    由于强度是物理可观测量，它必须是一个非负实数。

-   **空间相干性（Spatial Coherence）**：互强度的非对角线元素 $J(\mathbf{r}_1, \mathbf{r}_2)$（其中 $\mathbf{r}_1 \neq \mathbf{r}_2$）量化了场在两个不同点之间的相关性。为了方便比较，通常将其归一化为**复相干度（complex degree of coherence）** $\mu(\mathbf{r}_1, \mathbf{r}_2)$：
    $$
    \mu(\mathbf{r}_1, \mathbf{r}_2) = \frac{J(\mathbf{r}_1, \mathbf{r}_2)}{\sqrt{J(\mathbf{r}_1, \mathbf{r}_1) J(\mathbf{r}_2, \mathbf{r}_2)}} = \frac{J(\mathbf{r}_1, \mathbf{r}_2)}{\sqrt{I(\mathbf{r}_1) I(\mathbf{r}_2)}}
    $$
    根据施瓦茨不等式，复相干度的模满足 $0 \le |\mu(\mathbf{r}_1, \mathbf{r}_2)| \le 1$。$|\mu|=1$ 表示完全相干，意味着两点之间的相位关系是确定的；$|\mu|=0$ 表示完全非相干，意味着两点的相位完全不相关；而 $0  |\mu|  1$ 则表示部分相干。

在更普遍的非准单色情况下，我们使用**交叉光谱密度（cross-spectral density）** $W(\mathbf{r}_1, \mathbf{r}_2, \omega)$，它与互相干函数 $\Gamma(\mathbf{r}_1, \mathbf{r}_2, \tau) = \langle E(\mathbf{r}_1, t+\tau) E^*(\mathbf{r}_2, t) \rangle$ 通过关于时间延迟 $\tau$ 和角频率 $\omega$ 的傅里叶变换对相关联 [@problem_id:4130947]：
$$
W(\mathbf{r}_1, \mathbf{r}_2, \omega) = \frac{1}{2\pi} \int_{-\infty}^{\infty} \Gamma(\mathbf{r}_1, \mathbf{r}_2, \tau) e^{i\omega\tau} d\tau
$$
对于准单色场，其光谱集中在中心频率 $\omega_0$ 附近，此时互强度 $J(\mathbf{r}_1, \mathbf{r}_2)$ 可以视为交叉光谱密度在频率上的积分。

### 空域中的部分相干成像

理解了如何描述照明场的相干性之后，我们现在可以构建一个通用的成像模型。考虑一个线性、空间不变的投影系统，其相干振幅脉冲响应为 $h(\mathbf{r})$。当一个具有复振幅透过率 $t(\boldsymbol{\rho})$ 的掩模被一个部分相干场 $E_0(\boldsymbol{\rho}, t)$ 照明时，紧随掩模之后的光场为 $E_m(\boldsymbol{\rho}, t) = t(\boldsymbol{\rho}) E_0(\boldsymbol{\rho}, t)$。

经过投影系统后，像平面的光场 $E_i(\mathbf{r}, t)$ 是掩模平面出射场与系统脉冲响应的卷积：
$$
E_i(\mathbf{r}, t) = \int E_m(\boldsymbol{\rho}, t) h(\mathbf{r} - \boldsymbol{\rho}) d\boldsymbol{\rho} = \int t(\boldsymbol{\rho}) E_0(\boldsymbol{\rho}, t) h(\mathbf{r} - \boldsymbol{\rho}) d\boldsymbol{\rho}
$$
像平面的平均强度 $I(\mathbf{r})$ 是 $\langle |E_i(\mathbf{r}, t)|^2 \rangle$。将上式代入并展开，我们得到：
$$
I(\mathbf{r}) = \left\langle \left( \int t(\boldsymbol{\rho}_1) E_0(\boldsymbol{\rho}_1, t) h(\mathbf{r} - \boldsymbol{\rho}_1) d\boldsymbol{\rho}_1 \right) \left( \int t^*(\boldsymbol{\rho}_2) E_0^*(\boldsymbol{\rho}_2, t) h^*(\mathbf{r} - \boldsymbol{\rho}_2) d\boldsymbol{\rho}_2 \right) \right\rangle
$$
将积分和系综平均的次序交换，并利用照明光互强度的定义 $J_0(\boldsymbol{\rho}_1, \boldsymbol{\rho}_2) = \langle E_0(\boldsymbol{\rho}_1, t) E_0^*(\boldsymbol{\rho}_2, t) \rangle$，我们得到部分相干成像的普遍空域积分形式：
$$
I(\mathbf{r}) = \iint J_0(\boldsymbol{\rho}_1, \boldsymbol{\rho}_2) t(\boldsymbol{\rho}_1) t^*(\boldsymbol{\rho}_2) h(\mathbf{r} - \boldsymbol{\rho}_1) h^*(\mathbf{r} - \boldsymbol{\rho}_2) d\boldsymbol{\rho}_1 d\boldsymbol{\rho}_2
$$
这个积分方程深刻地揭示了部分相干成像的物理本质 [@problem_id:4130932]。像强度 $I(\mathbf{r})$ 不是简单地由物强度 $|t(\boldsymbol{\rho})|^2$ 决定，而是由物面上所有点对 $(\boldsymbol{\rho}_1, \boldsymbol{\rho}_2)$ 产生的场之间的干涉贡献的总和。每一对点产生的干涉图样由项 $h(\mathbf{r} - \boldsymbol{\rho}_1) h^*(\mathbf{r} - \boldsymbol{\rho}_2)$ 描述，而该干涉的可见度（强度）则由照明光的互强度 $J_0(\boldsymbol{\rho}_1, \boldsymbol{\rho}_2)$ 进行加权。由于 $I(\mathbf{r})$ 依赖于乘积项 $t(\boldsymbol{\rho}_1) t^*(\boldsymbol{\rho}_2)$，我们称其为掩模复振幅 $t(\boldsymbol{\rho})$ 的**双线性（bilinear）**函数。

一个重要的特例是**非相干极限（incoherent limit）**。在这种情况下，照明光在掩模平面上任意两个不同点之间都是完全不相关的。数学上，这意味着互强度是一个狄拉克 $\delta$ 函数：$J_0(\boldsymbol{\rho}_1, \boldsymbol{\rho}_2) \propto \delta(\boldsymbol{\rho}_1 - \boldsymbol{\rho}_2)$。代入上式，积分消去了所有 $\boldsymbol{\rho}_1 \neq \boldsymbol{\rho}_2$ 的交叉项，只剩下对角线项：
$$
I(\mathbf{r}) \propto \int |t(\boldsymbol{\rho})|^2 |h(\mathbf{r} - \boldsymbol{\rho})|^2 d\boldsymbol{\rho}
$$
这表明，在非相干极限下，系统在强度上是线性的：像强度是物强度 $|t(\boldsymbol{\rho})|^2$ 与系统的强度点扩散函数 $|h(\mathbf{r})|^2$ 的卷积。双线性关系退化为对 $t(\boldsymbol{\rho})$ 的纯二次依赖（即仅依赖于 $|t(\boldsymbol{\rho})|^2$）[@problem_id:4130932]。

在通过一个薄掩模时，出射场的互强度 $J_m$ 与入射场的互强度 $J_0$ 之间的关系可以通过基本定义推导得出 [@problem_id:4130945]。
$$
J_m(\mathbf{r}_1, \mathbf{r}_2) = \langle E_m(\mathbf{r}_1) E_m^*(\mathbf{r}_2) \rangle = \langle [t(\mathbf{r}_1) E_0(\mathbf{r}_1)] [t(\mathbf{r}_2) E_0(\mathbf{r}_2)]^* \rangle
$$
由于掩模 $t(\mathbf{r})$ 是确定性的，它可以从系综平均中提出，得到：
$$
J_m(\mathbf{r}_1, \mathbf{r}_2) = t(\mathbf{r}_1) t^*(\mathbf{r}_2) J_0(\mathbf{r}_1, \mathbf{r}_2)
$$
这个简单的关系是构建整个霍普金斯公式的基础。

### 频域中的霍普金斯公式

虽然空域积分在物理解释上非常直观，但在计算和分析中，频域表述往往更为方便。通过对空域积分进行傅里叶变换，我们可以得到霍普金斯公式的频域形式。这个形式的核心是三个关键要素：掩模频谱、光源分布和投影系统光瞳函数。

#### 掩模频谱 $M(\mathbf{f})$

掩模的复振幅透过率 $t(\mathbf{r})$ 的傅里叶变换被称为**掩模频谱** $M(\mathbf{f})$：
$$
M(\mathbf{f}) = \int t(\mathbf{r}) e^{-i 2\pi \mathbf{f} \cdot \mathbf{r}} d\mathbf{r}
$$
$M(\mathbf{f})$ 描述了掩模如何将入射的平面波散射成一系列不同方向（由空间频率 $\mathbf{f}$ 表征）的衍射波。对于周期性掩模，其频谱由一系列位于特定频率 $f_n = n/p$（$p$ 为周期）的离散衍射级组成。

例如，一个周期为 $p$、占空比为 $D$ 的一维二元光栅，其频谱由傅里叶级数系数决定。其零阶（DC分量）系数为 $a_0 = D$，高阶系数为 $a_n = \frac{\sin(\pi n D)}{\pi n}$ (对于 $n \neq 0$) [@problem_id:4130993]。

先进的掩模技术，如**交替相移掩模（alternating phase-shift mask, Alt-PSM）**，通过在相邻的透光区域引入 $\pi$ 的相位差来操纵频谱。对于一个由宽度为 $Dp$ 的透光条纹构成的 Alt-PSM，其有效周期变为 $2p$。一个显著的后果是，所有偶数阶衍射级（包括关键的零阶）都被抑制，即它们的系数为零。这使得一阶衍射级的对比度显著增强，从而提高了成像分辨率 [@problem_id:4130993]。

#### 光源分布 $S(\mathbf{f}_s)$ 和光瞳函数 $P(\mathbf{f})$

在霍普金斯模型中，扩展的、非相干的光源被建模为一系列独立的点源的集合。每个点源发出一个平面波，其传播方向由空间频率坐标 $\mathbf{f}_s$ 参数化。**光源分布** $S(\mathbf{f}_s)$ 是一个实的、非负的函数，描述了光源在不同方向上的强度分布，通常归一化为 $\int S(\mathbf{f}_s) d\mathbf{f}_s = 1$ [@problem_id:4130951]。光源的角区大小由**照明数值孔径** $\mathrm{NA}_{\mathrm{ill}}$ 定义，它决定了 $S(\mathbf{f}_s)$ 的支持域，即 $| \mathbf{f}_s | \le \mathrm{NA}_{\mathrm{ill}} / \lambda$。

**光瞳函数** $P(\mathbf{f})$ 描述了投影系统的透镜如何在其傅里叶平面（即光瞳平面）上过滤物体的频谱。它是一个复函数：
$$
P(\mathbf{f}) = A(\mathbf{f}) \exp\left( i \frac{2\pi}{\lambda} W(\mathbf{f}) \right)
$$
其中：
-   $A(\mathbf{f})$ 是振幅项，取值在 $[0, 1]$ 之间。它包括了由投影物镜**数值孔径** $\mathrm{NA}_{\mathrm{obj}}$ 定义的硬截断（即在截止频率 $| \mathbf{f} | > \mathrm{NA}_{\mathrm{obj}} / \lambda$ 之外 $A(\mathbf{f})=0$）以及任何额外的切趾（apodization）。
-   $W(\mathbf{f})$ 是光学系统中的**波阵面像差**，以光程差（Optical Path Difference, OPD）的形式给出。指数项将此光程差转换为相应的相位延迟 [@problem_id:4130951]。

部分相干性由**相干因子（coherence parameter）** $\sigma$ 来量化，它被定义为照明数值孔径与物镜数值孔径之比 [@problem_id:4130949]：
$$
\sigma = \frac{\mathrm{NA}_{\mathrm{ill}}}{\mathrm{NA}_{\mathrm{obj}}}
$$
在归一化的频率空间中（其中物镜光瞳的半径为 1），$\sigma$ 就是光源盘的半径。$\sigma \to 0$ 对应于相干成像（单点光源），而较大的 $\sigma$ 值表示照明角度范围更广，空间相干性更低。

### 传递交叉系数 (TCC)

将以上所有元素结合起来，像平面强度 $I(\mathbf{r})$ 可以表示为关于掩模频谱 $M(\mathbf{f})$ 的双线性形式：
$$
I(\mathbf{r}) = \iint M(\mathbf{f}_1) M^*(\mathbf{f}_2) TCC(\mathbf{f}_1, \mathbf{f}_2) e^{i 2\pi (\mathbf{f}_1 - \mathbf{f}_2) \cdot \mathbf{r}} d\mathbf{f}_1 d\mathbf{f}_2
$$
这个公式是霍普金斯成像理论的核心。其中的核函数 $TCC(\mathbf{f}_1, \mathbf{f}_2)$ 被称为**传递交叉系数（Transmission Cross-Coefficient）**。TCC 完全由光学系统本身决定，独立于掩模。其定义为 [@problem_id:4150407]：
$$
TCC(\mathbf{f}_1, \mathbf{f}_2) = \int S(\mathbf{f}_s) P(\mathbf{f}_s + \mathbf{f}_1) P^*(\mathbf{f}_s + \mathbf{f}_2) d\mathbf{f}_s
$$
TCC 的物理解释是，它量化了系统传递一对衍射级（来自掩模的频率分量 $\mathbf{f}_1$ 和 $\mathbf{f}_2$）并允许它们在像平面上产生干涉的能力 [@problem_id:4130946]。积分表示对所有光源点产生的贡献进行非相干叠加。对于给定的光源点 $\mathbf{f}_s$，只有当两个被平移的频率分量 $\mathbf{f}_s + \mathbf{f}_1$ 和 $\mathbf{f}_s + \mathbf{f}_2$ 都落在光瞳函数 $P$ 的通带内时，它们才能同时通过系统并发生干涉。TCC 正是这种重叠区域在整个光源上的积分。

对角线项 $TCC(\mathbf{f}, \mathbf{f})$ 描述了单个频率分量 $\mathbf{f}$ 对像强度贡献的传递效率，而非对角线项 $TCC(\mathbf{f}_1, \mathbf{f}_2)$ 则描述了不同频率分量之间的交叉耦合或干涉。正是这些非对角线项的存在，使得部分相干成像能够保留物体的相位信息，并产生比非相干成像更丰富的图像结构。

让我们通过一个具体的例子来理解 TCC 的作用 [@problem_id:4150407]。考虑一个理想的 Alt-PSM，其频谱仅包含两个点：$M(k_0) = 1$ 和 $M(-k_0) = e^{i\pi} = -1$。照明光源为两个对称的点源，位于 $\pm \alpha_0$。假设所有相关的衍射级都能够通过光瞳。在这种情况下，TCC 矩阵的所有四个元素 $T(k_0, k_0)$、 $T(k_0, -k_0)$、 $T(-k_0, k_0)$ 和 $T(-k_0, -k_0)$ 经过计算都等于 1。像中心 $x=0$ 处的强度为：
$$
I(0) = \sum_{k_i, k_j \in \{k_0, -k_0\}} M(k_i) M^*(k_j) T(k_i, k_j)
$$
$$
I(0) = M(k_0)M^*(k_0)T(k_0,k_0) + M(k_0)M^*(-k_0)T(k_0,-k_0) + M(-k_0)M^*(k_0)T(-k_0,k_0) + M(-k_0)M^*(-k_0)T(-k_0,-k_0)
$$
代入数值：
$$
I(0) = (1)(1)(1) + (1)(-1)(1) + (-1)(1)(1) + (-1)(-1)(1) = 1 - 1 - 1 + 1 = 0
$$
结果为零，这表明在像中心发生了完美的相消干涉。这正是 Alt-PSM 技术能够产生极高对比度暗线的核心机制。这个例子清晰地展示了霍普金斯双线性形式如何通过 TCC 编码不同衍射级之间的干涉效应。

### TCC的本征模态分解

在计算光刻中，直接计算双重积分的霍普金斯公式计算量巨大。一个高效的替代方法是利用 TCC 的数学特性进行模态分解。TCC 作为积分算子的核，具有两个关键性质 [@problem_id:4130970]：
1.  **厄米性（Hermitian）**: $TCC(\mathbf{f}_1, \mathbf{f}_2) = TCC^*(\mathbf{f}_2, \mathbf{f}_1)$。这源于其物理定义。
2.  **正半定性（Positive Semidefinite）**: 对于任何掩模频谱 $M(\mathbf{f})$，产生的总强度必须非负，这意味着 TCC 定义的积分算子是正半定的。

对于一个在紧凑支持域上连续的、厄米的、正半定的核，**默瑟定理（Mercer's Theorem）**保证它可以展开为一系列其本征函数 $\phi_n(\mathbf{f})$ 和非负本征值 $\lambda_n$ 的和：
$$
TCC(\mathbf{f}_1, \mathbf{f}_2) = \sum_{n=1}^{\infty} \lambda_n \phi_n(\mathbf{f}_1) \phi_n^*(\mathbf{f}_2)
$$
这个级数在支持域上绝对且一致收敛。即使 TCC 仅满足更弱的平方可积条件（希尔伯特-施密特核），该展开在 $L^2$ 范数下仍然收敛 [@problem_id:4130970]。

将此展开代入霍普金斯公式，像强度可以表示为：
$$
I(\mathbf{r}) = \sum_{n=1}^{\infty} \lambda_n \left| \int M(\mathbf{f}) \phi_n^*(\mathbf{f}) e^{i 2\pi \mathbf{f} \cdot \mathbf{r}} d\mathbf{f} \right|^2
$$
这个表达式具有深刻的物理意义：一个部分相干成像系统可以被精确地分解为一个非相干的、加权的独立**相干系统**的集合。每个相干系统（或称“相干模态”）由其本征函数 $\phi_n(\mathbf{f})$ 定义，可以看作是一个等效的相干光瞳。本征值 $\lambda_n$ 代表了每个相干模态在总图像强度中的“能量”或权重。

在实践中，这些本征值 $\lambda_n$ 会迅速衰减。这意味着我们只需保留前几个（例如，几十个）最大的本征值及其对应的本征函数，就可以非常精确地近似原始的部分相干系统。这种**截断**极大地降低了计算复杂度，是所有现代光刻仿真软件的核心算法。

### 标量理论的局限性与矢量扩展

霍普金斯标量理论是一个非常成功的模型，但它建立在场的行为可以用单个标量函数描述的假设之上。当光刻系统的数值孔径 $\mathrm{NA}$ 变得非常大（例如接近或超过1）时，这个假设便不再成立 [@problem_id:4130986]。主要有两个原因：

1.  **矢量衍射效应**：在高 NA 系统中，汇聚到像平面的光线夹角很大，远超近轴近似的范围。电磁场的矢量性质变得至关重要，例如，会出现显著的纵向电场分量（$E_z$），且不同偏振分量之间的相互作用无法忽略。

2.  **偏振相关效应**：掩模的三维结构和晶圆上的多层薄膜堆栈对不同偏振态的光（例如，TE 偏振和 TM 偏振）会产生不同的衍射、反射和透射响应。

为了准确建模这些效应，必须将霍普金斯公式**矢量化（vectorized）**。在这种扩展模型中：
-   电场被表示为一个二维横向矢量 $\mathbf{E} = [E_x, E_y]^T$。
-   场的相干性由一个 $2 \times 2$ 的互强度矩阵 $\mathbf{J}(\mathbf{r}_1, \mathbf{r}_2)$ 描述。
-   标量 TCC 被一个 $4 \times 4$ 的**矢量 TCC 矩阵**所取代。这个 $4 \times 4$ 的算子作用于一个由四个掩模频谱乘积项（如 $M_x(\mathbf{f}_1)M_x^*(\mathbf{f}_2)$, $M_x(\mathbf{f}_1)M_y^*(\mathbf{f}_2)$ 等）构成的矢量，从而计算出像平面上 $2 \times 2$ 相干矩阵的所有四个分量 [@problem_id:4130986]。

这个矢量模型能够捕捉到偏振混合、TE/TM 不对称性以及其他在高 NA 成像中至关重要的物理现象，是当前最先进的计算光刻技术不可或缺的一部分。