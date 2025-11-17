## 引言
在量子世界中，任何系统都不可避免地与周围环境发生相互作用，从而成为一个“[开放量子系统](@entry_id:138632)”。精确描述这类系统中相干性与耗散、确定性演化与随机涨落之间的复杂博弈，是现代物理学的核心挑战之一。布洛赫-朗之万方程（Bloch-Langevin Equations）正为此提供了一个强大而普适的理论框架，它超越了仅描述系统平均行为的半经典模型，将源于环境的量子噪声内禀地包含在内，从而构成了理解[开放量子系统](@entry_id:138632)动力学的基石。本文旨在系统性地剖析这一关键理论，填补[唯象模型](@entry_id:273816)与完整量子描述之间的知识鸿沟。

在接下来的内容中，我们将分三个章节展开深入探讨。首先，在“原理与机制”一章中，我们将从更为人熟知的[光学布洛赫方程](@entry_id:171131)出发，揭示其如何通过引入朗之万噪声项而演变为布洛赫-朗之万方程，并深入探讨耗散与涨落的微观物理起源，以及它们如何决定系统的动力学与谱学特性。随后，“应用与[交叉](@entry_id:147634)学科联系”一章将展示该理论惊人的普适性，通过一系列横跨[激光](@entry_id:194225)物理、[腔量子电动力学](@entry_id:149422)、[量子热力学](@entry_id:140152)乃至天体物理学的实例，阐明它如何成为连接不同物理分支的理论桥梁。最后，通过“动手实践”部分提供的一系列计算问题，读者将有机会亲手应用这些方程，从而将理论知识转化为解决实际问题的能力。让我们一同踏上这段探索开放量子世界的旅程。

## 原理与机制

继前一章对背景的介绍之后，本章将深入探讨布洛赫-朗之万方程（Bloch-Langevin Equations）的核心物理原理和数学机制。我们将从现象学的[光学布洛赫方程](@entry_id:171131)出发，逐步揭示其背后更为深刻的量子[随机过程](@entry_id:159502)。通过分析原子与光场相互作用中的关键现象，如饱和、[谱线](@entry_id:193408)移动和[光子统计](@entry_id:175965)，我们将系统地构建一个描述[开放量子系统](@entry_id:138632)中相干性与耗散的完整理论框架。

### [光学布洛赫方程](@entry_id:171131)：平均场图像

描述一个二能级原子与经典[单色光](@entry_id:178750)场相互作用的最简化、同时也是最广泛应用的理论模型是**[光学布洛赫方程](@entry_id:171131) (Optical Bloch Equations, OBEs)**。该模型在[半经典近似](@entry_id:147497)下成立，即原子被量子化处理，而光场则被视为经典的[正弦波](@entry_id:274998)。

为了消除光场[载波](@entry_id:261646)频率 $\omega_L$ 带来的快速[振荡](@entry_id:267781)，我们通常在一个以 $\omega_L$ 旋转的[参考系](@entry_id:169232)中分析问题。在这个[旋转参考系](@entry_id:174154)中，原子的状态可以用**[布洛赫矢量](@entry_id:144181) (Bloch vector)** $\vec{r} = (u, v, w)$ 来描述。其三个分量分别对应原子偶极矩的同相分量、异相（正交）分量以及[布居数反转](@entry_id:155020)：
- $u = \langle \hat{\sigma}_x \rangle$：与驱动场同相的偶极矩分量。
- $v = \langle \hat{\sigma}_y \rangle$：与驱动场正交的偶极矩分量。
- $w = \langle \hat{\sigma}_z \rangle = \langle |e\rangle\langle e| - |g\rangle\langle g| \rangle$：[激发态](@entry_id:261453)与[基态](@entry_id:150928)之间的布居数差。

