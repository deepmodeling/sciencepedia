## 应用与跨学科联系

我们已经花时间学习了[随机过程](@keyword=random_process|lang=zh-CN|style=Feynman)的正式规则和行为——泊松过程、布朗运动和奥恩斯坦-乌伦贝克运动及其相关过程。人们可能倾向于认为这些只是数学上的奇珍异品，是在黑板上玩的抽象游戏。但事实远非如此。真正的魔力始于我们将这些工具应用于现实世界。我们发现了一些非凡的东西：同样的基本随机模式，同样的数学结构，在科学最不相关的角落里一次又一次地出现。就好像自然界，尽管其复杂性令人困惑，却使用了一套惊人地小而优雅的随机蓝图。

这段旅程不是为了给清晰的确定性定律寻找杂乱的例外，而是为了认识到随机性并非秩序的敌人，而是其伙伴。它是变化的引擎，多样性的源泉，以及复杂系统的基本构成。在开始之前，有必要澄清我们所说的“不确定性”是什么意思。在评估像[基因驱动](@keyword=gene_drive|lang=zh-CN|style=Feynman)这样的新技术所带来的生态风险这类复杂任务中，科学家区分两种不确定性 [@problem_id:2766835]。第一种是**[认知不确定性](@keyword=epistemic_uncertainty|lang=zh-CN|style=Feynman)**（epistemic uncertainty），这只是“无知”的一个花哨说法。这是因为我们没有收集足够数据而产生的不确定性。我们可以通过做更多实验、更精确地测量参数来减少它。第二种是**[偶然不确定性](@keyword=aleatory_uncertainty|lang=zh-CN|style=Feynman)**（aleatory uncertainty），这是固有的、不可简化的偶然性。就像掷骰子。即使我们对系统的所有参数有完美的了解，这种随机性仍然存在。[随机过程](@keyword=random_process|lang=zh-CN|style=Feynman)模型正是为了描述这第二种不确定性——世界深刻、内在的随机性——而设计的。

### 原子的闪烁与河流的流动

让我们从最小的尺度开始我们的旅程。想象一个孤立的原子。当它被激发时，它会试图以一个单一、精确的频率辐射光，就像一个音叉发出纯净的音调。但如果这个原子处于气体中，不断被邻近的原子碰撞和推挤，会发生什么呢？每一次碰撞都是一个随机事件。模拟一连串独立的、无记忆事件的最简单方法，当然是[泊松过程](@keyword=poisson_process|lang=zh-CN|style=Feynman)。我们可以想象我们原子的光波相位保持稳定，然后在碰撞的瞬间，被立即[随机重置](@keyword=stochastic_resetting|lang=zh-CN|style=Feynman)。

这首被随机中断的歌曲的结果是什么？原子不再发射纯净的频率。这些中断使信号变得“模糊”。如果我们使用维纳-[辛钦定理](@keyword=khintchine_s_theorem|lang=zh-CN|style=Feynman)来找到这束光的[功率谱](@keyword=power_spectrum|lang=zh-CN|style=Feynman)，我们得到的不是一个尖锐的峰值，而是一条优美、平滑的曲线，称为[洛伦兹分布](@keyword=lorentzian_distribution|lang=zh-CN|style=Feynman) [@problem_id:1767384]。这条曲线的宽度与碰撞率 $\gamma$ 直接相关。碰撞越快，[谱线](@keyword=spectral_line|lang=zh-CN|style=Feynman)越宽。这种现象称为压力增宽，是天文学家和物理学家每天都在测量的东西。它是微观、泊松分布的混沌所产生的直接、宏观的后果。原子的随机舞蹈在来自遥远恒星的光中创造出可预测的形状。

现在，让我们从原子尺度跃迁到人类尺度，从一个气体容器到我们脚下的土地。想象一种污染物泄漏到地下水中。我们可能[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)它会随水流动并因[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)而稍微散开。但实际上，污染物羽流通常会比这种简单设想散布得远得多，形成长长的、持久的“尾巴”。为什么？原因与原子的故事惊人地相似。地面不是均匀的。污染物粒子的旅程不是在空间中的“[随机游走](@keyword=random_walk|lang=zh-CN|style=Feynman)”，而是在*速度*上的“[随机游走](@keyword=random_walk|lang=zh-CN|style=Feynman)”。当它移动时，它会遇到一些土壤区域，在这些区域它会强烈吸附（高吸附系数 $K_d$）并缓慢移动，而在另一些区域则吸附较弱并快速移动。

