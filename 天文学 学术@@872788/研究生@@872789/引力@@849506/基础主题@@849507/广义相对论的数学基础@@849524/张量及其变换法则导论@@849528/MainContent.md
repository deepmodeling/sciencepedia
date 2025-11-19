## 引言
在物理学和数学中，一个核心的挑战是如何描述独立于观察者主观选择的客观实在。我们所使用的[坐标系](@entry_id:156346)，无论是笛卡尔坐标、[球坐标](@entry_id:146054)还是更奇特的[坐标系](@entry_id:156346)，都只是描述自然的一种工具，物理定律本身不应依赖于这些工具的选择。为了解决这一问题，数学家和物理学家发展出了一种强大的语言——张量。张量并非简单的多维数组，而是一种具有明确坐标变换规律的几何或物理对象，正是这一特性使其成为构建普适物理理论的基石。

本文旨在为读者提供一个关于张量及其变换法则的全面介绍。我们将从最基本的概念出发，逐步揭示张量理论的深度和广度。在接下来的内容中，您将学习到：

- **第一章：原理与机制**，我们将深入探讨张量的本质定义——其分量在坐标变换下的特定行为。本章将详细解释[协变与逆变](@entry_id:189600)张量、[向量与余向量](@entry_id:180712)、以及[度规张量](@entry_id:160222)等核心概念，并阐明缩并、[拉回](@entry_id:160816)与[前推](@entry_id:158718)等基本操作。

- **第二章：应用与跨学科联系**，我们将跨越不同学科，展示张量理论的强大威力。您将看到张量是如何在连续介质力学中描述应力与各向异性，如何在狭义相对论中统一[电场](@entry_id:194326)与[磁场](@entry_id:153296)，以及如何在广义相对论中描绘弯曲的[时空几何](@entry_id:139497)。

- **第三章：动手实践**，理论学习需要通过实践来巩固。本章提供了一系列精心设计的问题，引导您亲手计算张量的变换，从而将抽象的法则转化为具体的技能。

通过这趟旅程，您将不仅掌握一个数学工具，更将领会一种深刻的物理思想，即如何以一种真正普适和内在的方式来理解我们所处的宇宙。

## 原理与机制

在物理学和数学中，为了摆脱对特定[坐标系](@entry_id:156346)的依赖，发展一套能够描述内在几何或物理规律的语言至关重要。张量（tensor）正是为此而生的数学对象。本章将深入探讨张量的核心定义、其在[坐标变换](@entry_id:172727)下的行为，以及相关的基本操作。我们不再将张量仅仅看作是“多维数组”，而是将其理解为在[流形](@entry_id:153038)上具有明确变换规律的几何实体。

### 什么是张量？坐标变换法则

从根本上说，一个**张量 (tensor)** 是一个几何或物理对象，它独立于任何用于描述它的[坐标系](@entry_id:156346)而存在。然而，当我们选择一个特定的[坐标系](@entry_id:156346)来“测量”或“表示”这个张量时，我们会得到一组数值，称为张量的**分量 (components)**。如果我们更换[坐标系](@entry_id:156346)，这些分量会以一种精确且可预测的方式改变。这种独特的变换规则，正是张量的定义性特征。

让我们以一个核心几何对象——**度规张量 (metric tensor)** $g$ 为例来阐明这一思想 [@problem_id:2983138]。度规张量 $g$ 是一个内在的、坐标无关的场，它在[流形](@entry_id:153038)的每一点 $p$ 的[切空间](@entry_id:199137) $T_p M$ 上定义了一个[内积](@entry_id:158127)（或[点积](@entry_id:149019)）。这个[内积](@entry_id:158127)使我们能够测量[切向量](@entry_id:265494)的长度以及它们之间的角度。这个张量本身 $g$ 是一个抽象的几何实体。

