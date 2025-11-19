## 引言
[复合材料](@entry_id:139856)凭借其卓越的可设计性和高性能，已成为从航空航天到生物医学等众多高科技领域的关键材料。然而，其性能的成功预测与优化，依赖于我们对其内部微观世界复杂相互作用的深刻理解。一个核心的挑战在于：如何仅根据基体和增强体各自的性能，精确地预测出整个[复合材料](@entry_id:139856)的宏观力学响应？这正是[复合材料微观力学](@entry_id:201432)所要解决的关键知识缺口。

本篇文章将系统性地引导您深入[复合材料微观力学](@entry_id:201432)的核心。在第一章“原理与机制”中，我们将从均质化的基本概念（如[代表性](@entry_id:204613)体积单元）出发，建立微观与宏观的联系，并详细阐述从基础的混合律（[Voigt-Reuss界](@entry_id:190099)限）到更高级的平均[场模](@entry_id:189270)型（如[Eshelby夹杂理论](@entry_id:188756)、Mori-Tanaka和自洽方案）的推导与物理内涵。随后，在第二章“应用与交叉学科联系”中，我们将展示这些理论模型如何应用于实际工程问题，包括结构设计、[多物理场耦合](@entry_id:171389)分析（如[热力学](@entry_id:141121)行为）以及损伤与失效预测，并揭示其在生物力学等[交叉](@entry_id:147634)学科中的应用。最后，在第三章“动手实践”中，您将通过一系列精心设计的问题，亲手应用这些理论，将抽象的数学模型转化为解决实际问题的有力工具。

## 原理与机制

[复合材料](@entry_id:139856)的[微观力学](@entry_id:195009)旨在基于其组分的性质和微观结构来预测其宏观力学行为。这一过程的核心是“均质化”——用一个等效的均匀介质来代替复杂的[非均质材料](@entry_id:196262)。本章将系统地阐述实现这一目标的基本原理和关键机制，从基本的平均化概念到先进的预测模型。

### 均质化的基础：从微观结构到等效性能

将非均质[复合材料](@entry_id:139856)视为一个均匀的连续体，只有在所考察的长度尺度远大于其内部非均质特征（如纤维、颗粒）的尺寸时才是有效的。为了在数学上严谨地建立微观细节与宏观响应之间的联系，我们必须引入几个基本概念。

#### [代表性](@entry_id:204613)体积单元（RVE）

均质化的基石是**代表性体积单元（Representative Volume Element, RVE）**的概念。RVE是[复合材料](@entry_id:139856)中的一个最小区域，其在统计意义上能够代表整个材料的微观结构和力学性能。一个精确且可操作的RVE定义必须满足几个条件 [@problem_id:2662334]。

首先是**[尺度分离](@entry_id:270204)**原则。RVE的特征尺寸 $\ell_{\mathrm{RVE}}$ 必须远大于微观结构的特征长度尺度，这些尺度包括夹杂物的尺寸 $d$、平均间距 $s$ 以及最重要的[统计相关](@entry_id:200201)长度 $\ell_c$（它量化了微观结构中[空间相关性](@entry_id:203497)的衰减）。同时，RVE必须远小于宏观结构或载荷变化的特征长度 $L$，这样才能被视为宏观上的一个“点”。因此，必须满足以下尺度分离的层级关系：

$$
\{d, s, \ell_c\} \ll \ell_{\mathrm{RVE}} \ll L
$$

这个条件确保了在RVE尺度上计算出的“等效”性能是局部化的，并且宏观场（如应力 $\boldsymbol{\Sigma}$ 和应变 $\boldsymbol{E}$）在RVE上可以被近似认为是均匀的。用梯度来表达，这意味着无量纲量 $\lVert\nabla \boldsymbol{\Sigma}\rVert\ell_{\mathrm{RVE}}/\lVert\boldsymbol{\Sigma}\rVert \ll 1$ 和 $\lVert\nabla \boldsymbol{E}\rVert\ell_{\mathrm{RVE}}/\lVert\boldsymbol{E}\rVert \ll 1$ 必须成立。

其次，对于一个统计上均匀的随机[复合材料](@entry_id:139856)，RVE的一个关键特性是，通过其计算出的等效性能对于施加在RVE边界上的特定“容许”边界条件（如线性位移、均匀应力或[周期性边界条件](@entry_id:147809)）不敏感。当体积单元足够大时，这种边界条件不敏感性便得以实现，RVE正是达到这种不敏感性所需的最小体积。

