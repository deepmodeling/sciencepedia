## 引言
在经典力学的广阔领域中，[非完整系统](@entry_id:173158)（Nonholonomic Systems）占据了一个独特而深刻的位置。与那些运动仅受限于位形空间[子流形](@entry_id:159439)的完整系统不同，[非完整系统](@entry_id:173158)的运动受到不可积分的速度约束，这导致了其运动学和动力学行为的极大丰富。从自行车的稳定行驶到卫星的姿态调整，再到微观世界中游泳微生物的运动，非完整现象无处不在，理解其背后的力学原理对于现代工程与科学至关重要。

然而，从直观的物理约束（如“无滑动滚动”）到其复杂的动力学后果（如对称性下的动量不守恒）之间，存在着一条概念上的鸿沟。本文旨在弥合这一鸿沟，以两个经典范例——滚动的圆盘和竖立的硬币——为线索，系统地揭示[非完整系统](@entry_id:173158)的内在几何结构。读者将跟随本文的脉络，从三个层面逐步深入：第一章“原理与机制”将奠定基础，详细阐述如何从物理约束出发，构建起[约束分布](@entry_id:1122944)、李括号和联络曲率等核心数学模型；第二章“应用与交叉学科联系”将展示这些抽象理论在[机器人运动规划](@entry_id:162933)、控制理论和[稳定性分析](@entry_id:144077)中的强大应用价值；最后，在“动手实践”部分，通过精选的计算问题，读者将有机会亲手验证和应用所学知识。

通过这一结构化的学习路径，本文将带领读者穿越经典力学、[微分几何](@entry_id:145818)与[控制论](@entry_id:262536)的交叉地带，最终掌握分析和理解[非完整系统](@entry_id:173158)的现代理论工具。现在，让我们首先进入第一章，深入探索[非完整系统](@entry_id:173158)的基本原理与力学机制。

## 原理与机制

在介绍性章节之后，我们现在深入探讨[非完整系统](@entry_id:173158)的核心原理和力学机制。本章将以两个经典范例——竖立滚动的圆盘和竖立的硬币——为载体，系统地阐述如何从物理约束出发，建立数学模型，并运用几何力学的语言来分析其独特的运动学和动力学行为。我们将从构型与约束的定义开始，逐步过渡到分布、可积性、[对称性破缺](@entry_id:158994)，最终抵达[联络与曲率](@entry_id:158520)的深刻几何图像。

### 系统的定义：构型与约束

描述一个力学系统的第一步是确定其所有可能状态，即其**构型流形 (configuration manifold)** $Q$，然后明确限制其运动的规则，即**约束 (constraints)**。

#### 竖立滚动的圆盘

我们首先考虑一个半径为 $R$ 的薄圆盘，它在水平面上保持竖立姿态滚动。为了完全确定其状态，我们需要以下信息：

1.  **位置**：圆盘中心在平面上的位置，由[笛卡尔坐标](@entry_id:167698) $(x, y)$ 描述。
2.  **朝向**：圆盘平面的方向，由其与 $x$ 轴的夹角 $\theta$（称为**航向角 (heading angle)** 或偏航角）定义。
3.  **自转**：圆盘绕其自身[对称轴](@entry_id:177299)滚动的角度 $\phi$（称为**自旋角 (spin angle)**）。

因此，该系统的构型流形为 $Q = \mathbb{R}^2 \times S^1 \times S^1$，由[广义坐标](@entry_id:156576) $q = (x, y, \theta, \phi)$ [参数化](@entry_id:265163) 。

此系统的关键在于“无滑动滚动”这一物理约束。该约束意味着在接触点处，圆盘相对于平面的[瞬时速度](@entry_id:167797)为零。这是一个运动学约束，因为它关联了系统各部分的速度。我们可以通过严格的[运动学分析](@entry_id:1126917)来导出其数学表达式 。

