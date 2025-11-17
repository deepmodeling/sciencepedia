## 引言
在自然界与社会科学的众多现象中，从悬浮在液体中的微粒运动到股票市场的价格波动，随机性扮演着不可或缺的角色。如何精确描述并预测这些受随机因素影响的系统的集体行为，是现代科学面临的核心挑战之一。[福克-普朗克](@entry_id:635508)方程（[Fokker-Planck](@entry_id:635508) Equation）正是应对这一挑战的强大数学工具，它为我们提供了一个描述系统状态概率密度如何随[时间演化](@entry_id:153943)的统一框架。该方程巧妙地将系统的确定性[演化趋势](@entry_id:173460)（漂移）与随机涨落效应（[扩散](@entry_id:141445)）结合在同一个[动力学方程](@entry_id:751029)中，从而揭示了复杂系统宏观统计规律的微观起源。

本文将系统地引导读者深入探索[福克-普朗克](@entry_id:635508)方程的理论核心与广泛应用。在第一部分“原理与机制”中，我们将剖析方程的数学结构，阐明漂移项、[扩散](@entry_id:141445)项及[概率流](@entry_id:150949)的物理意义，并追溯其从微观的朗之万方程和主方程到宏观描述的推导路径。随后，在“应用与跨学科联系”一章中，我们将展示该方程惊人的普适性，通过物理学、生物学、金融学乃至宇宙学等领域的具体案例，领略其作为通用建模语言的强大威力。最后，通过“动手实践”环节，读者将有机会运用所学知识解决具体问题，从而将理论理解转化为实际分析能力。

## 原理与机制

在对[随机过程](@entry_id:159502)的宏观统计行为进行描述时，[福克-普朗克](@entry_id:635508)方程（[Fokker-Planck](@entry_id:635508) Equation, FPE）扮演着核心角色。它是一个描述[概率密度函数](@entry_id:140610)（Probability Density Function, PDF）随时间和空间演化的[偏微分方程](@entry_id:141332)。本章将深入探讨[福克-普朗克](@entry_id:635508)方程的基本原理、其各项物理意义，以及它与微观动力学之间的深刻联系。我们将从方程的一般形式出发，逐步揭示其漂移项和[扩散](@entry_id:141445)项的物理内涵，并探讨其在不同物理情境下的具体应用和重要极限。

### [福克-普朗克](@entry_id:635508)方程的一般形式与[概率流](@entry_id:150949)

一个由[随机变量](@entry_id:195330) $\vec{r}$ 描述的连续[马尔可夫过程](@entry_id:160396)，其概率密度函数 $P(\vec{r}, t)$ 的演化通常可以由[福克-普朗克](@entry_id:635508)方程刻画。在多维空间中，该方程的一般形式为：
$$
\frac{\partial P(\vec{r}, t)}{\partial t} = -\sum_{i} \frac{\partial}{\partial x_i} [A_i(\vec{r}) P(\vec{r}, t)] + \frac{1}{2} \sum_{i,j} \frac{\partial^2}{\partial x_i \partial x_j} [B_{ij}(\vec{r}) P(\vec{r}, t)]
$$
其中，$P(\vec{r}, t)$ 是在时刻 $t$ 于位置 $\vec{r}$ 找到粒子的概率密度。方程右边的第一项由**漂移矢量** (drift vector) $\vec{A}(\vec{r})$ 决定，它描述了系统[状态变量](@entry_id:138790)的瞬时[平均变化率](@entry_id:193432)，通常与作用在系统上的确定性力有关。第二项则由**[扩散张量](@entry_id:748421)** (diffusion tensor) $B_{ij}(\vec{r})$ 决定，它描述了由快速随机涨落引起的系统[状态变量](@entry_id:138790)的[方差](@entry_id:200758)增长率。

