## 引言
超弹性材料，如橡胶、凝胶和生物软组织，因其承受巨大可逆变形的能力而在工程、医学和科学领域扮演着至关重要的角色。与传统金属材料不同，它们的力学响应高度非线性，小应变理论无法准确描述其行为。这就引出了一个核心挑战：如何建立一个既能精确预测其复杂应力-应变关系，又在物理上自洽的数学模型？超弹性材料建模理论正是为了解决这一问题而发展起来的，它以应变能函数的概念为基石，为分析这些软材料的行为提供了强大的框架。

本文将系统地引导读者深入超弹性材料建模的世界。我们将分三步展开：

- 在“**原则与机理**”一章中，我们将奠定理论基础，深入探讨描述大变形的运动学，揭示支配本构关系的客观性和对称性等基本原理，并掌握从应变能函数推导应力的核心数学方法。
- 接着，在“**应用与跨学科连接**”一章中，我们将把理论应用于实践，展示如何运用新胡克、穆尼-里夫林乃至各向异性的HGO等模型进行材料表征、结构分析和生物力学模拟，并探讨其在有限元分析等计算工具中的实现。
- 最后，“**动手实践**”部分将提供一系列精心设计的问题，帮助读者巩固所学知识，将理论概念转化为解决实际问题的能力。

通过本次学习，读者将构建起对超弹性力学从理论到应用的完整认识。让我们首先进入第一章，探索构建这一切的基石——超弹性建模的基本原则与机理。

## 原则与机理

在本章中，我们将深入探讨超弹性材料建模的理论核心：描述大变形的运动学框架、支配材料响应的基本本构原理，以及从应变能函数推导应力-应变关系的数学方法。这些原则和机理共同构成了分析和预测超弹性体在复杂载荷下行为的基石。

### 描述有限变形的运动学

为了精确描述材料从初始参考构型到变形后当前构型的几何变化，连续介质力学建立了一套严谨的运动学语言。其核心在于捕捉局部变形的非线性特征。

一个物体在参考构型 $\mathcal{B}_0$ 中占据的物质点，其位置由向量 $\mathbf{X}$ 描述。经过一个平滑的运动 $\boldsymbol{\varphi}$ 后，该点在当前构型 $\mathcal{B}_t$ 中的位置变为 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$。描述这一局部映射的关键物理量是**变形梯度 (deformation gradient)** $\mathbf{F}$。它被定义为空间位置 $\mathbf{x}$ 对材料位置 $\mathbf{X}$ 的梯度：
$$
\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}} = \nabla_{\mathbf{X}} \boldsymbol{\varphi}
$$
$\mathbf{F}$ 是一个二阶张量，它包含了关于局部变形（拉伸、剪切和旋转）的全部信息。它的基本作用是将参考构型中的一个无穷小线元 $d\mathbf{X}$ 映射到当前构型中的对应线元 $d\mathbf{x}$ [@problem_id:2893449]：
$$
d\mathbf{x} = \mathbf{F} \, d\mathbf{X}
$$

变形梯度 $\mathbf{F}$ 的行列式，即**雅可比行列式 (Jacobian)** $J$，具有明确的物理意义。它表示了局部体积的变化率 [@problem_id:2893449]：
$$
J = \det(\mathbf{F})
$$
一个无穷小的体积元 $dV$ 在变形后会变为 $dv = J \, dV$。由于物理上不可接受体积变为零或负值，因此必须满足 $J > 0$。当材料行为被建模为**不可压缩 (incompressible)** 时，意味着其体积在变形过程中保持不变，即 $dv = dV$，这等价于运动学约束 $J = 1$。

