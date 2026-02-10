## 引言
测量宇宙的浩瀚广袤是天文学最根本的挑战之一。在地球上，距离是一个直观的概念，但在一个膨胀的宇宙中，时空结构本身在伸展，这使我们的测量和直觉变得复杂。这种固有的动力学特性意味着单一的距离定义是不够的，从而在我们的地球经验和宇宙现实之间造成了知识鸿沟。本文旨在探讨这一复杂主题，以清晰地阐明我们如何绘制天图。首先，在“原理与机制”一章中，我们将深入探讨理论框架，定义[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)、[固有距离](@keyword=proper_distance|lang=zh-CN|style=Feynman)、[光度距离](@keyword=luminosity_distance|lang=zh-CN|style=Feynman)和[角直径距离](@keyword=angular_diameter_distance|lang=zh-CN|style=Feynman)等基本概念。我们将探索这些概念如何源于时空的膨胀和光的特性。接下来，“应用与跨学科联系”一章将展示天文学家如何将这些标度用作强大的工具——从确定宇宙的膨胀速率，到探测[暗能量](@keyword=dark_energy|lang=zh-CN|style=Feynman)的性质，再到使用[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)波等革命性新方法。要开始我们的旅程，我们必须首先学习由我们动态的宇宙所决定的新的测量规则。

## 原理与机制

在膨胀的宇宙中谈论“距离”，就意味着进入了一个新的领域，在这里，我们在看似静态的地球上磨练出的日常直觉，必须让位于一个更宏伟、更微妙的现实。如果宇宙是一个固定不变的舞台，距离将会很简单——即两点之间的直线间隔。但我们的舞台并非静止不变，它本身就是动态的、不断伸展的时空结构。要绘制宇宙图景，我们必须首先学习其新的测量规则。

### 膨胀的网格：[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)和[固有距离](@keyword=proper_distance|lang=zh-CN|style=Feynman)

想象一下，宇宙是一张无限的、透明的坐标纸，而星系是画在上面的墨点。随着宇宙膨胀，这张纸本身也在伸展，并带着这些墨点一起移动。这些点在此网格上的坐标——它们的“地址”——保持不变。这个网格代表**[共动坐标](@keyword=comoving_coordinates|lang=zh-CN|style=Feynman)**，而沿着这个不变的网格测量的两个星系之间的距离就是**[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)**，我们可以称之为 $\chi$。这是最基本的分离量度，因为它剔除了宇宙整体膨胀的影响。

然而，在任意一个宇宙时间瞬间，用一把假设的、无限长的卷尺所能测量的“真实”距离是**[固有距离](@keyword=proper_distance|lang=zh-CN|style=Feynman)**。它就是[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)乘以宇宙在该时刻已经伸展的程度。这个“伸展因子”就是著名的**尺度因子**，用 $a(t)$ 表示。因此，在时间 $t$ 的[固有距离](@keyword=proper_distance|lang=zh-CN|style=Feynman) $D_p$ 为 $D_p(t) = a(t) \chi$。今天，我们设定尺度因子 $a(t_0) = 1$，这意味着当前到某个遥远星系的[固有距离](@keyword=proper_distance|lang=zh-CN|style=Feynman)在数值上等于其[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)。

但我们如何求得这个[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)呢？我们无法铺设卷尺。我们从遥远宇宙接收的唯一信使是光子——光的粒子。来自遥远星系的光子需要经过数十亿年的旅行才能到达我们的望远镜。在它飞行的过程中，其下方的宇宙在持续膨胀。因此，[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)是光子在向我们行进的旅程中，在膨胀的网格上所覆盖的总距离。在数学上，这段旅程由一个积分来描述。对于一个在时间 $t_e$ 发射、在今天 $t_0$ 接收到的光子，其[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)是：

$$
\chi = \int_{t_e}^{t_0} \frac{c}{a(t)} dt
$$

这里，$c$ 是光速。请注意，光子相对于该网格的速度并非恒定；由于膨胀，它的速度被有效地减慢了，这由 $1/a(t)$ 项表示。为了求解这个积分，我们必须知道在光的发射和接收之间，宇宙的整个膨胀历史 $a(t)$ [@problem_id:1860458]。

### 观测者的工具箱：亮度和大小

既然我们无法直接测量光的传播路径，就必须更加巧妙。天文学家依赖遥远天体的两个主要属性：它们看起来有多亮和它们看起来有多大。这两个简单的观测引出了两种本质上截然不同的[宇宙学距离](@keyword=cosmological_distances|lang=zh-CN|style=Feynman)类型。

#### [光度距离](@keyword=luminosity_distance|lang=zh-CN|style=Feynman)：它有多暗？

想象一下你看到一盏远处的街灯。你知道所有这类街灯都使用相同的100瓦灯泡（即固有光度 $L$）。通过测量它在你看来有多暗（即其通量 $F$），你可以使用熟悉的平方反比定律 $F = L / (4\pi d^2)$ 来计算它的距离。这就是**[标准烛光](@keyword=standard_candles|lang=zh-CN|style=Feynman)**的原理。

