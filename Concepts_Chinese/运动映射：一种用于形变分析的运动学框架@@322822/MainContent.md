## 引言
我们宇宙中的一切，从恒星到活细胞，都处于不断运动和形变的状态。为了理解、预测和改造我们的世界，我们需要一种共同的语言来描述这些复杂的变化。这种通用语言存在于连续介质力学的数学中，其基石是**运动映射**的概念。该框架提供了一种严谨的方法来追踪一个物体如何随时间改变其在空间中的形状和位置。然而，描述这种变化带来了一个根本性的挑战：我们如何区分无害的刚体运动和可能导致失效的真实内部形变？我们又如何创建一种描述，无论我们是在固定的河岸上观察水流，还是在随波逐流的木筏上观察，这种描述都能保持有效？

本文全面概述了运动映射及其在科学和工程中的基础作用。我们首先在第一章“原理与机制”中解析其核心组成部分，其中我们将定义运动映射，探索强大的[形变梯度张量](@article_id:310788)，并揭示对旋转不敏感的“真实”应变测量的必要性。我们还将阐明用于描述物理现象的基本的[拉格朗日](@article_id:373322)和[欧拉视角](@article_id:328994)。随后，“应用与跨学科联系”一章将展示这种语言的非凡力量，演示它如何被用于确保工程中的结构安全，揭示物理学中的统一原理，甚至在生物学中解码生命过程本身。

## 原理与机制

想象你手里拿着一块透明柔软的明胶。你决定要绘制它的行为，于是在其中注入微小的、发光的尘埃颗粒，并给每个颗粒一个永久且独特的名牌——我们称这些名牌为 $\boldsymbol{X}$。所有可能名牌的集合，对应着未拉伸明胶块中的每一个点，构成了物理学家所说的**参考构型**，即 $\mathcal{B}_0$。这是物体的原始、未形变状态。现在，你挤压并扭转这块明胶。这些发光的尘埃移动到了空间中的新位置，我们称之为 $\boldsymbol{x}$。一个带有 $\boldsymbol{X}$ 名牌的尘埃现在位于位置 $\boldsymbol{x}$。[运动学](@article_id:323309)的宏伟任务就是描述这种关系：对于任意给定的尘埃 $\boldsymbol{X}$ 和任意时间 $t$，它现在在哪里？这种关系就是**运动映射**，一个我们记作 $\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X}, t)$ 的函数。[@problem_id:2607098] [@problem_id:2705825] 这个映射是我们用来描述任何物体形变的基础语言，无论是承受载荷的桥梁还是旋转的星系。

### 形变的局部字典

运动映射 $\boldsymbol{\chi}(\boldsymbol{X}, t)$ 告诉我们全局的故事，但我们通常感兴趣的是在单一点的无穷小邻域内局部发生的情况。想象两个尘埃，$\boldsymbol{X}$ 和它的一个邻居 $\boldsymbol{X} + d\boldsymbol{X}$，它们在参考块中由一个微小的矢量 $d\boldsymbol{X}$ 分隔。形变后，它们移动到 $\boldsymbol{x}$ 和 $\boldsymbol{x} + d\boldsymbol{x}$。新的连接矢量 $d\boldsymbol{x}$ 与旧的 $d\boldsymbol{X}$ 有何关系？对于一个平滑的形变，这种关系将是线性的，意味着它可以用矩阵乘法来描述。这个矩阵就是著名的**[形变梯度](@article_id:343158)**，用 $\boldsymbol{F}$ 表示。

$$
d\boldsymbol{x} = \boldsymbol{F} \, d\boldsymbol{X}
$$

[形变梯度](@article_id:343158)定义为运动映射对参考坐标的梯度：$\boldsymbol{F} = \frac{\partial \boldsymbol{\chi}}{\partial \boldsymbol{X}}$。[@problem_id:2624225] 它像一本局部字典，将无穷小矢量从参考语言翻译成当前的形变语言。它被称为**两点[张量](@article_id:321604)**，因为它的“输入”存在于参考构型中，而其“输出”则存在于当前的空间构型中。[@problem_id:2896807] 这个单一的[张量](@article_id:321604)包含了所有关于拉伸、剪切和旋转的局部信息。例如，在工程中使用[有限元法](@article_id:297335)进行的模拟中，物体的复杂、连续的运动是通过对几个关键点（节点）的位置进行插值来近似的。然后，每个小单元内的[形变梯度](@article_id:343158) $\boldsymbol{F}$ 就可以直接根据这些节点的位置和[插值函数](@article_id:326499)（称为[形函数](@article_id:301457)）的属性来计算。[@problem_id:2635686]

