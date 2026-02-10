## 引言
在爱因斯坦广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)所描述的宇宙中，质量并非物体的简单属性，而是时空曲率本身的来源。这就提出了一个深刻的问题：我们如何在不了解其内部所有信息的情况下，测量一个有限空间区域内所包含的质量？寻求一种“准局域质量”——即仅通过观察其边界的几何形状来衡量宇宙一部分质量的方法——正是为了应对这一根本性挑战。[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)是解决此问题最为优雅和强大的方案之一，为引力的本质提供了深刻的见解。本文将探讨[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)的理论与意义。在第一部分“原理与机制”中，我们将剖析[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)的巧妙公式，探索其背后的几何直觉及其卓越性质，例如在特定[几何演化](@keyword=geometric_evolution|lang=zh-CN|style=Feynman)下的单调行为。随后，“应用与跨学科联系”部分将展示其深远影响，揭示此概念如何为证明著名的[彭罗斯不等式](@keyword=penrose_inequality|lang=zh-CN|style=Feynman)提供关键，并为从动态[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)到我们膨胀宇宙的广阔区域提供一种一致的衡量方法。

## 原理与机制

在我们理解宇宙的征程中，一些最简单的问题往往最为深刻。什么是质量？在日常世界里，我们可以将物体放在秤上。但如果那个“物体”是一颗恒星、一个星系或一个[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)呢？在爱因斯坦的广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中，质量不仅仅是物体的属性，它被编织进了[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的结构之中。质量即能量，而能量使[时空](@keyword=space_time|lang=zh-CN|style=Feynman)弯曲。那么，我们如何仅通过观察一个区域边界的几何形状来测量其内部所含的质量呢？这就是对**准局域质量**的追寻——一种衡量宇宙一部分的方法。

### 一个巧妙的配方：定义[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)

想象你是一位宇宙勘测员，你在空间的某个区域周围绘制了一个封闭的二维[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)——姑且称之为球面。你想知道封闭在内的总质量是多少。物理学家 [Stephen Hawking](@keyword=stephen_hawking|lang=zh-CN|style=Feynman) 提出了一个优美而精妙的公式来做到这一点。乍一看，一个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman) $\Sigma$ 的**[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)** $m_H$ 的公式可能有点吓人：

$$
m_H(\Sigma) = \sqrt{\frac{|\Sigma|}{16\pi}} \left( 1 - \frac{1}{16\pi} \int_{\Sigma} H^2 \, d\mu \right)
$$

但我们不要被这些符号吓倒。让我们来谈谈它们的*含义*。可以把它看作一个包含两种主要成分的配方。

