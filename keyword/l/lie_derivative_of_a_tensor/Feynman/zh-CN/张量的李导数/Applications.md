## 应用与跨学科联系

我们花了一些时间来了解一个相当抽象的数学概念——[李导数](@keyword=lie_derivatives|lang=zh-CN|style=Feynman)。我们已经看到了它是如何定义的以及如何计算它。但是，一个工具的好坏取决于它能完成的工作。所以，让我们把这个优雅的工具从盒子里拿出来，投入使用。我们将看到，这一思想是一条金线，将物理学和数学中一些最美丽的概念联系在一起，从我们日常世界熟悉的对称性，到爱因斯坦宇宙最深层的原理。李导数不仅仅是一个公式；它是一种提出深刻问题的方式：“当万物都在运动时，什么保持不变？”

### “保持不变”的几何学

想象一下，你站在一个完全均匀、无限大的冰面上。如果你向前迈出一步，你周围的几何结构会改变吗？不会。如果你原地转一圈，冰本身会看起来有任何不同吗？不会。这些不变的变换——[平移和旋转](@keyword=translation_and_rotation|lang=zh-CN|style=Feynman)——在几何学家看来就是*[等距变换](@keyword=isometry|lang=zh-CN|style=Feynman)*。它们是空间的对称性。[李导数](@keyword=lie_derivatives|lang=zh-CN|style=Feynman)给了我们一种极其直接的方式来讨论这些对称性。

在上一节中，我们看到李导数 $\mathcal{L}_X T$ 告诉我们一个[张量场](@keyword=tensor_fields|lang=zh-CN|style=Feynman) $T$ 当我们沿着由[矢量场](@keyword=vector_field|lang=zh-CN|style=Feynman) $X$ 定义的路径“流动”时是如何变化的。一个空间的几何结构被编码在其度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman) $g$ 中。所以，空间的对称性是一个沿着[矢量场](@keyword=vector_field|lang=zh-CN|style=Feynman) $X$ 的流，这个流*使度规保持不变*。其数学表述简单得令人惊叹：

$$
\mathcal{L}_X g = 0
$$

