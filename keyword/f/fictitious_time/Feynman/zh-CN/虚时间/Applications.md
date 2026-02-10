## 应用与跨学科联系

在我们穿越了虚时间的原理之后，人们可能会倾向于将其视为一种聪明但或许小众的数学技巧。[复平面](@keyword=complex_plane|lang=zh-CN|style=Feynman)上的一次奇特旋转，简化了这里的或那里的一个方程。但这样做将只见树木不见森林。替换 $t \to -i\tau$ 不仅仅是变量的改变；它是一个新的透镜，一个新的视角，揭示了在表面上看起来毫无关联的科学领域之间惊人的一致性。现在让我们来探索这片应用的广阔天地，从实用的计算工具到关于[时空](@keyword=space_time|lang=zh-CN|style=Feynman)和现实的最深层问题。

### 终极冷却系统：寻找[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)

想象你有一个复杂的量子系统——一个分子、一个晶体、一团超冷原子云——而你想找到其可能能量最低的状态，即其“[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)”。这是量子物理学和化学中最基本的任务之一，因为[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)决定了系统的结构、稳定性和低温性质。但一个系统可以存在于无限多个能量态的令人眼花缭乱的叠加中。我们如何能分离出那个单一、独特的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)呢？

虚时间提供了一个惊人优雅的答案。正如我们所见，威克转动将[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的薛定谔方程转变为一个类似扩散的方程，这在数学上类似于描述热量如何传播和耗散的方程。想象一个热物体被留在冷房间里。热量从较热的区域流向较冷的区域，物体逐渐冷却，其热能耗散，直到达到一个均匀的最低温度。

完全相同地，在[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)中演化一个[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)会将其“冷却”下来。如果我们从一个任意的状态开始——一个[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)和许多高能“[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)”的杂乱叠加——并让它在虚时间中演化，高能分量会以比低能分量快得多的指数速度衰减掉。随着虚时间 $\tau$ 的推移，[激发态](@keyword=excited_state|lang=zh-CN|style=Feynman)被一个接一个地过滤掉，直到剩下的全是纯粹、无杂质的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。

这个原理不仅仅是一个美丽的理论思想；它是一些科学领域最强大的数值方法背后的引擎。计算物理学家和化学家利用这种虚时间传播来寻找各种系统的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)。他们可以计算简单量子谐振子的性质（[@problem_id:2211518], [@problem_id:2402642]），或者处理更复杂的场景，如双阱势，这是[化学键](@keyword=chemical_bond|lang=zh-CN|style=Feynman)和像氨这样的[分子结构](@keyword=molecular_structure|lang=zh-CN|style=Feynman)的基本模型（[@problem_id:2460933], [@problem_id:2441302]）。该方法如此稳健，甚至可以扩展到复杂的、相互作用的[多体系统](@keyword=many_body_systems|lang=zh-CN|style=Feynman)，如玻色-爱因斯坦凝聚，这是一种奇异的[物质状态](@keyword=states_of_matter|lang=zh-CN|style=Feynman)，其中成千上万的原子以完美的量子协同方式行动，由非线性的 Gross-Pitaevskii 方程控制（[@problem_id:2383399]）。

这种“[量子冷却](@keyword=quantum_cooling|lang=zh-CN|style=Feynman)”的力量是如此基础，以至于它现在正被应用于下一代技术：[量子计算](@keyword=quantum_computation|lang=zh-CN|style=Feynman)机。像变分虚[时间演化](@keyword=time_evolution|lang=zh-CN|style=Feynman)（Variational Imaginary Time Evolution, VITE）这样的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)正在被开发，以利用量子硬件来寻找分子的电子[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)，这对药物发现和[材料科学](@keyword=material_science|lang=zh-CN|style=Feynman)具有极其重要的意义（[@problem_id:2917648]）。起初的数学奇思，如今已成为未来计算机上运行[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)的核心。

### 穿越高山与[路径积分](@keyword=path_integration|lang=zh-CN|style=Feynman)的语言

