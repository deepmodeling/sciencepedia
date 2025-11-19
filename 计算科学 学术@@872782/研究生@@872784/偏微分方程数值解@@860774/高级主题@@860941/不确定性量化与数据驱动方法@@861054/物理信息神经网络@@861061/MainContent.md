## 引言
在科学计算的广阔领域中，我们[长期依赖](@entry_id:637847)于传统的数值方法（如[有限元法](@entry_id:749389)和有限差分法）来求解描述物理现象的[偏微分方程](@entry_id:141332)（PDEs）。尽管这些方法取得了巨大成功，但它们在处理复杂几何、高维度问题以及数据驱动的逆问题时常面临挑战。另一方面，纯粹的数据驱动[深度学习模型](@entry_id:635298)虽然在许多领域展现了惊人的能力，却往往缺乏物理一致性，其预测可能违背基本的自然法则。物理信息神经网络（Physics-Informed Neural Networks, [PINNs](@entry_id:145229)）正是在这一背景下应运而生，它代表了一种融合了第一性原理与机器学习的革命性[范式](@entry_id:161181)，旨在弥合这两种方法的鸿沟。

本文旨在系统地介绍PINN的理论框架与实践应用。在第一章“原理与机制”中，我们将深入剖析PINN的核心思想，阐明如何将物理定律编码为可微的损失函数，并探讨[自动微分](@entry_id:144512)和网络架构在其中的关键作用。接着，在第二章“应用与跨学科连接”中，我们将展示PINN如何作为一种通用工具，灵活地应用于从[固体力学](@entry_id:164042)到[金融工程](@entry_id:136943)等多个领域的正向与逆向问题求解。最后，在“动手实践”部分，您将通过具体的编程练习，将理论知识转化为解决实际问题的能力。

通过这三个层次的递进学习，您将全面掌握PINN这一前沿技术，并理解其在现代科学与工程研究中的巨大潜力。让我们首先从构建PINN的基石——其基本原理与核心机制开始。

## 原理与机制

[物理信息神经网络](@entry_id:145229)（Physics-Informed Neural Networks, [PINNs](@entry_id:145229)）是一种将物理定律以可微形式编码进[神经网](@entry_id:276355)络中的[科学机器学习](@entry_id:145555)方法。其核心思想是将一个[偏微分方程](@entry_id:141332)（PDE）的求解过程重新表述为一个[优化问题](@entry_id:266749)，其中[神经网](@entry_id:276355)络的参数被训练以最小化一个衡量其对控制方程和边界条件违反程度的[损失函数](@entry_id:634569)。本章将深入探讨构成PINN框架的基本原理和关键机制，从损失函数的构建到优化过程的动态特性，再到影响其性能的高级概念。

### 核心公式：基于物理的损失函数

PINN的基础是其独特的损失函数构造，它直接将PDE的结构嵌入到学习目标中。这个[损失函数](@entry_id:634569)通常由几个部分组成，每个部分都对应于待解问题的不同约束。

#### 强形式残差

考虑一个定义在域 $\Omega \subset \mathbb{R}^d$ 上的泛型PDE，其边界为 $\partial\Omega$。该问题可以表示为：
$$
\begin{align*}
\mathcal{N}[u](\boldsymbol{x}) = f(\boldsymbol{x}), \quad \boldsymbol{x} \in \Omega \\
\mathcal{B}[u](\boldsymbol{x}) = g(\boldsymbol{x}), \quad \boldsymbol{x} \in \partial\Omega
\end{align*}
$$
其中 $u(\boldsymbol{x})$ 是待求解的未知函数，$\mathcal{N}$ 是一个（可能为[非线性](@entry_id:637147)的）[微分算子](@entry_id:140145)，$f(\boldsymbol{x})$ 是源项，$\mathcal{B}$ 是[边界算子](@entry_id:160216)，$g(\boldsymbol{x})$ 是给定的边界数据。

