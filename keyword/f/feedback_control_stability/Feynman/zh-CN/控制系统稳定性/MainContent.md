## 引言
在工程和技术领域，维持[平衡](@keyword=equilibrium|lang=zh-CN|style=Feynman)不是一种被动的状态，而是一个主动、动态的过程。从飞机保持高度到化工厂维持温度，[反馈控制](@keyword=feedback_control|lang=zh-CN|style=Feynman)原理是确保系统按预期运行的无形之手。然而，控制行为本身也带来了不稳定的风险，一个小小的扰动就可能引发灾难性的故障。理解一个稳定的、行为良好的系统与一个混乱的、不稳定的系统之间的微妙界限，是[控制理论](@keyword=control_theory|lang=zh-CN|style=Feynman)的基石。本文旨在解决一个根本性问题：是什么让一个[反馈系统](@keyword=feedback_systems|lang=zh-CN|style=Feynman)保持稳定，以及我们如何设计它，使其在一个复杂且不确定的世界中保持稳定？

接下来的章节将[引导](@keyword=bootstrapping|lang=zh-CN|style=Feynman)您深入探讨这个关键主题。首先，在“原理与机制”中，我们将深入稳定性的数学核心，探索系统的特性如何被编码为[极点和零点](@keyword=poles_and_zeros|lang=zh-CN|style=Feynman)，以及像劳斯-赫尔维茨检验和[频域](@keyword=frequency_space|lang=zh-CN|style=Feynman)裕度等判据如何让我们无需复杂计算就能评估稳定性。然后，在“应用与跨学科联系”中，我们将看到这些原理的实际应用，审视它们从[机器人学](@keyword=robotics|lang=zh-CN|style=Feynman)、航空航天到[化学工程](@keyword=chemical_engineering|lang=zh-CN|style=Feynman)和计算建模等各个领域的深远影响，揭示[鲁棒稳定性](@keyword=robust_stability|lang=zh-CN|style=Feynman)是如何被融入现代技术构造之中的。

## 原理与机制

想象一下，你正试着用手掌[平衡](@keyword=equilibrium|lang=zh-CN|style=Feynman)一根扫帚。你的眼睛观察它的[倾斜](@keyword=vergence|lang=zh-CN|style=Feynman)，你的大脑处理误差，你的肌肉移动手来纠正它。这是最原始形式的[反馈控制](@keyword=feedback_control|lang=zh-CN|style=Feynman)。如果你的反应及时且恰当，扫帚就能保持直立——系统是稳定的。如果你反应过度或反应太迟，扫帚就会倒下——系统是不稳定的。稳定性的原理和机制，就是理解在这场精妙的博弈中区分成败的精确规则。这不仅仅关乎扫帚；它关乎一切，从保持飞机平飞到维持化工厂的反应温度。

### 运动的特性：平面上的[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)

是什么决定了一个系统在受到轻微推动后，是会恢复静止还是会趋于无穷？答案被编码在系统的基本“特性”中。用数学的语言来说，这种特性由一组称为系统**[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)**的数字所捕捉，或者在[控制理论](@keyword=control_theory|lang=zh-CN|style=Feynman)中更常被称为其[传递函数](@keyword=transfer_function|lang=zh-CN|style=Feynman)的**[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)**。

可以把这些[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)看作是系统运动的[遗传密码](@keyword=genetic_code|lang=zh-CN|style=Feynman)。它们决定了[系统响应](@keyword=system_response|lang=zh-CN|style=Feynman)的自然节律、[衰减](@keyword=attenuation|lang=zh-CN|style=Feynman)速率或增长[速度](@keyword=velocity|lang=zh-CN|style=Feynman)。为了将此可视化，我们把它们放在一个称为**[复平面](@keyword=complex_plane|lang=zh-CN|style=Feynman)**的图上。这个平面有一个水平的“实”轴和一个垂直的“虚”轴。一个[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)在这张图上的位置，告诉我们关于它对系统行为贡献的一切。

