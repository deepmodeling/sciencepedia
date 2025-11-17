## 引言
在[偏微分方程](@entry_id:141332)的数值求解中，任何[数值格式](@entry_id:752822)都是对真实解的一种近似。虽然[局部截断误差](@entry_id:147703)提供了对精度的初步评估，但它并未完全揭示误差在时间和空间中累积与传播的复杂动态，这正是理解和信任计算模拟结果的关键所在。为了弥补这一认知鸿沟，我们需要一个更全局的视角来分析[数值误差](@entry_id:635587)如何影响解的整体结构，例如波的形态、传播速度和振幅。

本文旨在系统性地介绍振幅与相位误差分析这一强大框架。在“原理与机制”一章中，我们将深入探讨[冯·诺依曼分析](@entry_id:153661)的核心思想，学习如何通过[放大因子](@entry_id:144315)将[误差分解](@entry_id:636944)为决定解衰减的振幅分量（数值耗散）和导致波形失真的相位分量（数值频散）。接着，在“应用与跨学科联系”一章中，我们将展示这一理论在实际问题中的威力，从比较不同格式的性能，到为地球物理、[流体力学](@entry_id:136788)等领域的复杂问题设计专门的数值方案。最后，通过“动手实践”部分，读者将有机会亲手应用这些分析工具，将理论知识转化为解决实际问题的能力。

## 原理与机制

在理解了[数值格式](@entry_id:752822)的截断误差是其精度的局部度量之后，我们转向一个更为全局的视角，分析误差在求解域中随时间的[累积和](@entry_id:748124)传播。本章介绍的方法，统称为[冯·诺依曼分析](@entry_id:153661)（或[傅里叶分析](@entry_id:137640)），通过将数值解分解为一系列傅里叶模式，并考察数值格式如何影响每个模式的振幅和相位，从而为我们提供了关于格式稳定性和准确性的深刻见解。

### 放大因子：一种统一的分析工具

对于线性[常系数](@entry_id:269842)[偏微分方程](@entry_id:141332)，其一个关键特性是[平移不变性](@entry_id:195885)。这意味着，当应用于一个傅里叶模式（即一个正弦或余弦波）时，其输出仍然是同一频率的傅里叶模式，只是振幅和相位可能有所改变。一个设计良好的线性[常系数](@entry_id:269842)[有限差分格式](@entry_id:749361)应继承这一特性。这使得傅里叶模式成为分析此类格式的理想工具。

考虑一个定义在均匀周期性网格上的单步、线性、[常系数](@entry_id:269842)差分格式。网格点索引为 $j$，时间层索引为 $n$。一个具有无量纲[波数](@entry_id:172452) $\theta$ 的离散傅里叶模式在时间层 $n$ 可以写作 $u_j^n = \hat{u}^n e^{ij\theta}$，其中 $\hat{u}^n$ 是该模式在时间 $n$ 的[复振幅](@entry_id:164138)。由于格式是线性和平移不变的，它作用于这个傅里叶模式的结果必然是相同波数的另一个傅里叶模式，即 $u_j^{n+1} = \hat{u}^{n+1} e^{ij\theta}$。

关键在于，新旧振幅之间存在一个固定的、仅依赖于[波数](@entry_id:172452) $\theta$ 的复数比例因子。我们将其定义为**放大因子** (amplification factor)，记作 $G(\theta)$。

$$ \hat{u}^{n+1} = G(\theta) \hat{u}^n $$

这个定义揭示了 $G(\theta)$ 的核心作用：它完全描述了单个傅里叶模式在一个时间步长内的演化。因此，通过分析 $G(\theta)$，我们可以理解格式对整个解（作为所有模式的叠加）的影响。从算子的角度看，$G(\theta)$ 是单步更新算子作用于其[特征函数](@entry_id:186820)（傅里叶模式 $e^{ij\theta}$）时对应的[特征值](@entry_id:154894) [@problem_id:3363488]。

为了找到特定格式的 $G(\theta)$，我们只需将傅里叶模式代入[差分方程](@entry_id:262177)。例如，考虑一个一般的显式两层格式：

$$ u^{n+1}_j = \sum_{m=-M}^{M} \alpha_m u^n_{j+m} $$

将 $u_j^n = \hat{u}^n e^{ij\theta}$ 代入，我们得到：