这个方程的核心物理意义在于**概率的[局域守恒](@entry_id:751393)**。它可以被写成一个更为直观的**[连续性方程](@entry_id:195013)** (continuity equation) 的形式：
$$
\frac{\partial P(\vec{r}, t)}{\partial t} + \nabla \cdot \vec{J}(\vec{r}, t) = 0
$$
这里的 $\vec{J}(\vec{r}, t)$ 被称为**[概率流密度](@entry_id:152013)矢量** (probability current density vector)，它描述了单位时间内通过单位面积的概率“流量”。通过比较[福克-普朗克](@entry_id:635508)方程的一般形式和连续性方程，我们可以识别出[概率流](@entry_id:150949)的表达式。将一般形式 FPE 的右侧重写为一个散度的负值：
$$
\frac{\partial P}{\partial t} = -\sum_{i} \frac{\partial}{\partial x_i} \left[ A_i P - \frac{1}{2} \sum_{j} \frac{\partial}{\partial x_j} (B_{ij} P) \right]
$$
由此，我们可以直接读出[概率流密度](@entry_id:152013)矢量 $\vec{J}$ 的第 $k$ 个分量 $J_k$ [@problem_id:2001763]：
$$
J_k(\vec{r}, t) = A_k(\vec{r}) P(\vec{r}, t) - \frac{1}{2} \sum_{j} \frac{\partial}{\partial x_j} [B_{kj}(\vec{r}) P(\vec{r}, t)]
$$
若将导数展开，则得到：
$$
J_k = A_k P - \frac{1}{2} \sum_{j} \left[ \left( \frac{\partial B_{kj}}{\partial x_j} \right) P + B_{kj} \frac{\partial P}{\partial x_j} \right]
$$
这个表达式清楚地表明，[概率流](@entry_id:150949)由两部分贡献构成：一部分是由确定性力驱动的**漂移流** ($A_k P$)，另一部分则与随机涨落的强度及其空间变化有关。

### 漂移与扩散的物理诠释

为了直观地理解漂移项和[扩散](@entry_id:141445)项各自的作用，我们可以考察一个简化的
一维系统，其中[漂移系数](@entry_id:199354) $A(x) = A_0$ 和[扩散](@entry_id:141445)系数 $B(x) = B_0$ 均为常数。假设粒子初始时刻精确地位于原点，即 $P(x, 0) = \delta(x)$。

考虑两种极端情况 [@problem_id:1934596]：

1.  **纯漂移过程** ($B_0 = 0, A_0 \neq 0$)：此时[福克-普朗克](@entry_id:635508)方程简化为 $\frac{\partial P}{\partial t} = -A_0 \frac{\partial P}{\partial x}$。这是一个典型的一阶波动方程，其解为 $P(x, t) = \delta(x - A_0 t)$。我们可以计算其均值和[方差](@entry_id:200758)的演化：
    *   **均值**：$\langle x(t) \rangle = \int x P(x,t) dx = A_0 t$。
    *   **[方差](@entry_id:200758)**：$\sigma^2(t) = \langle x^2(t) \rangle - \langle x(t) \rangle^2 = (A_0 t)^2 - (A_0 t)^2 = 0$。
    这表明，漂移项的作用是使整个[概率分布](@entry_id:146404)以恒定速度 $A_0$ 平移，而其形状（在此例中是一个尖锐的脉冲）保持不变。漂移主导了[分布](@entry_id:182848)中心的确定性运动。

2.  **纯[扩散过程](@entry_id:170696)** ($A_0 = 0, B_0 > 0$)：此时方程变为 $\frac{\partial P}{\partial t} = \frac{B_0}{2} \frac{\partial^2 P}{\partial x^2}$，这就是著名的**扩散方程**。其解是一个均值为零、[方差](@entry_id:200758)随时间线性增长的[高斯分布](@entry_id:154414)：$P(x, t) = \frac{1}{\sqrt{2\pi B_0 t}} \exp(-\frac{x^2}{2B_0 t})$。其均值和[方差](@entry_id:200758)为：
    *   **均值**：$\langle x(t) \rangle = 0$。
    *   **[方差](@entry_id:200758)**：$\sigma^2(t) = \langle x^2(t) \rangle - \langle x(t) \rangle^2 = B_0 t - 0 = B_0 t$。
    这表明，[扩散](@entry_id:141445)项本身不引起[分布](@entry_id:182848)中心的移动，但会导致[分布](@entry_id:182848)不断展宽，其宽度（由标准差 $\sigma(t) = \sqrt{B_0 t}$ 度量）随时间的平方根增长。[扩散](@entry_id:141445)主导了[分布](@entry_id:182848)的随机展宽。

在物理学中，[扩散](@entry_id:141445)系数通常用 $D$ 表示，它与[福克-普朗克](@entry_id:635508)方程中的 $B_0$ 通过关系 $B_0 = 2D$ 相关联。因此，对于纯[扩散过程](@entry_id:170696)，我们有 $\sigma^2(t) = 2Dt$，这是描述布朗运动的标志性结果。