虽然 $\mathbf{F}$ 完整地描述了变形，但它本身并非一个纯粹的“应变”度量，因为它包含了刚体转动。为了得到只反映拉伸和剪切的度量，我们引入了柯西-格林张量。**右柯西-格林张量 (right Cauchy-Green tensor)** $\mathbf{C}$ 定义在参考构型上：
$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}
$$
它通过比较参考构型和当前构型中线元的平方长度来度量应变。一个线元 $d\mathbf{X}$ 在变形前的平方长度为 $ds_0^2 = d\mathbf{X} \cdot d\mathbf{X}$，变形后的平方长度为 $ds^2 = d\mathbf{x} \cdot d\mathbf{x}$。利用 $d\mathbf{x} = \mathbf{F}d\mathbf{X}$，我们得到：
$$
ds^2 = (\mathbf{F}d\mathbf{X}) \cdot (\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{F}^{\mathsf{T}}\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{C}d\mathbf{X})
$$
可见，$\mathbf{C}$ 直接将参考线元与其变形后的长度联系起来，是一个纯粹的应变度量，且不受叠加在变形之上的刚体转动的影响 [@problem_id:2893449]。其特征值是主拉伸比的平方。相应地，定义在当前构型上的**左柯西-格林张量 (left Cauchy-Green tensor)** $\mathbf{B}$ 为：
$$
\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}}
$$
$\mathbf{B}$ 和 $\mathbf{C}$ 具有相同的特征值，它们是彼此通过变形映射关联的应变度量。

为了具体理解这些量，我们考虑一个均匀的三轴拉伸问题 [@problem_id:2893490]。设一个立方体沿其主轴方向被拉伸，主拉伸比分别为 $\lambda_1, \lambda_2, \lambda_3$。其运动可以描述为 $x_1 = \lambda_1 X_1, x_2 = \lambda_2 X_2, x_3 = \lambda_3 X_3$。据此，我们可以计算出：
- **变形梯度** $\mathbf{F}$：
$$
\mathbf{F} = \begin{pmatrix} \lambda_1 & 0 & 0 \\ 0 & \lambda_2 & 0 \\ 0 & 0 & \lambda_3 \end{pmatrix}
$$
- **右柯西-格林张量** $\mathbf{C}$ 和 **左柯西-格林张量** $\mathbf{B}$：
$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}} = \begin{pmatrix} \lambda_1^2 & 0 & 0 \\ 0 & \lambda_2^2 & 0 \\ 0 & 0 & \lambda_3^2 \end{pmatrix}
$$
- **雅可比行列式** $J$：
$$
J = \det(\mathbf{F}) = \lambda_1 \lambda_2 \lambda_3
$$

这些张量的不变量在构建本构模型时至关重要。对于一个二阶张量（如 $\mathbf{C}$），其三个**主不变量 (principal invariants)** 分别是：
$$
I_1(\mathbf{C}) = \mathrm{tr}(\mathbf{C})
$$
$$
I_2(\mathbf{C}) = \frac{1}{2}[(\mathrm{tr}(\mathbf{C}))^2 - \mathrm{tr}(\mathbf{C}^2)]
$$
$$
I_3(\mathbf{C}) = \det(\mathbf{C})
$$
对于上述三轴拉伸的例子，这些不变量为 [@problem_id:2893490]：
$$
I_1 = \lambda_1^2 + \lambda_2^2 + \lambda_3^2
$$
$$
I_2 = \lambda_1^2\lambda_2^2 + \lambda_2^2\lambda_3^2 + \lambda_3^2\lambda_1^2
$$
$$
I_3 = \lambda_1^2\lambda_2^2\lambda_3^2 = J^2
$$
最后一个关系，$I_3 = J^2$，是普遍成立的。

### 基本本构原理

超弹性材料的本构关系（即应力-应变关系）并非任意形式，它必须遵循若干基本物理原理，这些原理约束了应变能函数的数学形式。

#### 材料坐标系无关性原理

**材料坐标系无关性原理 (Principle of Material Frame Indifference)**，或称**客观性原理 (objectivity)**，是本构理论的基石。该原理指出，材料的本构响应（如应力或储存的能量）不应依赖于观察者。换言之，本构方程的形式在所有（刚性运动的）坐标系下都应相同 [@problem_id:2893468]。

