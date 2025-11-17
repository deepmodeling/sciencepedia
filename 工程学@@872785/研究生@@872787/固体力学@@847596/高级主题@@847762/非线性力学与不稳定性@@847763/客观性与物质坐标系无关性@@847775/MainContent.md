## 引言
在连续介质力学中，本构关系是连接变形与应力的桥梁，它定义了特定材料的力学行为。然而，一个数学上构造出的[本构方程](@entry_id:138559)若要真实地描述物理世界，就必须遵循一系列基本物理公理。在这些公理中，物质[坐标系](@entry_id:156346)无关性原理（或称[客观性原理](@entry_id:185412)）占据了核心地位。它断言，材料的内在物理响应不应随观察者的改变而改变——这是一个看似简单却影响深远的约束。若缺乏这一原理，我们构建的模型可能会预测出仅因观察者旋转就会产生应力的荒谬结果，从而失去了物理意义。

本文旨在系统地剖析[客观性原理](@entry_id:185412)。我们将从其根本出发，引领读者深入理解这一概念的内涵与外延。
- 在“原理与机制”一章中，我们将建立该原理的严谨数学框架，推导关键物理量在观察者变换下的客观性，并展示它如何从根本上塑造[本构方程](@entry_id:138559)的形式。
- 接着，在“应用与交叉学科联系”一章中，我们将展示[客观性原理](@entry_id:185412)在固体力学、[流体力学](@entry_id:136788)以及计算模拟等领域的广泛应用，阐明它为何是构建可靠模型的基石。
- 最后，“动手实践”部分将通过具体的编程与推导练习，帮助您将抽象的理论转化为解决实际问题的能力。

通过本次学习，您将掌握现代本构理论的核心准则之一，为更高阶的研究与应用打下坚实的基础。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，[本构关系](@entry_id:186508)描述了材料如何响应外部载荷和变形。然而，并非任何数学上看似合理的[本构方程](@entry_id:138559)都具有物理意义。为了确保物理实在性，[本构方程](@entry_id:138559)必须遵循若干基本物理原理。其中，**物质[坐标系](@entry_id:156346)无关性原理** (Principle of Material Frame-Indifference)，或称**[客观性原理](@entry_id:185412)** (Principle of Objectivity)，是最为根本的公理之一。它断言，材料的本构响应——即其内在的物理特性——不能依赖于观察者。本章将系统地阐述该原理的数学形式、其对本构理论的深刻影响，并将其与[材料对称性](@entry_id:190289)的概念加以区分。

### 物质[坐标系](@entry_id:156346)无关性原理 (客观性)

[客观性原理](@entry_id:185412)的核心思想是：物理定律对于所有惯性或[非惯性参考系](@entry_id:169712)的观察者都应具有相同的形式。在[连续介质力学](@entry_id:155125)的背景下，这意味着材料的本构行为（例如，应力如何依赖于变形）必须独立于观察者自身的刚体运动（平移和旋转）。

#### 数学形式化

为了精确地表述这一原理，我们考虑两个观察者。第一个观察者在“实验室”[参考系](@entry_id:169232)中观察一个连续体的运动，并将空间中的一个物质点在时刻 $t$ 的位置描述为 $\mathbf{x}$。第二个观察者相对于第一个观察者进行时变的刚体运动。在同一时刻 $t$，第二个观察者观察到的同一点的位置为 $\mathbf{x}^*$。这两个位置矢量之间的关系可以表示为：

$$
\mathbf{x}^*(t) = \mathbf{c}(t) + \mathbf{Q}(t)\mathbf{x}(t)
$$

其中，$\mathbf{c}(t)$ 是一个时变的平移矢量，$\mathbf{Q}(t)$ 是一个时变的**正常正交张量**（proper orthogonal tensor），即 $\mathbf{Q}(t) \in \mathrm{SO}(3)$，其中 $\mathrm{SO}(3)$ 是[三维特殊正交群](@entry_id:138200)，满足 $\mathbf{Q}\mathbf{Q}^T = \mathbf{I}$ 且 $\det(\mathbf{Q})=1$。这个变换被称为**叠加刚体运动** (superposed rigid body motion)。

