## 引言
在处理材料和结构的大变形问题时，仅依赖于当前变形构形的柯西应力已不足够。为了在更方便的初始参考构形中建立力学分析，连续介质力学引入了两种强大的工具：第一和第二皮奥拉-基尔霍夫(Piola-Kirchhoff, PK)应力张量。这些拉格朗日应力测度解决了如何在固定参考坐标系下描述力的作用和材料响应的难题，这对于理论推导和计算模拟（尤其是有限元法）至关重要。

本文将系统地引导您掌握这些核心概念。在“原理与机制”一章中，我们将从运动学基础出发，详细推导两种PK应力的定义、性质及其与柯西应力的关系。接下来的“应用与跨学科联系”一章将展示这些理论如何在超弹性本构模型、计算固体力学和材料科学等领域中发挥实际作用。最后，“动手实践”部分提供了具体的练习，帮助您将理论知识转化为解决实际问题的能力。通过这种由浅入深的结构，您将能够全面理解PK应力在现代固体力学中的基石地位。

## 原理与机制

在分析经历大变形的物体时，仅使用在当前（变形后）构形中定义的柯西（Cauchy）应力张量是不够的。许多情况下，尤其是在数值模拟（如有限元法）中，在初始（未变形）参考构形上建立控制方程会更为方便。这种方法被称为“全拉格朗日”或“材料”描述法。为了在这种框架下进行分析，我们需要引入几种备选的应力测度，它们能将力与参考构形中的几何量联系起来。本章将详细阐述两个核心的拉格朗日应力测度：第一和第二皮奥拉-基尔霍夫（Piola-Kirchhoff）应力张量。我们将从基本运动学原理出发，系统地推导它们的定义、物理意义、彼此之间的关系，以及它们在能量和本构关系中的关键作用。

### 变形的运动学基础

为了准确定义应力，我们首先必须精确描述变形本身。考虑一个连续体，它在初始时刻 $t=0$ 占据一个**参考构形** $\mathcal{B}_0$，在时刻 $t$ 占据一个**当前构形** $\mathcal{B}_t$。构形 $\mathcal{B}_0$ 和 $\mathcal{B}_t$ 是同一组物质点在不同时刻的空间位置集合。**运动**是一个映射 $\boldsymbol{\varphi}$，它将参考构形中的每个物质点 $\mathbf{X}$ 映射到其在当前构形中的空间位置 $\mathbf{x}$，即 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$。

局部变形的核心度量是**变形梯度**（deformation gradient）张量 $\mathbf{F}$，定义为：
$$
\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}} = \nabla_{\mathbf{X}} \boldsymbol{\varphi}
$$
变形梯度 $\mathbf{F}$ 包含了关于材料局部拉伸和旋转的全部信息。具体来说，它将参考构形中的一个无限小线元 $d\mathbf{X}$ 映射到当前构形中的对应线元 $d\mathbf{x}$ [@problem_id:2640987]：
$$
d\mathbf{x} = \mathbf{F} d\mathbf{X}
$$
$\mathbf{F}$ 的行列式 $J = \det \mathbf{F}$ 描述了体积的局部变化，即当前构形中的一个微元体积 $dV$ 与其在参考构形中的体积 $dV_0$ 之间的关系是 $dV = J dV_0$。物理上，物质不可穿透，且其局部朝向不会翻转，这要求 $J > 0$ 必须始终成立。我们将在本章末尾详细讨论这一重要约束。

为了更清晰地分离拉伸和旋转，可以对 $\mathbf{F}$ 进行**极分解**（polar decomposition）[@problem_id:2640987]：
$$
\mathbf{F} = \mathbf{R} \mathbf{U} = \mathbf{V} \mathbf{R}
$$
其中，$\mathbf{R}$ 是一个正常正交张量（即 $\mathbf{R}^T \mathbf{R} = \mathbf{I}$ 且 $\det \mathbf{R} = +1$），代表局部刚体旋转。$\mathbf{U}$ 和 $\mathbf{V}$ 是对称正定的拉伸张量，分别称为**右拉伸张量**和**左拉伸张量**。$\mathbf{U}$ 作用于参考构形，描述在旋转前发生的纯拉伸；而 $\mathbf{V}$ 作用于当前构形。

