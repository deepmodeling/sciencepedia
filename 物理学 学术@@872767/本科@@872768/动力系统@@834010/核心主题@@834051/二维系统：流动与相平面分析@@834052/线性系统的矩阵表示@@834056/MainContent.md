## 引言
动力系统无处不在，从行星的[轨道](@entry_id:137151)到经济的波动，它们描述了万物随时间演化的规律。然而，这些系统在各自领域中往往以形式各异的[高阶微分方程](@entry_id:171249)或复杂的耦合关系出现，这为统一的分析和控制带来了巨大挑战。我们如何才能洞察这些不同系统背后的共同结构和动态原理呢？

[线性系统的矩阵表示法](@entry_id:154722)，即[状态空间](@entry_id:177074)方法，正是解决这一难题的强大工具。它提供了一种通用语言，能将纷繁复杂的系统转化为简洁、标准的一阶矩阵方程 $\dot{\mathbf{x}} = A\mathbf{x}$。这种转化不仅是数学上的简化，更是一种深刻的洞察，让我们能用线性代数的利器来剖析系统的稳定性、响应和内在联系。

在本文中，您将踏上一段系统性的学习之旅。我们将首先在“原理与机制”一章中，详细阐述如何将各种物理和数学模型构建为矩阵形式，并解读矩阵背后的物理意义。接着，在“应用与跨学科联系”一章，我们将探索该方法如何在机械、控制、生物和经济等多个领域大放异彩。最后，通过“动手实践”环节，您将有机会亲手将理论应用于解决具体问题。让我们从掌握这一表示法的基础开始。

## 原理与机制

在本章中，我们将深入探讨[线性动力系统](@entry_id:150282)的核心——[矩阵表示法](@entry_id:190318)。从上一章的介绍中我们知道，动力系统描述了状态随[时间演化](@entry_id:153943)的规则。然而，许多物理、工程和[生物系统](@entry_id:272986)最初都是以[高阶微分方程](@entry_id:171249)或复杂的耦合关系来描述的。为了进行系统化的分析、预测和控制，我们需要一个统一且强大的数学框架。[状态空间](@entry_id:177074)方法，特别是[线性系统](@entry_id:147850)的[矩阵表示](@entry_id:146025)，正是为此而生。它将看似各不相同的系统，无论是[机械振动](@entry_id:167420)、[种群动态](@entry_id:136352)还是电路响应，都转化为一种[标准形式](@entry_id:153058)：一阶向量[微分方程](@entry_id:264184)。这种转化不仅是数学上的简化，更是一种深刻的洞察，它揭示了系统内在的结构、相互作用和基本动态特性。

本章将系统地阐述如何将各种形式的[线性系统](@entry_id:147850)模型转化为矩阵形式，并进一步探讨如何从[系统矩阵](@entry_id:172230)的结构和性质中解读出系统的行为机制和物理意义。

### [状态空间表示](@entry_id:147149)：一个统一的框架

将一个动力系统转化为[状态空间](@entry_id:177074)形式的第一步，是定义一个**状态向量** (state vector)，我们通常用 $\mathbf{x}(t)$ 表示。这个向量的各个分量，即**[状态变量](@entry_id:138790)** (state variables)，必须能够完全地、无冗余地描述系统在任意时刻 $t$ 的状态。对于一个由 $n$ 个状态变量描述的系统，状态向量 $\mathbf{x}(t)$ 是一个 $n$ 维向量。

