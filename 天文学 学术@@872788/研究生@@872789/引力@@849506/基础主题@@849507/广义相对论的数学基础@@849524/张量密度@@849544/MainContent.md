## 引言
在广义相对论和现代[场论](@entry_id:155241)中，物理定律必须以一种不依赖于观察者[坐标系](@entry_id:156346)选择的形式来表达，这就是[协变性原理](@entry_id:275808)。虽然张量为实现这一目标提供了强大的语言，但标准的张量理论在处理积分（如物理系统的作用量）时遇到了一个根本性难题：体积元本身在坐标变换下并不是一个[不变量](@entry_id:148850)。为了解决这个知识缺口，并建立一个能够处理积分[不变量](@entry_id:148850)的完整框架，我们必须引入张量概念的一个关键推广——[张量密度](@entry_id:191194)。

本文旨在系统地介绍[张量密度](@entry_id:191194)。在第一章“原理与机制”中，我们将从积分[不变性](@entry_id:140168)的需求出发，严格定义[张量密度](@entry_id:191194)及其权重，并阐述其代数性质和变换法则，同时辨析克氏符号等[非张量对象](@entry_id:201374)。接下来，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示[张量密度](@entry_id:191194)如何在广义相对论、[场论](@entry_id:155241)乃至凝聚态物理中作为核心工具，用于构造[守恒量](@entry_id:150267)、简化物理定律以及定义[引力能](@entry_id:193726)。最后，通过“动手实践”部分提供的精选问题，您将有机会亲手应用所学知识，巩固对[张量密度](@entry_id:191194)变换和物理应用的理解。

## 原理与机制

在物理学和数学中，张量的概念是描述物理定律和几何结构的核心，因为它提供了一种在坐标变换下保持形式不变的语言。标准的[张量变换法则](@entry_id:185176)是齐次的、线性的。然而，为了构建在弯曲空间或任意[坐标系](@entry_id:156346)中都有意义的物理理论，特别是那些涉及积分的理论（如[作用量原理](@entry_id:154742)），我们必须扩展张量的概念。本章将引入**[张量密度](@entry_id:191194) (tensor densities)** 的概念，阐明其定义、代数性质以及在物理学中的根本作用。

### 积分、体积元与[标量密度](@entry_id:161438)的必要性

我们从一个基本问题开始：如何在[流形](@entry_id:153038)上定义一个积分，使其值不依赖于我们选择的[坐标系](@entry_id:156346)？考虑一个 $n$ 维空间中的区域 $\mathcal{R}$，以及一个标量场 $\phi(x)$。我们可能想当然地认为积分 $I = \int_{\mathcal{R}} \phi(x) d^n x$ 是一个[不变量](@entry_id:148850)。然而，在[坐标变换](@entry_id:172727) $x \to x'$ 下，微观[体积元](@entry_id:267802) $d^n x$ 并非标量。根据多元微[积分中的变量替换](@entry_id:140343)法则，体积元会按照以下方式变换：

$$
d^n x' = \left| \det\left(\frac{\partial x'}{\partial x}\right) \right| d^n x
$$

其中 $\frac{\partial x'}{\partial x}$ 是[坐标变换](@entry_id:172727)的[雅可比矩阵](@entry_id:264467)，其分量为 $J^i_j = \frac{\partial x'^i}{\partial x^j}$。我们将其[行列式](@entry_id:142978)记为 $J = \det(J^i_j)$。为简洁起见，我们通常考虑保向的变换，其中 $J > 0$，因此[绝对值](@entry_id:147688)可以去掉。在这种情况下，[体积元](@entry_id:267802)变换为 $d^n x' = J d^n x$。

由于体积元本身不是[不变量](@entry_id:148850)，为了使积分 $I$ 成为一个与坐标无关的**[标量不变量](@entry_id:193787) (scalar invariant)**，被积函数必须以一种特殊的方式进行变换，以精确抵消[雅可比行列式](@entry_id:137120)因子 $J$。让我们假设在新的[坐标系](@entry_id:156346)中，积分写作 $I' = \int_{\mathcal{R}'} \phi'(x') d^n x'$。为了保持 $I = I'$，我们必须有：

