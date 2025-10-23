## 引言
当一个物体变形时，我们如何描述它的运动？对于书架的轻微下垂，简单的线性模型就足够了。但在拉伸的橡皮筋、揉皱的汽车车身和跳动的心脏的世界里，这些近似方法就失效了。我们进入了[有限变形](@article_id:351218)的领域，在这里，形状和方向的变化是巨大的、复杂的和非线性的。核心挑战是发展一种一致的数学语言，能够准确地捕捉这种运动的几何学，区分真实应变与简单旋转，并解释体积和形状的显著变化。本文为这个强大的框架提供了一个全面的介绍。第一章“原理与机制”将从基础开始构建理论，介绍变形梯度、客观[应变张量](@article_id:372284)和运动的极分解等基本概念。随后，“应用与跨学科联系”一章将展示这些原理对于解决软[材料力学](@article_id:380563)、[计算工程学](@article_id:357053)和[力学生物学](@article_id:306670)等不同领域的实际问题是何等关键。

## 原理与机制

想象一下你手里拿着一根橡皮筋。你拉它，它变长变细。你扭它，它扭曲变形。我们究竟如何能用物理学优美的精确性来描述这种巨大的、橡胶般的变形呢？我们不可能追踪每一个原子；那将是一项不可能完成的任务。我们需要一种更聪明、更优雅的方式来捕捉运动的本质。寻找这种描述方法的旅程是一个精彩的故事，它讲述了数学如何为物理世界提供一种完美的语言。

本章是关于我们为此目的发明的工具。我们暂时不会讨论所涉及的力——那是后话。在这里，我们纯粹关注*[运动学](@article_id:323309)*，即运动本身的几何学。当物体发生大幅度运动时，我们如何测量拉伸、剪切和旋转？

### 局部放大镜：变形梯度

让我们先想象一下我们变形前的橡皮筋。我们可以想象在这个初始的、舒适的状态下有一组“物[质点](@article_id:365946)”，我们称之为**参考构型**。我们可以用每个点的起始[位置矢量](@article_id:353860)来标记它，我们称之为$\boldsymbol{X}$。现在，我们使橡皮筋变形。每一个点$\boldsymbol{X}$都移动到空间中的一个新位置$\boldsymbol{x}$，这被称为**当前构型**。整个变形就是这样一个映射：对于每一个原始点$\boldsymbol{X}$，现在都有一个新点$\boldsymbol{x}$。

这个全局的图景很不错，但它并没有告诉我们材料*内部*发生了什么——拉伸和扭曲。要看到这一点，我们需要将材料的一个小邻域置于一个数学放大镜下。让我们看一个点$\boldsymbol{X}$和从它指向一个邻近点的微小无穷小矢量$d\boldsymbol{X}$。变形后，这两个点移动到了$\boldsymbol{x}$和$\boldsymbol{x} + d\boldsymbol{x}$。问题是，新的小矢量$d\boldsymbol{x}$与旧的$d\boldsymbol{X}$有什么关系？

对于一个平滑的变形，如果我们放大得足够近，复杂的弯曲和扭曲在局部看起来就像一个简单的[线性变换](@article_id:376365)。也就是说，新矢量只是旧矢量的一个线性函数。我们可以将这种关系写成：

$$
d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}
$$

这个矩阵（或者更正式地说，[二阶张量](@article_id:366843)）$\boldsymbol{F}$是我们这场秀的主角。它被称为**变形梯度**。毫不夸张地说，它就是最终位置矢量$\boldsymbol{x}$相对于初始位置矢量$\boldsymbol{X}$的梯度。你可以把它看作是变形的局部说明书。在每个点上，$\boldsymbol{F}$都准确地告诉你从该点发出的所有无穷小矢量是如何被拉伸和旋转的。它将局部邻域从参考构型映射到当前构型。[@problem_id:2558953]

然而，并非任何矩阵$\boldsymbol{F}$都能代表物理变形。我们必须坚持一些常识性规则。首先，我们不能让原始橡皮筋中的两个不同点最终落在同一个位置——物质不能自我穿透。我们也不能凭空制造撕裂或孔洞。这意味着从$\boldsymbol{X}$到$\boldsymbol{x}$的映射必须是连续且[一一对应](@article_id:304365)的，数学家称之为[同胚](@article_id:307350)。其次，也是至关重要的一点，一个无穷小体积元$dV_0$不能被压缩到零体积，或者更糟的是，被“里外翻转”。新[体积元](@article_id:331505)$dV$与旧体积元$dV_0$之比由$\boldsymbol{F}$的[行列式](@article_id:303413)给出，我们称之为**雅可比行列式**，$J = \det \boldsymbol{F}$。因此，对于任何固体的物理变形，其基本约束是在任何地方都有$J > 0$。[@problem_id:2558916]

### 测量真正重要的东西：应变

