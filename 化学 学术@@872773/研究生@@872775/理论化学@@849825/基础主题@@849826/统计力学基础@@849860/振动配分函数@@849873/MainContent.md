## 引言
[分子振动](@entry_id:140827)是化学与物理世界中无处不在的基本现象，它决定了分子的稳定性、[光谱](@entry_id:185632)特征以及热力学性质。然而，如何从微观的量子化振动能级精确地预测宏观的、可测量的物质行为，是[理论化学](@entry_id:199050)中的一个核心问题。[振动配分函数](@entry_id:138551)正是解决这一问题的关键理论工具，它构筑了连接微观量子世界与宏观[热力学](@entry_id:141121)统计行为的桥梁。本文旨在为读者提供一个关于[振动配分函数](@entry_id:138551)的全面而深入的理解，从其理论基础到广泛的实际应用。
在接下来的内容中，我们将分三个章节展开探讨。在“原理与机制”一章中，我们将从第一性原理出发，阐明[振动配分函数](@entry_id:138551)是如何在玻恩-奥本海默近似和[刚性转子-谐振子](@entry_id:169758)模型下被严格定义的，并推导其数学表达式及其与[热力学](@entry_id:141121)量的关系。随后，在“应用与跨学科联系”一章中，我们将展示这一理论工具的强大威力，探讨它在计算[气体热力学](@entry_id:151144)性质、解释[化学平衡](@entry_id:142113)与同位素效应、构建[过渡态理论](@entry_id:178694)以及理解[材料科学](@entry_id:152226)现象中的核心作用。最后，在“动手实践”部分，我们提供了一系列计算问题，旨在通过实际操作，加深读者对理论知识的掌握，并将其应用于解决真实的研究问题。

## 原理与机制

在上一章中，我们介绍了[分子振动](@entry_id:140827)在化学和物理学中的普遍重要性。现在，我们将深入探讨描述[振动](@entry_id:267781)状态统计分布的数学框架——[振动配分函数](@entry_id:138551)。本章的目标是建立一个从第一性原理出发的严谨理解，阐明如何从微观量子能级过渡到宏观[热力学性质](@entry_id:146047)。我们将首先探讨将分子总[能量分解](@entry_id:193582)为独立[振动](@entry_id:267781)贡献的理论基础，然后构建单个与多个[振动](@entry_id:267781)模式的[配分函数](@entry_id:193625)，最后将其与可测量的[热力学](@entry_id:141121)量联系起来。我们还将讨论标准[谐振子模型](@entry_id:178080)的局限性，并介绍更高级的处理方法。

### [分子配分函数](@entry_id:152768)的基石：可分离性近似

在[统计力](@entry_id:194984)学中，一个分子的[配分函数](@entry_id:193625) $q$ 是对所有可[能量子](@entry_id:145536)态 $i$ 的[玻尔兹曼因子](@entry_id:141054)求和：$q = \sum_{i} \exp(-\beta \epsilon_{i})$，其中 $\beta = 1/(k_{\mathrm{B}} T)$，$k_{\mathrm{B}}$ 是[玻尔兹曼常数](@entry_id:142384)，$\epsilon_{i}$ 是态 $i$ 的能量。对于一个真实的气相[多原子分子](@entry_id:268323)，其能量包含[平动](@entry_id:187700)、转动、[振动](@entry_id:267781)和电子贡献，以及它们之间复杂的耦合。为了能够有意义地定义一个独立的 **[振动配分函数](@entry_id:138551) (vibrational partition function)** $q_{\mathrm{vib}}$，我们必须首先对总能量进行近似分解。

这一分解过程依赖于一系列层次分明的物理近似 [@problem_id:2824249]。

