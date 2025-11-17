## 引言
电化学是理解能量转换的核心领域，它连接了[化学反应](@entry_id:146973)的内在驱动力与可被利用的电能。然而，我们如何精确地量化一个[化学反应](@entry_id:146973)产生电能的能力，并预测其在不同条件下的行为？这一基本问题是连接[化学热力学](@entry_id:137221)与电工学的桥梁。本文旨在系统地回答这一问题，深入探讨电池[电势](@entry_id:267554)、[吉布斯自由能](@entry_id:146774)和[平衡常数](@entry_id:141040)这三个关键[物理化学](@entry_id:145220)量之间的深刻联系。文章将分为三个部分：首先，在“原理与机制”一章中，我们将建立连接这三个量的核心数学方程，并探讨浓度和温度等因素如何影响它们。接着，在“应用与跨学科联系”一章中，我们将展示这些理论如何在能源科学、[材料工程](@entry_id:162176)、[分析化学](@entry_id:137599)乃至生命科学等领域发挥实际作用。最后，“动手实践”部分将提供具体问题，帮助读者巩固所学知识，将理论应用于解决实际的计算挑战。

## 原理与机制

在理解电化学系统的核心驱动力时，我们必须关联两个看似不同却内在统一的视角：化学[反应的自发性](@entry_id:139988)，通常用吉布斯自由能变($\Delta G$)来衡量；以及电化学电池对外做功能力的量度，即电池[电势](@entry_id:267554)($E_{cell}$)。本章将系统地阐述电池[电势](@entry_id:267554)、吉布斯自由能和[平衡常数](@entry_id:141040)这三个核心[热力学](@entry_id:141121)量之间的深刻联系，并探讨浓度和温度等条件如何影响这些关系。

### 电池[电势](@entry_id:267554)与[吉布斯自由能](@entry_id:146774)：基本原理

在恒温恒压下，一个[化学反应](@entry_id:146973)体系所能做的最大[非体积功](@entry_id:137402)（$w_{\text{max, non-exp}}$）等于其[吉布斯自由能](@entry_id:146774)的减少量。对于一个电化学电池，这种[非体积功](@entry_id:137402)主要是[电功](@entry_id:273970)。因此，当一个自发的氧化还原反应在电池中发生时，体系对外做的[最大电功](@entry_id:265133)等于吉布斯自由能变($\Delta G$)的负值：

$$ w_{\text{max, non-exp}} = w_{\text{elec}} = -\Delta G $$

从电学角度看，电功是转移的[电荷](@entry_id:275494)量($q$)与[电势差](@entry_id:275724)($E_{cell}$)的乘积。对于一个转移了 $n$ 摩尔电子的氧化还原反应，总[电荷](@entry_id:275494)量为 $q = nF$，其中 $F$ 是法拉第常数，约等于 $96485 \text{ C/mol}$，代表每摩尔电子所带的[电荷](@entry_id:275494)量。因此，[电功](@entry_id:273970)可以表示为：

$$ w_{\text{elec}} = nFE_{cell} $$

将这两个表达式结合起来，我们得到了连接[热力学](@entry_id:141121)与电化学的中心方程：

$$ \Delta G = -nFE_{cell} $$

这个方程揭示了电[化学反应](@entry_id:146973)的三个关键方面：

1.  **[反应的自发性](@entry_id:139988)**：一个[反应的自发性](@entry_id:139988)由 $\Delta G$ 的符号决定。由于 $n$ 和 $F$ 均为正值，$\Delta G$ 的符号与 $E_{cell}$ 的符号正好相反。
    *   当 $E_{cell} > 0$ 时，$\Delta G  0$，反应是自发的。这对应于一个**原电池**（galvanic cell），它能自发地产生电流。
    *   当 $E_{cell}  0$ 时，$\Delta G > 0$，反应是非自发的。必须从外界提供能量（例如，施加一个更高的电压）才能使反应发生。这对应于一个**[电解池](@entry_id:136674)**（electrolytic cell）。
    *   当 $E_{cell} = 0$ 时，$\Delta G = 0$，反应处于平衡状态，没有净反应发生，电池无法对外做功。

