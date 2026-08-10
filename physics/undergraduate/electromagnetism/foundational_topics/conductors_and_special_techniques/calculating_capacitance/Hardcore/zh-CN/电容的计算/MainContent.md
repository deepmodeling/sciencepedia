## 引言
[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)是现代电子学和电气工程中不可或缺的基本元件，其核心特性——电容，是衡量其储存[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)和能量能力的关键物理量。精确计算电容不仅是电磁学理论的基础要求，更是设计和优化从微芯片到高压输电系统等各类实际应用的关键一步。然而，电容的计算并非总是直截了当，它与导体的复杂几何形状、以及填充介质的多样物理属性紧密相关，这构成了我们面临的主要挑战。

本文旨在为您提供一个关于电容计算的全面而深入的指南。通过三个层次分明的章节，我们将系统地解决如何精确确定各种条件下[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)的电容值这一核心问题。
- 在“原理与机制”一章中，我们将从电容的根本定义出发，建立一套标准的计算流程，并深入探讨基于能量和力的更高级计算方法，同时揭示电容与其他物理量之间的内在联系。
- 接着，在“应用与跨学科联系”一章中，我们将视野扩展到实际工程和前沿科学，探讨电容概念在电路设计、[材料工程](@keyword=materials_engineering|lang=zh-CN|style=Feynman)、固态物理、生物物理乃至相对论中的具体体现和深刻影响。
- 最后，“动手实践”部分将提供一系列精心设计的问题，帮助您巩固所学知识，并将理论方法应用于解决实际问题。

让我们从电容最基本的原理开始，踏上这段从理论基础到前沿应用的探索之旅。

## 原理与机制

[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)是储存电能的基本元件，其核心属性是电容。电容的大小不仅取决于其几何构造，还与导体间的[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)材料密切相关。本章将系统地阐述计算电容的若干基本原理和核心方法，从定义出发，逐步深入到基于能量和力的计算，并探讨电容与其他物理量之间的深刻联系。

### 电容的定义：基本关系

从最根本的角度看，[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)是由两个相互绝缘的导体组成的系统。当这两个导体分别携带等量异号的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $+Q$ 和 $-Q$ 时，它们之间会建立起一个[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)，并因此产生一个确定的[电势差](@keyword=potential_difference|lang=zh-CN|style=Feynman) $V$。实验表明，对于一个给定的[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)，其储存的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)量 $Q$ 与两极板间的电势差 $V$ 成正比：

$Q = CV$

比例系数 $C$ 被定义为该[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)的**电容 (capacitance)**。电容是衡量[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)储存[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)能力的一个物理量，其单位是法拉 (F)。从定义式 $C = Q/V$ 可以看出，电容是一个只与[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)的几何结构（如导体的形状、大小、相对位置）和导体间的介质属性有关的量，而与导体上的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)量 $Q$ 或[电势差](@keyword=potential_difference|lang=zh-CN|style=Feynman) $V$ 无关。

虽然[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)通常指由两个导体组成的系统，但我们也可以讨论单个孤立导体的电容。在这种情况下，我们可以想象第二个导体位于无穷远处，并且其[电势](@keyword=electric_potential|lang=zh-CN|style=Feynman)按惯例定义为零。例如，考虑一个半径为 $R$ 的孤立导电球体，当它携带[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $Q$ 时，根据高斯定律，其外部的[电场](@keyword=electric_field|lang=zh-CN|style=Feynman) ($r \ge R$) 与一个位于球心的[点电荷](@keyword=point_charges|lang=zh-CN|style=Feynman) $Q$ 所产生的[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)完全相同，即 $E(r) = Q / (4\pi\epsilon_0 r^2)$。球体表面的[电势](@keyword=electric_potential|lang=zh-CN|style=Feynman)（相对于无穷远处）为：

$V = -\int_{\infty}^{R} \vec{E} \cdot d\vec{l} = \int_{R}^{\infty} E(r) dr = \int_{R}^{\infty} \frac{Q}{4\pi\epsilon_0 r^2} dr = \frac{Q}{4\pi\epsilon_0 R}$

根据电容的定义，这个孤立球体的电容为：

$C = \frac{Q}{V} = 4\pi\epsilon_0 R$

这个结果 [@problem_id:1786901] 表明，一个孤立导体的电容正比于其尺寸。地球的半径约为 $6400 \text{ km}$，其电容也仅有约 $710 \text{ μF}$，这说明法拉是一个非常大的单位。

### 计算电容的一般流程

对于由两个导体构成的、具有特定几何形状的[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)，计算其电容通常遵循一个标准流程：

1.  **假设[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)**：假设两个导体分别带有 $+Q$ 和 $-Q$ 的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)。对于具有[平移对称性](@keyword=translational_symmetry|lang=zh-CN|style=Feynman)的长直结构（如电缆），通常假设单位长度的[线电荷密度](@keyword=linear_charge_density|lang=zh-CN|style=Feynman)为 $+\lambda$ 和 $-\lambda$。

