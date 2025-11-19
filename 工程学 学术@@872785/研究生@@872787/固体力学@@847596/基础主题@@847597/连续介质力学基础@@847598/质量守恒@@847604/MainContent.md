## 引言
[质量守恒定律](@entry_id:147377)是物理学的基石之一，它断言物质在封闭系统内既不会被凭空创造，也不会无故消失。在连续介质力学领域，这一原理更是构建所有理论模型的出发点和基本约束。然而，将这一直观的物理概念转化为能够精确描述复杂变形、流动和多物理场耦合现象的严谨数学工具，并深刻理解其在不同学科中的广泛影响，是研究生阶段学习和研究的关键挑战。

本文旨在系统性地剖析[质量守恒定律](@entry_id:147377)。我们将首先在**“原理与机制”**一章中，从拉格朗日和欧拉两种描述出发，推导其在连续体中的各种数学表述，并探讨不可压缩性等重要特例。接着，在**“应用与跨学科联系”**一章中，我们将展示该定律如何作为核心约束，应用于[热力学耦合](@entry_id:170539)、[多孔介质力学](@entry_id:171662)、计算方法和材料[相变](@entry_id:147324)等前沿领域。最后，**“动手实践”**部分将通过一系列精心设计的计算和分析问题，帮助读者将理论知识转化为解决实际问题的能力。

让我们首先进入第一章，深入探讨质量守恒的数学原理与内在机制。

## 原理与机制

在连续介质力学中，[质量守恒](@entry_id:204015)原理是所有分析的基础支柱之一。它公理化了物质既不能被创造也不能被毁灭的物理直觉。本章旨在系统地阐述这一基本原理，从其在不同[参考系](@entry_id:169232)下的数学表述，到其在模拟复杂物理现象和确保数值模拟稳定性中的关键作用。我们将从基本公设出发，推导出各种等效的数学形式，并探讨其在特定条件（如不可压缩性）下的简化，最后将其推广到包含质量源和非[对流](@entry_id:141806)质量交换的更一般情况。

### [拉格朗日与欧拉描述](@entry_id:190556)中的质量密度

为了描述连续体的变形，我们采用两种互补的视角：拉格朗日（或称物质）描述和欧拉（或称空间）描述。[拉格朗日描述](@entry_id:264498)跟踪每个单独的物质[质点](@entry_id:186768)，而[欧拉描述](@entry_id:264722)则关注空间中的[固定点](@entry_id:156394)。

在时刻 $t=0$，我们定义一个**参考构型** $B_0$，其中的物质质点由其位置向量 $\mathbf{X}$ 来唯一标识。这个向量 $\mathbf{X}$ 就像是赋予每个[质点](@entry_id:186768)的永久“标签”。在任意时刻 $t$，连续体运动到一个**当前构型** $B_t$，原先位于 $\mathbf{X}$ 的[质点](@entry_id:186768)现在占据了空间位置 $\mathbf{x}$。这个映射关系由运动函数 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$ 给出。

为了量化质量的[分布](@entry_id:182848)，我们定义两种密度场 [@problem_id:2623905]：

1.  **参考质量密度** $\rho_0(\mathbf{X})$：这是一个**拉格朗日场**，定义在参考构型上。它表示单位参考体积内的质量。由于物质质点的质量是守恒的，且其标签 $\mathbf{X}$ 及其在参考构型中的[体积元](@entry_id:267802) $\mathrm{d}V$ 不随时间改变，因此 $\rho_0$ 是一个只依赖于物质质点 $\mathbf{X}$ 而与时间无关的量。其单位是 $\mathrm{kg \cdot m^{-3}}$。

2.  **当前质量密度** $\rho(\mathbf{x}, t)$：这是一个**欧拉场**，定义在当前构型上。它表示在时刻 $t$、空间点 $\mathbf{x}$ 处单位当前体积内的质量。由于变形会引起体积变化，即使总质量不变，局部密度也会随时间和空间位置而改变。其单位同样是 $\mathrm{kg \cdot m^{-3}}$。

混淆这两种描述是[连续介质力学](@entry_id:155125)初学者常见的错误。$\mathbf{X}$ 是质点的身份标签，固定不变；而 $\mathbf{x}$ 是该质点随时间变化的当前住址 [@problem_id:2623931]。这两种密度代表了同一个物理量（质量），但它们是相对于两种不同的体[积度量](@entry_id:637352)（参考体积和当前体积）来定义的。正确理解和转换这两种密度是建立质量守恒方程的第一步 [@problem_id:2623931] [@problem_id:2623905]。

### 局部质量守恒：[连续性方程](@entry_id:195013)

