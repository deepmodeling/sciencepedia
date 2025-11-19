## 引言
[非线性系统](@entry_id:168347)在自然界和工程技术中无处不在，其行为的复杂性使得通过直接[求解微分方程](@entry_id:137471)来分析它们变得异常困难，甚至常常是不可能的。因此，理解这些系统的稳定性——即它们在受到扰动后能否恢复到平衡状态——成为了预测和控制其动态行为的关键。本文旨在解决这一核心挑战：如何在不求解方程的情况下，定性乃至定量地判断一个[非线性系统的稳定性](@entry_id:264568)。

为实现这一目标，我们将分三步展开。首先，在“原理与机制”一章中，我们将深入探讨[李雅普诺夫稳定性理论](@entry_id:177166)、[拉萨尔不变性原理](@entry_id:266201)以及[分岔理论](@entry_id:143561)等基石性工具，这些工具为我们提供了从能量和几何视角审视系统动态的强大武器。接着，在“应用与跨学科联系”一章中，我们将展示这些理论如何在机械、电子、生物、化学乃至地球科学等多个领域中，被用来解释从神经元放电到行星[系统边界](@entry_id:158917)的各种复杂现象。最后，通过“动手实践”部分，读者将有机会通过解决具体问题来巩固所学知识，将理论应用于实践。

## 原理与机制

非线性系统的行为远比线性系统丰富和复杂，它们可以展现出多重[稳态](@entry_id:182458)、[极限环振荡](@entry_id:275225)、以及对参数变化的剧烈响应（即分岔）。因此，对[非线性系统稳定性](@entry_id:178090)的分析，不能仅仅依赖于求解其[微分方程](@entry_id:264184)——这在大多数情况下是不可能的。本章将介绍一系列强大的理论工具，使我们能够不通过直接求解，就能深刻理解非-线性系统在[平衡点](@entry_id:272705)附近的局部行为以及在整个相空间中的全局动态特性。这些方法的核心思想，是从几何和能量的角度来审视系统的演化。

### [李雅普诺夫稳定性理论](@entry_id:177166)框架

分析[非线性系统稳定性](@entry_id:178090)的最普适和强大的工具之一是[亚历山大·李雅普诺夫](@entry_id:202838)（[Aleksandr Lyapunov](@entry_id:202838)）提出的“第二方法”，或称“直接法”。该方法的核心思想是通过构造一个标量“能量样”函数，即**李雅普诺夫函数** (Lyapunov function)，来判断系统状态随时间演化的趋势。如果系统从一个[平衡点](@entry_id:272705)被扰动后，其“能量”总是耗散的，那么系统最终必然会回到该[平衡点](@entry_id:272705)。这种思想的巧妙之处在于，它将对复杂向量场的分析，转化为了对一个更简单的标量函数的分析。

#### [李雅普诺夫函数](@entry_id:273986)与定性

假设我们研究的[自治系统](@entry_id:173841)为 $\dot{\mathbf{x}} = \mathbf{f}(\mathbf{x})$，并且不失一般性地，我们已经将坐标平移，使得原点 $\mathbf{x} = \mathbf{0}$ 是系统的一个[平衡点](@entry_id:272705)，即 $\mathbf{f}(\mathbf{0}) = \mathbf{0}$。一个连续可微的标量函数 $V(\mathbf{x})$ 要成为原点附近的一个[李雅普诺夫函数](@entry_id:273986)候选者，必须具备类似于“能量”的性质。具体而言，它必须在包含原点的某个开邻域 $D$ 内满足两个条件：

1.  在[平衡点](@entry_id:272705)处取值为零：$V(\mathbf{0}) = 0$。
2.  在[平衡点](@entry_id:272705)之外取正值：对于所有 $\mathbf{x} \in D$ 且 $\mathbf{x} \neq \mathbf{0}$，有 $V(\mathbf{x}) > 0$。

满足这两个条件的函数被称为在原点邻域内是**正定的 (positive definite)**。如果第二个条件放宽为 $V(\mathbf{x}) \ge 0$，则称该函数是**半正定的 (positive semi-definite)**。相应地，若 $V(\mathbf{x})  0$（对于 $\mathbf{x} \neq \mathbf{0}$），则函数是**负定的 (negative definite)**。

