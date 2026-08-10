## 引言
链式反应是化学动力学中的一[类核](@keyword=nucleoid|lang=zh-CN|style=Feynman)心[反应机理](@keyword=reaction_mechanisms|lang=zh-CN|style=Feynman)，其独特的自我传播和放大效应使其在燃烧、[高分子](@keyword=macromolecules|lang=zh-CN|style=Feynman)合成、[大气化学](@keyword=atmospheric_chemistry|lang=zh-CN|style=Feynman)乃至生命科学中扮演着至关重要的角色。与简单的[基元反应](@keyword=elementary_reactions|lang=zh-CN|style=Feynman)不同，链式反应展现出复杂的动力学行为，例如非整数的反应级数和爆炸现象，这为初学者理解其内在规律带来了挑战。本文旨在填补这一知识鸿沟，系统性地阐明链式反应的本质。

在接下来的内容中，读者将循序渐进地掌握链式反应的完整图景。第一章“原理与机制”将剖析链式反应的基本构成——[链引发](@keyword=chain_initiation|lang=zh-CN|style=Feynman)、[链增长](@keyword=chain_propagation|lang=zh-CN|style=Feynman)和[链终止](@keyword=chain_termination|lang=zh-CN|style=Feynman)，并介绍稳态近似等核心分析工具。第二章“应用与[交叉](@keyword=chiasmata|lang=zh-CN|style=Feynman)学科联系”将展示这些理论如何应用于[高分子化学](@keyword=polymer_chemistry|lang=zh-CN|style=Feynman)、[燃烧科学](@keyword=combustion_science|lang=zh-CN|style=Feynman)和生物技术等前沿领域，揭示其广泛的实践价值。最后，在“动手实践”部分，你将有机会通过解决具体问题来巩固所学知识。让我们首先深入链式反应的内部，探索其精巧的原理与机制。

## 原理与机制

链式反应是化学动力学中一[类核](@keyword=nucleoid|lang=zh-CN|style=Feynman)心的复合反应机理，广泛存在于燃烧、聚合、[大气化学](@keyword=atmospheric_chemistry|lang=zh-CN|style=Feynman)和生物化学等众多领域。与逐级发生的反应不同，链式反应通过一小部分高活性中间体（称为[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)）的循环再生，实现反应的自我传播和放大。本章将深入探讨链式反应的基本原理、动力学特征以及由此产生的各种复杂现象。

### 链式反应的基本构成

一个典型的[链式反应机理](@keyword=chain_reaction_mechanism|lang=zh-CN|style=Feynman)可以分解为三个基本阶段：**[链引发](@keyword=chain_initiation|lang=zh-CN|style=Feynman) (initiation)**、**[链增长](@keyword=chain_propagation|lang=zh-CN|style=Feynman) (propagation)** 和 **[链终止](@keyword=chain_termination|lang=zh-CN|style=Feynman) (termination)**。理解这三个阶段中活性物种的生成与消耗，是掌握[链式反应动力学](@keyword=chain_reaction_kinetics|lang=zh-CN|style=Feynman)的关键。

**[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman) (Chain Carriers)** 是指在链式反应过程中起着传递和延续反应链作用的高[活性中间体](@keyword=reactive_intermediates|lang=zh-CN|style=Feynman)。它们通常是具有[未成对电子](@keyword=unpaired_electrons|lang=zh-CN|style=Feynman)的**[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman) (free radicals)** 或原子。由于其不稳定的电子构型，[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)具有极高的反应活性，能够迅速与稳定的反应物分子作用，从而推动反应链的进行。例如，在乙醛 ($\text{CH}_3\text{CHO}$) 的气相热[分解反应](@keyword=decomposition_reaction|lang=zh-CN|style=Feynman)中，甲基[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman) ($\text{CH}_3^\bullet$) 和乙酰甲基[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman) ($\text{CH}_2\text{CHO}^\bullet$) 就是关键的[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)。它们在一个[链增长步骤](@keyword=propagation_step|lang=zh-CN|style=Feynman)中被消耗，又在另一个[链增长步骤](@keyword=propagation_step|lang=zh-CN|style=Feynman)中被重新生成，构成了一个[催化循环](@keyword=catalytic_cycles|lang=zh-CN|style=Feynman)，从而将稳定的乙醛分子转化为最终产物甲烷 ($\text{CH}_4$) 和一氧化碳 ($\text{CO}$) [@problem_id:1476674]。

链式反应的三个基本步骤可以通过[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)数量的净变化来明确区分 [@problem_id:1476668]：

