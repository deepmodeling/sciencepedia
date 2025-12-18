## 引言
在计算热工领域，涉及熔化与凝固的相变过程无处不在，从金属铸造到冰川消融，其[精确模拟](@entry_id:749142)对于科学研究和工程设计至关重要。这类过程的数学描述通常归结为一个经典的[移动边界问题](@entry_id:170533)——[斯特凡问题](@entry_id:154099)。其核心挑战在于，固液[相界面](@entry_id:172947)本身的位置是未知的，并且其运动与温度场紧密耦合，这使得问题具有高度的[非线性](@entry_id:637147)和求解难度。本文旨在系统性地梳理和阐释用于解决[斯特凡问题](@entry_id:154099)的关键[数值离散化](@entry_id:752782)技术，填补理论物理与计算实践之间的知识鸿沟。

本文将通过三个循序渐进的章节，为读者构建一个完整的知识体系。首先，在“原理与机制”一章中，我们将深入探讨[斯特凡问题](@entry_id:154099)的物理基础和数学表述，从经典的锐利界面模型出发，逐步引入求解该问题的核心数值策略，包括前沿固定法、[焓法](@entry_id:148184)和[相场法](@entry_id:191689)。接着，“应用与跨学科联系”一章将展示这些理论和方法在材料科学、地球物理、航空航天等多个领域的实际应用，揭示其解决复杂工程问题的强大能力。最后，“动手实践”部分将提供一系列精心设计的编程练习，帮助读者将理论知识转化为实际的计算技能。通过本文的学习，读者将能够深刻理解并掌握处理相变问题的现代计算方法。

## 原理与机制

本章旨在深入阐述[相变传热](@entry_id:149240)问题（即[斯特凡问题](@entry_id:154099)）的核心物理原理及其计算建模中的关键机制。在前一章介绍背景的基础上，本章将从经典的锐利界面模型出发，系统地建立控制方程和[界面条件](@entry_id:750725)。随后，我们将探讨模型的简化、扩展，并最终介绍求解这些问题的三种主流数值方法：前沿固定法、[焓法](@entry_id:148184)和[相场法](@entry_id:191689)。通过本章的学习，读者将掌握从基本物理定律到高级计算方法的完整知识体系，为解决复杂的工程相变问题奠定坚实的理论基础。

### 经典[斯特凡问题](@entry_id:154099)：锐利界面表述

在宏观尺度上，固相和液相通常由一个厚度可忽略不计的锐利界面隔开。描述此类问题的数学模型被称为**经典[斯特凡问题](@entry_id:154099) (classical Stefan problem)**。该模型由两部分组成：描述体相传热的[偏微分](@entry_id:194612)方程和描述[界面演化](@entry_id:750730)的特殊边界条件。

#### 体相控制方程与边界条件

在没有内热源且仅考虑[热传导](@entry_id:143509)的情况下，能量守恒定律与[傅里叶定律](@entry_id:136311)相结合，得到每个相（固相 $\alpha=s$ 和液相 $\alpha=\ell$）内部的温度场 $T_\alpha(\mathbf{x}, t)$ 满足的**[热传导方程](@entry_id:194763) (heat equation)**：

$$
\rho_\alpha c_\alpha \frac{\partial T_\alpha}{\partial t} = \nabla \cdot (k_\alpha \nabla T_\alpha)
$$

其中，$\rho_\alpha$ 是密度，$c_\alpha$ 是比热容，$k_\alpha$ 是[热导](@entry_id:189019)率。这些物性参数在每个相内部可视为常数，但在相间可能存在差异。如果物性为常数，方程可简化为 $\partial_t T_\alpha = \alpha_\alpha \nabla^2 T_\alpha$，其中 $\alpha_\alpha = k_\alpha / (\rho_\alpha c_\alpha)$ 是热扩散系数。

为了确定一个唯一解，除了上述控制方程，还必须提供适当的**初始条件 (initial conditions)** 和**边界条件 (boundary conditions)**。初始条件包括初始时刻 $t=0$ 的界面位置 $s(0)$ 以及固液两相中的初始温度分布 $T_s(\mathbf{x}, 0)$ 和 $T_\ell(\mathbf{x}, 0)$。边界条件则指定了计算区域外部边界上的热学状态，例如固定温度（[狄利克雷条件](@entry_id:137096)）或固定热流（[诺伊曼条件](@entry_id:165471)）。

