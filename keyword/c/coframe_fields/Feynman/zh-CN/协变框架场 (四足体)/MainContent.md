## 引言
在现代物理学的图景中，广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)所描述的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)整体曲率与任何观测者根据等效原理和[狭义相对论](@keyword=special_relativity_theory|lang=zh-CN|style=Feynman)所体验到的局域平直性之间，存在着一种根本性的[张力](@keyword=tension_force|lang=zh-CN|style=Feynman)。我们如何才能建立一个既尊重这两种视角，又能描述物质量子特性的自洽理论？当涉及像电子这样由[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)描述的粒子时，这一挑战变得尤为尖锐。[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)内在地定义于[狭义相对论](@keyword=special_relativity_theory|lang=zh-CN|style=Feynman)的平直框架之中，无法自然地融入引力的弯曲几何。解决方案在于一个被称为协变框架场（或[多足标架](@keyword=vielbein|lang=zh-CN|style=Feynman)）的强大数学框架。本文旨在全面概述这一关键工具。在第一章“原理与机制”中，我们将深入剖析其核心概念，探讨协变框架如何构建[时空度规](@keyword=spacetime_metrics|lang=zh-CN|style=Feynman)，引入一个名为[局域洛伦兹对称性](@keyword=local_lorentz_symmetry|lang=zh-CN|style=Feynman)的新物理原理，并阐明为何必须使用[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)来描述旋量的输运。随后的“应用与跨学科联系”一章将展示协变框架的非凡功用——从简化几何计算，到构建[替代引力理论](@keyword=alternative_gravity|lang=zh-CN|style=Feynman)，乃至模拟晶体材料中的缺陷。我们将从审视使协变框架场成为物理学家和几何学家工具箱中不可或缺一部分的基本原理开始我们的旅程。

## 原理与机制

想象一下，你是一只生活在巨大、凹凸不平的橙子表面上的微小而聪明的蚂蚁。对你而言，任何时刻你所站立的那一小块橙皮看起来都是完全平坦的。你可以使用微小的尺子和量角器，所有平直的欧几里得几何法则似乎都适用。但如果你试图仅用这些局域的平坦测量数据来绘制整个橙子的巨大地图，你很快就会遇到麻烦。三角形的内角和将不再是180度，平行线也会神秘地相交。