判断一个函数是否正定是应用[李雅普诺夫方法](@entry_id:635639)的第一步。例如，考虑函数 $V(x, y) = 1 - \cos(x) + \frac{1}{2} y^2$ [@problem_id:2193204]。首先，我们验证它在原点的值：$V(0, 0) = 1 - \cos(0) + 0 = 1 - 1 = 0$，满足第一个条件。其次，我们分析它在原点附近的符号。我们知道，对于任何非零的 $x$，$\cos(x)  1$，因此 $1 - \cos(x) > 0$（在一个例如 $|x|  2\pi$ 的邻域内，等号只在 $x=0$ 成立）。同时，$\frac{1}{2} y^2 \ge 0$，等号只在 $y=0$ 成立。因此，只要 $(x, y) \neq (0, 0)$，两个非负项 $1-\cos(x)$ 和 $\frac{1}{2} y^2$ 中至少有一个是严格为正的，它们的和 $V(x, y)$ 必然为正。故 $V(x, y)$ 在原点附近是正定的。另一种有效的方法是利用[泰勒展开](@entry_id:145057)。在原点附近，$\cos(x) \approx 1 - \frac{x^2}{2}$，所以 $V(x, y) \approx 1 - (1 - \frac{x^2}{2}) + \frac{1}{2} y^2 = \frac{1}{2}x^2 + \frac{1}{2}y^2$。其二次型部分是正定的，这同样表明该函数在原点附近是正定的。

#### 基于时间导数的[稳定性判据](@entry_id:755304)

一个正定函数 $V(\mathbf{x})$ 仅仅是候选者。要真正判断稳定性，我们必须考察当系统沿着其轨迹演化时，$V(\mathbf{x})$ 的值如何变化。这个变化率由 $V$ 沿着系统向量场 $\mathbf{f}(\mathbf{x})$ 的时间导数 $\dot{V}$ 给出，根据链式法则，它等于 $V$ 的梯度与向量场的[点积](@entry_id:149019)：
$$
\dot{V}(\mathbf{x}) = \frac{dV}{dt} = \sum_{i=1}^{n} \frac{\partial V}{\partial x_i} \frac{dx_i}{dt} = \nabla V(\mathbf{x}) \cdot \mathbf{f}(\mathbf{x})
$$
李雅普诺夫的稳定性定理可以总结如下：
*   如果 $\dot{V}(\mathbf{x})$ 在原点的一个邻域内是**负定的** (negative definite)，即 $\dot{V}(\mathbf{x})  0$ 对于所有 $\mathbf{x} \neq \mathbf{0}$，那么[平衡点](@entry_id:272705) $\mathbf{x} = \mathbf{0}$ 是**[渐近稳定](@entry_id:168077)的 (asymptotically stable)**。这意味着任何从该邻域内出发的轨迹不仅会停留在原点附近，而且最终会收敛到原点。
*   如果 $\dot{V}(\mathbf{x})$ 仅为**负半定的** (negative semi-definite)，即 $\dot{V}(\mathbf{x}) \le 0$，那么我们只能保证[平衡点](@entry_id:272705)是**稳定的 (stable)**（有时称为李雅普诺夫意义下的稳定）。这意味着轨迹会停留在原点附近，但不一定收敛到原点（可能收敛到某个使 $\dot{V}=0$ 的集合）。

考虑一个具有[哈密顿量](@entry_id:172864) $H(x, y)$ 的保守系统，如果引入线性阻尼，其[动力学方程](@entry_id:751029)可以写为 $\dot{x} = \frac{\partial H}{\partial y} - \delta x$ 和 $\dot{y} = -\frac{\partial H}{\partial x} - \delta y$，其中 $\delta > 0$ 是阻尼系数 [@problem_id:1149585]。在这里，[哈密顿量](@entry_id:172864) $H$ 本身可以作为天然的李雅普诺夫函数候选者，因为它通常代表系统的能量。其时间导数为：
$$
\frac{dH}{dt} = \frac{\partial H}{\partial x}\dot{x} + \frac{\partial H}{\partial y}\dot{y} = \frac{\partial H}{\partial x}\left(\frac{\partial H}{\partial y} - \delta x\right) + \frac{\partial H}{\partial y}\left(-\frac{\partial H}{\partial x} - \delta y\right)
$$
展开后，交叉项 $\frac{\partial H}{\partial x}\frac{\partial H}{\partial y} - \frac{\partial H}{\partial y}\frac{\partial H}{\partial x}$ 相互抵消，剩下：
$$
\frac{dH}{dt} = -\delta \left(x \frac{\partial H}{\partial x} + y \frac{\partial H}{\partial y}\right)
$$
对于一个典型的物理系统，例如 $H(x, y) = \frac{1}{2}(\omega_1 x^2 + \omega_2 y^2) + \frac{\alpha}{4}x^4 + \frac{\beta}{2}x^2y^2$，其中所有系数均为正，那么 $\dot{H}$ 将是负定的。这直观地表明，阻尼项持续地从系统中耗散能量，迫使系统最终回到能量最低的状态，即[平衡点](@entry_id:272705)。