这一观察者变换直接影响了所有[运动学](@entry_id:173318)和动力学量的数学表示。[客观性原理](@entry_id:185412)要求我们推导出各个物理量在不同观察者[坐标系](@entry_id:156346)下的转换关系。

- **变形梯度 (Deformation Gradient) $\mathbf{F}$**:
变形梯度定义为当前构形位置对参考构形位置的梯度，$\mathbf{F} = \nabla_{\mathbf{X}}\mathbf{x}$。在星号[坐标系](@entry_id:156346)中，$\mathbf{F}^* = \nabla_{\mathbf{X}}\mathbf{x}^* = \nabla_{\mathbf{X}}(\mathbf{c} + \mathbf{Q}\mathbf{x})$。由于 $\mathbf{Q}$ 和 $\mathbf{c}$ 仅依赖于时间 $t$ 而不依赖于[参考位](@entry_id:754187)置 $\mathbf{X}$，我们得到：
$$
\mathbf{F}^* = \mathbf{Q}(\nabla_{\mathbf{X}}\mathbf{x}) = \mathbf{Q}\mathbf{F}
$$
这个关系表明，变形梯度 $\mathbf{F}$ 不是一个客观张量，它的表示会随着观察者的旋转而改变。

- **[速度梯度](@entry_id:261686) (Velocity Gradient) $\mathbf{L}$**:
[空间速度梯度](@entry_id:187198)定义为 $\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$。为了找到其变换规律，我们首先对 $\mathbf{F}^*$ 求时间导数：$\dot{\mathbf{F}}^* = \dot{\mathbf{Q}}\mathbf{F} + \mathbf{Q}\dot{\mathbf{F}}$。星号[坐标系](@entry_id:156346)下的[速度梯度](@entry_id:261686)为 $\mathbf{L}^* = \dot{\mathbf{F}}^*(\mathbf{F}^*)^{-1}$。代入 $\mathbf{F}^*$ 及其导数的表达式，我们有：
$$
\mathbf{L}^* = (\dot{\mathbf{Q}}\mathbf{F} + \mathbf{Q}\dot{\mathbf{F}})(\mathbf{Q}\mathbf{F})^{-1} = (\dot{\mathbf{Q}}\mathbf{F} + \mathbf{Q}\dot{\mathbf{F}})(\mathbf{F}^{-1}\mathbf{Q}^T) = \dot{\mathbf{Q}}\mathbf{Q}^T + \mathbf{Q}(\dot{\mathbf{F}}\mathbf{F}^{-1})\mathbf{Q}^T
$$
最终得到[速度梯度](@entry_id:261686)的变换关系 [@problem_id:2666734]：
$$
\mathbf{L}^* = \mathbf{Q}\mathbf{L}\mathbf{Q}^T + \dot{\mathbf{Q}}\mathbf{Q}^T
$$
由于存在附加项 $\dot{\mathbf{Q}}\mathbf{Q}^T$（代表两个观察者[参考系](@entry_id:169232)之间的相对自旋），速度梯度 $\mathbf{L}$ 显然不是一个客观张量。

