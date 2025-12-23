## 引言
在[地球科学](@entry_id:749876)领域，从油藏储量评估到环境[污染物[扩](@entry_id:195534)散](@entry_id:141445)模拟，我们处理的许多数据都具有空间连续性。简单地对离散样本点进行插值往往忽略了数据点之间固有的[空间相关性](@entry_id:203497)，也无法对预测的不确定性进行量化。地统计学，特别是其核心工具——[变异函数分析](@entry_id:186743)与[克里金法](@entry_id:751060)，为解决这一根本问题提供了严谨的统计框架。它不仅是一种插值技术，更是一种理解和建模[空间变异性](@entry_id:755146)的[科学方法](@entry_id:143231)。

本文旨在为读者提供一个关于地统计[克里金法](@entry_id:751060)与[变异函数分析](@entry_id:186743)的全面而深入的指南。我们将从基本原理出发，逐步深入到高级应用和前沿课题。在“原理与机制”一章中，您将学习到支撑[地质统计学](@entry_id:749879)的[平稳性假设](@entry_id:272270)，理解半变异函数的定义、数学性质及其关键参数（块金、基台、变程）的物理意义，并熟悉各类理论模型。接着，在“应用与跨学科连接”一章中，我们将展示这些理论如何在处理非高斯数据、融合[多源](@entry_id:170321)信息、建模复杂[时空结构](@entry_id:158931)以及应对大数据挑战等真实世界问题中发挥作用。最后，“动手实践”部分将通过一系列精心设计的问题，引导您思考和解决在实际分析中可能遇到的关键计算与统计挑战，从而巩固所学知识。

## 原理与机制

### [平稳性假设](@entry_id:272270)：[地质统计学](@entry_id:749879)的基础

为了对空间分布的地球物理属性进行统计推断，我们通常将其表示为一个[随机场](@entry_id:177952)或随机函数 $Z(\mathbf{x})$，其中 $\mathbf{x}$ 是 $d$ 维空间 $\mathbb{R}^d$ 中的一个位置向量。然而，如果没有任何关于该随机场统计特性的假设，我们几乎无法从有限的观测数据中推断出任何有用的信息。因此，[地质统计学](@entry_id:749879)的核心是建立在**平稳性 (stationarity)** 假设之上的。[平稳性假设](@entry_id:272270)限制了随机场的统计行为在空间中的变化方式，从而使得利用部分样本来推断整体成为可能。

最严格的[平稳性假设](@entry_id:272270)是**二阶平稳性 (second-order stationarity)**，也称为[弱平稳性](@entry_id:171204)。一个[随机场](@entry_id:177952) $Z(\mathbf{x})$ 被认为是二阶平稳的，如果它满足以下两个条件：
1.  期望（均值）在整个研究区域内为常数：$E[Z(\mathbf{x})] = \mu$。
2.  任意两点 $Z(\mathbf{x})$ 和 $Z(\mathbf{x}+\mathbf{h})$ 之间的协[方差](@entry_id:200758)仅依赖于它们的空间分离向量（滞后向量）$\mathbf{h}$，而与具体位置 $\mathbf{x}$ 无关：$\mathrm{Cov}(Z(\mathbf{x}), Z(\mathbf{x}+\mathbf{h})) = C(\mathbf{h})$。

[协方差函数](@entry_id:265031) $C(\mathbf{h})$ 描述了[空间变异性](@entry_id:755146)的结构。当 $\mathbf{h}=\mathbf{0}$ 时，$C(\mathbf{0}) = \mathrm{Var}[Z(\mathbf{x})] = \sigma^2$，即场的[方差](@entry_id:200758)，它在二阶平稳假设下也是一个常数。一个函数要成为一个有效的[协方差函数](@entry_id:265031)，它必须是**正定 (positive definite)** 的，这意味着对于任意一组位置和系数，[线性组合](@entry_id:154743)的[方差](@entry_id:200758)必须是非负的。

