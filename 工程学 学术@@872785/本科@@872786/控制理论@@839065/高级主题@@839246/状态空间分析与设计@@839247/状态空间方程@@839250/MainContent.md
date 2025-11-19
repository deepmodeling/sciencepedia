## 引言
在[系统动力学](@entry_id:136288)和控制理论的广阔领域中，建立精确的数学模型是理解、预测和控制系统行为的基石。经典控制理论主要依赖[传递函数](@entry_id:273897)，它在分析单输入单输出（SISO）[线性系统](@entry_id:147850)方面卓有成效。然而，面对日益复杂的多输入多输出（MIMO）系统、非零[初始条件](@entry_id:152863)的情境，以及深入洞察系统内部状态动态的需求，[传递函数](@entry_id:273897)法显得力不从心。这一知识空白催生了现代控制理论的核心工具——[状态空间](@entry_id:177074)法。

本文旨在系统地介绍[状态空间](@entry_id:177074)方程这一强大框架。通过学习本文，你将不仅掌握其理论精髓，更能体会其在解决实际问题中的巨大威力。
- 在“**原理与机制**”一章中，我们将深入[状态空间](@entry_id:177074)的核心，学习如何定义状态变量，如何从物理第一性原理或[传递函数](@entry_id:273897)建立[状态空间模型](@entry_id:137993)，并掌握求解[状态方程](@entry_id:274378)以及分析系统稳定性、能控性和能观性等关键性质的方法。
- 随后的“**应用与交叉学科联系**”一章将拓宽你的视野，通过电气、机械、经济乃至生物系统等丰富案例，展示[状态空间](@entry_id:177074)法作为一种通用语言，是如何连接不同学科并解决前沿问题的。
- 最后，在“**动手实践**”部分，你将通过一系列精心设计的问题，亲手将理论知识转化为解决具体工程问题的实践技能。

让我们一同开启这段探索之旅，揭开动态系统内部运作的奥秘。

## 原理与机制

在上一章中，我们探讨了经典控制理论中[传递函数](@entry_id:273897)的局限性，特别是在处理多输入多输出（MIMO）系统、非零初始条件以及揭示系统内部动态特性方面的不足。为了克服这些限制，我们需要一个更强大、更通用的系统描述方法。[状态空间](@entry_id:177074)法 (State-Space Method) 应运而生，它不仅提供了对线性系统的深刻洞察，也为分析非线性系统和[时变系统](@entry_id:175653)奠定了基础。本章将深入探讨[状态空间表示](@entry_id:147149)的原理与核心机制。

### [状态空间表示](@entry_id:147149)

一个物理系统的**状态 (state)** 是一个最小的变量集合，其在时刻 $t_0$ 的值，连同在 $t \ge t_0$ 时间段内的输入，足以完全确定系统在所有 $t \ge t_0$ 时刻的行为。这个变量集合构成了**状态向量 (state vector)**，记为 $\mathbf{x}(t)$。[状态向量](@entry_id:154607)所在的[向量空间](@entry_id:151108)被称为**状态空间 (state space)**。从概念上讲，[状态向量](@entry_id:154607)在任意时刻捕捉了系统的全部“记忆”，包含了过去所有输入对系统影响的累积效应。例如，一个质点在直线上的运动状态可以由其位置和速度完全描述。

对于一个[线性时不变](@entry_id:276287)（LTI）系统，其动态行为可以用一组[一阶微分方程](@entry_id:173139)来描述，这组方程构成了**[状态空间表示](@entry_id:147149) (state-space representation)**：

$$
\begin{aligned}
\dot{\mathbf{x}}(t) = \mathbf{A}\mathbf{x}(t) + \mathbf{B}\mathbf{u}(t) \quad \text{(状态方程)} \\
\mathbf{y}(t) = \mathbf{C}\mathbf{x}(t) + \mathbf{D}\mathbf{u}(t) \quad \text{(输出方程)}
\end{aligned}
$$

其中：
- $\mathbf{x}(t) \in \mathbb{R}^n$ 是 $n$ 维的[状态向量](@entry_id:154607)。
- $\mathbf{u}(t) \in \mathbb{R}^m$ 是 $m$ 维的输入向量。
- $\mathbf{y}(t) \in \mathbb{R}^p$ 是 $p$ 维的输出向量。
- $\mathbf{A}$ 是 $n \times n$ 的**状态矩阵 (state matrix)**，它描述了系统内部状态之间的相互作用。$\mathbf{A}$ 的特性决定了系统的固有动态，例如稳定性。
- $\mathbf{B}$ 是 $n \times m$ 的**输入矩阵 (input matrix)**，它描述了外部输入如何影响系统的状态。
- $\mathbf{C}$ 是 $p \times n$ 的**输出矩阵 (output matrix)**，它描述了系统的内部状态如何组合形成可观测的输出。
- $\mathbf{D}$ 是 $p \times m$ 的**前馈矩阵 (feedthrough/direct transmission matrix)**，它描述了输入直接传递到输出的路径，绕过了状态变量。对于许多物理系统，$\mathbf{D}$ 是[零矩阵](@entry_id:155836)。

