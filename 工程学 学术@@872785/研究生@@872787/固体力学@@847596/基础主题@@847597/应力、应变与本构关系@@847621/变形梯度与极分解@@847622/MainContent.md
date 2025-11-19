## 引言
在现代[固体力学](@entry_id:164042)中，精确描述物体在受力后如何发生[大变形](@entry_id:167243)是理解材料行为和结构响应的基石。当变形不再微小时，线性理论失效，我们需要一个更普适的数学框架来捕捉拉伸、剪切和旋转等复杂的运动学现象。变形梯度张量 (Deformation Gradient Tensor) 和其极分解 (Polar Decomposition) 正是这一框架的核心，它们提供了一种将局部变形与刚体旋转进行精确分离的强大工具，构成了从理论分析到[数值模拟](@entry_id:137087)的桥梁。

然而，对于初学者而言，这些概念往往显得抽象，其深刻的物理意义和在不同领域中的关键作用也容易被忽视。本文旨在弥合这一知识鸿沟，系统地、深入浅出地介绍变形梯度与极分解。读者将通过本文学习到：

- **第一章：原理与机制** 将从最基本的定义出发，阐明变形梯度如何量化局部变形，并详细推导极分解定理。本章将揭示[拉伸张量](@entry_id:193200)与[旋转张量](@entry_id:191990)的几何与物理内涵，并解释它们如何成为构建客观本构理论的数学基础。
- **第二章：应用与跨学科连接** 将展示这一理论框架的强大应用价值。我们将探讨它如何连接有限应变与微小应变理论，如何在[超弹性](@entry_id:159356)、[晶体塑性](@entry_id:141273)、材料[相变](@entry_id:147324)等固体力学和[材料科学](@entry_id:152226)的前沿领域中扮演关键角色，并简述其在[计算力学](@entry_id:174464)中的重要性。
- **第三章：动手实践** 将理论付诸实践。通过一系列精心设计的计算练习，读者将逐步掌握从基本计算到使用高级数值方法（如SVD）实现极分解的技能，从而将抽象的理论转化为解决实际问题的能力。

通过这三个章节的学习，本文将带领读者建立对有限变形[运动学](@entry_id:173318)的坚实理解，为进一步深入研究[非线性](@entry_id:637147)[连续介质力学](@entry_id:155125)、[材料科学](@entry_id:152226)和计算力学等领域奠定基础。让我们首先从变形的数学描述开始，进入第一章“原理与机制”。

## 原理与机制

在深入探讨连续介质力学的[本构关系](@entry_id:186508)和[运动学](@entry_id:173318)之前，必须对变形的局部描述建立一个坚实而精确的数学框架。本章旨在阐述描述有限变形的核心工具——变形梯度张量，并详细解析其最重要的数学结构——极分解。我们将从基本定义出发，逐步揭示这些概念的深刻几何意义、物理内涵及其在建立客观本构理论中的关键作用。

### 变形梯度张量

#### 定义与几何意义

连续体的运动将参考构型 $\mathcal{B}_0$ 中的物质点 $\mathbf{X}$ 映射到当前构型 $\mathcal{B}_t$ 中的空间点 $\mathbf{x}$，这一映射关系由运动函数 $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$ 描述。为了量化物质点邻域内的局部变形，我们引入**变形梯度张量 (deformation gradient tensor)** $\mathbf{F}$。它被定义为运动函数 $\boldsymbol{\chi}$ 对参考坐标 $\mathbf{X}$ 的梯度：

$$
\mathbf{F} = \frac{\partial \boldsymbol{\chi}(\mathbf{X})}{\partial \mathbf{X}} \equiv \nabla_{\mathbf{X}} \boldsymbol{\chi}
$$

在[笛卡尔坐标系](@entry_id:169789)中，$\mathbf{F}$ 的分量形式为 $F_{iJ} = \frac{\partial x_i}{\partial X_J}$，其中 $i$ 对应当前构型的坐标分量，$J$ 对应参考构型的坐标分量。因此，$\mathbf{F}$ 是一个**两点张量 (two-point tensor)**，因为它将参考构型中的矢量与当前构型中的矢量联系起来。

