## 引言
[声流](@entry_id:187348)（Acoustic Streaming）是一种迷人而反直觉的物理现象：一个高频[振荡](@entry_id:267781)、[时间平均](@entry_id:267915)效应看似为零的声场，竟能在流体中稳定地驱动起宏观的定向流动。这一效应不仅是[流体力学](@entry_id:136788)[非线性](@entry_id:637147)领域的一个经典课题，更在从微观尺度上的细胞操控到宏观尺度上的工业过程中，展现出巨大的应用潜力。其核心问题在于，[振荡运动](@entry_id:194817)如何转化为定常运动？本篇文章旨在系统性地回答这一问题，深入剖析声波与流体介质之间复杂的[非线性](@entry_id:637147)相互作用。

我们将分三部分展开探讨。在“原理与机制”一章中，我们将从[Navier-Stokes方程](@entry_id:161487)出发，揭示[声学](@entry_id:265335)雷诺兹应力的起源，并区分Eckart[声流](@entry_id:187348)和[Rayleigh声流](@entry_id:203296)这两种基本模式。随后，在“应用与跨学科[交叉](@entry_id:147634)”一章，我们将展示[声流](@entry_id:187348)如何在微流控、生物医学和[材料科学](@entry_id:152226)等前沿领域中作为一种强大的工具被利用。最后，“动手实践”部分将提供一系列练习，帮助读者巩固对关键概念的理解并将其应用于具体问题。

## 原理与机制

[声流](@entry_id:187348)现象的核心，在于一种看似矛盾的物理过程：一个时间平均为零的高频[振荡](@entry_id:267781)声场，如何能够在流体中驱动产生一个稳定的、非零的[定常流](@entry_id:191654)动？答案蕴藏在[流体动力学](@entry_id:136788)的[非线性](@entry_id:637147)特性之中。本章将从第一性原理出发，系统地阐释[声流](@entry_id:187348)的驱动力来源，探讨其产生旋转运动的机制，并详细区分两种主要的[声流](@entry_id:187348)类型——Eckart[声流](@entry_id:187348)和[Rayleigh声流](@entry_id:203296)，最后通过[标度分析](@entry_id:153681)，揭示[声流](@entry_id:187348)强度与声场及流体参数之间的普适关系。

### [振荡](@entry_id:267781)产生[定常流](@entry_id:191654)的起源：声学雷诺兹应力

描述[流体运动](@entry_id:182721)的基本方程是[Navier-Stokes方程](@entry_id:161487)。对于可压缩[牛顿流体](@entry_id:263796)，其[动量方程](@entry_id:197225)为：
$$
\rho \left( \frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \nabla) \mathbf{v} \right) = -\nabla p + \mu \nabla^2 \mathbf{v} + \left(\zeta + \frac{1}{3}\mu\right) \nabla(\nabla \cdot \mathbf{v})
$$
其中 $\rho$ 是流体密度，$p$ 是压力，$\mathbf{v}$ 是[速度场](@entry_id:271461)，$\mu$ 和 $\zeta$ 分别是[剪切粘度](@entry_id:141046)和体粘度。方程左侧的第二项，$(\mathbf{v} \cdot \nabla) \mathbf{v}$，被称为[对流](@entry_id:141806)项或惯性项，它是[非线性](@entry_id:637147)的。正是这个[非线性](@entry_id:637147)项，构成了[声流](@entry_id:187348)现象的物理基础。

为了分析声波引起的效应，我们将流场中的物理量分解为定常（或背景）部分和[声学振荡](@entry_id:161154)部分。例如，[速度场](@entry_id:271461)可以写成 $\mathbf{v} = \mathbf{v}_0 + \mathbf{v}_1 + \mathbf{v}_2 + \dots$，其中 $\mathbf{v}_0$ 是背景流速（此处假设为零），$\mathbf{v}_1$ 是与声波振幅成正比的一阶[振荡](@entry_id:267781)速度，$\mathbf{v}_2$ 是[二阶修正](@entry_id:199233)项。声波是周期性[振荡](@entry_id:267781)，因此其一阶量的长时间平均值为零，例如 $\langle \mathbf{v}_1 \rangle = \mathbf{0}$，其中 $\langle \cdot \rangle$ 表示在一个声波周期内进行[时间平均](@entry_id:267915)。

