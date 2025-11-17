## 引言
在[计算固体力学](@entry_id:169583)领域，对称[二阶张量](@entry_id:199780)是描述应力、应变等关键物理量的基石。要深刻理解材料在载荷下的力学行为，仅仅知道张量的分量是远远不够的；我们必须揭示其内在的几何与物理本质。谱分解理论正是实现这一目标的最强大工具，它能将一个复杂的张量状态分解为一组直观的物理量：主值（表示拉伸或压缩的强度）和[主方向](@entry_id:276187)（表示作用方向）。

然而，许多研究生虽然在线性代数中学习过[特征值问题](@entry_id:142153)，却难以将其与[连续介质力学](@entry_id:155125)中的复杂现象和高级数值计算的实际需求有效联系起来。如何运用[谱理论](@entry_id:275351)来分析有限变形、构建[各向异性本构模型](@entry_id:171281)，或是在[数值模拟](@entry_id:137087)中稳健地处理主值简并等问题，构成了从理论到实践的关键知识鸿沟。

本文旨在系统性地弥合这一鸿沟。我们将在“原理与机制”一章中，坚实地构建对称张量[谱分解](@entry_id:173707)的数学框架。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这一理论如何在变形[运动学](@entry_id:173318)、[本构模型](@entry_id:174726)开发、稳定性分析和计算方法中发挥核心作用。最后，通过“动手实践”中的具体问题，你将有机会亲手应用所学知识，将抽象理论转化为解决工程问题的能力。

## 原理与机制

本章旨在系统性地阐述对称张量的谱分解理论及其在[计算固体力学](@entry_id:169583)中的核心应用。我们将从[对称张量](@entry_id:148092)的基本性质出发，深入探讨谱定理的数学表述及其物理内涵，并最终将这些理论工具应用于连续介质力学中的关键问题，如应力张量分析、[本构模型](@entry_id:174726)构建和[数值算法](@entry_id:752770)的稳定性。

### [对称张量](@entry_id:148092)的基本性质

在[计算固体力学](@entry_id:169583)中，我们遇到的许多关键物理量，如[应力张量和应变张量](@entry_id:755512)，都由对称的二阶张量表示。对称性不是一个随意的数学假设，而是源于深刻的物理定律。理解对称性的后果是掌握其力学行为的第一步。

#### 对称性的定义与内涵

一个在三维欧几里得空间 $\mathbb{R}^3$ 中作用的[二阶张量](@entry_id:199780) $\boldsymbol{A}$，若在其任一标准正交基下的矩阵表示满足 $\boldsymbol{A} = \boldsymbol{A}^T$，则称其为**[对称张量](@entry_id:148092)**。此定义等价于一个不依赖于[坐标系](@entry_id:156346)的表述：对于任意向量 $\boldsymbol{x}, \boldsymbol{y} \in \mathbb{R}^3$，张量 $\boldsymbol{A}$ 满足[内积](@entry_id:158127)关系式：
$$
\langle \boldsymbol{A}\boldsymbol{x}, \boldsymbol{y} \rangle = \langle \boldsymbol{x}, \boldsymbol{A}\boldsymbol{y} \rangle
$$
这个性质在数学上被称为**自伴随性** (self-adjointness)。在[连续介质力学](@entry_id:155125)中，柯西应力张量 $\boldsymbol{\sigma}$ 的对称性是角动量守恒定律在无体力矩和面力偶情况下的直接推论 [@problem_id:3602004]。

#### [主值](@entry_id:189577)与主方向：特征值问题

