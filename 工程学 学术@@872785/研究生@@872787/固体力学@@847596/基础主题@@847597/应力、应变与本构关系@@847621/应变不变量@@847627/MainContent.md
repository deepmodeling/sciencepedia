## 引言
在[固体力学](@entry_id:164042)和工程领域，准确描述材料在受力后的变形行为是至关重要的。然而，物理定律必须独立于我们观察和测量它们时所选用的[坐标系](@entry_id:156346)——这一基本原则被称为“[客观性原理](@entry_id:185412)”。这就带来了一个核心挑战：我们如何用数学语言来捕捉变形的内在物理本质，而不是[坐标系](@entry_id:156346)选择所带来的人为假象？应变[不变量](@entry_id:148850)正是解决这一问题的关键。它们是从应变张量中提取出的、在[坐标系](@entry_id:156346)变换下保持不变的标量值，为建立普适的材料[本构模型](@entry_id:174726)提供了坚实的理论基础。

本文将系统地引导你深入理解应变[不变量](@entry_id:148850)。在“原理与机制”一章中，我们将从[张量代数](@entry_id:161671)出发，揭示[不变量](@entry_id:148850)的数学定义及其与[特征值](@entry_id:154894)的深刻联系，并探讨其在[有限应变运动学](@entry_id:168563)中的具体形式。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示[不变量](@entry_id:148850)如何成为构建超弹性、塑性和失效理论的基石，并探索其在[流体力学](@entry_id:136788)、[材料科学](@entry_id:152226)等领域的广泛应用。最后，通过“动手实践”部分提供的练习，你将有机会亲手计算和推导[不变量](@entry_id:148850)，将理论知识转化为解决实际问题的能力。

## 原理与机制

在连续介质力学中，描述材料行为的物理定律必须独立于观察者所选择的[坐标系](@entry_id:156346)。这一基本要求，即**客观性**（objectivity）或**物质标架无关性**（material frame-indifference），意味着我们的数学表述必须捕捉到变形或应力的内在几何或物理属性，而非[坐标系](@entry_id:156346)的[人为选择](@entry_id:168356)。[张量不变量](@entry_id:203254)正是实现这一目标的核心数学工具。它们是从张量中提取出的标量值，在[坐标系](@entry_id:156346)变换（例如旋转）下保持不变，从而为构建客观的[本构模型](@entry_id:174726)提供了坚实的基础。

### [张量不变量](@entry_id:203254)的概念

一个[二阶张量](@entry_id:199780)可以用一个 $3 \times 3$ 矩阵来表示，其分量会随着[坐标系](@entry_id:156346)的旋转而改变。然而，某些由张量分量构成的特定组合却具有不变性。这些标量被称为**[张量不变量](@entry_id:203254)**。对于三维空间中的任意一个二阶张量 $\mathbf{A}$，其三个最基本的[不变量](@entry_id:148850)，即**[主不变量](@entry_id:193522)**（principal invariants），定义如下：

$I_1(\mathbf{A}) = \operatorname{tr}(\mathbf{A})$

$I_2(\mathbf{A}) = \frac{1}{2} [(\operatorname{tr}(\mathbf{A}))^2 - \operatorname{tr}(\mathbf{A}^2)]$

$I_3(\mathbf{A}) = \det(\mathbf{A})$

其中 $\operatorname{tr}(\mathbf{A})$ 是张量的**迹**（trace），即矩阵主对角[线元](@entry_id:196833)素之和；$\det(\mathbf{A})$ 是张量的**[行列式](@entry_id:142978)**（determinant）。

这些量之所以被称为[不变量](@entry_id:148850)，是因为在任意[正交坐标](@entry_id:166074)变换下，它们的值保持不变。若新旧[坐标系](@entry_id:156346)通过一个正交张量 $\mathbf{Q}$（满足 $\mathbf{Q}^{\mathsf{T}}\mathbf{Q} = \mathbf{I}$ 且 $\det(\mathbf{Q})=1$）相关联，则张量 $\mathbf{A}$ 的分量矩阵会通过一个正交相似变换 $\mathbf{A} \mapsto \mathbf{A}' = \mathbf{Q}^{\mathsf{T}}\mathbf{A}\mathbf{Q}$ 进行转换。我们可以证明 $I_1, I_2, I_3$ 在此变换下是不变的 [@problem_id:2689516]。

