## 引言
[超弹性材料](@entry_id:190241)，如橡胶、凝胶和生物软组织，因其承受巨大可逆变形的能力而在工程、医学和科学领域扮演着至关重要的角色。与传统金属材料不同，它们的力学响应高度[非线性](@entry_id:637147)，小应变理论无法准确描述其行为。这就引出了一个核心挑战：如何建立一个既能精确预测其复杂[应力-应变关系](@entry_id:274093)，又在物理上自洽的数学模型？[超弹性材料](@entry_id:190241)建模理论正是为了解决这一问题而发展起来的，它以[应变能函数](@entry_id:178435)的概念为基石，为分析这些软材料的行为提供了强大的框架。

本文将系统地引导读者深入[超弹性材料](@entry_id:190241)建模的世界。我们将分三步展开：

- 在“**原则与机理**”一章中，我们将奠定理论基础，深入探讨描述大变形的运动学，揭示支配[本构关系](@entry_id:186508)的客观性和对称性等基本原理，并掌握从[应变能函数](@entry_id:178435)推导应力的核心数学方法。
- 接着，在“**应用与跨学科连接**”一章中，我们将把理论应用于实践，展示如何运用新胡克、穆尼-里夫林乃至各向异性的HGO等模型进行[材料表征](@entry_id:161346)、[结构分析](@entry_id:153861)和[生物力学](@entry_id:153973)模拟，并探讨其在[有限元分析](@entry_id:138109)等计算工具中的实现。
- 最后，“**动手实践**”部分将提供一系列精心设计的问题，帮助读者巩固所学知识，将理论概念转化为解决实际问题的能力。

通过本次学习，读者将构建起对超弹性力学从理论到应用的完整认识。让我们首先进入第一章，探索构建这一切的基石——[超弹性](@entry_id:159356)建[模的基](@entry_id:156416)本原则与机理。

## 原则与机理

在本章中，我们将深入探讨[超弹性材料](@entry_id:190241)建模的理论核心：描述[大变形](@entry_id:167243)的[运动学](@entry_id:173318)框架、支配材料响应的基本本构原理，以及从[应变能函数](@entry_id:178435)推导[应力-应变关系](@entry_id:274093)的数学方法。这些原则和机理共同构成了分析和预测超弹性体在复杂载荷下行为的基石。

### 描述有限变形的运动学

为了精确描述材料从初始参考构型到变形后当前构型的几何变化，[连续介质力学](@entry_id:155125)建立了一套严谨的[运动学](@entry_id:173318)语言。其核心在于捕捉局部变形的[非线性](@entry_id:637147)特征。

一个物体在参考构型 $\mathcal{B}_0$ 中占据的物质点，其位置由向量 $\mathbf{X}$ 描述。经过一个平滑的运动 $\boldsymbol{\varphi}$ 后，该点在当前构型 $\mathcal{B}_t$ 中的位置变为 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$。描述这一局部映射的关键物理量是**变形梯度 (deformation gradient)** $\mathbf{F}$。它被定义为空间位置 $\mathbf{x}$ 对材料位置 $\mathbf{X}$ 的梯度：
$$
\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}} = \nabla_{\mathbf{X}} \boldsymbol{\varphi}
$$
$\mathbf{F}$ 是一个[二阶张量](@entry_id:199780)，它包含了关于局部变形（拉伸、剪切和旋转）的全部信息。它的基本作用是将参考构型中的一个无穷小线元 $d\mathbf{X}$ 映射到当前构型中的对应[线元](@entry_id:196833) $d\mathbf{x}$ [@problem_id:2893449]：
$$
d\mathbf{x} = \mathbf{F} \, d\mathbf{X}
$$

