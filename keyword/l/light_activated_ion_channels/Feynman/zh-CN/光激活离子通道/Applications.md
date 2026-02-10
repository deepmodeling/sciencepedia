## 应用与跨学科联系

我们花了一些时间来理解[光激活离子通道](@keyword=light_activated_ion_channels|lang=zh-CN|style=Feynman)的非凡机制——这些从卑微藻类中借来的微小蛋白质，如何将一闪而过的光转换成细胞内的电信号。这本身就是一项优美的分子工程。但真正的魔力、真正的冒险始于我们提出一个简单的问题：既然我们有了这个完美的、微小的开关，我们可以把它放在哪里，可以打开什么？事实证明，答案几乎是我们能想象的任何地方。这个工具的应用为理解大脑乃至生命的基本过程打开了大门，揭示了贯穿生物学的美妙统一性。

### 新[神经解剖学](@keyword=neuroanatomy|lang=zh-CN|style=Feynman)：从相关性到因果性

一个多世纪以来，神经科学家一直在绘制大脑地图，识别区域并追踪它们之间庞大而错综复杂的连接网络。但这些地图是静态的。我们可以看到一条线路从A点连接到B点，但我们无法轻易知道它传递了什么信息，或者如果你单独沿着那条线路发送一个信号会发生什么。我们就像一个看着一台巨大未知机器接线图的人，图中充满了相关性，却缺少因果关系。[光遗传学](@keyword=optogenetics|lang=zh-CN|style=Feynman)改变了一切。

首先，考虑一个最基本的问题：我们如何知道[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)A是否真的在与[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)B“对话”？我们现在可以在[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)A中安装光激活通道，并在[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)B中安装一个在有钙离子（一种活动迹象）时会发光的荧光报告分子。然后，我们进行一个最简单、最优雅的实验：我们用光照射[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)A，观察[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)B是否亮起。如果亮了，我们不仅证实了一个功能性连接，我们还亲眼目睹了一个突触的活动，一个“词语”从一个细胞传递到另一个细胞 [@problem_id:2336428]。这相当于现代版的在电线一端敲击，在另一端听是否有声音。

但这仅仅是个开始。真正的力量来自于对行为做出因果论断。假设一位神经科学家观察到，每当动物执行一项特定任务时，某一组[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)就会活跃起来。这种神经活动是*导致*了该行为，还是仅仅是其结果？为了回答这个问题，我们必须成为实验者，而不仅仅是观察者。这需要两样东西：一种方法能将我们的[光开关](@keyword=optical_switch|lang=zh-CN|style=Feynman)靶向到*只*我们感兴趣的[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)上，以及一种方法能设计一个无懈可击的实验，使得结论无可辩驳。第一部分是一个遗传学奇迹，通常涉及将光激活通道（如 Channelrhodopsin-2）的基因与一个特定的[启动子](@keyword=promoter|lang=zh-CN|style=Feynman)——一个遗传“地址标签”——打包在一起，以确保它只在（比如说）多巴胺能[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)中制造 [@problem_id:2354563]。

第二部分是[对照实验](@keyword=controlled_experiment|lang=zh-CN|style=Feynman)的艺术。要声称激活这些[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)导致了某种行为，你必须证明，在经历了完全相同程序——手术、光照——但缺少功能性开关的动物身上，这种行为不会发生。这个对照组动物，可能表达的是一种无害的[荧光蛋白](@keyword=fluorescent_proteins|lang=zh-CN|style=Feynman)而不是[通道蛋白](@keyword=channel_proteins|lang=zh-CN|style=Feynman)，它是每个伟大光遗传学实验中默默无闻的英雄。实验动物与其[对照组](@keyword=control_group|lang=zh-CN|style=Feynman)“双胞胎”之间的任何差异都只能归因于一件事：那些特定[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)的放电 [@problem_id:2354440]。

