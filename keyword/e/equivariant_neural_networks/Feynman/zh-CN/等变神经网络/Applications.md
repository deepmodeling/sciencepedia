## 应用与跨学科联系

在我们之前的旅程中，我们已经探讨了“如何做”——即那些让我们能够构建理解三维空间对称性的[神经网络](@keyword=neural_networks|lang=zh-CN|style=Feynman)的原理和数学工具。我们构建的函数，其变换方式，从设计之初就与其所模拟的物理世界协同一致。但是，一件精美的机械只有在实际应用中才能真正被欣赏。现在，我们转向“为什么”和“在哪里”。为什么要费这么大功夫？这个想法又在哪些领域产生了影响？

你可能已经有了一些直觉。如果一个物理定律是正确的，它不会因为你碰巧转了一下头就变得错误。物理定律对于我们选择的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)是不变的。因此，任何旨在学习这些定律的[计算模型](@keyword=models_of_computation|lang=zh-CN|style=Feynman)，都应该将这一原则深深地根植于其灵魂之中，这似乎是显而易见的。多年来，机器学习的标准方法是暴力破解：给模型看一个分子，然后是同一个分子的旋转版本，再一个，又一个，希望它最终能“明白”它们都是同一个物体。然而，一个[等变网络](@keyword=equivariant_networks|lang=zh-CN|style=Feynman)不需要被这样教导。它从一开始就*知道*这一点。这一个强大而单一的想法，解锁了众多令人惊叹的应用，在[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)、[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)乃至新药设计之间建立了联系。

### 问题的核心：模拟原子的舞蹈

[等变网络](@keyword=equivariant_networks|lang=zh-CN|style=Feynman)最自然、影响最深远的应用或许是在原子和分子的世界里。这是[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)和[分子物理学](@keyword=molecular_physics|lang=zh-CN|style=Feynman)的领域，在这里，理解物质的行为始于理解其组成粒子之间的力。

想象一个分子。它不是一个静态的物体，而是一个动态的实体，其原子在复杂的[量子力学力](@keyword=quantum_mechanical_forces|lang=zh-CN|style=Feynman)的推拉下不断[振动](@keyword=oscillation|lang=zh-CN|style=Feynman)。理解这场舞蹈的关键是*[势能面](@keyword=potential_energy_surface|lang=zh-CN|style=Feynman)*，这是一个函数$E(\mathbf{R})$，它为原子的每一种可能的空间[排列](@keyword=permutation|lang=zh-CN|style=Feynman)$\mathbf{R}$赋予一个标量能量值。如果我们知道这个函数，我们就知道了一切。分子最稳定的形状是使该能量最小化的形状。更重要的是，每个原子上的力就是这个表面上的“下坡”方向——能量的负梯度，$\mathbf{F}(\mathbf{R}) = -\nabla_{\mathbf{R}}E(\mathbf{R})$。

奇迹就发生在这里。一个[等变网络](@keyword=equivariant_networks|lang=zh-CN|style=Feynman)可以被训练来从数据中学习能量函数$E(\mathbf{R})$。因为能量是一个标量，如果我们旋转或平移整个分子，它不应该改变。我们的[网络架构](@keyword=network_architecture|lang=zh-CN|style=Feynman)，如果被构造成输出一个不变的标量，就能保证这一点。然后，借助[自动微分](@keyword=automatic_differentiation|lang=zh-CN|style=Feynman)的力量——也就是用来训练网络的同一个“[反向传播](@keyword=backpropagation|lang=zh-CN|style=Feynman)”[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)——我们可以计算出学习到的能量函数相对于原子位置的梯度。这免费地给了我们力$\mathbf{F}$！而且因为我们是从一个势能中推导出它们，这些力被保证是物理上一致的（物理学家称之为*[保守场](@keyword=conservative_fields|lang=zh-CN|style=Feynman)*）。这个过程提供了一种极其快速和准确的方式来运行[分子动力学模拟](@keyword=molecular_dynamics_simulations|lang=zh-CN|style=Feynman)，使我们能够观察分子在远超传统[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)方法所能及的时间尺度上移动、折叠和反应[@problem_id:2903791]。

