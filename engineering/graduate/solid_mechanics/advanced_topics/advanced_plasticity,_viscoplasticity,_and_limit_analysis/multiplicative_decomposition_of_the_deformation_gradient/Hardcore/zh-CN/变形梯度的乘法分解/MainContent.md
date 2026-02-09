## 引言
在固体力学领域，精确描述材料在经历大变形时的复杂行为是一个核心挑战。当材料同时表现出可恢复的弹性变形和永久的塑性变形时，小应变理论中简单的应变加法分解（$\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}_{\mathrm{e}} + \boldsymbol{\varepsilon}_{\mathrm{p}}$）由于忽略了几何非线性而不再适用。这一局限性催生了对一个更基本、更普适的运动学框架的需求，以正确处理有限应变和有限转动下的弹塑性耦合问题。变形梯度的乘法分解（$\boldsymbol{F} = \boldsymbol{F}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{p}}$）正是为解决这一难题而提出的核心理论。它为有限应变塑性力学提供了坚实的理论基石，通过引入一个概念性的“中间构型”，从物理上清晰地分离了变形中的弹性与塑性部分。

本文将系统地引导读者深入理解这一关键理论。在“原理与机制”一章中，我们将探讨乘法分解的运动学基础、热力学推论以及其对本构模型构建的深远影响。接着，在“应用与交叉学科联系”一章中，我们将展示该理论如何跨越材料科学、计算力学乃至生物力学的界限，成为解决前沿工程与科学问题的有力工具。最后，通过“动手实践”中的具体问题，读者将有机会巩固所学，将抽象的理论应用于实际的力学分析中。

## 原理与机制

在有限应变理论中，为了描述兼具弹性和塑性行为的材料，必须建立一个能够清晰分离可恢复变形和永久变形的运动学框架。与仅适用于微小位移和转动的小应变理论中应变可直接进行加法分解不同，当材料经历大变形或大转动时，其几何非线性效应使得简单的加法分解不再成立。本章将深入探讨有限应变塑性理论的基石——变形梯度的乘法分解，系统阐述其核心原理、运动学推论以及在本构模型构建中的关键作用。

### 变形梯度的运动学分解：极分解

在深入探讨弹塑性分解之前，我们首先回顾一个纯粹的运动学概念——**极分解 (polar decomposition)**。任何一个可逆的变形梯度张量 $\boldsymbol{F}$（即雅可比行列式 $J = \det \boldsymbol{F} > 0$），都可以被唯一地分解为一个旋转张量和一个纯拉伸张量的乘积。这存在两种形式：

1.  **右极分解 (Right Polar Decomposition):** $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$
2.  **左极分解 (Left Polar Decomposition):** $\boldsymbol{F} = \boldsymbol{V}\boldsymbol{R}$

在这里，$\boldsymbol{R}$ 是一个真正交张量（$\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R} = \boldsymbol{I}$, $\det \boldsymbol{R} = +1$），代表了物质微元的**刚体旋转 (rigid body rotation)**。$\boldsymbol{U}$ 和 $\boldsymbol{V}$ 均为对称正定张量，分别称为**右拉伸张量 (right stretch tensor)** 和**左拉伸张量 (left stretch tensor)**。它们描述了变形中的纯拉伸部分，其特征值即为主拉伸比 $\lambda_i$。

右拉伸张量 $\boldsymbol{U}$ 与**右柯西-格林变形张量 (right Cauchy-Green deformation tensor)** $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$ 直接相关，具体为 $\boldsymbol{U} = \sqrt{\boldsymbol{C}}$。由于 $\boldsymbol{C}$ 完全由变形后的长度平方与初始长度平方之比确定，它及其平方根 $\boldsymbol{U}$ 都是在参考构型中定义的量，且不受叠加在当前构型上的任何刚体转动的影响，即它们是**客观的 (objective)**。相反，左拉伸张量 $\boldsymbol{V} = \sqrt{\boldsymbol{B}}$，其中 $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\mathsf{T}}$ 是**左柯西-格林变形张量 (left Cauchy-Green or Finger tensor)**，它是在当前（空间）构型中定义的。[@problem_id:2663646] [@problem_id:2663676]

