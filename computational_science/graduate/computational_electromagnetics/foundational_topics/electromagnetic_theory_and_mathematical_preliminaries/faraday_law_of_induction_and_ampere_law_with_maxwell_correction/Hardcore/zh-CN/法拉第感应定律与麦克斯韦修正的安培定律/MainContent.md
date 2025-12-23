## 引言
[法拉第感应定律](@entry_id:146175)和经麦克斯韦修正的安培定律是经典电磁理论的动态核心，是理解从电路到光波等一切电磁现象的基石。它们不仅是优雅的数学方程，更蕴含着深刻的物理对称性和守恒律。然而，超越了入门级的定义，对这些定律的深刻内涵——例如[能量守恒](@entry_id:140514)如何决定其形式、它们与狭义相对论的内在联系，以及它们如何延伸到[复杂介质](@entry_id:164088)和现代计算方法中——的理解，对于研究生和高级研究人员至关重要。

本文旨在填补这一认知空白。在第一章“原理与机制”中，我们将剖析这些定律的数学结构、其与[能量守恒](@entry_id:140514)及相对论[协变](@entry_id:634097)性的联系，并探讨其在[复杂介质](@entry_id:164088)中的推广。接下来的“应用与跨学科连接”一章将展示这些原理如何在准静态系统、[电磁波传播](@entry_id:272130)以及计算电磁学等多个领域中发挥作用。最后，通过“动手实践”部分，读者将有机会运用这些理论解决具体的物理和工程问题，从而将抽象的理论转化为强大的分析与设计能力。

## 原理与机制

在介绍性章节之后，我们现在深入探讨电磁理论的核心——[法拉第感应定律](@entry_id:146175)和[安培-麦克斯韦定律](@entry_id:266368)。这些定律不仅是宏观电磁现象的数学描述，更体现了深刻的物理原理和对称性。本章的目标是阐明这些定律的结构、其物理基础，以及它们在[复杂介质](@entry_id:164088)和计算方法中的延伸应用。

### 麦克斯韦感应与[安培定律](@entry_id:140092)的结构

[法拉第感应定律](@entry_id:146175)和修正后的[安培定律](@entry_id:140092)构成了[麦克斯韦方程组](@entry_id:150940)中描述场源关系的动态核心。理解它们的[微分](@entry_id:158718)和积分形式，以及两者之间的联系，对于理论分析和数值求解都至关重要。

#### [法拉第感应定律](@entry_id:146175)

[法拉第感应定律](@entry_id:146175)描述了变化的[磁场](@entry_id:153296)如何产生[电场](@entry_id:194326)。其积分形式通常是介绍该定律的起点，它直接与实验观测相关。对于一个以闭合回路 $\partial S$ 为边界的任意[曲面](@entry_id:267450) $S$，穿过[曲面](@entry_id:267450) $S$ 的[磁通量](@entry_id:268943) $\Phi_B = \int_{S}\mathbf{B}\cdot d\mathbf{S}$ 的变化率会产生一个电动势 (EMF) $\mathcal{E}$：

$$
\mathcal{E} = \oint_{\partial S}\mathbf{E}\cdot d\mathbf{l} = -\frac{d\Phi_B}{dt}
$$

其中，[电场](@entry_id:194326) $\mathbf{E}$ 沿回路 $\partial S$ 的[线积分](@entry_id:141417)定义了[电动势](@entry_id:203175)，而[磁感应强度](@entry_id:144179) $\mathbf{B}$ 在[曲面](@entry_id:267450) $S$ 上的[面积分](@entry_id:275394)定义了磁通量。回路的方向和[曲面](@entry_id:267450)的法向由[右手定则](@entry_id:156766)关联。此处的负号是[楞次定律](@entry_id:139402)的数学体现，它指明了[感应电场](@entry_id:267314)的方向总是抵抗[磁通量](@entry_id:268943)的变化。这一符号的深刻物理意义将在后文探讨。

当回路和[曲面](@entry_id:267450)固定不变时，时间导数可以移到积分号内部，作用于场本身。此时，定律写作 ：