这四个矩阵 $(\mathbf{A}, \mathbf{B}, \mathbf{C}, \mathbf{D})$ 完全定义了一个 LTI 系统的动态特性。

### 建立[状态空间模型](@entry_id:137993)

将物理系统或其数学描述转换为状态空间形式是控制分析的第一步。这个过程可以从系统的物理定律出发，也可以从已知的[传递函数](@entry_id:273897)入手。

#### 从物理原理和[微分方程](@entry_id:264184)建立模型

最直接的方法是从描述系统动态的[一阶微分方程](@entry_id:173139)组中直接提取矩阵。

考虑一个单轴纳米定位平台，其动态行为可以通过[状态变量](@entry_id:138790) $x_1(t)$（平台位置）和 $x_2(t)$（与速度相关的量）以及控制输入电压 $u(t)$ 来描述。假设系统的内部关系在拉普拉斯域中由以下方程给出 [@problem_id:1614957]：
1.  $sX_1(s) = X_2(s)$
2.  $sX_2(s) = -a_0 X_1(s) - a_1 X_2(s) + b_0 U(s)$
3.  $Y(s) = X_1(s)$

利用拉普拉斯变换的[微分性质](@entry_id:275298) $\mathcal{L}\{\dot{x}(t)\} = sX(s)$（假设初始条件为零），我们可以将这些方程转换回时域：
1.  $\dot{x}_1(t) = x_2(t)$
2.  $\dot{x}_2(t) = -a_0 x_1(t) - a_1 x_2(t) + b_0 u(t)$
3.  $y(t) = x_1(t)$

现在，我们可以将这些[一阶微分方程](@entry_id:173139)写成标准的[状态方程](@entry_id:274378)形式 $\dot{\mathbf{x}} = \mathbf{A}\mathbf{x} + \mathbf{B}u$：
$$
\begin{pmatrix} \dot{x}_1(t) \\ \dot{x}_2(t) \end{pmatrix} = \begin{pmatrix} 0  1 \\ -a_0  -a_1 \end{pmatrix} \begin{pmatrix} x_1(t) \\ x_2(t) \end{pmatrix} + \begin{pmatrix} 0 \\ b_0 \end{pmatrix} u(t)
$$
同样，输出方程 $y = \mathbf{C}\mathbf{x} + \mathbf{D}u$ 变为：
$$
y(t) = \begin{pmatrix} 1  0 \end{pmatrix} \begin{pmatrix} x_1(t) \\ x_2(t) \end{pmatrix} + \begin{pmatrix} 0 \end{pmatrix} u(t)
$$
因此，该系统的状态空间矩阵为：
$$
\mathbf{A} = \begin{pmatrix} 0  1 \\ -a_0  -a_1 \end{pmatrix}, \quad \mathbf{B} = \begin{pmatrix} 0 \\ b_0 \end{pmatrix}, \quad \mathbf{C} = \begin{pmatrix} 1  0 \end{pmatrix}, \quad \mathbf{D} = \begin{pmatrix} 0 \end{pmatrix}
$$

当系统由一个[高阶微分方程](@entry_id:171249)描述时，我们可以通过一种系统性的方式选择状态变量，将其转换为[状态空间](@entry_id:177074)形式。一种常见的选择是**[相变](@entry_id:147324)量 (phase variables)**，即将输出及其各阶导数选为状态变量。这种方法得到的模型被称为**观测器规范型 (observer canonical form)**。

例如，考虑一个由三阶[微分方程](@entry_id:264184)描述的化学过程 [@problem_id:1614939]：
$$
\frac{d^3y}{dt^3} + 5 \frac{d^2y}{dt^2} + 8 \frac{dy}{dt} + 4y = 2u(t)
$$
我们选择状态变量为：
- $x_1 = y$ (输出本身)
- $x_2 = \dot{y}$ (输出的[一阶导数](@entry_id:749425))
- $x_3 = \ddot{y}$ (输出的[二阶导数](@entry_id:144508))

接下来，我们写出这些[状态变量](@entry_id:138790)的一阶导数：
- $\dot{x}_1 = \dot{y} = x_2$
- $\dot{x}_2 = \ddot{y} = x_3$
- $\dot{x}_3 = \frac{d^3y}{dt^3}$

