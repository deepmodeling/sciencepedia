## 引言
电-力耦合与压电效应是现代工程与[材料科学](@entry_id:152226)中的一个核心概念，描述了特定材料在机械能与电能之间相互转换的能力。这种独特的性质使[压电材料](@entry_id:197563)成为从精密传感器、微型执行器到[能量收集](@entry_id:144965)器和射频滤波器等众多高科技设备不可或缺的组成部分。尽管其应用广泛，但要在理论层面深刻理解其复杂的物理机制，并将其有效地应用于解决实际工程问题，往往存在着知识上的鸿沟。许多学习者要么停留在现象的定性描述，要么陷入繁复的数学公式，难以将二者融会贯通。

本文旨在系统性地弥合这一差距，为读者提供一个从基础原理到前沿应用的完整知识框架。通过结构化的学习路径，您将能够自信地分析和解决复杂的[压电](@entry_id:268187)耦合问题。

- 在 **第一章：原理与机制** 中，我们将回归物理本源，从[电介质](@entry_id:147163)理论出发，揭示晶体对称性如何决定压电效应的产生，并详细推导线弹性[压电](@entry_id:268187)本构关系。您将理解线性[压电](@entry_id:268187)与铁电性的本质区别，并掌握构建完整边值问题的数学框架。

- 在 **第二章：应用与跨学科交叉** 中，我们将理论付诸实践，探讨如何通过电气边界条件调控[材料的机械性能](@entry_id:158743)，分析[压电材料](@entry_id:197563)在传感、驱动、[复合材料](@entry_id:139856)设计中的核心作用，并涉足热、化学、断裂力学等[多物理场耦合](@entry_id:171389)的前沿领域。

- 在 **第三章：动手实践** 中，您将通过一系列精心设计的计算练习，亲手推导解析解，实现[坐标变换](@entry_id:172727)，并对比不同的[非线性](@entry_id:637147)求解策略，从而将理论知识转化为可操作的计算技能。

本文将带领您开启一段探索压电世界的旅程，首先让我们深入其最核心的基石——原理与机制。

## 原理与机制

本章旨在系统地阐述电-力耦合与[压电效应](@entry_id:138222)的核心原理和关键机制。我们将从[电介质](@entry_id:147163)中[电场](@entry_id:194326)的基本概念出发，深入探讨[晶体对称性](@entry_id:198772)如何决定[压电效应](@entry_id:138222)的存在与否，然后详细推导并解释线弹性范围内的压电[本构关系](@entry_id:186508)。此外，我们还将区分线性和铁电两种[压电材料](@entry_id:197563)，并建立描述压电行为的完整[数学物理](@entry_id:265403)模型。最后，本章将展望有限变形理论，为更高级的[非线性](@entry_id:637147)分析奠定基础。

### [电介质](@entry_id:147163)中的[静电场](@entry_id:268546)基本理论

在研究[压电材料](@entry_id:197563)之前，我们必须首先理解[电场](@entry_id:194326)与[电介质](@entry_id:147163)相互作用的基本规律。在[电介质](@entry_id:147163)内部，存在三种描述电现象的基本矢量场：**[电场](@entry_id:194326)强度 (electric field)** $\mathbf{E}$、**[电极化强度](@entry_id:141475) (polarization)** $\mathbf{P}$ 和**[电位移场](@entry_id:273493) (electric displacement)** $\mathbf{D}$。

[电场](@entry_id:194326)强度 $\mathbf{E}$ 是一个宏观平均场，它源于空间中所有[电荷](@entry_id:275494)——无论是自由移动的**[自由电荷](@entry_id:264392)**（密度为 $\rho_f$），还是束缚在原子或分子内部的**束缚[电荷](@entry_id:275494)**（密度为 $\rho_b$）。根据高斯定律，总电荷密度 $\rho = \rho_f + \rho_b$ 决定了[电场](@entry_id:194326)强度的散度：
$$
\nabla \cdot \mathbf{E} = \frac{\rho_f + \rho_b}{\epsilon_0}
$$
其中 $\epsilon_0$ 是[真空介电常数](@entry_id:204253)。

