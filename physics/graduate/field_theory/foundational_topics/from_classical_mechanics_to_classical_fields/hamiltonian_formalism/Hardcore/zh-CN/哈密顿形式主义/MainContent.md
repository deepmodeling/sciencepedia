## 引言
哈密顿形式主义是理论物理学的一块基石，它提供了与拉格朗日形式主义互补但更为深刻的视角来描述物理系统的动力学。虽然拉格朗日方法在构建协变理论时表现出极大的优雅性，但哈密顿框架在揭示系统的对称性结构、进行量子化以及处理复杂的约束系统方面拥有无可替代的优势。

从经典场论过渡到量子场论，或者深入理解电磁学与广义相对论等规范理论的内在机制，都绕不开哈密顿形式主义。然而，将离散粒子的哈密顿力学推广到具有无穷自由度的场，并处理由此产生的奇异性与约束，是许多学习者面临的核心挑战。本文旨在系统性地扫清这些障碍。

在本文中，我们将带领读者踏上从原理到应用的完整旅程。在“原理与机制”一章，我们将建立场论的哈密顿形式，学习如何从拉格朗日密度出发构建哈密顿量，并探讨其在量子化中的作用。接着，在“应用与跨学科联系”一章，我们将展示哈密顿框架如何统一地描述粒子物理、凝聚态物质和宇宙学中的多样现象。最后，通过“动手实践”部分，你将有机会亲自运用这些知识解决具体物理问题，从而巩固你的理解。

## 原理与机制

从拉格朗日形式主义过渡到哈密顿形式主义，是理论物理学中一个至关重要的步骤，它为量子化提供了标准路径，并为处理具有规范对称性的理论（如电磁学和广义相对论）提供了强大的框架。在本章中，我们将系统地建立场论的哈密顿形式主义，阐明其核心原理，并探讨其在各种物理系统中的具体应用机制。

### 正则形式：从粒子到场

我们从经典力学中的勒让德变换（Legendre transform）开始。对于一个由广义坐标 $q$ 和广义速度 $\dot{q}$ 描述的系统，拉格朗日量是 $L(q, \dot{q})$。其哈密顿量 $H(q, p)$ 是通过引入共轭动量 $p = \frac{\partial L}{\partial \dot{q}}$ 来定义的：

$H(q, p) = p\dot{q} - L(q, \dot{q})$

在场论中，我们将场 $\phi(t, \mathbf{x})$ 视为一组无穷的广义坐标，其中每一个空间点 $\mathbf{x}$ 都标记着一个独立的自由度 $\phi(\mathbf{x})$。因此，$\partial_0\phi = \dot{\phi}$ 扮演着广义速度的角色。与场的每个“坐标” $\phi(\mathbf{x})$ 相关联的**正则动量密度**（canonical momentum density）$\pi(t, \mathbf{x})$ 定义为拉格朗日密度 $\mathcal{L}$ 对场的时间导数的偏导数：

$$
\pi(x) = \frac{\partial\mathcal{L}}{\partial(\partial_0\phi(x))}
$$

一旦定义了正则动量密度，我们就可以通过勒让德变换构建**哈密顿密度**（Hamiltonian density）$\mathcal{H}$：

$$
\mathcal{H}(\phi, \nabla\phi, \pi) = \pi(\partial_0\phi) - \mathcal{L}(\phi, \partial_\mu\phi)
$$

在这里，我们必须将表达式中所有的 $\partial_0\phi$ 都用 $\phi$、$\nabla\phi$ 和 $\pi$ 来代替。最终的哈密顿密度只应是场、其空间导数和其共轭动量的函数。系统的总**哈密顿量**（Hamiltonian）$H$ 则是哈密顿密度在整个空间上的积分：

$$
H = \int d^3x \, \mathcal{H}(\phi, \nabla\phi, \pi)
$$

这个哈密顿量在物理上代表了系统的总能量。

### 哈密顿量的构建：具体范例

构建哈密顿量的过程在不同理论中可能表现出不同的复杂性。下面我们通过几个例子来具体说明这一过程。

#### 标量场

对于一个标准的实标量场理论，其拉格朗日密度为 $\mathcal{L} = \frac{1}{2}(\partial_\mu\phi)^2 - V(\phi)$。例如，在正弦-戈登模型（Sine-Gordon model）中，势能项为 $V(\phi) = \frac{\alpha}{\beta^2} (1 - \cos(\beta \phi))$ ([@problem_id:327101])。首先计算正则动量密度：

$$
\pi = \frac{\partial\mathcal{L}}{\partial(\partial_0\phi)} = \partial_0\phi
$$

