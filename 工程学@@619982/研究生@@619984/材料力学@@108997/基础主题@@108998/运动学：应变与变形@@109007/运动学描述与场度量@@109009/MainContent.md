## 引言
在连续介质力学中，精确描述一个物体——无论是一块黏土、一根钢梁还是活体组织——如何从一种形状变为另一种形状，是理解其力学行为的基石。这不仅仅是追踪几个点的轨迹，而是需要一个能够捕捉整个连续体变形几何本质的严谨数学框架。然而，我们如何系统地量化这种复杂的“流动”，将拉伸、剪切和旋转等直观概念转化为精确的数学语言呢？

本文旨在系统地回答这一问题。我们将带领读者深入探索运动学描述，这门只关注变形几何、不考虑作用力的学科。通过本文，你将学习到如何使用变形梯度[张量](@article_id:321604)来解码局部变形的全部信息，理解应变的不同度量方式，并掌握将复杂变形分解为纯拉伸和刚性旋转的强大工具。文章将从最基本的概念出发，逐步构建起一个完整而自洽的理论体系。

我们的旅程，将从定义运动本身以及描述它的核心工具开始。

## 核心概念

想象一下，我们想描述一块黏土被揉捏、拉伸和扭曲的过程。我们如何用数学的语言，精确地捕捉这种从一种形状到另一种形状的“流动”？这不仅仅是跟踪几个点，而是要理解整个连续体的每一点是如何运动和变形的。这便是[运动学](@article_id:323309)描述的核心任务，它是我们进入[连续介质力学](@article_id:315536)世界的基石。它不关心力的大小或材料的种类，只专注于一件事：几何。

### 运动：一场从过去到现在的旅行

首先，我们需要一个“地图”。这个地图告诉我们，材料在初始状态（我们称之为**参考构型**，$\mathcal{B}_0$）中的每一个点 $\mathbf{X}$，在时刻 $t$ 会跑到空间中的哪个位置 $\mathbf{x}$（即**当前构型**，$\mathcal{B}_t$）。这个映射，我们称之为**运动**，写作 $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$。

这听起来很简单，但一个“物理上可能”的运动必须遵守两条基本法则，这源于物质世界的常识。首先，物质不能自己穿过自己。这意味着两个不同的物质点 $\mathbf{X}_1$ 和 $\mathbf{X}_2$ 在任何时刻都不能占据同一个空间位置。在数学上，这意味着映射 $\boldsymbol{\chi}$ 必须是**单射**的（injective）。一个试图将方块像折纸一样对折的运动，就会导致不同部分的物质重叠，这在物理上是不允许的 [@problem_id:2896781]。其次，一个物质微元在变形后，其“手性”或朝向不应该发生翻转。想象一下，你不可能把自己的左手手套变成右手手套而不把它翻过来。这个特性由一个叫做**变形梯度**（我们马上会讲到）的[张量](@article_id:321604)的[行列式](@article_id:303413) $J$ 来保证，它必须大于零 ($J>0$)。一个 $J0$ 的运动，就像是把物体变成了它在镜子里的像，这在连续的变形中是无法实现的 [@problem_id:2896781]。

### 变形的DNA：变形梯度 $\mathbf{F}$

现在，让我们请出我们故事中的主角：**变形梯度[张量](@article_id:321604)** $\mathbf{F}$。如果你想理解变形的所有秘密，$\mathbf{F}$ 就是那把钥匙。它的定义是运动函数对参考坐标的梯度：$\mathbf{F} = \nabla_{\mathbf{X}} \boldsymbol{\chi}$。

$\mathbf{F}$ 的魔力在于，它是一个**局部**的线性映射。它告诉我们，在参考构型中一个点 $\mathbf{X}$ 附近的一个无穷小矢量 $d\mathbf{X}$，在当前构型中会变成哪个矢量 $d\mathbf{x}$。它们的关系异常简洁：$d\mathbf{x} = \mathbf{F} d\mathbf{X}$ [@problem_id:2896807]。你可以把 $\mathbf{F}$ 想象成一个随位置和时间变化的“局部放大镜”，它不仅会缩放矢量，还会旋转和剪切它。

