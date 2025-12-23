## 引言
连续性方程是描述电荷等[守恒量](@entry_id:161475)在空间和时间上如何分布与流动的基本物理定律，是理解和设计从宏观器件到[纳米结构](@entry_id:148157)中所有电子现象的基石。然而，在教学和研究中，该方程常被视为一个孤立的公式，其背后深刻的物理渊源、与前沿[量子理论](@entry_id:145435)的联系及其在不同科学领域的普适性往往未得到充分探讨。本文旨在填补这一知识鸿沟，为读者提供一个关于连续性方程的全面而深入的视角。

在接下来的内容中，我们将开启一段从基本原理到前沿应用的探索之旅。在“原理与机制”一章中，我们将从电荷[局域守恒定律](@entry_id:261997)这一物理学基本公理出发，推导连续性方程，并追溯其在玻尔兹曼输运方程乃至量子输运理论中的微观根基。随后，在“应用与跨学科连接”一章，我们将展示如何运用该方程来分析光电器件、晶体管和新兴材料的复杂行为，并惊奇地发现它在量子力学、[地球科学](@entry_id:749876)甚至宇宙学中的相似身影。最后，在“动手实践”部分，我们将通过具体的编程练习，将理论知识转化为解决实际输运问题的数值计算能力。通过这一结构化的学习路径，读者将不仅掌握一个公式，更能领会一种贯穿物理学始终的强大分析思想。

## 原理与机制

本章在前一章介绍的基础上，深入探讨连续性方程的物理原理和数学机制。我们将从电荷[局域守恒](@entry_id:751393)这一基本物理定律出发，逐步揭示其在[经典电动力学](@entry_id:270496)、半导体物理以及前沿量子输运理论中的具体表现形式和深刻内涵。我们的目标是建立一个从宏观唯象描述到微观动力学基础的完整知识框架。

### [电荷的局域守恒](@entry_id:202633)定律

物理学中最基本的守恒定律之一是电荷守恒定律。然而，仅仅说明总电荷量不随时间改变是不够的。一个更强、更有用的陈述是**[电荷的局域守恒](@entry_id:202633) (local conservation of charge)**，即电荷不会在某处凭空消失，而在另一处瞬间出现。任何区域内电荷量的变化，都必须归因于电荷通过该区域边界的流动。这构成了[连续性方程](@entry_id:195013)的物理基础。

考虑空间中一个固定的任意体积 $V$，其边界为闭合曲面 $A$。体积 $V$ 内的总电荷量 $Q(t)$ 是[电荷密度](@entry_id:144672) $\rho(\mathbf{r}, t)$ 的[体积分](@entry_id:171119)：
$$Q(t) = \iiint_V \rho(\mathbf{r}, t) \, dV$$

根据[电荷的局域守恒](@entry_id:202633)，该体积内电荷量随时间的变化率 $\frac{dQ}{dt}$ 必须等于净流入该体积的电流。如果我们定义电流密度矢量为 $\mathbf{J}(\mathbf{r}, t)$，那么流出曲面 $A$ 的总电流为 $\oiint_A \mathbf{J} \cdot d\mathbf{A}$。因此，流入的净电流为该值的负数。我们得到积分形式的连续性方程：
$$\frac{d}{dt} \iiint_V \rho(\mathbf{r}, t) \, dV = - \oiint_A \mathbf{J}(\mathbf{r}, t) \cdot d\mathbf{A}$$

由于体积 $V$ 是固定的，左侧的时间导数可以移到积分号内部。对于右侧的面积分，我们可以应用[高斯散度定理](@entry_id:188065)，它将穿过闭合曲面的通量与场在体积内的散度联系起来：$\oiint_A \mathbf{J} \cdot d\mathbf{A} = \iiint_V (\nabla \cdot \mathbf{J}) \, dV$。代入上式可得：
$$\iiint_V \frac{\partial \rho}{\partial t} \, dV = - \iiint_V (\nabla \cdot \mathbf{J}) \, dV$$

将所有项移到等式的一边：
$$\iiint_V \left( \frac{\partial \rho}{\partial t} + \nabla \cdot \mathbf{J} \right) \, dV = 0$$

由于这个关系式对于空间中任意选择的体积 $V$ 都必须成立，这意味着被积函数本身在每一点都必须为零。这样，我们就得到了微分形式的**[连续性方程](@entry_id:195013)**：
$$\frac{\partial \rho}{\partial t} + \nabla \cdot \mathbf{J} = 0$$

