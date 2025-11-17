## 引言
在凝聚态物理中，理解粒子间的相互作用是揭示材料宏观性质的关键。孤立的[点电荷](@entry_id:263616)在真空中产生长程的[库仑势](@entry_id:154276)，但在固体中，情况截然不同。固体中存在的大量可移动载流子（如电子）会对外来[电荷](@entry_id:275494)作出集体响应，极大地改变其产生的[电场](@entry_id:194326)。这种现象被称为**[静电屏蔽](@entry_id:192260)**，它是理解金属[导电性](@entry_id:137481)、[半导体器件](@entry_id:192345)行为、合金稳定性乃至[化学反应](@entry_id:146973)活性的基础。然而，对这一看似简单的概念进行精确的理论描述，需要我们从量子力学和统计物理的基本原理出发，解决一个复杂的自洽问题：载流子响应[电场](@entry_id:194326)，而它们的响应又反过来改变了[电场](@entry_id:194326)。

本文旨在系统地阐述固体中静[电荷屏蔽](@entry_id:139450)的物理理论，填补基本电磁学直觉与凝聚态[多体理论](@entry_id:169452)之间的知识鸿沟。我们将带领读者从基础原理走向前沿应用，构建一幅完整而深入的物理图像。
在“**原理与机制**”一章中，我们将建立描述屏蔽的[介电函数](@entry_id:136859)形式，并详细剖析两种经典的屏蔽模型——[托马斯-费米模型](@entry_id:158193)和德拜-休克尔模型。我们还将超越这些简化图像，探讨由[费米面拓扑](@entry_id:138700)引起的[弗里德尔振荡](@entry_id:146905)，并讨论随机相近似的局限与修正。
随后，在“**应用与[交叉](@entry_id:147634)学科联系**”一章中，我们将展示这些理论如何在[半导体](@entry_id:141536)物理、金属学、[计算化学](@entry_id:143039)和软物质科学等领域找到具体应用，揭示[屏蔽效应](@entry_id:136974)在解释和预测[材料性质](@entry_id:146723)中的核心作用。
最后，在“**动手实践**”部分，读者将通过解决一系列精心设计的问题，亲手推导关键的物理结果，从而将理论知识转化为解决实际问题的能力，深化对屏蔽维度效应和量子振荡等核心概念的理解。

## 原理与机制

本章旨在深入探讨固体中静[电荷屏蔽](@entry_id:139450)的物理原理与核心机制。我们将从[自洽场理论](@entry_id:193711)出发，建立描述屏蔽现象的介电函数形式；随后，我们将详细分析两种典型的屏蔽模型——适用于[量子简并](@entry_id:146335)系统的托马斯-费米（Thomas-Fermi）模型和适用于经典非[简并系统](@entry_id:203460)的德拜-休克尔（Debye-Hückel）模型；接着，我们将超越这些简化模型，讨论由[费米面拓扑](@entry_id:138700)结构导致的弗里德尔（Friedel）[振荡](@entry_id:267781)现象；最后，我们将探讨随机相近似（RPA）的局限性，并引入[局域场修正](@entry_id:143541)（local-field corrections）的概念，以更精确地描述电子间的交换与关联效应。

### [自洽场](@entry_id:136549)与[介电函数](@entry_id:136859)：屏蔽的形式化描述

在固体中，引入一个外部[电荷](@entry_id:275494)（例如一个杂质离子）会扰乱原先处于平衡态的电子系统。固体内可移动的载流子（主要是电子）会重新排布，以试图“中和”或“屏蔽”这个外部[电荷](@entry_id:275494)产生的[电场](@entry_id:194326)。这种效应导致外部[电荷](@entry_id:275494)的[库仑势](@entry_id:154276)在长距离下被显著削弱。为了从理论上精确描述这一现象，我们需要引入自洽场的概念。

总的[静电势](@entry_id:188370) $\phi_{\text{tot}}(\mathbf{r})$ 是外部[电荷](@entry_id:275494)产生的外部势 $\phi_{\text{ext}}(\mathbf{r})$ 与可动载流子重新排布所产生的感应势 $\phi_{\text{ind}}(\mathbf{r})$ 的叠加：
$$ \phi_{\text{tot}}(\mathbf{r}) = \phi_{\text{ext}}(\mathbf{r}) + \phi_{\text{ind}}(\mathbf{r}) $$

