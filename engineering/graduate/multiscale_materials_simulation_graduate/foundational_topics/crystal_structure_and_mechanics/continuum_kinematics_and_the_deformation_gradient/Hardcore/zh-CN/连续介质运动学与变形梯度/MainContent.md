## 引言
在理解物质世界如何响应外力而运动和变形时，建立一个精确描述其几何变化的框架是第一步。这就是连续介质运动学的核心任务。然而，当变形不再微小时，传统的线性应变理论便会失效，我们需要一个更强大的数学工具来捕捉复杂的拉伸、剪切和旋转。这个知识上的空白正是由“变形梯度”这一核心概念来填补的。变形梯度张量不仅是描述从初始状态到当前状态局部映射的数学工具，更是连接运动学、材料本构关系和多尺度物理的桥梁。

本文将引导您深入理解连续介质运动学。在“原理与机制”一章中，我们将奠定坚实的数学基础，从运动的定义出发，引入变形梯度，并推导出应变、旋转和变形率等关键量。接着，在“应用与跨学科连接”一章，我们将超越理论，探索变形梯度如何在固体力学、材料科学、生物力学乃至计算科学中，作为统一的语言来解决复杂的实际问题。最后，通过“动手实践”部分的一系列练习，您将有机会亲手应用这些概念，将理论知识转化为解决问题的实践能力。

## 原理与机制

在连续介质力学中，运动学是研究物体变形和流动的几何学，而不考虑引起这些运动的力。本章的目标是建立一个精确的数学框架来描述一个连续体从其初始构形到其当前构形的映射。我们将引入变形梯度作为这一描述的核心，并从它出发推导出各种应变和应变率的度量。理解这些运动学量及其在不同观察者参考系下的变换性质，对于构建适用于大变形和复杂加载路径的材料本构模型至关重要。

### 运动、构形和位移

为了描述一个连续体的运动，我们首先需要一个参考系。我们选择一个固定的、通常是未变形的状态作为 **参考构形**（reference configuration），记为 $\mathcal{B}_0$。物体中的任何一个物质点都可以通过其在参考构形中的位置矢量 $\mathbf{X}$ 来唯一标识。这个矢量 $\mathbf{X}$ 被称为 **物质坐标**（material coordinate）或拉格朗日坐标。

随着时间的推移，物体运动并变形。在任意时刻 $t$，物体所占据的空间区域被称为 **当前构形**（current configuration），记为 $\mathcal{B}_t$。物质点 $\mathbf{X}$ 在时刻 $t$ 的空间位置由矢量 $\mathbf{x}$ 给出，它被称为 **空间坐标**（spatial coordinate）或欧拉坐标。

物体的 **运动**（motion）是一个映射 $\boldsymbol{\chi}$，它将每个物质点的参考位置 $\mathbf{X}$ 和时间 $t$ 映射到其当前位置 $\mathbf{x}$：
$$
\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)
$$
这个映射描述了整个物体随时间的完整运动学历史。在任何固定的时刻 $t$，映射 $\boldsymbol{\chi}(\cdot, t)$ 将参考构形 $\mathcal{B}_0$ 中的所有点映射到当前构形 $\mathcal{B}_t$。因此，$\mathcal{B}_t = \boldsymbol{\chi}(\mathcal{B}_0, t)$ [@problem_id:3798599]。我们假设这个映射是光滑且可逆的，这意味着物质不会相互穿透，并且在每个时刻我们都能从当前位置找到其唯一的初始位置 $\mathbf{X} = \boldsymbol{\chi}^{-1}(\mathbf{x}, t)$。

