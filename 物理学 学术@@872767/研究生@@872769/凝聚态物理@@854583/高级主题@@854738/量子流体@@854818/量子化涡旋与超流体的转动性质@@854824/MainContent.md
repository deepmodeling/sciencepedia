## 引言
超流体，作为一种[宏观量子态](@entry_id:192759)，其流动在本质上是无旋的，这与我们在日常经验中观察到的[旋转流](@entry_id:276737)体形成了鲜明对比。那么，当一个[超流体](@entry_id:180718)系统被置于旋转中时，它将如何响应？这一看似矛盾的问题引出了[凝聚态物理学](@entry_id:140205)中最迷人的概念之一：[量子化涡旋](@entry_id:147055)。这些拓扑缺陷作为角动量的量子载体，是理解超流体宏观转动性质的关键。本文旨在系统性地揭示[量子化涡旋](@entry_id:147055)的物理学。在“原理与机制”一章中，我们将深入探讨单个涡旋的定义、能量、动力学，以及它们如何形成[涡旋晶格](@entry_id:140837)来模拟[刚体转动](@entry_id:191086)。随后的“应用与跨学科联系”一章将展示这些基本原理如何应用于从实验室中的[玻色-爱因斯坦凝聚体](@entry_id:145990)到遥远[中子星](@entry_id:147259)内部等多样化的物理前沿。最后，“动手实践”部分将提供一系列计算问题，以加深对涡旋动力学及其与环境相互作用的理解。让我们首先从[量子化涡旋](@entry_id:147055)的基本原理与机制开始。

## 原理与机制

本章旨在系统性地阐述[量子化涡旋](@entry_id:147055)的基本原理及其在超流体宏观转动性质中所扮演的核心角色。我们将从单个[量子化涡旋](@entry_id:147055)的定义与性质出发，逐步探讨其动力学行为、在旋转超流体中形成的[集体态](@entry_id:168597)（[涡旋晶格](@entry_id:140837)），以及这些结构所支持的独特激发和耗散机制。

### [量子化涡旋](@entry_id:147055)线

超流体，作为一种[宏观量子现象](@entry_id:144018)，其状态可以通过一个复序参量，即[宏观波函数](@entry_id:143853) $\Psi(\mathbf{r}, t)$ 来描述：
$$
\Psi(\mathbf{r}, t) = \sqrt{n(\mathbf{r}, t)} e^{i\phi(\mathbf{r}, t)}
$$
其中 $n(\mathbf{r}, t)$ 是超流体中相干粒子的数密度，$\phi(\mathbf{r}, t)$ 是其宏观量子相。[超流体](@entry_id:180718)的[速度场](@entry_id:271461) $\mathbf{v}_s$ 与相位的梯度直接相关，其关系式为：
$$
\mathbf{v}_s = \frac{\hbar}{m} \nabla\phi
$$
这里 $m$ 是构成[超流体](@entry_id:180718)的单个粒子的质量，$\hbar$ 是[约化普朗克常数](@entry_id:275910)。从这个定义可以立即推导出一个关键性质：只要[波函数](@entry_id:147440) $\Psi$ 是单值且非零的，速度场就是无旋的，即 $\nabla \times \mathbf{v}_s = \frac{\hbar}{m} \nabla \times (\nabla\phi) \equiv 0$。这意味着[超流体](@entry_id:180718)的流动本质上是无涡的。

然而，超流体可以通过形成[拓扑缺陷](@entry_id:138787)来支持宏观上的旋转。这种缺陷被称为**[量子化涡旋](@entry_id:147055) (quantized vortex)**。在涡旋线的中心，[超流体](@entry_id:180718)密度 $n$ 降为零，[波函数](@entry_id:147440)的相位在此处出现[奇点](@entry_id:137764)。考虑一条环绕涡旋线的闭合路径 $C$，我们计算速度场的[环路积分](@entry_id:164828)，即**环量 (circulation)** $\Gamma$：
$$
\Gamma = \oint_C \mathbf{v}_s \cdot d\mathbf{l} = \frac{\hbar}{m} \oint_C \nabla\phi \cdot d\mathbf{l} = \frac{\hbar}{m} \Delta\phi_C
$$
由于[波函数](@entry_id:147440) $\Psi$ 必须是单值的，即绕行一圈后其值不变，相位的总变化量 $\Delta\phi_C$ 必须是 $2\pi$ 的整数倍，即 $\Delta\phi_C = 2\pi N$，其中 $N$ 是一个整数，称为[卷绕数](@entry_id:138707)。因此，环量是量子化的：
$$
\Gamma = N \frac{2\pi\hbar}{m} = N \kappa
$$
其中 $\kappa = 2\pi\hbar/m$ 被称为**环量量子 (quantum of circulation)**。在大多数情况下，能量上最有利的是形成[卷绕数](@entry_id:138707)为 $N=1$ 的涡旋。