这个方程是一个精确的、点状的陈述，它表明[电荷密度](@entry_id:144672)的局部增加（$\frac{\partial \rho}{\partial t} > 0$）必然伴随着一个净的电流汇聚（$\nabla \cdot \mathbf{J}  0$），反之亦然。值得强调的是，这里的 $\rho$ 代表**总电荷密度**，而 $\mathbf{J}$ 代表**总电流密度**。在此形式下，该方程是[电动力学](@entry_id:158759)的基本公理之一，等式右侧严格为零，不存在源项或漏项 。

为了建立直观理解，考虑一个半径为 $R$、长度为 $L$ 的圆柱形半导体材料。假设其中存在一个沿轴向（$z$ 轴）的[稳态电流](@entry_id:276565)，其电流密度为 $\mathbf{J}(\mathbf{r}) = \alpha z^2 \hat{z}$，其中 $\alpha$ 为正常数。尽管电流是[稳态](@entry_id:139253)的，但它在空间上并非均匀。根据[连续性方程](@entry_id:195013)，我们可以预测材料内部[电荷密度](@entry_id:144672)的变化。圆柱体内部总电荷的变化率为 $\frac{dQ}{dt} = \iiint_V \frac{\partial \rho}{\partial t} dV = -\iiint_V (\nabla \cdot \mathbf{J}) dV$。该[电流密度的散度](@entry_id:266331)为 $\nabla \cdot \mathbf{J} = \frac{\partial J_z}{\partial z} = 2\alpha z$。因此，电荷变化率为：
$$\frac{dQ}{dt} = - \int_{0}^{L} \int_{0}^{2\pi} \int_{0}^{R} (2\alpha z) r \,dr \,d\phi \,dz = -\alpha \pi R^2 L^2$$
结果为负值，表明尽管有[稳态电流](@entry_id:276565)流过，但由于电流强度沿 $z$ 轴增加，电荷正从该圆柱体中净流出，导致总电荷随时间减少 。

### [位移电流](@entry_id:190231)的角色

在实际材料中，总电流密度 $\mathbf{J}$ 由两部分组成：由[自由电荷](@entry_id:264392)（如导体中的电子或半导体中的电子和空穴）运动产生的**[自由电流](@entry_id:191634)密度**（或称[传导电流](@entry_id:265343)密度）$\mathbf{J}_{\mathrm{free}}$，以及由电场随时间变化引起的**位移电流密度** $\frac{\partial \mathbf{D}}{\partial t}$。这一概念由 Maxwell 提出，是其方程组的核心组成部分。[安培-麦克斯韦定律](@entry_id:266368)写为：
$$\nabla \times \mathbf{H} = \mathbf{J}_{\mathrm{free}} + \frac{\partial \mathbf{D}}{\partial t}$$

位移电流项并非可有可无的数学构造，而是确保[电荷守恒](@entry_id:264158)定律与电磁[场方程](@entry_id:1124935)相容的必要组成部分。对上式两边取散度，并利用矢量恒等式 $\nabla \cdot (\nabla \times \mathbf{H}) = 0$，我们得到：
$$0 = \nabla \cdot \mathbf{J}_{\mathrm{free}} + \nabla \cdot \left(\frac{\partial \mathbf{D}}{\partial t}\right)$$

交换时间和空间导数的次序，并应用电场的[高斯定律](@entry_id:141493) $\nabla \cdot \mathbf{D} = \rho_{\mathrm{free}}$（其中 $\rho_{\mathrm{free}}$ 是[自由电荷](@entry_id:264392)密度），我们得到：
$$0 = \nabla \cdot \mathbf{J}_{\mathrm{free}} + \frac{\partial}{\partial t}(\nabla \cdot \mathbf{D}) = \nabla \cdot \mathbf{J}_{\mathrm{free}} + \frac{\partial \rho_{\mathrm{free}}}{\partial t}$$

这正是[自由电荷](@entry_id:264392)的连续性方程。这个推导清晰地表明，正是位移电流项 $\frac{\partial \mathbf{D}}{\partial t}$ 的存在，才使得变化的电场能够与[自由电荷](@entry_id:264392)的流动协调一致，共同满足电荷守恒的要求 。

