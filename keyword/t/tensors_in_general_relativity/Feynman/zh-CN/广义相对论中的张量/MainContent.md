## 引言
爱因斯坦的广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)重塑了我们对宇宙的理解，它用一个全新的激进思想取代了牛顿将引力视为一种力的概念：引力即[时空](@keyword=space_time|lang=zh-CN|style=Feynman)本身的曲率。这一深刻的转变带来了一个巨大的挑战：在一个空间和时间都因质量和能量而动态变化、扭曲的世界里，我们该如何描述物理定律？我们熟悉的欧几里得几何和微积分法则已不再适用。为了构建适用于任何观察者、在任何运动状态下都成立的定律，我们需要一种新的、更强大的数学语言。本文探讨的正是这种语言——[张量](@keyword=tensor|lang=zh-CN|style=Feynman)的语言。

我们将踏上一段理解这一基本框架的旅程。第一部分，**原理与机制**，将揭开[张量](@keyword=tensor|lang=zh-CN|style=Feynman)的神秘面纱，解释它们是什么，以及为何[广义协变性原理](@keyword=principle_of_general_covariance|lang=zh-CN|style=Feynman)使其不可或缺。我们将构建该理论的关键组成部分，从定义几何的度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman)到支配几何的[爱因斯坦场方程](@keyword=einstein_s_field_equations|lang=zh-CN|style=Feynman)。随后，在**应用与跨学科联系**中，我们将见证这种语言的力量，用它来破译[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的秘密，描绘宇宙的膨胀，并揭示引力与自然界其他基本力之间令人惊讶的联系。

## 原理与机制

想象一下，两位科学家 Alice 和 Bob，各自乘坐飞船漂浮在虚空中。他们想要发现物理定律。如果不停翻滚的 Alice 发现了一条定律，而像陀螺一样旋转的 Bob 发现了另一条形式上不同的定律，那么他们发现的究竟是关于宇宙的基本真理，还是仅仅是关于他们各自特定处境的真理？爱因斯坦的深刻洞见，即**[广义协变性原理](@keyword=principle_of_general_covariance|lang=zh-CN|style=Feynman)**，坚信一条真正的自然定律对任何人来说都必须是相同的，无论他们的运动状态或用来描绘世界的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)如何 [@problem_id:1872194]。物理学必须是客观的。这就需要一种新的语言，在这种语言中，方程不会因为我们改变视角而失效。这种语言就是[张量](@keyword=tensor|lang=zh-CN|style=Feynman)的语言。

### [张量](@keyword=tensor|lang=zh-CN|style=Feynman)的普适语言

那么，什么是[张量](@keyword=tensor|lang=zh-CN|style=Feynman)？从本质上讲，[张量](@keyword=tensor|lang=zh-CN|style=Feynman)是一种数学对象，当改变[坐标时](@keyword=coordinate_time|lang=zh-CN|style=Feynman)，它会以一种非常具体、基于规则的方式进行变换。这个规则的设计使得，如果你将一条物理定律写成[张量](@keyword=tensor|lang=zh-CN|style=Feynman)方程，该方程在任何[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)下都能保持其形式。

假设我们有一个物理量，由一组数描述，我们在一个[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman) $x$ 中称之为 $T_{\alpha\beta}$。如果我们切换到一个新的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman) $x'$，新的分量 $T'_{\mu\nu}$ 就通过一个精确的法则得到 [@problem_id:1495281]：
$$
T'_{\mu\nu} = \frac{\partial x^\alpha}{\partial x'^\mu}\frac{\partial x^\beta}{\partial x'^\nu} T_{\alpha\beta}
$$
像 $\frac{\partial x^\alpha}{\partial x'^\mu}$ 这样的项是关联新旧坐标的[偏导数](@keyword=partial_derivatives|lang=zh-CN|style=Feynman)；它们是两个[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)之间的“翻译词典”。因为指标 $\mu$ 和 $\nu$ 在下方，我们称之为一个**协变**[张量](@keyword=tensor|lang=zh-CN|style=Feynman)。如果它们在上方，它就是一个**逆变**[张量](@keyword=tensor|lang=zh-CN|style=Feynman)，其变换规则将涉及形如 $\frac{\partial x'^\mu}{\partial x^\alpha}$ 的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)。指标的数量（本例中为两个）告诉我们[张量](@keyword=tensor|lang=zh-CN|style=Feynman)的**阶**。