对于沿 $z$ 轴的一条笔直的单[量子涡旋](@entry_id:147375)线（$N=1$），其[速度场](@entry_id:271461)在[柱坐标系](@entry_id:266798) $(r, \varphi, z)$ 中呈纯方位角[分布](@entry_id:182848)。通过应用环量[量子化条件](@entry_id:182165)于一个半径为 $r$ 的圆形路径，我们得到 $v_\phi \cdot 2\pi r = \kappa$，因此[速度场](@entry_id:271461)的大小为：
$$
v_\phi(r) = \frac{\kappa}{2\pi r} = \frac{\hbar}{mr}
$$
这个 $1/r$ 的[速度场](@entry_id:271461)在 $r \to 0$ 时发散，这在物理上是不可能的。实际上，在涡旋线的中心存在一个半径约为**[相干长度](@entry_id:139128) (coherence length)** $\xi$ 的**涡旋核 (vortex core)**。在这个核内，超[流体性质](@entry_id:200256)消失，粒子密度 $n$ 趋于零，从而避免了[速度场](@entry_id:271461)的发散。

### 单个涡旋的性质：能量与角动量

[量子化涡旋](@entry_id:147055)作为超流体中的基本[拓扑激发](@entry_id:157702)，拥有明确定义的能量和角动量。

#### 动能

一个涡旋的存在意味着超流体在流动，因此携带着动能。对于沿 $z$ 轴的笔直涡旋线，其单位长度的动能 $E/L$ 可以通过对[超流体](@entry_id:180718)区域内的动能密度 $\frac{1}{2}\rho_s v_s^2$ 进行积分得到（$\rho_s=mn_s$ 是[超流体](@entry_id:180718)质量密度）。假设[超流体](@entry_id:180718)被限制在半径为 $R$ 的圆柱形容器中，积分区域为从涡旋核半径 $\xi$ 到容器边界 $R$ 的环形区域：
$$
\frac{E}{L} = \int_{\xi}^{R} \frac{1}{2} \rho_s v_\phi(r)^2 (2\pi r) dr = \int_{\xi}^{R} \frac{1}{2} \rho_s \left( \frac{\kappa}{2\pi r} \right)^2 2\pi r dr = \frac{\rho_s \kappa^2}{4\pi} \int_{\xi}^{R} \frac{dr}{r}
$$
积分结果为：
$$
\frac{E}{L} = \frac{\rho_s \kappa^2}{4\pi} \ln\left(\frac{R}{\xi}\right)
$$
这个结果揭示了一个重要特征：涡旋的能量随系统尺寸 $R$ 对数发散。这是由其长程 $1/r$ 速度场造成的。这意味着将一个涡旋引入无限大的[超流体](@entry_id:180718)需要无穷大的能量。在实际系统中，能量总是有限的，并依赖于系统的边界或涡旋间的平均距离。

在更复杂的情况下，例如各向异性的[超流体](@entry_id:180718)中，其质量密度由张量 $\rho_{ij}$ 描述。对于沿 $z$ 轴的涡旋，其单位长度的能量取决于垂直于涡旋线的平面内的质量密度分量。通过详细计算可以证明，能量表达式变为 $E/L = \frac{\kappa^2}{8\pi}(\rho_x + \rho_y)\ln(\frac{R}{\xi})$，即有效的质量密度是垂直方向上两个[主轴](@entry_id:172691)密度的平均值 [@problem_id:193757]。

#### 角动量