当介质置于[电场](@entry_id:194326)中时，其内部的微观[带电粒子](@entry_id:160311)会重新排布，形成大量的微观[电偶极子](@entry_id:186870)。**[电极化强度](@entry_id:141475)** $\mathbf{P}$ 被定义为单位体积内这些电偶极矩的矢量和，它定量描述了介质的电学响应。束缚[电荷](@entry_id:275494)的出现正是电极化在空间上不[均匀分布](@entry_id:194597)的宏观体现。可以证明，束缚[电荷密度](@entry_id:144672)与电[极化强度的散度](@entry_id:190771)之间存在以下关系 ：
$$
\rho_b = -\nabla \cdot \mathbf{P}
$$
这个关系式表明，当电[极化场](@entry_id:197617) $\mathbf{P}$ 在空间中存在变化（即 $\nabla \cdot \mathbf{P} \neq 0$）时，就会在局部产生净的束缚[电荷](@entry_id:275494)。

将此关系代入[高斯定律](@entry_id:141493)，我们得到：
$$
\nabla \cdot \mathbf{E} = \frac{\rho_f - \nabla \cdot \mathbf{P}}{\epsilon_0}
$$
整理后可得：
$$
\nabla \cdot (\epsilon_0 \mathbf{E} + \mathbf{P}) = \rho_f
$$
这个结果启发我们定义一个[辅助场](@entry_id:155519)，即**[电位移场](@entry_id:273493)** $\mathbf{D}$，其定义为：
$$
\mathbf{D} \equiv \epsilon_0 \mathbf{E} + \mathbf{P}
$$
引入 $\mathbf{D}$ 场的巨大优势在于，它将[电场](@entry_id:194326)的源与材料的响应（极化）分离开来。现在，[高斯定律](@entry_id:141493)可以写成一个更简洁的形式，其散度仅由我们能直接控制的自由电荷密度 $\rho_f$ 决定：
$$
\nabla \cdot \mathbf{D} = \rho_f
$$
这三个场（$\mathbf{E}$, $\mathbf{P}$, $\mathbf{D}$）在物理意义上有所区别：$\mathbf{E}$ 是总作用[力场](@entry_id:147325)，$\mathbf{P}$ 是材料的响应，而 $\mathbf{D}$ 的引入则简化了对由[自由电荷](@entry_id:264392)产生的场的描述。对于许多线性、各向同性的[电介质](@entry_id:147163)，在弱场下，其[极化强度](@entry_id:188176) $\mathbf{P}$ 与[电场](@entry_id:194326)强度 $\mathbf{E}$ 成正比：
$$
\mathbf{P} = \chi_e \epsilon_0 \mathbf{E}
$$
其中 $\chi_e$ 是无量纲的**[电极化率](@entry_id:144209) (electric susceptibility)**。将此**[本构关系](@entry_id:186508) (constitutive relation)** 代入 $\mathbf{D}$ 的定义，可得：
$$
\mathbf{D} = \epsilon_0 (1 + \chi_e) \mathbf{E} = \epsilon \mathbf{E}
$$
这里，$\epsilon = \epsilon_0 (1 + \chi_e)$ 被称为材料的**[介电常数](@entry_id:146714) (permittivity)**。需要强调的是，即使在没有外加[电场](@entry_id:194326) $\mathbf{E}$ 的情况下，某些材料（如压电体）也可能因为机械应力而产生非零的[电极化强度](@entry_id:141475) $\mathbf{P}$ 。

### [压电性](@entry_id:144525)的物理基础：[晶体对称性](@entry_id:198772)

[压电效应](@entry_id:138222)是指某些晶体在受到机械应力时产生电极化（**[正压电效应](@entry_id:181737)**），或者在置于[电场](@entry_id:194326)中时发生机械形变（**[逆压电效应](@entry_id:261933)**）的现象。这种电-力耦合行为并非所有材料都具备，其根源在于材料的[晶体结构](@entry_id:140373)对称性。

