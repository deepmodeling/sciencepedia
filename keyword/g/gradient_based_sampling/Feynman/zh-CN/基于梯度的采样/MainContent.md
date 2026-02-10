## 引言
在许多科学和计算问题中，仅仅找到唯一的最佳解是不够的。我们需要的不仅仅是定位广阔景观中最低的山谷，而是要绘制出整个地形图——包括所有可能的低能量区域、山脊和盆地。这种从简单优化到全面探索的转变带来了一个重大挑战：我们如何才能在这些复杂的高维空间中导航，而不会陷入我们找到的第一个山谷？答案在于将通常用作下降工具的普通梯度，转变为一种精巧的探索向导。

本文深入探讨了功能强大的基于梯度的[采样方法](@keyword=sampling_methods|lang=zh-CN|style=Feynman)系列。它通过展示一点随机性和一些物理学知识如何将下坡滑动转变为智能探索策略，从而弥合了优化与采样之间的鸿沟。您将学习到这些技术如何使我们能够从复杂的[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)中生成[代表性样本](@keyword=representative_sample|lang=zh-CN|style=Feynman)，这是现代科学技术中的一项关键任务。

以下各节将首先解析核心的“原理与机制”，解释像Langevin Dynamics和Hamiltonian Monte Carlo这样的方法如何利用梯度进行探索，以及我们甚至如何能直接从数据中学习梯度。然后，我们将遍览“应用与跨学科联系”，探索这一思想如何成为[生成式人工智能](@keyword=generative_ai|lang=zh-CN|style=Feynman)、[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)、[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)领域突破的驱动力，甚至为我们审视生命本身提供了一个全新的视角。

## 原理与机制

想象一下，你正站在一片广阔、丘陵起伏且被浓雾笼罩的景观中。你的目标不仅仅是找到最低的山谷，而是要绘制出整个地形图——所有的山谷、山脊和盆地——以了解哪些区域是最常见的地带。你唯一的工具是一个高度计，它还能告诉你脚下的斜率，即**梯度**。这个指向最陡峭上升方向的简单工具，是探索复杂高维空间的一系列优美而强大方法的起点：基于梯度的采样。

### 下坡路径的诱惑

在数学和计算机科学的世界里，这种景观通常是一个“[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)”或一个“[损失函数](@keyword=loss_functions|lang=zh-CN|style=Feynman)”。对于一个优化任务，比如训练一个[机器学习模型](@keyword=machine_learning_models|lang=zh-CN|style=Feynman)，目标很简单：沿着负梯度——即最陡峭*下降*的方向——到达最低点，也就是最小损失。这是一种纯粹的局部策略；你只利用当前位置的斜率信息来决定下一步的走向[@problem_id:2156666]。

但是，如果仅仅找到唯一的最低点还不够呢？考虑一个像dodecane这样的长而柔性的分子，它可以扭曲和折叠成数量惊人的不同形状，或称“构象”。每种形状都有一个对应的势能。虽然有一种形状是最稳定的（全局能量最低），但在室温下，该分子会停留在一整套低能量形状的集合中。要理解其化学行为，我们需要知道这些常见的形状是什么，以及每种形状的概率有多大。我们需要绘制整个低能量景观图，而不仅仅是找到最深的坑 [@problem_id:2460666]。这是一项**采样**任务，而非优化任务。我们希望从一个[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)中收集[代表性样本](@keyword=representative_sample|lang=zh-CN|style=Feynman)，在物理学中，这通常是**[玻尔兹曼分布](@keyword=boltzmann_distribution|lang=zh-CN|style=Feynman)** (Boltzmann distribution)，$p(x) \propto \exp(-U(x))$，其中 $U(x)$ 是状态 $x$ 的势能。高概率对应于低能量。

我们的梯度跟随工具在这里能帮上什么忙呢？如果我们只是沿坡下滑，我们会被困在找到的第一个山谷里。我们需要一种方法来爬出山谷，探索整个景观。关键在于，也许有些违反直觉，那就是增加一点随机性。

