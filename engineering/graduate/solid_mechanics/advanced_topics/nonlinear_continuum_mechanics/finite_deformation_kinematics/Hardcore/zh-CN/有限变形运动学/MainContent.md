## 引言
在工程与科学领域，从橡胶密封圈的拉伸到金属板材的冲压，再到生物组织的生长，许多现象都涉及材料的大幅度变形和转动。经典的线性小应变理论在这些情况下会失效，因为它无法准确捕捉[几何非线性](@entry_id:169896)的复杂效应。因此，建立一个能够精确描述任意大小变形和旋转的理论框架——有限变形运动学——成为现代[固体力学](@entry_id:164042)的基石。该理论不仅是正确构建[非线性](@entry_id:637147)材料[本构关系](@entry_id:186508)（如[超弹性](@entry_id:159356)和[弹塑性](@entry_id:193198)）的先决条件，也是进行精确有限元分析的根本依据。

本文旨在系统性地阐述有限变形[运动学](@entry_id:173318)的核心概念与应用。我们将分三个章节展开：
- **原理与机制**：这一章将奠定理论基础，从最基本的运动映射出发，引入并深入剖析变形梯度、极分解、客观应变张量以及变形率等关键[运动学](@entry_id:173318)量。
- **应用与[交叉](@entry_id:147634)学科联系**：这一章将展示这些理论如何在超弹性、[弹塑性](@entry_id:193198)、生物力学和计算力学等前沿领域中，为构建复杂的[本构模型](@entry_id:174726)和解决实际工程问题提供支撑。
- **动手实践**：最后，这一章将通过具体的计算练习，帮助读者巩固理论知识，并将其转化为解决问题的实用技能。

通过这三个部分的学习，读者将能够全面掌握描述材料宏观变形行为的数学语言，为进一步深入研究[非线性](@entry_id:637147)连续介质力学、计算力学和[材料科学](@entry_id:152226)打下坚实的基础。

## 原理与机制

### 运动和变形梯度

在[连续介质力学](@entry_id:155125)中，我们通过一个光滑的、随时间变化的映射 $\boldsymbol{\chi}$ 来描述物体的运动。这个映射将物体在某个选定的**参考构型** $\mathcal{B}_0$ 中的每个物质点 $\mathbf{X}$ 与其在 $t$ 时刻在**当前构型** $\mathcal{B}_t$ 中的空间位置 $\mathbf{x}$ 建立[一一对应](@entry_id:143935)关系，即 $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$。参考构型是固定的，而当前构型则随[时间演化](@entry_id:153943)。

为了量化物质点邻域内的局部变形，我们引入一个核心的运动学量：**变形梯度 (deformation gradient)** $\mathbf{F}$。它被定义为运动映射 $\boldsymbol{\chi}$ 相对于参考坐标 $\mathbf{X}$ 的梯度：

$$
\mathbf{F}(\mathbf{X}, t) = \frac{\partial \boldsymbol{\chi}(\mathbf{X}, t)}{\partial \mathbf{X}} \equiv \nabla_{\mathbf{X}} \boldsymbol{\chi}(\mathbf{X}, t)
$$

在分量形式下，若参考坐标为 $\{X_I\}$，当前坐标为 $\{x_i\}$，则变形梯度的分量为 $F_{iI} = \frac{\partial x_i}{\partial X_I}$。

变形梯度 $\mathbf{F}$ 的基本物理意义在于它是一个[局部线性](@entry_id:266981)映射，它将参考构型中一个无穷小的物质线元 $\mathrm{d}\mathbf{X}$ 映射到当前构型中对应的空间[线元](@entry_id:196833) $\mathrm{d}\mathbf{x}$。具体而言，考虑两个相邻的物[质点](@entry_id:186768) $\mathbf{X}$ 和 $\mathbf{X} + \mathrm{d}\mathbf{X}$，它们在当前构型中的位置分别为 $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$ 和 $\mathbf{x} + \mathrm{d}\mathbf{x} = \boldsymbol{\chi}(\mathbf{X} + \mathrm{d}\mathbf{X}, t)$。通过对 $\boldsymbol{\chi}$ 进行泰勒展开，我们得到：

