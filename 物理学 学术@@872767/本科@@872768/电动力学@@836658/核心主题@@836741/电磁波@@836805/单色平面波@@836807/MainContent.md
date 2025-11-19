## 引言
单色[平面波](@entry_id:189798)是电动力学乃至整个物理学中最为基础和重要的概念之一。作为麦克斯韦方程组最简单的波动解，它不仅完美描述了光在真空中的传播，也构成了理解更复杂电磁现象（如波包、衍射和散射）的理论基石。然而，从抽象的数学表达式到对其物理内涵——如[能量流](@entry_id:142770)动、偏振特性和实际应用——的深刻把握，之间存在着一条需要系统学习才能跨越的鸿沟。

本篇文章旨在填补这一鸿沟，为读者构建一幅关于单色[平面波](@entry_id:189798)的完整图景。在“**原理与机制**”一章中，我们将从[波动方程](@entry_id:139839)出发，详细剖析单色平面波的数学定义、横波结构、能量动量属性，以及偏振和[驻波](@entry_id:148648)等叠加效应。接着，在“**应用与跨学科联系**”一章里，我们将展示这些基本原理如何在[光学工程](@entry_id:272219)、天体物理、原子物理乃至相对论等多个领域中发挥关键作用，揭示理论与实践的紧密联系。最后，“**动手实践**”部分提供了一系列精心设计的问题，旨在通过计算和分析，帮助读者巩固和深化对核心概念的理解。

通过这三个层次的递进学习，读者将能够全面掌握单色[平面波](@entry_id:189798)的理论精髓，并理解其在现代科技与前沿科学中的核心地位。现在，让我们首先进入“原理与机制”的学习，从最基本的定义开始，揭开单色[平面波](@entry_id:189798)的神秘面纱。

## 原理与机制

本章在前一章介绍的基础上，深入探讨单色平面波的数学描述、内在结构及其物理性质。我们将从[波动方程](@entry_id:139839)最基本的解出发，系统地构建起电磁[平面波](@entry_id:189798)的完整理论图像，并探索其能量、动量、偏振以及在不同条件下叠加的丰富现象。

### 单色平面波的数学描述

#### 定义[平面波](@entry_id:189798)

在不含源的线性、均匀、各向同性介质中，任何[标量场](@entry_id:151443) $\Psi(\vec{r}, t)$（例如[电场](@entry_id:194326)或[磁场](@entry_id:153296)的某个分量）都满足[三维波动方程](@entry_id:162663)：
$$ \nabla^2 \Psi - \frac{1}{v^2}\frac{\partial^2 \Psi}{\partial t^2} = 0 $$
其中 $v$ 是波在该介质中的传播速度。这个[偏微分方程](@entry_id:141332)的一个非常重要且普遍的解族具有以下形式：
$$ \Psi(\vec{r}, t) = f(\vec{k} \cdot \vec{r} - \omega t) $$
这里的 $f$ 是任意的二次[可微函数](@entry_id:144590)。这种形式的解描述了一个**行波 (traveling wave)**。函数的整个“形状”或“轮廓”会随着时间平移，而不会发生畸变。

为了理解这一点，我们考虑一个相位(phase)为常数的点。相位是函数 $f$ 的[自变量](@entry_id:267118)，即 $\phi = \vec{k} \cdot \vec{r} - \omega t$。在所有满足 $\vec{k} \cdot \vec{r} - \omega t = \text{常数}$ 的时空点 $(\vec{r}, t)$ 上，场 $\Psi$ 的值都相同。这些点构成了**等相面 (surfaces of constant phase)**，也称为**[波前](@entry_id:197956) (wavefronts)**。对于给定的时间 $t$，方程 $\vec{k} \cdot \vec{r} = \omega t + \text{常数}$ 描述了一系列相互平行的平面，其[法向量](@entry_id:264185)为 $\vec{k}$。因此，这种波被称为**[平面波](@entry_id:189798) (plane wave)**。