介质本身的这种可变性产生了一种称为宏观弥散的巨大[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)效应。如果不同类型土壤的斑块小且混合均匀，整体效果就像一个增强版的[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)，羽流看起来大致呈高斯分布。但如果存在极其“粘性”材料的罕见斑块，或者如果斑块在很长的距离上相关，那么简单的图像就完全失效了。一个粒子可能会“卡住”很长时间，导致浓度分布出现长尾。这被称为非菲克输运，要描述它，我们需要更高级的工具，如[连续时间随机游走](@keyword=continuous_time_random_walk|lang=zh-CN|style=Feynman)（CTRWs），其中在粘性区域的“等待时间”可以从[重尾分布](@keyword=heavy_tailed_distributions|lang=zh-CN|style=Feynman)中抽取 [@problem_id:2478707]。这里的相似性是深刻的：原子光波的随机中断和污染物路径上的随机障碍是同一枚硬币的两面，需要同一系列的数学思想才能被理解。

### 生命的节律：一场进化军备竞赛

在生物学中，偶然与必然的相互作用无处不在。思考一下细菌与捕食它们的病毒——[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)——之间的古老战争。许多[细菌进化](@keyword=bacterial_evolution|lang=zh-CN|style=Feynman)出一种称为[CRISPR-Cas](@keyword=crispr_cas|lang=zh-CN|style=Feynman)的复杂[适应性免疫系统](@keyword=adaptive_immune_system|lang=zh-CN|style=Feynman)。当一种新病毒攻击时，细菌有时能捕获一小段病毒DNA，并将其作为“间隔子”储存在自己的基因组中。这个间隔子随后充当记忆，使细菌能够在未来识别并摧毁该病毒。

当然，[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)通过突变其基因组中被间隔子识别的部分来反击，使间隔子失效。这就形成了一场永无休止的军备竞赛。新的间隔子被获得；旧的间隔子变得过时。我们[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)在一个细菌种群中随时能找到多少种不同的、功能性的间隔子类型？我们可以为此建立一个极其简单的模型 [@problem_id:2842413]。假设新的、有用的间隔子由种群通过[泊松过程](@keyword=poisson_process|lang=zh-CN|style=Feynman)以速率 $\alpha$ “发明”出来。再假设每种现有的间隔子类型都因[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)进化而以恒定的[风险率](@keyword=hazard_rate|lang=zh-CN|style=Feynman) $u$ 独立地“失效”，这意味着其功能寿命是一个指数[随机变量](@keyword=random_variable|lang=zh-CN|style=Feynman)。这是一个经典的移入-死亡过程。在[稳态](@keyword=steady_state_2|lang=zh-CN|style=Feynman)下，[到达率](@keyword=arrival_rate|lang=zh-CN|style=Feynman)必须与离开率平衡。功能性间隔子类型的[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)数量，即多样性 $D^{\ast}$，结果是：

$$ D^{\ast} = \frac{\alpha}{u} $$

这个结果简单得惊人。细菌免疫武库的多样性仅仅是创新率与过时率之比。这个优雅的公式，直接源于一个简单的[随机模型](@keyword=stochastic_models|lang=zh-CN|style=Feynman)，为理解[共同进化](@keyword=co_evolution|lang=zh-CN|style=Feynman)的动态提供了一个强大的概念框架。