#### 全局稳定性与[径向无界函数](@entry_id:178431)

[李雅普诺夫方法](@entry_id:635639)不仅能分析[局部稳定性](@entry_id:751408)，还能用于证明**全局[渐近稳定](@entry_id:168077) (global asymptotic stability)**，即系统从任何初始状态出发都会收敛到唯一的[平衡点](@entry_id:272705)。要做到这一点，[李雅普诺夫函数](@entry_id:273986) $V(\mathbf{x})$ 除了在整个相空间 $\mathbb{R}^n$ 上都是正定的，且其导数 $\dot{V}(\mathbf{x})$ 在整个相空间上都是负定的之外，还必须满足一个额外的条件：$V(\mathbf{x})$ 必须是**径向无界的 (radially unbounded)**。

径向无界意味着当状态[向量的范数](@entry_id:154882) $\|\mathbf{x}\|$ 趋于无穷时，$V(\mathbf{x})$ 的值也趋于无穷。这个条件确保了 $V(\mathbf{x})$ 的[等值面](@entry_id:196027)是闭合的，形成了一系列嵌套的“能量阱”。由于 $\dot{V}  0$，轨迹必须穿越这些[等值面](@entry_id:196027)朝向 $V$ 值更低的方向移动，而径向无界性保证了不存在可以逃逸到无穷远的路径。

例如，考虑函数 $V(x,y) = (x-y^2)^2 + \alpha y^k$，其中 $\alpha > 0$ [@problem_id:1121039]。为了使 $V$ 径向无界，我们必须确保当 $\|(x,y)\| \to \infty$ 时，$V(x,y) \to \infty$。我们需要考察所有可能的路径。如果沿着路径 $x=y^2$ 移动，第一项 $(x-y^2)^2$ 变为零。此时，$V(y^2, y) = \alpha y^k$。如果 $k$ 是奇数（例如 $k=1, 3, \dots$），那么当 $y \to -\infty$ 时，$V \to -\infty$，函数不是径向无界的。为了保证无论 $y$ 如何变化，$y^k$ 都趋向正无穷或保持非负， $k$ 必须是正偶数。因此，能确保 $V(x,y)$ 径向无界的最小正整数 $k$ 是 $2$。

#### 与线性系统的联系

对于[线性时不变系统](@entry_id:276591) $\dot{\mathbf{x}} = A\mathbf{x}$，其稳定性由矩阵 $A$ 的[特征值](@entry_id:154894)决定。如果所有[特征值](@entry_id:154894)的实部都为负（即 $A$ 是一个Hurwitz矩阵），则系统是[渐近稳定](@entry_id:168077)的。这一结论也可以通过李雅普诺夫理论得到。我们可以为稳定的[线性系统](@entry_id:147850)寻找一个二次型的[李雅普诺夫函数](@entry_id:273986) $V(\mathbf{x}) = \mathbf{x}^T P \mathbf{x}$，其中 $P$ 是一个[对称正定矩阵](@entry_id:136714)。其时间导数为：
$$
\dot{V}(\mathbf{x}) = \dot{\mathbf{x}}^T P \mathbf{x} + \mathbf{x}^T P \dot{\mathbf{x}} = (A\mathbf{x})^T P \mathbf{x} + \mathbf{x}^T P (A\mathbf{x}) = \mathbf{x}^T (A^T P + PA) \mathbf{x}
$$
为了使 $\dot{V}$ 是负定的，我们要求 $A^T P + PA = -Q$，其中 $Q$ 是任意一个[对称正定矩阵](@entry_id:136714)（通常为了方便选择 $Q=I$，[单位矩阵](@entry_id:156724)）。这个方程被称为**代数[李雅普诺夫方程](@entry_id:165178) (algebraic Lyapunov equation)**。李雅普诺夫的一个基本定理是：如果 $A$ 是Hurwitz矩阵，那么对于任何给定的[正定矩阵](@entry_id:155546) $Q$，上述方程总存在一个唯一的正定解 $P$。反之亦然。这个解 $P$ 甚至有一个积分表达式：$P = \int_0^\infty e^{A^T t} Q e^{At} dt$ [@problem_id:1149524]。这个联系为控制理论中的[稳定性分析](@entry_id:144077)和[控制器设计](@entry_id:274982)提供了坚实的数学基础。