向量 $\vec{k}$ 被称为**波矢 (wavevector)**，它指明了[波的传播](@entry_id:144063)方向，其大小 $k = |\vec{k}|$ 被称为**[波数](@entry_id:172452) (wavenumber)**，与波长 $\lambda$ 的关系是 $k = 2\pi/\lambda$。标量 $\omega$ 是**[角频率](@entry_id:261565) (angular frequency)**，与频率 $\nu$ 和周期 $T$ 的关系是 $\omega = 2\pi\nu = 2\pi/T$。波前以**相速度 (phase velocity)** $v_p = \omega/k$ 沿着 $\vec{k}$ 的方向传播。

#### [单色性](@entry_id:175510)与正弦形式

当[波函数](@entry_id:147440) $\Psi$ 具有单一、确定的频率 $\omega$ 时，我们称之为**单色波 (monochromatic wave)**。这意味着函数 $f$ 必须是正弦函数（正弦或余弦）。因此，一个单色[平面波](@entry_id:189798)最一般的实数形式可以写为：
$$ \Psi(\vec{r}, t) = A \cos(\vec{k} \cdot \vec{r} - \omega t + \delta) $$
其中 $A$ 是波的**振幅 (amplitude)**，$\delta$ 是**初始相位 (initial phase)**。

在许多分析中，使用复数表示法更为便捷：
$$ \tilde{\Psi}(\vec{r}, t) = \tilde{A} \exp(i(\vec{k} \cdot \vec{r} - \omega t)) $$
其中 $\tilde{A} = A \exp(i\delta)$ 是[复振幅](@entry_id:164138)。物理场是这个复数表达式的实部，即 $\Psi = \text{Re}(\tilde{\Psi})$。

#### 识别[行波](@entry_id:185008)

判断一个给定的函数形式是否能代表一个行进的单色[平面波](@entry_id:189798)，关键在于检查其相位是否是空间和时间的线性组合，即形如 $\vec{k} \cdot \vec{r} \pm \omega t$。例如，考虑沿 $z$ 轴传播的波，其相位应为 $kz \pm \omega t$。

- 函数 $\Psi(z, t) = B \cos(kz + \omega t)$ 显然符合这个定义，描述了一个沿 $-z$ 方向传播的波。

- 形式如 $\Psi(z, t) = D (\sin(kz - \omega t) + \cos(kz - \omega t))$ 的函数，通过[三角恒等式](@entry_id:165065)可以合并为一个单一的[正弦波](@entry_id:274998)：$D\sqrt{2}\sin(kz - \omega t + \pi/4)$。因此，它也代表了一个沿 $+z$ 方向传播的单色[平面波](@entry_id:189798)。

- 而函数 $\Psi(z,t) = A\sin(kz)\cos(\omega t)$ 并非[行波](@entry_id:185008)。利用积化和差公式，它可以展开为 $\frac{A}{2}[\sin(kz+\omega t) + \sin(kz-\omega t)]$，这实际上是两个振[幅相](@entry_id:269870)等、方向相反的行[波的叠加](@entry_id:166456)，形成的是**[驻波](@entry_id:148648) (standing wave)**，我们将在后面详细讨论。

- 同样，一个形如 $\Psi(z,t) = C \exp(-(kz - \omega t)^2)$ 的[高斯波包](@entry_id:151158)虽然也是一个行波（其形状沿 $z$ 轴平移），但它不是正弦形式，因此不是单色的，它是由一个连续[频率谱](@entry_id:276824)的波叠加而成。[@problem_id:1809094]

#### [波前](@entry_id:197956)与波矢

[波矢](@entry_id:178620) $\vec{k}$ 的方向定义了[波的传播](@entry_id:144063)方向，并且垂直于波前。假设一个在 $xz$ 平面内传播的波，其波前与 $xy$ 平面成 $\alpha$ 角。由于 $xy$ 平面的[法向量](@entry_id:264185)是 $\hat{z}$，这意味着[波的传播](@entry_id:144063)方向 $\hat{k}$ 与 $\hat{z}$ 轴的夹角为 $\alpha$。如果波在 $+x$ 方向有分量，那么在 $xz$ 平面内，这个单位传播矢量可以唯一地确定为 $\hat{k} = \sin(\alpha)\hat{x} + \cos(\alpha)\hat{z}$。[@problem_id:1593469]

### 真空中电磁[平面波](@entry_id:189798)的结构