1.  **玻恩–奥本海默近似 (Born–Oppenheimer Approximation)**：这是最核心的步骤。由于[原子核](@entry_id:167902)的质量远大于电子（$m_{\mathrm{nuc}} \gg m_e$），我们可以假定[原子核](@entry_id:167902)的运动相对于电子的瞬时运动是缓慢的。这允许我们将电子的运动和[原子核](@entry_id:167902)的运动[解耦](@entry_id:637294)。对于固定的[原子核](@entry_id:167902)构型，我们求解电子的薛定谔方程，得到一个电[子基](@entry_id:151637)态和一系列电子激发态。在大多数化学相关的温度下，分子处于其电[子基](@entry_id:151637)态，电子激发所需的能量 $\Delta E_{\mathrm{elec}}$ 远大于热能 $k_{\mathrm{B}} T$。因此，[原子核](@entry_id:167902)的运动可以看作是在由电子[基态能量](@entry_id:263704)构成的 **[势能面](@entry_id:147441) (potential energy surface, PES)** 上进行的。这一近似将总[哈密顿量](@entry_id:172864) $H$ 分解为 $H \approx H_{\mathrm{elec}} + H_{\mathrm{nuc}}$。

2.  **核运动的[解耦](@entry_id:637294)**：对于一个孤立的分子（[理想气体模型](@entry_id:191415)的一个方面），其[原子核](@entry_id:167902)的总运动可以精确地分离为分子质心的 **平动 (translation)** 和分子内部的 **转动 (rotation)** 与 **[振动](@entry_id:267781) (vibration)**。这使得[核哈密顿量](@entry_id:752710)可以进一步分解为 $H_{\mathrm{nuc}} = H_{\mathrm{trans}} + H_{\mathrm{int}}$。

3.  **[刚性转子](@entry_id:156317)–[谐振子](@entry_id:155622) (Rigid-Rotor Harmonic-Oscillator, RRHO) 近似**：内部[哈密顿量](@entry_id:172864) $H_{\mathrm{int}}$ 仍然包含转动和[振动](@entry_id:267781)之间的耦合项。为了将它们分离，我们引入两个关键模型：
    *   **[刚性转子](@entry_id:156317) (Rigid-Rotor)** 模型假定分子的键长和键角固定在其平衡值，忽略了分子旋转时产生的[离心畸变](@entry_id:156195)。
    *   **谐振子 (Harmonic-Oscillator)** 模型将[振动](@entry_id:267781)势能近似为原子偏离其平衡位置的二次函数。这忽略了真实化学键的 **[非谐性](@entry_id:137191) (anharmonicity)**。

在RRHO近似下，内部[哈密顿量](@entry_id:172864)最终可以分解为 $H_{\mathrm{int}} \approx H_{\mathrm{rot}} + H_{\mathrm{vib}}$。综合以上步骤，分子的总能量可以近似地写为各个独立自由度能量的总和：

$$E_{\mathrm{total}} \approx E_{\mathrm{trans}} + E_{\mathrm{rot}} + E_{\mathrm{vib}} + E_{\mathrm{elec}}$$

这种能量的可加性直接导致了分子[总配分函数](@entry_id:190183)的 **可[因子分解](@entry_id:150389)性 (factorization)**：

$$q_{\mathrm{total}} \approx q_{\mathrm{trans}} q_{\mathrm{rot}} q_{\mathrm{vib}} q_{\mathrm{elec}}$$

正是这一系列的近似，为我们独立研究[振动配分函数](@entry_id:138551) $q_{\mathrm{vib}}$ 提供了理论依据。

### 单个[振动](@entry_id:267781)模式：量子谐振子

[振动配分函数](@entry_id:138551)的最基本单元是描述单个[振动](@entry_id:267781)模式的[配分函数](@entry_id:193625)。在[谐振子近似](@entry_id:268588)下，一个[振动](@entry_id:267781)角频率为 $\omega$ 的模式的[量子化能级](@entry_id:140911)由下式给出：

$$E_n = \left(n + \frac{1}{2}\right)\hbar\omega,  \text{ 其中 } n = 0, 1, 2, \ldots$$