1.  **[链引发](@keyword=chain_initiation|lang=zh-CN|style=Feynman)**：此步骤从稳定的非[自由基反应](@keyword=radical_reactions|lang=zh-CN|style=Feynman)物中**净生成**[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)。这是反应链的起点。由于该过程通常涉及稳定[化学键](@keyword=chemical_bonding|lang=zh-CN|style=Feynman)的断裂，因此需要相当大的能量输入，例如通过加热（热引发）或光照（[光引发](@keyword=photoinitiation|lang=zh-CN|style=Feynman)）。一个典型的[链引发](@keyword=chain_initiation|lang=zh-CN|style=Feynman)步骤是分子的均裂，例如：
    $M_2 \rightarrow 2M^\bullet$
    在此过程中，[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)的数量从 $0$ 增加到 $2$。

2.  **[链增长](@keyword=chain_propagation|lang=zh-CN|style=Feynman)**：此步骤消耗一个[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)，但同时会生成一个或多个新的[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)，使得反应链得以延续。在最常见的**直链反应 (straight-chain reaction)** 中，每个[链增长步骤](@keyword=propagation_step|lang=zh-CN|style=Feynman)消耗一个[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)，同时生成一个[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)，[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)的总数保持不变。这使得[反应能](@keyword=reaction_energy|lang=zh-CN|style=Feynman)够以循环的方式持续进行，将反应物转化为产物。例如：
    $M^\bullet + N_2 \rightarrow MN + N^\bullet$
    在这个例子中，一个 $M^\bullet$ [自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)被消耗，但同时生成了一个 $N^\bullet$ [自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)，[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)的数量净变化为零。

3.  **[链终止](@keyword=chain_termination|lang=zh-CN|style=Feynman)**：此步骤**净消耗**[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)，导致反应链的中断。这通常通过两个[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)相互反应形成一个稳定的分子来实现，或者通过[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)与容器壁或杂质反应而被“捕获”。例如：
    $M^\bullet + N^\bullet \rightarrow MN$
    在此过程中，两个[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)结合，使其总数从 $2$ 减少到 $0$。

### 链式反应的动力学特征

链式反应的整体速率和效率由其各个基本步骤的速率常数共同决定。其中，引发、增长和[终止步骤](@keyword=termination_step|lang=zh-CN|style=Feynman)的活化能差异巨大，从而赋予了链式反应独特的动力学行为。

#### [链引发](@keyword=chain_initiation|lang=zh-CN|style=Feynman)的能垒与[链终止](@keyword=chain_termination|lang=zh-CN|style=Feynman)的无能垒特性

[链引发](@keyword=chain_initiation|lang=zh-CN|style=Feynman)步骤的本质是破坏稳定的[化学键](@keyword=chemical_bonding|lang=zh-CN|style=Feynman)以产生高活性的[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)。因此，其**活化能 ($E_a$)** 通常很高，数值上约等于被断裂化学键的**[键解离能](@keyword=bond_dissociation_energy|lang=zh-CN|style=Feynman) (Bond Dissociation Energy, BDE)**。例如，在甲烷 ($\text{CH}_4$) 与氯气 ($\text{Cl}_2$) 的热引发氯代反应中，可能的引发步骤是 $Cl-Cl$ 键或 $C-H$ 键的断裂。由于 $Cl-Cl$ 键的BDE（约 $243 \text{ kJ/mol}$）远低于 $C-H$ 键的BDE（约 $439 \text{ kJ/mol}$），因此在加热条件下，能量上最可行的引发步骤是氯气分子的均裂 [@problem_id:1476663]。

根据[阿伦尼乌斯方程](@keyword=arrhenius_equation|lang=zh-CN|style=Feynman) $k = A \exp(-E_a / RT)$，高活化能意味着引发步骤的速率常数对温度高度敏感，并且在室温下通常非常小。只有在足够高的温度下，才能获得可观的引发速率，从而“启动”整个链式反应。例如，假设一个典型的指前因子 $A = 2.0 \times 10^{13} \text{ s}^{-1}$，要使 $\text{Cl}_2$ 分解的[速率常数](@keyword=rate_constants|lang=zh-CN|style=Feynman)达到一个微小的阈值 $1.0 \times 10^{-5} \text{ s}^{-1}$，所需的温度 $T$ 可以计算得出：
$T = \frac{E_a}{R \ln(A/k_{\text{init}})} = \frac{243 \times 10^3 \text{ J/mol}}{8.314 \mathrm{J/(mol\cdot K)} \times \ln\left(\frac{2.0 \times 10^{13}}{1.0 \times 10^{-5}}\right)} \approx 694 \text{ K}$
这表明，没有足够的热能输入，链式反应甚至无法开始。