PINN引入一个参数为 $\theta$ 的[神经网](@entry_id:276355)络 $u_\theta(\boldsymbol{x})$ 作为代理或近似解。与传统数值方法不同，PINN不求解离散网格上的数值，而是学习一个在整个连续域上都有效的[解析函数](@entry_id:139584) $u_\theta$。训练的目标是找到最优参数 $\theta^*$，使得 $u_{\theta^*}(\boldsymbol{x})$ 近似满足上述PDE系统。

这是通过定义一个**强形式残差**（strong-form residual）来实现的。对于域内部的任意点 $\boldsymbol{x} \in \Omega$，PDE残差定义为：
$$
r_{\text{int}}(\boldsymbol{x}; \theta) = \mathcal{N}[u_\theta](\boldsymbol{x}) - f(\boldsymbol{x})
$$
类似地，对于边界上的任意点 $\boldsymbol{x} \in \partial\Omega$，边界残差定义为：
$$
r_{\text{b}}(\boldsymbol{x}; \theta) = \mathcal{B}[u_\theta](\boldsymbol{x}) - g(\boldsymbol{x})
$$
这两个残差函数量化了[神经网](@entry_id:276355)络近似解 $u_\theta$ 在每个点上对物理定律和边界条件的违反程度。值得强调的是，算子 $\mathcal{N}$ 和 $\mathcal{B}$ 是作用于函数 $u_\theta$ 上的[连续算子](@entry_id:143297)，其导数是通过**[自动微分](@entry_id:144512)**（Automatic Differentiation, AD）精确计算的，我们将在下一节详细讨论。

这个概念与传统数值方法（如有限差分法，FD）中的**[截断误差](@entry_id:140949)**（truncation error）有本质区别。[有限差分法](@entry_id:147158)的[截断误差](@entry_id:140949) $\tau_h(\boldsymbol{x}) = \mathcal{N}_h[u](\boldsymbol{x}) - \mathcal{N}[u](\boldsymbol{x})$，是在一个离散网格点 $\boldsymbol{x}$ 上，用离散算子 $\mathcal{N}_h$ 作用于*精确解* $u$ 时产生的误差。它衡量的是离散化方案本身的一致性。而PINN的残差是在任意连续点 $\boldsymbol{x}$ 上，用[连续算子](@entry_id:143297) $\mathcal{N}$ 作用于*近似解* $u_\theta$ 的结果，衡量的是近似解对PDE的满足程度 [@problem_id:3431046]。

#### [损失函数](@entry_id:634569)的构建

有了残差的定义，我们就可以构建一个可优化的[损失函数](@entry_id:634569)。这通常通过在从域和边界采样的**[配置点](@entry_id:169000)**（collocation points）集合上，计算均方残差来实现。给定内部[配置点](@entry_id:169000)集 $\{\boldsymbol{x}_i\}_{i=1}^{M} \subset \Omega$ 和边界[配置点](@entry_id:169000)集 $\{\boldsymbol{x}^{(b)}_j\}_{j=1}^{N} \subset \partial\Omega$，总损失函数 $L(\theta)$ 可以写成加权和的形式：
$$
L(\theta) = L_{\text{int}}(\theta) + \lambda_b L_{\text{b}}(\theta)
$$
其中，$L_{\text{int}}$ 是内部PDE残差损失，$L_{\text{b}}$ 是边界条件残差损失，$\lambda_b > 0$ 是一个平衡两者的超参数。

