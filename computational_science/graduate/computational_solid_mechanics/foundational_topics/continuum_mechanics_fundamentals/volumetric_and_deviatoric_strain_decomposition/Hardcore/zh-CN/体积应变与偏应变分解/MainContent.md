## 引言
在分析材料如何响应外力时，一个根本问题是：变形是改变了物体的体积，还是仅仅改变了其形状？在连续介质力学中，体积-偏[应变分解](@entry_id:186005)正是回答这一问题的核心工具。它将复杂的变形过程清晰地拆分为纯体积变化（膨胀或压缩）和纯形状变化（畸变），为理解和预测材料行为提供了深刻的物理洞察。

尽管这一概念在理论上很优雅，但在实际应用中，从线性小应变到[非线性](@entry_id:637147)[大变形](@entry_id:167243)，其数学表达和物理内涵会发生显著变化。工程师和研究人员常常面临的挑战是，如何将这一抽象分解有效地应用于构建精确的材料[本构模型](@entry_id:174726)，以及如何解决其在有限元数值模拟中引发的“体积自锁”等棘手问题。

本文旨在系统性地梳理体积-偏[应变分解](@entry_id:186005)的完整图景。在“原理与机制”一章中，我们将深入探讨其在线性与[有限应变理论](@entry_id:176941)中的数学基础和物理意义。随后的“应用与[交叉](@entry_id:147634)学科联系”一章将展示该理论如何在[计算力学](@entry_id:174464)、[材料科学](@entry_id:152226)、地球物理学等领域解决实际工程问题。最后，“动手实践”部分将提供具体的计算练习，帮助读者将理论知识转化为实践技能。

让我们首先从最基础的原理出发，在“原理与机制”一章中探索变形分解在力学世界中的精妙之处。

## 原理与机制

在连续介质力学中，将一个物体的变形分解为体积改变和形状改变两部分，是一种极为深刻且实用的方法。这种分解不仅为我们提供了直观的物理图像，更在材料本构模型的构建和数值计算的稳定性方面扮演着至关重要的角色。本章将系统阐述[应变张量](@entry_id:193332)的体积-偏[应变分解](@entry_id:186005)在小应变和[有限应变理论](@entry_id:176941)中的基本原理、物理意义及其在[计算固体力学](@entry_id:169583)中的应用。

### 小应变理论中的分解

在线性化的框架下，即小应变理论中，应变的分解表现为一种直接的加法形式，清晰地揭示了变形的两种[基本模式](@entry_id:165201)。

#### [运动学分解](@entry_id:751020)与物理意义

对于一个小变形过程，物体的应变状态由对称的[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon}$ 描述。任何一个二阶张量，包括 $\boldsymbol{\varepsilon}$，都可以唯一地分解为一个球量[部分和](@entry_id:162077)一个偏量部分。这构成了应变的 **加法分解** (additive decomposition)：

$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{\text{vol}} + \boldsymbol{\varepsilon}^{\text{dev}}
$$

其中，$\boldsymbol{\varepsilon}^{\text{vol}}$ 是 **[体积应变](@entry_id:267252)张量** (volumetric strain tensor)，$\boldsymbol{\varepsilon}^{\text{dev}}$ 是 **偏应变张量** (deviatoric strain tensor)。

**[体积应变](@entry_id:267252)** 代表了纯粹的体积变化，不涉及形状的改变。它被定义为[应变张量](@entry_id:193332)的球量部分，与单位张量 $\boldsymbol{I}$ 成正比：

$$
\boldsymbol{\varepsilon}^{\text{vol}} = \frac{1}{3}\operatorname{tr}(\boldsymbol{\varepsilon})\boldsymbol{I}
$$

