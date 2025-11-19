## 引言
在现代工程与科学领域，理解和控制动态系统的行为至关重要。传统的分析方法，如[传递函数](@entry_id:273897)，虽然在处理单输入单输出（SISO）[线性时不变](@entry_id:276287)（LTI）系统时非常有效，但在面对更复杂的现实世界问题——如多输入多输出（MIMO）系统、[时变系统](@entry_id:175653)或需要洞察系统内部状态的场景时，则显得力不从心。为了克服这些局限性，现代控制理论引入了一种更为强大和通用的工具：**[状态空间表示](@entry_id:147149)法**。

本文旨在为读者提供一个关于[连续时间系统](@entry_id:276553)[状态空间表示](@entry_id:147149)的全面而深入的介绍。我们将不再仅仅关注系统的输入与输出之间的关系，而是深入其“内部”，通过一组[一阶微分方程](@entry_id:173139)来揭示系统动态的完整图景。通过学习本文，你将掌握一种能够统一描述从电路、机械臂到生态种群等各类动态系统的数学语言。

为实现这一目标，本文将分为三个核心部分：
*   在“**原理与机制**”一章中，我们将建立[状态空间模型](@entry_id:137993)的数学基础，学习如何定义[状态变量](@entry_id:138790)和系统矩阵，并探讨其与经典[传递函数](@entry_id:273897)表示之间的转换关系。此外，我们还将深入研究稳定性、可控性和可观性等决定系统本质行为的关键概念。
*   在“**应用与交叉学科联系**”一章中，我们将展示[状态空间](@entry_id:177074)方法的广泛适用性，通过实例探讨其在电气工程、[机械系统](@entry_id:271215)、[过程控制](@entry_id:271184)乃至生物学和机器学习等不同领域的具体应用，彰显其作为统一分析框架的强大能力。
*   最后，“**动手实践**”部分将提供一系列精心设计的问题，帮助你巩固所学理论，将抽象的矩阵运算转化为解决实际[系统分析](@entry_id:263805)问题的技能。

现在，让我们一起踏上这段旅程，从构建[状态空间](@entry_id:177074)的基本方程开始，逐步揭开其背后的深刻原理与广阔应用。

## 原理与机制

在上一章中，我们介绍了[系统建模](@entry_id:197208)的多种方法。本章将深入探讨一种功能强大且应用广泛的现代控制理论核心工具——**[状态空间表示](@entry_id:147149)法 (State-Space Representation)**。与侧重于输入-输出关系的经典[传递函数](@entry_id:273897)方法不同，[状态空间](@entry_id:177074)法通过一组[一阶微分方程](@entry_id:173139)来描述系统的内部动态，从而为我们提供了一个更全面、更深刻的系统视角。这种方法不仅适用于线性和非线性系统、时变和非[时变系统](@entry_id:175653)，还能轻松处理多输入多输出（MIMO）问题，为[系统分析](@entry_id:263805)与设计提供了坚实的数学基础。

### [状态空间模型](@entry_id:137993)的定义

一个连续时间、[线性时不变](@entry_id:276287)（LTI）系统可以用以下一组标准方程来描述：

$$
\dot{\mathbf{x}}(t) = A\mathbf{x}(t) + B\mathbf{u}(t) \quad \text{(状态方程)}
$$

$$
\mathbf{y}(t) = C\mathbf{x}(t) + D\mathbf{u}(t) \quad \text{(输出方程)}
$$

这组方程构成了系统的**状态空间模型**。让我们逐一解析其中的关键元素：

*   **状态向量 (State Vector)** $\mathbf{x}(t)$：这是一个列向量，其元素 $x_1(t), x_2(t), \dots, x_n(t)$ 被称为**状态变量 (state variables)**。[状态向量](@entry_id:154607)包含了在任意时刻 $t_0$ 描述系统内部状态所需的最少信息量。换言之，只要我们知道了 $t_0$ 时刻的[状态向量](@entry_id:154607) $\mathbf{x}(t_0)$ 以及从 $t_0$ 开始施加的输入 $\mathbf{u}(t)$，我们就能完全确定系统在所有未来时刻 $t > t_0$ 的行为。因此，状态向量可以被视为系统动态的“记忆”。

*   **输入向量 (Input Vector)** $\mathbf{u}(t)$：这个向量包含了所有作用于系统的外部输入或控制信号。

*   **输出向量 (Output Vector)** $\mathbf{y}(t)$：这个向量代表了我们能够测量或感兴趣的系统变量。