质量守恒的公理指出：**任何物质体（即一组固定的物质[质点](@entry_id:186768)）的总质量在运动过程中保持不变。** 让我们将这个全局性的积分陈述转化为一个局部性的点态方程。

#### 几何基础：[体积元](@entry_id:267802)的变换

考虑在参考构型中，以点 $\mathbf{X}$ 为顶点的一个微小的物质平行六面体，由三个[线性无关](@entry_id:148207)的微小矢量 $\mathrm{d}\mathbf{X}_1, \mathrm{d}\mathbf{X}_2, \mathrm{d}\mathbf{X}_3$ 张成。其体积 $\mathrm{d}V$ 由标量三重积给出：
$$ \mathrm{d}V = (\mathrm{d}\mathbf{X}_1 \times \mathrm{d}\mathbf{X}_2) \cdot \mathrm{d}\mathbf{X}_3 $$
在运动 $\boldsymbol{\varphi}$ 的作用下，这些物质[线元](@entry_id:196833)被映射到当前构型中，成为新的线元 $\mathrm{d}\mathbf{x}_i$。根据**变形梯度** $\mathbf{F} = \nabla_{\mathbf{X}}\boldsymbol{\varphi}$ 的定义，我们有 $\mathrm{d}\mathbf{x}_i = \mathbf{F} \, \mathrm{d}\mathbf{X}_i$。当前构型中变形后的平行六面体的体积 $\mathrm{d}v$ 同样由标量三重积给出 [@problem_id:2623902]：
$$ \mathrm{d}v = (\mathrm{d}\mathbf{x}_1 \times \mathrm{d}\mathbf{x}_2) \cdot \mathrm{d}\mathbf{x}_3 = ((\mathbf{F}\,\mathrm{d}\mathbf{X}_1) \times (\mathbf{F}\,\mathrm{d}\mathbf{X}_2)) \cdot (\mathbf{F}\,\mathrm{d}\mathbf{X}_3) $$
利用线性代数恒等式，上式可以简化为一个优美的关系式：
$$ \mathrm{d}v = (\det\mathbf{F}) \, \mathrm{d}V $$
我们将变形梯度的[行列式](@entry_id:142978)记为 $J = \det\mathbf{F}$，它被称为**[雅可比行列式](@entry_id:137120)**或**雅可比安**。因此，我们得到了体积元之间至关重要的关系：
$$ \mathrm{d}v = J \, \mathrm{d}V $$
这个公式的几何意义是，[雅可比](@entry_id:264467)安 $J$ 度量了物质在局部经历的体积变化率。$J>1$ 表示体积膨胀，$J<1$ 表示体积压缩，$J=1$ 表示体积不变。

#### [拉格朗日形式](@entry_id:145697)的[连续性方程](@entry_id:195013)

现在，考虑这个微小物质[体积元](@entry_id:267802)的质量 $\mathrm{d}m$。根据[质量守恒](@entry_id:204015)，这个质量是不变的。在参考构型和当前构型中，这个质量可以分别表示为：
$$ \mathrm{d}m = \rho_0(\mathbf{X}) \, \mathrm{d}V \quad \text{和} \quad \mathrm{d}m = \rho(\mathbf{x}, t) \, \mathrm{d}v $$
令两者相等，并代入[体积元](@entry_id:267802)的关系式 $\mathrm{d}v = J\,\mathrm{d}V$，我们得到：
$$ \rho_0(\mathbf{X}) \, \mathrm{d}V = \rho(\boldsymbol{\varphi}(\mathbf{X}, t), t) \, (J \, \mathrm{d}V) $$
由于这个关系对任意非零的微元 $\mathrm{d}V$ 都成立，我们可以消去它，从而得到[质量守恒](@entry_id:204015)的**局部（点态）[拉格朗日形式](@entry_id:145697)**，也称为**物质形式的连续性方程** [@problem_id:2623905] [@problem_id:2623931]：
$$ \rho_0(\mathbf{X}) = \rho(\boldsymbol{\varphi}(\mathbf{X}, t), t) J(\mathbf{X}, t) $$
通常简记为 $\rho_0 = \rho J$。这个方程优雅地连接了两种密度和一个纯运动学量 $J$。它表明，当前密度可以通过参考密度除以局部体积比来计算：$\rho = \rho_0 / J$。

#### 物质不可入性原理

