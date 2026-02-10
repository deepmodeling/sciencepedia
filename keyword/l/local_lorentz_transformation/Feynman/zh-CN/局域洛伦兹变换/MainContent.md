## 引言
广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)描绘了一幅宇宙的画卷，它是一个宏大而弯曲的舞台；而量子力学则描述了在狭义相对论的平坦舞台上表演的“演员”——基本粒子。这就产生了一个深层次的概念性挑战：我们如何将量子“演员”置于引力的弯曲舞台之上？特别是，我们如何在一个[时空](@keyword=space_time|lang=zh-CN|style=Feynman)本身被质量和能量扭曲的宇宙中，描述像电子这样由其自旋定义并受平直[时空](@keyword=space_time|lang=zh-CN|style=Feynman)物理学支配的粒子？本文旨在通过探索[局域洛伦兹变换](@keyword=local_lorentz_transformations|lang=zh-CN|style=Feynman)的概念来解决这个根本问题。我们将揭示那套让物理学家得以调和这两大现代物理学支柱的优雅数学机制。

本文始于“原理与机制”一章，介绍[标架场形式](@keyword=tetrad_formalism|lang=zh-CN|style=Feynman)，这是一种在弯曲[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的每一点上构建一小块平直[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的工具。我们将看到这如何引出一种新的“局域”洛伦兹对称性，以及为何这种自由度需要引入一个新场——[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)——来保持理论的自洽性。在“应用与跨学科联系”一章，我们将看到这些思想并非纯粹的数学抽象。我们将从旋转粒子的精微进动，到奇异材料的奇特物理学，探索局域[洛伦兹不变性](@keyword=lorentz_invariance|lang=zh-CN|style=Feynman)原理如何在一系列令人惊奇的物理现象中显现，从而将宇宙与量子世界统一起来。

## 原理与机制

想象一下，你正坐在一趟疯狂的过山车上，试图描述一个被抛出的球的物理过程。你的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)——与那扭曲、俯冲的轨道相连——简直一团糟。球的路径看起来极其复杂。但若有那么一瞬间，你能漂浮在一个不受过山车作用力影响的小盒子里，球的运动就会再次变得简单：一道优美、清晰的抛物线。在你那个漂浮的小盒子里的物理定律，就是我们所熟悉的、简单的平直空间定律。

广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)告诉我们，引力*就是*一趟过山车。[时空](@keyword=space_time|lang=zh-CN|style=Feynman)本身就是那弯曲的轨道。**等效原理**的深刻洞见在于，在[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的任何一个单点，我们总能构建这样一个“漂浮的小盒子”——一个**[局域惯性系](@keyword=local_inertial_frames|lang=zh-CN|style=Feynman)**——在这里，物理定律看起来就和在[狭义相对论](@keyword=special_relativity_theory|lang=zh-CN|style=Feynman)中一模一样，引力荡然无存。核心的挑战与美妙之处在于，如何将所有这些局域的平直视角缝合在一起，形成一幅关于整个弯曲现实的连贯图景。这正是**标架场**和**[局域洛伦兹变换](@keyword=local_lorentz_transformations|lang=zh-CN|style=Feynman)**的魔力所在。

### [时空](@keyword=space_time|lang=zh-CN|style=Feynman)的局域词典：[标架场](@keyword=tetrad|lang=zh-CN|style=Feynman)

当我们描述一个弯曲时空时，我们使用一个**度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman)** $g_{\mu\nu}$。你可以把它看作是在那个特定弯曲几何中测量距离和时间的规则手册。这本手册可能很复杂；在一套[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)中，度规可能含有非对角分量，意味着时间和空间以一种非直观的方式混合在一起 [@problem_id:1550273]。

[标架场形式](@keyword=tetrad_formalism|lang=zh-CN|style=Feynman)，也称为 **vielbein** 形式（源自德语，意为“多足”），为我们提供了一种在[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中的每一点都建立一个简单、[标准化](@keyword=normalization|lang=zh-CN|style=Feynman)的[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)的方法。这个局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)根据其定义是平直的；它的度规就是[狭义相对论](@keyword=special_relativity_theory|lang=zh-CN|style=Feynman)中那个平淡无奇的[闵可夫斯基度规](@keyword=minkowski_metric|lang=zh-CN|style=Feynman)，$\eta_{ab} = \text{diag}(-1, 1, 1, 1)$。这里，我们用拉丁指标 $(a, b, c, \dots)$ 来标记这个局域、平直的“实验室”[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)中的方向，以区别于标记我们全局、[弯曲时空](@keyword=curved_spacetime|lang=zh-CN|style=Feynman)坐标的希腊指标 $(\mu, \nu, \lambda, \dots)$。