然后，我们进行勒让德变换：

$$
\mathcal{H} = \pi(\partial_0\phi) - \mathcal{L} = \pi^2 - \left(\frac{1}{2}(\partial_0\phi)^2 - \frac{1}{2}(\nabla\phi)^2 - V(\phi)\right)
$$

将 $\partial_0\phi = \pi$ 代入，我们得到标量场论中一个非常熟悉的结果：

$$
\mathcal{H} = \frac{1}{2}\pi^2 + \frac{1}{2}(\nabla\phi)^2 + V(\phi)
$$

这个表达式直观地表示了场的能量密度：第一项是动能密度，第二项是与场在空间中变化相关的梯度能量，第三项是势能密度。

然而，$\pi$ 与 $\partial_0\phi$ 之间的关系并非总是线性的。考虑一个具有导数自相互作用的理论，其拉格朗日密度包含一个 $(\partial_0\phi)^3$ 项 ([@problem_id:327191])：

$$
\mathcal{L} = \frac{1}{2} (\partial_0 \phi)^2 - \frac{1}{2} (\nabla\phi)^2 - \frac{1}{2}m^2\phi^2 - \frac{g}{6}(\partial_0 \phi)^3
$$

其正则动量为：

$$
\pi = \partial_0 \phi - \frac{g}{2} (\partial_0 \phi)^2
$$

这是一个关于 $\partial_0\phi$ 的二次方程。为了用 $\pi$ 表示 $\partial_0\phi$，我们需要解这个方程，这会得到两个解。物理上合理的解必须在相互作用趋于零（$g \to 0$）的极限下平滑地过渡到自由理论（其中 $\pi = \partial_0\phi$）。这个物理判据使我们能够唯一地确定正确的解支，从而构建出明确的哈密顿量。这个例子说明，即使在经典层面，相互作用也能使正则变量之间的关系变得高度非平凡。

对于复标量场，我们通常将其分解为两个实标量场来处理。例如，考虑一个由 $\phi = \frac{1}{\sqrt{2}}(\psi_1 + i\psi_2)$ 描述的复标量场，如果拉格朗日量中存在 $\phi^2 - (\phi^\dagger)^2$ 这样的项，它在实场基底下会产生一个 $\psi_1\psi_2$ 耦合项 ([@problem_id:327250])。这导致质量项在 $(\psi_1, \psi_2)$ 基底下不是对角的。哈密顿量中的势能部分将包含一个二次型 $\frac{1}{2}\boldsymbol{\psi}^T M^2 \boldsymbol{\psi}$，其中 $M^2$ 是一个非对角的质量平方矩阵。物理质量的平方就是该矩阵的本征值，而相应的本征向量则定义了无相互作用的、可自由传播的物理场。

#### 旋量场

对于费米子场，如狄拉克场或马约拉纳场，情况有所不同，因为它们是由反交换的格拉斯曼数（Grassmann numbers）描述的。在求导时，我们必须使用左导数或右导数。对于一个 (2+1) 维的马约拉纳费米子场 $\psi$ ([@problem_id:327110])，其拉格朗日密度为：

$$
\mathcal{L} = \frac{1}{2} \bar{\psi}(i\gamma^\mu \partial_\mu - m)\psi = \frac{i}{2} \psi^\dagger \dot{\psi} + \dots
$$

其中 $\dot{\psi} = \partial_0 \psi$，省略号代表不含时间导数的项。共轭动量 $\Pi$ 定义为对 $\dot{\psi}$ 的左导数：

$$
\Pi_\alpha = \frac{\partial \mathcal{L}}{\partial \dot{\psi}_\alpha} = \frac{i}{2}\psi_\alpha^\dagger
$$

或者用旋量记号写作 $\Pi = \frac{i}{2}\psi^\dagger$。现在构造哈密顿密度：

$$
\mathcal{H} = \Pi \dot{\psi} - \mathcal{L} = \left(\frac{i}{2}\psi^\dagger\right) \dot{\psi} - \left( \frac{i}{2} \psi^\dagger \dot{\psi} - \frac{i}{2} \bar{\psi} \gamma^j \partial_j\psi + \frac{m}{2} \bar{\psi}\psi \right)
$$

一个关键且普遍的特征是，包含时间导数 $\dot{\psi}$ 的项在哈密顿密度中完全抵消了。这留下：

$$
\mathcal{H} = \frac{1}{2} \bar{\psi}(-i\gamma^j \partial_j + m)\psi
$$