由于质量密度 $\rho_0$ 和 $\rho$ 在物理上必须是正值，上述[连续性方程](@entry_id:195013) $\rho_0 = \rho J$ 蕴含了一个深刻的物理约束：$J$ 必须恒为正值，即 $J > 0$。
- 如果 $J$ 变为负值，将意味着负的当前密度，这在经典物理中是荒谬的。$J  0$ 在几何上对应于物质的局部“翻转”，比如一个[右手坐标系](@entry_id:166669)定义的微元变成了左手[坐标系](@entry_id:156346)。
- 如果 $J$ 变为零，将意味着当前密度趋于无穷大，这对应于有限质量的物质被压缩到零体积。

因此，$J  0$ 的条件，即**物质不可入性公理**，是任何物理上可行的变形所必须满足的基本约束 [@problem_id:2623902]。这要求描述运动的函数 $\boldsymbol{\varphi}$ 必须是保持定向的，并且不能将有限体积的区域压垮为零体积的[曲面](@entry_id:267450)或线。从数学上讲，这要求 $\boldsymbol{\varphi}$ 具有足够的正则性，例如，在经典框架下，它是一个 $C^1$ [微分同胚](@entry_id:147249)；在更现代的[弱解](@entry_id:161732)理论中，它需要满足更复杂的索伯列夫空间条件，以确保其几乎处处是可逆的并且雅可比安为正 [@problem_id:2623942]。

### [连续性方程](@entry_id:195013)的等效形式

[拉格朗日形式](@entry_id:145697)的[连续性方程](@entry_id:195013) $\rho_0 = \rho J$ 对于理论推导非常方便，但在许多应用中，特别是[流体力学](@entry_id:136788)和数值计算，[欧拉形式](@entry_id:637896)更为常用。

#### [欧拉形式](@entry_id:637896)的[连续性方程](@entry_id:195013)

让我们从一个固定在空间中的任意[控制体](@entry_id:143882) $V$（[欧拉视角](@entry_id:265288)）出发。体积 $V$ 内总质量的变化率等于穿过其边界 $\partial V$ 的净质量通量。假设没有内部质量源，[质量平衡](@entry_id:181721)可以写成：
$$ \frac{\mathrm{d}}{\mathrm{d}t} \int_V \rho \, \mathrm{d}V = - \oint_{\partial V} (\rho \mathbf{v}) \cdot \mathbf{n} \, \mathrm{d}A $$
其中 $\mathbf{v}$ 是物质[速度场](@entry_id:271461)，$\mathbf{n}$ 是边界 $\partial V$ 的外[法线](@entry_id:167651)向量，$\rho\mathbf{v}$ 是**[对流通量](@entry_id:158187)**（单位时间穿过单位面积的质量）。左侧是质量的累积率，右侧是净流入率（负的流出率）[@problem_id:2623939]。

由于控制体 $V$ 是固定的，我们可以将时间导数移到积分号内。然后，利用**[高斯散度定理](@entry_id:188065)**将右侧的[面积分](@entry_id:275394)转换成[体积分](@entry_id:171119)：
$$ \int_V \frac{\partial \rho}{\partial t} \, \mathrm{d}V = - \int_V \nabla \cdot (\rho \mathbf{v}) \, \mathrm{d}V $$
将所有项移到一边，我们得到：
$$ \int_V \left( \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) \right) \mathrm{d}V = 0 $$
这个积分等式必须对**任意**[控制体](@entry_id:143882) $V$ 都成立。这一步从积分形式到微分形式的转换，被称为**局部化**。其严格的数学论证依赖于所谓的**变分法基本引理**或**[勒贝格微分定理](@entry_id:196721)**。如果被积函数是连续的，那么它必须处处为零。在更一般的情况下，只需假设场具有足够的正则性（例如，在适当的索伯列夫空间中），就可以得出被积函数**几乎处处**为零的结论 [@problem_id:2623875]。由此，我们得到[质量守恒](@entry_id:204015)的**局部[欧拉形式](@entry_id:637896)**，也称为**[空间形式](@entry_id:186145)的[连续性方程](@entry_id:195013)**：
$$ \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = 0 $$
这个方程是一个守恒律，它表明局部密度的增加（$\partial \rho / \partial t$）必须由质量的汇聚（$-\nabla \cdot (\rho \mathbf{v})$）来平衡。

#### 物质导数形式

