## 引言
在[数学物理](@entry_id:265403)和工程领域，非齐次[线性偏微分方程](@entry_id:172517)（PDE）是描述从[电磁场](@entry_id:265881)到热量[扩散](@entry_id:141445)等众多现象的基础。然而，当这些方程与复杂的边界条件相结合时，求解过程往往变得异常困难。[格林函数](@entry_id:147802)（Green's function）应运而生，它提供了一种系统而强大的思想框架，将求解微分方程的挑战巧妙地转化为一个积分问题，从而大大简化了分析和计算。本文旨在深入探讨[拉普拉斯算子](@entry_id:146319)（Laplacian）的[格林函数](@entry_id:147802)，它是势理论和许[多稳态](@entry_id:180390)物理问题的核心。

本文旨在填补从抽象定义到实际应用之间的知识鸿沟。许多学习者了解[格林函数](@entry_id:147802)的定义，却难以将其与直观的物理图像和具体的解题策略联系起来。通过本文的学习，读者将全面掌握格林函数的理论与实践。我们将从以下三个层面展开：
- **原理与机制**：本章将追溯[格林函数](@entry_id:147802)的物理起源——[点源](@entry_id:196698)响应，阐明其数学定义，探讨其与基本解的关系，并详细介绍其对称性和符号等关键性质。我们将重点讲解用于构造格林函数的经典“[镜像法](@entry_id:163138)”，并分析其适用性与局限性。
- **应用与跨学科联系**：本章将展示格林函数如何在静电学、[热传导](@entry_id:147831)和[流体力学](@entry_id:136788)等领域大放异彩。通过具体的物理情境，读者将看到[镜像法](@entry_id:163138)等工具如何被用来解决实际问题，并领略[格林函数](@entry_id:147802)思想如何与概率论、相对论[场论](@entry_id:155241)等更深层次的理论产生共鸣。
- **动手实践**：本章提供了一系列精心设计的练习，引导读者亲手验证格林函数的性质、应用镜像法构造解，从而将理论知识内化为扎实的解题技能。

让我们首先进入第一章，深入探索格林函数的基本原理与内在机制，为后续的应用和实践打下坚实的基础。

## 原理与机制

在[偏微分方程](@entry_id:141332)的研究中，[格林函数](@entry_id:147802)（Green's function）是一种用于求解非齐次[线性偏微分方程](@entry_id:172517)的强大工具，尤其是在处理带有边界条件的问题时。它将求解微分方程的复杂任务，转化为一个积分问题。本章将深入探讨[拉普拉斯算子](@entry_id:146319)（Laplacian）的格林函数的原理与机制，从其基本定义出发，到其构造方法、基本性质以及在求解边值问题中的具体应用。

### 作为[点源](@entry_id:196698)响应的[格林函数](@entry_id:147802)

从物理直觉出发，[格林函数](@entry_id:147802)的概念非常自然。想象一个无限大的均匀介质（例如一个金属块或一个导热平面），我们想知道在某一点 $\mathbf{x}_0$ 放置一个单位点热源或单位[点电荷](@entry_id:263616)后，在空间中任意一点 $\mathbf{x}$ 的温度或[电势](@entry_id:267554)[分布](@entry_id:182848)。这种由一个集中的“点源”引起的响应，正是[格林函数](@entry_id:147802)所描述的核心。

数学上，一个位于 $\mathbf{x}_0$ 的单位[点源](@entry_id:196698)可以用狄拉克-[德尔塔函数](@entry_id:273429) $\delta(\mathbf{x} - \mathbf{x}_0)$ 来表示。因此，描述该响应的函数 $G(\mathbf{x}, \mathbf{x}_0)$ 满足的方程是[泊松方程](@entry_id:143763)（Poisson's equation）的一种特殊形式：
$$ \Delta G(\mathbf{x}, \mathbf{x}_0) = \delta(\mathbf{x} - \mathbf{x}_0) $$
其中 $\Delta$ 是拉普拉斯算子。在二维笛卡尔坐标系中，$\Delta = \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2}$。在没有边界的无限空间中，这个方程的解被称为**基本解（fundamental solution）**，记作 $\Phi(\mathbf{x}, \mathbf{x}_0)$ 或 $\Phi(\mathbf{x} - \mathbf{x}_0)$。

