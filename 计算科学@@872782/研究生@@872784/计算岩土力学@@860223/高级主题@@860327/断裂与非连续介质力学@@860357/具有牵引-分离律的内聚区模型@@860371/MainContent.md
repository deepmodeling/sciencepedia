## 引言
岩石、土壤等[地质材料](@entry_id:749838)的断裂是计算地球力学中的一个核心挑战。传统的[线性弹性断裂力学](@entry_id:172400)（LEFM）虽然奠定了理论基础，但其在裂纹尖端的[应力奇异性](@entry_id:166362)假设和对[断裂过程区](@entry_id:749561)（FPZ）的忽略，限制了其在模拟准[脆性](@entry_id:198160)材料复杂断裂行为时的准确性。[内聚区模型](@entry_id:194108)（Cohesive Zone Models, CZM）通过引入描述界面分离力学行为的牵[引力](@entry_id:175476)-分离法则（Traction-Separation Law, TSL），为这一难题提供了强大的解决方案。它将复杂的断裂过程转化为一个定义在界面上的本构问题，从而能够更真实地模拟[能量耗散](@entry_id:147406)和从连续变形到完全断裂的过渡。

本文旨在系统性地阐述[内聚区模型](@entry_id:194108)的理论与实践。在“原理与机制”一章中，我们将深入探讨CZM的基本[热力学原理](@entry_id:142232)、关键参数（如断裂能和[内聚强度](@entry_id:194858)）以及不同TSL的具体形式，并解释其在数值计算中的实现要点。接着，在“应用与跨学科联系”一章中，我们将展示CZM如何被扩展应用于解决复杂的[地球科学](@entry_id:749876)问题，例如[水力压裂](@entry_id:750442)中的流固耦合、[地应力](@entry_id:750582)影响下的[混合模式断裂](@entry_id:182261)以及地震滑移的动态模拟。最后，“动手实践”部分将通过具体的计算问题，帮助读者巩固理论知识并掌握模型应用的关键技能。通过这三章的学习，读者将全面掌握[内聚区模型](@entry_id:194108)这一连接微观断裂物理与宏观工程应用的强大工具。

## 原理与机制

在连续介质力学中，裂纹的形成与扩展是一个核心问题。[线性弹性断裂力学](@entry_id:172400)（Linear Elastic Fracture Mechanics, LEFM）为我们理解裂纹行为提供了坚实的基础，但其假设裂纹尖端存在[应力奇异性](@entry_id:166362)，且裂纹表面为无应力边界，这在许多实际[地质材料](@entry_id:749838)中并不完全适用。真实材料的断裂过程通常发生在裂纹尖端前方一个有限大小的区域内，即**[断裂过程区](@entry_id:749561)**（Fracture Process Zone, FPZ）。在这一区域内，微裂纹的萌生、扩展、汇合，以及颗粒间的摩擦、联锁等复杂物理机制，使得看似分离的裂纹面之间仍然能够传递不可忽略的应力。为了更精确地描述这一物理现实，**[内聚区模型](@entry_id:194108)**（Cohesive Zone Models, CZM）应运而生。

[内聚区模型](@entry_id:194108)的核心思想是将[断裂过程区](@entry_id:749561)的复杂物理效应集总到一个零厚度的数学界面上，并通过定义界面上的**牵[引力](@entry_id:175476)-分离位移法则**（Traction-Separation Law, TSL）来描述其[本构关系](@entry_id:186508)。这套法则将界面上的牵[引力](@entry_id:175476)（traction）与位移不连续（即分离位移，separation）直接联系起来，从而将断裂问题转化为一个连续介质内部的本构问题。本章将深入探讨[内聚区模型](@entry_id:194108)的基本原理和内在机制。

### [内聚区模型](@entry_id:194108)的基本原理

#### 从格里菲斯裂纹到内聚界面

