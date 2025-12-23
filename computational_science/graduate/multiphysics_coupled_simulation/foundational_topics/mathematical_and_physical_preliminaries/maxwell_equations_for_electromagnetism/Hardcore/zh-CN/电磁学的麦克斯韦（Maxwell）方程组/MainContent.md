## 引言
[麦克斯韦方程组](@entry_id:150940)是经典电磁学的基石，以其无与伦比的简洁与深刻，统一了电、磁与光学现象，构成了现代科学与工程技术的支柱。这些方程不仅精确地描述了电磁波的传播，也为从发电机、[电动机](@entry_id:268448)到无线通信和医疗成像等无数技术创新奠定了理论基础。

然而，对于从事[多物理场耦合](@entry_id:171389)仿真领域的研究生和工程师而言，挑战不仅在于理解这组方程的抽象数学形式，更在于如何将其与热学、力学、[流体动力学](@entry_id:136788)等其他物理过程精确耦合，以解决真实的工程与科学问题。这一知识鸿沟需要一个能够连通基础理论与前沿应用的系统性框架来弥合。

本文旨在搭建从基础理论到高级应用的桥梁。我们将首先在“原理与机制”一章中，深入剖析[麦克斯韦方程组](@entry_id:150940)的物理内涵、数学结构、[守恒定律](@entry_id:269268)及关键的[准静态近似](@entry_id:264812)。随后，在“应用与跨学科联系”一章中，我们将通过[感应加热](@entry_id:192046)、机电[能量转换](@entry_id:165656)和波导等具体案例，展示这些原理如何解决复杂的多物理场问题。最后，“动手实践”部分将提供具体的数值练习，帮助读者将理论知识转化为解决实际问题的能力。通过这一系统性的学习路径，读者将能够全面掌握[麦克斯韦方程组](@entry_id:150940)的核心，并充满信心地将其应用于前沿的科研与工程实践中。

## 原理与机制

在对电磁学基本概念进行初步介绍之后，本章将深入探讨麦克斯韦方程组所蕴含的核心物理原理与数学机制。我们将从宏观场方程的表述出发，阐释物质如何响应[电磁场](@entry_id:265881)，并建立在不同[材料界面](@entry_id:751731)上场必须满足的边界条件。随后，我们将探究场本身的数学结构，引入求解这些方程的有力工具——[电磁势](@entry_id:266145)。最后，本章将重点阐述电磁学中两个最基本的守恒律——[能量守恒](@entry_id:140514)和[动量守恒](@entry_id:149964)，并介绍在[多物理场仿真](@entry_id:145294)中至关重要的[准静态近似](@entry_id:264812)方法。

### 宏观场方程

在包含物质的宏观尺度上，[电磁场](@entry_id:265881)由一套四个相互关联的[偏微分方程](@entry_id:141332)描述，即[麦克斯韦方程组](@entry_id:150940)。在[微分形式](@entry_id:146747)下，它们为：

$$
\begin{align*}
\nabla\cdot\mathbf{D}  = \rho_{\mathrm{f}}  \text{(高斯电场定律)} \\
\nabla\cdot\mathbf{B}  = 0  \text{(高斯磁场定律)} \\
\nabla\times\mathbf{E}  = -\frac{\partial\mathbf{B}}{\partial t}  \text{(法拉第电磁感应定律)} \\
\nabla\times\mathbf{H}  = \mathbf{J}_{\mathrm{f}} + \frac{\partial\mathbf{D}}{\partial t}  \text{(安培-麦克斯韦定律)}
\end{align*}
$$

这组方程引入了四个矢量场：**[电场](@entry_id:194326)强度 (electric field intensity)** $\mathbf{E}$、**[磁感应强度](@entry_id:144179) (magnetic flux density)** $\mathbf{B}$、**[电位移场](@entry_id:273493) (electric displacement field)** $\mathbf{D}$ 和 **[磁场强度](@entry_id:197932) (magnetic field intensity)** $\mathbf{H}$。同时，方程的源项为**自由电荷密度 (free charge density)** $\rho_{\mathrm{f}}$ 和**[自由电流](@entry_id:191634)密度 (free current density)** $\mathbf{J}_{\mathrm{f}}$。

