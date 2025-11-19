## 引言
在[几何分析](@entry_id:157700)领域，一个核心的挑战在于理解空间的局部几何特征（如曲率）如何决定其[全局分析](@entry_id:188294)与[拓扑性质](@entry_id:141605)。Bochner 恒等式及其推广的 Weitzenböck 公式，正是应对这一挑战的最强大、最优雅的工具之一。它们如同一座桥梁，精确地将[流形](@entry_id:153038)上微观的“弯曲”与宏观的结构以及其上函数的行为联系起来，构成了现代[黎曼几何](@entry_id:160508)的基石。然而，对于初学者而言，这些公式的推导和应用往往显得抽象，难以把握其统一的内在逻辑和应用的广泛性。

本文旨在系统地揭开 Bochner 技巧的神秘面纱，为读者提供一个从原理到应用的清晰路径。我们将首先在“**原理与机制**”中，从[黎曼流形](@entry_id:261160)上的基本概念出发，循序渐进地推导出这些关键恒等式，并深入剖析其各项的几何意义。接着，在“**应用与跨学科联系**”中，我们将探索这一技巧的巨大威力，展示它如何被用于证明深刻的拓扑定理、建立[偏微分方程解](@entry_id:166250)的估计，并与其他数学及物理分支产生联系。最后，一系列“**动手实践**”将引导读者亲手计算和应用这些公式，从而将理论知识内化为解决问题的能力。

通过本文的学习，读者将不仅掌握 Bochner-Weitzenböck 公式的推导，更能深刻理解其作为连接几何与分析的核心思想，并领略其在现代数学研究中的强大生命力。

## 原理与机制

在[几何分析](@entry_id:157700)中，将局部几何性质（如曲率）与[流形](@entry_id:153038)上的函数和张量场的[全局分析](@entry_id:188294)性质联系起来是一项核心任务。Bochner-Weitzenböck 公式是实现这一目标的最强大工具之一。这些恒等式将[拉普拉斯算子](@entry_id:146319)分解为若干项，揭示了[流形](@entry_id:153038)的曲率如何与函数或张量的[二阶导数](@entry_id:144508)相互作用。本章将系统地阐述这些公式背后的基本原理和推导机制。

### [流形](@entry_id:153038)上的基本[微分算子](@entry_id:140145)

在深入探讨 Bochner-Weitzenböck 公式之前，我们必须首先精确定义其构成要素：梯度、散度和[拉普拉斯-贝尔特拉米算子](@entry_id:267002)。

#### 梯度向量场

给定一个黎曼流形 $(M, g)$ 和一个[光滑函数](@entry_id:267124) $u \in C^{\infty}(M)$，其[微分](@entry_id:158718) $du$ 是一个余向量场（或称 1-形式）。在每一点 $p \in M$，$du_p$ 是切空间 $T_pM$ 上的一个线性泛函。黎曼度量 $g_p$ 在 $T_pM$ 上定义了一个[内积](@entry_id:158127)，使得 $T_pM$ 成为一个有限维[内积空间](@entry_id:271570)。

根据有限维[内积空间](@entry_id:271570)上的 **Riesz [表示定理](@entry_id:637872)**，对于任何线性泛函 $L$，都存在一个唯一的向量 $v$，使得对于所有向量 $X$，都有 $L(X) = \langle v, X \rangle$。将此定理应用于我们的场景，其中线性泛函是 $du_p$，[内积](@entry_id:158127)是 $g_p$，我们便可以定义函数 $u$ 的**梯度**（gradient）。

**定义：** 函数 $u$ 的梯度，记作 $\nabla u$，是在每一点 $p \in M$ 唯一确定的切向量场，它满足对于所有向量场 $X$，都有：
$$ g(\nabla u, X) = du(X) = X(u) $$
梯度的存在性和唯一性在每一点都由 Riesz [表示定理](@entry_id:637872)保证。由于 $u$ 和度量 $g$ 都是光滑的，由此产生的向量场 $\nabla u$ 也是光滑的。[@problem_id:3066407]

