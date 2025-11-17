## 引言
许多先进材料，如聚合物、橡胶和生物软组织，在实际应用中会经历大变形，并同时表现出弹性和黏性相结合的复杂力学行为。经典的小应变理论无法准确描述这些现象，因此，建立一个能够统一处理[大变形](@entry_id:167243)[几何非线性](@entry_id:169896)和材料时间依赖性的理论框架——即有限应变黏弹性理论——变得至关重要。本文旨在系统性地填补这一知识缺口，为读者提供一个从基本原理到前沿应用的全面视角。在接下来的内容中，我们将首先在“原理与机制”一章中，奠定有限变形运动学和[热力学](@entry_id:141121)的基础，并探讨本构模型的构建机制。随后，我们将在“应用与跨学科连接”一章中，展示该理论在工程设计、[生物力学](@entry_id:153973)和[材料科学](@entry_id:152226)中的实际应用。最后，通过“动手实践”部分，巩固和深化对核心概念的理解。

## 原理与机制

本章旨在系统性地阐述有限应变黏弹性理论的基本原理与核心机制。我们将从描述[大变形](@entry_id:167243)的运动学语言出发，建立必要的动力学和[热力学](@entry_id:141121)框架，最终探讨如何构建能够捕捉材料复杂行为的本构模型。本章内容是后续章节具体应用和数值实现的基础。

### 有限变形运动学：描述材料的形变

在线性弹性或黏弹性理论中，我们假设变形是“小”的，这极大地简化了数学描述。然而，对于聚合物、橡胶、生物软组织等材料，其工作变形往往远超小应变范畴，必须采用[有限应变理论](@entry_id:176941)。

#### 变形梯度与[雅可比行列式](@entry_id:137120)

描述一个连续体运动的核心工具是 **变形映射 (deformation map)** $\boldsymbol{\varphi}$。它将材料在某一参考构型 $\mathcal{B}_0$ 中的每个物[质点](@entry_id:186768) $\boldsymbol{X}$ 与其在当前构型中 $t$ 时刻的空间位置 $\boldsymbol{x}$ 建立[一一对应](@entry_id:143935)关系：$\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X}, t)$。

为了量化物[质点](@entry_id:186768)邻域内的局部变形，我们引入 **变形梯度 (deformation gradient)** 张量 $\boldsymbol{F}$。它被定义为变形映射 $\boldsymbol{\varphi}$ 对参考坐标 $\boldsymbol{X}$ 的梯度：
$$
\boldsymbol{F}(\boldsymbol{X}, t) = \nabla_{\boldsymbol{X}} \boldsymbol{\varphi}(\boldsymbol{X}, t)
$$
在分量形式下，记作 $F_{iJ} = \partial x_i / \partial X_J$。变形梯度的基本物理意义在于，它将参考构型中的一个无穷小[线元](@entry_id:196833) $d\boldsymbol{X}$ 线性地映射到当前构型中对应的[线元](@entry_id:196833) $d\boldsymbol{x}$：
$$
d\boldsymbol{x} = \boldsymbol{F} \, d\boldsymbol{X}
$$
这一定义是分析局部变形的基石。

从数学和物理的角度看，变形映射必须满足一定的合理性条件。首先，物质是不可穿透的，这意味着一个有限体积的物质不能被压缩至零体积或负体积。其次，物质点的局部邻域在变形后其“手性”或朝向应保持不变。这两个物理要求共同指向一个核心的数学约束，即变形梯度的[行列式](@entry_id:142978)，也称为 **雅可比行列式 (Jacobian determinant)** $J$，必须恒为正：
$$
J = \det \boldsymbol{F} > 0
$$
$J$ 的物理意义是局部体积变化的比例：当前构型中的一个微元体积 $dv$ 与其在参考构型中的对应体积 $dV$ 之间的关系为 $dv = J \, dV$。因此，$J > 1$ 表示局部[体积膨胀](@entry_id:144241)，$0 \lt J \lt 1$ 表示局部体积压缩，而 $J=1$ 则对应于 **[等容变形](@entry_id:196451) (isochoric deformation)**，即[体积保持](@entry_id:141001)不变。

