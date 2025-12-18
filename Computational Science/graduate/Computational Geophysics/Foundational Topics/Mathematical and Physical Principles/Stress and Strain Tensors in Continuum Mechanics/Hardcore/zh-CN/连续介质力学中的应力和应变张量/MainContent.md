## 引言
在[计算地球物理学](@entry_id:747618)的广阔领域中，从板块的缓慢漂移到地震的瞬时破裂，所有力学现象的背后都遵循着一套共同的物理语言——[连续介质力学](@entry_id:155125)。而[应力与应变](@entry_id:137374)张量，正是这门语言的核心词汇，它们是定量描述物质内部相互作用力与几何变形的根本工具。然而，对于许多研究生而言，从抽象的张量数学到解决具体的地球物理问题之间存在着一道鸿沟。如何将复杂的张量运算与[地幔对流](@entry_id:203493)、断层滑动或岩石损伤等实际过程联系起来，是学习和研究中的一个关键挑战。

本文旨在弥合这一差距。我们将以系统化的方式，引领读者穿越[应力与应变](@entry_id:137374)张量的理论与实践世界。在“原理与机制”一章中，我们将奠定坚实的理论基础，从连续介质假设出发，详细阐述不同[应力与应变](@entry_id:137374)度量的定义及物理意义。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些理论如何在[地球动力学](@entry_id:749832)、地震学和岩土工程等领域大放异彩，揭示理论与应用的紧密联系。最后，通过“动手实践”一章中的具体计算问题，您将有机会亲手应用所学知识，巩固理解并提升解决实际问题的能力。现在，让我们从最基本的原理开始，踏上这段探索之旅。

## 原理与机制

本章旨在深入探讨[连续介质力学](@entry_id:155125)的两大基石——[应力与应变](@entry_id:137374)张量。我们将从这些概念的基本定义出发，系统地阐述它们的物理意义、数学表达以及在不同变形尺度下的适用性。本章内容是后续学习地球物理介质复杂本构模型和进行[数值模拟](@entry_id:137087)的基础。我们将从基本原理出发，逐步构建一个完整的理论框架，并结合具体算例，阐明这些理论在[计算地球物理学](@entry_id:747618)中的应用。

### 连续介质假设：连接地球物理介质的宏观与微观

连续介质力学的根基是一个核心的理想化假设：**连续介质假设**。该假设认为，像岩石、土壤或地幔流体这样的物质，尽管在微观尺度上由离散的颗粒、晶体或分子构成，但在我们关心的宏观尺度上可以被视为一个连续、无间隙的整体。在此假设下，我们可以定义一系列连续的场变量，如密度场 $\rho(\boldsymbol{x}, t)$、[位移场](@entry_id:141476) $\boldsymbol{u}(\boldsymbol{x}, t)$ 和应[力场](@entry_id:147325) $\boldsymbol{\sigma}(\boldsymbol{x}, t)$，它们在空间中的每一点都有明确的定义。

这一假设的合理性依赖于**尺度分离**（scale separation）的概念。具体而言，我们必须能够找到一个中间的[特征长度尺度](@entry_id:266383) $\ell$，它远大于材料的微观结构尺度 $a$（如颗粒直径或[晶格](@entry_id:196752)尺寸），同时又远小于我们感兴趣的宏观问题尺度 $L$（如断层长度或岩层厚度）。即满足 $a \ll \ell \ll L$。

为了给场变量一个严格的物理定义，我们引入**[代表性](@entry_id:204613)单元体**（Representative Elementary Volume, REV）的概念。一个场量在空间点 $\boldsymbol{x}$ 的值，被定义为以 $\boldsymbol{x}$ 为中心、特征尺寸为 $\ell$ 的邻域内微观量的体积平均。当这个邻域的体积 $V_\ell$ 从微观尺度逐渐增大时，平均值会因包含的微观结构增多而迅速稳定下来，其统计涨落的[方差](@entry_id:200758)随 $V_\ell$ 的增大而衰减。REV就是使得这种平均值稳定到一个具有代表性数值所需的最小体积，其对应的特征尺寸为 $\ell_{\mathrm{REV}}$。

