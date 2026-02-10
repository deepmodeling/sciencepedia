## 应用与跨学科联系

在我们穿越了量子力学的原理和机制之后，你可能会留有一种抽象优雅的感觉。我们已经看到，如果两个算符，比如 $\hat{A}$ 和 $\hat{B}$，对易——也就是说，如果 $\hat{A}\hat{B} - \hat{B}\hat{A} = 0$——那么我们可以找到一个系统的状态，它同时具有对应的物理量 $A$ 和 $B$ 的确定值。这是一段优美的数学。但仅此而已吗？只是理论家们的好奇心吗？

绝对不是！这个原理是物理学家和化学家工具箱中最强大、最实用的工具之一。它是我们理解几乎所有事物，从原子的形状到计算机芯片功能的秘钥。要了解这一点，让我们思考一下拥有一个确定值到底意味着什么。如果一个系统处于一个对应于守恒量的算符的[本征态](@keyword=eigenstates|lang=zh-CN|style=Feynman)，它将*保持*在该本征态。这个值是一个“好标签”，是系统随时间携带的永久标记。在许多方面，物理学的艺术就是寻找这些好标签的艺术。而我们找到它们的方式就是寻找对称性。

### 构造宇宙：原子

让我们从最著名的成功故事开始：氢原子。电子并不仅仅是随机地围绕质子嗡嗡作响；它被库仑力固定在位，这个势只取决于它们之间的距离 $r$。电子是在北、南、东还是西并不重要；在相同距离下，力是相同的。这个系统具有[球对称性](@keyword=spherical_symmetry|lang=zh-CN|style=Feynman)。

这在算符的语言中意味着什么？这意味着决定系统能量的哈密顿算符 $\hat{H}$ 不会因任何旋转而改变。因此，$\hat{H}$ 必须与产生旋转的算符——[角动量算符](@keyword=angular_momentum_operators|lang=zh-CN|style=Feynman)——对易。具体来说，哈密顿算符与[总角动量](@keyword=total_angular_momentum|lang=zh-CN|style=Feynman)平方 $\hat{L}^2$ 以及它的任意一个分量（我们通常选择为 $\hat{L}_z$）对易[@problem_id:2676183]。

$$[\hat{H}, \hat{L}^2] = 0 \quad \text{和} \quad [\hat{H}, \hat{L}_z] = 0$$

因为这三个算符彼此都对易，我们可以找到一套完备的状态，它们是所有这三个算符的共同[本征函数](@keyword=eigenfunctions|lang=zh-CN|style=Feynman)！这些状态正是你在化学中学到的原子轨道。我们可以用一组“好”的[量子数](@keyword=quantum_numbers|lang=zh-CN|style=Feynman)来标记它们：主量子数 $n$ 代表能量，[轨道角动量量子数](@keyword=l_quantum_number|lang=zh-CN|style=Feynman) $\ell$ 代表 $\hat{L}^2$ 的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)，[磁量子数](@keyword=magnetic_quantum_number|lang=zh-CN|style=Feynman) $m$ 代表 $\hat{L}_z$ 的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)。这些不仅仅是任意的标签；它们是状态的深层、守恒的属性，由原子的基本对称性所保证。我们能够通过将氢原子的薛定谔方程分离成径向和角向部分来求解，这正是这种对称性的直接结果。能级的简并——为什么所有具有相同 $n$ 和 $\ell$ 但不同 $m$ 的状态具有相同的能量——并非偶然；它是来自势的[球对称性](@keyword=spherical_symmetry|lang=zh-CN|style=Feynman)的直接信息。

事实上，氢原子还有一个更奇特的、“偶然的”对称性，与其势的具体 $1/r$ 形式有关。这产生了另一个守恒量，即Laplace-Runge-Lenz矢量，它解释了为什么具有不同 $\ell$ 但相同 $n$ 的状态也是简并的。这种更深层次的对称性也使得这个问题可以在抛物线坐标中求解，这暗示了如果对称性足够丰富，自然界会提供多种同样有效的方式来标记其状态[@problem_id:2676183]。

### 从原子到分子和固体