$$
\boldsymbol{\chi}(\mathbf{X} + \mathrm{d}\mathbf{X}, t) = \boldsymbol{\chi}(\mathbf{X}, t) + \frac{\partial \boldsymbol{\chi}}{\partial \mathbf{X}} \mathrm{d}\mathbf{X} + o(\|\mathrm{d}\mathbf{X}\|)
$$

由此可得 $\mathrm{d}\mathbf{x}$ 和 $\mathrm{d}\mathbf{X}$ 之间的精确关系：

$$
\mathrm{d}\mathbf{x} = \mathbf{F} \, \mathrm{d}\mathbf{X}
$$

这个关系表明，变形梯度 $\mathbf{F}$ 在每一点都定义了一个[线性变换](@entry_id:149133)，将该点邻域内的物质纤维（线元）从参考构型“推送”到当前构型。因此，$\mathbf{F}$ 是一个**两点张量 (two-point tensor)**，因为它将一个定义在参考构型中某点 $\mathbf{X}$ 的[切空间](@entry_id:199137)中的向量，映射到当前构型中对应点 $\mathbf{x}$ 的[切空间](@entry_id:199137)中的向量 。$\mathbf{F}$ 完整地包含了关于局部变形的所有信息，包括拉伸、压缩、剪切和旋转。

### 变形的几何解释：[拉伸与旋转](@entry_id:150197)

变形梯度 $\mathbf{F}$ 同时包含了物体的刚体旋转和纯粹的变形（拉伸与剪切）。为了分别量化这两种效应，我们利用**极分解定理 (Polar Decomposition Theorem)**。该定理指出，任何可逆的[二阶张量](@entry_id:199780) $\mathbf{F}$ 都可以唯一地分解为两种形式：

1.  **右极分解 (Right Polar Decomposition)**: $\mathbf{F} = \mathbf{R} \mathbf{U}$
2.  **左极分解 (Left Polar Decomposition)**: $\mathbf{F} = \mathbf{V} \mathbf{R}$

在这里，$\mathbf{R}$ 是一个**[旋转张量](@entry_id:191990) (rotation tensor)**，属于[特殊正交群](@entry_id:146418) $\mathrm{SO}(3)$，即 $\mathbf{R}^{\mathsf{T}}\mathbf{R}=\mathbf{I}$ 且 $\det\mathbf{R}=1$。它描述了物质单元的局部刚体旋转。

$\mathbf{U}$ 和 $\mathbf{V}$ 分别称为**右[拉伸张量](@entry_id:193200) (right stretch tensor)** 和**左[拉伸张量](@entry_id:193200) (left stretch tensor)**。它们都是对称且正定的[二阶张量](@entry_id:199780)，纯粹地描述了变形，即沿其特征方向的拉伸或压缩。$\mathbf{U}$ 作用于参考构型中的向量，而 $\mathbf{V}$ 作用于当前构型中的向量。

为了计算这些量，我们引入两个重要的变形度量：**右柯西-格林变形张量 (right Cauchy-Green deformation tensor)** $\mathbf{C}$ 和**左柯西-格林变形张量 (left Cauchy-Green (or Finger) deformation tensor)** $\mathbf{b}$。它们的定义及其与[拉伸张量](@entry_id:193200)的关系如下：

$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}} \mathbf{F} = (\mathbf{R}\mathbf{U})^{\mathsf{T}}(\mathbf{R}\mathbf{U}) = \mathbf{U}^{\mathsf{T}}\mathbf{R}^{\mathsf{T}}\mathbf{R}\mathbf{U} = \mathbf{U}^2
$$
$$
\mathbf{b} = \mathbf{F} \mathbf{F}^{\mathsf{T}} = (\mathbf{V}\mathbf{R})(\mathbf{V}\mathbf{R})^{\mathsf{T}} = \mathbf{V}\mathbf{R}\mathbf{R}^{\mathsf{T}}\mathbf{V}^{\mathsf{T}} = \mathbf{V}^2
$$

因此，[拉伸张量](@entry_id:193200) $\mathbf{U}$ 和 $\mathbf{V}$ 分别是 $\mathbf{C}$ 和 $\mathbf{b}$ 的唯一正定平方根，即 $\mathbf{U} = \sqrt{\mathbf{C}}$ 和 $\mathbf{V} = \sqrt{\mathbf{b}}$。一旦求得 $\mathbf{U}$，[旋转张量](@entry_id:191990) $\mathbf{R}$ 即可通过 $\mathbf{R} = \mathbf{F}\mathbf{U}^{-1}$ 计算得出。

