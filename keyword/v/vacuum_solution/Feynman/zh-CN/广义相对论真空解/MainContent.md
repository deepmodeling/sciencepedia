## 引言
当空间中空无一物时会发生什么？在爱因斯坦的广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中，这个简单的问题揭示了一个充满复杂与奇妙的宇宙。如果作为引力曲率来源的[应力-能量张量](@keyword=stress_energy_tensor|lang=zh-CN|style=Feynman)为零，人们可能会[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)[时空](@keyword=space_time|lang=zh-CN|style=Feynman)是平直且平淡无奇的。然而，现实远比这迷人得多。[真空场方程](@keyword=vacuum_field_equations|lang=zh-CN|style=Feynman)并非虚无的配方，而是一套支配[时空](@keyword=space_time|lang=zh-CN|style=Feynman)[内蕴几何](@keyword=intrinsic_geometry|lang=zh-CN|style=Feynman)的规则，允许它弯曲、泛起涟漪并蕴含巨大能量。本文探讨了这些“[真空解](@keyword=vacuum_solution|lang=zh-CN|style=Feynman)”，弥合了我们对“空”的直观概念与其深刻物理含义之间的鸿沟。旅程始于“原理与机制”，我们将在此揭示[真空解](@keyword=vacuum_solution|lang=zh-CN|style=Feynman)的数学基础，并区分由物质产生的曲率与空旷空间中自由传播的曲率。然后，我们将在“应用与跨学科联系”中探索其深远影响，发现这些概念如何体现为[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)、膨胀的宇宙，甚至为量子现象提供了舞台。

## 原理与机制

既然我们已经搭建好了舞台，现在就让我们拉开帷幕，看看广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)在其最纯粹形式下的运作机制。当我们审视空无所有物质和能量的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)本身时，会发生什么？你可能会认为答案是“什么都不会发生”，但正如我们即将看到的，“什么都没有”是整个物理学中最引人入胜的主题之一。一个空荡的舞台不一定是一个无聊的舞台；这正是时空几何本身大展身手的时刻。

### 游戏规则：什么是真空？

在物理学中，我们有一个根深蒂固的信念，即自然法则可以用一种极其紧凑和优雅的方式来表达。我们常常发现，物理系统的演化方式会使其某个量随时间最小化或保持平稳。这被称为**[平稳作用量原理](@keyword=principle_of_stationary_action|lang=zh-CN|style=Feynman)**。对于[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)而言，这个量就是**[爱因斯坦-希尔伯特作用量](@keyword=einstein_hilbert_action|lang=zh-CN|style=Feynman)**。想象一下，你有一个[时空](@keyword=space_time|lang=zh-CN|style=Feynman)，然后你稍微“扭动”一下它的几何。正确的、物理上真实的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)是那个作用量在初始扰动下不发生变化的——它处于一个平稳点。

当我们对一个完全没有物质的区域——一个真正的真空——进行这种数学演算时，[平稳作用量原理](@keyword=principle_of_stationary_action|lang=zh-CN|style=Feynman)给了我们一组异常简洁的方程。它告诉我们，某个曲率的度量，即**爱因斯坦张量** $G_{\mu\nu}$，必须处处为零：
$$G_{\mu\nu} = R_{\mu\nu} - \frac{1}{2} R g_{\mu\nu} = 0$$
在这里，$R_{\mu\nu}$ 是**里奇张量**，它捕捉了一小团测试粒子的体积如何变化；$R$ 是**里奇标量**，即[里奇张量](@keyword=ricci_tensor|lang=zh-CN|style=Feynman)的迹。这个方程是我们讨论的核心。它是支配空旷空间形态的法则。

当你解这个方程时，会发生一件奇妙的事情。如果你取它的迹（一种对所有方向的“平均”），你会发现 $-R = 0$，这意味着[里奇标量](@keyword=ricci_scalar|lang=zh-CN|style=Feynman) $R$ 必须为零。将此结果代回[主方程](@keyword=master_equation|lang=zh-CN|style=Feynman)，我们得到了一个更简单的条件：
$$R_{\mu\nu} = 0$$
这些就是著名的**[真空场方程](@keyword=vacuum_field_equations|lang=zh-CN|style=Feynman)**。它们就是游戏规则。任何满足此条件的[时空几何](@keyword=spacetime_geometry|lang=zh-CN|style=Feynman)都是一个有效的“[真空解](@keyword=vacuum_solution|lang=zh-CN|style=Feynman)”。一个直接的推论是，它的[里奇标量](@keyword=ricci_scalar|lang=zh-CN|style=Feynman)也必须为零，这一事实看似微不足道，却是整个结构的基石。

