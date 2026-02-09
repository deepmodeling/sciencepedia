## 引言
在固体力学分析中，选择合适的坐标系是简化问题、高效求解的关键。对于大量涉及圆形边界、孔洞、或轴对称载荷的工程与物理问题——从高压容器到晶体中的缺陷——笛卡尔坐标系显得力不从心。极坐标系为此类问题提供了更为自然和强大的描述框架。然而，从固定的笛卡尔基矢量到随空间位置变化的极坐标基矢量的转变，也为运动学和动力学方程的推导带来了新的复杂性，构成了学习过程中的一个关键知识壁垒。

本文旨在系统性地攻克这一壁垒，为读者提供一个关于极坐标下固体力学问题的完整知识体系。我们将分三步深入探讨这一主题。首先，在“原理与机制”一章中，我们将从坐标系的几何基础出发，严谨推导应变-位移关系、平衡方程，并重点介绍求解二维弹性问题的强大工具——Airy应力函数法。接着，在“应用与交叉学科联系”一章中，我们将展示这些理论如何应用于解决经典的工程挑战，如厚壁圆筒、旋转圆盘和应力集中问题，并揭示其在断裂力学、材料科学乃至量子化学等前沿领域的深刻联系。最后，“动手实践”部分将提供一系列精心设计的问题，引导您将理论知识转化为解决实际问题的能力。

通过这一系列的学习，您将不仅掌握在极坐标下进行弹性力学分析的核心技术，更能深刻理解其在现代科学与工程中的广泛应用价值。

## 原理与机制

在连续介质力学中，问题的几何形状往往决定了最有效的分析坐标系。对于具有圆形或轴对称边界（例如孔洞、圆盘、圆柱体和楔形体）的问题，极坐标系 $(r, \theta)$ 提供了一种比笛卡尔坐标系更为自然和简洁的描述方式。本章旨在系统地阐述在极坐标系下进行固体力学分析所需的基本原理和关键机制。我们将从坐标系的几何基础出发，逐步建立运动学方程、动力学平衡方程，并最终探讨一种强大的求解二维弹性问题的系统方法——Airy 应力函数法。

### 极坐标系的几何基础与正交性

极坐标系由径向距离 $r$ 和从参考轴逆时针测量的角度 $\theta$ 定义。与笛卡尔坐标 $(x, y)$ 的转换关系为 $x = r \cos\theta$ 和 $y = r \sin\theta$。在极坐标系中，任意点的基矢量，即径向单位矢量 $\mathbf{e}_r$ 和切向单位矢量 $\mathbf{e}_\theta$，其方向随着点的移动而改变。这与笛卡尔坐标系中固定不变的基矢量 $(\mathbf{e}_x, \mathbf{e}_y)$ 形成了鲜明对比，也正是这种空间变异性导致了极坐标系下控制方程形式的复杂性。