$J>0$ 的条件也保证了变形映射在局部是可逆的。根据[反函数定理](@entry_id:275014)，如果映射 $X \mapsto \boldsymbol{\varphi}(X,t)$ 在某点是连续可微的（$C^1$），并且其雅可比行列式（即 $J=\det \boldsymbol{F}$）不为零，则该映射在该点的一个邻域内是可逆的。物理上的 $J>0$ 条件比数学上的 $J \neq 0$ 更为严格，它排除了 $J0$ 这种会导致物质邻域发生“内外翻转”的非物理情形。值得注意的是，$J>0$ 仅保证局部一一对应，并不能保证全局无自穿透。例如，一根长杆可以弯曲回来接触自身，尽管其内部每一点的 $J$ 都大于零。

#### 有限[应变张量](@entry_id:193332)

变形梯度 $\boldsymbol{F}$ 本身包含了[刚体转动](@entry_id:191086)和纯粹的拉伸变形。为了只描述导致应力产生的拉伸变形，我们需要引入 **[应变张量](@entry_id:193332) (strain tensors)**。在线性理论中，[位移梯度](@entry_id:165352)的小量部分就足以定义应变。但在有限变形下，我们需要能够正确处理大转动的客观应变量。

最常用的两个应变张量是 **[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)** $\boldsymbol{E}$ 和 **[欧拉-阿尔曼西应变张量](@entry_id:194948) (Euler-Almansi strain tensor)** $\boldsymbol{e}$。它们的定义都基于所谓的 **柯西-格林张量 (Cauchy-Green tensors)**。

**[右柯西-格林张量](@entry_id:174156) (right Cauchy-Green tensor)** $\boldsymbol{C}$ 定义为 $\boldsymbol{C} = \boldsymbol{F}^T \boldsymbol{F}$，它是一个定义在参考构型上的张量。$\boldsymbol{C}$度量了参考构型中[线元](@entry_id:196833)长度平方的变化。基于$\boldsymbol{C}$，[格林-拉格朗日应变张量](@entry_id:187745)定义为：
$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})
$$
其中 $\boldsymbol{I}$ 是单位张量。由于 $\boldsymbol{C}$ 是通过将变形梯度“[拉回](@entry_id:160816)”到参考构型来构造的，$\boldsymbol{E}$ 是一个 **参考构型 (referential)** 或 **拉格朗日 (Lagrangian)** 的应变量。

相应地，**[左柯西-格林张量](@entry_id:186163) (left Cauchy-Green tensor)** $\boldsymbol{b}$ 定义为 $\boldsymbol{b} = \boldsymbol{F} \boldsymbol{F}^T$，它是一个定义在当前构型上的张量。基于 $\boldsymbol{b}$，[欧拉-阿尔曼西应变张量](@entry_id:194948)定义为：
$$
\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{b}^{-1})
$$
由于 $\boldsymbol{b}$ 是一个[空间张量](@entry_id:185799)，$\boldsymbol{e}$ 是一个 **当前构型 (spatial)** 或 **欧拉 (Eulerian)** 的应变量。

这两个应变张量的一个关键性质是它们对叠加的[刚体转动](@entry_id:191086)具有客观性。如果物体在变形后经历一个额外的[刚体转动](@entry_id:191086) $\boldsymbol{Q}$，新的变形梯度为 $\hat{\boldsymbol{F}} = \boldsymbol{Q}\boldsymbol{F}$。可以证明，$\hat{\boldsymbol{C}} = \boldsymbol{C}$，因此 $\hat{\boldsymbol{E}} = \boldsymbol{E}$。这意味着[格林-拉格朗日应变](@entry_id:170427)对于当前构型的后续[刚体转动](@entry_id:191086)是不变的。而[欧拉-阿尔曼西应变](@entry_id:187104)则会跟随转动，$\hat{\boldsymbol{e}} = \boldsymbol{Q}\boldsymbol{e}\boldsymbol{Q}^T$，表现为一个客观的[空间张量](@entry_id:185799)。一个纯[刚体转动](@entry_id:191086)（无拉伸，$\boldsymbol{F}$ 为转动张量）不会产生任何应变，此时 $\boldsymbol{E}=\boldsymbol{0}$ 且 $\boldsymbol{e}=\boldsymbol{0}$。

