## 引言
在探索物体如何响应外力而运动和变形时，[连续介质力学](@entry_id:155125)提供了一套强大的理论框架。然而，当我们面对橡胶拉伸、[金属塑性](@entry_id:176585)成型或生物组织搏动这类显著的几何变化（即“[大变形](@entry_id:167243)”）时，仅仅描述各点的位移是远远不够的。位移本身混合了不引起内力的[刚体运动](@entry_id:193355)（平移和旋转）和真正引起材料拉伸与剪切的变形。为了精确、客观地量化材料内部的局部变形，我们需要一个更深刻的度量工具，这便是[格林-拉格朗日应变张量](@entry_id:187745)诞生的背景。它解决了如何从复杂的运动中剥离出纯粹变形这一核心问题。

本文旨在系统地介绍[格林-拉格朗日应变张量](@entry_id:187745)，带领读者从基本原理走向前沿应用。在接下来的内容中，您将学习到：

- **第一部分：原理与机制** 将深入探讨格林-拉格朗-日应变张量的数学定义、它如何从位移场中导出、其对刚体运动的不变性，以及其分量所对应的清晰几何诠释。
- **第二部分：应用与跨学科联系** 将展示该张量如何在[非线性力学](@entry_id:178303)、[材料科学](@entry_id:152226)、计算工程模拟（如[有限元分析](@entry_id:138109)）以及[生物力学](@entry_id:153973)等领域中作为核心工具，解决从[超弹性材料建模](@entry_id:187798)到[心脏功能](@entry_id:152687)评估等实际问题。
- **第三部分：动手实践** 将提供一系列精心设计的问题，引导您将理论知识应用于具体计算，从而巩固对这一重要概念的理解。

通过本次学习，您将构建起对有限变形理论的坚实基础，为后续更深入的力学研究与工程应用做好准备。让我们首先进入“原理与机制”的世界，揭示[格林-拉格朗日应变张量](@entry_id:187745)的奥秘。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，描述一个物体从初始（或参考）构型到当前（或变形后）构型的几何变化，是[运动学](@entry_id:173318)分析的核心。虽然[位移场](@entry_id:141476) $\mathbf{u}$ 提供了每个物[质点](@entry_id:186768)移动的直接信息，但它并不能直接量化材料本身的局部变形，因为[位移场](@entry_id:141476)中包含了不引起内力变化的刚体平移和旋转。为了真正度量材料的变形，即相邻物[质点](@entry_id:186768)之间距离的相对变化，我们需要引入一个更合适的物理量——[应变张量](@entry_id:193332)。本章将系统地阐述[格林-拉格朗日应变张量](@entry_id:187745)（Green-Lagrange Strain Tensor）的定义、物理意义及其在不同[坐标系](@entry_id:156346)和物理情境下的应用。

### 定义应变：一种基于材料的度量

应变的核心思想是量化变形过程中物质微元长度和角度的改变。让我们考虑参考构型中一个无限小的物质线元 $d\mathbf{X}$。经过变形后，这个线元变为当前构型中的 $d\mathbf{x}$。根据前一章的知识，这两个线元通过变形梯度张量 $\mathbf{F}$ 相关联：

$$
d\mathbf{x} = \mathbf{F} d\mathbf{X}
$$

我们可以通过比较这两个[线元](@entry_id:196833)长度的平方来量化其长度变化。设 $d\mathbf{X}$ 的初始长度平方为 $(dS)^2$，变形后的长度平方为 $(ds)^2$。我们有：

$$
(dS)^2 = d\mathbf{X} \cdot d\mathbf{X} = d\mathbf{X}^T d\mathbf{X}
$$

$$
(ds)^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F} d\mathbf{X}) \cdot (\mathbf{F} d\mathbf{X}) = d\mathbf{X}^T \mathbf{F}^T \mathbf{F} d\mathbf{X}
$$

长度平方的改变值 $(ds)^2 - (dS)^2$ 完全由变形引起，它是一个二次型，其形式为：

$$
(ds)^2 - (dS)^2 = d\mathbf{X}^T \mathbf{F}^T \mathbf{F} d\mathbf{X} - d\mathbf{X}^T \mathbf{I} d\mathbf{X} = d\mathbf{X}^T (\mathbf{F}^T \mathbf{F} - \mathbf{I}) d\mathbf{X}
$$

