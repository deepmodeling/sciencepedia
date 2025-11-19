## 引言
[电磁波](@entry_id:269629)是现代物理学和工程学的基石，而理解[电磁波](@entry_id:269629)的关键在于掌握其最基本的构成单元——单色平面波。尽管在现实世界中纯粹的单色平面波是一种理想化模型，但它为分析从无线电波到伽马射线等一切复杂电磁现象提供了无与伦比的理论框架。本文旨在填补从对[电磁波](@entry_id:269629)的宏观认识到对其微观机制深刻理解之间的鸿沟。

在接下来的章节中，你将系统地学习单色[平面波](@entry_id:189798)的完整图景。
*   **原理与机制** 章节将从麦克斯韦方程出发，详细剖析其数学形式、物理属性（如能量、动量和偏振）以及在不同介质中的传播行为。
*   **应用与跨学科联系** 章节将展示这些理论如何在光学、工程、相对论和量子物理等广阔领域中转化为实际技术和前沿研究。
*   最后，通过 **动手实践** 环节，你将有机会运用所学知识解决具体问题，巩固并深化你的理解。

## 原理与机制

继前一章对[电磁波](@entry_id:269629)的宏观介绍之后，本章将深入探讨其最基本、最重要的构件之一：**单色平面波 (monochromatic plane waves)**。通过剖析其数学形式、物理属性以及与物质的相互作用，我们将为其在光学、通信和等离子体物理等领域的广泛应用奠定坚实的理论基础。

### 单色[平面波](@entry_id:189798)的数学描述

从数学上讲，一个[波函数](@entry_id:147440) $\Psi(\vec{r}, t)$ 若要描述一个行进的单色[平面波](@entry_id:189798)，其形式必须满足特定的要求。首先，“[平面波](@entry_id:189798)”意味着在任意时刻 $t$，波的相位在所有垂直于特定传播方向的平面上是恒定的。这些等相位面是平面。“行进波”意味着这些等相位面会随着时间推移而移动，整个波形在空间中平移而不改变其形状。最后，“单色”意味着波动的频率是单一的，即波随时间和空间的[振荡](@entry_id:267781)是纯粹的正弦形式。

综合这些条件，一个沿 $z$ 轴传播的行进单色[平面波](@entry_id:189798)最普遍的数学形式为：
$$ \Psi(z, t) = A \cos(kz \mp \omega t + \phi_0) $$
其中 $A$ 是波的**振幅 (amplitude)**，$\phi_0$ 是初始相位。函数的核心变量是相位项 $(kz \mp \omega t)$。这个[线性组合](@entry_id:154743)确保了波形以速度 $v = \omega/k$ 沿 $z$ 轴传播（$kz - \omega t$ 对应正向传播，$kz + \omega t$ 对应负向传播）而保持形状不变。这里的 $k$ 是**[波数](@entry_id:172452) (wave number)**，与波长 $\lambda$ 的关系是 $k = 2\pi/\lambda$；$\omega$ 是**角频率 (angular frequency)**，与频率 $f$ 和周期 $T$ 的关系是 $\omega = 2\pi f = 2\pi/T$。

为了更清晰地理解这一概念，我们可以考察几种不同的函数形式 [@problem_id:1809094]。
例如，函数 $\Psi(z, t) = B \cos(kz + \omega t)$ 完全符合定义，它描述了一个沿 $-z$ 方向传播的单色平面波。
同样，一个形如 $\Psi(z, t) = D (\sin(kz - \omega t) + \cos(kz - \omega t))$ 的函数也代表一个行进单色平面波。利用[三角恒等式](@entry_id:165065)，我们可以将其重写为 $\sqrt{2}D \sin(kz - \omega t + \pi/4)$，这依然是具有单一频率和线性相位的[正弦波](@entry_id:274998)，只是振幅和初始相位有所不同。函数 $\Psi(z,t) = B \sin(kz+\omega t)$ 也能通过[三角恒等式](@entry_id:165065) $\sin(\alpha+\beta)=\sin\alpha\cos\beta+\cos\alpha\sin\beta$ 变换而来，因此也代表了一个行进单色[平面波](@entry_id:189798)。

