## 引言
[光吸收](@entry_id:136597)是物质与光相互作用最基本的过程之一，它不仅决定了材料的颜色和透明度，更是我们探测材料内部电子结构、设计新型光电器件的基石。从太阳能电池到[激光](@entry_id:194225)器，再到先进的[量子计算](@entry_id:142712)，对光吸收与[带间跃迁](@entry_id:138793)的深刻理解都至关重要。然而，从一个简单的[能带图](@entry_id:272375)到精确预测和解释实验中观察到的复杂吸收光谱，需要跨越理论上的巨大鸿沟。这其中涉及到[量子力学选择定则](@entry_id:151895)、[多体相互作用](@entry_id:751663)以及各种非理想效应，构成了凝聚态物理中一个丰富而深刻的领域。

本文旨在系统性地梳理[光吸收](@entry_id:136597)与[带间跃迁](@entry_id:138793)的核心理论，并展示其在现代科学研究与技术应用中的广阔图景。我们将带领读者从最基本的物理原理出发，逐步构建起一个完整且强大的理论框架。

在第一章“**原理与机制**”中，我们将奠定理论基础，从[费米黄金定则](@entry_id:146239)和守恒律出发，理解[垂直跃迁](@entry_id:275451)的由来。随后，我们将超越独立粒[子图](@entry_id:273342)像，引入至关重要的[激子](@entry_id:147299)效应，并最终介绍如何利用现代[第一性原理计算](@entry_id:198754)（如[GW-BSE](@entry_id:142900)方法）来[精确模拟](@entry_id:749142)真实材料的光学响应。

接下来，在第二章“**应用与[交叉](@entry_id:147634)学科联系**”中，我们将把理论应用于实践。通过分析一系列具体案例，读者将看到这些原理如何被用来表征材料（如[Tauc分析](@entry_id:193283)）、通过外部场调控光学性质（如[应变工程](@entry_id:139243)），以及如何解释低维材料（如[二维材料](@entry_id:142244)）和强关联系统中的新奇光学现象，并展现其与[材料科学](@entry_id:152226)、化学等领域的交叉融合。

最后，在第三章“**动手实践**”中，我们提供了一系列精心设计的练习，旨在引导读者亲手推导关键公式，加深对核心概念的理解，将理论知识转化为解决实际问题的能力。通过这一系列的学习，读者将能够全面掌握光吸收与[带间跃迁](@entry_id:138793)的物理内涵，并具备分析和理解相关前沿研究的能力。

## 原理与机制

本章旨在系统性地阐述固体中[光吸收](@entry_id:136597)与[带间跃迁](@entry_id:138793)的核心物理原理与机制。我们将从基本的[电子-光子相互作用](@entry_id:155851)出发，逐步建立起描述真实材料光学响应的理论框架。首先，我们将探讨支配跃迁过程的守恒律，并由此引出独立粒子图像下的吸收谱。随后，我们将引入电子-空穴相互作用，即[激子](@entry_id:147299)效应，这是理解[半导体光学性质](@entry_id:269418)的关键。最后，我们将介绍现代[多体微扰理论](@entry_id:168555)如何精确地预测和解释光学响应，并讨论如何从实验测量的光学数据中提取关键的材料参数。

### [光子](@entry_id:145192)-电子相互作用与守恒律

固体中的光吸收本质上是一个量子力学过程，其中一个电子吸收一个[光子](@entry_id:145192)，从一个较低的能级跃迁到一个较高的能级。在晶体中，这些能级属于特定的能带。对于[带间跃迁](@entry_id:138793)，电子从[价带](@entry_id:158227)（valence band, $v$）跃迁到导带（conduction band, $c$）。该过程的速率可以通过[费米黄金定则](@entry_id:146239)（Fermi's Golden Rule）来描述，它表明跃迁速率与描述[光与物质相互作用](@entry_id:142166)的微扰[哈密顿量](@entry_id:172864)的[矩阵元](@entry_id:186505)的平方成正比。

任何跃迁过程都必须遵守能量和动量守恒。

**[能量守恒](@entry_id:140514)** 要求电子的最终能量 $E_c(\mathbf{k}_f)$ 等于其初始能量 $E_v(\mathbf{k}_i)$ 加上吸收[光子](@entry_id:145192)的能量 $\hbar\omega$：
$$
E_c(\mathbf{k}_f) = E_v(\mathbf{k}_i) + \hbar\omega
$$
其中 $\mathbf{k}_i$ 和 $\mathbf{k}_f$ 分别是电子在跃迁前后的晶矢（crystal wavevector）。