现在，我们将这些普遍的波动概念应用于[电磁场](@entry_id:265881)。在没有[电荷](@entry_id:275494)和电流的真空区域，[麦克斯韦方程组](@entry_id:150940)为：
1.  $\nabla \cdot \vec{E} = 0$
2.  $\nabla \cdot \vec{B} = 0$
3.  $\nabla \times \vec{E} = -\frac{\partial \vec{B}}{\partial t}$
4.  $\nabla \times \vec{B} = \mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t}$

我们寻找这些方程的单色[平面波解](@entry_id:195230)，其形式为：
$$ \vec{E}(\vec{r}, t) = \vec{E}_0 \cos(\vec{k} \cdot \vec{r} - \omega t) $$
$$ \vec{B}(\vec{r}, t) = \vec{B}_0 \cos(\vec{k} \cdot \vec{r} - \omega t) $$
其中 $\vec{E}_0$ 和 $\vec{B}_0$ 是恒定的矢量振幅。

#### 横向性

将[平面波解](@entry_id:195230)代入高斯定律 $\nabla \cdot \vec{E} = 0$。利用[链式法则](@entry_id:190743)，$\nabla$ 作用于 $\cos(\vec{k} \cdot \vec{r} - \omega t)$ 相当于乘以 $-\vec{k}\sin(\vec{k} \cdot \vec{r} - \omega t)$。因此，我们得到：
$$ \nabla \cdot \vec{E} = -\vec{E}_0 \cdot \vec{k} \sin(\vec{k} \cdot \vec{r} - \omega t) = 0 $$
为使此式对所有时空点成立，必须有 $\vec{k} \cdot \vec{E}_0 = 0$。同理，从 $\nabla \cdot \vec{B} = 0$ 可得 $\vec{k} \cdot \vec{B}_0 = 0$。

这两个条件意味着[电场和磁场](@entry_id:261347)矢量都垂直于波的传播方向 $\vec{k}$。这正是[电磁波](@entry_id:269629)是**[横波](@entry_id:269527) (transverse waves)** 的数学证明。

#### 场矢量的相互关系与[真空色散](@entry_id:187358)关系

接下来，我们将[平面波解](@entry_id:195230)代入[法拉第定律](@entry_id:149836) $\nabla \times \vec{E} = -\frac{\partial \vec{B}}{\partial t}$。
左边：$\nabla \times \vec{E} = -\vec{k} \times \vec{E}_0 \sin(\vec{k} \cdot \vec{r} - \omega t)$。
右边：$-\frac{\partial \vec{B}}{\partial t} = -\vec{B}_0 \omega \sin(\vec{k} \cdot \vec{r} - \omega t)$。
比较两边，我们得到 $\vec{k} \times \vec{E}_0 = \omega \vec{B}_0$，进而有 $\vec{B} = \frac{1}{\omega}(\vec{k} \times \vec{E})$。

这个关系揭示了三个关键结构特性：
1.  **相互正交**：$\vec{B}$ 垂直于 $\vec{E}$。由于两者也都垂直于 $\vec{k}$，因此 $\vec{E}$、$\vec{B}$ 和 $\vec{k}$ 构成一个相互正交的[右手坐标系](@entry_id:166669)。
2.  **相位一致**：$\vec{E}$ 和 $\vec{B}$ 的[振荡](@entry_id:267781)是同相的。
3.  **振幅关系**：$B_0 = \frac{k}{\omega} E_0$。

我们可以通过一个具体的例子来验证这个推导。假设在真空中测量到一个沿 $z$ 轴传播的[磁场](@entry_id:153296)分量为 $\vec{B}(z, t) = -\hat{x} B_0 \sin(kz + \omega t + \phi_0)$。通过法拉第定律积分可以求得[电场](@entry_id:194326)，再利用[安培-麦克斯韦定律](@entry_id:266368)进行约束，最终可以唯一地确定[电场](@entry_id:194326)为 $\vec{E}(z,t) = -\hat{y} c B_0 \sin(kz + \omega t + \phi_0)$，并得到 $\omega/k=c$ 的关系。这完美地展示了如何从一个场导出另一个场，并揭示了它们之间的内在联系。[@problem_id:1593512]

