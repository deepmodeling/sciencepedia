## 引言
在量子世界中，光既是波又是粒子。将麦克斯韦的经典电磁理论与量子力学相结合，是现代物理学的核心任务之一。这一任务的基石，便是为电磁场构建一个量子化的能量描述——即自由电磁场的哈密顿量。它不仅是量子光学和量子场论的出发点，更是我们理解光子、真空以及光与物质相互作用的根本语言。

然而，如何从描述连续场的麦克斯韦方程，过渡到描述离散光子的量子算符？能量在这一转变中扮演了什么角色？本文旨在系统地回答这些问题，揭示从经典场到量子哈密顿量的完整路径。

为实现这一目标，本文将分为三个核心部分。在“原理与机制”一章中，我们将追溯从经典拉格朗日密度到量子化哈密顿量的推导过程，阐明将场模式视为量子谐振子的核心思想。接下来，在“应用与跨学科联系”一章中，我们将展示这一基本哈密顿量如何解释从卡西米尔效应到凝聚态系统中的演生光子等广泛的物理现象，彰显其强大的预测能力和跨学科的重要性。最后，通过“动手实践”部分，读者将有机会通过具体计算，加深对哈密顿量物理意义和动力学作用的理解。

## 原理与机制

在本章中，我们将深入探讨自由电磁场的哈密顿量，这是量子光学领域的基石。我们的目标是从经典场论出发，逐步建立起电磁场的量子化图像，并揭示其核心的物理原理与机制。这一过程不仅为我们提供了描述光子的语言，也揭示了真空等基本概念的深刻内涵。

### 从经典场到哈密顿量：光的能量

在量子力学中，系统的哈密顿量代表其总能量，其本征值对应于系统可能的能量测量结果。为了将电磁场量子化，我们首先需要为其建立一个哈密顿形式的经典描述。这需要我们借助拉格朗日和哈密顿场论的强大形式体系。

我们考虑在真空中没有电荷和电流的自由电磁场。通过选择合适的规范，例如库仑规范（$\nabla \cdot \mathbf{A} = 0$），标量势$\phi$可以被设为零。此时，场的全部动力学行为都可以由矢量势$\mathbf{A}(t, \mathbf{x})$描述。在这种情况下，系统的拉格朗日密度$\mathcal{L}$可以写作电场能量密度与磁场能量密度之差：

$$
\mathcal{L} = \frac{\epsilon_0}{2} \left(\frac{\partial \mathbf{A}}{\partial t}\right)^2 - \frac{1}{2\mu_0} (\nabla \times \mathbf{A})^2
$$

其中 $\epsilon_0$ 是真空介电常数，$\mu_0$ 是真空磁导率。在场论中，矢量势$\mathbf{A}$的分量$A_i$扮演着广义坐标的角色，而其时间导数 $\dot{A}_i = \partial A_i / \partial t$ 则是广义速度。

为了得到哈密顿量，我们首先需要定义与广义坐标$A_i$共轭的**正则动量密度** $\pi^i$。其定义为拉格朗日密度对广义速度的偏导数：

$$
\pi^i = \frac{\partial \mathcal{L}}{\partial \dot{A}_i} = \frac{\partial}{\partial \dot{A}_i} \left[ \frac{\epsilon_0}{2} \sum_{j} (\dot{A}_j)^2 - \frac{1}{2\mu_0} (\nabla \times \mathbf{A})^2 \right] = \epsilon_0 \dot{A}_i
$$

在矢量形式下，我们得到 $\boldsymbol{\pi} = \epsilon_0 \dot{\mathbf{A}}$。回顾电场与矢量势的关系 $\mathbf{E} = -\partial \mathbf{A} / \partial t = -\dot{\mathbf{A}}$，我们发现一个至关重要的联系：正则动量密度正比于负的电场强度，$\boldsymbol{\pi} = -\epsilon_0 \mathbf{E}$。这个关系是连接场论形式体系与电磁场物理量的桥梁。

接下来，我们通过对拉格朗日密度进行勒让德变换来构造**哈密顿密度** $\mathcal{H}$：