然而，当我们对整个[动量方程](@entry_id:197225)进行[时间平均](@entry_id:267915)，以求得[定常流](@entry_id:191654)动 $\mathbf{v}_s = \langle \mathbf{v}_2 \rangle$ 的控制方程时，[非线性](@entry_id:637147)项的平均值并不为零。考虑一个简化的不可压缩情况，动量方程的[对流](@entry_id:141806)项为 $\rho_0 (\mathbf{v} \cdot \nabla) \mathbf{v}$。将其展开到二阶并取[时间平均](@entry_id:267915)，我们会得到 $\rho_0 \langle ((\mathbf{v}_1 + \mathbf{v}_2) \cdot \nabla) (\mathbf{v}_1 + \mathbf{v}_2) \rangle$。由于 $\langle \mathbf{v}_1 \rangle = 0$，交叉项如 $\langle (\mathbf{v}_1 \cdot \nabla) \mathbf{v}_2 \rangle$ 在很多情况下也可以忽略，主导的[非线性](@entry_id:637147)贡献来自于一阶量的二次项：$\rho_0 \langle (\mathbf{v}_1 \cdot \nabla) \mathbf{v}_1 \rangle$。

利用矢量恒等式和连续性方程 $\nabla \cdot \mathbf{v}_1 = 0$（对于不可压缩情况），该项可以写成一个[张量的散度](@entry_id:191736)形式：
$$
\rho_0 \langle (\mathbf{v}_1 \cdot \nabla) \mathbf{v}_1 \rangle = \nabla \cdot (\rho_0 \langle \mathbf{v}_1 \mathbf{v}_1 \rangle)
$$
这里，$\mathbf{v}_1 \mathbf{v}_1$ 是一个[二阶张量](@entry_id:199780)，称为并矢（dyadic product）。因此，时间平均后的[动量方程](@entry_id:197225)中出现了一个额外的力项，它源于一阶声学[速度场](@entry_id:271461)的[非线性](@entry_id:637147)自作用。

这个时间平均的[动量通量](@entry_id:199796)，$\mathbf{\Pi} = \rho_0 \langle \mathbf{v}_1 \mathbf{v}_1 \rangle$，在[流体力学](@entry_id:136788)中被称为**雷诺兹[应力张量](@entry_id:148973)**。在[声学](@entry_id:265335)背景下，我们称之为**[声学](@entry_id:265335)雷诺兹应力**。它的物理意义是，[振荡](@entry_id:267781)的流[体元](@entry_id:267802)通过自身运动所携带的动量，其时间平均效应表现为一个应[力场](@entry_id:147325)。这个应[力场](@entry_id:147325)的空间不均匀性（即其散度）产生了一个等效的定常体积力 $\mathbf{F}_s$，驱动着定常的[声流](@entry_id:187348)运动 [@problem_id:1900140]。
$$
\mathbf{F}_s = - \nabla \cdot \mathbf{\Pi} = - \nabla \cdot (\rho_0 \langle \mathbf{v}_1 \mathbf{v}_1 \rangle)
$$
这个力也被称为**雷诺兹应力力**或**声[辐射力](@entry_id:196819)**。因此，描述[声流](@entry_id:187348)速度 $\mathbf{v}_s$ 的[稳态](@entry_id:182458)[Navier-Stokes方程](@entry_id:161487)（通常在低雷诺兹数下简化为[Stokes方程](@entry_id:196346)）变为：
$$
\mu \nabla^2 \mathbf{v}_s - \nabla p_s + \mathbf{F}_s = 0
$$
其中 $p_s$ 是与[声流](@entry_id:187348)相关的定常[压力修正](@entry_id:753714)。

