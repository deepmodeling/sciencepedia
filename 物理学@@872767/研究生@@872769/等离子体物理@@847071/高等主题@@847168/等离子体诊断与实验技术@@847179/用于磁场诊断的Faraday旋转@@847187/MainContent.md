## 引言
[磁场](@entry_id:153296)在宇宙中无处不在，从[地球磁层](@entry_id:193878)到遥远的星系，它主宰着等离子体的行为。在寻求可控[核聚变](@entry_id:139312)能源的实验室中，精确控制和理解[磁场](@entry_id:153296)结构更是决定成败的关键。然而，直接深入高温、致密的等离子体内部测量[磁场](@entry_id:153296)是一项极具挑战性的任务。[法拉第旋转](@entry_id:158372)效应为我们提供了一种强大而优雅的非侵入式解决方案，通过分析一束光穿过等离子体后偏振状态的微小变化，来揭示内部[磁场](@entry_id:153296)的秘密。尽管原理简洁，但如何从一个积分的测量值准确反演出局域的[磁场](@entry_id:153296)信息，并处理各种复杂的物理效应，是研究人员必须解决的知识鸿沟。

本文旨在系统性地构建从第一性原理到前沿应用的完整知识框架。在“原理与机制”一章中，我们将深入剖析[法拉第旋转](@entry_id:158372)的物理起源，推导其核心数学描述，并探讨碰撞、热效应等实际因素如何修正理想模型。接下来，“应用与跨学科联系”一章将展示该技术在[磁约束聚变](@entry_id:180408)、天体物理乃至凝聚态物理等多个领域的广泛应用实例，突显其强大的通用性。最后，通过“动手实践”部分提供的计算练习，您将有机会亲手应用所学知识，巩固对[法拉第旋转](@entry_id:158372)诊断技术的理解和应用能力。

## 原理与机制

本章旨在深入探讨[法拉第旋转](@entry_id:158372)效应的物理原理与基本机制。在前一章介绍其作为一种重要的[等离子体诊断](@entry_id:189276)工具的背景之后，我们将从第一性原理出发，系统地构建[法拉第旋转](@entry_id:158372)的理论框架。我们将从单个电子在电[磁场中的运动](@entry_id:261998)入手，推导出等离子体作为一种介电媒质的宏观响应，进而揭示[法拉第旋转](@entry_id:158372)的起源。随后，我们将讨论该效应在实际诊断应用中的各种复杂情况，包括共振、碰撞、热效应以及[测量误差](@entry_id:270998)的来源。

### 等离子体的各向异性：[法拉第旋转](@entry_id:158372)的根源

[法拉第旋转](@entry_id:158372)的根本原因在于，[磁化等离子体](@entry_id:201225)对于[电磁波](@entry_id:269629)是一种**各向异性 (anisotropic)** 介质。这种各向异性源于外部[磁场](@entry_id:153296) $\mathbf{B}_0$ 对等离子体中电子运动的约束。当一个[电磁波](@entry_id:269629)穿过等离子体时，其[电场](@entry_id:194326) $\mathbf{E}_1$ 会驱动电子运动，从而产生电流 $\mathbf{J}_1$。然而，由于洛伦兹力 $\mathbf{v} \times \mathbf{B}_0$ 的存在，电子的速度响应 $\mathbf{v}_1$ 并不会简单地与驱动[电场](@entry_id:194326) $\mathbf{E}_1$ 共线。

为了定量描述这种响应，我们可以考察一个均匀冷电子等离子体，其中背景[磁场](@entry_id:153296)为 $\mathbf{B}_0 = B_0 \hat{\mathbf{z}}$。电子的动力学行为由线性化的[弗拉索夫方程](@entry_id:161066)或等效的流体动量方程描述。对于一个频率为 $\omega$ 的时谐[电场](@entry_id:194326)扰动 $\mathbf{E}_1 e^{-i\omega t}$，线性化的电子动量方程为：
$$
m_e \frac{\partial \mathbf{v}_1}{\partial t} = -e(\mathbf{E}_1 + \mathbf{v}_1 \times \mathbf{B}_0)
$$
其中 $m_e$ 和 $-e$ 分别是电子的质量和[电荷](@entry_id:275494)。假设速度响应也具有时谐形式 $\mathbf{v}_1 e^{-i\omega t}$，上式变为：
$$
-i m_e \omega \mathbf{v}_1 = -e(\mathbf{E}_1 + \mathbf{v}_1 \times B_0 \hat{\mathbf{z}})
$$
将此矢量方程在垂直于[磁场](@entry_id:153296)的平面（$xy$ 平面）内展开，我们得到一个关于速度分量 $v_x$ 和 $v_y$ 的[方程组](@entry_id:193238)：
$$
\begin{align*}
-i m_e \omega v_x = -e E_x - e v_y B_0 \\
-i m_e \omega v_y = -e E_y + e v_x B_0
\end{align*}
$$
这个[方程组](@entry_id:193238)清楚地显示了 $x$ 和 $y$ 方向运动的耦合。$x$ 方向的[电场](@entry_id:194326)不仅驱动 $x$ 方向的速度，还通过洛伦兹力间接影响 $y$ 方向的速度，反之亦然。

