## 引言
标准的[机器学习模型](@keyword=machine_learning_models|lang=zh-CN|style=Feynman)是强大的[模式识别](@keyword=pattern_recognition|lang=zh-CN|style=Feynman)器，但它们通常像“黑箱”一样运作，对物理世界缺乏任何基本理解。这种知识差距可能导致预测在平均水平上准确，但却因违反[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)等基本定律而出现灾难性的失败。物理信息建模通过将经过时间考验的物理学原理嵌入到机器学习算法的架构和训练中，直接解决了这一局限。本文对这一变革性方法进行了全面综述。在第一章“原理与机制”中，我们将探讨用于赋予模型“物理良知”的核心技术，从修改损失函数到设计内蕴对称的架构。随后，“应用与跨学科联系”一章将展示这些方法如何给[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)、生物学和化学等不同领域带来革命，将预测工具转变为科学发现的合作伙伴。

## 原理与机制

想象一下，你正在教一个聪明但完全天真的学生宇宙的法则。这个学生可以记住海量信息，并以超人的能力发现模式，但没有任何先入为主的观念——没有关于世界如何运作的直觉。这本质上就是我们训练一个标准的[机器学习模型](@keyword=machine_learning_models|lang=zh-CN|style=Feynman)时所做的事情，这个模型就是一个由相互连接的节点和权重组成的“黑箱”。如果我们给它看数百万个苹果下落的视频，它可能在预测下一个苹果的轨迹方面变得极其出色。但如果你问它，如果一个苹果在月球上坠落会发生什么，或者一个苹果能否在半空中突然停下并反向运动，它可能会给你一个荒谬的答案。它学会了数据中的*相关性*，但没有学会其根本的*原因*——万有引力定律。

物理信息建模旨在超越这种天真的学习者。它的核心在于给我们的计算学生一张“备忘单”，上面写着几个世纪以来发现的基本原理：[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)、对称性、热力学定律。通过将这些知识直接融入学习过程，我们创造出的模型不仅更准确，而且更稳健、数据效率更高，并最终更符合它们试图描述的现实。

### 黑箱及其不满