#### 界面条件

界面的存在是[斯特凡问题](@entry_id:154099)的核心特征，其行为由两个关键的物理条件决定。

##### [热力学平衡](@entry_id:141660)与[温度连续性](@entry_id:755837)

经典模型的一个基本假设是**[局部热力学平衡](@entry_id:147993) (Local Thermodynamic Equilibrium, LTE)**。对于在固定压力下发生相变的纯物质，固液两相只能在一个唯一的温度下共存，即**平衡熔点 (equilibrium melting temperature)** $T_m$。因此，在锐利界面 $s(t)$ 上，温度必须是连续的，并且等于 $T_m$：

$$
T_s(s(t), t) = T_\ell(s(t), t) = T_m
$$

这个条件从[热力学](@entry_id:172368)角度“钉住”了界面的温度。从计算角度看，它为每个子区域的求解提供了狄利克雷边界条件。值得注意的是，虽然温度是连续的，但其梯度（即热流）通常是不连续的，这直接引出了下一个关键条件。

在某些极端情况下，例如极快的相变速率或微观尺度下的传热，LTE假设可能不成立。此时，界面上可能出现温度跳跃（如由**[卡皮察电阻](@entry_id:152481) (Kapitza resistance)** 引起）或界面温度偏离 $T_m$（如**动力学过冷/过热 (kinetic undercooling/superheating)**）。我们将在后续章节探讨这些更复杂的情况。

##### [斯特凡条件](@entry_id:149175)：界面能量平衡

由于界面本身没有厚度，不存储能量，因此流入界面的净热流必须恰好等于相变过程吸收或释放的**潜热 (latent heat)**。这个能量平衡关系被称为**[斯特凡条件](@entry_id:149175) (Stefan condition)**。

当界面以法向速度 $V_n$ 移动时，相变吸收或释放的能量速率为 $\rho L V_n$，其中 $L$ 是单位质量的潜热。这部分能量必须由界面两侧的[净热通量](@entry_id:155652)提供。设法向 $\mathbf{n}$ 指向液相。根据傅里叶定律 $\mathbf{q} = -k \nabla T$，从液相流向界面的热通量为 $-\mathbf{q}_\ell \cdot \mathbf{n}$，从固相流向界面的热通量为 $-\mathbf{q}_s \cdot \mathbf{n}$。不，更严谨的推导是基于界面上的热流跳跃。界面处的能量平衡可写为：
$$
\rho L V_n = (\text{来自液相的热流}) - (\text{流向固相的热流})
$$
用热[通量矢量](@entry_id:273577) $\mathbf{q}$ 表示，即 $\rho L V_n = \mathbf{q}_\ell \cdot (-\mathbf{n}) - \mathbf{q}_s \cdot (-\mathbf{n}) = (\mathbf{q}_s - \mathbf{q}_\ell) \cdot \mathbf{n}$。将[傅里叶定律](@entry_id:136311) $\mathbf{q} = -k \nabla T$ 代入，得到[斯特凡条件](@entry_id:149175)的[标准形式](@entry_id:153058)：

$$
\rho L V_n = k_s \left. \frac{\partial T_s}{\partial n} \right|_{s(t)} - k_\ell \left. \frac{\partial T_\ell}{\partial n} \right|_{s(t)}
$$

其中 $\partial / \partial n = \mathbf{n} \cdot \nabla$ 表示法向导数。该方程明确指出，界面速度 $V_n$ 由界面两侧的热流密度跳变 $[k \, \partial T / \partial n]_s - [k \, \partial T / \partial n]_\ell$ 决定。这正是[斯特凡问题](@entry_id:154099)的[非线性](@entry_id:637147)性和求解难度的根源：温度场决定了[界面运动](@entry_id:1126592)，而[界面运动](@entry_id:1126592)又反过来改变了温度场的求解域 。

