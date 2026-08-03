## 引言
表面张力是决定多相流体系统行为的关键物理效应，从微观的液滴动力学到宏观的工业过程，其影响无处不在。然而，在计算流体动力学（CFD）中，准确模拟这一作用于尖锐、动态演化界面上的力，尤其是在固定的欧拉网格上，是一个重大的数值挑战。

本文旨在系统性地解决这一问题，深入剖析一种强大而广泛应用的建模技术——连续介质表面力（Continuum Surface Force, CSF）模型。通过学习本文，读者将全面掌握如何将复杂的界面现象转化为可计算的物理模型。

我们将分三步展开：首先，在“原理与机制”一章中，我们将揭示CSF模型如何巧妙地将表面张力从一个界面应力转化为一个体积力源项，并探讨其数值实现中的核心要素与挑战，如伪电流问题。接着，在“应用与交叉学科联系”一章中，我们将展示CSF模型在模拟瑞利-普拉托不稳定性、马兰戈尼流以及与材料科学、地球物理学等领域交叉问题中的强大功能。最后，通过“动手实践”部分，您将有机会亲手实现和验证CSF模型的关键方面，将理论知识转化为实践能力。现在，让我们从CSF模型的基本原理开始，深入探索其精妙之处。

## 原理与机制

在本章中，我们将深入探讨在计算流体动力学中对表面张力进行建模的核心原理和机制。我们将重点介绍**连续介质表面力 (Continuum Surface Force, CSF)** 模型，这是一种在欧拉网格框架下处理相间界面张力效应的强大而广泛应用的方法。我们将从其物理基础出发，逐步构建其数学和数值表示，并详细分析在实际应用中遇到的关键挑战及其解决方案。

### 从表面应力到体积力：连续介质表面力模型

在物理上，表面张力是存在于两种不混溶流体相界面上的一个内聚效应。它在宏观上表现为一种作用于界面单位长度上的力，或等效地，单位面积上的能量。这种效应使得液体表面趋向于收缩到最小可能面积。对于一个弯曲的界面，表面张力会导致界面两侧产生压力差，这一关系由著名的 **Young-Laplace 方程** 描述：

$ \Delta p = \sigma \kappa $

其中, $\Delta p$ 是跨界面的压力跃变，$ \sigma $ 是表面张力系数，而 $ \kappa $ 是界面的平均曲率。在经典的流体力学表述中，这个压力跃变体现为界面上的一个**法向应力跳跃条件**。例如，对于一个位于流体2中的静态球形液滴（流体1），半径为 $R$，其曲率为 $ \kappa = 2/R $，压力跃变为 $ \Delta p = 2\sigma/R $ [@problem_id:3368660]。

然而，在基于固定欧拉网格的数值方法（如有限体积法）中，精确追踪并直接在 sharp interface 上施加这种跳跃条件是极其困难的。CSF 模型通过一种巧妙的转化解决了这个问题：它将作用在二维表面上的奇异力（singular force）重新表述为一个在三维空间中连续分布但仅限于界面附近一个薄层内的**体积力 (volumetric force)** [@problem_id:3368602]。

这个体积力密度 $\mathbf{f}_s$ 的数学形式可以写作：

$ \mathbf{f}_s = \sigma \kappa \mathbf{n} \delta_s $

让我们逐项解析这个表达式：
- $ \sigma $ 是表面张力系数，一个物性参数。
- $ \kappa $ 是界面的**平均曲率**。
- $ \mathbf{n} $ 是指向界面某一侧的**单位法向量**。
- $ \delta_s $ 是一个**狄拉克δ分布 (Dirac delta distribution)**，其支撑集 (support) 仅限于相界面 $ \Gamma(t) $。它的作用是将表面力“约束”在界面上。从数学上讲，对于任何光滑的测试函数 $\phi$，它满足 $ \int_{\Omega} \phi \, \delta_s \, \mathrm{d}V = \int_{\Gamma(t)} \phi \, \mathrm{d}S $。

通过这种方式，表面张力效应可以作为一个源项直接加入到单流体公式的Navier-Stokes动量方程中：

$ \rho\left(\frac{\partial \mathbf{u}}{\partial t} + \mathbf{u}\cdot\nabla \mathbf{u}\right) = -\nabla p + \nabla\cdot\left(2\mu\,\mathbf{D}(\mathbf{u})\right) + \rho \mathbf{g} + \mathbf{f}_s $