雷诺兹[应力张量](@entry_id:148973)的迹（trace），$\text{Tr}(\mathbf{\Pi}) = \rho_0 \langle v_{1i} v_{1i} \rangle = \rho_0 \langle |\mathbf{v}_1|^2 \rangle$，与声场的动能密度直接相关。例如，对于一个在x方向衰减的圆极化[横波](@entry_id:269527) $\mathbf{v}_1(x,t) = v_0 e^{-\alpha x} [ \cos(kx - \omega t) \hat{\mathbf{j}} + \sin(kx - \omega t) \hat{\mathbf{k}} ]$，其雷诺兹应力张量的迹为 $\rho_0 v_0^2 e^{-2\alpha x}$，直接反映了声能随传播距离的衰减 [@problem_id:646804]。

### 涡量的产生：[声流](@entry_id:187348)的“引擎”

一个定常体积力的存在，并不必然导致流体产生宏观流动。如果该力是**保守的**，即它可以表示为一个[标量势](@entry_id:276177) $\Phi$ 的梯度，$\mathbf{F}_s = -\nabla \Phi$，那么这个力可以被一个静定的压[力场](@entry_id:147325) $p_s = \Phi$ 完全平衡，而不会在无界流体中引起任何流动。流动，尤其是具有旋转结构的涡胞，其真正的“引擎”是**[涡量](@entry_id:142747)**（vorticity），定义为[速度场的旋度](@entry_id:183606) $\boldsymbol{\omega} = \nabla \times \mathbf{v}$。

一个[定常流](@entry_id:191654)场 $\mathbf{v}_s$ 的[涡量](@entry_id:142747) $\boldsymbol{\omega}_s = \nabla \times \mathbf{v}_s$ 是如何产生的呢？通过对[定常流](@entry_id:191654)动控制方程取旋度，我们可以得到[涡量输运方程](@entry_id:139098)。其中，涡量的产生项是[声学](@entry_id:265335)力的旋度，$\mathbf{S} = \nabla \times \mathbf{F}_s$。只有当[声学](@entry_id:265335)力 $\mathbf{F}_s$ 是**非保守的**（即 $\nabla \times \mathbf{F}_s \neq \mathbf{0}$）时，它才能成为涡量的净源泉，从而驱动起具有旋转结构的[声流](@entry_id:187348)。

我们可以通过一个具体的例子来理解这一点。考虑一个主要沿x方向传播的二维高斯声束，其一阶[速度场](@entry_id:271461)的[复振幅](@entry_id:164138)为 $\tilde{v}_{1x}(x, y) = V_0 \exp(-y^2/w^2) \exp(-\alpha x + ikx)$，其中 $\alpha$ 是衰减系数 [@problem_id:449493]。主导的雷诺兹应力分量是 $\Pi_{xx} = \frac{\rho_0}{2} |\tilde{v}_{1x}|^2 = \frac{\rho_0 V_0^2}{2} \exp(-2y^2/w^2) \exp(-2\alpha x)$。[声学](@entry_id:265335)[力场](@entry_id:147325)的主要分量为 $F_x = -\partial_x \Pi_{xx}$ 和 $F_y = -\partial_y \Pi_{xy}$。在傍轴近似下，[涡量](@entry_id:142747)源的z分量可以近似为：
$$
S_z = (\nabla \times \mathbf{F}_s)_z = \frac{\partial F_y}{\partial x} - \frac{\partial F_x}{\partial y} \approx \frac{\partial^2 \Pi_{xx}}{\partial x \partial y}
$$
计算可得：
$$
S_z \approx \frac{\partial^2}{\partial x \partial y} \left( \frac{\rho_0 V_0^2}{2} e^{-2y^2/w^2} e^{-2\alpha x} \right) = 2\alpha \rho_0 V_0^2 \left(\frac{2y}{w^2}\right) e^{-2y^2/w^2} e^{-2\alpha x}
$$
这个结果 [@problem_id:449493] 揭示了涡量产生的关键因素：首先，必须有声波的**衰减**（$\alpha \neq 0$）；其次，声场强度在**横向**（y方向）必须是不均匀的。正是声波能量在传播过程中的耗散，以及这种耗散在空间上的不[均匀分布](@entry_id:194597)，共同构成了非保守的[声学](@entry_id:265335)[力场](@entry_id:147325)，从而像一个引擎一样不断地为流体注入[涡量](@entry_id:142747)，驱动[声流](@entry_id:187348)涡胞的形成。

### 两种典型的[声流](@entry_id:187348)模式