[对称张量](@entry_id:148092)的核心力学特性通过其**主值** (principal values) 和**主方向** (principal directions) 来刻画。这些量在数学上对应于张量的**[特征值](@entry_id:154894)** (eigenvalues) 和**[特征向量](@entry_id:151813)** (eigenvectors)。[特征值问题](@entry_id:142153)表述为寻找一个非零向量 $\boldsymbol{n}$（[主方向](@entry_id:276187)）和一个标量 $\lambda$（[主值](@entry_id:189577)），使得张量 $\boldsymbol{A}$ 作用于 $\boldsymbol{n}$ 的结果是沿着 $\boldsymbol{n}$ 方向的纯粹拉伸或压缩：
$$
\boldsymbol{A}\boldsymbol{n} = \lambda\boldsymbol{n}
$$
从物理角度看，如果 $\boldsymbol{A}$ 是一个应力张量 $\boldsymbol{\sigma}$，$\boldsymbol{n}$ 代表一个微小面积元的法向，那么上式意味着作用在该面上的[面力矢量](@entry_id:189429) $\boldsymbol{t}(\boldsymbol{n}) = \boldsymbol{\sigma}\boldsymbol{n}$ 与法向 $\boldsymbol{n}$ 共线，即 $\boldsymbol{t}(\boldsymbol{n}) = \lambda\boldsymbol{n}$。这种情况下，该面上只有正应力，没有剪应力。这样的面被称为**[主平面](@entry_id:164488)** [@problem_id:3602004]。

#### [对称张量](@entry_id:148092)的谱特性：实[特征值](@entry_id:154894)与[正交特征向量](@entry_id:155522)

对称性（或自伴随性）赋予了张量两个至关重要的谱性质。

首先，**对称张量的[主值](@entry_id:189577)（[特征值](@entry_id:154894)）必为实数**。这一性质保证了[主应力](@entry_id:176761)、[主应变](@entry_id:197797)等物理量是可测量的实数。我们可以通过以下方式证明这一点。假设 $\lambda$ 是一个可能为复数的[特征值](@entry_id:154894)，$\boldsymbol{x}$ 是对应的（可能为[复向量](@entry_id:192851)的）[特征向量](@entry_id:151813)。我们考虑[复向量空间](@entry_id:264355)中的Hermitian[内积](@entry_id:158127) $\langle \boldsymbol{u}, \boldsymbol{v} \rangle = \boldsymbol{u}^H \boldsymbol{v}$。由于 $\boldsymbol{A}$ 是实[对称张量](@entry_id:148092)，它也是一个Hermitian算子（$\boldsymbol{A}^H = \boldsymbol{A}^T = \boldsymbol{A}$）。从 $\boldsymbol{A}\boldsymbol{x} = \lambda\boldsymbol{x}$ 出发，我们有：
$$
\lambda = \frac{\langle \boldsymbol{x}, \boldsymbol{A}\boldsymbol{x} \rangle}{\langle \boldsymbol{x}, \boldsymbol{x} \rangle}
$$
利用 $\boldsymbol{A}$ 的自伴随性，$\langle \boldsymbol{x}, \boldsymbol{A}\boldsymbol{x} \rangle = \langle \boldsymbol{A}\boldsymbol{x}, \boldsymbol{x} \rangle$。将 $\boldsymbol{A}\boldsymbol{x} = \lambda\boldsymbol{x}$ 和 $\langle \boldsymbol{A}\boldsymbol{x}, \boldsymbol{x} \rangle = \langle \lambda\boldsymbol{x}, \boldsymbol{x} \rangle = \bar{\lambda} \langle \boldsymbol{x}, \boldsymbol{x} \rangle$ 代入，我们得到：
$$
\lambda \langle \boldsymbol{x}, \boldsymbol{x} \rangle = \bar{\lambda} \langle \boldsymbol{x}, \boldsymbol{x} \rangle
$$
因为 $\boldsymbol{x}$ 是非[零向量](@entry_id:156189)，$\langle \boldsymbol{x}, \boldsymbol{x} \rangle \neq 0$，所以必然有 $\lambda = \bar{\lambda}$，这证明了 $\lambda$ 是实数 [@problem_id:3601964]。

