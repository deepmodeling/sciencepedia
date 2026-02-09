## 引言
在处理固体力学中的大变形问题时，常用的柯西应力张量因其定义在随时间变化的当前构型上，给理论分析和数值计算带来了诸多不便。例如，有限元法等计算技术往往依赖于一个固定不变的参考构型进行积分和求解。为了克服这一挑战，引入在参考构型中定义的应力测度变得至关重要。本文旨在系统性地介绍两种核心的拉格朗日应力张量：第一皮奥拉-基尔霍夫应力张量 (P) 和第二皮奥拉-基尔霍夫应力张量 (S)。

通过本文的学习，读者将全面掌握这些关键概念。在“原理与机制”一章中，我们将从变形运动学基础出发，详细阐述两种PK应力张量的定义、物理意义、数学性质（如对称性和客观性）及其与柯西应力的转换关系，并揭示它们在能量原理中的功能共轭作用。接下来的“应用与跨学科联系”一章将展示这些理论工具如何在建立统一的平衡方程、构建超弹性和各向异性材料本构模型、赋能计算固体力学以及推动断裂和构型力学等前沿理论中发挥核心作用。最后，“动手实践”部分将通过具体的计算问题，帮助读者巩固理论知识，并将其应用于解决实际的力学问题。

## 原理与机制

在对有限变形进行分析时，描述物体内部应力状态的柯西应力张量（Cauchy stress tensor）$\boldsymbol{\sigma}$ 是在当前构型中定义的，这在某些情况下会带来不便。例如，在许多数值模拟（如有限元法）中，积分和计算是在固定的、未变形的参考构型上进行的。因此，引入完全在参考构型中定义的应力张量变得至关重要。本章将详细阐述两个核心的拉格朗日应力张量：第一皮奥拉-基尔霍夫（First Piola-Kirchhoff）应力张量 $\mathbf{P}$ 和第二皮奥拉-基尔霍夫（Second Piola-Kirchhoff）应力张量 $\mathbf{S}$，并系统地探讨它们的定义、物理意义、相互关系以及在能量和本构理论中的应用。

### 变形的运动学基础

在深入探讨应力测度之前，我们必须首先回顾描述变形的几个关键运动学量。连续体的运动将参考构型 $\mathcal{B}_0$ 中的物质点 $\mathbf{X}$ 映射到当前构型 $\mathcal{B}_t$ 中的空间点 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$。这一映射的局部线性化由**变形梯度**（deformation gradient）$\mathbf{F}$ 描述：

$$
\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}}
$$

变形梯度 $\mathbf{F}$ 是连接参考构型和当前构型的桥梁。一个位于参考构型中的无限小线元 $d\mathbf{X}$，在变形后会变为当前构型中的线元 $d\mathbf{x}$，它们之间的关系为 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$ [@problem_id:2640987]。同样，参考构型中的有向面元 $\mathbf{N} dA$ 和当前构型中的对应面元 $\mathbf{n} da$ 之间的关系由**南森公式**（Nanson's formula）给出：

$$
\mathbf{n} da = J \mathbf{F}^{-T} \mathbf{N} dA
$$

其中 $J = \det(\mathbf{F})$ 是变形梯度的行列式，代表了局部体积的变化率 ($dV_t = J dV_0$)。物理上，物质不可穿透的要求意味着 $J > 0$ [@problem_id:2640987]。

为了将局部变形从刚体转动中分离出来，我们可以对变形梯度进行**极分解**（polar decomposition）[@problem_id:2640987]。右极分解将 $\mathbf{F}$ 分解为一个纯拉伸和一个刚体转动：

$$
\mathbf{F} = \mathbf{R} \mathbf{U}
$$

其中 $\mathbf{R}$ 是一个正常交张量（proper orthogonal tensor, $\mathbf{R}^T\mathbf{R}=\mathbf{I}, \det\mathbf{R}=+1$），代表局部刚体转动。$\mathbf{U}$ 是一个对称正定张量，称为**右拉伸张量**（right stretch tensor），它完全描述了在参考构型坐标系下测量的局部拉伸和剪切。为了方便起见，我们还定义了**右柯西-格林变形张量**（right Cauchy-Green deformation tensor）$\mathbf{C}$：