在宇宙学中，这个推断出的距离被称为**[光度距离](@keyword=luminosity_distance|lang=zh-CN|style=Feynman)**，$D_L$。但是，时空的膨胀给这个简单的图像带来了两个麻烦。首先，当光在膨胀的宇宙中传播时，其波长会被拉伸。这就是宇宙学**红移**，$z$。更长的波长意味着每个光子的能量更低，因此天体看起来更暗。这个效应使观测到的通量减少了 $(1+z)$ 倍。其次，膨胀也拉伸了相继到达的光子之间的时间间隔。如果一个星系以一秒的间隔发射两个光子，它们到达我们望远镜的时间间隔将超过一秒。这种时间膨胀效应进一步降低了测量的通量，同样是减少了 $(1+z)$ 倍。

由于观测到的通量被这两个效应共同削弱，它与 $1/(1+z)^2$ 成正比。因此，我们必须使用的平方反比定律被修正了。如果 $D_M$ 是考虑了空间几何的[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)（我们稍后会回到这点！），那么[光度距离](@keyword=luminosity_distance|lang=zh-CN|style=Feynman)是：

$$
D_L = (1+z) D_M
$$

一个[红移](@keyword=redshift|lang=zh-CN|style=Feynman) $z=1$ 的天体，仅仅由于这些宇宙学效应，其亮度看起来就像它的距离是其[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)所暗示的两倍一样远。

#### [角直径距离](@keyword=angular_diameter_distance|lang=zh-CN|style=Feynman)：它有多小？

现在想象你看到一辆远处的汽车。你知道所有这类汽车都是5米长（即固有尺寸 $d$）。通过测量它在你视野中占据的微小角度（$\delta\theta$），你可以用简单的三角学公式 $d = D_A \delta\theta$ 来计算它的距离。这就是**[标准尺](@keyword=standard_ruler|lang=zh-CN|style=Feynman)**的原理。

这个推断出的距离就是**[角直径距离](@keyword=angular_diameter_distance|lang=zh-CN|style=Feynman)**，$D_A$。在这里，膨胀也耍了一个有趣的把戏。向我们展示天体[角大小](@keyword=angular_size|lang=zh-CN|style=Feynman)的光，是在宇宙比现在小得多的时候发出的——具体来说，小了 $1/(1+z)$ 倍。在我们今天看到的光被发射时，该天体在物理上（以[固有距离](@keyword=proper_distance|lang=zh-CN|style=Feynman)衡量）要近得多。由于它在发射时更近，所以它看起来比你天真预期的要*更大*，从而显得*更近*。这个效应意味着[角直径距离](@keyword=angular_diameter_distance|lang=zh-CN|style=Feynman)与[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman) $D_M$ 的关系如下：

$$
D_A = \frac{D_M}{1+z}
$$

这导致了宇宙学中最奇特也最奇妙的预测之一：一个固定大小的天体，随着我们看向更高的[红移](@keyword=redshift|lang=zh-CN|style=Feynman)，它会显得越来越小，但这只到某一点为止。超过某个特定的红移（在我们的宇宙中大约是 $z \approx 1.6$），随着距离的增加，天体在天空中实际上会开始显得*更大*！我们看到它们的时候，宇宙是如此年轻和微小，以至于它们的[视大小](@keyword=angular_size|lang=zh-CN|style=Feynman)又开始增大了。

### 深刻的统一性：[Etherington关系](@keyword=etherington_relation|lang=zh-CN|style=Feynman)

我们现在有了两个截然不同的、操作上定义的距离，$D_L$ 和 $D_A$，它们似乎以相反的方式依赖于[红移](@keyword=redshift|lang=zh-CN|style=Feynman)。一个使物体看起来更远，另一个则更近。然而，它们并非[相互独立](@keyword=mutual_independence|lang=zh-CN|style=Feynman)。它们被一个优美简洁而又强大的方程联系在一起，即**[Etherington互易关系](@keyword=etherington_reciprocity_relation|lang=zh-CN|style=Feynman)**：

$$
D_L = (1+z)^2 D_A
$$

这个关系是现代宇宙学的基石。它不是一个假设，而是光在任何[有效引力](@keyword=effective_gravity|lang=zh-CN|style=Feynman)度规理论（包括广义相对论）中沿[测地线](@keyword=autoparallel_curve|lang=zh-CN|style=Feynman)传播方式的直接结果 [@problem_id:191995] [@problem_id:828685]。它的有效性是对我们物理学理解的基本检验。当一个天体的[红移](@keyword=redshift|lang=zh-CN|style=Feynman)为 $z=1$ 时，其[光度距离](@keyword=luminosity_distance|lang=zh-CN|style=Feynman)是其在发射时刻的[固有距离](@keyword=proper_distance|lang=zh-CN|style=Feynman)的四倍，这一事实正是这个优美原理的直接结果 [@problem_id:828685]。

