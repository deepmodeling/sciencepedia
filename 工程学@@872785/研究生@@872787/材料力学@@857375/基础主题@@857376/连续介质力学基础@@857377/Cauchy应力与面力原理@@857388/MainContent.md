## 引言
在[材料科学](@entry_id:152226)与工程领域，准确描述和预测物体在外力作用下的内部力学响应是实现安全设计与性能分析的核心。然而，一个连续体内部的力状态是复杂且难以直接测量的。如何建立一个普适的数学框架，来描述任意一点的内部力状态，并将其与作用于任意假想[截面](@entry_id:154995)上的力精确联系起来？这正是连续介质力学所要解决的基本问题。本文旨在系统阐述解决这一问题的基石——柯西应力和牵[引力](@entry_id:175476)原理。通过本文的学习，您将掌握从第一性原理到实际应用的完整知识体系。在“原理与机制”一章中，我们将从[牛顿定律](@entry_id:163541)出发，严谨推导柯西应力张量的概念及其基本性质。接下来的“应用与跨学科联系”一章将展示这些理论如何在结构工程、接触力学和微观[材料科学](@entry_id:152226)等领域中发挥关键作用。最后，“动手实践”部分将通过具体的计算问题，帮助您将理论知识转化为解决实际问题的能力。现在，让我们首先深入探讨这些核心概念的物理原理与数学机制。

## 原理与机制

在连续介质力学中，理解物体内部力的[分布](@entry_id:182848)和传递是核心任务。本章旨在深入探讨描述这一内部力状态的基本工具——柯西[应力张量](@entry_id:148973)，以及它与作用在任意[截面](@entry_id:154995)上的力（即牵[引力](@entry_id:175476)）之间的根本关系。我们将从第一性原理出发，通过严谨的推导，建立这些核心概念，并阐明其物理意义和基本性质。

### 柯西应力定理：从牵[引力](@entry_id:175476)到应力张量

想象一个连续体内部的任意一点 $P$。如果我们通过这一点做一个假想的切割，就会形成一个具有特定方向的[截面](@entry_id:154995)。该[截面](@entry_id:154995)的一侧物质会对另一侧物质施加一个[分布](@entry_id:182848)力。在点 $P$ 附近，这个力的作用效果可以被局部化。我们定义**牵[引力](@entry_id:175476)矢量 (traction vector)** $\mathbf{t}$ 为单位面积上所受的[接触力](@entry_id:165079)。这个矢量不仅依赖于考察点的位置 $\mathbf{x}$，还显式地依赖于[截面](@entry_id:154995)的方向，该方向由[截面](@entry_id:154995)的[单位法向量](@entry_id:178851) $\mathbf{n}$ 唯一确定。因此，我们将其记为 $\mathbf{t}(\mathbf{x}, \mathbf{n})$。

一个自然而然的问题是：在给定点 $\mathbf{x}$，牵[引力](@entry_id:175476)矢量 $\mathbf{t}$ 是如何随法向量 $\mathbf{n}$ 变化的？这是一个复杂的[非线性](@entry_id:637147)函数，还是存在一个更简单的内在结构？答案蕴含在奥古斯丁-路易·柯西 (Augustin-Louis Cauchy) 提出的一个精妙论证中，该论证最终导出了连续介质力学的一块基石——柯西应力定理。

#### 柯西四面体论证

为了揭示 $\mathbf{t}$ 与 $\mathbf{n}$ 之间的关系，我们考虑一个以点 $P$ 为顶点、体积无穷小的四面体。为方便起见，我们将点 $P$ 置于坐标原点。该四面体有四个面：三个面分别与坐标平面重合，其向外的[单位法向量](@entry_id:178851)为 $-\mathbf{e}_1, -\mathbf{e}_2, -\mathbf{e}_3$；第四个面是一个斜面，其面积为 $\Delta A$，向外的[单位法向量](@entry_id:178851)为 $\mathbf{n}$。通过简单的几何投影关系可知，第 $i$ 个坐标面上的面积为 $\Delta A_i = (\mathbf{n} \cdot \mathbf{e}_i) \Delta A = n_i \Delta A$。