$$
\mathbf{C} = \mathbf{F}^T \mathbf{F} = (\mathbf{R}\mathbf{U})^T (\mathbf{R}\mathbf{U}) = \mathbf{U}^T \mathbf{R}^T \mathbf{R} \mathbf{U} = \mathbf{U}^2
$$

由于 $\mathbf{C}$ 是 $\mathbf{U}$ 的平方，它同样是一个纯粹的变形度量，其特征值是主拉伸的平方。$\mathbf{C}$ 和 $\mathbf{U}$ 都在参考构型中定义，并且不受后续刚体转动 $\mathbf{R}$ 的影响，因此是客观的变形度量 [@problem_id:2640987]。

### 第一皮奥拉-基尔霍夫应力张量

柯西应力张量 $\boldsymbol{\sigma}$ 将当前构型中的面法线 $\mathbf{n}$ 映射到作用在该面上的柯西（真实）牵引力 $\mathbf{t}$（单位当前面积上的力），即 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$。然而，在许多分析中，我们更希望将力与参考构型中的面积关联起来。

为此，我们定义**名义牵引力**（nominal traction）$\mathbf{T}$，它表示作用在变形后物体上的力，但除以其在**参考构型**中的原始面积 $dA$。作用在面元上的力矢量 $d\mathbf{f}$ 是唯一的，因此：

$$
d\mathbf{f} = \mathbf{t} \, da = \mathbf{T} \, dA
$$

**第一皮奥拉-基尔霍夫应力张量**（First Piola-Kirchhoff stress tensor）$\mathbf{P}$ 就是将参考构型中的面法线 $\mathbf{N}$ 线性映射到名义牵引力 $\mathbf{T}$ 的张量 [@problem_id:2641039]：

$$
\mathbf{T} = \mathbf{P} \mathbf{N}
$$

为了找到 $\mathbf{P}$ 与 $\boldsymbol{\sigma}$ 的关系，我们将上述关系式结合起来：

$$
\mathbf{P} \mathbf{N} \, dA = \mathbf{T} \, dA = \mathbf{t} \, da = (\boldsymbol{\sigma} \mathbf{n}) \, da = \boldsymbol{\sigma} (\mathbf{n} \, da)
$$

利用南森公式 $\mathbf{n} \, da = J \mathbf{F}^{-T} \mathbf{N} \, dA$ 代入上式，我们得到：

$$
\mathbf{P} \mathbf{N} \, dA = \boldsymbol{\sigma} (J \mathbf{F}^{-T} \mathbf{N} \, dA)
$$

由于该式对任意面法线 $\mathbf{N}$ 均成立，我们便得到了 $\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 之间的基本关系，也称为皮奥拉变换（Piola transform） [@problem_id:2641039] [@problem_id:2640987]：

$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}
$$

反过来，我们也可以从 $\mathbf{P}$ 计算柯西应力 $\boldsymbol{\sigma}$：

$$
\boldsymbol{\sigma} = \frac{1}{J} \mathbf{P} \mathbf{F}^T
$$

例如，考虑一个特定的点，其变形梯度为 $F = \begin{pmatrix} 2  1 \\ 1  2 \end{pmatrix}$，第一皮奥拉-基尔霍夫应力为 $P = \begin{pmatrix} 0  \tau \\ \tau  0 \end{pmatrix}$。首先计算 $J = \det(F) = 2 \cdot 2 - 1 \cdot 1 = 3$。由于 $F$ 是对称的， $F^T = F$。因此，柯西应力为 [@problem_id:1549745]：

$$
\boldsymbol{\sigma} = \frac{1}{3} \mathbf{P} \mathbf{F}^T = \frac{1}{3} \begin{pmatrix} 0  \tau \\ \tau  0 \end{pmatrix} \begin{pmatrix} 2  1 \\ 1  2 \end{pmatrix} = \frac{1}{3} \begin{pmatrix} \tau  2\tau \\ 2\tau  \tau \end{pmatrix}
$$

