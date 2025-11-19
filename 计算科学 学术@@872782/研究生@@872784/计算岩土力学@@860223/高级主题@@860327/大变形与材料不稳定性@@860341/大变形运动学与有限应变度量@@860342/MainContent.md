## 引言
当材料（如岩土、金属或软组织）经历显著的形状或体积改变时，经典的小应变理论便不再适用。准确描述和模拟这类[大变形](@entry_id:167243)现象，是现代[计算力学](@entry_id:174464)，尤其是计算岩[土力学](@entry_id:180264)领域，面临的核心挑战。其关键在于建立一个能够严格区分[刚体运动](@entry_id:193355)与真实变形、并能为复杂材料行为提供坚实基础的运动学框架。本文旨在系统性地解决这一问题，为读者构建从基础理论到前沿应用的完整知识体系。

在接下来的内容中，我们将分三步深入探索这一领域。**第一章：原理与机制**将奠定数学基础，从变形梯度的定义出发，详细解析极分解、多种有限应变测度及其物理意义，并引入乘法[弹塑性](@entry_id:193198)等核心概念。**第二章：应用与交叉学科联系**将展示这些理论的强大应用价值，探讨如何利用它们构建高级[本构模型](@entry_id:174726)、处理复杂的边界条件，并解决[渗流](@entry_id:158786)、[热力耦合](@entry_id:183230)等交叉学科问题。最后，**第三章：动手实践**将通过一系列具体的计算练习，帮助读者将抽象的理论转化为可操作的技能。

## 原理与机制

本章旨在系统阐述[大变形](@entry_id:167243)[运动学](@entry_id:173318)和有限应变测度的核心原理与机制。在前一章介绍性内容的基础上，我们将深入探讨描述连续体运动与变形的数学工具，从变形梯度的基本概念出发，通过极分解将其分解为[刚体转动](@entry_id:191086)和纯拉伸，进而引出多种有限应变张量的定义。本章将重点辨析不同应变测度的物理意义、[适用范围](@entry_id:636189)及其在小应变和[大应变](@entry_id:751152)极限下的行为。此外，我们还将探讨变形率、[客观应力率](@entry_id:199282)等与[本构关系](@entry_id:186508)密切相关的概念，并最终将这些理论工具应用于岩土力学中的一个关键领域——[大应变](@entry_id:751152)[弹塑性](@entry_id:193198)。

### 运动学基础：运动、构型与变形

在连续介质力学中，一个物体的运动是通过一个光滑的映射函数 **运动（motion）** $\boldsymbol{\varphi}$ 来描述的。该函数将物体在某一参考时刻（通常设为 $t=0$）所占据的区域中的每一个物[质点](@entry_id:186768) $\mathbf{X}$，映射到当前时刻 $t$ 其在空间中的位置 $\mathbf{x}$。

$$
\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)
$$

物体在 $t=0$ 时占据的空间区域被称为 **参考构型（reference configuration）**，记为 $\mathcal{B}_0$。物[质点](@entry_id:186768)在参考构型中的位置矢量 $\mathbf{X}$ 被称为 **物质坐标（material coordinates）** 或拉格朗日坐标。随着时间的推移，物体在时刻 $t$ 占据的区域被称为 **当前构型（current configuration）**，记为 $\mathcal{B}_t$。物[质点](@entry_id:186768)在当前构型中的位置矢量 $\mathbf{x}$ 被称为 **空间坐标（spatial coordinates）** 或欧拉坐标。

基于这两种[坐标系](@entry_id:156346)，物理场（如温度、密度、位移等）可以有两种不同的描述方式。**物质描述（material description）**，或称 **[拉格朗日描述](@entry_id:264498)（Lagrangian description）**，将物理量视为物质坐标 $\mathbf{X}$ 和时间 $t$ 的函数，例如密度场 $A(\mathbf{X}, t)$。它追踪特定物[质点](@entry_id:186768)的物理量如何随[时间演化](@entry_id:153943)。相对地，**空间描述（spatial description）**，或称 **[欧拉描述](@entry_id:264722)（Eulerian description）**，将物理量视为空间坐标 $\mathbf{x}$ 和时间 $t$ 的函数，例如 $a(\mathbf{x}, t)$。它关注在特定空间位置上物理量的瞬时值，而不关心是哪个物[质点](@entry_id:186768)恰好经过该位置。这两种描述通过运动函数 $\boldsymbol{\varphi}$ 联系在一起：

