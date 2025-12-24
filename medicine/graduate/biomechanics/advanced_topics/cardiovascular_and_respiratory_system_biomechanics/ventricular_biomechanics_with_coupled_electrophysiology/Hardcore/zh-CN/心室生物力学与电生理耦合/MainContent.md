## 引言
心脏是人体最精密的泵，其功能依赖于电[信号传导](@entry_id:139819)与肌肉机械收缩之间复杂而精准的协同作用。心室的每一次搏动都始于一个电脉冲，它触发了[心肌细胞](@entry_id:898045)的收缩，产生驱动血液流动的力量；反过来，[心肌](@entry_id:924326)的机械变形又会影响其电生理特性，形成一个精密的反馈回路。尽管我们对这一过程的各个组成部分有所了解，但要将[电生理学](@entry_id:156731)、连续介质力学和[细胞生物学](@entry_id:143618)整合到一个统一的定量框架中，以全面理解心脏的健康与疾病状态，仍然是一个巨大的挑战。本文旨在填补这一空白，为读者提供一个关于心室电生理-生物力学耦合的综合性理论与应用指南。

在本文中，我们将系统地探索这一多物理场现象。第一章“原则与机制”将奠定理论基础，详细介绍描述[心肌](@entry_id:924326)电活动和力学变形的数学模型，包括单畴方程、有限变形理论以及连接两者的本构关系。第二章“应用与跨学科交叉”将展示这些理论模型的强大应用价值，通过模拟心律失常、[心肌缺血](@entry_id:911155)等临床病症，揭示疾病背后的生物力学机制，并探讨如何利用“数字孪生”优化治疗方案。最后，在“动手实践”部分，我们提供了一系列精选的计算练习，帮助读者将理论知识转化为实际的建模技能。

现在，让我们从构成心室电-力耦合模型的核心物理原则与数学框架开始，深入探讨其基本原理与机制。

## 原则与机制

心室的电生理活动与力学行为紧密耦合，共同构成了心脏作为泵的生理[功能基](@entry_id:139479)础。心室肌细胞的电兴奋触发了收缩，产生力学功，而心室的机械变形反过来又会调节其电生理特性。本章将深入探讨描述心室电-力耦合行为的核心物理原则与数学模型，为理解和模拟[心脏功能](@entry_id:152687)与疾病提供一个严谨的框架。我们将从宏观的连续介质力学和电生理学框架出发，逐步深入到微观结构驱动的本构关系，最终整合为一个完整的[多物理场耦合](@entry_id:171389)系统。

### 耦合系统：概览

心室电-力耦合的核心可以概括为一个双向作用的因果链。正向通路，即**[兴奋-收缩耦合](@entry_id:152858) (Excitation-Contraction Coupling, ECC)**，描述了电信号如何转化为机械力。其基本路径为：跨膜电位 ($V$) 的变化触发细胞内钙离子浓度 ($c$) 的瞬态变化，钙离子激活肌丝滑行，产生[主动应力](@entry_id:1120747) ($\sigma_a$)，最终导致[心肌](@entry_id:924326)组织产生位移 ($\mathbf{u}$) 和变形。这个过程可以简洁地表示为：

$V \rightarrow c \rightarrow \sigma_a \rightarrow \mathbf{u}$

反向通路，即**[力-电反馈](@entry_id:1127753) (Mechano-Electric Feedback, MEF)**，描述了机械变形如何影响电生理活动。[心肌](@entry_id:924326)的拉伸或收缩可以改变[离子通道](@entry_id:170762)的门控特性，从而影响跨膜电位。这形成了一个反馈回路：

$\mathbf{u} \rightarrow V$

