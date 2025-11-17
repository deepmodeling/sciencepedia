## 引言
在微分几何的宏伟架构中，克里斯托弗符号 ($\Gamma^k_{ij}$) 是定义协变导数、描述[测地线](@entry_id:269969)以及最终构建曲率理论的基石。然而，一个初学者常常困惑的微妙之处在于：尽管它在张量方程中无处不在，克里斯托弗符号本身的分量却并不遵循张量的变换法则。这种坐标依赖性引出了一个核心问题：当我们在[流形](@entry_id:153038)上从一个[坐标系](@entry_id:156346)切换到另一个时，这些符号究竟如何变化？以及，这种看似“不完美”的变换行为背后隐藏着怎样的深刻几何与物理原理？

本文旨在系统地解答这些问题，深入剖析克里斯托弗符号的变换法则。我们将首先在 **“原则与机制”** 章节中，从联络的第一性原理出发，一步步推导出完整的变换公式，并精确分析其非张量性的来源与表现。接着，在 **“应用与跨学科联系”** 章节，我们将展示这一定律的强大威力，探讨它如何在平直空间的[曲线坐标系](@entry_id:172561)中产生“虚拟”的[引力](@entry_id:175476)效应，如何在广义相对论中奠定[等效原理](@entry_id:157518)的数学基础，以及它如何确保物理定律的[协变](@entry_id:634097)性。最后，通过 **“动手实践”** 部分，您将有机会通过具体的计算问题，将理论知识内化为解决实际问题的能力。通过这一学习路径，读者将深刻理解坐标不变性的本质，并掌握微分几何中最核心的计算工具之一。

## 原则与机制

在[微分几何](@entry_id:145818)中，协变导数的概念是核心，它使我们能够在弯曲的[流形](@entry_id:153038)上对张量场进行[微分](@entry_id:158718)。正如我们在前一章所见，协变导数的坐标表达式依赖于一组称为 **克里斯托弗符号 (Christoffel symbols)** 的系数，记作 $\Gamma^k_{ij}$。这些符号捕捉了[坐标基](@entry_id:270149)矢从一点到另一点的变化方式。然而，一个至关重要且微妙的要点是，克里斯托弗符号本身 **不是** 张量的分量。它们的数值依赖于所选的局部坐标系。本章的目标是深入探究克里斯托弗符号在[坐标变换](@entry_id:172727)下的行为，推导其变换法则，并揭示其深层的几何意义。理解这一法则对于掌握[黎曼几何](@entry_id:160508)中坐标[不变性](@entry_id:140168)的本质至关重要。

### 从第一性原理推导变换法则

让我们从联络的定义出发，直接推导克里斯托弗符号的变换法则。假设在一个光滑流形 $M$ 上给定一个[仿射联络](@entry_id:160152) $\nabla$。考虑两个交集非空的[坐标卡](@entry_id:262338) $(U,x)$ 和 $(V,y)$，其中 $x=(x^1, \dots, x^n)$ 和 $y=(y^1, \dots, y^n)$ 是[局部坐标](@entry_id:181200)。

在 $x$-[坐标系](@entry_id:156346)中，联络由克里斯托弗符号 $\Gamma^\alpha_{\beta\gamma}$ 定义，其满足：
$$
\nabla_{\frac{\partial}{\partial x^\beta}}\left(\frac{\partial}{\partial x^\gamma}\right) = \Gamma^\alpha_{\beta\gamma} \frac{\partial}{\partial x^\alpha}
$$

类似地，在 $y$-[坐标系](@entry_id:156346)中，联络由另一组符号 $\tilde{\Gamma}^k_{ij}$ 定义：
$$
\nabla_{\frac{\partial}{\partial y^i}}\left(\frac{\partial}{\partial y^j}\right) = \tilde{\Gamma}^k_{ij} \frac{\partial}{\partial y^k}
$$

