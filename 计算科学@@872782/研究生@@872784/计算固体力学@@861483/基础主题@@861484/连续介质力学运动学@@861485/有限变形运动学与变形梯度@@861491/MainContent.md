## 引言
在现代工程与科学领域，从柔性电子设备的设计到生物组织的生长模拟，许多问题都涉及到材料的大位移、大转动和[大应变](@entry_id:751152)。在这些情况下，基于小变形假设的[线性弹性](@entry_id:166983)理论不再适用，我们必须转向一个更普适的框架——有限变形理论。该理论的基石是有限变形[运动学](@entry_id:173318)，它提供了一套精确描述和量化任意变形的数学工具。其中，变形梯度张量是理解整个理论体系的核心，它不仅是运动学的核心度量，也是连接运动与力（即[本构关系](@entry_id:186508)）的桥梁。本文旨在系统性地解析这一关键领域，填补从基础概念到高级应用的知识鸿沟。

本文将引导读者深入探索有限变形运动学的世界。首先，在“原理与机制”一章中，我们将建立起描述变形的数学语言，详细定义变形梯度、多种应变张量以及变形率，并阐明本构模型必须遵循的物质标架无关性等基本原理。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些理论概念如何在[固体力学](@entry_id:164042)、多物理场耦合、[材料科学](@entry_id:152226)乃至[计算机图形学](@entry_id:148077)和医学成像等多个领域中发挥关键作用。最后，“动手实践”部分将提供一系列精心设计的计算练习，帮助读者将抽象的理论转化为具体的计算能力。通过这一结构化的学习路径，读者将能够全面掌握有限变形[运动学](@entry_id:173318)的精髓，并具备将其应用于复杂实际问题的能力。

## 原理与机制

本章旨在系统性地阐述有限变形运动学的核心原理与机制。在前一章介绍性地探讨了连续介质力学的背景之后，本章将深入研究描述和量化变形的数学工具。我们将从定义运动和变形梯度开始，然后引入各种应变张量来量化变形，并探讨变形率的运动学。最后，我们将讨论本构关系必须遵守的基本原理，如物质标架无关性，并探讨一些确保运动学相容性的高级概念。

### 描述变形：运动与变形梯度

在[连续介质力学](@entry_id:155125)中，物体的变形是通过一个称为**运动(motion)**的数学映射来描述的。运动是一个函数$\boldsymbol{\chi}$，它将物体在**参考构型(reference configuration)**$\mathcal{B}_0$中的每一个物质点$\mathbf{X}$映射到其在时间$t$时刻在**当前构型(current configuration)**$\mathcal{B}_t$中的空间位置$\mathbf{x}$。数学上，这表示为：

$$
\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)
$$

这里，$\mathbf{X}$被称为**物质坐标(material coordinate)**或拉格朗日坐标，而$\mathbf{x}$被称为**空间坐标(spatial coordinate)**或欧拉坐标。参考构型是固定且方便的，通常选为物体在初始时刻($t=0$)未变形的状态。

为了量化变形，我们需要一个能够描述物[质点](@entry_id:186768)邻域如何被拉伸和旋转的量。这个量就是**变形梯度(deformation gradient)**，记为$\mathbf{F}$。它被定义为运动$\boldsymbol{\chi}$对物质坐标$\mathbf{X}$的梯度：

$$
\mathbf{F}(\mathbf{X}, t) = \frac{\partial \boldsymbol{\chi}(\mathbf{X}, t)}{\partial \mathbf{X}} = \nabla_{\mathbf{X}} \boldsymbol{\chi}
$$

变形梯度$\mathbf{F}$是一个二阶张量，它包含了关于局部变形的全部信息。它的一个基本几何意义是作为一个**切映射(tangent map)**[@problem_id:3565014]。考虑参考构型中一个从$\mathbf{X}$点出发的无限小物质线元$d\mathbf{X}$。经过变形后，这个[线元](@entry_id:196833)变为当前构型中的空间[线元](@entry_id:196833)$d\mathbf{x}$。它们之间的关系由变形梯度线性地给出：

$$
d\mathbf{x} = \mathbf{F} d\mathbf{X}
$$