物理量（如温度或密度）可以用两种方式描述。**物质描述**（material description）或 **拉格朗日描述**（Lagrangian description）将物理量视为物质点 $\mathbf{X}$ 和时间 $t$ 的函数，记为 $\widehat{f}(\mathbf{X}, t)$。而 **空间描述**（spatial description）或 **欧拉描述**（Eulerian description）则将其视为空间位置 $\mathbf{x}$ 和时间 $t$ 的函数，记为 $f(\mathbf{x}, t)$。这两者通过运动联系在一起：
$$
f(\mathbf{x}, t) = \widehat{f}(\boldsymbol{\chi}^{-1}(\mathbf{x}, t), t)
$$

另一个基本的运动学量是 **位移矢量场**（displacement vector field）$\mathbf{u}$，它定义为物质点从其参考位置到当前位置的矢量差：
$$
\mathbf{u}(\mathbf{X}, t) = \boldsymbol{\chi}(\mathbf{X}, t) - \mathbf{X}
$$
位移场在小变形理论中起着核心作用，但在有限变形理论中，我们很快就会看到，它本身不足以完整地描述局部变形。

### 变形梯度

为了量化物质点邻域内的局部变形，我们引入了连续介质运动学中最重要的概念之一：**变形梯度张量**（deformation gradient tensor）$\mathbf{F}$。它被定义为运动映射 $\boldsymbol{\chi}$ 对物质坐标 $\mathbf{X}$ 的梯度：
$$
\mathbf{F}(\mathbf{X}, t) = \nabla_{\mathbf{X}}\boldsymbol{\chi}(\mathbf{X}, t) \equiv \frac{\partial \boldsymbol{\chi}(\mathbf{X}, t)}{\partial \mathbf{X}}
$$
值得注意的是，变形梯度是关于 **物质坐标** 的梯度，因此它本质上是一个拉格朗日量，是 $(\mathbf{X}, t)$ 的函数 [@problem_id:3798599]。在分量形式中，$F_{iJ} = \partial x_i / \partial X_J$。

变形梯度的核心几何意义在于，它将参考构形中的一个无穷小物质线元 $d\mathbf{X}$ 线性映射到当前构形中对应的空间线元 $d\mathbf{x}$：
$$
d\mathbf{x} = \mathbf{F} \, d\mathbf{X}
$$
这一定义揭示了 $\mathbf{F}$ 如何编码了关于局部拉伸、收缩、剪切和旋转的所有信息。

变形梯度与位移梯度 $\nabla_{\mathbf{X}}\mathbf{u}$ 密切相关。通过对位移的定义式求梯度，我们得到：
$$
\mathbf{F} = \frac{\partial (\mathbf{X} + \mathbf{u})}{\partial \mathbf{X}} = \mathbf{I} + \nabla_{\mathbf{X}}\mathbf{u}
$$
其中 $\mathbf{I}$ 是二阶单位张量。这个关系表明，当变形很小时（即 $\nabla_{\mathbf{X}}\mathbf{u}$ 的分量远小于1），$\mathbf{F}$ 接近于单位张量。然而，它们的几何意义完全不同：$\mathbf{F}$ 将原始线元映射到变形后的线元，而 $\nabla_{\mathbf{X}}\mathbf{u}$ 将原始线元映射到变形增量线元 $d\mathbf{u} = d\mathbf{x} - d\mathbf{X}$ [@problem_id:3798623]。

#### 雅可比行列式与体积变化

变形梯度的行列式，被称为 **雅可比行列式**（Jacobian determinant）$J$，具有明确的物理意义。它描述了局部的体积变化：
$$
J(\mathbf{X}, t) = \det \mathbf{F}(\mathbf{X}, t)
$$
一个在参考构形中体积为 $dV$ 的无穷小元，在变形后其体积 $dv$ 变为：
$$
dv = J \, dV
$$
为了保持物质的物理真实性，必须有 $J > 0$，这意味着物质不能被压缩到零体积，其局部朝向也不能反转。如果运动是保体积的，这种运动被称为 **不可压缩**（incompressible）或 **等容**（isochoric）运动，其充分必要条件是 $J=1$ 处处成立 [@problem_id:3798599]。

