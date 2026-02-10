## 应用与跨学科联系

世界在许多层面上都是一个网络，这是一个深刻而美丽的事实。基因、细胞、人、材料——所有这些都可以被看作是由关系连接的节点。在这些巨大而纠结的网络中，一个基本的模式出现了：社区。在某些本质方面“相似”的事物倾向于聚集在一起，形成内部比与外部世界联系更紧密的群体。发现这些隐藏社区的艺术和科学，正是[基于图的聚类](@keyword=graph_based_clustering|lang=zh-CN|style=Feynman)的任务，这是一个具有非凡能力和多功能性的透镜。在理解了其原理之后，我们现在可以踏上一段旅程，看看这个单一的想法如何解开从生命密码到物质结构等整个科学领域的秘密。

### 生命密码：对基因、基因组和物种的[聚类](@keyword=clustering|lang=zh-CN|style=Feynman)

网络视角在任何领域的革命性影响都不及在生物学中。DNA测序技术的爆炸式发展为我们提供了成千上万种生物的“零件清单”，但清单本身并非解释。要理解生命如何运作和进化，我们必须组织这些零件。

最基本的任务是根据共同的祖先或同源性将基因分组成家族。我们可以想象我们测序的每种生物中的每个基因都是一个巨大图中的节点。如果任意两个基因显示出显著的[序列相似性](@keyword=sequence_similarity|lang=zh-CN|style=Feynman)，我们就在它们之间画一条边，例如使用像BLAST这样的工具获得相似性分数。相似性越强，边的“权重”就越大。现在，我们有了一个网络。我们如何找到这些家族呢？我们运行一个[聚类算法](@keyword=clustering_algorithms|lang=zh-CN|style=Feynman)。其中最成功的之一是马尔可夫[聚类算法](@keyword=clustering_algorithms|lang=zh-CN|style=Feynman)（MCL），它在图上模拟一个“流”过程。流自然地被困在[密集连接](@keyword=dense_connectivity|lang=zh-CN|style=Feynman)的区域内，这些区域就对应于[基因家族](@keyword=gene_families|lang=zh-CN|style=Feynman)。但大自然是狡猾的。简单的相似性是不够的。[序列相似性](@keyword=sequence_similarity|lang=zh-CN|style=Feynman)的“标尺”在不同物种之间可能会被拉伸或压缩，我们必须巧妙地对我们的分数进行归一化，以进行公平的比较。此外，我们必须区分[直系同源基因](@keyword=orthologs|lang=zh-CN|style=Feynman)（orthologs，因[物种形成](@keyword=speciation|lang=zh-CN|style=Feynman)事件而分化的基因）和旁系同源基因（paralogs，因基因复制事件后分化的基因）。一个复杂的流程会将[图聚类](@keyword=graph_clustering|lang=zh-CN|style=Feynman)作为出色的第一遍筛选，得到粗略的[基因家族](@keyword=gene_families|lang=zh-CN|style=Feynman)，但随后会更深入地研究，利用基因树本身与[物种树](@keyword=species_tree|lang=zh-CN|style=Feynman)进行协调，以理清表征进化的基因复制和丢失的复杂过程。

一旦我们有了这些可以称之为“[直系同源群](@keyword=orthology_groups|lang=zh-CN|style=Feynman)”（orthogroups）的[基因家族](@keyword=gene_families|lang=zh-CN|style=Feynman)，我们就可以将视野放得更远。我们可以不再关注单个基因，而是通过一个生物体所拥有的[直系同源群](@keyword=orthology_groups|lang=zh-CN|style=Feynman)集合来描述它。这就是[泛基因组学](@keyword=pangenomics|lang=zh-CN|style=Feynman)（pangenomics）背后的思想。考虑一个[巨型病毒](@keyword=giant_viruses|lang=zh-CN|style=Feynman)的谱系。哪些基因对它们所有成员都是必需的？这些构成了“核心”基因组。哪些是可有可无的，只存在于少数成员中？这些是“外壳”或“云”基因。通过简单地计算我们收集的病毒中每个[直系同源群](@keyword=orthology_groups|lang=zh-CN|style=Feynman)的存在与否，我们可以划分它们的整个遗传库。当然，我们必须小心。如果一个[基因组组装](@keyword=genome_assembly|lang=zh-CN|style=Feynman)只有$98\%$的完整度，一个真正的“核心”基因可能因偶然原因而显得缺失。一个稳健的分析会考虑到这一点，使用统计推理将“核心”基因定义为可能存在于$95\%$或更多基因组中，而不是$100\%$的基因组中，这个阈值是根据我们数据的质量选择的。通过这种方式，我们第一步聚类的输出（[直系同源群](@keyword=orthology_groups|lang=zh-CN|style=Feynman)）成为更高层次进化策略分析的输入。