然而，在许多地球物理应用中，二阶[平稳性假设](@entry_id:272270)过于严苛。例如，某些属性（如地形高程）可能不具有有限的全局[方差](@entry_id:200758)，或者可能存在缓慢变化的趋势。为了处理这些情况，[地质统计学](@entry_id:749879)引入了一个更弱、更具普适性的假设：**内蕴[平稳性假设](@entry_id:272270) (intrinsic stationarity hypothesis)**。一个随机场满足内蕴假设，如果它满足以下两个条件：
1.  任意增量 $Z(\mathbf{x}+\mathbf{h}) - Z(\mathbf{x})$ 的期望为零：$E[Z(\mathbf{x}+\mathbf{h}) - Z(\mathbf{x})] = 0$。如果 $Z(\mathbf{x})$ 的期望存在，这暗含了期望为常数。
2.  增量的[方差](@entry_id:200758)仅依赖于滞后向量 $\mathbf{h}$，而与位置 $\mathbf{x}$ 无关。

这个关于增量[方差](@entry_id:200758)的函数，正是我们定义**半变异函数 (semivariogram)** $\gamma(\mathbf{h})$ 的基础。

### 半变异函数：定义与数学性质

对于一个满足内蕴假设的[随机场](@entry_id:177952) $Z(\mathbf{x})$，其半变异函数定义为增量[方差](@entry_id:200758)的一半：
$$
\gamma(\mathbf{h}) = \frac{1}{2} \mathrm{Var}[Z(\mathbf{x}+\mathbf{h}) - Z(\mathbf{x})]
$$
由于增量的期望为零，这也可以写作：
$$
\gamma(\mathbf{h}) = \frac{1}{2} E\left[ (Z(\mathbf{x}+\mathbf{h}) - Z(\mathbf{x}))^2 \right]
$$
函数 $2\gamma(\mathbf{h})$ 通常被称为**变异函数 (variogram)**。根据内蕴假设，$\gamma(\mathbf{h})$ 不依赖于位置 $\mathbf{x}$，仅是滞后向量 $\mathbf{h}$ 的函数。

半变异函数的概念比[协方差函数](@entry_id:265031)更为宽泛。如果一个场是二阶平稳的，我们可以推导出其半变异函数与[协方差函数](@entry_id:265031)之间的关系：
$$
\begin{align*}
\gamma(\mathbf{h})  = \frac{1}{2} \mathrm{Var}[Z(\mathbf{x}+\mathbf{h}) - Z(\mathbf{x})] \\
 = \frac{1}{2} \left( E[Z(\mathbf{x}+\mathbf{h})^2] - 2E[Z(\mathbf{x}+\mathbf{h})Z(\mathbf{x})] + E[Z(\mathbf{x})^2] \right) \\
 = \frac{1}{2} \left( (\mathrm{Var}[Z(\mathbf{x}+\mathbf{h})] + \mu^2) - 2(\mathrm{Cov}(Z(\mathbf{x}), Z(\mathbf{x}+\mathbf{h})) + \mu^2) + (\mathrm{Var}[Z(\mathbf{x})] + \mu^2) \right) \\
 = \frac{1}{2} \left( C(\mathbf{0}) - 2C(\mathbf{h}) + C(\mathbf{0}) \right) \\
 = C(\mathbf{0}) - C(\mathbf{h})
\end{align*}
$$
这个重要的关系式 $\gamma(\mathbf{h}) = C(\mathbf{0}) - C(\mathbf{h})$ 表明，任何二阶[平稳过程](@entry_id:196130)必然也满足内蕴假设。然而，反之不成立。存在一些随机场，它们的半变异函数 $\gamma(\mathbf{h})$ 是良定义的，但其[方差](@entry_id:200758) $C(\mathbf{0})$ 是无限的，因此[协方差函数](@entry_id:265031) $C(\mathbf{h})$ 无法定义。例如，具有线性半变异函数 $\gamma(\mathbf{h}) = c\|\mathbf{h}\|$ 的[随机场](@entry_id:177952)就是如此。这类模型在半变异函数的框架下是有效的，但在[协方差函数](@entry_id:265031)的框架下则不然。这凸显了半变异函数在[地质统计学](@entry_id:749879)中的核心地位和更强的适用性。 

