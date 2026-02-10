## 应用与跨学科联系

在掌握了材料框架无关性原理的基本性质之后，我们现在准备看它如何发挥作用。你可能会认为这样一个抽象的原理——物理定律不应取决于你的旋转方式——只是哲学家的乐事，没什么实际用途。事实远非如此。这个原理并非什么深奥的脚注；它是一个严厉的守门人，一位大师级的建筑师，它规定了我们用以描述周遭世界的方程的形式。从橡皮筋的拉伸到冰川的流动，再到驱动超级计算机模拟的算法，这个原理是我们坚定不移的指南。它不告诉我们一种材料*是*什么，但它告诉我们任何对材料的合理解释*必须是*什么样的。

### 基础：构建可靠的材料模型

让我们从简单的东西开始，比如一块橡胶。当我们拉伸它时，它会储存能量。我们想为这种储存的能量编写一个定律。变形由变形梯度张量 $\mathbf{F}$ 捕捉。一个朴素的初步猜测可能是，能量 $W$ 只是 $\mathbf{F}$ 的某个函数。但材料框架无关性原理立刻告诉我们这是错误的。

想象你使橡胶块变形，然后我只是把它捡起来旋转一下，没有进一步的拉伸。变形梯度 $\mathbf{F}$ 变成了 $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$，其中 $\mathbf{Q}$ 是旋转。但储存的能量改变了吗？当然没有！橡胶块处于相同的拉伸状态，只是在空间中的朝向不同。因此，任何有效的储存能定律都必须满足 $W(\mathbf{F}) = W(\mathbf{Q}\mathbf{F})$ 对于任何旋转 $\mathbf{Q}$。

这个单一的要求产生了一个深远的结果。它迫使能量函数 $W$ 对 $\mathbf{F}$ 的依赖只能通过那些对旋转不敏感的组合。最方便的这类量是右柯西-格林变形张量，$\mathbf{C} = \mathbf{F}^\mathsf{T}\mathbf{F}$。如果我们旋转变形后的状态，新的 $\mathbf{C}^*$ 是 $(\mathbf{Q}\mathbf{F})^\mathsf{T}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^\mathsf{T}\mathbf{Q}^\mathsf{T}\mathbf{Q}\mathbf{F} = \mathbf{F}^\mathsf{T}\mathbf{F} = \mathbf{C}$。它保持不变！因此，该原理将我们的[超弹性](@keyword=superelasticity|lang=zh-CN|style=Feynman)[储能函数](@keyword=stored_energy_function_2|lang=zh-CN|style=Feynman)的形式从一个任意的九变量函数（$\mathbf{F}$ 的分量）约束为一个[对称张量](@keyword=symmetric_tensors|lang=zh-CN|style=Feynman)的函数，该张量的分量被构建为忽略旋转 [@problem_id:2893468]。这不仅仅是数学上的便利；它是一个深刻的物理洞见。材料本身不知道它在你的实验室里是如何定向的；它只知道它被拉伸了多少。

这种约束的美妙之处在于它保证了物理上合理的结果。考虑一个以此方式构建的[超弹性](@keyword=superelasticity|lang=zh-CN|style=Feynman)固体模型，其中能量仅依赖于 $\mathbf{C}$ 的不变量。如果材料经历纯[刚体](@keyword=rigid_bodies|lang=zh-CN|style=Feynman)旋转，这个模型会预测出什么应力？对于这样的运动，$\mathbf{F}$ 是一个[旋转张量](@keyword=rotation_tensor|lang=zh-CN|style=Feynman) $\mathbf{R}$。相应的应变张量是 $\mathbf{C} = \mathbf{R}^\mathsf{T}\mathbf{R} = \mathbf{I}$，即单位张量，这与未变形状态相同。由于应变状态与初始状态相同，模型正确地预测应力为零。材料模型没有被旋转所迷惑，因为框架无关性原理已经融入其结构之中 [@problem_id:3797547]。

### 河流穿行其间：流体中的框架无关性

支配拉伸固体的相同逻辑也适用于流动的流体，尽管语言有所变化。对于流体，我们关心的是变形的*速率*。关键量是速度梯度 $\mathbf{L}$，它告诉我们流场中速度如何随点变化。正如 $\mathbf{F}$ 可以分解为旋转和拉伸一样，$\mathbf{L}$ 也可以分为两部分：一个对称部分 $\mathbf{D}$，即变形率张量（描述流体元如何拉伸和剪切），和一个反对称部分 $\mathbf{W}$，即[自旋张量](@keyword=spin_tensor|lang=zh-CN|style=Feynman)（描述它如何旋转）。