基本解在源点 $\mathbf{x}_0$ 处是奇异的。为了理解这种奇异性如何与[德尔塔函数](@entry_id:273429)联系起来，我们可以考察一个“正则化”的函数。例如，在二维空间中，考虑函数 [@problem_id:2108247]：
$$ G(\mathbf{x}, \epsilon) = -\frac{1}{4\pi} \ln(x^2 + y^2 + \epsilon^2) $$
这里 $\mathbf{x}=(x,y)$，而 $\epsilon$ 是一个很小的正常数，它防止了在原点 $\mathbf{x}=\mathbf{0}$ 处的对数函数发散。如果我们计算这个函数的拉普拉斯算子，我们会得到：
$$ \Delta G(\mathbf{x}, \epsilon) = -\frac{\epsilon^2}{\pi(x^2 + y^2 + \epsilon^2)^2} $$
当 $\mathbf{x} \neq \mathbf{0}$ 时，随着 $\epsilon \to 0$，$\Delta G \to 0$。然而，在原点 $\mathbf{x} = \mathbf{0}$ 处，我们有：
$$ \Delta G(\mathbf{0}, \epsilon) = -\frac{1}{\pi\epsilon^2} $$
这个值随着 $\epsilon \to 0$ 而趋向负无穷。更重要的是，可以证明该函数在整个平面上的积分 $\int_{\mathbb{R}^2} \Delta G(\mathbf{x}, \epsilon) \,d\mathbf{x}$ 对于任意 $\epsilon > 0$ 都是一个常数（具体来说是-1，如果我们的方程是 $\Delta G = -\delta$）。这表明，当 $\epsilon \to 0$ 时，函数 $\Delta G(\mathbf{x}, \epsilon)$ 的行为就像一个在原点处[无限集](@entry_id:137163)中的脉冲，这正是[德尔塔函数](@entry_id:273429)的特征。

通过这个过程，我们确认了在不同维度下，[拉普拉斯算子](@entry_id:146319)的[基本解](@entry_id:184782)（在数学中通常定义 $\Delta \Phi = \delta$）为：
- 在二维空间 ($n=2$): $\Phi(\mathbf{x}, \mathbf{x}_0) = \frac{1}{2\pi} \ln|\mathbf{x} - \mathbf{x}_0|$
- 在三维空间 ($n=3$): $\Phi(\mathbf{x}, \mathbf{x}_0) = -\frac{1}{4\pi |\mathbf{x} - \mathbf{x}_0|}$

注意：物理学中，特别是在[静电学](@entry_id:140489)里，[电势](@entry_id:267554) $\phi$ 满足 $\Delta \phi = -\rho/\epsilon_0$。因此，物理背景下的[格林函数](@entry_id:147802)定义常带一个负号，例如三维空间中的 $G \propto 1/|\mathbf{x} - \mathbf{x}_0|$，代表正[电荷](@entry_id:275494)产生正[电势](@entry_id:267554)。在数学中，$\Delta G = \delta$ 的定义更为普遍，这导致二维和三维的基本解在源点附近分别趋向 $-\infty$。

### 边界的角色：狄利克雷[格林函数](@entry_id:147802)

[基本解](@entry_id:184782)描述了在无限空间中的响应，但大多数实际问题都涉及到一个有界或半有界的区域 $\Omega$，并在其边界 $\partial\Omega$ 上有特定的边界条件。例如，**[狄利克雷问题](@entry_id:274408)（Dirichlet problem）**要求解在边界上的值是固定的（例如，接地导体壳内部的[电势](@entry_id:267554)，其边界[电势](@entry_id:267554)为零）。

对于一个区域 $\Omega$ 上的[狄利克雷问题](@entry_id:274408)，其对应的[格林函数](@entry_id:147802) $G(\mathbf{x}, \mathbf{x}_0)$ 不仅要满足在区域内部的方程，还必须满足齐次狄利克雷边界条件：
1.  **[偏微分方程](@entry_id:141332)**: $\Delta G(\mathbf{x}, \mathbf{x}_0) = \delta(\mathbf{x} - \mathbf{x}_0)$, 对于 $\mathbf{x}, \mathbf{x}_0 \in \Omega$
2.  **边界条件**: $G(\mathbf{x}, \mathbf{x}_0) = 0$, 对于 $\mathbf{x} \in \partial\Omega$

