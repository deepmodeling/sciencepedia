## 引言
在多体[费米子](@entry_id:146235)构成的量子世界中，个体的复杂相互作用如何涌现出协调一致的集体行为，是一个贯穿近代物理学的核心问题。从[金属中的电子](@entry_id:138687)到液态[氦-3](@entry_id:195175)，再到[中子星](@entry_id:147259)的核心，这些系统中的集体激发模式不仅揭示了物质的宏观响应特性，更蕴含着微观相互作用的深刻信息。在众多[集体模](@entry_id:137129)式中，**[零声](@entry_id:142772) (Zero Sound)** 作为一种纯粹的量子现象，尤为引人注目。它不同于我们日常经验中由[粒子碰撞](@entry_id:160531)传播的普通声波（[第一声](@entry_id:144225)），而是一种在几乎没有碰撞的极限下，由粒子间自洽平均场维持的密度[振荡](@entry_id:267781)。

本文旨在系统性地阐明[零声](@entry_id:142772)及相关集体模式的物理。我们将以[朗道费米液体理论](@entry_id:151062)为基石，解决“相互作用如何驱动一种新的、无碰撞的[声学模](@entry_id:263916)式”这一核心问题。读者将通过本文的学习，构建一个从微观机制到宏观应用的完整知识框架。

-   **第一章：原理与机制** 将深入[朗道费米液体理论](@entry_id:151062)的核心，建立描述[准粒子](@entry_id:136584)动力学的方程，并详细剖析[第一声](@entry_id:144225)与[零声](@entry_id:142772)的本质区别、[零声](@entry_id:142772)的产生机制、传播条件及其与[朗道阻尼](@entry_id:137619)的联系。
-   **第二章：应用与交叉学科联系** 将展示这些理论概念的强大生命力，通过液态氦-3、金属中的等离激元、[核物质](@entry_id:158311)与[中子星](@entry_id:147259)、以及[超冷原子气体](@entry_id:143830)等实例，探讨[零声](@entry_id:142772)在不同物理情境下的表现及其作为探测工具的重要作用。
-   **第三章：动手实践** 提供了一系列精心设计的问题，旨在通过计算加深对[朗道阻尼](@entry_id:137619)、[弱耦合](@entry_id:140994)与强耦合极限下[零声](@entry_id:142772)行为的理解，将理论知识转化为解决实际问题的能力。

通过这三个层次的递进，本文将引导您深入探索[费米液体](@entry_id:142392)中迷人的[集体动力学](@entry_id:204455)世界。

## 原理与机制

本章旨在深入探讨费米液体中[集体模](@entry_id:137129)式，特别是[零声](@entry_id:142772)的物理原理与微观机制。我们将从[朗道费米液体理论](@entry_id:151062)的基本概念出发，建立描述[准粒子](@entry_id:136584)动力学的方程，并在此基础上揭示不同动力学区间内集体行为的本质区别。随后，我们将详细剖析[零声](@entry_id:142772)的产生机制、传播条件及其与[准粒子相互作用](@entry_id:146832)的深刻联系。最后，我们会将理论与实验观测联系起来，并讨论该理论在更广泛物理情境（如带电系统和[晶格](@entry_id:196752)环境）下的拓展和应用。

### [朗道费米液体理论](@entry_id:151062)基础

[朗道费米液体理论](@entry_id:151062)的基石是**[准粒子](@entry_id:136584)**（quasiparticle）的概念。在一个相互作用的[费米子](@entry_id:146235)系统中，低能[激发态](@entry_id:261453)与无[相互作用费米气体](@entry_id:160307)的[基态](@entry_id:150928)和低能[激发态](@entry_id:261453)之间存在[一一对应](@entry_id:143935)关系。这些携带了相互作用“云”的有效粒子就是[准粒子](@entry_id:136584)。它们拥有明确的动量 $\hbar\mathbf{k}$ 和自旋 $\sigma$，其行为由[分布函数](@entry_id:145626) $n_{\mathbf{k}\sigma}$ 描述。系统的总能量 $E$ 是该[分布函数](@entry_id:145626)的泛函。[准粒子](@entry_id:136584)的能量 $\epsilon_{\mathbf{k}\sigma}$ 被定义为系统总能量对[准粒子](@entry_id:136584)占据数 $n_{\mathbf{k}\sigma}$ 的泛函微商：

