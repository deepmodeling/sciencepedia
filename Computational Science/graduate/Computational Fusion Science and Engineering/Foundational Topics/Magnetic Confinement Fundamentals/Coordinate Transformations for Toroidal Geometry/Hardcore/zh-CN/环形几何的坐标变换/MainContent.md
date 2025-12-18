## 引言
在[磁约束聚变](@entry_id:180408)研究中，对[托卡马克](@entry_id:160432)和[仿星器](@entry_id:160569)等装置内[环形等离子体](@entry_id:202484)的精确描述，是理解和预测其行为的基石。这些装置固有的环形几何结构与[笛卡尔坐标系](@entry_id:169789)格格不入，因此，开发并应用一套专门的坐标系不仅是数学上的需要，更是物理建模的核心。本文旨在系统性地解决这一问题：如何构建一个既能精确描述复杂环形几何，又能简化关键物理过程（如粒子运动、等离子体稳定性和[能量输运](@entry_id:183081)）分析的数学框架。

为实现此目标，本文将引导读者踏上一段从基础到前沿的旅程。在“原理与机制”一章中，我们将从第一性原理出发，构建从简单环形坐标到复杂的[磁通坐标](@entry_id:1125149)系和[直场线坐标](@entry_id:1132468)系的完整理论，并深入探讨[度规张量](@entry_id:160222)和[雅可比行列式](@entry_id:137120)等核心几何概念。接着，在“应用与交叉学科联系”一章中，我们将展示这些[坐标变换](@entry_id:172727)如何在[MHD平衡](@entry_id:1127852)计算、[稳定性分析](@entry_id:144077)、回旋动理学理论以及大规模计算模拟中发挥关键作用。最后，“动手实践”部分将提供具体的练习，帮助读者将理论知识转化为解决实际问题的能力。现在，让我们从构建描述环形几何的基础语言开始。

## 原理与机制

在计算聚变科学中，对[环形等离子体](@entry_id:202484)（如[托卡马克](@entry_id:160432)和[仿星器](@entry_id:160569)中的等离子体）进行精确的物理建模，在很大程度上依赖于坐标系的恰当选择。虽然[笛卡尔坐标系](@entry_id:169789) $(x, y, z)$ 是描述三维欧几里得空间的基础，但它与[环形装置](@entry_id:188972)的[几何对称性](@entry_id:189059)和磁场拓扑结构并不匹配。因此，我们必须引入并掌握一系列专门为环形几何设计的[曲线坐标系](@entry_id:172561)。本章将从第一性原理出发，系统阐述这些坐标系的构建、它们的基本几何性质，以及它们如何与磁场结构相耦合，最终形成适用于高级[计算模型](@entry_id:637456)的强大框架。

### 环形几何的基本描述

研究[环形等离子体](@entry_id:202484)的第一步是建立一个能够精确描述其几何形状的数学框架。最直观的起点是标准的环形坐标系。

#### 环形坐标与[度规张量](@entry_id:160222)

我们可以通过一个从[参数空间](@entry_id:178581)到欧几里得空间的映射来定义一个理想的环形几何。设大半径为 $R_0$（从[对称轴](@entry_id:177299)到环管中心的距离），小半径为 $r$（在环管[截面](@entry_id:154995)内的半径）。我们引入角向坐标：极向角 $\theta$（沿小[圆环](@entry_id:163678)方向）和环向角 $\phi$（沿[大圆](@entry_id:268970)环方向）。从环形坐标 $(r, \theta, \phi)$ 到笛卡尔坐标 $(x, y, z)$ 的[标准映射](@entry_id:165002)为  ：
$$
x = (R_0 + r\cos\theta)\cos\phi
$$
$$
y = (R_0 + r\cos\theta)\sin\phi
$$
$$
z = r\sin\theta
$$
其中，我们通常假定 $R_0 > r$，以确保环面不自相交。

