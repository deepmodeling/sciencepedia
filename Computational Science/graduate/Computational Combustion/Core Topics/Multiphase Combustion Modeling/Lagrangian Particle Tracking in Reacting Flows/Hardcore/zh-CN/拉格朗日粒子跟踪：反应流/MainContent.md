## 引言
在众多科学与工程领域，从[内燃机](@entry_id:200042)的[喷雾燃烧](@entry_id:1132216)到大气中污染物的扩散，再到宇宙[大尺度结构](@entry_id:158990)的形成，我们都会遇到一个共同的挑战：理解和预测大量离散粒子在[复杂流体](@entry_id:198415)环境中的行为。反应流中的[拉格朗日粒子追踪](@entry_id:751115)（Lagrangian Particle Tracking, LPT）正是应对这一挑战的核心计算方法。它通过直接追踪单个或成组粒子的轨迹，为我们提供了一个连接微观[粒子动力学](@entry_id:1129385)与宏观系统行为的强大桥梁。然而，精确模拟这些过程需要深刻理解粒子与[湍流](@entry_id:151300)、化学反应以及热场之间错综复杂的相互作用。

本文旨在系统性地梳理[反应流](@entry_id:190741)中[拉格朗日粒子追踪](@entry_id:751115)的理论框架与应用实践。我们将带领读者深入探索这一多物理场耦合问题的核心。在“原理与机制”一章中，我们将建立控制粒子运动、传热和传质的基本方程，并探讨关键的[无量纲参数](@entry_id:169335)和物理现象，如[斯托克斯数](@entry_id:185766)、稀薄气体效应以及与[湍流](@entry_id:151300)的相互作用。随后，在“应用与跨学科交叉”一章中，我们将展示LPT方法如何作为一种通用工具，在燃烧、航空航天、[环境科学](@entry_id:187998)乃至天体物理学等多元领域中解决实际问题。最后，“动手实践”部分将引导读者将理论知识应用于具体的计算挑战中。通过这一系列的学习，读者将能够掌握LPT方法的基本原理，并洞悉其在现代科学研究中的广阔应用前景。

## 原理与机制

在深入探讨[反应流](@entry_id:190741)中[拉格朗日粒子追踪](@entry_id:751115)的计算方面之前，我们必须首先建立一个描述单个粒子在流体中行为的坚实物理和数学框架。本章阐述了控制粒子运动、传热和传质的基本原理。我们将从牛顿第二定律出发，系统地介绍作用在粒子上的各种力，然后探讨与周围气体环境的热和质量耦合，最后研究粒子与[湍流](@entry_id:151300)的复杂相互作用。

### 拉格朗日粒子[运动方程](@entry_id:264286)

在最根本的层面上，一个离散粒子在流体中的运动由牛顿第二定律描述。对于一个质量 $m_p$ 可能随时间变化的粒子（例如，由于蒸发或[表面反应](@entry_id:183202)），其动量 $m_p \boldsymbol{v}_p$ 的变化率等于作用在其上的合外力 $\sum \boldsymbol{F}$。这里，$\boldsymbol{v}_p$ 是粒子的拉格朗日速度。

$$
\frac{\mathrm{d}(m_p \boldsymbol{v}_p)}{\mathrm{d}t} = \sum \boldsymbol{F}
$$

使用[乘法法则](@entry_id:144424)展开左侧的时间导数，我们得到：

$$
m_p \frac{\mathrm{d}\boldsymbol{v}_p}{\mathrm{d}t} + \boldsymbol{v}_p \frac{\mathrm{d}m_p}{\mathrm{d}t} = \sum \boldsymbol{F}
$$

重新整理后，我们得到了[粒子加速](@entry_id:158202)度的表达式：

$$
\frac{\mathrm{d}\boldsymbol{v}_p}{\mathrm{d}t} = \frac{1}{m_p} \left( \sum \boldsymbol{F} - \boldsymbol{v}_p \frac{\mathrm{d}m_p}{\mathrm{d}t} \right)
$$

