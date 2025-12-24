## 引言
含时输运模拟是理解和预测粒子在介质中动态行为的关键技术，在核[反应堆安全分析](@entry_id:1130678)、天体物理、医学物理和[辐射屏蔽](@entry_id:1130501)等众多领域具有不可或缺的重要性。与仅关注系统[稳态](@entry_id:139253)行为的静态计算不同，瞬态模拟旨在捕捉系统随时间演化的完整过程，例如反应堆在控制棒移动或冷却剂密度变化后的功率响应。这要求我们超越简化的点堆动力学模型，转向能够精确描述粒子在空间、能量和角度上分布如何随时间变化的、更具根本性的物理模型。

本文旨在为读者提供一个关于含时输运模拟的全面而深入的理论与实践框架。我们将从最基本的物理原理出发，逐步构建起描述粒子输运过程的数学方程，并探讨求解这些复杂方程的先进数值方法。通过本文的学习，读者将能够理解瞬态[输运现象](@entry_id:147655)背后的核心机制，并掌握分析和解决相关工程与科学问题的基本工具。

文章将分为三个核心部分展开。在“**原理与机制**”一章中，我们将详细推导含时玻尔兹曼输运方程，剖析其中每一项的物理意义，并引入缓发中子模型，最终探讨数值求解的关键技术，包括确定论的离散纵标法和随机的蒙特卡罗方法。接下来的“**应用与跨学科连接**”一章将展示这些理论和方法在先进反应堆分析、[多物理场耦合](@entry_id:171389)以及天体物理和材料科学等交叉领域的广泛应用，揭示[输运理论](@entry_id:143989)的普适性。最后，在“**动手实践**”部分，我们将通过一系列精心设计的问题，引导读者将理论知识应用于实际计算，加深对数值方法稳定性和准确性的理解。

## 原理与机制

### [含时中子输运](@entry_id:1133153)方程

瞬态[中子输运模拟](@entry_id:1128710)的理论基础是**含时[玻尔兹曼输运方程](@entry_id:140472)**（Time-Dependent Boltzmann Transport Equation, TDNTE）。该方程是一个描述中子在相空间中分布随时间演化的守恒定律。相空间包括中子的空间位置 $\mathbf{r}$、运动方向 $\mathbf{\Omega}$ 和能量 $E$。在实际计算中，能量通常被离散化为有限数量的能群，这便引出了多群形式的[输运方程](@entry_id:174281)。

#### 基本平衡方程

对于一个给定的能群 $g$，中子在[微分](@entry_id:158422)相空间元 $d^3\mathbf{r} \, d\mathbf{\Omega}$ 内的守恒关系可以通过平衡方程来描述。该方程的核心变量是**[角中子通量](@entry_id:1121012)密度**（angular neutron flux），记为 $\psi_g(\mathbf{r}, \mathbf{\Omega}, t)$。它与**角中子数密度** $n_g(\mathbf{r}, \mathbf{\Omega}, t)$ 通过群[平均速度](@entry_id:267649) $v_g$ 相关联，即 $\psi_g = v_g n_g$。角通量密度代表在位置 $\mathbf{r}$ 处，单位时间内穿过垂直于方向 $\mathbf{\Omega}$ 的单位面积的、方向在 $\mathbf{\Omega}$ 附近的单位立体角内的群 $g$ 中子数。其单位通常为 $\mathrm{neutrons} \cdot \mathrm{m}^{-2} \cdot \mathrm{s}^{-1} \cdot \mathrm{sr}^{-1}$。