与此相对，函数 $\Psi(z, t) = A \sin(kz) \cos(\omega t)$ 描述的则是一种不同的物理现象。利用积化和差公式，它可以分解为 $\frac{A}{2}[\sin(kz - \omega t) + \sin(kz + \omega t)]$。这清晰地表明，该函数是两个振[幅相](@entry_id:269870)同、频率相同但传播方向相反的行进波的**叠加 (superposition)**。这种叠加产生的是**[驻波](@entry_id:148648) (standing wave)**，其[波节和波腹](@entry_id:186674)的位置固定，能量不会净向前传播。

此外，并非所有依赖于 $(kz - \omega t)$ 的函数都是单色的。例如，[高斯波包](@entry_id:151158) $\Psi(z,t) = C \exp(-(kz - \omega t)^{2})$ 虽然是一个行进波，但它不是正弦形式，通过傅里葉分析可以发现它是由一系列不同频率的[正弦波](@entry_id:274998)叠加而成，因此不是单色的。同时，如果相位不是空间坐标的线性函数，例如 $\Psi(z,t) = A \sin(k z^{2} - \omega t)$，那么等相位面将不再是平面，因此它不代表一个平面波。

### 麦克斯韦方程与[平面波解](@entry_id:195230)

单色平面波之所以在物理学中占据核心地位，是因为它们是真空中[麦克斯韦方程组](@entry_id:150940)的基石解。在没有[电荷](@entry_id:275494)和电流的自由空间中 ($\rho=0, \vec{J}=0$)，[麦克斯韦方程组](@entry_id:150940)可以推导出[电场](@entry_id:194326) $\vec{E}$ 和[磁场](@entry_id:153296) $\vec{B}$ 都满足的[波动方程](@entry_id:139839)：
$$ \nabla^2 \vec{E} - \frac{1}{c^2}\frac{\partial^2 \vec{E}}{\partial t^2} = 0 $$
$$ \nabla^2 \vec{B} - \frac{1}{c^2}\frac{\partial^2 \vec{B}}{\partial t^2} = 0 $$
其中 $c = 1/\sqrt{\epsilon_0 \mu_0}$ 是[真空中的光速](@entry_id:272753)。

让我们验证一个通用的[平面波解](@entry_id:195230) $\vec{E}(\vec{r}, t) = \vec{E}_0 \cos(\vec{k} \cdot \vec{r} - \omega t)$ 是否满足波动方程。对其求导可得：
$\nabla^2 \vec{E} = -|\vec{k}|^2 \vec{E}$
$\frac{\partial^2 \vec{E}}{\partial t^2} = -\omega^2 \vec{E}$

代入波动方程，我们得到：
$$ (-|\vec{k}|^2 + \frac{\omega^2}{c^2}) \vec{E} = 0 $$
要使这个解对任意非零[电场](@entry_id:194326)都成立，括号内的表达式必须为零。这便给出了真空中[电磁波](@entry_id:269629)的**[色散关系](@entry_id:140395) (dispersion relation)**：
$$ |\vec{k}| = \frac{\omega}{c} \quad \text{或} \quad \omega = ck $$
这表明在真空中，所有频率的[电磁波](@entry_id:269629)都以相同的速度 $c$ 传播。