将这两个通路结合起来，我们得到了一个高度[非线性](@entry_id:637147)的、多物理场耦合的[偏微分方程(PDE)](@entry_id:166689)系统。一个完整的模型必须包含以下几个核心组成部分  ：
1.  **电生理学模型**：一个[反应-扩散方程](@entry_id:170319)，通常是**单畴方程 (monodomain equation)**，用于描述跨膜电位 $V$ 在组织中的传播。
2.  **细胞离子动力学模型**：一组[常微分方程(ODEs)](@entry_id:147263)，描述各种[离子通道](@entry_id:170762)、泵和交换体的行为，并将 $V$ 的变化与细胞[内状态变量](@entry_id:750754)（如[门控变量](@entry_id:203222)和钙[离子浓度](@entry_id:268003) $c$）联系起来。
3.  **[主动应力模型](@entry_id:1120748)**：一个本构关系，将细[胞内钙](@entry_id:163147)[离子浓度](@entry_id:268003) $c$ 和[心肌](@entry_id:924326)的机械状态（如纤维拉伸）转化为主动产生的机械应力 $\boldsymbol{\sigma}_a$。
4.  **连续介质力学模型**：基于动量守恒定律，描述[心肌](@entry_id:924326)在被动弹性力和主动收缩力的共同作用下的变形。

接下来的章节将逐一详细阐述这些组成部分。

### 力学框架：[连续介质运动学](@entry_id:747813)与动力学

为了描述心脏作为一个连续体的变形，我们采用有限变形理论的框架。

#### 变形运动学

我们将[心肌](@entry_id:924326)组织视为一个连续体，它在变形过程中从一个无应力的**参考构型** (reference configuration) 映射到一个**当前构型** (current configuration)。一个物质点在参考构型中的位置用向量 $\mathbf{X}$ 表示，在时间 $t$ 运动到当前构型中的位置 $\mathbf{x}$。这个映射关系由**变形映射** (deformation map) $\boldsymbol{\varphi}$ 定义：$\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$。

描述局部变形的关键物理量是**变形梯度张量** (deformation gradient tensor) $\mathbf{F}$，它定义为变形映射对参考构型坐标的梯度：

$\mathbf{F} = \frac{\partial \boldsymbol{\varphi}}{\partial \mathbf{X}}$

$\mathbf{F}$ 将参考构型中的一个微元向量 $d\mathbf{X}$ 线性地映射到当前构型中的对应向量 $d\mathbf{x}$，即 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$。它包含了关于局部拉伸、剪切和旋转的全部信息。

从 $\mathbf{F}$ 可以导出多个[应变张量](@entry_id:1132487)，其中在[心肌](@entry_id:924326)[本构模型](@entry_id:174726)中最常用的是**右柯西-格林变形张量** (right Cauchy-Green deformation tensor) $\mathbf{C}$ 和**左柯西-格林变形张量** (left Cauchy-Green deformation tensor) $\mathbf{B}$ ：

$\mathbf{C} = \mathbf{F}^\top \mathbf{F}$
$\mathbf{B} = \mathbf{F} \mathbf{F}^\top$

$\mathbf{C}$ 定义在参考构型上，而 $\mathbf{B}$ 定义在当前构型上。它们都是[对称正定](@entry_id:145886)张量，其特征值等于主拉伸比的平方，为构建[应变能函数](@entry_id:178435)提供了客观的（不依赖于观察者[刚体](@entry_id:1131033)旋转）度量。

[心肌](@entry_id:924326)组织的一个重要特性是其**近乎不可压缩性** (near incompressibility)。这意味着在变形过程中，其体积几乎保持不变。在数学上，这由变形梯度的雅可比行列式 $J = \det(\mathbf{F})$ 来描述，$J$ 代表了局部体积变化率。对于近乎不可压缩的材料，我们有 $J \approx 1$。例如，在一个收缩中期的心室壁局部区域，如果测得的变形梯度在纤维-板层-板层法向坐标系下为对角阵 $\mathbf{F} = \mathrm{diag}(0.85, 1.10, 1.07)$，其体积比 $J = 0.85 \times 1.10 \times 1.07 = 1.00045$，非常接近于 1。这个例子清晰地展示了[心肌](@entry_id:924326)的生理特性：沿纤维方向 15% 的缩短（$\lambda_1=0.85$）必须由横向（板层和板层法向）的增厚（$\lambda_2=1.10, \lambda_3=1.07$）来代偿，以保持总体积不变 。