其中 $\mathbf{I}$ 是二阶单位张量。这个关系式清晰地表明，[对称张量](@entry_id:148092) $\mathbf{F}^T \mathbf{F} - \mathbf{I}$ 完全捕捉了所有物质线元长度平方的变化信息。为了方便，我们定义**右柯西-格林变形张量(Right Cauchy-Green Deformation Tensor)** $\mathbf{C} = \mathbf{F}^T \mathbf{F}$。于是，长度平方的变化可以写为 $d\mathbf{X}^T (\mathbf{C} - \mathbf{I}) d\mathbf{X}$。

为了定义一个在小变形情况下能够退化为我们所熟悉的[无穷小应变](@entry_id:197162)的量，我们引入因子 $\frac{1}{2}$，从而定义了**[格林-拉格朗日应变张量](@entry_id:187745) (Green-Lagrange strain tensor)**，记作 $\mathbf{E}$：

$$
\mathbf{E} = \frac{1}{2}(\mathbf{F}^T \mathbf{F} - \mathbf{I}) = \frac{1}{2}(\mathbf{C} - \mathbf{I})
$$

这个定义是连续介质力学中描述[大变形](@entry_id:167243)的核心。由于 $\mathbf{C}$ 是对称的（$\mathbf{C}^T = (\mathbf{F}^T \mathbf{F})^T = \mathbf{F}^T (\mathbf{F}^T)^T = \mathbf{F}^T \mathbf{F} = \mathbf{C}$），$\mathbf{E}$ 也是一个对称的[二阶张量](@entry_id:199780)。它完全在参考构型（即材料坐标 $\mathbf{X}$）中定义，因此它是一种**[拉格朗日描述](@entry_id:264498) (Lagrangian description)** 的[应变度量](@entry_id:755495) [@problem_id:1537001]。

### 格林-拉格朗日张量与位移

为了将[应变张量](@entry_id:193332)与更直观的物理量——[位移场](@entry_id:141476)联系起来，我们回忆[位移矢量](@entry_id:262782) $\mathbf{u}$ 的定义：它是一个物质点从初始位置 $\mathbf{X}$ 到当前位置 $\mathbf{x}$ 的矢量差。

$$
\mathbf{x}(\mathbf{X}, t) = \mathbf{X} + \mathbf{u}(\mathbf{X}, t)
$$

变形梯度 $\mathbf{F}$ 是当前位置 $\mathbf{x}$ 对初始位置 $\mathbf{X}$ 的梯度。我们将位移的表达式代入，得到：

$$
\mathbf{F} = \nabla_{\mathbf{X}} \mathbf{x} = \nabla_{\mathbf{X}} (\mathbf{X} + \mathbf{u}) = \nabla_{\mathbf{X}} \mathbf{X} + \nabla_{\mathbf{X}} \mathbf{u}
$$

由于 $\mathbf{X}$ 对自身的梯度是单位张量 $\mathbf{I}$，上式简化为：

$$
\mathbf{F} = \mathbf{I} + \nabla_{\mathbf{X}} \mathbf{u}
$$

这里的 $\nabla_{\mathbf{X}} \mathbf{u}$ 是[位移梯度张量](@entry_id:748571)，其分量为 $(\nabla_{\mathbf{X}} \mathbf{u})_{ij} = \frac{\partial u_i}{\partial X_j}$。现在，我们将这个关系代入 $\mathbf{E}$ 的定义中 [@problem_id:1547223]：

$$
\mathbf{E} = \frac{1}{2} \left( (\mathbf{I} + \nabla_{\mathbf{X}} \mathbf{u})^T (\mathbf{I} + \nabla_{\mathbf{X}} \mathbf{u}) - \mathbf{I} \right)
$$

展开乘积项：

$$
(\mathbf{I} + \nabla_{\mathbf{X}} \mathbf{u})^T (\mathbf{I} + \nabla_{\mathbf{X}} \mathbf{u}) = (\mathbf{I} + (\nabla_{\mathbf{X}} \mathbf{u})^T) (\mathbf{I} + \nabla_{\mathbf{X}} \mathbf{u}) = \mathbf{I} + \nabla_{\mathbf{X}} \mathbf{u} + (\nabla_{\mathbf{X}} \mathbf{u})^T + (\nabla_{\mathbf{X}} \mathbf{u})^T (\nabla_{\mathbf{X}} \mathbf{u})
$$