在小应变极限下（即 $\boldsymbol{F}$ 趋近于 $\boldsymbol{I}$），$\boldsymbol{E}$ 和 $\boldsymbol{e}$ 都会退化为我们熟悉的[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^T)$。但在有限应变下，它们的值显著不同。例如，对于沿 $x$ 轴的[单轴拉伸](@entry_id:188287)，主拉伸比为 $\lambda > 1$，对应的应变分量为 $E_{xx} = (\lambda^2-1)/2$ 和 $e_{xx} = (1-\lambda^{-2})/2$。不难发现，当 $\lambda > 1$ 时，$E_{xx} > e_{xx} > 0$。选择哪种[应变度量](@entry_id:755495)取决于所构建的本构理论的框架。

#### 变形率与自旋

黏[弹性理论](@entry_id:184142)的核心是[应力与应变](@entry_id:137374)历史（特别是应变率）的关系。因此，我们需要精确定义变形的“速率”。描述速率的关键量是 **[空间速度梯度](@entry_id:187198) (spatial velocity gradient)** $\boldsymbol{L}$，定义为[空间速度](@entry_id:190294)场 $\boldsymbol{v}(\boldsymbol{x}, t)$ 对当前空间坐标 $\boldsymbol{x}$ 的梯度：
$$
\boldsymbol{L}(\boldsymbol{x}, t) = \nabla_{\boldsymbol{x}} \boldsymbol{v}(\boldsymbol{x}, t)
$$
速度梯度 $\boldsymbol{L}$ 与变形梯度 $\boldsymbol{F}$ 之间存在一个重要的运动学恒等式，可以通过链式法则推导得出：
$$
\boldsymbol{L} = \dot{\boldsymbol{F}}\boldsymbol{F}^{-1}
$$
其中 $\dot{\boldsymbol{F}}$ 是 $\boldsymbol{F}$ 的[物质时间导数](@entry_id:190892)。这个关系将[拉格朗日描述](@entry_id:264498)下的变形梯度变化率与[欧拉描述](@entry_id:264722)下的[速度场](@entry_id:271461)梯度联系起来。

与变形梯度 $\boldsymbol{F}$ 类似，速度梯度 $\boldsymbol{L}$ 也同时包含了材料的拉伸速率和刚性转动速率信息。任何[二阶张量](@entry_id:199780)都可以唯一地分解为其对称[部分和](@entry_id:162077)反对称部分。$\boldsymbol{L}$ 的这种分解具有明确的物理意义：
$$
\boldsymbol{L} = \boldsymbol{D} + \boldsymbol{W}
$$
其中，对称部分 $\boldsymbol{D}$ 称为 **变形率张量 (rate-of-deformation tensor)**：
$$
\boldsymbol{D} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^T)
$$
它描述了材料微元的拉伸、剪切等形状变化的速率。反对称部分 $\boldsymbol{W}$ 称为 **[自旋张量](@entry_id:187346) (spin tensor)**：
$$
\boldsymbol{W} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^T)
$$
它描述了材料微元作为刚体的瞬时转动角速度。这种分解是唯一的，为区分材料的真实变形速率和纯刚性转动速率提供了坚实基础。

### [动力学与热力学](@entry_id:138039)基本定律

在建立了描述变形的运动学语言后，我们需要引入力、能量和热力学定律，它们共同构成了所有[连续介质力学](@entry_id:155125)理论（包括黏弹性）不可动摇的普适性基础。

#### [应力张量](@entry_id:148973)及其关系

为了描述物体内部的相互作用力，我们引入 **应力 (stress)** 的概念。在有限变形理论中，由于参考构型和当前构型的区别，可以定义多种[应力张量](@entry_id:148973)。

1.  **柯西应力张量 (Cauchy stress tensor)** $\boldsymbol{\sigma}$：也称为真实应力，它是在 **当前构型** 中定义的。它将当前构型中一个面的[单位法向量](@entry_id:178851) $\boldsymbol{n}$ 映射到作用在该面上的单位面积力（即 **真实牵[引力](@entry_id:175476) (true traction)** $\boldsymbol{t}$）上：$\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$。这是我们最常接触、也最符合物理直觉的应力，因为它与当前实际的几何构型相关联。

