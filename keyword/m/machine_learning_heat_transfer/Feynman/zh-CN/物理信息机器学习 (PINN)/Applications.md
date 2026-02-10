## 应用与跨学科联系

既然我们已经探索了将机器学习与物理科学相结合的基本原则，现在让我们踏上一段旅程，看看这些思想在实践中的应用。你可能会倾向于将机器学习视为一个“黑箱”，一个我们输入数据便能得到答案的神秘神谕。但这并非科学的精神。真正的力量、真正的美，在于我们打开这个箱子，将不可改变的物理定律编织进我们学习机器的结构之中。我们将看到，这种方法不仅解决了工程问题，还以惊人而深刻的方式连接了不同科学领域，揭示了我们探求理解世界过程中的一条共同线索。

### 从数字神谕到智能学徒

在最简单的情况下，机器学习可以扮演一个极其勤奋和迅速的学徒。想象一下，你是一名工程师，任务是为某个热的电子元件（比如一根圆柱形导线）设计一个冷却系统。几十年来，工程师们依赖于从无数实验中辛苦得出的复杂经验公式来预测这类物体的传热。一个著名的例子是 Churchill-Bernstein 关联式，这是一个看起来相当吓人的方程，它将传热（通过无量纲的努塞尔数 $\mathrm{Nu}$）与流体流动条件（[雷诺数](@keyword=reynolds_number|lang=zh-CN|style=Feynman) $\mathrm{Re}$）和流体性质（普朗特数 $\mathrm{Pr}$）联系起来。

如果我们能创造一个“数字学徒”，它能直接从几个例子中学习这种关系呢？这就是**[代理模型](@keyword=surrogate_models|lang=zh-CN|style=Feynman)**背后的思想。我们不再每次都计算复杂的公式或运行昂贵的[流体动力学](@keyword=hydrodynamics|lang=zh-CN|style=Feynman)模拟，而是使用一个训练好的机器学习模型作为替代品。在一个典型场景中，我们可能会利用已知的物理学作为我们的神谕，进行一小组智能选择的“虚拟实验”。我们不是随机选择点，而是使用巧妙的采样策略来高效地探索各种可能性空间。然后，我们将这些例子呈现给我们的机器学习模型。通过融入一些基本的物理直觉——例如，知道这些关系在[对数空间](@keyword=logarithmic_space|lang=zh-CN|style=Feynman)中通常是线性的——我们可以引导模型以惊人的准确性学习潜在的模式，即使只有十几个数据点 [@problem_id:2502984]。其结果是一个闪电般快速的预测器，它有效地捕捉了一个复杂物理定律的精髓，可随时用于快速的设计优化。

### 提出正确问题的艺术：局部精度与全局真理

建立一个模型是一回事，知道它是否是*正确*的模型是另一回事。一个模型“准确”意味着什么？假设我们前一个例子中的机器学习模型现在学会了不仅预测平均传热值，而且预测圆柱周长上每一点的传热。假设我们把模型的预测与高保真模拟进行比较，发现各处的[局部误差](@keyword=local_error|lang=zh-CN|style=Feynman)都非常小。成功了，对吗？

别急。一个设计整体冷却系统的工程师可能只关心一件事：每秒钟移除的总热量。这个全局量与整个表面上的*平均*努塞尔数有关。一个模型完全有可能[局部误差](@keyword=local_error|lang=zh-CN|style=Feynman)很小，但累加起来却导致总传热的显著误差。相反，一个模型可能有很大的局部误差，但这些误差恰好相互抵消，给出一个具有欺骗性的完美全局预测！

这揭示了一个更深层次的真理：“最好”的模型取决于你所问的问题。一个产生微小、高频误差的模型可能不适合预测应力集中，但对于预测总能量传递来说可能完全没问题。一个有轻微全局偏差的模型——比如总是高估 $2\%$——对于气候模型来说可能无法接受，但对于初步设计研究来说则没问题。这种对误差的深思熟虑的分析，剖析其性质并将其与不同的工程关注量（如总传热或[空气动力学](@keyword=aerodynamics|lang=zh-CN|style=Feynman)阻力）相关联，是在现实世界中应用机器学习的一个关键且常常被忽视的方面 [@problem_id:2502978]。

