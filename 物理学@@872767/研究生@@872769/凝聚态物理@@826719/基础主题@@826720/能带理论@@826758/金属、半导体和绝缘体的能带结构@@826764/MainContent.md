## 引言
[电子能带结构](@entry_id:136694)是理解固态物质电学、光学和热学性质的基石，是整个凝聚态物理学的核心概念之一。为何有些材料是闪亮的导体，而另一些却是透明的绝缘体？这一基本问题的答案深藏于晶体中电子遵循的量子力学规律之中。本文旨在系统地解决这一问题，弥合从孤立原子到宏观固体电子行为的认知鸿沟。我们将从量子力学第一性原理出发，构建[能带理论](@entry_id:139801)的完整图景。文章的第一部分，“原理与机制”，将深入剖析[布洛赫定理](@entry_id:137461)、[能隙](@entry_id:191975)的形成以及电子在能带中的动力学行为，从而为[金属、半导体和绝缘体](@entry_id:146062)的分类提供坚实的理论基础。第二部分，“应用与[交叉](@entry_id:147634)学科联系”，将展示这些抽象理论如何通过ARPES等实验技术被精确验证，并广泛应用于半导体器件、自旋电子学和[拓扑材料](@entry_id:142123)等前沿领域，揭示理论与现实世界的深刻联系。最后，在“动手实践”部分，你将有机会通过解决具体的计算问题，将理论知识转化为分析真实材料[能带结构](@entry_id:139379)的实践技能。通过这一逐层深入的结构，读者将建立起对[能带理论](@entry_id:139801)全面而深刻的理解。

## 原理与机制

本章旨在深入阐述晶体中电子能带结构的起源、基本原理及其对材料宏观电学和光学性质的决定性影响。我们将从量子力学第一性原理出发，构建[能带理论](@entry_id:139801)的理论框架，进而探讨电子在这些能带中的动力学行为。在此基础上，我们将建立一个严格的分类体系，以区分[金属、半导体和绝缘体](@entry_id:146062)。最后，我们将讨论能带理论的应用范畴及其局限性，并引出超越单粒[子图](@entry_id:273342)像的多体物理概念。

### 电子能带的起源

描述晶体中电子行为的出发点是处理在周期性势场 $V(\mathbf{r}) = V(\mathbf{r} + \mathbf{R})$ 中运动的单个电子，其中 $\mathbf{R}$ 是布拉维格矢。该问题的[哈密顿量](@entry_id:172864)为 $H = -\frac{\hbar^2}{2m}\nabla^2 + V(\mathbf{r})$。由于[势场](@entry_id:143025)的周期性，[哈密顿量](@entry_id:172864)与格点[平移算符](@entry_id:756122) $T_{\mathbf{R}}$ 对易，即 $[H, T_{\mathbf{R}}] = 0$。这意味着我们可以找到一组同时是 $H$ 和所有 $T_{\mathbf{R}}$ 的共同本征态。

#### 布洛赫定理与[晶体动量](@entry_id:136369)