令圆盘中心 $C$ 的位置矢量为 $\mathbf{r}_C = x\mathbf{e}_x + y\mathbf{e}_y + R\mathbf{e}_z$，其速度为 $\mathbf{v}_C = \dot{x}\mathbf{e}_x + \dot{y}\mathbf{e}_y$。从中心指向接触点 $P$ 的矢量为 $\mathbf{r}_{PC} = -R\mathbf{e}_z$。圆盘的角速度 $\boldsymbol{\omega}$ 是两个运动的叠加：绕竖直轴 $\mathbf{e}_z$ 的变向运动（[角速度](@entry_id:192539)为 $\dot{\theta}$）和绕自身车轴的自旋运动（[角速度](@entry_id:192539)为 $\dot{\phi}$）。车轴的方向由航向角 $\theta$ 决定，为 $\mathbf{n}(\theta) = -\sin\theta \mathbf{e}_x + \cos\theta \mathbf{e}_y$。因此，总角速度为：
$$
\boldsymbol{\omega} = \dot{\theta}\mathbf{e}_z + \dot{\phi}\mathbf{n}(\theta) = -\dot{\phi}\sin\theta \mathbf{e}_x + \dot{\phi}\cos\theta \mathbf{e}_y + \dot{\theta}\mathbf{e}_z
$$
根据[刚体运动学](@entry_id:203362)，接触点 $P$ 的速度为 $\mathbf{v}_P = \mathbf{v}_C + \boldsymbol{\omega} \times \mathbf{r}_{PC}$。无滑动条件要求 $\mathbf{v}_P = \mathbf{0}$。计算叉积：
$$
\boldsymbol{\omega} \times \mathbf{r}_{PC} = (-\dot{\phi}\sin\theta \mathbf{e}_x + \dot{\phi}\cos\theta \mathbf{e}_y + \dot{\theta}\mathbf{e}_z) \times (-R\mathbf{e}_z) = -R\dot{\phi}\cos\theta \mathbf{e}_x - R\dot{\phi}\sin\theta \mathbf{e}_y
$$
将此结果代入 $\mathbf{v}_P = \mathbf{0}$ 的表达式中，我们得到：
$$
(\dot{x} - R\dot{\phi}\cos\theta)\mathbf{e}_x + (\dot{y} - R\dot{\phi}\sin\theta)\mathbf{e}_y = \mathbf{0}
$$
由于[基矢](@entry_id:199546)量 $\mathbf{e}_x$ 和 $\mathbf{e}_y$ [线性无关](@entry_id:148207)，其系数必须为零。这便给出了两个**[非完整约束](@entry_id:167828)方程 (nonholonomic constraint equations)**：
$$
\dot{x} - R\dot{\phi}\cos\theta = 0
$$
$$
\dot{y} - R\dot{\phi}\sin\theta = 0
$$
这两个方程限制了系统的[瞬时速度](@entry_id:167797)，但它们本身无法被积分为仅涉及坐标 $(x, y, \theta, \phi)$ 的代数方程。这正是[非完整约束](@entry_id:167828)的核心特征。

#### 简化模型：竖立的硬币

为了更清晰地分离和研究非完整约束的本质，我们常常考虑一个更简单的模型——**竖立的硬币 (vertical coin)**，有时也称为**[查普雷金雪橇](@entry_id:1122269) (Chaplygin sleigh)**。在这个模型中，我们忽略圆盘的自旋角 $\phi$ 及其相关的动力学，只关注方向性约束。这等价于一个只能沿着其边缘方向移动的刀锋。

其构型流形简化为 $Q = \mathbb{R}^2 \times S^1$，由坐标 $(x, y, \theta)$ 描述 。唯一的约束是“刀锋约束”：不允许侧向滑动。这意味着[速度矢量](@entry_id:269648) $(\dot{x}, \dot{y})$ 必须与硬币的航向矢量 $(\cos\theta, \sin\theta)$ 平行。换言之，速度矢量在与航向垂直的**侧向 (lateral direction)** $(-\sin\theta, \cos\theta)$ 上的投影必须为零。
$$
(\dot{x}, \dot{y}) \cdot (-\sin\theta, \cos\theta) = 0
$$
这给出了单个非完整约束方程：
$$
-\sin\theta \dot{x} + \cos\theta \dot{y} = 0
$$

### [几何力学](@entry_id:169959)语言：分布与普法夫形式

几何力学提供了一套强有力的语言来描述和分析约束。其中，线性速度约束被优美地编码为[微分](@entry_id:158422)一形式（或普法夫形式）。

#### 速度约束作为普法夫形式

一个关于[广义速度](@entry_id:178456) $\dot{q}$ 的[线性方程](@entry_id:151487)，如 $\sum_i A_i(q)\dot{q}^i = 0$，可以被看作是一个**一形式 (one-form)** $\omega = \sum_i A_i(q)dq^i$ 对速度矢量 $v = \sum_i \dot{q}^i \frac{\partial}{\partial q^i}$ 的作用 $\omega(v) = 0$。