为了得到 $\dot{x}_3$ 的表达式，我们重新整理原始的三阶[微分方程](@entry_id:264184)，将其最高阶导数移到等式左边：
$$
\frac{d^3y}{dt^3} = -4y - 8\frac{dy}{dt} - 5\frac{d^2y}{dt^2} + 2u(t)
$$
用状态变量替换 $y$ 及其导数，我们得到：
$$
\dot{x}_3 = -4x_1 - 8x_2 - 5x_3 + 2u(t)
$$
将这三个[一阶微分方程](@entry_id:173139)组合成矩阵形式，得到[状态方程](@entry_id:274378)：
$$
\begin{pmatrix} \dot{x}_1 \\ \dot{x}_2 \\ \dot{x}_3 \end{pmatrix} = \begin{pmatrix} 0  1  0 \\ 0  0  1 \\ -4  -8  -5 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \\ x_3 \end{pmatrix} + \begin{pmatrix} 0 \\ 0 \\ 2 \end{pmatrix} u(t)
$$
输出为 $y = x_1$，所以输出方程为：
$$
y(t) = \begin{pmatrix} 1  0  0 \end{pmatrix} \begin{pmatrix} x_1 \\ x_2 \\ x_3 \end{pmatrix} + \begin{pmatrix} 0 \end{pmatrix} u(t)
$$
这样，我们就得到了系统的观测器规范型[状态空间表示](@entry_id:147149)。

#### 从[传递函数](@entry_id:273897)建立模型

[状态空间表示](@entry_id:147149)与[传递函数](@entry_id:273897)表示之间存在着紧密的联系。我们同样可以从一个给定的[传递函数](@entry_id:273897)得到一个[状态空间实现](@entry_id:166670)。对于一个给定的[传递函数](@entry_id:273897)，存在无限多个等价的[状态空间表示](@entry_id:147149)。**控制器规范型 (controller canonical form)** 提供了一种直接的构造方法。

考虑一个由[传递函数](@entry_id:273897)描述的SISO系统 [@problem_id:1614923]：
$$
G(s) = \frac{Y(s)}{U(s)} = \frac{b_{n-1}s^{n-1} + \dots + b_1s + b_0}{s^n + a_{n-1}s^{n-1} + \dots + a_1s + a_0}
$$
其控制器规范型的状态空间矩阵为：
$$
\mathbf{A} = \begin{pmatrix}
0  1  0  \cdots  0 \\
0  0  1  \cdots  0 \\
\vdots  \vdots  \vdots  \ddots  \vdots \\
0  0  0  \cdots  1 \\
-a_0  -a_1  -a_2  \cdots  -a_{n-1}
\end{pmatrix}, \quad
\mathbf{B} = \begin{pmatrix} 0 \\ 0 \\ \vdots \\ 0 \\ 1 \end{pmatrix}
$$
$$
\mathbf{C} = \begin{pmatrix} b_0  b_1  \cdots  b_{n-1} \end{pmatrix}, \quad
\mathbf{D} = [d]
$$
其中 $d$ 是[传递函数](@entry_id:273897)中分子和分母多项式最高次幂相同时的系数比。如果分子阶数低于分母，则 $d=0$。

例如，对于[传递函数](@entry_id:273897) $G(s) = \frac{1}{s^3 + 3s^2 + 2s + 1}$：
我们识别出 $n=3$，分母系数为 $a_2=3, a_1=2, a_0=1$。分子为 $1$，所以分子系数为 $b_2=0, b_1=0, b_0=1$。
根据上述规则，矩阵 $\mathbf{A}$ 的最后一行由分母系数的负值构成，$\mathbf{B}$ 是一个在最后位置为1的列向量，$\mathbf{C}$ 由分子系数构成。因此：
$$
\mathbf{A} = \begin{pmatrix} 0  1  0 \\ 0  0  1 \\ -1  -2  -3 \end{pmatrix}, \quad
\mathbf{B} = \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix}, \quad
\mathbf{C} = \begin{pmatrix} 1  0  0 \end{pmatrix}, \quad
\mathbf{D} = [0]
$$
这种形式因其在[控制器设计](@entry_id:274982)中的便利性而得名。

### 从[状态空间到传递函数](@entry_id:268082)