一个坐标系的局部几何特性可以通过其**度量张量** $\mathbf{g}$ 来描述。度量张量定义了在坐标空间中测量距离、角度和体积的方式。在任意曲线坐标系 $(u^1, u^2)$ 中，无穷小距离的平方 $ds^2$ 由下式给出：
$$
ds^2 = \sum_{\mu, \nu=1}^{2} g_{\mu\nu} du^\mu du^\nu
$$
其中 $g_{\mu\nu}$ 是度量张量的分量。对于从笛卡尔坐标 $(x^1, x^2) = (x, y)$ 到极坐标 $(u^1, u^2) = (r, \theta)$ 的变换，度量张量分量可以通过以下变换法则计算：
$$
g_{\mu\nu} = \sum_{i=1}^{2} \frac{\partial x^i}{\partial u^\mu} \frac{\partial x^i}{\partial u^\nu}
$$
通过计算各个偏导数，我们可以得到极坐标系下的度量张量 [@problem_id:1658195]。
$$
\frac{\partial x}{\partial r} = \cos\theta, \quad \frac{\partial y}{\partial r} = \sin\theta
$$
$$
\frac{\partial x}{\partial \theta} = -r\sin\theta, \quad \frac{\partial y}{\partial \theta} = r\cos\theta
$$
由此，我们可以计算出度量张量的各个分量：
$$
g_{rr} = \left(\frac{\partial x}{\partial r}\right)^2 + \left(\frac{\partial y}{\partial r}\right)^2 = \cos^2\theta + \sin^2\theta = 1
$$
$$
g_{\theta\theta} = \left(\frac{\partial x}{\partial \theta}\right)^2 + \left(\frac{\partial y}{\partial \theta}\right)^2 = (-r\sin\theta)^2 + (r\cos\theta)^2 = r^2(\sin^2\theta + \cos^2\theta) = r^2
$$
$$
g_{r\theta} = g_{\theta r} = \frac{\partial x}{\partial r}\frac{\partial x}{\partial \theta} + \frac{\partial y}{\partial r}\frac{\partial y}{\partial \theta} = (\cos\theta)(-r\sin\theta) + (\sin\theta)(r\cos\theta) = 0
$$
因此，极坐标系下的度量张量矩阵为：
$$
\mathbf{g} = \begin{pmatrix} g_{rr} & g_{r\theta} \\ g_{\theta r} & g_{\theta\theta} \end{pmatrix} = \begin{pmatrix} 1 & 0 \\ 0 & r^2 \end{pmatrix}
$$
度量张量的非对角分量 $g_{r\theta}$ 和 $g_{\theta r}$ 为零，这一结果具有深刻的几何意义：它表明极坐标系是**正交坐标系**。这意味着在任何一点，径向基矢量 $\mathbf{e}_r$ 和切向基矢量 $\mathbf{e}_\theta$ 总是相互垂直的。这种正交性极大地简化了矢量和张量在分解和计算时的复杂性。无穷小线元长度的表达式也因此简化为 $ds^2 = dr^2 + r^2 d\theta^2$，直观地反映了勾股定理在无穷小尺度上的应用。

### 运动学：极坐标系下的应变与转动

在连续介质力学中，物体的运动由位移场 $\mathbf{u}$ 描述。在极坐标中，位移矢量可以分解为径向分量 $u_r$ 和切向分量 $u_\theta$：$\mathbf{u} = u_r \mathbf{e}_r + u_\theta \mathbf{e}_\theta$。变形由应变张量 $\boldsymbol{\varepsilon}$ 描述，它是位移梯度的对称部分。由于基矢量 $\mathbf{e}_r$ 和 $\mathbf{e}_\theta$ 的方向随位置变化，应变-位移关系式中会出现额外的项，这些项正是为了解释基矢量的旋转效应。

在小变形假设下，极坐标系中的应变分量由下式给出：
- **径向正应变** ($\varepsilon_{rr}$): 描述径向纤维的伸长。
$$
\varepsilon_{rr} = \frac{\partial u_r}{\partial r}
$$
- **环向正应变** ($\varepsilon_{\theta\theta}$): 描述圆周纤维的伸长，也称为“环状应变”。它不仅与 $u_\theta$ 的周向变化有关，还与径向位移本身有关，因为一个纯粹的径向膨胀会拉伸所有周向纤维。
$$
\varepsilon_{\theta\theta} = \frac{1}{r}\frac{\partial u_\theta}{\partial \theta} + \frac{u_r}{r}
$$
- **剪应变** ($\varepsilon_{r\theta}$): 描述径向线元与环向线元之间夹角的变化。
$$
\varepsilon_{r\theta} = \frac{1}{2} \left( \frac{1}{r}\frac{\partial u_r}{\partial \theta} + \frac{\partial u_\theta}{\partial r} - \frac{u_\theta}{r} \right)
$$
同时，位移梯度的反对称部分描述了物质微元的**刚体转动**。在二维平面问题中，该转动可以用一个标量场 $\omega$ 表示，其定义为：
$$
\omega = \frac{1}{2} \left( \frac{1}{r}\frac{\partial (r u_\theta)}{\partial r} - \frac{1}{r}\frac{\partial u_r}{\partial \theta} \right) = \frac{1}{2} \left( \frac{\partial u_\theta}{\partial r} + \frac{u_\theta}{r} - \frac{1}{r}\frac{\partial u_r}{\partial \theta} \right)
$$