$$
\mathcal{H} = \sum_i \pi^i \dot{A}_i - \mathcal{L} = \boldsymbol{\pi} \cdot \dot{\mathbf{A}} - \mathcal{L}
$$

将 $\boldsymbol{\pi} = \epsilon_0 \dot{\mathbf{A}}$ 和 $\mathcal{L}$ 的表达式代入，我们得到：

$$
\mathcal{H} = (\epsilon_0 \dot{\mathbf{A}}) \cdot \dot{\mathbf{A}} - \left[ \frac{\epsilon_0}{2} \dot{\mathbf{A}}^2 - \frac{1}{2\mu_0} (\nabla \times \mathbf{A})^2 \right] = \frac{\epsilon_0}{2} \dot{\mathbf{A}}^2 + \frac{1}{2\mu_0} (\nabla \times \mathbf{A})^2
$$

最后，利用电场和磁场的定义（$\mathbf{E} = -\dot{\mathbf{A}}$ 和 $\mathbf{B} = \nabla \times \mathbf{A}$），我们可以将哈密顿密度完全用物理场表示 [@problem_id:2086079] [@problem_id:2071097]：

$$
\mathcal{H} = \frac{\epsilon_0}{2} \mathbf{E}^2 + \frac{1}{2\mu_0} \mathbf{B}^2
$$

这个结果毫不意外，它正是我们熟知的电磁场能量密度表达式。这证实了哈密顿密度确实代表了场的能量密度。系统的总哈密顿量$H$就是哈密顿密度在整个空间上的积分 $H = \int \mathcal{H} d^3x$。值得注意的是，即使我们从更高级的、相对论协变的拉格朗日密度 $\mathcal{L} = -\frac{1}{4} F_{\mu\nu} F^{\mu\nu}$ 出发，采用不同的规范（如时间规范 $A_0 = 0$），经过类似的正则程序，最终得到的哈密顿密度在物理上也是等价的 [@problem_id:66994]。这表明此能量表达式具有深刻的物理普适性。

### 场的分解：横场辐射与库仑相互作用

在深入量子化之前，理解哈密顿量的结构至关重要，特别是当存在电荷源时。根据亥姆霍兹定理，任何矢量场（在此为正则动量场 $\boldsymbol{\Pi}$）都可以唯一地分解为一个无散度的**横向分量** $\boldsymbol{\Pi}_{\perp}$（$\nabla \cdot \boldsymbol{\Pi}_{\perp} = 0$）和一个无旋度的**纵向分量** $\boldsymbol{\Pi}_{\|}$（$\nabla \times \boldsymbol{\Pi}_{\|} = 0$）。

在电动力学中，高斯定律作为一个约束条件出现，它将正则动量的散度与电荷密度 $\rho$ 联系起来：$\nabla \cdot \mathbf{E} = \rho / \epsilon_0$。由于 $\boldsymbol{\pi} = -\epsilon_0 \mathbf{E}$ (在无源自由场中)，推广到有源情况，我们有 $\boldsymbol{\Pi} = -\epsilon_0 \mathbf{E}$，因此高斯定律约束可以写成 $\nabla \cdot \boldsymbol{\Pi} = -\rho$。

将 $\boldsymbol{\Pi}$ 分解为横向和纵向部分，我们看到 $\nabla \cdot \boldsymbol{\Pi} = \nabla \cdot (\boldsymbol{\Pi}_{\perp} + \boldsymbol{\Pi}_{\|}) = \nabla \cdot \boldsymbol{\Pi}_{\|} = -\rho$。这表明，纵向动量完全由瞬时的电荷分布决定，它不代表一个独立的、可传播的动力学自由度。相反，横向动量满足 $\nabla \cdot \boldsymbol{\Pi}_{\perp} = 0$，它代表了与电荷源无关的、能够自由传播的辐射场。