变形梯度的核心几何意义在于，它为[非线性](@entry_id:637147)的变形映射提供了一个局部的线性近似。考虑参考构型中从物质点 $\mathbf{X}$ 出发的一个无限小物质[线元](@entry_id:196833) $d\mathbf{X}$。经过变形后，它在当前构型中变为[线元](@entry_id:196833) $d\mathbf{x}$。这两者之间的关系恰好由变形梯度张量给出 [@problem_id:2695202]：

$$
d\mathbf{x} = \mathbf{F} \, d\mathbf{X}
$$

这个关系表明，$\mathbf{F}$ 是一个线性映射，它将物[质点](@entry_id:186768) $\mathbf{X}$ 邻域内的所有物质[线元](@entry_id:196833)从参考构型的[切空间](@entry_id:199137) $T_{\mathbf{X}}\mathcal{B}_0$ 映射到当前构型的[切空间](@entry_id:199137) $T_{\mathbf{x}}\mathcal{B}_t$。从[微分几何](@entry_id:145818)的角度看，$\mathbf{F}$ 就是变形映射 $\boldsymbol{\chi}$ 在点 $\mathbf{X}$ 处的**切映射 (tangent map)** $T_{\mathbf{X}}\boldsymbol{\chi}$ [@problem_id:2695244]。具体而言，若有一条光滑曲线 $\mathbf{X}(s)$ 穿过点 $\mathbf{X}$（即 $\mathbf{X}(0) = \mathbf{X}$），其在 $s=0$ 处的切矢量为 $\dot{\mathbf{X}}(0) = \mathbf{A}$，则变形后的曲线 $\mathbf{x}(s) = \boldsymbol{\chi}(\mathbf{X}(s))$ 在 $s=0$ 处的切矢量为 $\frac{d}{ds}\boldsymbol{\chi}(\mathbf{X}(s))|_{s=0} = \mathbf{F}(\mathbf{X})\mathbf{A}$ [@problem_id:2695244]。

举一个具体的例子，考虑如下运动 [@problem_id:2695202]：
$$
x_1 = X_1 + a X_2 + \frac{1}{2} b X_1^2, \quad x_2 = X_2 + c X_1, \quad x_3 = (1 + d X_1) X_3
$$
其中 $a, b, c, d$ 为常数。通过对各分量求偏导，我们可以得到变形梯度张量的矩阵表示：
$$
[\mathbf{F}(\mathbf{X})] = \begin{pmatrix} 1 + b X_1  a  0 \\ c  1  0 \\ d X_3  0  1 + d X_1 \end{pmatrix}
$$
在特定的物[质点](@entry_id:186768)，例如 $\mathbf{X}^{\star}=(0, 0, L)$，代入后得到 $\mathbf{F}(\mathbf{X}^{\star})$ 的具体值。这个矩阵捕获了该点邻域内变形的所有信息，包括拉伸、剪切和旋转。

#### 体积、面积和方向的变换

变形梯度不仅描述了线元的变换，还决定了[体积元](@entry_id:267802)、面积元和方向的改变。这与其[行列式](@entry_id:142978)密切相关，该[行列式](@entry_id:142978)被称为**雅可比行列式 (Jacobian determinant)**，记为 $J$。

$$
J = \det(\mathbf{F})
$$

$J$ 的物理意义至关重要：它代表了局部的体积变化率 [@problem_id:2695206]。一个在参考构型中体积为 $dV$ 的无限小物质单元，在变形后其体积 $dv$ 为：

$$
dv = J \, dV
$$

这个关系源于[行列式的几何意义](@entry_id:200059)，即它度量了线性变换对体积的缩放效应。基于物理上的考量，物质不能被压缩至零体积或“翻转”过来，这意味着一个正的[体积元](@entry_id:267802)必须始终保持为正体积。因此，对于任何物理上可能的变形，必须满足**方向保持条件 (orientation-preserving condition)**：

$$
J  0
$$

另一方面，从数学角度看，根据[反函数定理](@entry_id:275014)，变形映射 $\boldsymbol{\chi}$ 在点 $\mathbf{X}$ 处局部可逆的充分必要条件是其[雅可比矩阵](@entry_id:264467)（即 $\mathbf{F}$）可逆。这等价于**[局部可逆性](@entry_id:143266)条件 (local invertibility condition)** [@problem_id:2695206]：

$$
J \neq 0
$$

显然，$J  0$ 是一个比 $J \neq 0$ 更强的条件。在[连续介质力学](@entry_id:155125)中，我们通常只考虑满足 $J0$ 的变形。

