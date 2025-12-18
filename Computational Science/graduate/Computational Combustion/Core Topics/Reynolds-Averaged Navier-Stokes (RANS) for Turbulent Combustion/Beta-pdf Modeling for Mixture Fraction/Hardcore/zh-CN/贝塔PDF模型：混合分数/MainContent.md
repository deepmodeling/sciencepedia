## 引言
在湍流[燃烧的[数值模](@entry_id:1128991)拟](@entry_id:146043)领域，准确捕捉[湍流](@entry_id:151300)流动与复杂化学反应之间的相互作用是一个持久的中心挑战。直接求解瞬态的化学反应动力学方程在计算上成本极高，因此，发展高效的[降阶模型](@entry_id:754172)至关重要。一种行之有效的方法是引入“守恒标量”的概念，其中**混合分数**（mixture fraction）因其能够简洁地描述燃料与氧化剂的混合状态而备受青睐。然而，由于[化学反应速率](@entry_id:147315)等关键物理量是混合分数的高度[非线性](@entry_id:637147)函数，直接使用时均混合分数进行计算会导致巨大误差，这就是所谓的**封闭问题**。

为了克服这一障碍，我们需要一种能够描述混合分数在[湍流](@entry_id:151300)中瞬时脉动的统计方法。本文聚焦于**Beta概率密度函数（Beta-PDF）模型**，这是一种广泛用于封闭[非预混燃烧](@entry_id:1128819)模型的优雅而强大的工具。通过本文的学习，您将深入理解如何运用这一模型来连接宏观的[湍流统计](@entry_id:200093)量与微观的化学反应过程。

本文分为三个核心章节。在“**原理与机制**”中，我们将从混合分数的定义出发，详细阐述Beta-PDF的数学构造、[参数化](@entry_id:265163)方法及其内在的物理和数学约束。接着，在“**应用与跨学科联系**”中，我们将展示该模型如何在实际的[CFD仿真](@entry_id:747242)中与火焰面模型协同工作，以预测温度场和污染物生成，并探讨其在更高级燃烧模型中的角色。最后，“**动手实践**”部分将通过具体的计算练习，巩固您对模型核心概念的理解和应用能力。

## 原理与机制

在非预混[湍流燃烧](@entry_id:756233)的建模中，将复杂的化学反应与[湍流](@entry_id:151300)流动耦合起来是一个核心挑战。为了简化这一问题，学术界发展了基于**[守恒标量](@entry_id:1122921)**（conserved scalar）的方法。其中，**混合分数**（mixture fraction）是一个关键变量，它描述了流场中任意一点的混合状态。本章将深入探讨混合分数的定义、描述其统计特性的beta-PDF模型，以及该模型在[计算流体动力学](@entry_id:142614)（CFD）中的应用、约束和局限性。

### 混合分数作为[守恒标量](@entry_id:1122921)

为了追踪燃料和氧化剂的混合过程，我们需要一个在化学反应中守恒的量。元素质量分数本身是守恒的，但直接求解每种元素的[输运方程](@entry_id:174281)仍然复杂。一个更优雅的解决方案是构造一个单一的守恒标量，即混合分数 $Z$。

一个广泛使用的定义是 **Bilger混合分数**，它基于元素质量分数构建。考虑一个包含碳（C）、氢（H）和氧（O）元素的系统。Bilger混合分[数基](@entry_id:634389)于一个[线性组合](@entry_id:154743)的标量 $\xi$ 定义，该标量经过精心设计，使其对于主要燃烧产物（如 $\text{CO}_2$ 和 $\text{H}_2\text{O}$）的值为零。其定义如下 ：
$$
\xi = \frac{2Y_C}{W_C} + \frac{1}{2}\frac{Y_H}{W_H} - \frac{Y_O}{W_O}
$$
其中，$Y_C$、$Y_H$ 和 $Y_O$ 分别是局部混合物中碳、氢、氧元素的质量分数，$W_C$、$W_H$ 和 $W_O$ 是它们的[原子量](@entry_id:145035)。由于元素在化学反应中是守恒的，并且在扩散系数相等的假设下，任何元素[质量分数](@entry_id:161575)的[线性组合](@entry_id:154743)都遵循一个没有化学源项的[输运方程](@entry_id:174281)，因此 $\xi$ 是一个守恒标量。

