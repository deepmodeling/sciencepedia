## 引言
在爱因斯坦广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)所描述的宇宙中，我们的物理直觉告诉我们，一个[孤立系统](@keyword=isolated_systems|lang=zh-CN|style=Feynman)的总能量（或质量）必须是正的。一个具有负质量的宇宙似乎违背了基本原理，然而几十年来，对这一观点的严格数学证明——即[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)——一直是一个难以企及的巨大挑战。本文将深入探讨 [Richard Schoen](@keyword=richard_schoen|lang=zh-CN|style=Feynman) 和 [Shing-Tung Yau](@keyword=shing_tung_yau|lang=zh-CN|style=Feynman) 的著名证明，这是[几何分析](@keyword=geometric_analysis|lang=zh-CN|style=Feynman)领域的一项杰作，它证实了这一物理直觉。接下来的章节将首先剖析该证明中精巧的“矛盾引擎”，探索其将物理能量转化为几何曲率并利用极小曲面性质的原理和机制。随后，我们将超越广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)，审视其应用和跨学科联系，探索这一强大的方法如何成为解决纯粹几何学中基本问题的一把万能钥匙。

## 原理与机制

### 从物理能量到几何曲率

在我们所经验的世界以及[经典物理学](@keyword=classical_physics|lang=zh-CN|style=Feynman)所描述的世界里，质量是一个顽固为正的量。一本书有质量，一颗行星有质量，但“负质量苹果”的想法只存在于科幻小说中。当爱因斯坦揭示他著名的方程 $E = mc^2$ 时，他告诉我们质量是能量的一种极其浓缩的形式。这加深了我们的直觉：一个行为良好的物理世界应该建立在正能量的基础之上。你不可能随处拥有“[负能量](@keyword=negative_energy|lang=zh-CN|style=Feynman)”；如果可以，你只需将它与正能量配对，就能无中生有地创造能量。

广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)采纳了这种物理直觉，并用几何学的语言将其编码。其正式表述被称为**优势[能量条件](@keyword=energy_conditions|lang=zh-CN|style=Feynman) (DEC)**。从本质上讲，优势[能量条件](@keyword=energy_conditions|lang=zh-CN|style=Feynman)是一个“宇宙速度极限”和一个正性要求的结合体。它断言，对于宇宙中任何地方的任何观察者来说，能量和动量的流动速度永远不能超过光速，并且他们测量的局部能量密度总是大于或等于零 [@problem_id:3036424]。这排除了各种奇异的、非物理的现象。

