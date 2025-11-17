## 引言
在[多相催化](@entry_id:139401)领域，催化剂表面的分子转化过程既复杂又迷人。为了从根本上理解并优化这些[化学反应](@entry_id:146973)，建立能够准确描述其内在规律的动力学模型至关重要。这些模型不仅是连接微观分子事件与宏观[反应速率](@entry_id:139813)的桥梁，也是理性设计高效催化剂的理论基石。然而，一个核心的知识挑战在于，如何区分和量化反应物在表面发生反应的不同基本路径。最经典的两种[范式](@entry_id:161181)——Langmuir-Hinshelwood (LH) 和 Eley-Rideal (ER) 机理——为解决这一问题提供了基本框架，但它们的适用性与甄别方法仍是催化研究中的关键课题。

本文将系统地引导您深入探索这两种核心的[表面催化](@entry_id:161295)机理。在“原理与机制”一章中，我们将从[Langmuir吸附](@entry_id:152394)模型出发，详细推导LH和ER机理的速率方程，并分析它们的动力学特征。随后的“应用与跨学科联系”一章，将聚焦于如何运用原位[光谱](@entry_id:185632)、瞬态动力学等现代实验技术来甄别这些机理，并探讨[产物抑制](@entry_id:166965)、[传质限制](@entry_id:148929)等真实世界的复杂性。最后，通过“动手实践”部分，您将有机会应用所学知识解决具体的动力学问题。通过这一学习路径，您将构建起一个从基本原理到实际应用的完整知识体系，为深入研究[表面催化](@entry_id:161295)现象打下坚实的基础。

## 原理与机制

在理解[多相催化](@entry_id:139401)的复杂[世界时](@entry_id:275204)，建立能够捕捉[表面过程](@entry_id:192310)本质的动力学模型至关重要。这些模型不仅提供了描述[反应速率](@entry_id:139813)如何随反应物浓度和温度变化的数学框架，还揭示了潜在的分子层面的相互作用。本章将系统地阐述两个基本的[多相催化](@entry_id:139401)机制：Langmuir-Hinshelwood (LH) 机制和 Eley-Rideal (ER) 机制。我们将从吸附的基本原理出发，逐步构建这些模型的速率表达式，并深入探讨如何通过分析反应动力学来区分它们。

### 吸附平衡：Langmuir 模型及其扩展

催化反应的第一步通常是反应物分子在催化剂表面的吸附。因此，对吸附过程的定量描述是所有[表面动力学](@entry_id:185097)模型的基础。

#### 单组分 Langmuir [吸附等温线](@entry_id:153357)

最基本且应用最广泛的[吸附模型](@entry_id:184889)是 **Langmuir [吸附模型](@entry_id:184889)**。该模型基于几个核心假设：(1) 催化剂表面拥有固定数量的、性质完全相同的吸附位点；(2) 每个位点最多只能吸附一个分子，形成[单层吸附](@entry_id:197714)；(3) 所有位点的吸附能相同，且吸附的分子之间没有相互作用；(4) 吸附是一个[动态平衡](@entry_id:136767)过程。

考虑一个气相物质 $A$ 在表面上的[非解离吸附](@entry_id:195696)过程，其基元步骤可以表示为：
$$ A(\mathrm{g}) + * \rightleftharpoons A* $$
其中 $*$ 代表一个空的表面位点，$A*$ 代表一个被 $A$ 分子占据的位点。