我们的目标是找到在交集 $U \cap V$ 上 $\tilde{\Gamma}^k_{ij}$ 与 $\Gamma^\alpha_{\beta\gamma}$ 之间的关系。关键在于利用联络的性质和[链式法则](@entry_id:190743)来联系这两个定义。

首先，我们利用[链式法则](@entry_id:190743)将 $y$-[坐标系](@entry_id:156346)的[基矢](@entry_id:199546)用 $x$-[坐标系](@entry_id:156346)的[基矢](@entry_id:199546)表示：
$$
\frac{\partial}{\partial y^j} = \frac{\partial x^\beta}{\partial y^j} \frac{\partial}{\partial x^\beta}
$$
我们将这个表达式代入 $\tilde{\Gamma}^k_{ij}$ 的定义式左侧：
$$
\nabla_{\frac{\partial}{\partial y^i}}\left(\frac{\partial}{\partial y^j}\right) = \nabla_{\frac{\partial}{\partial y^i}}\left(\frac{\partial x^\beta}{\partial y^j} \frac{\partial}{\partial x^\beta}\right)
$$
由于联络 $\nabla$ 在其第一个参数上是 $C^\infty(M)$ 线性的，我们可以将[坐标变换](@entry_id:172727)的[雅可比矩阵](@entry_id:264467)分量 $\frac{\partial x^\alpha}{\partial y^i}$ 提出来（其中 $\frac{\partial}{\partial y^i} = \frac{\partial x^\alpha}{\partial y^i} \frac{\partial}{\partial x^\alpha}$）：
$$
\nabla_{\frac{\partial}{\partial y^i}}\left(\frac{\partial}{\partial y^j}\right) = \frac{\partial x^\alpha}{\partial y^i} \nabla_{\frac{\partial}{\partial x^\alpha}}\left(\frac{\partial x^\beta}{\partial y^j} \frac{\partial}{\partial x^\beta}\right)
$$
接下来，我们对第二个参数使用乘积法则（Leibniz 法则），即 $\nabla_X(fY) = (Xf)Y + f\nabla_X Y$。这里，$X = \frac{\partial}{\partial x^\alpha}$，$f = \frac{\partial x^\beta}{\partial y^j}$，$Y = \frac{\partial}{\partial x^\beta}$。
$$
\nabla_{\frac{\partial}{\partial x^\alpha}}\left(\frac{\partial x^\beta}{\partial y^j} \frac{\partial}{\partial x^\beta}\right) = \left(\frac{\partial}{\partial x^\alpha}\left(\frac{\partial x^\beta}{\partial y^j}\right)\right) \frac{\partial}{\partial x^\beta} + \frac{\partial x^\beta}{\partial y^j} \nabla_{\frac{\partial}{\partial x^\alpha}}\left(\frac{\partial}{\partial x^\beta}\right)
$$
将此结果代回并整理，我们得到：
$$
\nabla_{\frac{\partial}{\partial y^i}}\left(\frac{\partial}{\partial y^j}\right) = \frac{\partial x^\alpha}{\partial y^i} \frac{\partial^2 x^\beta}{\partial x^\alpha \partial y^j} \frac{\partial}{\partial x^\beta} + \frac{\partial x^\alpha}{\partial y^i} \frac{\partial x^\beta}{\partial y^j} \nabla_{\frac{\partial}{\partial x^\alpha}}\left(\frac{\partial}{\partial x^\beta}\right)
$$
应用[链式法则](@entry_id:190743) $\frac{\partial}{\partial y^i} = \frac{\partial x^\alpha}{\partial y^i} \frac{\partial}{\partial x^\alpha}$，第一项的[微分](@entry_id:158718)部分可以简化为 $\frac{\partial^2 x^\beta}{\partial y^i \partial y^j}$。对于第二项，我们使用 $\Gamma^\mu_{\alpha\beta}$ 的定义：
$$
\nabla_{\frac{\partial}{\partial y^i}}\left(\frac{\partial}{\partial y^j}\right) = \frac{\partial^2 x^\beta}{\partial y^i \partial y^j} \frac{\partial}{\partial x^\beta} + \frac{\partial x^\alpha}{\partial y^i} \frac{\partial x^\beta}{\partial y^j} \Gamma^\mu_{\alpha\beta} \frac{\partial}{\partial x^\mu}
$$
为了比较系数，我们必须将右侧的所有[基矢](@entry_id:199546)都转换到 $y$-[坐标基](@entry_id:270149)矢 $\frac{\partial}{\partial y^k}$。我们使用[逆变](@entry_id:192290)换 $\frac{\partial}{\partial x^\mu} = \frac{\partial y^k}{\partial x^\mu} \frac{\partial}{\partial y^k}$。将[哑指标](@entry_id:188070) $\beta$ 替换为 $\mu$ 以统一形式后，我们得到：
$$
\tilde{\Gamma}^k_{ij} \frac{\partial}{\partial y^k} = \left( \frac{\partial y^k}{\partial x^\mu} \frac{\partial x^\alpha}{\partial y^i} \frac{\partial x^\beta}{\partial y^j} \Gamma^\mu_{\alpha\beta} + \frac{\partial y^k}{\partial x^\mu} \frac{\partial^2 x^\mu}{\partial y^i \partial y^j} \right) \frac{\partial}{\partial y^k}
$$
通过比较两侧 $\frac{\partial}{\partial y^k}$ 的系数，我们最终得到了克里斯托弗符号的变换法则 [@problem_id:3005709] [@problem_id:3005741]：
$$
\tilde{\Gamma}^k_{ij} = \frac{\partial y^k}{\partial x^\mu} \frac{\partial x^\alpha}{\partial y^i} \frac{\partial x^\beta}{\partial y^j} \Gamma^\mu_{\alpha\beta} + \frac{\partial y^k}{\partial x^\mu} \frac{\partial^2 x^\mu}{\partial y^i \partial y^j}
$$
这个公式是微分几何中的一个基石。它精确地描述了克里斯托弗符号如何随着[坐标系](@entry_id:156346)的改变而改变。

