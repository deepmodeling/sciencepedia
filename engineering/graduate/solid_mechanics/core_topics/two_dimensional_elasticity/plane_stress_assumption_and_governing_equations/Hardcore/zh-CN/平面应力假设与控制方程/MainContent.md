## 引言
在[固体力学](@entry_id:164042)领域，直接求解三维弹性问题通常面临巨大的数学挑战。因此，发展精确且高效的简化模型成为工程分析与科学研究的关键。[平面应力假设](@entry_id:184389)正是其中最重要和最广泛应用的二维模型之一，它为理解薄板状结构的核心力学行为提供了强有力的理论工具。然而，简单地将三维问题降至二维并非没有代价。深刻理解这一假设的物理基础、数学表述、适用边界及其在不同物理情境下的推论，是避免模型误用、进行精确工程设计的基石。

本文旨在系统性地构建[平面应力](@entry_id:172193)理论的知识体系。在“原理与机制”一章中，我们将深入其物理本质，从[动理学](@entry_id:136901)角度辨析其与平面应变的区别，并推导其控制方程。接下来的“应用与跨学科联系”一章将展示该理论如何在[应力集中](@entry_id:160987)、[热弹性](@entry_id:158447)、有限元分析乃至[生物力学](@entry_id:153973)等领域解决实际问题。最后，通过“动手实践”环节，读者将有机会运用所学知识解决具体的力学计算问题，从而巩固理论理解。

## 原理与机制

在三维弹性力学问题的研究中，完全的三维分析往往在数学上极为复杂。因此，在工程和科学的许多领域，发展了一系列简化模型，这些模型在特定的几何与载荷条件下能够以足够的精度捕捉系统的主要力学行为。平面应力（Plane Stress）是其中一种最基本、最重要的二维简化模型。本章将深入探讨[平面应力假设](@entry_id:184389)的物理原理、数学表述及其在不同力学框架下的应用。

### [平面应力](@entry_id:172193)：一种基于“力”的动理学假设

为了理解[平面应力假设](@entry_id:184389)的本质，我们首先必须将其与另一种常见的二维简化——[平面应变](@entry_id:167046)（Plane Strain）进行区分。这两种假设从根本上源于对不同物理量的约束。

