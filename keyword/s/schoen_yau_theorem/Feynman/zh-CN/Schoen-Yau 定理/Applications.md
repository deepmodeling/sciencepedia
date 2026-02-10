## 应用与跨学科联系

我们花了一些时间，可以说是亲身实践，仔细研究了[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)的复杂机制。我们看到 Schoen 和 Yau 如何以非凡的才智，利用极小曲面那如蛛丝般的薄膜，证明了关于引力本质的某个极其稳固的结论。但是，这个定理究竟有何用处？它仅仅是挂在墙上的一张证书，证明 Einstein 理论在数学上的一致性吗？还是它是一个实用的工具，一把能打开我们甚至未曾想象过的新房间的钥匙？

答案，正如在科学的伟大冒险中常有的那样，是两者兼而有之。[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)不仅是一个答案；它是一系列新问题和新答案的开端。它为我们理解引力提供了坚实的基础，但其影响涟漪般[扩散](@keyword=dispersal|lang=zh-CN|style=Feynman)开来，触及[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的几何、质量的定义本身，甚至解决了那些初看起来似乎完全属于另一个世界的纯数学问题。现在让我们来参观一下这些应用，并在此过程中，见证这个单一而强大的理念如何为科学思想的各个角落带来惊人的统一。

### [时空](@keyword=space_time|lang=zh-CN|style=Feynman)的稳定性

首先，[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)是一个关于稳定性的陈述。它回答了人们可以对引力理论提出的最基本问题：真空是稳定的吗？如果你从一个空荡荡的、平直的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)开始，什么也不做，它会保持空荡荡和平直吗？还是它会自发地衰变成一个负能量状态，并在此过程中辐射出正能量，就像一台宇宙[永动机](@keyword=perpetual_motion|lang=zh-CN|style=Feynman)？