理解这四个场的不同物理角色至关重要。$\mathbf{E}$ 和 $\mathbf{B}$ 是基本的[力场](@entry_id:147325)。它们定义于空间中的每一点，无论是在真空中还是在物质内部，其物理意义在于它们直接决定了作用在[电荷](@entry_id:275494)上的力。一个以速度 $\mathbf{v}$ 运动的点电荷 $q$ 所受的[洛伦兹力](@entry_id:145104) $\mathbf{F}$ 即由这两个场决定：$\mathbf{F} = q(\mathbf{E} + \mathbf{v} \times \mathbf{B})$。

相比之下，$\mathbf{D}$ 和 $\mathbf{H}$ 是为了在处理宏观物质中的电磁问题时提供便利而引入的**[辅助场](@entry_id:155519) (auxiliary fields)**。当外部[电磁场](@entry_id:265881)作用于介质时，介质内部的原子和分子会产生响应，导致微观[电荷](@entry_id:275494)的重新[分布](@entry_id:182848)，形成**电极化 (electric polarization)** 和**磁化 (magnetization)**。这些效应可以通过宏观量**极化强度矢量 (polarization vector)** $\mathbf{P}$ 和**磁化强度矢量 (magnetization vector)** $\mathbf{M}$ 来描述。$\mathbf{P}$ 代表单位体积内的[电偶极矩](@entry_id:178520)，而 $\mathbf{M}$ 代表单位体积内的[磁偶极矩](@entry_id:158175)。

这些微观的束缚[电荷](@entry_id:275494)和束缚电流同样会产生[电磁场](@entry_id:265881)，从而使总场变得非常复杂。为了简化描述，我们将物质的响应部分吸收到场的定义中，定义了 $\mathbf{D}$ 场和 $\mathbf{H}$ 场 ：
$$
\mathbf{D} \equiv \varepsilon_{0}\mathbf{E} + \mathbf{P}
$$
$$
\mathbf{H} \equiv \frac{1}{\mu_{0}}\mathbf{B} - \mathbf{M}
$$
其中 $\varepsilon_0$ 是[真空介电常数](@entry_id:204253)，$\mu_0$ 是[真空磁导率](@entry_id:186031)。通过这样的定义，由极化和磁化产生的束缚[电荷密度](@entry_id:144672) $\rho_b = -\nabla \cdot \mathbf{P}$ 和束缚电流密度 $\mathbf{J}_b = \nabla \times \mathbf{M} + \partial_t \mathbf{P}$ 就被巧妙地移出了麦克斯韦方程组的源项。结果是，[高斯电场定律](@entry_id:146732)和[安培-麦克斯韦定律](@entry_id:266368)的[源项](@entry_id:269111)分别只剩下我们通常能够直接控制或测量的自由电荷 $\rho_{\mathrm{f}}$ 和[自由电流](@entry_id:191634) $\mathbf{J}_{\mathrm{f}}$。

这种表述方式的巨大优势在于其普适性。例如，[高斯电场定律](@entry_id:146732)的积分形式为 $\oint_{S}\mathbf{D}\cdot d\mathbf{S} = Q_{\text{free, enclosed}}$，它表明通过任意闭合[曲面](@entry_id:267450)的[电位移场](@entry_id:273493)通量，精确地等于该[曲面](@entry_id:267450)所包围的**总[自由电荷](@entry_id:264392)**。这一结论完全不依赖于[曲面](@entry_id:267450)内部介质的复杂性。即使介质是各向异性的、非均匀的，甚至包含着复杂的永久[极化场](@entry_id:197617)，只要我们能计算出其内部的自由电荷总量，$\mathbf{D}$ 场的总通量就确定了 。这为分析复杂[复合材料](@entry_id:139856)中的静电问题提供了极其强大的工具。

### [本构关系](@entry_id:186508)：场与物质的相互作用

麦克斯韦方程组本身包含的场量多于方程数量，因此是不封闭的。为了求解一个特定的电磁问题，我们必须补充描述特定材料如何响应[电磁场](@entry_id:265881)的方程，这些方程被称为**[本构关系](@entry_id:186508) (constitutive relations)**。它们将辅助场 $(\mathbf{D}, \mathbf{H})$ 与基本场 $(\mathbf{E}, \mathbf{B})$ 联系起来。