感应势是由[感应电荷](@entry_id:266454)密度 $\rho_{\text{ind}}(\mathbf{r})$ 产生的，它们之间的关系由泊松方程确定。在傅里叶空间中，这一关系变为 $-q^2\phi_{\text{ind}}(\mathbf{q}) = \rho_{\text{ind}}(\mathbf{q})/\epsilon_b$，其中 $q=|\mathbf{q}|$ 是波矢的大小，$\epsilon_b$ 是背景[介电常数](@entry_id:146714)，代表了除我们正在考虑的可动载流子之外，固体中其他所有部分的贡献（例如，原子实离子的极化）。

[线性响应理论](@entry_id:145737)的核心思想是，在一个弱的扰动下，系统的响应（即[感应电荷](@entry_id:266454)密度）与引起它的**总**扰动（即总[电势](@entry_id:267554)）成正比。这是一个**自洽**的条件，因为[感应电荷](@entry_id:266454)本身又会贡献于总[电势](@entry_id:267554)。为了精确描述这一关系，我们引入极化函数（polarization function）$\Pi(\mathbf{q})$。电子[数密度](@entry_id:268986)的变化 $\delta n(\mathbf{q})$ 响应于电子感受到的总[势能](@entry_id:748988) $U_{\text{tot}}(\mathbf{q}) = -e\phi_{\text{tot}}(\mathbf{q})$：
$$ \delta n(\mathbf{q}) = \Pi(\mathbf{q}) U_{\text{tot}}(\mathbf{q}) = \Pi(\mathbf{q}) [-e \phi_{\text{tot}}(\mathbf{q})] $$
由于[感应电荷](@entry_id:266454)密度 $\rho_{\text{ind}}(\mathbf{q}) = -e \delta n(\mathbf{q})$，我们得到[感应电荷](@entry_id:266454)和总[电势](@entry_id:267554)之间的关键关系：
$$ \rho_{\text{ind}}(\mathbf{q}) = -e \left( -e \Pi(\mathbf{q}) \phi_{\text{tot}}(\mathbf{q}) \right) = e^{2}\Pi(\mathbf{q})\phi_{\text{tot}}(\mathbf{q}) $$
物理上，对于吸引电子的正[电势](@entry_id:267554)（$\phi_{\text{tot}} > 0$），电子会聚集过来，导致[感应电荷](@entry_id:266454)密度为负（$\rho_{\text{ind}}  0$）。这意味着对于[自由电子气模型](@entry_id:155154)，极化函数 $\Pi(\mathbf{q})$ 本身是一个负值。

现在我们可以将所有部分组合起来。在傅里叶空间中，感应势为：
$$ \phi_{\text{ind}}(\mathbf{q}) = \frac{\rho_{\text{ind}}(\mathbf{q})}{\epsilon_{0} q^{2}} = \frac{e^{2}\Pi(\mathbf{q})}{\epsilon_{0} q^{2}} \phi_{\text{tot}}(\mathbf{q}) $$
这里为简化起见，我们暂时忽略背景[介电常数](@entry_id:146714)，即令 $\epsilon_b=\epsilon_0$（[真空介电常数](@entry_id:204253)）。令[库仑相互作用](@entry_id:747947)的傅里叶形式为 $v(q) = e^{2}/(\epsilon_{0} q^{2})$，则上式变为：
$$ \phi_{\text{ind}}(\mathbf{q}) = v(q) \Pi(\mathbf{q}) \phi_{\text{tot}}(\mathbf{q}) $$
将其代入总[电势](@entry_id:267554)的定义式 $\phi_{\text{tot}} = \phi_{\text{ext}} + \phi_{\text{ind}}$ 中：
$$ \phi_{\text{tot}}(\mathbf{q}) = \phi_{\text{ext}}(\mathbf{q}) + v(q) \Pi(\mathbf{q}) \phi_{\text{tot}}(\mathbf{q}) $$
整理后可得：
$$ \phi_{\text{tot}}(\mathbf{q}) [1 - v(q) \Pi(\mathbf{q})] = \phi_{\text{ext}}(\mathbf{q}) $$
这引出了纵向介电函数 $\epsilon(\mathbf{q})$ 的定义。它将总[电势](@entry_id:267554)与外部[电势](@entry_id:267554)联系起来，描述了媒介如何削弱外部[电势](@entry_id:267554)：
$$ \phi_{\text{tot}}(\mathbf{q}) = \frac{\phi_{\text{ext}}(\mathbf{q})}{\epsilon(\mathbf{q})} $$
其中，[介电函数](@entry_id:136859)由下式给出：
$$ \epsilon(\mathbf{q}) = 1 - v(q) \Pi(\mathbf{q}) $$
这个表达式是随机相近似（Random Phase Approximation, RPA）的核心结果。它表明，要计算[介电函数](@entry_id:136859)，关键在于得到系统的极化函数 $\Pi(\mathbf{q})$。由于 $\Pi(\mathbf{q})$ 通常为负值而 $v(q)$ 为正值，因此 $\epsilon(\mathbf{q})$ 通常大于1，这体现了[电荷](@entry_id:275494)的屏蔽效应。