### 从优化到探索：[抖动](@keyword=dithering|lang=zh-CN|style=Feynman)的艺术

让我们暂时回到优化的世界。在庞大的数据集上训练机器学习模型时，计算所有数据点的真实梯度速度太慢。因此，我们通常使用**[小批量梯度下降](@keyword=minibatch_gradient_descent|lang=zh-CN|style=Feynman)法** (Mini-Batch Gradient Descent)，在每一步中使用一个随机的数据[子集](@keyword=subset|lang=zh-CN|style=Feynman)来估计梯度。这导致我们的参数不会沿着平滑、直接的路径走向最小值，而是会遵循一条嘈杂的“之”字形轨迹。路径会[抖动](@keyword=dithering|lang=zh-CN|style=Feynman)和[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)，但总体趋势仍然是向下的 [@problem_id:2186994]。

对于优化而言，这种[抖动](@keyword=dithering|lang=zh-CN|style=Feynman)是一种副作用，有时它能帮助我们跳出浅层的局部最小值，算是有益的。但对于采样而言，这种[抖动](@keyword=dithering|lang=zh-CN|style=Feynman)才是主角！它是一个想法的萌芽：我们可以刻意在梯度跟随过程中加入噪声来探索景观。这就是**Langevin Dynamics**的精髓。

想象一个浸在流体中的微小粒子，在我们的[能量景观](@keyword=energy_landscape|lang=zh-CN|style=Feynman)上移动。这个粒子感受到两种力。首先，它感受到来自景观本身的确定性拉力，这个力等于负梯度 $-\nabla U(x)$，将它拖向更低的能量区域。其次，它不断受到流体分子随机热运动的撞击。这些无数微小的碰撞表现为一种随机的“踢动”力。粒子的运动是在系统性的下坡拉力和这些随机踢动之间的一支舞。这种舞蹈的连续时间数学描述就是[Langevin方程](@keyword=langevin_equation|lang=zh-CN|style=Feynman)：
$$
d\theta_t = -\nabla U(\theta_t) dt + \sqrt{2T} dW_t
$$
在这里，$\theta_t$ 是粒子的位置，$-\nabla U(\theta_t)$ 是来自势能的力，而项 $\sqrt{2T}dW_t$ 代表随机热扰动，其中 $T$ 是温度，$dW_t$ 是[高斯白噪声](@keyword=gaussian_white_noise|lang=zh-CN|style=Feynman)。神奇之处在于，如果你让这个过程持续运行，粒子访问过的位置集合将构成一个完美的样本，其[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)遵循玻尔兹曼分布 $p(\theta) \propto \exp(-U(\theta)/T)$。随机噪声提供了恰到好处的能量，足以将粒子踢出局部最小值并探索整个空间，同时倾向于在低能量区域花费更多时间。

**随机梯度[Langevin动力学](@keyword=langevin_dynamics|lang=zh-CN|style=Feynman) (SGLD)** 是将这种物理直觉付诸实践的算法。在每一步，我们通过向负梯度方向迈出一小步（就像在[梯度下降](@keyword=gradient_descent|lang=zh-CN|style=Feynman)中一样）来更新我们的位置，然后添加少量经过正确缩放的[高斯噪声](@keyword=gaussian_noise|lang=zh-CN|style=Feynman)。如果梯度本身是带噪声的（因为我们使用的是小批量数据），那也没关系——它只会被整合到整体的随机动态中。通过仔细平衡梯度步长和注入的噪声，我们将一个优化器变成了一个强大的采样器。

此外，我们还可以使这个过程更加高效。如果我们的景观是一个狭长的峡谷，一个简单的下坡步骤是无效的。它只会在峡谷壁之间来回反弹。通过使用**预条件矩阵** (preconditioning matrix)，我们基本上可以重新缩放空间的几何结构，将狭窄的峡谷变成一个圆形的碗，其中“下坡”方向更直接地指向底部。这在数学上等同于在一个变换后的空间中进行简单的[随机游走](@keyword=random_walk|lang=zh-CN|style=Feynman)，而在这个空间里景观的性状更好[@problem_id:3291218]。