代回到 $\mathbf{E}$ 的表达式中，$\mathbf{I}$ 项被消去，最终得到[格林-拉格朗日应变张量](@entry_id:187745)用[位移梯度](@entry_id:165352)表示的形式：

$$
\mathbf{E} = \frac{1}{2} \left( \nabla_{\mathbf{X}} \mathbf{u} + (\nabla_{\mathbf{X}} \mathbf{u})^T + (\nabla_{\mathbf{X}} \mathbf{u})^T (\nabla_{\mathbf{X}} \mathbf{u}) \right)
$$

这个表达式揭示了 $\mathbf{E}$ 与[位移梯度](@entry_id:165352)之间的非线性关系。

### 关键属性与物理诠释

#### [刚体运动](@entry_id:193355)下的不变性

一个有效的[应变度量](@entry_id:755495)必须能够区分真实的[材料变形](@entry_id:169356)和不产生内应力的[刚体运动](@entry_id:193355)。换言之，对于纯刚体平移和旋转，应变必须为零。让我们来验证[格林-拉格朗日应变张量](@entry_id:187745)是否满足这一关键要求。

一个一般的刚体运动可以表示为：

$$
\mathbf{x}(\mathbf{X}, t) = \mathbf{c}(t) + \mathbf{Q}(t) \mathbf{X}
$$

其中 $\mathbf{c}(t)$ 是一个随时间变化的平移矢量，$\mathbf{Q}(t)$ 是一个随时间变化的**正常正交张量 (proper orthogonal tensor)**，代表旋转。由于 $\mathbf{c}(t)$ 仅是时间的函数，与 $\mathbf{X}$ 无关，其梯度为零。因此，变形梯度为：

$$
\mathbf{F} = \nabla_{\mathbf{X}} \mathbf{x} = \mathbf{Q}(t)
$$

将此代入 $\mathbf{E}$ 的定义中：

$$
\mathbf{E} = \frac{1}{2}(\mathbf{F}^T \mathbf{F} - \mathbf{I}) = \frac{1}{2}(\mathbf{Q}^T \mathbf{Q} - \mathbf{I})
$$

根据正交张量的定义，我们有 $\mathbf{Q}^T \mathbf{Q} = \mathbf{I}$。因此，对于任何[刚体运动](@entry_id:193355)，[格林-拉格朗日应变张量](@entry_id:187745)恒为零：

$$
\mathbf{E} = \frac{1}{2}(\mathbf{I} - \mathbf{I}) = \mathbf{0}
$$

这个结果至关重要，它证实了 $\mathbf{E}$ 确实只度量变形，而忽略了[刚体运动](@entry_id:193355) [@problem_id:1551022]。这一特性也被称为**客观性 (objectivity)**，尽管在更严格的定义中，客观性是指[应变度量](@entry_id:755495)在叠加任意刚体运动后保持不变。

#### 与[无穷小应变](@entry_id:197162)的关系

在工程应用中，尤其是在[小变形理论](@entry_id:174991)中，我们常用**[无穷小应变张量](@entry_id:167211) (infinitesimal strain tensor)**（或称为柯西[应变张量](@entry_id:193332)），记作 $\boldsymbol{\epsilon}$，其定义为：

$$
\boldsymbol{\epsilon} = \frac{1}{2} \left( \nabla_{\mathbf{X}} \mathbf{u} + (\nabla_{\mathbf{X}} \mathbf{u})^T \right)
$$

比较 $\mathbf{E}$ 和 $\boldsymbol{\epsilon}$ 的表达式，我们发现：

$$
\mathbf{E} = \boldsymbol{\epsilon} + \frac{1}{2} (\nabla_{\mathbf{X}} \mathbf{u})^T (\nabla_{\mathbf{X}} \mathbf{u})
$$

$\mathbf{E}$ 包含了[无穷小应变](@entry_id:197162) $\boldsymbol{\epsilon}$ 以及一个关于[位移梯度](@entry_id:165352)的二次[非线性](@entry_id:637147)项。这个[非线性](@entry_id:637147)项正是区分[有限应变理论](@entry_id:176941)和[无穷小应变](@entry_id:197162)理论的关键。