此外，[麦克斯韦方程组](@entry_id:150940)还对 $\vec{E}$ 和 $\vec{B}$ 场的方向和大小施加了严格的约束。由高斯定律 $\nabla \cdot \vec{E} = 0$ 和[高斯磁定律](@entry_id:182942) $\nabla \cdot \vec{B} = 0$ 可推导出，对于[平面波](@entry_id:189798)，[电场和磁场](@entry_id:261347)都必须垂直于传播方向 $\vec{k}$。也就是说，[电磁波](@entry_id:269629)是**横波 (transverse waves)**。
$$ \vec{k} \cdot \vec{E} = 0 \quad \text{and} \quad \vec{k} \cdot \vec{B} = 0 $$
[法拉第定律](@entry_id:149836) $\nabla \times \vec{E} = -\partial \vec{B}/\partial t$ 则揭示了 $\vec{E}$ 和 $\vec{B}$ 之间的相互关系。对于平面波，该定律简化为 $\vec{k} \times \vec{E} = \omega \vec{B}$。这表明 $\vec{B}$ 场不仅垂直于 $\vec{k}$，还垂直于 $\vec{E}$。因此，$\vec{E}$、$\vec{B}$ 和 $\vec{k}$ 三者构成了一个相互垂直的[右手系](@entry_id:166669)。其振幅之间的关系为 $E_0 = c B_0$。

我们可以通过一个具体例子来体会这些关系 [@problem_id:1593512]。假设一个沿 $z$ 轴传播的[平面波](@entry_id:189798)，其[磁场](@entry_id:153296)由 $\vec{B}(z, t) = -\hat{x} B_0 \sin(kz + \omega t + \phi_0)$ 给出。这是一个沿 $-z$ 方向传播的波。我们可以用[法拉第定律](@entry_id:149836) $\nabla \times \vec{E} = -\partial \vec{B}/\partial t$ 来求解对应的[电场](@entry_id:194326) $\vec{E}$。
$$ \frac{\partial \vec{B}}{\partial t} = -\hat{x} B_0 \omega \cos(kz + \omega t + \phi_0) $$
$$ \nabla \times \vec{E} = -\frac{\partial E_y}{\partial z}\hat{x} + \frac{\partial E_x}{\partial z}\hat{y} = \hat{x} B_0 \omega \cos(kz + \omega t + \phi_0) $$
比较 $\hat{x}$ 分量可知 $\partial E_y / \partial z = -B_0 \omega \cos(kz + \omega t + \phi_0)$。积分可得 $E_y = -\frac{\omega}{k} B_0 \sin(kz + \omega t + \phi_0)$。利用真空中的色散关系 $\omega = ck$，我们得到 $E_y = -c B_0 \sin(kz + \omega t + \phi_0)$。因此，$\vec{E}(z,t) = -\hat{y} c B_0 \sin(kz + \omega t + \phi_0)$。这个结果完美地展示了 $\vec{E}$ 和 $\vec{B}$ 的正交性，以及 $E_0=cB_0$ 的振幅关系。传播方向 $\hat{k}=-\hat{z}$，$\vec{E}$ 沿 $-\hat{y}$，$\vec{B}$ 沿 $-\hat{x}$，满足 $\vec{E} \times \vec{B}$ 指向传播方向。

这些场的基本性质直接决定了[电磁波](@entry_id:269629)与[带电粒子](@entry_id:160311)的相互作用。例如，考虑一个带[电荷](@entry_id:275494) $q$ 的粒子以速度 $\vec{v}$ 在[电磁波](@entry_id:269629)中运动，它将受到[洛伦兹力](@entry_id:145104) $\vec{F} = q(\vec{E} + \vec{v} \times \vec{B})$ 的作用 [@problem_id:1593482]。对于沿 $+z$ 方向传播的波，$\vec{B} = \frac{1}{c}(\hat{z} \times \vec{E})$。如果粒子也沿 $+z$ 方向运动，即 $\vec{v}=v_z \hat{z}$，那么[磁场](@entry_id:153296)力项为 $q(\vec{v} \times \vec{B}) = \frac{q v_z}{c} (\hat{z} \times (\hat{z} \times \vec{E})) = -\frac{q v_z}{c} \vec{E}$。总力为 $\vec{F} = q\vec{E} (1 - v_z/c)$。可见，力不仅取决于[电场](@entry_id:194326)，还受到粒子速度与光速之比的修正。

