## 引言
在连续介质力学中，理解物质点的运动是分析[材料力学](@entry_id:201885)行为的核心。任何复杂的局部运动都可以被分解为两部分：一部分改变材料微元的形状和尺寸（变形），另一部分则使其整体发生转动而不改变其形态（刚体旋转）。虽然描述变形的[无穷小应变张量](@entry_id:167211)广为人知，但对旋转的精确量度——**[无穷小旋转张量](@entry_id:192754) (infinitesimal rotation tensor)**——的深入理解同样至关重要。本文旨在系统阐述这一基本概念，填补从基本[运动学](@entry_id:173318)到高等应用的知识鸿沟，揭示其在理论和实践中的深刻意义。

在接下来的章节中，我们将踏上一段从基础到前沿的探索之旅。
- **第一章：原理与机制** 将从[位移梯度](@entry_id:165352)的分解出发，精确定义[无穷小旋转张量](@entry_id:192754)，阐明其作为纯旋转度量的物理意义，探讨其数学性质（如轴向矢量和与旋度的关系），并建立其与有限旋转理论之间作为线性近似的深刻联系。
- **第二章：应用与[交叉](@entry_id:147634)学科联系** 将展示该张量如何在多个领域发光发热，从解决经典固体力学问题（如简单剪切和扭转），到在高等连续介质力学中构建客观本构关系和发展微极介质理论，再到在现代计算和实验方法（如有限元分析和[纳米束](@entry_id:189854)[电子衍射](@entry_id:141284)）中的实际应用，甚至触及其在[微分几何](@entry_id:145818)等基础学科中的体现。
- **第三章：动手实践** 将通过一系列精心设计的计算问题，引导您将理论知识付诸实践，亲手从[位移场](@entry_id:141476)中分离出旋转分量，从而巩固和深化对这一核心概念的掌握。

让我们首先进入第一章，深入探索[无穷小旋转张量](@entry_id:192754)的基本原理与内在机制。

## 原理与机制

在对连续介质运动的分析中，一个核心任务是将材料点的局部运动分解为改变其形状和尺寸的纯变形，以及不改变其形状或尺寸的刚体旋转。[位移梯度](@entry_id:165352)的对称部分，即[无穷小应变张量](@entry_id:167211)，描述了变形。本章将重点阐述其反对称部分，即**[无穷小旋转张量](@entry_id:192754) (infinitesimal rotation tensor)**，探讨其定义、物理意义、数学性质，以及它与有限旋转理论的联系。

### [位移梯度](@entry_id:165352)的分解

我们从描述连续体运动的位移场 $\boldsymbol{u}(\boldsymbol{x})$ 出发。材料点邻域内的相对位移由**[位移梯度张量](@entry_id:748571) (displacement gradient tensor)** $\boldsymbol{L} = \nabla \boldsymbol{u}$ 捕捉，其分量形式为 $L_{ij} = \partial u_i / \partial x_j$。这个[二阶张量](@entry_id:199780)包含了关于局部运动的全部信息，包括拉伸、剪切和旋转。

任何一个[二阶张量](@entry_id:199780)（如此处的 $\boldsymbol{L}$）都可以唯一地分解为其对称[部分和](@entry_id:162077)反对称（或称斜对称）部分之和。这个纯粹的代数分解是理解无穷小[运动学](@entry_id:173318)的基石。

$$
\boldsymbol{L} = \boldsymbol{\varepsilon} + \boldsymbol{\omega}
$$

其中，对称部分被称为**[无穷小应变张量](@entry_id:167211) (infinitesimal strain tensor)**，定义为：

$$
\boldsymbol{\varepsilon} = \frac{1}{2} (\boldsymbol{L} + \boldsymbol{L}^{\mathsf{T}}) \quad \text{或} \quad \varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})
$$

反对称部分则被定义为**[无穷小旋转张量](@entry_id:192754) (infinitesimal rotation tensor)**：

$$
\boldsymbol{\omega} = \frac{1}{2} (\boldsymbol{L} - \boldsymbol{L}^{\mathsf{T}}) \quad \text{或} \quad \omega_{ij} = \frac{1}{2}(u_{i,j} - u_{j,i})
$$