现在，我们将牛顿第二定律（[线性动量守恒](@entry_id:165717)）应用于这个无穷小四面体。该定律的积分形式表明，作用于物体的所有力之和等于其动量的变化率。这些力包括作用于表面的**面力**（通过牵[引力](@entry_id:175476)体现）和作用于体积的**[体力](@entry_id:174230)**（如重力、[电磁力](@entry_id:196024)等）以及惯性力。对于我们的四面体，[动量平衡](@entry_id:193575)方程可以写为：
$$
\mathbf{t}(\mathbf{n}) \Delta A + \mathbf{t}(-\mathbf{e}_1) \Delta A_1 + \mathbf{t}(-\mathbf{e}_2) \Delta A_2 + \mathbf{t}(-\mathbf{e}_3) \Delta A_3 + \rho \mathbf{b} \Delta V = \rho \mathbf{a} \Delta V
$$
这里，$\rho$ 是密度，$\mathbf{b}$ 是单位质量的[体力](@entry_id:174230)，$\mathbf{a}$ 是加速度，$\Delta V$ 是四面体的体积。

根据牛顿第三定律的推论（柯西引理），在同一点作用于同一个面的两侧的牵[引力](@entry_id:175476)大小相等、方向相反，即 $\mathbf{t}(-\mathbf{n}) = -\mathbf{t}(\mathbf{n})$。将此应用于坐标面，我们得到 $\mathbf{t}(-\mathbf{e}_i) = -\mathbf{t}(\mathbf{e}_i)$。代入[动量平衡](@entry_id:193575)方程并整理，可得：
$$
\mathbf{t}(\mathbf{n}) \Delta A - \sum_{i=1}^{3} n_i \mathbf{t}(\mathbf{e}_i) \Delta A + (\rho \mathbf{b} - \rho \mathbf{a}) \Delta V = \mathbf{0}
$$

此处的关键在于**力的尺度分析 (scaling argument)**。若设四面体的[特征长度](@entry_id:265857)为 $\ell$（例如，从顶点 $P$ 到斜面的高），那么其表面积 $\Delta A$ 的量级为 $\mathcal{O}(\ell^2)$，而其体积 $\Delta V$ 的量级为 $\mathcal{O}(\ell^3)$。因此，面力（牵[引力](@entry_id:175476)乘以面积）的量级为 $\mathcal{O}(\ell^2)$，而[体力](@entry_id:174230)与惯性力（密度乘以加速度再乘以体积）的量级为 $\mathcal{O}(\ell^3)$。

为了考察点 $P$ 处的局部关系，我们将整个方程除以 $\Delta A$，然后取四面体无限缩小至点 $P$ 的极限，即 $\ell \to 0$：
$$
\mathbf{t}(\mathbf{n}) - \sum_{i=1}^{3} n_i \mathbf{t}(\mathbf{e}_i) + (\rho \mathbf{b} - \rho \mathbf{a}) \frac{\Delta V}{\Delta A} = \mathbf{0}
$$
由于 $\frac{\Delta V}{\Delta A}$ 的量级为 $\mathcal{O}(\ell)$，在 $\ell \to 0$ 的极限下，包含体力与惯性力的项将趋于零。这一步并不要求体力或惯性力本身为零，只要它们是有界的即可。极限的结果是一个只涉及面力的纯粹的代数关系：
$$
\mathbf{t}(\mathbf{n}) = \sum_{i=1}^{3} n_i \mathbf{t}(\mathbf{e}_i) = n_1 \mathbf{t}(\mathbf{e}_1) + n_2 \mathbf{t}(\mathbf{e}_2) + n_3 \mathbf{t}(\mathbf{e}_3)
$$

这个优美的公式就是**柯西应力定理**。它揭示了一个深刻的结论：在任意一点，作用于任意方向平面上的牵[引力](@entry_id:175476)矢量 $\mathbf{t}(\mathbf{n})$，是作用于三个相互垂直的坐标平面上的牵[引力](@entry_id:175476)矢量 $\mathbf{t}(\mathbf{e}_i)$ 的线性组合，其系数恰好是该方向的[法向量](@entry_id:264185)分量 $n_i$。这意味着，从[法向量](@entry_id:264185) $\mathbf{n}$ 到牵[引力](@entry_id:175476)向量 $\mathbf{t}(\mathbf{n})$ 的映射是一个**[线性映射](@entry_id:185132)**。