*   **系统矩阵 (System Matrices)**：
    *   $A$ 是 $n \times n$ 的**状态矩阵 (state matrix)**，它描述了系统内部状态变量之间的相互作用和耦合关系。$A$ 的特性决定了系统在没有外部输入时的自然响应行为。
    *   $B$ 是 $n \times p$ 的**输入矩阵 (input matrix)**，它决定了外部输入 $\mathbf{u}(t)$如何影响系统中的每一个[状态变量](@entry_id:138790)。
    *   $C$ 是 $q \times n$ 的**输出矩阵 (output matrix)**，它描述了如何从内部状态变量 $\mathbf{x}(t)$ 组合得到可观测的输出 $\mathbf{y}(t)$。
    *   $D$ 是 $q \times p$ 的**前馈矩阵 (feedthrough matrix)** 或**直通矩阵 (direct transmission matrix)**，它表示了输入 $\mathbf{u}(t)$ 对输出 $\mathbf{y}(t)$ 的瞬时直接影响。对于许多物理系统，输入需要经过系统的动态过程才能影响输出，因此 $D$ 矩阵通常为零矩阵。

为了将这些抽象概念具体化，让我们考虑一个经典的物理系统：弹簧-质量-阻尼系统 [@problem_id:1754992]。该系统由质量为 $m$ 的物体、[弹性系数](@entry_id:192914)为 $k$ 的弹簧和[阻尼系数](@entry_id:163719)为 $b$ 的阻尼器组成。选择系统的状态变量是建立模型的关键第一步。一个自然的选择是能够描述系统能量存储的变量。在这里，我们可以选择物体的位移 $p(t)$（与弹簧存储的[势能](@entry_id:748988)相关）和动量 $q(t)$（与物体携带的动能相关）作为状态变量。因此，[状态向量](@entry_id:154607)为 $\mathbf{x}(t) = \begin{pmatrix} p(t) \\ q(t) \end{pmatrix}$。

根据物理定律，我们有：
1.  位移的变化率是速度：$\dot{p}(t) = v(t)$。而速度与动量的关系是 $v(t) = q(t)/m$。
2.  根据[牛顿第二定律](@entry_id:274217)，动量的变化率等于物体所受的合外力。这里，合外力是弹簧的恢复力 $F_s = -kp(t)$ 和阻尼器的阻尼力 $F_d = -bv(t) = -b\frac{q(t)}{m}$ 之和。

将这些关系整理成[状态方程](@entry_id:274378)的形式：
$$
\dot{p}(t) = (0)p(t) + \frac{1}{m}q(t)
$$
$$
\dot{q}(t) = -kp(t) - \frac{b}{m}q(t)
$$

写成矩阵形式 $\dot{\mathbf{x}}(t) = A\mathbf{x}(t)$，我们得到状态矩阵 $A$：
$$
A = \begin{pmatrix} 0  \frac{1}{m} \\ -k  -\frac{b}{m} \end{pmatrix}
$$
这个例子清晰地展示了状态矩阵 $A$ 的元素是如何由系统的内在物理参数（$m, k, b$）决定的。矩阵的每一项都代表了[状态变量](@entry_id:138790)之间动态关系的特定方面。

### 不同表示间的转换

状态空间模型与我们之前学习的[传递函数](@entry_id:273897)或[高阶微分方程](@entry_id:171249)之间存在着紧密的联系。它们只是描述同一个系统动态特性的不同数学语言。

#### 从[状态空间到传递函数](@entry_id:268082)

对于一个由 $(A, B, C, D)$ 定义的单输入单输出（SISO）[LTI系统](@entry_id:271946)，其[传递函数](@entry_id:273897) $H(s) = Y(s)/U(s)$ 可以通过对[状态方程](@entry_id:274378)和输出方程进行[拉普拉斯变换](@entry_id:159339)来推导。假设系统的初始状态为零，即 $\mathbf{x}(0) = \mathbf{0}$。

对[状态方程](@entry_id:274378) $\dot{\mathbf{x}}(t) = A\mathbf{x}(t) + B u(t)$ 进行拉普拉斯变换，得到：
$$
s\mathbf{X}(s) - \mathbf{x}(0) = A\mathbf{X}(s) + B U(s)
$$
由于 $\mathbf{x}(0)=\mathbf{0}$，上式简化为：
$$
s\mathbf{X}(s) - A\mathbf{X}(s) = B U(s) \implies (sI - A)\mathbf{X}(s) = B U(s)
$$
其中 $I$ 是单位矩阵。求解 $\mathbf{X}(s)$，我们得到：
$$
\mathbf{X}(s) = (sI - A)^{-1}B U(s)
$$
接着，对输出方程 $y(t) = C\mathbf{x}(t) + D u(t)$ 进行拉普拉斯变换：
$$
Y(s) = C\mathbf{X}(s) + D U(s)
$$
将上面求得的 $\mathbf{X}(s)$ 表达式代入，得到：
$$
Y(s) = C(sI - A)^{-1}B U(s) + D U(s) = [C(sI - A)^{-1}B + D] U(s)
$$
由此，我们得到了从[状态空间表示](@entry_id:147149)到[传递函数](@entry_id:273897)的关键转换公式：
$$
H(s) = C(sI - A)^{-1}B + D
$$