因此，连续介质假设成立的一个必要条件是，我们研究的系统存在一个REV，并且该REV的尺寸远小于宏观梯度变化的尺度。在[计算地球物理学](@entry_id:747618)中，这意味着用于离散化控制方程的网格单元尺寸 $\Delta x$ 必须至少与REV同量级，即 $\Delta x \gtrsim \ell_{\mathrm{REV}}$，这样每个数值计算单元才能代表一个“连续介质点”。

一个关键的复杂性来自于微观结构中可能存在的长程关联，例如[颗粒介质](@entry_id:750006)中的[力链](@entry_id:199587)或孔隙网络。如果这些微观涨落具有一个特征关联长度 $\ell_c$，那么为了获得具有统计意义的平均值，REV的尺寸必须大于这个关联长度，即 $\ell_{\mathrm{REV}} \gtrsim \ell_c$。

设想一个[计算地球物理学](@entry_id:747618)家正在模拟一个部分饱和的断层泥及其周围的多孔围岩 。假设断层泥的平均颗粒直径为 $a = 5 \times 10^{-4} \ \mathrm{m}$，但其中存在着[相关长度](@entry_id:143364)为 $\ell_c = 5 \times 10^{-2} \ \mathrm{m}$ 的细观结构（如[力链](@entry_id:199587)和孔隙度涨落）。宏观研究区[域的特征](@entry_id:154386)长度为 $L = 10 \ \mathrm{m}$。如果计划采用的有限体积法网格间距为 $\Delta x = 1 \times 10^{-2} \ \mathrm{m}$，我们就会遇到一个问题。尽管网格远大于颗粒尺寸（$\Delta x \gg a$），但它却小于微观结构的关联长度（$\Delta x  \ell_c$）。由于有效的REV尺寸必须大于 $\ell_c$，这意味着所选的网格单元无法包含一个完整的REV。在这种情况下，每个网格单元内的物理量将表现出巨大的、非[代表性](@entry_id:204613)的涨落，连续介质模型在该分辨率下失效。此时，必须采用更粗的网格（$\Delta x \gtrsim \ell_c$）或者转向离散颗粒模型（如[离散元法](@entry_id:748501)）来直接解析颗粒间的相互作用。

### 变形的度量：[应变张量](@entry_id:193332)

当一个连续体从其初始的**参考构型**（由物质点坐标 $\boldsymbol{X}$ 描述）运动到一个新的**当前构型**（由空间点坐标 $\boldsymbol{x}$ 描述）时，我们称之为发生了变形。这一过程可以通过**运动映射** $\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)$ 来描述。位移场则定义为 $\boldsymbol{u} = \boldsymbol{x} - \boldsymbol{X}$。为了定量描述变形，我们需要引入应变张量。

描述局部变形最核心的量是**变形梯度张量**（deformation gradient tensor），定义为运动映射对参考坐标的梯度：
$$
\boldsymbol{F} = \frac{\partial \boldsymbol{\varphi}}{\partial \boldsymbol{X}} = \boldsymbol{I} + \frac{\partial \boldsymbol{u}}{\partial \boldsymbol{X}}
$$
其中 $\boldsymbol{I}$ 是单位张量。$\boldsymbol{F}$ 包含了关于局部拉伸和旋转的全部信息。一个纯粹的[刚体运动](@entry_id:193355)（平移和旋转）不产生应变，因此任何有效的[应变度量](@entry_id:755495)都必须对刚体运动不敏感。

#### [有限应变度量](@entry_id:185716)

对于地壳构造或[地幔对流](@entry_id:203493)中的大变形问题，必须使用[有限应变理论](@entry_id:176941)。

