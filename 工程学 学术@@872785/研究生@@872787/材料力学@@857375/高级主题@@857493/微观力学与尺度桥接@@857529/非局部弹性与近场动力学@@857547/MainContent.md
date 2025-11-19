## 引言
几个世纪以来，经典连续介质力学一直是[固体力学](@entry_id:164042)的基石，但其“局部作用”的基本假设在处理[材料失效](@entry_id:160997)、[裂纹扩展](@entry_id:749562)以及微纳米尺度下的[尺寸效应](@entry_id:153734)等现象时暴露了其局限性。在这些尺度上，原子间相互作用力的长程性变得至关重要，这形成了经典理论无法弥合的知识鸿沟。本文旨在介绍为应对这些挑战而设计的两个强大框架：[非局部弹性](@entry_id:193991)理论与[近场动力学](@entry_id:191791)。通过从根本上重新思考物质点间的相互作用，这些理论为模拟复杂的材料行为提供了更符合物理现实的基础。

在本文中，您将通过结构化的学习路径，逐步掌握这些前沿概念。在第一章“原理与机制”中，我们将从与柯西局部作用原理的分歧点出发，深入剖析[非局部理论](@entry_id:752667)的数学和物理基础。第二章“应用与交叉学科联系”将通过探索其在[断裂力学](@entry_id:141480)、尺度效应建模以及与其他物理域耦合中的应用，展示这些理论的实际效能。最后，“动手实践”部分将通过引导性问题挑战您应用所学知识，搭建理论与实践之间的桥梁。接下来，让我们首先重新审[视力](@entry_id:204428)学的基础原理，以理解[非局部模型](@entry_id:175315)产生的必然性与重要性。

## 原理与机制

在前一章中，我们介绍了[非局部弹性](@entry_id:193991)理论和[近场动力学](@entry_id:191791)作为对经典[连续介质力学](@entry_id:155125)在模拟材料失效和多尺度现象方面局限性的回应。本章将深入探讨这些理论的数学和物理基础，从它们与经典理论的根本分歧点出发，系统地阐述其核心原理与关键机制。我们将阐明非局部相互作用是如何在数学上形式化的，[近场动力学](@entry_id:191791)是如何重新构建[运动方程](@entry_id:170720)的，以及这些新框架如何能够自主地预测复杂现象，如裂纹的萌生与扩展。

### 重新审[视力](@entry_id:204428)学基础：局部作用原理及其超越

经典连续介质力学的基石之一是**柯西的局部作用原理（Cauchy's postulate of local action）**。该原理断言，在连续体内部任意一点 $\mathbf{x}$，作用于一个假想切割面上的[接触力](@entry_id:165079)仅取决于该点的物质状态和该面的[法线](@entry_id:167651)方向 $\mathbf{n}$，而与该面周围的形状或曲率无关 [@problem_id:2619656]。这一假设的直接推论是柯西应力定理，它保证了**柯西[应力张量](@entry_id:148973)（Cauchy stress tensor）** $\boldsymbol{\sigma}$ 的存在，使得作用在任何方向为 $\mathbf{n}$ 的表面上的牵[引力](@entry_id:175476)矢量 $\mathbf{t}$ 都可以通过线性关系 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$ 来表示。

在此基础上，通过应用[动量守恒](@entry_id:149964)和角动量守恒两大基本物理定律，可以推导出连续介质的局部运动方程。对于任意物质[子域](@entry_id:155812) $V$，[线性动量守恒](@entry_id:165717)和[角动量守恒](@entry_id:156798)的积分形式可以分别表示为：

$$
\frac{\mathrm{d}}{\mathrm{d}t}\int_V \rho \mathbf{v}\, \mathrm{d}V = \int_{\partial V} \mathbf{t}(\mathbf{n})\, \mathrm{d}A + \int_V \rho \mathbf{b}\, \mathrm{d}V
$$