为了用数字来描述它，我们必须引入一个[坐标系](@entry_id:156346)。在一个[局部坐标](@entry_id:181200)图 $(U, x)$ 中，坐标为 $x = (x^1, \dots, x^n)$，在每一点 $p \in U$ 的切空间 $T_p M$ 中，我们有一组自然基底向量 $\{\frac{\partial}{\partial x^i}\big|_p\}$。度规张量在这一基底下的分量 $g_{ij}$ 通过计算基底向量之间的[内积](@entry_id:158127)得到：
$$
g_{ij}(p) = g_p\left(\frac{\partial}{\partial x^i}\bigg|_p, \frac{\partial}{\partial x^j}\bigg|_p\right)
$$
这些分量 $g_{ij}$ 是定义在 $U$ 上的 $n \times n$ 个光滑函数的集合，它们共同构成了度规张量 $g$ 在 $x$ [坐标系](@entry_id:156346)下的**坐标表示 (coordinate representation)**。

现在，假设我们切换到另一个[坐标系](@entry_id:156346) $(V, y)$，其坐标为 $y = (y^1, \dots, y^n)$。在重叠区域 $U \cap V$ 中，我们有另一组基底向量 $\{\frac{\partial}{\partial y^\alpha}\big|_p\}$，以及另一组分量 $g'_{\alpha\beta}$：
$$
g'_{\alpha\beta}(p) = g_p\left(\frac{\partial}{\partial y^\alpha}\bigg|_p, \frac{\partial}{\partial y^\beta}\bigg|_p\right)
$$
由于 $g$ 本身是同一个几何对象，这两组分量必然是相关的。根据多元微积分的链式法则，两组基底向量之间存在如下关系：
$$
\frac{\partial}{\partial y^\alpha} = \sum_{i=1}^n \frac{\partial x^i}{\partial y^\alpha} \frac{\partial}{\partial x^i}
$$
我们将此关系代入 $g'_{\alpha\beta}$ 的定义中，并利用 $g_p$ 的[双线性性](@entry_id:146819)质：
$$
\begin{align}
g'_{\alpha\beta} & = g_p\left( \sum_{i=1}^n \frac{\partial x^i}{\partial y^\alpha} \frac{\partial}{\partial x^i}, \sum_{j=1}^n \frac{\partial x^j}{\partial y^\beta} \frac{\partial}{\partial x^j} \right) \\
& = \sum_{i,j=1}^n \frac{\partial x^i}{\partial y^\alpha} \frac{\partial x^j}{\partial y^\beta} g_p\left( \frac{\partial}{\partial x^i}, \frac{\partial}{\partial x^j} \right) \\
& = \sum_{i,j=1}^n \frac{\partial x^i}{\partial y^\alpha} \frac{\partial x^j}{\partial y^\beta} g_{ij}
\end{align}
$$
（在[张量分析](@entry_id:161423)中，我们通常使用**爱因斯坦求和约定 (Einstein summation convention)**，即当一个指标在一个单项式中同时出现为上、下标时，表示对该指标的所有可能值求和。这样，上述公式可以简洁地写为 $g'_{\alpha\beta} = \frac{\partial x^i}{\partial y^\alpha} \frac{\partial x^j}{\partial y^\beta} g_{ij}$。）

这个公式就是 $(0,2)$ 型**[协变张量](@entry_id:634493) (covariant tensor)** 的变换法则。这里的“[协变](@entry_id:634097)”指的是分量的变换矩阵是坐标变换[雅可比矩阵](@entry_id:264467)的逆矩阵（因为 $\frac{\partial x^i}{\partial y^\alpha}$ 是从 $y$ 到 $x$ 的[变换矩阵](@entry_id:151616)的元素，即 $x(y)$ 变换的[雅可比矩阵](@entry_id:264467)）。

这个例子完美地体现了张量的本质 [@problem_id:2983138]：
1.  张量 $g$ 是一个内在的、坐标无关的几何对象。
2.  它的分量 $g_{ij}$ 和 $g'_{\alpha\beta}$ 是坐标依赖的，因为它们是通过张量作用于特定[坐标系](@entry_id:156346)的基底向量得到的。
3.  不同[坐标系](@entry_id:156346)下的分量通过一个普适的变换法则联系在一起。

