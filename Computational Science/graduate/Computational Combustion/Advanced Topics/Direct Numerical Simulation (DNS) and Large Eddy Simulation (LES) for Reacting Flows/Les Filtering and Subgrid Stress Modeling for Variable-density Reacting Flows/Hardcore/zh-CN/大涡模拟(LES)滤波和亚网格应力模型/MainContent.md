## 引言
在能源、动力和航空航天等诸多工程领域，对可变密度反应流（如燃烧）的精确预测至关重要。[直接数值模拟](@entry_id:149543)（DNS）能够解析所有时空尺度，但其计算成本高昂到不切实际。大涡模拟（LES）作为一种折中方案，通过直接求解大尺度[湍流](@entry_id:151300)结构、并对小尺度（亚格子）脉动进行建模，在精度和成本之间取得了理想的平衡。然而，当流动涉及剧烈的密度变化和复杂的化学反应时，亚格子尺度的物理过程变得异常复杂，对其进行准确建模便构成了LES方法的核心挑战与知识缺口。

本文旨在系统性地介绍可变密度[反应流](@entry_id:190741)LES中的滤波与亚格子应力建模。读者将通过本文的学习，建立一个坚实的理论基础。
- 在“**原理与机制**”一章中，我们将从最基本的空间滤波操作出发，阐明为何Favre（密度加权）滤波是处理[可变密度流](@entry_id:756427)的标准工具。随后，我们将系统推导滤波后控制方程中出现的各类未封闭亚格子项，并重点分析化学反应源项的封闭难题。
- 在“**应用与交叉学科联系**”一章中，我们将探讨如何通过具体的亚格子应力模型（如[Smagorinsky模型](@entry_id:276289)、梯度模型）和[湍流燃烧模型](@entry_id:1133504)（如[增厚火焰模型](@entry_id:1133093)、层流火焰面模型）来封闭这些项，并展示这些原理如何应用于[超音速流](@entry_id:262511)动、多相流和传热学等多个交叉学科。
- 最后，在“**动手实践**”部分，读者将有机会通过具体计算，将理论知识应用于实践，加深对[亚格子模型](@entry_id:755588)物理意义的理解。

本文将引导你深入[湍流模拟](@entry_id:1133511)的核心，理解从基本原理到前沿应用的完整图景。

## 原理与机制

在[大涡模拟](@entry_id:153702)（Large-Eddy Simulation, LES）中，核心思想是通过[空间滤波](@entry_id:202429)将流场中的物理量分解为大尺度（可解）分量和小尺度（亚格子）分量。本章将深入探讨应用于可变密度[反应流](@entry_id:190741)的[LES滤波](@entry_id:1127170)的基本原理和由此产生的亚格子应力建模机制。我们将从滤波操作的数学定义出发，阐述为何在[可变密度流](@entry_id:756427)中需要采用[Favre滤波](@entry_id:749251)，并系统地推导在滤波后的[守恒方程](@entry_id:1122898)中出现的各项未封闭亚格子项，最终重点分析反应源项的复杂封闭问题。

### LES中的滤波操作

#### 空间滤波的定义与性质

LES的基础是**[空间滤波](@entry_id:202429)**（spatial filtering）操作，它通过一个**滤波核函数**（filter kernel）$G_\Delta$对瞬时流场变量$\phi(\mathbf{x}, t)$进行卷积，从而得到可解尺度场$\bar{\phi}(\mathbf{x}, t)$。这个过程在数学上定义为：

$$
\bar{\phi}(\mathbf{x}) = \int_{D} G_\Delta(\mathbf{x} - \mathbf{r}) \phi(\mathbf{r}) \, d\mathbf{r}
$$

其中，$D$是流动域，$\Delta$是**滤波宽度**（filter width），它表征了可解尺度与亚格子尺度之间的界限，并与[计算网格](@entry_id:168560)的尺寸直接相关。滤波核函数$G_\Delta$本质上是一个低通滤波器，它滤除了尺度小于$\Delta$的波动，保留了尺度大于$\Delta$的结构。

为了确保滤波过程的物理一致性，滤波核必须满足**[归一化条件](@entry_id:156486)**（normalization condition）：

$$
\int_{D} G_\Delta(\mathbf{r}) \, d\mathbf{r} = 1
$$