根据声学力产生的主要区域和物理机制，[声流](@entry_id:187348)通常被分为两大类。

#### Eckart[声流](@entry_id:187348)：流体内部驱动的流动

当声波在无界的粘性流体中传播时，由于流体的粘度和[热导率](@entry_id:147276)，声能会被吸收并转化为热，导致声波振幅随距离衰减。如前所述，这种能量耗散伴随着动量的转移，在流体“内部”（bulk）产生了一个驱动力。由此产生的[声流](@entry_id:187348)被称为**Eckart[声流](@entry_id:187348)**。

理解Eckart[声流](@entry_id:187348)的一个核心物理约束是质量守恒。考虑一个从声源发出的平面声波，在一个原本静止的流体中传播。尽管声波本身携带净动量（在一个周期内平均），但它不能产生净的质量输运。这意味着，在任何一个垂直于传播方向的平面上，总的时间平均质量通量必须为零。考虑到二阶效应，这个条件写作 $\langle \rho v_x \rangle = 0$。展开为：
$$
\langle (\rho_0 + \rho_1 + \dots)(v_{1x} + v_{2x} + \dots) \rangle = \rho_0 \langle v_{2x} \rangle + \langle \rho_1 v_{1x} \rangle + \dots = 0
$$
其中 $\rho_1$ 是一阶[密度扰动](@entry_id:159546)。由此，我们可以直接得到Eckart[声流](@entry_id:187348)速度 $v_s(x) = \langle v_{2x} \rangle$ 的表达式：
$$
v_s(x) = - \frac{\langle \rho_1 v_{1x} \rangle}{\rho_0}
$$
对于一个在+x方向传播的衰减平面声波 $v_{1x} = \text{Re}[v_a e^{-\alpha x} e^{i(kx - \omega t)}]$，通过线性化的连续性方程可以求得 $\rho_1$。计算时间平均的乘积 $\langle \rho_1 v_{1x} \rangle$ 会得到一个正值，它代表了声波（也称为“[声子气](@entry_id:147597)”）携带的质量通量。为了补偿这个通量，流体本身必须产生一个反向的[定常流](@entry_id:191654)动 [@problem_id:1248367]。计算结果表明：
$$
v_s(x) = -\frac{v_a^2}{2c_0}e^{-2\alpha x}
$$
这里的负号明确表示，Eckart[声流](@entry_id:187348)的方向与声波传播方向相反，如同声波衰减时[对流](@entry_id:141806)体产生的“反冲”。其大小与声波强度（$v_a^2$）成正比，并随声波能量的耗尽（$e^{-2\alpha x}$）而减弱。

这一原理同样适用于更复杂的几何形状。例如，对于一个从原点发出的三维球形衰减声波，在远场（$kr \gg 1$）区域，可以用同样的方法推导出径向的Eckart[声流](@entry_id:187348)速度 [@problem_id:646834]。其速度大小为：
$$
v_2(r) = \frac{\omega k |S_0|^2}{2 c_0^2 r^2} e^{-2\alpha r}
$$
其中 $S_0$ 是源强度。[声流](@entry_id:187348)速度随距离的平方 $r^2$ 衰减，这反映了声波能量在三维空间中的几何[扩散](@entry_id:141445)效应。

#### [Rayleigh声流](@entry_id:203296)：[边界层](@entry_id:139416)驱动的流动

第二种主要的[声流](@entry_id:187348)类型发生在固体边界附近，被称为**[Rayleigh声流](@entry_id:203296)**。其驱动力并非源于流体内部的衰减，而是集中在紧邻固体表面的一个薄层——**声学[边界层](@entry_id:139416)**（或[Stokes边界层](@entry_id:194443)）内。

当声波平行于一个固[体壁](@entry_id:272571)面传播时，由于流体的粘性，壁面处必须满足[无滑移边界条件](@entry_id:186229)（流速为零）。这导致在壁面附近形成一个[速度梯度](@entry_id:261686)极大的薄层，其厚度量级为 $\delta_v = \sqrt{2\nu/\omega}$，其中 $\nu$ 是流体的运动粘度，$\omega$ 是声波[角频率](@entry_id:261565)。高频声波对应的[边界层](@entry_id:139416)非常薄。