#### 柯西应力张量

既然 $\mathbf{n} \mapsto \mathbf{t}(\mathbf{n})$ 是一个线性映射，根据线性代数理论，这个映射可以由一个二阶张量来表示。这个张量就是**柯西应力张量 (Cauchy stress tensor)**，记为 $\boldsymbol{\sigma}$。柯西应力定理的表达式可以优雅地写成张量与矢量的乘积形式：
$$
\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}
$$
或者使用分量（爱因斯坦求和约定）表示为：
$$
t_i = \sigma_{ij} n_j
$$
这里的 $\sigma_{ij}$ 就是应力张量 $\boldsymbol{\sigma}$ 在选定[坐标系](@entry_id:156346)下的分量。$\sigma_{ij}$ 的物理意义是：作用在法向量为 $\mathbf{e}_j$ 的平面上（即 $j$ 平面）的牵[引力](@entry_id:175476)矢量在 $\mathbf{e}_i$ 方向（即 $i$ 方向）上的分量。换言之，应力张量矩阵的第 $j$ 列，就是作用在第 $j$ 个坐标平面上的牵[引力](@entry_id:175476)矢量 $\mathbf{t}(\mathbf{e}_j)$。

因此，我们得到了一个强大的结论：在连续体中的任意一点，无论[截面](@entry_id:154995)方向如何，其复杂的内部力状态都可以被一个包含九个分量（在三维空间中）的[二阶张量](@entry_id:199780) $\boldsymbol{\sigma}$ 完全描述。只要我们知道了 $\boldsymbol{\sigma}$，就可以通过简单的线性运算求出任何方向上的牵[引力](@entry_id:175476)。

### 应力张量的基本性质

柯西应力张量不仅仅是一个数学构造，它还具有深刻的物理性质，这些性质源于物理学的基本原理。

#### [坐标变换](@entry_id:172727)与张量本质

我们称 $\boldsymbol{\sigma}$ 为一个“张量”，这不仅仅是因为它有多个分量，更是因为它在[坐标系](@entry_id:156346)变换下遵循特定的变换法则。这一性质源于**物质[坐标系](@entry_id:156346)无关性原理 (principle of material frame-indifference)**，或称[客观性原理](@entry_id:185412)。该原理要求物理定律在所有[刚性运动](@entry_id:170523)的观察者看来形式相同。

考虑一个由正交张量 $\mathbf{Q}$（满足 $\mathbf{Q}^T\mathbf{Q}=\mathbf{I}$ 且 $\det\mathbf{Q}=+1$）描述的刚性旋转。在新[坐标系](@entry_id:156346)（带撇号的量）中，矢量（如力或位置）的客观变换法则是 $\mathbf{v}'=\mathbf{Q}\mathbf{v}$。因此，法向量和牵[引力](@entry_id:175476)向量分别变换为 $\mathbf{n}' = \mathbf{Q}\mathbf{n}$ 和 $\mathbf{t}' = \mathbf{Q}\mathbf{t}$。物理定律 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$ 在新旧[坐标系](@entry_id:156346)下都必须成立：
$$
\mathbf{t}' = \boldsymbol{\sigma}' \mathbf{n}'
$$
将变换关系代入，我们得到：
$$
\mathbf{Q}\mathbf{t} = \boldsymbol{\sigma}' (\mathbf{Q}\mathbf{n}) \implies \mathbf{Q}(\boldsymbol{\sigma}\mathbf{n}) = \boldsymbol{\sigma}' \mathbf{Q}\mathbf{n}
$$
由于这个等式必须对任意方向的 $\mathbf{n}$ 都成立，因此我们必然有 $\mathbf{Q}\boldsymbol{\sigma} = \boldsymbol{\sigma}'\mathbf{Q}$。用 $\mathbf{Q}^T$ 右乘该式，我们便得到了[二阶张量](@entry_id:199780)的变换法则：
$$
\boldsymbol{\sigma}' = \mathbf{Q} \boldsymbol{\sigma} \mathbf{Q}^T
$$
正是这种特定的变换行为，赋予了 $\boldsymbol{\sigma}$ 作为二阶张量的真正含义。

