## 引言
在连续介质力学中，准确描述物体的变形方式是一项基本挑战，尤其是当变形较大时。对于形状几乎不发生变化的材料，入门概念通常已足够，但当面对橡胶的极端拉伸、流体的流动或[金属成形](@article_id:367683)中的复杂过程时，这些概念便不再适用。这种局限性催生了对更稳健框架的需求，该框架承认一个关键的视角选择：我们是跟随材料[质点](@article_id:365946)一同运动，还是从固定位置观察流动？本文将探讨后一种观点，即[欧拉描述](@article_id:328429)，并通过其主要数学工具——[欧拉-阿尔曼西应变张量](@article_id:373844)进行阐述。在接下来的章节中，我们将首先揭示定义这种空间应变度量的基本“原理与机制”，并将其与基于物质的对应物——格林-拉格朗日[张量](@article_id:321604)进行对比。随后，我们将探讨其在“应用与跨学科联系”中的重要作用，展示为何欧拉-阿尔曼西视角不仅是一种备选方案，更是现代物理学和工程学（从[流体动力学](@article_id:319275)到先进计算模拟）中不可或缺的语言。

## 原理与机制

想象一下，您正在尝试描述一条河流的流动。您有两种选择。您可以坐上一只小筏，跟随一滴水顺流而下，细致地记录其路径和速度。这是**[拉格朗日](@article_id:373322)**视角，以 Joseph-Louis Lagrange 的名字命名。或者，您可以站在一座桥上的固定位置，观察流经您身边的水的属性——其速度、其深度。这是**欧拉**视角，以 Leonhard Euler 的名字命名。

在[材料科学](@article_id:312640)领域，当一个物体变形时——气球充气、金属棒被拉伸、一块面团被揉捏——我们面临同样的选择。我们可以从物体未变形时的初始位置追踪单个材料[质点](@article_id:365946)（拉格朗
日视角），或者我们可以将注意力固定在空间中的点上，描述当前占据这些点的材料发生了什么（[欧拉视角](@article_id:328994)）。**[欧拉-阿尔曼西应变张量](@article_id:373844)**正是这第二种[欧拉视角](@article_id:328994)的主要工具。这是物理学家站在桥上描述固体“流动”的方式。

### 两种观察世界：参考构型的选择

当固体变形时，其内部质点之间的距离会发生变化。“应变”的本质就是量化这种变化。但这种变化是相对于什么而言的？这是一个至关重要的问题。

**[格林-拉格朗日应变张量](@article_id:366888)**，我们称之为 $\boldsymbol{E}$，采用的是拉格朗日视角。它将变形后物体的几何形状与*原始、未变形的物体*的几何形状进行比较。这就像一位历史学家回顾旧地图来描述城市布局的变化。它回答了这样一个问题：“对于任意两个最初由微小向量 $\mathrm{d}\boldsymbol{X}$ 分隔的[质点](@article_id:365946)，它们之间距离的平方发生了怎样的变化？”

**[欧拉-阿尔曼西应变张量](@article_id:373844)**，即本文的主角，记作 $\boldsymbol{e}$，则采取欧拉立场。它从*当前已变形的物体*的视角量化同样的几何变化。这就像一位测量员在测量今天的城市并试图推断其原始布局。它回答了这样一个问题：“对于任意两个当前由微小向量 $\mathrm{d}\boldsymbol{x}$ 分隔的质点，它们之间的距离平方与最初相比发生了怎样的变化？”[@problem_id:2657136]。

这种视角的差异不仅仅是个人偏好问题，而是根本性的。格林-拉格朗日[张量](@article_id:321604) $\boldsymbol{E}$ 是一个**物质**量，意味着它定义在每个材料质点上，您可以将其视为初始坐标 $\boldsymbol{X}$ 的函数。欧拉-阿尔曼西[张量](@article_id:321604) $\boldsymbol{e}$ 是一个**空间**量，定义在当前被材料占据的每个空间点 $\boldsymbol{x}$ 上。

### 应变的定义：长度平方的变化

我们如何将这些思想用数学语言来表达？关键的洞见在于观察连接两个质点的微小[线元](@article_id:324062)*长度的平方*的变化，这构成了所有[有限应变理论](@article_id:355900)的基石。假设初始长度的平方为 $\mathrm{d}L^2 = \mathrm{d}\boldsymbol{X} \cdot \mathrm{d}\boldsymbol{X}$，最终的、即当前的长度平方为 $\mathrm{d}\ell^2 = \mathrm{d}\boldsymbol{x} \cdot \mathrm{d}\boldsymbol{x}$。