必须强调，极分解是一个纯粹的数学和运动学工具，它将任何变形分解为“拉伸”和“旋转”两个几何操作。然而，它并未区分变形的物理性质，即哪些是弹性的，哪些是塑性的。例如，一个纯剪切变形，在物理上可能完全是塑性的，但其极分解仍然会得到一个旋转分量 $\boldsymbol{R}$ 和一个拉伸分量 $\boldsymbol{U}$。因此，极分解不能直接用于建立弹塑性本构关系。[@problem_id:2663676]

### 弹塑性乘法分解的基本假设

为了从物理上分离弹性和塑性效应，E. H. Lee 等人提出了变形梯度乘法分解的核心思想。该理论假设总的变形过程可以概念性地分解为两个连续的映射：

$\boldsymbol{F} = \boldsymbol{F}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{p}}$

这里，$\boldsymbol{F}_{\mathrm{p}}$ 是**塑性变形梯度 (plastic part of the deformation gradient)**，它将物质微元从初始的**参考构型 (reference configuration)** 映射到一个假想的、局部的**中间构型 (intermediate configuration)**。这个映射过程代表了材料内部发生的永久性、不可恢复的变形，如晶体中的位错滑移。

$\boldsymbol{F}_{\mathrm{e}}$ 则是**弹性变形梯度 (elastic part of the deformation gradient)**，它接着将物质微元从中间构型映射到最终的**当前构型 (current configuration)**。这个映射代表了材料的可恢复弹性变形，例如原子晶格的拉伸和扭曲。

这个中间构型是乘法分解理论的核心。它被构想为一个通过局部“卸载”除去所有弹性应力后达到的状态。因此，中间构型是一个**局部无应力 (locally stress-free)** 的状态。总变形 $\boldsymbol{F}$ 就是这两个过程的复合，根据复合函数求导的链式法则，其梯度自然地表现为乘积形式。[@problem_id:2663674]

这种乘法形式与小应变理论中应变张量的加法分解 $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}_{\mathrm{e}} + \boldsymbol{\varepsilon}_{\mathrm{p}}$ 形成鲜明对比。加法分解是有限应变理论在位移梯度极小的假设下线性化的结果。当变形或转动变得显著时，几何非线性凸显，加法分解失效。乘法分解正是为了在有限应变和有限转动框架下正确描述弹塑性耦合而提出的。例如，在金属成型等工艺中，塑性应变和材料转动可能非常大，而弹性应变（晶格畸变）始终保持在很小的范围内。乘法分解框架能够精确地处理这种情况。[@problem_id:2663648]

### 中间构型的性质与推论

中间构型作为一个理论构造，其独特的性质引出了一系列重要的物理和数学推论。

#### 体积变化与塑性不可压缩性

变形梯度的行列式 $J = \det \boldsymbol{F}$ 描述了体积的变化率。根据行列式的乘法性质，我们有：
$J = \det(\boldsymbol{F}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{p}}) = (\det \boldsymbol{F}_{\mathrm{e}})(\det \boldsymbol{F}_{\mathrm{p}}) = J_{\mathrm{e}} J_{\mathrm{p}}$
其中 $J_{\mathrm{e}}$ 和 $J_{\mathrm{p}}$ 分别是弹性体积变化率和塑性体积变化率。[@problem_id:2663674]

对于金属等晶体材料，塑性变形主要由位错滑移等剪切机制主导，这些机制在很大程度上是保持体积的。因此，一个普遍且非常精确的假设是**塑性不可压缩性 (plastic incompressibility)**，即塑性变形过程不改变体积。数学上表示为：
$J_{\mathrm{p}} = \det \boldsymbol{F}_{\mathrm{p}} = 1$
在这一假设下，总的体积变化完全由弹性变形引起，即 $J = J_{\mathrm{e}}$。这一结论极大地简化了本构模型的建立。其率形式的推论是，塑性应变率张量 $\boldsymbol{D}_{\mathrm{p}}$ 的迹为零，即 $\operatorname{tr}(\boldsymbol{D}_{\mathrm{p}}) = 0$。[@problem_id:2649689]