$$
\oint_{\partial S}\mathbf{E}\cdot d\mathbf{l} = -\frac{\partial}{\partial t}\int_{S}\mathbf{B}\cdot d\mathbf{S} = -\int_{S}\frac{\partial\mathbf{B}}{\partial t}\cdot d\mathbf{S}
$$

为了从描述回路和[曲面](@entry_id:267450)等宏观量的积分形式过渡到描述空间每一点场行为的[微分形式](@entry_id:146747)，我们需要借助[斯托克斯定理](@entry_id:264534) (Stokes' Theorem)。该定理指出，对于一个连续可微的向量场（$C^1$ 类场），其沿闭合边界 $\partial S$ 的环流等于其旋度穿过[曲面](@entry_id:267450) $S$ 的通量：

$$
\oint_{\partial S}\mathbf{E}\cdot d\mathbf{l} = \int_{S}(\nabla\times\mathbf{E})\cdot d\mathbf{S}
$$

斯托克斯定理的成立依赖于场的光滑性和[曲面](@entry_id:267450)的良好几何性质（分片光滑、可定向），但并不要求场所在的整个区域具有特定的拓扑结构（如[单连通性](@entry_id:189103)） 。将[斯托克斯定理应用](@entry_id:204094)于[法拉第定律](@entry_id:149836)的左侧，我们得到：

$$
\int_{S}(\nabla\times\mathbf{E})\cdot d\mathbf{S} = -\int_{S}\frac{\partial\mathbf{B}}{\partial t}\cdot d\mathbf{S}
$$

由于这个关系式对于空间中任意选择的[曲面](@entry_id:267450) $S$ 都必须成立，因此两个积分号下的被积函数必须处处相等。这就引出了法拉第定律的微分形式：

$$
\nabla\times\mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}
$$

这个局部方程是[计算电磁学](@entry_id:265339)中许多时域算法（如FDTD）的基础。值得注意的是，如果[曲面](@entry_id:267450)或回路本身在[磁场](@entry_id:153296)中运动，完整的[感应电动势](@entry_id:264372)还包含由洛伦兹力产生的[动生电动势](@entry_id:264357)项。完整的积分定律应写为 $\oint_{\partial S(t)} (\mathbf{E} + \mathbf{v} \times \mathbf{B}) \cdot d\mathbf{l} = -\frac{d}{dt}\int_{S(t)}\mathbf{B}\cdot d\mathbf{S}$，其中 $\mathbf{v}$ 是回路元的运动速度。因此，最初的积分定律形式仅对固定回路普适有效 。

#### [安培-麦克斯韦定律](@entry_id:266368)

在[静磁学](@entry_id:140120)中，[安培环路定律](@entry_id:140092) $\nabla \times \mathbf{H} = \mathbf{J}$ 将磁场强度 $\mathbf{H}$ 的旋度与产生该场的[自由电流](@entry_id:191634)密度 $\mathbf{J}$ 联系起来。然而，这个方程在处理[时变场](@entry_id:180620)时存在一个根本性的缺陷。取其散度，我们得到 $\nabla \cdot (\nabla \times \mathbf{H}) \equiv 0$，这意味着 $\nabla \cdot \mathbf{J} = 0$。这与电荷守恒的连续性方程 $\nabla \cdot \mathbf{J} + \frac{\partial \rho}{\partial t} = 0$ 相矛盾，因为后者允许电荷密度 $\rho$ 随时间变化。

麦克斯韦通过引入一个额外的项——**位移电流密度** (displacement current density)，解决了这一矛盾。从高斯定律 $\nabla \cdot \mathbf{D} = \rho$ 出发（其中 $\mathbf{D}$ 是[电位移场](@entry_id:273493)，$\rho$ 是[自由电荷](@entry_id:264392)密度），对时间求导得到 $\frac{\partial}{\partial t}(\nabla \cdot \mathbf{D}) = \frac{\partial \rho}{\partial t}$。假设时空导数可交换，则 $\nabla \cdot (\frac{\partial \mathbf{D}}{\partial t}) = \frac{\partial \rho}{\partial t}$。代入连续性方程，我们得到：