- 对于 $I_1$，利用[迹的循环性质](@entry_id:153103) $\operatorname{tr}(\mathbf{XYZ}) = \operatorname{tr}(\mathbf{ZXY})$：
$I_1(\mathbf{A}') = \operatorname{tr}(\mathbf{Q}^{\mathsf{T}}\mathbf{A}\mathbf{Q}) = \operatorname{tr}(\mathbf{Q}\mathbf{Q}^{\mathsf{T}}\mathbf{A}) = \operatorname{tr}(\mathbf{IA}) = \operatorname{tr}(\mathbf{A}) = I_1(\mathbf{A})$

- 对于 $I_2$，我们需要证明 $\operatorname{tr}(\mathbf{A}^2)$ 也是[不变量](@entry_id:148850)。
$\operatorname{tr}((\mathbf{A}')^2) = \operatorname{tr}(\mathbf{Q}^{\mathsf{T}}\mathbf{A}\mathbf{Q}\mathbf{Q}^{\mathsf{T}}\mathbf{A}\mathbf{Q}) = \operatorname{tr}(\mathbf{Q}^{\mathsf{T}}\mathbf{A}^2\mathbf{Q}) = \operatorname{tr}(\mathbf{Q}\mathbf{Q}^{\mathsf{T}}\mathbf{A}^2) = \operatorname{tr}(\mathbf{A}^2)$
由于 $\operatorname{tr}(\mathbf{A})$ 和 $\operatorname{tr}(\mathbf{A}^2)$ 都不变，它们的任意代数组合（如 $I_2$）也必然是不变的。这个结论对任何[二阶张量](@entry_id:199780)都成立，无论其是否对称 [@problem_id:2689516]。

- 对于 $I_3$，利用[行列式的乘法性质](@entry_id:148055) $\det(\mathbf{XY}) = \det(\mathbf{X})\det(\mathbf{Y})$：
$I_3(\mathbf{A}') = \det(\mathbf{Q}^{\mathsf{T}}\mathbf{A}\mathbf{Q}) = \det(\mathbf{Q}^{\mathsf{T}})\det(\mathbf{A})\det(\mathbf{Q}) = (1)\det(\mathbf{A})(1) = \det(\mathbf{A}) = I_3(\mathbf{A})$

[不变量](@entry_id:148850)的根本来源在于它们与张量**[特征值](@entry_id:154894)**（eigenvalues）的深刻联系。一个张量的[特征值](@entry_id:154894)是其内在属性，不随[坐标系](@entry_id:156346)改变。张量的特征多项式 $p(\lambda) = \det(\mathbf{A} - \lambda\mathbf{I})$ 的系数也因此是客观的。对于三维[二阶张量](@entry_id:199780)，该多项式展开为：
$p(\lambda) = -\lambda^3 + I_1(\mathbf{A})\lambda^2 - I_2(\mathbf{A})\lambda + I_3(\mathbf{A})$
这表明，[主不变量](@entry_id:193522)正是[特征多项式](@entry_id:150909)的系数（符号有别）。若张量的[特征值](@entry_id:154894)为 $\lambda_1, \lambda_2, \lambda_3$，那么[不变量](@entry_id:148850)就是[特征值](@entry_id:154894)的**初等[对称多项式](@entry_id:153581)** [@problem_id:2689516]：
$I_1 = \lambda_1 + \lambda_2 + \lambda_3$
$I_2 = \lambda_1\lambda_2 + \lambda_2\lambda_3 + \lambda_3\lambda_1$
$I_3 = \lambda_1\lambda_2\lambda_3$
由于相似变换（$S^{-1}AS$）保持[特征值](@entry_id:154894)不变，因此[主不变量](@entry_id:193522)在更广泛的相似变换下也是不变的，而不仅限于正交变换 [@problem_id:2689516]。

### [有限应变运动学](@entry_id:168563)中的[不变量](@entry_id:148850)

在描述材料的[大变形](@entry_id:167243)时，我们使用**变形梯度**（deformation gradient） $\mathbf{F}$。为了构建一个客观的[应变度量](@entry_id:755495)，我们通常采用**右柯西-格林变形张量**（Right Cauchy-Green deformation tensor）$\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$。$\mathbf{C}$ 是[对称正定](@entry_id:145886)张量，并且是客观的，即在[刚体转动](@entry_id:191086)下不变。因此，它的[不变量](@entry_id:148850) $I_1(\mathbf{C}), I_2(\mathbf{C}), I_3(\mathbf{C})$ 成为描述有限应变状态的理想候选者。

为了具体理解这些[不变量](@entry_id:148850)的计算，考虑一个同时包含拉伸和剪切的均匀变形，其变形梯度为 [@problem_id:2689494]：
$$
\mathbf{F} =
\begin{bmatrix}
\alpha   s   0 \\
0   \beta   0 \\
0   0   \gamma
\end{bmatrix}
$$
首先计算 $\mathbf{C}$ 张量：
$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F} =
\begin{bmatrix}
\alpha  0  0 \\
s  \beta  0 \\
0  0  \gamma
\end{bmatrix}
\begin{bmatrix}
\alpha  s  0 \\
0  \beta  0 \\
0  0  \gamma
\end{bmatrix}
=
\begin{bmatrix}
\alpha^2  \alpha s  0 \\
\alpha s  \beta^2+s^2  0 \\
0  0  \gamma^2
\end{bmatrix}
$$
通过计算其特征多项式 $\det(\mathbf{C} - \lambda\mathbf{I}) = 0$，我们可以直接确定其[不变量](@entry_id:148850)：
$I_1 = \operatorname{tr}(\mathbf{C}) = \alpha^2 + (\beta^2+s^2) + \gamma^2 = \alpha^2 + \beta^2 + \gamma^2 + s^2$
$I_3 = \det(\mathbf{C}) = (\alpha\beta\gamma)^2$
而 $I_2$ 可以通过展开特征多项式或者使用定义式得到：
$I_2 = \alpha^2\beta^2 + \alpha^2\gamma^2 + \beta^2\gamma^2 + \gamma^2s^2$
这个例子清晰地展示了[不变量](@entry_id:148850)如何将复杂的变形分量（拉伸 $\alpha, \beta, \gamma$ 和剪切 $s$）综合成三个客观的标量度量。

[不变量](@entry_id:148850)的物理意义通过**[主伸长](@entry_id:194664)**（principal stretches）$\lambda_1, \lambda_2, \lambda_3$ 得到最深刻的揭示。[主伸长](@entry_id:194664)是 $\mathbf{F}$ 的奇异值，也是[右伸长张量](@entry_id:193756) $\mathbf{U}$ 的[特征值](@entry_id:154894)（其中 $\mathbf{F} = \mathbf{RU}$ 是 $\mathbf{F}$ 的极分解）。由于 $\mathbf{C} = \mathbf{U}^2$，$\mathbf{C}$ 的[特征值](@entry_id:154894)正是[主伸长](@entry_id:194664)的平方，即 $\lambda_1^2, \lambda_2^2, \lambda_3^2$。因此，$\mathbf{C}$ 的[不变量](@entry_id:148850)可以直接用[主伸长](@entry_id:194664)表示 [@problem_id:2689492]：
$I_1 = \lambda_1^2 + \lambda_2^2 + \lambda_3^2$
$I_2 = \lambda_1^2\lambda_2^2 + \lambda_2^2\lambda_3^2 + \lambda_3^2\lambda_1^2$
$I_3 = (\lambda_1\lambda_2\lambda_3)^2 = (\det\mathbf{F})^2 = J^2$
其中 $J = \det\mathbf{F}$ 是体积变化的[雅可比行列式](@entry_id:137120)。这些关系将抽象的代数[不变量](@entry_id:148850)与清晰的几何图像（沿三个主方向的拉伸）联系起来。

在某些情况下，使用**[格林-拉格朗日应变张量](@entry_id:187745)**（Green-Lagrange strain tensor）$\mathbf{E} = \frac{1}{2}(\mathbf{C}-\mathbf{I})$ 及其[不变量](@entry_id:148850) $(K_1, K_2, K_3)$ 可能更为方便。因为 $\mathbf{E}$ 和 $\mathbf{C}$ 之间存在简单的仿射关系，它们的[不变量](@entry_id:148850)集是代数等价的，均可作为构建本构模型的[完备基](@entry_id:143908)础。然而，$\mathbf{E}$ 的[不变量](@entry_id:148850)在未变形的参考构型（$\mathbf{F}=\mathbf{I}$）中为零，这使得它们在围绕参考构型进行级数展开时（例如，在小应变或中[等应变](@entry_id:184570)理论中）特别有用，可以直接与线性弹性理论建立联系 [@problem_id:2689525]。

### 物理容许性与[不变量](@entry_id:148850)空间

一个自然的问题是：任意给定一组[不变量](@entry_id:148850)值 $(I_1, I_2, I_3)$ 是否都对应一个物理上可能的变形？答案是否定的。由于[右柯西-格林张量](@entry_id:174156) $\mathbf{C}$ 必须是**对称正定**的，它的[特征值](@entry_id:154894) $(\lambda_1^2, \lambda_2^2, \lambda_3^2)$ 必须是三个正实数。

这意味着，由[不变量](@entry_id:148850) $(I_1, I_2, I_3)$ 作为系数构成的[特征方程](@entry_id:265849) $x^3 - I_1 x^2 + I_2 x - I_3 = 0$ 必须有三个正实根。要满足此条件，必须同时满足以下两点 [@problem_id:2689547] [@problem_id:2689542]：

1.  **根必须为实数**：对于三次多项式，所有根均为实数的充要条件是其[判别式](@entry_id:174614) $\Delta \ge 0$。对于上述特征多项式，[判别式](@entry_id:174614)为 $\Delta = I_1^2 I_2^2 - 4I_2^3 - 4I_1^3 I_3 - 27I_3^2 + 18I_1 I_2 I_3$。

2.  **实根必须为正**：如果根已确定为实数，那么根据**[笛卡尔符号法则](@entry_id:167245)**（Descartes' Rule of Signs），当 $I_10, I_20, I_30$ 时，系数符号序列为 $(+, -, +, -)$，存在三次变号，表明正实根的数量为3或1。同时，考察 $p(-x)$ 的系数符号，均为负，没有变号，表明没有负实根。由于 $p(0) = -I_3 \ne 0$，零也不是根。因此，在根为实数的前提下，三个[不变量](@entry_id:148850)均为正值是所有根都为正的充分必要条件。

综上所述，一组[不变量](@entry_id:148850) $(I_1, I_2, I_3)$ 对应于一个物理上可行的（即对称正定的）$\mathbf{C}$ 张量的**充分必要条件**是：$I_10, I_20, I_30$ 并且[判别式](@entry_id:174614) $\Delta \ge 0$。这些条件定义了“物理上容许的”[不变量](@entry_id:148850)空间，这对于发展和验证本构模型至关重要 [@problem_id:2689542]。

### [不变量](@entry_id:148850)在[本构模型](@entry_id:174726)中的应用

应变[不变量](@entry_id:148850)最重要的应用在于构建**[各向同性材料](@entry_id:170678)**（isotropic materials）的[本构关系](@entry_id:186508)。根据**[各向同性函数](@entry_id:750877)的[表示定理](@entry_id:637872)**（representation theorem for isotropic functions），任何客观且各向同性的标量函数（如[应变能密度函数](@entry_id:755490) $W$）如果依赖于一个对称[二阶张量](@entry_id:199780)（如 $\mathbf{C}$），那么它必定只能是该张量[主不变量](@entry_id:193522)的函数，即 $W = \hat{W}(I_1, I_2, I_3)$。

#### 体积-等容分解

在许多材料模型中，特别是针对橡胶类近不可压材料或[金属塑性](@entry_id:176585)，将变形响应分解为**体积响应**（volumetric response）和**等容响应**（isochoric response，即形状改变）是至关重要的。这在[有限应变理论](@entry_id:176941)中通过分解变形梯度来实现。

首先定义雅可比行列式 $J = \det \mathbf{F}$，它度量了局部体积的变化。然后，可以定义一个纯体积变形部分和一个纯形状改变部分。一种标准做法是引入一个修正的或“等容的”变形梯度 $\bar{\mathbf{F}} = J^{-1/3}\mathbf{F}$。这个新张量的[行列式](@entry_id:142978)为 $\det(\bar{\mathbf{F}}) = \det(J^{-1/3}\mathbf{F}) = (J^{-1/3})^3 \det(\mathbf{F}) = J^{-1}J=1$，表明它描述了一个保持体积不变的变形。

相应地，我们可以定义一个**修正的[右柯西-格林张量](@entry_id:174156)** [@problem_id:2689520]：
$$
\bar{\mathbf{C}} = \bar{\mathbf{F}}^{\mathsf{T}}\bar{\mathbf{F}} = (J^{-1/3}\mathbf{F})^{\mathsf{T}}(J^{-1/3}\mathbf{F}) = J^{-2/3}\mathbf{C}
$$
这个张量 $\bar{\mathbf{C}}$ 的一个关键特性是其[行列式](@entry_id:142978)恒为1：
$$
\det(\bar{\mathbf{C}}) = \det(J^{-2/3}\mathbf{C}) = (J^{-2/3})^3 \det(\mathbf{C}) = J^{-2} I_3 = J^{-2} J^2 = 1
$$
这意味着 $\bar{\mathbf{C}}$ 的第三[不变量](@entry_id:148850) $\bar{I}_3$ 总是1，不再包含体积变化的信息。此外，对于一个纯体积变形 $\mathbf{F} = \lambda\mathbf{I}$，我们有 $J = \lambda^3$ 且 $\mathbf{C} = \lambda^2\mathbf{I}$。此时，$\bar{\mathbf{C}} = (\lambda^3)^{-2/3}(\lambda^2\mathbf{I}) = \lambda^{-2}\lambda^2\mathbf{I} = \mathbf{I}$。这表明 $\bar{\mathbf{C}}$ 对纯体积变形不敏感，它只捕捉变形中的扭曲或剪切分量。因此，$\bar{\mathbf{C}}$ 的前两个[不变量](@entry_id:148850) $\bar{I}_1 = \operatorname{tr}(\bar{\mathbf{C}})$ 和 $\bar{I}_2$ 成为了纯粹的**畸变度量**（distortional measures）。

基于这种分解，各向同性[超弹性材料](@entry_id:190241)的[应变能密度函数](@entry_id:755490)可以写成可加形式：
$$
W(\mathbf{F}) = W_{\text{iso}}(\bar{I}_1, \bar{I}_2) + W_{\text{vol}}(J)
$$
其中 $W_{\text{iso}}$ 描述材料抵抗形状改变的能量，而 $W_{\text{vol}}$ 描述抵[抗体](@entry_id:146805)积改变的能量。

#### 应力响应的分解

这种[能量分解](@entry_id:193582)直接导致了应力响应的相应分解。对于上述形式的[应变能函数](@entry_id:178435)，可以从第一性原理推导出柯西应力 $\boldsymbol{\sigma}$ 的结构 [@problem_id:2689535]。推导过程虽然复杂，但其最终结果非常优雅且富有洞察力：

- 材料的**静水压力**（hydrostatic pressure） $p = \frac{1}{3}\operatorname{tr}(\boldsymbol{\sigma})$（应力张量的球量部分）完全由能量的体积部分决定：
  $$
  p = \frac{dW_{\text{vol}}}{dJ}
  $$

- 材料的**[偏应力张量](@entry_id:267642)**（deviatoric stress tensor） $\boldsymbol{\sigma}' = \boldsymbol{\sigma} - p\mathbf{I}$（[应力张量](@entry_id:148973)的偏量部分，描述[剪切应力](@entry_id:137139)）完全由能量的等容部分决定，其表达式仅包含对 $\bar{I}_1$ 和 $\bar{I}_2$ 的[偏导数](@entry_id:146280) $\frac{\partial W_{\text{iso}}}{\partial \bar{I}_1}$ 和 $\frac{\partial W_{\text{iso}}}{\partial \bar{I}_2}$。

这一结果意义重大：它为独立地建模和表征材料的体积行为和剪切行为提供了理论依据。例如，对于一个纯体积变形 $\mathbf{F} = J^{1/3}\mathbf{I}$，其[偏应力](@entry_id:163323)部分为零，总应力为纯静水压力 $\boldsymbol{\sigma} = p\mathbf{I}$。若体积能为 $W_{\text{vol}}(J) = U(J) = \frac{\kappa}{2}(J-1)^2$（其中 $\kappa$ 是[体积模量](@entry_id:160069)），则静水压力为 $p = \frac{dU}{dJ} = \kappa(J-1)$ [@problem_id:2689535]。

#### 小应变理论的联系

[体积-偏量分解](@entry_id:183756)的思想在小应变理论中也有直接的对应。对于**[无穷小应变张量](@entry_id:167211)** $\boldsymbol{\varepsilon}$，其分解为球量部分（[体积应变](@entry_id:267252)）和偏量部分（畸变应变）[@problem_id:2689529]：
$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}' + \frac{1}{3}(\operatorname{tr}\boldsymbol{\varepsilon})\mathbf{I}
$$
其中 $\boldsymbol{\varepsilon}' = \boldsymbol{\varepsilon} - \frac{1}{3}(\operatorname{tr}\boldsymbol{\varepsilon})\mathbf{I}$ 是**偏应变张量**，其迹为零。偏应变张量的[不变量](@entry_id:148850)，通常记为 $J_2^\varepsilon = \frac{1}{2}\boldsymbol{\varepsilon}':\boldsymbol{\varepsilon}'$ 和 $J_3^\varepsilon = \det(\boldsymbol{\varepsilon}')$，在[弹塑性力学](@entry_id:193198)中扮演着核心角色，例如，著名的 von Mises 屈服准则就是基于 $J_2^\varepsilon$。

#### [凯莱-哈密顿定理](@entry_id:150551)的应用

最后，[不变量](@entry_id:148850)在[张量代数](@entry_id:161671)运算中也提供了强大的工具。**[凯莱-哈密顿定理](@entry_id:150551)**（Cayley-Hamilton theorem）指出，任何一个二阶张量都满足其自身的特征方程。对于 $\mathbf{C}$ 张量，这意味着：
$$
\mathbf{C}^3 - I_1\mathbf{C}^2 + I_2\mathbf{C} - I_3\mathbf{I} = \mathbf{0}
$$
这个定理的一个直接而有用的应用是求解张量的逆。由于 $I_3 = \det(\mathbf{C}) = J^2  0$，$\mathbf{C}$ 是可逆的。我们可以将上式两边同乘以 $\mathbf{C}^{-1}$ 并整理，得到 $\mathbf{C}^{-1}$ 的一个显式表达式 [@problem_id:2689513]：
$$
\mathbf{C}^{-1} = \frac{1}{I_3}(\mathbf{C}^2 - I_1\mathbf{C} + I_2\mathbf{I})
$$
这个关系在解析推导和数值计算中都非常有用，它避免了直接求逆的复杂计算，而是将逆运算转化为张量的幂和[不变量](@entry_id:148850)的代数组合。

总而言之，应变[不变量](@entry_id:148850)不仅是满足[客观性原理](@entry_id:185412)的数学必然，更是连接抽象数学、物理直觉和工程应用的桥梁。从定义基本应变状态，到施加物理约束，再到构建和解释复杂的材料[本构模型](@entry_id:174726)，[不变量](@entry_id:148850)贯穿于现代固体力学的核心理论之中。