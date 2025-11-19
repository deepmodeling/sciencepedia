## 引言
[麦克斯韦方程组](@entry_id:150940)是经典电磁学的基石，它完美地统一了电、磁和光学现象。然而，随着20世纪初爱因斯坦狭义相对论的诞生，一个深刻的问题浮出水面：经典形式的[麦克斯韦方程组](@entry_id:150940)是否与“物理定律在所有[惯性参考系](@entry_id:276742)中形式不变”这一相对性原理相容？电场和磁场这两个看似独立的矢量场，在不同的观测者看来又将如何变换？

本文旨在系统地解答这些问题，其核心是引入[麦克斯韦方程组的协变形式](@entry_id:197529)——一种将电磁学与[狭义相对论原理](@entry_id:197470)无缝融合的优雅数学框架。通过采用四维时空语言，我们将超越传统的三维矢量分析，揭示电磁现象背后更深层次的统一性与对称性。

在接下来的章节中，你将学习到：第一章“原理与机制”将为你构建起协变形式的数学基础，包括四维矢量、[电磁场张量](@entry_id:158921)以及协变的麦克斯韦方程组；第二章“应用与跨学科联系”将展示这一强大工具在解决实际问题、理解[电磁场](@entry_id:265881)相对性，乃至连接广义相对论和[量子场论](@entry_id:138177)等前沿领域中的威力；最后，第三章“动手实践”将提供具体问题，助你巩固所学。让我们首先进入第一章，深入探索这一理论的原理与机制。

## 原理与机制

在本章中，我们将深入探讨电磁理论的[协变](@entry_id:634097)形式，这是一种将麦克斯韦方程组和[洛伦兹力定律](@entry_id:270735)与[狭义相对论原理](@entry_id:197470)无缝结合的优雅数学框架。通过引入四维矢量和张量的语言，我们将看到原本看似分离的电场和磁场、[电荷密度](@entry_id:144672)和[电流密度](@entry_id:190690)，如何被统一为单一的四维实体。这种表述不仅极大地简化了方程的形式，还深刻地揭示了电磁现象背后的基本对称性和守恒律。

### [电磁场](@entry_id:265881)中的[四维矢量](@entry_id:275085)

狭义相对论的核心思想是，物理定律在所有惯性参考系中都应具有相同的形式。为了实现这一点，我们将三维空间和一维时间融合成一个四维时空。在此框架下，许多经典的三维物理量需要被推广为[四维矢量](@entry_id:275085)（four-vectors），以确保它们在[洛伦兹变换](@entry_id:176827)下具有正确的变换性质。

#### [四维势](@entry_id:188407)

在经典电磁学中，我们引入标量势 $\phi$ 和矢量势 $\mathbf{A}$ 来简化对[电场](@entry_id:194326) $\mathbf{E}$ 和[磁场](@entry_id:153296) $\mathbf{B}$ 的计算。这两个势并非独立的实体，在相对论框架下，它们共同构成了**[四维势](@entry_id:188407)**（four-potential）$A^\mu$ 的不同分量。在一个时空坐标为 $x^\mu = (ct, x, y, z)$ 的惯性系中，逆变[四维势](@entry_id:188407)定义为：

$A^\mu = (\frac{\phi}{c}, A_x, A_y, A_z)$

其中 $c$ 是[真空中的光速](@entry_id:272753)。将 $\phi$ 和 $\mathbf{A}$ 统一为一个[四维矢量](@entry_id:275085)，意味着它们在不同惯性参考系之间的变换不再是独立的，而是作为一个整体遵循洛伦兹变换。例如，考虑一个由标量势 $\phi = -E_0 y$ 和矢量势 $\mathbf{A} = B_0 x \hat{\mathbf{y}}$ 描述的[电磁场](@entry_id:265881)，其中 $E_0$ 和 $B_0$ 为常数。对应的[四维势](@entry_id:188407)可以直接写出其四个分量 [@problem_id:1806986]：

$A^\mu = (-\frac{E_0 y}{c}, 0, B_0 x, 0)$

这种统一是协变形式的第一步，它预示着[电场和磁场](@entry_id:261347)本身也是一个更深层次的统一结构的不同侧面。