*   **位于[左半平面](@keyword=left_half_plane|lang=zh-CN|style=Feynman)的[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)（实部为负）：** 这些是“好”的[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)。它们代表随时间自然消逝的运动。例如，一个位于 $s = -2$ 的[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)对应于一个像 $\exp(-2t)$ 一样[衰减](@keyword=attenuation|lang=zh-CN|style=Feynman)的响应。一对像 $s = -1 \pm 3j$ 这样的[共轭复数](@keyword=complex_conjugate|lang=zh-CN|style=Feynman)[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)，则代表一个[衰减](@keyword=attenuation|lang=zh-CN|style=Feynman)的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)——就像一根被拨动的吉他弦，声音逐渐消失。任何所有[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)都位于这个[左半平面](@keyword=left_half_plane|lang=zh-CN|style=Feynman)的系统都是**渐近稳定的**。它总是会回到其[平衡](@keyword=equilibrium|lang=zh-CN|style=Feynman)状态。

*   **位于[右半平面](@keyword=right_half_plane|lang=zh-CN|style=Feynman)的[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)（实部为正）：** 这些是“坏”的[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)。它们代表失控的运动。一个位于 $s = +2$ 的[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)对应于一个像 $\exp(2t)$ 一样爆炸性增长的响应。任何系统只要有一个[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)在[右半平面](@keyword=right_half_plane|lang=zh-CN|style=Feynman)，它就是**不稳定的**。那根[平衡](@keyword=equilibrium|lang=zh-CN|style=Feynman)的扫帚，一旦开始倒下，就是一个不稳定的系统。