根据动力学原理，吸附速率 $r_{\mathrm{ads}}$ 正比于气相分子 $A$ 的压力 $P_A$ 和空位点的分数（覆盖度） $1-\theta_A$。[脱附速率](@entry_id:186413) $r_{\mathrm{des}}$ 则正比于已被占据位点的分数 $\theta_A$。
$$ r_{\mathrm{ads}} = k_{\mathrm{ads}} P_A (1 - \theta_A) $$
$$ r_{\mathrm{des}} = k_{\mathrm{des}} \theta_A $$
在[动态平衡](@entry_id:136767)时，吸附速率等于[脱附速率](@entry_id:186413)，$r_{\mathrm{ads}} = r_{\mathrm{des}}$。由此可得：
$$ k_{\mathrm{ads}} P_A (1 - \theta_A) = k_{\mathrm{des}} \theta_A $$
整理此方程，我们可以解出[表面覆盖度](@entry_id:202248) $\theta_A$ 作为压力 $P_A$ 的函数：
$$ \theta_A = \frac{K_A P_A}{1 + K_A P_A} $$
这就是著名的 **Langmuir [吸附等温线](@entry_id:153357)**，其中 $K_A = k_{\mathrm{ads}}/k_{\mathrm{des}}$ 是吸附[平衡常数](@entry_id:141040)，它反映了物质 $A$ 在该表面上吸附能力的强弱。