举例来说，考虑一个系统由以下矩阵定义 [@problem_id:1755017]：
$$
A = \begin{pmatrix} 0  1 \\ -2  -3 \end{pmatrix}, \quad B = \begin{pmatrix} 0 \\ 1 \end{pmatrix}, \quad C = \begin{pmatrix} 1  1 \end{pmatrix}, \quad D = [2]
$$
首先计算 $(sI-A)^{-1}$：
$$
sI - A = \begin{pmatrix} s  -1 \\ 2  s+3 \end{pmatrix}
$$
其[行列式](@entry_id:142978)为 $\det(sI-A) = s(s+3) - (-1)(2) = s^2 + 3s + 2 = (s+1)(s+2)$。
逆矩阵为：
$$
(sI-A)^{-1} = \frac{1}{s^2+3s+2} \begin{pmatrix} s+3  1 \\ -2  s \end{pmatrix}
$$
然后计算 $C(sI-A)^{-1}B$：
$$
C(sI-A)^{-1}B = \begin{pmatrix} 1  1 \end{pmatrix} \frac{1}{s^2+3s+2} \begin{pmatrix} s+3  1 \\ -2  s \end{pmatrix} \begin{pmatrix} 0 \\ 1 \end{pmatrix} = \frac{1}{s^2+3s+2} \begin{pmatrix} 1  1 \end{pmatrix} \begin{pmatrix} 1 \\ s \end{pmatrix} = \frac{s+1}{s^2+3s+2}
$$
最后加上直通项 $D$：
$$
H(s) = \frac{s+1}{s^2+3s+2} + 2 = \frac{s+1 + 2(s^2+3s+2)}{s^2+3s+2} = \frac{2s^2+7s+5}{s^2+3s+2}
$$
因式分解后，我们发现一个有趣的现象：
$$
H(s) = \frac{(2s+5)(s+1)}{(s+2)(s+1)} = \frac{2s+5}{s+2}
$$
这是一个**极点-零点对消 (pole-zero cancellation)** 的例子。虽然状态空间模型是二阶的（$A$ 是 $2 \times 2$ 矩阵），但其输入-输出行为可以用一个一阶[传递函数](@entry_id:273897)来描述。这暗示了系统内部存在一个“隐藏”的动态模式，我们将在稍后讨论[可控性](@entry_id:148402)和可观性时深入探讨这一点。

#### 从[状态空间](@entry_id:177074)到输入-输出[微分方程](@entry_id:264184)

反向转换，即从[状态空间模型](@entry_id:137993)得到一个高阶输入-输出[微分方程](@entry_id:264184)，同样是可行的。这通常通过对状态变量进行[微分](@entry_id:158718)和代数代换来实现。考虑一个二阶系统 [@problem_id:1754972]：
$$
A = \begin{pmatrix} -1  -2 \\ 3  -7 \end{pmatrix}, \quad B = \begin{pmatrix} 1 \\ 1 \end{pmatrix}, \quad C = \begin{pmatrix} 1  0 \end{pmatrix}, \quad D = 0
$$
其[状态方程](@entry_id:274378)为：
$$
\dot{x}_1 = -x_1 - 2x_2 + u
$$
$$
\dot{x}_2 = 3x_1 - 7x_2 + u
$$
输出方程为 $y = x_1$。我们的目标是找到一个只包含 $y$ 和 $u$ 及其导数的方程。
由于 $y=x_1$，我们可以将状态方程中的 $x_1$ 都替换为 $y$：
$$
\dot{y} = -y - 2x_2 + u \quad (1)
$$
$$
\dot{x}_2 = 3y - 7x_2 + u \quad (2)
$$
从方程(1)中，我们可以解出 $x_2$：
$$
x_2 = \frac{1}{2}(-\dot{y} - y + u)
$$
对上式求导，得到 $\dot{x}_2$：
$$
\dot{x}_2 = \frac{1}{2}(-\ddot{y} - \dot{y} + \dot{u})
$$
将这两个关于 $x_2$ 和 $\dot{x}_2$ 的表达式代入方程(2)，以消去 $x_2$：
$$
\frac{1}{2}(-\ddot{y} - \dot{y} + \dot{u}) = 3y - 7 \left( \frac{1}{2}(-\dot{y} - y + u) \right) + u
$$
乘以2并整理各项：
$$
-\ddot{y} - \dot{y} + \dot{u} = 6y + 7\dot{y} + 7y - 7u + 2u
$$
$$
-\ddot{y} - 8\dot{y} - 13y = -\dot{u} - 5u
$$
最后，将所有项移到一边，得到标准的[微分方程](@entry_id:264184)形式：
$$
\ddot{y} + 8\dot{y} + 13y = \dot{u} + 5u
$$
这个过程清楚地表明，[状态空间表示](@entry_id:147149)和[高阶微分方程](@entry_id:171249)是描述同一系统动态的等价方式。