对于竖立的硬币，其约束 $-\sin\theta \dot{x} + \cos\theta \dot{y} = 0$ 可以表示为一形式 $\omega = -\sin\theta dx + \cos\theta dy$ 对速度矢量的零化  。

对于竖立滚动的圆盘，两个[约束方程](@entry_id:138140)可以重新整理并写成两个一形式。将 $\dot{x}$ 和 $\dot{y}$ 的表达式 $\dot{x} = R\dot{\phi}\cos\theta$ 和 $\dot{y} = R\dot{\phi}\sin\theta$ 转化为齐次形式，我们得到：
$$
\omega^1 = dx - R\cos\theta d\phi = 0
$$
$$
\omega^2 = dy - R\sin\theta d\phi = 0
$$
任何满足滚动约束的速度矢量都必须被这两个一形式同时零化 。

#### 容许运动与[约束分布](@entry_id:1122944)

在构型流形 $Q$ 的每一点 $q$，所有满足约束的[速度矢量](@entry_id:269648)构成该点[切空间](@entry_id:199137) $T_qQ$ 的一个[线性子空间](@entry_id:151815)。所有这些子空间的集合构成了一个**分布 (distribution)**，记为 $D$。也就是说，$D_q = \{v \in T_qQ \mid \omega^i(v) = 0, \forall i\}$。这个分布 $D$ 恰好是容许运动的[瞬时速度](@entry_id:167797)空间。

对于竖立的硬币，$Q$ 是三维的，约束只有一个，因此 $D$ 是一个二维分布（秩为2）。对于滚动的圆盘，$Q$ 是四维的，约束有两个，因此 $D$ 也是一个二维分布。

我们可以为这个分布找到一组基矢量场。对于滚动的圆盘，其分布 $D$ 由满足 $\omega^1(v)=0$ 和 $\omega^2(v)=0$ 的矢量场张成。不难验证，以下两个矢量场构成 $D$ 的一组基  ：
$$
X_\theta = \frac{\partial}{\partial\theta}
$$
$$
X_\phi = R\cos\theta \frac{\partial}{\partial x} + R\sin\theta \frac{\partial}{\partial y} + \frac{\partial}{\partial\phi}
$$
$X_\theta$ 描述了原地转动航向角的运动，而 $X_\phi$ 描述了纯粹向前滚动的运动。任何容许的运动都是这两个基本运动的线性组合。

### 可积性与[和乐](@entry_id:137051)：[非完整系统](@entry_id:173158)的本质

“非完整”的真正含义在于约束是否限制了系统可到达的构型。这与[约束分布](@entry_id:1122944)的几何性质——**可积性 (integrability)** ——紧密相关。

#### 完整约束与[非完整约束](@entry_id:167828)

**完整约束 (Holonomic constraint)** 是指一个速度约束可以被积分为一个纯粹关于构型坐标的[代数方程](@entry_id:272665)，例如 $f(q) = 0$。这种约束将系统的运动限制在构型流形 $Q$ 的一个低维**[子流形](@entry_id:159439)** $S = \{q \in Q \mid f(q) = 0\}$ 上。此时，容许的速度分布 $D$ 恰好就是该[子流形](@entry_id:159439)的切丛 $TS$ 。例如，如果一个质点被限制在 $xy$ 平面上运动，约束 $z=0$ 是完整的。

相反，**非完整约束**是不可积的。尽管它在每一点都限制了速度的方向，但它并不限制系统可到达的构型区域。通过一系列巧妙的容许运动，系统可以到达任何构型。一个经典的例子就是平行泊车：汽车的[非完整约束](@entry_id:167828)（不能侧滑）不允许它直接横向移动到车位里，但通过前进和后退的组合，汽车最终可以实现纯粹的横向位移。

#### [弗罗贝尼乌斯可积性定理](@entry_id:161479)

判断一个分布 $D$ 是否可积的数学工具是**[弗罗贝尼乌斯定理](@entry_id:181858) (Frobenius Integrability Theorem)**。该定理指出，一个分布 $D$ 是可积的（即对应于一个[完整约束](@entry_id:140686)），当且仅当它是**对合的 (involutive)**。对合性意味着，对于分布 $D$ 中的任意两个矢量场 $X$ 和 $Y$，它们的**[李括号](@entry_id:636461) (Lie bracket)** $[X, Y]$ 仍然位于分布 $D$ 中。
$$
[X, Y] \in \Gamma(D) \quad \forall X, Y \in \Gamma(D)
$$
李括号 $[X,Y]$ 衡量了沿着 $X$ 和 $Y$ 方向的无穷小流动的不可交换性。如果 $[X,Y]$ 产生了 $D$ 之外的运动分量，那么分布就是不可积的。

