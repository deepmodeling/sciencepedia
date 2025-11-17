## 引言
[麦克斯韦方程组](@entry_id:150940)是经典电磁学的基石，它以无与伦比的精确性描述了宏观世界的电磁现象。然而，随着爱因斯坦[狭义相对论](@entry_id:275552)的诞生，一个根本性的问题浮出水面：这套看似完美的方程在不同惯性参考系之间变换时，是否能保持其形式不变？答案是肯定的，但其传统的三维矢量形式却巧妙地掩盖了这种深刻的[洛伦兹协变性](@entry_id:161987)。为了揭示并充分利用这一内在对称性，物理学家们发展出了一套更为强大的数学语言——四维时空中的[张量分析](@entry_id:161423)。

本文旨在系统地引导读者完成这一认知飞跃，将经典电磁理论重塑为其“不言自明”的协变形式。我们将不再孤立地看待[电场](@entry_id:194326)与[磁场](@entry_id:153296)、[电荷](@entry_id:275494)与电流，而是将它们视为统一的四维物理量在不同视角下的展现。

在接下来的章节中，你将学到：

- **第一章：原理与机制** 将奠定理论基础。我们将学习如何将标量势与矢量势统一为“[四维势](@entry_id:188407)”，将电荷密度与电流密度统一为“[四维流](@entry_id:199021)”，并最终将[电场](@entry_id:194326)与[磁场](@entry_id:153296)统一为核心概念——“[电磁场张量](@entry_id:158921)”。在此基础上，我们将看到原本复杂的[麦克斯韦方程组](@entry_id:150940)如何被压缩成两个异常简洁的张量方程。

- **第二章：应用与跨学科联系** 将展示这一新形式的强大威力。我们将探讨[电场](@entry_id:194326)与[磁场](@entry_id:153296)的相对性，分析协变形式下的[守恒定律](@entry_id:269268)，并领略它如何成为连接[狭义相对论](@entry_id:275552)、粒子物理乃至广义相对论等前沿领域的理论桥梁。

- **第三章：动手实践** 将通过一系列精心设计的问题，帮助你将抽象的理论转化为具体的计算能力，从而真正掌握[协变电动力学](@entry_id:272426)的分析工具。

通过本次学习，你将不仅仅是学会一种新的数学技巧，更是对电磁现象的本质以及物理定律的普适性与和谐之美获得一次深刻的洞见。

## 原理与机制

在经典电磁学中，[麦克斯韦方程组](@entry_id:150940)和[洛伦兹力定律](@entry_id:270735)完美地描述了电磁现象。然而，当阿尔伯特·爱因斯坦提出[狭义相对论](@entry_id:275552)时，一个深刻的问题出现了：这些电磁学定律在不同的[惯性参考系](@entry_id:276742)下是否保持形式不变？答案是肯定的，麦克斯韦方程组本身就内蕴着[洛伦兹协变性](@entry_id:161987)。然而，其传统的三维矢量形式掩盖了这一优美的对称性。为了揭示并利用这种对称性，我们需要一种新的数学语言——四维时空的张量语言。本章将系统地阐述如何将麦克斯韦理论重塑为一种不言自明（manifestly）的协变形式，从而统一[电场](@entry_id:194326)与[磁场](@entry_id:153296)、[电荷密度](@entry_id:144672)与[电流密度](@entry_id:190690)，并揭示其背后更深刻的物理原理。

### [四维势](@entry_id:188407)和[四维流](@entry_id:199021)：电磁学量的相对论统一