这种通过组件的“到达”和“离开”来描述系统的思想具有极强的通用性。我们可以将其应用于整个生态系统 [@problem_id:2794077]。想象一片森林。它不是一个静态的实体，而是不断被干扰所塑造。雷击引起的火灾，树倒在林冠上形成的空隙——这些都可以被建模为“脉冲”干扰，如果它们是独立事件，通常可以用[泊松过程](@keyword=poisson_process|lang=zh-CN|style=Feynman)很好地近似。许多这样的小事件累积的损害可以用[复合泊松过程](@keyword=compound_poisson_process|lang=zh-CN|style=Feynman)来建模。其他干扰是“按压”式的，比如持续的干旱。这些事件的发生可能不是完全随机的；也许它们与准周期的气候循环有关。在这种情况下，我们可以使用更一般的[更新过程](@keyword=renewal_processes|lang=zh-CN|style=Feynman)，其中事件之间的时间从像[爱尔朗分布](@keyword=erlang_distribution|lang=zh-CN|style=Feynman)这样的分布中抽取，这种分布比纯粹无记忆的指数分布更有规律。现代生态学家的工具箱里装满了这些[随机过程](@keyword=random_process|lang=zh-CN|style=Feynman)，使得对塑造我们生命世界的看似混乱的破坏与更新之舞进行精确、定量的描述成为可能。

### 细胞的[抖动](@keyword=dither|lang=zh-CN|style=Feynman)机器

让我们再次放大，深入到单个活细胞内部。几十年来，生物学被描绘成带有清晰箭头和方框的图表，暗示着一个整洁、确定性的工厂。我们现在知道，现实要混乱得多，有趣得多，而且根本上是随机的。这一切的核心是基因表达。基因并不仅仅是产生稳定的蛋白质流。基因本身经常以随机的方式开启和关闭。这可以被建模为一个“电报过程”，其中基因的状态以一定的时间单位概率在开启（ON）和关闭（OFF）之间翻转。当它处于开启状态时，信使RNA（mRNA）分子被产生，也许是作为一个[泊松过程](@keyword=poisson_process|lang=zh-CN|style=Feynman)。然后，这些mRNA中的每一个都会存活一段随机的时间才被降解。

这种机器中固有的随机性被称为*内在噪声*。但这还不是全部。细胞还生活在一个波动的环境中。信号分子或营养物 $L(t)$ 的浓度可能会上下[抖动](@keyword=dither|lang=zh-CN|style=Feynman)。我们可以将这个外部信号本身建模为一个[随机过程](@keyword=random_process|lang=zh-CN|style=Feynman)，例如，一个奥恩斯坦-乌伦贝克过程，它就像一个不断被拉向平均值的[随机游走](@keyword=random_walk|lang=zh-CN|style=Feynman) [@problem_id:2531206]。细胞对这个信号的反应——比如说，通过一个在配体 $L(t)$ 存在时开启或关闭基因的[核糖开关](@keyword=riboswitches|lang=zh-CN|style=Feynman)——因此是[内在噪声和外在噪声](@keyword=intrinsic_and_extrinsic_noise|lang=zh-CN|style=Feynman)的复杂相互作用。令人惊讶的是，我们可以使用我们的数学工具来剖析这些噪声来源，理解它们如何被细胞的调控网络过滤或放大，并预测由此产生的蛋白质水平的变异性。

这种[细胞噪声](@keyword=cellular_noise|lang=zh-CN|style=Feynman)重要吗？当然重要。它不仅仅是需要被平均掉的麻烦；它可能是生物功能的驱动力。考虑一株植物决定腋芽应该长成新枝还是保持休眠。这个决定由一个复杂的信号[网络控制](@keyword=network_control|lang=zh-CN|style=Feynman)，涉及像[独脚金内酯](@keyword=strigolactones|lang=zh-CN|style=Feynman)这样的激素。激素的局部浓度 $S$ 和芽细胞中受体分子的数量 $R$ 都会随机波动。依赖于 $S$ 和 $R$ 的信号活动 $A$ 因此也是一个[随机变量](@keyword=random_variable|lang=zh-CN|style=Feynman)。芽的“决定”可能取决于这个波动的活动 $A$ 是否碰巧超过了某个阈值。

这意味着，在一群相同的芽中，有些会生长，有些则不会，这仅仅是由于偶然性。使用[噪声传播](@keyword=noise_propagation|lang=zh-CN|style=Feynman)分析，我们甚至可以问哪个噪声源更重要 [@problem_id:2610868]。如果激素水平非常高（使受体饱和），那么激素的微[小波](@keyword=wavelets|lang=zh-CN|style=Feynman)动就不那么重要；受体数量的噪声将主导结果。如果激素水平非常低，系统对激素波动高度敏感，那个噪声源将占主导地位。从某种意义上说，植物并不是为其所有芽做出一个决定；它运行着一组并行的随机实验，其结果是一个[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)。

