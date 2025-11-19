## 引言
在化学世界中，能量的转化是所有反应的核心。精确量化反应过程中的热量变化，即[反应焓](@entry_id:149764)变，对于科学研究和工业生产都至关重要。然而，许多[化学反应](@entry_id:146973)由于速率过慢、过快、或伴有[副反应](@entry_id:271170)，其[反应热](@entry_id:140993)难以通过实验直接测量。赫斯热总和定律（Hess's Law of Heat Summation）为解决这一难题提供了优雅而强大的理论工具，它允许我们通过间接的、可测量的路径来确定目标反应的热效应。

本文将系统地引导您深入理解[赫斯定律](@entry_id:147875)。在“原理与机制”一章中，我们将追溯其[热力学](@entry_id:141121)根源——焓作为[状态函数](@entry_id:137683)的本质，并掌握利用[标准生成焓](@entry_id:144770)进行计算的核心方法。随后，在“应用与跨学科联系”一章中，我们将探索[赫斯定律](@entry_id:147875)如何跨越学科界限，在化学工程、[材料科学](@entry_id:152226)、生物化学等领域解决实际问题。最后，通过“动手实践”部分，您将有机会运用所学知识解决具体的热[化学计算](@entry_id:155220)问题。这趟旅程将从[赫斯定律](@entry_id:147875)最根本的基石开始，揭示为何[反应热](@entry_id:140993)的加和具有如此坚实的理论基础。

## 原理与机制

### 基本原理：焓作为状态函数

在[热化学](@entry_id:137688)领域，**焓**（**Enthalpy**），符号为 $H$，是一个核心的[热力学](@entry_id:141121)量。其定义为 $H \equiv U + pV$，其中 $U$ 是系统的内能，$p$ 是压力，$V$ 是体积。焓最重要的特性之一是它是一个**状态函数**（**state function**）。这意味着，一个系统焓的数值仅取决于其当前的[热力学状态](@entry_id:755916)（如温度、压力、物相和组成），而与系统如何达到该状态的历史路径无关。因此，当一个系统从一个初始状态（initial state）转变为一个最终状态（final state）时，其焓变（$\Delta H = H_{\text{final}} - H_{\text{initial}}$）是唯一确定的，与转变所经历的具体过程或途径无关。

为了深刻理解[状态函数](@entry_id:137683)的[路径无关性](@entry_id:163750)，我们可以将其与**[路径函数](@entry_id:144689)**（**path functions**）如**热**（**heat**, $q$）和**功**（**work**, $w$）进行对比。根据[热力学第一定律](@entry_id:146485)，$\Delta U = q + w$。虽然内能变 $\Delta U$ 是路径无关的，但热和功却依赖于过程的具体路径。

考虑一个具体的[化学反应](@entry_id:146973)，例如在标准条件下石墨的完全燃烧：
$$
\mathrm{C(graphite)} + \mathrm{O_2(g)} \to \mathrm{CO_2(g)}
$$
这个过程的初始态是1摩尔石墨和1摩尔氧气，最终态是1摩尔二氧化碳，它们都处于相同的温度和压力下。无论这个反应如何进行，系统的始末状态是确定的，因此其内能变 $\Delta U$ 和焓变 $\Delta H$ 都是固定值。

然而，我们可以设想两条不同的路径来实现这一转变 [@problem_id:2940936]：
1.  **路径一：简单燃烧**。在一个恒压容器中直接燃烧石墨。在这个过程中，气体摩尔数没有变化（$\Delta n_g = 1 - 1 = 0$），因此体系对环境做的[压力-体积功](@entry_id:139224) $w = -p_{\text{ext}}\Delta V$ 近似为零。根据第一定律，体系放出的热量 $q_p$ 等于[焓变](@entry_id:147639) $\Delta H$。

2.  **路径二：电化学路径**。在一个燃料电池中，通过电[化学反应](@entry_id:146973)使石墨氧化。在这个可逆过程中，化学能被高效地转化为了电能，体系可以对外界做大量的[非体积功](@entry_id:137402)（电功 $w_{\text{elec}}$）。理论上，在恒温恒压下可逆过程所能做的最大[非体积功](@entry_id:137402)等于[吉布斯自由能变](@entry_id:138324) $\Delta G$。此时，总功 $w = w_{p-V} + w_{\text{elec}}$。由于 $w$ 在两条路径中显著不同（路径二做的功远大于路径一），为了保持 $\Delta U$ 不变，体系与环境交换的热量 $q = \Delta U - w$ 也必须是[路径依赖](@entry_id:138606)的。

