## 引言
当物体经历大变形时，例如金属的塑性成型或软组织的拉伸，经典的线性应变理论不再适用。为了精确描述和预测这些复杂的力学行为，连续介质力学引入了有限应变的概念。然而，描述变形的形变梯度张量同时包含了拉伸与刚体转动，这使得直接使用它来构建本构关系变得困难且不符合物理客观性。如何从总变形中分离出纯粹的应变，是建立严谨的非线性力学理论所必须解决的核心问题。

本文旨在系统性地解决这一问题。在**“原理与机制”**一章中，我们将从形变梯度和客观性原理出发，详细推导三种关键的有限应变度量——Green-Lagrange应变、Almansi应变和Hencky应变，并比较它们的数学特性。接下来的**“应用与交叉学科联系”**一章将展示这些理论工具如何在超弹性、塑性理论、计算固体力学及生物力学等前沿领域中发挥关键作用，并阐明选择不同度量的具体考量。最后，通过**“动手实践”**部分提供的计算练习，读者将有机会亲手应用这些概念，深化对有限应变理论的理解。

## 原理与机制

在连续介质力学中，为了描述物体从初始参考构型到当前构型的变形，我们需要精确的数学工具。虽然形变梯度张量 $\mathbf{F}$ 包含了变形的全部信息，但它本身并非纯粹的应变度量，因为它还包含了刚体转动。一个有效的应变度量必须能将变形与刚体运动分离开来，这一要求引出了“客观性”原理。本章将深入探讨有限应变理论的基石，系统阐述Green-Lagrange应变、Almansi应变和Hencky应变这三种核心应变度量的定义、物理意义、数学性质及其在不同工程问题中的应用选择。

### 形变梯度与客观性原理

一切有限应变理论都始于**形变梯度**（deformation gradient）$\mathbf{F}$。它是一个二阶张量，定义为一个物质点$\mathbf{X}$在参考构型中的位置到其在当前构型中位置$\mathbf{x}$的映射$\mathbf{x} = \boldsymbol{\chi}(\mathbf{X})$的梯度：

$$
\mathbf{F} = \nabla_{\mathbf{X}} \boldsymbol{\chi}(\mathbf{X})
$$

形变梯度的核心作用在于它将参考构型中的无限小物质线元 $d\mathbf{X}$ 映射到当前构型中的空间线元 $d\mathbf{x}$：

$$
d\mathbf{x} = \mathbf{F} d\mathbf{X}
$$

然而，$\mathbf{F}$ 本身并非理想的应变度量。考虑一个刚体运动，即物体只发生平移和转动，其内部任何两点间的距离保持不变，因此不应产生任何应变。一个纯刚体运动的形变梯度可以表示为 $\mathbf{F} = \mathbf{Q}$，其中 $\mathbf{Q}$ 是一个正交张量（$\mathbf{Q}^{\mathsf{T}}\mathbf{Q}=\mathbf{I}$）。一个纯粹的应变度量在这种情况下应该为零。

为了使理论具有物理意义，应变度量必须满足**客观性原理**（principle of objectivity），也称**物质标架无关性**（material frame-indifference）。该原理指出，本构关系不应依赖于观察者。在运动学上，这意味着如果我们对当前构型再叠加一个刚体运动（例如，通过一个旋转张量 $\mathbf{Q}$），应变度量应该相应地保持不变或以明确的张量方式转换。这种叠加的刚体运动将使空间位置变为 $\mathbf{x}^* = \mathbf{Q}\mathbf{x} + \mathbf{c}$，对应的形变梯度变为 $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$ [@problem_id:2640340]。

对于一个定义在参考构型上的**物质（拉格朗日）应变度量** $\mathbf{S}(\mathbf{F})$，客观性要求它在叠加刚体运动后保持不变：

$$
\mathbf{S}(\mathbf{F}^*) = \mathbf{S}(\mathbf{Q}\mathbf{F}) = \mathbf{S}(\mathbf{F}) \quad \text{for all } \mathbf{Q} \in \mathrm{SO}(3)
$$

