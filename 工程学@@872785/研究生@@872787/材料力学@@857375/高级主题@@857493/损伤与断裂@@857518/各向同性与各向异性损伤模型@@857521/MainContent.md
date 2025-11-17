## 引言
材料在服役过程中，由于微裂纹、微孔洞的萌生与扩展，其[力学性能](@entry_id:201145)会逐渐退化，最终导致结构失效。[连续介质损伤力学](@entry_id:177438)（Continuum Damage Mechanics, CDM）为定量描述这一从微观缺陷累积到宏观性能衰退的全过程提供了一个强大的理论框架。准确地模拟材料的[损伤演化](@entry_id:184965)对于现代工程结构的设计、寿命预测和安全性评估至关重要。然而，如何构建一个既能反映复杂物理机制，又在数学上严谨、在应用上可行的模型，始终是力学研究的核心挑战。

本文旨在系统性地解决这一问题，为读者构建一个关于各向同性和[各向异性损伤模型](@entry_id:190894)的完整知识体系。我们将从最基本的物理概念出发，逐步深入到复杂的本构理论和前沿应用。通过本文的学习，你将掌握：

*   **第一章：原理与机制** 将深入剖析[损伤力学](@entry_id:178377)的核心原理。我们将从定义关键的[有效应力概念](@entry_id:196960)开始，建立一个严格的不可逆过程[热力学](@entry_id:141121)框架，并在此基础上详细推导[各向同性损伤模型](@entry_id:198443)的本构关系与演化规律。最后，本章将揭示标量损伤模型的局限性，并阐明为何以及如何向更复杂的[各向异性张量](@entry_id:746467)损伤模型过渡。

*   **第二章：应用与交叉学科联系** 将展示[损伤力学](@entry_id:178377)理论如何在实际问题中发挥作用。我们将探讨损伤模型如何用于表征材料的[非线性](@entry_id:637147)行为、处理[复合材料](@entry_id:139856)的各向异性、与塑性等其他不[可逆机](@entry_id:145128)制耦合，以及在[断裂模拟](@entry_id:199069)和[无损检测](@entry_id:273209)等领域的应用，从而连接理论与工程实践。

*   **第三章：动手实践** 将提供一系列精心设计的计算练习。通过解决这些问题，你将有机会亲手应用前两章学到的理论，加深对模型构建、参数影响和物理内涵的理解。

本文将引导你从[损伤力学](@entry_id:178377)的基本公理出发，最终能够理解并初步应用这些先进的工具来分析复杂的[材料失效](@entry_id:160997)问题。

## 原理与机制

本章旨在系统阐述[连续介质损伤力学](@entry_id:177438)的核心原理与本构模型。我们将从损伤的物理直观概念出发，逐步构建一个严格的[热力学](@entry_id:141121)框架，并在此基础上详细探讨各向同性和[各向异性损伤模型](@entry_id:190894)的数学表述与内在机制。

### [损伤力学](@entry_id:178377)的基础概念：[有效应力](@entry_id:198048)

在工程实践中，材料在加载过程中会产生微裂纹、微孔洞等缺陷。这些微观缺陷的萌生与扩展，会削弱材料的承载能力。[连续介质损伤力学](@entry_id:177438)的核心思想，便是在宏观连续介质的框架内，通过引入一个或多个内部状态变量来量化这种由微观缺陷引起的材料性能退化。

最基本、最直观的损伤模型源于 Kachanov 的思想，即损伤表现为有效承载面积的减少。考虑一个初始[横截面](@entry_id:154995)积为 $A_0$ 的杆件，承受单轴拉力 $F$。由于微观缺陷的存在，实际传递载荷的[有效面积](@entry_id:197911) $A_{\mathrm{eff}}$ 小于初始面积 $A_0$。我们可以将所有微观缺陷的总面积记为 $A_D$，则 $A_{\mathrm{eff}} = A_0 - A_D$。

为了在连续介质理论中描述这种效应，我们引入一个无量纲的**[标量损伤变量](@entry_id:196275)** $d$，其定义为缺陷面积与初始面积之比：

$$
d = \frac{A_D}{A_0}
$$