这个例子清晰地表明，热量 $q$ 和功 $w$ 的数值取决于[化学反应](@entry_id:146973)的具体实现方式，它们是[路径函数](@entry_id:144689)。与之形成鲜明对比的是，焓变 $\Delta H$ 仅由始末状态决定，与路径无关。正是焓的这种状态函数特性，构成了[赫斯定律](@entry_id:147875)的理论基石。

**[赫斯定律](@entry_id:147875)**（**Hess's Law of Constant Heat Summation**）的表述如下：一个[化学反应](@entry_id:146973)的[反应焓](@entry_id:149764)，无论是一步完成还是分多步完成，其[总焓](@entry_id:197863)变是相同的。换言之，[化学反应](@entry_id:146973)的焓变仅取决于反应物和产物的状态，而与反应所经过的途径无关。

### [赫斯定律](@entry_id:147875)的严谨表述与条件

[赫斯定律](@entry_id:147875)的简洁表述背后，是对应用条件的严格要求。一个严谨的[赫斯定律](@entry_id:147875)表述必须强调，所有比较的路径都必须连接完全相同的初始[状态和](@entry_id:193625)最终状态 [@problem_id:2940961]。这意味着：

1.  **温度和压力一致性**：所有分步反应的焓变都必须是在目标反应发生的相同温度和压力下测定或校正到该条件下的值。

2.  **物态同一性**：反应中涉及的每一种物质的物理状态（包括其[物相](@entry_id:196677)，如固相(s)、液相(l)、气相(g)，以及[同素异形体](@entry_id:137177)(allotrope)等）在目标反应和分步[反应路径](@entry_id:163735)的最终加和中必须完全对应。

任何对这些条件的偏离都会导致错误的结论。例如，一个常见的误区是认为只要[化学式](@entry_id:136318)匹配，就可以直接加和[焓变](@entry_id:147639)。然而，$\mathrm{H_2O}(l)$ 和 $\mathrm{H_2O}(g)$ 是两种具有不同焓值的[热力学状态](@entry_id:755916)。考虑氢气燃烧生成水的反应 [@problem_id:2940967]：
$$
\mathrm{H_2}(g) + \tfrac{1}{2}\mathrm{O_2}(g) \to \mathrm{H_2O}(g), \quad \Delta H^\circ_g = -241.8 \text{ kJ/mol}
$$
$$
\mathrm{H_2}(g) + \tfrac{1}{2}\mathrm{O_2}(g) \to \mathrm{H_2O}(l), \quad \Delta H^\circ_l = -285.8 \text{ kJ/mol}
$$
这两个[焓变](@entry_id:147639)值不同，但这并不违反[赫斯定律](@entry_id:147875)，因为它们对应的是两个不同的最终状态。这两个过程的[焓变](@entry_id:147639)之差恰好是1摩尔水在相同温度下的[汽化焓](@entry_id:141692)：
$$
\Delta H^\circ (\mathrm{H_2O}(l) \to \mathrm{H_2O}(g)) = \Delta H^\circ_g - \Delta H^\circ_l = -241.8 - (-285.8) = +44.0 \text{ kJ/mol}
$$
这说明，未能精确定义和匹配始末状态是导致“表观”[路径依赖性](@entry_id:186326)的主要原因。

此外，[赫斯定律](@entry_id:147875)的成立与反应的具体**机理**（**mechanism**）无关。无论反应是通过一个简单的基元步骤完成，还是通过一个包含多种中间体和催化剂的复杂多步机理完成，只要起始反应物和最终产物相同，总的[焓变](@entry_id:147639)就不会改变 [@problem_id:2940967]。例如，气相中水可以通过氢气和氧气[直接反应](@entry_id:161030)生成，也可以通过一个涉及过氧化氢（$\mathrm{H_2O_2}$）中间体的两步过程进行：

- **总反应**: $\mathrm{H_2}(g) + \tfrac{1}{2}\mathrm{O_2}(g) \to \mathrm{H_2O}(g)$, $\Delta_{\mathrm{r}} H^\circ = -241.826 \text{ kJ/mol}$

- **机理路径**:
    - 步骤1: $\mathrm{H_2}(g) + \mathrm{O_2}(g) \to \mathrm{H_2O_2}(g)$, $\Delta_{\mathrm{r}} H^\circ_1 = -136.106 \text{ kJ/mol}$
    - 步骤2: $\mathrm{H_2O_2}(g) \to \mathrm{H_2O}(g) + \tfrac{1}{2}\mathrm{O_2}(g)$, $\Delta_{\mathrm{r}} H^\circ_2 = -105.720 \text{ kJ/mol}$