作为一个具体例子，考虑一个厚度为 $L=0.02$ m 的一维平板，固相区为 $x \in [0, s(t)]$，液相区为 $x \in [s(t), L]$。边界温度分别为 $T(0)=-10^\circ\text{C}$ 和 $T(L)=20^\circ\text{C}$，[熔点](@entry_id:195793)为 $T_m=0^\circ\text{C}$。在某个瞬间，界面位于 $s=0.008$ m。我们用线性温度分布来近似界面两侧的温度梯度：
$$
\left.\frac{\partial T_s}{\partial x}\right|_{s} \approx \frac{T_m - T(0)}{s} = \frac{0 - (-10)}{0.008} = 1250 \text{ K/m}
$$
$$
\left.\frac{\partial T_\ell}{\partial x}\right|_{s} \approx \frac{T(L) - T_m}{L - s} = \frac{20 - 0}{0.02 - 0.008} \approx 1667 \text{ K/m}
$$
设固态[热导](@entry_id:189019)率 $k_s = 2.2 \text{ W/(m·K)}$，液态[热导](@entry_id:189019)率 $k_\ell = 0.6 \text{ W/(m·K)}$，密度 $\rho = 917 \text{ kg/m}^3$，潜热 $L_h = 3.34 \times 10^5 \text{ J/kg}$。在一维情况下，法向为 $+x$ 方向，法向速度为 $\dot{s}$，[斯特凡条件](@entry_id:149175)为：
$$
\rho L_h \dot{s} = k_s \left.\frac{\partial T_s}{\partial x}\right|_{s} - k_\ell \left.\frac{\partial T_\ell}{\partial x}\right|_{s}
$$
将数值代入，我们得到从界面传导至固相的热流密度为 $q''_s = k_s \left.\frac{\partial T_s}{\partial x}\right|_{s} = 2.2 \times 1250 = 2750 \text{ W/m}^2$。从液相传导至界面的热流密度为 $q''_\ell = k_\ell \left.\frac{\partial T_\ell}{\partial x}\right|_{s} = 0.6 \times 1667 \approx 1000 \text{ W/m}^2$。由于流入界面的热流（$1000 \text{ W/m}^2$）小于流出界面的热流（$2750 \text{ W/m}^2$），存在 $1750 \text{ W/m}^2$ 的能量赤字，这必须由界面凝固释放的潜热来补偿，因此界面将向右移动（$\dot{s}>0$，即熔化）。等一下，物理描述有误。能量平衡为：流入的热量 = 流出的热量 + 相变吸收的热量。即 $q''_\ell = q''_s + \rho L_h \dot{s}$。因此 $\rho L_h \dot{s} = q''_\ell - q''_s = 1000 - 2750 = -1750 \text{ W/m}^2$。这意味着 $\dot{s}$ 为负，即发生[凝固](@entry_id:156052)。

让我们重新检查计算：
$$
\dot{s} = \frac{1}{\rho L_h} \left( k_s \frac{\partial T_s}{\partial x} - k_\ell \frac{\partial T_\ell}{\partial x} \right) = \frac{1}{917 \times 3.34 \times 10^5} (2750 - 1000) \approx 5.714 \times 10^{-6} \text{ m/s}
$$
这里计算出的 $\dot{s}$ 是正值，表示熔化。这与我们上面物理推断的[凝固](@entry_id:156052)相矛盾。让我们检查热流跳跃公式：$\rho L \dot{s} = q_l(s) - q_s(s)$，其中 $q(s)$ 是在 $x=s$ 处的通量，定义为 $q = -k \frac{\partial T}{\partial x}$。所以 $\rho L \dot{s} = \left(-k_\ell \frac{\partial T_\ell}{\partial x}\right) - \left(-k_s \frac{\partial T_s}{\partial x}\right) = k_s \frac{\partial T_s}{\partial x} - k_\ell \frac{\partial T_\ell}{\partial x}$。这个公式是正确的，并且与数值计算一致。因此，物理描述“流入的热量 = 流出的热量 + ...”导致了混淆。正确的物理图像是，界面处的能量不平衡（即热流跳跃 $q_l - q_s$）驱动了相变。将数值代入，净热流跳变为 $q_l - q_s = -1000 - (-2750) = 1750 \text{ W/m}^2$。这个正值驱动了熔化。
$$
\dot{s} = \frac{1750}{917 \times 3.34 \times 10^5} \approx 5.714 \times 10^{-6} \text{ m/s}
$$
这个计算清晰地展示了如何利用界面两侧的温度信息来确定界面的瞬时运动速度 。