$$
A(\mathbf{X}, t) = a(\boldsymbol{\varphi}(\mathbf{X}, t), t) \quad \text{以及} \quad a(\mathbf{x}, t) = A(\boldsymbol{\varphi}^{-1}(\mathbf{x}, t), t)
$$

为了保证这种关系良好定义且物理上合理，运动函数 $\boldsymbol{\varphi}$ 必须满足一系列 **可容许性条件（admissibility conditions）** [@problem_id:3538138]。首先，为了定义[速度场](@entry_id:271461)，$\boldsymbol{\varphi}$ 必须对时间 $t$ 至少是一次连续可微的。其次，为了定义变形梯度，$\boldsymbol{\varphi}$ 必须对物质坐标 $\mathbf{X}$ 至少是一次连续可微的。更严格地说，为了确保物质与空间描述之间的可逆转换，对于任意固定的时刻 $t$，映射 $\boldsymbol{\varphi}(\cdot, t)$ 必须是一个从 $\mathcal{B}_0$ 到 $\mathcal{B}_t$ 的 **$C^1$ 阶微分同胚（$C^1$ diffeomorphism）**。这意味着该映射是双射（既是单射也是满射），且其本身和它的逆映射都是连续可微的。

物理上，这些数学条件对应着清晰的直观概念：
1.  **物质不可入性（Impenetrability of matter）**：不同的物质点在同一时刻不能占据相同的空间位置。这要求映射 $\boldsymbol{\varphi}(\cdot, t)$ 是 **单射的（injective）**。
2.  **方向保持性（Orientation preservation）**：物质微元不能被“翻转”成镜像。这要求运动的雅可比行列式（Jacobian）必须为正。

这些条件的综合，构成了大变形运动学分析的坚实基础。

### 变形梯度：局部变形的度量

描述局部变形的核心工具是 **变形梯度（deformation gradient）** 张量 $\mathbf{F}$。它被定义为运动函数 $\boldsymbol{\varphi}$ 对物质坐标 $\mathbf{X}$ 的梯度：

$$
\mathbf{F}(\mathbf{X}, t) = \nabla_{\mathbf{X}} \boldsymbol{\varphi}(\mathbf{X}, t) \equiv \frac{\partial \boldsymbol{\varphi}}{\partial \mathbf{X}}
$$

变形梯度是一个[二阶张量](@entry_id:199780)，它将参考构型中的一个无穷小物质[线元](@entry_id:196833) $d\mathbf{X}$ 映射到当前构型中对应的空间[线元](@entry_id:196833) $d\mathbf{x}$：

$$
d\mathbf{x} = \mathbf{F} d\mathbf{X}
$$

因此，$\mathbf{F}$ 完整地描述了一个物[质点](@entry_id:186768)邻域内的局部变形，包括拉伸、剪切和[刚体转动](@entry_id:191086)。

变形梯度的[行列式](@entry_id:142978)，即[雅可比行列式](@entry_id:137120) $J = \det \mathbf{F}$，具有极其重要的物理意义 [@problem_id:3538185]。它表示了局部体积的变化率。一个在参考构型中体积为 $dV_0$ 的无穷小物质微元，在当前构型中的体积 $dV$ 为：

$$
dV = J dV_0
$$

根据[质量守恒定律](@entry_id:147377)，物质微元的质量 $\rho_0 dV_0$ 保持不变，即 $\rho_0 dV_0 = \rho dV$，其中 $\rho_0$ 和 $\rho$ 分别是参考构型和当前构型中的密度。结合体积变化关系，我们得到局部质量守恒的表达式：

$$
\rho_0 = \rho J
$$

由于物质不能被压缩至零体积或负体积，且密度必须为正，物理上可容许的运动必须满足 $J > 0$。$J=1$ 表示体积不变（等容）变形；$0  J  1$ 表示体积压缩；$J  1$ 表示[体积膨胀](@entry_id:144241)。$J=0$ 对应于无限压缩的[物理奇点](@entry_id:260744)，而 $J  0$ 则对应于物质微元被“由内向外翻转”的非物理情况。

值得注意的是，$J  0$ 这一条件通过[反函数定理](@entry_id:275014)保证了运动映射在每个点的 **[局部可逆性](@entry_id:143266)（local invertibility）**。然而，它并 **不** 保证 **全局[单射性](@entry_id:147722)（global injectivity）** [@problem_id:3538185]。一个连续体完全可能在变形过程中发生“折叠”或“自穿透”，使得两个原本分离的物质点 $\mathbf{X}_1$ 和 $\mathbf{X}_2$ 被映射到同一个空间位置 $\mathbf{x}$，尽管在每一点的局部变形都是有效的（即 $J0$ 处处成立）。因此，全局[单射性](@entry_id:147722)是一个比 $J0$ 更强的、需要在整个物体和运动历史中加以验证的全局约束。