最简单的情形是**线性、各向同性、均匀 (linear, isotropic, homogeneous, LIH)** 的介质。在这种介质中，[本构关系](@entry_id:186508)为：
$$
\mathbf{D} = \epsilon \mathbf{E}, \qquad \mathbf{B} = \mu \mathbf{H}
$$
其中，**[介电常数](@entry_id:146714) (permittivity)** $\epsilon$ 和**[磁导率](@entry_id:154559) (permeability)** $\mu$ 是标量常数。

然而，在许多先进材料和多物理场耦合问题中，情况要复杂得多。
对于**各向异性 (anisotropic)** 介质，如晶体或受应力作用的材料，介质在不同方向上对[电场](@entry_id:194326)的响应可能不同。此时，$\mathbf{D}$ 场的方向通常不再与 $\mathbf{E}$ 场的方向平行。这种行为由张量本构关系描述 ：
$$
\mathbf{D} = \boldsymbol{\epsilon} \mathbf{E}, \qquad \mathbf{B} = \boldsymbol{\mu} \mathbf{H}
$$
这里，$\boldsymbol{\epsilon}$ 和 $\boldsymbol{\mu}$ 是[二阶张量](@entry_id:199780)（可以用 $3 \times 3$ 矩阵表示）。例如，[电位移场](@entry_id:273493)的第 $i$ 个分量 $D_i$ 依赖于[电场](@entry_id:194326)的所有三个分量：$D_i = \sum_{j} \epsilon_{ij} E_j$。这些张量还具有重要的物理属性：对于无损耗的**互易介质 (reciprocal medium)**，它们是对称的（即 $\epsilon_{ij} = \epsilon_{ji}$）；为了保证系统的[能量稳定性](@entry_id:748991)，它们必须是正定的，以确保任何非[零场](@entry_id:199169)储存的能量密度 $u=\tfrac{1}{2}\mathbf{E}\cdot(\boldsymbol{\epsilon}\mathbf{E})+\tfrac{1}{2}\mathbf{H}\cdot(\boldsymbol{\mu}\mathbf{H})$ 始终为正 。

在[多物理场耦合](@entry_id:171389)模拟中，材料属性本身可能依赖于其他物理场，如温度 $T$ 或应变 $\boldsymbol{\varepsilon}_{mech}$，从而成为空间 $(\mathbf{x})$ 和时间 $(t)$ 的函数。当 $\epsilon$ 或 $\mu$ 随时间和空间变化时，它们会产生等效的[电荷](@entry_id:275494)或[电流源](@entry_id:275668)。例如，将 $\mathbf{D} = \epsilon(\mathbf{x}, t) \mathbf{E}$ 代入[安培-麦克斯韦定律](@entry_id:266368)中的位移电流项，并使用乘法法则展开，我们得到：
$$
\frac{\partial \mathbf{D}}{\partial t} = \frac{\partial (\epsilon \mathbf{E})}{\partial t} = \epsilon \frac{\partial \mathbf{E}}{\partial t} + \frac{\partial \epsilon}{\partial t} \mathbf{E}
$$
这里的额外项 $(\partial \epsilon/\partial t) \mathbf{E}$ 表现为一个等效的[电流源](@entry_id:275668)，它源于[材料极化](@entry_id:269695)率随时间的变化。同样，空间变化的[介电常数](@entry_id:146714) $\epsilon(\mathbf{x})$ 在[高斯定律](@entry_id:141493) $\nabla \cdot (\epsilon(\mathbf{x}) \mathbf{E}) = \rho_f$ 中，展开后会产生一个与 $\nabla\epsilon$ 相关的等效[电荷](@entry_id:275494)项。理解这些由材料属性时空变化引入的耦合项，对于精确建模至关重要 。

### [材料界面](@entry_id:751731)处的边界条件

在处理由不同材料组成的系统时，我们需要知道[电磁场](@entry_id:265881)在[材料界面](@entry_id:751731)上如何变化。这些**边界条件 (boundary conditions)** 可以通过将[麦克斯韦方程组的积分形式](@entry_id:264550)应用于跨越界面的微小“高斯药盒”和“安培回路”来导出。