其中 $\rho$ 是密度，$\mu$ 是粘度，$\mathbf{u}$ 是速度， $p$ 是压力，$\mathbf{g}$ 是重力加速度。这种“一体化”的方法极大地简化了多相流问题的数值处理。

### 界面几何的数值表示

为了计算CSF力项 $\mathbf{f}_s = \sigma \kappa \mathbf{n} \delta_s$，我们必须首先在整个计算域（或至少在界面附近）获得界面的几何信息，即法向量 $\mathbf{n}$ 和曲率 $\kappa$。这通常通过一个隐式的标量场来表示界面位置，最常见的方法是**流体体积函数法 (Volume of Fluid, VOF)** 和 **水平集方法 (Level Set method)** [@problem_id:3368670]。

#### 水平集方法 (Level Set)

在水平集方法中，界面 $\Gamma(t)$ 被定义为一个连续函数 $\phi(\mathbf{x}, t)$ 的零等值面，即 $ \Gamma(t) = \{\mathbf{x} : \phi(\mathbf{x}, t)=0\} $。通常，$\phi$ 被构造为一个**符号距离函数 (Signed Distance Function, SDF)**，其值表示点 $\mathbf{x}$ 到界面的最短距离，符号则表示该点位于哪一流体中。例如，我们可以定义在流体1中 $\phi > 0$，在流体2中 $\phi  0$。

利用SDF，几何属性的计算变得非常直接：
- **单位法向量**: 法向量指向 $\phi$ 增加的方向。根据SDF的定义，其梯度模长为1，即 $|\nabla \phi| = 1$。因此，单位法向量就是梯度的方向：
  $ \mathbf{n} = \frac{\nabla \phi}{|\nabla \phi|} = \nabla \phi $
- **平均曲率**: 曲率是法向量场的散度。对于SDF，曲率的计算可以被极大地简化：
  $ \kappa = -\nabla \cdot \mathbf{n} = -\nabla \cdot (\nabla \phi) = -\nabla^2 \phi $

这种简化的前提是 $\phi$ 严格保持为SDF。正如我们稍后将讨论的，这在数值计算中是一个需要特别处理的挑战 [@problem_id:3368610]。

#### 流体体积函数法 (VOF)

VOF方法在每个网格单元中定义一个**体积分数 (volume fraction)** $C(\mathbf{x}, t)$，其值在0和1之间。$C=1$ 表示单元完全被流体1填充，$C=0$ 表示完全被流体2填充，而 $0  C  1$ 则表示该单元包含界面。

为了计算几何属性，通常需要根据离散的 $C$ 场重建一个连续的函数。法向量和曲率的计算方式与水平集方法类似，但使用的是 $C$ 函数：
- **单位法向量**: $ \mathbf{n} = \frac{\nabla C}{|\nabla C|} $
- **平均曲率**: $ \kappa = -\nabla \cdot \mathbf{n} = -\nabla \cdot \left( \frac{\nabla C}{|\nabla C|} \right) $

值得注意的是，直接对 VOF 的体积分数场 $C$ 求拉普拉斯（即 $-\nabla^2 C$）来计算曲率是不正确的，因为它忽略了梯度模长的归一化步骤，会导致结果依赖于界面 smeared 的程度 [@problem_id:3368670]。

#### 从奇异力到正则化力

理论上的狄拉克δ分布 $\delta_s$ 在离散网格上是无法表示的。因此，在数值实践中，我们必须用一个在界面附近具有有限厚度的**正则化核函数 (regularized kernel)** $\delta_{s,\epsilon}$ 来近似它。这个核函数的支撑集宽度由参数 $\epsilon$ 控制，而 $\epsilon$ 通常与网格尺寸 $h$ 成正比，以确保力在几个网格单元上平滑分布。

