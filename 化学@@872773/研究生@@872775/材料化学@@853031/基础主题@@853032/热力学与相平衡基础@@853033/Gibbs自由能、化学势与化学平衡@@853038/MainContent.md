## 引言
虽然热力学第二定律为我们提供了判断宇宙中[自发过程](@entry_id:137544)的终极准则——总[熵增](@entry_id:138799)加，但在[材料科学](@entry_id:152226)与化学的实际应用中，我们更关心在恒温恒压等非孤立条件下的系统行为。直接应用[熵增原理](@entry_id:142282)变得既不方便也不直观，这在预测[材料合成](@entry_id:152212)、[相变](@entry_id:147324)或[化学反应](@entry_id:146973)方向时构成了核心的知识挑战。为了解决这一问题，[热力学](@entry_id:141121)引入了更为强大的工具：吉布斯自由能与化学势。它们将复杂的[系统-环境相互作用](@entry_id:202993)内化为系统本身的状态函数，为预测平衡与自发性提供了直接而优雅的判据。

本篇文章将系统地引导您深入探索这些核心概念。我们首先在“原理与机制”一章中，从基本的热力学定律出发，推导出吉布斯自由能，并引入描述多组分体系物质行为的关键——化学势。您将学习到化学势如何作为所有物质转移和变化的统一驱动力。接着，在“应用与跨学科连接”一章中，我们将展示这些理论的巨大威力，探讨它们如何解释从合金相图、电池[电势](@entry_id:267554)到地球化学缓冲和生命[能量代谢](@entry_id:179002)等不同领域的现象。最后，通过“动手实践”部分提供的计算练习，您将有机会将理论知识应用于解决实际的[热力学](@entry_id:141121)问题，巩固您的理解。通过这趟学习之旅，您将掌握现代材料与[化学热力学](@entry_id:137221)的基石，获得预测和控制物质世界的强大能力。

## 原理与机制

在“绪论”中，我们确立了[热力学第二定律](@entry_id:142732)是判断自发过程的最终准则，即对于任何孤立系统，其熵永不减少。然而，在化学和[材料科学](@entry_id:152226)的实践中，我们更常处理在恒定温度和压力等约束条件下的系统，而不是[孤立系统](@entry_id:159201)。在这种情况下，直接应用宇宙总[熵增](@entry_id:138799)加原理既不方便也不直观。因此，我们需要发展新的[热力学函数](@entry_id:755914)，这些函数能够在其各自的约束条件下，仅通过系统自身性质的变化来预测平衡和自发性。本章旨在系统地阐述这些被称为**[热力学势](@entry_id:140516)**的函数，特别是[亥姆霍兹自由能](@entry_id:136442)和吉布斯自由能。我们将重点定义和阐释**化学势**——一个描述多组分体系中物质行为的核心概念。我们将展示化学势如何作为质量转移和[相变](@entry_id:147324)的根本驱动力，并最终确立其在[化学平衡](@entry_id:142113)中的决定性作用。

### 热力学势与平衡判据

为了在更实际的约束条件下应用第二定律，我们引入了两个关键的热力学势：[亥姆霍兹自由能](@entry_id:136442)和[吉布斯自由能](@entry_id:146774)。它们的作用是将[系统与环境](@entry_id:142270)的热交换和功交换整合到系统自身的状态函数中，从而为特定约束下的[自发过程](@entry_id:137544)提供一个极值判据。

#### [亥姆霍兹自由能](@entry_id:136442)：恒温恒容下的判据

**亥姆霍兹自由能**（Helmholtz free energy），符号为 $A$，通过[勒让德变换](@entry_id:146727)定义为：

$A \equiv U - TS$

其中 $U$ 是内能，$T$ 是温度，$S$ 是熵。其全微分形式为：

$\mathrm{d}A = \mathrm{d}U - T\mathrm{d}S - S\mathrm{d}T$

将内能的基本关系式 $\mathrm{d}U = T\mathrm{d}S - P\mathrm{d}V$（对于一个只做体积功的封闭简单系统）代入，我们得到：

