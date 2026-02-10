## 应用与跨学科联系

如果一个系统的能量是描述其状态的书，那么能量的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)就是讲述其故事的书页。知道能量告诉你系统*是*什么，但知道能量如何变化则告诉你它能*做*什么。它会[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)吗？会弯曲吗？会反应吗？会破碎吗？答案不在于能量的[绝对值](@keyword=absolute_value|lang=zh-CN|style=Feynman)，而在于当我们探究和推动系统时，能量的斜率、曲率以及它的曲折变化。正是在这些[导数](@keyword=derivative|lang=zh-CN|style=Feynman)中，物质的真实本性得以揭示，将电子的量子世界与我们日常观察到的宏观性质联系起来。让我们踏上一段旅程，看看这个强大的思想如何跨越从[光谱学](@keyword=spectroscopy|lang=zh-CN|style=Feynman)到[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)，甚至进入现代人工智能前沿的各个学科。

### 原子交响乐：[光谱学](@keyword=spectroscopy|lang=zh-CN|style=Feynman)与分子表征

想象一个分子不是一堆静态的球棍模型，而是一个动态的实体，一个由[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)的“弹簧”连接起来的微型原子“管弦乐队”。我们如何听到这个乐队的演奏？我们倾听它的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。当一个分子吸收红外光时，是因为光的频率与分子的固有[振动频率](@keyword=vibrational_frequency|lang=zh-CN|style=Feynman)相匹配。但这些频率是由什么决定的呢？答案就在于能量的二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)。

对于任何给定的[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)，其势能形成一个类似山谷的形状。一个稳定的键就位于这个谷底。键的刚度——即拉伸或压缩它一点点所需能量的多少——由这个山谷的*曲率*决定。一个陡峭狭窄的山谷对应一个刚性强的键，其振动频率高；而一个宽阔平坦的山谷则对应一个松散的键，其[振动频率](@keyword=vibrational_frequency|lang=zh-CN|style=Feynman)低。这个曲率正是势能相对于原子位置的二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)。通过计算这个被称为**Hessian矩阵**的二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)矩阵，我们可以确定一个分子的所有固有[振动频率](@keyword=vibrational_frequency|lang=zh-CN|style=Feynman) [@problem_id:2013479]。然后，我们甚至可以在踏入实验室之前就预测出它的整个[红外光谱](@keyword=ir_spectrum|lang=zh-CN|style=Feynman)！

但二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)告诉我们的不仅仅是交响乐的音符，它还告诉我们这个“管弦乐队”是否设置正确。当我们让计算机寻找一个分子的最稳定结构时，[优化算法](@keyword=optimization_algorithms|lang=zh-CN|style=Feynman)会搜索[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)上的一个点，在该点上所有原子受力为零。这等同于寻找一个能量一阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)（梯度）为零的点。然而，一个斜率为零的点可能是谷底（稳定极小点）、山顶（极大点），或者最有趣的，一个山口（[鞍点](@keyword=saddle_point|lang=zh-CN|style=Feynman)）。我们如何区分它们？我们看曲率。一个真正稳定的分子，就像碗里的一个球，必须在所有方向上都具有正曲率。如果我们计算Hessian矩阵并发现其中一个曲率为负，这意味着我们找到了一个**过渡态**——连接两个稳定山谷的山口 [@problem_id:1370842]。这不是失败！这些[过渡态](@keyword=activated_complex|lang=zh-CN|style=Feynman)是通往[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)的大门，找到它们是理解[反应机理](@keyword=chemical_mechanism|lang=zh-CN|style=Feynman)的关键一步。

在这个分析中，一个优美的物理学现象从数学中自然浮现。对于任何孤立的分子，你总会发现五个或六个振动频率恰好为零。零频率的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)意味着什么？它意味着一种完全不消耗能量的运动。这些不是[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)，而是整个分子在空间中的刚性平移或围绕其[质心](@keyword=center_of_mass|lang=zh-CN|style=Feynman)的旋转 [@problem_id:2457232]。物理定律在任何地方、任何方向都相同的这一事实，完美地反映在二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)的数学中。

随着更高阶导数的引入，故事变得更加深刻。一些分子的[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)虽然真实存在，但在[红外光谱](@keyword=ir_spectrum|lang=zh-CN|style=Feynman)中却是“不可见”的。我们通常可以用另一种称为拉曼光谱的技术来检测它们。如果一个分子的电子“可挤压性”——即其极化率——在[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)过程中发生变化，那么这个[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)就是[拉曼活性](@keyword=raman_activity|lang=zh-CN|style=Feynman)的。这个[极化率](@keyword=polarizability|lang=zh-CN|style=Feynman)本身就是一个二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)：能量相对于外加电场的二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)。因此，[拉曼强度](@keyword=raman_intensity|lang=zh-CN|style=Feynman)取决于当原子移动时这个二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)的*变化*，这与能量的**三阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)**有关 [@problem_id:2894873]。每一阶更高的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)都会揭开新的一层，展现出分子特性中更微妙的方面。