场的能量密度项 $\frac{1}{2\epsilon_0}\boldsymbol{\Pi}^2$ 也随之分解。由于横向和纵向分量在空间上是正交的，积分后我们有：
$$
\int \frac{1}{2\epsilon_0} \boldsymbol{\Pi}^2 d^3\mathbf{r} = \int \frac{1}{2\epsilon_0} \boldsymbol{\Pi}_{\perp}^2 d^3\mathbf{r} + \int \frac{1}{2\epsilon_0} \boldsymbol{\Pi}_{\|}^2 d^3\mathbf{r}
$$
后一项，即纵向场能量 $U_{\|}$，可以被证明恰好等于整个电荷分布的瞬时库仑相互作用能 [@problem_id:756413]。例如，对于一个半径为 $a$、总电量为 $Q$ 的均匀带电球体，其静电自能为 $\frac{3Q^2}{20\pi\epsilon_0 a}$，这正是 $U_{\|}$ 的计算结果。

这一分解揭示了一个深刻的物理图像：电磁场的哈密顿量可以分离为两部分。一部分是与电荷瞬时耦合的纵向场，其能量是静态的库仑能；另一部分是代表自由传播的电磁波（光）的横向场。因此，当我们讨论**自由电磁场**的量子化时，我们真正关注的是**横向场**的动力学自由度，其哈密顿量为：

$$
H_{\text{rad}} = \int \left( \frac{1}{2\epsilon_0} \mathbf{E}_{\perp}^2 + \frac{1}{2\mu_0} \mathbf{B}^2 \right) d^3\mathbf{r}
$$
其中磁场 $\mathbf{B}$ 天然是横向的（$\nabla \cdot \mathbf{B} = 0$）。

### 量子化：从场模式到谐振子

量子化电磁场的中心思想，是将场的每一个独立的振动模式视为一个独立的量子谐振子。为了直观地理解这一点，我们可以考虑一个被理想导体壁包围的一维腔体 [@problem_id:756264]。腔内的电磁场可以被分解为一系列驻波模式。

例如，对于其中一个特定的横向模式，其矢量势可以写成 $\mathbf{A}(x, t) = \hat{y} \mathcal{N} \sin(kx) q(t)$，其中 $q(t)$ 是描述该模式振幅随时间变化的广义坐标。通过计算该模式的总能量（即哈密顿量），我们会发现它具有一个熟悉的形式：

$$
H_{\text{mode}} = \frac{1}{2}M \dot{q}^2 + \frac{1}{2}M\omega^2 q^2
$$

这里的“质量”$M$和“频率”$\omega$是由腔体几何形状和物理常数（如 $\epsilon_0, S, L$）决定的参数。这个表达式正是标准的一维谐振子的哈密顿量。

这一发现是量子化的关键。我们可以直接套用量子力学中谐振子的量子化方法：将广义坐标 $q$ 和其共轭动量 $p = M\dot{q}$ 提升为满足对易关系 $[\hat{q}, \hat{p}] = i\hbar$ 的算符。然后，可以引入更方便的**产生算符** $\hat{a}^\dagger$ 和**湮灭算符** $\hat{a}$：

$$
\hat{q} = \sqrt{\frac{\hbar}{2M\omega}}(\hat{a} + \hat{a}^\dagger), \quad \hat{p} = i\sqrt{\frac{\hbar M\omega}{2}}(\hat{a}^\dagger - \hat{a})
$$

它们满足对易关系 $[\hat{a}, \hat{a}^\dagger] = 1$。用这些算符表示后，该模式的哈密顿量就变成了量子谐振子的标准形式：

$$
\hat{H}_{\text{mode}} = \hbar\omega \left(\hat{a}^\dagger \hat{a} + \frac{1}{2}\right)
$$

### 自由场的量子哈密顿量

现在，我们将这个思想从单个腔体模式推广到自由空间中的整个电磁场。自由空间可以看作一个无限大的腔体，其模式不再是分立的驻波，而是由波矢 $\mathbf{k}$ 和偏振 $\lambda$ 标记的连续的平面波。场的每一个模式 $(\mathbf{k}, \lambda)$ 都对应一个独立的量子谐振子。

因此，自由电磁场的总哈密顿量是所有这些无穷多个谐振子能量的总和：

$$
\hat{H} = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \left( \hat{a}_{\mathbf{k}, \lambda}^{\dagger} \hat{a}_{\mathbf{k}, \lambda} + \frac{1}{2} \right)
$$