最后，我们将这些结果代入[安培-麦克斯韦定律](@entry_id:266368) $\nabla \times \vec{B} = \mu_0 \epsilon_0 \frac{\partial \vec{E}}{\partial t}$。对[平面波解](@entry_id:195230)应用此定律，我们得到振幅之间的关系 $\vec{k} \times \vec{B}_0 = -\mu_0\epsilon_0\omega\vec{E}_0$。将[法拉第定律](@entry_id:149836)的结果 $\vec{B}_0 = \frac{1}{\omega}(\vec{k} \times \vec{E}_0)$ 代入此式：
$$ \vec{k} \times \left( \frac{1}{\omega}(\vec{k} \times \vec{E}_0) \right) = -\mu_0\epsilon_0\omega\vec{E}_0 $$
利用矢量恒等式 $\vec{A}\times(\vec{B}\times\vec{C}) = \vec{B}(\vec{A}\cdot\vec{C})-\vec{C}(\vec{A}\cdot\vec{B})$ 和横波条件 $\vec{k}\cdot\vec{E}_0=0$，上式左边可简化为 $-\frac{k^2}{\omega}\vec{E}_0$。因此，我们有：
$$ -\frac{k^2}{\omega}\vec{E}_0 = -\mu_0\epsilon_0\omega\vec{E}_0 $$
为了使方程对非零[电场](@entry_id:194326)成立，必须有 $k^2 = \mu_0 \epsilon_0 \omega^2$。这导出了真空中[电磁波](@entry_id:269629)的**色散关系 (dispersion relation)**：
$$ \frac{\omega}{k} = \frac{1}{\sqrt{\mu_0 \epsilon_0}} \equiv c $$
这表明，在真空中，所有频率的[电磁波](@entry_id:269629)都以相同的速度 $c$（光速）传播。这种介质被称为**非[色散介质](@entry_id:180771) (non-dispersive medium)**。
将此关系代入振幅关系，我们得到一个极为重要的结果：$E_0 = c B_0$。

值得注意的是，并非所有波动现象都遵循这个简单的[线性色散关系](@entry_id:266313)。例如，在[量子场论](@entry_id:138177)中，一个质量为 $m_0$ 的标量[玻色子](@entry_id:138266)场满足克莱因-戈尔登方程，其[平面波解](@entry_id:195230)的[色散关系](@entry_id:140395)为 $\omega^2 = c^2 k^2 + (m_0 c^2 / \hbar)^2$。这种[非线性](@entry_id:637147)的[色散关系](@entry_id:140395)意味着不同频率（或[波数](@entry_id:172452)）的波以不同的相速度传播，这种现象被称为**[色散](@entry_id:263750) (dispersion)**。[@problem_id:1809080]

### [电磁波的能量](@entry_id:275250)与动量

[电磁波](@entry_id:269629)不仅是场的[振荡](@entry_id:267781)，它们还携带能量和动量。

#### 能量密度与能量均分

[电场和磁场](@entry_id:261347)的瞬时能量密度分别为：
$$ u_E = \frac{1}{2}\epsilon_0 E^2 \quad \text{和} \quad u_B = \frac{1}{2\mu_0} B^2 $$
对于一个在真空中传播的单色平面波，由于 $E=cB$ 且 $c^2=1/(\epsilon_0\mu_0)$，我们可以证明：
$$ u_B = \frac{1}{2\mu_0} \left(\frac{E}{c}\right)^2 = \frac{E^2}{2\mu_0 c^2} = \frac{\epsilon_0 \mu_0 E^2}{2\mu_0} = \frac{1}{2}\epsilon_0 E^2 = u_E $$
这意味着在任意时刻、任意地点，单个行进[平面波](@entry_id:189798)的[电场能量密度](@entry_id:261497)和[磁场能量](@entry_id:267501)密度总是相等的。这被称为**能量均分 (energy equipartition)**。

#### 坡印亭矢量与波强度