2.  **[能量转换](@entry_id:165656)**：$\Delta G$ 代表反应中化学能的变化，而 $nFE_{cell}$ 代表系统能够输出的电能。此方程定量地描述了化学能到电能的转换。例如，如果一个电池的标准电势为 $E^{\circ}_{\text{cell}} = 1.61 \text{ V}$，并且在反应中有 $0.0750$ 摩尔的锌被消耗（$\text{Zn(s)} \rightarrow \text{Zn}^{2+}(\text{aq}) + 2e^-$），我们可以计算出其能做的[最大电功](@entry_id:265133)。每消耗1摩尔锌，转移2摩尔电子。因此，总共转移的电子摩尔数为 $n_{\text{total}} = 0.0750 \text{ mol} \times 2 = 0.150 \text{ mol}$。[最大功](@entry_id:143924)为 $w_{\text{max, non-exp}} = n_{\text{total}} F E_{\text{cell}} = (0.150 \text{ mol}) \times (96485 \text{ C/mol}) \times (1.61 \text{ J/C}) \approx 23.3 \text{ kJ}$。[@problem_id:1983493]

3.  **参数互算**：该方程允许我们通过测量一个量来计算另一个量。例如，如果我们通过[量热法](@entry_id:145378)等手段测得某反应的 $\Delta G^{\circ} = -96.5 \text{ kJ/mol}$，且已知该反应转移 $n=1$ 摩尔电子，我们就能计算其[标准电池电势](@entry_id:139386)：$E^{\circ}_{\text{cell}} = -\frac{\Delta G^{\circ}}{nF} = -\frac{-96500 \text{ J/mol}}{1 \text{ mol} \times 96485 \text{ C/mol}} \approx 1.00 \text{ V}$。[@problem_id:1983501] 反之，若已知 $\Delta G^{\circ}$ 和 $E^{\circ}_{\text{cell}}$，我们也可以确定反应中的电子转移数 $n$ [@problem_id:1983467]。

### 标准条件与[标准电势](@entry_id:154815)

为了能够在统一的基础上比较不同电[化学反应](@entry_id:146973)的内在趋势，化学家定义了一套**标准条件**：所有溶液组分的浓度（严格来说是活度）为 $1 \text{ M}$，所有气体组分的[分压](@entry_id:168927)（严格来说是逸度）为 $1 \text{ bar}$，温度通常指定为 $298.15 \text{ K}$ ($25 ^{\circ}\text{C}$)。在标准条件下的[吉布斯自由能变](@entry_id:138324)和电池[电势](@entry_id:267554)分别称为**[标准吉布斯自由能变](@entry_id:168647)**($\Delta G^{\circ}$)和**[标准电池电势](@entry_id:139386)**($E^{\circ}_{\text{cell}}$)，它们之间的关系为：

$$ \Delta G^{\circ} = -nFE^{\circ}_{\text{cell}} $$

然而，我们无法测量单个电极（半电池）的绝对[电势](@entry_id:267554)。任何电压测量都需要两个电极构成一个完整的回路。为了解决这个问题，国际上约定选择**[标准氢电极](@entry_id:145560)**（Standard Hydrogen Electrode, SHE）作为通用参比，并**定义**其在标准条件下的电极电势为 $0.00 \text{ V}$。

$$ 2\text{H}^{+}(\text{aq}, 1 \text{ M}) + 2e^{-} \rightleftharpoons \text{H}_2(\text{g}, 1 \text{ bar}) \quad E^{\circ} = 0.00 \text{ V} $$

这个零点是人为设定的约定，而非氢本身的某种“天然”零[电势](@entry_id:267554)属性。它为所有其他半反应[电势](@entry_id:267554)的测量提供了一个基准。[@problem_id:1979877] 其他所有[半反应](@entry_id:266806)的[标准还原电势](@entry_id:144699)都是相对于SHE测得的。

一个完整电池的[标准电势](@entry_id:154815) $E^{\circ}_{\text{cell}}$ 由其阴极（发生还原反应）和[阳极](@entry_id:140282)（发生氧化反应）的[标准还原电势](@entry_id:144699)决定：

$$ E^{\circ}_{\text{cell}} = E^{\circ}_{\text{cathode}} - E^{\circ}_{\text{anode}} $$

