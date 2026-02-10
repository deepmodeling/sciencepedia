## 引言
我们如何测量[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上的距离？对于一只在球面上爬行的蚂蚁来说，直接穿过球体内部的路径是不可能的；它的世界仅限于球面本身。这就引出了一个根本性问题：一个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)，或者任何存在于另一个空间内部的空间，是如何获得其自身的几何规则的？答案在于一个优美的数学概念——[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)，它为[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)从包含它的更大空间中继承其距离感提供了一种形式化的方法。本文旨在揭开这一强大思想的神秘面纱，弥合我们对空间的直观理解与弯曲世界的形式化几何之间的知识鸿沟。

接下来的章节将引导您踏上理解这一原理的旅程。首先，在“原理与机制”中，我们将探索[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)的核心思想，学习如何为各种[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)计算它，并揭示它所展现的内蕴几何与外蕴几何之间的深刻区别。然后，在“应用与跨学科联系”中，我们将见证[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)在不同科学领域中的应用，从工程师使用的固[体力](@keyword=body_forces|lang=zh-CN|style=Feynman)学到物理学家描述的[时空](@keyword=space_time|lang=zh-CN|style=Feynman)构造，从而揭示它是一种统一几何学与科学的语言。

## 原理与机制

我们拥有这些优美、光滑的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)——球面、甜甜圈形状的环面，或者其他更奇特的形状——它们都存在于我们所熟悉的三维世界中。我们知道如何在我们的世界中测量距离；很久以前，毕达哥拉斯就为我们提供了蓝图。但是，我们如何测量*在*这些[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上的距离呢？如果你是一只在气球上爬行的蚂蚁，你不可能直接钻一条隧道穿过中心。你必须沿着弯曲的表面行走。问题是，对于那只蚂蚁来说，几何规则是什么？它是否仍然“感觉”自己身处一个平坦的世界，还是它能分辨出自己的宇宙是弯曲的？

答案蕴含在一个极其优雅的思想中，即**[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)**。它是一种让[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)，或任何低维空间（数学家称之为**[流形](@keyword=manifold|lang=zh-CN|style=Feynman) (manifold)**），从其所[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)的更大空间中继承其几何感的方式。它是对蚂蚁的尺子的数学形式化。

### 继承而来的尺子

想象你有一张纸。它是一个二维物体。在你的手中，在三维空间里，你可以将它揉成一个复杂的形状。现在，你将如何测量那张揉皱的纸上两点之间的距离？你不会用一把尺子去测量*穿过空气*的直线距离；你会铺上一把软尺，并在纸上描绘出一条路径。你正在使用三维距离的规则，但你将自己*限制*在纸的二维表面上。

这就是中心思想。点所在的度量空间从环境空间继承其测量工具，即其**度量**。在[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上测量时，一系列越来越近的点，在更大的空间中测量时也是越来越近的。“接近”的定义本身是相同的 [@problem_id:1534001]。

让我们说得更精确一些。我们熟悉的三维[欧几里得空间](@keyword=euclidean_space|lang=zh-CN|style=Feynman)有一个由[毕达哥拉斯定理](@keyword=a^2=b^2+c^2|lang=zh-CN|style=Feynman)定义的度量。用微积分的语言来说，我们说一个分量为 $(dx, dy, dz)$ 的无穷小步长的平方长度是 $ds^2 = dx^2 + dy^2 + dz^2$。这就是我们环境中的“尺子”。

现在，考虑一个简单的一维[流形](@keyword=manifold|lang=zh-CN|style=Feynman)：在三维空间中从点 $\mathbf{p}_1$ 到 $\mathbf{p}_2$ 的一条直线段。我们可以用一个参数（称之为 $t$）来描述这条线上的任意一点，其中 $t$ 从 $0$ 变化到 $1$。位置由 $\mathbf{r}(t) = (1-t)\mathbf{p}_1 + t\mathbf{p}_2$ 给出。沿着这条线的一个小步长对应于一个微小的变化 $dt$。我们在三维空间中移动了多少距离？我们只需使用微积分和[链式法则](@keyword=chain_rule|lang=zh-CN|style=Feynman)！沿线的速度向量是 $\frac{d\mathbf{r}}{dt} = \mathbf{p}_2 - \mathbf{p}_1$。沿曲线的一个无穷小步长 $dt$ 对应于三维空间中的一个位移向量 $d\mathbf{r} = (\mathbf{p}_2 - \mathbf{p}_1)dt$。这个位移的平方长度就是该向量与自身的[点积](@keyword=dot_product|lang=zh-CN|style=Feynman)。线上的[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)，我们称之为 $g_{tt}$，是将 $(dt)^2$ 转换为这个平方长度的因子。事实证明，它就是速度向量的平方长度，对于一条直线来说，这是一个常数：$(x_2-x_1)^2 + (y_2-y_1)^2 + (z_2-z_1)^2$。这正是整个线段长度的平方 [@problem_id:1540347]。

这个过程被称为**[拉回](@keyword=pullback|lang=zh-CN|style=Feynman) (pullback)**。我们有一个从简单的参数空间（$t$ 轴）到更复杂的[环境空间](@keyword=ambient_space|lang=zh-CN|style=Feynman)（$\mathbb{R}^3$）的映射。为了在我们的简单空间中测量距离，我们把我们的步长“推”到大空间中，用大空间的尺子在那里测量它们，然后把测量结果“拉”回来。形式上，如果我们的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman) $M$ 通过函数 $f$ 映射到空间 $N$，且 $N$ 有一个度量 $h$，那么 $M$ 上的[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)（记作 $f^*h$）通过观察[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上的两个[切向量](@keyword=tangent_vectors|lang=zh-CN|style=Feynman) $u,v$ 在更大空间中变成什么样子，并在那里测量它们来度量它们：
$$ (f^*h)_p(u, v) = h_{f(p)}(d_p f(u), d_p f(v)) $$
这里，$d_p f$ 是映射的**[微分](@keyword=pushforward|lang=zh-CN|style=Feynman)**，它告诉我们 $M$ 上的[切向量](@keyword=tangent_vectors|lang=zh-CN|style=Feynman)如何变换成 $N$ 上的[切向量](@keyword=tangent_vectors|lang=zh-CN|style=Feynman)。这听起来可能很抽象，但这正是我们对直线所做的：我们取切向量 $\frac{d}{dt}$，在 $\mathbb{R}^3$ 中找到它的像 $\frac{d\mathbf{r}}{dt}$，然后测量它的长度。

### 弯曲世界的[地图学](@keyword=cartography|lang=zh-CN|style=Feynman)

这种[拉回](@keyword=pullback|lang=zh-CN|style=Feynman)机制是我们成为任何可以想象的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的地图绘制者的关键。我们现在可以创建一张“地图”，告诉我们每一点的几何规则。

让我们在一个半径为 $R$ 的球面上试试这个方法。球面上的一个点由标准的[球坐标](@keyword=spherical_coordinates|lang=zh-CN|style=Feynman)给出，即余纬 $\theta$ 和经度 $\phi$。从我们的二维坐标平面 $(\theta, \phi)$ 到三维空间的映射由以下公式给出：
$$ X(\theta, \phi) = (R \sin\theta \cos\phi, R \sin\theta \sin\phi, R \cos\theta) $$
为了找到[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)，我们需要看我们地图的网格线在画到球面上时是如何拉伸的。我们计算沿着这些网格线的[切向量](@keyword=tangent_vectors|lang=zh-CN|style=Feynman) $\frac{\partial X}{\partial \theta}$ 和 $\frac{\partial X}{\partial \phi}$。这些是三维空间中与球面相切的向量。然后，我们使用标准的欧几里得[点积](@keyword=dot_product|lang=zh-CN|style=Feynman)计算它们的长度和它们之间的[点积](@keyword=dot_product|lang=zh-CN|style=Feynman) [@problem_id:2994945] [@problem_id:2983149]。经过一番代数运算，一个优美的结果出现了。度量分量是：
$$
(g_{ij}) = \begin{pmatrix} R^2 & 0 \\ 0 & R^2 \sin^2\theta \end{pmatrix}
$$
这个矩阵告诉了我们关于球面[内蕴几何](@keyword=intrinsic_geometry|lang=zh-CN|style=Feynman)的一切！相应的无穷小距离是 $ds^2 = R^2 d\theta^2 + R^2 \sin^2\theta d\phi^2$。$g_{\theta\theta}=R^2$ 分量告诉我们，在 $\theta$ 方向（南北向）的一个小步长对应于 $R\,d\theta$ 的距离。$g_{\phi\phi}=R^2 \sin^2\theta$ 分量更有趣。它告诉我们，在 $\phi$ 方向（东西向）的一个小步长对应于 $R\sin\theta\,d\phi$ 的距离。这个 $\sin\theta$ 因子正是[球面几何](@keyword=sphere_geometry|lang=zh-CN|style=Feynman)的自我揭示！它表明，当你靠近两极（$\theta=0$ 或 $\theta=\pi$）时，纬度圈会变小，这一点你凭直觉已经知道了。而非对角项为零的事实告诉你，在球面上，南北向和东西向总是局部垂直的。

让我们绘制另一个世界：一个圆锥。圆锥可以用与[顶点距离](@keyword=vertex_distance|lang=zh-CN|style=Feynman) $r$ 和一个角度 $\theta$ 来[参数化](@keyword=parametrization|lang=zh-CN|style=Feynman)。到三维空间的映射是 $\mathbf{x}(r, \theta) = (r\cos\theta, r\sin\theta, ar)$，其中 $a$ 控制陡峭程度。遵循同样的程序 [@problem_id:1543304]，我们找到度量：
$$
(g_{ij}) = \begin{pmatrix} 1+a^2 & 0 \\ 0 & r^2 \end{pmatrix}
$$
无穷小距离是 $ds^2 = (1+a^2)dr^2 + r^2 d\theta^2$。同样，几何信息被编码在这些分量中。这些规则与球面不同。

### 高斯的绝妙骗局：内蕴几何 vs. 外蕴几何

接下来是真正令人费解的部分。伟大的数学家[卡尔·弗里德里希·高斯](@keyword=carl_friedrich_gauss|lang=zh-CN|style=Feynman)（Carl Friedrich Gauss）发现了一些如此深刻的东西，以至于他称之为他的*[绝妙定理](@keyword=theorema_egregium|lang=zh-CN|style=Feynman) (Theorema Egregium)*。

考虑两个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)。第一个是 $xy$ 平面上的一个简单的平坦区域。第二个是一块圆柱面，比如说半径为 1。在我们的眼中，从三维的有利位置看，它们显然是不同的。一个是平的，一个是弯的。这是它们的**外蕴**几何。

但是，生活*在*[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上的蚂蚁呢？它的**内蕴**几何是什么？让我们计算它们的[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)。
一块平面可以用 $P(u, v) = (u, v, 0)$ 来[参数化](@keyword=parametrization|lang=zh-CN|style=Feynman)。它的[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)是平凡的：$ds^2 = du^2 + dv^2$。这只是二维的毕达哥拉斯定理。
一个圆柱可以“展开”成一个矩形。我们可以将其参数化为 $C(u, v) = (\cos u, \sin u, v)$。现在，让我们计算它的[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)。我们找到切向量，求它们的[点积](@keyword=dot_product|lang=zh-CN|style=Feynman)，结果是…… $ds^2 = du^2 + dv^2$ [@problem_id:2973797]。

这太惊人了。平面和圆柱体具有*完全相同*的[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)！这意味着从内蕴的角度来看——对于我们的蚂蚁在[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上可能进行的任何距离或角度测量——这两个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)是相同的。圆柱体是“内蕴平坦的”。圆柱体上的蚂蚁会认为它生活在一个平面上。它会发现毕达哥拉斯定理成立，三角形的内角和等于 180 度。除非它能以某种方式感知到我们能看到的第三维度，否则它永远无法发现它所处世界的“弯曲性”。

这就是[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)的力量。它完美地将一个空间的[内蕴几何](@keyword=intrinsic_geometry|lang=zh-CN|style=Feynman)属性与其碰巧[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)到更高维度中的方式分离开来。那些可以纯粹从[度量张量](@keyword=metric_tensor|lang=zh-CN|style=Feynman)计算出来的属性，比如 **[高斯曲率](@keyword=gaussian_curvature|lang=zh-CN|style=Feynman) (Gaussian Curvature)**（对于平面和圆柱体都为零），是内蕴的。而那些依赖于[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)的属性，比如**平均曲率 (Mean Curvature)**（对于平面为零，但对于圆柱体不为零），是外蕴的。

### 几何的宇宙

这自然引出了一个深刻的问题。我们已经看到将[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)到 $\mathbb{R}^3$ 中赋予了它们一种几何。但是我们能否在纸上发明某种几何，某种抽象的度量张量，而它*不能*被实现为我们三维世界中的一个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)？

在很长一段时间里，这是一个悬而未决的问题。答案由杰出的数学家约翰·纳什（John Nash）证明，是一个响亮的“不！”。**[纳什嵌入定理](@keyword=nash_embedding_theorem|lang=zh-CN|style=Feynman)**指出，*任何*抽象的黎曼流形（一个在每一点都有一套光滑几何规则的空间）都可以被实现为某个更高维[欧几里得空间](@keyword=euclidean_space|lang=zh-CN|style=Feynman) $\mathbb{R}^N$ 的[子流形](@keyword=submanifolds|lang=zh-CN|style=Feynman)，其[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)与你开始时设定的度量完全相同 [@problem_id:2975241]。

这是另一个深刻的统一原则。它告诉我们，[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)的思想不仅仅是获得几何的一种方式；在某种意义上，它是*唯一*的方式。每一个可以想象的几何世界都可以被看作是生活在一个足够高维的平坦空间中的一个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)，其规则继承自那里简单的毕达哥拉斯定理。