为了满足这个边界条件，[格林函数](@entry_id:147802)可以被唯一地分解为两部分 [@problem_id:2108262]：
$$ G(\mathbf{x}, \mathbf{x}_0) = \Phi(\mathbf{x} - \mathbf{x}_0) + h(\mathbf{x}, \mathbf{x}_0) $$
这里：
- $\Phi(\mathbf{x} - \mathbf{x}_0)$ 是我们之前讨论过的基本解，它包含了在 $\mathbf{x} = \mathbf{x}_0$ 处的正确奇异性。
- $h(\mathbf{x}, \mathbf{x}_0)$ 是一个在整个区域 $\Omega$ 内都**正则（regular）**的**[调和函数](@entry_id:746864)（harmonic function）**，也就是说，它在 $\Omega$ 内处处光滑且满足[拉普拉斯方程](@entry_id:143689) $\Delta h(\mathbf{x}, \mathbf{x}_0) = 0$。

函数 $h$ 的作用是“修正”基本解 $\Phi$，使其在边界上的总和为零。因此，$h$ 必须满足以下的[边值问题](@entry_id:193901)：
$$ \Delta h(\mathbf{x}, \mathbf{x}_0) = 0, \quad \text{对于 } \mathbf{x} \in \Omega $$
$$ h(\mathbf{x}, \mathbf{x}_0) = -\Phi(\mathbf{x} - \mathbf{x}_0), \quad \text{对于 } \mathbf{x} \in \partial\Omega $$

### 构造方法：镜像法

如何找到这个修正函数 $h$ 呢？对于具有简单对称性的几何区域，**[镜像法](@entry_id:163138)（method of images）**是一种非常直观且强大的构造方法。这个方法的思想源于静电学 [@problem_id:2108283]。

想象一个点电荷在一个接地的无限大导体平面附近。导体平面必须是一个[等势面](@entry_id:158674)（[电势](@entry_id:267554)为零）。为了计算空间中的[电势](@entry_id:267554)[分布](@entry_id:182848)，我们可以在导体平面的另一侧，对称的位置放置一个等量异号的“[镜像电荷](@entry_id:266998)”。这个镜像电荷是虚构的，但它与原[电荷](@entry_id:275494)共同产生的[电场](@entry_id:194326)，恰好能使导体平面的位置成为一个零势面。在原[电荷](@entry_id:275494)所在的区域，这个由“真实[电荷](@entry_id:275494) + [镜像电荷](@entry_id:266998)”叠加产生的[电势](@entry_id:267554)场，就是该问题的唯一解。

这个思想可以直接翻译成构造格林函数的语言。修正函数 $h$ 就是由位于区域 $\Omega$ 外部的“镜像源”所产生的场。

让我们以二维上半平面 $\Omega = \{(x,y) \in \mathbb{R}^2 \mid y > 0\}$ 的[狄利克雷问题](@entry_id:274408)为例。源点为 $\mathbf{x}_0 = (x_0, y_0)$，其中 $y_0 > 0$。边界是 $x$ 轴（$y=0$）。为了让[格林函数](@entry_id:147802)在 $y=0$ 时为零，我们在区域外部的对称点 $\mathbf{x}_0^* = (x_0, -y_0)$ 放置一个“负镜像源”。

因此，格林函数由两部分构成：
1.  源于 $\mathbf{x}_0$ 的[基本解](@entry_id:184782): $\Phi(\mathbf{x} - \mathbf{x}_0) = \frac{1}{2\pi}\ln|\mathbf{x} - \mathbf{x}_0| = \frac{1}{4\pi}\ln((x-x_0)^2 + (y-y_0)^2)$。
2.  源于 $\mathbf{x}_0^*$ 的“镜像”[基本解](@entry_id:184782)，并带一个负号：$-\Phi(\mathbf{x} - \mathbf{x}_0^*) = -\frac{1}{4\pi}\ln((x-x_0)^2 + (y - (-y_0))^2)$。