理解[电势](@entry_id:267554)的**[强度性质](@entry_id:181209)**（intensive property）和自由能的**[广延性质](@entry_id:145410)**（extensive property）至关重要。$E^{\circ}$ 如同温度或密度，不依赖于反应物料的多少。如果我们将一个[反应的化学计量](@entry_id:153621)系数加倍，例如从反应 A 变为反应 B [@problem_id:1983477]：
反应 A: $\text{MnO}_4^- + 5\text{Fe}^{2+} + 8\text{H}^+ \rightarrow \text{Mn}^{2+} + 5\text{Fe}^{3+} + 4\text{H}_2\text{O}$
反应 B: $2\text{MnO}_4^- + 10\text{Fe}^{2+} + 16\text{H}^+ \rightarrow 2\text{Mn}^{2+} + 10\text{Fe}^{3+} + 8\text{H}_2\text{O}$

反应 B 的电子转移数 $n_B$ 是反应 A 的两倍（$n_B = 2n_A$），总的自由能变化 $\Delta G^{\circ}_B$ 也是两倍（$\Delta G^{\circ}_B = 2\Delta G^{\circ}_A$）。然而，[标准电池电势](@entry_id:139386)保持不变：

$$ E^{\circ}_B = -\frac{\Delta G^{\circ}_B}{n_B F} = -\frac{2\Delta G^{\circ}_A}{2n_A F} = -\frac{\Delta G^{\circ}_A}{n_A F} = E^{\circ}_A $$

由于 $E^{\circ}$ 不具有加和性，当组合[半反应](@entry_id:266806)以获得新的[半反应](@entry_id:266806)时，我们不能直接将它们的 $E^{\circ}$ 值相加。正确的方法是利用 $\Delta G^{\circ}$ 的加和性。例如，要计算[半反应](@entry_id:266806) $\text{VO}_2^+ + 4\text{H}^+ + 2e^- \rightarrow \text{V}^{3+} + 2\text{H}_2\text{O}$ 的 $E^{\circ}$，我们可以利用以下两个已知反应的 $\Delta G^{\circ}$ [@problem_id:1983443]：

1.  $\text{VO}_2^+ + 2\text{H}^+ + e^- \rightarrow \text{VO}^{2+} + \text{H}_2\text{O} \quad (\Delta G^{\circ}_1 = -n_1 F E^{\circ}_1)$
2.  $\text{VO}^{2+} + 2\text{H}^+ + e^- \rightarrow \text{V}^{3+} + \text{H}_2\text{O} \quad (\Delta G^{\circ}_2 = -n_2 F E^{\circ}_2)$

目标反应是上述两反应之和，其 $\Delta G^{\circ}_{\text{target}} = \Delta G^{\circ}_1 + \Delta G^{\circ}_2$。目标反应转移的电子数 $n_{\text{target}} = n_1 + n_2 = 2$。因此，其[标准电势](@entry_id:154815)为：

$$ E^{\circ}_{\text{target}} = -\frac{\Delta G^{\circ}_{\text{target}}}{n_{\text{target}}F} = -\frac{\Delta G^{\circ}_1 + \Delta G^{\circ}_2}{(n_1+n_2)F} = \frac{n_1 E^{\circ}_1 + n_2 E^{\circ}_2}{n_1+n_2} $$

这表明正确的组合方式是对 $E^{\circ}$ 值按电子转移数进行加权平均。

### 能斯特方程：浓度的影响

实际的电化学电池很少恰好在标准条件下工作。**[能斯特方程](@entry_id:146917)**（Nernst equation）将电池[电势](@entry_id:267554)与非标准条件下的反应物和产物浓度（或[分压](@entry_id:168927)）联系起来。它可以从基本的[热力学](@entry_id:141121)关系 $\Delta G = \Delta G^{\circ} + RT \ln Q$ 推导得出。其中，$Q$ 是[反应商](@entry_id:145217)，其形式与平衡常数表达式相同，但使用的是任意时刻的浓度或分压。

将 $\Delta G = -nFE_{\text{cell}}$ 和 $\Delta G^{\circ} = -nFE^{\circ}_{\text{cell}}$ 代入上式：

$$ -nFE_{\text{cell}} = -nFE^{\circ}_{\text{cell}} + RT \ln Q $$

两边同时除以 $-nF$，便得到[能斯特方程](@entry_id:146917)的标准形式：

$$ E_{\text{cell}} = E^{\circ}_{\text{cell}} - \frac{RT}{nF} \ln Q $$