让我们首先认识到我们试图解决的问题。一个标准的[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络是[通用函数逼近器](@keyword=universal_function_approximator|lang=zh-CN|style=Feynman)。只要有足够的数据和足够大的网络，它就可以学着逼近几乎任何[连续函数](@keyword=continuous_function|lang=zh-CN|style=Feynman)。但“几乎任何”是一个大到可怕的可能性空间，其中大多数在物理上都是荒谬的。

考虑一个[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)领域的真实任务：分析穆斯堡尔谱（Mössbauer spectroscopy）的[光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)数据，以确定含铁化合物的性质。一个纯数据驱动的[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络，在大型[光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)数据集上训练后，或许能学会预测我们关心的参数。然而，它也可能产生奇怪的失败。它可能预测出负的吸收强度，这就像说一种材料可以凭空创造光。它可能用不对称的峰来拟合一个磁性[光谱](@keyword=optical_spectra|lang=zh-CN|style=Feynman)，这违反了[原子核](@keyword=atomic_nucleus|lang=zh-CN|style=Feynman)的基本量子力学。或者它可能表明，不同位置的铁含量加起来不等于100%，这打破了简单的物质[守恒定律](@keyword=conservation_law|lang=zh-CN|style=Feynman)。这些并非假设性的缺陷，而是在忽略物理约束时常见的陷阱 [@problem_id:2501468]。

这个问题也延伸到了动力系统中。想象一下，训练一个[循环神经网络](@keyword=recurrent_neural_networks|lang=zh-CN|style=Feynman)（RNN）来根据一系列快照预测流体流动的演变。如果在一个稳定、低粘度的流动数据上进行训练，它可能能很好地学习短期动力学。但让它预测更长时间的流动，或者一个稍微不同的粘度，它可能会变得不稳定，预测系统的能量将指数级增长至无穷大——这明显违反了[Navier-Stokes方程](@keyword=navier_stokes_equation|lang=zh-CN|style=Feynman)中固有的[能量守恒](@keyword=conservation_of_energy|lang=zh-CN|style=Feynman)定律 [@problem_id:2432101] [@problem_id:3369176]。黑箱由于缺乏任何物理护栏，可以随意偏离物理上[可行解](@keyword=feasible_solution|lang=zh-CN|style=Feynman)的[流形](@keyword=manifold|lang=zh-CN|style=Feynman)。

### [物理信息](@keyword=physical_information|lang=zh-CN|style=Feynman)良知：在[损失函数](@keyword=loss_functions|lang=zh-CN|style=Feynman)中编码定律

赋予模型物理良知最直接的方法是修改它的“老师”——损失函数。损失函数在训练过程中告诉模型其预测有多错误。我们可以在这个函数中添加惩罚项，以惩罚任何违反已知物理定律的行为。

最常见的方法是使用控制方程本身。**物理信息神经网络（PINN）**就是这方面的一个绝佳例子。假设我们试图学习一个温度场 $u(x, t)$，我们知道它受热方程 $\partial_t u = \nu \nabla^2 u$ 控制。我们设计一个[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络，它以位置 $x$ 和时间 $t$ 为输入，输出一个预测的温度 $u_{\theta}(x, t)$。

PINN的[损失函数](@keyword=loss_functions|lang=zh-CN|style=Feynman)有两部分。第一部分是标准的[数据失配](@keyword=data_misfit|lang=zh-CN|style=Feynman)项：我们检查 $u_{\theta}$ 与我们拥有的实际温度测量值的匹配程度。第二部分，也是至关重要的部分，是**物理残差**。我们可以使用[自动微分](@keyword=automatic_differentiation|lang=zh-CN|style=Feynman)——[现代机器学习](@keyword=modern_machine_learning|lang=zh-CN|style=Feynman)中的一项关键技术——来计算网络输出的导数 $\partial_t u_{\theta}$ 和 $\nabla^2 u_{\theta}$，在任何空间和时间点上。然后，我们在[损失函数](@keyword=loss_functions|lang=zh-CN|style=Feynman)中对任何不满足[热方程](@keyword=heat_equation|lang=zh-CN|style=Feynman)的点，即 $\partial_t u_{\theta} - \nu \nabla^2 u_{\theta} \neq 0$ 的点，增加一个惩罚。通过在整个域中散布数千个这样的“[配置点](@keyword=collocation_points|lang=zh-CN|style=Feynman)”，我们迫使网络找到一个不仅拟合我们[稀疏数据](@keyword=sparse_data|lang=zh-CN|style=Feynman)，而且处处遵守该[偏微分方程](@keyword=partial_differential_equation|lang=zh-CN|style=Feynman)的解 [@problem_id:3301878] [@problem_id:3410569]。

有时，在每一点都强制执行一个[微分](@keyword=pushforward|lang=zh-CN|style=Feynman)定律过于严格或计算上困难。一种替代方法是以其积分形式强制执行一个**全局[守恒定律](@keyword=conservation_law|lang=zh-CN|style=Feynman)**。例如，在[固体力学](@keyword=solid_mechanics|lang=zh-CN|style=Feynman)中，[线性动量守恒](@keyword=conservation_of_linear_momentum|lang=zh-CN|style=Feynman)定律指出，对于一个处于静态平衡的物体，所有力的总和必须为零。这可以用Gauss散度定理来表示：物体表面的牵[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)（力）的积分必须与物体体积内的[体力](@keyword=body_forces|lang=zh-CN|style=Feynman)（如重力）的积分[相平衡](@keyword=phase_equilibrium|lang=zh-CN|style=Feynman)。我们可以构建一个损失项，计算预测应[力场](@keyword=force_field|lang=zh-CN|style=Feynman)的这两个积分，并惩罚任何不平衡。这确保了模型尊重全局平衡，即使局部方程有小误差 [@problem_id:3567167]。

物理学也为我们提供了强大的不等式。[热力学第二定律](@keyword=second_law_of_thermodynamics|lang=zh-CN|style=Feynman)，以**[Clausius-Duhem不等式](@keyword=clausius_duhem_inequality|lang=zh-CN|style=Feynman)**的形式，指出材料中[机械耗散](@keyword=mechanical_dissipation|lang=zh-CN|style=Feynman)的速率必须为非负。材料不能无中生有地创造能量。我们可以设计我们的材料行为模型——例如，一个从应变预测应力的[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络——来明确遵守这个定律。这是通过围绕一个[Helmholtz自由能](@keyword=helmholtz_free_energy|lang=zh-CN|style=Feynman)势和一个非负耗散势来构建模型实现的。这确保了任何模拟的材料都会表现出[热力学](@keyword=thermodynamics|lang=zh-CN|style=Feynman)上的一致性，这对于现实模拟来说是一个极其重要的约束 [@problem_id:3557096]。

### 内在的物理直觉：遵循定律的架构

因不良行为而惩罚模型是有效的，但设计一个*无法*产生不良行为的模型则更为优雅。这类似于将物理原理直接构建到模型的架构中，赋予其“内在的”物理直觉。

这里最有力的指导原则是**对称性**。物理定律与对称性密切相关。如果一个由相同分子组成的系统正在被建模，那么如果我们仅仅交换两个分子的标签，物理性质不应该改变。该系统在[置换](@keyword=permutation|lang=zh-CN|style=Feynman)下是对称的。那么为什么我们的模型不应该也是这样呢？我们可以设计明确具有**[置换](@keyword=permutation|lang=zh-CN|style=Feynman)[等变性](@keyword=equivariance|lang=zh-CN|style=Feynman)**的[神经网](@keyword=nerve_net|lang=zh-CN|style=Feynman)络。这意味着，如果你对输入进行[置换](@keyword=permutation|lang=zh-CN|style=Feynman)（例如，重新排序分子亚群的浓度），输出会以完全相同的方式进行[置换](@keyword=permutation|lang=zh-CN|style=Feynman)。这不仅仅是一个审美选择；它极大地约束了网络可以学习的函数类型。一个将 $n$ 个输入映射到 $n$ 个输出的通用线性层有 $n^2 + n$ 个参数。一个被强制为[置换](@keyword=permutation|lang=zh-CN|style=Feynman)[等变性](@keyword=equivariance|lang=zh-CN|style=Feynman)的等效层只有3个参数，无论 $n$ 是多少！通过构建这种物理对称性，我们大大缩小了[假设空间](@keyword=hypothesis_space|lang=zh-CN|style=Feynman)，使模型能够用少得多的数据进行更高效的学习 [@problem_id:3337998]。

一个类似的想法是**构造守恒**。如果我们知道一组化学物质的浓度总和必须是一个常数，我们可以设计网络的最后一层（例如，使用softmax函数）来保证这一属性，而不仅仅是在[损失函数](@keyword=loss_functions|lang=zh-CN|style=Feynman)中惩罚与它的偏差 [@problem_id:3301878]。

也许[经典物理学](@keyword=classical_physics|lang=zh-CN|style=Feynman)和[现代机器学习](@keyword=modern_machine_learning|lang=zh-CN|style=Feynman)最美丽的融合来自**[保结构积分器](@keyword=structure_preserving_integrators|lang=zh-CN|style=Feynman)**。几个世纪以来，物理学家们已经知道，在模拟[哈密顿系统](@keyword=hamiltonian_systems|lang=zh-CN|style=Feynman)（如[行星轨道](@keyword=planetary_orbits|lang=zh-CN|style=Feynman)或分子动力学）时，某些数值方法比其他方法更好。最好的那些，称为**[辛积分器](@keyword=symplectic_integrators|lang=zh-CN|style=Feynman)**（如[蛙跳格式](@keyword=leapfrog_scheme|lang=zh-CN|style=Feynman)），之所以特殊，是因为它们精确地保持了相空间的几何结构。一个关键的推论是它们完全保体积。现在，考虑一个名为[标准化流](@keyword=normalizing_flows|lang=zh-CN|style=Feynman)的现代[生成模型](@keyword=generative_models|lang=zh-CN|style=Feynman)，它通过一系列可逆层变换一个简单的[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)来学习一个复杂的[概率分布](@keyword=probability_distribution|lang=zh-CN|style=Feynman)。训练这样一个模型的一个至关重要且计算成本高昂的部分是计算每一层变换的[雅可比行列式](@keyword=jacobian_determinant|lang=zh-CN|style=Feynman)的对数。但如果我们构建的层模仿辛积分器呢？那么，因为变换是保体积的，[雅可比行列式](@keyword=jacobian_determinant|lang=zh-CN|style=Feynman)恰好为1，其对数为0！计算成本高昂的项消失了。通过借鉴经典力学中的一个深刻思想，我们可以构建更强大、更高效的深度学习模型 [@problem_id:3412383]。

### 终极回报：从预测到理解

我们为什么要费这么大劲呢？回报是巨大且多方面的。

首先，正如我们所见，[物理信息](@keyword=physical_information|lang=zh-CN|style=Feynman)模型在**数据效率**上要高得多。嵌入的物理知识作为一种强大的正则化器，[防止过拟合](@keyword=prevent_overfitting|lang=zh-CN|style=Feynman)，并允许模型从稀疏、嘈杂或不完整的数据中学习。

其次，它们表现出远为优越的**泛化和外推**能力。一个理解[流体动力学](@keyword=fluid_dynamics|lang=zh-CN|style=Feynman)基本方程的模型，在面对新的[流体粘度](@keyword=viscosity_of_gases_and_liquids|lang=zh-CN|style=Feynman)时，做出稳定、准确预测的可能性，要比一个只看过狭窄范围内例子的[黑箱模型](@keyword=black_box_model|lang=zh-CN|style=Feynman)大得多 [@problem_id:3369176]。这种稳健性对于工程设计和科学预测至关重要。

然而，最重要的是，这段旅程将我们从单纯的预测带向了真正的科学理解。一个在[测试集](@keyword=test_set|lang=zh-CN|style=Feynman)上实现低误差的[黑箱模型](@keyword=black_box_model|lang=zh-CN|style=Feynman)是一个有用的工具。但是，一个建立在对称性和[守恒定律](@keyword=conservation_law|lang=zh-CN|style=Feynman)基础上，能在新颖干预下做出准确预测，且其参数可唯一识别的简约模型，可以被视为一个真正的**科学解释**的候选者 [@problem_id:3410569]。这是一个不仅告诉我们*将会*发生什么，而且让我们洞察*为什么*会发生的模型。通过教我们的计算学生物理学的语言，我们不仅在创造更好的函数逼近器；我们还在为科学发现的探索建立合作伙伴。