涡旋周围的环形流动也携带了角动量。对于位于容器中心的单条涡旋线，其单位长度的角动量 $\mathcal{L}_z$ 是角[动量密度](@entry_id:271360) $\ell_z = \rho_s (\mathbf{r} \times \mathbf{v}_s)_z = \rho_s r v_\phi$ 在[截面](@entry_id:154995)上的积分：
$$
\mathcal{L}_z = \int_{\xi}^{R} (\rho_s r v_\phi) (2\pi r) dr = \int_{\xi}^{R} \rho_s r \left(\frac{\hbar}{mr}\right) 2\pi r dr = \frac{2\pi\rho_s\hbar}{m} \int_{\xi}^{R} r dr
$$
积分得到 $\mathcal{L}_z = \frac{\pi\rho_s\hbar}{m}(R^2 - \xi^2)$。现在，我们将其与单位长度内的超流体总粒子数 $N_{2D}$ 联系起来。单位长度内的总质量为 $M/L = \rho_s \pi (R^2 - \xi^2)$，因此粒子总数为 $N_{2D} = M/(Lm) = \frac{\rho_s \pi (R^2 - \xi^2)}{m}$。将此关系代入角动量表达式，我们得到一个惊人而深刻的结果 [@problem_id:193633]：
$$
\mathcal{L}_z = \hbar N_{2D}
$$
这意味着，当一个单[量子涡旋](@entry_id:147375)存在于系统中时，平均每个[超流体](@entry_id:180718)粒子贡献了大小为 $\hbar$ 的角动量。这个结果凸显了涡旋作为角动量量子载体的根本作用。

### 涡旋动力学：运动与相互作用

涡旋线不是静止的结构，它们会响应背景流、其他涡旋以及自身形状的影响而运动。其运动的基本准则是：**涡旋线的一小段会以其所在位置的局部超[流体速度](@entry_id:267320)运动**。这个局部速度是所有其他[速度场](@entry_id:271461)来源（如其他涡旋、边界效应、外部施加的流场）在该点贡献的总和，但不包括该段自身产生的[速度场](@entry_id:271461)。

#### 涡旋-反涡旋对 (2D)

在二维[超流体](@entry_id:180718)中，点状涡旋的相互作用为我们提供了理解涡旋动力学的基础。一个特别重要的系统是**涡旋-反涡旋对**，即一个卷绕数为 $+1$ 的涡旋和一个[卷绕数](@entry_id:138707)为 $-1$ 的反涡旋。使用[复势](@entry_id:162103)理论可以优雅地处理这个问题。一个位于 $z_0$ 的涡旋的[复势](@entry_id:162103)为 $\Phi(z) = -i \frac{\kappa}{2\pi} \ln(z-z_0)$，而[复速度](@entry_id:201810)为 $W(z) = v_x - i v_y = d\Phi/dz$。

考虑一个涡旋位于 $z_v = +id/2$，一个反涡旋位于 $z_{av} = -id/2$。在涡旋 $z_v$ 的位置，它感受到的速度是由反涡旋产生的。反涡旋的[复势](@entry_id:162103)为 $\Phi_{av}(z) = +i \frac{\kappa}{2\pi} \ln(z - z_{av})$，其产生的[复速度](@entry_id:201810)为 $W_{av}(z) = +i \frac{\kappa}{2\pi} \frac{1}{z - z_{av}}$。在 $z_v$ 处，这个速度为：
$$
W(z_v) = i \frac{\kappa}{2\pi} \frac{1}{id/2 - (-id/2)} = i \frac{\kappa}{2\pi} \frac{1}{id} = \frac{\kappa}{2\pi d}
$$
由于 $W = v_x - iv_y$ 是一个实数，这意味着 $v_y=0$，而 $v_x = \frac{\kappa}{2\pi d}$。同理可得，反涡旋感受到的由涡旋产生的速度也是 $(\frac{\kappa}{2\pi d}, 0)$。因此，涡旋-反涡旋对会共同以垂直于它们之间连线的方向匀速运动，速度大小与它们的间距 $d$ 成反比。若存在一个沿 $x$ 轴的背景流 $v_0$，涡旋的速度就是简单地叠加，变为 $v_x = v_0 + \frac{\kappa}{2\pi d}$ [@problem_id:193740]。

#### 涡旋环 (3D)

在三维空间中，涡旋线可以形成闭合的环，称为**涡旋环 (vortex ring)**。这种环状涡旋由于自身的弯曲，会产生自诱导运动。环的每一段都会被环上其他部分产生的速度场所驱动。其结果是，一个孤立的圆形涡旋环会沿着其对称轴方向以恒定速度传播，就像一个烟圈。

