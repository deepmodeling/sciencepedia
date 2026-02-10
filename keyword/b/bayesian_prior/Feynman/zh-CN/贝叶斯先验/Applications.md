## 应用与跨学科联系

我们已经花了一些时间学习贝叶斯推断的形式化机制——先验、[似然](@keyword=likelihood|lang=zh-CN|style=Feynman)、后验。这是一个整洁的数学世界。但它有什么*用处*呢？这个优雅的、用证据更新信念的系统，是否真的能帮助我们理解真实世界，从亚原子粒子的微动到演化的宏大画卷？答案是响亮的“是”。[贝叶斯框架](@keyword=bayesian_framework|lang=zh-CN|style=Feynman)，特别是先验的真正美妙之处，不在于其数学的纯粹性，而在于其令人难以置信的灵活性。它是一种在不确定性下进行推理的通用语言，一旦你学会了说这种语言，你就会开始发现它的语法无处不在。

在本章中，我们将踏上一段旅程，穿越五花八门的科学学科，看看一个简单的[先验信念](@keyword=prior_belief|lang=zh-CN|style=Feynman)如何绽放成为发现的强大工具。我们将看到，先验不仅仅是一个主观猜测，而是一种形式化的方式，用以编码我们的知识、物理定律、怀疑精神以及我们对世界如何构成的模型。

### 作为物理约束的先验：塑造现实