### 克里斯托弗符号的非张量性

张量是一个几何对象，其分量在[坐标变换](@entry_id:172727)下遵循特定的、线性的、齐次的变换法则。为了理解克里斯托弗符号为何不是张量，我们首先回顾一下[向量和余向量](@entry_id:181128)（covector）的变换法则。

给定一个[坐标变换](@entry_id:172727) $x \mapsto x'$，其雅可比矩阵及其逆矩阵定义为：
$$
J^i{}_m := \frac{\partial x'^i}{\partial x^m}, \qquad K^m{}_i := \frac{\partial x^m}{\partial x'^i}
$$
它们满足 $J^i{}_m K^m{}_j = \delta^i{}_j$ [@problem_id:3005739]。一个[逆变向量](@entry_id:272483)（contravariant vector）$V$ 的分量变换法则为 $V'^i = J^i{}_m V^m$，而一个[协变向量](@entry_id:263917)（covariant vector，或[余向量](@entry_id:157727)）$W$ 的分量变换法则为 $W'_i = K^m{}_i W_m$ [@problem_id:3005723]。

一个 $(1,2)$ 型张量 $T$（一个上指标，两个下指标）的分量变换法则是上述规则的直接推广：
$$
\tilde{T}^k_{ij} = \frac{\partial y^k}{\partial x^\mu} \frac{\partial x^\alpha}{\partial y^i} \frac{\partial x^\beta}{\partial y^j} T^\mu_{\alpha\beta}
$$
现在，我们将这个[张量变换法则](@entry_id:185176)与我们推导出的克里斯托弗符号变换法则进行比较：
$$
\tilde{\Gamma}^k_{ij} = \underbrace{\frac{\partial y^k}{\partial x^\mu} \frac{\partial x^\alpha}{\partial y^i} \frac{\partial x^\beta}{\partial y^j} \Gamma^\mu_{\alpha\beta}}_{\text{齐次部分 (张量部分)}} + \underbrace{\frac{\partial y^k}{\partial x^\mu} \frac{\partial^2 x^\mu}{\partial y^i \partial y^j}}_{\text{非齐次部分}}
$$
很明显，克里斯托弗符号的变换法则包含一个额外的、非齐次的项。这个项 [@problem_id:1880432]
$$
I^k_{ij} = \frac{\partial y^k}{\partial x^\mu} \frac{\partial^2 x^\mu}{\partial y^i \partial y^j}
$$
依赖于坐标变换函数的[二阶导数](@entry_id:144508)。正是这个非齐次项的存在，使得克里斯托弗符号不满足张量的定义 [@problem_id:3005722]。

