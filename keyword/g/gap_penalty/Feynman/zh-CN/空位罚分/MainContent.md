## 引言
在比较两个故事时，我们不仅会寻找被替换的词语，还会注意到缺失的段落。同样，在生物学中，比较 DNA 或蛋白质序列需要一个系统，该系统不仅要考虑替换，还要考虑插入和缺失（indels）。简单的评分方法无法捕捉这些“[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)”的生物学现实，因此需要一种更精细的方法。本文深入探讨了[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)[罚分](@keyword=gap_penalty|lang=zh-CN|style=Feynman)的概念，这是一种我们为这些进化事件赋予代价的机制。首先，在“原理与机制”部分，我们将探讨不同[罚分](@keyword=gap_penalty|lang=zh-CN|style=Feynman)模型背后的基本原理，从简单的线性代价到更复杂的[仿射空位罚分](@keyword=affine_gap_penalty|lang=zh-CN|style=Feynman)。然后，在“应用与跨学科联系”部分，我们将看到这个基本概念不仅被用于解读进化历史，还应用于[基因组学](@keyword=genomics|lang=zh-CN|style=Feynman)、地质学乃至艺术分析等不同领域。

## 原理与机制

想象一下，你是一位试图拼合两片古代文献碎片的考古学家。你来回滑动它们，寻找重叠的词语和短语。当你比对 $\text{APPLE}$ 和 $\text{APRICOT}$ 时，你会看到相似之处和不同之处。有些字母完全匹配，有些被替换了，有时，似乎有一整块被删除或添加了。生物学中的序列比对与此非常相似，但我们的文本是 DNA 和[蛋白质序列](@keyword=protein_sequence|lang=zh-CN|style=Feynman)，我们试图重建的故事是进化的故事。我们为比对赋予的分数是我们判断哪种进化故事最合理的方式。这一判断的核心在于**[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)罚分**的概念。

### 最简单的故事：计算一致性

衡量两个序列相似度的最基本方法是什么？你可以只计算字母相同的位数，然后除以总长度。这被称为**百分比一致性（percent identity）**。这种方法直观、简单，你可能一个下午就能编写出代码。

但让我们从物理学家的视角来看待这个问题。当我们使用百分比一致性作为分数时，我们*隐含*地做了什么假设？我们实际上在使用一个评分系统，其中[完美匹配](@keyword=perfect_matching|lang=zh-CN|style=Feynman)得分为 $+1$，而错配（例如，$\text{T}$ 与 $\text{C}$ 比对）得分为 $0$。那么[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)呢？如果一个字母与一个空格比对，它对我们的一致性计数贡献也为 $0$。所以，在这个简单的世界里，一个[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)与一个错配没有区别——两者都只是未能保持一致 [@problem_id:2428740]。

这是一个干净、简单的模型。但它符合自然规律吗？将一个氨基酸换成另一个的进化事件，真的等同于完全删除一个氨基酸的事件吗？生物学的答案是响亮的“不”。它们是根本不同类型的突变，我们的模型应该反映这一点。

### 一剂现实主义：[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)的代价

为了使我们的模型更贴近现实，我们必须承认[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)——插入和缺失，即**[插入缺失](@keyword=insertion_and_deletion_(indel)|lang=zh-CN|style=Feynman)（indels）**——是独特的进化事件。它们应该有自己特定的代价。最直接的方法是引入**[线性空位罚分](@keyword=linear_gap_penalty|lang=zh-CN|style=Feynman)（linear gap penalty）**。对于[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)中的每一个字符，我们从总比对分数中减去一个固定的量。假设这个罚分是 $d$。长度为 1 的[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)代价为 $d$，长度为 2 的[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)代价为 $2d$，长度为 $k$ 的[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)代价为 $k \cdot d$。

很简单，对吧？但这种简单性隐藏了一个奇特的假设。在线性罚分模型下，一个长度为（比如）五个氨基酸的连续[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)的罚分，与五个分散在序列各处、独立的单个氨基酸[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)的罚分完全相同。两者的代价都是 $5d$ [@problem_id:2793671]。

