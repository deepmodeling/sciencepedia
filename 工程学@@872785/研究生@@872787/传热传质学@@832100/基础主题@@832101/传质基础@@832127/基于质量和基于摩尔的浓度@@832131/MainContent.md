## 引言
在涉及[化学反应](@entry_id:146973)、[相变](@entry_id:147324)或组分混合的传热[传质](@entry_id:151908)问题中，准确描述混合物中各组分的浓度是进行定量分析的基石。物质的量可以通过质量或摩尔来度量，这自然地引出了两种基本而重要的浓度表示框架：基于质量的体系和基于摩尔的体系。然而，这两种框架的选择并非随意，错误或不恰当的选择可能导致模型变得异常复杂，甚至在概念上产生误解。本文旨在系统地解决这一核心问题，阐明两种浓度基准的内在联系与本质区别，[并指](@entry_id:276731)导读者在面对具体科学与工程问题时做出最优选择。

在接下来的内容中，读者将首先通过“原理与机制”一章，深入学习质量与[摩尔浓度](@entry_id:139283)的基本定义、它们之间的精确换算公式，以及如何基于不同的参考速度构建自洽的[组分守恒方程](@entry_id:151288)。随后，在“应用与跨学科联系”一章中，我们将通过一系列横跨环境科学、生物化学、[材料科学](@entry_id:152226)到[燃烧理论](@entry_id:141685)的真实案例，展示在不同场景下选择特定浓度基准的实际优势与深刻原因。最后，“动手实践”部分将提供具体的计算问题，帮助读者将理论知识转化为解决实际问题的能力。本文将引导您建立一个关于多组分[输运现象](@entry_id:147655)的清晰而完整的概念图景，从最基本的浓度定义出发，直至前沿的建模应用。

## 原理与机制

在多组分系统的传热传质分析中，准确描述混合物中各组分的浓度是首要任务。由于质量和摩尔是描述物质的两种[基本量纲](@entry_id:273221)，因此发展出了分别基于质量和摩尔的两种浓度表示方法。本章旨在深入探讨这些浓度表示法的基本原理、它们之间的相互关系，以及在建立输运方程和分析化学反应系统时，选择不同基准的理论考量与实际影响。

### 浓度的基本定义与换算

描述多组分混合物组成的出发点是定义各组分 $i$ 的局部浓度。最基本的两种浓度是 **质量浓度** (mass concentration) 和 **摩尔浓度** (molar concentration)。

质量浓度，或称偏密度 (partial density)，$\rho_i$，定义为单位体积内组分 $i$ 的质量。在由 $N$ 个组分构成的混合物中，总密度 $\rho$ 是所有组分质量浓度之和：
$$ \rho = \sum_{i=1}^{N} \rho_i $$

摩尔浓度 $c_i$ 定义为单位体积内组分 $i$ 的摩尔数。同样，总摩尔浓度 $c$ 是所有组分摩尔浓度之和：
$$ c = \sum_{i=1}^{N} c_i $$

质量浓度和[摩尔浓度](@entry_id:139283)通过组分 $i$ 的[摩尔质量](@entry_id:146110) $W_i$ (在一些文献中也用 $M_i$ 表示) 联系起来：
$$ \rho_i = W_i c_i $$

虽然质量浓度和[摩尔浓度](@entry_id:139283)是基本量，但在[输运理论](@entry_id:143989)中，更常用的是它们的无量纲形式：**质量分数** (mass fraction) $Y_i$ 和 **摩尔分数** (mole fraction) $X_i$。

质量分数 $Y_i$ 定义为组分 $i$ 的质量浓度与总密度的比值：
$$ Y_i = \frac{\rho_i}{\rho} $$

[摩尔分数](@entry_id:145460) $X_i$ 定义为组分 $i$ 的摩尔浓度与总[摩尔浓度](@entry_id:139283)的比值：
$$ X_i = \frac{c_i}{c} $$

根据定义，所有组分的质量分数之和与[摩尔分数](@entry_id:145460)之和恒为 1：
$$ \sum_{i=1}^{N} Y_i = 1 \quad \text{and} \quad \sum_{i=1}^{N} X_i = 1 $$

#### 质量基准与摩尔基准的转换