为了更深刻地理解这些公式，我们可以分析一个具体的位移场 [@problem_id:2569229]。考虑一个由 $u_r = \alpha r$ 和 $u_\theta = \beta r$ 定义的位移场，其中 $\alpha$ 和 $\beta$ 为常数。

首先，我们计算应变分量：
- $\varepsilon_{rr} = \frac{\partial}{\partial r}(\alpha r) = \alpha$
- $\varepsilon_{\theta\theta} = \frac{1}{r}\frac{\partial}{\partial \theta}(\beta r) + \frac{\alpha r}{r} = 0 + \alpha = \alpha$
- $\varepsilon_{r\theta} = \frac{1}{2} \left( \frac{1}{r}\frac{\partial}{\partial \theta}(\alpha r) + \frac{\partial}{\partial r}(\beta r) - \frac{\beta r}{r} \right) = \frac{1}{2} (0 + \beta - \beta) = 0$
这个结果表明，该位移场对应一个**均匀膨胀**或收缩状态，其中径向和环向的伸长率处处相等 ($\varepsilon_{rr} = \varepsilon_{\theta\theta} = \alpha$)，且没有剪切变形 ($\varepsilon_{r\theta} = 0$)。这种变形被称为**均匀展缩** (uniform dilatation)。

接着，我们分析其刚体转动：
- $\omega = \frac{1}{2} \left( \frac{\partial}{\partial r}(\beta r) + \frac{\beta r}{r} - \frac{1}{r}\frac{\partial}{\partial \theta}(\alpha r) \right) = \frac{1}{2}(\beta + \beta - 0) = \beta$
转动场 $\omega$ 是一个常数 $\beta$，这意味着整个物体经历了一个**均匀的刚体转动**。

因此，位移场 $\mathbf{u} = (\alpha r) \mathbf{e}_r + (\beta r) \mathbf{e}_\theta$ 描述了一个均匀展缩（变形）和一个均匀刚体转动（非变形运动）的叠加。这个例子清晰地揭示了运动是如何分解为变形和刚体运动的，并且突出了仅从位移场本身的形式（例如，$u_\theta$ 与 $r$ 呈线性关系）并不能直接判断是否存在剪切或转动，必须通过完整的运动学关系进行计算。值得注意的是，任何从一个连续、单值的位移场派生出来的应变场，必然自动满足**圣维南协调条件**。对于本例，将 $\varepsilon_{rr}=\alpha, \varepsilon_{\theta\theta}=\alpha, \varepsilon_{r\theta}=0$ 代入极坐标下的协调方程，会发现方程恒等于零，从而验证了其协调性。

### 动力学：平衡方程与边界条件

分析固体力学问题不仅需要运动学描述，还需要满足动力学法则。在没有体力（如重力）的静态情况下，**线性动量守恒**要求应力场在区域内的每一点都满足平衡方程。在极坐标系中，这两个平衡方程为：
- **径向平衡**:
$$
\frac{\partial \sigma_{rr}}{\partial r} + \frac{1}{r}\frac{\partial \sigma_{r\theta}}{\partial \theta} + \frac{\sigma_{rr} - \sigma_{\theta\theta}}{r} = 0
$$
- **切向平衡**:
$$
\frac{\partial \sigma_{r\theta}}{\partial r} + \frac{1}{r}\frac{\partial \sigma_{\theta\theta}}{\partial \theta} + \frac{2\sigma_{r\theta}}{r} = 0
$$
此外，**角动量守恒**对于非极性连续介质（即不考虑内禀体偶矩），要求柯西应力张量是对称的，即 $\sigma_{r\theta} = \sigma_{\theta r}$。