在经典断裂力学中，格里菲斯（Griffith）理论将裂纹面处理为自由表面，其上的牵[引力](@entry_id:175476)始终为零，即 $t=0$。然而，在存在有限大小的[断裂过程区](@entry_id:749561)时，这种处理方式忽略了微观尺度上的[应力传递](@entry_id:182468)机制。[内聚区模型](@entry_id:194108)通过引入牵[引力](@entry_id:175476)-分离位移法则，从根本上改变了裂纹的边界条件 [@problem_id:3506965]。

从[热力学](@entry_id:141121)和[能量守恒](@entry_id:140514)的第一性原理出发，我们可以理解这种转变的必然性。考虑一个包含[断裂过程区](@entry_id:749561)的系统，根据虚功原理，内力所做的[虚功](@entry_id:176403)不仅包括块体材料中应力与应变的乘积，还必须包含内聚界面上牵[引力](@entry_id:175476) $\mathbf{t}$ 与[虚位移](@entry_id:168781)跳跃 $\delta\boldsymbol{\delta}$ 的功。这表明，牵[引力](@entry_id:175476) $\mathbf{t}$ 与分离位移 $\boldsymbol{\delta}$ 是一对**[功共轭](@entry_id:194957)**的物理量。

[热力学第二定律](@entry_id:142732)（以[Clausius–Duhem不等式](@entry_id:187377)的形式）要求在[等温过程](@entry_id:143096)中，任何不[可逆过程](@entry_id:276625)的[耗散率](@entry_id:748577)必须为非负。在内聚界面上，这意味着牵[引力](@entry_id:175476)所做的功率减去[界面自由能](@entry_id:183036)的变化率必须大于等于零。这一约束条件将界面牵[引力](@entry_id:175476)提升为一个依赖于分离位移状态的**本构量**，而不再是一个简单的边界条件。因此，牵[引力](@entry_id:175476)-分离位移关系 $t(\delta)$ 是描述[断裂过程区](@entry_id:749561)能量耗散的内在 constitutive law。只有当分离位移达到临界值，内聚力完全消失后，我们才恢复到经典的 $t=0$ 条件。

#### 断裂能与能量耗散

在[内聚区模型](@entry_id:194108)中，一个至关重要的物理量是**[断裂能](@entry_id:174458)**（fracture energy），记为 $G_c$。它被定义为形成单位面积新裂纹面所消耗的能量。这一能量在数值上等于牵[引力](@entry_id:175476)-分离位移曲线下的总面积：

$$
G_c = \int_{0}^{\delta_f} \mathbf{t}(\boldsymbol{\delta}) \cdot \mathrm{d}\boldsymbol{\delta}
$$

其中 $\boldsymbol{\delta}_f$ 是牵[引力](@entry_id:175476)降为零时的最终分离位移。这个 $G_c$ 是一个描述界面断裂韧性的材料属性，直接由牵[引力](@entry_id:175476)-分离位移法则确定。

需要强调的是，[内聚区模型](@entry_id:194108)定义的 $G_c$ 在概念上与LEFM中的格里菲斯临界能量释放率有所区别 [@problem_id:3506911]。在LEFM中，能量释放率是远场弹性体因裂纹扩展而释放的势能，它被假设完全转化为产生新表面的表面能。而在一个存在[非线性](@entry_id:637147)过程区（如塑性或微裂纹）的更普遍情况下，从远场计算的能量释放率（例如通过[J积分](@entry_id:171895)计算）等于裂纹尖端区域内所有耗散机制消耗能量的总和。[内聚区模型](@entry_id:194108)中的 $G_c$ 精确地量化了通过内聚法则所描述的界面分离过程的能量耗散。如果[断裂过程区](@entry_id:749561)内还存在其他未被内聚法则包含的耗散机制（如块体塑性），那么总的能量释放率将大于 $G_c$。因此，内聚[断裂能](@entry_id:174458) $G_c$ 是一个**局部**的、定义在界面上的材料属性。

#### 与[弥散裂纹模型](@entry_id:183723)的对比