$\mathbf{F}$ 的作用远不止于此。它掌握着所有几何变形的信息：

-   **体积变化**：$\mathbf{F}$ 的[行列式](@article_id:303413) $J = \det(\mathbf{F})$，也称为[雅可比行列式](@article_id:365483)，给出了局部的体积变化率。一个微小的参考[体积元](@article_id:331505) $dV$ 经过变形后，其新的体积 $dv$ 满足 $dv = J dV$。如果 $J=1$，变形是保体积的；如果 $J>1$，[体积膨胀](@article_id:304671)；如果 $0  J  1$，[体积收缩](@article_id:326324)。如果我们考虑一个密度为 $\rho_0$ 的物体，根据质量守恒定律 $dm = \rho_0 dV = \rho dv$，我们可以立刻得到当前密度与参考密度的关系：$\rho = \rho_0 / J$ [@problem_id:2896792]。

-   **面积变化**：一个微小的[有向面积](@article_id:348805)元 $d\mathbf{A} = \mathbf{N} dA$ 在变形后会变成 $d\mathbf{a} = \mathbf{n} da$。它们之间的关系由著名的**[南森公式](@article_id:374449)（Nanson’s relation）**给出：$\mathbf{n} da = J \mathbf{F}^{-T} \mathbf{N} dA$ [@problem_id:2896807]。这在计算流体流过[曲面](@article_id:331153)或计算接触面上的力时至关重要。

### 剖析变形：[拉伸与旋转](@article_id:310616)

任何一个局部的变形，无论看起来多么复杂，本质上都可以分解为两个更简单的动作：纯粹的**拉伸**（stretching）和纯粹的**旋转**（rotation）。这就像你可以把任意一个[线性变换](@article_id:376365)分解为一个对称变换和一个[旋转变换](@article_id:378757)一样。这个美妙的数学事实被称为**极分解定理（Polar Decomposition Theorem）** [@problem_id:2896796]。

它告诉我们，变形梯度 $\mathbf{F}$ 可以唯一地分解为：
$\mathbf{F} = \mathbf{R}\mathbf{U}$ 或 $\mathbf{F} = \mathbf{V}\mathbf{R}$

这里：
-   $\mathbf{R}$ 是一个[旋转张量](@article_id:370993)（一个[行列式](@article_id:303413)为+1的正交[张量](@article_id:321604)）。它描述了物质微元经历的刚性旋转。
-   $\mathbf{U}$ 是**右[拉伸张量](@article_id:372157)**，它是一个对称[正定张量](@article_id:383010)。它作用在参考构型上，描述了在旋转**之前**发生的纯粹拉伸和剪切。
-   $\mathbf{V}$ 是**左[拉伸张量](@article_id:372157)**，也是一个对称[正定张量](@article_id:383010)。它作用在当前构型上，描述了旋转**之后**我们所看到的拉伸状态。

$\mathbf{U}$ 和 $\mathbf{V}$ 的[特征值](@article_id:315305)是相同的，被称为**[主拉伸](@article_id:373569)**，它们代表了相互垂直的三个方向上的最大、最小和中间拉伸率。它们的[特征向量](@article_id:312227)则指出了这些[主拉伸](@article_id:373569)的方向。

那么，我们如何从 $\mathbf{F}$ 中“提炼”出 $\mathbf{U}$ 和 $\mathbf{R}$ 呢？诀窍在于构造一个聪明的量，它只包含拉伸信息。这就是**右柯西-格林（Cauchy-Green）变形[张量](@article_id:321604)** $\mathbf{C} = \mathbf{F}^T\mathbf{F}$。代入 $\mathbf{F} = \mathbf{R}\mathbf{U}$，我们得到 $\mathbf{C} = (\mathbf{R}\mathbf{U})^T(\mathbf{R}\mathbf{U}) = \mathbf{U}^T\mathbf{R}^T\mathbf{R}\mathbf{U} = \mathbf{U}^T\mathbf{U} = \mathbf{U}^2$。看！旋转 $\mathbf{R}$ 被巧妙地消去了。由于 $\mathbf{U}$ 是唯一的对称正定平方根，我们可以通过计算 $\mathbf{C}$ 的平方根来得到 $\mathbf{U} = \sqrt{\mathbf{C}}$。一旦有了 $\mathbf{U}$，旋转也就迎刃而解：$\mathbf{R} = \mathbf{F}\mathbf{U}^{-1}$ [@problem_id:2896796]。