现在我们来检验滚动圆盘的[约束分布](@entry_id:1122944)。利用前面找到的[基矢](@entry_id:199546)量场 $X_\theta$ 和 $X_\phi$，我们计算它们的[李括号](@entry_id:636461)  ：
$$
[X_\theta, X_\phi] = \left[\frac{\partial}{\partial\theta}, R\cos\theta \frac{\partial}{\partial x} + R\sin\theta \frac{\partial}{\partial y} + \frac{\partial}{\partial\phi}\right] = -R\sin\theta\frac{\partial}{\partial x} + R\cos\theta\frac{\partial}{\partial y}
$$
这个结果是一个在 $xy$ 平面内的矢量场。它是否属于分布 $D$ 呢？一个矢量场属于 $D$ 当且仅当它是 $X_\theta$ 和 $X_\phi$ 的[线性组合](@entry_id:154743)。显然，$[X_\theta, X_\phi]$ 既没有 $\frac{\partial}{\partial\theta}$ 分量，也没有 $\frac{\partial}{\partial\phi}$ 分量，因此它不可能是 $X_\theta$ 或 $X_\phi$ 的非零倍数，也不可能是它们的线性组合。所以，$[X_\theta, X_\phi] \notin D$。

根据[弗罗贝尼乌斯定理](@entry_id:181858)，由于[约束分布](@entry_id:1122944) $D$ 在[李括号](@entry_id:636461)下不封闭，因此它是不可积的。这从数学上严格证明了滚动圆盘的约束是**非完整的**。

#### 几何诠释：[曲率与和乐](@entry_id:186596)

李括号 $[X_\theta, X_\phi]$ 的非零结果具有深刻的物理意义。它代表了一个通过一系列容许运动（原地转弯和前向滚动）可以产生的、但在瞬时被禁止的运动方向（侧滑）。这正是[非完整运动](@entry_id:1128847)规划（如平行泊车）的基础。

这个概念也引出了**[和乐](@entry_id:137051) (holonomy)** 的思想。[和乐](@entry_id:137051)是指系统在“[形状空间](@entry_id:1131536)”（即内部变量，此处为 $\theta$ 和 $\phi$）中执行一个闭合回路后，在“位置空间”（即群变量，此处为 $x$ 和 $y$）中产生的净位移。例如，让圆盘向前滚动、原地转弯、向后滚动、再转回原方向，可以使其最终位置发生净变化。

对于由单个一形式 $\omega=0$ 定义的约束（如竖立硬币），[弗罗贝尼乌斯定理](@entry_id:181858)有另一种等价形式：分布 $D=\ker\omega$ 可积的充要条件是 $\omega \wedge d\omega = 0$。对于竖立硬币的约束 $\omega = -\sin\theta dx + \cos\theta dy$，我们计算其[外微分](@entry_id:161900) $d\omega$：
$$
d\omega = d(-\sin\theta dx + \cos\theta dy) = -\cos\theta d\theta \wedge dx + (-\sin\theta) d\theta \wedge dy
$$
然后计算[楔积](@entry_id:147029)：
$$
\omega \wedge d\omega = -(\sin^2\theta + \cos^2\theta)dx \wedge dy \wedge d\theta = -dx \wedge dy \wedge d\theta
$$
由于 $\omega \wedge d\omega \neq 0$，约束是不可积的 。这个非零的三形式度量了分布的“扭曲”程度，或称之为不[可积性](@entry_id:142415)。

### [非完整系统](@entry_id:173158)的动力学与对称性

[非完整约束](@entry_id:167828)不仅影响运动学，还深刻地改变了系统的动力学行为，特别是与对称性和守恒律的关系。

#### [拉格朗日-达朗贝尔原理](@entry_id:1126999)