考虑一个特定的变形映射：$x_1 = a(t)X_1$, $x_2 = b(t)X_2$, $x_3 = c(t)X_3 + k(t)X_1$。其变形梯度为：
$$
\mathbf{F} = \begin{pmatrix} a(t) & 0 & 0 \\ 0 & b(t) & 0 \\ k(t) & 0 & c(t) \end{pmatrix}
$$
其雅可比行列式为 $J = \det \mathbf{F} = a(t)b(t)c(t)$。值得注意的是，代表剪切的项 $k(t)$ 并不影响体积比。这说明纯剪切是保体积的 [@problem_id:3798631]。

质量守恒定律为雅可比行列式提供了另一个重要的物理联系。考虑一个质量为 $dm$ 的物质元，其在参考构形和当前构形中的密度分别为 $\rho_0(\mathbf{X})$ 和 $\rho(\mathbf{x}, t)$。由于质量不变，$dm = \rho_0 dV = \rho dv$。结合 $dv = J dV$，我们得到局部质量守恒的基本关系：
$$
\rho_0 = J \rho \quad \text{或} \quad \rho(\mathbf{x}, t) = \frac{\rho_0(\mathbf{X})}{J(\mathbf{X}, t)}
$$
这表明，体积的膨胀（$J > 1$）会导致密度下降，而体积的压缩（$J < 1$）则导致密度增加 [@problem_id:3798631]。

### 变形的分解：拉伸与旋转

变形梯度 $\mathbf{F}$ 作为一个线性映射，可以分解为一个纯拉伸/收缩部分和一个纯刚体旋转部分。这种分解是通过 **极分解定理**（polar decomposition theorem）实现的，它提供了两种等价的分解方式 [@problem_id:3772243]：

1.  **右极分解**: $\mathbf{F} = \mathbf{R}\mathbf{U}$
2.  **左极分解**: $\mathbf{F} = \mathbf{V}\mathbf{R}$

在这里：
- $\mathbf{R}$ 是一个 **旋转张量**（rotation tensor），它是一个正常交阵（$\mathbf{R}^\top\mathbf{R} = \mathbf{I}$ 且 $\det\mathbf{R}=+1$）。它描述了物质的局部刚体旋转。
- $\mathbf{U}$ 是 **右拉伸张量**（right stretch tensor），它是一个对称正定张量 ($\mathbf{U}^\top = \mathbf{U}$ 且其特征值全为正)。
- $\mathbf{V}$ 是 **左拉伸张量**（left stretch tensor），它也是一个对称正定张量 ($\mathbf{V}^\top = \mathbf{V}$)。

右极分解 $\mathbf{F}\mathbf{N} = \mathbf{R}(\mathbf{U}\mathbf{N})$ 的物理解释是：一个参考方向 $\mathbf{N}$ 上的物质线元首先被 $\mathbf{U}$ 拉伸和剪切（作用于参考构形），然后结果矢量被 $\mathbf{R}$ 刚性旋转到当前构形。而左极分解 $\mathbf{F}\mathbf{N} = \mathbf{V}(\mathbf{R}\mathbf{N})$ 的解释是：物质线元首先被 $\mathbf{R}$ 旋转，然后被 $\mathbf{V}$ 拉伸和剪切（作用于当前构形）。

拉伸张量 $\mathbf{U}$ 和 $\mathbf{V}$ 与两个重要的应变度量——**柯西-格林张量**（Cauchy-Green tensors）直接相关：
- **右柯西-格林张量**: $\mathbf{C} = \mathbf{F}^\top\mathbf{F} = \mathbf{U}^2$。它定义在参考构形上。
- **左柯西-格林张量** (或Finger张量): $\mathbf{B} = \mathbf{F}\mathbf{F}^\top = \mathbf{V}^2$。它定义在当前构形上。

