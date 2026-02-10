## 应用与跨学科联系

想象一下试图理解一个时钟是如何工作的。过去的方法是用锤子把它砸碎，然后检查散落在地上的齿轮和弹簧。你可能会知道它由哪些零件组成，但你永远看不到它们是如何协同运转的。几十年来，我们就是这样研究细胞的。为了看到里面的分子，我们必须固定它们、冷冻它们、撕裂它们——简而言之，我们必须杀死我们想要理解的生命本身。我们研究的是一个动态过程的化石。

[生物正交化学](@keyword=bioorthogonal_chemistry|lang=zh-CN|style=Feynman)改变了游戏规则。在学习了它的原理——即其无干扰反应的“语法”之后——我们现在可以谱写科学的诗篇。我们可以在活细胞内放置微小、无声的化学报告基团，并按需激活它们。这是一种分子间谍活动，让我们能够在不中断表演的情况下，在其自然舞台上观看生命错综复杂的舞蹈。让我们来探索一下，利用这种新获得的力量，我们现在可以提出并回答哪些非凡的问题。

### 化无形为有形：分子间谍的艺术

在细胞令[人眼](@keyword=human_eye|lang=zh-CN|style=Feynman)花缭乱的分[子群](@keyword=subgroup|lang=zh-CN|style=Feynman)中，你如何追踪一种特定类型的分子？[生物正交化学](@keyword=bioorthogonal_chemistry|lang=zh-CN|style=Feynman)的第一个也是最直接的应用就是简单地让事物变得可见。考虑一个正在构建细胞壁的细菌。过去，为了看到这堵墙，我们可能会使用标记有荧光染料的[抗体](@keyword=antibodies|lang=zh-CN|style=Feynman)。但这需要杀死细胞并在其上打孔，以便让笨重的[抗体](@keyword=antibodies|lang=zh-CN|style=Feynman)进入。我们得到的是一张静态快照，一张成品墙壁的照片。

借助[生物正交化学](@keyword=bioorthogonal_chemistry|lang=zh-CN|style=Feynman)，我们可以做到远比这优雅得多的事情。我们可以给活的细菌喂食一种稍微修饰过的构建模块——比如，一个携带微小、惰性叠氮基“手柄”的糖分子。细菌没有注意到这种细微的变化，愉快地在其生长过程中将这个“间谍”分子整合到新的细胞壁中。在任何我们选择的时刻，我们可以加入第二个分子，一个携带互补炔基手柄的[荧光团](@keyword=fluorophore|lang=zh-CN|style=Feynman)。*咔哒！*生物正交反应只点亮了我们在提供间谍分子期间构建的那部分细胞壁。我们不再是看化石，而是在一个活生生的、会呼吸的生物体中实时观察施工现场 ([@problem_id:2067057])。

这种“[代谢标记](@keyword=metabolic_labeling|lang=zh-CN|style=Feynman)”的原理非常强大。我们可以为不同的生物合成途径设计间谍分子。例如，通过给细胞喂食一种修饰过的甘露糖胺糖 ($\mathrm{Ac_4ManNAz}$)，我们可以特异性地追踪一类称为[唾液酸](@keyword=sialic_acid|lang=zh-CN|style=Feynman)化糖蛋白的复杂糖链的合成。这些分子覆盖在我们细胞的表面，对通讯和免疫至关重要。通过细胞自身的代谢机器引入叠氮基手柄，然后点击连接上一个标签，研究人员可以绘制出整个“糖[蛋白质组](@keyword=proteome|lang=zh-CN|style=Feynman)”，识别出哪些蛋白质被这些特定的糖修饰，甚至可以利用复杂的遗传控制手段精确定位负责此过程的酶 ([@problem_id:2959570])。

但如果我们只想在成千上万种蛋白质中标记某一种特定的蛋白质呢？这时，我们需要一种更具排他性的策略。想象一下设计一个“秘密握手”。科学家们可以取一种蛋白质修饰酶，比如激酶，并巧妙地改变其[活性位点](@keyword=active_site|lang=zh-CN|style=Feynman)，创造出一个小“洞”。然后，他们合成一种该酶的底物（如ATP）的变体，该变体带有一个携带生物正交手柄的笨重“凸起”。这个“带凸起的”底物会被细胞中所有正常的酶忽略，但它能完美地[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)我们修饰过的酶的工程化“洞”中。这种工程酶于是成为唯一能够传递生物正交手柄的媒介，并且它只将手柄传递给其天然的蛋白质靶点。其结果是在活细胞内对一种（或一族）蛋白质进行极其特异性的标记，这是若非如此便无法实现的[分子识别](@keyword=molecular_recognition|lang=zh-CN|style=Feynman)壮举 ([@problem_id:2124941])。