我们通过一个**简单剪切 (simple shear)** 的例子来具体说明极分解的计算过程 。考虑一个变形梯度为 $\mathbf{F} = \mathbf{I} + \gamma \mathbf{e}_1 \otimes \mathbf{e}_2$ 的均匀变形，其矩阵形式为：
$$
[F] = \begin{pmatrix} 1  \gamma  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix}
$$
首先计算[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$：
$$
[C] = [F]^{\mathsf{T}}[F] = \begin{pmatrix} 1  0  0 \\ \gamma  1  0 \\ 0  0  1 \end{pmatrix} \begin{pmatrix} 1  \gamma  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix} = \begin{pmatrix} 1  \gamma  0 \\ \gamma  \gamma^2 + 1  0 \\ 0  0  1 \end{pmatrix}
$$
接下来，我们求解对称正定矩阵 $[U]$ 使得 $[U]^2 = [C]$。经过代数运算可以得到：
$$
[U] = \frac{1}{\sqrt{\gamma^2+4}} \begin{pmatrix} 2  \gamma  0 \\ \gamma  \gamma^2+2  0 \\ 0  0  \sqrt{\gamma^2+4} \end{pmatrix}
$$
最后，计算[旋转张量](@entry_id:191990) $\mathbf{R} = \mathbf{F}\mathbf{U}^{-1}$：
$$
[R] = \frac{1}{\sqrt{\gamma^2+4}} \begin{pmatrix} 2  \gamma  0 \\ -\gamma  2  0 \\ 0  0  \sqrt{\gamma^2+4} \end{pmatrix}
$$
这个 $\mathbf{R}$ 矩阵描述了一个在 $\mathbf{e}_1$-$\mathbf{e}_2$ 平面内的旋转。通过与标准旋转矩阵 $\begin{pmatrix} \cos\theta  -\sin\theta \\ \sin\theta  \cos\theta \end{pmatrix}$ 比较，我们可以发现 $\cos\theta = \frac{2}{\sqrt{\gamma^2+4}}$ 和 $\sin\theta = -\frac{\gamma}{\sqrt{\gamma^2+4}}$。因此，剪切变形包含了一个大小为 $\theta(\gamma) = \arctan(-\gamma/2)$ 的刚体旋转。这清晰地揭示了纯粹的[剪切变形](@entry_id:170920)在几何上包含拉伸和旋转两个部分。

### 应变张量：度量变形

变形梯度 $\mathbf{F}$ 本身并不是一个理想的“应变”度量，因为它在刚体旋转后会发生改变（$\mathbf{F}^* = \mathbf{Q}\mathbf{F}$），而一个纯粹的[应变度量](@entry_id:755495)应该在[刚体运动](@entry_id:193355)下保持不变。为了构建这样的度量，我们考察物质线元长度的平方的变化。

参考构型中线元 $\mathrm{d}\mathbf{X}$ 的长度平方为 $\mathrm{d}S^2 = \mathrm{d}\mathbf{X} \cdot \mathrm{d}\mathbf{X}$。当前构型中对应[线元](@entry_id:196833) $\mathrm{d}\mathbf{x}$ 的长度平方为 $\mathrm{d}s^2 = \mathrm{d}\mathbf{x} \cdot \mathrm{d}\mathbf{x}$。利用 $\mathrm{d}\mathbf{x} = \mathbf{F} \mathrm{d}\mathbf{X}$，我们有：
$$
\mathrm{d}s^2 = (\mathbf{F} \mathrm{d}\mathbf{X}) \cdot (\mathbf{F} \mathrm{d}\mathbf{X}) = \mathrm{d}\mathbf{X} \cdot (\mathbf{F}^{\mathsf{T}}\mathbf{F}) \mathrm{d}\mathbf{X} = \mathrm{d}\mathbf{X} \cdot \mathbf{C} \mathrm{d}\mathbf{X}
$$
长度平方的改变为 $\mathrm{d}s^2 - \mathrm{d}S^2 = \mathrm{d}\mathbf{X} \cdot (\mathbf{C} - \mathbf{I}) \mathrm{d}\mathbf{X}$。