### 变形的分解：转动与拉伸

变形梯度 $\mathbf{F}$ 包含了变形的全部信息，但直接使用它不便于区分拉伸和转动。**极分解定理（polar decomposition theorem）** 提供了一个强大的工具，能够将任意一个可逆的变形梯度唯一地分解为一个纯拉伸和一个[刚体转动](@entry_id:191086) [@problem_id:3538174]。

对于任何满足 $J = \det \mathbf{F}  0$ 的变形梯度，存在两种等价的分解形式：

1.  **右极分解（Right Polar Decomposition）**: $\mathbf{F} = \mathbf{R}\mathbf{U}$
2.  **左极分解（Left Polar Decomposition）**: $\mathbf{F} = \mathbf{V}\mathbf{R}$

这里：
-   $\mathbf{R}$ 是一个 **正常正交张量（proper orthogonal tensor）**，也即 **转动张量（rotation tensor）**，满足 $\mathbf{R}^\top\mathbf{R} = \mathbf{I}$ 和 $\det \mathbf{R} = 1$。它描述了物质微元的局部[刚体转动](@entry_id:191086)。
-   $\mathbf{U}$ 是 **右[拉伸张量](@entry_id:193200)（right stretch tensor）**，$\mathbf{V}$ 是 **左[拉伸张量](@entry_id:193200)（left stretch tensor）**。两者都是[对称正定](@entry_id:145886)张量（symmetric positive-definite, SPD），描述了物质微元的纯拉伸（无转动）。

这个分解的物理意义十分清晰：右极分解可以理解为先对物质微元进行纯拉伸（由 $\mathbf{U}$ 描述），然后再进行[刚体转动](@entry_id:191086)（由 $\mathbf{R}$ 描述）。左极分解则相反，是先转动后拉伸。重要的是，对于一个给定的 $\mathbf{F}$，转动 $\mathbf{R}$ 以及[拉伸张量](@entry_id:193200) $\mathbf{U}$ 和 $\mathbf{V}$ 都是 **唯一确定** 的。

这两个[拉伸张量](@entry_id:193200)与另外两个重要的变形张量—— **柯西-格林（Cauchy-Green）变形张量** ——密切相关：

-   **[右柯西-格林张量](@entry_id:174156)（Right Cauchy-Green tensor）** $\mathbf{C} = \mathbf{F}^\top\mathbf{F} = \mathbf{U}^2$
-   **[左柯西-格林张量](@entry_id:186163)（Left Cauchy-Green tensor）** $\mathbf{B} = \mathbf{F}\mathbf{F}^\top = \mathbf{V}^2$

$\mathbf{C}$ 和 $\mathbf{B}$ 都是对称正定张量，它们分别通过取唯一的[对称正定](@entry_id:145886)平方根来唯一地确定 $\mathbf{U}$ 和 $\mathbf{V}$。即 $\mathbf{U} = \sqrt{\mathbf{C}}$ 和 $\mathbf{V} = \sqrt{\mathbf{B}}$。一旦 $\mathbf{U}$ 被确定，转动张量 $\mathbf{R}$ 即可通过 $\mathbf{R} = \mathbf{F}\mathbf{U}^{-1}$ 唯一求出。这两个[拉伸张量](@entry_id:193200)通过转动张量联系在一起：$\mathbf{V} = \mathbf{R}\mathbf{U}\mathbf{R}^\top$。这意味着 $\mathbf{V}$ 和 $\mathbf{U}$ 具有相同的[特征值](@entry_id:154894)，但[特征向量](@entry_id:151813)（主拉伸方向）因转动 $\mathbf{R}$ 而不同。

### 有限应变测度：量化变形

虽然变形梯度描述了变形，但它本身不是一个纯粹的“应变”测度，因为它包含了[刚体转动](@entry_id:191086)。一个合理的应变测度应该只反映形状和大小的改变，而不受[刚体转动](@entry_id:191086)的影响，这一性质被称为 **客观性（objectivity）** 或 **标架无关性（frame-indifference）**。所有基于[拉伸张量](@entry_id:193200) $\mathbf{U}$ 或柯西-格林张量 $\mathbf{C}$ 定义的[应变张量](@entry_id:193332)都天然满足此要求。

