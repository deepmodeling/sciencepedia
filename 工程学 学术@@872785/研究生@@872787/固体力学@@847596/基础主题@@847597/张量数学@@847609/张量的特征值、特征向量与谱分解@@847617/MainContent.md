## 引言
张量的[特征值](@entry_id:154894)、[特征向量](@entry_id:151813)和谱分解是现代固体力学中不可或缺的数学语言。它们将抽象的张量算子转化为具有明确物理意义的量，如独立于[坐标系](@entry_id:156346)的[主应力](@entry_id:176761)和主拉伸，从而构成了连接理论与工程实践的桥梁。然而，初学者常常难以将线性代数中的抽象概念与连续介质力学中的具体物理问题（如应力状态分析或有限变形）建立起直观且严谨的联系。本文旨在填补这一认知鸿沟，系统性地阐明张量[谱理论](@entry_id:275351)的内涵及其在力学中的核心地位。

在接下来的章节中，我们将踏上一段从原理到应用的探索之旅。在“原则与机理”一章，我们将从物理动因出发，揭示[特征值问题](@entry_id:142153)如何自然地源于寻找[主应力方向](@entry_id:753737)，并深入探讨[对称张量](@entry_id:148092)的[谱定理](@entry_id:136620)、非对称张量的[奇异值分解](@entry_id:138057)等核心数学工具。随后，在“应用与跨学科联系”一章，我们将展示这些理论如何在[连续介质运动学](@entry_id:747813)、本构关系建模、材料损伤分析以及[计算力学](@entry_id:174464)算法中发挥关键作用。最后，通过“动手实践”部分，读者将有机会通过具体问题来巩固所学知识，将理论真正内化为解决实际问题的能力。

## 原则与机理

在本章中，我们将深入探讨[二阶张量](@entry_id:199780)的[特征值](@entry_id:154894)、[特征向量](@entry_id:151813)和谱分解的数学原理与力学机理。这些概念是[固体力学](@entry_id:164042)，尤其是本构理论和有限变形运动学中不可或缺的基石。我们将从[对称张量](@entry_id:148092)（如[应力张量和应变张量](@entry_id:755512)）的谱理论出发，逐步扩展到非对称张量（如[速度梯度张量](@entry_id:270928)）的更广义分解方法。

### 特征值问题的物理动因：[主应力与主方向](@entry_id:193792)

在连续介质力学中，[张量特征值问题](@entry_id:198059)的概念并非源于纯粹的数学抽象，而是植根于对[物理可观测量](@entry_id:154692)（Observables）的深刻理解。一个典型的例子便是柯西应力张量 $\boldsymbol{\sigma}$。根据柯西应力定理，作用在某一点处、法向为[单位向量](@entry_id:165907) $\boldsymbol{n}$ 的[截面](@entry_id:154995)上的面力密度（牵[引力](@entry_id:175476)）矢量 $\boldsymbol{t}$，可以通过一个[线性映射](@entry_id:185132)得到：$\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n}$。

一般情况下，牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}$ 与[截面](@entry_id:154995)法向 $\boldsymbol{n}$ 既不平行也不垂直。然而，我们可以设想是否存在一些特殊的[截面](@entry_id:154995)方向，其上的牵[引力](@entry_id:175476)完全是法向的，即没有任何剪切分量。对于这样的[截面](@entry_id:154995)，牵[引力](@entry_id:175476)矢量 $\boldsymbol{t}$ 必然与其法向矢量 $\boldsymbol{n}$ 共线。这个物理条件可以表示为：

$$
\boldsymbol{t} = \lambda \boldsymbol{n}
$$

其中 $\lambda$ 是一个标量，表示该法向牵[引力](@entry_id:175476)的大小。将柯西应力定理代入上式，我们便得到了一个深刻的数学关系式：

$$
\boldsymbol{\sigma}\boldsymbol{n} = \lambda \boldsymbol{n}
$$