**[晶体动量守恒](@entry_id:145588)** 则更为微妙。[光子](@entry_id:145192)本身携带一个动量 $\hbar\mathbf{q}$，其中 $\mathbf{q}$ 是光的[波矢](@entry_id:178620)。在晶体中，电子的动量是晶体动量，它是在一个[倒易晶格矢量](@entry_id:263351) $\mathbf{G}$ 的不定性下定义的。因此，包含[光子](@entry_id:145192)和[晶格](@entry_id:196752)在内的整个系统的动量守恒要求是：
$$
\hbar\mathbf{k}_f = \hbar\mathbf{k}_i + \hbar\mathbf{q} + \hbar\mathbf{G}
$$
在大多数情况下，我们关心的是不涉及[晶格](@entry_id:196752)吸收大块动量（即非U-过程，$\mathbf{G}=0$）的直接[光吸收](@entry_id:136597)过程。此时，电子晶矢的改变恰好等于[光子](@entry_id:145192)的[波矢](@entry_id:178620)：
$$
\Delta\mathbf{k} = \mathbf{k}_f - \mathbf{k}_i = \mathbf{q}
$$
然而，对于可见光或近紫外光范围内的[光子](@entry_id:145192)，其动量与晶体[布里渊区](@entry_id:142395)（Brillouin zone, BZ）的尺寸相比是极其微小的。我们可以通过一个简单的[数量级估算](@entry_id:164578)来证明这一点 [@problem_id:3008264]。考虑一个典型的[半导体](@entry_id:141536)，其晶格常数 $a \approx 5\,\mathrm{\AA}$。[布里渊区](@entry_id:142395)的尺寸由[倒易晶格矢量](@entry_id:263351)的大小决定，约为 $2\pi/a \approx 1.26\,\mathrm{\AA}^{-1}$。对于一个能量为 $\hbar\omega = 3\,\mathrm{eV}$ 的[光子](@entry_id:145192)，其在真空中的[波矢](@entry_id:178620)大小为 $|\mathbf{q}| = \omega/c = \hbar\omega/(\hbar c) \approx 3\,\mathrm{eV} / (1973\,\mathrm{eV}\cdot\mathrm{\AA}) \approx 0.0015\,\mathrm{\AA}^{-1}$。在[折射率](@entry_id:168910) $n$ 约为 $3.5$ 的介质中，[波矢](@entry_id:178620)大小变为 $|\mathbf{q}|_{med} = n|\mathbf{q}| \approx 0.0053\,\mathrm{\AA}^{-1}$。将[光子](@entry_id:145192)[波矢](@entry_id:178620)与[布里渊区](@entry_id:142395)的尺寸相比较，我们发现：
$$
\frac{|\mathbf{q}|_{med}}{2\pi/a} \approx \frac{0.0053\,\mathrm{\AA}^{-1}}{1.26\,\mathrm{\AA}^{-1}} \approx 4.2 \times 10^{-3}
$$
这个比值约为千分之几，说明[光子](@entry_id:145192)波矢与[布里渊区](@entry_id:142395)相比可以忽略不计。这意味着在跃迁过程中，电子的[晶体动量](@entry_id:136369)几乎不变，即 $\Delta\mathbf{k} = \mathbf{q} \approx \mathbf{0}$。这个近似被称为**[偶极近似](@entry_id:152759)**（dipole approximation），因为它等价于假设[电磁场](@entry_id:265881)的空间相位因子 $e^{i\mathbf{q}\cdot\mathbf{r}} \approx 1$，即[电磁场](@entry_id:265881)在单个[原胞](@entry_id:159354)尺度上是空间均匀的。

因此，对于光学频率的带间吸收，一个关键的选择定则是 $\mathbf{k}_f \approx \mathbf{k}_i$。在[能带结构图](@entry_id:276992)（$E$ vs. $\mathbf{k}$）上，这种跃迁表现为连接具有相同 $\mathbf{k}$ 值的[价带](@entry_id:158227)和[导带](@entry_id:159736)态的**[垂直跃迁](@entry_id:275451)**（vertical transition）。

这个结论对于[直接带隙和间接带隙](@entry_id:271502)[半导体](@entry_id:141536)都具有重要意义。在[直接带隙半导体](@entry_id:191146)中，[价带](@entry_id:158227)顶和[导带](@entry_id:159736)底位于[布里渊区](@entry_id:142395)的同一点（例如 $\Gamma$ 点），因此[垂直跃迁](@entry_id:275451)可以在[带隙](@entry_id:191975)能量附近有效地发生。然而，在[间接带隙](@entry_id:268921)[半导体](@entry_id:141536)中，价带顶和导带底位于 $\mathbf{k}$ 空间的不同位置。要实现最低能量的吸收，电子不仅需要能量，还需要一个显著的动量改变来跨越 $\mathbf{k}$ 空间的鸿沟。由于[光子](@entry_id:145192)无法提供如此大的动量，这个过程必须由[晶格振动](@entry_id:140970)的量子——**[声子](@entry_id:140728)**（phonon）——来辅助完成 [@problem_id:3008264]。[声子](@entry_id:140728)可以携带一个大小与[布里渊区](@entry_id:142395)相当的动量，但其能量通常远小于[带隙](@entry_id:191975)能量。