#### 对称性：[角动量守恒](@entry_id:156798)的推论

应力张量的一个至关重要的性质是其**对称性**，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$ 或 $\sigma_{ij} = \sigma_{ji}$。这个性质并非凭空而来，而是**[角动量守恒](@entry_id:156798)定律**的直接推论。

考虑一个无穷小的立方体微元。对其施加[角动量守恒](@entry_id:156798)定律，即作用在微元上的所有力矩之和等于其角动量的变化率。与线性动量分析类似，我们可以进行[尺度分析](@entry_id:153681)。作用在微元表面上的力矩（由[剪切应力](@entry_id:137139)产生）量级为 (应力 $\times$ 面积) $\times$ [力臂](@entry_id:162693) $\sim \ell^2 \times \ell = \mathcal{O}(\ell^3)$。而[体力](@entry_id:174230)矩和转动惯性力矩的量级则为 $\mathcal{O}(\ell^4)$。

在微元尺寸 $\ell \to 0$ 的极限下，$\mathcal{O}(\ell^4)$ 的项相对于 $\mathcal{O}(\ell^3)$ 的项可以忽略不计。因此，在没有**体力偶 (body couples)** 和**面力偶 (surface couples)** 的经典（非极性）连续[体力](@entry_id:174230)学框架下，极限情况下的[角动量平衡](@entry_id:181848)要求由[表面应力](@entry_id:191241)产生的[净力矩](@entry_id:166772)为零。通过简单的计算可以证明，这等价于要求[应力张量](@entry_id:148973)是对称的，即 $\sigma_{xy}=\sigma_{yx}$, $\sigma_{yz}=\sigma_{zy}$, $\sigma_{zx}=\sigma_{xz}$。

#### 前本构概念：应力理论的普适性

在此必须强调一个至关重要的概念点：柯西[应力张量](@entry_id:148973)的存在性（来自[线性动量守恒](@entry_id:165717)）及其对称性（来自角动量守恒）是**前本构 (pre-constitutive)** 的。这意味着它们的推导完全基于普适的物理[守恒定律](@entry_id:269268)和几何考虑，而与材料的具体性质无关。

无论材料是各向同性的（如钢），还是各向异性的（如木材或[复合材料](@entry_id:139856)），是弹性的，还是塑性的，只要它能被看作一个经典连续介质，那么在每一点都存在一个对称的柯西应力张量来描述其局部力状态。材料的各向异性等性质，是在后续的**本构关系**（连接应力与应变或应变率的方程）中才发挥作用，而不是在应力的定义阶段。

### 应用与分析

建立了应力张量的概念后，我们可以用它来分析和解决实际问题。

#### 平衡方程：从积分到[微分](@entry_id:158718)

柯西应力定理提供了连接宏观边界力与内部应[力场](@entry_id:147325)的桥梁。对于一个处于静态平衡的物体，其任何部分的[净力](@entry_id:163825)都必须为零。考虑物体内任意一个体积为 $V$、边界为 $\partial V$ 的子区域，其[静力平衡](@entry_id:163498)的积分形式为：
$$
\int_{\partial V} \mathbf{t} \,dA + \int_{V} \rho\mathbf{b} \,dV = \mathbf{0}
$$
其中 $\mathbf{b}$ 是单位质量的[体力](@entry_id:174230)。利用柯西关系 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$ 和高斯**[散度定理](@entry_id:143110)**，可以将面积分转化为[体积分](@entry_id:171119)：
$$
\int_{\partial V} \boldsymbol{\sigma}\mathbf{n} \,dA = \int_{V} (\nabla \cdot \boldsymbol{\sigma}) \,dV
$$
其中 $\nabla \cdot \boldsymbol{\sigma}$ 是[张量的散度](@entry_id:191736)。于是，平衡方程变为：
$$
\int_{V} (\nabla \cdot \boldsymbol{\sigma} + \rho\mathbf{b}) \,dV = \mathbf{0}
$$
由于这个方程对任意子区域 $V$ 都成立，所以被积函数本身必须处处为零。这就得到了描述连续体内部静态平衡的**局部（[微分](@entry_id:158718)）[平衡方程](@entry_id:172166)**：
$$
\nabla \cdot \boldsymbol{\sigma} + \rho\mathbf{b} = \mathbf{0}
$$
在[笛卡尔坐标系](@entry_id:169789)中，其分量形式为：
$$
\begin{cases}
\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{yx}}{\partial y} + \frac{\partial \sigma_{zx}}{\partial z} + \rho b_x = 0 \\
\frac{\partial \sigma_{xy}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} + \frac{\partial \sigma_{zy}}{\partial z} + \rho b_y = 0 \\
\frac{\partial \sigma_{xz}}{\partial x} + \frac{\partial \sigma_{yz}}{\partial y} + \frac{\partial \sigma_{zz}}{\partial z} + \rho b_z = 0
\end{cases}
$$
这组[偏微分方程](@entry_id:141332)构成了弹性力学和塑性力学求解的骨架。例如，如果我们有一个候选的应[力场](@entry_id:147325)，我们可以通过检验它是否满足平衡方程来判断它对于给定的体力是否是静态容许的。

