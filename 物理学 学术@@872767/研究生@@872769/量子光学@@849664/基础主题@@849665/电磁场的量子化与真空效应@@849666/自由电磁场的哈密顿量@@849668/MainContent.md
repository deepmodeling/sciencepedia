## 引言
在量子世界中，光既是波又是粒子。将麦克斯韦的经典电磁理论与量子力学相结合，是现代物理学的核心任务之一。这一任务的基石，便是为[电磁场](@entry_id:265881)构建一个量子化的能量描述——即[自由电磁场的哈密顿量](@entry_id:182976)。它不仅是[量子光学](@entry_id:140582)和[量子场论](@entry_id:138177)的出发点，更是我们理解[光子](@entry_id:145192)、真空以及[光与物质相互作用](@entry_id:142166)的根本语言。

然而，如何从描述连续场的麦克斯韦方程，过渡到描述离[散光](@entry_id:174378)子的[量子算符](@entry_id:137703)？能量在这一转变中扮演了什么角色？本文旨在系统地回答这些问题，揭示从经典场到量子[哈密顿量](@entry_id:172864)的完整路径。

为实现这一目标，本文将分为三个核心部分。在“原理与机制”一章中，我们将追溯从经典拉格朗日密度到量子化[哈密顿量](@entry_id:172864)的推导过程，阐明将场模式视为[量子谐振子](@entry_id:140678)的核心思想。接下来，在“应用与跨学科联系”一章中，我们将展示这一基本[哈密顿量](@entry_id:172864)如何解释从[卡西米尔效应](@entry_id:148651)到凝聚态系统中的演生[光子](@entry_id:145192)等广泛的物理现象，彰显其强大的预测能力和跨学科的重要性。最后，通过“动手实践”部分，读者将有机会通过具体计算，加深对[哈密顿量](@entry_id:172864)物理意义和动力学作用的理解。

## 原理与机制

在本章中，我们将深入探讨[自由电磁场的哈密顿量](@entry_id:182976)，这是量子光学领域的基石。我们的目标是从[经典场论](@entry_id:149475)出发，逐步建立起[电磁场的量子化](@entry_id:155376)图像，并揭示其核心的物理原理与机制。这一过程不仅为我们提供了描述[光子](@entry_id:145192)的语言，也揭示了真空等基本概念的深刻内涵。

### 从经典场到[哈密顿量](@entry_id:172864)：光的能量

在量子力学中，系统的[哈密顿量](@entry_id:172864)代表其总能量，其[本征值](@entry_id:154894)对应于系统可能的能量测量结果。为了将电磁[场量子化](@entry_id:160906)，我们首先需要为其建立一个哈密顿形式的经典描述。这需要我们借助拉格朗日和哈密顿场论的强大形式体系。

我们考虑在真空中没有[电荷](@entry_id:275494)和电流的自由[电磁场](@entry_id:265881)。通过选择合适的规范，例如[库仑规范](@entry_id:273044)（$\nabla \cdot \mathbf{A} = 0$），[标量势](@entry_id:276177)$\phi$可以被设为零。此时，场的全部动力学行为都可以由矢量势$\mathbf{A}(t, \mathbf{x})$描述。在这种情况下，系统的拉格朗日密度$\mathcal{L}$可以写作[电场能量密度](@entry_id:261497)与[磁场能量](@entry_id:267501)密度之差：

$$
\mathcal{L} = \frac{\epsilon_0}{2} \left(\frac{\partial \mathbf{A}}{\partial t}\right)^2 - \frac{1}{2\mu_0} (\nabla \times \mathbf{A})^2
$$

其中 $\epsilon_0$ 是[真空介电常数](@entry_id:204253)，$\mu_0$ 是[真空磁导率](@entry_id:186031)。在[场论](@entry_id:155241)中，矢量势$\mathbf{A}$的分量$A_i$扮演着[广义坐标](@entry_id:156576)的角色，而其时间导数 $\dot{A}_i = \partial A_i / \partial t$ 则是[广义速度](@entry_id:178456)。

