## 引言
在科学与工程领域，许多物理过程，如热量[扩散](@entry_id:141445)、流体流动和化学物质输运，都可以通过[多维偏微分方程](@entry_id:752273)（PDE）来描述。对这些方程进行精确高效的数值求解，是现代计算科学的核心挑战之一。诸如Crank-Nicolson这样的标准[隐式格式](@entry_id:166484)虽然具备理想的稳定性和二阶时间精度，但在应用于二维或更高维度问题时，会在每个时间步产生一个庞大且维度耦合的[线性方程组](@entry_id:148943)，其求解成本极高，严重制约了[计算效率](@entry_id:270255)。

为了解决[隐式格式](@entry_id:166484)在多维问题中的计算瓶颈，交替方向隐式（Alternating Direction Implicit, ADI）方法应运而生。[ADI方法](@entry_id:746385)的核心是一种被称为**[算子分裂](@entry_id:634210)**的巧妙策略，它将一个复杂的多维问题分解为一系列易于求解的一维问题。通过在各个空间方向上交替使用[隐式格式](@entry_id:166484)，[ADI方法](@entry_id:746385)既继承了[隐式格式](@entry_id:166484)优越的稳定性，又将计算量控制在求解高效的三对角线性方程组的水平。本文旨在深入剖析两种最经典且影响深远的ADI格式：Peaceman-Rachford（PR）格式和Douglas-Gunn（DG）格式。

在接下来的章节中，我们将系统地展开讨论。**第一章：原理与机制**将详细阐述PR和[DG格式](@entry_id:178043)的数学构造、精度分析和[稳定性理论](@entry_id:149957)，并揭示它们在处理不同类型问题（如[常系数](@entry_id:269842)与变系数）时的关键差异。**第二章：应用与跨学科联系**将展示这些方法如何被应用于解决[计算流体动力学](@entry_id:147500)、[热传导](@entry_id:147831)等领域的实际问题，并探讨其如何与其他数值技术（如[有限元法](@entry_id:749389)）融合以及如何构建更高阶的格式。最后，**第三章：动手实践**将提供具体的计算练习，帮助读者将理论知识转化为实际的编程与分析能力。通过本次学习，你将全面掌握[ADI方法](@entry_id:746385)的设计思想、理论基础和实践技巧。

## 原理与机制

在数值求解[多维偏微分方程](@entry_id:752273)时，一个核心的挑战是在精度、稳定性与计算效率之间取得平衡。对于[抛物型方程](@entry_id:144670)，例如[热传导方程](@entry_id:194763)，Crank-Nicolson (CN) 格式因其[无条件稳定性](@entry_id:145631)和时间上的二阶精度而备受青睐。然而，在二维或三维问题中，CN格式会导致在每个时间步都必须求解一个大型的、耦合所有空间维度的线性方程组。例如，对于二维问题 $u_t = u_{xx} + u_{yy}$，其CN格式为：

$$
\left(I - \frac{\Delta t}{2}(L_x + L_y)\right) u^{n+1} = \left(I + \frac{\Delta t}{2}(L_x + L_y)\right) u^n
$$

其中 $L_x$ 和 $L_y$ 分别是对应于 $u_{xx}$ 和 $u_{yy}$ 的离散算子。左侧的算子 $(I - \frac{\Delta t}{2}(L_x + L_y))$ 耦合了 $x$ 和 $y$ 方向上的未知数，形成的[系数矩阵](@entry_id:151473)不再是简单的三对角或带状结构，直接求解的计算成本非常高。

为了克服这一困难，**交替方向隐式 (Alternating Direction Implicit, ADI)** 方法应运而生。[ADI方法](@entry_id:746385)的核心思想是**[算子分裂](@entry_id:634210) (operator splitting)**，即将多维[问题分解](@entry_id:272624)为一系列一维问题来求解。通过在不同方向上交替使用[隐式格式](@entry_id:166484)，[ADI方法](@entry_id:746385)旨在保留[隐式格式](@entry_id:166484)的优良稳定性，同时将每个子步骤的计算量限制在一维问题的水平，这通常意味着仅仅需要求解高效的三对角[线性方程组](@entry_id:148943)。本章将深入探讨两种最经典和最有影响力的ADI格式：Peaceman-Rachford (PR) 格式和 Douglas-Gunn (DG) 格式。

### Peaceman-Rachford (PR) ADI 格式