### [福克-普朗克](@entry_id:635508)方程的微观起源

[福克-普朗克](@entry_id:635508)方程作为一个宏观的统计描述，其根源在于系统微观层面的动力学。我们可以从两个角度来理解其推导过程：离散[跳跃过程](@entry_id:180953)的[连续极限](@entry_id:162780)，以及单个粒子随机[运动方程](@entry_id:170720)的系综平均。

#### 从主方程到[扩散方程](@entry_id:170713)

考虑一个粒子在一维格点上进行连续时间的[随机行走](@entry_id:142620)。设格点间距为 $\ell$，粒子从任一格点跳跃到相邻格点的总速率为 $\Gamma$。对于一个无偏的[随机行走](@entry_id:142620)，向左和向右跳跃的速率均为 $\Gamma/2$。设 $P_n(t)$ 为时刻 $t$ 粒子位于格点 $n$ 的概率，其演化由一个**[主方程](@entry_id:142959)** (Master Equation) 描述 [@problem_id:2001767]：
$$
\frac{dP_n}{dt} = \frac{\Gamma}{2} (P_{n+1} - P_n) + \frac{\Gamma}{2} (P_{n-1} - P_n) = \frac{\Gamma}{2} (P_{n+1} + P_{n-1} - 2P_n)
$$
为了过渡到连续描述，我们引入[概率密度函数](@entry_id:140610) $P(x, t)$，并假设它在尺度 $\ell$ 上变化缓慢，因此 $P_n(t) \approx \ell P(x_n, t)$，其中 $x_n = n\ell$。将 $P(x \pm \ell, t)$ 在 $x$ 处进行泰勒展开：
$$
P(x \pm \ell, t) = P(x,t) \pm \ell \frac{\partial P}{\partial x} + \frac{\ell^2}{2} \frac{\partial^2 P}{\partial x^2} + O(\ell^3)
$$
代入[主方程](@entry_id:142959)，我们得到：
$$
\ell \frac{\partial P}{\partial t} \approx \frac{\Gamma}{2} \left[ \ell \left( P + \ell P_x + \frac{\ell^2}{2} P_{xx} \right) + \ell \left( P - \ell P_x + \frac{\ell^2}{2} P_{xx} \right) - 2\ell P \right]
$$
简化后得到：
$$
\frac{\partial P}{\partial t} \approx \frac{\Gamma \ell^2}{2} \frac{\partial^2 P}{\partial x^2}
$$
这正是纯[扩散方程](@entry_id:170713)。我们由此得到[扩散](@entry_id:141445)系数与微观跳跃参数的关系 $D = \frac{\Gamma \ell^2}{2}$。这个推导清晰地揭示了[扩散](@entry_id:141445)项中的**二阶空间导数**来源于离散[跳跃过程](@entry_id:180953)中相邻格点概率之间的差分。

#### 从[朗之万方程](@entry_id:144277)到[福克-普朗克](@entry_id:635508)方程

另一种更为普适的方法是从描述单个粒子运动的**朗之万方程** (Langevin Equation) 出发。[朗之万方程](@entry_id:144277)是一个随机微分方程，它包含了确定性力和随机力。例如，考虑一个质量为 $m$、[电荷](@entry_id:275494)为 $q$ 的粒子在[电场](@entry_id:194326) $E$ 和中性气体中运动。它受到[电场](@entry_id:194326)力 $qE$、与速度 $v$ 成正比的阻力 $-\gamma v$ 以及来自气体分子的随机力 $\xi(t)$。其朗之万方程为 [@problem_id:2001775]：
$$
m \frac{dv}{dt} = qE - \gamma v + \xi(t)
$$
随机力 $\xi(t)$ 通常被建模为[高斯白噪声](@entry_id:749762)，其统计性质为 $\langle \xi(t) \rangle = 0$ 和 $\langle \xi(t)\xi(t') \rangle = \Gamma \delta(t-t')$，其中 $\Gamma$ 是噪声强度。