$\mathbf{C}$ 和 $\mathbf{B}$ 提供了对局部变形引起的长度变化的直接度量。一个初始长度为 $|d\mathbf{X}|$ 的物质线元，变形后其长度的平方为：
$$
|d\mathbf{x}|^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F}d\mathbf{X}) \cdot (\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{F}^\top\mathbf{F} d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{C} d\mathbf{X})
$$
因此，沿单位矢量 $\mathbf{N}$ 方向的 **拉伸比**（stretch ratio）$\lambda$ 的平方为 $\lambda^2(\mathbf{N}) = \mathbf{N} \cdot \mathbf{C} \mathbf{N}$。$\mathbf{C}$ 和 $\mathbf{B}$ 的特征值都是主拉伸比的平方，即 $\lambda_i^2$ [@problem_id:3798618]。

### 客观性原理

在构建材料本构关系时，一个基本要求是物理定律不应依赖于观察者。这意味着，无论观察者是静止的，还是在进行刚体平移和旋转，他们观察到的材料响应规律应该是相同的。这一原则被称为 **物质标架无关性原理**（principle of material frame-indifference）或 **客观性原理**（principle of objectivity）。

考虑两个观察者，他们的空间坐标系通过一个时间相关的刚体运动相关联：
$$
\mathbf{x}'(t) = \mathbf{c}(t) + \mathbf{Q}(t)\mathbf{x}(t)
$$
其中 $\mathbf{c}(t)$ 是平移矢量，$\mathbf{Q}(t)$ 是一个旋转张量。在这种变换下，变形梯度变换为 $\mathbf{F}' = \mathbf{Q}\mathbf{F}$。由于 $\mathbf{Q}$ 通常不等于 $\mathbf{I}$，变形梯度 $\mathbf{F}$ 不是一个 **客观**（objective）的量。

然而，柯西-格林张量的变换行为则不同 [@problem_id:3798618]：
- 右柯西-格林张量 $\mathbf{C}$ 变换为 $\mathbf{C}' = (\mathbf{F}')^\top\mathbf{F}' = (\mathbf{Q}\mathbf{F})^\top(\mathbf{Q}\mathbf{F}) = \mathbf{F}^\top\mathbf{Q}^\top\mathbf{Q}\mathbf{F} = \mathbf{F}^\top\mathbf{F} = \mathbf{C}$。
- 左柯西-格林张量 $\mathbf{B}$ 变换为 $\mathbf{B}' = \mathbf{F}'(\mathbf{F}')^\top = (\mathbf{Q}\mathbf{F})(\mathbf{Q}\mathbf{F})^\top = \mathbf{Q}\mathbf{F}\mathbf{F}^\top\mathbf{Q}^\top = \mathbf{Q}\mathbf{B}\mathbf{Q}^\top$。

$\mathbf{C}$ 在观察者变换下保持不变，我们称之为一个客观的 **物质张量**。$\mathbf{B}$ 的变换方式符合一个客观的 **空间张量** 的定义。由于 $\mathbf{C}$ 和 $\mathbf{B}$ 捕捉了纯粹的变形（去除了刚体旋转），它们以及它们的标量不变量（如迹 $\operatorname{tr}(\mathbf{C})$ 和行列式 $\det(\mathbf{C})$）是构建本构模型的理想选择。

客观性原理对本构理论有深远的影响。例如，对于一个只依赖于变形梯度的弹性材料，其自由能函数 $\psi(\mathbf{F})$ 必须满足 $\psi(\mathbf{F}) = \psi(\mathbf{Q}\mathbf{F})$。利用极分解 $\mathbf{F}=\mathbf{R}\mathbf{U}$，并选择 $\mathbf{Q}=\mathbf{R}^\top$，我们可以证明 $\psi(\mathbf{F}) = \psi(\mathbf{U})$。这意味着能量只能是拉伸的函数，而不能是旋转的函数。因为 $\mathbf{U}$ 可由 $\mathbf{C}$ 唯一确定，所以能量最终可以表示为 $\mathbf{C}$ 的函数：$\psi(\mathbf{F}) = \widehat{\psi}(\mathbf{C})$ [@problem_id:3798615]。

### 运动与变形率

为了描述变形如何随时间演化，我们需要引入速率量。物质点 $\mathbf{X}$ 的 **速度**（velocity）是其位置的物质时间导数：$\mathbf{V}(\mathbf{X}, t) = \partial \boldsymbol{\chi}(\mathbf{X}, t) / \partial t$。其空间描述为 $\mathbf{v}(\mathbf{x}, t)$ [@problem_id:3798599]。

**空间速度梯度**（spatial velocity gradient）$\mathbf{L}$ 定义为空间速度场 $\mathbf{v}$ 对空间坐标 $\mathbf{x}$ 的梯度：
$$
\mathbf{L} = \nabla_{\mathbf{x}}\mathbf{v}
$$
它描述了在一点附近，速度是如何随空间位置变化的。$\mathbf{L}$ 与变形梯度的物质时间导数 $\dot{\mathbf{F}}$ 之间存在一个基本关系。通过链式法则可以证明：
$$
\dot{\mathbf{F}} = \mathbf{L}\mathbf{F} \quad \implies \quad \mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}
$$
这个关系是连接拉格朗日描述和欧拉描述速率的关键桥梁 [@problem_id:3798622]。同样，雅可比行列式的变化率也与 $\mathbf{L}$ 相关，即 **欧拉展开公式**（Euler's expansion formula）：
$$
\dot{J} = J \operatorname{tr}(\mathbf{L})
$$
其中 $\operatorname{tr}(\mathbf{L})$ 是 $\mathbf{L}$ 的迹，表示速度场的散度 $\nabla_{\mathbf{x}}\cdot\mathbf{v}$ [@problem_id:3798631]。