其次，**对称张量对应于不同[主值](@entry_id:189577)的主方向（[特征向量](@entry_id:151813)）是相互正交的**。设 $\lambda_1$ 和 $\lambda_2$ 是两个不同的[主值](@entry_id:189577)，对应的[特征向量](@entry_id:151813)为 $\boldsymbol{n}_1$ 和 $\boldsymbol{n}_2$。我们考察量 $\langle \boldsymbol{A}\boldsymbol{n}_1, \boldsymbol{n}_2 \rangle$。一方面，$\langle \boldsymbol{A}\boldsymbol{n}_1, \boldsymbol{n}_2 \rangle = \langle \lambda_1\boldsymbol{n}_1, \boldsymbol{n}_2 \rangle = \lambda_1 \langle \boldsymbol{n}_1, \boldsymbol{n}_2 \rangle$。另一方面，利用自伴随性，$\langle \boldsymbol{A}\boldsymbol{n}_1, \boldsymbol{n}_2 \rangle = \langle \boldsymbol{n}_1, \boldsymbol{A}\boldsymbol{n}_2 \rangle = \langle \boldsymbol{n}_1, \lambda_2\boldsymbol{n}_2 \rangle = \lambda_2 \langle \boldsymbol{n}_1, \boldsymbol{n}_2 \rangle$。因此，我们有：
$$
(\lambda_1 - \lambda_2) \langle \boldsymbol{n}_1, \boldsymbol{n}_2 \rangle = 0
$$
由于 $\lambda_1 \neq \lambda_2$，必须有 $\langle \boldsymbol{n}_1, \boldsymbol{n}_2 \rangle = 0$，即 $\boldsymbol{n}_1$ 和 $\boldsymbol{n}_2$ 正交 [@problem_id:3601964] [@problem_id:3601957]。

需要强调的是，这些优良性质是一般非对称张量所不具备的。非对称张量可能拥有复数[特征值](@entry_id:154894)，其[特征向量](@entry_id:151813)也未必正交 [@problem_id:3601964]。

### 谱定理及其表述形式

上述关于实[特征值](@entry_id:154894)和[正交特征向量](@entry_id:155522)的性质，最终汇集成一个统一而强大的定理——谱定理。

#### 谱定理：[正交对角化](@entry_id:149411)

**谱定理** (Spectral Theorem) 指出：对于任意一个作用于 $\mathbb{R}^3$ 的实对称[二阶张量](@entry_id:199780) $\boldsymbol{A}$，必然存在一个由其[特征向量](@entry_id:151813)构成的标准正交基 $\{\boldsymbol{n}_1, \boldsymbol{n}_2, \boldsymbol{n}_3\}$。这意味着 $\boldsymbol{A}$ 是**可[正交对角化](@entry_id:149411)的** (orthogonally diagonalizable)。

在矩阵表示中，这等价于存在一个**正交矩阵** $\boldsymbol{Q}$（其列向量为标准正交的[特征向量](@entry_id:151813) $\boldsymbol{n}_i$，满足 $\boldsymbol{Q}^T\boldsymbol{Q}=\boldsymbol{I}$），和一个由对应实[特征值](@entry_id:154894)构成的对角矩阵 $\boldsymbol{D} = \mathrm{diag}(\lambda_1, \lambda_2, \lambda_3)$，使得：
$$
\boldsymbol{A} = \boldsymbol{Q}\boldsymbol{D}\boldsymbol{Q}^T \quad \text{或等价地} \quad \boldsymbol{D} = \boldsymbol{Q}^T\boldsymbol{A}\boldsymbol{Q}
$$
这个变换的几何意义是，通过一个刚性转动（或旋转加反射）$\boldsymbol{Q}$，我们可以将[坐标系](@entry_id:156346)从原始基变换到主方向基。在新[坐标系](@entry_id:156346)（主[坐标系](@entry_id:156346)）中，张量 $\boldsymbol{A}$ 的[矩阵表示](@entry_id:146025)是纯对角的，所有“剪切”分量都消失了。这极大地简化了张量的分析 [@problem_id:3601957]。

#### [谱分解](@entry_id:173707)：张量的内禀结构