[标架场](@keyword=tetrad|lang=zh-CN|style=Feynman)，记作 $e^a_\mu(x)$，就是在这两种语言之间进行翻译的词典。对于每个坐标方向 $\mu$，它告诉你其沿着局域平直坐标轴 $a$ 的分量。定义标架场的基本关系式简单而优美：

$$
g_{\mu\nu}(x) = e^a_\mu(x) e^b_\nu(x) \, \eta_{ab}
$$

这个方程是[等效原理](@keyword=principle_of_equivalence|lang=zh-CN|style=Feynman)在实践中的体现 [@problem_id:2995522]。它表明，复杂且依赖于位置的时空度规 $g_{\mu\nu}$，可以通过将其投影到该点的一组简单的标准正交基矢上而完全重构。我们已将弯曲度规分解为局域闵可夫斯基框架的结构。例如，给定一个复杂的度规，你通常可以通过类似于“[配方法](@keyword=complete_the_square|lang=zh-CN|style=Feynman)”的方式反向求解，找到一组满足此关系的标架场分量 $e^a_\mu$ [@problem_id:1550273]。标架场让我们在曲率的世界里有了一块平坦的立足之地。

### 选择的自由：[局域洛伦兹对称性](@keyword=local_lorentz_symmetry|lang=zh-CN|style=Feynman)

好了，我们已经在过山车的某一点上建立了我们的小[实验室参考系](@keyword=laboratory_frame|lang=zh-CN|style=Feynman)。我们在这个实验室中选择的“北”、“东”和“上”方向是唯一可能的选择吗？当然不是！我们可以自由地旋转我们的实验设备，或者让它相对于我们最初的设置以一个[恒定速度](@keyword=constant_velocity|lang=zh-CN|style=Feynman)漂移（即一次助推）。这些旋转和助推正是我们所熟悉的狭义相对论中的**洛伦兹变换**。

关键的洞见在于，我们*在[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中的每一点都独立地拥有这种选择的自由*。这被称为**[局域洛伦兹对称性](@keyword=local_lorentz_symmetry|lang=zh-CN|style=Feynman)**。我们可以对我们的标架场基底施加一个[洛伦兹变换](@keyword=the_lorentz_transformation|lang=zh-CN|style=Feynman) $\Lambda^a{}_b(x)$：

$$
e'^a_\mu(x) = \Lambda^a{}_b(x) e^b_\mu(x)
$$

这会产生一个新的、完全有效的标架场 $e'^a_\mu$。当我们这样做时，[时空度规](@keyword=spacetime_metrics|lang=zh-CN|style=Feynman) $g_{\mu\nu}$ 会发生什么变化呢？让我们来验证一下：

$$
g'_{\mu\nu} = e'^a_\mu e'^b_\nu \eta_{ab} = (\Lambda^a{}_c e^c_\mu) (\Lambda^b{}_d e^d_\nu) \eta_{ab} = (\Lambda^a{}_c \Lambda^b{}_d \eta_{ab}) e^c_\mu e^d_\nu
$$

但[洛伦兹变换](@keyword=the_lorentz_transformation|lang=zh-CN|style=Feynman)的定义属性就是它保持[闵可夫斯基度规](@keyword=minkowski_metric|lang=zh-CN|style=Feynman)不变：$\Lambda^a{}_c \Lambda^b{}_d \eta_{ab} = \eta_{cd}$。因此，

$$
g'_{\mu\nu} = \eta_{cd} e^c_\mu e^d_\nu = g_{\mu\nu}
$$

时空度规完全没有改变！这是一个意义深远的结果。它告诉我们，标架场比度规本身包含了更多的信息。局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)朝向的选择是一种**[规范自由度](@keyword=gauge_freedom|lang=zh-CN|style=Feynman)**——这是我们描述中的一种冗余，它对底层的物理几何没有影响 [@problem_id:2995522]。我们可以通过施加依赖于点的旋转或助推来生成一整族有效的[标架场](@keyword=tetrad|lang=zh-CN|style=Feynman)，它们都将描述完全相同的弯曲时空，无论它是[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)周围的几何，还是[加速观察者](@keyword=accelerating_observer|lang=zh-CN|style=Feynman)的[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman) [@problem_id:1853717] [@problem_id:1853727]。