为了使混合分数具有更直观的物理意义，我们将其归一化，使其在纯燃料流（下标 F）中为1，在纯氧化剂流（下标 O）中为0。
$$
Z = \frac{\xi - \xi_O}{\xi_F - \xi_O}
$$
这里，$\xi_F$ 和 $\xi_O$ 分别是纯燃料和纯氧化剂流中的 $\xi$ 值。在理想的两股流[混合模型](@entry_id:266571)中，流场中任意一点的流体都可以看作是来[自燃](@entry_id:1121261)料流和氧化剂流的质量的线性叠加。若某点流体的质量中有 $\alpha$ 的份额来自燃料流，则该点的任何守恒标量的值都是两股初始流的[加权平均值](@entry_id:894528)：$\xi = \alpha \xi_F + (1-\alpha) \xi_O$。将此关系代入 $Z$ 的定义，我们得到 $Z = \alpha$。由于质量份额 $\alpha$ 必须在 $[0, 1]$ 区间内，因此混合分数 $Z$ 的值也被严格限制在 **[0, 1]** 区间内，这一特性与化学反应的状态无关 。

在CFD模拟中，我们求解的是混合分数的平均[输运方程](@entry_id:174281)。对于[可压缩流](@entry_id:747589)，通常使用**[法夫尔平均](@entry_id:198824)**（Favre averaging），定义为 $\tilde{\phi} = \overline{\rho \phi} / \bar{\rho}$，其中 $\rho$ 是密度，上划线代表[雷诺平均](@entry_id:754341)。[Favre平均](@entry_id:198824)的混合分数 $\tilde{Z}$ 的[输运方程](@entry_id:174281)（在[保守形式](@entry_id:747710)下）为 ：
$$
\frac{\partial (\bar{\rho}\tilde{Z})}{\partial t} + \nabla \cdot (\bar{\rho}\tilde{\boldsymbol{u}}\tilde{Z}) = \nabla \cdot \left[ \left(\bar{\rho}D + \frac{\mu_t}{Sc_t}\right) \nabla \tilde{Z} \right]
$$
左侧的第二项代表**对流**（convection），右侧代表**扩散**（diffusion），包括分子扩散（由[分子扩散系数](@entry_id:752110) $D$ 描述）和[湍流扩散](@entry_id:1133505)（由[湍流](@entry_id:151300)粘度 $\mu_t$ 和[湍流施密特数](@entry_id:150226) $Sc_t$ 描述）。重要的是，由于 $Z$ 是守恒标量，这个方程中没有**产生产**（production）或源项。

### [湍流](@entry_id:151300)波动与概率密度函数（PDF）

求解了平均混合分数 $\tilde{Z}$ 之后，我们面临一个新的问题：在[湍流燃烧](@entry_id:756233)中，许多关键物理量，如物种[质量分数](@entry_id:161575) $Y_i$ 和化学反应速率 $\dot{\omega}$，是混合分数 $Z$ 的高度[非线性](@entry_id:637147)函数。直接使用平均混合分数来计算这些量的平均值，例如，近似 $\tilde{Y}_i \approx Y_i(\tilde{Z})$，会引入巨大的误差。这被称为**封闭问题**（closure problem）。

为了正确计算平均值，我们必须考虑混合分数在[湍流](@entry_id:151300)中的**亚格子尺度脉动**（subgrid-scale fluctuations）。这通过引入混合分数的**概率密度函数**（Probability Density Function, PDF），记作 $p(\zeta)$，来实现。PDF描述了在某个时空点上，瞬时混合分数 $Z$ 取值为 $\zeta$ 的概率。