$\mathrm{d}A = (T\mathrm{d}S - P\mathrm{d}V) - T\mathrm{d}S - S\mathrm{d}T = -S\mathrm{d}T - P\mathrm{d}V$

这个关系式表明，$A$ 的自然变量是温度 $T$ 和体积 $V$。对于一个与恒温热库接触并保持恒定体积的封闭系统（$\mathrm{d}T = 0, \mathrm{d}V = 0$），任何[自发过程](@entry_id:137544)都必须满足 $\mathrm{d}A \le 0$。这意味着系统会自发地向着[亥姆霍兹自由能](@entry_id:136442)减小的方向演化，并在 $A$ 达到最小值时达到平衡。因此，**亥姆霍兹自由能的最小化是在恒定温度和恒定体积下系统[达到平衡](@entry_id:170346)的判据**。

#### 吉布斯自由能：恒温恒压下的判据

在化学实验和材料制备中，最常见的条件是系统与恒温热库和恒压环境接触，例如在[标准大气](@entry_id:266260)压下进行的反应。在这种情况下，**[吉布斯自由能](@entry_id:146774)**（Gibbs free energy），符号为 $G$，是更合适的判据。它的定义为：

$G \equiv H - TS = U + PV - TS$

其中 $H$ 是焓，$P$ 是压力。其全微分形式为：

$\mathrm{d}G = \mathrm{d}U + P\mathrm{d}V + V\mathrm{d}P - T\mathrm{d}S - S\mathrm{d}T$

再次代入 $\mathrm{d}U = T\mathrm{d}S - P\mathrm{d}V$，我们得到：

$\mathrm{d}G = (T\mathrm{d}S - P\mathrm{d}V) + P\mathrm{d}V + V\mathrm{d}P - T\mathrm{d}S - S\mathrm{d}T = -S\mathrm{d}T + V\mathrm{d}P$

这个关系式表明，$G$ 的自然变量是温度 $T$ 和压力 $P$。对于一个在恒定温度和恒定压力下进行的封闭系统（$\mathrm{d}T = 0, \mathrm{d}P = 0$），任何[自发过程](@entry_id:137544)都必须满足 $\mathrm{d}G \le 0$。这意味着系统会自发地向着吉布斯自由能减小的方向演化，并在 $G$ 达到最小值时达到平衡。因此，**[吉布斯自由能](@entry_id:146774)的最小化是在恒定温度和恒定压力下系统达到平衡的判据**。

选择哪个热力学势作为平衡判据完全取决于施加在系统上的约束条件。一个经典的例子可以说明这一点：考虑一个单组分晶体固体的两种同质异形体 $\alpha$ 和 $\beta$。假设在 $T=300\,\mathrm{K}$ 时，我们知道从 $\alpha$ 相转变为 $\beta$ 相的摩尔性质变化为 $\Delta U = U_{\beta}-U_{\alpha} = +50\,\mathrm{J\,mol^{-1}}$，$\Delta S \approx 0$，以及 $\Delta V = V_{\beta}-V_{\alpha} = -5.0 \times 10^{-6}\,\mathrm{m^3\,mol^{-1}}$。现在，我们在两种不同的实验装置中研究这个系统 [@problem_id:2488794]：
(i) 在恒定温度 $T=300\,\mathrm{K}$ 和恒定高压 $P=1.0 \times 10^9\,\mathrm{Pa}$ 下。
(ii) 在恒定温度 $T=300\,\mathrm{K}$ 和恒定总体积下。

在装置(i)中，约束条件是恒温恒压，因此我们必须使用[吉布斯自由能](@entry_id:146774) $G$。[相变](@entry_id:147324)导致的摩尔[吉布斯自由能变](@entry_id:138324)化为：
$\Delta G = \Delta U - T\Delta S + P\Delta V \approx (+50) - (300)(0) + (1.0 \times 10^9)(-5.0 \times 10^{-6}) = 50 - 5000 = -4950\,\mathrm{J\,mol^{-1}}$。
由于 $\Delta G  0$，从 $\alpha$ 到 $\beta$ 的[相变](@entry_id:147324)是自发的，因此在高压下 $\beta$ 相更稳定。