变形梯度 $\mathbf{F}$ 的[行列式](@entry_id:142978)，即**[雅可比行列式](@entry_id:137120) (Jacobian)** $J$，具有明确的物理意义。它表示了局部体积的变化率 [@problem_id:2893449]：
$$
J = \det(\mathbf{F})
$$
一个无穷小的[体积元](@entry_id:267802) $dV$ 在变形后会变为 $dv = J \, dV$。由于物理上不可接受体积变为零或负值，因此必须满足 $J > 0$。当材料行为被建模为**不可压缩 (incompressible)** 时，意味着其体积在变形过程中保持不变，即 $dv = dV$，这等价于[运动学](@entry_id:173318)约束 $J = 1$。

虽然 $\mathbf{F}$ 完整地描述了变形，但它本身并非一个纯粹的“应变”度量，因为它包含了[刚体转动](@entry_id:191086)。为了得到只反映拉伸和剪切的度量，我们引入了柯西-格林张量。**[右柯西-格林张量](@entry_id:174156) (right Cauchy-Green tensor)** $\mathbf{C}$ 定义在参考构型上：
$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}
$$
它通过比较参考构型和当前构型中[线元](@entry_id:196833)的平方长度来度量应变。一个[线元](@entry_id:196833) $d\mathbf{X}$ 在变形前的平方长度为 $ds_0^2 = d\mathbf{X} \cdot d\mathbf{X}$，变形后的平方长度为 $ds^2 = d\mathbf{x} \cdot d\mathbf{x}$。利用 $d\mathbf{x} = \mathbf{F}d\mathbf{X}$，我们得到：
$$
ds^2 = (\mathbf{F}d\mathbf{X}) \cdot (\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{F}^{\mathsf{T}}\mathbf{F}d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{C}d\mathbf{X})
$$
可见，$\mathbf{C}$ 直接将参考线元与其变形后的长度联系起来，是一个纯粹的[应变度量](@entry_id:755495)，且不受叠加在变形之上的[刚体转动](@entry_id:191086)的影响 [@problem_id:2893449]。其[特征值](@entry_id:154894)是主拉伸比的平方。相应地，定义在当前构型上的**[左柯西-格林张量](@entry_id:186163) (left Cauchy-Green tensor)** $\mathbf{B}$ 为：
$$
\mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}}
$$
$\mathbf{B}$ 和 $\mathbf{C}$ 具有相同的[特征值](@entry_id:154894)，它们是彼此通过变形映射关联的[应变度量](@entry_id:755495)。

为了具体理解这些量，我们考虑一个均匀的三轴拉伸问题 [@problem_id:2893490]。设一个立方体沿其[主轴](@entry_id:172691)方向被拉伸，主拉伸比分别为 $\lambda_1, \lambda_2, \lambda_3$。其运动可以描述为 $x_1 = \lambda_1 X_1, x_2 = \lambda_2 X_2, x_3 = \lambda_3 X_3$。据此，我们可以计算出：
- **变形梯度** $\mathbf{F}$：
$$
\mathbf{F} = \begin{pmatrix} \lambda_1 & 0 & 0 \\ 0 & \lambda_2 & 0 \\ 0 & 0 & \lambda_3 \end{pmatrix}
$$
- **[右柯西-格林张量](@entry_id:174156)** $\mathbf{C}$ 和 **[左柯西-格林张量](@entry_id:186163)** $\mathbf{B}$：
$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F} = \mathbf{B} = \mathbf{F}\mathbf{F}^{\mathsf{T}} = \begin{pmatrix} \lambda_1^2 & 0 & 0 \\ 0 & \lambda_2^2 & 0 \\ 0 & 0 & \lambda_3^2 \end{pmatrix}
$$
- **[雅可比行列式](@entry_id:137120)** $J$：
$$
J = \det(\mathbf{F}) = \lambda_1 \lambda_2 \lambda_3
$$

这些张量的[不变量](@entry_id:148850)在构建[本构模型](@entry_id:174726)时至关重要。对于一个[二阶张量](@entry_id:199780)（如 $\mathbf{C}$），其三个**[主不变量](@entry_id:193522) (principal invariants)** 分别是：
$$
I_1(\mathbf{C}) = \mathrm{tr}(\mathbf{C})
$$
$$
I_2(\mathbf{C}) = \frac{1}{2}[(\mathrm{tr}(\mathbf{C}))^2 - \mathrm{tr}(\mathbf{C}^2)]
$$
$$
I_3(\mathbf{C}) = \det(\mathbf{C})
$$
对于上述三轴拉伸的例子，这些[不变量](@entry_id:148850)为 [@problem_id:2893490]：
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