一个孤立的二能级原子在光场驱动下的演化是纯相干的，由[拉比频率](@entry_id:154019) $\Omega$（表征光场强度）和失谐 $\Delta = \omega_L - \omega_A$（光场频率与[原子跃迁](@entry_id:158267)频率之差）决定。然而，在真实物理系统中，原子不可避免地会与周围的环境（如真空[电磁场](@entry_id:265881)、热辐射场或[声子](@entry_id:140728)浴）发生相互作用。这种相互作用导致了能量的耗散和相位的随机化，即**弛豫 (relaxation)**。

[光学布洛赫方程](@entry_id:171131)通过引入唯象的弛豫速率，将这些不可逆过程纳入了动力学模型中。主要有两种弛豫过程：
1.  **纵向弛豫 (Longitudinal Relaxation)**：描述布居数反转 $w$ 回归其热平衡值 $w_{eq}$ 的过程，其速率为 $\Gamma_1$。这个过程通常与[能量耗散](@entry_id:147406)有关，例如原子的[自发辐射](@entry_id:140032)。
2.  **横向弛豫 (Transverse Relaxation)**：描述相干项 $u$ 和 $v$ 的衰减，其速率为 $\Gamma_2$。该过程也称为**[退相干](@entry_id:145157) (dephasing)**，它不仅包含由[能量弛豫](@entry_id:136820)引起的退相干，还可能包含不改变[能级布居](@entry_id:197877)的“[纯退相干](@entry_id:204036)”过程。

综合相干驱动和唯象弛豫，[光学布洛赫方程](@entry_id:171131)可写为如下的[线性微分方程组](@entry_id:155297) [@problem_id:648764] [@problem_id:648751]：
$$
\frac{d}{dt} \begin{pmatrix} u \\ v \\ w \end{pmatrix} = \begin{pmatrix} -\Gamma_2  -\Delta  0 \\ \Delta  -\Gamma_2  -\Omega \\ 0  \Omega  -\Gamma_1 \end{pmatrix} \begin{pmatrix} u \\ v \\ w \end{pmatrix} + \begin{pmatrix} 0 \\ 0 \\ \Gamma_1 w_{eq} \end{pmatrix}
$$
在许多情况下，例如原子与真空耦合，其平衡态是完全处于[基态](@entry_id:150928)，因此 $w_{eq} = -1$。这个[方程组](@entry_id:193238)是后续分析的基础，它描述了[布洛赫矢量](@entry_id:144181)在驱动和耗散共同作用下的平均动力学行为。

### [稳态解](@entry_id:200351)与饱和效应

当原子与光场的相互作用达到动态平衡时，[布洛赫矢量](@entry_id:144181)的各分量将不再随时间变化，即达到**[稳态](@entry_id:182458) (steady state)**。通过令 OBEs 中的时间导数为零，我们可以求解出[稳态解](@entry_id:200351)。

以共振驱动（$\Delta=0$）为例，我们来探讨[激发态](@entry_id:261453)布居数 $\rho_{ee} = (w+1)/2$ 如何随驱动强度 $\Omega$ 变化。从[稳态](@entry_id:182458) OBEs 出发：
$$
\begin{aligned}
0 = -\Gamma_2 u \\
0 = -\Gamma_2 v - \Omega w \\
0 = \Omega v - \Gamma_1(w - w_{eq})
\end{aligned}
$$
若驱动场存在（$\Omega \neq 0$），则 $u_{ss} = 0$。联立后两个方程，可以解得[稳态](@entry_id:182458)[布居数反转](@entry_id:155020) $w_{ss}$。在原子与真空耦合的常见情况下（$w_{eq}=-1$），我们得到：
$$
w_{ss} = \frac{-\Gamma_1 \Gamma_2}{\Gamma_1 \Gamma_2 + \Omega^2}
$$
相应的，[激发态](@entry_id:261453)布居数为：
$$
\rho_{ee, ss} = \frac{w_{ss}+1}{2} = \frac{1}{2} \frac{\Omega^2}{\Gamma_1 \Gamma_2 + \Omega^2}
$$
这个表达式揭示了一个核心现象：**饱和 (saturation)**。当驱动很弱时（$\Omega^2 \ll \Gamma_1 \Gamma_2$），[激发态](@entry_id:261453)布居数与驱动光强的平方成正比，$\rho_{ee, ss} \approx \frac{\Omega^2}{2\Gamma_1 \Gamma_2}$。随着 $\Omega$ 的增加，布居数增长变缓。当驱动非常强时（$\Omega^2 \gg \Gamma_1 \Gamma_2$），布居数趋于一个极限值 $1/2$。这意味着强驱动使得原子在[基态](@entry_id:150928)和[激发态](@entry_id:261453)之间快速往返，导致两个能级的布居数趋于相等。