多群[含时中子输运](@entry_id:1133153)方程的标准形式为：
$$
\frac{1}{v_g}\frac{\partial \psi_g(\mathbf{r},\mathbf{\Omega},t)}{\partial t} + \mathbf{\Omega}\cdot\nabla \psi_g + \Sigma_{t,g}\psi_g = \sum_{g'}\int_{4\pi}\Sigma_{s,g' \to g}(\mathbf{r}, \mathbf{\Omega}'\to\mathbf{\Omega})\psi_{g'}\,d\mathbf{\Omega}' + \frac{\chi_{p,g}}{4\pi}\sum_{g'}(1-\beta)\nu_{g'}\Sigma_{f,g'}\phi_{g'} + S_d + q_g
$$
为了深刻理解此方程，我们必须对其中每一项的物理意义和单位进行精确剖析 。方程的每一项都必须具有相同的单位，即[中子产生](@entry_id:1128705)或消失的速率密度，其[国际单位制](@entry_id:172547)（SI）单位为 $\mathrm{neutrons} \cdot \mathrm{m}^{-3} \cdot \mathrm{s}^{-1} \cdot \mathrm{sr}^{-1}$。

*   **时间积累项**: $\frac{1}{v_g}\frac{\partial \psi_g}{\partial t}$。这一项描述了在相空间元内中子数密度的变化率。由于 $\psi_g = v_g n_g$，该项等价于 $\frac{\partial n_g}{\partial t}$。其单位为 $(\mathrm{m}^{-1}\cdot\mathrm{s}) \cdot (\mathrm{neutrons} \cdot \mathrm{m}^{-2} \cdot \mathrm{s}^{-2} \cdot \mathrm{sr}^{-1}) = \mathrm{neutrons} \cdot \mathrm{m}^{-3} \cdot \mathrm{s}^{-1} \cdot \mathrm{sr}^{-1}$，符合要求。

*   **流出项 (Streaming Term)**: $\mathbf{\Omega}\cdot\nabla \psi_g$。此项代表由于中子沿方向 $\mathbf{\Omega}$ 运动而净流出[微分](@entry_id:158422)空间元 $d^3\mathbf{r}$ 的速率。梯度算子 $\nabla$ 的单位是 $\mathrm{m}^{-1}$，因此该项单位为 $\mathrm{m}^{-1} \cdot (\mathrm{neutrons} \cdot \mathrm{m}^{-2} \cdot \mathrm{s}^{-1} \cdot \mathrm{sr}^{-1}) = \mathrm{neutrons} \cdot \mathrm{m}^{-3} \cdot \mathrm{s}^{-1} \cdot \mathrm{sr}^{-1}$。

*   **碰撞损失项 (Collision Term)**: $\Sigma_{t,g}\psi_g$。此项描述了由于与介质原子核发生任何类型的相互作用（散射或吸收）而从相空间元中移除的中子速率。**宏观总截面** $\Sigma_{t,g}$ 定义为单位路径长度内发生相互作用的概率，单位为 $\mathrm{m}^{-1}$。因此，该项单位为 $\mathrm{m}^{-1} \cdot (\mathrm{neutrons} \cdot \mathrm{m}^{-2} \cdot \mathrm{s}^{-1} \cdot \mathrm{sr}^{-1}) = \mathrm{neutrons} \cdot \mathrm{m}^{-3} \cdot \mathrm{s}^{-1} \cdot \mathrm{sr}^{-1}$。

*   **散射源项 (Scattering Source)**: $\sum_{g'}\int_{4\pi}\Sigma_{s,g' \to g}(\mathbf{r}, \mathbf{\Omega}'\to\mathbf{\Omega})\psi_{g'}\,d\mathbf{\Omega}'$。此项代表从所有其他能群 $g'$ 和所有其他方向 $\mathbf{\Omega}'$ 散射进入目标能群 $g$ 和方向 $\mathbf{\Omega}$ 的中子速率。**[微分](@entry_id:158422)宏观[散射截面](@entry_id:140322)** $\Sigma_{s,g' \to g}$ 的单位是 $\mathrm{m}^{-1} \cdot \mathrm{sr}^{-1}$。对所有入射方向 $\mathbf{\Omega}'$ 积分后，该项单位为 $\mathrm{m}^{-1} \cdot \mathrm{sr}^{-1} \cdot (\mathrm{neutrons} \cdot \mathrm{m}^{-2} \cdot \mathrm{s}^{-1} \cdot \mathrm{sr}^{-1}) \cdot \mathrm{sr} = \mathrm{neutrons} \cdot \mathrm{m}^{-3} \cdot \mathrm{s}^{-1} \cdot \mathrm{sr}^{-1}$。