并非任何函数都可以作为有效的半变异函数模型。一个函数 $\gamma: \mathbb{R}^d \to [0, \infty)$ 要成为一个有效的半变异函数，它必须满足一组严格的数学条件，以确保由它定义的克里金（Kriging）[方差](@entry_id:200758)不会出现负值。这些必要且充分的条件是：
1.  $\gamma(\mathbf{0}) = 0$
2.  $\gamma(\mathbf{h}) = \gamma(-\mathbf{h})$ （[偶函数](@entry_id:163605)）
3.  $\gamma$ 是**条件负定 (conditionally negative definite)** 的。这意味着对于任意有限的位置集合 $\{\mathbf{x}_i\}_{i=1}^n$ 和满足 $\sum_{i=1}^n a_i = 0$ 的任意实系数 $\{a_i\}_{i=1}^n$，必须满足以下不等式：
    $$
    \sum_{i=1}^n \sum_{j=1}^n a_i a_j \gamma(\mathbf{x}_i - \mathbf{x}_j) \le 0
    $$
这个条件源于一个基本事实：任何满足 $\sum a_i = 0$ 的线性组合 $\sum a_i Z(\mathbf{x}_i)$（称为一个“允许的[线性组合](@entry_id:154743)”）的[方差](@entry_id:200758)必须是非负的，而这个[方差](@entry_id:200758)可以表示为 $-\sum \sum a_i a_j \gamma(\mathbf{x}_i - \mathbf{x}_j)$。

一个由 Schoenberg 提出的等价表述提供了另一种理解和验证半变异函数有效性的途径。一个满足 $\gamma(\mathbf{0})=0$ 和 $\gamma(\mathbf{h})=\gamma(-\mathbf{h})$ 的函数 $\gamma$ 是条件负定的，当且仅当对于所有 $t > 0$，函数 $\exp(-t \gamma(\mathbf{h}))$ 是一个正定函数（即一个有效的[协方差函数](@entry_id:265031)）。这个深刻的定理将半变异函数的有效性与[协方差函数](@entry_id:265031)的有效性联系起来。 

### 解读半变异函数：基台、变程与块金效应

在实践中，我们通常从观测数据中估计出**实验半变异函数 (experimental semivariogram)**，然后选择一个理论模型来拟合它。一个典型的有界半变异函数模型通常由三个关键参数来描述，它们各自具有明确的[地球物理学](@entry_id:147342)意义。

为了更好地理解这些参数，我们可以设想一个观测到的属性值 $Z(\mathbf{x})$ 是由三个独立的[随机过程](@entry_id:159502)叠加而成：$Z(\mathbf{x}) = S(\mathbf{x}) + U(\mathbf{x}) + \epsilon(\mathbf{x})$。其中：
- $S(\mathbf{x})$ 是一个空间连续且相关的结构化过程。
- $U(\mathbf{x})$ 是一个在采样尺度之下变化的微观尺度过程，它在不同的采样点之间不相关。
- $\epsilon(\mathbf{x})$ 是测量仪器引入的随机测量误差，它在不同的测量中也是不相关的。

基于此模型，总的半变异函数是各分量半变异函数之和：$\gamma_Z(h) = \gamma_S(h) + \gamma_U(h) + \gamma_{\epsilon}(h)$。

1.  **块金效应 (Nugget Effect, $c_0$)**
    实验半变异函数图在原点处往往表现出一个跳跃，即 $\lim_{h \to 0^+} \gamma(h) = c_0 > 0$，而根据定义 $\gamma(0)=0$。这个跳跃 $c_0$ 就是块金效应。它代表了在比最小采样间距更小的尺度上存在的变异性。根据我们的分解模型，当滞后距离 $h$ 趋近于零时，结构化部分 $S(\mathbf{x})$ 是连续的，因此 $\gamma_S(h) \to 0$。然而，微观尺度过程 $U(\mathbf{x})$ 和[测量误差](@entry_id:270998) $\epsilon(\mathbf{x})$ 在任意小的分离距离上都是不相关的。对于任意 $h > 0$，它们的半变异函数达到一个常数值，分别为它们各自的[方差](@entry_id:200758) $\sigma_U^2$ 和 $\sigma_\epsilon^2$。因此，块金效应是这两部分[方差](@entry_id:200758)的总和：$c_0 = \sigma_U^2 + \sigma_\epsilon^2$。这清楚地表明，**块金效应既包含了[测量误差](@entry_id:270998)，也包含了采样尺度以下的真实空间微观变异性**。通过在同一物理样本上进行重复测量，可以估计出[测量误差](@entry_id:270998)[方差](@entry_id:200758) $\sigma_\epsilon^2$，从而将块金效应分解为其两个组成部分。