在质量基准和摩尔基准之间进行转换，关键在于建立总密度 $\rho$ 和总[摩尔浓度](@entry_id:139283) $c$ 之间的联系。我们定义 **混合物平均[摩尔质量](@entry_id:146110)** (mixture-averaged molecular weight) $\bar{W}$ 为总密度与总摩尔浓度之比 [@problem_id:2504209]：
$$ \bar{W} = \frac{\rho}{c} $$

这个量是连接两个体系的桥梁。我们可以推导出 $\bar{W}$ 与各组分摩尔分数和[摩尔质量](@entry_id:146110)的关系。将 $\rho = \sum \rho_i = \sum W_i c_i$ 代入上式：
$$ \bar{W} = \frac{\sum_{i=1}^{N} W_i c_i}{c} = \sum_{i=1}^{N} W_i \left(\frac{c_i}{c}\right) = \sum_{i=1}^{N} W_i X_i $$
这表明，混合物的平均摩尔质量是各组分摩尔质量以[摩尔分数](@entry_id:145460)为权重的加权平均值。

有了 $\bar{W}$ 的表达式，我们就能轻易地在质量分数和[摩尔分数](@entry_id:145460)之间进行转换。考虑 $Y_i$ 的定义：
$$ Y_i = \frac{\rho_i}{\rho} = \frac{W_i c_i}{\bar{W} c} = \frac{W_i}{\bar{W}} \left(\frac{c_i}{c}\right) = X_i \frac{W_i}{\bar{W}} $$
这个关系式是精确的，并且至关重要。它表明，除非某组分的摩尔质量恰好等于混合物的平均[摩尔质量](@entry_id:146110) ($W_i = \bar{W}$)，否则其质量分数和摩尔分数通常是不同的。

通过这个关系，我们还可以推导出 $\bar{W}$ 的另一种表达形式。对上式变形得到 $X_i = Y_i \frac{\bar{W}}{W_i}$，并代入 $\sum X_i = 1$：
$$ \sum_{i=1}^{N} Y_i \frac{\bar{W}}{W_i} = 1 $$
整理后可得：
$$ \bar{W} = \left(\sum_{i=1}^{N} \frac{Y_i}{W_i}\right)^{-1} $$
这个表达式说明，平均[摩尔质量](@entry_id:146110)的倒数是各组分[摩尔质量](@entry_id:146110)倒数以[质量分数](@entry_id:161575)为权重的加权平均值。这两个 $\bar{W}$ 的表达式在数学上是等价的，并共同展现了浓度定义体系的内在[自洽性](@entry_id:160889) [@problem_id:2504209]。

#### 特殊体系中的浓度表示

对于特定类型的混合物，浓度还可以用其他方式表示，并且它们之间的转换关系可以被精确推导。

**[理想气体混合物](@entry_id:149212)**：对于[理想气体混合物](@entry_id:149212)，浓度可以直接与[热力学状态变量](@entry_id:151686)——压力 $p$ 和温度 $T$——联系起来。根据[道尔顿分压定律](@entry_id:140483)，组分 $i$ 的分压 $p_i$ 为 $p_i = X_i p$。对组分 $i$ 应用[理想气体状态方程](@entry_id:137803) $p_i V = n_i R_u T$（其中 $R_u$ 是[普适气体常数](@entry_id:136843)），我们可以得到[摩尔浓度](@entry_id:139283) $c_i = n_i/V$ 的表达式 [@problem_id:2504257]：
$$ c_i = \frac{p_i}{R_u T} = \frac{p X_i}{R_u T} $$
相应地，质量浓度 $\rho_i$ 为：
$$ \rho_i = c_i W_i = \frac{p X_i W_i}{R_u T} $$
这些关系在分析气体燃烧、[大气化学](@entry_id:198364)和气相沉积等过程中极为有用。

**液体溶液**：在液相中，特别是在[水溶液化学](@entry_id:275766)和电化学中，**[摩尔浓度](@entry_id:139283)** ($c_i$，molarity，单位 $\mathrm{mol}\cdot\mathrm{m}^{-3}$) 和 **质量摩尔浓度** ($m_i$，molality，单位 $\mathrm{mol}\cdot\mathrm{kg}^{-1}$) 也被广泛使用。[摩尔浓度](@entry_id:139283)定义为每单位**溶液**体积的溶质摩尔数，而质量摩尔浓度定义为每单位**溶剂**质量的溶质摩尔数。这种定义上的细微差别导致它们之间的转换并非平凡，通常需要知道溶液的总密度 $\rho$。

