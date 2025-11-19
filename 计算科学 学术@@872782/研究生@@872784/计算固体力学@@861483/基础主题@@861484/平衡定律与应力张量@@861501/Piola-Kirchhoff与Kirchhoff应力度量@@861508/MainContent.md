## 引言
在[固体力学](@entry_id:164042)的研究中，应力是描述材料内部相互作用力的核心概念。对于小变形问题，直观的柯西（Cauchy）应力（单位变形后面积上的力）足以胜任。然而，当材料经历大位移、大转动或[大应变](@entry_id:751152)时，即进入有限变形领域，情况变得复杂起来。物体的形状、体积和方向都发生显著改变，使得在持续变化的“当前构型”上定义和使用物理量变得极为不便，尤其是在以固定“参考构型”为基础的数值计算（如[有限元法](@entry_id:749389)）中。这一挑战催生了对替代应力度量的需求，它们能够在不变的参考构型和变化的当前构型之间建立严谨的数学与物理联系。

本文旨在系统地阐明在有限变形理论中至关重要的几种应力度量，特别是皮奥拉-基尔霍夫（Piola-Kirchhoff）应力与基尔霍夫（Kirchhoff）应力。我们将深入探讨为何需要这些看似抽象的[应力张量](@entry_id:148973)，以及它们各自独特的物理意义和应用场景。通过学习本文，读者将能够清晰地辨析不同应力度量之间的差异与联系，并理解如何根据具体问题选择最合适的力学描述框架。

文章将分为三个核心部分。第一章“原理和机制”，将系统阐述柯西、基尔霍夫、第一及[第二皮奥拉-基尔霍夫应力](@entry_id:173163)的定义、数学关系、对称性以及它们背后的[功共轭](@entry_id:194957)原理。第二章“应用与跨学科联系”，将通过[计算固体力学](@entry_id:169583)、高等本构模型、[生物力学](@entry_id:153973)和[多尺度建模](@entry_id:154964)等实例，展示这些应力度量在解决前沿科学与工程问题中的强大功能。最后，在“动手实践”部分，精选的计算问题将引导读者将理论知识付诸实践，加深对这些关键概念的理解。

## 原理和机制

在连续介质力学中，为了描述物体在变形过程中的内部力状态，我们引入了应力张量的概念。然而，当处理有限变形问题时，单一的应力定义不足以应对所有情况。这是因为变形不仅改变了物体内部力的作用大小和方向，也改变了力作用的面积微元本身。因此，我们需要发展一套能够在不同构型（即变形前和变形后）之间转换的应力度量体系。本章将系统地介绍几种关键的应力度量，包括柯西（Cauchy）应力、第一和第二皮奥拉-基尔霍夫（Piola-Kirchhoff）应力以及基尔霍夫（Kirchhoff）应力，并阐明它们各自的物理意义、数学关系以及在不同理论和计算场景中的应用。

### 变形[运动学](@entry_id:173318)基础

在深入探讨应力之前，我们必须首先建立描述变形的运动学框架。一个连续体在某一初始时刻占据的空间区域被称为**参考构型**（reference configuration），记作 $\mathcal{B}_0$。此构型中的物[质点](@entry_id:186768)由其位置矢量 $\boldsymbol{X}$ 标识。经过一段时间的运动，在当前时刻 $t$，该连续体占据了**当前构型**（current configuration）$\mathcal{B}_t$，同一物质点的位置变为 $\boldsymbol{x}$。这个从参考构型到当前构型的映射关系由运动函数 $\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X}, t)$ 描述。

为了量化局部变形，我们引入**变形梯度**（deformation gradient）张量 $\boldsymbol{F}$，它定义为当前构型位置矢量 $\boldsymbol{x}$ 对参考构型位置矢量 $\boldsymbol{X}$ 的梯度：

$$
\boldsymbol{F} = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{X}}
$$

