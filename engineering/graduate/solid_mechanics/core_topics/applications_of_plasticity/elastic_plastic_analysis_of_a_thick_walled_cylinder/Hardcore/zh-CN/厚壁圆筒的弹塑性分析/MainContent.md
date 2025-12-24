## 引言
[厚壁圆筒](@entry_id:189222)作为高压容器、管道和炮管等关键工程结构的核心部件，其在极端载荷下的力学行为直接关系到系统的安全与可靠性。传统的纯弹性设计方法往往过于保守，未能充分利用材料的承载潜力。为了实现更经济、更可靠的设计，并理解结构在超载下的[失效机制](@entry_id:184047)，深入研究其从弹性到塑性的完整响应过程至关重要。本文旨在填补基础理论与复杂工程应用之间的鸿沟，系统性地建立[厚壁圆筒](@entry_id:189222)[弹塑性分析](@entry_id:181788)的知识体系。

读者将首先在 **“原理与机制”** 一章中，掌握控制[弹塑性](@entry_id:193198)行为的基本方程、屈服准则和[塑性流动法则](@entry_id:189597)。随后，在 **“应用与跨学科交叉”** 一章中，我们将探索这些理论如何在[压力容器设计](@entry_id:184353)、自增强技术、热-力耦合乃至岩土工程等领域中得到应用和扩展。最后，通过 **“动手实践”** 部分，将理论知识与具体的计算问题相结合，巩固理解。这种从理论基础到应用实践的结构，将引导您逐步构建解决复杂[弹塑性](@entry_id:193198)边值问题的能力。

## 原理与机制

本章旨在系统地阐述[厚壁圆筒](@entry_id:189222)[弹塑性分析](@entry_id:181788)所依据的基本物理原理和力学机制。我们将从弹性力学的基础出发，逐步引入塑性力学的核心概念，包括[屈服准则](@entry_id:193897)、流动法则以及硬化模型。通过将这些理论构建模块化，我们最终将能够完整地建立一个描述部分塑性化圆筒的复杂[边值问题](@entry_id:193901)。

### 轴对称弹性的基本原理

在材料进入塑性状态之前，其行为遵循弹性力学的规律。对于[厚壁圆筒](@entry_id:189222)这类轴对称问题，其弹性响应是后续[弹塑性分析](@entry_id:181788)的基石。

#### [柱坐标系](@entry_id:266798)下的平衡与[运动学](@entry_id:173318)

我们首先考虑一个静态、轴对称的[厚壁圆筒](@entry_id:189222)，其受力状态在[柱坐标系](@entry_id:266798) $(r, \theta, z)$ 下仅依赖于[径向坐标](@entry_id:165186) $r$。根据[连续介质力学](@entry_id:155125)中的[动量守恒](@entry_id:149964)定律，在没有[体力](@entry_id:174230)的情况下，应力分量必须满足平衡方程。对于轴对称问题，剪应力分量 $\tau_{r\theta}, \tau_{rz}, \tau_{\theta z}$ 均为零，唯一非平凡的平衡方程是径向[平衡方程](@entry_id:172166) ：
$$
\frac{d\sigma_{r}}{dr} + \frac{\sigma_{r} - \sigma_{\theta}}{r} = 0
$$
其中，$\sigma_r$ 是[径向应力](@entry_id:197086)，$\sigma_{\theta}$ 是环向（或周向）应力。这个常微分方程从根本上联系了[径向应力](@entry_id:197086)的变化率与[径向应力](@entry_id:197086)和[环向应力](@entry_id:190931)之差。直观地，它描述了一个微小的扇形体在径向上的[力平衡](@entry_id:267186)。

在[运动学](@entry_id:173318)方面，轴对称变形意味着位移场也仅有径向分量，且该分量仅是 $r$ 的函数，即 $u_r = u(r)$，$u_\theta = u_z = 0$（在更一般情况下 $u_z$ 可以是 $z$ 的函数）。在小应变假设下，应变张量的分量由位移场的梯度定义。对于这种纯径向位移，非零的应变分量为 ：
- **径向应变 (Radial Strain)**: $\varepsilon_r = \dfrac{du}{dr}$
- **[环向应变](@entry_id:174548) (Hoop Strain)**: $\varepsilon_\theta = \dfrac{u}{r}$

径向应变描述了材料沿半径方向的拉伸或压缩，而[环向应变](@entry_id:174548)则描述了圆周的伸长或缩短。这两个应变分量通过位移函数 $u(r)$ 紧密耦合。