饱和现象的程度可以用**饱和参数 (saturation parameter)** $S$ 来量化。通常定义为 $S = \Omega^2 / (\Gamma_1 \Gamma_2)$。当 $S \sim 1$ 时，系统开始进入饱和区。有趣的是，我们可以从不同的角度定义饱和的特征点。例如，可以考察 $\rho_{ee}(\Omega)$ [曲线的曲率](@entry_id:267366)，其曲率达到极值的点也标志着系统从未饱和区到[饱和区](@entry_id:262273)的过渡。一个精巧的计算 [@problem_id:648881] 表明，对于共振驱动的情况，使 $\rho_{ee}(\Omega)$ 的[二阶导数](@entry_id:144508) $\frac{d^2\rho_{ee}}{d\Omega^2}$ 达到最小值的[拉比频率](@entry_id:154019) $\Omega_{peak}$ 满足 $\Omega_{peak}^2 = \Gamma_1 \Gamma_2$，这恰好对应于 $S=1$。

### 耗散与涨落的微观起源

[光学布洛赫方程](@entry_id:171131)中的弛豫速率 $\Gamma_1$ 和 $\Gamma_2$ 是唯象参数。要理解它们的物理来源，我们必须超越平均场图像，考虑原子与环境（[热库](@entry_id:143608)）的微观相互作用。环境不仅引起了能量耗散（体现为弛豫项），还引入了随机的量子涨落。将这些涨落项加入运动方程，就得到了**布洛赫-朗之万方程 (Bloch-Langevin Equations)**。

一个典型的[量子朗之万方程](@entry_id:191053)形式如下 [@problem_id:648787]：
$$
\frac{d}{dt}\hat{\sigma}^-(t) = (-i\omega_0 - \Gamma_2)\hat{\sigma}^-(t) + \hat{F}^-(t)
$$
这里的 $\hat{\sigma}^-$ 是原子的下降算符，$\Gamma_2$ 是我们熟悉的[退相干](@entry_id:145157)速率，而 $\hat{F}^-(t)$ 是一个**朗之万噪声算符 (Langevin noise operator)**。它是一个平均值为零的随机力，描述了[热库](@entry_id:143608)对原子的随机“踢动”。耗散（$\Gamma_2$）和涨落（$\hat{F}^-$）并非独立，而是由同一个微观相互作用引起，并通过**涨落-耗散定理 (fluctuation-dissipation theorem)** 紧密联系在一起。

下面我们探讨几种典型环境下弛豫速率的微观起源。

#### 真空环境与自发辐射

当原子处于电磁真空（温度 $T=0$ K）中时，唯一的耗散机制是**自发辐射 (spontaneous emission)**，即[激发态](@entry_id:261453)原子自发地发射一个[光子](@entry_id:145192)并回到[基态](@entry_id:150928)。这个过程的速率通常记为 $\Gamma$。自发辐射是一个不可逆的能量耗散过程，它贡献了纵向弛豫，即 $\Gamma_1 = \Gamma$。同时，任何[能级布居](@entry_id:197877)的改变都会破坏相干性。可以证明，一个布居衰减过程对横向弛豫的贡献是其速率的一半。因此，在纯自发辐射的情况下，$\Gamma_2 = \Gamma/2$。

