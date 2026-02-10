## 引言
在[微分几何](@keyword=differential_geometry|lang=zh-CN|style=Feynman)学的核心，有一个用以理解空间曲率的强大概念：和乐群。这个群捕捉了矢量沿闭合回路移动时所经历的累积“扭转”，为[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的[内蕴几何](@keyword=intrinsic_geometry|lang=zh-CN|style=Feynman)提供了独特的指纹。虽然大多数[流形](@keyword=manifold|lang=zh-CN|style=Feynman)表现出普遍的旋转行为，但 Marcel Berger 的开创性工作揭示了少数几个“特殊”和乐群的存在，它们标志着非凡几何结构的存在。其中最引人入胜的是[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)[和乐群](@keyword=holonomy_groups|lang=zh-CN|style=Feynman)——$\mathrm{Sp}(n)$ 和 $\mathrm{Sp}(n)\mathrm{Sp}(1)$，它们分别支配着[超凯勒流形](@keyword=hyperkähler_manifold|lang=zh-CN|style=Feynman)和[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)凯勒流形的几何。本文旨在探讨区分这两种密切相关几何的根本原因，以及为何这种区分如此重要。

本文的探索分为两部分。在“原理与机制”部分，我们将解析这些[和乐群](@keyword=holonomy_groups|lang=zh-CN|style=Feynman)之间的核心差异，对比 $\mathrm{Sp}(n)$ 的“冻结”四元数结构与 $\mathrm{Sp}(n)\mathrm{Sp}(1)$ 的“旋转”结构，并揭示这如何决定了曲率等关[键性](@keyword=bond_character|lang=zh-CN|style=Feynman)质。随后，“应用与跨学科联系”部分将展示这些抽象概念如何为构造几何空间提供了必不可少的工具，并成为现代物理学理论（如[超对称](@keyword=supersymmetry|lang=zh-CN|style=Feynman)和弦理论）的基础语言。为了开始理解几何如何产生这种扭转，让我们从一个思想实验开始。

## 原理与机制

想象你是一个在球面上行走的无穷小探险家。你手持一杆长矛，并决心在行走时让它始终指向“相同”的方向。你从赤道出发，将长矛指向北方。你沿着赤道行进了全球周长的四分之一，然后转向正北，走到北极。最后，你沿着一条经线走回起点。你完成了一个三角形回路，在此期间，你一丝不苟地保持长矛相对于你的路径没有旋转——数学家将这个过程称为**平行输运** (parallel transport)。然而，当你回到起点时，你发现长矛不再指向北方，而是指向了东方！它旋转了 90 度。

这种扭转效应是球面曲率的直接结果。一个矢量从某个起点出发，在沿所有可能的闭合回路进行平行输运后所能经历的所有变换的集合，构成一个数学群，称为**和乐群** (holonomy group)。这个群是[流形几何](@keyword=manifold_geometry|lang=zh-CN|style=Feynman)的有力指纹，它编码了其曲率的本质。和乐原理是现代几何学的基石之一，它告诉我们，任何在[平行输运](@keyword=vector_transport_on_curved_space|lang=zh-CN|style=Feynman)下保持不变的几何结构，都必然是在和乐群作用下保持不变的结构。

### 几何的“[元素周期表](@keyword=periodic_table|lang=zh-CN|style=Feynman)”

你可能会认为，可能的和乐群种类会是无穷无尽的，就像人们能想象的形状一样多种多样。然而，数学家 Marcel Berger 在 1950 年代有了一个惊人的发现：事实并非如此。对于一大类重要的空间（单连通、不可约且非过度对称），可能的和乐群列表非常简短和固定。它就像一张几何的“[元素周期表](@keyword=periodic_table|lang=zh-CN|style=Feynman)”。对于一个 $m$ 维的有向空间，“一般”的和乐群是 $\mathrm{SO}(m)$，即所有旋转构成的群。但在特殊的维度下，和乐群可以缩小或“约化”为更小、更有趣的群，这预示着存在着额外的、优美的结构。

在 Berger 的列表中，对于维度是四的倍数（比如 $\dim = 4n$）的空间，我们发现了两个特别迷人的近亲：紧[辛群](@keyword=symplectic_group|lang=zh-CN|style=Feynman) $\mathrm{Sp}(n)$ 及其更大的表亲 $\mathrm{Sp}(n)\mathrm{Sp}(1)$ [@problem_id:2980127]。具有这些[和乐群](@keyword=holonomy_groups|lang=zh-CN|style=Feynman)的[流形](@keyword=manifold|lang=zh-CN|style=Feynman)正是我们此行的主题。它们是构建在[四元数代数](@keyword=quaternion_algebras|lang=zh-CN|style=Feynman)之上的世界，这种四维数系由 [William Rowan Hamilton](@keyword=william_rowan_hamilton|lang=zh-CN|style=Feynman) 发现。

### 四元数结构：冻结 vs. 旋转

要理解这些群，让我们首先看一下最简单的 $4n$ 维世界：平坦的[欧几里得空间](@keyword=euclidean_space|lang=zh-CN|style=Feynman) $\mathbb{R}^{4n}$。你可能已经猜到，它的[和乐群](@keyword=holonomy_groups|lang=zh-CN|style=Feynman)是平凡的；沿任何回路的平行输运都会使矢量原封不动地返回 [@problem_id:2980124]。然而，即使在这个看似平淡无奇的环境中，我们也可以定义一个“四元数结构”。我们可以确定三个不同的变换，称之为 $I, J, K$，它们作用于该空间中的矢量，并遵循与 Hamilton 的[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)单位 $i, j, k$ 相同的代数规则：即 $I^2 = J^2 = K^2 = IJK = -\mathrm{Id}$。这可以被认为是定义“90 度转动”的三种不同方式，每一种都是一个独特的[复结构](@keyword=complex_structure|lang=zh-CN|style=Feynman)。

在平坦空间中，这些结构 $I, J, K$ 是协变常数——它们在平行输运下保持不变。因此，（平凡的）和乐群必须是保持 $I, J, K$ 不变的群的[子群](@keyword=subgroup|lang=zh-CN|style=Feynman)。而这个保持不变的群恰好是 $\mathrm{Sp}(n)$。这给了我们第一个线索：[和乐群](@keyword=holonomy_groups|lang=zh-CN|style=Feynman) $\mathrm{Sp}(n)$ 与一个*固定的*、平行的四元数结构的存在密切相关。

现在，让我们进入弯曲的世界。正是在这里，这个家族产生了分化。

- **[超凯勒流形](@keyword=hyperkähler_manifold|lang=zh-CN|style=Feynman) (Hyperkähler Manifolds) (和乐群 $\mathrm{Sp}(n)$):** 在这些空间中，几何结构使得三个[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)结构 $I, J, K$ 全都是**协变常数**。就像在平坦空间中一样，它们被“冻结”在[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的构造之中。无论你将它们[平行输运](@keyword=vector_transport_on_curved_space|lang=zh-CN|style=Feynman)到何处，它们都保持不变。和乐群仅由分别保持这三个结构不变的变换组成 [@problem_id:2979275]。这种刚性带来了深远的影响。

- **四元数凯勒流形 (Quaternionic Kähler Manifolds) (和乐群 $\mathrm{Sp}(n)\mathrm{Sp}(1)$):** 这里的情况更具动态性。单个的结构 $I, J, K$ *不是*协变常数。当你沿着路径输运它们时，它们会相互混合和旋转。和乐群中额外的 $\mathrm{Sp}(1)$ 因子（它同构于[单位四元数](@keyword=unit_quaternions|lang=zh-CN|style=Feynman)群，或 $\mathrm{SU}(2)$）正是这种旋转的动因。被保持的不是任何单一的复结构，而是在每一点上它们所张成的整个三维空间。这个空间构成一个秩为 3 的[向量丛](@keyword=vector_bundles|lang=zh-CN|style=Feynman)，我们可以称之为**四元数丛** $Q$。因此，对于四元数凯勒流形，联络保持丛 $Q$ 不变，但其中的结构却在不断旋转 [@problem_id:2980140]。想象一下你携带一个三脚架：在[超凯勒流形](@keyword=hyperkähler_manifold|lang=zh-CN|style=Feynman)上，它平移而不转动。而在[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)[凯勒流形](@keyword=kähler_manifold|lang=zh-CN|style=Feynman)上，三脚架在平移的同时自身也在旋转。

这种差异可以通过思考在丛 $Q$ 上诱导的联络来完美地捕捉。在[超凯勒流形](@keyword=hyperkähler_manifold|lang=zh-CN|style=Feynman)上，平行标架 $(I,J,K)$ 的存在意味着这个[诱导联络](@keyword=induced_connection|lang=zh-CN|style=Feynman)是平坦且平凡的。而在[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)凯勒流形上，这个联络通常是弯曲的，其曲率正是驱动“旋转”的原因 [@problem_id:2979275]。

### 和乐的指令：曲率与物理定律

我们为什么要关心这种冻结与旋转结构之间的区别？因为和乐决定了物理。[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的和乐群以非常具体的方式约束其曲率，并将其与物理学中最重要的方程之一——爱因斯坦场方程——联系起来。

如果一个[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的[里奇曲率张量](@keyword=ricci_curvature_tensor|lang=zh-CN|style=Feynman)与度量成正比，即 $\mathrm{Ric} = \lambda g$，那么它被称为**[爱因斯坦流形](@keyword=einstein_manifolds|lang=zh-CN|style=Feynman)**。一个在弦理论和超对称中极为重要的特例是当常数 $\lambda$ 为零时，此时[流形](@keyword=manifold|lang=zh-CN|style=Feynman)是**里奇平坦的**。

- **和乐群 $\mathrm{Sp}(n) \implies$ 里奇平坦:** [超凯勒流形](@keyword=hyperkähler_manifold|lang=zh-CN|style=Feynman)总是里奇平坦的。三个平行的、相容的复结构的存在，以一种特殊的方式约束了曲率，迫使里奇张量恒为零。其背后的直观原因很深刻：这些平行结构的存在意味着一个称为典范丛的相关对象是平凡的。这个丛的曲率恰好就是里奇张量。一个配有相容联络的平凡丛必须有零曲率，因此 $\mathrm{Ric}=0$ [@problem_id:2974182]。这些空间代表了爱因斯坦方程的[真空解](@keyword=vacuum_solution|lang=zh-CN|style=Feynman)，是完美平衡的几何舞台。

- **和乐群 $\mathrm{Sp}(n)\mathrm{Sp}(1) \implies$ [爱因斯坦流形](@keyword=einstein_manifolds|lang=zh-CN|style=Feynman):** [四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)凯勒流形（维度 $\ge 8$）总是[爱因斯坦流形](@keyword=einstein_manifolds|lang=zh-CN|style=Feynman)，但通常*不是*里奇平坦的。正是那个将其与[超凯勒流形](@keyword=hyperkähler_manifold|lang=zh-CN|style=Feynman)区分开来的特征——旋转的 $\mathrm{Sp}(1)$ 因子——导致了非零的里奇曲率。[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的曲率可以分解为位于李代数 $\mathfrak{sp}(n)$ 中的部分和位于 $\mathfrak{sp}(1)$ 中的部分。结果表明，$\mathfrak{sp}(n)$ 部分是里奇平坦的，而整个[里奇张量](@keyword=ricci_tensor|lang=zh-CN|style=Feynman)是由 $\mathfrak{sp}(1)$ 分量产生的 [@problem_id:2980129]。可以说，是旋转创造了物质-能量。

### [标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman)：连接两个世界的桥梁

所以，我们有两类[流形](@keyword=manifold|lang=zh-CN|style=Feynman)：里奇平坦、“冻结”的[超凯勒流形](@keyword=hyperkähler_manifold|lang=zh-CN|style=Feynman)，和爱因斯坦、“旋转”的[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)[凯勒流形](@keyword=kähler_manifold|lang=zh-CN|style=Feynman)。是什么将它们联系在一起？这座桥梁是在每一点都可以计算的一个数字：**[标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman)** $s$。

在四元数[凯勒流形](@keyword=kähler_manifold|lang=zh-CN|style=Feynman)上，旋转的 $\mathrm{Sp}(1)$ 丛的曲率与[流形](@keyword=manifold|lang=zh-CN|style=Feynman)的标量曲率 $s$ 成正比 [@problem_id:2980141]。这是一个非凡的联系，它将曲率的大尺度平均值 ($s$) 与[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)结构的[无穷小旋转](@keyword=infinitesimal_rotations|lang=zh-CN|style=Feynman)联系起来。

这意味着一些奇妙的事情。如果[标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman) $s$ 为零，那么 $\mathrm{Sp}(1)$ 的曲率必须消失。旋转停止了！[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)丛 $Q$ 上的联络变得平坦。这意味着，至少在局部上，可以找到一个平行的、“冻结”的标架 $(I,J,K)$，[流形](@keyword=manifold|lang=zh-CN|style=Feynman)因此变为**局部超凯勒**[流形](@keyword=manifold|lang=zh-CN|style=Feynman)。和乐群从 $\mathrm{Sp}(n)\mathrm{Sp}(1)$ 局部约化为 $\mathrm{Sp}(n)$ [@problem_id:2980133]。

一个[标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman)为零的四元数凯勒流形是否*全局*是[超凯勒流形](@keyword=hyperkähler_manifold|lang=zh-CN|style=Feynman)，就成了一个拓扑问题。如果[流形](@keyword=manifold|lang=zh-CN|style=Feynman)是[单连通的](@keyword=simply_connected|lang=zh-CN|style=Feynman)（意味着任何闭合回路都可以收缩到一个点），那么 $Q$ 丛的这种[局部平坦性](@keyword=local_flatness|lang=zh-CN|style=Feynman)保证了它可以在全局上平凡化。一个局部的冻结标架可以扩展到任何地方，[流形](@keyword=manifold|lang=zh-CN|style=Feynman)就此被揭示为一个真正的全局[超凯勒流形](@keyword=hyperkähler_manifold|lang=zh-CN|style=Feynman) [@problem_id:2980133]。如果 $s \neq 0$，旋转就是不可避免的，$Q$ 丛的曲率非零，这构成了即使是单个来自[四元数](@keyword=quaternions|lang=zh-CN|style=Feynman)族的平行[复结构](@keyword=complex_structure|lang=zh-CN|style=Feynman)也无法存在的基本障碍 [@problem_id:2980141]。

### 一个充满可能性的球面

让我们回到[超凯勒流形](@keyword=hyperkähler_manifold|lang=zh-CN|style=Feynman)那刚性而优美的世界。我们说过它们拥有三个平行的[复结构](@keyword=complex_structure|lang=zh-CN|style=Feynman) $I, J, K$。但现实甚至更为丰富。事实证明，任何形如 $\mathcal{J} = aI + bJ + cK$ 的[线性组合](@keyword=linear_combinations|lang=zh-CN|style=Feynman)，只要其中 $a, b, c$ 是满足 $a^2+b^2+c^2=1$ 的实数，那么它*也*是一个平行的复结构。

这意味着[超凯勒流形](@keyword=hyperkähler_manifold|lang=zh-CN|style=Feynman)不仅仅被赋予了三个特定的[复结构](@keyword=complex_structure|lang=zh-CN|style=Feynman)，而是拥有整整一个 **[2-球面](@keyword=s2_sphere|lang=zh-CN|style=Feynman)**的[复结构](@keyword=complex_structure|lang=zh-CN|style=Feynman)！在每一点，所有可用的平行复结构的集合构成一个球面，称为扭量球 (twistor sphere)。人们可以挑选这个球面上的任何一点，并将该[超凯勒流形](@keyword=hyperkähler_manifold|lang=zh-CN|style=Feynman)视为关于该选择的标准凯勒流形。这种几何不仅由一个刚性的三脚架定义，而是由一个充满可能性的完美球面所定义，这证明了隐藏在[和乐](@keyword=holonomy|lang=zh-CN|style=Feynman)约束之下的深刻而统一的美 [@problem_id:2980146]。