#### 主拉伸与变形[不变量](@entry_id:148850)

描述纯拉伸的最基本量是 **主拉伸（principal stretches）** $\lambda_1, \lambda_2, \lambda_3$，它们是右[拉伸张量](@entry_id:193200) $\mathbf{U}$（以及左[拉伸张量](@entry_id:193200) $\mathbf{V}$）的三个正[特征值](@entry_id:154894)。它们代表了物质微元在三个相互正交的 **主方向（principal directions）** 上的伸长率。值得注意的是，主拉伸也等于变形梯度 $\mathbf{F}$ 的奇异值 [@problem_id:3538191]。

由于[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{U}^2$，它的[特征值](@entry_id:154894)是主拉伸的平方，即 $\lambda_1^2, \lambda_2^2, \lambda_3^2$。任何不依赖于[坐标系](@entry_id:156346)选择的变形量都可以表示为主拉伸的函数。特别地，$\mathbf{C}$ 的三个 **[主不变量](@entry_id:193522)（principal invariants）** $I_1, I_2, I_3$ 可以完全由主拉伸表达 [@problem_id:3538147]：

$$
I_1 = \text{tr}(\mathbf{C}) = \lambda_1^2 + \lambda_2^2 + \lambda_3^2
$$

$$
I_2 = \frac{1}{2}[(\text{tr}(\mathbf{C}))^2 - \text{tr}(\mathbf{C}^2)] = \lambda_1^2\lambda_2^2 + \lambda_2^2\lambda_3^2 + \lambda_3^2\lambda_1^2
$$

$$
I_3 = \det(\mathbf{C}) = \lambda_1^2\lambda_2^2\lambda_3^2 = (\lambda_1\lambda_2\lambda_3)^2 = J^2
$$

这些[不变量](@entry_id:148850)在构建[各向同性材料](@entry_id:170678)的[本构模型](@entry_id:174726)时至关重要。

#### 应变测度的理想属性与 Seth-Hill 族

一个理想的各向同性有限应变测度 $\boldsymbol{\varepsilon}$，其[主值](@entry_id:189577) $\varepsilon_i$ 应为相应主拉伸 $\lambda_i$ 的函数，即 $\varepsilon_i = f(\lambda_i)$，且函数 $f$ 应满足以下理想属性 [@problem_id:3538155]：

1.  **零应变状态**：在未变形状态下（$\lambda_i=1$），应变为零，即 $f(1) = 0$。
2.  **单调性**：应变量应随拉伸量的增加而单调增加，即 $f'(\lambda)  0$ for $\lambda  0$。这保证了更大的拉伸对应于更大的应变。
3.  **同轴可加性**：对于一系列沿相同[主方向](@entry_id:276187)施加的变形，其总应变应等于各步应变之和。由于同轴变形的拉伸是相乘的（即 $\lambda_{total} = \lambda_1 \lambda_2$），这要求函数 $f$ 满足 $f(ab) = f(a) + f(b)$。

满足以上所有条件的函数形式是对数函数。这使得[对数应变](@entry_id:751438)具有独特的理论地位。然而，在实践中，多种不同的应变定义被广泛使用。它们可以被归入一个广义的 **Seth-Hill 应变族（Seth-Hill family of strains）**，其[主应变](@entry_id:197797)分量定义为：

$$
\varepsilon_i^{(m)} = \frac{\lambda_i^m - 1}{m}, \quad m \in \mathbb{R}, m \neq 0
$$

当 $m \to 0$ 时，通过[洛必达法则](@entry_id:147503)可得极限情况：

$$
\varepsilon_i^{(0)} = \lim_{m \to 0} \frac{\lambda_i^m - 1}{m} = \ln \lambda_i
$$

这个家族包含了许多著名的应变测度：

-   **[格林-拉格朗日应变](@entry_id:170427) (Green-Lagrange Strain)**, $\mathbf{E}$：对应于 $m=2$ 的情况（忽略了常数因子 $1/2$）。其张量形式为 $\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})$。它的[主值](@entry_id:189577)为 $E_i = \frac{1}{2}(\lambda_i^2 - 1)$。
-   **[亨基应变](@entry_id:191329) (Hencky Strain) 或[对数应变](@entry_id:751438) (Logarithmic Strain)**, $\mathbf{E}^{\log}$：对应于 $m=0$ 的情况。其张量形式为 $\mathbf{E}^{\log} = \ln \mathbf{U}$。它的主值为 $E^{\log}_i = \ln \lambda_i$。
-   **工程应变 (Engineering Strain)**：在线性理论中，它近似于 $m=1$ 的 Biot 应变。