### 系统的实现：从[传递函数](@entry_id:273897)到[状态空间](@entry_id:177074)

与[状态空间到传递函数](@entry_id:268082)的唯一映射不同，从一个给定的[传递函数](@entry_id:273897)到[状态空间表示](@entry_id:147149)的转换（称为**系统实现 (realization)**）不是唯一的。对于同一个[传递函数](@entry_id:273897)，存在无限多种[状态空间表示](@entry_id:147149)方法。然而，我们可以采用一些[标准化](@entry_id:637219)的实现方法，即**标准型 (canonical forms)**。

#### [可控标准型](@entry_id:165254)

**[可控标准型](@entry_id:165254) (Controllable Canonical Form)** 是一种常用的实现方法。对于一个 $n$ 阶、严格真分（分子阶数小于分母阶数）的[传递函数](@entry_id:273897)：
$$
H(s) = \frac{b_{n-1}s^{n-1} + \dots + b_1s + b_0}{s^n + a_{n-1}s^{n-1} + \dots + a_1s + a_0}
$$
其[可控标准型](@entry_id:165254)的状态空间矩阵 $(A, B, C, D)$ 具有非常规则的结构：
$$
A = \begin{pmatrix}
0  1  0  \cdots  0 \\
0  0  1  \cdots  0 \\
\vdots  \vdots  \vdots  \ddots  \vdots \\
0  0  0  \cdots  1 \\
-a_0  -a_1  -a_2  \cdots  -a_{n-1}
\end{pmatrix}, \quad
B = \begin{pmatrix} 0 \\ 0 \\ \vdots \\ 0 \\ 1 \end{pmatrix}
$$
$$
C = \begin{pmatrix} b_0  b_1  b_2  \cdots  b_{n-1} \end{pmatrix}, \quad
D = 0
$$
观察矩阵 $A$ 的结构：除了最后一行和主对角线上方的一条斜线为1外，其余元素均为0。最后一行由[传递函数](@entry_id:273897)分母多项式的系数（取负号）构成。矩阵 $B$ 非常简单，只有一个非零元素。矩阵 $C$ 的元素则直接由分子多项式的系数构成。

例如，对于[传递函数](@entry_id:273897) [@problem_id:1754994]：
$$
H(s) = \frac{2s^2 + 5s + 3}{s^3 + 6s^2 + 11s + 4}
$$
这是一个三阶系统（$n=3$）。我们首先识别出系数：
分母系数：$a_2 = 6, a_1 = 11, a_0 = 4$
分子系数：$b_2 = 2, b_1 = 5, b_0 = 3$
由于分子阶数（2）小于分母阶数（3），系统是严格真的，因此 $D=0$。
直接套用[可控标准型](@entry_id:165254)的公式，我们得到：
$$
A = \begin{pmatrix} 0  1  0 \\ 0  0  1 \\ -a_0  -a_1  -a_2 \end{pmatrix} = \begin{pmatrix} 0  1  0 \\ 0  0  1 \\ -4  -11  -6 \end{pmatrix}
$$
$$
B = \begin{pmatrix} 0 \\ 0 \\ 1 \end{pmatrix}, \quad C = \begin{pmatrix} b_0  b_1  b_2 \end{pmatrix} = \begin{pmatrix} 3  5  2 \end{pmatrix}, \quad D = 0
$$
这种“照章办事”的构建方法使得从[传递函数](@entry_id:273897)到[状态空间](@entry_id:177074)的转换变得非常直接。

#### 状态变换

[状态空间表示](@entry_id:147149)不唯一性的根源在于[状态变量](@entry_id:138790)的选择是任意的。只要一组新的状态变量 $\mathbf{z}(t)$ 是原始[状态变量](@entry_id:138790) $\mathbf{x}(t)$ 的一个[可逆线性变换](@entry_id:149915)，它就可以同样好地描述系统状态。这种变换称为**相似变换 (similarity transformation)** 或**状态变换 (state transformation)**。