这个关系表明，$\mathbf{F}$将参考构型中的矢量（如切矢量）映射到当前构型中的相应矢量。

变形梯度的[行列式](@entry_id:142978)，记为$J = \det \mathbf{F}$，具有重要的物理意义。它代表了局部的体积变化率。一个在参考构型中体积为$dV$的无限小体积元，在变形后其体积$dv$将变为：

$$
dv = J dV
$$

物理上，物质不能相互穿透，也不能从有限体积压缩为零体积。因此，我们通常要求$J > 0$。这个条件保证了变形是保向的（例如，[右手坐标系](@entry_id:166669)仍然是[右手坐标系](@entry_id:166669)），并且局部体积为正。纯[刚体转动](@entry_id:191086)是一个特殊的变形例子，其运动为$\boldsymbol{\chi}(\mathbf{X}, t) = \mathbf{Q}(t)\mathbf{X}$，其中$\mathbf{Q}(t)$是一个真正常交张量（[旋转张量](@entry_id:191990)）。在这种情况下，变形梯度处处等于[旋转张量](@entry_id:191990)本身，即$\mathbf{F} = \mathbf{Q}(t)$。由于[旋转张量](@entry_id:191990)的[行列式](@entry_id:142978)为$+1$，我们得到$J=1$，这意味着纯[刚体转动](@entry_id:191086)不改变体积、长度和角度[@problem_id:3565014]。

在描述物理场（如温度或密度）时，我们可以采用两种视角[@problem_id:3564995]。**物质描述(material description)**或[拉格朗日描述](@entry_id:264498)，将物理量视为物质点$\mathbf{X}$和时间$t$的函数，记为$\Phi(\mathbf{X}, t)$。而**空间描述(spatial description)**或[欧拉描述](@entry_id:264722)，将物理量视为空间点$\mathbf{x}$和时间$t$的函数，记为$\phi(\mathbf{x}, t)$。这两种描述通过运动联系在一起：

$$
\Phi(\mathbf{X}, t) = \phi(\boldsymbol{\chi}(\mathbf{X}, t), t)
$$

这两种描述下的梯度也通过变形梯度相关联。利用多元微积分的链式法则，可以推导出物质梯度$\operatorname{Grad}_{\mathbf{X}}\Phi$和空间梯度$\nabla_{\mathbf{x}}\phi$之间的关系：

$$
\operatorname{Grad}_{\mathbf{X}}\Phi = \mathbf{F}^{\top} \nabla_{\mathbf{x}}\phi
$$

这个关系也可以反过来写，将空间梯度表示为物质梯度的**[前推](@entry_id:158718)(push-forward)**：

$$
\nabla_{\mathbf{x}}\phi = \mathbf{F}^{-\top} \operatorname{Grad}_{\mathbf{X}}\Phi
$$

这些变换关系在需要在不同构型之间转换控制方程时至关重要。

### 测量应变：伸长张量与[主伸长](@entry_id:194664)

变形梯度$\mathbf{F}$本身包含了旋转和拉伸的信息。为了孤立地量化材料的“纯”拉伸或应变，我们需要构造不依赖于[刚体转动](@entry_id:191086)的量。这是通过定义**柯西-格林变形张量(Cauchy-Green deformation tensors)**来实现的。

**[右柯西-格林张量](@entry_id:174156)(right Cauchy-Green tensor)**$\mathbf{C}$定义为：

$$
\mathbf{C} = \mathbf{F}^{\top}\mathbf{F}
$$

**[左柯西-格林张量](@entry_id:186163)(left Cauchy-Green tensor)**$\mathbf{B}$ (也称为芬格张量，Finger tensor)定义为：

$$
\mathbf{B} = \mathbf{F}\mathbf{F}^{\top}
$$

$\mathbf{C}$是一个定义在参考构型上的张量，而$\mathbf{B}$是一个定义在当前构型上的张量。它们都是对称且正定的（只要$J>0$）。它们的物理意义在于量化长度的变化。对于一个物质线元$d\mathbf{X}$，其变形后的长度平方$ds^2 = d\mathbf{x} \cdot d\mathbf{x}$可以通过$\mathbf{C}$在参考构型中计算[@problem_id:3565011]：