#### 不同应变测度的比较

虽然所有有限应变测度在小变形极限下都趋近于经典的[小应变张量](@entry_id:754968)，但它们在[大变形](@entry_id:167243)下的行为则显著不同。以[单轴拉伸](@entry_id:188287)为例，设轴向主拉伸为 $\lambda$，我们可以比较[格林-拉格朗日应变](@entry_id:170427)和[亨基应变](@entry_id:191329)的轴向分量 [@problem_id:3538133]：

$$
E_{11} = \frac{1}{2}(\lambda^2 - 1) \quad \text{vs.} \quad E^{\log}_{11} = \ln \lambda
$$

-   **小应变极限**：设 $\lambda = 1 + \varepsilon$，其中 $|\varepsilon| \ll 1$。通过[泰勒展开](@entry_id:145057)，我们发现 $E_{11} = \varepsilon + \frac{1}{2}\varepsilon^2$ 和 $E^{\log}_{11} = \varepsilon - \frac{1}{2}\varepsilon^2 + O(\varepsilon^3)$。两者的一阶项都是工程应变 $\varepsilon$，它们的差异是二阶小量 $\mathcal{O}(\varepsilon^2)$。这说明在小变形范围内，所有应变测度的选择几乎没有差别。
-   **[大应变](@entry_id:751152)极限**：当 $\lambda \to \infty$ 时，$E_{11}$ 随 $\lambda^2$ 增长，而 $E^{\log}_{11}$ 仅随 $\ln \lambda$ 增长。$E_{11}$ 的增长速度远快于 $E^{\log}_{11}$，两者的差异 $\Delta(\lambda) = E_{11} - E^{\log}_{11}$ 会随着 $\lambda$ 的增大而急剧增大。对于 $\lambda  1$ 的拉伸情况，$E_{11}$ 总是大于 $E^{\log}_{11}$。

[亨基应变](@entry_id:191329)（[对数应变](@entry_id:751438)）因其同轴可加性的优良特性而在[弹塑性](@entry_id:193198)理论中备受青睐。此外，它还有一个重要的性质，即其迹（trace）直接与体积应变的对数相关 [@problem_id:3538191]：

$$
\text{tr}(\mathbf{E}^{\log}) = \text{tr}(\ln \mathbf{U}) = \sum_i \ln \lambda_i = \ln(\prod_i \lambda_i) = \ln(\det \mathbf{U}) = \ln J
$$

这个简洁的关系使得变形的体积[部分和](@entry_id:162077)偏斜部分可以清晰地分离，这在模拟岩土材料等压力敏感材料时尤其有用。

### 变形率与[客观应力率](@entry_id:199282)

在许多计算力学问题中，特别是对于非弹性材料，我们更关心变形的“速率”，并在此基础上建立[本构关系](@entry_id:186508)。这需要引入[欧拉描述](@entry_id:264722)下的运动学量。

**速度梯度（velocity gradient）** $\mathbf{L}$ 定义为[空间速度](@entry_id:190294)场 $\mathbf{v}(\mathbf{x}, t)$ 对空间坐标 $\mathbf{x}$ 的梯度：

$$
\mathbf{L} = \nabla_{\mathbf{x}} \mathbf{v}
$$

[速度梯度](@entry_id:261686)可以被分解为其对称和反对称部分：

$$
\mathbf{L} = \mathbf{D} + \mathbf{W}
$$

-   **变形率张量（rate-of-deformation tensor）** $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^\top)$ 是 $\mathbf{L}$ 的对称部分，它描述了变形的速率，包括拉伸率和[剪切变形](@entry_id:170920)率。
-   **[自旋张量](@entry_id:187346)（spin tensor）** $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^\top)$ 是 $\mathbf{L}$ 的反对称部分，它描述了物质微元的平均[刚体转动](@entry_id:191086)[角速度](@entry_id:192539)。

这些欧拉率量与拉格朗日量之间存在着重要的运动学恒等式 [@problem_id:3538171]。例如，[速度梯度](@entry_id:261686)与变形梯度的时间导数（物质导数）$\dot{\mathbf{F}}$ 之间通过下式联系：