#### 热辐射场：爱因斯坦系数

当原子处于温度为 $T$ 的[热辐射](@entry_id:145102)场中时，情况变得更加复杂。[热库](@entry_id:143608)中存在平均[光子](@entry_id:145192)数为 $\bar{n}_{th}(\omega_0) = [\exp(\frac{\hbar\omega_0}{k_B T}) - 1]^{-1}$ 的[光子](@entry_id:145192)。这些[光子](@entry_id:145192)可以诱导原子发生受激吸收（[基态](@entry_id:150928) $\to$ [激发态](@entry_id:261453)）和受激发射（[激发态](@entry_id:261453) $\to$ [基态](@entry_id:150928)）。

我们可以从微观速率方程出发，将其与宏观的布洛赫-[朗之万方程](@entry_id:144277)进行比较，从而建立深刻的联系 [@problem_id:648884]。考虑布居数 $p_e$ 和 $p_g$ 的变化率，它由三种基本过程决定：[自发辐射](@entry_id:140032)（速率 $A$）、[受激发射](@entry_id:150501)（速率 $B u(\omega_0)$）和受激吸收（速率 $B u(\omega_0)$），其中 $u(\omega_0)$ 是[热辐射](@entry_id:145102)场的能量密度。
$$
\frac{d p_e}{dt} = p_g B u(\omega_0) - p_e (A + B u(\omega_0))
$$
通过将 $p_e = (1+w)/2$ 和 $p_g = (1-w)/2$ 代入，我们可以得到[布居数反转](@entry_id:155020) $w$ 的[动力学方程](@entry_id:751029)。将其整理成布洛赫-朗之万方程的形式 $\dot{w} = -\gamma_\parallel (w - w_{eq})$，可以得到：
$$
\gamma_\parallel = A + 2B u(\omega_0)
$$
$$
w_{eq} = -\frac{A}{A + 2B u(\omega_0)}
$$
另一方面，通过更严格的[量子理论](@entry_id:145435)推导，可以得到 $\gamma_\parallel = A(1+2\bar{n}_{th})$ 和 $w_{eq} = -1/(1+2\bar{n}_{th})$。对比这两组表达式，我们立即得出一个重要关系：
$$
B u(\omega_0) = A \bar{n}_{th}(\omega_0)
$$
将普朗克黑体辐射定律 $u(\omega_0) = \frac{\hbar \omega_0^3}{\pi^2 c^3} \bar{n}_{th}(\omega_0)$ 代入，我们便能推导出爱因斯坦 $A$ 和 $B$ 系数之间的基本关系：
$$
\frac{A}{B} = \frac{\hbar \omega_0^3}{\pi^2 c^3}
$$
这个推导漂亮地展示了布洛赫-朗之万方程如何将宏观唯象参数与微观[量子跃迁](@entry_id:145857)过程联系起来。

#### [纯退相干](@entry_id:204036)：随机[频率调制](@entry_id:162932)

在某些情况下，横向弛豫速率 $\Gamma_2$ 会大于 $\Gamma_1/2$。这表明存在一种不改变[能级布居](@entry_id:197877)，但会破坏原子偶极矩相位信息的机制。这种机制被称为**[纯退相干](@entry_id:204036) (pure dephasing)**，其速率记为 $\gamma_{ph}$，使得 $\Gamma_2 = \Gamma_1/2 + \gamma_{ph}$。