通过求解这个[线性方程组](@entry_id:148943)，我们可以得到电子速度与[电场](@entry_id:194326)分量之间的关系。进而，我们可以计算出等离子体的线性电流响应 $\mathbf{J}_1 = -n_e e \mathbf{v}_1$，并根据[欧姆定律](@entry_id:276027)的张量形式 $\mathbf{J}_1 = \boldsymbol{\sigma} \cdot \mathbf{E}_1$ 确定**[电导率张量](@entry_id:155827) (conductivity tensor)** $\boldsymbol{\sigma}$。特别地，负责耦合的非对角项 $\sigma_{xy}$（定义为 $J_x = \sigma_{xx}E_x + \sigma_{xy}E_y$）可以被推导出来 [@problem_id:256449]。在定义了**[电子等离子体频率](@entry_id:197401) (electron plasma frequency)** $\omega_p = \sqrt{n_e e^2 / (\epsilon_0 m_e)}$ 和**[电子回旋频率](@entry_id:203398) (electron cyclotron frequency)** $\omega_c = e B_0 / m_e$ 后，我们得到：
$$
\sigma_{xy} = \epsilon_0 \frac{\omega_p^2 \omega_c}{\omega^2 - \omega_c^2}
$$
这个非零的非对角项 $\sigma_{xy}$ 是等离子体**[旋光性](@entry_id:139326) (gyrotropy)** 的直接体现，也是[法拉第旋转](@entry_id:158372)等[磁光效应](@entry_id:262395)的微观物理基础。[电导率张量](@entry_id:155827)与**[介电张量](@entry_id:194185) (dielectric tensor)** $\boldsymbol{\epsilon}$ 直接相关，关系为 $\boldsymbol{\epsilon} = \epsilon_0 \mathbf{I} + i \boldsymbol{\sigma} / \omega$，因此[介电张量](@entry_id:194185)同样具有非对角项，从而导致了介质的各向异性。

### [圆偏振](@entry_id:261702)[本征模](@entry_id:174677)与[折射率](@entry_id:168910)

在由[磁场](@entry_id:153296)引起的[各向异性介质](@entry_id:187796)中，沿[磁场](@entry_id:153296)方向传播的波的**本征模 (eigenmodes)** 不再是[线偏振](@entry_id:273116)波，而是**[圆偏振波](@entry_id:200164) (circularly polarized waves)**。具体来说，存在两种模式：**右旋圆偏振波 (Right-hand Circularly Polarized, RCP)** 和**左旋[圆偏振波](@entry_id:200164) (Left-hand Circularly Polarized, LCP)**。这两种模式在等离子体中传播时，会感受到不同的[介电常数](@entry_id:146714)，因此具有不同的[折射率](@entry_id:168910)。

对于沿[磁场](@entry_id:153296) $\mathbf{B}_0 = B_0 \hat{\mathbf{z}}$ 方向传播的波，RCP 和 LCP 模式的[折射率](@entry_id:168910) $N_R$ 和 $N_L$ 由著名的 Appleton-Hartree [色散关系](@entry_id:140395)给出：
$$
N_{R,L}^2 = 1 - \frac{\omega_{pe}^2}{\omega(\omega \mp \omega_{ce})}
$$
此处的负号（$-$）对应于 RCP 波，正号（$+$）对应于 LCP 波。从物理上看，RCP 波的[电场](@entry_id:194326)矢量旋转方向与电子在[磁场](@entry_id:153296)中的回旋运动方向相同，而 LCP 波则相反。

### [法拉第旋转](@entry_id:158372)现象的形成