这些方程限制了任何可能的应力状态。例如，考虑一个楔形体尖端附近的渐近应力场，其形式可以假设为变量分离的形式 [@problem_id:2871683]。若假设应力分量为 $\sigma_{ij} \sim r^{\alpha} f(\theta)$，将此形式代入平衡方程，将得到关于系数和指数 $\alpha$ 的代数约束关系。这表明，只有特定形式的应力分布才能满足物理上的平衡要求。

对于一个完整的边值问题，除了内部的平衡方程，还必须在物体的边界上施加**边界条件**。正确地将物理边界条件转化为数学表达式是求解问题的关键一步。边界条件通常分为两种：
1.  **位移边界条件 (Dirichlet 型)**：在边界的某些部分，位移是预先指定的。
2.  **应力边界条件 (Neumann 型)**：在边界的另一些部分，作用于边界上的面力（traction）是预先指定的。

面力矢量 $\mathbf{t}$ 与应力张量 $\boldsymbol{\sigma}$ 通过**柯西公式**相关联：$\mathbf{t} = \boldsymbol{\sigma} \cdot \mathbf{n}$，其中 $\mathbf{n}$ 是边界处指向域外的单位法向量。

让我们通过一个具体的例子来阐明如何设定边界条件 [@problem_id:2676743]。考虑一个位于 $a \le r \le b, 0 \le \theta \le \beta$ 的环扇形区域。

- **内边界 $r=a$**: 受到均匀流体压力 $p_0$ 的作用。
    - 此时，指向固体区域外的法向量是 $\mathbf{n} = -\mathbf{e}_r$。
    - 压力作用是压性的，因此施加的面力为 $\mathbf{t} = -p_0 \mathbf{n} = -p_0(-\mathbf{e}_r) = p_0 \mathbf{e}_r$。
    - 应用柯西公式 $\mathbf{t} = (\sigma_{rr} n_r + \sigma_{r\theta} n_\theta) \mathbf{e}_r + (\sigma_{\theta r} n_r + \sigma_{\theta\theta} n_\theta) \mathbf{e}_\theta$，代入 $n_r=-1, n_\theta=0$，得到 $\mathbf{t} = -\sigma_{rr}\mathbf{e}_r - \sigma_{r\theta}\mathbf{e}_\theta$。
    - 比较两式，得到应力边界条件：$\sigma_{rr}(a, \theta) = -p_0$ 和 $\sigma_{r\theta}(a, \theta) = 0$。后者反映了理想流体不能施加剪切力。

- **外边界 $r=b$**: 与光滑刚性支座接触。
    - 这是**混合边界条件**。
    - “刚性不可穿透”意味着径向位移为零，即 $u_r(b, \theta) = 0$（位移边界条件）。
    - “光滑接触”意味着没有摩擦力，即切向面力为零。此时法向量为 $\mathbf{n} = \mathbf{e}_r$，切向面力 $t_\theta = \sigma_{r\theta} n_r + \sigma_{\theta\theta} n_\theta = \sigma_{r\theta}(1) + \sigma_{\theta\theta}(0) = \sigma_{r\theta}$。因此条件为 $\sigma_{r\theta}(b, \theta) = 0$（应力边界条件）。
    - 注意，径向应力 $\sigma_{rr}(b, \theta)$ 是未知的接触反力，不能预先指定。

