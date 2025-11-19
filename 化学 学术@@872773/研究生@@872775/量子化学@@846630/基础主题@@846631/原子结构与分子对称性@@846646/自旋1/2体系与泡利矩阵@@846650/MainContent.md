## 引言
自旋是粒子内禀的角动量，是微观世界的基本属性之一。其中，自旋-1/2系统，如电子和质子，是构成我们物质世界和众多现代技术的基石。然而，经典的物理直觉在描述自旋现象时完全失效，它既是量子化的，又表现出[非对易](@entry_id:136599)的奇特性质。为了精确地描述和预测自旋的行为，我们需要一个严谨而强大的量子力学框架。本文旨在系统性地解决这一问题，为读者构建一个关于自旋-1/2系统和[泡利矩阵](@entry_id:139493)的完整知识体系。

在接下来的内容中，我们将分三个层次展开：首先，在**“原理与机制”**一章中，我们将深入量子力学的核心，建立描述[自旋态](@entry_id:149436)的[希尔伯特空间](@entry_id:261193)，引入关键的数学工具——[泡利矩阵](@entry_id:139493)，并探讨其[代数结构](@entry_id:137052)、不确定性原理以及与空间转动的深刻联系，最终形成布洛赫球这一优美的几何图像。接着，在**“应用与跨学科联系”**一章中，我们将跨出纯理论的范畴，探索这些原理如何在核[磁共振](@entry_id:143712)（NMR）、[量子计算](@entry_id:142712)、凝聚态物理和[材料科学](@entry_id:152226)等前沿领域中转化为强大的分析工具和技术驱动力。最后，通过**“动手实践”**环节，您将有机会亲手应用所学知识，通过解决具体的物理问题来巩固和深化对自[旋量](@entry_id:158054)子世界的理解。

## 原理与机制

本章旨在深入阐述描述自旋-$\frac{1}{2}$系统的量子力学原理与数学机制。我们将从定义系统的[希尔伯特空间](@entry_id:261193)开始，引入核心的算符——泡利矩阵，并探讨它们的代数性质与物理后果，如[不确定性关系](@entry_id:186128)。随后，我们会揭示自旋与空间转动之间的深刻联系，并藉此建立布洛赫球这一直观的几何图像。最后，我们将概念从[纯态](@entry_id:141688)推广到系综的混合态，并使用[密度矩阵](@entry_id:139892)形式化这一描述。

### 希尔伯特空间与旋量

描述单个[电子自旋](@entry_id:137016)的[量子态](@entry_id:146142)需要一个复杂的[向量空间](@entry_id:151108)。一个根本性的问题是：这个空间的维度应该是多少？原则上，[自旋角动量](@entry_id:149719)算符 $\hat{\mathbf{S}} = (\hat{S}_x, \hat{S}_y, \hat{S}_z)$ 必须满足[角动量代数](@entry_id:178952)，即非对易的[对易关系](@entry_id:136780) (commutation relations)：$[\hat{S}_i, \hat{S}_j] = i \hbar \sum_{k} \epsilon_{ijk} \hat{S}_k$。这些算符同时也是空间转动的生成元，构成了一个[特殊酉群](@entry_id:138145) $SU(2)$ 的连续酉表示。

若尝试在一个一维[复希尔伯特空间](@entry_id:185216)（同构于 $\mathbb{C}$）中实现此代数，任何线性算符都退化为乘以一个复数。由于[复数乘法](@entry_id:167843)是可交换的，所有算符都将相互对易，即 $[\hat{S}_i, \hat{S}_j] = 0$。这与[角动量代数](@entry_id:178952)的基本要求相矛盾，除非所有算符均为零算符（$\hat{\mathbf{S}} = \mathbf{0}$），但这只能描述一个没有自旋的平凡系统。因此，一个能够描述非零自旋的最小[希尔伯特空间](@entry_id:261193)，其维度必须大于一。

进一步的群论分析表明，任何 $SU(2)$ 的一维连续酉表示都是平凡的。此外，一个关键的物理特性是，对于自旋-$\frac{1}{2}$ 系统，绕任意轴旋转 $2\pi$ 会使[量子态](@entry_id:146142)获得一个 $-1$ 的相位因子。这种行为无法在[一维表示](@entry_id:136509)中实现。[@problem_id:2926137] [@problem_id:2926173]

事实证明，能够容纳这一非对易代数的最小非平凡[不可约表示](@entry_id:263310)空间是一个二维[复希尔伯特空间](@entry_id:185216)，通常记为 $\mathbb{C}^2$。这个空间中的向量被称为**旋量 (spinors)**。