一般地，一个 $(r,s)$ 型张量 $T$ 在[坐标变换](@entry_id:172727)下的分量变换法则是：
$$
T'^{k_1 \dots k_r}_{l_1 \dots l_s} = \left(\frac{\partial y^{k_1}}{\partial x^{i_1}} \cdots \frac{\partial y^{k_r}}{\partial x^{i_r}}\right) \left(\frac{\partial x^{j_1}}{\partial y^{l_1}} \cdots \frac{\partial x^{j_s}}{\partial y^{l_s}}\right) T^{i_1 \dots i_r}_{j_1 \dots j_s}
$$
这里有 $r$ 个**[逆变](@entry_id:192290) (contravariant)** 指标（上指标）和 $s$ 个**协变 (covariant)** 指标（下指标）。逆变指标的[变换矩阵](@entry_id:151616)为 $\frac{\partial y^k}{\partial x^i}$（从 $x$ 到 $y$ 的[雅可比矩阵](@entry_id:264467)），而协变指标的[变换矩阵](@entry_id:151616)为 $\frac{\partial x^j}{\partial y^l}$（[雅可比矩阵](@entry_id:264467)的[逆矩阵](@entry_id:140380)）。

一个至关重要的推论是，当一个张量的所有上、下指标都通过与另一个张量的分量相乘并求和（称为**缩并 (contraction)**）而被“饱和”时，其结果是一个**标量 (scalar)**，即一个 $(0,0)$ 型张量。标量在坐标变换下是不变的。例如，给定一个[切向量](@entry_id:265494) $v = v^i \frac{\partial}{\partial x^i} = v'^\alpha \frac{\partial}{\partial y^\alpha}$，它自身的长度平方是一个标量，其值不应依赖于[坐标系](@entry_id:156346)。计算表明 [@problem_id:2983138]：
$$
g_p(v,v) = g_{ij}(p) v^i v^j = g'_{\alpha\beta}(p) v'^\alpha v'^\beta
$$
尽管 $g_{ij}$ 和 $v^i$ 都随[坐标系](@entry_id:156346)改变，但它们的组合 $g_{ij} v^i v^j$ 保持不变。这正是物理定律要求具有的形式——它们所描述的物理实在必须独立于观察者选择的[坐标系](@entry_id:156346)。

### 向量、余向量及其变换

最简单也最基本的张量是[向量和余向量](@entry_id:181128)。

#### 向量（[逆变张量](@entry_id:636697)）

一个**[切向量](@entry_id:265494) (tangent vector)** 或简称**向量**，是一个 $(1,0)$ 型张量。它的分量 $V^i$ 在坐标变换下遵循逆变法则：
$$
V'^\alpha = \frac{\partial y^\alpha}{\partial x^i} V^i
$$
这个法则源于向量自身的[坐标无关性](@entry_id:159715)。一个向量 $V$ 可以表示为基底的[线性组合](@entry_id:154743)，这个表示必须在所有[坐标系](@entry_id:156346)下都成立：
$$
V = V^i \frac{\partial}{\partial x^i} = V'^\alpha \frac{\partial}{\partial y^\alpha}
$$
将基底变换关系 $\frac{\partial}{\partial y^\alpha} = \frac{\partial x^i}{\partial y^\alpha} \frac{\partial}{\partial x^i}$ 代入，我们得到 $V = V'^\alpha \frac{\partial x^i}{\partial y^\alpha} \frac{\partial}{\partial x^i}$。通过与 $V = V^i \frac{\partial}{\partial x^i}$ 比较系数，并乘以[雅可比矩阵](@entry_id:264467) $\frac{\partial y^\beta}{\partial x^i}$，即可得到上述变换法则。

与向量变换密切相关的一个概念是**[前推](@entry_id:158718) (pushforward)**。给定一个[光滑映射](@entry_id:203730) $\Phi: M \to N$，它将点从[流形](@entry_id:153038) $M$ 映到[流形](@entry_id:153038) $N$。这个映射自然地诱导了一个在它们切空间之间的[线性映射](@entry_id:185132) $(\Phi_*)_p: T_p M \to T_{\Phi(p)} N$，称为[前推](@entry_id:158718)。如果 $V$ 是 $M$ 上的一个向量场，它的[前推](@entry_id:158718) $(\Phi_*)V$ 就是 $N$ 上的一个向量场。计算[前推](@entry_id:158718)向量场的分量，是理解[向量变换法则](@entry_id:182717)的一个具体实践。