2.  **[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量 (First Piola-Kirchhoff stress tensor)** $\boldsymbol{P}$：也称为名义应力，它是一个“两点”张量。它将 **参考构型** 中的[单位法向量](@entry_id:178851) $\boldsymbol{N}$ 映射到作用在变形后[曲面](@entry_id:267450)上的力（但按参考面积计算），即 **名义牵[引力](@entry_id:175476) (nominal traction)** $\boldsymbol{T}$：$\boldsymbol{T} = \boldsymbol{P}\boldsymbol{N}$。由于 $\boldsymbol{P}$ 将参考构型的向量映射到当前构型的力向量，它在计算上不便，且通常是非对称的。

3.  **[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量 (Second Piola-Kirchhoff stress tensor)** $\boldsymbol{S}$：这是一个完全定义在 **参考构型** 上的对称张量。它在能量上与[格林-拉格朗日应变张量](@entry_id:187745) $\boldsymbol{E}$ 共轭。它的引入主要是为了理论推导的便利，可以将复杂的空间构型问题转化到固定的参考构型上进行分析。

4.  **[基尔霍夫应力](@entry_id:751039)张量 (Kirchhoff stress tensor)** $\boldsymbol{\tau}$：定义为 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$。它是柯西应力的一个体积加权版本，在有限变形的能量和[本构关系](@entry_id:186508)推导中非常有用。

这些[应力张量](@entry_id:148973)描述的是同一个物理状态，因此它们之间存在确定的数学转换关系，这些关系被称为 **推前 (push-forward)** 和 **[拉回](@entry_id:160816) (pull-back)** 操作。基于力的平衡和[面积元](@entry_id:263205)之间的关系（[南森公式](@entry_id:195566) $n\,da = J \boldsymbol{F}^{-T} N\,dA$），可以推导出这些核心关系：
$$
\boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-T}
$$
$$
\boldsymbol{S} = \boldsymbol{F}^{-1} \boldsymbol{P} = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-T}
$$
从这些关系可以进一步得到重要的推前/[拉回](@entry_id:160816)公式：
$$
\boldsymbol{P} = \boldsymbol{F}\boldsymbol{S}
$$
$$
\boldsymbol{\tau} = J \boldsymbol{\sigma} = \boldsymbol{F} \boldsymbol{S} \boldsymbol{F}^T
$$
后者表明，[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau}$ 是[第二皮奥拉-基尔霍夫应力](@entry_id:173163) $\boldsymbol{S}$ 通过变形梯度“推前”到当前构型的结果。在构建[本构模型](@entry_id:174726)时，我们常常在参考构型中为 $\boldsymbol{S}$ 建立模型，然后通过这些关系得到物理上可测量的柯西应力 $\boldsymbol{\sigma}$。

#### [守恒定律](@entry_id:269268)

无论材料的本构关系如何复杂，它都必须遵守经典物理学的基本[守恒定律](@entry_id:269268)。这些定律的局部形式（即在空间每一点都成立的[微分方程](@entry_id:264184)形式）是建立[有限元分析](@entry_id:138109)等数值方法的基础。

1.  **质量守恒定律 (Balance of Mass)**：其局部形式，也称为[连续性方程](@entry_id:195013)，表述为：
    $$
    \dot{\rho} + \rho\,\mathrm{div}\,\boldsymbol{v} = 0
    $$
    这里 $\rho$ 是当前密度，$\dot{\rho}$ 是其物质导数，$\boldsymbol{v}$ 是[速度场](@entry_id:271461)。这个方程表明，密度的变化率与速度场的散度（代表体积膨胀率）有关。在[拉格朗日描述](@entry_id:264498)下，它等价于一个更简洁的形式：$\rho J = \rho_0$，其中 $\rho_0$ 是参考构型中均匀的初始密度。

2.  **[线性动量守恒](@entry_id:165717)定律 (Balance of Linear Momentum)**：即[牛顿第二定律](@entry_id:274217)在连续介质中的推广，其局部形式为：
    $$
    \mathrm{div}\,\boldsymbol{\sigma} + \rho\,\boldsymbol{b} = \rho\,\dot{\boldsymbol{v}}
    $$
    这里 $\boldsymbol{b}$ 是单位质量的体力（如重力），$\dot{\boldsymbol{v}}$ 是[物质加速度](@entry_id:270992)。该方程表明，[应力的散度](@entry_id:185633)（代表内部作用力的合力）和体力共同导致了物质的加速。

