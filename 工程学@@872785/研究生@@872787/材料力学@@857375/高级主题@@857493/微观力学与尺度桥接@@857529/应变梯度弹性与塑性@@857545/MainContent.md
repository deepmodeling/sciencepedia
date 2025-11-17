## 引言
材料在宏观世界中所展现的力学性能，我们似乎已了如指掌。然而，当我们将视线投向微米甚至纳米尺度时，一个奇特而普遍的现象浮现出来：材料似乎变得“越小越强”。无论是弯曲一根微米级的细丝，还是用针尖按压金属表面，我们都会发现其表观刚度或强度远超宏观块体材料。这一“[尺寸效应](@entry_id:153734)”现象对微[机电系统](@entry_id:264947)（MEMS）、薄膜技术和先进[复合材料](@entry_id:139856)的设计构成了根本性的挑战。

问题在于，被奉为圭臬的经典连续介质力学在预测此类现象时却[无能](@entry_id:201612)为力。其理论框架内不包含任何内禀的[材料长度尺度](@entry_id:197771)，导致其预测结果与物体的绝对尺寸无关，这与大量的小尺度实验结果相矛盾。为了填补这一理论空白，[应变梯度](@entry_id:204192)弹性和塑性理论应运而生。它通过将应变的空间梯度作为基本变量引入本构关系，成功地将材料的微观结构特征（体现为一个或多个“[内禀长度尺度](@entry_id:750789)”）与宏观力学响应联系起来。

本文将系统地引导读者进入[应变梯度理论](@entry_id:180517)的世界。我们将深入探讨该理论的数学基础和物理内涵，从高阶运动学和本构关系出发，推导其独特的控制方程，并揭示其与[位错](@entry_id:157482)等微观缺陷的内在联系。我们还将展示该理论的强大解释力，阐明其如何应用于解释[裂纹尖端](@entry_id:182807)、微压痕、薄膜强化以及[霍尔-佩奇效应](@entry_id:144956)等一系列前沿科学和工程问题。最后，我们提供了一系列从简到难的计算练习，帮助读者将理论知识转化为解决实际问题的能力，并理解其在数值实现中的关键考量。让我们首先深入其核心，探究[应变梯度理论](@entry_id:180517)的基石。

## 原理与机制

在引言章节中，我们已经了解了在微米尺度下[材料力学](@entry_id:201885)行为中出现的尺寸效应，这些现象无法用经典的连续介质力学来解释。本章节将深入探讨[应变梯度理论](@entry_id:180517)的物理原理和数学框架，阐明其如何通过引入[内禀长度尺度](@entry_id:750789)来捕捉这些效应。我们将首先建立应变梯度弹性的[运动学](@entry_id:173318)和本构关系，推导其控制方程和边界条件。随后，我们将展示该理论如何解释[尺寸效应](@entry_id:153734)、[波色散](@entry_id:180230)和[应力奇异性](@entry_id:166362)的正则化。最后，我们将理论从弹性范畴扩展到塑性范畴，引入[位错](@entry_id:157482)的概念，并构建应变梯度塑性模型，以解释塑性变形中的“越小越强”现象。

### 经典理论的局限性：无尺度不变性

经典[连续介质力学](@entry_id:155125)的核心假设是，一个点处的应力仅由该点处的应变决定。这一假设导致其理论框架不包含任何内禀的[材料长度尺度](@entry_id:197771)。为了理解这一点，我们可以考虑一个思想实验。

在经典线性弹性理论中，控制方程（Navier-Cauchy 方程）可以写作：
$$
\mu \nabla^2 \mathbf{u} + (\lambda+\mu) \nabla(\nabla \cdot \mathbf{u}) + \mathbf{b} = \mathbf{0}
$$
其中 $\mathbf{u}$ 是[位移场](@entry_id:141476)，$\mathbf{b}$ 是体力密度，$\lambda$ 和 $\mu$ 是拉梅（Lamé）常数。这些材料常数，或等效的杨氏模量 $E$ 和[泊松比](@entry_id:158876) $\nu$，其量纲不包含长度。例如，$E$ 的单位是压力（力/面积）。