变形梯度 $\boldsymbol{F}$ 是一个[二阶张量](@entry_id:199780)，它将参考构型中的一个无穷小线元 $\mathrm{d}\boldsymbol{X}$ 映射到当前构型中的对应线元 $\mathrm{d}\boldsymbol{x}$，即 $\mathrm{d}\boldsymbol{x} = \boldsymbol{F} \mathrm{d}\boldsymbol{X}$。

与变形梯度密切相关的是**[雅可比行列式](@entry_id:137120)**（Jacobian determinant）$J$，定义为 $\boldsymbol{F}$ 的[行列式](@entry_id:142978)：

$$
J = \det(\boldsymbol{F})
$$

$J$ 的几何意义是局部体积变化的度量。参考构型中的一个无穷小体积微元 $\mathrm{d}V_0$ 在变形后变为当前构型中的体积微元 $\mathrm{d}V$，两者之间的关系为 $\mathrm{d}V = J \mathrm{d}V_0$ [@problem_id:3587940]。对于物理上可能的变形，物质不能穿透自身，因此必须满足 $J > 0$。根据[质量守恒定律](@entry_id:147377)，$\rho \mathrm{d}V = \rho_0 \mathrm{d}V_0$，其中 $\rho$ 和 $\rho_0$ 分别是当前构型和参考构型的质量密度。由此可得一个重要的关系式：$\rho J = \rho_0$ [@problem_id:3587975]。

### 当前构型中的应力度量：柯西应力与[基尔霍夫应力](@entry_id:751039)

最直观、物理意义最明确的应力是**柯西应力张量**（Cauchy stress tensor）$\boldsymbol{\sigma}$，它通常被称为“真实应力”。

-   **定义与性质**: 柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 完全定义在**当前构型**中。它通过柯西应力定理将作用在当前构型内任意一个[截面](@entry_id:154995)上的**真实[面力矢量](@entry_id:189429)**（traction vector）$\boldsymbol{t}$ 与该[截面](@entry_id:154995)的[单位法向量](@entry_id:178851) $\boldsymbol{n}$ 联系起来：
    $$
    \boldsymbol{t} = \boldsymbol{\sigma} \boldsymbol{n}
    $$
    这里的面力 $\boldsymbol{t}$ 是指单位**当前面积**上的力。在没有体力矩和耦合应力的情况下，动量矩平衡定律要求柯西[应力张量](@entry_id:148973)必须是**对称的**，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$ [@problem_id:3587937]。

尽管柯西应力物理意义清晰，但在以参考构型为基础进行数学描述（即[拉格朗日描述](@entry_id:264498)）的有限变形理论中，直接使用它会带来不便，因为 $\boldsymbol{\sigma}$ 和 $\boldsymbol{n}$ 都定义在不断变化的当前构型上。为了便于理论推导和数值计算，我们引入了[基尔霍夫应力](@entry_id:751039)张量。

**[基尔霍夫应力](@entry_id:751039)张量**（Kirchhoff stress tensor）$\boldsymbol{\tau}$ 同样是一个定义在**当前构型**中的[空间张量](@entry_id:185799)。它被定义为柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 与[雅可比行列式](@entry_id:137120) $J$ 的乘积：

$$
\boldsymbol{\tau} = J \boldsymbol{\sigma}
$$

-   **性质与物理诠释**: 由于 $J$ 是标量，$\boldsymbol{\sigma}$ 是对称的，因此 $\boldsymbol{\tau}$ 也是一个**[对称张量](@entry_id:148092)**。引入 $\boldsymbol{\tau}$ 的一个重要动机是它在[功能原理](@entry_id:172891)中的作用，我们将在后续章节详细讨论。此外，利用[质量守恒](@entry_id:204015)关系 $\rho J = \rho_0$，[基尔霍夫应力](@entry_id:751039)可以被赋予一个重要的物理诠释。将 $\boldsymbol{\tau} = J \boldsymbol{\sigma}$ 两边分别除以 $\rho_0$ 和 $\rho$，并利用 $J = \rho_0/\rho$，我们得到：
    $$
    \frac{\boldsymbol{\tau}}{\rho_0} = \frac{\boldsymbol{\sigma}}{\rho}
    $$
    此式表明，单位**参考质量**的[基尔霍夫应力](@entry_id:751039)等于单位**当前质量**的柯西应力。因此，$\boldsymbol{\tau}$ 可以被看作是一种考虑了体积变化的、与质量相关的应力度量 [@problem_id:3587975]。例如，在压缩过程中，$J  1$ 且 $\rho > \rho_0$，此时 $|\boldsymbol{\tau}|  |\boldsymbol{\sigma}|$。