以二维泊松方程为例 [@problem_id:3430996]，考虑在单位正方形 $\Omega = [0,1]^2$ 上的问题，其齐次狄利克雷边界条件为：
$$
-\Delta u = f \quad \text{in } \Omega, \qquad u = 0 \quad \text{on } \partial\Omega
$$
这里，[拉普拉斯算子](@entry_id:146319) $\Delta u = \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2}$。根据定义，内部残差为 $r_{\text{int}}(x,y; \theta) = - \Delta u_\theta(x,y) - f(x,y)$。边界残差为 $r_{\text{b}}(x,y; \theta) = u_\theta(x,y) - 0 = u_\theta(x,y)$。因此，总的[均方误差损失函数](@entry_id:634102)为：
$$
L(\theta) = \frac{1}{M} \sum_{i=1}^{M} \left( \frac{\partial^2 u_{\theta}}{\partial x^2}(x_i, y_i) + \frac{\partial^2 u_{\theta}}{\partial y^2}(x_i, y_i) + f(x_i, y_i) \right)^2 + \frac{\lambda_b}{N} \sum_{j=1}^{N} \left( u_{\theta}(x^{(b)}_{j}, y^{(b)}_{j}) \right)^2
$$
训练过程就是通过梯度下降等优化算法，寻找使该[损失函数](@entry_id:634569) $L(\theta)$ 最小化的参数 $\theta$。

### [自动微分](@entry_id:144512)与网络架构的角色

PINN框架的有效性在很大程度上依赖于两个关键技术：[自动微分](@entry_id:144512)（AD）和[神经网](@entry_id:276355)络的架构设计。

#### [自动微分](@entry_id:144512)：精确导数的计算引擎

如前所述，PINN残差的计算需要[微分算子](@entry_id:140145) $\mathcal{N}$ 作用于[神经网](@entry_id:276355)络 $u_\theta$。这意味着我们需要计算 $u_\theta$ 关于其输入坐标（例如 $x, y$）的任意阶偏导数。[自动微分](@entry_id:144512)是实现这一目标的核心机制。AD是一种计算技术，它能够以机器精度计算计算机程序所表示的函数的导数。与[符号微分](@entry_id:177213)（可能导致表达式爆炸）和[数值微分](@entry_id:144452)（引入截断和[舍入误差](@entry_id:162651)）不同，AD通过系统地应用[链式法则](@entry_id:190743)来计算精确的导数。

对于一个[前馈神经网络](@entry_id:635871)，它可以看作是一系列仿射变换和[非线性激活函数](@entry_id:635291)的复合。AD能够通过遍历这个[计算图](@entry_id:636350)来传播导数值。计算高阶导数，例如[泊松方程](@entry_id:143763)中的 $\frac{\partial^2 u_\theta}{\partial x^2}$，可以通过嵌套使用AD来实现。例如，可以先计算[一阶导数](@entry_id:749425) $\nabla u_\theta$，这本身是一个从 $\mathbb{R}^d$到 $\mathbb{R}^d$ 的映射，然后再次对这个映射应用AD来计算其[雅可比矩阵](@entry_id:264467)的某些分量，即 $u_\theta$ 的海森矩阵（Hessian matrix）的分量。现代深度学习框架（如TensorFlow和PyTorch）都内置了高效的AD功能。

一个高效的策略是所谓的**前向-反向混合模式AD**（forward-over-reverse mode AD）。首先，通过一次反向模式AD（也称反向传播），我们可以高效地计算出标量输出函数 $u_\theta$ 的完整梯度 $\nabla u_\theta$。然后，为了计算[海森-向量积](@entry_id:635156)（Hessian-vector product）$H(\boldsymbol{x})\boldsymbol{v}$，我们对梯度映射 $\boldsymbol{x} \mapsto \nabla u_\theta(\boldsymbol{x})$ 应用一次前向模式AD，并以 $\boldsymbol{v}$ 作为种子向量。例如，要计算 $\frac{\partial^2 u_\theta}{\partial x_i^2}$ 和 $\frac{\partial^2 u_\theta}{\partial x_i \partial x_j}$，我们只需计算[海森矩阵](@entry_id:139140)的第 $i$ 列，即 $H(\boldsymbol{x})\boldsymbol{e}_i$（其中 $\boldsymbol{e}_i$ 是[标准基向量](@entry_id:152417)）。这只需要一次前向-反向混合模式的计算，其计算成本与几次网络的[前向传播](@entry_id:193086)相当，而无需显式构造整个海森矩阵 [@problem_id:3431058]。

