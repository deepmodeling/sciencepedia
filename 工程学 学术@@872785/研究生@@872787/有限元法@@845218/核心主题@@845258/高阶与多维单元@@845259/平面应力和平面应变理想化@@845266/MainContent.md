## 引言
在工程与[科学计算](@entry_id:143987)领域，将复杂的三维（3D）结构力学问题简化为更易于管理的二维（2D）模型，是一项节省计算资源并深化物理洞察的关键技术。然而，这种[降维](@entry_id:142982)并非随意为之，它依赖于对结构几何、载荷与约束条件的深刻理解。[平面应力与平面应变](@entry_id:172357)正是实现这一简化的两种最基本且最强大的理想化模型，但何时以及如何正确应用它们，是工程师和分析师面临的核心挑战。本文旨在系统性地解决这一问题，为读者构建一个从理论基础到实际应用的完整知识框架。

在接下来的内容中，我们将分三步深入探讨：首先，在“原理与机制”章节中，我们将从第一性原理出发，剖析[平面应力与平面应变](@entry_id:172357)的物理假设、数学推导和[本构关系](@entry_id:186508)。接着，在“应用与跨学科联系”章节中，我们将通过丰富的实例，展示这些模型在土木、机械、断裂力学等领域的实际应用和关键作用。最后，通过“动手实践”环节，读者将有机会通过解决具体问题来巩固所学知识，将理论真正内化为解决实际问题的能力。

## 原理与机制

在[连续介质力学](@entry_id:155125)和[有限元分析](@entry_id:138109)中，将复杂的三维（3D）问题简化为更易于处理的二维（2D）模型是一种至关重要的工程与科学实践。这种[降维](@entry_id:142982)不仅可以大幅减少计算成本，还能使我们更清晰地洞察问题的物理本质。然而，这种简化并非任意为之，它必须基于对结构几何、载荷条件和约束的严格物理判断。本章将深入探讨两种最基本且应用最广泛的二维理想化模型：**平面应力**（**plane stress**）和**平面应变**（**plane strain**）。我们将从第一性原理出发，阐明这两种模型的物理基础、数学推导及其在有限元方法中的具体应用和影响。

### 概念基础：二维理想化的基本原理

三维弹性体中的[应力与应变](@entry_id:137374)状态通常由一个包含六个独立分量的[对称张量](@entry_id:148092)描述。直接求解这样的三维问题往往代价高昂。幸运的是，许多工程结构由于其特定的几何形态，其力学行为在本质上是二维的。二维理想化的核心思想，正是识别并利用这些几何特征来简化控制方程。

关键在于“特征尺度”的对比。我们通常关心两个尺度：一个是在我们感兴趣的平面（通常是 $xy$ 平面）内的**[特征长度](@entry_id:265857)** $L$，例如孔的直径或载荷变化的波长；另一个是垂直于该平面的**离面尺度**。根据离面尺度与面内特征长度 $L$ 的相对大小，我们可以区分两种典型的几何原型 [@problem_id:2588311]：

1.  **薄体结构**：例如薄板或薄壳，其厚度 $t$ 远小于面内特征长度 $L$，即 $t/L \ll 1$。在这种情况下，物体在厚度方向上的力学约束较弱。

2.  **长体结构**：例如长坝、隧道或长轴，其沿某一方向（$z$ 轴）的长度 $L_z$ 远大于[横截面](@entry_id:154995)的特征尺寸 $L$，即 $L_z/L \gg 1$。在这种情况下，物体在该长方向上的变形受到强烈的几何约束。

这两种几何原型分别对应着平面应力和平面应变这两种理想化模型。理解它们各自成立的物理前提是正确应用二维分析的关键。

### 平面应力：“薄体”理想化

**平面应力**是一种适用于分析薄体结构的理想化模型。其核心假设源于一个基于**应力（或力）的边界条件**，因此，它本质上是一种**基于力的约束**（traction-based constraint）[@problem_id:2588310]。

#### 物理原理与推导

考虑一个在 $z$ 方向厚度为 $h$ 的薄板，其上下表面位于 $z = \pm h/2$。当此薄板的面内特征尺寸 $L$ 远大于其厚度 $h$（即 $h \ll L$）时，我们可以进行如下分析。通常情况下，薄板的上下两个大表面是**无约束**且**无载荷**的，即它们是**自由表面**（traction-free surfaces）。根据柯西应力公式 $\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma}\mathbf{n}$，其中 $\mathbf{t}$ 是面力向量，$\mathbf{n}$ 是表面的外法向单位向量，$\boldsymbol{\sigma}$ 是柯西应力张量。