这个条件至关重要，因为它保证了对一个常数进行滤波会得到其自身，即$\overline{C} = C$。更重要的是，在守恒律的背景下，归一化确保了总的[守恒量](@entry_id:161475)在滤波前后保持不变。例如，考虑一个体积为$V$的域内的总质量$M = \int_V \rho \, d\mathbf{x}$。经过滤波后的总质量为$\bar{M} = \int_V \bar{\rho} \, d\mathbf{x}$。通过[交换积分次序](@entry_id:200463)可以证明，只有当滤波核归一化时，我们才能保证$\bar{M} = M$。若不满足此条件，滤波操作本身就会人为地引入或消除质量，从而破坏了系统的基本守恒性 。

#### 滤波操作与[微分](@entry_id:158422)的[交换性](@entry_id:140240)

在推导滤波后的控制方程时，一个关键问题是滤波操作与[微分](@entry_id:158422)操作是否可以交换顺序。对于一个仅依赖于位移向量$\mathbf{x}-\mathbf{r}$且滤波宽度$\Delta$在空间上恒定的**均匀滤波器**（uniform filter），滤波与[微分](@entry_id:158422)操作是可交换的，即：

$$
\overline{\frac{\partial \phi}{\partial x_i}} = \frac{\partial \bar{\phi}}{\partial x_i}
$$

然而，在实际的LES计算中，尤其是在使用[非均匀网格](@entry_id:752607)时，情况变得复杂。在[有限体积法](@entry_id:141374)中，通常采用网格单元上的[体积平均](@entry_id:1133895)作为**隐式滤波**（implicit filtering）：

$$
\bar{\phi}(\mathbf{x}_i) \equiv \frac{1}{\Delta V_i}\int_{V_i} \phi(\mathbf{x},t)\,\mathrm{d}V
$$

由于网格单元体积$\Delta V_i$随空间位置变化，滤波宽度$\Delta$不再是常数。这种滤波器的非均匀性导致滤波与[微分](@entry_id:158422)不再可交换。它们之间的差异被称为**交换误差**（commutation error）：

$$
\mathcal{C}_i(\phi)(\mathbf{x}) \equiv \overline{\frac{\partial \phi}{\partial x_i}}(\mathbf{x}) - \frac{\partial \bar{\phi}}{\partial x_i}(\mathbf{x}) \neq 0
$$

通过[分部积分](@entry_id:136350)可以推导出，该误差与滤波[核函数](@entry_id:145324)及其梯度的空间变化直接相关 。这个误差项是LES在[非均匀网格](@entry_id:752607)上理论分析和数值实现中的一个重要考虑因素。

与隐式滤波相对的是**[显式滤波](@entry_id:1124770)**（explicit filtering），它通过一个独立的、定义明确的核函数（如[高斯核](@entry_id:1125533)）进行卷积。在动态亚格子模型等高级建模技术中，[显式滤波](@entry_id:1124770)被用作**测试滤波器**（test filter），作用于已被网格隐式滤波的场上，以获取关于可解尺度最小端能量的信息 。

#### 与其他平均方法的区别

必须强调，LES中的空间滤波与[雷诺平均](@entry_id:754341)（RANS）中使用的**系综平均**（ensemble averaging）或在某些条件下使用的**[时间平均](@entry_id:267915)**（time filtering）有本质区别。系综平均是对无限多个相同流动实现的统计平均，它完全抹去了[湍流](@entry_id:151300)的瞬时结构。时间平均则在时间维度上平滑掉脉动。而空间滤波是在某一特定时刻对空间进行的局部平均。因此，即使在满足[遍历性假设](@entry_id:147104)的[定常流](@entry_id:191654)动中，长时间平均可以等同于系综平均，但它们通常都不等同于[空间滤波](@entry_id:202429)的结果。在非定常、非均匀的[反应流](@entry_id:190741)中，这三种操作是完全不同的，选择何种操作决定了整个建模框架的性质和所需求解的物理问题 。

### [可变密度流](@entry_id:756427)的[Favre滤波](@entry_id:749251)

在密度$\rho$恒定的不可压缩流中，直接对[Navier-Stokes](@entry_id:276387)方程进行滤波（称为**雷诺滤波**，Reynolds filtering）是直接的。然而，在燃烧等密度剧烈变化的[可变密度流](@entry_id:756427)中，雷诺滤波会带来严重的复杂性。