#### [网络架构](@entry_id:268981)：正则性要求

由于强形式PINN需要在[配置点](@entry_id:169000)上对PDE残差进行逐点评估，因此[神经网](@entry_id:276355)络 $u_\theta$ 的**正则性**（即光滑性或[可微性](@entry_id:140863)）变得至关重要。一个 $m$ 阶的[微分算子](@entry_id:140145) $\mathcal{N}$ 要求其作用的函数至少是 $m$ 阶可微的。为了确保残差函数本身是连续且行为良好的，我们通常要求 $u_\theta \in C^m(\Omega)$，即 $u_\theta$ 是 $m$ 阶连续可微的。

这一要求直接影响了[激活函数](@entry_id:141784)的选择 [@problem_id:3431055]。
- **光滑激活函数**：像[双曲正切](@entry_id:636446)（$\tanh$）、$\sin$ 或 $\text{swish}$ 这样的 $C^\infty$（无限次可微）[激活函数](@entry_id:141784)，当与[仿射变换](@entry_id:144885)复合时，产生的[神经网](@entry_id:276355)络 $u_\theta$ 也是 $C^\infty$ 的。这样的网络具有足够的正则性，能够表示任意高阶PDE的经典解。
- **非光滑激活函数**：相比之下，广泛使用的**[修正线性单元](@entry_id:636721)**（ReLU），即 $\text{ReLU}(z) = \max\{0, z\}$，仅是 $C^0$ 连续的。其一阶导数是分段常数（不连续），而其[二阶导数](@entry_id:144508)在经典意义上[几乎处处](@entry_id:146631)为零，在“[拐点](@entry_id:144929)”处未定义。如果用[ReLU网络](@entry_id:637021)来求解[二阶PDE](@entry_id:175326)（如[泊松方程](@entry_id:143763)），AD在几乎所有点上计算出的[二阶导数](@entry_id:144508)都将为零。这将导致网络无法学习具有非零曲率的解，因为残差中的[二阶导数](@entry_id:144508)项被错误地表示为零。

因此，对于求解高阶PDE的强形式PINN，选择足够光滑的[激活函数](@entry_id:141784)是理论上和实践上的必要条件。

### 边界条件的处理

如何精确有效地施加边界条件是PDE数值求解的核心挑战之一。在PINN框架中，主要有两种策略：软约束和硬约束 [@problem_id:3431031]。

#### 软约束（Soft Enforcement）

软约束是通过在损失函数中增加一个惩罚项来实现的，这也是我们在前面的[泊松方程](@entry_id:143763)示例中采用的方法。边界损失项 $L_b(\theta)$ 衡量了网络在边界[配置点](@entry_id:169000)上对给定边界条件的违反程度。这种方法的优点在于其通用性和实现的简便性。它不改变[网络架构](@entry_id:268981)，可以应用于各种类型的边界条件（狄利克雷、诺伊曼、罗宾等）。

然而，软约束也引入了挑战。它增加了一个或多个需要仔细调整的超参数（如 $\lambda_b$），用于平衡不同损失项。如果权重选择不当，可能会导致训练过程不稳定或收敛到不能很好满足边界条件的解。从约束优化的角度看，软约束是一种**罚函数法**。理论上，只有当惩罚权重 $\lambda_b \to \infty$ 时，才能保证边界条件被精确满足。在实践中，过大的 $\lambda_b$ 会使[损失函数](@entry_id:634569)变得病态，导致优化困难。

#### 硬约束（Hard Enforcement）

硬约束通过修改[神经网](@entry_id:276355)络的函数形式，使其**通过构造**（by construction）来精确满足边界条件。这意味着对于任何参数 $\theta$，近似解 $u_\theta$ 都自动满足边界条件。这样，边界损失项 $L_b$ 就可以从总[损失函数](@entry_id:634569)中移除，优化器只需专注于最小化内部PDE残差。