物理学中的一个基本原理是**诺依曼原理 (Neumann's Principle)**，它指出：材料的任何物理性质所表现出的对称性，必须包含其[晶体结构](@entry_id:140373)的[点群对称性](@entry_id:141230)。简而言之，材料的宏观属性不能比其微观结构更“不对称”。

压电效应是一种线性耦合，它通过一个三阶张量（[压电张量](@entry_id:141969)）将一个[极性矢量](@entry_id:184542)（如[电极化强度](@entry_id:141475) $\mathbf{P}$）和一个二阶对称张量（如应力 $\boldsymbol{\sigma}$ 或应变 $\boldsymbol{\epsilon}$）联系起来。为了探究何种[晶体结构](@entry_id:140373)允许压电效应的存在，我们只需考察**空间反演 (spatial inversion)** 这一对称操作。空间反演操作将空间中每一点的坐标 $\mathbf{x}$ 变为 $-\mathbf{x}$。在该操作下：
- [极性矢量](@entry_id:184542)（如 $\mathbf{P}$ 和 $\mathbf{E}$）是**奇性**的，即 $\mathbf{P} \rightarrow -\mathbf{P}$。
- 二阶[对称张量](@entry_id:148092)（如 $\boldsymbol{\sigma}$ 和 $\boldsymbol{\epsilon}$）是**偶性**的，即 $\boldsymbol{\epsilon} \rightarrow \boldsymbol{\epsilon}$。

对于一个具有**中心对称性 (centrosymmetry)** 的晶体（即其点群包含空间反演操作），根据诺依曼原理，其所有物理性质张量必须在空间反演下保持不变。考虑一个描述[压电](@entry_id:268187)耦合的能量项，其形式为 $w_{\text{piezo}} \propto P_i \epsilon_{jk}$。在空间反演下，该项变为 $(-P_i)(+\epsilon_{jk}) = -P_i \epsilon_{jk}$，即该能量项是奇性的。为了使总能量（一个标量）在反演下不变（偶性），这个奇性项的系数（即[压电张量](@entry_id:141969)）必须为零。因此，任何[中心对称](@entry_id:144242)的晶体都不能表现出[压电效应](@entry_id:138222)  。在32个[晶体点群](@entry_id:183880)中，有11个是中心对称的，它们都不具有[压电性](@entry_id:144525)。剩下的21个[非中心对称](@entry_id:157488)点群中，除了一个特殊情况（点群432）外，其余20个都允许[压电效应](@entry_id:138222)的存在。

与此相对，**挠曲电效应 (flexoelectricity)** 描述了电极化与应变**梯度**之间的线性耦合，其能量项形式为 $w_{\text{flexo}} \propto P_i \frac{\partial \epsilon_{jk}}{\partial x_l}$。由于[梯度算子](@entry_id:275922) $\nabla$ 也是奇性的（$\nabla \rightarrow -\nabla$），[应变梯度](@entry_id:204192) $\nabla\boldsymbol{\epsilon}$ 是奇性的。因此，能量项 $P_i (\nabla\boldsymbol{\epsilon})$ 是偶性的（奇性乘以奇性），在空间反演下保持不变。这意味着挠曲电耦合在所有32个[晶体点群](@entry_id:183880)中都是对称性允许的，使其成为一种普遍存在的效应，与[压电效应](@entry_id:138222)的对称性限制形成鲜明对比 。

### 线性压电[本构关系](@entry_id:186508)

对于表现出压电效应的[非中心对称材料](@entry_id:181206)，在小应变和小[电场](@entry_id:194326)假设下，其电-力耦合行为可以通过线性的[本构方程](@entry_id:138559)来描述。这些方程可以从一个热力学势函数系统地推导出来。

#### 热力学势与[本构方程](@entry_id:138559)

选择应变张量 $\mathbf{S}$ 和[电场](@entry_id:194326)强度 $\mathbf{E}$ 作为独立状态变量，我们可以定义一个**电焓密度 (electric enthalpy density)** $\mathcal{H}(\mathbf{S}, \mathbf{E})$。对于线性材料，$\mathcal{H}$ 是一个二次型函数：
$$
\mathcal{H}(\mathbf{S}, \mathbf{E}) = \frac{1}{2} S_{ij} c^{E}_{ijkl} S_{kl} - e_{kij} E_k S_{ij} - \frac{1}{2} E_i \epsilon^{S}_{ij} E_j
$$
其中，$c^{E}_{ijkl}$ 是恒定[电场](@entry_id:194326)下的[弹性张量](@entry_id:170728)，$e_{kij}$ 是压[电应力张量](@entry_id:194421)，$\epsilon^{S}_{ij}$ 是恒定应变下的[介电张量](@entry_id:194185)。

[应力张量](@entry_id:148973) $\mathbf{T}$ 和[电位移矢量](@entry_id:197092) $\mathbf{D}$ 作为[功共轭](@entry_id:194957)量，可以通过对电焓求偏导数得到 ：
$$
T_{ij} = \frac{\partial \mathcal{H}}{\partial S_{ij}} = c^{E}_{ijkl} S_{kl} - e_{kij} E_k
$$
$$
D_i = -\frac{\partial \mathcal{H}}{\partial E_i} = e_{ikl} S_{kl} + \epsilon^{S}_{ij} E_j
$$
这组方程被称为**应力-[电荷](@entry_id:275494)形式 (stress-charge form)** 的[本构关系](@entry_id:186508)，因为它表达了应力 $\mathbf{T}$ 和[电位移](@entry_id:269383) $\mathbf{D}$ 作为应变 $\mathbf{S}$ 和[电场](@entry_id:194326) $\mathbf{E}$ 的函数。

#### 不同形式的本构关系及其转换

通过代数变换，可以得到其他形式的[本构关系](@entry_id:186508)。例如，将应力-[电荷](@entry_id:275494)形式的第一式改写为 $\mathbf{S}$ 的表达式，并代入第二式，可以得到以应力 $\mathbf{T}$ 和[电场](@entry_id:194326) $\mathbf{E}$ 为[自变量](@entry_id:267118)的**应变-[电荷](@entry_id:275494)形式 (strain-charge form)** ：
$$
S_{ij} = s^{E}_{ijkl} T_{kl} + d_{kij} E_k
$$
$$
D_i = d_{ikl} T_{kl} + \epsilon^{T}_{ij} E_j
$$
其中，$s^{E}_{ijkl}$ 是恒定[电场](@entry_id:194326)下的柔度张量（$c^{E}$ 的逆），$d_{kij}$ 是[压电](@entry_id:268187)应变张量，$\epsilon^{T}_{ij}$ 是恒定应力下的[介电张量](@entry_id:194185)。这些不同形式的本构系数之间存在明确的换算关系，例如：$d_{kij} = e_{kmn} s^{E}_{mnij}$ 以及 $\epsilon^{T}_{ij} = \epsilon^{S}_{ij} + d_{imn} e_{jmn}$。

#### Voigt 记法与张量分量的缩减

在实际计算中，处理[高阶张量](@entry_id:200122)很不方便。因此，工程上广泛采用 **Voigt 记法**，将二阶[对称张量](@entry_id:148092)（应力 $\mathbf{T}$ 和应变 $\mathbf{S}$）表示为 $6 \times 1$ 的列向量，将四阶的弹性/柔度[张量表示](@entry_id:180492)为 $6 \times 6$ 的矩阵，三阶的[压电张量](@entry_id:141969)表示为 $3 \times 6$ 或 $6 \times 3$ 的矩阵。

映射规则通常为：
$11 \to 1, \quad 22 \to 2, \quad 33 \to 3, \quad (23, 32) \to 4, \quad (13, 31) \to 5, \quad (12, 21) \to 6$

使用 Voigt 记法时，必须注意剪切应变分量的定义。为了保持功密度的表达式 $T_{ij}S_{ij}$ 在张量和矩阵形式下不变，如果应力向量的分量为 $T_4 = T_{23}$，那么应变向量的相应分量必须是**工程剪切应变** $S_4 = 2S_{23}$ 。

晶体对称性不仅决定了[压电张量](@entry_id:141969)是否为零，还决定了其非零分量的具体形式。通过将[晶体点群](@entry_id:183880)的[对称操作](@entry_id:143398)（如旋转、镜像）应用于[压电张量](@entry_id:141969)，并要求张量不变，可以推导出其简化形式。例如：
- 对于具有 $6mm$ [点群对称性](@entry_id:141230)的[纤锌矿结构](@entry_id:160078)晶体（如 GaN, ZnO），其[压电](@entry_id:268187)应力矩阵 $\mathbf{e}$ 具有以下形式，包含3个独立常数：$e_{31}, e_{33}, e_{15}$ 。
$$
\mathbf{e} =
\begin{pmatrix}
0  0  0  0  e_{15}  0 \\
0  0  0  e_{15}  0  0 \\
e_{31}  e_{31}  e_{33}  0  0  0
\end{pmatrix}
$$
- 对于具有 $32$ [点群对称性](@entry_id:141230)的 $\alpha$-石英，其[压电](@entry_id:268187)应变张量 $d_{i\alpha}$ 具有不同的形式，仅包含2个独立常数：$d_{11}$ 和 $d_{14}$ 。

### [铁电性](@entry_id:144234)：一种特殊的[压电](@entry_id:268187)现象

在所有[压电材料](@entry_id:197563)中，有一类特殊的材料被称为**铁电体 (ferroelectrics)**，如[钛酸钡](@entry_id:161741) ($\text{BaTiO}_3$) 和锆钛酸铅 (PZT)。与石英等线性压电体相比，[铁电体](@entry_id:138549)具有独特的物理性质。

铁电性的核心特征是**自发极化 (spontaneous polarization)**。在低于某个临界温度——**居里温度 ($T_C$)** 时，[铁电体](@entry_id:138549)的[晶体结构](@entry_id:140373)会自发发生[相变](@entry_id:147324)，从高对称性的非[极性相](@entry_id:161819)（顺电相）转变为低对称性的[极性相](@entry_id:161819)（铁电相）。根据 **Landau 理论**，这个过程可以被描述为一个[自由能函数](@entry_id:749582)从单[势阱](@entry_id:151413)变为[双势阱](@entry_id:171252)（或多[势阱](@entry_id:151413)）的过程。在零[电场](@entry_id:194326)下，系统存在两个或多个[能量简并](@entry_id:203091)的稳定状态，对应于非零的[自发极化](@entry_id:141025) $\mathbf{P}_s$ 。

这种[自发极化](@entry_id:141025)是可被外[电场](@entry_id:194326)翻转的。当施加的[电场](@entry_id:194326)超过一个阈值——**[矫顽场](@entry_id:160296) ($E_c$)** 时，[材料的极化](@entry_id:271610)方向会发生反转。这个翻转过程是不可逆的，并在 $P-E$ 图上表现为标志性的**[电滞回线](@entry_id:182188) (hysteresis loop)**。

由于铁电体的极性结构，它必然也是[压电的](@entry_id:268187)。然而，反之不成立：并非所有压电体都是铁电体。线性压电体（如石英）没有自发极化，其电极化是外加应力或[电场](@entry_id:194326)的线性、可[逆响应](@entry_id:274510)，不存在电滞和[矫顽场](@entry_id:160296) 。

在工业应用中，许多高性能[压电材料](@entry_id:197563)（如PZT）是以[陶瓷](@entry_id:148626)形式存在的。刚制备好的[陶瓷](@entry_id:148626)由无数个取向随机的晶粒构成，每个晶粒内部又包含若干个自发极化方向不同的**电畴 (domains)**，导致宏观上净极化为零，不表现出压电性。通过施加一个强大的直流[电场](@entry_id:194326)（通常在高温下）进行**极化 (poling)** 处理，可以驱动电畴转向，使其自发极化方向尽可能与外[电场](@entry_id:194326)方向对齐。撤去[电场](@entry_id:194326)后，大部分电畴的取向被“冻结”，形成宏观的**[剩余极化](@entry_id:160843) (remanent polarization)**，从而使整个陶瓷体表现出强烈的[压电效应](@entry_id:138222)。极化后的[陶瓷](@entry_id:148626)通常具有横观各向同性（如 $4mm$ 或 $\infty mm$ [点群对称性](@entry_id:141230)），其[压电张量](@entry_id:141969)也反映了这种对称性 。需要警惕的是，在纳米尺度下，观测到的 $P-E$ [电滞回线](@entry_id:182188)不一定是铁电性的明确证据，因为[漏电流](@entry_id:261675)、[电荷](@entry_id:275494)注入与俘获等效应也可能产生类似的滞后行为 。

### 线性[压电](@entry_id:268187)问题的控制方程与定解条件

为了对压电结构进行力学分析，需要建立一套完整的[数学物理](@entry_id:265403)模型，包括控制方程、[本构关系](@entry_id:186508)和边界条件。

#### 准静态电磁近似

在大多数[压电](@entry_id:268187)应用中，机械变形和[电场](@entry_id:194326)变化的时间尺度远大于[电磁波传播](@entry_id:272130)所需的时间。因此，可以采用**准静态电磁 (electro-quasi-static, EQS)** 近似。在该近似下，我们忽略麦克斯韦方程中[磁场](@entry_id:153296)的时间变化项（[法拉第感应定律](@entry_id:146175) $\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$ 中的右侧项），这导致[电场](@entry_id:194326)是无旋的 ：
$$
\nabla \times \mathbf{E} \approx \mathbf{0}
$$
这一条件保证了[电场](@entry_id:194326)可以表示为一个标量[电势](@entry_id:267554) $\phi$ 的梯度：
$$
\mathbf{E} = -\nabla \phi
$$
这个近似极大地简化了问题，将完整的[电磁场](@entry_id:265881)问题[解耦](@entry_id:637294)为[静电场](@entry_id:268546)问题。

#### 强形式的[边值问题](@entry_id:193901)

一个完整的线性压电[边值问题](@entry_id:193901)（BVP）的强形式由以下几部分组成 ：

1.  **控制方程 (Governing Equations)**，在区域 $\Omega$ 内成立：
    -   [机械平衡](@entry_id:148830)方程（忽略[惯性力](@entry_id:169104)）：$\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}$
    -   静[电高斯定律](@entry_id:141493)：$\nabla \cdot \mathbf{D} = \rho_f$