[狭义相对论](@entry_id:275552)的基石是将时间和空间统一为四维时空。一个事件由其时空坐标 $x^\mu = (x^0, x^1, x^2, x^3) = (ct, x, y, z)$ 描述，其中 $c$ 是[真空中的光速](@entry_id:272753)。这被称为**四维位置矢量**。在闵可夫斯基时空中，两个无穷近事件之间的[时空间隔](@entry_id:154935) $ds^2$ 是一个[洛伦兹不变量](@entry_id:161821)，由[度规张量](@entry_id:160222) $\eta_{\mu\nu}$ 定义：$ds^2 = \eta_{\mu\nu} dx^\mu dx^\nu$。在本章中，我们采用 $(+,-,-,-)$ 的度规符号，即 $\eta_{\mu\nu} = \text{diag}(1, -1, -1, -1)$。上标表示**逆变**（contravariant）分量，下标表示**协变**（covariant）分量，它们通过度规张量相互转换，例如 $V_\mu = \eta_{\mu\nu}V^\nu$。

电磁学的协变之旅始于将标量势 $\phi$ 和矢量势 $\mathbf{A}$ 统一起来。在三维表述中，它们似乎是独立的实体，但在相对论框架下，它们被证明是同一个物理量在不同[参考系](@entry_id:169232)下的不同表现。我们将它们组合成一个**[四维势](@entry_id:188407)矢量** $A^\mu$：

$$
A^\mu = \left(\frac{\phi}{c}, \mathbf{A}\right) = \left(\frac{\phi}{c}, A_x, A_y, A_z\right)
$$

这个定义并非人为的拼凑，而是深刻物理洞见的体现。正如时间和空间是四维时空的组成部分一样，$\phi/c$ 和 $\mathbf{A}$ 也构成了[四维势](@entry_id:188407)矢量的“时间”分量和“空间”分量。例如，考虑一个由[标量势](@entry_id:276177) $\phi = -E_0 y$ 和矢量势 $\mathbf{A} = B_0 x \hat{\mathbf{y}}$ 描述的[电磁场](@entry_id:265881)，其中 $E_0$ 和 $B_0$ 为常数。根据定义，对应的逆变[四维势](@entry_id:188407) $A^\mu$ 可以直接写出 [@problem_id:1806986]：

$$
A^\mu = \left(\frac{-E_0 y}{c}, 0, B_0 x, 0\right)
$$

这个四维矢量在[洛伦兹变换](@entry_id:176827)下的行为与时空坐标 $x^\mu$ 完全相同，这确保了由它导出的物理定律的协变性。

与此类似，[电荷](@entry_id:275494)的源——电荷密度 $\rho$ 和[电流密度](@entry_id:190690) $\mathbf{j}$——也被统一到**[四维电流密度](@entry_id:262568)** $J^\mu$ 中：

$$
J^\mu = (c\rho, \mathbf{j}) = (c\rho, j_x, j_y, j_z)
$$

这个统一揭示了[电荷密度](@entry_id:144672)和[电流密度](@entry_id:190690)之间的内在联系：一个[参考系](@entry_id:169232)中观察到的纯[电荷密度](@entry_id:144672)，在另一个相对运动的[参考系](@entry_id:169232)中可能会表现为既有[电荷密度](@entry_id:144672)又有[电流密度](@entry_id:190690)。

让我们考虑一个具体的例子：一束[带电粒子](@entry_id:160311)沿 z 轴以速度 $\mathbf{v} = v \hat{\mathbf{k}}$ 运动。在与粒子共动的[参考系](@entry_id:169232)（静止系）中，粒子是静止的，因此没有[宏观电流](@entry_id:203974)，$\mathbf{j}' = \mathbf{0}$。如果粒子的固有[数密度](@entry_id:268986)为 $n$，每个粒子的[电荷](@entry_id:275494)为 $q$，那么静止系中的[固有电荷密度](@entry_id:181786)为 $\rho' = qn$。因此，静止系中的[四维电流](@entry_id:199021)为 $J'^{\mu} = (c\rho', \mathbf{0}) = (cqn, 0, 0, 0)$。