#### 不相容性与几何必需位错

如果一个张量场是某个向量场（位移场）的梯度，那么它的旋度必须为零。然而，塑性变形梯度 $\boldsymbol{F}_{\mathrm{p}}$ 一般不满足这个条件。也就是说，$\boldsymbol{F}_{\mathrm{p}}$ 场通常是**不相容的 (incompatible)**：
$\operatorname{Curl}(\boldsymbol{F}_{\mathrm{p}}) \neq \mathbf{0}$
这意味着，通常不存在一个全局、连续的位移函数 $\boldsymbol{\chi}_{\mathrm{p}}(\mathbf{X})$ 使得 $\boldsymbol{F}_{\mathrm{p}} = \nabla_{\mathbf{X}} \boldsymbol{\chi}_{\mathrm{p}}$。其物理意义是，由于材料内部微观缺陷（如位错）的非均匀分布，将一个连续体进行塑性变形后，即使局部都达到了无应力状态，也无法将这些局部微元 "无缝" 地拼回成一个连续的宏观物体。这个假想的中间构型在欧几里得空间中是“破损”的，存在间隙或重叠。[@problem_id:2663674] [@problem_id:2663648]

这种不相容性与材料科学中的**几何必需位错 (Geometrically Necessary Dislocations, GNDs)** 密度直接相关。GNDs 是为协调晶格变形的非均匀性所必需的位错。连续介质位错理论将GND密度张量 $\boldsymbol{\alpha}$ （定义在中间构型上）与 $\boldsymbol{F}_{\mathrm{p}}$ 的不相容性联系起来。通过斯托克斯定理，可以证明一个闭合回路的**伯格斯矢量 (Burgers vector)** $\widetilde{\mathbf{b}}$ 等于穿过该回路的曲面上GND通量的积分，也等于 $\boldsymbol{F}_{\mathrm{p}}$ 旋度的积分。一个关键的关系式将它们联系起来：
$\boldsymbol{\alpha} = - J_{\mathrm{p}}^{-1} \boldsymbol{F}_{\mathrm{p}} \operatorname{Curl}(\boldsymbol{F}_{\mathrm{p}})$
（注：此处的负号和具体形式取决于旋度和 $\boldsymbol{\alpha}$ 的定义约定。）这揭示了连续介质力学中的宏观运动学量与微观晶体缺陷之间的深刻联系。[@problem_id:2663666]

#### 非唯一性与规范自由度

中间构型的定义存在固有的模糊性，即其空间方位是任意的。对于任意一个与时间相关的旋转张量 $\boldsymbol{Q}(t) \in \mathrm{SO}(3)$，我们可以定义一组新的弹塑性分解：
$\boldsymbol{F}_{\mathrm{e}}^{\star} = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}}$
$\boldsymbol{F}_{\mathrm{p}}^{\star} = \boldsymbol{Q}\boldsymbol{F}_{\mathrm{p}}$
不难验证，这组新的分解给出了与原来完全相同的总变形梯度 $\boldsymbol{F} = \boldsymbol{F}_{\mathrm{e}}^{\star}\boldsymbol{F}_{\mathrm{p}}^{\star}$。[@problem_id:2663647]

这种可以任意旋转中间构型而不影响总变形的自由度被称为**规范自由度 (gauge freedom)**。这一特性对本构理论有重要影响。我们考察一些关键的弹性应变度量在该变换下的行为：
- 弹性右柯西-格林张量：$\boldsymbol{C}_{\mathrm{e}}^{\star} = (\boldsymbol{F}_{\mathrm{e}}^{\star})^{\mathsf{T}}\boldsymbol{F}_{\mathrm{e}}^{\star} = \boldsymbol{Q}\boldsymbol{C}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}}$。它会跟随着旋转。
- 弹性左柯西-格林张量：$\boldsymbol{b}_{\mathrm{e}}^{\star} = \boldsymbol{F}_{\mathrm{e}}^{\star}(\boldsymbol{F}_{\mathrm{e}}^{\star})^{\mathsf{T}} = \boldsymbol{b}_{\mathrm{e}}$。它在此变换下保持不变。