空间速度梯度 $\mathbf{L}$ 可以分解为一个对称部分和一个反对称部分：
$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$
其中：
- $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^\top)$ 是 **变形率张量**（rate of deformation tensor），它是对称的。
- $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^\top)$ 是 **自旋张量**（spin tensor），它是反对称的。

这个分解具有深刻的物理意义。$\mathbf{D}$ 描述了物质线元的拉伸或收缩速率。一个空间线元 $\mathbf{l}$ 的长度平方的变化率仅由 $\mathbf{D}$ 决定：
$$
\frac{d}{dt}(\mathbf{l}\cdot\mathbf{l}) = 2 \mathbf{l} \cdot (\mathbf{D}\mathbf{l})
$$
而 $\mathbf{W}$ 则描述了物质的局部刚体旋转速率（或称自旋），它不引起长度变化。与 $\mathbf{W}$ 相关的轴矢量是涡量矢量 $\boldsymbol{\omega}_v = \frac{1}{2} \nabla_{\mathbf{x}} \times \mathbf{v}$ [@problem_id:3798622]。

### 率形式本构关系中的客观性

对于许多材料（如金属塑性或流体），其本构关系是基于变形率而不是总变形来建立的。例如，一个简单的关系可能是应力率与变形率成正比。这就引出了一个问题：我们应该使用哪种应力率？

柯西应力 $\boldsymbol{\sigma}$ 是一个客观的空间张量，但它的标准物质时间导数 $\dot{\boldsymbol{\sigma}}$ 却不是客观的。为了构建客观的率形式本构律，我们需要定义一个 **客观应力率**（objective stress rate），它在刚体运动叠加下的变换行为应与应力张量本身相同。