任何满足此条件的[矢量场](@keyword=vector_field|lang=zh-CN|style=Feynman) $X$ 都被称为**[基灵矢量场](@keyword=killing_vector_fields|lang=zh-CN|style=Feynman)**，以 Wilhelm Killing 的名字命名。它是对称性的无穷小生成元。寻找一个[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的[基灵矢量场](@keyword=killing_vector_fields|lang=zh-CN|style=Feynman)，就像是寻找所有在其中移动而不会扰动其几何结构的方式。

对于我们在学校里都学过的平直平面来说，这是非常直观的。生成绕原点旋转的[矢量场](@keyword=vector_field|lang=zh-CN|style=Feynman) $X = -y \partial_x + x \partial_y$ 是一个[基灵矢量场](@keyword=killing_vector_fields|lang=zh-CN|style=Feynman) [@problem_id:1528271]。如果你沿着它流动，一切都只是旋转，但点与点之间的距离保持不变。对于一个简单的平移也是如此，在合适的[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)下，它只是一个常[矢量场](@keyword=vector_field|lang=zh-CN|style=Feynman) [@problem_id:1649431]。[李导数](@keyword=lie_derivatives|lang=zh-CN|style=Feynman)证实了我们直觉已经知道的：对于一个平坦无特征的平面，[平移和旋转](@keyword=translation_and_rotation|lang=zh-CN|style=Feynman)不会改变其几何。

但这个工具的真正威力在于它适用于*任何*空间，无论多么弯曲或奇异。一个完美的球面具有[旋转对称](@keyword=rotational_symmetry|lang=zh-CN|style=Feynman)性，因此，它拥有生成这些旋转的[基灵矢量场](@keyword=killing_vector_fields|lang=zh-CN|style=Feynman) [@problem_id:537561]。奇怪的、马鞍状的双曲几何世界也是如此 [@problem_id:990706]。要真正体会到这一点，可以考虑[爱因斯坦方程](@keyword=einstein_s_equations|lang=zh-CN|style=Feynman)最奇特的解之一：哥德尔宇宙。这是一个旋转的宇宙，[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的结构被扭曲得如此厉害，以至于允许[时间旅行](@keyword=time_travel|lang=zh-CN|style=Feynman)回到过去！然而，即使在这个令人困惑的舞台上，我们也可以探究其对称性。如果我们考虑沿其一个空间轴的简单“推动”——由[矢量场](@keyword=vector_field|lang=zh-CN|style=Feynman) $X = \partial_z$ 表示——并计算其度规的[李导数](@keyword=lie_derivatives|lang=zh-CN|style=Feynman)，我们发现结果为零 [@problem_id:1018728]。这意味着，尽管它有着令人晕眩的旋转和因果关系的奇异性，这个宇宙仍然拥有一个简单的平移对称性。[李导数](@keyword=lie_derivatives|lang=zh-CN|style=Feynman)在看似混沌中找到了秩序。

### 形变的物理学

所以，李导数为零意味着对称性。但当它*不*为零时呢？在很多方面，这甚至更有趣。一个非零的结果 $\mathcal{L}_X g \neq 0$ 并不是失败，而是一种测量。它给了我们一个新的张量场，精确地量化了空间几何是如何被流拉伸和剪切的。它是一部空间本身形变的电影。

这个想法在**[连续介质力学](@keyword=continuum_mechanics|lang=zh-CN|style=Feynman)**领域，特别是在流体研究中，找到了一个惊人而实用的应用。想象一条河流在流动。设每一点水的速度由一个[矢量场](@keyword=vector_field|lang=zh-CN|style=Feynman) $\mathbf{v}$ 描述。现在，想象一滴微小的球形染料悬浮在水中。随着水流，水流可能会将这滴染料拉伸成一个[椭球体](@keyword=ellipsoid|lang=zh-CN|style=Feynman)、扭曲它或压缩它。我们如何用数学来描述这种形变？

你可能已经猜到了。度规[张量](@keyword=tensor|lang=zh-CN|style=Feynman)关于[速度场](@keyword=velocity_field|lang=zh-CN|style=Feynman)的[李导数](@keyword=lie_derivatives|lang=zh-CN|style=Feynman) $\mathcal{L}_{\mathbf{v}} g$ 恰好告诉了我们这一点。事实上，它等于两倍的**[应变率张量](@keyword=rate_of_strain_tensor|lang=zh-CN|style=Feynman)**，这是[流体动力学](@keyword=hydrodynamics|lang=zh-CN|style=Feynman)中的一个基本量，描述了流体单元形变的速率 [@problem_id:655276]。其分量由这个优美的表达式给出：

$$
(\mathcal{L}_{\mathbf{v}} g)_{ij} = \nabla_i v_j + \nabla_j v_i
$$

突然之间，我们的抽象几何工具正在描述一个非常物理的过程。它将空间的几何（$g$）与运动的运动学（$\mathbf{v}$）联系起来。这个[张量](@keyword=tensor|lang=zh-CN|style=Feynman)决定了像蜂蜜或油这样的流体中的粘性力。所以，下次你看到奶油在咖啡中旋转时，你可以想象，在每一点上，都有一个微小的[李导数](@keyword=lie_derivatives|lang=zh-CN|style=Feynman)正在被计算，描述着由流体承载的空间度规是如何被流所变形的。无论是描述宇宙的对称性还是茶杯中的水流，这都是同样的数学。

### 曲率、守恒与宇宙

李导数的[影响范围](@keyword=range_of_influence|lang=zh-CN|style=Feynman)甚至更广，直达现代物理学的核心：**广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)**。爱因斯坦教会我们，引力不是一种力，而是[时空](@keyword=space_time|lang=zh-CN|style=Feynman)弯曲的表现。这种弯曲由[张量](@keyword=tensor|lang=zh-CN|style=Feynman)来描述，如里奇张量 $\mathrm{Ric}$ 和[标量曲率](@keyword=scalar_curvature|lang=zh-CN|style=Feynman) $R$。

当我们对这些[曲率张量](@keyword=curvature_tensor|lang=zh-CN|style=Feynman)取李导数时会发生什么？我们发现了物理学中最深刻的联系之一。事实证明，空间的对称性往往是其中物理学的对称性。对于一个像完美球面那样的[常曲率空间](@keyword=spaces_of_constant_curvature|lang=zh-CN|style=Feynman)，[里奇张量](@keyword=ricci_tensor|lang=zh-CN|style=Feynman)只是度规的倍数，$R_{ij} \propto g_{ij}$。由此便如白昼接替黑夜般简单地推断出，如果一个[基灵矢量场](@keyword=killing_vector_fields|lang=zh-CN|style=Feynman) $K$ 使度规保持不变（$\mathcal{L}_K g = 0$），那么它也必然使[里奇张量](@keyword=ricci_tensor|lang=zh-CN|style=Feynman)保持不变（$\mathcal{L}_K R_{ij} = 0$）[@problem_id:537561]。容器的对称性就是其所含之物的对称性。

这个原理，即李导数“尊重”其作用对象的结构，是一个普遍的原理 [@problem_id:1852254]。但它最深刻的推论，通过诺特定理，是对称性与**[守恒律](@keyword=conservation_laws|lang=zh-CN|style=Feynman)**之间的联系。在广义[相对论](@keyword=relativity|lang=zh-CN|style=Feynman)中，如果一个[时空](@keyword=space_time|lang=zh-CN|style=Feynman)拥有一个[基灵矢量](@keyword=killing_vectors|lang=zh-CN|style=Feynman)，那么一个自由穿行于该[时空](@keyword=space_time|lang=zh-CN|style=Feynman)的粒子在其路径上将有一个相应的守恒量。

*   如果一个[时空](@keyword=space_time|lang=zh-CN|style=Feynman)是**时间平移不变**的（它有一个指向时间方向的[基灵矢量场](@keyword=killing_vector_fields|lang=zh-CN|style=Feynman)），那么**能量**是守恒的。
*   如果它是**[空间平移](@keyword=spatial_translation|lang=zh-CN|style=Feynman)不变**的（它有一个指向空间方向的[基灵矢量场](@keyword=killing_vector_fields|lang=zh-CN|style=Feynman)），那么该方向上的线性**动量**是守恒的。
*   如果它是**旋转不变**的，那么**角动量**是守恒的。

李导数是解开这种对应关系的关键。通过找到那些使 $\mathcal{L}_X g = 0$ 的[矢量场](@keyword=vector_field|lang=zh-CN|style=Feynman) $X$，我们正在直接识别支配该宇宙中物理学的[守恒量](@keyword=conserved_quantity|lang=zh-CN|style=Feynman)。另一方面，如果我们发现[李导数](@keyword=lie_derivatives|lang=zh-CN|style=Feynman)非零，就像在一些我们可以研究的假设[时空](@keyword=space_time|lang=zh-CN|style=Feynman)中那样 [@problem_id:909589] [@problem_id:1490471]，那我们就是在证明相应守恒律的*不存在*。

这段旅程带领我们从简单的旋转到流体的漩涡，再到宇宙宏大的守恒律。在每一步中，[李导数](@keyword=lie_derivatives|lang=zh-CN|style=Feynman)都作为我们的向导，提供了一种单一、统一的语言来描述变化与永恒。它向我们展示了支撑[晶体对称性](@keyword=crystal_symmetry|lang=zh-CN|style=Feynman)、河流流动和宇宙演化的数学思想都是密切相关的。而且，对于真正好奇的人来说，这仅仅是个开始。李导数是一个更宏伟结构的基石，在这个结构中，物理定律本身被理解为[不变性](@keyword=invariance|lang=zh-CN|style=Feynman)的陈述——那是另一个有待讲述的故事了 [@problem_id:2998464]。