考虑一个已发生的变形 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X})$，其变形梯度为 $\mathbf{F}$。现在，让一个观察者相对于当前构型做一次刚体运动，包括一个平移 $\mathbf{c}(t)$ 和一个旋转 $\mathbf{Q}(t)$（其中 $\mathbf{Q} \in \mathrm{SO}(3)$ 是一个真 正交张量）。新观察者看到的位置为 $\mathbf{x}^* = \mathbf{c}(t) + \mathbf{Q}(t)\mathbf{x}$。该叠加运动导致的变形梯度为：
$$
\mathbf{F}^* = \nabla_{\mathbf{X}}\mathbf{x}^* = \mathbf{Q}\nabla_{\mathbf{X}}\mathbf{x} = \mathbf{Q}\mathbf{F}
$$
超弹性材料的应变能密度函数 $W$ 是一个标量，其值是材料的内在属性，不应随观察者而改变。因此，必须满足 $W(\mathbf{F}^*) = W(\mathbf{F})$，即：
$$
W(\mathbf{Q}\mathbf{F}) = W(\mathbf{F}), \quad \forall \mathbf{Q} \in \mathrm{SO}(3)
$$
为了满足这一要求，应变能函数 $W$ 不能直接依赖于包含旋转信息的 $\mathbf{F}$。一个在 $\mathbf{F} \to \mathbf{Q}\mathbf{F}$ 变换下保持不变的量是右柯西-格林张量 $\mathbf{C}$，因为：
$$
\mathbf{C}^* = (\mathbf{F}^*)^{\mathsf{T}}\mathbf{F}^* = (\mathbf{Q}\mathbf{F})^{\mathsf{T}}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^{\mathsf{T}}\mathbf{Q}^{\mathsf{T}}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\mathsf{T}}\mathbf{I}\mathbf{F} = \mathbf{C}
$$
因此，客观性原理的直接推论是，应变能函数必须只能通过右柯西-格林张量 $\mathbf{C}$ 来依赖于变形，即存在一个函数 $\widehat{W}$ 使得 $W = \widehat{W}(\mathbf{C})$ [@problem_id:2893468] [@problem_id:2893449]。这一结论极大地简化了本构模型的构建。

#### 材料对称性

材料的内部微观结构决定了其宏观力学响应的对称性。**材料对称性 (material symmetry)** 原理指出，本构函数的形式必须在反映材料对称性的坐标变换下保持不变。

对于**各向同性 (isotropic)** 材料，其力学属性在所有方向上都是相同的。这意味着应变能函数在参考构型的任意刚体旋转下都应保持不变。数学上，这要求对于任意旋转张量 $\mathbf{Q} \in \mathrm{SO}(3)$，都有 $\widehat{W}(\mathbf{Q}\mathbf{C}\mathbf{Q}^{\mathsf{T}}) = \widehat{W}(\mathbf{C})$。满足此条件的函数被称为各向同性张量函数。根据由 Cauchy、Rivlin 和 Ericksen 等人建立的**表示定理 (representation theorem)**，一个关于对称二阶张量 $\mathbf{C}$ 的各向同性标量函数，必定可以表示为其三个主不变量 $I_1, I_2, I_3$ 的函数 [@problem_id:2893433]：
$$
W = \widehat{W}(I_1, I_2, I_3)
$$
这为各向同性超弹性材料（如橡胶）的建模提供了理论基础，我们只需找到以不变量为变量的函数形式即可。

对于**各向异性 (anisotropic)** 材料，例如生物软组织或纤维增强复合材料，其对称性较低。以**横观各向同性 (transversely isotropic)** 材料为例，它在一个优选方向（例如纤维方向，由单位向量 $\mathbf{a}_0$ 表示）上具有旋转对称性。为了描述这种材料，我们需要引入额外的结构张量，通常是 $\mathbf{A}_0 = \mathbf{a}_0 \otimes \mathbf{a}_0$。此时，应变能函数 $W$ 必须是 $\mathbf{C}$ 和 $\mathbf{A}_0$ 的各向同性函数。表示定理表明，$W$ 可以表示为一个最小不变量集合的函数。对于可压缩横观各向同性材料，这个集合通常包含五个不变量 [@problem_id:2893439]：
- $I_1, I_2, I_3$: 与各向同性基体材料响应相关的三个基本不变量。
- $I_4 = \mathbf{a}_0 \cdot \mathbf{C}\mathbf{a}_0 = \| \mathbf{F}\mathbf{a}_0 \|^2$: 纤维方向拉伸比的平方，直接度量纤维的伸长。
- $I_5 = \mathbf{a}_0 \cdot \mathbf{C}^2\mathbf{a}_0$: 耦合不变量，它对纤维方向与周围基体之间的剪切变形敏感，使得模型能够区分具有相同纤维拉伸但剪切状态不同的变形。