一个常用的核函数是基于余弦函数的平滑核 [@problem_id:3368623]：
$$
\delta_{s,\epsilon}(\phi) =
\begin{cases}
\dfrac{1}{2\epsilon}\left(1 + \cos\left(\dfrac{\pi \phi}{\epsilon}\right)\right),  |\phi| \le \epsilon, \\
0,  \text{otherwise.}
\end{cases}
$$
这个核函数具有几个重要的性质：
1.  **归一化**: 对于任意 $\epsilon > 0$，其积分为1，即 $ \int_{-\infty}^{\infty} \delta_{s,\epsilon}(\phi)\, d\phi = 1 $。这保证了无论界面如何 smeared，施加的总力是守恒的。
2.  **对称性**: 这是一个偶函数，其一阶矩为零，即 $ \int_{-\infty}^{\infty} \phi \, \delta_{s,\epsilon}(\phi)\, d\phi = 0 $。这意味着正则化后的力的质心恰好位于 $\phi=0$ 的界面上，不会引入人为的力矩或偏移。
3.  **峰值**: 其最大值在 $\phi=0$ 处取得，为 $1/\epsilon$。这意味着界面越薄（$\epsilon$越小），体积力的峰值越高。

在VOF方法中，一个常见的简化是将 $\delta_s$ 直接近似为梯度模长 $|\nabla C|$。这使得体积力表达式变为 $\mathbf{f}_s = \sigma \kappa \mathbf{n} \delta_s \approx \sigma \kappa (\frac{\nabla C}{|\nabla C|}) |\nabla C| = \sigma \kappa \nabla C$ [@problem_id:3368602] [@problem_id:3368627]。这个形式在许多实现中被采用。

### 数值挑战与伪电流

尽管CSF模型在概念上很优雅，但其数值实现充满了挑战。其中最臭名昭著的问题是**伪电流 (spurious currents)** 或寄生电流 (parasitic currents)。这是一个数值伪影，即在一个本应保持静态的弯曲界面（如静止的液滴）附近，会产生非物理性的、持续存在的速度场 [@problem_id:3368617]。

伪电流的根本原因在于离散化的动量方程中，压力梯度项和表面张力体积力项之间存在**离散不平衡 (discrete imbalance)**。在静态平衡状态下，连续介质的动量方程简化为 $ \nabla p = \mathbf{f}_s $。这意味着表面张力力场必须是一个保守场，即它可以表示为某个标量势的梯度。

然而，在离散的有限体积（或有限差分）网格上，我们计算的是离散压力梯度 $(\nabla p)_d$ 和离散表面张力 $(\mathbf{f}_s)_d$。除非这两个离散算子经过精心设计以保持兼容，否则即使在理论上应该平衡的情况下，它们的差值也不会为零：
$ (\nabla p)_d - (\mathbf{f}_s)_d \neq \mathbf{0} $
这个非零的残余力会驱动流体产生非物理的流动，即伪电流。

伪电流的幅度与多个因素有关：
1.  **曲率计算误差**: 曲率计算涉及二阶导数，对界面场（$\phi$或$C$）中的噪声非常敏感。网格尺度的高频噪声（波数 $k \sim \pi/h$）在计算曲率时会被放大 $k^2$ 倍 [@problem_id:3368700]。这意味着来自界面表示的微小扰动会导致表面张力力场出现大的、波动的误差。
2.  **算子不一致**: 如上所述，如果计算压力梯度的离散算子与计算表面张力力的算子在 stencil 或代数结构上不兼容，即使几何信息（$\mathbf{n}, \kappa$）是精确的，也会产生不平衡 [@problem_id:3368630]。

在低雷诺数的斯托克斯流极限下，我们可以通过量纲分析来估计伪电流的量级。残余力 $f_{res} \sim \sigma \epsilon_\kappa / h$ (其中 $\epsilon_\kappa$ 是曲率误差，力分布在厚度为 $h$ 的层上) 被粘性力 $\mu U_s / h^2$ 平衡。这导致伪电流速度 $U_s$ 的一个关键标度关系 [@problem_id:3368617]:
$ U_s \sim \frac{\sigma h}{\mu} \epsilon_\kappa $
如果曲率误差本身与网格无关（例如，由界面场的噪声 $\varepsilon_{noise}$ 引起），那么 $U_s \sim \sigma \varepsilon_{noise} / \mu$，这意味着**减小网格尺寸并不能减小伪电流**，这是一个非常棘手的问题 [@problem_id:3368700]。

### 高级技术与数值考量

为了克服上述挑战，研究人员开发了多种高级技术。

#### 平衡力离散化 (Balanced-Force Discretization)