现在我们有了$\boldsymbol{F}$，这是变形的完整局部描述。但它是一个好的*应变*度量吗？应变应当是关于拉伸和畸变，而不仅仅是任何运动。想象一下，你拿一根钢梁，只是简单地旋转它。每个点都在移动。变形梯度$\boldsymbol{F}$将是一个旋转矩阵，而不是[单位矩阵](@article_id:317130)。但是这根梁被应变了吗？当然没有。一个好的应变度量必须对[刚体转动](@article_id:332325)“视而不见”。[@problem_id:2886632]

我们如何创造出这样一种度量呢？让我们回到我们的小矢量$d\boldsymbol{X}$。刚性旋转不改变其长度。所以，一个真正的变形度量应该与矢量的*长度变化*有关。我们原始矢量的长度平方是$dS^2 = d\boldsymbol{X} \cdot d\boldsymbol{X}$。我们新矢量的长度平方是$ds^2 = d\boldsymbol{x} \cdot d\boldsymbol{x}$。

现在来看一段优美的代数推导。我们知道$d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$。让我们把它代入$ds^2$的表达式中：

$$
ds^2 = (\boldsymbol{F} d\boldsymbol{X}) \cdot (\boldsymbol{F} d\boldsymbol{X}) = (d\boldsymbol{X})^T \boldsymbol{F}^T \boldsymbol{F} (d\boldsymbol{X})
$$

看！长度平方的变化取决于组合$\boldsymbol{F}^T\boldsymbol{F}$。让我们给这个重要的对象起个名字：它是**右柯西-格林变形[张量](@article_id:321604)**，$\boldsymbol{C} = \boldsymbol{F}^T\boldsymbol{F}$。这个[张量](@article_id:321604)非常棒。让我们看看如果变形只是一个纯旋转，即$\boldsymbol{F} = \boldsymbol{R}$，其中$\boldsymbol{R}$是一个旋转矩阵，会发生什么。由于旋转矩阵具有$\boldsymbol{R}^T\boldsymbol{R} = \boldsymbol{I}$（[单位矩阵](@article_id:317130)）的性质，我们发现$\boldsymbol{C} = \boldsymbol{I}$。如果$\boldsymbol{C} = \boldsymbol{I}$，那么$ds^2 = (d\boldsymbol{X})^T \boldsymbol{I} (d\boldsymbol{X}) = dS^2$。长度没有改变！所以，$\boldsymbol{C}$成功地忽略了刚性旋转，只告诉我们关于拉伸的信息。

如果根本没有变形，$\boldsymbol{F}=\boldsymbol{I}$，因此$\boldsymbol{C}=\boldsymbol{I}$。所以，$\boldsymbol{C}$与单位矩阵的差异是应变的纯粹度量。这引导我们定义**[Green-Lagrange应变张量](@article_id:366888)**：

$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I}) = \frac{1}{2}(\boldsymbol{F}^T\boldsymbol{F} - \boldsymbol{I})
$$

这个对象$\boldsymbol{E}$当且仅当变形是[刚体运动](@article_id:329499)时为零。它完美地分离了运动中的拉伸和剪切部分。任何无穷小矢量的长度平方变化可以用$\boldsymbol{E}$优雅地表示：

$$
ds^2 - dS^2 = 2 (d\boldsymbol{X})^T \boldsymbol{E} (d\boldsymbol{X})
$$

这个方程意义深远。它告诉我们，一旦我们知道某一点上[对称张量](@article_id:308511)$\boldsymbol{E}$的六个独立分量，我们就知道了穿过该点的*每一条线元*的长度平方是如何变化的。它是纯变形的一个完整的局部度量。[@problem_id:2558953]

### 分解运动：[拉伸与旋转](@article_id:310616)

我们可以将变形与旋转分开的想法是如此强大，以至于它被载入力学中一个优美的定理，称为**[极分解](@article_id:375742)**。它指出，任何变形梯度$\boldsymbol{F}$都可以唯一地分解为两部分：一个纯拉伸，然后是一个刚性旋转。我们写成：

$$
\boldsymbol{F} = \boldsymbol{R} \boldsymbol{U}
$$

这里，$\boldsymbol{U}$是一个[对称张量](@article_id:308511)，称为**右[拉伸张量](@article_id:372157)**，而$\boldsymbol{R}$是一个[旋转张量](@article_id:370993)。$\boldsymbol{U}$处理所有的拉伸，然后$\boldsymbol{R}$将结果旋转到其最终方向。奇妙之处在于$\boldsymbol{U}$与我们的朋友$\boldsymbol{C}$直接相关：它就是$\boldsymbol{C}$的平方根，$\boldsymbol{U} = \sqrt{\boldsymbol{C}}$。