与将断裂过程集中于一个界面的[内聚区模型](@entry_id:194108)不同，另一类模型——**[弥散裂纹模型](@entry_id:183723)**（smeared crack damage models）——通过在块体单元的积分点上引入[损伤变量](@entry_id:197066)来模拟[材料刚度](@entry_id:158390)的退化。从[热力学](@entry_id:141121)和计算的角度看，这两种方法有本质区别 [@problem_id:3506900]。

- **本构关系与[功共轭](@entry_id:194957)对**：[内聚区模型](@entry_id:194108)在界面 $\Gamma_c$ 上建立了牵[引力](@entry_id:175476) $\mathbf{t}$ 和位移跳跃 $\boldsymbol{\delta}$ 之间的[本构关系](@entry_id:186508)。而弥散损伤模型在块体 $\Omega$ 内定义了应力 $\boldsymbol{\sigma}$ 和应变 $\boldsymbol{\varepsilon}$ 之间的关系，通常形式为 $\boldsymbol{\sigma} = \mathbf{C}(d) : \boldsymbol{\varepsilon}$，其中 $d$ 是一个在体积内演化的[损伤变量](@entry_id:197066)。

- **能量耗散与[网格敏感性](@entry_id:178333)**：这是一个关键区别。对于没有引入内部长度尺度的局部弥散损伤模型，模拟中应变会集中在一个宽度与单元尺寸相当的区域内。当网格细化时，这个区域的体积趋于零，导致总耗散能也非物理地趋于零。这种现象被称为**病态[网格敏感性](@entry_id:178333)**。相比之下，[内聚区模型](@entry_id:194108)将所有耗散都限制在零体积的表面 $\Gamma_c$ 上。[断裂能](@entry_id:174458) $G_c$ 是一个单位面积的材料常数，因此总耗散能与周围块体的[网格划分](@entry_id:269463)无关，从而保证了结构响应在能量耗散方面的**网格客观性**。

### 牵[引力](@entry_id:175476)-分离位移法则的具体形式

牵[引力](@entry_id:175476)-分离位移法则（TSL）是[内聚区模型](@entry_id:194108)的核心。它可以有多种函数形式，以适应不同材料的断裂行为。一个典型的TSL通常由几个关键参数定义：**峰值牵[引力](@entry_id:175476)**（或称[内聚强度](@entry_id:194858)）$T_c$，以及**临界/最终分离位移** $\delta_f$。[断裂能](@entry_id:174458) $G_c$ 则是这些参数和TSL形状共同决定的。以下是几种常见的TSL形式 [@problem_id:3506952]。

#### 双线性法则 (Bilinear Law)

[双线性](@entry_id:146819)法则是最简单和最常用的TSL之一。它由一个线性上升段和一个线性下降（软化）段组成。

- **法则定义**：
  - 初始线性加载阶段（$0 \le \delta \le \delta_0$）：牵[引力](@entry_id:175476)从零线性增加到峰值 $T_c$。$t(\delta) = K_0 \delta = (T_c/\delta_0)\delta$。其中 $K_0$ 是初始[罚刚度](@entry_id:753321)，$\delta_0$ 是达到峰值牵[引力](@entry_id:175476)时的分离位移。
  - 线性软化阶段（$\delta_0  \delta \le \delta_f$）：牵[引力](@entry_id:175476)从 $T_c$ 线性减小到零。其表达式为：
    $$
    t(\delta) = T_c \left(1 - \frac{\delta - \delta_0}{\delta_f - \delta_0}\right)
    $$
  - 完全分离后（$\delta > \delta_f$）：$t(\delta) = 0$。

- **断裂能**：[双线性](@entry_id:146819)TSL下的面积构成一个底为 $\delta_f$、高为 $T_c$ 的三角形，因此[断裂能](@entry_id:174458)为：
  $$
  G_c = \frac{1}{2} T_c \delta_f
  $$

#### [梯形法则](@entry_id:145375) (Trapezoidal Law)