### 寂静之声：平直[时空](@keyword=space_time|lang=zh-CN|style=Feynman)解

方程 $R_{\mu\nu} = 0$ 最简单、最明显的解是什么？嗯，如果根本没有曲率呢？一个完全平直、毫无特征的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)。这就是狭义相对论的世界，即你在我们引入引力之前初次见到的**闵可夫斯基时空**。在熟悉的[笛卡尔坐标系](@keyword=cartesian_coordinate_system|lang=zh-CN|style=Feynman)中，它的度规看起来很简单：
$$ds^2 = -c^2 dt^2 + dx^2 + dy^2 + dz^2$$
因为度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman)的所有分量在这些坐标中都是常数，所以它所有的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)都为零。当你把这个代入[曲率张量](@keyword=curvature_tensor|lang=zh-CN|style=Feynman)的复杂公式时，一切都坍缩为零。描述完整[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)的**黎曼曲率张量** $R_{\alpha\beta\gamma\delta}$ 为零。如果整个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)都为零，那么它的迹，即里奇张量，也为零。因此，$R_{\mu\nu} = 0$ 得到满足。

这似乎太容易了。如果我们使用一个奇怪的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)会怎样？在[柱坐标系](@keyword=cylindrical_coordinate_system|lang=zh-CN|style=Feynman)中，平直[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的度规是 $ds^2 = -c^2 dt^2 + d\rho^2 + \rho^2 d\phi^2 + dz^2$。现在，度规分量 $g_{\phi\phi} = \rho^2$ 不再是常数。由度规[导数](@keyword=derivative|lang=zh-CN|style=Feynman)构成的克里斯托费尔符号也不再全部为零。它看起来是弯曲的！但这只是坐标的戏法。如果你费力地计算里奇张量，你会奇迹般地发现，所有非零项都完美地相互抵消，最终得到 $R_{\mu\nu}=0$。

这里的教训是深刻的。平直是几何的内蕴属性，而不是你用来描述它的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)的特征。一张平坦的纸，无论你是在上面画方形网格还是极坐标网格，它都是平的。用[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)的语言来说，任何你*能够*找到一个[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)使其度规变为常数的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)都是平直的，因此是一个平庸的[真空解](@keyword=vacuum_solution|lang=zh-CN|style=Feynman)。

### 机器中的幽灵：没有物质的曲率

所以，平直[时空](@keyword=space_time|lang=zh-CN|style=Feynman)是一个[真空解](@keyword=vacuum_solution|lang=zh-CN|style=Feynman)。但它是*唯一*的解吗？如果 $R_{\mu\nu} = 0$，是否意味着所有曲率都必须消失？这正是故事变得真正有趣的地方。

把完整的黎曼张量 $R_{\alpha\beta\gamma\delta}$ 看作[时空曲率](@keyword=spacetime_curvature|lang=zh-CN|style=Feynman)的全部特性。事实证明，这个特性有两种截然不同的性格。一部分是里奇张量 $R_{\mu\nu}$。这部分与局部物质和能量的存在直接相关，就像保龄球在床垫上造成的凹陷。真空方程 $R_{\mu\nu} = 0$ 是一个声明，即“这里”没有保龄球。

但[黎曼张量](@keyword=riemann_tensor|lang=zh-CN|style=Feynman)还有另一部分，一个更难以捉摸的角色，叫做**[外尔张量](@keyword=weyl_tensor|lang=zh-CN|style=Feynman)** $C_{\alpha\beta\gamma\delta}$。[外尔张量](@keyword=weyl_tensor|lang=zh-CN|style=Feynman)描述了即使在没有局部源的情况下也能存在的曲率。它是[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)的“自由”部分。它描述了潮汐力——你[坠入黑洞](@keyword=black_hole_infall|lang=zh-CN|style=Feynman)时会感受到的拉伸和挤压——而且它正是作为**引力波**在宇宙中传播的部分。它是床垫上向外传播的涟漪，在保龄球被移走后很久依然存在。