$$
\epsilon_{\mathbf{k}\sigma} = \frac{\delta E}{\delta n_{\mathbf{k}\sigma}}
$$

这个定义的核心在于，一个[准粒子](@entry_id:136584)的能量 $\epsilon_{\mathbf{k}\sigma}$ 自身依赖于系统中所有其他[准粒子](@entry_id:136584)的[分布](@entry_id:182848)，这正是相互作用效应的体现。

[准粒子](@entry_id:136584)之间的相互作用由**朗道相互作用函数**（Landau interaction function）$f_{\mathbf{k}\sigma, \mathbf{k}'\sigma'}$ 描述。它被定义为总能量对占据数的二阶泛函微商，物理上表示在 $(\mathbf{k}', \sigma')$ 态增加一个[准粒子](@entry_id:136584)对 $(\mathbf{k}, \sigma)$ 态[准粒子能量](@entry_id:173936)的影响：

$$
f_{\mathbf{k}\sigma, \mathbf{k}'\sigma'} = \frac{\delta \epsilon_{\mathbf{k}\sigma}}{\delta n_{\mathbf{k}'\sigma'}} = \frac{\delta^2 E}{\delta n_{\mathbf{k}\sigma} \delta n_{\mathbf{k}'\sigma'}}
$$

对于一个均匀、各向同性、顺磁性的费米液体（例如[液氦-3](@entry_id:147785)），由于体系具有平移、旋转和自旋[旋转不变性](@entry_id:137644)，[费米面](@entry_id:137798)上的相互作用函数仅依赖于动量 $\mathbf{k}$ 和 $\mathbf{k}'$ 之间的夹角 $\theta$ 以及自旋的相对取向。其最普遍的形式可以分解为自旋对称和自旋反对称两部分：

$$
f_{\mathbf{k}\sigma, \mathbf{k}'\sigma'} = f^{s}(\cos\theta) + f^{a}(\cos\theta)\,\boldsymbol{\sigma}\cdot\boldsymbol{\sigma}'
$$

其中 $f^s(\cos\theta)$ 描述了与密度涨落耦合的自旋无关相互作用，而 $f^a(\cos\theta)$ 描述了与自旋密度涨落耦合的相互作用。

为了便于分析，通常将这两个函数在费米面上按[勒让德多项式](@entry_id:141510) $P_{\ell}(\cos\theta)$ 展开。这定义了有量纲的[朗道参数](@entry_id:144630) $f_{\ell}^{s,a}$。为了得到无量纲的参数，我们乘以[费米能级](@entry_id:143215)处的[态密度](@entry_id:147894) $N(0)$（单位能量、单位体积、单个自旋方向的[态密度](@entry_id:147894)）。由此，我们得到了物理上至关重要的**无量纲[朗道参数](@entry_id:144630)**（dimensionless Landau parameters）$F_{\ell}^{s,a}$ [@problem_id:3024843]：

$$
F_{\ell}^{s,a} = N(0) f_{\ell}^{s,a} \quad \text{其中} \quad f^{s,a}(\cos\theta) = \sum_{\ell=0}^{\infty} f_{\ell}^{s,a} P_{\ell}(\cos\theta)
$$

这些[朗道参数](@entry_id:144630) $F_{\ell}^{s,a}$ 是现象学参数，编码了系统中复杂的相互作用信息，并直接决定了[费米液体](@entry_id:142392)的宏观响应性质，如有效质量、压缩率、磁化率以及我们将要讨论的集体模式的行为。

### [准粒子](@entry_id:136584)动力学：朗道[动力学方程](@entry_id:751029)

为了描述[费米液体](@entry_id:142392)中集体模式的动力学行为，我们需要一个能够刻画准[粒子分布函数](@entry_id:753202) $n_{\mathbf{k}}(\mathbf{r}, t)$ 时空演化的方程。在[半经典近似](@entry_id:147497)下，这个方程就是**朗道动力学方程**（Landau kinetic equation），也常被称为玻尔兹曼-朗道方程。它具有[刘维尔方程](@entry_id:156422)的一般形式，即相空间中的[分布函数](@entry_id:145626)沿着[准粒子](@entry_id:136584)运动轨迹的[流函数](@entry_id:266505)导数为零，加上一个描述碰撞的项：

