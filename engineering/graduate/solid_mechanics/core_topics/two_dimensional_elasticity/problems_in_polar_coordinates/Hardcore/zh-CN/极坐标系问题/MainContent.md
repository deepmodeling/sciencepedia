## 引言
在固体力学分析中，选择合适的[坐标系](@entry_id:156346)是简化问题、高效求解的关键。对于大量涉及圆形边界、孔洞、或轴对称载荷的工程与物理问题——从高压容器到晶体中的缺陷——笛卡尔坐标系显得力不从心。极[坐标系](@entry_id:156346)为此类问题提供了更为自然和强大的描述框架。然而，从固定的笛卡尔[基矢](@entry_id:199546)量到随空间位置变化的极[坐标基](@entry_id:270149)矢量的转变，也为运动学和[动力学方程](@entry_id:751029)的推导带来了新的复杂性，构成了学习过程中的一个关键知识壁垒。

本文旨在系统性地攻克这一壁垒，为读者提供一个关于极坐标下[固体力学](@entry_id:164042)问题的完整知识体系。我们将分三步深入探讨这一主题。首先，在“原理与机制”一章中，我们将从[坐标系](@entry_id:156346)的几何基础出发，严谨推导[应变-位移关系](@entry_id:173321)、[平衡方程](@entry_id:172166)，并重点介绍求解二维弹性问题的强大工具——[Airy应力函数](@entry_id:191331)法。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示这些理论如何应用于解决经典的工程挑战，如[厚壁圆筒](@entry_id:189222)、旋转圆盘和应力集中问题，并揭示其在[断裂力学](@entry_id:141480)、[材料科学](@entry_id:152226)乃至[量子化学](@entry_id:140193)等前沿领域的深刻联系。最后，“动手实践”部分将提供一系列精心设计的问题，引导您将理论知识转化为解决实际问题的能力。

通过这一系列的学习，您将不仅掌握在极坐标下进行弹性力学分析的核心技术，更能深刻理解其在现代科学与工程中的广泛应用价值。

## 原理与机制

在连续介质力学中，问题的几何形状往往决定了最有效的分析[坐标系](@entry_id:156346)。对于具有圆形或[轴对称](@entry_id:173333)边界（例如孔洞、圆盘、圆柱体和楔形体）的问题，极[坐标系](@entry_id:156346) $(r, \theta)$ 提供了一种比笛卡尔坐标系更为自然和简洁的描述方式。本章旨在系统地阐述在极[坐标系](@entry_id:156346)下进行固体力学分析所需的基本原理和关键机制。我们将从[坐标系](@entry_id:156346)的几何基础出发，逐步建立[运动学方程](@entry_id:173032)、[动力学平衡](@entry_id:187220)方程，并最终探讨一种强大的求解二维弹性问题的系统方法——Airy 应力函数法。

### 极[坐标系](@entry_id:156346)的几何基础与正交性

极[坐标系](@entry_id:156346)由径向距离 $r$ 和从参考轴逆时针测量的角度 $\theta$ 定义。与[笛卡尔坐标](@entry_id:167698) $(x, y)$ 的转换关系为 $x = r \cos\theta$ 和 $y = r \sin\theta$。在极[坐标系](@entry_id:156346)中，任意点的[基矢](@entry_id:199546)量，即径向单位矢量 $\mathbf{e}_r$ 和切向单位矢量 $\mathbf{e}_\theta$，其方向随着点的移动而改变。这与笛卡尔坐标系中固定不变的[基矢](@entry_id:199546)量 $(\mathbf{e}_x, \mathbf{e}_y)$ 形成了鲜明对比，也正是这种[空间变异性](@entry_id:755146)导致了极[坐标系](@entry_id:156346)下控制方程形式的复杂性。