位移电流的物理实在性可以通过一个思想实验来更好地理解。考虑一个由特殊介电材料制成的球壳，其内部通过某种假设的过程均匀地产生[自由电荷](@entry_id:264392)，使得[自由电荷](@entry_id:264392)密度随时间线性增长，即 $\rho_f(t) = kt$。假设该材料中没有[自由电荷](@entry_id:264392)的宏观传导（$\mathbf{J}_f = 0$）。根据高斯定律，球壳内部的[电位移矢量](@entry_id:197092) $\mathbf{D}$ 会随时间变化，因为 $\rho_f$ 在变化。这就产生了一个非零的位移电流密度 $\frac{\partial \mathbf{D}}{\partial t}$。根据[安培-麦克斯韦定律](@entry_id:266368)，这个随时间变化的电场（即[位移电流](@entry_id:190231)）将在其周围感生出磁场 ($\nabla \times \mathbf{H} \neq 0$)。因此，即使在没有真实电荷流动的区域，变化的电场也扮演着电流的角色，产生可观测的磁效应 。

在更实际的纳电子器件中，例如一个有漏电的纳米电容器，在交变电压 $V(t) = V_0 \cos(\omega t)$ 的驱动下，介质内部的总电流密度由[传导电流](@entry_id:265343) $\mathbf{J}_{\mathrm{free}} = \sigma\mathbf{E}$ 和位移电流 $\frac{\partial \mathbf{D}}{\partial t}$ 组成。在复数[相量表示法](@entry_id:196506)中，总电流密度[相量](@entry_id:270266)为 $\tilde{\mathbf{J}}_{\mathrm{total}} = (\sigma + i\omega\varepsilon) \tilde{\mathbf{E}}$。其中，与电场 $\mathbf{E}$同相的[传导电流](@entry_id:265343)部分 ($\sigma\mathbf{E}$) 导致不可逆的[焦耳热](@entry_id:150496)耗散。而与电场 $\mathbf{E}$ 相位相差 $90^\circ$ 的位移电流部分 ($i\omega\varepsilon\mathbf{E}$) 则对应于[电场能量](@entry_id:193072)的无耗散存储和释放（电容效应）。这两部分共同确保了电流在整个电路中的连续性，即使在电荷无法物理穿过的电容器间隙中也是如此 。

### 半导体中的载流子连续性

在[半导体器件物理](@entry_id:191639)中，我们更关心的是两种可移动的载流子——导带中的**电子**和价带中的**空穴**——各自的浓度分布和输运。因此，我们需要为电子和空穴分别建立[连续性方程](@entry_id:195013)。

让我们从粒子数守恒出发。对于电子，其浓度 $n(\mathbf{r}, t)$ 在某一体积内的变化率，等于通过边界的净流入率，加上体积内的净生成率。电子的净生成率通常表示为 $(G_n - R_n)$，其中 $G_n$ 是单位体积单位时间内的生成率， $R_n$ 是[复合率](@entry_id:203271)。电子的[粒子流](@entry_id:753205)密度（单位面积单位时间通过的粒子数）为 $\mathbf{j}_n$。于是，电子的粒子连续性方程为：
$$\frac{\partial n}{\partial t} + \nabla \cdot \mathbf{j}_n = G_n - R_n$$

在[器件建模](@entry_id:1123619)中，我们通常使用电荷电流密度 $\mathbf{J}_n$ 而非[粒子流](@entry_id:753205)密度 $\mathbf{j}_n$。由于电子带负电荷 $-q$（其中 $q$ 是元电荷大小），常规电流方向与电子运动方向相反。因此，它们的关系是 $\mathbf{J}_n = (-q) \mathbf{j}_n$。将 $\mathbf{j}_n = -\frac{1}{q}\mathbf{J}_n$ 代入粒子[连续性方程](@entry_id:195013)，得到：
$$\frac{\partial n}{\partial t} + \nabla \cdot \left(-\frac{1}{q}\mathbf{J}_n\right) = G_n - R_n$$

整理后得到**电子[连续性方程](@entry_id:195013)**的标准形式之一：
$$\frac{\partial n}{\partial t} = \frac{1}{q} \nabla \cdot \mathbf{J}_n + G_n - R_n$$

这里的符号需要仔细理解：$\nabla \cdot \mathbf{J}_n > 0$ 意味着电子电荷电流从某点流出发散，由于电子带负电，这对应于电子的汇集，从而使[电子浓度](@entry_id:190764) $n$ 增加。因此 $\nabla \cdot \mathbf{J}_n$ 项前面是正号。

