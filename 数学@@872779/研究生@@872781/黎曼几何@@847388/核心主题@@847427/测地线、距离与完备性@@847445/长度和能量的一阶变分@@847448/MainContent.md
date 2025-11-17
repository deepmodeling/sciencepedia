## 引言
在弯曲的空间中，两点之间最“直”的路径是什么？从地球表面的[大圆](@entry_id:268970)航线到广义相对论中光线在[引力场](@entry_id:169425)中的偏折，黎曼几何通过“[测地线](@entry_id:269969)”这一概念为这个问题提供了优美的解答。然而，如何严谨地定义并找到这些路径呢？现代几何学与物理学的答案植根于一个强大的思想：[变分原理](@entry_id:198028)。该原理将[测地线](@entry_id:269969)刻画为某些几何量（如长度或能量）的“最优”路径，即相应泛函的[临界点](@entry_id:144653)。这种观点不仅为[测地线](@entry_id:269969)理论提供了坚实的分析基础，也揭示了其与物理学、工程学乃至数据科学等众多领域的深刻联系。

本文旨在系统阐述[测地线](@entry_id:269969)的变分理论。我们将从最基本的原理出发，逐步揭示这一思想的威力与广度。在“原理与机制”一章中，我们将详细介绍长度与[能量泛函](@entry_id:170311)，推导它们的一阶变分公式，并阐明作为其欧拉-拉格朗日方程的[测地线方程](@entry_id:264349)。接着，在“应用与交叉学科联系”一章，我们将探索变分原理如何将[测地线](@entry_id:269969)与物理学中的守恒律、力学系统，以及图像处理、[断裂力学](@entry_id:141480)等现代应用联系起来，并讨论解的存在性等关键问题。最后，“动手实践”部分将提供具体的计算练习，帮助读者将理论知识转化为实践技能。通过这趟旅程，读者将深刻理解为何变分法是联结几何学中局域与全局的强大桥梁。

## 原理与机制

在黎曼几何中，连接两点的“最短”路径——[测地线](@entry_id:269969)——是核心研究对象。正如引言中所述，寻找这些路径的现代方法植根于变分法，即将[测地线](@entry_id:269969)刻画为某些几何泛函的[临界点](@entry_id:144653)。本章将深入探讨这一思想的两个基本实例：[长度泛函](@entry_id:203503)与[能量泛函](@entry_id:170311)。我们将推导它们的一阶变分公式，阐明其欧拉-拉格朗
日方程，并揭示两者之间深刻而微妙的联系。

### 长度与能量泛函

给定一个光滑的$n$维[黎曼流形](@entry_id:261160) $(M, g)$，我们考虑一条[几乎处处可微](@entry_id:200712)的曲线 $c: [a,b] \to M$。其[切向量](@entry_id:265494) $\dot{c}(t)$ 的长度（或速率）由度量 $g$ 在点 $c(t)$ 诱导的范数给出：
$$
\|\dot{c}(t)\| := \sqrt{g_{c(t)}(\dot{c}(t), \dot{c}(t))}
$$
基于此，我们定义两个核心的几何泛函：

1.  **[长度泛函](@entry_id:203503) (Length Functional)** $L(c)$，它测量曲线的弧长：
    $$
    L(c) = \int_a^b \|\dot{c}(t)\| \,dt
    $$

2.  **能量泛函 (Energy Functional)** $E(c)$，它测量速率平方的积分：
    $$
    E(c) = \frac{1}{2} \int_a^b g(\dot{c}(t), \dot{c}(t)) \,dt = \frac{1}{2} \int_a^b \|\dot{c}(t)\|^2 \,dt
    $$

为了使[变分法](@entry_id:163656)严谨可行，我们需要确定这些泛函的恰当定义域。对于光滑（$C^1$）曲线，这些积分显然是良定义的。然而，为了理论的完备性与应用的广泛性，我们需要将定义域扩展到更大的函数空间。