3.  **[角动量守恒](@entry_id:156798)定律 (Balance of Angular Momentum)**：对于绝大多数工程材料（非极性介质，即不存在体力矩和应力矩），角动量守恒定律最终简化为一个非常重要的代数约束：
    $$
    \boldsymbol{\sigma} = \boldsymbol{\sigma}^T
    $$
    即柯西[应力张量](@entry_id:148973)必须是对称的。通过[应力转换](@entry_id:193134)关系，可以证明[第二皮奥拉-基尔霍夫应力](@entry_id:173163) $\boldsymbol{S}$ 也必须是对称的。

需要再次强调，这三条定律是普适的，它们不依赖于材料是弹性的、塑性的还是黏性的。材料的特定行为（如黏弹性）是通过将应力与变形历史联系起来的 **[本构方程](@entry_id:138559) (constitutive equation)** 来引入的。

#### [热力学第二定律](@entry_id:142732)与耗散

黏弹性材料最显著的特征是能量耗散，例如，在循环加载下会产生滞回环并生热。这种不可逆过程的物理根源是热力学第二定律。对于连续介质，该定律通常以 **克劳修斯-杜恩不等式 (Clausius-Duhem inequality)** 的形式出现。

对于[等温过程](@entry_id:143096)，该不等式可以简化为一个关于机械功和能量储存的表达式。在当前构型（[欧拉描述](@entry_id:264722)）下，其局部形式为：
$$
\mathcal{D} = \boldsymbol{\sigma} : \boldsymbol{D} - \rho \dot{\psi} \geq 0
$$
其中：
- $\boldsymbol{\sigma} : \boldsymbol{D}$ 是 **[应力功率](@entry_id:182907)密度 (stress power density)**，表示单位体积[内应力](@entry_id:193721)作用于变形率所做的功的速率。注意，由于 $\boldsymbol{\sigma}$ 的对称性，$\boldsymbol{\sigma} : \boldsymbol{L} = \boldsymbol{\sigma} : (\boldsymbol{D} + \boldsymbol{W}) = \boldsymbol{\sigma} : \boldsymbol{D}$，即自旋部分不做功。
- $\psi$ 是单位质量的 **亥姆霍兹自由能 (Helmholtz free energy)**，它代表了系统中可以用来做功的“弹性”储能。$\rho \dot{\psi}$ 则是单位体积自由能的储存速率。
- $\mathcal{D}$ 是 **[耗散率](@entry_id:748577) (dissipation rate)**，即单位时间内不可逆地转化为热能的能量。

这个不等式的核心思想是：外力对材料做功的速率 ($\boldsymbol{\sigma} : \boldsymbol{D}$) 一部分以自由能的形式储存起来 ($\rho \dot{\psi}$)，另一部分则因内部摩擦等黏性效应而耗散掉 ($\mathcal{D}$)，且耗散的部分永远不能为负。对于纯弹性材料，$\mathcal{D}=0$，所有做功都可逆地储存为自由能。对于黏弹性材料，$\mathcal{D}>0$，这正是其力学行为具有历史依赖性和不[可逆性](@entry_id:143146)的[热力学](@entry_id:141121)根源。在参考构型（[拉格朗日描述](@entry_id:264498)）下，该不等式具有等价形式：
$$
\mathcal{D}_{ref} = \frac{1}{2}\boldsymbol{S}:\dot{\boldsymbol{C}} - \dot{\psi}_{ref} \ge 0
$$
其中 $\psi_{ref}$ 是单位参考体积的自由能。这个不等式是推导和检验黏弹性本构模型是否物理自洽的根本出发点。

### 本构模型构建机制

基于上述运动学和[热力学原理](@entry_id:142232)，我们可以开始构建能够描述有限应变黏弹性行为的数学模型。

#### 客观性与[客观率](@entry_id:198692)

[本构方程](@entry_id:138559)作为描述材料内在物理性质的规律，其形式不应依赖于观察者。具体来说，它不应受到观察者自身刚体运动（[平动](@entry_id:187700)和转动）的影响。满足这一要求的性质被称为 **物质客观性 (material objectivity)** 或 **标架无关性 (frame-indifference)**。