2.  **计算[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)**：利用[高斯定律](@keyword=gauss_s_law|lang=zh-CN|style=Feynman)或库仑定律，计算出由这些[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)在两导体之间区域产生的[电场](@keyword=electric_field|lang=zh-CN|style=Feynman) $\vec{E}$。对于具有高度对称性的系统（如[平行板](@keyword=parallel_plates|lang=zh-CN|style=Feynman)、同轴圆柱、同心球），[高斯定律](@keyword=gauss_s_law|lang=zh-CN|style=Feynman)是首选工具。

3.  **计算[电势差](@keyword=potential_difference|lang=zh-CN|style=Feynman)**：通过对[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)进行[线积分](@keyword=line_integrals|lang=zh-CN|style=Feynman)，计算两导体之间的电势差 $V = |\int_{+}^{-} \vec{E} \cdot d\vec{l}|$。积分路径从正[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)导体延伸到负[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)导体。

4.  **计算电容**：最后，利用电容的定义式 $C = Q/V$（或对于长直结构，$C_L = \lambda/V$）求得电容。

让我们通过一个典型的例子来实践这个流程。考虑一个长同轴电缆，它由半径为 $a$ 的实心内导体和内半径为 $b$ 的同轴空心外导体构成 [@problem_id:1786848]。假设内导体带有的[线电荷密度](@keyword=linear_charge_density|lang=zh-CN|style=Feynman)为 $\lambda$，外导体为 $-\lambda$。根据[圆柱对称性](@keyword=cylindrical_symmetry|lang=zh-CN|style=Feynman)，我们可以应用[高斯定律](@keyword=gauss_s_law|lang=zh-CN|style=Feynman)，选取一个半径为 $r$ ($a \lt r \lt b$)、长度为 $L$ 的同轴圆柱面作为[高斯面](@keyword=gaussian_surface|lang=zh-CN|style=Feynman)。通过该面的[电通量](@keyword=electric_flux|lang=zh-CN|style=Feynman)为 $E(r) \cdot 2\pi r L$，它包围的[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为 $\lambda L$。因此，[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)为：

$E(r) = \frac{\lambda}{2\pi\epsilon_0 r}$

两导体间的电势差为：

$V = -\int_{b}^{a} E(r) dr = \int_{a}^{b} \frac{\lambda}{2\pi\epsilon_0 r} dr = \frac{\lambda}{2\pi\epsilon_0} [\ln(r)]_{a}^{b} = \frac{\lambda}{2\pi\epsilon_0} \ln\left(\frac{b}{a}\right)$

值得注意的是，如果已知电势函数 $V(r) = V_0 \frac{\ln(b/r)}{\ln(b/a)}$，其中 $V_0$ 是内外导体间的电势差，我们也可以通过求导 $E_r(r) = -dV/dr$ 得到相同的[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)表达式，这两种方法是等价的。

最后，该同轴电缆的单位长度电容 $C_L$ 为：

$C_L = \frac{\lambda}{V} = \frac{\lambda}{\frac{\lambda}{2\pi\epsilon_0} \ln(\frac{b}{a})} = \frac{2\pi\epsilon_0}{\ln(b/a)}$

这个流程同样适用于更复杂的情况，例如当导体间的介质不均匀时。考虑一个由半径为 $R_1$ 和 $R_2$ 的同心导电球壳组成的[球形电容器](@keyword=spherical_capacitor|lang=zh-CN|style=Feynman)，其间填充了一种非均匀的[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)，其[相对介电常数](@keyword=relative_permittivity|lang=zh-CN|style=Feynman)随半径变化，$\kappa(r) = R_1/r$ [@problem_id:1786853]。此时，[介电常数](@keyword=dielectric_constant|lang=zh-CN|style=Feynman)为 $\epsilon(r) = \epsilon_0 \kappa(r) = \epsilon_0 R_1/r$。在这种情况下，使用包含自由电荷的高斯定律（针对[电位移矢量](@keyword=electric_displacement_vector|lang=zh-CN|style=Feynman) $\vec{D}$）会更方便。假设内球壳带[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $+Q$，外球壳带[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $-Q$。对于半径为 $r$ ($R_1 \lt r \lt R_2$) 的高斯球面，我们有 $\oint \vec{D} \cdot d\vec{A} = Q_{free}$，这给出 $D(r) \cdot 4\pi r^2 = Q$，所以 $D(r) = \frac{Q}{4\pi r^2}$。

[电场](@keyword=electric_field|lang=zh-CN|style=Feynman) $\vec{E}$ 可由关系式 $\vec{D} = \epsilon(r) \vec{E}$ 得到：

$E(r) = \frac{D(r)}{\epsilon(r)} = \frac{Q/(4\pi r^2)}{\epsilon_0 R_1/r} = \frac{Q}{4\pi \epsilon_0 R_1 r}$

有趣的是，尽管[介电常数](@keyword=dielectric_constant|lang=zh-CN|style=Feynman)随半径减小，但[电场](@keyword=electric_field|lang=zh-CN|style=Feynman) $E(r)$ 仍然是 $1/r$ 依赖关系，而不是通常的 $1/r^2$。两导体间的[电势差](@keyword=potential_difference|lang=zh-CN|style=Feynman)为：

$V = \int_{R_1}^{R_2} E(r) dr = \int_{R_1}^{R_2} \frac{Q}{4\pi \epsilon_0 R_1 r} dr = \frac{Q}{4\pi \epsilon_0 R_1} \ln\left(\frac{R_2}{R_1}\right)$

因此，电容为：

$C = \frac{Q}{V} = \frac{4\pi \epsilon_0 R_1}{\ln(R_2/R_1)}$

### 含[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)的[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)：组合

当[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)中填充多种[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)时，其总电容的计算可以等效为多个简单[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)的组合。组合方式取决于[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)相对于[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)方向的[排列](@keyword=permutation|lang=zh-CN|style=Feynman)方式。

#### [串联](@keyword=catenation|lang=zh-CN|style=Feynman)组合与[倒电容](@keyword=elastance|lang=zh-CN|style=Feynman)

如果多种[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)沿着[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)方向分层堆叠，这可以看作是多个[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)的**[串联](@keyword=catenation|lang=zh-CN|style=Feynman) (series combination)**。考虑一个平行板电容器，板面积为 $A$，总间距为 $d$。其间填充了两层厚度均为 $d/2$ 的[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)，[介电常数](@keyword=dielectric_constant|lang=zh-CN|style=Feynman)分别为 $\epsilon_1$ 和 $\epsilon_2$ [@problem_id:1786866]。

在[串联](@keyword=catenation|lang=zh-CN|style=Feynman)配置中，当极板带上自由电荷 $\pm Q$ 时，各层[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)中的[电位移矢量](@keyword=electric_displacement_vector|lang=zh-CN|style=Feynman) $D$ 的大小是连续且处处相等的，即 $D = Q/A$（忽略[边缘效应](@keyword=edge_effects|lang=zh-CN|style=Feynman)）。然而，每层中的[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)强度是不同的：$E_1 = D/\epsilon_1$ 和 $E_2 = D/\epsilon_2$。总[电势差](@keyword=potential_difference|lang=zh-CN|style=Feynman)是各层电势差之和：

$V = V_1 + V_2 = E_1 \frac{d}{2} + E_2 \frac{d}{2} = \frac{D d}{2} \left(\frac{1}{\epsilon_1} + \frac{1}{\epsilon_2}\right) = \frac{Q d}{2A} \left(\frac{\epsilon_1 + \epsilon_2}{\epsilon_1 \epsilon_2}\right)$

总电容 $C = Q/V$ 为：

$C = \frac{2A\epsilon_1 \epsilon_2}{d(\epsilon_1 + \epsilon_2)}$

这个结果可以从另一个角度理解。[串联](@keyword=catenation|lang=zh-CN|style=Feynman)[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)的[等效电容](@keyword=equivalent_capacitance|lang=zh-CN|style=Feynman) $C_{eq}$ 满足关系式 $\frac{1}{C_{eq}} = \sum \frac{1}{C_i}$。在这个问题中，我们可以将两层[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)视为两个独立的[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman) $C_1 = \frac{\epsilon_1 A}{d/2}$ 和 $C_2 = \frac{\epsilon_2 A}{d/2}$ [串联](@keyword=catenation|lang=zh-CN|style=Feynman)。于是：

$\frac{1}{C} = \frac{1}{C_1} + \frac{1}{C_2} = \frac{d/2}{\epsilon_1 A} + \frac{d/2}{\epsilon_2 A} = \frac{d}{2A} \left(\frac{1}{\epsilon_1} + \frac{1}{\epsilon_2}\right)$

这与我们直接推导的结果完全一致。为了方便处理[串联](@keyword=catenation|lang=zh-CN|style=Feynman)问题，物理学家有时会使用**[倒电容](@keyword=elastance|lang=zh-CN|style=Feynman) (elastance)**，定义为 $S = 1/C$。它的物理意义是单位[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)所产生的[电势差](@keyword=potential_difference|lang=zh-CN|style=Feynman)。对于[串联](@keyword=catenation|lang=zh-CN|style=Feynman)[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)，等效[倒电容](@keyword=elastance|lang=zh-CN|style=Feynman)就是各个[倒电容](@keyword=elastance|lang=zh-CN|style=Feynman)之和：$S_{eq} = \sum S_i$ [@problem_id:1786906]。[倒电容](@keyword=elastance|lang=zh-CN|style=Feynman)的单位是 F$^{-1}$。

#### 并联组合

如果多种[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)沿垂直于[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)的方向并排放置，这可以看作是多个[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)的**并联 (parallel combination)**。考虑一个平行板电容器，板面积为 $A$，间距为 $d$。其间被两种[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)填满，每种占据一半的体积，[介电常数](@keyword=dielectric_constant|lang=zh-CN|style=Feynman)分别为 $\epsilon_1$ 和 $\epsilon_2$ [@problem_id:1786912]。

在并联配置中，两块极板是[等势面](@keyword=equipotential_surfaces|lang=zh-CN|style=Feynman)，因此穿过两种[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)的[电势差](@keyword=potential_difference|lang=zh-CN|style=Feynman)是相同的，都等于总[电势差](@keyword=potential_difference|lang=zh-CN|style=Feynman) $V$。[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)在每个区域内是均匀的，$E_1 = E_2 = V/d$。但是，每个区域的[电位移矢量](@keyword=electric_displacement_vector|lang=zh-CN|style=Feynman)是不同的，$D_1 = \epsilon_1 E_1$ 和 $D_2 = \epsilon_2 E_2$。极板上的总[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $Q$ 是两个区域所对应的极板[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)之和 $Q_1+Q_2$。

$Q = Q_1 + Q_2 = D_1 \frac{A}{2} + D_2 \frac{A}{2} = (\epsilon_1 E_1 + \epsilon_2 E_2)\frac{A}{2} = (\epsilon_1 + \epsilon_2) \frac{V}{d} \frac{A}{2}$

总电容 $C = Q/V$ 为：

$C = \frac{A(\epsilon_1 + \epsilon_2)}{2d}$

同样，这可以看作是两个[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman) $C_1 = \frac{\epsilon_1 (A/2)}{d}$ 和 $C_2 = \frac{\epsilon_2 (A/2)}{d}$ 并联。对于并联[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)，总电容等于各个电容之和：$C_{eq} = \sum C_i$。

### [电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)中的能量与力

[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)储存的不仅是[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)，还有静[电场能量](@keyword=energy_stored_in_electric_field|lang=zh-CN|style=Feynman)。这一能量观点为计算电容和导体间相互作用力提供了另一种强大的途径。

#### 从能量计算电容

静[电场中的能量密度](@keyword=energy_density_in_electric_fields|lang=zh-CN|style=Feynman)为 $u = \frac{1}{2}\vec{E} \cdot \vec{D}$。对于线性介质，这简化为 $u = \frac{1}{2}\epsilon E^2$。通过在两导体之间的整个空间对能量密度进行积分，就可以得到[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)储存的总能量 $U$。

$U = \int_{\text{volume}} u \, d\tau = \frac{1}{2} \int \epsilon E^2 d\tau$

另一方面，[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)的总[储能](@keyword=energy_storage|lang=zh-CN|style=Feynman)也可以用其宏观量 $Q$ 和 $C$ (或 $V$ 和 $C$) 来表示。这两个常用的表达式是：

$U = \frac{Q^2}{2C} \quad \text{(适用于孤立系统，电荷 } Q \text{ 恒定)}$

$U = \frac{1}{2}CV^2 \quad \text{(适用于连接到电源的系统，电势差 } V \text{ 恒定)}$

这两个公式是等价的，通过 $Q=CV$ 可以相互转换。这个关系意味着，如果我们能通[过积分](@keyword=over_integration|lang=zh-CN|style=Feynman)[电场能量密度](@keyword=electric_field_energy_density|lang=zh-CN|style=Feynman)计算出总能量 $U$，就可以反过来求出电容 $C$。

让我们用这种[能量法](@keyword=energy_methods|lang=zh-CN|style=Feynman)重新计算同轴电缆的单位长度电容 [@problem_id:1786868]。我们已经知道，对于带[电荷密度](@keyword=charge_density|lang=zh-CN|style=Feynman)为 $\lambda$ 的电缆，其间的[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)为 $E(r) = \frac{\lambda}{2\pi\epsilon r}$。单位长度电缆储存的能量可以通过对一个长度为 $L=1$ 的[环形体](@keyword=toroid|lang=zh-CN|style=Feynman)积积分得到：

$U_L = \int_{a}^{b} \frac{1}{2}\epsilon E(r)^2 (2\pi r \cdot 1) dr = \int_{a}^{b} \frac{1}{2}\epsilon \left(\frac{\lambda}{2\pi\epsilon r}\right)^2 2\pi r dr$

$U_L = \frac{\lambda^2}{4\pi\epsilon} \int_{a}^{b} \frac{1}{r} dr = \frac{\lambda^2}{4\pi\epsilon} \ln\left(\frac{b}{a}\right)$

现在，使用关系式 $U_L = \frac{\lambda^2}{2C_L}$，我们得到：

$\frac{\lambda^2}{2C_L} = \frac{\lambda^2}{4\pi\epsilon} \ln\left(\frac{b}{a}\right)$

解出 $C_L$，我们得到 $C_L = \frac{2\pi\epsilon}{\ln(b/a)}$，这与之前用[电势法](@keyword=potentiometry|lang=zh-CN|style=Feynman)得到的结果完全一致。[能量法](@keyword=energy_methods|lang=zh-CN|style=Feynman)在处理复杂几何或场[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)时可能更具优势。

#### [静电力](@keyword=electrostatic_forces|lang=zh-CN|style=Feynman)计算

[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)极板之间的[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)会产生相互作用力。这些力可以通过[能量法](@keyword=energy_methods|lang=zh-CN|style=Feynman)精确计算。考虑[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)的一个几何参数发生微小变化 $dx$（例如，极板间距的改变），系统能量 $U$ 的变化与外力做的功 $dW_{ext}$ 以及电源做的功 $dW_{batt}$ 有关。根据[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)，[广义力](@keyword=generalized_forces|lang=zh-CN|style=Feynman) $F_x$ 可以表示为 $U$ 对 $x$ 的导数。但需要注意的是，具体表达式取决于约束条件。

1.  **孤立系统（恒定[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $Q$）**：如果[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)与外界电路断开，其[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $Q$ 保持不变。此时，外力所做的功等于系统[静电能](@keyword=electrostatic_energy|lang=zh-CN|style=Feynman)量的增加量，$dW_{ext} = dU$。因此，[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)力 $F_{elec}$ 与外[力平衡](@keyword=force_balance|lang=zh-CN|style=Feynman)，$F_{elec} \cdot dx = -dU$。所以：

    $F_x = -\left(\frac{\partial U}{\partial x}\right)_Q = -\frac{\partial}{\partial x}\left(\frac{Q^2}{2C(x)}\right) = \frac{Q^2}{2C^2}\frac{dC}{dx}$

    例如，在一个微[机电系统](@keyword=electromechanical_systems|lang=zh-CN|style=Feynman)（MEMS）中，一个可移动的极板在重力、弹簧力和[静电力](@keyword=electrostatic_forces|lang=zh-CN|style=Feynman)作用下[达到平衡](@keyword=equilibration|lang=zh-CN|style=Feynman) [@problem_id:1786873]。对于一个[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为 $Q$、面积为 $A$ 的平行板电容器，其电容为 $C(x) = \epsilon_0 A/x$。它所受的[静电吸引](@keyword=electrostatic_attraction|lang=zh-CN|style=Feynman)力为：

    $F_{elec} = -\frac{\partial}{\partial x}\left(\frac{Q^2 x}{2\epsilon_0 A}\right) = -\frac{Q^2}{2\epsilon_0 A}$

    这个力是吸[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)（指向 $x$ 减小的方向），且大小不依赖于间距 $x$。在平衡时，这个静电力、弹簧力 $k(x-L_0)$ 和重力 $mg$ 必须相互抵消。

2.  **恒定电压 $V$ 系统**：如果[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)始终连接到电压为 $V$ 的电源上，当其几何参数变化时，[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $Q=C(x)V$ 也会变化。为了维持电压恒定，电池会做功 $dW_{batt} = V dQ = V^2 dC$。根据[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)，系统静电能量的变化 $dU$ 等于电池做的功 $dW_{batt}$ 与[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)力做的功 $dW_{elec}$ 之和，即 $dU = dW_{batt} + dW_{elec}$。因此，[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)力做的功为 $dW_{elec} = dU - dW_{batt}$。代入 $U = \frac{1}{2}CV^2$，我们有 $dU = \frac{1}{2}V^2 dC$。所以[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)力做的功为：
    
    $dW_{elec} = \frac{1}{2}V^2 dC - V^2 dC = -\frac{1}{2}V^2 dC$
    
    噢，这个推导是错误的。正确的[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)关系是，电池做的功 $dW_{batt}$ 分别转化为系统[储能](@keyword=energy_storage|lang=zh-CN|style=Feynman)的增加 $dU$ 和[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)对外做的功 $dW_{elec}$，即 $dW_{batt} = dU + dW_{elec}$。因此[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)力做的功是：
    
    $dW_{elec} = dW_{batt} - dU = V^2 dC - \frac{1}{2}V^2 dC = \frac{1}{2}V^2 dC$
    
    因此，[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)力为：
    
    $F_x = \frac{dW_{elec}}{dx} = +\frac{1}{2}V^2 \frac{dC}{dx}$

    这里的正号表示，在恒定电压下，系统倾向于向电容增大的方向运动。一个典型的例子是插入[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)板时受到的力 [@problem_id:1786888]。当一个[介电常数](@keyword=dielectric_constant|lang=zh-CN|style=Feynman)为 $\kappa$ 的介质板被插入平行板电容器时，电容会增加。因此，[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)会对介质板产生一个将其拉入[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)的力。如果实验测得在恒定电压 $V$ 下，这个力的大小为常数 $F_0$，我们可以反推电容随插入深度 $x$ 的变化关系：

    $F_0 = \frac{1}{2}V^2 \frac{dC}{dx} \implies \frac{dC}{dx} = \frac{2F_0}{V^2}$

    积分可得 $C(x) = \frac{2F_0}{V^2}x + C_0$。其中积分常数 $C_0$ 是 $x=0$ 时（即没有介质板插入时）的电容，即 $C(0) = \epsilon_0 L^2 / d$。

### 一个类比：电容与电阻的关系

在处理充满均匀、弱导[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)的[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)时，存在一个深刻而优美的对偶关系。考虑一个由两个导体组成的系统，完全[浸没](@keyword=submersions|lang=zh-CN|style=Feynman)在一种既是完美[电介质](@keyword=dielectric_materials|lang=zh-CN|style=Feynman)（[介电常数](@keyword=dielectric_constant|lang=zh-CN|style=Feynman)为 $\epsilon$）又是欧姆导体（电导率为 $\sigma$，电阻率为 $\rho = 1/\sigma$）的均匀介质中。

对于给定的导体几何形状和它们之间的电势差 $V$，静态[电场](@keyword=electric_field|lang=zh-CN|style=Feynman) $\vec{E}$ 的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)由[拉普拉斯方程](@keyword=laplace_s_equation|lang=zh-CN|style=Feynman) $\nabla^2 \phi = 0$ 及其在导体表面的边界条件唯一确定。这个[电场](@keyword=electric_field|lang=zh-CN|style=Feynman) $\vec{E}$ 同时驱动着两种现象：
-   它在导体表面感应出面电荷密度，总[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)为 $Q = CV$。
-   它在介质中驱动一个[电流密度](@keyword=current_density|lang=zh-CN|style=Feynman) $\vec{J} = \sigma \vec{E}$，导致一个从一个导体流向另一个导体的总[漏电流](@keyword=leakage_current|lang=zh-CN|style=Feynman) $I$。系统的电阻 $R=V/I$。

由于[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman) $Q$ 和电流 $I$ 都源于同一个[电场](@keyword=electric_field|lang=zh-CN|style=Feynman) $\vec{E}$ 的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)，它们的比值应该只与介质的属性有关，而与几何形状无关。我们可以正式地推导这个关系。总[漏电流](@keyword=leakage_current|lang=zh-CN|style=Feynman) $I$ 是[电流密度](@keyword=current_density|lang=zh-CN|style=Feynman) $\vec{J}$ 穿过包围其中一个导体的任意闭合[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman) $S$ 的通量：

$I = \oint_S \vec{J} \cdot d\vec{A} = \oint_S \sigma \vec{E} \cdot d\vec{A} = \sigma \oint_S \vec{E} \cdot d\vec{A}$

根据[高斯定律](@keyword=gauss_s_law|lang=zh-CN|style=Feynman)，$\oint_S \vec{E} \cdot d\vec{A} = Q/\epsilon$。代入上式，我们得到：

$I = \sigma \frac{Q}{\epsilon}$

将 $I=V/R$ 和 $Q=CV$ 代入，我们得到：

$\frac{V}{R} = \frac{\sigma}{\epsilon} (CV) \implies RC = \frac{\epsilon}{\sigma} = \epsilon \rho$

这个简洁的关系式 $RC = \epsilon \rho$ 是一个强大的工具。它意味着如果我们通过计算或测量得知了一个特定几何结构的电阻 $R$，就可以立即得到相同几何结构的电容 $C$，反之亦然。例如，对于一个双线馈线电缆，如果已知其单位长度电阻为 $R_L = \frac{\rho}{\pi} \operatorname{arccosh}(\frac{d}{2a})$ [@problem_id:1786910]，那么它的单位长度电容 $C_L$ 必定是：

$C_L = \frac{\epsilon \rho}{R_L} = \frac{\epsilon \rho}{\frac{\rho}{\pi} \operatorname{arccosh}(\frac{d}{2a})} = \frac{\pi \epsilon}{\operatorname{arccosh}(\frac{d}{2a})}$

这种方法绕过了计算[电场](@keyword=electric_field|lang=zh-CN|style=Feynman)和[电势](@keyword=electric_potential|lang=zh-CN|style=Feynman)的复杂积分，为某些问题提供了优雅的捷径。