这可能看起来很抽象，但它有一个强大的推论：一个不是[张量](@keyword=tensor|lang=zh-CN|style=Feynman)方程的方程，就不是一个普适的定律。考虑一个假设的定律，它声称某个物理[张量](@keyword=tensor|lang=zh-CN|style=Feynman) $T_{ij}$ 总是等于[单位矩阵](@keyword=identity_matrix|lang=zh-CN|style=Feynman)的分量，即一个称为[克罗内克δ](@keyword=kronecker_delta|lang=zh-CN|style=Feynman)的简单对象 $\delta_{ij}$ [@problem_id:1872179]。这个“定律”在标准笛卡尔坐标系中完美成立。但如果你切换到[极坐标系](@keyword=polar_coordinate_system|lang=zh-CN|style=Feynman)，[张量变换](@keyword=tensor_transformations|lang=zh-CN|style=Feynman)的严格规则会将简单的[单位矩阵](@keyword=identity_matrix|lang=zh-CN|style=Feynman)变成一个依赖于函数的复杂矩阵。方程 $T'_{ij} = \delta_{ij}$ 将不再成立。这个“定律”仅仅因为我们改变了观察角度就被打破了。一条真正的物理定律不能如此脆弱。

一种更直观的思考[张量](@keyword=tensor|lang=zh-CN|style=Feynman)的方式是将其看作一种“插槽机器”[@problem_id:1844997]。[张量](@keyword=tensor|lang=zh-CN|style=Feynman)是一台带有一组输入插槽的机器。一些插槽用于矢量（逆变，上指标对象），另一些用于[余矢量](@keyword=covectors|lang=zh-CN|style=Feynman)（协变，下指标对象，如梯度）。当你将每种类型的一个对象填入所有插槽时，机器就会运转并输出一个单一的数字——一个**标量**——这是一个所有观察者都会认同的、真正的、客观的量。[张量](@keyword=tensor|lang=zh-CN|style=Feynman)的阶和类型，例如黎曼曲率张量 $R^\rho{}_{\sigma\mu\nu}$ 是(1,3)型，就只是告诉我们它有一个用于[余矢量](@keyword=covectors|lang=zh-CN|style=Feynman)的插槽和三个用于矢量的插槽。它是一台等待正确输入以描述一部分物理现实的机器。

### 度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman)：[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的终极标尺

[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中最重要的[张量](@keyword=tensor|lang=zh-CN|style=Feynman)，也是我们故事的绝对主角，是**度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman)** $g_{\mu\nu}$。这是一个对称的二阶[协变张量](@keyword=covariant_tensors|lang=zh-CN|style=Feynman)，其任务正是定义[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的几何。它是终极的标尺。给定两个由微小坐标差 $dx^\mu$ 分隔的邻近点，度规通过著名的方程告诉你它们之间实际的、物理的[时空间隔](@keyword=spacetime_interval|lang=zh-CN|style=Feynman) $ds$：
$$
ds^2 = g_{\mu\nu} dx^\mu dx^\nu
$$
在狭义相对论的平直[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中，这只是我们熟悉的[闵可夫斯基度规](@keyword=minkowski_metric|lang=zh-CN|style=Feynman) $\eta_{\mu\nu}$，在标准坐标下它是一个由 $1$ 和 $-1$ 组成的简单矩阵。但在引力存在的情况下，$g_{\mu\nu}$ 的分量会变成随位置变化的函数，描述着[动态几何](@keyword=dynamic_geometry|lang=zh-CN|style=Feynman)的扭曲和弯曲。

这听起来非常抽象，但爱因斯坦通过**等效原理**将其与一种切实的体验联系起来 [@problem_id:1554897]。想象你在一个电梯里，缆绳突然断了。在那可怕的一瞬间，你处于自由落体状态，感觉不到重量。在你下落的箱子里，一个被放下的苹果漂浮在你身边。引力似乎消失了！爱因斯坦意识到，这不是错觉；这是一个根本性的线索。在任何[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)中的任何一点，总可以找到一个“自由下落”的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)（一个*[局域惯性系](@keyword=local_inertial_frames|lang=zh-CN|style=Feynman)*），在该[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)中，对于那一点和那一瞬间，物理定律呈现出它们在[狭义相对论](@keyword=special_relativity_theory|lang=zh-CN|style=Feynman)中那种简单的、没有引力的形式。

对于度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman)来说，这意味着无论你的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)在全局上有多弯曲，在任何一点 $P$，你总能找到[局部坐标](@keyword=local_coordinates|lang=zh-CN|style=Feynman)，使得 $g_{\mu\nu}(P) = \eta_{\mu\nu}$。[时空](@keyword=space_time|lang=zh-CN|style=Feynman)是*局域平直*的。因此，曲率不是度规在某一点的值，而是它如何*从一点变化到另一点*——这是你跳进下落的电梯也*无法*摆脱的那部分几何。