### 参考构型中的应力度量：[皮奥拉-基尔霍夫应力](@entry_id:173629)

为了完全在不随时间变化的参考构型上建立控制方程，我们需要将应力的概念也“[拉回](@entry_id:160816)”到参考构型中。这便引出了[皮奥拉-基尔霍夫应力](@entry_id:173629)。

#### [第一皮奥拉-基尔霍夫应力](@entry_id:163971)

**[第一皮奥拉-基尔霍夫应力](@entry_id:163971)张量**（First Piola-Kirchhoff stress tensor）$\boldsymbol{P}$，也称为**名义应力**（nominal stress），是一个“两点张量”（two-point tensor）。

-   **定义**: $\boldsymbol{P}$ 将作用于参考构型中面积微元 $\mathrm{d}A_0$ 上的**名义[面力矢量](@entry_id:189429)** $\boldsymbol{t}_0$ 与该面积微元的[单位法向量](@entry_id:178851) $\boldsymbol{N}$ 联系起来。注意，这里的力矢量 $\mathrm{d}\boldsymbol{f} = \boldsymbol{t}_0 \mathrm{d}A_0$ 仍然是作用在当前构型上的真实物理力。$\boldsymbol{P}$ 的定义式为：
    $$
    \boldsymbol{t}_0 = \boldsymbol{P} \boldsymbol{N}
    $$
    其中 $\boldsymbol{t}_0$ 是单位**参考面积**上的力。通过力的等效性原则 $\mathrm{d}\boldsymbol{f} = \boldsymbol{t} \mathrm{d}A = \boldsymbol{t}_0 \mathrm{d}A_0$ 和面积微元之间的转换关系——[南森公式](@entry_id:195566)（Nanson's formula）$\boldsymbol{n} \mathrm{d}A = J \boldsymbol{F}^{-T} \boldsymbol{N} \mathrm{d}A_0$，可以推导出 $\boldsymbol{P}$ 与 $\boldsymbol{\sigma}$ 之间的关系 [@problem_id:3587940] [@problem_id:3587945]：
    $$
    \boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-T}
    $$
    结合[基尔霍夫应力](@entry_id:751039)的定义，上式也可以写为 $\boldsymbol{P} = \boldsymbol{\tau} \boldsymbol{F}^{-T}$，这进一步揭示了 $\boldsymbol{\tau} = \boldsymbol{P} \boldsymbol{F}^T$ [@problem_id:3587975]。

-   **对称性**: $\boldsymbol{P}$ 通常是**非对称的**。即使 $\boldsymbol{\sigma}$ 是对称的，由于 $\boldsymbol{F}^{-T}$ 的存在，乘积 $J \boldsymbol{\sigma} \boldsymbol{F}^{-T}$ 一般不具有对称性。动量矩平衡在参考构型中的表达形式是 $\boldsymbol{P} \boldsymbol{F}^T = (\boldsymbol{P} \boldsymbol{F}^T)^T$，这等价于 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$，但它并不要求 $\boldsymbol{P}$ 本身是对称的 [@problem_id:3587937] [@problem_id:3588008]。