体积不发生变化的变形称为**不可压缩变形 (incompressible deformation)** 或**[等容变形](@entry_id:196451) (isochoric deformation)**。对于这类变形，[运动学](@entry_id:173318)约束条件为 $J=1$ [@problem_id:2695206]。如果一种材料是可压缩的，那么 $J$ 的值可以大于1（局部膨胀）、小于1（局部压缩）或等于1。对于二维问题， $J$ 则代表了局部面积的变化率 [@problem_id:2695206]。

#### 存在的[正则性条件](@entry_id:166962)

变形梯度的存在性和连续性取决于运动函数 $\boldsymbol{\chi}$ 的光滑程度或**正则性 (regularity)**。仅有连续性是不足以保证 $\mathbf{F}$ 存在的 [@problem_id:2695244]。

最简单的情形是，如果运动 $\boldsymbol{\chi}$ 在其定义域的[闭包](@entry_id:148169) $\overline{\Omega}$ 上是**一阶连续可微的**（记为 $\boldsymbol{\chi} \in C^1(\overline{\Omega})$），那么变形梯度 $\mathbf{F}$ 在每一点都存在且在 $\overline{\Omega}$ 上连续 [@problem_id:2695244]。这是经典连续介质力学中通常做的隐式假设。

在更广泛的数学框架中，可以考虑更弱的条件。例如，如果 $\boldsymbol{\chi}$ 是**[利普希茨连续的](@entry_id:267396) (Lipschitz continuous)**，根据Rademacher定理，$\mathbf{F}$ 将在 $\Omega$ 内**几乎处处 (almost everywhere)** 存在（在勒贝格测度意义下），并且其范数有界，即 $\mathbf{F} \in L^{\infty}(\Omega)$。然而，$\mathbf{F}$ 不必是连续的 [@problem_id:2695244]。在更现代的[非线性弹性](@entry_id:185743)理论中，通常在索博列夫空间 (Sobolev spaces) 的框架下研究变形，例如 $\boldsymbol{\chi} \in W^{1,p}(\Omega)$。这些更深入的数学结果对于理解塑性、断裂和接触等非光滑现象至关重要 [@problem_id:2695244]。

### 极分解

变形梯度 $\mathbf{F}$ 将一个纯粹的几何操作（旋转）和一个纯粹的变形操作（拉伸与剪切）耦合在一起。**极分解定理 (Polar Decomposition Theorem)** 提供了一种将这两种效应精确分离的优雅方法。

#### 定理与几何直观

该定理指出，任何满足 $J = \det(\mathbf{F})  0$ 的变形梯度张量 $\mathbf{F}$，都可以被唯一地分解为一个旋转和一个纯拉伸的乘积。具体来说，存在两种形式的分解：

1.  **右极分解 (Right Polar Decomposition)**: $\mathbf{F} = \mathbf{R}\mathbf{U}$
2.  **左极分解 (Left Polar Decomposition)**: $\mathbf{F} = \mathbf{V}\mathbf{R}$

在这里：
- $\mathbf{R}$ 是一个**[旋转张量](@entry_id:191990) (rotation tensor)**，它是一个**真正交张量 (proper orthogonal tensor)**，满足 $\mathbf{R}^{\mathsf{T}}\mathbf{R}=\mathbf{I}$ 和 $\det(\mathbf{R})=1$。它属于[特殊正交群](@entry_id:146418) $\mathrm{SO}(3)$。
- $\mathbf{U}$ 是**右[拉伸张量](@entry_id:193200) (right stretch tensor)**，它是一个**对称正定 (symmetric positive-definite, SPD)** 张量。
- $\mathbf{V}$ 是**左[拉伸张量](@entry_id:193200) (left stretch tensor)**，它也是一个对称正定张量。

对于一个给定的 $\mathbf{F}$，张量 $\mathbf{R}$, $\mathbf{U}$, $\mathbf{V}$ 都是唯一确定的 [@problem_id:2695202, @problem_id:2695204]。

右极分解的几何图像是：一个物质邻域首先经历由 $\mathbf{U}$ 描述的纯拉伸和剪切（变形），然后整体经历由 $\mathbf{R}$ 描述的刚体旋转。左极分解则对应于先旋转后变形。重要的是，两种分解中的[旋转张量](@entry_id:191990) $\mathbf{R}$ 是同一个。