为了量化这个坐标系下的几何性质，我们必须引入**度规张量**（metric tensor）$g_{ij}$。其分量定义为[协变基](@entry_id:198968)矢 $\mathbf{e}_i$ 的点积，而[协变基](@entry_id:198968)矢本身是位置矢量 $\mathbf{x}(r, \theta, \phi)$ 对各个坐标的偏导数。即 $\mathbf{e}_i = \partial\mathbf{x}/\partial q^i$（其中 $q^i \in \{r, \theta, \phi\}$），且 $g_{ij} = \mathbf{e}_i \cdot \mathbf{e}_j$。

我们可以直接计算这些[基矢](@entry_id:199546)：
$$
\mathbf{e}_r = \frac{\partial\mathbf{x}}{\partial r} = (\cos\theta \cos\phi)\hat{\mathbf{i}} + (\cos\theta \sin\phi)\hat{\mathbf{j}} + (\sin\theta)\hat{\mathbf{k}}
$$
$$
\mathbf{e}_\theta = \frac{\partial\mathbf{x}}{\partial \theta} = (-r \sin\theta \cos\phi)\hat{\mathbf{i}} + (-r \sin\theta \sin\phi)\hat{\mathbf{j}} + (r \cos\theta)\hat{\mathbf{k}}
$$
$$
\mathbf{e}_\phi = \frac{\partial\mathbf{x}}{\partial \phi} = -(R_0 + r \cos\theta) \sin\phi \hat{\mathbf{i}} + (R_0 + r \cos\theta) \cos\phi \hat{\mathbf{j}}
$$
通过计算这些基矢的点积，我们可以得到度规张量的所有分量 。对角分量为：
$$
g_{rr} = \mathbf{e}_r \cdot \mathbf{e}_r = 1
$$
$$
g_{\theta\theta} = \mathbf{e}_\theta \cdot \mathbf{e}_\theta = r^2
$$
$$
g_{\phi\phi} = \mathbf{e}_\phi \cdot \mathbf{e}_\phi = (R_0 + r\cos\theta)^2
$$
而非对角分量，如 $g_{r\theta} = \mathbf{e}_r \cdot \mathbf{e}_\theta$，经计算均为零。[度规张量](@entry_id:160222)的非对角分量为零，意味着这个特定的环形坐标系是**正交的**（orthogonal）。因此，度规张量可以简洁地写成一个[对角矩阵](@entry_id:637782)：
$$
g_{ij} = \begin{pmatrix}
1  & 0  & 0 \\
0  & r^2  & 0 \\
0  & 0  & (R_0 + r \cos\theta)^2
\end{pmatrix}
$$
在[正交坐标](@entry_id:166074)系中，我们定义**标度因子**（scale factors）为 $h_i = \sqrt{g_{ii}}$。对于上述坐标系，它们分别是 $h_r = 1$，$h_\theta = r$，和 $h_\phi = R_0 + r\cos\theta$。这些标度因子量化了在每个坐标方向上，单位坐标变化对应的物理长度。例如，沿 $\theta$ 方向移动一个无穷小角度 $d\theta$，对应的物理[弧长](@entry_id:191173)是 $dl_\theta = h_\theta d\theta = r d\theta$。

#### [雅可比行列式](@entry_id:137120)与[体积元](@entry_id:267802)