-   **在[动量平衡](@entry_id:193575)方程中的作用**: $\boldsymbol{P}$ 的一个核心应用是构建参考构型下的[动量平衡](@entry_id:193575)方程（即[拉格朗日形式](@entry_id:145697)的[运动方程](@entry_id:170720)）。其强形式为：
    $$
    \mathrm{Div}(\boldsymbol{P}) + \rho_0 \boldsymbol{b} = \rho_0 \boldsymbol{a}
    $$
    其中 $\mathrm{Div}(\cdot)$ 是在参考构型[坐标系](@entry_id:156346) $\boldsymbol{X}$ 下的[散度算子](@entry_id:265975)。这个方程之所以使用 $\boldsymbol{P}$，是因为它是从当前构型中的柯西应力通过严格的[积分变换](@entry_id:186209)自然推导出的结果 [@problem_id:3587952]。

#### [第二皮奥拉-基尔霍夫应力](@entry_id:173163)

$\boldsymbol{P}$ 的非对称性在构建[本构关系](@entry_id:186508)时会带来不便，因为描述材料应变状态的应变张量（如[格林-拉格朗日应变张量](@entry_id:187745)）通常是对称的。为了得到一个与对称[应变度量](@entry_id:755495)共轭的、定义在参考构型上的对称应力度量，我们引入了**[第二皮奥拉-基尔霍夫应力](@entry_id:173163)张量**（Second Piola-Kirchhoff stress tensor）$\boldsymbol{S}$。

-   **定义**: $\boldsymbol{S}$ 是一个纯粹的**[材料张量](@entry_id:196294)**，它通过将 $\boldsymbol{P}$ 张量从当前构型“[拉回](@entry_id:160816)”到参考构型来定义：
    $$
    \boldsymbol{S} = \boldsymbol{F}^{-1} \boldsymbol{P}
    $$
    将 $\boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-T}$ 代入，可得 $\boldsymbol{S}$ 与 $\boldsymbol{\sigma}$ 的关系：
    $$
    \boldsymbol{S} = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-T}
    $$
    这个操作被称为**回拉**（pull-back）。反之，从 $\boldsymbol{S}$ 得到 $\boldsymbol{\sigma}$ 的操作 $\boldsymbol{\sigma} = \frac{1}{J} \boldsymbol{F} \boldsymbol{S} \boldsymbol{F}^T$ 则被称为**[前推](@entry_id:158718)**（push-forward） [@problem_id:3587994]。

-   **对称性**: 如果柯西应力 $\boldsymbol{\sigma}$ 是对称的，那么[第二皮奥拉-基尔霍夫应力](@entry_id:173163) $\boldsymbol{S}$ **也必然是对称的**。这可以通过其定义式 $(J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-T})^T$ 直接验证 [@problem_id:3587937] [@problem_id:3588008]。$\boldsymbol{S}$ 的对称性使其成为与对称的[格林-拉格朗日应变张量](@entry_id:187745) $\boldsymbol{E}$ 进行[本构建模](@entry_id:183370)的理想选择。

-   **在理论中的作用**: $\boldsymbol{S}$ 本身没有直接的、像柯西应力那样的物理图像（例如，它不直接与某个面上的力相关）。它的主要价值在于理论和计算层面。对于[超弹性材料](@entry_id:190241)，[应变能密度函数](@entry_id:755490) $W$ 通常表示为[应变度量](@entry_id:755495)（如[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}=\boldsymbol{F}^T\boldsymbol{F}$）的函数，而 $\boldsymbol{S}$ 可以直接通过对 $W$ 求导得到：$\boldsymbol{S} = 2 \frac{\partial W}{\partial \boldsymbol{C}}$ [@problem_id:3587952]。此外，$\boldsymbol{S}$ 在[虚功原理](@entry_id:138749)的弱形式表述中扮演着核心角色，这使其在有限元方法的实现中至关重要。

### [功共轭](@entry_id:194957)原理与功率等价性

不同应力度量之间的关系不仅仅是数学上的[坐标变换](@entry_id:172727)，其背后有着深刻的物理原理——功率等价性。该原理指出，内力在变形过程中所做的功率（即[应力功率](@entry_id:182907)）是一个不依赖于观察者或数学描述（拉格朗日或欧拉）的客观物理量。