有了这种建立因果关系的能力，我们可以提出具有惊人特异性的问题。例如，大脑的奖赏系统涉及一个名为[腹侧被盖区](@keyword=ventral_tegmental_area|lang=zh-CN|style=Feynman) (VTA) 的区域中的多巴胺[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)，它们向许多其他地方发送投射或“线路”，包括[伏隔核](@keyword=nucleus_accumbens|lang=zh-CN|style=Feynman) (NAc)。奖赏的感觉是由 VTA [神经元](@keyword=neurons|lang=zh-CN|style=Feynman)普遍产生的，还是由它们沿着 VTA-到-NAc 这条线路发送的信号特异性产生的？利用巧妙的病毒策略，只在那些既位于 VTA *又*向 NAc 发送线路的[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)中安装[光开关](@keyword=optical_switch|lang=zh-CN|style=Feynman)，我们现在可以选择只激活那一条通路。实验表明，激活这个特定的投射足以使动物为其工作，证明这条通路是强化的有效驱动力。然后，通过证明如果稍微移动光束或在 NAc 局部阻断[多巴胺受体](@keyword=dopamine_receptors|lang=zh-CN|style=Feynman)，效果就会消失，我们就能确信，我们正在触动大脑巨大复杂性中的一个特定的、有意义的环路 [@problem_id:2605719]。

### 解析心智与身体

凭借这种前所未有的精确性，我们可以开始解决一些关于心智及其与身体联系的最深层问题。

什么是记忆？我们长期以来认为它储存在一组特定的[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)中，即一个“印迹 (engram)”。这是一个美好的想法，但如何证明呢？有了光遗传学，这成为可能。研究人员可以利用遗传学技巧标记小鼠海马体中在一次恐惧诱导事件中活跃的[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)，只在这个“恐惧印迹”中安装光激活通道。第二天，小鼠处在一个安全、中性的地方。如果科学家将光照射到[海马体](@keyword=hippocampus|lang=zh-CN|style=Feynman)，只激活恐惧[印迹](@keyword=engram|lang=zh-CN|style=Feynman)的那些细胞，小鼠就会恐惧地僵住。在非常真实的意义上，它正在回忆那段记忆，因为实验者用一个开关打开了它。这将记忆这个抽象概念转化为了某种有形的、物理的东西：一组特定的、现在可控的细胞 [@problem_id:1722126]。

这种控制水平超越了认知，延伸到大脑对身体本身的调节。例如，你的基础血压是由你脑干中的一组[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)（延髓头端腹外侧区，RVLM）持续的、低水平的活动来维持的。这些[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)指令你的血管保持部分收缩。如果你沉默掉这种低水平活动会发生什么？通过在这些[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)中表达一种光激活的*抑制性*通道，科学家们做到了这一点。光一亮，[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)就被沉默了。结果是即时而戏剧性的：[血压](@keyword=blood_pressure|lang=zh-CN|style=Feynman)、[心率](@keyword=heart_rate|lang=zh-CN|style=Feynman)和外周阻力急剧下降。这个实验惊人地展示了[中枢神经系统](@keyword=central_nervous_system|lang=zh-CN|style=Feynman)对我们最重要生理功能所施加的直接、即时的控制 [@problem_id:1694001]。

甚至我们日常生活的节律也受到这种光控的影响。我们大脑中的主时钟，即[视交叉上核 (SCN)](@keyword=suprachiasmatic_nucleus_(scn)|lang=zh-CN|style=Feynman)，协调着我们24小时的[昼夜节律](@keyword=circadian_rhythms|lang=zh-CN|style=Feynman)周期。科学家们早就假设，这个微小结构的不同部分可能分别负责提前我们的时钟（比如我们向东飞时）或延迟它（向西飞时）。通过将一根精细的[光纤](@keyword=optical_fiber|lang=zh-CN|style=Feynman)对准生活在持续黑暗中的动物的 SCN 的不同亚区，研究人员可以向仅仅几百个细胞传递一个“人造日光脉冲”，并观察动物整个日常节律的相应变化。这使他们能够以极其精细的细节绘制出我们内部时钟的功能地理图 [@problem_id:1444812]。