值得注意的是，当[光子能量](@entry_id:139314)非常高时，例如在软[X射线](@entry_id:187649)区域（数百电子伏特），其动量 $|\mathbf{q}|$ 将变得与[布里渊区](@entry_id:142395)尺寸相当，此时[偶极近似](@entry_id:152759)失效，非[垂直跃迁](@entry_id:275451)（$\Delta\mathbf{k} = \mathbf{q} \neq \mathbf{0}$）就变得重要了 [@problem_id:3008264]。

### [独立粒子模型](@entry_id:161055)中的[带间跃迁](@entry_id:138793)

在忽略电子与空穴之间相互作用的独立粒子图像中，[吸收系数](@entry_id:156541) $\alpha(\omega)$ 主要由两个因素决定：跃迁[矩阵元](@entry_id:186505)和[联合态密度](@entry_id:143002)。[吸收系数](@entry_id:156541)与跃迁速率成正比，可表示为：
$$
\alpha(\omega) \propto \frac{1}{\omega} \int_{\text{BZ}} |M_{cv}(\mathbf{k})|^2 \delta(E_c(\mathbf{k}) - E_v(\mathbf{k}) - \hbar\omega) \, d^3k
$$
其中 $M_{cv}(\mathbf{k})$ 是跃迁矩阵元，积分部分则与[联合态密度](@entry_id:143002)相关。

#### 跃迁矩阵元

跃迁[矩阵元](@entry_id:186505) $M_{cv}(\mathbf{k})$ 描述了在光场作用下，电子从初态 $|v,\mathbf{k}\rangle$ 跃迁到末态 $|c,\mathbf{k}\rangle$ 的量子力学几率幅。在[偶极近似](@entry_id:152759)下，它正比于[动量算符](@entry_id:151743)的矩阵元：
$$
M_{cv}(\mathbf{k}) \propto \langle \psi_{c\mathbf{k}} | \hat{\mathbf{p}} | \psi_{v\mathbf{k}} \rangle
$$
其中 $\psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r})$ 是[布洛赫波函数](@entry_id:144223)，$u_{n\mathbf{k}}(\mathbf{r})$ 是具有[晶格](@entry_id:196752)周期性的原胞周期部分。一个深刻的问题是：跃迁是由[布洛赫波函数](@entry_id:144223)的平面波部分 $e^{i\mathbf{k}\cdot\mathbf{r}}$ 还是[原胞](@entry_id:159354)周期部分 $u_{n\mathbf{k}}(\mathbf{r})$ 决定的？

通过对动量[矩阵元](@entry_id:186505)进行仔细分析 [@problem_id:3008269]，我们可以将其分解为两部分。动量算符 $\hat{\mathbf{p}} = -i\hbar\nabla$ 作用在初态上得到：
$$
\hat{\mathbf{p}} \psi_{v\mathbf{k}} = \hat{\mathbf{p}}(e^{i\mathbf{k}\cdot\mathbf{r}} u_{v\mathbf{k}}) = (\hbar\mathbf{k}) (e^{i\mathbf{k}\cdot\mathbf{r}} u_{v\mathbf{k}}) + e^{i\mathbf{k}\cdot\mathbf{r}} (\hat{\mathbf{p}} u_{v\mathbf{k}})
$$
代入[矩阵元](@entry_id:186505)表达式后，第一项的贡献为 $\hbar\mathbf{k} \langle \psi_{c\mathbf{k}} | \psi_{v\mathbf{k}} \rangle$。由于不同能带的[布洛赫函数](@entry_id:189422)在整个晶体上是正交的，即 $\langle \psi_{c\mathbf{k}} | \psi_{v\mathbf{k}} \rangle = 0$ (当 $c \neq v$)，因此这一项为零。这一正交性也直接导致了[原胞](@entry_id:159354)周期部分的正交性：$\int_{V_{cell}} u_{c\mathbf{k}}^*(\mathbf{r}) u_{v\mathbf{k}}(\mathbf{r}) d^3r = 0$。