一个自然的扩展是考虑**绝对连续曲线 (absolutely continuous curves)**。一条曲线 $c: [a,b] \to M$ 被称为绝对连续的，如果它在任意[局部坐标](@entry_id:181200)卡中的表示都是经典意义下绝对连续的。这类曲线保证了其切向量 $\dot{c}(t)$ [几乎处处](@entry_id:146631)存在，并且其速率 $\|\dot{c}(t)\|$ 是[勒贝格可积](@entry_id:192052)的，即 $\|\dot{c}\| \in L^1([a,b])$。因此，[长度泛函](@entry_id:203503) $L(c)$ 在由所有连接固定端点的绝对连续曲线构成的空间上是良定义的 [@problem_id:2975390]。

对于[能量泛函](@entry_id:170311) $E(c)$，其被积函数是速率的平方。为了保证积分的有限性，我们需要 $\|\dot{c}(t)\|^2$ 是 $L^1$ 可积的，这等价于速率 $\|\dot{c}(t)\|$ 是平方可积的，即 $\|\dot{c}\| \in L^2([a,b])$。满足此条件的曲线构成了所谓的**索博列夫空间 (Sobolev space)** $H^1([a,b], M)$。因此，能量泛函的自然定义域是 $H^1$ 空间。由于在有界区间 $[a,b]$ 上有 $L^2([a,b]) \subset L^1([a,b])$，故任何能量有限的曲线其长度也必定有限 [@problem_id:2975390]。

这两个泛函的一个根本区别在于它们对**[曲线参数化](@entry_id:635915) (reparametrization)** 的反应。[长度泛函](@entry_id:203503)在保持方向的重[参数化](@entry_id:272587)下是不变的。设 $\varphi: [\alpha, \beta] \to [a,b]$ 是一个光滑的、保持方向的重参数化（即 $\varphi'(\tau) > 0$），并令 $\tilde{c}(\tau) = c(\varphi(\tau))$。根据链式法则，$\dot{\tilde{c}}(\tau) = \dot{c}(\varphi(\tau))\varphi'(\tau)$，因此 $\|\dot{\tilde{c}}(\tau)\| = \|\dot{c}(\varphi(\tau))\|\varphi'(\tau)$。通过变量代换 $t = \varphi(\tau)$，我们得到：
$$
L(\tilde{c}) = \int_\alpha^\beta \|\dot{\tilde{c}}(\tau)\| \,d\tau = \int_\alpha^\beta \|\dot{c}(\varphi(\tau))\| \varphi'(\tau) \,d\tau = \int_a^b \|\dot{c}(t)\| \,dt = L(c)
$$
这表明长度是曲线的内在几何属性，不依赖于我们“行进”在曲线上的速度。