这个关系可以直接观测。考虑一个星系的**表面亮度**——即单位天区面积内包含了多少光。总亮度随 $D_L^2$ 下降，而它所占据的天区面积随 $D_A^2$ 下降。因此，表面亮度与 $(D_A/D_L)^2$ 成比例，根据[Etherington关系](@keyword=etherington_relation|lang=zh-CN|style=Feynman)，这等于 $(1+z)^{-4}$。遥远星系的单位面积亮度比邻近星系要暗得多，这种现象被称为宇宙学昏暗效应，它使得观测[早期宇宙](@keyword=early_universe|lang=zh-CN|style=Feynman)成为一项巨大的挑战 [@problem_id:278922]。

### 宇宙配方与空间形状

为了实际计算这些距离中的任何一个的数值，我们必须回到那个计算[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)的基本积分。这需要知道由宇宙的内含物通过爱因斯坦的弗里德曼方程决定的膨胀历史 $a(t)$。宇宙膨胀是一场宇宙级的拔河比赛，一方是试图使其减速的物质和暗物质的[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)拉力，另一方是试图使其加速的暗能量的排斥推力。

对于一个只充满物质的简单、假设性的宇宙（一个“爱因斯坦-德西特”宇宙），这些方程可以被精确求解。到[红移](@keyword=redshift|lang=zh-CN|style=Feynman)为 $z$ 的天体的[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)结果是一个简洁的解析函数 [@problem_id:1860458]：

$$
\chi(z) = \frac{2c}{H_0} \left(1 - \frac{1}{\sqrt{1+z}}\right)
$$

其中 $H_0$ 是哈勃常数，即今天的膨胀率。我们可以使用这样的模型在一个简化的设定中探索距离和红移之间的关系 [@problem_id:1862787] [@problem_id:935216]。

然而，我们真实的宇宙不仅包含物质，还含有大量的暗能量，这是一种导致膨胀加速的神秘成分。在这个更现实的**Λ冷暗物质（ΛCDM）**模型中，膨胀历史 $H(z)$ 更为复杂，而[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)的积分通常没有简单的闭合解。我们必须借助计算机对任意给定的[红移](@keyword=redshift|lang=zh-CN|style=Feynman)进行数值计算 [@problem_id:3469306]。

此外，时空本身可以有整体曲率。它可以是**平坦的**（像一张纸，$\Omega_k=0$），**闭合的**（像球面，$\Omega_k \lt 0$），或者**开放的**（像[马鞍面](@keyword=hyperbolic_paraboloid|lang=zh-CN|style=Feynman)，$\Omega_k \gt 0$）。这种曲率影响着广阔尺度上的空间几何。在一个平坦的宇宙中，横向[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman) $D_M$ 就等于视线[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman) $\chi$。但在一个弯曲的宇宙中，几何规则会改变。横向距离 $D_M$ 通过[三角函数](@keyword=trigonometric_functions|lang=zh-CN|style=Feynman)（$\sin$）或[双曲函数](@keyword=hyperbolic_functions|lang=zh-CN|style=Feynman)（$\sinh$）与 $\chi$ 相关，具体取决于空间是闭合的还是开放的。因此，测量到非常遥远天体的距离可以揭示我们整个宇宙的整体形状 [@problem_id:3469235]。

通过测量一系列红移处的[Ia型超新星](@keyword=type_ia_supernovae|lang=zh-CN|style=Feynman)（我们最好的标准烛光）的[光度距离](@keyword=luminosity_distance|lang=zh-CN|style=Feynman)，并将数据与各种模型的预测进行比较，宇宙学家可以精确地确定宇宙的“配方”：物质（$\Omega_m$）、[暗能量](@keyword=dark_energy|lang=zh-CN|style=Feynman)（$\Omega_\Lambda$）和曲率（$\Omega_k$）的相对含量。正是通过这种方法，由暗能量驱动的[宇宙加速膨胀](@keyword=accelerated_expansion_of_the_universe|lang=zh-CN|style=Feynman)被发现了。对于小[红移](@keyword=redshift|lang=zh-CN|style=Feynman)，这些详细的距离标度与更简单的哈勃-勒梅特定律趋于一致，而它们与直线的微小偏离使我们能够测量像**[减速参数](@keyword=deceleration_parameter|lang=zh-CN|style=Feynman)** $q_0$ 这样的参数，该参数量化了宇宙膨胀是正在加速还是减速的速率 [@problem_id:935303]。

这些距离标度所揭示的膨胀历史甚至决定了我们与宇宙的终极联系。在一个[加速膨胀的宇宙](@keyword=accelerating_universe|lang=zh-CN|style=Feynman)中，比如由[宇宙学常数](@keyword=cosmological_constant|lang=zh-CN|style=Feynman)（$w=-1$）驱动的宇宙，存在一个**事件视界**。这是时空中的一个边界，在此之外发生的事件，无论我们等待多久，都永远无法看到，因为空间的膨胀将它们的光带离我们的速度比光向我们传播的速度还要快。对于这样一个宇宙，到这个视界的[固有距离](@keyword=proper_distance|lang=zh-CN|style=Feynman)总是等于哈勃半径 $c/H(t)$——在一个哈勃参数恒定的宇宙中，这是一个恒定的距离 [@problem_id:874296]。事实证明，测量距离无异于绘制我们宇宙的历史、内含物和最终命运。