**[平面应力](@entry_id:172193)**假设适用于几何上“薄”的板状结构。这类结构的一个维度（厚度方向，通常设为 $z$ 轴）远小于另外两个维度（平面内尺寸）。当板的两个主表面（例如 $z = \pm t/2$）不受外力作用，即无面力（traction-free）时，我们可以合理地假设在这些表面上，垂直于表面的应力分量为零。[平面应力](@entry_id:172193)模型将这一边界条件推广，**假设**在整个板的厚度范围内，所有与 $z$ 方向相关的应力分量均为零。用张量分量表示，即：
$$
\sigma_{zz} = \sigma_{xz} = \sigma_{yz} = 0
$$
由于应力是与力直接相关的物理量（动理学量，kinetic quantity），因此[平面应力假设](@entry_id:184389)是一种**动理学假设**。它直接约束了[应力张量](@entry_id:148973)的三个分量。在此假设下，[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的结构简化为：
$$
\boldsymbol{\sigma} = \begin{pmatrix} \sigma_{xx} & \sigma_{xy} & 0 \\ \sigma_{yx} & \sigma_{yy} & 0 \\ 0 & 0 & 0 \end{pmatrix}
$$
考虑到应力[张量的对称性](@entry_id:202126)（$\sigma_{xy} = \sigma_{yx}$），在一个二维问题中，我们只需要求解三个独立的应力分量：$\sigma_{xx}$、$\sigma_{yy}$ 和 $\sigma_{xy}$ 。

与此相对，**平面应变**假设适用于几何上“长”的柱状体结构（例如大坝、隧道），其几何形状、载荷和约束在长度方向（$z$ 轴）上不发生变化。在这种情况下，我们可以假设物体的变形也与 $z$ 坐标无关，并且没有沿 $z$ 方向的位移。这导致了对所有与 $z$ 方向相关的应变分量的约束：
$$
\varepsilon_{zz} = \varepsilon_{xz} = \varepsilon_{yz} = 0
$$
由于应变是描述几何变形的物理量（[运动学](@entry_id:173318)量，kinematic quantity），因此[平面应变假设](@entry_id:186003)是一种**[运动学](@entry_id:173318)假设**。

一个核心区别在于，平面应力直接约束 $\sigma_{zz}=0$，而平面应变直接约束 $\varepsilon_{zz}=0$。在每种情况下，那个“未被约束”的对应量（平面应力中的 $\varepsilon_{zz}$ 和[平面应变](@entry_id:167046)中的 $\sigma_{zz}$）通常不为零，其值由材料的本构关系（constitutive law）决定。我们将在后续章节详细探讨这一点 。

### 物理合理性：薄板的[渐近分析](@entry_id:160416)

[平面应力假设](@entry_id:184389)不仅仅是一种数学上的便利，它植根于对薄结构力学行为的深刻物理洞察。其合理性可以通过对三维平衡方程的[渐近分析](@entry_id:160416)来严格证明。

考虑一个厚度为 $t$、特征平面尺寸为 $L$ 的薄板，其中 $t \ll L$。板的上下表面 $z = \pm t/2$ 无面力作用。三维静态平衡方程（无[体力](@entry_id:174230)）为：
$$
\frac{\partial \sigma_{ij}}{\partial x_j} = 0
$$
无面力的边界条件意味着在 $z=\pm t/2$ 处，$\sigma_{xz} = \sigma_{yz} = \sigma_{zz} = 0$。

现在，我们进行一个量级分析。假设由平面[内载荷](@entry_id:195654)引起的平面内应力分量（$\sigma_{xx}, \sigma_{yy}, \sigma_{xy}$）的特征尺度为 $S$。这些应[力场](@entry_id:147325)在平面内的变化尺度为 $L$，在厚度方向的变化尺度为 $t$。
从前两个[平衡方程](@entry_id:172166)（$i=x, y$）可得 $\frac{\partial \sigma_{xz}}{\partial z} = -(\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y})$。右侧的量级为 $\mathcal{O}(S/L)$。将此式沿厚度方向从 $-t/2$ 积分到 $z$，并利用边界条件 $\sigma_{xz}(z=-t/2)=0$，可以估计出横向[剪切应力](@entry_id:137139) $\sigma_{xz}$ 的量级为 $\mathcal{O}(t \cdot S/L)$。同理，$\sigma_{yz} \sim \mathcal{O}(S \cdot t/L)$。

接着，考察第三个[平衡方程](@entry_id:172166)：$\frac{\partial \sigma_{zz}}{\partial z} = -(\frac{\partial \sigma_{xz}}{\partial x} + \frac{\partial \sigma_{yz}}{\partial y})$。右侧的量级为 $\mathcal{O}((S \cdot t/L)/L) = \mathcal{O}(S \cdot t/L^2)$。再次沿厚度方向积分，并利用边界条件 $\sigma_{zz}(z=-t/2)=0$，我们发现横向[正应力](@entry_id:260622) $\sigma_{zz}$ 的量级为 $\mathcal{O}(t \cdot S \cdot t/L^2) = \mathcal{O}(S \cdot (t/L)^2)$。

因此，当 $t/L \to 0$ 时，我们有：
$$
\frac{\sigma_{xz}}{S}, \frac{\sigma_{yz}}{S} \sim \mathcal{O}\left(\frac{t}{L}\right) \to 0
$$
$$
\frac{\sigma_{zz}}{S} \sim \mathcal{O}\left(\left(\frac{t}{L}\right)^2\right) \to 0
$$
这个分析清晰地表明，对于薄板结构，在远离[边缘效应](@entry_id:183162)的内部区域，横向应力分量与平面[内应力](@entry_id:193721)分量相比是高阶小量，可以忽略不计。这为[平面应力假设](@entry_id:184389) $\sigma_{zz} = \sigma_{xz} = \sigma_{yz} = 0$ 提供了坚实的理论基础 。

