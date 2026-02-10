## 应用与跨学科联系

既然我们已经剖析了 `bfloat16` 格式的内部结构，我们可能会留下一个萦绕不去的问题：何必多此一举？为什么要心甘情愿地扔掉我们宝贵精度的一半？这感觉有点像一个音乐家选择用一门弦更少的乐器来演奏。正如我们即将看到的，答案是出奇地反直觉。这种刻意牺牲的行为不是一种妥协，而是一把钥匙——一把能够解锁计算速度和能源效率惊人收益的钥匙，它正在彻底改变从人工智能到基础[科学模拟](@keyword=scientific_simulation|lang=zh-CN|style=Feynman)的各个领域。这是一个关于“足够好”的算术艺术的故事，以及它如何帮助我们以十年前只能梦想的方式进行计算。

### 现代人工智能的引擎：速度、规模与能耗

让我们从计算最原始的方面开始：能耗。芯片上每当一个晶体管翻转，它就消耗一小口电能。当你有数十亿个晶体管每秒翻转数十亿次时，这些小口就汇成了一场洪流。现代 [CMOS](@keyword=complementary_metal_oxide_semiconductor|lang=zh-CN|style=Feynman) 芯片的动态[功耗](@keyword=power_dissipation|lang=zh-CN|style=Feynman)遵循一个来自物理学的优美而简单的关系式：$P_{\text{dyn}} = \alpha C V^2 f$。功耗随工作电压 $V$ 的平方增长！这种平方依赖关系是个“暴君”。为了构建更快、更节能的芯片，架构师们拼命地想降低电压。

我们的故事就从这里开始。为 `bfloat16` 这种更简单的格式设计的专用硬件，通常可以比其更复杂、更高精度的同类产品在更低的电压下运行。即使 `bfloat16` 操作涉及稍高的[开关电容](@keyword=switched_capacitor|lang=zh-CN|style=Feynman) $C$，从 $V^2$ 项中获得的收益也可能是巨大的。这导致每次计算消耗的能量急剧下降，我们可以将这个量建模为 $E_{\text{op}} = \alpha C V^2$。在一个数据中心耗电量与小国相当的世界里，这不仅仅是学术上的好奇心，更是一项全球性的迫切需求 [@problem_id:3634564]。

当然，如果结果无用，这种节能将是一笔愚蠢的交易。我们付出的数值代价是什么？让我们想象一个长长的计算链，比如在[卷积神经网络](@keyword=convolutional_neural_networks|lang=zh-CN|style=Feynman)中处理单个图像所需的数百万次乘加运算。每个 `bfloat16` 操作都会引入一个微小的[舍入误差](@keyword=roundoff_error|lang=zh-CN|style=Feynman)。虽然每个误差都很小，但它们会累积起来。我们可以将其建模为在每一步都添加一点“噪声”。

这个噪声有多“大”？如果我们分析[信噪比 (SNR)](@keyword=signal_to_noise_ratio_(snr)|lang=zh-CN|style=Feynman)，即真实信号强度与累积计算噪声的比值，差异是惊人的。一个在标准 32 位浮点 (FP32) 格式下可能具有高达 $8.44 \times 10^{10}$ 的卓越信噪比的假设计算，在相同条件下用 `bfloat16` 执行时，其信噪比可能会下降到约 $19.7$ [@problem_id:3636764]。另一种看待它的方式是通过最坏情况的视角，即累积的[相对误差](@keyword=relative_error|lang=zh-CN|style=Feynman)会在多次运算后大幅增长 [@problem_id:3634569]。