### 平面波的能量与动量

[电磁波](@entry_id:269629)不仅传递信息，还携带能量和动量。单位体积内的[电磁场能量](@entry_id:265463)，即**能量密度 (energy density)**，由[电场和磁场](@entry_id:261347)共同贡献：
$$ u = u_E + u_B = \frac{1}{2}\epsilon_0 E^2 + \frac{1}{2\mu_0} B^2 $$
对于在真空中传播的单色平面波，由于 $E=cB$ 和 $c^2=1/(\epsilon_0\mu_0)$，我们可以证明 $u_E = u_B$。即[电场和磁场](@entry_id:261347)携带的能量相等。因此，总能量密度可以写为 $u = \epsilon_0 E^2$。

能量的流动由**[坡印廷矢量](@entry_id:269386) (Poynting vector)** $\vec{S}$ 描述，它代表单位时间通过单位面积的能量，即能量流密度：
$$ \vec{S} = \frac{1}{\mu_0} (\vec{E} \times \vec{B}) $$
对于[平面波](@entry_id:189798)，$\vec{E}$ 和 $\vec{B}$ 相互垂直，所以 $|\vec{E} \times \vec{B}| = EB = E^2/c$。[坡印廷矢量](@entry_id:269386)的方向与传播方向 $\vec{k}$ 一致。
$$ \vec{S} = \frac{1}{\mu_0 c} E^2 \hat{k} = c \epsilon_0 E^2 \hat{k} = c u \hat{k} $$
这表明能量以光速 $c$ 沿着[波的传播](@entry_id:144063)方向流动。由于 $E$ 场是随时间[振荡](@entry_id:267781)的，$\vec{S}$ 也是瞬时变化的。在实验中，我们通常关心的是其[时间平均](@entry_id:267915)值，即**波的强度 (intensity)** $I$。
$$ I = |\langle \vec{S} \rangle| = \langle c \epsilon_0 E_0^2 \cos^2(\vec{k} \cdot \vec{r} - \omega t) \rangle $$
由于 $\langle \cos^2(\cdot) \rangle = 1/2$，我们得到：
$$ I = \frac{1}{2} c \epsilon_0 E_0^2 = \frac{c}{2\mu_0} B_0^2 $$

[电磁波](@entry_id:269629)不仅携带能量，还携带动量。单位体积内的动量密度为 $\vec{p} = \vec{S}/c^2$。当[电磁波](@entry_id:269629)被物体吸收或反射时，动量的转移会对物体产生力，这被称为**辐射压力 (radiation pressure)**。
考虑一个面积为 $A$ 的完美反射面，垂直入射的[电磁波](@entry_id:269629)被完全反射回来，动量的变化是入射动量的两倍。单位时间内的动量变化率就是力 $F$。因此，作用在帆上的压力 $P_{rad} = F/A$ 是入射动量流率的两倍，即 $P_{rad} = 2 |\vec{p}| c = 2 |\vec{S}|/c = 2I/c$。
这个原理是[太阳帆](@entry_id:273839)技术的基础。例如，通过测量[太阳帆](@entry_id:273839)受到的推力 $F$，我们可以反推出入射阳光的[磁场](@entry_id:153296)振幅 $B_0$ [@problem_id:1593509]。
由 $F = P_{rad} A = \frac{2IA}{c}$，可得 $I = \frac{Fc}{2A}$。
再结合 $I = \frac{1}{2} c^3 \epsilon_0 B_0^2$，联立两式可解得：
$$ B_0 = \sqrt{\frac{F}{A c^2 \epsilon_0}} $$
这优雅地将一个宏观可测的力与微观的场振幅联系起来。

### [电磁波的偏振](@entry_id:192074)