为了得到[哈密顿量](@entry_id:172864)，我们首先需要定义与[广义坐标](@entry_id:156576)$A_i$共轭的**[正则动量](@entry_id:155151)密度** $\pi^i$。其定义为拉格朗日密度对[广义速度](@entry_id:178456)的[偏导数](@entry_id:146280)：

$$
\pi^i = \frac{\partial \mathcal{L}}{\partial \dot{A}_i} = \frac{\partial}{\partial \dot{A}_i} \left[ \frac{\epsilon_0}{2} \sum_{j} (\dot{A}_j)^2 - \frac{1}{2\mu_0} (\nabla \times \mathbf{A})^2 \right] = \epsilon_0 \dot{A}_i
$$

在矢量形式下，我们得到 $\boldsymbol{\pi} = \epsilon_0 \dot{\mathbf{A}}$。回顾[电场](@entry_id:194326)与矢量势的关系 $\mathbf{E} = -\partial \mathbf{A} / \partial t = -\dot{\mathbf{A}}$，我们发现一个至关重要的联系：[正则动量](@entry_id:155151)密度正比于负的[电场](@entry_id:194326)强度，$\boldsymbol{\pi} = -\epsilon_0 \mathbf{E}$。这个关系是连接[场论](@entry_id:155241)形式体系与[电磁场](@entry_id:265881)物理量的桥梁。

接下来，我们通过对拉格朗日密度进行[勒让德变换](@entry_id:146727)来构造**哈密顿密度** $\mathcal{H}$：

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

这个结果毫不意外，它正是我们熟知的[电磁场能量](@entry_id:265463)密度表达式。这证实了哈密顿密度确实代表了场的能量密度。系统的总[哈密顿量](@entry_id:172864)$H$就是哈密顿密度在整个空间上的积分 $H = \int \mathcal{H} d^3x$。值得注意的是，即使我们从更高级的、相对论协变的拉格朗日密度 $\mathcal{L} = -\frac{1}{4} F_{\mu\nu} F^{\mu\nu}$ 出发，采用不同的规范（如时间规范 $A_0 = 0$），经过类似的正则程序，最终得到的哈密顿密度在物理上也是等价的 [@problem_id:66994]。这表明此能量表达式具有深刻的物理普适性。

### 场的分解：横场辐射与[库仑相互作用](@entry_id:747947)

在深入量子化之前，理解[哈密顿量](@entry_id:172864)的结构至关重要，特别是当存在[电荷](@entry_id:275494)源时。根据[亥姆霍兹定理](@entry_id:275687)，任何矢量场（在此为[正则动量](@entry_id:155151)场 $\boldsymbol{\Pi}$）都可以唯一地分解为一个无散度的**横向分量** $\boldsymbol{\Pi}_{\perp}$（$\nabla \cdot \boldsymbol{\Pi}_{\perp} = 0$）和一个无旋度的**纵向分量** $\boldsymbol{\Pi}_{\|}$（$\nabla \times \boldsymbol{\Pi}_{\|} = 0$）。

在电动力学中，[高斯定律](@entry_id:141493)作为一个约束条件出现，它将[正则动量](@entry_id:155151)的散度与[电荷密度](@entry_id:144672) $\rho$ 联系起来：$\nabla \cdot \mathbf{E} = \rho / \epsilon_0$。由于 $\boldsymbol{\pi} = -\epsilon_0 \mathbf{E}$ (在无源自由场中)，推广到有源情况，我们有 $\boldsymbol{\Pi} = -\epsilon_0 \mathbf{E}$，因此高斯定律约束可以写成 $\nabla \cdot \boldsymbol{\Pi} = -\rho$。