对于 $z = +h/2$ 的上表面，其外法向为 $\mathbf{n} = \mathbf{e}_z$。无面力条件 $\mathbf{t} = \mathbf{0}$ 意味着：
$$
\begin{pmatrix} \sigma_{xz} \\ \sigma_{yz} \\ \sigma_{zz} \end{pmatrix} = \begin{pmatrix} \sigma_{xx} & \sigma_{xy} & \sigma_{xz} \\ \sigma_{yx} & \sigma_{yy} & \sigma_{yz} \\ \sigma_{zx} & \sigma_{zy} & \sigma_{zz} \end{pmatrix} \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \\ 0 \end{pmatrix}
$$
这直接给出了在 $z = \pm h/2$ 这两个表面上，离面应力分量必须为零的精确边界条件：
$$
\sigma_{xz}(x, y, \pm h/2) = 0, \quad \sigma_{yz}(x, y, \pm h/2) = 0, \quad \sigma_{zz}(x, y, \pm h/2) = 0
$$

现在，我们考虑这些应力分量在薄板内部（即 $-h/2  z  h/2$ 的区域）的行为。在没有[体力](@entry_id:174230)的情况下，平衡方程 $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$ 的分量形式为：
$$
\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} + \frac{\partial \sigma_{xz}}{\partial z} = 0 \\
\frac{\partial \sigma_{yx}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} + \frac{\partial \sigma_{yz}}{\partial z} = 0 \\
\frac{\partial \sigma_{zx}}{\partial x} + \frac{\partial \sigma_{zy}}{\partial y} + \frac{\partial \sigma_{zz}}{\partial z} = 0
$$
由于薄板的厚度 $h$ 非常小，且 $\sigma_{xz}$ 与 $\sigma_{yz}$ 在上下表面均为零，我们可以合理地假设它们在整个厚度范围内都非常小。更严谨地，通过量级分析可以表明，横向剪应力 $\sigma_{xz}$ 和 $\sigma_{yz}$ 的量级为 $O(h/L)$，而横向[正应力](@entry_id:260622) $\sigma_{zz}$ 的量级为 $O((h/L)^2)$ [@problem_id:2588315]。既然 $h/L \ll 1$，将这些小的离面应力分量近似为零是合理的。

因此，**[平面应力](@entry_id:172193)理想化**的核心假设是，在整个物体中，所有离面应力分量均为零：
$$
\sigma_{zz} = \sigma_{xz} = \sigma_{yz} = 0
$$
这样，三维应力状态就简化为了一个仅由面内分量 $\sigma_{xx}$、$\sigma_{yy}$ 和 $\tau_{xy}$（即 $\sigma_{xy}$）描述的二维状态。

#### 泊松效应的体现

一个常见的误解是，既然离面应力为零，离面应变也应为零。然而，事实并非如此。根据[广义胡克定律](@entry_id:203555)，[法向应变](@entry_id:204633) $\varepsilon_{zz}$ 与所有法向应力相关：
$$
\varepsilon_{zz} = \frac{1}{E} [ \sigma_{zz} - \nu (\sigma_{xx} + \sigma_{yy}) ]
$$
在[平面应力条件](@entry_id:168184)下，我们令 $\sigma_{zz} = 0$，上式变为：
$$
\varepsilon_{zz} = -\frac{\nu}{E}(\sigma_{xx} + \sigma_{yy})
$$
由于面内应力 $\sigma_{xx}$ 和 $\sigma_{yy}$ 通常不为零，所以 $\varepsilon_{zz}$ 也通常不为零 [@problem_id:2588352]。这体现了**泊松效应**（Poisson's effect）：当薄板在面内被拉伸时（$\sigma_{xx} + \sigma_{yy} > 0$），它会在厚度方向上收缩（$\varepsilon_{zz}  0$），反之亦然。因此，平面应力状态并不意味着[平面应变](@entry_id:167046)。

### 平面应变：“长体”理想化

与平面应力相反，**[平面应变](@entry_id:167046)**是一种适用于分析长体结构的理想化模型。其核心假设源于一个**位移（或几何）的约束**，因此，它本质上是一种**基于位移的约束**（displacement-based constraint）[@problem_id:2588310]。

#### 物理原理与推导