[谱定理](@entry_id:136620)的另一种等价且更具内涵的表述形式是**[谱分解](@entry_id:173707)** (spectral decomposition)。它将张量 $\boldsymbol{A}$ 表示为其[主值](@entry_id:189577)和主方向[张量积](@entry_id:140694) (dyadic product) 的[线性组合](@entry_id:154743)：
$$
\boldsymbol{A} = \sum_{i=1}^{3} \lambda_i (\boldsymbol{n}_i \otimes \boldsymbol{n}_i)
$$
这种形式直观地揭示了张量的内在结构：张量 $\boldsymbol{A}$ 对任意向量的作用，可以分解为将该向量分别投影到三个相互正交的主方向上，然后按相应的[主值](@entry_id:189577)进行缩放，最后再将结果叠加起来 [@problem_id:3601964]。

#### 特征[投影算子](@entry_id:154142)

[谱分解](@entry_id:173707)中的每一项 $\boldsymbol{P}_i = \boldsymbol{n}_i \otimes \boldsymbol{n}_i$ 自身就是一个重要的线性算子，称为**特征[投影算子](@entry_id:154142)** (eigenprojection operator)。它将任意向量正交投影到由[主方向](@entry_id:276187) $\boldsymbol{n}_i$ 张成的一维[子空间](@entry_id:150286)上。这些[投影算子](@entry_id:154142)构成了一个完备的算[子集](@entry_id:261956)合，并具有以下代数性质 [@problem_id:3602013]：

1.  **[幂等性](@entry_id:190768) (Idempotency)**：对同一方向连续投影两次，结果不变。
    $$
    \boldsymbol{P}_i \boldsymbol{P}_i = \boldsymbol{P}_i^2 = \boldsymbol{P}_i
    $$
2.  **正交性 (Orthogonality)**：向一个主方向投影后，其在其他主方向上的分量为零。
    $$
    \boldsymbol{P}_i \boldsymbol{P}_j = \boldsymbol{0} \quad (\text{if } i \neq j)
    $$
    这两个性质可以合并写作 $\boldsymbol{P}_i \boldsymbol{P}_j = \delta_{ij} \boldsymbol{P}_i$，其中 $\delta_{ij}$ 是Kronecker delta。

3.  **完备性 (Completeness)**：所有[投影算子](@entry_id:154142)之和等于单位张量 $\boldsymbol{I}$，这意味着任意向量都可以被这组投影算子完全分解。
    $$
    \sum_{i=1}^{3} \boldsymbol{P}_i = \boldsymbol{I}
    $$

利用这些投影算子，谱分解可以简洁地写成 $\boldsymbol{A} = \sum_{i=1}^{3} \lambda_i \boldsymbol{P}_i$。

### 重复主值与简并特征[子空间](@entry_id:150286)

当张量的某些主值相等时，即出现**[重复特征值](@entry_id:154579)**（或[简并特征值](@entry_id:187316)），其谱结构会展现出新的特性，这在物理上通常与对称性或各向同性有关。

#### [代数重数与几何重数](@entry_id:151502)

一个[特征值](@entry_id:154894) $\lambda$ 作为[特征多项式](@entry_id:150909)根的次数被称为其**[代数重数](@entry_id:154240)**。该[特征值](@entry_id:154894)对应的[线性无关](@entry_id:148207)[特征向量](@entry_id:151813)所张成的[子空间](@entry_id:150286)（即特征[子空间](@entry_id:150286) $E_\lambda$）的维度，被称为其**[几何重数](@entry_id:155584)**。对于一般张量，[几何重数](@entry_id:155584)可能小于[代数重数](@entry_id:154240)。然而，[对称张量](@entry_id:148092)的一个关键优点是，**其任意[特征值](@entry_id:154894)的[几何重数](@entry_id:155584)恒等于[代数重数](@entry_id:154240)**。这意味着特征[子空间](@entry_id:150286)足够“大”，总能找到足够多的线性无关[特征向量](@entry_id:151813)来张成整个空间，从而保证了[可对角化性](@entry_id:748379) [@problem_id:3601948]。

#### [主方向](@entry_id:276187)的非唯一性