**[格林-拉格朗日应变张量](@entry_id:187745)**（Green-Lagrange strain tensor）$\boldsymbol{E}$ 是一个**拉格朗日**（Lagrangian）度量，它在参考构型中定义。它通过比较参考构型中一个无限小[线元](@entry_id:196833) $d\boldsymbol{X}$ 在变形前后的长度平方变化来定义。变形后的[线元](@entry_id:196833)为 $d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$。其长度平方的改变为：
$$
|d\boldsymbol{x}|^2 - |d\boldsymbol{X}|^2 = (d\boldsymbol{X})^T \boldsymbol{F}^T \boldsymbol{F} d\boldsymbol{X} - (d\boldsymbol{X})^T \boldsymbol{I} d\boldsymbol{X} = (d\boldsymbol{X})^T (\boldsymbol{F}^T \boldsymbol{F} - \boldsymbol{I}) d\boldsymbol{X}
$$
我们定义 $\boldsymbol{E}$ 使得 $|d\boldsymbol{x}|^2 - |d\boldsymbol{X}|^2 = 2 (d\boldsymbol{X})^T \boldsymbol{E} d\boldsymbol{X}$，因此：
$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{F}^T \boldsymbol{F} - \boldsymbol{I}) = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})
$$
其中 $\boldsymbol{C} = \boldsymbol{F}^T\boldsymbol{F}$ 被称为**[右柯西-格林张量](@entry_id:174156)**（right Cauchy-Green tensor）。由于[刚体运动](@entry_id:193355)下 $\boldsymbol{F}$ 是一个正交张量 $\boldsymbol{Q}$（满足 $\boldsymbol{Q}^T\boldsymbol{Q} = \boldsymbol{I}$），此时 $\boldsymbol{C} = \boldsymbol{I}$，故 $\boldsymbol{E} = \boldsymbol{0}$，这证实了 $\boldsymbol{E}$ 是一个纯粹的变形度量 。

相对地，**[欧拉-阿尔曼西应变张量](@entry_id:194948)**（Euler-Almansi strain tensor）$\boldsymbol{e}$ 是一个**欧拉**（Eulerian）度量，它在当前构型中定义。它将同一个长度平方变化与当前构型的[线元](@entry_id:196833) $d\boldsymbol{x}$ 联系起来。通过关系 $d\boldsymbol{X} = \boldsymbol{F}^{-1} d\boldsymbol{x}$，可推导出：
$$
|d\boldsymbol{x}|^2 - |d\boldsymbol{X}|^2 = (d\boldsymbol{x})^T (\boldsymbol{I} - \boldsymbol{F}^{-T} \boldsymbol{F}^{-1}) d\boldsymbol{x}
$$
因此，
$$
\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{F}^{-T} \boldsymbol{F}^{-1}) = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{B}^{-1})
$$
其中 $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^T$ 是**[左柯西-格林张量](@entry_id:186163)**（left Cauchy-Green tensor）。与 $\boldsymbol{E}$ 类似，$\boldsymbol{e}$ 在[刚体运动](@entry_id:193355)下也为零 。

例如，考虑一个平面应变拉伸，其变形梯度为 $\boldsymbol{F} = \mathrm{diag}(\lambda, \lambda^{-1}, 1)$。对于 $\lambda = 1.2$ 的情况，我们可以计算出两种应变的主要分量。$E_{11} = \frac{1}{2}(1.2^2 - 1) = 0.22$，而 $e_{11} = \frac{1}{2}(1 - 1.2^{-2}) \approx 0.1528$。这清楚地表明，对于同一个物理变形，不同的[应变度量](@entry_id:755495)会给出不同的数值，因此在选择[本构模型](@entry_id:174726)时必须指明所用的[应变度量](@entry_id:755495)。

#### 微小（无穷小）应变

在许多地球物理应用中，如[地震波传播](@entry_id:165726)或微小的地壳形变，[位移梯度](@entry_id:165352)非常小，即 $\|\nabla\boldsymbol{u}\| \ll 1$。在这种情况下，可以采用线性化的[运动学](@entry_id:173318)，大大简化问题。