这意味着，如果材料的弹性响应是**各向同性的 (isotropic)**，其储存的能量 $\psi$ 仅依赖于 $\boldsymbol{C}_{\mathrm{e}}$ 或 $\boldsymbol{b}_{\mathrm{e}}$ 的标量不变量（例如主应变）。由于标量不变量在正交变换下不变 ($I_k(\boldsymbol{C}_{\mathrm{e}}^{\star}) = I_k(\boldsymbol{C}_{\mathrm{e}})$），因此各向同性材料的本构关系天然地对中间构型的旋转不敏感，即具有**规范不变性 (gauge invariance)**。

然而，对于**各向异性 (anisotropic)** 材料（如单晶或织构材料），其弹性储能函数可能依赖于 $\boldsymbol{C}_{\mathrm{e}}$ 和定义在中间构型中的某些结构张量（如晶格方向）。在这种情况下，为了保证物理定律的客观性，必须明确如何处理这种规范自由度。一种方法是引入一个额外的演化方程来确定中间构型的方位，或者选择一个特定的约定（例如，要求 $\boldsymbol{F}_{\mathrm{p}}$ 的旋转部分为单位张量）来固定这个规范。[@problem_id:2663647]

### 本构关系与应力度量

乘法分解为建立有限应变下的弹塑性本构关系提供了理想的框架。

#### 弹性响应与热力学框架

热力学第二定律要求塑性变形过程必须是耗散的。这通过假设材料的**亥姆霍兹自由能 (Helmholtz free energy)** $\psi$ 仅是弹性状态的函数来实现。为了满足**材料客观性原理 (principle of material frame-indifference)**，即本构关系不应依赖于观察者的刚体运动，$\psi$ 必须是一个纯弹性应变度量的函数。标准选择是弹性右柯西-格林张量 $\boldsymbol{C}_{\mathrm{e}}$：
$\psi = \hat{\psi}(\boldsymbol{C}_{\mathrm{e}})$
其中 $\boldsymbol{C}_{\mathrm{e}} = \boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}\boldsymbol{F}_{\mathrm{e}}$。由于 $\boldsymbol{C}_{\mathrm{e}}$ 不受叠加在当前构型上的刚体转动的影响，这种形式的储能函数自动保证了客观性。[@problem_id:2663674] [@problem_id:2663676]

#### 应力张量的定义与推导

在超弹性理论中，应力是储能函数对应变度量的导数。在弹塑性框架下，所有应力都源于弹性变形。我们首先定义与 $\boldsymbol{C}_{\mathrm{e}}$ 共轭的应力度量，即**弹性第二Piola-Kirchhoff (PK2) 应力 (elastic Second Piola-Kirchhoff stress)** $\boldsymbol{S}_{\mathrm{e}}$，它作用在中间构型上：
$\boldsymbol{S}_{\mathrm{e}} = 2 \frac{\partial \psi}{\partial \boldsymbol{C}_{\mathrm{e}}}$

从 $\boldsymbol{S}_{\mathrm{e}}$ 出发，可以通过标准的推拉操作 (push-forward and pull-back) 得到其他常用的应力张量：
- **Kirchhoff应力 ($\boldsymbol{\tau}$):** 它是 $\boldsymbol{S}_{\mathrm{e}}$ 通过弹性映射 $\boldsymbol{F}_{\mathrm{e}}$ push-forward到当前构型的结果，是描述当前构型应力状态的能量共轭量。
  $\boldsymbol{\tau} = \boldsymbol{F}_{\mathrm{e}} \boldsymbol{S}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}$
