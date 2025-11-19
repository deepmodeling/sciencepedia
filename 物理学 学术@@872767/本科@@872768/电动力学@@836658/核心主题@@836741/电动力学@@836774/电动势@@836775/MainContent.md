## 引言
从点亮城市的巨大发电机到为手机充电的微小变压器，现代文明的运转离不开电流的驱动。而这一切的起点，是一个深刻而强大的物理概念——电动势（Electromotive Force, EMF）。尽管其名称中带有“力”字，但电动势并非传统意义上的力，其本质也比简单的电压或电势差更为微妙和深刻。理解电动势的真正内涵，区分其与相关概念的异同，是掌握电磁学乃至整个物理学的关键一步。

本文旨在系统性地揭开电动势的神秘面纱。在第一章**“原理与机制”**中，我们将深入法拉第[电磁感应](@entry_id:181154)定律，详细剖析感生电动势与[动生电动势](@entry_id:264357)的物理起源。随后的第二章**“应用与跨学科联系”**将展示这些原理如何转化为从工程技术到前沿物理的广泛应用，揭示其无与伦比的普适性。最后，在**“动手实践”**部分，我们将通过具体问题引导读者将理论应用于实践，巩固所学知识。现在，让我们从其最核心的物理定律开始，踏上探索电动势的旅程。

## 原理与机制

在介绍性章节之后，我们现在深入探究电动势（electromotive force, EMF）的核心原理和产生机制。电动势是电磁学中的一个基石概念，它描述了非静电力对[电荷](@entry_id:275494)做功以驱动电流的能力。虽然“力”这个词可能会引起误解，但电动势并非传统意义上的力，它的单位是伏特（V），与[电势](@entry_id:267554)相同，代表每单位[电荷](@entry_id:275494)所做的功。

理解电动势的关键在于认识到它源于**法拉第[电磁感应](@entry_id:181154)定律（Faraday's law of induction）**。该定律是电磁学的支柱之一，它以简洁而深刻的数学形式，将变化的[磁场](@entry_id:153296)与产生的[电场](@entry_id:194326)效应联系起来。本章将系统地剖析这一定律，揭示其背后两种截然不同但又内在统一的物理机制：由随时间变化的[磁场](@entry_id:153296)产生的**感生电动势（transformer EMF）**和由导体在[磁场](@entry_id:153296)中运动产生的**[动生电动势](@entry_id:264357)（motional EMF）**。

### [法拉第定律](@entry_id:149836)：统一的观点

法拉第电磁感应定律指出，任何闭合回路中感应出的电动势 $\mathcal{E}$，等于穿过该回路所限定的任意[曲面](@entry_id:267450)的磁通量 $\Phi_B$ 的变化率的负值。其积分形式为：

$$
\mathcal{E} = - \frac{d\Phi_B}{dt}
$$

其中，磁通量 $\Phi_B$ 的定义为[磁场](@entry_id:153296) $\mathbf{B}$ 穿过一个开放[曲面](@entry_id:267450) $S$ 的积分：

$$
\Phi_B = \int_S \mathbf{B} \cdot d\mathbf{A}
$$

式中的负号体现了**[楞次定律](@entry_id:139402)（Lenz's law）**，即感应电流的方向总是使得它自身产生的[磁场](@entry_id:153296)反抗引起感应电流的[磁通量](@entry_id:268943)变化。

这个看似简单的方程蕴含了丰富的物理内容。[磁通量](@entry_id:268943)的变化 $\frac{d\Phi_B}{dt}$ 可以通过两种方式实现：

1.  回路本身静止，但穿过它的[磁场](@entry_id:153296) $\mathbf{B}$ 随时间 $t$ 变化。
2.  [磁场](@entry_id:153296) $\mathbf{B}$ 本身是恒定的，但回路在[磁场](@entry_id:153296)中运动或形变，导致其所围面积或方位发生变化。

