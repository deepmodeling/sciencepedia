## 应用与跨学科联系

好了，我们已经看过了这个奇妙合作关系的蓝图。我们有[经典计算](@keyword=classical_computation|lang=zh-CN|style=Feynman)机，这位总建筑师，负责绘制宏伟蓝图和管理工作流程。我们还有量子处理器，这位才华横溢但专精一隅的神童，准备好应对那些让经典机器完全束手无策、极其复杂的任务。这在理论上是一个美好的想法。但这个充满活力的二人组究竟能 *构建* 出什么？它们又在何处落地实践呢？

让我们离开抽象的理论，踏上一段进入科学与工程工作坊的旅程，在那里，这些混合[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)有望成为新的强大工具。我们将看到，核心策略总是一样的：找到计算瓶颈，那颗抵抗经典铁锤的顽固钉子，并设计一个量子工具来狠狠地敲打它。

### 革新分子与[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)

混合[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)最自然的主场是[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)领域。毕竟，有什么比[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机更适合模拟量子系统呢？几十年来，化学家们使用了一种名为[自洽场](@keyword=self_consistent_field|lang=zh-CN|style=Feynman)（SCF）方法的强大策略。你可以把它想象成一个绝妙的迭代猜谜游戏。你猜测分子中所有电子的排布方式，计算它们产生的电场，然后在这个电场中为电子找到一个 *更佳的* 排布。你一遍又一遍地重复这个过程，直到你的排布不再改变——它变得“自洽”了。

这个游戏中的一步，对应于求解一个名为 Roothaan 方程的矩阵[本征值问题](@keyword=eigenvalue_problems|lang=zh-CN|style=Feynman)，在计算上相当繁重。这是一个明确定义的常规任务，但对于大分子来说成本可能很高。所以，这里就有了我们第一个、最直接的应用：为什么不把这一步交给我们的量子朋友呢？在经典 SCF 过程的每一步，[经典计算](@keyword=classical_computation|lang=zh-CN|style=Feynman)机构建必要的矩阵——[Fock 矩阵](@keyword=fock_matrix|lang=zh-CN|style=Feynman)——并将其发送给量子处理器。[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机的工作就是简单地找到这个矩阵的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)和本征向量，而像[变分量子本征求解器](@keyword=variational_quantum_eigensolver|lang=zh-CN|style=Feynman)（VQE）这样的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)正是为此设计的。然后它将答案交还给经典计算机，后者用它来准备下一轮计算。这就像是把你汽车引擎的某个部件换成一个更强大但颇具异国情调的替代品 [@problem_id:2464763]。

但这仅仅是热身。化学领域的真正奖赏并不仅仅是加速旧的近似方法，而是解决以前无法解决的问题。真正的“猛兽”是物理学家所说的“电子关联”——电子间因相互排斥而产生的复杂、协调的舞蹈。这种舞蹈是所有[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)的来源，但要完美精确地描述它，其复杂性呈指数级增长，即使是最大的超级计算机也力不从心。这正是混合方法开始大放异彩的地方。

我们可以巧妙地避开一次性模拟整个舞蹈的难题。在像“双杂化”密度泛函理论这样的高级方法中，计算中最棘手的部分就涉及这种关联。所以，我们聚焦于此。我们将描述完整关联之舞的艰巨任务分解为大量更小、更易于管理的问题，比如一次只处理一对电子之间的相互作用。这些微小的“二重奏”中的每一个都可以交给一个小型量子处理器处理。量子设备解决一对电子的关联能，然后是另一对，再另一对。[经典计算](@keyword=classical_computation|lang=zh-CN|style=Feynman)机则扮演总编舞的角色，收集数百万个微小[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)的结果，以组装出完整的杰作 [@problem_id:2454275]。