考虑[质量守恒](@entry_id:204015)方程（[连续性方程](@entry_id:195013)）：
$$
\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = 0
$$
对其进行雷诺滤波，我们得到：
$$
\frac{\partial \bar{\rho}}{\partial t} + \nabla \cdot (\overline{\rho \mathbf{u}}) = 0
$$
如果我们试图用可解尺度速度$\bar{\mathbf{u}}$来表示其中的通量项$\overline{\rho \mathbf{u}}$，则必须进行如下分解：
$$
\overline{\rho \mathbf{u}} = \bar{\rho} \bar{\mathbf{u}} + (\overline{\rho \mathbf{u}} - \bar{\rho} \bar{\mathbf{u}})
$$
其中，括号内的项$\overline{\rho \mathbf{u}} - \bar{\rho} \bar{\mathbf{u}}$代表了密度与速度在亚格子尺度上的脉动关联，称为**亚格子质量通量**（subgrid mass flux）。它是一个未封闭项，必须被建模。在动量和[标量输运方程](@entry_id:1131253)中，类似的[密度关联](@entry_id:157860)项会大量出现，使得方程组变得异常复杂。

为了克服这一困难，我们引入**密度加权滤波**（density-weighted filtering），也称为**[Favre滤波](@entry_id:749251)**（Favre filtering）。对于任意物理量$\phi$，其[Favre滤波](@entry_id:749251)量$\tilde{\phi}$定义为：
$$
\tilde{\phi} \equiv \frac{\overline{\rho \phi}}{\bar{\rho}}
$$
这个定义的巧妙之处在于，它将密度作为一个权重函数融入到滤波操作中。现在，我们可以直接重写滤波后的质量通量项：$\overline{\rho \mathbf{u}} = \bar{\rho} \tilde{\mathbf{u}}$。代入滤波后的连续性方程，得到：
$$
\frac{\partial \bar{\rho}}{\partial t} + \nabla \cdot (\bar{\rho} \tilde{\mathbf{u}}) = 0
$$
这个方程在形式上与原始的瞬时方程完全一致，并且只包含可解尺度量（$\bar{\rho}$和$\tilde{\mathbf{u}}$），没有任何需要建模的亚格子项。正是由于这种简化，[Favre滤波](@entry_id:749251)成为了[可变密度流](@entry_id:756427)LES的标准方法 [@problem_id:4035239, @problem_id:4035234]。

值得注意的是，在密度恒定的情况下（$\rho = \text{const}$），$\bar{\rho} = \rho$，[Favre滤波](@entry_id:749251)的定义退化为$\tilde{\phi} = \overline{\rho \phi} / \rho = \overline{\phi}$，即[Favre滤波](@entry_id:749251)等同于雷诺滤波。此时，亚格子质量通量项也自然为零，这再次说明了[Favre滤波](@entry_id:749251)是专门为解决可变密度问题而设计的工具 。

### 滤波后方程中的亚格子项

尽管[Favre滤波](@entry_id:749251)简化了连续性方程，但在动量和[标量输运方程](@entry_id:1131253)中，由于[非线性](@entry_id:637147)对流项的存在，未封闭的亚格子项依然会出现。

#### [动量方程](@entry_id:197225)与亚格子[应力张量](@entry_id:148973)

对动量方程的[非线性](@entry_id:637147)对流项$\nabla \cdot (\rho \mathbf{u} \mathbf{u})$进行滤波，得到$\nabla \cdot (\overline{\rho \mathbf{u} \mathbf{u}})$。使用[Favre滤波](@entry_id:749251)的思想，我们希望将其表示为可解尺度Favre速度$\tilde{\mathbf{u}}$的函数。其分解如下：
$$
\overline{\rho u_i u_j} = \bar{\rho} \tilde{u}_i \tilde{u}_j + \underbrace{(\overline{\rho u_i u_j} - \bar{\rho} \tilde{u}_i \tilde{u}_j)}_{\boldsymbol{\tau}_{ij}}
$$
上式中，$\boldsymbol{\tau}_{ij}$被定义为**[Favre滤波](@entry_id:749251)亚格子应力（SGS）张量**（Favre-filtered subgrid-scale stress tensor），它代表了未解析的动量输运。通过引入Favre速度的脉动分量$u_i'' = u_i - \tilde{u}_i$，[SGS应力张量](@entry_id:1131522)可以被物理解释为$\boldsymbol{\tau}_{ij} = \bar{\rho} \widetilde{u_i'' u_j''}$，即亚格子尺度速度脉动的协方差。这个张量是一个未封闭项，必须通过**[亚格子模型](@entry_id:755588)**（subgrid-scale model）来封闭 [@problem_id:4035214, @problem_id:4035239]。

