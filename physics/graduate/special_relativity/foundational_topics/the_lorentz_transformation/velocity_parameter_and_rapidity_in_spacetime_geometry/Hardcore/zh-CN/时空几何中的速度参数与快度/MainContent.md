## 引言
在阿尔伯特·爱因斯坦构建的狭义相对论宏伟框架中，洛伦兹变换取代了伽利略变换，成为连接不同[惯性参考系](@keyword=non_rotating_reference_frame|lang=zh-CN|style=Feynman)的时空法则。然而，这一新法则带来的[速度合成](@keyword=composition_of_velocities|lang=zh-CN|style=Feynman)公式却显得[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)且与日常直觉相悖，这暗示着速度本身或许并非描述相对运动最根本的物理量。为了解决这一难题并揭示洛伦兹变换背后更深层的对称性，物理学家引入了一个更为优雅和强大的参数——快度（rapidity）。[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)不仅理顺了[运动学](@keyword=kinematics|lang=zh-CN|style=Feynman)的[代数结构](@keyword=algebraic_structure|lang=zh-CN|style=Feynman)，更将我们对时空的理解从代数运算提升到了几何直觉的层面。

本文旨在系统性地阐释快度这一核心概念。在第一章“原理与机制”中，我们将从类比欧几里得旋转出发，定义快度为时空中的“双曲角”，并展示它如何将复杂的[速度合成](@keyword=composition_of_velocities|lang=zh-CN|style=Feynman)简化为简单的线性相加。接着，在第二章“应用与跨学科联系”中，我们将探索快度在粒子物理、天体物理学、电磁学乃至前沿理论中的广泛应用，见证其解决实际问题的强大威力。最后，通过第三章“动手实践”中的具体问题，读者将有机会亲手运用快度来解决相对论问题，从而深化对理论的理解。本文将引导读者穿越[相对论运动学](@keyword=relativistic_kinematics|lang=zh-CN|style=Feynman)的迷雾，揭示隐藏在速度参数背后的简洁而深刻的时空几何。

## 原理与机制

在狭义相对论中，从一个惯性参考系到另一个惯性参考系的[坐标变换](@keyword=coordinate_transformations|lang=zh-CN|style=Feynman)由[洛伦兹变换](@keyword=the_lorentz_transformation|lang=zh-CN|style=Feynman)描述。虽然这些变换在代数上是线性的，但它们的一些物理后果，特别是速度的合成，却显得[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)且有悖常理。为了揭示[洛伦兹变换](@keyword=the_lorentz_transformation|lang=zh-CN|style=Feynman)背后更深层次的几何与[代数结构](@keyword=algebraic_structure|lang=zh-CN|style=Feynman)，物理学家引入了一个比速度更基本的[运动学](@keyword=kinematics|lang=zh-CN|style=Feynman)参数：**[快度](@keyword=rapidity|lang=zh-CN|style=Feynman) (rapidity)**。本章将系统地阐述快度的原理及其在[时空几何](@keyword=spacetime_geometry|lang=zh-CN|style=Feynman)与动力学中的应用。我们将看到，[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)不仅简化了[速度合成](@keyword=composition_of_velocities|lang=zh-CN|style=Feynman)的计算，更将[洛伦兹变换](@keyword=the_lorentz_transformation|lang=zh-CN|style=Feynman)诠释为时空中的一种旋转——[双曲旋转](@keyword=hyperbolic_rotations|lang=zh-CN|style=Feynman)，从而为我们理解[相对论运动学](@keyword=relativistic_kinematics|lang=zh-CN|style=Feynman)提供了更为深刻的视角。

### 快度：时空的双曲角

我们从一个熟悉的类比开始：二维欧几里得空间中的旋转。一个绕原点的[旋转变换](@keyword=rotational_transform|lang=zh-CN|style=Feynman)保持了点到原点的距离 $r^2 = x^2 + y^2$ 不变。这个变换是线性的，可以用一个[旋转矩阵](@keyword=rotation_matrix|lang=zh-CN|style=Feynman)来表示：
$$
\begin{pmatrix} x' \\ y' \end{pmatrix} = \begin{pmatrix} \cos\theta  -\sin\theta \\ \sin\theta  \cos\theta \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix}
$$
这里的参数 $\theta$ 是旋转角。角度的一个关键特性是其可加性：连续两次旋转的角度等于两次旋转角度之和，即 $\theta_{total} = \theta_1 + \theta_2$。