反过来，我们也可以从一个[状态空间表示](@entry_id:147149) $(\mathbf{A}, \mathbf{B}, \mathbf{C}, \mathbf{D})$ 推导出其对应的[传递函数](@entry_id:273897)。我们对状态方程和输出方程进行拉普拉斯变换（假设[初始条件](@entry_id:152863)为零）：
$$
s\mathbf{X}(s) = \mathbf{A}\mathbf{X}(s) + \mathbf{B}\mathbf{U}(s)
$$
$$
\mathbf{Y}(s) = \mathbf{C}\mathbf{X}(s) + \mathbf{D}\mathbf{U}(s)
$$
从第一个方程中解出 $\mathbf{X}(s)$：
$$
s\mathbf{X}(s) - \mathbf{A}\mathbf{X}(s) = \mathbf{B}\mathbf{U}(s)
$$
$$
(s\mathbf{I} - \mathbf{A})\mathbf{X}(s) = \mathbf{B}\mathbf{U}(s)
$$
$$
\mathbf{X}(s) = (s\mathbf{I} - \mathbf{A})^{-1}\mathbf{B}\mathbf{U}(s)
$$
将 $\mathbf{X}(s)$ 的表达式代入输出方程：
$$
\mathbf{Y}(s) = \mathbf{C}(s\mathbf{I} - \mathbf{A})^{-1}\mathbf{B}\mathbf{U}(s) + \mathbf{D}\mathbf{U}(s) = [\mathbf{C}(s\mathbf{I} - \mathbf{A})^{-1}\mathbf{B} + \mathbf{D}]\mathbf{U}(s)
$$
[传递函数](@entry_id:273897)（或[传递函数矩阵](@entry_id:271746)）$\mathbf{G}(s)$ 定义为 $\mathbf{Y}(s) = \mathbf{G}(s)\mathbf{U}(s)$，因此我们得到核心关系式：
$$
\mathbf{G}(s) = \mathbf{C}(s\mathbf{I} - \mathbf{A})^{-1}\mathbf{B} + \mathbf{D}
$$
以一个SISO系统为例 [@problem_id:1614943]，其矩阵为：
$$
\mathbf{A} = \begin{bmatrix} -3  1 \\ 0  -2 \end{bmatrix}, \quad \mathbf{B} = \begin{bmatrix} 0 \\ 1 \end{bmatrix}, \quad \mathbf{C} = \begin{bmatrix} 1  0 \end{bmatrix}, \quad \mathbf{D} = [0]
$$
首先计算 $(s\mathbf{I} - \mathbf{A})$：
$$
s\mathbf{I} - \mathbf{A} = \begin{bmatrix} s  0 \\ 0  s \end{bmatrix} - \begin{bmatrix} -3  1 \\ 0  -2 \end{bmatrix} = \begin{bmatrix} s+3  -1 \\ 0  s+2 \end{bmatrix}
$$
然后求其逆矩阵：
$$
(s\mathbf{I} - \mathbf{A})^{-1} = \frac{1}{(s+3)(s+2)} \begin{bmatrix} s+2  1 \\ 0  s+3 \end{bmatrix} = \begin{bmatrix} \frac{1}{s+3}  \frac{1}{(s+3)(s+2)} \\ 0  \frac{1}{s+2} \end{bmatrix}
$$
最后，计算[传递函数](@entry_id:273897) $G(s)$：
$$
G(s) = \begin{bmatrix} 1  0 \end{bmatrix} \begin{bmatrix} \frac{1}{s+3}  \frac{1}{(s+3)(s+2)} \\ 0  \frac{1}{s+2} \end{bmatrix} \begin{bmatrix} 0 \\ 1 \end{bmatrix} + 0
$$
$$
G(s) = \begin{bmatrix} 1  0 \end{bmatrix} \begin{bmatrix} \frac{1}{(s+3)(s+2)} \\ \frac{1}{s+2} \end{bmatrix} = \frac{1}{(s+3)(s+2)} = \frac{1}{s^2 + 5s + 6}
$$
这个过程验证了状态空间模型和[传递函数](@entry_id:273897)模型之间的数学等价性。值得注意的是，[传递函数](@entry_id:273897)的分母的根（即[系统的极点](@entry_id:261618)）恰好是矩阵 $\mathbf{A}$ 的[特征值](@entry_id:154894)。

### [状态方程](@entry_id:274378)的解

理解状态空间模型的核心在于求解[状态方程](@entry_id:274378)，这能让我们预测系统在任意给定输入下的行为。

#### [状态转移矩阵](@entry_id:269075)

首先考虑没有输入的**[齐次系统](@entry_id:150411) (homogeneous system)**：
$$
\dot{\mathbf{x}}(t) = \mathbf{A}\mathbf{x}(t)
$$
给定初始状态 $\mathbf{x}(0)$，这个方程的解类似于标量情况下的 $x(t) = e^{at}x(0)$，其矩阵形式为：
$$
\mathbf{x}(t) = e^{\mathbf{A}t} \mathbf{x}(0)
$$
其中 $e^{\mathbf{A}t}$ 是**矩阵指数 (matrix exponential)**，定义为泰勒级数：
$$
e^{\mathbf{A}t} = \mathbf{I} + \mathbf{A}t + \frac{(\mathbf{A}t)^2}{2!} + \frac{(\mathbf{A}t)^3}{3!} + \dots = \sum_{k=0}^{\infty} \frac{(\mathbf{A}t)^k}{k!}
$$
这个矩阵 $e^{\mathbf{A}t}$ 被称为**[状态转移矩阵](@entry_id:269075) (state transition matrix)**，记为 $\boldsymbol{\Phi}(t)$。它将系统在时间 $0$ 的状态“转移”到时间 $t$ 的状态。它具有以下重要性质：
1. $\boldsymbol{\Phi}(0) = e^{\mathbf{A} \cdot 0} = \mathbf{I}$
2. $\frac{d}{dt}\boldsymbol{\Phi}(t) = \mathbf{A} e^{\mathbf{A}t} = \mathbf{A}\boldsymbol{\Phi}(t)$
3. $\boldsymbol{\Phi}(t_2 - t_1)$ 将状态从时间 $t_1$ 转移到 $t_2$：$\mathbf{x}(t_2) = \boldsymbol{\Phi}(t_2 - t_1) \mathbf{x}(t_1)$
4. $\boldsymbol{\Phi}^{-1}(t) = \boldsymbol{\Phi}(-t) = e^{-\mathbf{A}t}$