其中 $\hat{a}_{\mathbf{k}, \lambda}$ 和 $\hat{a}_{\mathbf{k}, \lambda}^{\dagger}$ 分别是湮灭和产生模式 $(\mathbf{k}, \lambda)$ 的一个光量子的算符，它们满足对易关系，如 $[\hat{a}_{\mathbf{k}, \lambda}, \hat{a}_{\mathbf{k}', \lambda'}^\dagger] = \delta_{\mathbf{k}, \mathbf{k}'} \delta_{\lambda, \lambda'}$ （对于离散模式）或包含狄拉克delta函数的形式（对于连续模式）。

这个哈密顿量是对电磁场的完整量子描述。场的算符，如电场算符 $\hat{\mathbf{E}}(\mathbf{r})$ 和磁场算符 $\hat{\mathbf{B}}(\mathbf{r})$，现在可以表示为所有模式的产生和湮灭算符的叠加 [@problem_id:711806]。

有趣的是，我们可以反向验证这一过程。如果我们从经典的能量积分 $H = \int \mathcal{H} d^3x$ 出发，并将场的量子算符表达式代入，我们会发现结果是：

$$
\hat{H} = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \hat{a}_{\mathbf{k}, \lambda}^{\dagger} \hat{a}_{\mathbf{k}, \lambda} + \sum_{\mathbf{k}, \lambda} \frac{1}{2}\hbar \omega_k
$$

第二项是所有模式的零点能之和，由于模式有无穷多个，这是一个发散的、无限大的常数。为了解决这个问题，物理学家引入了**正规排序**（Normal Ordering）的约定，记作 $:\dots:$。正规排序的作用是重新排列一个算符乘积，将所有的产生算符移动到所有湮灭算符的左边。例如，$:\hat{a}\hat{a}^\dagger: = \hat{a}^\dagger\hat{a}$。当正规排序作用于哈密顿量时，它有效地移除了这个无限大的常数项，因为它不包含任何 $\hat{a}^\dagger\hat{a}$ 形式的项。这样，我们重新定义了一个以真空能为零点的哈密顿量 [@problem_id:711806]：

$$
\hat{H} = \frac{1}{2}\int d^3x :\!\left( \epsilon_0 \hat{\mathbf{E}}^2(\mathbf{r}) + \frac{1}{\mu_0} \hat{\mathbf{B}}^2(\mathbf{r}) \right)\!: = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \hat{a}_{\mathbf{k}, \lambda}^{\dagger} \hat{a}_{\mathbf{k}, \lambda}
$$

### 量子哈密顿量的属性与推论

正规排序后的哈密顿量简洁而优美，它蕴含了丰富的物理内容。

#### 光的粒子性：光子

哈密顿量的对角化形式 $\hat{H} = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \hat{N}_{\mathbf{k}, \lambda}$，其中 $\hat{N}_{\mathbf{k}, \lambda} = \hat{a}_{\mathbf{k}, \lambda}^{\dagger} \hat{a}_{\mathbf{k}, \lambda}$ 被称为**粒子数算符**。它的本征值是 $0, 1, 2, \dots$，表示模式 $(\mathbf{k}, \lambda)$ 中能量量子的数量。

- **真空态** $|0\rangle$ 是系统的基态，被定义为没有任何量子的状态，即对所有模式都有 $\hat{a}_{\mathbf{k}, \lambda}|0\rangle = 0$。它的能量为零。
- **单光子态**：当产生算符 $\hat{a}_{\mathbf{k}_0, \lambda_0}^{\dagger}$ 作用于真空态时，它会创建一个新的状态 $|\psi_{\mathbf{k}_0, \lambda_0}\rangle = \hat{a}_{\mathbf{k}_0, \lambda_0}^{\dagger} |0\rangle$。通过计算可知，这个新状态是哈密顿量的本征态，其能量恰好比真空态高出 $\hbar \omega_{\mathbf{k}_0}$ [@problem_id:717275]。这个能量为 $\hbar \omega_{\mathbf{k}_0}$ 的能量量子，就是我们所说的**光子**。

因此，量子哈密顿量清晰地描绘了光的粒子图像：电磁场的总能量是所有光子能量的总和。

#### 零点能问题