2.  **基台 (Sill, $c_0+c$)**
    随着滞后距离 $h$ 的增加，半变异函数值通常会趋于一个平稳的平台，这个平台的高度被称为基台。对于二阶[平稳过程](@entry_id:196130)，基台值等于场的总[方差](@entry_id:200758) $\mathrm{Var}[Z(\mathbf{x})]$。在我们的分解模型中，当 $h$ 变得足够大时，结构化分量 $S(\mathbf{x})$ 在相距遥远的两点之间也变得不相关，此时 $\gamma_S(h)$ 趋近于其自身的[方差](@entry_id:200758) $\sigma_S^2$。因此，总的基台为 $c_0 + c = (\sigma_U^2 + \sigma_\epsilon^2) + \sigma_S^2 = \mathrm{Var}[Z(\mathbf{x})]$。其中，$c = \sigma_S^2$ 被称为**偏基台 (partial sill)**，代表了场中空间结构化部分的[方差](@entry_id:200758)。

3.  **变程 (Range, $a$)**
    变程是半变异函数达到基台时的滞后距离。它标志着[空间自相关](@entry_id:177050)性的[影响范围](@entry_id:166501)：相距大于变程的两个样本点可以被认为在统计上是独立的。这个参数对于[克里金插值](@entry_id:751060)至关重要，因为它定义了用于估计一个未知点值的“邻域”大小。对于某些模型（如指数模型），半变异函数是渐近达到基台的，因此我们定义一个**有效变程 (effective range)** 或**实用变程 (practical range)**，例如，当半变异函数值达到基台值的95%时的距离。

### 常用的允许半变异函数模型

为了在[克里金插值](@entry_id:751060)中使用，我们需要将实验半变异函数拟合到一个数学上有效的理论模型。以下是一些最常用的各向同性（isotropic，即变异函数仅依赖于距离 $h=\|\mathbf{h}\|$ 而非方向）模型。所有模型都包含块金效应 $c_0$、偏基台 $c$ 和距离参数 $a$。为了简洁，以下公式定义了 $h>0$ 时的模型形式，并隐含 $\gamma(0)=0$。

-   **球状模型 (Spherical Model)**：这是一个具有有限变程的模型。
    $$
    \gamma(h) =
    \begin{cases}
    c_0 + c \left( \frac{3h}{2a} - \frac{h^3}{2a^3} \right),  0 \lt h \le a \\
    c_0 + c,  h > a
    \end{cases}
    $$
    其真实变程就是参数 $a$。该模型在原点附近是线性的，表明场是[连续但不可微](@entry_id:261860)的。

-   **指数模型 (Exponential Model)**：该模型渐近地达到基台。
    $$
    \gamma(h) = c_0 + c \left[ 1 - \exp\left(-\frac{h}{a}\right) \right]
    $$
    其有效变程通常定义为 $3a$，此时 $\gamma(h)$ 达到基台的约95%。指数模型在原点处也是线性的，其对应的随机场也是[连续但不可微](@entry_id:261860)的。

-   **高斯模型 (Gaussian Model)**：该模型也渐近地达到基台，但在原点附近具有抛物线形状。
    $$
    \gamma(h) = c_0 + c \left[ 1 - \exp\left(-\left(\frac{h}{a}\right)^2\right) \right]
    $$
    其有效变程通常取为 $\sqrt{3}a$。原点处的平滑行为表明，其对应的随机场是均方意义下无限可微的，即非常光滑。高斯模型在任何维度 $d$ 上都是一个有效的模型。其有效性可以通过 Schoenberg 定理来证明：函数 $\varphi(s) = \exp(-s/\alpha^2)$ 是一个**完全单调函数 (completely monotone function)**，这保证了 $C(\mathbf{h})=\varphi(\|\mathbf{h}\|^2)$ 在所有维度上都是正定的。