将 $\boldsymbol{\Pi}$ 分解为横向和纵向部分，我们看到 $\nabla \cdot \boldsymbol{\Pi} = \nabla \cdot (\boldsymbol{\Pi}_{\perp} + \boldsymbol{\Pi}_{\|}) = \nabla \cdot \boldsymbol{\Pi}_{\|} = -\rho$。这表明，纵向动量完全由瞬时的[电荷分布](@entry_id:144400)决定，它不代表一个独立的、可传播的动力学自由度。相反，横向动量满足 $\nabla \cdot \boldsymbol{\Pi}_{\perp} = 0$，它代表了与[电荷](@entry_id:275494)源无关的、能够自由传播的辐射场。

场的能量密度项 $\frac{1}{2\epsilon_0}\boldsymbol{\Pi}^2$ 也随之分解。由于横向和纵向分量在空间上是正交的，积分后我们有：
$$
\int \frac{1}{2\epsilon_0} \boldsymbol{\Pi}^2 d^3\mathbf{r} = \int \frac{1}{2\epsilon_0} \boldsymbol{\Pi}_{\perp}^2 d^3\mathbf{r} + \int \frac{1}{2\epsilon_0} \boldsymbol{\Pi}_{\|}^2 d^3\mathbf{r}
$$
后一项，即[纵向场](@entry_id:264833)能量 $U_{\|}$，可以被证明恰好等于整个[电荷分布](@entry_id:144400)的[瞬时库仑相互作用](@entry_id:196309)能 [@problem_id:756413]。例如，对于一个半径为 $a$、总电量为 $Q$ 的均匀带电球体，其[静电自能](@entry_id:177518)为 $\frac{3Q^2}{20\pi\epsilon_0 a}$，这正是 $U_{\|}$ 的计算结果。

这一分解揭示了一个深刻的物理图像：[电磁场](@entry_id:265881)的[哈密顿量](@entry_id:172864)可以分离为两部分。一部分是与[电荷](@entry_id:275494)瞬时耦合的[纵向场](@entry_id:264833)，其能量是静态的[库仑能](@entry_id:161936)；另一部分是代表自由传播的[电磁波](@entry_id:269629)（光）的[横向场](@entry_id:266489)。因此，当我们讨论**自由[电磁场](@entry_id:265881)**的量子化时，我们真正关注的是**[横向场](@entry_id:266489)**的动力学自由度，其[哈密顿量](@entry_id:172864)为：

$$
H_{\text{rad}} = \int \left( \frac{1}{2\epsilon_0} \mathbf{E}_{\perp}^2 + \frac{1}{2\mu_0} \mathbf{B}^2 \right) d^3\mathbf{r}
$$
其中[磁场](@entry_id:153296) $\mathbf{B}$ 天然是横向的（$\nabla \cdot \mathbf{B} = 0$）。

### 量子化：从场模式到谐振子

量子化[电磁场](@entry_id:265881)的中心思想，是将场的每一个独立的[振动](@entry_id:267781)模式视为一个独立的量子谐振子。为了直观地理解这一点，我们可以考虑一个被理想导体壁包围的一维腔体 [@problem_id:756264]。腔内的[电磁场](@entry_id:265881)可以被分解为一系列驻波模式。

例如，对于其中一个特定的[横向模式](@entry_id:163265)，其矢量势可以写成 $\mathbf{A}(x, t) = \hat{y} \mathcal{N} \sin(kx) q(t)$，其中 $q(t)$ 是描述该模式振幅随时间变化的[广义坐标](@entry_id:156576)。通过计算该模式的总能量（即[哈密顿量](@entry_id:172864)），我们会发现它具有一个熟悉的形式：

$$
H_{\text{mode}} = \frac{1}{2}M \dot{q}^2 + \frac{1}{2}M\omega^2 q^2
$$

这里的“质量”$M$和“频率”$\omega$是由腔体几何形状和物理常数（如 $\epsilon_0, S, L$）决定的参数。这个表达式正是标准的一维[谐振子](@entry_id:155622)的[哈密顿量](@entry_id:172864)。

这一发现是量子化的关键。我们可以直接套用量子力学中谐振子的量子化方法：将[广义坐标](@entry_id:156576) $q$ 和其[共轭动量](@entry_id:172203) $p = M\dot{q}$ 提升为满足对易关系 $[\hat{q}, \hat{p}] = i\hbar$ 的算符。然后，可以引入更方便的**[产生算符](@entry_id:191512)** $\hat{a}^\dagger$ 和**[湮灭算符](@entry_id:165390)** $\hat{a}$：