$$
ds^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F}d\mathbf{X}) \cdot (\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{F}^{\top}\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{C}d\mathbf{X})
$$

类似地，一个空间线元$d\mathbf{x}$在变形前的长度平方$dS^2 = d\mathbf{X} \cdot d\mathbf{X}$可以通过$\mathbf{B}$的逆在当前构型中计算：

$$
dS^2 = d\mathbf{X} \cdot d\mathbf{X} = (\mathbf{F}^{-1}d\mathbf{x}) \cdot (\mathbf{F}^{-1}d\mathbf{x}) = d\mathbf{x} \cdot (\mathbf{F}^{-\top}\mathbf{F}^{-1}d\mathbf{x}) = d\mathbf{x} \cdot (\mathbf{B}^{-1}d\mathbf{x})
$$

为了更直观地理解变形的分解，我们引入**极分解(polar decomposition)**定理[@problem_id:3565039]。该定理指出，任何非奇异的变形梯度$\mathbf{F}$(即$\det\mathbf{F} \neq 0$)都可以唯一地分解为一个旋转和一个纯拉伸的乘积。具体来说，存在两种分解方式：

$$
\mathbf{F} = \mathbf{R}\mathbf{U} \quad (\text{右极分解})
$$
$$
\mathbf{F} = \mathbf{V}\mathbf{R} \quad (\text{左极分解})
$$

这里：
- $\mathbf{R}$是一个**[旋转张量](@entry_id:191990)(rotation tensor)**，属于真正常交群$SO(3)$，满足$\mathbf{R}^{\top}\mathbf{R} = \mathbf{I}$和$\det\mathbf{R}=+1$。它代表了物[质点](@entry_id:186768)的局部[刚体转动](@entry_id:191086)。
- $\mathbf{U}$是**[右伸长张量](@entry_id:193756)(right stretch tensor)**，是一个[对称正定](@entry_id:145886)张量，它在参考构型中描述拉伸。
- $\mathbf{V}$是**[左伸长张量](@entry_id:197330)(left stretch tensor)**，也是一个对称正定张量，它在当前构型中描述拉伸。

这些张量与柯西-格林张量直接相关：

$$
\mathbf{U} = \sqrt{\mathbf{C}} = (\mathbf{F}^{\top}\mathbf{F})^{1/2}
$$
$$
\mathbf{V} = \sqrt{\mathbf{B}} = (\mathbf{F}\mathbf{F}^{\top})^{1/2}
$$

$\mathbf{U}$和$\mathbf{V}$是通过取对称正定张量$\mathbf{C}$和$\mathbf{B}$的唯一正定平方根来定义的。$\mathbf{U}$和$\mathbf{V}$通过[旋转张量](@entry_id:191990)$\mathbf{R}$相互关联：$\mathbf{V} = \mathbf{R}\mathbf{U}\mathbf{R}^{\top}$。这意味着它们具有相同的[特征值](@entry_id:154894)，但[特征向量](@entry_id:151813)（[主方向](@entry_id:276187)）因旋转$\mathbf{R}$而不同。

$\mathbf{U}$和$\mathbf{V}$的[特征值](@entry_id:154894)被称为**[主伸长](@entry_id:194664)(principal stretches)**，记为$\lambda_1, \lambda_2, \lambda_3$。它们代表了相互正交的三个方向上的最大、最小和中间拉伸比。由于$\mathbf{C}=\mathbf{U}^2$和$\mathbf{B}=\mathbf{V}^2$，$\mathbf{C}$和$\mathbf{B}$的[特征值](@entry_id:154894)都是[主伸长](@entry_id:194664)的平方，即$\lambda_1^2, \lambda_2^2, \lambda_3^2$[@problem_id:3565011]。$\mathbf{C}$的[特征向量](@entry_id:151813)定义了**物质[主方向](@entry_id:276187)(material principal directions)**，而$\mathbf{B}$的[特征向量](@entry_id:151813)定义了**空间主方向(spatial principal directions)**。