$$ \hat{u}^{n+1} e^{ij\theta} = \sum_{m=-M}^{M} \alpha_m (\hat{u}^n e^{i(j+m)\theta}) = \hat{u}^n e^{ij\theta} \left( \sum_{m=-M}^{M} \alpha_m e^{im\theta} \right) $$

根据 $G(\theta)$ 的定义，$\hat{u}^{n+1} = G(\theta) \hat{u}^n$，代入上式并消去公共项 $\hat{u}^n e^{ij\theta}$，我们便得到 $G(\theta)$ 的表达式 [@problem_id:3363488]：

$$ G(\theta) = \sum_{m=-M}^{M} \alpha_m e^{im\theta} $$

让我们以一个具体的例子来阐述。考虑一维线性[平流方程](@entry_id:144869) $u_t + c u_x = 0$ ($c>0$)，采用时间上的一阶向前欧拉和空间上的一阶[迎风](@entry_id:756372)（后向）差分格式：

$$ \frac{u_j^{n+1} - u_j^n}{\Delta t} + c \frac{u_j^n - u_{j-1}^n}{\Delta x} = 0 $$

整理后得到 $u_j^{n+1} = (1-\lambda)u_j^n + \lambda u_{j-1}^n$，其中 $\lambda = c\Delta t/\Delta x$ 是著名的**Courant–Friedrichs–Lewy (CFL) 数**。代入傅里叶模式 $u_j^n = \hat{u}^n e^{ij\theta}$，我们得到：

$$ \hat{u}^{n+1} e^{ij\theta} = (1-\lambda)\hat{u}^n e^{ij\theta} + \lambda \hat{u}^n e^{i(j-1)\theta} $$

消去 $\hat{u}^n e^{ij\theta}$，得到该格式的[放大因子](@entry_id:144315) [@problem_id:3363510]：

$$ G(\theta) = (1-\lambda) + \lambda e^{-i\theta} $$

这个复数 $G(\theta)$ 包含了格式在一个时间步内对[波数](@entry_id:172452)为 $\theta$ 的模式所做的一切——它既改变了振幅，也改变了相位。接下来，我们将分别探讨这两个方面。

### 振幅误差与[数值耗散](@entry_id:168584)

[放大因子](@entry_id:144315)的模 $|G(\theta)|$ 决定了傅里叶模式的振幅如何随时间演化。$|G(\theta)| > 1$ 意味着该模式的振幅会无限制地[指数增长](@entry_id:141869)，导致数值解发散。因此，对于一个稳定的格式，我们必须要求对于所有相关的波数 $\theta$，都满足**[冯·诺依曼稳定性](@entry_id:756579)条件**：

$$ |G(\theta)| \le 1 $$

$|G(\theta)| < 1$ 表示模式的振幅会随时间衰减。这种现象称为**[数值耗散](@entry_id:168584)** (numerical dissipation) 或[数值黏性](@entry_id:141318) (numerical viscosity)。如果原始的[偏微分方程](@entry_id:141332)本身是耗散的（例如，[热传导方程](@entry_id:194763)），那么[数值格式](@entry_id:752822)可能需要引入适量的耗散来模拟物理过程。然而，如果原始方程是守恒的（例如，线性[平流方程](@entry_id:144869)，其精确解的傅里叶模式振幅保持不变），那么任何由[数值格式](@entry_id:752822)引起的振幅衰减都是一种误差，称为**伪耗散** (spurious dissipation)。

为了更定量地描述这种效应，我们可以将离散的、步进式的放大过程与一个等效的连续指数衰减过程联系起来。如果一个模式在一个时间步 $\Delta t$ 内振幅乘以 $|G(\theta)|$，那么在时间 $t=n\Delta t$ 后，其振幅变为 $|G(\theta)|^n$。我们可以定义一个**[数值耗散](@entry_id:168584)率** $\delta(\kappa)$，使得等效的连续演化振幅为 $e^{-\delta(\kappa) t}$。在 $t=\Delta t$ 时，应有 $e^{-\delta(\kappa) \Delta t} = |G(\theta)|$。由此可解得 [@problem_id:3363548]：

$$ \delta(\kappa) = -\frac{1}{\Delta t} \ln|G(\theta)| $$