我们定义**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)** $\mathbf{E}$ 来量化这种变化，使得 $\mathrm{d}s^2 - \mathrm{d}S^2 = 2 \mathrm{d}\mathbf{X} \cdot \mathbf{E} \mathrm{d}\mathbf{X}$。由此可得：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^{\mathsf{T}}\mathbf{F} - \mathbf{I})
$$
$\mathbf{E}$ 是一个**物质 (material)** 或 **拉格朗日 (Lagrangian)** 张量，因为它定义在参考构型上，与物[质点](@entry_id:186768)紧密相连。

类似地，我们可以将长度平方的变化表示在当前构型中。利用 $\mathrm{d}\mathbf{X} = \mathbf{F}^{-1} \mathrm{d}\mathbf{x}$，我们有 $\mathrm{d}S^2 = \mathrm{d}\mathbf{x} \cdot (\mathbf{F}^{-\mathsf{T}}\mathbf{F}^{-1}) \mathrm{d}\mathbf{x} = \mathrm{d}\mathbf{x} \cdot \mathbf{b}^{-1} \mathrm{d}\mathbf{x}$。于是 $\mathrm{d}s^2 - \mathrm{d}S^2 = \mathrm{d}\mathbf{x} \cdot (\mathbf{I} - \mathbf{b}^{-1}) \mathrm{d}\mathbf{x}$。我们定义**[欧拉-阿尔曼西应变张量](@entry_id:194948) (Euler-Almansi strain tensor)** $\mathbf{e}$ 来量化这种变化，使得 $\mathrm{d}s^2 - \mathrm{d}S^2 = 2 \mathrm{d}\mathbf{x} \cdot \mathbf{e} \mathrm{d}\mathbf{x}$。由此可得：
$$
\mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{b}^{-1}) = \frac{1}{2}(\mathbf{I} - \mathbf{F}^{-\mathsf{T}}\mathbf{F}^{-1})
$$
$\mathbf{e}$ 是一个**空间 (spatial)** 或 **欧拉 (Eulerian)** 张量，因为它定义在当前构型上。

这两个[应变张量](@entry_id:193332)的关键特性是，对于任何纯刚体旋转（$\mathbf{F}=\mathbf{Q}$），我们有 $\mathbf{C} = \mathbf{Q}^{\mathsf{T}}\mathbf{Q} = \mathbf{I}$ 和 $\mathbf{b} = \mathbf{Q}\mathbf{Q}^{\mathsf{T}} = \mathbf{I}$，这导致 $\mathbf{E} = \mathbf{0}$ 和 $\mathbf{e} = \mathbf{0}$。这证实了它们是纯粹的变形度量，不受刚体旋转的影响 。此外，对于主拉伸为 $\lambda_i$ 的纯拉伸变形，$\mathbf{E}$ 和 $\mathbf{e}$ 的主值分别为 $E_i = \frac{1}{2}(\lambda_i^2 - 1)$ 和 $e_i = \frac{1}{2}(1 - \lambda_i^{-2})$。

### 变形的[张量变换](@entry_id:183453)：推前与[拉回](@entry_id:160816)

为了系统地处理在参考构型和当前构型之间转换张量的问题，我们正式引入**推前 (push-forward)** 和**[拉回](@entry_id:160816) (pull-back)** 操作。这些操作由变形映射 $\boldsymbol{\chi}$ 及其梯度 $\mathbf{F}$ 诱导。

- **向量的推前**：一个定义在参考构型中的向量（例如，[线元](@entry_id:196833) $\mathrm{d}\mathbf{X}$）通过 $\mathbf{F}$ 被“推前”到当前构型，成为一个空间向量 $\mathrm{d}\mathbf{x} = \mathbf{F} \mathrm{d}\mathbf{X}$。
- **向量的[拉回](@entry_id:160816)**：反之，一个空间向量 $\mathbf{v}$ 通过 $\mathbf{F}^{-1}$ 被“[拉回](@entry_id:160816)”到参考构型，成为一个物质向量 $\mathbf{V} = \mathbf{F}^{-1} \mathbf{v}$。