任何标量 $\phi$ 的[Favre平均](@entry_id:198824)值可以通过对其条件平均值（给定 $Z = \zeta$ 时的平均值，记作 $\langle \phi | Z=\zeta \rangle$）在 $Z$ 的所有可能值上进行加权积分得到。这个权重就是[Favre平均](@entry_id:198824)的PDF，$\tilde{p}(\zeta)$。对于物种[质量分数](@entry_id:161575) $Y_i$，其平均值为 ：
$$
\tilde{Y}_i = \int_0^1 \langle Y_i | Z=\zeta \rangle \tilde{p}(\zeta) d\zeta
$$
这里的 $\tilde{p}(\zeta)$ 是通过 $\tilde{p}(\zeta) = \overline{\rho \delta(Z-\zeta)} / \bar{\rho}$ 定义的质量加权PDF，其中 $\delta$ 是[狄拉克δ函数](@entry_id:153299)。在**火焰面模型**（flamelet model）中，$\langle Y_i | Z=\zeta \rangle$ 通常被简化为仅由 $Z$ 决定的函数 $Y_i(\zeta)$，该函数关系可以从一维层流火焰的计算中预先获得。

对于像[化学反应速率](@entry_id:147315) $\dot{\omega}(Z)$ 这样的高度[非线性](@entry_id:637147)函数，PDF的作用尤为关键 ：
$$
\tilde{\dot{\omega}} = \int_0^1 \dot{\omega}(\zeta) \tilde{p}(\zeta) d\zeta
$$
这个积分形式明确显示，平均[反应速率](@entry_id:185114)不仅取决于平均混合状态 $\tilde{Z}$，还强烈地依赖于 $Z$ 的脉动分布形态，即 $p(Z)$ 的形状。

### Beta-PDF模型

为了在CFD模拟中实际使用上述积分，我们需要一个具体的 $p(Z)$ 的数学模型。**Beta分布**（Beta distribution）是一个理想的选择，原因如下 ：

1.  **物理边界**：Beta分布的支撑集恰好是 $[0, 1]$，与混合分数的物理取值范围完全一致。
2.  **形状灵活性**：Beta分布有两个[形状参数](@entry_id:270600) $\alpha$ 和 $\beta$，通过调整这两个参数，它可以呈现出多种形状，包括对称的钟形、偏斜的峰形、J形或U形，能够灵活地模拟不同[湍流混合](@entry_id:202591)状态下的 $Z$ 分布。

Beta-PDF的数学形式为 ：
$$
p(\zeta; \alpha, \beta) = \frac{\zeta^{\alpha-1}(1-\zeta)^{\beta-1}}{B(\alpha, \beta)}
$$
其中，$\alpha > 0$ 和 $\beta > 0$ 是[形状参数](@entry_id:270600)。分母中的 $B(\alpha, \beta)$ 是**Beta函数**，作为[归一化常数](@entry_id:752675)，它通过**Gamma函数** $\Gamma(\cdot)$ 定义：
$$
B(\alpha, \beta) = \int_0^1 t^{\alpha-1}(1-t)^{\beta-1} dt = \frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}
$$

### [参数化](@entry_id:265163)：[矩量法](@entry_id:277025)

为了使用Beta-PDF，我们必须确定其两个参数 $\alpha$ 和 $\beta$。标准方法是**[矩量法](@entry_id:277025)**（method of moments），即选择 $\alpha$ 和 $\beta$，使得Beta分布的前两个[中心矩](@entry_id:270177)——**平均值** $\tilde{Z}$ 和**方差** $\widetilde{Z''^2}$——与[CFD模型](@entry_id:747239)中求解的相应值相匹配。