$$
\nabla \cdot \mathbf{J} + \nabla \cdot \left(\frac{\partial \mathbf{D}}{\partial t}\right) = \nabla \cdot \left(\mathbf{J} + \frac{\partial \mathbf{D}}{\partial t}\right) = 0
$$

麦克斯韦假设，产生[磁场](@entry_id:153296)的源不仅是传导电流 $\mathbf{J}$，还应包括这个新的矢量 $\frac{\partial \mathbf{D}}{\partial t}$，使得总的“电流”源是无散的。这样，修正后的[安培定律](@entry_id:140092)，即[安培-麦克斯韦定律](@entry_id:266368)，其[微分形式](@entry_id:146747)为 ：

$$
\nabla\times\mathbf{H} = \mathbf{J} + \frac{\partial \mathbf{D}}{\partial t}
$$

这里的 $\mathbf{J}$ 指的是自由电荷的运动（[传导电流](@entry_id:265343)），而[位移电流](@entry_id:190231)项 $\frac{\partial \mathbf{D}}{\partial t}$ 则源于[电位移场](@entry_id:273493)的时变。在介质中，$\mathbf{D} = \varepsilon_0 \mathbf{E} + \mathbf{P}$，其中 $\mathbf{P}$ 是[电极化强度](@entry_id:141475)，描述了束缚[电荷](@entry_id:275494)的响应。因此，[位移电流](@entry_id:190231)包含了真空[电场](@entry_id:194326)变化和介质极化变化两个部分的贡献。这个修正项是麦克斯韦理论的巅峰之作，它预言了[电磁波](@entry_id:269629)的存在。

与法拉第定律类似，通过斯托克斯定理，我们可以得到[安培-麦克斯韦定律](@entry_id:266368)的积分形式 ：

$$
\oint_{\partial S}\mathbf{H}\cdot d\mathbf{l} = \int_{S}\mathbf{J}\cdot d\mathbf{S} + \int_{S}\frac{\partial \mathbf{D}}{\partial t}\cdot d\mathbf{S}
$$

对于固定[曲面](@entry_id:267450)，右侧第二项可以写作总时间导数 $\frac{d}{dt}\int_{S}\mathbf{D}\cdot d\mathbf{S}$。这个积分形式明确指出，[磁场](@entry_id:153296)的环流由穿过[曲面](@entry_id:267450)的[传导电流](@entry_id:265343)和位移电流共同产生。

### [能量守恒](@entry_id:140514)作为基础

物理定律的形式并非任意，它们必须服从更深层次的守恒原理。法拉第定律中的负号和[安培-麦克斯韦定律](@entry_id:266368)中的位移电流项，都可以从[能量守恒](@entry_id:140514)的角度得到深刻的理解。

#### [楞次定律](@entry_id:139402)与[能量守恒](@entry_id:140514)

法拉第定律中的负号，即楞次定律，是[能量守恒](@entry_id:140514)的直接体现。我们可以通过两种方式来论证这一点 。

第一种方式是考虑场的能量。[电磁场](@entry_id:265881)的能量密度 $u$ 和[能量流](@entry_id:142770)密度（坡印亭矢量） $\mathbf{S}$ 由坡印亭定理联系，该定理源于[麦克斯韦方程组](@entry_id:150940)。让我们假设法拉第定律的形式为 $\nabla \times \mathbf{E} = \sigma \frac{\partial \mathbf{B}}{\partial t}$，其中 $\sigma$ 是待定的符号（$+1$ 或 $-1$）。在无源的线性介质中，通过标准的矢量恒等式和[麦克斯韦方程组](@entry_id:150940)，可以推导出[能量平衡方程](@entry_id:191484)：

$$
\frac{\partial}{\partial t} \left( \frac{1}{2}\mathbf{E}\cdot\mathbf{D} - \frac{\sigma}{2}\mathbf{B}\cdot\mathbf{H} \right) + \nabla \cdot (\mathbf{E} \times \mathbf{H}) = 0
$$