这个方程揭示了两个关键点。首先，粒子的加速度由作用在其上的力的总和决定。这些力包括[流体动力](@entry_id:750449)、重力以及其他潜在的[力场](@entry_id:147325)。其次，当[粒子质量](@entry_id:156313)发生变化时（$\mathrm{d}m_p/\mathrm{d}t \neq 0$），会产生一个额外的项。如果质量减少（例如，通过表面反应消耗），项 $- \boldsymbol{v}_p \frac{\mathrm{d}m_p}{\mathrm{d}t}$ 表现为一个推力，因为当质量减少（即 $\frac{\mathrm{d}m_p}{\mathrm{d}t}  0$）时，该项与[粒子速度](@entry_id:196946) $\boldsymbol{v}_p$ 同向。

要完整描述粒子的轨迹，我们还需要求解其位置 $\boldsymbol{x}_p$ 的运动学关系：

$$
\frac{\mathrm{d}\boldsymbol{x}_p}{\mathrm{d}t} = \boldsymbol{v}_p(t)
$$

接下来的挑战在于准确地识别和建模合力 $\sum \boldsymbol{F}$ 以及质量变化率 $\mathrm{d}m_p/\mathrm{d}t$。

### 连续介质区中的[流体动力](@entry_id:750449)

当粒子远大于气体分子的平均自由程时，我们可以将周围的流体视为连续介质。在这种情况下，作用在粒子上的主要流体动力包括曳力、压力[梯度力](@entry_id:166847)、[附加质量](@entry_id:267870)力和非定常力。

#### 曳力

**曳力 (Drag Force)** 是最基本也是最重要的[流体动力](@entry_id:750449)，它源于粒子与流体之间的相对运动。该力抵抗粒子相对于流体的运动。滑移速度定义为气体速度 $\boldsymbol{u}$ 与[粒子速度](@entry_id:196946) $\boldsymbol{v}_p$ 之差，即 $\boldsymbol{w} = \boldsymbol{u} - \boldsymbol{v}_p$。曳力的一般形式为：

$$
\boldsymbol{F}_d = \frac{1}{2} \rho_f |\boldsymbol{w}| A_p C_D \frac{\boldsymbol{w}}{|\boldsymbol{w}|}
$$

其中 $\rho_f$ 是流体密度，$A_p$ 是粒子的投影面积，$C_D$ 是无量纲的曳力系数。曳力系数 $C_D$ 主要依赖于**粒子雷诺数 (particle Reynolds number)**，$Re_p = \frac{\rho_f |\boldsymbol{w}| d_p}{\mu}$，其中 $d_p$ 是粒子直径，$\mu$ 是流体的[动力粘度](@entry_id:268228)。

在许多燃烧应用中，特别是在研究小颗粒（如煤粉、液滴或烟尘）时，$Re_p$ 通常远小于1。在这个[蠕动流](@entry_id:263844)区域，曳力系数可以简化为 $C_D = 24/Re_p$，代入上式后得到著名的**斯托克斯曳力 (Stokes drag)** 定律：

$$
\boldsymbol{F}_d = 3\pi\mu d_p (\boldsymbol{u} - \boldsymbol{v}_p)
$$

斯托克斯曳力与滑移速度成线性关系，这极大地简化了[运动方程](@entry_id:264286)的求解。对于更高的雷诺数，需要使用经验性的 $C_D(Re_p)$ 关联式。

#### 压力[梯度力](@entry_id:166847)与[浮力](@entry_id:154088)

当粒子浸没在存在压力梯度的流场中时，其表面会受到不均匀的[压力分布](@entry_id:275409)，从而产生一个[净力](@entry_id:163825)。对于一个远小于压[力场](@entry_id:147325)变化特征长度的粒子，作用在其上的**压力[梯度力](@entry_id:166847) (pressure gradient force)** 可以近似为：

$$
\boldsymbol{F}_p = -V_p \nabla p
$$

其中 $V_p$ 是粒子体积，$\nabla p$ 是粒子所在位置的未受扰动的[流体压力](@entry_id:142203)梯度。根据[无粘流](@entry_id:273124)体的[动量方程](@entry_id:197225)（欧拉方程），压力梯度与流体加速度密切相关：$\rho_f \frac{D\boldsymbol{u}}{Dt} = -\nabla p + \dots$（其中 $D/Dt$ 是物质导数）。因此，压力[梯度力](@entry_id:166847)通常表示为：

$$
\boldsymbol{F}_p \approx \rho_f V_p \frac{D\boldsymbol{u}}{Dt}
$$