Beta分布的平均值和方差可以表示为 $\alpha$ 和 $\beta$ 的函数：
$$
\tilde{Z} = \frac{\alpha}{\alpha+\beta}
$$
$$
\widetilde{Z''^2} = \frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}
$$
在[CFD应用](@entry_id:144462)中，我们需要的是[逆关系](@entry_id:274206)：由已知的 $\tilde{Z}$ 和 $\widetilde{Z''^2}$ 来计算 $\alpha$ 和 $\beta$。通过代数运算，可以得到以下求解公式 ：
$$
\alpha = \tilde{Z} \left( \frac{\tilde{Z}(1-\tilde{Z})}{\widetilde{Z''^2}} - 1 \right)
$$
$$
\beta = (1-\tilde{Z}) \left( \frac{\tilde{Z}(1-\tilde{Z})}{\widetilde{Z''^2}} - 1 \right)
$$
这组公式是Beta-PDF模型的核心计算工具。例如，对于一个平均混合分数为 $\tilde{Z}=0.3$，方差为 $\widetilde{Z''^2}=0.015$ 的情况，我们可以计算出参数为 $\alpha=3.9$ 和 $\beta=9.1$。

### 模型的物理和数学约束：可实现性

并非任意的平均值和方差组合都能对应一个有效的Beta分布。这个约束被称为**可实现性**（realizability）。

首先，对于任何一个定义在 $[0, 1]$ 区间内的[随机变量](@entry_id:195330) $Z$，其方差 $\sigma^2$ 和平均值 $\mu$ 必须满足一个普适的不等式 ：
$$
\sigma^2 \le \mu(1-\mu)
$$
这个不等式的物理意义在于，对于给定的平均混合状态 $\mu$，方差存在一个上限。当等号成立时，$\sigma^2 = \mu(1-\mu)$，这对应于一个完全**分离**（segregated）的混合物，其中只存在纯燃料（$Z=1$）和纯氧化剂（$Z=0$），其概率分别为 $\mu$ 和 $1-\mu$。任何分子层面的混合（即产生 $0  Z  1$ 的状态）都会使方差减小。

其次，为了让Beta-PDF的参数 $\alpha$ 和 $\beta$ 为正值（这是分布有效的必要条件），上述不等式必须是严格的 [@problem_id:4009932, @problem_id:4009845, @problem_id:4009878]：
$$
\widetilde{Z''^2}  \tilde{Z}(1-\tilde{Z})
$$
这个**[可实现性](@entry_id:193701)条件**在[数值模拟](@entry_id:146043)中至关重要。在求解 $\alpha$ 和 $\beta$ 之前，必须检查从[输运方程](@entry_id:174281)得到的 $\tilde{Z}$ 和 $\widetilde{Z''^2}$ 是否满足此条件。例如，若 $\tilde{Z}=0.2$，则方差的上限为 $0.2 \times 0.8 = 0.16$。如果计算得到的方差为 $\widetilde{Z''^2}=0.05$，由于 $0.05  0.16$，模型是可实现的，可以计算出相应的 $\alpha=0.44$ 和 $\beta=1.76$ 。

Beta-PDF的形状与方差的大小密切相关。当方差趋于零（$\widetilde{Z''^2} \to 0$）时，PDF会变得无限窄，极限情况下成为一个在平均值处的**[狄拉克δ函数](@entry_id:153299)** $\delta(\zeta-\tilde{Z})$，代表均匀混合。当方差趋于其最大值（$\widetilde{Z''^2} \to \tilde{Z}(1-\tilde{Z})$）时，PDF的质量会向两个端点 $Z=0$ 和 $Z=1$ 集中，极限情况下成为一个两点**[伯努利分布](@entry_id:266933)**，代表完全分离 。

### 矩的[输运方程](@entry_id:174281)模型