我们可以将这个想法推向其最终结论：对生物体本身进行分类。病毒因其频繁交换基因且缺乏类似于细胞生命中[核糖体RNA](@keyword=ribosomal_rna|lang=zh-CN|style=Feynman)那样的通用标记基因，而极难被置于单一的“生命之树”上。但是我们可以构建一个网络，其中每个节点都是一个完整的[病毒基因组](@keyword=viral_genome|lang=zh-CN|style=Feynman)。我们如何连接它们？我们可以在两个病毒之间画一条边，其权重由它们共享的基因家族（蛋白质簇）数量决定。一种常见的衡量方法是Jaccard指数，$J_{ij} = |C_i \cap C_j| / |C_i \cup C_j|$，其中 $C_i$ 是基因组 $i$ 中的[基因家族](@keyword=gene_families|lang=zh-CN|style=Feynman)集合。这个“基因共享网络”代表了一种集体进化史。对这个网络进行聚类，可以揭示共享共同生活方式和进化轨迹的病毒群组，为[病毒分类](@keyword=virus_classification|lang=zh-CN|style=Feynman)学提供了一个合理、稳健的框架，而这正是传统基于树的方法所无法做到的。从基因到基因组，再到物种的定义，[图聚类](@keyword=graph_clustering|lang=zh-CN|style=Feynman)提供了在每个尺度上观察结构的工具。

### 细胞社会：揭示生物组织

让我们从宏大的进化史诗转向单个生物体的结构。一个发育中的昆虫翅膀、一个细菌菌落或一个人类大脑，都不是同质的细胞袋；它们是复杂的专家社会。我们如何识别这些不同的细胞类型和状态？单细胞RNA测序使我们能够读出数千个单个细胞的基因表达谱。现在，每个细胞都是一个非常高维的“基因表达空间”中的一个点。

就像我们通过[序列相似性](@keyword=sequence_similarity|lang=zh-CN|style=Feynman)连接基因一样，我们现在可以通过表达谱的相似性来连接细胞。我们构建一个$k$-近邻（$k$NN）图，其中每个细胞都与其在这个高维空间中最相似的 $k$ 个邻居相连。结果是一个捕捉了数据局部[流形](@keyword=manifold|lang=zh-CN|style=Feynman)结构的图。当我们对这个图应用[社区发现](@keyword=community_detection|lang=zh-CN|style=Feynman)时，出现的聚类就是我们推定的细胞类型或状态。然后，我们可以查看每个[聚类](@keyword=clustering|lang=zh-CN|style=Feynman)中哪些基因是特异性活跃的，从而赋予它们生物学身份：这些是静脉形成细胞，这些是铰链细胞，等等。