**[无穷小应变张量](@entry_id:167211)**（infinitesimal strain tensor）$\boldsymbol{\varepsilon}$ 定义为[位移梯度](@entry_id:165352)的对称部分：
$$
\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^T)
$$
这个线性化的[应变度量](@entry_id:755495)是[格林-拉格朗日应变](@entry_id:170427) $\boldsymbol{E}$ 在小变形假设下的近似。将 $\boldsymbol{F} = \boldsymbol{I} + \nabla\boldsymbol{u}$ 代入 $\boldsymbol{E}$ 的定义中，我们得到 ：
$$
\boldsymbol{E} = \frac{1}{2}((\boldsymbol{I} + \nabla\boldsymbol{u})^T(\boldsymbol{I} + \nabla\boldsymbol{u}) - \boldsymbol{I}) = \frac{1}{2}(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^T + (\nabla\boldsymbol{u})^T\nabla\boldsymbol{u})
$$
于是，
$$
\boldsymbol{E} = \boldsymbol{\varepsilon} + \frac{1}{2}(\nabla\boldsymbol{u})^T\nabla\boldsymbol{u}
$$
近似的误差项 $\boldsymbol{E} - \boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\boldsymbol{u})^T\nabla\boldsymbol{u}$ 是[位移梯度](@entry_id:165352)的二次项。这意味着当 $\|\nabla\boldsymbol{u}\| \ll 1$ 时，误差是高阶小量，使用 $\boldsymbol{\varepsilon}$ 代替 $\boldsymbol{E}$ 是合理的。例如，在简单剪切变形中，[位移梯度](@entry_id:165352)量级为 $\gamma$，误差的量级则为 $\gamma^2$ 。类似地，可以证明 $\boldsymbol{e}$ 在小变形下也近似等于 $\boldsymbol{\varepsilon}$ 。然而，必须注意，这种线性化仅在[位移梯度](@entry_id:165352)和旋转都很小的情况下成立。对于大旋转小应变的情况，[无穷小应变张量](@entry_id:167211)会产生虚假的应变，此时必须使用[有限应变理论](@entry_id:176941)。

#### 高级[应变度量](@entry_id:755495)：[亨基应变](@entry_id:191329)

除了上述两种经典[应变度量](@entry_id:755495)，还存在其他[有限应变度量](@entry_id:185716)，其中**[亨基应变](@entry_id:191329)**（Hencky strain）或[对数应变](@entry_id:751438)在描述某些材料（特别是塑性材料）的行为时具有独特的优势。它基于变形梯度的极分解 $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$，其中 $\boldsymbol{R}$ 是[旋转张量](@entry_id:191990)，$\boldsymbol{U}$ 是对称正定的右[拉伸张量](@entry_id:193200)。[亨基应变](@entry_id:191329)定义为：
$$
\boldsymbol{H} = \ln(\boldsymbol{U})
$$
$\boldsymbol{H}$ 的一个重要特性是，对于共轴的连续变形，总应变是各阶段应变的简单加和，因此被认为是“真实”的[应变度量](@entry_id:755495)。在后续讨论[非线性](@entry_id:637147)[本构关系](@entry_id:186508)时，我们将看到基于不同[应变度量](@entry_id:755495)（如 $\boldsymbol{E}$ 或 $\boldsymbol{H}$）的材料模型会产生截然不同的应力响应 。

### 内力的度量：[应力张量](@entry_id:148973)

连续体内部的相互作用力通过应力张量来描述。根据柯西应力原理，作用在连续体内一个假想面上的力（称为**面力**，traction），与该面的法向有关。

#### 柯西应力张量

**柯西[应力张量](@entry_id:148973)**（Cauchy stress tensor）$\boldsymbol{\sigma}$ 是我们通常所说的“真实”应力。它是一个定义在**当前构型**下的[二阶张量](@entry_id:199780)，它通过柯西关系式将[面力矢量](@entry_id:189429) $\boldsymbol{t}$ 与该面的单位法向矢量 $\boldsymbol{n}$ 联系起来：
$$
\boldsymbol{t} = \boldsymbol{\sigma} \boldsymbol{n} \quad \text{或} \quad t_i = \sigma_{ij} n_j
$$
$\boldsymbol{\sigma}$ 的一个基本性质是其**对称性**，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$。这个性质并非来自材料属性，而是源于物理学的基本定律——**[角动量守恒](@entry_id:156798)**。对于一个不存在体偶（body couples）和面偶（couple stresses）的经典（非极性）连续体，局部的[角动量平衡](@entry_id:181848)方程最终会简化为一个纯粹的代数条件 $\sigma_{ij} = \sigma_{ji}$。这一结论对于任何材料、无论变形大小都成立 。

