## 引言
[Sturm-Liouville理论](@entry_id:142729)是[数学物理](@entry_id:265403)方法中的基石，为求解科学与工程领域中大量的[二阶常微分方程](@entry_id:204212)提供了强有力的框架。然而，许多学习者对其理解往往停留在表面，未能系统地把握其深刻的数学结构及其在不同学科间的统一作用。本文旨在填补这一知识鸿沟，引领读者进行一次从核心原理到实际应用的深度探索。在接下来的内容中，我们将首先在“原理与机制”一章中，深入剖析[Sturm-Liouville问题](@entry_id:173382)的数学核心，包括自伴性、[谱定理](@entry_id:136620)和[变分原理](@entry_id:198028)等。随后，在“应用与跨学科联系”一章中，我们将展示该理论如何在[振动](@entry_id:267781)系统、量子力学、数值方法乃至[非线性动力学](@entry_id:190195)等多个领域大放异彩。最后，通过“动手实践”环节，读者将有机会将理论应用于具体问题，从而巩固和深化所学知识。

## 原理与机制

在介绍章节之后，我们现在深入探讨[Sturm-Liouville理论](@entry_id:142729)的核心原理和内在机制。本章将系统地阐述Sturm-[Liouville方程](@entry_id:156422)的规范形式、自伴性、[本征值](@entry_id:154894)的谱性质、[变分原理](@entry_id:198028)以及渐近行为等关键概念。这些内容构成了求解大量物理与工程问题的数学基础。

### [规范形](@entry_id:153058)式与自伴性

[Sturm-Liouville理论](@entry_id:142729)的核心是研究一类特定的[二阶线性常微分方程](@entry_id:189146)。一个一般的[二阶线性齐次常微分方程](@entry_id:172835)可以写作 $a_2(x)y'' + a_1(x)y' + a_0(x)y = 0$。通过引入一个[积分因子](@entry_id:177812)，这[类方程](@entry_id:144428)通常可以转化为Sturm-Liouville的**规范形式 (canonical form)**：

$$
\frac{d}{dx}\left[p(x)\frac{dy}{dx}\right] + [q(x) + \lambda w(x)]y = 0
$$

这里，$y(x)$ 是待求函数，$\lambda$ 是一个参数，通常称为**[本征值](@entry_id:154894) (eigenvalue)**。函数 $p(x)$、$q(x)$ 和 $w(x)$ 具有特定的名称和物理意义：$p(x)$ 是Sturm-Liouville系数，$q(x)$ 常被称为**[势函数](@entry_id:176105) (potential function)**，而 $w(x)$ 则是**权重函数 (weight function)** 或密度函数。在物理问题中，$p(x)$ 可能与介质的传导性或几何形状有关，$q(x)$ 代表一个背景势场，而 $w(x)$ 则常与系统各部分的质量或能量密度[分布](@entry_id:182848)有关。