现在，我们转向 (1+1) 维闵可夫斯基时空。一个沿 $x$ 轴的洛伦兹变换（或称“助推”，boost）保持了时空间隔 $s^2 = (ct)^2 - x^2$ 不变。这个变换同样是线性的，其标准形式由速度参数 $\beta = v/c$ 和洛伦兹因子 $\gamma = (1-\beta^2)^{-1/2}$ 给出：
$$
\begin{pmatrix} ct' \\ x' \end{pmatrix} = \begin{pmatrix} \gamma  -\gamma\beta \\ -\gamma\beta  \gamma \end{pmatrix} \begin{pmatrix} ct \\ x \end{pmatrix}
$$
观察这个矩阵与旋转矩阵的相似性，一个自然的问题是：是否存在一个类似于旋转角 $\theta$ 的参数，使得洛伦兹变换可以被更简洁地描述，并且这个参数也具有某种可加性？

答案是肯定的。这个参数就是[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)，通常用 $\phi$ 表示。我们可以利用[双曲函数](@keyword=hyperbolic_functions|lang=zh-CN|style=Feynman) $\cosh\phi$ 和 $\sinh\phi$ 来[参数化](@keyword=parametrization|lang=zh-CN|style=Feynman)[洛伦兹变换](@keyword=the_lorentz_transformation|lang=zh-CN|style=Feynman)矩阵，因为它们满足恒等式 $\cosh^2\phi - \sinh^2\phi = 1$，这恰好能保证[时空间隔](@keyword=spacetime_interval|lang=zh-CN|style=Feynman)的[不变性](@keyword=invariance|lang=zh-CN|style=Feynman)。我们将洛伦兹变换矩阵写成一种“[双曲旋转](@keyword=hyperbolic_rotations|lang=zh-CN|style=Feynman)”的形式 [@problem_id:1868498]：
$$
\begin{pmatrix} ct' \\ x' \end{pmatrix} = \begin{pmatrix} \cosh\phi  -\sinh\phi \\ -\sinh\phi  \cosh\phi \end{pmatrix} \begin{pmatrix} ct \\ x \end{pmatrix}
$$
通过比较这两种矩阵形式的对应元素，我们可以建立速度与快度之间的直接联系：
$$
\gamma = \cosh\phi
$$
$$
\gamma\beta = \sinh\phi
$$
将第二式除以第一式，我们得到：
$$
\beta = \frac{\sinh\phi}{\cosh\phi} = \tanh\phi
$$
因此，快度 $\phi$ 与相对速度 $v$ 之间的基本关系是：
$$
\phi = \operatorname{arctanh}\left(\frac{v}{c}\right)
$$
这个关系式是理解[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)的基石。它表明，[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)是速度的双曲反正切。当速度 $v$ 从 $0$ 增加到 $c$ 时，快度 $\phi$ 从 $0$ 增加到无穷大。这暗示了快度是一个没有上限的参数，与有光速限制的速度形成了鲜明对比。

几何上，快度 $\phi$ 的意义是[时空图](@keyword=spacetime_diagrams|lang=zh-CN|style=Feynman)中的一个**双曲角**。所有与原点具有相同类时或类空时空间隔的事件点，分别构成一条双曲线。例如，对于所有满足 $(ct)^2 - x^2 = R^2$ 的事件，快度 $\phi$ 就是参数化这条双曲线的“角度”，使得事件坐标可以写为 $(ct, x) = (R\cosh\phi, R\sinh\phi)$。

### [快度](@keyword=rapidity|lang=zh-CN|style=Feynman)的代数威力：共线速度的合成

快度最显著的优点在于它极大地简化了[速度合成](@keyword=composition_of_velocities|lang=zh-CN|style=Feynman)法则。我们知道，在伽利略变换中，共线速度是直接相加的。但在[狭义相对论](@keyword=special_relativity_theory|lang=zh-CN|style=Feynman)中，速度的合成遵循更为复杂的爱因斯坦[速度合成](@keyword=composition_of_velocities|lang=zh-CN|style=Feynman)公式。若[参考系](@keyword=frames_of_reference|lang=zh-CN|style=Feynman) $S'$ 相对于 $S$ 以速度 $v_1$ 运动，[参考系](@keyword=frames_of_reference|lang=zh-CN|style=Feynman) $S''$ 相对于 $S'$ 以速度 $v_2$ 运动（均为沿 $x$ 轴），则 $S''$ 相对于 $S$ 的速度 $v_{12}$ 为：
$$
v_{12} = \frac{v_1 + v_2}{1 + \frac{v_1 v_2}{c^2}}
$$
这个公式保证了合成速度永远不会超过光速 $c$，但也使其在代数上显得笨拙。