#### [四维流密度](@entry_id:262568)

[电磁场](@entry_id:265881)的源是[电荷](@entry_id:275494)和电流。与势类似，[电荷密度](@entry_id:144672) $\rho$（单位体积的[电荷](@entry_id:275494)）和三维电流密度 $\mathbf{J}$ 也可以被统一为一个[四维矢量](@entry_id:275085)，称为**[四维流密度](@entry_id:262568)**（four-current density）$J^\mu$。其定义为：

$J^\mu = (c\rho, J_x, J_y, J_z) = (c\rho, \mathbf{J})$

$J^\mu$ 的时间分量 $J^0 = c\rho$ 与电荷密度成正比，而其空间分量则构成了三维电流密度矢量 $\mathbf{J}$。这个四维矢量的引入，使得[电荷守恒](@entry_id:264158)定律有了一个极其简洁的表达形式，我们将在稍后探讨。

为了理解 $J^\mu$ 如何体现其[四维矢量](@entry_id:275085)特性，我们可以考虑一个具体的物理情景 [@problem_id:1573984]。设想一束[带电粒子](@entry_id:160311)沿 z 轴正方向以恒定速度 $\mathbf{v} = v \hat{\mathbf{k}}$ 运动。在与粒子共同运动的[参考系](@entry_id:169232)（静止系）中，粒子是静止的，因此三维电流密度为零 ($\mathbf{J}' = \mathbf{0}$)。如果粒子的固有[数密度](@entry_id:268986)为 $n$，每个粒子的[电荷](@entry_id:275494)为 $q$，那么静止系中的电荷密度就是 $\rho' = qn$。因此，在静止系中，[四维流密度](@entry_id:262568)为：

$J'^\mu = (c\rho', \mathbf{J}') = (cqn, 0, 0, 0)$

现在，我们想知道在[实验室参考系](@entry_id:166991)中观测到的[四维流密度](@entry_id:262568) $J^\mu$ 是什么。实验室系相对于静止系以速度 $v$ 沿 z 轴运动。$J^\mu$ 的分量可以通过对 $J'^\mu$ 应用[洛伦兹变换](@entry_id:176827)得到。对于沿 z 轴的加速，变换关系为：

$J^0 = \gamma (J'^0 + \beta J'^3)$
$J^3 = \gamma (J'^3 + \beta J'^0)$
$J^1 = J'^1$
$J^2 = J'^2$

其中 $\beta = v/c$，[洛伦兹因子](@entry_id:159588) $\gamma = (1 - v^2/c^2)^{-1/2}$。代入静止系的值 $J'^0=cqn$ 和 $J'^{1,2,3}=0$，我们得到实验室系中的分量：

$J^0 = \gamma (cqn + 0) = \frac{qnc}{\sqrt{1 - v^2/c^2}}$
$J^1 = 0$
$J^2 = 0$
$J^3 = \gamma (0 + \beta cqn) = \gamma v q n = \frac{qnv}{\sqrt{1 - v^2/c^2}}$

这个结果揭示了一个深刻的物理事实：在一个[参考系](@entry_id:169232)中纯粹的电荷密度（由 $J'^0$ 体现），在另一个[相对运动](@entry_id:169798)的[参考系](@entry_id:169232)中会同时表现为[电荷密度](@entry_id:144672)（$J^0 = c\rho = c(\gamma qn)$）和电流密度（$\mathbf{J} = (\gamma qn)\mathbf{v}$）。电荷密度的增加因子 $\gamma$ 正是由于长度收缩效应导致的。这个例子完美地展示了[电荷密度](@entry_id:144672)和电流密度是如何作为单个四维实体 $J^\mu$ 的不同分量而相互关联的。

### 电磁场张量

将[电场](@entry_id:194326) $\mathbf{E}$ 和[磁场](@entry_id:153296) $\mathbf{B}$ 统一起来的数学对象是**电磁场张量**（electromagnetic field tensor），也称为**[法拉第张量](@entry_id:158921)**（Faraday tensor），记为 $F^{\mu\nu}$。它是一个二阶[反对称张量](@entry_id:199349)，其定义将场与[四维势](@entry_id:188407)联系起来。

#### 从[四维势](@entry_id:188407)到[场张量](@entry_id:186486)

[电磁场张量](@entry_id:158921) $F^{\mu\nu}$ 定义为[四维势](@entry_id:188407) $A^\mu$ 的“四维旋度”：

$F^{\mu\nu} = \partial^\mu A^\nu - \partial^\nu A^\mu$

这里，$\partial^\mu = \eta^{\mu\sigma}\frac{\partial}{\partial x^\sigma} = (\frac{1}{c}\frac{\partial}{\partial t}, -\nabla)$ 是[逆变](@entry_id:192290)四维梯度算符。从这个定义可以立刻看出 $F^{\mu\nu}$ 的一个基本性质：它是**反对称的**，即 $F^{\mu\nu} = -F^{\nu\mu}$。这是因为交换索引 $\mu$ 和 $\nu$ 只会给表达式带来一个负号。

我们可以通过一个例子来练习这个定义 [@problem_id:1806993]。给定一个[四维势](@entry_id:188407) $A^\mu = (K x y, \lambda z^2, D x z, 0)$，我们可以计算 $F^{\mu\nu}$ 的任意分量，例如 $F^{12}$：

$F^{12} = \partial^1 A^2 - \partial^2 A^1 = (-\frac{\partial}{\partial x})(Dxz) - (-\frac{\partial}{\partial y})(\lambda z^2) = -Dz - 0 = -Dz$

这个计算直接将势的导数与[场张量](@entry_id:186486)的分量联系起来。

#### [场张量](@entry_id:186486)的分量：[电场](@entry_id:194326)与[磁场](@entry_id:153296)

$F^{\mu\nu}$ 的真正威力在于它的16个分量（由于反对称性，只有6个是独立的）恰好对应于[电场](@entry_id:194326) $\mathbf{E}$ 的3个分量和[磁场](@entry_id:153296) $\mathbf{B}$ 的3个分量。通过将定义 $F^{\mu\nu} = \partial^\mu A^\nu - \partial^\nu A^\mu$ 展开，并与经典关系式 $\mathbf{E} = -\nabla\phi - \frac{\partial\mathbf{A}}{\partial t}$ 和 $\mathbf{B} = \nabla \times \mathbf{A}$ 进行比较，可以确定 $F^{\mu\nu}$ 的各个分量。在使用 $(+,-,-,-)$ [闵可夫斯基度规](@entry_id:154660) $\eta_{\mu\nu}$ 时，[逆变](@entry_id:192290)[场张量](@entry_id:186486) $F^{\mu\nu}$ 的矩阵形式为：

$F^{\mu\nu} = \begin{pmatrix} 0  -E_x/c  -E_y/c  -E_z/c \\ E_x/c  0  -B_z  B_y \\ E_y/c  B_z  0  -B_x \\ E_z/c  -B_y  B_x  0 \end{pmatrix}$

这个矩阵优美地将 $\mathbf{E}$ 场和 $\mathbf{B}$ 场统一在同一个数学结构中。时间-空间分量 ($F^{0i}$) 对应于[电场](@entry_id:194326)，而空间-空间分量 ($F^{ij}$) 对应于[磁场](@entry_id:153296)。

理解如何从这个张量中“读取”电场和磁场分量至关重要 [@problem_id:1573954]。例如：
- [电场](@entry_id:194326)分量 $E_y$ 可以通过 $F^{02}$ 得到：$E_y = -c F^{02}$。由于反对称性，$F^{20} = -F^{02}$，因此 $E_y = c F^{20}$。
- [磁场](@entry_id:153296)分量 $B_z$ 与 $F^{12}$ 和 $F^{21}$ 有关。从矩阵中我们看到 $F^{12} = -B_z$ 和 $F^{21} = B_z$。
- 我们还可以使用[协变张量](@entry_id:634493) $F_{\mu\nu} = \eta_{\mu\alpha}\eta_{\nu\beta}F^{\alpha\beta}$。对于 $(+,-,-,-)$ 度规，$F_{0i} = E_i/c$，$F_{ij} = -F^{ij}$。因此，$B_z = F_{12}$。
- [磁场](@entry_id:153296)分量也可以通过三维[列维-奇维塔符号](@entry_id:193594) $\epsilon_{ijk}$ 表示：$B_k = -\frac{1}{2}\epsilon_{ijk}F^{ij}$。

这种统一的表示法再次强调，[电场和磁场](@entry_id:261347)并非独立实体，而是同一个物理实体——[电磁场张量](@entry_id:158921)——在特定[参考系](@entry_id:169232)下的不同表现。一个观察者看到的纯[电场](@entry_id:194326)，在另一个相对运动的观察者看来可能既有[电场](@entry_id:194326)也有[磁场](@entry_id:153296)。

#### 规范不变性

从定义 $F^{\mu\nu} = \partial^\mu A^\nu - \partial^\nu A^\mu$ 可见，[场张量](@entry_id:186486)是通过对[四维势](@entry_id:188407)求导得到的。这意味着我们可以对[四维势](@entry_id:188407)进行某种变换而不改变物理上可观测的场。这种变换被称为**[规范变换](@entry_id:176521)**（gauge transformation），其形式为：

$A'^\mu = A^\mu + \partial^\mu \chi$

其中 $\chi(x^\mu)$ 是任意一个光滑的标量场（[规范函数](@entry_id:749731)）。让我们看看这个变换对[场张量](@entry_id:186486)有什么影响 [@problem_id:1806929]。新的[场张量](@entry_id:186486) $F'^{\mu\nu}$ 为：

$F'^{\mu\nu} = \partial^\mu A'^\nu - \partial^\nu A'^\mu = \partial^\mu (A^\nu + \partial^\nu \chi) - \partial^\nu (A^\mu + \partial^\mu \chi)$

展开后得到：

$F'^{\mu\nu} = (\partial^\mu A^\nu - \partial^\nu A^\mu) + (\partial^\mu \partial^\nu \chi - \partial^\nu \partial^\mu \chi)$

由于[偏导数](@entry_id:146280)的求导次序可以交换（$\partial^\mu \partial^\nu = \partial^\nu \partial^\mu$），括号中的第二项恒为零。因此，我们得到了一个至关重要的结果：

$F'^{\mu\nu} = F^{\mu\nu}$

这表明[电磁场张量](@entry_id:158921)在规范变换下是**不变的**。由于所有[物理可观测量](@entry_id:154692)（如[电场](@entry_id:194326)、[磁场](@entry_id:153296)、力和能量）都只依赖于 $F^{\mu\nu}$，这意味着物理定律本身具有规范不变性。这种[不变性](@entry_id:140168)是现代规范场论的基石，而电磁理论是其最简单、最经典的原型。

### [协变](@entry_id:634097)形式的[麦克斯韦方程组](@entry_id:150940)

有了[四维势](@entry_id:188407) $A^\mu$、[四维流密度](@entry_id:262568) $J^\mu$ 和[电磁场张量](@entry_id:158921) $F^{\mu\nu}$ 这些工具，我们现在可以将四个[麦克斯韦方程组](@entry_id:150940)重写为两个异常简洁的张量方程。

#### 非[齐次方程](@entry_id:163650)与电荷守恒

包含源（[电荷](@entry_id:275494)和电流）的两个麦克斯韦方程——[高斯定律](@entry_id:141493)（$\nabla \cdot \mathbf{E} = \rho/\epsilon_0$）和[安培-麦克斯韦定律](@entry_id:266368)（$\nabla \times \mathbf{B} = \mu_0 \mathbf{J} + \mu_0 \epsilon_0 \frac{\partial \mathbf{E}}{\partial t}$）——可以被统一成一个单一的方程：

$\partial_\mu F^{\mu\nu} = \mu_0 J^\nu$

这个方程被称为**非齐次麦克斯韦方程**。其中 $\partial_\mu = \frac{\partial}{\partial x^\mu}$ 是[协变](@entry_id:634097)四维梯度算符。这是一个张量方程，因此在所有惯性系中形式相同。让我们验证它确实包含了那两个经典定律。

- **当 $\nu = 0$ 时**：
  $\partial_\mu F^{\mu 0} = \partial_0 F^{00} + \partial_i F^{i0} = \mu_0 J^0$
  代入 $F^{i0} = -F^{0i} = E_i/c$ 和 $J^0 = c\rho$，我们得到：
  $0 + \frac{\partial}{\partial x^i}(E_i/c) = \frac{1}{c} (\nabla \cdot \mathbf{E}) = \mu_0 c \rho$
  使用 $c^2 = 1/(\epsilon_0 \mu_0)$，这可以化简为 $\nabla \cdot \mathbf{E} = \rho/\epsilon_0$，即[高斯定律](@entry_id:141493)。

- **当 $\nu = j$ (例如 $j=1$) 时**：
  $\partial_\mu F^{\mu j} = \partial_0 F^{0j} + \partial_i F^{ij} = \mu_0 J^j$
  代入分量 $F^{0j} = -E_j/c$, $F^{ij} = -\epsilon_{ijk}B_k$ 和 $J^j=J_j$：
  $\frac{1}{c}\frac{\partial}{\partial t}(-E_j/c) + \frac{\partial}{\partial x^i}(-\epsilon_{ijk}B_k) = \mu_0 J_j$
  这可以整理为 $(\nabla \times \mathbf{B})_j - \frac{1}{c^2}\frac{\partial E_j}{\partial t} = \mu_0 J_j$，这正是[安培-麦克斯韦定律](@entry_id:266368)的 j 分量。

我们可以利用这个强大的方程来解决实际问题。例如，给定[电场](@entry_id:194326) $\mathbf{E} = \alpha t \hat{\mathbf{y}}$ 和[磁场](@entry_id:153296) $\mathbf{B} = \beta x \hat{\mathbf{z}}$，我们可以确定产生这个场的[电流密度](@entry_id:190690) [@problem_id:1573983]。我们需要计算 $J_y = J^2$。根据协变方程：
$\mu_0 J^2 = \partial_\mu F^{\mu 2} = \partial_0 F^{02} + \partial_1 F^{12} + \partial_3 F^{32}$
其中 $E_y=\alpha t$ and $B_z=\beta x$。所以 $F^{02} = -E_y/c = -\alpha t/c$，$F^{12} = -B_z = -\beta x$。其他相关的场分量为零。
$\mu_0 J_y = \frac{1}{c}\frac{\partial}{\partial t}(-\frac{\alpha t}{c}) + \frac{\partial}{\partial x}(-\beta x) = -\frac{\alpha}{c^2} - \beta$
因此，电流密度的 y 分量为 $J_y = -\frac{1}{\mu_0}(\frac{\alpha}{c^2} + \beta)$。

这个方程还有一个极为深刻的推论：**[电荷守恒](@entry_id:264158)**。对非[齐次方程](@entry_id:163650)两边取四维散度 $\partial_\nu$：
$\partial_\nu (\partial_\mu F^{\mu\nu}) = \mu_0 \partial_\nu J^\nu$
方程的左边是一个二阶张量 $\partial_\nu \partial_\mu F^{\mu\nu}$。由于 $\partial_\nu \partial_\mu$ 对[光滑函数](@entry_id:267124)是对称的，而 $F^{\mu\nu}$ 是反对称的，这两者缩并的结果恒为零。因此，我们必然得到：
$\mu_0 \partial_\nu J^\nu = 0 \implies \partial_\nu J^\nu = 0$
这个方程 $\partial_\nu J^\nu = \frac{\partial (c\rho)}{\partial (ct)} + \nabla \cdot \mathbf{J} = \frac{\partial\rho}{\partial t} + \nabla \cdot \mathbf{J} = 0$ 正是[电荷守恒](@entry_id:264158)的**连续性方程**。这表明，[电荷守恒](@entry_id:264158)并非一个独立的假设，而是[麦克斯韦方程组](@entry_id:150940)内在结构的必然结果。协变形式使这一点变得一目了然。如果麦克斯韦方程的形式稍有不同，电荷守恒就可能不成立 [@problem_id:1806974]。

#### [齐次方程](@entry_id:163650)与对偶张量

另外两个不含源的麦克斯韦方程——[法拉第感应定律](@entry_id:146175)（$\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$）和[高斯磁定律](@entry_id:182942)（$\nabla \cdot \mathbf{B} = 0$）——被称为**齐次麦克斯韦方程**。它们也可以被统一成一个单一的张量方程。一种方式是写出所谓的[比安基恒等式](@entry_id:261685)（Bianchi identity）：
$\partial_\lambda F_{\mu\nu} + \partial_\mu F_{\nu\lambda} + \partial_\nu F_{\lambda\mu} = 0$
这个方程之所以成立，是因为 $F_{\mu\nu}$ 可以由[四维势](@entry_id:188407) $A_\mu$ 导出（$F_{\mu\nu} = \partial_\mu A_\nu - \partial_\nu A_\mu$）。

然而，为了与非齐次方程 $\partial_\mu F^{\mu\nu} = \mu_0 J^\nu$ 形成更优美的对偶形式，我们引入**对偶[电磁场张量](@entry_id:158921)**（dual electromagnetic field tensor）$G^{\mu\nu}$。它的定义是：
$G^{\mu\nu} = \frac{1}{2} \epsilon^{\mu\nu\lambda\sigma} F_{\lambda\sigma}$
其中 $\epsilon^{\mu\nu\lambda\sigma}$ 是四维[列维-奇维塔符号](@entry_id:193594)（$\epsilon^{0123}=1$）。实际上，$G^{\mu\nu}$ 的矩阵形式可以通过对 $F^{\mu\nu}$ 进行替换 $\mathbf{E}/c \to \mathbf{B}$ 和 $\mathbf{B} \to -\mathbf{E}/c$ 来得到：
$G^{\mu\nu} = \begin{pmatrix} 0  -B_x  -B_y  -B_z \\ B_x  0  E_z/c  -E_y/c \\ B_y  -E_z/c  0  E_x/c \\ B_z  E_y/c  -E_x/c  0 \end{pmatrix}$
利用这个对偶张量，两个[齐次方程](@entry_id:163650)可以被写成一个与非[齐次方程](@entry_id:163650)形式完全对称的方程 [@problem_id:1573956]：

$\partial_\mu G^{\mu\nu} = 0$

这个方程的四维散度为零，直接对应于“磁荷”和“磁流”的密度为零。展开这个方程可以验证它确实等价于[法拉第定律](@entry_id:149836)和[高斯磁定律](@entry_id:182942)。例如，当 $\nu = 0$ 时，我们得到 $\nabla \cdot \mathbf{B} = 0$。当 $\nu = i$ 时，我们得到 $\nabla \times \mathbf{E} + \frac{\partial \mathbf{B}}{\partial t} = 0$。

综上所述，经典的四个[麦克斯韦方程组](@entry_id:150940)在协变形式下被简化为两个方程：
$\partial_\mu F^{\mu\nu} = \mu_0 J^\nu$
$\partial_\mu G^{\mu\nu} = 0$
这种表述的简洁性和对称性是惊人的，它充分展示了相对论框架下物理定律的内在和谐。

### 动力学与[不变量](@entry_id:148850)

最后，我们探讨[电磁场](@entry_id:265881)如何与带电物质相互作用，以及在洛伦兹变换下哪些关于场的量是保持不变的。

#### [协变](@entry_id:634097)[洛伦兹力](@entry_id:145104)

[电磁场](@entry_id:265881)通过洛伦兹力对[带电粒子](@entry_id:160311)施加作用。这个力学定律也有一个极其优美的协变形式。我们定义粒子的**[四维速度](@entry_id:269673)** $u^\mu = dx^\mu/d\tau = \gamma(c, \mathbf{v})$ 和**[四维动量](@entry_id:272346)** $p^\mu = m u^\mu$，其中 $\tau$ 是粒子的固有时。**[四维力](@entry_id:273918)** $f^\mu$ 定义为四维动量对固有时的一阶导数，$f^\mu = dp^\mu/d\tau$。

描述一个[电荷](@entry_id:275494)为 $q$ 的粒子在[电磁场](@entry_id:265881) $F^{\mu\nu}$ 中运动的**协变[洛伦兹力定律](@entry_id:270735)**为 [@problem_id:1573969]：

$f^\mu = q F^{\mu\nu} u_\nu$

其中 $u_\nu = \eta_{\nu\sigma}u^\sigma = \gamma(c, -\mathbf{v})$ 是[协变](@entry_id:634097)[四维速度](@entry_id:269673)。这个方程的张量形式保证了它在所有[惯性系](@entry_id:266190)下都成立。它的时间分量 $(\mu=0)$ 描述了[电磁场](@entry_id:265881)对粒子所做的功率（能量变化率），而其空间分量 $(\mu=1,2,3)$ 则给出了我们熟悉的三维[洛伦兹力](@entry_id:145104) $\mathbf{F} = q(\mathbf{E} + \mathbf{v} \times \mathbf{B})$。

#### 场的洛伦兹不变量

尽管[电场](@entry_id:194326) $\mathbf{E}$ 和[磁场](@entry_id:153296) $\mathbf{B}$ 的分量依赖于观察者的[参考系](@entry_id:169232)，但我们可以从[场张量](@entry_id:186486) $F^{\mu\nu}$ 构造出一些特殊的标量，它们的值对于所有惯性观察者都是相同的。这些量被称为**洛伦兹不变量**。有两个基本的[洛伦兹不变量](@entry_id:161821)。

第一个[不变量](@entry_id:148850)是[场张量](@entry_id:186486)与自身的完全缩并 [@problem_id:1806984]：

$S_1 = F_{\mu\nu}F^{\mu\nu} = 2\left(B^2 - \frac{E^2}{c^2}\right)$

这个量的值不随[参考系](@entry_id:169232)的改变而改变。它的符号具有明确的物理意义：
- 如果 $S_1  0$（[磁场](@entry_id:153296)占优），总可以找到一个洛伦兹变换后的[参考系](@entry_id:169232)，在该系中[电场](@entry_id:194326)为零，只存在[磁场](@entry_id:153296)。
- 如果 $S_1  0$（[电场](@entry_id:194326)占优），总可以找到一个[参考系](@entry_id:169232)，在该系中[磁场](@entry_id:153296)为零，只存在[电场](@entry_id:194326)。
- 如果 $S_1 = 0$，例如对于平面[电磁波](@entry_id:269629)，那么在任何[参考系](@entry_id:169232)中都有 $E = cB$。

第二个[不变量](@entry_id:148850)涉及到对偶张量，或者等价地，利用四维[列维-奇维塔符号](@entry_id:193594)：

$S_2 = \frac{1}{4} \epsilon^{\mu\nu\lambda\sigma} F_{\mu\nu} F_{\lambda\sigma} = -\frac{1}{c}(\mathbf{E} \cdot \mathbf{B})$

这个量也对所有惯性观察者保持不变。它告诉我们关于 $\mathbf{E}$ 场和 $\mathbf{B}$ 场相对方向的信息。
- 如果 $S_2 = 0$（即 $\mathbf{E} \cdot \mathbf{B} = 0$），那么如果 $\mathbf{E}$ 和 $\mathbf{B}$ 都不为零，它们在该[参考系](@entry_id:169232)中是相互垂直的。更重要的是，如果 $S_1 \neq 0$ 且 $S_2 = 0$，我们总能找到一个[参考系](@entry_id:169232)，使得[电场](@entry_id:194326)或[磁场](@entry_id:153296)其中一个为零。
- 如果 $S_2 \neq 0$，则在任何[参考系](@entry_id:169232)中，$\mathbf{E}$ 和 $\mathbf{B}$ 都不能同时为零，并且它们之间总有一个夹角（永远不可能平行或反平行，除非在某个场为零的特殊系中）。

这两个[不变量](@entry_id:148850)为我们提供了一种不依赖于[参考系](@entry_id:169232)的方式来刻画[电磁场](@entry_id:265881)的内在属性。

通过本章的学习，我们已经看到，采用[协变](@entry_id:634097)语言不仅仅是一种数学上的简化，它更深刻地揭示了电磁理论的内在结构，阐明了其与时空几何的密切关系，并将看似无关的物理概念统一在了一个连贯而优美的理论框架之下。