### 可能性的物理学

虽然数学允许函数做任何事，但物理学施加了规则。一个物理物体的两个点不能同时占据同一个位置——这是不可入性原理。这意味着我们的运动映射 $\boldsymbol{\chi}$ 必须是**一对一**的。此外，我们不能让明胶块的一部分“里外翻转”。这对应于对[形变梯度](@article_id:343158)的一个条件：它的[行列式](@article_id:303413)，称为**雅可比行列式**，记作 $J = \det \boldsymbol{F}$，必须为正。[@problem_id:2558916]

雅可比行列式有一个非常简洁的物理意义：它是局部体积变化的比率。如果我们在参考块中取一个无穷小体积元 $dV$，它在形变状态下的体积将是 $dv = J \, dV$。[@problem_id:2896807] 对于像水（或者近似地，我们的明胶）这样的[不可压缩材料](@article_id:354959)，$J$ 必须处处等于 $1$。对于像气体这样的可压缩材料，$J$ 可以变化，材料模型通常会包含一个对 $J$ 偏离 $1$ 的能量惩罚项，以表示压缩或膨胀材料所需的功。[@problem_id:2624225] 面积元也以一种精确的方式变换，遵循一个称为 Nanson 关系式的规则，该规则同时涉及 $J$ 和 $\boldsymbol{F}$。[@problem_id:2896807]

### 寻求“真实”应变

我们的目标是测量形变。但什么是形变？如果我们拿起明胶块，仅仅移动或旋转它，它的形状并没有改变。一个好的应变测量必须足够聪明，能够忽略这种[刚体运动](@article_id:329499)，只捕捉拉伸和剪切。

一个初步的、直观的尝试是对非常小的形变有效的**[无穷小应变张量](@article_id:346500)**，$\boldsymbol{\epsilon}_{ij} = \frac{1}{2}\left(\frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i}\right)$，其中 $\boldsymbol{u}$ 是位移场 $\boldsymbol{u} = \boldsymbol{x} - \boldsymbol{X}$。这个[张量](@article_id:321604)就是[位移梯度](@article_id:344697)的对称部分。[@problem_id:2601644] 对于微小的摆动和[振动](@article_id:331484)，它工作得非常好。

但是，让我们通过一个思想实验来检验这个直觉。如果我们让物体经历一个大的、有限的旋转，但完全没有拉伸呢？这显然是一个刚体运动。我们的[无穷小应变张量](@article_id:346500)会给出零吗？令人惊讶的答案是：不会！如果你为一个有限旋转计算 $\boldsymbol{\epsilon}$ 的分量，你会发现它们通常不为零。[@problem_id:1551738] 我们的直观应变测量失败了！它被一个纯粹的旋转所欺骗，以为存在应变。这个美妙的悖论表明，对于大形变的世界，我们需要一个更复杂的工具。

答案在于回到[形变梯度](@article_id:343158) $\boldsymbol{F}$。让我们考虑无穷小矢量 $d\boldsymbol{X}$ 的*长度平方*的变化。它原始的长度平方是 $d\boldsymbol{X} \cdot d\boldsymbol{X}$。它新的长度平方是 $d\boldsymbol{x} \cdot d\boldsymbol{x} = (\boldsymbol{F} \, d\boldsymbol{X}) \cdot (\boldsymbol{F} \, d\boldsymbol{X}) = d\boldsymbol{X} \cdot (\boldsymbol{F}^{\mathsf T}\boldsymbol{F}) \, d\boldsymbol{X}$。几何形状的变化完全由[张量](@article_id:321604) $\boldsymbol{C} = \boldsymbol{F}^{\mathsf T}\boldsymbol{F}$ 捕捉，该[张量](@article_id:321604)被称为**[右 Cauchy-Green 形变张量](@article_id:351851)**。由此，我们定义**Green-Lagrange [应变张量](@article_id:372284)**为：

$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I}) = \frac{1}{2}(\boldsymbol{F}^{\mathsf T}\boldsymbol{F} - \boldsymbol{I})
$$