#### 有限变形下的应力度量

在有限变形理论中，由于参考构型和当前构型存在显著差异，我们需要引入其他应力度量来方便地在不同构型之间建立联系。

**[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量**（First Piola-Kirchhoff stress tensor）$\boldsymbol{P}$，也称为**名义应力**（nominal stress），是一个混合度量。它将作用在**当前构型**上面元 $d\boldsymbol{a}$ 上的力 $d\boldsymbol{f}$，与**参考构型**中对应的面元 $d\boldsymbol{A}$ 联系起来：$d\boldsymbol{f} = \boldsymbol{P} d\boldsymbol{A}$。它与柯西应力的关系为 ：
$$
\boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-T}
$$
其中 $J = \det(\boldsymbol{F})$ 是体积变化率。由于 $\boldsymbol{P}$ 的定义混合了两个构型（力在当前构型，面积在参考构型），它是一个“两点张量”，并且通常是**非对称**的 。其主要优点在于，动量方程可以用完全在参考构型上定义的量来表达，便于求解。

**[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量**（Second Piola-Kirchhoff stress tensor）$\boldsymbol{S}$ 是一个完全的**拉格朗日**量。它将一个“伪力”矢量 $d\boldsymbol{f}_0 = \boldsymbol{F}^{-1} d\boldsymbol{f}$ 与参考构型中的面元 $d\boldsymbol{A}$ 联系起来。它与 $\boldsymbol{P}$ 和 $\boldsymbol{\sigma}$ 的关系为 ：
$$
\boldsymbol{S} = \boldsymbol{F}^{-1} \boldsymbol{P} = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-T}
$$
这个从柯西应力到第二PK应力的变换称为**[拉回](@entry_id:160816)**（pull-back）操作。由于柯西应力 $\boldsymbol{\sigma}$ 是对称的，通过上述变换可以证明 $\boldsymbol{S}$ 也是**对称**的 。$\boldsymbol{S}$ 的一个关键物理意义是它在能量上与[格林-拉格朗日应变](@entry_id:170427) $\boldsymbol{E}$ **[功共轭](@entry_id:194957)**，即[应变能密度](@entry_id:200085)率可以表达为 $\dot{W} = \boldsymbol{S}:\dot{\boldsymbol{E}}$。此外，$\boldsymbol{S}$ 对于[刚体转动](@entry_id:191086)是不变的，这意味着它只度量由材料拉伸和剪切引起的应力，是建立材料[本构关系](@entry_id:186508)的理想选择。

例如，对于一个经历了变形梯度为 $\boldsymbol{F} = \mathrm{diag}(1.2, 0.8, 1.0)$ 的[地质材料](@entry_id:749838)，如果在当前构型下测得的柯西应力为 $\boldsymbol{\sigma} = \mathrm{diag}(100, 50, 25) \ \mathrm{MPa}$，我们可以利用上述公式计算出对应的第一和[第二皮奥拉-基尔霍夫应力](@entry_id:173163) 。计算表明，尽管 $\boldsymbol{\sigma}$ 是对角的，但由于变形的非均匀性，变换后的 $\boldsymbol{P}$ 和 $\boldsymbol{S}$ 的分量值会发生显著变化，反映了面积和方向的改变对名义应力和物质应力的影响。

### 应力状态的分解与[不变量](@entry_id:148850)

为了更好地理解和应用[应力张量](@entry_id:148973)，特别是在建立材料的屈服和破坏准则时，我们需要对其进行分解并识别其[不变量](@entry_id:148850)。

