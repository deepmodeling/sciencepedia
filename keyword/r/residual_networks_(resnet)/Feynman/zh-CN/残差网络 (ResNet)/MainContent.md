## 引言
随着神经网络为解决更复杂的问题而变得越来越深，它们遇到了一个根本性的障碍：退化问题。当网络深度超过某个阈值后，增加更多的层不仅无法提升性能，反而会对其造成损害，这主要是由于[梯度消失问题](@keyword=vanishing_gradient_problem|lang=zh-CN|style=Feynman)削弱了学习过程。我们如何才能构建成百上千层深度的网络，同时确保它们能够被有效训练呢？[残差网络](@keyword=residual_networks|lang=zh-CN|style=Feynman) ([ResNet](@keyword=resnets|lang=zh-CN|style=Feynman)s) 为这一挑战提供了一个极其简洁而又非常有效的解决方案。本文将深入探讨使 [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 成为深度学习历史上最重要突破之一的核心思想。

首先，我们将探讨 [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 背后的**原理与机制**，剖析[残差块](@keyword=residual_blocks|lang=zh-CN|style=Feynman)并理解它如何重新构建学习任务。我们将揭示保证梯度稳定流动的数学基础，正是这一基础使得网络深度达到了前所未有的水平。随后，关于**应用与跨学科联系**的章节将拓宽我们的视野，揭示 [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 原理不仅仅是一种工程技巧，更是一个在物理学、生物学和数值分析中均有呼应的基本概念，为学习、动力学和稳定性提供了一个统一的视角。

## 原理与机制

想象一下，你正试图教一个聪明的学生一门全新的、复杂的学科。你可以尝试让他们从头开始记住一整本教科书。或者，你可以从他们已有的知识——比如经典力学——入手，只教给他们理解量子力学所需的*修正*部分。后一种方法几乎总是更容易。学生无需背负重新学习所有知识的负担，而是可以将其强大的智力集中在掌握新旧知识之间的“[残差](@keyword=residue|lang=zh-CN|style=Feynman)”差异上。

[残差网络](@keyword=residual_networks|lang=zh-CN|style=Feynman) ([ResNet](@keyword=resnets|lang=zh-CN|style=Feynman)s) 就建立在这种极其简单而强大的思想之上。我们不强迫一堆网络层从头学习一个复杂的变换，而是要求它们学习*[残差](@keyword=residue|lang=zh-CN|style=Feynman)*，即对一个更简单的基准变换——[恒等变换](@keyword=identity_transformation|lang=zh-CN|style=Feynman)——的修正。

### 学习“剩下”要学习的东西

[ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 的核心是**[残差块](@keyword=residual_blocks|lang=zh-CN|style=Feynman)**。一个标准的[神经网络](@keyword=neural_networks|lang=zh-CN|style=Feynman)层可能会尝试学习一个映射 $H(x)$，将输入 $x$ 转换为[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的输出。然而，一个[残差块](@keyword=residual_blocks|lang=zh-CN|style=Feynman)重新定义了这个任务。它旨在学习一个[残差](@keyword=residue|lang=zh-CN|style=Feynman)函数，我们称之为 $F(x)$，使得该块的输出定义为 $y = x + F(x)$。

为什么这种方法如此有效？网络现在有了一个选择。如果对于某个给定层，最优的变换就是[恒等变换](@keyword=identity_transformation|lang=zh-CN|style=Feynman)——即，只是将输入原封不动地传递过去——网络可以非常轻松地实现这一点：它只需要学习使[残差](@keyword=residue|lang=zh-CN|style=Feynman)函数 $F(x)$ 的输出为零。这远比强迫一堆复杂的非线性层去学习[单位矩阵](@keyword=identity_matrix|lang=zh-CN|style=Feynman)要容易得多，后者是一项出了名的困难任务。

这种“误差修正”的观点可以更具体地阐述。假设对于给定的输入 $x$，理想的目标表示是 $t$。一个传统的层将难以学习整个映射 $H(x) = t$。而一个[残差块](@keyword=residual_blocks|lang=zh-CN|style=Feynman)则重新构建了这个问题。[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的输出是 $t = x + F(x)$，这意味着[残差](@keyword=residue|lang=zh-CN|style=Feynman)函数只需要学习它们之间的差值，即 $F(x) = t - x$。直观上，我们可以想象在训练过程中，网络的优化过程将驱动[残差](@keyword=residue|lang=zh-CN|style=Feynman)函数的输出 $F(x)$ 在方向上与这个目标误差 $t-x$ 对齐。一个简单的衡量方法是观察这两个向量之间夹角的余弦值；一个接近 1 的值将表明该块正在成功地学习如何修正输入以逼近目标 [@problem_id:3169972]。

### 不受阻碍的信息高速公路

[残差连接](@keyword=residual_connections|lang=zh-CN|style=Feynman)的具体形式 $y = x + F(x)$ 并非任意选择。其简单的加性特性是它的超能力所在。为了理解这一点，回顾一个相关的想法——**Highway Network** 会有所帮助。Highway Network 使用了类似的结构，但带有一个动态的“门”来控制[信息流](@keyword=information_flow|lang=zh-CN|style=Feynman)：
$$ y = T(x) \odot F(x) + (1 - T(x)) \odot x $$
这里，$\odot$ 表示按元素乘法，而 $T(x)$ 是一个“变换门”，其输出值在 0 和 1 之间。如果 $T(x)$ 为 1，输出就是变换后的 $F(x)$。如果 $T(x)$ 为 0，输出就是[恒等变换](@keyword=identity_transformation|lang=zh-CN|style=Feynman) $x$。

这似乎更灵活，那么为什么更简单的 [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 结构变得如此主导呢？想象一下，恒等路径是一条信息高速公路，它允许数据，更重要的是，梯度，从网络末端毫不费力地流回起点。在 Highway Network 中，门 $T(x)$ 就像这条高速公路上的一个可变收费站。原则上，网络可以学会将门设置为零，保持高速公路畅通。但它也可能学会将门设置为接近一的值，这实际上关闭了恒等路径，并迫使所有信息通过复杂的变换 $F(x)$。如果发生这种情况，我们就又回到了起点，面对一个深度的“普通”网络，其中的[信息流](@keyword=information_flow|lang=zh-CN|style=Feynman)很容易退化。

[ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 的加性连接 $x + F(x)$ 就像一条带有永久“快速通道”的高速公路。信息总有一条清晰、无阻碍的线性路径可以通行。[残差](@keyword=residue|lang=zh-CN|style=Feynman)函数 $F(x)$ 仅仅是一个为主流动添加新信息的出口和入口匝道。这种架构上的保证才是关键所在。它确保了网络至少不会比[恒等变换](@keyword=identity_transformation|lang=zh-CN|style=Feynman)表现得更差，为学习提供了一个坚实的骨干 [@problem_id:3170021]。

### [深度学习](@keyword=deep_learning|lang=zh-CN|style=Feynman)的微积分

这种“不受阻碍的高速公路”的直觉得到了一个优美而精确的数学基础的支持，这也是 [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 能够被训练到前所未有的深度的关键。极深的“普通”网络的问题在于梯度。在训练期间，误差信号（梯度）必须从最后一层一直传播回第一层来更新权重。这是通过微积分的[链式法则](@keyword=chain_rule|lang=zh-CN|style=Feynman)完成的，对于深度网络而言，这涉及到一长串[雅可比矩阵](@keyword=jacobian_matrix|lang=zh-CN|style=Feynman)的乘积，每一层对应一个。
$$ g_{\text{input}} = J_1^T J_2^T \dots J_L^T g_{\text{output}} $$
如果这些[雅可比矩阵](@keyword=jacobian_matrix|lang=zh-CN|style=Feynman)的范数持续小于 1，它们的乘积将呈指数级缩小，导致**[梯度消失](@keyword=vanishing_gradients|lang=zh-CN|style=Feynman)**——信号消失了。如果它们的范数持续大于 1，乘积将呈指数级增长，导致**[梯度爆炸](@keyword=exploding_gradients|lang=zh-CN|style=Feynman)**——信号过载。

让我们看一下单个 [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 块的[雅可比矩阵](@keyword=jacobian_matrix|lang=zh-CN|style=Feynman)。其变换是 $y = x + F(x)$。这个[映射的雅可比矩阵](@keyword=jacobian_matrix_of_a_map|lang=zh-CN|style=Feynman) $J_{\text{res}}$ 是：
$$ J_{\text{res}} = \frac{\partial}{\partial x} (x + F(x)) = I + \frac{\partial F(x)}{\partial x} = I + J_{\text{plain}} $$
其中 $I$ 是单位矩阵，$J_{\text{plain}}$ 是[残差](@keyword=residue|lang=zh-CN|style=Feynman)函数 $F(x)$ 本身的[雅可比矩阵](@keyword=jacobian_matrix|lang=zh-CN|style=Feynman)。这个简单的方程就是秘诀所在。它告诉我们，通过[残差块](@keyword=residual_blocks|lang=zh-CN|style=Feynman)的变换不是某个任意矩阵，而是单位矩阵*加上一个微调*。

这对变换的[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)有什么影响？如果向量 $v$ 是 $J_{\text{plain}}$ 的一个[特征向量](@keyword=eigenvector|lang=zh-CN|style=Feynman)，其[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)为 $\mu$，那么 $(I + J_{\text{plain}})v = Iv + J_{\text{plain}}v = v + \mu v = (1+\mu)v$。整个 [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 块的[雅可比矩阵的特征值](@keyword=jacobian_matrix_eigenvalues|lang=zh-CN|style=Feynman)就是[残差](@keyword=residue|lang=zh-CN|style=Feynman)的[雅可比矩阵的特征值](@keyword=jacobian_matrix_eigenvalues|lang=zh-CN|style=Feynman)再加 1！如果[残差](@keyword=residue|lang=zh-CN|style=Feynman)函数 $F(x)$ 初始化为一个小的变换（一个“[弱学习器](@keyword=weak_learners|lang=zh-CN|style=Feynman)”），它的[雅可比矩阵](@keyword=jacobian_matrix|lang=zh-CN|style=Feynman) $J_{\text{plain}}$ 的[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)将接近于零。这意味着整个块的[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman) $1+\mu$ 将聚集在 1 附近。一个[特征值](@keyword=eigenvalue|lang=zh-CN|style=Feynman)和[奇异值](@keyword=singular_values|lang=zh-CN|style=Feynman)都接近 1 的矩阵，在与之相乘时，能在很大程度上保持[向量的范数](@keyword=norm_of_a_vector|lang=zh-CN|style=Feynman)。当我们通过一个深度 [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 进行[反向传播](@keyword=backpropagation|lang=zh-CN|style=Feynman)时，我们实际上是在乘以一长串这样的矩阵。由于它们的范数都接近 1，它们的乘积不会系统性地消失或爆炸，从而允许梯度信号完整地跨越成百上千层传播 [@problem_id:3187046]。

然而，这并非万能灵药。其原理是保持雅可比范数接近 1。如果[残差](@keyword=residue|lang=zh-CN|style=Feynman)的雅可比矩阵 $J_{\text{plain}}$ 变得过大，且其方式与单位矩阵对齐，那么 $I + J_{\text{plain}}$ 的范数就可能持续超过 1，导致[梯度爆炸](@keyword=exploding_gradients|lang=zh-CN|style=Feynman)。更高级的变体使用缩放[残差](@keyword=residue|lang=zh-CN|style=Feynman)，如 $(1-\beta)x + \alpha F(x)$，来明确控制雅可比范数，并保证其有界于 1，从而提供更稳定的训练 [@problem_id:3185064]。

### 更深层次的观点与统一的原理

当我们看到[残差连接](@keyword=residual_connections|lang=zh-CN|style=Feynman)如何将[深度学习](@keyword=deep_learning|lang=zh-CN|style=Feynman)与科学和数学中的其他基本思想联系起来时，其真正的美才得以展现。

#### [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 作为离散化的[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)

再次考虑[残差](@keyword=residue|lang=zh-CN|style=Feynman)更新规则：$x_{l+1} = x_l + F(x_l)$。如果我们将每个层索引 $l$ 想象成时间上的一个离散步骤，并将函数 $F$ 看作是一个小步长 $h$ 乘以某个[向量场](@keyword=vector_field|lang=zh-CN|style=Feynman) $f$，我们就得到 $x_{l+1} = x_l + h \cdot f(x_l)$。这无非就是**[显式欧拉法](@keyword=explicit_euler_method|lang=zh-CN|style=Feynman)**，是求解形如 $\dot{x}(t) = f(x(t))$ 的[常微分方程](@keyword=ordinary_differential_equations|lang=zh-CN|style=Feynman) (ODE) 的最简单数值方法之一。

从这个角度看，一个 [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 不仅仅是一堆离散的层；它是在模拟一个[连续时间动力系统](@keyword=continuous_time_dynamical_system|lang=zh-CN|style=Feynman)。输入特征 $x_0$ 是一个初始条件，网络根据一个学习到的[向量场](@keyword=vector_field|lang=zh-CN|style=Feynman)，通过“时间”（深度）来演化这个状态，最终达到最终状态 $x_L$。更深的网络对应于更小的步长 $h$，正如任何学过数值方法的学生所知，这通常能更精确地逼近真实的连续轨迹 [@problem_id:3223766]。这个强大的类比将整个数值分析工具箱引入到[网络架构](@keyword=network_architecture|lang=zh-CN|style=Feynman)设计中。例如，我们知道像前向欧拉法这样的显式方法对于某些“刚性”问题可能会变得不稳定，需要极小的步长。这转化为在某些任务上需要极深的网络。这一洞见启发了基于更稳定的*隐式* ODE 求解器的新架构，这些架构可以用少得多的层数达到相同的结果 [@problem_id:3202086]。

#### [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 作为学习器集成

看待 [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 的另一种方式是“展开”其递推关系。最终层 $L$ 的输出是：
$$ x_L = x_{L-1} + F_{L-1}(x_{L-1}) = (x_{L-2} + F_{L-2}(x_{L-2})) + F_{L-1}(x_{L-1}) = \dots = x_0 + \sum_{l=0}^{L-1} F_l(x_l) $$
这揭示了最终的表示是初始表示加上所有后续[残差](@keyword=residue|lang=zh-CN|style=Feynman)修改的总和。这与**[集成方法](@keyword=ensemble_methods|lang=zh-CN|style=Feynman)**（如[梯度提升](@keyword=gradient_boosting|lang=zh-CN|style=Feynman)）有着惊人的相似之处，在[集成方法](@keyword=ensemble_methods|lang=zh-CN|style=Feynman)中，最终的预测是通过对许多“[弱学习器](@keyword=weak_learners|lang=zh-CN|style=Feynman)”的贡献求和得出的，每个[弱学习器](@keyword=weak_learners|lang=zh-CN|style=Feynman)都被训练来纠正其前面学习器的错误。在这种观点下，[ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 不是一个单一的庞大模型，而是一个非常深的集成。每个[残差块](@keyword=residual_blocks|lang=zh-CN|style=Feynman) $F_l$ 并不是试图解决整个问题，而只是学习对表示进行一次小范围、有针对性的修正。在训练过程中，梯度信号沿着恒等高速公路清晰地向下流动，鼓励每个块贡献一个与减少总体损[失相](@keyword=dephasing|lang=zh-CN|style=Feynman)一致的修正 [@problem_id:3169973]。

这一观点也阐明了通用近似的概念。虽然 [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 并未从根本上扩展可以被近似的函数类别，但它重新构建了问题。用 [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 近似[目标函数](@keyword=objective_function|lang=zh-CN|style=Feynman) $f(x)$ 等价于用一个普通网络来近似[残差](@keyword=residue|lang=zh-CN|style=Feynman)函数 $f(x) - x$ [@problem_id:3194207]。如果[目标函数](@keyword=objective_function|lang=zh-CN|style=Feynman)已经接近[恒等变换](@keyword=identity_transformation|lang=zh-CN|style=Feynman)，那么[残差](@keyword=residue|lang=zh-CN|style=Feynman)就很小，从而使它成为一个更容易学习的函数。

### 架构的改进

这些核心原则指导了 [ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 架构的改进。例如，最初的论文将 ReLU 非线性层置于加法*之后*（后激活）。然而，从“不受阻碍的高速公路”的角度思考，研究人员意识到，将激活函数移到[残差](@keyword=residue|lang=zh-CN|style=Feynman)分支内卷积层*之前*（预激活）会创建一条更纯粹的恒等路径。这确保了捷径是一个纯粹的恒等连接，从而带来更好的性能 [@problem_id:3197663]。同样，分析反向传播路径的组合结构表明，[ResNet](@keyword=resnets|lang=zh-CN|style=Feynman) 创建了一种非常特定的模式：在任意两层之间，存在许多并行路径，但它们的长度完全相同。这在结构上不同于其他架构，如 [DenseNet](@keyword=densenet|lang=zh-CN|style=Feynman)，后者创建了大量不同长度的路径，导致了一种不同形式的“隐式深度监督” [@problem_id:3114054]。

归根结底，[残差网络](@keyword=residual_networks|lang=zh-CN|style=Feynman)的力量在于其优雅的简洁性。通过将学习问题从整体变换重新构建为增量修正，它为构建我们最强大的学习机器提供了一个稳健、稳定且深度统一的框架。