但故事并没有在能量和力这里结束。分子还有其他同样重要的性质。原子核周围的电子云并非总是完美[均匀分布](@keyword=uniform_distribution|lang=zh-CN|style=Feynman)。这种不对称性产生了一个*电偶极矩*$\boldsymbol{\mu}$，一个从负电荷中心指向正电荷中心的微小向量。这个向量对于理解分子之间以及分子与电场如何相互作用至关重要。一个输出头被设计为产生向量的[等变网络](@keyword=equivariant_networks|lang=zh-CN|style=Feynman)，可以直接从分子的几何结构中学习预测偶极矩。根据其构造，如果我们旋转分子，模型预测的偶极矩向量将完美地随之旋转，就像真实的偶极矩一样[@problem_id:2903795]。

这种能力使我们能够探索化学中真正微妙的方面。考虑一个*手性*分子——它存在“左手”和“右手”两种形式，互为镜像，就像你的双手一样。一个重要的问题是这种分子是否可以有偶极矩。一个具有反演[对称中心](@keyword=center_of_inversion|lang=zh-CN|style=Feynman)的相关分子，根据对称性，不能有偶极矩。然而，手性分子缺乏这种对称性，因此可以有偶极矩。一个建立在[正常旋转](@keyword=proper_rotation|lang=zh-CN|style=Feynman)和平移群$\mathrm{SE}(3)$上的[等变网络](@keyword=equivariant_networks|lang=zh-CN|style=Feynman)可以正确地捕捉到这一点！因为反射不是$\mathrm{SE}(3)$的元素，模型不被约束为对一个分子及其镜像给出相同的答案。这种自由度使其能够学习[对映异构体](@keyword=enantiomers|lang=zh-CN|style=Feynman)的不同物理性质，正确地预测对称构象异构体的偶极矩为零，而手性构象异构体的偶极矩非零[@problem_id:2903829]。这完美地展示了模型不仅能理解几何，还能理解立体化学对称性的深远后果。

我们甚至可以更进一步。分子如何与光相互作用，不仅取决于其静态偶极矩，还取决于其[电荷分布](@keyword=charge_distribution|lang=zh-CN|style=Feynman)在电场中如何*变形*。这个性质由*[极化率张量](@keyword=polarizability_tensor|lang=zh-CN|style=Feynman)*$\boldsymbol{\alpha}$（一个[2阶张量](@keyword=rank_2_tensor|lang=zh-CN|style=Feynman)）来描述。分子的[红外和拉曼光谱](@keyword=ir_and_raman_spectra|lang=zh-CN|style=Feynman)取决于偶极矩和[极化率张量](@keyword=polarizability_tensor|lang=zh-CN|style=Feynman)相对于[分子振动](@keyword=molecular_vibrations|lang=zh-CN|style=Feynman)的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)。[等变网络](@keyword=equivariant_networks|lang=zh-CN|style=Feynman)可以被设计用来预测这些高阶、依赖方向的量，为完全通过机器学习计算光谱性质开辟了新的前沿[@problem_id:2395448] [@problem_id:2898167]。

### 从原子到工程：材料的力学

支配单个分子的相同思想也适用于构成固体材料的巨大、有序的原子阵列。在固体力学领域，[等变性](@keyword=equivariance|lang=zh-CN|style=Feynman)原则有另一个名字：*材料框架无关性*或*客观性*。这是同样的概念：材料对变形的内部响应不能依赖于观察者的视角。

想象一下，试图创建一个数据驱动的模型，根据一小块区域内原子的[排列](@keyword=permutation|lang=zh-CN|style=Feynman)来预测材料的内部应力——一个[2阶张量](@keyword=rank_2_tensor|lang=zh-CN|style=Feynman)$\boldsymbol{\sigma}$。我们可以将这个局部原子邻域表示为一个图，并将其输入到一个[图神经网络](@keyword=graph_neural_networks|lang=zh-CN|style=Feynman)（GNN）中。如果我们不内置框架无关性，我们的模型可能会预测一块钢仅仅因为我们旋转了它而变弱。这在物理上是荒谬的。然而，一个等变GNN保证这种情况永远不会发生。通过使用作用于原子相对位置的等变层，网络可以学习一个从原子构型到应力张量的映射，这个映射在构造上就是客观的[@problem_id:2898860] [@problem_id:2629397]。