在局部坐标系 $(x^1, \dots, x^n)$ 中，度量[张量表示](@entry_id:180492)为 $g_{ij}$，其逆矩阵为 $g^{ij}$。函数 $u$ 的[微分](@entry_id:158718)是 $du = \frac{\partial u}{\partial x^j} dx^j$。设 $\nabla u = (\nabla u)^i \frac{\partial}{\partial x^i}$。根据定义，我们有：
$$ g(\nabla u, \frac{\partial}{\partial x^j}) = g((\nabla u)^i \frac{\partial}{\partial x^i}, \frac{\partial}{\partial x^j}) = (\nabla u)^i g_{ij} $$
同时，
$$ du(\frac{\partial}{\partial x^j}) = \frac{\partial u}{\partial x^j} $$
因此，$(\nabla u)^i g_{ij} = \frac{\partial u}{\partial x^j}$。两边与 $g^{jk}$ 缩并，我们得到梯度的坐标表达式：
$$ (\nabla u)^k = g^{jk} \frac{\partial u}{\partial x^j} $$
这个表达式明确显示，梯度 $\nabla u$ 深刻地依赖于黎曼度量 $g$。如果度量发生改变，梯度场通常也会改变。一个重要的例子是**共形变换**（conformal change）。若新度量 $\tilde{g}$ 与原度量 $g$ 的关系为 $\tilde{g} = e^{2\phi} g$，其中 $\phi$ 是一个光滑函数，那么相应的逆度量为 $\tilde{g}^{ij} = e^{-2\phi} g^{ij}$。根据梯度的定义，新梯度 $\nabla^{\tilde{g}} u$ 满足 $\tilde{g}(\nabla^{\tilde{g}} u, X) = du(X)$。将其与原定义 $g(\nabla^g u, X) = du(X)$ 比较，可得：
$$ e^{2\phi} g(\nabla^{\tilde{g}} u, X) = g(\nabla^g u, X) $$
由于这对所有 $X$ 都成立且 $g$ 是非退化的，我们必然得到：
$$ \nabla^{\tilde{g}} u = e^{-2\phi} \nabla^g u $$
这再次说明，梯度并非一个独立于度量的几何量。[@problem_id:3066407]

#### 散度与[拉普拉斯-贝尔特拉米算子](@entry_id:267002)

**散度**（divergence）衡量了一个向量场引起的[体积元](@entry_id:267802)的变化率。在一个定向的黎曼流形上，给定向量场 $X$，其散度 $\operatorname{div} X$ 由下式几何地定义：
$$ L_X d\mathrm{vol}_g = (\operatorname{div} X) d\mathrm{vol}_g $$
其中 $L_X$ 是沿 $X$ 的[李导数](@entry_id:171745)，$d\mathrm{vol}_g$ 是[黎曼体积形式](@entry_id:275973)。这一定义等价于向量场[协变导数](@entry_id:152476)的迹，在[局部坐标](@entry_id:181200)中表示为：
$$ \operatorname{div} X = \operatorname{tr}_g(\nabla X) = \nabla_i X^i $$
[散度算子](@entry_id:265975)的一个关键性质通过[分部积分](@entry_id:136350)（或[散度定理](@entry_id:143110)）体现出来。对于[紧支集](@entry_id:276214)函数 $u$ 或在无边[紧流形](@entry_id:158804)上，我们有：
$$ \int_M u (\operatorname{div} X) \, d\mathrm{vol}_g = - \int_M g(\nabla u, X) \, d\mathrm{vol}_g $$
这表明[散度算子](@entry_id:265975) $\operatorname{div}$ 是[梯度算子](@entry_id:275922) $\nabla$ 的负伴随算子。[@problem_id:3066452]

有了梯度和散度的概念，我们就可以定义**[拉普拉斯-贝尔特拉米算子](@entry_id:267002)**（Laplace-Beltrami operator），通常简称为[拉普拉斯算子](@entry_id:146319)。