2.  **几何关系 (Kinematic Relations)**：
    -   [应变-位移关系](@entry_id:173321)：$\boldsymbol{\epsilon}(\mathbf{u}) = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^\top)$
    -   [电场](@entry_id:194326)-[电势](@entry_id:267554)关系：$\mathbf{E} = -\nabla \phi$

3.  **本构关系 (Constitutive Relations)**：
    -   例如，应力-[电荷](@entry_id:275494)形式：$\boldsymbol{\sigma}(\boldsymbol{\epsilon}, \mathbf{E}), \mathbf{D}(\boldsymbol{\epsilon}, \mathbf{E})$

4.  **边界条件 (Boundary Conditions)**，在边界 $\partial \Omega$ 上给出：
    -   力学边界：在 $\Gamma_u$ 上给定**位移** $\mathbf{u} = \bar{\mathbf{u}}$ (Dirichlet)，在 $\Gamma_t$ 上给定**面力** $\boldsymbol{\sigma}\mathbf{n} = \bar{\mathbf{t}}$ (Neumann)。
    -   电学边界：在 $\Gamma_\phi$ 上给定**[电势](@entry_id:267554)** $\phi = \bar{\phi}$ (Dirichlet)，在 $\Gamma_q$ 上给定**表面[自由电荷](@entry_id:264392)密度** $\mathbf{D} \cdot \mathbf{n} = \bar{q}$ (Neumann)。