$$
\frac{\partial n_{\mathbf{k}}}{\partial t} + \dot{\mathbf{r}} \cdot \nabla_{\mathbf{r}} n_{\mathbf{k}} + \dot{\mathbf{k}} \cdot \nabla_{\mathbf{k}} n_{\mathbf{k}} = \mathcal{I}_{\text{coll}}[n]
$$

这里的 $\dot{\mathbf{r}}$ 和 $\dot{\mathbf{k}}$ 是[准粒子](@entry_id:136584)的[半经典运动方程](@entry_id:138500)，由哈密顿形式给出，其中[准粒子能量](@entry_id:173936) $\epsilon_{\mathbf{k}}(\mathbf{r},t)$ 扮演了[哈密顿量](@entry_id:172864)的角色：$\dot{\mathbf{r}} = \nabla_{\mathbf{k}} \epsilon_{\mathbf{k}}$ 和 $\dot{\mathbf{k}} = -\nabla_{\mathbf{r}} \epsilon_{\mathbf{k}}$。

考虑一个小的偏离[平衡分布](@entry_id:263943) $n^0_{\mathbf{k}}$ 的涨落 $\delta n_{\mathbf{k}}(\mathbf{r}, t)$，它是由一个弱的外部标量势 $U_{\text{ext}}(\mathbf{r}, t)$ 引起的。[准粒子能量](@entry_id:173936)也相应地偏离其平衡值 $\epsilon^0_{\mathbf{k}}$，其变化量 $\delta\epsilon_{\mathbf{k}}$ 由两部分构成：外部势和由[密度涨落](@entry_id:143540)自身产生的自洽平均场：

