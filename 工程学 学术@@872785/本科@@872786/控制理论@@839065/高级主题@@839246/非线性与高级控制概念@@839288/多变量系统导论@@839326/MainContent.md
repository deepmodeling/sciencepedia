## 引言
在我们周围的世界中，从精密的机器人到复杂的生态系统，绝大多数动态过程都具有多个输入和多个输出。这些“[多变量系统](@entry_id:169616)”（MIMO）的核心特征是其内部组件之间存在着错综复杂的相互作用或“耦合”。试图用传统的单输入单输出（SISO）模型来理解它们，就如同只用一只眼睛观察一个三维物体，会丢失至关重要的深度信息。因此，掌握一套能够精确描述和分析这种多维交互的理论框架至关重要。

本文旨在系统地介绍[多变量系统](@entry_id:169616)的基本原理和分析方法，填补SIS[O模](@entry_id:186318)型留下的认知空白。通过学习本文，你将能够驾驭描述复杂系统的强大数学工具，并理解如何应用它们来解决现实世界中的挑战。在接下来的章节中，我们将首先在**第一章“原理与机制”**中，深入探讨描述这些系统的数学语言，包括[状态空间表示](@entry_id:147149)法和[传递函数矩阵](@entry_id:271746)，并揭示能控性、能观性等深刻的内部结构属性。随后，**第二章“应用与交叉学科联系”**将通过一系列生动的实例，展示这些理论如何应用于解决工程、生物和机器人学等不同领域的实际问题。最后，**第三章“动手实践”**将提供具体的计算和分析练习，帮助你将理论知识真正付诸实践。

现在，让我们从[多变量系统](@entry_id:169616)的[基本表示](@entry_id:157678)方法开始，踏上理解复杂动态世界的第一步。

## 原理与机制

在对[多变量系统](@entry_id:169616)有了初步认识之后，本章将深入探讨其核心的数学原理与物理机制。我们将从系统的内部状态描述出发，逐步过渡到其外部输入输出行为，并最终揭示连接这两者的深刻结构性概念，如能控性、能观性与隐藏模态。

### [多变量系统](@entry_id:169616)的表示：[状态空间](@entry_id:177074)方法

描述动态系统最强大和通用的方法之一是**[状态空间表示](@entry_id:147149)法** (state-space representation)。与专注于输入和输出之间直接关系的[传递函数](@entry_id:273897)不同，状态空间方法引入了**[状态变量](@entry_id:138790)** (state variables) 的概念，它们构成了一个向量 $\mathbf{x}(t)$，完整地概括了系统在任意时刻 $t$ 的内部状况。有了当前的状态 $\mathbf{x}(t)$ 和未来所有时间的输入 $\mathbf{u}(t)$，我们就能唯一地确定系统未来的所有[状态和](@entry_id:193625)输出 $\mathbf{y}(t)$。

对于一个[线性时不变](@entry_id:276287)（LTI）系统，其[状态空间模型](@entry_id:137993)由以下一对标准方程给出：

$$
\dot{\mathbf{x}}(t) = A\mathbf{x}(t) + B\mathbf{u}(t) \quad (\text{状态方程})
$$

$$
\mathbf{y}(t) = C\mathbf{x}(t) + D\mathbf{u}(t) \quad (\text{输出方程})
$$

其中：
- $\mathbf{x}(t)$ 是 $n \times 1$ 的**状态向量**，其分量是状态变量。$n$ 是系统的阶数。
- $\mathbf{u}(t)$ 是 $m \times 1$ 的**输入向量**，代表外部施加的[控制信号](@entry_id:747841)或扰动。
- $\mathbf{y}(t)$ 是 $p \times 1$ 的**输出向量**，代表我们能够测量或关心的系统量。
- $A$ 是 $n \times n$ 的**状态矩阵** (state matrix)，描述了系统内部[状态变量](@entry_id:138790)之间的相互影响，决定了系统的固有动态特性。
- $B$ 是 $n \times m$ 的**输入矩阵** (input matrix)，描述了每个输入如何影响每个状态变量的变化率。
- $C$ 是 $p \times n$ 的**输出矩阵** (output matrix)，描述了每个[状态变量](@entry_id:138790)如何组合形成可测量的输出。
- $D$ 是 $p \times m$ 的**馈通矩阵** (feedthrough matrix) 或前馈矩阵，描述了输入信号是否直接、瞬时地影响输出。