在装置(ii)中，约束条件是恒温恒容，我们必须使用[亥姆霍兹自由能](@entry_id:136442) $A$。[相变](@entry_id:147324)导致的摩尔亥姆霍兹自由能变化为：
$\Delta A = \Delta U - T\Delta S \approx (+50) - (300)(0) = +50\,\mathrm{J\,mol^{-1}}$。
由于 $\Delta A  0$，从 $\alpha$ 到 $\beta$ 的[相变](@entry_id:147324)是非自发的。在这种约束下，$\alpha$ 相更稳定。这个例子清晰地表明，外部约束条件决定了哪个[热力学势](@entry_id:140516)是合适的，并且可以对系统的稳定性做出截然不同的预测。

### 化学势：变化的引擎

到目前为止，我们只考虑了封闭系统，其中物质的总量是固定的。然而，化学和[材料科学](@entry_id:152226)的核心在于物质的转化和迁移——[化学反应](@entry_id:146973)、[相变](@entry_id:147324)、[扩散](@entry_id:141445)等。为了描述这些现象，我们必须将组分的变化引入[热力学](@entry_id:141121)框架。

#### 将组分引入吉布斯自由能

对于一个开放或多组分系统，其[吉布斯自由能](@entry_id:146774)不仅是温度和压力的函数，也是系统中每种组分摩尔数 $n_i$ 的函数。吉布斯自由能的全[微分形式](@entry_id:146747)被扩展为：

$\mathrm{d}G = -S\mathrm{d}T + V\mathrm{d}P + \sum_i \mu_i \mathrm{d}n_i$

这个方程被称为**[热力学基本方程](@entry_id:180245)**。其中新增的项 $\sum_i \mu_i \mathrm{d}n_i$ 描述了由于物质数量变化对吉布斯自由能的贡献。系数 $\mu_i$ 被称为组分 $i$ 的**化学势** (chemical potential)。

根据这个微分形式，我们可以给出化学势的严格定义：

$\mu_i \equiv \left(\frac{\partial G}{\partial n_i}\right)_{T,P,\{n_{j\neq i}\}}$

换言之，**化学势是在恒定温度、压力以及所有其他组分数量不变的条件下，向系统中加入一摩尔组分 $i$ 所引起的[吉布斯自由能](@entry_id:146774)的变化**。因此，化学势是一个[偏摩尔量](@entry_id:136234)，具体来说，是**偏摩尔[吉布斯自由能](@entry_id:146774)** [@problem_id:2488796]。它量化了在特定化学环境中（由 T, P 和其他组分的浓度决定）一摩尔物质所具有的“能量”或“驱动力”。

#### [吉布斯自由能](@entry_id:146774)的[广延性](@entry_id:144932)与积分形式

像内能 $U$、熵 $S$ 和体积 $V$ 一样，[吉布斯自由能](@entry_id:146774) $G$ 是一个**[广延性质](@entry_id:145410)**（extensive property），这意味着它的值与系统的总[物质的量](@entry_id:140225)成正比。如果我们将系统中所有组分的摩尔数都放大 $\lambda$ 倍（$n_i \mapsto \lambda n_i$），而保持温度 $T$ 和压力 $P$ 等[强度性质](@entry_id:181209)不变，那么总的[吉布斯自由能](@entry_id:146774)也会放大 $\lambda$ 倍，$G \mapsto \lambda G$。

这个性质表明，在恒定的 $T$ 和 $P$ 下，$G$ 是关于摩尔数 $\{n_i\}$ 的一级齐次函数。根据[欧拉齐次函数定理](@entry_id:186434)，这样的函数可以表示为其所有[偏导数](@entry_id:146280)与其对应变量的乘[积之和](@entry_id:266697)。应用到 $G$ 上，我们有 [@problem_id:2488796]：

$G(T, P, \{n_i\}) = \sum_i n_i \left(\frac{\partial G}{\partial n_i}\right)_{T, P, \{n_{j\neq i}\}}}$

将化学势的定义代入，我们得到一个至关重要的关系：

$G = \sum_i n_i \mu_i$

这个方程表明，在恒定 $T$ 和 $P$ 下，一个多组分体系的总[吉布斯自由能](@entry_id:146774)等于各组分的摩尔数与其各自化学势的乘积之和。