对于带正电荷 $+q$ 的空穴，其粒子流密度与电荷电流密度方向相同，$\mathbf{J}_p = (+q) \mathbf{j}_p$。遵循同样的推导逻辑，我们得到**空穴[连续性方程](@entry_id:195013)**：
$$\frac{\partial p}{\partial t} = -\frac{1}{q} \nabla \cdot \mathbf{J}_p + G_p - R_p$$
此处，$\nabla \cdot \mathbf{J}_p > 0$ 意味着正电荷的流出发散，导致空穴浓度 $p$ 降低，因此该项前面是负号 。这两个方程是[半导体器件](@entry_id:192345)模拟的基石。

我们可以从这两个载流子方程出发，重新推导总电荷的[连续性方程](@entry_id:195013)。半导体中的总[电荷密度](@entry_id:144672) $\rho$ 由可移动的电子和空穴，以及固定的已电离的施主 ($N_D^+$) 和受主 ($N_A^-$) 构成：
$$\rho = q(p - n + N_D^+ - N_A^-)$$

假设掺杂原子的电离状态不随时间变化，其时间导数为零。对 $\rho$ 求时间导数：
$$\frac{\partial \rho}{\partial t} = q \left(\frac{\partial p}{\partial t} - \frac{\partial n}{\partial t}\right)$$

将电子和空穴的[连续性方程](@entry_id:195013)代入，并假设主要的生成-复合机制是带间过程（即电子和空穴成[对产生](@entry_id:154125)和湮灭，因此 $G_n=G_p$ 且 $R_n=R_p$），我们发现生成-复合项恰好抵消：
$$\frac{\partial \rho}{\partial t} = q \left[ \left(-\frac{1}{q} \nabla \cdot \mathbf{J}_p\right) - \left(\frac{1}{q} \nabla \cdot \mathbf{J}_n\right) \right] = -(\nabla \cdot \mathbf{J}_p + \nabla \cdot \mathbf{J}_n)$$

由于总的[传导电流](@entry_id:265343)密度为 $\mathbf{J}_{\mathrm{total}} = \mathbf{J}_n + \mathbf{J}_p$，上式可以写为：
$$\frac{\partial \rho}{\partial t} = - \nabla \cdot \mathbf{J}_{\mathrm{total}}$$
这与我们从[基本电荷](@entry_id:272261)守恒定律出发得到的形式完全一致，展示了载流子图像与宏观电磁理论的内在统一性 。

### 从宏观到微观：动力学视角

[连续性方程](@entry_id:195013)作为一个宏观的唯象方程，其背后有着深刻的[微观动力学](@entry_id:1127874)基础。它可以通过对描述载流子在相空间中演化的**[玻尔兹曼输运方程](@entry_id:140472) (Boltzmann Transport Equation, BTE)** 进行矩展开来导出。

BTE 描述了载流子分布函数 $f(\mathbf{r}, \mathbf{k}, t)$ 在相空间（位置 $\mathbf{r}$ 和[晶格动量](@entry_id:143609) $\mathbf{k}$）中的演化：
$$\frac{\partial f}{\partial t} + \mathbf{v}(\mathbf{k}) \cdot \nabla_{\mathbf{r}} f + \frac{\mathbf{F}}{\hbar} \cdot \nabla_{\mathbf{k}} f = \left(\frac{\partial f}{\partial t}\right)_{\mathrm{coll}}$$
其中 $\mathbf{v}(\mathbf{k})$ 是[群速度](@entry_id:147686)，$\mathbf{F}$ 是外力，碰撞项 $(\frac{\partial f}{\partial t})_{\mathrm{coll}}$ 描述了散射、生成和复合等过程。

宏观物理量是[分布函数](@entry_id:145626)在动量空间（[k空间](@entry_id:142033)）的矩（积分）。具体来说，载流子浓度 $n(\mathbf{r}, t)$ 是 $f$ 的零阶矩，而粒子流密度 $\mathbf{j}(\mathbf{r}, t)$ 是一阶矩：
$$n(\mathbf{r}, t) = \frac{1}{4\pi^3} \int f(\mathbf{r}, \mathbf{k}, t) d^3k$$
$$\mathbf{j}(\mathbf{r}, t) = \frac{1}{4\pi^3} \int \mathbf{v}(\mathbf{k}) f(\mathbf{r}, \mathbf{k}, t) d^3k$$