为了将这些抽象的矩阵与物理现实联系起来，让我们考虑一个环境测试箱的简化模型[@problem_id:1583888]。该系统有两个输入：加热元件功率 $P(t)$ 和循环风扇电压 $V(t)$；以及两个输出：箱内温度 $T(t)$ 和空气流速 $v(t)$。系统的内部状态可以用温度 $T(t)$ 和风扇[角速度](@entry_id:192539) $\omega(t)$ 来描述。基于物理定律（[热力学](@entry_id:141121)、电机学），我们可以写出如下的耦合[微分方程](@entry_id:264184)：

$$
\frac{dT(t)}{dt} = -\alpha T(t) - \beta \omega(t) + \gamma P(t)
$$

$$
\frac{d\omega(t)}{dt} = -\epsilon T(t) -\delta \omega(t) + \zeta V(t)
$$

输出则与状态变量相关：$y_1(t) = T(t)$ 且 $y_2(t) = v(t) = \eta \omega(t)$。其中 $\alpha, \beta, \gamma, \delta, \epsilon, \zeta, \eta$ 均为代表物理参数的正常数。

通过将这些方程与标准状态[空间形式](@entry_id:186145)进行匹配，我们可以轻松构建[系统矩阵](@entry_id:172230)。定义[状态向量](@entry_id:154607) $\mathbf{x}(t) = \begin{pmatrix} T(t) \\ \omega(t) \end{pmatrix}$，输入向量 $\mathbf{u}(t) = \begin{pmatrix} P(t) \\ V(t) \end{pmatrix}$，和输出向量 $\mathbf{y}(t) = \begin{pmatrix} y_1(t) \\ y_2(t) \end{pmatrix}$。微分方程组可以写成矩阵形式：

$$
\frac{d}{dt}\begin{pmatrix} T \\ \omega \end{pmatrix} = \begin{pmatrix} -\alpha  -\beta \\ -\epsilon  -\delta \end{pmatrix} \begin{pmatrix} T \\ \omega \end{pmatrix} + \begin{pmatrix} \gamma  0 \\ 0  \zeta \end{pmatrix} \begin{pmatrix} P \\ V \end{pmatrix}
$$

输出方程则为：

$$
\begin{pmatrix} y_1 \\ y_2 \end{pmatrix} = \begin{pmatrix} 1  0 \\ 0  \eta \end{pmatrix} \begin{pmatrix} T \\ \omega \end{pmatrix} + \begin{pmatrix} 0  0 \\ 0  0 \end{pmatrix} \begin{pmatrix} P \\ V \end{pmatrix}
$$

由此我们得到了该系统的[状态空间](@entry_id:177074)矩阵：$A = \begin{pmatrix} -\alpha  -\beta \\ -\epsilon  -\delta \end{pmatrix}$，$B = \begin{pmatrix} \gamma  0 \\ 0  \zeta \end{pmatrix}$，$C = \begin{pmatrix} 1  0 \\ 0  \eta \end{pmatrix}$，以及 $D = \begin{pmatrix} 0  0 \\ 0  0 \end{pmatrix}$。

在这个例子中，$D$ 矩阵是[零矩阵](@entry_id:155836)，这意味着输入信号（功率、电压）不会立即出现在输出端（温度、流速）。输出的变化必须通过系统的内部动态（状态）进行传递。然而，在许多系统中，$D$ 矩阵并非为零。一个非零的 $D$ 矩阵意味着输入和输出之间存在一条直接的代数路径。

考虑一个[串联](@entry_id:141009)[RLC电路](@entry_id:171534)[@problem_id:1583860]，输入为电压源 $u(t) = v_{in}(t)$，状态变量为电感电流 $x_1(t) = i_L(t)$ 和电容电压 $x_2(t) = v_C(t)$。如果我们选择一个输出为电容电压 $y_1(t) = v_C(t)$，另一个输出为[电感](@entry_id:276031)和电阻上的电压之和 $y_2(t) = v_L(t) + v_R(t)$。根据[基尔霍夫电压定律](@entry_id:276614)，$v_{in}(t) = v_L(t) + v_R(t) + v_C(t)$，因此 $y_2(t) = v_{in}(t) - v_C(t) = u(t) - x_2(t)$。输出方程可以写成：