与拉伸张量密切相关的是**右柯西-格林变形张量**（right Cauchy-Green deformation tensor）$\mathbf{C}$，定义为：
$$
\mathbf{C} = \mathbf{F}^T \mathbf{F}
$$
$\mathbf{C}$ 完全在参考构形中定义，它度量了材料线元长度平方的变化：$|d\mathbf{x}|^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F} d\mathbf{X}) \cdot (\mathbf{F} d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{F}^T \mathbf{F} d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{C} d\mathbf{X})$。由极分解可知，$\mathbf{C} = (\mathbf{R}\mathbf{U})^T(\mathbf{R}\mathbf{U}) = \mathbf{U}^T \mathbf{R}^T \mathbf{R} \mathbf{U} = \mathbf{U}^2$。这意味着 $\mathbf{C}$ 的特征值是主拉伸比的平方，其特征向量定义了材料的主拉伸方向 [@problem_id:2640987]。相应的，**格林-拉格朗日应变张量**（Green-Lagrange strain tensor）$\mathbf{E}$ 定义为：
$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})
$$
$\mathbf{E}$ 是一个纯粹的材料应变测度，当且仅当发生刚体运动时（$\mathbf{C}=\mathbf{I}$），$\mathbf{E}$ 为零。

### 第一皮奥拉-基尔霍夫应力张量 (P)

在许多工程问题中，我们施加的力是作用在物体的初始边界上的。例如，在一个压力容器的设计中，我们关心的是施加在未变形表面上的压力。这就引出了一个问题：我们如何定义一个应力，它能够将作用在当前构形中的力与参考构形中的面积联系起来？

答案在于**第一皮奥拉-基尔霍夫应力张量**（First Piola-Kirchhoff stress tensor），通常记作 $\mathbf{P}$。我们首先定义**名义牵引力**（nominal traction）$\mathbf{T}_0$ 为作用在当前构形中的力除以其对应的**参考**面积。与之对比，**柯西牵引力**（Cauchy traction）$\mathbf{t}$ 是力除以**当前**面积。$\mathbf{P}$ 的物理定义就是将参考构形中的单位法向量 $\mathbf{N}$ 映射到名义牵引力矢量 $\mathbf{T}_0$ 的线性变换 [@problem_id:2587891]：
$$
\mathbf{T}_0 = \mathbf{P} \mathbf{N}
$$
需要特别注意的是，$\mathbf{P}$ 是一个**两点张量**（two-point tensor）。它将参考构形中的一个矢量（$\mathbf{N}$）映射到当前构形中的一个矢量（$\mathbf{T}_0$）。它的分量 $P_{iJ}$ 将参考坐标系的标号 $J$ 与当前坐标系的标号 $i$ 联系起来。

#### 与柯西应力的关系

$\mathbf{P}$ 张量与我们更熟悉的、在当前构形中定义的**柯西应力张量**（Cauchy stress tensor）$\boldsymbol{\sigma}$ 之间存在着明确的关系。柯西应力通过柯西公式 $\mathbf{t} = \boldsymbol{\sigma} \mathbf{n}$ 与柯西牵引力 $\mathbf{t}$ 和当前构形的单位法向量 $\mathbf{n}$ 相联系。

考虑作用于一个微元面积上的力矢量 $d\mathbf{f}$。无论是在参考构形还是当前构形中描述，这个力矢量是相同的：
$$
d\mathbf{f} = \mathbf{T}_0 dA_0 = \mathbf{t} da
$$
其中 $dA_0$ 和 $da$ 分别是参考面积和当前面积。这两个有向面积元之间的关系由**南森公式**（Nanson's formula）给出：$\mathbf{n} da = J \mathbf{F}^{-T} \mathbf{N} dA_0$。将所有关系代入力平衡方程：
$$
(\mathbf{P} \mathbf{N}) dA_0 = (\boldsymbol{\sigma} \mathbf{n}) da = \boldsymbol{\sigma} (\mathbf{n} da) = \boldsymbol{\sigma} (J \mathbf{F}^{-T} \mathbf{N} dA_0)
$$
由于这个等式对任意的法向量 $\mathbf{N}$ 都成立，我们便得到了连接 $\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 的著名关系式，即**皮奥ла变换**（Piola transform）[@problem_id:2641039] [@problem_id:2640987]：
$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}
$$

#### 对称性问题

我们知道，在没有体偶矩的情况下，角动量守恒要求柯西应力张量 $\boldsymbol{\sigma}$ 是对称的。一个自然的问题是：这种对称性是否会传递给第一皮奥拉-基尔霍夫应力 $\mathbf{P}$？