想一想这对生物学过程意味着什么。它表明，五个独立的[插入缺失突变](@keyword=indel_mutation|lang=zh-CN|style=Feynman)事件与一个一次性移除五个[残基](@keyword=residue|lang=zh-CN|style=Feynman)的单一事件发生的可能性相同。根据我们对分子生物学的了解，特别是像**[复制滑动](@keyword=replication_slippage|lang=zh-CN|style=Feynman)（replication slippage）**这样的事件，其中细胞机制可能会“口吃”并使一段 DNA 形成环状结构，这感觉不太对。一个单一事件导致一个更大、连续的[插入缺失](@keyword=insertion_and_deletion_(indel)|lang=zh-CN|style=Feynman)是一个众所周知的现象。似乎启动一个[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)应该是困难的部分；一旦机制发生滑动，延伸这个滑动可能没有那么“昂贵”。我们的[线性模型](@keyword=linear_models|lang=zh-CN|style=Feynman)未能捕捉到这个故事。它将一个关于删除的长而连贯的故事，仅仅看作是一系列不相关的单字母拼写错误。

### 仿射模型：一个优雅的进化故事

为了写出更好的故事，我们需要一支更精妙的笔。这就引出了**[仿射空位罚分](@keyword=affine_gap_penalty|lang=zh-CN|style=Feynman)（affine gap penalty）**这个优美的想法。我们现在不再只有一个罚分，而是有两个：

1.  一个**[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)开放罚分（gap opening penalty）**（$g_{open}$）：为开始任何新的[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)而*一次性*支付的高昂代价，无论[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)多长。
2.  一个**[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)延伸罚分（gap extension penalty）**（$g_{extend}$）：为[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)内的*每个*字符支付的较低代价。

因此，一个长度为 $k$ 的[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)的总罚分不再是 $k \cdot d$，而是 $g_{open} + k \cdot g_{extend}$（或者通常表述为 $g_{open} + (k-1) \cdot g_{extend}$，如果开放罚分包含了第一个字符）。让我们用一个具体的例子。假设我们有一个系统，其中[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)开放[罚分](@keyword=gap_penalty|lang=zh-CN|style=Feynman)为 $-11$，延伸[罚分](@keyword=gap_penalty|lang=zh-CN|style=Feynman)为 $-1$。一个 5 个[残基](@keyword=residue|lang=zh-CN|style=Feynman)的[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)的代价是多少？你支付 $-11$ 来打开它，然后为*额外的*四个[残基](@keyword=residue|lang=zh-CN|style=Feynman)支付延伸代价：$4 \times (-1) = -4$。总[罚分](@keyword=gap_penalty|lang=zh-CN|style=Feynman)为 $-11 - 4 = -15$ [@problem_id:2136038]。在一个[线性模型](@keyword=linear_models|lang=zh-CN|style=Feynman)下，如果每个[残基](@keyword=residue|lang=zh-CN|style=Feynman)的[罚分](@keyword=gap_penalty|lang=zh-CN|style=Feynman)为（比如说）$-3$（为了使总代价相同），五个独立的单[残基](@keyword=residue|lang=zh-CN|style=Feynman)[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)的代价也会是 $5 \times (-3) = -15$。但使用我们的仿射模型，五个独立的单[残基](@keyword=residue|lang=zh-CN|style=Feynman)[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)中的每一个都会产生高昂的开放[罚分](@keyword=gap_penalty|lang=zh-CN|style=Feynman)，总代价高达 $5 \times (-11) = -55$！

这种差异是深远的。仿射模型强烈倾向于将[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)组合在一起。它“相信”一个单一、大的[插入缺失](@keyword=insertion_and_deletion_(indel)|lang=zh-CN|style=Feynman)事件远比许多小的、独立的事件更有可能发生 [@problem_id:2121486] [@problem_id:2136317]。这一个数学上的转变——从线性函数到[仿射函数](@keyword=affine_function|lang=zh-CN|style=Feynman)——突然捕捉到了一个深刻的生物学真理：启动像[插入缺失](@keyword=insertion_and_deletion_(indel)|lang=zh-CN|style=Feynman)这样的突变是一个罕见事件（高昂的开放代价），但这样的事件可以有延伸的后果（低廉的延伸代价）[@problem_id:2793671]。