$$
\mathbf{y}(t) = \begin{pmatrix} y_1(t) \\ y_2(t) \end{pmatrix} = \begin{pmatrix} 0  1 \\ 0  -1 \end{pmatrix} \begin{pmatrix} x_1(t) \\ x_2(t) \end{pmatrix} + \begin{pmatrix} 0 \\ 1 \end{pmatrix} u(t)
$$

这里的馈通矩阵 $D = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$。非零的第二行元素表明，输入电压 $u(t)$ 的变化会瞬时地、按比例地反映在输出 $y_2(t)$ 上。这在物理上是合理的，因为 $y_2$ 的定义中直接包含了输入电压的一部分。

### 外部描述：[传递函数矩阵](@entry_id:271746)

虽然状态空间模型提供了系统的完整内部视图，但在许多工程应用中，我们更关心系统对外部输入的响应，即其“黑箱”行为。这种行为由**[传递函数矩阵](@entry_id:271746)** (transfer function matrix) $G(s)$ 描述，它将输入向量的[拉普拉斯变换](@entry_id:159339) $U(s)$ 映射到输出向量的拉普拉斯变换 $Y(s)$：

$$
Y(s) = G(s)U(s)
$$

对于一个有 $m$ 个输入和 $p$ 个输出的系统，$G(s)$ 是一个 $p \times m$ 的矩阵，其每个元素 $G_{ij}(s)$ 是从第 $j$ 个输入 $U_j(s)$ 到第 $i$ 个输出 $Y_i(s)$ 的标量[传递函数](@entry_id:273897)（假设所有其他输入为零）。

从[状态空间表示](@entry_id:147149) $(A, B, C, D)$ 出发，可以通过对[状态和](@entry_id:193625)输出方程进行[拉普拉斯变换](@entry_id:159339)来推导[传递函数矩阵](@entry_id:271746)。假设初始条件为零，[状态方程](@entry_id:274378)变为 $sX(s) = AX(s) + BU(s)$，整理后得到 $(sI - A)X(s) = BU(s)$，因此[状态向量](@entry_id:154607)为 $X(s) = (sI - A)^{-1}BU(s)$。将此表达式代入输出方程的[拉普拉斯变换](@entry_id:159339) $Y(s) = CX(s) + DU(s)$，我们得到：

$$
Y(s) = C(sI - A)^{-1}BU(s) + DU(s) = [C(sI - A)^{-1}B + D]U(s)
$$

由此，我们得到了连接两种表示法的基本公式：

$$
G(s) = C(sI - A)^{-1}B + D
$$

这个公式是现代控制理论的基石之一。它表明，系统的外部行为 $G(s)$ 完全由其内部模型 $(A, B, C, D)$ 决定。

让我们通过一个具体的数值例子来演示这个计算过程[@problem_id:1583879]。假设一个热力系统的[状态空间](@entry_id:177074)矩阵为：
$$
A = \begin{pmatrix} -3  1 \\ 2  -4 \end{pmatrix}, \quad B = \begin{pmatrix} 1  0 \\ 0  2 \end{pmatrix}, \quad C = \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix}, \quad D = \begin{pmatrix} 0  0 \\ 0  0 \end{pmatrix}
$$

首先，计算 $(sI - A)$：
$$
sI - A = \begin{pmatrix} s+3  -1 \\ -2  s+4 \end{pmatrix}
$$

然后，求其[逆矩阵](@entry_id:140380)。对于一个 $2 \times 2$ 矩阵 $\begin{pmatrix} a  b \\ c  d \end{pmatrix}$，其逆为 $\frac{1}{ad-bc}\begin{pmatrix} d  -b \\ -c  a \end{pmatrix}$。因此：
$$
(sI - A)^{-1} = \frac{1}{(s+3)(s+4) - 2} \begin{pmatrix} s+4  1 \\ 2  s+3 \end{pmatrix} = \frac{1}{s^2 + 7s + 10} \begin{pmatrix} s+4  1 \\ 2  s+3 \end{pmatrix}
$$

