## 引言
在黎曼几何的探索中，[测地线](@entry_id:269969)作为[欧几里得空间](@entry_id:138052)中“直线”的推广，构成了研究[弯曲空间几何](@entry_id:198138)结构的基本骨架。我们或许已通过平行输运的直观概念认识了[测地线](@entry_id:269969)，即那些“尽可能直”的路径。然而，是否存在一种更深刻、更具分析性的方式来精确捕捉其本质？本文旨在回答这一问题，它将揭示[测地线](@entry_id:269969)的一个核心特性：它们是连接两点的所有路径中，使“能量”这一物理量达到平稳的特殊路径。

本文将带领读者深入变分法的世界，以一种全新的视角重新审视[测地线](@entry_id:269969)。我们将不再仅仅依赖于几何直观，而是通过严谨的分析工具，将寻找[测地线](@entry_id:269969)的问题转化为一个泛函极值问题。通过这一旅程，你将学习到：

在“原理和机制”一章，我们将建立核心的数学框架。我们将定义曲线的能量泛函，并推导其在微小扰动下的一阶变分公式。这一过程将揭示一个惊人的结果：[能量泛函](@entry_id:170311)的[临界点](@entry_id:144653)所满足的[欧拉-拉格朗日方程](@entry_id:137827)，正是我们所熟知的[测地线方程](@entry_id:264349)。

接着，在“应用与跨学科联系”一章，我们将把这一理论付诸实践。通过分析球面、环面等具体空间中的[测地线](@entry_id:269969)，我们将看到变分原理的威力。更重要的是，我们将探索这一思想如何与[物理学中的对称性](@entry_id:144576)与守恒律（[诺特定理](@entry_id:145690)）以及[最优控制理论](@entry_id:139992)中的边界问题交相辉映。

最后，在“动手实践”部分，你将有机会通过解决具体问题来巩固所学知识，将抽象的变分公式转化为具体的计算，从而真正掌握这一强大的几何分析工具。

现在，让我们从构建[变分问题](@entry_id:756445)的舞台开始，正式进入“原理和机制”的探索。

## 原理和机制

[黎曼流形](@entry_id:261160)上的[测地线](@entry_id:269969)是欧几里得空间中“直线”的推广，可以直观地理解为沿着自身[切向量](@entry_id:265494)场平行移动的曲线。在本章中，我们将建立一个更深刻、更具分析性的[测地线](@entry_id:269969)刻画。我们将使用[变分法](@entry_id:163656)这一强大的数学工具，将[测地线](@entry_id:269969)描述为连接两点的所有曲线中，某个特定泛函的“[临界点](@entry_id:144653)”。这个泛函就是[能量泛函](@entry_id:170311)。通过推导[能量的第一变分](@entry_id:635793)公式，我们将证明测地线方程正是其对应的欧拉-拉格朗日方程。这一方法不仅为[测地线](@entry_id:269969)提供了坚实的分析基础，也揭示了它与[长度泛函](@entry_id:203503)以及物理世界中[作用量原理](@entry_id:154742)的深刻联系。

### [变分问题](@entry_id:756445)的舞台：曲线、泛函与变分

在[黎曼几何](@entry_id:160508)中，我们常常关心曲线的各种几何性质，其中最基本的莫过于其长度。然而，从[变分法](@entry_id:163656)的角度看，另一个密切相关的量——能量，在数学上更为便捷和深刻。

#### 衡量曲线：长度与能量泛函