[梯形法则](@entry_id:145375)在达到峰值牵[引力](@entry_id:175476)后引入了一个平台段，这可以用于模拟一些材料在断裂前经历的[延性](@entry_id:160108)行为。

- **法则定义**：
  - 初始线性加载阶段（$0 \le \delta \le \delta_0$）：$t(\delta) = (T_c/\delta_0)\delta$。
  - 恒定牵[引力](@entry_id:175476)平台阶段（$\delta_0  \delta \le \delta_p$）：牵[引力](@entry_id:175476)保持为 $T_c$。
  - 线性软化阶段（$\delta_p  \delta \le \delta_f$）：牵[引力](@entry_id:175476)从 $T_c$ 线性减小到零。
    $$
    t(\delta) = T_c \left(1 - \frac{\delta - \delta_p}{\delta_f - \delta_p}\right)
    $$

- **断裂能**：梯形法则下的面积可以通过计算各部分面积之和得到 [@problem_id:3506906]。它等于一个三角形、一个矩形和一个三角形面积之和：
  $$
  G_c = \frac{1}{2}\delta_0 T_c + (\delta_p - \delta_0)T_c + \frac{1}{2}(\delta_f - \delta_p)T_c
  $$
  简化后得到：
  $$
  G_c = \frac{1}{2} T_c (\delta_f + \delta_p - \delta_0)
  $$

#### 指数法则 (Exponential Law)

指数法则提供了一个光滑的牵[引力](@entry_id:175476)-分离位移曲线，其导数连续，这在数值计算中可能具有优势。一个常见的指数形式（Xu-Needleman法则）如下：

- **法则定义**：
  $$
  t(\delta) = T_c \frac{\delta}{\delta_*} \exp\left(1 - \frac{\delta}{\delta_*}\right)
  $$
  其中 $\delta_*$ 是达到峰值牵[引力](@entry_id:175476) $T_c$ 时的分离位移。此后，牵[引力](@entry_id:175476)渐近趋于零，因此理论上 $\delta_f = \infty$。

- **断裂能**：通过对上述表达式从 $0$ 到 $\infty$ 积分，可得[断裂能](@entry_id:174458)为：
  $$
  G_c = T_c e \delta_*
  $$
  其中 $e$ 是自然对数的底。

### 内禀内聚长度尺度

[内聚区模型](@entry_id:194108)的一个深刻启示是，它自然地引入了一个**[内禀长度尺度](@entry_id:750789)**（intrinsic length scale），这个尺度将材料的宏观弹性行为（如[杨氏模量](@entry_id:140430) $E$）与断裂界面的内聚属性（$T_c$ 和 $G_c$）联系起来。这个长度尺度对于判断结构的脆性行为至关重要。

我们可以通过一个简单的思想实验来推导这个长度尺度 [@problem_id:3506933]。考虑一个长度为 $L$、杨氏模量为 $E$ 的一维弹性杆，其中包含一个内聚界面。杆的总伸长量 $U$ 是块体弹性伸长 $\varepsilon L$ 和界面开度 $w$ 的总和，即 $U = \varepsilon L + w$。杆中的应力 $\sigma$ 等于界面上的牵[引力](@entry_id:175476) $T$，且 $\sigma = E\varepsilon$。联立这些关系可得：
$$
U = \frac{L}{E}T(w) + w
$$
在[位移控制](@entry_id:748569)加载下，结构的响应是否稳定取决于总伸长量-牵[引力](@entry_id:175476)[曲线的斜率](@entry_id:178976)。在软化开始的瞬间，即 $w$ 刚开始从0增大的时候，我们可以考察总伸长量 $U$ 的增量 $\mathrm{d}U$ 和牵[引力](@entry_id:175476)增量 $\mathrm{d}T$ 的关系：
$$
\mathrm{d}U = \frac{L}{E}\mathrm{d}T + \mathrm{d}w
$$
由于 $\mathrm{d}T = T'(w)\mathrm{d}w$，其中 $T'(w)$ 是TSL的斜率，代入上式可得结构刚度 $\mathrm{d}T/\mathrm{d}U$ 的表达式。当结构尺寸 $L$ 超过某个临界值时，结构的响应会变得不稳定（出现“[突跳](@entry_id:177661)”现象），表现为[脆性断裂](@entry_id:158949)。这个临界尺寸正比于一个由材料和内聚参数构成的组合量。这个组合量具有长度的量纲，被称为**内禀内聚长度** $l_c$：
$$
l_c = \frac{E G_c}{T_c^2}
$$
这个长度尺度可以被看作是[断裂过程区](@entry_id:749561)大小的一个度量。结构的宏观断裂行为取决于其特征尺寸 $L$ 与材料内禀长度 $l_c$ 的比值 $L/l_c$。当 $L/l_c$ 很大时，结构储存的弹性应变能足以在没有外部能量持续输入的情况下驱动裂纹失稳扩展，表现为**脆性**行为。反之，当 $L/l_c$ 很小时，断裂过程是稳定的，需要持续增加外加载荷才能使[裂纹扩展](@entry_id:749562)，表现为**韧性**行为。