$T_{\mathbf{R}}$ 的[本征值](@entry_id:154894)必须满足平移群的代数关系 $T_{\mathbf{R}_1}T_{\mathbf{R}_2} = T_{\mathbf{R}_1+\mathbf{R}_2}$，这要求其[本征值](@entry_id:154894)具有 $e^{i\mathbf{k}\cdot\mathbf{R}}$ 的形式。因此，[哈密顿量](@entry_id:172864)的本征态（即电子[波函数](@entry_id:147440)）可以被一个矢量 $\mathbf{k}$ 标记，并满足 $T_{\mathbf{R}}\psi_{\mathbf{k}}(\mathbf{r}) = \psi_{\mathbf{k}}(\mathbf{r} + \mathbf{R}) = e^{i\mathbf{k}\cdot\mathbf{R}}\psi_{\mathbf{k}}(\mathbf{r})$。这便是**布洛赫定理 (Bloch's Theorem)**。该定理的一个等价表述是，[波函数](@entry_id:147440)可以写成一个[平面波](@entry_id:189798) $e^{i\mathbf{k}\cdot\mathbf{r}}$ 与一个具有[晶格](@entry_id:196752)周期性的函数 $u_{n\mathbf{k}}(\mathbf{r})$ 的乘积，即 $\psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}}u_{n\mathbf{k}}(\mathbf{r})$。

这里的矢量 $\mathbf{k}$ 被称为**[晶体动量](@entry_id:136369) (crystal momentum)**，它是一个[量子数](@entry_id:145558)，用于标记电子在周期性势场中的[本征态](@entry_id:149904)。值得注意的是，晶体动量 $\hbar\mathbf{k}$ 并非电子的真实动量（即[动量算符](@entry_id:151743) $-i\hbar\nabla$ 的[本征值](@entry_id:154894)），因为在[非均匀势](@entry_id:263876)场中，真实动量不是一个[守恒量](@entry_id:150267)。

[晶体动量](@entry_id:136369)的一个核心性质是它定义在[倒易晶格](@entry_id:136718)空间中，并且是模倒易格矢 $\mathbf{G}$ 定义的。倒易格矢 $\mathbf{G}$ 满足 $e^{i\mathbf{G}\cdot\mathbf{R}} = 1$。因此，对于任意 $\mathbf{G}$，我们有 $e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}e^{i\mathbf{G}\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}$。这意味着[晶体动量](@entry_id:136369) $\mathbf{k}$ 和 $\mathbf{k}+\mathbf{G}$ 对应于平移群的同一个[不可约表示](@entry_id:263310)，它们标记的[量子态](@entry_id:146142)在物理上是等价的。这直接导致了[能量本征值](@entry_id:144381) $E_n(\mathbf{k})$ 的周期性：$E_n(\mathbf{k}) = E_n(\mathbf{k}+\mathbf{G})$。因此，我们只需在倒易晶格的一个[原胞](@entry_id:159354)内研究[能带结构](@entry_id:139379)即可，这个[原胞](@entry_id:159354)通常选为**[第一布里渊区](@entry_id:269110) (First Brillouin Zone)**，它是倒易空间中离原点最近的一块区域 [@problem_id:2971151]。

#### [近自由电子模型](@entry_id:138124)与[能隙](@entry_id:191975)的形成

为了理解能带和[能隙](@entry_id:191975)是如何形成的，我们可以采用**[近自由电子模型](@entry_id:138124) (Nearly-Free Electron Model)**。该模型将[周期性势场](@entry_id:140652) $V(\mathbf{r})$ 视为对[自由电子气](@entry_id:145649)的一个微扰。自由电子的色散关系为 $\epsilon_{\mathbf{k}} = \frac{\hbar^2 |\mathbf{k}|^2}{2m}$，它是一条连续的抛物线。

当引入一个弱的周期性势场 $V(\mathbf{r}) = \sum_{\mathbf{G}} V_{\mathbf{G}} e^{i\mathbf{G}\cdot\mathbf{r}}$ 时，势场的傅里叶分量 $V_{\mathbf{G}}$ 会耦合那些波矢相差一个 $\mathbf{G}$ 的平面波态。当两个或多个这样的平面波态的自由电子[能量简并](@entry_id:203091)时，微扰会产生最显著的影响。这种情况恰好发生在布里渊区的边界上。[布里渊区](@entry_id:142395)边界由[布拉格衍射](@entry_id:148063)条件 $| \mathbf{k} |^2 = | \mathbf{k} - \mathbf{G} |^2$ 定义，等价于 $2\mathbf{k}\cdot\mathbf{G} = |\mathbf{G}|^2$。