[格林-拉格朗日应变](@article_id:349620) $\boldsymbol{E}$ 的定义旨在从物质视角捕捉这一变化：
$$
\mathrm{d}\ell^2 - \mathrm{d}L^2 = 2\, \mathrm{d}\boldsymbol{X} \cdot (\boldsymbol{E}\, \mathrm{d}\boldsymbol{X})
$$
这个方程告诉我们，$\boldsymbol{E}$ 就像一台机器，输入一对初始[线元](@article_id:324062) $\mathrm{d}\boldsymbol{X}$，就能输出长度平方的变化。通过数学推导，可以得到其著名的定义，该定义涉及**变形梯度** $\boldsymbol{F}$（将初始向量映射到最终向量的[张量](@article_id:321604)，$\mathrm{d}\boldsymbol{x} = \boldsymbol{F} \mathrm{d}\boldsymbol{X}$）和**[右柯西-格林张量](@article_id:353212)** $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$：
$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})
$$
这里，$\boldsymbol{I}$ 是单位[张量](@article_id:321604)。[张量](@article_id:321604) $\boldsymbol{C}$ [实质](@article_id:309825)上衡量了空间度规在物质构型中是如何被拉伸和剪切的。如果没有变形，则 $\boldsymbol{F}=\boldsymbol{I}$，因此 $\boldsymbol{C}=\boldsymbol{I}$ 且 $\boldsymbol{E}=\boldsymbol{0}$，这与预期相符。

[欧拉-阿尔曼西应变](@article_id:366270) $\boldsymbol{e}$ 的定义旨在捕捉完全相同的[不变量](@article_id:309269)变化，但却是从空间视角出发 [@problem_id:2648740]：
$$
\mathrm{d}\ell^2 - \mathrm{d}L^2 = 2\, \mathrm{d}\boldsymbol{x} \cdot (\boldsymbol{e}\, \mathrm{d}\boldsymbol{x})
$$
请注意其中微妙而深刻的差别：我们现在使用当前的[线元](@article_id:324062) $\mathrm{d}\boldsymbol{x}$作为我们的参照。为了得到 $\boldsymbol{e}$ 的公式，我们必须用当前的几何量来表示初始长度 $\mathrm{d}L^2$。这涉及到逆变形梯度，$\mathrm{d}\boldsymbol{X} = \boldsymbol{F}^{-1} \mathrm{d}\boldsymbol{x}$。由此可以得到 $\boldsymbol{e}$ 以**[左柯西-格林张量](@article_id:365366)** $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\mathsf{T}}$ 表示的定义：
$$
\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{B}^{-1})
$$
这个定义非常直观 [@problem_id:2640421]。它表明，当前构型中的应变 $\boldsymbol{e}$ 是当前度规（由 $\boldsymbol{I}$ 表示）与*前推*到当前构型中的初始构型度规（由 $\boldsymbol{B}^{-1}$ 表示）之间的比较。如果没有变形，$\boldsymbol{B}=\boldsymbol{I}$，同样 $\boldsymbol{e}=\boldsymbol{0}$。

### 拉伸带的故事：格林-拉格朗日与[欧拉-[阿尔曼西应](@article_id:366270)变](@article_id:370173)的实际应用

我们来让这个概念更具体一些。考虑一根初始长度为 $L_0$ 的橡皮筋被拉伸到新长度 $L$。**伸长率**为 $\lambda = L/L_0$。我们的两种应变度量如何描述这个简单情况？

对于这种单轴情况，通过定义推导可以得到两个看起来截然不同的公式 [@problem_id:2708309]：
- 主[格林-拉格朗日应变](@article_id:349620)：$E = \frac{1}{2}(\lambda^2 - 1)$
- 主[欧拉-阿尔曼西应变](@article_id:366270)：$e = \frac{1}{2}(1 - \lambda^{-2})$