更重要的是这些操作如何作用于描述物理性质的[二阶张量](@entry_id:199780)。以度量张量为例，它定义了空间中的[内积](@entry_id:158127)和长度。在笛卡尔坐标系下，空间度量 $\mathbf{g}$ 由单位张量 $\mathbf{I}$ 表示。将空间度量 $\mathbf{g}$ **[拉回](@entry_id:160816)**到参考构型，意味着我们在参考构型中定义一个新的度量，用它来测量物质向量，其结果与将这些向量推前到当前构型后用空间度量 $\mathbf{g}$ 测量的结果相同。对于任意两个物质向量 $\mathrm{d}\mathbf{X}_1$ 和 $\mathrm{d}\mathbf{X}_2$，这个[拉回](@entry_id:160816)的度量 $\chi^*(\mathbf{g})$ 必须满足：
$$
(\chi^*(\mathbf{g}))(\mathrm{d}\mathbf{X}_1, \mathrm{d}\mathbf{X}_2) = \mathbf{g}(\mathbf{F} \mathrm{d}\mathbf{X}_1, \mathbf{F} \mathrm{d}\mathbf{X}_2) = (\mathbf{F} \mathrm{d}\mathbf{X}_1)^{\mathsf{T}} \mathbf{I} (\mathbf{F} \mathrm{d}\mathbf{X}_2) = \mathrm{d}\mathbf{X}_1^{\mathsf{T}} (\mathbf{F}^{\mathsf{T}}\mathbf{F}) \mathrm{d}\mathbf{X}_2
$$
因此，我们发现[拉回](@entry_id:160816)的空间度量正是[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$。这赋予了 $\mathbf{C}$ 一个深刻的几何意义：它是在参考构型中体现当前构型几何的度量张量 。

不同类型的张量有不同的变换法则。例如，一个将参考构型中的切向量映射到[切向量](@entry_id:265494)的[二阶张量](@entry_id:199780) $\mathbf{T}$（类型(1,1)），其推前形式 $\mathbf{t}$ 的变换法则是 $\mathbf{t} = \mathbf{F} \mathbf{T} \mathbf{F}^{-1}$。而[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$ 与[欧拉-阿尔曼西应变](@entry_id:187104) $\mathbf{e}$ 之间的关系正是通过[拉回](@entry_id:160816)操作联系起来的：
$$
\mathbf{E} = \mathbf{F}^{\mathsf{T}} \mathbf{e} \mathbf{F}
$$
这表明 $\mathbf{E}$ 是空间应变张量 $\mathbf{e}$ 的[拉回](@entry_id:160816) 。理解这些变换法则是正确建立和转换不同构型下物理方程（如本构关系）的基础。

### 物理容许性与相容性

并非任意一个张量场 $\mathbf{F}(\mathbf{X})$ 都能代表一个真实的物理变形。它必须满足两个基本条件：物理容许性和[运动学](@entry_id:173318)相容性。

**物理容许性 (Physical Admissibility)** 主要关注于物质的不可侵入性。首先，局部体积变化由变形梯度的[雅可比行列式](@entry_id:137120) $J = \det \mathbf{F}$ 描述：一个无穷小的参考体积 $\mathrm{d}V_0$ 变形为 $\mathrm{d}V_t = J \mathrm{d}V_0$。
- **保持定向**：为了保持物质的原始手性（例如，右手表观系统不变形为左手系），变形后的体积必须为正，即 $J > 0$。如果 $J < 0$，则发生局部物质反转，这在物理上是不可能的。
- **物质不可压缩至零体积**：如果 $J = 0$，则一个三维物质微元被压缩成一个平面或一条线，体积为零。根据[质量守恒定律](@entry_id:147377) $\rho_t = \rho_0 / J$（其中 $\rho_0$ 和 $\rho_t$ 分别是参考和当前密度），$J \to 0$ 意味着密度趋于无穷大，这在物理上也是不可能的。
- **[局部可逆性](@entry_id:143266)**：根据[反函数定理](@entry_id:275014)，只有当 $J = \det \mathbf{F} \neq 0$ 时，变形映射 $\boldsymbol{\chi}$ 才在局部是可逆的。

因此，一个局部物理上容许的变形必须处处满足 $J = \det\mathbf{F} > 0$ 。值得注意的是，这是一个**局部**条件。即使处处满足 $J > 0$，整个物体仍可能发生自相交或穿透，即映射 $\boldsymbol{\chi}$ 在全局上不是单射的。因此，全局的物理容许性还需要额外的**全局[单射性](@entry_id:147722) (global injectivity)** 条件 。

**运动学相容性 (Kinematic Compatibility)** 回答了这样一个问题：给定一个连续可微的张量场 $\mathbf{F}(\mathbf{X})$，是否存在一个[位移场](@entry_id:141476)或运动场 $\boldsymbol{\varphi}(\mathbf{X})$，使得 $\mathbf{F}$ 是它的梯度？
如果 $\mathbf{F} = \nabla_{\mathbf{X}} \boldsymbol{\varphi}$，那么对于足够光滑的 $\boldsymbol{\varphi}$，其二阶[混合偏导数](@entry_id:139334)必须相等，即 $\frac{\partial^2 \varphi_i}{\partial X_J \partial X_K} = \frac{\partial^2 \varphi_i}{\partial X_K \partial X_J}$。这等价于要求 $\mathbf{F}$ 的每一行的旋度都为零。这个条件可以简洁地写成一个张量方程：
$$
\operatorname{Curl} \mathbf{F} = \mathbf{0}
$$
其中 $\operatorname{Curl}$ 算子作用于 $\mathbf{F}$ 的每一行。在单连通区域内，这个条件是 $\mathbf{F}$ 场可积的充分必要条件。从几何上看，该条件等价于 $\mathbf{F}$ 沿任何闭合路径的积分为零，$\oint \mathbf{F} \, \mathrm{d}\mathbf{X} = \mathbf{0}$。在[晶体塑性理论](@entry_id:180579)中，这个积分被称为**[伯格斯矢量](@entry_id:160637) (Burgers vector)**，其非零值表示存在[位错](@entry_id:157482)等[晶格缺陷](@entry_id:270099)。因此，[相容性条件](@entry_id:637057)在宏观尺度上意味着连续体中没有连续分布的几何缺陷 。对于多连通区域（例如带孔洞的物体），除了要求 $\operatorname{Curl}\mathbf{F} = \mathbf{0}$，还必须要求 $\mathbf{F}$ 绕所有不可收缩回路的[环路积分](@entry_id:164828)为零，以保证位移场的[单值性](@entry_id:174849) 。

### [客观性原理](@entry_id:185412)

物理定律和[本构关系](@entry_id:186508)不应依赖于观察者。在力学中，不同的观察者通过一个刚体运动（[旋转和平移](@entry_id:175994)）相关联。这一要求被称为**[物质客观性原理](@entry_id:191727) (principle of material objectivity)** 或**标架无关性 (frame-indifference)**。

考虑一个叠加在当前构型上的[刚体运动](@entry_id:193355)，将点 $\mathbf{x}$ 移动到 $\mathbf{x}^* = \mathbf{Q}(t)\mathbf{x} + \mathbf{c}(t)$，其中 $\mathbf{Q}(t)$ 是一个时间相关的[旋转张量](@entry_id:191990)。在这种变换下，新的变形梯度为 $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$。

一个依赖于 $\mathbf{F}$ 的标量物理量 $\phi(\mathbf{F})$ 如果是客观的，其值就不能因观察者的改变而改变。这意味着它必须满足：
$$
\phi(\mathbf{F}^*) = \phi(\mathbf{F}) \quad \text{即} \quad \phi(\mathbf{Q}\mathbf{F}) = \phi(\mathbf{F})
$$
对于所有的旋转 $\mathbf{Q} \in \mathrm{SO}(3)$ 成立。

让我们用这个判据来检验两个简单的量 。
1.  $\phi_1(\mathbf{F}) = \operatorname{tr}(\mathbf{F})$：一般来说 $\operatorname{tr}(\mathbf{Q}\mathbf{F}) \neq \operatorname{tr}(\mathbf{F})$。因此，$\operatorname{tr}(\mathbf{F})$ 不是一个客观标量。
2.  $\phi_2(\mathbf{F}) = \operatorname{tr}(\mathbf{C})$：由于 $\mathbf{C}^* = (\mathbf{Q}\mathbf{F})^{\mathsf{T}}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^{\mathsf{T}}\mathbf{Q}^{\mathsf{T}}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \mathbf{C}$，我们有 $\operatorname{tr}(\mathbf{C}^*) = \operatorname{tr}(\mathbf{C})$。因此，$\operatorname{tr}(\mathbf{C})$ 是一个客观标量。

这个例子揭示了一个普遍规律：任何只通过[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ （或右[拉伸张量](@entry_id:193200) $\mathbf{U}$）表达的量都是客观的。例如，[格林-拉格朗日应变](@entry_id:170427) $\mathbf{E}$ 就是客观的。

为了构建客观的[本构关系](@entry_id:186508)（例如[应变能函数](@entry_id:178435)），我们通常使用 $\mathbf{C}$ 的**[主不变量](@entry_id:193522) (principal invariants)**，因为它们是客观标量。对于三维空间中的张量 $\mathbf{C}$，其三个[主不变量](@entry_id:193522)为：
$$
\begin{align*}
I_1 = \operatorname{tr}(\mathbf{C}) \\
I_2 = \frac{1}{2}[(\operatorname{tr}\mathbf{C})^2 - \operatorname{tr}(\mathbf{C}^2)] \\
I_3 = \det(\mathbf{C}) = (\det\mathbf{F})^2 = J^2
\end{align*}
$$
这些[不变量](@entry_id:148850)是客观的，因为它们只依赖于 $\mathbf{C}$ 的[特征值](@entry_id:154894)，而 $\mathbf{C}$ 本身是客观的 。

### 变形率与速度梯度

为了描述变形随时间的变化率，我们引入**[速度梯度张量](@entry_id:270928) (velocity gradient tensor)** $\mathbf{L}$。它被定义为[空间速度](@entry_id:190294)场 $\mathbf{v}(\mathbf{x},t)$ 相对于当前空间坐标 $\mathbf{x}$ 的梯度：
$$
\mathbf{L} = \nabla_{\mathbf{x}} \mathbf{v}
$$
速度梯度与变形梯度的[物质时间导数](@entry_id:190892) $\dot{\mathbf{F}}$ 之间存在一个基本关系。通过[链式法则](@entry_id:190743)，我们有 $\dot{\mathbf{F}} = \nabla_{\mathbf{X}}\mathbf{v} = (\nabla_{\mathbf{x}}\mathbf{v})(\nabla_{\mathbf{X}}\mathbf{x}) = \mathbf{L}\mathbf{F}$。因此，
$$
\mathbf{L} = \dot{\mathbf{F}} \mathbf{F}^{-1}
$$
这个关系在更新有限元计算中的变形梯度时至关重要 。

[速度梯度](@entry_id:261686) $\mathbf{L}$ 可以分解为其对称和反对称部分：$\mathbf{L} = \mathbf{D} + \mathbf{W}$。
- **变形率张量 (rate of deformation tensor)** $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\mathsf{T}})$ 是 $\mathbf{L}$ 的对称部分。它描述了物质微元的拉伸和剪切变形速率。其迹 $\operatorname{tr}(\mathbf{D}) = \nabla_{\mathbf{x}}\cdot\mathbf{v}$ 代表了单位体积的体积变化率，即膨胀率。
- **[自旋张量](@entry_id:187346) (spin tensor)** $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\mathsf{T}})$ 是 $\mathbf{L}$ 的反对称部分。它描述了物质微元的瞬时刚体旋转[角速度](@entry_id:192539)（或称涡度）。一个经典的例子是简单剪切流 $\mathbf{v} = (\dot{\gamma}x_2, 0, 0)$，其[自旋张量](@entry_id:187346)非零，表明材料微元在剪切过程中会发生旋转 。