### 高级[本构模型](@entry_id:174726)特征

实际断裂过程往往更为复杂，需要更高级的本构模型来描述。

#### [混合模式断裂](@entry_id:182261)

许多情况下的断裂并非纯粹的张开（I型），而是张开与剪切（II型或III型）的组合，即**[混合模式断裂](@entry_id:182261)**（mixed-mode fracture）。为了描述这种情况，需要将TSL扩展到矢量形式。一种常用且[热力学一致的](@entry_id:755906)方法是引入一个**等效分离位移** $\bar{\delta}$，它将法向分离位移 $\delta_n$ 和切向滑移 $\delta_t$ 组合起来 [@problem_id:3506946]。

一个常见的等效分离位移定义如下：
$$
\bar{\delta} = \sqrt{\langle \delta_n \rangle^2 + \beta \delta_t^2}
$$
其中 $\langle \delta_n \rangle = \max(0, \delta_n)$ 是Macaulay括号，确保法向压缩不引起损伤。$\beta$ 是一个无量纲的**[模式混合](@entry_id:197206)参数**，用于调整切向滑移对等效分离位移的贡献权重。

在一个基于势能的框架中，可以定义一个仅依赖于 $\bar{\delta}$ 的[界面自由能](@entry_id:183036)密度 $\Psi(\bar{\delta})$。根据[热力学一致性](@entry_id:138886)要求，法向和切向牵[引力](@entry_id:175476)可以通过[对势能](@entry_id:203104)求导得到：
$$
t_n = \frac{\partial \Psi}{\partial \delta_n} = \Psi'(\bar{\delta}) \frac{\partial \bar{\delta}}{\partial \delta_n} = \Psi'(\bar{\delta}) \frac{\langle \delta_n \rangle}{\bar{\delta}}
$$
$$
\mathbf{t}_t = \frac{\partial \Psi}{\partial \boldsymbol{\delta}_t} = \Psi'(\bar{\delta}) \frac{\partial \bar{\delta}}{\partial \boldsymbol{\delta}_t} = \Psi'(\bar{\delta}) \frac{\beta \boldsymbol{\delta}_t}{\bar{\delta}}
$$
其中 $\Psi'(\bar{\delta}) = \mathrm{d}\Psi/\mathrm{d}\bar{\delta}$。从这些关系可以看出，参数 $\beta$ 直接影响了在给定的分离位移状态 $(\delta_n, \delta_t)$ 下，切向牵[引力](@entry_id:175476)与法向牵[引力](@entry_id:175476)的相对大小。同时，界面的[失效准则](@entry_id:195168)（例如 $\bar{\delta}$ 达到临界值 $\bar{\delta}_c$）在 $(\delta_n, \delta_t)$ 平面上定义了一个椭圆形的失效[包络线](@entry_id:174062)，其形状由 $\beta$ 控制。