一个特殊且常见的情况是[静止流体](@entry_id:187621)中的重[力场](@entry_id:147325)，此时压力梯度用于平衡重力，即 $\nabla p = \rho_f \boldsymbol{g}$。在这种情况下，作用在粒子上的总重力与压力[梯度力](@entry_id:166847)之和为 $m_p \boldsymbol{g} + \boldsymbol{F}_p = \rho_p V_p \boldsymbol{g} - \rho_f V_p \boldsymbol{g} = (\rho_p - \rho_f) V_p \boldsymbol{g}$。这就是我们熟知的**[浮力](@entry_id:154088) (buoyancy force)**。

#### [附加质量](@entry_id:267870)力

当粒子在流体中加速时，它必须同时加速其周围的流体。这种效应产生了一个抵抗相对加速度的力，称为**[附加质量](@entry_id:267870)力 (added-mass force)** 或虚拟质量力。其表达式为：

$$
\boldsymbol{F}_{am} = - C_{am} \rho_f V_p \frac{\mathrm{d}(\boldsymbol{v}_p - \boldsymbol{u})}{\mathrm{d}t}
$$

其中 $C_{am}$ 是[附加质量](@entry_id:267870)系数，对于球体，$C_{am} = 1/2$。该力的大小正比于流体密度 $\rho_f$。因此，它对于密度远大于流体密度的粒子（$\rho_p \gg \rho_f$，如固体颗粒在气体中）通常可以忽略，但对于气泡在液体中或密度相近的系统则非常重要。

在一个设想的场景中，我们可以清晰地看到压力[梯度力](@entry_id:166847)和[附加质量](@entry_id:267870)力如何共同决定粒子的加速度 。考虑一个粒子处于[无粘流](@entry_id:273124)中，仅受这两种力的作用。粒子的[运动方程](@entry_id:264286)为 $m_p a_p = \boldsymbol{F}_p + \boldsymbol{F}_{am}$，其中 $a_p = d\boldsymbol{v}_p/dt$ 是粒子加速度。代入表达式：

$$
\rho_p V_p a_p = \rho_f V_p \frac{D\boldsymbol{u}}{Dt} - \frac{1}{2} \rho_f V_p \left(\frac{\mathrm{d}\boldsymbol{v}_p}{\mathrm{d}t} - \frac{\mathrm{d}\boldsymbol{u}}{\mathrm{d}t}\right)
$$

在粒子与流体无滑移的瞬间，[物质导数](@entry_id:262900) $D\boldsymbol{u}/Dt$ 和时间导数 $d\boldsymbol{u}/dt$ 是等价的，都代表流体加速度 $a_f$。于是方程简化为：

$$
\left(\rho_p + \frac{1}{2}\rho_f\right) a_p = \frac{3}{2} \rho_f a_f
$$

利用欧拉方程 $a_f = -(1/\rho_f)\nabla p$，我们最终得到[粒子加速](@entry_id:158202)度与压力梯度的直接关系 ：

$$
a_p = -\frac{3/2}{\rho_p + \rho_f/2} \nabla p
$$

这个结果表明，粒子（即使密度远大于流体）也会响应流场的压力梯度，其加速度方向与压力梯度方向相反，即从高压区被推向低压区。

#### Basset历史力

**Basset历史力 (Basset history force)** 是一个更为复杂的非定常力，它源于滑移速度变化时，从粒子[表面扩散](@entry_id:186850)出去的[涡量](@entry_id:142747)的[延迟效应](@entry_id:199612)。它是一个[卷积积分](@entry_id:155865)形式，表示了粒子过去运动历史对其当前受力的影响：

$$
\boldsymbol{F}_B(t) = 6 a^2 \sqrt{\pi \rho_f \mu} \int_{-\infty}^{t} \frac{\mathrm{d}(\boldsymbol{u}-\boldsymbol{v}_p)/\mathrm{d}\tau}{\sqrt{t-\tau}} \mathrm{d}\tau
$$

其中 $a$ 是粒子半径。由于其积分形式，Basset力在计算上非常昂贵，因此在许多实际模拟中被忽略。然而，在粒子运动经历高频振荡或快速变化的流场中，它可能变得非常重要。

为了量化其重要性，我们可以考虑一个粒子在经历谐波滑移速度振荡 $w(t) = W_{amp} \exp(i\omega t)$ 的情况。通过求解上述积分，可以推导出Basset力的振幅与[稳态](@entry_id:139253)斯托克斯曳力振幅的比值 ：

$$
\frac{|\boldsymbol{F}_B|}{|\boldsymbol{F}_S|} = a \sqrt{\frac{\rho_f \omega}{\mu}}
$$