例如，考虑一个由溶质1和溶剂2组成的二元溶液。我们可以严格地从定义出发，推导[摩尔浓度](@entry_id:139283) $c_1$ 和质量摩尔浓度 $m_1$ 之间的精确关系。通过引入[质量分数](@entry_id:161575) $Y_1$ 作为中间变量，可以分别建立 $c_1$ 与 $Y_1$ 以及 $m_1$ 与 $Y_1$ 的关系，然后消去 $Y_1$，最终得到 [@problem_id:2504266]：
$$ c_1 = \frac{m_1 \rho}{1 + m_1 W_1} $$
这个关系式在任何浓度下都精确成立，它清楚地表明了溶液密度 $\rho$ 在不同浓度[单位转换](@entry_id:136593)中的关键作用。与质量摩尔浓度不同，[摩尔浓度](@entry_id:139283)会随温度变化（因为密度 $\rho$ 是温度的函数），这是在进行非[等温过程](@entry_id:143096)分析时需要注意的一点。

### [平均速度](@entry_id:267649)与[扩散通量](@entry_id:748422)

在多组分流动中，不同组分可能以不同的速度 $\boldsymbol{v}_i$ 运动。这种[相对运动](@entry_id:169798)的现象就是[扩散](@entry_id:141445)。为了描述混合物的整体运动（即[对流](@entry_id:141806)），我们需要定义一个混合物平均速度。然而，如何“平均”是一个关键问题，不同的平均方式会产生不同的参考速度，从而导致对“[扩散](@entry_id:141445)”的不同定义。

最常用的两种[平均速度](@entry_id:267649)是 **[质量平均速度](@entry_id:149575)** (mass-average velocity) $\boldsymbol{v}$ 和 **摩尔平均速度** (molar-average velocity) $\boldsymbol{v}^*$。

[质量平均速度](@entry_id:149575) $\boldsymbol{v}$ 定义为各组分速度以其质量分数为权重的加权平均值，或者等价地，总质量通量与总密度的比值：
$$ \boldsymbol{v} = \sum_{i=1}^{N} Y_i \boldsymbol{v}_i = \frac{\sum_{i=1}^{N} \rho_i \boldsymbol{v}_i}{\rho} $$
这个速度也被称为 **[质心速度](@entry_id:175479)** (barycentric velocity)，因为它代表了混合物流体微元的[质心运动](@entry_id:178374)速度。

摩尔[平均速度](@entry_id:267649) $\boldsymbol{v}^*$ 定义为各组分速度以其[摩尔分数](@entry_id:145460)为权重的加权平均值，或者等价地，总[摩尔通量](@entry_id:156263)与总摩尔浓度的比值：
$$ \boldsymbol{v}^* = \sum_{i=1}^{N} X_i \boldsymbol{v}_i = \frac{\sum_{i=1}^{N} c_i \boldsymbol{v}_i}{c} $$
这个速度代表了混合物中分子的平均运动速度。

除非所有组分的[摩尔质量](@entry_id:146110)都相等（此时 $Y_i = X_i$），否则[质量平均速度](@entry_id:149575)和摩尔[平均速度](@entry_id:267649)通常不相等。例如，在一个包含两种组分A和B的二元气体混合物中，即使流场很简单，这两种速度也可能指向不同方向或具有不同大小 [@problem_id:2504204]。

#### [扩散通量](@entry_id:748422)

选择不同的[平均速度](@entry_id:267649)作为参考，就定义了不同的[扩散通量](@entry_id:748422)。