一个[坐标系](@entry_id:156346)的局部几何特性可以通过其**度量张量** $\mathbf{g}$ 来描述。度量张量定义了在坐标空间中测量距离、角度和体积的方式。在任意[曲线坐标系](@entry_id:172561) $(u^1, u^2)$ 中，无穷小距离的平方 $ds^2$ 由下式给出：
$$
ds^2 = \sum_{\mu, \nu=1}^{2} g_{\mu\nu} du^\mu du^\nu
$$
其中 $g_{\mu\nu}$ 是度量张量的分量。对于从[笛卡尔坐标](@entry_id:167698) $(x^1, x^2) = (x, y)$ 到极坐标 $(u^1, u^2) = (r, \theta)$ 的变换，度量张量分量可以通过以下变换法则计算：
$$
g_{\mu\nu} = \sum_{i=1}^{2} \frac{\partial x^i}{\partial u^\mu} \frac{\partial x^i}{\partial u^\nu}
$$
通过计算各个偏导数，我们可以得到极[坐标系](@entry_id:156346)下的度量张量 。
$$
\frac{\partial x}{\partial r} = \cos\theta, \quad \frac{\partial y}{\partial r} = \sin\theta
$$
$$
\frac{\partial x}{\partial \theta} = -r\sin\theta, \quad \frac{\partial y}{\partial \theta} = r\cos\theta
$$
由此，我们可以计算[出度](@entry_id:263181)量张量的各个分量：
$$
g_{rr} = \left(\frac{\partial x}{\partial r}\right)^2 + \left(\frac{\partial y}{\partial r}\right)^2 = \cos^2\theta + \sin^2\theta = 1
$$
$$
g_{\theta\theta} = \left(\frac{\partial x}{\partial \theta}\right)^2 + \left(\frac{\partial y}{\partial \theta}\right)^2 = (-r\sin\theta)^2 + (r\cos\theta)^2 = r^2(\sin^2\theta + \cos^2\theta) = r^2
$$
$$
g_{r\theta} = g_{\theta r} = \frac{\partial x}{\partial r}\frac{\partial x}{\partial \theta} + \frac{\partial y}{\partial r}\frac{\partial y}{\partial \theta} = (\cos\theta)(-r\sin\theta) + (\sin\theta)(r\cos\theta) = 0
$$
因此，极[坐标系](@entry_id:156346)下的度量张量矩阵为：
$$
\mathbf{g} = \begin{pmatrix} g_{rr} & g_{r\theta} \\ g_{\theta r} & g_{\theta\theta} \end{pmatrix} = \begin{pmatrix} 1 & 0 \\ 0 & r^2 \end{pmatrix}
$$
度量张量的非对角分量 $g_{r\theta}$ 和 $g_{\theta r}$ 为零，这一结果具有深刻的几何意义：它表明极[坐标系](@entry_id:156346)是**[正交坐标](@entry_id:166074)系**。这意味着在任何一点，径向[基矢](@entry_id:199546)量 $\mathbf{e}_r$ 和切向[基矢](@entry_id:199546)量 $\mathbf{e}_\theta$ 总是相互垂直的。这种正交性极大地简化了矢量和张量在分解和计算时的复杂性。无穷小线元长度的表达式也因此简化为 $ds^2 = dr^2 + r^2 d\theta^2$，直观地反映了勾股定理在无穷小尺度上的应用。

### 运动学：极[坐标系](@entry_id:156346)下的应变与转动

在连续介质力学中，物体的运动由[位移场](@entry_id:141476) $\mathbf{u}$ 描述。在极坐标中，[位移矢量](@entry_id:262782)可以分解为径向分量 $u_r$ 和切向分量 $u_\theta$：$\mathbf{u} = u_r \mathbf{e}_r + u_\theta \mathbf{e}_\theta$。变形由[应变张量](@entry_id:193332) $\boldsymbol{\varepsilon}$ 描述，它是[位移梯度](@entry_id:165352)的对称部分。由于[基矢](@entry_id:199546)量 $\mathbf{e}_r$ 和 $\mathbf{e}_\theta$ 的方向随位置变化，[应变-位移关系](@entry_id:173321)式中会出现额外的项，这些项正是为了解释[基矢](@entry_id:199546)量的旋转效应。