在进行积分运算时，例如计算等离子体的总质量或总能量，我们需要知道[坐标变换](@entry_id:172727)下的[体积元](@entry_id:267802) $dV = dx dy dz$ 如何用环形坐标表示。这由**[雅可比行列式](@entry_id:137120)**（Jacobian determinant）$J$ 决定，其定义为由[协变基](@entry_id:198968)矢构成的平行六面体的体积：
$$
J = \det(\frac{\partial(x,y,z)}{\partial(r,\theta,\phi)}) = \mathbf{e}_r \cdot (\mathbf{e}_\theta \times \mathbf{e}_\phi)
$$
对于一个[正交坐标](@entry_id:166074)系，雅可比行列式就是三个标度因子的乘积：
$$
|J| = h_r h_\theta h_\phi
$$
代入我们之前计算的标度因子，可以得到  ：
$$
|J| = 1 \cdot r \cdot (R_0 + r\cos\theta) = r(R_0 + r\cos\theta)
$$
因此，无穷小体积元 $dV$ 为：
$$
dV = |J| \,dr\,d\theta\,d\phi = r(R_0 + r\cos\theta) \,dr\,d\theta\,d\phi
$$
这个表达式直观地反映了环形几何的特点：距离磁轴越远（$r$ 越大）或在环的外侧（$\cos\theta > 0$），单位坐标空间的体积越大。

#### 环形坐标中的微分算子

物理定律通常用[微分算子](@entry_id:140145)（如梯度、散度和拉普拉斯算子）来表达。在[曲线坐标系](@entry_id:172561)中，这些算子的形式也由[度规张量](@entry_id:160222)或标度因子决定。例如，一个[标量场](@entry_id:151443) $f(r, \theta, \phi)$ 的梯度 $\nabla f$ 在[正交坐标](@entry_id:166074)系中可以表示为 ：
$$
\nabla f = \frac{\hat{\mathbf{e}}_r}{h_r} \frac{\partial f}{\partial r} + \frac{\hat{\mathbf{e}}_\theta}{h_\theta} \frac{\partial f}{\partial \theta} + \frac{\hat{\mathbf{e}}_\phi}{h_\phi} \frac{\partial f}{\partial \phi}
$$
其中 $\hat{\mathbf{e}}_i = \mathbf{e}_i / h_i$ 是归一化的单位[基矢](@entry_id:199546)。代入我们的标度因子，得到：
$$
\nabla f = \hat{\mathbf{e}}_r \frac{\partial f}{\partial r} + \frac{\hat{\mathbf{e}}_\theta}{r} \frac{\partial f}{\partial \theta} + \frac{\hat{\mathbf{e}}_\phi}{R_0 + r\cos\theta} \frac{\partial f}{\partial \phi}
$$
这个表达式是进行输运、MHD稳定性和波传播等计算的出发点。

### [磁通坐标](@entry_id:1125149)系

尽管几何环形坐标系为我们提供了一个起点，但它并未考虑等离子体中最重要的结构——磁场。磁约束聚变的核心思想是利用磁[场线](@entry_id:172226)构建一系列嵌套的、闭合的**[磁通面](@entry_id:751623)**（magnetic flux surfaces），等离子体被限制在这些面上。为了更自然地描述这一物理图像，我们需要引入与磁场拓扑结构相适应的**[磁通坐标](@entry_id:1125149)系**（flux coordinates）。

#### 磁通面与磁通函数

一个理想的[磁通面](@entry_id:751623) $S$ 是一个磁场 $\mathbf{B}$ 处处与其相切的曲面。用数学语言来说，如果 $\mathbf{n}_S$ 是曲面 $S$ 的[单位法向量](@entry_id:178851)，那么在 $S$ 上的每一点都满足 $\mathbf{B} \cdot \mathbf{n}_S = 0$。对于[环形等离子体](@entry_id:202484)，这些磁通面通常是嵌套的环面。

为了给这些嵌套的[磁通面](@entry_id:751623)“贴标签”，我们需要定义一个在每个[磁通面](@entry_id:751623)上都取常数值的量，即**磁通函数**（flux function）。两个最重要的磁通函数是**环向磁通**（toroidal flux）$\Phi$ 和**极向磁通**（poloidal flux）$\psi$ 。

- **环向磁通 $\Phi(S)$** 定义为穿过以一条极向回路 $C_{\text{pol}}$ 为边界的任意[截面](@entry_id:154995) $\Sigma_{\text{pol}}$ 的磁通量。
  $$ \Phi(S) = \int_{\Sigma_{\text{pol}}} \mathbf{B} \cdot \mathrm{d}\mathbf{S}, \quad \text{其中 } \partial\Sigma_{\text{pol}} = C_{\text{pol}} \subset S $$