通过定义可以立即验证，$\boldsymbol{\varepsilon}$ 是对称的（$\varepsilon_{ij} = \varepsilon_{ji}$），而 $\boldsymbol{\omega}$ 是反对称的（$\omega_{ij} = -\omega_{ji}$）[@problem_id:2697694]。由于任何[反对称张量](@entry_id:199349)的对角元素均为零（由 $\omega_{ii} = -\omega_{ii}$ 得出），所以[无穷小旋转张量](@entry_id:192754)的迹恒为零，即 $\operatorname{tr}(\boldsymbol{\omega}) = 0$ [@problem_id:2697651]。

这种分解不仅是唯一的，而且在[弗罗贝尼乌斯内积](@entry_id:153693)（Frobenius inner product）的意义下是正交的。两个[二阶张量](@entry_id:199780) $\boldsymbol{A}$ 和 $\boldsymbol{B}$ 的[弗罗贝尼乌斯内积](@entry_id:153693)定义为 $\langle \boldsymbol{A}, \boldsymbol{B} \rangle = \operatorname{tr}(\boldsymbol{A}^{\mathsf{T}}\boldsymbol{B}) = A_{ij}B_{ij}$。[应变张量](@entry_id:193332)和[旋转张量](@entry_id:191990)的[内积](@entry_id:158127)为零：

$$
\langle \boldsymbol{\varepsilon}, \boldsymbol{\omega} \rangle = \varepsilon_{ij}\omega_{ij}
$$

利用[张量的对称性](@entry_id:202126)和[反对称性](@entry_id:261893)，并通过交换[哑指标](@entry_id:188070) $i$ 和 $j$，我们得到：

$$
\varepsilon_{ij}\omega_{ij} = \varepsilon_{ji}\omega_{ji} = (\varepsilon_{ij})(-\omega_{ij}) = -\varepsilon_{ij}\omega_{ij}
$$

这个结果意味着 $\langle \boldsymbol{\varepsilon}, \boldsymbol{\omega} \rangle = -\langle \boldsymbol{\varepsilon}, \boldsymbol{\omega} \rangle$，因此 $\langle \boldsymbol{\varepsilon}, \boldsymbol{\omega} \rangle = 0$。这表明应变和旋转在代数上是相互独立的分量 [@problem_id:2697694]。

### 物理诠释：变形与旋转的分离

将[位移梯度](@entry_id:165352)分解为 $\boldsymbol{\varepsilon}$ 和 $\boldsymbol{\omega}$ 的物理动机源于它们在描述材料纤维长度和朝向变化时扮演的不同角色。

考虑一个初始构型中的无穷小材料[线元](@entry_id:196833) $\mathrm{d}\boldsymbol{X}$。在变形后，它变为 $\mathrm{d}\boldsymbol{x}$。在[小变形理论](@entry_id:174991)的框架下，两者之间的关系由变形梯度 $\boldsymbol{F} = \boldsymbol{I} + \nabla\boldsymbol{u}$ 描述，即 $\mathrm{d}\boldsymbol{x} = \boldsymbol{F}\,\mathrm{d}\boldsymbol{X} = (\boldsymbol{I} + \boldsymbol{\varepsilon} + \boldsymbol{\omega})\,\mathrm{d}\boldsymbol{X}$。

我们来考察[线元](@entry_id:196833)长度的平方变化，并只保留[位移梯度](@entry_id:165352)的一阶项。

$$
\mathrm{d}\boldsymbol{x} \cdot \mathrm{d}\boldsymbol{x} - \mathrm{d}\boldsymbol{X} \cdot \mathrm{d}\boldsymbol{X} = [(\boldsymbol{I} + \nabla\boldsymbol{u})\,\mathrm{d}\boldsymbol{X}] \cdot [(\boldsymbol{I} + \nabla\boldsymbol{u})\,\mathrm{d}\boldsymbol{X}] - \mathrm{d}\boldsymbol{X} \cdot \mathrm{d}\boldsymbol{X}
$$
$$
= \mathrm{d}\boldsymbol{X} \cdot [(\boldsymbol{I} + \nabla\boldsymbol{u})^{\mathsf{T}}(\boldsymbol{I} + \nabla\boldsymbol{u})]\,\mathrm{d}\boldsymbol{X} - \mathrm{d}\boldsymbol{X} \cdot \mathrm{d}\boldsymbol{X}
$$