PR格式是对[Crank-Nicolson格式](@entry_id:147733)的一种巧妙的[因子分解](@entry_id:150389)近似。其思想是将CN格式中的算子 $(I \mp \frac{\Delta t}{2}(L_x+L_y))$ 近似为因子化的形式 $(I \mp \frac{\Delta t}{2}L_x)(I \mp \frac{\Delta t}{2}L_y)$。

#### 格式的构建

考虑[二维热方程](@entry_id:746155) $u_t = \kappa(u_{xx} + u_{yy})$，其半离散形式为 $u_t = (L_x + L_y)u$。PR格式将从时间层 $n$到 $n+1$ 的推进过程分解为两个子步骤。令 $\theta = \Delta t / 2$，该格式的[标准形式](@entry_id:153058)是引入一个中间时间步 $n+1/2$ [@problem_id:3429902]：

**第一步（x方向隐式）：**
$$
\left(I - \theta L_x\right) u^{n+1/2} = \left(I + \theta L_y\right) u^n
$$

**第二步（y方向隐式）：**
$$
\left(I - \theta L_y\right) u^{n+1} = \left(I + \theta L_x\right) u^{n+1/2}
$$

在第一步中，我们在 $x$ 方向上是隐式的，而在 $y$ 方向上是显式的。这意味着对于网格中的每一条 $y$ 方向的网格线，我们需要求解一个关于 $x$ 方向未知数的三对角线性方程组。完成所有 $y$ 方向网格线的计算后，我们得到了中间解 $u^{n+1/2}$。在第二步中，角色互换：我们在 $y$ 方向上是隐式的，而在 $x$ 方向上是显式的。此时，对于每一条 $x$ 方向的网格线，我们求解一个关于 $y$ 方向未知数的[三对角方程组](@entry_id:163398)。这个过程的[计算效率](@entry_id:270255)远高于直接求解二维耦合系统。

为了分析该格式的性质，我们可以消去中间变量 $u^{n+1/2}$。假设算子 $(I - \theta L_x)$ 和 $(I - \theta L_y)$ 可逆，并且它们相互**通勤 (commute)**，即 $L_x L_y = L_y L_x$（这在[常系数](@entry_id:269842)和均匀矩形网格下成立），我们可以得到等价的单步格式 [@problem_id:3429902]：
$$
\left(I - \theta L_x\right)\left(I - \theta L_y\right) u^{n+1} = \left(I + \theta L_x\right)\left(I + \theta L_y\right) u^{n}
$$
这个单步形式清晰地展示了PR格式的本质：它用两个可分离的一维算子的乘积来近似二维的隐式算子。

#### 精度与相容性

PR格式的一个关键优点是它在时间上具有二阶精度，即全局误差为 $O(\Delta t^2)$。我们可以通过分析其**[局部截断误差](@entry_id:147703) (Local Truncation Error, LTE)** 来验证这一点。[局部截断误差](@entry_id:147703)定义为将方程的精确解代入数值格式后得到的残差。

我们考察PR格式的单步形式。将其展开，我们得到：
$$
\left(I - \theta(L_x+L_y) + \theta^2 L_x L_y\right) u^{n+1} = \left(I + \theta(L_x+L_y) + \theta^2 L_x L_y\right) u^n
$$
与原始的CN格式 $\left(I - \theta(L_x + L_y)\right) u^{n+1} = \left(I + \theta(L_x + L_y)\right) u^n$ 相比，PR格式在等式两边都增加了一个 $\theta^2 L_x L_y$ 项。这意味着PR格式与CN格式相差一个扰动项 $\theta^2 L_x L_y (u^{n+1} - u^n)$。由于 $u^{n+1} - u^n = O(\Delta t) = O(\theta)$，这个扰动项的量级为 $O(\theta^3) = O(\Delta t^3)$。由于CN格式本身的[局部截断误差](@entry_id:147703)就是 $O(\Delta t^3)$，这个额外的扰动项并不会降低格式的精度。因此，PR格式保持了时间上的[二阶精度](@entry_id:137876)。

我们可以更严格地进行分析。考虑PDE $u_t = (\alpha u_{xx} + \beta u_{yy})$ 的一个精确特征解 $u(x,y,t) = \exp(\lambda t) \cos(\mu x) \cos(\nu y)$，其中 $\lambda = -(\alpha\mu^2 + \beta\nu^2)$ [@problem_id:3429890]。对于该解，算子 $X = \alpha \partial_{xx}$ 和 $Y = \beta \partial_{yy}$ 的作用仅仅是乘以对应的[特征值](@entry_id:154894) $\lambda_X = -\alpha\mu^2$ 和 $\lambda_Y = -\beta\nu^2$。将精确解代入PR格式的残差定义中，并通过泰勒展开，可以证明其[局部截断误差](@entry_id:147703)的最低阶项是 $O(\Delta t^3)$。具体来说，其残差 $\rho^{n+1}$ 的主项为：
$$
\rho^{n+1} = \frac{1}{12}(\lambda_X^3 + \lambda_Y^3) \Delta t^3 u(t_n) + O(\Delta t^4) = \frac{1}{12}\left((-\alpha\mu^2)^3 + (-\beta\nu^2)^3\right) \Delta t^3 u(t_n) + O(\Delta t^4)
$$
由于残差是 $O(\Delta t^3)$，这表明PR格式是二阶相容的，因此其全局误差为 $O(\Delta t^2)$。