在满足此条件的 $\mathbf{k}$ 点，自由电子态 $|\mathbf{k}\rangle$ 和 $|\mathbf{k}-\mathbf{G}\rangle$ 的[能量简并](@entry_id:203091)，$\epsilon_{\mathbf{k}} = \epsilon_{\mathbf{k}-\mathbf{G}}$。我们可以应用[简并微扰理论](@entry_id:143587)，在由这两个态张成的[子空间](@entry_id:150286)中对角化[哈密顿量](@entry_id:172864)矩阵。该 $2\times2$ [有效哈密顿量](@entry_id:748813)矩阵为：
$$
\mathbf{H}_{\text{eff}} = \begin{pmatrix} \langle\mathbf{k}|H|\mathbf{k}\rangle  \langle\mathbf{k}|H|\mathbf{k}-\mathbf{G}\rangle \\ \langle\mathbf{k}-\mathbf{G}|H|\mathbf{k}\rangle  \langle\mathbf{k}-\mathbf{G}|H|\mathbf{k}-\mathbf{G}\rangle \end{pmatrix} = \begin{pmatrix} \epsilon_{\mathbf{k}}  V_{\mathbf{G}} \\ V_{-\mathbf{G}}  \epsilon_{\mathbf{k}-\mathbf{G}} \end{pmatrix}
$$
这里我们忽略了势的平均值 $V_0$。在简并点，$\epsilon_{\mathbf{k}} = \epsilon_{\mathbf{k}-\mathbf{G}}$。求解本征值问题，并利用实势场条件 $V_{-\mathbf{G}} = V_{\mathbf{G}}^*$，我们得到两个新的[能量本征值](@entry_id:144381)：
$$
E_{\pm} = \epsilon_{\mathbf{k}} \pm |V_{\mathbf{G}}|
$$
可见，原来的简并能级被微扰打开，形成了一个宽度为 $E_g = E_+ - E_- = 2|V_{\mathbf{G}}|$ 的**[能隙](@entry_id:191975) (band gap)** [@problem_id:2971127]。这个[能隙](@entry_id:191975)的打开是[布洛赫电子](@entry_id:277005)与[晶格](@entry_id:196752)[周期性势场](@entry_id:140652)发生[相干散射](@entry_id:267724)（[布拉格衍射](@entry_id:148063)）的直接结果，是一个单粒子量子现象，无需考虑[电子-电子相互作用](@entry_id:139900) [@problem_id:2971121]。

在[能隙](@entry_id:191975)边界处，新的[本征态](@entry_id:149904)是原来两个[平面波](@entry_id:189798)的相干叠加，形成驻波。能量较低的态 $\psi_-$ 的电子云密度倾向于聚集在[势能](@entry_id:748988) $V(\mathbf{r})$ 较低的区域（离子实附近），而能量较高的态 $\psi_+$ 的电子云密度则聚集在势能较高的区域（离子实之间）。这种电荷密度的重新[分布](@entry_id:182848)正是能级劈裂的物理根源 [@problem_id:2971121]。如果由于[晶体结构](@entry_id:140373)的对称性导致某个 $V_{\mathbf{G}}$ 为零，那么在一级微扰下，对应的[布里渊区](@entry_id:142395)边界上不会打开[能隙](@entry_id:191975)。

### 电子动力学与[有效质量](@entry_id:142879)

能带理论不仅给出了电子的静态能谱，还提供了描述电子在外场下动力学行为的框架。

#### [半经典运动方程](@entry_id:138500)

在一个缓变的[电场](@entry_id:194326) $\mathbf{E}$ 和[磁场](@entry_id:153296) $\mathbf{B}$ 中，一个位于能带 $n$、晶体动量为 $\mathbf{k}$ 的电子[波包](@entry_id:154698)的运动由以下**[半经典运动方程](@entry_id:138500) (semiclassical equations of motion)** 描述：
$$
\hbar \frac{d\mathbf{k}}{dt} = -e(\mathbf{E} + \mathbf{v}_n(\mathbf{k}) \times \mathbf{B})
$$
$$
\mathbf{v}_n(\mathbf{k}) = \frac{1}{\hbar} \nabla_{\mathbf{k}} E_n(\mathbf{k})
$$
其中，$\mathbf{v}_n(\mathbf{k})$ 是电子波包的**[群速度](@entry_id:147686) (group velocity)**，它描述了电子在晶体中的运动速度。这个速度由[能带色散](@entry_id:138609)关系 $E_n(\mathbf{k})$ 的梯度决定，而非与 $\mathbf{k}$ 成正比。

#### [有效质量](@entry_id:142879)与空穴