要在[实验室参考系](@entry_id:166991)中找到 $J^\mu$，我们只需对 $J'^{\mu}$ 应用一个沿 z 轴的[洛伦兹变换](@entry_id:176827)。变换关系为 $J^\mu = \Lambda^\mu_{\,\,\,\nu} J'^\nu$，其中 $\Lambda^\mu_{\,\,\,\nu}$ 是洛伦兹变换矩阵。其结果是 [@problem_id:1573984]：

$$
J^0 = \gamma(J'^0 + \beta J'^3) = \gamma (cqn) = \frac{cqn}{\sqrt{1 - v^2/c^2}}
$$
$$
J^3 = \gamma(J'^3 + \beta J'^0) = \gamma \beta (cqn) = \frac{vqn}{\sqrt{1 - v^2/c^2}}
$$
$$
J^1 = J'^1 = 0, \quad J^2 = J'^2 = 0
$$

其中 $\gamma = (1 - v^2/c^2)^{-1/2}$ 是洛伦兹因子，$\beta = v/c$。因此，在[实验室参考系](@entry_id:166991)中，[四维电流](@entry_id:199021)为 $J^\mu = (\gamma cqn, 0, 0, \gamma vqn)$。我们看到，[实验室参考系](@entry_id:166991)中的[电荷密度](@entry_id:144672) $\rho = J^0/c = \gamma qn$，这正是由于长度收缩效应导致的结果。同时，实验室中也出现了[电流密度](@entry_id:190690) $j_z = J^3 = \gamma vqn = \rho v$，这完全符合预期。

### [电磁场张量](@entry_id:158921)

既然[电磁场](@entry_id:265881)的势和源都是四维矢量，那么[电场](@entry_id:194326) $\mathbf{E}$ 和[磁场](@entry_id:153296) $\mathbf{B}$ 本身又是什么呢？它们不再是独立的矢量，而是统一为一个二阶[反对称张量](@entry_id:199349)的不同分量。这个张量被称为**电磁场张量**或**法拉第张量** $F^{\mu\nu}$，它由[四维势](@entry_id:188407)通过[微分](@entry_id:158718)定义：

$$
F^{\mu\nu} = \partial^\mu A^\nu - \partial^\nu A^\mu
$$

这里的 $\partial^\mu = \eta^{\mu\sigma}\frac{\partial}{\partial x^\sigma} = (\frac{1}{c}\frac{\partial}{\partial t}, -\nabla)$ 是逆变四维[梯度算子](@entry_id:275922)。从这个定义可以立即看出 $F^{\mu\nu}$ 的一个关键性质：它是**反对称**的，即 $F^{\mu\nu} = -F^{\nu\mu}$。这是因为 $\partial^\mu \partial^\nu - \partial^\nu \partial^\mu = 0$。

我们可以通过一个具体的计算来理解这个定义。给定一个假设的[四维势](@entry_id:188407) $A^\mu = (K x y, \lambda z^2, D x z, 0)$，我们可以计算 $F^{\mu\nu}$ 的一个分量，例如 $F^{12}$ [@problem_id:1806993]。根据定义：

$$
F^{12} = \partial^1 A^2 - \partial^2 A^1
$$

其中 $\partial^1 = -\frac{\partial}{\partial x}$，$\partial^2 = -\frac{\partial}{\partial y}$，以及 $A^1 = \lambda z^2$，$A^2 = Dxz$。
计算得到：
$$
\partial^1 A^2 = -\frac{\partial}{\partial x}(Dxz) = -Dz
$$
$$
\partial^2 A^1 = -\frac{\partial}{\partial y}(\lambda z^2) = 0
$$
因此，$F^{12} = -Dz - 0 = -Dz$。

将 $F^{\mu\nu}$ 的所有分量展开，我们便能发现它与 $\mathbf{E}$ 和 $\mathbf{B}$ 场的联系。通过将 $A^\mu = (\phi/c, \mathbf{A})$ 代入定义，并利用 $\mathbf{E} = -\nabla\phi - \frac{\partial \mathbf{A}}{\partial t}$ 和 $\mathbf{B} = \nabla \times \mathbf{A}$，可以得到 $F^{\mu\nu}$ 的矩阵形式：