设 $\mathbf{z}(t) = P\mathbf{x}(t)$，其中 $P$ 是一个可逆的 $n \times n$ 矩阵。我们可以推导出在新[坐标系](@entry_id:156346)下系统的[状态空间](@entry_id:177074)矩阵 $(\hat{A}, \hat{B}, \hat{C}, \hat{D})$。
首先，$\mathbf{x}(t) = P^{-1}\mathbf{z}(t)$。对其求导得到 $\dot{\mathbf{x}}(t) = P^{-1}\dot{\mathbf{z}}(t)$。
将这些代入原始状态方程：
$$
P^{-1}\dot{\mathbf{z}}(t) = A(P^{-1}\mathbf{z}(t)) + B\mathbf{u}(t)
$$
两边同时左乘 $P$：
$$
\dot{\mathbf{z}}(t) = (PAP^{-1})\mathbf{z}(t) + (PB)\mathbf{u}(t)
$$
与新状态方程 $\dot{\mathbf{z}}(t) = \hat{A}\mathbf{z}(t) + \hat{B}\mathbf{u}(t)$ 比较，可知：
$$
\hat{A} = PAP^{-1}, \quad \hat{B} = PB
$$
同样，代入输出方程：
$$
\mathbf{y}(t) = C(P^{-1}\mathbf{z}(t)) + D\mathbf{u}(t) = (CP^{-1})\mathbf{z}(t) + D\mathbf{u}(t)
$$
与 $\mathbf{y}(t) = \hat{C}\mathbf{z}(t) + \hat{D}\mathbf{u}(t)$ 比较，可知：
$$
\hat{C} = CP^{-1}, \quad \hat{D} = D
$$
一个重要的结论是，[相似变换](@entry_id:152935)不改变系统的外部特性。例如，新系统的[传递函数](@entry_id:273897)与原系统完全相同：
$$
\hat{H}(s) = \hat{C}(sI - \hat{A})^{-1}\hat{B} + \hat{D} = (CP^{-1})(sI - PAP^{-1})^{-1}(PB) + D = C(P(sI-A)P^{-1})^{-1}B + D = C(sI-A)^{-1}B + D = H(s)
$$
此外，由于矩阵 $A$ 和 $\hat{A}$ 是[相似矩阵](@entry_id:155833)，它们的[特征值](@entry_id:154894)也完全相同。这意味着系统的稳定性等内在特性在状态变换下是**[不变量](@entry_id:148850)**。

考虑一个具体的变换例子 [@problem_id:1754999]，原系统为：
$$
A = \begin{pmatrix} 0  1 \\ -2  -3 \end{pmatrix}, \quad P = \begin{pmatrix} 1  1 \\ -1  -2 \end{pmatrix}
$$
首先求 $P$ 的[逆矩阵](@entry_id:140380) $P^{-1}$：
$$
P^{-1} = \frac{1}{(1)(-2)-(1)(-1)} \begin{pmatrix} -2  -1 \\ 1  1 \end{pmatrix} = \begin{pmatrix} 2  1 \\ -1  -1 \end{pmatrix}
$$
然后计算新的状态矩阵 $\hat{A} = PAP^{-1}$：
$$
\hat{A} = \begin{pmatrix} 1  1 \\ -1  -2 \end{pmatrix} \begin{pmatrix} 0  1 \\ -2  -3 \end{pmatrix} \begin{pmatrix} 2  1 \\ -1  -1 \end{pmatrix} = \begin{pmatrix} -2  -2 \\ 4  5 \end{pmatrix} \begin{pmatrix} 2  1 \\ -1  -1 \end{pmatrix} = \begin{pmatrix} -2  0 \\ 3  -1 \end{pmatrix}
$$
尽管新矩阵 $\hat{A}$ 的形式与 $A$ 大相径庭，但它们描述的是同一个系统，具有相同的[特征值](@entry_id:154894)（$\lambda = -1, -2$）和相同的[传递函数](@entry_id:273897)。

### 系统响应与稳定性

状态空间模型为分析系统响应，特别是其内在的稳定性，提供了强有力的工具。

#### [状态转移矩阵](@entry_id:269075)

对于没有输入的系统，状态方程简化为[齐次方程](@entry_id:163650) $\dot{\mathbf{x}}(t) = A\mathbf{x}(t)$。其解可以表示为：
$$
\mathbf{x}(t) = e^{At}\mathbf{x}(0)
$$
其中 $e^{At}$ 是一个 $n \times n$ 的矩阵，称为**矩阵指数 (matrix exponential)**，定义为泰勒级数：
$$
e^{At} = I + At + \frac{(At)^2}{2!} + \frac{(At)^3}{3!} + \dots = \sum_{k=0}^{\infty} \frac{(At)^k}{k!}
$$
这个矩阵 $e^{At}$ 也被称为**[状态转移矩阵](@entry_id:269075) (state transition matrix)**，记作 $\Phi(t)$。它的作用是将系统在初始时刻的状态 $\mathbf{x}(0)$ “转移”到 $t$ 时刻的状态 $\mathbf{x}(t)$。