在四维真空[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中，出现了一个美妙的简化。由于里奇张量被强制为零，黎曼张量变得与外尔张量完全相同。
$$R_{\alpha\beta\gamma\delta} = C_{\alpha\beta\gamma\delta} \quad (\text{in vacuum})$$
这是一个宏伟的洞见！它告诉我们，真空中存在的任何及所有曲率都属于这种自由的、潮汐性的、传播性的类型。空旷空间这部机器中的幽灵就是[外尔张量](@keyword=weyl_tensor|lang=zh-CN|style=Feynman)。

这引出了一个强有力的结论。如果我们发现一个真空[时空](@keyword=space_time|lang=zh-CN|style=Feynman)（$R_{\mu\nu}=0$），同时出于某种原因它也没有[潮汐力](@keyword=tidal_forces|lang=zh-CN|style=Feynman)（即 $C_{\alpha\beta\gamma\delta}=0$），会怎样？如果曲率的里奇部分和外尔部分都为零，那么整个[黎曼张量](@keyword=riemann_tensor|lang=zh-CN|style=Feynman)必定为零。该[时空](@keyword=space_time|lang=zh-CN|style=Feynman)没有任何曲率。它必定是我们的老朋友，平直的[闵可夫斯基空间](@keyword=minkowski_space|lang=zh-CN|style=Feynman)。一个非平庸的[真空解](@keyword=vacuum_solution|lang=zh-CN|style=Feynman)*必须*有一个非零的外尔张量。

我们生活的维度数量在这里至关重要。在一个假设只有两个空间维度和一个时间维度（3D[时空](@keyword=space_time|lang=zh-CN|style=Feynman)）的世界里，由于一个数学上的巧合，[外尔张量](@keyword=weyl_tensor|lang=zh-CN|style=Feynman)总是恒等于零。因此，在3D中，如果你施加真空条件 $R_{\mu\nu}=0$，整个黎曼张量会自动消失。这意味着在一个(2+1)维的宇宙中，空旷空间总是平直的。没有（标准类型的）[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)，也没有引力波。我们研究的丰富引力现象是我们生活在四维空间中的直接结果，在那里外尔张量可以自由驰骋。

### 一个简单的宇宙：[黑洞解](@keyword=black_hole_solutions|lang=zh-CN|style=Feynman)

有了这种理解，我们终于可以去寻找那些真正栖息在真空中的有趣野兽：非平直解。这些[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的形状不是由局部物质决定的，而是由其他地方的质能集中，或者可能是由某次灾难性事件遗留下来的。

其中最著名的是**[史瓦西解](@keyword=schwarzschild_solution|lang=zh-CN|style=Feynman)**，它描述了任何不旋转的球对称物体（如恒星或行星）外部的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)。令人惊奇的是，一项被称为**[伯克霍夫定理](@keyword=birkhoff_s_theorem|lang=zh-CN|style=Feynman)**的结论证明，要得到这个解，你唯一需要做的物理假设就是[时空](@keyword=space_time|lang=zh-CN|style=Feynman)是球对称的。你不需要假设恒星是静止的。即使恒星以完全球对称的方式脉动、收缩或爆炸，其外部的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)也保持完全静止和不变。它就是[史瓦西度规](@keyword=schwarzschild_metric|lang=zh-CN|style=Feynman)。任何球对称的运动都被隐藏起来；外部世界感受不到引力波。这些方程是刚性的，它们为一个对称的真空指定了一个唯一的、静态的答案。

如果产生曲率的物体在旋转怎么办？这是一个难得多的问题，但它的解更加惊人。结果是**[克尔解](@keyword=kerr_solution|lang=zh-CN|style=Feynman)**，它描述了一个旋转的[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)。几十年来，物理学家们一直在想，是否可能存在其他类型的[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)，比如更崎岖不平的，或者具有反映其坍缩前杂乱物体特性的奇怪属性的[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)。答案以**“无毛”定理**的形式出现。

其中最强大的定理之一是 Israel-Carter-Robinson 唯一性定理。它指出，如果你在一个原本空无一物的宇宙中有一个稳定的、[轴对称](@keyword=axial_symmetry|lang=zh-CN|style=Feynman)的、不带电的[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)，它*必须*是一个[克尔黑洞](@keyword=kerr_black_hole|lang=zh-CN|style=Feynman)。最终状态仅由两个数字唯一描述：它的总质量 $M$ 和总角动量 $J$。所有其他细节——无论它是由恒星、尘埃云还是一堆旧电视机形成的——都被辐射掉了。[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)没有“毛发”。

想一想这其中惊人的含义。从一颗坍缩恒星的无限复杂性中，真空中的引力定律将其本质提炼为仅仅两个参数。这是从混沌中涌现出简单的终极范例。这些解，[史瓦西解](@keyword=schwarzschild_solution|lang=zh-CN|style=Feynman)和[克尔解](@keyword=kerr_solution|lang=zh-CN|style=Feynman)，不仅仅是数学上的奇珍。它们就是我们生活的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)，是我们宇宙中每一颗恒星、行星和[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的模板。它们是空旷空间那寂静、优美而强大的形状。