### [静态极限](@entry_id:262480)的物理内涵

上述讨论是在**静态**极限下进行的，即我们只考虑不随时间变化的[电荷](@entry_id:275494)和[电势](@entry_id:267554)。这一看似简单的假设背后蕴含着深刻的物理意义。

[静态极限](@entry_id:262480)（频率 $\omega=0$）在物理上对应于一个**绝热开启**并长期保持不变的扰动。这意味着外部势场是从零开始，在一个远大于系统内部[弛豫时间](@entry_id:191572)的尺度 $T_{\text{sw}}$ 上缓慢地施加的。这种缓慢的过程保证了系统在每个瞬间都近似处于[局部平衡](@entry_id:156295)态，而不会激发等离激元等高频集体模式。当扰动最终固定后，系统达到一个稳定的[定态](@entry_id:137260)，此时[感应电荷](@entry_id:266454)密度 $\rho_{\text{ind}}$ 不再随时间变化，即 $\partial_t \rho = 0$。

在多组分固体中，不同载流子的响应时间不同。电子的弛豫时间通常非常短（飞秒量级），而离子（或[晶格](@entry_id:196752)）的[振动](@entry_id:267781)周期（皮秒量级）则长得多。因此，施加扰动的速率决定了哪些组分能对屏蔽做出贡献：
- 如果 $T_{\text{sw}}$ 远大于离子[振动](@entry_id:267781)周期，电子和离子都有足够的时间达到新的[平衡位置](@entry_id:272392)，[屏蔽效应](@entry_id:136974)由**静态[介电常数](@entry_id:146714)** $\epsilon_s$ (或 $\epsilon_0$) 描述，它包含了电子和离子的全部贡献。
- 如果 $T_{\text{sw}}$ 远小于离子[振动](@entry_id:267781)周期但远大于电子[弛豫时间](@entry_id:191572)，则只有电子能跟上[势场](@entry_id:143025)的变化，而离子因其惯性被“冻结”在原位。此时的屏蔽由**高频[介电常数](@entry_id:146714)** $\epsilon_\infty$ 描述，它只包含电子的贡献。

此外，对于一个空间局域的扰动（如[点电荷](@entry_id:263616)），其傅里叶展开包含一系列不同波矢 $\mathbf{q}$ 的分量。为了描述[屏蔽势](@entry_id:193863)在空间中的具体形态，我们必须考虑[介电函数](@entry_id:136859)在有限 $\mathbf{q}$ 值的行为，而不仅仅是 $\mathbf{q} \to 0$ 的极限。因此，正确的处理顺序是先取[静态极限](@entry_id:262480) $\omega \to 0$，再分析其对不同 $\mathbf{q}$ 分量的影响。这与研究宏观[输运性质](@entry_id:203130)（如[电导率](@entry_id:137481)）时先取长波极限 $\mathbf{q} \to 0$ 的顺序是截然不同的。

最后，静态描述忽略了[电磁场](@entry_id:265881)的传播延迟（retardation effects）。这在扰动尺度 $L$ 远小于[电磁波](@entry_id:269629)波长 $c/\omega$ 时是合理的。在严格的[静态极限](@entry_id:262480) $\omega=0$下，此条件自然满足，[泊松方程](@entry_id:143763)是精确的。

### [托马斯-费米模型](@entry_id:158193)：[简并电子气](@entry_id:161524)中的屏蔽

最简单且应用最广的屏蔽模型之一是托马斯-费米（Thomas-Fermi, TF）理论，它适用于高密度、低温下的[简并电子气](@entry_id:161524)（如金属中的传导电子）。T[F理论](@entry_id:184208)本质上是RPA在长波极限（$q \to 0$）下的近似。