#### 不可逆损伤与加卸载行为

断裂是一个[能量耗散](@entry_id:147406)的不可逆过程。这意味着一旦界面发生损伤，其刚度就会永久性下降。在循环加载或部分卸载的情况下，必须精确定义材料的**加卸载**路径。这通常通过引入一个内部**[损伤变量](@entry_id:197066)** $d \in [0, 1]$ 来实现 [@problem_id:3506958]。

一个典型的损伤模型将牵[引力](@entry_id:175476)表示为：
$$
\mathbf{t} = (1-d) \mathbf{K}_0 \boldsymbol{\delta}
$$
其中 $\mathbf{K}_0$ 是界面的初始（未损伤）[罚刚度](@entry_id:753321)。损伤的不[可逆性](@entry_id:143146)要求 $\dot{d} \ge 0$。为了在卸载和重加载时保持损伤不变，同时在新的加载阶段让损伤继续演化，需要引入一个**历史变量**，通常取为经历过的最大等效分离位移，记为 $\kappa(t) = \max_{s \le t} \bar{\delta}(s)$。

[损伤变量](@entry_id:197066) $d$ 则被定义为历史变量 $\kappa$ 的一个单调不减函数，即 $d = g(\kappa)$。其演化遵循一套**Kuhn-Tucker加载/卸载条件**：
$$
\dot{\kappa} \ge 0, \qquad f(\bar{\delta}, \kappa) := \bar{\delta} - \kappa \le 0, \qquad \dot{\kappa} f(\bar{\delta}, \kappa) = 0
$$
这套条件确保了：
1.  **加载**：当 $\bar{\delta} = \kappa$ 且 $\dot{\bar{\delta}} > 0$ 时，历史变量更新为 $\kappa = \bar{\delta}$，损伤 $d$ 随之增加。此时，牵[引力](@entry_id:175476)-分离位移关系必须满足预设的软化包络线 $\widehat{t}(\bar{\delta})$。
2.  **卸载/重加载**：当 $\bar{\delta}  \kappa$ 时，$\dot{\kappa} = 0$，损伤 $d$ 保持不变。此时牵[引力](@entry_id:175476)与分离位移呈线性关系 $\mathbf{t} = (1-d)\mathbf{K}_0\boldsymbol{\delta}$，即沿一条[割线](@entry_id:178768)返回原点，其斜率（退化刚度）小于初始刚度 $\mathbf{K}_0$。

这种基于[损伤力学](@entry_id:178377)的框架，能够精确描述断裂过程中的[刚度退化](@entry_id:202277)和[能量耗散](@entry_id:147406)，并为数值实现提供了清晰的算法流程。

### 计算实现中的关键概念

将[内聚区模型](@entry_id:194108)应用于有限元等数值方法时，需要解决两个核心问题：如何在离散模型中表示位移不连续，以及如何求解由此产生的[非线性方程组](@entry_id:178110)。

#### 强不连续[运动学](@entry_id:173318)增强

在标准有限元中，位移场在单元内部是连续的。为了模拟裂纹（一种**强不连续**），需要对[有限元基函数](@entry_id:749279)进行**运动学增强**。[扩展有限元法](@entry_id:162867)（XFEM）或嵌入式不连续方法（EDM）等技术为此提供了成熟的框架 [@problem_id:3506923]。

其核心思想是在包含[不连续面](@entry_id:180188) $\Gamma_c$ 的单元中，将位移场 $u(x)$ 分解为连续部分 $\bar{u}(x)$ 和一个引入跳跃的增强部分。增强部分通常通过乘以一个**亥维赛德函数**（Heaviside function）$H(\phi(x))$ 来构造，其中 $\phi(x)$ 是描述[不连续面](@entry_id:180188)的水平集函数（level-set function），在 $\Gamma_c$ 上 $\phi(x)=0$。一个通用的增强[位移场](@entry_id:141476)形式为：
$$
\mathbf{u}(x) = \bar{\mathbf{u}}(x) + M(x) H(\phi(x)) \boldsymbol{\delta}
$$
其中 $M(x)$ 是一个光滑的局部化函数（如[单位分解](@entry_id:150115)函数），确保增强项只在特定区域起作用，并且在 $\Gamma_c$ 上 $M(x)=1$。$\boldsymbol{\delta}$ 是代表位移跳跃大小的附加自由度。这种形式的位移场能够在 $\Gamma_c$ 上精确地产生一个大小为 $\boldsymbol{\delta}$ 的位移跳跃。