令 $(M,g)$ 为一个光滑黎曼流形，$\gamma: [a, b] \to M$ 为其上的一条分段光滑曲线。其速度向量为 $\dot{\gamma}(t) \in T_{\gamma(t)}M$。在任意一点 $p \in M$，黎曼度量 $g_p$ 定义了[切空间](@entry_id:199137) $T_pM$ 上的一个[内积](@entry_id:158127)。由此，我们可以定义曲线在 $t$ 时刻的 **速率** (speed)，即其速度[向量的范数](@entry_id:154882)：
$$
|\dot{\gamma}(t)| = \sqrt{g_{\gamma(t)}(\dot{\gamma}(t), \dot{\gamma}(t))}
$$
曲线的总长度自然就是速率在整个时间区间上的积分。因此，我们定义**[长度泛函](@entry_id:203503)** (length functional) $L(\gamma)$ 为：
$$
L(\gamma) = \int_a^b |\dot{\gamma}(t)| \,dt = \int_a^b \sqrt{g_{\gamma(t)}(\dot{\gamma}(t), \dot{\gamma}(t))} \,dt
$$
在经典力学中，一个质点的动能正比于其速率的平方。受此启发，在[黎曼几何](@entry_id:160508)中，我们定义曲线的**能量拉格朗日量** (energy Lagrangian) 为速率平方的一半。通过对这个[拉格朗日量](@entry_id:174593)进行积分，我们得到曲线的**能量泛函** (energy functional) $E(\gamma)$ [@problem_id:3046480]：
$$
E(\gamma) = \frac{1}{2} \int_a^b |\dot{\gamma}(t)|^2 \,dt = \frac{1}{2} \int_a^b g_{\gamma(t)}(\dot{\gamma}(t), \dot{\gamma}(t)) \,dt
$$
乍一看，[长度泛函](@entry_id:203503)似乎是更自然的研究对象。然而，[能量泛函](@entry_id:170311)的被积函数是 $\dot{\gamma}(t)$ 的二次[齐次多项式](@entry_id:178156)，而[长度泛函](@entry_id:203503)的被积函数带有一个平方根。这个小小的差异使得[能量泛函](@entry_id:170311)在求导和变分计算中表现出更好的性质，避免了处理平方根可能带来的奇异性（例如在 $\dot{\gamma}(t)=0$ 的点）。我们将在后续的讨论中看到，通过研究[能量泛函](@entry_id:170311)的[临界点](@entry_id:144653)，我们同样可以有效地找到长度最短的曲线。

#### 变分的概念

[变分法](@entry_id:163656)的核心思想是研究当一个函数（在这里是曲线 $\gamma$）发生微小“扰动”时，一个依赖于该函数的量（泛函 $L(\gamma)$ 或 $E(\gamma)$）如何变化。为了精确地描述这种扰动，我们引入**光滑变分** (smooth variation) 的概念。

给定一条光滑曲线 $\gamma: [a, b] \to M$，它的一个光滑变分是一个[光滑映射](@entry_id:203730) $\Gamma: (-\epsilon, \epsilon) \times [a, b] \to M$，其中 $\epsilon > 0$ 是一个小数，且满足以下条件 [@problem_id:3046509]：
1.  当变分参数 $s=0$ 时，映射与原曲线一致，即 $\Gamma(0, t) = \gamma(t)$ 对所有 $t \in [a, b]$ 成立。
2.  对于每一个固定的 $s \in (-\epsilon, \epsilon)$，映射 $t \mapsto \Gamma(s, t)$ 都是一条光滑曲线。我们常记这条“变动后的”曲线为 $\gamma_s(t) = \Gamma(s, t)$。

这个映射 $\Gamma$ 可以被看作一个以 $s$ 为参数的曲线族，其中 $\gamma_0 = \gamma$ 是我们研究的中心曲线。当我们考虑连接两个[固定点](@entry_id:156394) $p, q$ 的曲线时，我们自然要求所有的变动曲线都保持相同的端点。这被称为**固定端点条件** (fixed-endpoint condition)：
$$
\Gamma(s, a) = \gamma(a) = p \quad \text{且} \quad \Gamma(s, b) = \gamma(b) = q \quad \text{对所有 } s \in (-\epsilon, \epsilon)
$$
与此相对，如果端点 $\Gamma(s, a)$ 和 $\Gamma(s, b)$ 可以随着 $s$ 自由变化，我们则称之为**自由端点变分** (free-endpoint variation) [@problem_id:3046481]。