#### 平均化与能量一致性：[Hill-Mandel条件](@entry_id:163076)

微观场与宏观场之间的联系通过体积平均建立。宏观应力 $\boldsymbol{\Sigma}$ 和宏观应变 $\boldsymbol{E}$ 分别被定义为微观应力 $\boldsymbol{\sigma}(\mathbf{x})$ 和微观应变 $\boldsymbol{\varepsilon}(\mathbf{x})$ 在RVE上的体积平均：

$$
\boldsymbol{\Sigma} = \langle \boldsymbol{\sigma} \rangle \equiv \frac{1}{V_{\mathrm{RVE}}} \int_{V_{\mathrm{RVE}}} \boldsymbol{\sigma}(\mathbf{x}) \, dV
$$

$$
\boldsymbol{E} = \langle \boldsymbol{\varepsilon} \rangle \equiv \frac{1}{V_{\mathrm{RVE}}} \int_{V_{\mathrm{RVE}}} \boldsymbol{\varepsilon}(\mathbf{x}) \, dV
$$

为了确保均质化过程在能量上是客观一致的，宏观尺度上的功率必须等于微观尺度上功率的平均值。这一原理被称为**Hill-Mandel宏观[均匀性](@entry_id:152612)条件**或能量一致性条件 [@problem_id:2519130]。它要求对于任何与施加的宏观[应变率](@entry_id:154778) $\dot{\boldsymbol{E}}$ 一致的容许微观变形率场 $\dot{\boldsymbol{\varepsilon}}(\mathbf{x})$，以下等式必须成立：

$$
\boldsymbol{\Sigma} : \dot{\boldsymbol{E}} = \langle \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} \rangle
$$

将宏观量的定义代入，该条件可写为：

$$
\langle \boldsymbol{\sigma} \rangle : \langle \dot{\boldsymbol{\varepsilon}} \rangle = \langle \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} \rangle
$$

这个条件并非一个普通的恒等式，它深刻地指出“平均值的乘积”等于“乘积的平均值”。这一等式为选择适用于RVE分析的边界条件提供了理论约束，并确保了从微观尺度到宏观尺度的[能量守恒](@entry_id:140514)。它保证了通过不同容许边界条件（如均匀位移、均匀应力或周期性边界条件）计算出的等效本构关系在RVE足够大时收敛于同一个结果，从而使均质化过程客观有效。

### 基本界限：混合律

在深入研究复杂的模型之前，我们可以通过一些简化的物理假设来获得[复合材料](@entry_id:139856)等效性能的初步估计。最著名的是[Voigt和Reuss模型](@entry_id:202293)，它们为等效模量提供了一组严格的数学界限。

#### Voigt模型（[等应变](@entry_id:184570)条件）

Voigt模型基于一个非常强的假设：[复合材料](@entry_id:139856)中所有组分的**应变场是均匀的**，且等于宏观应变，即 $\boldsymbol{\varepsilon}(\mathbf{x}) = \boldsymbol{E}$。这种情况被称为**[等应变](@entry_id:184570)**条件。这个假设自动满足了变形的几何相容性。

在[等应变](@entry_id:184570)条件下，宏观应力是各相[平均应力](@entry_id:751819)的加权平均：

$$
\boldsymbol{\Sigma} = \sum_{i=1}^{N} v_i \langle \boldsymbol{\sigma} \rangle_i = \sum_{i=1}^{N} v_i (\mathbf{C}_i : \langle \boldsymbol{\varepsilon} \rangle_i) = \left( \sum_{i=1}^{N} v_i \mathbf{C}_i \right) : \boldsymbol{E}
$$

其中 $v_i$ 和 $\mathbf{C}_i$ 分别是第 $i$ 相的[体积分数](@entry_id:756566)和[刚度张量](@entry_id:176588)。因此，Voigt模型的等效[刚度张量](@entry_id:176588) $\mathbf{C}_V$ 是各相[刚度张量](@entry_id:176588)的算术平均：

$$
\mathbf{C}_V = \sum_{i=1}^{N} v_i \mathbf{C}_i
$$

对于两相[复合材料](@entry_id:139856)在[单轴拉伸](@entry_id:188287)下的等效[杨氏模量](@entry_id:140430)，这简化为**算术混合律**：$E_V = v_1 E_1 + v_2 E_2$。Voigt模型通常会高估材料的实际刚度，它构成了等效模量的一个**上界**。这种理想化的[等应变](@entry_id:184570)状态在一种层合板结构中可以近似实现，即当载荷平行于各层铺设方向时，各层由于完美的粘接而必须共同伸长 [@problem_id:2519195]。