[电磁波](@entry_id:269629)的**偏振 (polarization)** 描述的是其横向[电场](@entry_id:194326)矢量 $\vec{E}$ 在传播过程中的[振荡](@entry_id:267781)轨迹。
*   **线偏振 (Linear Polarization):** 如果 $\vec{E}$ 矢量始终在一个固定的方向上[振荡](@entry_id:267781)，则称该波为[线偏振](@entry_id:273116)波。我们之前讨论的大多数例子，如 $\vec{E} = \hat{x} E_0 \cos(kz - \omega t)$，都属于[线偏振](@entry_id:273116)。

*   **[圆偏振](@entry_id:261702)和[椭圆偏振](@entry_id:270497) (Circular and Elliptical Polarization):** 当两个具有相同频率、在空间上正交的[线偏振](@entry_id:273116)波叠加，且它们之间存在相位差时，就会产生更复杂的偏振状态。
    
    考虑两个沿 $+z$ 方向传播的波：$\vec{E}_1 = \hat{x} E_0 \cos(kz - \omega t)$ 和 $\vec{E}_2 = \hat{y} E_0 \cos(kz - \omega t + \delta)$。合成[电场](@entry_id:194326)为 $\vec{E} = \vec{E}_1 + \vec{E}_2$。
    
    一个特别重要的情形是当相位差 $\delta = \pm \pi/2$ 时 [@problem_id:1809063]。例如，若 $\delta = \pi/2$，则 $\vec{E}_2 = \hat{y} E_0 \cos(kz - \omega t + \pi/2) = -\hat{y} E_0 \sin(kz - \omega t)$。
    总[电场](@entry_id:194326)为 $\vec{E}(z,t) = E_0 [ \hat{x}\cos(kz - \omega t) - \hat{y}\sin(kz - \omega t) ]$。
    在任意固定位置 $z$，随着时间 $t$ 的推移，$\vec{E}$ 矢量的末端会描绘出一个圆。这就是**[圆偏振波](@entry_id:200164) (circularly polarized wave)**。值得注意的是，该波的[电场](@entry_id:194326)振幅大小是恒定的：$|\vec{E}|^2 = E_0^2 (\cos^2 + \sin^2) = E_0^2$。因此，其[坡印廷矢量](@entry_id:269386)的大小也是恒定的 $S = c\epsilon_0 E_0^2$，其[时间平均](@entry_id:267915)值就是它本身，即 $I = c\epsilon_0 E_0^2$。这恰好是两个分量波强度之和 ($I = I_1 + I_2 = \frac{1}{2}c\epsilon_0 E_0^2 + \frac{1}{2}c\epsilon_0 E_0^2$)。

为了更方便地处理偏振和相位，物理学家引入了**复数表示法 (complex notation)**。我们将一个物理场 $\vec{E}(\vec{r}, t)$ 表示为一个复数场 $\tilde{\vec{E}}(\vec{r}, t) = \tilde{\vec{E}}_0 \exp(i(\vec{k} \cdot \vec{r} - \omega t))$ 的实部，即 $\vec{E} = \Re\{\tilde{\vec{E}}\}$。其中[复振幅](@entry_id:164138) $\tilde{\vec{E}}_0$ 包含了振幅和相位信息。