然而，当我们用快度来描述这个过程时，复杂的[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)合成变成了简单的线性相加。设 $v_1 = c\tanh\phi_1$ 和 $v_2 = c\tanh\phi_2$，那么合成速度 $v_{12} = c\tanh\phi_{12}$ 对应的快度 $\phi_{12}$ 是多少呢？利用[双曲正切](@keyword=hyperbolic_tangent_(tanh)|lang=zh-CN|style=Feynman)的加法公式：
$$
\tanh(\phi_1 + \phi_2) = \frac{\tanh\phi_1 + \tanh\phi_2}{1 + \tanh\phi_1 \tanh\phi_2}
$$
将 $\tanh\phi_1 = v_1/c$ 和 $\tanh\phi_2 = v_2/c$ 代入，我们得到：
$$
\tanh(\phi_1 + \phi_2) = \frac{v_1/c + v_2/c}{1 + (v_1/c)(v_2/c)} = \frac{1}{c} \frac{v_1 + v_2}{1 + v_1 v_2/c^2} = \frac{v_{12}}{c}
$$
这立即得出：
$$
\phi_{12} = \phi_1 + \phi_2
$$
这个优美的结果表明，**对于共线运动，快度是可加的**。这恢复了我们对[速度合成](@keyword=composition_of_velocities|lang=zh-CN|style=Feynman)的直观认识——变换的“量”应该是可以累加的，而快度正是这个正确的“量”。

为了体会其威力，我们来看一个具体的例子 [@problem_id:414891]。假设飞船 A 相对于地球以 $v_1 = \frac{3}{5}c$ 的速度飞行，飞船 B 相对于飞船 A 以 $v_2 = \frac{4}{5}c$ 的速度沿同一方向飞行。求飞船 B 相对于地球的速度 $v_{12}$。

我们首先将速度转换为[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)：
$$
\phi_1 = \operatorname{arctanh}\left(\frac{3}{5}\right) = \frac{1}{2}\ln\left(\frac{1+3/5}{1-3/5}\right) = \frac{1}{2}\ln(4) = \ln(2)
$$
$$
\phi_2 = \operatorname{arctanh}\left(\frac{4}{5}\right) = \frac{1}{2}\ln\left(\frac{1+4/5}{1-4/5}\right) = \frac{1}{2}\ln(9) = \ln(3)
$$
总快度为：
$$
\phi_{12} = \phi_1 + \phi_2 = \ln(2) + \ln(3) = \ln(6)
$$
现在，我们将总[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)转换回速度：
$$
\frac{v_{12}}{c} = \tanh(\phi_{12}) = \tanh(\ln 6) = \frac{e^{2\ln 6} - 1}{e^{2\ln 6} + 1} = \frac{36-1}{36+1} = \frac{35}{37}
$$
因此，合成速度为 $v_{12} = \frac{35}{37}c$。读者可以自行验证，使用传统的[速度合成](@keyword=composition_of_velocities|lang=zh-CN|style=Feynman)公式会得到相同的结果，但计算过程远不如快度法来得直接和优雅。

### 快度与[洛伦兹变换](@keyword=the_lorentz_transformation|lang=zh-CN|style=Feynman)的结构