考虑一个沿 $z$ 轴方向很长的棱柱体结构，例如水坝、隧道或挡土墙。其[横截面](@entry_id:154995)几何形状以及所受载荷在 $z$ 轴方向上保持不变或变化非常缓慢。此外，该结构在 $z$ 方向的运动受到严格限制，例如被两端的刚性墙体夹住，或者因为结构本身非常长，根据[圣维南原理](@entry_id:165302)（Saint-Venant's principle），远离两端加载区域的中间部分的变形将趋于与 $z$ 无关 [@problem_id:2588408]。

这些物理情况启发我们做出一个**运动学假设**（kinematic assumption）：物体的变形完全发生在 $xy$ 平面内，且这种变形在沿 $z$ 轴的任何[横截面](@entry_id:154995)上都是相同的。数学上，这意味着[位移场](@entry_id:141476)具有以下形式：
$$
u = u(x,y), \quad v = v(x,y), \quad w = \text{constant}
$$
通常，我们可以通过选择合适的参考[坐标系](@entry_id:156346)令常数 $w$ 为零。从能量最小化原理的角度看，任何偏离此状态的变形，如[横截面](@entry_id:154995)的翘曲（$w$ 依赖于 $x,y$）或沿 $z$ 轴的变化，都会引入额外的应变能，而在没有相应外力做功的情况下，系统会自然趋向于能量最低的、无翘曲的二维变形状态 [@problem_id:2588408]。

基于这个[运动学](@entry_id:173318)假设，我们可以立即检视其对应变场的影响。根据[应变-位移关系](@entry_id:173321) $\varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})$：
$$
\varepsilon_{zz} = \frac{\partial w}{\partial z} = 0 \\
\gamma_{xz} = 2\varepsilon_{xz} = \frac{\partial u}{\partial z} + \frac{\partial w}{\partial x} = 0 + 0 = 0 \\
\gamma_{yz} = 2\varepsilon_{yz} = \frac{\partial v}{\partial z} + \frac{\partial w}{\partial y} = 0 + 0 = 0
$$
因此，**[平面应变](@entry_id:167046)理想化**的核心假设是，在整个物体中，所有离面应变分量均为零：
$$
\varepsilon_{zz} = \gamma_{xz} = \gamma_{yz} = 0
$$
这样，三维应变状态就简化为了一个仅由面内分量 $\varepsilon_{xx}$、$\varepsilon_{yy}$ 和 $\gamma_{xy}$ 描述的二维状态。

#### [泊松效应](@entry_id:158876)的体现

同样地，离面应变为零并不意味着离面应力为零。我们再次考察法向[应力-应变关系](@entry_id:274093)：
$$
\sigma_{zz} = \lambda(\varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz}) + 2\mu\varepsilon_{zz}
$$
其中 $\lambda$ 和 $\mu$ 是拉梅常数（Lamé parameters）。在[平面应变](@entry_id:167046)条件下，我们令 $\varepsilon_{zz} = 0$，上式变为：
$$
\sigma_{zz} = \lambda(\varepsilon_{xx} + \varepsilon_{yy})
$$
用更常见的弹性模量 $E$ 和[泊松比](@entry_id:158876) $\nu$ 表示，这等价于：
$$
\sigma_{zz} = \nu(\sigma_{xx} + \sigma_{yy})
$$
由于面内应变 $\varepsilon_{xx}$ 和 $\varepsilon_{yy}$ 通常不为零，所以 $\sigma_{zz}$ 也通常不为零 [@problem_id:2588352]。这个 $\sigma_{zz}$ 是一个**反力应力**，它的存在是为了抵抗材料因[泊松效应](@entry_id:158876)而产生的沿 $z$ 轴变形的趋势，从而强制维持 $\varepsilon_{zz}=0$ 的运动学约束。

### 二维[本构矩阵](@entry_id:164908)的推导

为了在有限元分析中实施[平面应力](@entry_id:172193)或[平面应变](@entry_id:167046)模型，我们需要推导相应的二维本构关系，即连接面内应力向量 $\{\sigma_{xx}, \sigma_{yy}, \tau_{xy}\}^{\mathsf{T}}$ 和面内应变向量 $\{\varepsilon_{xx}, \varepsilon_{yy}, \gamma_{xy}\}^{\mathsf{T}}$ 的 $3 \times 3$ [本构矩阵](@entry_id:164908) $\mathbf{D}$。这个过程清晰地展示了两种理想化在数学上的根本区别 [@problem_id:2588334]。