[超弹性材料](@entry_id:190241)的本构关系（即[应力-应变关系](@entry_id:274093)）并非任意形式，它必须遵循若干基本物理原理，这些原理约束了[应变能函数](@entry_id:178435)的数学形式。

#### 材料[坐标系](@entry_id:156346)无关性原理

**材料[坐标系](@entry_id:156346)无关性原理 (Principle of Material Frame Indifference)**，或称**[客观性原理](@entry_id:185412) (objectivity)**，是本构理论的基石。该原理指出，材料的本构响应（如应力或储存的能量）不应依赖于观察者。换言之，[本构方程](@entry_id:138559)的形式在所有（[刚性运动](@entry_id:170523)的）[坐标系](@entry_id:156346)下都应相同 [@problem_id:2893468]。

考虑一个已发生的变形 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X})$，其变形梯度为 $\mathbf{F}$。现在，让一个观察者相对于当前构型做一次刚体运动，包括一个平移 $\mathbf{c}(t)$ 和一个旋转 $\mathbf{Q}(t)$（其中 $\mathbf{Q} \in \mathrm{SO}(3)$ 是一个真 正交张量）。新观察者看到的位置为 $\mathbf{x}^* = \mathbf{c}(t) + \mathbf{Q}(t)\mathbf{x}$。该叠加运动导致的变形梯度为：
$$
\mathbf{F}^* = \nabla_{\mathbf{X}}\mathbf{x}^* = \mathbf{Q}\nabla_{\mathbf{X}}\mathbf{x} = \mathbf{Q}\mathbf{F}
$$
[超弹性材料](@entry_id:190241)的[应变能密度函数](@entry_id:755490) $W$ 是一个标量，其值是材料的内在属性，不应随观察者而改变。因此，必须满足 $W(\mathbf{F}^*) = W(\mathbf{F})$，即：
$$
W(\mathbf{Q}\mathbf{F}) = W(\mathbf{F}), \quad \forall \mathbf{Q} \in \mathrm{SO}(3)
$$
为了满足这一要求，[应变能函数](@entry_id:178435) $W$ 不能直接依赖于包含旋转信息的 $\mathbf{F}$。一个在 $\mathbf{F} \to \mathbf{Q}\mathbf{F}$ 变换下保持不变的量是[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$，因为：
$$
\mathbf{C}^* = (\mathbf{F}^*)^{\mathsf{T}}\mathbf{F}^* = (\mathbf{Q}\mathbf{F})^{\mathsf{T}}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^{\mathsf{T}}\mathbf{Q}^{\mathsf{T}}\mathbf{Q}\mathbf{F} = \mathbf{F}^{\mathsf{T}}\mathbf{I}\mathbf{F} = \mathbf{C}
$$
因此，[客观性原理](@entry_id:185412)的直接推论是，[应变能函数](@entry_id:178435)必须只能通过[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 来依赖于变形，即存在一个函数 $\widehat{W}$ 使得 $W = \widehat{W}(\mathbf{C})$ [@problem_id:2893468] [@problem_id:2893449]。这一结论极大地简化了[本构模型](@entry_id:174726)的构建。

#### [材料对称性](@entry_id:190289)

材料的内部微观结构决定了其宏观力学响应的对称性。**[材料对称性](@entry_id:190289) (material symmetry)** 原理指出，本构函数的形式必须在反映[材料对称性](@entry_id:190289)的[坐标变换](@entry_id:172727)下保持不变。

对于**各向同性 (isotropic)** 材料，其力学属性在所有方向上都是相同的。这意味着[应变能函数](@entry_id:178435)在参考构型的任意刚体旋转下都应保持不变。数学上，这要求对于任意[旋转张量](@entry_id:191990) $\mathbf{Q} \in \mathrm{SO}(3)$，都有 $\widehat{W}(\mathbf{Q}\mathbf{C}\mathbf{Q}^{\mathsf{T}}) = \widehat{W}(\mathbf{C})$。满足此条件的函数被称为[各向同性张量](@entry_id:195105)函数。根据由 Cauchy、Rivlin 和 Ericksen 等人建立的**[表示定理](@entry_id:637872) (representation theorem)**，一个关于对称二阶张量 $\mathbf{C}$ 的各向同性标量函数，必定可以表示为其三个[主不变量](@entry_id:193522) $I_1, I_2, I_3$ 的函数 [@problem_id:2893433]：
$$
W = \widehat{W}(I_1, I_2, I_3)
$$
这为各向同性[超弹性材料](@entry_id:190241)（如橡胶）的建模提供了理论基础，我们只需找到以[不变量](@entry_id:148850)为变量的函数形式即可。

对于**各向异性 (anisotropic)** 材料，例如生物软组织或[纤维增强复合材料](@entry_id:194995)，其对称性较低。以**横观各向同性 (transversely isotropic)** 材料为例，它在一个优选方向（例如纤维方向，由单位向量 $\mathbf{a}_0$ 表示）上具有[旋转对称](@entry_id:137077)性。为了描述这种材料，我们需要引入额外的结构张量，通常是 $\mathbf{A}_0 = \mathbf{a}_0 \otimes \mathbf{a}_0$。此时，[应变能函数](@entry_id:178435) $W$ 必须是 $\mathbf{C}$ 和 $\mathbf{A}_0$ 的[各向同性函数](@entry_id:750877)。[表示定理](@entry_id:637872)表明，$W$ 可以表示为一个最小[不变量](@entry_id:148850)集合的函数。对于可压缩横观各向同性材料，这个集合通常包含五个[不变量](@entry_id:148850) [@problem_id:2893439]：
- $I_1, I_2, I_3$: 与各向同性基体材料响应相关的三个基本[不变量](@entry_id:148850)。
- $I_4 = \mathbf{a}_0 \cdot \mathbf{C}\mathbf{a}_0 = \| \mathbf{F}\mathbf{a}_0 \|^2$: 纤维方向拉伸比的平方，直接度量纤维的伸长。
- $I_5 = \mathbf{a}_0 \cdot \mathbf{C}^2\mathbf{a}_0$: 耦合[不变量](@entry_id:148850)，它对纤维方向与周围基体之间的剪切变形敏感，使得模型能够区分具有相同纤维拉伸但剪切状态不同的变形。

### 应力、[应变能](@entry_id:162699)与[本构关系](@entry_id:186508)

建立了[应变能函数](@entry_id:178435)的合理形式后，下一步是从中导出应力。这需要我们理解不同应力张量的定义及其与应变率的[功共轭](@entry_id:194957)关系。

#### 四种基本应力张量

在有限变形理论中，根据力、面积和构型的不同定义，有多种应力张量 [@problem_id:2893483]：
1.  **柯西应力 (Cauchy stress)** $\boldsymbol{\sigma}$: 这是物理上最直观的“真实”应力。它定义在**当前构型**上，表示单位**当前面积**上的力。在没有[体力](@entry_id:174230)矩的情况下，[角动量守恒](@entry_id:156798)要求 $\boldsymbol{\sigma}$ 是对称的。
2.  **第一类[皮奥拉-基尔霍夫应力](@entry_id:173629) (First Piola-Kirchhoff stress)** $\mathbf{P}$: 也称为**名义应力 (nominal stress)**。它是一个“两点”张量，将作用在**当前构型**上的力关联到**参考构型**的面积上。即，单位**参考面积**上的力。$\mathbf{P}$ 通常是非对称的。
3.  **第二类[皮奥拉-基尔霍夫应力](@entry_id:173629) (Second Piola-Kirchhoff stress)** $\mathbf{S}$: 这是一个完全定义在**参考构型**上的应力张量。它通过一个映射将力从当前构型“[拉回](@entry_id:160816)”到参考构型。$\mathbf{S}$ 是对称的，使其在理论推导中非常有用。
4.  **[基尔霍夫应力](@entry_id:751039) (Kirchhoff stress)** $\boldsymbol{\tau}$: 定义为 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$。它与柯西应力一样是定义在当前构型上的[对称张量](@entry_id:148092)。在不可压缩情况下（$J=1$），它与柯西应力相等。

这些应力张量之间可以通过变形梯度 $\mathbf{F}$ 进行转换。最基本的关系是：
$$
\mathbf{P} = J\boldsymbol{\sigma}\mathbf{F}^{-\mathsf{T}} \quad \text{和} \quad \mathbf{P} = \mathbf{F}\mathbf{S}
$$
由这两个关系可以推导出所有应力之间的转换公式，例如 $\mathbf{S} = J\mathbf{F}^{-1}\boldsymbol{\sigma}\mathbf{F}^{-\mathsf{T}}$。

#### [功共轭](@entry_id:194957)与本构推导

这些应力度量的价值在于它们分别与某个[应变率](@entry_id:154778)度量是**[功共轭](@entry_id:194957) (work-conjugate)** 的。这意味着两者的缩并（[内积](@entry_id:158127)）给出了单位体积的功率。单位参考体积的功率 $\mathcal{P}_V$ 可以表示为以下等价形式 [@problem_id:2893483]：
$$
\mathcal{P}_V = \mathbf{P} : \dot{\mathbf{F}} = \mathbf{S} : \dot{\mathbf{E}} = \boldsymbol{\tau} : \mathbf{d}
$$
其中 $\dot{\mathbf{F}}$ 是变形梯度的[物质时间导数](@entry_id:190892)，$\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})$ 是[格林-拉格朗日应变张量](@entry_id:187745)，$\mathbf{d} = \mathrm{sym}(\dot{\mathbf{F}}\mathbf{F}^{-1})$ 是[空间速度梯度](@entry_id:187198)的对称部分，即变形率张量。