在小变形假设下，极[坐标系](@entry_id:156346)中的应变分量由下式给出：
- **径向[正应变](@entry_id:204633)** ($\varepsilon_{rr}$): 描述径向纤维的伸长。
$$
\varepsilon_{rr} = \frac{\partial u_r}{\partial r}
$$
- **环向[正应变](@entry_id:204633)** ($\varepsilon_{\theta\theta}$): 描述圆周纤维的伸长，也称为“环状应变”。它不仅与 $u_\theta$ 的周向变化有关，还与径向位移本身有关，因为一个纯粹的径向膨胀会拉伸所有周向纤维。
$$
\varepsilon_{\theta\theta} = \frac{1}{r}\frac{\partial u_\theta}{\partial \theta} + \frac{u_r}{r}
$$
- **[剪应变](@entry_id:175241)** ($\varepsilon_{r\theta}$): 描述径向[线元](@entry_id:196833)与环向[线元](@entry_id:196833)之间夹角的变化。
$$
\varepsilon_{r\theta} = \frac{1}{2} \left( \frac{1}{r}\frac{\partial u_r}{\partial \theta} + \frac{\partial u_\theta}{\partial r} - \frac{u_\theta}{r} \right)
$$
同时，[位移梯度](@entry_id:165352)的反对称部分描述了物质微元的**[刚体转动](@entry_id:191086)**。在二维平面问题中，该转动可以用一个标量场 $\omega$ 表示，其定义为：
$$
\omega = \frac{1}{2} \left( \frac{1}{r}\frac{\partial (r u_\theta)}{\partial r} - \frac{1}{r}\frac{\partial u_r}{\partial \theta} \right) = \frac{1}{2} \left( \frac{\partial u_\theta}{\partial r} + \frac{u_\theta}{r} - \frac{1}{r}\frac{\partial u_r}{\partial \theta} \right)
$$

为了更深刻地理解这些公式，我们可以分析一个具体的[位移场](@entry_id:141476) 。考虑一个由 $u_r = \alpha r$ 和 $u_\theta = \beta r$ 定义的[位移场](@entry_id:141476)，其中 $\alpha$ 和 $\beta$ 为常数。

首先，我们计算应变分量：
- $\varepsilon_{rr} = \frac{\partial}{\partial r}(\alpha r) = \alpha$
- $\varepsilon_{\theta\theta} = \frac{1}{r}\frac{\partial}{\partial \theta}(\beta r) + \frac{\alpha r}{r} = 0 + \alpha = \alpha$
- $\varepsilon_{r\theta} = \frac{1}{2} \left( \frac{1}{r}\frac{\partial}{\partial \theta}(\alpha r) + \frac{\partial}{\partial r}(\beta r) - \frac{\beta r}{r} \right) = \frac{1}{2} (0 + \beta - \beta) = 0$
这个结果表明，该位移场对应一个**均匀膨胀**或收缩状态，其中径向和环向的伸长率处处相等 ($\varepsilon_{rr} = \varepsilon_{\theta\theta} = \alpha$)，且没有剪切变形 ($\varepsilon_{r\theta} = 0$)。这种变形被称为**均匀展缩** (uniform dilatation)。

接着，我们分析其[刚体转动](@entry_id:191086)：
- $\omega = \frac{1}{2} \left( \frac{\partial}{\partial r}(\beta r) + \frac{\beta r}{r} - \frac{1}{r}\frac{\partial}{\partial \theta}(\alpha r) \right) = \frac{1}{2}(\beta + \beta - 0) = \beta$
转动场 $\omega$ 是一个常数 $\beta$，这意味着整个物体经历了一个**均匀的[刚体转动](@entry_id:191086)**。

因此，[位移场](@entry_id:141476) $\mathbf{u} = (\alpha r) \mathbf{e}_r + (\beta r) \mathbf{e}_\theta$ 描述了一个均匀展缩（变形）和一个均匀[刚体转动](@entry_id:191086)（非变形运动）的叠加。这个例子清晰地揭示了运动是如何分解为变形和刚体运动的，并且突出了仅从位移场本身的形式（例如，$u_\theta$ 与 $r$ 呈线性关系）并不能直接判断是否存在剪切或转动，必须通过完整的运动学关系进行计算。值得注意的是，任何从一个连续、单值的[位移场](@entry_id:141476)派生出来的应变场，必然自动满足**[圣维南协调条件](@entry_id:173493)**。对于本例，将 $\varepsilon_{rr}=\alpha, \varepsilon_{\theta\theta}=\alpha, \varepsilon_{r\theta}=0$ 代入极坐标下的协调方程，会发现方程恒等于零，从而验证了其协调性。