将这两个步骤的反应和焓变相加：
$$
\Delta_{\mathrm{r}} H^\circ_1 + \Delta_{\mathrm{r}} H^\circ_2 = -136.106 + (-105.720) = -241.826 \text{ kJ/mol}
$$
其结果与总反应的[焓变](@entry_id:147639)完全一致。这雄辩地证明了，[反应机理](@entry_id:149504)的复杂性影响的是[反应速率](@entry_id:139813)（动力学），而非反应的整体[焓变](@entry_id:147639)（[热力学](@entry_id:141121)）。

### [赫斯定律](@entry_id:147875)的实际应用

[赫斯定律](@entry_id:147875)最强大的功能在于，它允许我们通过已知的[反应焓](@entry_id:149764)变来计算那些难以直接通过实验测定的[反应焓](@entry_id:149764)变。这种计算能力在化学、[材料科学](@entry_id:152226)、生物化学等领域都至关重要。

#### [反应焓](@entry_id:149764)的组合

[赫斯定律](@entry_id:147875)的应用常常涉及对[热化学方程式](@entry_id:191883)的代数运算。我们可以像处理[代数方程](@entry_id:272665)一样，对[热化学方程式](@entry_id:191883)进行加、减、乘除和逆向操作：
- **逆转反应**：[反应焓](@entry_id:149764)的符号相反。
- **乘以常数**：[反应焓](@entry_id:149764)也乘以相同的常数。

**示例1：计算[三氟化氯](@entry_id:147966)的[生成焓](@entry_id:139204)**
假设我们想要求解[三氟化氯](@entry_id:147966)气体 ($\mathrm{ClF_3(g)}$) 的[标准生成焓](@entry_id:144770)，但该数据不易直接测量。不过，我们已知以下两个反应的[焓变](@entry_id:147639) [@problem_id:1984211]：
1.  $\tfrac{1}{2}\mathrm{Cl_2}(g) + \tfrac{1}{2}\mathrm{F_2}(g) \to \mathrm{ClF}(g), \quad \Delta H^\circ_1 = -55.8 \text{ kJ/mol}$
2.  $\mathrm{ClF}(g) + \mathrm{F_2}(g) \to \mathrm{ClF_3}(g), \quad \Delta H^\circ_2 = -110.5 \text{ kJ/mol}$

我们想要得到的目标反应是 $\mathrm{ClF_3(g)}$ 从其元素的形成反应：
$$
\tfrac{1}{2}\mathrm{Cl_2}(g) + \tfrac{3}{2}\mathrm{F_2}(g) \to \mathrm{ClF_3}(g), \quad \Delta H^\circ_f = ?
$$
通过观察可以发现，将反应(1)和反应(2)直接相加，即可得到目标反应：
$$
(\tfrac{1}{2}\mathrm{Cl_2}(g) + \tfrac{1}{2}\mathrm{F_2}(g)) + (\mathrm{ClF}(g) + \mathrm{F_2}(g)) \to (\mathrm{ClF}(g)) + (\mathrm{ClF_3}(g))
$$
合并同类项后得到： $\tfrac{1}{2}\mathrm{Cl_2}(g) + \tfrac{3}{2}\mathrm{F_2}(g) \to \mathrm{ClF_3}(g)$。根据[赫斯定律](@entry_id:147875)，目标反应的焓变就是两个分步[反应焓](@entry_id:149764)变之和：
$$
\Delta H^\circ_f(\mathrm{ClF_3}, g) = \Delta H^\circ_1 + \Delta H^\circ_2 = -55.8 + (-110.5) = -166.3 \text{ kJ/mol}
$$