第一种成分 $\sqrt{\frac{|\Sigma|}{16\pi}}$ 是你能做出的最简单的猜测。如果你相信你的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman) $\Sigma$ 是一个[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的视界，那么它的面积 $|\Sigma|$ 与其质量直接相关。该项实质上是如果[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)视界面积为此值时，它所应具有的质量。它如此基础，以至于出现在一个名为**黎曼[彭罗斯不等式](@keyword=penrose_inequality|lang=zh-CN|style=Feynman)**的著名猜想中，该猜想根据[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)视界的面积为系统的总质量设定了一个下限 [@problem_id:3031182] [@problem_id:3036633]。所以，我们的第一个猜测是将质量与我们[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的一种“面积半径”联系起来。

但大多数[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)并非[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)视界。它们可能是凹凸不平、布满褶皱或扭曲的。这时第二种成分就派上用场了：修正因子 $\left( 1 - \frac{1}{16\pi} \int_{\Sigma} H^2 \, d\mu \right)$。其中，$H$ 是[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的**平均曲率**，用于衡量[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)在每一点的弯曲程度。$\int_{\Sigma} H^2 \, d\mu$ 这一项在几何学中被称为**Willmore能量**。它衡量的是[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的*总弯曲量*。一个完美光滑的圆球面具有最小的Willmore能量；任何其他形状，无论你如何使其褶皱或变形，其Willmore能量都会更大。因此，这个修正项会根据我们测量的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)与完美圆球面的偏离程度来调整我们的初始猜测。就好像这个公式在说：“从你根据面积所[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的质量开始，然后为所有的褶皱减去一个惩罚项。”

当然，像 $16\pi$ 这样的常数并非凭空捏造。它们经过精心选择，以使整个方案完美运作，我们稍后将看到这一点。这个定义也不仅限于三维空间。同样的逻辑可用于在更高维度构建类似的质量，这证明了其底层几何思想的普适性 [@problem_id:3036635]。

### 试金石：空无一物的质量为零，有所包含则有相应质量

一个好的定义应该通过一些合理性检验。首先，如果我们处于完全空旷的平直空间（高中几何中熟悉的欧几里得空间）中，我们绘制的任何[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)应包含零质量。[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)对此有何说法？让我们取最对称的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)：一个半径为 $r$ 的完美球面。直接计算表明，对于这样一个球面，公式中的面积项和弯曲项完美平衡。修正因子恰好为零，因此[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)为 $m_H(\text{球面}) = 0$ [@problem_id:3031187] [@problem_id:3036633] [@problem_id:525794]。它成功了！该定义经过校准，对于平直空间中最基本的对象给出零值。

现在进行一个更有趣的测试。让我们去一个*存在*质量的地方。在广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中，最简单的地方是单个不[旋转黑洞](@keyword=rotating_black_holes|lang=zh-CN|style=Feynman)周围的空间，由**[Schwarzschild解](@keyword=schwarzschild_solution|lang=zh-CN|style=Feynman)**描述。这个[时空](@keyword=space_time|lang=zh-CN|style=Feynman)只有一个质量参数 $m$。让我们在这个[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)周围绘制勘测员的球面。我们可以在远处画一个球面，也可以在非常靠近视界的地方画一个。这些球面的[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)是多少？一个堪称数学小奇迹的计算结果表明，这些同心球面中*每一个*的[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)都恰好是 $m$ [@problem_id:3036589] [@problem_id:3036633]。我们测量的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)距离远近无关紧要；该公式穿透了几何畸变，报告了[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)真实、内在的质量。这个非凡的结果向我们保证，[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)不仅仅是一个数学上的奇物，它是一个具有物理意义的质量度量。

### 几何之流：在[逆平均曲率流](@keyword=inverse_mean_curvature_flow|lang=zh-CN|style=Feynman)上不断增长的质量

当我们观察[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)在运动中的行为时，它的真正力量和美感便显现出来。想象一下，我们的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)不是静态的，而是在一部电影中，随[时间演化](@keyword=time_evolution|lang=zh-CN|style=Feynman)。有一种非常特殊的演化[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的方式，一种对数学家而言已是金矿的几何流：**[逆平均曲率流](@keyword=inverse_mean_curvature_flow|lang=zh-CN|style=Feynman)（IMCF）**。

可以把它想象成吹气球。IMCF 指示[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)向外扩张，但遵循一个奇特的规则：[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上任何一点的移动速度都与其平均曲率成反比（$v = 1/H$）。这意味着[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)中高度弯曲的部分（如凸起的尖端）扩张得非常慢，而较平坦的部分扩张得很慢。总体效果是，随着[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的增长，这个流倾向于使其变得更圆。

现在，这里有一个深刻的发现，这是 Gerhard Huisken 和 Tom Ilmanen 工作的核心成果：如果我们所处的空间具有所谓的**非负[标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman)**（一个物理条件，基本意味着引力平均而言是吸引的，正如你从普通物质和能量中所[期望](@keyword=expectation_value|lang=zh-CN|style=Feynman)的那样），那么当我们的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)在 IMCF 下演化时，其[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)*绝不会减小*。它是一个**单调**量 [@problem_id:3031182] [@problem_id:3036620]。

这是一个深刻而有力的论断。它提出了一个宏大的策略：我们可以从遥远空间中近乎平坦部分的一个很小的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)开始，我们知道那里的[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)接近系统的总质量（**[Arnowitt-Deser-Misner](@keyword=arnowitt_deser_misner|lang=zh-CN|style=Feynman) (ADM) 质量**）。然后我们可以将流在时间上向后运行（这意味着[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)会收缩）。单调性定理保证了我们在此过程中测得的[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)只会下降（或保持不变）。当我们跟随这个收缩的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)时，它最终会“找到”什么？它会找到[质量分布](@keyword=mass_distribution|lang=zh-CN|style=Feynman)的最内层边界——[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)视界。无穷远处的质量与视界几何之间的这种联系，正是黎曼[彭罗斯不等式](@keyword=penrose_inequality|lang=zh-CN|style=Feynman)的核心。

### 当流动中断时：跳跃、[奇点](@keyword=singularities|lang=zh-CN|style=Feynman)和弱形式的力量

这种平滑流动的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)图景听起来很美妙，但在现实世界中存在一个严重问题。[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)视界是**[极小曲面](@keyword=minimal_surfaces|lang=zh-CN|style=Feynman)**，意味着它们的平均曲率为零（$H=0$）。当我们的演化[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)在速度为 $v=1/H$ 的流下，接近一个 $H$ 接近于零的区域时，会发生什么？速度会激增至无穷大！平滑的流将在到达视界之前崩溃，撕裂自己 [@problem_id:3036630]。