因此，非零的跃迁矩阵元完全来自于第二项：
$$
M_{cv}(\mathbf{k}) \propto \langle \psi_{c\mathbf{k}} | e^{i\mathbf{k}\cdot\mathbf{r}} (\hat{\mathbf{p}} u_{v\mathbf{k}}) \rangle = \int u_{c\mathbf{k}}^*(\mathbf{r}) (\hat{\mathbf{p}} u_{v\mathbf{k}}(\mathbf{r})) d^3r
$$
这表明，**[带间跃迁](@entry_id:138793)是由光场与电子在原胞内部的相互作用驱动的，其性质由原胞[周期函数](@entry_id:139337) $u_{n\mathbf{k}}$ 的对称性和形状决定，而非由平面波包络 $e^{i\mathbf{k}\cdot\mathbf{r}}$ 决定**。这解释了为什么跃迁选择定则（例如，[宇称选择定则](@entry_id:203598)）与能带在特定 $\mathbf{k}$ 点的对称性密切相关。如果初态和末态的对称性使得该[矩阵元](@entry_id:186505)在带边（例如 $\mathbf{k}=0$）处为零，那么该跃迁就被称为**[禁戒跃迁](@entry_id:153557)**（forbidden transition），即使[态密度](@entry_id:147894)[允许跃迁](@entry_id:160018)发生 [@problem_id:3008207]。

#### [联合态密度](@entry_id:143002) (JDOS)

[联合态密度](@entry_id:143002)（Joint Density of States, JDOS）$J(\omega)$ 定义为单位能量间隔内，能量差恰好为 $\hbar\omega$ 的电子-空穴对的数量。它直接反映了满足[能量守恒](@entry_id:140514)条件的跃迁通道数目。其形式化定义为 [@problem_id:3008207]：
$$
J(\omega) = \frac{2}{(2\pi)^3} \int_{\text{BZ}} \delta(E_c(\mathbf{k}) - E_v(\mathbf{k}) - \hbar\omega) \, d^3k
$$
因子 $2$ 考虑了自旋简并。如果跃迁[矩阵元](@entry_id:186505) $M_{cv}(\mathbf{k})$ 在带边附近变化缓慢，那么[吸收系数](@entry_id:156541) $\alpha(\omega)$ 的谱形主要由 $J(\omega)$ 决定。

对于一个典型的三维（3D）[直接带隙半导体](@entry_id:191146)，其带边附近的能带可以近似为抛物线形：$E_c(\mathbf{k}) \approx E_g + \frac{\hbar^2 k^2}{2m_c}$ 和 $E_v(\mathbf{k}) \approx -\frac{\hbar^2 k^2}{2m_v}$。能量差为 $E_c - E_v = E_g + \frac{\hbar^2 k^2}{2m_r}$，其中 $m_r = (\frac{1}{m_c} + \frac{1}{m_v})^{-1}$ 是约化[有效质量](@entry_id:142879)。计算可得，三维体系的JDOS为：
$$
J_{3D}(\omega) \propto \sqrt{\hbar\omega - E_g}
$$
对于 $\hbar\omega > E_g$，否则为零。这导致吸收边呈现平方根形式的上升。

而在二维（2D）体系（如量子阱）中，采用类似的抛物线能带模型，计算出的JDOS是一个[阶跃函数](@entry_id:159192) [@problem_id:3008207]：
$$
J_{2D}(\omega) \propto \Theta(\hbar\omega - E_g)
$$
其中 $\Theta$ 是亥维赛德阶跃函数。这意味着在2D材料中，吸收在[带隙](@entry_id:191975)能量处突然开启，并（在理想模型下）保持为一个常数。

在能带结构的更高能量处，当 $E_c(\mathbf{k}) - E_v(\mathbf{k})$ 的[色散关系](@entry_id:140395)出现[极值](@entry_id:145933)点时，即 $\nabla_{\mathbf{k}}(E_c(\mathbf{k}) - E_v(\mathbf{k})) = \mathbf{0}$，JDOS会出现[奇异点](@entry_id:199525)，称为**[范霍夫奇点](@entry_id:144019)**（van Hove singularities）。这些[奇点](@entry_id:137764)表现为吸收谱中的峰或[尖点](@entry_id:636792)，为研究整个[布里渊区](@entry_id:142395)的[电子结构](@entry_id:145158)提供了重要的实验指纹 [@problem_id:3008207]。

### 吸收谱分析

基于上述理论，我们可以通过分析实验测得的吸收谱 $\alpha(\omega)$ 的形状来推断[半导体](@entry_id:141536)的基本属性，如[带隙](@entry_id:191975)类型（直接或间接）和大小。这种分析方法的核心是构造所谓的**陶克图**（Tauc plot）[@problem_id:3008208]。