### 当尺子失灵：奇异的几何

为我们的旅程画上句号，让我们考虑最后一个奇怪的转折。如果环境空间不遵守毕达哥拉斯定理会怎样？爱因斯坦的[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)告诉我们，我们的宇宙是一个四维[时空](@keyword=space_time|lang=zh-CN|style=Feynman)，具有一个**伪黎曼**度量，通常写为 $ds^2 = dx^2 + dy^2 + dz^2 - c^2 dt^2$。那个负号是关键的区别。在这个世界里，一个向量的“平方长度”可以是正的（类空）、负的（类时），甚至是零（类光或零性）！

如果我们将一个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)[嵌入](@keyword=embedding|lang=zh-CN|style=Feynman)到这样的空间中，它的[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)可能会有一些非常奇怪的性质。[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)有可能变得**退化**，意味着它的[行列式](@keyword=determinant|lang=zh-CN|style=Feynman)为零。这意味着什么呢？它表示[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上存在一个在[环境空间](@keyword=ambient_space|lang=zh-CN|style=Feynman)中长度为零的方向。在这个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上的蚂蚁可以在某个方向上移动，而它个人的“尺子”却记录不到任何距离 [@problem_id:1533958]。

这不仅仅是一个数学上的好奇心。在广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中，[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的事件视界正是这样的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)——它们是“零[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)”，[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的一个维度与环境[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的类光方向对齐。[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)是让我们能够理解这些终极宇宙边界的奇特而美妙的几何的工具。

从气球上的一只简单蚂蚁到[黑洞](@keyword=black_hole|lang=zh-CN|style=Feynman)的边缘，[诱导度量](@keyword=induced_metric|lang=zh-CN|style=Feynman)是让我们能够讨论一个世界存在于另一个世界之中的几何的基本概念。它是简单与复杂、内蕴与外蕴之间的桥梁，也是现代几何学和物理学大部分内容建立其上的基础。