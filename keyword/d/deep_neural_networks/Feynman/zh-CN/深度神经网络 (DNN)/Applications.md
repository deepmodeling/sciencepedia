## 应用与跨学科联系

我们花了一些时间，可以说是拆解了手表，检查了[深度神经网络](@keyword=deep_neural_networks|lang=zh-CN|style=Feynman)的齿轮和弹簧。现在是时候把它重新组装起来，并提出真正的问题：它报的是什么时间？这些错综复杂的数学机器到底能*做*什么？事实上，我们正处在一个应用爆炸的时代。我们发现这些网络无处不在，从平凡到革命性。仅仅列出它们的用途就像通过罗列书名来编目一个图书馆的内容；这完全不能告诉你里面的故事。

因此，让我们踏上一段旅程，穿越这些网络所栖居的思想版图。我们将看到它们如何为旧问题提供一种新的、强有力的实用主义视角，它们如何作为全新的科学仪器来探测未知，以及它们如何与传统的[科学方法](@keyword=scientific_method|lang=zh-CN|style=Feynman)展开一场深刻而迷人的对话。最后，我们将上升到最高的抽象层次，看看这些网络如何与数学和[可计算性](@keyword=computability|lang=zh-CN|style=Feynman)本身的根本基石相联系。

### 新视角：实用主义的力量

几十年来，科学和工程领域的许多问题都是用一种“生成式”哲学来处理的。如果你想制造一台机器来识别口语单词，你会尝试为每个音素建立一个详细的统计模型，描述人类声道如何产生声音。你会试图模拟整个过程，在某种意义上，自己生成数据。这是一种优美、有原则的方法，但它也异常困难。现实世界是混乱的，我们的模型总是近似的。

深度神经网络提供了一种不同的、极其有效的哲学：“[判别式](@keyword=discriminant|lang=zh-CN|style=Feynman)”方法。一个为语音识别训练的深度神经网络不一定学习了一个关于声带和[共振频率](@keyword=resonant_frequency|lang=zh-CN|style=Feynman)的深度模型。相反，它只是学会了区分声音。它问的是：“在这个声学信号中，有哪些最小的、必不可少的特征能让我区分'cat'和'scat'？”它只关注决策边界，即分隔一个类别与另一个类别的线，而不需要对两边的领域有完整的地图[@problem_id:3124859]。这种从建模世界（$p(\text{data}|\text{class})$）到建模决策（$p(\text{class}|\text{data})$）的转变，是深度学习成功背后的驱动力。这是一种纯粹实用主义的[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)。

但网络做出决策后会发生什么？在现实世界中，并非所有错误都是等价的。想象一辆自动驾驶汽车的摄像头系统，它使用一个[深度神经网络](@keyword=deep_neural_networks|lang=zh-CN|style=Feynman)进行[语义分割](@keyword=semantic_segmentation|lang=zh-CN|style=Feynman)——将其视野中的每个像素标记为“道路”、“天空”、“其他车辆”或“行人”。网络可能会输出它有$0.58$的把握认为一个像素是“背景”，$0.27$的把握是“道路”，$0.15$的把握是“行人”。一种天真的方法是简单地选择最可能的类别：“背景”。

但如果那个像素*是*一个行人呢？将行人错误地标记为背景是一个灾难性的错误，远比将道路错误地标记为背景严重得多。在这里，[深度学习](@keyword=deep_learning|lang=zh-CN|style=Feynman)与有百年历史的贝叶斯决策理论相联系。我们可以为每种类型的错误分配一个成本。将行人误认为道路的成本可能是将道路误认为建筑物的成本的100倍。网络的工作是提供概率。工程师的工作是将这些概率与一个[成本矩阵](@keyword=cost_matrix|lang=zh-CN|style=Feynman)相结合，以做出最小化*[期望风险](@keyword=expected_risk|lang=zh-CN|style=Feynman)*的决策[@problem_id:3136306]。最优选择不再仅仅是最可能的那个，而是代表最安全赌注的那个。通过这种方式，[神经网络](@keyword=neural_networks|lang=zh-CN|style=Feynman)的“黑箱”成为一个透明、理性的[风险管理](@keyword=risk_management|lang=zh-CN|style=Feynman)系统中至关重要但又融为一体的组成部分。