#### [适定性](@entry_id:148590)与唯一性

对于一个[边值问题](@entry_id:193901)，解的存在性和唯一性至关重要。对于纯 Neumann 问题（即 $\Gamma_u$ 或 $\Gamma_\phi$ 的测度为零），必须满足特定的**相容性条件 (compatibility conditions)** 才能保证解的存在 ：
-   **力学相容性**：当 $\Gamma_u = \emptyset$ 时，所有外力（[体力](@entry_id:174230) $\mathbf{b}$ 和面力 $\bar{\mathbf{t}}$）必须自身平衡，即合力与[合力矩](@entry_id:166772)均为零。若满足此条件，位移解 $\mathbf{u}$ 仅在相差一个刚体运动（平动和转动）的意义下是唯一的。
-   **电学相容性**：当 $\Gamma_\phi = \emptyset$ 时，流入边界的总自由电荷必须等于体内的总[自由电荷](@entry_id:264392)。若满足此条件，[电势](@entry_id:267554)解 $\phi$ 仅在相差一个任意常数的意义下是唯一的（[规范自由度](@entry_id:160491)）。

在数值求解时，必须通过施加额外的约束来消除这些不确定性，以获得唯一的数值解。

### 有限变形理论框架

当材料经历大变形时，小应变假设不再成立，必须采用**有限变形 (finite deformation)** 理论。在此框架下，一个核心要求是**[客观性原理](@entry_id:185412) (principle of frame indifference)**，即[本构关系](@entry_id:186508)不能依赖于观察者的[参考系](@entry_id:169232)。