假设一个光滑界面将区域1和区域2分开，[单位法向量](@entry_id:178851) $\hat{\mathbf{n}}$ 从区域1指向区域2。界面上可能存在自由[表面电荷密度](@entry_id:272693) $\rho_s$ 和自由[表面电流密度](@entry_id:274967) $\mathbf{J}_s$。在界面上，[电磁场](@entry_id:265881)必须满足以下四个条件 ：

1.  $\hat{\mathbf{n}}\cdot(\mathbf{D}_2 - \mathbf{D}_1) = \rho_s$
    *   [电位移场](@entry_id:273493)的法向分量的跳变等于界面上的自由[表面电荷密度](@entry_id:272693)。若无自由表面电荷，则 $\mathbf{D}$ 的法向分量连续。

2.  $\hat{\mathbf{n}}\cdot(\mathbf{B}_2 - \mathbf{B}_1) = 0$
    *   [磁感应强度](@entry_id:144179)的法向分量总是连续的。这反映了磁单极子不存在的更深层物理原理。

3.  $\hat{\mathbf{n}}\times(\mathbf{E}_2 - \mathbf{E}_1) = \mathbf{0}$
    *   [电场](@entry_id:194326)强度的切向分量总是连续的。

4.  $\hat{\mathbf{n}}\times(\mathbf{H}_2 - \mathbf{H}_1) = \mathbf{J}_s$
    *   [磁场强度](@entry_id:197932)的切向分量的跳变等于界面上的自由[表面电流密度](@entry_id:274967)。若无自由[表面电流](@entry_id:261791)，则 $\mathbf{H}$ 的切向分量连续。

这四条边界条件是普适的，适用于任何类型的材料，包括[各向异性介质](@entry_id:187796)。它们是求解包含多个材料区域的电磁问题的基础，也是有限元等数值方法的关键组成部分。

### 数学结构与势函数

[麦克斯韦方程组](@entry_id:150940)不仅是物理定律，也蕴含着深刻的数学结构。**[亥姆霍兹分解](@entry_id:181767)定理 (Helmholtz decomposition theorem)** 指出，在无限大或边界条件合适的区域内，任何矢量场都可以唯一地分解为一个无旋（irrotational）部分和一个无散（solenoidal）部分。

我们可以将这一定理应用于[电磁场](@entry_id:265881) ：
*   对于[磁感应强度](@entry_id:144179) $\mathbf{B}$，高斯[磁场](@entry_id:153296)定律 $\nabla \cdot \mathbf{B} = 0$ 表明 $\mathbf{B}$ 场是一个纯粹的[无散场](@entry_id:260932)（即[螺线管](@entry_id:261182)场）。一个[无散场](@entry_id:260932)总可以表示为另一个[矢量场的旋度](@entry_id:146155)。这启发我们引入**磁矢量势 (magnetic vector potential)** $\mathbf{A}$，使得：
    $$ \mathbf{B} = \nabla \times \mathbf{A} $$

*   对于[电场](@entry_id:194326)强度 $\mathbf{E}$，它通常既有散度（源于[电荷](@entry_id:275494)）又有旋度（源于变化的[磁场](@entry_id:153296)），因此它同时包含无旋和无散两个部分。将 $\mathbf{B} = \nabla \times \mathbf{A}$ 代入[法拉第定律](@entry_id:149836)，我们得到 $\nabla \times \mathbf{E} = -\partial_t (\nabla \times \mathbf{A})$，可以整理为 $\nabla \times (\mathbf{E} + \partial_t \mathbf{A}) = \mathbf{0}$。一个[无旋场](@entry_id:183486)可以表示为一个[标量场的梯度](@entry_id:270765)。因此，我们引入**电[标量势](@entry_id:276177) (electric scalar potential)** $\phi$，使得：
    $$ \mathbf{E} + \frac{\partial \mathbf{A}}{\partial t} = -\nabla \phi \quad \implies \quad \mathbf{E} = -\nabla\phi - \frac{\partial\mathbf{A}}{\partial t} $$