为了使括号中的项代表一个物理上有意义的、正定的能量密度 $u = \frac{1}{2}(\epsilon E^2 + \mu H^2)$，符号 $\sigma$ 必须为 $-1$。如果 $\sigma = +1$，能量密度将是 $u = \frac{1}{2}(\epsilon E^2 - \mu H^2)$，它可以为负值，这意味着可以从真空中凭空创造能量，这在物理上是不可接受的。因此，[能量守恒](@entry_id:140514)要求[法拉第定律](@entry_id:149836)必须带有负号。

第二种方式是考虑一个力学思想实验。想象一个导体回路以恒定速度被拉出均匀[磁场](@entry_id:153296)区域。[磁通量](@entry_id:268943)减少，产生感应电流。这个电流在[磁场](@entry_id:153296)中会受到洛伦兹力。根据[能量守恒](@entry_id:140514)，维持回路恒速运动所需的[机械功率](@entry_id:163535)必须等于回路上因电阻而消耗的热功率 $I^2 R$。这意味着拉动回路的力必须克服一个阻碍运动的磁力。只有当[感应电流](@entry_id:270047)产生的[磁场](@entry_id:153296)试图“填补”正在减少的[磁通量](@entry_id:268943)时，才会产生这样的阻力。这个“反抗”行为正是楞次定律的体现，它同样要求[感应电动势](@entry_id:264372)与磁通量变化率反号，即 $\sigma = -1$。如果符号为正，磁力将是助推力，导致电流和速度失控增长，凭空产生能量，这显然违背了[能量守恒](@entry_id:140514)定律。

#### [位移电流](@entry_id:190231)与能量储存

[位移电流](@entry_id:190231)不仅是为了数学上的自洽，它在物理上也扮演着能量转换和传输的关键角色。再次考察坡印亭定理的完整形式：

$$
-\nabla \cdot (\mathbf{E} \times \mathbf{H}) = \mathbf{J} \cdot \mathbf{E} + \mathbf{E} \cdot \frac{\partial \mathbf{D}}{\partial t} + \mathbf{H} \cdot \frac{\partial \mathbf{B}}{\partial t}
$$

左边代表单位体积内能量的净流入速率。右边第一项 $\mathbf{J} \cdot \mathbf{E}$ 是[电场](@entry_id:194326)对自由电荷做功的[功率密度](@entry_id:194407)，通常表现为[焦耳热](@entry_id:150496)。后两项代表储存在电场和磁场中能量密度的增加率。特别是 $\mathbf{E} \cdot \frac{\partial \mathbf{D}}{\partial t}$ 这一项，它直接来源于[安培-麦克斯韦定律](@entry_id:266368)中的[位移电流](@entry_id:190231)。在一个理想的无损电容器充电过程中，极板间没有[传导电流](@entry_id:265343)（$\mathbf{J}=0$），但有时变的[电场](@entry_id:194326)。能量从外部电路通过坡印亭矢量流入[电容器](@entry_id:267364)内部，并以 $\frac{\partial u_E}{\partial t} = \mathbf{E} \cdot \frac{\partial \mathbf{D}}{\partial t}$ 的速率储存在[电场](@entry_id:194326)中 。因此，[位移电流](@entry_id:190231)不仅是产生[磁场](@entry_id:153296)的“等效”电流，它也是能量在[电场](@entry_id:194326)中储存和释放的媒介。

### 相对论[协变](@entry_id:634097)性

麦克斯韦方程组的结构之美，最深刻地体现在其与[狭义相对论](@entry_id:275552)的内在联系中。爱因斯坦建立狭义相对论的两个基本假设之一，就是“[光速不变原理](@entry_id:201268)”，而这个原理本身就是麦克斯韦方程组的直接推论。[麦克斯韦方程组的形式](@entry_id:189625)在所有惯性参考系中保持不变，这一性质被称为**[洛伦兹协变性](@entry_id:161987)** (Lorentz covariance)。