电子在[电场](@entry_id:194326)中的加速度 $\mathbf{a} = d\mathbf{v}_n/dt$ 可以通过[链式法则](@entry_id:190743)计算得出：
$$
a_i = \frac{1}{\hbar} \sum_j \frac{\partial^2 E_n}{\partial k_i \partial k_j} \frac{dk_j}{dt} = \frac{1}{\hbar^2} \sum_j \left( \frac{\partial^2 E_n}{\partial k_i \partial k_j} \right) (-eE_j)
$$
将此式与牛顿第二定律的张量形式 $a_i = \sum_j (m^*)^{-1}_{ij} F_j$ 进行比较，其中作用在电子上的力为 $F_j = -eE_j$，我们可以定义一个**[有效质量张量](@entry_id:147018) (effective mass tensor)** $m^*$：
$$
(m^*)^{-1}_{ij} = \frac{1}{\hbar^2} \frac{\partial^2 E_n}{\partial k_i \partial k_j}
$$
[有效质量](@entry_id:142879)描述了电子在晶体中对外界力的响应程度，它由能带的**曲率 (curvature)** 决定。在能带底部，[色散关系](@entry_id:140395)近似为抛物线型 $E(\mathbf{k}) \approx E_c + \frac{\hbar^2 k^2}{2m_e^*}$，曲率为正，有效质量 $m_e^*$ 为正。

对于一个近乎填满的能带（价带），用少数的空态来描述系统更为方便。这些空态被称为**空穴 (holes)**。一个空穴可以被看作一个[准粒子](@entry_id:136584)，其[电荷](@entry_id:275494)为 $+e$，晶体动量为 $\mathbf{k}_h = -\mathbf{k}_e$（其中 $\mathbf{k}_e$ 是所缺失电子的晶体动量）。空穴的动力学行为由其自身有效质量 $m_h^*$ 描述，其张量定义为：
$$
(m_h^*)^{-1}_{ij} = -\frac{1}{\hbar^2} \frac{\partial^2 E_v}{\partial k_i \partial k_j}
$$
在价带顶（能带极大值处），能带曲率为负，$\partial^2 E_v / \partial k_i \partial k_j \le 0$。因此，定义中的负号确保了空穴的有效质量 $m_h^*$ 是正的。例如，在一个[简单立方晶格](@entry_id:160687)的[紧束缚模型](@entry_id:143446)中，价带顶在 $\Gamma$ 点（$\mathbf{k}=0$），其色散关系近似为 $E_v(\mathbf{k}) \approx E_v^0 - t a^2 |\mathbf{k}|^2$（其中 $t$ 为[跃迁积分](@entry_id:147296)，$a$ 为晶格常数）。通过计算[二阶导数](@entry_id:144508)，可以得到一个正的、各向同性的空穴有效质量 $m_h^* = \frac{\hbar^2}{2ta^2}$ [@problem_id:2971134]。

### 固体的分类：金属、绝缘体与[半导体](@entry_id:141536)

[材料的电学性质](@entry_id:197927)主要取决于其能带结构以及电子对能带的填充情况。在绝对零度 $T=0$ 时，电子会填充从最低能量开始的所有可用[量子态](@entry_id:146142)，直到一个称为**费米能级 (Fermi level)** $E_F$ 的能量。

#### 金属

如果[费米能级](@entry_id:143215) $E_F$ 穿过一个或多个能带，这意味着存在一个或多个**部分填充的能带 (partially filled bands)**，那么该材料就是**金属 (metal)**。在 $\mathbf{k}$ 空间中，由方程 $E_n(\mathbf{k}) = E_F$ 定义的[等能面](@entry_id:262911)被称为**费米面 (Fermi surface)**。

[费米面](@entry_id:137798)的存在是金属[导电性](@entry_id:137481)的根本原因。当施加一个微弱的[电场](@entry_id:194326)时，费米面附近的电子可以被加速到能量稍高的、邻近的未占据态，从而形成净电流。只要[费米面](@entry_id:137798)上的态具有非零的[群速度](@entry_id:147686)，系统在 $T=0$ 的纯净极限下就表现出有限的[直流电导率](@entry_id:273370)，即存在一个**[德鲁德权重](@entry_id:140162) (Drude weight)**。反之，如果[费米能级](@entry_id:143215)处的态速度处处为零（例如，一个完全平坦的能带），尽管[费米面](@entry_id:137798)存在，系统也不会表现出金属性 [@problem_id:2971120]。

