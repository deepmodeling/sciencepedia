## 应用与跨学科联系

在前面的讨论中，我们就像是学徒机械师，仔细学习我们新工坊里每一样工具的名称和功能：度规、联络、[曲率张量](@keyword=curvature_tensor|lang=zh-CN|style=Feynman)和[导数](@keyword=derivative|lang=zh-CN|style=Feynman)。我们摆弄它们，看看它们是如何组合在一起的。现在，真正的乐趣开始了。我们拿起这些工具，用它们来建造、理解和探索。我们将看到，[微分几何](@keyword=differential_geometry|lang=zh-CN|style=Feynman)这种抽象的语言一点也不抽象；它是物理宇宙的母语。它描述肥皂膜的优美曲线，就像它决定星系在宇宙中的运动一样优雅。这里，就是这套机器焕发生机的地方。

### 形状的逻辑：从肥皂膜到[极小曲面](@keyword=minimal_surfaces|lang=zh-CN|style=Feynman)

让我们从一些你能看到和触摸——或者至少能想象——的东西开始。拿一根弯曲的铁丝，将它[浸入](@keyword=immersions|lang=zh-CN|style=Feynman)肥皂溶液中，然后取出。一层闪闪发光的半透明薄膜将横跨在铁丝的边界上。它为什么会呈现出那样的形状？来自物理学的答案很简单：这个膜会“偷懒”！它会稳定在一个使其总表面[张力](@keyword=tension_force|lang=zh-CN|style=Feynman)能最小化的形状，这意味着它使其表面积最小化。

这种最小化的物理原理在几何语言中有一个直接而优美的对应。一个局部使其面积最小化的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)被称为**极小曲面**（minimal surface）。我们的几何工具可以告诉我们关于这类[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)的非常具体的信息。平均曲率$H$，它是一个点上两个相互垂直方向曲率的平均值，在[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上的每一点都必须为零。$H=0$是由表面[张力](@keyword=tension_force|lang=zh-CN|style=Feynman)塑造的形状的几何标志。

但在这里，一个更深层、更令人惊讶的几何真理显现了出来。如果我们要求[平均曲率](@keyword=mean_curvature|lang=zh-CN|style=Feynman)$H = \frac{k_1 + k_2}{2}$为零，这意味着两个主曲率必须大小相等、符号相反：$k_2 = -k_1$。这对[高斯曲率](@keyword=gaussian_curvature|lang=zh-CN|style=Feynman)$K = k_1 k_2$意味着什么？它必然是$K = k_1(-k_1) = -k_1^2$。由于$k_1^2$永远不可能是负的，所以极小曲面的高斯曲率必须小于或等于零，$K \le 0$ [@problem_id:1653561]。

想想这意味着什么。一个球体处处都有正的[高斯曲率](@keyword=gaussian_curvature|lang=zh-CN|style=Feynman)；它在所有方向上都向外凸出。我们的结果证明了你*永远*无法用肥[皂膜](@keyword=soap_film|lang=zh-CN|style=Feynman)形成一块球面。极小曲面要么是局部平坦的（$K=0$），要么是鞍形的（$K0$），在一个方向向上弯曲，同时在另一个方向向下弯曲。大自然对效率的追求禁止了某些几何形状的存在。这是我们第一次窥见物理学和几何学是如何紧密相连的。

### 宏伟的设计：用引力编织[时空](@keyword=space_time|lang=zh-CN|style=Feynman)

现在让我们从肥皂膜的小尺度优雅转向最宏大的舞台：宇宙本身。我们用来测量地图上或地球表面距离的几何学被称为[黎曼几何](@keyword=riemannian_geometry|lang=zh-CN|style=Feynman)（Riemannian geometry）。正如我们所见，它的一个关键特征是其度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman)是**正定**的。这是一个花哨的说法，意思是任何两个不同点之间的距离总是一个正数。你不可能从A点旅行到B点而路径的“长度”为零[@problem_id:1527197]。