对于[超弹性材料](@entry_id:190241)，功率消耗等于应变能的变化率，即 $\mathcal{P}_V = \dot{W}$。若 $W = \widehat{W}(\mathbf{C})$，则 $\dot{W} = (\partial \widehat{W} / \partial \mathbf{C}) : \dot{\mathbf{C}}$。利用 $\dot{\mathbf{C}} = 2\dot{\mathbf{E}}$ 和 $\mathcal{P}_V = \mathbf{S} : \dot{\mathbf{E}}$，我们立即得到第二类[皮奥拉-基尔霍夫应力](@entry_id:173629)的本构关系：
$$
\mathbf{S} = 2 \frac{\partial \widehat{W}}{\partial \mathbf{C}}
$$
这是从[应变能函数](@entry_id:178435)计算应力的核心公式。一旦求得 $\mathbf{S}$，其他[应力张量](@entry_id:148973)就可以通过转换公式得到：
$$
\mathbf{P} = \mathbf{F}\mathbf{S} = 2\mathbf{F}\frac{\partial \widehat{W}}{\partial \mathbf{C}}
$$
$$
\boldsymbol{\tau} = \mathbf{F}\mathbf{S}\mathbf{F}^{\mathsf{T}} = 2\mathbf{F}\frac{\partial \widehat{W}}{\partial \mathbf{C}}\mathbf{F}^{\mathsf{T}}
$$
$$
\boldsymbol{\sigma} = \frac{1}{J}\boldsymbol{\tau}
$$

