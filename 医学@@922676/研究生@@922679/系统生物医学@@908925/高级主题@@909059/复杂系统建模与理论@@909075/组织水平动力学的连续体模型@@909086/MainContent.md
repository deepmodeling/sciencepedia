## 引言
生物组织，从搏动的心肌到承重的骨骼，其生理功能与其复杂的力学行为密不可分。为了在宏观尺度上理解、预测和调控这些行为，我们需要一个强大的数学和物理框架。连续介质模型正是为此而生，它将由无数离散细胞和分子构成的组织抽象为具有[连续分布](@entry_id:264735)物理属性（如密度、应力）的材料，从而使我们能够运用[偏微分](@entry_id:194612)方程来描述其动力学过程。

然而，组织是由离散的细胞和细胞外基质构成的微观世界，如何从这些离散组分的相互作用中“涌现”出连续的、可预测的宏观动力学，是系统生物医学中的一个核心挑战。本文旨在系统性地介绍组织尺度动力学的连续介质模型，作为连接微观与宏观的理论桥梁，并阐明其在现代生物医学研究中的核心地位。

本文将引导读者循序渐进地构建这一知识体系。在第一章“原理与机制”中，我们将奠定理论基础，详细阐述描述变形、力和材料响应的数学语言。随后，在第二章“应用与交叉学科联系”中，我们将展示这些理论如何被应用于解释从被动响应到主动收缩、从生长重塑到[模式形成](@entry_id:139998)等多样化的生物学现象。最后，在第三章“动手实践”中，我们提供了将理论转化为计算实践的练习，帮助读者巩固理解并迈向[数值模拟](@entry_id:146043)的第一步。通过这三个层次的递进，读者将全面掌握如何运用连续介质模型来分析复杂的生物组织动力学问题。

## 原理与机制

本章旨在系统性地阐述描述组织尺度动力学的连续介质模型背后的核心原理与机制。我们将从描述组织变形的运动学语言开始，继而探讨引起这些变形的力（即动力学），然后建立连接力和变形的本构关系。最后，我们将介绍用于模拟生物组织多相特性和生长重塑等复杂现象的高级理论框架。

### 变形运动学：描述组织运动

为了定量描述生物组织的变形，我们需要一个精确的数学框架。[连续介质力学](@entry_id:155125)的运动学分支为此提供了基础。其核心思想在于比较组织在变形前（参考构型）和变形后（当前构型）的状态。

#### 参考构型与当前构型：[拉格朗日与欧拉描述](@entry_id:190556)

想象一下，我们正在观察一块正在变形的组织。我们可以采用两种不同的视角来描述其内部任意一点的物理量（如位移、速度、密度等）。

第一种是**[拉格朗日描述](@entry_id:264498) (Lagrangian description)**，它好比给组织中的每一个“物[质点](@entry_id:186768)”都贴上一个永久的标签。我们使用物质坐标 $\mathbf{X}$ 来唯一标识这个点，该坐标通常是其在初始参考构型 $\mathcal{B}_0$ 中的位置。然后，我们追踪这个被标记的物[质点](@entry_id:186768)在不同时刻 $t$ 的空间位置 $\mathbf{x}$。因此，在[拉格朗日描述](@entry_id:264498)中，所有的物理场都被表示为物质坐标 $\mathbf{X}$ 和时间 $t$ 的函数，例如速度场 $\mathbf{V}(\mathbf{X}, t)$。

第二种是**[欧拉描述](@entry_id:264722) (Eulerian description)**，它好比在空间中设置一个固定的观测站。我们关注的是在特定空间位置 $\mathbf{x}$ 和时刻 $t$ 发生的事情，而不关心是哪个物质点恰好经过这个位置。因此，在[欧拉描述](@entry_id:264722)中，物理场被表示为空间坐标 $\mathbf{x}$ 和时间 $t$ 的函数，例如速度场 $\mathbf{v}(\mathbf{x}, t)$。

这两种描述通过**运动映射 (motion map)** $\boldsymbol{\chi}$ 联系起来，它给出了每个物[质点](@entry_id:186768) $\mathbf{X}$ 在时刻 $t$ 的空间位置：$\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$。这两种描述各有优势：[拉格朗日描述](@entry_id:264498)天然适用于追踪材料属性的变化，而[欧拉描述](@entry_id:264722)则更常用于流[体力](@entry_id:174230)学，其控制方程形式更为简洁 [@problem_id:4330717]。

#### 变形梯度