Beta-PDF模型需要 $\tilde{Z}$ 和 $\widetilde{Z''^2}$ 作为输入。如前所述，$\tilde{Z}$ 由其自身的[输运方程](@entry_id:174281)确定。那么，方差 $\widetilde{Z''^2}$ 是如何得到的呢？在RANS或LES框架下，我们同样可以为其建立一个[输运方程](@entry_id:174281)。

对于 $\widetilde{Z''^2}$，其[输运方程](@entry_id:174281)（忽略输运项后）的核心是**产生**和**耗散**之间的平衡 ：
$$
\text{产生} = \text{耗散}
$$
方差的**产生项** $P_Z$ 主要来自于[湍流](@entry_id:151300)脉动与平均混合分数梯度的相互作用，其精确形式为 $P_Z = -2 \overline{\rho \boldsymbol{u}'' Z''} \cdot \nabla \tilde{Z}$。采用梯度扩散假设 ($\overline{\rho \boldsymbol{u}'' Z''} = - \rho \frac{\nu_t}{Sc_t} \nabla \tilde{Z}$) 后，产生项可以模型化为：
$$
P_Z \approx 2 \rho \frac{\nu_t}{Sc_t} |\nabla \tilde{Z}|^2
$$
方差的**耗散项** $D_Z$ 是由于分子扩散在微小尺度上“抹平”了混合分数的梯度，导致脉动减弱。这个过程由**[标量耗散率](@entry_id:754534)** $\tilde{\chi}$ 来量化，其定义为 $\tilde{\chi} = 2D \widetilde{|\nabla Z|^2}$。在标准模型中，标量耗散率与方差本身、湍动能 $k$ 及其耗散率 $\varepsilon$ 相关联：
$$
D_Z = \rho \tilde{\chi} \approx \rho C_{\chi} \frac{\varepsilon}{k} \widetilde{Z''^2}
$$
其中 $C_{\chi}$ 是一个模型常数。

在[局部平衡](@entry_id:156295)的假设下（即产生等于耗散），我们可以得到一个关于 $\widetilde{Z''^2}$ 的代数表达式。例如，在均匀剪切流中，其中平均梯度为 $G=|\nabla \tilde{Z}|$，通过联立上述模型，可以解出方差 ：
$$
\widetilde{Z''^2} = \frac{2 C_{\mu}}{C_{\chi} Sc_{t}} \frac{k^3}{\varepsilon^2} G^2
$$
其中 $C_{\mu}$ 是[湍流](@entry_id:151300)粘度模型中的常数。这个方程将混合分数方差与流场的主导[湍流](@entry_id:151300)参数（$k$, $\varepsilon$）和平均混合梯度联系起来，从而为Beta-PDF模型提供了第二个必要的输入，实现了模型的封闭。

### 模型的应用与局限性

#### [非线性](@entry_id:637147)平均的影响

Beta-PDF模型的一个主要用途是对[非线性](@entry_id:637147)函数进行平均，如[反应速率](@entry_id:185114) $\dot{\omega}(Z)$。通过对 $\dot{\omega}(Z)$ 在平均值 $\tilde{Z}$ 附近进行泰勒展开，我们可以更清楚地看到[湍流](@entry_id:151300)脉动的影响 ：
$$
\tilde{\dot{\omega}} = \int_0^1 \dot{\omega}(\zeta) p(\zeta) d\zeta \approx \dot{\omega}(\tilde{Z}) + \frac{1}{2}\dot{\omega}''(\tilde{Z})\widetilde{Z''^2} + \dots
$$
这个展开式揭示了，与简单的平均场近似 $\dot{\omega}(\tilde{Z})$ 相比，平均[反应速率](@entry_id:185114)有一个由方差 $\widetilde{Z''^2}$ 贡献的修正项。如果 $\dot{\omega}(Z)$ 是一个**凸函数**（$\dot{\omega}'' > 0$），[湍流](@entry_id:151300)脉动会**增加**平均[反应速率](@entry_id:185114)；如果是**[凹函数](@entry_id:274100)**（$\dot{\omega}''  0$），则会**减小**平均[反应速率](@entry_id:185114)。这直接体现了**[詹森不等式](@entry_id:144269)**（Jensen's inequality）的效应。

