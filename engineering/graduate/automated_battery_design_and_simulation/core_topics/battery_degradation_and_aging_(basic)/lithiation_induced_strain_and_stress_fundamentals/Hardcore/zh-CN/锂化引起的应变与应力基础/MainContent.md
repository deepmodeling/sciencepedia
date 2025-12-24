## 引言
在追求更高能量密度和更长[循环寿命](@entry_id:275737)的[锂离子电池](@entry_id:150991)设计中，化学-力学耦合效应扮演着至关重要的角色。电池在充放电过程中，锂离子在电极材料中的嵌入和脱出不可避免地引起材料的体积变化，进而产生内部应力。这些应力是导致[电极材料](@entry_id:199373)粉化、结构坍塌、[SEI膜破裂](@entry_id:1131388)以及容量快速衰减等一系列机械退化问题的根源。因此，深入理解锂化诱导应变与应力的基本原理，是预测电池寿命、诊断失效模式以及设计更可靠、更耐用电池系统的基石。

本文旨在为读者构建一个关于锂化诱导应变与应力的全面知识框架。我们将系统地解决一个核心问题：锂化过程如何产生应力，以及这些应力又如何[反作用](@entry_id:203910)于电池的电化学行为。通过学习本文，读者将掌握从微观物理化学机制到宏观工程应用的完整分析方法。

为实现这一目标，文章分为三个核心章节。第一章“原理与机制”将奠定理论基础，详细阐述化学应变的定义、应力的产生机制，以及应力、化学势与物质扩散之间深刻的耦合关系。第二章“应用与跨学科联系”将展示这些理论如何在实际问题中应用，从单个颗粒的断裂分析到[复合电极](@entry_id:261775)的力学行为，再到复杂的SEI膜失效，并揭示其与材料科学、电化学和[计算模拟](@entry_id:146373)等领域的交叉融合。最后，在“动手实践”部分，通过一系列引导性问题，读者将有机会亲手推导和应用关键模型，从而巩固所学知识，并将其转化为解决实际工程问题的能力。

## 原理与机制

本章旨在深入探讨锂化过程中诱导的应变与应力的基本原理和核心机制。在“引言”章节的基础上，我们将系统地建立一个从基本定义到复杂耦合现象的理论框架。我们将从锂化引起的应变（即[本征应变](@entry_id:198120)）的定义开始，然后阐明这种应变在何种条件下会产生内部应力，并最终探讨应力、化学势和物质传输之间深刻的相互作用。本章内容将为后续章节中关于[电极材料](@entry_id:199373)机械退化和失效行为的详细分析奠定坚实的理论基础。

### 锂化诱导应变的基本概念

#### 化学膨胀与[本征应变](@entry_id:198120)

[电极材料](@entry_id:199373)在锂离子嵌入（锂化）和脱出（去锂化）过程中会发生体积变化，这是电池中电化学-力学耦合现象的根源。从物理本质上看，当锂原子或离子占据主体材料的[晶格](@entry_id:148274)间隙或替代原有原子时，会引起[晶格参数](@entry_id:191810)的改变，从而导致宏观上的尺寸变化。这种由成分变化引起的、在没有外部应力作用下即可发生的应变，被称为**化学应变 (chemical strain)** 或**本征应变 (eigenstrain)**，我们用符号 $\boldsymbol{\epsilon}^{\text{chem}}$ 表示。

[本征应变](@entry_id:198120)是一个核心概念，它类似于热胀冷缩中的[热应变](@entry_id:187744)。一个物体在自由状态下均匀加热时会膨胀，但内部不会产生应力。同样，一个[电极材料](@entry_id:199373)颗粒若能在完全自由、不受任何约束的情况下均匀锂化，它会发生均匀的膨胀，但其内部应处于无应力状态。应力的产生，正源于这种[自由膨胀](@entry_id:139216)受到了阻碍。

#### 化学膨胀的量化：[偏摩尔体积](@entry_id:143502)与维伽定律