引入[势函数](@entry_id:176105) $\phi$ 和 $\mathbf{A}$ 的好处是巨大的：四个麦克斯韦方程中的两个（$\nabla \cdot \mathbf{B} = 0$ 和 $\nabla \times \mathbf{E} = -\partial_t \mathbf{B}$）被自动满足。我们从求解四个耦合的一阶矢量PDE，简化为求解关于两个势函数的[二阶PDE](@entry_id:175326)。

然而，势函数的定义并非唯一。对于任意一个光滑的标量函数 $\chi(\mathbf{x}, t)$，如果我们进行如下**[规范变换](@entry_id:176521) (gauge transformation)**：
$$
\mathbf{A}' = \mathbf{A} + \nabla \chi, \qquad \phi' = \phi - \frac{\partial \chi}{\partial t}
$$
可以证明，新的势 $(\phi', \mathbf{A}')$ 产生的[电场和磁场](@entry_id:261347) $(\mathbf{E}, \mathbf{B})$ 与原来完全相同 。这种选择 $\chi$ 的自由度被称为**规范自由度 (gauge freedom)**。我们可以利用这种自由度来选择一个**[规范条件](@entry_id:749730) (gauge condition)**，以简化[势函数](@entry_id:176105)所满足的方程。

两种最常见的规范是：
1.  **[库仑规范](@entry_id:273044) (Coulomb gauge)**：$\nabla \cdot \mathbf{A} = 0$。在此规范下，[高斯电场定律](@entry_id:146732)变为泊松方程 $\nabla^2 \phi = -\rho_f/\epsilon$，其解在形式上与[静电学](@entry_id:140489)相同，表明[标量势](@entry_id:276177)是瞬时响应[电荷分布](@entry_id:144400)的。这个规范在量子力学和分离场的横向与纵向分量时很有用。

2.  **[洛伦兹规范](@entry_id:153650) (Lorenz gauge)**：$\nabla \cdot \mathbf{A} + \mu\epsilon \frac{\partial \phi}{\partial t} = 0$。这个规范的优越性在于它能将麦克斯韦方程组完全解耦为两个对称的[非齐次波动方程](@entry_id:176877) ：
    $$
    \nabla^2 \phi - \mu\epsilon \frac{\partial^2 \phi}{\partial t^2} = -\frac{\rho_f}{\epsilon}
    $$
    $$
    \nabla^2 \mathbf{A} - \mu\epsilon \frac{\partial^2 \mathbf{A}}{\partial t^2} = -\mu \mathbf{J}_f
    $$
    这些[波动方程](@entry_id:139839)清晰地揭示了电磁扰动以有限速度 $v = 1/\sqrt{\mu\epsilon}$ 传播。其解可以表示为**[推迟势](@entry_id:204770) (retarded potentials)** 的形式，体现了因果律：在时间 $t$、位置 $\mathbf{x}$ 处的势，是由源在更早的**[推迟时间](@entry_id:274033)** $t_r = t - |\mathbf{x}-\mathbf{x}'|/v$ 时刻的状态决定的，其中 $|\mathbf{x}-\mathbf{x}'|/v$ 正是信号从源点 $\mathbf{x}'$ 传播到观察点 $\mathbf{x}$ 所需的时间 。

### 电磁学中的守恒律

如同力学中的基本守恒律一样，麦克斯韦方程组也蕴含着深刻的能量和动量守恒定律。这些定律在[多物理场耦合](@entry_id:171389)中扮演着核心角色，因为它们精确地描述了[电磁场](@entry_id:265881)与其它物理系统（如热学、力学）之间的能量和动量交换。

#### [能量守恒](@entry_id:140514)