至关重要的是，上述推导仅依赖于[平衡方程](@entry_id:172166)和几何形状，完全不涉及材料的[本构关系](@entry_id:186508)。这意味着[平面应力](@entry_id:172193)作为一个应力状态的近似，其有效性不局限于线弹性或小应变理论。只要板是薄的且横向载荷可以忽略，即使材料表现出[非线性](@entry_id:637147)、塑性或经历有限变形，其内部的应力状态在主导阶上仍然是[平面应力](@entry_id:172193)状态。这是一个深刻的结论，凸显了该假设的广泛适用性 。

### [运动学](@entry_id:173318)与本构的推论

在确立了[平面应力](@entry_id:172193)状态的定义和合理性之后，我们来探讨它对物体变形（运动学）和[应力-应变关系](@entry_id:274093)（本构）所带来的影响。

#### 平面内应变与平面外应变

平面应力模型通常用于分析由平面[内载荷](@entry_id:195654)引起的平面内变形。假设[位移场](@entry_id:141476)的主要分量是平面内的 $u(x,y)$ 和 $v(x,y)$。在小应变理论中，平面内应变分量由位移的平面内梯度决定：
$$
\varepsilon_{xx} = \frac{\partial u}{\partial x}, \quad \varepsilon_{yy} = \frac{\partial v}{\partial y}, \quad \gamma_{xy} = 2\varepsilon_{xy} = \frac{\partial u}{\partial y} + \frac{\partial v}{\partial x}
$$
其中 $\gamma_{xy}$ 是工程[剪应变](@entry_id:175241) 。

然而，[平面应力假设](@entry_id:184389) $\sigma_{zz}=0$ 并不意味着平面外应变 $\varepsilon_{zz}$ 也为零。恰恰相反，$\varepsilon_{zz}$ 的值是由[本构关系](@entry_id:186508)决定的一个重要结果。对于线弹性[各向同性材料](@entry_id:170678)，三维胡克定律中[正应变](@entry_id:204633)与应力的关系为：
$$
\varepsilon_{zz} = \frac{1}{E} \left[ \sigma_{zz} - \nu (\sigma_{xx} + \sigma_{yy}) \right]
$$
其中 $E$ 是杨氏模量，$\nu$ 是[泊松比](@entry_id:158876)。将[平面应力条件](@entry_id:168184) $\sigma_{zz}=0$ 代入上式，我们得到：
$$
\varepsilon_{zz} = -\frac{\nu}{E} (\sigma_{xx} + \sigma_{yy})
$$
这个非零的 $\varepsilon_{zz}$ 正是著名的**泊松效应**（Poisson's effect）的体现：当板在平面内被拉伸时（$\sigma_{xx} + \sigma_{yy} > 0$），它会在厚度方向上收缩（$\varepsilon_{zz} < 0$），反之亦然。因此，在[平面应力](@entry_id:172193)模型中，$\varepsilon_{zz}$ 是一个由平面[内应力](@entry_id:193721)状态决定的从动量，不能预先设定为零 。

我们还可以将 $\varepsilon_{zz}$ 完全用平面内应变来表示。通过求解平面应力下的二维本构关系，可以得到 $\sigma_{xx} + \sigma_{yy} = \frac{E}{1-\nu}(\varepsilon_{xx} + \varepsilon_{yy})$。将其代入 $\varepsilon_{zz}$ 的表达式，可得：
$$
\varepsilon_{zz} = -\frac{\nu}{1-\nu} (\varepsilon_{xx} + \varepsilon_{yy})
$$
这个关系在求解具体问题时非常有用。例如，考虑一个由[位移场](@entry_id:141476) $u(x,y) = 0.08x^2y - 0.03y^3 + 0.05x$ 和 $v(x,y) = -0.06xy^2 + 0.04x^3 - 0.02y$ 描述的变形。我们可以首先通过求导计算出任意点的平面内应变 $\varepsilon_{xx}$ 和 $\varepsilon_{yy}$，然后利用上述公式和给定的[泊松比](@entry_id:158876) $\nu$，直接计算出该点的平面外应变 $\varepsilon_{zz}$，而无需先求解应力 。