那么，像水或蜂蜜这样的简单流体中的应力应该取决于哪一部分呢？直觉表明它应该是变形部分 $\mathbf{D}$。框架无关性原理以不容置疑的逻辑证实了这一点。柯西应力 $\boldsymbol{\sigma}$ 是一个客观量；其物理现实不依赖于观察者。变形率 $\mathbf{D}$ 也是客观的。但[自旋张量](@keyword=spin_tensor|lang=zh-CN|style=Feynman) $\mathbf{W}$ *不是*客观的。

为了理解这一点，想象你静静地坐在一屋子静止的空气中。你测得空气的[速度梯度](@keyword=velocity_gradient|lang=zh-CN|style=Feynman)为零，所以 $\mathbf{D}$ 和 $\mathbf{W}$ 都为零。现在，想象你正以恒定速率在一张转椅上旋转。从你旋转的视角来看，屋子里的空气似乎在你周围旋转！你会测量到一个非零的[自旋张量](@keyword=spin_tensor|lang=zh-CN|style=Feynman) $\mathbf{W}$，但变形率 $\mathbf{D}$ 仍然为零。如果空气中的应力取决于 $\mathbf{W}$，那就意味着你脸上的气压仅仅因为你开始旋转就会改变。这是荒谬的。空气的物理状态不能依赖于观察它的人的运动。因此，用于简单牛顿流体的本构律（它将应力与变形率联系起来）必须只依赖于 $\mathbf{D}$，并且完全独立于 $\mathbf{W}$ [@problem_id:4082469]。这就是为什么著名的[牛顿流体](@keyword=newtonian_fluids|lang=zh-CN|style=Feynman)定律写成 $\boldsymbol{\tau} = 2\mu \mathbf{D}$，其中 $\boldsymbol{\tau}$ 是[偏应力](@keyword=deviatoric_stress|lang=zh-CN|style=Feynman)，$\mu$ 是粘度。自旋部分被[客观性原理](@keyword=principle_of_objectivity|lang=zh-CN|style=Feynman)禁止进入方程。

### 变化的挑战：当率变得复杂

材料世界远比简单的橡胶块和水要丰富得多。在许多领域，如[金属塑性](@keyword=metal_plasticity|lang=zh-CN|style=Feynman)或岩[土力学](@keyword=soil_mechanics|lang=zh-CN|style=Feynman)，以“率形式”编写定律更为方便：应力如何响应微小的变形增量而*变化*？这是*次弹性*的领域，并且是大量[计算模型](@keyword=model_of_computation|lang=zh-CN|style=Feynman)的基础。

在这里，我们遇到了一个微妙但关键的陷阱。写出像“应力变化率与变形率成正比”这样的定律，即 $\dot{\boldsymbol{\sigma}} = f(\mathbf{D})$，似乎很自然。但框架无关性原理发出了响亮的警报。简单的[物质时间导数](@keyword=material_time_derivative|lang=zh-CN|style=Feynman) $\dot{\boldsymbol{\sigma}}$ 并不是客观的！

让我们回到我们旋转的观察者。如果他们看一块在实验室坐标系中完全无应力的材料，其应力 $\boldsymbol{\sigma}$ 为零且不变，所以 $\dot{\boldsymbol{\sigma}}=\mathbf{0}$。但对旋转的观察者来说，（仍然为零的）[应力张量](@keyword=stress_tensor|lang=zh-CN|style=Feynman)的*分量*在他们旋转的坐标系中是变化的。他们会测量到一个非零的 $\dot{\boldsymbol{\sigma}}^*$。这意味着 $\dot{\boldsymbol{\sigma}}$ 是一个依赖于观察者的量。如果我们的本构律使用了 $\dot{\boldsymbol{\sigma}}$，它就会做出依赖于观察者运动的预测，从而违反了我们的基本原理 [@problem_id:3797576]。

