## 引言
在[计算材料科学](@entry_id:145245)领域，理解材料的电子结构是预测和设计其功能的基石。然而，第一性原理计算产生的原始数据（如复杂的[能带图](@entry_id:272375)）往往难以直观地与材料的宏观性质建立联系。电子[态密度(DOS)](@entry_id:136965)及其投影形式(PDOS)正是为了解决这一问题而生的关键分析工具，它们将抽象的[量子态](@entry_id:146142)信息转化为化学直观且与实验直接相关的物理量，弥合了微观理论与宏观现象之间的鸿沟。

本文旨在为读者提供一个关于[态密度](@entry_id:147894)和[投影态密度](@entry_id:260980)的全面而深入的指南。通过学习本文，您将能够掌握从理论到实践的全过程。

在**“原理与机制”**一章中，我们将从固态物理的第一性原理出发，系统阐述[态密度](@entry_id:147894)的定义、归一化方式，并深入探讨[投影态密度](@entry_id:260980)(PDOS)和[局域态密度(LDOS)](@entry_id:141451)的物理意义。我们还将讨论数值计算中的关键技术，如[k点取样](@entry_id:177715)和展宽方案，并触及超越单粒子图像的[多体效应](@entry_id:173569)。

接着，在**“应用与跨学科连接”**一章中，我们将展示这些概念在解决实际问题中的强大威力。您将看到[态密度](@entry_id:147894)如何被用来解释材料的电子、磁学和[热力学性质](@entry_id:146047)，分析化学键合与催化活性，以及研究[半导体缺陷](@entry_id:147796)、表面和界面等复杂体系。

最后，**“动手实践”**部分将理论知识付诸实践，通过一系列精心设计的计算问题，引导您亲手计算和分析不同体系的[态密度](@entry_id:147894)，从而巩固理论理解并提升实际科研技能。

## 原理与机制

### 态密度的基本定义

在固态物理中，**[电子态密度](@entry_id:182354) (Density of States, DOS)** 是一个核心概念，它描述了在给定能量区间内，单位能量、单位体积（或单位原胞）内[量子态](@entry_id:146142)的数量。理解[态密度](@entry_id:147894)是掌握材料电子、光学、磁学和热力学性质的关键。

#### 从[量子态](@entry_id:146142)计数到[态密度](@entry_id:147894)积分

对于一个宏观体积为 $V$ 的周期性晶体，在[玻恩-冯·卡门](@entry_id:201892)周期性边界条件下，电子的波矢 $\mathbf{k}$ 是量子化的。在倒易空间中，每个允许的 $\mathbf{k}$ 点占据的体积为 $\frac{(2\pi)^3}{V}$。这意味着在[倒易空间](@entry_id:754151)中一个无穷小的[体积元](@entry_id:267802) $d^3k$ 内，存在的[量子态](@entry_id:146142)数量为 $\frac{V}{(2\pi)^3}d^3k$。在[热力学极限](@entry_id:143061)下 ($V \to \infty$)，$\mathbf{k}$ 点的[分布](@entry_id:182848)趋于连续，离散求和可以被积分所替代：

$$
\sum_{\mathbf{k}} \to \frac{V}{(2\pi)^3} \int d^3k
$$

这一转换是从微观离散态过渡到宏观连续谱的桥梁 ()。根据布洛赫定理，晶体中的单电子本征态由能带指数 $n$ 和[波矢](@entry_id:178620) $\mathbf{k}$ 共同标记，其能量为 $\varepsilon_{n\mathbf{k}}$。[态密度](@entry_id:147894)的形式化定义 $D(E)$ 就是对所有能量为 $E$ 的态进行计数。这可以通过狄拉克 $\delta$ 函数来实现，它在 $E = \varepsilon_{n\mathbf{k}}$ 时筛选出相应的态。

因此，整个晶体的总[态密度](@entry_id:147894) $D_{\text{total}}(E)$ 是对所有能带和布里渊区 (Brillouin Zone, BZ) 内所有 $\mathbf{k}$ 点的贡献求和（积分）：

$$
D_{\text{total}}(E) = \sum_{n} \sum_{\mathbf{k}} \delta(E - \varepsilon_{n\mathbf{k}}) \to \sum_{n} \frac{V}{(2\pi)^3} \int_{\text{BZ}} d^3k \, \delta(E - \varepsilon_{n\mathbf{k}})
$$