其中，$\kappa = \theta / \Delta x$ 是物理[波数](@entry_id:172452)。这个 $\delta(\kappa)$ 的单位是时间的倒数，代表了每单位时间的指数衰减率。对于一个守恒的PDE，其精确耗散率为零。此时，任何非零的 $\delta(\kappa)$ 都直接度量了格式引入的伪耗散。对于一个本身就耗散的PDE，其精确解的模式演化遵循 $e^{\text{Re}(\lambda(\kappa))t}$，其中 $\lambda(\kappa)$ 是PDE的符号。精确的衰减率是 $-\text{Re}(\lambda(\kappa))$。那么，**振幅误差率**就是数值耗散率与精确耗散率之差 [@problem_id:3363548]：

$$ \text{振幅误差率} = \delta(\kappa) - (-\text{Re}(\lambda(\kappa))) = \delta(\kappa) + \text{Re}(\lambda(\kappa)) $$

回到我们的[迎风格式](@entry_id:756374)例子，其放大因子为 $G(\theta) = (1-\lambda) + \lambda(\cos\theta - i\sin\theta)$。其模的平方为：

$$ |G(\theta)|^2 = (1 - \lambda + \lambda\cos\theta)^2 + (-\lambda\sin\theta)^2 = 1 - 2\lambda(1-\lambda)(1-\cos\theta) $$

利用半角公式 $1-\cos\theta = 2\sin^2(\theta/2)$，我们得到其振幅的简洁表达式 [@problem_id:3363510]：

$$ |G(\theta)| = \sqrt{1 - 4\lambda(1-\lambda)\sin^2(\frac{\theta}{2})} $$

由于线性[平流方程](@entry_id:144869)是守恒的，理想情况下 $|G(\theta)|$ 应恒等于 $1$。但从上式可以看出，只要 $\lambda \in (0,1)$ 且 $\sin(\theta/2) \neq 0$，我们就有 $|G(\theta)| < 1$。这意味着迎风格式总是耗散的。这种耗散在抑制高频[振荡](@entry_id:267781)（对应于大的 $\theta$）方面可能是有益的，但它也同样会不物理地耗散掉解中我们希望保留的中低频部分。

### [相位误差](@entry_id:162993)与数值频散

放大因子的辐角 $\arg(G(\theta))$ 决定了傅里叶模式的相位如何随[时间演化](@entry_id:153943)。一个[行波解](@entry_id:272909)可以表示为 $e^{i(kx - \omega t)}$，其中 $\omega$ 是[角频率](@entry_id:261565)。在一个时间步 $\Delta t$ 内，其相位变化为 $e^{-i\omega \Delta t}$。类似地，我们可以将数值解的一个傅里叶模式写成 $u_j^n \propto e^{i(j\theta - n\tilde{\omega}(\theta)\Delta t)}$，其中 $\tilde{\omega}(\theta)$ 是**数值角频率**。在一个时间步内，其[复振幅](@entry_id:164138)乘以因子 $e^{-i\tilde{\omega}(\theta)\Delta t}$。

将此与[放大因子](@entry_id:144315)的定义 $\hat{u}^{n+1} = G(\theta)\hat{u}^n$ 相比较，我们可以建立起 $G(\theta)$ 和 $\tilde{\omega}(\theta)$ 之间的联系。如果我们暂时忽略振幅变化（即假设 $|G(\theta)|=1$），则 $G(\theta) = e^{i\arg(G(\theta))}$。比较两种相位演化形式，可得 $e^{i\arg(G(\theta))} = e^{-i\tilde{\omega}(\theta)\Delta t}$。这给出了**数值频散关系** (numerical dispersion relation) [@problem_id:3363495] [@problem_id:3363488]：

$$ \tilde{\omega}(\theta) = -\frac{1}{\Delta t} \arg(G(\theta)) $$

波的**相速度** (phase velocity) 定义为 $c_p = \omega/k$。它描述了波形上恒定相位点（如波峰）的传播速度。精确的平流方程 $u_t+cu_x=0$ 的精确频散关系是 $\omega = ck$，因此其相速度对于所有波数都是常数 $c$。

数值格式的**数值相速度** (numerical phase velocity) 则为：

$$ \tilde{c}_p(\theta) = \frac{\tilde{\omega}(\theta)}{k} = \frac{\tilde{\omega}(\theta)}{\theta/\Delta x} $$

当 $\tilde{c}_p(\theta)$ 不等于精确相速度 $c$ 时，就产生了**相位误差**。更重要的是，当 $\tilde{c}_p(\theta)$ 依赖于波数 $\theta$ 时，不同波长的波将以不同的速度传播。这种现象称为**数值频散** (numerical dispersion)。一个最初由多个傅里叶[模式叠加](@entry_id:168041)构成的[波包](@entry_id:154698)，在数值[演化过程](@entry_id:175749)中会因为其组分以不同速度传播而变形或“散开”。