当变形非常小时，[位移梯度](@entry_id:165352)的所有分量都远小于1，即 $||\nabla_{\mathbf{X}} \mathbf{u}|| \ll 1$。在这种情况下，二次项 $(\nabla_{\mathbf{X}} \mathbf{u})^T (\nabla_{\mathbf{X}} \mathbf{u})$ 是一个更高阶的小量，可以被忽略。此时，[格林-拉格朗日应变张量](@entry_id:187745)近似等于[无穷小应变张量](@entry_id:167211)：

$$
\mathbf{E} \approx \boldsymbol{\epsilon} \quad (\text{for } ||\nabla_{\mathbf{X}} \mathbf{u}|| \ll 1)
$$

这个关系阐明了为什么 $\mathbf{E}$ 是一个普适的[应变度量](@entry_id:755495)，它在有限变形（[大变形](@entry_id:167243)）时是精确的，并在小变形极限下自然地过渡到线性理论。例如，考虑一个一维拉伸问题，位移为 $u_1(X_1) = C X_1^3$ [@problem_id:1557338]。此时，$\epsilon_{11} = \frac{\partial u_1}{\partial X_1} = 3CX_1^2$，而 $E_{11} = \epsilon_{11} + \frac{1}{2}(\epsilon_{11})^2$。两者之间的相对差异为 $\frac{|E_{11} - \epsilon_{11}|}{|E_{11}|} = \frac{\frac{1}{2}\epsilon_{11}^2}{\epsilon_{11} + \frac{1}{2}\epsilon_{11}^2} = \frac{\epsilon_{11}}{2 + \epsilon_{11}}$。只有当 $\epsilon_{11}$ 远小于1时，这个差异才可忽略不计。

### 几何诠释：长度与角度的变化

[格林-拉格朗日应变张量](@entry_id:187745)的各个分量具有明确的几何意义，它们直接关联于材料纤维的拉伸和成对纤维之间角度的改变。

#### 伸长应变（拉伸）

考虑参考构型中一根沿单位矢量 $\mathbf{N}$ 方向的无限小材料纤维。其初始长度平方为 $|\mathbf{N}|^2 = 1$。变形后，这根纤维变为矢量 $\mathbf{n} = \mathbf{F}\mathbf{N}$。

我们定义**拉伸比 (stretch ratio)** $\lambda_{(\mathbf{N})}$ 为纤维的最终长度与初始长度之比。因此，$\lambda_{(\mathbf{N})}^2$ 是长度的平方比：

$$
\lambda_{(\mathbf{N})}^2 = \frac{|\mathbf{n}|^2}{|\mathbf{N}|^2} = |\mathbf{F}\mathbf{N}|^2 = (\mathbf{F}\mathbf{N}) \cdot (\mathbf{F}\mathbf{N}) = \mathbf{N}^T \mathbf{F}^T \mathbf{F} \mathbf{N} = \mathbf{N}^T \mathbf{C} \mathbf{N}
$$

使用关系 $\mathbf{C} = 2\mathbf{E} + \mathbf{I}$，我们得到：

$$
\lambda_{(\mathbf{N})}^2 = \mathbf{N}^T (2\mathbf{E} + \mathbf{I}) \mathbf{N} = \mathbf{N}^T \mathbf{I} \mathbf{N} + 2\mathbf{N}^T \mathbf{E} \mathbf{N} = 1 + 2\mathbf{N}^T \mathbf{E} \mathbf{N}
$$

这个方程揭示了 $\mathbf{E}$ 的一个深刻的几何意义：二次型 $\mathbf{N}^T \mathbf{E} \mathbf{N}$ 正是沿 $\mathbf{N}$ 方向的纤维长度平方变化的一半。我们定义沿 $\mathbf{N}$ 方向的**伸长应变 (extensional strain)** $e_{(\mathbf{N})}$ 为：

$$
e_{(\mathbf{N})} = \mathbf{N}^T \mathbf{E} \mathbf{N}
$$

结合上面的拉伸比公式，我们得到一个等价且常用的关系 [@problem_id:1551024]：

$$
e_{(\mathbf{N})} = \frac{1}{2}(\lambda_{(\mathbf{N})}^2 - 1)
$$

例如，如果一个二维变形的变形梯度为 $\mathbf{F} = \begin{pmatrix} 1.1  0.3 \\ 0.2  1.3 \end{pmatrix}$，对于初始方向为 $\mathbf{N} = \frac{1}{\sqrt{5}}(1, 2)^T$ 的纤维，变形后的矢量为 $\mathbf{n} = \mathbf{F}\mathbf{N} = \frac{1}{\sqrt{5}}(1.7, 2.8)^T$。拉伸比的平方为 $\lambda_{(\mathbf{N})}^2 = |\mathbf{n}|^2 = \frac{1}{5}(1.7^2 + 2.8^2) = 2.146$。因此，该纤维的伸长应变为 $e_{(\mathbf{N})} = \frac{1}{2}(2.146 - 1) = 0.573$。