尽管正规排序将真空的能量重置为零，但底层的谐振子模型依然预示着每个模式都拥有一个不可消除的基态能量，即**零点能** $\frac{1}{2}\hbar\omega_k$。所有模式的零点能之和 $E_0 = \sum_{\mathbf{k}, \lambda} \frac{1}{2}\hbar\omega_k$ 导致了发散的**真空能量密度**。

这是一个理论物理学中的重大难题，与宇宙学中的宇宙学常数问题密切相关。虽然这个无限大的能量通常在计算可观测效应时被忽略，但它的存在本身就是一个深刻的谜团。在理论计算中，可以通过引入一个高能截断（regularization）来获得一个有限的（但依赖于截断标度）结果。例如，可以假设在高频处能量贡献被一个指数因子 $e^{-\omega_k / \Omega}$ 压低，或者假设色散关系本身在高能时发生改变 [@problem_id:756347] [@problem_id:327317]。这些方法虽然是人为的，但它们是处理量子场论中无穷大的重要工具。

#### 守恒量

除了能量，场的总动量也是一个重要的物理量。场的总动量算符可以表示为：

$$
\mathbf{P} = \sum_{\mathbf{k}, \lambda} \hbar \mathbf{k} \, \hat{a}^\dagger_{\mathbf{k}, \lambda} \hat{a}_{\mathbf{k}, \lambda}
$$

这个表达式的物理意义很明确：总动量是所有光子动量（$\hbar \mathbf{k}$）的总和。通过直接计算可以证明，哈密顿量与动量算符的任意分量都是对易的，即 $[\hat{H}, \hat{P}_j] = 0$ [@problem_id:756384]。这意味着能量和动量是守恒量，并且可以被同时确定。一个具有确定能量的系统（哈密顿量的本征态）也可以处于一个具有确定动量的状态。这反映了自由空间中时间和空间平移的对称性。

#### 场动力学与真空涨落

在海森堡绘景中，算符随时间演化。利用海森堡运动方程 $\frac{d\hat{O}}{dt} = \frac{1}{i\hbar}[\hat{O}, \hat{H}]$，我们可以求出湮灭算符的时间演化：

$$
\frac{d\hat{a}_{\mathbf{k}, \lambda}}{dt} = \frac{1}{i\hbar}[\hat{a}_{\mathbf{k}, \lambda}, \hat{H}] = -i\omega_k \hat{a}_{\mathbf{k}, \lambda}
$$

其解为 $\hat{a}_{\mathbf{k}, \lambda}(t) = \hat{a}_{\mathbf{k}, \lambda}(0) e^{-i\omega_k t}$，这正是一个经典谐振子的时间演化行为 [@problem_id:756323]。

量子场论一个最令人惊讶的推论是**真空涨落**。尽管真空态 $|0\rangle$ 的平均电场和磁场为零（$\langle 0 | \hat{\mathbf{E}}(\mathbf{r},t) | 0 \rangle = 0$），但场的平方的期望值却不为零（$\langle 0 | \hat{\mathbf{E}}^2(\mathbf{r},t) | 0 \rangle \neq 0$）。这意味着即使在没有光子的“空无一物”的真空中，电磁场也在不停地随机起伏。

这些真空涨落具有可观测的物理效应，例如兰姆移位和卡西米尔效应。我们甚至可以计算这些涨落的特性。例如，在之前的一维腔体模型中，可以计算出真空中电场和磁场涨落的乘积 $\Delta E_y \Delta B_z$，它是一个与 $\hbar$ 成正比的非零值，体现了不确定性原理 [@problem_id:756264]。同样，我们也可以计算真空中的两点时间关联函数，如 $\langle 0 | \hat{X}(t) \hat{X}(0) | 0 \rangle$（其中 $\hat{X}$ 是场的某个分量），它会显示出由模式频率 $\omega$ 决定的振荡衰减行为，表明真空涨落不是完全无序的，而是具有内在的时空结构 [@problem_id:756323]。

综上所述，自由电磁场的哈密顿量不仅为我们提供了描述光子世界的数学工具，也引领我们一窥真空的奥秘，揭示了看似空无的空间中蕴含的丰富物理内涵。