### [模型简化](@entry_id:171175)与扩展

完整的两相[斯特凡问题](@entry_id:154099)在求解上可能非常复杂。在特定物理情境下，可以对其进行简化或扩展。

#### 单相与两相模型

在许多工程应用中，可以对模型进行简化。最常见的简化是**单相斯特凡模型 (one-phase Stefan model)**。

- **两相模型 (Two-phase model)**：这是我们前面描述的完整模型，需要在固、液两个区域内同时求解[热传导方程](@entry_id:194763)，并通过完整的[斯特凡条件](@entry_id:149175)（即热流跳变）来确定界面速度 。

- **单相模型 (One-phase model)**：当其中一个相（例如液相）的导热能力非常强，或者存在剧烈的对流使得该相的温度[几乎处处](@entry_id:146631)均匀并等于熔点 $T_m$ 时，我们就可以忽略该相内的温度梯度，即 $\nabla T_\ell \approx 0$。此时，我们只需在另一个相（固相）中求解[热传导方程](@entry_id:194763)。[斯特凡条件](@entry_id:149175)也随之简化，因为来自液相的热流项消失了：

$$
\rho L V_n = k_s \left. \frac{\partial T_s}{\partial n} \right|_{s(t)}
$$

这种简化极大地降低了计算的复杂度，因为我们只需处理一个求解域，并且界面条件也变得更简单 。

这种简化的合理性可以通过[量纲分析](@entry_id:140259)来评估。关键的无量纲参数是**[斯特凡数](@entry_id:162817) (Stefan number)** $\mathrm{Ste} = c \Delta T / L$，它代表了显热与潜热的相对重要性。当液相的过热度很小，即液相[斯特凡数](@entry_id:162817) $\mathrm{Ste}_\ell = c_\ell (T_i - T_m)/L \ll 1$（其中 $T_i$ 是液体初始温度）时，意味着液体携带的显热远小于相变潜热，因此可以近似认为液体对[界面运动](@entry_id:1126592)的贡献可以忽略。更精确的[误差分析](@entry_id:142477)表明，单相近似引入的[相对误差](@entry_id:147538) $\epsilon$ 大致与 $\mathrm{Ste}_\ell / \mathrm{Ste}_s$ 成正比（其中 $\mathrm{Ste}_s$ 是固相的[斯特凡数](@entry_id:162817)）。此外，边界的热流条件（通过**毕渥数 (Biot number)** $\mathrm{Bi}$ 表征）也会影响误差的大小。只有当 $\mathrm{Ste}_\ell$ 足够小且 $\mathrm{Bi}$ 不至于过小时，单相模型才是有效的近似 。

#### 吉布斯-汤姆逊效应

经典斯特凡模型假设界面温度恒为 $T_m$，这仅对平直界面严格成立。当界面发生弯曲时，**[界面能](@entry_id:198323) (interface energy)** 或**表面张力 (surface tension)** 的存在会导致平衡温度的改变。这种现象被称为**吉布斯-汤姆逊效应 (Gibbs-Thomson effect)**。

根据热力学原理，一个凸起的固相（例如，凝固过程中形成的晶核）比平直界面更不稳定，其平衡[熔点](@entry_id:195793)会降低。对于各向同性的表面张力，界面温度 $T_\Gamma$ 与其[平均曲率](@entry_id:162147) $\kappa$ 存在线性关系：

$$
T_\Gamma = T_m - \Gamma \kappa - \mu V_n
$$

- **曲率项 $(-\Gamma \kappa)$**：$\Gamma$ 是一个正的**吉布斯-汤姆逊系数**，它与表面张力成正比。按照惯例，若法向指向液体，则凸起固相的曲率 $\kappa > 0$，此项为负，导致温度下降。反之，凹陷的固[相界面](@entry_id:172947)（$\kappa  0$）温度会升高。

- **动力学项 $(-\mu V_n)$**：$\mu$ 是一个正的**动力学系数**。此项表示，要驱动界面以有限速度 $V_n$ 运动，需要一个偏离平衡的驱动力，即**动力学过冷**。对于凝固（$V_n  0$），界面实际温度必须低于当前的平衡温度；对于熔化（$V_n  0$），则需要过热。