此外，许多材料并非在所有方向上都相同。木材沿纹理[方向比](@keyword=direction_ratios|lang=zh-CN|style=Feynman)横跨纹理方向更坚固。石英晶体具有特定的六边形结构，这决定了它的性质。这种方向依赖性称为*各向异性*。材料的性质并非在*所有*旋转下都对称，而只在其*[晶体学点群](@keyword=crystallographic_point_groups|lang=zh-CN|style=Feynman)*所形成的特定旋转集下对称。我们可以将这种专家知识赋予我们的网络。通过设计网络的滤波器和操作，使其不仅仅对整个$\mathrm{SO}(3)$群对称，而是只对材料的特[定点](@keyword=fixed_points|lang=zh-CN|style=Feynman)群——无论是立方、四面体还是其他——对称，我们就可以创建一个专门的模型，理解该特定材料独特的各向异性[@problem_id:2629397] [@problem_id:38643]。这是深度学习与有数百年历史的晶体学科学的深刻融合。

### 设计生命分子：药物发现

对称性和几何学的原则是普适的，从无机晶体的世界延伸到生命自身的复杂机器。现代医学和[生物信息学](@keyword=bioinformatics|lang=zh-CN|style=Feynman)的核心问题之一是药物发现，这通常可以归结为一个几何谜题：一个小药物分子（*配体*）如何装入一个大蛋白质（*受体*）的[活性位点](@keyword=active_site|lang=zh-CN|style=Feynman)？这个“锁和钥匙”问题被称为[分子对接](@keyword=molecular_docking|lang=zh-CN|style=Feynman)。

在这里，等变框架再次提供了一个强大而优雅的解决方案。我们可以创建一个模型，将蛋白质和配体都视为[三维几何](@keyword=3d_geometry|lang=zh-CN|style=Feynman)对象。使用等变GNN，该模型可以处理两个分子的完整三维结构，学习根据原子的化学性质和相对几何形状，生成原子对之间的相互作用分数。从这些分数中，可以构建一个在所有可能的结合姿态——即配体所有可能的位置和方向——的整个空间上的端到端可微*能量函数*。

自然的、最稳定的结合姿态是使该[能量最小化](@keyword=energy_minimization|lang=zh-CN|style=Feynman)的那一个。因为整个系统建立在等变基础上，所以给定姿态的预测能量与蛋白质-配体复合物在实验室[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)中的朝向无关。这使得模型能够纯粹关注相互作用的内在物理学。通过在已知的蛋白质-配体结构上训练这样一个模型，它学习了[分子识别](@keyword=molecular_recognition|lang=zh-CN|style=Feynman)的微妙几何和化学规则，使研究人员能够以前所未有的速度和准确性筛选数百万候选药物分子并预测它们的结合模式[@problem_id:2387789]。

### 训练的艺术：一种微妙的平衡

创建一个能够预测多种物理性质的模型是一项了不起的成就，但它也带来了自身的实际挑战。一个单一的[等变网络](@keyword=equivariant_networks|lang=zh-CN|style=Feynman)可以被训练来同时预测能量（一个标量）、力（一组向量）和偶极矩（一个向量）。这被称为*[多任务学习](@keyword=multi_task_learning|lang=zh-CN|style=Feynman)*，它非常强大，因为所有这些性质都源于分子的同一个底层[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)；将它们一起学习可以得到一个更稳健、更准确的模型。

然而，这些不同的任务涉及的量具有截然不同的尺度和单位。与力相关的数值损失可能比能量的损失大数千倍。如果我们天真地将这些损失相加，模型的训练将完全被力所主导，它可能永远学不会很好地预测能量。为了解决这个问题，可以使用一种称为*梯度归一化*的巧妙技术。在训练过程中，我们可以动态调整每个任务对网络共享部分更新的贡献权重。通过确保来自能量、力和偶极矩任务的梯度“信号”具有可比的幅度，我们确保模型对所有任务都给予同等关注。这就像主持一个委员会，确保每个声音，无论大小，都被平等地听到，从而做出一个平衡且信息充分的最终决定[@problem_id:2903832]。

从原子的精妙舞蹈到新材料和救生药物的设计，我们看到了一条统一的线索。通过将自然的根本原则——对称性——[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)我们计算工具的结构中，我们创造出的模型不仅更高效、更准确，而且更符合它们试图理解的物理现实。这便是等变[深度学习](@keyword=deep_learning|lang=zh-CN|style=Feynman)的承诺和深刻之美。