#### 稳定性分析

PR格式的另一个核心优势是其**[无条件稳定性](@entry_id:145631) (unconditional stability)**。对于[常系数](@entry_id:269842)问题，我们可以使用冯·诺依曼（Fourier）分析来证明这一点。考虑一个离散的傅里葉模态 $u_{i,j}^n = (\zeta)^n e^{i(k_x i h_x + k_y j h_y)}$，其中 $\zeta$ 是**[放大因子](@entry_id:144315) (amplification factor)**。稳定性要求对所有[波数](@entry_id:172452) $(k_x, k_y)$，都有 $|\zeta| \le 1$。

通过将傅里葉模态代入PR格式的两个子步骤，我们可以求解得到[放大因子](@entry_id:144315) [@problem_id:3429871] [@problem_id:3429863]。对于标准的[二阶中心差分](@entry_id:170774)算子，其傅里葉符号（[特征值](@entry_id:154894)）为 $\hat{D}_x = -\frac{4}{h_x^2}\sin^2(\frac{k_x h_x}{2})$ 和 $\hat{D}_y = -\frac{4}{h_y^2}\sin^2(\frac{k_y h_y}{2})$。最终，整个时间步的[放大因子](@entry_id:144315) $G(k_x, k_y)$ 为：
$$
G(k_x, k_y) = \frac{\left(1 + \frac{\alpha \Delta t}{2} \hat{D}_x\right)\left(1 + \frac{\alpha \Delta t}{2} \hat{D}_y\right)}{\left(1 - \frac{\alpha \Delta t}{2} \hat{D}_x\right)\left(1 - \frac{\alpha \Delta t}{2} \hat{D}_y\right)}
$$
将 $\hat{D}_x$ 和 $\hat{D}_y$ 的表达式代入，并定义[无量纲数](@entry_id:136814) $r_x = \frac{\alpha \Delta t}{h_x^2}$ 和 $r_y = \frac{\alpha \Delta t}{h_y^2}$，我们得到：
$$
G(k_x, k_y) = \frac{\left(1 - 2r_x\sin^2(\frac{k_x h_x}{2})\right)\left(1 - 2r_y\sin^2(\frac{k_y h_y}{2})\right)}{\left(1 + 2r_x\sin^2(\frac{k_x h_x}{2})\right)\left(1 + 2r_y\sin^2(\frac{k_y h_y}{2})\right)}
$$
由于 $r_x, r_y > 0$ 且 $\sin^2(\cdot) \ge 0$，上式中每个括号内的项都可以看作是 $\frac{1-a}{1+a}$ 的形式，其中 $a \ge 0$。对于任何非负实数 $a$，我们都有 $|\frac{1-a}{1+a}| \le 1$。因此，放大因子的模长 $|G(k_x, k_y)|$ 是两个模长不大于1的数的乘积，故其自身模长也不大于1。即：
$$
\sup_{k_x, k_y} |G(k_x, k_y)| = 1
$$
这证明了PR格式对于[二维热方程](@entry_id:746155)是无条件稳定的，即无论时间步长 $\Delta t$ 和空间步长 $h_x, h_y$ 如何取值，数值解都不会发散。

从[算子理论](@entry_id:139990)的角度看，我们也可以得到同样的结论 [@problem_id:3429861]。如果算子 $A$ 和 $B$ 共享一套完整的[特征向量](@entry_id:151813)，并且它们的[特征值](@entry_id:154894) $\lambda_A, \lambda_B$ 均为非正实数，则[放大因子](@entry_id:144315)可以表示为 $G(z_A, z_B) = \frac{(1+z_A/2)(1+z_B/2)}{(1-z_A/2)(1-z_B/2)}$，其中 $z_A=\Delta t \lambda_A \le 0$，$z_B=\Delta t \lambda_B \le 0$。容易验证，对于所有 $z_A \le 0$ 和 $z_B \le 0$，我们都有 $|G(z_A, z_B)| \le 1$。这个方法从更抽象的层面证实了其[无条件稳定性](@entry_id:145631)。