相比之下，能量泛函通常不是重[参数化](@entry_id:272587)不变的。对[能量泛函](@entry_id:170311)进行同样的计算会得到：
$$
E(\tilde{c}) = \frac{1}{2} \int_\alpha^\beta \|\dot{\tilde{c}}(\tau)\|^2 \,d\tau = \frac{1}{2} \int_\alpha^\beta \|\dot{c}(\varphi(\tau))\|^2 (\varphi'(\tau))^2 \,d\tau
$$
除非 $\varphi'(\tau) \equiv 1$（即 $\varphi$ 是一个平凡的平移），否则这个积分通常不等于 $E(c)$。例如，在欧氏平面 $\mathbb{R}^2$ 中，考虑曲线 $c(t)=(t,0)$，$t \in [0,1]$。其长度 $L(c)=1$，能量 $E(c)=1/2$。若使用重参数化 $\varphi(t) = t^2$，则新曲线 $\tilde{c}(t)=(t^2,0)$ 的能量为 $E(\tilde{c}) = \frac{1}{2}\int_0^1 \|(2t,0)\|^2 dt = \frac{1}{2}\int_0^1 4t^2 dt = 2/3 \neq E(c)$。[能量泛函](@entry_id:170311)对[参数化](@entry_id:272587)非常敏感，它倾向于选择速率均匀的曲线 [@problem_id:2975419]。这一性质是理解[测地线](@entry_id:269969)理论的关键。

### [变分法](@entry_id:163656)的基本工具

为了计算泛函的“导数”，我们需要引入曲线变分的概念和相应的[微分](@entry_id:158718)工具。

#### 曲线的变分与边界条件

一条光滑曲线 $c: [a,b] \to M$ 的**光滑变分 (smooth variation)** 是一个[光滑映射](@entry_id:203730) $\Gamma: (-\epsilon, \epsilon) \times [a,b] \to M$，使得 $\Gamma(0,t) = c(t)$。我们可以将此想象成一个以 $c$ 为中心的光滑曲线族 $\{\gamma_s(t) = \Gamma(s,t)\}_{s \in (-\epsilon, \epsilon)}$。

在 $s=0$ 处对参数 $s$ 求导，我们得到一个沿着曲线 $c$ 的向量场，称为**变分向量场 (variational vector field)**：
$$
V(t) = \left.\frac{\partial \Gamma}{\partial s}\right|_{s=0}(t) \in T_{c(t)}M
$$
$V(t)$ 描述了曲线 $c$ 在 $t$ 点的“形变”方向与速率。

[变分问题](@entry_id:756445)的设置强烈依赖于**边界条件**。最常见的几种情况包括：
-   **固定端点 (Fixed Endpoints)**：变分过程中曲线的端点保持不动，即 $\Gamma(s,a) = c(a)$ 和 $\Gamma(s,b) = c(b)$ 对所有 $s$ 成立。对 $s$ 求导立即得到 $V(a)=0$ 和 $V(b)=0$ [@problem_id:2975392]。
-   **自由端点 (Free Endpoints)**：端点可以自由移动。在这种情况下，对 $V(a)$ 和 $V(b)$ 不施加任何先验限制。
-   **端点在[子流形](@entry_id:159439)上 (Endpoints on Submanifolds)**：端点被约束在给定的子流形中，例如 $\Gamma(s,a) \in N_a \subset M$。这意味着曲线 $s \mapsto \Gamma(s,a)$ 完全位于 $N_a$ 内。根据切空间的定义，该曲线在 $s=0$ 的[切向量](@entry_id:265494)——即 $V(a)$——必须位于[子流形](@entry_id:159439) $N_a$ 在 $c(a)$ 点的切空间内。因此，条件是 $V(a) \in T_{c(a)}N_a$ 和 $V(b) \in T_{c(b)}N_b$ [@problem_id:2975392] [@problem_id:2975401]。

#### [沿曲线的协变导数](@entry_id:192566)

要对沿曲线的向量场（如 $V(t)$ 或 $\dot{c}(t)$）进行[微分](@entry_id:158718)，我们不能简单地使用普通导数，因为对于不同的 $t_1, t_2$，向量 $W(t_1)$ 和 $W(t_2)$ 属于不同的[切空间](@entry_id:199137) $T_{c(t_1)}M$ 和 $T_{c(t_2)}M$，无法直接相减。[黎曼几何](@entry_id:160508)中的**[协变导数](@entry_id:152476) (covariant derivative)** $\nabla$ 提供了解决方案。

给定一个沿曲线 $c$ 的向量场 $W(t)$，其沿 $c$ 的[协变导数](@entry_id:152476)记为 $\nabla_t W(t)$ 或 $\frac{D}{dt}W(t)$。其严格定义为 $\nabla_{\dot{c}(t)}\widetilde{W}|_{c(t)}$，其中 $\widetilde{W}$ 是 $W$ 在 $c(t)$ 某个邻域上的任意光滑延拓。这个定义不依赖于延拓 $\widetilde{W}$ 的选择。

在[局部坐标](@entry_id:181200) $\{x^i\}$ 中，设 $\dot{c}(t) = \dot{c}^j(t)\frac{\partial}{\partial x^j}$ 和 $W(t) = W^k(t)\frac{\partial}{\partial x^k}$，[协变导数](@entry_id:152476)的分量形式为：
$$
(\nabla_t W)^i(t) = \frac{dW^i}{dt}(t) + \Gamma^i_{jk}(c(t)) \dot{c}^j(t) W^k(t)
$$
其中 $\Gamma^i_{jk}$ 是[列维-奇维塔联络](@entry_id:161107)（Levi-Civita connection）的[克里斯托费尔符号](@entry_id:159831) (Christoffel symbols)。这个公式直观地展示了协变导数由普通导数和一项“修正项”组成，后者解释了[基向量](@entry_id:199546) $\frac{\partial}{\partial x^k}$ 随位置的变化 [@problem_id:2975416]。

[沿曲线的协变导数](@entry_id:192566)满足两个关键性质：
1.  **关于函数的[莱布尼茨法则](@entry_id:157949) (Leibniz Rule for Functions)**：对任意光滑函数 $f: [a,b] \to \mathbb{R}$，有 $\nabla_t(fW) = \frac{df}{dt}W + f\nabla_t W$。
2.  **[度量兼容性](@entry_id:265910) (Metric Compatibility)**：对任意两个沿 $c$ 的向量场 $W, Z$，有
    $$
    \frac{d}{dt}g(W,Z) = g(\nabla_t W, Z) + g(W, \nabla_t Z)
    $$
    这个性质意味着，协变导数与度量 $g$ 可以“交换”。特别地，它告诉我们向量场长度的变化率与它的协变导数有关：$\frac{d}{dt}\|W\|^2 = 2g(\nabla_t W, W)$ [@problem_id:2975416]。

#### 协变导数的[交换性](@entry_id:140240)

在推导变分公式时，一个至关重要的技术引理是[协变导数](@entry_id:152476)对于变分参数 $s$ 和曲线参数 $t$ 的[交换性](@entry_id:140240)。对于光滑变分 $\Gamma(s,t)$，我们有：
$$
\nabla_s \partial_t \Gamma = \nabla_t \partial_s \Gamma
$$
这里 $\nabla_s$ 和 $\nabla_t$ 分别表示沿 $s$-[参数曲线](@entry_id:634039)和 $t$-[参数曲线](@entry_id:634039)的协变导数。这个等式源于[列维-奇维塔联络](@entry_id:161107)的**无挠性 (torsion-free)** 特征，以及普通偏导数的交换性 $\frac{\partial^2}{\partial s \partial t} = \frac{\partial^2}{\partial t \partial s}$。在[局部坐标](@entry_id:181200)中，这表现为[克里斯托费尔符号](@entry_id:159831)的对称性 $\Gamma^i_{jk} = \Gamma^i_{kj}$ [@problem_id:2975377]。这个性质允许我们在计算中自由交换求导顺序，是连接变分场 $V$ 和曲线速度 $\dot{\gamma}$ 的桥梁。

### 长度与能量的一阶变分

现在我们具备了所有工具来计算长度和[能量泛函](@entry_id:170311)的一阶变分，即它们在 $s=0$ 处对变分参数 $s$ 的导数。我们将考虑最常见的情形：具有固定端点的变分。

#### 能量的一阶变分

能量泛函为 $E(s) = \frac{1}{2}\int_a^b g(\partial_t \Gamma, \partial_t \Gamma) dt$。对其求导：
$$
\frac{dE}{ds} = \frac{1}{2} \int_a^b \frac{\partial}{\partial s} g(\partial_t \Gamma, \partial_t \Gamma) \,dt = \int_a^b g(\nabla_s \partial_t \Gamma, \partial_t \Gamma) \,dt
$$
接着，利用协变导数的[交换性](@entry_id:140240) $\nabla_s \partial_t \Gamma = \nabla_t \partial_s \Gamma$，我们得到：
$$
\frac{dE}{ds} = \int_a^b g(\nabla_t \partial_s \Gamma, \partial_t \Gamma) \,dt
$$
在 $s=0$ 处计算，$\partial_s \Gamma|_{s=0} = V(t)$ 且 $\partial_t \Gamma|_{s=0} = \dot{c}(t)$。因此，一阶变分 $\delta E = \left.\frac{dE}{ds}\right|_{s=0}$ 为：
$$
\delta E = \int_a^b g(\nabla_t V, \dot{c}) \,dt
$$
最后，我们使用[分部积分法](@entry_id:136350)。利用[度量兼容性](@entry_id:265910)导出的积分法则 $g(\nabla_t V, \dot{c}) = \frac{d}{dt}g(V, \dot{c}) - g(V, \nabla_t \dot{c})$，我们有：
$$
\delta E = \int_a^b \left( \frac{d}{dt}g(V, \dot{c}) - g(V, \nabla_t \dot{c}) \right) dt = \left[g(V, \dot{c})\right]_a^b - \int_a^b g(V, \nabla_t \dot{c}) \,dt
$$
由于是固定端点变分，$V(a)=V(b)=0$，边界项消失。我们最终得到**能量的一阶变分公式** [@problem_id:2975417]：
$$
\delta E = - \int_a^b g(V, \nabla_t \dot{c}) \,dt
$$

#### 长度的一阶变分

[长度泛函](@entry_id:203503) $L(s) = \int_a^b \|\partial_t \Gamma\| dt$ 的计算类似，但需要多一步[链式法则](@entry_id:190743)。
$$
\frac{dL}{ds} = \int_a^b \frac{\partial}{\partial s} \sqrt{g(\partial_t \Gamma, \partial_t \Gamma)} \,dt = \int_a^b \frac{g(\nabla_s \partial_t \Gamma, \partial_t \Gamma)}{\|\partial_t \Gamma\|} \,dt
$$
在 $s=0$ 处计算，并记[单位切向量](@entry_id:262985)为 $T(t) = \dot{c}(t) / \|\dot{c}(t)\|$（假设曲线是正则的，即 $\|\dot{c}(t)\| > 0$），我们得到：
$$
\delta L = \int_a^b g(\nabla_t V, T) \,dt
$$
与能量变分完全相同的[分部积分](@entry_id:136350)步骤给出了**长度的一阶变分公式** [@problem_id:2975417]：
$$
\delta L = - \int_a^b g(V, \nabla_t T) \,dt
$$

### 作为[临界点](@entry_id:144653)的[测地线](@entry_id:269969)

一阶变分公式是寻找泛函[临界点](@entry_id:144653)的关键。一条曲线 $c$ 是一个泛函（如 $L$ 或 $E$）的**[临界点](@entry_id:144653) (critical point)**，如果对于所有容许的变分向量场 $V$，其一阶变分 $\delta L$ 或 $\delta E$ 都为零。根据变分法基本引理，这要求积分号下的部分 $g(\cdot, \cdot)$ 对于任意 $V$ 恒为零，这意味着括号内的第二个向量参数必须为零。

#### 欧拉-拉格朗日方程

从能量的一阶变分公式 $\delta E = - \int g(V, \nabla_t \dot{c}) dt = 0$，我们得到[能量泛函](@entry_id:170311)的欧拉-拉格朗日方程：
$$
\nabla_t \dot{c} = 0
$$
这个方程被称为**[测地线方程](@entry_id:264349) (geodesic equation)**。它表明，作为能量[临界点](@entry_id:144653)的曲线，其速度向量场沿自身是[平行输运](@entry_id:160671)的。换句话说，它的加速度向量为零。一个直接的推论是，[测地线](@entry_id:269969)的速率是常数，因为 $\frac{d}{dt}\|\dot{c}\|^2 = 2g(\nabla_t \dot{c}, \dot{c}) = 2g(0, \dot{c}) = 0$。因此，[能量泛函](@entry_id:170311)的[临界点](@entry_id:144653)是**常速[测地线](@entry_id:269969)**。

从长度的一阶变分公式 $\delta L = - \int g(V, \nabla_t T) dt = 0$，我们得到[长度泛函](@entry_id:203503)的欧拉-拉格朗日方程：
$$
\nabla_t T = 0
$$
其中 $T = \dot{c}/\|\dot{c}\|$ 是[单位切向量](@entry_id:262985)。这个方程表明，作为长度[临界点](@entry_id:144653)的曲线，其[单位切向量](@entry_id:262985)场沿自身是平行输运的。

#### 长度与能量[临界点](@entry_id:144653)之间的差异与调和

乍一看，这两个方程似乎不同。让我们来分析长度的[欧拉-拉格朗日方程](@entry_id:137827) $\nabla_t T=0$：
$$
\nabla_t \left( \frac{\dot{c}}{\|\dot{c}\|} \right) = \left( \frac{d}{dt}\frac{1}{\|\dot{c}\|} \right) \dot{c} + \frac{1}{\|\dot{c}\|} \nabla_t \dot{c} = -\frac{\|\dot{c}\|'}{\|\dot{c}\|^2}\dot{c} + \frac{1}{\|\dot{c}\|} \nabla_t \dot{c} = 0
$$
整理后得到：
$$
\nabla_t \dot{c} = \frac{\|\dot{c}\|'}{\|\dot{c}\|} \dot{c}
$$
这个方程表明，长度[临界曲线](@entry_id:203397)的加速度向量 $\nabla_t \dot{c}$ 必须与其速度向量 $\dot{c}$ 平行。这样的曲线被称为**前[测地线](@entry_id:269969) (pre-geodesic)**。它们的几何轨迹与[测地线](@entry_id:269969)完全相同，但其[参数化](@entry_id:272587)（即沿曲线移动的速度）可以是任意的，只要加速度始终保持在[切线](@entry_id:268870)方向即可 [@problem_id:2975395]。

这种差异的根源在于[长度泛函](@entry_id:203503)的**[重参数化不变性](@entry_id:197540)**。因为 $L(c)$ 不依赖于参数化的速度，所以它对那些仅仅改变参数化速度的切向变分“视而不见”。因此，通过最小化长度，我们只能确定曲线的几何形状，而无法唯一确定其参数化。这在[变分问题](@entry_id:756445)中被称为一种“[规范自由度](@entry_id:160491)” (gauge freedom) [@problem_id:2975404]。

相反，[能量泛函](@entry_id:170311)不是重[参数化](@entry_id:272587)不变的，它“惩罚”了非均匀的速率。因此，最小化能量不仅能找到[测地线](@entry_id:269969)的几何轨迹，还能自动选出一个“最佳”的参数化——常速参数化。

有两种标准方法来处理[长度泛函](@entry_id:203503)的这种“退化”：
1.  **固定参数化**：在变分之前，先将研究范围限制在具有特定[参数化](@entry_id:272587)的曲线上，最自然的选择是**单位速率**（或弧长）[参数化](@entry_id:272587)。如果 $\|\dot{c}\|=1$，则 $\|\dot{c}\|'=0$，长度的欧拉-拉格朗日方程 $\nabla_t \dot{c} = \frac{\|\dot{c}\|'}{\|\dot{c}\|} \dot{c}$ 就简化为测地线方程 $\nabla_t \dot{c}=0$。
2.  **转而使用[能量泛函](@entry_id:170311)**：由于[能量泛函](@entry_id:170311)的[临界点](@entry_id:144653)（常速[测地线](@entry_id:269969)）的轨迹与[长度泛函](@entry_id:203503)的[临界点](@entry_id:144653)（前[测地线](@entry_id:269969)）完全相同，并且能量泛函的[欧拉-拉格朗日方程](@entry_id:137827)更简洁、非退化，因此在实践中，人们常常通过寻找[能量泛函](@entry_id:170311)的[临界点](@entry_id:144653)来研究[测地线](@entry_id:269969) [@problem_id:2975404]。

这两种方法的深刻联系可以通过比较单位速率下的一阶变分公式来揭示。如果我们假设中心曲线 $c(t)$ 已经按[单位速率参数化](@entry_id:634139)，即 $\|\dot{c}(t)\|=1$，那么 $T=\dot{c}$。此时，长度的一阶变分公式变为：
$$
\delta L = -\int_a^b g(V, \nabla_t \dot{c}) \,dt
$$
这与能量的一阶变分公式完全相同！[@problem_id:2975403]。这从根本上说明了，对于[单位速率曲线](@entry_id:635194)族而言，长度和能量的[变分问题](@entry_id:756445)是等价的。这也为我们使用在代数上更简单的[能量泛函](@entry_id:170311)来研究本质上是长度最小化问题的[测地线](@entry_id:269969)提供了坚实的理论基础。