**示例2：计算[相变](@entry_id:147324)焓**
[赫斯定律](@entry_id:147875)同样适用于物理过程，如[相变](@entry_id:147324)。例如，固体的[升华](@entry_id:139006)过程（固态 $\to$ 气态）可以看作是先熔化（固态 $\to$ 液态），再汽化（液态 $\to$ 气态）的两步过程。因此，**[升华焓](@entry_id:193394)**等于**[熔化焓](@entry_id:143962)**与**[汽化焓](@entry_id:141692)**之和。对于萘 ($\mathrm{C_{10}H_8}$)，已知其标准[摩尔熔化焓](@entry_id:139030)为 $+18.98 \text{ kJ/mol}$，标准[摩尔汽化焓](@entry_id:187768)为 $+43.3 \text{ kJ/mol}$ [@problem_id:1984269]。因此，其标准摩尔[升华焓](@entry_id:193394)为：
$$
\Delta H_{\text{sub}}^{\circ} = \Delta H_{\text{fus}}^{\circ} + \Delta H_{\text{vap}}^{\circ} = 18.98 + 43.3 = 62.28 \approx 62.3 \text{ kJ/mol}
$$
反过来，我们也可以利用[赫斯定律](@entry_id:147875)从[燃烧反应](@entry_id:152943)数据中提取[相变](@entry_id:147324)焓。例如，已知甲烷燃烧生成液态水和气态水的[焓变](@entry_id:147639)不同 [@problem_id:1984231]：
1.  $\mathrm{CH_4}(g) + 2\mathrm{O_2}(g) \to \mathrm{CO_2}(g) + 2\mathrm{H_2O}(l), \quad \Delta H^\circ_1 = -890.8 \text{ kJ/mol}$
2.  $\mathrm{CH_4}(g) + 2\mathrm{O_2}(g) \to \mathrm{CO_2}(g) + 2\mathrm{H_2O}(g), \quad \Delta H^\circ_2 = -802.6 \text{ kJ/mol}$

将反应(1)逆转，并与反应(2)相加，可以消去 $\mathrm{CH_4}$、$\mathrm{O_2}$ 和 $\mathrm{CO_2}$，得到水的汽化反应：$2\mathrm{H_2O}(l) \to 2\mathrm{H_2O}(g)$。其[焓变](@entry_id:147639)为：
$$
\Delta H^\circ = \Delta H^\circ_2 - \Delta H^\circ_1 = -802.6 - (-890.8) = +88.2 \text{ kJ}
$$
由于这是2摩尔水的[汽化焓](@entry_id:141692)，因此水的标准[摩尔汽化焓](@entry_id:187768)为：
$$
\Delta H_{\text{vap}}^{\circ}(\mathrm{H_2O}) = \frac{+88.2 \text{ kJ}}{2 \text{ mol}} = 44.1 \text{ kJ/mol}
$$

#### [标准生成焓](@entry_id:144770)的概念

虽然直接组合[反应焓](@entry_id:149764)的方法很直观，但为每一个可能的反应都去寻找一个特定的反应路径组合是低效的。一个更系统化的方法是引入**[标准生成焓](@entry_id:144770)**（**Standard Enthalpy of Formation**），符号为 $\Delta H_f^\circ$。它被定义为：在标准状态下（通常指压力为 $1 \text{ bar}$ 和指定温度），由其最稳定形式的组成元素生成1摩尔化合物时的[焓变](@entry_id:147639)。

为了建立一个统一的比较基准，[热化学](@entry_id:137688)中采用了一个重要的约定 [@problem_id:2940975]：
**任何元素处于其在指定温度和标准压力下的参考状态（reference state）时，其[标准生成焓](@entry_id:144770)规定为零。**
参考状态通常指该元素最[热力学](@entry_id:141121)稳定的[同素异形体](@entry_id:137177)。例如：
-   在 $298.15 \text{ K}$ 和 $1 \text{ bar}$ 下，碳的参考状态是石墨 (graphite)，因此 $\Delta H_f^\circ(\mathrm{C, graphite}) = 0$。
-   氧的参考状态是氧气 ($\mathrm{O_2(g)}$)，因此 $\Delta H_f^\circ(\mathrm{O_2}, g) = 0$。
-   硫的参考状态是[斜方硫](@entry_id:156206) ($\mathrm{S}(\alpha, \text{rhombic})$)，因此 $\Delta H_f^\circ(\mathrm{S}, \alpha) = 0$。

对于非参考状态的[同素异形体](@entry_id:137177)，其[标准生成焓](@entry_id:144770)不为零，等于由参考状态转化而来时的[焓变](@entry_id:147639)。例如：
-   **金刚石 (diamond)**: $\mathrm{C(graphite)} \to \mathrm{C(diamond)}$ 的[反应焓](@entry_id:149764)为 $+1.90 \text{ kJ/mol}$，因此 $\Delta H_f^\circ(\mathrm{C, diamond}) = +1.90 \text{ kJ/mol}$。
-   **臭氧 (ozone)**: $\tfrac{3}{2}\mathrm{O_2(g)} \to \mathrm{O_3(g)}$ 的[反应焓](@entry_id:149764)为 $+142.7 \text{ kJ/mol}$，因此 $\Delta H_f^\circ(\mathrm{O_3}, g) = +142.7 \text{ kJ/mol}$ [@problem_id:2940975]。
-   **[单斜硫](@entry_id:156632) (monoclinic sulfur)**: $\mathrm{S(\alpha)} \to \mathrm{S(\beta)}$ 的焓变为 $+0.33 \text{ kJ/mol}$，因此 $\Delta H_f^\circ(\mathrm{S}, \beta) = +0.33 \text{ kJ/mol}$ [@problem_id:2940975]。