### [学会学习](@keyword=learning_to_learn|lang=zh-CN|style=Feynman)：迁移的通用语言

[现代机器学习](@keyword=modern_machine_learning|lang=zh-CN|style=Feynman)最像人类的方面或许是其**迁移知识**的能力。我们并非从零开始学习一切。一个理解[波动力学](@keyword=wave_mechanics|lang=zh-CN|style=Feynman)的物理学家可以更容易地学习量子力学。一个知道如何修理汽车的技工可以更快地学会修理卡车。核心原理是可以迁移的。

机器学习模型也能做到这一点。想象一下，我们想为一个非常复杂的系统建立一个代理模型，比如一根带有内肋以增强传热的管道。为这个系统获取数据是昂贵的。但我们有大量关于一个更简单系统的数据：一块光滑的平板。两种情况下，[湍流对流](@keyword=turbulent_convection|lang=zh-CN|style=Feynman)的基本物理学是相似的。我们能利用这一点吗？

当然可以。我们可以首先在一个简单平板的庞大、廉价的数据集上“[预训练](@keyword=pre_training|lang=zh-CN|style=Feynman)”一个模型。这个模型学习了[湍流传热](@keyword=turbulent_heat_transfer|lang=zh-CN|style=Feynman)的基本“语言”——它如何随速度和流体性质而变化。然后，我们拿这个[预训练](@keyword=pre_training|lang=zh-CN|style=Feynman)好的模型，在来自带肋通道的少数昂贵数据点上进行“微调”。模型不是从一张白纸开始，而是从坚实的物理知识基础上开始。其结果是一个比仅在有限的带肋通道数据上从头开始训练的模型准确得多、数据效率高得多的模型 [@problem_id:2502983]。

这个思想不仅限于传热学，它是贯穿科学的普适原则。
- 在**[系统生物学](@keyword=systems_biology|lang=zh-CN|style=Feynman)**中，研究人员使用在数百万个通用蛋白质序列上[预训练](@keyword=pre_training|lang=zh-CN|style=Feynman)的巨型模型。当面临预测一种新药是否会与一个特定的癌症相关蛋白家族结合的挑战时（他们对此任务的数据很少），他们不会从零开始。他们使用[预训练](@keyword=pre_training|lang=zh-CN|style=Feynman)模型将蛋白质序列“编码”成一个丰富的数值表示，然后在这个表示上训练一个小型、简单的模型。关于是什么构成一个蛋白质的知识被迁移过来，极大地提高了在新特定任务上的预测能力 [@problem_id:1426776]。
- 在**基因组学**中，科学家使用像 DNA-BERT 这样的模型，这是一个在许多物种基因组构成的整个生命之“书”上[预训练](@keyword=pre_training|lang=zh-CN|style=Feynman)的大型 [Transformer](@keyword=transformers|lang=zh-CN|style=Feynman) 模型。这个模型在没有任何明确标签的情况下学习 DNA 的“语法”——[局部基](@keyword=local_basis|lang=zh-CN|style=Feynman)序和[长程依赖](@keyword=long_range_dependencies|lang=zh-CN|style=Feynman)关系。当一个研究人员想在一个新的基因组中用少量标记数据集寻找特定的调控区域（如[启动子](@keyword=promoter|lang=zh-CN|style=Feynman)）时，他们可以利用这个[预训练](@keyword=pre_training|lang=zh-CN|style=Feynman)模型。这种知识迁移起到了强大的正则化作用，防止模型基于小数据集做出虚假的结论，并引导它走向一个与基因组通用结构一致的解决方案 [@problem-id:2429075]。

无论是[流体动力学](@keyword=hydrodynamics|lang=zh-CN|style=Feynman)的语言、蛋白质结构的语言，还是遗传学的语言，[迁移学习](@keyword=transfer_learning|lang=zh-CN|style=Feynman)都使我们能够在现有知识的基础上进行构建，这本身就是科学进步的基石。

### 将物理学编织进模型的结构中

到目前为止，我们都将模型视为局外人，从数据中学习物理。最深刻的一步是将物理学*构建到*模型的架构中。

#### 对称性的交响曲：不变性与[等变性](@keyword=equivariance|lang=zh-CN|style=Feynman)