这就是现代理论真正天才之处。Huisken 和 Ilmanen 没有放弃，而是设计了该流的一种**弱形式**。在这个框架中，当流即将因遇到极小曲面而形成[奇点](@keyword=singularities|lang=zh-CN|style=Feynman)时，它会做出非凡的举动：它会**跳跃**。[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)瞬间吞噬有问题的区域，并在另一侧重新出现，继续其演化。这个“跳跃”并非任意的；[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)会跳到所谓的**向外极小化包络**，这是一个以最小可能面积包围旧[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的新[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)。此构造最关键的部分在于它被设计成即使在[跳跃过程](@keyword=jump_processes|lang=zh-CN|style=Feynman)中，[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)*仍然不会减小* [@problem_id:3001585]。这种弱流足够稳健，可以在一个充满[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的凹凸不平的宇宙中航行，使其能够从无穷远处开始并成功“着陆”在视界上，从而提供了证明[彭罗斯不等式](@keyword=penrose_inequality|lang=zh-CN|style=Feynman)所需的关键联系。

### 细则：为何宇宙关心连通性

这个错综复杂的谜题还有最后一块。单调性这个优美的性质——即保证质量在流中永不减小——在一个关键的拓扑条件下成立：演化的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)必须是单一的**连通**部分。

为了理解原因，考虑一个思想实验。想象一个包含两个独立[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的空间。我们从两个独立的勘测球面开始，每个球面围绕一个[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)。在 IMCF 下，两个球面都扩张。只要它们是分开的，总[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)（简单定义为两个单独质量之和）将是非递减的。但当它们接触并合并时会发生什么？弱流规定了一次跳跃。两个接触的球面被一个包围它们的单一连通[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)所取代。

这里的转折点是：计算表明，这个新的单一[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的[霍金质量](@keyword=hawking_mass|lang=zh-CN|style=Feynman)可能*小于*它们合并前两个独立[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的质量之和 [@problem_id:3036606]。总质量下降了！就好像将两个物体识别为一个单一相互作用系统的行为本身，揭示了一种降低总质量的“结合能”。这惊人地清晰地表明，我们习惯的简单的、可加的质量概念在广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中失效了。几何，特别是我们测量[曲面的拓扑](@keyword=topology_of_surfaces|lang=zh-CN|style=Feynman)，与我们测量的质量密不可分。这个几何宇宙的法则似乎适用于整体、连通的系统，而不仅仅是其各部分之和。