变分在 $t$ 点产生的“[无穷小位移](@entry_id:202209)”由**变分向量场** (variational vector field) $V(t)$ 描述。它定义为变分曲线在 $s=0$ 时对参数 $s$ 的偏导数，即在每个点 $\gamma(t)$ 处，变动方向的“速度”：
$$
V(t) = \left. \frac{\partial \Gamma}{\partial s} \right|_{s=0}(t) \in T_{\gamma(t)}M
$$
对于固定端点变分，由于端点位置不随 $s$ 变化，变分向量场在端点处必然为零。这是因为 $s \mapsto \Gamma(s, a)$ 是一个常值映射（到点 $p$），其导数自然是零向量。因此，固定端点条件等价于对变分向量场的边界条件 [@problem_id:3046515]：
$$
V(a) = 0 \quad \text{且} \quad V(b) = 0
$$
这个条件在后续的推导中至关重要。

### [能量的第一变分](@entry_id:635793)与[测地线方程](@entry_id:264349)

现在我们具备了所有必要的工具，可以开始本章的核心任务：计算能量泛函 $E(\gamma_s)$ 对变分参数 $s$ 的一阶导数，并找出其为零的条件。这个过程被称为计算**[第一变分](@entry_id:174697)** (first variation)。

#### 推导[第一变分](@entry_id:174697)公式

考虑一个固定端点的光滑变分 $\Gamma(s, t)$。变动曲线 $\gamma_s(t)$ 的能量为：
$$
E(s) = E(\gamma_s) = \frac{1}{2} \int_a^b g(\dot{\gamma}_s(t), \dot{\gamma}_s(t)) \,dt
$$
这里 $\dot{\gamma}_s(t) = \frac{\partial \Gamma}{\partial t}(s, t)$。我们想计算 $\left. \frac{dE}{ds} \right|_{s=0}$。由于 $\Gamma$ 是光滑的，我们可以将求导运算移到积分号内部：
$$
\frac{dE}{ds} = \frac{1}{2} \int_a^b \frac{\partial}{\partial s} g(\dot{\gamma}_s, \dot{\gamma}_s) \,dt
$$
黎曼几何中的一个关键工具是与度量 $g$ 相容的**列维-奇维塔联络** (Levi-Civita connection) $\nabla$。它的**度量相容性** (metric compatibility) 意味着 $\nabla g = 0$，这可以用乘法法则的形式表达：对于任意向量场 $X, Y, Z$，都有 $Z(g(X, Y)) = g(\nabla_Z X, Y) + g(X, \nabla_Z Y)$。令 $Z = \frac{\partial}{\partial s}$ 和 $X=Y=\dot{\gamma}_s$，我们得到：
$$
\frac{\partial}{\partial s} g(\dot{\gamma}_s, \dot{\gamma}_s) = 2 g(\nabla_{\partial/\partial s} \dot{\gamma}_s, \dot{\gamma}_s)
$$
代入积分中，并记 $T = \dot{\gamma}_s = \frac{\partial \Gamma}{\partial t}$ 和 $V_s = \frac{\partial \Gamma}{\partial s}$，我们有：
$$
\frac{dE}{ds} = \int_a^b g(\nabla_{V_s} T, T) \,dt
$$
[列维-奇维塔联络](@entry_id:161107)的另一个基本性质是**无挠性** (torsion-free)。对于参[数域](@entry_id:155558) $(s, t)$ 上的[坐标向量](@entry_id:153319)场 $\frac{\partial}{\partial s}$ 和 $\frac{\partial}{\partial t}$，它们的[李括号](@entry_id:636461)为零。无挠性意味着 $\nabla_{V_s} T - \nabla_T V_s = [V_s, T] = 0$，因此我们可以交换[协变导数](@entry_id:152476)的顺序：
$$
\nabla_{V_s} T = \nabla_T V_s
$$
将此代入并设置 $s=0$ (此时 $T=\dot{\gamma}$, $V_s=V$)，[第一变分](@entry_id:174697)变为：
$$
\delta E = \left. \frac{dE}{ds} \right|_{s=0} = \int_a^b g(\nabla_{\dot{\gamma}} V, \dot{\gamma}) \,dt
$$
接下来是关键的一步：**[分部积分](@entry_id:136350)**。沿曲线 $\gamma$ 的[协变导数](@entry_id:152476)满足一个乘法法则：$\frac{d}{dt} g(V, \dot{\gamma}) = g(\nabla_{\dot{\gamma}} V, \dot{\gamma}) + g(V, \nabla_{\dot{\gamma}} \dot{\gamma})$。于是：
$$
g(\nabla_{\dot{\gamma}} V, \dot{\gamma}) = \frac{d}{dt} g(V, \dot{\gamma}) - g(V, \nabla_{\dot{\gamma}} \dot{\gamma})
$$
对上式两边积分，我们得到：
$$
\delta E = \int_a^b \left( \frac{d}{dt} g(V, \dot{\gamma}) \right) dt - \int_a^b g(V, \nabla_{\dot{\gamma}} \dot{\gamma}) \,dt
$$
根据[微积分基本定理](@entry_id:201377)，第一项变为一个边界项：
$$
\delta E = \left[ g(V(t), \dot{\gamma}(t)) \right]_a^b - \int_a^b g(V, \nabla_{\dot{\gamma}} \dot{\gamma}) \,dt
$$
由于我们考虑的是固定端点变分，我们有 $V(a)=0$ 和 $V(b)=0$。因此，边界项自动消失 [@problem_id:3046515]。我们最终得到了固定端点变分下能量泛函的[第一变分](@entry_id:174697)公式 [@problem_id:3046485]：
$$
\delta E = - \int_a^b g(V(t), \nabla_{\dot{\gamma}} \dot{\gamma}(t)) \,dt
$$