描述局部变形最核心的量是**变形梯度 (deformation gradient)** 张量 $\mathbf{F}$。它被定义为运动映射 $\boldsymbol{\chi}$ 对物质坐标 $\mathbf{X}$ 的梯度：
$$
\mathbf{F}(\mathbf{X}, t) = \nabla_{\mathbf{X}} \boldsymbol{\chi}(\mathbf{X}, t) \quad \text{或以分量形式写作} \quad F_{ij} = \frac{\partial x_i}{\partial X_j}
$$
$\mathbf{F}$ 是一个二阶张量，它包含了关于局部变形的全部信息。其物理意义在于，它将参考构型中的一个无穷小物质[线元](@entry_id:196833) $d\mathbf{X}$ 映射到当前构型中的对应[线元](@entry_id:196833) $d\mathbf{x}$：
$$
d\mathbf{x} = \mathbf{F} \, d\mathbf{X}
$$
例如，考虑一个同时经历轴向拉伸和剪切的组织，其变形映射为 $x_1 = \lambda X_1 + \Gamma X_2$, $x_2 = \lambda^{-1} X_2$, $x_3 = X_3$。通过计算各分量的偏导数，我们可以得到其变形梯度矩阵 [@problem_id:4330721]：
$$
\mathbf{F} = \begin{pmatrix} \lambda & \Gamma & 0 \\ 0 & \lambda^{-1} & 0 \\ 0 & 0 & 1 \end{pmatrix}
$$
这个矩阵清晰地展示了 $X_1$ 方向的拉伸、由 $\Gamma$ 引起的剪切以及 $X_2$ 方向的压缩。

#### 局部体积、面积和长度的变化

变形梯度 $\mathbf{F}$ 使我们能够量化变形如何改变组织的几何性质。

**体积变化**：局部体积的变化由 $\mathbf{F}$ 的行列式，即**[雅可比行列式](@entry_id:137120) (Jacobian determinant)** $J$ 来描述：
$$
J = \det(\mathbf{F})
$$
$J$ 代表了局部体积的变化率。一个在参考构型中体积为 $dV_0$ 的微元，在当前构型中其体积将变为 $dV = J \, dV_0$ [@problem_id:4330774]。对于生物组织而言，由于其含水量极高（通常超过70%），在很多情况下可以近似为**不可压缩 (incompressible)** 材料。这意味着在变形过程中其局部[体积保持](@entry_id:141001)不变，其运动学约束条件即为 $J=1$。在前面给出的拉伸剪切例子中，我们可以验证 $J = \det(\mathbf{F}) = \lambda \cdot \lambda^{-1} \cdot 1 = 1$，这表明该变形是保体积的 [@problem_id:4330721]。

**面积变化**：参考构型中的[有向面积](@entry_id:169588)微元 $d\mathbf{A} = \mathbf{N} dA$ 与当前构型中的对应微元 $d\mathbf{a} = \mathbf{n} da$ 之间的关系由著名的**[南森公式](@entry_id:195566) (Nanson's formula)** 给出：
$$
\mathbf{n} \, da = J \mathbf{F}^{-T} \mathbf{N} \, dA
$$
其中 $\mathbf{F}^{-T}$ 是 $\mathbf{F}$ 的逆之转置。这个公式在推导不同构型下物理量（如应力、通量）之间的关系时至关重要 [@problem_id:4330717] [@problem_id:4330697]。

**长度变化与应变**：为了描述材料内部的真实拉伸或压缩，我们需要一个不受[刚体转动](@entry_id:191086)影响的度量。为此，我们引入**右柯西-格林变形张量 (Right Cauchy-Green deformation tensor)** $\mathbf{C}$：
$$
\mathbf{C} = \mathbf{F}^T \mathbf{F}
$$
$\mathbf{C}$ 是一个对称正定张量，它捕捉了物质线元长度平方的变化。一个参考线元 $d\mathbf{X}$ 的长度平方为 $|d\mathbf{X}|^2 = d\mathbf{X} \cdot d\mathbf{X}$，其在当前构型中对应的线元 $d\mathbf{x} = \mathbf{F}d\mathbf{X}$ 的长度平方为：
$$
|d\mathbf{x}|^2 = (\mathbf{F}d\mathbf{X}) \cdot (\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{F}^T \mathbf{F}) d\mathbf{X} = d\mathbf{X} \cdot \mathbf{C} \, d\mathbf{X}
$$
从 $\mathbf{C}$ 中减去单位张量 $\mathbf{I}$ 可以得到一个直接衡量应变的量，即**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)** $\mathbf{E}$：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})
$$
当变形很小时，$\mathbf{E}$ 趋近于经典的线性应变张量。对于[大变形](@entry_id:167243)问题，如[软组织力学](@entry_id:199866)，使用 $\mathbf{C}$ 或 $\mathbf{E}$ 是必要的 [@problem_id:4330721]。