$$
F^{\mu\nu} = 
\begin{pmatrix}
0        -E_x/c   -E_y/c   -E_z/c \\
E_x/c    0        -B_z     B_y \\
E_y/c    B_z      0        -B_x \\
E_z/c    -B_y     B_x      0
\end{pmatrix}
$$

这个矩阵清晰地展示了 $\mathbf{E}$ 场和 $\mathbf{B}$ 场是如何作为同一个[二阶张量](@entry_id:199780) $F^{\mu\nu}$ 的六个独立分量出现的。时间-空间分量 ($F^{0i}$) 对应于[电场](@entry_id:194326)，而空间-空间分量 ($F^{ij}$) 对应于[磁场](@entry_id:153296)。例如，从矩阵中可以直接读出 $E_y = -c F^{02}$ 和 $B_z = -F^{12}$ [@problem_id:1573954]。这个统一的观点是革命性的：[电场和磁场](@entry_id:261347)不再是两个独立的实体，它们可以像时间和空间一样，在不同的惯性参考系之间相互转化。一个观察者看到的纯[电场](@entry_id:194326)，在另一个[相对运动](@entry_id:169798)的观察者看来可能是一个混合了电场和磁场的场。

### [协变](@entry_id:634097)形式下的[规范不变性](@entry_id:137857)

在[经典电动力学](@entry_id:270496)中，[电磁势](@entry_id:266145)并非唯一确定。我们可以对势进行**[规范变换](@entry_id:176521)**，$\phi' = \phi - \frac{\partial \chi}{\partial t}$ 和 $\mathbf{A}' = \mathbf{A} + \nabla\chi$，其中 $\chi$ 是任意一个标量函数，而电场和磁场保持不变。这个重要的性质被称为**[规范不变性](@entry_id:137857)**。在[协变](@entry_id:634097)形式下，这个变换变得异常简洁。

将[四维势](@entry_id:188407) $A^\mu$ 和标量函数 $\chi$ 结合，[规范变换](@entry_id:176521)可以统一写为：

$$
A'^\mu = A^\mu - \partial^\mu \chi
$$

其中 $\partial^\mu \chi$ 是 $\chi$ 的四维梯度。现在我们可以证明，电磁场张量 $F^{\mu\nu}$ 在此变换下保持不变，这体现了物理的[可观测性](@entry_id:152062)（场）不依赖于我们选择的数学工具（势）。变换后的[场张量](@entry_id:186486)为：

$$
F'^{\mu\nu} = \partial^\mu A'^\nu - \partial^\nu A'^\mu = \partial^\mu (A^\nu - \partial^\nu \chi) - \partial^\nu (A^\mu - \partial^\mu \chi)
$$
$$
= (\partial^\mu A^\nu - \partial^\nu A^\mu) - (\partial^\mu \partial^\nu \chi - \partial^\nu \partial^\mu \chi)
$$

由于[偏导数](@entry_id:146280)可以交换次序（$\partial^\mu \partial^\nu = \partial^\nu \partial^\mu$），上式右边的第二项恒为零。因此，我们得到：

$$
F'^{\mu\nu} = F^{\mu\nu}
$$

这证明了电磁场张量是规范不变的。我们可以通过一个例子来具体验证这一点 [@problem_id:1573971]。假设初始[四维势](@entry_id:188407)为 $A^\mu = (0, -ky, kx, 0)$，[规范函数](@entry_id:749731)为 $\chi = -kxy$。根据变换规则 $A'^\mu = A^\mu - \partial^\mu\chi$，新的势 $A'^\mu$ 为：
$A'^\mu = A^\mu - \partial^\mu(-kxy) = A^\mu + \partial^\mu(-kxy) = (0, -ky, kx, 0) + (0, ky, kx, 0) = (0, 0, 2kx, 0)$。
尽管势从 $A^\mu$ 变成了 $A'^\mu$，但计算出的[场张量](@entry_id:186486)分量 $F'^{12}$ 却与原来的 $F^{12}$ 完全相同，均为 $-2k$。这表明，势可以有无穷多种选择（对应不同的规范），但它们都描述同一个物理实在——[电磁场](@entry_id:265881)。