这个修正后的温度条件是模拟[枝晶生长](@entry_id:155385)等复杂形态演变的关键。在数值计算中，需要精确计算界面的曲率 $\kappa$。例如，在使用水平集方法时，曲率可以通过对[水平集](@entry_id:751248)函数 $\phi$ 的导数进行[中心差分](@entry_id:173198)来获得二阶精度的近似值 。

### [斯特凡问题](@entry_id:154099)的数值方法

求解[斯特凡问题](@entry_id:154099)的主要挑战在于如何处理移动的、其位置本身也是待求一部分的[相界面](@entry_id:172947)。数值方法大致可分为两大类：追踪界面位置的**锐利界面法 (sharp-interface methods)** 和在整个固定网格上求解的**弥散界面/[固定域](@entry_id:155430)法 (diffuse-interface/fixed-domain methods)**。

#### 前沿追踪与前沿固定法

这类方法的核心思想是显式地表示和追踪界面的位置。例如，界面可以由一系列拉格朗日网格点描述。然而，当界面拓扑结构发生复杂变化（如合并或断裂）时，这类方法会变得异常困难。

一个巧妙的变种是**前沿固定法 (front-fixing method)**，其中最著名的是一维问题中的**朗道变换 (Landau transformation)**。通过引入一个新的坐标变量，例如 $\xi = x/s(t)$，将随时间变化的物理域 $x \in [0, s(t)]$ 映射到一个固定的计算域 $\xi \in [0, 1]$。

通过[链式法则](@entry_id:190743)，原始的[热传导方程](@entry_id:194763) $\rho c \partial_t T = k \partial_x^2 T$ 在新的 $(\xi, t)$ 坐标系下会转变为一个更复杂的形式。对时间导数的变换是关键：

$$
\frac{\partial T}{\partial t} = \frac{\partial \theta}{\partial t} + \frac{\partial \theta}{\partial \xi} \frac{\partial \xi}{\partial t} = \frac{\partial \theta}{\partial t} - \frac{\partial \theta}{\partial \xi} \frac{\xi \dot{s}(t)}{s(t)}
$$

其中 $\theta(\xi, t) = T(x, t)$。变换后的[热传导方程](@entry_id:194763)变为：

$$
\rho c \frac{\partial \theta}{\partial t} = \frac{k}{s(t)^2} \frac{\partial^2 \theta}{\partial \xi^2} + \rho c \frac{\xi \dot{s}(t)}{s(t)} \frac{\partial \theta}{\partial \xi}
$$

可以观察到，方程中出现了一个**伪对流项 (fictitious convective term)**，其系数与界面速度 $\dot{s}(t)$ 成正比。尽管方程变复杂了，但它现在可以在一个固定的、均匀的网格上进行求解，大大简化了数值离散。[斯特凡条件](@entry_id:149175)本身也变换为关于 $s(t)$ 的常微分方程，与[偏微分](@entry_id:194612)方程耦合求解 。

#### [固定域](@entry_id:155430)方法之一：[焓法](@entry_id:148184)

与追踪界面不同，**[焓法](@entry_id:148184) (enthalpy method)** 采用了一种完全不同的哲学：它在一个固定的计算域上求解一个单一的能量方程，而界面位置则是事后从求解结果中隐式地确定。

该方法的核心是引入**体积焓 (volumetric enthalpy)** $H$ 作为基本求解变量。焓被定义为显热和潜热之和：

$$
H(T) = \int_{T_{\text{ref}}}^T \rho c(\theta) d\theta + \rho L \chi(T)
$$

其中，第一项是显热，第二项是潜热。$\chi(T)$ 是**液相分数 (liquid fraction)** 函数，它随温度变化，从固相的 $0$ 平滑过渡到液相的 $1$。例如，对于在温度区间 $[T_s, T_l]$ 内发生相变的“[糊状区](@entry_id:147943) (mushy zone)”，可以定义：

$$
\chi(T) = 
\begin{cases}
0,  T \le T_s \\
\frac{T - T_s}{T_l - T_s},  T_s  T  T_l \\
1,  T \ge T_l
\end{cases}
$$