对于可压缩或[可变密度流](@entry_id:756427)，[SGS应力张量](@entry_id:1131522)$\boldsymbol{\tau}_{ij}$可以进一步分解为其**各向同性**（isotropic）和**偏（或无迹）**（deviatoric）部分：
$$
\boldsymbol{\tau}_{ij} = \boldsymbol{\tau}_{ij}^d + \frac{1}{3} \boldsymbol{\tau}_{kk} \delta_{ij}
$$
其中，$\delta_{ij}$是克罗内克符号。各向同性部分与[SGS应力张量](@entry_id:1131522)的迹$\boldsymbol{\tau}_{kk}$有关，而$\boldsymbol{\tau}_{kk} = \overline{\rho u_k u_k} - \bar{\rho} \tilde{u}_k \tilde{u}_k$。定义**亚格子动能**（subgrid-scale kinetic energy）为$k_{\text{sgs}} = \frac{1}{2} \widetilde{u_k'' u_k''}$，可以推导出$\boldsymbol{\tau}_{kk} = 2 \bar{\rho} k_{\text{sgs}}$。各向同性部分对[动量方程](@entry_id:197225)的贡献是一个纯梯度项：
$$
\frac{\partial}{\partial x_j} \left( \frac{1}{3} \boldsymbol{\tau}_{kk} \delta_{ij} \right) = \frac{\partial}{\partial x_i} \left( \frac{1}{3} \boldsymbol{\tau}_{kk} \right) = \frac{\partial}{\partial x_i} \left( \frac{2}{3} \bar{\rho} k_{\text{sgs}} \right)
$$
这个梯度项可以与滤波后的压力梯度$\nabla \bar{p}$合并，定义一个修正压力$p^\star = \bar{p} + \frac{2}{3}\bar{\rho}k_{\text{sgs}}$。这意味着[SGS应力](@entry_id:1131521)的各向同性部分（常被称为“[湍流](@entry_id:151300)压力”）不直接产生涡量，其主要作用通过$k_{\text{sgs}}$的建模和[能量耦合](@entry_id:137595)体现在系统中。而产生剪切和[涡量](@entry_id:142747)耗散的主要是[偏应力](@entry_id:163323)部分$\boldsymbol{\tau}_{ij}^d$，它通常通过涡粘模型来封闭 。

#### [标量输运方程](@entry_id:1131253)与亚格子标量通量

同样地，对于一个通用标量（如物种质量分数$Y_k$或[反应进度](@entry_id:140591)变量$c$）的[输运方程](@entry_id:174281)：
$$
\frac{\partial (\rho \phi)}{\partial t} + \nabla \cdot (\rho \mathbf{u} \phi) = \nabla \cdot \mathbf{J}_\phi + \dot{\omega}_\phi
$$
进行[Favre滤波](@entry_id:749251)后，[非线性](@entry_id:637147)对流项$\overline{\rho \mathbf{u} \phi}$同样产生一个未封闭的**亚格子标量通量**（subgrid-scale scalar flux）：
$$
\mathbf{q}_\phi = \overline{\rho \mathbf{u} \phi} - \bar{\rho} \tilde{\mathbf{u}} \tilde{\phi} = \bar{\rho} (\widetilde{\mathbf{u} \phi} - \tilde{\mathbf{u}} \tilde{\phi})
$$
该项代表了亚格子速度脉动对可解尺度标量的输运作用，通常采用梯度扩散假设来建模：$\mathbf{q}_\phi \approx - \frac{\mu_t}{\text{Sc}_t} \nabla \tilde{\phi}$，其中$\mu_t$是涡粘性系数，$\text{Sc}_t$是[湍流施密特数](@entry_id:150226) 。

除了对流项，[分子扩散](@entry_id:154595)项$\overline{\nabla \cdot \mathbf{J}_\phi}$和化学反应源项$\overline{\dot{\omega}_\phi}$也是未封闭的。[分子输运](@entry_id:195239)系数（如扩散系数$\mathcal{D}$）通常是温度和组分的[非线性](@entry_id:637147)函数，导致$\overline{\mathcal{D} \nabla \phi} \neq \tilde{\mathcal{D}} \nabla \tilde{\phi}$。然而，在LES中，最严峻的封闭挑战来自化学反应源项 。

### 反应源项的封闭问题