1.  **直接[允许跃迁](@entry_id:160018)**：如前所述，对于3D系统，$\alpha(\omega) \propto \frac{1}{\omega} J_{3D}(\omega) \propto \frac{\sqrt{\hbar\omega-E_g}}{\hbar\omega}$。在带边附近 $\hbar\omega \approx E_g$，$\alpha(\omega)$ 近似正比于 $\sqrt{\hbar\omega-E_g}$。因此，$(\alpha\hbar\omega)^2$ 与 $\hbar\omega$ 呈线性关系。通过绘制 $(\alpha\hbar\omega)^2$ vs. $\hbar\omega$ 的图像，我们可以得到一条直线，其与能量轴的交点即为光学[带隙](@entry_id:191975) $E_g$。

2.  **直接[禁戒跃迁](@entry_id:153557)**：如果跃迁在带边（$\mathbf{k}=0$）因对称性禁戒，但随着 $k$ 的增加而变为允许，跃迁[矩阵元](@entry_id:186505) $|M_{cv}|^2 \propto k^2 \propto (\hbar\omega-E_g)$。此时，$\alpha(\omega)\hbar\omega \propto (\hbar\omega-E_g) \cdot \sqrt{\hbar\omega-E_g} = (\hbar\omega-E_g)^{3/2}$。因此，绘制 $(\alpha\hbar\omega)^{2/3}$ vs. $\hbar\omega$ 会得到一条直线，其截距同样为 $E_g$。

3.  **间接[允许跃迁](@entry_id:160018)**：此过程涉及[声子](@entry_id:140728)的吸收或发射，是一个二阶过程。[能量守恒](@entry_id:140514)变为 $\hbar\omega \pm \hbar\Omega = E_g + E_{c}(\mathbf{k}_c) - E_{v}(\mathbf{k}_v)$，其中 $\hbar\Omega$ 是[声子](@entry_id:140728)能量。对所有可能的初末态求和后，发现 $\alpha(\omega)\hbar\omega \propto (\hbar\omega - E_g \pm \hbar\Omega)^2$。因此，绘制 $(\alpha\hbar\omega)^{1/2}$ vs. $\hbar\omega$ 会得到两个线性部分。一个部分的起始点（截距）在 $E_g + \hbar\Omega$（[声子](@entry_id:140728)发射），另一个在 $E_g - \hbar\Omega$（[声子](@entry_id:140728)吸收）。[声子](@entry_id:140728)吸收过程需要[晶格](@entry_id:196752)中已存在热激发[声子](@entry_id:140728)，因此其强度随温度降低而迅速减弱，在低温下几乎不可见。

### 真实晶体中的非理想效应

[理想晶体](@entry_id:138314)模型为我们提供了基础，但真实材料的光学性质会受到各种非理想因素的影响。

#### 能带填充与伯斯坦-莫斯位移

在重掺杂的n型[半导体](@entry_id:141536)中，[导带](@entry_id:159736)底部被电子占据，一直填充到[费米能级](@entry_id:143215) $E_F$。根据[泡利不相容原理](@entry_id:141850)，[光学跃迁](@entry_id:160047)的末态必须是未被占据的态。在 $T=0$ 时，这意味着电子只能跃迁到能量高于 $E_F$ 的态。因此，最低能量的跃迁不再是发生在[带隙](@entry_id:191975) $E_g$ 处，而是从[价带](@entry_id:158227)的某个态跃迁到导带的费米面上。这导致测得的光学[带隙](@entry_id:191975)蓝移，这种现象被称为**伯斯坦-莫斯位移**（Burstein-Moss shift）[@problem_id:3008246]。

该位移的大小 $\Delta E$ 可以定量计算。在 $T=0$ 时，电子填充了导带中所有[波矢](@entry_id:178620) $|\mathbf{k}| \le k_F$ 的态，其中[费米波矢](@entry_id:140713) $k_F$ 由[电子浓度](@entry_id:190764) $n$ 决定：$k_F = (3\pi^2 n / g_v)^{1/3}$（$g_v$ 是[能谷简并](@entry_id:137132)度）。最低能量的[垂直跃迁](@entry_id:275451)发生在 $k=k_F$ 处，其能量为：
$$
E^*_{g} = E_c(k_F) - E_v(k_F) = E_g + \frac{\hbar^2 k_F^2}{2m_c} + \frac{\hbar^2 k_F^2}{2m_v} = E_g + \frac{\hbar^2 k_F^2}{2m_r}
$$
因此，伯斯坦-莫斯位移为：
$$
\Delta E = E^*_{g} - E_g = \frac{\hbar^{2}}{2m_r} \left( \frac{3\pi^{2} n}{g_{v}} \right)^{2/3}
$$
这个效应在设计[透明导电氧化物](@entry_id:147219)和[半导体激光器](@entry_id:269261)等光电子器件中至关重要。