#### Reuss模型（[等应力](@entry_id:204402)条件）

与Voigt模型相对，Reuss模型假设[复合材料](@entry_id:139856)中所有组分的**应[力场](@entry_id:147325)是均匀的**，且等于宏观应力，即 $\boldsymbol{\sigma}(\mathbf{x}) = \boldsymbol{\Sigma}$。这种情况被称为**[等应力](@entry_id:204402)**条件。这个假设满足了[静力平衡](@entry_id:163498)和界面上的应力连续性要求。

在[等应力](@entry_id:204402)条件下，宏观应变是各相平均应变的加权平均：

$$
\boldsymbol{E} = \sum_{i=1}^{N} v_i \langle \boldsymbol{\varepsilon} \rangle_i = \sum_{i=1}^{N} v_i (\mathbf{S}_i : \langle \boldsymbol{\sigma} \rangle_i) = \left( \sum_{i=1}^{N} v_i \mathbf{S}_i \right) : \boldsymbol{\Sigma}
$$

其中 $\mathbf{S}_i = \mathbf{C}_i^{-1}$ 是第 $i$ 相的柔度张量。因此，Reuss模型的等效柔度张量 $\mathbf{S}_R$ 是各相柔度张量的算术平均，其等效刚度 $\mathbf{C}_R = \mathbf{S}_R^{-1}$ 是各相刚度的[调和平均](@entry_id:750175)。对于两相[复合材料](@entry_id:139856)的[杨氏模量](@entry_id:140430)，这简化为**反混合律**：

$$
\frac{1}{E_R} = \frac{v_1}{E_1} + \frac{v_2}{E_2} \quad \text{或} \quad E_R = \left( \frac{v_1}{E_1} + \frac{v_2}{E_2} \right)^{-1}
$$

Reuss模型通常会低估材料的实际刚度，它构成了等效模量的一个**下界**。这种[等应力](@entry_id:204402)状态在另一种层合板结构中可以近似实现，即当载荷垂直于各层铺设方向时，[静力平衡](@entry_id:163498)要求每层的应力都等于施加的宏观应力 [@problem_id:2519195]。

对于任意微观结构的[复合材料](@entry_id:139856)，其真实的等效模量 $E_{\text{eff}}$ 必然位于[Voigt和Reuss界](@entry_id:171021)限之间：$E_R \le E_{\text{eff}} \le E_V$。然而，这两个界限之间的差距可能非常大。例如，考虑一个由体积分数 $v_1=0.4$ 的硬质相（$E_1 = 210$ GPa）和 $v_2=0.6$ 的软质相（$E_2 = 3$ GPa）组成的[复合材料](@entry_id:139856)。其Voigt[上界](@entry_id:274738)为 $E_V = 85.8$ GPa，而Reuss下界仅为 $E_R \approx 4.95$ GPa [@problem_id:2662318]。如此宽泛的范围凸显了发展更精确模型的必要性。

### 各向同性[复合材料](@entry_id:139856)的更严密界限：[Hashin-Shtrikman界](@entry_id:190152)限

[Voigt-Reuss界](@entry_id:190099)限是普适的，不依赖于微观结构的几何形态。然而，如果我们知道更多关于微观结构的信息，例如它是统计上各向同性的，那么就可以推导出更严密的界限。**Hashin-Shtrikman (HS) 界限**正是这样一组界限，它们是利用[变分原理](@entry_id:198028)推导出的、对于给定[体积分数](@entry_id:756566)的两相各向同性[复合材料](@entry_id:139856)最严密的可能界限。

对于由[体积分数](@entry_id:756566)为 $f_1$ 和 $f_2$、剪切模量为 $G_1, G_2$、体积模量为 $K_1, K_2$ 的两[相组成](@entry_id:197559)的各向同性[复合材料](@entry_id:139856)，假设相1比相2更硬（$G_1 > G_2, K_1 > K_2$），其等效剪切模量 $G^*$ 的HS上下界由以下复杂公式给出 [@problem_id:2519133]：

$$
G_{\mathrm{HS,lower}} = G_2 + \frac{f_1}{\frac{1}{G_1 - G_2} + \frac{6 f_2 (K_2 + 2 G_2)}{5 G_2 (3 K_2 + 4 G_2)}}
$$