在最一般的情况下，这两种情况可以同时发生。通用[磁通量](@entry_id:268943)法则（universal flux rule）完美地统一了这两种机制。考虑一个随时间 $t$ 运动和形变的回路，穿过它的[磁通量](@entry_id:268943)变化率可以展开为：

$$
\frac{d\Phi_B}{dt} = \int_S \frac{\partial \mathbf{B}}{\partial t} \cdot d\mathbf{A} + \oint_{\partial S} (\mathbf{B} \times \mathbf{v}) \cdot d\mathbf{l}
$$

其中 $\mathbf{v}$ 是回路元 $d\mathbf{l}$ 的运动速度。结合法拉第定律，我们可以将总电动势分解为两个部分，分别对应上述两种机制。

### 感生电动势：时变[磁场](@entry_id:153296)的作用

当导体回路静止（$\mathbf{v} = 0$）而[磁场](@entry_id:153296)随时间变化时，法拉第定律简化为：

$$
\mathcal{E} = \oint \mathbf{E} \cdot d\mathbf{l} = - \int_S \frac{\partial \mathbf{B}}{\partial t} \cdot d\mathbf{A}
$$

这表明，一个时变的[磁场](@entry_id:153296)会在空间中激发一个[电场](@entry_id:194326) $\mathbf{E}$。这个[电场](@entry_id:194326)的[环路积分](@entry_id:164828)（即其环流）不为零，这意味着它是一个**[非保守场](@entry_id:265048)（non-conservative field）**。与由静[电荷](@entry_id:275494)产生的保守（无旋）[静电场](@entry_id:268546)不同，这种[感应电场](@entry_id:267314)的电场线是闭合的涡旋线。正是这个[感应电场](@entry_id:267314)驱动导体中的自由电荷，形成感应电流。这种由时变[磁场](@entry_id:153296)产生的电动势，我们称之为**感生电动势**或**变压器电动势（transformer EMF）**。

一个典型的例子是，将一个固定的导电线圈置于一个随时间[振荡](@entry_id:267781)的均匀[磁场](@entry_id:153296)中 [@problem_id:1578335]。假设一个半径为 $R$、匝数为 $N$ 的圆形线圈位于 $xy$ 平面，而[磁场](@entry_id:153296)为 $\mathbf{B}(t) = B_0 \cos(\omega t) \hat{k}$。穿过单匝线圈的[磁通量](@entry_id:268943)为 $\Phi_1(t) = B(t) A = \pi R^2 B_0 \cos(\omega t)$。对于 $N$ 匝线圈，总[磁通](@entry_id:191239)链 $\Lambda(t) = N\Phi_1(t)$。根据[法拉第定律](@entry_id:149836)，[感应电动势](@entry_id:264372)为：

$$
\mathcal{E}(t) = -\frac{d\Lambda}{dt} = - \frac{d}{dt} \left( N \pi R^2 B_0 \cos(\omega t) \right) = N \pi R^2 B_0 \omega \sin(\omega t)
$$

这个交变的电动势会在电阻为 $r$ 的线圈中驱动一个电流 $I(t) = \mathcal{E}(t) / r$，从而产生热耗散。其平均功率可以通过对[瞬时功率](@entry_id:174754) $P(t) = \mathcal{E}(t)^2 / r$ 在一个周期[内积](@entry_id:158127)分求平均得到，结果为 $\langle P \rangle = \frac{N^2 \pi^2 R^4 B_0^2 \omega^2}{2r}$。

[感应电场](@entry_id:267314)的一个显著特征是它的非定域性。[感应电场](@entry_id:267314) $\mathbf{E}$ 的存在与否取决于穿过回路的[磁通量](@entry_id:268943) *变化率*，而并非该点局域的[磁场](@entry_id:153296)值。即使在[磁场](@entry_id:153296)为零的区域，只要该区域包围着一个磁通量正在变化的区域，也可能存在非零的[感应电场](@entry_id:267314) [@problem_id:1795460]。