**定义：** 作用于函数 $u$ 的[拉普拉斯-贝尔特拉米算子](@entry_id:267002) $\Delta u$ 定义为 $u$ 的[梯度的散度](@entry_id:270716)：
$$ \Delta u = \operatorname{div}(\nabla u) $$
结合梯度的坐标表达式和散度的定义，可以推导出 $\Delta u = \operatorname{tr}_g(\nabla^2 u)$，其中 $\nabla^2 u$ 是 $u$ 的[协变黑塞矩阵](@entry_id:637103)（Hessian）。拉普拉斯算子在[局部坐标](@entry_id:181200)下的完整表达式为：
$$ \Delta u = \frac{1}{\sqrt{\det(g)}} \frac{\partial}{\partial x^i} \left( \sqrt{\det(g)} \, g^{ij} \frac{\partial u}{\partial x^j} \right) $$
这个算子是[欧氏空间](@entry_id:138052)中标准拉普拉斯算子 $\sum_i \frac{\partial^2}{\partial (x^i)^2}$ 在黎曼流形上的自然推广。

根据上述定义和[分部积分公式](@entry_id:145262)，我们可以确定 $\Delta$ 的符号约定。令 $X = \nabla v$：
$$ \int_M u \, \Delta v \, d\mathrm{vol}_g = \int_M u \, \operatorname{div}(\nabla v) \, d\mathrm{vol}_g = - \int_M g(\nabla u, \nabla v) \, d\mathrm{vol}_g $$
特别地，当 $u=v$ 时，我们得到：
$$ \int_M u \, \Delta u \, d\mathrm{vol}_g = - \int_M |\nabla u|^2_g \, d\mathrm{vol}_g \le 0 $$
这表明，在[几何分析](@entry_id:157700)的标准约定（“几何学家的[拉普拉斯算子](@entry_id:146319)”）中，$\Delta$ 是一个非[正算子](@entry_id:263696)，其[特征值](@entry_id:154894)均为非正数。与之相对，“分析学家的[拉普拉斯算子](@entry_id:146319)”通常定义为 $-\Delta$，它是一个非负算子。在本书中，我们将遵循几何学家的约定。[@problem_id:3066452]

### 曲率：协变导数交换的障碍

Bochner-Weitzenböck 公式中的曲率项源于一个深刻的几何事实：在弯曲空间中，[二阶协变导数](@entry_id:193368)的求导次序不可交换。这种不[可交换性](@entry_id:263314)由黎曼曲率张量精确地量化。

给定一个黎曼流形 $(M,g)$ 及其 Levi-Civita 联络 $\nabla$，**[黎曼曲率张量](@entry_id:160189)**（Riemann curvature tensor）$R$ 定义为：
$$ R(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]}Z $$
其中 $X, Y, Z$ 是任意向量场，$[X,Y] = XY - YX$ 是[李括号](@entry_id:636461)。在[局部坐标系](@entry_id:751394)中，[基向量](@entry_id:199546)场 $\frac{\partial}{\partial x^i}$ 的李括号为零，因此上式简化为 $R(\partial_i, \partial_j)\partial_k = \nabla_i \nabla_j \partial_k - \nabla_j \nabla_i \partial_k$。

为了理解曲率如何在 Bochner-Weitzenböck 公式中出现，我们必须计算协变导数交换子 $[\nabla_i, \nabla_j] = \nabla_i \nabla_j - \nabla_j \nabla_i$ 作用在[张量场](@entry_id:190170)上的结果。让我们以一个 1-形式 $\omega$ 为例进行推导。