### 不可压缩与可压缩[材料建模](@entry_id:751724)

利用上述框架，我们可以为不同类型的材料行为构建具体的模型。

#### [不可压缩材料](@entry_id:159741)

许多类橡胶材料在变形过程中体积几乎不变，因此常被建模为[不可压缩材料](@entry_id:159741)，即满足运动学约束 $J=1$。处理这种约束的经典方法是**拉格朗日乘子法 (Lagrange multiplier method)** [@problem_id:2893434]。我们将系统的总势能泛函增加一个约束项：
$$
\Pi = \int_{\Omega_0} [W(\mathbf{F}) - p(J-1)] \, dV
$$
其中 $p$ 是一个标量场，称为[拉格朗日乘子](@entry_id:142696)，其物理意义是静水压力。通过变分法，可以推导出此时的应力表达式。例如，第一类[皮奥拉-基尔霍夫应力](@entry_id:173629)变为：
$$
\mathbf{P} = \frac{\partial W}{\partial \mathbf{F}} - p\mathbf{F}^{-\mathsf{T}}
$$
柯西应力则为：
$$
\boldsymbol{\sigma} = \frac{1}{J}\mathbf{P}\mathbf{F}^{\mathsf{T}} - p\mathbf{I} = \boldsymbol{\sigma}_{\text{dev}} - p\mathbf{I}
$$
这里的 $p$ 是一个未知的静水压力，需要通过平衡方程和边界条件来确定。这种压力-偏应力的分解形式在[不可压缩材料](@entry_id:159741)力学中非常普遍。对于不可压缩情况，$J=1$ 使得[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau}$ 与柯西应力 $\boldsymbol{\sigma}$ 相等，其本构关系能够清晰地分离压力项和由[应变能](@entry_id:162699)决定的[偏应力](@entry_id:163323)项，因此在计算中尤为方便 [@problem_id:2893488]。