-   **Matérn 模型族 (Matérn Family)**：这是一个非常灵活的通用模型族，由两个参数控制：距离参数 $a$ 和光滑度参数 $\nu > 0$。
    $$
    \gamma(h) = c_0 + c \left[ 1 - \frac{1}{2^{\nu-1}\Gamma(\nu)} \left(\frac{h}{a}\right)^{\nu} K_{\nu}\left(\frac{h}{a}\right) \right]
    $$
    其中 $\Gamma(\nu)$ 是伽玛函数，$K_{\nu}$ 是[第二类修正贝塞尔函数](@entry_id:201421)。Matérn 模型族的强大之处在于，光滑度参数 $\nu$ 直接控制了[随机场](@entry_id:177952)的**均方可微性 (mean-square differentiability)**。一个具有 Matérn 协[方差](@entry_id:200758)的随机场是 $m$ 次均方可微的，当且仅当 $\nu > m$。这与场的[光谱](@entry_id:185632)密度 $S(\boldsymbol{\omega})$ 在高频区的衰减行为直接相关，$S(\boldsymbol{\omega}) \asymp \|\boldsymbol{\omega}\|^{-2\nu - d}$，$\nu$ 越大，高频分量衰减越快，场就越光滑。特别地，当 $\nu = 0.5$ 时，Matérn 模型退化为指数模型；当 $\nu \to \infty$ 时，它趋近于高斯模型。这使得 Matérn 模型能够描述从非常粗糙到非常光滑的各种空间现象。

所有这些模型的参数必须满足约束条件 $c_0 \ge 0$, $c \ge 0$, $a > 0$ (以及 Matérn 模型中的 $\nu > 0$) 才能保证其为有效的半变异函数。

### 高级变异函数建模技术

#### 嵌套结构 (Nested Structures)

许多地球物理现象在不同尺度上表现出变异性。例如，一个油藏的渗透率可能同时受到微观孔隙结构（短程变异）、岩相单元[分布](@entry_id:182848)（中程变异）和区域构造（长程变异）的控制。这种多尺度变异性可以通过**嵌套结构模型**来描述。

一个[嵌套模型](@entry_id:635829)是多个（比如两个）允许的半变异函数模型的[线性组合](@entry_id:154743)：
$$
\gamma(h) = \gamma_1(h) + \gamma_2(h)
$$
其中 $\gamma_1(h)$ 和 $\gamma_2(h)$ 分别代表不同尺度的空间结构，具有各自的偏基台 $c_1, c_2$ 和变程 $a_1, a_2$。由于允许的半变异函数模型构成的集合在加法和正标量乘法下是封闭的，因此[嵌套模型](@entry_id:635829)本身也是一个有效的半变异函数模型。

对于这样的模型，总基台是各个分量基台之和：$C_{total} = c_1 + c_2$ (假设无块金效应)。短程结构 ($\gamma_1$，具有较小的 $a_1$) 描述了场在短距离内的快速变化，对半变异函数在原点附近的陡峭程度贡献最大，控制着高频变异性。长程结构 ($\gamma_2$，具有较大的 $a_2$) 则描述了场在大范围内的缓慢变化，维持了远距离样本之间的[空间相关性](@entry_id:203497)，控制着低频变异性。模型的表观实用变程 $h^*$ 是一个综合效应，需要通过求解 $\gamma(h^*) = 0.95 \times C_{total}$ 来确定，它通常介于 $a_1$ 和 $a_2$ 之间，其具体数值取决于 $c_1, c_2, a_1, a_2$ 的相对大小。

#### 各向异性 (Anisotropy)

前面的模型都假设了各向同性，即[空间相关性](@entry_id:203497)与方向无关。然而，许多地质过程具有方向性。例如，沉积岩的渗透率在平行于层面方向上的相关性通常大于垂直方向。这种方向依赖的变异性被称为**各向异性 (anisotropy)**。

最常见的各向异性类型是**几何各向异性 (geometric anisotropy)**。在这种情况下，半变异函数的等值线是椭球形，但在不同方向上具有相同的基台值。它可以通过对一个各向同性[基模](@entry_id:165201)型 $\tilde{\gamma}(r)$ 进行[坐标变换](@entry_id:172727)来构建：
$$
\gamma(\mathbf{h}) = \tilde{\gamma}(\|\mathbf{A}\mathbf{h}\|)
$$
其中 $\mathbf{A}$ 是一个对称正定矩阵。这个变换相当于在一个“拉伸”或“压缩”过的[坐标系](@entry_id:156346)中计算距离。