根据其物理意义，$d$ 的取值范围为 $[0, 1)$。$d=0$ 表示材料完好无损，$A_{\mathrm{eff}} = A_0$。随着损伤累积，$d$ 逐渐增大。当 $d \to 1$ 时，有效承载面积趋于零，材料发生宏观断裂。

基于[损伤变量](@entry_id:197066) $d$ 的定义，有效承载面积可以表示为 $A_{\mathrm{eff}} = A_0(1-d)$。现在我们可以区分两种应力定义：

1.  **名义应力 (Nominal Stress)** $\sigma$：定义为作用力 $F$ 除以初始[横截面](@entry_id:154995)积 $A_0$，即 $\sigma = F/A_0$。这是工程中易于测量的宏观应力。

2.  **[有效应力](@entry_id:198048) (Effective Stress)** $\tilde{\sigma}$：定义为作用力 $F$ 除以实际承载的有效[横截面](@entry_id:154995)积 $A_{\mathrm{eff}}$，即 $\tilde{\sigma} = F/A_{\mathrm{eff}}$。有效应力反映了材料未损伤部分所承受的真实应力水平。

通过联立以上定义，我们可以轻松推导出名义应力与[有效应力](@entry_id:198048)之间的基本关系 [@problem_id:2895663]。将 $F = \sigma A_0$ 和 $A_{\mathrm{eff}} = A_0(1-d)$ 代入[有效应力](@entry_id:198048)的定义中，可得：

$$
\tilde{\sigma} = \frac{\sigma A_0}{A_0(1-d)} = \frac{\sigma}{1-d}
$$

这个关系式是[各向同性损伤](@entry_id:750875)力学的基石。它表明，对于任何非零损伤 ($d > 0$)，有效应力总是大于名义应力。随着损伤的增长，$d$ 趋近于 $1$，即使在一个很小的名义应力下，[有效应力](@entry_id:198048)也会急剧增大，最终导致材料的失效。有效应力的概念至关重要，因为它被认为是驱动[材料变形](@entry_id:169356)、塑性流动和进一步[损伤演化](@entry_id:184965)的真正物理量。

### 各向同性[损伤的[热力学]](@entry_id:188411)(@entry_id:141121)框架

为了确保损伤模型的物理合理性，必须将其置于不可逆过程[热力学](@entry_id:141121)的框架内。这要求模型的建立满足[热力学](@entry_id:141121)第一和第二定律。

#### 热力学定律与内部变量

对于[等温过程](@entry_id:143096)，热力学第二定律的局部形式，即**克劳修斯-杜亥姆不等式 (Clausius-Duhem Inequality, CDI)**，要求材料内部的能量耗散率 $\mathcal{D}$ 必须非负。耗散率定义为[应力功率](@entry_id:182907)密度与材料储存的自由能变化率之差：

$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0
$$

这里，$\boldsymbol{\sigma}$ 是柯西应力张量，$\boldsymbol{\varepsilon}$ 是[小应变张量](@entry_id:754968)，$\psi$ 是单位体积的**[亥姆霍兹自由能](@entry_id:136442) (Helmholtz Free Energy)**，冒号“$:$”表示张量的[双点积](@entry_id:748648)，上标点“$\dot{\_}$”表示对时间的[物质导数](@entry_id:172646)。

在[损伤力学](@entry_id:178377)中，[亥姆霍兹自由能](@entry_id:136442)被视为一个状态函数，它不仅依赖于[宏观可观测量](@entry_id:751601)（如应变 $\boldsymbol{\varepsilon}$），还依赖于描述材料内部微观结构的内部状态变量。对于简单的[各向同性损伤](@entry_id:750875)，该内部变量就是[标量损伤变量](@entry_id:196275) $d$。因此，$\psi = \psi(\boldsymbol{\varepsilon}, d)$。

#### 本构关系与[能量耗散](@entry_id:147406)的推导

根据[链式法则](@entry_id:190743)，自由能的变化率可以展开为：

$$
\dot{\psi} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} : \dot{\boldsymbol{\varepsilon}} + \frac{\partial \psi}{\partial d} \dot{d}
$$

将此式代入克劳修斯-杜亥姆不等式，得到：

$$
\left( \boldsymbol{\sigma} - \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} \right) : \dot{\boldsymbol{\varepsilon}} - \frac{\partial \psi}{\partial d} \dot{d} \ge 0
$$