与此形成鲜明对比的是，链[终止步骤](@keyword=termination_step|lang=zh-CN|style=Feynman)，特别是两个[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)结合成稳定分子的反应（如 $R^\bullet + R^\bullet \rightarrow R_2$），其活化能通常非常小，接近于零 [@problem_id:1476678]。其根本原因在于，该过程仅涉及新[化学键](@keyword=chemical_bonding|lang=zh-CN|style=Feynman)的形成，而无需断裂任何已有的[化学键](@keyword=chemical_bonding|lang=zh-CN|style=Feynman)。当两个带有未成对电子的[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)相互靠近时，它们的电子可以配对形成成键轨道，导致体系的[势能](@keyword=energy_potential|lang=zh-CN|style=Feynman)单调下降，直至形成稳定的[化学键](@keyword=chemical_bonding|lang=zh-CN|style=Feynman)。整个[反应路径](@keyword=reaction_path|lang=zh-CN|style=Feynman)上不存在能量势垒，因此[反应速率](@keyword=reaction_rate|lang=zh-CN|style=Feynman)极快，通常仅受限于[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)在介质中的[扩散](@keyword=diffusion|lang=zh-CN|style=Feynman)速率。

#### 稳态近似与分数反应级数

[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)（[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)）具有极高的反应活性，一旦生成就会迅速参与后续反应。因此，在链式反应开始后极短的时间内，其浓度会达到一个非常低但近似恒定的值。这一特性是应用**[稳态近似](@keyword=steady_state_approximation|lang=zh-CN|style=Feynman) (Steady-State Approximation, SSA)** 的基础。稳态近似假设[活性中间体](@keyword=reactive_intermediates|lang=zh-CN|style=Feynman)的生成速率等于其消耗速率，从而使其净变化率为零，即 $\frac{d[R^\bullet]}{dt} \approx 0$。

稳态近似是分析[链式反应动力学](@keyword=chain_reaction_kinetics|lang=zh-CN|style=Feynman)的强大工具，它能够将复杂的微分方程组转化为[代数方程](@keyword=algebraic_equations|lang=zh-CN|style=Feynman)组，从而推导出总反应的速率方程。一个重要的推论是，链式反应的宏观反应级数通常不是简单的整数，而是**分数级数 (fractional order)**。

考虑一个假设的[链式反应机理](@keyword=chain_reaction_mechanism|lang=zh-CN|style=Feynman) [@problem_id:1476694]：
1.  **引发**: $M \xrightarrow{k_i} 2 R^\bullet$ （速率为 $k_i[M]$）
2.  **增长**: $R^\bullet + M \xrightarrow{k_p} P + R^\bullet$ （速率为 $k_p[R^\bullet][M]$）
3.  **终止**: $R^\bullet + R^\bullet \xrightarrow{k_t} \text{稳定产物}$ （速率为 $k_t[R^\bullet]^2$）

对[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman) $R^\bullet$ 应用[稳态近似](@keyword=steady_state_approximation|lang=zh-CN|style=Feynman)：
$\frac{d[R^\bullet]}{dt} = 2k_i[M] - 2k_t[R^\bullet]^2 \approx 0$

从此方程中解出[稳态](@keyword=steady_states|lang=zh-CN|style=Feynman)时的[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)浓度 $[R^\bullet]_{ss}$：
$[R^\bullet]_{ss} = \left(\frac{k_i}{k_t}\right)^{1/2} [M]^{1/2}$

总产物 $P$ 的生成速率由[链增长步骤](@keyword=propagation_step|lang=zh-CN|style=Feynman)决定：
$\frac{d[P]}{dt} = k_p[R^\bullet]_{ss}[M]$

将 $[R^\bullet]_{ss}$ 的表达式代入，我们得到总反应的速率方程：
$\frac{d[P]}{dt} = k_p \left(\frac{k_i}{k_t}\right)^{1/2} [M]^{1/2} [M] = k_p \left(\frac{k_i}{k_t}\right)^{1/2} [M]^{3/2}$

这个结果清晰地表明，尽管所有[基元步骤](@keyword=elementary_steps|lang=zh-CN|style=Feynman)都是简单的单分子或[双分子反应](@keyword=bimolecular_reactions|lang=zh-CN|style=Feynman)，但最终的宏观速率方程对反应物 $M$ 的级数却是 $3/2$。这种分数级数是[链式反应机理](@keyword=chain_reaction_mechanism|lang=zh-CN|style=Feynman)的一个标志性特征。

#### 链长与反应效率