展开并忽略二阶项 $(\nabla\boldsymbol{u})^{\mathsf{T}}(\nabla\boldsymbol{u})$，我们得到：

$$
(\boldsymbol{I} + \nabla\boldsymbol{u})^{\mathsf{T}}(\boldsymbol{I} + \nabla\boldsymbol{u}) \approx \boldsymbol{I} + (\nabla\boldsymbol{u})^{\mathsf{T}} + \nabla\boldsymbol{u} = \boldsymbol{I} + 2\boldsymbol{\varepsilon}
$$

因此，长度平方的一阶变化为：

$$
\mathrm{d}\boldsymbol{x} \cdot \mathrm{d}\boldsymbol{x} - \mathrm{d}\boldsymbol{X} \cdot \mathrm{d}\boldsymbol{X} \approx \mathrm{d}\boldsymbol{X} \cdot [(\boldsymbol{I} + 2\boldsymbol{\varepsilon})\,\mathrm{d}\boldsymbol{X}] - \mathrm{d}\boldsymbol{X} \cdot \mathrm{d}\boldsymbol{X} = 2\,\mathrm{d}\boldsymbol{X} \cdot (\boldsymbol{\varepsilon}\,\mathrm{d}\boldsymbol{X})
$$

这个关键结果 [@problem_id:2644603] 表明，**材料线元的长度变化仅由[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon}$ 控制**。[无穷小旋转张量](@entry_id:192754) $\boldsymbol{\omega}$ 对一阶长度变化没有贡献，这正是我们对“刚体旋转”的期望。这为将 $\boldsymbol{\varepsilon}$ 视为纯变形的度量、将 $\boldsymbol{\omega}$ 视为纯旋转的度量提供了坚实的物理基础。

同样，我们可以考察体积的变化。变形的[雅可比行列式](@entry_id:137120) $J = \det(\boldsymbol{F})$ 描述了体积的局部比率变化。对于小变形，$\boldsymbol{F} = \boldsymbol{I} + \nabla\boldsymbol{u}$，其[行列式](@entry_id:142978)可以线性化为 $J \approx 1 + \operatorname{tr}(\nabla\boldsymbol{u})$。单位体积的无穷小变化即为 $\operatorname{tr}(\nabla\boldsymbol{u})$。由于[迹算子](@entry_id:183665)的线性性，我们有：

$$
\operatorname{tr}(\nabla\boldsymbol{u}) = \operatorname{tr}(\boldsymbol{\varepsilon} + \boldsymbol{\omega}) = \operatorname{tr}(\boldsymbol{\varepsilon}) + \operatorname{tr}(\boldsymbol{\omega})
$$

正如我们前面指出的，任何[反对称张量](@entry_id:199349)的迹都为零，所以 $\operatorname{tr}(\boldsymbol{\omega}) = 0$。因此，$\operatorname{tr}(\nabla\boldsymbol{u}) = \operatorname{tr}(\boldsymbol{\varepsilon})$ [@problem_id:2697651]。这表明**无穷小体积变化完全由[应变张量](@entry_id:193332)的迹决定**，它等于位移场的散度 $\nabla \cdot \boldsymbol{u}$。$\boldsymbol{\omega}$ 所代表的旋转是保体积的，这进一步巩固了它的物理诠释。

### [无穷小旋转张量](@entry_id:192754)的性质

#### 轴向矢量

在三维空间中，任何一个反对称[二阶张量](@entry_id:199780) $\boldsymbol{\omega}$ 都可以由一个唯一的向量，即**轴向矢量 (axial vector)** $\boldsymbol{w}$ 来表示。它们之间的关系通过[叉积](@entry_id:156672)定义：对于任意向量 $\boldsymbol{v}$，都有 $\boldsymbol{\omega}\boldsymbol{v} = \boldsymbol{w} \times \boldsymbol{v}$。

使用[列维-奇维塔符号](@entry_id:193594) (Levi-Civita symbol) $\epsilon_{ijk}$，我们可以建立张量分量和矢量分量之间的显式映射。从轴向矢量到张量的映射为：

$$
\omega_{ij} = -\epsilon_{ijk}w_k
$$

其逆映射，即从张量中提取轴向矢量，可以通过以下公式计算 [@problem_id:2697635]：