$$
G_{\mathrm{HS,upper}} = G_1 + \frac{f_2}{\frac{1}{G_2 - G_1} + \frac{6 f_1 (K_1 + 2 G_1)}{5 G_1 (3 K_1 + 4 G_1)}}
$$

这些公式虽然复杂，但它们包含了相的体积和[剪切模量](@entry_id:167228)信息，从而能提供更精确的预测。以前述[Voigt-Reuss界](@entry_id:190099)限中使用的材料为例（假设 $G_1 = 30$ GPa, $K_1 = 45$ GPa; $G_2 = 1.3$ GPa, $K_2 = 3.5$ GPa; $f_1=0.4$），[Voigt-Reuss界](@entry_id:190099)限给出的[剪切模量](@entry_id:167228)范围是 $[2.11, 12.78]$ GPa。而[Hashin-Shtrikman界](@entry_id:190152)限则给出了一个显著收紧的范围：$[2.90, 8.76]$ GPa [@problem_id:2519133]。这清楚地表明，包含更多微观结构信息的模型能极大地提高预测的准确性。

### [Eshelby夹杂问题](@entry_id:187523)：高级模型的基石

为了超越界限模型并获得对等效性能的单一估计值，[微观力学](@entry_id:195009)领域引入了更复杂的“平均场”方法。这些方法几乎都建立在J.D. Eshelby于1957年解决的一个经典问题之上——无限大弹性介质中的单个椭球夾杂问题。

Eshelby的理论探讨了一个占据椭球区域 $V$ 的夹杂，该夹杂相对于周围的无限大基体经历了一个均匀的**固有应变**（或称**[本征应变](@entry_id:198120)**）$\boldsymbol{\varepsilon}^*$。这种应变可以想象成由[热膨胀](@entry_id:137427)、[相变](@entry_id:147324)或塑性变形引起。Eshelby最非凡的发现是：对于一个椭球形的夹杂，由均匀固有应变 $\boldsymbol{\varepsilon}^*$ 在夹杂内部引起的[弹性应变](@entry_id:189634)（称为**约束应变**）也是**均匀的** [@problem_id:2662327]。

这个结果可以用一个[四阶张量](@entry_id:181350)——**[Eshelby张量](@entry_id:186614)** $\mathbb{S}$——来表示，它将约束应变 $\boldsymbol{\varepsilon}^{\text{in}}$ 与固有应变 $\boldsymbol{\varepsilon}^*$ 联系起来：

$$
\boldsymbol{\varepsilon}^{\text{in}} = \mathbb{S} : \boldsymbol{\varepsilon}^*
$$

[Eshelby张量](@entry_id:186614) $\mathbb{S}$ 具有一些重要的性质：对于各向同性基体，它仅依赖于基体的[泊松比](@entry_id:158876) $\nu$ 和夹杂的几何形状（即椭球的轴比），而与基体的其他[弹性常数](@entry_id:146207)（如杨氏模量或[剪切模量](@entry_id:167228)）以及夹杂本身的材料属性无关。$\mathbb{S}$ 的对称性由椭球的形状决定：对于一般椭球是[正交各向异性](@entry_id:196967)，对于旋转椭球（如问题[@problem_id:2662327]中讨论的[长椭球](@entry_id:176438)）是横观各向同性，对于球体则是完全各向同性。

Eshelby的解可以进一步推广到“非均质夹杂”问题，即夹杂与基体具有不同的弹性常数，并且整个系统受到[远场](@entry_id:269288)均匀应变 $\boldsymbol{E}$ 的作用。在这种情况下，夹杂内部的应变 $\langle\boldsymbol{\varepsilon}\rangle_i$ 仍然是均匀的，并且与远场应变 $\boldsymbol{E}$ 之间存在一个线性关系，这个关系由所谓的**[应变集中](@entry_id:187026)张量** $\boldsymbol{A}$ 描述。Eshelby的理论为计算这个张量提供了精确的方法，从而为构建更真实的[复合材料](@entry_id:139856)模型奠定了基础。

### 平均场均质化方案

[平均场方法](@entry_id:141668)通过对夹杂物之间的相互作用做出某种平均化的假设，从而给出了等效性能的单一估计值。

#### [Mori-Tanaka方案](@entry_id:186339)