#### [线性动量平衡](@entry_id:193575)

[心肌](@entry_id:924326)的运动由牛顿第二定律的连续介质形式——**柯西第一运动定律** (Cauchy's first law of motion)——所支配。在当前构型中，它表述为：

$\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \rho \mathbf{a}$

其中，$\boldsymbol{\sigma}$ 是**柯西应力张量** (Cauchy stress tensor)，代表单位面积上的内力；$\mathbf{b}$ 是单位体积的[体力](@entry_id:174230)（如重力）；$\rho$ 是当前构型的密度；$\mathbf{a} = \frac{\partial^2 \mathbf{u}}{\partial t^2}$ 是物质点的加速度，$\mathbf{u}$ 为[位移场](@entry_id:141476)。

在心脏生理频率下，一个关键的简化是**准静态近似** (quasi-static approximation)。我们可以通过[标度分析](@entry_id:153681)来验证这一近似的合理性。考虑左心室壁，其特征厚度 $L \approx 1.0 \times 10^{-2} \text{ m}$，组织密度 $\rho \approx 1.05 \times 10^3 \text{ kg m}^{-3}$。在收缩早期，[心肌](@entry_id:924326)加速度峰值约为 $|\mathbf{a}| \approx 5.0 \text{ m s}^{-2}$，而峰值柯西应力可达 $\sigma_{\text{pk}} \approx 1.0 \times 10^5 \text{ Pa}$。应力梯度项的量级为 $|\nabla \cdot \boldsymbol{\sigma}| \sim \sigma_{\text{pk}} / L \approx 10^7 \text{ N m}^{-3}$，而惯性项的量级为 $\rho |\mathbf{a}| \sim 5.25 \times 10^3 \text{ N m}^{-3}$。两者之比约为 $5 \times 10^{-4} \ll 1$。这表明[惯性力](@entry_id:169104)远小于组织内部的力，因此可以忽略加速度项，得到准静态的动量平衡方程 ：

$\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}$

在[心脏力学](@entry_id:1122088)中，体力 $\mathbf{b}$（主要是重力）通常也远小于应力梯度项，可以被忽略，方程进一步简化为 $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$。

力学模型的边界条件至关重要。对于左心室，**[心内膜](@entry_id:897668)** (endocardial surface) 表面承受着血液压力 $p_{\text{LV}}$。忽略血液粘性产生的微小剪切应力，其**曳力边界条件** (traction boundary condition) 为 $\boldsymbol{\sigma}\mathbf{n} = -p_{\text{LV}}\mathbf{n}$，其中 $\mathbf{n}$ 是[心肌](@entry_id:924326)组织向外的法向量。**[心外膜](@entry_id:893123)** (epicardial surface) 则承受着[心包](@entry_id:900341)压力 $p_{\text{peri}}$，其边界条件类似地为 $\boldsymbol{\sigma}\mathbf{n} = -p_{\text{peri}}\mathbf{n}$ 。在心底等与其他结构连接的部位，则可能施加[位移边界条件](@entry_id:203261)，如 $\mathbf{u}=\mathbf{0}$ 。

### [电生理学](@entry_id:156731)框架：组织电生理学

[心肌](@entry_id:924326)组织的电活动由大量细胞的集体行为所决定。在组织尺度上，我们可以用一个均质化的[反应-扩散方程](@entry_id:170319)来描述跨膜电位的时空演化。

#### 单畴方程

最常用的组织电生理模型是**单畴方程** (monodomain equation)。它源于[电荷守恒](@entry_id:264158)原理，描述了跨膜电位 $V$ 的变化率如何由跨膜[离子电流](@entry_id:170309)和组织内部的传导电流共同决定  。在当前构型中，其标准形式为：

$\chi C_m \frac{\partial V}{\partial t} = \nabla \cdot (\mathbf{D} \nabla V) - \chi I_{\text{ion}}(V, \mathbf{w}) + I_{\text{stim}}$