看待量子力学的另一种方式是通过 [Richard Feynman](@keyword=richard_feynman|lang=zh-CN|style=Feynman) 的[路径积分表述](@keyword=path_integral_formulation|lang=zh-CN|style=Feynman)。在这里，一个从 A 点行进到 B 点的粒子不走单一路径；它同时探索*所有可能的路径*，到达 B 点的概率是所有这些历史的总和。在实时间里，这个总和涉及复杂的、[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的相位，这正是[量子干涉](@keyword=quantum_interference|lang=zh-CN|style=Feynman)成为可能的原因。

当我们切换到[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)时，神奇的事情发生了。[振荡](@keyword=oscillation|lang=zh-CN|style=Feynman)的总和转变为一个统计总和，其中每条路径都由一个实数因子 $e^{-S_E/\hbar}$ 加权。这里，$S_E$ 是“[欧几里得作用量](@keyword=euclidean_action|lang=zh-CN|style=Feynman)”，贡献最大的路径是那些使这个量最小化的路径。这些主导路径被称为 **瞬子 (instantons)**。

那么，什么是[瞬子](@keyword=instantons|lang=zh-CN|style=Feynman)呢？它无非是经典[运动方程](@keyword=equations_of_motion|lang=zh-CN|style=Feynman)的一个解，但有一个转折。[欧几里得作用量](@keyword=euclidean_action|lang=zh-CN|style=Feynman) $S_E$ 中的势能项是实时间动力学中势能的*负值*。这意味着粒子遵循的经典轨迹是在一个每座山都是谷、每座谷都是山的世界里。

考虑量子隧穿现象，一个粒子可以穿过一个它在经典上不应能克服的能量壁垒。[路径积分](@keyword=path_integration|lang=zh-CN|style=Feynman)如何描述这一点？在[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)里，能量壁垒变成了一个能量阱。瞬子路径就是粒子“滚过”这个反转阱的经典运动（[@problem_id:404285]）。这个瞬子路径的[欧几里得作用量](@keyword=euclidean_action|lang=zh-CN|style=Feynman)给出了隧穿概率的主要贡献。这个深刻而优美的思想提供了一个定量的工具，用来计算从[放射性衰变](@keyword=radioactive_decay|lang=zh-CN|style=Feynman)到微观磁体翻转等各种过程的速率。

### 时间的秘密身份：温度与[时空](@keyword=space_time|lang=zh-CN|style=Feynman)

我们现在来到了最深刻、最令人费解的联系。虚时间与温度之间的关系不仅仅是一个类比；它是一种同一性。

在[量子统计力学](@keyword=quantum_statistical_mechanics|lang=zh-CN|style=Feynman)中，一个系统在温度 $T$ 下的热性质被编码在其[配分函数](@keyword=sum_over_states_2|lang=zh-CN|style=Feynman) $Z = \text{Tr}(e^{-\beta \hat{H}})$ 中，其中 $\beta = 1/(k_B T)$ 是[逆温](@keyword=temperature_inversion|lang=zh-CN|style=Feynman)度。将其与[量子时间演化](@keyword=quantum_time_evolution|lang=zh-CN|style=Feynman)算符 $U(t) = e^{-i\hat{H}t/\hbar}$ 相比较。如果我们进行替换 $t = -i\hbar\beta$，这两个表达式是相同的。在实时间间隔 $t$ 上的演化，在数学上等同于处于[逆温](@keyword=temperature_inversion|lang=zh-CN|style=Feynman)度 $\beta = it/\hbar$ 的[热平衡](@keyword=thermal_balance|lang=zh-CN|style=Feynman)状态。

这种形式上的同一性是一块罗塞塔石碑，让我们能将量子场论的语言翻译成[统计力](@keyword=statistical_forces|lang=zh-CN|style=Feynman)学的语言。它告诉我们，一个在有限温度 $T$ 下的量子系统可以由一个路径积分来描述，其中[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)维度不是无限的，而是紧化成一个周长为 $\beta = \hbar/(k_B T)$ 的圆（[@problem_id:1907767]）。一个非常热的系统对应于一个微小的、紧紧卷曲的虚时间维度，而绝对零度则对应于一个延伸至无穷远的[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)轴。

这种量子到经典的映射带来了惊人的后果。

**[量子临界性](@keyword=quantum_criticality|lang=zh-CN|style=Feynman)：** 在绝对[零度](@keyword=nullity|lang=zh-CN|style=Feynman)下，一些材料可以被调谐到一个“[量子临界点](@keyword=quantum_critical_point|lang=zh-CN|style=Feynman)”，这是两种不同[量子态](@keyword=quantum_state|lang=zh-CN|style=Feynman)（例如，磁体和非磁体）之间的[连续相变](@keyword=continuous_phase_transitions|lang=zh-CN|style=Feynman)。在这一点上，涨落在所有长度和时间尺度上发生，但空间和时间的标度方式不同。这种关系由一个动力学临界指数 $z$ 控制，即如果空间被缩放一个因子 $b$，时间必须被缩放 $b^z$。量子到经典的映射告诉我们，一个 $d$ 维的[量子临界点](@keyword=quantum_critical_point|lang=zh-CN|style=Feynman)等效于一个[有效维度](@keyword=effective_dimension|lang=zh-CN|style=Feynman)为 $d+z$ 的经典统计系统。[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)实际上充当了一个额外的空间维度，使得经典[临界现象](@keyword=critical_phenomena|lang=zh-CN|style=Feynman)的强大工具可以被应用于量子世界（[@problem_id:2978227]）。

**[黑洞热力学](@keyword=black_hole_thermodynamics|lang=zh-CN|style=Feynman)：** 最令人震惊的应用来自量子力学与广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)的结合。在[经典物理学](@keyword=classical_physics|lang=zh-CN|style=Feynman)中，[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)是一个完美吸收体，任何东西都无法逃脱。但是，当我们在虚时间中观察其几何——[史瓦西度规](@keyword=schwarzschild_metric|lang=zh-CN|style=Feynman)——时会发生什么？在[事件视界](@keyword=event_horizon|lang=zh-CN|style=Feynman)，即不归点，发生了一件奇怪的事情。除非虚时间坐标被设为周期性的，否则几何会发展出一个“[锥形奇点](@keyword=cone_singularity|lang=zh-CN|style=Feynman)”，一个像圆锥尖端一样的尖锐点，这将代表物理学的崩溃。为了确保[时空](@keyword=space_time|lang=zh-CN|style=Feynman)是平滑和行为良好的，人们*被迫*使[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)成为周期性的。