**绝对相位误差**定义为数值相速度与精确相速度之差 [@problem_id:3363495]：

$$ e_p(\theta) = \tilde{c}_p(\theta) - c $$

对于我们的迎风格式例子，$G(\theta) = (1 - \lambda + \lambda\cos\theta) - i(\lambda\sin\theta)$。其辐角为 [@problem_id:3363510]：

$$ \arg(G(\theta)) = \arctan\left(\frac{-\lambda\sin\theta}{1 - \lambda + \lambda\cos\theta}\right) = -\arctan\left(\frac{\lambda\sin\theta}{1 - \lambda(1-\cos\theta)}\right) $$

数值相速度为：

$$ \tilde{c}_p(\theta) = -\frac{\Delta x}{\theta\Delta t} \arg(G(\theta)) = \frac{c}{\lambda\theta} \arctan\left(\frac{\lambda\sin\theta}{1 - \lambda(1-\cos\theta)}\right) $$

显然，$\tilde{c}_p(\theta)$ 是 $\theta$ 的一个复杂函数，并且不等于常数 $c$。因此，[迎风格式](@entry_id:756374)既是耗散的，也是频散的。短波（大的 $\theta$）的传播速度与长波（小的 $\theta$）显著不同，导致波形失真。

### 误差来源的深度分析

放大因子 $G(\theta)$ 混合了空间离散和时间离散所共同引入的误差。为了更深入地理解误差的来源，我们可以采用两种强大的补充分析方法：[修正波数](@entry_id:141354)和修正方程。

#### [修正波数](@entry_id:141354)：分离空间误差

我们可以只关注空间差分算子本身引入的误差。考虑一个算子 $\mathcal{D}$ 用来逼近导数 $\partial_x$。当 $\mathcal{D}$ 作用于傅里叶模式 $e^{ij\theta}$ 时，其结果可以写成 $i\tilde{k}(\theta) e^{ij\theta}$ 的形式。这里的 $\tilde{k}(\theta)$ 被称为**[修正波数](@entry_id:141354)** (modified wavenumber) [@problem_id:3363503]。它代表了差分算子在傅里叶空间中的实际作用，而理想情况下它应该等于物理波数 $k = \theta/\Delta x$。

[修正波数](@entry_id:141354)通常是一个复数，$\tilde{k}(\theta) = \text{Re}\,\tilde{k}(\theta) + i\,\text{Im}\,\tilde{k}(\theta)$。
-   **实部 $\text{Re}\,\tilde{k}(\theta)$** 与[波的传播](@entry_id:144063)有关。$\text{Re}\,\tilde{k}(\theta)$ 与 $k$ 的偏差导致了频散。
-   **虚部 $\text{Im}\,\tilde{k}(\theta)$** 与振幅的增长或衰减有关。一个非零的 $\text{Im}\,\tilde{k}(\theta)$ 意味着该空间算子本身就是耗散或反耗散的 [@problem_id:3363503]。

例如，对于[二阶中心差分](@entry_id:170774)算子 $\mathcal{D}u_j = (u_{j+1}-u_{j-1})/(2\Delta x)$，我们应用到 $e^{ij\theta}$ 上：
$$ \mathcal{D} e^{ij\theta} = \frac{e^{i(j+1)\theta} - e^{i(j-1)\theta}}{2\Delta x} = \frac{e^{ij\theta}(e^{i\theta}-e^{-i\theta})}{2\Delta x} = \frac{e^{ij\theta}(2i\sin\theta)}{2\Delta x} = i\left(\frac{\sin\theta}{\Delta x}\right)e^{ij\theta} $$
因此，其[修正波数](@entry_id:141354)为 $\tilde{k}(\theta) = \frac{\sin\theta}{\Delta x}$ [@problem_id:3363503]。这是一个纯实数，意味着[中心差分](@entry_id:173198)本身是**非耗散**的。然而，由于 $\sin\theta/\Delta x \neq \theta/\Delta x = k$，它又是**频散**的。