有多种方法可以构造这样的客观率，其中最著名的是 **Jaumann率**（Jaumann rate），记为 $\overset{\triangle}{\boldsymbol{\sigma}}$。它通过在物质导数上加上与自旋张量 $\mathbf{W}$ 相关的项来修正非客观性：
$$
\overset{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\mathbf{W} - \mathbf{W}\boldsymbol{\sigma}
$$
可以证明，在叠加刚体运动下，$\mathbf{W}$ 的非客观变换项（$\mathbf{W}' = \mathbf{Q}\mathbf{W}\mathbf{Q}^\top + \dot{\mathbf{Q}}\mathbf{Q}^\top$）恰好抵消了 $\dot{\boldsymbol{\sigma}}$ 中的非客观项，从而使得 Jaumann 率是客观的，即 $\overset{\triangle}{\boldsymbol{\sigma}}' = \mathbf{Q}\overset{\triangle}{\boldsymbol{\sigma}}\mathbf{Q}^\top$ [@problem_id:3798617]。

然而，Jaumann 率并非唯一的客观率，也不是完美的。例如，在模拟大剪切变形时，使用 Jaumann 率的简单弹塑性模型可能会预测出非物理的应力振荡现象 [@problem_id:3798617]。这促使了其他客观率（如 Green-Naghdi 率或 Truesdell 率）的发展，以期更准确地描述材料在复杂加载下的行为。

### 高等运动学概念

#### 协变与逆变变换

变形梯度 $\mathbf{F}$ 不仅是描述变形的工具，也是连接两个构形中张量场的桥梁。不同类型的物理量在构形间的映射方式不同。

- **逆变矢量**（Contravariant vectors），如切矢量 $d\mathbf{X}$，通过 **前推**（push-forward）运算从参考构形映射到当前构形：$d\mathbf{x} = \mathbf{F}d\mathbf{X}$。
- **协变矢量**（Covariant vectors），如标量场的梯度 $\nabla_{\mathbf{X}}\phi$，其前推运算遵循不同的法则：$(\nabla_{\mathbf{x}}\phi) = \mathbf{F}^{-\top}(\nabla_{\mathbf{X}}\phi)$。

这些变换规则源于保持标量积不变的要求，例如，向量与其对偶（协变向量）之间的内积在映射前后应保持不变 [@problem_id:3798614]。理解这些变换对于在不同构形之间正确转换张量方程至关重要。

#### 相容性与材料缺陷

到目前为止，我们都假设存在一个光滑的单值运动场 $\boldsymbol{\chi}(\mathbf{X})$，并从中推导出变形梯度 $\mathbf{F}$。现在我们反过来问：给定一个二阶张量场 $\mathbf{F}(\mathbf{X})$，它是否能对应于某个真实的、连续的物体运动？这个问题被称为 **相容性**（compatibility）问题。

根据矢量分析的基本定理，一个矢量场是某个标量场的梯度的充要条件是其旋度为零。将此思想应用于变形梯度的每一行，我们发现在一个 **单连通**（simply connected）的物体中，一个变形梯度场 $\mathbf{F}$ 是相容的（即存在一个单值的位移场 $\mathbf{u}$），当且仅当其 **物质旋度**（material curl）为零 [@problem_id:3798636]：
$$
\mathrm{Curl}\,\mathbf{F} = \mathbf{0}
$$
其中 $(\mathrm{Curl}\,\mathbf{F})_{iK} = \varepsilon_{KLM} \frac{\partial F_{iM}}{\partial X_L}$，$\varepsilon_{KLM}$ 是列维-奇维塔符号。

当 $\mathrm{Curl}\,\mathbf{F} \neq \mathbf{0}$ 时，变形场是不相容的，这意味着不可能在整个物体内定义一个连续的、单值的位移场。这种不相容性在物理上对应于材料内部存在连续分布的 **位错**（dislocations）。**位错密度张量** $\boldsymbol{\alpha}$ 被定义为与变形梯度的旋度直接相关：
$$
\boldsymbol{\alpha} = \mathrm{Curl}\,\mathbf{F}
$$
这个深刻的联系将纯粹的几何运动学与材料科学中的晶体缺陷理论联系起来，为多尺度材料模拟中从离散位错到连续塑性模型的过渡提供了理论基础 [@problem_id:3798636]。