这正是我们在广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中面临的挑战。[时空](@keyword=space_time|lang=zh-CN|style=Feynman)是弯曲的，但在任何单一点上的足够小区域内，物理定律看起来与狭义相对论平直[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中的完全一样。这就是[等效原理](@keyword=principle_of_equivalence|lang=zh-CN|style=Feynman)的核心。问题在于，我们如何建立一个既能尊重[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的整体曲率，又能体现任何观测者所经历的局域“平直性”的自洽物理描述？

答案在于一个优美而强大的数学工具：**协变框架场**，也被称为**[多足标架](@keyword=vielbein|lang=zh-CN|style=Feynman)**（在四维[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中称为**四足**）。它就像一本词典，或一块罗塞塔石碑，让我们能够在[弯曲时空](@keyword=curved_spacetime|lang=zh-CN|style=Feynman)的“凹凸不平”的全局语言和观测者个人实验室中纯净“平直”的局域语言之间进行翻译。

### 为何我们需要一种新语言：旋量的困境

你可能会问：“为什么要费这么大劲？难道我们不是已经有了[张量](@keyword=tensor|lang=zh-CN|style=Feynman)和协变导数来处理弯曲空间吗？” 对于许多事物来说，是的。但对于宇宙中一些最基本的粒子，比如构成你我的电子和夸克，广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)的标准工具箱是不够的。

这些粒子由一种称为**[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)**的客体描述。关于[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)，最关键的一点是，根据其定义，它们是在**[洛伦兹群](@keyword=lorentz_group|lang=zh-CN|style=Feynman)**——即支配[狭义相对论](@keyword=special_relativity_theory|lang=zh-CN|style=Feynman)的升压和[旋转群](@keyword=rotation_group|lang=zh-CN|style=Feynman)——下进[行变换](@keyword=row_operations|lang=zh-CN|style=Feynman)的客体。它们从根本上与闵可夫斯基时空的平直、刚性结构绑定。它们根本不知道如何响应广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)赖以为生的、更为宽泛的广义坐标变换群（[微分同胚](@keyword=diffeomorphism|lang=zh-CN|style=Feynman)）。试图将一个[旋量](@keyword=spinors|lang=zh-CN|style=Feynman)直接置于由度规 $g_{\mu\nu}$ 描述的弯曲时空中，就像是上演一出莎士比亚戏剧，但演员只会说克林贡语；舞台的语言和演员的语言不匹配 [@problem_id:1881205]。

协变框架场解决了这个问题。它在[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的每一点上都建立了一个微小的、私有的“洛伦兹舞台”。在这个局域舞台上，我们的旋量演员可以表演他们的戏剧，说着他们洛伦兹变换的母语。因此，协变框架形式体系不仅仅是一种便利；它是将物质场的量子描述编织进引力经典织锦中的绝对必需品。

### 罗塞塔石碑：锻造度规

那么这本词典是如何工作的呢？我们引入两套指标。熟悉的希腊指标，如 $\mu$ 和 $\nu$，标记弯曲时空[流形](@keyword=manifold|lang=zh-CN|style=Feynman)上的坐标——这是我们的全局、“凹凸不平的橙子”视角。然后我们引入新的拉丁指标，如 $a$ 和 $b$，它们标记观测者局域、平直、[惯性参考系](@keyword=inertial_frame_of_reference|lang=zh-CN|style=Feynman)中的方向——即蚂蚁那片微小、平坦的橙皮。

协变框架场，写作一组[1-形式](@keyword=one_forms|lang=zh-CN|style=Feynman) $e^a = e^a_\mu \,dx^\mu$，是连接这两个世界的客体。它的分量 $e^a_\mu$ 一脚踏入一个世界，同时带有一个拉丁指标和一个希腊指标。其基本的翻译规则是一个优雅的方程，它通过协变框架分量和简单平直的[闵可夫斯基度规](@keyword=minkowski_metric|lang=zh-CN|style=Feynman) $\eta_{ab} = \text{diag}(-1, 1, 1, 1)$ 来构建全局度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman) $g_{\mu\nu}$：

$$
g_{\mu\nu}(x) = \eta_{ab}\,e^a_\mu(x)\,e^b_\nu(x)
$$

这是整个形式体系的基石 [@problem_id:2995522]。这是一个保证。它表明，如果你在你的局域实验室中使用协变框架[基矢](@keyword=basis_vector|lang=zh-CN|style=Feynman)进行测量，结果将总是符合[狭义相对论](@keyword=special_relativity_theory|lang=zh-CN|style=Feynman)的规则，那里的度规就是 $\eta_{ab}$。弯曲度规 $g_{\mu\nu}$ 那些复杂的、依赖于位置的分量，完全被编码在协变框架场那些随位置变化的“词典条目”中。

这种关系是如此深刻，以至于连[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的[体积元](@keyword=volume_element|lang=zh-CN|style=Feynman)——一个无穷小四维空间块的度量——也直接由协变框架[矩阵的行列式](@keyword=determinant_of_a_matrix|lang=zh-CN|style=Feynman)给出：$\sqrt{-\det(g_{\mu\nu})} = \det(e^a_\mu)$ [@problem_id:1550277]。协变框架不仅仅是*与*几何*相关*；在非常真实的意义上，它*就是*几何本身。

### 表达的自由：[局域洛伦兹对称性](@keyword=local_lorentz_symmetry|lang=zh-CN|style=Feynman)

当我们采用这种新语言时，一件奇怪的事情发生了。度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman) $g_{\mu\nu}$ 是对称的，因此在四维中它有10个独立分量。但协变框架场 $e^a_\mu$ 是一个 $4 \times 4$ 矩阵，拥有16个分量。我们似乎引入了比描述[引力场](@keyword=gravitational_field|lang=zh-CN|style=Feynman)所需更多的变量。这额外的自由度是什么？

这不是一个缺陷；它是一个辉煌的新特性！这额外的自由度对应于我们能够在*[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中的每一点上，独立地*选择我们局域测量装置——我们那套局域的尺子和时钟——的朝向。在 $x$ 点，你可以定向你的[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)。在另一个点 $y$，另一个观测者可以用完全不同的方式定向他们的[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)。这种对局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)指标（$a, b, \dots$）执行依赖于[时空](@keyword=space_time|lang=zh-CN|style=Feynman)点 $x$ 的[洛伦兹变换](@keyword=the_lorentz_transformation|lang=zh-CN|style=Feynman)（旋转或升压）的自由，被称为**[局域洛伦兹对称性](@keyword=local_lorentz_symmetry|lang=zh-CN|style=Feynman)**。

如果我们应用这样一个变换，协变框架会改变：$e'^a_\mu = \Lambda^a{}_b(x) \, e^b_\mu$。但是[时空度规](@keyword=spacetime_metrics|lang=zh-CN|style=Feynman)会发生什么变化呢？让我们来验证一下：

$$
g'_{\mu\nu} = \eta_{ab} e'^a_\mu e'^b_\nu = \eta_{ab} \left(\Lambda^a{}_c(x) e^c_\mu\right) \left(\Lambda^b{}_d(x) e^d_\nu\right) = \left(\eta_{ab} \Lambda^a{}_c \Lambda^b{}_d\right) e^c_\mu e^d_\nu
$$

根据洛伦兹变换的定义，它是一个保持[闵可夫斯基度规](@keyword=minkowski_metric|lang=zh-CN|style=Feynman)不变的矩阵，所以括号中的项就是 $\eta_{cd}$。这样我们就得到 $g'_{\mu\nu} = \eta_{cd} e^c_\mu e^d_\nu = g_{\mu\nu}$。[时空度规](@keyword=spacetime_metrics|lang=zh-CN|style=Feynman)——即实际的物理几何——完全没有改变！[@problem_id:2995522]。这意味着[局域洛伦兹对称性](@keyword=local_lorentz_symmetry|lang=zh-CN|style=Feynman)是一种**规范对称性**：即我们描述中的一种冗余，它不改变底层的物理，就像选择用摄氏度或华氏度测量温度不会改变实际的炎热程度一样。

### 连接各点：[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)

现在我们在每一点都有了一个局域平直[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)。但我们如何比较P点的[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)中的一个矢量（或旋量）与无穷近的[Q点](@keyword=q_point|lang=zh-CN|style=Feynman)[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)中的一个呢？当我们在弯曲的[流形](@keyword=manifold|lang=zh-CN|style=Feynman)上移动时，我们精心构建的局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)将不可避免地相互扭转和旋转。我们如何追踪这种变化？