Mori-Tanaka (MT) 方法是一种非常流行且有效的平均场模型。其核心思想是，将每个夹杂物视为一个孤立的Eshelby问题，但它所感受到的“远场”应变并不是宏观平均应变 $\overline{\boldsymbol{\varepsilon}}$，而是**基体相中的平均应变** $\langle \boldsymbol{\varepsilon} \rangle_m$ [@problem_id:2662340]。这个假设巧妙地考虑了周围其他夹杂物对基[体应变](@entry_id:267252)场产生的扰动，从而间接地考虑了夹杂物之间的相互作用。

基于这个假设，即 $\langle \boldsymbol{\varepsilon} \rangle_i = \boldsymbol{A}_i^{\text{dil}} : \langle \boldsymbol{\varepsilon} \rangle_m$（其中 $\boldsymbol{A}_i^{\text{dil}}$ 是单个夹杂在无限大基体中的稀疏浓度张量），并结合平均应变和[平均应力](@entry_id:751819)的定义，可以推导出Mori-Tanaka的等效[刚度张量](@entry_id:176588) $\boldsymbol{C}^{\text{MT}}$ 的表达式 [@problem_id:2662340]：

$$
\boldsymbol{C}^{\text{MT}} = \Big(c_m \boldsymbol{C}_m + c_i \boldsymbol{C}_i : \boldsymbol{A}_i^{\text{dil}}\Big) : \big(c_m \boldsymbol{I} + c_i \boldsymbol{A}_i^{\text{dil}}\big)^{-1}
$$

其中 $c_m, c_i$ 是体积分数，$\boldsymbol{C}_m, \boldsymbol{C}_i$ 是[刚度张量](@entry_id:176588)，$\boldsymbol{I}$ 是四阶单位张量。MT模型特别适用于具有明确连续基体相和弥散增强相的[复合材料](@entry_id:139856)，尤其是在中低浓度范围内。

#### 自洽方案

自洽 (Self-Consistent, SC) 方案采用了另一种不同的物理图像。它不区分基体和夹杂，而是将每一相的颗粒都同等对待。其核心假设是：将每一相的颗粒视为一个单独的[Eshelby夹杂问题](@entry_id:187523)，但它嵌入的介质不是某个特定的基体相，而是**未知的等效介质本身**，其刚度为 $\mathbb{C}^*$ [@problem_id:2519188]。

这个假设导出了一个自洽条件：用于计算夹杂应变的假想宿主介质的性能，必须与最终计算出的[复合材料](@entry_id:139856)整体等效性能相一致。这形成了一个关于未知等效刚度 $\mathbb{C}^*$ 的隐式[不动点方程](@entry_id:203270)。对于一个N相[复合材料](@entry_id:139856)，该方程可以写作：

$$
\mathbb{C}^* = \sum_{r=1}^N c_r \, \mathbb{C}_r : \mathbb{A}_r(\mathbb{C}^*)
$$

其中，[应变集中](@entry_id:187026)张量 $\mathbb{A}_r(\mathbb{C}^*)$ 是通过Eshelby理论计算得出的，但它本身依赖于未知的 $\mathbb{C}^*$：

$$
\mathbb{A}_r(\mathbb{C}^*) = \big[\mathbb{I} + \mathbb{S}_r(\mathbb{C}^*) : (\mathbb{C}^*)^{-1} : (\mathbb{C}_r - \mathbb{C}^*)\big]^{-1}
$$

其中 $\mathbb{S}_r(\mathbb{C}^*)$ 是在刚度为 $\mathbb{C}^*$ 的宿主介质中，形状为 $r$ 的夹杂的[Eshelby张量](@entry_id:186614)。求解这个[不动点方程](@entry_id:203270)即可得到自洽模型的预测值。自洽方案由于其对称地处理所有相，因此特别适用于多晶体材料或各相浓度都很高、没有明显基体相的[复合材料](@entry_id:139856)。

### 在各向异性和短纤维[复合材料](@entry_id:139856)中的应用

上述原理和模型可以应用于更具体的[复合材料](@entry_id:139856)体系，例如工程中常见的[纤维增强复合材料](@entry_id:194995)。

#### [Halpin-Tsai方程](@entry_id:191532)

对于由连续纤维单向[排列](@entry_id:136432)（UD）组成的[复合材料](@entry_id:139856)，其[力学性能](@entry_id:201145)是高度各向异性的。虽然沿纤维方向的模量（$E_1$）可以很好地通过简单的混合律估算，但[横向模量](@entry_id:191863)（$E_2$）和面内[剪切模量](@entry_id:167228)（$G_{12}$）的预测则要复杂得多。