计算[状态转移矩阵](@entry_id:269075)通常比较复杂，但对于特殊结构的矩阵 $A$ 会变得简单。例如，如果 $A$ 是一个对角矩阵 [@problem_id:1755023]：
$$
A = \begin{pmatrix} -3  0 \\ 0  -7 \end{pmatrix}
$$
那么 $A$ 的任意次幂 $A^k$ 也是[对角矩阵](@entry_id:637782)：
$$
(At)^k = \begin{pmatrix} (-3t)^k  0 \\ 0  (-7t)^k \end{pmatrix}
$$
代入级数定义，[矩阵指数](@entry_id:139347)的计算就分解为对角线上每个元素的标量指数计算：
$$
e^{At} = \sum_{k=0}^{\infty} \frac{1}{k!} \begin{pmatrix} (-3t)^k  0 \\ 0  (-7t)^k \end{pmatrix} = \begin{pmatrix} \sum_{k=0}^{\infty} \frac{(-3t)^k}{k!}  0 \\ 0  \sum_{k=0}^{\infty} \frac{(-7t)^k}{k!} \end{pmatrix} = \begin{pmatrix} e^{-3t}  0 \\ 0  e^{-7t} \end{pmatrix}
$$
这清楚地表明，对于解耦的系统（$A$ 为对角阵），每个[状态变量](@entry_id:138790)都按其对应的[特征值](@entry_id:154894)独立演化。

#### [零输入响应](@entry_id:274925)与系统稳定性

当系统输入为零时（$u(t)=0$），其响应完全由初始状态 $\mathbf{x}(0)$ 决定，称为**[零输入响应](@entry_id:274925) (zero-input response)**。输出为：
$$
y_{zi}(t) = C\mathbf{x}(t) = C e^{At}\mathbf{x}(0)
$$
这个响应的行为完全由矩阵 $A$ 的**[特征值](@entry_id:154894) (eigenvalues)** 决定。实际上，$A$ 的[特征值](@entry_id:154894)正是系统[传递函数](@entry_id:273897)的**极点 (poles)**。它们是决定系统动态行为的“基因”。

$A$ 的[特征值](@entry_id:154894) $\lambda_i$ 的位置与[系统响应](@entry_id:264152)的定性行为有如下关系 [@problem_id:1754985]：
*   **稳定 (Stable)**：如果所有[特征值](@entry_id:154894)的实部都为负 ($\text{Re}(\lambda_i)  0$)，则所有响应模式都会随时间衰减至零。系统是稳定的。
    *   如果[特征值](@entry_id:154894)为互不相等的负实数，系统表现为**[过阻尼](@entry_id:167953) (overdamped)**，响应无[振荡](@entry_id:267781)地衰减。
    *   如果[特征值](@entry_id:154894)为具有负实部的[共轭复数对](@entry_id:150139)，系统表现为**欠阻尼 (underdamped)**，响应以指数衰减的幅度进行[振荡](@entry_id:267781)。
*   **不稳定 (Unstable)**：如果至少有一个[特征值](@entry_id:154894)的实部为正 ($\text{Re}(\lambda_i) > 0$)，则对应的响应模式会随时间无限增长。系统是不稳定的。
*   **[临界稳定](@entry_id:147657) (Marginally Stable)**：如果[特征值](@entry_id:154894)实部都不为正，但至少有一个或一对[特征值](@entry_id:154894)的实部为零，系统处于临界稳定状态。
    *   如果存在零实部的单阶[特征值](@entry_id:154894)（例如一对纯虚数 $\pm j\omega$），系统会产生**持续[振荡](@entry_id:267781) (undamped/purely oscillatory)**。

例如，对于一个[二阶系统](@entry_id:276555) $\dot{\mathbf{x}} = A\mathbf{x}$，我们可以通过计算 $A$ 的[特征值](@entry_id:154894)来判断其行为。[特征值](@entry_id:154894)是[特征方程](@entry_id:265849) $\det(sI-A) = s^2 - (\text{tr}A)s + (\det A) = 0$ 的根。
*   对于矩阵 $A_C = \begin{pmatrix} 0  1 \\ -5  -2 \end{pmatrix}$ [@problem_id:1754985]，其迹 $\text{tr}(A_C) = -2$，[行列式](@entry_id:142978) $\det(A_C) = 5$。特征方程为 $s^2 + 2s + 5 = 0$，根为 $s = -1 \pm j2$。由于[特征值](@entry_id:154894)是具有负实部的共轭复数，系统是欠阻尼的，会产生衰减[振荡](@entry_id:267781)。
*   对于矩阵 $A_A = \begin{pmatrix} 0  1 \\ -9  0 \end{pmatrix}$，[特征值](@entry_id:154894)为 $\pm j3$。它们是纯虚数，系统会产生持续[振荡](@entry_id:267781)。