通过对法拉第定律和[安培-麦克斯韦定律](@entry_id:266368)进行适当的矢量运算，可以推导出电磁[能量的[局域守](@entry_id:268756)恒定律](@entry_id:261997)，即**坡印亭定理 (Poynting's theorem)** ：
$$
\frac{\partial u}{\partial t} + \nabla \cdot \mathbf{S} = - \mathbf{J}_{\mathrm{f}} \cdot \mathbf{E}
$$
其中：
*   $u = \frac{1}{2} (\mathbf{E} \cdot \mathbf{D} + \mathbf{H} \cdot \mathbf{B})$ 是单位体积内的**[电磁能量密度](@entry_id:271095) (electromagnetic energy density)**。
*   $\mathbf{S} = \mathbf{E} \times \mathbf{H}$ 是**坡印亭矢量 (Poynting vector)**，代表单位时间通过单位面积的[能量流](@entry_id:142770)密度，即**[能流密度](@entry_id:266056) (energy flux density)**。

这个方程的物理意义是：在一个体积内，[电磁能量密度](@entry_id:271095)的增加率，加上通过边界流出的能量，等于[电磁场](@entry_id:265881)对[自由电流](@entry_id:191634)所做的负功。换言之，$\mathbf{J}_{\mathrm{f}} \cdot \mathbf{E}$ 这一项代表了[电磁场能量](@entry_id:265463)转化为其他形式能量的[功率密度](@entry_id:194407)。在导[电介质](@entry_id:147163)中，这部分能量通常通过**焦耳热 (Joule heating)** 不可逆地转化为热能，其[功率密度](@entry_id:194407)为 $\dot{q} = \mathbf{J}_{\mathrm{f}} \cdot \mathbf{E}$。这正是[电磁场](@entry_id:265881)与热传导方程耦合的主要机制 。

值得注意的是，如果材料属性随时间变化（例如，由于温度变化导致[介电常数](@entry_id:146714)改变），[能量守恒方程](@entry_id:748978)中会出现额外的[源项](@entry_id:269111)，代表[电磁场](@entry_id:265881)与导致材料属性变化的物理过程之间的能量交换 。

#### 动量守恒

[电磁场](@entry_id:265881)不仅携带能量，也携带动量。作用在物质上的洛伦兹力密度 $\mathbf{f} = \rho_{\mathrm{f}}\mathbf{E} + \mathbf{J}_{\mathrm{f}} \times \mathbf{B}$ 是[电磁场](@entry_id:265881)与力学系统动量交换的媒介。同样，通过对[麦克斯韦方程组](@entry_id:150940)的数学变换，可以将[洛伦兹力](@entry_id:145104)密度表示为纯粹场量的时空导数 ：
$$
\mathbf{f} = \nabla \cdot \mathbf{T} - \frac{\partial \mathbf{g}}{\partial t}
$$
这个方程是[电磁动量](@entry_id:268129)的[局域守恒定律](@entry_id:261997)。其中：
*   $\mathbf{g} = \mathbf{D} \times \mathbf{B}$ 是**[电磁动量](@entry_id:268129)密度 (electromagnetic momentum density)**。
*   $\mathbf{T}$ 是**[麦克斯韦应力张量](@entry_id:153513) (Maxwell stress tensor)**，一个[二阶张量](@entry_id:199780)。对于各向同性介质，其分量为：
    $$
    T_{ij} = \epsilon E_i E_j + \mu H_i H_j - \frac{1}{2}(\epsilon |\mathbf{E}|^2 + \mu |\mathbf{H}|^2)\delta_{ij}
    $$

[动量守恒](@entry_id:149964)方程可以改写为 $\mathbf{f} + \frac{\partial \mathbf{g}}{\partial t} = \nabla \cdot \mathbf{T}$。它的物理诠释是：作用于物质的力密度（[机械动量](@entry_id:156068)变化率）与[场动量密度](@entry_id:189791)的变化率之和，等于[麦克斯韦应力张量](@entry_id:153513)的散度。张量 $\mathbf{T}$ 描述了动量在空间中的流动。$\mathbf{T} \cdot \hat{\mathbf{n}}$ 代表通过以 $\hat{\mathbf{n}}$ 为法向的单位面积的动量流，也即作用在该面上的力。

因此，作用在体积 $V$ 内物质上的总电磁力可以通过一个包围该体积的闭合[曲面](@entry_id:267450) $\partial V$ 上的[面积分](@entry_id:275394)来计算：
$$
\mathbf{F}_{\mathrm{mech}} = \int_V \mathbf{f} \,dV = \oint_{\partial V} \mathbf{T}\cdot \hat{\mathbf{n}}\, dA - \frac{d}{dt}\int_{V} \mathbf{g}\,dV
$$
这个强大的公式允许我们通过计算物体外部的场来确定其所受的总力，这在计算[电动机](@entry_id:268448)、传感器和等离子体中的[电磁力](@entry_id:196024)时至关重要 。

### [准静态近似](@entry_id:264812)

在许多工程应用中，[电磁场](@entry_id:265881)的时[变频](@entry_id:196535)率 $\omega$ 相对较低，或者系统的特征尺寸 $L$ 较小，使得电磁[波的传播](@entry_id:144063)时间 $L/v$ 远小于变化的特征时间 $1/\omega$。在这些情况下，完整的波动行为变得不那么重要，我们可以采用**[准静态近似](@entry_id:264812) (quasistatic approximations)** 来简化[麦克斯韦方程组](@entry_id:150940)。

一个特别重要的近似是**磁准静态 (Magnetoquasistatic, MQS)** 近似。它适用于良导体中的低频问题，如[涡流加热](@entry_id:187291)、[电动机](@entry_id:268448)和变压器。其核心思想是忽略[安培-麦克斯韦定律](@entry_id:266368)中的[位移电流](@entry_id:190231) $\partial\mathbf{D}/\partial t$。

这一近似的有效性可以通过比较[位移电流](@entry_id:190231)和[传导电流](@entry_id:265343) $\mathbf{J}$ 的大小来判断。对于一个以角频率 $\omega$ 变化的场，它们的大小尺度分别为 $|\partial\mathbf{D}/\partial t| \sim \omega\epsilon E$ 和 $|\mathbf{J}| \sim \sigma E$。因此，MQS近似成立的条件是它们的比值远小于1 ：
$$
\frac{\omega \epsilon}{\sigma} \ll 1
$$
在此近似下，[安培定律](@entry_id:140092)恢复到其准静态形式 $\nabla \times \mathbf{H} \approx \mathbf{J}$。这意味着[磁场](@entry_id:153296)主要由传导电流产生，而[电场](@entry_id:194326)产生的[位移电流](@entry_id:190231)对[磁场](@entry_id:153296)的影响可以忽略不计。

在MQS框架下，如果导体还在以速度 $\mathbf{U}$ 运动（如在[磁流体动力学](@entry_id:264274)中），可以通过组合法拉第定律、欧姆定律和简化后的[安培定律](@entry_id:140092)得到[磁场](@entry_id:153296)的**[感应方程](@entry_id:750617) (induction equation)**：
$$
\frac{\partial \mathbf{B}}{\partial t} \approx \nabla \times (\mathbf{U} \times \mathbf{B}) - \nabla \times \left(\frac{1}{\sigma\mu} \nabla \times \mathbf{B}\right)
$$
这个方程描述了[磁场](@entry_id:153296)被流体**平流 (advection)**（第一项）和在导体中**[扩散](@entry_id:141445) (diffusion)**（第二项）的竞争过程。这两个过程的相对重要性由一个无量纲参数——**[磁雷诺数](@entry_id:270538) (magnetic Reynolds number)** 来决定：
$$
\mathrm{Rm} = \mu \sigma U L
$$
当 $\mathrm{Rm} \gg 1$ 时，[磁场](@entry_id:153296)线仿佛被“冻结”在流体中并随之运动；当 $\mathrm{Rm} \ll 1$ 时，[磁场](@entry_id:153296)则主要在导体中[扩散](@entry_id:141445)。需要强调的是，判断MQS近似是否有效的标准（$\omega\epsilon/\sigma \ll 1$）与判断平流和[扩散](@entry_id:141445)哪个占主导的标准（$\mathrm{Rm}$ 的大小）是两个独立的问题 。

与MQS相对应的是**电准静态 (Electroquasistatic, EQS)** 近似，它在电容性、低[电导](@entry_id:177131)或无[电导](@entry_id:177131)的系统中很有用，此时法拉第定律中的感应项 $-\partial\mathbf{B}/\partial t$ 被忽略。正确地选择和应用这些[准静态近似](@entry_id:264812)，是高效、准确地进行[电磁场](@entry_id:265881)多物理场耦合仿真的关键。