- **变形率张量 (Rate-of-Deformation Tensor) $\mathbf{D}$**:
变形率张量是[速度梯度](@entry_id:261686)的对称部分，$\mathbf{D} = \frac{1}{2}(\mathbf{L}+\mathbf{L}^T)$。其变换规律可以通过对 $\mathbf{L}^*$ 取对称部分得到：
$$
\mathbf{D}^* = \frac{1}{2}(\mathbf{L}^* + (\mathbf{L}^*)^T) = \frac{1}{2}[(\mathbf{Q}\mathbf{L}\mathbf{Q}^T + \dot{\mathbf{Q}}\mathbf{Q}^T) + (\mathbf{Q}\mathbf{L}\mathbf{Q}^T + \dot{\mathbf{Q}}\mathbf{Q}^T)^T]
$$
由于 $\dot{\mathbf{Q}}\mathbf{Q}^T$ 是一个[反对称张量](@entry_id:199349)（即 $(\dot{\mathbf{Q}}\mathbf{Q}^T)^T = -\dot{\mathbf{Q}}\mathbf{Q}^T$），附加项在对称化过程中被消除了 [@problem_id:2666734]。因此，我们得到：
$$
\mathbf{D}^* = \frac{1}{2}(\mathbf{Q}\mathbf{L}\mathbf{Q}^T + \mathbf{Q}\mathbf{L}^T\mathbf{Q}^T) = \mathbf{Q}\frac{1}{2}(\mathbf{L}+\mathbf{L}^T)\mathbf{Q}^T = \mathbf{Q}\mathbf{D}\mathbf{Q}^T
$$
这个结果表明，**变形率张量 $\mathbf{D}$ 是一个客观的[二阶张量](@entry_id:199780)**。同样地，可以证明[自旋张量](@entry_id:187346) $\mathbf{W} = \frac{1}{2}(\mathbf{L}-\mathbf{L}^T)$ 不是客观的。

