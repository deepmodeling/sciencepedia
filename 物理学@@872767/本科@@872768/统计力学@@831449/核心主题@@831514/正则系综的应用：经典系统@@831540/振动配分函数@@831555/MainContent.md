## 引言
在分子的微观世界中，原子永不停歇地运动，其中[振动](@entry_id:267781)是其最基本的运动形式之一，深刻影响着物质的宏观性质。然而，经典物理学无法解释为何[固体的热容](@entry_id:144937)在低温下会趋于零，也无法精确描述化学反应的平衡和速率。这揭示了一个知识上的鸿沟：我们如何将原子间化学键的量子化[振动](@entry_id:267781)行为与我们可测量的[热力学](@entry_id:141121)世界联系起来？[振动](@entry_id:267781)[配分函数](@entry_id:193625)正是填补这一鸿沟的核心[统计力](@entry_id:194984)学工具。

本文将系统地引导你掌握[振动](@entry_id:267781)[配分函数](@entry_id:193625)的理论与应用。你将学习到：

*   **原理与机制**：我们将从量子谐振子模型出发，详细推导[振动](@entry_id:267781)[配分函数](@entry_id:193625)的数学表达式，并深入探讨其物理意义、极限行为以及如何用它来计算关键的[热力学函数](@entry_id:755914)。
*   **应用与[交叉](@entry_id:147634)学科联系**：我们将探索[振动](@entry_id:267781)[配分函数](@entry_id:193625)在[光谱学](@entry_id:141940)、固态物理、[化学平衡](@entry_id:142113)与动力学等多个领域的广泛应用，特别是它在解释同位素效应中的关键作用。
*   **动手实践**：通过一系列计算练习，你将把理论知识付诸实践，加深对分子振动如何贡献于系统总能量和热力学性质的理解。

让我们首先进入第一章，深入了解[振动](@entry_id:267781)[配分函数](@entry_id:193625)的构建原理及其基本机制。

## 原理与机制

在上一章中，我们介绍了分子的运动可以被分解为[平动](@entry_id:187700)、转动和[振动](@entry_id:267781)。本章将深入探讨[振动自由度](@entry_id:141707)的[统计力](@entry_id:194984)学处理。我们将以量子谐振子模型为基础，构建[振动](@entry_id:267781)[配分函数](@entry_id:193625)，并揭示它如何将微观的[量子化能级](@entry_id:140911)与宏观的[热力学性质](@entry_id:146047)（如能量、热容和自由能）联系起来。

### 单个谐振子的[振动](@entry_id:267781)[配分函数](@entry_id:193625)

分子中的化学键并非刚性不变，[原子核](@entry_id:167902)会在其[平衡位置](@entry_id:272392)附近进行[振动](@entry_id:267781)。在许多情况下，这种[振动](@entry_id:267781)的势能可以很好地用抛物线来近似，这使得我们可以将分子振动简化为一个或多个**量子谐振子（quantum harmonic oscillator）**。根据量子力学，一个角频率为 $\omega$ 的一维谐振子的能量是量子化的，其能级为：

$E_n = \left(n + \frac{1}{2}\right)\hbar\omega, \quad n = 0, 1, 2, \ldots$

其中 $n$ 是[振动](@entry_id:267781)[量子数](@entry_id:145558)，$\hbar$ 是约化普朗克常数。能量最低的态，即 $n=0$ 的[基态](@entry_id:150928)，其能量为 $E_0 = \frac{1}{2}\hbar\omega$。这被称为**零点能（zero-point energy）**，是量子系统固有的最低能量，即使在绝对零度时也存在。

根据[正则系综](@entry_id:142391)的定义，单个粒子的[配分函数](@entry_id:193625) $z$ 是对所有可能状态的[玻尔兹曼因子](@entry_id:141054) $\exp(-\beta E_n)$ 的求和，其中 $\beta = (k_B T)^{-1}$，$k_B$ 是[玻尔兹曼常数](@entry_id:142384)，$T$ 是[绝对温度](@entry_id:144687)。因此，单个谐振子的完整[振动](@entry_id:267781)[配分函数](@entry_id:193625)为：