一旦定义了状态向量，我们的目标就是将系统的演化规则写成一个关于状态向量的[一阶微分方程](@entry_id:173139)。对于**[线性时不变 (LTI) 系统](@entry_id:178866)**，这个方程具有一个特别简洁和优美的形式：
$$
\frac{d\mathbf{x}}{dt} = A\mathbf{x} + \mathbf{b}
$$
其中，$A$ 是一个 $n \times n$ 的常数矩阵，被称为**[系统矩阵](@entry_id:172230)** (system matrix) 或**状态矩阵** (state matrix)。它描述了系统内部各状态变量之间的相互作用和自身动态。$\mathbf{b}$ 是一个 $n$ 维常数向量，代表系统受到的**外部输入** (external input) 或恒定驱动力。如果系统没有外部输入（$\mathbf{b} = \mathbf{0}$），则系统是**齐次的** (homogeneous)，其形式为：
$$
\frac{d\mathbf{x}}{dt} = A\mathbf{x}
$$
这个简单的矩阵方程构成了现代控制理论和[系统分析](@entry_id:263805)的基石。接下来的挑战在于，如何从一个给定的物理或数学模型中，正确地构建出矩阵 $A$ 和向量 $\mathbf{b}$。

### 构建系统矩阵：从模型到矩阵

将系统的动态特性转化为矩阵形式是一个系统性的过程，它适用于[连续时间系统](@entry_id:276553)、[离散时间系统](@entry_id:263935)，甚至数值计算格式。

#### 从[高阶常微分方程](@entry_id:138159)（连续时间）

物理和工程系统中，许多模型最初都以[高阶常微分方程](@entry_id:138159)（ODE）的形式出现。标准做法是通过巧妙地选择[状态变量](@entry_id:138790)，将一个 $n$ 阶ODE转化为一个由 $n$ 个一阶ODE组成的系统。

最自然的状态变量选择是系统变量本身及其各阶导数（直到 $n-1$ 阶）。让我们从一个二阶系统开始。考虑一个旋转[飞轮](@entry_id:195849)，由于内部摩擦，其转动会逐渐减慢。其[角位置](@entry_id:174053) $\theta(t)$ 遵循一个二阶齐次ODE [@problem_id:1692579]：
$$
I\frac{d^2\theta}{dt^2} + c\frac{d\theta}{dt} = 0
$$
其中 $I$ 是[转动惯量](@entry_id:174608)，$c$ 是粘滞[阻尼系数](@entry_id:163719)。这是一个二阶系统，因此我们需要两个状态变量来描述它。一个自然的选择是[角位置](@entry_id:174053)和[角速度](@entry_id:192539)。我们定义状态向量 $\mathbf{x}(t)$ 为：
$$
\mathbf{x}(t) = \begin{pmatrix} x_1(t) \\ x_2(t) \end{pmatrix} = \begin{pmatrix} \theta(t) \\ \frac{d\theta(t)}{dt} \end{pmatrix}
$$
现在，我们来寻找 $\dot{\mathbf{x}} = A\mathbf{x}$ 的形式。对[状态变量](@entry_id:138790)求导：
$\dot{x}_1 = \frac{d\theta}{dt}$，根据我们的定义，这正是 $x_2$。所以，第一个方程是 $\dot{x}_1 = x_2 = 0 \cdot x_1 + 1 \cdot x_2$。
$\dot{x}_2 = \frac{d^2\theta}{dt^2}$。我们可以从原始ODE中解出 $\ddot{\theta}$：$\ddot{\theta} = -\frac{c}{I}\dot{\theta}$。用状态变量替换，得到 $\dot{x}_2 = -\frac{c}{I}x_2 = 0 \cdot x_1 - \frac{c}{I}x_2$。
将这两个一阶方程写成矩阵形式，即：
$$
\frac{d}{dt}\begin{pmatrix} x_1 \\ x_2 \end{pmatrix} = \begin{pmatrix} 0  1 \\ 0  -\frac{c}{I} \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \end{pmatrix}
$$
因此，该系统的状态矩阵是 $A = \begin{pmatrix} 0  1 \\ 0  -c/I \end{pmatrix}$。