[纯退相干](@entry_id:204036)的一个典型物理图像是原子跃迁频率的随机波动。例如，原子在[晶格](@entry_id:196752)中由于[声子](@entry_id:140728)碰撞，其周围的[电场](@entry_id:194326)环境会发生变化，从而导致其能级发生随机移动。我们可以用一个经典[随机过程](@entry_id:159502)来模拟这种效应 [@problem_id:648739]。假设[原子跃迁](@entry_id:158267)频率为 $\omega(t) = \omega_0 + \delta\omega(t)$，其中 $\delta\omega(t)$ 是一个平均值为零的随机噪声，其关联函数为 $\langle \delta\omega(t)\delta\omega(t') \rangle = \sigma^2 e^{-\gamma_c|t-t'|}$（[奥恩斯坦-乌伦贝克过程](@entry_id:140047)），$\sigma$ 是涨落幅度，$\tau_c = 1/\gamma_c$ 是关联时间。

在旋转频率为 $\omega_0$ 的[参考系](@entry_id:169232)中，下降算符的平均值演化由下式给出：
$$
\frac{d}{dt}\langle \tilde{\sigma}_-(t) \rangle = -i \langle \delta\omega(t) \tilde{\sigma}_-(t) \rangle
$$
通过对噪声进行平均，在[马尔可夫近似](@entry_id:192525)下（噪声关联时间 $\tau_c$ 远小于其引起的[退相干时间](@entry_id:154396)），可以推导出[相干性](@entry_id:268953)按指数衰减：
$$
\frac{d}{dt}\langle \tilde{\sigma}_-(t) \rangle = -\Gamma_{pd} \langle \tilde{\sigma}_-(t) \rangle
$$
其中[纯退相干](@entry_id:204036)速率为：
$$
\Gamma_{pd} = \frac{\sigma^2}{\gamma_c}
$$
这个结果直观地表明，更强（$\sigma$ 更大）或更慢（$\gamma_c$ 更小，即关联时间更长）的频率涨落会导致更快的退相干。

### 动力学与谱学特性

布洛赫-[朗之万方程](@entry_id:144277)的动力学特性由其[系统矩阵](@entry_id:172230)的[本征值](@entry_id:154894)决定。这些[本征值](@entry_id:154894)的实部决定了系统弛豫到[稳态](@entry_id:182458)的速率，而虚部则对应于系统[瞬态响应](@entry_id:165150)中的[振荡频率](@entry_id:269468)。

#### AC 斯塔克位移

当一个原子被失谐的光场驱动时，光场会“缀饰”原子能级，导致其有效跃迁频率发生改变。这种光致频移被称为 **AC 斯塔克位移 (AC Stark Shift)**。我们可以通过分析[布洛赫方程](@entry_id:153789)系统矩阵 $M$ 的[本征值](@entry_id:154894)来计算它 [@problem_id:648764]。
$$
M = \begin{pmatrix} -\Gamma_2  -\Delta  0 \\ \Delta  -\Gamma_2  -\Omega \\ 0  \Omega  -\Gamma_1 \end{pmatrix}
$$
在没有驱动场（$\Omega=0$）时，[本征值](@entry_id:154894)为 $\lambda_1^{(0)} = -\Gamma_1$ 和 $\lambda_{2,3}^{(0)} = -\Gamma_2 \pm i\Delta$。后两个[本征值](@entry_id:154894)描述了[原子相干性](@entry_id:191358)在失谐频率 $\Delta$ 附近[振荡](@entry_id:267781)并以速率 $\Gamma_2$ 衰减。

当引入弱驱动场时，我们可以用微扰理论计算[本征值](@entry_id:154894)的修正。对 $\lambda^{(0)} = -\Gamma_2 + i\Delta$ 的[一阶修正](@entry_id:155896) $\delta\lambda$ 的虚部即为 AC 斯塔克位移 $\delta_{AC}$。经过计算可得：
$$
\delta_{AC} = \text{Im}(\delta\lambda) = \frac{\Omega^2 \Delta}{\Delta^2 + 4(\Gamma_1 - \Gamma_2)^2}
$$
将 $\Gamma_1=\Gamma$ 和 $\Gamma_2 = \Gamma/2 + \gamma_{ph}$ 代入，得到：
$$
\delta_{AC} = \frac{\Omega^2 \Delta}{\Delta^2 + (\Gamma - 2\gamma_{ph})^2}
$$
这个结果表明，AC 斯塔克位移的大小与光强的平方成正比，符号与[失谐](@entry_id:148084) $\Delta$ 相同。蓝失谐光场（$\Delta > 0$）使原子跃迁频率增加，[红失谐](@entry_id:160023)光场（$\Delta  0$）则使其减小。