### Hamiltonian Monte Carlo：完美投掷的艺术

[Langevin动力学](@keyword=langevin_dynamics|lang=zh-CN|style=Feynman)通过随机、[抖动](@keyword=dithering|lang=zh-CN|style=Feynman)的行走来探索景观。而**Hamiltonian Monte Carlo (HMC)**则借鉴了经典力学中一个深刻而优美的思想，提供了一种更优雅且通常效率高得多的解决方案 [@problem_id:3547147]。

想象一个无摩擦的滑冰者或[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)中的卫星，而不是流体中的粒子。为了探索景观 $U(\theta)$，我们不只是让它滑行。我们给它一个随机的推动——也就是说，我们赋予它一个随机的**动量** $r$。系统的总能量现在由一个**[哈密顿量](@keyword=hamiltonian_function|lang=zh-CN|style=Feynman)** (Hamiltonian) $H(\theta, r)$ 描述，它是势能 $U(\theta)$ 和动能 $K(r) = \frac{1}{2}r^\top M^{-1} r$ 的总和。

现在，我们让滑冰者滑行。由于[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)，当滑冰者移动到势能更高的区域（上坡）时，它会减速（动能减少）；而当它进入山谷时，它会加速。其轨迹由[哈密顿运动方程](@keyword=hamilton_s_equations_of_motion|lang=zh-CN|style=Feynman)决定，其中的力由[势能的梯度](@keyword=gradient_of_potential_energy|lang=zh-CN|style=Feynman) $-\nabla_\theta U(\theta)$ 决定。因为没有[摩擦力](@keyword=friction_force|lang=zh-CN|style=Feynman)，滑冰者可以滑行很长距离，在一次平滑的运动中穿越景观的大部分区域。

在HMC中，我们从一个点 $\theta$ 开始，抽取一个随机动量 $r$，然后模拟这个[哈密顿动力学](@keyword=hamiltonian_dynamics|lang=zh-CN|style=Feynman)一段固定的时间，以提出一个新的点 $\theta'$。因为这个模拟完美地保持了总能量，它探索景观的效率远高于[Langevin动力学](@keyword=langevin_dynamics|lang=zh-CN|style=Feynman)的小而随机的步长。在实践中，我们使用一种称为**[蛙跳法](@keyword=leap_frog_method|lang=zh-CN|style=Feynman)** (leapfrog method) 的数值积分器来模拟动力学过程。这种方法会在总能量上产生微小误差，我们通过最后的接受/拒绝步骤来修正这些误差，从而确保我们的样本精确地来自正确的目标分布。HMC是物理学与统计学统一的绝佳范例，它利用经典力学的机制来解决一个现代计算问题。

### 看不见的梯度：从数据中学习景观

所有这些方法都依赖于一个关键要素：对数概率的梯度 $\nabla \log p(\theta)$，我们一直称之为[势能梯度](@keyword=potential_energy_gradient|lang=zh-CN|style=Feynman) $-\nabla U(\theta)$。如果我们没有 $p(\theta)$ 的公式怎么办？如果我们只有从中抽取的样本——例如，一个庞大的人脸图像数据集——我们还能进行基于梯度的采样吗？