这是减少伪电流最根本的方法。其核心思想是确保离散的表面张力项 $(\mathbf{f}_s)_d$ 在代数上可以精确地表示为某个标量场的离散梯度，使用的梯度算子与压力梯度算子 $(\nabla)_d$ 相同。通过这种方式，数值压力场可以精确地调整自身以完全抵消表面张力力，从而在静态情况下实现 machine-precision 的平衡 [@problem_id:3368630] [@problem_id:3368627]。这通常需要精心设计表面张力项和压力梯度项在控制体上的位置和插值方法。

#### 改进的曲率估计

由于曲率误差是伪电流的主要驱动因素之一，改进其计算精度至关重要。
- **界面场平滑**: 在计算导数之前，对界面场（$\phi$ 或 $C$）进行适度平滑，可以有效滤除高频噪声，抑制 $k^2$ 误差放大效应 [@problem_id:3368700]。
- **几何重构方法**: 在VOF框架中，可以不直接对 $C$ 场求导，而是先利用 $C$ 的值重构出界面的几何形状（例如，使用**高度函数 (Height-Function)** 方法），然后从重构的几何形状解析地计算曲率。这种方法对噪声不敏感，能显著降低伪电流 [@problem_id:3368660] [@problem_id:3368700]。
- **水平集重初始化**: 在水平集方法中，流体速度场的平流作用会使 $\phi$ 场偏离其SDF特性（即 $|\nabla\phi| \neq 1$）。这会导致曲率计算公式 $\kappa = -\nabla^2\phi$ 不再准确。完整的曲率公式 $\kappa = - \nabla \cdot (\nabla\phi / |\nabla\phi|)$ 包含复杂的项，对 $|\nabla\phi|$ 的偏离很敏感，容易引入误差 [@problem_id:3368610]。为了解决这个问题，需要周期性地对 $\phi$ 场进行**重初始化 (reinitialization)**，即求解一个偏微分方程（如 $ \partial_\tau \phi + \operatorname{sgn}(\phi_0)(|\nabla \phi| - 1) = 0 $）来将其重新恢复为SDF，同时保持零等值面位置不变。

#### 接触角处理

当界面与固体壁面接触时，必须施加**接触角 (contact angle)** 边界条件。在CSF框架下，这通常通过在靠近壁面的单元中调整法向量 $\mathbf{n}$ 来实现，强制使其与壁面法向量 $\mathbf{n}_w$ 满足关系 $ \mathbf{n} \cdot \mathbf{n}_w = \cos\theta $，其中 $\theta$ 是指定的接触角 [@problem_id:3368627]。

### 显式时间积分的稳定性

在许多求解器中，表面张力项因为其复杂性而被显式处理。然而，表面张力会在界面上引起高频的**毛细波 (capillary waves)**。显式时间积分格式的稳定性受到系统中传播速度最快的波的限制，即Courant-Friedrichs-Lewy (CFL) 条件。

毛细波的[色散关系](@entry_id:140395)为 $\omega^2 = (\sigma k^3) / \rho$，其中 $\omega$ 是角频率，$k$是波数。网格上能解析的最短波长与网格尺寸 $\Delta$ 成正比，对应最大波数 $k_{max} \sim 1/\Delta$。这导致了最高频率 $\omega_{max} \sim \sqrt{\sigma / (\rho \Delta^3)}$。

为了数值稳定，时间步长 $\Delta t$ 必须小于这些最快波的周期，从而得到一个严格的**毛细波CFL条件** [@problem_id:3368636]：
$ \Delta t_{max} \le C \sqrt{\frac{\rho \Delta^3}{\sigma}} $
其中 $C$ 是一个 $\mathcal{O}(1)$ 的常数。这个条件非常苛刻。例如，对于水（$\rho=1000\,\mathrm{kg/m^3}$, $\sigma=0.072\,\mathrm{N/m}$）和 $1\,\mathrm{mm}$ 的网格（$\Delta=10^{-3}\,\mathrm{m}$），使用 $C=0.5$ 的稳定常数，最大允许时间步长仅为 $ \Delta t_{max} \approx 1.86 \times 10^{-3}\,\mathrm{s} $。

这个限制与对流CFL条件（$\Delta t \propto \Delta$）有显著不同。由于 $\Delta t \propto \Delta^{3/2}$，当网格加密时，时间步长需要以更快的速度减小，这使得具有显式表面张力处理的高分辨率模拟在计算上异常昂贵。