将两者相加，得到[上半平面](@entry_id:199119)的格林函数：
$$ G(\mathbf{x}, \mathbf{x}_0) = \frac{1}{4\pi} \left[ \ln\left((x-x_0)^2 + (y-y_0)^2\right) - \ln\left((x-x_0)^2 + (y+y_0)^2\right) \right] $$
在这个表达式中，第一项是[基本解](@entry_id:184782) $\Phi(\mathbf{x}-\mathbf{x}_0)$，而第二项就是正则调和部分 $h(\mathbf{x}, \mathbf{x}_0)$ [@problem_id:2108262]：
$$ h(\mathbf{x}, \mathbf{x}_0) = -\frac{1}{4\pi}\ln\left((x-x_0)^2 + (y+y_0)^2\right) $$
由于镜像点 $\mathbf{x}_0^*$ 位于区域 $\Omega$ 之外，所以 $h$ 在 $\Omega$ 内部是光滑的[调和函数](@entry_id:746864)。我们可以计算 $h$ 在源点 $\mathbf{x}_0$ 处的值，这代表了边界对源点自身的影响 [@problem_id:2108267]：
$$ h(\mathbf{x}_0, \mathbf{x}_0) = -\frac{1}{4\pi}\ln\left((x_0-x_0)^2 + (y_0+y_0)^2\right) = -\frac{1}{4\pi}\ln(4y_0^2) = -\frac{1}{2\pi}\ln(2y_0) $$
这个值只依赖于源点到边界的距离 $y_0$。

镜像法之所以有效，是因为它利用了几何的对称性。它对于平面、球面或楔形等边界是成功的。然而，对于更复杂的几何形状，如立方体，简单镜像法会失效 [@problem_id:2108273]。对立方体的一个面做镜像，会在该面上满足边界条件，但同时会破坏其他五个面上的边界条件。为了修正，需要对新的镜像再做镜像，这个过程会无限延续下去，形成一个复杂的镜像[晶格](@entry_id:196752)。对于一般源点位置，这个无限级数的和并不能保证在所有六个面上都精确地为零。

### 格林函数的基本性质

狄利克雷[格林函数](@entry_id:147802)具有一些深刻且普适的性质。

#### 对称性（互易性）

[格林函数](@entry_id:147802)最重要的性质之一是**对称性（symmetry）**或**互易性（reciprocity）**：
$$ G(\mathbf{x}, \mathbf{x}_0) = G(\mathbf{x}_0, \mathbf{x}) $$
这个性质可以用[格林第二恒等式](@entry_id:169499)来证明。它的物理意义非常深远。考虑一个[静电学](@entry_id:140489)情景 [@problem_id:2108282]：在一个接地的导体壳内，[电势](@entry_id:267554) $\phi$ 与点电荷 $q_s$ 的关系是 $\phi(\mathbf{r}) = C \cdot q_s G(\mathbf{r}, \mathbf{r}_s)$，$C$ 为常数。
- 实验一：在点 $\mathbf{r}_1$ 放置[电荷](@entry_id:275494) $q_1$，在点 $\mathbf{r}_2$ 测得的[电势](@entry_id:267554)为 $V_M = C q_1 G(\mathbf{r}_2, \mathbf{r}_1)$。
- 实验二：在点 $\mathbf{r}_2$ 放置[电荷](@entry_id:275494) $q_2$，在点 $\mathbf{r}_1$ 测得的[电势](@entry_id:267554)为 $V' = C q_2 G(\mathbf{r}_1, \mathbf{r}_2)$。