这里的标量 $\operatorname{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{kk}$ 是应变张量的迹，它本身具有明确的物理意义。在小应变假设下，$\operatorname{tr}(\boldsymbol{\varepsilon})$ 近似等于单位体积的相对变化量 $\frac{\Delta V}{V}$。这是因为对于一个变形梯度为 $\boldsymbol{F} = \boldsymbol{I} + \nabla\boldsymbol{u}$ 的变形，其体积比 $J = \det(\boldsymbol{F})$ 在小梯度下可以线性化为 $J \approx 1 + \operatorname{tr}(\nabla\boldsymbol{u})$。由于 $\operatorname{tr}(\boldsymbol{\varepsilon}) = \operatorname{tr}(\nabla\boldsymbol{u})$，我们得到 $\frac{\Delta V}{V} = J - 1 \approx \operatorname{tr}(\boldsymbol{\varepsilon})$ 。因此，应变张量的迹直接量化了材料的膨胀或压缩程度。

**[偏应变](@entry_id:201263)** 则描述了在保持体积不变的情况下发生的形状改变（即畸变）。它被定义为从总应变中减去[体积应变](@entry_id:267252)部分：

$$
\boldsymbol{\varepsilon}^{\text{dev}} = \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{\text{vol}} = \boldsymbol{\varepsilon} - \frac{1}{3}\operatorname{tr}(\boldsymbol{\varepsilon})\boldsymbol{I}
$$

偏[应变张量](@entry_id:193332)的一个根本性质是其迹恒为零，即 $\operatorname{tr}(\boldsymbol{\varepsilon}^{\text{dev}}) = 0$。这数学上保证了它所代表的变形是 **等容的** (isochoric)，即不引起体积变化 。一个非零的偏应变张量意味着材料单元被拉伸、压缩或剪切，从而改变了其形状，但其总[体积保持](@entry_id:141001)不变。值得注意的是，一个[等容变形](@entry_id:196451) ($\operatorname{tr}(\boldsymbol{\varepsilon})=0$) 并不意味着没有应变，而是指该应变纯粹是形状的改变，例如纯剪切，这与无应变的[刚体运动](@entry_id:193355)有本质区别 。

为了具体说明这一分解过程，我们考虑一个给定的[无穷小应变张量](@entry_id:167211) ：
$$
\boldsymbol{\varepsilon} = \begin{pmatrix}
\frac{1}{60}  \frac{1}{30}  -\frac{1}{20} \\
\frac{1}{30}  -\frac{1}{12}  \frac{1}{15} \\
-\frac{1}{20}  \frac{1}{15}  \frac{1}{10}
\end{pmatrix}
$$
首先，计算其迹：
$$
\operatorname{tr}(\boldsymbol{\varepsilon}) = \frac{1}{60} - \frac{1}{12} + \frac{1}{10} = \frac{1 - 5 + 6}{60} = \frac{2}{60} = \frac{1}{30}
$$
这代表了一个微小的[体积膨胀](@entry_id:144241)。随后，我们可以构建[体积应变](@entry_id:267252)张量：
$$
\boldsymbol{\varepsilon}^{\text{vol}} = \frac{1}{3}\left(\frac{1}{30}\right)\boldsymbol{I} = \frac{1}{90}\boldsymbol{I} = \begin{pmatrix} \frac{1}{90}  0  0 \\ 0  \frac{1}{90}  0 \\ 0  0  \frac{1}{90} \end{pmatrix}
$$
最后，通过相减得到偏[应变张量](@entry_id:193332)：
$$
\boldsymbol{\varepsilon}^{\text{dev}} = \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{\text{vol}} = \begin{pmatrix}
\frac{1}{180}  \frac{1}{30}  -\frac{1}{20} \\
\frac{1}{30}  -\frac{17}{180}  \frac{1}{15} \\
-\frac{1}{20}  \frac{1}{15}  \frac{16}{180}
\end{pmatrix}
$$
通过直接计算可以验证 $\operatorname{tr}(\boldsymbol{\varepsilon}^{\text{dev}}) = \frac{1}{180} - \frac{17}{180} + \frac{16}{180} = 0$，证实了其描述的是纯形状改变。

在塑性力学中，偏[应变张量](@entry_id:193332)的大小对于描述[材料屈服](@entry_id:751736)至关重要。其大小通常通过 **第二偏应[不变量](@entry_id:148850)** $J_{2}$ 来衡量：
$$
J_{2} = \frac{1}{2}\boldsymbol{\varepsilon}^{\text{dev}} : \boldsymbol{\varepsilon}^{\text{dev}} = \frac{1}{2} \sum_{i,j} (\varepsilon_{ij}^{\text{dev}})^2
$$
$J_{2}$ 量化了畸变的大小，是许多[屈服准则](@entry_id:193897)（如 von Mises 准则）的核心组成部分 。

#### 本构关系的解耦

应变的体积-偏[应变分解](@entry_id:186005)之所以在物理上如此重要，是因为对于[各向同性材料](@entry_id:170678)，其对体积变化和形状变化的抵抗能力是相互独立的。这在材料的本构关系中得到了精确的体现。

考虑一个[各向同性线弹性](@entry_id:185899)材料，其[应变能密度函数](@entry_id:755490) $\psi$ 是应变张量 $\boldsymbol{\varepsilon}$ 的二次标量函数。通常用拉梅参数 $\lambda$ 和 $\mu$ 表示为：
$$
\psi(\boldsymbol{\varepsilon}) = \frac{\lambda}{2}(\operatorname{tr}\boldsymbol{\varepsilon})^{2} + \mu\,\boldsymbol{\varepsilon}:\boldsymbol{\varepsilon}
$$
通过引入体积-偏[应变分解](@entry_id:186005) $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{\text{dev}} + \frac{1}{3}(\operatorname{tr}\boldsymbol{\varepsilon})\boldsymbol{I}$，并利用偏应变张量的无迹性（即 $\boldsymbol{\varepsilon}^{\text{dev}}:\boldsymbol{I} = 0$），我们可以将上式重新表达为一种[解耦](@entry_id:637294)的形式 。关键步骤是展开 $\boldsymbol{\varepsilon}:\boldsymbol{\varepsilon}$ 项：
$$
\boldsymbol{\varepsilon}:\boldsymbol{\varepsilon} = \left(\boldsymbol{\varepsilon}^{\text{dev}} + \frac{1}{3}(\operatorname{tr}\boldsymbol{\varepsilon})\boldsymbol{I}\right):\left(\boldsymbol{\varepsilon}^{\text{dev}} + \frac{1}{3}(\operatorname{tr}\boldsymbol{\varepsilon})\boldsymbol{I}\right) = \boldsymbol{\varepsilon}^{\text{dev}}:\boldsymbol{\varepsilon}^{\text{dev}} + \frac{1}{3}(\operatorname{tr}\boldsymbol{\varepsilon})^2
$$
将此结果代回 $\psi$ 的表达式并整理，得到：
$$
\psi(\boldsymbol{\varepsilon}) = \frac{1}{2}\left(\lambda + \frac{2}{3}\mu\right)(\operatorname{tr}\boldsymbol{\varepsilon})^{2} + \mu\,\boldsymbol{\varepsilon}^{\text{dev}}:\boldsymbol{\varepsilon}^{\text{dev}}
$$
这个形式非常优雅。如果我们定义 **[体积模量](@entry_id:160069)** (bulk modulus) $K = \lambda + \frac{2}{3}\mu$ 和 **剪切模量** (shear modulus) $G = \mu$，则[应变能密度函数](@entry_id:755490)可以写为：
$$
\psi(\boldsymbol{\varepsilon}) = \frac{1}{2}K(\operatorname{tr}\boldsymbol{\varepsilon})^{2} + G\,\boldsymbol{\varepsilon}^{\text{dev}}:\boldsymbol{\varepsilon}^{\text{dev}}
$$
这个[解耦](@entry_id:637294)的能量表达式  清楚地表明：总应变能是体积变化应变能（由 $K$ 和体积应变 $\operatorname{tr}\boldsymbol{\varepsilon}$ 决定）和形状变化应变能（由 $G$ 和[偏应变](@entry_id:201263) $\boldsymbol{\varepsilon}^{\text{dev}}$ 决定）的简单加和。$K$ 量化了材料抵抗均匀压缩或膨胀的能力，而 $G$ 量化了材料抵抗剪切或形状畸变的能力。

通过对[应变能密度](@entry_id:200085)求导 $\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}$，我们可以得到同样[解耦](@entry_id:637294)的[应力-应变关系](@entry_id:274093)：
$$
\boldsymbol{\sigma} = K\operatorname{tr}(\boldsymbol{\varepsilon})\boldsymbol{I} + 2G\boldsymbol{\varepsilon}^{\text{dev}}
$$
这表明，应力张量 $\boldsymbol{\sigma}$ 也可分解为一个球应力部分（静水压力 $p = K\operatorname{tr}(\boldsymbol{\varepsilon})$）和一个[偏应力](@entry_id:163323)部分（$\boldsymbol{s} = 2G\boldsymbol{\varepsilon}^{\text{dev}}$）。