其中 $\mathrm{SO}(3)$ 是三维特殊正交群（即旋转群）。任何直接线性依赖于 $\mathbf{F}$ 的量，例如 $\mathbf{F}-\mathbf{I}$，都无法满足此要求，因为它会变成 $\mathbf{Q}\mathbf{F}-\mathbf{I}$，这通常不等于 $\mathbf{F}-\mathbf{I}$。事实上，可以证明，任何线性依赖于$\mathbf{F}$的物质应变度量，若要满足客观性，则其值必须恒为零 [@problem_id:2640387]。这迫使我们必须寻找对 $\mathbf{F}$ 具有非线性依赖关系的应变度量，这些度量能够“滤除”旋转$\mathbf{Q}$的影响。

### 极分解：分离拉伸与转动

解决客观性问题的关键在于**极分解定理**（polar decomposition theorem）。该定理指出，任何可逆的形变梯度 $\mathbf{F}$（即 $\det \mathbf{F} > 0$）都可以被唯一地分解为一个纯拉伸（或压缩）与一个纯旋转的乘积。这存在两种形式 [@problem_id:2640372]：

1.  **右极分解**：$\mathbf{F} = \mathbf{R}\mathbf{U}$
2.  **左极分解**：$\mathbf{F} = \mathbf{V}\mathbf{R}$

在这里，$\mathbf{R}$ 是一个唯一的旋转张量（$\mathbf{R} \in \mathrm{SO}(3)$）。$\mathbf{U}$ 和 $\mathbf{V}$ 分别是唯一的对称正定（SPD）张量，被称为**右拉伸张量**（right stretch tensor）和**左拉伸张量**（left stretch tensor）。$\mathbf{U}$ 作用于参考构型，而 $\mathbf{V}$ 作用于旋转后的构型。

这两个拉伸张量包含了所有关于纯变形（即形状和尺寸变化）的信息。它们通过旋转张量$\mathbf{R}$相互关联：$\mathbf{V} = \mathbf{R}\mathbf{U}\mathbf{R}^{\mathsf{T}}$。这意味着它们是相似张量，拥有相同的特征值。这些特征值，记为 $\lambda_i$（$i=1,2,3$），被称为**主拉伸**（principal stretches），它们量化了在三个相互垂直方向上的拉伸或压缩程度 [@problem_id:2640372]。

极分解的深刻意义在于，它为我们指明了构建客观应变度量的正确道路：任何只依赖于拉伸张量 $\mathbf{U}$ 或 $\mathbf{V}$ 的函数都将自动满足客观性要求。

### 拉格朗日应变度量：物质视角

拉格朗日（Lagrangian）或物质（material）度量是在参考构型中定义的。它们从初始状态出发，衡量变形的程度。

#### 右柯西-格林张量

构建拉格朗日应变度量的基石是**右柯西-格林张量**（right Cauchy-Green tensor）$\mathbf{C}$，定义为：

$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}
$$

利用右极分解 $\mathbf{F}=\mathbf{R}\mathbf{U}$，我们可以看到 $\mathbf{C} = (\mathbf{R}\mathbf{U})^{\mathsf{T}}(\mathbf{R}\mathbf{U}) = \mathbf{U}^{\mathsf{T}}\mathbf{R}^{\mathsf{T}}\mathbf{R}\mathbf{U} = \mathbf{U}^{\mathsf{T}}\mathbf{I}\mathbf{U} = \mathbf{U}^2$（因为$\mathbf{U}$是对称的）。因此，$\mathbf{C}$ 直接度量了拉伸的平方。

$\mathbf{C}$最重要的性质是其在叠加刚体运动下的**不变性**。对于变换后的形变梯度 $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$，我们有：

$$
\mathbf{C}^* = (\mathbf{F}^*)^{\mathsf{T}}\mathbf{F}^* = (\mathbf{Q}\mathbf{F})^{\mathsf{T}}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^{\mathsf{T}}\mathbf{Q}^{\mathsf{T}}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\mathsf{T}}\mathbf{I}\mathbf{F} = \mathbf{C}
$$

由于 $\mathbf{C}$ 不受叠加的刚体转动 $\mathbf{Q}$ 的影响，任何仅依赖于 $\mathbf{C}$ 的张量都将是客观的物质度量 [@problem_id:2640340] [@problem_id:2640387]。

从物理上看，$\mathbf{C}$ 描述了物质线元长度的平方如何变化。一个初始长度为 $dS^2 = d\mathbf{X} \cdot d\mathbf{X}$ 的线元，变形后的长度平方为 $ds^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F}d\mathbf{X}) \cdot (\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{F}^{\mathsf{T}}\mathbf{F} d\mathbf{X}) = d\mathbf{X} \cdot \mathbf{C} d\mathbf{X}$ [@problem_id:2640392]。