### 新仪器：开拓科学前沿

也许最激动人心的故事是深度学习作为一种新型科学仪器的角色。就像望远镜或显微镜一样，它让我们能够看到我们以前从未见过的东西。

最著名的例子是在结构生物学领域。50年来，从蛋白质的一维氨基酸序列预测其三维形状一直是一个重大挑战。然后[AlphaFold](@keyword=alphafold|lang=zh-CN|style=Feynman)出现了。其核心是一个[深度神经网络](@keyword=deep_neural_networks|lang=zh-CN|style=Feynman)，它学习了将序列翻译成结构的极其复杂的“语法”。但当我们审视实际过程时，一个有趣的见解浮现出来。预测本身——在强大的GPU上通过巨大的神经网络进行[前向传播](@keyword=forward_pass|lang=zh-CN|style=Feynman)——出奇地快。真正的瓶颈往往是预备步骤：在巨大的已知[蛋白质数据库](@keyword=protein_databases|lang=zh-CN|style=Feynman)中搜索，以找到进化上相关的序列。这个多重序列比对（MSA）提供了至关重要的背景，即网络施展其魔力所需的进化线索[@problem_id:2107886]。这告诉我们，这场革命不仅仅是关于聪明的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)；它是关于这些[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)与大数据的协同作用。网络是杰出的大脑，但MSA是它需要阅读的浩瀚图书馆。

应用不仅限于做出预测；深度神经网络还可以改进我们对科学数据的看法。在生物学中，我们经常寻找相关性。如果一个[蛋白质序列](@keyword=protein_sequence|lang=zh-CN|style=Feynman)中的两个氨基酸在进化过程中共同突变，这暗示它们可能在物理上接触。但这个信号极其嘈杂。两个[残基](@keyword=residue|lang=zh-CN|style=Feynman)可能共同进化，不是因为它们接触，而是因为它们都接触了第三个中心[残基](@keyword=residue|lang=zh-CN|style=Feynman)。这就是直接与间接相关性的问题。像[直接耦合分析](@keyword=direct_coupling_analysis|lang=zh-CN|style=Feynman)（DCA）这样的技术被开发出来以“去噪”这个信号，但它们计算量很大。研究人员已经表明，可以训练一个[深度神经网络](@keyword=deep_neural_networks|lang=zh-CN|style=Feynman)来直接学习这种转换——将一个充满噪声的简单相关性矩阵作为输入，输出一个清晰的直接[耦合矩阵](@keyword=coupling_matrix|lang=zh-CN|style=Feynman)[@problem_id:2380711]。网络学习了全局校正效应，像一个复杂的过滤器一样，解开了复杂的相互作用网络。

这种力量使我们能够探索那些在实验上无法触及的问题。考虑一下[人类进化](@keyword=human_evolution|lang=zh-CN|style=Feynman)的深远历史。我们知道我们的祖先曾与尼安德特人杂交。但他们是否与其他“幽灵”古人类（我们没有[化石记录](@keyword=fossil_record|lang=zh-CN|style=Feynman)）杂交过？我们无法进行这个实验。但我们可以模拟它。利用[群体遗传学](@keyword=population_genetics|lang=zh-CN|style=Feynman)，我们可以在各种情景下创建人工基因组——一些有[幽灵基因渗入](@keyword=ghost_introgression|lang=zh-CN|style=Feynman)，一些没有。这些模拟事件在基因组的统计数据中留下了微妙而独特的印记。然后我们可以训练一个[深度神经网络](@keyword=deep_neural_networks|lang=zh-CN|style=Feynman)，使其成为在我们模拟的宇宙中区分这些模式的专家。一旦训练完成，我们就可以将这位专家应用到真实的人类基因组上，寻找这些早已失落的相遇留下的微弱统计回响[@problem_id:2692255]。这种基于模拟的推断[范式](@keyword=normal_forms|lang=zh-CN|style=Feynman)是一种强大的新型科学研究方式，而深度神经网络是使其成为可能的引擎。

### 对话：第一性原理与黑箱