在实际应用中，我们通常更关心与材料内禀属性相关的、不依赖于样品大小的物理量。因此，态密度通常被归一化到单位体积或单位[原胞](@entry_id:159354)。

**[态密度](@entry_id:147894) (单位体积)**, $D_{\text{vol}}(E)$，通过将总[态密度](@entry_id:147894)除以晶体体积 $V$ 得到：

$$
D_{\text{vol}}(E) = \frac{D_{\text{total}}(E)}{V} = \sum_{n} \int_{\text{BZ}} \frac{d^3k}{(2\pi)^3} \, \delta(E - \varepsilon_{n\mathbf{k}})
$$

这里的[积分因子](@entry_id:177812) $(2\pi)^{-3}$ 源于周期性边界条件下倒易空间中[量子态](@entry_id:146142)的密度 ()。

**态密度 (单位原胞)**, $D_{\text{uc}}(E)$，则是通过将总[态密度](@entry_id:147894)除以晶体中[原胞](@entry_id:159354)的总数 $N_{\text{uc}} = V/V_{\text{uc}}$ (其中 $V_{\text{uc}}$ 是[原胞](@entry_id:159354)体积) 得到。利用[布里渊区](@entry_id:142395)体积 $\Omega_{\text{BZ}} = (2\pi)^3 / V_{\text{uc}}$ 的关系，我们可以得到一个优雅的表达式 ()：

$$
D_{\text{uc}}(E) = \frac{D_{\text{total}}(E)}{N_{\text{uc}}} = V_{\text{uc}} \left( \sum_{n} \int_{\text{BZ}} \frac{d^3k}{(2\pi)^3} \, \delta(E - \varepsilon_{n\mathbf{k}}) \right) = \sum_{n} \int_{\text{BZ}} \frac{d^3k}{\Omega_{\text{BZ}}} \, \delta(E - \varepsilon_{n\mathbf{k}})
$$

这种归一化方式非常有用，因为它揭示了一个基本事实：对单个能带 $n$ 的态密度在全能量范围[内积](@entry_id:158127)分，得到的结果恰好为 1。这意味着每个[原胞](@entry_id:159354)、每个能带恰好包含一个（单自旋通道的）[量子态](@entry_id:146142)。

$$
\int_{-\infty}^{\infty} dE \left( \int_{\text{BZ}} \frac{d^3k}{\Omega_{\text{BZ}}} \, \delta(E - \varepsilon_{n\mathbf{k}}) \right) = \int_{\text{BZ}} \frac{d^3k}{\Omega_{\text{BZ}}} = \frac{\Omega_{\text{BZ}}}{\Omega_{\text{BZ}}} = 1
$$

在不引起混淆的情况下，我们后续将使用 $D(E)$ 来泛指[态密度](@entry_id:147894)，具体归一化方式视上下文而定。此外，若无特殊说明，表达式通常指单个自旋通道；对于非[磁性材料](@entry_id:137953)，总态密度需要乘以自旋简并因子 $g_s=2$。

### 态密度的分解：[投影态密度](@entry_id:260980)与局域态密度

总态密度 $D(E)$ 提供了关于[能量本征值](@entry_id:144381)[分布](@entry_id:182848)的全局信息，但它无法告诉我们这些态的“[化学成分](@entry_id:138867)”或[空间分布](@entry_id:188271)。为了获得更深入的洞见，我们引入了两种分解态密度的方式：[投影态密度](@entry_id:260980) (Projected Density of States, PDOS) 和局域态密度 (Local Density of States, [LDOS](@entry_id:136852))。

#### [投影态密度](@entry_id:260980) (PDOS)

PDOS 回答了这样一个问题：“在能量 $E$ 处，有多少态具有特定原子或[轨道](@entry_id:137151)的属性？”这个概念通过将[布洛赫态](@entry_id:147552) $\lvert \psi_{n\mathbf{k}} \rangle$ 投影到一个预先选定的局域化[原子轨道](@entry_id:140819)[基矢](@entry_id:199546)集上来实现。