考虑一个半径为 $R_0$ 的长圆柱体内，[磁场](@entry_id:153296) $\mathbf{B}$ 平行于轴线，并随时间 $t$ 和径向距离 $r$ 变化，即 $B(r,t) = B_0 \frac{r}{R_0} \frac{t}{\tau}$ ($r \le R_0$)，而在圆柱体外 ($r > R_0$) [磁场](@entry_id:153296)为零。我们可以在圆柱体外取一个半径为 $r_1 > R_0$ 的同轴圆形路径来计算[感应电场](@entry_id:267314)。通过该路径的[磁通量](@entry_id:268943)仅由 $r \le R_0$ 区域内的[磁场](@entry_id:153296)贡献，计算可得 $\Phi_B(t) = \frac{2\pi}{3} B_0 R_0^2 \frac{t}{\tau}$。其随时间的变化率是恒定的：$\frac{d\Phi_B}{dt} = \frac{2\pi B_0 R_0^2}{3\tau}$。根据法拉第定律的积分形式 $\oint \mathbf{E} \cdot d\mathbf{l} = E(2\pi r_1) = -\frac{d\Phi_B}{dt}$，我们可以解出在圆柱体外 $r_1$ 处的[感应电场](@entry_id:267314)大小为：

$$
E = \frac{1}{2\pi r_1} \left| -\frac{d\Phi_B}{dt} \right| = \frac{B_0 R_0^2}{3\tau r_1}
$$

这个结果有力地证明了，即使在 $\mathbf{B}=0$ 的空间区域，一个变化的[磁通量](@entry_id:268943)也能够产生一个实实在在的[电场](@entry_id:194326)。

### [动生电动势](@entry_id:264357)：运动导体的洛伦兹力效应

当导体在[恒定磁场](@entry_id:195560)中运动时，也会产生电动势。这种情况下 $\frac{\partial \mathbf{B}}{\partial t} = 0$，但由于回路的运动，穿过它的[磁通量](@entry_id:268943)仍然会变化。这种电动势的微观起源是作用在导体内部自由电荷上的**洛伦兹磁力（magnetic Lorentz force）**。

当一段导体以速度 $\mathbf{v}$ 在[磁场](@entry_id:153296) $\mathbf{B}$ 中运动时，导体内的自由电荷（例如电子）也以相同的速度 $\mathbf{v}$ 随之运动。这些[电荷](@entry_id:275494)会受到一个磁力 $\mathbf{F}_m = q(\mathbf{v} \times \mathbf{B})$。这个力会驱使[电荷](@entry_id:275494)在导体内部移动，一端聚集正[电荷](@entry_id:275494)，另一端聚集负[电荷](@entry_id:275494)，直到由此产生的静电场力 $\mathbf{F}_e = q\mathbf{E}_s$ 与磁力相抗衡，[达到平衡](@entry_id:170346)。单位[电荷](@entry_id:275494)所受到的等效非静电力（源[力场](@entry_id:147325)）就是 $\mathbf{f}_m = \mathbf{v} \times \mathbf{B}$。将这个[力场](@entry_id:147325)沿整个闭合回路积分，就得到了**[动生电动势](@entry_id:264357)**：

$$
\mathcal{E} = \oint (\mathbf{v} \times \mathbf{B}) \cdot d\mathbf{l}
$$

一个经典的宏观例子是飞机在地球[磁场](@entry_id:153296)中飞行 [@problem_id:18570]。假设一架翼展为 $L$ 的飞机在地球[磁场](@entry_id:153296)中水平飞行。地球[磁场](@entry_id:153296) $\mathbf{B}$ 具有一个垂直向下的分量 $B_{\text{vert}} = B\sin\delta$，其中 $\delta$ 是磁倾角。飞机的机翼作为导体，以水平速度 $\mathbf{v}$ 切割这个垂直[磁场](@entry_id:153296)分量。机翼中的[电荷](@entry_id:275494)会感受到一个沿翼展方向的[洛伦兹力](@entry_id:145104)，其[力场](@entry_id:147325)大小为 $v B_{\text{vert}}$。因此，在翼尖之间会产生一个[动生电动势](@entry_id:264357)。如果考虑到机翼后掠角 $\theta$，有效切割[磁场](@entry_id:153296)的翼展长度是 $L\cos\theta$。因此，翼尖间的电动势大小为：

