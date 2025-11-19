## 引言
材料的光学性质——它如何反射、吸收、透射和[色散](@entry_id:263750)光——是其最基本的物理属性之一，决定了从一块玻璃的透明度到一个半导体器件的效率等一切。然而，理解这些宏观现象需要深入其微观世界，揭示光与物质内部电子、[晶格](@entry_id:196752)及其他[准粒子相互作用](@entry_id:146832)的复杂机制。本文旨在弥合宏观光学现象与微观量子物理之间的知识鸿沟，为读者提供一个全面而深入的视角。

在接下来的章节中，我们将首先在“原理与机制”一章中，系统地建立描述光学响应的理论框架，并剖析其背后的微观物理过程。随后，在“应用与跨学科交叉”一章中，我们将展示这些原理如何在先进[材料表征](@entry_id:161346)、能源转换和[光子](@entry_id:145192)学等前沿领域中发挥关键作用。最后，通过“动手实践”部分的具体案例，您将有机会将理论知识应用于解决实际问题。通过这一学习路径，您将全面掌握材料光学性质的核心概念及其在现代科技中的强大力量。

## 原理与机制

本章旨在深入探讨材料光学性质背后的基本原理与微观机制。我们将从宏观电磁理论出发，建立描述材料光学响应的核心物理量，并揭示它们之间的内在联系。随后，我们将深入微观世界，剖析自由载流子、[晶格振动](@entry_id:140970)、电子的[带间跃迁](@entry_id:138793)以及[激子](@entry_id:147299)效应对材料[光谱](@entry_id:185632)特征的决定性作用。最终，我们将简要介绍如何通过[第一性原理计算](@entry_id:198754)来预测和理解这些复杂的现象。

### 宏观光学[响应函数](@entry_id:142629)

材料对[电磁波](@entry_id:269629)的响应，本质上是材料内部的[电荷](@entry_id:275494)在入射[电磁场](@entry_id:265881)驱动下的响应。在宏观电磁理论中，这种响应被统一封装在一系列[线性响应函数](@entry_id:160418)中。这些函数不仅是理论分析的基石，也是连接实验测量与材料内在物理性质的桥梁。

我们从频率域中的麦克斯韦方程组出发。对于不含自由电荷和电流源的、线性的、各向同性的、非磁性的介质，[方程组](@entry_id:193238)为：
$$
\begin{align*}
\nabla \cdot \mathbf{D}(\omega) = 0 \\
\nabla \cdot \mathbf{B}(\omega) = 0 \\
\nabla \times \mathbf{E}(\omega) = i\omega \mathbf{B}(\omega) \\
\nabla \times \mathbf{H}(\omega) = \mathbf{J}(\omega) - i\omega \mathbf{D}(\omega)
\end{align*}
$$
这里我们采用了 $\exp(-i\omega t)$ 的时间演化约定。$\mathbf{E}$ 和 $\mathbf{H}$ 分别是宏观电场和磁场强度，而 $\mathbf{D}$ 和 $\mathbf{B}$ 是[电位移矢量](@entry_id:197092)和[磁感应强度](@entry_id:144179)，它们包含了介质的响应。$\mathbf{J}$ 是传导电流密度。

为了简化描述，物理学家们将介质中所有由[电场](@entry_id:194326)引起的响应——无论是束缚电子的极化还是自由电子的传导——都归入一个统一的[复介电函数](@entry_id:143480) $\boldsymbol{\epsilon(\omega)}$ 中。考虑一个同时具有束缚[电荷](@entry_id:275494)极化和[自由电荷](@entry_id:264392)传导的材料。其[电位移矢量](@entry_id:197092)可以写为 $\mathbf{D}(\omega) = \epsilon_0 \epsilon_\infty \mathbf{E}(\omega) + \mathbf{P}_{\text{add}}(\omega)$，其中 $\epsilon_\infty$ 是由高频束缚电子贡献的实数[相对介电常数](@entry_id:267815)背景，$\mathbf{P}_{\text{add}}$ 代表其他极化机制。传导电流由欧姆定律的[频域](@entry_id:160070)形式给出：$\mathbf{J}(\omega) = \sigma(\omega) \mathbf{E}(\omega)$，其中 $\boldsymbol{\sigma(\omega)}$ 是复[光学电导率](@entry_id:139437)。