我们可以通过一个思想实验来数值地验证这一点 。考虑一个在实验室参考系 $\mathcal{S}$ 中沿x轴传播的平面[电磁波](@entry_id:269629)。其场量 $\mathbf{E}$ 和 $\mathbf{B}$ 是[麦克斯韦方程组](@entry_id:150940)的精确解。现在，我们切换到一个相对于 $\mathcal{S}$ 系以速度 $u$ 沿x轴运动的新[参考系](@entry_id:169232) $\mathcal{S}'$。根据狭义相对论，时空坐标和[电磁场](@entry_id:265881)分量都需要通过[洛伦兹变换](@entry_id:176827)进行转换：

$$
t' = \gamma (t - ux/c^2), \quad x' = \gamma (x - ut)
$$
$$
\mathbf{E}' = \gamma(\mathbf{E} + \mathbf{u} \times \mathbf{B}) - \frac{\gamma^2}{\gamma+1}\frac{\mathbf{u}}{c^2}(\mathbf{u}\cdot\mathbf{E}) \quad \text{(general form)}
$$
$$
\mathbf{B}' = \gamma(\mathbf{B} - \frac{\mathbf{u} \times \mathbf{E}}{c^2}) - \frac{\gamma^2}{\gamma+1}\frac{\mathbf{u}}{c^2}(\mathbf{u}\cdot\mathbf{B}) \quad \text{(general form)}
$$

将 $\mathcal{S}$ 系中的[平面波解](@entry_id:195230)代入，我们可以得到在新[参考系](@entry_id:169232) $\mathcal{S}'$ 中观测到的场 $\mathbf{E}'$ 和 $\mathbf{B}'$ (作为 $x'$ 和 $t'$ 的函数)。这些变换后的场看起来会不一样——它们的振幅、频率和波长都会因[相对论性多普勒效应](@entry_id:267059)而改变。然而，核心问题是：这些新的场 $\mathbf{E}'(x', t')$ 和 $\mathbf{B}'(x', t')$ 是否仍然满足[麦克斯韦方程组](@entry_id:150940)在 $\mathcal{S}'$ 系中的形式，即 $\nabla' \times \mathbf{E}' = -\frac{\partial \mathbf{B}'}{\partial t'}$ 和 $\nabla' \times \mathbf{B}' = \mu_0\epsilon_0\frac{\partial \mathbf{E}'}{\partial t'}$？

通过数值计算，例如使用有限差分来近似求导，我们可以计算[麦克斯韦方程组](@entry_id:150940)的残差。结果表明，只要变换是正确的，残差在[数值精度](@entry_id:173145)范围内为零。这雄辩地证明了[麦克斯韦方程组](@entry_id:150940)的[洛伦兹协变性](@entry_id:161987)。[电场和磁场](@entry_id:261347)并非独立的实体，而是同一个物理实体——电磁场张量——在不同[参考系](@entry_id:169232)下的不同表现。

### [复杂介质](@entry_id:164088)中的电动力学

在实际应用中，[电磁场](@entry_id:265881)与各种[复杂介质](@entry_id:164088)相互作用。麦克斯韦方程组的宏观形式通过[电位移场](@entry_id:273493) $\mathbf{D}$ 和[磁场强度](@entry_id:197932) $\mathbf{H}$ 来包含介质的响应，这需要辅以描述介质电磁特性的**[本构关系](@entry_id:186508)** (constitutive relations)。

#### [色散介质](@entry_id:180771)

在许多介质中，极化响应并非瞬时完成，而是依赖于[电场](@entry_id:194326)的历史。这种现象称为**[色散](@entry_id:263750)** (dispersion)。此时，简单的[本构关系](@entry_id:186508) $\mathbf{D} = \epsilon \mathbf{E}$ 不再适用。取而代之的是一个卷积关系 ：

$$
\mathbf{D}(t) = \int_{-\infty}^{t} \epsilon(t-t') \mathbf{E}(t') dt' = (\epsilon * \mathbf{E})(t)
$$