利用向量微积分的[乘法法则](@entry_id:144424)，$\nabla \cdot (\rho \mathbf{v}) = (\nabla \rho) \cdot \mathbf{v} + \rho (\nabla \cdot \mathbf{v})$，我们可以将[空间形式](@entry_id:186145)的[连续性方程](@entry_id:195013)改写为：
$$ \left(\frac{\partial \rho}{\partial t} + \mathbf{v} \cdot \nabla \rho\right) + \rho (\nabla \cdot \mathbf{v}) = 0 $$
括号中的项正是当前密度 $\rho$ 的**物质导数**（或随流导数）$\frac{D\rho}{Dt}$，它表示一个随物质质点运动的观察者所测得的密度变化率。因此，我们得到了连续性方程的另一种等效形式 [@problem_id:2623939]：
$$ \frac{D\rho}{Dt} + \rho (\nabla \cdot \mathbf{v}) = 0 $$
这个形式非常直观：一个物质[质点](@entry_id:186768)周围的密度增加率（$\frac{D\rho}{Dt}$）等于该点的密度乘以[速度场](@entry_id:271461)的散度（即[体积膨胀](@entry_id:144241)率）的负值。

这三种形式——$\rho_0 = \rho J$（拉格朗日）、$\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = 0$（欧拉守恒）、以及 $\frac{D\rho}{Dt} + \rho (\nabla \cdot \mathbf{v}) = 0$（欧拉非守恒）——是完全等价的。例如，对 $\rho_0 = \rho J$ 两边取[物质导数](@entry_id:172646)，并利用 $\frac{D\rho_0}{Dt}=0$ 和[运动学](@entry_id:173318)恒等式 $\frac{DJ}{Dt} = J(\nabla \cdot \mathbf{v})$，可以直接推导出 $\frac{D\rho}{Dt} + \rho (\nabla \cdot \mathbf{v}) = 0$ [@problem_id:2623902]。

### 特殊情况：[不可压缩性](@entry_id:274914)

**[不可压缩材料](@entry_id:159741)**是一个重要的理想化模型，其定义为：**在任何运动过程中，每个物质质点的密度保持为其初始值。**

- **物理定义**: $\rho(\boldsymbol{\varphi}(\mathbf{X}, t), t) = \rho_0(\mathbf{X})$。换句话说，$\frac{D\rho}{Dt} = 0$。

根据这个定义，我们可以立即从连续性方程的不同形式中得出不可压缩性的运动学约束 [@problem_id:2623946]：
1.  从[拉格朗日形式](@entry_id:145697) $\rho_0 = \rho J$，代入 $\rho = \rho_0$ 立即得到**精确的有限应变不可压缩条件**：
    $$ J = \det(\mathbf{F}) = 1 $$
    这意味着不可压缩变形是**等体积**（isochoric）变形。注意，这个条件并不要求初始密度 $\rho_0$ 是均匀的。一个非均匀的材料（例如[复合材料](@entry_id:139856)）也可以是不可压缩的，只要其每个组分的密度都保持不变。

2.  从[物质导数](@entry_id:172646)形式 $\frac{D\rho}{Dt} + \rho (\nabla \cdot \mathbf{v}) = 0$，代入 $\frac{D\rho}{Dt} = 0$ 得到**欧拉速率形式的不可压缩条件**：
    $$ \nabla \cdot \mathbf{v} = 0 $$
    这个条件表明，[不可压缩流](@entry_id:140301)动的速度场是无散的（solenoidal）。

#### 线性化不可压缩条件

在线性化理论（小应变理论）中，[位移梯度](@entry_id:165352) $\mathbf{H} = \nabla_{\mathbf{X}}\mathbf{u}$ 被假设为微小量。此时，$\mathbf{F} = \mathbf{I} + \mathbf{H}$，其[行列式](@entry_id:142978)可以近似为：
$$ J = \det(\mathbf{I} + \mathbf{H}) \approx 1 + \mathrm{tr}(\mathbf{H}) = 1 + \nabla \cdot \mathbf{u} $$
将精确条件 $J=1$ 应用于这个一阶近似，我们得到**线性化的不可压缩条件** [@problem_id:2623946]：
$$ \nabla \cdot \mathbf{u} = 0 $$
必须强调，$\nabla \cdot \mathbf{u} = 0$ 只是对 $J=1$ 的一阶近似。一个满足 $\nabla \cdot \mathbf{u} = 0$ 的有限变形不一定是等体积的。例如，一个[位移场](@entry_id:141476) $\mathbf{u} = (-\alpha X_1, \alpha X_2, 0)$ 满足 $\nabla \cdot \mathbf{u} = -\alpha + \alpha + 0 = 0$，但其雅可比安是 $J = (1-\alpha)(1+\alpha) = 1 - \alpha^2$，当 $\alpha \neq 0$ 时显然不等于1。因此，$\nabla \cdot \mathbf{u}=0$ 仅在小应变假设下是不可压缩性的有效表述 [@problem_id:2623946]。

### 推广：质量源与非[对流](@entry_id:141806)质量通量