例如，一个沿 $z$ 轴传播、具有[椭圆偏振](@entry_id:270497)的[磁场](@entry_id:153296)可以写为 $\tilde{\vec{B}}(z, t) = (B_{x0} \hat{x} + i B_{y0} \hat{y}) \exp[i(kz - \omega t)]$ [@problem_id:1593510]。这里的[复振幅](@entry_id:164138) $\tilde{\vec{B}}_0 = B_{x0} \hat{x} + i B_{y0} \hat{y}$ 表明，$x$ 分量和 $y$ 分量之间存在 $\pi/2$ 的相位差，但它们的振幅 $B_{x0}$ 和 $B_{y0}$ 不一定相等，因此 $\vec{B}$ 矢量的末端会描绘一个椭圆。利用复数表示，计算[时间平均](@entry_id:267915)的物理量变得非常简便。例如，[时间平均](@entry_id:267915)的[坡印廷矢量](@entry_id:269386)可由下式计算：
$$ \langle \vec{S} \rangle = \frac{1}{2} \Re\{ \tilde{\vec{E}} \times \tilde{\vec{B}}^* \} $$
其中 $\tilde{\vec{B}}^*$ 是 $\tilde{\vec{B}}$ 的[复共轭](@entry_id:174690)。对于上述[磁场](@entry_id:153296)，对应的[电场](@entry_id:194326)为 $\tilde{\vec{E}} = c(\tilde{\vec{B}} \times \hat{z}) = c(iB_{y0}\hat{x} - B_{x0}\hat{y})\exp[i(kz - \omega t)]$。计算可得 $\tilde{\vec{E}} \times \tilde{\vec{B}}^* = c(B_{x0}^2 + B_{y0}^2)\hat{z}$。这是一个实数，因此
$$ \langle \vec{S} \rangle = \frac{c}{2\mu_0} (B_{x0}^2 + B_{y0}^2) \hat{z} $$
这再次表明总强度是各正交分量强度之和。

### [波的叠加](@entry_id:166456)：驻波

当我们研究波与界面的相互作用时，例如光从镜面反射，[波的叠加](@entry_id:166456)现象变得至关重要。如前所述，一个行进波与其反射波的叠加会形成[驻波](@entry_id:148648)。

让我们详细分析一个[线偏振](@entry_id:273116)波垂直入射到位于 $z=0$ 的部分反射面上的情况 [@problem_id:1593492]。入射波为 $\vec{E}_i = \hat{x} E_0 \cos(kz-\omega t)$，反射波为 $\vec{E}_r = \hat{x} r E_0 \cos(kz+\omega t)$，其中 $r$ 是[电场](@entry_id:194326)[振幅反射系数](@entry_id:171753)。在 $z \le 0$ 的区域，总[电场](@entry_id:194326)为：
$$ \vec{E} = \vec{E}_i + \vec{E}_r = \hat{x} E_0 [\cos(kz-\omega t) + r\cos(kz+\omega t)] $$
对应的总[磁场](@entry_id:153296)为：
$$ \vec{B} = \vec{B}_i + \vec{B}_r = \hat{y} \frac{E_0}{c} [\cos(kz-\omega t) - r\cos(kz+\omega t)] $$
注意反射波的[磁场](@entry_id:153296)方向因 $\vec{k} \times \vec{E} \propto \vec{B}$ 的关系而反转。

一个显著的特征是，在这种叠加场中，[电场能量密度](@entry_id:261497)和[磁场能量](@entry_id:267501)密度的 时间平均值通常不再相等。经过计算可得：
$$ \langle u_E \rangle = \frac{1}{4}\epsilon_0 E_0^2 [1 + r^2 + 2r \cos(2kz)] $$
$$ \langle u_B \rangle = \frac{1}{4}\epsilon_0 E_0^2 [1 + r^2 - 2r \cos(2kz)] $$
总能量密度 $\langle u \rangle = \langle u_E \rangle + \langle u_B \rangle = \frac{1}{2}\epsilon_0 E_0^2 (1+r^2)$ 不再是均匀的，而是呈现空间调制。更重要的是，$\langle u_E \rangle$ 和 $\langle u_B \rangle$ 的比值依赖于空间位置 $z$：
$$ \mathcal{R}(z) = \frac{\langle u_E \rangle}{\langle u_B \rangle} = \frac{1 + r^2 + 2r \cos(2kz)}{1 + r^2 - 2r \cos(2kz)} $$
仅当 $r=0$ (无反射，纯行进波) 时，$\mathcal{R}(z) = 1$。在其他情况下，能量在电场和磁场之间以空间周期性模式进行分配。例如，在 $z = -\lambda/6$ 处， $2kz = 2(2\pi/\lambda)(-\lambda/6) = -2\pi/3$，$\cos(2kz) = -1/2$。若[反射系数](@entry_id:194350) $r=1/3$，该比值为 $\mathcal{R} = (1+1/9-1/3)/(1+1/9+1/3) = 7/13$。这表明在此位置，[磁场](@entry_id:153296)平均能量密度大于[电场](@entry_id:194326)[平均能量](@entry_id:145892)密度。