这个无量纲比值表明，Basset力的相对重要性随粒子半径 $a$、流体密度 $\rho_f$ 和[振荡频率](@entry_id:269468) $\omega$ 的增加而增加，随[流体粘度](@entry_id:267219) $\mu$ 的增加而减小。在一个典型的燃烧环境中，对于一个半径为 $20 \, \mu\mathrm{m}$ 的液滴，在 $5000 \, \mathrm{Hz}$ 的高频[声学振荡](@entry_id:161154)下，Basset力的振幅可以达到斯托克斯曳力振幅的 $25\%$ 。这凸显了在某些[反应流](@entry_id:190741)场景中，精确建模[非定常流体](@entry_id:1133151)动力的必要性。

### 超越连续介质：[滑移流](@entry_id:154133)与稀薄气体效应

当粒子尺寸接近或小于气体分子的平均自由程 $\lambda$ 时，连续介质的假设不再成立。描述这种稀薄气体效应的关键[无量纲参数](@entry_id:169335)是**克努森数 (Knudsen number)**：

$$
\mathrm{Kn} = \frac{\lambda}{d_p}
$$

根据Knudsen数的大小，可以划分不同的流态：
- **连续介质流 (Continuum flow)**: $\mathrm{Kn}  0.01$
- **[滑移流](@entry_id:154133) (Slip flow)**: $0.01  \mathrm{Kn}  0.1$
- **过渡流 (Transition flow)**: $0.1  \mathrm{Kn}  10$
- **[自由分子流](@entry_id:1125300) (Free molecular flow)**: $\mathrm{Kn} > 10$

在燃烧过程中产生的纳米级颗粒，如烟尘，其直径通常在 $10-100 \, \mathrm{nm}$ 范围内。在[标准大气](@entry_id:266260)压和高温下，气体分子的平均自由程约为数百纳米。因此，这些颗粒的[Knudsen数](@entry_id:139772)通常大于0.1，处于过渡流或[滑移流区](@entry_id:150965)域。

在[滑移流区](@entry_id:150965)域，流体在粒子表面不再满足[无滑移边界条件](@entry_id:186229)，而是存在一个速度滑移。这导致粒子受到的曳力减小。为了修正连续介质理论，我们引入了**Cunningham滑移修正因子 (Cunningham slip correction factor)**, $C_c$。修正后的斯托克斯曳力为：

$$
\boldsymbol{F}_D = \frac{3\pi \mu d_p}{C_c} (\boldsymbol{u} - \boldsymbol{v}_p)
$$

$C_c$ 的值大于1，其大小依赖于Knudsen数。一个常用的经验公式是 ：

$$
C_c = 1 + \mathrm{Kn}\left(A + B \exp\left(-\frac{C}{\mathrm{Kn}}\right)\right)
$$

其中 $A, B, C$ 是经验常数。为了应用这个修正，我们必须首先计算平均自由程 $\lambda$。根据气体动力学理论，$\lambda$ 可以通过宏观气体性质估算：

$$
\lambda = \frac{\mu}{p} \sqrt{\frac{\pi R_s T}{2}}
$$

其中 $p$ 是压力，$T$ 是温度，$R_s$ 是比气体常数。

考虑一个纳米级烟尘颗粒在高温后火焰区中沉降的实际问题 ，计算其[终端速度](@entry_id:1132946)需要综合上述所有概念。首先，通过Sutherland定律计算高温下的[气体粘度](@entry_id:175253) $\mu$。然后，利用[理想气体定律](@entry_id:146757)计算气体密度 $\rho_g$。接着，计算平均自由程 $\lambda$ 和[Knudsen数](@entry_id:139772) $\mathrm{Kn}$。之后，计算滑移修正因子 $C_c$。最后，在重力、[浮力](@entry_id:154088)和修正后的斯托克斯曳力之间建立力平衡，求解终端[沉降速度](@entry_id:1123566) $v_t$：

$$
(\rho_p - \rho_g)\frac{\pi d_p^3}{6} g = \frac{3\pi \mu d_p}{C_c} v_t
$$

$$
v_t = \frac{(\rho_p - \rho_g) d_p^2 g}{18 \mu} C_c
$$