一个线偏振波可以被数学上分解为两个等幅度的、旋向相反的[圆偏振波](@entry_id:200164)的叠加。当这个[线偏振](@entry_id:273116)波入射到磁化等离子体中时，它会分解为 RCP 和 LCP 两个本征模。由于 $N_R \neq N_L$，这两个分量将以不同的**相速度 (phase velocity)** $v_p = c/N$ 传播。

随着波的传播，RCP 和 LCP 分量之间会逐渐累积一个相位差。在传播距离 $z$ 后，这个相位差为 $\Delta \psi = (k_L - k_R)z$，其中 $k_{L,R} = (\omega/c)N_{L,R}$ 是各自的波数。当这两个圆偏振分量在 $z$ 点重新叠加时，它们合成的线偏振[波的偏振](@entry_id:262733)平面相对于初始方向旋转了一个角度 $\phi(z)$。这个旋转角恰好是相位差的一半，$\phi(z) = \Delta \psi / 2$。

因此，单位传播距离上的[偏振旋转](@entry_id:188808)角，即**[法拉第旋转](@entry_id:158372)率 (Faraday rotation rate)**，可以表示为：
$$
\frac{d\phi}{dz} = \frac{1}{2}(k_L - k_R) = \frac{\omega}{2c}(N_L - N_R)
$$
这是描述[法拉第旋转](@entry_id:158372)现象的核心方程 [@problem_id:256372] [@problem_id:256507] [@problem_id:256342]。

在许多诊断应用中，探测波的频率 $\omega$ 远高于等离子体中的特征频率，即 $\omega \gg \omega_{pe}$ 和 $\omega \gg \omega_{ce}$。在这个**[高频近似](@entry_id:750288) (high-frequency approximation)**下，我们可以对[折射率](@entry_id:168910)表达式进行[泰勒展开](@entry_id:145057)。$N_{R,L}$ 近似为：
$$
N_{R,L} \approx 1 - \frac{\omega_{pe}^2}{2\omega^2} \left(1 \pm \frac{\omega_{ce}}{\omega}\right)
$$
代入旋转率公式，我们得到一个极为重要的简化结果：
$$
\frac{d\phi}{dz} \approx \frac{\omega}{2c} \left( \frac{\omega_{pe}^2 \omega_{ce}}{\omega^3} \right) = \frac{e^3}{2\epsilon_0 m_e^2 c} \frac{n_e B_\parallel}{\omega^2}
$$
这里 $B_\parallel$ 是[磁场](@entry_id:153296)沿传播方向的分量（在此例中为 $B_0$）。这个公式表明，在高频极限下，[法拉第旋转](@entry_id:158372)率正比于电子密度 $n_e$ 和平行[磁场](@entry_id:153296)分量 $B_\parallel$ 的乘积。这构成了利用[法拉第旋转](@entry_id:158372)进行[等离子体诊断](@entry_id:189276)的理论基础。

### 积分测量及其应用

在实际的诊断实验中，我们测量的是[激光](@entry_id:194225)束穿过整个等离子体后累积的**总旋转角 (total rotation angle)** $\phi_{total}$。这个总角度是局部旋转率沿着光束路径 $L$ 的线积分：
$$
\phi_{total} = \int_0^L \frac{d\phi}{dz} dz \propto \int_0^L n_e(z) B_\parallel(z) dz
$$
这意味着[法拉第旋转](@entry_id:158372)测量提供的是 $n_e B_\parallel$ 乘积的路径积分值。如果等离子体的密度和[磁场](@entry_id:153296)沿路径是变化的，例如在一个具有特定剖面的[等离子体柱](@entry_id:194522)中，我们需要对 $n_e(z)$ 和 $B_\parallel(z)$ 的乘积进行积分才能得到总旋转角 [@problem_id:256507]。通过测量 $\phi_{total}$，并结合来自其他诊断（如[干涉仪](@entry_id:261784)测量得到的密度剖面 $\int n_e dz$）的信息，研究人员就可以解译出关于等离子体内部[磁场](@entry_id:153296)结构的关键信息。

### 模型修正与复杂效应

简单的冷、无碰撞、高频模型为理解[法拉第旋转](@entry_id:158372)提供了清晰的物理图像，但真实等离子体要复杂得多。本节将探讨一些重要的修正和效应。

#### 波的共振