这一性质推广到所有**斜对称** (skew-symmetric) 的差分格式。一个逼近一阶导数的算子，如果其系数满足反对称性 $a_m = -a_{-m}$，那么其[修正波数](@entry_id:141354)总是纯实的，因此该空间格式是天然保幅的。这是一个非常有用的设计原则 [@problem_id:3363530]。例如，我们可以构建一个四阶精度的斜对称格式来最小化频散误差，同时完全消除空间格式带来的耗散。通过求解[泰勒展开](@entry_id:145057)的系数方程，可以得到这样一个格式 [@problem_id:3363530]：
$$ (\mathcal{D}u)_j = \frac{1}{\Delta x}\left[\frac{2}{3}(u_{j+1}-u_{j-1}) - \frac{1}{12}(u_{j+2}-u_{j-2})\right] $$
其[修正波数](@entry_id:141354)为 $\tilde{k}(\theta) = \frac{\sin\theta(4-\cos\theta)}{3\Delta x}$，它是一个纯实数，因此该格式是无耗散的，但仍有（较小的）频散误差。

相比之下，[一阶迎风格式](@entry_id:749417) $\mathcal{D}u_j = (u_j - u_{j-1})/\Delta x$ 的[修正波数](@entry_id:141354)为 [@problem_id:3363503]：
$$ \tilde{k}(\theta) = \frac{\sin\theta}{\Delta x} - i\frac{1-\cos\theta}{\Delta x} $$
其非零的虚部表明，这个空间格式本身就带有耗散。

#### 修正方程：一种物理解释

另一种分析误差的方法是**修正方程** (modified equation) 方法。其思想是，一个[有限差分格式](@entry_id:749361)虽然意图求解某个PDE，但它实际上精确地求解了另一个不同的PDE，这个PDE包含了所有阶的[截断误差](@entry_id:140949)项。通过将差分格式中的每一项进行泰勒展开，并利用原PDE反复替换时间导数，我们可以得到这个修正方程。

对于我们的[迎风格式](@entry_id:756374)例子，通过[泰勒展开](@entry_id:145057)可以证明，它实际求解的方程（保留至最低阶误差项）是 [@problem_id:3363591]：

$$ u_t + c u_x = \left(\frac{c\Delta x}{2} - \frac{c^2\Delta t}{2}\right) u_{xx} + O(\Delta x^2, \Delta t^2) $$

这个方程令人震惊地揭示了该格式的内在行为。它不仅仅是平流方程 $u_t+cu_x=0$，而是附加了一个[二阶导数](@entry_id:144508)项，就像一个物理的[扩散](@entry_id:141445)或黏性项。这个项的系数 $\alpha = \frac{c\Delta x}{2}(1-\lambda)$ 被称为**[有效扩散系数](@entry_id:183973)** (effective diffusion coefficient)。这完美地解释了我们在[傅里叶分析](@entry_id:137640)中观察到的数值耗散现象：[迎风格式](@entry_id:756374)的[截断误差](@entry_id:140949)表现为一个物理的耗散过程！

这个 $\alpha$ 项总是非负的（在稳定条件下 $0 \le \lambda \le 1$），因此它总是一个耗散项，会抹平解中的尖锐特征。修正方程为我们提供了一种将抽象的[截断误差](@entry_id:140949)与具体的物理过程（如[扩散](@entry_id:141445)和频散）联系起来的强大方式。

### 数值误差的高级论题

#### 相速度误差与群速度误差

[相位误差](@entry_id:162993)的分析可以更进一步。除了单个波峰的[传播速度](@entry_id:189384)（相速度），我们还关心由多个波数构成的[波包](@entry_id:154698)的整体移动速度。这个速度由**群速度** (group velocity) $c_g = d\omega/dk$ 决定，它描述了[波包](@entry_id:154698)能量和信息的传播。

相应地，我们可以定义**数值群速度** (numerical group velocity) [@problem_id:3363538]：
$$ \tilde{c}_g(\theta) = \frac{d\tilde{\omega}}{dk} = \frac{d\tilde{\omega}}{d\theta}\frac{d\theta}{dk} = \Delta x \frac{d\tilde{\omega}}{d\theta} $$
**群速度误差** $\tilde{c}_g(\theta) - c_g$ 对于准确模拟[波包](@entry_id:154698)的传播至关重要。在许多应用中，如[天气预报](@entry_id:270166)或[地震波模拟](@entry_id:754654)，正确预测能量到达的时间比精确解析单个波纹的相位更为重要。

#### 多层格式与计算模式