但 Albert Einstein 的伟大洞见在于，我们居住的宇宙不是一个三维空间，而是一个四维的**[时空](@keyword=space_time|lang=zh-CN|style=Feynman)**。而这个[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的几何学有着根本的不同。它由一个伪黎曼（或洛伦兹）度规描述，其最著名的特征是一个负号。在简化的坐标中，两个邻近事件之间的“距离”平方$ds^2$不是$dx^2 + dy^2 + dz^2$，而是$ds^2 = -c^2 dt^2 + dx^2 + dy^2 + dz^2$。

那个负号不是一个数学上的怪癖；它是因果性的几何编码。正因为有了它，沿路径的“距离”平方可以是负的、零或正的。
-   **类时路径**（$ds^2 \lt 0$）是像你我这样比光速慢的大质量物体的轨迹。
-   **类光路径**（$ds^2 = 0$）是光本身的轨迹。
-   **类空路径**（$ds^2 \gt 0$）分隔了因果上无关联的事件；一个事件无法影响另一个。

单是这个结构就是狭义相对论的几何——一个平坦、刚性的舞台。但 Einstein 并未止步于此。他问道：引力是什么？他革命性的答案是，引力不是一种力，而是[时空](@keyword=space_time|lang=zh-CN|style=Feynman)*曲率*的表现。物质和能量告诉[时空](@keyword=space_time|lang=zh-CN|style=Feynman)如何弯曲，而[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的曲率告诉物质如何运动。

为了将这一深刻思想转化为一个量化理论，Einstein 需要找到一个描述曲率的几何量，并且至关重要的是，这个量要像质量和能量那样是“守恒的”。物理定律表明，描述能量和[动量密度](@keyword=momentum_density|lang=zh-CN|style=Feynman)及流动的应力-能量张量$T_{\mu\nu}$的[协变散度](@keyword=covariant_divergence|lang=zh-CN|style=Feynman)为零：$\nabla^\mu T_{\mu\nu} = 0$。Einstein 寻找一个由时空曲率构成且具有相同性质的[张量](@keyword=tensor|lang=zh-CN|style=Feynman)。

他在**爱因斯坦张量**（Einstein tensor）$G_{\mu\nu} = R_{\mu\nu} - \frac{1}{2} R g_{\mu\nu}$中找到了它。奇迹般地，由于一个被称为[比安基恒等式](@keyword=bianchi_identity|lang=zh-CN|style=Feynman)（Bianchi identities）的深刻几何性质，这个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)是自动守恒的：$\nabla^\mu G_{\mu\nu} = 0$ [@problem_id:1508225]。这种对应关系太完美了，不可能是巧合。Einstein 大胆地跨出一步，将它们设为成正比：
$$
G_{\mu\nu} = \frac{8\pi G}{c^4} T_{\mu\nu}
$$
这就是广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)的核心。在右边，是物理学：物质和能量的分布。在左边，是几何学：[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的曲率。它们是一回事。

这个方程描述了什么样的宇宙？我们可以探索最简单的解。考虑一个处处相同、方向也无异的宇宙——一个**[最大对称空间](@keyword=maximally_symmetric_spaces|lang=zh-CN|style=Feynman)**（maximally symmetric space）[@problem_id:1525064]。在这样的空间中，曲率必须是恒定的。这些理想化的模型构成了现代宇宙学的基础。例如，一个带有“[真空能](@keyword=vacuum_energy|lang=zh-CN|style=Feynman)”（由宇宙学常数$\Lambda$表示）的空宇宙对应于一种被称为德西特或[反德西特时空](@keyword=anti_de_sitter_spacetime|lang=zh-CN|style=Feynman)的特殊[最大对称空间](@keyword=maximally_symmetric_spaces|lang=zh-CN|style=Feynman)。这些不仅仅是数学上的奇珍；它们是我们用以研究我们这个[加速膨胀的宇宙](@keyword=accelerating_universe|lang=zh-CN|style=Feynman)的过去和未来的最佳工作模型[@problem_id:1547958]。

### 终极的统一：当局部凸起决定全局形状

我们已经看到，像某一点的曲率这样的局部几何属性如何产生深刻的物理后果。但所有联系中最深刻的一种，是将局部几何与一个空间的全局、整体*形状*——即其拓扑——联系起来。

想象一个完美的球体。它具有一定的“圆度”，即一个在每一点都相同的正[高斯曲率](@keyword=gaussian_curvature|lang=zh-CN|style=Feynman)$K$。现在，想象一个凹凸不平的土豆。它的曲率从一点到另一点变化剧烈——在尖锐的部分曲率很高，在较平坦的区域曲率较低，甚至可能还有负曲率的鞍状凹陷。然而，从拓扑学上讲，这个土豆只是一个变形的球体。它们都是没有洞的[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)。

这些局部的凸起和摆动（几何）与它没有洞这个事实（拓扑）之间是否存在联系？答案是肯定的，而且它是数学中最优美的定理之一：**[陈-高斯-博内定理](@keyword=chern_gauss_bonnet_theorem|lang=zh-CN|style=Feynman)**（Chern-Gauss-Bonnet theorem）。

对于一个二维[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)，该定理指出，如果你将整个[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)上的[高斯曲率](@keyword=gaussian_curvature|lang=zh-CN|style=Feynman)相加，总和与一个纯粹的拓扑数——[欧拉示性数](@keyword=euler_characteristic|lang=zh-CN|style=Feynman)$\chi$——成正比：
$$
\int_M K \, dA = 2\pi \chi(M)
$$
欧拉示性数是一个描述形状拓扑的数字。对于一个球体（或一个土豆），$\chi=2$。对于一个环面（甜甜圈形状），$\chi=0$。对于一个双孔环面，$\chi=-2$。它是一个整数，无论你如何拉伸或弯曲[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)，它都不会改变。

这个定理令人震惊。它说，无论你如何变形一个球体，其所有局部曲率的总和*总是*必须恰好等于$4\pi$。如果你在一个地方制造一个大的正曲率凸起，[曲面](@keyword=2_dimensional_manifold|lang=zh-CN|style=Feynman)必须在别处相应地产生负曲率，以保持总和恒定。局部几何“知道”全局拓扑。

这个原理可以推广到更高维的偶数维空间。曲率变成了一个更复杂的对象，称为[欧拉形式](@keyword=euler_form|lang=zh-CN|style=Feynman)，但思想是相同的。将这个局部几何量在整个空间上积分，得到全局的、拓扑的[欧拉示性数](@keyword=euler_characteristic|lang=zh-CN|style=Feynman)。使这种联系得以成立的神奇要素是[广义斯托克斯定理](@keyword=generalized_stokes__theorem|lang=zh-CN|style=Feynman)（generalized Stokes' theorem），它将一个区域上[导数](@keyword=derivative|lang=zh-CN|style=Feynman)的积分与其边界上的积分联系起来。由于像球体或环面这样的闭合空间没有边界，这就导致了总曲率积分的非凡不变性[@problem_id:2993520]。

从卑微的肥皂膜到宇宙的结构，再到形状的本质，微分几何是将这一切联系在一起的线索。它揭示了一个宇宙，其中物理定律是几何原理的表达，最错综复杂的局部细节与最宏伟的全局真理密不可分。这些工具不仅用于计算，更用于理解。它们是我们观察世界内在美与统一的透镜。