对于典型的金属，载流子浓度 $n$ 基本不随温度变化。其电导率 $\sigma(T)$ 的温度依赖性主要来源于[散射时间](@entry_id:272979) $\tau(T)$ 的变化。随着温度升高，[电子-声子散射](@entry_id:138098)增强，导致 $\tau(T)$ 减小，从而[电导率](@entry_id:137481)下降 [@problem_id:2971101]。

#### 绝缘体与[半导体](@entry_id:141536)

如果[费米能级](@entry_id:143215) $E_F$ 恰好位于两个能带之间的[能隙](@entry_id:191975)中，那么在 $T=0$ 时，所有费米能级以下的能带（[价带](@entry_id:158227)）被完全填满，而所有费米能级以上的能带（[导带](@entry_id:159736)）完全空着。这样的材料被称为**绝缘体 (insulator)** 或**[半导体](@entry_id:141536) (semiconductor)**。

一个完全填满的能带无法贡献净电流。这是因为对于一个填满的能带 $n$，其对[电流密度](@entry_id:190690)的贡献正比于 $\int_{\text{BZ}} \mathbf{v}_n(\mathbf{k}) d^3k = \frac{1}{\hbar}\int_{\text{BZ}} \nabla_{\mathbf{k}} E_n(\mathbf{k}) d^3k$。根据[高斯定理](@entry_id:143110)，这个[体积分](@entry_id:171119)可以转化为布里渊区边界上的[面积分](@entry_id:275394)，由于 $E_n(\mathbf{k})$ 的周期性，该面积分为零。因此，在 $T=0$ 且存在[能隙](@entry_id:191975)的情况下，没有载流子可以响应[电场](@entry_id:194326)，[电导率](@entry_id:137481)为零 [@problem_id:2971077]。

当温度 $T>0$ 时，部分电子可以借助热能（[能量尺度](@entry_id:196201)为 $k_B T$）越过[能隙](@entry_id:191975)，从价带激发到[导带](@entry_id:159736)，形成导带中的电子和[价带](@entry_id:158227)中的空穴。这些热生载流子的浓度 $n(T)$ 对温度极其敏感，近似地随 $e^{-E_g / (2k_B T)}$ 指数增长。尽管[载流子迁移率](@entry_id:158766)会因[声子散射](@entry_id:140674)增强而随温度升高而略有下降，但[载流子浓度](@entry_id:143028)的[指数增长](@entry_id:141869)是主导因素，导致[半导体](@entry_id:141536)的[电导率](@entry_id:137481)随温度升高而显著增加 [@problem_id:2971101]。

绝缘体和[半导体](@entry_id:141536)之间的区别是量化的，而非本质的。通常，[能隙](@entry_id:191975) $E_g$ 较大的材料（例如，大于 3 eV）被称为绝缘体，因为在室温下其[本征载流子浓度](@entry_id:144530)极低；[能隙](@entry_id:191975)较小的被称为[半导体](@entry_id:141536)。

#### 精细分类：[半金属](@entry_id:152277)

能带填充规则可以更精确地表述：一个[原胞](@entry_id:159354)内含有奇数个价电子的晶体，在单粒子能带理论中**必然**是金属。这是因为每个（考虑自旋的）非简并能带可以容纳偶数个电子（每个 $\mathbf{k}$ 点两个[自旋态](@entry_id:149436)），所以奇数个电子无法完全填满整数个能带。

然而，一个[原胞](@entry_id:159354)内含有偶数个价电子的晶体**未必**是绝缘体。虽然偶数个电子原则上可以填满整数个能带，但能带的能量顺序可能在 $\mathbf{k}$ 空间中发生交错。如果最高[价带](@entry_id:158227)的能量最大值 $E_v^{\text{max}}$ 高于最低导带的能量最小值 $E_c^{\text{min}}$（即 $E_v^{\text{max}} > E_c^{\text{min}}$），则会发生**能带交叠 (band overlap)**。在这种情况下，[价带](@entry_id:158227)顶部的一些电子会“溢出”到[导带](@entry_id:159736)的底部，直到系统达到一个统一的费米能级。这导致在[价带](@entry_id:158227)顶附近形成小的[空穴口袋](@entry_id:269009)，在[导带](@entry_id:159736)底附近形成小的[电子口袋](@entry_id:266080)。尽管总电子数是偶数，但系统在 $T=0$ 时仍然拥有一个费米面和有限的载流子浓度，表现出金属性。这类材料被称为**半金属 (semimetal)** [@problem_id:2971077]。石墨和铋是典型的半金属。