假设我们将橡皮筋拉伸到其原始长度的两倍，即 $\lambda = 2$。
[格林-拉格朗日应变](@article_id:349620)为 $E = \frac{1}{2}(2^2 - 1) = 1.5$。
[欧拉-阿尔曼西应变](@article_id:366270)为 $e = \frac{1}{2}(1 - 2^{-2}) = \frac{1}{2}(1 - 0.25) = 0.375$。
这两个数字截然不同！这不是矛盾，而是它们不同参考构型的结果。$\boldsymbol{E}$ 是相对于较短的初始长度来度量应变的，因此它给出了一个较大的数值。$\boldsymbol{e}$ 是相对于较长的最终长度来度量应变的，因此它给出了一个较小的数值。

如果我们将其压缩到一半长度，即 $\lambda = 0.5$ 呢？
[格林-拉格朗日应变](@article_id:349620)为 $E = \frac{1}{2}(0.5^2 - 1) = -0.375$。
[欧拉-阿尔曼西应变](@article_id:366270)为 $e = \frac{1}{2}(1 - 0.5^{-2}) = \frac{1}{2}(1 - 4) = -1.5$。
现在情况反过来了！$\boldsymbol{E}$ 的[绝对值](@article_id:308102)较小，因为它参考的是较长的初始长度，而 $\boldsymbol{e}$ 的[绝对值](@article_id:308102)较大，因为它参考的是较短的最终长度。描述方式的选择至关重要。

### 当两个世界交汇：小应变近似

但是等等。在大多数工程应用中，我们使用简单的“工程应变”，即 $\varepsilon_{\text{eng}} = \lambda-1$。这又如何与上述理论相符？在这里我们看到了物理学的统一性。更复杂的理论必须在适当的极限下简化为更简单且成功的理论。这里的极限就是**小应变**，即变形非常微小，所以 $\lambda$ 非常接近 1。

我们令 $\lambda = 1 + \varepsilon$，其中 $\varepsilon$ 是一个非常小的数。让我们使用[泰勒级数展开](@article_id:298916) $E$ 和 $e$ 的公式，保留到 $\varepsilon = \lambda - 1$ 的二阶项 [@problem_id:2886611]：
- [格林-拉格朗日应变](@article_id:349620)：$E = \frac{1}{2}((1+\varepsilon)^2 - 1) = \frac{1}{2}(1 + 2\varepsilon + \varepsilon^2 - 1) = \varepsilon + \frac{1}{2}\varepsilon^2$
- [欧拉-阿尔曼西应变](@article_id:366270)：$e = \frac{1}{2}(1 - (1+\varepsilon)^{-2}) \approx \frac{1}{2}(1 - (1 - 2\varepsilon + 3\varepsilon^2)) = \varepsilon - \frac{3}{2}\varepsilon^2$

看！在一阶近似下，$E$ 和 $e$ 都等于 $\varepsilon$，也就是工程应变！
$$
E \approx \varepsilon, \quad e \approx \varepsilon, \quad \text{for } |\varepsilon| \ll 1
$$
这是一个优美的结果 [@problem_id:2708309]。它表明，当变形很小时，参考构型的选择变得无关紧要。历史学家和测量员达成了一致。这就是为什么在建造桥梁或设计飞机机翼（希望它们变形不大！）时，简单的[线性化](@article_id:331373)应变就足够了。但对于像橡胶这样的软材料、生物组织或[金属成形](@article_id:367683)过程，二阶差异才能揭示真实情况。

### [客观性原理](@article_id:356369)：纯变形的度量

任何*应变*度量的一个基本要求是，它必须只测量*变形*——即拉伸和剪切——而不包括任何[刚体运动](@article_id:329499)。如果你拿起一个钢块，只是旋转它或将它移动到另一张桌子上，它并没有发生应变。一个在这种运动下会发生变化的应变度量将是无用的。这个关键属性被称为**客观性**或[标架无关性](@article_id:376074)。

格林-拉格朗日[张量](@article_id:321604)和欧拉-阿尔曼西[张量](@article_id:321604)都是客观的，这证明了它们的物理合理性。如果我们有一个纯刚体运动，其中 $\boldsymbol{F}$ 只是一个[旋转张量](@article_id:370993) $\boldsymbol{Q}$，那么 $\boldsymbol{C} = \boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q} = \boldsymbol{I}$ 且 $\boldsymbol{B} = \boldsymbol{Q}\boldsymbol{Q}^{\mathsf{T}} = \boldsymbol{I}$。将这些代入，我们得到 $\boldsymbol{E}=\boldsymbol{0}$ 和 $\boldsymbol{e}=\boldsymbol{0}$。它们都正确地报告了零应变，正如所要求的那样 [@problem_id:2922623]。