相对于[质量平均速度](@entry_id:149575) $\boldsymbol{v}$ 的 **[扩散](@entry_id:141445)质量通量** (diffusive mass flux) $\boldsymbol{j}_i$ 定义为：
$$ \boldsymbol{j}_i = \rho_i (\boldsymbol{v}_i - \boldsymbol{v}) $$
$\boldsymbol{j}_i$ 代表了组分 $i$ 相对于流体[质心运动](@entry_id:178374)的[质量输运](@entry_id:151908)速率。根据[质量平均速度](@entry_id:149575)的定义，可以证明所有组分的[扩散](@entry_id:141445)质量通量之和恒为零：
$$ \sum_{i=1}^{N} \boldsymbol{j}_i = \sum_{i=1}^{N} \rho_i (\boldsymbol{v}_i - \boldsymbol{v}) = \sum \rho_i \boldsymbol{v}_i - \boldsymbol{v} \sum \rho_i = \rho \boldsymbol{v} - \rho \boldsymbol{v} = \boldsymbol{0} $$
这个性质是质量基准体系的一个核心优点。

相对于摩尔平均速度 $\boldsymbol{v}^*$ 的 **[扩散](@entry_id:141445)[摩尔通量](@entry_id:156263)** (diffusive molar flux) $\boldsymbol{J}_i^*$ 定义为：
$$ \boldsymbol{J}_i^* = c_i (\boldsymbol{v}_i - \boldsymbol{v}^*) $$
$\boldsymbol{J}_i^*$ 代表了组分 $i$ 相对于分子平均运动的摩尔输运速率。同样，根据摩尔[平均速度](@entry_id:267649)的定义，所有组分的[扩散](@entry_id:141445)[摩尔通量](@entry_id:156263)之和也恒为零：
$$ \sum_{i=1}^{N} \boldsymbol{J}_i^* = \sum_{i=1}^{N} c_i (\boldsymbol{v}_i - \boldsymbol{v}^*) = \sum c_i \boldsymbol{v}_i - \boldsymbol{v}^* \sum c_i = c \boldsymbol{v}^* - c \boldsymbol{v}^* = \boldsymbol{0} $$

这两种平均速度和相应的[扩散通量](@entry_id:748422)定义了两种描述多组分[输运现象](@entry_id:147655)的自洽框架。选择哪一个框架取决于问题的性质和建模的便利性。一个重要的特例是 **[等摩尔反向扩散](@entry_id:151863)** (equimolar counter-diffusion)，其定义为总[摩尔通量](@entry_id:156263)为零，即 $\boldsymbol{v}^* = \boldsymbol{0}$。在这种情况下，除非组分[摩尔质量](@entry_id:146110)相等，否则[质量平均速度](@entry_id:149575) $\boldsymbol{v}$ 通常不为零 [@problem_id:2504204]。

### [组分守恒方程](@entry_id:151288)

多组分[系统分析](@entry_id:263805)的核心是求解各组分的守恒方程。这些方程本质上是每个组分的质量（或摩尔）平衡式。根据所选的浓度基准，守恒方程有不同的形式。

#### 质量基准的守恒方程

考虑一个可压缩、反应性的多组分混合物。对于组分 $i$ 的质量守恒，其普遍的微分形式可以写作 [@problem_id:2504331]：
$$ \frac{\partial \rho_i}{\partial t} + \nabla \cdot (\rho_i \boldsymbol{v}_i) = \dot{\omega}_i $$
其中，$\rho_i$ 是组分 $i$ 的质量浓度，$\boldsymbol{v}_i$ 是其绝对速度，$\dot{\omega}_i$ 是单位体积内[化学反应](@entry_id:146973)生成的组分 $i$ 的质量速率（即质量源项）。