这个思想远远超出了单个原子。考虑一个旋转的分子。它不是一个球体；它可能像一个哑铃或一个旋转的陀螺。它的对称性不同，但原理是相同的。对于一个[对称陀螺分子](@keyword=symmetric_top_molecules|lang=zh-CN|style=Feynman)，哈密顿算符仍然与总角动量 $J^2$ 及其在实验室固定坐标轴上的投影 $J_z$ 对易。但它也与角动量在分子自身对称轴上的投影 $\hat{J}_{\text{body-z}}$ 对易[@problem_id:2623869]。这组[对易算符](@keyword=commuting_operators|lang=zh-CN|style=Feynman) $\{H, J^2, J_z, \hat{J}_{\text{body-z}}\}$，给了我们一组新的、稳健的[量子数](@keyword=quantum_numbers|lang=zh-CN|style=Feynman) $(J, M, K)$，它们唯一地标记了旋转状态。当[分子光谱学](@keyword=molecular_spectroscopy|lang=zh-CN|style=Feynman)家在他们的数据中看到尖锐的吸收线时，他们正在见证这些状态之间的量子跃迁，每一个状态都由自然的对称性精心标记。

让我们再次扩大规模，到一个包含无数原子[排列](@keyword=permutation|lang=zh-CN|style=Feynman)在完美、重复[晶格](@keyword=crystal_lattice|lang=zh-CN|style=Feynman)中的整个晶体。这里决定性的对称性不是旋转，而是*平移*。如果你将整个晶体平移一个[晶格间距](@keyword=lattice_spacing|lang=zh-CN|style=Feynman) $a$，势看起来完全一样。这意味着[哈密顿算符](@keyword=hamiltonian_operator|lang=zh-CN|style=Feynman) $\hat{H}$ 必须与平移算符 $\hat{T}_a$ 对易[@problem_id:2834256]。

$$[\hat{H}, \hat{T}_a] = 0$$

这告诉我们什么？它告诉我们，晶体中电子的能量本征态也可以被选为平移算符的本征态。像 $\hat{T}_a$ 这样的幺[正算符](@keyword=positive_operator|lang=zh-CN|style=Feynman)的[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)必须是模为1的复数，所以我们可以把它们写成 $e^{ika}$，其中 $k$ 是一种新的标签。这个 $k$ 就是著名的*[准动量](@keyword=crystal_momentum|lang=zh-CN|style=Feynman)*。它不是真正的动量，但它是来自晶体平移对称性的“好标签”。对于任何给定的 $k$，都有一整梯可能的能级，由另一个整数 $n$ 索引。当我们改变 $k$ 时，这些能级描绘出著名的固体*[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)*。所有现代电子学的基础——金属、绝缘体和[半导体](@keyword=semiconductor|lang=zh-CN|style=Feynman)的整个理论——都建立在这个简单的思想之上。你的手机处理器之所以能工作，正是电子在周期性晶体中拥有良好量子标签的直接结果。

### 简化的艺术：计算科学

到目前为止，我们已经谈到了对称性提供的优美概念框架。但它们的力量也是非常实用的。对于任何比氢原子更复杂的系统，精确求解薛定谔方程都是不可能的。我们必须求助于强大的计算机来寻找近似解。

考虑计算分子电子结构的任务。像[Hartree-Fock](@keyword=hartree_fock|lang=zh-CN|style=Feynman)或[组态相互作用](@keyword=configuration_interaction|lang=zh-CN|style=Feynman)（CI）这样的方法涉及到构建和[对角化](@keyword=diagonalization|lang=zh-CN|style=Feynman)巨大的矩阵。即使是一个中等大小分子的矩阵也可能有数十亿个元素。这在计算上是不可能的。但在这里，对称性前来拯救。分子的[哈密顿算符](@keyword=hamiltonian_operator|lang=zh-CN|style=Feynman)几乎总是与其他算符对易，例如总自旋 $\hat{S}^2$ 或对应于分子空间对称性（旋转、反射）的算符[@problem_id:2457206], [@problem_id:2765437]。