在构建各向同性材料的本构模型时，[响应函数](@entry_id:142629)通常不依赖于[坐标系](@entry_id:156346)的选择，而是依赖于变形张量的[不变量](@entry_id:148850)。$\mathbf{C}$的三个**[主不变量](@entry_id:193522)(principal invariants)**通常定义为[@problem_id:3564997]：

$$
I_1 = \operatorname{tr}(\mathbf{C}) = \lambda_1^2 + \lambda_2^2 + \lambda_3^2
$$
$$
I_2 = \frac{1}{2}[(\operatorname{tr}\mathbf{C})^2 - \operatorname{tr}(\mathbf{C}^2)] = \lambda_1^2\lambda_2^2 + \lambda_2^2\lambda_3^2 + \lambda_3^2\lambda_1^2
$$
$$
I_3 = \det(\mathbf{C}) = (\det\mathbf{F})^2 = J^2 = \lambda_1^2\lambda_2^2\lambda_3^2
$$

由于$\mathbf{B}$和$\mathbf{C}$具有相同的[特征值](@entry_id:154894)，它们的[不变量](@entry_id:148850)也相同。

### 变形率：速度梯度

[运动学](@entry_id:173318)不仅关心变形的结果，还关心变形发生的速度。描述变形率的关键量是**[空间速度梯度](@entry_id:187198)(spatial velocity gradient)**，记为$\mathbf{L}$。它被定义为[空间速度](@entry_id:190294)场$\mathbf{v}(\mathbf{x}, t)$对空间坐标$\mathbf{x}$的梯度：

$$
\mathbf{L} = \nabla_{\mathbf{x}}\mathbf{v}
$$

[速度梯度](@entry_id:261686)$\mathbf{L}$描述了邻近点之间的相对速度，因此包含了关于材料变形速率和旋转速率的信息。通过将其分解为对称和反对称两部分，我们可以清晰地分离这两种效应[@problem_id:3565027]：

$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$

其中：
- $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\top})$是**变形率张量(rate-of-deformation tensor)**或伸长率张量。它是一个对称张量，描述了材料线元长度和夹角变化的[瞬时速率](@entry_id:182981)。一个沿着单位方向$\mathbf{n}$的线元，其长度平方的[瞬时变化率](@entry_id:141382)为$2\mathbf{n}\cdot\mathbf{D}\mathbf{n}$。
- $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\top})$是**[自旋张量](@entry_id:187346)(spin tensor)**或[涡量张量](@entry_id:189621)。它是一个[反对称张量](@entry_id:199349)，描述了材料的瞬时刚体角速度。[反对称张量](@entry_id:199349)$\mathbf{W}$的作用等效于与一个[轴矢量](@entry_id:196296)$\boldsymbol{\omega}$(称为[涡量矢量](@entry_id:187667))的叉乘。

[拉格朗日描述](@entry_id:264498)和[欧拉描述](@entry_id:264722)之间有一个关于变形率的基本关系。变形梯度的时间导数（固定物[质点](@entry_id:186768)$\mathbf{X}$）$\dot{\mathbf{F}}$与[空间速度梯度](@entry_id:187198)$\mathbf{L}$通过以下重要关系式相连[@problem_id:3565004]：

$$
\dot{\mathbf{F}} = \mathbf{L}\mathbf{F}
$$

这个关系可以通过对$\mathbf{F} = \nabla_{\mathbf{X}}\mathbf{x}$求[物质时间导数](@entry_id:190892)并交换求导次序来推导。从这个关系式可以得到$\mathbf{L}$的另一种表达形式$\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$，这清楚地表明$\mathbf{L}$是变形梯度率的当前构型表示。

在计算力学中，网格本身可能以独立于物质的速度运动，这被称为**任意拉格朗日-欧拉(Arbitrary Lagrangian-Eulerian, ALE)**方法。如果网格速度为$\mathbf{w}(\mathbf{x}, t)$，则在固定网格点上观察到的$\mathbf{F}$的时间导数（ALE导数）由以下[输运方程](@entry_id:756133)给出[@problem_id:3565004]：

$$
\frac{\partial^{\mathrm{a}} \mathbf{F}}{\partial t} + ((\mathbf{v}-\mathbf{w})\cdot \nabla)\mathbf{F} = \mathbf{L}\mathbf{F}
$$