#### 剪切应变（角度变化）

现在考虑参考构型中两根最初正交的材料纤维，其方向由单位矢量 $\mathbf{M}_1$ 和 $\mathbf{M}_2$ 描述（即 $\mathbf{M}_1 \cdot \mathbf{M}_2 = 0$）。变形后，它们变为矢量 $\mathbf{m}_1 = \mathbf{F}\mathbf{M}_1$ 和 $\mathbf{m}_2 = \mathbf{F}\mathbf{M}_2$。

变形后两根纤维之间的夹角 $\theta$ 可以通过它们的[点积](@entry_id:149019)来确定：

$$
\mathbf{m}_1 \cdot \mathbf{m}_2 = (\mathbf{F}\mathbf{M}_1) \cdot (\mathbf{F}\mathbf{M}_2) = \mathbf{M}_1^T \mathbf{F}^T \mathbf{F} \mathbf{M}_2 = \mathbf{M}_1^T \mathbf{C} \mathbf{M}_2
$$

再次使用 $\mathbf{C} = 2\mathbf{E} + \mathbf{I}$：

$$
\mathbf{m}_1 \cdot \mathbf{m}_2 = \mathbf{M}_1^T (2\mathbf{E} + \mathbf{I}) \mathbf{M}_2 = 2\mathbf{M}_1^T \mathbf{E} \mathbf{M}_2 + \mathbf{M}_1^T \mathbf{I} \mathbf{M}_2 = 2\mathbf{M}_1^T \mathbf{E} \mathbf{M}_2
$$

上式中 $\mathbf{M}_1^T \mathbf{I} \mathbf{M}_2 = \mathbf{M}_1 \cdot \mathbf{M}_2 = 0$。这个结果表明，二次型 $2\mathbf{M}_1^T \mathbf{E} \mathbf{M}_2$ 直接量化了初始正交的纤维在变形后的[点积](@entry_id:149019)。如果这个[点积](@entry_id:149019)不为零，则说明两根纤维不再正交，发生了**剪切变形 (shear deformation)**。$\mathbf{E}$ 的非对角分量正是剪切的度量。

具体来说，变形后夹角的余弦为：

$$
\cos\theta = \frac{\mathbf{m}_1 \cdot \mathbf{m}_2}{|\mathbf{m}_1| |\mathbf{m}_2|} = \frac{2\mathbf{M}_1^T \mathbf{E} \mathbf{M}_2}{\lambda_{(\mathbf{M}_1)} \lambda_{(\mathbf{M}_2)}} = \frac{2\mathbf{M}_1^T \mathbf{E} \mathbf{M}_2}{\sqrt{(1+2\mathbf{M}_1^T \mathbf{E} \mathbf{M}_1)(1+2\mathbf{M}_2^T \mathbf{E} \mathbf{M}_2)}}
$$

在一个具体实例中 [@problem_id:1551044]，如果 $\mathbf{M}_1 = \mathbf{e}_1$ 和 $\mathbf{M}_2 = \mathbf{e}_2$，则 $\mathbf{M}_1^T \mathbf{E} \mathbf{M}_2 = E_{12}$，$\mathbf{M}_1^T \mathbf{E} \mathbf{M}_1 = E_{11}$，$\mathbf{M}_2^T \mathbf{E} \mathbf{M}_2 = E_{22}$。于是，

$$
\cos\theta = \frac{2E_{12}}{\sqrt{(1+2E_{11})(1+2E_{22})}}
$$

这清晰地展示了非对角项 $E_{12}$ 如何导致初始正交的坐标轴在变形后发生角度偏离。

### 高等主题与公式

#### 应变与体积变化

变形过程中的体积变化由变形梯度的[行列式](@entry_id:142978) $J = \det(\mathbf{F})$ 描述，称为**[雅可比行列式](@entry_id:137120) (Jacobian determinant)**。$J$ 是局部体积变化率。我们希望将这个纯[运动学](@entry_id:173318)量与[格林-拉格朗日应变张量](@entry_id:187745)联系起来。