在这个二维空间中，我们可以选择一组正交归一基底，例如自旋$z$分量算符 $\hat{S}_z$ 的本征态。我们通常用 $|0\rangle$（或 $|{\uparrow}\rangle$）表示自旋向上态（$\hat{S}_z$ [本征值](@entry_id:154894)为 $+\frac{\hbar}{2}$），用 $|1\rangle$（或 $|{\downarrow}\rangle$）表示自旋向下态（$\hat{S}_z$ [本征值](@entry_id:154894)为 $-\frac{\hbar}{2}$）。任何一个纯自旋态（pure state）都可以表示为这两个基底向量的线性叠加：
$$
|\psi\rangle = \alpha|0\rangle + \beta|1\rangle
$$
其中，$\alpha$ 和 $\beta$ 是复数系数。

根据量子力学的基本假设，物理态必须被归一化。使用[狄拉克符号](@entry_id:154811)，一个[右矢](@entry_id:152965)（ket）$|\psi\rangle$ 的[厄米共轭](@entry_id:191215)是其对应的左矢（bra）$\langle\psi|$。[厄米共轭](@entry_id:191215)操作包括对系数取复共轭，因此 $\langle\psi| = \alpha^*\langle0| + \beta^*\langle1|$。[归一化条件](@entry_id:156486)要求态向量与自身的[内积](@entry_id:158127)为1：
$$
\langle\psi|\psi\rangle = (\alpha^*\langle0| + \beta^*\langle1|)(\alpha|0\rangle + \beta|1\rangle) = \alpha^*\alpha\langle0|0\rangle + \beta^*\beta\langle1|1\rangle + \alpha^*\beta\langle0|1\rangle + \beta^*\alpha\langle1|0\rangle
$$
利用基底的正交归一性（$\langle i|j \rangle = \delta_{ij}$），上式简化为：
$$
|\alpha|^2 + |\beta|^2 = 1
$$
这是对系数 $\alpha$ 和 $\beta$ 的**归一化约束**。[@problem_id:2926202]

另一个基本原理是，乘以一个**[全局相位](@entry_id:147947)因子 (global phase factor)** $e^{i\phi}$（其中 $\phi$ 为实数）的态向量 $|\psi'\rangle = e^{i\phi}|\psi\rangle$ 与原始态 $|\psi\rangle$ 描述的是同一个物理态。这是因为所有[可观测量](@entry_id:267133)的[期望值](@entry_id:153208) $\langle\hat{A}\rangle = \langle\psi|\hat{A}|\psi\rangle$ 和跃迁概率 $P=|\langle\chi|\psi\rangle|^2$ 在此变换下都保持不变。例如，[期望值](@entry_id:153208)的变换为 $\langle\psi'|\hat{A}|\psi'\rangle = \langle e^{i\phi}\psi|\hat{A}|e^{i\phi}\psi\rangle = e^{-i\phi}e^{i\phi}\langle\psi|\hat{A}|\psi\rangle = \langle\psi|\hat{A}|\psi\rangle$。因此，只有不同分量之间的**[相对相位](@entry_id:148120) (relative phase)** 才具有物理意义。[@problem_id:2926202] [@problem_id:2926166]

### [自旋算符](@entry_id:155419)与泡利矩阵

在二维[希尔伯特空间](@entry_id:261193)中，[自旋角动量](@entry_id:149719)算符 $\hat{S}_x, \hat{S}_y, \hat{S}_z$ 可由一组 $2 \times 2$ 矩阵表示。通常我们引入**泡利矩阵 (Pauli matrices)** $\boldsymbol{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$，它们与[自旋算符](@entry_id:155419)的关系为：
$$
\hat{\mathbf{S}} = \frac{\hbar}{2}\boldsymbol{\sigma}
$$
泡利矩阵是量子力学中最核心的数学对象之一。它们可以由一组代数性质唯一确定（在幺正等价的意义下）：
1.  **[厄米性](@entry_id:141899) (Hermitian)**: $\sigma_i^\dagger = \sigma_i$。这保证了对应的物理量（自旋分量）是实数。
2.  **无迹性 (Traceless)**: $\mathrm{tr}(\sigma_i) = 0$。
3.  **对合性 (Involutory)**: $\sigma_i^2 = I$，其中 $I$ 是 $2 \times 2$ 单位矩阵。
4.  **对易与[反对易关系](@entry_id:153815)**: 它们的对易子满足 $[\sigma_i, \sigma_j] = 2i \sum_k \epsilon_{ijk} \sigma_k$，而[反对易子](@entry_id:139754)满足 $\{\sigma_i, \sigma_j\} = \sigma_i\sigma_j + \sigma_j\sigma_i = 2\delta_{ij}I$。

在以 $\sigma_z$ 的本征态 $|{\uparrow}\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ 和 $|{\downarrow}\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$ 为基底的标准表示（也称作泡利-狄拉克表示）中，这些矩阵具有如下的具体形式：
$$
\sigma_x = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}, \quad \sigma_y = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}, \quad \sigma_z = \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}
$$
这组矩阵满足上述所有代数性质。例如，可以直接验证 $[\sigma_x, \sigma_y] = \sigma_x\sigma_y - \sigma_y\sigma_x = 2i\sigma_z$。[@problem_id:2926174]