涡旋环的动力学可以通过哈密顿力学来描述。其能量 $E(R)$ 和[正则动量](@entry_id:155151) $P(R)$ 是环半径 $R$ 的函数。对于半径为 $R$、核半径为 $a_0$ 的环，其能量和动量分别近似为 $E(R) \approx \frac{1}{2} \rho_s \kappa^2 R (\ln(\frac{8R}{a_0}) - C)$ 和 $P(R) = \pi \rho_s \kappa R^2$，其中 $C$ 是一个与涡旋核结构有关的常数。环的[传播速度](@entry_id:189384) $v$ 可以通过哈密顿关系 $v = dE/dP$ 得到，这类似于波包的[群速度](@entry_id:147686)。利用链式法则 $v = (dE/dR) / (dP/dR)$，可以推导出 [@problem_id:193635]：
$$
v = \frac{\kappa}{4\pi R} \left( \ln\left(\frac{8R}{a_0}\right) - C + 1 \right)
$$
这个结果表明，与[二维涡旋](@entry_id:158722)对不同，涡旋环的自诱导速度对半径的依赖是对数形式的，并且半径越大的环运动得越慢。

#### [开尔文波](@entry_id:185207)

涡旋线本身也可以发生[振动](@entry_id:267781)。沿涡旋线传播的螺旋形扰动被称为**[开尔文波](@entry_id:185207) (Kelvin waves)**。这种波的产生源于涡旋线的局部曲率引起的自诱导运动。在**局域诱导近似 (local induction approximation, LIA)** 中，涡旋线上一段的运动速度正比于该点的曲率。对于一个沿 $z$ 轴的小位移 $\mathbf{r}_\perp(z, t)$，其[运动方程](@entry_id:170720)可以写为 $\frac{\partial \mathbf{r}_\perp}{\partial t} \propto \hat{\mathbf{z}} \times \frac{\partial^2 \mathbf{r}_\perp}{\partial z^2}$。如果系统整体还在以[角速度](@entry_id:192539) $\mathbf{\Omega}$ 旋转，则还需加上一项背景速度的贡献。

考虑一个沿 $z$ 轴传播的[圆偏振波](@entry_id:200164) $\mathbf{r}_\perp(z, t) = A(\cos(kz - \omega t) \hat{\mathbf{x}} + \sin(kz - \omega t) \hat{\mathbf{y}})$，代入完整的运动方程，可以解出其色散关系 $\omega(k)$ [@problem_id:193657]：
$$
\omega(k) = \frac{\kappa k^2}{4\pi} \ln\left(\frac{c}{ka}\right) - \Omega
$$
其中第一项是自诱导产生的，表明高频（大 $k$）扰动传播得更快；第二项是背景旋转引起的进动频率的修正。当 $\omega=0$ 时，[开尔文波](@entry_id:185207)会变得不稳定，这在[超流体](@entry_id:180718)[湍流](@entry_id:151300)和[中子星](@entry_id:147259)的动力学中具有重要意义。

### 超流体与旋转：[涡旋晶格](@entry_id:140837)

经典流体可以通过形成一个刚体旋转的矢量场（$v=\Omega r$）来适应外部施加的旋转。然而，超流体的无旋性（$\nabla \times \mathbf{v}_s = 0$）禁止了这种流动。那么，超流体是如何实现宏观旋转的呢？答案是：通过形成一个[量子化涡旋](@entry_id:147055)的阵列。

#### 涡旋的形成与临界角速度

将[超流体](@entry_id:180718)置于一个以角速度 $\Omega$ 旋转的容器中，系统的自由能需要在旋转参考系中进行评估。旋转参考系中的自由能 $F'$ 与[实验室参考系](@entry_id:166991)中的能量 $E$ 和角动量 $L_z$ 的关系是 $F' = E - \Omega L_z$。