### 应力、应变能与本构关系

建立了应变能函数的合理形式后，下一步是从中导出应力。这需要我们理解不同应力张量的定义及其与应变率的功共轭关系。

#### 四种基本应力张量

在有限变形理论中，根据力、面积和构型的不同定义，有多种应力张量 [@problem_id:2893483]：
1.  **柯西应力 (Cauchy stress)** $\boldsymbol{\sigma}$: 这是物理上最直观的“真实”应力。它定义在**当前构型**上，表示单位**当前面积**上的力。在没有体力矩的情况下，角动量守恒要求 $\boldsymbol{\sigma}$ 是对称的。
2.  **第一类皮奥拉-基尔霍夫应力 (First Piola-Kirchhoff stress)** $\mathbf{P}$: 也称为**名义应力 (nominal stress)**。它是一个“两点”张量，将作用在**当前构型**上的力关联到**参考构型**的面积上。即，单位**参考面积**上的力。$\mathbf{P}$ 通常是非对称的。
3.  **第二类皮奥拉-基尔霍夫应力 (Second Piola-Kirchhoff stress)** $\mathbf{S}$: 这是一个完全定义在**参考构型**上的应力张量。它通过一个映射将力从当前构型“拉回”到参考构型。$\mathbf{S}$ 是对称的，使其在理论推导中非常有用。
4.  **基尔霍夫应力 (Kirchhoff stress)** $\boldsymbol{\tau}$: 定义为 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$。它与柯西应力一样是定义在当前构型上的对称张量。在不可压缩情况下（$J=1$），它与柯西应力相等。

这些应力张量之间可以通过变形梯度 $\mathbf{F}$ 进行转换。最基本的关系是：
$$
\mathbf{P} = J\boldsymbol{\sigma}\mathbf{F}^{-\mathsf{T}} \quad \text{和} \quad \mathbf{P} = \mathbf{F}\mathbf{S}
$$
由这两个关系可以推导出所有应力之间的转换公式，例如 $\mathbf{S} = J\mathbf{F}^{-1}\boldsymbol{\sigma}\mathbf{F}^{-\mathsf{T}}$。

#### 功共轭与本构推导

这些应力度量的价值在于它们分别与某个应变率度量是**功共轭 (work-conjugate)** 的。这意味着两者的缩并（内积）给出了单位体积的功率。单位参考体积的功率 $\mathcal{P}_V$ 可以表示为以下等价形式 [@problem_id:2893483]：
$$
\mathcal{P}_V = \mathbf{P} : \dot{\mathbf{F}} = \mathbf{S} : \dot{\mathbf{E}} = \boldsymbol{\tau} : \mathbf{d}
$$
其中 $\dot{\mathbf{F}}$ 是变形梯度的物质时间导数，$\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})$ 是格林-拉格朗日应变张量，$\mathbf{d} = \mathrm{sym}(\dot{\mathbf{F}}\mathbf{F}^{-1})$ 是空间速度梯度的对称部分，即变形率张量。