#### [平面应力本构矩阵](@entry_id:172920) ($D^{ps}$)

我们从三维胡克定律的应变-应力形式入手，并应用[平面应力条件](@entry_id:168184) $\sigma_{zz} = 0$：
$$
\varepsilon_{xx} = \frac{1}{E}(\sigma_{xx} - \nu\sigma_{yy}) \\
\varepsilon_{yy} = \frac{1}{E}(\sigma_{yy} - \nu\sigma_{xx})
$$
这是一个关于 $\sigma_{xx}$ 和 $\sigma_{yy}$ 的线性方程组。通过求解这个[方程组](@entry_id:193238)，我们可以反向得到应力关于应变的表达式。同时，剪切关系保持不变：$\tau_{xy} = G\gamma_{xy} = \frac{E}{2(1+\nu)}\gamma_{xy}$。

这个代数消去过程（本质上是[静态凝聚](@entry_id:176722)或[舒尔补](@entry_id:142780)）体现了[泊松效应](@entry_id:158876)的耦合 [@problem_id:2588352]。最终得到的平面应力本构关系为 [@problem_id:2588399]：
$$
\begin{pmatrix} \sigma_{xx} \\ \sigma_{yy} \\ \tau_{xy} \end{pmatrix} = \mathbf{D}^{ps} \begin{pmatrix} \varepsilon_{xx} \\ \varepsilon_{yy} \\ \gamma_{xy} \end{pmatrix}
$$
其中，[平面应力本构矩阵](@entry_id:172920) $\mathbf{D}^{ps}$ 为：
$$
\mathbf{D}^{ps} = \frac{E}{1-\nu^2} \begin{pmatrix} 1  \nu  0 \\ \nu  1  0 \\ 0  0  \frac{1-\nu}{2} \end{pmatrix}
$$

#### [平面应变本构矩阵](@entry_id:176145) ($D^{pe}$)

推导[平面应变](@entry_id:167046)矩阵则更为直接。我们从三维胡克定律的应力-应变形式入手，并直接应用[平面应变](@entry_id:167046)条件 $\varepsilon_{zz}=0, \gamma_{xz}=0, \gamma_{yz}=0$。
$$
\sigma_{xx} = \lambda(\varepsilon_{xx} + \varepsilon_{yy}) + 2\mu\varepsilon_{xx} \\
\sigma_{yy} = \lambda(\varepsilon_{xx} + \varepsilon_{yy}) + 2\mu\varepsilon_{yy} \\
\tau_{xy} = \mu\gamma_{xy}
$$
将拉梅常数用 $E$ 和 $\nu$ 替换，并整理成矩阵形式，即可得到[平面应变](@entry_id:167046)本构关系 [@problem_id:2588318]：
$$
\begin{pmatrix} \sigma_{xx} \\ \sigma_{yy} \\ \tau_{xy} \end{pmatrix} = \mathbf{D}^{pe} \begin{pmatrix} \varepsilon_{xx} \\ \varepsilon_{yy} \\ \gamma_{xy} \end{pmatrix}
$$
其中，[平面应变本构矩阵](@entry_id:176145) $\mathbf{D}^{pe}$ 为：
$$
\mathbf{D}^{pe} = \frac{E}{(1+\nu)(1-2\nu)} \begin{pmatrix} 1-\nu  \nu  0 \\ \nu  1-\nu  0 \\ 0  0  \frac{1-2\nu}{2} \end{pmatrix}
$$

#### 模型对比总结

下表总结了平面应力、平面应变以及另一种常见的二维理想化——**[轴对称](@entry_id:173333)**（**axisymmetric**）模型的关键特征，以作对比 [@problem_id:2588325]。[轴对称](@entry_id:173333)模型适用于几何、载荷和约束都围绕一个轴线旋转对称的物体，其分析在 $(r, z)$ 平面内进行，但必须考虑环向（hoop）应力 $\sigma_{\theta}$ 和应变 $\varepsilon_{\theta} = u_r/r$ 的影响。