这个方程告诉我们：
*   当 $Q  1$ 时（反应物浓度相对较高），$\ln Q  0$，因此 $E_{\text{cell}} > E^{\circ}_{\text{cell}}$。相对于标准态，电池的驱动力更大。
*   当 $Q > 1$ 时（产物浓度相对较高），$\ln Q > 0$，因此 $E_{\text{cell}}  E^{\circ}_{\text{cell}}$。电池的驱动力减小。
*   当 $Q = 1$ 时（[标准态](@entry_id:145000)），$\ln Q = 0$，因此 $E_{\text{cell}} = E^{\circ}_{\text{cell}}$。

例如，考虑一个基于反应 $\text{Sn}(s) + \text{Fe}^{2+}(\text{aq}) \rightarrow \text{Sn}^{2+}(\text{aq}) + \text{Fe}(s)$ 的电池，其 $E^{\circ}_{\text{cell}} = -0.30 \text{ V}$。如果在非标准条件下，$[\text{Fe}^{2+}] = 2.25 \text{ M}$ 且 $[\text{Sn}^{2+}] = 0.0500 \text{ M}$，那么[反应商](@entry_id:145217) $Q = \frac{[\text{Sn}^{2+}]}{[\text{Fe}^{2+}]} = \frac{0.0500}{2.25} \approx 0.0222$。由于 $Q  1$，我们预期 $E_{\text{cell}}$ 会比 $E^{\circ}_{\text{cell}}$ 更正（或更少负）。通过能斯特方程计算，在 $298.15 \text{ K}$，可以得到 $E_{\text{cell}} \approx -0.251 \text{ V}$，证实了这一点。[@problem_id:1983516]

能斯特方程完美地解释了为什么电池在使用过程中电压会下降。随着电池放电，反应物被消耗，产物被生成，导致 $Q$ 值不断增大，$\ln Q$ 项的负贡献也随之增大，从而使 $E_{\text{cell}}$ 持续降低。一个更复杂的例子是计算一个电池在放电一定时间（例如，以 $0.750 \text{ A}$ 电流放电 $4.00$ 小时）后的[电势](@entry_id:267554)。这需要先利用法拉第定律 ($n_e = It/F$) 计算转移的电子摩尔数，然后根据[化学计量关系](@entry_id:144494)更新各离子的浓度，计算出新的 $Q$ 值，最后代入能斯特方程求解新的 $E_{\text{cell}}$。[@problem_id:1983488]

一个特别能体现能斯特方程精髓的例子是**[浓差电池](@entry_id:262780)**。这种电池的两个半电池使用完全相同的化学物质，因此它们的[标准还原电势](@entry_id:144699)相同，$E^{\circ}_{\text{cathode}} = E^{\circ}_{\text{anode}}$，导致 $E^{\circ}_{\text{cell}} = 0$。[@problem_id:1544734] 然而，只要两个半池中对应物质的浓度不同，就会产生[电势](@entry_id:267554)。[电势](@entry_id:267554)完全来源于浓度梯度所驱动的使浓度均一化的趋势。对于一个银[浓差电池](@entry_id:262780)，其[电势](@entry_id:267554)为 $E_{\text{cell}} = -\frac{RT}{F} \ln \frac{[\text{Ag}^+]_{\text{anode}}}{[\text{Ag}^+]_{\text{cathode}}}$。

值得注意的是，能斯特方程的严格形式应使用**活度**($a$)代替浓度([C])或[分压](@entry_id:168927)(P)。活度是物质的“有效浓度”，通过活度系数($\gamma$)进行修正：$a = \gamma [C]$。在稀溶液中，$\gamma \approx 1$，浓度是活度的良好近似。但在浓溶液中，离子间的相互作用变得显著，$\gamma$ 会偏离1，此时必须使用活度才能进行精确计算。忽略活度系数会给计算结果带来可观的误差。[@problem_id:1983510]

### [电化学平衡](@entry_id:268744)

任何自发的原电池反应最终都会达到一个不再有宏观变化的终点，这个状态就是**[化学平衡](@entry_id:142113)**。从[热力学](@entry_id:141121)角度看，此时体系的吉布斯自由能达到最小值，进一步反应的驱动力($\Delta G$)为零。

根据我们的中心方程 $\Delta G = -nFE_{\text{cell}}$，当 $\Delta G = 0$ 时，必然有 $E_{\text{cell}} = 0$。这意味着一个“没电”的电池，其[电势](@entry_id:267554)为零，其内部的[化学反应](@entry_id:146973)已经达到了平衡。