- **径向边界 $\theta=0$ 和 $\theta=\beta$**: 自由边界（traction-free）。
    - 在 $\theta=\beta$ 处，外法线为 $\mathbf{n} = \mathbf{e}_\theta$；在 $\theta=0$ 处，外法线为 $\mathbf{n} = -\mathbf{e}_\theta$。
    - 对于 $\mathbf{n} = \mathbf{e}_\theta$，$n_r=0, n_\theta=1$，面力为 $\mathbf{t} = \sigma_{r\theta}\mathbf{e}_r + \sigma_{\theta\theta}\mathbf{e}_\theta$。
    - 自由边界意味着 $\mathbf{t} = \mathbf{0}$，因此两个分量都必须为零：$\sigma_{r\theta}(r, \beta)=0$ 和 $\sigma_{\theta\theta}(r, \beta)=0$。
    - 类似地，在 $\theta=0$ 处也得到 $\sigma_{r\theta}(r, 0)=0$ 和 $\sigma_{\theta\theta}(r, 0)=0$。

这个例子全面展示了如何根据物理描述（压力、接触、自由表面）和几何情况（法向量方向）严谨地写出数学上精确的边界条件。

### Airy 应力函数：二维弹性问题的统一解法

对于二维弹性力学问题（平面应力或平面应变），**Airy 应力函数** $\Phi(r, \theta)$ 提供了一种极为优雅和强大的求解策略。其核心思想是引入一个标量势函数 $\Phi$，使得应力分量可以通过对 $\Phi$ 求导得到，从而自动满足平衡方程。

在极坐标中，应力分量由 Airy 函数定义如下 [@problem_id:2889543]：
$$
\sigma_{rr} = \frac{1}{r}\frac{\partial \Phi}{\partial r} + \frac{1}{r^2}\frac{\partial^2 \Phi}{\partial \theta^2}
$$
$$
\sigma_{\theta\theta} = \frac{\partial^2 \Phi}{\partial r^2}
$$
$$
\sigma_{r\theta} = -\frac{\partial}{\partial r}\left(\frac{1}{r}\frac{\partial \Phi}{\partial \theta}\right) = \frac{1}{r^2}\frac{\partial \Phi}{\partial \theta} - \frac{1}{r}\frac{\partial^2 \Phi}{\partial r \partial \theta}
$$
可以验证，只要 $\Phi$ 具有足够的光滑性，将这些表达式代入上一节的两个平衡方程，方程将恒等于零。这样，平衡方程的求解问题就被巧妙地绕过了。

然而，一个合法的弹性解不仅要满足平衡，还必须对应一个连续的位移场，即应变场必须是协调的。在没有体力的情况下，对于均匀各向同性线弹性材料，应变协调条件可以等价地表示为关于应力和的 **Beltrami-Michell 方程**：$\nabla^2(\sigma_{rr} + \sigma_{\theta\theta}) = 0$。

使用 Airy 函数的定义，我们计算正应力和：
$$
\sigma_{rr} + \sigma_{\theta\theta} = \left(\frac{1}{r}\frac{\partial \Phi}{\partial r} + \frac{1}{r^2}\frac{\partial^2 \Phi}{\partial \theta^2}\right) + \frac{\partial^2 \Phi}{\partial r^2} = \nabla^2 \Phi
$$
其中 $\nabla^2$ 是极坐标下的拉普拉斯算子。将此结果代入 Beltrami-Michell 方程，我们得到了 Airy 应力函数必须满足的单一主导偏微分方程：
$$
\nabla^2(\nabla^2 \Phi) = \nabla^4 \Phi = 0
$$
这个方程被称为**双和谐方程** (biharmonic equation)。因此，求解二维弹性问题就转化为了寻找一个满足双和谐方程和边界条件的 Airy 应力函数 $\Phi$ 的问题。