答案是，通常不会。让我们检验一下 $\mathbf{P}$ 的转置：
$$
\mathbf{P}^T = (J \boldsymbol{\sigma} \mathbf{F}^{-T})^T = J (\mathbf{F}^{-T})^T \boldsymbol{\sigma}^T = J \mathbf{F}^{-1} \boldsymbol{\sigma}
$$
这里我们已经使用了 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$。要使 $\mathbf{P}$ 对称，即 $\mathbf{P} = \mathbf{P}^T$，必须满足 $J \boldsymbol{\sigma} \mathbf{F}^{-T} = J \mathbf{F}^{-1} \boldsymbol{\sigma}$，或者等价地 $\mathbf{F} \boldsymbol{\sigma} = \boldsymbol{\sigma} \mathbf{F}^T$。这个条件对于任意变形 $\mathbf{F}$ 和应力状态 $\boldsymbol{\sigma}$ 来说，通常是不成立的。因此，**$\mathbf{P}$ 通常是非对称的** [@problem_id:2640989] [@problem_id:2641039]。

这是否意味着角动量守恒在参考构形中被违反了呢？并非如此。在材料描述中，角动量守恒要求的是另一个张量，即 $\mathbf{P}\mathbf{F}^T$，是对称的。我们可以验证这一点：
$$
\mathbf{P}\mathbf{F}^T = (J \boldsymbol{\sigma} \mathbf{F}^{-T}) \mathbf{F}^T = J \boldsymbol{\sigma} (\mathbf{F}^{-T} \mathbf{F}^T) = J \boldsymbol{\sigma}
$$
由于 $J$ 是标量且 $\boldsymbol{\sigma}$ 是对称的，所以 $J\boldsymbol{\sigma}$（有时称为**基尔霍夫应力** $\boldsymbol{\tau}$）是对称的。因此，$\mathbf{P}\mathbf{F}^T$ 的对称性得到了保证 [@problem_id:2640989]。$\mathbf{P}$ 的非对称性与变形 $\mathbf{F}$ 精确地耦合在一起，以确保力矩的平衡。

### 第二皮奥拉-基尔霍夫应力张量 (S)

$\mathbf{P}$ 张量作为两点张量的性质以及其非对称性，在某些情况下会带来不便，尤其是在建立材料本构关系时。例如，对于一个各向异性材料，其材料属性（如纤维方向）是固定在参考构形中的。我们希望有一个应力测度，它能完全在参考构形中定义，并且是对称的。

**第二皮奥拉-基尔霍夫应力张量**（Second Piola-Kirchhoff stress tensor），记作 $\mathbf{S}$，正是为了满足这些要求而被引入的。它通过将 $\mathbf{P}$ 张量“拉回”（pull-back）到参考构形来定义：
$$
\mathbf{P} = \mathbf{F} \mathbf{S} \quad \text{或等价地} \quad \mathbf{S} = \mathbf{F}^{-1} \mathbf{P}
$$
这个定义赋予了 $\mathbf{S}$ 一个清晰的物理图像：名义牵引力 $\mathbf{T}_0 = \mathbf{P}\mathbf{N}$ 是一个空间矢量。如果我们将其通过 $\mathbf{F}^{-1}$ 变换回参考构形，我们就得到了一个材料矢量 $\mathbf{F}^{-1}\mathbf{T}_0$。$\mathbf{S}$ 就是将参考法向量 $\mathbf{N}$ 映射到这个“伪牵引力”材料矢量的张量 [@problem_id:2641038]：
$$
\mathbf{F}^{-1}\mathbf{T}_0 = \mathbf{S} \mathbf{N}
$$
与 $\mathbf{P}$ 不同，$\mathbf{S}$ 是一个纯粹的**材料张量**，它只涉及参考构形中的矢量。

#### 与柯西应力的关系及对称性

通过结合 $\mathbf{S}$ 和 $\mathbf{P}$ 的定义式以及 $\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 的关系式，我们可以得到 $\mathbf{S}$ 和 $\boldsymbol{\sigma}$ 之间的直接联系：
$$
\mathbf{S} = \mathbf{F}^{-1} \mathbf{P} = \mathbf{F}^{-1} (J \boldsymbol{\sigma} \mathbf{F}^{-T}) = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T}
$$
现在我们可以检验 $\mathbf{S}$ 的对称性。假设 $\boldsymbol{\sigma}$ 是对称的：
$$
\mathbf{S}^T = (J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T})^T = J (\mathbf{F}^{-T})^T \boldsymbol{\sigma}^T (\mathbf{F}^{-1})^T = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T} = \mathbf{S}
$$
这个结果表明，**只要柯西应力 $\boldsymbol{\sigma}$ 是对称的，第二皮奥拉-基尔霍夫应力 $\mathbf{S}$ 就始终是对称的** [@problem_id:2640989] [@problem_id:2641038]。这一优良特性使 $\mathbf{S}$ 成为发展本构理论的理想选择。