[1-形式](@entry_id:270392) $\omega$ 的协变导数定义为 $(\nabla_i \omega)_k = \partial_i \omega_k - \Gamma^\ell_{ik} \omega_\ell$，其中 $\Gamma^\ell_{ik}$ 是 Christoffel 符号。我们计算[二阶协变导数](@entry_id:193368) $\nabla_i(\nabla_j \omega)$。注意 $\nabla_j \omega$ 是一个 (0,2)-型张量，其[协变导数](@entry_id:152476)遵循相应的法则：
$$ (\nabla_i \nabla_j \omega)_k = \partial_i (\nabla_j \omega)_k - \Gamma^\ell_{ij} (\nabla_\ell \omega)_k - \Gamma^\ell_{ik} (\nabla_j \omega)_\ell $$
将 $(\nabla_j \omega)_k$ 的表达式代入并展开，会得到包含 $\omega$ 的[偏导数](@entry_id:146280)、Christoffel 符号以及 Christoffel 符号偏导数的复杂表达式。接着，我们计算 $(\nabla_j \nabla_i \omega)_k$，即交换上式中的 $i$ 和 $j$。

最后，计算二者之差 $([\nabla_i, \nabla_j]\omega)_k$。经过一番细致的计算，利用[偏导数的对称性](@entry_id:194790)（$\partial_i \partial_j = \partial_j \partial_i$）和 Levi-Civita 联络的无挠性（$\Gamma^k_{ij} = \Gamma^k_{ji}$），所有包含 $\omega$ 导数的项都会奇迹般地抵消。剩下的项只与 $\omega$ 本身有关，形成一个纯代数（零阶）算子。其结果为：
$$ ([\nabla_i, \nabla_j]\omega)_k = (\partial_i \Gamma^\ell_{jk} - \partial_j \Gamma^\ell_{ik} + \Gamma^p_{jk}\Gamma^\ell_{ip} - \Gamma^p_{ik}\Gamma^\ell_{jp}) \omega_\ell $$
方括号内的表达式正是[黎曼曲率张量](@entry_id:160189)分量 $R^\ell{}_{kji}$ 的定义（根据符号约定的不同，可能相差一个负号）。在一个常见的约定下，我们得到著名的**里奇恒等式**（Ricci identity）：
$$ (\nabla_i \nabla_j - \nabla_j \nabla_i)\omega_k = - R^\ell{}_{kij} \omega_\ell $$
这个恒等式是所有 Weitzenböck-Bochner 公式的基石。它表明，[协变导数的交换子](@entry_id:198075)本身就是一个由曲率张量定义的代数算子。[@problem_id:3066424]

### Weitzenböck-Bochner 公式

现在我们具备了构建核心恒等式的全部要素。这些恒等式通过统一的模式，将不同类型的[拉普拉斯算子](@entry_id:146319)（如作用于函数、向量场或微分形式的拉普拉斯算子）分解为“动能”项（粗糙拉普拉斯算子）和“势能”项（曲率项）。

#### 统一原理：分解拉普拉斯算子

在[黎曼流形](@entry_id:261160)上，我们可以定义多种拉普拉斯算子。除了作用于函数的[拉普拉斯-贝尔特拉米算子](@entry_id:267002) $\Delta$ 外，对于微分形式，还有**[霍奇-拉普拉斯算子](@entry_id:261049)**（Hodge Laplacian），定义为 $\Delta_H = d\delta + \delta d$，其中 $d$ 是外微分，$\delta$ 是其[伴随算子](@entry_id:140236)（[余微分](@entry_id:197182)）。对于一般的张量场 $s$，还有**粗糙拉普拉斯算子**（rough Laplacian）或称**[联络拉普拉斯算子](@entry_id:197120)**（connection Laplacian），定义为 $\nabla^*\nabla = -\operatorname{tr}_g(\nabla^2)$，它是协变导数 $\nabla$ 与其伴随算子 $\nabla^*$ 的复合。

Weitzenböck 公式揭示了这些算子之间的深刻联系。其统一思想是：
$$ \text{“自然的”拉普拉斯算子} = \text{粗糙拉普拉斯算子} + \text{曲率项} $$
这个原理精妙地将分析（导数项）与几何（代数曲率项）分离开来。[@problem_id:3066402]

#### [微分形式](@entry_id:146747)的 Weitzenböck 公式