[信噪比](@keyword=signal_to_quantization_noise_ratio|lang=zh-CN|style=Feynman)大约只有二十！这听起来很糟糕！但这就是许多机器学习算法的魔力所在。通过梯度下降法训练[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络的过程本身就是一个充满噪声的[随机过程](@keyword=stochastic_process|lang=zh-CN|style=Feynman)。损失函数的地形是一个狂野的高维地带，而算法只是在试图找到下山的路。来自 `bfloat16` 算术的额外噪声通常就像一种温和的、随机的颠簸，并不会使算法偏离[轨道](@keyword=orbit|lang=zh-CN|style=Feynman)——在某些情况下，甚至可能帮助它摆脱一个糟糕的局部最小值！对于许多常见的、表现良好的问题，无论你使用 `bfloat16` 还是 FP32，最终的准确性几乎是相同的。

然而，这并非一个普适的保证。如果问题在数值上很棘手（“病态的”），或者我们需要找到一个精度极高的解，`bfloat16` 的[量化噪声](@keyword=quantization_noise|lang=zh-CN|style=Feynman)可能就太大了。优化过程可能会减慢，甚至永久卡住，无法进行达到目标所需的最后、微妙的调整 [@problem_id:3210624]。艺术在于知道何时“足够好”是真的足够好，并通过适当地预缩放数据来管理数字的动态范围，以防止上溢或[下溢](@keyword=underflow|lang=zh-CN|style=Feynman) [@problem_id:3634529]。

当我们从单个处理器转向用于训练当今庞大基础模型的大规模[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)式超级计算机时，`bfloat16` 的好处会成倍增加。这些模型非常大，必须被分割到数千个 GPU 上。这个过程中的一个关键瓶颈是通信：GPU 必须不断地相互通信以同步它们的工作，主要方式是在一个称为全归约 (All-Reduce) 的步骤中对它们本地计算的梯度求和。由于 `bfloat16` 数字的大小是 FP32 的一半，你可以在相同的成本下通过网络线路传输两倍的数据，或者在一半的时间内传输相同的数据。这极大地减少了依赖于网络带宽的通信时间。

但在这里，大自然也揭示了它的微妙之处。通信时间有两个部分：一个带宽项（管道有多粗？）和一个延迟项（第一滴水通过需要多长时间？）。`bfloat16` 有助于前者，但对后者毫无作用。在极端规模下，当你拥有大量处理器时，随着处理器数量增长的延迟项可能成为主要瓶颈，较小数据格式的优势随之减弱。理解计算、带宽和延迟之间的这种相互作用，对于构建下一代人工智能超级计算机至关重要 [@problem_id:3270717]。

### 超越[深度学习](@keyword=deep_learning|lang=zh-CN|style=Feynman)：科学发现的新工具

你可能认为这只是一个关于人工智能的故事。但科学中最深刻的思想往往会溢出其原有的边界。在[深度学习](@keyword=deep_learning|lang=zh-CN|style=Feynman)的熔炉中磨练出来的[混合精度计算](@keyword=mixed_precision_computing|lang=zh-CN|style=Feynman)原理，现在正在改变传统科学和工程模拟的格局。

考虑计算科学中最古老、最基本的问题之一：求解线性方程组 $Ax = b$。这是从设计桥梁到预测天气等一切事物的核心。标准方法，即 LU 分解，对于大型系统来说在计算上可能极其严苛。但如果我们能用一个技巧呢？如果我们用快速的低精度 `bfloat16` 来执行大部分工作——即昂贵的分解过程呢？这将给我们一个快速但有些不准确的初始答案。现在，神来之笔在于，我们使用高精度的 64 位算术来计算我们的答案偏差了多少（即“残差”）。这个残差告诉我们解中的误差。然后我们再次使用我们快速但廉价的求解器来求解一个*修正量*，并将这个修正量在高精度下加回到我们的解中。

这个过程被称为*[迭代求精](@keyword=iterative_refinement|lang=zh-CN|style=Feynman)*，就像用粗炭笔画出粗略的草图，然后用细尖笔清理细节。通过重复几次，我们通常能以完全高精度求解成本的一小部分，获得一个高度准确的解 [@problem_id:3245419]。同样强大的思想也延伸到更复杂的求解器，如用于[计算地球物理学](@keyword=computational_geophysics|lang=zh-CN|style=Feynman)等领域的 GMRES。在这里，人们必须更像一位艺术家，仔细[选择算法](@keyword=selection_algorithm|lang=zh-CN|style=Feynman)的哪些部分可以容忍 `bfloat16` 的噪声（如矩阵-向量乘积），哪些部分需要[双精度](@keyword=double_precision_2|lang=zh-CN|style=Feynman)不折不扣的精确性（如确保[基向量](@keyword=basis_vector|lang=zh-CN|style=Feynman)保持正交的步骤） [@problem_id:3616860]。

这将我们带到了一个激动人心的融合点：机器学习与传统科学模拟的结合。科学家们现在正在使用*物理信息神经网络* (PINN) 来求解复杂的[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)，例如控制[流体流动](@keyword=fluid_flow|lang=zh-CN|style=Feynman)的[纳维-斯托克斯方程](@keyword=navier_stokes_equations|lang=zh-CN|style=Feynman)。PINN 通过不仅试图满足实验数据，而且试图满足方程本身的物理定律来学习解。为了训练这些用于复杂 3D 问题的庞大模型，我们需要动用我们所有的技巧。我们使用 `bfloat16` 来实现网络中闪电般快速的前向和后向传播。但是，当我们计算损失函数——它衡量网络遵守物理定律的程度——我们必须格外小心。这些计算通常涉及相减两个几乎相等的大数，这在低精度下是灾难性的，被称为灾难性抵消。因此，基于物理的残差必须在更高精度下计算和累积。这种技术的优雅融合使我们能够利用人工智能硬件的力量来解决以前无法企及的科学问题，这完美地证明了计算原理的统一力量 [@problem_id:3410608]。

### 精度的哲学

我们与 `bfloat16` 的旅程，带领我们从单个晶体管的物理学走向行星级超级计算机的架构；从[神经网络损失函数](@keyword=neural_network_loss_function|lang=zh-CN|style=Feynman)地形的抽象世界走向[流体动力学](@keyword=fluid_dynamics|lang=zh-CN|style=Feynman)的具体模拟。我们发现一个反复出现的主题：在每一步都追求绝对精度并不总是最明智的道路。通过理解我们问题和算法的结构，我们可以在关键之处应用精度，并在能够加速我们进程的地方拥抱“足够好”。`bfloat16` 格式不仅仅是一个巧妙的工程技巧；它是这种更深层次计算智慧的体现。它告诉我们，通过智能地放弃完美，我们可以实现以前不可能完成的事情。