根据对称性 $G(\mathbf{r}_2, \mathbf{r}_1) = G(\mathbf{r}_1, \mathbf{r}_2)$，我们可以立即得到两个实验测量值之间的关系：
$$ \frac{V_M}{q_1} = \frac{V'}{q_2} \implies V' = \frac{q_2}{q_1}V_M $$
换言之，在 $\mathbf{r}_1$ 处的源对 $\mathbf{r}_2$ 处产生的影响，与将源和观测点互换后的影响是相同的。这体现了物理定律的互易性。

#### 符号性质

对于有界区域 $\Omega$ 上的狄利克雷格林函数，它具有明确的符号性质：
$$ G(\mathbf{x}, \mathbf{x}_0)  0 \quad \text{对于所有 } \mathbf{x} \in \Omega, \mathbf{x} \neq \mathbf{x}_0 $$
这个性质的严格证明依赖于[调和函数](@entry_id:746864)的**[极值原理](@entry_id:138611)（Maximum Principle）** [@problem_id:2108290]。对于固定的源点 $\mathbf{x}_0$，函数 $u(\mathbf{x}) = G(\mathbf{x}, \mathbf{x}_0)$ 在区域 $\Omega \setminus \{\mathbf{x}_0\}$ 内是调和的。在边界 $\partial\Omega$ 上，$u(\mathbf{x})=0$。在源点 $\mathbf{x}_0$ 附近，基本解部分 $\Phi$ 趋向于 $-\infty$，因此 $u(\mathbf{x})$ 在 $\mathbf{x}_0$ 附近是负的。根据调和函数的[弱极值原理](@entry_id:191971)，函数 $u(\mathbf{x})$ 在区域内的最大值不会超过其边界上的最大值。由于在“内边界”（包围 $\mathbf{x}_0$ 的小球面）上函数值为负，在外边界 $\partial\Omega$ 上函数值为零，因此函数在整个区域内 $u(\mathbf{x}) \le 0$。再根据强[极值原理](@entry_id:138611)，如果函数在区域内任何一点达到最大值（这里是0），它必须是[常数函数](@entry_id:152060)。但 $G$ 显然不是常数零，所以它在区域内部必须严格小于零。

物理上，这可以理解为：在一个接地的空腔内放置一个正[电荷](@entry_id:275494)（源），腔壁上会感应出负[电荷](@entry_id:275494)，导致[空腔](@entry_id:197569)内各处的[电势](@entry_id:267554)都低于边界上的[电势](@entry_id:267554)（零[电势](@entry_id:267554)）。

### 应用：求解[边值问题](@entry_id:193901)

[格林函数](@entry_id:147802)的最终目的是求解[边值问题](@entry_id:193901)。根据[格林第二恒等式](@entry_id:169499)，拉普拉斯方程的[狄利克雷问题](@entry_id:274408)：
$$ \Delta u = 0 \quad \text{在 } \Omega \text{ 内}, \qquad u = g(\mathbf{x}) \quad \text{在 } \partial\Omega \text{ 上} $$
其解可以通过一个边界积分给出：
$$ u(\mathbf{x}) = \int_{\partial\Omega} g(\mathbf{x}_0) \frac{\partial G(\mathbf{x}, \mathbf{x}_0)}{\partial n_0} dS_0 $$
这里 $\frac{\partial}{\partial n_0}$ 是沿边界外法线方向的方向导数，作用在变量 $\mathbf{x}_0$ 上。这个公式将求解PDE转化为了计算一个积分，前提是我们已经知道了格林函数 $G$。

让我们再次回到二维[上半平面](@entry_id:199119)的例子 [@problem_id:2108270]。边界是 $x$ 轴，边界条件为 $u(x_0, 0) = g(x_0)$。我们将积分变量记为 $\mathbf{x}_0 = (x_0, y_0)$。边界是 $y_0 = 0$，外[法线](@entry_id:167651)向量是 $\mathbf{n}_0 = (0, -1)$，所以[法向导数](@entry_id:169511)是 $\frac{\partial}{\partial n_0} = -\frac{\partial}{\partial y_0}$。解的公式变为：
$$ u(x,y) = \int_{-\infty}^{\infty} g(x_0) \left[ -\frac{\partial G((x,y), (x_0,y_0))}{\partial y_0} \right]_{y_0=0} dx_0 $$
我们需要计算核函数 $K(x,y,x_0) = \left[ -\frac{\partial G}{\partial y_0} \right]_{y_0=0}$。我们有：
$$ G(\mathbf{x}, \mathbf{x}_0) = \frac{1}{4\pi} \left[ \ln\left((x-x_0)^2 + (y-y_0)^2\right) - \ln\left((x-x_0)^2 + (y+y_0)^2\right) \right] $$
对 $y_0$ 求偏导数：
$$ \frac{\partial G}{\partial y_0} = \frac{1}{4\pi} \left[ \frac{-2(y-y_0)}{(x-x_0)^2 + (y-y_0)^2} - \frac{2(y+y_0)}{(x-x_0)^2 + (y+y_0)^2} \right] $$
在边界 $y_0=0$ 处求值：
$$ \left. \frac{\partial G}{\partial y_0} \right|_{y_0=0} = \frac{1}{4\pi} \left[ \frac{-2y}{(x-x_0)^2 + y^2} - \frac{2y}{(x-x_0)^2 + y^2} \right] = -\frac{y}{\pi((x-x_0)^2 + y^2)} $$
因此，[核函数](@entry_id:145324)为：
$$ K(x,y,x_0) = -\left( -\frac{y}{\pi((x-x_0)^2 + y^2)} \right) = \frac{y}{\pi((x-x_0)^2 + y^2)} $$
这就是著名的**泊松核（Poisson kernel）**。最终，上半平面拉普拉斯方程的解就是（将积分变量 $x_0$ 写为 $x'$ 以免混淆）：
$$ u(x,y) = \frac{y}{\pi} \int_{-\infty}^{\infty} \frac{g(x')}{(x-x')^2 + y^2} dx' $$
这便是泊松积分公式，它完全由边界值 $g$ 决定了内部任意一点的解。

### 扩展：诺依曼问题

除了[狄利克雷问题](@entry_id:274408)，另一类重要的[边值问题](@entry_id:193901)是**诺依曼问题（Neumann problem）**，其中边界上给定的是解的[法向导数](@entry_id:169511)，例如 $\frac{\partial u}{\partial n} = g(\mathbf{x})$。

与[狄利克雷问题](@entry_id:274408)不同，诺依曼问题不总是存在解。对方程 $\Delta u = f$ 在区域 $\Omega$ [内积](@entry_id:158127)分，并使用散度定理，可得：
$$ \int_{\Omega} f(\mathbf{x}) dV = \int_{\Omega} \Delta u \, dV = \int_{\partial\Omega} \frac{\partial u}{\partial n} dS = \int_{\partial\Omega} g(\mathbf{x}) dS $$
这个**可解性条件（solvability condition）**表明，源的总和必须等于边界上的总通量。如果这个条件不满足，问题就无解。例如，在一个封闭的绝缘容器中，如果内部持续产[生热](@entry_id:167810)量（$\int f > 0$），而边界上没有热量流出（$\int g = 0$），系统温度显然无法达到[稳态](@entry_id:182458) [@problem_id:2108275]。

这个可解性条件也影响了诺依曼[格林函数](@entry_id:147802)的定义。如果我们天真地定义 $\Delta G_N = \delta(\mathbf{x} - \mathbf{x}_0)$ 并要求 $\frac{\partial G_N}{\partial n} = 0$，那么应用可解性条件会得到 $1=0$ 的矛盾。
为了解决这个问题，诺依曼[格林函数](@entry_id:147802) $G_N$ 的定义需要修正。一种常见的做法是 [@problem_id:2108229]：
1.  **[偏微分方程](@entry_id:141332)**: $\Delta G_N(\mathbf{x}, \mathbf{x}_0) = \delta(\mathbf{x} - \mathbf{x}_0) - \frac{1}{|\Omega|}$, 对于 $\mathbf{x} \in \Omega$
2.  **边界条件**: $\frac{\partial G_N}{\partial n}(\mathbf{x}, \mathbf{x}_0) = 0$, 对于 $\mathbf{x} \in \partial\Omega$
这里 $|\Omega|$ 是区域的体积或面积。另一种常见的定义是：
1.  **[偏微分方程](@entry_id:141332)**: $\Delta G_N(\mathbf{x}, \mathbf{x}_0) = \delta(\mathbf{x} - \mathbf{x}_0)$, 对于 $\mathbf{x} \in \Omega$
2.  **边界条件**: $\frac{\partial G_N}{\partial n}(\mathbf{x}, \mathbf{x}_0) = C$, 对于 $\mathbf{x} \in \partial\Omega$

其中 $C$ 是一个常数。将可解性条件应用于 $G_N$ 本身，我们得到：
$$ \int_{\Omega} \delta(\mathbf{x} - \mathbf{x}_0) dV = 1 = \int_{\partial\Omega} \frac{\partial G_N}{\partial n} dS = \int_{\partial\Omega} C \, dS = C \cdot |\partial\Omega| $$
其中 $|\partial\Omega|$ 是边界的面积（或长度）。因此，常数必须取值为 $C = \frac{1}{|\partial\Omega|}$。例如，在二维[单位圆盘](@entry_id:172324)上，边界[周长](@entry_id:263239)为 $2\pi$，因此诺依曼格林函数的边界条件应为 $\frac{\partial G_N}{\partial n} = \frac{1}{2\pi}$。此外，由于[常数函数](@entry_id:152060)是诺依曼问题的齐次解，诺依曼[格林函数](@entry_id:147802)只在相差一个任意常数的意义下是唯一的。