在[深度神经网络](@keyword=deep_neural_networks|lang=zh-CN|style=Feynman)的数据驱动、“黑箱”性质与建立在[第一性原理](@keyword=ab_initio|lang=zh-CN|style=Feynman)、物理定律和[可解释模型](@keyword=interpretable_models|lang=zh-CN|style=Feynman)之上的传统[科学方法](@keyword=scientific_method|lang=zh-CN|style=Feynman)之间，存在一种天然的[张力](@keyword=tension_force|lang=zh-CN|style=Feynman)。然而，这种[张力](@keyword=tension_force|lang=zh-CN|style=Feynman)正被证明是极富成效的。

考虑一下合成生物学中设计[核糖体结合位点](@keyword=ribosome_binding_site|lang=zh-CN|style=Feynman)（RBS）的挑战，这是一个控制基因产生多少蛋白质的短RNA序列。人们可以基于[RNA折叠](@keyword=rna_folding|lang=zh-CN|style=Feynman)和[核糖体](@keyword=ribosome|lang=zh-CN|style=Feynman)结合的[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)建立一个“机理”模型。这个模型是基于[第一性原理](@keyword=ab_initio|lang=zh-CN|style=Feynman)构建的。或者，人们可以用成千上万个RBS序列及其测得的[蛋白质输出](@keyword=protein_export|lang=zh-CN|style=Feynman)的例子来训练一个[深度神经网络](@keyword=deep_neural_networks|lang=zh-CN|style=Feynman)。

当我们比较它们时，一个美妙的故事展开了。在看起来与训练数据非常相似的数据上，[深度神经网络](@keyword=deep_neural_networks|lang=zh-CN|style=Feynman)更准确。它记住了那个特定背景下的复杂模式。但当在“分布外”数据上测试时——比如说，具有不同结构特性的序列——[深度神经网络](@keyword=deep_neural_networks|lang=zh-CN|style=Feynman)的性能常常会崩溃。基于物理的模型，虽然在原始数据集上准确性较低，但事实证明它更鲁棒，并且能更好地泛化到新情况。它有一个基于物理定律的更强的“[归纳偏置](@keyword=inductive_bias|lang=zh-CN|style=Feynman)”，即使数据发生变化，这些定律仍然成立[@problem_id:2773028]。这是偏差-方差权衡的一个完美例证。灵活的深度神经网络偏差低但方差高，使其容易过拟合；刚性的物理[模型偏差](@keyword=model_bias|lang=zh-CN|style=Feynman)较高但方差较低，使其更稳定。没有哪个是绝对“更好”的；它们是用于不同目标的不同工具。

未来不在于选择其一，而在于将它们融合。想象一下试图诊断一种可能由单个[基因突变](@keyword=genetic_mutations|lang=zh-CN|style=Feynman)或环境暴露引起的疾病——一种“[拟表型](@keyword=phenocopy|lang=zh-CN|style=Feynman)”。我们有每个病人的大量数据：他们的基因表达（[转录组](@keyword=transcriptome|lang=zh-CN|style=Feynman)）、蛋白质水平（蛋白质组）和代谢物水平（[代谢组](@keyword=metabolome|lang=zh-CN|style=Feynman)）。一个天真的[深度神经网络](@keyword=deep_neural_networks|lang=zh-CN|style=Feynman)可能只是将所有这些数据连接成一个巨大的向量，忽略了[分子生物学中心法则](@keyword=the_central_dogma_of_molecular_biology|lang=zh-CN|style=Feynman)（DNA $\rightarrow$ RNA $\rightarrow$ 蛋白质）所描述的美妙结构。一个遗传损伤原则上应该在这些数据类型之间产生一系列连贯的变化。一种更复杂的方法是建立一个[混合模型](@keyword=mixture_models|lang=zh-CN|style=Feynman)——一个贝叶斯[潜因子模型](@keyword=latent_factor_models|lang=zh-CN|style=Feynman)——它受到[神经网络架构](@keyword=neural_network_architecture|lang=zh-CN|style=Feynman)的启发，但受到生物学现实的约束。它学习代[表生](@keyword=supergene|lang=zh-CN|style=Feynman)物过程的共享“[潜因子](@keyword=latent_factors|lang=zh-CN|style=Feynman)”，但它是在一个理解[转录组学](@keyword=transcriptomics|lang=zh-CN|style=Feynman)、蛋白质组学和[代谢组学](@keyword=metabolomics|lang=zh-CN|style=Feynman)不仅仅是任意数字列表，而是一个单一生物系统中因果相连的层次的框架内进行的[@problem_id:2807724]。这就是前沿：将深度神经网络的[表示学习](@keyword=representation_learning|lang=zh-CN|style=Feynman)能力与第一性原理科学的可解释性和鲁棒性相结合的[混合模型](@keyword=mixture_models|lang=zh-CN|style=Feynman)。