*   **瞬发裂变源项 (Prompt Fission Source)**: $\frac{\chi_{p,g}}{4\pi}\sum_{g'}(1-\beta)\nu_{g'}\Sigma_{f,g'}\phi_{g'}$。这是由裂变事件瞬时产生的中子源。
    *   $\phi_{g'}(\mathbf{r},t) = \int_{4\pi} \psi_{g'}(\mathbf{r}, \mathbf{\Omega}, t) d\mathbf{\Omega}$ 是**标通量密度**，单位为 $\mathrm{neutrons} \cdot \mathrm{m}^{-2} \cdot \mathrm{s}^{-1}$。
    *   $\Sigma_{f,g'}$ 是群 $g'$ 的**宏观裂变[截面](@entry_id:154995)**，单位为 $\mathrm{m}^{-1}$。
    *   $\nu_{g'}$ 是每次裂变产生的总中子数（无量纲）。
    *   $\beta$ 是总的[缓发中子份额](@entry_id:158691)（无量纲），因此 $(1-\beta)$ 是瞬发中子份额。
    *   $\chi_{p,g}$ 是[瞬发中子](@entry_id:161367)产生在能群 $g$ 的概率（无量纲），满足 $\sum_g \chi_{p,g} = 1$。
    *   $1/(4\pi)$ 因子（单位为 $\mathrm{sr}^{-1}$）说明裂变中子是各向同性发射的。
    *   整个裂变源项的单位为 $\mathrm{sr}^{-1} \cdot (\text{dimensionless}) \cdot \mathrm{m}^{-1} \cdot (\mathrm{neutrons} \cdot \mathrm{m}^{-2} \cdot \mathrm{s}^{-1}) = \mathrm{neutrons} \cdot \mathrm{m}^{-3} \cdot \mathrm{s}^{-1} \cdot \mathrm{sr}^{-1}$。

*   **缓发中子源项 ($S_d$) 和外源项 ($q_g$)**: 这些项也必须具有相同的单位 $\mathrm{neutrons} \cdot \mathrm{m}^{-3} \cdot \mathrm{s}^{-1} \cdot \mathrm{sr}^{-1}$，以确保方程的[量纲一致性](@entry_id:271193)。我们将在下一节详细讨论缓发中子源项。

#### 缓发中子的引入

在真实的[反应堆动力学](@entry_id:1130674)中，一小部分裂变中子（份额为 $\beta$）并非瞬时产生，而是由特定的[裂变产物](@entry_id:1125033)（称为**缓发中子先驱核**）在放射性衰变后发射的。这个过程对反应堆的控制至关重要。为了模拟这一现象，我们需要引入描述先驱核浓度演化的附加方程 。

假设有 $I$ 个不同的先驱核家族，每个家族 $i$ 的浓度为 $C_i(\mathbf{r}, t)$（单位：$\mathrm{nuclei} \cdot \mathrm{m}^{-3}$）。其浓度变化率由产生和衰变两项决定：
$$
\frac{\partial C_i(\mathbf{r}, t)}{\partial t} = \text{产生率} - \text{衰变率}
$$
先驱核的产生率正比于总的裂变[中子产生](@entry_id:1128705)率。对于家族 $i$，其份额为 $\beta_i$。因此，产生率为 $\beta_i \sum_{g'} \nu_{g'} \Sigma_{f,g'} \phi_{g'}$。[衰变率](@entry_id:156530)则遵循[放射性衰变](@entry_id:142155)定律，即 $\lambda_i C_i(\mathbf{r}, t)$，其中 $\lambda_i$ 是[衰变常数](@entry_id:149530)（单位：$\mathrm{s}^{-1}$）。综合起来，先驱核的[平衡方程](@entry_id:172166)为：
$$
\frac{\partial C_i(\mathbf{r}, t)}{\partial t} = \beta_i \sum_{g=1}^{G} \nu_g \Sigma_{f,g}(\mathbf{r}) \phi_g(\mathbf{r}, t) - \lambda_i C_i(\mathbf{r}, t)
$$
其中，$\beta = \sum_{i=1}^I \beta_i$ 是总的[缓发中子份额](@entry_id:158691)。

当一个先驱[核衰变](@entry_id:140740)时，它会发射一个缓发中子。因此，来自所有先驱核家族的缓发中子总体积源率为 $\sum_{i=1}^I \lambda_i C_i(\mathbf{r}, t)$。这些中子具有特定的能量谱 $\chi_{d,g}$（归一化为 $\sum_g \chi_{d,g} = 1$），并且通常假设其发射是各向同性的。因此，进入[输运方程](@entry_id:174281)的**缓发中子角源项** $S_d$ 为：
$$
S_{d,g}(\mathbf{r}, \mathbf{\Omega}, t) = \frac{\chi_{d,g}}{4\pi} \sum_{i=1}^{I} \lambda_i C_i(\mathbf{r}, t)
$$
这两个方程与基本[输运方程](@entry_id:174281)耦合，构成了描述反应堆瞬态行为的完整数学模型。

#### 良定性：初始与边界条件

TDNTE 是一个一阶[双曲型偏微分方程](@entry_id:1126291)。为了获得一个唯一的、稳定的、且具有物理意义的解，必须提供适当的初始条件和边界条件 。

**初始条件**：
必须在模拟的初始时刻 $t=0$ 指定整个相空间（即所有位置 $\mathbf{r}$、方向 $\mathbf{\Omega}$ 和能群 $g$）的中子角通量密度分布：
$$
\psi_g(\mathbf{r}, \mathbf{\Omega}, 0) = \psi_{g,0}(\mathbf{r}, \mathbf{\Omega})
$$
对于物理上可接受的解，初始角通量密度必须是**非负**的，因为中子密度不能为负。此外，它应属于某个[函数空间](@entry_id:143478)，例如 $L^1$，以确保总中子数和总反应率是有限的。

**边界条件**：
双曲型方程的解沿着**特征线**传播，其方向由中子运动方向 $\mathbf{\Omega}$ 决定。对于一个有界凸区域，边界上的条件仅需且必须在**流入边界**上指定。流入边界是指中子正要进入计算区域的方向。若 $\mathbf{n}(\mathbf{r}_b)$ 是[边界点](@entry_id:176493) $\mathbf{r}_b$ 处的外[法线](@entry_id:167651)向量，则流入条件适用于满足 $\mathbf{\Omega} \cdot \mathbf{n}(\mathbf{r}_b)  0$ 的所有方向 $\mathbf{\Omega}$。在这些流入方向上，必须给定角通量密度：
$$
\psi_g(\mathbf{r}_b, \mathbf{\Omega}, t) = \psi_{b,g}(\mathbf{r}_b, \mathbf{\Omega}, t) \quad \text{for} \quad \mathbf{\Omega} \cdot \mathbf{n}(\mathbf{r}_b)  0
$$
对于流出边界（$\mathbf{\Omega} \cdot \mathbf{n}(\mathbf{r}_b) \ge 0$），角通量密度是由区域内部的解确定的，不能独立指定，否则问题将变得超定。

一个常见的边界条件是**[真空边界条件](@entry_id:1133678)**，它假定没有中子从外界进入计算区域。这对应于在整个流入边界上设置角通量密度为零：
$$
\psi_g(\mathbf{r}_b, \mathbf{\Omega}, t) = 0 \quad \text{for} \quad \mathbf{\Omega} \cdot \mathbf{n}(\mathbf{r}_b)  0
$$
通过正确设定这些初始和边界数据，TDNTE 问题就成为一个**良定问题**，保证了解的存在性、唯一性和稳定性。

### [模态分析](@entry_id:163921)与反应堆动力学

为了理解[输运方程](@entry_id:174281)解的长期行为，我们可以采用[模态分析](@entry_id:163921)方法，寻找具有特定时间依赖性的分离变量解。

#### Alpha[本征值问题](@entry_id:142153)

假设系统中没有外源，我们可以寻找形如 $\psi_g(\mathbf{r},\mathbf{\Omega},t) = \widehat{\psi}_g(\mathbf{r},\mathbf{\Omega})\exp(\alpha t)$ 的解。这种形式的解代表一个**模态**，其中中子通量密度的空间、角度和能量分布（即模态形状 $\widehat{\psi}_g$）保持不变，而其振幅随时间呈指数变化，变化率为 $\alpha$ 。将此解代入齐次TDNTE（这里为了简化，我们暂时只考虑总裂变源项，不区分瞬发和缓发），可以得到一个关于 $\alpha$ 的广义[本征值问题](@entry_id:142153)：
$$
\frac{\alpha}{v_g} \widehat{\psi}_g + \mathbf{\Omega} \cdot \nabla \widehat{\psi}_g + \Sigma_{t,g} \widehat{\psi}_g = \sum_{g'}\int_{4\pi}\Sigma_{s,g' \to g} \widehat{\psi}_{g'}\,d\mathbf{\Omega}' + \frac{\chi_g}{4\pi}\sum_{g'}\nu_{g'}\Sigma_{f,g'}\widehat{\phi}_{g'}
$$
我们可以用算子形式重写此方程。定义输运算子 $\mathcal{L}$、散射算子 $\mathcal{S}$、裂变算子 $\mathcal{F}$ 和逆速度算子 $\mathcal{M}$：
$$
(\mathcal{S} + \mathcal{F} - \mathcal{L})\widehat{\psi} = \alpha \mathcal{M} \widehat{\psi}
$$
该方程的解是一系列本征值 $\alpha_n$ 和对应的[本征函数](@entry_id:154705)（模态）$\widehat{\psi}_n$。在足够长的时间后，中子通量将由具有最大实部本征值 $\alpha_0$ 的**[主模](@entry_id:263463)态**主导。这个**主alpha本征值** $\alpha_0$ 决定了反应堆的渐近时间行为：

*   $\alpha_0 > 0$: 反应堆**超临界**，中子布居数呈[指数增长](@entry_id:141869)。
*   $\alpha_0  0$: 反应堆**次临界**，中子布居数呈指数衰减。
*   $\alpha_0 = 0$: 反应堆**临界**，中子布居数保持稳定。

$\alpha_0$ 因此是反应堆动态响应的一个关键度量，称为**反应堆周期**的倒数。

#### 反应性与[瞬发中子](@entry_id:161367)代长时间

在[反应堆物理](@entry_id:158170)学中，**反应性** $\rho$ 是衡量系统偏离临界状态程度的无量纲量。它通常通过**有效增殖因子** $k_{\text{eff}}$ 来定义，后者是静态[输运方程](@entry_id:174281)的本征值，表示一代裂变与上一代裂变的中子数之比。反应性的标准定义为 ：
$$
\rho(t) = \frac{k(t) - 1}{k(t)}
$$
其中 $k(t)$ 是在 $t$ 时刻冻结系统材料性质时的瞬时有效增殖因子。

另一个关键参数是**[瞬发中子](@entry_id:161367)代长时间** $\Lambda(t)$，它代表中子完成一代裂变循环（从一次裂变中产生，到下一次裂变中被吸收）所需的平均时间。利用伴随通量加权，它可以严谨地定义为中子布居数与瞬发裂变产生率之比。

对于偏离临界不远（$|\rho| \ll 1$）且动力学由[瞬发中子](@entry_id:161367)主导的系统，$\alpha$ 本征值、反应性和代长时间之间存在一个非常有用的近似关系。通过对[输运方程](@entry_id:174281)进行[微扰分析](@entry_id:178808)可以证明：
$$
\alpha_0(t) \approx \frac{\rho(t)}{\Lambda(t)}
$$
这个关系直观地说明了中子布居数的变化率（由 $\alpha_0$ 描述）正比于系统的超额[中子产生](@entry_id:1128705)率（由 $\rho$ 描述），而反比于完成一个增殖循环所需的时间（由 $\Lambda$ 描述）。这个近似在分析快速瞬态（例如超[瞬发临界](@entry_id:159881)事故）时非常重要，因为此时缓发中子的影响可以忽略不计。

### 数值求解方法

由于TDNTE的复杂性，解析解仅限于极少数高度简化的 idealized 问题。在实践中，我们必须依赖数值方法。这些方法主要分为两大类：确定论方法和随机方法。

#### 确定论方法：离散化原理

确定论方法通过在整个相空间上离散化方程，将其转化为一个大型的[代数方程](@entry_id:272665)组来求解。这个过程通常涉及对所有[自变量](@entry_id:267118)（空间、角度、能量、时间）的离散化。

##### 角度离散化（S_N方法）

**[离散纵标法](@entry_id:1123828)** ($S_N$ 方法) 是最常用的角度[离散化技术](@entry_id:1123836)。它将连续的角度变量 $\mathbf{\Omega}$ 替换为一组精心选择的离散方向 $\lbrace \mathbf{\Omega}_m \rbrace_{m=1}^M$ 和相应的**[求积权重](@entry_id:753910)** $\lbrace w_m \rbrace_{m=1}^M$。这些方向和权重构成了一个**[求积组](@entry_id:156430)**，用于近似角度相关的积分，例如：
$$
\int_{4\pi} f(\mathbf{\Omega}) \,d\mathbf{\Omega} \approx \sum_{m=1}^M w_m f(\mathbf{\Omega}_m)
$$
[求积组](@entry_id:156430)被设计为能够精确积分直到某个阶数的[球谐函数](@entry_id:178380)，且权重之和等于 $4\pi$ 。

将 $S_N$ 方法应用于TDNTE，特别是散射源项，会将积分转化为求和。对于[各向异性散射](@entry_id:148372)，其[微分截面](@entry_id:137333)通常通过[勒让德多项式](@entry_id:141510)展开：
$$
\Sigma_{s,g' \to g}(\mathbf{\Omega}' \cdot \mathbf{\Omega}) = \sum_{\ell=0}^{L} \frac{2\ell+1}{4\pi} \Sigma_{s\ell, g' \to g} P_\ell(\mathbf{\Omega}' \cdot \mathbf{\Omega})
$$
应用 $S_N$ 求積后，离散方向 $\mathbf{\Omega}_m$ 上的散射源项变为：
$$
Q_{s,g,m}(\mathbf{r},t) = \sum_{g'} \sum_{\ell=0}^{L} \frac{2\ell+1}{4\pi} \Sigma_{s\ell, g' \to g} \sum_{m'=1}^{M} w_{m'} P_{\ell}(\mathbf{\Omega}_{m} \cdot \mathbf{\Omega}_{m'}) \psi_{g',m'}(\mathbf{r},t)
$$
其中 $\psi_{g',m'}(\mathbf{r},t)$ 是在离散方向 $\mathbf{\Omega}_{m'}$ 上的角通量密度。[求积权重](@entry_id:753910) $w_{m'}$ 在此扮演着关键角色，它们确保了离散散射算子能够准确地保持[连续算子](@entry_id:143297)的关键矩（例如，标通量和[中子流](@entry_id:1128689)）。

##### 时间离散化与稳定性

在空间和角度离散化之后，TDNTE变成一个关于时间的大型[常微分方程组](@entry_id:907499)（ODE）：
$$
\frac{d\boldsymbol{\psi}(t)}{dt} = \mathbf{L}\boldsymbol{\psi}(t) + \mathbf{s}(t)
$$
其中 $\boldsymbol{\psi}(t)$ 是包含所有空间网格、离散方向和能群未知数的巨型向量。下一步是离散化时间导数。一个通用且强大的框架是 **$\theta$-方法** 。将上述ODE在时间步 $[t^n, t^{n+1}]$ 上积分，并用端点值的加权平均来近似右侧项，可得：
$$
(\mathbf{I} - \theta \Delta t \mathbf{L})\boldsymbol{\psi}^{n+1} = (\mathbf{I} + (1-\theta) \Delta t \mathbf{L})\boldsymbol{\psi}^{n} + \text{source terms}
$$
其中 $\theta \in [0,1]$ 是一个参数，它决定了[时间积分格式](@entry_id:165373)的性质：

*   $\theta = 0$: **[前向欧拉法](@entry_id:141238)** (Explicit Forward Euler)，这是一个**显式**方法，$\boldsymbol{\psi}^{n+1}$ 可以直接计算。
*   $\theta = 1$: **[后向欧拉法](@entry_id:139674)** (Implicit Backward Euler)，这是一个**隐式**方法，需要在每个时间步求解一个[线性方程组](@entry_id:148943)。
*   $\theta = 1/2$: **Crank-Nicolson法**，这是一个二阶精度的[隐式方法](@entry_id:138537)。

数值方法的**稳定**性是其最重要的属性之一。如果小的扰动（如[舍入误差](@entry_id:162651)）在计算中被无限放大，则该方法是不稳定的。通过**冯·诺伊曼[稳定性分析](@entry_id:144077)**，可以研究一个格式对不同频率误差的放大行为 。对于一个简化的纯对流-吸收方程，采用[前向欧拉法](@entry_id:141238)和一阶迎风格式（一种显式格式），[稳定性分析](@entry_id:144077)表明，时间步长 $\Delta t$ 必须满足一个严格的条件，即**Courant-Friedrichs-Lewy (CFL) 条件**：
$$
\Delta t \le \frac{1}{\frac{v_g}{\Delta x} + v_g \Sigma_{t,g}}
$$
这个条件限制了在一个时间步内，中子传播的距离不能超过一个空间网格的宽度。violation of this condition leads to exponential error growth.

对于[隐式方法](@entry_id:138537)，如[后向欧拉法](@entry_id:139674)（$\theta=1$），[稳定性分析](@entry_id:144077)（特别是**A-稳定性**分析）表明，该方法对于任何 $\Delta t > 0$ 都是[无条件稳定](@entry_id:146281)的 。这意味着无论时间步长多大，数值解都不会发散。然而，[无条件稳定](@entry_id:146281)并不意味着可以任意选择大的时间步长。即使是稳定的隐式格式，也存在对**数值因果关系**的考量 。一个[隐式格式](@entry_id:166484)的**[数值依赖域](@entry_id:163312)**（numerical domain of dependence）可能远大于物理依赖域。例如，对于后向欧拉[迎风格式](@entry_id:756378)，一个网格点的值依赖于其所有上风向网格点在当前时间步的值，这意味着信息在数值上可以瞬间传播整个计算域。为了获得物理上准确的结果，避免过度的[数值弥散](@entry_id:168584)，即使对于[隐式方法](@entry_id:138537)，时间步长也应满足类似CFL的条件（例如，$v_g \Delta t / \Delta x \lesssim 1$），但这更多是出于对精度的要求，而非稳定性。

#### 随机方法：含时蒙特卡罗

与在离散网格上求解方程的确定论方法不同，**蒙特卡罗方法**通过模拟大量单个中子的生命史来统计地[求解输运方程](@entry_id:1131949)。这是一种基于概率的、非常强大的方法，尤其适用于复杂的几何和能量依赖性问题。

在**事件驱动的含时蒙特卡罗**模拟中，每个中子的状态（位置、方向、能量、时间、权重）都被显式跟踪 。模拟的核心循环是推进粒子从一个事件到下一个事件。对于一个以速度 $v(E)$ 运动的中子，它在均匀介质中自由飞行直到下一次碰撞的距离 $s$ 可以从指数分布 $p(s) = \Sigma_t \exp(-\Sigma_t s)$ 中抽样得到。相应地，**飞行时间** $\tau$ 为 $\tau = s/v(E)$。粒子钟被推进这个时间，位置也相应更新。或者，可以直接从[指数分布](@entry_id:273894) $p(\tau) = v(E)\Sigma_t \exp(-v(E)\Sigma_t \tau)$ 中抽样飞行时间 $\tau$。

为了从这些粒子历史中获得宏观物理量，如通量密度和反应率，我们需要使用**估计子**（estimators）。在含时模拟中，这些估计子必须对时间和空间进行划分（binning）。

*   **[径迹长度估计](@entry_id:1133281) (Track-Length Estimator)**: 该估计子基于一个事实，即在一个区域内所有中子的总径迹长度与该区域的通量密度积分成正比。对于一个体积为 $V$、时间窗为 $[t_b, t_b+\Delta t)$ 的时空单元，其平均标通量密度可以通过累加所有穿过该单元的径迹长度来估计：
    $$
    \phi_{V}^{\Delta t} \approx \frac{1}{V \Delta t} \sum_{\text{tracks}} w \cdot \ell_{\text{overlap}}
    $$
    其中 $w$是粒子权重，$\ell_{\text{overlap}}$是径迹在特定时空单元内的那部分长度。如果一个径迹跨越了多个时间窗或空间单元，它的贡献需要被相应地分割。

*   **碰撞估计 (Collision Estimator)**: 该估计子在每次粒子发生碰撞时记录贡献。对于反应类型 $i$，其反应率 $R_i = \Sigma_i \phi$ 的平均值可以通过下式估计：
    $$
    R_{i,V}^{\Delta t} \approx \frac{1}{V \Delta t} \sum_{\text{collisions}} w \cdot \frac{\Sigma_i}{\Sigma_t}
    $$
    这里的求和是对所有发生在特定时空单元内的碰撞进行的。$\Sigma_i/\Sigma_t$ 是碰撞事件为反应类型 $i$ 的概率。

这些估计子提供了对时空相关的物理量的无偏估计，其精度随着模拟的中子历史数的增加而提高（通常与历史数的平方根成反比）。含时蒙特卡罗方法为研究复杂的瞬态现象提供了高保真的模拟工具。