#### Green-Lagrange应变张量

有了 $\mathbf{C}$，定义一个纯应变度量就变得直截了当。我们希望应变在没有变形时（即 $\mathbf{F}=\mathbf{I}$，此时 $\mathbf{C}=\mathbf{I}$）为零。**Green-Lagrange应变张量**（Green-Lagrange strain tensor）$\mathbf{E}$ 正是为此而生，它被定义为：

$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^{\mathsf{T}}\mathbf{F} - \mathbf{I})
$$

这个定义源于对线元长度平方变化量的直接度量。长度平方的改变值 $ds^2 - dS^2$ 可以写成：

$$
ds^2 - dS^2 = d\mathbf{X} \cdot \mathbf{C} d\mathbf{X} - d\mathbf{X} \cdot \mathbf{I} d\mathbf{X} = d\mathbf{X} \cdot (\mathbf{C}-\mathbf{I}) d\mathbf{X} = 2 d\mathbf{X} \cdot \mathbf{E} d\mathbf{X}
$$

因此，$\mathbf{E}$ 直接量化了变形引起的度量变化 [@problem_id:2640367] [@problem_id:2640392]。由于 $\mathbf{C}$ 是客观的，$\mathbf{E}$ 显然也是一个客观的物质应变张量。对于任何刚体运动（$\mathbf{F}=\mathbf{Q}$），$\mathbf{C}=\mathbf{I}$，因此 $\mathbf{E}=\mathbf{0}$，这符合应变度量的基本要求 [@problem_id:2640367]。

### 欧拉应变度量：空间视角

与拉格朗日度量相反，欧拉（Eulerian）或空间（spatial）度量是在当前构型中定义的。它们着眼于最终状态，描述到达该状态所经历的变形。

#### 左柯西-格林张量

与右柯西-格林张量相对应，**左柯西-格林张量**（left Cauchy-Green tensor），也称**Finger张量**，定义为：

$$
\mathbf{b} = \mathbf{F}\mathbf{F}^{\mathsf{T}}
$$

利用左极分解 $\mathbf{F}=\mathbf{V}\mathbf{R}$，可得 $\mathbf{b} = \mathbf{V}^2$。$\mathbf{b}$ 在叠加刚体运动下的变换规律与 $\mathbf{C}$ 不同。对于 $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$：

$$
\mathbf{b}^* = \mathbf{F}^*(\mathbf{F}^*)^{\mathsf{T}} = (\mathbf{Q}\mathbf{F})(\mathbf{Q}\mathbf{F})^{\mathsf{T}} = \mathbf{Q}\mathbf{F}\mathbf{F}^{\mathsf{T}}\mathbf{Q}^{\mathsf{T}} = \mathbf{Q}\mathbf{b}\mathbf{Q}^{\mathsf{T}}
$$

这个变换规律表明 $\mathbf{b}$ 并非不变量，但它遵循一个客观空间二阶张量的变换法则。因此，任何基于 $\mathbf{b}$ 并遵循适当张量法则构造的量，都可以是客观的空间度量 [@problem_id:2640340]。$\mathbf{b}$ 的不变量（如迹 $\text{tr}(\mathbf{b})$ 和行列式 $\det(\mathbf{b})$）在叠加刚体运动下保持不变 [@problem_id:2640340]。

#### Almansi应变张量

为了得到一个空间应变度量，我们将长度平方的变化量 $ds^2 - dS^2$ 表示为当前构型线元 $d\mathbf{x}$ 的二次型。我们有 $d\mathbf{X} = \mathbf{F}^{-1}d\mathbf{x}$，因此 $dS^2 = d\mathbf{X} \cdot d\mathbf{X} = d\mathbf{x} \cdot (\mathbf{F}^{-\mathsf{T}}\mathbf{F}^{-1}d\mathbf{x}) = d\mathbf{x} \cdot \mathbf{b}^{-1}d\mathbf{x}$。于是：

$$
ds^2 - dS^2 = d\mathbf{x} \cdot \mathbf{I} d\mathbf{x} - d\mathbf{x} \cdot \mathbf{b}^{-1} d\mathbf{x} = d\mathbf{x} \cdot (\mathbf{I} - \mathbf{b}^{-1}) d\mathbf{x}
$$