[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)的可加性根植于[洛伦兹群](@keyword=lorentz_group|lang=zh-CN|style=Feynman)的数学结构中。一个沿 $x$ 轴的[洛伦兹助推](@keyword=lorentz_boosts|lang=zh-CN|style=Feynman)矩阵 $\Lambda(\phi)$ 可以写为：
$$
\Lambda(\phi) = \begin{pmatrix} \cosh\phi  -\sinh\phi  0  0 \\ -\sinh\phi  \cosh\phi  0  0 \\ 0  0  1  0 \\ 0  0  0  1 \end{pmatrix}
$$
两个连续的、沿同一方向的助推 $\Lambda(\phi_1)$ 和 $\Lambda(\phi_2)$ 的复合效应由[矩阵乘法](@keyword=matrix_multiplication|lang=zh-CN|style=Feynman) $\Lambda_{total} = \Lambda(\phi_2)\Lambda(\phi_1)$ 给出。通过直接计算矩阵乘积，并利用[双曲函数](@keyword=hyperbolic_functions|lang=zh-CN|style=Feynman)的和角公式，可以证明：
$$
\Lambda(\phi_2)\Lambda(\phi_1) = \Lambda(\phi_1 + \phi_2)
$$
这再次确认了快度的可加性。从群论的角度看，沿确定方向的[洛伦兹助推](@keyword=lorentz_boosts|lang=zh-CN|style=Feynman)构成一个单参数[阿贝尔群](@keyword=z_module|lang=zh-CN|style=Feynman)，而[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)正是这个群的参数。

这种深刻的结构关系也可以从[洛伦兹群的李代数](@keyword=lie_algebra_of_lorentz_group|lang=zh-CN|style=Feynman)角度来理解。任何一个[洛伦兹助推](@keyword=lorentz_boosts|lang=zh-CN|style=Feynman)都可以通过一个“生成元”矩阵的指数化来生成 [@problem_id:414906]。对于沿 $x$ 轴的助推，其生成元为：
$$
\mathcal{K}_x = \begin{pmatrix} 0  -1  0  0 \\ -1  0  0  0 \\ 0  0  0  0 \\ 0  0  0  0 \end{pmatrix}
$$
洛伦兹变换矩阵可以表示为[矩阵指数](@keyword=matrix_exponential|lang=zh-CN|style=Feynman)：
$$
\Lambda(\phi) = \exp(\phi \mathcal{K}_x) = \sum_{n=0}^{\infty} \frac{\phi^n}{n!} \mathcal{K}_x^n
$$
通过计算 $\mathcal{K}_x$ 的幂次，我们发现 $\mathcal{K}_x^2 = \text{diag}(1,1,0,0)$，$\mathcal{K}_x^3 = \mathcal{K}_x$，等等。将级数按奇偶次幂分开，恰好可以重组为 $\cosh\phi$ 和 $\sinh\phi$ 的级数，从而推导出上面给出的 $\Lambda(\phi)$ 矩阵形式。

这个指数形式清晰地揭示了复合变换的规律：$\Lambda(\phi_1)\Lambda(\phi_2) = \exp(\phi_1 \mathcal{K}_x)\exp(\phi_2 \mathcal{K}_x) = \exp((\phi_1+\phi_2)\mathcal{K}_x) = \Lambda(\phi_1+\phi_2)$。这意味着，一个具有快度 $2\phi$ 的变换矩阵 $\Lambda(2\phi)$ 正是快度为 $\phi$ 的变换矩阵的平方，即 $\Lambda^2(\phi)$。例如，其时间-时间分量为 $(\Lambda(2\phi))^0_{\ 0} = \cosh(2\phi)$。这一性质在分析[粒子加速器](@keyword=particle_accelerators|lang=zh-CN|style=Feynman)等场景中非常有用。例如，如果一个粒子经过两次完全相同的共线加速，最终测量得到总变换矩阵的时间-时间分量为 $(\Lambda^2)^0_{\ 0} = 41/9$，我们就可以立刻断定 $\cosh(2\phi) = 41/9$。利用反双曲余弦的对数表达式 $\operatorname{arccosh}(z) = \ln(z+\sqrt{z^2-1})$，可以解得 $2\phi = \ln(9)$，因此单次加速对应的快度为 $\phi = \ln(3)$ [@problem_id:414944]。

### 快度的几何与物理诠释

除了其代数上的便利性，[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)还提供了对相对论现象的深刻几何与物理洞察。

#### [光锥坐标](@keyword=light_cone_coordinates|lang=zh-CN|style=Feynman)下的伸缩变换