$\mathbf{P}$ 张量是一个**两点张量**（two-point tensor），因为它将参考构型中的一个矢量（$\mathbf{N}$）映射到当前构型中的一个矢量（$\mathbf{T}$）。这在概念上和计算上都可能显得有些复杂。

### 第二皮奥拉-基尔霍夫应力张量

为了得到一个完全在参考构型中定义的应力张量，我们引入了**第二皮奥拉-基尔霍夫应力张量**（Second Piola-Kirchhoff stress tensor）$\mathbf{S}$。其定义方式是将名义牵引力矢量 $\mathbf{T}$（存在于当前空间）通过变形梯度的逆 “拉回”（pull back）到参考构型中。这个被拉回的伪力矢量 $\mathbf{F}^{-1}\mathbf{T}$ 与参考法线 $\mathbf{N}$ 通过 $\mathbf{S}$ 关联起来。

这个定义可以简洁地通过 $\mathbf{P}$ 和 $\mathbf{S}$ 的关系来表达 [@problem_id:2641038]：

$$
\mathbf{P} = \mathbf{F} \mathbf{S} \quad \text{或等价地} \quad \mathbf{S} = \mathbf{F}^{-1} \mathbf{P}
$$

现在，名义牵引力可以写为 $\mathbf{T} = \mathbf{F} (\mathbf{S} \mathbf{N})$。这意味着矢量 $\mathbf{S} \mathbf{N}$ 是一个定义在参考构型中的“伪牵引力”，当它被变形梯度 $\mathbf{F}$ “推前”（push forward）到当前构型时，就得到了真实的名义牵引力 $\mathbf{T}$ [@problem_id:2641038]。

将 $\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}$ 代入 $\mathbf{S}$ 的定义，我们得到 $\mathbf{S}$ 和 $\boldsymbol{\sigma}$ 的直接关系：

$$
\mathbf{S} = \mathbf{F}^{-1} (J \boldsymbol{\sigma} \mathbf{F}^{-T}) = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T}
$$

这个关系表明，$\mathbf{S}$ 是通过将**基尔霍夫应力张量**（Kirchhoff stress tensor）$\boldsymbol{\tau} = J\boldsymbol{\sigma}$ 从当前构型“拉回”到参考构型而得到的。由于 $\mathbf{F}^{-1}$、$\boldsymbol{\sigma}$ 和 $\mathbf{F}^{-T}$ 的变换性质，$\mathbf{S}$ 是一个完全在参考构型中定义的张量，因此它是一个纯粹的拉格朗日量。

例如，考虑一个变形，其变形梯度为 $F = \begin{pmatrix} 1  \gamma  0 \\ 0  1  0 \\ 0  0  \lambda \end{pmatrix}$，柯西应力为 $\sigma = \sigma_0 \begin{pmatrix} 1  0  1 \\ 0  2  0 \\ 1  0  1 \end{pmatrix}$。我们可以通过上述公式计算 $\mathbf{S}$。首先，$J = \det(F) = \lambda$。然后计算 $F^{-1}$ 和 $F^{-T}$，并执行矩阵乘法 $S = \lambda F^{-1} \sigma F^{-T}$，最终得到 [@problem_id:1549770]：

$$
S = \sigma_{0} \begin{pmatrix} \lambda(1 + 2\gamma^{2})  -2\lambda\gamma  1 \\ -2\lambda\gamma  2\lambda  0 \\ 1  0  \frac{1}{\lambda} \end{pmatrix}
$$

### 不同应力张量的性质与关联

#### 对称性

对称性是应力张量的一个核心性质，它源于动量矩平衡。
1.  **柯西应力 $\boldsymbol{\sigma}$**：在没有体力矩或耦合应力的情况下，动量矩平衡定律要求柯西应力张量必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$ [@problem_id:2640989]。这是我们分析其他应力张量对称性的出发点。