- **Cauchy应力 ($\boldsymbol{\sigma}$):** 这是物理上“真实”的应力，即单位当前面积上的力。它与Kirchhoff应力的关系为：
  $\boldsymbol{\sigma} = J^{-1} \boldsymbol{\tau}$
- **第一Piola-Kirchhoff (PK1) 应力 ($\boldsymbol{P}$):** 它将参考构型中的力与当前构型的面积联系起来，其与 $\boldsymbol{\tau}$ 的关系为 $\boldsymbol{P} = \boldsymbol{\tau} \boldsymbol{F}^{-\mathsf{T}}$。代入 $\boldsymbol{\tau}$ 和 $\boldsymbol{F}$ 的分解，可得其在弹塑性框架下的表达式：
  $\boldsymbol{P} = \boldsymbol{F}_{\mathrm{e}} \boldsymbol{S}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{p}}^{-\mathsf{T}}$

这一套关系式清晰地展示了所有宏观应力如何由弹性变形 $\boldsymbol{F}_{\mathrm{e}}$ 和储能函数 $\psi(\boldsymbol{C}_{\mathrm{e}})$ 唯一确定。[@problem_id:2663649]

#### 塑性流动的驱动力：Mandel应力

塑性流动（即 $\boldsymbol{F}_{\mathrm{p}}$ 的演化）需要一个“驱动力”。根据热力学一致性，这个驱动力应该是与塑性应变率共轭的应力度量。通过分析塑性耗散功率 $\mathcal{D}_{\mathrm{p}}$，可以找到这个应力。从Clausius-Duhem不等式出发，可以推导出塑性耗散（单位参考体积）为：
$\mathcal{D}_{\mathrm{p}} = \boldsymbol{P}:\dot{\boldsymbol{F}} - \dot{\psi} \ge 0$

经过一系列推导，可以证明该耗散功率在中间构型中可以表达为一个应力度量和一个应变率度量的内积。定义**塑性速度梯度 (plastic velocity gradient)** 为 $\boldsymbol{L}_{\mathrm{p}} = \dot{\boldsymbol{F}}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{p}}^{-1}$，其对称部分为塑性应变率 $\boldsymbol{D}_{\mathrm{p}}$。最终可得：
$\mathcal{D}_{\mathrm{p}} = \boldsymbol{M}:\boldsymbol{L}_{\mathrm{p}}$
其中 $\boldsymbol{M} = \boldsymbol{C}_{\mathrm{e}}\boldsymbol{S}_{\mathrm{e}}$ 被称为**Mandel应力 (Mandel stress)**。

Mandel应力 $\boldsymbol{M}$ 是在中间构型中定义的应力张量，它与塑性速度梯度 $\boldsymbol{L}_{\mathrm{p}}$ (或在特定情况下与 $\boldsymbol{D}_{\mathrm{p}}$) 形成能量共轭对。因此，$\boldsymbol{M}$ 是驱动塑性流动的正确热力学力。塑性流动法则，如屈服准则和流动方向，理应表示为Mandel应力的函数。[@problem_id:2663673]

### 运动学率形式与自旋分解

为了发展率相关的塑性理论，我们需要分析变形梯度的演化率。

#### 速度梯度的分解

对乘法分解式 $\boldsymbol{F} = \boldsymbol{F}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{p}}$ 求时间导数，并经过变换，可以得到空间**速度梯度 (velocity gradient)** $\boldsymbol{L} = \dot{\boldsymbol{F}}\boldsymbol{F}^{-1}$ 的加法分解：
$\boldsymbol{L} = \boldsymbol{L}_{\mathrm{e}} + \boldsymbol{F}_{\mathrm{e}} \boldsymbol{L}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{e}}^{-1}$
其中，$\boldsymbol{L}_{\mathrm{e}} = \dot{\boldsymbol{F}}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{e}}^{-1}$ 是弹性速度梯度，$\boldsymbol{L}_{\mathrm{p}} = \dot{\boldsymbol{F}}_{\mathrm{p}}\boldsymbol{F}_{\mathrm{p}}^{-1}$ 是在中间构型中定义的塑性速度梯度。上式表明，总的空间速度梯度是弹性部分与从中间构型push-forward到当前构型的塑性部分之和。[@problem_id:2649689]