这个约定的建立，使得所有化合物的[生成焓](@entry_id:139204)都有了一个共同的零点，从而可以方便地进行比较和计算。值得注意的是，由于任何[化学反应](@entry_id:146973)都遵循元素守恒，[反应焓](@entry_id:149764)的计算只涉及[生成焓](@entry_id:139204)的差值，因此这个零点的选择不会影响最终计算出的任何[反应焓](@entry_id:149764)值 [@problem_id:2940975]。

#### 利用[生成焓](@entry_id:139204)计算[反应焓](@entry_id:149764)

[标准生成焓](@entry_id:144770)为我们提供了一个计算任何[反应焓](@entry_id:149764)变的普适公式。我们可以将任何反应想象成一个两步过程：
1.  **分解**：所有反应物分解成其最稳定形式的组成元素。此过程的[焓变](@entry_id:147639)是所有反应物[生成焓](@entry_id:139204)总和的负值。
2.  **生成**：这些元素重新组合成产物。此过程的焓变等于所有产物[生成焓](@entry_id:139204)的总和。

根据[赫斯定律](@entry_id:147875)，总[反应焓](@entry_id:149764)等于这两步的焓变之和，即：
$$
\Delta H_{\text{rxn}}^{\circ} = \sum \nu_p \Delta H_{f}^{\circ}(\text{products}) - \sum \nu_r \Delta H_{f}^{\circ}(\text{reactants})
$$
其中，$\nu_p$ 和 $\nu_r$ 分别是产物和反应物的[化学计量系数](@entry_id:204082)。

**示例：计算氨[合成反应](@entry_id:150159)的[焓变](@entry_id:147639)**
考虑一个替代的[氨合成](@entry_id:153072)路线：$2\mathrm{NO}(g) + 5\mathrm{H}_2(g) \to 2\mathrm{NH}_3(g) + 2\mathrm{H_2O}(l)$ [@problem_id:1984249]。
已知[标准生成焓](@entry_id:144770) ($\text{kJ/mol}$):
$\Delta H_f^\circ[\text{NO}(g)] = +91.26$
$\Delta H_f^\circ[\text{NH}_3(g)] = -45.94$
$\Delta H_f^\circ[\text{H}_2\text{O}(l)] = -285.83$
$\Delta H_f^\circ[\text{H}_2(g)] = 0$ (元素参考态)

应用上述公式：
$$
\Delta H_{\text{rxn}}^{\circ} = [2 \cdot \Delta H_f^\circ(\text{NH}_3, g) + 2 \cdot \Delta H_f^\circ(\text{H}_2\text{O}, l)] - [2 \cdot \Delta H_f^\circ(\text{NO}, g) + 5 \cdot \Delta H_f^\circ(\text{H}_2, g)]
$$
$$
\Delta H_{\text{rxn}}^{\circ} = [2(-45.94) + 2(-285.83)] - [2(91.26) + 5(0)]
$$
$$
\Delta H_{\text{rxn}}^{\circ} = [-91.88 - 571.66] - [182.52] = -663.54 - 182.52 = -846.06 \text{ kJ/mol}
$$
这个计算表明，利用[标准生成焓](@entry_id:144770)数据表，我们可以预测几乎任何[化学反应](@entry_id:146973)的热效应。

#### 利用[反应焓](@entry_id:149764)计算[生成焓](@entry_id:139204)

反之，如果我们能够实验测定一个反应的焓变（例如，通过[量热法](@entry_id:145378)测定[燃烧焓](@entry_id:145539)），并且知道除一种物质外的所有其他物质的[生成焓](@entry_id:139204)，我们就可以利用[赫斯定律](@entry_id:147875)计算这个未知物质的[生成焓](@entry_id:139204)。