对于狄利克雷边界条件 $u|_{\partial\Omega} = g$，一个常见的硬约束构造是：
$$
u_\theta(\boldsymbol{x}) = g(\boldsymbol{x}) + d(\boldsymbol{x}) N_\theta(\boldsymbol{x})
$$
其中 $N_\theta(\boldsymbol{x})$ 是一个标准的[神经网](@entry_id:276355)络，而 $d(\boldsymbol{x})$ 是一个已知的、在边界 $\partial\Omega$ 上为零但在域内部 $\Omega$ 非零的函数。例如，$d(\boldsymbol{x})$ 可以是点 $\boldsymbol{x}$ 到边界的（符号）距离函数。当 $\boldsymbol{x} \in \partial\Omega$ 时，$d(\boldsymbol{x})=0$，因此 $u_\theta(\boldsymbol{x}) = g(\boldsymbol{x})$，边界条件被精确满足。

硬约束的优点是消除了边界损失项和相关的权重超参数，简化了损失函数景观。然而，它也有缺点。首先，这种构造需要一个解析的边界函数 $g(\boldsymbol{x})$ 和距离函数 $d(\boldsymbol{x})$，这在复杂几何域中可能难以获得。其次，对 $u_\theta$ 应用[微分算子](@entry_id:140145) $\mathcal{N}$ 时，需要通过链式法则对乘积项 $d(\boldsymbol{x}) N_\theta(\boldsymbol{x})$ 求导，这可能产生更复杂的表达式，有时会给优化带来新的困难。最后，硬约束限制了[神经网](@entry_id:276355)络的[假设空间](@entry_id:635539)，如果真实解的结构与所选构造形式不匹配，可能会影响模型的[表达能力](@entry_id:149863)。

### 训练的挑战与策略

将PDE求解转化为[优化问题](@entry_id:266749)后，PINN的成功在很大程度上取决于我们能否有效地最小化其高度非凸的[损失函数](@entry_id:634569)。这一过程面临诸多挑战，也催生了相应的解决策略。

#### [多目标优化](@entry_id:637420)视角

PINN的训练本质上是一个**[多目标优化](@entry_id:637420)问题** [@problem_id:3431056]。每个损失项（PDE残差、边界条件、[初始条件](@entry_id:152863)等）都可以被视为一个独立的目标。加权和[损失函数](@entry_id:634569) $L(\theta) = \lambda_r L_r(\theta) + \lambda_b L_b(\theta)$ 是解决这类问题的一种常用[标量化](@entry_id:634761)方法。不同的权重 $(\lambda_r, \lambda_b)$ 选择对应于在不同目标之间进行不同权衡的解，这些解构成了所谓的**帕累托前沿**（Pareto front）。

一个核心的挑战是，不同的损失项可能具有截然不同的量级和梯度范数。例如，涉及高阶导数的PDE残差 $L_r$ 的值可能比边界残差 $L_b$ 小几个[数量级](@entry_id:264888)，但其梯度 $\nabla_\theta L_r$ 可能要大得多。如果使用固定的、未经仔细调整的权重，总梯度 $\nabla_\theta L = \lambda_r \nabla_\theta L_r + \lambda_b \nabla_\theta L_b$ 可能会被其中一个项完全主导。这会导致优化器只关注降低一个目标的损失，而忽略了其他目标，最终导致训练失败。例如，网络可能很好地拟合了边界条件，但在域内部却严重违反PDE。

为了应对这种梯度病理学，研究人员提出了多种策略，包括对变量进行无量纲化、使用自适应权重算法（如基于梯度范数平衡或[不确定性加权](@entry_id:635992)的方法）以及采用真正的[多目标优化](@entry_id:637420)算法。

#### 优化器的选择

在实践中，优化器的选择对PINN的训练效果有显著影响 [@problem_id:3431013]。两种最常用的优化器是Adam和[L-BFGS](@entry_id:167263)。