这种非张量行为有一个深刻的后果。如果一个张量的所有分量在某一点 $p$ 的一个[坐标系](@entry_id:156346)中都为零，那么它在任何其他[坐标系](@entry_id:156346)中在该点的分量也必定为零。然而，克里斯托弗符号并非如此。在[黎曼几何](@entry_id:160508)中，我们总可以在任意一点 $p$ 找到一个特殊的[坐标系](@entry_id:156346)，称为 **黎曼[法坐标](@entry_id:143194)系 (Riemannian normal coordinates)**，使得在该点 $p$ 的克里斯托弗符号全部为零，即 $\Gamma^k_{ij}(p) = 0$。现在，如果我们变换到一个任意的、[非线性](@entry_id:637147)的新[坐标系](@entry_id:156346) $y$，那么在该点的新符号将由变换法则给出：
$$
\tilde{\Gamma}^k_{ij}(p) = \left. \frac{\partial y^k}{\partial x^\mu} \frac{\partial^2 x^\mu}{\partial y^i \partial y^j} \right|_p
$$
这个值通常是非零的。这雄辩地证明了克里斯托弗符号是坐标依赖的，而不是一个内在的几何张量 [@problem_id:3005722]。

值得注意的是，只有当坐标变换是 **[仿射变换](@entry_id:144885)** 时（即 $\frac{\partial^2 x^\mu}{\partial y^i \partial y^j} = 0$），非齐次项才会消失。在这种特殊情况下，克里斯托弗符号的变换方式确实和张量一样 [@problem_id:3005722]。

### [不变性](@entry_id:140168)与替代引出

克里斯托弗符号的非[张量变换法则](@entry_id:185176)并非一个缺陷，而是确保更深层次[几何不变性](@entry_id:637068)的必要代价。我们可以从两个核心的物理与几何原理——协变导数的[不变性](@entry_id:140168)和测地线方程的[不变性](@entry_id:140168)——来反向推导出这个法则。

#### 协变导数的协变性

协变导数算符 $\nabla$ 本身是一个几何对象。将它作用于一个向量场 $V$ 会得到一个 $(1,1)$ 型张量场 $\nabla V$。这意味着 $\nabla V$ 的分量 $(\nabla V)^i_j = \nabla_j V^i$ 必须遵循 $(1,1)$ 型张量的变换法则。让我们从这个物理要求出发 [@problem_id:3005739]。

在 $x'$ [坐标系](@entry_id:156346)中，$(\nabla V)'^i_j = J^i_p K^q_j (\nabla V)^p_q$。使用[协变导数](@entry_id:152476)的坐标表达式 $\nabla_j V^i = \partial_j V^i + \Gamma^i_{jk} V^k$，我们展开上式两边：
$$
\partial'_j V'^i + \Gamma'^i_{jk} V'^k = J^i_p K^q_j (\partial_q V^p + \Gamma^p_{qr} V^r)
$$
通过代入 $V'^i = J^i_m V^m$ 并利用乘积法则和链式法则对左边的 $\partial'_j V'^i$ 进行展开，经过一系列代数运算，我们会发现，为了使该等式对任意向量场 $V$ 都成立，$\Gamma'^i_{jk}$ 与 $\Gamma^p_{qr}$ 之间必须满足的恰好就是我们之[前推](@entry_id:158718)导出的那个包含非齐次项的变换法则。