[电磁场](@entry_id:265881)的能量流密度由**坡印亭矢量 (Poynting vector)** 描述：
$$ \vec{S} = \frac{1}{\mu_0}(\vec{E} \times \vec{B}) $$
对于一个沿 $\hat{k}$ 方向传播的平面波，$\vec{E}$ 和 $\vec{B}$ 正交，$\vec{E} \times \vec{B}$ 的方向与 $\hat{k}$ 相同，其大小为 $EB$。因此：
$$ \vec{S} = \frac{1}{\mu_0} EB \hat{k} = \frac{1}{\mu_0 c} E^2 \hat{k} = c \epsilon_0 E^2 \hat{k} = (u_E + u_B) c \hat{k} $$
这个结果的物理意义非常直观：能量密度 $(u_E+u_B)$ 以速度 $c$ 沿传播方向 $\hat{k}$ 流动。

由于场是随时间快速[振荡](@entry_id:267781)的，我们通常更关心其时间平均值。波的**强度 (intensity)** $I$ 定义为坡印亭矢量大小的时间平均值：
$$ I = |\langle \vec{S} \rangle| = \langle c \epsilon_0 E_0^2 \cos^2(\vec{k} \cdot \vec{r} - \omega t) \rangle $$
由于 $\langle\cos^2(\theta)\rangle = 1/2$，我们得到：
$$ I = \frac{1}{2} c \epsilon_0 E_0^2 $$
这个公式将宏观可测量的强度与微观的场振幅联系起来。

#### 辐射压

[电磁波](@entry_id:269629)不仅携带能量，还携带动量。动量密度为 $\vec{g} = \vec{S}/c^2$。当[电磁波](@entry_id:269629)被物体吸收或反射时，它会对物体施加一个力，产生**[辐射压](@entry_id:143156) (radiation pressure)**。
考虑一个面积为 $A$ 的完美反射镜，垂直于入射的[电磁波](@entry_id:269629)。波的动量被完全反向，传递给镜面的动量是入射动量的两倍。单位时间内传递的动量即为力 $F$。
$$ F = \frac{d\vec{p}}{dt} \cdot \hat{k} = (2 \times \frac{I}{c}) A $$
因此，辐射压 $P = F/A = 2I/c$。这个原理是[太阳帆](@entry_id:273839)等未来航天技术的理论基础。通过测量施加在帆上的力，我们可以反推出入射光的[磁场](@entry_id:153296)振幅 $B_0$。结合 $I = F c/(2A)$ 和 $I = \frac{1}{2}c\epsilon_0 E_0^2 = \frac{1}{2}c^3\epsilon_0 B_0^2$，可以解得 $B_0 = \sqrt{F/(Ac^2\epsilon_0)}$。[@problem_id:1593509]

#### 与[带电粒子](@entry_id:160311)的相互作用

[电磁波](@entry_id:269629)通过[洛伦兹力](@entry_id:145104)与[带电粒子](@entry_id:160311)相互作用。一个[电荷](@entry_id:275494)为 $q$，以速度 $\vec{v}$ 运动的粒子受到的力为：
$$ \vec{F} = q(\vec{E} + \vec{v} \times \vec{B}) $$
考虑一个沿 $+z$ 方向传播、[电场](@entry_id:194326)振幅为 $E_0$、偏振方向与 $x$ 轴成 $\theta$ 角的[线偏振](@entry_id:273116)波。在 $(z,t)=(0,0)$ 时刻，$\vec{E} = E_0(\cos\theta \hat{x} + \sin\theta \hat{y})$，而 $\vec{B} = \frac{1}{c}(\hat{z} \times \vec{E}) = \frac{E_0}{c}(\cos\theta \hat{y} - \sin\theta \hat{x})$。对于一个以速度 $\vec{v} = v_z\hat{z}$ 穿过原点的电子，它所受到的力可以精确计算出来。这个例子清晰地展示了[电磁波](@entry_id:269629)的完整矢量结构如何决定其对物质的具体作用。[@problem_id:1593482]

### 平面波的叠加

由于麦克斯韦方程是线性的，[波的叠加原理](@entry_id:166456)成立：当多个[电磁波](@entry_id:269629)同时存在于一个区域时，总的[电场和磁场](@entry_id:261347)分别是各个波的电场和磁场的矢量和。

#### 偏振