- **Adam** (Adaptive Moment Estimation) 是一种基于梯度一阶和[二阶矩估计](@entry_id:635769)的[随机梯度下降](@entry_id:139134)变体。它对[梯度噪声](@entry_id:165895)具有鲁棒性，在训练初期能快速探索[损失函数](@entry_id:634569)景观，非常适合与**小批量随机梯度**（stochastic mini-batching）结合使用。当[配置点](@entry_id:169000)数量巨大（数百万或更多）时，计算全批量梯度成本高昂，此时Adam和mini-batching是首选。
- **[L-BFGS](@entry_id:167263)** (Limited-memory Broyden–Fletcher–Goldfarb–Shanno) 是一种**[拟牛顿法](@entry_id:138962)**。它通过存储最近几次迭代的梯度和参数变化来近似[海森矩阵](@entry_id:139140)的逆，从而能够利用二阶曲率信息进行优化。对于光滑、确定性的全批量[损失函数](@entry_id:634569)，[L-BFGS](@entry_id:167263)通常比一阶方法（如Adam）收敛得更快、更精确，因为它能更有效地处理[PINN损失函数](@entry_id:137288)中常见的病态（ill-conditioned）曲率。然而，标准的[L-BFGS](@entry_id:167263)对[梯度噪声](@entry_id:165895)非常敏感，直接与随机小批量一起使用时性能会急剧下降，因为噪声会破坏其对曲率的精确估计。

一个非常有效且流行的**混合策略**是：在训练初期使用Adam（通常配合mini-batch）进行快速的全局探索，找到一个有希望的损失盆地；然后，切换到全批量的[L-BFGS](@entry_id:167263)进行精细的局部优化，以达到更高的精度。这种策略结合了两种优化器的优点，是训练PINN的强大实用技巧。

### 高级主题与局限性

除了上述基本原理，PINN的性能还受到一些更深层次因素的影响，理解这些局限性对于成功应用PINN至关重要。

#### 谱偏差与傅里叶特征

标准的[神经网](@entry_id:276355)络在训练中表现出强烈的**谱偏差**（spectral bias），即它们会优先学习[目标函数](@entry_id:267263)的低频分量，而学习高频分量的速度则慢得多 [@problem_id:3430997]。对于具有[振荡](@entry_id:267781)或多尺度解的PDE（例如高[波数](@entry_id:172452)的亥姆霍兹方程），这种偏差是一个严重障碍。网络可能需要极长的时间才能捕捉到解中的高频细节，甚至完全失败。

为了克服谱偏差，一种有效的技术是使用**傅里叶特征**（Fourier features）或**位置编码**（positional encoding）。其思想是在将坐标 $\boldsymbol{x}$ 输入网络之前，先通过一个[非线性映射](@entry_id:272931) $\gamma(\boldsymbol{x})$ 进行变换。一个常见的选择是：
$$
\gamma_B(\boldsymbol{x}) = [\sin(2\pi B \boldsymbol{x}), \cos(2\pi B \boldsymbol{x})]
$$
其中 $B$ 是一个频率带参数矩阵。通过这个映射，输入坐标被投影到一组高频的正弦和余弦[基函数](@entry_id:170178)上。这使得网络可以更容易地通过对这些[基函数](@entry_id:170178)进行线性组合来构造高频函数，从而绕过了从头学习[高频模式](@entry_id:750297)的困难。

傅里叶特征的成功取决于两个条件：首先，频率带 $B$ 的选择需要与待求解问题中的主导频率相匹配。其次，[配置点](@entry_id:169000)的密度必须足够高，以满足**[奈奎斯特采样定理](@entry_id:268107)**。如果特征的频率超出了[配置点](@entry_id:169000)网格所能解析的范围，就会发生**[混叠](@entry_id:146322)**（aliasing），导致残差计算错误，从而破坏训练过程。当解包含广泛的[频率谱](@entry_id:276824)时，可以使用多个频率带，这种方法类似于随机傅里叶特征（Random Fourier Features），可以显著提升PINN学习宽带函数的能力。