如果一个主值 $\lambda_k$ 是非重复的（[代数重数](@entry_id:154240)为1），其对应的特征[子空间](@entry_id:150286)是一维的（一条直线），因此其主方向 $\boldsymbol{n}_k$ 是唯一的（不计符号和长度归一化）。

然而，如果一个[主值](@entry_id:189577)是重复的，例如 $\lambda_1 = \lambda_2 \neq \lambda_3$，那么对应于 $\lambda_1$ 的特征[子空间](@entry_id:150286) $E_{\lambda_1}$ 的维度将是2（一个平面）。这个平面与 $\lambda_3$ 的主方向 $\boldsymbol{n}_3$ 相互正交。此时，**任何位于该平面内的非零向量都是 $\boldsymbol{A}$ 对应于主值 $\lambda_1$ 的一个有效[主方向](@entry_id:276187)**。因此，[主方向](@entry_id:276187)不再唯一。我们可以从这个二维特征[子空间](@entry_id:150286)中任意选取一组标准正交基 $\{\boldsymbol{n}_1, \boldsymbol{n}_2\}$ 作为[主方向](@entry_id:276187)基底。这个选择的任意性是理解横观[各向同性材料](@entry_id:170678)行为的关键 [@problem_id:3602002]。

作为一个具体的例子，考虑张量 $\boldsymbol{A} = 2\boldsymbol{I} + 3\boldsymbol{u}\otimes\boldsymbol{u}$，其中 $\boldsymbol{u}$ 是一个[单位向量](@entry_id:165907)。
*   对于方向 $\boldsymbol{u}$，我们有 $\boldsymbol{A}\boldsymbol{u} = 2\boldsymbol{I}\boldsymbol{u} + 3(\boldsymbol{u}\otimes\boldsymbol{u})\boldsymbol{u} = 2\boldsymbol{u} + 3\boldsymbol{u}(\boldsymbol{u}\cdot\boldsymbol{u}) = 5\boldsymbol{u}$。因此，$\lambda_1=5$ 是一个主值，$\boldsymbol{u}$ 是对应的主方向。
*   对于任何与 $\boldsymbol{u}$ 正交的向量 $\boldsymbol{v}$（即 $\boldsymbol{u}\cdot\boldsymbol{v}=0$），我们有 $\boldsymbol{A}\boldsymbol{v} = 2\boldsymbol{I}\boldsymbol{v} + 3(\boldsymbol{u}\otimes\boldsymbol{u})\boldsymbol{v} = 2\boldsymbol{v} + 3\boldsymbol{u}(\boldsymbol{u}\cdot\boldsymbol{v}) = 2\boldsymbol{v}$。因此，$\lambda_2=2$ 是一个主值，所有与 $\boldsymbol{u}$ 正交的向量都是其主方向。
这个例子表明，主值 $\lambda=2$ 具有一个二维的特征[子空间](@entry_id:150286)（即垂直于 $\boldsymbol{u}$ 的平面），其[代数重数与几何重数](@entry_id:151502)均为2 [@problem_id:3601948]。

#### 物理上的各向同性

*   **横观各向同性 (Transverse Isotropy)**：当两个[主值](@entry_id:189577)相等时（$\lambda_1 = \lambda_2 \neq \lambda_3$），张量所描述的物理性质在一个平面（由 $\boldsymbol{n}_1, \boldsymbol{n}_2$ 张成的平面）内是各向同性的，但在垂直于该平面的方向（$\boldsymbol{n}_3$ 方向）则表现不同。这种状态对应于材料在一个方向上具有独特的纤维或层状结构 [@problem_id:3602002]。

*   **完全各向同性 (Full Isotropy) / 球张量**：当三个[主值](@entry_id:189577)全部相等时（$\lambda_1 = \lambda_2 = \lambda_3 = p$），张量在所有方向上都表现出相同的性质。此时，任何向量都是[特征向量](@entry_id:151813)，张量必定是单位张量的标量倍，即 $\boldsymbol{A} = p\boldsymbol{I}$。这种状态在[应力分析](@entry_id:168804)中被称为**静水压应力状态** (hydrostatic stress state) [@problem_id:3602004]。