在更一般的情况下，一个物质体的质量可能由于内部[化学反应](@entry_id:146973)（质量源或汇）或相对于主体材料的扩散过程（非[对流](@entry_id:141806)质量通量）而发生变化。

考虑一个物质体，其质量变化率现在等于内部[质量生成](@entry_id:161427)率和穿过其边界的净质量通量之和。除了随物质运动的**[对流通量](@entry_id:158187)** $\rho\mathbf{v}$ 之外，我们引入一个**非[对流通量](@entry_id:158187)**（或相对通量）$\mathbf{j}$，它表示质量相对于背景材料运动的通量 [@problem_id:2623926]。同时，我们引入一个**体积质量源** $r$，它表示单位体积、单位时间内生成的质量。

对于一个在空间中固定的控制体 $V$，[质量平衡方程](@entry_id:178786)变为 [@problem_id:2623918]：
$$ \frac{\mathrm{d}}{\mathrm{d}t} \int_V \rho \, \mathrm{d}V = - \oint_{\partial V} (\rho \mathbf{v} + \mathbf{j}) \cdot \mathbf{n} \, \mathrm{d}A + \int_V r \, \mathrm{d}V $$
经过与之前相同的局部化步骤，我们得到推广的[连续性方程](@entry_id:195013)：
$$ \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v} + \mathbf{j}) = r $$
在许多标准的[固体力学](@entry_id:164042)问题中，我们假设质量是严格守恒且“冻结”在材料中的，这意味着 $r=0$ 和 $\mathbf{j}=\mathbf{0}$。然而，在许多重要的物理场景中，$\mathbf{j} \neq \mathbf{0}$ 是不可或缺的 [@problem_id:2623926]：
- **[高温蠕变](@entry_id:189747)**: 在像 Nabarro-Herring 或 Coble 蠕变这样的扩散控制[蠕变](@entry_id:150410)机制中，原子通过[晶格](@entry_id:196752)或[晶界扩散](@entry_id:190000)以响应施加的应力，这构成了相对于[晶格](@entry_id:196752)运动的质量通量。
- **[烧结](@entry_id:140230)**: 在[粉末冶金](@entry_id:159298)中，材料的[致密化](@entry_id:161543)是通过原子从颗粒[表面扩散](@entry_id:186850)到颈部来实现的。
- **[电迁移](@entry_id:141380)**: 在微电子器件中，高电流密度可以驱动金属原子相对于[晶格](@entry_id:196752)迁移，导致导线失效。
- **[多孔介质](@entry_id:154591)**: 在充满流体的[多孔固体](@entry_id:154776)中，流体相对于固体骨架的流动可以被模型化为一个非[对流](@entry_id:141806)质量通量。

在这些情况下，即使是单组分材料，也必须考虑 $\mathbf{j}$ 的存在。

#### 边界条件

当处理包含非[对流通量](@entry_id:158187) $\mathbf{j}$ 的问题时（例如，基于菲克定律 $\mathbf{j} = -D \nabla \rho$ 的[扩散](@entry_id:141445)问题），必须在区域的边界上指定适当的边界条件才能使问题适定。常见的边界条件类型有 [@problem_id:2623935]：
- **狄利克雷（Dirichlet）条件**: 指定边界上的密度值，$\rho = \rho_{\text{prescribed}}$。这代表与一个恒定浓度的大“储库”接触。
- **诺伊曼（Neumann）条件**: 指定穿过边界的法向通量。在随体运动的物质边界上，净通量就是非[对流通量](@entry_id:158187) $\mathbf{j} \cdot \mathbf{n}$。因此，指定 $\mathbf{j} \cdot \mathbf{n} = f$ 是一个[诺伊曼条件](@entry_id:165471)。一个常见的例子是**不渗透边界**，其条件为 $\mathbf{j} \cdot \mathbf{n} = 0$。对于一个固定边界，则必须指定总通量 $(\rho\mathbf{v}+\mathbf{j})\cdot\mathbf{n}$。
- **罗宾（Robin）或混合条件**: 边界通量与边界上的密度值相关联，例如 $\mathbf{j} \cdot \mathbf{n} = k(\rho - \rho_{\infty})$。这通常模拟了有限的界面[传质](@entry_id:151908)速率，其中传质速率正比于[表面密度](@entry_id:161889)与外部环境密度 $\rho_{\infty}$ 之间的差异。

选择哪种边界条件取决于所研究系统的具体物理情况。错误地指定边界条件，例如在需要考虑总通量的固定边界上只指定 $\mathbf{j} \cdot \mathbf{n}$，会导致模型在物理上是不正确的。