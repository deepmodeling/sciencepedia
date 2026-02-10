## 应用与跨学科联系

我们花了一些时间探索几何分析的复杂机制——一个由极小曲面、[共形变换](@keyword=conformal_transformations|lang=zh-CN|style=Feynman)和曲率构成的世界。你可能会问，这一切有什么用？这些只是数学家在黑板上玩的美丽抽象游戏吗？令人欣喜的答案是：不是！这套由[Richard Schoen](@keyword=richard_schoen|lang=zh-CN|style=Feynman)及其同时代人发展的机制，原来是一串万能钥匙，解开了在初看起来相隔甚远的领域中的深刻问题。我们即将踏上一段旅程，从[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的质量到空间本身的形状，我们将发现这些看似迥异的领域被优雅而强大的几何原理紧密地联系在一起。

### 引力的几何学与宇宙的质量

让我们从一些有形的东西开始——至少，像[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)那样有形的东西。Einstein的广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)告诉我们，引力不是一种力，而是时空曲率的表现。物质告诉[时空](@keyword=space_time|lang=zh-CN|style=Feynman)如何弯曲，[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的曲率告诉物质如何运动。但这引出了一个相当宏大的问题：一个物体，甚至整个孤立宇宙的*总*质量是多少？你不能简单地把它放在秤上！

物理学家们提出了一个名为[ADM质量](@keyword=adm_mass|lang=zh-CN|style=Feynman)的概念，以Arnowitt、Deser和Misner的名字命名。其思想是通过观察空间几何在遥远的“空间无穷远处”偏离完美平坦的程度来测量质量。事实证明，我们学到的[共形几何](@keyword=conformal_geometry|lang=zh-CN|style=Feynman)语言非常适合于此。对于一个由[Schwarzschild时空](@keyword=schwarzschild_spacetime|lang=zh-CN|style=Feynman)描述的简单的、不旋转的[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)，其[ADM质量](@keyword=adm_mass|lang=zh-CN|style=Feynman)$M$可以通过检查一个[特殊函数](@keyword=special_functions|lang=zh-CN|style=Feynman)——即那个能将几何“拉平”的[共形因子](@keyword=conformal_factor|lang=zh-CN|style=Feynman)——的渐近行为来找到 [@problem_id:890343]。质量并非“内部”的某个东西；它是一个表征整个空间几何的数字。

这引出了一个更深刻的原理：**[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)** (Positive Mass Theorem)。从物理角度思考，既然引力是吸引的，你会[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)一个[孤立系统](@keyword=isolated_systems|lang=zh-CN|style=Feynman)的总能量（也就是质量）是正的。你不可能拥有一个整体上排斥物体的[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)。[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)就是对这一直觉的严格[数学证明](@keyword=mathematical_proof|lang=zh-CN|style=Feynman)。对于任何满足合理物理条件（非负的局域能量密度）的孤立引力系统，其总[ADM质量](@keyword=adm_mass|lang=zh-CN|style=Feynman)必须是非负的，$m_{\mathrm{ADM}} \ge 0$。此外，质量为零的唯一途径是空间完全空荡且平坦——没有物质，没有引力，什么都没有。

Schoen和[Shing-Tung Yau](@keyword=shing_tung_yau|lang=zh-CN|style=Feynman)首次使用他们强大的极小曲面技术证明了这一定理。其背后的直觉虽然技术性很强，但却十分精妙：他们证明如果一个空间具有负质量，你就可以构造出一种被迫坍缩的几何“气泡”。但通过使用极小曲面——可以把它们想象成跨越空间部分的完美高效的皂膜——他们证明了这种坍缩是不可能的，从而导致矛盾。在某种意义上，一小片[皂膜](@keyword=soap_film|lang=zh-CN|style=Feynman)维系着宇宙，并保证了其质量为正！

值得注意的是，[Edward Witten](@keyword=edward_witten|lang=zh-CN|style=Feynman)发现了第二个完全不同的证明，他使用了来自量子[场论](@keyword=field_theory|lang=zh-CN|style=Feynman)的思想，涉及一种称为[旋量](@keyword=spinors|lang=zh-CN|style=Feynman) (spinor) 的对象 [@problem_id:3036753]。这揭示了经典引力与量子世界之间惊人且意想不到的联系。更引人入胜的是，对于我们日常经验的维度$n=3$，Witten的优雅证明*总是*适用的，因为根据一个深刻的拓扑学事实，每个可定向的三维空间都具有他的论证所需的“旋量”性质 [@problem_id:3036753]。这两个解决同一基本问题的不同证明，优美地展示了数学与物理的统一性。

故事并未就此结束。**[黎曼Penrose不等式](@keyword=riemannian_penrose_inequality|lang=zh-CN|style=Feynman)** (Riemannian Penrose Inequality) 将这一思想更推进了一步。它指出，一个[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的总质量必须至少与其[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的质量当量一样大。质量不能全部“隐藏”在[事件视界](@keyword=event_horizon|lang=zh-CN|style=Feynman)之后。证明这个不等式是[数学物理](@keyword=mathematical_physics|lang=zh-CN|style=Feynman)学中的一个重大挑战，而最成功的方法之一是使用一个称为[逆平均曲率流](@keyword=inverse_mean_curvature_flow|lang=zh-CN|style=Feynman)的过程，该过程再次依赖于[极小曲面](@keyword=minimal_surfaces|lang=zh-CN|style=Feynman)理论。有趣的是，这种证明技术在维度 $n \le 7$ 时非常有效，但在维度 $n \ge 8$ 时遇到了障碍。为什么？因为证明中使用的极小曲面在更高维度中可能产生“[奇点](@keyword=singularities|lang=zh-CN|style=Feynman)”——即它们不光滑的点或折痕——而我们的数学工具难以驾驭这些皱褶 [@problem_id:3036636]。对[黑洞质量](@keyword=black_hole_mass|lang=zh-CN|style=Feynman)的探索，出人意料地取决于高维[皂膜](@keyword=soap_film|lang=zh-CN|style=Feynman)的抽象[正则性理论](@keyword=regularity_theory|lang=zh-CN|style=Feynman)！

### 宇宙可以有哪些形状？[Yamabe问题](@keyword=yamabe_problem|lang=zh-CN|style=Feynman)

在用几何学衡量了宇宙之后，让我们转向一个纯粹美学的问题。给定一个[拓扑空间](@keyword=topological_spaces|lang=zh-CN|style=Feynman)——一个像橡胶片一样灵活、无形的物体——我们能否赋予它一个“最佳”或“最美”的几何？在几何学中，“美”通常意味着“均匀”。**[Yamabe问题](@keyword=yamabe_problem|lang=zh-CN|style=Feynman)**正是这样提问的：我们能否在一个给定的共形类（一组通过局域缩放相关的几何）中找到一个具有*[常标量曲率](@keyword=constant_scalar_curvature|lang=zh-CN|style=Feynman)*的几何？这就像试图熨平一块褶皱的布料，使其各处的[张力](@keyword=tension_force|lang=zh-CN|style=Feynman)都相同。

这个问题的解决方案由Schoen完成，是一项里程碑式的成就。主要的障碍是一种称为“起泡”的现象，即一列不断改进的度量可能会突然在单一点上产生[无限集](@keyword=infinite_sets|lang=zh-CN|style=Feynman)中的曲率，从而无法形成光滑的解。Schoen的天才之处在于将这个问题与[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)联系起来 [@problem_id:3036796]。他证明，如果这样一个气泡在某一点形成，它周围的几何将看起来像一个完整的、孤立的宇宙。这个“气泡宇宙”将具有非负的[标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman)，并且——这是关键的洞见——它的[ADM质量](@keyword=adm_mass|lang=zh-CN|style=Feynman)恰好为零 [@problem_id:3036742]。

但是等等！我们刚从[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)中学到，唯一质量为零的宇宙是平坦的[欧几里得空间](@keyword=euclidean_space|lang=zh-CN|style=Feynman)。这导致了一个矛盾，证明了这种曲率气泡是无法形成的（除非[流形](@keyword=manifold|lang=zh-CN|style=Feynman)本身就是一个简单的圆球面）。因此，对于一大类[流形](@keyword=manifold|lang=zh-CN|style=Feynman)，“最佳”几何的存在性得到了保证。在一个惊人的转折中，一个诞生于引力物理学的定理成为解决纯粹几何学中一个基本问题的关键。

### 塑造空间：手术与[几何刚性](@keyword=geometric_rigidity|lang=zh-CN|style=Feynman)

有了解决[Yamabe问题](@keyword=yamabe_problem|lang=zh-CN|style=Feynman)和证明[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)的强大工具，我们就可以开始提出真正探索空间形状（拓扑）和大小（几何）之间关系的问题。如果我们对一个[流形](@keyword=manifold|lang=zh-CN|style=Feynman)进行手术，切掉一块再粘上另一块，会发生什么？

一个被称为**Gromov-Lawson-[Schoen-Yau](@keyword=schoen_yau|lang=zh-CN|style=Feynman)手术定理**的卓越结果给出了部分答案。它指出，如果你有一个允许具有[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)度量的[流形](@keyword=manifold|lang=zh-CN|style=Feynman)，并且你进行了一次“[余维数](@keyword=codimension|lang=zh-CN|style=Feynman) $\ge 3$”的手术（你可以将其视为一个足够小且局域化的操作），那么得到的新[流形](@keyword=manifold|lang=zh-CN|style=Feynman)*也*允许具有[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的度量 [@problem_id:3036717]。拥有[正曲率](@keyword=positive_curvature|lang=zh-CN|style=Feynman)几何的性质在这种拓扑修改下是稳健的。然而，对于较低[余维数](@keyword=codimension|lang=zh-CN|style=Feynman)的手术，这种保持性会失效，这表明拓扑与几何之间的相互作用是微妙的。

当然，并非所有[流形](@keyword=manifold|lang=zh-CN|style=Feynman)都能拥有[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)。不起眼的环面，即甜甜圈的形状，就是一个典型的例子。它的自然状态是“平坦的”。[Gauss-Bonnet定理](@keyword=gauss_bonnet_theorem|lang=zh-CN|style=Feynman)表明，对于一个[二维环面](@keyword=2_torus|lang=zh-CN|style=Feynman)，其总曲率必须为零，所以不可能处处为正。Schoen和Yau使用[极小曲面](@keyword=minimal_surfaces|lang=zh-CN|style=Feynman)证明了这一点在3到7维成立，而Gromov和Lawson后来使用旋量技术给出了适用于所有维度的替代证明 [@problem_id:3035399]。这表明某些拓扑形状天生就存在一种“阻碍”，使其无法拥有某些类型的优美几何。

### 球面及其相似者：夹挤曲率与[奇异结构](@keyword=exotic_structures|lang=zh-CN|style=Feynman)

这把我们带到了最后一个主题：刚性。如果一个空间*几乎*看起来像一个球面，它是否就*必须*是一个球面？这个问题由著名的**[微分球定理](@keyword=differentiable_sphere_theorem|lang=zh-CN|style=Feynman)** (Differentiable Sphere Theorem) 回答。什么叫“几乎看起来像一个球面”？条件是它的截面曲率（一个点上所有可能的二维切片的曲率）必须是正的，并且“夹挤”得非常紧密。

这里的神奇数字是$1/4$。该定理在其由Brendle和Schoen证明的最强形式中指出，如果一个紧致、单连通的[流形](@keyword=manifold|lang=zh-CN|style=Feynman)在每一点的[截面曲率](@keyword=sectional_curvature|lang=zh-CN|style=Feynman)都是严格$1/4$夹挤的（即最小曲率与最大曲率之比总是大于$1/4$），那么该[流形](@keyword=manifold|lang=zh-CN|style=Feynman)必须与标[准球面](@keyword=director_sphere|lang=zh-CN|style=Feynman)*[微分同胚](@keyword=diffeomorphism|lang=zh-CN|style=Feynman)* [@problem_id:2994801] [@problem_id:2994702]。这个证明是[几何分析](@keyword=geometric_analysis|lang=zh-CN|style=Feynman)的又一杰作，利用了[Ricci流](@keyword=ricci_flow|lang=zh-CN|style=Feynman)——一种像热流一样演化度量的过程——来表明任何这样的夹挤度量都会平滑地变形为完美浑圆的球面度量。那些恰好是$1/4$夹挤但不是球面的空间，比如[复射影空间](@keyword=complex_projective_space|lang=zh-CN|style=Feynman)，表明这个定理是完全精确的；你不能放宽这个严格不等式。

但该定理最惊人的推论在于其最后一个词：“微分同胚”。在七维及更高维度，数学家们发现了一系列奇异的物体，称为**[奇异球面](@keyword=exotic_spheres|lang=zh-CN|style=Feynman)** (exotic spheres)。这些[流形](@keyword=manifold|lang=zh-CN|style=Feynman)在拓扑上与标[准球面](@keyword=director_sphere|lang=zh-CN|style=Feynman)相同（它们可以被连续地拉伸和弯曲成一个标[准球面](@keyword=director_sphere|lang=zh-CN|style=Feynman)），但具有不同的“[光滑结构](@keyword=smooth_structure|lang=zh-CN|style=Feynman)”（它们“皱巴巴”的方式使得永远无法被熨平以匹配标[准球面](@keyword=director_sphere|lang=zh-CN|style=Feynman)）。它们是外星世界，在拓拓学家看来是球面，但对几何学家来说感觉不同。

[微分球定理](@keyword=differentiable_sphere_theorem|lang=zh-CN|style=Feynman)对这些奇异物体做出了惊人的裁决 [@problem_id:2990834]。它说，如果一个空间——任何空间，标准的或奇异的——足够光滑以至于可以测量其曲率，并且它满足严格的$1/4$夹挤条件，那么它必须与*标准*球面微分同胚。这意味着没有[奇异球面](@keyword=exotic_spheres|lang=zh-CN|style=Feynman)能够支持如此优美夹挤的[正曲率](@keyword=positive_curvature|lang=zh-CN|style=Feynman)几何。这个强大的几何约束是如此刚性，以至于它完全杜绝了拓扑奇异性的可能性。几何的美丽和均匀性迫使底层的[光滑结构](@keyword=smooth_structure|lang=zh-CN|style=Feynman)成为我们熟悉和喜爱的那个。

### 一个统一的愿景

从[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的[ADM质量](@keyword=adm_mass|lang=zh-CN|style=Feynman)到[奇异球面](@keyword=exotic_spheres|lang=zh-CN|style=Feynman)上的皱褶，我们见证了[Richard Schoen](@keyword=richard_schoen|lang=zh-CN|style=Feynman)及其合作者的思想如何跨越数学和物理学。这段旅程揭示了一个充满深刻且常常出人意料的相互联系的世界。物理原理引导着解决几何学中的抽象问题，而纯粹几何学的工具反过来又提供了唯一足够精确的语言来阐明和证明关于我们宇宙的基本事实。这证明了一个事实：在追求真理与美的过程中，学科之间的界限并非高墙，而是等待被发现的桥梁。