这种分解框架使得分析材料在极端条件下的行为变得异常清晰 ：
*   **不可压缩极限 ($K \to \infty$)**：为了保持有限的应变能，[体积应变](@entry_id:267252)必须趋于零，即 $\operatorname{tr}(\boldsymbol{\varepsilon}) \to 0$。这在运动学上施加了一个不可压缩的约束。此时，[静水压力](@entry_id:275365) $p$ 不再由[体积应变](@entry_id:267252)决定，而是成为一个用以维持该约束的待定[拉格朗日乘子](@entry_id:142696)。在[有限元分析](@entry_id:138109)中，对于[近不可压缩材料](@entry_id:752388)，纯位移格式的单元会因此产生“[体积锁定](@entry_id:172606)”（Volumetric Locking）现象，导致错误的数值结果。
*   **理想流体极限 ($G \to 0$)**：当剪切模量为零时，材料失去抵抗任何形状改变的能力。偏应力部分消失，应力张量变为纯球量 $\boldsymbol{\sigma} = K\operatorname{tr}(\boldsymbol{\varepsilon})\boldsymbol{I}$。这正是理想（无粘性）流体的本构特征。

### [有限应变理论](@entry_id:176941)中的分解

当变形不再微小时，旋转与拉伸耦合在一起，简单的加法分解不再适用。我们需要一种更深刻的分解方法，它必须满足 **客观性** (objectivity) 或称 **标架无关性** (frame-indifference) 的原理，即材料的本构响应不应依赖于观察者的刚体运动。