这个方法可以推广到任意 $n$ 阶线性齐次ODE。考虑一个三阶系统，例如用于控制[原子力显微镜](@entry_id:163411)（AFM）探针平滑运动的模型，其中不仅控制加速度，还控制加加速度（jerk）[@problem_id:1692614]。其位置 $x(t)$ 由以下方程描述：
$$
\frac{d^3x}{dt^3} + a_2 \frac{d^2x}{dt^2} + a_1 \frac{dx}{dt} + a_0 x = 0
$$
我们定义状态向量为 $\mathbf{y}(t) = \begin{pmatrix} x(t) \\ \dot{x}(t) \\ \ddot{x}(t) \end{pmatrix} = \begin{pmatrix} y_1 \\ y_2 \\ y_3 \end{pmatrix}$。
求导可得：
$\dot{y}_1 = \dot{x} = y_2$
$\dot{y}_2 = \ddot{x} = y_3$
$\dot{y}_3 = \dddot{x}$。从原方程解出 $\dddot{x}$：$\dddot{x} = -a_0 x - a_1 \dot{x} - a_2 \ddot{x} = -a_0 y_1 - a_1 y_2 - a_2 y_3$。
将这三个[方程组](@entry_id:193238)合成矩阵形式：
$$
\frac{d\mathbf{y}}{dt} = \begin{pmatrix} 0  1  0 \\ 0  0  1 \\ -a_0  -a_1  -a_2 \end{pmatrix} \mathbf{y}
$$
这个特定结构的矩阵被称为**[友矩阵](@entry_id:148203)** (companion matrix)。对于任何 $n$ 阶线性齐次ODE，只要我们选择[状态变量](@entry_id:138790)为 $x, \dot{x}, \dots, x^{(n-1)}$，其[系统矩阵](@entry_id:172230)都将呈现这种[友矩阵形式](@entry_id:747524)：超对角线上为1，最后一行是ODE系数的负值，其余元素为0。

如果系统受到外部恒定作用力，则为非[齐次系统](@entry_id:150411)。例如，一个受恒定风力 $F_0$ 作用的建筑物模型 [@problem_id:1692588]：
$$
m\ddot{x} + c\dot{x} + kx = F_0
$$
使用相同的状态向量 $\mathbf{y}(t) = \begin{pmatrix} x(t) \\ \dot{x}(t) \end{pmatrix}$，我们有：
$\dot{y}_1 = y_2$
$\dot{y}_2 = \ddot{x} = \frac{1}{m}(F_0 - kx - c\dot{x}) = -\frac{k}{m}y_1 - \frac{c}{m}y_2 + \frac{F_0}{m}$。
写成 $\dot{\mathbf{y}} = A\mathbf{y} + \mathbf{b}$ 的形式：
$$
\frac{d\mathbf{y}}{dt} = \begin{pmatrix} 0  1 \\ -k/m  -c/m \end{pmatrix} \mathbf{y} + \begin{pmatrix} 0 \\ F_0/m \end{pmatrix}
$$
这里，外部作用力 $F_0$ 体现在了输入向量 $\mathbf{b}$ 中。

#### 从[递推关系](@entry_id:189264)（离散时间）