由此，我们定义**Almansi应变张量**（Almansi strain tensor）$\mathbf{e}$ 为：

$$
\mathbf{e} = \frac{1}{2}(\mathbf{I} - \mathbf{b}^{-1})
$$

使得 $ds^2 - dS^2 = 2 d\mathbf{x} \cdot \mathbf{e} d\mathbf{x}$ [@problem_id:2640421]。$\mathbf{e}$ 是一个客观的空间应变张量，其变换规律为 $\mathbf{e}^* = \mathbf{Q}\mathbf{e}\mathbf{Q}^{\mathsf{T}}$，并且对于刚体运动（$\mathbf{F}=\mathbf{Q}$, $\mathbf{b}=\mathbf{I}$）其值为零 [@problem_id:2640421]。

#### 拉格朗日与欧拉度量的联系

$\mathbf{E}$ 和 $\mathbf{e}$ 分别从物质和空间视角描述了同一个变形过程，它们之间存在着密切的代数关系。通过简单的代换可以证明，它们可以通过形变梯度 $\mathbf{F}$相互转换，这种操作分别称为**前推**（push-forward）和**后拉**（pull-back）：

$$
\mathbf{e} = \mathbf{F}^{-\mathsf{T}}\mathbf{E}\mathbf{F}^{-1} \quad \text{(E to e: push-forward)}
$$
$$
\mathbf{E} = \mathbf{F}^{\mathsf{T}}\mathbf{e}\mathbf{F} \quad \text{(e to E: pull-back)}
$$

这些关系在不同力学框架（如总拉格朗日法和更新拉格朗日法）之间转换应力与应变时至关重要 [@problem_id:2640367] [@problem_id:2640421]。

### Hencky应变：对数视角

Green-Lagrange和Almansi应变都是基于长度的*平方*定义的，这导致它们在描述连续发生的变形时不具备简单的可加性。为了克服这一限制，**Hencky应变**（Hencky strain），或称**对数应变**（logarithmic strain），被提了出来。它直接基于拉伸张量本身，而非其平方。

利用张量对数函数，Hencky应变被定义为：

*   物质（拉格朗日）Hencky应变： $\mathbf{H} = \ln \mathbf{U} = \frac{1}{2}\ln \mathbf{C}$
*   空间（欧拉）Hencky应变： $\mathbf{h} = \ln \mathbf{V} = \frac{1}{2}\ln \mathbf{b}$

这里的张量对数是通过对张量的谱分解（spectral decomposition）来定义的。如果一个对称张量 $\mathbf{S}$ 的谱分解为 $\mathbf{S} = \sum_{i=1}^3 \mu_i \mathbf{n}_i \otimes \mathbf{n}_i$，其中 $\mu_i$ 是特征值，$\mathbf{n}_i$ 是对应的特征向量，则其对数为 $\ln \mathbf{S} = \sum_{i=1}^3 (\ln \mu_i) \mathbf{n}_i \otimes \mathbf{n}_i$ [@problem_id:2640338]。因此，Hencky应变的主值就是主拉伸的自然对数，即 $\ln \lambda_i$。

Hencky应变具有两个非常优越的性质：

1.  **可加性**：对于两个连续发生的、主方向相同的（共轴）变形，其总的Hencky应变等于各个步骤Hencky应变之和。如果两次变形的右拉伸张量分别为 $\mathbf{U}_1$ 和 $\mathbf{U}_2$ 且它们可交换（$\mathbf{U}_1\mathbf{U}_2=\mathbf{U}_2\mathbf{U}_1$），则总拉伸为 $\mathbf{U} = \mathbf{U}_2\mathbf{U}_1$。由于对数函数将乘法转换为加法，我们有 $\mathbf{H} = \ln(\mathbf{U}_2\mathbf{U}_1) = \ln \mathbf{U}_2 + \ln \mathbf{U}_1 = \mathbf{H}_2 + \mathbf{H}_1$。相比之下，Green-Lagrange应变 $\mathbf{E}$ 和 Almansi应变 $\mathbf{e}$ 均不具备此性质 [@problem_id:2640338] [@problem_id:2640405]。