根据 Coleman-Noll 程序，该不等式必须对所有可能的[热力学过程](@entry_id:141636)都成立。这意味着对于任意的[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}$，不等式均须满足。为了保证这一点，$\dot{\boldsymbol{\varepsilon}}$ 的系数项必须为零。由此，我们得到了应力张量的超弹性本构关系：

$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}
$$

这一关系表明，对于给定的内部状态，应力完全由应变决定，并且可以从一个[势函数](@entry_id:176105)（亥姆霍兹自由能）中导出。将此应力表达式代回不等式，与应变相关的项便消失了，剩下的部分完全归因于内部变量的演化所产生的耗散 [@problem_id:2895652]：

$$
\mathcal{D}_d = - \frac{\partial \psi}{\partial d} \dot{d} \ge 0
$$

这部分耗散即为**损伤耗散**。为了方便分析，我们定义一个与[损伤变量](@entry_id:197066) $d$ [热力学](@entry_id:141121)共轭的力，称为**[损伤能量释放率](@entry_id:195626) (Damage Energy Release Rate)** 或损伤驱动力，记为 $Y$：

$$
Y = - \frac{\partial \psi}{\partial d}
$$

这样，损伤[耗散不等式](@entry_id:188634)就可以简洁地写为 $\mathcal{D}_d = Y \dot{d} \ge 0$。由于损伤是一个不可逆过程，其速率必须非负，即 $\dot{d} \ge 0$。因此，为了满足[热力学第二定律](@entry_id:142732)，[损伤能量释放率](@entry_id:195626) $Y$ 也必须是非负的。这一条件 ($Y \ge 0$) 为我们构建合理的[自由能函数](@entry_id:749582)提供了重要的约束。

### [各向同性损伤](@entry_id:750875)的[本构模型](@entry_id:174726)

[热力学](@entry_id:141121)框架为我们提供了推导本构关系的[一般性](@entry_id:161765)方法，但并未指明亥姆霍兹自由能 $\psi(\boldsymbol{\varepsilon}, d)$ 的具体形式。选择合适的[自由能函数](@entry_id:749582)是建立具体损伤模型的关键。

#### 自由能形式与关键假设

对于初始为线弹性的材料，其未损伤时的自由能密度为 $\psi_0(\boldsymbol{\varepsilon}) = \frac{1}{2} \boldsymbol{\varepsilon} : \mathbb{C}_0 : \boldsymbol{\varepsilon}$，其中 $\mathbb{C}_0$ 是材料初始的四阶[弹性刚度张量](@entry_id:170728)。为了构建受损材料的自由能 $\psi(\boldsymbol{\varepsilon}, d)$，学术界提出了几个核心假设。

**[应变等效](@entry_id:186173)性假设 (Strain Equivalence Hypothesis)** 是 Lemaitre 模型的基础。该假设认为，受损材料的[本构关系](@entry_id:186508)与未损伤材料的本构关系具有相同的形式，只需将名义应力替换为有效应力即可。这一假设可以直接通过构建[自由能函数](@entry_id:749582)来实现 [@problem_id:2895543] [@problem_id:2897256]。一个普遍采用且满足[热力学](@entry_id:141121)要求的形式是：

$$
\psi(\boldsymbol{\varepsilon}, d) = (1-d) \psi_0(\boldsymbol{\varepsilon}) = \frac{1}{2} (1-d) \boldsymbol{\varepsilon} : \mathbb{C}_0 : \boldsymbol{\varepsilon}
$$

根据 $\boldsymbol{\sigma} = \partial \psi / \partial \boldsymbol{\varepsilon}$，我们可以导出受损材料的[应力-应变关系](@entry_id:274093)：

$$
\boldsymbol{\sigma} = (1-d) \mathbb{C}_0 : \boldsymbol{\varepsilon}
$$

这表明，损伤的宏观效应体现为材料整体刚度的退化，有效[刚度张量](@entry_id:176588)为 $\mathbb{C}(d) = (1-d) \mathbb{C}_0$。该关系式与之前基于面积缩减概念推导的[有效应力](@entry_id:198048)公式 $\tilde{\boldsymbol{\sigma}} = \boldsymbol{\sigma} / (1-d)$ 完全自洽，因为 $\boldsymbol{\sigma} / (1-d) = \mathbb{C}_0 : \boldsymbol{\varepsilon}$，这恰好是未损伤材料在有效应力 $\tilde{\boldsymbol{\sigma}}$ 下的[本构方程](@entry_id:138559)。