$$
w_i = -\frac{1}{2}\epsilon_{ijk}\omega_{jk}
$$

例如，通过这个公式，我们可以推导出 $\omega_{12} = -\epsilon_{123}w_3 = -w_3$。

这个轴向矢量的物理意义是材料点的**无穷小转动角速度矢量**。

#### 与位移场旋度的关系

轴向矢量 $\boldsymbol{w}$ 与[位移场](@entry_id:141476) $\boldsymbol{u}$ 本身有一个直接而深刻的联系。通过其分量定义可以证明，轴向矢量恰好是[位移场](@entry_id:141476)旋度的一半 [@problem_id:2644603]：

$$
\boldsymbol{w} = \frac{1}{2} (\nabla \times \boldsymbol{u})
$$

这个关系在[流体力学](@entry_id:136788)中尤为重要，其中 $2\boldsymbol{w}$ 被称为**涡量 (vorticity)**，它描述了流体微元的局部旋转速率。在固体力学中，这意味着如果一个[位移场](@entry_id:141476)是无旋的（$\nabla \times \boldsymbol{u} = \boldsymbol{0}$），那么[无穷小旋转张量](@entry_id:192754)必定为零（$\boldsymbol{\omega} = \boldsymbol{0}$），这种变形是纯粹的拉伸/压缩和剪切，不包含局部旋转。根据[亥姆霍兹分解](@entry_id:181767)定理，在单连通域上，[无旋场](@entry_id:183486)可以表示为一个标量势 $\phi$ 的梯度，即 $\boldsymbol{u} = \nabla\phi$ [@problem_id:2644603]。

#### 在刚体运动下的变换

理解 $\boldsymbol{\varepsilon}$ 和 $\boldsymbol{\omega}$ 如何在叠加的刚体运动下变换，对于建立客观的材料本构关系至关重要。考虑一个附加的无穷小刚体运动，它由一个恒定的平移矢量 $\boldsymbol{c}$ 和一个恒定的[无穷小旋转](@entry_id:166635)（由[反对称张量](@entry_id:199349) $\boldsymbol{W}$ 表示）组成。新的位移场为 $\boldsymbol{u}_{new} = \boldsymbol{u} + \boldsymbol{c} + \boldsymbol{W}\boldsymbol{X}$。

新的[位移梯度](@entry_id:165352)为：

$$
\nabla\boldsymbol{u}_{new} = \nabla\boldsymbol{u} + \nabla(\boldsymbol{c}) + \nabla(\boldsymbol{W}\boldsymbol{X}) = \nabla\boldsymbol{u} + \boldsymbol{0} + \boldsymbol{W}
$$

新的[应变张量](@entry_id:193332)为：

$$
\boldsymbol{\varepsilon}_{new} = \frac{1}{2}(\nabla\boldsymbol{u}_{new} + \nabla\boldsymbol{u}_{new}^{\mathsf{T}}) = \frac{1}{2}(\nabla\boldsymbol{u} + \boldsymbol{W} + (\nabla\boldsymbol{u})^{\mathsf{T}} + \boldsymbol{W}^{\mathsf{T}}) = \frac{1}{2}(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^{\mathsf{T}}) + \frac{1}{2}(\boldsymbol{W} + \boldsymbol{W}^{\mathsf{T}})
$$

由于 $\boldsymbol{W}$ 是反对称的，$\boldsymbol{W} + \boldsymbol{W}^{\mathsf{T}} = \boldsymbol{0}$。因此，$\boldsymbol{\varepsilon}_{new} = \boldsymbol{\varepsilon}$。这表明**[无穷小应变张量](@entry_id:167211)在刚体运动下是不变的**，它是一个**客观 (objective)** 的量度。

相反，新的[旋转张量](@entry_id:191990)为：

$$
\boldsymbol{\omega}_{new} = \frac{1}{2}(\nabla\boldsymbol{u}_{new} - \nabla\boldsymbol{u}_{new}^{\mathsf{T}}) = \frac{1}{2}(\nabla\boldsymbol{u} + \boldsymbol{W} - (\nabla\boldsymbol{u})^{\mathsf{T}} - \boldsymbol{W}^{\mathsf{T}}) = \frac{1}{2}(\nabla\boldsymbol{u} - (\nabla\boldsymbol{u})^{\mathsf{T}}) + \frac{1}{2}(\boldsymbol{W} - \boldsymbol{W}^{\mathsf{T}})
$$