#### 无序与乌尔巴赫边

在任何真实晶体中，都存在偏离完美周期性的情况，这包括由晶格振动引起的热无序（动态）和由缺陷、杂质、合金成分起伏等引起的结构无序（静态）。这些无序效应会在[带隙](@entry_id:191975)中引入所谓的“带尾态”，并导致吸收边不再是理想模型预测的陡峭形状，而是在低于[带隙](@entry_id:191975)的能量处出现一个指数形式的吸收“尾巴”，称为**乌尔巴赫边**（Urbach tail）[@problem_id:3008248]。

经验上，乌尔巴赫边遵循以下指数定律：
$$
\alpha(\omega) = \alpha_0 \exp\left(\frac{\hbar\omega - E_0}{E_U}\right)
$$
其中 $E_U$ 是**[乌尔巴赫能量](@entry_id:267177)**，它表征了吸收边的陡峭程度（$E_U$ 越大，边越平缓）。$E_0$ 是一个汇聚能量点，通常接近激子吸收峰的位置。实验上，通过绘制 $\ln \alpha$ vs. $\hbar\omega$，可以得到一条直线，其斜率的倒数即为 $E_U$。

[乌尔巴赫能量](@entry_id:267177) $E_U$ 同时包含了静态和[动态无序](@entry_id:187807)的贡献。其温度依赖性主要来源于[声子](@entry_id:140728)的热占据，遵循[玻色-爱因斯坦统计](@entry_id:139965)。在高温极限下，$E_U$ 近似与温度 $T$ 成正比。[静态无序](@entry_id:144184)则贡献一个与温度无关的项。因此，增加晶体的结构无序度（例如，在非晶[半导体](@entry_id:141536)中）会显著增大 $E_U$ 的值，使[吸收边](@entry_id:274704)变得更加弥散。

### [多体效应](@entry_id:173569)：[激子](@entry_id:147299)

到目前为止，我们都忽略了光生电子和它在[价带](@entry_id:158227)留下的空穴之间的库仑相互作用。在[半导体](@entry_id:141536)和绝缘体中，这种相互作用至关重要，它能将电子和空穴束缚在一起，形成一个类似氢原子的[准粒子](@entry_id:136584)，称为**[激子](@entry_id:147299)**（exciton）。激子效应深刻地改变了吸收谱的形状。

#### [瓦尼尔-莫特激子](@entry_id:140412)与埃利奥特公式

在大多数[半导体](@entry_id:141536)中，电子-空穴相互作用被[晶格](@entry_id:196752)的介电效应屏蔽，使得电子和空穴的束缚半径远大于晶格常数，这种[激子](@entry_id:147299)称为**[瓦尼尔-莫特激子](@entry_id:140412)**。其行为可以用一个有效质量和[屏蔽库仑势](@entry_id:151053)的氢原子模型来描述。

这个模型预测了两种主要的光学特征，由**埃利奥特公式**（Elliott formula）概括 [@problem_id:3008249]：

1.  **离散的[激子](@entry_id:147299)吸收峰**：在连续带间[吸收边](@entry_id:274704) $E_g$ 以下，形成一个分立的束缚态能级序列，其能量为：
    $$
    E_n = E_g - \frac{R_y^*}{n^2}, \quad n=1, 2, 3, \ldots
    $$
    其中 $R_y^*$ 是有效里德堡能量，即[激子](@entry_id:147299)的结合能。只有 $s$ [波函数](@entry_id:147440)（角动量 $l=0$）在电子-空穴重合处 ($\mathbf{r}=0$) 的几率幅不为零，因此只有 $s$ 态激子是[光学活性](@entry_id:139326)的。其吸收强度（[振子强度](@entry_id:147221)）随着主量子数 $n$ 的增加而减小，正比于 $|\phi_n(0)|^2 \propto 1/n^3$。这导致在吸收谱上出现一系列分立的、强度递减的吸收线。

2.  **增强的连续谱吸收**：在 $\hbar\omega > E_g$ 的能量区域，[电子和空穴](@entry_id:274534)是自由的，但它们仍然感受到彼此的吸引。这种持续的库仑相互作用增强了它们在空间中相遇的概率，从而增强了吸收。这种增强效应由**索末菲因子**（Sommerfeld factor）描述。它使得吸收在[带隙](@entry_id:191975)能量 $E_g$ 处不再是零（如[独立粒子模型](@entry_id:161055)预测的 $\sqrt{\hbar\omega - E_g}$），而是一个有限的常数，并平滑地过渡到高能下 $\sqrt{\hbar\omega - E_g}$ 的行为。