计算[状态转移矩阵](@entry_id:269075)是分析系统动态的关键。对于某些特殊结构的矩阵 $\mathbf{A}$，计算可以简化。例如，考虑一个描述微型卫星姿态阻尼模式的系统，其状态矩阵为一个约旦块 [@problem_id:1614977]：
$$
\mathbf{A} = \begin{bmatrix} -a  1 \\ 0  -a \end{bmatrix}
$$
我们可以将 $\mathbf{A}$ 分解为 $\mathbf{A} = -a\mathbf{I} + \mathbf{N}$，其中 $\mathbf{N} = \begin{pmatrix} 0  1 \\ 0  0 \end{pmatrix}$。由于 $-a\mathbf{I}$ 与 $\mathbf{N}$ 可交换（即 $(-a\mathbf{I})\mathbf{N} = \mathbf{N}(-a\mathbf{I})$），我们可以使用性质 $e^{(\mathbf{X}+\mathbf{Y})t} = e^{\mathbf{X}t}e^{\mathbf{Y}t}$。
$$
e^{\mathbf{A}t} = e^{(-a\mathbf{I} + \mathbf{N})t} = e^{-a\mathbf{I}t} e^{\mathbf{N}t}
$$
其中 $e^{-a\mathbf{I}t} = e^{-at}\mathbf{I}$。矩阵 $\mathbf{N}$ 是一个**[幂零矩阵](@entry_id:152732) (nilpotent matrix)**，因为 $\mathbf{N}^2 = \mathbf{0}$。这意味着其指数级数会很快截断：
$$
e^{\mathbf{N}t} = \mathbf{I} + \mathbf{N}t + \frac{(\mathbf{N}t)^2}{2!} + \dots = \mathbf{I} + \mathbf{N}t = \begin{pmatrix} 1  t \\ 0  1 \end{pmatrix}
$$
因此，[状态转移矩阵](@entry_id:269075)为：
$$
\boldsymbol{\Phi}(t) = e^{\mathbf{A}t} = (e^{-at}\mathbf{I})(\mathbf{I} + \mathbf{N}t) = e^{-at} \begin{pmatrix} 1  t \\ 0  1 \end{pmatrix} = \begin{pmatrix} e^{-at}  te^{-at} \\ 0  e^{-at} \end{pmatrix}
$$

#### 完整解