### 能量共轭与本构关系

应力张量的另一个核心作用是它们在内能或应变能表达式中的角色。单位参考体积的内功率密度（应力功率）可以表示为某个应力测度与其共轭的应变率测度的缩并。

单位参考体积的应力功率 $\dot{w}_0$ 可以写作第一皮奥拉-基尔霍夫应力 $\mathbf{P}$ 与变形梯度率 $\dot{\mathbf{F}}$ 的缩并 [@problem_id:2525704]：
$$
\dot{w}_0 = \mathbf{P} : \dot{\mathbf{F}}
$$
其中“:”表示张量的双点积（Frobenius内积）。这表明 ($\mathbf{P}$, $\dot{\mathbf{F}}$) 是一对**能量共轭**（work-conjugate）的量。一个具体的计算实例可以在 [@problem_id:1549744] 中看到，其中通过计算 $\mathbf{P} : \delta\mathbf{F}$ 来求得虚功密度。

现在，我们使用关系式 $\mathbf{P} = \mathbf{F}\mathbf{S}$ 来转换这个表达式：
$$
\dot{w}_0 = (\mathbf{F}\mathbf{S}) : \dot{\mathbf{F}}
$$
可以证明（利用 $\mathbf{S}$ 的对称性），上式等价于：
$$
\dot{w}_0 = \mathbf{S} : \dot{\mathbf{E}}
$$
其中 $\dot{\mathbf{E}} = \frac{1}{2}(\dot{\mathbf{F}}^T\mathbf{F} + \mathbf{F}^T\dot{\mathbf{F}})$ 是格林-拉格朗日应变率。这个重要的恒等式 [@problem_id:2641038] [@problem_id:2641039] 表明，**第二皮奥拉-基尔霍夫应力 $\mathbf{S}$ 与格林-拉格朗日应变率 $\dot{\mathbf{E}}$ 是能量共轭的**。

这种共轭关系对于**超弹性**（hyperelastic）材料至关重要。对于这类材料，其本构行为由一个应变能密度函数 $\Psi$ 描述。如果我们将 $\Psi$ 视为 $\mathbf{E}$ 的函数，那么 $\mathbf{S}$ 可以直接通过求导得到：
$$
\mathbf{S} = \frac{\partial \Psi}{\partial \mathbf{E}}
$$
由于 $\mathbf{E}$ 完全基于参考构形，且 $\mathbf{S}$ 也是一个材料张量，这个本构关系在形式上非常简洁，并且自动满足材料客观性原理。此外，对于各向同性材料，$\Psi$ 必须是 $\mathbf{C}$（或等价地，$\mathbf{E}$）的标量不变量的函数。根据张量表示理论，这意味着 $\mathbf{S}$ 必须是 $\mathbf{C}$ 的一个同轴张量函数，即 **$\mathbf{S}$ 和 $\mathbf{C}$ 具有相同的主方向** [@problem_id:2587891]。

### 客观性与标架无关性

一个基本物理原则是，材料的本构响应不应依赖于观察者的参考系。具体来说，如果在当前构形上叠加一个刚体运动，材料内部的“真实”应力状态不应改变。这个性质被称为**客观性**（objectivity）或**标架无关性**（frame-indifference）。

让我们考察在一个已变形的构形 $\mathbf{x}$ 上叠加一个刚体旋转 $\mathbf{Q}$（$\mathbf{x}^* = \mathbf{Q}\mathbf{x}$）时，各个应力张量的行为。新的变形梯度为 $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$。

- **第一皮奥拉-基尔霍夫应力 $\mathbf{P}$** 的变换为：
  $$
  \mathbf{P}^* = J^* \boldsymbol{\sigma}^* (\mathbf{F}^*)^{-T} = J (\mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T) (\mathbf{Q}\mathbf{F})^{-T} = \mathbf{Q} (J \boldsymbol{\sigma} \mathbf{F}^{-T}) = \mathbf{Q}\mathbf{P}
  $$
  $\mathbf{P}$ 张量会随着叠加的旋转而旋转，因此它**不是客观的** [@problem_id:2641039]。