### 应变：如何量化“拉伸了多少”？

我们已经分离出了拉伸，但如何量化它呢？这就引出了**应变（strain）**的概念。但是，这里有一个哲学问题：我们应该站在哪个角度来衡量应变？

想象一下拉伸一根橡皮筋。我们可以：
1.  **从过去看现在（[拉格朗日](@article_id:373322)视角）**：我们站在未变形的参考构型中，比较变形后的长度与原始长度的差异。我们的测量工具是[右柯西-格林张量](@article_id:353212) $\mathbf{C}$。一个微元 $d\mathbf{X}$ 的原始长度平方是 $d\mathbf{X} \cdot d\mathbf{X}$，变形后的长度平方是 $d\mathbf{x} \cdot d\mathbf{x} = ( \mathbf{F} d\mathbf{X} ) \cdot ( \mathbf{F} d\mathbf{X} ) = d\mathbf{X} \cdot (\mathbf{C} d\mathbf{X})$ [@problem_id:2896806]。长度平方的改变就是 $d\mathbf{X} \cdot (\mathbf{C} - \mathbf{I}) d\mathbf{X}$。这启发我们定义**格林-[拉格朗日](@article_id:373322)（Green-Lagrange）[应变张量](@article_id:372284)**：
    $\mathbf{E} = \frac{1}{2}(\mathbf{C}-\mathbf{I})$
    它是一个**物质**量，因为它是在参考构型中定义的。

2.  **从现在看过去（[欧拉视角](@article_id:328994)）**：我们站在已经变形的当前构型中，思考一个微元 $d\mathbf{x}$ 在变形前应该有多长。我们的测量工具是**[左柯西-格林张量](@article_id:365366)（或称Finger[张量](@article_id:321604)）** $\mathbf{B} = \mathbf{F}\mathbf{F}^T$ 的逆 $\mathbf{B}^{-1}$。原始长度平方可以表示为 $d\mathbf{X} \cdot d\mathbf{X} = (\mathbf{F}^{-1} d\mathbf{x}) \cdot (\mathbf{F}^{-1} d\mathbf{x}) = d\mathbf{x} \cdot (\mathbf{B}^{-1}d\mathbf{x})$ [@problem_id:2896806]。长度平方的改变同样可以从当前构型来看。这启发我们定义**欧拉-阿尔曼西（Euler-Almansi）应变张量**：
    $\mathbf{e} = \frac{1}{2}(\mathbf{I}-\mathbf{B}^{-1})$
    它是一个**空间**量，因为它是在当前构型中定义的 [@problem_id:2896798]。

$\mathbf{E}$ 和 $\mathbf{e}$ 就像是从不同角度拍摄的同一物体的两张照片，它们通过 $\mathbf{F}$ 相互关联 ($\mathbf{E} = \mathbf{F}^T \mathbf{e} \mathbf{F}$)。最美妙的是，当变形非常小（$\mathbf{F}$ 接近单位[张量](@article_id:321604) $\mathbf{I}$）时，这两个看起来截然不同的应变张量会趋于同一个形式——我们在线性弹性理论中熟悉的**小应变张量** $\boldsymbol{\varepsilon}$ [@problem_id:2896798]。这揭示了物理理论内在的和谐与统一。

### 物质的流动：变化率的艺术

到目前为止，我们都在看变形的“快照”。但力学是关于运动和变化的，我们需要描述事物如何随[时间演化](@article_id:314355)。这里，拉格朗日和欧拉的两种视角再次出现。

-   **拉格朗日（物质）视角**：我们像一个随波逐流的软木塞，跟着一个特定的物质点 $\mathbf{X}$ 运动，记录它的物理量（如温度、速度）如何随时间变化。
-   **欧拉（空间）视角**：我们像一个固定在河岸上的观察者，测量流经该空间点 $\mathbf{x}$ 的水的不同物理量。