$$
\int_{\mathcal{R}} \phi(x) d^n x = \int_{\mathcal{R}'} \phi'(x') d^n x' = \int_{\mathcal{R}} \phi'(x'(x)) J d^n x
$$

由于这个等式必须对任何积分区域 $\mathcal{R}$ 都成立，因此被积函数必须满足如下关系：

$$
\phi(x) = \phi'(x'(x)) J \quad \implies \quad \phi'(x') = J^{-1} \phi(x)
$$

这个推论激发了一个新的定义。我们称一个量 $\mathcal{S}$ 为权重为 $W$ 的**[标量密度](@entry_id:161438) (scalar density)**，如果它在坐标变换下的变换法则是：

$$
\mathcal{S}'(x') = J^W \mathcal{S}(x)
$$

其中 $W$ 是一个称为**权重 (weight)** 的实数。根据这个定义，一个要能被积分并产生[标量不变量](@entry_id:193787)的量，例如经典物理中的**[概率密度](@entry_id:175496)** $\rho(x)$ [@problem_id:1542728] 或**电荷密度** $\rho$ [@problem_id:1542761]，必须是一个权重为 $W=-1$ 的[标量密度](@entry_id:161438)。

这个原理在现代物理学中至关重要。例如，在[场论](@entry_id:155241)中，物理系统的动力学由作用量 $S = \int \mathcal{L} d^n x$ 决定，其中 $\mathcal{L}$ 是**拉格朗日密度 (Lagrangian density)**。根据最小作用量原理，作用量 $S$ 必须是一个[洛伦兹标量](@entry_id:275319)，并且在[广义坐标](@entry_id:156576)变换下也是一个[不变量](@entry_id:148850)。这就要求拉格朗日密度 $\mathcal{L}$ 本身必须是一个权重为 $W=-1$ 的[标量密度](@entry_id:161438)，以抵消[体积元](@entry_id:267802) $d^n x$ 的变换效应。如果一个理论中的某个场 $\Psi$ 本身是一个权重为 $W_\Psi$ 的[标量密度](@entry_id:161438)，而拉格朗日密度是该场的函数，例如 $\mathcal{L} = [\Psi(x)]^3$，那么为了使作用量不变，我们必须有 $\mathcal{L}$ 的权重为 -1。由于 $\mathcal{L}' = (\Psi')^3 = (J^{W_\Psi} \Psi)^3 = J^{3W_\Psi} \mathcal{L}$，我们要求 $3W_\Psi = -1$，这意味着场 $\Psi$ 的权重必须是 $W_\Psi = -1/3$ [@problem_id:1542765]。

### [张量密度](@entry_id:191194)的定义与代数

这个概念可以自然地推广到带有指标的张量。一个类型为 $(p, q)$、权重为 $W$ 的**[张量密度](@entry_id:191194)** $\mathfrak{T}$ 的分量在[坐标变换](@entry_id:172727) $x \to x'$ 下的变换法则是：