通过将[传导电流](@entry_id:265343)项 $\mathbf{J}$ 在形式上视为一种等效的[极化电流](@entry_id:196744)，我们可以将[安培定律](@entry_id:140092)改写为 $\nabla \times \mathbf{H} = -i\omega \mathbf{D}_{\text{eff}}$ 的形式，其中 $\mathbf{D}_{\text{eff}} = \epsilon_0 \epsilon(\omega) \mathbf{E}(\omega)$。将 $\mathbf{J}$ 和 $\mathbf{D}$ 的本构关系代入原始的[安培定律](@entry_id:140092)，我们得到：
$$
\nabla \times \mathbf{H} = \sigma(\omega)\mathbf{E}(\omega) - i\omega \epsilon_0 \epsilon(\omega) \mathbf{E}(\omega)
$$
为了将所有响应统一到 $\epsilon(\omega)$ 中，我们通常将复电导率 $\sigma(\omega)$ 定义为包含除高频电子响应之外的所有传导和极化过程。这样，总的响应可以写作：
$$
-i\omega \epsilon_0 \epsilon(\omega) \mathbf{E}(\omega) = \sigma(\omega)\mathbf{E}(\omega) - i\omega\epsilon_0\epsilon_\infty\mathbf{E}(\omega)
$$
由此，我们得到了[复介电函数](@entry_id:143480)与复[电导率](@entry_id:137481)之间的基本关系 [@problem_id:2503713]：
$$
\epsilon(\omega) = \epsilon_\infty + \frac{i\sigma(\omega)}{\epsilon_0\omega}
$$
这个关系式至关重要，它表明材料的[介电响应](@entry_id:140146)和[电导](@entry_id:177131)响应在电磁学上是同一物理过程的两个方面。将 $\epsilon(\omega)$ 和 $\sigma(\omega)$ 分解为实部和虚部，$\epsilon(\omega) = \epsilon_1(\omega) + i\epsilon_2(\omega)$ 和 $\sigma(\omega) = \sigma_1(\omega) + i\sigma_2(\omega)$，我们得到：
$$
\epsilon_1(\omega) = \epsilon_\infty - \frac{\sigma_2(\omega)}{\epsilon_0\omega} \quad \text{and} \quad \epsilon_2(\omega) = \frac{\sigma_1(\omega)}{\epsilon_0\omega}
$$
$\epsilon_2(\omega)$ 与[电导率](@entry_id:137481)的实部 $\sigma_1(\omega)$ 直接相关，后者正比于材料在交变[电场](@entry_id:194326)下的能量吸收速率。因此，$\boldsymbol{\epsilon_2(\omega)}$ 是衡量材料光学吸收的关键参数。

另一个核心[光学常数](@entry_id:186307)是**[复折射率](@entry_id:268061)** $\boldsymbol{\tilde{n}(\omega) = n(\omega) + i\kappa(\omega)}$。其中，实部 $\boldsymbol{n(\omega)}$ 是通常意义上的**[折射率](@entry_id:168910)**，它决定了光在介质中的相速度 $v_p = c/n(\omega)$；虚部 $\boldsymbol{\kappa(\omega)}$ 被称为**[消光系数](@entry_id:270201)**，它描述了光波在介质中传播时振幅的衰减。对于非磁性材料，[复介电函数](@entry_id:143480)与[复折射率](@entry_id:268061)通过以下简单关系联系在一起 [@problem_id:2503707]：
$$
\epsilon(\omega) = \tilde{n}(\omega)^2
$$
展开这个关系式，我们得到 $\epsilon_1(\omega) = n(\omega)^2 - \kappa(\omega)^2$ 和 $\epsilon_2(\omega) = 2n(\omega)\kappa(\omega)$。

这些宏观量直接与实验可测量的光学性质——反射、吸收和透射——相关联。
*   **吸收 (Absorption)**：当[平面波](@entry_id:189798)在介质中沿 $z$ 方向传播时，其[电场](@entry_id:194326)振幅按 $\exp(-\frac{\omega\kappa(\omega)z}{c})$ 衰减。光的强度 $I$ 正比于[电场](@entry_id:194326)振幅的平方，因此 $I(z) = I(0)\exp(-\frac{2\omega\kappa(\omega)z}{c})$。根据比尔-朗伯定律 $I(z) = I(0)\exp(-\alpha z)$，我们定义了**[吸收系数](@entry_id:156541)** $\boldsymbol{\alpha(\omega)}$ [@problem_id:2503707]：
    $$
    \alpha(\omega) = \frac{2\omega\kappa(\omega)}{c} = \frac{\omega\epsilon_2(\omega)}{n(\omega)c}
    $$
    吸收系数 $\alpha$ 的单位是长度的倒数，它量化了光强度在穿过单位长度材料后衰减的比例。