一个简单的例子可以清楚地说明这一点。考虑一个方块沿$X_1$轴被拉伸到其长度的$\lambda$倍，并沿$X_2$轴被压缩到$1/\lambda$。变形梯度是一个简单的[对角矩阵](@article_id:642074)。事实证明，这个矩阵本身就是对称的，代表了纯拉伸，所以在这种情况下，$\boldsymbol{U}=\boldsymbol{F}$，旋转$\boldsymbol{R}$只是[单位矩阵](@article_id:317130)。[@problem_id:2558945] 然而，如果我们进行相同的拉伸，然后旋转物体，$\boldsymbol{F}$会变成一个更复杂的[非对称矩阵](@article_id:313666)。但是当我们计算$\boldsymbol{C} = \boldsymbol{F}^T\boldsymbol{F}$时，旋转部分奇迹般地消失了，只留下一个仅包含纯拉伸信息的[张量](@article_id:321604)。[@problem_id:2886632]

[拉伸张量](@article_id:372157)$\boldsymbol{U}$的[特征值](@article_id:315305)具有直接的物理意义：它们是**[主拉伸](@article_id:373569)**，通常表示为$\lambda_1, \lambda_2, \lambda_3$。这三个数字告诉你沿着三个特殊的、初始相互垂直方向（主方向）的拉伸比。它们代表了对变形最纯粹的描述，完全剥离了任何旋转信息。它们是真正的“应变”。[@problem_id:2681400] 关联力与变形的材料[本构定律](@article_id:357811)，通常最自然地用这些[主拉伸](@article_id:373569)或其[不变量](@article_id:309269)来表示。[@problem_id:2666927]

### 通往现实的桥梁：小应变与大错误

我们中许多人初次学习应变是在一个简化的“小应变”世界里。那个熟悉的图景如何与这个更通用、更强大的[有限变形理论](@article_id:381645)联系起来？让我们用[位移场](@article_id:301917)$\boldsymbol{u} = \boldsymbol{x} - \boldsymbol{X}$来表示我们的应变张量$\boldsymbol{E}$。位移的梯度是$\boldsymbol{H} = \nabla_{\boldsymbol{X}}\boldsymbol{u}$，经过一些代数运算可以得到$\boldsymbol{F} = \boldsymbol{I} + \boldsymbol{H}$。将此代入$\boldsymbol{E}$的公式，得到一个非凡的结果：

$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{H} + \boldsymbol{H}^T) + \frac{1}{2}\boldsymbol{H}^T\boldsymbol{H}
$$

第一项，$\boldsymbol{\varepsilon} = \frac{1}{2}(\boldsymbol{H} + \boldsymbol{H}^T)$，正是你可能从入门课程中记得的**[线性化](@article_id:331373)应变张量**！第二项，$\frac{1}{2}\boldsymbol{H}^T\boldsymbol{H}$，是一个纯粹的非线性项，是[位移梯度](@article_id:344697)的二次项。[@problem_id:2558935]

所以，熟悉的小应变理论只是真实的、几何精确理论的一个*近似*。它是你假装非线性项不存在时得到的理论。为了使这个近似有效，[位移梯度](@article_id:344697)$\boldsymbol{H}$的所有分量都必须远小于1。多小才算小？考虑一个简单的[剪切变形](@article_id:350092)，一个正方形的顶部被横向滑动。真实应变$\boldsymbol{E}$和[线性化](@article_id:331373)应变$\boldsymbol{\varepsilon}$之间的差异正是这个非线性项。对于一个小的剪切，比如$\kappa=0.2$，误差很小，约为$0.02$。但对于一个大的剪切$\kappa=1$，误差变得相当大，约为$0.5$，这显示了线性化理论如何迅速失效。[@problem_id:2558928]

这个非线性项的重要性无论如何强调都不为过。正是这一项保证了我们的应变度量对于大的刚体旋转为零。线性化应变$\boldsymbol{\varepsilon}$未能通过这一关键测试；它会错误地预测一个只被旋转的物体中的应变（以及应力！）。$\frac{1}{2}\boldsymbol{H}^T\boldsymbol{H}$这一项是修正这个问题的英雄。[@problem_id:2558935]

这仅仅是数学上的迂腐吗？绝对不是。对大变形问题使用小应变理论是灾难的根源。想象一下模拟一个在重载下变形的流体饱和土。理论必须跟踪体积的变化（$J$）以了解有多少流体被挤出。小应变理论，就其本质而言，假设$J \approx 1$。它完全错过了主要事件！这导致违反了基本的[质量守恒定律](@article_id:307792)，产生了完全虚假和非物理的压力预测。[金属塑性](@article_id:355551)也是如此，其中$\boldsymbol{F}$分解为弹性和塑性部分的[乘法分解](@article_id:378267)对于获得正确的物理现象至关重要。[@problem_id:2701386] [@problem_id:2673828]

[有限变形运动学](@article_id:374704)的原理不仅仅是一项学术练习。它们是现代工程的基石，使我们能够精确地模拟从汽车安全气囊的充气、涡轮叶片的锻造到人类心脏的跳动等一切事物。它们为理解一个变形世界的几何学提供了一个优美一致且物理上稳健的框架。