#### [泛化误差](@entry_id:637724)之谜

在机器学习中，一个核心问题是模型在训练数据上的表现（[训练误差](@entry_id:635648)）能否推广到未见过的数据上（[泛化误差](@entry_id:637724)）。对于PINN，这意味着：在[配置点](@entry_id:169000)上的小残差是否保证了在整个域上的解都是精确的？答案是否定的，原因有二 [@problem_id:3430984]。

1.  **[假设空间](@entry_id:635539)的复杂度**：从[统计学习理论](@entry_id:274291)的角度看，[泛化误差](@entry_id:637724)由[训练误差](@entry_id:635648)和一个与模型**复杂度**相关的项共同决定。PINN的损失函数涉及微分算子，而[微分](@entry_id:158718)会“放大”函数的复杂性。这意味着PINN的残差函数类（即所有可能的残差函数构成的集合）可能比网络函数类本身要复杂得多。这种被放大的复杂度意味着需要非常大量的[配置点](@entry_id:169000)才能保证训练残差和真实期望残差之间有很小的差距。因此，即使在少量[配置点](@entry_id:169000)上达到了零残差，也不能排除残差函数在点与点之间剧烈[振荡](@entry_id:267781)的可能性。

2.  **[采样策略](@entry_id:188482)的偏差**：标准的[泛化界](@entry_id:637175)衡量的是在某个数据[分布](@entry_id:182848) $\mathbb{P}$ 下的**平均**误差。如果[配置点](@entry_id:169000)的[采样分布](@entry_id:269683) $\mathbb{P}$ 未能充分覆盖解的关键区域（如[边界层](@entry_id:139416)、激波或高梯度区），那么即使平均误差很小，在这些[欠采样](@entry_id:272871)区域的**逐点误差**也可能非常大。这对于[科学计算](@entry_id:143987)应用来说是致命的，因为我们通常关心的是解在所有地方都精确，而不仅仅是平均意义上的精确。因此，开发能够自适应地在残差大的区域增加采样点的策略，对于提高PINN的可靠性至关重要。

#### [变分PINN](@entry_id:756443) (vPINN)

为了缓解强形式PINN对解和网络架构正则性的严格要求，研究人员提出了**[变分物理信息神经网络](@entry_id:756443)**（Variational PINNs, vPINNs）[@problem_id:3431039]。vPINN基于PDE的**弱形式**或**[变分形式](@entry_id:166033)**，这与有限元方法（FEM）的思想一脉相承。

其核心步骤是通过与一个**测试函数** $\varphi$ 相乘并在域上积分，然后应用**[分部积分](@entry_id:136350)**（或[格林恒等式](@entry_id:176369)）。对于一个二阶算子，如 $-\nabla \cdot (a \nabla u)$，[分部积分](@entry_id:136350)可以将一个导数从待求函数 $u$ 转移到测试函数 $\varphi$ 上：
$$
\int_{\Omega} (-\nabla \cdot (a \nabla u)) \varphi \, d\boldsymbol{x} = \int_{\Omega} a \nabla u \cdot \nabla \varphi \, d\boldsymbol{x} - \int_{\partial\Omega} \varphi (a \nabla u \cdot \boldsymbol{n}) \, dS
$$
观察右侧的积分项，我们发现对 $u_\theta$ 的导数要求从二阶降至一阶。这意味着近似解 $u_\theta$ 只需要是 $H^1$ 空间的函数即可，而不是强形式所要求的 $H^2$。这种放宽的正则性要求为网络架构的选择提供了更大的灵活性。

vPINN的代价是，其损失函数不再是简单的点态残差评估，而是需要计算积分。这些积分必须通过**数值积分**（numerical quadrature）来近似，例如使用[高斯积分法](@entry_id:178260)。尽管这增加了实现的复杂性，但vPINN在处理某些问题时，尤其是在解的正则性较低时，展现出了优于标准PINN的稳定性和准确性。