现在是见证奇迹的时刻。[爱因斯坦场方程](@keyword=einstein_s_field_equations|lang=zh-CN|style=Feynman)是连接宇宙的“物质”——能量和动量（由一个称为[应力-能量张量](@keyword=stress_energy_tensor|lang=zh-CN|style=Feynman) $T$ 的数学对象描述）——与这一切上演的“舞台”——[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的弯曲几何（由度量 $g$ 描述）之间的桥梁。这些方程精确地告诉我们物质和能量如何决定[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的曲率。

为了理解其后果，让我们想象在某一瞬间为宇宙拍下一张快照。这给了我们一个三维的空间“切片”。如果我们考虑最简单的情况——一个静态或**时间对称**的切片，在那个瞬间事物没有变化——[爱因斯坦方程](@keyword=einstein_s_equations|lang=zh-CN|style=Feynman)会得到极大的简化。在这样的切片上，[动量密度](@keyword=momentum_density|lang=zh-CN|style=Feynman) $J$ 为零，而优势[能量条件](@keyword=energy_conditions|lang=zh-CN|style=Feynman)仅要求局部能量密度 $\rho$ 为非负。关键在于：这种情况下广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)的[约束方程](@keyword=constraint_equations|lang=zh-CN|style=Feynman)给出了能量密度与该切片几何之间的直接联系。具体来说，我们三维空间的**标量曲率** $R_g$ 由以下公式给出：

$$ R_g = 16\pi \rho $$

既然我们已经从物理原理确定了 $\rho \ge 0$，那么我们空间的标量曲率也必然是非负的，即 $R_g \ge 0$ [@problem_id:3036424]。这是一个深刻的飞跃。一个关于物理学中能量本质的基本原理，被转化为了一个关于空间几何的具体陈述。这个几何条件——非负标量曲率——成为了构建[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)的基石。

### 宏大猜想：[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)

因此，一个物理上合理的宇宙，至少在一个静态时刻，对应于一个具有非负标量曲率的三维空间。这个空间还被假定为**[渐近平坦](@keyword=asymptotic_flatness|lang=zh-CN|style=Feynman)**的——这意味着如果你远离所有物质和能量，行至非常非常远的地方，空间的几何将变得与高中几何中学到的熟悉的、平坦的[欧几里得空间](@keyword=euclidean_space|lang=zh-CN|style=Feynman)无法区分。所有有趣的东西，比如由恒星和[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)产生的“引力井”，都包含在一个有限的区域内。

如何测量这样一个系统的总质量？你不需要深入其中，把所有东西加起来。正如我们可以通过观察远处行星的轨道（在那里太阳的引力很弱）来推断太阳的质量一样，[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)学者可以通过仔细考察空间几何在无穷远处*如何*趋于平坦来测量系统的总质量。这个量是一个[几何不变量](@keyword=geometric_invariants|lang=zh-CN|style=Feynman)，称为 **Arnowitt–Deser–Misner (ADM) 质量**，记作 $m_{\mathrm{ADM}}$。

于是，**[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)**做出了一个大胆而优美的断言。它指出，对于任何具有非负标量曲率（$R_g \ge 0$）的完备、[渐近平坦](@keyword=asymptotic_flatness|lang=zh-CN|style=Feynman)空间，其总 ADM 质量也必须是非负的（$m_{\mathrm{ADM}} \ge 0$）。此外，该定理还包含一个强有力的“刚性”陈述：质量恰好为零的唯一可能是，该空间完全空无一物且完美平坦——即与标准的[欧几里得空间](@keyword=euclidean_space|lang=zh-CN|style=Feynman) $(\mathbb{R}^n, \delta)$ 等距。任何非平凡的几何，任何对应于物质的肿块或凸起，*必定*贡献一个正的总质量 [@problem_id:3025806]。这正是 [Richard Schoen](@keyword=richard_schoen|lang=zh-CN|style=Feynman) 和 [Shing-Tung Yau](@keyword=shing_tung_yau|lang=zh-CN|style=Feynman) 著名证明所证实的猜想。但如何证明这样一个普适的陈述呢？你无法检查所有可能的宇宙。你需要构建一个逻辑机器，保证对所有宇宙都有效。

### 矛盾引擎：构造极小曲面

Schoen 和 Yau 的方法是[反证法](@keyword=reductio_ad_absurdum|lang=zh-CN|style=Feynman)的杰作，这种策略被称为*[归谬法](@keyword=reductio_ad_absurdum|lang=zh-CN|style=Feynman)*。其逻辑很简单：让我们假设该定理是错的，然后看看宇宙是否会陷入逻辑上的荒谬境地。所以，让我们进入一个假想的“如果”世界，其中存在一个空间，它具有非负的[标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman)（$R_g \ge 0$），但总质量为负（$m_{\mathrm{ADM}}  0$）。

负质量会*做什么*？在远离中心的地方，它的作用类似于一种“反引力”。它不是向内拉动物体，而是提供一种温和的、排斥性的推力。我们可以通过检查我们假想空间中遥远的[渐近平坦](@keyword=asymptotic_flatness|lang=zh-CN|style=Feynman)区域里巨大球面的曲率来观察这种效应。在一个正常的、正质量的宇宙中，引力向内拉动一个大球面的表面，使其曲率比平坦空间中同样大小的球面略“小”一些。在我们的负质量世界里，情况正好相反。排斥性的反引力向外推，使得这些巨大的球面“格外”弯曲。用几何学的语言来说，它们是**严格[平均凸](@keyword=mean_convex|lang=zh-CN|style=Feynman)**的 [@problem_id:3036442]。

这个看似微小的细节是启动引擎的关键。这些格外弯曲的球面充当了完美的、不可穿透的屏障。想象一下在一个金属线框里吹一个肥皂泡。肥皂膜会自然地形成一个在附着于线框的同时，表面积达到绝对最小的形状。Schoen 和 Yau 在宇宙尺度上做了类似的事情。他们考虑了所有被困在他们巨大的、[平均凸](@keyword=mean_convex|lang=zh-CN|style=Feynman)的球形屏障之一内部的可能[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)，并运用**[几何测度论](@keyword=geometric_measure_theory|lang=zh-CN|style=Feynman) (GMT)** 的强大工具证明了，其中必定存在一个面积绝对最小的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)。这被称为**[面积最小化超曲面](@keyword=area_minimizing_hypersurfaces|lang=zh-CN|style=Feynman)** [@problem_id:3033303]。

凭借其作为面积最小化者的本质，这个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)（我们称之为 $\Sigma$）具有两个显著的特性。首先，它是一个**[极小曲面](@keyword=minimal_surfaces|lang=zh-CN|style=Feynman)**，意味着它的[平均曲率](@keyword=mean_curvature|lang=zh-CN|style=Feynman)处处为零。它是绷紧的肥[皂膜](@keyword=soap_film|lang=zh-CN|style=Feynman)在更高维度上的完美类比，没有任何偏向一方或另一方的趋势。其次，同样重要的是，它是**稳定**的。这意味着如果你试图轻微地摆动或变形它，它的表面积只会增加（或者在最坏的情况下，在二阶上保持不变）。它舒适地坐落在一个“面积谷底”，而不是摇摇欲坠地栖息在一个“[鞍点](@keyword=saddle_point|lang=zh-CN|style=Feynman)”上 [@problem_id:3033312]。