在分析“长”圆筒问题时，通常会遇到两种重要的简化假设：**[平面应变](@entry_id:167046) (plane strain)** 和 **平面应力 (plane stress)**。
- **[平面应变](@entry_id:167046)** 假设在轴向（$z$ 方向）上没有变形，即 $\varepsilon_z = 0$。这通常适用于两端固定的长圆筒，其轴向伸长受到约束。
- **[平面应力](@entry_id:172193)** 假设在轴向上的应力为零，即 $\sigma_z = 0$。这适用于两端自由、薄壁的圆筒或管帽。
明确区分这两种状态至关重要，因为它们会导致截然不同的应力[分布](@entry_id:182848)，尤其是在塑性分析中 。

#### 弹性本构关系（[胡克定律](@entry_id:149682)）

[平衡方程](@entry_id:172166)和运动学关系必须与材料的本构行为相结合才能求解问题。对于在[线性弹性](@entry_id:166983)范围内均匀各向同性材料，[应力与应变](@entry_id:137374)的关系由**[广义胡克定律](@entry_id:203555) (Generalized Hooke's Law)** 描述。在[主应力方向](@entry_id:753737)（对于[轴对称](@entry_id:173333)圆筒即 $r, \theta, z$ 方向）上，其分量形式为 ：
$$
\varepsilon_r = \frac{1}{E} \left[ \sigma_r - \nu(\sigma_\theta + \sigma_z) \right]
$$
$$
\varepsilon_\theta = \frac{1}{E} \left[ \sigma_\theta - \nu(\sigma_r + \sigma_z) \right]
$$
$$
\varepsilon_z = \frac{1}{E} \left[ \sigma_z - \nu(\sigma_r + \sigma_\theta) \right]
$$
其中 $E$ 是**杨氏模量 (Young's Modulus)**，$\nu$ 是**泊松比 (Poisson's Ratio)**。

当应用**平面应变**条件 $\varepsilon_z = 0$ 时，从第三个方程我们可以直接得到轴向应力与另外两个主应力的关系：
$$
\sigma_z = \nu(\sigma_r + \sigma_\theta)
$$
这表明，为了维持轴向不变形，必须存在一个非零的轴向应力 $\sigma_z$ 来抵抗由径向和[环向应力](@entry_id:190931)引起的泊松效应。将此关系代入前两个方程，可以得到[平面应变](@entry_id:167046)条件下的二维本构关系。将这套完整的弹性关系与平衡方程和[运动学方程](@entry_id:173032)联立求解，便可得到著名的**拉梅解 (Lamé's solution)**，它给出了纯弹性[厚壁圆筒](@entry_id:189222)在内外压力作用下的应[力场](@entry_id:147325)和[位移场](@entry_id:141476)。这个解是判断材料何时何地首次进入塑性状态的基础。

### 塑性起始：屈服准则

当载荷增加到一定程度时，材料内部某点的应力状态会达到一个临界值，使得材料开始产生不可恢复的永久变形。这个现象称为**屈服 (yielding)**。

#### 屈服的概念

在[应力空间](@entry_id:199156)中，所有能够引起屈服的应力状态组合构成一个[曲面](@entry_id:267450)，称为**[屈服面](@entry_id:175331) (yield surface)**。对于给定的材料，当其应力状态位于[屈服面](@entry_id:175331)内部时，其行为是纯弹性的；当应力状态达到屈服面时，塑性变形开始发生。描述这个[曲面](@entry_id:267450)的数学方程即为**[屈服准则](@entry_id:193897) (yield criterion)**。

#### [静水应力](@entry_id:186327)与偏[应力分解](@entry_id:272862)

大量实验表明，对于金属等晶体材料，均匀施加的**[静水压力](@entry_id:275365) (hydrostatic pressure)** 对其屈服行为影响甚微。这意味着材料能否屈服，并不取决于应力有多“大”，而更多地取决于应力状态的“形状”或剪切程度。为了在数学上体现这一物理特性，我们将[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 分解为一个**[静水应力](@entry_id:186327) (hydrostatic stress)** [部分和](@entry_id:162077)一个**偏应力 (deviatoric stress)** 部分。

[静水应力](@entry_id:186327)，或称[平均应力](@entry_id:751819)，$\sigma_m = \frac{1}{3}(\sigma_r + \sigma_\theta + \sigma_z)$，它与材料的体积变化相关。[偏应力张量](@entry_id:267642) $\mathbf{s} = \boldsymbol{\sigma} - \sigma_m \mathbf{I}$（其中 $\mathbf{I}$ 是单位张量）则代表了导致形状改变（畸变）的应力部分。由于压力无关的屈服特性，适用于金属的[屈服准则](@entry_id:193897)通常仅是[偏应力张量](@entry_id:267642)的函数 。

#### 压力无关的屈服准则

基于上述物理观察，发展了多种[屈服准则](@entry_id:193897)。其中最经典的是 Tresca 准则和 von Mises 准则。

**Tresca 准则（[最大剪应力](@entry_id:181794)准则）**
该准则认为，当材料内某点的[最大剪应力](@entry_id:181794) $\tau_{\max}$ 达到一个临界值时，材料便开始屈服。这个临界值通常通过简单[拉伸试验](@entry_id:185444)来标定。在[单轴拉伸](@entry_id:188287)中，当应力达到[屈服强度](@entry_id:162154) $\sigma_Y$ 时，[最大剪应力](@entry_id:181794)为 $\tau_{\max} = \sigma_Y / 2$。因此，Tresca 准则可以写成 $\tau_{\max} = \sigma_Y / 2$。若用纯剪切试验中的剪切[屈服强度](@entry_id:162154) $k$ 来表示，则 $k = \sigma_Y / 2$ 。

**von Mises 准则（[畸变能](@entry_id:198925)密度准则）**
von Mises 准则是一个更为平滑且在多数情况下与实验结果更吻合的模型。它假设当[偏应力张量](@entry_id:267642)的第二个[不变量](@entry_id:148850) $J_2 = \frac{1}{2} s_{ij}s_{ij}$ 达到临界值时，材料发生屈服。为了便于工程应用，通常将其表示为**[等效应力](@entry_id:749064) (equivalent stress)** $\sigma_{eq}$：
$$
\sigma_{eq} = \sqrt{3 J_2} = \sqrt{\frac{1}{2} \left[ (\sigma_r - \sigma_\theta)^2 + (\sigma_\theta - \sigma_z)^2 + (\sigma_z - \sigma_r)^2 \right]}
$$
屈服条件即为 $\sigma_{eq} = \sigma_Y$。从这个定义式可以清楚地看到，$\sigma_{eq}$ 仅依赖于主应力之差，任何附加的[静水压力](@entry_id:275365)（即给所有[主应力](@entry_id:176761)增加一个相同的值）都不会改变 $\sigma_{eq}$ 的值，从而完美地体现了压力无关性  。

von Mises 准则也被称为**[畸变能](@entry_id:198925)密度准则**，因为在弹性范围内，单位体积的[畸变能](@entry_id:198925)（与形状改变相关的[应变能](@entry_id:162699)）为 $u_d = J_2 / (2G)$，其中 $G$ 是剪切模量。因此，该准则等价于宣告“当[畸变能](@entry_id:198925)密度达到临界值时发生屈服”。在[单轴拉伸](@entry_id:188287)屈服时，该临界值为 $u_d^* = \sigma_Y^2 / (6G)$ 。根据 von Mises 准则，纯剪切试验中的剪切[屈服强度](@entry_id:162154) $k$ 与单轴[屈服强度](@entry_id:162154) $\sigma_Y$ 的关系是 $k = \sigma_Y / \sqrt{3}$，这与 Tresca 准则的预测 ($k = \sigma_Y/2$) 有所不同。

#### 案例：受压圆筒的初次屈服

我们可以运用上述理论来确定一个受[内压](@entry_id:153696)的[厚壁圆筒](@entry_id:189222)何时开始屈服。考虑一个长圆筒，在[平面应变](@entry_id:167046)条件下，其内外径分别为 $a$ 和 $b$，仅受[内压](@entry_id:153696) $p_i$ 作用。

1.  **弹性应[力场](@entry_id:147325)**：首先，利用拉梅解得到圆筒壁内的弹性应力[分布](@entry_id:182848) $\sigma_r(r)$, $\sigma_\theta(r)$ 和 $\sigma_z(r)$。
2.  **计算[等效应力](@entry_id:749064)**：将得到的三个[主应力](@entry_id:176761)分量代入 von Mises [等效应力](@entry_id:749064)公式，得到 $\sigma_{eq}$ 作为半径 $r$ 的函数。
3.  **确定最危险点**：分析表明，$\sigma_{eq}(r)$ 在内壁 $r=a$ 处取得最大值。这意味着屈服将首先在圆筒的内表面发生。
4.  **求解[临界压力](@entry_id:138833)**：令内壁处的[等效应力](@entry_id:749064)等于材料的屈服强度，即 $\sigma_{eq}(a) = \sigma_Y$。由此可以反解出引起初次屈服所需的临界[内压](@entry_id:153696) $p_i$。

例如，对于一个内径 $a=0.05\,\mathrm{m}$、外径 $b=0.15\,\mathrm{m}$、泊松比 $\nu=0.3$、屈服强度 $\sigma_Y=420\,\mathrm{MPa}$ 的钢制圆筒，在平面应变条件下，可以通过上述步骤计算得出，当内压达到约 $215.5\,\mathrm{MPa}$ 时，其内壁开始进入塑性状态 。

### 塑性流动的力学机制

一旦应力状态达到屈服面，材料便开始[塑性流动](@entry_id:201346)。描述这种流动的规律是塑性力学理论的核心。

#### 应变的增量分解

在[弹塑性](@entry_id:193198)理论中，一个核心假设是总应变率（或增量）$\dot{\boldsymbol{\varepsilon}}$ 可以分解为弹性部分 $\dot{\boldsymbol{\varepsilon}}^e$ 和塑性部分 $\dot{\boldsymbol{\varepsilon}}^p$ 之和 ：
$$
\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^e + \dot{\boldsymbol{\varepsilon}}^p
$$
弹性应变率 $\dot{\boldsymbol{\varepsilon}}^e$ 依然遵循胡克定律的率形式，与应力率 $\dot{\boldsymbol{\sigma}}$ 相关。而塑性应变率 $\dot{\boldsymbol{\varepsilon}}^p$ 则由**流动法则 (flow rule)** 决定。

#### [流动法则](@entry_id:177163)

流动法则给出了塑性应变率张量的“方向”。最常用的[流动法则](@entry_id:177163)是**关联[流动法则](@entry_id:177163) (associated flow rule)**，它假定塑性应变率的方向垂直于屈服面。数学上，这表示为 ：
$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$
其中 $f$ 是[屈服函数](@entry_id:167970)，$f(\boldsymbol{\sigma})=0$ 定义了屈服面，$\dot{\lambda}$ 是一个非负的标量，称为**塑性乘子 (plastic multiplier)**，它的大小决定了塑性流动的速率。$\dot{\lambda} > 0$ 表示正在发生塑性加载，$\dot{\lambda} = 0$ 表示弹性加载或卸载。

对于 von Mises 屈服准则 $f = \sigma_{eq} - \sigma_Y$，其对 $\boldsymbol{\sigma}$ 的梯度可以计算为 $\frac{\partial f}{\partial \boldsymbol{\sigma}} = \frac{3}{2} \frac{\mathbf{s}}{\sigma_{eq}}$。因此，关联流动法则具体表现为：
$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \left( \frac{3}{2} \frac{\mathbf{s}}{\sigma_{eq}} \right)
$$
这个重要的关系表明，塑性[应变率张量](@entry_id:266108)与[偏应力张量](@entry_id:267642)成正比。

#### [塑性不可压缩性](@entry_id:183440)

关联[流动法则](@entry_id:177163)应用于压力无关的屈服准则（如 von Mises 或 Tresca）时，会导出一个深刻的结论：塑性变形是保持体积不变的。这被称为**[塑性不可压缩性](@entry_id:183440) (plastic incompressibility)**。

我们可以通过计算塑性应变率的迹（[体积应变率](@entry_id:272471)）来证明这一点。由于 $\dot{\boldsymbol{\varepsilon}}^p$ 与[偏应力张量](@entry_id:267642) $\mathbf{s}$ 成正比，而[偏应力张量](@entry_id:267642)的迹根据其定义恒为零（$\mathrm{tr}(\mathbf{s})=0$），因此  ：
$$
\mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) = \dot{\varepsilon}_{pr} + \dot{\varepsilon}_{p\theta} + \dot{\varepsilon}_{pz} = 0
$$
这意味着在塑性流动过程中，材料的体积不会因为塑性变形而改变。所有的塑性变形都是纯粹的形状改变（畸变）。这也进一步强化了[静水应力](@entry_id:186327)与塑性变形解耦的观点：[静水应力](@entry_id:186327)引起弹性体积变化，而偏应力驱动塑性形状变化。

#### [硬化](@entry_id:177483)模型

许多材料在发生塑性变形后，其屈服强度会提高，这种现象称为**[硬化](@entry_id:177483) (hardening)**。**[理想塑性](@entry_id:753335) (perfect plasticity)** 模型忽略了这种效应，假设[屈服强度](@entry_id:162154) $\sigma_Y$ 是一个常数。而更实际的模型则考虑了硬化。

在**[各向同性硬化](@entry_id:164486) (isotropic hardening)** 模型中，屈服面在应力空间中均匀扩大，但其形状和中心保持不变。屈服强度 $\sigma_Y$ 成为**等效塑性应变 (equivalent plastic strain)** $\kappa$ (或 $\varepsilon_p^{eq}$) 的函数，$\kappa$ 是一个累[积度量](@entry_id:637352)塑性变形量的标量。常见的[硬化](@entry_id:177483)规律包括 ：
- **线性[硬化](@entry_id:177483)**: $\sigma_Y(\kappa) = \sigma_{Y0} + H\kappa$，其中 $\sigma_{Y0}$ 是初始[屈服强度](@entry_id:162154)，$H$ 是常数[硬化](@entry_id:177483)模量。
- **[幂律](@entry_id:143404)硬化**: $\sigma_Y(\kappa) = K\kappa^n$，其中 $K$ 和 $n$ 是材料参数。

[硬化](@entry_id:177483)行为可以通过**塑性模量 (plastic modulus)** $H' = d\sigma_Y / d\kappa$ 来表征。在塑性加载过程中，材料的有效刚度（[切线](@entry_id:268870)模量）会降低，其值依赖于弹性模量 $E$ 和当前的塑性模量 $H'$。例如，在一个近似单轴的应力状态下，[弹塑性切线模量](@entry_id:189492)可以表示为 $E_{ep} = \frac{EH'}{E+H'}$。当 $H' \to \infty$（强[硬化](@entry_id:177483)）时，$E_{ep} \to E$；当 $H' = 0$（[理想塑性](@entry_id:753335)）时，$E_{ep} = 0$ 。

### [弹塑性](@entry_id:193198)[边值问题的建立](@entry_id:189543)

综合以上所有原理，我们现在可以完整地构建求解部分塑性化的[厚壁圆筒](@entry_id:189222)问题的数学框架。假设内压 $p_i$ 足够大，使得圆筒内层区域 $a \le r \le r_p$ 进入塑性状态，而外层区域 $r_p \le r \le b$ 仍保持弹性。我们需要求解整个应[力场](@entry_id:147325)、[位移场](@entry_id:141476)以及未知的[弹塑性](@entry_id:193198)交界半径 $r_p$。

这个问题的完整提法（即**边值问题**的建立）如下 ：

**1. [区域划分](@entry_id:748628)与控制方程:**
- **弹性区 ($r_p \le r \le b$)**:
    - 平衡方程: $\frac{d\sigma_r}{dr} + \frac{\sigma_r - \sigma_\theta}{r} = 0$
    - [运动学](@entry_id:173318)关系: $\varepsilon_r = \frac{du}{dr}$, $\varepsilon_\theta = \frac{u}{r}$
    - 弹性本构（平面应变）: [胡克定律](@entry_id:149682)，以及 $\sigma_z = \nu(\sigma_r + \sigma_\theta)$
- **塑性区 ($a \le r \le r_p$)**:
    - [平衡方程](@entry_id:172166): $\frac{d\sigma_r}{dr} + \frac{\sigma_r - \sigma_\theta}{r} = 0$
    - [运动学](@entry_id:173318)关系: $\varepsilon_r = \frac{du}{dr}$, $\varepsilon_\theta = \frac{u}{r}$
    - 屈服条件（作为约束）: von Mises 准则 $\sigma_{eq}(\sigma_r, \sigma_\theta, \sigma_z) = \sigma_Y$
    - 流动法则与[应变分解](@entry_id:186005): $\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^e + \dot{\boldsymbol{\varepsilon}}^p$ 以及关联流动法则（这些在求解增量问题时使用，对于求解最终应力状态，屈服条件是关键）。

**2. 边界条件与交界条件:**
- **外边界 ($r=b$)**: $\sigma_r(b) = 0$
- **内边界 ($r=a$)**: $\sigma_r(a) = -p_i$
- **[弹塑性](@entry_id:193198)交界面 ($r=r_p$)**:
    - **应力连续性**: [径向应力](@entry_id:197086) $\sigma_r$ 必须连续。
    - **位移连续性**: 径向位移 $u$ 必须连续。
    - **屈服条件**: 在交界面上的应力状态必须恰好满足屈服条件，即 $\sigma_{eq}(r_p) = \sigma_Y$。

这个完整的[方程组](@entry_id:193238)和边界/交界条件集合定义了一个复杂的非[线性边值问题](@entry_id:197996)。求解此问题将给出在给定内压下，圆筒内部的应力、应变和位移的完整[分布](@entry_id:182848)，以及塑性区域的大小。这为评估结构的承载能力、设计安全厚度以及分析如自增强（autofrettage）等工艺提供了理论基础。