重要的是要区分化学势（一个[偏摩尔量](@entry_id:136234)）和混合物的平均摩尔[吉布斯自由能](@entry_id:146774) $\bar{G} = G/n_{\text{tot}}$（其中 $n_{\text{tot}} = \sum_i n_i$）。将上面的积分形式除以总摩尔数 $n_{\text{tot}}$，我们得到：

$\bar{G} = \frac{G}{n_{\text{tot}}} = \sum_i \frac{n_i}{n_{\text{tot}}} \mu_i = \sum_i x_i \mu_i$

其中 $x_i$ 是组分 $i$ 的摩尔分数。可见，平均摩尔吉布斯自由能是各组分化学势的[摩尔分数](@entry_id:145460)加权平均。一般而言，对于混合物中的任一组分 $i$，其化学势 $\mu_i$ 并不等于平均摩尔吉布斯自由能 $\bar{G}$ [@problem_id:2488783]。只有在纯物质（$x_i=1$）的特殊情况下，两者才相等。

#### 吉布斯-杜亥姆关系

化学势之间并非完全独立。通过对 $G = \sum_i n_i \mu_i$ 进行[全微分](@entry_id:171747)，我们得到：

$\mathrm{d}G = \sum_i (\mu_i \mathrm{d}n_i + n_i \mathrm{d}\mu_i)$

将此式与[热力学基本方程](@entry_id:180245) $\mathrm{d}G = -S\mathrm{d}T + V\mathrm{d}P + \sum_i \mu_i \mathrm{d}n_i$ 进行比较，可以消去 $\sum_i \mu_i \mathrm{d}n_i$ 项，得到：

$-S\mathrm{d}T + V\mathrm{d}P = \sum_i n_i \mathrm{d}\mu_i$

这个方程被称为**吉布斯-杜亥姆关系** (Gibbs-Duhem relation)。它表明，在一个相中，强度变量 $T$, $P$ 和所有化学势 $\{\mu_i\}$ 的变化是相互约束的，不是独立的。在恒定温度和压力下（$\mathrm{d}T=0, \mathrm{d}P=0$），该关系简化为：

$\sum_i n_i \mathrm{d}\mu_i = 0$ (在恒定 $T, P$ 下)

或用摩尔分数表示：$\sum_i x_i \mathrm{d}\mu_i = 0$。这意味着在[二元混合物](@entry_id:168452)中，如果一个组分的化学势随成分变化而增加，另一个组分的化学势必须减少，以保持该关系成立 [@problem_id:2488796]。

### 化学势与平衡

化学势的真正威力在于它为[相平衡](@entry_id:136822)和化学平衡提供了统一的判据，并揭示了所有[自发过程](@entry_id:137544)背后的根本驱动力。

#### 相平衡的普遍条件

考虑一个[封闭系统](@entry_id:139565)，包含 $\alpha$ 和 $\beta$ 两个相，处于恒定的温度和压力下。设想有无穷小量的组分 $i$ 从 $\alpha$ 相转移到 $\beta$ 相，转移的量为 $\mathrm{d}n_i^\alpha = -\mathrm{d}n_i^\beta$。系统的总[吉布斯自由能变](@entry_id:138324)化为 [@problem_id:2927943]：

$\mathrm{d}G_{\text{tot}} = \mathrm{d}G^\alpha + \mathrm{d}G^\beta = \mu_i^\alpha \mathrm{d}n_i^\alpha + \mu_i^\beta \mathrm{d}n_i^\beta = \mu_i^\alpha (-\mathrm{d}n_i^\beta) + \mu_i^\beta \mathrm{d}n_i^\beta = (\mu_i^\beta - \mu_i^\alpha) \mathrm{d}n_i^\beta$

根据[吉布斯自由能最小化](@entry_id:151466)原理，在平衡状态下，任何无穷小的变化都不能导致 $G_{\text{tot}}$ 降低，对于可逆过程，$\mathrm{d}G_{\text{tot}}=0$。由于物质可以从 $\beta$ 转移到 $\alpha$（$\mathrm{d}n_i^\beta  0$）也可以从 $\alpha$ 转移到 $\beta$（$\mathrm{d}n_i^\beta  0$），要使 $\mathrm{d}G_{\text{tot}}$ 始终为零，唯一的可能是其系数为零：