### 从分子到材料：物质的性质

支配单个分子的相同原理也决定了块状材料的行为。让我们从少数几个原子扩大到晶体中数以万亿计的原子。是什么决定了一块钢的刚度或一种聚合物的柔韧性？

我们再次求助于能量的二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)。对于晶体，我们可以问当施加一个小的形变或**应变**时，其总能量如何变化。能量对应变的一阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)给出了材料的[内应力](@keyword=internal_stress|lang=zh-CN|style=Feynman)。二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)则告诉我们对于给定的应变，应力变化了多少。这个量正是材料的**[弹性常数](@keyword=elastic_constants|lang=zh-CN|style=Feynman)**，或其刚度 [@problem_id:2814473]。那个给出[单键](@keyword=single_bond|lang=zh-CN|style=Feynman)[振动频率](@keyword=vibrational_frequency|lang=zh-CN|style=Feynman)的数学工具，现在又给出了固体材料的宏观刚度。这提供了一座从电子和原子核的量子力学相互作用到日常物品工程性质的直接、定量的桥梁。

我们还可以通过其他方式探测材料的电子响应。想象一下将一个[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)靠近一种材料。材料中的电子将如何重新[排列](@keyword=permutation|lang=zh-CN|style=Feynman)以作响应？答案被编码在**[化学硬度](@keyword=chemical_hardness|lang=zh-CN|style=Feynman)**的概念中。通过考虑当我们在构成体系的原子上增加或移除[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)时体系能量的变化，我们可以定义一个“硬度矩阵”。这个矩阵——你猜对了——就是能量相对于原子[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)的二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)矩阵 [@problem_id:180748]。具有“软”硬度矩阵的材料很容易被极化；其电子可以轻易地移动。这一性质对于理解从[电荷转移](@keyword=charge_transfer|lang=zh-CN|style=Feynman)是关键的催化作用，到[电容器](@keyword=capacitor|lang=zh-CN|style=Feynman)和其他电子元件的设计等一切都至关重要。

### 教机器学物理：新前沿

近年来，这个故事又谱写了新的篇章，将这些经典概念与人工智能的前沿技术联系起来。使用量子力学计算一个系统的能量通常计算成本高昂。如果我们能训练一个机器学习模型或神经网络，让它充当一个可以即时预测能量的“代理”呢？

这就是[机器学习原子间势](@keyword=machine_learning_interatomic_potentials|lang=zh-CN|style=Feynman)函数的目标。要构建一个精确的模型，人们可能认为仅仅用一个包含大量分子结构及其对应能量的数据库来训练就足够了。然而，我们可以做得更好。能量值只是一个复杂高维[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上的点。要学习这个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的真实*形状*，向模型提供关于其[导数](@keyword=derivative|lang=zh-CN|style=Feynman)的信息会有效得多。

通过不仅对参考能量进行训练，还对参考力——即能量的负一阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)——进行训练，我们提供了远为丰富的信息。告知模型每个点的斜率，比起只告知其高度，能更严格地约束[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的可能形状 [@problem_id:2784646]。这种“力匹配”方法彻底改变了该领域，使得我们能够创造出精度接近量子力学但[计算成本](@keyword=computational_cost|lang=zh-CN|style=Feynman)仅为其一小部分的势函数。

这个原理同样完美地延伸到了材料领域。如果我们的目标是创建一个能够准确预测[晶体弹性](@keyword=crystal_elasticity|lang=zh-CN|style=Feynman)性质的机器学习模型，我们需要教它关于二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)的知识。如何做？通过对一阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)进行训练！我们在训练数据中不仅包括力（能量相对于原子位置的一阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)），还包括**[应力张量](@keyword=stress_tensor|lang=zh-CN|style=Feynman)**（能量相对于应变的一阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)）[@problem_id:2908447]。通过迫使模型正确地学习这些一阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)，我们极大地提高了它复现我们真正关心的二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)——弹性常数——的能力。这种[导数](@keyword=derivative|lang=zh-CN|style=Feynman)的层次结构为教我们的机器学习物理定律提供了一个强大且有物理基础的方案。

从单个分子键的共鸣，到钢铁的刚度，再到人工智能的大脑，能量的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)是一条贯穿始终的主线。它们将静态的能量概念转化为描述所有物质行为、响应和潜能的动态脚本。在它们的斜率和曲率中，我们找到了物理世界的通用语言。