从能带交叠的半金属到具有小间接[能隙](@entry_id:191975)的[半导体](@entry_id:141536)，可以通过调节参数（如压力）实现连续的[相变](@entry_id:147324)。当能带交叠量 $\Delta = E_{v0} - E_{c0}$ 从正值变为负值时，电子和空穴口袋的体积会[连续收缩](@entry_id:154115)至零，费米面消失。这种由[费米面拓扑](@entry_id:138700)结构改变驱动的[相变](@entry_id:147324)被称为**里夫希茨[相变](@entry_id:147324) (Lifshitz transition)** [@problem_id:2971116]。

### 与光的相互作用：探测[能带结构](@entry_id:139379)

材料的光学性质，特别是[光吸收](@entry_id:136597)，为实验探测能带结构提供了强有力的工具。电子吸收一个能量为 $\hbar\omega$、波矢为 $\mathbf{q}$ 的[光子](@entry_id:145192)，从初态 $(\mathbf{k}_i, E_i)$ 跃迁到末态 $(\mathbf{k}_f, E_f)$，必须同时满足能量和[晶体动量守恒](@entry_id:145588)：
$$
E_f = E_i + \hbar\omega
$$
$$
\mathbf{k}_f = \mathbf{k}_i + \mathbf{q} \pmod{\mathbf{G}}
$$
对于可见光或红外光，[光子](@entry_id:145192)波矢 $\mathbf{q}$ 的大小远小于布里渊区的尺寸。因此，在光吸收过程中，电子的[晶体动量](@entry_id:136369)近似守恒，即 $\mathbf{k}_f \approx \mathbf{k}_i$。这意味着光跃迁在 $E-\mathbf{k}$ 图上是**垂直 (vertical)** 的。

这一选择定则导致了**直接[能隙](@entry_id:191975) (direct band gap)** 和**间接[能隙](@entry_id:191975) (indirect band gap)** 的重要区别：
*   **直接[能隙](@entry_id:191975)**：如果[价带](@entry_id:158227)顶（VBM）和导带底（CBM）位于 $\mathbf{k}$ 空间中的同一点，即 $\mathbf{k}_v = \mathbf{k}_c$，那么材料具有直接[能隙](@entry_id:191975)。在[能隙](@entry_id:191975)边缘的吸收可以通过单个[光子](@entry_id:145192)过程高效地发生，因为动量守恒条件天然满足。GaAs 就是一个典型的直接[能隙](@entry_id:191975)[半导体](@entry_id:141536)。

*   **间接[能隙](@entry_id:191975)**：如果价带顶和[导带](@entry_id:159736)底位于 $\mathbf{k}$ 空间中的不同点，即 $\mathbf{k}_v \neq \mathbf{k}_c$，那么材料具有间接[能隙](@entry_id:191975)。在这种情况下，要实现从价带顶到[导带](@entry_id:159736)底的最低能量跃迁，电子不仅需要吸收[光子](@entry_id:145192)获得能量，还需要通过与**[声子](@entry_id:140728) (phonon)** 的相互作用来改变其[晶体动量](@entry_id:136369)，以弥补 $\mathbf{k}_c - \mathbf{k}_v$ 的差值。由于这是一个涉及[光子](@entry_id:145192)和[声子](@entry_id:140728)的二阶过程，其跃迁几率远低于直接跃迁。硅（Si）和锗（Ge）是典型的间接[能隙](@entry_id:191975)[半导体](@entry_id:141536) [@problem_id:2971087]。

### 超越单粒[子图](@entry_id:273342)像

至今为止的讨论都基于一个核心假设：电子之间不相互作用，它们只是在同一个静态的周期性势场中独立运动。这个**[单粒子近似](@entry_id:138558) (single-particle approximation)** 是能带理论的基石，它在解释大量[材料性质](@entry_id:146723)方面取得了巨大成功。然而，电子间的库仑排斥是真实存在的，在某些情况下，这种相互作用会从根本上改变材料的物理性质，导致单粒子能带理论失效。

#### [准粒子](@entry_id:136584)与[自能](@entry_id:145608)