化学反应速率$\dot{\omega}$通常是物种浓度和温度的极度[非线性](@entry_id:637147)函数（例如，阿伦尼乌斯形式）。由于这种强[非线性](@entry_id:637147)，滤波后的[反应速率](@entry_id:185114)**不等于**基于滤波后变量计算的[反应速率](@entry_id:185114)：
$$
\overline{\dot{\omega}(\mathbf{Y}, T)} \neq \dot{\omega}(\tilde{\mathbf{Y}}, \tilde{T})
$$
这个不等式是湍流燃烧LES建模的核心难题，称为**[湍流-化学相互作用](@entry_id:756223)**（turbulence-chemistry interaction）的封闭问题 。直接使用$\dot{\omega}(\tilde{\mathbf{Y}}, \tilde{T})$来代替$\overline{\dot{\omega}}$（即所谓的“层[流化](@entry_id:192588)学”假设）会引入巨大误差。

#### 杰森不等式与滤波偏差

我们可以通过数学上的**杰森不等式**（Jensen's Inequality）来理解这种偏差的根源。以阿伦尼乌斯速率中的指数项$f(T) = \exp(-E_a/RT)$为例，其中$E_a$是活化能。对于典型的燃烧过程，活化能很高，使得该函数在其主要贡献区间内是关于温度$T$的**严格[凸函数](@entry_id:143075)**（strictly convex function）。杰森不等式指出，对于一个[凸函数](@entry_id:143075)$f$，其[期望值](@entry_id:150961)（或滤波值）大于或等于基于[期望值](@entry_id:150961)（或滤波值）计算的函数值：
$$
\overline{f(T)} \ge f(\bar{T})
$$
当亚格子温度存在脉动（方差不为零）时，不等式严格成立。这意味着，忽略亚格子温度脉动会系统性地低估真实的平均[反应速率](@entry_id:185114)。我们可以通过对$f(T)$在$\tilde{T}$附近进行二阶[泰勒展开](@entry_id:145057)来量化这个偏差。偏差因子$B = \overline{f(T)}/f(\tilde{T})$ 近似为：
$$
B \approx 1 + \frac{1}{2} \left[ \left( \frac{E_a}{R\tilde{T}} \right)^2 - 2 \frac{E_a}{R\tilde{T}} \right] \frac{\sigma_T^2}{\tilde{T}^2}
$$
其中$\sigma_T^2$是亚格子温度方差。这个表达式明确显示了偏差与亚格子温度波动的强度（$\sigma_T^2/\tilde{T}^2$）和反应的温度敏感性（由$E_a/R\tilde{T}$，即[Zel'dovich数](@entry_id:1134172)，衡量）直接相关 。

#### [概率密度函数](@entry_id:140610)（PDF）方法

为了从根本上解决这个问题，我们需要亚格子尺度上温度和组分[联合分布](@entry_id:263960)的信息。形式上，滤波后的[反应速率](@entry_id:185114)可以通过对瞬时[反应速率](@entry_id:185114)函数与**Favre加权[联合概率密度函数](@entry_id:267139)**（Favre-weighted joint Probability Density Function, PDF）$p^{(F)}(\mathbf{Y}, T)$求积分得到 ：
$$
\overline{\dot{\omega}} = \bar{\rho} \int \dots \int \dot{\omega}(\mathbf{y}, \tau) \, p^{(F)}(\mathbf{y}, \tau) \, d\mathbf{y} \, d\tau
$$
其中$p^{(F)}$的精确定义为：
$$
p^{(F)}(\mathbf{y}, \tau) = \frac{\overline{\rho \delta(\mathbf{y}-\mathbf{Y}) \delta(\tau-T)}}{\bar{\rho}}
$$
$\delta$是狄拉克函数。这个表达式是精确的，但未封闭，因为$p^{(F)}$本身是未知的。

实际的建模策略是采用**[假定PDF](@entry_id:753720)方法**（presumed PDF approach）。该方法假定$p^{(F)}$具有某种特定的函数形式（例如，用Beta分布描述归一化的质量分数，用高斯分布或Delta分布描述温度），其参数（如均值和方差）由可解尺度场量和亚格子模型提供。例如，如果假设温度和组分在亚格子尺度上统计独立，则联合PDF可以分解为各自边缘PDF的乘积。这样，复杂的[多维积分](@entry_id:184252)就可以简化，有时甚至可以得到解析或半解析的封闭表达式 。这些方法，包括火焰面模型（Flamelet models）和火焰面生成流形（FGM）等，构成了现代反应流LES中[湍流-化学相互作用](@entry_id:756223)建模的理论基础 。