#### [共振荧光](@entry_id:195107)与莫洛三线谱

被强[激光](@entry_id:194225)场驱动的二能级原子发射的荧光[光谱](@entry_id:185632)是一个[量子光学](@entry_id:140582)的经典问题。在强驱动极限下（$\Omega \gg \Gamma$），荧光[光谱](@entry_id:185632)不再是单一的洛伦兹峰，而是分裂成三个峰，即著名的**莫洛三线谱 (Mollow Triplet)**。

[光谱](@entry_id:185632)的结构由原子偶极矩的两时间关联函数的[傅里叶变换](@entry_id:142120)决定。根据**[量子回归定理](@entry_id:186216) (Quantum Regression Theorem)**，这些关联函数的动力学行为与单时间[期望值](@entry_id:153208)的动力学行为遵循相同的演化方程。因此，[光谱](@entry_id:185632)的峰位和线宽信息就蕴含在[布洛赫方程](@entry_id:153789)的[本征值](@entry_id:154894)中。

考虑共振驱动（$\Delta=0$）的情况 [@problem_id:648746]。描述[相干性](@entry_id:268953) ($v$) 和布居数 ($w$) 涨落演化的子矩阵为：
$$
M_{sub} = \begin{pmatrix} -\frac{\Gamma}{2}  -\Omega \\ \Omega  -\Gamma \end{pmatrix}
$$
其[本征值](@entry_id:154894)为：
$$
\lambda_\pm = -\frac{3\Gamma}{4} \pm i \sqrt{\Omega^2 - (\frac{\Gamma}{4})^2} \approx -\frac{3\Gamma}{4} \pm i\Omega \quad (\text{for } \Omega \gg \Gamma)
$$
这两个复数[本征值](@entry_id:154894)直接给出了莫洛三线谱[旁瓣](@entry_id:270334)的信息：
- **虚部 $\pm \Omega$**：给出了两个旁瓣相对于中心频率 $\omega_L$ 的位置，分别位于 $\omega_L \pm \Omega$。
- **实部 $-3\Gamma/4$**：决定了旁瓣的衰减速率。衰减速率的[绝对值](@entry_id:147688)给出了[谱线](@entry_id:193408)的半高半宽 (HWHM)。

因此，莫洛三线谱旁瓣的半高半宽为 $3\Gamma/4$，其全宽半高 (FWHM) 为：
$$
\text{FWHM}_{\text{sideband}} = 2 \times \frac{3\Gamma}{4} = \frac{3\Gamma}{2}
$$
中心峰的宽度则与另一个[本征值](@entry_id:154894)（与 $u$ 分量相关的[本征值](@entry_id:154894) $\lambda = -\Gamma/2$）有关，其 FWHM 为 $\Gamma$。

### [量子涨落](@entry_id:154889)与关联

朗之万噪声项的存在意味着原子算符本身也成为了[随机过程](@entry_id:159502)，其值在平均值附近涨落。这些涨落的特性蕴含了深刻的[物理信息](@entry_id:152556)，可以通过计算多时间关联函数来揭示。

#### [量子回归定理](@entry_id:186216)与两时间关联

如前所述，**[量子回归定理](@entry_id:186216) (Quantum Regression Theorem, QRT)** 是计算两时间关联函数的核心工具。它指出，形如 $\langle \hat{A}(t_0) \hat{B}(t) \rangle$（对于 $t > t_0$）的关联函数，其关于时间 $t$ 的演化方程与单时间[期望值](@entry_id:153208) $\langle \hat{B}(t) \rangle$ 的演化方程相同。