$$
\hat{q} = \sqrt{\frac{\hbar}{2M\omega}}(\hat{a} + \hat{a}^\dagger), \quad \hat{p} = i\sqrt{\frac{\hbar M\omega}{2}}(\hat{a}^\dagger - \hat{a})
$$

它们满足[对易关系](@entry_id:136780) $[\hat{a}, \hat{a}^\dagger] = 1$。用这些算符表示后，该模式的[哈密顿量](@entry_id:172864)就变成了量子谐振子的[标准形式](@entry_id:153058)：

$$
\hat{H}_{\text{mode}} = \hbar\omega \left(\hat{a}^\dagger \hat{a} + \frac{1}{2}\right)
$$

### 自由场的量子[哈密顿量](@entry_id:172864)

现在，我们将这个思想从单个腔体模式推广到自由空间中的整个[电磁场](@entry_id:265881)。自由空间可以看作一个无限大的腔体，其模式不再是分立的驻波，而是由波矢 $\mathbf{k}$ 和偏振 $\lambda$ 标记的连续的[平面波](@entry_id:189798)。场的每一个模式 $(\mathbf{k}, \lambda)$ 都对应一个独立的[量子谐振子](@entry_id:140678)。

因此，自由[电磁场](@entry_id:265881)的总[哈密顿量](@entry_id:172864)是所有这些无穷多个谐振子能量的总和：

$$
\hat{H} = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \left( \hat{a}_{\mathbf{k}, \lambda}^{\dagger} \hat{a}_{\mathbf{k}, \lambda} + \frac{1}{2} \right)
$$

其中 $\hat{a}_{\mathbf{k}, \lambda}$ 和 $\hat{a}_{\mathbf{k}, \lambda}^{\dagger}$ 分别是湮灭和产生模式 $(\mathbf{k}, \lambda)$ 的一个[光量子](@entry_id:173025)的算符，它们满足[对易关系](@entry_id:136780)，如 $[\hat{a}_{\mathbf{k}, \lambda}, \hat{a}_{\mathbf{k}', \lambda'}^\dagger] = \delta_{\mathbf{k}, \mathbf{k}'} \delta_{\lambda, \lambda'}$ （对于离散模式）或包含狄拉克delta函数的形式（对于[连续模](@entry_id:158807)式）。

这个[哈密顿量](@entry_id:172864)是对[电磁场](@entry_id:265881)的完整量子描述。场的算符，如[电场算符](@entry_id:196320) $\hat{\mathbf{E}}(\mathbf{r})$ 和磁[场算符](@entry_id:140269) $\hat{\mathbf{B}}(\mathbf{r})$，现在可以表示为所有模式的产生和湮灭算符的叠加 [@problem_id:711806]。

有趣的是，我们可以反向验证这一过程。如果我们从经典的[能量积分](@entry_id:166228) $H = \int \mathcal{H} d^3x$ 出发，并将场的[量子算符](@entry_id:137703)表达式代入，我们会发现结果是：

$$
\hat{H} = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \hat{a}_{\mathbf{k}, \lambda}^{\dagger} \hat{a}_{\mathbf{k}, \lambda} + \sum_{\mathbf{k}, \lambda} \frac{1}{2}\hbar \omega_k
$$

第二项是所有模式的[零点能](@entry_id:142176)之和，由于模式有无穷多个，这是一个发散的、无限大的常数。为了解决这个问题，物理学家引入了**[正规排序](@entry_id:145434)**（Normal Ordering）的约定，记作 $:\dots:$。[正规排序](@entry_id:145434)的作用是重新[排列](@entry_id:136432)一个算符乘积，将所有的[产生算符](@entry_id:191512)移动到所有[湮灭算符](@entry_id:165390)的左边。例如，$:\hat{a}\hat{a}^\dagger: = \hat{a}^\dagger\hat{a}$。当[正规排序](@entry_id:145434)作用于[哈密顿量](@entry_id:172864)时，它有效地移除了这个无限大的常数项，因为它不包含任何 $\hat{a}^\dagger\hat{a}$ 形式的项。这样，我们重新定义了一个以[真空能](@entry_id:155067)为零点的[哈密顿量](@entry_id:172864) [@problem_id:711806]：