$$
\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}
$$

体积变化率也与变形率[张量的迹](@entry_id:190669)直接相关，这被称为欧拉膨胀公式：

$$
\frac{\dot{J}}{J} = \text{tr}(\mathbf{L}) = \text{tr}(\mathbf{D})
$$

在建立[大变形](@entry_id:167243)下的本构关系时，一个核心挑战是应力率的定义。简单的柯西应力 $\boldsymbol{\sigma}$ 的[物质时间导数](@entry_id:190892) $\dot{\boldsymbol{\sigma}}$ 并不是客观的，因为它会受到[刚体转动](@entry_id:191086)的影响。为了构建客观的[本构关系](@entry_id:186508)（例如 $\text{应力率} = f(\mathbf{D})$），必须使用 **[客观应力率](@entry_id:199282)（objective stress rate）**。

一个广泛使用的[客观应力率](@entry_id:199282)是 ** [Jaumann 率](@entry_id:185572)（Jaumann rate）**，定义为 [@problem_id:3538148]：

$$
\overset{\triangledown}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\mathbf{W} - \mathbf{W}\boldsymbol{\sigma}
$$

[Jaumann 率](@entry_id:185572)通过引入[自旋张量](@entry_id:187346) $\mathbf{W}$ 来修正[物质时间导数](@entry_id:190892)，从而抵消了[刚体转动](@entry_id:191086)的影响，使其成为一个客观量。然而，尽管 [Jaumann 率](@entry_id:185572)是客观的，但基于它的本构模型（即 hypoelastic 模型）存在一个严重缺陷：它通常不是 **功能共轭（work-conjugate）** 的。这意味着不存在一个可积的有限[应变能函数](@entry_id:178435)，使得基于 [Jaumann 率](@entry_id:185572)的[应力-应变关系](@entry_id:274093)能够从中导出。这导致此类模型可能是非保守的，即在封闭的变形循环中会产生或耗散虚假的能量。这一缺陷促使研究者发展了其他更复杂的、能够保证[能量守恒](@entry_id:140514)的本构框架。

### 在岩土力学中的应用：乘法[弹塑性](@entry_id:193198)

在描述岩土等材料的大塑性变形时，**乘法[弹塑性](@entry_id:193198)（multiplicative elastoplasticity）** 理论提供了一个强大的框架。其核心思想是将总变形梯度 $\mathbf{F}$ 分解为一个塑性部分 $\mathbf{F}_p$ 和一个弹性部分 $\mathbf{F}_e$ 的乘积 [@problem_id:3538167]：

$$
\mathbf{F} = \mathbf{F}_e \mathbf{F}_p
$$

这个分解引入了一个 **[中间构型](@entry_id:193000)（intermediate configuration）** 的概念。可以想象，这个构型是通过从当前构型中“[弹性卸载](@entry_id:748863)”掉所有应力而得到的。$\mathbf{F}_p$ 描述了从参考构型到这个假想的、无应力的[中间构型](@entry_id:193000)的变形，代表了材料内部已经发生的永久性、不可恢复的塑性流动。随后，$\mathbf{F}_e$ 描述了从这个[中间构型](@entry_id:193000)到最终承载应力的当前构型的弹性变形。

对于饱和土体，一个常见的简化假设是 **[塑性不可压缩性](@entry_id:183440)（plastic incompressibility）**，即塑性流动本身不引起体积变化。这在数学上表示为：

$$
\det \mathbf{F}_p = 1
$$

在这个假设下，总的体积变化完全由弹性变形贡献：$J = \det \mathbf{F} = \det(\mathbf{F}_e \mathbf{F}_p) = (\det \mathbf{F}_e)(\det \mathbf{F}_p) = \det \mathbf{F}_e$。这个看似简单的假设在岩土力学中具有深远的意义。它意味着，即使在不排水剪切这样总体积不变的变形过程中，由于剪切引起的塑性流动（$\det \mathbf{F}_p = 1$）仍然可以诱导弹性体积的改变（$\det \mathbf{F}_e \neq 1$）。这种弹性体积的变化正是通过改变[有效应力](@entry_id:198048)、进而导致[孔隙水压力](@entry_id:753587)变化来实现的。因此，[塑性不可压缩性](@entry_id:183440)假设成功地将塑性剪切与孔压响应和弹性[体积应变](@entry_id:267252)联系起来，构成了[临界状态土力学](@entry_id:748062)等现代本构理论的[运动学](@entry_id:173318)基础。