- **极向磁通 $\psi(S)$** 定义为穿过以一条环向回路 $C_{\text{tor}}$ 为边界的“环孔”的任意[截面](@entry_id:154995) $\Sigma_{\text{tor}}$ 的磁通量。
  $$ \psi(S) = \int_{\Sigma_{\text{tor}}} \mathbf{B} \cdot \mathrm{d}\mathbf{S}, \quad \text{其中 } \partial\Sigma_{\text{tor}} = C_{\text{tor}} \subset S $$
  （注意：在文献中，$\psi$ 有时会包含一个 $2\pi$ 的归一化因子。）

这些定义之所以成立，有两个关键的物理和数学原因 ：
1.  由于磁场是无散的（麦克斯韦方程之一，$\nabla \cdot \mathbf{B} = 0$），根据高斯散度定理，穿过任何闭合曲面的总磁通量为零。这意味着上述积分的值仅依赖于其边界回路 $C$，而不依赖于所选取的具体[截面](@entry_id:154995) $\Sigma$。
2.  由于磁场线与[磁通面](@entry_id:751623)相切（$\mathbf{B} \cdot \mathbf{n}_S = 0$），如果我们在同一个[磁通面](@entry_id:751623) $S$ 上选取两条[同伦](@entry_id:139266)的回路（例如，两条不同的极向回路），它们之间的磁通量为零。这保证了 $\Phi(S)$ 和 $\psi(S)$ 的值在整个曲面 $S$ 上是唯一的，只依赖于曲面本身，而不依赖于回路的具体选择。

因此，$\psi$（或 $\Phi$）是一个在每个磁通面上都取常数的良定义的标量函数。只要磁场结构良好，$\psi$ 会随着磁通面的嵌套层次单调变化，因此可以被用作一个“径向”坐标，来标记和区分不同的[磁通面](@entry_id:751623)。这个结论非常重要，因为它不依赖于系统是否具有[轴对称](@entry_id:1130776)性，即使在复杂的三维[仿星器](@entry_id:160569)磁场中，只要存在[嵌套磁通面](@entry_id:752411)，我们就可以使用 $\psi$ 作为[径向坐标](@entry_id:165186)。

#### 场线约束与坐标的[非正交性](@entry_id:192553)

一旦我们将 $\psi$ 选定为[径向坐标](@entry_id:165186)，磁场线被约束在 $\psi = \text{const}$ 的曲面上的条件就可以用一个简洁的数学表达式来描述：
$$
\mathbf{B} \cdot \nabla\psi = 0
$$
这个等式是所有[磁通坐标](@entry_id:1125149)系理论的基石 。它的几何意义是，磁场矢量 $\mathbf{B}$ 处处垂直于 $\psi$ 的梯度方向。而我们知道，一个[标量场的梯度](@entry_id:270765)方向总是垂直于其等值面，因此 $\nabla\psi$ 指向[磁通面](@entry_id:751623)的法向方向。所以，$\mathbf{B} \cdot \nabla\psi = 0$ 精确地表达了磁场与磁通面相切的物理事实。沿着一条由[弧长](@entry_id:191173) $l$ [参数化](@entry_id:265163)的磁[场线](@entry_id:172226) $\mathbf{r}(l)$，$\psi$ 的变化率为 $\mathrm{d}\psi/\mathrm{d}l = \nabla\psi \cdot (\mathrm{d}\mathbf{r}/\mathrm{d}l) = \nabla\psi \cdot (\mathbf{B}/|\mathbf{B}|) = (\mathbf{B} \cdot \nabla\psi)/|\mathbf{B}| = 0$。这再次证明了场线被“冻结”在磁通面上。