### [色散介质](@entry_id:180771)中的[波包](@entry_id:154698)

到目前为止，我们的讨论主要集中在真空中，其色散关系 $\omega=ck$ 是线性的。然而，当[电磁波](@entry_id:269629)在介质（如玻璃、水或等离子体）中传播时，情况会变得更加复杂。介质的响应通常依赖于频率，导致色散关系变为[非线性](@entry_id:637147)函数 $\omega(k)$。这种现象称为**[色散](@entry_id:263750) (dispersion)**。

一个直接的后果是，不同频率的波以不同的速度传播。我们定义**相速度 (phase velocity)** $v_p = \omega/k$，它代表了等相位面的[传播速度](@entry_id:189384)。在[色散介质](@entry_id:180771)中，$v_p$ 是 $k$ (或 $\omega$) 的函数。

考虑一个由大量不同频率的平面波叠加而成的**[波包](@entry_id:154698) (wave packet)**，它在空间上是局域化的。这样的波包（例如一个光脉冲）整体移动的速度由**[群速度](@entry_id:147686) (group velocity)** 决定：
$$ v_g = \frac{d\omega}{dk} $$
群速度描述了[波包](@entry_id:154698)振幅包络的[传播速度](@entry_id:189384)，也即能量和信息传播的速度。

一个经典的例子是[电磁波](@entry_id:269629)在稀薄等离子体中的传播 [@problem_id:1809112]。其色散关系为：
$$ \omega^2 = \omega_p^2 + c^2 k^2 $$
其中 $\omega_p$ 是[等离子体频率](@entry_id:137429)，一个取决于电子密度的常数。从此关系式可知，只有当 $\omega > \omega_p$ 时，$k$才是实数，波才能在等离子体中传播。
相速度为 $v_p = \omega/k = c\sqrt{1 + (\omega_p/ck)^2}$，它总是大于光速 $c$。但这并不违反相对论，因为它不代表信息传播速度。
群速度可以通过对色散关系[微分](@entry_id:158718)得到：$2\omega d\omega = 2c^2 k dk$，所以 $v_g = d\omega/dk = c^2k/\omega$。将其表示为 $\omega$ 的函数：
$$ v_g = c \sqrt{1 - \frac{\omega_p^2}{\omega^2}} $$
群速度总是小于光速 $c$。当 $\omega \gg \omega_p$ 时，$v_g \approx c$；当 $\omega$ 接近 $\omega_p$ 时，$v_g$ 趋于零。这种频率依赖的[传播速度](@entry_id:189384)是天文学家利用[脉冲星](@entry_id:203514)信号探测[星际介质](@entry_id:150031)性质的基础。

这种通过将平面波代入其控制方程来获得[色散关系](@entry_id:140395)的方法非常普适。例如，在[量子场论](@entry_id:138177)中，描述质量为 $m_0$ 的标量[玻色子](@entry_id:138266)的[克莱因-戈登方程](@entry_id:153831)也允许[平面波解](@entry_id:195230)，但其[色散关系](@entry_id:140395)不同 [@problem_id:1809080]：
$$ \omega^2 = c^2 k^2 + \left(\frac{m_0 c^2}{\hbar}\right)^2 $$
这表明即使在真空中，有质量粒子的[德布罗意波](@entry_id:266512)也是[色散](@entry_id:263750)的。

### [各向异性介质](@entry_id:187796)中的传播