对于一个直径为 $100 \, \mathrm{nm}$ 的颗粒，在 $1800 \, \mathrm{K}$ 的大气压环境中，[Knudsen数](@entry_id:139772)可达5以上，导致 $C_c$ 的值接近10。这意味着由于稀薄气体效应，曳力被减小了近一个数量级，从而使[终端速度](@entry_id:1132946)比传统[斯托克斯定律](@entry_id:147173)预测的值高出近十倍 。这充分说明了在处理纳米颗粒时考虑稀薄效应的极端重要性。

### 与[反应气体](@entry_id:754126)的质量和[能量耦合](@entry_id:137595)

在反应流中，粒子不仅与流体交换动量，还通过[表面反应](@entry_id:183202)和热交换参与到化学和热力学过程中。

#### [粒子质量](@entry_id:156313)演化

粒子的质量可以因多种机制而改变，如[液滴蒸发](@entry_id:748678)、烟尘凝结或表面化学反应。对于一个经历[表面反应](@entry_id:183202)的固体颗粒（如碳的氧化），其质量变化率 $\mathrm{d}m_p/\mathrm{d}t$ 由表面积 $A_p$ 和单位面积的质量通量 $\dot{m}''$ 决定：

$$
\frac{\mathrm{d}m_p}{\mathrm{d}t} = \dot{m}'' A_p
$$

对于消耗性反应，$\dot{m}''$ 为负值。假设粒子密度 $\rho_p$ 恒定，我们可以将质量变化与直径变化联系起来。因为 $m_p = \rho_p \pi d_p^3 / 6$，我们有：

$$
\frac{\mathrm{d}m_p}{\mathrm{d}t} = \frac{1}{2} \rho_p \pi d_p^2 \frac{\mathrm{d}d_p}{\mathrm{d}t}
$$

结合 $A_p = \pi d_p^2$，我们得到一个简单的直径演化方程 ：

$$
\frac{\mathrm{d}d_p}{\mathrm{d}t} = \frac{2 \dot{m}''}{\rho_p}
$$

#### 粒子能量演化

对于温度可以被认为是均匀的（即**毕渥数 (Biot number)** $\mathrm{Bi} = h d_p / k_p \ll 1$，其中 $k_p$ 是粒子导热系数）的粒子，其温度 $T_p$ 的变化由[集总电容模型](@entry_id:140095)描述，这本质上是粒子能量守恒的表达：

$$
m_p c_p \frac{\mathrm{d}T_p}{\mathrm{d}t} = \dot{Q}_{\text{net}}
$$

其中 $c_p$ 是粒子的比热容，$\dot{Q}_{\text{net}}$ 是进入粒子的净热量率。$\dot{Q}_{\text{net}}$ 通常包括几个部分：

$$
\dot{Q}_{\text{net}} = \dot{Q}_{\text{conv}} + \dot{Q}_{\text{rad}} + \dot{Q}_{\text{chem}}
$$

- **[对流换热](@entry_id:151349)** $\dot{Q}_{\text{conv}} = h A_p (T_g - T_p)$，其中 $h$ 是[对流换热系数](@entry_id:151029)，通常通过**努塞尔数 (Nusselt number)** $Nu = h d_p / k_g$ 的关联式获得（$k_g$ 是气体导热系数）。
- **辐射换热** $\dot{Q}_{\text{rad}}$，涉及粒子表面与周围环境（其他粒子、墙壁、气体）之间的[辐射交换](@entry_id:150522)。
- **化学[反应热](@entry_id:140993)** $\dot{Q}_{\text{chem}}$，由[表面反应](@entry_id:183202)释放或吸收的热量。

#### [热惯性](@entry_id:147003)与[热滞后](@entry_id:154614)

由于粒子的热容，其温度不会瞬时响应周围气体温度的变化。这种**热惯性 (thermal inertia)** 导致了粒子与气体之间的[热滞后](@entry_id:154614)。我们可以通过分析一个在振荡温度场中运动的粒子来理解这个现象 。

考虑一个粒子，其温度方程为 $\frac{\mathrm{d}T_p}{\mathrm{d}t} = \frac{1}{\tau_T} (T_g(t) - T_p(t))$，其中 $\tau_T = \frac{\rho_p c_p d_p}{6h}$ 是**粒子热[响应时间](@entry_id:271485) (particle thermal response time)**。如果粒子经历的有效气体温度呈谐波振荡 $T_g(t) \propto \cos(\omega_{\text{eff}}t)$，那么在长时间后，粒子的温度也将以相同的频率振荡，但会有一个相位滞后 $\phi$：$T_p(t) \propto \cos(\omega_{\text{eff}}t - \phi)$。这个[相位滞后](@entry_id:172443)可以通过[求解微分方程](@entry_id:137471)得到：