需要注意的是，$\mathbf{R}$ 一般不等于 $\mathbf{F}$ 的反对称部分 $\frac{1}{2}(\mathbf{F}-\mathbf{F}^{\mathsf{T}})$。后者是小应变理论中[无穷小旋转](@entry_id:166635)的近似，对于有限变形是不成立的 [@problem_id:2695202]。

#### 应变张量与[拉伸张量](@entry_id:193200)

[拉伸张量](@entry_id:193200) $\mathbf{U}$ 和 $\mathbf{V}$ 与另外两个重要的[应变度量](@entry_id:755495)——柯西-格林张量 (Cauchy-Green tensors) 密切相关。

**右柯西-格林变形张量 (right Cauchy-Green deformation tensor)** $\mathbf{C}$ 定义为：

$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}
$$

**左柯西-格林变形张量 (left Cauchy-Green deformation tensor)** $\mathbf{B}$（也称Finger张量）定义为：

$$
\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}}
$$

将极分解式 $\mathbf{F} = \mathbf{R}\mathbf{U}$ 代入 $\mathbf{C}$ 的定义，我们得到 $\mathbf{C} = (\mathbf{R}\mathbf{U})^{\mathsf{T}}(\mathbf{R}\mathbf{U}) = \mathbf{U}^{\mathsf{T}}\mathbf{R}^{\mathsf{T}}\mathbf{R}\mathbf{U}$。由于 $\mathbf{R}$ 是正交的且 $\mathbf{U}$ 是对称的，这简化为 $\mathbf{C} = \mathbf{U}^2$。类似地，可以得到 $\mathbf{B} = \mathbf{V}^2$。

因此，右[拉伸张量](@entry_id:193200) $\mathbf{U}$ 是[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 的唯一[对称正定](@entry_id:145886)平方根，即 $\mathbf{U} = \sqrt{\mathbf{C}}$。同理，$\mathbf{V} = \sqrt{\mathbf{B}}$。这提供了一条从 $\mathbf{F}$ 计算 $\mathbf{U}$ 和 $\mathbf{V}$ 的明确路径。

由于 $\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}} = (\mathbf{R}\mathbf{U})(\mathbf{R}\mathbf{U})^{\mathsf{T}} = \mathbf{R}\mathbf{U}^2\mathbf{R}^{\mathsf{T}} = \mathbf{R}\mathbf{C}\mathbf{R}^{\mathsf{T}}$，我们得到了左[右柯西-格林张量](@entry_id:174156)之间的一个重要关系 [@problem_id:1537026]。这个关系表明 $\mathbf{B}$ 和 $\mathbf{C}$ 是相似的，因此它们具有相同的[特征值](@entry_id:154894)和[不变量](@entry_id:148850)。

$\mathbf{U}$ 和 $\mathbf{V}$ 的[特征值](@entry_id:154894)是相同的，记为 $\lambda_1, \lambda_2, \lambda_3$，被称为**[主伸长](@entry_id:194664) (principal stretches)**。它们量化了三个相互正交方向上的拉伸程度。$\mathbf{U}$ 的特征矢量 $\mathbf{N}_i$ 定义了参考构型中的**主拉伸方向 (principal directions of stretch)**，而 $\mathbf{V}$ 的特征矢量 $\mathbf{n}_i$ 定义了当前构型中的主拉伸方向。

利用极分解，雅可比行列式 $J$ 可以表达为[主伸长](@entry_id:194664)的乘积。因为 $J = \det(\mathbf{F}) = \det(\mathbf{R}\mathbf{U}) = \det(\mathbf{R})\det(\mathbf{U})$，且对于 $J0$ 的情况 $\det(\mathbf{R})=1$，我们有 [@problem_id:2695206]：

$$
J = \det(\mathbf{U}) = \lambda_1 \lambda_2 \lambda_3
$$

#### [旋转张量](@entry_id:191990)的几何意义

一旦确定了右[拉伸张量](@entry_id:193200) $\mathbf{U}$（通过计算 $\mathbf{C}$ 并开方），[旋转张量](@entry_id:191990) $\mathbf{R}$ 就可以通过 $\mathbf{R} = \mathbf{F}\mathbf{U}^{-1}$ 唯一确定。这个代数关系背后有着深刻的几何内涵。