| 特征 | [平面应力](@entry_id:172193) | [平面应变](@entry_id:167046) | 轴对称 |
| :--- | :--- | :--- | :--- |
| **适用几何** | 薄板（$h \ll L$） | 长棱柱体（$L_z \gg L$） | 旋转体 |
| **[坐标系](@entry_id:156346)** | 笛卡尔 $(x,y)$ | 笛卡尔 $(x,y)$ | 柱坐标 $(r,z)$ |
| **核心假设** | $\sigma_{zz}, \sigma_{xz}, \sigma_{yz} = 0$ | $\varepsilon_{zz}, \gamma_{xz}, \gamma_{yz} = 0$ | 对 $\theta$ 轴对称, $u_{\theta}=0$ |
| **离面分量** | $\varepsilon_{zz} \neq 0$ | $\sigma_{zz} \neq 0$ | $\sigma_{\theta}, \varepsilon_{\theta} \neq 0$ |
| **[本构矩阵](@entry_id:164908)** | $\mathbf{D}^{ps}$ | $\mathbf{D}^{pe}$ | $\mathbf{D}^{axi}$ (4x4) |

### 进阶主题：不可压缩性与[体积锁定](@entry_id:172606)

在处理橡胶等近乎不可压缩的材料时，泊松比 $\nu$ 趋近于 $0.5$。这个极限情况对平面应力和[平面应变](@entry_id:167046)模型，尤其是在[有限元分析](@entry_id:138109)中，有着截然不同的影响 [@problem_id:2588362]。

#### 不可压缩极限下的本构行为

当 $\nu \to 0.5$ 时，材料的体积几乎不可压缩，这要求[体积应变](@entry_id:267252) $\mathrm{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{xx}+\varepsilon_{yy}+\varepsilon_{zz} \approx 0$。我们来考察两种二维模型的[本构矩阵](@entry_id:164908)在该极限下的行为：

-   **平面应力**：当 $\nu \to 0.5$ 时，分母 $1-\nu^2 \to 0.75$，整个 $\mathbf{D}^{ps}$ 矩阵的系数保持有界。物理上，这是因为薄板可以通过改变其厚度（即产生一个非零的 $\varepsilon_{zz}$）来自由满足体积不变的约束，因此面内响应不会变得无限刚硬。

-   **[平面应变](@entry_id:167046)**：当 $\nu \to 0.5$ 时，分母 $(1-2\nu) \to 0$，导致 $\mathbf{D}^{pe}$ 矩阵的所有法向应力相关项的系数都趋向于无穷大。通过[特征值分析](@entry_id:273168)可以发现，对应于面[内体](@entry_id:170034)积变形（膨胀/收缩）模式的[特征值](@entry_id:154894)会趋于无穷，而对应于剪切（形状改变）变形模式的[特征值](@entry_id:154894)则保持有界。这意味着在平面应变模型中，任何试图改变面内面积的变形都会受到无限大的刚度惩罚。

#### [体积锁定](@entry_id:172606)（Volumetric Locking）

这种在不可压缩极限下[平面应变](@entry_id:167046)模型中出现的无限刚度，是导致低阶位移[协调元](@entry_id:178102)（如四节点四边形元）产生**[体积锁定](@entry_id:172606)**现象的根源。

在[有限元离散化](@entry_id:193156)中，单元的位移模式由低阶多项式插值函数定义，这使得单元能够精确表示的应变模式非常有限。当 $\nu \to 0.5$ 时，单元的应变能要求处处满足体积应变（在[平面应变](@entry_id:167046)中为 $\varepsilon_{xx}+\varepsilon_{yy}$）为零。对于一个低阶单元，这个严格的逐点约束会过度限制其节点位移，导致单元几乎无法变形，表现出远超其实际物理刚度的虚假刚度。这种现象即为[体积锁定](@entry_id:172606)。

为了克服[体积锁定](@entry_id:172606)，必须采用特殊的单元技术，其核心思想是放松对不可压缩约束的强制满足方式 [@problem_id:2588362]：
- **混合单元法**（Mixed Formulations）：将压力作为独立的插值场引入，通过弱形式（积分形式）来施加体积约束。
- **[选择性减缩积分](@entry_id:168281)**（Selective Reduced Integration）：对[刚度矩阵](@entry_id:178659)中的体积项采用比剪切项更低阶的积分法则，从而在积分点层面减弱约束。
- **B-bar 方法**：通过对单元内的[体积应变](@entry_id:267252)进行平均化处理，确保单元在整体上满足约束，而不是在每个积分点上都严格满足。

总之，理解平面应力和平面应变不仅是掌握二维分析的前提，其背后深刻的物理和数学原理，更是我们理解和解决有限元方法中诸如“锁定”等数值难题的基石。