**示例1：计算葡萄糖的[生成焓](@entry_id:139204)**
营养学研究中，葡萄糖 ($\mathrm{C_6H_{12}O_6}(s)$) 的[标准生成焓](@entry_id:144770)是一个重要数据。它可以通过精确测量其[燃烧焓](@entry_id:145539)来确定 [@problem_id:1984258]。
[燃烧反应](@entry_id:152943)为：
$$
\mathrm{C_6H_{12}O_6}(s) + 6\mathrm{O_2}(g) \to 6\mathrm{CO_2}(g) + 6\mathrm{H_2O}(l)
$$
实验测得其[标准燃烧焓](@entry_id:182652) $\Delta H_c^\circ = -2805.0 \text{ kJ/mol}$。
已知 ($\text{kJ/mol}$):
$\Delta H_f^\circ[\mathrm{CO_2}(g)] = -393.51$
$\Delta H_f^\circ[\mathrm{H_2O}(l)] = -285.83$
$\Delta H_f^\circ[\mathrm{O_2}(g)] = 0$

设 $\Delta H_f^\circ[\mathrm{C_6H_{12}O_6}(s)] = x$。根据[赫斯定律](@entry_id:147875)：
$$
\Delta H_c^\circ = [6 \cdot \Delta H_f^\circ(\mathrm{CO_2}, g) + 6 \cdot \Delta H_f^\circ(\mathrm{H_2O}, l)] - [1 \cdot \Delta H_f^\circ(\mathrm{C_6H_{12}O_6}, s) + 6 \cdot \Delta H_f^\circ(\mathrm{O_2}, g)]
$$
$$
-2805.0 = [6(-393.51) + 6(-285.83)] - [x + 6(0)]
$$
$$
-2805.0 = [-2361.06 - 1714.98] - x = -4076.04 - x
$$
解得：
$$
x = -4076.04 + 2805.0 = -1271.04 \approx -1271.0 \text{ kJ/mol}
$$

**示例2：综合应用——考虑[物相](@entry_id:196677)校正**
在更复杂的计算中，可能需要结合多种[赫斯定律](@entry_id:147875)的应用技巧。例如，计算甲烷 ($\mathrm{CH_4(g)}$) 的[标准生成焓](@entry_id:144770) [@problem_id:2941004]。
假设我们测得甲烷燃烧生成**气态水**的[反应焓](@entry_id:149764)：
$$
\mathrm{CH_4}(g) + 2\mathrm{O_2}(g) \to \mathrm{CO_2}(g) + 2\mathrm{H_2O}(g), \quad \Delta_r H^\circ = -802.30 \text{ kJ/mol}
$$
而我们拥有的数据通常是**液态水**的[生成焓](@entry_id:139204) $\Delta H_f^\circ(\mathrm{H_2O}, l) = -285.83 \text{ kJ/mol}$，以及水的[汽化焓](@entry_id:141692) $\Delta_{\text{vap}} H^\circ(\mathrm{H_2O}) = +44.01 \text{ kJ/mol}$。

在应用[赫斯定律](@entry_id:147875)公式之前，我们必须首先确保所有物相都匹配。因此，第一步是计算气态水的[标准生成焓](@entry_id:144770)：
$$
\Delta H_f^\circ(\mathrm{H_2O}, g) = \Delta H_f^\circ(\mathrm{H_2O}, l) + \Delta_{\text{vap}} H^\circ(\mathrm{H_2O})
$$
$$
\Delta H_f^\circ(\mathrm{H_2O}, g) = -285.83 + 44.01 = -241.82 \text{ kJ/mol}
$$
现在，我们拥有了所有物相一致的数据，可以计算甲烷的[生成焓](@entry_id:139204)了。设 $\Delta H_f^\circ(\mathrm{CH_4}, g) = y$。
$$
\Delta_r H^\circ = [1 \cdot \Delta H_f^\circ(\mathrm{CO_2}, g) + 2 \cdot \Delta H_f^\circ(\mathrm{H_2O}, g)] - [y + 2 \cdot \Delta H_f^\circ(\mathrm{O_2}, g)]
$$
$$
-802.30 = [-393.51 + 2(-241.82)] - [y + 0]
$$
$$
-802.30 = [-393.51 - 483.64] - y = -877.15 - y
$$
解得：
$$
y = -877.15 + 802.30 = -74.85 \text{ kJ/mol}
$$
这个例子完美地展示了在实际应用[赫斯定律](@entry_id:147875)时，对物态精确性的高度要求，以及如何通过组合[相变](@entry_id:147324)焓和[反应焓](@entry_id:149764)来解决复杂的[热化学](@entry_id:137688)问题。