通过让外部球形屏障变得无限大的极限过程，Schoen 和 Yau 证明了这个过程会锻造出一个延伸至无穷远的完备、非紧、稳定的极小曲面 $\Sigma$。负质量的假设不仅仅是一个闲置的假说；它已成为一个构造工具。它迫使我们假想的宇宙包含这个非常特殊的物体。

### 纸牌屋的崩塌：曲率与稳定性

到目前为止，我们这个 $m_{\mathrm{ADM}}  0$ 的“如果”世界已经成功地产生了一个美丽的、无限的、稳定的肥皂膜 $\Sigma$。但我们还没有使用我们另一个[初始条件](@keyword=initial_conditions|lang=zh-CN|style=Feynman)：[环境空间](@keyword=ambient_space|lang=zh-CN|style=Feynman)具有非负的[标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman)，$R_g \ge 0$。正是在这里，我们假想世界的两大支柱被证明存在致命的冲突。

一个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)*本身*的曲率与它*周围*空间的曲率之间存在着深刻而精确的关系。这个规则手册就是著名的**[高斯方程](@keyword=gauss_equation|lang=zh-CN|style=Feynman)**。与此同时，我们的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman) $\Sigma$ 是*稳定*的这一事实为我们提供了一个强大的约束，即**稳定性不等式**。这个不等式指出，[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)“弹回”以减小面积的趋势必须克服任何试图使其屈曲的外力。这些外力由空间的背景曲率描述，具体来说是一个称为[里奇曲率](@keyword=ricci_curvature|lang=zh-CN|style=Feynman)的量，$\mathrm{Ric}_g(\nu, \nu)$，它测量空间在垂直于 $\Sigma$ 方向上的弯曲程度。

Schoen 和 Yau 的巧妙之处在于，他们发现这两部分数学——[高斯方程](@keyword=gauss_equation|lang=zh-CN|style=Feynman)和稳定性不等式——可以结合起来 [@problem_id:3033317]。他们将[高斯方程](@keyword=gauss_equation|lang=zh-CN|style=Feynman)作为一种“罗塞塔石碑”，把稳定性不等式中的[里奇曲率](@keyword=ricci_curvature|lang=zh-CN|style=Feynman)项转换成一个由他们可以控制的量所组成的表达式：即[环境空间](@keyword=ambient_space|lang=zh-CN|style=Feynman)的标量曲率 $R_g$ 和 $\Sigma$ 本身的内蕴曲率。

一旦完成了这个代换，最终的矛盾便豁然开朗。当你代入条件 $R_g \ge 0$ 时，合并后的不等式导出了一个不可能的结论。它实际上表明，像 $\Sigma$ 这样的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)不可能存在。一个稳定的[极小曲面](@keyword=minimal_surfaces|lang=zh-CN|style=Feynman)试图尽可能地“平坦”，但周围空间的非负曲率迫使它以一种与稳定性根本不相容的方式弯曲。这是一场没有任何可能解决方案的几何拔河。

于是，宏大的矛盾就此产生：
1.  $m_{\mathrm{ADM}}  0$ 的假设迫使一个完备、稳定的[极小曲面](@keyword=minimal_surfaces|lang=zh-CN|style=Feynman) $\Sigma$ **存在** [@problem_id:3036442]。
2.  $R_g \ge 0$ 的假设禁止同一个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的**存在**。

既然我们的逻辑是健全的，那么唯一可能的失败必定在于我们的初始前提。那个质量可以为负的假想世界在逻辑上是不可能存在的。因此，任何此类系统的质量永远不能为负。它必须大于或等于零。定理得证。

### [时空](@keyword=space_time|lang=zh-CN|style=Feynman)中的一道皱纹：维度限制

眼尖的读者可能已经注意到，在我们的讨论中一直出现一条细则：[Schoen-Yau](@keyword=schoen_yau|lang=zh-CN|style=Feynman) 证明适用于维度为 $n$ 且 $3 \le n \le 7$ 的空间。维度 7 有什么神奇之处？为什么这个似乎借鉴了如此基本原理的宏伟机器，在我们试图将其应用于 8 维空间时会突然卡住？