#### 体积-偏[应力分解](@entry_id:272862)

任何一个三维应力张量 $\boldsymbol{\sigma}$ 都可以唯一地分解为一个**球形应力**（isotropic/spherical stress）部分和一个**[偏应力](@entry_id:163323)**（deviatoric stress）部分 ：
$$
\boldsymbol{\sigma} = p\boldsymbol{I} + \boldsymbol{s}
$$
其中，球形应力部分由**[平均应力](@entry_id:751819)**（mean stress）或**[静水压力](@entry_id:275365)**（hydrostatic pressure）$p$ 和单位张量 $\boldsymbol{I}$ 构成。平均应力定义为[应力张量](@entry_id:148973)迹的三分之一：
$$
p = \frac{1}{3} \mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33})
$$
这部分应力与材料的体积变化相关。在地球科学中，通常规定压应力为正，因此大的正 $p$ 值表示高的围压。

[偏应力张量](@entry_id:267642) $\boldsymbol{s}$ 则通过从总应力中减去球形应力部分得到：
$$
\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}
$$
根据定义，[偏应力张量](@entry_id:267642)的迹恒为零，$\mathrm{tr}(\boldsymbol{s}) = 0$。它代表了应力状态中引起形状改变（剪切变形）的部分。例如，对于一个应力状态 $\boldsymbol{\sigma} = \begin{pmatrix} 120  30 \\ 30  80 \end{pmatrix}$ MPa（为简化只看二维），其平均应力为 $p = (120+80)/2 = 100$ MPa。其[偏应力](@entry_id:163323)部分为 $\boldsymbol{s} = \begin{pmatrix} 20  30 \\ 30  -20 \end{pmatrix}$ MPa。这种分解在[粘塑性](@entry_id:165397)本构模型中至关重要，因为材料的屈服和流动通常主要由[偏应力](@entry_id:163323)驱动，而破坏和损伤则可能同时受到静水压力和[偏应力](@entry_id:163323)的影响。

#### [应力不变量](@entry_id:170526)

对于一个**各向同性**（isotropic）材料，其力学行为不应依赖于[坐标系](@entry_id:156346)的选择。这意味着描述其行为的[本构方程](@entry_id:138559)必须是**标架无关**（frame-indifferent）或**客观**（objective）的。因此，如果一个[本构关系](@entry_id:186508)（如[屈服准则](@entry_id:193897)）是应力的函数，它必须通过应力的**[不变量](@entry_id:148850)**（invariants）来表达。[不变量](@entry_id:148850)是在[坐标系](@entry_id:156346)旋转下保持不变的标量。

对于一个三维对称应力张量，存在三个独立的**[主不变量](@entry_id:193522)**。在塑性力学和[岩石力学](@entry_id:754400)中，通常使用以下一组[不变量](@entry_id:148850) ：
1.  **第一[应力不变量](@entry_id:170526) $I_1$**：等于应力张量的迹，与[平均应力](@entry_id:751819)直接相关。
    $$ I_1 = \mathrm{tr}(\boldsymbol{\sigma}) = 3p $$
    它反映了应力状态的[静水压力](@entry_id:275365)水平。
2.  **第二偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_2$**：与[偏应力](@entry_id:163323)的“大小”或[剪切应力](@entry_id:137139)的强度相关。
    $$ J_2 = \frac{1}{2} \boldsymbol{s}:\boldsymbol{s} = \frac{1}{2} \mathrm{tr}(\boldsymbol{s}^2) $$
    $J_2$ 与材料中的[畸变能](@entry_id:198925)密度有关。
3.  **第三偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_3$**：等于[偏应力张量](@entry_id:267642)的[行列式](@entry_id:142978)。
    $$ J_3 = \det(\boldsymbol{s}) $$
    $J_3$ (或通过它定义的**[Lode角](@entry_id:191590)**) 描述了应力状态在偏平面上的“形状”，区分了三轴压缩、三轴拉伸和纯剪等不同的加载模式。