这种[局域洛伦兹对称性](@keyword=local_lorentz_symmetry|lang=zh-CN|style=Feynman)与[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中通常的**[微分同胚不变性](@keyword=diffeomorphism_invariance|lang=zh-CN|style=Feynman)**（[广义协变性](@keyword=general_covariance|lang=zh-CN|style=Feynman)）是完全不同的概念，后者处理的是事物在[时空](@keyword=space_time|lang=zh-CN|style=Feynman)坐标变换下的变化方式。微分同胚变换的是 $\mu, \nu$ 指标，而[局域洛伦兹变换](@keyword=local_lorentz_transformations|lang=zh-CN|style=Feynman)变换的是 $a, b$ 指标 [@problem_id:2995522]。

### 真正的理由：欢迎旋量进入引力的怀抱

至此，你可能会觉得这只是一个聪明但或许不必要的数学游戏。毕竟，Einstein 仅用带有空时指标的[张量](@keyword=tensor|lang=zh-CN|style=Feynman)就很好地建立起了广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)。为什么还要引入这新的一层局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)和额外的对称性呢？

答案在于量子世界中一个奇特而美妙的存在：**[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)**。像电子、夸克和中微子这样的粒子是由旋量场描述的。但问题在于：[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)，就其本性而言，并不知道如何在广义坐标变换下进[行变换](@keyword=row_operations|lang=zh-CN|style=Feynman)。它们不是[张量](@keyword=tensor|lang=zh-CN|style=Feynman)。[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)是由它们在**[洛伦兹群](@keyword=lorentz_group|lang=zh-CN|style=Feynman)**下如何变换来定义的 [@problem_id:1881205] [@problem_id:1876082]。如果你问一个[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)，当你从笛卡尔坐标切换到极坐标时它的分量如何变化，它只会茫然地看着你。但如果你问它，当你旋转或助推它时它的分量如何变化，它会欣然从命。

这就给将电子置于[弯曲时空](@keyword=curved_spacetime|lang=zh-CN|style=Feynman)带来了根本性的问题。为了能够*定义*一个[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)，你首先需要一个[洛伦兹变换](@keyword=the_lorentz_transformation|lang=zh-CN|style=Feynman)有意义的空间。[标架场](@keyword=tetrad|lang=zh-CN|style=Feynman)恰好提供了这一点：在弯曲时空的每一点，它都搭建了一个局域的闵可夫斯基舞台，[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)可以在这个舞台上表演它的量子之舞。

**狄拉克方程** $(i\gamma^\mu \partial_\mu - m)\psi = 0$ 是支配旋量的定律。在平直空间中，著名的[伽马矩阵](@keyword=gamma_matrices|lang=zh-CN|style=Feynman) $\gamma^a$ 是满足[克利福德代数](@keyword=clifford_algebra|lang=zh-CN|style=Feynman) $\{\gamma^a, \gamma^b\} = 2\eta^{ab}$ 的常数矩阵。为了让这个方程在弯曲时空中成立，我们不能简单地塞进[克里斯托费尔符号](@keyword=christoffel_symbols|lang=zh-CN|style=Feynman)。[伽马矩阵](@keyword=gamma_matrices|lang=zh-CN|style=Feynman)内在地与平直度规 $\eta_{ab}$ 绑定。标架场就是那座桥梁。我们使用它的逆 $e^\mu_a$ 从常数[伽马矩阵](@keyword=gamma_matrices|lang=zh-CN|style=Feynman)构建出依赖于位置的[伽马矩阵](@keyword=gamma_matrices|lang=zh-CN|style=Feynman)：

$$
\gamma^\mu(x) = e^\mu_a(x) \gamma^a
$$

这些新对象奇迹般地满足了正确的弯曲空间[克利福德代数](@keyword=clifford_algebra|lang=zh-CN|style=Feynman) $\{\gamma^\mu(x), \gamma^\nu(x)\} = 2g^{\mu\nu}(x)$ [@problem_id:1881205]。没有[标架场](@keyword=tetrad|lang=zh-CN|style=Feynman)，根本无法在[弯曲时空](@keyword=curved_spacetime|lang=zh-CN|style=Feynman)中以一种自洽的方式写下狄拉克方程。

### 自由的代价：[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)

我们已经付出了一个代价：引入了[标架场](@keyword=tetrad|lang=zh-CN|style=Feynman)。但是，我们每一点都能自由选择局域洛伦兹系的自由，还带来了另一个更深远的后果。想象一下，在点 $P$ 有一个[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)，在邻近的点 $Q$ 有另一个。点 $P$ 的局域“实验室”[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)可能相对于点 $Q$ 的[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)有轻微的旋转。你如何比较这两个旋量？这就像比较伦敦一个矢量的指北分量和纽约一个矢量的指北分量。两个“北”是不同的。你不能直接将它们相减。