可以证明，[旋转张量](@entry_id:191990) $\mathbf{R}$ 正是那个将右[拉伸张量](@entry_id:193200) $\mathbf{U}$ 的[主方向](@entry_id:276187) $\mathbf{N}_i$ 旋转到左[拉伸张量](@entry_id:193200) $\mathbf{V}$ 的[主方向](@entry_id:276187) $\mathbf{n}_i$ 的张量 [@problem_id:2695188]：

$$
\mathbf{n}_i = \mathbf{R}\mathbf{N}_i
$$

这个关系构成了对旋转 $\mathbf{R}$ 最直观的理解：它连接了变形前后的主[拉伸坐标](@entry_id:269878)系。此外，$\mathbf{R}$ 也是在所有旋转中与 $\mathbf{F}$ “最接近”的那个，即 $\mathbf{R}$ 是以下最小化问题的唯一解 [@problem_id:2695188]：
$$
\min_{\mathbf{Q}\in\mathrm{SO}(3)} \|\mathbf{F}-\mathbf{Q}\|_F
$$
其中 $\|\cdot\|_F$ 是[弗罗贝尼乌斯范数](@entry_id:143384) (Frobenius norm)。这为 $\mathbf{R}$ 提供了变分和最优近似的解释。

从计算角度看，极分解与**奇异值分解 (Singular Value Decomposition, SVD)** 密切相关。若 $\mathbf{F}$ 的SVD为 $\mathbf{F} = \mathbf{W}\mathbf{\Sigma}\mathbf{V}_{\text{svd}}^{\mathsf{T}}$，其中 $\mathbf{W}, \mathbf{V}_{\text{svd}} \in \mathrm{SO}(3)$，$\mathbf{\Sigma}$ 是包含[奇异值](@entry_id:152907)（即[主伸长](@entry_id:194664) $\lambda_i$）的[对角矩阵](@entry_id:637782)，则极分解的各个部分可以被直接构造出来 [@problem_id:2695211]：

$$
\mathbf{U} = \mathbf{V}_{\text{svd}} \mathbf{\Sigma} \mathbf{V}_{\text{svd}}^{\mathsf{T}}, \quad \mathbf{V} = \mathbf{W} \mathbf{\Sigma} \mathbf{W}^{\mathsf{T}}, \quad \mathbf{R} = \mathbf{W}\mathbf{V}_{\text{svd}}^{\mathsf{T}}
$$

#### 唯一性与奇异情况

极分[解的唯一性](@entry_id:143619)取决于变形梯度 $\mathbf{F}$ 的性质 [@problem_id:2695204]。

- **情形 1：$\mathbf{F}$ 可逆且 $\det(\mathbf{F})  0$**
这是物理上最常见的情况。如前所述，存在唯一的分解 $\mathbf{F} = \mathbf{R}\mathbf{U}$，其中 $\mathbf{R} \in \mathrm{SO}(3)$ 且 $\mathbf{U}$ 是[对称正定](@entry_id:145886)的 (SPD)。$\mathbf{U}$ 作为 $\mathbf{F}^{\mathsf{T}}\mathbf{F}$ 的唯一SPD平方根是唯一的，而 $\mathbf{R} = \mathbf{F}\mathbf{U}^{-1}$ 也因此是唯一的。即使 $\mathbf{U}$ 有重根（即某些[主伸长](@entry_id:194664)相等），$\mathbf{R}$ 和 $\mathbf{U}$ 本身仍然是唯一的 [@problem_id:2695204]。

- **情形 2：$\mathbf{F}$ 可逆且 $\det(\mathbf{F})  0$**
这种情况在物理上对应于物质的“内外翻转”，通常被排除。然而从数学上讲，此时不存在 $\mathbf{R} \in \mathrm{SO}(3)$ 的分解。但存在一个唯一的分解 $\mathbf{F} = \mathbf{R}\mathbf{U}$，其中 $\mathbf{U}$ 是SPD，但 $\mathbf{R}$ 是一个**非真反常正交张量 (improper orthogonal tensor)**，其[行列式](@entry_id:142978)为-1（例如一个反射）[@problem_id:2695204]。