*   **位于[虚轴上的极点](@keyword=poles_on_imaginary_axis|lang=zh-CN|style=Feynman)（实部为零）：** 这是边界。这里的[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)代表既不[衰减](@keyword=attenuation|lang=zh-CN|style=Feynman)也不增长，而是永远持续下去的运动。一对位于 $s = \pm 3j$ 的[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)对应于一个纯粹的、永不消逝的[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，就像一个完美的无[摩擦](@keyword=friction|lang=zh-CN|style=Feynman)摆锤。这被称为**[临界稳定](@keyword=marginal_stability|lang=zh-CN|style=Feynman)**。

[反馈控制](@keyword=feedback_control|lang=zh-CN|style=Feynman)的魔力在于，我们可以主动改变这些[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)的位置。通过测量系统的状态并将其反馈回来，我们改变了系统的动态特性，从而将其[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)从“坏”的位置移动到“好”的位置。想象一个生物机器人系统，它管理着一个两种[物种相互作用](@keyword=species_interactions|lang=zh-CN|style=Feynman)的[生态系统](@keyword=ecosystems|lang=zh-CN|style=Feynman) [@problem_id:1754974]。如果任其自然发展，它们的[种群](@keyword=biological_population|lang=zh-CN|style=Feynman)数量可能会激增或崩溃。通过实施一个[状态反馈控制器](@keyword=state_feedback_controller|lang=zh-CN|style=Feynman)，我们实际上重写了系统的动态，创建了一个具有一组新[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)的新的[闭环系统](@keyword=closed_loop_systems|lang=zh-CN|style=Feynman)。如果我们正确地选择反馈，我们就可以将这些[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)移到稳定的[左半平面](@keyword=left_half_plane|lang=zh-CN|style=Feynman)，确保[生态系统](@keyword=ecosystems|lang=zh-CN|style=Feynman)保持在健康的[平衡](@keyword=equilibrium|lang=zh-CN|style=Feynman)状态。

有时，我们甚至不用找到[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)就能发现[不稳定性](@keyword=lability|lang=zh-CN|style=Feynman)。例如，对于一个简单的[二阶系统](@keyword=second_order_systems|lang=zh-CN|style=Feynman)，[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)实部之和与[系统矩阵](@keyword=system_matrix|lang=zh-CN|style=Feynman)的一个属性——**迹**——有关。如果迹是正数，这意味着实部之和是正数。两个负数相加不可能得到一个正数，所以至少有一个[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)的实部必须是正的——这保证了[不稳定性](@keyword=lability|lang=zh-CN|style=Feynman) [@problem_id:2201579]。这是一个极其简洁的诊断测试。

### 洞察先机：无需解算的稳定性判断

对于一个复杂的系统，比如一架拥有数百万变量的现代飞机，找到每个[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)的确切位置可能是一项艰巨的任务。幸运的是，19世纪的数学家给了我们一个强大的工具，可以在不求解[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)的情况下检查稳定性。**[劳斯-赫尔维茨判据](@keyword=routh_hurwitz_criterion|lang=zh-CN|style=Feynman)**是一种代数方法，就像医生检查病人的生命体征一样。它不是进行侵入性手术（[求根](@keyword=root_finding_2|lang=zh-CN|style=Feynman)），而只是检查系统[特征多项式](@keyword=characteristic_polynomial|lang=zh-CN|style=Feynman)的系数。

这个过程包括将这些系数[排列](@keyword=permutations|lang=zh-CN|style=Feynman)成一个特定的数组，规则很简单：要使系统稳定，这个数组第一列的所有数字都必须是正数。如果任何数字是负数或零，这都是一个明确的信号，表明至少有一个“坏”的[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)潜伏在[右半平面](@keyword=right_half_plane|lang=zh-CN|style=Feynman)或[虚轴](@keyword=imaginary_axis|lang=zh-CN|style=Feynman)上。例如，对于一个三阶系统，其[特征方程](@keyword=characteristic_equation|lang=zh-CN|style=Feynman)为 $s^3 + a_2 s^2 + a_1 s + a_0 = 0$，其中所有的 $a_i$ 系数都是正数，这个判据可以简化为一个单一而优雅的条件：$a_2 a_1 > a_0$ [@problem_id:1749888]。如果这个不等式成立，系统就是稳定的。如果不成立，它就是不稳定的。

当我们面对工程学中最大的难题之一：**不确定性**时，这个工具变得不可或缺。真实系统的组件永远不会完全符合蓝图中的规格。一个机械臂的质量可能会随其负载而变化，或者一个[电子](@keyword=electrons|lang=zh-CN|style=Feynman)元件的[电阻](@keyword=electrical_resistance|lang=zh-CN|style=Feynman)可能会随温度而漂移。这意味着我们[特征多项式](@keyword=characteristic_polynomial|lang=zh-CN|style=Feynman)的系数不是固定的数字，而是在一个范围内。

当我们设计[控制器](@keyword=control_unit|lang=zh-CN|style=Feynman)时，我们必须保证稳定性不仅适用于[理想](@keyword=ideals|lang=zh-CN|style=Feynman)的**标称**系统，还要适用于所有可能的变化——这是一个更难的要求，称为**[鲁棒稳定性](@keyword=robust_stability|lang=zh-CN|style=Feynman)**。想象一下为一只机械臂设计一个[控制器](@keyword=control_unit|lang=zh-CN|style=Feynman)，其中一个参数 $\alpha$ 的标称值是 4，但可能在 2 到 6 之间漂移 [@problem_id:1617652]。使用[劳斯-赫尔维茨判据](@keyword=routh_hurwitz_criterion|lang=zh-CN|style=Feynman)，我们可能会发现对于标称值 $\alpha=4$，系统在[控制器增益](@keyword=controller_gain|lang=zh-CN|style=Feynman) $K$ 高达 20 时是稳定的。但是为了确保在 $\alpha$ 的整个范围内都稳定，我们必须满足最坏情况下的[稳定性条件](@keyword=stability_condition|lang=zh-CN|style=Feynman)。这可能意味着最大安全增益 $K_{rob,max}$ 仅为 6。不确定性的存在迫使我们更加保守，缩小了我们的“稳定”操作区域。标称性能和[鲁棒性能](@keyword=robust_performance|lang=zh-CN|style=Feynman)之间的这种差距是[控制工程](@keyword=control_engineering|lang=zh-CN|style=Feynman)中的一个核心主题。

### 离边缘有多远？[频域](@keyword=frequency_space|lang=zh-CN|style=Feynman)中的安全裕度

思考稳定性的另一种方式，是分析系统对不同频率[正弦输入](@keyword=sinusoidal_inputs|lang=zh-CN|style=Feynman)的响应，这能让我们对系统“有多稳定”有更直观的感觉。这种[频域](@keyword=frequency_space|lang=zh-CN|style=Feynman)视角提出了关于[反馈回路](@keyword=feedback_loops|lang=zh-CN|style=Feynman)的两个关键问题：

1.  在什么频率下，一个信号在环路中传播一圈后，返回时的[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman)与原来完全相同（增益为1）？这被称为**[增益交越频率](@keyword=gain_crossover_frequency|lang=zh-CN|style=Feynman)**，$\omega_{gc}$。
2.  在什么频率下，一个信号返回时被完美反相（[相移](@keyword=phase_shifts|lang=zh-CN|style=Feynman)为-180°），准备进行破坏性（或者在反馈术语中，建设性）的自我加强？这被称为**[相位交越频率](@keyword=phase_crossover_frequency|lang=zh-CN|style=Feynman)**，$\omega_{pc}$。

稳定性取决于在这两个关键频率下发生的事情。为了保持稳定，环路在相位为-180°的频率下，增益绝对不能为1（或更大）。如果出现这种情况，那个频率的任何微小扰动都会在环路中循环，每一次都会增强，导致那种你从放置不当的麦克风和扬声器中听到的啸叫反馈。

由此，我们得到了两个衡量安全裕度的关键指标：

*   **[增益裕度](@keyword=gain_margin|lang=zh-CN|style=Feynman) (GM):** 这个问题是：在[相位交越频率](@keyword=phase_crossover_frequency|lang=zh-CN|style=Feynman) $\omega_{pc}$（相位为-180°）时，我们的增益比1小多少？如果此时的增益是，比如说，0.355，这意味着我们远低于1这个[临界](@keyword=criticality|lang=zh-CN|style=Feynman)阈值。[增益裕度](@keyword=gain_margin|lang=zh-CN|style=Feynman)是指在达到不稳定之前，我们可以将增益增加的倍数，即 $1 / 0.355 \approx 2.8$。用[分贝](@keyword=decibels|lang=zh-CN|style=Feynman)表示，这是一个大约 $9$ dB 的安全裕度 [@problem_id:1613015]。这是我们对抗系统放大倍数增加的缓冲。

*   **[相位裕度](@keyword=phase_margin|lang=zh-CN|style=Feynman) (PM):** 这个问题是：在[增益交越频率](@keyword=gain_crossover_frequency|lang=zh-CN|style=Feynman) $\omega_{gc}$（增益为1）时，我们的相位离[临界](@keyword=criticality|lang=zh-CN|style=Feynman)的-180°标记有多远？如果此时的相位是-157°，我们就有一个 $180^\circ - 157^\circ = 23^\circ$ 的缓冲，才达到不[稳定点](@keyword=stationary_points|lang=zh-CN|style=Feynman) [@problem_id:1613038]。这就是我们的**[相位裕度](@keyword=phase_margin|lang=zh-CN|style=Feynman)**，它代表了我们对系统中时间延迟的容忍度 [@problem_id:1599438]。

一个健康的[相位裕度](@keyword=phase_margin|lang=zh-CN|style=Feynman)可以说是[反馈回路](@keyword=feedback_loops|lang=zh-CN|style=Feynman)中良好性能和鲁棒性最重要的单一指标。它告诉我们，在控制动作的时机上我们有多少“余地”。

### 不可避免的[滞后](@keyword=hysteresis|lang=zh-CN|style=Feynman)：为什么延迟是危险的

[相位裕度](@keyword=phase_margin|lang=zh-CN|style=Feynman)的概念让我们清晰地理解了为什么控制中最常见和最有害的现象之一——**时间延迟**——是如此破坏稳定。时间延迟的作用正如其名：它接收一个信号，并在稍后将其原封不动地输出。在[频域](@keyword=frequency_space|lang=zh-CN|style=Feynman)中，这有一个奇妙的效果。一个 $\tau$ 秒的纯时间延迟完全不改变[正弦波](@keyword=sinusoidal_waves|lang=zh-CN|style=Feynman)的[振幅](@keyword=amplitude|lang=zh-CN|style=Feynman)。其增益始终为1。然而，它使波形发生[相位偏移](@keyword=phase_deviation|lang=zh-CN|style=Feynman)，偏移量等于 $-\omega \tau$。

至关重要的是，这个[相位滞后](@keyword=phase_lag|lang=zh-CN|style=Feynman)不是恒定的；它随着频率 $\omega$ 的增加而变得越来越大。延迟给我们的系统引入了一个无情的、依赖于频率的[相移](@keyword=phase_shifts|lang=zh-CN|style=Feynman) [@problem_id:1564349]。

现在，考虑它对我们[相位裕度](@keyword=phase_margin|lang=zh-CN|style=Feynman)的影响。[增益交越频率](@keyword=gain_crossover_frequency|lang=zh-CN|style=Feynman) $\omega_{gc}$ 仅由系统的增益决定，而延迟不影响增益。所以，$\omega_{gc}$ 保持不变。但是，在这个关键频率下的相位现在变得更负，减少了 $\omega_{gc}\tau$。延迟直接蚕食了我们的[相位裕度](@keyword=phase_margin|lang=zh-CN|style=Feynman)。如果我们原来的[相位裕度](@keyword=phase_margin|lang=zh-CN|style=Feynman)是 $45^\circ$，而延迟在[增益交越频率](@keyword=gain_crossover_frequency|lang=zh-CN|style=Feynman)处引入了 $30^\circ$ 的[滞后](@keyword=hysteresis|lang=zh-CN|style=Feynman)，我们新的[相位裕度](@keyword=phase_margin|lang=zh-CN|style=Feynman)就只有区区 $15^\circ$。如果延迟大到使得 $\omega_{gc}\tau$ 大于我们原来的[相位裕度](@keyword=phase_margin|lang=zh-CN|style=Feynman)，系统就会变得不稳定。

这就是为什么远程手术机器人、基于互联网的[控制系统](@keyword=control_systems|lang=zh-CN|style=Feynman)，甚至带有长管道的化学过程都如此难以设计。不可避免的通信或传输[滞后](@keyword=hysteresis|lang=zh-CN|style=Feynman)就像一种毒药，稳步[侵蚀](@keyword=etching|lang=zh-CN|style=Feynman)[相位裕度](@keyword=phase_margin|lang=zh-CN|style=Feynman)，将系统推向不稳定。

### 隐藏的破坏者：不稳定的[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)和内部模式

随着我们层层深入，会发现更深层、更微妙的稳定性威胁。到目前为止，我们一直关注决定系统内在趋势的[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)。但系统也有**[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)**，你可以把它们看作是塑造外部输入或控制信号如何与这些趋势相互作用的因素。和[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)一样，[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)也可以在[左半平面](@keyword=left_half_plane|lang=zh-CN|style=Feynman)或[右半平面](@keyword=right_half_plane|lang=zh-CN|style=Feynman)。[右半平面](@keyword=right_half_plane|lang=zh-CN|style=Feynman)的[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)被称为**[非最小相位](@keyword=non_minimum_phase|lang=zh-CN|style=Feynman) (NMP)** [零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)，它是一个臭名昭著的破坏者。

一个NMP[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)会带来一个奇怪的特性：系统最初的响应方向与其最终的[稳态响应](@keyword=steady_state_response|lang=zh-CN|style=Feynman)方向*相反*。想象一下倒车时拖着一辆拖车：为了让拖车向左转，你必须先把方向盘向右打。这种初始的“反向”响应可能会对[反馈控制](@keyword=feedback_control|lang=zh-CN|style=Feynman)器造成严重破坏。一个试图消除误差的[控制器](@keyword=control_unit|lang=zh-CN|style=Feynman)看到系统走向了错误的方向，会施加一个更强的校正，这可能导致[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)和不稳定。

考虑两个具有相同稳定[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)的系统，但一个在[左半平面](@keyword=left_half_plane|lang=zh-CN|style=Feynman)有一个“好”的[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)，另一个在[右半平面](@keyword=right_half_plane|lang=zh-CN|style=Feynman)有一个“坏”的NMP[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman) [@problem_id:1602045]。具有好[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)的系统通常可以通过高[控制器增益](@keyword=controller_gain|lang=zh-CN|style=Feynman)变得更快、响应更灵敏，并且保持稳定。但具有NMP[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)的系统存在根本性限制。当你调高增益时，NMP[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)就像一个锚，将[系统的极点](@keyword=poles_of_a_system|lang=zh-CN|style=Feynman)拉向不稳定的[右半平面](@keyword=right_half_plane|lang=zh-CN|style=Feynman)。超过某个增益，系统将不可避免地变得不稳定。这些NMP[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)代表了性能上固有的物理限制，任何巧妙的[线性](@keyword=linearity|lang=zh-CN|style=Feynman)控制都无法克服。

这就引出了最后一个，也是最关键的原则：**[内部稳定性](@keyword=internal_stability|lang=zh-CN|style=Feynman)**。设计一个从外部看*似乎*稳定，但内部却是一颗定时炸弹的系统是可能的。这种情况发生在一个不稳定的设备部分被[控制器](@keyword=control_unit|lang=zh-CN|style=Feynman)“完美”抵消时。假设你的设备有一个位于 $s=+1$ 的[不稳定极点](@keyword=unstable_poles|lang=zh-CN|style=Feynman)。你可能认为可以通过设计一个在完全相同位置 $s=+1$ 有一个[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)的[控制器](@keyword=control_unit|lang=zh-CN|style=Feynman)来解决这个问题 [@problem_id:1581490]。在总的输入到输出[传递函数](@keyword=transfer_function|lang=zh-CN|style=Feynman)中，分子中的 $(s-1)$ 项（来自[控制器](@keyword=control_unit|lang=zh-CN|style=Feynman)的[零点](@keyword=complex_analysis_zeros|lang=zh-CN|style=Feynman)）将抵消分母中的 $(s-1)$ 项（来自设备的[极点](@keyword=extreme_points|lang=zh-CN|style=Feynman)），不稳定的模式将从方程中消失。对于一个施加测试信号的外部观察者来说，系统看起来是稳定的。

但这个不稳定的模式并没有消失，它只是被隐藏了起来。它不再受输入的影响，但它仍然是环路内部运作的一部分。任何微小的内部扰动，或者抵消中哪怕最细微的不完美，都会激发这个不稳定的模式，导致某个内部信号（比如[控制器](@keyword=control_unit|lang=zh-CN|style=Feynman)自身的输出）无界增长，最终使系统饱和并被摧毁。真正的稳定性——[内部稳定性](@keyword=internal_stability|lang=zh-CN|style=Feynman)——要求[反馈回路](@keyword=feedback_loops|lang=zh-CN|style=Feynman)内部的*所有*信号都保持有界。仅仅看从主输入到最终输出的[传递函数](@keyword=transfer_function|lang=zh-CN|style=Feynman)是不够的。你必须检查所有的内部路径，以确保没有隐藏的炸弹等着爆炸。这是反馈的终极教训：你不能简单地掩盖固有的[不稳定性](@keyword=lability|lang=zh-CN|style=Feynman)，你必须主动地驯服它。