这种“分而治之”的哲学可以更进一步。想象你是一名电影导演。你不需要用最昂贵的高清摄影机去拍摄背景演员；你会把它留给主角。[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)家也可以做同样的事情。在一个庞大而复杂的系统中——比如一个药物分子与一个酶结合，或者一个[催化剂](@keyword=catalyst|lang=zh-CN|style=Feynman)吸附在表面上——最有趣的[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)发生在一个小的、局域的“[活性位点](@keyword=active_site|lang=zh-CN|style=Feynman)”。系统的其余部分主要只是在搭建舞台。于是，我们使用一种“[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)”理论，比如名字起得很棒的[密度矩阵嵌入理论](@keyword=density_matrix_embedding_theory|lang=zh-CN|style=Feynman)（DMET）。经典计算机在较低的近似水平上模拟整个系统。但对于那个小的、至关重要的[活性位点](@keyword=active_site|lang=zh-CN|style=Feynman)，它会构建一个量身定制的量子问题。它将这个问题（现在包含了周围环境的影响）交给量子处理器，进行全面、高精度的求解。然后两台机器来回沟通，确保它们对彼此边界的描述[完美匹配](@keyword=perfect_matching|lang=zh-CN|style=Feynman)。这就是我们如何利用一台小型[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机来研究一个实际大小的系统——通过仅在最关键的地方集中其力量 [@problem_id:2797527]。

经典世界和量子世界之间这种紧密、迭代的握手也是诸如[完全活性空间自洽场](@keyword=casscf|lang=zh-CN|style=Feynman)（CASSCF）[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)等方法的核心。在这里，[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机（使用 VQE）解决一个小的“活性空间”轨道内的完整关联问题，而[经典计算](@keyword=classical_computation|lang=zh-CN|style=Feynman)机利用这些结果——即单粒子和双粒子密度矩阵——来计算如何旋转轨道本身以找到更低的能量。这种来回往复一直持续到活性空间内的[波函数](@keyword=wavefunction|lang=zh-CN|style=Feynman)和定义该空间的轨道都共同优化为止 [@problem_id:2932467]。

但分子不是静态的物体；它们[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)、旋转和反应。它们生活在一个动态的世界中。要捕捉这一点，我们需要模拟它们随时间的运动。在这里，混合方法再次变得至关重要。在溶剂中的[化学反应](@keyword=chemical_reaction|lang=zh-CN|style=Feynman)模拟中，反应分子是我们的量子“明星”，而成千上万的溶剂分子则是经典的“环境”。随着环境中的经典原子因热运动而[抖动](@keyword=dither|lang=zh-CN|style=Feynman)和流动，它们会改变量子子系统感受到的电场。这反过来又会改变[量子能级](@keyword=quantum_energy_levels|lang=zh-CN|style=Feynman)，甚至可能引发[量子跃迁](@keyword=quantum_jumps|lang=zh-CN|style=Feynman)——[非绝热跃迁](@keyword=non_adiabatic_transitions|lang=zh-CN|style=Feynman)——这是[光化学](@keyword=photochemistry|lang=zh-CN|style=Feynman)和许多生物过程的本质。因此，一个完整的模拟必须是一个动态的、自洽的循环：环境的经典运动影响量子的演化，而量子系统的状态决定了作用于经典环境的力 [@problem_id:2777939]。描述这种深度相互作用的理论，融合了经典[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学和[开放量子系统](@keyword=open_quantum_systems|lang=zh-CN|style=Feynman)的思想，其本身就是智识传统的美丽“混合体” [@problem_id:2637881] [@problem_id:2928319]。

### 超越分子：工程与物理学的新工具

使用量子求解器来解决一个特别棘手的子问题的原则并不仅限于化学领域。这是一个可以应用于整个科学和工程领域的通用策略。考虑一下模拟新飞机机翼上的气流，或复杂发动机部件中的热流所面临的挑战。这些现象由[偏微分方程](@keyword=partial_differential_equation|lang=zh-CN|style=Feynman)（PDE）控制。几十年来，工程师们一直使用像“[区域分解](@keyword=domain_decomposition|lang=zh-CN|style=Feynman)”这样的技术来解决这些问题。他们将物理空间——机翼、发动机——切割成更小的、重叠的子区域，并在每个部分上求解方程，在边界之间来回传递信息，直到找到[全局解](@keyword=global_solution|lang=zh-CN|style=Feynman)。

现在，想象其中一个子区域特别棘手。也许它是一个极端[湍流](@keyword=turbulence|lang=zh-CN|style=Feynman)区，或者是两种不同材料相遇的[边界层](@keyword=boundary_layer|lang=zh-CN|style=Feynman)，产生了难以用经典方法建模的复杂物理现象。这为混合[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)提供了一个完美的切入点。[经典计算](@keyword=classical_computation|lang=zh-CN|style=Feynman)机可以处理所有“简单”的子区域，而量子处理器则负责在那个“困难”的区域求解方程 [@problem_id:2387023]。尽管用于求解由[偏微分方程](@keyword=partial_differential_equation|lang=zh-CN|style=Feynman)产生的大型线性系统的量子算法仍在发展中，但这种[区域分解](@keyword=domain_decomposition|lang=zh-CN|style=Feynman)框架为将它们集成到作为现代工程基石的大规模模拟代码中，提供了一个自然而强大的蓝图。

### 几句忠告：[量子加速](@keyword=quantum_speedup|lang=zh-CN|style=Feynman)的艺术

讲到这里，我们很容易得意忘形，以为只要在任何难题上撒上一点量子算法，就能期待奇迹般的加速。但[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机不是魔杖。它是一个工具，和任何工具一样，它也可能被错误使用。其艺术在于知道 *何时* 以及 *如何* 应用它。

让我们回到最初的任务：寻找箱中量子粒子的能级。“打靶法”是一种经典的技巧。你猜测一个能量，解出薛定谔方程，然后看你的解在边界处是否表现正常。如果不对，你就调整能量再试一次。一位同事可能会建议：“啊哈！这是一个搜索问题！让我们创建一个包含一百万个可能能量的列表，并使用 Grover 的量子搜索算法来找到正确的那一个。它是量子的，一定更快！”

这是一个绝妙的，也是绝妙地错误的想法。想象一下你正在调谐一个老式模拟收音机。如果电台位于完全随机的频率上，你可能需要检查刻度盘上的每一个点——这是一次[非结构化搜索](@keyword=unstructured_search|lang=zh-CN|style=Feynman)。量子搜索确实可以加速这个过程。但收音机并非如此工作。当你越接近正确的频率，信号就越清晰。你不是[随机搜索](@keyword=random_search|lang=zh-CN|style=Feynman)，你只是“跟着信号”走向峰值。寻找[能量本征值](@keyword=energy_eigenvalues|lang=zh-CN|style=Feynman)的问题就像那样——它是一个 *结构化* 搜索。随着你逼近真实能量，解的“不匹配度”会以一种可预测的方式减小。像[二分法](@keyword=bisection_method|lang=zh-CN|style=Feynman)这样的经典[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)可以利用这种结构以令人难以置信的效率逼近答案，所需的步数仅随所需精度的 *对数* 增长。

另一方面，提议的 Grover 搜索完全忽略了这种结构。它将能量列表视为一堆随机的杂物。虽然它比 *经典[随机搜索](@keyword=random_search|lang=zh-CN|style=Feynman)* 提供了平方级加速，但其成本与精度的 *平方根* 成比例。对于任何合理高的精度，智能的经典[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)不仅更快，而且是 *压倒性地* 更快。在这里使用 Grover [算法](@keyword=algorithm|lang=zh-CN|style=Feynman)就像用推土机砸核桃。这是一种壮观的力量展示，但一个简单的手持核桃夹会有效得多 [@problem_id:2437478]。这里的教训是深刻的：只有当[量子算法](@keyword=quantum_algorithms|lang=zh-CN|style=Feynman)能够以经典计算机无法做到的方式利用问题结构时，[量子加速](@keyword=quantum_speedup|lang=zh-CN|style=Feynman)才可能实现。

### [算法](@keyword=algorithm|lang=zh-CN|style=Feynman)构建[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)：一个[自指](@keyword=self_referencing|lang=zh-CN|style=Feynman)的转折

或许这个故事中最令人愉快和脑洞大开的转折是，混合[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)正被用来构建……嗯，用来构建更好的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机。一个由人类编写的量子程序是一组抽象的操作。要在真实的量子处理器上运行它，它必须被“编译”——即翻译成硬件能够实际执行的一系列基本操作，如物理[激光脉冲](@keyword=laser_pulses|lang=zh-CN|style=Feynman)或微波信号。这个编译问题本身就极为复杂。

著名的 Solovay-Kitaev 定理告诉我们，我们可以用一个有限[通用门集](@keyword=universal_gate_sets|lang=zh-CN|style=Feynman)合中的一个门序列来近似任何[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的[量子操作](@keyword=quantum_operations|lang=zh-CN|style=Feynman)。找到这个序列的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)是递归的。但在每个递归步骤的核心都是一个搜索问题：从一个预先计算好的库（或网）中为一个目标操作寻找一个“粗略”的近似。而我们拥有的搜索库的最佳工具是什么？量子搜索！

于是，我们得到了一个美丽的、自指的循环。我们使用一个混合[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)来编译我们的量子程序，其中经典计算机指导递归策略，但在每一步，它都会调用量子处理器来运行 Grover [算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，以找到谜题的下一块。这里甚至还有一个微妙的优化游戏可以玩，即平衡量子搜索的成本与最终门序列的长度，以找到最佳的递归层数 [@problem_id:172581]。在一个非常真实的意义上，[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机正在靠自己的力量“拔靴[自举](@keyword=bootstrapping|lang=zh-CN|style=Feynman)”——当然，也离不开其经典伙伴的一点点、也是至关重要的帮助。

从发现新药到设计更高效的飞机，再到构建[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)本身的结构，近未来的故事不是一个新技术取代旧技术的故事。它是一个关于伙伴关系、关于协同作用的故事。它是一种认识：世界既有经典特性，也有量子特性，要真正理解和改造它，我们的计算工具也必须兼具这两种特性。