想象你是一名试图解读带噪信号的分析师。如果你盯得够久，小孩的涂鸦也可能看起来像有意义的信息；而一个没有任何背景知识的计算机[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，很容易在[随机噪声](@keyword=stochastic_noise|lang=zh-CN|style=Feynman)中找到虚假的模式。我们如何引导我们的搜索走向合理的答案？我们使用我们已经*知道*的关于世界的知识。[贝叶斯先验](@keyword=bayesian_priors|lang=zh-CN|style=Feynman)正是向我们的数学模型低语这些规则和约束的完美工具。

考虑一下一位[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)家使用[X射线光电子能谱](@keyword=x_ray_photoelectron_spectroscopy|lang=zh-CN|style=Feynman)（XPS）探测[表面化学](@keyword=surface_chemistry|lang=zh-CN|style=Feynman)性质的世界。原始数据是一张谱图——一条[电子计数](@keyword=electron_counting|lang=zh-CN|style=Feynman)随能量变化的波浪线——通常伴随着重叠的峰和嘈杂的背景。一个简单的[曲线拟合](@keyword=curve_fitting|lang=zh-CN|style=Feynman)程序可能会以无数种方式解释这团乱麻。但物理学家知道自然遵循规则。对于某个特定元素，量子力学定律规定其谱学特征应该是一个“自旋-轨道双峰”：两个峰具有特征性的能量分离和可预测的强度比。此外，基础化学告诉我们，[氧化态](@keyword=formal_oxidation_state|lang=zh-CN|style=Feynman)原子的谱峰应该比还原态原子的谱峰有更高的结合能。

[贝叶斯分析](@keyword=bayesian_analysis|lang=zh-CN|style=Feynman)师不会僵硬地固定这些值，因为那样会很脆弱，且无法察觉细微的、真实世界的变化，而是将这些知识编码为先验 [@problem_id:2508687]。[自旋-轨道分裂](@keyword=spin_orbit_splitting|lang=zh-CN|style=Feynman)不被强制设为恰好 $1.5$ [电子伏特](@keyword=electron_volt|lang=zh-CN|style=Feynman)，而是被赋予一个以 $1.5$ 为中心、方差很小的先验分布。这告诉模型：“我[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)分裂大约在这里，但如果数据足够有力，我愿意相信它略有不同。”[氧化态](@keyword=formal_oxidation_state|lang=zh-CN|style=Feynman)峰的能量 $E_{\mathrm{ox}}$ 必须大于还原态峰的能量 $E_{\mathrm{red}}$ 这一知识，可以作为简单的非[等式约束](@keyword=equality_constraints|lang=zh-CN|style=Feynman)来施加：对于任何 $E_{\mathrm{ox}} < E_{\mathrm{red}}$ 的解，其[先验概率](@keyword=a_priori_probabilities|lang=zh-CN|style=Feynman)被设为零。这可以防止模型返回物理上荒谬的结果。先验的作用不像一副镣铐，而更像雕塑家的手，温和地引导模型从嘈杂数据的粗糙石料中雕刻出物理上有意义的现实。

同样的原则在工程领域也拯救了我们，尤其是在面对所谓的“[逆问题](@keyword=inverse_problems|lang=zh-CN|style=Feynman)”时。想象一下，你试图确定施加在一块金属板上随时间变化的热量，但你只能测量其内部深处一个点的温度 [@problem_id:2497805]。这是一个极其困难的问题；热量会扩散并变得平滑，因此关于初始快速变化的通量信息在到达你的传感器时已经变得微弱且被扰乱。你[温度测量](@keyword=thermometry|lang=zh-CN|style=Feynman)的微小误差可能导致对表面热通量的重建结果大相径庭，且常常是荒谬的。这个问题是“不适定的”。

在这里，先验再次成为我们与现实的纽带。如果我们有一些先验知识——也许来自过去的实验——知道热通量可能在某个平均值附近波动，我们可以将其编码为一个信息丰富的高斯先验。当模型试图用一个剧烈[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的热通量来解释数据中的微[小波](@keyword=wavelets|lang=zh-CN|style=Feynman)动时，先验会温和地将其[拉回](@keyword=pullback|lang=zh-CN|style=Feynman)，仿佛在说：“根据我们所知，那是一个非常不可能的模式。”最终的解，即后验估计，变成了一个优美而稳定的折中：我们的先验信念与新测量数据所讲述的故事之间的[加权平均](@keyword=weighted_average|lang=zh-CN|style=Feynman)。这种“收缩”效应，将估计值从嘈杂的数据拉向一个合理的先验均值，是[贝叶斯正则化](@keyword=bayesian_regularization|lang=zh-CN|style=Feynman)的一个标志，将一个无解的问题变成了一个可解的问题。

### 作为假设的先验：权衡证据

科学不仅仅是测量事物，它还关乎权衡相互竞争的观点。这种新药有效，还是和安慰剂没什么两样？这次基因杂交遵循了[孟德尔定律](@keyword=mendel_s_laws|lang=zh-CN|style=Feynman)，还是存在某种隐藏的扭曲？人类是单次浪潮走出非洲的，还是故事更为复杂？[贝叶斯框架](@keyword=bayesian_framework|lang=zh-CN|style=Feynman)提供了一种自然而直观的方式来组织假设之间的较量。

让我们回到遗传学。一个经典的实验涉及将两株[杂合性](@keyword=heterozygosity|lang=zh-CN|style=Feynman)状的豌豆植株进行杂交（$Aa \times Aa$）。[孟德尔分离定律](@keyword=mendel_s_law_of_segregation|lang=zh-CN|style=Feynman)预测，后代的基因型将以 $1:2:1$ 的精确比例出现，分别对应 $AA$、$Aa$ 和 $aa$。这意味着 $AA$ 个体的比例应该恰好是 $p = 1/4$。但如果我们做了实验，观察到的比例不完全是 $1/4$ 呢？这仅仅是随机机会，还是定律被违背了？

一种名为“尖峰厚板”（spike-and-slab）先验的强大贝叶斯工具，让我们能直接提出这个问题 [@problem_id:2828750]。想象你在下注。你可以将一部分信念——“尖峰”——押在定律*完全*正确（$p=1/4$）这个假设上。然后你将余下的信念——“厚板”——分散在 $p$ 的一个连续的备选值范围内。在你收集数据（计算后代数量）后，[贝叶斯定理](@keyword=bayes__theorem|lang=zh-CN|style=Feynman)会告诉你如何精确地重新分配你的信念。如果数据与 $p=1/4$ 高度一致，“尖峰”上的后验概率将会增加。如果数据强烈地偏离 $1/4$，信念将从尖峰流向厚板。后验概率为我们提供了一个直接、可解释的度量，衡量数据为支持或反对精确的孟德尔假设提供了多少证据。

这种比较模型的方法可以扩展到处理科学中一些最宏大的问题，即使其底层过程异常复杂。思考一下我们自身的起源问题 [@problem_id:1973148]。“走出非洲”的一个模型假设，一个单一、充分混合的非洲种群是所有非非洲种群的始祖。另一个模型则认为，创始群体是两个更古老、已分离的非洲谱系的混合体。这些模型的似然函数，即预测我们今天所见的[遗传模式](@keyword=genetic_inheritance_patterns|lang=zh-CN|style=Feynman)的函数，在数学上是难以处理的。

在这里，我们可以使用一种叫做近似贝叶斯计算（ABC）的巧妙技术。它的工作方式如下：我们用计算机在两种竞争模型下，分别模拟数千个新的遗传数据集。然后，我们将每个模拟数据集与我们*实际*观察到的遗传数据进行比较。如果一个模拟产生的数据“看起来像”真实数据（即其[摘要统计](@keyword=summary_statistics|lang=zh-CN|style=Feynman)量非常接近），我们就“接受”它。在混合来源模型下接受的模拟次数与在单一来源模型下接受的模拟次数之比，为我们提供了[贝叶斯因子](@keyword=bayes_factor|lang=zh-CN|style=Feynman)的近似值。它告诉我们哪个模型更能生成我们所看到的世界。如果混合来源模型产生的“被接受”模拟是单一来源模型的三倍，那么数据告诉我们这个假设的可能性是后者的三倍。然后，我们可以用这个[贝叶斯因子](@keyword=bayes_factor|lang=zh-CN|style=Feynman)来更新我们对这两个模型的先验信念，从而为一个关于我们过去的深刻问题提供一个定量的答案。

同样的权衡证据的逻辑也应用于临床医学这个高度实践性的领域。当在患者身上发现一个新的基因变异时，它是一个无害的怪癖还是其疾病的病因？美国[医学遗传学](@keyword=medical_genetics|lang=zh-CN|style=Feynman)与基因组学学会（ACMG）建立了一套证据标准（代码如“PVS1”代表“[致病性](@keyword=pathogenicity|lang=zh-CN|style=Feynman)非常强”，或“BP4”代表“良性支持”）。这个系统可以优雅地用[贝叶斯框架](@keyword=bayesian_framework|lang=zh-CN|style=Feynman)来表述 [@problem_id:2378888]。我们从一个该变异是[致病性](@keyword=pathogenicity|lang=zh-CN|style=Feynman)的先验概率开始——对于一个随机变异来说，这个概率可能非常低。我们找到的每一条证据，对应一个 ACMG 代码，都与一个似然比相关联。一条“强”的[致病性](@keyword=pathogenicity|lang=zh-CN|style=Feynman)证据可能意味着“如果该变异是[致病性](@keyword=pathogenicity|lang=zh-CN|style=Feynman)的，这个观察结果出现的可能性是其为良性时的 18.7 倍”。当遗传学家收集线索时，他们只需将先验[优势比](@keyword=odds_ratio|lang=zh-CN|style=Feynman)乘以每条新证据的似然比。信念被逐条线索地顺序更新，为[致病性](@keyword=pathogenicity|lang=zh-CN|style=Feynman)的支持或反对提供了实时累加的证据。

### 作为怀疑主义的先验：“非凡的主张需要非凡的证据”

先验最深刻的用途之一是强制执行一种健康的科学怀疑精神。在一个有效的市场中，一个真正的、无风险的[套利机会](@keyword=arbitrage_opportunity|lang=zh-CN|style=Feynman)——一台印钞机——应该是极其罕见的。如果有人声称找到了一个，我们的默认立场应该是怀疑。

[贝叶斯框架](@keyword=bayesian_framework|lang=zh-CN|style=Feynman)允许我们将这种怀疑形式化 [@problem_id:2375575]。我们可以为一个给定的交易策略代表真实套利的假设设置一个非常小的先验概率 $\pi_A$。这意味着我们反对套利的先验[优势比](@keyword=odds_ratio|lang=zh-CN|style=Feynman)是巨大的。为了让数据说服我们，它必须提供一个压倒性的信号。支持套利的[贝叶斯因子](@keyword=bayes_factor|lang=zh-CN|style=Feynman)必须足够大才能克服我们最初的怀疑。如果一个策略在有限的样本中显示出微小的正回报，一个带有怀疑先验的模型很可能会断定这只是噪音。只有当证据如此强大和一致，以至于无法用随机性来解释时，它才会将一个机会标记为真实。这是“非凡的主张需要非凡的证据”这一原则的数学体现。先验并不是在偏袒结果，而是在确保我们不会因为追逐噪音中的鬼影而自欺欺人。

### 作为蓝图的先验：构建[分层模型](@keyword=hierarchical_models|lang=zh-CN|style=Feynman)

到目前为止，我们已经看到先验作为约束、假设权重和怀疑尺度。但它们最强大的角色或许是作为构建复杂的、多层次现实模型的建筑蓝图。这就是[分层贝叶斯模型](@keyword=hierarchical_bayesian_models|lang=zh-CN|style=Feynman)的领域。

让我们看看合成生物学的最前沿：为 [CRISPR](@keyword=crispr|lang=zh-CN|style=Feynman) [基因编辑](@keyword=gene_editing|lang=zh-CN|style=Feynman)设计向导 RNA。一个关键的挑战是确保向导 RNA 切割基因组中的预期靶点，但避免“脱靶”位点。我们如何预测在特定位点发生脱靶切割的概率？我们可以建立一个模型，其中切割的*先验概率*不是一个固定数值，而是其本身是该位点特征的函数：错配的 DNA 碱[基数](@keyword=cardinality|lang=zh-CN|style=Feynman)量、其在基因组中的位置、[染色质](@keyword=chromatin|lang=zh-CN|style=Feynman)的可及性等等 [@problem_id:2727874]。这个先验模型，也许是一个[逻辑回归](@keyword=logistic_regression|lang=zh-CN|style=Feynman)，封装了我们现有的生物学知识。然后，我们可以进行一个实验来测量整个基因组的切割活性。这个新数据被用来*更新*我们基于特征的先验，从而得到一个更准确的后验预测。这是一个两阶段的杰作：一个关于先验的模型，然后由数据来更新。

这种分层逻辑是现代[系统发育学](@keyword=phylogenetics|lang=zh-CN|style=Feynman)——重建[生命之树](@keyword=tree_of_life|lang=zh-CN|style=Feynman)的科学——的引擎。[多物种溯祖](@keyword=multispecies_coalescent|lang=zh-CN|style=Feynman)（MSC）模型就是一个美丽的例子 [@problem_id:2375040]。它可以通过一个类比来理解：把物种的进化史想象成一棵分枝的“思想谱系树”。在每个文化谱系（树上的一个分支）内部，个体持有信念。单个信念的历史就是一个“信念宗谱”。由于随机机会（类似于遗传漂变），一个信念宗谱可能与思想谱系树的分支模式不匹配——这种现象被称为[不完全谱系分选](@keyword=incomplete_lineage_sorting|lang=zh-CN|style=Feynman)。MSC 是一个捕捉这一点的[分层模型](@keyword=hierarchical_models|lang=zh-CN|style=Feynman)：
1.  在最高层，有一个物种树（$S$），带有种群大小（$\eta$）等参数。这棵树是未知的，我们对它有一个先验。
2.  物种树作为[基因树](@keyword=gene_tree|lang=zh-CN|style=Feynman)（$G$）的*先验*。给定一个物种树，溯祖过程会导出一个关于[基因树](@keyword=gene_tree|lang=zh-CN|style=Feynman)可能形状的[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)。基因树更可能与物种树匹配，但也可能存在不一致，模型量化了这种不一致的概率。
3.  每个基因树反过来又作为观测到的 DNA 序列数据（$X$）的*先验*。给定[基因树](@keyword=gene_tree|lang=zh-CN|style=Feynman)，一个标准的[替换模型](@keyword=substitution_models|lang=zh-CN|style=Feynman)给出了我们实际看到的 DNA 序列的似然。

推断过程是通过同时学习这个层次结构的所有层面来进行的 [@problem_id:2706442]。来自底层的 DNA 序列信息向上流动，为我们对基因树的估计提供信息；而所有[基因树](@keyword=gene_tree|lang=zh-CN|style=Feynman)的综合信息向上流动，为我们对物种树的估计提供信息。这种结构使我们能够解开数百万年来塑造基因组的复杂、多层次的过程。同样的逻辑也是生态学中[适应性管理](@keyword=adaptive_management|lang=zh-CN|style=Feynman)的核心，在生态学中，我们必须同时了解系统的状态（例如，两种害虫模型中哪一个是正确的）并决定如何对其采取行动 [@problem_id:2499076]。我们从竞争模型的[先验概率](@keyword=a_priori_probabilities|lang=zh-CN|style=Feynman)开始，对系统的每一次观察都让我们能够更新这些概率，从而随着时间的推移完善我们的知识并改进我们的决策。

从在[光谱仪](@keyword=spectrometer|lang=zh-CN|style=Feynman)中强制执行物理定律，到重建生命之树，[贝叶斯先验](@keyword=bayesian_priors|lang=zh-CN|style=Feynman)证明了自己是科学家工具箱中最通用、最强大的概念之一。它是学习的形式化机制，是一座桥梁，连接了我们对世界已有的理解和新数据讲述的新故事，从而创造出一幅更丰富、更稳健的现实图景。