计算[零输入响应](@entry_id:274925)本身，就是求解[齐次微分方程](@entry_id:166017)组。例如，对于系统 [@problem_id:1754976]：
$$
A = \begin{pmatrix} 0  1 \\ -3  -4 \end{pmatrix}, \quad C = \begin{pmatrix} 1  2 \end{pmatrix}, \quad x(0) = \begin{pmatrix} 1 \\ 0 \end{pmatrix}
$$
$A$ 的[特征值](@entry_id:154894)为 $-1$ 和 $-3$。因此，状态变量 $x_1(t)$ 和 $x_2(t)$ 的通解形式为 $c_1 e^{-t} + c_2 e^{-3t}$ 的[线性组合](@entry_id:154743)。通过[初始条件](@entry_id:152863) $x(0)$ 可以求出特定系数，进而得到 $x_1(t) = \frac{3}{2}e^{-t} - \frac{1}{2}e^{-3t}$ 和 $x_2(t) = -\frac{3}{2}e^{-t} + \frac{3}{2}e^{-3t}$。最后，输出响应为 $y(t) = x_1(t) + 2x_2(t) = -\frac{3}{2}e^{-t} + \frac{5}{2}e^{-3t}$。

### 基本系统属性：[可控性](@entry_id:148402)与可观性

除了稳定性，[状态空间](@entry_id:177074)框架还引出了两个至关重要的系统属性：[可控性](@entry_id:148402)和可观性。

#### [可控性](@entry_id:148402)

**[可控性](@entry_id:148402) (Controllability)** 回答了这样一个问题：我们是否能够通过操纵输入 $\mathbf{u}(t)$，在有限时间内将系统的状态从任意初始状态 $\mathbf{x}(t_0)$ 驱动到任意期望的最终状态 $\mathbf{x}(t_f)$？如果可以，系统就是**完全可控的 (completely controllable)**。这个属性对于设计有效的控制器至关重要。如果一个系统不是完全可控的，意味着其内部某些状态（或状态的组合）是“够不着”的，无论我们如何设计控制输入都无法影响它们。

判断一个[LTI系统](@entry_id:271946)是否可控的数学工具是**卡尔曼[可控性](@entry_id:148402)检验 (Kalman controllability test)**。首先构建一个 $n \times np$ 的**[可控性矩阵](@entry_id:271824) (controllability matrix)** $\mathcal{C}$：
$$
\mathcal{C} = \begin{pmatrix} B  AB  A^2B  \cdots  A^{n-1}B \end{pmatrix}
$$
系统是完全可控的，当且仅当[可控性矩阵](@entry_id:271824) $\mathcal{C}$ 的秩为 $n$（即满秩）。

在某些情况下，系统的参数可能会影响其可控性。例如，考虑一个由参数 $\alpha$ 描述的系统 [@problem_id:1755029]：
$$
A = \begin{pmatrix} -1  \alpha \\ 1  -2 \end{pmatrix}, \quad B = \begin{pmatrix} 1 \\ 2 \end{pmatrix}
$$
为了确定是否存在某个 $\alpha$ 值使系统变得不可控，我们构建[可控性矩阵](@entry_id:271824) $\mathcal{C} = \begin{pmatrix} B  AB \end{pmatrix}$。首先计算 $AB$：
$$
AB = \begin{pmatrix} -1  \alpha \\ 1  -2 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} -1+2\alpha \\ -3 \end{pmatrix}
$$
[可控性矩阵](@entry_id:271824)为：
$$
\mathcal{C} = \begin{pmatrix} 1  -1+2\alpha \\ 2  -3 \end{pmatrix}
$$
系统变得不可控的条件是 $\mathcal{C}$ 不满秩，对于一个 $2 \times 2$ 矩阵，这等价于其[行列式](@entry_id:142978)为零。
$$
\det(\mathcal{C}) = (1)(-3) - (2)(-1+2\alpha) = -3 + 2 - 4\alpha = -1 - 4\alpha
$$
令 $\det(\mathcal{C}) = 0$，我们得到 $-1 - 4\alpha = 0$，解得 $\alpha = -1/4$。这意味着，当[耦合系数](@entry_id:273384) $\alpha$ 取这个特定值时，系统的一个动态模式将脱离输入的控制。

#### 可观性

**可观性 (Observability)** 是可控性的对偶概念。它回答了另一个问题：我们是否能够仅通过观测有限时间段内的输出 $\mathbf{y}(t)$，来唯一地确定系统的初始状态 $\mathbf{x}(0)$？如果可以，系统就是**完全可观的 (completely observable)**。可观性对于状态估计和[状态反馈](@entry_id:151441)至关重要。如果一个系统不是完全可观的，意味着其内部某些状态（或状态的组合）的变化对输出没有任何影响，它们是“看不见”的。