状态空间的概念同样适用于[离散时间系统](@entry_id:263935)，其演化由递推关系描述，形式为 $\mathbf{v}_{n+1} = A \mathbf{v}_n$。考虑一个二阶[递推关系](@entry_id:189264) $x_{n+2} = 3x_{n+1} - 2x_n$ [@problem_id:1692584]。
标准的[状态向量](@entry_id:154607)选择是 $\mathbf{u}_n = \begin{pmatrix} x_n \\ x_{n+1} \end{pmatrix}$。那么 $\mathbf{u}_{n+1} = \begin{pmatrix} x_{n+1} \\ x_{n+2} \end{pmatrix} = \begin{pmatrix} x_{n+1} \\ 3x_{n+1} - 2x_n \end{pmatrix} = \begin{pmatrix} 0  1 \\ -2  3 \end{pmatrix} \begin{pmatrix} x_n \\ x_{n+1} \end{pmatrix}$。
然而，状态向量的选择并不唯一，不同的选择会产生不同的系统矩阵 $A$，但它们描述的是同一个底层系统。例如，如果我们选择一个非标准的状态向量 $\mathbf{v}_n = \begin{pmatrix} x_n \\ x_{n+1} + x_n \end{pmatrix}$，我们仍然可以找到一个矩阵 $A$ 使得 $\mathbf{v}_{n+1} = A\mathbf{v}_n$。
$\mathbf{v}_{n+1} = \begin{pmatrix} x_{n+1} \\ x_{n+2} + x_{n+1} \end{pmatrix}$。我们需要用 $\mathbf{v}_n$ 的分量 $v_{n,1}=x_n$ 和 $v_{n,2}=x_{n+1}+x_n$ 来表示 $\mathbf{v}_{n+1}$ 的分量。
第一个分量：$x_{n+1} = (x_{n+1}+x_n) - x_n = v_{n,2} - v_{n,1}$。
第二个分量：$x_{n+2}+x_{n+1} = (3x_{n+1}-2x_n) + x_{n+1} = 4x_{n+1}-2x_n$。代入 $x_{n+1}=v_{n,2}-v_{n,1}$，得到 $4(v_{n,2}-v_{n,1}) - 2v_{n,1} = 4v_{n,2} - 6v_{n,1}$。
因此，
$$
\mathbf{v}_{n+1} = \begin{pmatrix} -v_{n,1} + v_{n,2} \\ -6v_{n,1} + 4v_{n,2} \end{pmatrix} = \begin{pmatrix} -1  1 \\ -6  4 \end{pmatrix} \begin{pmatrix} v_{n,1} \\ v_{n,2} \end{pmatrix}
$$
这个例子表明，[状态空间表示](@entry_id:147149)法具有极大的灵活性，关键在于找到从当前状态到下一状态的[线性映射](@entry_id:185132)。

#### 从数值积分格式

在计算科学中，我们常用数值方法[求解微分方程](@entry_id:137471) $\dot{\mathbf{x}} = A\mathbf{x}$，这本质上是创建了一个[离散时间系统](@entry_id:263935)。例如，**隐式[后向欧拉法](@entry_id:139674)** [@problem_id:1692580] 是一个特别稳定的数值格式，其更新规则为：
$$
\frac{\mathbf{x}_{n+1} - \mathbf{x}_n}{h} = A\mathbf{x}_{n+1}
$$
其中 $h$ 是时间步长。这个形式是“隐式”的，因为未知量 $\mathbf{x}_{n+1}$ 出现在方程两侧。为了得到一个直接的迭代格式 $\mathbf{x}_{n+1} = M\mathbf{x}_n$，我们需要进行代数整理：
$\mathbf{x}_{n+1} - \mathbf{x}_n = h A\mathbf{x}_{n+1}$
$\mathbf{x}_n = \mathbf{x}_{n+1} - h A\mathbf{x}_{n+1} = (I - hA)\mathbf{x}_{n+1}$
假设矩阵 $(I-hA)$ 是可逆的，我们两边左乘其[逆矩阵](@entry_id:140380)：
$$
\mathbf{x}_{n+1} = (I - hA)^{-1}\mathbf{x}_n
$$
因此，后向欧拉法将连续系统 $\dot{\mathbf{x}} = A\mathbf{x}$ 转化为了一个离散系统 $\mathbf{x}_{n+1} = M\mathbf{x}_n$，其[转移矩阵](@entry_id:145510)为 $M=(I-hA)^{-1}$。

### 解读系统矩阵：揭示系统结构与动态

[系统矩阵](@entry_id:172230) $A$ 不仅仅是一堆数字，它编码了系统的全部内在联系。通过分析 $A$ 的元素和结构，我们可以洞察系统的行为模式。

#### 矩阵元素的物理意义

对于系统 $\dot{\mathbf{x}} = A\mathbf{x}$，其第 $i$ 个分量的方程是 $\dot{x}_i = \sum_{j=1}^n a_{ij}x_j = a_{ii}x_i + \sum_{j \neq i} a_{ij}x_j$。

- **对角元素 $a_{ii}$**：代表了[状态变量](@entry_id:138790) $x_i$ 的**内在增长/衰减率**。如果所有其他状态变量 $x_j (j \neq i)$ 均为零，则方程简化为 $\dot{x}_i = a_{ii}x_i$。若 $a_{ii} > 0$，$x_i$ 会指数增长；若 $a_{ii}  0$，$x_i$ 会指数衰减。