$z_{\text{vib,full}} = \sum_{n=0}^{\infty} \exp\left[-\beta E_n\right] = \sum_{n=0}^{\infty} \exp\left[-\beta \left(n + \frac{1}{2}\right)\hbar\omega\right]$

为了简化计算，我们可以将[零点能](@entry_id:142176)的贡献因子 $\exp(-\beta\hbar\omega/2)$ 提出来：

$z_{\text{vib,full}} = \exp\left(-\frac{\beta\hbar\omega}{2}\right) \sum_{n=0}^{\infty} \exp(-\beta n\hbar\omega) = \exp\left(-\frac{\beta\hbar\omega}{2}\right) \sum_{n=0}^{\infty} \left[\exp(-\beta\hbar\omega)\right]^n$

上式中的求和部分是一个[公比](@entry_id:275383)为 $r = \exp(-\beta\hbar\omega)$ 的无穷[几何级数](@entry_id:158490)。由于对于任何正温度 $T \gt 0$，[公比](@entry_id:275383) $r$ 满足 $0 \lt r \lt 1$，级数收敛于 $\frac{1}{1-r}$。因此，

$z_{\text{vib,full}} = \frac{\exp(-\frac{\beta\hbar\omega}{2})}{1 - \exp(-\beta\hbar\omega)}$

在[统计力](@entry_id:194984)学中，我们常常关心的是能量相对于[基态](@entry_id:150928)的变化，因为许多[热力学](@entry_id:141121)量（如内能和热容）都只与能量差有关。因此，一种普遍且方便的做法是选择能量零点，使得基态能量为零。[@problem_id:2015488] 这种约定意味着我们将所有能级都减去[零点能](@entry_id:142176) $E_0$：

$E_n' = E_n - E_0 = \left(n + \frac{1}{2}\right)\hbar\omega - \frac{1}{2}\hbar\omega = n\hbar\omega$

采用这套新的能级，我们得到了常规的**[振动](@entry_id:267781)[配分函数](@entry_id:193625) (vibrational partition function)** [@problem_id:2015502]：