形式上，我们定义一个投影算符 $P_{\alpha}$，它将任意态投影到由[轨道](@entry_id:137151) $\alpha$（例如，某个原子的 $d_{z^2}$ [轨道](@entry_id:137151)）所张成的[子空间](@entry_id:150286)中。对于一个归一化的[布洛赫态](@entry_id:147552) $\lvert \psi_{n\mathbf{k}} \rangle$，其属于[子空间](@entry_id:150286) $\alpha$ 的权重由[期望值](@entry_id:153208) $w_{n\mathbf{k}}^{(\alpha)} = \langle \psi_{n\mathbf{k}} \rvert P_{\alpha} \rvert \psi_{n\mathbf{k}} \rangle$ 给出 ()。这个权重是一个 $0$ 到 $1$ 之间的实数，量化了[轨道](@entry_id:137151) $\alpha$ 对该[布洛赫态](@entry_id:147552)的贡献程度。

将这个权重因子引入态密度的定义中，我们便得到了投影到[子空间](@entry_id:150286) $\alpha$ 的[态密度](@entry_id:147894)，即 PDOS（以单位体积为例）：

$$
D_{\alpha}(E) = \sum_{n} \int_{\text{BZ}} \frac{d^3k}{(2\pi)^3} \, \langle \psi_{n\mathbf{k}} \rvert P_{\alpha} \rvert \psi_{n\mathbf{k}} \rangle \, \delta(E - \varepsilon_{n\mathbf{k}})
$$

PDOS 的一个至关重要的性质是其**求和规则**。如果所选的投影算符集合 $\lbrace P_{\alpha} \rbrace$ 是完备的，即它们满足单位分解 $\sum_{\alpha} P_{\alpha} = I$（其中 $I$ 是恒等算符），那么将所有 PDOS 分量相加，必然能恢复出总态密度 (, )：

$$
\sum_{\alpha} D_{\alpha}(E) = \sum_{\alpha} \sum_{n} \int_{\text{BZ}} \frac{d^3k}{(2\pi)^3} \langle \psi_{n\mathbf{k}} \rvert P_{\alpha} \rvert \psi_{n\mathbf{k}} \rangle \delta(E - \varepsilon_{n\mathbf{k}}) = \sum_{n} \int_{\text{BZ}} \frac{d^3k}{(2\pi)^3} \langle \psi_{n\mathbf{k}} \rvert \left( \sum_{\alpha} P_{\alpha} \right) \rvert \psi_{n\mathbf{k}} \rangle \delta(E - \varepsilon_{n\mathbf{k}}) = D(E)
$$

需要强调的是，PDOS 的具体数值依赖于投影[基矢](@entry_id:199546)的选择，例如[原子轨道](@entry_id:140819)的类型和[截断半径](@entry_id:136708)。因此，它是一个依赖于[基组](@entry_id:160309)的量，主要用于定性分析和趋势比较，而非一个严格的物理可观测量。

#### [局域态密度](@entry_id:136852) (LDOS)

与 PDOS 在[轨道空间](@entry_id:148658)分解 DOS 不同，[局域态密度](@entry_id:136852) ([LDOS](@entry_id:136852)) 在真[实空间](@entry_id:754128)中分解 DOS。[LDOS](@entry_id:136852), $n(\mathbf{r}, E)$，定义为在空间中特定一点 $\mathbf{r}$ 处、单位能量的[电子态密度](@entry_id:182354)：

$$
n(\mathbf{r}, E) = \sum_{n,\mathbf{k}} |\psi_{n\mathbf{k}}(\mathbf{r})|^2 \delta(E - \varepsilon_{n\mathbf{k}})
$$

其中 $|\psi_{n\mathbf{k}}(\mathbf{r})|^2$ 是电子在 $\mathbf{r}$ 点被发现的概率密度。与 PDOS 不同，LDOS 是一个不依赖于任何投影[基组](@entry_id:160309)的、物理上明确定义的量。将 LDOS 在整个空间中积分，即可恢复总态密度：$\int_V n(\mathbf{r}, E) d^3r = D_{\text{total}}(E)$。