- **非对角元素 $a_{ij}$ ($i \neq j$)**：代表了[状态变量](@entry_id:138790) $x_j$ 对状态变量 $x_i$ 变化率的**影响**。$a_{ij}$ 的符号和大小描述了这种相互作用的性质和强度。

让我们通过一个生态学模型来具体理解。考虑两种微生物的种群动态 $\dot{\mathbf{x}} = A\mathbf{x}$，其中 $x_1, x_2$ 分别是两个物种的种群数量。

在一个**捕食-被捕食**关系中，例如物种1是被捕食者，物种2是捕食者 [@problem_id:1692569]。我们预期：
1. 被捕食者（物种1）在没有捕食者的情况下会自我增长，所以 $a_{11} > 0$。
2. 捕食者（物种2）在没有被捕食者的情况下会因饥饿而衰亡，所以 $a_{22}  0$。
3. 捕食者的存在对被捕食者有害，所以 $a_{12}  0$ (物种2对物种1增长率的贡献为负)。
4. 被捕食者的存在对捕食者有益，所以 $a_{21} > 0$ (物种1对物种2增长率的贡献为正)。
一个形如 $A = \begin{pmatrix} 0.4  -0.8 \\ 0.1  -0.2 \end{pmatrix}$ 的矩阵就完美符合这种捕食-被捕食的模式。

而在一个**竞争**关系中 [@problem_id:1692566]，两个物种互相抑制对方的生长。这意味着非对角元素都为负：$a_{12}  0$ 且 $a_{21}  0$。例如，矩阵 $A = \begin{pmatrix} -3  -1 \\ -2  -4 \end{pmatrix}$ 描述了一个竞争系统，其中两个物种的存在都对对方的增长率产生负面影响。

#### 矩阵结构与系统耦合

矩阵中的零元素同样传递着重要信息，它们表示系统内部的**解耦** (decoupling)。

如果矩阵 $A$ 的某个元素 $a_{ij}$ 为零，则意味着状态变量 $x_j$ 的值对 $x_i$ 的变化率没有直接影响。例如，在一个三组分[化学反应](@entry_id:146973)模型中，若要让物种 $x_1$ 的[反应速率](@entry_id:139813)只依赖于其自身浓度，而与 $x_2$ 和 $x_3$ 的浓度无关 [@problem_id:1692583]，则描述 $\dot{x}_1$ 的方程必须是 $\dot{x}_1 = a_{11}x_1$。这要求 $\dot{x}_1 = a_{11}x_1 + a_{12}x_2 + a_{13}x_3$ 中的系数 $a_{12}$ 和 $a_{13}$ 必须为零。

当零元素以特定模式出现时，可以揭示更大尺度的系统结构。一个特别重要的结构是**[块对角矩阵](@entry_id:145530)** (block-diagonal matrix)。如果系统矩阵 $A$ 是块[对角形式](@entry_id:264850)，那么整个系统可以分解为若干个完全独立的子系统。
考虑一个包含四个物种的生态系统，其[系统矩阵](@entry_id:172230)为 [@problem_id:1692551]：
$$
A = \begin{pmatrix}
-0.5  1.2  0  0 \\
-0.8  -0.1  0  0 \\
0  0  -0.9  0.3 \\
0  0  0.1  -0.4
\end{pmatrix}
= \begin{pmatrix} A_{11}  0 \\ 0  A_{22} \end{pmatrix}
$$
其中 $A_{11} = \begin{pmatrix} -0.5  1.2 \\ -0.8  -0.1 \end{pmatrix}$ 和 $A_{22} = \begin{pmatrix} -0.9  0.3 \\ 0.1  -0.4 \end{pmatrix}$。
定义子向量 $\mathbf{x}^{(1)} = \begin{pmatrix} x_1 \\ x_2 \end{pmatrix}$ 和 $\mathbf{x}^{(2)} = \begin{pmatrix} x_3 \\ x_4 \end{pmatrix}$，则原系统 $\dot{\mathbf{x}} = A\mathbf{x}$ 可以分解为两个完全独立的子系统：
$$
\dot{\mathbf{x}}^{(1)} = A_{11}\mathbf{x}^{(1)} \quad \text{和} \quad \dot{\mathbf{x}}^{(2)} = A_{22}\mathbf{x}^{(2)}
$$
这表明，物种1和2构成一个独立的生态子系统，它们之间的动态与物种3和4无关。同样，物种3和4也构成另一个独立的子系统。识别这种解耦结构对于分析和理解大型复杂系统至关重要。