$\mu_i^\beta - \mu_i^\alpha = 0 \implies \mu_i^\alpha = \mu_i^\beta$

这个推导表明，**对于能够在两相之间自由转移的任何组分，其在两相中的化学势相等，是相平衡的必要条件**。进一步地，如果化学势不相等，例如 $\mu_i^\alpha  \mu_i^\beta$，那么物质会自发地从 $\alpha$ 相流向 $\beta$ 相（$\mathrm{d}n_i^\alpha  0$），使得 $\mathrm{d}G_{\text{tot}} = (\mu_i^\beta - \mu_i^\alpha)\mathrm{d}n_i^\beta  0$。这表明系统尚未[达到平衡](@entry_id:170346)。因此，化学势相等也是**充分条件** [@problem_id:2927943]。

这个强大的结论是普适的，适用于多组分多相体系中的所有组分。在完全平衡状态下，**每个组分在所有共存相中的化学势都必须相等**。例如，在A-B[二元合金](@entry_id:160005)的 $\alpha$ 和 $\beta$ 两[相平衡](@entry_id:136822)中，必须同时满足 $\mu_A^\alpha = \mu_A^\beta$ 和 $\mu_B^\alpha = \mu_B^\beta$ [@problem_id:2488792]。

#### 作为驱动力的化学势

前面的推导不仅确立了平衡条件，还揭示了一个更深层的机制：**在恒定温度和压力下，物质自发地从化学势高的区域流向化学势低的区域**。化学势的差[异或](@entry_id:172120)梯度，正是质量转移和[相变](@entry_id:147324)的根本[热力学](@entry_id:141121)驱动力。

我们可以通过具体的例子来理解这一点 [@problem_id:2488792]：
1.  **质量转移**：设想两个A-B合金溶液储槽，通过一个只允许A组分通过的[半透膜](@entry_id:139634)连接。如果储槽1中A的化学势为 $\mu_A^{(1)} = -10200\,\mathrm{J\,mol^{-1}}$，而储槽2中为 $\mu_A^{(2)} = -10500\,\mathrm{J\,mol^{-1}}$。由于 $\mu_A^{(1)}  \mu_A^{(2)}$，A组分会自发地从储槽1流向储槽2，以降低系统的总吉布斯自由能。
2.  **[相变](@entry_id:147324)（沉淀析出）**：在一个[过饱和](@entry_id:200794)的 $\alpha$ 基体中，要形成化学计量比为 $\mathrm{AB_2}$ 的 $\beta$ 相沉淀。这个过程可以看作是一个“反应”：$\mathrm{A}(\text{在}\alpha\text{中}) + 2\mathrm{B}(\text{在}\alpha\text{中}) \rightarrow \mathrm{AB_2}(\text{在}\beta\text{中})$。形成一摩尔 $\mathrm{AB_2}$ 的吉布斯自由能变化（即驱动力）为 $\Delta G_{\text{chem}} = \mu_{\mathrm{AB}_2}^\beta - (\mu_A^\alpha + 2\mu_B^\alpha)$。如果这个值为负，沉淀过程就是自发的。

#### [扩散](@entry_id:141445)与[化学势梯度](@entry_id:142294)

一个常见的误解是，[浓度梯度](@entry_id:136633)是[扩散](@entry_id:141445)的驱动力。然而，真正的驱动力是**[化学势梯度](@entry_id:142294)**。[扩散通量](@entry_id:748422) $J_i$ 正比于 $-\nabla\mu_i$。在许多简单情况下，[化学势梯度](@entry_id:142294)和[浓度梯度](@entry_id:136633)方向一致，但这并非总是如此。化学势不仅依赖于浓度，还依赖于压力、应[力场](@entry_id:147325)、[电场](@entry_id:194326)等。例如，在一块成分均匀的受压[固溶体](@entry_id:137535)中，由于应力[分布](@entry_id:182848)不均，会导致各处的活性系数不同，从而产生[化学势梯度](@entry_id:142294) ($\nabla\mu_i \neq 0$)，即使此时[浓度梯度](@entry_id:136633)为零 ($\nabla c_i = 0$)。这种[化学势梯度](@entry_id:142294)仍然会驱动[扩散](@entry_id:141445)，这一现象被称为应力诱导[扩散](@entry_id:141445) [@problem_id:2488792]。