为了进行有意义的比较——为了定义一个[导数](@keyword=derivative|lang=zh-CN|style=Feynman)——我们需要一条规则，告诉我们如何将[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)从 $P$ “[平行输运](@keyword=vector_transport_on_curved_space|lang=zh-CN|style=Feynman)”到 $Q$ 以计及局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)的变化。这条规则被编码在一个新的场中，称为**[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)** $\omega_{\mu ab}(x)$。

这是现代物理学中的一个经典故事，一个关于**规范场**的故事。将一个*全局*对称性（如狭义相对论的洛伦兹对称性）提升为一个*局域*对称性，需要引入一个联络场（一个规范场）来补偿局域变换。[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)就是[局域洛伦兹对称性](@keyword=local_lorentz_symmetry|lang=zh-CN|style=Feynman)的[规范场](@keyword=gauge_fields|lang=zh-CN|style=Feynman)。

当我们为旋量定义一个**协变导数**时，我们必须加上一个包含[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)的项：

$$
D_\mu \psi = \partial_\mu \psi + \Gamma_\mu \psi
$$

这个联络项 $\Gamma_\mu$ 是一个由[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)分量 $\omega_{\mu ab}$ 和[旋量表示](@keyword=spinor_representations|lang=zh-CN|style=Feynman)下的[洛伦兹变换](@keyword=the_lorentz_transformation|lang=zh-CN|style=Feynman)生成元 $\sigma^{ab} = \frac{i}{2}[\gamma^a, \gamma^b]$ 构建的矩阵。标准的构造是 [@problem_id:1876110]：

$$
\Gamma_\mu = \frac{1}{2} \omega_{\mu ab} \sigma^{ab}
$$

[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)分量 $\omega_{\mu ab}$ 是这个新“[力场](@keyword=force_field|lang=zh-CN|style=Feynman)”的势，其作用是确保当我们自由选择每一点的局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)时，物理定律（如[狄拉克方程](@keyword=dirac_equation|lang=zh-CN|style=Feynman)）保持不变 [@problem_id:1547481]。事实上，如果你从一个没有[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)且[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)为零的情境开始，然后通过一个依赖于位置的洛伦兹变换来选择一套新的局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)，你会发现你已经生成了一个非零的[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)。正是我们扭转局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)的行为本身，使得这个场得以存在 [@problem_id:1876116]。

### 对称性与现实：计算自由度

现在我们可以看到整个优美的结构。[标架场](@keyword=tetrad|lang=zh-CN|style=Feynman) $e^a_\mu$ 在每一点有 16 个分量。而时空度规 $g_{\mu\nu}$ 是对称的，只有 10 个分量。[标架场](@keyword=tetrad|lang=zh-CN|style=Feynman)中多出来的六个自由度是从哪里来的？

它们恰好是[局域洛伦兹变换](@keyword=local_lorentz_transformations|lang=zh-CN|style=Feynman)的六个参数（三个旋转和三个助推）。这六个自由度是“纯规范”的。它们代表了我们定向局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)的自由，对物理度规没有影响。

一项优美的分析明确地证明了这一点 [@problem_id:1550281]。如果我们考虑标架场相对于平直背景的一个小微扰 $\epsilon_{\mu\nu}$，我们可以将其分解为一个对称部分 $S_{\mu\nu}$ 和一个反对称部分 $A_{\mu\nu}$。结果发现，对称部分直接与物理度规的微扰 $h_{\mu\nu}$ 相关——它描述了真实的[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)，即引力波。而反对称部分 $A_{\mu\nu}$ 则是规范自由度。通过施加一个无穷小的[局域洛伦兹变换](@keyword=local_lorentz_transformations|lang=zh-CN|style=Feynman)，我们可以任意改变 $A_{\mu\nu}$ 而完全不改变 $S_{\mu\nu}$。

所以，[标架场形式](@keyword=tetrad_formalism|lang=zh-CN|style=Feynman)不仅为将旋量与引力耦合提供了必要的结构，而且还优雅地将[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)的物理自由度与选择局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)相关的纯[规范自由度](@keyword=gauge_freedom|lang=zh-CN|style=Feynman)分离开来。这是一个完美的例子，说明了在我们的自然法则中要求更深层次的对称性，可以如何导出一个更丰富、更具预测性、并最终更优美的物理理论。