一个无涡旋的静止超流体，$E=0, L_z=0$，因此 $F'_0=0$。当一个[涡旋形成](@entry_id:270192)时，系统获得了能量 $E_1$ 和角动量 $L_1$。这个状态的自由能为 $F'_1 = E_1 - \Omega L_1$。只有当 $F'_1  F'_0 = 0$ 时，形成涡旋在能量上才是有利的。这定义了形成第一个涡旋的**[热力学](@entry_id:141121)临界角速度** $\Omega_c$：
$$
\Omega_c = \frac{E_1}{L_1} = \frac{\frac{\rho_s \kappa^2}{4\pi} \ln(\frac{R}{\xi})}{\frac{\pi\rho_s\hbar}{m}(R^2 - \xi^2)} \approx \frac{\hbar}{mR^2} \ln\left(\frac{R}{\xi}\right)
$$
这个[临界角](@entry_id:169189)速度的存在解释了为什么慢速旋转的超流体中没有涡旋。只有当旋转足够快，[转动带](@entry_id:754426)来的自由能减少 $(-\Omega L_1)$ 足以补偿形成涡旋所需的能量 $E_1$ 时，涡旋才会自发成核。值得注意的是，这个 $\Omega_c$ 中包含的对数因子 $\ln(R/\xi)$ 构成了一个[能量势](@entry_id:748988)垒，使得涡旋的[成核](@entry_id:140577)比一个简单的估计要困难 [@problem_id:193631]。

#### [费曼关系](@entry_id:199893)与[涡旋晶格](@entry_id:140837)

当角速度远大于 $\Omega_c$ 时，大量的涡旋会充满超流体。这些涡旋的排布并非随机，由于它们之间存在排斥相互作用（对于同号涡旋），它们会自发组织成一个规则的二维[晶格](@entry_id:196752)，通常是三角形的，这被称为**[阿布里科索夫涡旋晶格](@entry_id:146969) (Abrikosov vortex lattice)**。

在这个状态下，尽管在微观尺度上（涡旋之间），流场仍然是无旋的，但在宏观尺度上（远大于涡旋间距），对[速度场](@entry_id:271461)进行平均，得到的平均速度 $\langle \mathbf{v}_s \rangle$ 恰好模拟了刚体旋转：$\langle \mathbf{v}_s \rangle = \mathbf{\Omega} \times \mathbf{r}$。

我们可以利用这个宏观-微观的联系来推导涡旋的[面密度](@entry_id:161889) $n_v$（单位面积的涡旋数量）。考虑一个宏观大圈 $C$，其面积为 $A$。一方面，环量可以由宏观平均速度场通过斯托克斯定理计算：
$$
\Gamma = \oint_C \langle \mathbf{v}_s \rangle \cdot d\mathbf{l} = \int_A (\nabla \times \langle \mathbf{v}_s \rangle) \cdot d\mathbf{A} = \int_A (2\mathbf{\Omega}) \cdot d\mathbf{A} = 2\Omega A
$$
另一方面，这个总环量必须等于圈内所有涡旋环量量子的总和，即 $\Gamma = N_v \kappa = (n_v A) \kappa$。联立这两个表达式，我们得到著名的**[费曼关系](@entry_id:199893) (Feynman relation)** [@problem_id:193656]：
$$
n_v = \frac{2\Omega}{\kappa} = \frac{m\Omega}{\pi\hbar}
$$
这个关系式简洁地将一个宏观的力学量（[角速度](@entry_id:192539) $\Omega$）与一个微观的量子统计量（涡旋密度 $n_v$）联系起来，是[超流体](@entry_id:180718)物理学中的一个里程碑。[涡旋晶格](@entry_id:140837)的形成是超流体响应旋转的普遍机制，从实验室中的液氦、玻色-爱因斯坦凝聚体到遥远的[中子星](@entry_id:147259)内部，都遵循这一原理。涡旋之间的相互作用驱动着[晶格](@entry_id:196752)的集体运动，一个简单的例子是，四个位于正方形顶点的涡旋会作为一个刚性结构绕中心旋转 [@problem_id:193760]。

### [集体激发](@entry_id:145026)与耗散效应

[涡旋晶格](@entry_id:140837)本身并非一个静态的背景，它是一个动态的弹性介质，能够支持其自身的集体激发，并介导[超流体](@entry_id:180718)与[正常流体](@entry_id:183299)之间的能量和动量交换。

#### [特卡琴科波](@entry_id:161491)

[涡旋晶格](@entry_id:140837)虽然由流体中的线缺陷构成，但它具有类似于固体的弹性，特别是抵抗剪切形变的能力。这种弹性使得[晶格](@entry_id:196752)可以支持一种低频的横波，称为**[特卡琴科波](@entry_id:161491) (Tkachenko waves)**。这种波对应于涡旋格点的横向位移[振动](@entry_id:267781)。