内[功率密度](@entry_id:194407)（单位体积的功率）可以通过特定应力度量与一个与之**[功共轭](@entry_id:194957)**（work-conjugate）的应变率度量的缩并（[双点积](@entry_id:748648)）来计算。

-   **基本关系**: 在当前构型中，单位**当前体积**的[应力功率](@entry_id:182907)是 $\boldsymbol{\sigma}:\boldsymbol{d}$，其中 $\boldsymbol{d} = \frac{1}{2}(\nabla_{\boldsymbol{x}}\boldsymbol{v} + (\nabla_{\boldsymbol{x}}\boldsymbol{v})^T)$ 是变形率张量。
-   物体的总内功率为 $\mathcal{P}_{int} = \int_{\mathcal{B}_t} \boldsymbol{\sigma}:\boldsymbol{d} \, \mathrm{d}V$。将此[积分变换](@entry_id:186209)到参考构型上，我们得到：
    $$
    \mathcal{P}_{int} = \int_{\mathcal{B}_0} (\boldsymbol{\sigma}:\boldsymbol{d}) J \, \mathrm{d}V_0 = \int_{\mathcal{B}_0} (J \boldsymbol{\sigma}):\boldsymbol{d} \, \mathrm{d}V_0 = \int_{\mathcal{B}_0} \boldsymbol{\tau}:\boldsymbol{d} \, \mathrm{d}V_0
    $$
    这表明，$(\boldsymbol{\tau}, \boldsymbol{d})$ 是一对[功共轭](@entry_id:194957)的量，其缩并给出单位**参考体积**的[应力功率](@entry_id:182907) [@problem_id:3587975]。

通过进一步的运动学推导，可以证明以下[功共轭](@entry_id:194957)关系，它们计算的都是单位**参考体积**的[应力功率](@entry_id:182907)，并且在数值上是等价的 [@problem_id:3587984] [@problem_id:3587932]：

$$
\text{应力功率密度} = \boldsymbol{\tau}:\boldsymbol{d} = \boldsymbol{P}:\dot{\boldsymbol{F}} = \boldsymbol{S}:\dot{\boldsymbol{E}}
$$

其中 $\dot{\boldsymbol{F}}$ 是变形梯度的[物质时间导数](@entry_id:190892)，$\dot{\boldsymbol{E}}$ 是[格林-拉格朗日应变张量](@entry_id:187745) $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C}-\boldsymbol{I})$ 的[物质时间导数](@entry_id:190892)。这组等式是有限变形力学的核心，它不仅揭示了不同应力-[应变率](@entry_id:154778)对之间的深刻联系，也为推导它们之间的转换关系提供了物理基础 [@problem_id:3587994] [@problem_id:3588008]。例如，从 $\boldsymbol{S}:\dot{\boldsymbol{E}} = \boldsymbol{\tau}:\boldsymbol{d}$ 出发，利用[运动学](@entry_id:173318)关系 $\dot{\boldsymbol{E}} = \boldsymbol{F}^T \boldsymbol{d} \boldsymbol{F}$，可以直接推导出 $\boldsymbol{\tau} = \boldsymbol{F} \boldsymbol{S} \boldsymbol{F}^T$。

### 客观性与材料无差异性

所有本构关系和物理量都必须满足**材料无差异性原理**（principle of material frame-indifference），也称**客观性**（objectivity）。该原理要求材料的响应不应依赖于观察者的刚体运动。对于应力度量，这意味着施加一个纯[刚体转动](@entry_id:191086)不应在初始无应力的各向同性材料中产生任何应力。