在二维空间中，矩阵 $\mathbf{A}$ 完全定义了各向异性的特征。通过对 $\mathbf{A}$ 进行[特征分解](@entry_id:181333) $\mathbf{A} = \mathbf{Q}\boldsymbol{\Lambda}\mathbf{Q}^\top$ (其中 $\mathbf{Q}$ 是[正交矩阵](@entry_id:169220)，$\boldsymbol{\Lambda} = \mathrm{diag}(\lambda_1, \lambda_2)$ 是正[特征值](@entry_id:154894)组成的[对角矩阵](@entry_id:637782))，我们可以提取出各向异性的几何参数。假定 $\lambda_{\max} \ge \lambda_{\min} > 0$。

-   **[主轴](@entry_id:172691)方向 (Orientation)**：各向异性的[主轴](@entry_id:172691)方向由 $\mathbf{A}$ 的[特征向量](@entry_id:151813)（即 $\mathbf{Q}$ 的列向量）给出。
-   **变程 (Ranges)**：定向变程 $R_{dir}(\mathbf{u})$ 与 $\|\mathbf{A}\mathbf{u}\|$ 成反比。这意味着，**最大变程 ([主方向](@entry_id:276187))** 出现在使 $\|\mathbf{A}\mathbf{u}\|$ 最小的方向上，即与**[最小特征值](@entry_id:177333) $\lambda_{\min}$** 对应的[特征向量](@entry_id:151813)方向上。同理，最小变程（次要方向）与最大[特征值](@entry_id:154894) $\lambda_{\max}$ 对应的[特征向量](@entry_id:151813)方向对齐。
-   **各向异[性比](@entry_id:172643) (Anisotropy Ratio)**：定义为最大变程与最小变程之比，它等于**最大[特征值](@entry_id:154894)与最小特征值之比**：$\frac{R_{\max}}{R_{\min}} = \frac{\lambda_{\max}}{\lambda_{\min}}$。

因此，通过分析变换矩阵 $\mathbf{A}$ 的谱特性，我们可以完全量化几何各向异性的方向和强度。

### 从理论到实践：实验半变异函数的估计

理论模型必须基于从实际数据中获得的变异性信息。这个过程的第一步是计算**实验半变异函数**。最常用的估计方法是 Matheron 提出的**[矩估计法](@entry_id:270941) (method-of-moments estimator)**。对于一个给定的滞后向量 $\mathbf{h}$，其估计值 $\hat{\gamma}(\mathbf{h})$ 计算如下：
$$
\hat{\gamma}(\mathbf{h}) = \frac{1}{2|N(\mathbf{h})|} \sum_{(i,j) \in N(\mathbf{h})} [Z(\mathbf{x}_i) - Z(\mathbf{x}_j)]^2
$$
其中 $N(\mathbf{h})$ 是所有满足 $\mathbf{x}_i - \mathbf{x}_j \approx \mathbf{h}$ 的样本对 $(i,j)$ 的集合， $|N(\mathbf{h})|$ 是该集合中的样本对数量。

在实践中，由于数据点通常是不规则[分布](@entry_id:182848)的，几乎不可能找到大量具有完全相同的滞后向量 $\mathbf{h}$ 的样本对。因此，我们必须进行**分组 (binning)**，即将滞后向量落在某个“容差”范围内的所有样本对归为一组。对于各向同性分析，我们定义一系列滞后距离的区间（例如，$h \pm \delta h$）。对于各向异性分析，我们还需定义方向容差（例如，[方位角](@entry_id:164011) $\pm \delta \theta$）和带宽限制。

分组参数的选择体现了经典的**[偏差-方差权衡](@entry_id:138822) (bias-variance trade-off)**。选择较宽的容差（即较大的 $\delta h$ 或 $\delta \theta$）会使得每个组内的样本对数量 $|N(\mathbf{h})|$ 增加，从而降低估计值 $\hat{\gamma}(\mathbf{h})$ 的采样[方差](@entry_id:200758)，使其更稳定。然而，如果真实的 $\gamma(\mathbf{h})$ 函数在该组内变化剧烈，那么 $\hat{\gamma}(\mathbf{h})$ 将是对该组内所有真实 $\gamma$ 值的平均，这会导致对中心点 $\gamma(\mathbf{h})$ 的估计产生偏差。反之，选择较窄的容差会减小偏差，但可能因样本对数量过少而导致估计值极不稳定。