#### 客观性与[乘法分解](@entry_id:199514)

一个客观的[应变度量](@entry_id:755495)必须独立于叠加在变形上的刚体旋转。变形梯度 $\boldsymbol{F}$ 本身不是客观的，因为它包含了旋转信息。考虑一个叠加的刚体旋转 $\boldsymbol{Q}$，新的变形梯度为 $\boldsymbol{F}^* = \boldsymbol{Q}\boldsymbol{F}$。为了构建客观的[应变度量](@entry_id:755495)，我们必须首先从 $\boldsymbol{F}$ 中“剥离”出纯拉伸部分。

这可以通过 **极分解** (polar decomposition) $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$ 来实现，其中 $\boldsymbol{R}$ 是[旋转张量](@entry_id:191990)，$\boldsymbol{U}$ 是[对称正定](@entry_id:145886)的 **右[拉伸张量](@entry_id:193200)**。在叠加旋转 $\boldsymbol{Q}$ 后，新的右[拉伸张量](@entry_id:193200) $\boldsymbol{U}^*$ 仍等于 $\boldsymbol{U}$，这表明 $\boldsymbol{U}$ 是客观的 。因此，所有有效的[有限应变度量](@entry_id:185716)都必须是 $\boldsymbol{U}$ 或与其等价的 **[右柯西-格林张量](@entry_id:174156)** $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = \boldsymbol{U}^2$ 的函数 。

基于这一思想，有限变形的体积-偏[应变分解](@entry_id:186005)建立在变形梯度的 **[乘法分解](@entry_id:199514)** (multiplicative decomposition) 之上 ：

$$
\boldsymbol{F} = J^{1/3}\bar{\boldsymbol{F}}
$$

这里，$J = \det(\boldsymbol{F})$ 是体积比，代表了纯体积变化。$J^{1/3}$ 是一个在三维空间中各向同性的尺度因子。$\bar{\boldsymbol{F}}$ 是 **[等容变形](@entry_id:196451)梯度**，其[行列式](@entry_id:142978) $\det(\bar{\boldsymbol{F}})=1$，代表了纯形状改变。

这个[乘法分解](@entry_id:199514)可以传递到柯西-格林张量上 ：
$$
\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = (J^{1/3}\bar{\boldsymbol{F}})^{\mathsf{T}}(J^{1/3}\bar{\boldsymbol{F}}) = J^{2/3}\bar{\boldsymbol{F}}^{\mathsf{T}}\bar{\boldsymbol{F}} = J^{2/3}\bar{\boldsymbol{C}}
$$
其中 $\bar{\boldsymbol{C}} = \bar{\boldsymbol{F}}^{\mathsf{T}}\bar{\boldsymbol{F}}$ 是等容[右柯西-格林张量](@entry_id:174156)，其[行列式](@entry_id:142978) $\det(\bar{\boldsymbol{C}}) = (\det\bar{\boldsymbol{F}})^2 = 1$。