同时，在平衡状态下，[反应商](@entry_id:145217) $Q$ 也达到了其特定温度下的定值，即**平衡常数** $K$。所以，在[电化学平衡](@entry_id:268744)点上，我们有以下[等价关系](@entry_id:138275) [@problem_id:1983508]：

$$ E_{\text{cell}} = 0 \quad \iff \quad \Delta G = 0 \quad \iff \quad Q = K $$

我们可以从一个反应进程的图像上直观地理解这一点。如果绘制体系总吉布斯自由能 $G$ 随[反应进度](@entry_id:140591) $\xi$ 变化的曲线，对于一个[自发反应](@entry_id:140874)，曲线将从代表纯反应物的初始高点下降。[曲线的斜率](@entry_id:178976) $(\partial G / \partial \xi)_{T,P}$ 就是反应的吉布斯自由能变 $\Delta_r G$ (即 $\Delta G$)。因为 $\Delta G = -nFE_{\text{cell}}$，所以曲线的负斜率与 $E_{\text{cell}}$ 成正比。反应开始时，斜率最陡峭（最负），对应于最大的初始[电势](@entry_id:267554)。随着反应进行，曲线趋于平缓，斜率减小，$E_{\text{cell}}$ 也随之下降。当体系达到曲线的最低点时，斜率为零，这意味着 $\Delta G = 0$ 和 $E_{\text{cell}} = 0$，系统达到平衡。[@problem_id:1983476]

### 三位一体：$E^{\circ}_{\text{cell}}$、$\Delta G^{\circ}$ 与 $K$ 的关系

[标准电池电势](@entry_id:139386) $E^{\circ}_{\text{cell}}$、[标准吉布斯自由能变](@entry_id:168647) $\Delta G^{\circ}$ 和[平衡常数](@entry_id:141040) $K$ 是描述一个[化学反应](@entry_id:146973)内在趋势的三个核心[热力学](@entry_id:141121)参数。它们是内在关联的，知道其中任何一个，就可以计算出另外两个。

我们已经建立了它们两两之间的关系：
1.  $\Delta G^{\circ} = -nFE^{\circ}_{\text{cell}}$
2.  $\Delta G^{\circ} = -RT \ln K$

将这两个方程联立，消去 $\Delta G^{\circ}$，我们得到 $E^{\circ}_{\text{cell}}$ 和 $K$ 之间的直接关系 [@problem_id:460645] [@problem_id:2921152]：

$$ -nFE^{\circ}_{\text{cell}} = -RT \ln K $$

$$ E^{\circ}_{\text{cell}} = \frac{RT}{nF} \ln K $$

这组方程构成了[电化学热力学](@entry_id:264154)的“金三角”，允许我们从任意一个顶点出发，到达另一个顶点。

**定性关系** [@problem_id:1978031]：
*   如果 $K > 1$，则 $\ln K > 0$，意味着 $\Delta G^{\circ}  0$ 且 $E^{\circ}_{\text{cell}} > 0$。反应在标准条件下是自发的。
*   如果 $K  1$，则 $\ln K  0$，意味着 $\Delta G^{\circ} > 0$ 且 $E^{\circ}_{\text{cell}}  0$。反应在标准条件下是非自发的。
*   如果 $K = 1$，则 $\ln K = 0$，意味着 $\Delta G^{\circ} = 0$ 且 $E^{\circ}_{\text{cell}} = 0$。反应在标准条件下即处于平衡状态。[@problem_id:1983463]

**定量计算**：
这些关系是进行定量计算的强大工具。例如，对于 $\text{Cu}^+$ 的[歧化反应](@entry_id:138031) $2\text{Cu}^+(\text{aq}) \rightleftharpoons \text{Cu}^{2+}(\text{aq}) + \text{Cu}(s)$，通过组合两个相关的半反应[电势](@entry_id:267554)，可以计算出其 $E^{\circ}_{\text{cell}} = +0.362 \text{ V}$。有了这个值，我们就可以在 $298.15 \text{ K}$ 计算其平衡常数 $K$：
$$ \ln K = \frac{nFE^{\circ}_{\text{cell}}}{RT} = \frac{1 \times 96485 \times 0.362}{8.314 \times 298.15} \approx 14.09 $$
$$ K = \exp(14.09) \approx 1.32 \times 10^6 $$
这个巨大的 $K$ 值表明 $\text{Cu}^+$ 在[水溶液](@entry_id:145101)中是高度不稳定的，会强烈地趋向于歧化。[@problem_id:1995276] 同样，我们也可以从已知的平衡常数出发，通过组合它们的对数（因为 $\Delta G^\circ$ 是可加的）来求得未知反应的 $E^{\circ}_{\text{cell}}$。[@problem_id:1983449]