现在，让我们来检验这个新的测量方法。如果我们有一个纯粹的刚体旋转，[形变梯度](@article_id:343158) $\boldsymbol{F}$ 就是[旋转矩阵](@article_id:300745) $\boldsymbol{R}$。由于旋转矩阵是正交的，$\boldsymbol{R}^{\mathsf T}\boldsymbol{R} = \boldsymbol{I}$。将此代入我们的公式得到 $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{I}) = \boldsymbol{0}$。成功了！对于任何刚体旋转，无论多大，Green-Lagrange 应变都精确为零。[@problem_id:2558937] 它完美地分离出了纯形变。[极分解](@article_id:375742)定理在数学上证实了这一点，该定理指出任何[形变梯度](@article_id:343158)都可以唯一地分解为一个旋转和一个纯拉伸（$\boldsymbol{F}=\boldsymbol{R}\boldsymbol{U}$）：$\boldsymbol{C}$ 仅取决于拉伸部分 $\boldsymbol{U}$（$\boldsymbol{C}=\boldsymbol{U}^2$），使其对旋转 $\boldsymbol{R}$ 不敏感。[@problem_id:2624225]

### 两种观察方式：河流与木筏

我们如何描述像速度或温度这样的场，取决于我们的视角。在连续介质力学中有两种经典的观点。

第一种是**[拉格朗日描述](@article_id:328205)**。这就像身处顺流而下的木筏上。你附着于一组特定的水分子（一个物[质点](@article_id:365946) $\boldsymbol{X}$），并且你总是从你的木筏的视角来描述一切——你的速度、水温——它们都是时间的函数。所有属性都是 $(\boldsymbol{X}, t)$ 的函数。这是我们用来定义运动映射的观点，也是许多计算方法中使用的**全拉格朗日列式法**的基础。这种方法之所以强大，是因为它将整个问题建立在固定的、不变的参考构型 $\mathcal{B}_0$ 上，这简化了计算，因为积分域永远不会改变。[@problem_id:2705825] [@problem_id:2607098]

第二种是**[欧拉描述](@article_id:328429)**。这就像站在河岸上观察水流。你测量在给定时间 $t$ 恰好经过空间中一个固定点 $\boldsymbol{x}$ 的水的速度和温度。所有属性都是 $(\boldsymbol{x}, t)$ 的函数。这是[流体动力学](@article_id:319275)的自然视角。

这两种观点必须是一致的。木筏的速度（[拉格朗日](@article_id:373322)速度）就是其位置对时间的[导数](@article_id:318324)：$\boldsymbol{V}(\boldsymbol{X},t) = \frac{\partial \boldsymbol{\chi}}{\partial t}(\boldsymbol{X}, t)$。在河岸上测量的速度（欧拉速度，$\boldsymbol{v}(\boldsymbol{x},t)$）是那一刻恰好处在点 $\boldsymbol{x}$ 的任何木筏的速度。[@problem_id:2659098]

这引出了物理学中最重要的概念之一：**物质导数**。想象你在木筏上，水温正在变化。你随时间感觉到的变化，$\frac{D\theta}{Dt}$，是由两种效应引起的：首先，你经过的固定点的温度本身可能在变化（上游的一个温泉开始涌出），这是局部时间[导数](@article_id:318324) $\frac{\partial \theta}{\partial t}$。其次，随着你漂流，你正在进入一个可能具有不同温度的区域，这是[对流](@article_id:302247)项 $\boldsymbol{v} \cdot \nabla\theta$。将它们合在一起，就得到了著名的关系式：

$$
\frac{D\theta}{Dt} = \frac{\partial \theta}{\partial t} + \boldsymbol{v} \cdot \nabla \theta
$$

这个公式是连接两个世界的桥梁。它告诉我们一个粒子所经历的变化率与该场在空间和时间上的变化有何关系。要正确定义[欧拉视角](@article_id:328994)下的加速度，必须使用这个[导数](@article_id:318324)，因为加速度是速度的[物质导数](@article_id:369934)。[@problem_id:2659098] [@problem_id:2896779] 使用这个统一的框架，我们可以推导出深刻的关系，例如体积变化率如何与速度场的散度相关：$\dot{J} = J (\nabla \cdot \boldsymbol{v})$。[@problem_id:2896779] 从一个追踪点的简单想法出发，我们已经建立了一个完整而强大的数学结构，能够描述形变物质丰富而复杂的舞蹈。