同时，一个重要的事实是，物理上合理的[磁通坐标](@entry_id:1125149)系通常是**非正交的**。以[轴对称](@entry_id:1130776)情况为例，如果我们选择 $\zeta$ 为几何环向角 $\phi$，那么坐标 $(\theta, \zeta)$ 在磁通面上的正交性由度规张量的非对角项 $g_{\theta\zeta}$ 决定。根据一般表达式 ：
$$
g_{\theta\zeta} = (\partial_{\theta} R)(\partial_{\zeta} R) + R^2 (\partial_{\theta} \phi)(\partial_{\zeta} \phi) + (\partial_{\theta} Z)(\partial_{\zeta} Z)
$$
在[轴对称](@entry_id:1130776)且 $\phi=\zeta$ 时，由于 $R$ 和 $Z$ 不依赖于 $\zeta$，$\partial_\zeta R = 0, \partial_\zeta Z = 0$，同时 $\partial_\theta \phi = 0$，所以 $g_{\theta\zeta} = 0$，坐标系是正交的。然而，在非[轴对称](@entry_id:1130776)的[仿星器](@entry_id:160569)中，$R$ 和 $Z$ 都会依赖于 $\zeta$，导致 $(\partial_{\theta} R)(\partial_{\zeta} R) + (\partial_{\theta} Z)(\partial_{\zeta} Z)$ 一般不为零。此外，即使在[轴对称](@entry_id:1130776)情况下，如果我们为了某些目的对环向角进行重定义，例如 $\phi = \zeta + \sigma(\psi, \theta)$，也会引入非零的 $g_{\theta\zeta}$ 项。因此，[非正交性](@entry_id:192553)是环形[磁约束](@entry_id:161852)几何中的普遍特征。

### [直场线坐标](@entry_id:1132468)系

在任意选取的 $(\psi, \theta, \phi)$ 坐标系中，磁场线在 $(\theta, \phi)$ 平面上的投影通常是复杂的曲线。磁[场线](@entry_id:172226)斜率 $d\theta/d\phi = (\mathbf{B}\cdot\nabla\theta) / (\mathbf{B}\cdot\nabla\phi)$ 会随位置 $(\theta, \phi)$ 而变化。这给磁场线追踪、[稳定性分析](@entry_id:144077)和输运计算带来了极大的不便。

#### 动机与定义

为了简化分析，我们可以通过巧妙地重新定义极向角，来“拉直”磁场线。我们寻求一个新的极向角 $\Theta$，使得在 $(\Theta, \phi)$ 坐标下，磁场线的斜率在整个磁通面上是一个常数。这个常数被定义为**旋转变换**（rotational transform）$\iota(\psi)$：
$$
\frac{d\Theta}{d\phi} = \iota(\psi)
$$
满足这个条件的坐标系被称为**[直场线坐标](@entry_id:1132468)系**（straight-field-line coordinates） 。旋转变换 $\iota(\psi)$ 是一个重要的磁通函数，它描述了磁场线每环向绕行一圈，在极向角上平均前进的角度。它的倒数 $q(\psi) = 1/\iota(\psi)$ 被称为**安全因子**（safety factor）。

在[直场线坐标](@entry_id:1132468)系中，磁场线可以被一个称为**[场线](@entry_id:172226)标签**（field-line label）的量 $\alpha$ 来标记。定义 $\alpha = \Theta - \iota(\psi)\phi$，我们可以验证 $\mathbf{B} \cdot \nabla\alpha = \mathbf{B} \cdot \nabla\Theta - \iota(\psi)(\mathbf{B} \cdot \nabla\phi) = 0$。这意味着 $\alpha$ 的值在一条磁[场线](@entry_id:172226)上是恒定的，每条磁场线都对应一个唯一的 $\alpha$ 值。