可以证明，任何基于 $(I_1, J_2, J_3)$ 构建的标量函数 $f(\boldsymbol{\sigma}) = \hat{f}(I_1, J_2, J_3)$ 都是客观的 。

这些[不变量](@entry_id:148850)是构建[各向同性材料](@entry_id:170678)模型的基石。例如，经典的**[von Mises屈服准则](@entry_id:174339)**假设材料的屈服只与[畸变能](@entry_id:198925)有关，与静水压力无关，其[屈服函数](@entry_id:167970)形式为 $f(J_2) = \sqrt{J_2} - k = 0$。对于岩石和土壤这类压力敏感材料，[屈服强度](@entry_id:162154)会随围压的增加而提高。**Drucker-Prager[屈服准则](@entry_id:193897)**便是一个考虑了压力敏感性的模型，其[屈服函数](@entry_id:167970)同时依赖于 $I_1$ 和 $J_2$ ：
$$
f(I_1, J_2) = \sqrt{J_2} + \alpha I_1 - k = 0
$$
这里，参数 $\alpha$ 控制了压力敏感性。这个模型忽略了[Lode角](@entry_id:191590)的影响，即认为材料在不同剪切模式下的屈服应力是相同的。更复杂的模型，如Mohr-Coulomb或更现代的岩石损伤模型，会同时利用所有三个[不变量](@entry_id:148850)来更精确地描述材料行为。

### 本构关系：连接应力与应变

本构关系（constitutive relation）是描述特定材料应力与应变之间关系的数学方程，它是连续介质力学的核心。

#### 线性弹性与各向异性

最简单的[本构模型](@entry_id:174726)是**线性弹性**，即[广义胡克定律](@entry_id:203555)，它假设应力与应变成线性关系：
$$
\sigma_{ij} = C_{ijkl} \varepsilon_{kl}
$$
其中 $\mathbb{C}$ 是四阶**[刚度张量](@entry_id:176588)**（stiffness tensor）。对于完全各向异性的线性弹性材料，由于应力和应变[张量的对称性](@entry_id:202126)以及[应变能](@entry_id:162699)的存在，81个 $C_{ijkl}$ 分量中只有21个是独立的。

地球物理介质常常表现出**各向异性**。例如，页岩或沉积岩由于其层状结构，在平行于层面和垂直于层面的方向上具有不同的力学属性。一个常见的模型是**横观各向同性**（transversely isotropic）模型。假设材料的对称轴为 $x_3$ 轴（垂直方向），$x_1-x_2$ 平面为各向同性平面。通过施加绕 $x_3$ 轴任意旋转下的不变性要求，可以推导出[刚度张量](@entry_id:176588)的特定形式。在[Voigt表示法](@entry_id:166691)下（将二阶张量表示为向量，[四阶张量](@entry_id:181350)表示为6x6矩阵），横观[各向同性材料](@entry_id:170678)的刚度矩阵 $\mathbf{C}^V$ 具有如下结构 ：
$$
\mathbf{C}^{V} = \begin{pmatrix} C_{11}  C_{11} - 2C_{66}  C_{13}  0  0  0 \\ C_{11} - 2C_{66}  C_{11}  C_{13}  0  0  0 \\ C_{13}  C_{13}  C_{33}  0  0  0 \\ 0  0  0  C_{44}  0  0 \\ 0  0  0  0  C_{44}  0 \\ 0  0  0  0  0  C_{66} \end{pmatrix}
$$
此时，独立的弹性常数从21个减少到5个（$C_{11}, C_{33}, C_{44}, C_{66}, C_{13}$），这极大地简化了对这类材料的建模。

#### 有限变形下的超弹性

对于大变形问题，[线性弹性](@entry_id:166983)不再适用。**[超弹性](@entry_id:159356)**（hyperelasticity）模型假设应力可以从一个[应变能密度函数](@entry_id:755490) $W$ 中导出。然而，一个关键问题是：$W$ 应该是哪种[应变度量](@entry_id:755495)的函数？不同的选择将导致截然不同的[非线性](@entry_id:637147)本构模型。