[福克-普朗克](@entry_id:635508)方程的[漂移和扩散](@entry_id:148816)系数可以通过考察速度在微小时间间隔 $\Delta t$ 内的增量 $\Delta v = v(t+\Delta t) - v(t)$ 的[统计矩](@entry_id:268545)来确定：
$$
A(v) = \lim_{\Delta t \to 0} \frac{1}{\Delta t} \langle \Delta v \rangle_{v(t)=v}
$$
$$
B_{vv}(v) = \lim_{\Delta t \to 0} \frac{1}{\Delta t} \langle (\Delta v)^2 \rangle_{v(t)=v}
$$
注意这里我们使用 $B_{vv}$ 表示[福克-普朗克](@entry_id:635508)方程中的[扩散](@entry_id:141445)系数。通过对[朗之万方程](@entry_id:144277)在 $\Delta t$ [内积](@entry_id:158127)分，并利用 $\langle \xi(t) \rangle = 0$ 可以得到 $\langle \Delta v \rangle \approx (\frac{qE}{m} - \frac{\gamma}{m}v) \Delta t$。因此，[漂移系数](@entry_id:199354)为：
$$
A(v) = \frac{qE}{m} - \frac{\gamma}{m}v
$$
这精确地对应于除去随机力后的确定性加速度。

对于二阶矩，在计算 $\langle (\Delta v)^2 \rangle$ 时，包含 $\xi(t)$ 的项在取平均后留下一项，其值为 $\frac{\Gamma}{m^2}\Delta t$。因此，[速度空间](@entry_id:181216)的[扩散](@entry_id:141445)系数为：
$$
B_{vv} = \frac{\Gamma}{m^2}
$$
这是一个常数，仅依赖于随机力的强度和粒子质量。这个过程建立了从微观动力学（朗之万方程）到统计描述（[福克-普朗克](@entry_id:635508)方程系数）的直接桥梁。

### [稳态解](@entry_id:200351)与热平衡

当系统演化足够长时间后，可能会达到一个**[稳态](@entry_id:182458)** (stationary state)，此时[概率分布](@entry_id:146404)不再随时间变化，即 $\frac{\partial P}{\partial t} = 0$。根据连续性方程，这意味着概率流的散度为零：$\nabla \cdot \vec{J}_{st} = 0$。

对于被束缚在势场中的系统（例如，粒子被[光镊](@entry_id:157699)束缚在[谐振子势](@entry_id:750179) $U(x) = \frac{1}{2}\kappa x^2$ 中），通常可以施加一个更强的条件，即**[细致平衡](@entry_id:145988)** (detailed balance)，它要求[稳态概率](@entry_id:276958)流在空间中每一点都为零：$\vec{J}_{st}(\vec{r}) = 0$。

在一维情况下，设[扩散](@entry_id:141445)系数 $D$ 为常数，零流条件 $J_{st}(x) = 0$ 给出：
$$
A(x) P_{st}(x) - D \frac{dP_{st}(x)}{dx} = 0
$$
这导出了[漂移系数](@entry_id:199354)、[扩散](@entry_id:141445)系数与稳态分布之间的一个普适关系 [@problem_id:2001801]：
$$
A(x) = D \frac{1}{P_{st}(x)} \frac{dP_{st}(x)}{dx} = D \frac{d}{dx} \ln P_{st}(x)
$$
如果系统处于温度为 $T$ 的[热平衡](@entry_id:141693)状态，其稳态分布由**玻尔兹曼分布** (Boltzmann distribution) 给出：
$$
P_{st}(x) = N \exp\left(-\frac{U(x)}{k_B T}\right)
$$
其中 $k_B$ 是[玻尔兹曼常数](@entry_id:142384)，$U(x)$ 是势能。将此代入上述关系，我们得到[漂移系数](@entry_id:199354)与[势能](@entry_id:748988)之间的重要联系：
$$
A(x) = D \frac{d}{dx} \left( \ln N - \frac{U(x)}{k_B T} \right) = -\frac{D}{k_B T} \frac{dU(x)}{dx}
$$
由于力 $F(x) = -\frac{dU(x)}{dx}$，这可以写成 $A(x) = \frac{D}{k_B T} F(x)$。这个关系式，以及更广为人知的形式 $D = \mu k_B T$（其中 $\mu$ 是迁移率，定义为 $A(x) = \mu F(x)$），被称为**爱因斯坦-斯莫洛霍夫斯基关系** (Einstein-Smoluchowski relation)。它深刻地揭示了耗散（通过漂移/迁移率体现）和涨落（通过[扩散](@entry_id:141445)/温度体现）之间的内在联系，是涨落-耗散定理的一个具体体现。