$$
\mathfrak{T}'^{i'_1 \dots i'_p}_{j'_1 \dots j'_q} = (J)^W \left(\frac{\partial x'^{i'_1}}{\partial x^{i_1}} \dots \frac{\partial x'^{i'_p}}{\partial x^{i_p}}\right) \left(\frac{\partial x^{j_1}}{\partial x'^{j'_1}} \dots \frac{\partial x^{j_q}}{\partial x'^{j'_q}}\right) \mathfrak{T}^{i_1 \dots i_p}_{j_1 \dots j_q}
$$

这里我们再次使用了爱因斯坦求和约定。从定义中可以清楚地看到，一个普通的张量（有时称为**真张量 (true tensor)** 或**绝对张量 (absolute tensor)**）只不过是一个权重为 $W=0$ 的[张量密度](@entry_id:191194)。

[张量密度](@entry_id:191194)的代数运算遵循一些简单的规则，这些规则直接源于它们的定义：

1.  **加法**：只有类型和权重完全相同的[张量密度](@entry_id:191194)才能相加，其结果是具有相同类型和权重的[张量密度](@entry_id:191194)。

2.  **乘积与缩并**：当两个[张量密度](@entry_id:191194)（权重分别为 $W_1$ 和 $W_2$）相乘或进行缩并时，得到的新的[张量密度](@entry_id:191194)的权重是它们权重之和，$W_{new} = W_1 + W_2$。例如，考虑一个二阶[逆变张量](@entry_id:636697)密度 $M^{ij}$（权重 $W_1$）和一个二阶[协变张量](@entry_id:634493)密度 $N_{jk}$（权重 $W_2$）。它们的缩并 $P^i_k = M^{ij}N_{jk}$ 的变换法则是（为清晰起见，使用带撇的指标表示新[坐标系](@entry_id:156346)分量）：
    $$
    P'^{i'}_{k'} = M'^{i'j'}N'_{j'k'} = (J^{W_1} \frac{\partial x'^{i'}}{\partial x^a}\frac{\partial x'^{j'}}{\partial x^b} M^{ab}) (J^{W_2} \frac{\partial x^c}{\partial x'^{j'}}\frac{\partial x^d}{\partial x'^{k'}} N_{cd})
    $$
    重新组合各项并利用链式法则 $\frac{\partial x'^{j'}}{\partial x^b} \frac{\partial x^c}{\partial x'^{j'}} = \frac{\partial x^c}{\partial x^b} = \delta^c_b$，我们得到：
    $$
    P'^{i'}_{k'} = J^{W_1+W_2} \frac{\partial x'^{i'}}{\partial x^a} \frac{\partial x^d}{\partial x'^{k'}} M^{ab} (\delta^c_b) N_{cd} = J^{W_1+W_2} \frac{\partial x'^{i'}}{\partial x^a} \frac{\partial x^d}{\partial x'^{k'}} M^{ab} N_{bd}
    $$
    由于 $P^a_d = M^{ab}N_{bd}$，所以 $P'^{i'}_{k'} = J^{W_1+W_2} \frac{\partial x'^{i'}}{\partial x^a} \frac{\partial x^d}{\partial x'^{k'}} P^a_d$。这表明 $P^i_k$ 是一个权重为 $W_1+W_2$ 的[混合张量](@entry_id:182079)密度 [@problem_id:1542764]。

    这个性质有一个非常重要的推论：通过将一个权重为 $W$ 的[张量密度](@entry_id:191194)与一个权重为 $-W$ 的[张量密度](@entry_id:191194)进行缩并，可以构造出一个权重为 $W+(-W)=0$ 的真张量 [@problem_id:1542742]。这是一种从[张量密度](@entry_id:191194)构建[物理可观测量](@entry_id:154692)（必须是真张量）的常用方法。

3.  **[升降指标](@entry_id:161292)**：在[黎曼几何](@entry_id:160508)中，指标的上升和下降是通过度规张量 $g_{ij}$ 及其逆 $g^{ij}$ 来实现的。根据广义相对论的基本假设，[度规张量](@entry_id:160222)是一个真张量，即其权重为 $W=0$。由于[升降指标](@entry_id:161292)操作本质上是与[度规张量](@entry_id:160222)进行缩并，根据权重相加的规则，这个操作不会改变[张量密度](@entry_id:191194)的权重。例如，如果我们用 $g^{ki}g^{lj}$ 来提升一个权重为 $W$ 的[协变张量](@entry_id:634493)密度 $\mathfrak{T}_{ij}$ 的两个指标，得到 $\mathfrak{T}^{kl} = g^{ki}g^{lj}\mathfrak{T}_{ij}$，那么新对象 $\mathfrak{T}^{kl}$ 的权重仍然是 $W$ [@problem_id:1542713]。

### 重要的[张量密度](@entry_id:191194)实例

#### 度规[行列式](@entry_id:142978)

在黎曼几何中，一个极其重要的[标量密度](@entry_id:161438)是[度规张量](@entry_id:160222) $g_{ij}$ 的[行列式](@entry_id:142978)，记为 $g = \det(g_{ij})$。度规张量是一个二阶[协变](@entry_id:634097)真张量（权重为 0），其变换法则是：
$$
g'_{kl} = \frac{\partial x^i}{\partial x'^k} \frac{\partial x^j}{\partial x'^l} g_{ij}
$$
用矩阵形式表示，令 $A$ 为逆[雅可比矩阵](@entry_id:264467)，其分量为 $A^i_k = \frac{\partial x^i}{\partial x'^k}$，则 $g' = A^T g A$。对两边取[行列式](@entry_id:142978)，我们得到：
$$
\det(g') = \det(A^T) \det(g) \det(A) = (\det A)^2 \det(g)
$$
由于 $\det A = \det((\frac{\partial x'}{\partial x})^{-1}) = (\det(\frac{\partial x'}{\partial x}))^{-1} = J^{-1}$，我们有：
$$
g' = (J^{-1})^2 g = J^{-2} g
$$
这表明度规的[行列式](@entry_id:142978) $g$ 是一个权重为 $W=-2$ 的[标量密度](@entry_id:161438) [@problem_id:1542739]。

这个结果是广义相对论的基石之一。它意味着 $\sqrt{-g}$（在通常的[洛伦兹度规](@entry_id:184391)下 $g0$）是一个权重为 $W=-1$ 的[标量密度](@entry_id:161438)。因此，积分元 $d^4\mathcal{V} = \sqrt{-g} d^4 x$ 是一个不依赖于坐标的**不变体积元 (invariant volume element)**。这是因为 $\sqrt{-g}$ 的权重-1 正好抵消了坐标体积元 $d^4 x$ 变换时产生的 $J$ 因子（即 $d^4 x$ 可以被视为权重为+1的密度）。因此，任何形如 $S = \int \mathcal{L} \sqrt{-g} d^4 x$ 的作用量，只要其[拉格朗日量](@entry_id:174593) $\mathcal{L}$ 是一个真标量（权重为0），该作用量就自然地成为一个[不变量](@entry_id:148850)。

#### [列维-奇维塔张量](@entry_id:191101)密度

另一个关键例子是**[列维-奇维塔符号](@entry_id:193594) (Levi-Civita symbol)** $\epsilon_{i_1 \dots i_n}$。它被定义为：如果 $(i_1, \dots, i_n)$ 是 $(1, \dots, n)$ 的偶[排列](@entry_id:136432)，则为+1；如果是奇[排列](@entry_id:136432)，则为-1；如果有任何重复的指标，则为0。一个常见的误解是认为它是一个张量。

为了说明这一点，让我们考虑一个三维[笛卡尔坐标系](@entry_id:169789)中的真张量 $T_{ijk}$，其分量恰好等于 $\epsilon_{ijk}$。现在考虑一个[坐标变换](@entry_id:172727) $x' = -2x, y' = y, z' = z$。这个变换的[雅可比矩阵](@entry_id:264467)是对角的，而[逆变](@entry_id:192290)换的偏导数为 $\frac{\partial x}{\partial x'} = -1/2$, $\frac{\partial y}{\partial y'} = 1$, $\frac{\partial z}{\partial z'} = 1$。根据[协变张量](@entry_id:634493)的变换法则，新的分量 $T'_{123}$ 为：
$$
T'_{123} = \frac{\partial x^i}{\partial x'^1} \frac{\partial x^j}{\partial x'^2} \frac{\partial x^k}{\partial x'^3} T_{ijk} = \frac{\partial x}{\partial x'} \frac{\partial y}{\partial y'} \frac{\partial z}{\partial z'} T_{123} = (-\frac{1}{2})(1)(1)(+1) = -\frac{1}{2}
$$
显然，$T'_{123} \neq \epsilon_{123}$ [@problem_id:1542709]。这证明了其分量在某个[坐标系](@entry_id:156346)中等于 $\epsilon_{ijk}$ 的张量，在其他[坐标系](@entry_id:156346)中通常不等于。

真正的**[列维-奇维塔张量](@entry_id:191101)密度** $\varepsilon_{ijk}$（有时也称为[伪张量](@entry_id:193048)）是指其分量在*任何*[坐标系](@entry_id:156346)下都等于[列维-奇维塔符号](@entry_id:193594)的几何对象。让我们推导它的权重。[协变张量](@entry_id:634493)密度 $\varepsilon_{ijk}$ 的变换法则是：
$$
\varepsilon'_{pqr} = J^W \frac{\partial x^i}{\partial x'^p} \frac{\partial x^j}{\partial x'^q} \frac{\partial x^k}{\partial x'^r} \varepsilon_{ijk}
$$
我们要求在任何[坐标系](@entry_id:156346)中都有 $\varepsilon_{ijk} = \epsilon_{ijk}$。利用[行列式](@entry_id:142978)和[列维-奇维塔符号](@entry_id:193594)的关系，我们知道：
$$
\frac{\partial x^i}{\partial x'^p} \frac{\partial x^j}{\partial x'^q} \frac{\partial x^k}{\partial x'^r} \epsilon_{ijk} = \det\left(\frac{\partial x}{\partial x'}\right) \epsilon_{pqr} = J^{-1} \epsilon_{pqr}
$$
代入变换法则，我们要求 $\epsilon_{pqr} = J^W (J^{-1} \epsilon_{pqr})$。为了使此式对任意 $J$ 成立，必须有 $J^{W-1} = 1$，这意味着权重 $W=1$。因此，协变的[列维-奇维塔符号](@entry_id:193594)是一个权重为 $W=+1$ 的[张量密度](@entry_id:191194)。类似地，可以证明[逆变](@entry_id:192290)的[列维-奇维塔符号](@entry_id:193594) $\varepsilon^{ijk}$ 是一个权重为 $W=-1$ 的[张量密度](@entry_id:191194)。

如果一个变换的[雅可比行列式](@entry_id:137120)为负（例如，一个[反射变换](@entry_id:175518)），$J^W$ 的符号取决于 $W$。那些在变换中包含 $\text{sgn}(J)$ 因子的对象被称为**[伪张量](@entry_id:193048) (pseudotensors)**。[张量密度](@entry_id:191194)为这个概念提供了更普适的框架。

### 变换法则的应用：一个计算实例

为了具体展示[张量密度](@entry_id:191194)变换的完整过程，让我们考虑一个权重为 $W$ 的二阶[协变张量](@entry_id:634493)密度 $\mathcal{T}$ [@problem_id:528780]。假设在二维笛卡尔坐标系 $(x^1, x^2) = (x, y)$ 中，其分量为克罗内克符号 $\mathcal{T}_{ij} = \delta_{ij}$。现在引入一个新的[坐标系](@entry_id:156346) $(x'^1, x'^2) = (u, v)$，其关系为 $x = u \cosh(v)$ 和 $y = u \sinh(v)$。我们想计算在新[坐标系](@entry_id:156346)下该[张量密度](@entry_id:191194)的迹 $\text{tr}(\mathcal{T}') = \mathcal{T}'_{11} + \mathcal{T}'_{22}$。

首先，我们计算逆变换的雅可比矩阵 $A^i_j = \frac{\partial x^i}{\partial x'^j}$ 的分量：
$$
\frac{\partial x}{\partial u} = \cosh(v), \quad \frac{\partial x}{\partial v} = u \sinh(v)
$$
$$
\frac{\partial y}{\partial u} = \sinh(v), \quad \frac{\partial y}{\partial v} = u \cosh(v)
$$
因此，[雅可比行列式](@entry_id:137120) $J = \det(\frac{\partial x'}{\partial x}) = (\det A)^{-1}$。我们先计算 $\det A$：
$$
\det A = \frac{\partial x}{\partial u} \frac{\partial y}{\partial v} - \frac{\partial x}{\partial v} \frac{\partial y}{\partial u} = \cosh(v)(u \cosh(v)) - (u \sinh(v))(\sinh(v)) = u(\cosh^2 v - \sinh^2 v) = u
$$
所以 $J = u^{-1}$。[张量密度](@entry_id:191194)的变换法则为：
$$
\mathcal{T}'_{kl} = (J)^W \frac{\partial x^i}{\partial x'^k} \frac{\partial x^j}{\partial x'^l} \mathcal{T}_{ij} = (u^{-1})^W \frac{\partial x^i}{\partial x'^k} \frac{\partial x^j}{\partial x'^l} \delta_{ij} = u^{-W} \sum_{i=1}^2 \frac{\partial x^i}{\partial x'^k} \frac{\partial x^i}{\partial x'^l}
$$
我们计算对角分量：
$$
\mathcal{T}'_{11} = u^{-W} \left[ \left(\frac{\partial x}{\partial u}\right)^2 + \left(\frac{\partial y}{\partial u}\right)^2 \right] = u^{-W} (\cosh^2 v + \sinh^2 v) = u^{-W} \cosh(2v)
$$
$$
\mathcal{T}'_{22} = u^{-W} \left[ \left(\frac{\partial x}{\partial v}\right)^2 + \left(\frac{\partial y}{\partial v}\right)^2 \right] = u^{-W} (u^2 \sinh^2 v + u^2 \cosh^2 v) = u^{-W} u^2 (\sinh^2 v + \cosh^2 v) = u^{2-W} \cosh(2v)
$$
最终，迹为：
$$
\text{tr}(\mathcal{T}') = \mathcal{T}'_{11} + \mathcal{T}'_{22} = u^{-W} \cosh(2v) + u^{2-W} \cosh(2v) = u^{-W}(1+u^2)\cosh(2v)
$$
这个例子系统地演示了从坐标关系出发，通过计算[雅可比矩阵](@entry_id:264467)和应用变换法则来得到新[坐标系](@entry_id:156346)下[张量密度](@entry_id:191194)分量的完整步骤。

### [非张量对象](@entry_id:201374)：克氏符号

最后，为了更好地理解[张量密度](@entry_id:191194)的定义，我们必须考察一个不符合其变换法则的重要对象：**克氏符号 (Christoffel symbol)** $\Gamma^k_{ij}$。它在[坐标变换](@entry_id:172727)下的行为是：
$$
\Gamma'^{k}_{ij} = \frac{\partial x'^k}{\partial x^a} \frac{\partial x^b}{\partial x'^i} \frac{\partial x^c}{\partial x'^j} \Gamma^a_{bc} + \frac{\partial x'^k}{\partial x^a} \frac{\partial^2 x^a}{\partial x'^i \partial x'^j}
$$
与[张量密度](@entry_id:191194)的变换法则相比，[克氏符号的变换法则](@entry_id:180944)包含一个额外的、不依赖于原分量 $\Gamma^a_{bc}$ 的**非齐次项 (inhomogeneous term)**。这个加性项的存在，使得它的变换不是线性和齐次的，因此无法写成 $\Gamma' = J^W (\dots) \Gamma$ 的形式。这意味着克氏符号既不是张量，也不是任何权重的[张量密度](@entry_id:191194) [@problem_id:1542757]。正是因为克氏符号的这种“病态”变换行为，我们才需要引入协变导数，其定义恰好利用克氏符号来抵消这一非齐次项，从而保证导数运算作用在张量上能得到另一个张量。

总之，[张量密度](@entry_id:191194)是张量概念的自然推广，它为在[广义坐标](@entry_id:156576)系中建立积分[不变量](@entry_id:148850)提供了严格的数学框架，是现代[场论](@entry_id:155241)和广义相对论等理论不可或缺的组成部分。