总的来说，库仑相互作用并未创造新的跃迁，而是将原本[分布](@entry_id:182848)在连续谱中的**振子强度**（oscillator strength）进行了重新分配。一部分强度被“拉”到[带隙](@entry_id:191975)下方，集中在分立的[激子](@entry_id:147299)峰上，另一部分则用于增强带边附近的连续谱吸收。根据**[托马斯-赖歇-库恩求和规则](@entry_id:169841)**（Thomas-Reiche-Kuhn sum rule），总的[振子强度](@entry_id:147221)是守恒的 [@problem_id:3008249]。

#### [第一性原理计算](@entry_id:198754)的层次

现代[计算物理学](@entry_id:146048)为我们提供了从第一性原理（即只基于原子种类和位置）计算光学谱的强大工具。这些方法在处理[多体效应](@entry_id:173569)方面形成了明确的层次结构 [@problem_id:3008210]：

1.  **随机相近似 (RPA)**：这是最简单的多体方法。当基于[密度泛函理论](@entry_id:139027)（DFT）的科恩-沈（Kohn-Sham）[轨道](@entry_id:137151)进行计算时，它本质上是一个[独立粒子模型](@entry_id:161055)。由于DFT普遍低估[半导体](@entry_id:141536)的[带隙](@entry_id:191975)（所谓的“[带隙问题](@entry_id:143831)”），RPA预测的[吸收边](@entry_id:274704)能量（$E_g^{\mathrm{KS}}$）通常远低于实验值，并且完全忽略了激子效应。

2.  **[GW近似](@entry_id:140388)**：GW方法通过计算电子的自能 $\Sigma = iGW$ 来修正DFT的能级，从而得到更准确的**[准粒子](@entry_id:136584)**（quasiparticle）能量。这通常能极大地改善[带隙](@entry_id:191975)的预测值，使其与实验测量的[准粒子](@entry_id:136584)[带隙](@entry_id:191975) $E_g^{\mathrm{GW}}$ 非常吻合。然而，如果仅使用GW修正的能级来计算吸收谱（所谓的独立[准粒子](@entry_id:136584)近似），虽然[吸收边](@entry_id:274704)的位置正确了，但仍然没有包含电子-空穴相互作用，因此无法描述[激子](@entry_id:147299)峰。

3.  **贝特-萨尔佩特方程 (BSE)**：BSE方法是计算光学谱的黄金标准。它在GW[准粒子](@entry_id:136584)图像的基础上，通过求解一个描述[电子-空穴对](@entry_id:142506)的二体方程，显式地包含了电子-空穴相互作用。

#### 贝特-萨尔佩特方程 (BSE)