接下来，将结果与 $B$ 和 $C$ 相乘：
$$
G(s) = C(sI - A)^{-1}B = \frac{1}{s^2 + 7s + 10} \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix} \begin{pmatrix} s+4  1 \\ 2  s+3 \end{pmatrix} \begin{pmatrix} 1  0 \\ 0  2 \end{pmatrix}
$$
$$
G(s) = \frac{1}{s^2 + 7s + 10} \begin{pmatrix} 1  1 \\ 1  -1 \end{pmatrix} \begin{pmatrix} s+4  2 \\ 2  2(s+3) \end{pmatrix}
$$
$$
G(s) = \frac{1}{s^2 + 7s + 10} \begin{pmatrix} s+6  2s+8 \\ s+2  -2s-4 \end{pmatrix} = \begin{pmatrix} \frac{s+6}{s^2+7s+10}  \frac{2s+8}{s^2+7s+10} \\ \frac{s+2}{s^2+7s+10}  \frac{-2s-4}{s^2+7s+10} \end{pmatrix}
$$

我们也可以将这个公式应用于之前环境测试箱的例子[@problem_id:1583888]，从而得到其[传递函数矩阵](@entry_id:271746)，进一步验证了物理模型和外部描述之间的联系。

### 理解系统动态：极点、零点与模态

[传递函数矩阵](@entry_id:271746) $G(s)$ 和状态矩阵 $A$ 包含了关于系统动态行为的丰富信息。其中，极点、零点和模态是理解这些行为的关键概念。

#### [系统极点](@entry_id:275195)与模态

**[系统极点](@entry_id:275195)** (system poles) 是状态矩阵 $A$ 的[特征值](@entry_id:154894)。它们是系统固有动态特性的核心，决定了系统在没有外部输入（即**[零输入响应](@entry_id:274925)**）时的行为。极点的位置直接关系到系统的稳定性、响应速度和[振荡](@entry_id:267781)特性。
- 位于复平面[左半平面](@entry_id:270729)的极点对应于衰减的响应，系统是稳定的。
- 位于[右半平面](@entry_id:277010)的极点对应于发散的响应，系统是不稳定的。
- 位于[虚轴上的极点](@entry_id:273240)对应于持续[振荡](@entry_id:267781)或[线性增长](@entry_id:157553)的响应（取决于重根情况）。

与每个[特征值](@entry_id:154894)（极点）$\lambda_i$ 相关联的是一个[特征向量](@entry_id:151813) $\mathbf{v}_i$。这对 $(\lambda_i, \mathbf{v}_i)$ 定义了系统的一个**动态模态** (dynamic mode)。一个模态可以被看作是系统的一种“自然运动”模式。系统的任何[零输入响应](@entry_id:274925)都可以表示为这些模态的线性组合。

考虑最简单的情况，当状态矩阵 $A$ 是一个对角矩阵时[@problem_id:1583882]：
$$
A = \begin{pmatrix} -0.5  0 \\ 0  -2.0 \end{pmatrix}
$$
这代表一个污染物处理系统，其中 $x_1$ 和 $x_2$ 分别是两种不同污染物的浓度。由于 $A$ 是对角矩阵，状态方程是**[解耦](@entry_id:637294)**的：
$$
\dot{x}_1 = -0.5 x_1
$$
$$
\dot{x}_2 = -2.0 x_2
$$
其解为 $x_1(t) = x_1(0)e^{-0.5t}$ 和 $x_2(t) = x_2(0)e^{-2.0t}$。这里的极点是 $\lambda_1 = -0.5$ 和 $\lambda_2 = -2.0$。它们分别对应两个独立的衰减模态。第一个模态只涉及污染物X，其衰减速率为 $0.5$；第二个模态只涉及污染物Y，其衰减速率为 $2.0$。