对于超弹性材料，功率消耗等于应变能的变化率，即 $\mathcal{P}_V = \dot{W}$。若 $W = \widehat{W}(\mathbf{C})$，则 $\dot{W} = (\partial \widehat{W} / \partial \mathbf{C}) : \dot{\mathbf{C}}$。利用 $\dot{\mathbf{C}} = 2\dot{\mathbf{E}}$ 和 $\mathcal{P}_V = \mathbf{S} : \dot{\mathbf{E}}$，我们立即得到第二类皮奥拉-基尔霍夫应力的本构关系：
$$
\mathbf{S} = 2 \frac{\partial \widehat{W}}{\partial \mathbf{C}}
$$
这是从应变能函数计算应力的核心公式。一旦求得 $\mathbf{S}$，其他应力张量就可以通过转换公式得到：
$$
\mathbf{P} = \mathbf{F}\mathbf{S} = 2\mathbf{F}\frac{\partial \widehat{W}}{\partial \mathbf{C}}
$$
$$
\boldsymbol{\tau} = \mathbf{F}\mathbf{S}\mathbf{F}^{\mathsf{T}} = 2\mathbf{F}\frac{\partial \widehat{W}}{\partial \mathbf{C}}\mathbf{F}^{\mathsf{T}}
$$
$$
\boldsymbol{\sigma} = \frac{1}{J}\boldsymbol{\tau}
$$

### 不可压缩与可压缩材料建模

利用上述框架，我们可以为不同类型的材料行为构建具体的模型。

#### 不可压缩材料

许多类橡胶材料在变形过程中体积几乎不变，因此常被建模为不可压缩材料，即满足运动学约束 $J=1$。处理这种约束的经典方法是**拉格朗日乘子法 (Lagrange multiplier method)** [@problem_id:2893434]。我们将系统的总势能泛函增加一个约束项：
$$
\Pi = \int_{\Omega_0} [W(\mathbf{F}) - p(J-1)] \, dV
$$
其中 $p$ 是一个标量场，称为拉格朗日乘子，其物理意义是静水压力。通过变分法，可以推导出此时的应力表达式。例如，第一类皮奥拉-基尔霍夫应力变为：
$$
\mathbf{P} = \frac{\partial W}{\partial \mathbf{F}} - p\mathbf{F}^{-\mathsf{T}}
$$
柯西应力则为：
$$
\boldsymbol{\sigma} = \frac{1}{J}\mathbf{P}\mathbf{F}^{\mathsf{T}} - p\mathbf{I} = \boldsymbol{\sigma}_{\text{dev}} - p\mathbf{I}
$$
这里的 $p$ 是一个未知的静水压力，需要通过平衡方程和边界条件来确定。这种压力-偏应力的分解形式在不可压缩材料力学中非常普遍。对于不可压缩情况，$J=1$ 使得基尔霍夫应力 $\boldsymbol{\tau}$ 与柯西应力 $\boldsymbol{\sigma}$ 相等，其本构关系能够清晰地分离压力项和由应变能决定的偏应力项，因此在计算中尤为方便 [@problem_id:2893488]。

**示例：不可压缩新胡克材料的单轴拉伸** [@problem_id:2893434]
考虑一个不可压缩新胡克模型，其应变能函数为 $W = \frac{\mu}{2}(I_1-3)$，其中 $\mu$ 是剪切模量。对于沿 $X_1$ 方向的单轴拉伸，变形梯度为 $\mathbf{F} = \mathrm{diag}(\lambda, \lambda^{-1/2}, \lambda^{-1/2})$ 以满足 $J=1$。通过在侧面施加名义牵引力为零的边界条件 ($P_{22}=P_{33}=0$)，我们可以求解出静水压力 $p=\mu\lambda^{-1}$。进而，可以得到产生该变形所需的轴向名义应力 $T_0$：
$$
T_0 = P_{11} = \mu\lambda - p\lambda^{-1} = \mu(\lambda - \lambda^{-2})
$$
这个经典结果将材料参数 $\mu$ 与宏观的力-伸长响应直接联系起来。

**示例：不可压缩新胡克材料的纯剪切** [@problem_id:2893488]
对于纯剪切变形，变形梯度为 $\mathbf{F} = \begin{pmatrix} 1 & \gamma & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}$，其中 $\gamma$ 是剪切应变量。这种变形是等体积的（$J=1$）。利用公式 $\boldsymbol{\tau} = 2\mathbf{F}(\partial W / \partial \mathbf{C})\mathbf{F}^{\mathsf{T}}$，可以计算出新胡克材料的基尔霍夫剪切应力分量：
$$
\tau_{12} = \mu\gamma
$$
这个线性关系表明，对于纯剪切，新胡克模型表现出与小变形理论相似的胡克定律行为。