我们最后的讨论转向一个更高级的主题：[电磁波](@entry_id:269629)在**各向异性 (anisotropic)** 介质中的传播，例如许多晶体。在这些材料中，[介电常数](@entry_id:146714)不再是一个标量 $\epsilon$，而是一个张量 $\boldsymbol{\epsilon}$。因此，[电位移矢量](@entry_id:197092) $\vec{D}$ 和[电场](@entry_id:194326) $\vec{E}$ 之间的关系变为 $\vec{D} = \boldsymbol{\epsilon} \vec{E}$。

这一改变带来了深刻的物理后果。一个关键点是：$\vec{D}$ 和 $\vec{E}$ 通常不再平行。
回顾麦克斯韦方程，$\nabla \cdot \vec{D} = 0$ 意味着 $\vec{k} \cdot \vec{D} = 0$，即 $\vec{D}$ 垂直于传播方向。然而，由于 $\vec{E}$ 不与 $\vec{D}$ 平行，$\vec{E}$ 不再保证垂直于 $\vec{k}$。[电磁波](@entry_id:269629)可以是纵向和横向的混合模式。

另一个更重要的后果是[能量传播](@entry_id:202589)方向的改变。[坡印廷矢量](@entry_id:269386) $\vec{S}$ 正比于 $\vec{E} \times \vec{H}$（在非磁性材料中 $\vec{H}=\vec{B}/\mu_0$）。由于 $\vec{k}$ 垂直于 $\vec{D}$ 和 $\vec{B}$，而 $\vec{S}$ 垂直于 $\vec{E}$ 和 $\vec{B}$，当 $\vec{D}$ 和 $\vec{E}$ 不平行时，$\vec{k}$ 和 $\vec{S}$ 也将不平行。这意味着，**波的能量流方向（由 $\vec{S}$ 定义）可能不同于波的相速度方向（由 $\vec{k}$ 定义）**。

我们可以通过一个例子来量化这个效应 [@problem_id:1809101]。考虑一个非磁性晶体，其[介电张量](@entry_id:194185)在主轴[坐标系](@entry_id:156346)中是对角化的 $\epsilon_r = \text{diag}(\epsilon_{rx}, \epsilon_{ry}, \epsilon_{rz})$。一个 $\vec{E}$ 场和 $\vec{k}$ 矢量都位于 $xz$ 平面内的平面波在该晶体中传播。$\vec{k}$ 与 $z$ 轴夹角为 $\theta$。
由 $\vec{k} \cdot \vec{D} = 0$ 和 $\vec{D} = \epsilon_0 \boldsymbol{\epsilon_r} \vec{E}$，我们可以推导出 $\vec{E}$ 各分量之间的关系，进而确定 $\vec{E}$ 的方向。然后我们可以计算出 $\vec{D}$ 的方向。$\vec{E}$ 和 $\vec{D}$ 之间的夹角 $\alpha$ 就等于 $\vec{k}$ 和 $\vec{S}$ 之间的夹角。
经过推导，可以发现 $\vec{D}$ 的方向与 $\vec{k}$ 垂直，而 $\vec{E}$ 的方向则依赖于[介电常数](@entry_id:146714)的各向异性程度 $(\epsilon_{rz}/\epsilon_{rx})$ 和传播方向 $\theta$。当 $\epsilon_{rx} \ne \epsilon_{rz}$ 时，$\vec{E}$ 和 $\vec{D}$ 之间就会出现一个夹角 $\alpha$。例如，对于 $\epsilon_{rx}=2.25, \epsilon_{rz}=3.61$ 和 $\theta = 30^\circ$ 的情况，计算表明[能量流](@entry_id:142770)方向会偏离波矢方向约 $10.2^\circ$。这一现象，被称为“[坡印廷矢量](@entry_id:269386)走离”(Poynting vector walk-off)，在非线性光学和[晶体光学](@entry_id:191952)中具有极其重要的应用。

本章通过对单色[平面波](@entry_id:189798)的层层剖析，从其基本定义到在真空、[色散介质](@entry_id:180771)和[各向异性介质](@entry_id:187796)中的行为，我们构建了理解更复杂电磁现象的坚实基础。