$z_{\text{vib}} = \sum_{n=0}^{\infty} \exp(-\beta E_n') = \sum_{n=0}^{\infty} \exp(-\beta n\hbar\omega) = \frac{1}{1 - \exp(-\beta\hbar\omega)}$

这个表达式简洁明了，是本章后续讨论的基石。需要强调的是，这种能量零点的选择会影响亥姆霍兹自由能 $A = -k_B T \ln Z$ 和化学势等绝对量的值，但对于通过对 $\ln Z$求导得到的量，如内能、熵和[热容](@entry_id:137594)，其结果不受影响。在本书中，除非特别说明，我们将采用以[基态能量](@entry_id:263704)为零点的常规[振动](@entry_id:267781)[配分函数](@entry_id:193625)。

### [配分函数](@entry_id:193625)的物理意义

[振动](@entry_id:267781)[配分函数](@entry_id:193625) $z_{\text{vib}}$ 不仅仅是一个数学表达式，它具有深刻的物理意义：**它衡量了在给定温度下，分子[热力学](@entry_id:141121)上可及的振动能级的有效数目**。

当温度极低时 ($T \to 0$, $\beta \to \infty$)，指数项 $\exp(-\beta\hbar\omega) \to 0$，因此 $z_{\text{vib}} \to 1$。这表明，在低温下，几乎所有的分子都处于[振动](@entry_id:267781)[基态](@entry_id:150928) ($n=0$)，只有最低的能级是可及的。

随着温度升高，$\exp(-\beta\hbar\omega)$ 的值增大，分母 $1 - \exp(-\beta\hbar\omega)$ 减小，导致 $z_{\text{vib}}$ 增大。这意味着有更多的热能可以用来激发分子到更高的振动能级 ($n=1, 2, \ldots$)，因此可及的能级数目增加。

除了温度，[振动频率](@entry_id:199185) $\omega$ 也是决定[配分函数](@entry_id:193625)大小的关键因素。在相同温度下，分子的[振动频率](@entry_id:199185)越高，相邻能级之间的能量间隔 $\Delta E = \hbar\omega$ 就越大。要布居这些高能级就需要更多的能量。因此，**频率越高，在给定温度下可及的能级数就越少，[振动](@entry_id:267781)[配分函数](@entry_id:193625)也就越小**。[@problem_id:2015524]

这个原理可以通过一个具体的例子来加深理解。考虑在室温（$T = 300 \, \text{K}$）下，氢气分子 ($\text{H}_2$) 和[碘](@entry_id:148908)分子 ($\text{I}_2$) 的[振动](@entry_id:267781)行为。$\text{H}_2$ 的[振动频率](@entry_id:199185)非常高（[波数](@entry_id:172452) $\tilde{\nu}_{\text{H}_2} = 4401 \, \text{cm}^{-1}$），而 $\text{I}_2$ 的键相对较弱，原子质量大，[振动频率](@entry_id:199185)低得多（$\tilde{\nu}_{\text{I}_2} = 214.5 \, \text{cm}^{-1}$）。我们可以计算相应的能量间隔与热能 $k_B T$ 的比值 $x = \frac{hc\tilde{\nu}}{k_B T}$（其中 $c$ 是光速）。计算表明，对于 $\text{H}_2$，$x_{\text{H}_2} \approx 21.1$，而对于 $\text{I}_2$，$x_{\text{I}_2} \approx 1.03$。[@problem_id:2023579]

-   对于 $\text{H}_2$，$z_{\text{vib, H}_2} = \frac{1}{1 - \exp(-21.1)} \approx 1.000000007$，这几乎等于 1。这表明在室温下，$\text{H}_2$ 分子几乎全部处于其[振动](@entry_id:267781)[基态](@entry_id:150928)，其[振动](@entry_id:267781)模式被“冻结”了。

-   对于 $\text{I}_2$，$z_{\text{vib, I}_2} = \frac{1}{1 - \exp(-1.03)} \approx 1.56$。这个值显著大于 1，说明除了[基态](@entry_id:150928)之外，第一[激发态](@entry_id:261453)甚至更高能级也有不可忽略的布居。

这个对比鲜明地说明了[振动频率](@entry_id:199185)如何影响[热力学](@entry_id:141121)行为。同样，比较含有 $\text{C-H}$ 键和 $\text{C-D}$ 键（[氘](@entry_id:194706)是氢的同位素）的分子时，由于[氘](@entry_id:194706)的质量更大，$\text{C-D}$ 键的[振动频率](@entry_id:199185) $\omega_{\text{CD}}$ 低于 $\text{C-H}$ 键的 $\omega_{\text{CH}}$。因此，在相同温度下，$\text{C-D}$ 键的[振动](@entry_id:267781)[配分函数](@entry_id:193625) $q_{\text{CD}}$ 将大于 $\text{C-H}$ 键的 $q_{\text{CH}}$。[@problem_id:2015524]

为了更方便地判断温度对[振动](@entry_id:267781)的影响，我们常定义一个**[特征振动温度](@entry_id:153344) (characteristic vibrational temperature)** $\Theta_{\text{vib}}$：

$\Theta_{\text{vib}} = \frac{\hbar\omega}{k_B} = \frac{hc\tilde{\nu}}{k_B}$

$\Theta_{\text{vib}}$ 代表了振动能级间隔与热能相当的温度尺度。[振动](@entry_id:267781)[配分函数](@entry_id:193625)可以写成 $z_{\text{vib}} = \frac{1}{1 - \exp(-\Theta_{\text{vib}}/T)}$。
-   当 $T \ll \Theta_{\text{vib}}$ 时，[振动](@entry_id:267781)被冻结，$z_{\text{vib}} \approx 1$。
-   当 $T \gg \Theta_{\text{vib}}$ 时，许多[振动能级](@entry_id:193001)被布居，$z_{\text{vib}} \gt 1$。

例如，$\text{H}_2$ 的 $\Theta_{\text{vib}} \approx 6300 \, \text{K}$，远高于室温；而 $\text{I}_2$ 的 $\Theta_{\text{vib}} \approx 308 \, \text{K}$，与室温相当。

### 极限情况：[经典极限](@entry_id:148587)

在高温极限下，即 $k_B T \gg \hbar\omega$ 或 $T \gg \Theta_{\text{vib}}$，热能远大于振动能级间隔。此时 $\beta\hbar\omega \ll 1$。我们可以对[指数函数](@entry_id:161417)进行[泰勒展开](@entry_id:145057) $\exp(-x) \approx 1 - x$（对于小 $x$）。将此应用于[振动](@entry_id:267781)[配分函数](@entry_id:193625)的分母：[@problem_id:2015507]

$z_{\text{vib}} = \frac{1}{1 - \exp(-\beta\hbar\omega)} \approx \frac{1}{1 - (1 - \beta\hbar\omega)} = \frac{1}{\beta\hbar\omega} = \frac{k_B T}{\hbar\omega}$

这被称为[振动](@entry_id:267781)[配分函数](@entry_id:193625)的**[经典极限](@entry_id:148587)**。在这个极限下，能级间隔相对于热能可以忽略不计，量子效应变得不重要，系统的行为趋向于[经典谐振子](@entry_id:153404)。值得注意的是，[配分函数](@entry_id:193625)与温度成正比，这与[平动配分函数](@entry_id:136950)类似。

### 从[配分函数](@entry_id:193625)到热力学性质

[振动](@entry_id:267781)[配分函数](@entry_id:193625)是连接微观世界和宏观热力学性质的桥梁。一旦我们得到了 $z_{\text{vib}}$，就可以推导出一系列重要的[热力学](@entry_id:141121)量。

#### 亥姆霍兹自由能

对于一个由 $N$ 个可分辨的、独立的谐振子组成的系统（例如[晶格](@entry_id:196752)中的原子），总的[振动](@entry_id:267781)[配分函数](@entry_id:193625) $Z_{\text{vib}}$ 是单个[配分函数](@entry_id:193625)的 $N$ 次方：

$Z_{\text{vib}} = (z_{\text{vib}})^N$

[振动](@entry_id:267781)对亥姆霍兹自由能 $A_{\text{vib}}$ 的贡献可以通过基本关系式 $A = -k_B T \ln Z$ 得到：[@problem_id:2015504]

$A_{\text{vib}} = -k_B T \ln Z_{\text{vib}} = -k_B T \ln (z_{\text{vib}}^N) = -N k_B T \ln z_{\text{vib}}$

将 $z_{\text{vib}}$ 的表达式代入，得到：

$A_{\text{vib}} = -N k_B T \ln \left(\frac{1}{1 - \exp(-\beta\hbar\omega)}\right) = N k_B T \ln(1 - \exp(-\beta\hbar\omega))$

如果我们使用包含零点能的[配分函数](@entry_id:193625) $z_{\text{vib,full}}$，则自由能中还会包含一项总的零点能 $N \cdot \frac{1}{2}\hbar\omega$。

#### 平均振动能

系统的[平均能量](@entry_id:145892) $U$ (或 $\langle E \rangle$) 可以通过对[总配分函数](@entry_id:190183) $Z$ 的对数求导得到：$U = -\left(\frac{\partial \ln Z}{\partial \beta}\right)_V$。为了得到包含零点能的完整[平均能量](@entry_id:145892)，我们必须使用 $z_{\text{vib,full}}$。对于单个[振子](@entry_id:271549)：

$\ln z_{\text{vib,full}} = -\frac{\beta\hbar\omega}{2} - \ln(1 - \exp(-\beta\hbar\omega))$

对其求导：[@problem_id:1901692]

$\langle E_{\text{vib}} \rangle = -\frac{\partial}{\partial \beta} \ln z_{\text{vib,full}} = -\left[ -\frac{\hbar\omega}{2} - \frac{\hbar\omega \exp(-\beta\hbar\omega)}{1 - \exp(-\beta\hbar\omega)} \right]$

$\langle E_{\text{vib}} \rangle = \frac{\hbar\omega}{2} + \frac{\hbar\omega \exp(-\beta\hbar\omega)}{1 - \exp(-\beta\hbar\omega)}$

通过分子分母同乘以 $\exp(\beta\hbar\omega)$，上式可以写成更常见的形式：

$\langle E_{\text{vib}} \rangle = \frac{\hbar\omega}{2} + \frac{\hbar\omega}{\exp(\beta\hbar\omega) - 1}$

这个表达式非常重要。第一项 $\frac{1}{2}\hbar\omega$ 是与温度无关的零点能。第二项是随温度变化的**[热激发](@entry_id:275697)能**，它描述了系统因热搅动而获得的超越[零点能](@entry_id:142176)的平均能量。

在高温[经典极限](@entry_id:148587)下 ($k_B T \gg \hbar\omega$, $\beta\hbar\omega \ll 1$)，我们利用泰勒展开 $\exp(x) \approx 1 + x$，得到：

$\langle E_{\text{vib}} \rangle \approx \frac{\hbar\omega}{2} + \frac{\hbar\omega}{(1 + \beta\hbar\omega) - 1} = \frac{\hbar\omega}{2} + \frac{1}{\beta} = \frac{\hbar\omega}{2} + k_B T$

除去[零点能](@entry_id:142176)后，平均热能为 $k_B T$。这精确地符合了经典**[能量均分定理](@entry_id:136972)**：每个二次方的能量项（谐振子的动能和[势能](@entry_id:748988)各一个）在[热平衡](@entry_id:141693)时平均贡献 $\frac{1}{2}k_B T$ 的能量，总共为 $k_B T$。

#### [振动热容](@entry_id:151645)

恒容[热容](@entry_id:137594) $C_V$ 定义为内能在恒定体积下对温度的导数，$C_{V,\text{vib}} = \left(\frac{\partial U_{\text{vib}}}{\partial T}\right)_V$。对于由 $N$ 个独立一维谐振子组成的系统，总能量为 $U_{\text{vib}} = N \langle E_{\text{vib}} \rangle$。求导时，零点能项是常数，没有贡献。我们利用[链式法则](@entry_id:190743) $\frac{\partial}{\partial T} = \frac{\partial \beta}{\partial T} \frac{\partial}{\partial \beta} = -\frac{1}{k_B T^2} \frac{\partial}{\partial \beta}$：[@problem_id:2015492]

$C_{V,\text{vib}} = N \frac{\partial}{\partial T} \left[ \frac{\hbar\omega}{\exp(\beta\hbar\omega) - 1} \right] = N \left(-\frac{1}{k_B T^2}\right) \frac{\partial}{\partial \beta} \left[ \frac{\hbar\omega}{\exp(\beta\hbar\omega) - 1} \right]$

$C_{V,\text{vib}} = N \left(-\frac{1}{k_B T^2}\right) \left[ -\frac{(\hbar\omega)^2 \exp(\beta\hbar\omega)}{(\exp(\beta\hbar\omega) - 1)^2} \right]$

整理后得到**爱因斯坦[热容](@entry_id:137594)公式**：

$C_{V,\text{vib}} = N k_B \left(\frac{\hbar\omega}{k_B T}\right)^2 \frac{\exp(\hbar\omega/k_B T)}{[\exp(\hbar\omega/k_B T) - 1]^2} = N k_B \left(\frac{\Theta_{\text{vib}}}{T}\right)^2 \frac{\exp(\Theta_{\text{vib}}/T)}{[\exp(\Theta_{\text{vib}}/T) - 1]^2}$

这个公式完美地解释了固体热容的实验行为：
-   在高温极限 ($T \gg \Theta_{\text{vib}}$)下，$C_{V,\text{vib}} \to N k_B$。对于三维晶体中的原子，每个原子有三个[振动自由度](@entry_id:141707)，所以总热容趋近于 $3N k_B$，这正是经典的**[杜隆-珀蒂定律](@entry_id:191078)**。
-   在低温极限 ($T \ll \Theta_{\text{vib}}$)下，指数项远大于1，热容以指数形式趋于零 $C_{V,\text{vib}} \to 0$。这成功地解释了[经典物理学](@entry_id:150394)无法解释的现象——[热容](@entry_id:137594)在低温下会消失。

### 推广至[多原子分子](@entry_id:268323)

对于包含 $N_{atoms}$ 个原子的分子，其复杂的[振动](@entry_id:267781)可以被分解为一组独立的**简正模式 (normal modes)**，每一种模式都表现为一个具有特定频率 $\omega_i$ 的谐振子。
-   对于一个[非线性分子](@entry_id:175085)，有 $3N_{atoms}-6$ 个[振动简正模](@entry_id:141283)式。
-   对于一个[线性分子](@entry_id:166760)，有 $3N_{atoms}-5$ 个[振动简正模](@entry_id:141283)式。

由于这些简正模式是相互独立的，系统的总[振动](@entry_id:267781)[哈密顿量](@entry_id:172864)是各个模式[哈密顿量](@entry_id:172864)的和，这意味着总能量是各个模式能量的和 $E_{\text{total}} = \sum_i E_i$。[统计力](@entry_id:194984)学的一个基本原理是，当系统的能量可以表示为独立子系统的能量之和时，其[总配分函数](@entry_id:190183)就是各子系统[配分函数](@entry_id:193625)的乘积。[@problem_id:2015533]

因此，[多原子分子](@entry_id:268323)的总[振动](@entry_id:267781)[配分函数](@entry_id:193625)是其所有[简正模](@entry_id:139640)式[配分函数](@entry_id:193625)的乘积：

$Z_{\text{vib,total}} = \prod_i z_{\text{vib},i} = \prod_i \frac{1}{1 - \exp(-\beta\hbar\omega_i)}$

同样，总平均振动能和总[振动热容](@entry_id:151645)也是各个模式贡献的加和：

$U_{\text{vib,total}} = \sum_i \langle E_{\text{vib},i} \rangle = \sum_i \left( \frac{\hbar\omega_i}{2} + \frac{\hbar\omega_i}{\exp(\beta\hbar\omega_i) - 1} \right)$

$C_{V,\text{vib,total}} = \sum_i C_{V,\text{vib},i}$

在处理[多原子分子](@entry_id:268323)时，必须注意**简并度 (degeneracy)**。如果某个频率 $\omega_j$ 对应于 $d_j$ 个独立的简正模式（即 $d_j$ 重简并），那么在计算[总配分函数](@entry_id:190183)时，该模式的因子需要计为 $(z_{\text{vib},j})^{d_j}$；在计算总能量或热容时，该模式的贡献需要乘以 $d_j$。

例如，一个线性的[三原子分子](@entry_id:155569)（如 $\text{CO}_2$），有 $3 \times 3 - 5 = 4$ 个[振动](@entry_id:267781)模式。它们分别是：对称伸缩（频率 $\omega_s$），反[对称伸缩](@entry_id:165187)（频率 $\omega_a$），以及一个双重简并的弯曲模式（频率 $\omega_b$）。因此，其总平均振动能（除去零点能）为：[@problem_id:2015508]

$U_{\text{vib,total}} = \frac{\hbar\omega_s}{\exp(\beta\hbar\omega_s) - 1} + \frac{\hbar\omega_a}{\exp(\beta\hbar\omega_a) - 1} + \frac{2\hbar\omega_b}{\exp(\beta\hbar\omega_b) - 1}$

使用[特征振动温度](@entry_id:153344) $\Theta_i = \hbar\omega_i/k_B$ 表示则为：

$U_{\text{vib,total}} = k_B \left( \frac{\Theta_s}{\exp(\Theta_s/T) - 1} + \frac{\Theta_a}{\exp(\Theta_a/T) - 1} + \frac{2\Theta_b}{\exp(\Theta_b/T) - 1} \right)$

这个框架为计算任何分子的[振动](@entry_id:267781)[热力学性质](@entry_id:146047)提供了一个强大而系统的方法，只需知道其简正模式的[振动频率](@entry_id:199185)即可。