这正是线性代数中的标准**特征值问题** (Eigenvalue Problem) [@problem_id:2633158]。在此物理情境下：
- 使剪切牵[引力](@entry_id:175476)为零的特殊方向 $\boldsymbol{n}$ 被称为**[主方向](@entry_id:276187)** (Principal Directions)，它们是应力张量 $\boldsymbol{\sigma}$ 的**[特征向量](@entry_id:151813)** (Eigenvectors)。
- 在这些主方向[截面](@entry_id:154995)上的法向牵[引力](@entry_id:175476)大小 $\lambda$ 被称为**[主应力](@entry_id:176761)** (Principal Stresses)，它们是[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的**[特征值](@entry_id:154894)** (Eigenvalues)。

[主应力](@entry_id:176761)和[主方向](@entry_id:276187)是真实、可测量的物理量，因此它们的数值和方向不应依赖于我们描述它们所选择的[坐标系](@entry_id:156346)。这种性质被称为**客观性** (Objectivity) 或**标架无关性** (Frame-Independence)。数学上，这意味着在[坐标系](@entry_id:156346)旋转（由正交张量 $\boldsymbol{Q}$ 描述）下，张量分量虽然会改变（$\boldsymbol{\sigma}' = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}$），但其物理内涵——[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)所代表的物理方向——保持不变。[特征值](@entry_id:154894)作为标量是完全不变的，而[特征向量](@entry_id:151813)作为空间中的一个方向，其坐标分量会随[坐标系](@entry_id:156346)客观地变换（$\boldsymbol{n}' = \boldsymbol{Q}\boldsymbol{n}$）[@problem_id:2633158]。

### 特征值问题的数学基础

#### 代数定义与[内积](@entry_id:158127)无关性

从更根本的层面看，一个[线性算子](@entry_id:149003)（二阶张量）$\mathbf{T}$ 的[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)的定义是一个纯粹的**代数**概念 [@problem_id:2633198]。方程 $\mathbf{T}\mathbf{n} = \lambda\mathbf{n}$ 只涉及矢量空间的加法和[标量乘法](@entry_id:155971)运算。因此，一个给定的线性算子 $\mathbf{T}$ 的[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)是其内禀属性，不依赖于在该矢量空间上是否定义了**[内积](@entry_id:158127)** (Inner Product) 或度规。[内积](@entry_id:158127)引入了长度、角度和正交性等**几何**概念，但这些对于定义[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)本身而言并非必要。

#### [特征方程](@entry_id:265849)与[张量不变量](@entry_id:203254)

[特征值](@entry_id:154894) $\lambda$ 是**[特征多项式](@entry_id:150909)** (Characteristic Polynomial) $\det(\mathbf{T} - \lambda\mathbf{I}) = 0$ 的根。对于三维空间中的[二阶张量](@entry_id:199780)，这是一个关于 $\lambda$ 的三次方程。这个方程可以完全由张量的[不变量](@entry_id:148850)来表示 [@problem_id:2633187]。张量的**[主不变量](@entry_id:193522)** (Principal Invariants) 是在[坐标变换](@entry_id:172727)下保持不变的标量，它们是：

$$
\begin{align*}
I_1(\mathbf{T})  &= \operatorname{tr}\mathbf{T} \\
I_2(\mathbf{T})  &= \frac{1}{2} [(\operatorname{tr}\mathbf{T})^2 - \operatorname{tr}(\mathbf{T}^2)] \\
I_3(\mathbf{T})  &= \det\mathbf{T}
\end{align*}
$$

这些[不变量](@entry_id:148850)分别是[特征值](@entry_id:154894) $\lambda_1, \lambda_2, \lambda_3$ 的初等[对称多项式](@entry_id:153581)：
$I_1 = \lambda_1 + \lambda_2 + \lambda_3$
$I_2 = \lambda_1\lambda_2 + \lambda_2\lambda_3 + \lambda_3\lambda_1$
$I_3 = \lambda_1\lambda_2\lambda_3$

因此，特征方程可以典范地写为：

$$
\lambda^3 - I_1\lambda^2 + I_2\lambda - I_3 = 0
$$

由于[不变量](@entry_id:148850) $I_1, I_2, I_3$ 在所有[正交坐标](@entry_id:166074)系下都具有相同的值，所以特征方程及其根（[特征值](@entry_id:154894)）也是与[坐标系](@entry_id:156346)无关的，这为前述主应力的客观性提供了严格的[数学证明](@entry_id:137161)。其他如**[弗罗贝尼乌斯范数](@entry_id:143384)** (Frobenius norm) $\|\mathbf{T}\| = \sqrt{\mathbf{T}:\mathbf{T}}$ 等也是重要的[不变量](@entry_id:148850) [@problem_id:2633192]。

### 对称张量的[谱理论](@entry_id:275351)

在固体力学中，我们遇到的大多数重要张量，如柯西应力张量 $\boldsymbol{\sigma}$（由角动量守恒保证）、[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E}$ 以及[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$，都是对称的。对称性极大地简化并丰富了特征值问题的内涵。

一个算子 $\mathbf{T}$ 关于某个[内积](@entry_id:158127) $\langle \cdot, \cdot \rangle$ 是对称的（或称**自伴的**），如果对于任意矢量 $\mathbf{u}, \mathbf{v}$，都满足 $\langle \mathbf{T}\mathbf{u}, \mathbf{v} \rangle = \langle \mathbf{u}, \mathbf{T}\mathbf{v} \rangle$。需要强调的是，对称性是与[内积](@entry_id:158127)相关的属性；一个算子在一个[内积](@entry_id:158127)下是对称的，在另一个[内积](@entry_id:158127)下可能并非如此 [@problem_id:2633198]。在标准的[欧几里得空间](@entry_id:138052)中，这等价于张量的[矩阵表示](@entry_id:146025)是对称的，即 $\mathbf{T} = \mathbf{T}^{\mathsf{T}}$。

**[谱定理](@entry_id:136620)** (Spectral Theorem) 是对称张量理论的核心。它指出，对于一个三维实对称二阶张量 $\mathbf{T}$：
1.  它有三个**实数**[特征值](@entry_id:154894)。
2.  存在一组由其[特征向量](@entry_id:151813)构成的**[标准正交基](@entry_id:147779)**。

[谱定理](@entry_id:136620)的一个关键推论是，属于**不同**[特征值](@entry_id:154894)的[特征向量](@entry_id:151813)必定是相互**正交**的 [@problem_id:2686494]。这可以通过简单的代数证明：若 $\mathbf{T}\mathbf{n}_1 = \lambda_1\mathbf{n}_1$ 且 $\mathbf{T}\mathbf{n}_2 = \lambda_2\mathbf{n}_2$ 并且 $\lambda_1 \neq \lambda_2$，则：
$\lambda_1 (\mathbf{n}_1 \cdot \mathbf{n}_2) = (\lambda_1 \mathbf{n}_1) \cdot \mathbf{n}_2 = (\mathbf{T}\mathbf{n}_1) \cdot \mathbf{n}_2 = \mathbf{n}_1 \cdot (\mathbf{T}^{\mathsf{T}}\mathbf{n}_2) = \mathbf{n}_1 \cdot (\mathbf{T}\mathbf{n}_2) = \mathbf{n}_1 \cdot (\lambda_2 \mathbf{n}_2) = \lambda_2 (\mathbf{n}_1 \cdot \mathbf{n}_2)$。
整理得到 $(\lambda_1 - \lambda_2)(\mathbf{n}_1 \cdot \mathbf{n}_2) = 0$。因为 $\lambda_1 \neq \lambda_2$，所以必然有 $\mathbf{n}_1 \cdot \mathbf{n}_2 = 0$。

[谱定理](@entry_id:136620)保证了我们可以将任何对称张量 $\mathbf{T}$ 分解为其[特征值](@entry_id:154894)和特征方向的组合，这被称为**[谱分解](@entry_id:173707)** (Spectral Decomposition)：

$$
\mathbf{T} = \sum_{i=1}^{3} \lambda_i \mathbf{n}_i \otimes \mathbf{n}_i
$$

其中 $\lambda_i$ 是[特征值](@entry_id:154894)，$\mathbf{n}_i$ 是对应的单位[特征向量](@entry_id:151813)，$\{\mathbf{n}_1, \mathbf{n}_2, \mathbf{n}_3\}$ 构成一个标准正交基。这里的 $\mathbf{P}_i = \mathbf{n}_i \otimes \mathbf{n}_i$ 是一个秩为1的**投影算子**，它将任意矢量投影到由 $\mathbf{n}_i$ 张成的方向上。

例如，对于[应力张量](@entry_id:148973) $\boldsymbol{\sigma} = \begin{pmatrix} 5 & 2 & 0 \\ 2 & 1 & 0 \\ 0 & 0 & 3 \end{pmatrix}$，其主应力（[特征值](@entry_id:154894)）为 $\{3+2\sqrt{2}, 3-2\sqrt{2}, 3\}$，对应的[主方向](@entry_id:276187)（[特征向量](@entry_id:151813)）构成一个[标准正交基](@entry_id:147779)。因此，它可以被唯一地分解为三个主应力与其对应主方向投影的加权和 [@problem_id:2686494]。

### [特征值](@entry_id:154894)简并的情形

当两个或三个[特征值](@entry_id:154894)相等时，我们称之为**[特征值](@entry_id:154894)简并** (Degeneracy)。例如，对于一个绕 $\mathbf{n}_3$ 轴对称的应力状态，我们会有 $\lambda_1 = \lambda_2 \neq \lambda_3$。在这种情况下，与[重复特征值](@entry_id:154579) $\lambda_1$ 对应的[特征空间](@entry_id:638014)不再是一条直线，而是一个二维平面（称为**特征平面**）。该平面内的**任何**非零向量都是一个[特征值](@entry_id:154894)为 $\lambda_1$ 的[特征向量](@entry_id:151813) [@problem_id:2633191]。

这意味着我们无法唯一地确定两个独立的主方向，但[主平面](@entry_id:164488)本身是唯一的。[谱分解](@entry_id:173707)的表达形式也需要相应调整，以反映这种基于[子空间](@entry_id:150286)的结构。此时，分解应写成：

$$
\mathbf{T} = \lambda_1 \mathbf{P}_{12} + \lambda_3 \mathbf{P}_3
$$

其中 $\mathbf{P}_3 = \mathbf{n}_3 \otimes \mathbf{n}_3$ 是向简单[特征值](@entry_id:154894) $\lambda_3$ 的特征方向（$\mathbf{n}_3$）上投影的秩1投影算子，而 $\mathbf{P}_{12}$ 是向与 $\lambda_1$ 对应的二维特征平面上投影的**秩2投影算子**。这个秩2投影算子是唯一的，并且可以通过 $\mathbf{P}_{12} = \mathbf{I} - \mathbf{P}_3$ 得到。虽然我们可以在该平面内任意选择一组[标准正交基](@entry_id:147779) $\{\mathbf{e}_1, \mathbf{e}_2\}$，但它们的投影和 $\mathbf{e}_1 \otimes \mathbf{e}_1 + \mathbf{e}_2 \otimes \mathbf{e}_2$ 总是等于唯一的投影算子 $\mathbf{P}_{12}$。

这些投影算子本身可以完全由张量 $\mathbf{T}$ 及其[特征值](@entry_id:154894)确定，这进一步证明了谱分[解的唯一性](@entry_id:143619)和客观性。例如，上述的投影算子可以表示为 [@problem_id:2633191]：

$$
\mathbf{P}_3 = \frac{\mathbf{T} - \lambda_1 \mathbf{I}}{\lambda_3 - \lambda_1} \qquad \text{and} \qquad \mathbf{P}_{12} = \frac{\mathbf{T} - \lambda_3 \mathbf{I}}{\lambda_1 - \lambda_3}
$$

### 进阶应用与讨论

#### 张量函数

在[有限应变理论](@entry_id:176941)中，我们常常需要定义张量的函数，例如计算[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 的平方根以得到[右伸长张量](@entry_id:193756) $\mathbf{U} = \mathbf{C}^{1/2}$，或者计算[对数应变](@entry_id:751438) $\mathbf{E} = \frac{1}{2}\ln\mathbf{C}$。[谱分解](@entry_id:173707)为定义任意一个标量函数 $f$ 作用于[对称张量](@entry_id:148092) $\mathbf{T}$ 上提供了坚实的基础 [@problem_id:2633190]。

其思想是，首先对于多项式函数 $p(x)$，我们有 $p(\mathbf{T}) = \sum_{i=1}^3 p(\lambda_i) \mathbf{n}_i \otimes \mathbf{n}_i$。对于一般的[连续函数](@entry_id:137361) $f(x)$，根据[Weierstrass逼近定理](@entry_id:139729)，总能找到一个多项式序列 $p_k(x)$ 一致收敛于 $f(x)$。于是，张量函数 $f(\mathbf{T})$ 可以被定义为张量序列 $p_k(\mathbf{T})$ 的极限，其结果是：

$$
f(\mathbf{T}) = \sum_{i=1}^{3} f(\lambda_i) \mathbf{n}_i \otimes \mathbf{n}_i
$$

这个定义被称为**[谱映射定理](@entry_id:264489)** (Spectral Mapping Theorem)，它极为强大，因为它表明要计算 $f(\mathbf{T})$，我们只需将函数 $f$ 应用于其各个[特征值](@entry_id:154894)上，而保持[特征向量](@entry_id:151813)不变。这个方法只需要函数 $f$ 是连续的，而不需要更强的[解析性](@entry_id:140716)条件，这对于像开方这样在原点处非解析的函数至关重要。

#### [偏张量](@entry_id:185837)

另一个重要的应用是应力或[应变张量](@entry_id:193332)的分解。任何张量 $\mathbf{T}$ 都可以分解为一个球量[部分和](@entry_id:162077)一个偏量部分。**[偏张量](@entry_id:185837)** (Deviatoric Tensor) 定义为：

$$
\operatorname{dev}\mathbf{T} = \mathbf{T} - \frac{1}{3}(\operatorname{tr}\mathbf{T})\mathbf{I} = \mathbf{T} - \frac{1}{3}I_1\mathbf{I}
$$

偏[张量的迹](@entry_id:190669)恒为零。对于[对称张量](@entry_id:148092) $\mathbf{T}$，其[偏张量](@entry_id:185837) $\operatorname{dev}\mathbf{T}$ 具有与 $\mathbf{T}$ 完全相同的**[主方向](@entry_id:276187)**（[特征向量](@entry_id:151813)）。其[特征值](@entry_id:154894)（称为主偏应力或主[偏应变](@entry_id:201263)）则是原[特征值](@entry_id:154894)减去平均应力（静水压） [@problem_id:2633192]：

$$
\lambda_i^{\text{dev}} = \lambda_i - \frac{1}{3}I_1
$$

#### 特征系统的微扰

在许多物理问题中，张量会随某个参数（如时间或载荷）平滑演化，即 $\mathbf{T}(\varepsilon)$。一个自然的问题是，其[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)是否也随 $\varepsilon$ 平滑变化。当[特征值](@entry_id:154894)都是简单（非简并）的时，答案是肯定的。但当路径经过一个简并点时（例如 $\varepsilon=0$ 时 $\lambda_1(0) = \lambda_2(0)$），情况会变得非常微妙 [@problem_id:2633164]。

此时，单个[特征向量](@entry_id:151813)的路径可能不再是连续或可微的。例如，如果按大小顺序来追踪[特征向量](@entry_id:151813)，当 $\varepsilon$ 穿过0时，两个[特征值](@entry_id:154894)的大小关系互换，可能导致所追踪的[特征向量](@entry_id:151813)从一个方向突然跳到另一个正交的方向。然而，尽管单个[特征向量](@entry_id:151813)可能表现出不稳定的行为，但整个**特征[子空间](@entry_id:150286)**（及其对应的投影算子）通常仍然是平滑变化的。此外，通常可以找到一组随参数 $\varepsilon$ 平滑变化的[标准正交基](@entry_id:147779)来跨越该[子空间](@entry_id:150286)。这提醒我们在对特征系统进行[微分](@entry_id:158718)或进行数值追踪时必须格外小心。

### 超越对称性：非[对称张量](@entry_id:148092)与[奇异值分解](@entry_id:138057)

尽管[对称张量](@entry_id:148092)在[固体力学](@entry_id:164042)中占主导地位，但非对称张量也扮演着关键角色，其中最重要的例子是[速度梯度张量](@entry_id:270928) $\mathbf{L}$ 和变形梯度张量 $\mathbf{F}$。

对于非[对称张量](@entry_id:148092) $\mathbf{L}$，[特征值问题](@entry_id:142153)变得更加复杂 [@problem_id:2633185]：
- **左右[特征向量](@entry_id:151813)**：我们区分**右[特征向量](@entry_id:151813)** $\mathbf{r}$ ($\mathbf{L}\mathbf{r} = \lambda\mathbf{r}$) 和**左[特征向量](@entry_id:151813)** $\boldsymbol{\ell}$ ($\mathbf{L}^{\mathsf{T}}\boldsymbol{\ell} = \lambda\boldsymbol{\ell}$ 或等价地 $\boldsymbol{\ell}^{\mathsf{T}}\mathbf{L} = \lambda\boldsymbol{\ell}^{\mathsf{T}}$)。对于同一个[特征值](@entry_id:154894) $\lambda$，左右[特征向量](@entry_id:151813)通常指向不同方向。
- **复数[特征值](@entry_id:154894)**：非对称实张量的[特征值](@entry_id:154894)可能成对出现为复共轭数。
- **[非正交性](@entry_id:192553)**：最关键的区别在于，非对称张量的[特征向量](@entry_id:151813)通常**不是正交的**。只有当张量满足**正规条件** (Normality) $\mathbf{L}\mathbf{L}^{\mathsf{T}} = \mathbf{L}^{\mathsf{T}}\mathbf{L}$ 时，才保证存在一组标准正交的[特征向量](@entry_id:151813)。[对称张量](@entry_id:148092)是正规张量的一个特例。
- **[双正交性](@entry_id:746831)**：尽管右[特征向量](@entry_id:151813)集和左[特征向量](@entry_id:151813)集内部通常都不是正交的，但属于不同[特征值](@entry_id:154894)的右[特征向量](@entry_id:151813) $\mathbf{r}_i$ 和左[特征向量](@entry_id:151813) $\boldsymbol{\ell}_j$ 之间存在**双[正交关系](@entry_id:145540)**：$\boldsymbol{\ell}_j^{\mathsf{T}}\mathbf{r}_i = 0$ (当 $\lambda_i \neq \lambda_j$ 时)。

由于非对称张量的[特征向量](@entry_id:151813)缺乏良好的正交结构，且其[特征值](@entry_id:154894)可能是复数，直接对其进行[谱分解](@entry_id:173707)在物理和几何解释上存在困难。例如，变形梯度 $\mathbf{F}$ 的[特征值](@entry_id:154894)不是客观的，不能代表真实的材料拉伸 [@problem_id:2633175]。

因此，对于一般的非对称或矩形张量，一个更有力、更具物理意义的分解工具是**[奇异值分解](@entry_id:138057)** (Singular Value Decomposition, SVD)。任何一个实[二阶张量](@entry_id:199780) $\mathbf{F}$ 都可以分解为：

$$
\mathbf{F} = \mathbf{W}\boldsymbol{\Sigma}\mathbf{V}^{\mathsf{T}}
$$

其中：
- $\mathbf{W}$ 和 $\mathbf{V}$ 是**正交张量**。$\mathbf{W}$ 的列向量是[左奇异向量](@entry_id:751233)，$\mathbf{V}$ 的列向量是[右奇异向量](@entry_id:754365)。
- $\boldsymbol{\Sigma}$ 是一个[对角矩阵](@entry_id:637782)，其对角元 $\sigma_i \ge 0$ 称为**奇异值** (Singular Values)。

SVD在有限变形运动学中至关重要的原因在于 [@problem_id:2633175]：
1.  **普适性和稳健性**：SVD对任何张量都存在且唯一（在一定条件下）。
2.  **物理意义**：SVD与对称的柯西-格林[应变张量](@entry_id:193332)直接相关。可以证明，$\mathbf{F}$ 的[奇异值](@entry_id:152907) $\sigma_i$ 正是[右伸长张量](@entry_id:193756) $\mathbf{U}=\sqrt{\mathbf{F}^{\mathsf{T}}\mathbf{F}}$ 的[特征值](@entry_id:154894)，即**[主伸长](@entry_id:194664)** (Principal Stretches)。
3.  **几何解释**：[右奇异向量](@entry_id:754365)（$\mathbf{V}$ 的列）是[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$ 的[主方向](@entry_id:276187)，代表了参考构形中相互正交的材料纤维方向。[左奇异向量](@entry_id:751233)（$\mathbf{W}$ 的列）是[左柯西-格林张量](@entry_id:186163) $\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}}$ 的主方向，代表了这些材料纤维在当前构形中的最终指向，它们同样相互正交。
4.  **客观性**：由于[奇异值](@entry_id:152907)与客观张量 $\mathbf{C}$ 的谱相关，它们本身也是客观的物理量，完美地扮演了描述材料拉伸的角色。

总之，对于对称张量，谱分解提供了关于其[主值](@entry_id:189577)和[主方向](@entry_id:276187)的完整信息。对于非对称张量，尤其是运动学中的变形梯度，[奇异值分解](@entry_id:138057)（及其相关的极分解）是揭示其拉伸和转动内涵的正确且强大的工具。