#### 实系统与复数表示

许多真实系统表现出[振荡](@entry_id:267781)行为，这在线性系统中通常与矩阵 $A$ 的**复数[特征值](@entry_id:154894)**相关。将二维实数平面上的点 $(x, y)$ 看作复数 $z = x + iy$ 是一种非常有效的分析工具。

考虑一个由复数变量 $z(t)$ 描述的系统，其动力学由一个简单的复数[线性方程](@entry_id:151487)给出 [@problem_id:1692601]：
$$
\frac{dz}{dt} = (\lambda + i\omega)z
$$
其中 $\lambda$ 和 $\omega$ 是实常数。为了理解它在实数平面上的行为，我们将其转换回关于 $x(t)$ 和 $y(t)$ 的[实数系](@entry_id:157774)统。
代入 $z = x+iy$ 和 $\dot{z} = \dot{x} + i\dot{y}$：
$$
\dot{x} + i\dot{y} = (\lambda + i\omega)(x + iy) = (\lambda x - \omega y) + i(\omega x + \lambda y)
$$
通过分别令等式两边的实部和虚部相等，我们得到一个二维[实数系](@entry_id:157774)统：
$\dot{x} = \lambda x - \omega y$
$\dot{y} = \omega x + \lambda y$
写成矩阵形式：
$$
\frac{d}{dt}\begin{pmatrix} x \\ y \end{pmatrix} = \begin{pmatrix} \lambda  -\omega \\ \omega  \lambda \end{pmatrix} \begin{pmatrix} x \\ y \end{pmatrix}
$$
这个 $2 \times 2$ 的矩阵是[线性系统分析](@entry_id:166972)中的一个基本构建块。它代表了两种基本运动的结合：$\lambda$ 项控制着径向的缩放（$\lambda>0$ 为扩张，$\lambda0$ 为收缩），而 $\omega$ 项控制着旋转（$\omega$ 是角频率）。因此，复数[特征值](@entry_id:154894) $\lambda \pm i\omega$ 对应于实数平面上的螺旋动态。

### 矩阵性质与[守恒量](@entry_id:150267)

物理系统中的守恒律（如质量守恒、[能量守恒](@entry_id:140514)）是其基本属性。这些物理守恒律在[状态空间表示](@entry_id:147149)中会转化为对系统矩阵 $A$ 的特定代数约束。

#### 总量守恒