例如，考虑两种各向同性的[超弹性](@entry_id:159356)模型 ：
1.  **圣维南-基尔霍夫（SVK）模型**：应变能是[格林-拉格朗日应变](@entry_id:170427) $\boldsymbol{E}$ 的二次函数。对应的第二PK应力为 $\boldsymbol{S}_E = \lambda \mathrm{tr}(\boldsymbol{E})\boldsymbol{I} + 2\mu\boldsymbol{E}$。
2.  **二次亨[基模](@entry_id:165201)型**：[应变能](@entry_id:162699)是[亨基应变](@entry_id:191329) $\boldsymbol{H}$ 的二次函数。它直接给出与 $\boldsymbol{H}$ [功共轭](@entry_id:194957)的[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau}_H = \lambda \mathrm{tr}(\boldsymbol{H})\boldsymbol{I} + 2\mu\boldsymbol{H}$。

尽管在[无穷小应变](@entry_id:197162)下 $\boldsymbol{E} \approx \boldsymbol{H} \approx \boldsymbol{\varepsilon}$，这两种模型会收敛于[线性弹性](@entry_id:166983)，但在有限应变下，它们的预测会大相径庭。例如，在俯冲带相关的大压缩和剪切变形下，SVK模型可能会预测出不切实际的应力行为（如在剪切下产生大的压应力），而基于[亨基应变](@entry_id:191329)的模型通常表现得更为物理。这凸显了在有限变形计算中，选择合适的[应变度量](@entry_id:755495)和本构框架的极端重要性。

#### 率形式本构与[客观应力率](@entry_id:199282)

对于粘弹性或[弹塑性](@entry_id:193198)等具有率相关行为的材料，本构关系通常以率的形式给出，即应力**率**与应变**率**之间的关系。在欧拉构架下进行[大变形](@entry_id:167243)数值模拟时（如模拟[地幔对流](@entry_id:203493)），一个核心挑战是时间导数的客观性。

简单地对柯西[应力张量](@entry_id:148973)求[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$，得到的张量率并**不是客观的**。这意味着，即使在一个纯刚体旋转运动中（无变形），$\dot{\boldsymbol{\sigma}}$ 也不为零，它会错误地反映出应力的变化。为了构建一个在物理上成立的率形式本构律，必须使用**[客观应力率](@entry_id:199282)**。

[客观应力率](@entry_id:199282)通过从物质导数中减去由材料自旋引起的非客观部分来构造。最常用的两种[客观应力率](@entry_id:199282)是 ：

1.  **Jaumann应力率**（或称协转应力率）：
    $$
    \overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}
    $$
    其中 $\boldsymbol{W} = \frac{1}{2}(\nabla\boldsymbol{v} - (\nabla\boldsymbol{v})^T)$ 是[自旋张量](@entry_id:187346)（[速度梯度](@entry_id:261686)的反对称部分）。它直观地表示在随着材料旋转的[坐标系](@entry_id:156346)中观察到的应力变化率。

2.  **Oldroyd上随体应力率**（upper-convected stress rate）：
    $$
    \overset{\triangledown}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^T
    $$
    其中 $\boldsymbol{L} = \nabla\boldsymbol{v}$ 是[速度梯度张量](@entry_id:270928)。这个率与特定的[应变度量](@entry_id:755495)（与[上随体导数](@entry_id:756365)相关的[应变率](@entry_id:154778)）自然共轭。

这两种应力率都是客观的，因为在刚体旋转下它们都为零。然而，它们在包含剪切的流动中会给出不同的结果。例如，在[稳态](@entry_id:182458)简单[剪切流](@entry_id:266817)中，基于Jaumann率的弹性模型会预测出非物理的[振荡](@entry_id:267781)剪应力，而基于Oldroyd率的模型则不会。因此，在为计算[地球动力学](@entry_id:749832)[模型选择](@entry_id:155601)[本构方程](@entry_id:138559)时，对不同[客观应力率](@entry_id:199282)特性的理解是至关重要的。