分析 Langmuir [等温线](@entry_id:151893)的极限行为对于理解[表面动力学](@entry_id:185097)至关重要 [@problem_id:2669635]。
在 **低压（或低覆盖度）极限**下，即 $K_A P_A \ll 1$，分母中的 $K_A P_A$ 项可以忽略不计。此时，[等温线](@entry_id:151893)简化为：
$$ \theta_A \approx K_A P_A $$
这表明在低覆盖度下，[表面覆盖度](@entry_id:202248)与气体压力成正比，这被称为**亨利定律 (Henry's Law)** 区。这个线性近似的有效性取决于无量纲乘积 $K_A P_A$ 远小于 1，而不仅仅是压力 $P_A$ 本身足够小。

在 **高压（或高覆盖度）极限**下，即 $K_A P_A \gg 1$，分母中的 1 可以忽略。此时：
$$ \theta_A \approx \frac{K_A P_A}{K_A P_A} = 1 $$
这表明在高压下，表面几乎被吸附物完全覆盖，达到了饱和，即 $\theta_A \to 1$。此时，覆盖度对压力的变化不再敏感。

#### 竞争吸附

在多组分反应体系中，不同种类的分子会争夺有限的表面位点。这种**竞争吸附**是 Langmuir-Hinshelwood 机制的核心特征。假设有两种[非解离吸附](@entry_id:195696)的物质 $A$ 和 $B$，它们的吸附平衡分别为：
$$ A(\mathrm{g}) + * \rightleftharpoons A* \quad \text{平衡常数 } K_A $$
$$ B(\mathrm{g}) + * \rightleftharpoons B* \quad \text{平衡常数 } K_B $$
空位点的分数现在是 $\theta_* = 1 - \theta_A - \theta_B$。通过建立两种物质各自的吸附-[脱附](@entry_id:186847)平衡，我们可以推导出它们在[竞争条件](@entry_id:177665)下的覆盖度 [@problem_id:2669668]：
$$ \theta_A = K_A P_A \theta_* $$
$$ \theta_B = K_B P_B \theta_* $$
将这两个表达式代入位点守恒方程 $1 = \theta_A + \theta_B + \theta_*$ 中，解得空位点的覆盖度：
$$ \theta_* = \frac{1}{1 + K_A P_A + K_B P_B} $$
最后，我们可以得到每种物质的覆盖度表达式：
$$ \theta_A = \frac{K_A P_A}{1 + K_A P_A + K_B P_B} $$
$$ \theta_B = \frac{K_B P_B}{1 + K_A P_A + K_B P_B} $$
这些方程清楚地表明，一种物质的覆盖度不仅取决于其自身的分压，还反过来取决于竞争吸附物的分压和吸附能力。一种强吸附物质的存在会显著降低另一种弱吸附物质的[表面覆盖度](@entry_id:202248)。

#### 超越理想模型：考虑横向相互作用

Langmuir 模型的“无相互作用”假设在许多真实体系中并不成立。吸附的分子之间可能存在吸引或排斥力，即**横向相互作用**。在平均场近似下，我们可以考虑一个吸附分子与其 $z$ 个最近邻分子之间的平均[相互作用能](@entry_id:264333) $zw\theta$（其中 $w$ 为[相互作用能](@entry_id:264333)，$w > 0$ 表示排斥，$w  0$ 表示吸引）。这导致了 **Fowler-Guggenheim (或 Frumkin) [等温线](@entry_id:151893)** [@problem_id:2669676]：
$$ \frac{\theta}{1-\theta} = K P \exp\left(-\frac{z w \theta}{k_B T}\right) $$
指数项 $\exp(-zw\theta/k_B T)$ 描述了相互作用对吸附平衡的影响。排斥作用 ($w>0$) 会使有效吸附常数随覆盖度的增加而减小，从而抑制进一步的吸附。相反，吸引作用 ($w0$) 则会促进吸附，可能导致表面发生二维凝聚现象。

### 核心催化机制：Langmuir-Hinshelwood 与 Eley-Rideal

基于对吸附的理解，我们现在可以构建两种最基本的双分子[表面催化](@entry_id:161295)[反应机制](@entry_id:149504)。

#### Langmuir-Hinshelwood (LH) 机制

在 **Langmuir-Hinshelwood (LH) 机制**中，反应发生在两个都已化学吸附在催化剂表面的物种之间。对于一个典型的[双分子反应](@entry_id:165027) $A+B \to P$，其 LH 路径包括以下步骤：
1.  $A$ 的吸附：$A(\mathrm{g}) + * \rightleftharpoons A*$
2.  $B$ 的吸附：$B(\mathrm{g}) + * \rightleftharpoons B*$
3.  表面反应（速率决定步骤, RDS）：$A* + B* \to P(\mathrm{g}) + 2*$

[反应速率](@entry_id:139813)正比于表面上 $A*$ 和 $B*$ 的覆盖度的乘积：
$$ r_{LH} = k \theta_A \theta_B $$
其中 $k$ 是[表面反应](@entry_id:183202)的[速率常数](@entry_id:196199)。将前面推导的竞争吸附覆盖度表达式代入，我们得到 LH 机制的完整速率方程：
$$ r_{LH} = \frac{k K_A K_B P_A P_B}{(1 + K_A P_A + K_B P_B)^2} $$
这个方程形式复杂，但蕴含了丰富的动力学行为。

#### Eley-Rideal (ER) 机制

与 LH 机制不同，**Eley-Rideal (ER) 机制**涉及一个气相分子直接与一个已吸附的物种发生反应。对于同一个反应 $A+B \to P$，如果 $B$ 吸附而 $A$ 不吸附，其 ER 路径为：
1.  $B$ 的吸附：$B(\mathrm{g}) + * \rightleftharpoons B*$
2.  表面反应（速率决定步骤, RDS）：$A(\mathrm{g}) + B* \to P(\mathrm{g}) + *$

[反应速率](@entry_id:139813)正比于[气相反应](@entry_id:169269)物 $A$ 的分压 $P_A$ 和已吸附物种 $B*$ 的覆盖度 $\theta_B$：
$$ r_{ER} = k' P_A \theta_B $$
在此机制中，只有 $B$ 参与吸附平衡。因此，$\theta_B$ 服从单组分 Langmuir [等温线](@entry_id:151893)（假设产物或其他惰性物质不吸附）：
$$ \theta_B = \frac{K_B P_B}{1 + K_B P_B} $$
代入速率表达式，得到 ER 机制的完整速率方程：
$$ r_{ER} = \frac{k' K_B P_A P_B}{1 + K_B P_B} $$
ER 机制的[速率方程](@entry_id:198152)在形式上比 LH 机制的方程更简单，这导致了它们截然不同的动力学特征。

### 动力学分析与机制甄别

通过测量[反应速率](@entry_id:139813)如何随反应物[分压](@entry_id:168927)变化，我们可以获得关于[反应级数](@entry_id:142981)的信息，从而为判断潜在的反应机制提供有力证据。

#### [表观反应级数](@entry_id:154795)分析

**[表观反应级数](@entry_id:154795)**被定义为 $n_i = (\partial \ln r / \partial \ln P_i)_{T, P_{j \ne i}}$，它描述了在[其他条件不变](@entry_id:637315)时，[反应速率](@entry_id:139813)对某一组分分压的敏感度。

对于 **Langmuir-Hinshelwood 机制**，其反应级数随覆盖度的变化而显著改变 [@problem_id:2669654] [@problem_id:2669666]：
*   **低覆盖度极限** ($K_A P_A \ll 1$ 且 $K_B P_B \ll 1$)：此时分母近似为 1，$r_{LH} \approx k K_A K_B P_A P_B$。反应对 $A$ 和 $B$ 都是一级，即 $n_A = 1, n_B = 1$。这对应于一个大部分为空的表面，速率由反应物到达并吸附的频率决定。
*   **单一组分高覆盖度极限** (例如，$A$ 强吸附且高压，$K_A P_A \gg 1+K_B P_B$)：此时表面几乎被 $A$ 占据，$\theta_A \approx 1$。$B$ 的吸附则受到空位点稀缺的限制，$\theta_B = K_B P_B \theta_* \approx K_B P_B / (K_A P_A)$。速率表达式近似为 $r_{LH} \approx k \cdot 1 \cdot \frac{K_B P_B}{K_A P_A}$。此时，反应级数变为 $n_A = -1$ 和 $n_B = 1$。$A$ 的表观级数为负一，这是一种**[自抑制](@entry_id:169700)效应**：增加 $P_A$ 会进一步挤占 $B$ 的吸附位点，反而导致总[反应速率](@entry_id:139813)下降。这种负级数是 LH 机制在高覆盖度下的一个标志性特征。

对于 **Eley-Rideal 机制**，动力学行为则有所不同 [@problem_id:2669666]：
*   对于[气相反应](@entry_id:169269)物 $A$，速率 $r_{ER}$ 总是正比于 $P_A$，因此其[表观反应级数](@entry_id:154795)始终为 $n_A = 1$（在最简单的模型中）。
*   对于吸附的反应物 $B$，其级数随 $P_B$ 的变化而变化：
    *   在低 $P_B$ ($K_B P_B \ll 1$) 时，$\theta_B \approx K_B P_B$，所以 $r_{ER} \propto P_A P_B$，级数 $n_B=1$。
    *   在高 $P_B$ ($K_B P_B \gg 1$) 时，表面被 $B$ 饱和，$\theta_B \approx 1$，所以 $r_{ER} \propto P_A$，级数 $n_B=0$。速率不再依赖于 $P_B$ 的变化。

总结来说，ER 机制永远不会对任何反应物表现出负的[反应级数](@entry_id:142981)，而 LH 机制则会在高覆盖度下因竞争吸附而表现出负级数。

#### 基于动力学实验的机制甄别

这些独特的动力学特征为实验上区分 LH 和 ER 机制提供了可能。一个经典的思想实验是：在一个反应物（如 $B$）的分压很高以至于表面被其饱和的条件下，测量[反应速率](@entry_id:139813)随另一个反应物（$A$）分压的变化 [@problem_id:2669661]。
*   如果反应遵循 **ER 机制** ($A(g) + B* \to P$)：由于 $\theta_B$ 在 $B$ 饱和的条件下近似为常数 1，速率 $r_{ER} = k' P_A \theta_B \approx k' P_A$。因此，初始速率 $r_0$ 与 $P_A$ 应呈现**[线性关系](@entry_id:267880)**。
*   如果反应遵循 **LH 机制** ($A* + B* \to P$)：在 $P_B$ 固定的高压条件下，速率表达式为 $r_{LH} = \frac{(\text{常数}) \cdot P_A}{(\text{另一常数} + K_A P_A)^2}$。速率与 $P_A$ 的关系是**亚线性的**（sublinear）。随着 $P_A$ 的增加，速率起初上升，但由于 $A*$ 对 $B*$ 的竞争性取代，速率会达到一个最大值然后下降。

因此，通过观察速率对 $P_A$ 的响应是线性的还是[非线性](@entry_id:637147)的（弯曲的），我们就能有力地推断反应是更倾向于 ER 机制还是 LH 机制。

### 温度依赖性与活化能

温度是影响催化[反应速率](@entry_id:139813)的另一个关键参数。通过研究速率的[温度依赖性](@entry_id:147684)，我们可以获得关于[反应能](@entry_id:143747)垒和[吸附热](@entry_id:199302)力学的重要信息。

#### [吸附热](@entry_id:199302)力学参数的测定

吸附[平衡常数](@entry_id:141040) $K$ 的温度依赖性由 **van 't Hoff 方程**描述：
$$ \ln K = -\frac{\Delta G_{\text{ads}}^{\circ}}{RT} = -\frac{\Delta H_{\text{ads}}^{\circ}}{RT} + \frac{\Delta S_{\text{ads}}^{\circ}}{R} $$
其中 $\Delta H_{\text{ads}}^{\circ}$ 和 $\Delta S_{\text{ads}}^{\circ}$ 分别是标准[吸附焓](@entry_id:171774)和标准吸附熵。实验上，我们可以通过在多个温度下测量 Langmuir [吸附等温线](@entry_id:153357)来确定这些参数 [@problem_id:2669611]。具体步骤如下：
1.  在每个温度 $T$下，测量一系列 $(P_A, \theta_A)$ 数据。
2.  对 Langmuir 方程进行线性化，例如，绘制 $\frac{\theta_A}{1 - \theta_A}$ 对 $P_A$ 的图。该图的斜率即为吸附[平衡常数](@entry_id:141040) $K_p(T)$。
3.  获得一系列不同温度下的 $K_p(T)$ 值后，绘制 $\ln K_p(T)$ 对 $1/T$ 的图（van 't Hoff 图）。
4.  该图的斜率为 $-\Delta H_{\text{ads}}^{\circ}/R$，截距为 $\Delta S_{\text{ads}}^{\circ}/R + \ln(P^\circ)$（如果使用有量纲的 $K_p$），由此即可求出[吸附焓](@entry_id:171774)和吸附熵。通常，[化学吸附](@entry_id:149998)是[放热过程](@entry_id:147168)，因此 $\Delta H_{\text{ads}}^{\circ}$ 为负值。

#### [表观活化能](@entry_id:186705)

对于一个复杂的[表面催化](@entry_id:161295)反应，实验测得的**[表观活化能](@entry_id:186705) ($E_{\text{app}}$)** 是一个复合量，它不仅包含了表面[基元反应](@entry_id:177550)步骤的真实能垒，还包含了反应物[表面覆盖度](@entry_id:202248)随温度变化的贡献。$E_{\text{app}}$ 由总包[反应速率](@entry_id:139813) $r$ 的温度依赖性定义：
$$ E_{\text{app}} \equiv -R \frac{\partial \ln r}{\partial(1/T)}\Bigg|_{P_A, P_B} $$
对于 **ER 机制** ($A(g) + B* \to P$)，其[表观活化能](@entry_id:186705)的表达式可以推导为 [@problem_id:2669649]：
$$ E_{\text{app}} = E_{\text{ER}} + \frac{\Delta H_{\text{ads}, B}}{1 + K_B P_B} $$
其中 $E_{\text{ER}}$ 是表面反应的真实活化能，$\Delta H_{\text{ads}, B}$ 是 $B$ 的[吸附焓](@entry_id:171774)。
*   在低覆盖度极限 ($K_B P_B \ll 1$)， $E_{\text{app}} \approx E_{\text{ER}} + \Delta H_{\text{ads}, B}$。由于吸附通常是放热的 ($\Delta H_{\text{ads}, B}  0$)，[表观活化能](@entry_id:186705)会低于真实活化能。这是因为升温虽然加速了表面反应，但也降低了反应物 $B$ 的覆盖度（Le Châtelier 原理），这两个效应部分抵消。
*   在高覆盖度极限 ($K_B P_B \gg 1$)，表面被 $B$ 饱和，$\theta_B \approx 1$。此时 $E_{\text{app}} \approx E_{\text{ER}}$。[表观活化能](@entry_id:186705)等于真实活化能，因为此时覆盖度不再随温度变化。

对于 **LH 机制** ($A* + B* \to P$)，[表观活化能](@entry_id:186705)的表达式更为复杂 [@problem_id:2669662]：
$$ E_{\text{app}} = E_a + \Delta H_A + \Delta H_B - 2 \frac{K_A P_A \Delta H_A + K_B P_B \Delta H_B}{1 + K_A P_A + K_B P_B} $$
其中 $E_a$ 是表面反应的真实活化能，$\Delta H_A$ 和 $\Delta H_B$ 分别是 $A$ 和 $B$ 的[吸附焓](@entry_id:171774)。这个表达式表明，对于 LH 机制，$E_{\text{app}}$ 不是一个常数，它强烈地依赖于反应条件（压力和温度），因为它取决于[表面覆盖度](@entry_id:202248)。

#### [活化熵](@entry_id:169746)与[指前因子](@entry_id:145277)

根据过渡态理论，速率常数 $k$ 不仅取决于[活化焓](@entry_id:167343)（能垒），还取决于**[活化熵](@entry_id:169746) ($\Delta S^{\ddagger}$)**：
$$ k = \frac{k_B T}{h} \exp\left(\frac{\Delta S^{\ddagger}}{R}\right) \exp\left(-\frac{\Delta H^{\ddagger}}{RT}\right) $$
[活化熵](@entry_id:169746)反映了从反应物到过渡态的构型和自由度的变化。$\exp(\Delta S^{\ddagger}/R)$ 项直接影响[速率常数](@entry_id:196199)的**[指前因子](@entry_id:145277)**。比较 LH 和 ER 机制的[活化熵](@entry_id:169746)，可以为我们提供更深层次的分子见解 [@problem_id:2669660]。

*   在 **LH 机制**中，过渡态由两个原先可在表面上二维平动的吸附物种结合而成。这个过程伴随着显著的平动和[转动自由度](@entry_id:141502)的损失，导致一个很大的[负活化熵](@entry_id:182140)（例如，$\Delta S_{\mathrm{LH}}^{\ddagger}$ 可能为 $-100 \, \mathrm{J\,mol^{-1}\,K^{-1}}$）。
*   在 **ER 机制**中，过渡态由一个气相分子和一个吸附物种结合而成。这个过程主要损失了气相分子的三维[平动自由度](@entry_id:140257)。尽管也是熵减过程，但其熵损失通常小于 LH 机制中两个表面物种的结合。因此，ER 机制的[活化熵](@entry_id:169746)通常没有那么负（例如，$\Delta S_{\mathrm{ER}}^{\ddagger}$ 可能为 $-20 \, \mathrm{J\,mol^{-1}\,K^{-1}}$）。

这意味着，即使两个机制具有相同的反应能垒 ($\Delta H^{\ddagger}$)，ER 机制在熵上也是更有利的。指前因子的差异可能非常巨大。例如，对于上述给定的[活化熵](@entry_id:169746)值，在 $600 \, \mathrm{K}$ 时，速率常数之比可达：
$$ \frac{k_{\mathrm{ER}}}{k_{\mathrm{LH}}} = \exp\left(\frac{\Delta S_{\mathrm{ER}}^{\ddagger} - \Delta S_{\mathrm{LH}}^{\ddagger}}{R}\right) = \exp\left(\frac{-20 - (-100)}{8.314}\right) \approx \exp(9.6) \sim 1.5 \times 10^4 $$
因此，熵效应可以使 ER 机制的[速率比](@entry_id:164491) LH 机制快几个[数量级](@entry_id:264888)，这在[催化剂设计](@entry_id:155343)和机理研究中是一个不可忽视的重要因素。