**[Halpin-Tsai方程](@entry_id:191532)**是一组广受欢迎的半经验公式，用于估算这些性能。它们的形式被巧妙地设计成可以在[Voigt和Reuss界](@entry_id:171021)限之间进行插值。对于某个模量 $P$（例如 $E_2$ 或 $G_{12}$），其通用形式为 [@problem_id:2662360]：

$$
\frac{P}{P_m} = \frac{1 + \xi \eta V_f}{1 - \eta V_f} \quad \text{其中} \quad \eta = \frac{P_f/P_m - 1}{P_f/P_m + \xi}
$$

这里的关键是一个无量纲的**几何参数** $\xi$。这个参数并非材料常数，而是用来描述增强体几何形状（如纤维[截面](@entry_id:154995)形状、短纤维的长径比）和排布方式（如方形或六方[排列](@entry_id:136432)）对刚度的影响。通过调整 $\xi$ 的值，[Halpin-Tsai方程](@entry_id:191532)可以拟合实验数据或更精确的[微观力学](@entry_id:195009)模型的解。例如，对于圆形[截面](@entry_id:154995)的连续纤维，通常取 $\xi \approx 2$ 来估算 $E_2$，取 $\xi \approx 1$ 来估算 $G_{12}$。

#### 短纤维[复合材料](@entry_id:139856)的取向平均

许多[复合材料](@entry_id:139856)（如[注塑成型](@entry_id:161178)的短纤维[复合材料](@entry_id:139856)）中的增强体并非完美对齐，而是遵循一定的取向[分布](@entry_id:182848)。为了在这种情况下预测等效性能，我们需要对单个纤维的贡献在所有可能的取向上进行平均。

这一过程的核心是**[取向分布函数](@entry_id:191240) (Orientation Distribution Function, ODF)** $\psi(\mathbf{n})$，它是一个定义在单位[球面上的概率](@entry_id:272145)密度函数，描述了纤维轴向 $\mathbf{n}$ 指向某个方向的概率。根据概率的定义，它必须满足 $\psi(\mathbf{n}) \ge 0$ 和 $\int_{S^2} \psi(\mathbf{n}) d\Omega = 1$ [@problem_id:2519172]。

纤维取向的统计信息通常通过**取向张量**来概括，它们是[方向向量](@entry_id:169562) $\mathbf{n}$ 的分量对ODF加权的矩。最重要的包括：

- **二阶取向张量**: $a_{ij} = \langle n_i n_j \rangle = \int_{S^2} n_i n_j \psi(\mathbf{n}) d\Omega$
- **四阶取向张量**: $A_{ijkl} = \langle n_i n_j n_k n_l \rangle = \int_{S^2} n_i n_j n_k n_l \psi(\mathbf{n}) d\Omega$

二阶张量 $a_{ij}$ 是对称的，且其迹恒为1 ($a_{ii}=1$)。对于完全随机的3D取向（各向同性），$a_{ij} = \frac{1}{3}\delta_{ij}$；对于在$x$-$y$平面内随机的2D取向，$a_{ij} = \mathrm{diag}(\frac{1}{2}, \frac{1}{2}, 0)$ [@problem_id:2519172]。

在进行刚度平均时，一个至关重要的问题出现了。因为刚度是一个[四阶张量](@entry_id:181350)，其在不同[坐标系](@entry_id:156346)下的转换涉及四个[方向余弦](@entry_id:170591)的乘积，所以对[刚度张量](@entry_id:176588)的取向平均严格来说需要**四阶取向张量** $A_{ijkl}$。然而，实验上测量$A_{ijkl}$非常困难，而二阶张量 $a_{ij}$ 则相对容易获得。因此，一个核心的挑战是找到一种从已知的 $a_{ij}$ 估算未知的 $A_{ijkl}$ 的方法。这种方法被称为**闭合近似 (closure approximation)**。需要强调的是，不存在一个对所有取向[分布](@entry_id:182848)都精确的简单闭合关系。例如，常见的二次闭合近似 $A_{ijkl} \approx a_{ij} a_{kl}$ 只是一个近似，对于许多[分布](@entry_id:182848)（如各向同性）其误差很大 [@problem_id:2519172]。发展更精确的闭合近似是短纤维[复合材料建模](@entry_id:747578)领域一个持续活跃的研究方向。