作为一个基本应用，我们可以计算在[热平衡](@entry_id:141693)中原子的偶极-偶极关联函数 [@problem_id:648787]。原子算符 $\hat{\sigma}^-(t)$ 的演化由 $\frac{d}{dt}\hat{\sigma}^-(t) = (-i\omega_0 - \Gamma_2)\hat{\sigma}^-(t) + \hat{F}^-(t)$ 描述。根据 QRT，对于 $t>0$，关联函数 $\langle \hat{\sigma}^+(t)\hat{\sigma}^-(0) \rangle$ 遵循其[齐次方程](@entry_id:163650)：
$$
\frac{d}{dt} \langle \hat{\sigma}^+(t)\hat{\sigma}^-(0) \rangle = (i\omega_0 - \Gamma_2) \langle \hat{\sigma}^+(t)\hat{\sigma}^-(0) \rangle
$$
其解为 $\langle \hat{\sigma}^+(t)\hat{\sigma}^-(0) \rangle = \langle \hat{\sigma}^+(0)\hat{\sigma}^-(0) \rangle e^{(i\omega_0 - \Gamma_2)t}$。通过考虑 $t0$ 的情况并利用[平稳性](@entry_id:143776)，可以得到对称化的关联函数：
$$
\langle \{\hat{\sigma}^+(t), \hat{\sigma}^-(0)\} \rangle = e^{i\omega_0 t - \Gamma_2 |t|}
$$
这个函数描述了原子偶极矩的[相干性](@entry_id:268953)如何随时间衰减。它的[傅里叶变换](@entry_id:142120)即为原子的吸收谱，是一个中心在 $\omega_0$、宽度为 $\Gamma_2$ 的洛伦兹峰。

#### [光子统计](@entry_id:175965)与 $g^{(2)}(\tau)$

[原子荧光](@entry_id:170887)的[光子](@entry_id:145192)不是随机发射的，而是具有特定的时间关联。二阶强度关联函数 $g^{(2)}(\tau)$ 是衡量这种关联的工具，它正比于在时刻 $t$ 探测到一个[光子](@entry_id:145192)后，在时刻 $t+\tau$ 再次探测到一个[光子](@entry_id:145192)的条件概率。

对于单个二能级原子，一个关键的量子效应是**[光子反聚束](@entry_id:165214) (photon antibunching)**，即 $g^{(2)}(0) = 0$。这背后的物理图像是，当原子发射一个[光子](@entry_id:145192)后，它必然回到了[基态](@entry_id:150928)。要发射第二个[光子](@entry_id:145192)，它必须首先被[激光](@entry_id:194225)场重新激发，这个过程需要时间。因此，原子不可能在同一时刻连续发射两个[光子](@entry_id:145192)。

我们可以利用[布洛赫方程](@entry_id:153789)来计算完整的 $g^{(2)}(\tau)$ [@problem_id:648821]。其计算思想是：$g^{(2)}(\tau)$ 正比于原子在 $t=0$ 时刻被投影到[基态](@entry_id:150928)后，在 $\tau$ 时刻处于[激发态](@entry_id:261453)的概率 $P_{ee}(\tau)$。这意味着我们需要求解[布洛赫方程](@entry_id:153789)，但[初始条件](@entry_id:152863)是 $w(0) = -1$（原子在[基态](@entry_id:150928)）。在弱驱动、过阻尼条件下（$\Omega  \Gamma/4$），$g^{(2)}(\tau)$ 的解为：
$$
g^{(2)}(\tau) = 1 - e^{-\tfrac{3\Gamma\tau}{4}}\left[\cosh\left(\tfrac{\tau}{2}\sqrt{\tfrac{\Gamma^2}{4}-4\Omega^2}\right) + \frac{3\Gamma}{2\sqrt{\tfrac{\Gamma^2}{4}-4\Omega^2}}\sinh\left(\tfrac{\tau}{2}\sqrt{\tfrac{\Gamma^2}{4}-4\Omega^2}\right)\right]
$$
这个表达式清晰地显示了 $g^{(2)}(0)=0$，并且随着 $\tau$ 的增加，$g^{(2)}(\tau)$ 会[振荡](@entry_id:267781)并趋于[稳态](@entry_id:182458)值 1，这些[振荡](@entry_id:267781)被称为**[拉比振荡](@entry_id:137940) (Rabi oscillations)**。