**[动力学链长](@keyword=kinetic_chain_length|lang=zh-CN|style=Feynman) (kinetic chain length, $\nu$)** 是衡量链式反应效率的关键参数，定义为[链增长](@keyword=chain_propagation|lang=zh-CN|style=Feynman)反应的速率与[链引发](@keyword=chain_initiation|lang=zh-CN|style=Feynman)反应的速率之比：
$\nu = \frac{\text{Rate of propagation}}{\text{Rate of initiation}}$

链长代表了平均每个引发事件（即产生初始[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)的事件）能够引发多少次[链增长](@keyword=chain_propagation|lang=zh-CN|style=Feynman)循环，从而生成多少个产物分子。一个长的链长 ($\nu \gg 1$) 意味着链式反应非常高效，少量的引发就能导致大量反应物的转化。

链式反应的整体效率不仅取决于引发的难易，更关键的是[链增长步骤](@keyword=propagation_step|lang=zh-CN|style=Feynman)的速率。如果[链增长步骤](@keyword=propagation_step|lang=zh-CN|style=Feynman)本身具有很高的活化能 $E_{a,p}$，那么即使引发速率很高，[链增长](@keyword=chain_propagation|lang=zh-CN|style=Feynman)的[速率常数](@keyword=rate_constants|lang=zh-CN|style=Feynman) $k_p$ 也会很小。这将导致两个后果 [@problem_id:1476676]：
1.  **链长很短**：根据定义，小的 $k_p$ 直接导致了短的链长 $\nu$。这意味着[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)在有机会进行多次增长循环之前，就通过[终止步骤](@keyword=termination_step|lang=zh-CN|style=Feynman)被消耗掉了。
2.  **总产物生成速率低**：由于产物是在[链增长步骤](@keyword=propagation_step|lang=zh-CN|style=Feynman)中生成的，缓慢的[链增长](@keyword=chain_propagation|lang=zh-CN|style=Feynman)自然导致了缓慢的产物生成。

因此，一个高效的链式反应需要一个相对容易的引发步骤和一个活化能非常低的快速[链增长步骤](@keyword=propagation_step|lang=zh-CN|style=Feynman)。

此外，链长的概念也与稳态近似的有效性密切相关。[稳态近似](@keyword=steady_state_approximation|lang=zh-CN|style=Feynman)的核心前提是中间体浓度远低于反应物浓度。可以证明，中间体[稳态](@keyword=steady_states|lang=zh-CN|style=Feynman)浓度与反应物初始浓度之比 $\frac{[R^\bullet]_{ss}}{[M_0]}$ 与链长成反比 [@problem_id:1476682]。具体来说，对于上述模型，可以推导出：
$\frac{[R^\bullet]_{ss}}{[M_0]} = \frac{k_p}{\nu_0 k_t}$
其中 $\nu_0$ 是初始链长。这个关系表明，链长越长（$\nu_0$ 越大），[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)的相对浓度就越低，[稳态近似](@keyword=steady_state_approximation|lang=zh-CN|style=Feynman)也就越准确。

### 链式反应的复杂现象

基于上述基本原理，链式反应可以表现出一些更为复杂的动力学行为，如诱导期、爆炸和抑制。

#### 诱导期

许多链式反应在开始阶段，产物的生成速率非常缓慢，几乎为零，经过一段时间后，[反应速率](@keyword=reaction_rate|lang=zh-CN|style=Feynman)才迅速增加到某个稳定值。这段初始的静默期被称为**诱导期 (induction period)**。其根本原因是反应开始时，体系中没有[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)，需要一定时间让[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)的浓度通过引发步骤逐渐累积，直至达到其[稳态](@keyword=steady_states|lang=zh-CN|style=Feynman)浓度 [@problem_id:1476690]。

在反应极早期，由于[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)浓度 $[R]$ 非常低，[终止步骤](@keyword=termination_step|lang=zh-CN|style=Feynman)（速率 $\propto [R]^2$）可以忽略不计，[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)的浓度主要由引发步骤决定。此时，[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)浓度的变化率近似为：
$\frac{d[R]}{dt} \approx 2k_i[M]_0$
积分可得，在诱导期内，[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)浓度随时间[线性增长](@keyword=linear_growth|lang=zh-CN|style=Feynman)：
$[R](t) \approx 2k_i[M]_0 t$
由于产物生成速率正比于 $[R]$，因此在诱导期内，[反应速率](@keyword=reaction_rate|lang=zh-CN|style=Feynman)也从零开始缓慢增加，直到 $[R]$ 达到[稳态](@keyword=steady_states|lang=zh-CN|style=Feynman)值后，[反应速率](@keyword=reaction_rate|lang=zh-CN|style=Feynman)才趋于稳定。

