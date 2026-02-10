## 应用与[交叉](@keyword=chiasmata|lang=zh-CN|style=Feynman)学科联系

现在我们已经窥探了克尔猫[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)的原理，一个自然而激动人心的问题随之而来：我们用它来做什么？物理学家笔记本里的一个巧妙想法是一回事；一台工作机器中的有用组件则是另一回事。像克尔猫[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)这样的概念，其真正的美妙之处并非孤立地显现，而是在于我们看到它如何与更广阔的世界连接，解决旧问题，并不可避免地创造新问题。它从一个抽象原理到实用设备的旅程，迫使我们像建筑师和工程师一样思考，跨越学科界限，应对只有在尝试构建真实事物时才会出现的挑战。

### 量子动物园：构建[混合系统](@keyword=hybrid_systems|lang=zh-CN|style=Feynman)

[量子计算](@keyword=quantum_computing|lang=zh-CN|style=Feynman)的世界并非铁板一块。它是一个充满活力的[生态系统](@keyword=ecosystems|lang=zh-CN|style=Feynman)，一个名副其实的不同[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)技术的动物园。一些[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)，比如我们遇到过的超导transmon，就像短跑运动员——[速度](@keyword=velocity|lang=zh-CN|style=Feynman)快、敏捷，非常适合执行快速计算。另一些则像马拉松运动员——更稳定，能更长时间地保持其[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)，但操纵起来可能较慢。克尔猫[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)，凭借其对一种误差类型的内置保护，是扮演马拉松运动员角色的主要候选者，一个潜在的[量子存储器](@keyword=quantum_memory|lang=zh-CN|style=Feynman)。

宏大的愿景是构建一台*混合*[量子计算](@keyword=quantum_computing|lang=zh-CN|style=Feynman)机，一个由专家组成的团队，其中不同类型的[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)协同工作，各展其长。一个快速的transmon可能执行一项计算，然后将结果交给一个稳健的克尔猫[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)进行保管。这听起来很棒，但正如任何翻译人员所知，在两种不同“语言”之间传递信息是一门精细的艺术。

想象一下将[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)从一个标准码（比如由三个常规[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)构成的码）[转移](@keyword=metastasis|lang=zh-CN|style=Feynman)到一个克尔猫[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)的任务。这不仅仅是一个理论练习；它是任何此类混合机器中的基本操作。科学家们已经探索了实现这种“编码切换”的协议。但当现实世界带着其持续的噪声介入时，会发生什么呢？

让我们考虑一个基于这一挑战的场景 [@problem_id:68425]。假设我们初始系统中的一个常规[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)容易发生相位翻转误差，而克尔猫[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)天生*不*能防御这类误差。我们执行交接操作，这是一段精心编排的量子舞蹈，旨在将信息[转移](@keyword=metastasis|lang=zh-CN|style=Feynman)过去。我们发现了一些既微妙又深刻的东西：误差随着信息一起被转换了。初始常规[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)上的相位翻转误差，可能会在最终状态上表现为逻辑相位翻转误差，此时信息已存储在克尔猫系统中。

这是一个至关重要的见解！它告诉我们，[混合系统](@keyword=hybrid_systems|lang=zh-CN|style=Feynman)一个部分的噪声特性可以直接影响另一部分，即使第二部分使用了完全不同的物理编码。克尔猫对比特翻转的内在偏置是一个巨大的优势，但这并不意味着系统能免受所有威胁，尤其是在与外部世界通信时。这迫使我们进行整体思考。设计[量子计算](@keyword=quantum_computing|lang=zh-CN|style=Feynman)机不仅仅是完善单个[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)；它关乎理解和管理它们之间的*接口*。这是[量子工程](@keyword=quantum_engineering|lang=zh-CN|style=Feynman)的一个新前沿，在这里，[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)的原理与硬件设计的实用性相遇。

### 邻近问题：规模化带来的关联误差

让我们从连接不同*类型*的[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)，转向连接许多*相同*类型的[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)。如果我们想构建一台真正强大的[量子计算](@keyword=quantum_computing|lang=zh-CN|style=Feynman)机，我们需要扩大规模。我们需要的不是一两个克尔猫[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)，而是成千上万，甚至数百万个，都[排列](@keyword=permutations|lang=zh-CN|style=Feynman)在一个芯片上。而一旦我们将物体靠得很近，它们就开始相互作用，并不总是以我们期望的方式。