将速度梯度分解为对称和反对称部分，即**应变率张量 (rate of deformation tensor)** $\boldsymbol{D} = \operatorname{sym}(\boldsymbol{L})$ 和**自旋张量 (spin tensor)** $\boldsymbol{W} = \operatorname{skew}(\boldsymbol{L})$，我们得到：
$\boldsymbol{D} = \boldsymbol{D}_{\mathrm{e}} + \operatorname{sym}(\boldsymbol{F}_{\mathrm{e}} \boldsymbol{L}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{e}}^{-1})$
$\boldsymbol{W} = \boldsymbol{W}_{\mathrm{e}} + \operatorname{skew}(\boldsymbol{F}_{\mathrm{e}} \boldsymbol{L}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{e}}^{-1})$
其中 $\boldsymbol{D}_{\mathrm{e}}$ 和 $\boldsymbol{W}_{\mathrm{e}}$ 分别是弹性应变率和弹性自旋。

#### 晶格旋转、弹性自旋与塑性自旋

在晶体塑性理论中，一个关键问题是晶格的方位如何随变形演化。晶格方位由弹性变形梯度 $\boldsymbol{F}_{\mathrm{e}}$ 的旋转部分 $\boldsymbol{R}_{\mathrm{e}}$（来自其极分解 $\boldsymbol{F}_{\mathrm{e}} = \boldsymbol{R}_{\mathrm{e}}\boldsymbol{U}_{\mathrm{e}}$）来描述。晶格的旋转速率由反对称张量 $\dot{\boldsymbol{R}}_{\mathrm{e}}\boldsymbol{R}_{\mathrm{e}}^{\mathsf{T}}$ 给出。

通过对 $\boldsymbol{L}_{\mathrm{e}} = \dot{\boldsymbol{F}}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{e}}^{-1}$ 进行分解，可以推导出**晶格旋转速率 (lattice rotation rate)** 与**弹性自旋 (elastic spin)** $\boldsymbol{W}_{\mathrm{e}}$ 之间的精确关系：
$\dot{\boldsymbol{R}}_{\mathrm{e}}\boldsymbol{R}_{\mathrm{e}}^{\mathsf{T}} = \boldsymbol{W}_{\mathrm{e}} - \operatorname{skew}(\boldsymbol{R}_{\mathrm{e}} \dot{\boldsymbol{U}}_{\mathrm{e}} \boldsymbol{U}_{\mathrm{e}}^{-1} \boldsymbol{R}_{\mathrm{e}}^{\mathsf{T}})$

这个重要的结果表明，晶格的旋转速率通常不等于弹性自旋 $\boldsymbol{W}_{\mathrm{e}}$。它们之间相差一个由弹性拉伸率 $\dot{\boldsymbol{U}}_{\mathrm{e}}$ 与弹性拉伸 $\boldsymbol{U}_{\mathrm{e}}$ 的非共轴性引起的项。只有在弹性变形是纯旋转（$\boldsymbol{U}_{\mathrm{e}}=\boldsymbol{I}$）或者弹性拉伸与拉伸率共轴（$\dot{\boldsymbol{U}}_{\mathrm{e}}$ 和 $\boldsymbol{U}_{\mathrm{e}}$ 的主方向相同）的特殊情况下，晶格旋转速率才等于弹性自旋。[@problem_id:2663660]

此外，上述关系式中没有出现**塑性自旋 (plastic spin)** $\boldsymbol{W}_{\mathrm{p}} = \operatorname{skew}(\boldsymbol{L}_{\mathrm{p}})$。这说明塑性自旋不直接贡献于晶格的旋转。塑性自旋描述的是塑性流动内在的涡旋或旋转，它影响的是总的空间自旋 $\boldsymbol{W}$，而不是晶格本身的方位。这一区分对于正确模拟织构演化至关重要。