对于在单一熔点 $T_m$ 发生相变的纯物质，这对应于 $T_s = T_l = T_m$ 的极限情况，此时 $\chi(T)$ 变为一个[阶跃函数](@entry_id:159192) 。

将[焓的定义](@entry_id:137586)代入能量守恒方程 $\partial_t H = \nabla \cdot (k \nabla T)$，我们得到了一个在整个计算域上都有效的**单一[偏微分](@entry_id:194612)方程**。这个方程的巧妙之处在于，它通过[非线性](@entry_id:637147)的 $H(T)$ 关系将潜热效应“吸收”到了方程本身。我们可以定义一个**有效热容 (effective heat capacity)** $c_{\text{eff}}(T) = dH/dT = \rho c(T) + \rho L (d\chi/dT)$。在相变区域，由于 $d\chi/dT$ 很大（对于纯物质是狄拉克 $\delta$ 函数），有效热容会急剧增大，从而在不显式追踪界面的情况下正确地吸收或释放潜热 。

在数值上，例如使用[有限体积法 (FVM)](@entry_id:749403)，可以在每个控制体中守恒地更新焓 $H$，然后再通过反查[非线性](@entry_id:637147)的 $H(T)$ 关系来得到新的温度 $T$。这种方法的优点是稳健、易于实现，并且能够自然地处理复杂的[拓扑变化](@entry_id:136654)，因此在工程计算中得到了广泛应用 。

#### [固定域](@entry_id:155430)方法之二：[相场法](@entry_id:191689)

**[相场法](@entry_id:191689) (phase-field method)** 是另一种更先进的[固定域](@entry_id:155430)方法，它将物理上锐利的界面在数学上处理为一个具有有限厚度 $\epsilon$ 的**弥散过渡区**。该方法引入一个连续的**[序参量](@entry_id:144819) (order parameter)** 场 $\psi(\mathbf{x}, t)$ 来描述相态，例如，$\psi \approx +1$ 代表固相，$\psi \approx -1$ 代表液相，而界面则对应于 $\psi \approx 0$ 的区域。

[序参量](@entry_id:144819)的演化由一个[偏微分](@entry_id:194612)方程（如 Allen-Cahn 方程）描述，该方程基于系统的总[自由能泛函](@entry_id:184428)导出。一个典型的[相场模型](@entry_id:1129578)系统如下：

$$
\partial_t \psi = M \left( \epsilon^2 \nabla^2 \psi - f'(\psi) \right) + \lambda (T - T_m)
$$
$$
\rho c \partial_t T = k \nabla^2 T + \frac{L}{2} \partial_t \psi
$$

第一式描述序参量的演化。$f(\psi)$ 是一个[双势阱](@entry_id:171252)函数，其极小值对应于稳定相。$\epsilon^2 \nabla^2 \psi$ 项引入了[界面能](@entry_id:198323)。与温度的耦合项 $\lambda(T-T_m)$ 提供了相变的热力学驱动力。第二式是[热传导方程](@entry_id:194763)，其中源项 $(L/2) \partial_t \psi$（$L$为体积潜热）表示[相变过程](@entry_id:147919)中的潜热释放或吸收，它将能量方程与相场演化耦合起来。

[相场法](@entry_id:191689)的强大之处在于其深厚的[热力学](@entry_id:172368)基础。通过严谨的**[渐近分析](@entry_id:1121160)**可以证明，在界面厚度 $\epsilon \to 0$ 的**锐利界面极限 (sharp-interface limit)** 下，[相场模型](@entry_id:1129578)能够自动恢复正确的宏观界面条件，包括[斯特凡条件](@entry_id:149175)和（带有曲率和动力学效应的）吉布斯-汤姆逊条件。这表明[相场法](@entry_id:191689)不仅是一种数值技巧，更是一个在介观尺度上统一描述了[热力学](@entry_id:172368)和动力学过程的物理模型 。

在数值实现上，[相场法](@entry_id:191689)也受益于固定网格，并且其控制方程通常是平滑的，易于使用标准方法（如有限差分或有限元）离散。采用合适的半[隐式时间积分格式](@entry_id:1126422)，可以构建出既保持能量守恒又具有良好稳定性的数值方案 。