令人惊讶的是，答案是肯定的，这要归功于采样与**去噪** (denoising) 之间深刻而出人意料的联系 [@problem_id:3442907]。梯度场 $\nabla \log p(\theta)$ 通常被称为**[分数函数](@keyword=score_function|lang=zh-CN|style=Feynman)** (score function)。事实证明，你可以通过训练一个[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络来学习这个[分数函数](@keyword=score_function|lang=zh-CN|style=Feynman)，任务非常简单：接收一张带噪声的图像，并学会去除噪声。

这个结果是[Tweedie公式](@keyword=tweedie_s_formula|lang=zh-CN|style=Feynman)的一种形式，它指出，被高斯噪声轻微模糊的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)的分数与最优去噪器直接相关。具体来说，如果你有一个带噪声的样本 $y = x + \text{noise}$，那么在 $y$ 点的分数与 $(\mathbb{E}[x|y] - y)$ 成正比，这是对 $x$ 的最优去噪估计与带噪声输入 $y$ 之间的差值。换句话说，在[概率空间](@keyword=probability_space|lang=zh-CN|style=Feynman)中指向“上坡”的向量，与去噪器用来清理图像的向量是相同的！

通过在我们的数据集上训练一个强大的去噪器，我们可以隐式地学习到基础数据[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)的[分数函数](@keyword=score_function|lang=zh-CN|style=Feynman)。然后，我们可以将这个学习到的[分数函数](@keyword=score_function|lang=zh-CN|style=Feynman)代入[Langevin动力学](@keyword=langevin_dynamics|lang=zh-CN|style=Feynman)中来生成新的样本。这使我们能够在复杂的科学问题中将基于梯度的采样用作先验，从而在数据驱动的景观理解指导下，生成现实的解决方案。

### 现实考量与梯度的[禁区](@keyword=forbidden_zone|lang=zh-CN|style=Feynman)

虽然这些想法很强大，但现实世界带来了挑战。
首先，获取梯度并不总是那么容易。对于复杂的模型，例如描述生化网络的[微分方程](@keyword=differential_equation|lang=zh-CN|style=Feynman)，[计算模拟](@keyword=computational_simulation|lang=zh-CN|style=Feynman)输出对其参数的梯度是一项重大的工程壮举。这通常需要复杂的**伴随方法** (adjoint methods)——[可微编程](@keyword=differentiable_programming|lang=zh-CN|style=Feynman)的基石——来高效地完成 [@problem_id:3287526]。

其次，梯度仅在连续空间上定义。如果我们的景观是离散的，比如所有可能的二值图像空间，该怎么办？我们无法沿坡下滑；我们必须从一个离散状态跳到另一个。在这种情况下，梯度的概念就失效了，我们必须转向无梯度方法，如Metropolis-Hastings，它提议随机的“位翻转”而不是梯度步。或者，可以使用巧妙的“连续松弛”方法，用一个平滑空间来近似[离散空间](@keyword=discrete_space|lang=zh-CN|style=Feynman)，从而使梯度能够重新发挥作用，尽管会带有一些近似误差 [@problem_id:3122300]。

最后，在实现这些方法时有一条微妙但至关重要的规则：随机性的来源必须是神圣不可侵犯的。当我们使用[随机数生成器](@keyword=random_number_generators|lang=zh-CN|style=Feynman)（RNG）在[Langevin动力学](@keyword=langevin_dynamics|lang=zh-CN|style=Feynman)中提供热扰动或在HMC中提供初始动量时，我们必须确保我们的[自动微分](@keyword=automatic_differentiation|lang=zh-CN|style=Feynman)软件不会试图*穿过*RNG计算梯度。支撑这些方法的数学恒等式要求随机数独立于模型参数。试图对RNG进行[微分](@keyword=pushforward|lang=zh-CN|style=Feynman)在计算上是无稽之谈——其底层的整数运算是不可微的——在统计上也是错误的。这就像试图在开奖后通过改变彩票规则来找到一张“更好”的彩票。正确的做法是将随机数视为可微计算部分的固定输入，以确保过程的完整性 [@problem_id:3511474]。

从简单的下坡滑动到模拟哈密顿物理，基于梯度的[采样方法](@keyword=sampling_methods|lang=zh-CN|style=Feynman)将普通的梯度从一个寻找最低点的工具，转变为一个探索世界上最复杂、最迷人景观的精巧向导。