### 在[连续介质力学](@entry_id:155125)中的应用与进阶概念

[谱理论](@entry_id:275351)为分析和[计算固体力学](@entry_id:169583)中的张量问题提供了强大的数学框架。

#### 柯西应力[张量的对称性](@entry_id:202126)

在经典[连续介质力学](@entry_id:155125)中，若不存在体力矩密度和面力偶密度，则角动量守恒定律的局部形式要求柯西应力张量 $\boldsymbol{\sigma}$ 必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$。这个结果（有时被称为柯西第二运动定律）保证了[应力张量](@entry_id:148973)拥有谱定理的所有良好性质，是进行主[应力分析](@entry_id:168804)的物理基础 [@problem_id:3602004]。

#### [张量不变量](@entry_id:203254)与特征方程

对于一个二阶张量 $\boldsymbol{A}$，其**[主不变量](@entry_id:193522)** (principal invariants) $I_1, I_2, I_3$ 是不随[坐标系](@entry_id:156346)旋转而改变的标量。它们可以通过张量本身的运算直接计算：
$$
I_1(\boldsymbol{A}) = \mathrm{tr}(\boldsymbol{A})
$$
$$
I_2(\boldsymbol{A}) = \frac{1}{2} \left[ (\mathrm{tr}(\boldsymbol{A}))^2 - \mathrm{tr}(\boldsymbol{A}^2) \right]
$$
$$
I_3(\boldsymbol{A}) = \det(\boldsymbol{A})
$$
这些[不变量](@entry_id:148850)与张量的[主值](@entry_id:189577)（[特征值](@entry_id:154894)）之间有着直接的联系，它们是[主值](@entry_id:189577)的[基本对称多项式](@entry_id:152224)：
$$
I_1 = \lambda_1 + \lambda_2 + \lambda_3
$$
$$
I_2 = \lambda_1\lambda_2 + \lambda_2\lambda_3 + \lambda_3\lambda_1
$$
$$
I_3 = \lambda_1\lambda_2\lambda_3
$$
[不变量](@entry_id:148850)在构建不依赖于观察者[坐标系](@entry_id:156346)的材料本构关系（例如，[屈服准则](@entry_id:193897)和[应变能函数](@entry_id:178435)）时至关重要。此外，它们也是张量特征多项式 $p_{\boldsymbol{A}}(\lambda) = \det(\boldsymbol{A} - \lambda\boldsymbol{I})$ 的系数：
$$
p_{\boldsymbol{A}}(\lambda) = -\lambda^3 + I_1\lambda^2 - I_2\lambda + I_3
$$
特征方程 $p_{\boldsymbol{A}}(\lambda)=0$ 的根就是张量的主值 [@problem_id:3602021]。

#### Cayley-Hamilton 定理

**Cayley-Hamilton 定理**指出，任何一个方阵（或二阶张量）都满足其自身的[特征方程](@entry_id:265849)。对于三维空间中的二阶张量 $\boldsymbol{A}$，这意味着：
$$
-\boldsymbol{A}^3 + I_1\boldsymbol{A}^2 - I_2\boldsymbol{A} + I_3\boldsymbol{I} = \boldsymbol{0}
$$
这个强大的定理提供了一个递归关系，允许我们将任何高于二次的张量幂 $\boldsymbol{A}^k$ ($k \ge 3$) 表示为一个关于 $\boldsymbol{A}$ 的最高为二次的多项式。例如，$\boldsymbol{A}^3 = I_1\boldsymbol{A}^2 - I_2\boldsymbol{A} + I_3\boldsymbol{I}$。这个性质在解析和数值计算中极为有用，例如，在计算张量[指数函数](@entry_id:161417) $\exp(\boldsymbol{A})$ 等复杂张量函数时，它可以将无穷级数简化为有限项 [@problem_id:3601984]。

#### 球张量与偏[张量分解](@entry_id:173366)