将整个BTE对 $\mathbf{k}$ 积分，我们可以逐项分析：
1.  时间导数项：$\int \frac{\partial f}{\partial t} d^3k$ 变为 $\frac{\partial n}{\partial t}$。
2.  空间梯度项：$\int \mathbf{v} \cdot \nabla_{\mathbf{r}} f d^3k$ 变为 $\nabla_{\mathbf{r}} \cdot \int \mathbf{v} f d^3k$，即 $\nabla \cdot \mathbf{j}$。
3.  力项：$\int \frac{\mathbf{F}}{\hbar} \cdot \nabla_{\mathbf{k}} f d^3k$ 通过[分部积分](@entry_id:136350)，并假设 $f$ 在[k空间](@entry_id:142033)边界处为零，该项积分为零。
4.  碰撞项：$\int (\frac{\partial f}{\partial t})_{\mathrm{coll}} d^3k$ 给出宏观的净生成率 $(G-R)$。

将这些结果组合起来，我们精确地重现了粒子连续性方程：$\frac{\partial n}{\partial t} + \nabla \cdot \mathbf{j} = G - R$。这表明宏观的连续性方程是微观粒子数守恒在BTE框架下的直接体现。任何出现在BTE中的微观源项，在积分后都会对宏观[连续性方程](@entry_id:195013)产生贡献。例如，若某种新奇的量子过程在BTE中引入一个微观源项 $S_{anom}(\mathbf{k}) = \alpha |\mathbf{k}|^2 \exp(-\beta |\mathbf{k}|^2)$，那么它对宏观净生成率的贡献将是该函数在整个k[空间的积](@entry_id:151742)分 $\Sigma_{anom} = \frac{1}{4\pi^3}\int S_{anom}(\mathbf{k}) d^3k$ 。

### 高等输运模型与[连续性方程](@entry_id:195013)

对于纳米尺度的前沿半导体材料和器件，经典的BTE和简单的漂移-[扩散模型](@entry_id:142185)可能不再适用。我们需要更先进的理论框架，但连续性方程作为基本守恒定律的核心地位依然不变。

#### [简并系统](@entry_id:203460)与准费米能级

在重掺杂或强注入条件下，半导体中的电子或空穴气体会进入**[简并态](@entry_id:274678)**，其统计行为由[费米-狄拉克分布](@entry_id:138909)描述，而非经典的[麦克斯韦-玻尔兹曼分布](@entry_id:144245)。在这种情况下，传统的漂移-扩散电流方程 $\mathbf{J}_n = qn\mu_n\mathbf{E} + qD_n\nabla n$ 及其依赖的爱因斯坦关系 $D/\mu = k_BT/q$ 不再精确。

真正的驱动力是**[电化学势](@entry_id:141179)**的梯度。对于非[平衡态](@entry_id:270364)下的电子，我们引入**电子准费米能级 (electron quasi-Fermi level)** $E_{Fn}(\mathbf{r})$ 来描述其局域的电化学势。通过使用适用于任意简并度的[广义爱因斯坦关系](@entry_id:144202)，并结合[费米-狄拉克统计](@entry_id:140706)，可以证明，看似复杂的漂移和扩散两项可以被优雅地统一。经过严格推导，电子电流密度可以被简洁地表示为：
$$\mathbf{J}_n = \mu_n n \nabla E_{Fn}$$

这个极为重要的结果表明，无论载流子简并与否，净电流都是由[准费米能级](@entry_id:1130433)的空间梯度驱动的。它将由电场驱动的“漂移”和由浓度不均匀引起的“扩散”统一在同一个物理根源之下。如果定义电子[准费米势](@entry_id:1130433) $\varphi_n(\mathbf{r})$ 为 $E_{Fn} = -q\varphi_n$，那么电流表达式变为 $\mathbf{J}_n = -q\mu_n n \nabla \varphi_n$。将这个更普适的电流表达式代入[连续性方程](@entry_id:195013)，就可以对工作在[简并区](@entry_id:143263)的先进器件（如二维过渡金属硫化物沟道晶体管）进行精确建模 。

#### 量子输运：[维格纳函数](@entry_id:153092)视角