让我们逐项分析这个方程的物理意义：
-   $\chi C_m \frac{\partial V}{\partial t}$：**[电容电流](@entry_id:272835)密度** (capacitive current density)，单位是 $[A\,m^{-3}]$。$C_m$ 是单位面积的[膜电容](@entry_id:171929) ($[F\,m^{-2}]$)，$\chi$ 是[细胞膜](@entry_id:146704)表面积与组织体积之比 ($[m^{-1}]$)，因此 $\chi C_m$ 是单位体积的有效电容 ($[F\,m^{-3}]$)。这一项代表了为改变膜电位而对[细胞膜](@entry_id:146704)进行充放电所需的电流。
-   $\nabla \cdot (\mathbf{D} \nabla V)$：**传导电流散度** (divergence of conduction current)。$\mathbf{D}$ 是**[电导率张量](@entry_id:155827)** (conductivity tensor) ($[S\,m^{-1}]$)。根据[欧姆定律](@entry_id:276027)，组织内的传导电流密度为 $\mathbf{J} = -\mathbf{D}\nabla V$。该项代表了由邻近区域[电位差](@entry_id:275724)驱动的流入或流出某一点的净电流，它负责动作电位在组织中的传播。
-   $\chi I_{\text{ion}}(V, \mathbf{w})$：**[离子电流](@entry_id:170309)密度** (ionic current density)。$I_{\text{ion}}$ 是通过[离子通道](@entry_id:170762)、泵和交换器流出细胞的单位膜面积的净电流 ($[A\,m^{-2}]$)，它依赖于膜电位 $V$ 和一组描述通道状态的**门控变量** (gating variables) $\mathbf{w}$。按照惯例，$I_{\text{ion}}$ 为正表示正电荷外流（使细胞复极化），因此在方程中带负号。
-   $I_{\text{stim}}$：**外部刺激电流密度** (external stimulus current density) ($[A\,m^{-3}]$)，用于在模拟中人为地触发动作电位。

#### 各向异性与变形

[心肌](@entry_id:924326)的[电传导](@entry_id:190687)具有显著的**各向异性** (anisotropy)：沿肌纤维方向的传导速度远快于横向。这体现在[电导率张量](@entry_id:155827) $\mathbf{D}$ 中。对于以纤维方向 $\mathbf{f}$ 为唯一[对称轴](@entry_id:177299)的横观[各向同性材料](@entry_id:170678)，$\mathbf{D}$ 可以表示为 ：

$\mathbf{D} = d_t \mathbf{I} + (d_l - d_t) \mathbf{f} \otimes \mathbf{f}$

其中 $d_l$ 和 $d_t$ 分别是纵向和横向电导率。

在电-力耦合模型中，组织的变形会改变纤维的朝向和间距，从而影响电导率。在当前构型中的[电导率张量](@entry_id:155827) $\mathbf{D}$（或记为 $\boldsymbol{\sigma}_m$）是通过对参考构型中的[电导率张量](@entry_id:155827) $\mathbf{D}_0$ 进行**推前变换** (push-forward transformation) 得到的 ：

$\mathbf{D} = J^{-1} \mathbf{F} \mathbf{D}_0 \mathbf{F}^\top$

这个变换解释了变形如何通过拉伸和旋转纤维来改变[电传导](@entry_id:190687)通路，是力学影响电学的一个重要机制。

#### [无通量边界条件](@entry_id:168487)

对于一个离体的[心肌](@entry_id:924326)组织块，其表面与绝缘介质（如空气或非导电溶液）接触，没有电流可以流出。这对应于**[无通量边界条件](@entry_id:168487)** (no-flux boundary condition)，即边界上法向电流分量为零：

$\mathbf{n} \cdot (\mathbf{D} \nabla V) = 0$

这是[心肌](@entry_id:924326)组织电生理模拟中最常用的边界条件 。

### 本构模型：问题的核心

本构模型定义了材料的内在属性，是将宏观物理定律与微观生理机制联系起来的桥梁。对于[心肌](@entry_id:924326)，我们需要定义其被动机械行为、主动收缩机制以及两种物理场之间的耦合关系。