对于更一般的情况，当 $A$ 不是对角矩阵时，模态是耦合的。系统的[零输入响应](@entry_id:274925) $\mathbf{x}(t)$ 是由初始状态 $\mathbf{x}(0)$ 激发的。如果 $\mathbf{x}(0)$ 恰好是 $A$ 的一个[特征向量](@entry_id:151813) $\mathbf{v}_i$，那么响应将沿着该[特征向量](@entry_id:151813)的方向演化，即 $\mathbf{x}(t) = e^{\lambda_i t}\mathbf{v}_i$。对于任意初始状态 $\mathbf{x}(0)$，我们可以将其分解为[特征向量](@entry_id:151813)的[线性组合](@entry_id:154743) $\mathbf{x}(0) = \sum_{i=1}^{n} c_i \mathbf{v}_i$。由于线性性，总响应就是各个模态响应的叠加：
$$
\mathbf{x}(t) = e^{At}\mathbf{x}(0) = \sum_{i=1}^{n} c_i e^{\lambda_i t} \mathbf{v}_i
$$
最终的输出响应则是 $\mathbf{y}(t) = C\mathbf{x}(t)$。例如，在一个具有非对角 $A$ 矩阵的系统中，给定初始条件 $\mathbf{x}(0) = \begin{pmatrix} 2 \\ -1 \end{pmatrix}$，我们可以通过计算 $A$ 的[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)，然后将 $\mathbf{x}(0)$ 分解到[特征向量基](@entry_id:163721)上，从而求得系统的[零输入响应](@entry_id:274925) $\mathbf{y}(t)$ [@problem_id:1583846]。这个过程清晰地展示了系统的内部模态如何被初始状态“激活”，并共同塑造最终的输出行为。

#### 系统零点：传递零点

与极点描述系统的固有动态相反，零点描述了系统如何响应特定频率或模式的输入。对于[多变量系统](@entry_id:169616)，零点的概念比单输入单输出（SISO）系统要复杂得多。一个核心概念是**传递零点** (transmission zeros)。

传递零点是复数 $s$ 的值，在这些值上，系统会“阻止”某些输入信号的传递。更准确地说，对于一个特定的输入信号方向和频率 $s_0$，如果存在一个非零输入 $U(s_0)$ 使得输出 $Y(s_0) = G(s_0)U(s_0) = \mathbf{0}$，那么 $s_0$ 就是一个传递零点。对于一个方阵 $G(s)$（即输入和输出数量相同），这等价于[传递函数矩阵](@entry_id:271746) $G(s)$ 在 $s=s_0$ 处失去满秩，即：

$$
\det(G(s_0)) = 0
$$

值得注意的是，传递零点是整个[多变量系统](@entry_id:169616)的属性，而不是其任何单个 $G_{ij}(s)$ 元素的属性。

让我们分析一个化工单元的[传递函数矩阵](@entry_id:271746)来区分极点和零点[@problem_id:1583852]：
$$
G(s) = \begin{pmatrix} \frac{1}{s+1}  \frac{1}{(s+1)(s+3)} \\ \frac{2}{s+2}  \frac{s+1}{s+2} \end{pmatrix}
$$

系统的**极点**集合是 $G(s)$ 所有元素分母的根的并集。在这里，分母因子是 $(s+1)$, $(s+2)$, 和 $(s+3)$，所以[系统极点](@entry_id:275195)集为 $\{-1, -2, -3\}$。

为了找到**传递零点**，我们计算 $G(s)$ 的[行列式](@entry_id:142978)：
$$
\det G(s) = \left(\frac{1}{s+1}\right)\left(\frac{s+1}{s+2}\right) - \left(\frac{1}{(s+1)(s+3)}\right)\left(\frac{2}{s+2}\right)
$$
$$
\det G(s) = \frac{1}{s+2} - \frac{2}{(s+1)(s+2)(s+3)} = \frac{(s+1)(s+3) - 2}{(s+1)(s+2)(s+3)} = \frac{s^2 + 4s + 1}{(s+1)(s+2)(s+3)}
$$
传递零点是使[行列式](@entry_id:142978)分子为零的 $s$ 值，即 $s^2 + 4s + 1 = 0$。使用[二次方程](@entry_id:163234)求根公式，我们得到传递零点为 $s = -2 \pm \sqrt{3}$。

这个例子清楚地表明，[系统极点](@entry_id:275195)（$\{-1, -2, -3\}$）和传递零点（$\{-2 + \sqrt{3}, -2 - \sqrt{3}\}$）是完全不同的两组值，它们描述了系统动态行为的不同方面。