我们需要另一个新工具：**[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)** $\omega^a{}_b$。这是一组1-形式，充当着[局域洛伦兹对称性](@keyword=local_lorentz_symmetry|lang=zh-CN|style=Feynman)的“规范场”。它的任务是精确地告诉你，当你沿某一特定方向移动时，你的局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)旋转了多少。如果你有一个旋量 $\psi$，并且想知道当它沿 $x^\mu$ 方向移动时如何变化，你不能只使用[偏导数](@keyword=partial_derivatives|lang=zh-CN|style=Feynman)。你必须使用包含[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)的协变导数：

$$
D_\mu \psi = \left(\partial_\mu + \frac{1}{4} \omega_{\mu ab} \gamma^{ab}\right) \psi
$$

这确保了[导数](@keyword=derivative|lang=zh-CN|style=Feynman)以一种简单、可预测的方式变换。[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)是把所有局域[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)粘合成一个连贯、[可微结构](@keyword=differentiable_structures|lang=zh-CN|style=Feynman)的胶水。

你可能会认为[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)只是谈论时空曲率的一种花哨方式。但它比那更微妙。想象一下，你处于完全平直的[闵可夫斯基空间](@keyword=minkowski_space|lang=zh-CN|style=Feynman)，那里根本没有引力。现在，你决定不使用静态[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)，而是用一个以[角速度](@keyword=angular_velocity|lang=zh-CN|style=Feynman) $\Omega$ *旋转*的[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)来描述一切。尽管[时空](@keyword=space_time|lang=zh-CN|style=Feynman)是平直的，你的[基矢](@keyword=basis_vector|lang=zh-CN|style=Feynman)却在点与点之间变化（具体来说，是从一个时刻到下一个时刻）。如果你为这个[旋转参考系](@keyword=rotating_reference_frames|lang=zh-CN|style=Feynman)计算[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)，你会发现它不是零！实际上，它的分量将与 $\Omega$ 成正比 [@problem_id:1876100]。因此，[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)测量的是[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)场本身的变化，这既可以归因于[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的内禀曲率，也可以仅仅归因于我们选择铺设[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)场的“非自然”方式。

### 法则：零挠率与嘉当方程

这就引出了最后一块拼图：对于给定的几何，我们如何找到其[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman)？在 Einstein 的广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中，我们做出了一个关键的物理假设：[时空](@keyword=space_time|lang=zh-CN|style=Feynman)具有零**挠率**。直观地讲，这意味着如果你沿着两个不同的矢量方向移动来描绘一个无穷小的平行四边形，这个四边形是闭合的。[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的“扭曲”为零。

这个物理假设提供了一个强大的数学约束。它可以用微分形式这种优美而紧凑的语言表达为**[嘉当第一结构方程](@keyword=cartan_s_first_structure_equation|lang=zh-CN|style=Feynman)**：

$$
d e^a + \omega^a{}_b \wedge e^b = 0
$$

在这里，$d$ 是外微分，$\wedge$ 是[楔积](@keyword=wedge_product|lang=zh-CN|style=Feynman)。不要被这些符号吓到。可以把它想象成一台机器 [@problem_id:1027636] [@problem_id:1876102] [@problem_id:1491763]。你输入你的协变框架 $e^a$（它描述了几何）。然后这个方程转动曲柄，就会得到与该几何相容且保证零挠率的唯一[自旋联络](@keyword=spin_connection|lang=zh-CN|style=Feynman) $\omega^a{}_b$。它完美地打包了关于[时空曲率](@keyword=spacetime_curvature|lang=zh-CN|style=Feynman)和你所选协变框架场扭曲的信息。

有趣的是，我们可以放宽这个假设。如果我们考虑挠率*不*为零的理论，即 $T^a = de^a + \omega^a{}_b \wedge e^b \neq 0$ 会怎样？那么联络就会比标准广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)包含更多的信息。这为[替代引力理论](@keyword=alternative_gravity|lang=zh-CN|style=Feynman)打开了大门，比如[远平行引力](@keyword=teleparallel_gravity|lang=zh-CN|style=Feynman)，其中引力的物理学不是由曲率描述，而是由[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的扭曲、挠率特性来描述 [@problem_id:1491789]。

### 关于坐标的一点说明：非完整宇宙

最后一个微妙之处。我们在每一点都创造了这套奇妙的正交归一[基矢](@keyword=basis_vector|lang=zh-CN|style=Feynman) $\mathbf{e}_{(a)}$。人们很容易认为这个[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)场可以用来在整个[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中定义一个新的、“良好”的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)。如果[基矢](@keyword=basis_vector|lang=zh-CN|style=Feynman)相互对易——也就是说，如果**李括号** $[\mathbf{e}_{(a)}, \mathbf{e}_{(b)}]$ 总是为零——那么这将是正确的。这样的基底被称为**完整**的。

然而，在弯曲空间中，情况几乎从非如此。观测者会使用的物理上自然的[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)通常是**非完整**的。例如，在我们膨胀宇宙的[标准宇宙学模型](@keyword=standard_cosmological_model|lang=zh-CN|style=Feynman)中，与宇宙膨胀共同移动的观测者自然使用的[参考系](@keyword=reference_frames|lang=zh-CN|style=Feynman)场就是非完整的。对应于时间和径向距离的[基矢](@keyword=basis_vector|lang=zh-CN|style=Feynman)不对易 [@problem_id:1517058]。这是一个深刻的几何事实。它告诉我们，我们局域的、物理的“直”的概念无法拼接成一个全局的、直线的网格。我们这个由局域平直舞台构成的宇宙，并不能形成一个全局平直的剧院；它在根本上是不可约地弯曲的。而正是协变框架和联络的语言，让我们能够在其中航行。