将[涡旋晶格](@entry_id:140837)视为一个具有有效剪切模量 $\mu$ 的连续弹性介质，其[位移场](@entry_id:141476) $\mathbf{u}(\mathbf{r}, t)$ 的[运动方程](@entry_id:170720)与超流体速度 $\mathbf{v}_s$ 的[欧拉方程](@entry_id:177914)耦合。对于[横波](@entry_id:269527)（$\nabla \cdot \mathbf{u}=0$），可以推导出位移场 $\mathbf{u}$ 满足一个简单的[波动方程](@entry_id:139839) [@problem_id:193661]：
$$
\rho_s \frac{\partial^2 \mathbf{u}}{\partial t^2} = \mu \nabla^2 \mathbf{u}
$$
这立即给出了波的相速度 $c_T = \sqrt{\mu/\rho_s}$。对于三角形[涡旋晶格](@entry_id:140837)，[剪切模量](@entry_id:167228)为 $\mu = \frac{\rho_s \kappa^2 n_v}{8\pi}$。代入[费曼关系](@entry_id:199893) $n_v=2\Omega/\kappa$，我们最终得到[特卡琴科波](@entry_id:161491)的[线性色散关系](@entry_id:266313)：
$$
\omega(k) = c_T k = \sqrt{\frac{\kappa \Omega}{4\pi}} k
$$
这种[声学模](@entry_id:263916)式的色散关系是[涡旋晶格](@entry_id:140837)作为一个有序物态（“量子固体”）存在的直接证据。

#### 互摩擦

在有限温度下（如氦-II），超流体可以由**[双流体模型](@entry_id:139846) (two-fluid model)** 描述，即一个无粘的[超流体](@entry_id:180718)组分（密度 $\rho_s$，速度 $\mathbf{v}_s$）和一个粘性的正常流体组分（密度 $\rho_n$，速度 $\mathbf{v}_n$，由[声子](@entry_id:140728)、转子等热[元激发](@entry_id:140859)构成）。

[量子化涡旋](@entry_id:147055)是[超流体](@entry_id:180718)组分中的缺陷，但它们可以与[正常流体](@entry_id:183299)组分中的热[元激发](@entry_id:140859)发生散射，从而在两组分之间传递动量。这种机制被称为**互摩擦 (mutual friction)**。作用在单位长度涡旋线上的互[摩擦力](@entry_id:171772) $\mathbf{f}_{ns}$ 由 Hall-Vinen-Bekarevich-Khalatnikov (HVBK) 理论描述：
$$
\mathbf{f}_{ns} = \alpha (\mathbf{v}_n - \mathbf{v}_L)_\perp - \alpha' \hat{\boldsymbol{\kappa}} \times (\mathbf{v}_n - \mathbf{v}_L)
$$
这里，$\mathbf{v}_L$ 是涡旋线的速度，$\hat{\boldsymbol{\kappa}}$ 是涡旋线的切向单位矢量。第一项由耗散系数 $\alpha$ 描述，代表平行于相对速度 $(\mathbf{v}_n - \mathbf{v}_L)$ 的垂直分量的阻力。第二项由反应系数 $\alpha'$ 描述，代表类似于[马格努斯效应](@entry_id:191011)的、垂直于相对速度的“[升力](@entry_id:274767)”。这两个系数都依赖于温度。

例如，考虑一条沿 $z$ 轴静止的涡旋线（$\mathbf{v}_L=\mathbf{0}$），而[正常流体](@entry_id:183299)具有速度 $\mathbf{v}_n = v_{n,x}\hat{\mathbf{x}} + v_{n,z}\hat{\mathbf{z}}$。作用在涡旋线上的力仅取决于垂直于涡旋线的相对速度分量，即 $\mathbf{v}_{n\perp} = v_{n,x}\hat{\mathbf{x}}$。计算得到的力为 $\mathbf{f}_{ns} = \alpha v_{n,x}\hat{\mathbf{x}} - \alpha' v_{n,x}\hat{\mathbf{y}}$。其大小为 $|\mathbf{f}_{ns}| = |v_{n,x}|\sqrt{\alpha^2 + \alpha'^2}$ [@problem_id:193768]。互摩擦是旋转[超流体](@entry_id:180718)达到平衡状态以及超流体[湍流](@entry_id:151300)中[能量耗散](@entry_id:147406)的关键机制。