在这个[边界层](@entry_id:139416)内部，粘性力与惯性力同等重要，导致一阶声学[速度场](@entry_id:271461)不仅振幅发生剧烈变化，其相位也与[边界层](@entry_id:139416)外的声场不同。这种剧烈的速度梯度和相位变化，使得[边界层](@entry_id:139416)内的雷诺兹应力 $\rho_0 \langle \mathbf{v}_1 \mathbf{v}_1 \rangle$ 变得非常显著，从而在此薄层内产生了一个强大的非保守声学力。

这个局域化的力源驱动了两种紧密关联的流动：
1.  **内[声流](@entry_id:187348)（Schlichting Streaming）**：发生在[声学](@entry_id:265335)[边界层](@entry_id:139416) *内部* 的[定常流](@entry_id:191654)动。其速度剖面复杂，但它的大小和方向可以通过[边界层](@entry_id:139416)外的“外部”声场速度来确定。例如，对于一个沿其轴线[振荡](@entry_id:267781)的物体，其表面附近产生的切向内[声流](@entry_id:187348)速度 $\langle u_s \rangle$ 可由以下公式给出 [@problem_id:646842]：
    $$
    \langle u_s \rangle = - \frac{3}{4\omega} \text{Re} \left[ \tilde{u}_p^*(s) \frac{d\tilde{u}_p(s)}{ds} \right]
    $$
    其中 $\tilde{u}_p(s)$ 是物体表面相[对流](@entry_id:141806)体的切向滑动速度的[复振幅](@entry_id:164138)，$s$ 是沿物体表面的[弧长](@entry_id:191173)坐标。这个公式表明，[声流](@entry_id:187348)是由表面滑动速度的**空间梯度**驱动的。在一个沿轴线[振荡](@entry_id:267781)的抛物面体上，这个公式可以用来计算出表面各点的[声流](@entry_id:187348)速度，并找到其最大值 [@problem_id:646842]。

2.  **外[声流](@entry_id:187348)**：发生在声学[边界层](@entry_id:139416) *外部* 的较大尺度的流动。从宏观上看，[边界层](@entry_id:139416)内的内[声流](@entry_id:187348)起到了一个“泵”的作用，它将流体从某些区域吸入[边界层](@entry_id:139416)，再从另一些区域排出。对于外部的流场而言，这等效于在[边界层](@entry_id:139416)外缘（$y \sim \delta_v$）处存在一个有效的**滑移速度**（slip velocity）。这个滑移速度驱动了外部区域的流动，形成了经典的、由一对对反向旋转的涡胞组成的[Rayleigh声流](@entry_id:203296)结构。

考虑一个沿壁面传播的部分[驻波](@entry_id:148648) $\hat{u}_{1,inv}(x) = U_0(e^{ikx} + R e^{-ikx})$，其中 $R$ 是[反射系数](@entry_id:194350)。在[边界层](@entry_id:139416)外缘的等效滑移速度可以计算得出 [@problem_id:646818]：
$$
u_{slip}(x) = -\frac{kU_0^2(1-R^2)}{4\omega} + \frac{3kU_0^2R}{2\omega}\sin(2kx)
$$
这个表达式包含两部分：第一项是空间均匀的，代表一种净的流体漂移（有时称为“声风”）；第二项是空间周期性的，其振幅为 $\frac{3kU_0^2R}{2\omega}$。正是这个周期性变化的滑移速度，驱动了外部流体形成空间周期为 $\pi/k$（半个声波波长）的涡胞阵列。

一旦驱动力或边界条件确定，具体的[声流](@entry_id:187348)[速度剖面](@entry_id:266404)就可以通过求解定常[Stokes方程](@entry_id:196346)来获得。例如，若已知[边界层](@entry_id:139416)内的[声学](@entry_id:265335)力密度为 $F_x(y) = F_0 \exp(-y/\delta) \sin(y/\delta)$，并给定无滑移和[远场](@entry_id:269288)条件，我们可以积分求解动量方程 $\mu \frac{d^2 u_s}{dy^2} + F_x(y) = 0$。这会得到一个明确的速度剖面 $u_s(y)$，并可以计算出其最大速度，这对于微流控等应用中的流速控制至关重要 [@problem_id:1768681]。另一个例子是在封闭通道中，由[声学](@entry_id:265335)力驱动的流动必须满足总通量为零的约束，这会诱导一个逆向的压力梯度和相应的Poiseuille回流，最终的流场是声力直接驱动流和压力驱动回流的叠加 [@problem_id:460831]。