#### 相干与[非相干散射](@entry_id:190180)

原子散射的光可以分为两个部分：**[相干散射](@entry_id:267724) (coherent scattering)** 和 **[非相干散射](@entry_id:190180) (incoherent scattering)**。[相干散射](@entry_id:267724)光的相位与入射[激光](@entry_id:194225)场锁定，它源于原子的平均偶极矩 $\langle \hat{\sigma}^- \rangle$ 的[振荡](@entry_id:267781)。[非相干散射](@entry_id:190180)光则具有随机相位，它源于偶极矩算符围绕其平均值的涨落 $\delta \hat{\sigma}^- = \hat{\sigma}^- - \langle \hat{\sigma}^- \rangle$。总的辐射功率 $P_{total}$ 是这两部分之和。

利用[布洛赫方程](@entry_id:153789)的[稳态解](@entry_id:200351)，我们可以计算出这两部分功率。例如，在弱驱动下，我们可以将[稳态解](@entry_id:200351)按 $\Omega$ 的幂次展开 [@problem_id:648751]。可以发现，相干部分 $P_{coh} \propto |\langle \hat{\sigma}^- \rangle|^2 \propto \Omega^2$，而非相干部分 $P_{incoh} = P_{total} - P_{coh}$ 则包含了更复杂的依赖关系。计算表明，驱动场的引入会改变[非相干散射](@entry_id:190180)的功率，其变化量 $\Delta P_{incoh}$ 取决于热库的性质（通过 $w_{eq}$）和弛豫速率。

#### 噪声关联与[扩散](@entry_id:141445)系数

[朗之万方程](@entry_id:144277)的理论框架提供了一个计算噪声算符与系统算符之间关联的方法。噪声的强度由**[扩散](@entry_id:141445)系数 (diffusion coefficients)** $D_{ij}$ 描述，它定义了不同朗之万力之间的关联，例如 $\langle \hat{F}_i(t) \hat{F}_j(t') \rangle \propto D_{ij} \delta(t-t')$。

一个重要的结论是，对于由真空耗散引起的噪声，系统算符与噪声的单时间关联可以被直接计算出来。例如，噪声与原子偶极矩的互关联为 [@problem_id:648877]：
$$
\text{Re}[\langle \hat{F}^+(t) \hat{\sigma}^-(t) \rangle_{\text{ss}}] = -\frac{\gamma}{2} \langle \hat{\sigma}^z \rangle_{\text{ss}}
$$
将之前求得的[稳态](@entry_id:182458)[布居数反转](@entry_id:155020) $\langle\hat\sigma^z\rangle_{\rm ss} = -\frac{\gamma^2}{\gamma^2+2\Omega^2}$ 代入，我们得到：
$$
\text{Re}[\langle \hat{F}^+(t) \hat{\sigma}^-(t) \rangle_{\text{ss}}] = \left(-\frac{\gamma}{2}\right) \left(-\frac{\gamma^2}{\gamma^2+2\Omega^2}\right) = \frac{\gamma^3}{2(\gamma^2+2\Omega^2)}
$$
这个结果深刻地体现了涨落-耗散定理：系统与噪声的关联强度，直接由耗散速率 $\gamma$ 和系统的状态 $\langle \hat{\sigma}^z \rangle_{\text{ss}}$ 决定。这再次强调了耗散和涨落是同一物理过程的两个密不可分的方面，它们共同主导着[开放量子系统](@entry_id:138632)的动力学。