在塑性力学和流变学中，将应力或[应变张量分解](@entry_id:184653)为其**球量** (spherical part) 和**偏量** (deviatoric part) 部分是一种常见的做法。对于应力张量 $\boldsymbol{\sigma}$，其分解形式为：
$$
\boldsymbol{\sigma} = \boldsymbol{s} + p\boldsymbol{I}
$$
其中 $p = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})$ 是[平均应力](@entry_id:751819)或静水压力，它代表了引起体积变化的应力部分。$\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}$ 是**应力[偏张量](@entry_id:185837)**，其迹为零 ($\mathrm{tr}(\boldsymbol{s}) = 0$)，它代表了引起形状改变（剪切变形）的应力部分。

这个分解对谱分析有着简洁的影响。由于我们只是从原张量中减去一个球张量 $p\boldsymbol{I}$，其主方向保持不变。设 $\boldsymbol{n}_i$ 是 $\boldsymbol{\sigma}$ 的主方向，则：
$$
\boldsymbol{s}\boldsymbol{n}_i = (\boldsymbol{\sigma} - p\boldsymbol{I})\boldsymbol{n}_i = \boldsymbol{\sigma}\boldsymbol{n}_i - p\boldsymbol{n}_i = \sigma_i\boldsymbol{n}_i - p\boldsymbol{n}_i = (\sigma_i - p)\boldsymbol{n}_i
$$
这表明，$\boldsymbol{s}$ 和 $\boldsymbol{\sigma}$ 共享相同的[主方向](@entry_id:276187)。而应力偏量的主值 $s_i$ 与原应力[主值](@entry_id:189577) $\sigma_i$ 的关系为 $s_i = \sigma_i - p$。因此，[主应力](@entry_id:176761)差 $(\sigma_i - \sigma_j)$ 等于[偏应力](@entry_id:163323)主值之差 $(s_i - s_j)$，这解释了为什么许多屈服准则（如von Mises和Tresca）可以用偏[应力[不变](@entry_id:170526)量](@entry_id:148850)来表述 [@problem_id:3601976]。

#### 谱演化与[微分性质](@entry_id:275298)

在模拟加载过程时，我们经常处理一个随时间（或某个加载参数 $t$）平滑变化的张量族 $\boldsymbol{\sigma}(t)$。一个关键的计算问题是如何高效且准确地追踪其谱（[主值](@entry_id:189577)和主方向）的演化。

虽然主值作为[特征多项式的根](@entry_id:270910)，在远离重复点时是 $t$ 的平滑函数，但[主方向](@entry_id:276187)（[特征向量](@entry_id:151813)）的行为要复杂得多。当路径通过一个具有重复主值的点时，尽管理论上存在平滑演化的[特征向量基](@entry_id:163721)，但任意选择的、在每个时刻都由标准数值库计算出的[特征向量基](@entry_id:163721)，在经过该点时通常是**不可微的**。这种不连续性会对依赖主方向导数的算法（如[客观应力率](@entry_id:199282)的计算）造成严重问题。

一个更稳健的替代方案是转而分析**[谱投影算子](@entry_id:755184)** $\boldsymbol{P}_S(t)$ 的演化。只要一个[特征值](@entry_id:154894)簇（例如，在 $t=0$ 时重复的[特征值](@entry_id:154894)）与其余的谱保持分离，那么投影到该簇对应的不变子空间 $S(t)$ 的算子 $\boldsymbol{P}_S(t)$ 就是 $t$ 的一个平滑函数。它的导数 $\dot{\boldsymbol{P}}_S(0)$ 可以通过求解一个良定的 Sylvester 型方程来唯一确定。因此，在现代[计算力学](@entry_id:174464)中，直接对[谱投影算子](@entry_id:755184)进行操作，而不是试[图追踪](@entry_id:263851)不稳定的单个[特征向量](@entry_id:151813)，已成为处理[重复特征值](@entry_id:154579)问题的标准[范式](@entry_id:161181) [@problem_id:3601995]。