其中 $\hbar$ 是约化普朗克常数，$n$ 是[振动](@entry_id:267781)[量子数](@entry_id:145558)。$n=0$ 的能级被称为 **[零点能](@entry_id:142176) (zero-point energy, ZPE)**，其值为 $E_0 = \frac{1}{2}\hbar\omega$。

根据定义，单个[振动](@entry_id:267781)模式的[配分函数](@entry_id:193625) $z_{\mathrm{vib}}$ 是对所有[振动能级](@entry_id:193001)求和：

$$z_{\mathrm{vib}} = \sum_{n=0}^{\infty} \exp(-\beta E_n) = \sum_{n=0}^{\infty} \exp\left[-\beta\left(n + \frac{1}{2}\right)\hbar\omega\right]$$

我们可以将[零点能](@entry_id:142176)因子 $\exp(-\frac{1}{2}\beta\hbar\omega)$ 提出：

$$z_{\mathrm{vib}} = \exp\left(-\frac{\beta\hbar\omega}{2}\right) \sum_{n=0}^{\infty} \left[\exp(-\beta\hbar\omega)\right]^n$$

上式中的求和部分是一个[公比](@entry_id:275383)为 $r = \exp(-\beta\hbar\omega)$ 的无穷几何级数。由于 $\beta > 0$ 和 $\omega > 0$，[公比](@entry_id:275383) $r$ 满足 $0  r  1$，因此级数收敛于 $\frac{1}{1-r}$。最终，我们得到包含[零点能](@entry_id:142176)的[振动配分函数](@entry_id:138551)表达式：

$$z_{\mathrm{vib}} = \frac{\exp(-\beta\hbar\omega/2)}{1 - \exp(-\beta\hbar\omega)}$$

在许多应用中，为了简化计算，我们常常将能量零点设定在[基态](@entry_id:150928)（即 $n=0$ 的态）上。这意味着我们计算的是相对于[基态](@entry_id:150928)的能量 $E_n^{(\text{rel})} = E_n - E_0 = n\hbar\omega$。在这种约定下，[配分函数](@entry_id:193625)记为 $\tilde{z}_{\mathrm{vib}}$ [@problem_id:2015502]：

$$\tilde{z}_{\mathrm{vib}} = \sum_{n=0}^{\infty} \exp(-\beta n\hbar\omega) = \frac{1}{1 - \exp(-\beta\hbar\omega)}$$

这两种能量约定的选择对[热力学](@entry_id:141121)量的计算有重要影响 [@problem_id:2824207]。通过比较两种[配分函数](@entry_id:193625)，$z_{\mathrm{vib}} = \exp(-\frac{1}{2}\beta\hbar\omega) \tilde{z}_{\mathrm{vib}}$，我们可以分析其对不同[热力学](@entry_id:141121)量的影响。对于一个包含 $N$ 个相同[振子](@entry_id:271549)的体系，[总配分函数](@entry_id:190183) $Z_{\mathrm{vib}} = (z_{\mathrm{vib}})^N$ 和 $\tilde{Z}_{\mathrm{vib}} = (\tilde{z}_{\mathrm{vib}})^N$ 的关系是 $Z_{\mathrm{vib}} = \exp(-\frac{1}{2}N\beta\hbar\omega) \tilde{Z}_{\mathrm{vib}}$。

*   对于依赖于[配分函数](@entry_id:193625)[绝对值](@entry_id:147688)的 **能量型函数**，如亥姆霍兹自由能 $A = -k_B T \ln Z$ 和内能 $U = -(\partial \ln Z / \partial \beta)_V$，选择不同的能量零点会导致一个恒定的能量偏移。具体来说，$A_{\mathrm{incl}} = A_{\mathrm{shift}} + \frac{1}{2}N\hbar\omega$ 和 $U_{\mathrm{incl}} = U_{\mathrm{shift}} + \frac{1}{2}N\hbar\omega$。同样，焓 $H$ 和吉布斯自由能 $G$ 也会有相同的能量偏移。