#### 被动机械行为

[心肌](@entry_id:924326)的被动力学响应（即在没有肌肉收缩时对拉伸的抵抗）表现为一种[非线性](@entry_id:637147)的、各向异性的[超弹性](@entry_id:159356)行为。这种行为由一个**[应变能密度函数](@entry_id:755490)** (strain-energy density function) $W$ 描述，柯西应力可以从 $W$ 对变形的导数中得出。

为了满足**物质坐标系下的[客观性原理](@entry_id:185412)** (principle of material frame indifference)，$W$ 必须是[应变张量](@entry_id:1132487)（如 $\mathbf{C}$ 或 $\mathbf{B}$）的不变量的函数。为了体现组织的各向异性，需要引入描述微观结构的向量。[心肌](@entry_id:924326)的微观结构通常被理想化为一个正交的**纤维-板层-板层法向** ($\mathbf{f}_0, \mathbf{s}_0, \mathbf{n}_0$) 坐标系 。通过构建这些[方向向量](@entry_id:169562)与[应变张量](@entry_id:1132487) $\mathbf{C}$ 的不变量，可以将结构信息引入 $W$。例如，不变量 $I_{4f} = \mathbf{f}_0 \cdot (\mathbf{C} \mathbf{f}_0)$ 代表了纤维方向拉伸的平方。

一个著名的[心肌](@entry_id:924326)被动[本构模型](@entry_id:174726)是 **Holzapfel-Ogden 模型**。对于近乎不可压缩的材料，它将应变能分解为偏形变部分 $\bar{W}$ 和体积变化部分 $U(J)$。$\bar{W}$ 进一步分解为各向同性基质项和沿纤维、板层以及它们之间剪切的各向异性项 ：

$W = \bar{W}(\bar{I}_1, \bar{I}_{4f}, \bar{I}_{4s}, \bar{I}_{8fs}) + U(J)$

其中一个具体形式为：
$W = \frac{a}{2b}(e^{b(\bar{I}_1-3)}-1) + \frac{a_f}{2b_f}(e^{b_f(\bar{I}_{4f}-1)^2}-1) + \frac{a_s}{2b_s}(e^{b_s(\bar{I}_{4s}-1)^2}-1) + \frac{a_{fs}}{2b_{fs}}(e^{b_{fs}\bar{I}_{8fs}^2}-1) + \frac{k}{2}(J-1)^2$

这里的 $\bar{I}_1, \bar{I}_{4f}, \ldots$ 是基于[等容变形](@entry_id:196451)张量 $\bar{\mathbf{C}} = J^{-2/3}\mathbf{C}$ 计算的不变量。每个指数项都模拟了组织在[大应变](@entry_id:751152)下的指数级“变硬”特性。参数 $a, a_f, a_s, a_{fs}$ 具有应力单位，控制着基质、纤维、板层及纤维-板层剪切的刚度；[无量纲参数](@entry_id:169335) $b, b_f, b_s, b_{fs}$ 控制着[非线性](@entry_id:637147)程度；$k$ 是[体积模量](@entry_id:160069)，用于惩罚体积变化以实现近乎[不可压缩性](@entry_id:274914) 。

#### [兴奋-收缩耦合](@entry_id:152858) (ECC)

ECC 描述了从电信号到机械收缩的转化过程，即 $V \rightarrow c \rightarrow \sigma_a$ 的链条。

##### [钙离子动力学](@entry_id:166646)

ECC 的核心中介是细[胞内钙](@entry_id:163147)离子浓度 $c$ 的瞬态变化。[动作电位](@entry_id:138506)使[细胞膜](@entry_id:146704)去极化，打开 L-型钙通道，少量钙离子内流。这会触发[肌浆网](@entry_id:151258) (Sarcoplasmic Reticulum, SR) 上的兰尼碱受体 (Ryanodine Receptors, RyR) 开放，导致大量钙离子从 SR 释放到胞浆中，引发所谓的“钙诱导的钙释放”。我们可以用一个简化的**双室模型**（胞浆和[肌浆网](@entry_id:151258)）来描述这一过程 。胞浆自由钙浓度 $c$ 和[肌浆网](@entry_id:151258)钙浓度 $c_{\text{SR}}$ 的演化由以下常微分方程组控制：