### 化学势的建模

为了在实际中应用化学势，我们需要具体的数学模型来将其与可测量的量（如温度、压力和组分）联系起来。

#### [理想气体混合物](@entry_id:149212)

最简单的模型是[理想气体混合物](@entry_id:149212)。通过[热力学积分](@entry_id:156321)或经典的[半透膜](@entry_id:139634)思想实验可以推导出，混合物中组分 $i$ 的化学势为 [@problem_id:2488775]：

$\mu_i(T, P, y_i) = \mu_i^\circ(T) + RT \ln\left(\frac{P_i}{P^\circ}\right) = \mu_i^\circ(T) + RT \ln\left(\frac{y_i P}{P^\circ}\right)$

其中 $\mu_i^\circ(T)$ 是在相同温度 $T$ 和标准压力 $P^\circ$（通常为1 bar）下纯组分 $i$ 的化学势，被称为**[标准化](@entry_id:637219)学势**。$P_i = y_i P$ 是组分 $i$ 的分压，$y_i$ 是其[摩尔分数](@entry_id:145460)。这个表达式首次揭示了化学势与组分的对数依赖关系。

#### 理想[固溶体](@entry_id:137535)

对于凝聚相，如固溶体或液[态混合](@entry_id:148060)物，我们也可以定义理想行为。对于一个理想二元替代型固溶体，我们可以从[统计力](@entry_id:194984)学出发。混合过程唯一的贡献来自组态熵的增加，即原子随机[排列](@entry_id:136432)方式的数量。通过[玻尔兹曼熵公式](@entry_id:136916) $S = k_B \ln \Omega$ 和[斯特林近似](@entry_id:137296)，可以推导出[混合熵](@entry_id:161398)为 $\Delta S_{\text{mix}} = -R \sum_i n_i \ln x_i$。由于[理想混合](@entry_id:150763)的[混合焓](@entry_id:158999) $\Delta H_{\text{mix}} = 0$，[混合吉布斯自由能](@entry_id:137582)为 $\Delta G_{\text{mix}} = -T\Delta S_{\text{mix}} = RT \sum_i n_i \ln x_i$。总的[吉布斯自由能](@entry_id:146774) $G = \sum_i n_i \mu_i^\circ + \Delta G_{\text{mix}}$，对其求偏导，我们得到组分 $i$ 的化学势为 [@problem_id:2488759]：

$\mu_i = \mu_i^\circ + RT \ln x_i$

其中 $\mu_i^\circ$ 是在相同 $T, P$ 下纯组分 $i$ 的化学势。这个结果将化学势中的对数项与微观尺度上的混合无序度直接联系起来。

#### 真实溶液：活性与[标准态](@entry_id:145000)

真实系统中的原子/分子间存在相互作用，导致[混合焓](@entry_id:158999)不为零，[混合熵](@entry_id:161398)也偏离[理想混合](@entry_id:150763)熵。为了保留 $\mu_i = \mu_i^\circ + RT \ln(\dots)$ 这种简洁的数学形式，我们引入了**活性**（activity），$a_i$，的概念：

$\mu_i = \mu_i^\circ + RT \ln a_i$

活性 $a_i$ 可以看作是组分 $i$ 在真实溶液中的“有效浓度”或“有效[摩尔分数](@entry_id:145460)”，它将所有偏离理想行为的复杂效应都包含在内。活性的值依赖于我们如何定义**[标准态](@entry_id:145000)**（standard state），即 $\mu_i^\circ$ 所对应的状态。