#### [链支化](@keyword=chain_branching|lang=zh-CN|style=Feynman)与爆炸

在某些链式反应中，存在一种特殊的[链增长步骤](@keyword=propagation_step|lang=zh-CN|style=Feynman)，称为**[链支化](@keyword=chain_branching|lang=zh-CN|style=Feynman) (chain branching)**。在这种步骤中，一个[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)反应后会生成超过一个[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)，导致[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)数量呈指数级增长。例如：
$A^\bullet + B \rightarrow P + 2A^\bullet$

[链支化](@keyword=chain_branching|lang=zh-CN|style=Feynman)是导致**化学爆炸 (chemical explosion)** 的核心机制。当[链支化](@keyword=chain_branching|lang=zh-CN|style=Feynman)产生[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)的速率超过[链终止](@keyword=chain_termination|lang=zh-CN|style=Feynman)消耗[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)的速率时，体系中的[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)浓度会急剧增加，从而使总[反应速率](@keyword=reaction_rate|lang=zh-CN|style=Feynman)在瞬间增大到近乎无限，宏观上表现为爆炸。

考虑一个包含[链支化](@keyword=chain_branching|lang=zh-CN|style=Feynman)的简单机理 [@problem_id:1476672]：
1.  **引发**: $A_2 \xrightarrow{k_i} 2A^\bullet$
2.  **支化**: $A^\bullet + B \xrightarrow{k_b} P + 2A^\bullet$
3.  **终止**: $A^\bullet \xrightarrow{k_t} Q$

对 $A^\bullet$ 应用[稳态近似](@keyword=steady_state_approximation|lang=zh-CN|style=Feynman)，可得其[稳态](@keyword=steady_states|lang=zh-CN|style=Feynman)浓度和产物生成速率：
$[A^\bullet]_{ss} = \frac{2k_i[A_2]}{k_t - k_b[B]}$
$\frac{d[P]}{dt} = k_b [A^\bullet]_{ss} [B] = \frac{2k_i k_b [A_2][B]}{k_t - k_b[B]}$

观察速率方程的分母项 $(k_t - k_b[B])$。当支化项 $k_b[B]$ 趋近于终止项 $k_t$ 时，分母趋近于零，导致 $[A^\bullet]_{ss}$ 和[反应速率](@keyword=reaction_rate|lang=zh-CN|style=Feynman)急剧增大。当 $k_b[B] \ge k_t$ 时，[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)的生成速率超过消耗速率，[稳态假设](@keyword=steady_state_assumption|lang=zh-CN|style=Feynman)失效，[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)浓度和[反应速率](@keyword=reaction_rate|lang=zh-CN|style=Feynman)将指数增长，引发爆炸。这个条件定义了爆炸的[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)，解释了为何爆炸现象通常只在反应物浓度、压力和温度达到特定阈值时才会发生。

#### 抑制与猝灭

与促进反应的[链支化](@keyword=chain_branching|lang=zh-CN|style=Feynman)相反，**抑制剂 (inhibitor)** 或**猝灭剂 (quencher)** 能够有效减缓或中止链式反应。抑制剂通常是自身稳定但能高效清除[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)的分子。其作用机理是提供一个比正常[链终止](@keyword=chain_termination|lang=zh-CN|style=Feynman)或[链增长](@keyword=chain_propagation|lang=zh-CN|style=Feynman)更快的途径来消耗[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman) [@problem_id:1476689]。

一个有效的抑制剂 $Inh$ 会与[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman) $X^\bullet$ 发生快速反应，生成一个稳定的、不参与[链增长](@keyword=chain_propagation|lang=zh-CN|style=Feynman)的产物：
$Inh + X^\bullet \rightarrow \text{稳定非自由基产物}$

这个反应与[链增长步骤](@keyword=propagation_step|lang=zh-CN|style=Feynman) ($A + X^\bullet \rightarrow P + X^\bullet$) 形成竞争。由于抑制剂通常被设计为具有极高的反应活性（对[自由基](@keyword=free_radicals|lang=zh-CN|style=Feynman)而言），即使其浓度很低，也能有效地“捕获”[链载体](@keyword=chain_carriers|lang=zh-CN|style=Feynman)，从而大大缩短了[动力学链长](@keyword=kinetic_chain_length|lang=zh-CN|style=Feynman)，使总[反应速率](@keyword=reaction_rate|lang=zh-CN|style=Feynman)显著下降，甚至完全停止。这一原理在工业生产和化学品储存中具有重要应用，例如在易聚合的[单体](@keyword=monomer|lang=zh-CN|style=Feynman)中加入阻聚剂，以防止其在储存和运输过程中发生不期望的链式聚合反应。