对于包含输入的**非[齐次系统](@entry_id:150411) (non-homogeneous system)** $\dot{\mathbf{x}}(t) = \mathbf{A}\mathbf{x}(t) + \mathbf{B}\mathbf{u}(t)$，我们可以使用**[常数变易法](@entry_id:756435) (variation of constants)** 来求其完整解。其最终形式，也被称为**柯西公式 (Cauchy's formula)**，给出了[状态向量](@entry_id:154607)的完整时间演化 [@problem_id:1614961]：
$$
\mathbf{x}(t) = e^{\mathbf{A}t}\mathbf{x}_0 + \int_{0}^{t} e^{\mathbf{A}(t-\tau)}\mathbf{B}\mathbf{u}(\tau) d\tau
$$
这个解由两部分组成，体现了线性系统的[叠加原理](@entry_id:144649)：
1.  **[零输入响应](@entry_id:274925) (Zero-Input Response)**：$e^{\mathbf{A}t}\mathbf{x}_0$。这是系统在没有外部输入时，仅由初始状态 $\mathbf{x}_0$ 引起的响应。它描述了系统的“自然”行为。
2.  **[零状态响应](@entry_id:273280) (Zero-State Response)**：$\int_{0}^{t} e^{\mathbf{A}(t-\tau)}\mathbf{B}\mathbf{u}(\tau) d\tau$。这是系统在初始状态为零时，完全由输入 $\mathbf{u}(t)$ 引起的响应。这是一个[卷积积分](@entry_id:155865)，表示在过去每个时刻 $\tau$ 的输入 $\mathbf{u}(\tau)$ 通过 $\mathbf{B}$ 作用于系统，其影响经过 $t-\tau$ 时间的“转移”后，在当前时刻 $t$ 的累积效应。

这个公式是[LTI系统理论](@entry_id:178867)的基石，它将系统的响应明确地分解为与初始条件相关的[部分和](@entry_id:162077)与输入相关的部分。

### 基本系统性质

[状态空间表示](@entry_id:147149)不仅便于求解，更重要的是它能揭示系统的三个基本性质：稳定性、能控性和能观性。

#### 稳定性

系统的**稳定性 (stability)** 是指当系统受到扰动偏离其[平衡点](@entry_id:272705)后，能否自行恢复到[平衡点](@entry_id:272705)。对于[LTI系统](@entry_id:271946) $\dot{\mathbf{x}} = \mathbf{A}\mathbf{x}$，[平衡点](@entry_id:272705)是 $\mathbf{x} = \mathbf{0}$。稳定性完全由状态矩阵 $\mathbf{A}$ 的**[特征值](@entry_id:154894) (eigenvalues)** 决定。
系统的[零输入响应](@entry_id:274925)为 $\mathbf{x}(t) = e^{\mathbf{A}t}\mathbf{x}(0)$。当 $t \to \infty$ 时，如果 $\mathbf{x}(t) \to \mathbf{0}$，则系统是稳定的。$e^{\mathbf{A}t}$ 的行为与 $\mathbf{A}$ 的[特征值](@entry_id:154894) $\lambda_i$ 直接相关。

-   **渐近稳定 (Asymptotically Stable)**：如果 $\mathbf{A}$ 的所有[特征值](@entry_id:154894)的实部都严格为负（即 $\text{Re}(\lambda_i) \lt 0$），则对于任何初始条件，状态都会收敛到零。
-   **不稳定 (Unstable)**：如果 $\mathbf{A}$ 至少有一个[特征值](@entry_id:154894)的实部为正（$\text{Re}(\lambda_i) \gt 0$），或者存在实部为零的重根[特征值](@entry_id:154894)，则状态通常会发散。
-   **[临界稳定](@entry_id:147657) (Marginally Stable)**：如果 $\mathbf{A}$ 没有实部为正的[特征值](@entry_id:154894)，但至少有一个实部为零的非[重根](@entry_id:151486)[特征值](@entry_id:154894)，则状态既不收敛到零也不发散，而是会保持[振荡](@entry_id:267781)或停留在某个非零值。

例如，一个由矩阵 $A = \begin{bmatrix} 0  1 \\ -8  -6 \end{bmatrix}$ 描述的系统 [@problem_id:1614921]，其稳定性可以通过计算[特征值](@entry_id:154894)来判断。特征方程为：
$$
\det(\lambda\mathbf{I} - \mathbf{A}) = \det\begin{pmatrix} \lambda  -1 \\ 8  \lambda+6 \end{pmatrix} = \lambda(\lambda+6) - (-1)(8) = \lambda^2 + 6\lambda + 8 = 0
$$
解得[特征值](@entry_id:154894)为 $\lambda_1 = -2$ 和 $\lambda_2 = -4$。由于两个[特征值](@entry_id:154894)的实部都严格为负，该系统是**渐近稳定**的。

#### 能控性

**能控性 (Controllability)** 回答了一个根本问题：我们是否能够通过选择合适的控制输入 $\mathbf{u}(t)$，在有限时间内将系统从任意初始状态 $\mathbf{x}(0)$ 驱动到任意期望的最终状态 $\mathbf{x}(t_f)$？如果可以，则系统是**完全状态能控的 (completely state controllable)**。

对于[LTI系统](@entry_id:271946)，能控性可以通过**卡尔曼能控性判据 (Kalman's rank condition for controllability)** 来检验。系统 $(\mathbf{A}, \mathbf{B})$ 是能控的，当且仅当其 $n \times nm$ 的**能控性矩阵 (controllability matrix)** $\mathcal{C}$ 的秩为 $n$（即满秩）：
$$
\mathcal{C} = \begin{pmatrix} \mathbf{B}  \mathbf{A}\mathbf{B}  \mathbf{A}^2\mathbf{B}  \cdots  \mathbf{A}^{n-1}\mathbf{B} \end{pmatrix}
$$
$$
\text{rank}(\mathcal{C}) = n
$$

能控性是一个结构性属性。如果系统不能控，意味着存在某些状态或状态的组合是输入无法影响的。例如，考虑一个简化的[卫星姿态控制](@entry_id:270670)模型 [@problem_id:1614945]，其中 $A = \begin{bmatrix} 0  1  0 \\ 0  0  0 \\ 0  0  0 \end{bmatrix}$ 和 $B = \begin{bmatrix} 0 \\ -\alpha \\ 1 \end{bmatrix}$。状态方程为 $\dot{x}_1 = x_2, \dot{x}_2 = -\alpha u, \dot{x}_3 = u$。
其能控性矩阵为：
$$
\mathcal{C} = \begin{bmatrix} \mathbf{B}  \mathbf{A}\mathbf{B}  \mathbf{A}^2\mathbf{B} \end{bmatrix} = \begin{bmatrix} 0  -\alpha  0 \\ -\alpha  0  0 \\ 1  0  0 \end{bmatrix}
$$
由于第三列是[零向量](@entry_id:156189)，该[矩阵的秩](@entry_id:155507)最多为2。因为 $n=3$，所以 $\text{rank}(\mathcal{C}) = 2 \lt 3$，系统是**不能控的**。

从物理上看，这意味着存在一个不受控制输入 $u(t)$ 影响的状态组合。考察状态量 $x_2 + \alpha x_3$ 的导数：
$$
\frac{d}{dt}(x_2 + \alpha x_3) = \dot{x}_2 + \alpha \dot{x}_3 = -\alpha u + \alpha u = 0
$$
这表明 $x_2(t) + \alpha x_3(t)$ 是一个[守恒量](@entry_id:150267)，其值仅由初始状态决定，任何控制输入都无法改变它。因此，我们无法将系统驱动到任意一个最终状态，而只能到达那些满足 $x_{2,f} + \alpha x_{3,f} = x_{2,0} + \alpha x_{3,0}$ 的状态。

#### 能观性

**能观性 (Observability)** 是能控性的对偶概念。它回答了另一个根本问题：我们是否能够通过在有限时间区间 $[0, t_f]$ 内观测系统的输出 $\mathbf{y}(t)$，来唯一地确定系统的初始状态 $\mathbf{x}(0)$？如果可以，则系统是**完全状态能观的 (completely state observable)**。

如果一个系统不能观，意味着存在某些内部状态或运动模式，它们不会对输出产生任何影响，就像是“隐藏”在系统内部一样。
同样，能观性也可以通过**卡尔曼能观性判据 (Kalman's rank condition for observability)** 来检验。系统 $(\mathbf{A}, \mathbf{C})$ 是能观的，当且仅当其 $np \times n$ 的**能观性矩阵 (observability matrix)** $\mathcal{O}$ 的秩为 $n$（即满秩）：
$$
\mathcal{O} = \begin{pmatrix} \mathbf{C} \\ \mathbf{C}\mathbf{A} \\ \mathbf{C}\mathbf{A}^2 \\ \vdots \\ \mathbf{C}\mathbf{A}^{n-1} \end{pmatrix}
$$
$$
\text{rank}(\mathcal{O}) = n
$$

考虑一个双弹簧质量系统 [@problem_id:1614927]，其输出由一个传感器测量，该传感器测量两个质量块位置的线性组合 $y(t) = x_1(t) - \gamma x_2(t)$。系统的某个[振动](@entry_id:267781)模式（对应一个自然频率和模态振型）如果不能被传感器观测到，就意味着该模式是**不能观的**。这种情况发生在该模式的[振型](@entry_id:179030)向量 $\mathbf{v}$ 恰好位于输出矩阵 $\mathbf{C}$ 的零空间中，即 $\mathbf{C}\mathbf{v} = 0$。对于这个例子，$\mathbf{C} = \begin{pmatrix} 1  -\gamma \end{pmatrix}$（如果我们只考虑位置状态），而 $\mathbf{v} = \begin{pmatrix} v_1 \\ v_2 \end{pmatrix}$ 是模态振型。不能观的条件是 $v_1 - \gamma v_2 = 0$，即 $\gamma = v_1/v_2$。通过计算系统的模态振型，可以找到一个特定的传感器参数 $\gamma$ 值，使得某个特定的[振动](@entry_id:267781)模式对输出“隐形”，从而导致系统不能观。这揭示了[传感器布局](@entry_id:754692)（由矩阵 $\mathbf{C}$ 决定）对系统能观性的关键作用。

### 状态变换与非唯一性

一个重要的事实是，一个物理系统的[状态空间表示](@entry_id:147149)不是唯一的。我们可以通过一个可逆的[线性变换](@entry_id:149133) $\mathbf{T}$ 来选择一组新的[状态变量](@entry_id:138790) $\mathbf{z}(t)$，定义为 $\mathbf{z} = \mathbf{T}\mathbf{x}$。原始状态 $\mathbf{x}$ 可以表示为 $\mathbf{x} = \mathbf{T}^{-1}\mathbf{z}$。

将这个关系代入原始的[状态空间](@entry_id:177074)方程，我们可以推导出在新[坐标系](@entry_id:156346)下的系统矩阵 $(\mathbf{A}_z, \mathbf{B}_z, \mathbf{C}_z, \mathbf{D}_z)$ [@problem_id:1614950]：
$$
\dot{\mathbf{z}} = \mathbf{T}\dot{\mathbf{x}} = \mathbf{T}(\mathbf{A}\mathbf{x} + \mathbf{B}u) = \mathbf{T}\mathbf{A}(\mathbf{T}^{-1}\mathbf{z}) + \mathbf{T}\mathbf{B}u
$$
$$
y = \mathbf{C}\mathbf{x} + \mathbf{D}u = \mathbf{C}(\mathbf{T}^{-1}\mathbf{z}) + \mathbf{D}u
$$
因此，新的[状态空间表示](@entry_id:147149)为：
$$
\dot{\mathbf{z}} = \mathbf{A}_z \mathbf{z} + \mathbf{B}_z u, \quad y = \mathbf{C}_z \mathbf{z} + \mathbf{D}_z u
$$
其中：
$$
\mathbf{A}_z = \mathbf{T}\mathbf{A}\mathbf{T}^{-1}, \quad \mathbf{B}_z = \mathbf{T}\mathbf{B}, \quad \mathbf{C}_z = \mathbf{C}\mathbf{T}^{-1}, \quad \mathbf{D}_z = \mathbf{D}
$$
这种变换被称为**[相似变换](@entry_id:152935) (similarity transformation)**。

虽然[状态空间表示](@entry_id:147149)改变了，但系统的外部行为和基本属性保持不变。例如，新系统的[传递函数](@entry_id:273897)为：
$$
G_z(s) = \mathbf{C}_z(s\mathbf{I} - \mathbf{A}_z)^{-1}\mathbf{B}_z + \mathbf{D}_z = (\mathbf{C}\mathbf{T}^{-1})(s\mathbf{I} - \mathbf{T}\mathbf{A}\mathbf{T}^{-1})^{-1}(\mathbf{T}\mathbf{B}) + \mathbf{D}
$$
利用 $(s\mathbf{I} - \mathbf{T}\mathbf{A}\mathbf{T}^{-1}) = \mathbf{T}(s\mathbf{I} - \mathbf{A})\mathbf{T}^{-1}$ 和 $(\mathbf{XYZ})^{-1} = \mathbf{Z}^{-1}\mathbf{Y}^{-1}\mathbf{X}^{-1}$，上式简化为：
$$
G_z(s) = (\mathbf{C}\mathbf{T}^{-1})(\mathbf{T}(s\mathbf{I} - \mathbf{A})^{-1}\mathbf{T}^{-1})(\mathbf{T}\mathbf{B}) + \mathbf{D} = \mathbf{C}(s\mathbf{I} - \mathbf{A})^{-1}\mathbf{B} + \mathbf{D} = G(s)
$$
这表明[传递函数](@entry_id:273897)在状态变换下是不变的。同样，系统的[特征值](@entry_id:154894)（决定稳定性）、能控性和能观性等内在属性在相似变换下也保持不变。

选择合适的坐标变换可以极大地简化[系统分析](@entry_id:263805)。一个特别有用的变换是将状态矩阵 $\mathbf{A}$ [对角化](@entry_id:147016)。如果 $\mathbf{A}$ 有一组[线性无关](@entry_id:148207)的[特征向量](@entry_id:151813)，我们可以选择变换矩阵 $\mathbf{T}$ 为由[特征向量](@entry_id:151813)构成的矩阵的逆，从而使得新的状态矩阵 $\mathbf{A}_z = \mathbf{T}\mathbf{A}\mathbf{T}^{-1}$ 成为一个[对角矩阵](@entry_id:637782)，其对角[线元](@entry_id:196833)素就是 $\mathbf{A}$ 的[特征值](@entry_id:154894)。在这种**对角规范型 (diagonal canonical form)**下，状态方程变为一组解耦的[一阶微分方程](@entry_id:173139)，使得[系统分析](@entry_id:263805)变得异常简单。

例如，对于系统 $\mathbf{A} = \begin{pmatrix} 0  1 \\ -6  -5 \end{pmatrix}$，其[特征值](@entry_id:154894)为 $-2$ 和 $-3$。通过选择特定的[变换矩阵](@entry_id:151616) $\mathbf{T} = \begin{pmatrix} 2  1 \\ 3  1 \end{pmatrix}$，新的状态矩阵被[对角化](@entry_id:147016)为 $\mathbf{A}_z = \begin{pmatrix} -3  0 \\ 0  -2 \end{pmatrix}$ [@problem_id:1614950]。

本章介绍了[状态空间](@entry_id:177074)方法的基本框架，从模型的建立到方程的求解，再到系统核心性质的分析。[状态空间](@entry_id:177074)提供了一个统一而深刻的视角来理解动态系统，为下一章将要学习的现代控制设计技术奠定了坚实的理论基础。