其中$(\mathbf{v}-\mathbf{w})$是物质相对于网格的[对流](@entry_id:141806)速度。

### [本构模型](@entry_id:174726)的基本原理

[本构定律](@entry_id:178936)（或本构关系）描述了材料如何响应变形，例如应力如何依赖于应变。这些定律不能是任意的，必须遵循某些普适的物理原理。

#### 物质[标架无关性原理](@entry_id:200995)（客观性）

**物质标架无关性(material frame-indifference)**或**客观性(objectivity)**原理指出，[本构关系](@entry_id:186508)必须独立于观察者。观察者的变换是通过一个叠加的[刚体运动](@entry_id:193355)来描述的，即对当前构型施加一个随时间变化的旋转$\mathbf{Q}(t)$和平移$\mathbf{c}(t)$：

$$
\mathbf{x}^* = \mathbf{Q}(t)\mathbf{x} + \mathbf{c}(t)
$$

在这个变换下，一个物理量是否客观，取决于它的变换规律是否符合其几何或物理本质[@problem_id:3564990]。
- **客观的空间矢量**$\mathbf{a}$变换为$\mathbf{a}^* = \mathbf{Q}\mathbf{a}$。
- **客观的空间[二阶张量](@entry_id:199780)**$\mathbf{A}$变换为$\mathbf{A}^* = \mathbf{Q}\mathbf{A}\mathbf{Q}^{\top}$。
- **客观的参考构型量**（标量、矢量或张量）保持不变，因为参考构型不受观察者变换的影响。

根据这些定义，我们可以检验之前介绍的运动学量的客观性：
- 变形梯度$\mathbf{F}$变换为$\mathbf{F}^* = \mathbf{Q}\mathbf{F}$，它**不是**客观的。
- [右柯西-格林张量](@entry_id:174156)$\mathbf{C}$变换为$\mathbf{C}^* = \mathbf{C}$，它是客观的参考构型张量。
- [左柯西-格林张量](@entry_id:186163)$\mathbf{B}$变换为$\mathbf{B}^* = \mathbf{Q}\mathbf{B}\mathbf{Q}^{\top}$，它是客观的[空间张量](@entry_id:185799)。
- 变形率张量$\mathbf{D}$变换为$\mathbf{D}^* = \mathbf{Q}\mathbf{D}\mathbf{Q}^{\top}$，它是客观的。
- [自旋张量](@entry_id:187346)$\mathbf{W}$变换为$\mathbf{W}^* = \mathbf{Q}\mathbf{W}\mathbf{Q}^{\top} + \dot{\mathbf{Q}}\mathbf{Q}^{\top}$，由于额外的项$\dot{\mathbf{Q}}\mathbf{Q}^{\top}$（叠加的[角速度](@entry_id:192539)），它**不是**客观的。

[本构关系](@entry_id:186508)必须仅由客观量构成。例如，柯西应力$\boldsymbol{\sigma}$（一个客观的[空间张量](@entry_id:185799)）必须表示为其他客观运动学量的函数，如$\mathbf{B}$或$\mathbf{D}$。

#### [材料对称性](@entry_id:190289)（各向同性）

[材料对称性](@entry_id:190289)是材料的内在属性，与观察者无关。它描述了材料在参考构型中旋转时其响应是否发生变化[@problem_id:3565007]。一个材料如果其[本构关系](@entry_id:186508)在任意旋转参考[坐标系](@entry_id:156346)后保持不变，则被称为**各向同性(isotropic)**。

客观性是所有材料都必须满足的普适原理，而各向同性是某些特定材料（如许多金属、非晶聚合物）才具有的属性。
- **客观性**约束了本构函数的形式。例如，一个标量函数$\phi(\mathbf{B})$要想是客观的，它必须满足$\phi(\mathbf{Q}\mathbf{B}\mathbf{Q}^{\top}) = \phi(\mathbf{B})$，这意味着$\phi$只能是$\mathbf{B}$的[不变量](@entry_id:148850)的函数。
- **各向同性**则对[本构关系](@entry_id:186508)施加了关于材料坐标的额外约束。例如，对于一个各向同性材料，其[应变能函数](@entry_id:178435)$\Psi(\mathbf{C})$必须满足$\Psi(\mathbf{Q}_{0}^{\top}\mathbf{C}\mathbf{Q}_{0}) = \Psi(\mathbf{C})$对于所有旋转$\mathbf{Q}_{0}$成立。这意味着$\Psi$只能是$\mathbf{C}$的[主不变量](@entry_id:193522)$I_1, I_2, I_3$的函数。