**偏振 (polarization)** 描述了[电场](@entry_id:194326)矢量 $\vec{E}$ 在空间中传播时其端点轨迹的形状。
- **线偏振 (Linear Polarization)**：我们之前讨论的波，其 $\vec{E}$ 矢量始终在同一个方向上[振荡](@entry_id:267781)。
- **圆偏振与[椭圆偏振](@entry_id:270497) (Circular and Elliptical Polarization)**：当两个具有相同频率、在空间上正交的[线偏振](@entry_id:273116)波叠加时，如果它们之间存在相位差，就会产生更复杂的偏振状态。

考虑两个沿 $+z$ 方向传播的波，振幅均为 $E_0$，一个沿 $x$ 轴偏振 $\vec{E}_1 = E_0 \cos(kz-\omega t)\hat{x}$，另一个沿 $y$ 轴偏振且[相位超前](@entry_id:269084) $\pi/2$，$\vec{E}_2 = E_0 \cos(kz-\omega t+\pi/2)\hat{y} = -E_0 \sin(kz-\omega t)\hat{y}$。
总[电场](@entry_id:194326)为 $\vec{E} = \vec{E}_1 + \vec{E}_2 = E_0[\cos(kz-\omega t)\hat{x} - \sin(kz-\omega t)\hat{y}]$。
在任一固定位置 $z$，随着时间 $t$ 的推移，[电场](@entry_id:194326)矢量 $\vec{E}$ 的端点在 $xy$ 平面内描绘出一个圆。这种波被称为**[圆偏振波](@entry_id:200164) (circularly polarized wave)**。一个有趣的结果是，这种波的坡印亭矢量 $\vec{S} = \epsilon_0 c E_0^2 \hat{z}$ 是一个恒定的矢量，不随时间或空间变化。这意味着[圆偏振光](@entry_id:198374)的[能量流](@entry_id:142770)是均匀且稳定的，这与线偏振光瞬时[能量流](@entry_id:142770)的脉动形成对比。[@problem_id:1809063]

#### [驻波](@entry_id:148648)

当两个振幅、频率和偏振都相同，但传播方向相反的波叠加时，会形成**[驻波](@entry_id:148648) (standing wave)**。
例如，叠加 $\vec{E}_1 = E_0 \cos(kz-\omega t)\hat{x}$ 和 $\vec{E}_2 = E_0 \cos(kz+\omega t)\hat{x}$：
$$ \vec{E}_{total}(z, t) = 2E_0 \cos(kz) \cos(\omega t) \hat{x} $$
这个表达式的特点是空间部分 $\cos(kz)$ 和时间部分 $\cos(\omega t)$ 是分离的。场的振幅 $2E_0|\cos(kz)|$ 仅取决于位置。
- **[波节](@entry_id:167209) (Nodes)**：在振幅永远为零的位置，即 $\cos(kz)=0$ 的地方，如 $z = (n+\frac{1}{2})\frac{\pi}{k}$。
- **波腹 (Ant[inode](@entry_id:750667)s)**：在振幅达到最大的位置，即 $|\cos(kz)|=1$ 的地方，如 $z = n\frac{\pi}{k}$。

对应的[磁场](@entry_id:153296)为：
$$ \vec{B}_{total}(z, t) = \frac{2E_0}{c} \sin(kz) \sin(\omega t) \hat{y} $$
我们发现，[磁场](@entry_id:153296)的[波节](@entry_id:167209)（$\sin(kz)=0$）恰好是[电场](@entry_id:194326)的波腹，而[磁场](@entry_id:153296)的波腹（$|\sin(kz)|=1$）恰好是[电场](@entry_id:194326)的[波节](@entry_id:167209)。电场和磁场的[波节](@entry_id:167209)（或波腹）在空间上相互错开，最小间隔为 $\Delta z = \frac{\pi}{2k} = \frac{\pi c}{2\omega}$，即四分之一波长。此外，[电场和磁场](@entry_id:261347)在时间上也有 $\pi/2$ 的相位差（一个随 $\cos(\omega t)$ 变化，另一个随 $\sin(\omega t)$ 变化）。[@problem_id:1593456]

