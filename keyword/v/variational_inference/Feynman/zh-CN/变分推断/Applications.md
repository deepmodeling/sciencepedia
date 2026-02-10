## 应用与跨学科联系

我们已经走过了变分推断的原理之旅，窥探了那些使我们能够近似不可能的数学机制。但是，一个工具的好坏取决于它能解决的问题。正是在应用领域，变分推断的真正美丽和力量才得以展现。它不仅仅是一个巧妙的计算捷径；它是一种统一的语言，连接了从人工智能的硅电路到人类大脑复杂的[生物网络](@keyword=biological_networks|lang=zh-CN|style=Feynman)等不同学科。现在，让我们来探索这片广阔的思想版图。

### 谦逊的机器：量化“我不知道”

变分推断最深刻和最实际的应用之一，是教我们的机器拥有一份谦逊。一个标准的人工智能模型在面对问题时，总是会以坚定不移且往往不合理的自信给出答案。但如果问题是模棱两可的呢？或者，如果这是模型从未见过的问题类型呢？我们希望机器能够表达它的不确定性——能够说，“我不知道”。

这正是变分推断让我们能够做到的。我们可以区分两种基本类型的不确定性 [@problem_id:4871478]。第一种是**[偶然不确定性](@keyword=aleatoric_uncertainty|lang=zh-CN|style=Feynman)**（aleatoric uncertainty），它内在于数据本身。想象一张模糊的照片或一段充满静电的录音；无论你的模型多聪明，能推断出的信息都有一个根本的限制。第二种，也许更重要的是**认知不确定性**（epistemic uncertainty），它反映了模型自身的知识匮乏。当模型在有限的数据上训练，或被呈现远超其训练经验的内容时，就会出现这种情况。

变分推断提供了一种有原则的方法来捕捉这种认知不确定性。我们不是为神经网络中的每个权重学习一个单一的、固定的值，而是使用 VI 为每个权重推断一个完整的概率分布。一个后验权重分布宽泛而不确定的网络，就是一个告诉我们它缺乏信心的网络。对于一个新的输入，我们不是得到一个单一的预测，而是可以从我们的变分后验中采样多组权重，通过网络运行它们，并观察结果的分布。分布范围广，就表示认知不确定性高。

这一能力正在改变医学等高风险领域。想象一个[计算机辅助诊断](@keyword=computer_aided_diagnosis|lang=zh-CN|style=Feynman)系统正在分析一张医学扫描图 [@problem_id:4534142]。如果系统报告恶性肿瘤的概率很高，临床医生需要知道*为什么*。模型是不确定是因为扫描本身模棱两可（[偶然不确定性](@keyword=aleatoric_uncertainty|lang=zh-CN|style=Feynman)），还是因为这是一个模型不熟悉的[罕见病](@keyword=rare_diseases|lang=zh-CN|style=Feynman)例（认知不确定性）？通过分解总预测不确定性，一个用 VI 训练的[贝叶斯神经网络](@keyword=bayesian_neural_networks|lang=zh-CN|style=Feynman)可以提供这一关键背景信息。其输出的方差可以分解为数据噪声项和[模型参数不确定性](@keyword=model_parameter_uncertainty|lang=zh-CN|style=Feynman)项，从而为临床医生提供更丰富、更值得信赖的画面 [@problem_id:4871478]。这不仅适用于基于图像的模型，如[卷积神经网络](@keyword=convolutional_neural_networks|lang=zh-CN|style=Feynman)（CNNs），也适用于分析[序列数据](@keyword=sequential_data|lang=zh-CN|style=Feynman)的模型，例如从[电子健康记录](@keyword=electronic_health_record|lang=zh-CN|style=Feynman)中预测患者结局的贝叶斯 [LSTM](@keyword=lstms|lang=zh-CN|style=Feynman)，尽管这些模型的循环性质给推断过程带来了独特的计算挑战 [@problem_id:5196645]。

值得注意的是，[深度学习](@keyword=deep_learning|lang=zh-CN|style=Feynman)中一种名为蒙特卡洛 dropout 的流行技术，已被证明是一种巧妙的近似变分推断形式 [@problem_id:3500238]。通过在预测时保持 dropout 开启，并将同一样本多次输入网络，我们可以生成一个输出分布，其方差可以很好地作为认知不确定性的代理。这使得[贝叶斯深度学习](@keyword=bayesian_deep_learning|lang=zh-CN|style=Feynman)变得易于使用和实用，将一个曾经深奥的理论变成了构建更安全、更可靠人工智能的强大工具。

### 一种科学仪器：解混世界与比较思想

除了工程设计更好的工具，变分推断还作为一种强大的科学发现仪器。科学往往是一个“解混”的过程——即从复杂、混乱的观察中，梳理出产生它们的隐藏原因。

考虑[大型强子对撞机](@keyword=large_hadron_collider|lang=zh-CN|style=Feynman)的物理学家们面临的挑战。当粒子以巨大能量碰撞时，它们会产生一个我们感兴趣的主要“硬散射”事件，但这个事件叠加在较柔和的“基础事件”背景以及数十个同时发生的、称为“堆积效应”的无关碰撞之上。VI 可用于构建一个概率模型，将量能器单元中观察到的能量视为这三个隐藏分量的总和。通过应用变分算法，物理学家可以推断每个分量对总信号的最可能贡献，从而有效地清洗数据并分离出感兴趣的事件 [@problem_id:3528701]。同样的原理也适用于其他领域，例如在材料科学中为昂贵的[量子模拟](@keyword=quantum_simulation|lang=zh-CN|style=Feynman)构建快速的代理模型，其中 VI 可以提供关键的[不确定性估计](@keyword=uncertainty_estimation|lang=zh-CN|style=Feynman)，告诉科学家何时可以信任这个快速模型 [@problem_id:3500238]。