度规还有一个至关重要的任务。它充当着一个通用翻译器，允许我们在[张量](@keyword=tensor|lang=zh-CN|style=Feynman)的协变（下指标）和逆变（上指标）形式之间进行转换 [@problem_id:1060435]。使用度规 $g_{\mu\nu}$ 及其逆 $g^{\mu\nu}$，我们可以“升”或“降”指标，例如，将一个[余矢量](@keyword=covectors|lang=zh-CN|style=Feynman) $V_\mu$ 变成一个矢量 $V^\mu = g^{\mu\nu}V_\nu$。正是这种数学机制赋予几何结构，定义了配对[矢量和余矢量](@keyword=vectors_and_covectors|lang=zh-CN|style=Feynman)以产生[不变量](@keyword=invariant|lang=zh-CN|style=Feynman)标量的自然方式。

### [协变导数](@keyword=covariant_derivative|lang=zh-CN|style=Feynman)：在弯曲世界中导航

我们现在有了在任何[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)下都能正确表现的对象，但我们如何描述它们*如何变化*呢？我们如何计算一个梯度或变化率，使其本身也是一个行为良好的[张量](@keyword=tensor|lang=zh-CN|style=Feynman)？

在这里我们遇到了一个主要障碍。如果我们取一个[矢量场](@keyword=vector_field|lang=zh-CN|style=Feynman) $V^\mu$ 并直接计算其偏导数 $\partial_\nu V^\mu$，得到的对象*不是*一个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)。它的变换方式完全错误。原因微妙而优美。在一个像地球仪一样的弯曲表面上，坐标线本身会弯曲和伸展。当我们取一个简单的[偏导数](@keyword=partial_derivatives|lang=zh-CN|style=Feynman)时，我们不知不觉地将矢量的*真实*变化与由[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)自身扭曲所带来的*表观*变化混淆了 [@problem_id:1872189]。

为了解决这个问题，我们需要一个更智能的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)，一个能感知其所在几何的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)。这就是**协变导数**，记作 $\nabla_\mu$。对于一个矢量，它具有以下形式：
$$
\nabla_\nu V^\mu = \partial_\nu V^\mu + \Gamma^\mu_{\nu\lambda} V^\lambda
$$
第一部分是熟悉的[偏导数](@keyword=partial_derivatives|lang=zh-CN|style=Feynman)。第二部分，涉及**[克里斯托费尔符号](@keyword=christoffel_symbols|lang=zh-CN|style=Feynman)** $\Gamma^\mu_{\nu\lambda}$，是关键的修正项。克里斯托费尔符号是由度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman)的[导数](@keyword=derivative|lang=zh-CN|style=Feynman)计算出来的，所以它们精确地知道几何是如何逐点弯曲的。它们精确地减去了来自[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)的“虚假”变化，只留下矢量的纯粹的、物理的变化。结果 $\nabla_\nu V^\mu$ 是一个真正的[张量](@keyword=tensor|lang=zh-CN|style=Feynman)。有了[协变导数](@keyword=covariant_derivative|lang=zh-CN|style=Feynman)，我们终于拥有了一套适用于弯曲世界的完整微积分。