### 非交换算[子带](@entry_id:154462)来的挑战与 Douglas-Gunn 格式

PR格式的优雅与高效是建立在一个关键假设之上的：**空间算子 $L_x$ 和 $L_y$ 相互通勤**。对于[常系数](@entry_id:269842)问题 $u_t = \alpha u_{xx} + \beta u_{yy}$ 在矩形网格上，离散算子确实通勤。然而，一旦我们面对更一般的问题，例如带有变量系数的扩散方程 $u_t = \partial_x(a(x,y) \partial_x u) + \partial_y(b(x,y) \partial_y u)$，离散后的算子 $A_x$ 和 $A_y$ 通常不再通勤，即 $[A_x, A_y] := A_x A_y - A_y A_x \neq 0$。

#### PR格式的精度下降

当算子不通勤时，PR格式的精度会从二阶下降到一阶。这是因为在推导单步格式时，我们依赖于算子顺序的可交换性。[因子分解](@entry_id:150389) $(I - \theta(L_x+L_y)) \approx (I-\theta L_x)(I-\theta L_y) = I - \theta(L_x+L_y) + \theta^2 L_x L_y$ 引入的误差与[Crank-Nicolson格式](@entry_id:147733)的差异，在不通勤的情况下，会产生一个 $O(\Delta t^2 [A_x, A_y])$ 的项，这个项不再是 $O(\Delta t^3)$，从而导致整个格式的[局部截断误差](@entry_id:147703)变为 $O(\Delta t^2)$，全局精度降为 $O(\Delta t)$。

更深入的分析可以使用[Magnus展开](@entry_id:141768)等工具 [@problem_id:3429911]。对于不通勤的算子，PR格式的演化算子 $G_{\mathrm{PR}}(\Delta t)$ 的对数展开式中，会出现由[交换子](@entry_id:158878)构成的误差项。其主误差项为 $O(\Delta t^3)$，具体形式为：
$$
\ln G_{\mathrm{PR}}(\Delta t) = \Delta t(A_x + A_y) + \frac{\Delta t^3}{12}\left([A_x,[A_x,A_y]] + [A_y,[A_y,A_x]]\right) + \mathcal{O}(\Delta t^5)
$$
这个 $O(\Delta t^3)$ 的项源于算子的不通勤性，它扰动了原本的[二阶精度](@entry_id:137876)。

#### Douglas-Gunn (DG) 格式

为了解决PR格式在变系数问题上的精度下降问题，Douglas和Gunn提出了一种修正的ADI格式，即[DG格式](@entry_id:178043)。[DG格式](@entry_id:178043)通过一个多阶段的“预测-校正”过程来构建，从而抵消由算子不通勤性引入的误差。对于方程 $u_t = (A_x + A_y)u$，一个标准的二阶[DG格式](@entry_id:178043)如下 [@problem_id:3429886]：

**第一步（预测步）：**
$$
u^* = u^n + \Delta t (A_x+A_y)u^n
$$

**第二步（x方向校正）：**
$$
\left(I - \frac{\Delta t}{2} A_x\right) u^{**} = u^* - \frac{\Delta t}{2} A_x u^n
$$

**第三步（y方向校正）：**
$$
\left(I - \frac{\Delta t}{2} A_y\right) u^{n+1} = u^{**} - \frac{\Delta t}{2} A_y u^n
$$

通过代数替换和[泰勒展开](@entry_id:145057)可以证明，这个三步格式的[局部截断误差](@entry_id:147703)为 $O(\Delta t^3)$，即使在 $A_x$ 和 $A_y$ 不通勤的情况下也是如此，从而保证了其二阶时间精度和[无条件稳定性](@entry_id:145631)。其核心思想是，预测步中引入的显式误差，在后续的隐式校正步骤中被高阶地抵消掉了。

#### PR与[DG格式](@entry_id:178043)的比较：[数值各向异性](@entry_id:752775)

除了对变系数的鲁棒性不同，PR和[DG格式](@entry_id:178043)在处理物理各向异性（即不同方向的[扩散](@entry_id:141445)系数不同）时也表现出不同的特性 [@problem_id:3429909]。