这样的情景对物理学来说将是一场灾难。我们的宇宙将从根本上不稳定，像一座一触即溃的纸牌屋。[时空](@keyword=space_time|lang=zh-CN|style=Feynman)[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)证明了这场灾难不会发生。它不仅考虑了宇宙的一个静态快照，还考虑了[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的一个一般切片，一个由度量 $g$ 及其变化率——[外在曲率](@keyword=extrinsic_curvature|lang=zh-CN|style=Feynman) $K$ 所定义的初始数据集。这些是由物质和能量的分布决定的，由能量密度 $\mu$ 和[动量密度](@keyword=momentum_density|lang=zh-CN|style=Feynman) $J$ 描述。

只要物质是“物理上合理的”——即遵守所谓的优势[能量条件](@keyword=energy_conditions|lang=zh-CN|style=Feynman)，该条件本质上说能量的[传播速度](@keyword=propagation_velocity|lang=zh-CN|style=Feynman)不能超过光速——该定理就保证系统的总能量 $E$ 大于或等于其[总动量](@keyword=total_linear_momentum|lang=zh-CN|style=Feynman) $|P|$ 的大小 ([@problem_id:3025843], [@problem_id:3001562])。用[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)的语言来说，这意味着总的能量-动量[四维矢量](@keyword=4_vectors|lang=zh-CN|style=Feynman)是“未来指向且非类空的”。这是一个技术性术语，描述了一个简单而令人安心的事实：宇宙的总质量，定义为 $m = \sqrt{E^2 - |P|^2}$，是实数且非负的。孤立系统不能有虚数质量，那将对应于[超光速](@keyword=superluminal_velocity|lang=zh-CN|style=Feynman)的不稳定性。空间不会自发地“沸腾”出[负能量](@keyword=negative_energy|lang=zh-CN|style=Feynman)的幻影。

该定理的“刚性”部分更为深刻。如果总质量恰好为零呢？什么样的宇宙会有 $E = |P|$？定理给出的答案是明确的：只有一种。一个总质能为零的宇宙，其整体必须是完全空旷平直的闵可夫斯基时空。任何一点物质、任何一丝引力波的涟漪、任何非平凡的几何结构，都会给宇宙一个正的、非零的质量。没有办法将正能量物质[排列](@keyword=permutation|lang=zh-CN|style=Feynman)组合，使其总和恰好抵消为零。引力，在其本质上，总是累加的。

### 称量[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)

该定理告诉我们质量是正的。但我们能说得更多吗？如果一个宇宙包含一个[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)，你会想象这应该贡献一定量的质量。[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)有一个视界，一个有去无回的表面，其面积为 $A$。这个面积是否对宇宙能拥有的*最小*质量设置了一个限制？

答案是肯定的，它以优美而强大的**Penrose 不等式**的形式出现 ([@problem_id:3036419])。它指出，包含[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的总 ADM 质量 $m$ 必须至少为：

$$
m \ge \sqrt{\frac{A}{16\pi}}
$$

这是对[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)的绝妙改进。它说天平的读数不能只是一个正数；它必须读取一个至少与它所包含的[黑洞面积](@keyword=black_hole_area|lang=zh-CN|style=Feynman)相对应的质量一样大的数值。[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)之外的所有其他物质和[引力能](@keyword=gravitational_energy|lang=zh-CN|style=Feynman)只能增加更多的质量；它们永远不能从中减去。如果你增加更多物质，质量 $m$ 可能会增加，或者视界面积 $A$ 可能会增加，但这个不等式将永远成立。

这个不等式在某种程度上是全息原理的先驱——即空间体积内的物理学可以由其边界上的理论来描述的观点。在这里，整个[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的一个全局属性——其总质量，在“无穷远处”测量——被其内部深处一个边界的局部属性——[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)视界的面积——所下界。这个不等式的证明本身就是一段发现之旅，由 Huisken 和 Ilmanen 使用一种称为“[逆平均曲率流](@keyword=inverse_mean_curvature_flow|lang=zh-CN|style=Feynman)”的演化[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)而著名地实现。他们证明了，可以从视界处的[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)（等于 $\sqrt{\frac{A}{16\pi}}$）开始，随着[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)向[外流](@keyword=external_flow|lang=zh-CN|style=Feynman)动到无穷远，这个质量永不减少。在无穷远处，它变成了 ADM 质量，从而证明了该不等式。这就好像几何本身强制了质量信息从[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)向宇宙的单向流动。

### 从宇宙到实验室：准局域质量

ADM 质量和 Penrose 不等式涉及的是*整个*宇宙。这很宏大，但如果你是一个只想知道单个恒星或星系质量的天体物理学家，这有点不切实际。当质量本身是[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)的属性，而[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)无处不在时，你如何称量宇宙的一个有限部分？

这就是臭名昭著的“准局域质量”问题。其中最成功的方法之一是 Brown–York 质量，它通过比较一个区域边界[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的几何与[平直空间](@keyword=flat_space|lang=zh-CN|style=Feynman)中参考[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的几何来定义该区域的质量。但是，你如何证明这个听起来合理的定义对于一个包含普通物质的区域总是正的呢？

再一次，[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)通过 Shi 和 Tam 的一个极其巧妙的论证提供了关键 ([@problem_id:3001566])。这个想法是一种“偷天换日”。你取你想要称量的有限空间区域，然后扔掉它外面真实的宇宙其余部分。然后，你数学上构造一个新的、伪造的外部，将其粘贴到你区域的边界上。这个伪造的外部被精心设计成[渐近平坦](@keyword=asymptotic_flatness|lang=zh-CN|style=Feynman)，并且关键是，其标量曲率为零。

现在你创造了一个完整的、自洽的，但却是人造的宇宙。神奇之处在于：一个计算表明，这个整个人造宇宙的 ADM 质量恰好等于你开始时原始区域的 Brown–York 准局域质量！现在你可以将[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)的全部威力施加到这个人造宇宙上。由于它处处具有非负标量曲率（在原始区域内根据假设为非负，在伪造部分为零），其 ADM 质量必须是非负的。因此，你原始区域的准局域质量必须是非负的。这是一个将局部问题转化为全局问题的绝佳例子，目的只是为了用[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)这把强大的锤子来解决它。

### 几何学的惊喜：空间的形状

到目前为止，我们的旅程一直停留在物理学和引力的范畴内。但现在，我们急转弯进入纯数学的世界，[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)在这里作为一个意想不到且不可或缺的英雄出现。这个故事是关于**Yamabe 问题**的。

Yamabe 问题提出了一个看似简单的几何问题：任何弯曲的形状（准确地说，是一个紧致黎曼流形）是否都可以通过[共形形变](@keyword=conformal_deformation|lang=zh-CN|style=Feynman)——逐点拉伸或收缩，而不撕裂——使其[标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman)处处变为常数？想象一个凹凸不平、布满皱纹的气球。你总能将它重新充气成一个完美的、均匀弯曲的形状吗？

几十年来，这个问题一直未能得到完全解决。主要的困难在于分析：当试图通过最小化某个能量泛函（Yamabe 泛函）来找到理想的“拉伸因子”时，能量可能会集中在单一点上，形成一个“气泡”，从而阻碍了光滑解的存在 ([@problem_id:3001559])。

是 [Richard Schoen](@keyword=richard_schoen|lang=zh-CN|style=Feynman) 看到了与引力的惊人联系。他意识到，如果你无限放大这些假想的气泡之一，你看到的几何将会完全像一个完备、非紧、[渐近平坦](@keyword=asymptotic_flatness|lang=zh-CN|style=Feynman)的[流形](@keyword=manifold|lang=zh-CN|style=Feynman) ([@problem_id:3036742])。然后你可以问：这个“气泡宇宙”的 ADM 质量是多少？

Schoen 的神来之笔是证明了一个将气泡能量与 Yamabe 泛函联系起来的公式。该公式表明，如果 Yamabe 问题*没有*解，那一定是因为会形成一个 ADM 质量恰好为零的气泡。但是等等！这个气泡宇宙，由一个具有非负[标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman)的[流形](@keyword=manifold|lang=zh-CN|style=Feynman)形成，其本身也必须具有非负[标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman)。现在陷阱已经设好。[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)的刚性部分告诉我们，唯一具有非负标量曲率和零质量的[渐近平坦流形](@keyword=asymptotically_flat_manifold|lang=zh-CN|style=Feynman)就是平直的[欧几里得空间](@keyword=euclidean_space|lang=zh-CN|style=Feynman)本身！这导致了一个矛盾，表明这种有问题的、无质量的气泡不可能形成（至少在许多重要情况下是这样）。因此，Yamabe 问题的解必须存在。

在这里，我们从一个全新的角度看待[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)。一个为确保 Einstein 物理宇宙稳定性而锻造的定理，跨越学科，解决了一个关于抽象空间可能形状的基本问题。这是数学深刻而常被隐藏的统一性的一个惊人证明。同样值得注意的是，[Schoen-Yau](@keyword=schoen_yau|lang=zh-CN|style=Feynman) 最初证明 PMT 本身也有局限性，只在维度 $n \le 7$ 时有效，因为高维中极小曲面可能出现[奇点](@keyword=singularities|lang=zh-CN|style=Feynman)——这是一个有趣的窗口，揭示了我们数学工具的局限性如何塑造我们知识的前沿 ([@problem_id:3005223])。

### 一个宏大的分类：宇宙可以有哪些形状？

有了这些强大的思想，我们可以尝试一件真正大胆的事情：创建一个可以支持[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)度量的三维宇宙所有可能形状的完整列表。

思考具有[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的空间是很自然的。在某种意义上，它们是最“行为良好”或“受约束”的几何。那么，名单上有哪些形状呢？答案来自两种思想流派的结合，一种是构造性的，一种是阻碍性的，两者都与 Schoen 和 Yau 的工作有关。

首先，**阻碍**：用于证明[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)的相同极小曲面技术可以被改造，以证明许多[流形](@keyword=manifold|lang=zh-CN|style=Feynman)*不能*容许[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的度量。例如，环面（甜甜圈的形状）就不能。更一般地，任何“非球面”[流形](@keyword=manifold|lang=zh-CN|style=Feynman)——其[高阶同伦群](@keyword=higher_homotopy_groups|lang=zh-CN|style=Feynman)是平凡的[流形](@keyword=manifold|lang=zh-CN|style=Feynman)——都与[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)不相容 ([@problem_id:3035420])。这样的空间在拓扑上过于“庞大”或“松散”，无法被正曲率拉紧。

其次，**构造**：Misha Gromov 和 Blaine Lawson 发展了一种强大的[割补理论](@keyword=geometric_surgery|lang=zh-CN|style=Feynman)。他们表明，如果你从一个具有[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的形状（如球面）开始，你可以对其进行割补——切掉一块再粘上另一块——只要割补不太剧烈（具体来说，其余维必须至少为 3），得到的形状也将容许[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的度量 ([@problem_id:3032113])。

现在，我们引入 [3-流形](@keyword=3_manifolds|lang=zh-CN|style=Feynman)拓扑学的最高成就：Perelman 对[几何化猜想](@keyword=geometrization_conjecture|lang=zh-CN|style=Feynman)的证明。这个定理为所有 [3-流形](@keyword=3_manifolds|lang=zh-CN|style=Feynman)提供了一套“乐高积木”。它说，任何闭的、可定向的 [3-流形](@keyword=3_manifolds|lang=zh-CN|style=Feynman)都可以被切割成素分解块，并且每个块都属于八种几何类型之一。

以下是宏大的综合 ([@problem_id:3032089])：
1.  取任何 [3-流形](@keyword=3_manifolds|lang=zh-CN|style=Feynman) $M$。使用素分解将其分解为其乐高积木块。
2.  使用 [Schoen-Yau](@keyword=schoen_yau|lang=zh-CN|style=Feynman) 阻碍法，扔掉所有“不合法”的块——那些不能有[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的非球面块。
3.  剩下的唯一块是球形块（[3-球面](@keyword=s3_sphere|lang=zh-CN|style=Feynman)的商，$S^3/\Gamma$）和[流形](@keyword=manifold|lang=zh-CN|style=Feynman) $S^2 \times S^1$。
4.  Gromov-Lawson 的构造确保了我们可以将这些合法的块重新粘合在一起（通过[连通和](@keyword=connected_sum|lang=zh-CN|style=Feynman)操作，这是一种余维为 3 的割补），并且得到的[流形](@keyword=manifold|lang=zh-CN|style=Feynman)仍然会容许[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)的度量。

因此，我们得到了一个完整且惊人优雅的分类：一个闭的 [3-流形](@keyword=3_manifolds|lang=zh-CN|style=Feynman)容许[正标量曲率](@keyword=positive_scalar_curvature|lang=zh-CN|style=Feynman)度量，当且仅当它是一些球形[空间形式](@keyword=space_forms|lang=zh-CN|style=Feynman)和 $S^2 \times S^1$ 的副本的[连通和](@keyword=connected_sum|lang=zh-CN|style=Feynman)。一个关于曲率的问题被转化为一个完整的拓扑清单。这也许是所有应用中最辉煌的一个，源于引力物理学的思想与几何学和拓扑学的最深层结果相结合，最终告诉我们关于空间本身形状的终极答案。

从宇宙的粗犷稳定性到其可能形式的精细分类，[Schoen-Yau](@keyword=schoen_yau|lang=zh-CN|style=Feynman) 定理及其后继者已经证明是具有惊人力量和广度的工具。它是一个美丽的例证，说明一个单一、深刻的物理原理——能量是正的——如何在科学的殿堂中回响，揭示出一个连接我们的宇宙与纯粹思想抽象领域的丰富和谐结构。