在[客观性原理](@entry_id:185412)的框架下，$\mathbf{D}$ 和 $\mathbf{W}$ 的变换行为有显著差异。可以证明，在叠加刚体运动下，变形率张量是客观的（变换为 $\mathbf{D}^* = \mathbf{Q}\mathbf{D}\mathbf{Q}^{\mathsf{T}}$），而[自旋张量](@entry_id:187346)不是客观的（变换为 $\mathbf{W}^* = \mathbf{Q}\mathbf{W}\mathbf{Q}^{\mathsf{T}} + \dot{\mathbf{Q}}\mathbf{Q}^{\mathsf{T}}$）。$\dot{\mathbf{Q}}\mathbf{Q}^{\mathsf{T}}$ 项表示叠加的刚体旋转速率，这表明[自旋张量](@entry_id:187346)的值会因观察者的旋转而改变 。

最后，需要注意的是，变形率张量 $\mathbf{D}$ 与[格林-拉格朗日应变](@entry_id:170427)的时间导数 $\dot{\mathbf{E}}$ 并不相等。它们是不同构型下的量，其关系为 $\dot{\mathbf{E}} = \mathbf{F}^{\mathsf{T}}\mathbf{D}\mathbf{F}$，即 $\dot{\mathbf{E}}$ 是 $\mathbf{D}$ 的[拉回](@entry_id:160816)。