当器件的特征尺寸小到与电子的[德布罗意波长](@entry_id:139033)相当时，量子相干效应变得不可忽略。此时，半经典的BTE失效，需要采用真正的[量子输运](@entry_id:138932)理论。**[维格纳函数](@entry_id:153092) (Wigner function)** $W(\mathbf{r}, \mathbf{k}, t)$ 提供了一种在相空间中描述量子系统的[准概率分布](@entry_id:203668)。其动力学由维格纳-[玻尔兹曼方程](@entry_id:138866)（或量子[刘维尔方程](@entry_id:156422)）描述，其中包含一个反映[量子非局域性](@entry_id:143788)的**非局域势能项**。

一个自然的问题是：这个复杂的量子项是否会改变[连续性方程](@entry_id:195013)的形式？答案是不会。通过与处理经典BTE完全相同的矩展开方法，对维格纳-玻尔兹曼方程在[k空间](@entry_id:142033)积分，我们依然可以得到形式完全一样的粒子[连续性方程](@entry_id:195013) $\frac{\partial n}{\partial t} + \nabla \cdot \mathbf{J} = S_{\mathrm{coll}}$。关键在于，对于厄米哈密顿量，那个复杂的非局域势能项（数学上由莫亚尔括号表示）在[k空间](@entry_id:142033)积分为零。它的作用是在相空间中重新分布粒子（即在给定位置 $\mathbf{r}$ 改变粒子的动量 $\mathbf{k}$），但它本身不产生或湮灭粒子，因此不会在宏观的粒子[连续性方程](@entry_id:195013)中引入源项 。

这个视角也澄清了经典模型的适用边界。从完整的量子输运描述回到经典的漂移-扩散模型需要两个关键的近似：
1.  **[半经典近似](@entry_id:147497)**：当电势在电子波长尺度上变化缓慢时，量子非局域效应可以忽略，维格纳-[玻尔兹曼方程](@entry_id:138866)简化为经典的BTE。
2.  **[流体动力学近似](@entry_id:145502)**：当散射足够强，使得载流子在两次碰撞之间能够达到局域准平衡时，BTE可以进一步简化为宏观的[漂移-扩散方程](@entry_id:136261)组。

#### 量子输运：[非平衡格林函数](@entry_id:144847)视角

在现代纳米电子学研究中，**[非平衡格林函数](@entry_id:144847) (Nonequilibrium Green's Function, NEGF)** 形式是描述[量子输运](@entry_id:138932)的金标准。它能够从第一性原理出发，系统地处理相干输运、散射和多体相互作用。在NEGF中，相互作用（如[电子-声子耦合](@entry_id:139197)）通过**自能 (self-energy)** $\Sigma$ 来描述。

一个核心且微妙的问题是：包含[非弹性散射](@entry_id:138624)（即载流子与环境交换能量，如发射或吸收声子）是否会破坏[电荷的局域守恒](@entry_id:202633)？理论上，[非弹性散射](@entry_id:138624)只是能量的转移，而不应创造或消灭电荷。NEGF形式论的优美之处在于，如果它被正确地构建，就能保证这一点。

这里的关键是**瓦德恒等式 (Ward identities)**，它是[量子场论](@entry_id:138177)中$U(1)$[规范不变性](@entry_id:137857)（即电荷守恒）在[格林函数](@entry_id:147802)和[自能](@entry_id:145608)层面上的数学体现。如果所采用的自能近似是所谓的“**[守恒近似](@entry_id:139611)**”（例如，从一个泛函 $\Phi[G]$ 导出的Baym-Kadanoff近似），那么它将自动满足瓦德恒等式。这从根本上保证了，即使在存在复杂的[非弹性散射](@entry_id:138624)过程时，计算出的电流和[电荷密度](@entry_id:144672)仍然严格遵守局域连续性方程 $\partial_t n + \nabla \cdot \mathbf{J} = 0$（在器件内部，远离源漏接触点）。

反之，一个常见的理论陷阱是采用不满足守恒条件的近似[自能](@entry_id:145608)，例如非自洽的[玻恩近似](@entry_id:138141)。这种简化虽然计算上方便，但因为它破坏了理论的内在对称性，可能导致计算结果中出现虚假的电荷源或漏，即 $\nabla \cdot \mathbf{J} \neq 0$，从而得出物理上错误的结论。这凸显了在先进的器件模拟中，保持理论框架的严谨性和对称性是何等重要 。