*   对于依赖于[配分函数](@entry_id:193625)对温度的导数的 **熵型函数**，如熵 $S = (U-A)/T$ 和热容 $C_V = (\partial U / \partial T)_V$，这个恒定的能量偏移在求导过程中会被消除。因此，$S_{\mathrm{incl}} = S_{\mathrm{shift}}$ 且 $C_{V, \mathrm{incl}} = C_{V, \mathrm{shift}}$。

结论是，虽然绝对能量值依赖于能量零点的选择，但熵、热容以及能量或自由能的变化值（如[化学反应](@entry_id:146973)中的 $\Delta G$）是不变的。然而，在[计算化学](@entry_id:143039)反应的平衡常数 $K = \exp(-\Delta G^{\circ}/(k_B T))$ 时，必须注意，反应物和产物的总[零点能](@entry_id:142176)之差 $\Delta E_{\mathrm{ZPE}}$ 是一个真实的物理量，它对 $\Delta G^{\circ}$ 有重要贡献。因此，在计算中必须一致地包含或排除零点能，或者在使用相对能量标度后，将 $\Delta E_{\mathrm{ZPE}}$ 单独加回到总能量变化中。

### [多原子分子](@entry_id:268323)：[振动](@entry_id:267781)模式的组合

一个含有 $N$ 个原子的[非线性分子](@entry_id:175085)有 $3N-6$ 个独立的[振动](@entry_id:267781)模式（[线性分子](@entry_id:166760)有 $3N-5$ 个）。在[谐振子近似](@entry_id:268588)下，这些 **[简正模](@entry_id:139640)式 (normal modes)** 是相互独立的。这意味着分子的总振动能 $E_{\mathrm{vib}}$ 是其所有[简正模](@entry_id:139640)式能量之和：

$$E_{\mathrm{vib}}(\{n_i\}) = \sum_{i=1}^{3N-6} E_{n_i} = \sum_{i=1}^{3N-6} \left(n_i + \frac{1}{2}\right)\hbar\omega_i$$

其中 $\{n_i\} = (n_1, n_2, \ldots)$ 代表了所有模式的[振动](@entry_id:267781)[量子数](@entry_id:145558)组合。

由于能量是可加的，总[振动配分函数](@entry_id:138551) $q_{\mathrm{vib}}$ 可以分解为各个独立模式[配分函数](@entry_id:193625) $z_i$ 的乘积 [@problem_id:2015533]：

$$q_{\mathrm{vib}} = \sum_{\{n_i\}} \exp\left(-\beta \sum_i E_{n_i}\right) = \prod_{i=1}^{3N-6} \sum_{n_i=0}^{\infty} \exp(-\beta E_{n_i}) = \prod_{i=1}^{3N-6} z_i$$

将单个模式的[配分函数](@entry_id:193625)代入，我们得到[多原子分子](@entry_id:268323)的总[振动配分函数](@entry_id:138551)（包含ZPE）：

$$q_{\mathrm{vib}} = \prod_{i=1}^{3N-6} \frac{\exp(-\beta\hbar\omega_i/2)}{1 - \exp(-\beta\hbar\omega_i)}$$

在[分子对称性](@entry_id:202199)导致某些[振动](@entry_id:267781)模式具有相同频率 $\omega$ 的情况下，即出现 **简并 (degeneracy)**，计算会变得更加简洁。如果一个频率 $\omega$ 的简并度为 $g$（即有 $g$ 个模式具有相同的频率），那么它们对[总配分函数](@entry_id:190183)的贡献就是单个模式[配分函数](@entry_id:193625)的 $g$ 次方 [@problem_id:2824245]。

$$q_{\mathrm{vib, degen}} = (z_{\mathrm{vib}}(\omega))^g = \left(\frac{\exp(-\beta\hbar\omega/2)}{1 - \exp(-\beta\hbar\omega)}\right)^g$$