**卡尔曼可观性检验 (Kalman observability test)** 用于判断可观性。构建一个 $nq \times n$ 的**可观性矩阵 (observability matrix)** $\mathcal{O}$：
$$
\mathcal{O} = \begin{pmatrix} C \\ CA \\ CA^2 \\ \vdots \\ CA^{n-1} \end{pmatrix}
$$
系统是完全可观的，当且仅当可观性矩阵 $\mathcal{O}$ 的秩为 $n$（即满秩）。

传感器的设计或放置方式会直接影响系统的可观性。考虑一个由传感器参数 $\alpha$ 决定的系统 [@problem_id:1755015]：
$$
A = \begin{pmatrix} 0  -1 \\ 4  -4 \end{pmatrix}, \quad C = \begin{pmatrix} 1  \alpha \end{pmatrix}
$$
我们构建可观性矩阵 $\mathcal{O} = \begin{pmatrix} C \\ CA \end{pmatrix}$。计算 $CA$：
$$
CA = \begin{pmatrix} 1  \alpha \end{pmatrix} \begin{pmatrix} 0  -1 \\ 4  -4 \end{pmatrix} = \begin{pmatrix} 4\alpha  -1-4\alpha \end{pmatrix}
$$
可观性矩阵为：
$$
\mathcal{O} = \begin{pmatrix} 1  \alpha \\ 4\alpha  -1-4\alpha \end{pmatrix}
$$
系统失去可观性的条件是 $\det(\mathcal{O}) = 0$：
$$
\det(\mathcal{O}) = (1)(-1-4\alpha) - (\alpha)(4\alpha) = -1 - 4\alpha - 4\alpha^2 = -(4\alpha^2 + 4\alpha + 1) = -(2\alpha+1)^2
$$
令 $\det(\mathcal{O}) = 0$，得到 $\alpha = -1/2$。当传感器权重 $\alpha$ 取这个精确值时，输出 $y(t)$ 中位置和速度分量的组合方式恰好使得系统内部的一个动态模式（对应于[特征值](@entry_id:154894) $\lambda=-2$ 的重根模式）无法在输出中被观察到。

#### [最小实现](@entry_id:176932)

[可控性](@entry_id:148402)和可观性与[传递函数](@entry_id:273897)中的[极零点对消](@entry_id:261496)现象密切相关，并引出了**[最小实现](@entry_id:176932) (minimal realization)** 的概念。一个[状态空间实现](@entry_id:166670)的阶数（即[状态向量](@entry_id:154607)的维数 $n$）是最小的，当且仅当该系统既是完全可控的又是完全可观的。[最小实现](@entry_id:176932)的阶数等于系统[传递函数](@entry_id:273897)在消去所有公因子后的分母阶数。

当[传递函数](@entry_id:273897)中出现[极零点对消](@entry_id:261496)时，意味着对应的[状态空间实现](@entry_id:166670)不是最小的。被消去的极点所对应的动态模式，要么是不可控的，要么是不可观的（或两者都是）。

例如，之前我们遇到的[传递函数](@entry_id:273897) [@problem_id:1755020]：
$$
H(s) = \frac{s + 2}{s^3 + 9s^2 + 26s + 24} = \frac{s + 2}{(s+2)(s+3)(s+4)}
$$
这个三阶[传递函数的极点](@entry_id:266427)在 $s=-2, -3, -4$，零点在 $s=-2$。由于在 $s=-2$ 处存在[极零点对消](@entry_id:261496)，系统的[最小实现](@entry_id:176932)实际上是二阶的，其[传递函数](@entry_id:273897)为：
$$
H_{red}(s) = \frac{1}{(s+3)(s+4)} = \frac{1}{s^2 + 7s + 12}
$$
如果我们为这个[二阶系统](@entry_id:276555)构建一个[可控标准型](@entry_id:165254)实现，其状态矩阵 $A$ 为：
$$
A_{min} = \begin{pmatrix} 0  1 \\ -12  -7 \end{pmatrix}
$$
这个二阶实现是最小的。与此相对，任何直接基于原始三阶[传递函数](@entry_id:273897)的实现都会包含一个与极点 $s=-2$ 相关的模式，这个模式要么不可控，要么不可观，因此该实现不是最小的。这个例子完美地阐释了输入-输出行为（[传递函数](@entry_id:273897)）与内部结构（可控性/可观性）之间的深刻联系。

本章系统地介绍了[状态空间表示](@entry_id:147149)法的核心原理与机制。从基本定义到与经典方法的联系，再到稳定性、可控性、可观性等高级概念的分析，状态空间法为我们理解和设计复杂动态系统提供了一个统一而强大的框架。