#### [测地线](@entry_id:269969)作为能量的[临界点](@entry_id:144653)

如果一条曲线 $\gamma$ 是能量泛函的**[临界点](@entry_id:144653)** (critical point) 或**驻点** (stationary point)，意味着对于任何无穷小的扰动（即任何满足条件的变分向量场 $V$），能量的一阶变化量 $\delta E$ 都为零。
$$
\delta E = - \int_a^b g(V(t), \nabla_{\dot{\gamma}} \dot{\gamma}(t)) \,dt = 0 \quad \text{对所有容许的 } V \text{ 成立}
$$
根据变分法基本引理，如果一个[连续函数](@entry_id:137361)（此处为 $\nabla_{\dot{\gamma}}\dot{\gamma}$）与任意一个在边界点为零的光滑函数（此处为 $V$）的[内积](@entry_id:158127)的积分为零，那么这个[连续函数](@entry_id:137361)本身必须处处为零。因此，我们得到：
$$
\nabla_{\dot{\gamma}} \dot{\gamma} = 0
$$
这个方程被称为**[测地线方程](@entry_id:264349)** (geodesic equation)。它精确地表达了我们在引言中给出的直观定义：一条曲线是[测地线](@entry_id:269969)，当且仅当它的速度向量场沿着自身是平行移动的，即其**协变加速度** (covariant acceleration) 为零。

这个结果意义重大：它将一个纯粹的几何概念（“最直的”曲线）与一个分析概念（[能量泛函](@entry_id:170311)的[临界点](@entry_id:144653)）等同起来。寻找[测地线](@entry_id:269969)的问题，现在转化为了一个求解[二阶常微分方程](@entry_id:204212)组的问题。

#### [局部坐标](@entry_id:181200)下的计算

为了更具体地理解上述推导，我们可以在[局部坐标](@entry_id:181200)中进行计算。在一个[局部坐标](@entry_id:181200)图 $(x^1, \dots, x^n)$ 中，度量[张量表示](@entry_id:180492)为矩阵 $(g_{ij})$，黎曼联络由**[克里斯托费尔符号](@entry_id:159831)** (Christoffel symbols) $\Gamma^k_{ij}$ 描述。曲线 $\gamma(t)$ 及其导数可以写成坐标分量形式 $\gamma(t) = (\gamma^1(t), \dots, \gamma^n(t))$ 和 $\dot{\gamma}(t) = (\dot{\gamma}^1(t), \dots, \dot{\gamma}^n(t))$。

