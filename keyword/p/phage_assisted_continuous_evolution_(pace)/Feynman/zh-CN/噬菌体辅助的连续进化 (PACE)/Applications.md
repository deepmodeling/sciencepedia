## 应用与跨学科联系

既然我们已经探索了[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)辅助的连续进化这一精巧的发条装置——这个由捕食者与猎物、突变与生存构成的独立世界——你可能会好奇：“这台奇妙的机器究竟是用来做什么的？”这是一个合理的问题。一个美好的想法是一回事，但它真正的力量体现在它能让我们做什么。对于PACE而言，答案是：几乎任何我们能想象到的事，只要我们足够聪明，能够将我们*想要的*与[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)*需要的*联系起来。我们即将踏上一段穿越现代生物学广阔领域的旅程，从医学到[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)，看看这个单一而强大的定向进化原则是如何重塑我们工程化生命本身的能力。

### [蛋白质工程](@keyword=protein_engineering|lang=zh-CN|style=Feynman)师的梦想：雕琢分子

从本质上说，生物学是一个用蛋白质讲述的故事。这些分子是细胞的工作者、信使和支架。几十年来，科学家们一直梦想着能随心所欲地雕琢它们，为新的目的量身定制。PACE将这个梦想变成了触手可及的现实。

想象一下，你想要为一个遗传回路创造一个新的开关。你需要一个蛋白质，一个[转录因子](@keyword=transcription_factor|lang=zh-CN|style=Feynman)，它能识别一段它从未见过的特定DNA序列。你会如何创造它呢？利用PACE，我们可以设置一个简单而优美的挑战。我们把正在进化的[转录因子](@keyword=transcription_factor|lang=zh-CN|style=Feynman)的基因放在[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)上。在宿主细菌中，我们将[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)必需的生存基因`gIII`置于一把锁后——这把锁就是我们希望蛋白质识别的新DNA序列。[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)获得其`gIII`蛋白并复制自身的唯一途径，是它正在进化的蛋白质“学会”结合到那个新的DNA序列上，从而转动锁中的钥匙 [@problem_id:2054610]。潟湖变成了一个无情的训练场，在数天之内，一个能读取新遗传密码的蛋白质便从亿万个失败品中脱颖而出。

但我们可以提出更高的要求。结合是一回事；催化——主动地*做*某事——是另一回事。假设我们需要一种酶，比如[DNA连接酶](@keyword=dna_ligase|lang=zh-CN|style=Feynman)，它不能在细菌舒适的温度下工作，而要能在PCR仪的酷热中发挥功能。我们可以在那个高温下设置我们的潟湖，并设计一个`gIII`基因被破坏的筛选体系。修复它的唯一方法是让[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)正在进化的连接酶将其重新拼接起来。在这片炼狱中，只有携带了偶然发现更稳定、耐热结构的连接酶变体的罕见[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)才能完成这项修复。所有其他的都会灭亡。选择是绝对的，其结果就是一种为极端条件量身定制的酶 [@problem_id:2054587]。

这种根据功能进行筛选的能力带来了令人难以置信的精确性。通常，我们不仅希望一个蛋白质做一些新的事情；我们还希望它*停止*做一些旧的事情。一种酶可能很“滥交”，作用于错误的靶标。在这里，PACE允许一种极其巧妙的双向筛选策略。在一个系统中，我们可以为作用于新靶标设置奖励（例如，产生`gIII`），同时为作用于旧靶标设置惩罚（例如，产生一种致命毒素）。[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)的净复制速率 $r$ 变成一个简单的收益与成本方程：$r = (\text{对新的奖励}) - (\text{对旧的惩罚}) - (\text{冲刷速率})$。只有那些成为真正专家的变体——获得新活性的同时摆脱旧活性——才能茁壮成长 [@problem_id:2054562]。我们不再只是在草堆里找一根针；我们是特地要求一根不是别针的针。

### 搭建桥梁：为医学及其他领域组建复杂系统

生命很少是关于单个分子孤立行动的。它是关于网络、伙伴关系和复杂相互作用的。PACE不仅限于雕琢单个蛋白质；它还可以用来工程化连接它们的桥梁。

思考一下为一种新药疗法改进[抗体](@keyword=antibodies|lang=zh-CN|style=Feynman)的挑战。[抗体](@keyword=antibodies|lang=zh-CN|style=Feynman)通过结合发挥作用，更强的结合通常意味着更有效的药物。我们可以通过将其结合事件与[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)生存关联起来，来工程化[抗体](@keyword=antibodies|lang=zh-CN|style=Feynman)片段。一种特别巧妙的方法使用了“蛋白质分割”技巧。我们可以将必需的pIII蛋白分解成两个无功能的半体。一半附着在目标抗原上，另一半在概念上由正在进化的[抗体](@keyword=antibodies|lang=zh-CN|style=Feynman)片段引入。只有当[抗体](@keyword=antibodies|lang=zh-CN|style=Feynman)片段与其靶标强力结合时，pIII的两个半体才能被足够长时间地保持在一起，重新组装成一个功能完整的整体，从而让[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)得以繁殖。通过这种方式，“[结合亲和力](@keyword=binding_affinity|lang=zh-CN|style=Feynman)”这个抽象概念被转化为了生存这一具体通货 [@problem_id:2054589] [@problem_id:2054585]。我们是在直接筛选分子间更紧密的握手。