这个方程虽然普适，但在实际应用中通常会使用混合物[平均速度](@entry_id:267649)和[扩散通量](@entry_id:748422)来重写。将绝对通量 $\rho_i \boldsymbol{v}_i$ 分解为[对流通量](@entry_id:158187)和[扩散通量](@entry_id:748422)。选择[质量平均速度](@entry_id:149575) $\boldsymbol{v}$ 作为参考速度，则 $\rho_i \boldsymbol{v}_i = \rho_i \boldsymbol{v} + \boldsymbol{j}_i$。代入守恒方程并使用质量分数 $Y_i = \rho_i / \rho$（因此 $\rho_i = \rho Y_i$），我们得到以[质量分数](@entry_id:161575)为变量的[组分守恒方程](@entry_id:151288)：
$$ \frac{\partial (\rho Y_i)}{\partial t} + \nabla \cdot (\rho Y_i \boldsymbol{v} + \boldsymbol{j}_i) = \dot{\omega}_i $$
这个方程可以进一步写成如下形式，以便更清晰地辨识各项的物理意义：
$$ \frac{\partial (\rho Y_i)}{\partial t} + \nabla \cdot (\rho Y_i \boldsymbol{v}) = -\nabla \cdot \boldsymbol{j}_i + \dot{\omega}_i $$
- $\frac{\partial (\rho Y_i)}{\partial t}$：非定常项，表示单位体积内组分 $i$ 质量的累积速率。
- $\nabla \cdot (\rho Y_i \boldsymbol{v})$：[对流](@entry_id:141806)项，表示由主体流动（以[质量平均速度](@entry_id:149575) $\boldsymbol{v}$ 描述）引起的组分 $i$ 质量的净流出率。
- $-\nabla \cdot \boldsymbol{j}_i$：[扩散](@entry_id:141445)项，表示由[扩散](@entry_id:141445)（相对于主体流动）引起的组分 $i$ 质量的净流入率。
- $\dot{\omega}_i$：[源项](@entry_id:269111)，表示[化学反应](@entry_id:146973)对组分 $i$ 质量的净生成率。

将此方程对所有组分 $i$ 求和，并利用 $\sum Y_i = 1$，$\sum \boldsymbol{j}_i = \boldsymbol{0}$（[扩散](@entry_id:141445)质量通量的定义）以及 $\sum \dot{\omega}_i = 0$（[化学反应](@entry_id:146973)中的总[质量守恒](@entry_id:204015)），可以直接恢复总质量守恒方程（连续性方程）[@problem_id:2504342]：
$$ \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \boldsymbol{v}) = 0 $$
这一特性是质量基准表述的一个巨大优势，尤其是在[数值模拟](@entry_id:137087)中，它为保证总质量守恒提供了一种自然的方式。

#### 摩尔基准的守恒方程

与质量基准完全类似，我们也可以为[摩尔浓度](@entry_id:139283) $c_i$ 写出守恒方程 [@problem_id:2504261]。组分 $i$ 的摩尔守恒方程的普适形式为：
$$ \frac{\partial c_i}{\partial t} + \nabla \cdot (c_i \boldsymbol{v}_i) = \dot{\nu}_i $$
其中 $\dot{\nu}_i$ 是单位体积内[化学反应](@entry_id:146973)生成的组分 $i$ 的摩尔速率（摩尔源项）。

选择摩尔[平均速度](@entry_id:267649) $\boldsymbol{v}^*$ 作为参考速度，并将总[摩尔通量](@entry_id:156263) $\boldsymbol{N}_i = c_i \boldsymbol{v}_i$ 分解为[对流通量](@entry_id:158187)和[扩散通量](@entry_id:748422)：$\boldsymbol{N}_i = c_i \boldsymbol{v}^* + \boldsymbol{J}_i^*$。守恒方程变为：
$$ \frac{\partial c_i}{\partial t} + \nabla \cdot (\boldsymbol{N}_i) = \dot{\nu}_i $$
或者展开为：
$$ \frac{\partial c_i}{\partial t} + \nabla \cdot (c_i \boldsymbol{v}^*) = -\nabla \cdot \boldsymbol{J}_i^* + \dot{\nu}_i $$
各项的物理意义与质量基准下的方程完全对应。

然而，一个关键的区别在于[源项](@entry_id:269111)。虽然[化学反应](@entry_id:146973)总质量守恒（$\sum \dot{\omega}_i = 0$），但总摩尔数通常不守恒（例如，在反应 $\mathrm{N}_2\mathrm{O}_4 \rightarrow 2\mathrm{NO}_2$ 中，1 摩尔反应物生成 2 摩尔产物）。因此，一般情况下：
$$ \sum_{i=1}^{N} \dot{\nu}_i \neq 0 $$
这意味着将所有组分的摩尔守恒方程相加，不会像质量基准那样自动退化为一个简单的总[摩尔浓度](@entry_id:139283)守恒方程。

### 连接两种框架：[菲克定律](@entry_id:155177)与反应源项

为了完成描述，我们需要为[扩散通量](@entry_id:748422)（$\boldsymbol{j}_i$ 或 $\boldsymbol{J}_i^*$）和反应源项（$\dot{\omega}_i$ 或 $\dot{\nu}_i$）提供[本构关系](@entry_id:186508)。