### [拉萨尔不变性原理](@entry_id:266201)与平面动力学

当[李雅普诺夫函数](@entry_id:273986)的导数 $\dot{V}$ 仅仅是负半定（即 $\dot{V} \le 0$）时，我们无法直接断定系统会收敛到[平衡点](@entry_id:272705)。轨迹可能会停留在使得 $\dot{V}=0$ 的任何区域。**[拉萨尔不变性原理](@entry_id:266201) (LaSalle's Invariance Principle)** 对此进行了完善，它指出，如果轨迹是有界的，那么它最终将收敛到集合 $E = \{\mathbf{x} | \dot{V}(\mathbf{x}) = 0\}$ 中的最大**[不变集](@entry_id:275226) (invariant set)**。[不变集](@entry_id:275226)是指任何从该集合中出发的轨迹将永远留在该集合内。

#### [拉萨尔不变性原理](@entry_id:266201)的应用

拉萨尔原理在分析具有非孤立[平衡点](@entry_id:272705)的系统时尤其有用。考虑系统 [@problem_id:1149580]：
$$
\begin{aligned}
\dot{x} = -x(x^2+y^2-R^2) \\
\dot{y} = -y(x^2+y^2-R^2) \\
\dot{z} = -z
\end{aligned}
$$
这个系统的[平衡点](@entry_id:272705)集合包括 $z$ 轴（$x=y=0$）以及圆环 $x^2+y^2=R^2, z=0$。让我们构造一个简单的[李雅普诺夫函数](@entry_id:273986)候选者来分析 $xy$ 平面上的动态：$V(x,y,z) = x^2+y^2$。它的时间导数为：
$$
\dot{V} = 2x\dot{x} + 2y\dot{y} = 2x[-x(x^2+y^2-R^2)] + 2y[-y(x^2+y^2-R^2)] = -2(x^2+y^2)(x^2+y^2-R^2)
$$
令 $r^2 = x^2+y^2$，则 $\dot{V} = -2r^2(r^2-R^2)$。可见，$\dot{V}$ 并不是负定的。它在 $r=0$（$z$轴）和 $r=R$ 处为零。根据拉萨尔原理，轨迹将收敛到使 $\dot{V}=0$ 的最大[不变集](@entry_id:275226)。
这个集合 $E = \{(x,y,z) | x=y=0\} \cup \{(x,y,z) | x^2+y^2=R^2\}$。
*   对于集合 $x=y=0$（$z$轴），我们有 $\dot{x}=0, \dot{y}=0$。这意味着 $z$ 轴本身是一个[不变集](@entry_id:275226)。
*   对于集合 $x^2+y^2=R^2$，我们有 $\dot{x}=0, \dot{y}=0$。这意味着任何半径为 $R$ 的圆柱面也是不变的。

同时，$\dot{z}=-z$ 的解为 $z(t) = z_0 e^{-t}$，表明无论[初始条件](@entry_id:152863)如何，$z(t)$ 都会渐近趋于 $0$。因此，所有轨迹最终都会趋近于 $z=0$ 平面。结合以上分析，对于任何非 $z$ 轴的初始点，轨迹的 $\omega$-[极限集](@entry_id:138626)（即 $t \to \infty$ 时的[极限点集](@entry_id:178514)合）必须是包含在 $E$ 中且满足 $z=0$ 的最大[不变集](@entry_id:275226)，这个集合就是圆 $x^2+y^2=R^2, z=0$。因此，所有轨迹最终都会汇聚到这个圆上。

#### [庞加莱-本迪克松定理](@entry_id:264953)与陷阱区域

对于二维（平面）[自治系统](@entry_id:173841)，我们有更专门且强大的工具。**[庞加莱-本迪克松定理](@entry_id:264953) (Poincaré-Bendixson theorem)** 指出，如果一个平面系统的轨迹被限制在一个紧致的（即封[闭且有界](@entry_id:140798)的）、不包含任何[平衡点](@entry_id:272705)的**陷阱区域 (trapping region)** 内，那么该轨迹的 $\omega$-[极限集](@entry_id:138626)必然是一个**极限环 (limit cycle)**，即一个孤立的周期轨道。

这个定理的实际应用关键在于如何找到一个陷阱区域。一个区域是陷阱区域，意味着在它的边界上，系统的向量场都指向区域内部或与之相切。对于一个以原点为中心的圆形区域 $D_R = \{ (x,y) | x^2+y^2 \le R^2 \}$，要成为陷阱区域，只需在边界 $r=R$ 上，[径向速度](@entry_id:159824) $\dot{r}$ 满足 $\dot{r} \le 0$。

考虑一个平面系统 [@problem_id:1149375]，通过转换为极坐标 $(r, \theta)$，其径向动态由 $\dot{r} = r(a_0 - a_1 r^2 + a_2 r^4)$ 给出，其中 $a_0, a_1, a_2$ 均为正参数。要使半径为 $R$ 的圆盘成为陷阱区域，我们需要在 $r=R$ 处 $\dot{r} \le 0$：
$$
R(a_0 - a_1 R^2 + a_2 R^4) \le 0
$$
由于我们关心的是 $R>0$，这等价于 $a_2 R^4 - a_1 R^2 + a_0 \le 0$。这是一个关于 $u = R^2$ 的二次不等式 $a_2 u^2 - a_1 u + a_0 \le 0$。假设 $a_1^2 > 4a_0 a_2$，该二次方程有两个正实根 $u_1  u_2$。该不等式在两根之间成立，即 $u_1 \le u \le u_2$。这意味着半径 $R$ 只要满足 $\sqrt{u_1} \le R \le \sqrt{u_2}$，对应的圆盘就是一个陷阱区域。其中最小的陷阱区域半径为 $R_{min} = \sqrt{u_1} = \sqrt{\frac{a_1 - \sqrt{a_1^2 - 4a_0 a_2}}{2a_2}}$。

#### 排除周期轨道：本迪克松-[杜拉克判据](@entry_id:268769)

与寻找极限环相反，有时我们需要证明[极限环](@entry_id:274544)**不存在**。**本迪克松-[杜拉克判据](@entry_id:268769) (Bendixson-Dulac criterion)** 为此提供了一个有效方法。它指出，对于平面系统 $\dot{x}=P(x,y), \dot{y}=Q(x,y)$，如果在一个单连通区域 $D$ 内，存在一个连续可微的函数 $\phi(x,y)$（称为[杜拉克函数](@entry_id:262898)），使得表达式 $\nabla \cdot (\phi \mathbf{F}) = \frac{\partial (\phi P)}{\partial x} + \frac{\partial (\phi Q)}{\partial y}$ 的符号恒定（恒正或恒负，允许在测度为零的集合上为零），则区域 $D$ 内不存在任何完全包含在其中的周期轨道。

最简单的选择是 $\phi(x,y) = 1$。这时，判据简化为检查[向量场的散度](@entry_id:136342) $\nabla \cdot \mathbf{F} = \frac{\partial P}{\partial x} + \frac{\partial Q}{\partial y}$ 的符号。如果散度在区域内恒不为零，则根据[格林公式](@entry_id:173118)，任何闭合轨线 $\mathcal{C}$ 的[线积分](@entry_id:141417) $\oint_{\mathcal{C}} (P dy - Q dx)$ 将为零，而另一方面，它又等于区域内散度的面积分，这就导致了矛盾。

考虑一个Liénard方程 [@problem_id:1149477]，它可以写成系统形式 $\dot{x}_1 = x_2$ 和 $\dot{x}_2 = -\beta x_1 + (\alpha - \gamma - \cos x_1 - x_1^2)x_2$。选择 $\phi=1$，其散度为：
$$
\nabla \cdot \mathbf{F} = \frac{\partial (x_2)}{\partial x_1} + \frac{\partial (\dot{x_2})}{\partial x_2} = 0 + (\alpha - \gamma - \cos x_1 - x_1^2)
$$
为了保证没有周期解，我们要求该散度在整个[相平面](@entry_id:168387)上符号恒定，例如恒为负。即要求对于所有的 $x_1 \in \mathbb{R}$，$\alpha - \gamma - \cos x_1 - x_1^2 \le 0$。这等价于 $\alpha \le \gamma + \cos x_1 + x_1^2$。为了使这个不等式对所有 $x_1$ 成立，$\alpha$ 必须小于或等于函数 $g(x_1) = \gamma + \cos x_1 + x_1^2$ 的[全局最小值](@entry_id:165977)。通过求导我们发现 $g(x_1)$ 在 $x_1=0$ 处取得最小值 $g(0)=\gamma+1$。因此，只要 $\alpha \le \gamma + 1$，系统就不会有周期解。这个条件给出了保证系统无[振荡](@entry_id:267781)的参数范围。

### 分岔：定性行为的突变

非线性系统的一个显著特征是，当系统参数缓慢变化时，其相图的拓扑结构可能在某个临界值发生突然的、定性的改变。这种现象称为**[分岔](@entry_id:273973) (bifurcation)**。在[分岔点](@entry_id:187394)，系统的稳定性会发生改变，例如[平衡点](@entry_id:272705)的产生或消失、稳定性的转换，或是[极限环](@entry_id:274544)的诞生。

#### 线性化的局限性与非[双曲平衡点](@entry_id:165723)

分析[平衡点稳定性](@entry_id:261937)的标准方法是**线性化**：计算系统在[平衡点](@entry_id:272705)处的雅可比矩阵 $J$，并考察其[特征值](@entry_id:154894) $\lambda$。如果所有[特征值](@entry_id:154894)的实部都不为零，该[平衡点](@entry_id:272705)称为**双曲的 (hyperbolic)**。此时，[哈特曼-格罗布曼定理](@entry_id:158812)保证了[非线性系统](@entry_id:168347)在[平衡点](@entry_id:272705)附近的局部行为与其线性化系统是[拓扑共轭](@entry_id:161965)的。
*   所有 $\text{Re}(\lambda)  0$：[稳定结点](@entry_id:261492)或[焦点](@entry_id:174388)。
*   所有 $\text{Re}(\lambda) > 0$：不[稳定结点](@entry_id:261492)或[焦点](@entry_id:174388)。
*   存在 $\text{Re}(\lambda) > 0$ 和 $\text{Re}(\lambda)  0$：[鞍点](@entry_id:142576)。

然而，当存在至少一个[特征值](@entry_id:154894)的实部为零时，[平衡点](@entry_id:272705)是**非双曲的 (non-hyperbolic)**。在这种情况下，线性化分析是**不确定的 (inconclusive)** [@problem_id:1467581]。线性项消失，[平衡点](@entry_id:272705)附近的动力学行为由更高阶的[非线性](@entry_id:637147)项决定。这种情况正是分岔发生的标志。例如，对于一个一维系统 $\dot{x}=f(x)$，在[平衡点](@entry_id:272705) $x^*$ 处的[特征值](@entry_id:154894) $\lambda = f'(x^*)$。如果 $\lambda=0$，那么对微小扰动 $\delta x = x - x^*$ 的线性化方程为 $\dot{\delta x} \approx 0 \cdot \delta x = 0$，这无法告诉我们扰动是增长还是衰减。此时，我们必须考察泰勒展开中的二阶项 $\frac{1}{2}f''(x^*)(\delta x)^2$ 来判断稳定性。

#### [鞍结分岔](@entry_id:263507)

最简单也最常见的分岔之一是**鞍结分岔 (saddle-node bifurcation)**，它描述了[平衡点](@entry_id:272705)的产生和湮灭过程。在一个一维系统中，当参数 $r$ 变化时，一个稳定[平衡点](@entry_id:272705)和一个[不稳定平衡](@entry_id:174306)点（在更高维度下它们是结点和[鞍点](@entry_id:142576)）相互靠近，在临界参数值 $r_c$ 处碰撞并湮灭。在[分岔点](@entry_id:187394)，系统恰好拥有一个半稳定的非[双曲平衡点](@entry_id:165723)。

[鞍结分岔](@entry_id:263507)发生的条件是[平衡点](@entry_id:272705)条件 $\dot{\theta}=0$ 和非双曲条件 $\frac{\partial\dot{\theta}}{\partial\theta}=0$ 同时满足。考虑一个在圆周上的动力学系统 $\dot{\theta} = r + \cos(\theta) + a\cos(2\theta)$ [@problem_id:1149588]。分岔点 $(\theta_c, r_c)$ 必须满足：
$$
\begin{cases}
r_c + \cos(\theta_c) + a\cos(2\theta_c) = 0 \\
-\sin(\theta_c) - 2a\sin(2\theta_c) = 0
\end{cases}
$$
第二个方程给出 $\sin\theta_c(1+4a\cos\theta_c)=0$。这产生了两种可能的解：$\sin\theta_c=0$ 或 $\cos\theta_c = -1/(4a)$。将这些解代入第一个方程，就可以求出对应的临界参数值 $r_c$。通过比较不同解得到的 $r_c$ 值，我们可以确定使[分岔](@entry_id:273973)发生的最大或最小参数值，从而描绘出系统行为随参数变化的“[相图](@entry_id:144015)”。

#### [霍普夫分岔](@entry_id:136805)与[振荡](@entry_id:267781)的产生

另一种至关重要的[分岔](@entry_id:273973)是**霍普夫分岔 (Hopf bifurcation)**，它描述了极限环是如何从一个[平衡点](@entry_id:272705)“诞生”的。当一个系统的参数变化，导致[平衡点](@entry_id:272705)的一对复共轭[特征值](@entry_id:154894) $\lambda = \sigma \pm i\omega$ 的实部 $\sigma$ 穿过零点时，霍普夫分岔就可能发生。如果 $\sigma$ 从负变正，原先稳定的[焦点](@entry_id:174388)[平衡点](@entry_id:272705)将失稳，同时在其周围会生成一个小的、稳定的[极限环](@entry_id:274544)。这标志着系统从一个稳定的定常状态转变为持续的[振荡](@entry_id:267781)状态。

在包含时间延迟的系统中，霍普夫分岔尤其常见。考虑一个[延迟反馈](@entry_id:260831)系统 [@problem_id:1149519]，其线性化方程为 $\frac{dx}{dt} = \alpha x(t) - \beta\gamma x(t-\tau)$。我们通过代入特征解 $x(t) \propto e^{\lambda t}$ 来寻找特征方程：
$$
\lambda = \alpha - \beta\gamma e^{-\lambda\tau}
$$
霍普夫分岔的[临界点](@entry_id:144653)是稳定性改变的边界，此时系统恰好处于纯[振荡](@entry_id:267781)状态，对应于一个纯虚[特征值](@entry_id:154894) $\lambda = i\omega$（其中 $\omega$ 是振荡频率）。将它代入特征方程：
$$
i\omega = \alpha - \beta\gamma e^{-i\omega\tau} = \alpha - \beta\gamma(\cos(\omega\tau) - i\sin(\omega\tau))
$$
分离实部和虚部，我们得到一个[方程组](@entry_id:193238)：
$$
\begin{cases}
0 = \alpha - \beta\gamma\cos(\omega\tau) \\
\omega = \beta\gamma\sin(\omega\tau)
\end{cases}
$$
从这两个方程中，我们可以消去延迟 $\tau$。由 $\cos(\omega\tau) = \alpha/(\beta\gamma)$ 和 $\sin(\omega\tau) = \omega/(\beta\gamma)$，利用恒等式 $\cos^2(\cdot)+\sin^2(\cdot)=1$，我们得到：
$$
\left(\frac{\alpha}{\beta\gamma}\right)^2 + \left(\frac{\omega}{\beta\gamma}\right)^2 = 1 \implies \alpha^2 + \omega^2 = (\beta\gamma)^2
$$
由此解出[振荡频率](@entry_id:269468) $\omega = \sqrt{(\beta\gamma)^2 - \alpha^2}$。这个频率就是当延迟 $\tau$ 增加到某个临界值，系统开始出现[振荡](@entry_id:267781)时的固有频率。这一分析是理解和控制[延迟系统](@entry_id:270560)中[振荡](@entry_id:267781)行为的关键。