#### [各向异性材料](@entry_id:184874)的影响

当材料是各向异性时，例如[正交各向异性材料](@entry_id:190111)，其[本构关系](@entry_id:186508)更为复杂。若材料[主轴](@entry_id:172691)与坐标轴对齐，$\varepsilon_{zz}$ 的表达式为：
$$
\varepsilon_{zz} = -\frac{\nu_{zx}}{E_z}\sigma_{xx} - \frac{\nu_{zy}}{E_z}\sigma_{yy}
$$
其中 $E_z$ 是厚度方向的[杨氏模量](@entry_id:140430)，$\nu_{zx}$ 和 $\nu_{zy}$ 是描述平面内应力引起平面外应变的泊松比。有趣的是，即便在厚度方向刚度极大的情况下（$E_z \gg E_x, E_y$），只要板足够薄，[平面应力](@entry_id:172193)的**应力假设**（$\sigma_{zz} \approx 0$）依然成立。其后果是，为了维持 $\sigma_{zz} \approx 0$，变形场必须做出调整。由上式可知，对于给定的平面内应力，当 $E_z \to \infty$ 时，$\varepsilon_{zz} \to 0$。这意味着，一个在厚度方向上非常刚硬的薄板，在[平面应力](@entry_id:172193)状态下，其行为会自然地趋近于[平面应变](@entry_id:167046)状态的运动学约束。这是几何与材料特性相互作用的一个精妙体现 。

### 控制方程与求解框架

将[平面应力假设](@entry_id:184389)与平衡方程、本构关系及[运动学](@entry_id:173318)关系相结合，我们可以构建起一套完整的二维控制方程体系。根据求解策略的不同，可以形成多种等价的数学提法。

#### 二维[平衡方程](@entry_id:172166)与本构关系

将三维平衡方程沿厚度方向积分，并使用厚度[平均应力](@entry_id:751819) $\bar{\sigma}_{ij} = \frac{1}{t}\int_{-t/2}^{t/2} \sigma_{ij} dz$，可以得到二维平衡方程（以[体力](@entry_id:174230) $\mathbf{b}$ 为例）：
$$
\frac{\partial \bar{\sigma}_{xx}}{\partial x} + \frac{\partial \bar{\sigma}_{xy}}{\partial y} + \bar{b}_x = 0
$$
$$
\frac{\partial \bar{\sigma}_{xy}}{\partial x} + \frac{\partial \bar{\sigma}_{yy}}{\partial y} + \bar{b}_y = 0
$$
这些方程构成了求解三个未知平均应力分量的两个[偏微分方程](@entry_id:141332) 。

为了封闭[方程组](@entry_id:193238)，我们需要二维的[本构关系](@entry_id:186508)。通过在三维[胡克定律](@entry_id:149682)中设 $\sigma_{zz}=0$ 并整理，可以得到平面应力下的[应力-应变关系](@entry_id:274093)。用矩阵形式（[Voigt表示法](@entry_id:166691)）书写，$\boldsymbol{\sigma} = \mathbf{D}_{ps} \boldsymbol{\varepsilon}$，其中 $\boldsymbol{\sigma} = [\sigma_{xx}, \sigma_{yy}, \tau_{xy}]^T$，$\boldsymbol{\varepsilon} = [\varepsilon_{xx}, \varepsilon_{yy}, \gamma_{xy}]^T$，$\tau_{xy}=\sigma_{xy}$。对于[各向同性材料](@entry_id:170678)，[平面应力本构矩阵](@entry_id:172920) $\mathbf{D}_{ps}$ 为：
$$
\mathbf{D}_{ps} = \frac{E}{1-\nu^2} \begin{pmatrix} 1 & \nu & 0 \\ \nu & 1 & 0 \\ 0 & 0 & \frac{1-\nu}{2} \end{pmatrix}
$$
这个矩阵是后续位移法和[能量法](@entry_id:183021)分析的基石 。