其核心思想是，在一个缓慢变化的[电势](@entry_id:267554)场中，可以认为局部电子密度 $n(\mathbf{r})$ 由局部的[电化学势](@entry_id:141179)决定。在平衡状态下，整个体系的[电化学势](@entry_id:141179) $\mu_{\text{ec}}(\mathbf{r}) = \mu_{\text{int}}(\mathbf{r}) - e\phi_{\text{tot}}(\mathbf{r})$ 必须是一个常数，其中 $\mu_{\text{int}}$ 是与电子密度相关的内禀化学势。这意味着内禀化学势的变化 $\delta\mu_{\text{int}}$ 必须精确地补偿势能的变化：$\delta\mu_{\text{int}} = e\phi_{\text{tot}}$。

在[线性响应](@entry_id:146180)下，密度的变化 $\delta n$ 与内禀化学势的变化 $\delta\mu_{\text{int}}$ 成正比：
$$ \delta n = \left(\frac{\partial n}{\partial \mu}\right) \delta\mu_{\text{int}} = \left(\frac{\partial n}{\partial \mu}\right) e\phi_{\text{tot}} $$
将其与我们之前的关系式 $\delta n = -e \Pi \phi_{\text{tot}}$ 比较，可以得到极化函数在长波极限下的重要结果，即**[可压缩性求和规则](@entry_id:151722)**（compressibility sum rule）：
$$ \lim_{q \to 0} \Pi(q) = - \frac{\partial n}{\partial \mu} $$
这里的[热力学](@entry_id:141121)导数 $\partial n/\partial \mu$ 反映了改变化学势时系统容纳更多粒子的能力，与系统的可压缩性直接相关。对于费米系统，在零温下，$\mu$ 等于费米能 $\epsilon_F$，而 $\partial n/\partial \mu$ 恰好等于费米能级处的[态密度](@entry_id:147894) $g(\epsilon_F)$。

将此结果代入[介电函数](@entry_id:136859) $\epsilon(q) = 1 - v(q)\Pi(q)$ 中，并取 $q \to 0$ 极限：
$$ \epsilon(q) \approx 1 - \frac{e^2}{\epsilon_0 q^2} \left(-\frac{\partial n}{\partial \mu}\right) = 1 + \frac{e^2}{\epsilon_0 q^2} \frac{\partial n}{\partial \mu} $$
这正是TF[介电函数](@entry_id:136859)的形式，通常写作 $\epsilon(q) = 1 + \kappa_{\text{TF}}^2 / q^2$，其中 $\kappa_{\text{TF}}$ 是**[托马斯-费米屏蔽](@entry_id:145372)波矢**，其平方由下式定义：
$$ \kappa_{\text{TF}}^2 = \frac{e^2}{\epsilon_0} \frac{\partial n}{\partial \mu} = \frac{e^2}{\epsilon_0} g(\epsilon_F) $$
对于零温下的三维[自由电子气](@entry_id:145649)，可以具体计算出 $g(\epsilon_F) = \frac{m k_F}{\pi^2 \hbar^2} = \frac{3n}{2\epsilon_F}$，其中 $k_F$ 是[费米波矢](@entry_id:140713)。因此，TF屏蔽[波矢](@entry_id:178620)可以表示为：
$$ \kappa_{\text{TF}}^2 = \frac{e^2}{\epsilon_0} \frac{m k_F}{\pi^2 \hbar^2} = \frac{e^2}{\epsilon_0} \frac{3n}{2\epsilon_F} $$
一个点电荷 $Q$ 的裸库仑势在傅里叶空间中为 $\phi_{\text{ext}}(q) = Q/(\epsilon_0 q^2)$。经过TF屏蔽后，总[电势](@entry_id:267554)为：
$$ \phi_{\text{tot}}(q) = \frac{\phi_{\text{ext}}(q)}{\epsilon(q)} = \frac{Q/(\epsilon_0 q^2)}{1 + \kappa_{\text{TF}}^2/q^2} = \frac{Q}{\epsilon_0(q^2 + \kappa_{\text{TF}}^2)} $$
将此式[傅里叶逆变换](@entry_id:178300)回[实空间](@entry_id:754128)，或者直接求解线性化的TF方程，可得到著名的**汤川势**（Yukawa potential）形式：
$$ \phi_{\text{tot}}(r) = \frac{Q}{4\pi\epsilon_0 r} \exp(-\kappa_{\text{TF}} r) $$
这表明，在[简并电子气](@entry_id:161524)中，裸露的长程 $1/r$ [库仑势](@entry_id:154276)被屏蔽成一个短程的指数衰减势，其[特征衰减长度](@entry_id:183295)为**[托马斯-费米屏蔽长度](@entry_id:141666)** $\lambda_{\text{TF}} = 1/\kappa_{\text{TF}}$。