### 输入输出行为与交互

[多变量系统](@entry_id:169616)的核心特征在于其输入和输出之间的复杂交互。这些交互通过[传递函数矩阵](@entry_id:271746)的结构和系统的[方向性](@entry_id:266095)增益来量化。

#### 耦合与[阶跃响应](@entry_id:148543)

在[传递函数矩阵](@entry_id:271746) $G(s)$ 中，对角元素 $G_{ii}(s)$ 描述了第 $i$ 个输入对第 $i$ 个输出的“直接”影响，而非对角元素 $G_{ij}(s)$ ($i \neq j$) 则代表了**[交叉](@entry_id:147634)耦合** (cross-coupling)。一个显著的非对角项意味着一个输入通道的变化会强烈地影响到另一个输出通道。

考虑一个双核处理器的热管理系统模型[@problem_id:1583862]。输入 $u_1, u_2$ 是两个核心的加热功率，输出 $y_1, y_2$ 是两个核心附近的温度。其[传递函数矩阵](@entry_id:271746)具有以下形式：
$$
G(s) = \begin{pmatrix} G_{11}(s)  G_{12}(s) \\ G_{21}(s)  G_{22}(s) \end{pmatrix} = \begin{pmatrix} \frac{K_{11}}{\tau_{1}s + 1}  \frac{K_{12}}{\tau_{c}s + 1} \\ \frac{K_{21}}{\tau_{c}s + 1}  \frac{K_{22}}{\tau_{2}s + 1} \end{pmatrix}
$$
其中 $K_{ij}$ 是[稳态](@entry_id:182458)增益，$\tau$ 是时间常数。$G_{21}(s)$ 代表了从核心1到核心2的热传递效应。如果我们只在输入1上施加一个单位阶跃信号（即 $U_1(s) = 1/s, U_2(s) = 0$），输出响应的[拉普拉斯变换](@entry_id:159339)为：
$$
Y_1(s) = G_{11}(s)U_1(s) = \frac{K_{11}}{s(\tau_1 s + 1)}
$$
$$
Y_2(s) = G_{21}(s)U_1(s) = \frac{K_{21}}{s(\tau_c s + 1)}
$$
通过拉普拉斯反变换，我们得到[时域响应](@entry_id:271891)：
$$
y_1(t) = K_{11}(1 - e^{-t/\tau_1})
$$
$$
y_2(t) = K_{21}(1 - e^{-t/\tau_c})
$$
这个结果清晰地表明，即使输入2始终为零，输出2也会因为交叉耦合项 $G_{21}(s)$ 的存在而产生响应。对核心1的加热不仅使其自身升温，也通过[热传导](@entry_id:147831)使核心2升温。在设计控制器时，必须考虑并补偿这种耦合效应，否则对一个通道的控制操作可能会无意中干扰到其他通道。

#### [方向性与增益](@entry_id:264397)：[奇异值分析](@entry_id:169001)

对于SISO系统，增益在任何频率下都只是一个标量。但对于[MIMO系统](@entry_id:268566)，增益是**方向性的**。这意味着，对于相同大小（范数）的输入向量 $\mathbf{u}$，如果其方向不同，产生的输出向量 $\mathbf{y}$ 的大小可能会有很大差异。

一个关键问题是：系统在哪个输入方向上具有最大的放大能力？为了回答这个问题，我们使用**[奇异值分解](@entry_id:138057)** (Singular Value Decomposition, SVD)。首先，我们关注[稳态](@entry_id:182458)行为，这由**[直流增益](@entry_id:267449)矩阵** (DC gain matrix) $G(0)$ 决定。对于一个常数输入 $\mathbf{u}$，[稳态](@entry_id:182458)输出为 $\mathbf{y}_{ss} = G(0)\mathbf{u}$。

$G(0)$ 的[奇异值](@entry_id:152907) $\sigma_i$ 给出了系统在各个主方向上的[稳态](@entry_id:182458)增益。最大的[奇异值](@entry_id:152907) $\sigma_{max}$ 代表了系统可能实现的最大[稳态](@entry_id:182458)增益，即 $\max \frac{\|\mathbf{y}_{ss}\|}{\|\mathbf{u}\|} = \sigma_{max}$。达到这个最大增益的输入方向由对应的[右奇异向量](@entry_id:754365) $\mathbf{v}_{max}$ 给出。