例如，考虑复平面 $\mathbb{C}^*$ 上的复数[反演映射](@entry_id:168169) $\Phi(z) = 1/z$ [@problem_id:897765]。我们可以在源空间和目标空间都使用极坐标，源坐标为 $(r, \theta)$，目标坐标为 $(\rho, \phi)$。映射关系为 $\rho = 1/r, \phi = -\theta$。给定源空间中的一个向量场 $V = r^p \partial_r + q \partial_\theta$，其[前推](@entry_id:158718)向量场 $(\Phi_*)V = W^\rho \partial_\rho + W^\phi \partial_\phi$ 的分量可以通过[链式法则](@entry_id:190743)计算：
$$
W^\rho = (\Phi_*)V (\rho) = V(\rho \circ \Phi) = V(1/r) = (r^p \partial_r + q \partial_\theta)(r^{-1}) = -r^{p-2} = -\rho^{2-p}
$$
$$
W^\phi = (\Phi_*)V (\phi) = V(\phi \circ \Phi) = V(-\theta) = (r^p \partial_r + q \partial_\theta)(-\theta) = -q
$$
这个计算清晰地展示了如何将一个向量场从一个空间“推”到另一个空间，并得到其在新[坐标系](@entry_id:156346)下的表示。

#### 余向量（[协变张量](@entry_id:634493)）

与向量对偶的概念是**余切向量 (cotangent vector)**，也称为**余向量 (covector)** 或**1-形式 (1-form)**。它是一个 $(0,1)$ 型张量。其分量 $\omega_i$ 在坐标变换下遵循协变法则：
$$
\omega'_\alpha = \frac{\partial x^i}{\partial y^\alpha} \omega_i
$$
最典型的[余向量](@entry_id:157727)是[标量场](@entry_id:151443) $\phi$ 的梯度。在 $x$ [坐标系](@entry_id:156346)下，其分量为 $\frac{\partial\phi}{\partial x^i}$。在 $y$ [坐标系](@entry_id:156346)下，分量为 $\frac{\partial\phi}{\partial y^\alpha}$。根据[链式法则](@entry_id:190743)，它们的关系是：
$$
\frac{\partial\phi}{\partial y^\alpha} = \frac{\partial x^i}{\partial y^\alpha} \frac{\partial\phi}{\partial x^i}
$$
这正是 $(0,1)$ 型张量的变换法则。

与[前推](@entry_id:158718)对偶的操作是**[拉回](@entry_id:160816) (pullback)**。一个[光滑映射](@entry_id:203730) $\Phi: M \to N$ 可以将 $N$ 上的[余向量](@entry_id:157727)（或更高阶的[协变张量](@entry_id:634493)）“[拉回](@entry_id:160816)”到 $M$ 上，得到 $M$ 上的一个对应张量。设 $g$ 是 $N$ 上的一个 $(0,2)$ 型[协变张量](@entry_id:634493)（例如[度规张量](@entry_id:160222)），其[拉回](@entry_id:160816) $\tilde{g} = \Phi^*g$ 在 $M$ 上的分量由下式给出：
$$
\tilde{g}_{\alpha\beta}(p) = g_{ij}(\Phi(p)) \frac{\partial \Phi^i}{\partial x^\alpha} \frac{\partial \Phi^j}{\partial x^\beta}
$$
这里 $x^\alpha$ 是 $M$ 上的坐标，$\Phi^i$ 是 $N$ 上的坐标。

一个极具启发性的例子是球极投影 [@problem_id:897750]。这是一个从[二维球面](@entry_id:269890) $S^2$（除去北极点）到其赤道平面的映射 $\Phi: S^2 \setminus \{N\} \to \mathbb{R}^2$。球面本身具有由其在三维[欧氏空间](@entry_id:138052)中的嵌入所诱导的**标[准圆](@entry_id:175119)形度规 (round metric)** $g$。通过[拉回](@entry_id:160816)操作，我们可以在原本平直的 $\mathbb{R}^2$ 平面上得到一个新的度规 $\tilde{g} = \Phi^*g$。计算表明，这个新的度规在平面坐标 $(x,y)$ 下的形式为：
$$
\tilde{g}_{ij} = \left( \frac{2R^2}{x^2+y^2+R^2} \right)^2 \delta_{ij}
$$
其中 $R$ 是球半径，$\delta_{ij}$ 是欧氏度规。这表明，平直的欧氏平面通过球极投影，被赋予了一个弯曲的几何结构。这揭示了度规张量作为几何结构描述者的深刻作用，也具体展示了[协变张量](@entry_id:634493)的[拉回](@entry_id:160816)变换机制。