与[应变等效](@entry_id:186173)性假设并行的是**能量等效性假设 (Energy Equivalence Hypothesis)**，由 Sidoroff 提出。该假设主张，受损材料的弹性应变能等于未损伤材料在[有效应力](@entry_id:198048)下的弹性应变能。这两个假设虽然在哲学思想上相似，但在数学上会导致不同的[刚度退化](@entry_id:202277)形式 [@problem_id:2895685]。
- 基于**[应变等效](@entry_id:186173)性**，我们得到 $\mathbb{C}(d) = (1-d) \mathbb{C}_0$。
- 基于**能量等效性**，可以推导出 $\mathbb{C}(d) = (1-d)^2 \mathbb{C}_0$。

这种差异凸显了[损伤力学](@entry_id:178377)中模型假设选择的重要性，不同的假设将导致模型预测能力的差异。在许多应用中，基于[应变等效](@entry_id:186173)性的线性退化模型 $(1-d)$ 因其简洁性和物理直观性而被广泛采用。

#### 损伤驱动力的表达式

确定了自由能的形式后，我们便可以计算[损伤能量释放率](@entry_id:195626) $Y$。对于基于[应变等效](@entry_id:186173)性的标准模型 $\psi = \frac{1}{2} (1-d) \boldsymbol{\varepsilon} : \mathbb{C}_0 : \boldsymbol{\varepsilon}$，我们有 [@problem_id:2895543] [@problem_id:2895665]：

$$
Y = - \frac{\partial \psi}{\partial d} = - \frac{\partial}{\partial d} \left( \frac{1}{2} (1-d) \boldsymbol{\varepsilon} : \mathbb{C}_0 : \boldsymbol{\varepsilon} \right) = \frac{1}{2} \boldsymbol{\varepsilon} : \mathbb{C}_0 : \boldsymbol{\varepsilon}
$$

这个结果非常值得注意：对于该模型，[损伤能量释放率](@entry_id:195626) $Y$ 恰好等于在相同应变 $\boldsymbol{\varepsilon}$ 下，**虚拟的未损伤材料**所储存的[应变能密度](@entry_id:200085) $\psi_0(\boldsymbol{\varepsilon})$，并且它不依赖于当前的损伤水平 $d$。

在某些情况下，将 $Y$ 表示为应力 $\boldsymbol{\sigma}$ 的函数会更加方便。利用本构关系 $\boldsymbol{\varepsilon} = \mathbb{S}(d) : \boldsymbol{\sigma} = \frac{1}{1-d} \mathbb{S}_0 : \boldsymbol{\sigma}$（其中 $\mathbb{S}_0 = \mathbb{C}_0^{-1}$ 是初始柔度张量），我们可以进行[变量替换](@entry_id:141386) [@problem_id:2895605]：

$$
Y = \frac{1}{2} \left( \frac{1}{1-d} \mathbb{S}_0 : \boldsymbol{\sigma} \right) : \mathbb{C}_0 : \left( \frac{1}{1-d} \mathbb{S}_0 : \boldsymbol{\sigma} \right) = \frac{1}{2(1-d)^2} \boldsymbol{\sigma} : \mathbb{S}_0 : \mathbb{C}_0 : \mathbb{S}_0 : \boldsymbol{\sigma} = \frac{1}{2(1-d)^2} \boldsymbol{\sigma} : \mathbb{S}_0 : \boldsymbol{\sigma}
$$

这两种等价的表达式（一个以应变为变量，一个以应力为变量）为理论分析和数值实现提供了灵活性。例如，在给定的三维应变状态下（如 [@problem_id:2895665] 中所示的算例），通过计算材料的拉梅参数 $\lambda$ 和 $\mu$，并代入公式 $Y = \psi_0(\boldsymbol{\varepsilon}) = \frac{1}{2}\lambda(\operatorname{tr}\boldsymbol{\varepsilon})^2 + \mu(\boldsymbol{\varepsilon}:\boldsymbol{\varepsilon})$，我们可以精确地求出该状态下的[损伤能量释放率](@entry_id:195626)数值。