[LDOS](@entry_id:136852) 不仅是一个理论构想，它与现代实验技术紧密相连。在**扫描隧道显微镜 (Scanning Tunneling Microscopy, STM)** 和**[扫描隧道谱](@entry_id:157738) (Scanning Tunneling Spectroscopy, STS)** 中，测量的隧道电流直接与样品的电子结构相关。根据 **Tersoff-Hamann 近似**，在低温、小偏压和 $s$ 波形的针尖等理想条件下，[微分](@entry_id:158718)[电导](@entry_id:177131) $\mathrm{d}I/\mathrm{d}V$ 与针尖下方样品表面的 LDOS 成正比 ()：

$$
\frac{\mathrm{d}I}{\mathrm{d}V} \propto n(\mathbf{r}_{\text{tip}}, E_F + eV)
$$

这里 $\mathbf{r}_{\text{tip}}$ 是针尖的位置，$E_F$ 是费米能级，$V$ 是施加的偏压。这意味着通过测量不同偏压下的 $\mathrm{d}I/\mathrm{d}V$ 谱，STS 能够直接“看到”样品表面的局域态密度。LDOS 的空间变化直接反映了电子[波函数](@entry_id:147440) $|\psi_{n\mathbf{k}}(\mathbf{r})|^2$ 的空间形态，因此它包含了丰富的[轨道对称性](@entry_id:142623)信息，例如[波函数](@entry_id:147440)的节面会表现为 LDOS 为零的区域。当超出 Tersoff-Hamann 近似的范畴时（例如，使用非 $s$ 波针尖或施加较大偏压），$\mathrm{d}I/\mathrm{d}V$ 将不再简单地正比于 LDOS，而是反映了针尖和样品态密度、以及能量和对称性依赖的隧道矩阵元的复杂卷积 ()。

### DOS 在决定[材料性质](@entry_id:146723)中的作用

态密度是连接微观[电子结构](@entry_id:145158)和宏观[材料性质](@entry_id:146723)的核心纽带。

#### [电子性质](@entry_id:748898)：[金属与绝缘体](@entry_id:148635)

在绝对[零度](@entry_id:156285) ($T=0$)，电子会填充从最低能量开始的所有可用[量子态](@entry_id:146142)，直到所有电子都被容纳。最后一个被占据的能级被称为**[费米能级](@entry_id:143215)** ($E_F$)。我们可以通过**累积态密度** $N(E)$ 来形式化地确定[费米能级](@entry_id:143215)，它表示能量低于 $E$ 的总态数：