区分这两个概念至关重要：客观性是关于空间[坐标系](@entry_id:156346)的变换（改变观察者），而[材料对称性](@entry_id:190289)是关于物质[坐标系](@entry_id:156346)的变换（旋转材料本身）。

### 高级[运动学](@entry_id:173318)考虑

#### 变形的相容性

一个自然的问题是：任意给定的一个二阶张量场$\mathbf{F}(\mathbf{X})$是否都能成为某个连续变形的变形梯度？答案是否定的。为了使一个场$\mathbf{F}$能够从一个连续的、足够光滑的运动场$\boldsymbol{\chi}(\mathbf{X})$通过求梯度得到，即$\mathbf{F} = \nabla_0 \boldsymbol{\chi}$，$\mathbf{F}$必须满足一定的**[相容性条件](@entry_id:637057)(compatibility condition)**[@problem_id:3565005]。

这个条件源于[混合偏导数的对称性](@entry_id:146941)($\partial^2 \boldsymbol{\chi} / \partial X_K \partial X_L = \partial^2 \boldsymbol{\chi} / \partial X_L \partial X_K$)。对于一个在单连通域$\Omega_0$上定义的、连续可微的[张量场](@entry_id:190170)$\mathbf{F}$，它是一个相容的变形梯度的充分必要条件是它的**物质旋度(material curl)**为零：

$$
\mathrm{Curl}_0\,\mathbf{F} = \mathbf{0}
$$

这里的[旋度算子](@entry_id:184984)是逐行作用的。这个条件保证了从$\mathbf{F}$积分得到运动$\boldsymbol{\chi}$时，结果与积分路径无关，从而能够定义一个唯一的（不计刚体平移）运动场。

#### 全局[单射性](@entry_id:147722)与非贯穿性

在物理上，物体不能自己穿过自己。这意味着运动映射$\boldsymbol{\chi}$必须是**[单射](@entry_id:183792)的(injective)**或一对一的：不同的物[质点](@entry_id:186768)$\mathbf{X}_1 \neq \mathbf{X}_2$必须映射到不同的空间点$\boldsymbol{\chi}(\mathbf{X}_1) \neq \boldsymbol{\chi}(\mathbf{X}_2)$。

一个常见的误解是，只要局部体积变化率$J = \det\mathbf{F} > 0$处处成立，就能保证全局[单射性](@entry_id:147722)。然而，事实并非如此。$J>0$仅通过[反函数定理](@entry_id:275014)保证了**局部**[单射性](@entry_id:147722)。一个物体完全可能在保持局部体积为正的情况下发生全局性的自相交或折叠[@problem_id:3565034]。一个经典的二维例子是映射$\varphi(X_1, X_2) = (X_1^2 - X_2^2, 2X_1X_2)$。对于一个不包含原点的环形域，此映射的雅可比行列式$J = 4(X_1^2 + X_2^2)$处处为正，但它不是全局单射的，因为任意两个相差一个负号的点（如$(X_1, X_2)$和$(-X_1, -X_2)$）会映射到同一点。

在[非线性弹性](@entry_id:185743)理论和计算中，确保全局[单射性](@entry_id:147722)是一个深刻且困难的问题。仅仅在[有限元网格](@entry_id:174862)的每个单元或积分点上强制$J>0$是不够的，它不能阻止不同部分的网格相互接触或穿透。更强的条件，如Ciarlet-Nečas条件（要求$\int_{\Omega} J(X) dX \le |\varphi(\Omega)|$）或基于[拓扑度](@entry_id:264252)理论的条件，才能在数学上保证全局[单射性](@entry_id:147722)（或几乎处处[单射](@entry_id:183792)）[@problem_id:3565034]。这些高级概念对于开发稳健的大变形计算方法至关重要。