对于无约束或仅受完整约束的系统，其[运动方程](@entry_id:264286)可由[哈密顿原理](@entry_id:175601)导出。对于非完整系统，我们使用**[拉格朗日-达朗贝尔原理](@entry_id:1126999) (Lagrange-d'Alembert principle)**，该原理要求虚功在满足约束的虚位移上为零。这通常导致带有[拉格朗日乘子](@entry_id:142696)的[运动方程](@entry_id:264286)，其中乘子代表维持约束所需的[约束力](@entry_id:170052)。

对于像滚动圆盘这样的特定系统（称为[查普雷金系统](@entry_id:1122270)），存在一种更直接的方法。我们可以将[约束方程](@entry_id:138140)代入系统的拉格朗日量中，得到一个**约化[拉格朗日量](@entry_id:174593) (reduced Lagrangian)**。滚动圆盘的拉格朗日量是其动能（假设在水平面上滚动，无势能）：
$$
L(q, \dot{q}) = \frac{m}{2}(\dot{x}^2 + \dot{y}^2) + \frac{I_\theta}{2}\dot{\theta}^2 + \frac{I_\phi}{2}\dot{\phi}^2
$$
其中 $I_\theta$ 和 $I_\phi$ 分别是绕竖直轴和自身车轴的[转动惯量](@entry_id:174608)。将约束 $\dot{x} = R\dot{\phi}\cos\theta$ 和 $\dot{y} = R\dot{\phi}\sin\theta$ 代入上式：
$$
L_c = \frac{m}{2}((R\dot{\phi}\cos\theta)^2 + (R\dot{\phi}\sin\theta)^2) + \frac{I_\theta}{2}\dot{\theta}^2 + \frac{I_\phi}{2}\dot{\phi}^2 = \frac{mR^2}{2}\dot{\phi}^2(\cos^2\theta + \sin^2\theta) + \frac{I_\theta}{2}\dot{\theta}^2 + \frac{I_\phi}{2}\dot{\phi}^2
$$
整理后得到约化拉格朗日量：
$$
L_c(\theta, \phi, \dot{\theta}, \dot{\phi}) = \frac{1}{2}(I_\phi + mR^2)\dot{\phi}^2 + \frac{1}{2}I_\theta\dot{\theta}^2
$$
这个仅依赖于形状变量 $(\theta, \phi)$ 及其速度的拉格朗日量，描述了系统在[约束分布](@entry_id:1122944)上的动力学。形状空间的[运动方程](@entry_id:264286)可以从 $L_c$ 导出，而位置 $(x,y)$ 的演化则通过积分[约束方程](@entry_id:138140)（一个称为**重构 (reconstruction)** 的过程）来恢复。

#### 对称性破缺与动量不守恒

在无[约束系统](@entry_id:164587)中，[拉格朗日量](@entry_id:174593)的连续对称性通过[诺特定理](@entry_id:145690) (Noether's theorem) 对应于一个[守恒量](@entry_id:161475)。例如，滚动圆盘的[拉格朗日量](@entry_id:174593) $L$ 在空间平移和旋转（即[二维欧几里得群](@entry_id:196732) $SE(2)$ 的作用）下是不变的。这通常意味着[线动量](@entry_id:174467)和角动量守恒 。

然而，在[非完整系统](@entry_id:173158)中，情况截然不同。尽管[拉格朗日量](@entry_id:174593)具有 $SE(2)$ 对称性，但与之相关的**动量映射 (momentum map)** $J = (p_x, p_y, xp_y - yp_x + p_\theta)$ 却**不守恒**。

其根本原因在于，维持[非完整约束](@entry_id:167828)所需的[约束力](@entry_id:170052)在对称性变换下做了“[虚功](@entry_id:176403)”。从几何角度看，对称性[群作用](@entry_id:268812)产生的[无穷小位移](@entry_id:202209)（即对称性生成元矢量场）并不位于容许的[约束分布](@entry_id:1122944) $D$ 之内。换言之，对称性变换本身“违反”了约束。因此，[拉格朗日量](@entry_id:174593)的对称性没有下降为受约束系统的对称性，[诺特定理](@entry_id:145690)的条件不再满足 。动量映射的时间导数不为零，其变化率恰好由[约束力](@entry_id:170052)沿[对称性破缺](@entry_id:158994)方向所做的功率给出。

### 高级几何观点：[联络与曲率](@entry_id:158520)

几何力学的最终力量在于它能够将[非完整约束](@entry_id:167828)的这些看似复杂的特性统一到一个优美的几何框架中——[主丛上的联络](@entry_id:159386)理论。

#### [主丛](@entry_id:160029)图像

我们可以将系统的构型空间 $Q$ 视为一个**[主丛](@entry_id:160029) (principal bundle)** 。这是一个[纤维丛](@entry_id:159565)，其纤维是系统的对称性群 $G$。丛的**底空间 (base space)** $B$ 是“[形状空间](@entry_id:1131536)”，即除去对称性自由度后剩下的内部变量空间。

对于滚动圆盘，如果我们只考虑平移对称性，则对称群为 $G = \mathbb{R}^2$。[构型空间](@entry_id:149531) $Q = \mathbb{R}^2 \times S^1 \times S^1$ 是一个以形状空间 $B = S^1 \times S^1$（由 $(\theta, \phi)$ [参数化](@entry_id:265163)）为底，以位置空间 $G = \mathbb{R}^2$ 为纤维的[主丛](@entry_id:160029)。[投影映射](@entry_id:153398) $\pi: Q \to B$ 就是简单地“忘记”位置信息：$\pi(x,y,\theta,\phi) = (\theta,\phi)$。

#### [非完整联络](@entry_id:1128845)及其曲率

在这个[主丛](@entry_id:160029)框架下，[约束分布](@entry_id:1122944) $D$ 定义了一种将切[空间分解](@entry_id:755142)为**水平**和**垂直**子空间的方式。垂直子空间 $V_q$ 是与纤维相切的空间（在此例中由 $\frac{\partial}{\partial x}$ 和 $\frac{\partial}{\partial y}$ 张成），而水平子空间 $H_q$ 就是[约束分布](@entry_id:1122944) $D_q$。

这个分解 $T_qQ = H_q \oplus V_q$ 定义了一个**埃雷斯曼联络 (Ehresmann connection)**，或在此情境下称为**[非完整联络](@entry_id:1128845) (nonholonomic connection)**。联络提供了一种从底空间（[形状空间](@entry_id:1131536)）“平行提升”路径到全空间（构型空间）的方法。在这里，非完整约束本身就规定了这种提升的规则：一旦形状变量 $(\theta(t), \phi(t))$ 的演化给定，位置 $(x(t), y(t))$ 的演化就由积分[约束方程](@entry_id:138140)唯一确定。

联络可以用一个**联络一形式 (connection one-form)** $A$ 来描述。它是一个取值于对称群[李代数](@entry_id:137954) $\mathfrak{g}$ 的一形式，其核空间恰好是[水平分布](@entry_id:196663) $D$。对于滚动圆盘和平移群 $G=\mathbb{R}^2$（其[李代数](@entry_id:137954)为 $\mathbb{R}^2$），[联络形式](@entry_id:160771)的两个分量正是我们之前遇到的约束形式 ：
$$
A^x = dx - R\cos\theta d\phi
$$
$$
A^y = dy - R\sin\theta d\phi
$$
联络的**曲率 (curvature)** $F$ 衡量了水平子空间沿不同方向变化的程度。对于[阿贝尔群](@entry_id:150284)（如 $\mathbb{R}^2$），曲率简单地由[联络形式](@entry_id:160771)的[外微分](@entry_id:161900)给出，$F=dA$。计算可得：
$$
F^x = d(A^x) = d(dx - R\cos\theta d\phi) = R\sin\theta d\theta \wedge d\phi
$$
$$
F^y = d(A^y) = d(dy - R\sin\theta d\phi) = -R\cos\theta d\theta \wedge d\phi
$$
**这个非零的曲率 $F$ 才是故事的核心** 。它在几何上精确地量化了[约束分布](@entry_id:1122944)的不[可积性](@entry_id:142415)。前面计算的[李括号](@entry_id:636461) $[X_\theta, X_\phi]$ 所产生的“垂直”分量（即不在 $D$ 中的部分），正是由曲率决定的。更准确地说，水平矢量场的[李括号](@entry_id:636461)的垂直部分由曲率给出。

此外，曲率 $F$ 度量了系统的和乐。在形状空间中沿一个无穷小闭合回路运动，在位置空间中产生的净位移正比于该回路所包围面积上的曲率积分。最后，在动力学约化理论中，正是这个曲率导致了[约化相空间](@entry_id:165136)上的近[泊松括号](@entry_id:151133) (almost-Poisson bracket) 不满足雅可比恒等式，从而使其无法成为一个真正的[泊松括号](@entry_id:151133)。

综上所述，从一个简单的物理约束“无滑动滚动”出发，我们通过几何力学的语言，最终将其不可积的本质追溯到一个深刻的几何对象——[非完整联络](@entry_id:1128845)的非零曲率。这展示了现代微分几何如何为经典力学问题提供一个统一而有力的视角。