### 抽象宇宙：数学与计算的极限

最后，让我们把视野放大到纯粹的抽象世界。从数学家的角度来看，这些网络是什么？一个深度神经网络只是一个非常复杂的、高维的函数，$f(x)$。这个函数的景观——它的山丘、山谷和悬崖——决定了它的行为。关于[深度神经网络](@keyword=deep_neural_networks|lang=zh-CN|style=Feynman)的一大焦虑是它们的脆弱性；对输入图像的一个微小、难以察觉的扰动有时会导致网络出现严重的错误分类。这就像站在函数景观中一个隐藏的悬崖边。

我们如何能确定自己站在安全的地面上？在这里，我们可以求助于一个来自17世纪的工具：[泰勒定理](@keyword=taylor_s_theorem|lang=zh-CN|style=Feynman)。就像我们可以用切线在局部近似一条曲线一样，我们可以用它的线性部分$\nabla f(x)^\top \delta$来近似我们的高维函数$f(x+\delta)$。这个近似的误差由[余项](@keyword=remainder_term|lang=zh-CN|style=Feynman)捕捉，它取决于函数的曲率——它的二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)，即Hessian矩阵$H_f$。如果我们能证明我们函数的曲率是有界的（即，它的[谱范数](@keyword=spectral_norm|lang=zh-CN|style=Feynman)小于某个常数$M$），我们就能推导出一个严格的数学保证。我们可以肯定地说，对于任何大小不超过$\epsilon$的扰动$\delta$，函数的输出变化不会超过一个特定的量。这使我们能够计算出一个“鲁棒性证书”，一个确保网络预测保持稳定的充分条件[@problem_id:3266756]。这是一个古典数学为现代复杂对象提供清晰视角的优美例子。

这把我们带到了最后一个问题。我们已经看到了深度神经网络能做什么。它们的最终极限是什么？它们能*计算*什么？[丘奇-图灵论题](@keyword=church_turing_thesis|lang=zh-CN|style=Feynman)假设，任何可以被直观地“计算”的函数都可以由[图灵机计算](@keyword=turing_machine_computation|lang=zh-CN|style=Feynman)。一个在真实计算机上运行的真实[神经网络](@keyword=neural_networks|lang=zh-CN|style=Feynman)，当然是由[图灵机模拟](@keyword=turing_machine_simulation|lang=zh-CN|style=Feynman)的，并且能做的不超过[图灵机](@keyword=turing_machines|lang=zh-CN|style=Feynman)。但一个*理想化*的[神经网络](@keyword=neural_networks|lang=zh-CN|style=Feynman)呢？

考虑一个思想实验：一个拥有可数无限个[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)、经过无限步训练的网络。每个组件——初始权重、[激活函数](@keyword=activation_functions|lang=zh-CN|style=Feynman)、训练[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)——都是完全可计算的。在任何有限的训练步骤$t$计算出的函数，我们称之为$N_t(x)$，因此是可计算的。但是[极限函数](@keyword=limit_function|lang=zh-CN|style=Feynman)，$f(x) = \lim_{t \to \infty} N_t(x)$呢？事实证明，这个极限函数不保证是图灵可计算的。一个[可计算函数](@keyword=computable_functions|lang=zh-CN|style=Feynman)的序列可以收敛到一个不可计算的函数。事实上，这样一个过程理论上可以计算出停机问题——经典不可计算问题——的答案[@problem_id:1450211]。这不是建造一个现实世界超计算机的配方。相反，这是[计算理论](@keyword=theory_of_computation|lang=zh-CN|style=Feynman)的一个深刻见解，它将现代深度学习的机器与关于知识和[形式系统](@keyword=formal_systems|lang=zh-CN|style=Feynman)极限的最深层问题联系起来。

从风险管理的实用性，到生物学的巨大挑战，再到计算的哲学边界，深度神经网络不仅仅是一个工具。它们是一种新的语言，一个新的视角，也是我们永无止境的发现之旅中的新伙伴。