$$
\hat{H} = \frac{1}{2}\int d^3x :\!\left( \epsilon_0 \hat{\mathbf{E}}^2(\mathbf{r}) + \frac{1}{\mu_0} \hat{\mathbf{B}}^2(\mathbf{r}) \right)\!: = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \hat{a}_{\mathbf{k}, \lambda}^{\dagger} \hat{a}_{\mathbf{k}, \lambda}
$$

### 量子[哈密顿量](@entry_id:172864)的属性与推论

[正规排序](@entry_id:145434)后的[哈密顿量](@entry_id:172864)简洁而优美，它蕴含了丰富的物理内容。

#### [光的粒子性](@entry_id:150555)：[光子](@entry_id:145192)

[哈密顿量](@entry_id:172864)的对角化形式 $\hat{H} = \sum_{\mathbf{k}, \lambda} \hbar \omega_k \hat{N}_{\mathbf{k}, \lambda}$，其中 $\hat{N}_{\mathbf{k}, \lambda} = \hat{a}_{\mathbf{k}, \lambda}^{\dagger} \hat{a}_{\mathbf{k}, \lambda}$ 被称为**[粒子数算符](@entry_id:153568)**。它的[本征值](@entry_id:154894)是 $0, 1, 2, \dots$，表示模式 $(\mathbf{k}, \lambda)$ 中能量量子的数量。

- **真空态** $|0\rangle$ 是系统的[基态](@entry_id:150928)，被定义为没有任何量子的状态，即对所有模式都有 $\hat{a}_{\mathbf{k}, \lambda}|0\rangle = 0$。它的能量为零。
- **单[光子](@entry_id:145192)态**：当[产生算符](@entry_id:191512) $\hat{a}_{\mathbf{k}_0, \lambda_0}^{\dagger}$ 作用于真空态时，它会创建一个新的状态 $|\psi_{\mathbf{k}_0, \lambda_0}\rangle = \hat{a}_{\mathbf{k}_0, \lambda_0}^{\dagger} |0\rangle$。通过计算可知，这个新状态是[哈密顿量](@entry_id:172864)的本征态，其能量恰好比真空态高出 $\hbar \omega_{\mathbf{k}_0}$ [@problem_id:717275]。这个能量为 $\hbar \omega_{\mathbf{k}_0}$ 的能量量子，就是我们所说的**[光子](@entry_id:145192)**。

因此，量子[哈密顿量](@entry_id:172864)清晰地描绘了光的粒子图像：[电磁场](@entry_id:265881)的总能量是所有[光子能量](@entry_id:139314)的总和。

#### 零点能问题

尽管[正规排序](@entry_id:145434)将真空的能量重置为零，但底层的谐振子模型依然预示着每个模式都拥有一个不可消除的[基态能量](@entry_id:263704)，即**零点能** $\frac{1}{2}\hbar\omega_k$。所有模式的零点能之和 $E_0 = \sum_{\mathbf{k}, \lambda} \frac{1}{2}\hbar\omega_k$ 导致了发散的**真空能量密度**。

这是一个理论物理学中的重大难题，与宇宙学中的[宇宙学常数问题](@entry_id:154962)密切相关。虽然这个无限大的能量通常在计算可观测效应时被忽略，但它的存在本身就是一个深刻的谜团。在理论计算中，可以通过引入一个高能截断（regularization）来获得一个有限的（但依赖于截断标度）结果。例如，可以假设在高频处能量贡献被一个指数因子 $e^{-\omega_k / \Omega}$ 压低，或者假设[色散关系](@entry_id:140395)本身在高能时发生改变 [@problem_id:756347] [@problem_id:327317]。这些方法虽然是人为的，但它们是处理[量子场论](@entry_id:138177)中无穷大的重要工具。