当探测波频率 $\omega$ 接近[电子回旋频率](@entry_id:203398) $\omega_{ce}$ 时，[高频近似](@entry_id:750288)不再成立。从[折射率](@entry_id:168910)表达式 $N_R^2 = 1 - \frac{\omega_{pe}^2}{\omega(\omega - \omega_{ce})}$ 可以看出，当 $\omega \to \omega_{ce}$ 时，$N_R^2$ 会趋向无穷大（在无碰撞模型中）。这意味着 RCP 波发生了**共振 (resonance)**。物理上，这是因为波的[电场](@entry_id:194326)以与电子相同的回旋频率旋转，能够持续地将[能量传递](@entry_id:174809)给电子。

这种共振导致[法拉第旋转](@entry_id:158372)率在 $\omega$ 趋近 $\omega_{ce}$ 时表现出奇异行为。由于 $N_R$ 发散而 $N_L$ 保持有限，旋转率 $\frac{d\phi}{dz} \approx -\frac{\omega}{2c}N_R$ 将会发散。通过仔细分析其渐近行为，可以发现旋转率与 $(\omega_{ce}-\omega)^{-1/2}$ 成正比 [@problem_id:256372]。这种强烈的频率依赖性在某些特定的诊断方案（如[回旋共振](@entry_id:139685)吸收）中具有重要应用。

#### 碰撞效应

在真实等离子体中，电子会与离子和中性粒子发生**碰撞 (collisions)**。碰撞起到一种阻尼或摩擦的作用，可以从电子的[动量方程](@entry_id:197225)中引入一个碰撞项 $-m_e \nu \mathbf{v}_e$ 来描述，其中 $\nu$ 是有效[碰撞频率](@entry_id:138992)。

引入碰撞后，[介电常数](@entry_id:146714)和[折射率](@entry_id:168910)都将变为复数。例如，LCP 和 RCP 模式的介电函数变为：
$$
\epsilon_{R,L} = 1 - \frac{\omega_{pe}^2}{\omega(\omega + i\nu \mp \omega_{ce})}
$$
[折射率](@entry_id:168910) $N = \sqrt{\epsilon}$ 的实部决定相速度，而虚部则描述波的**衰减 (damping)** 或吸收。对于[法拉第旋转](@entry_id:158372)，我们关心的是[折射率](@entry_id:168910)实部的差异。在考虑碰撞后，旋转率的表达式变得更加复杂 [@problem_id:256313]：
$$
\Theta = \frac{\omega}{2c} \text{Re}(N_R - N_L) = \frac{\omega_{pe}^2 \omega_{ce}}{2c} \frac{\omega^2 - \omega_{ce}^2 - \nu^2}{(\omega^2 - \omega_{ce}^2 - \nu^2)^2 + 4\omega^2\nu^2}
$$
一个重要的结果是，碰撞消除了在 $\omega = \omega_{ce}$ 处的奇异性。旋转率在共振点附近达到一个峰值，但保持有限，其宽度与碰撞频率 $\nu$ 有关。

#### 热效应

**[冷等离子体](@entry_id:204266) (cold plasma)** 模型假设电子没有热运动（$T_e=0$）。对于**热等离子体 (warm plasma)**，电子具有一定的速度[分布](@entry_id:182848)（通常是麦克斯韦[分布](@entry_id:182848)），这会引入新的物理效应。在基于[弗拉索夫方程](@entry_id:161066)的动理学模型中，热效应通过波与粒子相互作用中的多普勒频移项 $k v_z$ 体现。

对于沿[磁场](@entry_id:153296)传播的波，考虑热效应后，[折射率](@entry_id:168910)表达式中的分母变为对速度[分布](@entry_id:182848)的积分，例如 $\int dv_z \frac{f_{0z}(v_z)}{\omega - k v_z \mp \omega_{ce}}$。在热效应较弱（即电子[热速度](@entry_id:755900) $v_{th}$ 远小于波的相速度）的情况下，可以对该积分进行展开，得到对[冷等离子体](@entry_id:204266)结果的修正。[法拉第旋转](@entry_id:158372)率的**一阶热修正 (leading-order thermal correction)** 项与 $v_{th}^2$ 成正比 [@problem_id:256342]。例如，在高频极限下，热修正项为：
$$
\left(\frac{d\phi}{dz}\right)_{th} = \frac{3 \omega_{pe}^2 \omega_{ce} v_{th}^2}{2 c^3 \omega^2}
$$
其中 $v_{th} = \sqrt{k_B T_e / m_e}$。这表明在高温等离子体中，尤其是在诊断波频率不那么高的情况下，必须考虑温度对[法拉第旋转](@entry_id:158372)测量的影响。

#### 群速度与脉冲传播