为了对化学膨胀进行定量描述，我们需要建立应变量与锂浓度之间的关系。在[化学热力学](@entry_id:137221)中，描述成分变化引起体积变化的最基本物理量是**[偏摩尔体积](@entry_id:143502) (partial molar volume)**，记为 $\Omega$。它定义为在恒温恒压下，体系体积随某组分摩尔数量变化的速率：
$$
\Omega \equiv \left(\frac{\partial V}{\partial n_{\mathrm{Li}}}\right)_{T,P,n_{\mathrm{host}}}
$$
其中 $V$ 是体系的当前体积，$n_{\mathrm{Li}}$ 是锂的摩尔数。如果我们将锂浓度 $c$ 定义为单位参考体积（通常是去锂化状态的体积 $V_0$）中的锂摩尔数，即 $c \equiv n_{\mathrm{Li}}/V_0$，那么在 $\Omega$ 为常数的情况下，积分上式可得体积增量 $\Delta V = V - V_0 = \Omega n_{\mathrm{Li}}$。由此，我们可以定义**体积化学应变 (volumetric chemical strain)** $\varepsilon_V^{\mathrm{chem}} \equiv \Delta V / V_0$，并得到它与浓度的直接关系：
$$
\varepsilon_V^{\mathrm{chem}} = \frac{\Omega n_{\mathrm{Li}}}{V_0} = \Omega c
$$
在许多实际材料中，[偏摩尔体积](@entry_id:143502) $\Omega$ 可能会随浓度 $c$ 变化。在这种情况下，必须采用增量形式，即 $\mathrm{d}V = \Omega(c) \mathrm{d}n_{\mathrm{Li}}$，这导致[体积应变](@entry_id:267252)需要通过积分计算：
$$
\mathrm{d}\varepsilon_V^{\mathrm{chem}} = \frac{\mathrm{d}V}{V_0} = \frac{\Omega(c) V_0 \mathrm{d}c}{V_0} = \Omega(c) \mathrm{d}c \quad \implies \quad \varepsilon_V^{\mathrm{chem}}(c) = \int_0^c \Omega(\xi) \mathrm{d}\xi
$$
这是一个更普适的定义。