#### [损伤演化](@entry_id:184965)律

我们已经确定了驱动损伤的“力” $Y$，但尚未规定[损伤变量](@entry_id:197066) $d$ 如何随加载历史而“动”。这就需要一个**[损伤演化](@entry_id:184965)律**。对于率无关材料，这一规律通常通过定义一个**损伤面 (Damage Surface)** 来描述，这与塑性力学中的屈服面概念类似。

损伤面定义了一个弹性区域，当材料状态位于该区域内部时，损伤不发展。[损伤演化](@entry_id:184965)仅当材料状态点达到并试图穿越损伤面时才会发生。一个典型的损伤面函数可以写成：

$$
f(Y, \kappa) = Y - Y_c(\kappa) \le 0
$$

其中，$\kappa$ 是一个代表累积损伤效应的历史变量（有时直接取为[损伤变量](@entry_id:197066) $d$），$Y_c(\kappa)$ 是当前的损伤阈值。当 $Y  Y_c(\kappa)$ 时，材料处于弹性状态，损伤不增长。当 $Y = Y_c(\kappa)$ 时，材料达到[损伤演化](@entry_id:184965)条件。损伤阈值 $Y_c(\kappa)$ 通常是历史变量 $\kappa$ 的增函数，以描述**损伤硬化**现象，即随着损伤的累积，需要更大的[能量释放率](@entry_id:158357)才能驱动其进一步发展。例如，可以采用[线性硬化模型](@entry_id:180941) $Y_c(\kappa) = Y_0(1+\eta\kappa)$，其中 $Y_0$ 是初始损伤阈值，$\eta$ 是[硬化](@entry_id:177483)参数 [@problem_id:2895662]。

率无关的[损伤演化](@entry_id:184965)过程可以用一组**加载/卸载条件**（或称 Kuhn-Tucker [互补条件](@entry_id:747558)）来精确描述：

$$
f(Y, \kappa) \le 0, \quad \dot{\lambda} \ge 0, \quad \dot{\lambda} f(Y, \kappa) = 0
$$

这里，$\dot{\lambda}$ 是一个非负的**一致性参数率**（或损伤乘子）。这些条件意味着：(1) 材料状态点永远不能超出损伤面；(2) [损伤演化](@entry_id:184965)是不可逆的；(3) 只有当状态点在损伤面上时（$f=0$），才可能发生[损伤演化](@entry_id:184965)（$\dot{\lambda}>0$）。

在加载过程中（即 $\dot{\lambda} > 0$），状态点必须始终保持在演化中的损伤面上，这要求损伤面函数的时间导数必须为零，即**一致性条件** $\dot{f}=0$。通过对 $f(Y, \kappa) = 0$ 求导，并结合关联流动法则（例如，$\dot{\kappa} = \dot{\lambda}$），我们可以求解出一致性参数率。对于上述[线性硬化模型](@entry_id:180941)，[一致性条件](@entry_id:637057)为：

$$
\dot{f} = \dot{Y} - \frac{dY_c}{d\kappa}\dot{\kappa} = \dot{Y} - Y_0\eta\dot{\lambda} = 0
$$

解得 $\dot{\lambda} = \dot{Y} / (Y_0\eta)$ [@problem_id:2895662]。这个方程将损伤的演化速率与损伤驱动力的加载速率直接联系起来，从而完整地定义了损伤的[演化过程](@entry_id:175749)。

### 向[各向异性损伤](@entry_id:199086)的过渡

尽管标量损伤模型在描述许多材料（如金属在单调拉伸下的[延性损伤](@entry_id:198998)）的行为时非常有效，但其内在的各向同性假设限制了其应用范围。

#### 标量损伤模型的局限性

许多工程材料，如[纤维增强复合材料](@entry_id:194995)、轧制金属板、甚至木材，其损伤行为具有显著的[方向性](@entry_id:266095)。例如，[单向复合材料](@entry_id:196178)沿纤维方向的[损伤演化](@entry_id:184965)规律与其垂直方向截然不同。当材料的初始状态是各向同性的，但损伤的累积使其呈现出方向相关的性能退化时，我们就称之为**损伤诱导的各向异性**。