### 张量的抽象形式化定义

迄今为止，我们主要通过分量的变换法则来定义张量。这是一种操作性定义，非常实用。然而，现代[微分几何](@entry_id:145818)提供了一种更抽象、更内在的定义，它完全不依赖于[坐标系](@entry_id:156346)。

一个 $(r,s)$ 型张量 $T$ 在[流形](@entry_id:153038)上的一点 $p$ 可以被定义为一个[多重线性映射](@entry_id:274221) [@problem_id:2992314]：
$$
T_p: \underbrace{T_p^*M \times \dots \times T_p^*M}_{r \text{ 个}} \times \underbrace{T_pM \times \dots \times T_pM}_{s \text{ 个}} \to \mathbb{R}
$$
这个映射接收 $r$ 个余向量和 $s$ 个向量作为输入，并输出一个实数，且对每一个输入参数都是线性的。这个定义是完全坐标无关的。它与我们之前的分量定义是等价的：张量的分量 $T^{i_1 \dots i_r}_{j_1 \dots j_s}$ 正是这个[多重线性映射](@entry_id:274221)作用在基底向量和基底[余向量](@entry_id:157727)上的结果：
$$
T^{i_1 \dots i_r}_{j_1 \dots j_s} = T_p(dx^{i_1}, \dots, dx^{i_r}, \frac{\partial}{\partial x^{j_1}}, \dots, \frac{\partial}{\partial x^{j_s}})
$$

将所有点 $p \in M$ 的 $(r,s)$ 型张量空间 $T_p^{r,s}M$ 汇集在一起，就构成了一个称为**[张量丛](@entry_id:203012) (tensor bundle)** $\mathrm{T}^{r,s}M$ 的几何结构。这是一个以 $M$ 为基底空间的向量丛。而一个 $(r,s)$ 型**[张量场](@entry_id:190170) (tensor field)** 就是这个[张量丛](@entry_id:203012)的一个**光滑[截面](@entry_id:154995) (smooth section)** [@problem_id:2992314]。这意味着一个[张量场](@entry_id:190170) $T$ 是一个映射 $T: M \to \mathrm{T}^{r,s}M$，它为[流形](@entry_id:153038)上的每一点 $p$ 指定该点的一个张量 $T_p$，并且这种指定是“光滑”变化的。

“光滑”这个要求至关重要。在[微分几何](@entry_id:145818)中，我们希望能够对[张量场](@entry_id:190170)进行[微分](@entry_id:158718)运算（如协变导数），这要求场本身是足够光滑的。一个张量场 $T$ 是光滑的，当且仅当对于任意光滑的向量场 $X_1, \dots, X_s$ 和光滑的[余向量](@entry_id:157727)场 $\omega^1, \dots, \omega^r$，标量函数 $p \mapsto T_p(\omega^1_p, \dots, \omega^r_p, X_{1,p}, \dots, X_{s,p})$ 在整个[流形](@entry_id:153038) $M$ 上是光滑的 [@problem_id:2992314]。这个判据为我们提供了一个不依赖于坐标来验证张量场光滑性的方法。

### [主动变换与被动变换](@entry_id:175638)

在讨论变换时，区分两种视角至关重要：**被动变换 (passive transformations)** 和**主动变换 (active transformations)**。

到目前为止我们讨论的坐标变换都属于被动变换。在这种视角下，物理系统或几何对象是固定的，我们只是改变了描述它的[坐标系](@entry_id:156346)。向量、基底和张量分量都改变了它们的[数值表示](@entry_id:138287)，但底层的几何实体保持不变。