$$
\delta\epsilon_{\mathbf{k}}(\mathbf{r},t) = U_{\text{ext}}(\mathbf{r},t) + \sum_{\mathbf{k}'} f_{\mathbf{k}\mathbf{k}'} \delta n_{\mathbf{k}'}(\mathbf{r},t)
$$

将这些关系代入[动力学方程](@entry_id:751029)并只保留至 $\delta n$ 的一阶项，我们便得到线性化的朗道[动力学方程](@entry_id:751029) [@problem_id:3024846]：

$$
\frac{\partial \delta n_{\mathbf{k}}}{\partial t} + \mathbf{v}_{\mathbf{k}} \cdot \nabla_{\mathbf{r}} \delta n_{\mathbf{k}} - \nabla_{\mathbf{r}}\!\left[ U_{\text{ext}} + \sum_{\mathbf{k}'} f_{\mathbf{k}\mathbf{k}'} \delta n_{\mathbf{k}'} \right]\! \cdot \nabla_{\mathbf{k}} n^0_{\mathbf{k}} = \mathcal{I}_{\text{coll}}[\delta n]
$$

其中 $\mathbf{v}_{\mathbf{k}} = \nabla_{\mathbf{k}}\epsilon^0_{\mathbf{k}}$ 是平衡态下的准粒子速度。该方程的左边描述了[准粒子](@entry_id:136584)的相干动力学：第一项是时间演化项，第二项是描述[准粒子](@entry_id:136584)自由运动的**漂移项**（drift term），第三项是**力项**（force term），它描述了[准粒子](@entry_id:136584)在空间变化的自洽势场中的加速。右边的**[碰撞积分](@entry_id:152100)项** $\mathcal{I}_{\text{coll}}$ 描述了非相干的散射过程，它驱动系统趋向于[局域平衡](@entry_id:156295)。这个方程是研究[费米液体](@entry_id:142392)中所有[集体模](@entry_id:137129)式的出发点。

### [集体动力学](@entry_id:204455)的两种机制：[第一声](@entry_id:144225)和[零声](@entry_id:142772)

朗道动力学方程中的漂移项/力项与碰撞项的相对重要性，由一个关键的无量纲参数 $\omega\tau$ 决定。这里，$\omega$ 是集体振荡的[角频率](@entry_id:261565)，而 $\tau$ 是费米面上[准粒子](@entry_id:136584)的平均[碰撞时间](@entry_id:261390)。这个参数将[集体动力学](@entry_id:204455)划分为两个截然不同的物理区间 [@problem_id:3024823]。

1.  **[流体动力学](@entry_id:136788)区间 ($\omega\tau \ll 1$)：[第一声](@entry_id:144225)**
    当振荡频率远低于碰撞频率时 ($\omega \ll 1/\tau$)，$\omega\tau \ll 1$。这意味着在一个[振荡周期](@entry_id:271387)内，[准粒子](@entry_id:136584)会经历多次碰撞。频繁的碰撞使得系统能够迅速地达到**局域热力学平衡**。此时，系统的动力学行为由宏观的守恒律（粒子数、动量、能量）主导，可以用[流体动力学](@entry_id:136788)方程描述。在这种情况下，[集体模](@entry_id:137129)式是一种密度波，其恢复力来自于压强的梯度。这与经典气体中的声波完全类似，被称为**[第一声](@entry_id:144225)**（first sound）。其传播速度 $c_1$ 由系统的[等熵压缩](@entry_id:138727)率决定。例如，对于一个弱相互作用的简并费米液体，其速度近似为 $c_1 \approx v_F/\sqrt{3}$，其中 $v_F$ 是费米速度。此区间内的声[波阻](@entry_id:263999)尼主要来源于粘滞效应，[阻尼系数](@entry_id:163719)与[波矢](@entry_id:178620)的平方 $q^2$ 成正比。

2.  **无碰撞区间 ($\omega\tau \gg 1$)：[零声](@entry_id:142772)**
    当振荡频率远高于碰撞频率时 ($\omega \gg 1/\tau$)，$\omega\tau \gg 1$。这意味着在一个[振荡周期](@entry_id:271387)内，[准粒子](@entry_id:136584)几乎不发生碰撞。[碰撞积分](@entry_id:152100)项 $\mathcal{I}_{\text{coll}}$ 相比于动力学项可以被忽略，系统远非[局域平衡](@entry_id:156295)。此时，动力学由**无碰撞朗道[动力学方程](@entry_id:751029)**（也称朗道-[弗拉索夫方程](@entry_id:161066)）主导。[振荡](@entry_id:267781)的恢复力不再来源于碰撞导致的压强，而是来源于[准粒子](@entry_id:136584)密度涨落产生的**自洽平均场**，即朗道相互作用本身。如果相互作用是排斥性的（例如 $F_0^s > 0$），它就能提供一个恢复力来维持一种新的[集体模](@entry_id:137129)式。这种模式本质上是费米面自身的一种传播形变，被称为**[零声](@entry_id:142772)**（zero sound）。[零声](@entry_id:142772)是一种纯粹的量子现象，没有经典对应物。

从空间角度看，$\omega\tau \gg 1$ 的条件等价于 $ql \gg 1$（其中 $l=v_F\tau$ 是[准粒子](@entry_id:136584)的[平均自由程](@entry_id:139563)，$q$ 是波矢），这意味着[准粒子](@entry_id:136584)的平均自由程远大于[振荡](@entry_id:267781)的波长 [@problem_id:3024823]。

### [零声](@entry_id:142772)的微观机制

现在我们聚焦于无碰撞区间，深入探讨[零声](@entry_id:142772)的产生机制。

#### 色散关系

我们从无碰撞的线性化朗道动力学方程出发，并寻找其自持的（即没有外场 $U_{\text{ext}}=0$）[平面波解](@entry_id:195230) $\delta n_{\mathbf{k}} \propto \exp\{i(\mathbf{q}\cdot\mathbf{r}-\omega t)\}$。在零温极限下，[平衡分布](@entry_id:263943)的[能量导数](@entry_id:170468) $-\partial n^0/\partial\epsilon$ 变为一个在[费米能级](@entry_id:143215) $\epsilon_F$ 处的狄拉克 $\delta$ 函数，这意味着只有费米面上的[准粒子](@entry_id:136584)参与动力学。通过一系列推导，我们可以得到一个关于[费米面](@entry_id:137798)上的涨落振幅 $\phi(\hat{\mathbf{p}})$ 的[积分方程](@entry_id:138643) [@problem_id:3024822]：

$$
(\omega - \mathbf{q}\cdot\mathbf{v}_{\mathbf{p}}) \phi(\hat{\mathbf{p}}) = (\mathbf{q}\cdot\mathbf{v}_{\mathbf{p}}) \int \frac{d\Omega'}{4\pi} \sum_{\ell} F_{\ell}^{s} P_{\ell}(\hat{\mathbf{p}}\cdot\hat{\mathbf{p}}') \phi(\hat{\mathbf{p}}')
$$

其中 $\hat{\mathbf{p}}$ 是动量的单位矢量，$\mathbf{v}_{\mathbf{p}} = v_F \hat{\mathbf{p}}$。方程左边描述了单个[准粒子](@entry_id:136584)的响应，右边则体现了所有其他[准粒子](@entry_id:136584)通过朗道相互作用 $F_{\ell}^s$ 产生的[自洽场](@entry_id:136549)。

对于纵向的密度[振荡](@entry_id:267781)（[零声](@entry_id:142772)），起主导作用的是 $\ell=0$ 的[朗道参数](@entry_id:144630) $F_0^s$。假设只有 $F_0^s$ 非零，上述方程可以简化并导出一个关于[零声](@entry_id:142772)色散关系的[超越方程](@entry_id:276279)：

$$
\frac{1}{F_0^s} = \Phi(s) \equiv \frac{1}{2} \int_{-1}^{1} d\mu \frac{\mu}{s-\mu}
$$

这里，$s \equiv \omega/(qv_F)$ 是无量纲的相速度，$\mu = \cos\theta = \hat{\mathbf{p}}\cdot\hat{\mathbf{q}}$。这个积分可以被精确计算出来 [@problem_id:3024822]：

$$
\Phi(s) = -1 + \frac{s}{2} \ln\left(\frac{s+1}{s-1}\right)
$$

这个方程的解 $s(F_0^s)$ 给出了[零声](@entry_id:142772)的相速度 $c_0 = s \cdot v_F$ 是如何由[相互作用强度](@entry_id:192243) $F_0^s$ 决定的。

#### 传播条件：避免[朗道阻尼](@entry_id:137619)

[色散](@entry_id:263750)方程 $\Phi(s)$ 的形式揭示了一个至关重要的物理图像。观察函数 $\Phi(s)$ 中的对数项，当 $s < 1$ 时，其宗量 $(\frac{s+1}{s-1})$ 为负，导致 $\Phi(s)$ 产生虚部。一个有虚部的色散关系意味着模式是阻尼的。

这个数学特性有深刻的物理根源。在费米海洋中，一个能量为 $\hbar\omega$、动量为 $\hbar\mathbf{q}$ 的外部扰动可以激发一个[准粒子](@entry_id:136584)从费米面下的态 $\mathbf{k}$ 跃迁到费米面上的态 $\mathbf{k}+\mathbf{q}$，形成一个**粒子-空穴对**（particle-hole pair）。在零温下，这些单粒子激发满足的运动学条件是 $\omega \le v_F q$，或者说 $s \le 1$。这个区域 $(\omega, q)$ 被称为**[粒子-空穴连续谱](@entry_id:191825)**（particle-hole continuum）。

当一个[集体模](@entry_id:137129)式的色散关系落入这个连续谱内时 ($s \le 1$)，它就能够与满足[共振条件](@entry_id:754285) $\omega = \mathbf{q}\cdot\mathbf{v}_{\mathbf{p}}$ 的[准粒子](@entry_id:136584)发生共振，将能量转移给单个的[粒子-空穴激发](@entry_id:137289)，从而导致[集体模](@entry_id:137129)式的衰减。这个无碰撞的阻尼机制被称为**[朗道阻尼](@entry_id:137619)**（Landau damping）[@problem_id:3024883]。

因此，一个能够长程传播的、无阻尼的集体模式，必须存在于[粒子-空穴连续谱](@entry_id:191825)之外。对于[零声](@entry_id:142772)而言，这意味着其无量纲相速度必须满足 $s > 1$，即相速度 $\omega/q$ 必须大于费米速度 $v_F$。在这种情况下，没有任何[准粒子](@entry_id:136584)能够“追上”[集体模](@entry_id:137129)式的波前并与之发生共振，[朗道阻尼](@entry_id:137619)的通道被运动学关系所禁止，集体模式得以稳定传播 [@problem_id:3024883]。

#### 相互作用的角色

既然无阻尼传播要求 $s > 1$，那么什么样的相互作用才能支持这样的模式存在呢？我们来分析[色散](@entry_id:263750)方程 $1/F_0^s = \Phi(s)$。函数 $\Phi(s)$ 在 $s \in (1, \infty)$ 区间内是一个从 $+\infty$ 单调递减到 $0$ 的实函数。因此，为了使该方程有解，等式左边的 $1/F_0^s$ 必须大于零，这直接要求：

$$
F_0^s > 0
$$

这表明，只有当[准粒子](@entry_id:136584)之间的相互作用是**排斥性**的，纵向[零声](@entry_id:142772)模式才能存在。这在物理上是直观的：排斥相互作用提供了对密度压缩的恢复力，就像一个“量子弹簧”，使得密度波得以传播。吸引相互作用 ($F_0^s < 0$) 则会加剧密度不均匀性，可能导致系统的不稳定（[Pomeranchuk不稳定性](@entry_id:138293)），而不是传播模式。

此外，由于 $\Phi(s)$ 是 $s$ 的单调减函数，当排斥相互作用 $F_0^s$ 增强时，$1/F_0^s$ 减小，要求 $\Phi(s)$ 也减小，这对应于 $s$ 的增大。因此，**更强的排斥相互作用会产生更快的[零声](@entry_id:142772)速度**，使模式进一步远离[粒子-空穴连续谱](@entry_id:191825)的边界，从而更加稳定 [@problem_id:3024871]。

### 观测特征与理论拓展

#### 实验探针：[动态结构因子](@entry_id:143433)

理论上预测的[集体模](@entry_id:137129)式如何与实验观测联系起来？中子散射或[X射线散射](@entry_id:152296)等实验测量的是系统的**[动态结构因子](@entry_id:143433)**（dynamic structure factor）$S(\mathbf{q}, \omega)$，它描述了系统在受到一个能量为 $\hbar\omega$、动量为 $\hbar\mathbf{q}$ 的探针激发时产生密度涨落的概率。

根据**涨落-耗散定理**（Fluctuation-Dissipation Theorem），[动态结构因子](@entry_id:143433)与系统的密度-密度响应函数（或称磁化率）$\chi_{nn}(\mathbf{q}, \omega)$ 的虚部直接相关 [@problem_id:3024851]。其关系式为：

$$
S(\mathbf{q},\omega) = -\frac{2\hbar}{1 - e^{-\beta \hbar \omega}} \text{Im}\,\chi_{nn}^R(\mathbf{q},\omega)
$$

其中 $\beta=1/(k_B T)$，$R$ 表示这是一个推迟[响应函数](@entry_id:142629)。一个寿命有限的[集体模](@entry_id:137129)式（如[零声](@entry_id:142772)）在响应函数中表现为一个极点，例如 $\chi_{nn}^R(\mathbf{q},\omega) \propto (\omega - \omega_0(\mathbf{q}) + i\gamma(\mathbf{q}))^{-1}$。这个极点在 $S(\mathbf{q}, \omega)$ 中会产生一个以模式频率 $\omega_0(\mathbf{q})$ 为中心、宽度为阻尼率 $\gamma(\mathbf{q})$ 的洛伦兹峰。在理想的无阻尼极限下 ($\gamma \to 0$)，这个峰会变成一个在 $\omega = \omega_0(\mathbf{q})$ 处的狄拉克 $\delta$ 函数峰。因此，通过测量 $S(\mathbf{q}, \omega)$，实验学家可以直接描绘出[零声](@entry_id:142772)等[集体模](@entry_id:137129)式的[色散曲线](@entry_id:197598) $\omega_0(\mathbf{q})$ [@problem_id:3024851]。

#### 连接两种机制：从[第一声](@entry_id:144225)到[零声](@entry_id:142772)的过渡

[第一声](@entry_id:144225)和[零声](@entry_id:142772)分别是在 $\omega\tau \ll 1$ 和 $\omega\tau \gg 1$ 极限下的集体[声学模](@entry_id:263916)式。在中间的过渡区域 $\omega\tau \sim 1$，需要一个更精细的理论来描述声速如何从[第一声](@entry_id:144225)速度 $c_1$ 连续演化到[零声](@entry_id:142772)速度 $c_0$。这可以通过在朗道[动力学方程](@entry_id:751029)的[碰撞积分](@entry_id:152100)项中采用一个满足粒子数守恒的**[弛豫时间近似](@entry_id:138429)**（Relaxation-Time Approximation, RTA）来实现。这种方法构造出的[响应函数](@entry_id:142629) $\chi(q, \omega)$ 能够正确地再现 $\omega \to 0$ 时的[流体动力学极限](@entry_id:141281)（由压缩率决定）和 $\omega\tau \to \infty$ 时的无碰撞极限。其结果是，集体模式的极点会随着 $\omega\tau$ 的变化而连续移动，从而平滑地将声速从 $c_1$ 连接到 $c_0$ [@problem_id:3024881]。

#### 带电系统中的[集体模](@entry_id:137129)式：二维[等离激元](@entry_id:146184)

[朗道费米液体理论](@entry_id:151062)的框架和思想也适用于带电系统，如金属中的电子气。然而，相互作用势的性质会极大地改变集体模式的行为。一个重要的例子是[二维电子气](@entry_id:146876)（2DEG）中的**[等离激元](@entry_id:146184)**（plasmon）。这里的相互作用是长程的库仑相互作用，其傅里叶分量 $V(\mathbf{q}) \propto 1/|q|$。在随机相近似（RPA）下，可以计算出[等离激元](@entry_id:146184)的色散关系。与[零声](@entry_id:142772)不同，二维等离激元在长波极限下 ($q \to 0$) 是**无能隙**的，其色散关系为 $\omega_p \propto \sqrt{q}$。

这种 $\sqrt{q}$ 的行为是库仑相互作用的 $1/q$ 形式与非相互作用响应函数 $\Pi^0(q,\omega)$ 在高频下 $\propto q^2/\omega^2$ 的行为共同作用的结果。由于在 $q \to 0$ 时 $\sqrt{q} \gg q$，等离激元的能量总是高于[粒子-空穴连续谱](@entry_id:191825)的上边界 $\omega=v_Fq$，因此在长波长下是无[朗道阻尼](@entry_id:137619)的。然而，随着 $q$ 的增大，$\sqrt{q}$ 曲线最终会与线性边界 $\omega=v_Fq$ 相交。在交点之外的更大 $q$ 值处，[等离激元](@entry_id:146184)进入了[粒子-空穴连续谱](@entry_id:191825)，从而变得有阻尼。这个[交叉点](@entry_id:147634)的位置由系统的基本参数（如[有效玻尔半径](@entry_id:275821)）决定 [@problem_id:3024825]。

#### 超越伽利略[不变性](@entry_id:140168)：晶体中的费米液体

将[朗道理论](@entry_id:138967)应用于真实[金属中的电子](@entry_id:138687)时，必须考虑[晶格](@entry_id:196752)的存在破坏了**伽利略[不变性](@entry_id:140168)**（Galilean Invariance）。在具有伽利略[不变性](@entry_id:140168)的[连续系统](@entry_id:178397)中（如[液氦-3](@entry_id:147785)），有一个精确的关系将[准粒子有效质量](@entry_id:140437) $m^*$ 与[朗道参数](@entry_id:144630) $F_1^s$ 联系起来：$m^*/m = 1 + F_1^s/3$，其中 $m$ 是裸[粒子质量](@entry_id:156313)。这个关系源于[动量守恒](@entry_id:149964)的[沃德恒等式](@entry_id:147000)。

然而，在[晶格](@entry_id:196752)中，动量不守恒（[晶格动量](@entry_id:143609)仅在忽略翁克拉普散射时近似守恒），上述关系不再成立。[准粒子](@entry_id:136584)的[有效质量](@entry_id:142879) $m^*$ 和能带底部的**能带质量** $m_b$ 成为两个独立的参数，与 $F_1^s$ 没有固定的关系。

这一改变对两种声速有重要影响 [@problem_id:3024886]：
-   [第一声](@entry_id:144225)（[流体动力学](@entry_id:136788)声）的速度 $c_{hd}^2$ 由压缩率和[惯性质量](@entry_id:267233)密度决定，其表达式为 $c_{hd}^2 \propto \frac{1+F_0^s}{m_b m^*}k_F^2$，明确地依赖于能带质量 $m_b$ 和有效质量 $m^*$ 的比值。
-   [零声](@entry_id:142772)的速度 $c_0$ 在主导阶数上仍由[色散](@entry_id:263750)方程 $1/F_0^s = \Phi(s)$ 决定，其速度主要依赖于 $F_0^s$ 和[准粒子](@entry_id:136584)费米速度 $v_F^* = \hbar k_F/m^*$。

由于 $m^*/m_b$ 和 $F_1^s$ [解耦](@entry_id:637294)，[第一声](@entry_id:144225)和[零声](@entry_id:142772)的速度不再像伽利略不变系统中那样被紧密地联系在一起。这揭示了将[费米液体理论](@entry_id:144069)从理想模型应用于真实材料时所必须考虑的重要物理细节。