#### [扩散](@entry_id:141445)定律的等价性

最简单的[扩散模型](@entry_id:142185)是[菲克第一定律](@entry_id:141732) (Fick's first law)。对于一个[二元混合物](@entry_id:168452)，以摩尔基准描述，[扩散](@entry_id:141445)[摩尔通量](@entry_id:156263)正比于摩尔分数的梯度：
$$ \boldsymbol{J}_1^* = -c D_{12} \nabla X_1 $$
其中 $D_{12}$ 是二元[扩散](@entry_id:141445)系数。

一个自然的问题是：如果我们选择用质量基准来描述同一个物理过程，相应的[菲克定律](@entry_id:155177)形式是怎样的？我们期望找到一个形式为 $\boldsymbol{j}_1 = -\rho D_{12}^{(m)} \nabla Y_1$ 的关系，并确定质量基准下的[扩散](@entry_id:141445)系数 $D_{12}^{(m)}$ 与 $D_{12}$ 的关系。

通过一系列严格的代数推导，利用各种浓度的定义以及它们之间的转换关系，可以证明一个非常简洁而深刻的结果：对于[二元混合物](@entry_id:168452)，两种基准下的[扩散](@entry_id:141445)系数是完全相同的 [@problem_id:2504322]。
$$ D_{12}^{(m)} = D_{12} $$
这个结论表明，二元[扩散](@entry_id:141445)系数 $D_{12}$ 是一个基本的[物理化学](@entry_id:145220)性质，它描述了分子对 1 和 2 之间的相互作用，而不依赖于我们选择的数学描述框架。在推导过程中出现的与摩尔质量和组分相关的复杂因子，最终会完全抵消。

#### 反应[源项](@entry_id:269111)的转换与守恒

质量[源项](@entry_id:269111) $\dot{\omega}_i$ 和摩尔[源项](@entry_id:269111) $\dot{\nu}_i$ 之间的关系可以直接从 $\rho_i = W_i c_i$ 推导出来。由于[化学反应](@entry_id:146973)发生在固定的[控制体积](@entry_id:143882)内，对时间求导可得 [@problem_id:2504337]：
$$ \dot{\omega}_i = W_i \dot{\nu}_i $$

这个简单的关系揭示了更深层次的守恒原理。[化学反应](@entry_id:146973)的基本法则是元素守恒。对于任意元素 $\alpha$，其原子在反应中既不产生也不消失。设 $a_{\alpha i}$ 为一个组分 $i$ 分子中所含元素 $\alpha$ 的[原子数](@entry_id:746561)，那么元素 $\alpha$ 的总摩尔浓度守恒意味着其变化率为零：
$$ \frac{d}{dt} \left( \sum_i a_{\alpha i} c_i \right) = \sum_i a_{\alpha i} \frac{dc_i}{dt} = \sum_i a_{\alpha i} \dot{\nu}_i = 0 $$
这个条件对每一种元素 $\alpha$ 都必须成立。

现在，我们可以利用这个微观的元素[守恒定律](@entry_id:269268)来证明宏观的总[质量守恒](@entry_id:204015)。将 $\dot{\nu}_i = \dot{\omega}_i / W_i$ 代入元素守恒条件：
$$ \sum_i a_{\alpha i} \frac{\dot{\omega}_i}{W_i} = 0 $$
一个分子的摩尔质量 $W_i$ 是其构成原子的摩尔质量 $b_{\alpha}$ 之和，即 $W_i = \sum_{\alpha} a_{\alpha i} b_{\alpha}$。将元素守恒方程两边乘以 $b_{\alpha}$ 并对所有元素 $\alpha$ 求和：
$$ \sum_{\alpha} b_{\alpha} \left( \sum_i a_{\alpha i} \frac{\dot{\omega}_i}{W_i} \right) = \sum_i \frac{\dot{\omega}_i}{W_i} \left( \sum_{\alpha} a_{\alpha i} b_{\alpha} \right) = \sum_i \frac{\dot{\omega}_i}{W_i} (W_i) = \sum_i \dot{\omega}_i = 0 $$
这个推导优美地展示了，宏观的质量守恒定律（$\sum \dot{\omega}_i = 0$）是微观层面原子（元素）守恒的直接结果。例如，在甲烷氧化反应 $\mathrm{CH}_4 + 2\mathrm{O}_2 \rightarrow \mathrm{CO}_2 + 2\mathrm{H}_2\mathrm{O}$ 中，对碳、氢、氧三种元素分别应用 $\sum_i a_{\alpha i} \dot{\nu}_i = 0$，可以验证其均成立，从而保证了该反应描述的总质量是守恒的 [@problem_id:2504337]。

### 实际应用中的框架选择

既然质量基准和摩尔基准的框架都是自洽且等价的，那么在实际建模和计算中，我们应该如何选择？答案取决于具体应用场景的便利性。

**质量基准 ($Y_i$) 的优势**：
如前所述，在质量基准框架下，所有[组分守恒方程](@entry_id:151288)之和能够自动恢复总质量[连续性方程](@entry_id:195013)。这在[计算流体动力学](@entry_id:147500) (CFD) 中尤其有用。求解 $N-1$ 个组分的[质量分数](@entry_id:161575)输运方程，然后通过 $\sum Y_i = 1$ 来代数地确定最后一个组分的质量分数，这种方法能内在、精确地保证总质量的守恒 [@problem_id:2504342]。

**摩尔基准 ($c_i$) 的优势**：
摩尔基准在处理化学问题时，特别是[化学平衡](@entry_id:142113)和元素守恒约束时，显示出巨大优势。在一个[封闭系统](@entry_id:139565)中，元素守恒可以表示为一组关于摩尔浓度 $c_i$ 的线性代数方程 [@problem_id:2504342]：
$$ \sum_i a_{\alpha i} c_i = \text{常数} $$
这些线性约束在数学上比非线性约束更容易处理。如果试图用[质量分数](@entry_id:161575) $Y_i$ 来表达同样的约束，利用关系式 $c_i = \rho Y_i / W_i$，[约束方程](@entry_id:138140)会变为：
$$ \rho \sum_i \frac{a_{\alpha i}}{W_i} Y_i = \text{常数} $$
这个方程不仅包含了变量 $\rho$（它本身是温度、压力和组分的函数），而且使得约束在[状态变量](@entry_id:138790)空间中成为[非线性](@entry_id:637147)[曲面](@entry_id:267450)，处理起来要复杂得多。

#### 何时两种基准的差异可以忽略？

在某些情况下，两种基准的差异很小，可以近似互换。这通常发生在稀溶液或痕量组分的情形中。我们可以量化这种差异。[质量分数](@entry_id:161575)和[摩尔分数](@entry_id:145460)之间的差值为 [@problem_id:2504298]：
$$ |Y_i - X_i| = \left| X_i \frac{W_i}{\bar{W}} - X_i \right| = X_i \left| \frac{W_i}{\bar{W}} - 1 \right| $$
这个差值取决于两个因素：组分的[摩尔分数](@entry_id:145460) $X_i$ 和其摩尔质量与混合物平均摩尔质量的比值 $W_i/\bar{W}$。

对于一个稀疏组分 ($X_i \ll 1$)，如果其[摩尔质量](@entry_id:146110)与主体载气的平均摩尔质量相近 ($W_i \approx \bar{W}$)，那么 $|Y_i - X_i|$ 将非常小。在这种情况下，无论采用质量基准还是摩尔基准，对该组分的描述都非常相似，其[输运方程](@entry_id:756133)的解也差别不大。

我们可以设定一个无量纲容差 $\eta$，如果 $X_i |W_i/\bar{W} - 1| < \eta$，则认为两种基准的差异可以接受，可以选择计算上更方便的一种。反之，如果该值较大（例如，一个轻的分子如氢气 $H_2$ 在一个重的载气如六氟化硫 $SF_6$ 中[扩散](@entry_id:141445)），那么 $W_i/\bar{W}$ 远小于1，两种基准的差异会很显著，必须谨慎选择更合适的框架。通常，对于[理想气体](@entry_id:200096)，摩尔基准下的[输运方程](@entry_id:756133)形式更简单（因为总[摩尔浓度](@entry_id:139283) $c$ 在等温等压下是常数），因此在差异显著时，优先选择摩尔基准是更稳妥的做法 [@problem_id:2504298]。