考虑在 (1+1) 维时空中的[光锥坐标](@keyword=light_cone_coordinates|lang=zh-CN|style=Feynman) $(u, v)$，它们定义为：
$$
u = ct - x
$$
$$
v = ct + x
$$
这些坐标代表了沿负向和正向光锥传播的光信号的位置。在这种[坐标系](@keyword=coordinate_system|lang=zh-CN|style=Feynman)下，洛伦兹变换的形式变得异常简单。一个[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)为 $\phi$ 的沿 $x$ 轴的助推，将坐标 $(u, v)$ 变换为 $(u', v')$，其关系为 [@problem_id:414877]：
$$
u' = e^{-\phi} u
$$
$$
v' = e^{\phi} v
$$
(请注意：这里变换因子的符号取决于助推方向和坐标定义，但变换本质总是一个方向压缩、另一个方向拉伸)。
这个结果极为优美。它表明，[洛伦兹助推](@keyword=lorentz_boosts|lang=zh-CN|style=Feynman)在几何上等价于沿着两个[光锥](@keyword=null_cone|lang=zh-CN|style=Feynman)方向的**伸缩变换**。一个方向上的坐标被因子 $e^{\phi}$ 拉伸，而另一个方向则被因子 $e^{-\phi}$ 压缩，其乘积 $u'v' = uv$ 保持不变。这正是时空间隔 $(ct)^2 - x^2$ 在[光锥坐标](@keyword=light_cone_coordinates|lang=zh-CN|style=Feynman)下的表现形式。因子 $e^{\phi} = \sqrt{(1+\beta)/(1-\beta)}$ 也正是[相对论性多普勒效应](@keyword=relativistic_doppler_effect|lang=zh-CN|style=Feynman)中的频率移动因子。

#### 快度与[固有加速度](@keyword=proper_acceleration|lang=zh-CN|style=Feynman)

[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)与动力学之间也存在着深刻的联系。一个粒子的四维速度 $U^\mu = dx^\mu/d\tau$（其中 $\tau$ 是[固有时](@keyword=proper_time|lang=zh-CN|style=Feynman)间）可以方便地用快度[参数化](@keyword=parametrization|lang=zh-CN|style=Feynman)。对于沿 $x$ 轴的运动，有：
$$
U^\mu = (\gamma c, \gamma v, 0, 0) = (c\cosh\phi, c\sinh\phi, 0, 0)
$$
粒子的[四维加速度](@keyword=acceleration_four_vector|lang=zh-CN|style=Feynman)定义为 $A^\mu = dU^\mu/d\tau$。其大小是一个[洛伦兹不变量](@keyword=lorentz_invariants|lang=zh-CN|style=Feynman)，称为**[固有加速度](@keyword=proper_acceleration|lang=zh-CN|style=Feynman)** $a_0$，定义为 $A_\mu A^\mu = -a_0^2$（在 $(+,-,-,-)$ 度规下）。通过对 $U^\mu$ 求导，我们可以找到快度变化率与[固有加速度](@keyword=proper_acceleration|lang=zh-CN|style=Feynman)之间的关系 [@problem_id:414888]：
$$
A^\mu = \frac{dU^\mu}{d\tau} = \left( c\sinh\phi \frac{d\phi}{d\tau}, c\cosh\phi \frac{d\phi}{d\tau}, 0, 0 \right)
$$
计算其模长的平方：
$$
A_\mu A^\mu = (A^0)^2 - (A^1)^2 = \left(c\sinh\phi \frac{d\phi}{d\tau}\right)^2 - \left(c\cosh\phi \frac{d\phi}{d\tau}\right)^2 = c^2(\sinh^2\phi - \cosh^2\phi)\left(\frac{d\phi}{d\tau}\right)^2 = -c^2\left(\frac{d\phi}{d\tau}\right)^2
$$
将其与 $A_\mu A^\mu = -a_0^2$ 相比较，我们得到了一个极为简洁的关系：
$$
\frac{d\phi}{d\tau} = \frac{a_0}{c}
$$
这意味着，**快度对固有时间的变化率等于[固有加速度](@keyword=proper_acceleration|lang=zh-CN|style=Feynman)（除以 c）**。对于一个经历恒定[固有加速度](@keyword=proper_acceleration|lang=zh-CN|style=Feynman) $a_0$ 的观察者（例如在理想火箭中），其[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)将随其自身时钟的流逝而[线性增长](@keyword=linear_growth|lang=zh-CN|style=Feynman)：$\phi(\tau) = (a_0/c)\tau$。这使得[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)成为描述加速运动的最自然的[运动学](@keyword=kinematics|lang=zh-CN|style=Feynman)变量。