如果我们足够聪明，*首先*将我们的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)构建成这些对称性算符的[本征函数](@keyword=eigenfunctions|lang=zh-CN|style=Feynman)，那么[对易算符](@keyword=commuting_operators|lang=zh-CN|style=Feynman)的原理保证了那个庞大的[哈密顿矩阵](@keyword=hamiltonian_matrix|lang=zh-CN|style=Feynman)将变得*[块对角化](@keyword=block_diagonalization|lang=zh-CN|style=Feynman)*。所有非零元素将被限制在沿对角线的小方块中，而不同块之间的元素将恰好为零。计算机不再需要[对角化](@keyword=diagonalization|lang=zh-CN|style=Feynman)一个不可能大的矩阵，而只需要对角化许多更小、可管理的矩阵。这个技巧，源于对易的抽象原理，将棘手的问题简化为常规计算。毫不夸张地说，没有它，现代[计算化学](@keyword=computational_chemistry|lang=zh-CN|style=Feynman)和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)将是不可能的。

### 新前沿：[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)

这个原理不仅仅是用来理解世界本来的样子；它也是构建未来的蓝图。在蓬勃发展的[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)领域，一个主要挑战是保护脆弱的[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)（[量子比特](@keyword=qubit|lang=zh-CN|style=Feynman)）免受噪声和错误的影响。最有前途的策略之一是使用[量子纠错码](@keyword=quantum_error_correcting_codes|lang=zh-CN|style=Feynman)。

许多这类编码，被称为[稳定子码](@keyword=stabilizer_codes|lang=zh-CN|style=Feynman)，直接建立在共同[本征态](@keyword=eigenstates|lang=zh-CN|style=Feynman)的思想之上。人们定义一组对易的算符，即“稳定子”，并将“编码空间”——[量子信息](@keyword=quantum_information|lang=zh-CN|style=Feynman)的安全港——定义为所有状态的子空间，这些状态是*每一个[稳定子算符](@keyword=stabilizer_operators|lang=zh-CN|style=Feynman)*的共同本征矢量，且[本征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)均为 $+1$ [@problem_id:946907]。通过测量这些[稳定子算符](@keyword=stabilizer_operators|lang=zh-CN|style=Feynman)，可以检测是否发生了错误（通过检查状态是否仍在 $+1$ [本征空间](@keyword=eigenspaces|lang=zh-CN|style=Feynman)中），而不会干扰编码在其中的宝贵信息。这些复杂编码的整个架构都是寻找“[对易可观测量](@keyword=commuting_observables|lang=zh-CN|style=Feynman)完[全集](@keyword=universal_set|lang=zh-CN|style=Feynman)”的直接、工程化的应用。

### 一点警示：非对易之美

认为[非对易算符](@keyword=non_commuting_operators|lang=zh-CN|style=Feynman)是一种麻烦是错误的。事实上，它们不能对易是量子力学一些最深刻、最惊人特征的源泉。当两个算符*不*对易时，这是来自自然界的一个信息：你不能同时知道这两个量。你不可能有一套完整的共享标签。

例如，对于一个自旋为1的粒子，自旋的z分量算符 $\hat{S}_z$ 和x分量平方算符 $\hat{S}_x^2$ 不对易[@problem_id:2086039]。这告诉你，一般而言，一个具有确定 $S_z$ 值的状态不能有确定的 $S_x^2$ 值。这就是不确定性原理的根源。

后果可能更加微妙。对于一个由两个相互作用的自旋组成的系统，总自旋平方算符 $\hat{S}^2$ 与*第一个*[粒子自旋](@keyword=particle_spin|lang=zh-CN|style=Feynman)的z分量 $\hat{S}_{1z}$ 不对易[@problem_id:2086065], [@problem_id:2086297]。这意味着什么？这意味着你通常不能构建一个既有确定[总自旋](@keyword=total_spin|lang=zh-CN|style=Feynman)*又*有确定粒子1自旋的状态。这就是纠缠的核心。像单态 $\frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle)$ 这样的状态，具有完全确定的[总自旋](@keyword=total_spin|lang=zh-CN|style=Feynman)（$S=0$），但每个独立粒子的自旋是完全不确定的。知其整体便失其部分。这种[非对易性](@keyword=non_commutativity|lang=zh-CN|style=Feynman)不是一个缺陷；它是对自然界最深奥谜团之一的数学描述。

从物质的结构到计算的逻辑，两个算符是否对易这个简单的问题具有深远的影响。它提供了一条贯穿始终的主线，一个单一的原理，告诉我们如何标记世界，如何简化我们对世界的描述，以及如何欣赏其内在的、不可简化的奇异性。