$$
\mathcal{E} = \int_{\text{wingtip}}^{\text{wingtip}} (\mathbf{v} \times \mathbf{B}) \cdot d\mathbf{l} = v B_{\text{vert}} (L\cos\theta) = vBL\cos\theta\sin\delta
$$

[动生电动势](@entry_id:264357)不仅限于直线运动。当导体做旋转运动时，同样会产生电动势。一个很好的例子是**[单极发电机](@entry_id:261619)（homopolar generator）** [@problem_id:1578364]。一根长度为 $L$ 的导电杆，一端固定在[转轴](@entry_id:187094)上，以恒定[角速度](@entry_id:192539) $\omega$ 在垂直于自身的均匀[磁场](@entry_id:153296) $B$ 中旋转。杆上距离[转轴](@entry_id:187094) $r$ 处的点的线速度为 $v = \omega r$。此处的洛伦兹力场为 $\mathbf{v} \times \mathbf{B}$，其大小为 $\omega r B$，方向沿着杆。由于速度 $v$ 随半径 $r$ 变化，我们需要对整个杆长进行积分来求得总电动势：

$$
\mathcal{E} = \int_0^L (\mathbf{v} \times \mathbf{B}) \cdot d\mathbf{r} = \int_0^L (\omega r B) dr = \frac{1}{2} B \omega L^2
$$

如果将转轴和杆的另一端通过一个电阻 $R$ 连接，就会形成一个持续的直流电流，其热功率为 $P = \mathcal{E}^2/R = \frac{B^2 \omega^2 L^4}{4R}$。

[交流发电机](@entry_id:267674)的工作原理也是[动生电动势](@entry_id:264357)（或等效地，变化的[磁通量](@entry_id:268943)）的直接应用 [@problem_id:1795425]。一个面积为 $A=LW$ 的矩形线圈在均匀[磁场](@entry_id:153296) $\mathbf{B}$ 中以[角速度](@entry_id:192539) $\omega$ 旋转。如果[旋转轴](@entry_id:187094)与[磁场](@entry_id:153296)方向有一个夹角 $\phi$，那么只有垂直于旋转轴的[磁场](@entry_id:153296)分量 $B_{\perp} = B\sin\phi$ 会[对产生](@entry_id:154125)变化的[磁通量](@entry_id:268943)有贡献。在任意时刻 $t$，线圈[法向量](@entry_id:264185)与 $B_{\perp}$ 的夹角为 $\omega t$（假设从夹角为0开始）。穿过线圈的[磁通量](@entry_id:268943)为 $\Phi(t) = A B_{\perp} \cos(\omega t) = A B \sin\phi \cos(\omega t)$。根据法拉第定律，[感应电动势](@entry_id:264372)为：

$$
\mathcal{E}(t) = -\frac{d\Phi}{dt} = \omega A B \sin\phi \sin(\omega t)
$$

这是一个正弦交流电动势，其最大值（振幅）为 $\mathcal{E}_{\text{max}} = \omega A B \sin\phi = \omega B L W \sin\phi$。

### 两种机制的综合应用

在许多实际情况中，感生电动势和[动生电动势](@entry_id:264357)可能同时存在。法拉第定律的通用形式 $\mathcal{E} = -d\Phi_B/dt$ 优雅地涵盖了所有情况。当一个回路既在运动，又处于时变[磁场](@entry_id:153296)中时，我们只需计算总[磁通量](@entry_id:268943) $\Phi_B(t) = \int \mathbf{B}(t) \cdot d\mathbf{A}(t)$，然后对时间求导。