[法拉第旋转](@entry_id:158372)角由相速度的差异决定。然而，如果使用短[激光](@entry_id:194225)**脉冲 (pulse)** 进行诊断，那么脉冲包络的传播是由**[群速度](@entry_id:147686) (group velocity)** $v_g = (dk/d\omega)^{-1}$ 决定的。由于[折射率](@entry_id:168910) $N(\omega)$ 是频率的函数（即介质是[色散](@entry_id:263750)的），[群速度](@entry_id:147686)通常不等于相速度。

由于 RCP 和 LCP 模式的[色散关系](@entry_id:140395)不同，它们的[群速度](@entry_id:147686) $v_{g,R}$ 和 $v_{g,L}$ 也不同。这意味着，一个初始的线偏振脉冲在穿过等离子体后，其 RCP 和 LCP 成分不仅会产生[相位偏移](@entry_id:276073)，还会在时间上发生分离。它们到达探测器的时间会有微小的差异 $\Delta t = |t_R - t_L| = L|v_{g,R}^{-1} - v_{g,L}^{-1}|$。这个到达时间差本身也是一种可测量的量，它同样依赖于[等离子体参数](@entry_id:195285) [@problem_id:256296]。在[高频近似](@entry_id:750288)下，这个时间差为：
$$
\Delta t = \frac{2 L \omega_p^2 \omega_{ce}}{c \omega^3}
$$
这种效应被称为[群延迟](@entry_id:267197)[双折射](@entry_id:167246)，是磁化等离子体各向异性的另一种表现。

### 实际测量中的挑战

将[法拉第旋转](@entry_id:158372)应用于实际诊断时，会遇到一系列挑战，这些挑战可能导致测量误差或需要更复杂的分析模型。

#### 横向[磁场](@entry_id:153296)的影响：[Cotton-Mouton效应](@entry_id:197284)

[法拉第效应](@entry_id:202412)是由平行于波传播方向的[磁场](@entry_id:153296) $B_\parallel$ 引起的。然而，垂直于传播方向的[磁场](@entry_id:153296)分量 $B_\perp$ 也会影响[波的偏振](@entry_id:262733)，这种效应称为**[Cotton-Mouton效应](@entry_id:197284) (Cotton-Mouton effect)**。它是一种**线性[双折射](@entry_id:167246) (linear birefringence)**，即偏振平行于 $B_\perp$ 和垂直于 $B_\perp$ 的[电场](@entry_id:194326)分量会以不同的相速度传播。

[法拉第效应](@entry_id:202412)（[圆双折射](@entry_id:175692)）使线[偏振旋转](@entry_id:188808)，而 Cotton-Mouton 效应（线性双折射）则会使线偏振波变为[椭圆偏振](@entry_id:270497)波。在许多实验中，比如[托卡马克](@entry_id:182005)中的垂直弦测量，探测光束垂直穿过强大的[环向磁场](@entry_id:756057) $B_T$（即 $B_\perp$ 很大），同时试图测量微弱的极向[磁场](@entry_id:153296) $B_p$（即 $B_\parallel$ 很小）。在这种情况下，Cotton-Mouton 效应可能非常显著，它产生的偏振椭圆化会被一个简单的[旋光](@entry_id:201162)仪错误地解读为[偏振旋转](@entry_id:188808)，从而产生一个虚假的**“表观旋转角” (apparent rotation angle)**，严重污染对 $B_p$ 的测量 [@problem_id:256247]。这个系统误差通常与 $B_T^2$ 和入射偏振角有关。

#### 综合效应与[斯托克斯矢量](@entry_id:168374)形式

当[法拉第效应](@entry_id:202412)和 Cotton-Mouton 效应同时存在，并且[磁场](@entry_id:153296)方向沿路径变化时（例如在具有磁剪切的聚变等离子体中），偏振态的演化会变得非常复杂。描述这种演化的最通用和最强大的工具是**[斯托克斯矢量](@entry_id:168374) (Stokes vector)** $\mathbf{S} = (\mathcal{Q}, \mathcal{U}, \mathcal{V})^T$ 和[庞加莱球](@entry_id:265729)。

偏振态沿传播路径 $z$ 的演化由一个旋进方程描述：
$$
\frac{d\mathbf{S}}{dz} = \mathbf{\Omega}(z) \times \mathbf{S}(z)
$$
其中，**旋进矢量 (precession vector)** $\mathbf{\Omega}(z)$ 由介质性质决定。其 $z$ 分量 $\Omega_z$ (或 $\rho_V$) 代表[法拉第旋转](@entry_id:158372)率，与 $B_\parallel$ 成正比。其横向分量 $(\Omega_x, \Omega_y)$ (或 $\rho_L$) 代表 Cotton-Mouton 效应的强度和方向，与 $B_\perp^2$ 成正比。