由于 $\boldsymbol{W} - \boldsymbol{W}^{\mathsf{T}} = 2\boldsymbol{W}$，我们得到 $\boldsymbol{\omega}_{new} = \boldsymbol{\omega} + \boldsymbol{W}$。[无穷小旋转张量](@entry_id:192754)**不是客观的**；它会随着观察者[参考系](@entry_id:169232)的旋转而改变 [@problem_id:2644603] [@problem_id:2697650]。

这一区别具有深远的物理意义。材料的内在属性（如其储存能量的能力）不应依赖于观察者。因此，[应变能函数](@entry_id:178435)等[本构关系](@entry_id:186508)必须只依赖于客观量。在[线性弹性](@entry_id:166983)理论中，这意味着[应变能](@entry_id:162699)是应变张量 $\boldsymbol{\varepsilon}$ 的函数，而不能依赖于非客观的[旋转张量](@entry_id:191990) $\boldsymbol{\omega}$ [@problem_id:2644603]。

### 与有限旋转的联系

到目前为止，我们的讨论局限于“无穷小”运动。为了更深刻地理解 $\boldsymbol{\omega}$，必须将它与**有限旋转 (finite rotation)** 联系起来。有限旋转由**[特殊正交群](@entry_id:146418) $SO(3)$** 中的[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 描述。这些张量满足 $\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R}=\boldsymbol{I}$ 和 $\det(\boldsymbol{R})=1$。

#### 近似关系

$\boldsymbol{\omega}$ 与 $\boldsymbol{R}$ 之间的核心联系在于，当旋转角度非常小时，$\boldsymbol{\omega}$ 是对有限旋转的线性近似。具体来说，$\boldsymbol{\omega}$ 近似于有限[旋转张量](@entry_id:191990)与单位张量之差，即 $\boldsymbol{\omega} \approx \boldsymbol{R} - \boldsymbol{I}$。

让我们更精确地审视这一近似。
-   **正交性**: 有限[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 精确满足正交条件 $\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R}=\boldsymbol{I}$。而 $\boldsymbol{I}+\boldsymbol{\omega}$ 只是近似满足：$(\boldsymbol{I}+\boldsymbol{\omega})^{\mathsf{T}}(\boldsymbol{I}+\boldsymbol{\omega}) = (\boldsymbol{I}-\boldsymbol{\omega})(\boldsymbol{I}+\boldsymbol{\omega}) = \boldsymbol{I} - \boldsymbol{\omega}^2 = \boldsymbol{I} + \mathcal{O}(\|\boldsymbol{\omega}\|^2)$。它在一阶上是正交的，但误差为二阶 [@problem_id:2697654]。类似地，$\boldsymbol{R}$ 的列向量是精确归一正交的，而 $\boldsymbol{I}+\boldsymbol{\omega}$ 的列[向量长度](@entry_id:156432)只是在一阶上为1，其长度的平方等于 $1+\mathcal{O}(\|\boldsymbol{\omega}\|^2)$ [@problem_id:2697654]。
-   **[参数化](@entry_id:272587)**: 在单位元 $\boldsymbol{I}$ 附近，$SO(3)$ 中的旋转可以由3个独立参数描述（例如[欧拉角](@entry_id:171794)）。一个[反对称张量](@entry_id:199349) $\boldsymbol{\omega}$ 也由3个独立分量（其轴向矢量的分量）确定。事实上，所有 $3 \times 3$ [反对称张量](@entry_id:199349)的集合构成了 $SO(3)$ 在[单位元处的切空间](@entry_id:266468)，即其**[李代数](@entry_id:137954) (Lie algebra)** $\mathfrak{so}(3)$。因此，$\boldsymbol{\omega}$ 可以被看作是旋转群的一个[局部线性](@entry_id:266981)参数 [@problem_id:2697654]。
-   **极分解**: 更深刻的联系来自变形梯度 $\boldsymbol{F}$ 的**极分解 (polar decomposition)**，$\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$。这里 $\boldsymbol{R}$ 是有限[旋转张量](@entry_id:191990)，$\boldsymbol{U}$ 是[对称正定](@entry_id:145886)的右[拉伸张量](@entry_id:193200)。当变形很小时，$\boldsymbol{F} = \boldsymbol{I} + \nabla\boldsymbol{u} = \boldsymbol{I} + \boldsymbol{\varepsilon} + \boldsymbol{\omega}$。通过对 $\boldsymbol{R}$ 和 $\boldsymbol{U}$ 进行泰勒展开，$\boldsymbol{R} \approx \boldsymbol{I} + \boldsymbol{R}^{(1)}$ 和 $\boldsymbol{U} \approx \boldsymbol{I} + \boldsymbol{U}^{(1)}$，可以严格证明 [@problem_id:2697693]：
    $$
    \boldsymbol{R}^{(1)} = \boldsymbol{\omega} \quad \text{and} \quad \boldsymbol{U}^{(1)} = \boldsymbol{\varepsilon}
    $$
    这表明，[无穷小旋转张量](@entry_id:192754) $\boldsymbol{\omega}$ 正是有限旋转 $\boldsymbol{R}$ 的一阶近似，而[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon}$ 则是右拉伸 $\boldsymbol{U}$ 的一阶近似。