在多体物理的框架下，与[晶格](@entry_id:196752)相互作用的电子云被重新概念化为一个**[准粒子](@entry_id:136584) (quasiparticle)**。[准粒子](@entry_id:136584)可以被看作一个被其自身引起的极化云“穿着”的电子。它的性质（如能量和寿命）与裸电子不同，这些修正由一个称为**[自能](@entry_id:145608) (self-energy)** $\Sigma(\mathbf{k}, \omega)$ 的复数量描述。

[准粒子](@entry_id:136584)的能量 $E_{\mathbf{k}}$ 不再由简单的薛定谔方程给出，而是由[戴森方程](@entry_id:146246)的实部决定：
$$
E_{\mathbf{k}} - \epsilon_{\mathbf{k}} - \text{Re}\Sigma(\mathbf{k}, E_{\mathbf{k}}) = 0
$$
这里 $\epsilon_{\mathbf{k}}$ 是单粒子能带理论中的能量。$\text{Re}\Sigma$ 对单粒子能带进行了修正，而 $\text{Im}\Sigma$ 则与[准粒子](@entry_id:136584)的有限寿命 $\tau_{\mathbf{k}}$ 相关，$\tau_{\mathbf{k}} \propto 1/|\text{Im}\Sigma|$。一个定义良好的[准粒子](@entry_id:136584)要求其寿命足够长，即 $|\text{Im}\Sigma|$ 足够小。

实验上，如**角分辨光电子能谱 (ARPES)** 等技术测量的正是[准粒子](@entry_id:136584)的谱函数 $A(\mathbf{k}, \omega)$，其峰位对应于[准粒子](@entry_id:136584)的[色散关系](@entry_id:140395) $E_{\mathbf{k}}$。理论计算（如 $GW$ 方法）的目标就是计算[自能](@entry_id:145608)，从而得到与实验可比的[准粒子](@entry_id:136584)[能带结构](@entry_id:139379)。对于[半导体](@entry_id:141536)和绝缘体，电子相互作用通常会修正[能隙](@entry_id:191975)的大小，这解释了为何基于[密度泛函理论](@entry_id:139027)（一种平均场理论）计算的[能隙](@entry_id:191975)通常小于实验值 [@problem_id:2971081]。

#### [莫特绝缘体](@entry_id:140685)

[能带理论](@entry_id:139801)最引人注目的失败之一是无法解释**莫特绝缘体 (Mott insulator)**。考虑一个简单的晶体，每个[原胞](@entry_id:159354)只有一个原子，且该原子最外层只有一个电子（例如，一个由氢原子构成的假想晶体）。根据能带理论，该系统每个原胞有奇数个电子，其能带必然是半填充的，因此它必须是金属。

然而，实验和更高级的理论表明，当原子间距足够大时，这类材料实际上是绝缘体。**哈伯德模型 (Hubbard model)** 抓住了这个问题的本质。该模型在[紧束缚模型](@entry_id:143446)的基础上增加了一个描述电子在同一个格点上相遇时的库仑排斥能 $U$ 的项：
$$
H = -t \sum_{\langle ij \rangle, \sigma} (c^\dagger_{i\sigma} c_{j\sigma} + h.c.) + U \sum_i n_{i\uparrow} n_{i\downarrow}
$$
在强关联极限下 ($U \gg t$)，电子为了避免支付巨大的能量代价 $U$，会尽可能避免在同一个原子上出现双重占据。在半填充情况下，每个格点上都有一个电子。任何电子的移动（跃迁到邻近格点）都必然会产生一个双重占据的格点和一个空格点，这个过程需要克服一个约为 $U$ 的[能量势](@entry_id:748988)垒。这个由强电子关联打开的[能隙](@entry_id:191975)被称为**莫特[能隙](@entry_id:191975) (Mott gap)**。

因此，[莫特绝缘体](@entry_id:140685)是一种由于强电子间[库仑排斥](@entry_id:181876)导致电子局域化而形成的绝缘体，其机制完全超出了将电子视为在[周期势](@entry_id:140652)中独立运动的[能带理论](@entry_id:139801)范畴 [@problem_id:2971123]。这类现象标志着从能带物理到强关联多体物理的过渡，是现代凝聚态物理的核心研究领域之一。