$$
N(E) = \int_{-\infty}^{E} D(E') \, dE'
$$

如果一个[原胞](@entry_id:159354)内有 $N_e$ 个电子，那么在 $T=0$ 时，[费米能级](@entry_id:143215) $E_F$ 由以下条件确定 ()：

$$
N(E_F) = N_e
$$

材料是金属还是绝缘体，完全取决于费米能级处的态密度 $D(E_F)$：
- **金属 (Metal)**：[费米能级](@entry_id:143215)穿过一个或多个能带，导致 $D(E_F) > 0$。这意味着在费米能级附近有大量可用的、未被填满的电子态。在外加[电场](@entry_id:194326)下，电子可以轻易地被激发到这些邻近的空态中，从而形成电流。在金属中，由于 $N(E)$ 在 $E_F$ 附近是严格单调递增的，[费米能级](@entry_id:143215)由 $N(E_F) = N_e$ 唯一确定。
- **绝缘体 (Insulator) 或[半导体](@entry_id:141536) (Semiconductor)**：[费米能级](@entry_id:143215)位于一个**[带隙](@entry_id:191975) (band gap)** 之中，此处 $D(E)=0$。价带（低于[带隙](@entry_id:191975)的能带）被完全填满，而导带（高于[带隙](@entry_id:191975)的能带）完全空着。由于没有邻近的态可供电子跃迁，需要一个至少等于[带隙](@entry_id:191975)能量的激发才能产生导电电子。在绝缘体中，由于 $N(E)$ 在整个[带隙](@entry_id:191975)内是一个等于 $N_e$ 的平台区，[费米能级](@entry_id:143215)的具体位置在[带隙](@entry_id:191975)内是不确定的 ()。

利用累积[投影态密度](@entry_id:260980) $N_{\alpha}(E) = \int_{-\infty}^{E} D_{\alpha}(E') dE'$，我们还可以进一步分析被占据电子态的[化学成分](@entry_id:138867)。例如，通过计算 $N_{\alpha}(E_F)$，我们可以得知在[费米能级](@entry_id:143215)以下的占据态中，[轨道](@entry_id:137151) $\alpha$ 总共贡献了多少电子，这对于理解化学成键和反应活性至关重要 ()。

#### DOS 的结构特征：Van Hove [奇点](@entry_id:137764)

[态密度](@entry_id:147894)函数通常不是平滑的，它在某些能量点上会呈现尖峰或不连续的导数，这些特征被称为 **van Hove [奇点](@entry_id:137764) (van Hove singularities)**。它们源于能带结构中的**[临界点](@entry_id:144653)**，即 $\mathbf{k}$ 空间中能量对波矢的梯度为零的点（$\nabla_{\mathbf{k}} E(\mathbf{k}) = 0$）。

要理解其起源，我们可以将[态密度](@entry_id:147894)的定义改写为在[等能面](@entry_id:262911)上的积分：

$$
D(E) \propto \int_{S_E} \frac{dS_k}{|\nabla_{\mathbf{k}} E(\mathbf{k})|}
$$

其中 $S_E$ 是能量为 $E$ 的[等能面](@entry_id:262911)。当能量 $E$ 接近某个[临界点](@entry_id:144653)能量 $E_c$ 时，分母 $|\nabla_{\mathbf{k}} E(\mathbf{k})|$ 在[临界点](@entry_id:144653) $\mathbf{k}_c$ 处趋于零，这可能导致积分发散，从而在 $D(E)$ 中产生[奇点](@entry_id:137764)。

[奇点](@entry_id:137764)的具体形式与维度和[临界点](@entry_id:144653)的类型（极小值、极大值或[鞍点](@entry_id:142576)）密切相关 ()：
- 在**二维 (2D)** 系统中：
    - 抛物线型的能带[极值](@entry_id:145933)点（极大/小值）会导致 $D(E)$ 出现一个**阶跃不连续**。例如，对于 $E(\mathbf{k}) \propto k_x^2 + k_y^2$，态密度 $D(E)$ 是一个常数。
    - **[鞍点](@entry_id:142576)**（即主曲率符号相反的[临界点](@entry_id:144653)）则会产生一个**对数发散**的[奇点](@entry_id:137764)，即 $D(E) \propto -\ln|E - E_c|$。一个典型的例子是二维方格子上最近邻[紧束缚模型](@entry_id:143446) $E(\mathbf{k}) = -2t[\cos(k_x a) + \cos(k_y a)]$，它在能量 $E=0$ 处有一个[鞍点](@entry_id:142576)，并在[态密度](@entry_id:147894)中表现为一个对数峰 ()。

这些[奇点](@entry_id:137764)在实验上是可观测的，例如在光学吸收谱或 STS 谱中。值得注意的是，PDOS 中的 van Hove [奇点](@entry_id:137764)可能被抑制。如果某个[临界点](@entry_id:144653) $\mathbf{k}_c$ 处的[布洛赫波函数](@entry_id:144223) $\lvert \psi_{n\mathbf{k}_c} \rangle$ 对某个[轨道](@entry_id:137151) $\alpha$ 的投影权重恰好为零，那么在 $D_{\alpha}(E)$ 中，相应的[奇点](@entry_id:137764)就会消失或减弱 ()。

### 从理论到实践：[态密度](@entry_id:147894)的数值计算

在实际的[计算材料科学](@entry_id:145245)研究中，态密度的表达式需要被离散化和近似处理。这主要涉及两个方面：[布里渊区积分](@entry_id:188454)的近似和狄拉克 $\delta$ 函数的处理。

#### [布里渊区积分](@entry_id:188454)：k 点取样

理论上的连续 BZ 积分在数值上通过在一个离散的 **k 点网格**（例如 Monkhorst-Pack 网格）上求和来近似。设网格包含 $N_k$ 个点，每个点的权重为 $w_{\mathbf{k}}$，则 DOS 的计算式变为：

$$
D(E) \approx \sum_n \sum_{\mathbf{k}} w_{\mathbf{k}} \, \delta(E - \varepsilon_{n\mathbf{k}})
$$

这种近似在数学上等价于在周期性定义域上使用**多维梯形法则**。其[收敛速度](@entry_id:636873)极大地依赖于被积函数的平滑度 ()。由于能带函数 $\varepsilon_n(\mathbf{k})$ 在 BZ 上是周期性的，如果被积函数是解析的（例如，当 $\delta$ 函数被一个光滑函数替换后），[梯形法则](@entry_id:145375)的误差会随网格密度呈指数级下降。具体来说，对于一个 $M \times M \times M$ 的网格 ($N_k=M^3$)，误差衰减为 $\mathcal{O}(\exp(-cM))$ 或 $\mathcal{O}(\exp(-c N_k^{1/3}))$。如果能带函数仅具有有限的 $C^r$ 光滑度，则[误差收敛](@entry_id:137755)速度为代数形式，即 $\mathcal{O}(M^{-r})$ 或 $\mathcal{O}(N_k^{-r/3})$ ()。

#### $\delta$ 函数的处理：展宽方案

直接使用离散的能量值 $\varepsilon_{n\mathbf{k}}$ 会产生一个由一系列尖刺组成的、难以解读的谱图。为了得到平滑的曲线并模拟物理展宽效应，$\delta$ 函数通常被一个归一化的、具有有限宽度的**展宽函数** $g_{\sigma}(x)$ 所替代，例如高斯函数或[洛伦兹函数](@entry_id:199503)。

$$
\delta(E - \varepsilon_{n\mathbf{k}}) \to g_{\sigma}(E - \varepsilon_{n\mathbf{k}}) = \frac{1}{\sigma\sqrt{2\pi}} \exp\left(-\frac{(E-\varepsilon_{n\mathbf{k}})^2}{2\sigma^2}\right)
$$

展宽参数 $\sigma$ 的选择是一个**偏差-方差权衡 (bias-variance tradeoff)** 的经典问题 ()。
- **偏差 (Bias)**：展宽会模糊掉 DOS 中的尖锐特征（如 van Hove [奇点](@entry_id:137764)），引入系统性误差。这个误差与展宽函数的形状和宽度有关。对于高斯展宽，主导的偏差项正比于 $\sigma^2 D''(E)$，它与 DOS 的曲率成正比。
- **[方差](@entry_id:200758) (Variance)**：有限的 k 点取样会引入统计噪声或“取样噪声”。展宽可以通过平均邻近能量的贡献来有效地降低这种噪声。[方差](@entry_id:200758)反比于 k 点数 $N_k$ 和展宽 $\sigma$，即 $\text{Var} \propto 1/(N_k \sigma)$。

为了获得最优的 DOS 估计，我们需要最小化总的**[均方误差](@entry_id:175403) (Mean Squared Error, MSE)**，MSE $\approx (\text{Bias})^2 + \text{Var}$。通过最小化 MSE，可以推导出最优展宽宽度 $\sigma_{\text{opt}}$ 与 k 点数 $N_k$ 的依赖关系：

$$
\sigma_{\text{opt}} \propto N_k^{-1/5}
$$

这个关系 () 告诉我们一个重要的实践准则：随着 k 点取样密度的增加（$N_k$ 增大），我们应该适度地减小展宽 $\sigma$ 来获得更高的[能量分辨率](@entry_id:180330)，但减小的速度不能太快，以避免噪声过分放大。

### 超越单粒子图像：相互作用体系的态密度

以上讨论均基于独立的、无相互作用的电[子图](@entry_id:273342)像。在真实材料中，电子之间以及电子与[晶格振动](@entry_id:140970)（[声子](@entry_id:140728)）之间存在复杂的相互作用。这些[多体效应](@entry_id:173569)深刻地改变了态密度的概念和形态。

#### 物理展宽：有限的[准粒子寿命](@entry_id:145453)

在相互作用体系中，一个被激发的电子（或空穴）会通过与其他[粒子散射](@entry_id:152941)而衰变，使其不再是一个能量确定的稳定本征态。这个“穿上”了相互作用“外套”的电子被称为**[准粒子](@entry_id:136584) (quasiparticle)**，它具有有限的**寿命**。

这种效应可以通过**[多体格林函数](@entry_id:196569)**理论来描述。[单粒子格林函数](@entry_id:140400) $G^R(\mathbf{k}, E)$ 的分母中包含了一个复数且依赖于能量的**[自能](@entry_id:145608) (self-energy)** $\Sigma(\mathbf{k}, E)$：

$$
G^R(\mathbf{k}, E) = \left[ E - \varepsilon_{\mathbf{k}} - \Sigma(\mathbf{k}, E) \right]^{-1}
$$

自能的实部 $\text{Re}\,\Sigma$ 导致了[准粒子能量](@entry_id:173936)的[重整化](@entry_id:143501)，而其虚部 $\text{Im}\,\Sigma$ 则与[准粒子](@entry_id:136584)的散射率或寿命的倒数相关。一个简单的模型是，在[准粒子能量](@entry_id:173936)附近，$\text{Im}\,\Sigma \approx -\Gamma/2$，其中 $\Gamma$ 是一个正的常数。在这种情况下，单粒子态密度不再是 $\delta$ 函数，而是由**[谱函数](@entry_id:147628) (spectral function)** $A(\mathbf{k}, E)$ 给出：

$$
A(\mathbf{k}, E) = -\frac{1}{\pi} \text{Im}\,G^R(\mathbf{k}, E) = \frac{1}{\pi} \frac{\Gamma/2}{(E - \tilde{\varepsilon}_{\mathbf{k}})^2 + (\Gamma/2)^2}
$$

其中 $\tilde{\varepsilon}_{\mathbf{k}}$ 是重整化后的[准粒子能量](@entry_id:173936)。这个函数是一个**[洛伦兹分布](@entry_id:155999)**，其半峰全宽 (FWHM) 正是 $\Gamma$ ()。这代表了一种内禀的、物理上的能量展宽，与数值计算中人为引入的展宽截然不同。

#### 完整的相互作用谱函数

在更一般的情况下，[自能](@entry_id:145608) $\Sigma(\mathbf{k}, E)$ 具有复杂的能量依赖性，导致谱函数 $A(\mathbf{k}, E)$ 的结构远比单个洛伦兹峰复杂。相互作用体系的[态密度](@entry_id:147894)需要通过对完整的谱函数在[布里渊区积分](@entry_id:188454)得到 ()：

$$
\rho(E) = g_s \sum_{\mathbf{k}} w_{\mathbf{k}} A(\mathbf{k}, E)
$$

此时的[谱函数](@entry_id:147628) $A(\mathbf{k}, E)$ 通常包含两类结构：
1.  **相干[准粒子](@entry_id:136584)峰 (Coherent quasiparticle peak)**：一个相对尖锐的峰，对应于寿命较长的[准粒子激发](@entry_id:138475)。然而，这个峰的积分权重，即**[准粒子](@entry_id:136584)[重整化](@entry_id:143501)因子** $Z_{\mathbf{k}}$，严格小于 1 ($0  Z_{\mathbf{k}}  1$)。
2.  **非相干背景和卫星峰 (Incoherent background and satellites)**：除了[准粒子](@entry_id:136584)峰之外，谱函数的其余部分构成了宽阔的非相干背景，其中可能出现一些被称为**卫星峰**的次级峰。

一个至关重要的**求和规则**是，对于任意 $\mathbf{k}$，[谱函数](@entry_id:147628)在全能量范围内的积分必须等于 1：

$$
\int_{-\infty}^{\infty} A(\mathbf{k}, E) \, dE = 1
$$

这表明，[多体相互作用](@entry_id:751663)并不会创造或消灭[量子态](@entry_id:146142)，而仅仅是**重新分配[谱权重](@entry_id:144751)**。相互作用将一部分本应属于[准粒子](@entry_id:136584)峰的[谱权重](@entry_id:144751)（即 $1 - Z_{\mathbf{k}}$ 的部分）转移到了非相干的卫星峰和背景中 ()。这些卫星峰不是计算假象，而是真实的物理特征，对应于更复杂的激发过程，例如一个电子的产生伴随着一个[等离激元](@entry_id:146184)或[声子](@entry_id:140728)的激发。因此，在[强关联电子体系](@entry_id:183796)中，[态密度](@entry_id:147894)谱往往呈现出[准粒子](@entry_id:136584)峰与高能量处宽阔卫星峰共存的复杂景象。