### 来自远古的回声

到目前为止，我们已经使用[随机过程](@keyword=random_process|lang=zh-CN|style=Feynman)来观察世界随时间向前演化。但它们最强大的应用之一来自于掉头向后看。这就是群体遗传学的领域，我们试图在现存生物的DNA中读取历史。

想象一下，你取了比如说四个个体的样本。每个个体都携带一个特定基因的拷贝。如果我们追溯它们的祖先，它们的谱系将会合并。在某个时间点，四个谱系中的两个会在一个共同的祖先处相遇。现在我们有三个独特的谱系。过了一段时间，这三个中的两个会合并。现在我们有两个。最后，这两个也会合并，我们就找到了整个四个样本的[最近共同祖先](@keyword=most_recent_common_ancestor|lang=zh-CN|style=Feynman)（MRCA）。

这就是Kingman的[溯祖模型](@keyword=coalescent_models|lang=zh-CN|style=Feynman) [@problem_id:725365] 背后的美妙思想。它是一个向后追溯时间的[随机过程](@keyword=random_process|lang=zh-CN|style=Feynman)。关键的洞见是，溯祖合并的速率取决于谱系的数量。当有 $k$ 个谱系时，有 $\binom{k}{2}$ 对可能合并，所以*下一次*溯祖事件的等待时间是一个速率为 $\binom{k}{2}$ 的指数[随机变量](@keyword=random_variable|lang=zh-CN|style=Feynman)。当谱系很多时，合并发生得更快，随着谱系数量的减少而减慢。通过将这些随机的等待时间相加，我们可以计算出[最近共同祖先](@keyword=most_recent_common_ancestor|lang=zh-CN|style=Feynman)（[TMRCA](@keyword=tmrca|lang=zh-CN|style=Feynman)）的[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)。这个理论框架是让我们能够估计“线粒体夏娃”或“Y[染色体](@keyword=chromosome|lang=zh-CN|style=Feynman)亚当”生活在多久以前的引擎，将[基因序列](@keyword=gene_sequence|lang=zh-CN|style=Feynman)变成解读我们自己遥远过去的[分子钟](@keyword=molecular_clock|lang=zh-CN|style=Feynman)。

这些模型也成为我们进行关于进化的[科学推断](@keyword=scientific_inference|lang=zh-CN|style=Feynman)的主要工具。假设我们观察一个性状，比如脑容量，在一系列相关物种中。这个性状是通过简单的[随机游走](@keyword=random_walk|lang=zh-CN|style=Feynman)，即布朗运动（BM）过程演化的，其中变化是无方向的吗？还是它不断被稳定选择拉向某个最优大小，这个过程更适合用奥恩斯坦-乌伦贝克（OU）模型来描述？通过将两种模型拟合到[系统发育树](@keyword=phylogenetic_trees|lang=zh-CN|style=Feynman)和现存物种的性状数据上，我们可以使用像[似然比检验](@keyword=likelihood_ratio_test_2|lang=zh-CN|style=Feynman)这样的统计方法，来看哪个故事为我们今天看到的世界提供了更好的解释 [@problem_id:2735163]。[随机过程](@keyword=random_process|lang=zh-CN|style=Feynman)不仅仅是用来描述世界；它们是用来检验关于世界的假设的。

从原子的闪烁到[生命之树](@keyword=tree_of_life|lang=zh-CN|style=Feynman)的分支，我们发现同样的数学思想提供了一种深刻而统一的语言。[随机过程](@keyword=random_process|lang=zh-CN|style=Feynman)并不会推翻物理定律优雅的确定性。它们完善了它，为我们提供了一个框架来理解我们所居住的这个嘈杂、[抖动](@keyword=dither|lang=zh-CN|style=Feynman)和光荣复杂的宇宙。它们向我们揭示了一种不羁但深刻的秩序。