### 德拜-休克尔模型与温度效应

与[简并电子气](@entry_id:161524)相对的是经典非[简并系统](@entry_id:203460)，例如高温低密度下的[半导体](@entry_id:141536)载流子或等离子体。在这种情况下，载流子遵循[麦克斯韦-玻尔兹曼统计](@entry_id:746908)。

我们可以沿用 $\kappa^2 = (e^2/\epsilon_0)(\partial n/\partial \mu)$ 的一般形式，但需要计算经典气体的 $\partial n/\partial \mu$。对于[经典理想气体](@entry_id:156161)，密度 $n$ 和化学势 $\mu$ 的关系为 $n \propto \exp(\mu/(k_B T))$。因此，我们立即得到：
$$ \frac{\partial n}{\partial \mu} = \frac{n}{k_B T} $$
代入后得到**[德拜屏蔽](@entry_id:161612)[波矢](@entry_id:178620)**（Debye screening wavevector）$\kappa_D$ 的表达式：
$$ \kappa_D^2 = \frac{n e^2}{\epsilon_0 k_B T} $$
这与TF屏蔽有本质区别：TF屏蔽在零温下是有限的，主要由[费米能](@entry_id:143977)决定，而[德拜屏蔽](@entry_id:161612)反比于温度 $T$。温度越高，热运动越剧烈，电子越不容易被束缚在[势阱](@entry_id:151413)中，屏蔽效应越弱（[屏蔽长度](@entry_id:143797) $\lambda_D = 1/\kappa_D$ 越长）。

TF和[德拜屏蔽](@entry_id:161612)分别代表了量子和经典两种极限情况。一个统一的图像可以通过考虑任意温度和简并度下的[费米-狄拉克统计](@entry_id:140706)来获得。利用[费米-狄拉克积分](@entry_id:193319) $F_\nu(\eta)$（其中 $\eta = \mu/(k_B T)$），可以证明对于抛物线能带，[热力学](@entry_id:141121)导数的一般形式为：
$$ \frac{\partial n}{\partial \mu} = \frac{n}{k_B T} \frac{F_{-1/2}(\mu/(k_B T))}{F_{1/2}(\mu/(k_B T))} $$
于是，屏蔽波矢的普适表达式为：
$$ \kappa^2(T, \mu) = \frac{n e^2}{\epsilon k_B T} \frac{F_{-1/2}(\mu/(k_B T))}{F_{1/2}(\mu/(k_B T))} $$
这个表达式完美地展示了从经典到量子的过渡：
- 在非简并（经典）极限下，$\eta \to -\infty$，[费米-狄拉克积分](@entry_id:193319)之比趋近于1，恢复了[德拜屏蔽](@entry_id:161612)的形式。
- 在强简并（量子）极限下，$\eta \to \infty$，积分之比趋近于 $3/(2\eta) = 3k_B T/(2\mu)$，代入后恰好恢复了TF屏蔽的形式 $\kappa^2 = 3ne^2/(2\epsilon\mu)$（此时 $\mu \approx \epsilon_F$）。

### 超越平均场：[弗里德尔振荡](@entry_id:146905)

TF和德拜模型都基于长波（$q \to 0$）近似，这导致了[屏蔽势](@entry_id:193863)的单调指数衰减。然而，对于简并费米系统，一个更精确的描述揭示了在长距离处存在一种独特的[振荡](@entry_id:267781)行为，即**[弗里德尔振荡](@entry_id:146905)**（Friedel oscillations）。

这种现象的根源在于极化函数 $\Pi(q)$ 在波矢 $q=2k_F$ 处存在一个**非解析点**。对于三维[电子气](@entry_id:140692)，$\Pi(q)$ 的导数在 $q=2k_F$ 处有对数奇异性；对于[二维电子气](@entry_id:146876)，$\Pi(q)$ 本身在该点有一个尖点（cusp）。这个非解析行为源于费米面在零温下的尖锐边界：能量和动量守恒只允许动量转移小于 $2k_F$ 的[费米面](@entry_id:137798)内部的零能电子-空穴对激发。