#### 可压缩材料与等体积-体积分解

对于可压缩材料，一种常见的建模策略是将变形和应变能函数进行**等体积-体积分解 (isochoric-volumetric decomposition)**。其思想是，材料的响应可以分为改变形状（等体积或偏）的部分和改变体积的部分。

为此，我们将变形梯度 $\mathbf{F}$ 分解为一个体积改变部分和一个保体积部分 $\overline{\mathbf{F}}$：
$$
\mathbf{F} = J^{1/3}\mathbf{I} \cdot \overline{\mathbf{F}}, \quad \text{其中} \quad \det(\overline{\mathbf{F}}) = 1
$$
相应地，右柯西-格林张量 $\mathbf{C}$ 也可被分解：
$$
\overline{\mathbf{C}} = J^{-2/3}\mathbf{C}, \quad \text{其中} \quad \det(\overline{\mathbf{C}}) = 1
$$
$\overline{\mathbf{C}}$ 捕捉了纯粹的形状变化。然后，应变能函数可以假设为体积部分和等体积部分之和：
$$
W = W_{\text{vol}}(J) + W_{\text{iso}}(\overline{I}_1, \overline{I}_2)
$$
其中 $\overline{I}_1$ 和 $\overline{I}_2$ 是 $\overline{\mathbf{C}}$ 的主不变量。它们与 $\mathbf{C}$ 的不变量 $I_1, I_2$ 之间存在简单的关系 [@problem_id:2893467]：
$$
\overline{I}_1 = \mathrm{tr}(\overline{\mathbf{C}}) = J^{-2/3}I_1
$$
$$
\overline{I}_2 = \frac{1}{2}[(\mathrm{tr}(\overline{\mathbf{C}}))^2 - \mathrm{tr}(\overline{\mathbf{C}}^2)] = J^{-4/3}I_2
$$
这种分解方法在为近不可压缩材料（如生物组织）建模时特别有效，因为它能清晰地分离体积响应（通常非常刚硬）和剪切响应。

### 物理与数学适定性的基础

并非任何形式的应变能函数 $W(\mathbf{F})$ 都是物理上合理或数学上适定的。一个物理上稳定的材料在受力变形时其能量应该增加。从数学角度看，为了保证基于能量最小化原理的边值问题存在唯一且稳定的解， $W$ 需要满足一定的**凸性 (convexity)** 条件。

在非线性弹性理论中，普通的凸性条件过于严苛，无法描述真实材料的剪切和压缩行为。因此，数学家们引入了更弱的凸性概念 [@problem_id:2893454]：
- **秩一凸性 (Rank-one convexity)**: 要求 $W$ 在任何秩一方向上的函数都是凸的。这是材料免于出现微观失稳（如剪切带）的必要条件。
- **拟凸性 (Quasiconvexity)**: 一个非局域的平均化条件，它是保证能量泛函弱下半连续性的充要条件，从而确保通过变分法直接法求得的极小值解存在。
- **多凸性 (Polyconvexity)**: 一个比拟凸性更强但更易于验证的条件。它要求 $W$ 可以表示为变形梯度 $\mathbf{F}$ 及其所有子行列式（在三维中即 $\mathbf{F}$, $\mathrm{cof}(\mathbf{F})$, $\det(\mathbf{F})$）的一个凸函数。

这些凸性概念之间存在严格的蕴含关系：
$$
\text{凸性} \implies \text{多凸性} \implies \text{拟凸性} \implies \text{秩一凸性}
$$
反向的蕴含关系通常不成立。在现代超弹性理论中，多凸性扮演着核心角色。由 J.M. Ball 发展的理论表明，如果一个应变能函数是多凸的，满足一定的增长和强制性条件，并且在体积趋于零时能量趋于无穷大（形成一个“屏障”），那么相应的弹性静力学边值问题就保证存在能量极小值解 [@problem_id:2893454]。这一理论不仅为数值模拟的稳定性提供了坚实的基础，也指导了如何构建物理上和数学上都“表现良好”的本构模型。