考虑一个矩形线圈，它绕一条边以角速度 $\omega$ 旋转，同时整个空间中的[磁场](@entry_id:153296)也在随时间变化 [@problem_id:1578324]。例如，设线圈在 $t=0$ 时位于 $xy$ 平面，绕 $y$ 轴旋转，其法向量为 $\hat{n}(t) = -\sin(\omega t)\hat{i} + \cos(\omega t)\hat{k}$。[磁场](@entry_id:153296)为 $\mathbf{B}(t) = B_0 \hat{j} + (\gamma + \beta t) \hat{k}$。穿过线圈的[磁通量](@entry_id:268943)为：

$$
\Phi(t) = A \cdot \mathbf{B}(t) \cdot \hat{n}(t) = LW [(\gamma + \beta t) \hat{k}] \cdot [-\sin(\omega t)\hat{i} + \cos(\omega t)\hat{k}] = LW (\gamma + \beta t)\cos(\omega t)
$$

应用[法拉第定律](@entry_id:149836)，并使用乘法[求导法则](@entry_id:145443)：

$$
\mathcal{E}(t) = -\frac{d\Phi}{dt} = -LW \left[ \beta\cos(\omega t) - \omega(\gamma + \beta t)\sin(\omega t) \right] = LW \left[ \omega(\gamma + \beta t)\sin(\omega t) - \beta\cos(\omega t) \right]
$$

在这个表达式中，$\omega(\gamma + \beta t)\sin(\omega t)$ 项与线圈的旋转（动生部分）有关，而 $-\beta\cos(\omega t)$ 项与[磁场](@entry_id:153296)自身的[线性增长](@entry_id:157553)（感生部分）有关。这清晰地展示了总电动势是两种机制贡献的叠加。

### 深入探讨：电动势、电势差与电路

#### 电动势与[电势差](@entry_id:275724)的辨析

在静电学中，[电场](@entry_id:194326)是[保守场](@entry_id:137555)，[电场](@entry_id:194326)力做的功与路径无关，因此可以明确定义[电势](@entry_id:267554) $V$。任意两点间的电势差 $V_Q - V_P$ 就是将单位正[电荷](@entry_id:275494)从 P 点移动到 Q 点[电场](@entry_id:194326)力所做的功。然而，在[电磁感应](@entry_id:181154)现象中，[感应电场](@entry_id:267314)是非保守的，其[环路积分](@entry_id:164828)不为零。这意味着我们无法为[感应电场](@entry_id:267314)定义一个[标量势](@entry_id:276177)。

此时，空间中的总[电场](@entry_id:194326)可以分解为一个保守的静电场分量 $\mathbf{E}_{es}$（由[导体表面的电荷](@entry_id:275974)积累产生，可以写成 $-\nabla V$）和一个非保守的[感应电场](@entry_id:267314)分量 $\mathbf{E}_{nc}$（由变化的磁通量产生）。即 $\mathbf{E}_{\text{total}} = \mathbf{E}_{es} + \mathbf{E}_{nc}$。

理想电压表测量的是其两端接线柱之间的**[电势差](@entry_id:275724)**，即 $\Delta V = -\int \mathbf{E}_{es} \cdot d\mathbf{l}$。这个读数是否等于电动势，取决于测量路径和电路的具体情况。

一个极具启发性的例子是一个电阻[分布](@entry_id:182848)不均匀的圆形回路，处于均匀变化[磁场](@entry_id:153296)中 [@problem_id:1578330]。设上半圆的单位长度电阻为 $\rho_1$，下半圆为 $\rho_2$。变化的[磁场](@entry_id:153296)在回路上产生一个均匀的切向[感应电场](@entry_id:267314) $E_{nc}$。这个[感应电场](@entry_id:267314)驱动一个电流 $I$ 在回路中流动。根据[欧姆定律](@entry_id:276027)的微观形式，沿线材的总[电场](@entry_id:194326)切向分量 $E_{\text{total}, \parallel}$ 满足 $E_{\text{total}, \parallel} = \rho(s) I$。因此，静电场分量为 $E_{es, \parallel} = E_{\text{total}, \parallel} - E_{nc, \parallel} = \rho(s) I - E_{nc}$。