将一个普通[二阶微分方程](@entry_id:269365)转化为Sturm-Liouville规范形式是一个基本技巧。考虑一个在物理学中出现的方程 [@problem_id:1151004]：
$$
\frac{d^2y}{dx^2} + \frac{2}{x}\frac{dy}{dx} + (\lambda - V_0)y = 0
$$
其中 $x > 0$，$V_0$ 是一个实常数。此方程并非规范形式。为了转化它，我们寻找一个[积分因子](@entry_id:177812) $\mu(x)$，使得方程的前两项 $\mu(x)y'' + \mu(x)\frac{2}{x}y'$ 可以写成 $(\mu(x)y')'$ 的形式。通过展开导数 $(\mu y')' = \mu y'' + \mu' y'$，我们发现需要满足 $\mu' = \mu \frac{2}{x}$。这个简单的一阶方程的解是 $\mu(x) = x^2$（忽略常[数乘](@entry_id:155971)子）。将原方程两边同乘以 $x^2$，我们得到：
$$
x^2\frac{d^2y}{dx^2} + 2x\frac{dy}{dx} + (\lambda - V_0)x^2y = 0
$$
前两项现在可以完美地合并为 $\frac{d}{dx}[x^2 y']$。于是，方程变为：
$$
\frac{d}{dx}\left[x^2\frac{dy}{dx}\right] + (\lambda x^2 - V_0 x^2)y = 0
$$
与规范形式 $\frac{d}{dx}[p(x)y'] + [q(x) + \lambda w(x)]y = 0$ 逐项对比，我们便可识别出该问题的系数：$p(x) = x^2$，$q(x) = -V_0 x^2$，以及权重函数 $w(x) = x^2$。

[Sturm-Liouville形式](@entry_id:171486)的重要性在于它与**自伴算子 (self-adjoint operator)** 的深刻联系。定义[Sturm-Liouville算子](@entry_id:171782) $L$ 为：
$$
L[y] = \frac{1}{w(x)} \left( -\frac{d}{dx}\left[p(x)\frac{dy}{dx}\right] - q(x)y \right)
$$
[本征值问题](@entry_id:142153)便可简洁地写成 $L[y] = \lambda y$。一个算子 $L$ 在带有权重 $w(x)$ 的[内积空间](@entry_id:271570)中被称为自伴的，如果它满足关系 $\langle L[u], v \rangle_w = \langle u, L[v] \rangle_w$。此处的[加权内积](@entry_id:163877)定义为 $\langle u, v \rangle_w = \int_a^b u(x) \overline{v(x)} w(x) dx$。

算子 $L$ 的自伴性可以通过**[拉格朗日恒等式](@entry_id:151058) (Lagrange's identity)** 来检验。对于任意两个足够光滑的函数 $u(x)$ 和 $v(x)$，我们有：
$$
\int_a^b \left( \overline{v} L[u] - u \overline{L[v]} \right) w(x) dx = \left[ p(x) \left( u(x) \overline{v'(x)} - \overline{v(x)} u'(x) \right) \right]_a^b
$$
这个恒等式的右边是一个边界项。如果这个边界项对于我们所关心的函数类恒为零，那么算子 $L$ 在该函数空间上就是自伴的。这种性质保证了[本征值](@entry_id:154894)和本征函数具有一系列优美的数学特性。

从另一个角度看，我们也可以主动寻找一个权重函数 $w(x)$，使得给定的一个微分算子 $A[y]$ 乘以 $w(x)$ 后，得到的算子 $w(x)A[y]$ 能够写成Sturm-Liouville的[微分形式](@entry_id:146747) $(p(x)y')' + \tilde{q}(x)y$，从而成为**形式自伴 (formally self-adjoint)** 的 [@problem_id:1150997]。例如，对于算子 $L[y] = -y'' - \frac{4}{x}y'$，我们希望找到 $w(x)$ 使得 $-w(x)y'' - \frac{4w(x)}{x}y'$ 等于 $(p(x)y')'$。比较 $y''$ 的系数可知 $p(x)=-w(x)$。比较 $y'$ 的系数可知 $p'(x) = -w'(x)$ 必须等于原式中 $y'$ 的系数 $-\frac{4w(x)}{x}$。这导出了关于 $w(x)$ 的[微分方程](@entry_id:264184) $w'(x) = \frac{4w(x)}{x}$，其解为 $w(x) = C x^4$。通过特定的[归一化条件](@entry_id:156486)，如 $w(1)=1$，我们可以唯一确定 $w(x)=x^4$。

### 边界条件与[Sturm-Liouville问题](@entry_id:173382)

仅有[微分方程](@entry_id:264184)不足以构成一个完整的物理或数学问题；我们还需要**边界条件 (boundary conditions)**。一个[Sturm-Liouville问题](@entry_id:173382)由Sturm-[Liouville方程](@entry_id:156422)和定义在区间 $[a,b]$ 端点上的边界条件共同组成。

边界条件的主要作用是限定解的范围，并确保[拉格朗日恒等式](@entry_id:151058)中的边界项为零，从而使算子成为真正的自伴算子。常见的边界条件类型包括：
1.  **分离边界条件 (separated boundary conditions)**：每个端点的条件只涉及该端点的函数值和导数值。
    $$
    \alpha_1 y(a) + \alpha_2 y'(a) = 0 \\
    \beta_1 y(b) + \beta_2 y'(b) = 0
    $$
    其中 $\alpha_1, \alpha_2, \beta_1, \beta_2$ 是实常数，且 $\alpha_1^2 + \alpha_2^2 > 0$，$\beta_1^2 + \beta_2^2 > 0$。常见的特例有**狄利克雷 (Dirichlet)** 条件 ($y(a)=0$) 和**诺伊曼 (Neumann)** 条件 ($y'(a)=0$)。

2.  **周期性边界条件 (periodic boundary conditions)**：函数及其导数在区间的两端点处的值相关联。
    $$
    y(a) = y(b) \\
    p(a)y'(a) = p(b)y'(b)
    $$

当函数 $u$ 和 $v$ 满足这些类型的边界条件时，可以证明[拉格朗日恒等式](@entry_id:151058)右侧的边界项 $\left[ p(u\overline{v}' - \overline{v}u') \right]_a^b$ 等于零。这使得[Sturm-Liouville算子](@entry_id:171782)在其定义域（即满足给定边界条件的光滑函数空间）上是自伴的。

如果边界条件不满足使边界项为零的特定形式，那么算子的自伴性就会被破坏，其[本征函数](@entry_id:154705)也就不再保证具有正交性。考虑一个在 $[0, \pi]$ 上的简单问题 $u'' + \lambda u = 0$，但其边界条件非常规：$u(\pi) = 2u(0)$ 和 $u'(\pi) = 0$ [@problem_id:1151002]。对于这个系统，[拉格朗日恒等式](@entry_id:151058)的边界项为 $[u_1 u_2' - u_2 u_1']_0^\pi$。代入边界条件后，该表达式变为 $u_1(\pi)u_2'(\pi) - u_2(\pi)u_1'(\pi) - (u_1(0)u_2'(0) - u_2(0)u_1'(0)) = - (u_1(0)u_2'(0) - u_2(0)u_1'(0))$。这通常不为零。因此，该问题不是自伴的，其不同[本征值](@entry_id:154894)对应的本征函数不保证正交。例如，可以验证函数 $u_1(x) = \cos(\frac{x}{3}) + \sqrt{3}\sin(\frac{x}{3})$ 和 $u_2(x) = \cos(\frac{5x}{3}) - \sqrt{3}\sin(\frac{5x}{3})$ 都是该问题的本征函数，但它们之间的积分为 $\int_0^\pi u_1(x) u_2(x) dx = -\frac{3\sqrt{3}}{4}$，显然不为零。这个例子清晰地表明，恰当的边界条件是[Sturm-Liouville理论](@entry_id:142729)中一系列重要性质的基石。

### [本征值与本征函数](@entry_id:167055)的基本性质

当一个[Sturm-Liouville问题](@entry_id:173382)是自伴的（即方程为[Sturm-Liouville形式](@entry_id:171486)，系数为实函数，且边界条件为自伴类型），其[本征值](@entry_id:154894) $\lambda$ 和[本征函数](@entry_id:154705) $y(x)$ 会展现出一系列非凡的性质。

#### [本征值](@entry_id:154894)的实数性

自伴[Sturm-Liouville问题](@entry_id:173382)的所有[本征值](@entry_id:154894)都是实数。这个性质是自伴性的直接结果。证明思路如下：假设 $\lambda$ 是一个复[本征值](@entry_id:154894)，对应的[本征函数](@entry_id:154705)为 $y(x)$。根据定义有 $L[y] = \lambda y$。我们计算[内积](@entry_id:158127) $\langle L[y], y \rangle_w$：
$$
\langle L[y], y \rangle_w = \langle \lambda y, y \rangle_w = \lambda \langle y, y \rangle_w = \lambda \int_a^b |y(x)|^2 w(x) dx
$$
利用算子的自伴性，我们又有：
$$
\langle L[y], y \rangle_w = \langle y, L[y] \rangle_w = \langle y, \lambda y \rangle_w = \int_a^b y(x) \overline{\lambda y(x)} w(x) dx = \overline{\lambda} \langle y, y \rangle_w
$$
比较两式可得 $(\lambda - \overline{\lambda}) \langle y, y \rangle_w = 0$。由于 $y(x)$ 是非零的本征函数且 $w(x)>0$，[内积](@entry_id:158127) $\langle y, y \rangle_w$ 是一个正数。因此，必须有 $\lambda - \overline{\lambda} = 0$，即 $\lambda = \overline{\lambda}$，证明了 $\lambda$ 是实数。

这个结论依赖于算子中所有系数（包括权重函数 $w(x)$）都是实数。如果 $w(x)$ 是复函数，情况会变得复杂 [@problem_id:2129568]。考虑一个具有实系数 $p(x), q(x)$ 但复权重函数 $w(x)$ 的问题 $L[y] = \lambda w(x) y$。对整个方程取复共轭，由于 $L$ 是实算子（[微分](@entry_id:158718)和实系数函数），我们有 $\overline{L[y]} = L[\overline{y}]$。因此，共轭方程为 $L[\overline{y}] = \overline{\lambda} \overline{w(x)} \overline{y}$。这表明 $\overline{\lambda}$ 是一个不同问题的[本征值](@entry_id:154894)，其权重函数为 $\overline{w(x)}$，而不是原来的 $w(x)$。除非 $w(x)$ 是实函数（即 $\overline{w(x)}=w(x)$），否则我们不能保证 $\overline{\lambda}$ 也是原问题的[本征值](@entry_id:154894)。

#### [本征函数的正交性](@entry_id:150712)

对应于不同[本征值](@entry_id:154894)的[本征函数](@entry_id:154705)是相互**正交 (orthogonal)** 的，其正交性由权重函数 $w(x)$ 定义。设 $\lambda_m$ 和 $\lambda_n$ 是两个不同的[本征值](@entry_id:154894)，对应的本征函数分别为 $y_m(x)$ 和 $y_n(x)$。我们有：
$$
L[y_m] = \lambda_m y_m \quad \text{和} \quad L[y_n] = \lambda_n y_n
$$
利用算子的自伴性（对于实[本征值](@entry_id:154894)），我们有 $\langle L[y_m], y_n \rangle_w = \langle y_m, L[y_n] \rangle_w$。代入本征方程，得到：
$$
\langle \lambda_m y_m, y_n \rangle_w = \langle y_m, \lambda_n y_n \rangle_w
$$
$$
\lambda_m \langle y_m, y_n \rangle_w = \lambda_n \langle y_m, y_n \rangle_w
$$
移项后得到 $(\lambda_m - \lambda_n) \langle y_m, y_n \rangle_w = 0$。因为我们假设 $\lambda_m \neq \lambda_n$，所以必须有 $\langle y_m, y_n \rangle_w = \int_a^b y_m(x) \overline{y_n(x)} w(x) dx = 0$。这就证明了正交性。

#### [正则Sturm-Liouville问题](@entry_id:167559)的谱定理

对于**[正则Sturm-Liouville问题](@entry_id:167559) (regular Sturm-Liouville problem)**，即在有限[闭区间](@entry_id:136474) $[a,b]$ 上，$p(x)$ 和 $w(x)$ 始终为正，且所有系数函数连续，我们有以下深刻的谱定理 [@problem_id:2203116]：
*   存在一个无穷序列的实数[本征值](@entry_id:154894) $\lambda_0, \lambda_1, \lambda_2, \dots$。
*   这些[本征值](@entry_id:154894)是离散的，没有有限的[聚点](@entry_id:177089)，并且可以被排序为一个严格递增的序列：$\lambda_0  \lambda_1  \lambda_2  \dots$。
*   该序列无[上界](@entry_id:274738)，即 $\lim_{n \to \infty} \lambda_n = \infty$。
*   对于每个[本征值](@entry_id:154894) $\lambda_n$，（对于正则问题）存在一个唯一的（在常数因子意义下）实值[本征函数](@entry_id:154705) $y_n(x)$。
*   由所有本征函数构成的集合 $\{y_n(x)\}_{n=0}^\infty$ 是一个完备的[正交基](@entry_id:264024)。这意味着任何在 $[a,b]$ 上满足相同边界条件的“行为良好”的函数，都可以唯一地展开为这些本征函数的级数（类似于[傅里叶级数](@entry_id:139455)）。

这些性质是[Sturm-Liouville理论](@entry_id:142729)如此强大的原因。它为求解[偏微分方程的[分离变量](@entry_id:171323)法](@entry_id:168509)提供了理论基础，保证了我们总能找到一组“基本[振动](@entry_id:267781)模式”（即[本征函数](@entry_id:154705)），并将任何复杂的[振动](@entry_id:267781)表示为这些[基本模式](@entry_id:165201)的叠加。

### 定量分析与变分原理

除了定性性质，我们还可以对Sturm-Liouville[本征值](@entry_id:154894)进行定量估计。一个极其有力的工具是**[瑞利商](@entry_id:137794) (Rayleigh quotient)**。对于算子 $L$，瑞利商定义为：
$$
R[y] = \frac{\langle L[y], y \rangle_w}{\langle y, y \rangle_w} = \frac{\int_a^b y L[y] w dx}{\int_a^b y^2 w dx}
$$
(此处为简便，假设 $y$ 为实函数)。如果 $y$ 是一个[本征函数](@entry_id:154705) $y_n$，那么 $L[y_n]=\lambda_n y_n$，瑞利商的值就是对应的[本征值](@entry_id:154894) $\lambda_n$。

对于 $L[y] = \frac{1}{w}(- (py')' - qy)$ 的形式，并将 $y$ 满足的自伴边界条件代入[拉格朗日恒等式](@entry_id:151058)，[瑞利商](@entry_id:137794)可以被改写为：
$$
R[y] = \frac{\int_a^b \left( p(x) [y'(x)]^2 + q(x) [y(x)]^2 \right) dx}{\int_a^b w(x) [y(x)]^2 dx}
$$
这个形式在物理上非常直观：分子代表系统的总能量（动能项 $p(y')^2$ 和势能项 $q y^2$），分母是一个归一化因子。

**[瑞利-里兹变分原理](@entry_id:185834) (Rayleigh-Ritz variational principle)** 指出，最低[本征值](@entry_id:154894) $\lambda_0$ 等于[瑞利商](@entry_id:137794)在所有满足边界条件的非零函数中可能取到的最小值。更高阶的[本征值](@entry_id:154894) $\lambda_n$ 可以通过在与前 $n$ 个本征函数 $y_0, \dots, y_{n-1}$ 正交的函数[子空间](@entry_id:150286)中最小化[瑞利商](@entry_id:137794)来获得。

[变分原理](@entry_id:198028)是估计[本征值](@entry_id:154894)的强大工具。例如，考虑一个[Sturm-Liouville问题](@entry_id:173382) $-y'' + q(x)y = \lambda y$，边界条件为 $y(0)=y(L)=0$，其中势函数 $q(x)$ 是定义在 $[0,L]$ 上的任意非负[连续函数](@entry_id:137361)，即 $q(x) \ge 0$ [@problem_id:1151020]。该问题的最低[本征值](@entry_id:154894) $\lambda_1(q)$ 由瑞利商的最小值给出：
$$
\lambda_1(q) = \min_{y} \frac{\int_0^L \left( [y'(x)]^2 + q(x) [y(x)]^2 \right) dx}{\int_0^L [y(x)]^2 dx}
$$
由于 $q(x) \ge 0$，积分项 $\int_0^L q(x) [y(x)]^2 dx \ge 0$。因此，对于任何函数 $y(x)$，我们都有：
$$
\frac{\int_0^L \left( [y']^2 + q y^2 \right) dx}{\int_0^L y^2 dx} \ge \frac{\int_0^L [y']^2 dx}{\int_0^L y^2 dx}
$$
这意味着 $\lambda_1(q)$ 的值必然大于或等于当 $q(x)$ 恒等于零时的最低[本征值](@entry_id:154894)。当 $q(x) \equiv 0$ 时，问题简化为 $-y'' = \lambda y$，其在狄利克雷边界条件下的最低[本征值](@entry_id:154894)为 $\lambda_1(0) = (\frac{\pi}{L})^2$。因此，对于所有非负的势函数 $q(x)$，最低[本征值](@entry_id:154894)的[下确界](@entry_id:140118) (infimum) 就是 $\frac{\pi^2}{L^2}$。这个下确界在 $q(x)$ 选择为零函数时达到。

### 高级主题与[渐近行为](@entry_id:160836)

[Sturm-Liouville理论](@entry_id:142729)还包含许多更深入和精细的结果，这些结果在理论物理和[应用数学](@entry_id:170283)中至关重要。

#### [比较定理](@entry_id:637672)与[本征值](@entry_id:154894)的交错

Sturm的理论提供了一系列**[比较定理](@entry_id:637672) (comparison theorems)**，用于比较不同Sturm-[Liouville方程](@entry_id:156422)解的行为。其中一个重要推论是**[本征值交错](@entry_id:180866)定理 (eigenvalue interlacing theorem)**。例如，对于同一个Sturm-[Liouville方程](@entry_id:156422)，在区间 $[a,b]$ 上分别施加[狄利克雷边界条件](@entry_id:173524)（$y(a)=y(b)=0$）和[诺伊曼边界条件](@entry_id:142124)（$y'(a)=y'(b)=0$），得到的两组[本征值](@entry_id:154894) $\{\lambda_n^D\}$ 和 $\{\mu_n^N\}$ 会严格交错：
$$
\mu_0  \lambda_0  \mu_1  \lambda_1  \mu_2  \dots
$$
这种交错性质可以通过分析一个依赖于[本征值](@entry_id:154894) $\lambda$ 的**特征函数 (characteristic function)** 来严格证明 [@problem_id:1151055]。考虑一个满足 $y(a, \lambda) = 0$ 和 $y'(a, \lambda) = 1$ 的解 $y(x, \lambda)$。我们可以定义一个在端点 $b$ 的函数 $F(\lambda) = p(b) \frac{y'(b, \lambda)}{y(b, \lambda)}$。这个[函数的零点](@entry_id:180934)对应于诺伊曼[本征值](@entry_id:154894)（$y'(b)=0$），而极点对应于狄利克雷[本征值](@entry_id:154894)（$y(b)=0$）。通过复杂的推导，可以证明这个函数的导数总是负的：
$$
\frac{dF}{d\lambda} = -\frac{\int_a^b w(x) [y(x, \lambda)]^2 dx}{[y(b, \lambda)]^2}  0
$$
由于 $F(\lambda)$ 在两个相邻的极点（狄利克雷[本征值](@entry_id:154894)）之间是单调递减的，它必然从 $+\infty$ 降到 $-\infty$，因此在这个区间内必须且仅有一次穿过零点。这优雅地证明了狄利克雷和诺伊曼[本征值](@entry_id:154894)的严格交错性。

此外，[本征值](@entry_id:154894)也依赖于问题的其他参数，如区间长度。例如，在量子力学中，Pöschl-Teller势 $V(x) = -V_0 \operatorname{sech}^2(x)$ 是一个重要的可解模型。考虑算子 $L[y] = -y'' - 6\operatorname{sech}^2(x)y$ 在对称区间 $[-a, a]$ 上并施加[狄利克雷边界条件](@entry_id:173524)。随着区间半长度 $a$ 的增加，最低[本征值](@entry_id:154894) $\lambda_0$ 会减小。当 $\lambda_0$ 首次变为零时，算子就不再是正定的。这个临界半长度 $a_{cr}$ 对应于零能量方程 $L[y]=0$ 首次出现满足边界条件的非[平凡解](@entry_id:155162)的时刻 [@problem_id:1150982]。通过变量替换 $z = \tanh(x)$，该零能量方程可以转化为[勒让德方程](@entry_id:264827)，其解为勒让德多项式。通过求解 $y(a_{cr})=0$，可以精确地得到临界长度 $a_{cr} = \operatorname{arccosh}(\sqrt{3/2})$。

#### [本征值](@entry_id:154894)的渐近行为

当序号 $n \to \infty$ 时，[本征值](@entry_id:154894) $\lambda_n$ 和本征函数 $y_n$ 的行为趋于规律化。研究这种**[渐近行为](@entry_id:160836) (asymptotic behavior)** 对理解高频[振动](@entry_id:267781)或高能级[量子态](@entry_id:146142)至关重要。一个关键技术是**刘维尔变换 (Liouville transformation)**，它能将一般的Sturm-[Liouville方程](@entry_id:156422)转化为更简单的**刘维尔正规形式 (Liouville normal form)**：$u''(z) + (\lambda - Q(z))u(z) = 0$。

当[本征值](@entry_id:154894) $\lambda$ 很大时，势函数 $Q(z)$ 的影响相对较小，方程近似为 $u''(z) + \lambda u(z) = 0$。利用这个近似，我们可以推导出狄利克雷和诺伊曼[本征值](@entry_id:154894)的[渐近公式](@entry_id:189846)。对于变换后的区间 $[0, L]$，其中 $L = \int_a^b \sqrt{w(x)/p(x)} dx$，可以得到 [@problem_id:1151105]：
$$
\lambda_n^D \sim \left( \frac{(n+1)\pi}{L} \right)^2 \quad \text{和} \quad \mu_n^N \sim \left( \frac{n\pi}{L} \right)^2 \quad (\text{for large } n)
$$
由此，我们可以计算出狄利克雷和诺伊曼[本征值](@entry_id:154894)之差的渐近主项：
$$
\lambda_n^D - \mu_n^N \sim \frac{((n+1)^2 - n^2)\pi^2}{L^2} = \frac{(2n+1)\pi^2}{L^2} \sim \frac{2n\pi^2}{L^2}
$$
代回 $L$ 的表达式，我们得到一个依赖于原始系数 $p(x)$ 和 $w(x)$ 的深刻结果：
$$
\lambda_n^D - \mu_n^N \sim \frac{2n\pi^2}{\left(\int_a^b \sqrt{\frac{w(x)}{p(x)}} dx\right)^2}
$$
这揭示了在高能极限下，不同边界条件导致的能谱差异是如何随能量（或序号 $n$）变化的。

#### [奇异Sturm-Liouville问题](@entry_id:173343)

当区间是无限的，或者系数 $p(x)$ 或 $w(x)$ 在区间的某个端点为零或发散时，我们称之为**[奇异Sturm-Liouville问题](@entry_id:173343) (singular Sturm-Liouville problem)**。许多重要的物理方程，如[贝塞尔方程](@entry_id:164013)、[勒让德方程](@entry_id:264827)和[埃尔米特方程](@entry_id:196615)，都属于此类。

在[奇异点](@entry_id:199525)附近，解的行为可能非常复杂。外尔 (Hermann Weyl) 的工作将[奇点](@entry_id:137764)分为两类：**[极限点](@entry_id:177089)型 (limit-point case)** 和**极限圆型 (limit-circle case)**。这个分类至关重要，因为它决定了在[奇点](@entry_id:137764)处是否需要以及需要施加多少个边界条件才能使问题自伴。简而言之，极限点型[奇点](@entry_id:137764)“天然地”表现良好，不需要额外边界条件；而极限圆型[奇点](@entry_id:137764)则需要一个边界条件来唯一确定物理上有意义的解。

一个端点属于哪种类型，取决于在[奇点](@entry_id:137764)附近，方程 $L[y]=\lambda y$ 的所有解是否关于权重 $w(x)$ 平方可积。如果所有解都平方可积，则为极限圆型；否则为极限点型。这个分类可以通过分析系数函数在[奇点](@entry_id:137764)附近的行为来确定。例如，考虑在 $(0, 1]$ 上的算子，其系数呈[幂律](@entry_id:143404)行为 $p(x) = x^\beta, q(x) = C x^{-\alpha}, w(x) = x^\gamma$ [@problem_id:1151120]。在[奇点](@entry_id:137764) $x=0$ 处的分类，其性质在某个[临界指数](@entry_id:142071) $\alpha_c$ 处会发生根本性转变。这个转变点标志着[微分方程](@entry_id:264184)中“动能项” $-(py')'$ 和“势能项” $qy$ 的相对主导地位发生了变化。通过细致的[渐近分析](@entry_id:160416)可以发现，这个临界指数由 $\alpha_c = 2 - \beta$ 给出。当 $\alpha > \alpha_c$ 时，势能项在 $x \to 0$ 处的影响变得非常强，通常导致极限点行为。当 $\alpha  \alpha_c$ 时，动能项占主导，其行为更接近于可解的[欧拉-柯西方程](@entry_id:191139)。这个[临界指数](@entry_id:142071)的确定，为处理带有复杂[奇点](@entry_id:137764)的物理问题提供了重要的理论指导。