- **柯西-格林张量 (Cauchy-Green Tensors)**:
[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^T\mathbf{F}$ 在观察者变换下的形式为：
$$
\mathbf{C}^* = (\mathbf{F}^*)^T\mathbf{F}^* = (\mathbf{Q}\mathbf{F})^T(\mathbf{Q}\mathbf{F}) = \mathbf{F}^T\mathbf{Q}^T\mathbf{Q}\mathbf{F} = \mathbf{F}^T\mathbf{I}\mathbf{F} = \mathbf{C}
$$
$\mathbf{C}$ 在观察者变换下保持不变，它是一个**客观的物质张量**。而[左柯西-格林张量](@entry_id:186163) $\mathbf{B} = \mathbf{F}\mathbf{F}^T$ 的变换形式为：
$$
\mathbf{B}^* = \mathbf{F}^*(\mathbf{F}^*)^T = (\mathbf{Q}\mathbf{F})(\mathbf{Q}\mathbf{F})^T = \mathbf{Q}\mathbf{F}\mathbf{F}^T\mathbf{Q}^T = \mathbf{Q}\mathbf{B}\mathbf{Q}^T
$$
$\mathbf{B}$ 的变换方式与 $\mathbf{D}$ 相同，是一个**客观的[空间张量](@entry_id:185799)**。

- **柯西应力张量 (Cauchy Stress Tensor) $\boldsymbol{\sigma}$**:
柯西应力张量必须是客观的。这可以通过考虑作用在任意微元面上的[面力矢量](@entry_id:189429) $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$ 来论证。面力 $\mathbf{t}$ 和法向 $\mathbf{n}$ 都是物理矢量，它们在观察者变换下遵循 $\mathbf{t}^* = \mathbf{Q}\mathbf{t}$ 和 $\mathbf{n}^* = \mathbf{Q}\mathbf{n}$。根据柯西关系式，在星号[坐标系](@entry_id:156346)中应有 $\mathbf{t}^* = \boldsymbol{\sigma}^*\mathbf{n}^*$。代入变换关系：
$$
\mathbf{Q}\mathbf{t} = \boldsymbol{\sigma}^*(\mathbf{Q}\mathbf{n}) \implies \mathbf{Q}(\boldsymbol{\sigma}\mathbf{n}) = \boldsymbol{\sigma}^*(\mathbf{Q}\mathbf{n})
$$
由于该式对任意法向 $\mathbf{n}$ 均成立，我们必然得到 $\mathbf{Q}\boldsymbol{\sigma} = \boldsymbol{\sigma}^*\mathbf{Q}$，即：
$$
\boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T
$$
这确认了柯西应力是一个客观的空间二阶张量。

### 对本构模型的约束

[客观性原理](@entry_id:185412)对本构模型的形式施加了强大的约束。一个本构律，例如 $\boldsymbol{\sigma} = \mathcal{T}(\text{运动学量})$，必须对所有观察者都具有相同的函数形式 $\mathcal{T}$。这意味着，将变换后的量代入函数 $\mathcal{T}$，其结果必须与直接变换原始结果相一致。

#### 标量本构函数（例如[储能函数](@entry_id:197811)）

考虑一个依赖于变形梯度的[储能函数](@entry_id:197811) $\psi = \psi(\mathbf{F})$。客观性要求对于任意的 $\mathbf{Q} \in \mathrm{SO}(3)$，函数值不应改变：
$$
\psi(\mathbf{F}^*) = \psi(\mathbf{Q}\mathbf{F}) = \psi(\mathbf{F})
$$
这一要求极大地限制了 $\psi$ 的函数形式。利用**极分解定理** (polar decomposition theorem)，任何可逆的变形梯度 $\mathbf{F}$ 都可以唯一地分解为一个[旋转张量](@entry_id:191990) $\mathbf{R} \in \mathrm{SO}(3)$ 和一个[对称正定](@entry_id:145886)的[右伸长张量](@entry_id:193756) $\mathbf{U}$，即 $\mathbf{F} = \mathbf{R}\mathbf{U}$。在客观性条件中，我们可以取 $\mathbf{Q} = \mathbf{R}^T$，从而得到 [@problem_id:2666729]：
$$
\psi(\mathbf{F}) = \psi(\mathbf{R}\mathbf{U}) = \psi(\mathbf{R}^T(\mathbf{R}\mathbf{U})) = \psi(\mathbf{U})
$$
这表明，一个客观的标量函数只能通过其纯变形部分（[右伸长张量](@entry_id:193756) $\mathbf{U}$）依赖于变形梯度 $\mathbf{F}$。由于 $\mathbf{U} = \sqrt{\mathbf{C}}$ 是[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 的唯一正定平方根，这等价于说[储能函数](@entry_id:197811)必须是 $\mathbf{C}$ 的函数：
$$
\psi(\mathbf{F}) = \hat{\psi}(\mathbf{C}) = \hat{\psi}(\mathbf{F}^T\mathbf{F})
$$
这种形式被称为[本构方程](@entry_id:138559)的**简约形式** (reduced form)。任何直接依赖于非客观量 $\mathbf{F}$ 的形式，例如 $\psi = \alpha\,\mathrm{tr}(\mathbf{F})$，都将违反[客观性原理](@entry_id:185412)，因而是不符合物理的 [@problem_id:2666732]。

#### 张量本构函数（例如[应力-应变关系](@entry_id:274093)）

对于张量值的本构函数，如柯西应力 $\boldsymbol{\sigma}$，[客观性原理](@entry_id:185412)要求：
$$
\mathcal{T}(\text{变换后的运动学量}) = \mathbf{Q}\,\mathcal{T}(\text{原始运动学量})\,\mathbf{Q}^T
$$
让我们通过几个例子来检验这一准则 [@problem_id:2666736]：

- **反例 1: St. Venant-Kirchhoff 模型**:
一个常见的[线性弹性](@entry_id:166983)模型（通常用于小变形）若被错误地推广到大变形，可能会写成 $\boldsymbol{\sigma} = \lambda\,\mathrm{tr}(\mathbf{E})\,\mathbf{I} + 2\,\mu\,\mathbf{E}$，其中 $\mathbf{E} = \frac{1}{2}(\mathbf{C}-\mathbf{I})$ 是[格林-拉格朗日应变张量](@entry_id:187745)。由于 $\mathbf{E}$ 是一个客观的物质张量（$\mathbf{E}^* = \mathbf{E}$），该本构律在变换后的[坐标系](@entry_id:156346)中预测的应力为 $\boldsymbol{\sigma}^*_{\text{law}} = \boldsymbol{\sigma}$。然而，客观性要求应力变换为 $\mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T$。除非 $\mathbf{Q}=\mathbf{I}$ 或 $\boldsymbol{\sigma}$ 是球张量，否则 $\boldsymbol{\sigma} \neq \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T$。因此，这个模型将[空间张量](@entry_id:185799)（$\boldsymbol{\sigma}$）与物质张量（$\mathbf{E}$）直接等同起来，违反了客观性。

- **正例 1: [牛顿流体](@entry_id:263796) (Newtonian Fluid)**:
对于[牛顿流体](@entry_id:263796)，[本构关系](@entry_id:186508)为 $\boldsymbol{\sigma} = -p\mathbf{I} + 2\eta\mathbf{D}$，其中 $p$ 是客观标量压力，$\eta$ 是粘度。在观察者变换下，我们有 $\boldsymbol{\sigma}^*_{\text{law}} = -p^*\mathbf{I}^* + 2\eta\mathbf{D}^* = -p\mathbf{I} + 2\eta(\mathbf{Q}\mathbf{D}\mathbf{Q}^T)$。这与直接变换原始应力得到的结果 $\mathbf{Q}(-p\mathbf{I} + 2\eta\mathbf{D})\mathbf{Q}^T = -p\mathbf{I} + 2\eta\mathbf{Q}\mathbf{D}\mathbf{Q}^T$ 完全一致。因此，该模型是客观的。

- **正例 2: [超弹性材料](@entry_id:190241) (Hyperelasticity)**:
从客观的[储能函数](@entry_id:197811) $\psi = \hat{\psi}(\mathbf{C})$ 出发，可以通过能量共轭关系推导出客观的应力表达式。一个关键的结果是 **Doyle-Ericksen 公式**：
$$
\boldsymbol{\sigma} = \frac{2}{J} \mathbf{F} \frac{\partial \hat{\psi}(\mathbf{C})}{\partial \mathbf{C}} \mathbf{F}^T
$$
其中 $J = \det(\mathbf{F})$。我们可以验证这个表达式是客观的。变换后的表达式为：
$$
\boldsymbol{\sigma}^*_{\text{law}} = \frac{2}{J^*} \mathbf{F}^* \frac{\partial \hat{\psi}(\mathbf{C}^*)}{\partial \mathbf{C}^*} (\mathbf{F}^*)^T = \frac{2}{J} (\mathbf{Q}\mathbf{F}) \frac{\partial \hat{\psi}(\mathbf{C})}{\partial \mathbf{C}} (\mathbf{Q}\mathbf{F})^T = \mathbf{Q} \left( \frac{2}{J} \mathbf{F} \frac{\partial \hat{\psi}(\mathbf{C})}{\partial \mathbf{C}} \mathbf{F}^T \right) \mathbf{Q}^T = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T
$$
此式完全满足客观性要求。这里的 $\mathbf{F}(\dots)\mathbf{F}^T$ 结构是一种将物质构形下的响应（$\partial\hat{\psi}/\partial\mathbf{C}$）**推前** (push-forward) 到当前空间构形的标准方法。

#### 关于率形式[本构关系](@entry_id:186508)的问题

许多材料模型（如塑性力学和一些[粘弹性模型](@entry_id:175352)）采用率形式的[本构关系](@entry_id:186508)。一个看似简单的关系是 $\dot{\boldsymbol{\sigma}} = \mathbb{C}:\mathbf{D}$，其中 $\dot{(\cdot)}$ 是[物质时间导数](@entry_id:190892)。然而，这违反了客观性。因为柯西应力 $\boldsymbol{\sigma}$ 的[物质时间导数](@entry_id:190892)不是客观的。通过对 $\boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T$ 求时间导数，我们得到：
$$
\dot{\boldsymbol{\sigma}}^* = \dot{\mathbf{Q}}\boldsymbol{\sigma}\mathbf{Q}^T + \mathbf{Q}\dot{\boldsymbol{\sigma}}\mathbf{Q}^T + \mathbf{Q}\boldsymbol{\sigma}\dot{\mathbf{Q}}^T
$$
这表明 $\dot{\boldsymbol{\sigma}}$ 的变换除了标准的[张量变换](@entry_id:183453)项 $\mathbf{Q}\dot{\boldsymbol{\sigma}}\mathbf{Q}^T$ 外，还包含了与观察者自旋 $\dot{\mathbf{Q}}$ 相关的附加项。因此，任何使用简单[物质时间导数](@entry_id:190892)的本构律都是非客观的 [@problem_id:2666736]。这一困境催生了各种**[客观应力率](@entry_id:199282)** (objective stress rates) 的定义，例如 [Jaumann 率](@entry_id:185572)、Green-Naghdi 率和 Truesdell 率，它们通过从物质导数中减去特定的自旋项来构造客观的率度量。

### 客观性与[材料对称性](@entry_id:190289)的区别

客观性与**[材料对称性](@entry_id:190289)** (material symmetry) 是两个必须严格区分的概念 [@problem_id:2666735] [@problem_id:2666730]。

- **客观性 (Material Frame-Indifference)** 是一个普适的物理原理，适用于所有材料。它关注的是在**当前（空间）构形**上叠加一个刚体运动，即改变观察者。数学上，这对应于对变形梯度进行**左乘**：$\mathbf{F} \to \mathbf{Q}\mathbf{F}$。

- **[材料对称性](@entry_id:190289)** 描述的是材料本身的内在属性。它关注的是在**参考（物质）构形**中进行刚体旋转，材料的响应是否改变。如果存在一个旋转 $\mathbf{H}$，使得旋转后的参考构形与原始构形在物理上无法区分，那么 $\mathbf{H}$ 就属于该材料的[对称群](@entry_id:146083) $\mathcal{G}$。数学上，这对应于对变形梯度进行**右乘**：$\mathbf{F} \to \mathbf{F}\mathbf{H}$。

对于一个[超弹性材料](@entry_id:190241)，客观性要求 $\psi(\mathbf{Q}\mathbf{F}) = \psi(\mathbf{F})$，而[材料对称性](@entry_id:190289)要求 $\psi(\mathbf{F}\mathbf{H}) = \psi(\mathbf{F})$ 对所有 $\mathbf{H} \in \mathcal{G}$ 成立。

- **各向同性 (Isotropy)**: 如果材料在所有方向上都具有相同的性质，其[对称群](@entry_id:146083)就是整个[正交群](@entry_id:152531) $\mathcal{G} = \mathrm{SO}(3)$。对于一个客观的[各向同性材料](@entry_id:170678)，其[储能函数](@entry_id:197811) $\psi = \hat{\psi}(\mathbf{C})$ 必须满足 $\hat{\psi}(\mathbf{C}) = \hat{\psi}(\mathbf{H}^T\mathbf{C}\mathbf{H})$ 对所有 $\mathbf{H} \in \mathrm{SO}(3)$ 成立。根据[张量表示](@entry_id:180492)定理，这意味着 $\hat{\psi}$ 只能是 $\mathbf{C}$ 的**[主不变量](@entry_id:193522)** (principal invariants) 的函数 [@problem_id:2666729]：
    - $I_1(\mathbf{C}) = \mathrm{tr}(\mathbf{C})$
    - $I_2(\mathbf{C}) = \frac{1}{2}[(\mathrm{tr}\mathbf{C})^2 - \mathrm{tr}(\mathbf{C}^2)]$
    - $I_3(\mathbf{C}) = \det(\mathbf{C})$
因此，各向同性客观材料的[储能函数](@entry_id:197811)具有形式 $\psi = \bar{\psi}(I_1, I_2, I_3)$。

- **各向异性 (Anisotropy)**: 如果材料具有一个或多个优势方向（例如[纤维增强复合材料](@entry_id:194995)），其[对称群](@entry_id:146083) $\mathcal{G}$ 只是 $\mathrm{SO}(3)$ 的一个[子群](@entry_id:146164)。例如，对于沿参考方向 $\mathbf{a}_0$ 的**横观各向同性** (transversely isotropic) 材料，其对称群包含所有绕 $\mathbf{a}_0$ 轴的旋转。为了描述这种材料，需要引入**结构张量** (structural tensor)，如 $\mathbf{A} = \mathbf{a}_0 \otimes \mathbf{a}_0$。此时，[储能函数](@entry_id:197811) $\psi$ 不仅依赖于 $\mathbf{C}$ 的[不变量](@entry_id:148850)，还依赖于 $\mathbf{C}$ 和 $\mathbf{A}$ 的混合[不变量](@entry_id:148850)。一个完备的函数基包含五个[不变量](@entry_id:148850) [@problem_id:2666730]：$I_1, I_2, I_3$ 以及两个额外的伪[不变量](@entry_id:148850)：
    - $I_4 = \mathrm{tr}(\mathbf{C}\mathbf{A}) = \mathbf{a}_0 \cdot \mathbf{C}\mathbf{a}_0$
    - $I_5 = \mathrm{tr}(\mathbf{C}^2\mathbf{A}) = \mathbf{a}_0 \cdot \mathbf{C}^2\mathbf{a}_0$

### 扩展与高等应用：Cosserat 连续体

[客观性原理](@entry_id:185412)的普适性在于它可以应用于更广义的连续介质理论，如 Cosserat 或[微极连续体](@entry_id:751972)理论。这类理论适用于描述具有内部微观结构的材料，例如[颗粒材料](@entry_id:750005)、[多孔介质](@entry_id:154591)或液晶。

在 Cosserat 理论中，每个物质点除了具有平移自由度（通过速度矢量 $\boldsymbol{v}$ 描述）外，还具有独立的[转动自由度](@entry_id:141502)，由一个微[旋转张量](@entry_id:191990) $\boldsymbol{R} \in \mathrm{SO}(3)$ 描述。[客观性原理](@entry_id:185412)同样适用于这个扩展的[运动学](@entry_id:173318)框架 [@problem_id:2666732]。

- **广义运动学和动力学量的变换**:
    - 微[旋转张量](@entry_id:191990) $\boldsymbol{R}$ 描述了微观结构在空间中的方向，它是一个客观量，其变换规律为 $\boldsymbol{R}^* = \mathbf{Q}\boldsymbol{R}$。
    - 与[微旋转](@entry_id:184355)相共轭的应力偶张量 $\boldsymbol{\mu}$ 也必须是客观的，其变换规律为 $\boldsymbol{\mu}^* = \mathbf{Q}\boldsymbol{\mu}\mathbf{Q}^T$。
- **[非对称应力张量](@entry_id:184161)**: Cosserat 理论的一个显著特征是，由于存在应力偶，角动量守恒不再要求柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 是对称的。$\boldsymbol{\sigma}$ 的反对称部分与应力偶的散度[相平衡](@entry_id:136822)。这是理论的内禀特征，而非违反客观性。
- **客观本构关系**: 构造 Cosserat 材料的[本构关系](@entry_id:186508)同样需要遵循客观性。例如，[储能函数](@entry_id:197811)可以依赖于客观的[应变度量](@entry_id:755495)。由于 $\mathbf{F}$ 和 $\boldsymbol{R}$ 都不是物质张量，我们需要构造它们的组合，例如相对变形张量 $\boldsymbol{R}^T\mathbf{F}$。或者，可以构造完全客观的物质张量作为函数的宗量，例如 $\boldsymbol{R}^T\mathbf{B}\boldsymbol{R}$ 和 $\boldsymbol{R}^T(\mathrm{Curl}\,\boldsymbol{R})$，其中 $\mathrm{Curl}$ 是对[张量场](@entry_id:190170)的[旋度算子](@entry_id:184984)。任何依赖于这些客观宗量的标量函数都将自动满足客观性要求 [@problem_id:2666732]。

总之，物质[坐标系](@entry_id:156346)无关性原理不仅是一个抽象的哲学要求，更是一个强大的数学工具。它深刻地塑造了现代连续介质力学的本构理论，为我们筛选物理上合理的模型、理解[材料对称性](@entry_id:190289)以及发展更高级的力学理论提供了坚实的理论基石。