在虚功原理的弱形式表述中，内聚牵[引力](@entry_id:175476) $t(\delta)$ 的贡献表现为一个内边界上的积分项。对于任意[虚位移](@entry_id:168781)场，其对应的[虚位移](@entry_id:168781)跳跃为 $\llbracket w \rrbracket$，则[内聚力](@entry_id:274824)所做的[虚功](@entry_id:176403)为：
$$
\delta W_{coh} = \int_{\Gamma_c} \mathbf{t}(\boldsymbol{\delta}) \cdot \llbracket \mathbf{w} \rrbracket \, \mathrm{d}\Gamma
$$
这一项被加入到有限元[方程组](@entry_id:193238)的[内力向量](@entry_id:750751)中。

#### [非线性](@entry_id:637147)求解与一致性[切线刚度](@entry_id:166213)

由于牵[引力](@entry_id:175476)-分离位移法则是[非线性](@entry_id:637147)的（特别是包含软化段），最终得到的代数方程组也是[非线性](@entry_id:637147)的，必须通过迭代方法求解，如**牛顿-拉夫逊（[Newton-Raphson](@entry_id:177436)）方法**。[牛顿法](@entry_id:140116)的核心在于利用系统残差对自由度的一阶导数——即**[切线刚度矩阵](@entry_id:170852)**——来指导迭代方向。

为了保证[牛顿法](@entry_id:140116)具有二次收敛速度，必须使用精确的[切线刚度矩阵](@entry_id:170852)。在[内聚区模型](@entry_id:194108)中，这意味着需要计算牵[引力](@entry_id:175476) $\mathbf{t}$ 对分离位移 $\boldsymbol{\delta}$ 的精确导数，这个导数被称为**一致性[算法切线](@entry_id:165770)刚度**（consistent algorithmic tangent）$\mathbf{C}_{\text{coh}}$ [@problem_id:3506909]：
$$
\mathbf{C}_{\text{coh}} = \frac{\partial \mathbf{t}}{\partial \boldsymbol{\delta}}
$$
对于一个基于损伤的[本构模型](@entry_id:174726) $\mathbf{t} = (1-d(\boldsymbol{\delta}))\mathbf{K}_0 \boldsymbol{\delta}$，在加载过程中 $d$ 是 $\boldsymbol{\delta}$ 的函数，因此必须使用[链式法则](@entry_id:190743)进行求导：
$$
\mathbf{C}_{\text{coh}} = (1-d) \mathbf{K}_0 - (\mathbf{K}_0 \boldsymbol{\delta}) \otimes \frac{\partial d}{\partial \boldsymbol{\delta}}
$$
其中 $\otimes$ 代表外积（dyadic product）。第二项是由于[损伤演化](@entry_id:184965)引起的，它在软化阶段是负定的，导致[切线刚度矩阵](@entry_id:170852)可能不再是正定的。忽略这一项（例如，仅使用第一项的割线刚度，或使用初始弹性刚度）虽然可以简化计算，但会破坏[牛顿法](@entry_id:140116)的二次收敛性，导致[收敛速度](@entry_id:636873)下降为线性甚至更慢，尤其是在软化行为显著的计算后期，可能会导致收敛困难。因此，精确计算并使用一致性[切线刚度](@entry_id:166213)对于保证[非线性](@entry_id:637147)求解过程的效率和鲁棒性至关重要。