$$
\frac{\mathrm{d}}{\mathrm{d}t}\int_V \rho (\mathbf{x}-\mathbf{x}_0)\times \mathbf{v}\, \mathrm{d}V = \int_{\partial V} (\mathbf{x}-\mathbf{x}_0)\times \mathbf{t}(\mathbf{n})\, \mathrm{d}A + \int_V (\mathbf{x}-\mathbf{x}_0)\times \rho \mathbf{b}\, \mathrm{d}V
$$

其中 $\rho$ 是质量密度，$\mathbf{v}$ 是速度场，$\mathbf{b}$ 是单位质量的[体力](@entry_id:174230)。通过应用[高斯散度定理](@entry_id:188065)和假定被积函数连续，这些积分形式的守恒律可以转化为它们的局部（[微分](@entry_id:158718)）形式：

1.  **[线性动量守恒](@entry_id:165717)（柯西第一运动定律）**：$\nabla\cdot\boldsymbol{\sigma} + \rho \mathbf{b} = \rho \ddot{\mathbf{u}}$
2.  **角动量守恒（柯西第二运动定律）**：$\boldsymbol{\sigma} = \boldsymbol{\sigma}^\mathsf{T}$ (在没有体力偶和内禀力偶的假设下)

一个至关重要的概念是，这些平衡方程是**前本构的（pre-constitutive）** [@problem_id:2905446]。它们的推导仅依赖于[守恒定律](@entry_id:269268)和局部作用假设，而完全不涉及应力 $\boldsymbol{\sigma}$ 是如何与变形或应变 $\boldsymbol{\epsilon}$ 联系起来的。因此，无论材料的[本构关系](@entry_id:186508)是局部的（例如，$\boldsymbol{\sigma}(\mathbf{x})$ 仅依赖于 $\boldsymbol{\epsilon}(\mathbf{x})$）还是非局部的，这些[平衡方程](@entry_id:172166)本身的形式保持不变。非局部性改变的是本构关系本身，而非力学平衡的基本法则。

### 积分形式的[非局部弹性](@entry_id:193991)

[非局部理论](@entry_id:752667)的出发点是对局部作用原理的扬弃。它认为，在微观层面，物质点间的相互作用力（如原子间的键力）是长程的，因此一个点的宏观应力状态应该受到其邻域内所有点变形状态的影响。这种思想引入了一个**[内禀长度尺度](@entry_id:750789)（internal length scale）**，使得模型能够描述与[材料微观结构](@entry_id:198422)尺寸相关的[尺寸效应](@entry_id:153734)。

#### 非局部[本构关系](@entry_id:186508)

在经典[线性弹性](@entry_id:166983)中，本构关系是局部的：$\sigma_{ij}(\mathbf{x}) = C_{ijkl}(\mathbf{x})\epsilon_{kl}(\mathbf{x})$。而[非局部弹性](@entry_id:193991)理论将其推广为一个积分形式。对于一个线性、均匀、各向同性的[非局部弹性](@entry_id:193991)体，其本构关系通常表示为应变场与一个**衰减[核函数](@entry_id:145324)（attenuation kernel function）** $\alpha$ 的空间卷积 [@problem_id:2905405]：

$$
\sigma_{ij}(\mathbf{x}) = \int_{\Omega} \alpha\left(|\mathbf{x}-\mathbf{x}'|\right) C_{ijkl} \epsilon_{kl}(\mathbf{x}') \, \mathrm{d}V'
$$

这里的 $C_{ijkl}$ 是经典的[各向同性弹性](@entry_id:203237)张量。核函数 $\alpha(r)$ 描述了点 $\mathbf{x}'$ 处的应变对点 $\mathbf{x}$ 处应力的影响，它通常是一个随距离 $r=|\mathbf{x}-\mathbf{x}'|$ 增加而衰减的正值函数。为了使模型在物理上和数学上是合理的，核函数 $\alpha(r)$ 必须满足几个关键条件 [@problem_id:2905436]：