#### 极分解：拉伸与转动

变形梯度 $\mathbf{F}$ 可以唯一地分解为一个纯拉伸和一个[刚体转动](@entry_id:191086)的乘积，这被称为**极分解 (polar decomposition)** [@problem_id:4330761]。最常见的形式是右极分解：
$$
\mathbf{F} = \mathbf{R} \mathbf{U}
$$
这里，$\mathbf{U}$ 是**右[拉伸张量](@entry_id:193200) (right stretch tensor)**，它是一个对称正定张量，描述了在参考构型坐标系下的纯拉伸和剪切。它与[右柯西-格林张量](@entry_id:174156)直接相关，即 $\mathbf{U} = \sqrt{\mathbf{C}}$。$\mathbf{R}$ 是一个**转动张量 (rotation tensor)**，它是一个正常正交（即 $\mathbf{R}^T\mathbf{R}=\mathbf{I}$ 且 $\det(\mathbf{R})=1$）的张量，描述了材料微元在经历 $\mathbf{U}$ 的纯变形后所进行的刚体转动。

这个分解的深刻之处在于它将变形的两个基本物理过程——形状改变和方向改变——清晰地分离开来。材料线元的长度变化完全由[拉伸张量](@entry_id:193200) $\mathbf{U}$ 决定，而与转动 $\mathbf{R}$ 无关，因为转动是保长的变换。即 $|d\mathbf{x}| = |\mathbf{F}d\mathbf{X}| = |\mathbf{R}\mathbf{U}d\mathbf{X}| = |\mathbf{U}d\mathbf{X}|$。这对于理解和构建材料[本构模型](@entry_id:174726)至关重要，因为材料的储能和应力通常只与拉伸有关，而与刚体转动无关。

例如，组织中胶原纤维的拉伸就可以通过 $\mathbf{U}$ 或 $\mathbf{C}$ 来计算。如果一束纤维在参考构型中的方向由[单位向量](@entry_id:165907) $\mathbf{a}_0$ 表示，那么其拉伸比 $\lambda_f$ 的平方就是 [@problem_id:4330761]：
$$
\lambda_f^2 = \mathbf{a}_0 \cdot \mathbf{C} \, \mathbf{a}_0 = \mathbf{a}_0 \cdot \mathbf{U}^2 \, \mathbf{a}_0 = |\mathbf{U} \mathbf{a}_0|^2
$$

### 动力学：作用中的力

运动学描述了“如何动”，而动力学则研究“为何动”。它涉及作用在组织上的力以及这些力如何改变组织的运动状态。

#### [线性动量守恒](@entry_id:165717)