解决方案是[连续介质力学](@keyword=continuum_mechanics|lang=zh-CN|style=Feynman)中最优雅的思想之一：发明**[客观应力率](@keyword=objective_stress_rates|lang=zh-CN|style=Feynman)**。如果简单的时间导数被旋转“污染”了，我们可以通过明确地减去旋转部分来修正它。其中最著名的是**Jaumann率**，定义为：
$$
\overset{\triangledown}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \mathbf{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{W}
$$
这个构造优美地抵消了由观察者自旋产生的非客观项。从物理上讲，你可以把它想象成在一个与材料在该点一同旋转的框架中测量应力的变化率。有了这个修正后的率，我们现在可以写出一个客观的次弹性定律，$\overset{\triangledown}{\boldsymbol{\sigma}} = f(\mathbf{D})$，它将为所有观察者提供相同的物理预测，无论他们如何旋转 [@problem_id:3601294] [@problem_id:2657749]。

### [客观率](@keyword=objective_rates|lang=zh-CN|style=Feynman)的大观园

Jaumann率仅仅是个开始。一旦这扇门被打开，物理学家和工程师们意识到有许多方法可以构造一个[客观率](@keyword=objective_rates|lang=zh-CN|style=Feynman)，每种方法都对应于关于使用哪个“正确的”旋转框架作为参考的不同物理直觉。

*   在研究**粘弹性流体**（如聚合物熔体）时，通常使用**上随钻导数**。这个率可以被认为是坐标轴不仅在旋转，而且还在随流体拉伸和变形的观察者所看到的变化率，就好像它们被画在材料上一样 [@problem_id:3388285]。

*   在**[地球物理学](@keyword=geophysics|lang=zh-CN|style=Feynman)**中，当模拟岩石板块缓慢、大规模的变形时，会使用其他率，如**[Green-Naghdi率](@keyword=green_naghdi_rate|lang=zh-CN|style=Feynman)**（基于$\mathbf{F}$的极分解得到的旋转）和**[Truesdell率](@keyword=truesdell_rate|lang=zh-CN|style=Feynman)**。虽然它们都是客观的，并且都能正确预测纯[刚体运动](@keyword=rigid_body_motion|lang=zh-CN|style=Feynman)中不产生应力，但它们在处理有限拉伸方面有所不同，导致在复杂变形中的预测略有差异。它们之间的选择是一个微妙的建模决策，但它们都为满足框架无关性而设计这一事实至关重要 [@problem_id:3581301]。

### 超越应力与应变：建模物质的构造

该原理的[影响范围](@keyword=range_of_influence|lang=zh-CN|style=Feynman)超出了[应力与应变](@keyword=stress_and_strain|lang=zh-CN|style=Feynman)。它支配着我们用来描述材料内部状态的任何变量。考虑在混凝土或岩石等岩土材料中对损伤进行建模。如果材料产生的微裂纹优先沿一个方向排列，那么损伤就是各向异性的，可以用一个张量 $\mathbf{D}$ 来表示。

为了使从该张量导出的任何标量（如储存在受损材料中的能量）是客观的，损伤张量本身必须像一个客观张量一样变换，即在观察者变换下 $\mathbf{D}' = \mathbf{Q}\mathbf{D}\mathbf{Q}^\mathsf{T}$ [@problem_id:3510345]。相反，如果损伤是各向同性的（在所有方向上都相同），则可以用一个简单的标量 $D$ 来描述。标量本质上是客观的；当你[旋转坐标系](@keyword=rotating_coordinate_systems|lang=zh-CN|style=Feynman)时，它的值不会改变。因此，它不需要特殊的旋转更新规则。将两者混淆，试图将张量旋转应用于标量变量，是一个违反该原理基本逻辑的典型错误 [@problemid:2897264]。

### 现代模拟的两条路径

最终，这个抽象的原理在[计算力学](@keyword=computational_mechanics|lang=zh-CN|style=Feynman)领域找到了其最关键的应用——这些超级计算机模拟帮助我们设计更安全的汽车、更具弹性的建筑，并理解地球物理灾害。在为[有限元法](@keyword=finite_element_methods|lang=zh-CN|style=Feynman)（FEM）或[物质点法](@keyword=material_point_method|lang=zh-CN|style=Feynman)（MPM）等方法开发算法时，材料框架无关性原理迫使建模者选择两条基本路径之一。

**路径1：率型公式。** 这条路径对于具有复杂历史的材料很常见，比如经历塑性变形的金属。建模者为应力在小时间步内如何*变化*编写一个定律。为此，他们*必须*使用我们讨论过的[客观应力率](@keyword=objective_stress_rates|lang=zh-CN|style=Feynman)之一，如Jaumann率。这确保了即使材料正在经历大旋转和复杂变形，模拟结果在物理上也是有意义的 [@problem_id:2657749]。

**路径2：[超弹性](@keyword=superelasticity|lang=zh-CN|style=Feynman)公式。** 这条路径对于类橡胶材料很常见，但也是现代塑性模型的理论基础。建模者不是定义一个率定律，而是基于一个客观的总应变量度（如$\mathbf{C}_e$）来定义一个总储存能函数。应力在每一步都直接从这个势函数计算出来。这种方法是“通过构造实现客观性”的。它巧妙地回避了整个[客观率](@keyword=objective_rates|lang=zh-CN|style=Feynman)的问题，因为该公式从一开始就是为了对旋转不敏感而设计的 [@problem_id:2897264]。

这两条路径，如果正确实施，都能带来强大且具有预测性的模拟。它们之间的选择是[计算力学](@keyword=computational_mechanics|lang=zh-CN|style=Feynman)中的一个核心主题。材料框架无关性原理远非一个纯粹的学术好奇心，它是一个强大、实用且不可或缺的工具。它是每个方程中的沉默伙伴，是每个模拟中无形的蓝图，确保我们对物质世界的模型建立在物理真理的基础之上。