对于直接联系[应力张量和应变张量](@entry_id:755512)的[本构关系](@entry_id:186508)（如[超弹性](@entry_id:159356)模型 $S = S(C)$），客观性很容易满足，因为 $S$ 和 $C$ 都是物质张量，不受空间[刚体转动](@entry_id:191086)的影响。然而，对于黏弹性材料，本构关系通常是率相关的，即应力与变形率有关。这就带来了难题：[空间张量](@entry_id:185799)（如柯西应力 $\boldsymbol{\sigma}$ 或变形率 $\boldsymbol{D}$）的普通[物质时间导数](@entry_id:190892)（如 $\dot{\boldsymbol{\sigma}}$）并不是客观的。在叠加一个[刚体转动](@entry_id:191086)后，它会包含与观察者转动角速度相关的额外项。

为了建立客观的率型[本构方程](@entry_id:138559)，我们需要使用所谓的 **[客观应力率](@entry_id:199282) (objective stress rates)**。这些“率”通过在普通物质导数上增加一些项来抵消观察者[转动带](@entry_id:754426)来的非客观影响。常见的[客观率](@entry_id:198692)包括：

- **[Jaumann 率](@entry_id:185572)**: $\dot{\boldsymbol{\tau}}^{J} = \dot{\boldsymbol{\tau}} + \boldsymbol{\tau} \boldsymbol{W} - \boldsymbol{W} \boldsymbol{\tau}$
- **Oldroyd 上随转率 (upper-convected rate)**: $\dot{\boldsymbol{A}}^{\nabla} = \dot{\boldsymbol{A}} - \boldsymbol{L} \boldsymbol{A} - \boldsymbol{A} \boldsymbol{L}^T$
- **Truesdell 率**: $\dot{\boldsymbol{\sigma}}^{T} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma} \boldsymbol{L}^T + \mathrm{tr}(\boldsymbol{L})\,\boldsymbol{\sigma}$

可以严格证明，所有这三种率都满足客观性要求，即在叠加[刚体转动](@entry_id:191086) $\boldsymbol{Q}(t)$ 后，变换后的率 $\widetilde{\mathcal{R}[A]}$ 等于 $Q \mathcal{R}[A] Q^T$。它们之间的选择取决于具体的模型和理论背景。例如，Truesdell 率和 Oldroyd 率之间存在一个简单的关系：$J\,\dot{\boldsymbol{\sigma}}^{T} = \dot{\boldsymbol{\tau}}^{\nabla}$，其中 $\boldsymbol{\tau}$ 是[基尔霍夫应力](@entry_id:751039)。这表明，如果一个本构模型使用其中一种率是客观的，那么使用另一种率的等价形式也是客观的。

#### 从线性叠加到[准线性](@entry_id:637689)黏弹性

在小应变下，线性黏弹性理论取得了巨大成功。其核心是 **Boltzmann [叠加原理](@entry_id:144649) (Boltzmann superposition principle)**，它将当前应力表示为应变历史的[卷积积分](@entry_id:155865)：
$$
\sigma(t) = \int_0^t E(t-s) \frac{d\varepsilon}{ds} ds
$$
其中 $E(t)$ 是与应变大小无关的松弛模量。一个自然的想法是，能否将此模型直接推广到有限应变？例如，简单地将 $\varepsilon$ 替换为某个[有限应变度量](@entry_id:185716)，如工程应变 $\lambda-1$。

答案是否定的。这种直接的推广从根本上是错误的。原因在于，[非线性弹性](@entry_id:185743)材料的瞬时响应（刚度）本身就依赖于当前的变形状态。例如，对于一个 neo-Hookean 材料，在[单轴拉伸](@entry_id:188287)下，其瞬时[切线](@entry_id:268870)模量为 $\mu(2\lambda + \lambda^{-2})$，这明显是当前拉伸比 $\lambda$ 的函数。而一个固定的松弛核函数 $E(t)$ 作用于线性应变增量的模型，其瞬时响应是常数 $E(0)$，无法捕捉到这种状态依赖的刚度变化。因此，在不同预拉伸状态下施加相同的微小应变增量，该模型会预测相同的应力增量，这与实验事实相悖。