[协变](@entry_id:634097)加速度 $\nabla_{\dot{\gamma}}\dot{\gamma}$ 的第 $k$ 个分量为：
$$
(\nabla_{\dot{\gamma}}\dot{\gamma})^k = \ddot{\gamma}^k + \sum_{i,j=1}^n \Gamma^k_{ij}(\gamma(t)) \dot{\gamma}^i \dot{\gamma}^j
$$
因此，[测地线方程](@entry_id:264349) $\nabla_{\dot{\gamma}}\dot{\gamma}=0$ 展开为一个包含 $n$ 个[二阶常微分方程](@entry_id:204212)的[方程组](@entry_id:193238)：
$$
\ddot{\gamma}^k + \sum_{i,j=1}^n \Gamma^k_{ij}(\gamma(t)) \dot{\gamma}^i \dot{\gamma}^j = 0, \quad k=1, \dots, n
$$
通过[第一变分](@entry_id:174697)公式的[局部坐标](@entry_id:181200)推导，可以验证这个结果 [@problem_id:3046513]。对于给定的黎曼度量，我们可以计算出其[克里斯托费尔符号](@entry_id:159831)，然后代入上述[方程组](@entry_id:193238)，从而求解出具体的[测地线](@entry_id:269969)。例如，在欧几里得空间 $\mathbb{R}^n$ 中，标准度量的所有 $g_{ij}$ 都是常数，因此所有 $\Gamma^k_{ij}=0$，[测地线方程](@entry_id:264349)简化为 $\ddot{\gamma}^k=0$，其解是直线 $\gamma(t) = at+b$，这与我们的直觉完全相符。

### [测地线](@entry_id:269969)的性质与刻画

将[测地线](@entry_id:269969)确立为能量泛函的[临界点](@entry_id:144653)，为我们提供了一个强大的视角来探索其更深层次的性质。

#### 能量、长度与参数化

我们选择能量泛函而非[长度泛函](@entry_id:203503)进行变分计算，主要是为了数学上的便利。现在我们来审视这两个泛函与[曲线参数化](@entry_id:635915)的关系。

[长度泛函](@entry_id:203503) $L(\gamma)$ 具有一个重要的性质：**[参数化](@entry_id:272587)不变性**。如果我们对曲线 $\gamma:[a, b] \to M$ 进行一个光滑的、保持定向的重参数化 $\tilde{\gamma} = \gamma \circ \phi$，其中 $\phi: [c, d] \to [a, b]$ 是一个严格递增的满射，那么新曲线的长度与原曲线完全相同，$L(\tilde{\gamma}) = L(\gamma)$。这符合我们的直觉：曲线的几何长度不应依赖于我们以何种速度沿着它走。

然而，能量泛函 $E(\gamma)$ 却**依赖于[参数化](@entry_id:272587)** [@problem_id:3046511]。直观上，以更快的速度走过相同的路径会消耗更多的能量。具体而言，可以证明在所有具有相同路径（像）的参数化中，能量泛函取到最小值的当且仅当曲线是以**常速率** (constant speed) 参数化的。这可以通过柯西-[施瓦茨不等式](@entry_id:202153)证明。