1.  **归一化（Normalization）**：为了在均匀应变场（$\boldsymbol{\epsilon}(\mathbf{x}') = \boldsymbol{\epsilon}_0$）下能够恢复经典胡克定律，[核函数](@entry_id:145324)在整个空间上的积分必须为1。
    $$
    \int_{\mathbb{R}^d} \alpha(|\boldsymbol{\xi}|) \, \mathrm{d}\boldsymbol{\xi} = 1
    $$
    这一条件确保了[非局部模型](@entry_id:175315)与经典理论在长波极限下的一致性。

2.  **可积性（Integrability）**：为了保证对于平方可积的应变场（$\boldsymbol{\epsilon} \in L^2(\Omega)$），其弹性能量是有限的，核函数必须是绝对可积的，即 $\alpha \in L^1(\mathbb{R}^d)$。这通过[杨氏卷积不等式](@entry_id:266357)保证了应[力场](@entry_id:147325)也是平方可积的。

3.  **对称性（Symmetry）**：柯西应力[张量的对称性](@entry_id:202126) $\sigma_{ij} = \sigma_{ji}$ 在此积分形式中是自动满足的，这得益于[弹性张量](@entry_id:170728) $C_{ijkl}$ 的次对称性 ($C_{ijkl}=C_{jikl}$)，而无需对标量[核函数](@entry_id:145324) $\alpha(r)$ 施加额外条件。

这种积分形式的非局部性具有一个重要优点：它能**正则化（regularize）**奇异场。在经典弹性力学中，[裂纹尖端](@entry_id:182807)等缺陷处的应[力场](@entry_id:147325)是奇异的（趋于无穷大）。而[非局部模型](@entry_id:175315)通过在邻域内进行积分平均，有效地“抹平”了这些[奇点](@entry_id:137764)，得到了有限的应力值，这更符合物理实际 [@problem_id:2905405]。

#### [微分](@entry_id:158718)近似及其悖论

在某些情况下，积分形式的非局部本构关系可以被一个[微分方程](@entry_id:264184)所近似，这在解析求解中更具便利性。这种关系被称为**Eringen[微分](@entry_id:158718)模型**。通过对光滑应变场进行泰勒展开，可以表明积分模型近似于一个[应变梯度理论](@entry_id:180517) [@problem_id:2905405]。更精确地，如果在傅里叶空间中，[核函数](@entry_id:145324)的[傅里叶变换](@entry_id:142120)恰好具有特定形式 $\widehat{\alpha}(|\mathbf{k}|) = (1+\ell^2 |\mathbf{k}|^2)^{-1}$，那么积分模型与以下的Helmholtz型[微分方程](@entry_id:264184)是**完全等价的**（在无限大空间中）[@problem_id:2905431]：

$$
(1 - \ell^2 \nabla^2) \boldsymbol{\sigma}(\mathbf{x}) = \mathbf{C} : \boldsymbol{\epsilon}(\mathbf{x})
$$

这里 $\ell$ 是[内禀长度尺度](@entry_id:750789)。与该[傅里叶变换](@entry_id:142120)对应的[实空间](@entry_id:754128)[核函数](@entry_id:145324)是著名的**[汤川势](@entry_id:139645)（Yukawa potential）** 或**[屏蔽库仑势](@entry_id:151053)（screened-Coulomb potential）**。例如，在一维情况下，该[核函数](@entry_id:145324)为 $\alpha(x) = \frac{1}{2\ell} \exp(-|x|/\ell)$ [@problem_id:2905431]。

然而，这种[微分](@entry_id:158718)近似模型存在严重的局限性，最著名的例子是**[悬臂梁](@entry_id:174096)悖论（cantilever beam paradox）** [@problem_id:2905380]。考虑一个端部受集中力作用的[悬臂梁](@entry_id:174096)，根据梁的平衡方程，梁内部的弯矩 $M(x)$ 是线性函数，这意味着 $d^2M/dx^2 = 0$。当此结果代入一维的Eringen[微分](@entry_id:158718)模型 $(1 - \ell^2 d^2/dx^2)M(x) = EI\kappa(x)$ 时，包含内禀长度 $\ell$ 的非局部项消失了，模型退化为经典的局部[欧拉-伯努利梁方程](@entry_id:147768) $M(x) = EI\kappa(x)$。这导致模型无法预测任何[非局部效应](@entry_id:198046)或[尺寸效应](@entry_id:153734)。此外，该[高阶微分方程](@entry_id:171249)所需的边界条件比经典理论多，导致在标准边界条件下问题变得数学上**不适定的（ill-posed）**。这个悖论揭示了[微分](@entry_id:158718)模型仅仅是一种近似，它在处理边界和集中载荷等问题时可能会失效，从而凸显了积分模型的根本重要性。

### [近场动力学](@entry_id:191791)：一种彻底的革新

[近场动力学](@entry_id:191791)（Peridynamics, PD）提供了一种更为激进的非局部建模[范式](@entry_id:161181)。它完全摒弃了应力、应变以及基于它们的[偏微分](@entry_id:194612)[运动方程](@entry_id:170720)。其核心假设是，连续体由一系列物[质点](@entry_id:186768)组成，这些点通过**“键（bonds）”**进行长程的、成对的力学相互作用 [@problem_id:2619656]。

#### [近场动力学](@entry_id:191791)[运动方程](@entry_id:170720)

在[近场动力学](@entry_id:191791)中，一个物[质点](@entry_id:186768) $\mathbf{x}$ 的[运动方程](@entry_id:170720)由牛顿第二定律直接写成积分形式，即该点的质量与加速度之积等于作用于其上的所有内力和外力之和 [@problem_id:2905397]：

$$
\rho(\mathbf{x})\ddot{\mathbf{u}}(\mathbf{x},t) = \int_{\mathcal{H}_{\mathbf{x}}} \mathbf{f}\left(\mathbf{u}(\mathbf{x}',t)-\mathbf{u}(\mathbf{x},t), \mathbf{x}'-\mathbf{x}\right) \, \mathrm{d}V' + \mathbf{b}(\mathbf{x},t)
$$

这个方程中的每一个组成部分都具有明确的物理意义：
- $\mathcal{H}_{\mathbf{x}} = \{\mathbf{x}' \in \Omega : |\mathbf{x}'-\mathbf{x}| \le \delta\}$ 是点 $\mathbf{x}$ 的**视域（horizon）**，一个半径为 $\delta$ 的球形邻域。相互作用仅存在于视域内部。$\delta$ 是该理论的[内禀长度尺度](@entry_id:750789)。
- $\mathbf{f}(\boldsymbol{\eta}, \boldsymbol{\xi})$ 是**成对力函[数密度](@entry_id:268986)（pairwise force density function）**，表示位于 $\mathbf{x}'$ 的物[质点](@entry_id:186768)对位于 $\mathbf{x}$ 的物[质点](@entry_id:186768)施加的力密度。它依赖于相对位移 $\boldsymbol{\eta} = \mathbf{u}' - \mathbf{u}$ 和相对位置 $\boldsymbol{\xi} = \mathbf{x}' - \mathbf{x}$。
- 为了满足[牛顿第三定律](@entry_id:166652)（作用力与反作用力定律），成[对力](@entry_id:159909)函数必须满足[反对称性](@entry_id:261893)：$\mathbf{f}(\boldsymbol{\eta}, \boldsymbol{\xi}) = -\mathbf{f}(-\boldsymbol{\eta}, -\boldsymbol{\xi})$。

由于该方程不包含位移场 $\mathbf{u}$ 的任何空间导数，它在位移场不连续（如裂纹面）的情况下依然是良好定义的。这正是[近场动力学](@entry_id:191791)在[断裂力学](@entry_id:141480)中取得巨大成功的根本原因。

#### 键基[近场动力学](@entry_id:191791)及其局限

最简单的[近场动力学](@entry_id:191791)模型是**键基（bond-based）**[近场动力学](@entry_id:191791)。在该模型中，任意一对物质点之间的相互作用力被假定为：
1.  仅依赖于连接这对点的“键”本身的变形。
2.  力的方向始终沿着变形后连接两点的直线方向（即[中心力](@entry_id:267832)）。

对于一个线性的微弹性材料，该力的大小正比于键的**伸长率（stretch）** $s = (|\boldsymbol{\xi}+\boldsymbol{\eta}| - |\boldsymbol{\xi}|)/|\boldsymbol{\xi}|$ [@problem_id:2905415]。线性化的成对力函数可以表示为：

$$
\mathbf{f}(\boldsymbol{\eta}, \boldsymbol{\xi}) = c(|\boldsymbol{\xi}|) s \frac{\boldsymbol{\xi}+\boldsymbol{\eta}}{|\boldsymbol{\xi}+\boldsymbol{\eta}|} \approx c(|\boldsymbol{\xi}|) s \frac{\boldsymbol{\xi}}{|\boldsymbol{\xi}|}
$$

其中 $c(|\boldsymbol{\xi}|)$ 被称为**微观模量函数（micromodulus function）**。

尽管键[基模](@entry_id:165201)型概念简单且功能强大，但其[中心力](@entry_id:267832)的假设带来了一个严重的限制。通过将均匀变形下的[近场动力学](@entry_id:191791)[应变能](@entry_id:162699)与经典[弹性理论](@entry_id:184142)的应变能进行等效匹配，可以发现，对于三维各向同性材料，键[基模](@entry_id:165201)型预测的等效**泊松比（Poisson's ratio）** 恒为 $\nu = 1/4$（在二维[平面应力](@entry_id:172193)下为 $\nu = 1/3$）[@problem_id:2905415] [@problem_id:2905406]。这个固定的泊松比与材料的微观模量 $c$ 或视域大小 $\delta$ 无关，限制了其模拟真实材料的能力。

#### 态基[近场动力学](@entry_id:191791)

为了克服键基模型的泊松比限制，**态基（state-based）**[近场动力学](@entry_id:191791)被提出。其核心思想是，一个键中的力不再仅仅依赖于该键自身的变形，而是可以依赖于该物质点视域内所有键的集体变形状态 [@problem_id:2905406]。

在态基模型中，我们定义：
- **变形态（Deformation State）** $\underline{\mathbf{Y}}$：一个将邻域内每个初始键向量 $\boldsymbol{\xi}$ 映射到其变形后向量 $\mathbf{Y}\langle\boldsymbol{\xi}\rangle = \mathbf{y}(\mathbf{x}+\boldsymbol{\xi}) - \mathbf{y}(\mathbf{x})$ 的算子（其中 $\mathbf{y}$ 是变形后的位置）。
- **力态（Force State）** $\underline{\mathbf{T}}$：一个将邻域内每个初始键向量 $\boldsymbol{\xi}$ 映射到作用在该键上的力向量 $\mathbf{T}\langle\boldsymbol{\xi}\rangle$ 的算子。

本构关系现在是力态与变形态之间的泛函关系 $\underline{\mathbf{T}} = \mathcal{F}(\underline{\mathbf{Y}})$。由于力态 $\mathbf{T}\langle\boldsymbol{\xi}\rangle$ 依赖于整个变形态 $\underline{\mathbf{Y}}$，它不再需要与变形后的键向量 $\mathbf{Y}\langle\boldsymbol{\xi}\rangle$ 共线。这种非[中心力](@entry_id:267832)的引入使得模型能够独立地描述剪切变形和体积变形，从而可以表示任意的[泊松比](@entry_id:158876)。

在一种被称为**“对应”模型（correspondence model）**的流行态基公式中，通过引入一个**形状张量（shape tensor）** $\mathbf{K}$，可以定义一个**非局部变形梯度（nonlocal deformation gradient）** $\mathbf{F}$ [@problem_id:2905406]：
$$
\mathbf{K}(\mathbf{x}) = \int_{\mathcal{H}_{\mathbf{x}}} \omega(|\boldsymbol{\xi}|) (\boldsymbol{\xi} \otimes \boldsymbol{\xi}) \, \mathrm{d}V'
$$
$$
\mathbf{F}(\mathbf{x}) = \left( \int_{\mathcal{H}_{\mathbf{x}}} \omega(|\boldsymbol{\xi}|) \mathbf{Y}\langle\boldsymbol{\xi}\rangle \otimes \boldsymbol{\xi} \, \mathrm{d}V' \right) \mathbf{K}(\mathbf{x})^{-1}
$$
其中 $\omega$ 是一个权重函数。这种构造方式保证了在均匀变形下，非局部变形梯度 $\mathbf{F}$ 精确地等于经典的局部变形梯度。这为建立与经典连续介质力学相容的[本构模型](@entry_id:174726)提供了桥梁。

### 非局部性的关键应用与实现

[非局部理论](@entry_id:752667)，特别是[近场动力学](@entry_id:191791)，为[材料力学](@entry_id:201885)中的一些长期挑战提供了创新的解决方案。

#### 无需追踪的[断裂模拟](@entry_id:199069)

经典[断裂力学](@entry_id:141480)依赖于对[裂纹尖端奇异性](@entry_id:171868)的复杂处理，并且需要额外的准则（如能量释放率或应力强度因子）来判断裂纹的扩展方向和速度。[近场动力学](@entry_id:191791)的最大优势之一是它能够**自主地（autonomously）**预测裂纹的萌生和扩展，而无需任何外部的裂纹追踪算法 [@problem_id:2905398]。

在[近场动力学](@entry_id:191791)中断裂的建模非常直观：
1.  为每个键定义一个**临界伸长率（critical stretch）** $s_c$。
2.  在模拟过程中，如果一个键的伸长率 $s(t)$ 首次超过 $s_c$，则该键发生不可逆的“断裂”，其承载的力永久性地设为零。
3.  裂纹被自然地定义为一系列断裂键的集合。当足够多的键在一个宏观表面附近断裂时，该表面两侧的物质点就失去了力学联系，从而形成一个宏观的、能够承受位移间断的裂纹面。

这个过程可以被优雅地描述为一个时变图的拓扑演化：物[质点](@entry_id:186768)是图的顶点，完好的键是边。[损伤演化](@entry_id:184965)对应于边的移除。当一个“切割集”的边被移除，将[图分割](@entry_id:152532)成两个或多个不连通的[子图](@entry_id:273342)时，一个宏观裂纹就形成了 [@problem_id:2905398]。重要的是，在合适的参数标定下（使断裂能 $\mathcal{G}_c$ 在 $\delta \to 0$ 时收敛于一个有限值），[近场动力学](@entry_id:191791)预测的[脆性断裂](@entry_id:158949)行为与经典的[Griffith理论](@entry_id:159659)相符 [@problem_id:2905398]。

#### 边界条件的处理

由于[非局部模型](@entry_id:175315)中的相互作用力是长程的，边界附近物质点的视域会延伸到物体外部。这些“缺失的键”意味着经典的点状边界条件（如 $\mathbf{t}(\mathbf{x}) = \bar{\mathbf{t}}$）不再适用。施加在边界上的外力必须以一种与非局部框架相容的方式传递到物体内部 [@problem_id:2905437]。

在实践中，有两种主流方法来施加力（诺伊曼）边界条件：
1.  **边界约束区（Boundary Collar）法**：在靠近物理边界 $\partial\Omega$ 的一个厚度为 $\delta$ 的层（称为约束区）内施加一个虚拟的[体力](@entry_id:174230) $\mathbf{g}(\mathbf{x})$。该体力场 $\mathbf{g}$ 的选取应保证其在任何[虚位移](@entry_id:168781)场上做的[虚功](@entry_id:176403)都等价于所期望的经典边界牵[引力](@entry_id:175476)所做的[虚功](@entry_id:176403)。

2.  **虚拟层（Fictitious Layer）法**：在物体外部创建一个虚拟的物质层。然后，通过定义物理物体内的点与虚拟层内的点之间的成对相互作用力，来施加外部载荷。这些外部相互作用力同样通过[虚功原理](@entry_id:138749)来确定，以匹配经典牵[引力](@entry_id:175476)所做的功。

这两种方法都将经典的[表面力](@entry_id:188034)重新解释为一个作用在[边界层](@entry_id:139416)体积上的非局部载荷，从而解决了边界条件施加的难题，并保证了全局[动量守恒](@entry_id:149964) [@problem_id:2905437]。