现在，让我们对系统进行尺度变换。假设有一个特征尺寸为 $L$ 的物体，其坐标为 $\mathbf{x}$。我们定义无量纲坐标 $\mathbf{x}' = \mathbf{x}/L$。如果我们对几何相似的物体施加几何相似的载荷，那么在无[体力](@entry_id:174230)的情况下，Navier-Cauchy 方程可以被无量纲化。[无量纲化](@entry_id:136704)的位移场 $\mathbf{u}'(\mathbf{x}')$ 所满足的方程将不包含任何与物体绝对尺寸 $L$ 相关的参数。这意味着，对于两个几何相似但尺寸不同（例如，一个尺寸是另一个的 $\alpha$ 倍）的物体，在承受几何相似的载荷时，其归一化的位移场和应变场是完全相同的。因此，经典[弹性理论](@entry_id:184142)是**无尺度的（scale-free）**，它无法从根本上预测材料的表观刚度会随着试样尺寸的变化而变化。

然而，大量微米尺度的弯曲、扭转和压痕实验明确表明，当试样尺寸减小到微米量级时，材料表现出显著的[硬化](@entry_id:177483)行为，即“越小越强”。这一矛盾表明，在小尺度上，材料的响应必然依赖于某些内禀的长度尺度，而经典理论恰恰缺失了这一点。[应变梯度理论](@entry_id:180517)正是为了弥补这一缺陷而提出的，其核心思想是允许材料的能量和应力不仅依赖于应变，还依赖于应变的**空间梯度**。

### 高阶连续介质的[运动学](@entry_id:173318)

为了描述变形在空间中的不均匀性，我们需要引入新的[运动学](@entry_id:173318)量。在小变形假设下，除了标准的**应变张量（strain tensor）** $\boldsymbol{\varepsilon}$ 和**无穷小转动矢量（infinitesimal rotation vector）** $\boldsymbol{\omega}$ 之外，它们各自的梯度也变得至关重要。

给定一个位移场 $\mathbf{u}(\mathbf{x})$，[位移梯度](@entry_id:165352) $\nabla\mathbf{u}$ 可以分解为其对称部分和反对称部分，分别定义了应变张量 $\boldsymbol{\varepsilon}$ 和转动张量。应变张量的分量为：
$$
\varepsilon_{ij} = \frac{1}{2} (u_{i,j} + u_{j,i})
$$
其中逗号下标表示对相应坐标的[偏导数](@entry_id:146280)，例如 $u_{i,j} = \partial u_i / \partial x_j$。应变张量是二阶对称张量，即 $\varepsilon_{ij} = \varepsilon_{ji}$。

无穷小转动矢量 $\boldsymbol{\omega}$ 的分量定义为：
$$
\omega_i = \frac{1}{2} \epsilon_{ijk} u_{k,j}
$$
其中 $\epsilon_{ijk}$ 是列维-奇维塔（Levi-Civita）符号。

[应变梯度理论](@entry_id:180517)的核心[运动学](@entry_id:173318)量是**[应变梯度](@entry_id:204192)张量（strain gradient tensor）**，我们记作 $\nabla\boldsymbol{\varepsilon}$ 或 $\boldsymbol{\eta}$。它是一个三阶张量，其分量通过对**应变**求空间导数得到：
$$
\eta_{ijk} = \varepsilon_{ij,k} = \frac{\partial \varepsilon_{ij}}{\partial x_k} = \frac{1}{2} (u_{i,jk} + u_{j,ik})
$$
由于 $\varepsilon_{ij}$ 对称，应变梯度张量必然在其前两个指标上是对称的，即 $\eta_{ijk} = \eta_{jik}$。然而，它在后两个指标上通常没有对称性。

为了更深刻地理解变形梯度的[二阶导数](@entry_id:144508)所包含的物理信息，我们可以将应变梯度与**转动梯度张量（gradient of rotation tensor）**进行对比。转动梯度张量记作 $\nabla\boldsymbol{\omega}$ 或 $\boldsymbol{\chi}$，是一个二阶张量，其分量定义为：
$$
\chi_{ij} = \omega_{i,j} = \frac{\partial \omega_i}{\partial x_j} = \frac{1}{2} \epsilon_{ikl} u_{l,kj}
$$
与[应变梯度](@entry_id:204192)不同，转动梯度张量通常既不是对称的也不是反对称的。但它有一个重要的性质：它是**无迹的（traceless）**。其迹为：
$$
\mathrm{tr}(\boldsymbol{\chi}) = \chi_{ii} = \frac{1}{2} \epsilon_{ikl} u_{l,ki}
$$
由于位移场足够光滑时[二阶偏导数](@entry_id:635213)可交换（$u_{l,ki} = u_{l,ik}$），而 $\epsilon_{ikl}$ 在交换任意两个指标时变号，对称张量 $u_{l,ik}$ 与[反对称张量](@entry_id:199349) $\epsilon_{ikl}$ 在指标 $i,k$ 上的缩并为零。因此，$\mathrm{tr}(\boldsymbol{\chi}) = 0$。

应变梯度 $\nabla\boldsymbol{\varepsilon}$ 和转动梯度 $\nabla\boldsymbol{\omega}$ 捕捉了位移场[二阶导数](@entry_id:144508)的不同方面：前者主要描述了应变的非均匀性，而后者描述了[晶格](@entry_id:196752)转动的非[均匀性](@entry_id:152612)。在[晶体塑性](@entry_id:141273)中，这两种梯度都与[几何必需位错](@entry_id:187571)密度直接相关。

### 应变梯度弹性：本构与控制方程

#### 自由能与[高阶应力](@entry_id:186008)

在[超弹性](@entry_id:159356)框架下，材料的[本构关系](@entry_id:186508)由一个[标量势](@entry_id:276177)函数——[亥姆霍兹自由能](@entry_id:136442)密度 $\psi$ ——完全确定。对于应变梯度弹性体，$\psi$ 不仅是应变 $\boldsymbol{\varepsilon}$ 的函数，还是[应变梯度](@entry_id:204192) $\nabla\boldsymbol{\varepsilon}$ 的函数，即 $\psi = \psi(\boldsymbol{\varepsilon}, \nabla\boldsymbol{\varepsilon})$。

与这些[运动学](@entry_id:173318)变量共轭的应力量通过对自由能密度求导得到。
- **柯西[应力张量](@entry_id:148973)（Cauchy stress tensor）** $\boldsymbol{\sigma}$，与应变 $\boldsymbol{\varepsilon}$ 共轭：
$$
\sigma_{ij} = \frac{\partial \psi}{\partial \varepsilon_{ij}}
$$
由于 $\varepsilon_{ij}$ 是对称的，其共轭的柯西应力 $\sigma_{ij}$ 也必须是对称的，即 $\sigma_{ij} = \sigma_{ji}$。这与经典理论中角动量守恒的要求一致。

- **[高阶应力](@entry_id:186008)张量（higher-order stress tensor）** 或 **双重[应力张量](@entry_id:148973)（double stress tensor）** $\mathbf{m}$，与[应变梯度](@entry_id:204192) $\nabla\boldsymbol{\varepsilon}$ 共轭：
$$
m_{ijk} = \frac{\partial \psi}{\partial \varepsilon_{ij,k}}
$$
由于应变梯度 $\varepsilon_{ij,k}$ 在其前两个指标上是对称的（$\varepsilon_{ij,k} = \varepsilon_{ji,k}$），其共轭的[高阶应力](@entry_id:186008) $m_{ijk}$ 也必然在这两个指标上是对称的，即 $m_{ijk} = m_{jik}$。

对于一个各向同性的线性[应变梯度](@entry_id:204192)弹性材料，其自由能密度 $\psi$ 可以写成 $\boldsymbol{\varepsilon}$ 和 $\nabla\boldsymbol{\varepsilon}$ 的二次型[不变量](@entry_id:148850)的组合。一个简单的形式是：
$$
\psi(\boldsymbol{\varepsilon}, \nabla\boldsymbol{\varepsilon}) = \frac{1}{2}\lambda(\mathrm{tr}\boldsymbol{\varepsilon})^2 + \mu \boldsymbol{\varepsilon}:\boldsymbol{\varepsilon} + \frac{1}{2}\mu \ell^2 \sum_{i,j,k,p,q,r} A_{ijkpqr} \varepsilon_{ij,k} \varepsilon_{pq,r}
$$
其中第一、二项是经典线弹性能，第三项是梯度能。$\ell$ 是一个具有长度量纲的**内禀[材料长度尺度](@entry_id:197771)**，它正是捕捉尺寸效应的关键。$A_{ijkpqr}$ 是一个无量纲的六阶张量，对于各向同性材料，它可以由少数几个独立的梯度弹性模量确定。

#### 控制方程与边界条件

[应变梯度](@entry_id:204192)弹性体的控制方程可以通过[变分原理](@entry_id:198028)（如[哈密顿原理](@entry_id:175601)或[虚功原理](@entry_id:138749)）导出。考虑一个一维杆的轴向运动作为例子，其自由能密度简化为：
$$
\psi(\varepsilon, \varepsilon') = \frac{1}{2}E\varepsilon^2 + \frac{1}{2}E\ell^2(\varepsilon')^2
$$
其中 $\varepsilon = u'$ 是[轴向应变](@entry_id:160811)，$\varepsilon' = u''$ 是应变梯度。通过[哈密顿原理](@entry_id:175601)，可以推导出其运动方程（强形式场方程）：
$$
\rho \frac{\partial^2 u}{\partial t^2} = E \frac{\partial^2 u}{\partial x^2} - E\ell^2 \frac{\partial^4 u}{\partial x^4} + b(x,t)
$$
这是一个[四阶偏微分方程](@entry_id:176247)（Partial Differential Equation, PDE），与经典[弹性理论](@entry_id:184142)的[二阶波动方程](@entry_id:754606)形成鲜明对比。[高阶导数](@entry_id:140882)项 $-E\ell^2 u''''$ 正是[应变梯度](@entry_id:204192)效应的体现。

在三维情况下，计及[高阶应力](@entry_id:186008)的[线性动量平衡](@entry_id:193575)方程（即平衡方程）为：
$$
\sigma_{ij,j} - m_{ijk,kj} + b_i = \rho \ddot{u}_i
$$
经典应力散度 $\sigma_{ij,j}$ 现在被一个包含[高阶应力](@entry_id:186008)二阶散度的项 $m_{ijk,kj}$ 所修正。

由于控制方程是更高阶的，求解它需要更多的边界条件。在[应变梯度理论](@entry_id:180517)中，边界上不仅可以指定经典的位移或力，还可以指定高阶的[运动学](@entry_id:173318)量或力学量。在一个光滑边界 $\Gamma$ 上，典型的边界条件分为两对：
- **本质（几何）边界条件**: 在边界的一部分 $\Gamma_u$上指定位移 $\mathbf{u}$ 和位移的**[法向导数](@entry_id:169511)** $\partial \mathbf{u} / \partial n$。
- **自然（力学）边界条件**: 在边界的另一部分 $\Gamma_t$上指定一个**广义牵[引力](@entry_id:175476)** $\mathbf{t}$ 和一个与位移[法向导数](@entry_id:169511)共轭的**高阶牵[引力](@entry_id:175476)**（或称双重力）$\mathbf{m}_n$。

这种扩展的边界条件集合是高阶连续介质理论的一个基本特征，它为模拟约束在微观尺度下的力学行为提供了必要的数学工具。

### [应变梯度](@entry_id:204192)弹性的物理效应

引入应变梯度项不仅解决了经典理论的尺度不变性问题，还带来了一系列新的物理预测。

#### [尺寸效应](@entry_id:153734)的解释

现在我们可以回到[尺寸效应](@entry_id:153734)的问题。当我们用特征外部尺寸 $L$（如梁的直径）来无量纲化四阶控制方程时，梯度项和经典项的系数之比会产生一个[无量纲数](@entry_id:136814)，其形式为 $(\ell/L)^2$。这意味着，无量纲化的解将依赖于[内禀长度尺度](@entry_id:750789) $\ell$ 和外部几何尺寸 $L$ 的比值。当 $L$ 很大时（宏观尺度），$\ell/L \to 0$，梯度项可以忽略，理论退化为经典弹性。而当 $L$ 减小到与 $\ell$ 可比拟时（微观尺度），$\ell/L$ 变大，梯度项变得显著，导致了与经典理论不同的、依赖于尺寸的力学响应，通常表现为刚度的增加。

#### 声学[波的色散](@entry_id:275520)

在经典[弹性理论](@entry_id:184142)中，[弹性波](@entry_id:196203)的相速度是恒定的，不随波长或频率改变。然而，[应变梯度理论](@entry_id:180517)预测波在介质中会发生**[色散](@entry_id:263750)（dispersion）**。考虑一维杆中的平面[谐波](@entry_id:181533)解 $u(x,t) = \hat{u} \exp(i(kx - \omega t))$，其中 $k$ 是波数，$\omega$ 是角频率。将其代入[一维运动](@entry_id:190890)方程，可得到[色散关系](@entry_id:140395)：
$$
\omega(k) = \sqrt{\frac{E k^2 + E\ell^2 k^4}{\rho}} = c_0 k \sqrt{1 + \ell^2 k^2}
$$
其中 $c_0 = \sqrt{E/\rho}$ 是经典杆中的[波速](@entry_id:186208)。显然，相速度 $v_p = \omega/k = c_0\sqrt{1 + \ell^2 k^2}$ 和群速度 $v_g = d\omega/dk = c_0(1+2\ell^2 k^2)/\sqrt{1+\ell^2 k^2}$ 都依赖于波数 $k$。这意味着不同波长（$\lambda = 2\pi/k$）的波将以不同的速度传播，这与[晶格动力学](@entry_id:145448)对[声子色散曲线](@entry_id:262236)的预测在长波近似下是一致的。

#### 奇异性的正则化

经典弹性理论在处理集中力或[裂纹尖端](@entry_id:182807)等问题时，会预测出非物理的应力或应变[奇异点](@entry_id:199525)（即无限大）。[应变梯度](@entry_id:204192)弹性通过其高阶微分算子自然地**正则化（regularize）**了这些奇异性。四阶或更高阶的控制方程所对应的格林函数比二阶算子的[格林函数](@entry_id:147802)更为光滑。例如，施加一个集中力时，经典弹性解的应力在作用点是奇异的，而[应变梯度](@entry_id:204192)弹性解的应力在作用点是有限的。这种正则化机制是**局域的**，因为它源于本构关系中对局部高阶导数的依赖。这与其他[广义连续介质理论](@entry_id:193621)（如非局部积分理论）通过[空间平均](@entry_id:203499)来“抹平”奇异性的机制形成了对比。

### 从弹性到塑性：[位错](@entry_id:157482)的角色

当材料进入塑性变形阶段，其不可恢复的变形主要是通过[位错](@entry_id:157482)的运动和增殖来实现的。为了将梯度效应引入塑性理论，我们必须建立连续介质场变量与离散[位错](@entry_id:157482)结构之间的联系。

[位错](@entry_id:157482)可分为两类：
- **[统计存储位错](@entry_id:181754)（Statistically Stored Dislocations, SSDs）**: 这些[位错](@entry_id:157482)以偶极子、环等形式随机[分布](@entry_id:182848)在晶体中。它们在宏观上不引起[晶格](@entry_id:196752)的净曲率，但在均匀变形过程中通过相互作用导致[加工硬化](@entry_id:160669)。
- **[几何必需位错](@entry_id:187571)（Geometrically Necessary Dislocations, GNDs）**: 当塑性变形不均匀时，为了保持[晶格](@entry_id:196752)的连续性，必须存在这些[位错](@entry_id:157482)。它们导致了[晶格](@entry_id:196752)的净曲率。例如，一个弯曲的晶体必须包含净的[刃位错](@entry_id:191098)。

描述GNDs密度的关键连续介质场量是**[奈氏位错密度张量](@entry_id:186646)（Nye dislocation density tensor）** $\boldsymbol{\alpha}$。在一个小变形框架下，总[位移梯度](@entry_id:165352) $\nabla\mathbf{u}$ 可以分解为弹性部分 $\boldsymbol{\beta}^e$ 和塑性部分 $\boldsymbol{\beta}^p$。塑性部分 $\boldsymbol{\beta}^p$ 通常是**不协调的（incompatible）**，即它的旋度不为零。[奈氏张量](@entry_id:200495)正是通过塑性畸变张量 $\boldsymbol{\beta}^p$ 的旋度来定义的：
$$
\boldsymbol{\alpha} = - \nabla \times \boldsymbol{\beta}^p \quad \text{或分量形式} \quad \alpha_{ij} = - \epsilon_{jkl} \beta^p_{il,k}
$$
（注意：符号约定可能不同，此处采用与部分文献一致的负号定义，其物理意义不变）。[奈氏张量](@entry_id:200495)的物理意义是穿过某一面元的净伯格斯矢量密度。其积分形式为：
$$
b_i = \int_S \alpha_{ij} n_j dA
$$
其中 $\mathbf{b}$ 是穿过[曲面](@entry_id:267450) $S$ 的净[伯格斯矢量](@entry_id:160637)。由于SSDs在宏观尺度上其[伯格斯矢量](@entry_id:160637)相互抵消，它们的净贡献为零。因此，[奈氏张量](@entry_id:200495) $\boldsymbol{\alpha}$ 只量度了GNDs的密度。

### [应变梯度塑性理论](@entry_id:172852)

#### 基于[位错](@entry_id:157482)的[硬化](@entry_id:177483)模型

[应变梯度塑性理论](@entry_id:172852)的核心思想是，[流变应力](@entry_id:198884)不仅依赖于累积的塑性应变（这与SSDs密度相关），还依赖于塑性应变的梯度（这与GNDs密度相关）。一个简单而物理直观的模型是基于**[泰勒硬化](@entry_id:184921)（Taylor hardening）**关系建立的。

[泰勒关系](@entry_id:161818)指出，[流变应力](@entry_id:198884) $\sigma_{\text{flow}}$ 与总[位错密度](@entry_id:161592) $\rho_{\text{total}}$ 的平方根成正比：
$$
\sigma_{\text{flow}} = M \alpha \mu b \sqrt{\rho_{\text{total}}}
$$
其中 $M$ 是泰勒因子，$\alpha$ 是一个无量纲常数，$\mu$ 是[剪切模量](@entry_id:167228)，$b$ 是伯格斯矢量模长。总位错密度是SSDs和GNDs之和：$\rho_{\text{total}} = \rho_S + \rho_G$。

关键的联系在于，GND密度 $\rho_G$ 与塑性[应变梯度](@entry_id:204192)的模量成正比：
$$
\rho_G \approx \eta \frac{|\nabla \boldsymbol{\varepsilon}^p|}{b}
$$
其中 $\eta$ 是一个几何因子。将此关系代入泰勒公式，我们得到一个梯度增强的[流变应力](@entry_id:198884)模型：
$$
\sigma_{\text{flow}} = M \alpha \mu b \sqrt{\rho_S + \eta \frac{|\nabla \boldsymbol{\varepsilon}^p|}{b}}
$$
这个模型直观地解释了[塑性中的尺寸效应](@entry_id:187409)。对于给定的宏观塑性变形，在更小的几何特征中（如微压痕、细丝），必然伴随着更大的塑性[应变梯度](@entry_id:204192) $|\nabla\boldsymbol{\varepsilon}^p|$。这导致了更高的GND密度 $\rho_G$，从而需要更大的[流变应力](@entry_id:198884)来驱动变形。这就是“越小越强”现象在塑性中的[微观力学](@entry_id:195009)根源。

#### 能量和耗散长度尺度

在更一般化的[热力学](@entry_id:141121)框架下，梯度效应可以通过两种不同的方式进入塑性模型，这引出了**能量长度尺度（energetic length scale）** $\ell_e$ 和 **耗散长度尺度（dissipative length scale）** $\ell_d$ 的概念。

- **能量长度尺度 $\ell_e$**: 如果塑性应变梯度（作为状态变量）贡献于系统的[亥姆霍兹自由能](@entry_id:136442)（例如，GNDs[排列](@entry_id:136432)形成的亚[晶界](@entry_id:196965)储存了能量），那么这种效应是**能量性的**。自由能中会包含一个与 $\ell_e$ 相关的项，其形式通常为 $\psi_{\text{grad}} \sim \mu \ell_e^2 |\nabla\boldsymbol{\varepsilon}^p|^2$。$\ell_e$ 因此表征了与塑性变形不均匀性相关的能量存[储能](@entry_id:264866)力。

- **耗散长度尺度 $\ell_d$**: 如果塑性[应变率](@entry_id:154778)的梯度（作为率变量）影响了材料的耗散过程（即屈服或流动准则），那么这种效应是**[耗散性](@entry_id:162959)的**。这可以出现在率相关的模型中，其中耗散势包含如 $\mathcal{R}_{\text{grad}} \sim \sigma_y \ell_d^2 |\nabla\dot{\boldsymbol{\varepsilon}}^p|^2$ 的项；也可以出现在率无关的模型中，其中屈服应力本身就依赖于塑性应变梯度，例如[屈服函数](@entry_id:167970)写成 $f(\sigma, \varepsilon^p, \ell_d |\nabla \boldsymbol{\varepsilon}^p|)$ 的形式。$\ell_d$ 因此表征了塑性流动对变形梯度的敏感性。

区分这两种长度尺度对于建立和理解不同类型的[应变梯度](@entry_id:204192)塑性模型至关重要。[能量尺度](@entry_id:196201)与缺陷结构的能量存储有关，而耗散尺度则与驱动[塑性流动](@entry_id:201346)的阻力有关。在许多实际模型中，这两种效应可能同时存在，共同决定了材料在微米尺度下的复杂力学行为。