例如，对于[谐振子势](@entry_id:750179) $U(x) = \frac{1}{2}\kappa x^2$，力为 $F(x) = -\kappa x$。因此，[漂移系数](@entry_id:199354)必须为 $A(x) = -\frac{D\kappa}{k_B T} x$ [@problem_id:2001801]。如果实验上测得[漂移系数](@entry_id:199354)为 $A(x) = -\gamma x$，通过比较系数，我们可以反解出[扩散](@entry_id:141445)系数 $D = \frac{\gamma k_B T}{\kappa}$ [@problem_id:1934597]。

### 概率守恒与边界条件

[福克-普朗克](@entry_id:635508)方程的连续性方程形式 $\frac{\partial P}{\partial t} = -\nabla \cdot \vec{J}$ 暗示了总概率的守恒。考虑一个区域 $\Omega$，其中的总概率为 $N(t) = \int_{\Omega} P(\vec{r}, t) d\vec{r}$。其随时间的变化率为：
$$
\frac{dN}{dt} = \int_{\Omega} \frac{\partial P}{\partial t} d\vec{r} = -\int_{\Omega} \nabla \cdot \vec{J} d\vec{r} = -\oint_{\partial \Omega} \vec{J} \cdot d\vec{S}
$$
这里我们使用了[高斯散度定理](@entry_id:188065)。这个结果表明，一个区域内总概率的变化率等于通过该区域边界的净[概率流](@entry_id:150949)出的负值。

如果系统定义在整个空间，并且我们要求粒子不会跑到无穷远处（即 $P$ 和 $\vec{J}$ 在无穷远处足够快地趋于零），那么总概率 $\int P d\vec{r}$ 将是一个守恒量。

然而，在有限区域内，边界条件起着决定性作用 [@problem_id:2001797]：
*   **[反射边界](@entry_id:634534)** (Reflecting boundary)：边界是不可逾越的，没有概率流穿过。这要求边界上法向的[概率流](@entry_id:150949)分量为零，即 $\vec{J} \cdot \hat{n} = 0$。
*   **[吸收边界](@entry_id:201489)** (Absorbing boundary)：粒子一旦到达边界就会被移除。这要求边界上的概率密度为零，即 $P = 0$。

考虑一个[DNA结合蛋白](@entry_id:180925)在一维DNA片段 $[0, L]$ 上[扩散](@entry_id:141445)的模型。如果 $x=0$ 是[反射边界](@entry_id:634534)，而 $x=L$ 是一个吸收靶点，那么总概率 $N(t) = \int_0^L P(x,t) dx$ 将会随时间减少。其变化率为：
$$
\frac{dN}{dt} = J(0,t) - J(L,t)
$$
由于 $x=0$ 是[反射边界](@entry_id:634534)， $J(0,t)=0$。因此，$\frac{dN}{dt} = -J(L,t)$。总概率的减少速率等于流出[吸收边界](@entry_id:201489)的概率流。

### 重要极限与高级主题

#### 高摩擦极限：斯莫洛霍夫斯基方程

在许多物理和化学系统中，例如胶体粒子在粘性流体中的运动，粒子动量的弛豫时间远小于其位置变化的[特征时间](@entry_id:173472)。这种情况被称为**高摩擦**或**过阻尼** (overdamped) 极限。在此极限下，我们可以从描述位置和速度的完整[福克-普朗克](@entry_id:635508)方程（有时称为克莱默斯方程）出发，通过绝热消除速度变量，得到一个仅描述位置坐标 $x$ 的概率密度 $P(x,t)$ 的有效方程，即**斯莫洛霍夫斯基方程** (Smoluchowski equation) [@problem_id:2001772]：
$$
\frac{\partial P(x, t)}{\partial t} = \frac{\partial}{\partial x} \left[ \frac{1}{\gamma} \frac{dU(x)}{dx} P(x, t) + D \frac{\partial P(x, t)}{\partial x} \right]
$$
其中 $\gamma$ 是[摩擦系数](@entry_id:150354)。该方程本身就是一个[福克-普朗克](@entry_id:635508)方程，其漂移项 $A(x) = -\frac{1}{\gamma}\frac{dU}{dx}$ 和[扩散](@entry_id:141445)项 $D$ 满足爱因斯坦关系 $D=k_B T/\gamma$。