2.  **第二皮奥拉-基尔霍夫应力 $\mathbf{S}$**：我们可以检验 $\mathbf{S}$ 的对称性。利用 $\boldsymbol{\sigma}$ 的对称性，我们有：
    $$
    \mathbf{S}^T = (J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T})^T = J (\mathbf{F}^{-T})^T \boldsymbol{\sigma}^T (\mathbf{F}^{-1})^T = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T} = \mathbf{S}
    $$
    因此，如果柯西应力是对称的，那么第二皮奥拉-基尔霍夫应力也**总是对称的** [@problem_id:2640989] [@problem_id:2641038]。

3.  **第一皮奥拉-基尔霍夫应力 $\mathbf{P}$**：现在我们来检验 $\mathbf{P}$ 的对称性。
    $$
    \mathbf{P}^T = (J \boldsymbol{\sigma} \mathbf{F}^{-T})^T = J (\mathbf{F}^{-T})^T \boldsymbol{\sigma}^T = J \mathbf{F}^{-1} \boldsymbol{\sigma}
    $$
    将此式与 $\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}$ 比较，可以发现除非在非常特殊的情况下（例如 $\mathbf{F}$ 是一个纯拉伸乘以一个标量），$\mathbf{P}$ **通常是非对称的** [@problem_id:2640989] [@problem_id:2641039]。

$\mathbf{P}$ 的非对称性并不意味着动量矩平衡被违反。实际上，动量矩平衡在参考构型中的正确表达形式是要求张量 $\mathbf{P}\mathbf{F}^T$ 是对称的。我们可以证明这一点：
$$
\mathbf{P}\mathbf{F}^T = (J \boldsymbol{\sigma} \mathbf{F}^{-T}) \mathbf{F}^T = J \boldsymbol{\sigma} (\mathbf{F}^{-T} \mathbf{F}^T) = J \boldsymbol{\sigma}
$$
由于 $\boldsymbol{\sigma}$ 是对称的，$J$ 是标量，所以 $J\boldsymbol{\sigma}$（基尔霍夫应力）也是对称的。因此，$\mathbf{P}\mathbf{F}^T$ 的对称性是动量矩平衡在材料描述下的自然结果 [@problem_id:2640989]。

#### 客观性 (Material Frame-Indifference)

客观性原则要求本构关系在叠加一个任意的刚体运动后形式不变。这意味着本构关系中使用的物理量应该是客观的。
- 柯西应力 $\boldsymbol{\sigma}$ 在刚体转动 $\mathbf{Q}$ 下的变换关系为 $\boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^T$。
- 可以证明，第一皮奥拉-基尔霍夫应力 $\mathbf{P}$ 的变换关系为 $\mathbf{P}^* = \mathbf{Q}\mathbf{P}$。由于它不是像 $\boldsymbol{\sigma}$ 那样变换，因此 $\mathbf{P}$ **不是一个客观张量** [@problem_id:2641039]。
- 相比之下，第二皮奥拉-基尔霍夫应力 $\mathbf{S}$ 在刚体转动下是**不变的**，即 $\mathbf{S}^* = \mathbf{S}$。这意味着 $\mathbf{S}$ 是一个客观张量。它的客观性，加上它的对称性，使其成为构建依赖于纯变形的本构关系（即材料的内在响应）的理想选择。

### 功能共轭关系与本构理论

应力张量和应变张量之间的关系不仅是代数的，更深层次的联系体现在它们在能量耗散（或储存）中的作用。单位参考体积的**应力功率**（stress power）$W_R$ 是应力在变形过程中所做的功的速率。

应力功率的基本表达式是第一皮奥拉-基尔霍夫应力 $\mathbf{P}$ 与变形梯度率 $\dot{\mathbf{F}}$ 的点积：

$$
W_R = \mathbf{P} : \dot{\mathbf{F}}
$$

这个关系表明，$\mathbf{P}$ 和 $\mathbf{F}$ 是一对**功能共轭**（work-conjugate）的量。这解释了为什么在以位移（其梯度为 $\mathbf{F}$）为基本未知量的力学公式中，$\mathbf{P}$ 会自然出现 [@problem_id:2640959]。例如，在有限元法的虚功原理中，内力虚功项通常写为 $\int_{\mathcal{B}_0} \mathbf{P} : \delta\mathbf{F} \, dV_0$。