当电压表沿着直径连接 P、Q 两点时，由于[感应电场](@entry_id:267314)是纯环形的，它在直径路径上的积分为零。因此，电压表读数就是纯粹的[静电势](@entry_id:188370)差 $V(Q) - V(P)$。通过沿上半圆或下半圆积分 $E_{es, \parallel}$，我们可以计算这个[电势差](@entry_id:275724)。例如，沿下半圆从 P 到 Q 积分：

$$
V(Q) - V(P) = \int_P^Q \mathbf{E}_{es} \cdot d\mathbf{l} = \int_P^Q (\rho_2 I - E_{nc}) ds = (\rho_2 I - E_{nc})\pi R
$$

将通过 $\oint (\rho_1+\rho_2)I ds = \oint E_{nc} ds$ 求出的电流 $I$ 代入，经过代数运算，最终得到电压表的读数为：

$$
V_{meter} = V(Q) - V(P) = \frac{\pi k R^2}{2} \frac{\rho_2 - \rho_1}{\rho_1 + \rho_2}
$$

这个结果表明，电压表的读数取决于两段半圆电阻的 *差异*。只有当 $\rho_1 = \rho_2$ 时，电压表读数才为零，尽管回路中存在非零的电动势和电流。这个例子深刻地揭示了电动势（驱动电流的全域效应）和[电势差](@entry_id:275724)（两点间的局域静电属性）之间的微妙区别。

#### [自感](@entry_id:265778)与[反电动势](@entry_id:268189)

当电流在电路中（尤其是在线圈中）流动时，它会产生自身的[磁场](@entry_id:153296)。如果这个电流发生变化，它产生的磁通量也会随之变化，根据法拉第定律，这将在电路自身中感应出一个电动势。这种现象称为**[自感](@entry_id:265778)（self-inductance）**。

[自感](@entry_id:265778)电动势，也常被称为**[反电动势](@entry_id:268189)（back EMF）**，其大小与电流的变化率成正比：

$$
\mathcal{E}_{\text{back}} = -L \frac{dI}{dt}
$$

其中 $L$ 是电路的**[自感](@entry_id:265778)系数**或**[电感](@entry_id:276031)（inductance）**，单位是亨利（H）。[反电动势](@entry_id:268189)的方向总是反抗电流的变化。

在[交流发电机](@entry_id:267674)等实际电路中，[自感](@entry_id:265778)效应是不可忽略的 [@problem_id:18627]。考虑一个由旋转线圈驱动的 R-L [串联电路](@entry_id:275175)。根据[基尔霍夫电压定律](@entry_id:276614)，外加的[动生电动势](@entry_id:264357) $\mathcal{E}_{\text{motional}}$ 必须等于电阻上的电压降 $IR$ 和[电感](@entry_id:276031)上的[反电动势](@entry_id:268189) $L\frac{dI}{dt}$ 之和：

$$
\mathcal{E}_{\text{motional}}(t) = I(t)R + L\frac{dI}{dt}
$$

对于一个正弦变化的[动生电动势](@entry_id:264357) $\mathcal{E}_{\text{motional}}(t) = \mathcal{E}_0 \sin(\omega t)$，其中 $\mathcal{E}_0 = N B A \omega$，这是一个[一阶线性微分方程](@entry_id:164869)。在[稳态](@entry_id:182458)下，电流 $I(t)$ 也是正弦的，但与电动势之间存在一个相位差。使用[复阻抗](@entry_id:273113)法可以方便地求解。电路的总阻抗为 $Z = R + j\omega L$，其模为 $|Z| = \sqrt{R^2 + (\omega L)^2}$。因此，电流的振幅为 $I_{amp} = \frac{\mathcal{E}_0}{|Z|}$。我们关心的电阻两端的电压振幅为：