利用该方程，我们可以分析系统向平衡态弛豫的动力学。例如，对于[谐波](@entry_id:181533)势 $U(x)=\frac{1}{2}Kx^2$，可以推导出平均位置 $\langle x \rangle(t)$ 的演化方程为：
$$
\frac{d\langle x \rangle}{dt} = -\frac{K}{\gamma} \langle x \rangle
$$
这表明平均位置以指数形式衰减到零，其[弛豫时间](@entry_id:191572)常数为 $\tau = \frac{\gamma}{K}$ [@problem_id:2001772]。

#### [乘性噪声](@entry_id:261463)：Itō-Stratonovich 困境

当朗之万方程中的噪声项的强度依赖于系统状态时，我们称之为**[乘性噪声](@entry_id:261463)** (multiplicative noise)。例如，考虑一个具有空间依赖[扩散](@entry_id:141445)的[过阻尼系统](@entry_id:177220) [@problem_id:2190159]：
$$
\frac{dx}{dt} = a(x) + b(x) \xi(t)
$$
其中 $b^2(x) = 2D(x)$。由于[白噪声](@entry_id:145248) $\xi(t)$ 的奇异性，包含 $b(x)\xi(t)$ 的随机积分的数学定义变得模棱两可。主要有两种不同的诠释，它们导致了形式上不同的[福克-普朗克](@entry_id:635508)方程 [@problem_id:2674961]。

1.  **Itō 诠释**：这种诠释在数学上最为方便，它将积分定义为“前向点”近似，即在每个时间步长内，噪声幅度 $b(x)$ 取步长开始时的值。这种非预期的性质使得它在[随机过程](@entry_id:159502)理论中具有许多优良的数学性质。对应的 Itō [福克-普朗克](@entry_id:635508)方程为：
    $$
    \frac{\partial P}{\partial t} = -\frac{\partial}{\partial x}[a(x)P] + \frac{\partial^2}{\partial x^2}[D(x)P]
    $$

2.  **Stratonovich 诠释**：这种诠释使用“中点”近似，更符合物理上光滑路径的极限。它遵循普通的微积分链式法则。对应的 Stratonovich [福克-普朗克](@entry_id:635508)方程形式更为复杂：
    $$
    \frac{\partial P}{\partial t} = -\frac{\partial}{\partial x}[a(x)P] + \frac{\partial}{\partial x}\left[\sqrt{D(x)}\frac{\partial}{\partial x}(\sqrt{D(x)}P)\right]
    $$

这两种描述是等价的，前提是正确地转换漂移项。一个 Stratonovich 过程可以被精确地写成一个具有修正漂移项的 Itō 过程。这个修正项，有时被称为“伪漂移”或“噪声诱导漂移”，其表达式为 $\frac{1}{2}b(x)b'(x)$。即，若一个系统的物理漂移为 $a_S(x)$，那么在 Stratonovich 图像下，漂移项就是 $a_S(x)$；而在 Itō 图像下，为了描述相同的物理过程，必须使用一个修正后的漂移项 $a_I(x) = a_S(x) + \frac{1}{2}b(x)b'(x)$。

在物理建模中，Stratonovich 诠释通常被认为是更“物理”的，因为它是由具有有限关联时间的真实（有色）噪声在关联时间趋于零时的极限。通过绝热消除快变量得到的有效[动力学方程](@entry_id:751029)自然地呈现为 Stratonovich 形式。而 Itō 诠释则是离散[跳跃过程](@entry_id:180953)的[扩散极限](@entry_id:168181)的自然结果，并且在数值模拟（如[欧拉-丸山法](@entry_id:142440)）中被直接实现。理解这两种诠释的差异和联系对于正确建模和分析具有状态依赖性涨落的复杂系统至关重要 [@problem_id:2674961]。

例如，在问题 [@problem_id:2190159] 中，从[朗之万方程](@entry_id:144277) $dx/dt = -k/x + \sqrt{2D_0 x^2}\xi(t)$ 出发，若采用 Itō 诠释，则[漂移系数](@entry_id:199354) $A(x) = -k/x$，[扩散](@entry_id:141445)系数 $D(x) = D_0 x^2$。对应的概率流为 $J(x,t) = A(x)P - \frac{\partial}{\partial x}[D(x)P]$。展开导数后得到 $J = -\frac{k}{x}P - D_0 x^2 \frac{\partial P}{\partial x} - 2D_0 x P$。这里的最后一项 $-2D_0 x P = -D'(x)P$ 就是由于[扩散](@entry_id:141445)系数的空间依赖性而在概率流表达式中出现的额外项，这正是 Itō 形式的特征。