*   **反射 (Reflection)**：当光从真空（或空气，[折射率](@entry_id:168910)近似为1）[正入射](@entry_id:260681)到[折射率](@entry_id:168910)为 $\tilde{n}(\omega)$ 的半无限大介质表面时，反射的能量比例由**[反射率](@entry_id:155393)** $\boldsymbol{R(\omega)}$ 给出 [@problem_id:2503713, 2503707]：
    $$
    R(\omega) = \left| \frac{1 - \tilde{n}(\omega)}{1 + \tilde{n}(\omega)} \right|^2 = \frac{(n(\omega)-1)^2 + \kappa(\omega)^2}{(n(\omega)+1)^2 + \kappa(\omega)^2}
    $$
    值得注意的是，即使两种介质的实[折射率](@entry_id:168910) $n(\omega)$ 匹配（例如，一种假设材料的 $n(\omega)=1$），只要[消光系数](@entry_id:270201) $\kappa(\omega)$ 不为零，反射率就不会为零。这是因为吸收（$\kappa \neq 0$）本身就意味着[阻抗失配](@entry_id:261346)，从而导致反射 [@problem_id:2503707]。

*   **[色散](@entry_id:263750) (Dispersion)**：[折射率](@entry_id:168910) $n(\omega)$ 随频率的变化现象被称为**[色散](@entry_id:263750)**。正是[色散](@entry_id:263750)效应使得棱镜能够将白光分解成不同颜色的[光谱](@entry_id:185632)。

### 因果律与 [Kramers-Kronig 关系](@entry_id:140966)

在[线性响应理论](@entry_id:145737)中，一个基本物理原则是**因果律**：响应不能发生在其驱动力之前。对于光学性质而言，这意味着材料在时刻 $t$ 的极化只能依赖于时刻 $t' \le t$ 的[电场](@entry_id:194326)。这一看似简单的物理约束，在数学上对[响应函数](@entry_id:142629) $\epsilon(\omega)$ 的形式施加了极强的限制。