$$
\phi = \arctan(\omega_{\text{eff}}\tau_T)
$$

这个结果清晰地表明，[热滞后](@entry_id:154614) $\phi$ 直接取决于粒子热[响应时间](@entry_id:271485) $\tau_T$ 和气体温度振荡频率 $\omega_{\text{eff}}$ 的乘积。在快速变化的温度场中（大的 $\omega_{\text{eff}}$）或对于[热惯性](@entry_id:147003)大的粒子（大的 $\tau_T$），粒子温度将显著落后于气体温度 。

#### 扩散限制下的热质耦合

在许多高温燃烧场景中，表面反应速率非常快，以至于反应物（如氧气）的消耗速率受到其向粒子[表面扩散](@entry_id:186850)的速率的限制。在这种**[扩散限制](@entry_id:153636) (diffusion-limited)** 的条件下，粒子表面温度由化学反应放热和向周围气体导热散热之间的精细平衡决定。

我们可以通过一个理想化的模型来分析这种耦合 。考虑一个球形碳粒在富氧环境中发生无限快[表面反应](@entry_id:183202) $\mathrm{C} + \mathrm{O}_2 \rightarrow \mathrm{CO}_2$。
1.  **质量扩散**：首先，我们求解[稳态](@entry_id:139253)球对称的物种[守恒方程](@entry_id:1122898)，并应用边界条件：远处氧气质量分数为 $Y_{O_2,\infty}$，粒子表面为零（因反应无限快）。这给出了到达粒子表面的氧气质量通量。
2.  **热量传导**：类似地，我们求解[稳态](@entry_id:139253)球对称的能量方程，边界条件为：远处气体温度为 $T_g$，粒子表面温度为待求的 $T_s$。这给出了从粒子表面传导出去的热流。
3.  **表面能平衡**：在[稳态](@entry_id:139253)下，化学反应释放的热量率 $\dot{Q}_{\text{chem}}$ 必须等于传导走的热量率 $\dot{Q}_{\text{cond}}$。$\dot{Q}_{\text{chem}}$ 与氧气消耗率和[反应焓](@entry_id:149764) $\Delta h_{ox}$ 成正比。

通过联立这三个物理过程，我们可以推导出粒子表面温度 $T_s$ 的表达式 ：

$$
T_s = T_g - \frac{\rho_g D_{O_2} Y_{O_2,\infty} \Delta h_{ox}}{k_g M_{O_2}}
$$

其中 $D_{O_2}$ 是氧气的扩散系数，$M_{O_2}$ 是其[摩尔质量](@entry_id:146110)。一个有趣的发现是，对于这个简化模型，表面温度 $T_s$ 竟然与粒子大小无关。这个方程优雅地将[热物理性质](@entry_id:1133078) ($k_g, \rho_g$)、[输运性质](@entry_id:203130) ($D_{O_2}$) 和[化学热力学](@entry_id:137221)性质 ($Y_{O_2,\infty}, \Delta h_{ox}, M_{O_2}$) 联系在一起，共同决定了反应粒子的温度。

### 粒子运动的[无量纲分析](@entry_id:188181)

为了理解控制粒子动力学的关键物理机制，进行[无量纲分析](@entry_id:188181)是至关重要的。通过将[运动方程](@entry_id:264286)缩放，我们可以识别出决定系统行为的主导参数。让我们以一个正在反应、受重力影响且经历斯托克斯曳力的粒子为例 。

其量纲化的[运动方程](@entry_id:264286)为：

$$
\frac{\mathrm{d}\boldsymbol{v}_{p}}{\mathrm{d}t} = \frac{18\mu}{\rho_{p}d_{p}^{2}}(\boldsymbol{u} - \boldsymbol{v}_{p}) + \boldsymbol{g} + \frac{6\dot{m}''}{\rho_{p}d_{p}}\boldsymbol{v}_{p}
$$

其中我们已经使用了表面质量通量 $\dot{m}''$ 来表示质量变化引起的推力项。使用特征流速 $U_0$、特征长度 $L_0$ 和初始[粒径](@entry_id:161460) $d_0$ 对该方程进行无量纲化，我们得到 ：