但组织不仅仅是细胞类型的集合；它是一种空间[排列](@keyword=permutation|lang=zh-CN|style=Feynman)。[空间转录组学](@keyword=spatial_transcriptomics|lang=zh-CN|style=Feynman)这一新前沿技术为我们提供了基因表达数据以及每个测量点的物理坐标。这使我们能够提出一个更深刻的问题：我们能否找到既在[转录](@keyword=rna_transcription|lang=zh-CN|style=Feynman)上相似又在空间上连续的组织区域？是的，关键在于构建一个同时了解这两个世界的图。我们可以构建一个图，其中边只在空间上相邻的点之间绘制，并且每条边的权重由它们基因表达的相似性决定。对这个图进行[聚类](@keyword=clustering|lang=zh-CN|style=Feynman)会自动找到边界，在这些边界处，相邻点在表达上突然“看起来”不同，从而揭示出组织中隐藏的解剖区域。在更精细的尺度上，有了足够高分辨率的数据，我们可以使用类似的原理将分子读数的云“分割”成单个细胞，从头开始构建一个[凝聚式聚类](@keyword=agglomerative_clustering|lang=zh-CN|style=Feynman)[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，其合并标准根据测序技术的特定噪声特性量身定制。图再次证明，它是一个极好的灵活工具，能够将不同类型的信息整合到一个单一、连贯的模型中。

### 超越生物学：普适的组织模式

一个思想的力量只有在超越其原始领域时才能真正显现。[基于图的聚类](@keyword=graph_based_clustering|lang=zh-CN|style=Feynman)原理不仅限于生物学；它们是普适的组织原理。

考虑[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)的世界。一位化学家合成了一种三元合金薄膜，其中三种元素（比如A、B和C）的成分在一个三角形晶片上平滑变化。在每个点上，他们测量一个属性，比如X射线衍射（XRD）图谱，这告诉他们局部的[晶体结构](@keyword=crystal_structure|lang=zh-CN|style=Feynman)。他们的目标是绘制一张[相图](@keyword=phase_portraits|lang=zh-CN|style=Feynman)——标出不同稳定晶相的区域。这个问题与空间转录组学完美对应！我们有一个“成分空间”（就像组织的物理空间）和一个“[特征空间](@keyword=feature_space|lang=zh-CN|style=Feynman)”（XRD图谱，就像基因表达）。相场应该是连续的[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)先验知识与组织区域是连续的生物学先验知识是相同的。解决方案是相同的：构建一个连接成分空间中相邻点的图，根据它们XRD特征的相似性为边加权，然后对其进行聚类。由此产生的社区就是未知的相。

让我们做最后一次令人振奋的飞跃。我们能否使用一种旨在寻找DNA分子中折叠结构域的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)来发现立法机构中的政治联盟？这似乎很荒谬，但让我们想一想。我们可以构建一个相似性矩阵，其中条目 $C_{ij}$ 是两位立法者 $i$ 和 $j$ 投票方式相同的比例。这是我们的“接触图”。一个政治联盟将是一个由投票方式非常相似的立法者组成的“区块”。这听起来很像[基因组学](@keyword=genomics|lang=zh-CN|style=Feynman)中的[拓扑关联结构域](@keyword=topologically_associating_domains|lang=zh-CN|style=Feynman)（TAD）。但有一个问题。大多数[TAD识别](@keyword=tad_identification|lang=zh-CN|style=Feynman)[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)都依赖于DNA分子提供自然的一维顺序这一事实。立法者没有这样自然的顺序。将该[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)应用于任意顺序（如按字母顺序）将是无意义的。

绝妙的洞见在于我们可以*创建*一个有意义的顺序。利用谱[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)等技术，我们可以将立法者[排列](@keyword=permutation|lang=zh-CN|style=Feynman)在一条线上，使得投票记录相似的立法者被放置在一起。在这个*新的*、构建的一维坐标上，一个联盟*将*表现为一个连续的区块。现在，我们可以应用[TAD识别](@keyword=tad_identification|lang=zh-CN|style=Feynman)[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，该[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)沿着这条线滑动一个窗口，寻找相邻区块之间低共同投票率的“绝缘”区域——以识别联盟之间的边界。这个例子是[数据科学](@keyword=data_science|lang=zh-CN|style=Feynman)的一个大师级课程：它表明，通过理解我们工具的深层假设，我们可以创造性地调整它们来解决看似无关领域的问题。

从[染色体](@keyword=chromosome|lang=zh-CN|style=Feynman)复杂的折叠到议会中隐藏的派系，探索的目标是相同的：在复杂的相互作用网络中寻找结构。[基于图的聚类](@keyword=graph_based_clustering|lang=zh-CN|style=Feynman)提供了一种简单、优雅且极其统一的思维方式，让我们能够看到构成我们世界基石的社区。