我们现在可以将这两个[罚分](@keyword=gap_penalty|lang=zh-CN|style=Feynman)值看作我们比对机器上的控制旋钮。如果我们想找到具有很少、集中的[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)的比对，我们就把 `gap_open` 旋钮调得很高，把 `gap_extend` 旋钮调得很低。如果出于某种原因，我们认为单[残基](@keyword=residue|lang=zh-CN|style=Feynman)[插入缺失](@keyword=insertion_and_deletion_(indel)|lang=zh-CN|style=Feynman)更为常见，我们就会反其道而行之 [@problem_id:2121506]。仿射模型为我们提供了灵活性，可以根据我们的生物学理解来调整我们的假设。

### 交易的艺术：用错配换取[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)

所以，一个比对[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)试图最大化一个分数。匹配会增加分数，而错配和[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)会减少分数。这就构成了一个有趣的经济学权衡。是接受几个错配“更便宜”，还是引入一个[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)来相对滑动序列以在后续创造更多的匹配“更便宜”？

让我们构建一个思想实验。假设你有两个序列，在没有任何[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)的情况下，最好的比对有 6 个匹配和 6 个错配。如果匹配=+2，错配=-1，那么分数为 $(6 \times 2) + (6 \times -1) = 6$。现在，你团队里一位聪明的生物学家发现，通过插入一个单一的[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)，你可以重新[排列](@keyword=permutation|lang=zh-CN|style=Feynman)比对，得到 10 个匹配和只有 1 个错配。这个新比对的替换分数为 $(10 \times 2) + (1 \times -1) = 19$。这是一个巨大的提升！但这是以[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)的代价换来的。

只有当新的含[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)比对的总分高于原来的 6 时，它才更好。也就是说，$19 - (\text{空位代价}) \ge 6$。如果[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)代价仅仅是开放罚分 $g_{open}$，那么只有当 $g_{open} \le 13$ 时，这笔交易才是划算的。数字 $13$ 就是**[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)**。如果开放一个[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)的罚分高于 13，比对[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)将“决定”宁愿忍受 6 个错配，也不愿支付[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)的代价 [@problem_id:2392977]。

这揭示了比对分数的真正本质：它是一种评估相互竞争的进化假说的货币。[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)[罚分](@keyword=gap_penalty|lang=zh-CN|style=Feynman)是汇率。通过设定它们，我们正在定义点突变和[插入缺失](@keyword=insertion_and_deletion_(indel)|lang=zh-CN|style=Feynman)事件之间权衡的确切条款。我们甚至可以求解出能使两种不同进化故事（例如，一个有[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)，一个没有）同样 plausible 的[罚分](@keyword=gap_penalty|lang=zh-CN|style=Feynman)值，从而完美地平衡账目 [@problem_id:2428701]。

### 完善叙事：特殊情况与未来方向

一个好的物理模型的美妙之处在于它可以被调整和完善。[仿射空位罚分](@keyword=affine_gap_penalty|lang=zh-CN|style=Feynman)是现代生物信息学的主力，但故事并未就此结束。

例如，序列最开始或结尾的[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)怎么办？如果你正在将一个短的蛋白质序列与整个[染色体](@keyword=chromosome|lang=zh-CN|style=Feynman)进行比较，以找到它所属的位置，你不会[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)两端能够完美匹配。像惩罚内部[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)一样严厉地惩罚这些**末端[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)（terminal gaps）**是没有意义的。因此，许多[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)使用变体，其中末端[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)是“免费的”或具有降低的[罚分](@keyword=gap_penalty|lang=zh-CN|style=Feynman)，这是一个简单的调整，但对最终的分数和比对有重大影响 [@problem_id:2393053]。

我们还可以变得更复杂。仿射模型假设将一个[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)从长度 4 延伸到 5 的代价与将其从长度 99 延伸到 100 的代价相同。这总是正确的吗？也许某些生物学机制使得非常大的插入或删除像一个单一、内聚的单元一样起作用。这引出了**凹形[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)[罚分](@keyword=gap_penalty|lang=zh-CN|style=Feynman)（concave gap penalties）**的想法，即随着[空位](@keyword=vacancies|lang=zh-CN|style=Feynman)变长，延伸[罚分](@keyword=gap_penalty|lang=zh-CN|style=Feynman)本身会减小。虽然处理这个问题的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)更复杂，但物理直觉是清晰的：我们总是在努力完善我们的数学模型，以讲述一个关于美丽、混乱而又迷人的进化过程的更准确、更精细的故事 [@problem_id:2371048]。