首先，我们考虑[右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^T\mathbf{F}$ 的[行列式](@entry_id:142978)：

$$
\det(\mathbf{C}) = \det(\mathbf{F}^T \mathbf{F}) = \det(\mathbf{F}^T)\det(\mathbf{F}) = (\det(\mathbf{F}))^2 = J^2
$$

又因为 $\mathbf{C} = \mathbf{I} + 2\mathbf{E}$，所以体积变化的关系可以写成：

$$
J^2 = \det(\mathbf{I} + 2\mathbf{E})
$$

对于三维空间中的任意二阶张量 $\mathbf{T}$，其[行列式](@entry_id:142978) $\det(\mathbf{I} + x\mathbf{T})$ 可以用 $\mathbf{T}$ 的[主不变量](@entry_id:193522) $I_T, II_T, III_T$ 表示：

$$
\det(\mathbf{I} + x\mathbf{T}) = 1 + x I_T + x^2 II_T + x^3 III_T
$$

将此恒等式应用于 $J^2 = \det(\mathbf{I} + 2\mathbf{E})$，令 $\mathbf{T} = \mathbf{E}$ 且 $x=2$，我们得到：

$$
J^2 = 1 + 2 I_E + 4 II_E + 8 III_E
$$

其中 $I_E, II_E, III_E$ 是 $\mathbf{E}$ 的三个[主不变量](@entry_id:193522)。这个公式将体积变化直接与应变张量的[不变量](@entry_id:148850)联系起来。一个特别重要的情形是**[不可压缩材料](@entry_id:159741) (incompressible material)** 的**[等容变形](@entry_id:196451) (isochoric deformation)**，其特征是[体积保持](@entry_id:141001)不变，即 $J=1$。在这种情况下，我们得到一个只涉及[应变不变量](@entry_id:190518)的[约束方程](@entry_id:138140) [@problem_id:1551019]：

$$
1 = 1 + 2 I_E + 4 II_E + 8 III_E \quad \implies \quad I_E + 2 II_E + 4 III_E = 0
$$

这个方程为处理[不可压缩材料](@entry_id:159741)的有限变形问题提供了重要的数学工具。

#### 变换性质

[格林-拉格朗日应变张量](@entry_id:187745)是一个定义在参考构型上的张量。因此，如果我们改变参考构型的选择，$\mathbf{E}$ 的分量也会相应改变。考虑这样一种情况：我们首先对参考构型进行一次刚体旋转 $\mathbf{Q}$，得到一个新的参考构型。然后，相对于这个新的、已旋转的构型，我们施加一个由变形梯度 $\mathbf{F}$ 描述的变形。

根据变形梯度的链式法则，总的变形梯度 $\mathbf{F}_{\text{new}}$ 是两次变形的复合：

$$
\mathbf{F}_{\text{new}} = \mathbf{F} \mathbf{Q}
$$

相应的新[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E}_{\text{new}}$ 为：

$$
\mathbf{E}_{\text{new}} = \frac{1}{2}(\mathbf{F}_{\text{new}}^T \mathbf{F}_{\text{new}} - \mathbf{I}) = \frac{1}{2}((\mathbf{F}\mathbf{Q})^T (\mathbf{F}\mathbf{Q}) - \mathbf{I}) = \frac{1}{2}(\mathbf{Q}^T \mathbf{F}^T \mathbf{F} \mathbf{Q} - \mathbf{I})
$$

由于 $\mathbf{Q}$ 是正交的，我们可以插入一个 $\mathbf{Q}^T\mathbf{Q} = \mathbf{I}$：

$$
\mathbf{E}_{\text{new}} = \frac{1}{2}(\mathbf{Q}^T \mathbf{F}^T \mathbf{F} \mathbf{Q} - \mathbf{Q}^T \mathbf{I} \mathbf{Q}) = \mathbf{Q}^T \left( \frac{1}{2}(\mathbf{F}^T \mathbf{F} - \mathbf{I}) \right) \mathbf{Q}
$$

括号内的正是原始的应变张量 $\mathbf{E}$。因此，我们得到了 $\mathbf{E}$ 在参考构型旋转下的变换法则 [@problem_id:1551033]：

$$
\mathbf{E}_{\text{new}} = \mathbf{Q}^T \mathbf{E} \mathbf{Q}
$$

这表明 $\mathbf{E}$ 作为一个定义在材料空间中的[二阶张量](@entry_id:199780)，在参考[坐标系](@entry_id:156346)发生旋转时，其分量遵循标准的[张量变换法则](@entry_id:185176)。

#### [曲线坐标系](@entry_id:172561)下的表述

到目前为止，我们的讨论主要基于笛卡尔坐标系。然而，[格林-拉格朗日应变张量](@entry_id:187745)的定义是几何的，可以自然地推广到任意**[曲线坐标系](@entry_id:172561) (curvilinear coordinate system)**。这种推广在处理具有特定几何形状（如圆柱、球体）的物体时尤其强大。

设物质点的初始位置 $\mathbf{X}$ 和当前位置 $\mathbf{x}$ 都是一组物质坐标 $(\xi^1, \xi^2, \xi^3)$ 的函数。参考构型和当前构型的几何性质分别由它们的度量张量描述。

参考构型的**度量张量 (metric tensor)** $G_{IJ}$ (也称[第一基本形式](@entry_id:274022)) 的分量为：
$$
G_{IJ} = \frac{\partial \mathbf{X}}{\partial \xi^I} \cdot \frac{\partial \mathbf{X}}{\partial \xi^J}
$$
它描述了参考构型中坐标网格的几何。参考构型中任意微元线段的长度平方为 $dS^2 = G_{IJ} d\xi^I d\xi^J$。

类似地，我们可以定义一个描述变形后物体几何的度量张量 $g_{IJ}$，它是通过将空间度量“[拉回](@entry_id:160816)”到物质[坐标系](@entry_id:156346)来计算的：
$$
g_{IJ} = \frac{\partial \mathbf{x}}{\partial \xi^I} \cdot \frac{\partial \mathbf{x}}{\partial \xi^J}
$$
变形后微元线段的长度平方为 $ds^2 = g_{IJ} d\xi^I d\xi^J$。

长度平方的变化 $(ds)^2 - (dS)^2$ 现在可以表示为：
$$
(ds)^2 - (dS)^2 = (g_{IJ} - G_{IJ}) d\xi^I d\xi^J
$$
这启发我们定义[格林-拉格朗日应变张量](@entry_id:187745)在物质[坐标系](@entry_id:156346)下的**协变分量 (covariant components)** [@problem_id:1551036]：

$$
E_{IJ} = \frac{1}{2} (g_{IJ} - G_{IJ})
$$

这个表达式非常优雅和强大，它将应变的计算转化为计算两个构型的度量张量之差。例如，在圆柱坐标 $(R, \Theta, Z)$ 下分析圆柱体的扭转变形，其变形映射为 $\mathbf{x}(R, \Theta, Z) = R\cos(\Theta + kZ)\mathbf{e}_1 + R\sin(\Theta + kZ)\mathbf{e}_2 + Z\mathbf{e}_3$。我们可以通过计算 $G_{\Theta Z}$ 和 $g_{\Theta Z}$ 来找到剪切应变分量 $E_{\Theta Z}$。计算表明 $G_{\Theta Z}=0$ 而 $g_{\Theta Z} = kR^2$，因此剪切应变为 $E_{\Theta Z} = \frac{1}{2} kR^2$。

#### [相容性条件](@entry_id:637057)（简述）

最后，值得一提的是，并非任意一个对称的[二阶张量](@entry_id:199780)场 $\mathbf{E}(\mathbf{X})$ 都能代表一个真实、连续物体的变形。一个物理上可能的应变场必须能够从一个连续、单值的位移场 $\mathbf{u}(\mathbf{X})$ 中导出。这意味着 $\mathbf{E}$ 的六个独立分量之间必须满足一定的[微分](@entry_id:158718)约束关系，这些关系被称为**圣维南相容性条件 (Saint-Venant compatibility conditions)**。

从几何角度看，[相容性条件](@entry_id:637057)等价于要求由度量张量 $g_{IJ} = G_{IJ} + 2E_{IJ}$ 定义的物质空间是平直的（即其黎曼曲率张量为零）。如果应变场不满足[相容性条件](@entry_id:637057) [@problem_id:1547226]，那么在积分求位移时会导致矛盾，物理上意味着材料在变形过程中会产生裂纹或发生物质点的重叠。这一概念为[断裂力学](@entry_id:141480)和[位错理论](@entry_id:160051)等更高级的学科奠定了基础。