#### [守恒量](@entry_id:150267)

除了能量，场的总动量也是一个重要的物理量。场的总[动量算符](@entry_id:151743)可以表示为：

$$
\mathbf{P} = \sum_{\mathbf{k}, \lambda} \hbar \mathbf{k} \, \hat{a}^\dagger_{\mathbf{k}, \lambda} \hat{a}_{\mathbf{k}, \lambda}
$$

这个表达式的物理意义很明确：总动量是所有[光子](@entry_id:145192)动量（$\hbar \mathbf{k}$）的总和。通过直接计算可以证明，[哈密顿量](@entry_id:172864)与动量算符的任意分量都是对易的，即 $[\hat{H}, \hat{P}_j] = 0$ [@problem_id:756384]。这意味着能量和动量是守恒量，并且可以被同时确定。一个具有确定能量的系统（[哈密顿量](@entry_id:172864)的[本征态](@entry_id:149904)）也可以处于一个具有确定动量的状态。这反映了自由空间中时间和空间平移的对称性。

#### 场动力学与[真空涨落](@entry_id:154889)

在[海森堡绘景](@entry_id:141162)中，算符随[时间演化](@entry_id:153943)。利用[海森堡运动方程](@entry_id:140445) $\frac{d\hat{O}}{dt} = \frac{1}{i\hbar}[\hat{O}, \hat{H}]$，我们可以求出[湮灭算符](@entry_id:165390)的时间演化：

$$
\frac{d\hat{a}_{\mathbf{k}, \lambda}}{dt} = \frac{1}{i\hbar}[\hat{a}_{\mathbf{k}, \lambda}, \hat{H}] = -i\omega_k \hat{a}_{\mathbf{k}, \lambda}
$$

其解为 $\hat{a}_{\mathbf{k}, \lambda}(t) = \hat{a}_{\mathbf{k}, \lambda}(0) e^{-i\omega_k t}$，这正是一个[经典谐振子](@entry_id:153404)的[时间演化](@entry_id:153943)行为 [@problem_id:756323]。

[量子场论](@entry_id:138177)一个最令人惊讶的推论是**真空涨落**。尽管真空态 $|0\rangle$ 的平均[电场和磁场](@entry_id:261347)为零（$\langle 0 | \hat{\mathbf{E}}(\mathbf{r},t) | 0 \rangle = 0$），但场的平方的[期望值](@entry_id:153208)却不为零（$\langle 0 | \hat{\mathbf{E}}^2(\mathbf{r},t) | 0 \rangle \neq 0$）。这意味着即使在没有[光子](@entry_id:145192)的“空无一物”的真空中，[电磁场](@entry_id:265881)也在不停地随机起伏。

这些[真空涨落](@entry_id:154889)具有可观测的物理效应，例如兰姆移位和[卡西米尔效应](@entry_id:148651)。我们甚至可以计算这些涨落的特性。例如，在之前的一维腔体模型中，可以计算出真空中电场和磁场涨落的乘积 $\Delta E_y \Delta B_z$，它是一个与 $\hbar$ 成正比的非零值，体现了不确定性原理 [@problem_id:756264]。同样，我们也可以计算真空中的两点时间关联函数，如 $\langle 0 | \hat{X}(t) \hat{X}(0) | 0 \rangle$（其中 $\hat{X}$ 是场的某个分量），它会显示出由模式频率 $\omega$ 决定的[振荡](@entry_id:267781)衰减行为，表明真空涨落不是完全无序的，而是具有内在的[时空结构](@entry_id:158931) [@problem_id:756323]。

综上所述，[自由电磁场的哈密顿量](@entry_id:182976)不仅为我们提供了描述[光子](@entry_id:145192)世界的数学工具，也引领我们一窥真空的奥秘，揭示了看似空无的空间中蕴含的丰富物理内涵。