此外，平均值的大小还取决于PDF $p(\zeta)$ 和函数 $\dot{\omega}(\zeta)$ 形状的**重叠程度**。例如，[化学反应速率](@entry_id:147315)通常在[化学计量](@entry_id:137450)混合分数 $Z_{st}$ 附近达到峰值。如果PDF的峰值（模态）也位于 $Z_{st}$ 附近，则积分得到的 $\tilde{\dot{\omega}}$ 会较大。相反，如果PDF是U形的，将大部分概率分布在 $Z=0$ 和 $Z=1$ 的贫燃和富燃区域，而这些区域的 $\dot{\omega}(\zeta)$ 很小，那么即使平均值 $\tilde{Z}$ 可能接近 $Z_{st}$，计算出的 $\tilde{\dot{\omega}}$ 也会被严重低估 。

#### 差示扩散的挑战

混合分数守恒的假设依赖于所有相关物种具有相同的扩散系数。然而在现实中，不同物种的分子扩散速率不同，特别是轻质物种（如 $\text{H}_2$）的扩散远快于重质物种。这种**差示扩散**（differential diffusion）效应会破坏Bilger混合分数的守恒性。

当物种扩散系数 $D_i$ 不相等时，元素通量的总和不再能简化为单一Fickian扩散形式，这导致在混合分数的[输运方程](@entry_id:174281)中出现一个非零的“源项” $S_{dd}$ 。
$$
\nabla \cdot (\rho \boldsymbol{u} \beta) = \nabla \cdot (\text{复杂扩散通量}) \neq \nabla \cdot (\rho D_{\text{ref}} \nabla \beta)
$$
这个效应的强度取决于燃料类型。对于甲烷-空气火焰，主要物种的扩散系数差异不大，差示扩散引入的误差相对较小，通常在百分之几的量级。然而，对于氢气-空气火焰，由于 $\text{H}_2$ 的扩散系数比其他物种大数倍，差示扩散效应非常显著，可能导致百分之几十甚至更高的误差，严重影响了标准混合分数方法的准确性 。

#### 复杂分布形态的局限性

最后，标准的单峰Beta-PDF模型在描述某些复杂流动结构时存在固有的数学局限性。通过对其导数分析可知，一个标准的Beta分布最多只能有一个**内部峰值**（即在 $(0, 1)$ 区间内的模态）。它可以是单峰的，也可以是J形或U形（峰值在边界上），但绝不可能在 $(0, 1)$ 内部呈现两个或更多的峰值 。

然而，在一些复杂的流动中，例如**横流中的射流**（jet-in-crossflow），在某些空间位置，瞬时混合分数的测量值可能呈现出**[双峰分布](@entry_id:166376)**。这通常反映了该点间歇性地被来自两条不同路径的流体（例如，直接来自射流核心的流体和与横流充分混合的流体）扫过。

为了模拟这种[双峰分布](@entry_id:166376)，单一Beta-PDF是[无能](@entry_id:201612)为力的。一个自然的扩展是采用**混合Beta模型**（mixture-of-betas model），它将总PDF表示为两个或多个Beta分布的加权和：
$$
p(Z) = w \cdot \text{Beta}(Z; \alpha_1, \beta_1) + (1-w) \cdot \text{Beta}(Z; \alpha_2, \beta_2)
$$
其中 $w$ 是权重因子。通过选择两组参数，使得每个分量Beta分布都是单峰的，但它们的峰值位置不同，这个混合模型就能够有效地生成一个具有两个内部峰值的[双峰分布](@entry_id:166376)，同时仍然保持 $Z$ 在 $[0, 1]$ 范围内的物理约束 。这为模拟更复杂的湍流混合场提供了更强大的工具。