### [麦克斯韦方程组的协变形式](@entry_id:197529)

电磁学理论的核心是[麦克斯韦方程组](@entry_id:150940)。在四维时空语言中，这四组八个方程可以被优雅地压缩为两个简洁的张量方程。

#### 非齐次方程

包含源（[电荷](@entry_id:275494)和电流）的两个麦克斯韦方程——[高斯电场定律](@entry_id:146732)和[安培-麦克斯韦定律](@entry_id:266368)——可以被统一成一个单一的方程：

$$
\partial_\mu F^{\mu\nu} = \mu_0 J^\nu
$$

其中 $\partial_\mu = \frac{\partial}{\partial x^\mu}$ 是协变四维[梯度算子](@entry_id:275922)，$\mu_0$ 是[真空磁导率](@entry_id:186031)。这个方程的含义是，[电磁场张量](@entry_id:158921)的四维散度等于源（[四维电流](@entry_id:199021)）。这是一个张量方程，因此在所有惯性系下都保持形式不变。

这个方程包含了四个分量（对应于[自由指标](@entry_id:189430) $\nu=0, 1, 2, 3$）。让我们来“解开”它，看看它如何还原为我们熟悉的形式 [@problem_id:1573967]。

当 $\nu=0$ 时（时间分量）：
$$
\partial_\mu F^{\mu 0} = \partial_0 F^{00} + \partial_1 F^{10} + \partial_2 F^{20} + \partial_3 F^{30} = \mu_0 J^0
$$
利用 $F^{\mu\nu}$ 的反对称性 ($F^{i0} = -F^{0i} = E_i/c$) 和 $F^{00}=0$，上式变为：
$$
\frac{\partial (E_x/c)}{\partial x} + \frac{\partial (E_y/c)}{\partial y} + \frac{\partial (E_z/c)}{\partial z} = \mu_0 (c\rho)
$$
整理后得到 $\nabla \cdot \mathbf{E} = \mu_0 c^2 \rho$。利用关系 $c^2 = 1/(\mu_0 \epsilon_0)$，这正是**[高斯电场定律](@entry_id:146732)**: $\nabla \cdot \mathbf{E} = \rho/\epsilon_0$。

当 $\nu=k$（空间分量，例如 $k=1$ 对应x分量）时：
$$
\partial_\mu F^{\mu 1} = \partial_0 F^{01} + \partial_1 F^{11} + \partial_2 F^{21} + \partial_3 F^{31} = \mu_0 J^1
$$
代入 $F^{\mu\nu}$ 的分量 ($F^{01}=-E_x/c$, $F^{21}=B_z$, $F^{31}=-B_y$) 和 $J^1 = j_x$，我们得到：
$$
\frac{1}{c}\frac{\partial (-E_x/c)}{\partial t} + \frac{\partial (0)}{\partial x} + \frac{\partial B_z}{\partial y} - \frac{\partial B_y}{\partial z} = \mu_0 j_x
$$
整理后得到 $(\nabla \times \mathbf{B})_x - \frac{1}{c^2}\frac{\partial E_x}{\partial t} = \mu_0 j_x$。写成矢量形式并使用 $c^2 = 1/(\mu_0 \epsilon_0)$，这正是**[安培-麦克斯韦定律](@entry_id:266368)**: $\nabla \times \mathbf{B} = \mu_0 \mathbf{j} + \mu_0 \epsilon_0 \frac{\partial \mathbf{E}}{\partial t}$。