- **情形 3：$\mathbf{F}$ 奇异，即 $\det(\mathbf{F}) = 0$**
这种情况对应于体积被压缩为零，例如一个三维物体被压成一个平面。此时，[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 是对称半正定的 (SPSD)，它仍然存在一个唯一的SPSD平方根 $\mathbf{U}$。然而，由于 $\mathbf{U}$ 不可逆，我们不能用 $\mathbf{R} = \mathbf{F}\mathbf{U}^{-1}$ 来确定 $\mathbf{R}$。可以证明，虽然存在满足 $\mathbf{F} = \mathbf{R}\mathbf{U}$ 的正交张量 $\mathbf{R}$，但它不再是唯一的。不唯一性源于 $\mathbf{U}$ 存在[零空间](@entry_id:171336) (null space)，$\mathbf{R}$ 在这个[零空间](@entry_id:171336)上的作用是不受约束的 [@problem_id:2695204]。

### 应用与推论

变形梯度和极分解是建立宏观材料本构理论的基石。它们最重要的应用之一是确保本构关系满足[客观性原理](@entry_id:185412)。

#### [客观性原理](@entry_id:185412) (物质标架无关性)

**[客观性原理](@entry_id:185412) (Principle of material frame indifference)**，或称物质标架无关性，要求物理定律（特别是材料的本构关系）不应依赖于观察者。这意味着，如果一个观察者相对于另一个观察者正在进行刚体运动（平移和旋转），他们观察到的材料响应规律应该是等价的。

考虑一个额外的刚体旋转 $\mathbf{Q} \in \mathrm{SO}(3)$ 施加在当前构型上。新的运动变为 $\mathbf{x}^* = \mathbf{Q}\mathbf{x}$，对应的变形梯度为 $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$。[客观性原理](@entry_id:185412)要求本构关系必须以一种与 $\mathbf{Q}$ 协调的方式变换。

让我们分析关键运动学量在这一变换下的行为 [@problem_id:2695201, @problem_id:2695222]：
- 新的[右柯西-格林张量](@entry_id:174156) $\mathbf{C}^* = (\mathbf{F}^*)^{\mathsf{T}}\mathbf{F}^* = (\mathbf{Q}\mathbf{F})^{\mathsf{T}}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^{\mathsf{T}}\mathbf{Q}^{\mathsf{T}}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \mathbf{C}$。
- 因此，右[拉伸张量](@entry_id:193200) $\mathbf{U}^* = \sqrt{\mathbf{C}^*} = \sqrt{\mathbf{C}} = \mathbf{U}$。

我们发现 $\mathbf{C}$ 和 $\mathbf{U}$ 在叠加的刚体旋转下保持不变。它们是**客观的 (objective)** 或 **标架无关的 (frame-indifferent)** 张量。相反，[左柯西-格林张量](@entry_id:186163)和[旋转张量](@entry_id:191990)则会变换：
- $\mathbf{B}^* = \mathbf{Q}\mathbf{B}\mathbf{Q}^{\mathsf{T}}$
- $\mathbf{R}^* = \mathbf{Q}\mathbf{R}$

这一结果对于建立[本构关系](@entry_id:186508)具有决定性意义。对于一个标量本构函数，例如[超弹性材料](@entry_id:190241)的**[应变能密度函数](@entry_id:755490) (strain energy density function)** $\Psi$，客观性要求 $\Psi(\mathbf{F}^*) = \Psi(\mathbf{F})$，即 $\Psi(\mathbf{Q}\mathbf{F}) = \Psi(\mathbf{F})$。这表明 $\Psi$ 只能通过那些客观的量来依赖于 $\mathbf{F}$。因此，任何客观的[应变能函数](@entry_id:178435)必须可以写成仅依赖于 $\mathbf{C}$ 或 $\mathbf{U}$ 的形式 [@problem_id:2695201]：

$$
\Psi(\mathbf{F}) = \hat{\Psi}(\mathbf{C}) \quad \text{或等价地} \quad \Psi(\mathbf{F}) = \tilde{\Psi}(\mathbf{U})
$$

直接依赖于 $\mathbf{F}$ 本身（例如 $\Psi = \alpha\,\mathrm{tr}(\mathbf{F})$）或 $\mathbf{R}$ 的本构关系通常会违反[客观性原理](@entry_id:185412)。例如，对于 $\Psi = \alpha\,\mathrm{tr}(\mathbf{F})$，$\mathrm{tr}(\mathbf{F}^*) = \mathrm{tr}(\mathbf{Q}\mathbf{F})$ 通常不等于 $\mathrm{tr}(\mathbf{F})$，因此该形式是非客观的 [@problem_id:2695222]。对于张量值的本构关系，如柯西应力 $\boldsymbol{\sigma}$，客观性要求 $\boldsymbol{\sigma}(\mathbf{F}^*) = \mathbf{Q}\boldsymbol{\sigma}(\mathbf{F})\mathbf{Q}^{\mathsf{T}}$。可以证明，形如 $\boldsymbol{\sigma} = \beta \mathbf{B}$ 的关系是客观的，而形如 $\boldsymbol{\sigma} = \delta (\mathbf{F}+\mathbf{F}^{\mathsf{T}})$ 的关系则不是 [@problem_id:2695222]。

#### 作为度量张量的应变

[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 还有一个更为深刻的几何解释：它是变形在物质构型上诱导的**度量张量 (metric tensor)** [@problem_id:2695189]。

我们可以将参考构型 $\mathcal{B}_0$ 视为一个抽象的**物质[流形](@entry_id:153038) (material manifold)**。变形映射 $\boldsymbol{\chi}$ 将这个[流形嵌入](@entry_id:159781)到我们熟悉的欧几里得空间 $\mathbb{R}^3$ 中。[欧氏空间](@entry_id:138052)本身带有一个标准的度量 $g(\mathbf{a}, \mathbf{b}) = \mathbf{a} \cdot \mathbf{b}$，它定义了长度和角度。

通过映射 $\boldsymbol{\chi}$，我们可以将空间度量 $g$ “[拉回](@entry_id:160816)” (pullback) 到物质[流形](@entry_id:153038)上，从而在 $\mathcal{B}_0$ 上定义一个新的度量 $\mathbf{G} = \boldsymbol{\chi}^*g$。根据[拉回](@entry_id:160816)的定义，对于物质点 $\mathbf{X}$ 处的任意两个切矢量（代表两个物质线元方向）$\mathbf{U}_{\text{vec}}, \mathbf{V}_{\text{vec}} \in T_{\mathbf{X}}\mathcal{B}_0$，它们在新度量下的[内积](@entry_id:158127)为：

$$
\mathbf{G}_{\mathbf{X}}(\mathbf{U}_{\text{vec}}, \mathbf{V}_{\text{vec}}) = g_{\boldsymbol{\chi}(\mathbf{X})}(T\boldsymbol{\chi}_{\mathbf{X}}\mathbf{U}_{\text{vec}}, T\boldsymbol{\chi}_{\mathbf{X}}\mathbf{V}_{\text{vec}}) = (\mathbf{F}\mathbf{U}_{\text{vec}}) \cdot (\mathbf{F}\mathbf{V}_{\text{vec}})
$$

在矩阵分量形式下，这可以写作 $\mathbf{U}_{\text{vec}}^{\mathsf{T}}\mathbf{F}^{\mathsf{T}}\mathbf{F}\mathbf{V}_{\text{vec}} = \mathbf{U}_{\text{vec}}^{\mathsf{T}}\mathbf{C}\mathbf{V}_{\text{vec}}$。这惊人地揭示了：

**[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 正是空间欧氏度量在物质[流形](@entry_id:153038)上诱导的度量张量的分量矩阵。**

这个观点为 $\mathbf{C}$ 赋予了清晰的几何意义。它定义了如何在参考构型中测量长度和角度，就好像这些测量是在变形后的当前构型中进行的一样。例如，参考构型中一个[线元](@entry_id:196833) $d\mathbf{X}$ 的“变形后长度”的平方是 $ds^2 = |d\mathbf{x}|^2 = |\mathbf{F}d\mathbf{X}|^2 = (d\mathbf{X})^{\mathsf{T}}\mathbf{C}(d\mathbf{X})$。因此，$\mathbf{C}$ 是描述变形状态的内在量度。由于 $\mathbf{C}$ 是客观的，这个诱导度量自然也是客观的。

从这个角度看，$\mathbf{C} = \mathbf{U}^2$ 的谱分解也变得非常自然。$\mathbf{C}$ 的[特征值](@entry_id:154894) $\lambda_i^2$ 和特征矢量 $\mathbf{N}_i$ 正是这个诱导度量的[主伸长](@entry_id:194664)（的平方）和[主方向](@entry_id:276187) [@problem_id:2695189]。这一现代几何观点统一并深化了我们对变形和应变的理解，为更高级的材料理论（如非欧几何[弹塑性](@entry_id:193198)）奠定了基础。