$$
\frac{\mathrm{d}\boldsymbol{v}_{p}^{\ast}}{\mathrm{d}t^{\ast}} = \frac{1}{St} \frac{1}{(d^{\ast})^2} (\boldsymbol{u}^{\ast} - \boldsymbol{v}_{p}^{\ast}) - \frac{1}{Fr^2}\boldsymbol{e}_y + \frac{Da_m}{d^{\ast}}\boldsymbol{v}_{p}^{\ast}
$$

这个无量纲方程中出现了三个关键的[无量纲数](@entry_id:260863)：

- **斯托克斯数 (Stokes Number, $St$)**: $St = \frac{\tau_v}{\tau_f} = \frac{\rho_p d_0^2 U_0}{18 \mu L_0}$。它是粒子动量响应时间 $\tau_v = \rho_p d_0^2 / (18\mu)$ 与流体特征时间 $\tau_f = L_0/U_0$ 的比值。这是描述[粒子动力学](@entry_id:1129385)最重要的参数。
    - 若 $St \ll 1$，粒子响应时间远小于流场变化时间，粒子几乎能瞬时适应流体速度，表现为**示踪粒子 (tracer)**。
    - 若 $St \gg 1$，[粒子惯性](@entry_id:195369)极大，其轨迹几乎不受流场局部波动的影响，表现为**弹道式 (ballistic)** 运动。
    - 若 $St \sim 1$，粒子与流场涡旋发生强烈的动态相互作用，导致复杂的行为，如[优先聚集](@entry_id:199717)。

- **弗劳德数 (Froude Number, $Fr$)**: $Fr = U_0 / \sqrt{g L_0}$。其平方的倒数 $\frac{1}{Fr^2} = \frac{gL_0}{U_0^2}$ 代表了重力与流体[惯性力](@entry_id:169104)的比值，衡量了重力对[粒子轨迹](@entry_id:204827)的影响程度。

- **质量达姆科勒数 (Mass Damköhler Number, $Da_m$)**: $Da_m = \frac{6|\dot{m}''|L_0}{\rho_p d_0 U_0}$。它代表了流体特征时间与粒子消耗特征时间的比值，量化了[粒子质量](@entry_id:156313)变化相对于其在流场中输运的快慢。

通过比较这些[无量纲数](@entry_id:260863)的大小，我们可以预判在特定条件下哪个物理过程将主导粒子的行为。

### 粒子与[湍流](@entry_id:151300)的相互作用

反应流本质上几乎总是[湍流](@entry_id:151300)。[湍流](@entry_id:151300)的[随机和](@entry_id:266003)多尺度特性给[粒子追踪](@entry_id:190741)带来了极大的复杂性。

#### 拉格朗日运动学与[湍流弥散](@entry_id:197290)

一个粒子的轨迹，或称**迹线 (pathline)**，是通过对其速度随时间的积分得到的。对于一个给定的速度场 $\boldsymbol{u}(\boldsymbol{x}, t)$，求解[运动学方程](@entry_id:173032) $\mathrm{d}\boldsymbol{x}_p/\mathrm{d}t = \boldsymbol{u}(\boldsymbol{x}_p, t)$ 即可获得迹线。即使对于一个结构看似简单的线性速度场，如果系数是时变的，求解过程也可能相当复杂，有时需要借助[复变量](@entry_id:175312)等数学技巧来获得解析解 。

在[湍流](@entry_id:151300)中，粒子的速度是随机的。对于一个理想的示踪粒子（$St \to 0$），其速度完全跟随[流体速度](@entry_id:267320)。根据G.I. Taylor的经典理论，这种粒子在均匀定常[湍流](@entry_id:151300)中的均方位移 $\langle [x(t)-x(0)]^2 \rangle$ 在长时间后会呈[线性增长](@entry_id:157553)：

$$
\lim_{t \to \infty} \langle [x(t)-x(0)]^2 \rangle = 2 D_{eff} t
$$

这里的 $D_{eff}$ 被称为**有效弥散系数 (effective dispersion coefficient)**，它与[拉格朗日速度自相关](@entry_id:199450)函数有关：

$$
D_{eff} = \int_0^\infty \langle u(t) u(t+\tau) \rangle_L d\tau = \langle u^2 \rangle \tau_L
$$