### 引力的架构：一个必然性的故事

我们终于准备好写下引力定律了。我们需要一个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)方程，将引力的来源——物质和能量——与其效应——[时空曲率](@keyword=spacetime_curvature|lang=zh-CN|style=Feynman)——联系起来。用一句口号来说，就是`[几何[张量](@keyword=tensor|lang=zh-CN|style=Feynman)] = [物质[张量](@keyword=tensor|lang=zh-CN|style=Feynman)]`。

这就是著名的**爱因斯坦场方程** [@problem_id:1860733]：
$$
G_{\mu\nu} = \frac{8\pi G}{c^4} T_{\mu\nu}
$$
方程的右边是**应力-能量张量** $T_{\mu\nu}$。这是“物质”的一边。它是宇宙中所有非引力物质的宏大概括：其能量密度、动量、压强和应力。它是源。方程的左边是**爱因斯坦张量** $G_{\mu\nu}$。这是“几何”的一边，一个由度规及其[导数](@keyword=derivative|lang=zh-CN|style=Feynman)构成的复杂[张量](@keyword=tensor|lang=zh-CN|style=Feynman)，它巧妙地描述了[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的曲率。这个方程做出了由 John Archibald Wheeler 阐明的著名宣告：**“[时空](@keyword=space_time|lang=zh-CN|style=Feynman)告诉物质如何运动；物质告诉[时空](@keyword=space_time|lang=zh-CN|style=Feynman)如何弯曲。”**

但一个深刻的问题依然存在。在我们可能构建的用以描述曲率的所有[张量](@keyword=tensor|lang=zh-CN|style=Feynman)中，为什么偏偏是这一个，$G_{\mu\nu}$？答案揭示了该理论惊人的内在逻辑。在物理学中，源通常受守恒定律支配。[电荷](@keyword=electric_charge|lang=zh-CN|style=Feynman)总量是守恒的。对于引力，“源荷”是能量-动量，其守恒性体现在[张量](@keyword=tensor|lang=zh-CN|style=Feynman)方程 $\nabla^\mu T_{\mu\nu} = 0$ 中。应力-能量张量的[协变散度](@keyword=covariant_divergence|lang=zh-CN|style=Feynman)为零。

现在，再看一遍场方程。如果右边的散度恒等于零，那么为了让这个方程普遍成立，左边的散度也*必须*恒等于零。这对我们选择“几何[张量](@keyword=tensor|lang=zh-CN|style=Feynman)”是一个严苛的约束 [@problem_id:1832863]。你不能随便挑选任何一个旧的曲率度量。一个幼稚的选择，比如一个简单的波算子，就通不过这个测试；它的散度不是自动为零，这意味着方程只能偶然成立，或者需要对几何本身施加额外的、非物理的约束。

而奇迹就在这里。微分几何学如同在[银盘](@keyword=galactic_disk|lang=zh-CN|style=Feynman)上端出了一份独特的解决方案。存在一个特定的曲率张量组合，恰好就是爱因斯坦张量 $G_{\mu\nu} \equiv R_{\mu\nu} - \frac{1}{2}g_{\mu\nu}R$（其中 $R_{\mu\nu}$ 是里奇张量，$R$ 是里奇标量），它具有一个非凡的性质，即其[协变散度](@keyword=covariant_divergence|lang=zh-CN|style=Feynman)*总是*为零，无论[时空](@keyword=space_time|lang=zh-CN|style=Feynman)如何。这个数学事实被称为**缩并的毕安基恒等式** [@problem_id:1850181]。

[爱因斯坦方程](@keyword=einstein_s_equations|lang=zh-CN|style=Feynman)的形式并非任意选择；它是一项深刻的发现。当能量-动量守恒的物理原理用[张量](@keyword=tensor|lang=zh-CN|style=Feynman)语言写出时，它要求一个同样自动守恒的几何伙伴。弯曲[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的数学提供了一个，且仅有一个，自然候选者。其结果是一个不仅强大，而且在深刻意义上是必然的引力理论。