让我们看一个例子[@problem_id:1583828]。一个系统的[直流增益](@entry_id:267449)矩阵为：
$$
A = G(0) = \begin{pmatrix} 4  4 \\ -3  3 \end{pmatrix}
$$
为了找到奇异值，我们计算 $A^T A$ 的[特征值](@entry_id:154894)。
$$
A^T A = \begin{pmatrix} 4  -3 \\ 4  3 \end{pmatrix} \begin{pmatrix} 4  4 \\ -3  3 \end{pmatrix} = \begin{pmatrix} 25  7 \\ 7  25 \end{pmatrix}
$$
其[特征值](@entry_id:154894)为 $\lambda_1 = 32$ 和 $\lambda_2 = 18$。[奇异值](@entry_id:152907)是[特征值](@entry_id:154894)的平方根，所以 $\sigma_{max} = \sqrt{32} = 4\sqrt{2} \approx 5.657$，$\sigma_{min} = \sqrt{18} = 3\sqrt{2}$。

最大增益为 $\sigma_{max} \approx 5.657$。对应的输入方向是 $A^T A$ 对应于[特征值](@entry_id:154894) $32$ 的[特征向量](@entry_id:151813)。求解 $(A^T A - 32I)\mathbf{v} = \mathbf{0}$，我们得到 $\begin{pmatrix} -7  7 \\ 7  -7 \end{pmatrix}\mathbf{v} = \mathbf{0}$，这意味着 $v_1 = v_2$。因此，实现最大增益的输入方向是 $\mathbf{u} = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$（或其单位向量形式 $\begin{pmatrix} 1/\sqrt{2} \\ 1/\sqrt{2} \end{pmatrix}$）。这意味着，当输入能量平均分配在两个通道上时，系统输出的能量（范数）被最大程度地放大了。[奇异值分析](@entry_id:169001)为理解和量化[MIMO系统](@entry_id:268566)的多向性增益提供了一个强大的工具。

### 内部结构：能控性、能观性与[最小实现](@entry_id:176932)

到目前为止，我们似乎有两个等效的系统描述：内部的[状态空间模型](@entry_id:137993) $(A, B, C, D)$ 和外部的[传递函数矩阵](@entry_id:271746) $G(s)$。一个自然的问题是：这种等价性是绝对的吗？$G(s)$ 是否总能揭示系统所有的动态特性？答案是否定的。

#### 隐藏模态问题

在从状态空间模型计算[传递函数矩阵](@entry_id:271746) $G(s) = C(sI-A)^{-1}B+D$ 的过程中，可能会发生**极零相消**。具体来说，$(sI-A)^{-1}$ 的某些极点（即 $A$ 的[特征值](@entry_id:154894)）可能会被 $C$ 和 $B$ 的乘积效应所“抵消”，从而不会出现在最终 $G(s)$ 的任何一个元素的极点中。这些没有在输入输出关系中表现出来的[系统极点](@entry_id:275195)所对应的模态被称为**隐藏模态** (hidden modes)。

考虑一个三阶系统[@problem_id:1583834]，其状态矩阵 $A$ 是上三角矩阵：
$$
A = \begin{pmatrix} -1  1  0 \\ 0  -2  0 \\ 0  0  -3 \end{pmatrix}
$$
其极点（[特征值](@entry_id:154894)）显然是 $\{-1, -2, -3\}$。假设 $B, C, D$ 矩阵经过计算后得到的[传递函数矩阵](@entry_id:271746)为：
$$
G(s) = \begin{pmatrix} \frac{1}{(s+1)(s+2)}  \frac{1}{s+1} \\ \frac{1}{s+2}  0 \end{pmatrix}
$$
观察 $G(s)$，我们发现其元素的极点只包含 $\{-1, -2\}$。系统原有的极点 $s=-3$ 神秘地消失了。这意味着与 $s=-3$ 相关的动态模态是隐藏的。无论我们施加什么样的输入信号，都无法从输出端观察到这个模态的行为。这是一种危险的情况，因为如果这个隐藏模态是不稳定的（例如，极点在右半平面），系统内部状态可能会发散到无穷大，而输出却可能保持平静，直到系统崩溃。