#### 位移法：Navier方程

将本构关系代入平衡方程，再将[运动学](@entry_id:173318)关系代入，最终可以得到一组只包含位移分量 $u$ 和 $v$ 的控制方程，即**Navier方程**。对于无体力的[平面应力](@entry_id:172193)问题，其形式为：
$$
\mu \nabla^2 \mathbf{u} + (\lambda_{\mathrm{ps}} + \mu) \nabla(\nabla \cdot \mathbf{u}) = \mathbf{0}
$$
其中 $\mathbf{u}=(u,v)$，$\mu = G$ 是[剪切模量](@entry_id:167228)，而 $\lambda_{\mathrm{ps}} = \frac{2\mu\nu}{1-\nu} = \frac{E\nu}{1-\nu^2}$ 是平面应力下的有效拉梅常数。这是一个[二阶偏微分方程](@entry_id:175326)组，配合位移或力的边界条件即可求解 。

#### 应力法：[Airy应力函数](@entry_id:191331)

对于无体力（或保守[体力](@entry_id:174230)）的问题，可以引入一个标量函数 $\phi(x,y)$，称为**[Airy应力函数](@entry_id:191331)**，使得应力分量自动满足平衡方程：
$$
\sigma_{xx} = \frac{\partial^2 \phi}{\partial y^2}, \quad \sigma_{yy} = \frac{\partial^2 \phi}{\partial x^2}, \quad \sigma_{xy} = -\frac{\partial^2 \phi}{\partial x \partial y}
$$
这样，[平衡方程](@entry_id:172166)得到了恒等满足。接下来，需要满足的是应变协调条件（compatibility condition），即应变场必须能积分得到一个单值的连续位移场。对于二维问题，协调条件为 $\frac{\partial^2 \varepsilon_{xx}}{\partial y^2} + \frac{\partial^2 \varepsilon_{yy}}{\partial x^2} = \frac{\partial^2 \gamma_{xy}}{\partial x \partial y}$。将用 $\phi$ 表示的应力代入[本构关系](@entry_id:186508)，再代入协调条件，对于[各向同性材料](@entry_id:170678)，可以推导出 Airy 应力函数必须满足著名的**[双调和方程](@entry_id:165706)**（biharmonic equation）：
$$
\nabla^4 \phi = \frac{\partial^4 \phi}{\partial x^4} + 2\frac{\partial^4 \phi}{\partial x^2 \partial y^2} + \frac{\partial^4 \phi}{\partial y^4} = 0
$$
问题的求解转化为求解一个[四阶偏微分方程](@entry_id:176247)。此方法在解析求解中威力巨大。值得注意的是，能产生同一应[力场](@entry_id:147325)的 Airy 应力函数不是唯一的，它们可以相差一个关于 $x,y$ 的任意线性多项式，这不影响应力的计算结果 。

#### [能量法](@entry_id:183021)：势能原理

[变分原理](@entry_id:198028)，特别是**[最小势能原理](@entry_id:173340)**，为弹性力学问题提供了另一种强大的求解途径，并且是[有限元法](@entry_id:749389)的理论基础。该原理指出，在所有满足[位移边界条件](@entry_id:203261)的变形状态中，真实的平衡状态是使系统总[势能](@entry_id:748988) $\Pi$ 取驻（对于稳定平衡为极小）的那一个。

对于平面应力问题，总势能泛函 $\Pi$ 由两部分组成：内部应变能 $U$ 和外力[势能](@entry_id:748988) $V$。
$$
\Pi[u,v] = U + V = \int_{\Omega} \frac{1}{2} \boldsymbol{\varepsilon}^T \mathbf{D}_{ps} \boldsymbol{\varepsilon} \,dA - \int_{\Omega} \mathbf{b} \cdot \mathbf{u} \,dA - \int_{\Gamma_t} \bar{\mathbf{t}} \cdot \mathbf{u} \,ds
$$
这里，第一项是积分在整个区域 $\Omega$ 上的[应变能密度](@entry_id:200085)；第二项是[体力](@entry_id:174230) $\mathbf{b}$ 所做的功的负值；第三项是作用在边界 $\Gamma_t$ 上的给定面力 $\bar{\mathbf{t}}$ 所做的功的负值。对该泛函求变分并使其等于零（$\delta\Pi=0$），得到的结果与Navier方程和自然边界条件（力的边界条件）完[全等](@entry_id:273198)价 。