[标量损伤变量](@entry_id:196275) $d$ 无法描述这种现象 [@problem_id:2873730]。因为在模型 $\mathbb{C}(d) = (1-d)\mathbb{C}_0$ 中，标量因子 $(1-d)$ 等比例地缩放了初始[刚度张量](@entry_id:176588) $\mathbb{C}_0$ 的所有分量。如果材料初始是各向同性的，那么退化后的[刚度张量](@entry_id:176588) $\mathbb{C}(d)$ 仍然是各向同性的。它无法描述材料在某个[方向比](@entry_id:166826)另一个方向“更”受损的情况。

#### [各向异性损伤](@entry_id:199086)的张量描述

为了克服这一局限性，必须引入具有方向信息的张量作为[损伤变量](@entry_id:197066)。最直接的推广是使用一个**二阶[对称张量](@entry_id:148092)** $\mathbf{D}$ 来描述损伤状态。
- 该张量的**[特征向量](@entry_id:151813)**（[主方向](@entry_id:276187)）可以定义为损伤的三个主要方向。
- 其对应的**[特征值](@entry_id:154894)** $D_1, D_2, D_3$（$0 \le D_\alpha  1$）则量化了沿各自主要方向的损伤程度。

通过二阶损伤张量 $\mathbf{D}$，我们可以构建各向异性的[刚度退化](@entry_id:202277)模型。一种常见的方法是，通过一个由 $\mathbf{D}$ 构造的**损伤效应张量**（或称为完整性张量，如 $\mathbf{A} = \mathbf{I}-\mathbf{D}$），将名义[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 映射到一个有效[应变张量](@entry_id:193332) $\tilde{\boldsymbol{\varepsilon}}$，然后再代入未损伤的[本构关系](@entry_id:186508)中 [@problem_id:2873730]。例如，可以定义 $\tilde{\boldsymbol{\varepsilon}} = \frac{1}{2}(\mathbf{A}\boldsymbol{\varepsilon}\mathbf{A}^T + \mathbf{A}^T\boldsymbol{\varepsilon}\mathbf{A})$，则受损应力为 $\boldsymbol{\sigma} = \mathbb{C}_0 : \tilde{\boldsymbol{\varepsilon}}$。当 $\mathbf{D}$ 的[特征值](@entry_id:154894)不相等时，这种构造将导致有效的[刚度张量](@entry_id:176588)呈现出各向异性（例如，从初始各向同性演变为[正交各向异性](@entry_id:196967)），从而能够捕捉到方向依赖的[刚度退化](@entry_id:202277)。

#### 各向异性模型的对称性考量

引入[张量损伤变量](@entry_id:195924)虽然能够描述更复杂的物理现象，但也大大增加了模型的复杂性。更一般地，人们甚至可以引入一个**四阶损伤张量** $\mathbb{D}$，它直接作用于柔度或[刚度张量](@entry_id:176588)，例如 $\mathbb{S}_{\mathrm{dam}} = (\mathbb{I}+\mathbb{D}):\mathbb{S}_0:(\mathbb{I}+\mathbb{D})^\star$。

这些[高阶张量](@entry_id:200122)必须满足特定的对称性要求。首先是源于弹性理论的内在对称性，包括次对称性（$D_{ijkl} = D_{jikl} = D_{ijlk}$）和主对称性（$D_{ijkl} = D_{klij}$）。一个满足这些对称性的[四阶张量](@entry_id:181350)在三维空间中最多有 $21$ 个独立分量。

此外，损伤张量还必须遵循材料本身的**[材料对称性](@entry_id:190289)**。例如，如果材料具有[正交各向异性](@entry_id:196967)对称性，那么损伤张量 $\mathbb{D}$ 的分量在描述该对称性的坐标变换下必须保持不变。可以证明，施加[正交各向异性](@entry_id:196967)对称性约束后，满足上述内在对称性的[四阶张量](@entry_id:181350) $\mathbb{D}$ 的独立分量数量将从 $21$ 个减少到 $9$ 个 [@problem_id:2895555]。这与[正交各向异性弹性](@entry_id:178993)张量的独立分量数目相同。这一结论深刻地揭示了本构理论中物理对称性与数学结构之间的内在联系，也为复杂[各向异性损伤模型](@entry_id:190894)的参数标定提供了理论指导。