#### [快度](@keyword=rapidity|lang=zh-CN|style=Feynman)与[不变量](@keyword=invariant|lang=zh-CN|style=Feynman)

[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)也与各种[洛伦兹不变量](@keyword=lorentz_invariants|lang=zh-CN|style=Feynman)紧密相连。例如，考虑两个粒子 A 和 B，它们的四维速度分别为 $U_A$ 和 $U_B$。它们之间的标积 $U_A \cdot U_B$ 是一个洛伦兹不变量。在粒子 A 的静止系中，$U_A = (c, 0, 0, 0)$，而 $U_B$ 则是粒子 B 在该系中的[四维速度](@keyword=velocity_four_vector|lang=zh-CN|style=Feynman)，其时间分量为 $\gamma_{rel}c$，其中 $\gamma_{rel}$ 是它们的相对洛伦兹因子。因此，$U_A \cdot U_B = c(\gamma_{rel}c) = \gamma_{rel}c^2$。由于该标积是不变的，此式在任何[参考系](@keyword=frames_of_reference|lang=zh-CN|style=Feynman)中都成立。如果我们用相对[快度](@keyword=rapidity|lang=zh-CN|style=Feynman) $\phi_{AB}$ 来表示，即 $\gamma_{rel} = \cosh(\phi_{AB})$，那么：
$$
U_A \cdot U_B = c^2 \cosh(\phi_{AB})
$$
这个关系将两个[四维速度](@keyword=velocity_four_vector|lang=zh-CN|style=Feynman)的几何关系（它们的标积）与它们的[相对运动](@keyword=relative_motion|lang=zh-CN|style=Feynman)状态（相对快度）联系起来。此外，这个标积还可以通过系统的总[不变质量](@keyword=invariant_mass|lang=zh-CN|style=Feynman) $M$ 来表示 [@problem_id:414886]，从而在粒子物理的碰撞问题中建立起运动学和[不变量](@keyword=invariant|lang=zh-CN|style=Feynman)质量之间的桥梁。

最后，快度作为双曲角的几何意义也可以从[时空几何](@keyword=spacetime_geometry|lang=zh-CN|style=Feynman)中直接看出。考虑一条由 $x^2 - (ct)^2 = R^2$ 定义的类空双曲线。这条[双曲线](@keyword=hyperbola|lang=zh-CN|style=Feynman)上的点可以由快度参数化为 $(ct, x) = (R\sinh\phi, R\cosh\phi)$。连接双曲线上分别对应于[快度](@keyword=rapidity|lang=zh-CN|style=Feynman) $\phi_1$ 和 $\phi_2$ 的两个事件 $E_1$ 和 $E_2$ 的弦，其[时空间隔](@keyword=spacetime_interval|lang=zh-CN|style=Feynman)平方 $(\Delta s_{12})^2$ 为 [@problem_id:414884]：
$$
(\Delta s_{12})^2 = (c\Delta t)^2 - (\Delta x)^2 = R^2(\sinh\phi_2 - \sinh\phi_1)^2 - R^2(\cosh\phi_2 - \cosh\phi_1)^2
$$
利用[双曲函数](@keyword=hyperbolic_functions|lang=zh-CN|style=Feynman)恒等式化简后，我们得到：
$$
(\Delta s_{12})^2 = 2R^2[\cosh(\phi_2 - \phi_1) - 1]
$$
这个结果表明，连接双曲线上任意两点的弦的时空间隔，仅仅依赖于这两点对应的快度之差 $\phi_2 - \phi_1$。这完全类似于欧几里得几何中，圆上两点所夹弦长仅由两点所夹圆心角决定。这再次雄辩地证明，[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)是闵可夫斯基时空几何中一个内在的、基本的“角度”度量。

综上所述，[快度](@keyword=rapidity|lang=zh-CN|style=Feynman)不仅仅是一个为简化计算而引入的数学技巧。它揭示了洛伦兹变换的本质是时空中的[双曲旋转](@keyword=hyperbolic_rotations|lang=zh-CN|style=Feynman)，统一了[运动学](@keyword=kinematics|lang=zh-CN|style=Feynman)、动力学和[时空几何](@keyword=spacetime_geometry|lang=zh-CN|style=Feynman)，是深入理解狭义相对论不可或缺的核心概念。