### 超越大脑：一种通用的生命工具

也许光激活通道最深远的影响是它们从神经科学迁移到几乎所有其他生物学领域。电和离子流的原理并非[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)独有；它们对所有活细胞都至关重要。

思考一下发育的奇迹，一个[受精](@keyword=fertilization|lang=zh-CN|style=Feynman)卵如何转变成一个复杂的有机体。这个过程涉及细胞移动、改变形状以及组织成组织和器官的惊人编排。许多这些运动是由物理力驱动的。例如，上皮片层折叠成管状结构——形成脊髓或肠道的关键步骤——是由细胞“顶端”或顶部侧的收缩驱动的。利用[光遗传学](@keyword=optogenetics|lang=zh-CN|style=Feynman)，我们可以直接测试这一点。通过在发育中的胚胎的一片细胞中表达光激活通道，科学家可以指令这些细胞在光照下收缩其顶端表面。仿佛变魔术一般，平坦的组织[片层](@keyword=lamellae|lang=zh-CN|style=Feynman)可以按指令弯曲和内陷，证明这种局部的机械力足以塑造一个发育中的组织 [@problem_id:1697033]。

细胞不仅改变形状；它们还会迁移。在原肠胚形成期间，细胞在胚胎中穿行以找到自己应有的位置。一个引人入胜的假说是，它们是由[生物电](@keyword=bioelectricity|lang=zh-CN|style=Feynman)梯度构成的无形“轨道”引导的。人们怎么可能检验这样的想法呢？光遗传学再次提供了关键。通过在迁移细胞爬行其上的基底细胞中表达光激活通道，研究人员可以用光来“绘制”或“擦除”这些[生物电](@keyword=bioelectricity|lang=zh-CN|style=Feynman)轨道。他们可以创造一个人工的电“山丘”，看看迁移的细胞是否会停滞不前，无法攀登。这使得对指导[身体蓝图](@keyword=body_plan|lang=zh-CN|style=Feynman)构建的物理线索进行直接、功能性的测试成为可能 [@problem_id:1689234]。

最后，我们可以将视角完全[拉回](@keyword=pullback|lang=zh-CN|style=Feynman)到单个非兴奋性细胞的内部运作上。你身体里的任何细胞，无论是皮肤细胞还是肝细胞，其膜上都维持着一个电压。使用光激活通道，我们可以随意改变那个电压。这使我们能够用光作为触发一整串内部事件的扳机。例如，我们可以引起一次轻微的[去极化](@keyword=depolarization|lang=zh-CN|style=Feynman)，刚好足以打开膜上的其他电压敏感通道，如钙通道。由此产生的钙离子流入可以继而触发一系列下游过程。这将我们的[光开关](@keyword=optical_switch|lang=zh-CN|style=Feynman)变成了复杂[链式反应](@keyword=self_sustaining_reaction|lang=zh-CN|style=Feynman)中的第一块多米诺骨牌，为我们提供了一个强大的工具来剖析支配每个细胞生命的复杂信号通路 [@problem_id:1456043]。

从突触的连接到胚胎的塑造，从记忆的所在到心跳的调节，[光激活离子通道](@keyword=light_activated_ion_channels|lang=zh-CN|style=Feynman)被证明是一把功能极其多样的钥匙。它赋予我们力量，从观察走向干预，去检验那些曾经看似无法检验的假说，并揭示电、力学和我们称之为生命的现象之间深刻而往往令人惊讶的联系。从[藻类](@keyword=algae|lang=zh-CN|style=Feynman)中的一个光敏蛋白到一个能重新激活记忆的工具，这段旅程证明了生物学原理的基本统一性，以及当我们学会用新的眼光看待世界时涌现出的无限可能性。