这一区别带来了重要的推论 [@problem_id:3046514]：
1.  对于**能量泛函 $E$**，任何光滑曲线（无论其速率如何）是其[临界点](@entry_id:144653)，当且仅当它满足[测地线方程](@entry_id:264349) $\nabla_{\dot{\gamma}}\dot{\gamma}=0$。并且，一个必然的推论是，任何能量泛函的[临界点](@entry_id:144653)（即[测地线](@entry_id:269969)）都必须具有恒定的速率。这是因为 $\frac{d}{dt}|\dot{\gamma}|^2 = 2 g(\nabla_{\dot{\gamma}}\dot{\gamma}, \dot{\gamma})$，若 $\nabla_{\dot{\gamma}}\dot{\gamma}=0$，则速率的平方不随时间改变。
2.  对于**[长度泛函](@entry_id:203503) $L$**，情况则更微妙。只有当一条曲线**已经被假定为常速[率参数](@entry_id:265473)化**时，它作为[长度泛函](@entry_id:203503)的[临界点](@entry_id:144653)才等价于满足测地线方程。对于非恒定速率的曲线，作为[长度泛函](@entry_id:203503)的[临界点](@entry_id:144653)仅意味着其协变加速度向量必须与其速度向量平行，这比[测地线方程](@entry_id:264349)（要求[协变](@entry_id:634097)加速度为零）要弱。

因此，能量泛函提供了一个更直接和普适的变分原理来刻画[测地线](@entry_id:269969)，它自动地为我们筛选出了具有“良好”[参数化](@entry_id:272587)（即常速率）的曲线。

#### 测地线方程的[不变性](@entry_id:140168)

我们已经看到，[测地线](@entry_id:269969)的几何路径不应依赖于参数化，但[测地线方程](@entry_id:264349) $\nabla_{\dot{\gamma}}\dot{\gamma}=0$ 呢？事实证明，这个方程并非在任意重参数化下都保持形式不变。

可以证明，[测地线方程](@entry_id:264349)在且仅在**仿射重[参数化](@entry_id:272587)** (affine reparametrization) 下保持不变 [@problem_id:3046496]。仿射重参数化是指形式为 $t \mapsto as+b$ 的变换，其中 $a, b$ 是常数且 $a \neq 0$。如果 $\gamma(t)$ 是一条[测地线](@entry_id:269969)，并且我们定义 $\tilde{\gamma}(s) = \gamma(as+b)$，那么 $\tilde{\gamma}(s)$ 同样满足测地线方程（在其自身的参数 $s$ 下）。这可以通过直接计算协变加速度的变换规律得到，也可以从能量泛函的[缩放性质](@entry_id:273821)看出。

这一性质告诉我们，一条“[测地线](@entry_id:269969)”严格来说不是单指一条[参数化](@entry_id:272587)曲线，而是指由所有仿射重[参数化](@entry_id:272587)关联起来的一族等价的[参数化](@entry_id:272587)曲线。它们描绘了[流形](@entry_id:153038)上相同的几何路径。

#### 能量最小化与长度最小化

最后，我们来阐明[能量最小化](@entry_id:147698)、长度最小化与[测地线](@entry_id:269969)之间的最终联系。我们已经知道，在连接两点的所有曲线中，[测地线](@entry_id:269969)是[能量泛函](@entry_id:170311)的[临界点](@entry_id:144653)。但它们是最小值点吗？并且，这与长度最小化有什么关系？

考虑连接两点 $p, q$ 的所有光滑曲线。
1.  一个重要的结论是：在给定时间区间 $[0, T]$ 内连接 $p, q$ 的曲线中，如果一条曲线 $\gamma$ 使得能量泛函 $E(\gamma)$ 达到最小值，那么这条曲线不仅是一条[测地线](@entry_id:269969)，而且它也必然是连接 $p, q$ 的**长度最短**的曲线之一 [@problem_id:3046484]。
2.  反过来，任何一条连接 $p, q$ 的长度最短的曲线，都可以被（以常速率）重参数化，使其成为在某个固定时间区间上能量最小的曲线。

这个[等价关系](@entry_id:138275)是极其深刻的。它意味着，我们最初为了寻找长度最短的路径而提出的问题，可以通过寻找能量泛函的[临界点](@entry_id:144653)（即[求解测地线](@entry_id:180752)方程）来解决。[能量泛函](@entry_id:170311)，这个看似更“物理”和“分析”的工具，最终为我们通向纯粹几何的“最短路径”概念铺平了道路。这正是变分法在现代几何中的威力所在。