在极坐标下，双和谐方程可以写作紧凑的算子形式 [@problem_id:2920462]：
$$
\left(\frac{\partial^{2}}{\partial r^{2}}+\frac{1}{r}\frac{\partial}{\partial r}+\frac{1}{r^{2}}\frac{\partial^{2}}{\partial \theta^{2}}\right) \left(\frac{\partial^{2}\Phi}{\partial r^{2}}+\frac{1}{r}\frac{\partial \Phi}{\partial r}+\frac{1}{r^{2}}\frac{\partial^{2}\Phi}{\partial \theta^{2}}\right) = 0
$$
将其完全展开，则得到一个更为复杂的表达式：
$$
\frac{\partial^{4}\Phi}{\partial r^{4}}+\frac{2}{r}\frac{\partial^{3}\Phi}{\partial r^{3}}-\frac{1}{r^{2}}\frac{\partial^{2}\Phi}{\partial r^{2}}+\frac{1}{r^{3}}\frac{\partial \Phi}{\partial r} +\frac{2}{r^{2}}\frac{\partial^{4}\Phi}{\partial r^{2}\partial \theta^{2}} -\frac{2}{r^{3}}\frac{\partial^{3}\Phi}{\partial r\,\partial \theta^{2}} +\frac{1}{r^{4}}\frac{\partial^{4}\Phi}{\partial \theta^{4}} +\frac{4}{r^{4}}\frac{\partial^{2}\Phi}{\partial \theta^{2}} = 0
$$

双和谐方程的通解（称为 Michell 解）是一系列形如 $r^n f(\theta)$ 的项的线性组合。选择哪些项来构造解，取决于问题的具体几何域和边界条件。例如 [@problem_id:2889543]：
-  $\Phi = A r^2$ ($A$ 为常数) 是一个有效的双和谐函数。它产生的应力场为 $\sigma_{rr} = 2A$, $\sigma_{\theta\theta} = 2A$, $\sigma_{r\theta} = 0$。这是一个**均匀的静水压力（或拉力）状态**，常用于模拟远场的双轴载荷。
-  $\Phi = C r^{-2} \cos(2\theta)$ ($C$ 为常数) 也是双和谐的。然而，它产生的应力场（如 $\sigma_{rr} = -6Cr^{-4}\cos(2\theta)$）在原点 $r=0$ 处是奇异的（趋于无穷）。因此，对于包含原点的实体区域（如实心圆盘），该项必须被舍弃（即令 $C=0$），因为它不符合物理实际。但是，对于不包含原点的区域，如环形区域或带孔的无限大平板 ($r>a>0$)，这一项是**完全合法且至关重要的**。它恰恰是用来描述孔边应力集中的关键部分。

最后，我们通过一个实例来展示如何利用 Airy 函数求解一个具体的边值问题 [@problem_id:2676747]。考虑一个半径为 $R$ 的实心圆盘，其边界 $r=R$ 上作用着特定的面力 $t_r = -T_0 \cos(n\theta)$ 和 $t_\theta = T_0 \sin(n\theta)$ ($n \ge 2$)。我们尝试用一个单项的 Airy 函数 $\Phi = A r^n \cos(n\theta)$ 来求解。

首先，计算该 $\Phi$ 对应的应力分量：
$$
\sigma_{rr} = A n (1-n) r^{n-2} \cos(n\theta)
$$
$$
\sigma_{r\theta} = A n (n-1) r^{n-2} \sin(n\theta)
$$
在边界 $r=R$ 上，面力分量为 $t_r = \sigma_{rr}|_{r=R}$ 和 $t_\theta = \sigma_{r\theta}|_{r=R}$。将计算出的应力与给定的边界条件进行匹配：
$$
A n (1-n) R^{n-2} \cos(n\theta) = -T_0 \cos(n\theta) \quad \implies \quad A n (1-n) R^{n-2} = -T_0
$$
$$
A n (n-1) R^{n-2} \sin(n\theta) = T_0 \sin(n\theta) \quad \implies \quad A n (n-1) R^{n-2} = T_0
$$
两个方程给出了一致的结果。从第二个方程解得系数 $A$：
$$
A = \frac{T_0}{n(n-1)R^{n-2}}
$$
这个过程完美地展示了 Airy 应力函数法的威力：通过选择合适形式的函数，并将待定系数与边界条件联系起来，我们可以系统地求解复杂的弹性力学问题。