- **第二皮奥拉-基尔霍夫应力 $\mathbf{S}$** 的变换为：
  $$
  \mathbf{S}^* = (\mathbf{F}^*)^{-1} \mathbf{P}^* = (\mathbf{Q}\mathbf{F})^{-1} (\mathbf{Q}\mathbf{P}) = (\mathbf{F}^{-1}\mathbf{Q}^{-1}) (\mathbf{Q}\mathbf{P}) = \mathbf{F}^{-1} (\mathbf{Q}^T\mathbf{Q}) \mathbf{P} = \mathbf{F}^{-1}\mathbf{P} = \mathbf{S}
  $$
  $\mathbf{S}$ 张量在刚体旋转下保持不变。因此，**$\mathbf{S}$ 是一个客观的张量** [@problem_id:2587891]。数值算例 [@problem_id:1549814] 清晰地展示了这一点，即在施加旋转后计算得到的 $\mathbf{S}^*$ 与原始的 $\mathbf{S}$ 完全相同。$\mathbf{S}$ 的客观性是其在现代本构理论中占据核心地位的另一个主要原因。

### 应力测度之间的关系总结

至此，我们已经引入了四个主要的应力张量。它们之间的关系可以通过“推前”（push-forward，从参考构形到当前构形）和“拉回”（pull-back，从当前构形到参考构形）操作来系统地总结。引入**基尔霍夫应力**（Kirchhoff stress）$\boldsymbol{\tau} = J\boldsymbol{\sigma}$，它可以被看作是考虑了体积变化的柯西应力。

下面是这些关系的核心摘要 [@problem_id:2887012]：

- **从 $\boldsymbol{\sigma}$ 到 $\mathbf{P}$ 和 $\mathbf{S}$ (拉回):**
  $$
  \mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}
  $$
  $$
  \mathbf{S} = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T} = \mathbf{F}^{-1} \mathbf{P}
  $$

- **从 $\mathbf{S}$ 到 $\mathbf{P}$ 和 $\boldsymbol{\tau}$ (推前):**
  $$
  \mathbf{P} = \mathbf{F} \mathbf{S}
  $$
  $$
  \boldsymbol{\tau} = \mathbf{F} \mathbf{S} \mathbf{F}^T
  $$

这些变换关系构成了有限变形力学中应力分析的基础，使得我们可以在最方便的构形中进行计算，并在不同描述之间进行精确转换。

### 物理约束：雅可比行列式 $J > 0$ 的重要性

在所有讨论中，我们都假设变形梯度的行列式 $J = \det \mathbf{F}$ 恒为正。这个条件不仅是一个数学上的便利，更是一个深刻的物理约束。

- **物理意义**：$J$ 代表了局部体积比。$J>0$ 意味着材料的局部朝向得以保持。$J=0$ 意味着一个有限体积被压缩为零，对应于无限大的密度，这是物理上不可能的。$J  0$ 则意味着材料发生了“翻转”或“穿透自身”，这违背了物质的不可入性原理。从质量守恒 $\rho = \rho_0/J$ 来看，$J  0$ 将导致负的质量密度，这在物理上是荒谬的 [@problem_id:2587867]。

- **本构约束**：为了使理论模型符合物理现实，任何有效的超弹性应变能函数 $\Psi$ 都必须包含一个能量壁垒，以阻止 $J$ 趋近于零。这通常通过引入一个仅依赖于 $J$ 的体积能项 $\Psi_{\text{vol}}(J)$ 来实现，该项具有以下性质：
  $$
  \lim_{J \to 0^+} \Psi_{\text{vol}}(J) = \infty
  $$
  例如，包含 $\ln J$ 或 $1/J$ 的项都可以实现这种效果。由于这些函数在 $J \le 0$ 时是未定义的，因此基于这些能量函数导出的应力张量 $\mathbf{P}$ 和 $\mathbf{S}$ 在物理上有意义的理论中也只对 $J0$ 有定义。

- **计算实践**：在非线性有限元分析中，迭代求解过程中可能会出现数值上的过度推进，导致某些积分点的 $J$ 暂时变为负值。这是一个数值失稳的信号，表明迭代步长过大。稳健的有限元程序会采用多种策略来防止或纠正这种情况，包括：使用带有体积惩罚项的本构模型、通过线搜索或信赖域等全局化策略来限制迭代步长，以及在每次迭代后检查单元的雅可比行列式，一旦发现 $J \le 0$ 就拒绝当前增量并减小时间步长（“cutback”） [@problem_id:2587867]。

总之，皮奥拉-基尔霍夫应力张量为在参考构形中分析大变形问题提供了强大而必要的工具。第一PK应力 $\mathbf{P}$ 直接与名义牵引力相关，在边界条件设定中非常有用。而第二PK应力 $\mathbf{S}$ 因其对称性和客观性，在发展描述材料内在力学行为的本构关系中扮演着无可替代的角色。对这些应力测度的深刻理解是掌握现代固体力学和计算力学的基石。