2.  **精确的体积-偏量分离**：一个变形可以分解为体积改变和形状改变（等容变形）两部分。Hencky应变的迹（trace）直接与体积变化的对数相关。体积比 $J = \det \mathbf{F} = \lambda_1\lambda_2\lambda_3$。Hencky应变的迹为：
    $$
    \text{tr}(\mathbf{H}) = \sum_{i=1}^3 \ln \lambda_i = \ln(\lambda_1\lambda_2\lambda_3) = \ln J
    $$
    这意味着，$\mathbf{H}$ 的迹准确地捕捉了体积变化，而其偏量部分 $\text{dev}(\mathbf{H}) = \mathbf{H} - \frac{1}{3}\text{tr}(\mathbf{H})\mathbf{I}$ 则纯粹描述了形状的改变（等容变形）。对于等容变形（$J=1$），Hencky应变的迹恒为零 [@problem_id:2640338]。这一清晰的分离在$\mathbf{E}$和$\mathbf{e}$中是不存在的，这使得Hencky应变在弹塑性等本构理论中极具优势 [@problem_id:2640409]。

### 比较分析与选择标准

为了更直观地理解这三种应变度量的差异，我们考察一个简单的一维拉伸问题，$x = \lambda X$，其中 $\lambda$ 是拉伸比。此时，各种张量退化为标量：$F=\lambda, C=b=\lambda^2, U=V=\lambda$。三种应变度量相应简化为 [@problem_id:2640403]：

*   Green-Lagrange应变： $E = \frac{1}{2}(\lambda^2 - 1)$
*   Almansi应变： $e = \frac{1}{2}(1 - \lambda^{-2})$
*   Hencky应变： $H = \ln \lambda$

通过分析这些函数可以发现：

- **排序关系**：对于任何 $\lambda > 0$，这些应变度量满足不等式 $E \ge H \ge e$，等号仅在 $\lambda=1$（无变形）时成立 [@problem_id:2640403]。在拉伸（$\lambda>1$）时，$E$ 的值最大；在压缩（$\lambda1$）时，$e$ 的绝对值最大。

- **小应变极限**：当变形很小时，即 $\lambda = 1+\varepsilon$ 且 $|\varepsilon| \ll 1$，这三种应变度量都趋近于工程应变 $\varepsilon$。通过泰勒展开：
    $E = \frac{1}{2}((1+\varepsilon)^2 - 1) = \varepsilon + O(\varepsilon^2)$
    $e = \frac{1}{2}(1 - (1+\varepsilon)^{-2}) = \varepsilon + O(\varepsilon^2)$
    $H = \ln(1+\varepsilon) = \varepsilon + O(\varepsilon^2)$
    这表明有限应变理论在小变形情况下能够自然地过渡到经典的线性应变理论 [@problem_id:2640403]。

- **对称性**：在拉伸和压缩之间，Hencky应变表现出最佳的对称性，$H(1/\lambda) = \ln(1/\lambda) = - \ln \lambda = -H(\lambda)$。而Green-Lagrange和Almansi应变之间存在一种有趣的对偶关系：$E(1/\lambda) = \frac{1}{2}(\lambda^{-2} - 1) = -e(\lambda)$ [@problem_id:2640403]。

在实际应用中，选择哪种应变度量取决于具体的物理问题和计算框架 [@problem_id:2640409]：

- **Green-Lagrange应变 ($\mathbf{E}$)** 是**总拉格朗日（Total Lagrangian）**有限元公式的首选。在这种公式中，所有计算都在初始参考构型上进行。对于许多超弹性材料（如橡胶），其应变能函数通常被方便地表达为$\mathbf{C}$（或$\mathbf{E}$）的不变量的函数。

- **Almansi应变 ($\mathbf{e}$)** 及其相关的率形式在**欧拉（Eulerian）**描述中更为自然，例如在流体力学或流固耦合问题中，计算网格固定在空间中，材料流过网格。此时，所有物理量都在当前构型上定义，使用空间应变度量更为便捷。

- **Hencky应变 ($\mathbf{H}$)** 在**大应变弹塑性**和晶体塑性等领域占据主导地位。其对于共轴变形的可加性和精确的体积-偏量分离特性，与金属塑性流动理论的物理假设（如屈服面通常只依赖于偏量应力）完美契合，极大地简化了本构模型的构建和数值积分算法的实现。

综上所述，Green-Lagrange、Almansi和Hencky应变虽然在小变形下趋于一致，但在有限变形领域，它们各自具有独特的数学性质和物理诠释。理解这些差异并根据问题需求做出明智选择，是进行高级非线性力学分析的关键一步。