需要强调的是，[简正模](@entry_id:139640)式是分子内部可区分的自由度（例如，$\text{CO}_2$ 的两个简并弯曲[振动](@entry_id:267781)在空间上是正交的），因此它们的[配分函数](@entry_id:193625)直接相乘。这不同于处理 $g$ 个不可区分的气体粒子，后者需要在[配分函数](@entry_id:193625)中引入 $1/g!$ 因子。

### 从[配分函数](@entry_id:193625)到热力学性质

[振动配分函数](@entry_id:138551)是连接微观量子世界和宏观[热力学性质](@entry_id:146047)的桥梁。一旦我们得到了[配分函数](@entry_id:193625) $Z_{\mathrm{vib}}$，所有相关的[热力学](@entry_id:141121)量都可以通过标准公式推导出来。

#### [亥姆霍兹自由能](@entry_id:136442)

亥姆霍兹自由能 $A$ 与[配分函数](@entry_id:193625) $Z$ 的基本关系是 $A = -k_B T \ln Z$。因此，[振动](@entry_id:267781)对亥姆霍兹自由能的贡献为 $A_{\mathrm{vib}} = -k_B T \ln Z_{\mathrm{vib}}$。对于由 $N$ 个可区分的独立分子组成的体系（例如[晶格](@entry_id:196752)中的分子），[总配分函数](@entry_id:190183)是 $Z_{\mathrm{vib}} = (z_{\mathrm{vib}})^N$，其中 $z_{\mathrm{vib}}$ 是单个分子的[振动配分函数](@entry_id:138551)。此时，自由能为 [@problem_id:2015504]：

$$A_{\mathrm{vib}} = -N k_B T \ln z_{\mathrm{vib}}$$

#### 平均振动能

体系的平均[振动能](@entry_id:157909) $\langle U_{\mathrm{vib}} \rangle$ 可以通过对 $\ln Z_{\mathrm{vib}}$ 求导得到：

$$\langle U_{\mathrm{vib}} \rangle = - \left( \frac{\partial \ln Z_{\mathrm{vib}}}{\partial \beta} \right)_V$$

对于单个谐振子（使用相对能量标度 $\tilde{z}_{\mathrm{vib}}$），$\ln \tilde{z}_{\mathrm{vib}} = -\ln(1 - \exp(-\beta\hbar\omega))$，其[平均能量](@entry_id:145892)为：

$$\langle \epsilon_{\mathrm{vib}} \rangle = \frac{\hbar\omega \exp(-\beta\hbar\omega)}{1 - \exp(-\beta\hbar\omega)} = \frac{\hbar\omega}{\exp(\beta\hbar\omega) - 1}$$

这个表达式展示了[配分函数](@entry_id:193625)与能量之间的直接联系。例如，如果实验测得在某温度下单分子[振动[配分函](@entry_id:138551)数](@entry_id:193625) $\tilde{z}_v$（相对能量标度）的值为 $1.5$，我们可以反解出 $\exp(-\beta h\nu) = 1/3$，进而计算出平均振动能 $\langle \epsilon_v \rangle = \frac{h\nu}{2}$。由于 $\beta h\nu = \ln 3$，即 $h\nu = k_B T \ln 3$，我们可以得到 $\langle \epsilon_v \rangle = \frac{k_B T \ln 3}{2} \approx 0.5493 k_B T$ [@problem_id:2023556]。

#### [振动热容](@entry_id:151645)

恒容[热容](@entry_id:137594) $C_V$ 定义为内能在恒定体积下对温度的导数，$C_{V,\mathrm{vib}} = (\frac{\partial \langle U_{\mathrm{vib}} \rangle}{\partial T})_V$。对于一个包含 $N$ 个相同独立一维[谐振子](@entry_id:155622)的体系，其总振动能为 $U_{\mathrm{vib}} = N \left( \frac{1}{2}h\nu + \frac{h\nu}{\exp(\beta h\nu) - 1} \right)$。对温度求导（注意[零点能](@entry_id:142176)项是常数，其导数为零），我们得到[振动热容](@entry_id:151645)的表达式 [@problem_id:2015492]：