为了解决这个问题，**[准线性](@entry_id:637689)黏弹性 (Quasi-Linear Viscoelasticity, QLV)** 模型被提出。其核心思想是 **时间-应变可分离性 (time-strain separability)**。QLV 假设总应力可以表示为一个与变形历史无关的[非线性弹性](@entry_id:185743)响应 $\sigma_e(\lambda)$ 和一个只与时间相关的线性松弛函数 $g(t)$ 的卷积：
$$
\sigma(t) = \int_0^t g(t-s) \frac{d\sigma_e(\lambda(s))}{ds} ds
$$
在这个模型中，卷积作用的对象不再是应变，而是[非线性](@entry_id:637147)的“弹性应力”。这样一来，模型的瞬时响应 $\Delta\sigma = g(0) \Delta\sigma_e$ 就自然地包含了弹性响应的[非线性](@entry_id:637147)，从而能够正确地反映瞬时刚度随变形状态的变化。QLV 模型虽然仍是一个唯象近似（真实材料的时间-应变可分离性只在一定变形范围内成立），但它在描述生物组织等材料的中等有限应变行为方面非常成功和实用。

#### 基于[热力学](@entry_id:141121)的[内变量模型](@entry_id:750757)

QLV 模型虽然实用，但其唯象本质使其缺乏更深层次的物理洞察力。一个更严谨和通用的方法是基于[热力学](@entry_id:141121)和 **内变量 (internal variables)** 来构建模型。这种方法将材料的黏性行为归因于一些无法直接观测的微观结构状态（内变量）的演化。

我们可以将材料想象成一个复杂的流变网络，由代表可逆储能的“弹簧”和代表耗散的“黏壶”组成。在有限应变框架下，我们可以假设亥姆霍兹自由能 $\psi$ 不仅依赖于宏观变形（如 $\boldsymbol{C}$），还依赖于一组代表黏性分支状态的内变量张量 $\lbrace \boldsymbol{C}_v^{(k)} \rbrace$。一个典型的可分离形式是：
$$
\psi(\boldsymbol{C}, \{\boldsymbol{C}_v^{(k)}\}) = \psi_{eq}(\boldsymbol{C}) + \sum_{k=1}^N \psi_k(C, \boldsymbol{C}_v^{(k)})
$$
其中 $\psi_{eq}$ 是长期平衡（完全松弛）时的弹性[储能](@entry_id:264866)，而每个 $\psi_k$ 代表一个非平衡分支的[储能](@entry_id:264866)。

将此自由能形式代入[热力学第二定律](@entry_id:142732)的不等式 $\frac{1}{2}\boldsymbol{S}:\dot{\boldsymbol{C}} - \dot{\psi} \ge 0$ 中，并应用 Coleman-Noll 方法，我们可以系统地推导出完整的本构结构：

1.  **[应力-应变关系](@entry_id:274093)**: 总应力 $\boldsymbol{S}$ 必须是自由能对应变的[偏导数](@entry_id:146280)：
    $$
    \boldsymbol{S} = 2 \frac{\partial \psi}{\partial \boldsymbol{C}} = \underbrace{2 \frac{\partial \psi_{eq}}{\partial \boldsymbol{C}}}_{\boldsymbol{S}^{eq}} + \sum_{k=1}^N \underbrace{2 \frac{\partial \psi_k}{\partial \boldsymbol{C}}}_{\boldsymbol{S}^{(k)}}
    $$
    这表明总应力可以分解为平衡应力（[弹性网络](@entry_id:143357)）和一系列非平衡应力（黏性分支）之和。

2.  **耗散与[热力学力](@entry_id:161907)**: 不等式化简为只包含内变量演化的残余部分：
    $$
    \mathcal{D} = \sum_{k=1}^N \boldsymbol{A}^{(k)} : \frac{1}{2}\dot{\boldsymbol{C}}_v^{(k)} \ge 0
    $$
    其中 $\boldsymbol{A}^{(k)} = -2 \frac{\partial \psi_k}{\partial \boldsymbol{C}_v^{(k)}}$ 被称为 **[热力学力](@entry_id:161907) (thermodynamic force)**，它驱动着内变量 $\boldsymbol{C}_v^{(k)}$ 的演化。