[驻波中的能量](@entry_id:194086)行为也与行波截然不同。[驻波](@entry_id:148648)的坡印亭矢量的时间平均值为零，$\langle \vec{S} \rangle = 0$，表示没有净能量的定向传输。能量只是在[电场和磁场](@entry_id:261347)之间、在[波节和波腹](@entry_id:186674)之间来回“[振荡](@entry_id:267781)”。在[驻波](@entry_id:148648)中，时间平均的电能密度和[磁能密度](@entry_id:193006)通常不相等，并且都与位置有关。例如，在一个纯[驻波](@entry_id:148648)中，$\langle u_E \rangle \propto \cos^2(kz)$，而 $\langle u_B \rangle \propto \sin^2(kz)$。它们的比值 $\langle u_B \rangle / \langle u_E \rangle = \tan^2(kz)$ 明显依赖于位置 $z$。[@problem_id:1593500]

#### 部分反射与混合波

在更实际的情况下，例如当一个波入射到一个部分反射的表面上时，会形成一个由[行波](@entry_id:185008)和驻波混合而成的场。在反射区域，总场是入射波和较弱的反射[波的叠加](@entry_id:166456)。这种混合波既有能量的净传输（由行波分量贡献），又有[驻波](@entry_id:148648)的空间结构特征。
在这种情况下，[时间平均](@entry_id:267915)的电能密度和[磁能密度](@entry_id:193006)的比值会变得非常复杂，它既依赖于位置，也依赖于表面的[反射系数](@entry_id:194350) $r$。对于一个沿 $z$ 轴传播的波，在 $z \le 0$ 区域，这个比值可以表示为：
$$ \mathcal{R}(z) = \frac{\langle u_E \rangle}{\langle u_B \rangle} = \frac{1 + r^2 + 2r \cos(2kz)}{1 + r^2 - 2r \cos(2kz)} $$
这个表达式揭示了复杂的能量[分布](@entry_id:182848)：在某些位置（$\cos(2kz)=1$），比值达到最小值 $(1-r)^2/(1+r)^2$；而在另一些位置（$\cos(2kz)=-1$），比值达到最大值 $(1+r)^2/(1-r)^2$。这与纯[行波](@entry_id:185008)中比值恒为 1 以及纯[驻波](@entry_id:148648)中比值在 0 和无穷大之间变化形成了鲜明对比。[@problem_id:1593492]

### [物质中的电磁波](@entry_id:189104)：简要展望

当[电磁波](@entry_id:269629)在[电介质](@entry_id:147163)或导体等物质中传播时，其行为会因与物质的相互作用而改变。

#### 导体中的波

在具有电导率 $\sigma$ 的良导体中，[电场](@entry_id:194326)会驱动传导电流 $\vec{J}_f = \sigma \vec{E}$。这在[安培-麦克斯韦定律](@entry_id:266368)中增加了一项。对于单色波，这等效于引入一个[复介电常数](@entry_id:160910) $\epsilon_c = \epsilon - i\sigma/\omega$。求解[波动方程](@entry_id:139839)会导致一个复数[波矢](@entry_id:178620) $\tilde{k}$，其实部导致相移，虚部导致**衰减 (attenuation)**。

一个重要的后果是，在导体中，[电场](@entry_id:194326) $\vec{E}$ 和[磁场](@entry_id:153296) $\vec{B}$ 不再同相。[磁场](@entry_id:153296)会滞后于[电场](@entry_id:194326)一个相位角 $\delta$。这个相位滞后的物理根源在于，产生[磁场](@entry_id:153296)的源（根据[安培定律](@entry_id:140092)）现在是位移电流（与 $\partial\vec{E}/\partial t$ 成正比，[相位超前](@entry_id:269084) $\vec{E}$ 90度）和[传导电流](@entry_id:265343)（与 $\vec{E}$ 同相）的矢量和。
这个相位滞后角 $\delta$ 的大小取决于[传导电流](@entry_id:265343)与位移电流的相对大小，可以用无量纲参数 $\xi = \sigma/(\omega\epsilon)$ 来量化：
$$ \delta = \frac{1}{2}\arctan(\xi) $$
对于绝缘体（$\sigma \to 0, \xi \to 0$），$\delta \to 0$，场是同相的。对于良导体（$\sigma \to \infty, \xi \to \infty$），$\delta \to \pi/4$，[磁场](@entry_id:153296)滞后[电场](@entry_id:194326)45度。[@problem_id:1593460]