除了基于[热力学](@entry_id:172368)定义的[偏摩尔体积](@entry_id:143502)，材料科学领域更常用一个经验性的线性关系，即**维伽定律 (Vegar[d'](@entry_id:902691)s law)**。它假设材料的[晶格常数](@entry_id:158935)随溶质浓度线性变化。在宏观连续介质力学中，这通常表现为**线性化学应变 (linear chemical strain)** $\varepsilon^{\mathrm{chem}}$ 与浓度 $c$ 成正比：
$$
\varepsilon^{\mathrm{chem}} = \beta c
$$
其中 $\beta$ 被称为**维伽系数 (Vegard coefficient)** 或化学膨胀系数。对于[各向同性材料](@entry_id:170678)，这意味着在每个[主方向](@entry_id:276187)上都发生大小为 $\beta c$ 的线性应变。

这两个描述（[偏摩尔体积](@entry_id:143502)和维伽定律）之间存在内在联系。对于各向同性膨胀，在小应变假设下，[体积应变](@entry_id:267252)约等于线性应变之和的三倍，即 $\varepsilon_V^{\mathrm{chem}} \approx 3\varepsilon^{\mathrm{chem}}$。将上述两个关系代入，我们得到 $\Omega c \approx 3(\beta c)$，这揭示了在小应变和各向同性假设下，[热力学](@entry_id:172368)量 $\Omega$ 与经验系数 $\beta$ 之间的重要关系：
$$
\Omega \approx 3\beta
$$
这个关系是连接宏观唯象模型和微观物理化学性质的桥梁。

#### 化学膨胀的各向异性

尽管我们常假设材料是各向同性的，但许多电极材料（如石墨、磷酸铁锂）是单晶或具有织构的[多晶体](@entry_id:139228)，其化学膨胀行为表现出显著的**各向异性 (anisotropy)**。例如，石墨在锂化时，沿其[层状结构](@entry_id:913477)（面内方向）的膨胀非常小，而垂直于层面（c轴方向）的膨胀则非常剧烈。

为了描述这种各向异性行为，我们需要将标量的维伽系数 $\beta$ 推广为一个[二阶张量](@entry_id:199780)，即**化学膨胀张量 (chemical expansion tensor)** $\boldsymbol{\beta}$。此时，化学应变张量与浓度的关系变为：
$$
\boldsymbol{\epsilon}^{\text{chem}} = \boldsymbol{\beta} c
$$
根据**[诺伊曼原理](@entry_id:136408) (Neumann's principle)**，材料物理性质的对称性必须包含其[晶体结构](@entry_id:140373)的对称性。这意味着化学膨胀张量 $\boldsymbol{\beta}$ 的形式受到晶体[点群对称性](@entry_id:141230)的严格约束。对于任意一个属于该[晶体点群](@entry_id:183880)的[对称操作](@entry_id:143398)（用旋转矩阵 $\boldsymbol{R}$ 表示），$\boldsymbol{\beta}$ 必须满足[不变性条件](@entry_id:171412)：
$$
\boldsymbol{R} \boldsymbol{\beta} \boldsymbol{R}^{\top} = \boldsymbol{\beta}
$$
这一原理极大地简化了 $\boldsymbol{\beta}$ 的形式。例如：
*   对于**立方[晶系](@entry_id:137271)**（如[尖晶石结构](@entry_id:154362)的锰酸锂），其高度对称性要求 $\boldsymbol{\beta}$ 是各向同性的，即 $\boldsymbol{\beta} = \beta_0 \boldsymbol{I}$，其中 $\boldsymbol{I}$ 是单位张量。
*   对于**正交[晶系](@entry_id:137271)**（如[橄榄石](@entry_id:1129103)结构的磷酸铁锂），对称性要求 $\boldsymbol{\beta}$ 在晶轴坐标系下为对角阵，但三个对角元通常是独立的：$\boldsymbol{\beta} = \text{diag}(\beta_{xx}, \beta_{yy}, \beta_{zz})$。
*   对于**四方[晶系](@entry_id:137271)**和**六方[晶系](@entry_id:137271)**（如石墨），对称性要求面内膨胀系数相等，但与c轴方向的膨胀系数不同，形式为 $\boldsymbol{\beta} = \text{diag}(\beta_a, \beta_a, \beta_c)$。

理解各向异性膨胀至关重要，因为它会导致复杂的三维应力状态，即便是在均匀锂化的情况下，也可能成为驱动材料断裂的力学因素。

### 化学-力学应力的产生

#### [应变分解](@entry_id:186005)原理

如前所述，化学膨胀本身（即本征应变）并不直接产生应力。应力的产生源于材料的实际变形状态与其自由化学膨胀状态之间的不匹配。在小应变理论框架下，这一思想被精确地表述为**[应变分解](@entry_id:186005)原理 (principle of strain decomposition)**。该原理假设总应变张量 $\boldsymbol{\epsilon}$ 可以被加和分解为一个**[弹性应变](@entry_id:189634) (elastic strain)** $\boldsymbol{\epsilon}^e$ 和一个化学[本征应变](@entry_id:198120) $\boldsymbol{\epsilon}^{\text{chem}}$：
$$
\boldsymbol{\epsilon} = \boldsymbol{\epsilon}^{e} + \boldsymbol{\epsilon}^{\text{chem}}
$$
在材料的[本构关系](@entry_id:186508)中，只有[弹性应变](@entry_id:189634) $\boldsymbol{\epsilon}^e$ 才会引起应力。对于线弹性材料，这遵循**[胡克定律](@entry_id:149682) (Hooke's Law)**：
$$
\boldsymbol{\sigma} = \mathbb{C} : \boldsymbol{\epsilon}^e
$$
其中 $\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973)，$\mathbb{C}$ 是四阶[弹性刚度张量](@entry_id:170728)。

将[应变分解](@entry_id:186005)式代入[胡克定律](@entry_id:149682)，我们得到描述[化学-力学耦合](@entry_id:187897)的基本本构方程：
$$
\boldsymbol{\sigma} = \mathbb{C} : (\boldsymbol{\epsilon} - \boldsymbol{\epsilon}^{\text{chem}})
$$
这个方程明确指出，应力是总应变（由物体位移和边界条件决定）与化学[本征应变](@entry_id:198120)（由局部锂浓度决定）之差的函数。当总应变恰好等于化学应变时（即 $\boldsymbol{\epsilon} = \boldsymbol{\epsilon}^{\text{chem}}$），[弹性应变](@entry_id:189634)为零，应力也为零。

#### 约束膨胀产生的应力

在电池的实际工作中，电极活性材料颗粒的[自由膨胀](@entry_id:139216)几乎总是受到各种形式的约束。这些约束可以是外部的，例如颗粒被粘结剂、导电剂和周围其他颗粒所包围；也可以是内部的，例如在单个颗粒内部，由于[锂离子扩散](@entry_id:1127352)不均匀，导致不同区域的化学膨胀程度不同，从而相互制约。

当[自由膨胀](@entry_id:139216) $\boldsymbol{\epsilon}^{\text{chem}}$ 与由[位移边界条件](@entry_id:203261)所决定的总应变 $\boldsymbol{\epsilon}$ 不兼容时，就会产生非零的弹性应变 $\boldsymbol{\epsilon}^e$，从而导致内部应力的出现。以下两个经典例子可以很好地说明这一机制：

1.  **一维约束杆：** 考虑一根细长的电极棒，其两端被完全固定，因此其总轴向伸长为零（即轴向总应变 $\epsilon_{xx} = 0$）。当这根棒均匀锂化，浓度增加 $\Delta c$ 时，它会产生一个均匀的轴向化学应变 $\epsilon_{xx}^{\text{chem}} = \beta \Delta c$。根据[应变分解](@entry_id:186005)，轴向[弹性应变](@entry_id:189634)为 $\epsilon_{xx}^e = \epsilon_{xx} - \epsilon_{xx}^{\text{chem}} = 0 - \beta \Delta c = -\beta \Delta c$。这个压缩性的[弹性应变](@entry_id:189634)将产生一个压缩应力：
    $$
    \sigma_{xx} = E \epsilon_{xx}^e = -E \beta \Delta c
    $$
    其中 $E$ 是[杨氏模量](@entry_id:140430)。锂化（$\Delta c > 0$）导致压应力，而去锂化（$\Delta c  0$）导致拉应力。

2.  **二维约束薄膜：** 考虑一层电极薄膜，它被完美地粘结在一个刚性基底（如铜箔集流体）上。基底阻止了薄膜在平面内的任何伸缩，因此平面内的总应变分量为零（$\epsilon_{xx} = \epsilon_{yy} = 0$）。当薄膜均匀锂化，浓度增加 $\Delta c$ 时，它会试图在各个方向上膨胀 $\beta \Delta c$。由于平面内膨胀受阻，会产生一个等双轴的压应力 $\sigma_{xx} = \sigma_{yy} = \sigma$。在[平面应力条件](@entry_id:168184)下（薄膜厚度方向自由，$\sigma_{zz}=0$），平面内的[应力-应变关系](@entry_id:274093)为 $\epsilon_{xx}^e = \frac{1}{E}(\sigma_{xx} - \nu \sigma_{yy})$。代入[应变分解](@entry_id:186005) $\epsilon_{xx}^e = \epsilon_{xx} - \epsilon_{xx}^{\text{chem}} = 0 - \beta\Delta c$，我们得到：
    $$
    -\beta \Delta c = \frac{1}{E}(\sigma - \nu \sigma) = \frac{\sigma(1-\nu)}{E}
    $$
    解得双轴应力为：
    $$
    \sigma = -\frac{E}{1-\nu} \beta \Delta c
    $$
    这个组合模量 $\frac{E}{1-\nu}$ 被称为**[双轴模量](@entry_id:184945) (biaxial modulus)**，它比[杨氏模量](@entry_id:140430) $E$ 更大，反映了二维约束下材料变得更“硬”。

这两个例子清晰地表明，即便化学膨胀是均匀的，宏观的几何约束也会导致巨大的内部应力。这些应力是导致电极颗粒粉化、薄膜从[集流体](@entry_id:1123301)上剥离等机械失效模式的直接原因。

#### [大应变](@entry_id:751152)框架（高等主题）

小应变理论在许多[电极材料](@entry_id:199373)（如石墨）中是足够精确的。然而，对于经历巨大体积变化的材料（如硅，体积变化可超过300%），必须采用**有限应变 (finite strain)** 理论。

在有限应变框架下，应变的加和分解不再适用。取而代之的是**变形梯度 (deformation gradient)** $\boldsymbol{F}$ 的**[乘法分解](@entry_id:199514) (multiplicative decomposition)**：
$$
\boldsymbol{F} = \boldsymbol{F}_e \boldsymbol{F}_c
$$
这里的 $\boldsymbol{F}_c$ 代表纯化学膨胀，它将材料从初始参考构型映射到一个假想的、无应力的[中间构型](@entry_id:193000)。$\boldsymbol{F}_e$ 则是弹性变形梯度，它将这个[中间构型](@entry_id:193000)映射到最终的、有应力的真实构型。应力完全由 $\boldsymbol{F}_e$ 决定。

对于各向同性的化学膨胀，$\boldsymbol{F}_c = \lambda_c \boldsymbol{I} = (1 + \beta c) \boldsymbol{I}$。体积的变化由雅可比行列式 $J = \det(\boldsymbol{F})$ 给出。化学膨胀部分的体积比为 $J_c = \det(\boldsymbol{F}_c) = \det((1+\beta c)\boldsymbol{I}) = (1+\beta c)^3$。这与[小应变近似](@entry_id:754971) $\varepsilon_V^{\text{chem}} \approx 3\beta c$ 形成对比，精确地捕捉了[大变形](@entry_id:167243)下的体积变化效应。在无约束的[自由膨胀](@entry_id:139216)中，弹性变形为零（$\boldsymbol{F}_e = \boldsymbol{I}$），总变形即为化学变形（$\boldsymbol{F} = \boldsymbol{F}_c$），此时材料内部无应力。

### 应力、化学势与扩散的耦合

力学应力不仅是锂化的结果，它反过来也会深刻影响锂离子的输运和分布，形成一个完整的闭环耦合。这种反向耦合主要是通过应力对化学势的影响来实现的。

#### 应力增广的化学势

**化学势 (chemical potential)** $\mu$ 是驱动物质扩散的“势能”。扩散总是自发地从高化学势区域流向低化学势区域。在一个受应力的固体中，插入一个额外的溶质原子（如锂）不仅需要克服化学相互作用，还需要克服机械应[力场](@entry_id:147325)做功。因此，固体的化学势必须包含一个力学项。

对于一个在应[力场](@entry_id:147325) $\boldsymbol{\sigma}$ 中的溶质，其化学势可以写成：
$$
\mu = \mu_0(c, T) + \mu_{\text{mech}}(\boldsymbol{\sigma})
$$
其中 $\mu_0$ 是无应力状态下的化学势（主要取决于浓度和温度），$\mu_{\text{mech}}$ 是力学贡献项。通过[热力学](@entry_id:172368)推导可以证明，这个力学项正比于材料的[偏摩尔体积](@entry_id:143502) $\Omega$ 和**[静水应力](@entry_id:186327) (hydrostatic stress)** $\sigma_{\text{hyd}}$ 的乘积：
$$
\mu_{\text{mech}} = -\Omega \cdot \frac{1}{3}\text{tr}(\boldsymbol{\sigma}) = \Omega p
$$
这里，我们定义[静水压力](@entry_id:275365) $p = -\frac{1}{3}\text{tr}(\boldsymbol{\sigma})$（拉伸为负），这与[流体静压力](@entry_id:275365)的定义一致。或者，若定义静水拉应力 $\sigma_{\text{hyd}} = \frac{1}{3}\text{tr}(\boldsymbol{\sigma})$，则力学项为 $-\Omega\sigma_{\text{hyd}}$。无论采用何种符号约定，其物理意义是明确的：
*   在**压缩应力**（$\text{tr}(\boldsymbol{\sigma})  0$, $p > 0$）区域，化学势会**增加**。这在直觉上是容易理解的：将一个原子塞进一个已经被挤压的空间需要更多的能量。
*   在**拉伸应力**（$\text{tr}(\boldsymbol{\sigma}) > 0$, $p  0$）区域，化学势会**降低**。拉伸状态下的[晶格](@entry_id:148274)为锂离子的进入提供了更有利的“空间”。

这个关系也可以从一个给定的亥姆霍兹自由能密度 $\psi(\boldsymbol{\epsilon}, c)$ 出发，通过求其对浓度 $c$ 的偏导数 $\mu = \partial\psi/\partial c$ 来严格导出。对于包含弹性储能项 $\psi_{\text{el}} = \frac{1}{2}(\boldsymbol{\epsilon} - \boldsymbol{\epsilon}^{\text{chem}}):\mathbb{C}:(\boldsymbol{\epsilon} - \boldsymbol{\epsilon}^{\text{chem}})$ 的自由能，可以推导出化学势中的力学耦合项恰好为 $-\boldsymbol{\sigma} : (\partial\boldsymbol{\epsilon}^{\text{chem}}/\partial c) = -\boldsymbol{\sigma} : (\beta \boldsymbol{I}) = -\beta \text{tr}(\boldsymbol{\sigma})$。这再次确认了化学势与[静水应力](@entry_id:186327)之间的线性耦合关系。

#### 应力耦合的扩散

化学势中的力学项直接影响了扩散动力学。根据非[平衡热力学](@entry_id:139780)，[扩散通量](@entry_id:748422) $\boldsymbol{J}$ 与化学[势的梯度](@entry_id:268447)成正比：
$$
\boldsymbol{J} = -M c \nabla\mu
$$
其中 $M$ 是迁移率。将应力增广的化学势代入，并做出一系列简化假设（如[理想溶液](@entry_id:148303)行为、等温条件、常数扩散系数 $D$ 和[偏摩尔体积](@entry_id:143502) $\Omega$ 等），可以得到一个广为使用的**[应力耦合扩散](@entry_id:1132504)方程**：
$$
\boldsymbol{J} = -D \nabla c - \frac{D\Omega}{RT} c \nabla\sigma_{\text{hyd}}
$$
其中 $R$ 是理想气体常数，$T$ 是[绝对温度](@entry_id:144687)，$\sigma_{\text{hyd}}$ 是静水拉应力。该方程包含两项：
1.  **$-D \nabla c$**：经典的**菲克定律**项，由浓度梯度驱动。
2.  **$-\frac{D\Omega}{RT} c \nabla\sigma_{\text{hyd}}$**：**应力梯度驱动项**。由于 $\Omega>0$，这一项表明锂离子会从高静水拉应力（或低静水压）区域向低静水拉应力（或高静水压）区域迁移。换句话说，**锂离子倾向于聚集在受压区域**。

这种[应力-扩散耦合](@entry_id:1132505)效应在电池中具有重要意义。例如，在电极颗粒的[裂纹尖端](@entry_id:182807)，由于应力集中，通常存在很高的拉应力。根据此理论，锂离子会倾向于从[裂纹尖端](@entry_id:182807)区域“逃离”，这可能会在一定程度上减缓裂纹的扩展。反之，材料中受压的区域会吸引更多的锂，从而可能加剧局部膨胀和应力。

### 高等化学-力学现象

基于以上建立的基本原理，我们可以进一步理解[电池材料](@entry_id:1121422)中更复杂的行为，这些行为往往是导致性能衰退和失效的关键。

#### 相分离与相干应变

许多[电极材料](@entry_id:199373)（如[磷酸铁锂](@entry_id:162170)、硅）在锂化过程中会发生**相变 (phase transformation)**，即从一个低锂浓度的$\alpha$相转变为一个高锂浓度的$\beta$相。在[热力学](@entry_id:172368)上，这种行为源于材料的化学自由能 $f_h(c)$ 具有双阱（double-well）特征。
*   在没有应力的情况下，相分离的条件由 $f_h(c)$ 的形状决定。当均匀相的曲率 $f_h''(c)  0$ 时，该相是不稳定的，会自发分解为两个不同的相，这个区域称为**化学亚稳区 (chemical spinodal)**。两相平衡的成分由**[公切线构造](@entry_id:187353) (common-tangent construction)** 确定。
*   然而，在固体中，如果新相与母相之间的界面是**相干的 (coherent)**（即[晶格](@entry_id:148274)是连续的），那么由于两相具有不同的[晶格常数](@entry_id:158935)（即不同的本征应变），界面处就会产生巨大的**相干[应变能](@entry_id:162699) (coherency strain energy)**。这部分弹性储能总是正的，它会增加体系的总自由能。
*   这个额外的能量项会抑制相分离的发生。其效果是使得总自由能的曲率增加了一个正的弹性项，即 $f_{\text{eff}}''(c) = f_h''(c) + \eta$，其中 $\eta$ 正比于[弹性模量](@entry_id:198862)和化学膨胀系数的平方（$\eta \propto E\beta^2$）。因此，相分离的实际发生条件变为 $f_{\text{eff}}''(c)  0$，这意味着只有在 $f_h''(c)$ 足够负时才能克服弹性惩罚。这导致在固体中的**相干亚稳区 (coherent spinodal)** 比纯化学亚稳区要窄得多。
*   这一整套复杂的耦合动力学可以通过**[相场模型](@entry_id:1129578) (phase-field models)**，如**Cahn-Hilliard方程**来描述。在该框架下，化学势不仅包含化学项和梯度项，还必须包含应力耦合项 $\mu = f_h'(c) - \kappa \nabla^2 c - \beta \text{tr}(\boldsymbol{\sigma})$，从而完整地捕捉化学、相变和力学之间的相互作用。

#### 化学-塑性与[蠕变](@entry_id:150410)

当锂化诱导的应力超过材料的**[屈服强度](@entry_id:162154) (yield strength)** 时，材料会发生**塑性变形 (plastic deformation)**，这是一种不可恢复的永久变形。这种现象在硅等高容量电极中尤为普遍。
*   为了描述这种行为，需要将[应变分解](@entry_id:186005)进一步扩展为：$\boldsymbol{\epsilon} = \boldsymbol{\epsilon}^e + \boldsymbol{\epsilon}^p + \boldsymbol{\epsilon}^{\text{chem}}$，其中 $\boldsymbol{\epsilon}^p$ 是塑性[应变张量](@entry_id:1132487)。
*   塑性变形的发生由一个**[屈服函数](@entry_id:167970) (yield function)** $f(\boldsymbol{\sigma}, c, ...)=0$ 控制。这个函数不仅是应力的函数，通常还依赖于锂浓度 $c$，因为锂化会改变材料的微观结构，从而影响其[屈服强度](@entry_id:162154)（例如，锂化硅比纯硅更“软”）。一个典型的J2塑性[屈服函数](@entry_id:167970)可以写为 $f = \sigma_{\text{eq}} - \sigma_y(c, \varepsilon_p^{\text{eq}})$，其中 $\sigma_{\text{eq}}$ 是[von Mises等效应力](@entry_id:756574)，$\sigma_y$ 是与浓度和累积塑性应变 $\varepsilon_p^{\text{eq}}$ 相关的[屈服应力](@entry_id:274513)。
*   塑性应变的演化由**[流动法则](@entry_id:177163) (flow rule)** 决定，它规定了塑性应变率的方向和大小。为了保证[热力学](@entry_id:172368)第二定律（即[塑性耗散](@entry_id:201273)非负 $\mathcal{D} = \boldsymbol{\sigma}:\dot{\boldsymbol{\epsilon}}^p \ge 0$），通常采用关联[流动法则](@entry_id:177163)。
*   此外，在电池的工作温度和应力水平下，材料还可能表现出**蠕变 (creep)**，即在恒定应力下随时间缓慢发生的塑性变形。这在电池充放电过程中的恒压阶段（dwell periods）尤其重要。蠕变可以通过**黏塑性 (viscoplasticity)** 模型（如[Perzyna过应力模型](@entry_id:165503)）来描述，其中塑性应变率与应力超过[屈服面](@entry_id:175331)的“过应力”大小有关。

塑性变形和蠕变是累积损伤和导致电极不可逆容量损失的关键机制。它们通过耗散[机械能](@entry_id:162989)、改变电极的微观结构和几何形状，最终导致电极的粉化和失效。在进行高保真度的[电池寿命预测](@entry_id:1121415)和设计时，必须考虑这些复杂的化学-塑性耦合效应。例如，在[有限元分析](@entry_id:138109)等[数值模拟](@entry_id:146043)中，需要精确推导和实现包含浓度依赖性的[弹性模量](@entry_id:198862)、化学膨胀系数以及塑性参数的完整[本构模型](@entry_id:174726)的**切线模量 (tangent moduli)**，这是确保计算收敛性和准确性的关键。