### [标度分析](@entry_id:153681)与[声学](@entry_id:265335)雷诺兹数

为了获得对[声流](@entry_id:187348)现象更普适的理解，我们可以采用量纲分析和[标度分析](@entry_id:153681)的方法。这有助于我们判断在不同条件下，哪种物理效应占主导地位，并预测[声流](@entry_id:187348)速度如何依赖于系统参数。

我们回到定常[涡量输运方程](@entry_id:139098)，并进行[标度分析](@entry_id:153681)。设 $U_s$ 和 $a$ 分别是[声流](@entry_id:187348)的特征速度和特征尺度，$U_a$ 是声波的[特征速度](@entry_id:165394)振幅。[涡量输运方程](@entry_id:139098)各项的[标度关系](@entry_id:273705)如下 [@problem_id:638549]：
$$
\underbrace{\rho \nabla \times [(\mathbf{u}_s \cdot \nabla) \mathbf{u}_s]}_{\sim \rho U_s^2 / a^2} = \underbrace{\mu \nabla^2 \boldsymbol{\omega}_s}_{\sim \mu U_s / a^3} + \underbrace{\nabla \times \mathbf{F}_s}_{\sim \rho U_a^2 / a^2}
$$
将方程各项除以 $\rho/a^2$，我们得到一个关于 $U_s$ 的[标度关系](@entry_id:273705)式：
$$
U_s^2 \sim \frac{\mu}{\rho a} U_s + U_a^2
$$
这个简单的[二次方程](@entry_id:163234)揭示了[声流](@entry_id:187348)的两种不同行为模式，其转换由一个关键的[无量纲参数](@entry_id:169335)——**[声学](@entry_id:265335)雷诺兹数** $Re_a = \frac{\rho U_a a}{\mu}$——控制。该参数衡量了声场中的[惯性力](@entry_id:169104)与[粘性力](@entry_id:263294)的比值。

1.  **低声学雷诺兹数区 ($Re_a \ll 1$)**：
    在这种情况下，粘性效应在[声流](@entry_id:187348)中占主导地位。标度方程中的 $U_s^2$ 项可以忽略，得到 $\frac{\mu}{\rho a} U_s \sim U_a^2$。因此，[声流](@entry_id:187348)速度的标度为：
    $$
    U_s \sim \frac{\rho a}{\mu} U_a^2 = Re_a \cdot U_a
    $$
    在此区域，[声流](@entry_id:187348)速度与声波振幅的**平方**成正比（即与声强成正比），并且[流动相](@entry_id:197006)对较弱。

2.  **高声学雷诺兹数区 ($Re_a \gg 1$)**：
    当声场强度很高或流体粘性很低时，[声流](@entry_id:187348)本身的惯性变得重要。此时，标度方程中的粘性项 $\frac{\mu}{\rho a} U_s$ 变得次要，我们得到 $U_s^2 \sim U_a^2$。因此，[声流](@entry_id:187348)速度的标度为：
    $$
    U_s \sim U_a
    $$
    在此区域，[声流](@entry_id:187348)速度与声波振幅**线性**相关，流动变得非常显著，其速度可以与声波的质点运动速度相媲美。

通过求解上述二次标度方程并进行泰勒展开，我们还可以得到高雷诺兹数区下对[线性关系](@entry_id:267880)的一阶粘性修正 [@problem_id:638549]：
$$
U_s \approx U_a \left(1 - \frac{\mu}{2\rho U_a a}\right) = U_a \left(1 - \frac{1}{2 Re_a}\right)
$$
这个结果定量地描述了从惯性主导区向粘性影响区过渡的行为。这种[标度分析](@entry_id:153681)不仅统一了对[声流](@entry_id:187348)现象的认识，而且为实验设计和应用预测提供了强有力的理论工具。