此外，任何满足 $\nabla\cdot\mathbf{B}=0$ 和 $\mathbf{B}\cdot\nabla\psi=0$ 的磁场，都可以用两个[标量场](@entry_id:151443)（Clebsch势）来表示。在[直场线坐标](@entry_id:1132468)系中，这种表示尤为简洁 ：
$$
\mathbf{B} = \nabla\psi \times \nabla\alpha = \nabla\psi \times \nabla(\Theta - \iota(\psi)\phi)
$$
这种形式自动满足了磁场的无散性和与[磁通面](@entry_id:751623)相切的条件。

#### 在[微扰分析](@entry_id:178808)中的应用

[直场线坐标](@entry_id:1132468)系的巨大威力体现在对等离子体中各种微扰（如不稳定性模式）的分析中。一个具有特定[螺旋结构](@entry_id:183721)的微扰通常可以[傅里叶分解](@entry_id:160101)为形如 $\exp[i(m\Theta - n\phi)]$ 的谐波，其中 $m$ 和 $n$ 分别是极向和环向模数。

该微扰沿磁[场线](@entry_id:172226)方向的相位变化率由其平行波数 $k_\parallel$ 决定，而 $k_\parallel \propto \mathbf{B}\cdot\nabla(m\Theta - n\phi)$。利用[直场线坐标](@entry_id:1132468)的性质，我们有 ：
$$
\mathbf{B}\cdot\nabla(m\Theta - n\phi) = m(\mathbf{B}\cdot\nabla\Theta) - n(\mathbf{B}\cdot\nabla\phi) = m\iota(\psi)(\mathbf{B}\cdot\nabla\phi) - n(\mathbf{B}\cdot\nabla\phi) = (m\iota(\psi) - n)(\mathbf{B}\cdot\nabla\phi)
$$
这个结果表明，平[行波](@entry_id:1133416)数在整个磁通面上都正比于 $m\iota(\psi) - n$。当一个[磁通面](@entry_id:751623)满足**共振条件** $m\iota(\psi) - n = 0$（或 $q(\psi) = m/n$）时，该微扰沿背景磁场线的相位不再变化 ($k_\parallel=0$)。这意味着微扰的[螺旋结构](@entry_id:183721)与该磁通面上磁场线的螺旋结构完全匹配，使得微扰能够有效地与等离子体相互作用，并可能驱动不稳定性或形成[磁岛](@entry_id:1127585)。[直场线坐标](@entry_id:1132468)将复杂的空间共振问题简化为一个只依赖于[径向坐标](@entry_id:165186) $\psi$ 的代数条件。

### 用于三维平衡的先进坐标系

在[仿星器](@entry_id:160569)等完全三维的磁约束位形中，磁场结构更为复杂。为了进一步简化MHD方程，物理学家发展了更为精巧的[直场线坐标](@entry_id:1132468)系，其中最著名的是Hamada坐标和[Boozer坐标](@entry_id:746925)。它们通过对坐标系施加额外的约束，使得磁场 $\mathbf{B}$ 的某些分量形式变得特别简单。

#### 磁场的[协变与逆变](@entry_id:189600)表示

在一般的[曲线坐标系](@entry_id:172561) $(\psi, \theta, \zeta)$ 中，矢量 $\mathbf{B}$ 有两种自然的表示方法 ：
- **协变表示**：将 $\mathbf{B}$ 分解到梯度基矢（[逆变基](@entry_id:197906)矢）$\{\nabla\psi, \nabla\theta, \nabla\zeta\}$上：
  $$ \mathbf{B} = B_\psi \nabla\psi + B_\theta \nabla\theta + B_\zeta \nabla\zeta $$
  其中 $B_i = \mathbf{B} \cdot \mathbf{e}_i$ 是[协变](@entry_id:634097)分量（$\mathbf{e}_i$ 是切向[基矢](@entry_id:199546)）。由于 $\mathbf{B} \cdot \nabla\psi = 0$，我们总有 $B_\psi=0$ 的一种表示。