考虑一个从参考构型（坐标 $\mathbf{X}$）到当前构型（坐标 $\mathbf{x}$）的变形。其变形梯度为 $\mathbf{F} = \nabla_{\! \mathbf{X}} \mathbf{x}$。在观察者变换 $\mathbf{x}^{*} = \mathbf{Q}\mathbf{x} + \mathbf{c}$（其中 $\mathbf{Q}$ 是旋转矩阵）下，不同的物理量具有不同的变换性质 ：
-   变形梯度 $\mathbf{F}$ 不是客观的：$\mathbf{F}^* = \mathbf{Q}\mathbf{F}$。
-   [右柯西-格林张量](@entry_id:174156) $\mathbf{C} = \mathbf{F}^\top\mathbf{F}$ 是客观的（不变）：$\mathbf{C}^* = \mathbf{C}$。
-   [左柯西-格林张量](@entry_id:186163) $\mathbf{b} = \mathbf{F}\mathbf{F}^\top$ 是客观的：$\mathbf{b}^* = \mathbf{Q}\mathbf{b}\mathbf{Q}^\top$。
-   参考[电场](@entry_id:194326) $\mathbf{E}_0 = -\nabla_{\! \mathbf{X}}\phi$ 是客观的（不变）：$\mathbf{E}_0^* = \mathbf{E}_0$。
-   空间[电场](@entry_id:194326) $\mathbf{e} = -\nabla_{\! \mathbf{x}}\phi$ 是客观的：$\mathbf{e}^* = \mathbf{Q}\mathbf{e}$。