$\beta_{i} V_{i} \frac{\mathrm{d}c}{\mathrm{d}t} = J_{\text{mem}}(t) - J_{\text{up}} + J_{\text{rel}}$
$\beta_{\text{SR}} V_{\text{SR}} \frac{\mathrm{d}c_{\text{SR}}}{\mathrm{d}t} = J_{\text{up}} - J_{\text{rel}}$

其中，$J_{\text{mem}}$ 是跨膜净钙流，$J_{\text{up}}$ 是通过 SERCA 泵将钙从胞浆回收到 SR 的通量（一个依赖于 $c$ 的饱和过程，如 $J_{\text{up}}=V_{\max}\frac{c^2}{K^2+c^2}$），$J_{\text{rel}}$ 是从 SR 释放到胞浆的通量（一个依赖于 $c_{\text{SR}}$ 的过程，如 $J_{\text{rel}}=k_{\text{rel}}c_{\text{SR}}$）。$\beta$ 和 $V$ 分别代表缓冲系数和室的体积。这组方程为连接 $V$ 和 $c$ 提供了具体的数学描述。

##### [主动应力](@entry_id:1120747)生成

胞浆钙离子与[肌钙蛋白](@entry_id:152123)结合，触发[肌动蛋白和肌球蛋白](@entry_id:148159)丝的滑行，从而产生主动张力。在组织尺度上，这被模型化为一个沿当前纤维方向 $\mathbf{f}$ 的主动柯西[应力张量](@entry_id:148973) $\boldsymbol{\sigma}_a = \sigma_a (\mathbf{f} \otimes \mathbf{f})$。主动应力的大小 $\sigma_a$ 通常表示为一个[现象学模型](@entry_id:1129607) ：

$\sigma_a = \sigma_{\max} \cdot f_c(c) \cdot f_l(\lambda_f) \cdot f_v(v_f)$

这个模型将主动应力分解为三个关键生理机制的乘积：
1.  **钙依赖性 ($f_c(c)$)**：描述了钙离子如何激活收缩。这是一个S型的饱和函数，当 $c=0$ 时 $f_c=0$，随着 $c$ 增加而增加，最终在钙浓度很高时饱和到 $f_c=1$。
2.  **长度依赖性 ($f_l(\lambda_f)$)**：这是**[弗兰克-斯大林机制](@entry_id:153565)** (Frank-Starling mechanism) 在组织层面的体现。在生理范围内，[心肌](@entry_id:924326)拉伸得越长（$\lambda_f$ 越大），其产生的主动张力就越大。
3.  **速度依赖性 ($f_v(v_f)$)**：这是肌肉的**[力-速度关系](@entry_id:151449)** (force-velocity relation)。在等长收缩 ($v_f=0$) 时，力最大（归一化为 $f_v=1$）。当肌肉缩短速度越快 ($v_f > 0$)，能产生的力就越小。

#### [力-电反馈](@entry_id:1127753) (MEF)

MEF 是指机械状态[反作用](@entry_id:203910)于电生理的过程。一个主要的机制是**拉伸激活通道** (Stretch-Activated Channels, SACs)。[心肌细胞](@entry_id:898045)膜上的这些非选择性阳[离子通道](@entry_id:170762)在细胞被拉伸时开放概率增加。这会产生一个额外的[离子电流](@entry_id:170309) $I_{\text{SAC}}$，其形式通常为 ：

$I_{\text{SAC}} = G_{\text{SAC}}\,\phi(\lambda_f)\,(V - E_{\text{rev}})$

其中 $G_{\text{SAC}}$ 是最大电导，$\phi(\lambda_f)$ 是一个随纤维拉伸 $\lambda_f$ 增加而增加的无量纲激活函数，而 $E_{\text{rev}}$ 是该通道的逆转电位（通常接近 0 mV）。