以上分析主要针对两层（如 $n$ 和 $n+1$）格式。对于涉及更多时间层（如 $n-1, n, n+1$）的**多层格式** (multi-level schemes)，情况会变得更加复杂。以求解[平流方程](@entry_id:144869)的经典[蛙跳格式](@entry_id:163462) (leapfrog scheme) 为例：

$$ \frac{u_j^{n+1} - u_j^{n-1}}{2\Delta t} + c \frac{u_{j+1}^n - u_{j-1}^n}{2\Delta x} = 0 $$

进行[冯·诺依曼分析](@entry_id:153661)，代入 $u_j^n = G^n e^{ij\xi}$（这里用 $\xi$ 代替 $\theta$），我们会得到一个关于 $G$ 的[二次方程](@entry_id:163234) [@problem_id:3363590]：

$$ G^2 + (2i\mu\sin\xi)G - 1 = 0 $$

其中 $\mu = c\Delta t/\Delta x$。这个方程有两个根，$G_1$ 和 $G_2$。通过对[小波](@entry_id:636492)数 $\xi$ 进行分析，可以发现其中一个根 $G_1$ 逼近了精确解的放大因子 $e^{-i\mu\xi}$。这个根被称为**物理模式** (physical mode)。而另一个根 $G_2$ 则具有截然不同的行为，其相位近似为 $-\pi$。这个根被称为**计算模式** (computational mode) 或寄生模式。它的存在是多层格式引入的纯粹的数值产物。在[蛙跳格式](@entry_id:163462)中，这个计算模式的振幅大小与物理模式相同（$|G_1|=|G_2|=1$，在稳定条件下），但它的符号每步都会[振荡](@entry_id:267781)，可能导致解中出现高频的“棋盘”噪声。处理这些非物理的计算模式是设计和使用多层格式时的一个核心挑战。

#### 超越傅里叶分析：[非正规算子](@entry_id:752588)与[瞬时增长](@entry_id:263654)

[冯·诺依曼分析](@entry_id:153661)有一个根本性的限制：它严格依赖于一个正交的[傅里叶基](@entry_id:201167)底，这个基底能够[对角化](@entry_id:147016)差分算子。这只在具有[周期性边界条件](@entry_id:147809)的均匀网格上才能实现，因为此时的离散算子矩阵是**正规的** (normal)（即 $\mathbf{L}\mathbf{L}^* = \mathbf{L}^*\mathbf{L}$）。

然而，在许多实际问题中，边界条件是[非周期性](@entry_id:275873)的（例如Dirichlet或Neumann边界）。在这种情况下，空间离散算子矩阵 $\mathbf{L}$ 通常是**非正规的** (non-normal)。[非正规算子](@entry_id:752588)的[特征向量](@entry_id:151813)不再是相互正交的。

对于[非正规系统](@entry_id:270295)，即使所有[特征值](@entry_id:154894)的实部都小于等于零（对应于[冯·诺依曼条件](@entry_id:756578) $|G(\theta)|\le 1$），解的范数也可能在衰减到零之前经历一个显著的**[瞬时增长](@entry_id:263654)** (transient growth) [@problem_id:3363500]。这种增长是由于非正交的[特征向量](@entry_id:151813)之间可以发生短暂的[相长干涉](@entry_id:276464)。此时，仅靠谱（[特征值](@entry_id:154894)）分析会给出关于稳定性的误导性结论。

要正确地分析[非正规系统](@entry_id:270295)的稳定性，必须考察**resolvent** $(z\mathbf{I}-\mathbf{L})^{-1}$。[瞬时增长](@entry_id:263654)的大小与算子的**伪谱** (pseudospectrum) 密切相关，[伪谱](@entry_id:138878)衡量了算子对微小扰动的敏感性。一个定量度量[瞬时增长](@entry_id:263654)潜力的工具是**Kreiss常数** [@problem_id:3363500]：

$$ K(\mathbf{L}) := \sup_{\text{Re}(z)>0} \text{Re}(z) \|(z\mathbf{I}-\mathbf{L})^{-1}\| $$

这个量给出了系统范数演化 $\|e^{t\mathbf{L}}\|$ 的[上界](@entry_id:274738)。一个大的Kreiss常数预示着即使系统是[渐近稳定](@entry_id:168077)的，也可能出现巨大的瞬时放大。这一现象在[流体力学](@entry_id:136788)和其他[对流](@entry_id:141806)主导的问题中尤为重要，它解释了为什么即使在“线性稳定”的流场中也能观察到扰动的显著增长。