为了构建一个客观的能量密度函数，必须恰当地选择其[自变量](@entry_id:267118)。
-   一个纯**拉格朗日 (Lagrangian)** 形式的能量密度 $W(\mathbf{C}, \mathbf{E}_0)$ 是自动客观的，因为它的所有自变量在观察者变换下都是[不变量](@entry_id:148850)。这是构建[非线性](@entry_id:637147)[本构模型](@entry_id:174726)最直接可靠的方法 。
-   一个纯**欧拉 (Eulerian)** 形式的能量密度 $\psi(\mathbf{b}, \mathbf{e})$ 则不是自动客观的。为了满足客观性要求 $\psi(\mathbf{Q}\mathbf{b}\mathbf{Q}^\top, \mathbf{Q}\mathbf{e}) = \psi(\mathbf{b}, \mathbf{e})$，函数 $\psi$ 必须写成一组[标量不变量](@entry_id:193787)的函数。例如，对于各向同性材料，这些[不变量](@entry_id:148850)可以是 $\mathbf{b}$ 的[主不变量](@entry_id:193522)以及 $\mathbf{e}$ 和 $\mathbf{b}$ 的耦合[不变量](@entry_id:148850)，如 $\mathbf{e} \cdot \mathbf{e}$, $\mathbf{e} \cdot \mathbf{b}\mathbf{e}$, 等等。一种正确的构造方式是选择 $\psi(I_1, I_2, I_3, I_4, \dots)$，其中 $I_1=\mathrm{tr}\,\mathbf{b}$，$I_2=\mathrm{tr}\,\mathrm{cof}\,\mathbf{b}$，$I_3=\det\mathbf{b}$，$I_4=\mathbf{e} \cdot \mathbf{b}^{-1}\mathbf{e}$ 都是[标量不变量](@entry_id:193787) 。

对有限变形电-力耦合问题的正确建模是[计算固体力学](@entry_id:169583)中的一个前沿领域，它为分析[大变形](@entry_id:167243)下的[压电](@entry_id:268187)器件和柔性电子设备提供了理论基础。