这个反馈机制具有重要的生理和病理意义。例如，在舒张期，心室充盈导致[心肌](@entry_id:924326)被拉伸（$\lambda_f > 1$），此时膜电位 $V$ 处于静息态（约 -80 mV）。由于 $V \ll E_{\text{rev}}$，拉伸会产生一个内向（去极化）的 $I_{\text{SAC}}$。这个去[极化电流](@entry_id:196744)会使[静息电位](@entry_id:176014)升高，如果足够强，可能触发早[后除极](@entry_id:167958)或期前收缩，是[心律失常](@entry_id:909082)的一个潜在来源  。

### 完整系统与数值求解策略

#### 构建耦合系统

将以上所有部分整合起来，我们便得到了一个描述心室电-力耦合行为的完整数学模型。该模型由一组耦合的、[非线性](@entry_id:637147)的[偏微分](@entry_id:194612)方程和[常微分方程组](@entry_id:907499)成，其核心是电生理的单畴方程和力学的准静态动量平衡方程，通过复杂的[本构关系](@entry_id:186508)和源项相互连接 。

**电生理子系统**:
$\chi C_m \frac{\partial V}{\partial t} = \nabla \cdot (\mathbf{D}(\mathbf{F}) \nabla V) - \chi I_{\text{ion}}(V, \mathbf{w}) - I_{\text{SAC}}(\lambda_f, V) + I_{\text{stim}}$
$\frac{d\mathbf{w}}{dt} = \mathbf{g}(V, \mathbf{w}, c)$
$\beta_{i} V_{i} \frac{\mathrm{d}c}{\mathrm{d}t} = J_{\text{mem}}(t,V) - J_{\text{up}}(c) + J_{\text{rel}}(c_{\text{SR}})$
(以及其他相关ODE)

**力学子系统**:
$\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$
$\boldsymbol{\sigma} = \boldsymbol{\sigma}_p(\mathbf{F}) + \boldsymbol{\sigma}_a(c, \lambda_f, v_f)$
$\mathbf{F} = \mathbf{I} + \nabla \mathbf{u}$

这个系统的求解是计算心脏病学中的一个重大挑战。

#### 数值求解方法

由于该系统的复杂性，解析解是不可能的，必须依赖数值方法。主要有两种策略 ：

1.  **整体式求解 (Monolithic Solvers)**：在每个时间步，将所有未知量（$V, \mathbf{w}, c, \mathbf{u}$ 等）的离散化方程作为一个巨大的、单一的[非线性](@entry_id:637147)代数系统来同时求解。这种方法的优点是能够完全隐式地处理所有耦合项，因此对于强耦合和刚性问题具有很好的稳定性和鲁棒性。缺点是需要构建和求解一个非常庞大且结构复杂的[雅可比矩阵](@entry_id:178326)，实现难度大，计算成本高。

2.  **分离式求解 (Partitioned Solvers)**：也称为**[算子分裂](@entry_id:634210)** (operator splitting)。在每个时间步，将电生理子系统和力学子系统分离开，依次求解。例如，在一个时间步内，先固定力学状态，求解电生理方程；然后用更新后的电生理状态（如钙浓度）作为输入，求解力学方程。这种方法更具模块化，易于实现，并且可以为每个子问题使用最高效的专用求解器。其主要缺点是，通过在子问题间交替传递信息，耦合项被显式或半隐式地处理，这会引入**分裂误差** (splitting error)。对于强耦合问题，这可能导致稳定性和精度的下降，除非使用非常小的时间步长。为了保证精度，时间步长必须能够解析系统中最快的物理过程，即约 1ms 的动作电位上升沿 。

为了改善分离式方法的稳定性和精度，可以在每个时间步内进行多次**子迭代** (sub-iterations)，在电学和力学求解器之间来回传递更新的信息，直到耦合变量收敛。当子迭代收敛时，其解将趋近于整体式方法的解，从而结合了两种策略的优点 。选择何种求解策略取决于模型的具体耦合强度、所需的精度以及可用的计算资源。