- **PR格式** 的[放大因子](@entry_id:144315) $G_{\mathrm{PR}}$ 在结构上对于 $A_x$ 和 $A_y$ 是对称的。这意味着如果物理问题是各向同性的（例如 $\alpha=\beta$），则[数值阻尼](@entry_id:166654)（由 $|G|$ 决定）在所有方向上也是对称的。如果物理问题是各向异性的，PR格式会忠实地反映这种物理上的各向异性，而不会引入额外的、纯粹由[数值格式](@entry_id:752822)导致的“[数值各向异性](@entry_id:752775)”。

- **[DG格式](@entry_id:178043)** 的[标准形式](@entry_id:153058)（如上所述）在结构上对于 $A_x$ 和 $A_y$ 是不对称的。这意味着即使对于物理上各向同性的问题，[DG格式](@entry_id:178043)也会引入[数值各向异性](@entry_id:752775)，其阻尼特性会依赖于[算子分裂](@entry_id:634210)的顺序。虽然可以通过对称化的分裂步骤来缓解此问题，但标准[DG格式](@entry_id:178043)的这一特性是在追求对非交换算子的鲁棒性时付出的一个代价。例如，我们可以定义一个敏感度因子 $S = G_{\mathrm{PR}}(k_x, 0) / G_{\mathrm{DG}}(0, k_y)$ 来量化这种差异。在一个具体的各向异性问题中（$\alpha=1, \beta=4$），可以计算出 $S = 253/9 \approx 28.1$，这显著地表明了两种格式在处理不同方向的高频模态时阻尼特性的巨大差异 [@problem_id:3429909]。

### 推广与应用

[ADI方法](@entry_id:746385)的思想具有很强的扩展性，可以应用于更复杂的问题。

#### 广义ADI格式

PR和[DG格式](@entry_id:178043)可以被看作是一个更广泛的ADI格式家族中的特例。例如，可以构建一个含参数 $\theta$ 的广义ADI格式，并通过[泰勒展开](@entry_id:145057)分析，找到能使格式达到[二阶精度](@entry_id:137876)的 $\theta$ 值。分析表明，为了使格式的泰勒展开与精确解的指数算子展开在 $O(\Delta t^2)$ 阶上吻合，参数需要取 $\theta=1/2$ [@problem_id:3429882]。这揭示了在ADI格式设计中，时间步分裂点（即中间步的位置）的选择对于保证高精度至关重要。

#### 处理混合导数项

当PDE包含[混合偏导数](@entry_id:139334)项时，例如 $u_t = a u_{xx} + 2b u_{xy} + c u_{yy}$，标准的ADI分裂会遇到困难，因为 $u_{xy}$ 项内在耦合了 $x$ 和 $y$ 方向。一个常见的处理策略是将 $L_x$ 和 $L_y$ 算子部分继续做隐式处理，而将耦合的混合导数算子 $M$ 完全显式处理 [@problem_id:3429906]。例如，修改后的PR格式可以写成：
$$
\left(I - \frac{\Delta t}{2} L_x\right)\left(I - \frac{\Delta t}{2} L_y\right) u^{n+1} = \left(I + \frac{\Delta t}{2} L_x\right)\left(I + \frac{\Delta t}{2} L_y\right) u^n + \Delta t M u^n
$$
这种处理方式保留了[求解三对角系统](@entry_id:166973)的[计算效率](@entry_id:270255)，但显式处理的 $M$ 项可能会对格式的稳定性产生影响。其放大因子为：
$$
G(k_x, k_y) = \frac{\left(1 + \frac{\Delta t}{2}\lambda_{L_x}\right)\left(1 + \frac{\Delta t}{2}\lambda_{L_y}\right) + \Delta t \lambda_M}{\left(1 - \frac{\Delta t}{2}\lambda_{L_x}\right)\left(1 - \frac{\Delta t}{2}\lambda_{L_y}\right)}
$$
其中 $\lambda_M$ 是算子 $M$ 的傅里葉符号。分析这个[放大因子](@entry_id:144315)的模长会发现，[无条件稳定性](@entry_id:145631)不再得到保证，稳定性条件将依赖于混合导数项的系数 $b$ 以及时间步长 $\Delta t$。这展示了在应用[ADI方法](@entry_id:746385)时，必须根据具体方程的结构做出仔细的设计和分析。

总之，Peaceman-Rachford和[Douglas-Gunn格式](@entry_id:748652)是求解多维[抛物型方程](@entry_id:144670)的强大工具。PR格式简洁高效，在算子通勤的情况下表现优异。而[DG格式](@entry_id:178043)则通过更精巧的设计，将[二阶精度](@entry_id:137876)推广到了更具挑战性的变系数和[非交换](@entry_id:136599)算子问题中，展示了数值方法设计中精度、稳定性与计算效率之间深刻的权衡与折衷。