作为[可观测量](@entry_id:267133)的代表，[泡利矩阵](@entry_id:139493)的谱性质（[本征值](@entry_id:154894)和[本征向量](@entry_id:151813)）至关重要。通过求解特征方程 $\det(\sigma_i - \lambda I) = 0$，可以证明所有三个[泡利矩阵](@entry_id:139493)的**[本征值](@entry_id:154894)**都是 $+1$ 和 $-1$。相应地，[自旋算符](@entry_id:155419) $\hat{S}_i$ 的[本征值](@entry_id:154894)为 $\pm\frac{\hbar}{2}$。

每个[泡利矩阵](@entry_id:139493)都有一套独特的、正交归一的**[本征向量](@entry_id:151813)**。在标准基底下，并采用首个非零分量为正实数的相位约定，这些[本征向量](@entry_id:151813)为：
*   **$\sigma_z$**:
    *   [本征值](@entry_id:154894) $+1$: $|{+z}\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$
    *   [本征值](@entry_id:154894) $-1$: $|{-z}\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$
*   **$\sigma_x$**:
    *   [本征值](@entry_id:154894) $+1$: $|{+x}\rangle = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ 1 \end{pmatrix}$
    *   [本征值](@entry_id:154894) $-1$: $|{-x}\rangle = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -1 \end{pmatrix}$
*   **$\sigma_y$**:
    *   [本征值](@entry_id:154894) $+1$: $|{+y}\rangle = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ i \end{pmatrix}$
    *   [本征值](@entry_id:154894) $-1$: $|{-y}\rangle = \frac{1}{\sqrt{2}}\begin{pmatrix} 1 \\ -i \end{pmatrix}$

观察可知，$\sigma_x, \sigma_y, \sigma_z$ 的[本征向量](@entry_id:151813)集是互不相同的。例如，$|{+x}\rangle$ 是 $|{+z}\rangle$ 和 $|{-z}\rangle$ 的等幅叠加。这直接反映了不同自旋分量之间的不相容性。[@problem_id:2926160]

### 不相容的[可观测量](@entry_id:267133)与[不确定性原理](@entry_id:141278)

在量子力学中，两个[可观测量](@entry_id:267133)是否能被同时精确测量，取决于它们对应的算符是否对易。如果 $[\hat{A}, \hat{B}] = 0$，则存在一个共同的本征基底，系统可以处于一个态上，使得 $\hat{A}$ 和 $\hat{B}$ 都具有确定的值。

然而，自旋分量算符的对易关系是 $[\hat{S}_i, \hat{S}_j] = i\hbar \epsilon_{ijk} \hat{S}_k \neq 0$ (当 $i \neq j$ 时)。这表明任意两个不同的自旋分量都是**不相容的可观测量 (incompatible observables)**。因此，不存在一个共同的本征基底可以[同时对角化](@entry_id:196036) $\hat{S}_x, \hat{S}_y, \hat{S}_z$。换句话说，**不可能**制备一个[量子态](@entry_id:146142)，使其在两个或更多不同方向上的自旋分量同时具有确定的值。[@problem_id:2926190]