让我们看看这个原理在[微分形式](@entry_id:146747)上的具体体现。
- **0-形式（函数）：** 对于一个函数 $f$，其[霍奇-拉普拉斯算子](@entry_id:261049)为 $\Delta_H f = \delta d f$。而粗糙拉普拉斯算子为 $\nabla^*\nabla f = \delta(\nabla f)$。由于作用在函数上，梯度 $\nabla f$ 通过度量对应于[外微分](@entry_id:161900) $df$，我们直接得到 $\Delta_H f = \nabla^*\nabla f$。这意味着，对于0-形式，Weitzenböck 公式中没有曲率项。[@problem_id:3066400] [@problem_id:3066402]

- **[1-形式](@entry_id:270392)：** 对于一个 [1-形式](@entry_id:270392) $\omega$，情况变得有趣起来。通过直接计算 $\Delta_H \omega = (\delta d + d\delta)\omega$ 的分量，并使用我们之[前推](@entry_id:158718)导的里奇恒等式来处理[协变导数的交换子](@entry_id:198075)，可以得到：
  $$ \Delta_H \omega = \nabla^*\nabla \omega + \operatorname{Ric}^\sharp(\omega) $$
  其中 $\operatorname{Ric}^\sharp$ 是由里奇张量 $\operatorname{Ric}$ 诱导的在 [1-形式](@entry_id:270392)空间上的[线性变换](@entry_id:149133)（endomorphism）。具体来说，$(\operatorname{Ric}^\sharp(\omega))_k = R_{k\ell} \omega^\ell$。这里的曲率项恰好是里奇曲率。[@problem_id:3066402] [@problem_id:3066400]

- **p-形式（$p>1$）：** 对于更高阶的 $p$-形式，Weitzenböck 公式仍然成立，但形式更复杂：
  $$ \Delta_H \omega = \nabla^*\nabla \omega + \mathcal{R}_p(\omega) $$
  这里的 $\mathcal{R}_p$ 是一个更复杂的[曲率算子](@entry_id:198006)，它由完整的[黎曼曲率张量](@entry_id:160189) $R$ 决定，而不仅仅是其迹——[里奇张量](@entry_id:159336)。这意味着，即使在[里奇平坦](@entry_id:159097)（$\operatorname{Ric}=0$）的[流形](@entry_id:153038)上，对于 $p>1$ 的形式，$\mathcal{R}_p$ 也未必为零。只有在[流形](@entry_id:153038)是真正平坦（$R=0$）时，我们才有 $\Delta_H = \nabla^*\nabla$ 对所有阶的微分形式成立。[@problem_id:3066414] [@problem_id:3066402]

#### 函数的 Bochner 恒等式

最著名也最常用的 Bochner 型公式是作用于函数梯度范数平方 $\frac{1}{2}|\nabla f|^2$ 的恒等式。这个量可以看作是函数 $f$ 的“能量密度”。其[拉普拉斯算子](@entry_id:146319) $\frac{1}{2}\Delta |\nabla f|^2$ 衡量了这种能量密度的[局部凸性](@entry_id:271002)。

通过对 $\frac{1}{2}|\nabla f|^2 = \frac{1}{2} g(\nabla f, \nabla f)$ 求两次协变导数并取迹，我们可以推导出 **Bochner 恒等式**（Bochner identity）。推导过程的关键一步在于处理包含 $f$ 的三阶协变导数的项，例如 $g^{ij} u_{;ikj} u^k$。为了重新整理求导次序，必须使用里奇恒等式，这正是[里奇曲率](@entry_id:162038)进入公式的根本原因。[@problem_id:3066426] [@problem_id:3066449]

最终得到的公式为：
$$ \frac{1}{2}\Delta |\nabla f|^2 = |\nabla^2 f|^2 + \langle \nabla(\Delta f), \nabla f \rangle + \operatorname{Ric}(\nabla f, \nabla f) $$
其中 $|\nabla^2 f|^2$ 是 $f$ 的黑塞[矩阵范数](@entry_id:139520)的平方，$\langle \cdot, \cdot \rangle$ 是度量诱导的[内积](@entry_id:158127)。