#### 能控性与能观性

隐藏模态的存在与两个深刻的结构性概念密切相关：**能控性** (controllability) 和**能观性** (observability)。

- **能控性** 回答了这样一个问题：我们能否通过选择合适的输入 $\mathbf{u}(t)$，在有限时间内将系统的状态 $\mathbf{x}(t)$ 从任意初始状态驱动到任意最终状态？如果一个系统的某个模态是不可控的，那就意味着没有任何输入信号能够“激发”或影响这个模态。

- **能观性** 回答了另一个问题：我们能否通过在有限时间内观察输出 $\mathbf{y}(t)$，唯一地确定系统的初始状态 $\mathbf{x}(0)$？如果一个系统的某个模态是不可观的，那就意味着这个模态的任何活动都不会在输出端产生任何痕迹。

隐藏模态的出现，正是因为该模态要么是不可控的，要么是不可观的，或者两者都是。在上面的例子[@problem_id:1583834]中，极点 $s=-3$ 对应的模态是不可观的，因此它对输出没有影响，从而在 $G(s)$ 中被“隐藏”了。

判断一个系统是否完全能控和能观，可以使用**卡尔曼秩判据** (Kalman rank conditions)。对于一个 $n$ 阶系统，其能控性矩阵和能观性矩阵分别定义为：
$$
\mathcal{C} = \begin{pmatrix} B  AB  A^2B  \cdots  A^{n-1}B \end{pmatrix} \quad (n \times nm \text{ 矩阵})
$$
$$
\mathcal{O} = \begin{pmatrix} C \\ CA \\ CA^2 \\ \vdots \\ CA^{n-1} \end{pmatrix} \quad (np \times n \text{ 矩阵})
$$

系统是完全能控的，当且仅当 $\text{rank}(\mathcal{C}) = n$。
系统是完全能观的，当且仅当 $\text{rank}(\mathcal{O}) = n$。

例如，对于一个机器人机械臂模型[@problem_id:1583856]，其矩阵为 $A = \begin{pmatrix} -3  1 \\ 2  -4 \end{pmatrix}$, $B = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$, $C = \begin{pmatrix} 1  -1 \end{pmatrix}$。
其能控性矩阵为：
$$
\mathcal{C} = \begin{pmatrix} B  AB \end{pmatrix} = \begin{pmatrix} 1  -3 \\ 0  2 \end{pmatrix}
$$
由于 $\det(\mathcal{C}) = 2 \neq 0$，该矩阵满秩，所以系统是完全能控的。
其能观性矩阵为：
$$
\mathcal{O} = \begin{pmatrix} C \\ CA \end{pmatrix} = \begin{pmatrix} 1  -1 \\ -5  5 \end{pmatrix}
$$
由于 $\det(\mathcal{O}) = 5 - 5 = 0$，该[矩阵秩](@entry_id:153017)为1（小于阶数2），所以系统是不可观的。存在一个不可观测的模态组合，这会导致信息丢失，并且可能存在隐藏模态。

#### [最小实现](@entry_id:176932)

一个既完全能控又完全能观的状态空间模型被称为一个**[最小实现](@entry_id:176932)** (minimal realization)。它的重要性在于，对于一个给定的[传递函数矩阵](@entry_id:271746) $G(s)$，其[最小实现](@entry_id:176932)的阶数 $n$ 是所有能够产生该 $G(s)$ 的状态空间模型中最低的。一个[最小实现](@entry_id:176932)是“刚刚好”的描述：它不多不少，包含了所有必要的动态信息，没有任何冗余或隐藏的状态。

从一个非最小的实现（即存在不可控或不可观模态的实现）出发，总是可以通过数学方法剔除这些隐藏模态，从而得到一个阶数更低、输入输出行为完全相同的[最小实现](@entry_id:176932)。因此，能控性和能观性的概念不仅揭示了系统的深层结构，也为我们寻找最简洁、最有效的系统模型提供了理论基础。