这种不相容性通过[海森堡不确定性原理](@entry_id:171099)得到量化。对于任意两个算符 $\hat{A}$ 和 $\hat{B}$，其[标准差](@entry_id:153618)（或不确定度）$\Delta A$ 和 $\Delta B$ 必须满足[罗伯逊不确定性关系](@entry_id:149837)：
$$
\Delta A \Delta B \ge \frac{1}{2} |\langle[\hat{A}, \hat{B}]\rangle|
$$
将此应用于自旋分量，例如 $\hat{S}_x$ 和 $\hat{S}_y$，我们得到：
$$
\Delta S_x \Delta S_y \ge \frac{1}{2} |\langle[\hat{S}_x, \hat{S}_y]\rangle| = \frac{1}{2} |\langle i\hbar \hat{S}_z \rangle| = \frac{\hbar}{2} |\langle \hat{S}_z \rangle|
$$
这个关系揭示了一个深刻的物理事实：如果一个自旋态的 $z$ 分量有非零的[期望值](@entry_id:153208)（即自旋在 $z$ 方向上有一定的取向），那么其 $x$ 和 $y$ 分量的不确定度乘积就有一个非零的下限。

我们可以通过一个具体的例子来验证这一点。考虑一个处于 $\hat{S}_z$ [本征态](@entry_id:149904) $|{+z}\rangle$ 的电子，其 $\hat{S}_z$ 的值确定为 $+\frac{\hbar}{2}$。在此态下，$\Delta S_z = 0$，且 $\langle \hat{S}_z \rangle = \frac{\hbar}{2}$。我们可以计算 $\hat{S}_x$ 和 $\hat{S}_y$ 的[方差](@entry_id:200758) $\Delta S_i^2 = \langle \hat{S}_i^2 \rangle - \langle \hat{S}_i \rangle^2$。
由于 $\hat{S}_i^2 = (\frac{\hbar}{2})^2\sigma_i^2 = \frac{\hbar^2}{4}I$，对于任何归一化态，$\langle \hat{S}_i^2 \rangle = \frac{\hbar^2}{4}$。
对于 $|{+z}\rangle$ 态，直接计算可得 $\langle \hat{S}_x \rangle = \langle{+z}|\hat{S}_x|{+z}\rangle = 0$ 和 $\langle \hat{S}_y \rangle = \langle{+z}|\hat{S}_y|{+z}\rangle = 0$。
因此，[方差](@entry_id:200758)为：
$$
\Delta S_x^2 = \frac{\hbar^2}{4} - 0^2 = \frac{\hbar^2}{4} \quad \text{and} \quad \Delta S_y^2 = \frac{\hbar^2}{4} - 0^2 = \frac{\hbar^2}{4}
$$
不确定度为 $\Delta S_x = \frac{\hbar}{2}$ 和 $\Delta S_y = \frac{\hbar}{2}$。它们的乘积 $\Delta S_x \Delta S_y = \frac{\hbar^2}{4}$。
[不确定性关系](@entry_id:186128)的右边为 $\frac{\hbar}{2} |\langle \hat{S}_z \rangle| = \frac{\hbar}{2} |\frac{\hbar}{2}| = \frac{\hbar^2}{4}$。
我们看到 $\frac{\hbar^2}{4} \ge \frac{\hbar^2}{4}$，不等式成立，并且在这种情况下取等号，表明 $|{+z}\rangle$ 态是关于 $\hat{S}_x$ 和 $\hat{S}_y$ 的最小不确定度态。这完美地展示了当一个自旋分量被精确确定时，其他正交分量必然是完全不确定的（具有最大[方差](@entry_id:200758)）。[@problem_id:2926162]

更有甚者，对于任何纯自旋-$\frac{1}{2}$态，可以证明三个分量的[方差](@entry_id:200758)之和是一个常数。对于任何纯态，`|\langle\mathbf{S}\rangle|^2 = \langle S_x \rangle^2 + \langle S_y \rangle^2 + \langle S_z \rangle^2 = (\hbar/2)^2`。因此：
$$
(\Delta S_x)^2 + (\Delta S_y)^2 + (\Delta S_z)^2 = \sum_i (\langle S_i^2 \rangle - \langle S_i \rangle^2) = 3 \cdot \frac{\hbar^2}{4} - (\frac{\hbar}{2})^2 = \frac{\hbar^2}{2}
$$
这个恒等式定量地表明，不可能有两个或更多的自旋分量的[方差](@entry_id:200758)同时为零。不确定性是系统固有的，并在三个空间方向上“共享”。[@problem_id:2926190]

### 自旋与空间转动：布洛赫球