### 捕捉活性的快照：谁在做什么，以及何时做？

看到一个分子*在*哪里是一回事；知道它在*做*什么则是另一回事。细胞中的许多蛋白质，特别是酶，就像工厂里的工人——有些在忙碌，有些在休息，还有些已经永久退休。简单的蛋白质普查无法区分它们。[生物正交化学](@keyword=bioorthogonal_chemistry|lang=zh-CN|style=Feynman)使我们能够调查*活跃*的劳动力。

这就是基于活性的蛋白[质谱分析](@keyword=mass_spectrometry|lang=zh-CN|style=Feynman) (ABPP) 的世界。在ABPP中，我们设计一种化学探针，它不仅能与酶结合，而且被设计成*只有*当酶处于其活性的、[功能性状](@keyword=functional_traits|lang=zh-CN|style=Feynman)态时才与它发生共价反应。这些探针装备有生物正交手柄。通过将探针加入到细胞裂解液中，我们可以“标记”所有特定类别的活性酶。然后，利用点击反应，我们可以连接一个报告基团，看看谁当时“在岗”。这对药物发现具有革命性意义。我们可以用一种潜在的药物处理细胞，然后使用ABPP来观察哪些酶被抑制了——也就是说，哪些工人被药物强制安排了计划外的休息 ([@problem_id:2333515])。这项技术非常精确，可以用来发现抗生素的工作原理，方法是识别它们在细菌内的确切靶点，例如关键的细胞壁构建酶MurA和[青霉素结合蛋白](@keyword=penicillin_binding_proteins|lang=zh-CN|style=Feynman) (PBPs) ([@problem_id:2505016])。

我们可以将“活性”这一概念进一步拓展，从催化作用延伸到仅仅是邻近关系。我们感兴趣的蛋白质在和谁交谈？它的邻居是谁？邻近标记技术，如APEX2，将我们的蛋白质变成一个临时的灯塔。该蛋白质与一种酶 (APEX2) 融合，当给予特定探针（如炔基苯酚）和一小股过氧化氢时，它会释放出一团高活性、短寿命的[自由基](@keyword=free_radical|lang=zh-CN|style=Feynman)。这些[自由基](@keyword=free_radical|lang=zh-CN|style=Feynman)会用炔基手柄标记任何附近的蛋白质。关键在于，反应在空间（纳米级的半径）和时间（亚分钟级的脉冲[持续时间](@keyword=holding_times|lang=zh-CN|style=Feynman)）上都受到限制。

现在，想象一下你可以做的真正精彩的实验。一个蛋白质在受到刺激后从细胞质移动到线粒体。谁*与*它一起移动（真正的伙伴），而谁只是本来就在目的地（旁观者）？利用两种正交探针（例如，炔基苯酚和叠氮基苯酚）和两次不同的脉冲——一次在移动前，一次在移动后——我们就可以解开这个谜题。在第一次脉冲中被标记的蛋白质获得一个“轻”同位素标签，而在第二次脉冲中被标记的蛋白质获得一个“重”标签。一个真正的伙伴会在两次脉冲中都被标记，并在我们的[质谱仪](@keyword=mass_spectrometer|lang=zh-CN|style=Feynman)中显示为轻/重对。而一个旁观者只会在第二次脉冲中被标记，并仅显示为重峰。这是一种令人叹为观止的巧妙方法，利用时间、空间和[正交化](@keyword=orthogonalization|lang=zh-CN|style=Feynman)学来绘制细胞内动态的社交网络 ([@problem_id:2938468])。

### 记录[蛋白质组](@keyword=proteome|lang=zh-CN|style=Feynman)的生命周期：诞生、存活与更替

也许细胞中最具活力的过程就是新蛋白质的不断合成。我们如何才能区分一分钟前诞生的蛋白质和已经存在了数天的蛋白质？这就是生物正交[非经典氨基酸](@keyword=noncanonical_amino_acids|lang=zh-CN|style=Feynman)标记 (BONCAT) 的用武之地。通过在含有带生物正交手柄的甲硫氨酸类似物（如叠氮高丙氨酸AHA或高炔丙基[甘氨酸](@keyword=glycine|lang=zh-CN|style=Feynman)HPG）的培养基中培养细胞，这段时间内合成的每一个蛋白质都会被打上“制造于[日期]”的印章。在标记期结束后，我们可以使用[点击化学](@keyword=click_chemistry|lang=zh-CN|style=Feynman)连接荧光染料（一种称为FUNCAT的技术）来可视化新蛋白质在何时何地被制造，或者连接生物素标签 (BONCAT) 来钓出整个新合成的[蛋白质组](@keyword=proteome|lang=zh-CN|style=Feynman)进行鉴定 ([@problem_id:2743361])。