$$C_{V,\mathrm{vib}} = N k_B \left(\frac{h\nu}{k_B T}\right)^2 \frac{\exp(h\nu/k_B T)}{[\exp(h\nu/k_B T) - 1]^2}$$

这个函数形式，通常被称为 **爱因斯坦函数**，是描述固体[热容](@entry_id:137594)的爱因斯坦模型的核心。它正确地预测了在高温极限下（$k_B T \gg h\nu$），每个[振子](@entry_id:271549)对[热容](@entry_id:137594)的贡献趋近于经典值 $k_B$（[杜隆-珀蒂定律](@entry_id:191078)）；在低温极限下（$k_B T \ll h\nu$），热容指数式地趋近于零，符合[热力学](@entry_id:141121)第三定律。

#### [振动熵](@entry_id:756496)

[振动熵](@entry_id:756496) $S_{\mathrm{vib}}$ 可以通过 $S_{\mathrm{vib}} = (U_{\mathrm{vib}} - A_{\mathrm{vib}})/T = k_B \ln Z_{\mathrm{vib}} + U_{\mathrm{vib}}/T$ 计算。对于单个[谐振子](@entry_id:155622)，其表达式为：

$$S_{\mathrm{vib}} = k_B \left[ \frac{\beta\hbar\omega}{\exp(\beta\hbar\omega) - 1} - \ln(1 - \exp(-\beta\hbar\omega)) \right]$$

值得注意的是，此表达式与能量零点的选择无关。在高温极限下 ($k_B T \gg \hbar\omega$)，熵的行为近似为 $S \approx k_B[1 - \ln(\beta\hbar\omega)]$。在低温极限下 ($T \to 0$)，熵趋近于零，$S \to 0$，符合[热力学](@entry_id:141121)第三定律，因为体系的[基态](@entry_id:150928)是唯一的（所有[振子](@entry_id:271549)处于 $n=0$ 态）[@problem_id:2824245]。

### 超越谐振子模型：高级主题

尽管RRH[O模](@entry_id:186318)型功能强大，但它终究是一个近似。在某些情况下，其局限性会变得非常明显，需要更精细的模型来获得准确的[热化学](@entry_id:137688)数据。

#### 低频模式与熵的发散问题

在柔性[大分子](@entry_id:150543)（如大环或长链分子）中，常常存在一些频率非常低的 **[软模式](@entry_id:137007) (soft modes)**，例如内部扭转[振动](@entry_id:267781)。当使用标准谐振子模型处理这些频率接近于零（例如 $\tilde{\nu}  100\,\text{cm}^{-1}$）的模式时，会出现一个严重的问题：计算出的熵会变得异常大，甚至趋于无穷 [@problem_id:2824198]。

我们可以从熵的表达式来理解这个问题。在低频极限下（$\nu \to 0$，即 $x = h\nu/k_B T \to 0$），熵的近似行为是：

$$S_{\mathrm{vib}} \approx k_B [1 - \ln(h\nu/k_B T)] = k_B[1 + \ln(k_B T / h) - \ln\nu]$$

这个表达式表明，当 $\nu \to 0$ 时，熵会随 $\ln(\nu^{-1})$ 对数发散。其物理根源在于，谐振子势 $V(q) = \frac{1}{2} k q^2$ 是一个无界抛物线，允许[振子](@entry_id:271549)在能量足够高时运动到无穷远处。当频率 $\nu$ 极低时，[能级间距](@entry_id:181168) $h\nu$ 变得非常小，在任何有限温度下，热能 $k_B T$ 都足以布居大量密集的能级，导致统计上的状态数（即熵）趋于无穷。