#### 近似的有效性

上述近似关系并非无条件成立。它要求**[位移梯度](@entry_id:165352)的范数 $\|\nabla\boldsymbol{u}\|$ 在整个物体内一致地小** [@problem_id:2697648]。如果 $\|\nabla\boldsymbol{u}\|$ 很小（例如，$\|\nabla\boldsymbol{u}\| = \mathcal{O}(\delta)$，其中 $\delta \ll 1$），那么二阶及更高阶的项（$\mathcal{O}(\delta^2)$）才可以被忽略，线性化理论才有效。仅仅位移小（$\|\boldsymbol{u}\| \ll 1$）或仅仅应变小（$\|\boldsymbol{\varepsilon}\| \ll 1$）都是不够的，因为可能存在小位移大梯度（例如高频[振动](@entry_id:267781)）或小应变大旋转的情况。

我们可以定量地分析这个近似的误差。考虑一个绕固定单位轴 $\boldsymbol{a}$ 的纯有限转动，角度为 $\phi$。其精确的[旋转张量](@entry_id:191990)由[罗德里格旋转公式](@entry_id:165151)给出：$\boldsymbol{R} = \boldsymbol{I} + (\sin\phi)\boldsymbol{W} + (1-\cos\phi)\boldsymbol{W}^2$，其中 $\boldsymbol{W}$ 是与 $\boldsymbol{a}$ 对应的[反对称张量](@entry_id:199349)。其线性近似为 $\boldsymbol{I} + \boldsymbol{\omega} = \boldsymbol{I} + \phi\boldsymbol{W}$。两者之间的误差张量为 $\boldsymbol{E} = \boldsymbol{R} - (\boldsymbol{I}+\boldsymbol{\omega}) = (\sin\phi - \phi)\boldsymbol{W} + (1-\cos\phi)\boldsymbol{W}^2$。其[弗罗贝尼乌斯范数](@entry_id:143384)的平方可以精确计算为：
$$
\|\boldsymbol{E}\|_F^2 = 2(\sin\phi - \phi)^2 + 2(1-\cos\phi)^2 = 4 - 4\cos\phi - 4\phi\sin\phi + 2\phi^2
$$
当 $\phi \to 0$ 时，对上式进行泰勒展开，可以发现 $\|\boldsymbol{E}\|_F^2 \approx \frac{1}{2}\phi^4$。因此，[误差范数](@entry_id:176398) $\|\boldsymbol{E}\|_F \approx \frac{1}{\sqrt{2}}\phi^2$，这表明误差是 $\phi$ 的二阶小量，验证了 $\boldsymbol{I}+\boldsymbol{\omega}$ 是对 $\boldsymbol{R}$ 的[一阶近似](@entry_id:147559) [@problem_id:2697686]。

### 综合示例