其中 $\langle u^2 \rangle$ 是速度脉动的方差，$\tau_L$ 是拉格朗日积分时间尺度。在[湍流模型](@entry_id:190404)（如RANS或LES）中，我们需要为未解析的速度脉动提供模型。例如，在基于 $k-\epsilon$ 模型的[随机过程](@entry_id:268487)中，我们通常假设 $\langle u^2 \rangle = \frac{2}{3}k$ 和 $\tau_L \propto k/\epsilon$。因此，未解析尺度引起的[湍流弥散](@entry_id:197290)系数可以被建模为 ：

$$
D_{eff} \propto \frac{k^2}{\epsilon}
$$

这个关系揭示了一个重要的区别：在RANS模拟中，$k$ 和 $\epsilon$ 代表整个湍谱的能量和耗散，因此计算出的弥散效应较强；而在LES中，$k_{sgs}$ 和 $\epsilon_{sgs}$ 仅代表亚格子尺度，因此模拟的[随机弥散](@entry_id:1132419)效应要弱得多，因为大尺度涡的输运作用已被直接解析 。

#### 惯性粒子的[优先聚集](@entry_id:199717)

与理想示踪粒子不同，具有有限惯性（$St \sim 1$）的重粒子（$\rho_p > \rho_f$）不会均匀地分布在[湍流](@entry_id:151300)中。它们倾向于被[离心力](@entry_id:173726)从涡旋中心（高涡量区域）甩出，并聚集在**高应变率、低涡量**的区域。这种现象被称为**[优先聚集](@entry_id:199717) (preferential concentration)**。

这个过程的内在机制可以通过对[粒子速度](@entry_id:196946)进行小[斯托克斯数](@entry_id:185766)的[渐近展开](@entry_id:173196)来揭示 。[粒子速度](@entry_id:196946)可以近似为：

$$
\boldsymbol{v}_p \approx \boldsymbol{u} - \tau_p \frac{D\boldsymbol{u}}{Dt}
$$

取其散度，并利用流体的不可压缩性 $\nabla \cdot \boldsymbol{u} = 0$，我们得到粒子速度场的散度：

$$
\nabla \cdot \boldsymbol{v}_p \approx -\tau_p \nabla \cdot \left(\frac{D\boldsymbol{u}}{Dt}\right)
$$

通过对Navier-Stokes方程取散度，可以得到压力泊松方程，它将流体加速度的散度与[速度梯度张量](@entry_id:270928)的不变量联系起来：$\nabla \cdot (D\boldsymbol{u}/Dt) = S_{ij}S_{ij} - \Omega_{ij}\Omega_{ij} = \chi$。其中 $S_{ij}$ 是[应变率张量](@entry_id:266108)，$\Omega_{ij}$ 是旋转率（[涡量](@entry_id:142747)）张量。因此，我们得到了一个关键关系：

$$
\nabla \cdot \boldsymbol{v}_p \approx -\tau_p \chi
$$

这个表达式的含义是：
- 在应变主导的区域（$\chi > 0$），[粒子速度](@entry_id:196946)场是收敛的（$\nabla \cdot \boldsymbol{v}_p  0$），粒子会在此处聚集。
- 在[涡量](@entry_id:142747)主导的区域（$\chi  0$），[粒子速度](@entry_id:196946)场是发散的（$\nabla \cdot \boldsymbol{v}_p > 0$），粒子会被排出。

这种[优先聚集](@entry_id:199717)效应在反应流中具有深远的影响。如果[化学反应速率](@entry_id:147315)（例如，由标量耗散率驱动）与流场拓扑结构（如 $\chi$）相关，那么惯性粒子将会优先采样流场中的特定区域。这将导致沿[粒子轨迹](@entry_id:204827)测量的平均[反应速率](@entry_id:185114) $\langle R \rangle_{\text{inertial}}$ 与真实的欧拉平均（或示踪粒子平均）$\langle R \rangle_{\text{tracer}}$ 之间存在偏差。这个偏差的大小与[粒子惯性](@entry_id:195369)（$\tau_p$）以及[反应速率](@entry_id:185114)场与流场结构（$\chi$）的[关联强度](@entry_id:924074)成正比 。

理解这些基本原理和机制是进行任何有意义的[反应流](@entry_id:190741)拉格朗日[粒子模拟](@entry_id:144357)的先决条件。它们构成了更高级模型和计算方法的基础，并为解释模拟结果提供了必要的物理洞察力。