我们也可以反过来应用这个强大的方程。例如，如果已知[电场](@entry_id:194326) $\mathbf{E} = \alpha t \hat{\mathbf{y}}$ 和[磁场](@entry_id:153296) $\mathbf{B} = \beta x \hat{\mathbf{z}}$，我们可以通过计算 $\partial_\mu F^{\mu\nu}$ 来确定产生这种场所需要的电流密度 [@problem_id:1573983]。计算表明，[电流密度](@entry_id:190690)的y分量必须为 $J_y = -\frac{1}{\mu_0}(\frac{\alpha}{c^2} + \beta)$。

#### [齐次方程](@entry_id:163650)与电荷守恒

另外两个不含源的麦克斯韦方程——高斯[磁场](@entry_id:153296)定律和[法拉第感应定律](@entry_id:146175)——又如何表示呢？它们可以由所谓的**[比安基恒等式](@entry_id:261685)**（Bianchi identity）给出：

$$
\partial_\lambda F_{\mu\nu} + \partial_\mu F_{\nu\lambda} + \partial_\nu F_{\lambda\mu} = 0
$$

这个方程之所以成立，是因为 $F_{\mu\nu}$ 可以由一个势 $A_\mu$ 导出。为了得到一个更紧凑且与非齐次方程形式更对称的表达，我们引入**对偶[电磁张量](@entry_id:272274)** $G^{\mu\nu}$：

$$
G^{\mu\nu} = \frac{1}{2} \epsilon^{\mu\nu\lambda\sigma} F_{\lambda\sigma}
$$

其中 $\epsilon^{\mu\nu\lambda\sigma}$ 是四维[列维-奇维塔符号](@entry_id:193594)（$\epsilon^{0123}=1$）。这个变换本质上是进行了 $\mathbf{E}/c \to \mathbf{B}$ 和 $\mathbf{B} \to -\mathbf{E}/c$ 的对偶替换。对偶张量的矩阵形式为：
$$
G^{\mu\nu} = 
\begin{pmatrix}
0        -B_x    -B_y    -B_z \\
B_x      0       E_z/c   -E_y/c \\
B_y      -E_z/c  0       E_x/c \\
B_z      E_y/c   -E_x/c  0
\end{pmatrix}
$$

利用对偶张量，齐次麦克斯韦方程可以惊人地写成与非齐次方程完全相似的形式 [@problem_id:1573956]：

$$
\partial_\mu G^{\mu\nu} = 0
$$

这个方程的四维散度为零，其 $\nu=0$ 分量给出了**高斯[磁场](@entry_id:153296)定律** $\nabla \cdot \mathbf{B} = 0$，而其空间分量（$\nu=1,2,3$）则给出了**[法拉第感应定律](@entry_id:146175)** $\nabla \times \mathbf{E} + \frac{\partial \mathbf{B}}{\partial t} = 0$。

协变形式不仅统一了方程，还揭示了一个基本定律的深刻根源：**电荷守恒**。考虑非[齐次方程](@entry_id:163650) $\partial_\mu F^{\mu\nu} = \mu_0 J^\nu$。如果我们对这个方程两边同时求四维散度（即作用算子 $\partial_\nu$）：

$$
\partial_\nu (\partial_\mu F^{\mu\nu}) = \mu_0 \partial_\nu J^\nu
$$

方程的左边 $\partial_\nu \partial_\mu F^{\mu\nu}$ 是一个[对称算子](@entry_id:272489) $\partial_\nu \partial_\mu$ 作用在一个[反对称张量](@entry_id:199349) $F^{\mu\nu}$ 上。由于偏导数可交换，而 $F^{\mu\nu}$ 反对称，这个项恒等于零。因此，我们必然得到：

$$
\partial_\nu J^\nu = 0
$$