[自旋角动量](@entry_id:149719)算符的根本作用是作为空间转动的**生成元 (generators)**。一个绕单位矢量 $\hat{\mathbf{n}}$ 旋转角度 $\theta$ 的操作由一个幺正算符 $\hat{U}(\hat{\mathbf{n}}, \theta)$ 实现：
$$
\hat{U}(\hat{\mathbf{n}}, \theta) = \exp\left(-i\frac{\theta}{\hbar}\hat{\mathbf{n}} \cdot \hat{\mathbf{S}}\right) = \exp\left(-i\frac{\theta}{2}\hat{\mathbf{n}} \cdot \boldsymbol{\sigma}\right)
$$
利用[泡利矩阵](@entry_id:139493)的性质 $(\hat{\mathbf{n}} \cdot \boldsymbol{\sigma})^2 = I$，我们可以将指数函数展开成[泰勒级数](@entry_id:147154)，并将其重新求和得到一个简洁的闭合形式：
$$
\hat{U}(\hat{\mathbf{n}}, \theta) = I \cos\left(\frac{\theta}{2}\right) - i(\hat{\mathbf{n}} \cdot \boldsymbol{\sigma}) \sin\left(\frac{\theta}{2}\right)
$$
这个公式揭示了自旋-$\frac{1}{2}$系统一个惊人的特性。考虑绕任意轴旋转一个整圈，即 $\theta=2\pi$：
$$
\hat{U}(\hat{\mathbf{n}}, 2\pi) = I \cos(\pi) - i(\hat{\mathbf{n}} \cdot \boldsymbol{\sigma}) \sin(\pi) = -I
$$
一个 $2\pi$ 的转动并没有使态向量恢复原状，而是使其乘以了一个 $-1$ 的相位因子：$|\psi\rangle \to -|\psi\rangle$。这意味着[旋量](@entry_id:158054)必须“旋转两圈”（即 $4\pi$）才能回到它最初的态。这正是旋量与经典向量的根本区别，也是 $SU(2)$ 群是 $SO(3)$ 群的双重覆盖（double cover）的体现。[@problem_id:2926173]

转动算符不仅作用于态矢，也通过相似变换作用于其他算符：$\hat{A}' = \hat{U}\hat{A}\hat{U}^\dagger$。例如，将 $\sigma_x$ 绕 $z$ 轴旋转角度 $\theta$：
$$
\sigma_x' = \exp\left(-i\frac{\theta}{2}\sigma_z\right) \sigma_x \exp\left(i\frac{\theta}{2}\sigma_z\right) = \sigma_x \cos\theta + \sigma_y \sin\theta
$$
这个结果表明，算符 $\sigma_x$ 在此变换下的行为就像一个在 $xy$ 平面中旋转了角度 $\theta$ 的经典向量的 $x$ 分量。这为我们将自旋态与三维空间中的向量联系起来提供了线索。[@problem_id:2926192]

为了直观地表示一个自旋-$\frac{1}{2}$系统的[纯态](@entry_id:141688)，我们引入**布洛赫球 (Bloch sphere)**。任何纯态都可以写成（在选择合适的[全局相位](@entry_id:147947)后）：
$$
|\psi(\theta, \phi)\rangle = \cos\left(\frac{\theta}{2}\right)|{+z}\rangle + e^{i\phi}\sin\left(\frac{\theta}{2}\right)|{-z}\rangle
$$
其中 $\theta \in [0, \pi]$ 和 $\phi \in [0, 2\pi)$ 是两个参数。我们可以为这个态定义一个三维实向量，称为**布洛赫向量 (Bloch vector)** $\mathbf{r}$，其分量是泡利矩阵的[期望值](@entry_id:153208)：$\mathbf{r} = \langle\boldsymbol{\sigma}\rangle = (\langle\sigma_x\rangle, \langle\sigma_y\rangle, \langle\sigma_z\rangle)$。

通过直接计算，我们可以得到布洛赫向量的三个分量：
$$
r_x = \langle\psi|\sigma_x|\psi\rangle = \sin\theta\cos\phi \\
r_y = \langle\psi|\sigma_y|\psi\rangle = \sin\theta\sin\phi \\
r_z = \langle\psi|\sigma_z|\psi\rangle = \cos\theta
$$
这些恰好是三维欧几里得空间中[单位球](@entry_id:142558)面上的一个点的[球坐标](@entry_id:146054)表示。极角 $\theta$ 和方位角 $\phi$ 分别对应于态矢参数中的 $\theta$ 和 $\phi$。因此，所有纯自旋态都与布洛赫球的球面上的点[一一对应](@entry_id:143935)。[@problem_id:2926166]

*   北极点 $(\theta=0)$ 对应于自旋向上态 $|{+z}\rangle$。
*   南极点 $(\theta=\pi)$ 对应于自旋向下态 $|{-z}\rangle$。
*   赤道上的点 $(\theta=\pi/2)$ 对应于 $|{+z}\rangle$ 和 $|{-z}\rangle$ 的等幅叠加态。