3.  **演化方程**: 为了保证耗散恒为非负，我们必须为内变量设定 **[演化方程](@entry_id:268137) (evolution law)** 或动力学定律。一个通用的[线性形式](@entry_id:276136)是假设“流”（$\dot{\boldsymbol{C}}_v^{(k)}$）与“力”（$\boldsymbol{A}^{(k)}$）成正比：
    $$
    \dot{\boldsymbol{C}}_v^{(k)} = \mathbb{L}^{(k)} : \boldsymbol{A}^{(k)}
    $$
    其中 $\mathbb{L}^{(k)}$ 是一个四阶的 **迁移率张量 (mobility tensor)**。只要 $\mathbb{L}^{(k)}$ 是[对称正定](@entry_id:145886)的，耗散非负的条件就自动满足。

这种基于内变量的方法为构建复杂的、物理上自洽的有限应变黏弹性模型提供了强大而系统的框架。

#### 体积-等容响应分离

许多黏弹性材料（如橡胶和生物组织）在压缩时表现出极大的刚度，近似于不可压缩。然而，它们的剪切行为则相对柔软并表现出显著的黏弹性。为了有效模拟这类材料，将变形和响应分解为 **体积 (volumetric)** 部分和 **等容 (isochoric)** 部分是一种非常有效的策略。

运动学上，我们可以将[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}$ 唯一地分解为一个标量 $J^2 = \det \boldsymbol{C}$（代表体积变化）和一个满足 $\det \bar{\boldsymbol{C}} = 1$ 的 **等容部分 (isochoric part)** $\bar{\boldsymbol{C}}$：
$$
\bar{\boldsymbol{C}} = J^{-2/3}\boldsymbol{C}
$$
相应地，我们可以将[亥姆霍兹自由能](@entry_id:136442)也分解为体积和等容两部分的和：
$$
\psi(\boldsymbol{C}, \mathcal{Z}) = \psi_{vol}(J) + \psi_{iso}(\bar{\boldsymbol{C}}, \mathcal{Z})
$$
这里，我们将所有与黏弹性相关的内变量 $\mathcal{Z}$ 都放入等容能量项 $\psi_{iso}$ 中，而体积能量项 $\psi_{vol}$ 只依赖于 $J$。

这种分解具有深刻的物理和数学后果：

1.  **[应力分解](@entry_id:272862)**: 总应力 $S$ 也相应地分解为 $S_{vol} + S_{iso}$。其中，体积应力 $S_{vol} = 2 \partial \psi_{vol}/\partial C = J \psi_{vol}'(J) C^{-1}$，完全由[弹性势能](@entry_id:168893) $\psi_{vol}$ 决定，不含内变量，因此 **体积响应是纯弹性的**。

2.  **等容应力的性质**: 等容应力 $S_{iso} = 2 \partial \psi_{iso}/\partial C$ 具有一个关键性质：$S_{iso} : \boldsymbol{C} = 0$。这意味着当将其推前到当前构型后，对应的[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau}_{iso}$ 的迹为零（$\mathrm{tr}(\boldsymbol{\tau}_{iso}) = \boldsymbol{S}_{iso} : \boldsymbol{C} = 0$）。迹为零的张量称为 **[偏张量](@entry_id:185837) (deviatoric tensor)**。这表明，[等容变形](@entry_id:196451)只产生偏应力，这与我们对[不可压缩流体](@entry_id:181066)中压力的认识相一致。

3.  **耗散的约束**: 由于 $\psi_{vol}$ 不含内变量，所有的耗散都源于 $\psi_{iso}$ 的演化。如果我们采用内变量张量 $C_v$ 来描述黏性，那么为了保证黏性流动自身也是等容的（不产生体积耗散），我们需要对 $C_v$ 的演化施加约束，即 $\det C_v = 1$。其速率形式为 $\mathrm{tr}(\dot{\boldsymbol{C}}_v \boldsymbol{C}_v^{-1}) = 0$。

通过这种体积-等容分解的策略，我们能够构建出更符合物理实际的模型，将复杂的黏弹性效应精确地限制在材料的剪切和形状改变响应中，同时用一个简单的弹性模型来处理其体积响应。