对于稀溶液，通常采用一种非对称的约定 [@problem_id:2488777] [@problem_id:2488788]：
- **溶剂（主要组分）**：当其[摩尔分数](@entry_id:145460) $x_{\text{solvent}} \to 1$ 时，其行为接近纯液体。因此，我们选择在相同 $T, P$ 下的**纯液体**作为其[标准态](@entry_id:145000)。在此约定下，当 $x_{\text{solvent}} \to 1$ 时，$a_{\text{solvent}} \to x_{\text{solvent}}$。这被称为**[拉乌尔定律](@entry_id:139880)（Raoult's law）标准态**。
- **溶质（次要组分）**：当其[摩尔分数](@entry_id:145460) $x_{\text{solute}} \to 0$ 时，其行为遵循[亨利定律](@entry_id:147254)（Henry's law），即其[蒸气压](@entry_id:136384)正比于其[摩尔分数](@entry_id:145460)，$p_{\text{solute}} \propto x_{\text{solute}}$。为了方便，我们定义一个**假想的标准态**，使得在此极限下活性系数 $\gamma_{\text{solute}} = a_{\text{solute}}/x_{\text{solute}} \to 1$。这意味着 $a_{\text{solute}} \to x_{\text{solute}}$。这个标准态被称为**[亨利定律](@entry_id:147254)标准态**，其[标准化](@entry_id:637219)学势 $\mu_{\text{solute}}^\circ$ 的值与溶剂的种类有关。

这种灵活定义[标准态](@entry_id:145000)和活性的方法，为处理复杂的真实溶液提供了一个强大而系统的[热力学](@entry_id:141121)框架。

### 化学势对温度和压力的依赖性

最后，我们需要知道化学势本身如何随温度和压力变化。通过对[吉布斯自由能](@entry_id:146774)的二阶[混合偏导数](@entry_id:139334)使用麦克斯韦关系，我们可以推导出化学势对 $T$ 和 $P$ 的依赖关系。回顾 $\mathrm{d}G = -S\mathrm{d}T + V\mathrm{d}P + \sum_i \mu_i \mathrm{d}n_i$，我们有：

$\left(\frac{\partial \mu_i}{\partial T}\right)_{P, \{n_k\}} = \frac{\partial^2 G}{\partial T \partial n_i} = \frac{\partial}{\partial n_i}\left(\frac{\partial G}{\partial T}\right) = -\left(\frac{\partial S}{\partial n_i}\right)_{T,P,\{n_{j\neq i}\}} \equiv -\bar{s}_i$

$\left(\frac{\partial \mu_i}{\partial P}\right)_{T, \{n_k\}} = \frac{\partial^2 G}{\partial P \partial n_i} = \frac{\partial}{\partial n_i}\left(\frac{\partial G}{\partial P}\right) = \left(\frac{\partial V}{\partial n_i}\right)_{T,P,\{n_{j\neq i}\}} \equiv \bar{v}_i$

其中 $\bar{s}_i$ 和 $\bar{v}_i$ 分别是组分 $i$ 的**偏摩尔熵**和**[偏摩尔体积](@entry_id:143502)**。因此，在固定组分下，化学势的[全微分](@entry_id:171747)为 [@problem_id:2488762]：

$\mathrm{d}\mu_i = -\bar{s}_i \mathrm{d}T + \bar{v}_i \mathrm{d}P$

这个关系非常重要，因为它将抽象的化学势的变化与可测量的物理量（偏摩尔熵和[偏摩尔体积](@entry_id:143502)）联系起来。如果我们知道 $\bar{s}_i$ 和 $\bar{v}_i$ 作为温度和压力的函数，我们就可以通过积分计算出化学势从一个状态 $(T_0, P_0)$ 变化到另一个状态 $(T, P)$ 的值。这使得我们能够预测温度和压力变化如何影响相平衡和[化学平衡](@entry_id:142113)的位置。例如，通过积分此式，可以构建相图，或计算在[高压合成](@entry_id:155909)等极端条件下材料的稳定性 [@problem_id:2488762]。

总之，[吉布斯自由能](@entry_id:146774)和化学势共同构成了现代[化学热力学](@entry_id:137221)的基石。它们不仅为[化学平衡](@entry_id:142113)和相平衡提供了严格的判据，更重要的是，揭示了驱动所有物质变化的统一内在力量——化学势的差异。通过对化学势进行建模和量化，我们获得了预测和控制材料行为的强大工具。