BSE方法将[激子](@entry_id:147299)看作是所有可能独立[电子-空穴对](@entry_id:142506) $|vc\mathbf{k}\rangle$ 的[相干叠加](@entry_id:170209)。在常用的静态近似和塔姆-丹可夫近似（Tamm-Dancoff approximation, TDA）下，BSE可以化为一个有效的[哈密顿量本征值](@entry_id:203607)问题 [@problem_id:3008219]：
$$
\sum_{v'c'\mathbf{k}'} H^{\text{exc}}_{vc\mathbf{k},v'c'\mathbf{k}'} A^{S}_{v'c'\mathbf{k}'} = \Omega_{S} A^{S}_{vc\mathbf{k}}
$$
其中，[激子](@entry_id:147299)[哈密顿量](@entry_id:172864) $H^{\text{exc}}$ 的对角元是独立[准粒子](@entry_id:136584)跃迁能量 $(E_{c\mathbf{k}}^{\mathrm{GW}} - E_{v\mathbf{k}}^{\mathrm{GW}})$，而非对角元是电子-空穴[相互作用核](@entry_id:193790) $K^{\mathrm{eh}}$。该核包含两个关键部分：
-   一个有吸[引力](@entry_id:175476)的**直接项** $K^d$，描述了[电子和空穴](@entry_id:274534)之间被屏蔽的库仑吸引。
-   一个有排斥力的**交换项** $K^x$，源于[泡利不相容原理](@entry_id:141850)，是一个短程的、未被屏蔽的相互作用。

求解该方程可以得到[激子](@entry_id:147299)的本征能量 $\Omega_S$ 和对应的本征矢量 $A^S$。$A^S_{vc\mathbf{k}}$ 代表了独立[电子-空穴对](@entry_id:142506) $|vc\mathbf{k}\rangle$ 在激子态 $|S\rangle$ 中的振幅。

最终的吸收谱由所有[激子](@entry_id:147299)态的振子强度决定。第 $S$ 个激子态的跃迁几率幅是所有组分跃迁的相干求和：
$$
t_S \propto \sum_{vc\mathbf{k}} A^{S}_{vc\mathbf{k}} \langle c\mathbf{k} | \hat{\mathbf{p}} | v\mathbf{k} \rangle
$$
吸收谱，即[介电函数](@entry_id:136859)虚部 $\varepsilon_2(\omega)$，表现为一系列位于[激子](@entry_id:147299)能量 $\Omega_S$ 处的 $\delta$ 峰，其权重为 $|t_S|^2$：
$$
\varepsilon_2(\omega) \propto \sum_S |t_S|^2 \delta(\hbar\omega - \Omega_S)
$$
通过BSE方法，不仅可以准确预测出束缚[激子](@entry_id:147299)峰的位置和强度，还能正确描述连续谱因电子-空穴相互作用而发生的重塑，从而能够与高精度的实验[光谱](@entry_id:185632)进行直接比较。

### 介电函数与[克拉默斯-克勒尼希关系](@entry_id:140966)

我们已经看到，[吸收系数](@entry_id:156541) $\alpha(\omega)$ 与宏观介电函数 $\varepsilon_M(\omega) = \varepsilon_1(\omega) + i\varepsilon_2(\omega)$ 的虚部 $\varepsilon_2(\omega)$ 密切相关，关系式为 $\alpha(\omega) = \frac{\omega}{nc}\varepsilon_2(\omega)$，其中 $n$ 是[折射率](@entry_id:168910)。$\varepsilon(\omega)$ 完整地描述了材料对[电磁波](@entry_id:269629)的[线性响应](@entry_id:146180)。

在实验中，直接测量 $\alpha(\omega)$ 或 $\varepsilon_2(\omega)$ 通常很困难。更常见的技术是测量材料的反射率 $R(\omega)$。然而，$R(\omega)$ 同时依赖于 $\varepsilon_1(\omega)$ 和 $\varepsilon_2(\omega)$，并且在测量中丢失了相位信息。一个关键的问题是：我们能否仅从反射率谱 $R(\omega)$ 中重构出完整的[复介电函数](@entry_id:143480)？

答案是肯定的，这要归功于**[克拉默斯-克勒尼希关系](@entry_id:140966)**（Kramers-Kronig relations）。这个关系是物理[响应函数](@entry_id:142629)（如 $\varepsilon(\omega)$）必须满足的因果律的直接数学推论。它将响应函数的实部和虚部通过一个[积分变换](@entry_id:186209)联系起来。

对于从实验数据重构[介电函数](@entry_id:136859)而言，最实用的方法是应用于复[反射系数](@entry_id:194350) $r(\omega) = \sqrt{R(\omega)} e^{i\theta(\omega)}$ [@problem_id:3008275]。由于在测量中只得到振幅 $\sqrt{R(\omega)}$，相位 $\theta(\omega)$ 是未知的。通过对 $\ln r(\omega) = \frac{1}{2}\ln R(\omega) + i\theta(\omega)$ 应用[克拉默斯-克勒尼希关系](@entry_id:140966)，我们可以从 $\ln R(\omega)$ 计算出相位 $\theta(\omega)$：
$$
\theta(\omega) = -\frac{\omega}{\pi} \mathcal{P} \int_0^\infty \frac{\ln R(\omega')}{\omega'^2 - \omega^2} d\omega'
$$
其中 $\mathcal{P}$ 表示[柯西主值](@entry_id:192761)。这个积分需要知道从零到无穷大频率范围内的 $R(\omega)$。由于实验测量总是在一个有限的频率窗口 $[\omega_{\min}, \omega_{\max}]$ 内进行，因此必须对测量范围之外的区域进行物理上合理的**外推**（extrapolation）。例如，对于金属，低频区可以用哈根-鲁本斯关系（Hagen-Rubens relation, $R(\omega) \approx 1-A\sqrt{\omega}$）外推，高频区可以用[自由电子气模型](@entry_id:155154)（$R(\omega) \propto \omega^{-4}$）外推。

一旦通过这种方式获得了完整的复[反射系数](@entry_id:194350) $r(\omega)$，就可以通过菲涅尔方程的反演来计算[复折射率](@entry_id:268061) $N(\omega)$，进而得到[复介电函数](@entry_id:143480) $\varepsilon(\omega) = N^2(\omega)$。这一强大的分析工具构成了连接光学理论预测与实验测量的关键桥梁。