这正是**[电荷守恒](@entry_id:264158)的连续性方程** $\frac{\partial \rho}{\partial t} + \nabla \cdot \mathbf{j} = 0$ 的[协变](@entry_id:634097)形式。这表明，[电荷守恒](@entry_id:264158)并非一个独立的假设，而是电磁理论内在结构的必然结果。如果理论被修改，例如，假设 $\partial_\mu F^{\mu\nu} = \mu_0 J^\nu + \alpha x^\nu$ [@problem_id:1806974]，那么取散度后会得到 $\partial_\nu J^\nu = -4\alpha/\mu_0$，这意味着[电荷](@entry_id:275494)不再守恒。这突显了麦克斯韦理论结构的精妙与严谨。

### [洛伦兹力定律](@entry_id:270735)与粒子动力学

一个完整的理论不仅需要描述场如何由源产生（[麦克斯韦方程组](@entry_id:150940)），还需要描述场如何作用于物质（[洛伦兹力定律](@entry_id:270735)）。在协变形式下，描述一个[带电粒子运动](@entry_id:262424)的方程也同样优雅。

一个质量为 $m$ 的粒子，其运动状态由**[四维速度](@entry_id:269673)** $u^\mu = \frac{dx^\mu}{d\tau} = \gamma(c, \mathbf{v})$ 描述，其中 $\tau$ 是粒子的固有时。相应的**[四维动量](@entry_id:272346)**为 $p^\mu = m u^\mu$。作用在粒子上的**[四维力](@entry_id:273918)**被定义为[四维动量](@entry_id:272346)随[固有时](@entry_id:192124)的变化率，$f^\mu = \frac{dp^\mu}{d\tau}$。

[电磁场](@entry_id:265881)对[电荷](@entry_id:275494)为 $q$ 的粒子的作用力，即[洛伦兹力](@entry_id:145104)，其[协变](@entry_id:634097)表达式为 [@problem_id:1573969]：

$$
f^\mu = q F^{\mu\nu} u_\nu
$$

这个简洁的方程将粒子的[电荷](@entry_id:275494)、场的强度以及粒子的运动状态联系在一起，给出了一个[四维力](@entry_id:273918)。这个[四维力](@entry_id:273918)的时间分量（$\mu=0$）描述了[电磁场](@entry_id:265881)对粒子所做的功率（能量变化率），而其空间分量（$\mu=1,2,3$）则对应于我们熟悉的三维[洛伦兹力](@entry_id:145104) $\mathbf{F} = q(\mathbf{E} + \mathbf{v} \times \mathbf{B})$。

例如，$f^0 = q F^{0\nu} u_\nu = q(F^{0i} u_i) = q(\frac{-E_i}{c})(-\gamma v_i) = \frac{\gamma}{c} q(\mathbf{E} \cdot \mathbf{v})$。而已知 $f^0 = \frac{dp^0}{d\tau} = \frac{d(E/c)}{d\tau} = \gamma \frac{d(E/c)}{dt}$，联立两式可得功率方程 $\frac{dE}{dt} = q\mathbf{E}\cdot\mathbf{v}$。

值得注意的是，[四维力](@entry_id:273918) $f^\mu$ 总是与[四维速度](@entry_id:269673) $u_\mu$ 正交，即 $f^\mu u_\mu = 0$。这是因为 $f^\mu u_\mu = q F^{\mu\nu} u_\nu u_\mu$，由于 $F^{\mu\nu}$ 反对称而 $u_\nu u_\mu$ 对称，它们的缩并为零。这个[正交关系](@entry_id:145540)有一个重要的物理意义：[电磁力](@entry_id:196024)虽然可以改变粒子的能量和三维动量，但它不能改变粒子的静止质量。

至此，我们完成了电磁理论的协变表述。通过引入[四维矢量](@entry_id:275085)和张量，我们将看似分离的物理量统一起来，将复杂的麦克斯韦方程组和[洛伦兹力定律](@entry_id:270735)化为简洁而优美的形式，并彰显了其在所有惯性参考系下不变的深刻对称性。这种表述不仅是数学上的简化，更是对电磁现象本质的更深层次的理解，为后来规范场论的发展奠定了坚实的基础。