也许更深刻的是，VI 提供了一个比较相互竞争的科学假说的框架。在贝叶斯世界观中，我们使用一个称为**模型证据**的量来比较模型，它代表了在给定整个模型的情况下观察到数据的概率。一个具有高证据值的模型是既能很好地拟[合数](@keyword=composite_numbers|lang=zh-CN|style=Feynman)据又不过于复杂的模型。[贝叶斯因子](@keyword=bayes_factor|lang=zh-CN|style=Feynman)，即两个[模型证据](@keyword=model_evidence|lang=zh-CN|style=Feynman)的比值，告诉我们哪个模型更受数据支持。

[计算模型](@keyword=model_of_computation|lang=zh-CN|style=Feynman)证据需要一个棘手的积分，但在这里 VI 提供了一个优雅的解决方案。我们在变分推断过程中最大化的那个量——[证据下界](@keyword=evidence_lower_bound|lang=zh-CN|style=Feynman)，或称**自由能**——正是[模型证据](@keyword=model_evidence|lang=zh-CN|style=Feynman)对数的一个紧密近似 [@problem_id:4157566]。这意味着，用 VI 训练模型的过程本身也为模型质量打出了一个分数！

神经科学家利用这一思想来裁决关于大脑功能的不同理论。使用一种称为[动态因果模型](@keyword=dynamic_causal_modeling|lang=zh-CN|style=Feynman)（DCM）的技术，他们可以构建几个合理的“布[线图](@keyword=line_graphs|lang=zh-CN|style=Feynman)”，代表不同大脑区域之间可能如何相互影响。通过使用变分推断将这些模型中的每一个拟合到 fMRI 数据上，他们可以比较产生的自由能。具有较高自由能的模型就是更受数据支持的模型，这使得研究人员能够对大脑的有效连接做出有原则的推断 [@problem_id:4157566] [@problem_id:4322100]。通过这种方式，变分推断成为一个虚拟的裁判，权衡着相互竞争的科学思想的证据。

### 大一统理论：[贝叶斯大脑](@keyword=bayesian_brain|lang=zh-CN|style=Feynman)

我们已经看到 VI 作为我们用来构建机器和理解数据的工具。但最诱人的想法是，变分推断不仅仅是我们*对*大脑所做的事情，而是大脑*本身正在做*的事情。这就是**贝叶斯大脑假说**的精髓。

该假说认为，大脑已经建立了一个内部的、概率性的**生成模型**来模拟世界——一个关于环境中隐藏的成因如何产生它所接收到的感官信号的模型 [@problem_id:4063533]。在这种观点下，感知是一个**近似贝叶斯推断**的过程：大脑反转其[生成模型](@keyword=generative_models|lang=zh-CN|style=Feynman)，以推断其感觉的最可能成因。当你看到一个影子移动时，你的大脑正在含蓄地计算各种原因——一只猫、风、一个捕食者——的后验概率，这是基于感官输入和你的先验知识。

这听起来像是一项极其复杂的任务，确实，精确推断是棘手的。这就是**[自由能原理](@keyword=free_energy_principle_2|lang=zh-CN|style=Feynman)**作为一种宏大的、统一的理论登场的地方 [@problem_id:4027150]。它提出，所有自组织系统，从单细胞到人类大脑，都在采取行动以最小化其[变分自由能](@keyword=variational_free_energy|lang=zh-CN|style=Feynman)。正如我们所见，最小化自由能在数学上等同于执行近似贝叶斯推断。因此，大脑是一个推断引擎，不断努力最小化其对世界的预测与接收到的感官证据之间的不匹配。这个单一而强大的思想将感知（更新信念以更好地解释感觉）和学习（更新模型本身以做出更好的长期预测）联系在一起。关于大脑的层级回路中如何实现这一点，一个流行的算法理论是**预测编码**，其中自上而下的预测与自下而上的感官信号进行比较，目标是在层级的每一级都最小化[预测误差](@keyword=prediction_error|lang=zh-CN|style=Feynman) [@problem_id:4027150] [@problem_id:4063533]。

该理论甚至延伸到了行动。**主动推断**将规划重塑为另一种形式的推断 [@problem_id:4028537]。策略，即行动序列，被视为待推断的潜在变量。大脑选择它预测将导致未来具有低自由能的行动。这意味着我们的行动既是为了实现我们的目标（体验我们有强烈先验偏好的状态），也是为了收集信息（减少关于世界的不确定性）。规划、感知、学习和行动都成为同一基本过程的不同方面：通过变分推断最小化自由能。

从构建可信赖人工智能的实际挑战，到解混信号的科学探索，再到关于生命和认知本身的深刻理论，变分推断提供了一条共同的数学线索。它证明了一个单一、优美的思想在照亮我们的世界以及，或许，我们自身方面的强大力量。