- **逆变表示**：将 $\mathbf{B}$ 分解到切向基矢（[协变基](@entry_id:198968)矢）$\{\partial\mathbf{r}/\partial\psi, \partial\mathbf{r}/\partial\theta, \partial\mathbf{r}/\partial\zeta\}$上：
  $$ \mathbf{B} = B^\psi \frac{\partial\mathbf{r}}{\partial\psi} + B^\theta \frac{\partial\mathbf{r}}{\partial\theta} + B^\zeta \frac{\partial\mathbf{r}}{\partial\zeta} $$
  其中 $B^i = \mathbf{B} \cdot \nabla q^i$ 是[逆变分量](@entry_id:185440)。由于 $\mathbf{B} \cdot \nabla\psi = 0$，我们总有 $B^\psi=0$。

在任意的[直场线坐标](@entry_id:1132468)系中，[逆变分量](@entry_id:185440)满足 $B^\theta/B^\zeta = \iota(\psi)$，且可以推导出它们与[雅可比行列式](@entry_id:137120) $J$ 的关系为：
$$
B^\theta = \frac{\iota(\psi)}{J(\psi,\theta,\zeta)}, \quad B^\zeta = \frac{1}{J(\psi,\theta,\zeta)}
$$

#### Hamada坐标与[Boozer坐标](@entry_id:746925)

Hamada坐标和[Boozer坐标](@entry_id:746925)都是[直场线坐标](@entry_id:1132468)，它们的区别在于对[雅可比行列式](@entry_id:137120) $J$ 施加了不同的约束 ：

- **Hamada坐标**：其定义要求雅可比行列式 $J$ 是一个磁通函数，即 $J = J(\psi)$。这个选择使得坐标格点的“体积”在[磁通面](@entry_id:751623)上是均匀的。在此条件下，[逆变分量](@entry_id:185440) $B^\theta = \iota(\psi)/J(\psi)$ 和 $B^\zeta = 1/J(\psi)$ 也都变成了磁通函数。这在研究等离子体体积相关的宏观性质时非常有用。

- **[Boozer坐标](@entry_id:746925)**：其定义要求磁场的**逆变**分量可以写为：
  $$ \mathbf{B} = I(\psi)\nabla\theta + G(\psi)\nabla\zeta $$
  其中 $I(\psi)$ 和 $G(\psi)$ 分别与环向电流和极向电流相关。这个选择极大地简化了[带电粒子漂移](@entry_id:1122290)[运动方程](@entry_id:264286)的形式，因此在研究[新经典输运](@entry_id:188243)和高能[粒子约束](@entry_id:148454)时至关重要。

#### [Boozer坐标](@entry_id:746925)[雅可比行列式](@entry_id:137120)的特殊性质

在[Boozer坐标](@entry_id:746925)中，既然[逆变分量](@entry_id:185440)是磁通函数，那么协变分量一般就不再是磁通函数了，因为[雅可比行列式](@entry_id:137120) $J$ 必须随角度变化。通过联立磁场的协变和逆变表示，可以推导出一个关于[Boozer坐标](@entry_id:746925)雅可比行列式的非凡性质 ：
$$
J B^2 = G(\psi) + \iota(\psi) I(\psi)
$$
由于上式右边所有量都是磁通函数，这意味着在[Boozer坐标](@entry_id:746925)中，乘积 $J B^2$ 在整个[磁通面](@entry_id:751623)上是一个常数。换言之，雅可比行列式 $J$ 必须与磁场强度的平方成反比：
$$
J(\psi, \theta, \phi) \propto \frac{1}{B^2(\psi, \theta, \phi)}
$$
这个性质意味着，在磁场强的区域，坐标格点的体积被压缩得更小；在磁场弱的区域，坐标格点的体积则被拉伸得更大。这种“非均匀”的坐标[网格划分](@entry_id:1127808)，恰好使得对任意物理量 $A$ 进行[磁通面平均](@entry_id:1125140)时，[磁场强度](@entry_id:197932)被均匀加权：$\langle A \rangle = \int \int A J d\theta d\phi / \int \int J d\theta d\phi$。这为理论分析和计算提供了一个极为便利的框架。