这个恒等式也可以被看作是 [1-形式](@entry_id:270392) Weitzenböck 公式的一个推论。事实上，存在一个更普适的 Bochner 恒等式，它对任意 p-形式 $\omega$ 都成立：
$$ \frac{1}{2}\Delta |\omega|^2 = |\nabla \omega|^2 - \langle \Delta_H \omega, \omega \rangle + \langle \mathcal{R}_p(\omega), \omega \rangle $$
当我们取 $p=1$ 并令 $\omega = df$ 时，这个普适公式就能完美地转化为上述函数的 Bochner 恒等式。具体对应关系为：$|\nabla(df)|^2 = |\nabla^2 f|^2$；曲率项 $\langle \mathcal{R}_1(df), df \rangle = \operatorname{Ric}(\nabla f, \nabla f)$；以及利用 $\Delta_H(df) = d\delta(df) = d(-\Delta f)$，我们得到 $-\langle \Delta_H(df), df \rangle = \langle d(\Delta f), df \rangle = \langle \nabla(\Delta f), \nabla f \rangle$。这种统一性展示了这些公式背后深刻的结构一致性。[@problem_id:3066457] [@problem_id:3066411]

### 几何解释与应用

Bochner-Weitzenböck 公式不仅仅是漂亮的代数恒等式，它们的真正威力在于其各项都有着清晰的几何解释，从而可以将几何条件转化为分析结果。

#### Bochner 恒等式各项的几何意义

让我们逐一剖析函数 Bochner 恒等式中的三项：[@problem_id:3066411] [@problem_id:3066449]

1.  **$|\nabla^2 f|^2$：** 这一项是 $f$ 的黑塞[矩阵范数](@entry_id:139520)的平方。黑塞矩阵 $\nabla^2 f$ 描述了 $f$ 的二阶变化。沿[测地线](@entry_id:269969) $\gamma(t)$，我们有 $(f \circ \gamma)''(t) = (\nabla^2 f)(\dot{\gamma}(t), \dot{\gamma}(t))$。因此，$|\nabla^2 f|^2$ 度量了函数 $f$ 在所有方向上偏离“线性”或“仿射”的程度。它是一个非负项，可以被看作是 $f$ 的**“[测地线](@entry_id:269969)凸性”**的量度。

2.  **$\langle \nabla(\Delta f), \nabla f \rangle$：** 这一项是 $\Delta f$ 沿着 $\nabla f$ 方向的[方向导数](@entry_id:189133)。它与扩散过程密切相关。考虑[热方程](@entry_id:144435) $\partial_t u = \Delta u$，它描述了热量在[流形](@entry_id:153038)上的[扩散](@entry_id:141445)。我们可以计算能量密度随时间的变化率：$\frac{\partial}{\partial t}(\frac{1}{2}|\nabla u|^2) = \langle \nabla(\partial_t u), \nabla u \rangle = \langle \nabla(\Delta u), \nabla u \rangle$。因此，这一项精确地描述了**扩散过程如何改变梯度的局部大小**。

3.  **$\operatorname{Ric}(\nabla f, \nabla f)$：** 这一项直接体现了背景几何（曲率）的影响。[里奇曲率](@entry_id:162038) $\operatorname{Ric}(X,X)$ 衡量了包含 $X$ 方向的平面[截面曲率](@entry_id:159738)的平均值。[正里奇曲率](@entry_id:199145)通常与[测地线](@entry_id:269969)的汇聚（focusing）相关联。在 Bochner 公式中，$\operatorname{Ric}(\nabla f, \nabla f)$ 反映了**[流形](@entry_id:153038)几何如何“弯曲”梯度流线**。[正里奇曲率](@entry_id:199145)倾向于使[梯度流](@entry_id:635964)线汇聚，从而对 $\Delta|\nabla f|^2$ 做出正贡献，抑制梯度范数形成[局部极大值](@entry_id:137813)。