这个结果表明，对于一阶导数形式的费米子拉格朗日量，其哈密顿量不依赖于正则动量（因为它正比于场本身），而是直接由场及其空间导数给出。

### 哈密顿框架下的动力学

哈密顿形式主义的真正威力在于它提供了一个描述系统时间演化的新框架。

#### 哈密顿运动方程

场的经典动力学由哈密顿运动方程给出，这是对无限维相空间的直接推广：

$$
\partial_0 \phi(x) = \frac{\delta H}{\delta \pi(x)}
$$

$$
\partial_0 \pi(x) = -\frac{\delta H}{\delta \phi(x)}
$$

这里的 $\frac{\delta}{\delta f}$ 表示**泛函导数**（functional derivative）。对于一个局域场论，其哈密顿量 $H = \int d^3x \, \mathcal{H}(\phi, \partial_i\phi, \pi)$，泛函导数的计算规则是：

$$
\frac{\delta H}{\delta \phi(x)} = \frac{\partial \mathcal{H}}{\partial \phi(x)} - \partial_i \left( \frac{\partial \mathcal{H}}{\partial(\partial_i \phi(x))} \right)
$$

这条规则考虑了哈密顿密度对场本身的依赖，以及对场空间导数的依赖。

我们可以验证，这组一阶微分方程等价于从拉格朗日量得到的二阶欧拉-拉格朗日方程。以正弦-戈登模型为例 ([@problem_id:327101])，我们有 $\mathcal{H} = \frac{1}{2}\pi^2 + \frac{1}{2}(\partial_x\phi)^2 + V(\phi)$。第一个哈密顿方程给出 $\partial_0\phi = \frac{\delta H}{\delta \pi} = \pi$，这重现了正则动量的定义。第二个方程给出：

$$
\partial_0\pi = -\frac{\delta H}{\delta \phi} = -\left( \frac{\partial\mathcal{H}}{\partial\phi} - \partial_x\frac{\partial\mathcal{H}}{\partial(\partial_x\phi)} \right) = -\left(\frac{dV}{d\phi} - \partial_x^2\phi\right)
$$

结合这两个方程，并代入 $\pi = \partial_0\phi$，我们得到 $\partial_0^2\phi = \partial_x^2\phi - \frac{dV}{d\phi}$，这正是该模型的欧拉-拉格朗日方程。

#### 量子动力学与守恒律

在量子场论中，经典泊松括号被算符的对易子取代。场算符及其共轭动量算符满足**等时对易关系**（Equal-Time Commutation Relations, CCRs）。对于标量场，它们是：

$$
[\phi(\mathbf{x}, t), \pi(\mathbf{y}, t)] = i\delta^{(3)}(\mathbf{x}-\mathbf{y})
$$

在海森堡绘景（Heisenberg picture）中，算符随时间演化，其动力学由**海森堡运动方程**描述：

$$
i \frac{d\mathcal{O}}{dt} = [\mathcal{O}, H]
$$

这个方程是理解守恒律的关键。如果一个物理量（由算符 $Q$ 表示）不随时间变化，那么它就是守恒的，这意味着 $[Q, H] = 0$。

一个深刻的例子来自对狄拉克场的角动量分析。对于自由狄拉克场，人们可以定义轨道角动量算符 $L^k$。然而，通过计算 $[H, L^k]$ ([@problem_id:327114])，可以发现这个对易子不为零。具体来说，$[H, L^k]$ 正比于一个描述“力矩”的算符，这表明轨道角动量本身并不守恒。

$$
[H, L^k] = \int d^3x \, \psi^\dagger(\mathbf{x}) (-i\epsilon^{kij} \alpha^i p_j) \psi(\mathbf{x}) \neq 0
$$

这个非零的结果揭示了一个基本事实：在相对论性量子理论中，电子的轨道运动和其内在的自旋是耦合的。为了得到一个守恒的总角动量 $J$，我们必须引入一个自旋角动量算符 $S$，使得 $[H, J^k] = [H, L^k+S^k] = 0$。因此，哈密顿形式主义为自旋的存在提供了动力学上的根本原因。

同样，海森堡方程也可以应用于场算符本身，从而得到算符运动方程，如耦合标量场的克莱因-戈登方程 ([@problem_id:327109])。一旦量子化的理论建立，诸如角动量之类的算符就可以作用在由创生算符构建的量子态上，以提取物理可观测量，例如角动量的本征值 ([@problem_id:327216])。

### 约束哈密顿系统