而在主动变换中，[坐标系](@entry_id:156346)是固定的，物理系统本身被移动或变形。例如，对一个系统进行整体旋转。在这种情况下，我们是在比较同一个[坐标系](@entry_id:156346)中，变换前后的不同张量场。

考虑一个由对称 $(2,0)$ 型[张量场](@entry_id:190170) $T^{ij}$ 描述的物理系统 [@problem_id:897832]。在笛卡尔坐标系 $(x,y,z)$ 中，该场有特定分量。现在，我们将整个系统绕 $y$ 轴逆时针旋转一个角度 $\theta$。一个原先位于点 $\vec{x}$ 的物理点被移动到新位置 $\vec{x}' = R\vec{x}$，其中 $R$ 是[旋转矩阵](@entry_id:140302)。变换后的新[张量场](@entry_id:190170) $T'$ 在新点 $\vec{x}'$ 的值，是原张量场在旧点 $\vec{x}$ 的值经过[旋转变换](@entry_id:200017)得到的：
$$
T'^{ij}(\vec{x}') = R^i_{\;k} R^j_{\;l} T^{kl}(\vec{x})
$$
这是一个主动变换的法则。我们需要计算在固定[坐标系](@entry_id:156346)中，新张量场 $T'$ 在某个点 $P_0$ 的分量。这意味着 $\vec{x}' = P_0$，而我们需要用原[张量场](@entry_id:190170)在变换前的对应点 $\vec{x} = R^{-1} P_0$ 的值来计算。这是一个涉及坐标代换和[张量变换法则](@entry_id:185176)的综合计算。通过这样的计算，我们可以分析物理系统在经历实际的物理运动（如旋转）后，其张量描述会如何演变。

### 类张量对象

除了严格意义上的张量，物理学和几何学中还存在一些在[坐标变换](@entry_id:172727)下行为类似但有细微差别的对象。理解它们与真张量的区别同样重要。

#### 非张量性量

并非所有带指标的量都是张量。一个典型的例子是标量场 $\phi$ 的[二阶偏导数](@entry_id:635213) $\frac{\partial^2 \phi}{\partial x'^\alpha \partial x'^\beta}$。如果我们天真地应用[张量变换法则](@entry_id:185176)，会发现它并不成立。让我们从一阶导数的变换法则 $\frac{\partial \phi}{\partial x'^\beta} = \frac{\partial x^\nu}{\partial x'^\beta} \frac{\partial \phi}{\partial x^\nu}$ 出发，再对它求一次导数 [@problem_id:897759]：
$$
\begin{align}
\frac{\partial^2 \phi}{\partial x'^\alpha \partial x'^\beta} & = \frac{\partial}{\partial x'^\alpha} \left( \frac{\partial x^\nu}{\partial x'^\beta} \frac{\partial \phi}{\partial x^\nu} \right) \\
& = \left( \frac{\partial^2 x^\nu}{\partial x'^\alpha \partial x'^\beta} \right) \frac{\partial \phi}{\partial x^\nu} + \left( \frac{\partial x^\nu}{\partial x'^\beta} \right) \left( \frac{\partial}{\partial x'^\alpha} \frac{\partial \phi}{\partial x^\nu} \right) \\
& = \frac{\partial^2 x^\nu}{\partial x'^\alpha \partial x'^\beta} \frac{\partial \phi}{\partial x^\nu} + \frac{\partial x^\mu}{\partial x'^\alpha} \frac{\partial x^\nu}{\partial x'^\beta} \frac{\partial^2 \phi}{\partial x^\mu \partial x^\nu}
\end{align}
$$
变换后的结果包含两项。第二项 $\frac{\partial x^\mu}{\partial x'^\alpha} \frac{\partial x^\nu}{\partial x'^\beta} \frac{\partial^2 \phi}{\partial x^\mu \partial x^\nu}$ 正是 $(0,2)$ 型张量所期望的变换形式。然而，第一项 $\frac{\partial^2 x^\nu}{\partial x'^\alpha \partial x'^\beta} \frac{\partial \phi}{\partial x^\nu}$ 是一个额外的“杂项”，它使得[二阶偏导数](@entry_id:635213)整体不具有张量性。这个非张量项的存在，根源于[坐标基](@entry_id:270149)底向量自身在空间中的变化。在后续章节中我们将看到，引入**[协变导数](@entry_id:152476) (covariant derivative)** 的主要动机之一，就是为了修正普通导数，使其作用在张量上能产生一个新的张量。[协变导数](@entry_id:152476)中引入的**[克里斯托费尔符号](@entry_id:159831) (Christoffel symbols)** 正是用来抵消这个非张量项的。