#### [主应力与主方向](@entry_id:193792)：应力状态的[对角化](@entry_id:147016)

[应力张量](@entry_id:148973)以一种简洁的方式包含了某一点的全部应力信息，但其九个分量（由于对称性，实为六个独立分量）的物理图像不够直观。为了更好地理解应力状态，我们寻找一种特殊的[坐标系](@entry_id:156346)，使得在该[坐标系](@entry_id:156346)下[应力张量](@entry_id:148973)的描述最为简单。

我们提出一个问题：在一点处，是否存在某些特定的[截面](@entry_id:154995)，其上的牵[引力](@entry_id:175476)矢量 $\mathbf{t}$ 恰好与[截面](@entry_id:154995)的[法向量](@entry_id:264185) $\mathbf{n}$ 平行？如果存在，那么在这些[截面](@entry_id:154995)上，牵[引力](@entry_id:175476)是纯法向的，**剪切应力 (shear stress)** 为零。这个条件可以写为：
$$
\mathbf{t}(\mathbf{n}) = \lambda \mathbf{n}
$$
其中 $\lambda$ 是一个标量。将柯西关系 $\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma}\mathbf{n}$ 代入，我们得到：
$$
\boldsymbol{\sigma}\mathbf{n} = \lambda \mathbf{n}
$$
这正是线性代数中标准的**[特征值问题](@entry_id:142153)**。因此，那些剪切应力为零的特殊方向，就是[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的**[特征向量](@entry_id:151813) (eigenvectors)**。这些方向被称为**[主方向](@entry_id:276187) (principal directions)**。对应的[特征值](@entry_id:154894) $\lambda$ 称为**主应力 (principal stresses)**。

由于应力张量 $\boldsymbol{\sigma}$ 是对称的实数张量，根据[谱定理](@entry_id:136620)，它总是有三个实数[特征值](@entry_id:154894)（主应力），以及一组三个相互正交的[特征向量](@entry_id:151813)（[主方向](@entry_id:276187)）。这意味着在任何一点，我们总能找到一个[正交坐标](@entry_id:166074)系（主[坐标系](@entry_id:156346)），在该[坐标系](@entry_id:156346)下应力张量矩阵是一个对角矩阵，其对角元就是三个主应力：
$$
\boldsymbol{\sigma}_{\text{principal}} = \begin{pmatrix} \lambda_1 & 0 & 0 \\ 0 & \lambda_2 & 0 \\ 0 & 0 & \lambda_3 \end{pmatrix}
$$
[主应力](@entry_id:176761)不仅是[剪切应力](@entry_id:137139)为零平面上的法向应力，它们也代表了该点法向应力的极值（最大、最小或[鞍点](@entry_id:142576)值）。如果某个主应力存在重根（例如 $\lambda_1 = \lambda_2 \neq \lambda_3$），则对应于该[主应力](@entry_id:176761)的主方向不是唯一的，而是在一个平面（称为[主平面](@entry_id:164488)）内的任意方向。

#### 应力状态的分解与计算

在实际分析中，我们常常需要计算给定[截面](@entry_id:154995)上的牵[引力](@entry_id:175476)，并将其分解为[法向和切向分量](@entry_id:166204)。

给定某点的应力张量 $\boldsymbol{\sigma}$ 和一个[单位法向量](@entry_id:178851) $\mathbf{n}$，计算步骤如下：
1.  **计算牵[引力](@entry_id:175476)矢量**: $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$。
2.  **计算[法向应力](@entry_id:260622)**: [法向应力](@entry_id:260622) $\sigma_n$ 是 $\mathbf{t}$ 在 $\mathbf{n}$ 方向上的投影大小：
    $$
    \sigma_n = \mathbf{t} \cdot \mathbf{n} = (\boldsymbol{\sigma}\mathbf{n}) \cdot \mathbf{n} = \mathbf{n}^T \boldsymbol{\sigma} \mathbf{n}
    $$
3.  **分解牵[引力](@entry_id:175476)矢量**: 牵[引力](@entry_id:175476)矢量可以分解为法向分量 $\mathbf{t}_n$ 和切向（剪切）分量 $\mathbf{t}_s$：
    $$
    \mathbf{t} = \mathbf{t}_n + \mathbf{t}_s
    $$
    其中，法向分量为 $\mathbf{t}_n = \sigma_n \mathbf{n}$，切向分量为 $\mathbf{t}_s = \mathbf{t} - \mathbf{t}_n$。
4.  **计算剪切应力大小**: 剪切应力的大小 $|\mathbf{t}_s|$ 可以通过[勾股定理](@entry_id:264352)计算：
    $$
    |\mathbf{t}_s|^2 = |\mathbf{t}|^2 - |\mathbf{t}_n|^2 = |\mathbf{t}|^2 - \sigma_n^2
    $$
通过一个具体的数值算例可以更好地掌握这个过程。例如，给定[应力张量](@entry_id:148973)
$$
\boldsymbol{\sigma} = 
\begin{pmatrix}
120 & 35 & -20 \\
35 & 80 & 15 \\
-20 & 15 & 60
\end{pmatrix}
\ \text{MPa}
$$
和[法向量](@entry_id:264185) $\mathbf{n}=\frac{1}{\sqrt{14}}(1, 2, 3)^T$，我们可以一步步计算出作用在该平面上的总牵[引力](@entry_id:175476)、法向应力和[剪切应力](@entry_id:137139)的大小。

### 扩展与展望：[广义连续介质理论](@entry_id:193621)

我们之[前推](@entry_id:158718)导出应力[张量的对称性](@entry_id:202126)是基于一个关键假设：连续体是“经典的”或“非极性的”，即不存在体力偶和面力偶。然而，对于一些具有显着内部微观结构的材料，如[颗粒材料](@entry_id:750005)、泡沫、液晶或具有大分子链的聚合物，物[质点](@entry_id:186768)本身不仅能[平动](@entry_id:187700)，还能独立转动，并能传递力偶。

描述这类材料的理论被称为**[广义连续介质理论](@entry_id:193621) (generalized continuum theories)**，其中最著名的是**科瑟拉 (Cosserat) 理论**或称**微极性理论 (micropolar theory)**。在该理论中，除了经典的[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$，还引入了**[力偶应力](@entry_id:747952)张量 (couple-stress tensor)** $\boldsymbol{\mu}$，它描述了单位面积上传递的力偶。

此时，局部[角动量平衡](@entry_id:181848)方程需要被修正，以包含体力偶 $\mathbf{c}$ 和[力偶应力](@entry_id:747952)的贡献。修正后的方程形式为：
$$
\epsilon_{ijk}\sigma_{kj} + c_i + \mu_{ij,j} = 0
$$
其中 $\epsilon_{ijk}$ 是[列维-奇维塔符号](@entry_id:193594)。这个方程表明，与[应力张量](@entry_id:148973)反对称部分相关的轴矢量 $\epsilon_{ijk}\sigma_{kj}$，现在由[体力](@entry_id:174230)偶和力偶[应力的散度](@entry_id:185633)来平衡。因此，在科瑟拉理论中，**柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 不再必须是对称的**。

这一扩展不仅展示了物理理论的演进，也反过来凸显了经典柯西理论中“对称性”这一性质所依赖的物理假设。理解这些假设的边界，对于正确应用和未来发展[连续介质力学](@entry_id:155125)至关重要。