在实验中，[能斯特方程](@entry_id:146917)的[线性形式](@entry_id:276136) $E_{\text{cell}} = E^{\circ}_{\text{cell}} - (\frac{RT}{nF}) \ln(Q)$ 提供了一种测定这些[热力学](@entry_id:141121)参数的实用方法。如果绘制 $E_{\text{cell}}$ (y轴) 对 $\ln(Q)$ (x轴) 的关系图，应得到一条直线。这条直线的 y-截距（即 $\ln Q = 0$ 或 $Q=1$ 时）就是 $E^{\circ}_{\text{cell}}$，而[直线的斜率](@entry_id:165209)等于 $-\frac{RT}{nF}$，从中可以求出电子转移数 $n$。x-截距（即 $E_{\text{cell}}=0$ 时）则对应于 $\ln K$。[@problem_id:1983480]

### [电池电势的温度依赖性](@entry_id:262824)

电池[电势](@entry_id:267554)并非一个恒定值，它会随温度变化。这种依赖关系蕴含了更丰富的[热力学](@entry_id:141121)信息。从基本的[热力学关系式](@entry_id:139032) $\Delta G^{\circ} = \Delta H^{\circ} - T\Delta S^{\circ}$ 出发，并代入 $\Delta G^{\circ} = -nFE^{\circ}_{\text{cell}}$，我们得到：

$$ -nFE^{\circ}_{\text{cell}} = \Delta H^{\circ} - T\Delta S^{\circ} $$

整理后可得 $E^{\circ}_{\text{cell}}$ 与温度 $T$ 的关系：

$$ E^{\circ}_{\text{cell}} = -\frac{\Delta H^{\circ}}{nF} + \left(\frac{\Delta S^{\circ}}{nF}\right)T $$

如果在一个小温度范围内，$\Delta H^{\circ}$ 和 $\Delta S^{\circ}$ 可以近似看作常数，那么 $E^{\circ}_{\text{cell}}$ 与 $T$呈线性关系。这条线的斜率与标准反应熵变 $\Delta S^{\circ}$ 直接相关，而截距则与[标准反应焓](@entry_id:141844)变 $\Delta H^{\circ}$ 相关。

更普遍地，利用[吉布斯-亥姆霍兹方程](@entry_id:262508)的一个推论，$\Delta S^{\circ} = -(\frac{\partial \Delta G^{\circ}}{\partial T})_P$，我们可以得到熵变与[电势温度系数](@entry_id:266458)之间的精确关系：

$$ \Delta S^{\circ} = - \frac{\partial(-nFE^{\circ}_{\text{cell}})}{\partial T} = nF \left(\frac{\partial E^{\circ}_{\text{cell}}}{\partial T}\right)_P $$

这意味着，通过精确测量[标准电池电势](@entry_id:139386)随温度的变化率，我们就能直接确定该反应的[标准熵变](@entry_id:139601) $\Delta S^{\circ}$。例如，如果一个传感器 cell 的[标准电势](@entry_id:154815)与温度的关系被实验确定为 $E^{\circ}(T) = 1.055 + (5.12 \times 10^{-4}) T$，其中 $n=4$，那么该反应的熵变为 $\Delta S^{\circ} = 4 \times 96485 \text{ C/mol} \times 5.12 \times 10^{-4} \text{ V/K} \approx 198 \text{ J/(mol}\cdot\text{K)}$。[@problem_id:1983486] 一旦通过这种方法确定了 $\Delta S^{\circ}$，就可以利用 $\Delta G^{\circ}$ 和 $\Delta S^{\circ}$ 计算出 $\Delta H^{\circ}$，从而仅通过电化学测量就能获得一个反应的全部关键[热力学状态函数](@entry_id:204381)。同样，一旦 $\Delta H^{\circ}$ 和 $\Delta S^{\circ}$ 已知，便可以计算出任意温度下的 $\Delta G^{\circ}(T)$，进而计算出该温度下的平衡常数 $K(T)$。[@problem_id:2921152]