考虑一个纯[刚体转动](@entry_id:191086) $\boldsymbol{x} = \boldsymbol{Q}\boldsymbol{X}$，其中 $\boldsymbol{Q}$ 是一个正常交张量（$\boldsymbol{Q}^T\boldsymbol{Q}=\boldsymbol{I}, \det\boldsymbol{Q}=1$）。在此情况下，变形梯度 $\boldsymbol{F}=\boldsymbol{Q}$，雅可比行列式 $J=1$，[右柯西-格林张量](@entry_id:174156) $\boldsymbol{C}=\boldsymbol{F}^T\boldsymbol{F}=\boldsymbol{Q}^T\boldsymbol{Q}=\boldsymbol{I}$。由于 $\boldsymbol{C}=\boldsymbol{I}$，材料在变形度量上与参考构型完全相同。对于一个依赖于 $\boldsymbol{C}$ 的各向同性[应变能函数](@entry_id:178435)（如 [@problem_id:3587938] 中给出的），当 $\boldsymbol{C}=\boldsymbol{I}$ 且 $J=1$ 时，计算出的[第二皮奥拉-基尔霍夫应力](@entry_id:173163) $\boldsymbol{S}$ 必为零。进而，通过变换关系，$\boldsymbol{P}$, $\boldsymbol{\tau}$ 和 $\boldsymbol{\sigma}$ 也都为零。这验证了这些应力度量及其本构关系满足客观性要求。

### 总结与在[计算力学](@entry_id:174464)中的应用

下表总结了本章讨论的四种核心[应力张量](@entry_id:148973)的关键特性：

| 应力张量 | 符号 | 定义构型 | 对称性 | [功共轭](@entry_id:194957)应变率 | 主要应用 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 柯西应力 | $\boldsymbol{\sigma}$ | 当前 (欧拉) | 是 | $\boldsymbol{d}$ | 物理诠释，[流体力学](@entry_id:136788) |
| [基尔霍夫应力](@entry_id:751039) | $\boldsymbol{\tau}$ | 当前 (欧拉) | 是 | $\boldsymbol{d}$ | [弹塑性](@entry_id:193198)理论，功率关系 |
| [第一皮奥拉-基尔霍夫应力](@entry_id:163971) | $\boldsymbol{P}$ | 参考 (拉格朗日) | 否 | $\dot{\boldsymbol{F}}$ | 拉格朗日[动量方程](@entry_id:197225)的强形式 |
| [第二皮奥拉-基尔霍夫应力](@entry_id:173163) | $\boldsymbol{S}$ | 参考 (拉格朗日) | 是 | $\dot{\boldsymbol{E}}$ | [超弹性](@entry_id:159356)本构律，弱形式 (有限元) |

在**[计算固体力学](@entry_id:169583)**中，这些应力度量各司其职。当采用基于参考构型的[拉格朗日描述](@entry_id:264498)时（这是大多数固体力学有限元程序的基础）：
- **$\boldsymbol{S}$ 张量**是核心，因为它与对称的[格林-拉格朗日应变](@entry_id:170427) $\boldsymbol{E}$ [功共轭](@entry_id:194957)，使得从[应变能函数](@entry_id:178435)推导本构关系变得简洁明了 [@problem_id:3587952]。
- [虚功原理](@entry_id:138749)的离散化形式通常表示为 $\boldsymbol{S}$ 和 $\delta\boldsymbol{E}$ 的积分，从而形成[单元刚度矩阵](@entry_id:139369)。
- **$\boldsymbol{P}$ 张量**虽然在推导和理论分析中不可或缺（尤其是在建立动量方程的强形式时），但在标准的位移有限元实现中其作用不那么直接。
- **$\boldsymbol{\sigma}$ 张量**通常作为最终的输出结果，因为它具有最清晰的物理意义，便于工程师理解和进行强度校核。
- **$\boldsymbol{\tau}$ 张量**在某些高级本构模型（如有限变形塑性）和理论推导中非常有用，因为它巧妙地联系了欧拉和[拉格朗日描述](@entry_id:264498)中的功率表达式。

理解这些应力度量之间的精确关系以及它们各自的适用场景，是掌握和应用[非线性](@entry_id:637147)连续介质力学的关键。