**示例：不可压缩新胡克材料的[单轴拉伸](@entry_id:188287)** [@problem_id:2893434]
考虑一个不可压缩[新胡克模型](@entry_id:165881)，其[应变能函数](@entry_id:178435)为 $W = \frac{\mu}{2}(I_1-3)$，其中 $\mu$ 是剪切模量。对于沿 $X_1$ 方向的[单轴拉伸](@entry_id:188287)，变形梯度为 $\mathbf{F} = \mathrm{diag}(\lambda, \lambda^{-1/2}, \lambda^{-1/2})$ 以满足 $J=1$。通过在侧面施加名义牵[引力](@entry_id:175476)为零的边界条件 ($P_{22}=P_{33}=0$)，我们可以求解出静水压力 $p=\mu\lambda^{-1}$。进而，可以得到产生该变形所需的轴向名义应力 $T_0$：
$$
T_0 = P_{11} = \mu\lambda - p\lambda^{-1} = \mu(\lambda - \lambda^{-2})
$$
这个经典结果将材料参数 $\mu$ 与宏观的力-伸长响应直接联系起来。

**示例：不可压缩新胡克材料的纯剪切** [@problem_id:2893488]
对于纯[剪切变形](@entry_id:170920)，变形梯度为 $\mathbf{F} = \begin{pmatrix} 1 & \gamma & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix}$，其中 $\gamma$ 是剪切应变量。这种变形是等体积的（$J=1$）。利用公式 $\boldsymbol{\tau} = 2\mathbf{F}(\partial W / \partial \mathbf{C})\mathbf{F}^{\mathsf{T}}$，可以计算出新胡克材料的基尔霍夫[剪切应力](@entry_id:137139)分量：
$$
\tau_{12} = \mu\gamma
$$
这个线性关系表明，对于纯剪切，[新胡克模型](@entry_id:165881)表现出与[小变形理论](@entry_id:174991)相似的胡克定律行为。

#### 可压缩材料与等体积-[体积分](@entry_id:171119)解

对于可压缩材料，一种常见的建模策略是将变形和[应变能函数](@entry_id:178435)进行**等体积-[体积分](@entry_id:171119)解 (isochoric-volumetric decomposition)**。其思想是，材料的响应可以分为改变形状（等体积或偏）的[部分和](@entry_id:162077)改变体积的部分。