$$
V_{R, \text{amp}} = I_{amp} R = \frac{\mathcal{E}_0 R}{|Z|} = \frac{N B A \omega R}{\sqrt{R^2 + (\omega L)^2}}
$$

这个结果表明，由于[自感](@entry_id:265778)的存在，电路的有效“阻力”增加了，导致电流和电阻上的电压都小于没有电感时的情况。

#### [磁矢势](@entry_id:141246)的视角

为了从更根本的层面理解电磁感应，我们可以引入**[磁矢势](@entry_id:141246)（magnetic vector potential）** $\mathbf{A}$。磁矢势定义为 $\mathbf{B} = \nabla \times \mathbf{A}$。将此代入法拉第定律的[微分形式](@entry_id:146747) $\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$，我们得到：

$$
\nabla \times \mathbf{E} = -\frac{\partial}{\partial t}(\nabla \times \mathbf{A}) = -\nabla \times \left(\frac{\partial \mathbf{A}}{\partial t}\right)
$$

$$
\nabla \times \left(\mathbf{E} + \frac{\partial \mathbf{A}}{\partial t}\right) = 0
$$

一个场的旋度为零，意味着这个场是保守场，可以表示为某个标量势（这里是[静电势](@entry_id:188370) $-V$）的梯度。因此，我们得到[电场](@entry_id:194326) $\mathbf{E}$ 最普遍的表达式：

$$
\mathbf{E} = -\nabla V - \frac{\partial \mathbf{A}}{\partial t}
$$

这个表达式清楚地显示了[电场](@entry_id:194326)的两个来源：由电荷分布产生的静电势 $V$ 的梯度，和由[磁矢势](@entry_id:141246)的时间变化率 $\frac{\partial \mathbf{A}}{\partial t}$ 产生的[感应电场](@entry_id:267314)。

我们可以利用这个方法来重新审视感应问题，例如计算一个电流随时间变化的无限长[螺线管](@entry_id:261182)在其外部同轴圆形回路中产生的电动势 [@problem_id:1578350]。对于半径为 $a$、单位长度匝数为 $n$ 的长螺线管，其内部[磁场](@entry_id:153296)为 $B = \mu_0 n I$，外部为零。通过[斯托克斯定理](@entry_id:264534)或安培环路定律的[矢势](@entry_id:153642)形式，可以求得在[螺线管](@entry_id:261182)外部 ($s > a$) 的[磁矢势](@entry_id:141246)为 $\mathbf{A} = \frac{\mu_0 n a^2 I}{2s} \hat{\phi}$。

由于没有[自由电荷](@entry_id:264392)积累，[静电势](@entry_id:188370) $V$ 为零。[感应电场](@entry_id:267314)完全由 $\mathbf{A}$ 的时间变化给出：

$$
\mathbf{E} = -\frac{\partial \mathbf{A}}{\partial t} = -\frac{\mu_0 n a^2}{2s} \frac{dI}{dt} \hat{\phi}
$$

将这个[电场](@entry_id:194326)在一个半径为 $r > a$ 的回路上积分，得到[感应电动势](@entry_id:264372)：

$$
\mathcal{E} = \oint \mathbf{E} \cdot d\mathbf{l} = E_{\phi}(r) \cdot (2\pi r) = \left(-\frac{\mu_0 n a^2}{2r} \frac{dI}{dt}\right)(2\pi r) = -\mu_0 n \pi a^2 \frac{dI}{dt}
$$

这个结果与直接使用磁通量法则 $\mathcal{E} = -d\Phi/dt$（其中 $\Phi = B \cdot (\pi a^2) = \mu_0 n I \pi a^2$）得到的结果完全一致。通过[磁矢势](@entry_id:141246)的路径，我们不仅得到了电动势的大小，还得到了空间中每一点的[感应电场](@entry_id:267314)[分布](@entry_id:182848)，这为我们提供了关于电磁感应现象更为深刻和根本的物理图像。