在许多最重要的物理理论中，包括电磁学和广义相对论，拉格朗日量是“奇异的”（singular）。这意味着正则动量的定义不能被反解出来以表达所有的广义速度。这种情况导致了**约束**（constraints），即相空间变量之间必须满足的代数关系。处理这类系统的标准方法是**狄拉克-贝格曼程序**（Dirac-Bergmann procedure）。

#### 约束的来源与分类

当 Hessian 矩阵 $\frac{\partial^2\mathcal{L}}{\partial \dot{\phi}_a \partial \dot{\phi}_b}$ 的行列式为零时，拉格朗日量是奇异的。这意味着至少有一个正则动量 $\pi_a$ 的定义不依赖于任何时间导数 $\dot{\phi}_b$。这样的关系 $\pi_a - f(\phi) = 0$ 被称为**主约束**（primary constraint），记为 $\Phi_a \approx 0$。符号 "$\approx$" 表示“弱等于”，意味着这个等式只在物理状态上成立。

物理上，约束必须在时间演化中保持。要求主约束的时间导数为零，即 $\dot{\Phi}_a = \{\Phi_a, H_T\} \approx 0$（其中 $H_T$ 是包含主约束的总哈密顿量），可能会产生新的约束，称为**次级约束**（secondary constraints）。这个过程需要一直迭代，直到不再产生新的约束为止。

所有这些约束可以被分为两类：
1.  **第一类约束**（First-class constraints）：其与所有其他约束的泊松括号在约束曲面上弱等于零。第一类约束是规范变换的生成元。
2.  **第二类约束**（Second-class constraints）：不满足上述条件的约束。每一对第二类约束都代表相空间中的一个冗余自由度，可以在量子化之前通过引入狄拉克括号来消除。

#### 物理自由度的计数

约束的存在减少了系统的独立自由度。相空间中的物理态必须满足所有约束。物理自由度（propagating degrees of freedom）的数量可以通过以下公式计算：

$$
N_{\text{phys}} = \frac{1}{2} \left( N_{\text{phase}} - 2 N_{\text{1st}} - N_{\text{2nd}} \right)
$$

其中 $N_{\text{phase}}$ 是初始相空间的维度，$N_{\text{1st}}$ 是第一类约束的数量，$N_{\text{2nd}}$ 是第二类约束的数量。

以一个反对称2-形式张量场 $B_{\mu\nu}$ 为例 ([@problem_id:327260])，这个理论描述了弦论中的卡尔布-拉蒙场（Kalb-Ramond field）。哈密顿分析揭示了三条主约束 $\Pi^{0i} \approx 0$ 和三条次级约束 $\partial_j \Pi^{ji} \approx 0$。这些约束都是第一类的（尽管存在一个依赖关系，使得独立的第一类约束只有5个）。通过仔细计数，我们发现 $D=4$ 维时空中的 $B_{\mu\nu}$ 场只描述了 **一个** 物理标量自由度。

#### 广义相对论：一个完全约束的系统

广义相对论（GR）是约束哈密顿系统的终极范例。在 ADM (Arnowitt-Deser-Misner) 形式主义中，时空被分解为空间切片。度规分量 $g_{0\mu}$（即**移位函数** $N$ 和**滑移矢量** $N^i$）没有对应的共轭动量，它们本身就是拉格朗日乘子。

对爱因斯坦-希尔伯特作用量进行勒让德变换后发现，哈密顿量完全由约束构成：

$$
H = \int d^3x (N \mathcal{H} + N_i \mathcal{H}^i)
$$

其中 $\mathcal{H} \approx 0$ 被称为**哈密顿约束**（或标量约束），而 $\mathcal{H}^i \approx 0$ 被称为**动量约束**（或矢量约束）。这些约束的消失是爱因斯坦场方程的一部分。例如，在 (2+1) 维真空中，可以明确地证明，通过勒让德变换得到的哈密顿约束密度 $\mathcal{H}$ 与从协变场方程导出的标量约束 $C = R^{(2)} + K^2 - K_{ij}K^{ij}$ 直接成正比 ([@problem_id:327239])。这深刻地表明，在广义相对论中，没有外部的“时间演化”，动力学本身就是由约束所生成的规范变换（坐标变换）所驱动的。即使在线性化的引力理论中，我们也可以看到这些约束的具体形式，例如，哈密顿约束表现为对时空度规扰动 $\bar{h}_{ij}$ 的一个复杂的二阶微分算子 ([@problem_id:327195])。

总之，哈密顿形式主义不仅为正则量子化提供了基础，而且通过其对约束的精细处理，为我们理解规范理论和引力的深刻结构提供了无可替代的工具。