同样的原则可以应用于我们这个时代最紧迫的挑战之一：抗生素耐药性。细菌在不断进化以逃避我们的药物。但它们也有[天敌](@keyword=natural_enemies|lang=zh-CN|style=Feynman)——[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)。如果我们能进化[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)以跟上细菌的步伐呢？在对PACE主题的精彩扭转中，选择压力可以来自系统的物理参数。[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)感染细菌的能力取决于其尾丝与细菌表面受体的结合。更强的结合意味着更快的感染周期和更高的复制速率 $k_{\text{rep}}$。在[恒化器](@keyword=chemostat|lang=zh-CN|style=Feynman)中，我们可以简单地增加培养物被冲刷掉的稀释速率 $D$。为了让[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)生存，其复制速率必须大于稀释速率 ($k_{\text{rep}} > D$)。通过缓慢加大流速，我们施加了无情的压力，迫使[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)进化出对其细菌靶标（甚至是耐药菌株上新出现的靶标）具有越来越高亲和力的尾丝 [@problem_id:2034423]。在这里，我们没有使用工程化的[遗传回路](@keyword=genetic_circuits|lang=zh-CN|style=Feynman)，而是利用了捕食者-猎物关系本身的原始[生物物理学](@keyword=biological_physics|lang=zh-CN|style=Feynman)。

### 重新定义生命工具箱：新化学与新物理

也许PACE最深刻的应用是那些挑战我们所认为的“生物学”边界的应用。

我们所知的生命是由一套标准的20种氨基酸构成的。但如果我们能加入具有全新化学性质的新氨基酸呢？这将使我们能够构建自然界从未发明过的功能性蛋白质。关键在于工程化一种酶——[氨酰-tRNA合成酶](@keyword=aminoacyl_trna_synthetases|lang=zh-CN|style=Feynman)——它能特异性识别一种[非标准氨基酸](@keyword=non_canonical_amino_acids|lang=zh-CN|style=Feynman) (nsAA) 并将其连接到tRNA上，从而将其插入到生长中的蛋白质中。挑战在于特异性；你希望合成酶使用nsAA，但*绝不*使用外观相似的天然氨基酸。这是PACE双向筛选能力的完美任务。通过使`gIII`的产生依赖于nsAA的掺入来启用正向筛选。同时，通过让天然氨基酸的掺入导致致命毒素的产生来实现负向筛选 [@problem_id:2043429]。幸存者是那些编码超特异性合成酶的[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)，它们为我们打开遗传密码新篇章提供了一把钥匙。

这种定制酶的能力可以对准我们自己紧迫的环境问题。想象一下，进化一种酶来分解一种污染物，比如一种目前不可生物降解的新型塑料。我们可以设计一个PACE系统，其中酶在塑料上的活性会释放一个小分子。这个小分子反过来又作为诱导剂，开启`gIII`基因。[噬菌体](@keyword=bacteriophages|lang=zh-CN|style=Feynman)的酶变体降解的塑料越多，产生的诱导剂就越多，该[噬菌体复制](@keyword=bacteriophage_replication|lang=zh-CN|style=Feynman)得就越快 [@problem_id:2054624]。实际上，我们是在告诉进化过程：“解决这个污染问题的方案就是你生存的关键。找到它。”

这段旅程并不止于新化学，它延伸到了新遗传学。地球上所有的生命都使用DNA和RNA。但生命能否基于其他遗传聚合物？科学家们已经合成了具有不同糖骨架的“[异种核酸](@keyword=xenonucleic_acid|lang=zh-CN|style=Feynman)” (XNAs)。要使这些成为生命系统的一部分，我们需要能够读写它们的聚合酶。利用PACE，我们可以进化一种聚合酶，例如，读取由苏糖核酸 (TNA) 构成的模板，并将其[转录](@keyword=rna_transcription|lang=zh-CN|style=Feynman)成DNA序列。如果该DNA序列是`gIII`的[启动子](@keyword=promoter|lang=zh-CN|style=Feynman)，那么我们就有了对能够桥接自然DNA和合成XNA世界的聚合酶诞生的直接筛选 [@problem_id:2079284]。这是朝着创造真正的[合成生命](@keyword=synthetic_life|lang=zh-CN|style=Feynman)形式和探索遗传基本约束迈出的激动人心的一步。

最后，PACE不仅让我们能够工程化单个分子的特性，还能工程化它们的集体物理行为。许多细胞过程是由自发凝聚成液滴状的[蛋白质组](@keyword=proteome|lang=zh-CN|style=Feynman)织的，这种现象称为[液-液相分离](@keyword=liquid_liquid_phase_separation|lang=zh-CN|style=Feynman)。这个过程受本质无序蛋白 (IDPs) 的[生物物理学](@keyword=biological_physics|lang=zh-CN|style=Feynman)控制。我们可以通过将一个IDP与一个分裂酶的一半融合，而另一半在细胞中自由漂浮，来进化这个IDP使其更容易发生相分离。只有当IDP凝聚形成液滴时，融合半体的局部浓度才变得足够高，以有效地找到另一半，重构酶并产生`gIII`。通过增加冲刷速率，我们筛选出在越来越具挑战性的条件下形成这些必要凝聚物的IDP变体 [@problem_id:2054577]。我们正在一个活细胞内进化一种物质的物理状态。

从雕琢单个蛋白质到调控分[子群](@keyword=subgroup|lang=zh-CN|style=Feynman)落的行为，从抗击疾病到清洁环境，甚至创造新的生命形式，PACE 的应用与我们的创造力一样广阔。它证明了一个简单理念的力量：通过在适应度与功能之间建立明确的联系，我们就能让无情、优美而又富有创造力的进化引擎为我们所用。