现在，我们希望找到与第二皮奥拉-基尔霍夫应力 $\mathbf{S}$ 功能共轭的应变率。为此，我们引入**格林-拉格朗日应变张量**（Green-Lagrange strain tensor）$\mathbf{E}$：

$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})
$$

$\mathbf{E}$ 是一个纯粹的变形度量，它在参考构型中定义并且是客观的。它的物质时间导数为 $\dot{\mathbf{E}} = \frac{1}{2}(\dot{\mathbf{F}}^T\mathbf{F} + \mathbf{F}^T\dot{\mathbf{F}})$。现在，我们将 $\mathbf{P} = \mathbf{F}\mathbf{S}$ 代入应力功率表达式中：

$$
W_R = (\mathbf{F}\mathbf{S}) : \dot{\mathbf{F}} = \text{tr}((\mathbf{F}\mathbf{S})^T \dot{\mathbf{F}}) = \text{tr}(\mathbf{S}^T \mathbf{F}^T \dot{\mathbf{F}})
$$

由于 $\mathbf{S}$ 是对称的，并且利用迹的循环性质，可以证明：

$$
W_R = \text{tr}(\mathbf{S} \mathbf{F}^T \dot{\mathbf{F}}) = \mathbf{S} : (\mathbf{F}^T\dot{\mathbf{F}})
$$

利用 $\dot{\mathbf{E}}$ 的表达式和 $\mathbf{S}$ 的对称性，我们也可以证明 $\mathbf{S} : \dot{\mathbf{E}} = \mathbf{S} : (\mathbf{F}^T\dot{\mathbf{F}})$。因此，我们得到了一个至关重要的恒等式 [@problem_id:2641038] [@problem_id:1549750]：

$$
W_R = \mathbf{P} : \dot{\mathbf{F}} = \mathbf{S} : \dot{\mathbf{E}}
$$

这个恒等式表明，$\mathbf{S}$ 和 $\mathbf{E}$ 也是一对功能共轭的量。

这种功能共轭关系在**超弹性**（hyperelasticity）理论中具有核心地位。对于超弹性材料，存在一个应变能密度函数 $\Psi$（单位参考体积的储存能量），应力可以由其导出。
- 如果应变能表示为变形梯度的函数 $\Psi = \hat{\Psi}(\mathbf{F})$，那么第一皮奥拉-基尔霍夫应力为：
  $$
  \mathbf{P} = \frac{\partial \hat{\Psi}}{\partial \mathbf{F}}
  $$
- 更常见地，根据客观性原理，应变能应仅依赖于纯变形，因此表示为格林-拉格朗日应变（或右柯西-格林张量）的函数 $\Psi = \tilde{\Psi}(\mathbf{E})$。在这种情况下，第二皮奥拉-基尔霍夫应力自然地成为与 $\mathbf{E}$ 共轭的应力：
  $$
  \mathbf{S} = \frac{\partial \tilde{\Psi}}{\partial \mathbf{E}}
  $$

综上所述，$\mathbf{P}$ 和 $\mathbf{S}$ 并非相互竞争的应力定义，而是服务于不同目的的数学工具。$\mathbf{P}$ 作为与 $\mathbf{F}$ 功能共轭的量，自然地出现在以位移为基础的平衡方程和边界条件中（例如，名义牵引力边界条件 $\mathbf{P}\mathbf{N} = \mathbf{t}_0$）。而 $\mathbf{S}$ 作为与纯应变度量 $\mathbf{E}$ 功能共轭的对称、客观张量，是构建材料本构关系的最理想选择 [@problem_id:2640959]。在实际的有限元计算中，通常先通过本构关系（基于 $\mathbf{S}$ 和 $\mathbf{E}$）计算出 $\mathbf{S}$，然后通过变换 $\mathbf{P} = \mathbf{F}\mathbf{S}$ 得到 $\mathbf{P}$，最后用 $\mathbf{P}$ 来计算内力矢量以求解全局平衡方程。