具体而言，因果律要求[复介电函数](@entry_id:143480) $\epsilon(\omega)$（以及其他[线性响应函数](@entry_id:160418)，如 $\sigma(\omega)$ 和 $\chi(\omega)$）在复频率平面的[上半平面](@entry_id:199119)是解析的。这一[解析性](@entry_id:140716)的直接数学推论是，$\epsilon(\omega)$ 的实部 $\epsilon_1(\omega)$ 和虚部 $\epsilon_2(\omega)$ 并非[相互独立](@entry_id:273670)，而是通过一组[积分变换](@entry_id:186209)紧密联系在一起，这组关系被称为 **Kramers-Kronig (KK) 关系** [@problem_id:2503736, 2503693]：
$$
\begin{align*}
\epsilon_1(\omega) - 1 = \frac{2}{\pi} \mathcal{P} \int_{0}^{\infty} \frac{\omega' \epsilon_2(\omega')}{\omega'^2 - \omega^2} d\omega' \\
\epsilon_2(\omega) = -\frac{2\omega}{\pi} \mathcal{P} \int_{0}^{\infty} \frac{\epsilon_1(\omega') - 1}{\omega'^2 - \omega^2} d\omega'
\end{align*}
$$
其中 $\mathcal{P}$ 表示[柯西主值](@entry_id:192761)积分。

KK关系具有深刻的物理和实践意义：
1.  **吸收决定[色散](@entry_id:263750)**：第一条关系式表明，只要我们知道材料在所有频率范围内的吸收谱 $\epsilon_2(\omega)$，我们原则上就可以计算出它在任意频率下的[折射率](@entry_id:168910)（[色散](@entry_id:263750)）谱 $\epsilon_1(\omega)$。反之亦然。这意味着材料的吸收和[色散](@entry_id:263750)是同一物理实在的两个不同侧面，不可分割。

2.  **[反常色散](@entry_id:270636)**：任何吸收峰（$\epsilon_2(\omega)$ 的一个峰值）必然伴随着一个特征性的[色散](@entry_id:263750)结构。在吸收峰的低频侧，[折射率](@entry_id:168910) $n(\omega)$ 随频率增加而增加（$dn/d\omega > 0$），这被称为**[正常色散](@entry_id:175792)**。而在吸收峰的高频侧，[折射率](@entry_id:168910)随频率增加而减小（$dn/d\omega  0$），这被称为**[反常色散](@entry_id:270636)**。因此，[反常色散](@entry_id:270636)是吸收存在的必然标志 [@problem_id:2503736]。

3.  **实践应用与挑战**：在实验上，我们通常更容易精确测量吸收谱（如通过透射测量得到 $\alpha(\omega)$，进而换算得到 $\epsilon_2(\omega)$）。利用KK关系，我们可以从有限频率范围 $[\omega_{\min}, \omega_{\max}]$ 内测得的 $\epsilon_2(\omega)$ 数据推算 $\epsilon_1(\omega)$。然而，这是一个具有挑战性的[逆问题](@entry_id:143129)，因为积分需要覆盖从0到无穷大的整个频率范围。严谨的处理方法要求对测量范围之外的区域进行物理上合理的**外推**（extrapolation），例如，在低频端使用德鲁德或[声子](@entry_id:140728)模型，在高频端使用已知的渐近行为（如 $\epsilon_2 \sim \omega^{-3}$）。此外，测量噪声会通过长程的KK积分核传播并可能被放大，需要通过正则化或基于模型的拟合等方法来抑制 [@problem_id:2503693]。

4.  **[群速度](@entry_id:147686)与因果律**：在[反常色散](@entry_id:270636)区域，[群速度](@entry_id:147686) $v_g = c / (n + \omega \frac{dn}{d\omega})$ 可能变得[超光速](@entry_id:202289)（$v_g > c$）甚至为负。这并不违反因果律。群速度描述的是波包峰值的传播速度，而在强吸收和[色散](@entry_id:263750)的介质中，波包会发生剧烈的“整形”。[超光速](@entry_id:202289)或负的[群速度](@entry_id:147686)是[波包](@entry_id:154698)整形的结果，而信息传播的速度（由[波前](@entry_id:197956)速度定义）永远不会超过真空光速 $c$ [@problem_id:2503736]。利用KK关系，人们甚至可以设计特定的吸收谱（例如，在两个吸收峰之间制造一个窄的透明窗口，即[电磁感应透明](@entry_id:164772) EIT），从而获得极大的[正常色散](@entry_id:175792)（$dn/d\omega \gg 0$），实现“[慢光](@entry_id:144258)”（$v_g \ll c$）。

### 光学响应的微观机制

宏观[响应函数](@entry_id:142629) $\epsilon(\omega)$ 的具体[谱线形状](@entry_id:172308)，源于材料内部不同[准粒子](@entry_id:136584)的激发。根据[激发能](@entry_id:190368)量和类型的不同，我们可以将主要的光学响应机制分为以下几类。

#### 自由载流子：[德鲁德模型](@entry_id:141896)

金属和重[掺杂半导体](@entry_id:145553)中存在大量自由载流子（电子或空穴），它们对中远红外和可见[光谱](@entry_id:185632)区的光学性质起主导作用。**[德鲁德模型](@entry_id:141896) (Drude model)** 是描述这种响应的经典模型 [@problem_id:2503657]。

该模型将自由载流子视为在[电场](@entry_id:194326)驱动下运动的经典粒子，并受到一个与速度成正比的[阻尼力](@entry_id:265706)（代表与[晶格](@entry_id:196752)、缺陷等的碰撞）。从[牛顿运动定律](@entry_id:163846)出发，可以推导出[复介电函数](@entry_id:143480)的形式：
$$
\epsilon(\omega) = \epsilon_{\infty} - \frac{\omega_p^2}{\omega^2 + \gamma^2} + i\frac{\omega_p^2\gamma}{\omega(\omega^2 + \gamma^2)}
$$
其中，$\epsilon_\infty$ 是由原子实（束缚电子）贡献的高频介电背景；$\gamma$ 是载流子的动量弛豫速率，代表了碰撞的频繁程度。最重要的参数是**等离激元频率 (plasma frequency)** $\boldsymbol{\omega_p}$：
$$
\omega_p^2 = \frac{ne^2}{\epsilon_0 m^*}
$$
这里 $n$ 是[载流子浓度](@entry_id:143028)，$e$ 是电子[电荷](@entry_id:275494)，$m^*$ 是载流子的有效质量。$\omega_p$ 是描述载流子[集体[振](@entry_id:158973)荡](@entry_id:267781)行为的特征频率。

[德鲁德模型](@entry_id:141896)的介电函数呈现出典型的行为：
-   在低频区（$\omega \ll \omega_p$），$\epsilon_1(\omega)$ 是一个大的负数。负的 $\epsilon_1$ 意味着[复折射率](@entry_id:268061) $\tilde{n}$ 主要是虚数，即 $\tilde{n} \approx i\kappa$。这导致反射率 $R(\omega)$ 接近1。这就是金属呈现高反射率的原因。
-   随着频率升高，当 $\omega$ 接近某个特征频率时，$\epsilon_1(\omega)$ 从负值穿越零点变为正值。这个零点标志着材料从“类金属”行为（反射）向“类介电”行为（透射）的转变。这个转变区域被称为**[等离激元](@entry_id:146184)边 (plasma edge)** 或**反射边 (reflectance edge)**。
-   在弱阻尼极限下（$\gamma \ll \omega$），$\epsilon_1(\omega) = \epsilon_\infty - \omega_p^2/\omega^2$。令 $\epsilon_1(\omega) = 0$ 求解，我们得到反射边出现的频率，即**屏蔽等离激元频率**：
    $$
    \omega_{\text{edge}} \approx \frac{\omega_p}{\sqrt{\epsilon_\infty}}
    $$
    由于 $\omega_p \propto \sqrt{n/m^*}$，所以可以通过改变[半导体](@entry_id:141536)的掺杂浓度 $n$ 来调控其反射边的位置。例如，一个载流子浓度为 $5.0 \times 10^{20} \text{ cm}^{-3}$、有效质量为 $0.20 m_e$、介电背景为 $\epsilon_\infty=11$ 的重[掺杂半导体](@entry_id:145553)，其反射边能量经计算约为 $0.56 \text{ eV}$，位于红外波段 [@problem_id:2503657]。

#### 晶格振动：极性晶体中的[声子](@entry_id:140728)

在[离子晶体](@entry_id:138598)（如 NaCl）中，正负离子构成两个子[晶格](@entry_id:196752)。当红外光的[电场](@entry_id:194326)驱动这两个子[晶格](@entry_id:196752)发生相对位移时，会产生强烈的极化，并与特定频率的[晶格振动](@entry_id:140970)——**[光学声子](@entry_id:136993)**——发生共振吸收。

这种响应可以用**[洛伦兹振子模型](@entry_id:274156) (Lorentz oscillator model)** 来描述 [@problem_id:2503706]。该模型将离子对的相对运动视为一个受[电场](@entry_id:194326)驱动的、有阻尼的谐振子。其[介电函数](@entry_id:136859)（在无阻尼极限下）具有以下形式：
$$
\epsilon(\omega) = \epsilon_\infty + \frac{(\epsilon(0) - \epsilon_\infty)\omega_{\mathrm{TO}}^2}{\omega_{\mathrm{TO}}^2 - \omega^2}
$$
其中，$\epsilon(0)$ 是静态[介电常数](@entry_id:146714)，$\boldsymbol{\omega_{\mathrm{TO}}}$ 是**横向光学 (Transverse Optical, TO) [声子频率](@entry_id:753407)**，即[晶格振动](@entry_id:140970)的固有[共振频率](@entry_id:265742)。

对于纵向的晶格振动，其产生的极化会诱导一个宏观的退[极化场](@entry_id:197617)，这个场提供了额外的恢复力，使得[纵向振动](@entry_id:176640)的频率高于横向[振动](@entry_id:267781)。这个频率被称为**纵向光学 (Longitudinal Optical, LO) [声子频率](@entry_id:753407)** $\boldsymbol{\omega_{\mathrm{LO}}}$。它对应于[介电函数](@entry_id:136859)为零的频率，即 $\epsilon(\omega_{\mathrm{LO}}) = 0$。将此条件代入[洛伦兹模型](@entry_id:144803)，可以推导出著名的 **Lyddane-Sachs-Teller (LST) 关系**：
$$
\frac{\epsilon(0)}{\epsilon_\infty} = \left(\frac{\omega_{\mathrm{LO}}}{\omega_{\mathrm{TO}}}\right)^2
$$
LST 关系揭示了[晶格](@entry_id:196752)的宏观介电性质（$\epsilon(0), \epsilon_\infty$）与微观动力学性质（$\omega_{\mathrm{TO}}, \omega_{\mathrm{LO}}$）之间的深刻联系。

在 $\omega_{\mathrm{TO}}$ 和 $\omega_{\mathrm{LO}}$ 之间的频率范围内，$\epsilon(\omega)$ 为负值。与[德鲁德模型](@entry_id:141896)类似，这导致了近乎100%的反射率。这个高反射带被称为**[剩余射线带](@entry_id:147008) (Reststrahlen band)**，是极性晶体红外[光谱](@entry_id:185632)的标志性特征 [@problem_id:2503706]。此外，LST关系也为理解[铁电相变](@entry_id:185454)提供了线索：在位移型[铁电体](@entry_id:138549)中，当材料接近[相变](@entry_id:147324)温度时，某个 TO [声子模式](@entry_id:201212)会“软化”（$\omega_{\mathrm{TO}} \to 0$），根据 LST 关系，这直接导致了静态[介电常数](@entry_id:146714) $\epsilon(0)$ 的发散，这正是铁电性的标志。

#### [带间跃迁](@entry_id:138793)：[半导体](@entry_id:141536)与绝缘体

在[半导体](@entry_id:141536)和绝缘体中，当[光子能量](@entry_id:139314) $\hbar\omega$ 大于或等于其**[带隙](@entry_id:191975)能量 ($E_g$)** 时，[光子](@entry_id:145192)可以被吸收，将一个电子从满的价带激发到空的[导带](@entry_id:159736)。这个过程称为**[带间跃迁](@entry_id:138793) (interband transition)**，它是这些材料在可见光和紫外波段吸收的主要来源。

吸收系数 $\alpha(\omega)$ 的[谱线形状](@entry_id:172308)由两个关键因素决定：量子力学跃迁概率和[能量-动量守恒](@entry_id:194427)。根据[费米黄金定则](@entry_id:146239)，跃迁速率正比于**动量[矩阵元](@entry_id:186505)**的平方 $|\mathbf{p}_{cv}|^2$ 和**[联合态密度](@entry_id:143002) (Joint Density of States, JDOS)** $\rho_{cv}(\hbar\omega)$ [@problem_id:2503772]。JDOS 描述了在价带和[导带](@entry_id:159736)之间，能量差恰好为 $\hbar\omega$ 的电子态对的数量。

根据晶体的[能带结构](@entry_id:139379)，[带间跃迁](@entry_id:138793)分为两类：
*   **直接跃迁 (Direct Transition)**：如果[价带](@entry_id:158227)顶和导带底位于布里渊区中相同的晶体动量 $\mathbf{k}$ 处（即“直接带隙”），电子可以直接吸收一个[光子](@entry_id:145192)完成跃迁（因为[光子](@entry_id:145192)的动量与[晶体动量](@entry_id:136369)相比几乎为零）。对于三维抛物线形能带，JDOS 的能量依赖关系为 $\rho_{cv}(\hbar\omega) \propto \sqrt{\hbar\omega - E_g}$。因此，对于直接[允许跃迁](@entry_id:160018)，吸收边附近的[吸收系数](@entry_id:156541)满足：
    $$
    \alpha(\omega) \propto (\hbar\omega - E_g)^{1/2}
    $$
    这导致吸收谱在[带隙](@entry_id:191975)能量处有一个陡峭的上升沿。

*   **间接跃迁 (Indirect Transition)**：如果[价带](@entry_id:158227)顶和导带底位于不同的 $\mathbf{k}$ 点（即“间接带隙”），[电子跃迁](@entry_id:152949)需要同时吸收（或发射）一个[声子](@entry_id:140728)来补偿动量差。这是一个二阶过程，其概率远低于直接跃迁。能量和动量必须同时守恒。这种过程的吸收谱形状更为平缓，对于三维抛物线形能带，其特征依赖关系为：
    $$
    \alpha(\omega) \propto (\hbar\omega - E_g^{\mathrm{ind}} \pm \hbar\Omega)^2
    $$
    其中 $E_g^{\mathrm{ind}}$ 是间接带隙能量，$\hbar\Omega$ 是参与过程的[声子](@entry_id:140728)能量。正负号分别对应[声子](@entry_id:140728)的发射和吸收。

#### 激子效应：电子-空穴的相互作用

在描述[带间跃迁](@entry_id:138793)时，我们通常假设被激发的电子和留在[价带](@entry_id:158227)的空穴是[相互独立](@entry_id:273670)的。然而，由于库仑相互作用，带负电的电子和带正电的空穴会相互吸引，形成一个束缚对，这个[准粒子](@entry_id:136584)被称为**激子 (exciton)**。[激子](@entry_id:147299)效应深刻地改变了[半导体](@entry_id:141536)在[带隙](@entry_id:191975)附近的吸收光谱 [@problem_id:2503770]。

在典型的[半导体](@entry_id:141536)中，这种束缚态是**莫特-瓦尼尔激子 (Mott-Wannier exciton)**，其束缚较弱，电子和空穴的[相对运动](@entry_id:169798)可以类比于一个氢原子模型。[电子-空穴对](@entry_id:142506)的库仑吸引被[晶格](@entry_id:196752)的介电背景 $\epsilon_b$ 所屏蔽。[激子](@entry_id:147299)的束缚能 $E_B$ 和[玻尔半径](@entry_id:154675) $a_B$ 分别为：
$$
E_B \propto \frac{\mu}{\epsilon_b^2}, \quad a_B \propto \frac{\epsilon_b}{\mu}
$$
其中 $\mu$ 是电子-空穴的折合[有效质量](@entry_id:142879)。

[激子](@entry_id:147299)的[光谱](@entry_id:185632)特征包括：
1.  **[激子](@entry_id:147299)吸收峰**：激子的形成使得吸收可以在低于[带隙](@entry_id:191975)能量处发生。在吸收谱 $\epsilon_2(\omega)$ 中，会出现一系列分立的、类似[洛伦兹线型](@entry_id:165845)的吸收峰，其能量位于 $E_n = E_g - E_B/n^2$（$n=1, 2, ...$）。最强的吸收峰对应于[基态](@entry_id:150928)激子（$n=1$），位于 $E_g - E_B$。

2.  **振子强度与屏蔽**：激子吸收的强度（[振子强度](@entry_id:147221)）正比于电子和空穴在同一点被找到的概率，即 $|\psi_{1s}(0)|^2 \propto 1/a_B^3$。因此，振子强度与背景[介电常数](@entry_id:146714)的关系为 $\propto \epsilon_b^{-3}$。这意味着，在[介电屏蔽](@entry_id:266074)更强的材料中，[激子](@entry_id:147299)束缚更弱（$E_B$ 更小），空间尺寸更大（$a_B$ 更大），吸收峰也更弱 [@problem_id:2503770]。

3.  **反射谱特征**：由于[激子](@entry_id:147299)吸收峰非常尖锐，根据 KK 关系，它会在[折射率](@entry_id:168910) $n(\omega)$ 中引起一个强烈的、[反常色散](@entry_id:270636)为主的“类导数”结构。这导致在反射谱 $R(\omega)$ 中也出现一个复杂的、非对称的特征，而不是一个简单的峰或谷 [@problem_id:2503770]。

4.  **索末菲增强**：即使光子能量足以产生自由的电子-空穴对（$\hbar\omega > E_g$），它们之间的库仑吸引仍然存在，这会增强它们在近距离相遇的概率，从而使得带边以上的连续吸收谱比无相互作用模型预测的要强。这种效应被称为**索末菲增强 (Sommerfeld enhancement)** [@problem_id:2503770]。

#### 序乱效应：[乌尔巴赫尾](@entry_id:269771)

在真实的晶体中，不可避免地存在各种缺陷（[静态无序](@entry_id:144184)）以及[晶格](@entry_id:196752)热[振动](@entry_id:267781)（[动态无序](@entry_id:187807)）。这些无序会造成局域势的涨落，使得能带边不再是一个清晰的界限，而是在空间和时间上发生波动。

这种效应在光学吸收谱上的直接体现是**[乌尔巴赫尾](@entry_id:269771) (Urbach tail)** [@problem_id:2503673]。它指的是在[带隙](@entry_id:191975)能量 $E_g$ 以下，吸收系数并不立即降为零，而是呈现出一个指数衰减的吸收边：
$$
\alpha(\hbar\omega) \propto \exp\left(\frac{\hbar\omega - E_0}{E_U}\right)
$$
其中，$E_U$ 是**[乌尔巴赫能量](@entry_id:267177)**，它表征了[吸收边](@entry_id:274704)的展宽程度，反映了系统中无序的强度。

[乌尔巴赫尾](@entry_id:269771)的指数形式源于统计物理中的[大偏差理论](@entry_id:273365)。吸收一个能量为 $\hbar\omega  E_g$ 的[光子](@entry_id:145192)，需要[晶格](@entry_id:196752)（通过多[声子](@entry_id:140728)过程）或静态缺陷势提供一个能量为 $\delta E = E_g - \hbar\omega$ 的涨落。提供这样一个大的、罕见的[能量涨落](@entry_id:148029)的概率是指数形式的。[乌尔巴赫能量](@entry_id:267177) $E_U$ 随温度升高而增加，因为它反映了热[声子](@entry_id:140728)振幅的增加。在 $T \to 0$ 时，它趋于一个由[静态无序](@entry_id:144184)决定的有限值。

### 第一性原理计算方法

上述模型（德鲁德、洛伦兹等）为理解光学性质提供了清晰的物理图像，但它们是唯象的，依赖于实验输入的参数。现代[材料科学](@entry_id:152226)追求从更基本的层面——仅基于材料的原子构成——来预测其光学性质。这通常通过**[第一性原理计算](@entry_id:198754)**来实现。

计算光学谱的标准现代工作流程是所谓的 **[GW-BSE](@entry_id:142900) 方法** [@problem_id:2503777]，它建立在密度泛函理论 (DFT) 的基础之上，并系统地包含了[多体相互作用](@entry_id:751663)效应：

1.  **[基态](@entry_id:150928)计算**：首先，通过 DFT 计算材料的电子基态，得到 Kohn-Sham 轨函数和能级。然而，DFT 的能级（[本征值](@entry_id:154894)）通常会严重低估[半导体](@entry_id:141536)的[带隙](@entry_id:191975)（即“[带隙问题](@entry_id:143831)”）。

2.  **[准粒子](@entry_id:136584)修正 (GW)**：为了获得准确的单粒子激发能谱（即[准粒子](@entry_id:136584)能谱），需要超越 DFT。**GW 近似**是一种计算[电子自能](@entry_id:148523) $\Sigma$ 的方法，它可以修正 DFT 能级，得到准确的[准粒子](@entry_id:136584)[带隙](@entry_id:191975)和[能带结构](@entry_id:139379)。

3.  **[激子](@entry_id:147299)效应 (BSE)**：获得了准确的[准粒子](@entry_id:136584)[带隙](@entry_id:191975)后，下一步是计入电子-空穴相互作用。通过求解**贝特-萨尔佩特方程 (Bethe-Salpeter Equation, BSE)**，可以得到包含相互作用的、真实的双粒子[激发态](@entry_id:261453)——[激子](@entry_id:147299)的能谱和[波函数](@entry_id:147440)。BSE 的核心是一个描述电子-空穴有效相互作用的积分核，它包含了一个有吸[引力](@entry_id:175476)的、被[静态屏蔽](@entry_id:262850)的直接库仑项和一个有排斥力的、裸的交换项。

4.  **计算吸收谱**：最后，从 BSE 的解（激子能量和[振子强度](@entry_id:147221)）出发，就可以构建出宏观介电函数 $\epsilon(\omega)$，从而得到理论预测的吸收谱。

[GW-BSE](@entry_id:142900) 方法能够高精度地预测材料的[光谱](@entry_id:185632)，因为它在统一的量子力学框架内，系统地处理了[带间跃迁](@entry_id:138793)、静态和[动态屏蔽](@entry_id:267421)以及激子束缚等所有关键的微观物理过程。