让我们通过一个具体的例子来整合这些概念 [@problem_id:2697650]。考虑一个[位移场](@entry_id:141476)：
$$
\boldsymbol{u}(\boldsymbol{x}) = \boldsymbol{a} + \boldsymbol{\theta} \times \boldsymbol{x} + \boldsymbol{H}\boldsymbol{x} + \boldsymbol{g}(\boldsymbol{x})
$$
其中 $\boldsymbol{a}$ 是常数平移，$\boldsymbol{\theta}$ 是常数[刚体转动](@entry_id:191086)轴向矢量，$\boldsymbol{H}$ 是常数对称张量，$\boldsymbol{g}(\boldsymbol{x})$ 是一个高阶[非线性](@entry_id:637147)项。

首先计算[位移梯度](@entry_id:165352) $\boldsymbol{L} = \nabla\boldsymbol{u}$：
-   平移项的梯度为零：$\nabla\boldsymbol{a} = \boldsymbol{0}$。
-   [刚体转动](@entry_id:191086)项的梯度是一个[反对称张量](@entry_id:199349) $\boldsymbol{\Omega}$，其轴向矢量为 $\boldsymbol{\theta}$ (或严格来说，$\boldsymbol{\Omega}_{ij} = -\epsilon_{ijk}\theta_k$)。
-   线性项 $\boldsymbol{H}\boldsymbol{x}$ 的梯度就是 $\boldsymbol{H}$ 本身。
-   [非线性](@entry_id:637147)项的梯度为 $\nabla\boldsymbol{g}$。

所以，$\boldsymbol{L}(\boldsymbol{x}) = \boldsymbol{\Omega} + \boldsymbol{H} + \nabla\boldsymbol{g}(\boldsymbol{x})$。

现在，我们计算[无穷小旋转张量](@entry_id:192754) $\boldsymbol{\omega} = \frac{1}{2}(\boldsymbol{L} - \boldsymbol{L}^{\mathsf{T}})$：
$$
\boldsymbol{\omega}(\boldsymbol{x}) = \frac{1}{2}[(\boldsymbol{\Omega} + \boldsymbol{H} + \nabla\boldsymbol{g}) - (\boldsymbol{\Omega}^{\mathsf{T}} + \boldsymbol{H}^{\mathsf{T}} + (\nabla\boldsymbol{g})^{\mathsf{T}})]
$$
利用 $\boldsymbol{\Omega}$ 的[反对称性](@entry_id:261893) ($\boldsymbol{\Omega}^{\mathsf{T}} = -\boldsymbol{\Omega}$) 和 $\boldsymbol{H}$ 的对称性 ($\boldsymbol{H}^{\mathsf{T}} = \boldsymbol{H}$)，上式简化为：
$$
\boldsymbol{\omega}(\boldsymbol{x}) = \frac{1}{2}[2\boldsymbol{\Omega} + (\boldsymbol{H}-\boldsymbol{H}) + (\nabla\boldsymbol{g} - (\nabla\boldsymbol{g})^{\mathsf{T}})] = \boldsymbol{\Omega} + \mathrm{skew}(\nabla\boldsymbol{g}(\boldsymbol{x}))
$$
这个结果清晰地表明：
1.  恒定的平移 $\boldsymbol{a}$ 对[无穷小旋转](@entry_id:166635)没有贡献。
2.  恒定的对称应变场 $\boldsymbol{H}$ 对[无穷小旋转](@entry_id:166635)没有贡献；它完全贡献给了[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ [@problem_id:2697650]。
3.  场的[无穷小旋转](@entry_id:166635)由两部分组成：一个是由[刚体转动](@entry_id:191086) $\boldsymbol{\theta}$ 产生的均匀旋转 $\boldsymbol{\Omega}$，另一个是由[位移场](@entry_id:141476)的非均匀（[非线性](@entry_id:637147)）部分产生的局部旋转 $\mathrm{skew}(\nabla\boldsymbol{g})$。
4.  如果再叠加一个额外的[刚体转动](@entry_id:191086)（由轴向矢量 $\boldsymbol{\varphi}$ 和张量 $\boldsymbol{\Phi}$ 表示），新的[旋转张量](@entry_id:191990)将是 $\boldsymbol{\omega}_{new} = \boldsymbol{\omega} + \boldsymbol{\Phi}$，这体现了[无穷小旋转](@entry_id:166635)的线性叠加性 [@problem_id:2697650]。

通过这个例子，我们可以看到[无穷小旋转张量](@entry_id:192754)如何从复杂的运动场中被精确地分离出来，并理解其各个来源。