考虑一个[封闭系统](@entry_id:139565)，其中某种物质（如营养物、[电荷](@entry_id:275494)或人口）在不同隔间之间交换，但系统的总物质数量保持不变。例如，在一个由三个隔间组成的闭环[水培](@entry_id:141599)系统中，营养物总量 $T(t) = x_1(t) + x_2(t) + x_3(t)$ 是一个常数 [@problem_id:1692611]。
为了找到这在矩阵 $A$ 上施加的约束，我们对总量 $T(t)$ 求导：
$$
\frac{dT}{dt} = \dot{x}_1 + \dot{x}_2 + \dot{x}_3
$$
这可以优雅地用[向量表示](@entry_id:166424)。令 $\mathbf{s} = \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}$，则 $T(t) = \mathbf{s}^T \mathbf{x}(t)$。求导得：
$$
\frac{dT}{dt} = \mathbf{s}^T \dot{\mathbf{x}}(t) = \mathbf{s}^T A \mathbf{x}(t)
$$
为了使总量 $T(t)$ 对任意初始状态 $\mathbf{x}(0)$ 都守恒，导数必须恒为零，即 $\mathbf{s}^T A \mathbf{x}(t) = 0$ 对所有 $\mathbf{x}(t)$ 成立。这只有当行向量 $\mathbf{s}^T A$ 为[零向量](@entry_id:156189)时才可能。
$\mathbf{s}^T A = \begin{pmatrix} 1  1  1 \end{pmatrix} \begin{pmatrix} a_{11}  a_{12}  a_{13} \\ a_{21}  a_{22}  a_{23} \\ a_{31}  a_{32}  a_{33} \end{pmatrix} = \begin{pmatrix} \sum_i a_{i1}  \sum_i a_{i2}  \sum_i a_{i3} \end{pmatrix} = \begin{pmatrix} 0  0  0 \end{pmatrix}$
这要求矩阵 $A$ 的**每一列元素之和都必须为零**。这个条件的物理解释是直观的：列 $j$ 的元素描述了单位数量的 $x_j$ 如何影响所有隔间的变化率。列和为零意味着从隔间 $j$ 流出的总量等于流入其他隔间的总量，从而保证了系统整体的物质守恒。

#### 范数守恒（[能量守恒](@entry_id:140514)）

在理想的无[耗散力](@entry_id:166970)学系统或封闭的量子系统中，一个常见的守恒量是[状态向量](@entry_id:154607)的[欧几里得范数](@entry_id:172687)的平方，即 $L(t) = ||\mathbf{x}(t)||^2 = \mathbf{x}(t)^T \mathbf{x}(t)$。这通常与系统的总能量成正比。

为了研究这个守恒律对矩阵 $A$ 的要求，我们对 $L(t)$ 求时间导数 [@problem_id:1692578]：
$$
\frac{dL}{dt} = \frac{d}{dt}(\mathbf{x}^T\mathbf{x}) = \dot{\mathbf{x}}^T\mathbf{x} + \mathbf{x}^T\dot{\mathbf{x}}
$$
代入 $\dot{\mathbf{x}} = A\mathbf{x}$ 和 $\dot{\mathbf{x}}^T = (A\mathbf{x})^T = \mathbf{x}^T A^T$：
$$
\frac{dL}{dt} = (\mathbf{x}^T A^T)\mathbf{x} + \mathbf{x}^T(A\mathbf{x}) = \mathbf{x}^T A^T \mathbf{x} + \mathbf{x}^T A \mathbf{x} = \mathbf{x}^T (A^T + A) \mathbf{x}
$$
为了使 $L(t)$ 守恒，其导数必须对所有可能的 $\mathbf{x}$ 恒为零。这意味着二次型 $\mathbf{x}^T (A^T + A) \mathbf{x}$ 必须恒为零。由于矩阵 $(A^T+A)$ 是对称的，这只有在它本身是零矩阵时才成立。
$$
A^T + A = 0 \quad \iff \quad A^T = -A
$$
这个条件定义了一类特殊的矩阵：**斜对称矩阵** (skew-symmetric matrix)。因此，一个[线性系统](@entry_id:147850) $\dot{\mathbf{x}} = A\mathbf{x}$ 保持其[状态向量](@entry_id:154607)欧氏范数守恒的充要条件是，其[系统矩阵](@entry_id:172230) $A$ 是斜对称的。
所有 $n \times n$ 实[斜对称矩阵](@entry_id:155998)的集合构成一个重要的数学结构，称为**正交[李代数](@entry_id:137954)** (orthogonal Lie algebra)，记作 $\mathfrak{so}(n)$。这类系统产生的演化对应于[状态空间](@entry_id:177074)中的纯旋转（广义上的），不会改变状态向量的“长度”。

通过本章的学习，我们已经看到，[矩阵表示法](@entry_id:190318)不仅仅是一种记法上的便利，它是一个强大的分析工具。它将系统的动态行为、内部结构和物理守恒律与矩阵的代数性质紧密地联系在一起，为深入理解和操控动力系统提供了坚实的数学基础。