这个方程描述了[斯托克斯矢量](@entry_id:168374)在[庞加莱球](@entry_id:265729)面上绕着旋进矢量 $\mathbf{\Omega}$ 的旋转。即使对于复杂的[磁场](@entry_id:153296)结构，如螺旋[磁场](@entry_id:153296)，只要 $\mathbf{\Omega}(z)$ 已知，原则上也可以求解这个方程，从而精确追踪偏振态的演化，并将[法拉第效应](@entry_id:202412)和 Cotton-Mouton 效应分离开来 [@problem_id:256493]。

#### [等离子体湍流](@entry_id:186467)的影响

真实的等离子体很少是完全均匀和静止的。密度、温度和[磁场](@entry_id:153296)的**[湍流](@entry_id:151300)涨落 (turbulent fluctuations)** 是普遍存在的。当探测光束穿过[湍流](@entry_id:151300)等离子体时，沿路径的电子密度 $n_e(z)$ 是一个随机变化的量。

由于[法拉第旋转](@entry_id:158372)角是 $n_e(z)$ 的积分，[密度涨落](@entry_id:143540) $\delta n_e(z)$ 会导致测得的总旋转角 $\phi_{total}$ 出现随机涨落。这个涨落的统计特性，例如其**[方差](@entry_id:200758) (variance)** $\sigma^2_{\Delta\phi}$，取决于[湍流](@entry_id:151300)的统计性质，如涨落的[均方根值](@entry_id:276804) $\sigma_n$ 和**关联长度 (correlation length)** $\lambda_c$。通过计算，可以得到旋转角[方差](@entry_id:200758)与这些[湍流](@entry_id:151300)参数之间的关系 [@problem_id:256267]。例如，对于具有指数关联函数的[密度涨落](@entry_id:143540)，[方差](@entry_id:200758)为：
$$
\sigma^2_{\Delta\phi} = 2 K^{2}B_{0}^{2}\sigma_{n}^{2}\lambda_{c}\left(L-\lambda_{c}\bigl(1-e^{-L/\lambda_{c}}\bigr)\right)
$$
这一结果一方面表明[湍流](@entry_id:151300)是[法拉第旋转](@entry_id:158372)测量的一个噪声来源，限制了测量的精度；另一方面，通过分析旋转角的涨落信号，也可以反过来诊断等离子体中的密度[湍流](@entry_id:151300)特性。

### 极端物理条件下的[法拉第效应](@entry_id:202412)

在极端物理条件下，例如[中子星](@entry_id:147259)或磁星周围的超强[磁场](@entry_id:153296)环境中，连真空本身都会表现出[非线性电动力学](@entry_id:275004)行为。根据**[量子电动力学](@entry_id:150740) (Quantum Electrodynamics, QED)**，强[磁场](@entry_id:153296)可以极化真空，使其表现得像一个介电媒质。

当[电磁波](@entry_id:269629)穿过这种同时含有等离子体和强[磁场](@entry_id:153296)的区域时，[真空极化](@entry_id:153495)效应会与等离子体响应相互作用。在超强[磁场](@entry_id:153296)（$B_0 \gg B_{cr}$，其中 $B_{cr} = m_e^2 c^2 / (e\hbar)$ 是[施温格临界场](@entry_id:184457)）的极限下，一个主要的 QED 效应是**屏蔽 (screening)** 等离子体的[介电响应](@entry_id:140146)。这可以被模型化为将等离子体的[磁化率张量](@entry_id:751635) $\boldsymbol{\chi}_p$ 除以一个与[磁场强度](@entry_id:197932)相关的修正因子 $1+\lambda$。

这种[屏蔽效应](@entry_id:136974)会直接修正[法拉第旋转](@entry_id:158372)率。修正后的大小 $K_{QED}$ 会小于没有 QED 效应时的 $K_0$。其相对变化 $(K_{QED} - K_0)/K_0$ 直接依赖于描述[真空极化](@entry_id:153495)强度的因子 $\lambda$ [@problem_id:256321]。这展示了[法拉第旋转](@entry_id:158372)作为一个诊断工具，其[适用范围](@entry_id:636189)可以从实验室等离子体一直延伸到探索天体物理环境中基本物理定律的前沿领域。