根据[傅里叶分析](@entry_id:137640)的一般原理，[动量空间](@entry_id:148936)中的奇异性会转化为实空间中的长程代数衰减行为。具体而言，$q=2k_F$ 处的非[解析性](@entry_id:140716)导致了[感应电荷](@entry_id:266454)密度 $\delta n(r)$ 在长距离处出现以 $2k_F$ 为周期的[振荡](@entry_id:267781)，其振幅随距离 $r$ 按[幂律衰减](@entry_id:262227)：
- 在三维（3D）中：$\delta n(r) \sim \frac{\cos(2k_F r)}{r^3}$
- 在二维（2D）中：$\delta n(r) \sim \frac{\cos(2k_F r)}{r^2}$

这些[振荡](@entry_id:267781)意味着屏蔽并非完美，在杂质周围会形成一系列正负交替的[电荷](@entry_id:275494)“晕”。在有限温度下，费米分布函数在[费米能级](@entry_id:143215)附近被热能展宽，这使得 $\Pi(q)$ 在 $q=2k_F$ 处的奇异性被“抹平”。其结果是，[弗里德尔振荡](@entry_id:146905)在超出热长度尺度 $l_T \sim \hbar v_F / (k_B T)$ 后会受到指数抑制。

### 超越RPA：交换、关联与[局域场修正](@entry_id:143541)

至今我们使用的RPA框架，尽管能预测出[弗里德尔振荡](@entry_id:146905)，但其核心假设是电子作为独立粒子对**平均**自洽场作出响应。它忽略了电子之间更复杂的相互作用，即**交换**（exchange）和**关联**（correlation）效应。

RPA在描述短程行为时会遇到严重困难。一个显著的失败是，RPA计算出的电子对关联函数 $g(r)$（表示在原点有一个电子的条件下，在距离 $r$ 处发现另一个电子的概率）在 $r \to 0$ 时会变为负值，这在物理上是荒谬的。这是因为它没有正确地包含[泡利不相容原理](@entry_id:141850)（交换效应）和[库仑排斥](@entry_id:181876)（关联效应）所导致的每个电子周围的“交换-关联空穴”。

为了修正这一缺陷，需要引入**[局域场修正](@entry_id:143541)**（local-field correction）的概念。其物理思想是，作用于某个电子的真实有效场并不仅仅是宏观平均场 $\phi_{\text{tot}}$，还应该包括其周围交换-关联空穴带来的额外修正。形式上，这通过引入一个[局域场](@entry_id:146504)因子 $G(q)$ 来实现，它修正了电子间的有效相互作用。修正后的介电函数变为：
$$ \epsilon(\mathbf{q}) = 1 - \frac{v(\mathbf{q}) \chi_0(\mathbf{q})}{1 + v(\mathbf{q}) G(\mathbf{q}) \chi_0(\mathbf{q})} $$
RPA对应于 $G(q)=0$ 的情况。为了修正RPA在短程的失败，并保证对关联函数等物理量有正确的行为，[局域场](@entry_id:146504)因子 $G(q)$ 在大[波矢](@entry_id:178620)极限 $q \to \infty$ 时必须趋于一个非零常数。

此外，在真实的晶体中，由于周期性[晶格](@entry_id:196752)势的存在，电子气并非完全均匀。一个波矢为 $\mathbf{q}$ 的外部扰动不仅会引起[波矢](@entry_id:178620)为 $\mathbf{q}$ 的响应，还会通过所谓的“乌姆克拉普”（Umklapp）过程，耦合到[波矢](@entry_id:178620)为 $\mathbf{q}+\mathbf{G}$ 的响应上，其中 $\mathbf{G}$ 是[倒格矢](@entry_id:263351)。这意味着介电函数和[极化函数](@entry_id:265572)实际上是定义在倒格子空间中的矩阵，$\epsilon_{\mathbf{G}\mathbf{G}'}(\mathbf{q})$。这种由[晶格](@entry_id:196752)周期性引起的宏观场和微观场之间的差异，是另一种形式的[局域场效应](@entry_id:141628)，对精确计算固体的介电性质至关重要。