### 动力学：[平衡方程](@entry_id:172166)与边界条件

分析[固体力学](@entry_id:164042)问题不仅需要运动学描述，还需要满足动力学法则。在没有[体力](@entry_id:174230)（如重力）的静态情况下，**[线性动量守恒](@entry_id:165717)**要求应[力场](@entry_id:147325)在区域内的每一点都满足[平衡方程](@entry_id:172166)。在极[坐标系](@entry_id:156346)中，这两个平衡方程为：
- **径向平衡**:
$$
\frac{\partial \sigma_{rr}}{\partial r} + \frac{1}{r}\frac{\partial \sigma_{r\theta}}{\partial \theta} + \frac{\sigma_{rr} - \sigma_{\theta\theta}}{r} = 0
$$
- **切向平衡**:
$$
\frac{\partial \sigma_{r\theta}}{\partial r} + \frac{1}{r}\frac{\partial \sigma_{\theta\theta}}{\partial \theta} + \frac{2\sigma_{r\theta}}{r} = 0
$$
此外，**[角动量守恒](@entry_id:156798)**对于非极性连续介质（即不考虑内禀体偶矩），要求柯西应力张量是对称的，即 $\sigma_{r\theta} = \sigma_{\theta r}$。

这些方程限制了任何可能的应力状态。例如，考虑一个楔形体尖端附近的渐近应[力场](@entry_id:147325)，其形式可以假设为变量分离的形式 。若假设应力分量为 $\sigma_{ij} \sim r^{\alpha} f(\theta)$，将此形式代入[平衡方程](@entry_id:172166)，将得到关于系数和指数 $\alpha$ 的代数约束关系。这表明，只有特定形式的应力[分布](@entry_id:182848)才能满足物理上的平衡要求。

对于一个完整的边值问题，除了内部的平衡方程，还必须在物体的边界上施加**边界条件**。正确地将物理边界条件转化为数学表达式是求解问题的关键一步。边界条件通常分为两种：
1.  **[位移边界条件](@entry_id:203261) (Dirichlet 型)**：在边界的某些部分，位移是预先指定的。
2.  **应力边界条件 (Neumann 型)**：在边界的另一些部分，作用于边界上的面力（traction）是预先指定的。