一个在空间点 $\mathbf{x}$ 的速度场 $\mathbf{v}(\mathbf{x}, t)$ 是一个[欧拉描述](@article_id:328429)。那么，一个物[质点](@article_id:365946)感受到的物理量（比如一个[标量场](@article_id:314722) $\phi(x,t)$）的变化率是多少呢？这不仅仅是场在空间定点的变化率 $\partial\phi/\partial t$，还包括了物[质点](@article_id:365946)运动到场值不同的新位置所带来的变化。这个总变化率被称为**物质导数（material derivative）**，记为 $D\phi/Dt$。根据[链式法则](@article_id:307837)，它等于：
$$ \frac{D\phi}{Dt} = \frac{\partial\phi}{\partial t} + \mathbf{v} \cdot (\nabla \phi) $$
这个公式优雅地连接了[欧拉视角](@article_id:328994)的局部变化率和[拉格朗日](@article_id:373322)视角的随体变化率 [@problem_id:2896812]。

正如 $\mathbf{F}$ 描述了变形的“状态”，[速度梯度](@article_id:325397) $\mathbf{L} = \nabla_{\mathbf{x}}\mathbf{v}$ 则描述了变形的“速率”。就像 $\mathbf{F}$ 可以分解为拉伸和旋转一样，$\mathbf{L}$ 也可以分解为一个对称部分和一个反对称部分：
$\mathbf{L} = \mathbf{D} + \mathbf{W}$

-   $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T)$ 是**变形率[张量](@article_id:321604)**，它描述了物质的拉伸和剪切的速率。它的迹 $\text{tr}(\mathbf{D}) = \nabla \cdot \mathbf{v}$ 代表了体积的膨胀率。如果 $\text{tr}(\mathbf{D}) = 0$，则运动是局部保体积的（不可压缩）[@problem_id:2896770]。
-   $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^T)$ 是**[自旋张量](@article_id:366504)（spin tensor）**，它描述了物质微元的瞬时刚性转动[角速度](@article_id:323935)，也与流体的涡量（vorticity）直接相关 [@problem_id:2896770]。

### 尾声：物理定律的游戏规则

这套描述运动和变形的数学框架不仅强大，其自身也必须遵循深刻的物理原则，就像任何游戏都有其规则一样。

第一个规则是**客观性（Objectivity）**，或称**[标架无关性](@article_id:376074)（Frame-Indifference）**。物理定律不应该依赖于观察者。如果一个观察者在旋转，他看到的物理现象本质上应该和静止的观察者一样。然而，简单的[物质导数](@article_id:369934)（如 $\dot{\boldsymbol{\sigma}}$）并不“客观”，它会因为观察者的旋转而改变。因此，为了建立普适的[本构关系](@article_id:323747)（连接力与变形的定律），物理学家们必须“发明”出**[客观应力率](@article_id:378041)**，如[Jaumann率](@article_id:364795)或[Green-Naghdi率](@article_id:369882)。这些“率”被巧妙地构造出来，以剔除观察者旋转带来的虚假变化，确保我们描述的是材料的真实响应 [@problem_id:2896809]。

第二个规则是**相容性（Compatibility）**。给定一个任意的光滑[对称张量](@article_id:308511)场 $\boldsymbol{\varepsilon}$，它是否总能代表一个真实的、连续的物体的应变场？答案是否定的。应变场不是可以随意杜撰的，它必须满足一定的[微分](@article_id:319122)约束条件，才能保证可以积分得到一个连续、单值的位移场 $\mathbf{u}$。这个条件被称为**圣维南（Saint-Venant）[相容性条件](@article_id:379809)**，其紧凑形式惊人地优雅：$\text{curl}(\text{curl}\,\boldsymbol{\varepsilon})^T = \mathbf{0}$ [@problem_id:2896773]。这就像一个内置的“完整性检查”，确保我们描述的几何变形在数学上是可能的。

从描述一个点的运动，到剖析变形的内在结构，再到思考描述变化率的普适规则，运动学为我们提供了一套完整而自洽的语言。它不仅仅是数学工具的堆砌，更是一次深入探索空间、时间和物质几何本质的壮丽旅程。