物理定律是对称的。实验结果不取决于你是在伦敦还是在东京进行（平移对称性），也不取决于你实验室的朝向（[旋转对称](@keyword=rotational_symmetry|lang=zh-CN|style=Feynman)性）。物理量对这些对称性以特定的方式响应。一个标量，如温度或能量，是**不变的**——当你旋转系统时，它的值不会改变。一个矢量，如力或[热通量](@keyword=heat_flux|lang=zh-CN|style=Feynman)，是**等变的**——它不会保持不变，而是*随着*系统一起旋转。

标准的[神经网络](@keyword=neural_networks|lang=zh-CN|style=Feynman)对这些对称性一无所知。如果你给它看一个涡旋的模拟，然后再给它看同一个涡旋旋转了 90 度的模拟，它会看到两个完全不同的输入，并且必须从头开始学习两者。这是极其低效的。

解决方案是构建**[等变神经网络](@keyword=equivariant_neural_networks|lang=zh-CN|style=Feynman)**。这些是特殊的架构，其中对称性是网络布线的基本组成部分。一个[等变网络](@keyword=equivariant_networks|lang=zh-CN|style=Feynman)通过其构造*就知道*矢量和其他几何对象应该如何变换。如果它学会了预测一种分子构型中原子的力，它会自动知道该分子的任何旋转版本的力，而无需被展示过 [@problem_id:2479779] [@problem_id:2777670]。这一原则甚至可以扩展到基本物理学的深奥对称性，如支配粒子相互作用的规范对称性 [@problem_id:2410578]。对我们来说，这意味着我们可以构建能够正确处理像速度和热通量这样的[矢量场](@keyword=vector_field|lang=zh-CN|style=Feynman)的模型，从根本上尊重它们的方向性。

#### 两全其美：物理-机器学习混合模型

最后，我们不必在我们经过时间考验的物理模型和机器学习的新世界之间做出选择。我们可以将它们统一起来。我们的许多物理模型功能强大但并不完美。一个典型的例子是[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)建模，其中雷诺平均纳维-斯托克斯 (RANS) 方程提供了一种计算上可行但近似的[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)描述。这些近似是预测传热和阻力时产生显著误差的来源。

与其试图完全取代 RANS，我们可以使用机器学习来预测一个**修正项**。我们可以从昂贵的模拟（如[大涡模拟](@keyword=large_eddy_simulation|lang=zh-CN|style=Feynman)，LES）或实验中获取稀疏、高保真的数据，并训练一个模型来学习其中的差异——即 RANS 模型出错的部分。但我们以一种符合物理原则的方式来做这件事。我们设计的修正旨在修改模型关于[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)率的假设，确保[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)和[热力学第二定律](@keyword=second_law_of_thermodynamics|lang=zh-CN|style=Feynman)等基本定律永远不会被违反。使用像高斯过程这样的[贝叶斯框架](@keyword=bayesian_framework|lang=zh-CN|style=Feynman)，我们甚至可以让模型告诉我们它对其修正的[置信度](@keyword=confidence_levels|lang=zh-CN|style=Feynman)有多高，从而为最终的预测提供宝贵的不确定性界限 [@problem_id:2536800]。

这种混合方法是一个反复出现的主题。在**[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)**中，计算成本低的模型如[密度泛函理论 (DFT)](@keyword=density_functional_theory_dft|lang=zh-CN|style=Feynman) 会产生近似的“[Kohn-Sham](@keyword=kohn_sham|lang=zh-CN|style=Feynman) 轨道”，这些轨道存在已知的缺陷。而更准确但成本高得多的方法能产生决定[光电离](@keyword=photoionization|lang=zh-CN|style=Feynman)的真实“Dyson 轨道”。一个被赋予了正确的[旋转对称](@keyword=rotational_symmetry|lang=zh-CN|style=Feynman)性和对其输出施加了物理约束的机器学习模型，可以被训练来学习从廉价、近似的轨道到昂贵、正确的轨道之间的映射 [@problem_id:2456904]。机器学习模型充当了连接不同层次物理理论之间的学习桥梁。

从智能学徒到对称性大师，再到混合理论中的强大合作者，机器学习正迅速成为科学事业中不可或缺的工具。它是跨学科思想的[催化剂](@keyword=catalyst|lang=zh-CN|style=Feynman)，向我们展示了学习和发现的模式与我们力求理解的物理定律一样普适。