其中，$\epsilon(t)$ 是[介电响应](@entry_id:140146)函数。由于物理响应不能发生在激励之前，$\epsilon(t)$ 必须满足[因果性条件](@entry_id:161083)，即当 $t  0$ 时 $\epsilon(t)=0$。在[频域](@entry_id:160070)中，卷积定理使该关系简化为乘积：$\mathbf{D}(\omega) = \epsilon(\omega) \mathbf{E}(\omega)$。这里的 $\epsilon(\omega)$ 是一个复数，称为[复介电常数](@entry_id:160910)，其频率依赖性描述了[色散](@entry_id:263750)。

$$
\epsilon(\omega) = \epsilon'(\omega) - i\epsilon''(\omega)
$$

其实部 $\epsilon'(\omega)$ 与能量储存有关，虚部 $\epsilon''(\omega)$ 与能量损耗（吸收）有关。因果性在数学上导致 $\epsilon'(\omega)$ 和 $\epsilon''(\omega)$ 并非独立，它们通过克拉默-克若尼关系 (Kramers-Kronig relations) 相互关联。一个具体的例子是**[德拜弛豫模型](@entry_id:203189)** (Debye relaxation model)，它描述了偶极子在交变[电场](@entry_id:194326)中的弛豫过程，其[复介电常数](@entry_id:160910)为：

$$
\epsilon(\omega) = \epsilon_{\infty} + \frac{\epsilon_{s}-\epsilon_{\infty}}{1+i\omega\tau}
$$

在这种情况下，位移电流 $\mathbf{J}_d(\omega) = i\omega \mathbf{D}(\omega) = i\omega \epsilon(\omega) \mathbf{E}(\omega)$ 也会是一个复杂的函数，同时包含储能和损耗的成分。

#### [非线性](@entry_id:637147)介质

当外加[电场](@entry_id:194326)非常强时，许多介质的响应不再是线性的。例如，在**[克尔效应](@entry_id:138959)** (Kerr effect) 中，[介电常数](@entry_id:146714)本身依赖于[电场](@entry_id:194326)强度 ：

$$
\mathbf{D}(\mathbf{E}) = \epsilon(\mathbf{E}) \mathbf{E}, \quad \text{with} \quad \epsilon(\mathbf{E}) = \epsilon_0 \epsilon_L + \epsilon_0 \alpha \lVert \mathbf{E} \rVert^2
$$

在这种情况下，[位移电流](@entry_id:190231)的计算变得更加复杂。根据链式法则，我们有：

$$
\mathbf{J}_d = \frac{\partial \mathbf{D}}{\partial t} = \frac{\partial \mathbf{D}}{\partial \mathbf{E}} \frac{\partial \mathbf{E}}{\partial t} = \mathbb{C}(\mathbf{E}) \frac{\partial \mathbf{E}}{\partial t}
$$

其中 $\mathbb{C}(\mathbf{E})$ 是一个 $3 \times 3$ 的矩阵，称为**[微分](@entry_id:158718)[介电张量](@entry_id:194185)** (differential permittivity tensor)，它是 $\mathbf{D}$ 对 $\mathbf{E}$ 的雅可比矩阵。对于克尔介质，它具有各向异性的形式，即使介质本身是各向同性的。这个张量在求解[非线性](@entry_id:637147)问题的数值方法（如牛顿-拉夫逊法）中至关重要，它构成了[切线刚度矩阵](@entry_id:170852)的核心部分。同时，[非线性](@entry_id:637147)也改变了[储能](@entry_id:264866)的计算方式，能量密度 $u_E$ 不再是简单的 $\frac{1}{2}\mathbf{D}\cdot\mathbf{E}$，而需要通[过积分](@entry_id:753033) $u_E = \int_0^{\mathbf{E}} \mathbf{E'} \cdot d\mathbf{D}(\mathbf{E'})$ 来得到。

#### [准静态近似](@entry_id:264812)