为此，我们将变形梯度 $\mathbf{F}$ 分解为一个体积改变[部分和](@entry_id:162077)一个保体积部分 $\overline{\mathbf{F}}$：
$$
\mathbf{F} = J^{1/3}\mathbf{I} \cdot \overline{\mathbf{F}}, \quad \text{其中} \quad \det(\overline{\mathbf{F}}) = 1
$$
相应地，[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 也可被分解：
$$
\overline{\mathbf{C}} = J^{-2/3}\mathbf{C}, \quad \text{其中} \quad \det(\overline{\mathbf{C}}) = 1
$$
$\overline{\mathbf{C}}$ 捕捉了纯粹的形状变化。然后，[应变能函数](@entry_id:178435)可以假设为体积部分和等体积部分之和：
$$
W = W_{\text{vol}}(J) + W_{\text{iso}}(\overline{I}_1, \overline{I}_2)
$$
其中 $\overline{I}_1$ 和 $\overline{I}_2$ 是 $\overline{\mathbf{C}}$ 的[主不变量](@entry_id:193522)。它们与 $\mathbf{C}$ 的[不变量](@entry_id:148850) $I_1, I_2$ 之间存在简单的关系 [@problem_id:2893467]：
$$
\overline{I}_1 = \mathrm{tr}(\overline{\mathbf{C}}) = J^{-2/3}I_1
$$
$$
\overline{I}_2 = \frac{1}{2}[(\mathrm{tr}(\overline{\mathbf{C}}))^2 - \mathrm{tr}(\overline{\mathbf{C}}^2)] = J^{-4/3}I_2
$$
这种分解方法在为[近不可压缩材料](@entry_id:752388)（如生物组织）建模时特别有效，因为它能清晰地分离体积响应（通常非常刚硬）和剪切响应。

### 物理与数学[适定性](@entry_id:148590)的基础

并非任何形式的[应变能函数](@entry_id:178435) $W(\mathbf{F})$ 都是物理上合理或数学上适定的。一个物理上稳定的材料在受力变形时其能量应该增加。从数学角度看，为了保证基于[能量最小化](@entry_id:147698)原理的[边值问题](@entry_id:193901)存在唯一且稳定的解， $W$ 需要满足一定的**凸性 (convexity)** 条件。

在[非线性弹性](@entry_id:185743)理论中，普通的凸性条件过于严苛，无法描述真实材料的剪切和压缩行为。因此，数学家们引入了更弱的[凸性](@entry_id:138568)概念 [@problem_id:2893454]：
- **[秩一凸性](@entry_id:191019) (Rank-one convexity)**: 要求 $W$ 在任何秩一方向上的函数都是凸的。这是材料免于出现微观失稳（如剪切带）的必要条件。
- **拟[凸性](@entry_id:138568) (Quasiconvexity)**: 一个非局域的平均化条件，它是保证[能量泛函](@entry_id:170311)[弱下半连续性](@entry_id:198224)的充要条件，从而确保通过[变分法](@entry_id:163656)直接法求得的极小值解存在。
- **[多凸性](@entry_id:185154) (Polyconvexity)**: 一个比拟凸性更强但更易于验证的条件。它要求 $W$ 可以表示为变形梯度 $\mathbf{F}$ 及其所有子[行列式](@entry_id:142978)（在三维中即 $\mathbf{F}$, $\mathrm{cof}(\mathbf{F})$, $\det(\mathbf{F})$）的一个[凸函数](@entry_id:143075)。

这些[凸性](@entry_id:138568)概念之间存在严格的蕴含关系：
$$
\text{凸性} \implies \text{多凸性} \implies \text{拟凸性} \implies \text{秩一凸性}
$$
反向的蕴含关系通常不成立。在现代超[弹性理论](@entry_id:184142)中，[多凸性](@entry_id:185154)扮演着核心角色。由 J.M. Ball 发展的理论表明，如果一个[应变能函数](@entry_id:178435)是多凸的，满足一定的增长和强制性条件，并且在体积趋于零时能量趋于无穷大（形成一个“屏障”），那么相应的[弹性静力学边值问题](@entry_id:199165)就保证存在能量极小值解 [@problem_id:2893454]。这一理论不仅为[数值模拟](@entry_id:137087)的稳定性提供了坚实的基础，也指导了如何构建物理上和数学上都“表现良好”的本构模型。