想象一下两个人在一个狭小、安静的房间里试图进行独立的对话。不偷听到对方是不可能的。[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)也是如此。如果我们将两个克尔猫[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)彼此靠近放置，并将它们连接到一个共同的硬件——比如一个用于读出其状态的共享导[线或](@keyword=wired_or|lang=zh-CN|style=Feynman)“[传输线](@keyword=transmission_lines|lang=zh-CN|style=Feynman)”——它们就不再是真正独立的了。这条共享线路可以成为噪声的共同[信道](@keyword=information_channel|lang=zh-CN|style=Feynman)。

在这里，我们遇到了[量子计算](@keyword=quantum_computing|lang=zh-CN|style=Feynman)版图上最强大的巨龙之一：*关联误差*。我们最简单的[纠错](@keyword=error_correction|lang=zh-CN|style=Feynman)模型通常假设误差在每个[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)上是随机且独立地出现的。但是，如果一个单一的物理事件同时在多个[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)上引起误差呢？

这正是我们被迫面对的新物理学。考虑两个耦合到共同“泄漏”环境的克尔猫[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman) [@problem_id:68414]。正如我们所见，猫[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)的主要误差是[光子](@keyword=photons|lang=zh-CN|style=Feynman)损耗，这会导致逻辑比特翻转。现在，想象一个[光子](@keyword=photons|lang=zh-CN|style=Feynman)从*共享*环境中泄漏出去。它来自哪里？系统不知道。这个事件本身是[光子](@keyword=photons|lang=zh-CN|style=Feynman)来自第一个[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)和[光子](@keyword=photons|lang=zh-CN|style=Feynman)来自第二个[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)的[叠加](@keyword=superposition|lang=zh-CN|style=Feynman)。

惊人的结果是，这个单一的物理事件并不仅仅导致[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)A*或*[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)B上的比特翻转。相反，它可以使[双量子比特系统](@keyword=two_qubit_system|lang=zh-CN|style=Feynman)进入一个*误差的[纠缠态](@keyword=entangled_states|lang=zh-CN|style=Feynman)*——一个“A上比特翻转，B上无事”和“A上无事，B上比特翻转”的幽灵般的[叠加](@keyword=superposition|lang=zh-CN|style=Feynman)。一个单一的、局域的物理事件，导致了一个非局域的、关联的逻辑误差。这比一个简单的、独立的误差要复杂得多。这些误差[纠缠](@keyword=entanglement|lang=zh-CN|style=Feynman)的程度，物理学家用一个称为*并发度*（concurrence）的量来[量化](@keyword=quantization|lang=zh-CN|style=Feynman)，直接取决于物理布局——每个[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)与那个共享的、泄漏的信[道耦合](@keyword=channel_coupling|lang=zh-CN|style=Feynman)的强度。

这说明了一个优美而又发人深省的观点。扩大规模和连接组件的行为本身就引入了新的、集体的误差现象，这些现象在单[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)层面是不存在的。在这种背景下，克尔猫[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)变成了一个强大的探针。通过研究它在多[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)阵列中的行为，我们了解了这些关联误差的性质，这对于设计下一代[量子纠错码](@keyword=quantum_error_correcting_codes|lang=zh-CN|style=Feynman)至关重要——这些[纠错码](@keyword=error_correcting_codes|lang=zh-CN|style=Feynman)能够意识到它们所运行硬件的物理几何形状和共享相互作用。

从混合架构到关联噪声的幽灵，克尔猫[量子比特](@keyword=qubits|lang=zh-CN|style=Feynman)不仅仅是一个有前途的硬件。它是一位向导，引领我们穿越系统级[量子工程](@keyword=quantum_engineering|lang=zh-CN|style=Feynman)这个迷人而复杂的领域。它教导我们，通往[容错量子计算机](@keyword=fault_tolerant_quantum_computer|lang=zh-CN|style=Feynman)的[道路](@keyword=continuous_path|lang=zh-CN|style=Feynman)，不仅仅是在孤立中改进单个组件，更是要理解和掌握整个系统丰富、互联的物理学。这段旅程揭示了单个[谐振](@keyword=resonance|lang=zh-CN|style=Feynman)器的[量子力学](@keyword=quantum_mechanics|lang=zh-CN|style=Feynman)与计算机宏大架构原理之间的深刻统一。