**相对相位** $\phi$ 的几何意义现在变得非常清晰：它决定了布洛赫向量在 $xy$ 平面（赤道面）内的方向。例如，$\phi=0$ 对应于 $|{+x}\rangle$ 态，其布洛赫向量指向 $+x$ 方向。$\phi=\pi/2$ 对应于 $|{+y}\rangle$ 态，其布洛赫向量指向 $+y$ 方向。

在[哈密顿量](@entry_id:172864) $\hat{H} = \frac{\hbar\Omega}{2}\sigma_z$（例如，在沿 $z$ 方向的[磁场](@entry_id:153296)中）的驱动下，[时间演化算符](@entry_id:196774)为 $\hat{U}(t) = \exp(-i\frac{\Omega t}{2}\sigma_z)$。它作用在一般态上会使相对相位演化为 $\phi(t) = \phi_0 + \Omega t$。在布洛赫球图像中，这对应于布洛赫向量绕 $z$ 轴以角频率 $\Omega$ 进行**[拉莫尔进动](@entry_id:143131) (Larmor precession)**。[@problem_id:2926166]

### [混合态](@entry_id:141568)与密度矩阵

在许多实际情况中，例如在有限温度下的分子系综中，系统并非处于一个确定的[纯态](@entry_id:141688)，而是处于不同[纯态](@entry_id:141688)的统计混合中。这种情况需要用**[密度算符](@entry_id:138151) (density operator)** 或**[密度矩阵](@entry_id:139892) (density matrix)** $\rho$ 来描述。

对于自旋-$\frac{1}{2}$系统，任何 $2 \times 2$ 的密度矩阵都可以用泡利矩阵和[单位矩阵](@entry_id:156724) $I$ 作为基底展开。由于 $\rho$ 必须是厄米、正半定且迹为1的，其最一般的形式可以写成：
$$
\rho = \frac{1}{2}(I + \mathbf{r} \cdot \boldsymbol{\sigma})
$$
其中，$\mathbf{r}$ 仍然是布洛赫向量，其分量 $r_i = \mathrm{tr}(\rho\sigma_i)$。正半定性要求 $\rho$ 的[本征值](@entry_id:154894)非负，这导致对布洛赫向量的长度施加了约束：
$$
|\mathbf{r}|^2 = r_x^2 + r_y^2 + r_z^2 \le 1
$$
这个结果极大地扩展了布洛赫球的几何图像：
*   **[纯态](@entry_id:141688) (Pure states)** 对应于布洛赫向量长度为1的态，即所有位于**布洛赫球表面**上的点。
*   **混合态 (Mixed states)** 对应于布洛赫[向量长度](@entry_id:156432)小于1的态，即所有位于**布洛赫球内部**的点。
*   [完全混合态](@entry_id:139247)（或[最大熵](@entry_id:156648)态）$\rho = \frac{1}{2}I$ 对应于球心 $\mathbf{r} = \mathbf{0}$，表示自旋在任何方向上都没有净极化。

一个衡量态的混合程度的常用量是**纯度 (purity)** $\mathcal{P} = \mathrm{tr}(\rho^2)$。对于[纯态](@entry_id:141688)，$\rho^2=\rho$，所以 $\mathcal{P}=1$。对于混合态，$\mathcal{P}  1$。我们可以计算出纯度与布洛赫向量长度的关系：
$$
\rho^2 = \frac{1}{4}(I + \mathbf{r} \cdot \boldsymbol{\sigma})^2 = \frac{1}{4}(I^2 + 2\mathbf{r} \cdot \boldsymbol{\sigma} + (\mathbf{r} \cdot \boldsymbol{\sigma})^2) = \frac{1}{4}(I + 2\mathbf{r} \cdot \boldsymbol{\sigma} + |\mathbf{r}|^2 I)
$$
取迹后得到：
$$
\mathcal{P} = \mathrm{tr}(\rho^2) = \frac{1}{4}\mathrm{tr}((1+|\mathbf{r}|^2)I + 2\mathbf{r} \cdot \boldsymbol{\sigma}) = \frac{1}{4}(1+|\mathbf{r}|^2)\mathrm{tr}(I) = \frac{1+|\mathbf{r}|^2}{2}
$$
这个简洁的公式将态的统计性质（纯度）与其几何表示（布洛赫向量的长度）直接联系起来，凸显了布洛赫球表述的强大威力。[@problem_id:2926140]