惊人的结果是，所需的周期 $\beta$ 由[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的质量唯一确定：$\beta = 8\pi M$（在 $G=c=k_B=\hbar=1$ 的单位制下）（[@problem_id:667855]）。利用基本关系 $\beta = 1/T$，这意味着[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)必须有一个温度，$T = 1/(8\pi M)$。这就是著名的[霍金温度](@keyword=hawking_temperature|lang=zh-CN|style=Feynman)。一个纯粹的数学上对虚时间平滑性的要求，揭示了一个深刻的物理事实：[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)并非真正的黑色，而是像热体一样辐射。很难想象有比这更优美的例子能说明一个物理原理的统一力量了。

### 量子世界的母语（以及翻译的代价）

对于许多现代[理论物理学](@keyword=theoretical_physics|lang=zh-CN|style=Feynman)领域来说，虚时间不仅仅是一个有用的工具；它是表达理论的自然语言。例如，在量子凝聚态物理学中，涉及许多相互作用电子的计算几乎总是使用“[松原形式](@keyword=imaginary_time_formalism|lang=zh-CN|style=Feynman)”来进行，该形式完全在虚时间和频率中操作。像 [Sachdev-Ye-Kitaev (SYK) 模型](@keyword=sachdev_ye_kitaev_(syk)_model|lang=zh-CN|style=Feynman)这样的高级模型——一个用于理解量子混沌和全息理论的迷人理论游乐场——是使用[虚时间](@keyword=imaginary_time|lang=zh-CN|style=Feynman)[格林函数](@keyword=green_s_functions|lang=zh-CN|style=Feynman)来表述和求解的（[@problem_id:3014119]）。

然而，这种理论上的便利是有代价的。我们并不生活在欧几里得[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中。我们的实验测量的是实时间和实频率下的量，例如被光从材料中踢出的电子的能谱。因此，我们虚时间计算的结果必须被“翻译”回现实世界的语言。

这个翻译过程被称为 **[解析延拓](@keyword=analytic_continuation|lang=zh-CN|style=Feynman) (analytic continuation)**。它涉及从虚频率轴上一组离散点上的已知值来重建实频率轴上的函数。这被证明是一个臭名昭著的困难的、“不适定”的问题（[@problem_id:2456227]）。连接这两个域的[积分变换](@keyword=integral_transforms|lang=zh-CN|style=Feynman)就像一个模糊滤镜，平滑并抑制了尖锐的特征。从“模糊”的数据（[虚频](@keyword=imaginary_vibrational_frequency|lang=zh-CN|style=Feynman)[格林函数](@keyword=green_s_functions|lang=zh-CN|style=Feynman)）中恢复原始的、清晰的“图像”（实[频谱](@keyword=frequency_spectrum|lang=zh-CN|style=Feynman)）对初始计算中的任何噪声或不精确性都极其敏感。这是[计算物理学](@keyword=computational_physics|lang=zh-CN|style=Feynman)中的一个主要挑战，需要复杂的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，仔细地整合函数的已知解析性质。

从一个简单的数学戏法出发，我们已经跨越了整个科学版图。虚构时间不再是虚构，而是一把钥匙，它解锁了物质的[基态](@keyword=basis_states|lang=zh-CN|style=Feynman)，解释了[量子隧穿](@keyword=quantum_mechanical_tunneling|lang=zh-CN|style=Feynman)的奥秘，统一了量子力学与[热力学](@keyword=thermomechanics|lang=zh-CN|style=Feynman)，并揭示了[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)隐藏的热性质。它为我们一些最先进的理论提供了母语，提醒我们，有时，关于我们真实世界最深刻的真理，是通过大胆地踏入虚构领域而发现的。