### 计算实现：磁轴处的[奇点](@entry_id:266699)

在将这些复杂的坐标系应用于实际的计算代码时，我们必须处理一个棘手的几何问题：磁轴处的[坐标奇点](@entry_id:159160)。

#### [坐标奇点](@entry_id:159160)的本质

磁轴是[嵌套磁通面](@entry_id:752411)的中心，在几何上，它是一条[闭合曲线](@entry_id:264519)，对应的[磁通面](@entry_id:751623)体积为零（$\psi=0$ 或 $r=0$）。在磁轴上，极向角 $\theta$ 的定义变得模糊不清——就像在地球的北极点，经度的概念失去了意义。

从数学上看，这个问题的根源在于描述极向[弧长](@entry_id:191173)的标度因子 $h_\theta = r$ 在 $r \to 0$ 时趋于零。这导致度规张量分量 $g_{\theta\theta} = r^2 \to 0$。而[度规张量](@entry_id:160222)的[逆矩阵](@entry_id:140380)（其分量为 $g^{ij}$）中，相应的分量 $g^{\theta\theta}$ 则会像 $1/r^2$ 一样发散。由于[梯度算子](@entry_id:1125719)等依赖于 $g^{ij}$，如 $\nabla\theta$ 的分量包含 $g^{\theta\theta}$，这些[微分算子](@entry_id:140145)在磁轴处会变得无界，从而导致数值计算的崩溃 。

#### 使用[柱坐标](@entry_id:271645)片区的[正则化方法](@entry_id:150559)

解决这个问题的标准方法是**分区域处理**（domain decomposition）或**片区法**（patching）。我们不在整个等离子体区域都使用单一的[磁通坐标](@entry_id:1125149)系，而是在磁轴附近的一个小区域内，切换回一个没有[奇点](@entry_id:266699)的、更简单的坐标系。

对于[轴对称](@entry_id:1130776)的[托卡马克](@entry_id:160432)，最自然的选择是在磁轴附近使用一个局部的[柱坐标系](@entry_id:266798) $(R, \phi, Z)$ 。具体操作如下：
1.  **定义片区**：在[径向坐标](@entry_id:165186) $\psi$ 小于某个阈值 $\psi_{\text{core}}$ 的核心区域，我们放弃使用 $(\psi, \theta, \zeta)$ 坐标。
2.  **切换坐标**：在该核心区域内，我们使用以主[对称轴](@entry_id:177299)为基准的[柱坐标](@entry_id:271645) $(R, \phi, Z)$。
3.  **表示物理场**：任何物理标量场 $f(\psi, \theta, \zeta)$ 在该区域内被表示为关于 $(R-R_0, Z)$ 的光滑泰勒级数，其中 $R_0$ 是磁轴的大半径位置。例如，$f(R, \phi, Z) \approx c_0 + c_1(R-R_0) + c_2 Z + \dots$。这种表示自然地处理了角度的退化问题，保证了物理场在磁轴处的[光滑性](@entry_id:634843)。
4.  **计算算子**：所有的[微分算子](@entry_id:140145)都在[柱坐标](@entry_id:271645)下进行计算。[柱坐标](@entry_id:271645)的[雅可比行列式](@entry_id:137120)为 $J_{\text{cyl}} = R$，在磁轴附近 $R \approx R_0 > 0$，是良定义的。其梯度、散度等算子在 $R>0$ 的区域内也都是非奇异的。

通过在[磁通坐标](@entry_id:1125149)区域和[柱坐标](@entry_id:271645)核心区域的边界上进行平滑的数据拼接，我们就可以在整个计算域内获得一个稳定且精确的数值解，成功地规避了磁轴处的[坐标奇点](@entry_id:159160)问题。这一技术是现代[聚变模拟](@entry_id:1125419)代码中不可或缺的一部分。