### [乘法分解](@entry_id:199514)与[中间构型](@entry_id:193000)

对于[弹塑性](@entry_id:193198)等具有复杂内部[结构演化](@entry_id:186256)的材料，一个非常有用的运动学框架是**变形梯度的[乘法分解](@entry_id:199514) (multiplicative decomposition of the deformation gradient)**。其核心思想是将总变形梯度 $\mathbf{F}$ 分解为一个“塑性”部分 $\mathbf{F}_p$ 和一个“弹性”部分 $\mathbf{F}_e$ 的乘积：
$$
\mathbf{F} = \mathbf{F}_e \mathbf{F}_p
$$
这个分解引入了一个概念上的**[中间构型](@entry_id:193000) (intermediate configuration)**。从运动学角度看，这相当于一个两步过程：首先，物质通过 $\mathbf{F}_p$ 从参考构型进行“塑性”重排，到达[中间构型](@entry_id:193000)；然后，再通过 $\mathbf{F}_e$ 从[中间构型](@entry_id:193000)进行“弹性”变形，到达最终的当前构型 。

纯粹从[运动学](@entry_id:173318)角度出发，这个分解有几个重要的特点：
- **不唯一性**：对于给定的 $\mathbf{F}$，其分解 $\mathbf{F}_e$ 和 $\mathbf{F}_p$ 不是唯一的。我们可以引入任意一个可逆张量 $\mathbf{G}$，定义新的因子 $\mathbf{F}'_e = \mathbf{F}_e \mathbf{G}$ 和 $\mathbf{F}'_p = \mathbf{G}^{-1}\mathbf{F}_p$，它们的乘积仍然是 $\mathbf{F}$。在具体的物理理论中，这种不确定性通常通过本构假设来消除（例如，要求[中间构型](@entry_id:193000)反映材料的[晶格](@entry_id:196752)取向）。
- **$\mathbf{F}_p$ 的不相容性**：即使总变形梯度 $\mathbf{F}$ 是相容的（即 $\operatorname{Curl}\mathbf{F} = \mathbf{0}$），其塑性部分 $\mathbf{F}_p$ 也完全可以是不相容的（$\operatorname{Curl}\mathbf{F}_p \neq \mathbf{0}$）。这种情况在物理上对应于材料中存在连续分布的[位错](@entry_id:157482)等微观缺陷。弹性变形 $\mathbf{F}_e$ 则必须“补偿”这种不相容性，以保证最终的总变形 $\mathbf{F}$ 是相容的 。
- **体积变化**：在[金属塑性](@entry_id:176585)理论中，通常假设塑性变形是保持体积的，即 $\det\mathbf{F}_p = 1$。然而，这并非一个普适的运动学定律，而是一个**本构假设**。对于多孔材料的压实或剪胀等现象，塑性[体积应变](@entry_id:267252)是存在的，即 $\det\mathbf{F}_p \neq 1$。

[乘法分解](@entry_id:199514)极大地扩展了连续介质力学的描述能力，为建立复杂材料（如金属、土壤和聚合物）的有限变形[本构模型](@entry_id:174726)提供了坚实的运动学基础。例如，[右柯西-格林张量](@entry_id:174156)可以表示为 $\mathbf{C} = \mathbf{F}_p^{\mathsf{T}} \mathbf{C}_e \mathbf{F}_p$，其中 $\mathbf{C}_e = \mathbf{F}_e^{\mathsf{T}} \mathbf{F}_e$ 是弹性柯西-格林张量。这使得应力或[应变能](@entry_id:162699)可以被假设为仅依赖于弹性变形部分，从而将弹性响应与不可恢复的[塑性流动](@entry_id:201346)分离开来 。