### 模型的局限性：翘曲效应

经典的（或称“膜式”）[平面应力](@entry_id:172193)理论建立在一个隐含的运动学假设之上：平面内位移 $u$ 和 $v$ 不随厚度坐标 $z$ 变化，即 $u=u(x,y), v=v(x,y)$。然而，三维弹性理论的严格分析表明，这个假设仅在非常特殊的情况下才与物理现实完全相符。

我们已经知道，平面应力状态下会产生平面外应变 $\varepsilon_{zz} = -\frac{\nu}{E}(\sigma_{xx}+\sigma_{yy})$。如果平面[内应力](@entry_id:193721)在 $(x,y)$ 平面上不是[均匀分布](@entry_id:194597)的，那么 $\varepsilon_{zz}$ 也将是 $(x,y)$ 的函数。现在，我们考察横向[剪应变](@entry_id:175241)与位移的关系：
$$
\gamma_{zx} = \frac{\partial u}{\partial z} + \frac{\partial w}{\partial x}
$$
其中 $w$ 是横向位移。对 $\varepsilon_{zz} = \partial w / \partial z$ 积分可得 $w(x,y,z) = z \cdot \varepsilon_{zz}(x,y) + w_0(x,y)$。代入上式，得到：
$$
\gamma_{zx} = \frac{\partial u}{\partial z} + z\frac{\partial \varepsilon_{zz}}{\partial x} + \frac{\partial w_0}{\partial x}
$$
由于[平面应力假设](@entry_id:184389) $\sigma_{xz}=0$，从而 $\gamma_{zx}=0$。这意味着：
$$
\frac{\partial u}{\partial z} = -z\frac{\partial \varepsilon_{zz}}{\partial x} - \frac{\partial w_0}{\partial x}
$$
这个结果表明，只要 $\varepsilon_{zz}$ 在平面内有梯度（即 $\partial \varepsilon_{zz}/\partial x \neq 0$），那么位移 $u$ 就必须是 $z$ 的函数，即 $\partial u/\partial z \neq 0$。这意味着原本垂直于中面的直线（法线）在变形后不再保持为直线，这种现象称为**翘曲**（warping）。

只有当平面内应力[均匀分布](@entry_id:194597)时，$\varepsilon_{zz}$ 才是一个常数，其梯度为零，此时 $\partial u/\partial z$ 可以为零，经典[平面应力](@entry_id:172193)模型的运动学假设才被严格满足。在应力梯度显著的区域，例如孔边或集中载荷附近，$\varepsilon_{zz}$ 的梯度很大，翘曲效应会非常显著 。

量级分析表明，翘曲引起的位移变化与板的厚度-长度比的平方成正比，即 $\Delta u_{\text{warp}}/U \sim \nu(t/L)^2$。这解释了为何对于薄板（$t/L \ll 1$），这种效应通常可以忽略；但对于厚板，或者在[应力集中](@entry_id:160987)区域（局部[特征长度](@entry_id:265857) $L$ 与厚度 $t$ 相当），翘曲效应变得不可忽视。在这些情况下，需要采用更高级的板壳理论（如考虑[横向剪切变形](@entry_id:176673)的[Reissner-Mindlin理论](@entry_id:174798)）或直接进行三维分析才能准确捕捉结构的力学行为 。

综上所述，平面应力模型是分析薄板结构平面内行为的强大工具，但理解其假设的来源、推论的细节以及应用的边界，对于深刻掌握固体力学和进行精确的工程分析至关重要。