[面力矢量](@entry_id:189429) $\mathbf{t}$ 与[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 通过**柯西公式**相关联：$\mathbf{t} = \boldsymbol{\sigma} \cdot \mathbf{n}$，其中 $\mathbf{n}$ 是边界处指向域外的[单位法向量](@entry_id:178851)。

让我们通过一个具体的例子来阐明如何设定边界条件 。考虑一个位于 $a \le r \le b, 0 \le \theta \le \beta$ 的环扇形区域。

- **内边界 $r=a$**: 受到均匀流体压力 $p_0$ 的作用。
    - 此时，指向固体区域外的[法向量](@entry_id:264185)是 $\mathbf{n} = -\mathbf{e}_r$。
    - 压力作用是压性的，因此施加的面力为 $\mathbf{t} = -p_0 \mathbf{n} = -p_0(-\mathbf{e}_r) = p_0 \mathbf{e}_r$。
    - 应用柯西公式 $\mathbf{t} = (\sigma_{rr} n_r + \sigma_{r\theta} n_\theta) \mathbf{e}_r + (\sigma_{\theta r} n_r + \sigma_{\theta\theta} n_\theta) \mathbf{e}_\theta$，代入 $n_r=-1, n_\theta=0$，得到 $\mathbf{t} = -\sigma_{rr}\mathbf{e}_r - \sigma_{r\theta}\mathbf{e}_\theta$。
    - 比较两式，得到应力边界条件：$\sigma_{rr}(a, \theta) = -p_0$ 和 $\sigma_{r\theta}(a, \theta) = 0$。后者反映了[理想流体](@entry_id:161909)不能施加剪切力。

- **外边界 $r=b$**: 与光滑刚性支座接触。
    - 这是**[混合边界条件](@entry_id:176456)**。
    - “刚性不可穿透”意味着径向位移为零，即 $u_r(b, \theta) = 0$（[位移边界条件](@entry_id:203261)）。
    - “光滑接触”意味着没有[摩擦力](@entry_id:171772)，即切向面力为零。此时法向量为 $\mathbf{n} = \mathbf{e}_r$，切向面力 $t_\theta = \sigma_{r\theta} n_r + \sigma_{\theta\theta} n_\theta = \sigma_{r\theta}(1) + \sigma_{\theta\theta}(0) = \sigma_{r\theta}$。因此条件为 $\sigma_{r\theta}(b, \theta) = 0$（应力边界条件）。
    - 注意，[径向应力](@entry_id:197086) $\sigma_{rr}(b, \theta)$ 是未知的接触反力，不能预先指定。

- **径向边界 $\theta=0$ 和 $\theta=\beta$**: 自由边界（traction-free）。
    - 在 $\theta=\beta$ 处，外[法线](@entry_id:167651)为 $\mathbf{n} = \mathbf{e}_\theta$；在 $\theta=0$ 处，外法线为 $\mathbf{n} = -\mathbf{e}_\theta$。
    - 对于 $\mathbf{n} = \mathbf{e}_\theta$，$n_r=0, n_\theta=1$，面力为 $\mathbf{t} = \sigma_{r\theta}\mathbf{e}_r + \sigma_{\theta\theta}\mathbf{e}_\theta$。
    - 自由边界意味着 $\mathbf{t} = \mathbf{0}$，因此两个分量都必须为零：$\sigma_{r\theta}(r, \beta)=0$ 和 $\sigma_{\theta\theta}(r, \beta)=0$。
    - 类似地，在 $\theta=0$ 处也得到 $\sigma_{r\theta}(r, 0)=0$ 和 $\sigma_{\theta\theta}(r, 0)=0$。

这个例子全面展示了如何根据物理描述（压力、接触、自由表面）和几何情况（法向量方向）严谨地写出数学上精确的边界条件。

### Airy 应力函数：二维弹性问题的统一解法

对于二维弹性力学问题（平面应力或[平面应变](@entry_id:167046)），**Airy 应力函数** $\Phi(r, \theta)$ 提供了一种极为优雅和强大的求解策略。其核心思想是引入一个[标量势](@entry_id:276177)函数 $\Phi$，使得应力分量可以通过对 $\Phi$ 求导得到，从而自动满足[平衡方程](@entry_id:172166)。

在极坐标中，应力分量由 Airy 函数定义如下 ：
$$
\sigma_{rr} = \frac{1}{r}\frac{\partial \Phi}{\partial r} + \frac{1}{r^2}\frac{\partial^2 \Phi}{\partial \theta^2}
$$
$$
\sigma_{\theta\theta} = \frac{\partial^2 \Phi}{\partial r^2}
$$
$$
\sigma_{r\theta} = -\frac{\partial}{\partial r}\left(\frac{1}{r}\frac{\partial \Phi}{\partial \theta}\right) = \frac{1}{r^2}\frac{\partial \Phi}{\partial \theta} - \frac{1}{r}\frac{\partial^2 \Phi}{\partial r \partial \theta}
$$
可以验证，只要 $\Phi$ 具有足够的[光滑性](@entry_id:634843)，将这些表达式代入上一节的两个[平衡方程](@entry_id:172166)，方程将恒等于零。这样，平衡方程的求解问题就被巧妙地绕过了。

然而，一个合法的弹性解不仅要满足平衡，还必须对应一个连续的位移场，即应变场必须是协调的。在没有[体力](@entry_id:174230)的情况下，对于均匀[各向同性线弹性](@entry_id:185899)材料，应变协调条件可以等价地表示为关于应力和的 **Beltrami-Michell 方程**：$\nabla^2(\sigma_{rr} + \sigma_{\theta\theta}) = 0$。

使用 Airy 函数的定义，我们计算[正应力](@entry_id:260622)和：
$$
\sigma_{rr} + \sigma_{\theta\theta} = \left(\frac{1}{r}\frac{\partial \Phi}{\partial r} + \frac{1}{r^2}\frac{\partial^2 \Phi}{\partial \theta^2}\right) + \frac{\partial^2 \Phi}{\partial r^2} = \nabla^2 \Phi
$$
其中 $\nabla^2$ 是极坐标下的[拉普拉斯算子](@entry_id:146319)。将此结果代入 Beltrami-Michell 方程，我们得到了 Airy 应力函数必须满足的单一主导[偏微分方程](@entry_id:141332)：
$$
\nabla^2(\nabla^2 \Phi) = \nabla^4 \Phi = 0
$$
这个方程被称为**双和谐方程** (biharmonic equation)。因此，求解二维弹性问题就转化为了寻找一个满足双和谐方程和边界条件的 Airy 应力函数 $\Phi$ 的问题。

在极坐标下，双和谐方程可以写作紧凑的算子形式 ：
$$
\left(\frac{\partial^{2}}{\partial r^{2}}+\frac{1}{r}\frac{\partial}{\partial r}+\frac{1}{r^{2}}\frac{\partial^{2}}{\partial \theta^{2}}\right) \left(\frac{\partial^{2}\Phi}{\partial r^{2}}+\frac{1}{r}\frac{\partial \Phi}{\partial r}+\frac{1}{r^{2}}\frac{\partial^{2}\Phi}{\partial \theta^{2}}\right) = 0
$$
将其完全展开，则得到一个更为复杂的表达式：
$$
\frac{\partial^{4}\Phi}{\partial r^{4}}+\frac{2}{r}\frac{\partial^{3}\Phi}{\partial r^{3}}-\frac{1}{r^{2}}\frac{\partial^{2}\Phi}{\partial r^{2}}+\frac{1}{r^{3}}\frac{\partial \Phi}{\partial r} +\frac{2}{r^{2}}\frac{\partial^{4}\Phi}{\partial r^{2}\partial \theta^{2}} -\frac{2}{r^{3}}\frac{\partial^{3}\Phi}{\partial r\,\partial \theta^{2}} +\frac{1}{r^{4}}\frac{\partial^{4}\Phi}{\partial \theta^{4}} +\frac{4}{r^{4}}\frac{\partial^{2}\Phi}{\partial \theta^{2}} = 0
$$

双和谐方程的通解（称为 Michell 解）是一系列形如 $r^n f(\theta)$ 的项的线性组合。选择哪些项来构造解，取决于问题的具体几何域和边界条件。例如 ：
-  $\Phi = A r^2$ ($A$ 为常数) 是一个有效的双和谐函数。它产生的应[力场](@entry_id:147325)为 $\sigma_{rr} = 2A$, $\sigma_{\theta\theta} = 2A$, $\sigma_{r\theta} = 0$。这是一个**均匀的静水压力（或拉力）状态**，常用于模拟[远场](@entry_id:269288)的双轴载荷。
-  $\Phi = C r^{-2} \cos(2\theta)$ ($C$ 为常数) 也是双和谐的。然而，它产生的应[力场](@entry_id:147325)（如 $\sigma_{rr} = -6Cr^{-4}\cos(2\theta)$）在原点 $r=0$ 处是奇异的（趋于无穷）。因此，对于包含原点的实体区域（如实心圆盘），该项必须被舍弃（即令 $C=0$），因为它不符合物理实际。但是，对于不包含原点的区域，如环形区域或带孔的无限大平板 ($r>a>0$)，这一项是**完全合法且至关重要的**。它恰恰是用来描述孔边[应力集中](@entry_id:160987)的关键部分。

最后，我们通过一个实例来展示如何利用 Airy 函数求解一个具体的边值问题 。考虑一个半径为 $R$ 的实心圆盘，其边界 $r=R$ 上作用着特定的面力 $t_r = -T_0 \cos(n\theta)$ 和 $t_\theta = T_0 \sin(n\theta)$ ($n \ge 2$)。我们尝试用一个单项的 Airy 函数 $\Phi = A r^n \cos(n\theta)$ 来求解。

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