#### [对数应变](@entry_id:751438)及其加法分解

虽然变形的分解在运动学上是乘法形式的，但有一种特殊的[应变度量](@entry_id:755495)——**[亨基应变](@entry_id:191329)** (Hencky strain) 或 **[对数应变](@entry_id:751438)** (logarithmic strain)，它能够将这种乘法关系转化为优雅的加法关系。[亨基应变](@entry_id:191329)定义为右[拉伸张量](@entry_id:193200)的[矩阵对数](@entry_id:169041)：

$$
\boldsymbol{h} = \ln \boldsymbol{U}
$$

[亨基应变](@entry_id:191329)的一个优美特性是其迹与体积比的对数直接相关 ：
$$
\operatorname{tr}(\boldsymbol{h}) = \operatorname{tr}(\ln \boldsymbol{U}) = \ln(\det \boldsymbol{U}) = \ln J
$$
这完美地推广了小应变理论中的 $\operatorname{tr}(\boldsymbol{\varepsilon}) \approx \ln(1+\operatorname{tr}(\boldsymbol{\varepsilon})) \approx \ln J$ 的关系。

正因为如此，对[亨基应变](@entry_id:191329)张量 $\boldsymbol{h}$ 进行标准的加法分解，可以得到与运动学[乘法分解](@entry_id:199514)精确对应的体积和[偏应变](@entry_id:201263)部分：
$$
\boldsymbol{h} = \boldsymbol{h}^{\text{vol}} + \boldsymbol{h}^{\text{dev}}
$$
其中，体积部分为：
$$
\boldsymbol{h}^{\text{vol}} = \frac{1}{3}\operatorname{tr}(\boldsymbol{h})\boldsymbol{I} = \frac{1}{3}\ln(J)\boldsymbol{I}
$$
[偏应变](@entry_id:201263)部分为：
$$
\boldsymbol{h}^{\text{dev}} = \boldsymbol{h} - \boldsymbol{h}^{\text{vol}} = \ln(\boldsymbol{U}) - \frac{1}{3}\ln(J)\boldsymbol{I} = \ln(J^{-1/3}\boldsymbol{U})
$$
最后一个等式  揭示了核心联系：[亨基应变](@entry_id:191329)的偏量部分正是等容[拉伸张量](@entry_id:193200) $\bar{\boldsymbol{U}} = J^{-1/3}\boldsymbol{U}$ 的对数。因此，[亨基应变](@entry_id:191329)能够在线性代数的意义上干净地将体积变化和形状变化分离开来。其[偏应变](@entry_id:201263)部分 $\boldsymbol{h}^{\text{dev}}$ 是无迹的，并且其[矩阵指数的行列式](@entry_id:185417)为1，即 $\det(\exp(\boldsymbol{h}^{\text{dev}}))=1$，表明它代表了一个纯等容的变形 。

相比之下，其他[有限应变度量](@entry_id:185716)，如 **[格林-拉格朗日应变](@entry_id:170427)** $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})$，其标准的加法分解 $\operatorname{dev}\boldsymbol{E}$ 并不能完全对应于[等容变形](@entry_id:196451)产生的应变 $\bar{\boldsymbol{E}} = \frac{1}{2}(\bar{\boldsymbol{C}} - \boldsymbol{I})$ 。通常情况下 $\operatorname{dev}\boldsymbol{E} \neq \bar{\boldsymbol{E}}$，只有在纯体积变形（即 $\boldsymbol{C}$ 是 $\boldsymbol{I}$ 的倍数）这种特殊情况下两者才会相等。这凸显了[亨基应变](@entry_id:191329)在进行体积-偏[应变分解](@entry_id:186005)时的独特优势。

在构建[超弹性本构模型](@entry_id:191665)时，通常会采用解耦的[应变能函数](@entry_id:178435)形式，例如：
$$
W(\boldsymbol{F}) = W_{\text{vol}}(J) + W_{\text{iso}}(\bar{I}_1, \bar{I}_2)
$$
其中 $W_{\text{vol}}$ 仅依赖于体积比 $J$，而 $W_{\text{iso}}$ 依赖于[等容变形](@entry_id:196451)张量（如 $\bar{\boldsymbol{B}}=\bar{\boldsymbol{F}}\bar{\boldsymbol{F}}^{\mathsf{T}}$）的 **[不变量](@entry_id:148850)** $\bar{I}_1 = \operatorname{tr}(\bar{\boldsymbol{B}})$ 和 $\bar{I}_2 = \frac{1}{2}[(\operatorname{tr}\bar{\boldsymbol{B}})^2 - \operatorname{tr}(\bar{\boldsymbol{B}}^2)]$。这些[不变量](@entry_id:148850)只与形状改变有关，与体积变化无关 。这种形式的本构模型中，材料的偏应力响应完全由 $W_{\text{iso}}$ 决定 。