这显然是不物理的。真实的分子内运动，如扭转，是被限制在有限空间内的。一个扭转角只能在 $0$到 $2\pi$ 之间变化。因此，更物理的模型应该是一个 **受阻转子 (hindered rotor)** 或被限制在有限区域内的粒子。这些模型具有不同的能级结构，其熵在任何温度下都是有限的。在计算化学实践中，解决这个问题的方法包括：
*   用受阻转子模型代替谐振子模型来处理特定的低频模式。
*   采用 **准[谐波](@entry_id:181533) (quasi-harmonic)** 修正，例如，设定一个频率的下限，低于此阈值的频率被强制提升到该值，这相当于隐含地施加了一个空间限制。

#### [转振耦合](@entry_id:157969)

RRH[O模](@entry_id:186318)型的另一个核心近似是完全分离转动和[振动](@entry_id:267781)。然而，实际上分子的转动惯量会随着[振动态](@entry_id:162097)的改变而变化。当一个键伸长时，转动惯量会增大，导致[转动常数](@entry_id:191788)减小。这种 **[转振耦合](@entry_id:157969) (rovibrational coupling)** 效应可以通过高分辨率[光谱](@entry_id:185632)实验精确测量。

一个更精确的能量模型将转动常数表示为[振动](@entry_id:267781)量子数 $\mathbf{v} = (v_1, \dots, v_f)$ 的函数：

$$B_{\mathbf{v}} = B_e - \sum_{i=1}^f \alpha_i^B \left(v_i + \frac{1}{2}\right) + \sum_{i,j=1}^f \gamma_{ij}^B \left(v_i + \frac{1}{2}\right)\left(v_j + \frac{1}{2}\right) + \dots$$

其中 $B_e$ 是平衡构型下的转动常数，$\alpha_i$ 和 $\gamma_{ij}$ 是从[光谱](@entry_id:185632)中得到的一阶和二阶[转振相互作用](@entry_id:181261)常数。

为了系统地将这些耦合效应纳入[热力学](@entry_id:141121)计算，最严谨的计算方案是执行 **逐态求和 (state-by-state summation)** [@problem_id:2824247]。该方案的步骤如下：
1.  对于每一个可能的[振动态](@entry_id:162097) $\mathbf{v}$，使用上述[光谱](@entry_id:185632)公式计算其特定的[转动常数](@entry_id:191788) $A_{\mathbf{v}}, B_{\mathbf{v}}, C_{\mathbf{v}}$。
2.  使用这些[振动态](@entry_id:162097)依赖的转动常数，计算该[振动态](@entry_id:162097)下的所有[转动能级](@entry_id:155495) $E_{\mathrm{rot}}^{(\mathbf{v})}(J, \tau)$。
3.  构造总的[转振能级](@entry_id:204091) $E(\mathbf{v}, J, \tau) = E_{\mathrm{vib}}(\mathbf{v}) + E_{\mathrm{rot}}^{(\mathbf{v})}(J, \tau)$。
4.  通过对所有转振态 $(\mathbf{v}, J, \tau)$ 的[玻尔兹曼因子](@entry_id:141054)进行直接求和，构建总的转振[配分函数](@entry_id:193625) $Q_{\mathrm{rovib}}$。这个求和需要进行到足够高的[量子数](@entry_id:145558)，直到[配分函数](@entry_id:193625)的值收敛。
5.  最后，从这个收敛的、包含了耦合效应的[配分函数](@entry_id:193625) $Q_{\mathrm{rovib}}$ 出发，推导所有的[热力学函数](@entry_id:755914)。

这种方法虽然计算量巨大，但它从根本上是正确的，避免了诸如使用热平均[转动常数](@entry_id:191788)等简化近似所带来的误差，是[高精度计算](@entry_id:200567)[化学热力学](@entry_id:137221)数据的标准方法之一。