#### 经典应用：从曲率到拓扑

Bochner-Weitzenböck 公式的威力在与积分和最大值原理结合时表现得淋漓尽致。一个经典例子是 Bochner 消失定理。

考虑一个紧致无边的[黎曼流形](@entry_id:261160) $(M,g)$。
- **对于函数：** 假设[流形](@entry_id:153038)具有[非负里奇曲率](@entry_id:633979)（$\operatorname{Ric} \ge 0$），并且 $f$ 是一个[调和函数](@entry_id:746864)（harmonic function），即 $\Delta f=0$。此时，Bochner 恒等式简化为：
  $$ \frac{1}{2}\Delta |\nabla f|^2 = |\nabla^2 f|^2 + \operatorname{Ric}(\nabla f, \nabla f) \ge 0 $$
  我们将上式在整个[流形](@entry_id:153038) $M$ 上积分。由于 $\int_M \Delta F \, d\mathrm{vol}_g = 0$ 对任何函数 $F$ 成立（散度定理），我们得到：
  $$ 0 = \int_M (|\nabla^2 f|^2 + \operatorname{Ric}(\nabla f, \nabla f)) \, d\mathrm{vol}_g $$
  由于两个积分项都是非负的，它们必须处处为零。因此，我们得出结论：$|\nabla^2 f|^2 \equiv 0$ 且 $\operatorname{Ric}(\nabla f, \nabla f) \equiv 0$。$|\nabla^2 f|^2 \equiv 0$ 意味着 $\nabla^2 f \equiv 0$。代回简化的 Bochner 恒等式，得到 $\Delta |\nabla f|^2 = 0$，这意味着 $|\nabla f|^2$ 是一个调和函数。在紧流形上，唯一的[调和函数](@entry_id:746864)是常数。所以，任何在 $\operatorname{Ric} \ge 0$ 的紧[流形上的[调和函](@entry_id:203259)数](@entry_id:746864)，其梯度范数的平方必为常数。[@problem_id:3066414]

- **对于 1-形式：** 同样，在 $\operatorname{Ric} \ge 0$ 的[紧流形](@entry_id:158804)上，考虑一个调和 1-形式 $\omega$（$\Delta_H \omega=0$）。Weitzenböck 公式为 $\Delta_H \omega = \nabla^*\nabla \omega + \operatorname{Ric}^\sharp(\omega)$。两边与 $\omega$ 做[内积](@entry_id:158127)并积分：
  $$ 0 = \int_M \langle \Delta_H \omega, \omega \rangle \, d\mathrm{vol}_g = \int_M (|\nabla \omega|^2 + \operatorname{Ric}(\omega^\sharp, \omega^\sharp)) \, d\mathrm{vol}_g $$
  同样，这迫使 $|\nabla \omega|^2 \equiv 0$，即 $\nabla \omega \equiv 0$。这意味着任何调和 [1-形式](@entry_id:270392)必须是**平行**（parallel）的。[@problem_id:3066414] [@problem_id:3066402]

如果[里奇曲率](@entry_id:162038)更强，为正定（$\operatorname{Ric} > 0$），那么 $\int_M \operatorname{Ric}(\omega^\sharp, \omega^\sharp) \, d\mathrm{vol}_g > 0$ 除非 $\omega \equiv 0$。这意味着在这种[流形](@entry_id:153038)上不存在非平凡的调和 [1-形式](@entry_id:270392)。根据[霍奇理论](@entry_id:161814)，[流形](@entry_id:153038)的第一个[贝蒂数](@entry_id:153109) $b_1(M)$ 等于调和 [1-形式](@entry_id:270392)空间的维数，因此我们得到了一个纯粹由局部几何（[正里奇曲率](@entry_id:199145)）推出的深刻拓扑结论：$b_1(M) = 0$。

这些例子仅仅是冰山一角，它们展示了 Bochner-Weitzenböck 公式作为连接几何与分析的桥梁所具有的非凡力量。