这个推导过程揭示了非齐次项的第一个重要角色：它是一个“修正项”，恰好抵消了普通导数 $\partial_j$ 在[坐标变换](@entry_id:172727)下的非张量行为，从而确保了整个[协变导数](@entry_id:152476) $\nabla_j$ 的变换行为是张量性的 [@problem_id:3005723]。

#### 测地线方程的不变性

[测地线](@entry_id:269969)是[流形](@entry_id:153038)上“最直”的路径，是广义相对论中自由下落物体的轨迹。一个参数为 $\lambda$ 的曲线 $x^i(\lambda)$ 是[测地线](@entry_id:269969)的条件是它满足[测地线方程](@entry_id:264349)：
$$
\frac{d^2 x^i}{d\lambda^2} + \Gamma^i_{jk} \frac{dx^j}{d\lambda} \frac{dx^k}{d\lambda} = 0
$$
一条曲线是否为[测地线](@entry_id:269969)，是一个不依赖于[坐标系](@entry_id:156346)的几何事实。因此，[测地线方程](@entry_id:264349)的形式必须在所有[坐标系](@entry_id:156346)下保持不变 [@problem_id:3005700]。

让我们来验证这一点。考虑一个坐标变换 $x \mapsto x'$。我们计算新坐标下的加速度项 $\frac{d^2 x'^i}{d\lambda^2}$。通过两次应用链式法则：
$$
\frac{dx'^i}{d\lambda} = \frac{\partial x'^i}{\partial x^a} \frac{dx^a}{d\lambda}
$$
$$
\frac{d^2 x'^i}{d\lambda^2} = \frac{d}{d\lambda}\left(\frac{\partial x'^i}{\partial x^a}\right) \frac{dx^a}{d\lambda} + \frac{\partial x'^i}{\partial x^a} \frac{d^2 x^a}{d\lambda^2} = \frac{\partial^2 x'^i}{\partial x^a \partial x^b} \frac{dx^a}{d\lambda} \frac{dx^b}{d\lambda} + \frac{\partial x'^i}{\partial x^a} \frac{d^2 x^a}{d\lambda^2}
$$
现在，我们将原[坐标系](@entry_id:156346)中的测地线方程 $\frac{d^2 x^a}{d\lambda^2} = -\Gamma^a_{bc} \frac{dx^b}{d\lambda} \frac{dx^c}{d\lambda}$ 代入上式：
$$
\frac{d^2 x'^i}{d\lambda^2} = \frac{\partial^2 x'^i}{\partial x^a \partial x^b} \frac{dx^a}{d\lambda} \frac{dx^b}{d\lambda} - \frac{\partial x'^i}{\partial x^a} \Gamma^a_{bc} \frac{dx^b}{d\lambda} \frac{dx^c}{d\lambda}
$$
为了让它具有测地线方程的形式 $\frac{d^2 x'^i}{d\lambda^2} = -\Gamma'^i_{jk} \frac{dx'^j}{d\lambda} \frac{dx'^k}{d\lambda}$，我们必须将右边的速度项 $\frac{dx}{d\lambda}$ 换成 $\frac{dx'}{d\lambda}$。最终，我们发现 $\Gamma'^i_{jk}$ 必须通过我们之[前推](@entry_id:158718)导的变换法则与 $\Gamma^a_{bc}$ 相关联。

这个推导从另一个角度揭示了非齐次项的几何意义：它精确地补偿了由于[坐标系](@entry_id:156346)自身的“弯曲”或[非线性](@entry_id:637147)而对曲线加速度产生的表观效应。正是这个修正项，保证了[测地线](@entry_id:269969)这个内在的几何概念在任何[坐标系](@entry_id:156346)下都具有相同的数学形式 [@problem_id:3005700]。

### 一个具体例子：欧氏平面中的极坐标

为了更具体地理解这一点，让我们看一个简单的例子：平坦的二维[欧氏空间](@entry_id:138052) $\mathbb{R}^2$ [@problem_id:2968175]。

在标准的[笛卡尔坐标系](@entry_id:169789) $(x^1, x^2) = (x, y)$ 中，空间是平直的，[基矢](@entry_id:199546) $\frac{\partial}{\partial x}$ 和 $\frac{\partial}{\partial y}$ 在任何地方都指向相同的方向。因此，相应的列维-奇维塔联络的克里斯托弗符号全部为零：$\Gamma^k_{ij} = 0$。

现在，我们切换到极[坐标系](@entry_id:156346) $(\tilde{x}^1, \tilde{x}^2) = (r, \theta)$。这是一个[非线性](@entry_id:637147)坐标变换：
$$
x = r\cos\theta, \qquad y = r\sin\theta
$$
由于原[坐标系](@entry_id:156346)中的 $\Gamma^k_{ij}$ 为零，新[坐标系](@entry_id:156346)中的克里斯托弗符号 $\tilde{\Gamma}^m_{ab}$ 将完全由变换法则中的非齐次项给出：
$$
\tilde{\Gamma}^m_{ab} = \frac{\partial \tilde{x}^m}{\partial x^k} \frac{\partial^2 x^k}{\partial \tilde{x}^a \partial \tilde{x}^b}
$$
其中求和约定作用于重复指标 $k=1, 2$。让我们计算其中一个分量，例如 $\tilde{\Gamma}^r_{\theta\theta}$（即 $m=r, a=\theta, b=\theta$）：
$$
\tilde{\Gamma}^r_{\theta\theta} = \frac{\partial r}{\partial x} \frac{\partial^2 x}{\partial \theta^2} + \frac{\partial r}{\partial y} \frac{\partial^2 y}{\partial \theta^2}
$$
我们需要一些[偏导数](@entry_id:146280)：
$$
\frac{\partial x}{\partial \theta} = -r\sin\theta \implies \frac{\partial^2 x}{\partial \theta^2} = -r\cos\theta
$$
$$
\frac{\partial y}{\partial \theta} = r\cos\theta \implies \frac{\partial^2 y}{\partial \theta^2} = -r\sin\theta
$$
以及 $r = \sqrt{x^2+y^2}$ 的导数：
$$
\frac{\partial r}{\partial x} = \frac{x}{\sqrt{x^2+y^2}} = \frac{r\cos\theta}{r} = \cos\theta
$$
$$
\frac{\partial r}{\partial y} = \frac{y}{\sqrt{x^2+y^2}} = \frac{r\sin\theta}{r} = \sin\theta
$$
代入计算 $\tilde{\Gamma}^r_{\theta\theta}$：
$$
\tilde{\Gamma}^r_{\theta\theta} = (\cos\theta)(-r\cos\theta) + (\sin\theta)(-r\sin\theta) = -r(\cos^2\theta + \sin^2\theta) = -r
$$
例如，在点 $(r, \theta) = (3, \pi/3)$ 处，该分量的值为 $-3$ [@problem_id:2968175]。

这个例子生动地说明：即使在固有的平坦空间中，仅仅因为我们使用了“弯曲”的[坐标系](@entry_id:156346)（极坐标），也会导致克里斯托弗符号非零。这里的 $\tilde{\Gamma}^r_{\theta\theta}=-r$ 并不代表空间本身是弯曲的（我们知道它不是），而是反映了极坐标的[基矢](@entry_id:199546) $\frac{\partial}{\partial r}$ 和 $\frac{\partial}{\partial \theta}$ 的方向和大小随着位置的变化而变化。

### 高等几何诠释

我们可以从更抽象和现代的几何视角来理解克里斯托弗符号的变换法则。

#### [正则性条件](@entry_id:166962)

我们推导中自由地使用了[二阶导数](@entry_id:144508)，这隐含了[对流](@entry_id:141806)形和度量的光滑性要求。为了让克里斯托弗符号及其变换法则是良定义的（至少是连续的），我们需要满足一定的 **[正则性条件](@entry_id:166962) (regularity conditions)** [@problem_id:3005708]。

1.  **度量的正则性**：列维-奇维塔联络的克里斯托弗符号是通过度量张量 $g_{ij}$ 的[一阶导数](@entry_id:749425)定义的：$\Gamma^k_{ij} = \frac{1}{2}g^{kl}(\partial_i g_{lj} + \partial_j g_{il} - \partial_l g_{ij})$。为了使这些[一阶导数](@entry_id:749425)存在且连续，度量张量的分量 $g_{ij}$ 至少需要是 $C^1$ 类（一阶连续可导）。

2.  **图卡的正则性**：克里斯托弗符号的变换法则包含坐标变换函数的[二阶导数](@entry_id:144508)项 $\frac{\partial^2 x^\mu}{\partial y^i \partial y^j}$。为了使这一项存在且连续，[坐标变换](@entry_id:172727)函数 $x(y)$ 必须至少是 $C^2$ 类（二阶连续可导）。这意味着定义[流形](@entry_id:153038)的图册（atlas）必须是 $C^2$ 类的。

综上，要使克里斯托弗符号及其变换法则在整个[流形](@entry_id:153038)上都有良好定义，我们通常要求[流形](@entry_id:153038)的图册至少是 $C^2$ 类，而[黎曼度量](@entry_id:754359)至少是 $C^1$ 类。

#### 联络的[仿射空间](@entry_id:152906)与2-射流

克里斯托弗符号变换法则的[代数结构](@entry_id:137052)揭示了一个深刻的几何事实：[流形](@entry_id:153038)上所有线性联络的集合构成一个 **[仿射空间](@entry_id:152906) (affine space)**，其关联的[向量空间](@entry_id:151108)是 $(1,2)$ 型[张量场](@entry_id:190170)的空间 [@problem_id:3005696]。这意味着，给定两个不同的联络 $\nabla$ 和 $\hat{\nabla}$，它们的克里斯托弗符号之差 $A^k_{ij} = \Gamma^k_{ij} - \hat{\Gamma}^k_{ij}$ 会表现为一个真正的 $(1,2)$ 型张量。这是因为在[坐标变换](@entry_id:172727)下，$\Gamma$ 和 $\hat{\Gamma}$ 的非齐次项是完全相同的（因为它只依赖于坐标变换本身），所以在相减时被消除了。

变换法则还可以用 **射流 (jet)** 的语言来优雅地描述。一个映射在一点的 $k$-阶射流 ($k$-jet) 是该映射在该点的[泰勒展开](@entry_id:145057)到 $k$ 阶的[等价类](@entry_id:156032)。[坐标变换](@entry_id:172727) $y(x)$ 在一点 $p$ 的 **2-阶射流 (2-jet)** 就包含了它在该点的[一阶导数](@entry_id:749425)（[雅可比矩阵](@entry_id:264467) $J$）和[二阶导数](@entry_id:144508)（Hessian相关项）。

克里斯托弗符号的变换法则，实际上是[流形](@entry_id:153038)上所有[局部微分同胚](@entry_id:203529)的2-射流群 $J^2_p(\text{Diff}(M))$ 在该点所有可能[坐标系](@entry_id:156346)下的克里斯托弗符号集合上的一个 **仿射作用 (affine action)**。这个作用可以写成：
$$
(A,B) \cdot \Gamma: \quad \tilde{\Gamma} = \text{Ad}_A(\Gamma) + \Psi(A,B)
$$
其中，$A$ 代表[一阶导数](@entry_id:749425)部分（雅可比矩阵），$B$ 代表[二阶导数](@entry_id:144508)部分。$\text{Ad}_A(\Gamma)$ 是由 $A$ 诱导的线性“张量部分”变换，而 $\Psi(A,B)$ 是由 $A$ 和 $B$ 共同决定的非齐次“平移部分”。这种观点将一个看似复杂的坐标计算公式，提升到了一个描述几何结构（联络）如何与坐标变换的二阶信息相互作用的深刻层面 [@problem_id:3005696]。