在许多低频或小尺寸应用中，完整的[电磁波](@entry_id:269629)动行为可能不是主要效应，此时可以对[麦克斯韦方程组](@entry_id:150940)进行简化，即**[准静态近似](@entry_id:264812)** (quasistatic approximations) 。基本前提是系统特征尺寸 $L$ 远小于工作波长 $\lambda$，即系统“电尺寸”很小。

- **磁准静态 (MQS) 近似**: 当传导电流或磁效应占主导时，可以忽略位移电流。这通常发生在良导体中，其条件是传导电流远大于位移电流（$\sigma \gg \omega\epsilon$），并且系统是电小尺寸的。此时[安培定律](@entry_id:140092)简化为 $\nabla \times \mathbf{H} \approx \mathbf{J}$，但[法拉第定律](@entry_id:149836)保持完整。该近似适用于电感器、变压器和[涡流](@entry_id:271366)问题。

- **电准静态 (EQS) 近似**: 当[电荷](@entry_id:275494)或[电场](@entry_id:194326)效应占主导时，可以忽略[磁感应](@entry_id:153690)。此时法拉第定律近似为 $\nabla \times \mathbf{E} \approx \mathbf{0}$，这意味着[电场](@entry_id:194326)近似为[无旋场](@entry_id:183486)，可以由一个标量电[势的梯度](@entry_id:268447)表示。[安培-麦克斯韦定律](@entry_id:266368)保持完整，用于计算次要的[磁场](@entry_id:153296)。该近似适用于[电容器](@entry_id:267364)、绝缘系统和某些[生物电](@entry_id:177639)磁问题。

### 从连续到离散：计算中的守恒律

将麦克斯韦方程组应用于计算机求解时，我们需要将其从连续的[偏微分方程](@entry_id:141332)形式转化为离散的[代数方程](@entry_id:272665)形式。一个优秀的离散化方案，如[有限差分](@entry_id:167874)时域 (FDTD) 方法中使用的**Yee元胞** (Yee cell)，不仅要逼近原始方程，还应在离散层面保持其内在的物理守恒律。

一个关键的例子是电荷守恒。我们已经看到，在连续域中，[安培-麦克斯韦定律](@entry_id:266368) $\nabla \times \mathbf{H} = \mathbf{J} + \frac{\partial \mathbf{D}}{\partial t}$ 内蕴地保证了[电荷守恒](@entry_id:264158) $\nabla \cdot \mathbf{J} + \frac{\partial \rho}{\partial t} = 0$。在离散化的网格上，这两个方程也应紧密联系。

考虑一个采用[蛙跳格式](@entry_id:163462)更新电场和磁场的粒子-in-cell (PIC) 模拟 。[带电粒子运动](@entry_id:262424)产生[电流密度](@entry_id:190690) $J$，然后通过离散的[安培-麦克斯韦定律](@entry_id:266368)更新[电场](@entry_id:194326) $E$。同时，粒子位置的变化也改变了网格上的[电荷密度](@entry_id:144672) $\rho$。如果计算电流 $J$ 的数值方案（称为“电流淀积”）和计算[电荷密度](@entry_id:144672) $\rho$ 的方案是“[电荷守恒](@entry_id:264158)的”，即它们精确地满足离散形式的连续性方程，那么就可以证明，通过离散的[安培-麦克斯韦定律](@entry_id:266368)更新的[电场](@entry_id:194326)将自动地、精确地满足下一时刻离散的[高斯定律](@entry_id:141493)。

换言之，一个精确满足离散[连续性方程](@entry_id:195013)的电流淀积方案，可以保证由[龙格-库塔](@entry_id:140452)积分（或任何其他[时间积分](@entry_id:267413)）推进的[高斯定律](@entry_id:141493)的误差不会随时间累积。这是计算电磁学中的一个深刻结果，它展示了忠实地模仿麦克斯韦方程组的几何和拓扑结构（例如通过Yee元胞的[交错网格](@entry_id:147661)）如何能够在[数值模拟](@entry_id:137087)中自动保持基本的物理守恒律。这对于需要进行数百万个时间步长的长期、[高保真度模拟](@entry_id:750285)至关重要。