### 超越平稳性：处理趋势与普适克里金

内蕴[平稳性假设](@entry_id:272270)虽然比二阶平稳性更弱，但它仍然要求场的期望为常数。当数据中存在明显的空间趋势（drift），例如一个线性或二次的缓变背景时，内蕴假设不再成立。在这种情况下，直接计算的实验半变异函数将无法收敛到一个基台，而是会随着滞后距离的增加而持续增长（表现为“漂移”），这会严重误导对底层变异结构的认知。

为了在存在趋势的情况下进行地质统计分析，Matheron 发展了**$k$阶内蕴随机函数 (Intrinsic Random Function of order k, IRF-k)** 的理论。其核心思想是，虽然[随机场](@entry_id:177952) $Z(\mathbf{x})$本身不是平稳的，但其经过某种高阶差分运算后得到的场是平稳的。

在 IRF-k 框架下，[随机场](@entry_id:177952) $Z(\mathbf{x})$ 的期望被建模为一个 $k-1$ 次多项式：
$$
E[Z(\mathbf{x})] = M(\mathbf{x}) = \sum_{j=1}^p \beta_j f_j(\mathbf{x})
$$
其中 $\{f_j(\mathbf{x})\}$ 是 $k-1$ 次[多项式的基](@entry_id:148579)函数，$\{\beta_j\}$ 是未知的趋势系数。此时，我们不再对所有增量要求平稳性，而是只对那些能够“滤除”或“消除”多项式趋势的**允许的线性组合 (allowable linear combinations)** $\sum a_i Z(\mathbf{x}_i)$ 要求其具有平稳的[方差](@entry_id:200758)。一个[线性组合](@entry_id:154743)是允许的，当且仅当它作用于任意 $k-1$ 次多项式时结果均为零，即 $\sum a_i f_j(\mathbf{x}_i) = 0$ 对所有 $j$ 成立。

对于这类允许的组合，其[方差](@entry_id:200758)可以用一个**广义[协方差函数](@entry_id:265031) (generalized covariance function, GCF)** $G(\mathbf{h})$ 来表示：
$$
\mathrm{Var}\left(\sum_{i=1}^n a_i Z(\mathbf{x}_i)\right) = \sum_{i=1}^n \sum_{j=1}^n a_i a_j G(\mathbf{x}_i - \mathbf{x}_j)
$$
函数 $G(\mathbf{h})$ 替代了传统协[方差](@entry_id:200758)或半变异函数的角色，它需要满足**$k$阶条件正定性**，以确保[方差](@entry_id:200758)的非负性。

这个理论框架是**普适克里金 (Universal Kriging, UK)** 的基石。UK 旨在提供一个线性无偏最优估计，其中“无偏”意味着估计器必须能够精确地重现趋势部分。对于估计点 $\mathbf{x}_0$ 的估计值 $\hat{Z}(\mathbf{x}_0) = \sum \lambda_i Z(\mathbf{s}_i)$，其无偏性约束条件为：
$$
\sum_{i=1}^n \lambda_i f_j(\mathbf{s}_i) = f_j(\mathbf{x}_0), \quad \text{for } j = 1, \dots, p
$$
UK 的目标就是在满足这些约束的条件下，最小化[估计误差](@entry_id:263890)[方差](@entry_id:200758) $\mathrm{Var}[\hat{Z}(\mathbf{x}_0) - Z(\mathbf{x}_0)]$。这个最小化问题可以用广义[协方差函数](@entry_id:265031) $G(\mathbf{h})$ (或与其等价的 IRF-k 变异函数) 来构建和求解。

一个重要的特例是，当 $k=1$ 时，趋势是一个0次多项式，即一个未知的常数均值 $M(\mathbf{x}) = \mu$。此时，唯一的[基函数](@entry_id:170178)是 $f_1(\mathbf{x}) = 1$，无偏性约束简化为 $\sum \lambda_i = 1$。这正是**普通克里金 (Ordinary Kriging, OK)** 的约束条件。因此，OK可以被视为UK在处理未知常数均值趋势下的一个特例。