答案在于我们在构造过程中做出的一个微妙但至关重要的假设：我们的面积最小化[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman) $\Sigma$ 是完美光滑的。整个论证，包括[高斯方程](@keyword=gauss_equation|lang=zh-CN|style=Feynman)的使用和积分，都依赖于 $\Sigma$ 是一个行为良好的[流形](@keyword=manifold|lang=zh-CN|style=Feynman)，没有尖点、扭结或其他“[奇点](@keyword=singularities|lang=zh-CN|style=Feynman)”。

长久以来，数学家们一直想知道极小曲面是否总是光滑的。突破来自于[几何测度论](@keyword=geometric_measure_theory|lang=zh-CN|style=Feynman)的一项巨大努力，它建立了一条惊人的规则：对于一个 $n$ 维空间中的[面积最小化超曲面](@keyword=area_minimizing_hypersurfaces|lang=zh-CN|style=Feynman)，其[奇点](@keyword=singularities|lang=zh-CN|style=Feynman)集的[豪斯多夫维数](@keyword=hausdorff_dimension|lang=zh-CN|style=Feynman)最多为 $n-8$ [@problem_id:3036405]。

让我们来解读一下。如果我们处于一个 7 维空间（$n=7$），那么我们 6 维[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman) $\Sigma$ 的[奇点](@keyword=singularities|lang=zh-CN|style=Feynman)集维数最多为 $7-8 = -1$。由于任何集合的维数都不可能为负，这意味着[奇点](@keyword=singularities|lang=zh-CN|style=Feynman)集必须是空的。[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)是完美光滑的！对于任何 $n  8$ 的维度，这都成立。

但在 $n=8$ 时，情况发生了巨大变化。[奇点](@keyword=singularities|lang=zh-CN|style=Feynman)集的维数可以高达 $8-8=0$。一个维数为 0 的集合是一组孤立的点。这不再仅仅是一个理论上的可能性。一个著名的[反例](@keyword=counterexample|lang=zh-CN|style=Feynman)，即 $\mathbb{R}^8$ 中的 **Simons 锥**，就是一个面积最小化[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)（一个由两个 4 维球面构成的锥体），它虽然稳定，但在其顶点处有一个尖锐的[奇点](@keyword=singularities|lang=zh-CN|style=Feynman) [@problem_id:3033313] [@problem_id:3036405]。

因为我们的[极小曲面](@keyword=minimal_surfaces|lang=zh-CN|style=Feynman) $\Sigma$ 在 8 维及更高维度*可能*会产生这些点状[奇点](@keyword=singularities|lang=zh-CN|style=Feynman)，经典微分几何的工具就不能再盲目地应用了。证明的引擎就此卡壳。这是一个惊人的提醒：在几何学中，维度不仅仅是数字；每个维度都有其独特的特性，并可[能带](@keyword=energy_bands|lang=zh-CN|style=Feynman)来自己的惊喜。（值得注意的是，[正质量定理](@keyword=positive_mass_theorem|lang=zh-CN|style=Feynman)在所有维度上*都*是成立的。然而，要证明 $n \ge 8$ 的情况，需要完全不同且同样卓越的思想，例如 [Edward Witten](@keyword=edward_witten|lang=zh-CN|style=Feynman) 使用旋量和[狄拉克算子](@keyword=dirac_operator|lang=zh-CN|style=Feynman)的著名证明。）

### 真理的稳固性

Schoen 和 Yau 的原始证明假定[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的织物，即度量 $g$ ，是完美光滑的。但如果它更粗糙一些，带有曲率没有被良好定义的扭结或角落呢？像能量正性这样的基本真理，会依赖于如此理想化的假设吗？

值得注意的是，它不会。该证明的现代扩展显示了该定理是多么的稳固。其策略是用一系列光滑的几何来逼近“粗糙”的几何，这些光滑几何越来越接近原始几何 [@problem_id:3001579]。这会带来一个小问题：这个平滑过程可能会无意中产生小块的负标量曲率。然而，数学家们还有另一招：**[共形变换](@keyword=conformal_transformations|lang=zh-CN|style=Feynman)**。通过以恰到好处的方式局部拉伸或收缩几何——这个过程就像通过一个精心设计的放大镜观察空间——他们可以“熨平”这些不希望出现的负曲率区域。至关重要的是，这可以在不改变无穷远处几何的情况下完成，从而保持总 ADM 质量不变。

这就产生了一系列光滑、行为良好的空间，每个都具有非负的标量曲率。经典的 [Schoen-Yau](@keyword=schoen_yau|lang=zh-CN|style=Feynman) 证明适用于它们中的每一个，因此每一个都必须具有正质量。由于这些逼近空间的质量收敛于原始粗糙空间的质量，那么原始空间也必须具有正质量。这个优美的论证表明，质量的正性不是数学理想化的脆弱产物，而是任何建立在正能量原理上的宇宙深刻而坚韧的特征。