连续介质中的牛顿第二定律通常以**[线性动量守恒](@entry_id:165717) (balance of linear momentum)** 的形式表述，也称为**柯西第一运动定律 (Cauchy's first law of motion)**。对于空间中任意一个物质区域，其总动量的[物质导数](@entry_id:172646)等于作用在该区域上的所有外力之和。通过一系列推导，可以得到其局部（[微分](@entry_id:158422)）形式，即在[欧拉描述](@entry_id:264722)下的动量方程 [@problem_id:4330723]：
$$
\rho \frac{D\mathbf{v}}{Dt} = \nabla \cdot \boldsymbol{\sigma} + \mathbf{b}
$$
我们来逐一解析这个方程中的每一项：
- $\rho(\mathbf{x}, t)$ 是当前构型下的**质量密度**。
- $\frac{D\mathbf{v}}{Dt}$ 是速度场 $\mathbf{v}$ 的**[物质导数](@entry_id:172646) (material derivative)**，表示跟随一个物质点测得的加速度。它包括两部分：[局部加速度](@entry_id:272847) $\frac{\partial \mathbf{v}}{\partial t}$ 和[对流加速度](@entry_id:263153) $(\mathbf{v} \cdot \nabla)\mathbf{v}$。
- $\boldsymbol{\sigma}(\mathbf{x}, t)$ 是**柯西应力张量 (Cauchy stress tensor)**，它描述了材料内部的[接触力](@entry_id:165079)状态。它是一个[二阶张量](@entry_id:199780)，其分量 $\sigma_{ij}$ 表示在 $i$ 方向上作用于法向为 $j$ 方向的单位面积上的力。
- $\nabla \cdot \boldsymbol{\sigma}$ 是柯西应力张量的**散度**，代表由应力不均匀分布引起的单位体积净力。
- $\mathbf{b}(\mathbf{x}, t)$ 是**体力密度 (body force density)**，代表作用于材料体积的“超距力”，如重力（$\mathbf{b} = \rho \mathbf{g}$）。在生物组织的多相模型中，它也可以代表组分间的相互作用力，例如流体对固体基质的拖曳力 [@problem_id:4330723]。

#### 应力张量与[客观性原理](@entry_id:185412)

柯西应力 $\boldsymbol{\sigma}$ 是一个定义在当前（空间）构型上的“真实”应力。然而，在处理大变形问题时，直接使用 $\boldsymbol{\sigma}$ 会遇到困难，因为它与在参考构型中定义的应变张量（如 $\mathbf{E}$）不直接关联。因此，另外两种在参考（物质）构型中定义的[应力张量](@entry_id:148973)被引入：

1.  **[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量 (First Piola-Kirchhoff stress, PK1)** $\mathbf{P}$：它将参考构型中的[法向量](@entry_id:264185) $\mathbf{N}$ 映射为当前构型中的力。$\mathbf{P}$ 通常是非对称的。
2.  **[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量 (Second Piola-Kirchhoff stress, PK2)** $\mathbf{S}$：它将参考构型中的法向量 $\mathbf{N}$ 映射为“拉回”到参考构型中的一个[虚拟力](@entry_id:165088)。$\mathbf{S}$ 是对称的，并且与[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E}$ 是[功共轭](@entry_id:194957)的，这使得它在[超弹性](@entry_id:159356)本构理论中极为有用。

这三种[应力张量](@entry_id:148973)之间可以通过变形梯度 $\mathbf{F}$ 进行转换。其中，$\boldsymbol{\sigma}$ 和 $\mathbf{S}$ 之间的关系尤为重要 [@problem_id:4330697]：
$$
\boldsymbol{\sigma} = \frac{1}{J} \mathbf{F} \mathbf{S} \mathbf{F}^T \quad \text{(push-forward)}
$$
$$
\mathbf{S} = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T} \quad \text{(pull-back)}
$$
这些变换关系保证了无论我们选择在哪种构型下计算，力都是一个客观的物理量。

这引出了**物质框架无关性原理 (principle of material frame-indifference)**，或称**[客观性原理](@entry_id:185412) (principle of objectivity)**。该原理要求[本构关系](@entry_id:186508)（即描述材料行为的方程）不能依赖于观察者的参考系。具体来说，如果在当前变形的基础上再叠加一个[刚体运动](@entry_id:193355)（转动 $\mathbf{Q}$ 和平移 $\mathbf{c}$），材料的响应应当是等价的。这一要求对应力张量的变换方式施加了严格的约束。在这样一个叠加的[刚体运动](@entry_id:193355)下，柯西应力 $\boldsymbol{\sigma}$ 会随之转动，即 $\boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T$。而[第二皮奥拉-基尔霍夫应力](@entry_id:173163) $\mathbf{S}$，由于其定义在不随观察者改变的物质构型中，必须保持不变，即 $\mathbf{S}^* = \mathbf{S}$。正是 $\mathbf{S}$ 的这种不变性使其成为构建客观本构模型的理想选择 [@problem_id:4330697]。

### 本构模型：连接应力与应变

运动学和[动力学方程](@entry_id:751029)对于任何连续介质都是普适的，但要描述特定材料（如特定类型的生物组织）的行为，我们必须建立**本构关系 (constitutive relation)**，即连接[应力与应变](@entry_id:137374)（或[应变率](@entry_id:154778)）的方程。

#### [超弹性](@entry_id:159356)与[应变能函数](@entry_id:178435)

许多生物软组织在经历弹性变形时，其行为可以被理想化为**[超弹性](@entry_id:159356)的 (hyperelastic)**。这意味着[应力-应变关系](@entry_id:274093)可以从一个标量的**[应变能密度函数](@entry_id:755490) (strain-energy density function)** $\psi$ 中导出。这个函数代表了材料因变形而储存的单位参考体积的弹性能。

根据[客观性原理](@entry_id:185412)，应变能函数 $\psi$ 必须是一个客观标量，因此它只能通过客观的[应变度量](@entry_id:755495)来依赖于变形梯度 $\mathbf{F}$。最常见的选择是将其表示为[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 的函数，$\psi = \psi(\mathbf{C})$。

对于**各向同性 (isotropic)** 材料，其力学性质没有方向性。这意味着 $\psi$ 必须对任意坐标转动都不变，因此它只能是 $\mathbf{C}$ 的不变量的函数，即 $\psi = \psi(I_1, I_2, I_3)$，其中 $I_1 = \mathrm{tr}(\mathbf{C})$, $I_2 = \frac{1}{2}[(\mathrm{tr}(\mathbf{C}))^2 - \mathrm{tr}(\mathbf{C}^2)]$, $I_3 = \det(\mathbf{C})$ 是 $\mathbf{C}$ 的三个[主不变量](@entry_id:193522)。等价地，它可以表示为主拉伸比 $(\lambda_1, \lambda_2, \lambda_3)$ 的[对称函数](@entry_id:177113)。

#### 各向异性模型：[纤维增强](@entry_id:194439)组织

然而，绝大多数生物组织，如肌肉、肌腱、动脉壁等，由于其内部有序的微观结构（如胶原纤维束），都表现出显著的**各向异性 (anisotropy)**。它们的力学响应强烈依赖于加载方向。

为了在宏观[连续模](@entry_id:158807)型中描述这种各向异性，我们引入了**结构张量 (structural tensors)** 的概念。对于一个具有单一优先纤维方向的组织（即**横观各向同性, transversely isotropic**），我们可以在参考构型中定义一个[单位向量](@entry_id:165907) $\mathbf{a}_0$ 来表示该纤维方向。然后，我们可以构建额外的、依赖于方向的“伪不变量”来构建[应变能函数](@entry_id:178435)。最重要的两个是 [@problem_id:4330750]：
- $I_4 = \mathbf{a}_0 \cdot \mathbf{C} \, \mathbf{a}_0 = \lambda_f^2$：这个不变量直接量度了纤维方向上的拉伸的平方。
- $I_5 = \mathbf{a}_0 \cdot \mathbf{C}^2 \, \mathbf{a}_0$：这个不变量包含了纤维方向与[剪切变形](@entry_id:170920)的耦合信息。

一个典型的横观[各向同性材料](@entry_id:170678)的应变能函数可以写成 $\psi(I_1, I_2, I_4, I_5)$。一个常见且实用的简化形式是将其分解为基质的各向同性[部分和](@entry_id:162077)纤维的各向异性部分之和，例如 [@problem_id:4330750]：
$$
\psi(I_1, I_4) = \psi_{\text{iso}}(I_1) + \psi_{\text{aniso}}(I_4)
$$
例如，我们可以用一个[新胡克模型](@entry_id:165881)描述基质，用一个指数函数描述纤维在拉伸时表现出的高度非线性“[应变硬化](@entry_id:160669)”行为：
$$
\psi(I_1, I_4) = \frac{\mu}{2}(I_1 - 3) + \frac{k_1}{2k_2} \left[ \exp\left( k_2(I_4-1)^2 \right) - 1 \right]
$$
其中 $\mu, k_1, k_2$ 是材料参数。这种形式的函数能够很好地捕捉[纤维增强](@entry_id:194439)组织在沿纤维方向拉伸时刚度急剧增加的典型特征。

许多著名的[唯象模型](@entry_id:273816)，如 **Fung 指数模型**和 **Ogden 模型**，都可以通过选择不同的函数形式以及是否包含各向异性不变量来描述组织的[非线性力学](@entry_id:178303)行为 [@problem_id:4330728]。Fung 模型 $\psi = \frac{c}{2}(e^Q - 1)$ 通过在指数 $Q$ 中包含 $I_4, I_5$ 等伪不变量可以很自然地描述各向异性。而标准的 Ogden 模型 $\psi = \sum_{i=1}^N \frac{\mu_i}{\alpha_i}(\lambda_1^{\alpha_i} + \lambda_2^{\alpha_i} + \lambda_3^{\alpha_i} - 3)$ 是主拉伸比的[对称函数](@entry_id:177113)，因此是各向同性的，除非额外加入依赖于方向的项 [@problem_id:4330728]。

### 组织动力学中的高级机制

除了基本的弹塑性变形，生物组织的动力学行为还涉及更复杂的、与其生命活动密切相关的过程。

#### 混合物理论与多相组织

生物组织本质上是多[相混合](@entry_id:199798)物，主要由细胞、细胞外基质（如胶原和弹性蛋白）以及间质流体组成。将组织视为单一连续体是一种简化。更精确的模型采用**混合物理论 (mixture theory)**，将组织视为多个连续介质的“重叠共存” [@problem_id:4330705]。

在混合物理论中，每个组分（如固体基质 $s$ 和流体 $f$）都有其自身的物理量：
- **体积分数** $\phi_i$：组分 $i$ 在[代表性体积元](@entry_id:164290)中占的[体积分数](@entry_id:756566)，满足 $\sum_i \phi_i = 1$。
- **真实密度** $\rho_i$：组分 $i$ 自身的密度（单位组分体积的质量）。
- **偏密度** $\rho_i^p = \phi_i \rho_i$：组分 $i$ 在单位混合物体积中的质量。
- **速度** $\mathbf{v}_i$：组分 $i$ 的速度场。

混合物的总密度是各偏密度的和：$\rho = \sum_i \phi_i \rho_i$。混合物的**[质心速度](@entry_id:175479) (barycentric velocity)** $\mathbf{v}$ 是由动量相加性定义的质量加权[平均速度](@entry_id:267649)：
$$
\mathbf{v} = \frac{\sum_i \phi_i \rho_i \mathbf{v}_i}{\sum_i \phi_i \rho_i}
$$
各组分相对于[质心速度](@entry_id:175479)的运动称为**扩散 (diffusion)**。混合物理论为研究诸如多孔弹性（描述流体在可变形[多孔固体](@entry_id:154776)中的流动，是模拟软骨等组织的关键）等现象提供了坚实的理论基础。例如，当一个含流体的组织变形时，其总体积变化 $J$ 会改变固相和流相的体积分数。若固相组分本身不可压缩，则其当前[体积分数](@entry_id:756566) $n^s$ 与初始体积分数 $n_0^s$ 之间的关系为 $n^s = n_0^s / J$ [@problem_id:4330774]。

#### 生长与重塑的运动学

生物组织是“活”的材料，它们可以通过细胞增殖、细胞外基质沉积或降解、细胞尺寸变化等方式进行生长、萎缩和重塑。这些过程改变了组织的“天然”或“无应力”构型。**形态[弹性理论](@entry_id:184142) (morphoelasticity)** 采用变形梯度的**[乘法分解](@entry_id:199514) (multiplicative decomposition)** 来描述这一现象 [@problem_id:4330729]：
$$
\mathbf{F} = \mathbf{F}_e \mathbf{F}_g
$$
这个分解的物理解释如下：
1.  **生长张量 $\mathbf{F}_g$**：代表由于[生物过程](@entry_id:164026)引起的局部、无应力的材料度量变化。例如，各向同性生长可以表示为 $\mathbf{F}_g = \gamma \mathbf{I}$，其中 $\gamma > 1$ 表示体积增加。重要的是，由于生长在空间上可能是不均匀的，$\mathbf{F}_g$ 通常不是一个相容的变形梯度（即它不能被积分为一个全局的无应力[位移场](@entry_id:141476)）。想象一下在一个甜甜圈的外圈进行不均匀的生长，如果不产生[内应力](@entry_id:193721)，它将无法保持其环形形状。
2.  **弹性张量 $\mathbf{F}_e$**：代表为了将这个在概念上“生长”了的、不相容的[中间构型](@entry_id:193000)“嵌入”到现实的欧几里得空间中，并满足边界条件和外[力平衡](@entry_id:267186)，所必须发生的弹性变形。

所有的机械应力和储存的弹性势能都只由弹性变形 $\mathbf{F}_e$ 产生。[应变能函数](@entry_id:178435)因此写为 $\psi = \psi(\mathbf{C}_e)$，其中 $\mathbf{C}_e = \mathbf{F}_e^T \mathbf{F}_e$。由于 $\mathbf{F}_g$ 的不相容性，即使在没有外力的情况下，组织内部也会存在由 $\mathbf{F}_e$ 引起的**残余应力 (residual stress)**。

在许多模型中，弹性响应被假定为不可压缩的，即 $\det(\mathbf{F}_e) = 1$。在这种情况下，组织的所有体积变化都归因于生长过程，即 $J = \det(\mathbf{F}) = \det(\mathbf{F}_e)\det(\mathbf{F}_g) = \det(\mathbf{F}_g)$。这个强大的框架能够解释和预测由生长引起的形状改变和[内应力](@entry_id:193721)分布，在发育生物学、肿瘤生长和组织工程等领域有广泛应用。