#### [赝张量](@entry_id:193048)

另一类重要的类张量对象是**[赝张量](@entry_id:193048) (pseudotensor)**，有时也称为[张量密度](@entry_id:191194)。它的变换法则与真张量非常相似，但额外乘上了一个因子，即坐标变换雅可比矩阵[行列式](@entry_id:142978)的符号 $\text{sgn}(\det(J))$，或者在某些约定下是[行列式](@entry_id:142978)本身。

最著名的[赝张量](@entry_id:193048)是**[列维-奇维塔符号](@entry_id:193594) (Levi-Civita symbol)** $\epsilon_{ijk}$ [@problem_id:897834]。在三维[欧氏空间](@entry_id:138052)中，我们定义 $\epsilon_{123}=+1$，并且它在任意两个指标的交换下是全反对称的。现在考虑一个**[宇称变换](@entry_id:159187) (parity transformation)**，即空间反演 $x'^a = -x^a$。这个变换将一个[右手坐标系](@entry_id:166669)映为一个左手[坐标系](@entry_id:156346)。该变换的[雅可比矩阵](@entry_id:264467)是 $J^a_i = \frac{\partial x'^a}{\partial x^i} = -\delta^a_i$，其[逆矩阵](@entry_id:140380)的元素为 $\frac{\partial x^i}{\partial x'^a} = -\delta^i_a$。此逆[矩阵的[行列](@entry_id:148198)式](@entry_id:142978)为 $\det(-\mathbb{I}) = (-1)^3 = -1$。

如果一个量 $T_{ijk}$ 是一个真正的 $(0,3)$ 型[协变张量](@entry_id:634493)，其分量变换为：
$$
T'_{abc} = \frac{\partial x^i}{\partial x'^a} \frac{\partial x^j}{\partial x'^b} \frac{\partial x^k}{\partial x'^c} T_{ijk} = (-1)^3 T_{abc} = -T_{abc}
$$
然而，如果一个量 $P_{ijk}$ 是一个[协变](@entry_id:634097)[赝张量](@entry_id:193048)，其变换法则包含[行列式因子](@entry_id:154584)：
$$
P'_{abc} = \det\left(\frac{\partial x^l}{\partial x'^m}\right) \frac{\partial x^i}{\partial x'^a} \frac{\partial x^j}{\partial x'^b} \frac{\partial x^k}{\partial x'^c} P_{ijk} = (-1) \cdot (-1)^3 P_{abc} = +P_{abc}
$$
若取 $T_{ijk} = P_{ijk} = \epsilon_{ijk}$，我们发现，在空间反演下，$T'_{abc} = -\epsilon_{abc}$，而 $P'_{abc} = +\epsilon_{abc}$。这表明[列维-奇维塔符号](@entry_id:193594)是一个[赝张量](@entry_id:193048)。它的分量在从[右手系](@entry_id:166669)到左手系的变换中保持不变。这解释了为什么像角动量和[磁场](@entry_id:153296)（它们是[轴矢量](@entry_id:196296)，或称赝矢量）这样的物理量在空间反射下的行为与像速度和[电场](@entry_id:194326)（它们是[极矢量](@entry_id:184542)，或称[真矢量](@entry_id:190731)）这样的量不同。[体积元](@entry_id:267802)也具有[赝张量](@entry_id:193048)性质，这保证了无论我们使用左手系还是[右手系](@entry_id:166669)，计算出的体积总是正的。

掌握张量及其相关对象的变换法则是构建坐标无关物理理论的基石。它确保了我们写下的方程所描述的物理规律是普适的，不因观察者的主观选择而改变。在此基础上，下一步便是研究如何在保持张量性的前提下对它们进行[微分](@entry_id:158718)，这将引导我们进入[协变导数](@entry_id:152476)和曲率的领域。