### 在二维模型中的应用

在[计算力学](@entry_id:174464)中，为了降低计算成本，常常采用二维简化模型，如[平面应变](@entry_id:167046)和[平面应力](@entry_id:172193)。在这些模型中，体积-偏[应变分解](@entry_id:186005)的定义需要根据具体情况进行调整，以确保物理意义和计算上的一致性。

#### [平面应变](@entry_id:167046) (Plane Strain)

[平面应变假设](@entry_id:186003)在一个方向（例如 $z$ 方向）上的应变为零，即 $\varepsilon_{zz} = \varepsilon_{xz} = \varepsilon_{yz} = 0$。在这种情况下，物体仍然是一个三维实体，只是其变形受到了约束。因此，最自然和物理上最一致的做法是继续使用三维的分解框架 。

体积应变为三维应变张量的迹：
$$
\operatorname{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz} = \varepsilon_{xx} + \varepsilon_{yy}
$$
尽管 $\varepsilon_{zz}=0$，但在概念上，我们仍然是在一个三维空间中定义[体积应变](@entry_id:267252)。因此，偏[应变张量](@entry_id:193332)仍然通过减去三维球量部分得到：
$$
\boldsymbol{\varepsilon}^{\text{dev}} = \boldsymbol{\varepsilon} - \frac{1}{3}\operatorname{tr}(\boldsymbol{\varepsilon})\boldsymbol{I}_{3\times3}
$$
这会导致面外的正[偏应变](@entry_id:201263)分量 $\varepsilon_{zz}^{\text{dev}} = -\frac{1}{3}(\varepsilon_{xx} + \varepsilon_{yy})$ 不为零。

#### 平面应力 (Plane Stress)

[平面应力假设](@entry_id:184389)在一个方向上的应力为零，即 $\sigma_{zz} = \sigma_{xz} = \sigma_{yz} = 0$。对于[各向同性材料](@entry_id:170678)，这并不意味着 $\varepsilon_{zz}=0$。事实上，由于泊松效应，面内的拉伸或压缩会引起面外的收缩或膨胀。根据[胡克定律](@entry_id:149682)，可以推导出 ：
$$
\varepsilon_{zz} = -\frac{\lambda}{2\mu+\lambda}(\varepsilon_{xx} + \varepsilon_{yy}) = -\frac{\nu}{1-\nu}(\varepsilon_{xx} + \varepsilon_{yy})
$$
其中 $\nu$ 是[泊松比](@entry_id:158876)。

在这种情况下，计算中通常采用一种更符合二维模型直觉的分解方式。定义 **面内体积应变** 为二维[应变张量](@entry_id:193332)的迹：
$$
\operatorname{tr}_{\text{2D}}(\boldsymbol{\varepsilon}) = \varepsilon_{xx} + \varepsilon_{yy}
$$
相应地，**面内[偏应变](@entry_id:201263)** 的定义也应基于二维空间。在二维空间中，球量部分的系数是 $\frac{1}{2}$ 而不是 $\frac{1}{3}$：
$$
\boldsymbol{\varepsilon}^{\text{dev}}_{\text{in-plane}} = \boldsymbol{\varepsilon}_{\text{in-plane}} - \frac{1}{2}\operatorname{tr}_{\text{2D}}(\boldsymbol{\varepsilon})\boldsymbol{I}_{2\times2}
$$
其中 $\boldsymbol{\varepsilon}_{\text{in-plane}}$ 和 $\boldsymbol{I}_{2\times2}$ 分别是 $xy$ 平面内的[应变张量](@entry_id:193332)和单位张量 。

总结而言，为平面应变和平面应力问题选择合适的体积-偏[应变分解](@entry_id:186005)框架，需要仔细考虑其背后的物理假设和数学上的一致性，这对于确保数值模拟的准确性至关重要。