如果我们先使物体变形，*然后*在其上施加一个刚性旋转 $\boldsymbol{Q}$ 呢？新的变形梯度是 $\boldsymbol{\hat{F}} = \boldsymbol{Q}\boldsymbol{F}$。我们的[应变张量](@article_id:372284)会如何变化？
- 对于[格林-拉格朗日应变](@article_id:349620)，我们发现 $\boldsymbol{\hat{E}} = \boldsymbol{E}$。它完全保持不变！这非常合理：$\boldsymbol{E}$ 是一个物质[张量](@article_id:321604)，存在于参考构型中，不受我们在空间中对物体所做操作的影响。
- 对于[欧拉-阿尔曼西应变](@article_id:366270)，我们发现 $\boldsymbol{\hat{e}} = \boldsymbol{Q}\boldsymbol{e}\boldsymbol{Q}^{\mathsf{T}}$。[张量](@article_id:321604) $\boldsymbol{e}$ 本身不是[不变量](@article_id:309269)，但它的变换或“旋转”方式与变形后物体的任何物理属性完全一致。它附着在物体上，随之旋转。这正是客观[空间张量](@article_id:365009)正确的变换法则 [@problem_id:2922623] [@problem_id:2657136]。

### 更深层的结构与联系

拉格朗日世界和欧拉世界并非相互孤立。它们是同一物理现实的两种对偶视角，而变形梯度 $\boldsymbol{F}$ 就是在它们之间进行翻译的字典。例如，这两个应变张量通过 $\boldsymbol{F}$ 优雅地联系在一起 [@problem_id:2695241]。[欧拉-阿尔曼西应变](@article_id:366270)是[格林-拉格朗日应变](@article_id:349620)的**[前推](@article_id:319122)**：
$$
\boldsymbol{e} = \boldsymbol{F}^{-\mathsf{T}} \boldsymbol{E} \boldsymbol{F}^{-1}
$$
反之，$\boldsymbol{E}$ 则是 $\boldsymbol{e}$ 的**[拉回](@article_id:321220)**。这种关系确保了它们的一致性。

这种联系还要更深。**极分解**定理告诉我们，任何变形 $\boldsymbol{F}$ 都可以看作是一个拉伸后跟一个旋转。[欧拉-阿尔曼西应变](@article_id:366270) $\boldsymbol{e}$ 与**左伸长[张量](@article_id:321604)** $\boldsymbol{V}$ 密切相关，后者从空间角度描述了拉伸。它们之间的关系是一个简单而优美的表达式 [@problem_id:2681806]：
$$
\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{V}^{-2})
$$
应变张量的[主值](@article_id:368662)（[特征值](@article_id:315305)）代表了最大和最小应变，它们之间也直接相关。如果 $\epsilon$ 是 $\boldsymbol{E}$ 的一个主值，$\eta$ 是 $\boldsymbol{e}$ 对应的那个[主值](@article_id:368662)，它们通过一个简单的代数公式联系起来 [@problem_id:1551021]：
$$
\epsilon = \frac{\eta}{1 - 2\eta}
$$
这表明，尽管它们的定义看起来不同，但它们只是描述相同潜在物理拉伸的不同数学“语言”。

最后，有人可能会问：如果一个物体经历一次变形，然后再经历另一次，我们能简单地将应变相加吗？对于 $\boldsymbol{E}$ 和 $\boldsymbol{e}$，答案是响亮的“不” [@problem_id:2640405]。它们的定义是变形梯度的二次形式（它们涉及 $\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$ 或其逆）。这种非线性意味着，对于连续变形 $\boldsymbol{F} = \boldsymbol{F}_2 \boldsymbol{F}_1$，总应变不等于各部分应变之和。这看似一个缺陷，但实际上是大变形世界中几何学的一个基本特征。这也是为什么存在其他应变度量，如对数 Hencky 应变的原因——对于某些问题，特别是在塑性力学中，拥有一个可加的度量更为方便。

那么，[欧拉-阿尔曼西应变](@article_id:366270)就不仅仅是一个公式了。它是一个完整且一致的视角——桥上的观察者——用以理解我们物理世界中错综复杂的变形之舞。它提供了一种语言来描述材料*当下*的应变状态，这使得它在现代模拟和理论中不可或缺，因为在这些领域中，当前的应力状态取决于当前的应变状态。