当我们将多种正交工具结合起来，在单个样本内进行时间分辨研究时，这种方法的真正威力就显现出来了。考虑一个我们进行刺激的[神经元](@keyword=neurons|lang=zh-CN|style=Feynman)。我们想精确地知道它的蛋白质生产是如何*响应*于该刺激而变化的。我们可以进行一个脉冲-追踪-脉冲实验。首先，用一种类似物（例如，含叠氮基的AHA）进行“刺激前”脉冲。然后，用正常的甲硫氨酸进行“追踪”，以洗掉类似物并停止标记。在追踪期间，我们施加刺激。最后，用第二种正交的类似物（例如，含炔基的HPG）进行“刺激后”脉冲。

裂解细胞后，我们进行两次独立的正交点击反应。我们将一个“轻”同位素报告基团连接到叠氮基标记的蛋白质（刺激前），并将一个“重”报告基团连接到炔基标记的蛋白质（刺激后）。在单次[质谱分析](@keyword=mass_spectrometry|lang=zh-CN|style=Feynman)中，我们现在可以对每一个蛋白质，比较其在刺激前后的合成速率。这个多重实验，是[代谢标记](@keyword=metabolic_labeling|lang=zh-CN|style=Feynman)、正交反应和同位素定量的交响乐，提供了一个极其丰富的数据集，以单蛋白质分辨率揭示了细胞对其环境的动态响应 ([@problem_id:2743365])。

### 从分子层面构建物质

[生物正交化学](@keyword=bioorthogonal_chemistry|lang=zh-CN|style=Feynman)不仅是一种观察工具，它也是一种创造性工具。它允许我们以分子精度构建[新形式](@keyword=newforms|lang=zh-CN|style=Feynman)的功能性物质。通过[扩展遗传密码](@keyword=expanding_the_genetic_code|lang=zh-CN|style=Feynman)，我们可以编程细胞，在蛋白质的任何[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)位点插入一个带有独特化学手柄的[非天然氨基酸](@keyword=non_canonical_amino_acids|lang=zh-CN|style=Feynman)——比如在对乙酰苯丙氨酸中的酮基。这为我们提供了一个单一、定义明确的化学修饰点。

这对医学具有深远的影响。许多[治疗性蛋白质](@keyword=therapeutic_proteins|lang=zh-CN|style=Feynman)从体内清除得太快。延长其寿命的一个常用策略是连接一种名为聚乙二醇 (PEG) 的聚合物。过去，这是通过杂乱的化学方法完成的，PEG会附着在蛋白质的各处，常常损害其功能。现在，利用生物正交安装的酮基手柄，我们可以在一个经过理[性选择](@keyword=sexual_selection|lang=zh-CN|style=Feynman)、不会干扰蛋白质活性的位点上连接单个PEG链，进行一种“分子手术”以增强其治疗特性 ([@problem_id:2591104])。

这一愿景超越了单个分子，延伸到整个材料。构成我们结缔组织的[胶原蛋白](@keyword=collagen|lang=zh-CN|style=Feynman)，会组装成美丽、有序的原纤维。我们能否在胶原支架上添加新的生物信号，例如，为了更好地引导[组织再生](@keyword=tissue_regeneration|lang=zh-CN|style=Feynman)，而不破坏其基本的结构？粗略的化学方法就像在杰作上泼油漆——它们会破坏维持原纤维结合的精细静电模式。但是，通过温和的、位点特异性的酶促或生物正交反应，我们可以在原纤维表面装饰上生物活性肽。我们可以在尊重材料固有结构的同时添加新功能，与自然合作，为再生医学构建更智能的[生物材料](@keyword=biomaterials|lang=zh-CN|style=Feynman) ([@problem_id:2564102])。

从观察单个细菌的生长到工程化[治疗性蛋白质](@keyword=therapeutic_proteins|lang=zh-CN|style=Feynman)和先进[生物材料](@keyword=biomaterials|lang=zh-CN|style=Feynman)，[生物正交化学](@keyword=bioorthogonal_chemistry|lang=zh-CN|style=Feynman)的应用与我们的科学想象力一样广阔。它代表了从研究生物学的死亡遗物到参与生命本身动态化学的根本性转变。