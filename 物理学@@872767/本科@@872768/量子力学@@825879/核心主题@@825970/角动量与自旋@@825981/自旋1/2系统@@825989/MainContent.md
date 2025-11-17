## 引言
自旋是粒子的一种内禀量子属性，尽管它与经典的角动量有相似之处，却无直接的经典对应物。在所有基本粒子中，自旋1/2系统（如电子、质子和中子）占据了核心地位，它们不仅是构成物质的基本单元，也是量子力学最纯粹、最深刻概念的完美展示平台。从抽象的数学结构到变革性的技术应用，对自旋1/2系统的理解是通往整个量子世界的大门。

然而，学习者常常面临一个挑战：如何将描述自旋的优雅数学形式（如泡利矩阵和[旋量](@entry_id:158054)）与其实际的物理行为（如[磁共振](@entry_id:143712)）和深远的理论意义（如量子纠缠）联系起来。本文旨在弥合这一差距。我们将系统地剖析自旋1/2系统的理论，并将其与前沿的科学应用和思想实验紧密结合，为读者构建一个完整而深入的知识框架。

在接下来的章节中，你将学到：第一章“原理与机制”将奠定坚实的理论基础，详细介绍自旋的量子力学描述、测量法则、[不确定性原理](@entry_id:141278)以及在[磁场](@entry_id:153296)中的动力学演化。第二章“应用与跨学科连接”将展示这些原理如何在[量子控制](@entry_id:136347)、[量子信息科学](@entry_id:150091)、凝聚态物理乃至哲学思辨中大放异彩。最后，第三章“动手实践”将通过一系列具体问题，帮助你巩固和应用所学知识。让我们一同启程，探索这个虽小却蕴含无穷奥秘的量子领域。

## 原理与机制

自旋是粒子的一种内禀量子特性，类似于经典的角动量，但它没有经典对应。对于自旋为1/2的粒子，如电子、质子和中子，其自旋状态的描述构成了量子力学的一个基本且丰富的领域。本章将深入探讨自旋1/2系统的核心原理与机制，从数学形式到其在物理世界中的动力学行为。

### 自旋的量子力学描述

描述自旋1/2系统的 Hilbert 空间是二维的。我们通常选择自旋角动量在 $z$ 方向的分量算符 $\hat{S}_z$ 的[本征态](@entry_id:149904)作为[基矢](@entry_id:199546)。这两个[基矢](@entry_id:199546)分别被称为“自旋向上” ($|\uparrow\rangle$) 和“自旋向下” ($|\downarrow\rangle$)，它们满足：

$\hat{S}_z |\uparrow\rangle = +\frac{\hbar}{2} |\uparrow\rangle$
$\hat{S}_z |\downarrow\rangle = -\frac{\hbar}{2} |\downarrow\rangle$

在这个基底下，任何自旋态都可以表示为这两个[基矢](@entry_id:199546)的线性组合，形式为一个二维[复向量](@entry_id:192851)，称为**[旋量](@entry_id:158054) (spinor)**。例如，自旋向上态和自旋向下态分别表示为：

$|\uparrow\rangle = \begin{pmatrix} 1 \\ 0 \end{pmatrix}, \quad |\downarrow\rangle = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$

[自旋角动量](@entry_id:149719)的三个分量算符 $\hat{S}_x, \hat{S}_y, \hat{S}_z$ 在这个基底下的矩阵表示为：

$\hat{S}_x = \frac{\hbar}{2} \sigma_x = \frac{\hbar}{2} \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix}$

$\hat{S}_y = \frac{\hbar}{2} \sigma_y = \frac{\hbar}{2} \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix}$

$\hat{S}_z = \frac{\hbar}{2} \sigma_z = \frac{\hbar}{2} \begin{pmatrix} 1  0 \\ 0  -1 \end{pmatrix}$

其中，$\sigma_x, \sigma_y, \sigma_z$ 是著名的**[泡利矩阵](@entry_id:139493) (Pauli matrices)**。这些矩阵是[厄米矩阵](@entry_id:155147)（Hermitian），确保了其[本征值](@entry_id:154894)（即可观测的物理量）是实数。同时，泡利矩阵也是幺[正矩阵](@entry_id:149490)（Unitary），并且它们的平方等于单位矩阵 $I$，即 $\sigma_x^2 = \sigma_y^2 = \sigma_z^2 = I$。[@problem_id:2122138]

与[轨道角动量](@entry_id:191303)类似，自旋角动量的不同分量算符之间不对易。它们遵循着一个基本的**[对易关系](@entry_id:136780)**：

$[\hat{S}_i, \hat{S}_j] = i\hbar \sum_k \epsilon_{ijk} \hat{S}_k$

其中 $\epsilon_{ijk}$ 是 Levi-Civita 符号。例如，我们可以利用[泡利矩阵](@entry_id:139493)的表示来显式验证 $[\hat{S}_x, \hat{S}_y]$ 的关系 [@problem_id:2122101]：

$[\hat{S}_x, \hat{S}_y] = \hat{S}_x \hat{S}_y - \hat{S}_y \hat{S}_x = \left(\frac{\hbar}{2}\right)^2 (\sigma_x \sigma_y - \sigma_y \sigma_x)$

$\sigma_x \sigma_y = \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix} \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix} = \begin{pmatrix} i  0 \\ 0  -i \end{pmatrix} = i \sigma_z$

$\sigma_y \sigma_x = \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix} \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix} = \begin{pmatrix} -i  0 \\ 0  i \end{pmatrix} = -i \sigma_z$

因此，$[\hat{S}_x, \hat{S}_y] = \frac{\hbar^2}{4} (i \sigma_z - (-i \sigma_z)) = \frac{\hbar^2}{4} (2i \sigma_z) = i\hbar \left(\frac{\hbar}{2} \sigma_z\right) = i\hbar \hat{S}_z$。这个非对易关系是量子力学中许多非经典现象的根源，包括不确定性原理。

### 任意方向上的[自旋测量](@entry_id:196098)

虽然我们习惯于使用 $z$ 方向的基底，但物理上我们可以在任何空间方向上测量自旋。沿任意方向单位矢量 $\hat{n} = (\sin\theta \cos\phi, \sin\theta \sin\phi, \cos\theta)$ 的自旋分量算符由[点积](@entry_id:149019)定义：

$\hat{S}_n = \vec{S} \cdot \hat{n} = \hat{S}_x n_x + \hat{S}_y n_y + \hat{S}_z n_z = \frac{\hbar}{2} (\vec{\sigma} \cdot \hat{n})$

一个惊人但基本的结果是，无论选择哪个方向 $\hat{n}$，对 $\hat{S}_n$ 的测量结果**只能**是 $+\frac{\hbar}{2}$ 或 $-\frac{\hbar}{2}$。我们可以通过一个巧妙的代数方法证明这一点 [@problem_id:2122155]。考虑算符 $(\vec{\sigma} \cdot \hat{n})^2$：

$(\vec{\sigma} \cdot \hat{n})^2 = (n_x \sigma_x + n_y \sigma_y + n_z \sigma_z)^2 = \sum_{i,j} n_i n_j \sigma_i \sigma_j$

利用[泡利矩阵](@entry_id:139493)的性质 $\sigma_i \sigma_j = \delta_{ij}I + i\sum_k \epsilon_{ijk}\sigma_k$，我们得到：

$\sum_{i,j} n_i n_j (\delta_{ij}I + i\sum_k \epsilon_{ijk}\sigma_k) = (\sum_i n_i^2)I + i\sum_{i,j,k} \epsilon_{ijk} n_i n_j \sigma_k$

由于 $\hat{n}$ 是单位矢量，$\sum_i n_i^2 = |\hat{n}|^2 = 1$。另外，由于 $n_i n_j$ 在交换索引 $i, j$ 时是对称的，而 $\epsilon_{ijk}$ 是反对称的，第二项的和为零。因此，我们得到一个非常简洁的结果：

$(\vec{\sigma} \cdot \hat{n})^2 = I$

如果 $\lambda$ 是 $\vec{\sigma} \cdot \hat{n}$ 的[本征值](@entry_id:154894)，那么 $\lambda^2 = 1$，这意味着 $\lambda = \pm 1$。相应地，$\hat{S}_n = \frac{\hbar}{2} (\vec{\sigma} \cdot \hat{n})$ 的[本征值](@entry_id:154894)就是 $\pm \frac{\hbar}{2}$。这表明自旋的量子化是内禀的，与测量方向无关。

与[本征值](@entry_id:154894)相对应，$\hat{S}_n$ 的[本征态](@entry_id:149904)，即沿 $\hat{n}$ 方向自旋确[定态](@entry_id:137260)，可以表示为：

$|\uparrow\rangle_n = \cos(\frac{\theta}{2}) |\uparrow\rangle + \exp(i\phi)\sin(\frac{\theta}{2}) |\downarrow\rangle$
$|\downarrow\rangle_n = \sin(\frac{\theta}{2}) |\uparrow\rangle - \exp(i\phi)\cos(\frac{\theta}{2}) |\downarrow\rangle$

一个态的测量结果的概率由[量子态](@entry_id:146142)在该测量基底下的投影决定。例如，假设一个粒子被制备在沿 $\vec{n}$ 方向自旋向上的态 $|\psi\rangle = |\uparrow\rangle_n$，其中 $\vec{n}$ 在 x-z 平面内，与 z 轴夹角为 $\theta$（即 $\phi=0$）。如果我们此时去测量沿 $y$ 轴的自旋分量 $\hat{S}_y$，得到 $+\frac{\hbar}{2}$ 的概率是多少？根据[量子测量](@entry_id:272490)法则，该概率为 $P = |\langle \uparrow_y | \psi \rangle|^2$。$\hat{S}_y$ 的自旋向上[本征态](@entry_id:149904)是 $|\uparrow_y\rangle = \frac{1}{\sqrt{2}}(|\uparrow\rangle + i|\downarrow\rangle)$。因此，概率的计算如下 [@problem_id:2122113]：

$P = \left| \left( \frac{1}{\sqrt{2}}(\langle\uparrow| - i\langle\downarrow|) \right) \left( \cos(\frac{\theta}{2})|\uparrow\rangle + \sin(\frac{\theta}{2})|\downarrow\rangle \right) \right|^2$
$P = \left| \frac{1}{\sqrt{2}} (\cos(\frac{\theta}{2}) - i\sin(\frac{\theta}{2})) \right|^2 = \frac{1}{2} (\cos^2(\frac{\theta}{2}) + \sin^2(\frac{\theta}{2})) = \frac{1}{2}$

这个结果 $1/2$ 与角度 $\theta$ 无关，揭示了 $x-z$ 平面内的任何自旋态在 $y$ 方向上的投影都具有均等的机会得到向上或向下的结果。

### 自旋与[不确定性原理](@entry_id:141278)

算符的非对易性直接导致了**[海森堡不确定性原理](@entry_id:171099)**。对于任意两个算符 $\hat{A}$ 和 $\hat{B}$，其测量标准差的乘积满足：

$(\Delta A)(\Delta B) \ge \frac{1}{2} |\langle[\hat{A}, \hat{B}]\rangle|$

对于自旋分量，我们有 $[\hat{S}_x, \hat{S}_y] = i\hbar \hat{S}_z$。这意味着我们无法同时精确知道一个粒子在 $x$ 方向和 $y$ 方向的自旋分量。

让我们以一个具体例子来说明 [@problem_id:2122117]。考虑一个处于 $z$ 方向自旋向上态 $|\psi\rangle = |\uparrow_z\rangle$ 的粒子。对于这个态，$\hat{S}_z$ 的值是确定的（$+\frac{\hbar}{2}$），因此 $\Delta S_z = 0$。现在我们计算 $\hat{S}_x$ 和 $\hat{S}_y$ 的不确定度。首先是[期望值](@entry_id:153208)：

$\langle S_x \rangle = \langle\uparrow_z| \hat{S}_x |\uparrow_z\rangle = \frac{\hbar}{2} \begin{pmatrix} 1  0 \end{pmatrix} \begin{pmatrix} 0  1 \\ 1  0 \end{pmatrix} \begin{pmatrix} 1 \\ 0 \end{pmatrix} = 0$
$\langle S_y \rangle = \langle\uparrow_z| \hat{S}_y |\uparrow_z\rangle = \frac{\hbar}{2} \begin{pmatrix} 1  0 \end{pmatrix} \begin{pmatrix} 0  -i \\ i  0 \end{pmatrix} \begin{pmatrix} 1 \\ 0 \end{pmatrix} = 0$

接下来计算平方的[期望值](@entry_id:153208)，利用 $\sigma_x^2 = \sigma_y^2 = I$：

$\langle S_x^2 \rangle = \langle\uparrow_z| (\frac{\hbar}{2}\sigma_x)^2 |\uparrow_z\rangle = \frac{\hbar^2}{4} \langle\uparrow_z| I |\uparrow_z\rangle = \frac{\hbar^2}{4}$
$\langle S_y^2 \rangle = \langle\uparrow_z| (\frac{\hbar}{2}\sigma_y)^2 |\uparrow_z\rangle = \frac{\hbar^2}{4} \langle\uparrow_z| I |\uparrow_z\rangle = \frac{\hbar^2}{4}$

不确定度 $\Delta A = \sqrt{\langle A^2 \rangle - \langle A \rangle^2}$ 因此为：

$\Delta S_x = \sqrt{\frac{\hbar^2}{4} - 0} = \frac{\hbar}{2}$
$\Delta S_y = \sqrt{\frac{\hbar^2}{4} - 0} = \frac{\hbar}{2}$

它们的乘积是 $(\Delta S_x)(\Delta S_y) = \frac{\hbar^2}{4}$。现在我们看海森堡[不确定性关系](@entry_id:186128)的下限：

$\frac{1}{2} |\langle[\hat{S}_x, \hat{S}_y]\rangle| = \frac{1}{2} |\langle i\hbar \hat{S}_z \rangle| = \frac{\hbar}{2} |\langle \hat{S}_z \rangle| = \frac{\hbar}{2} \left(\frac{\hbar}{2}\right) = \frac{\hbar^2}{4}$

可见，对于 $S_z$ 的[本征态](@entry_id:149904)，$\hat{S}_x$ 和 $\hat{S}_y$ 的不确定度乘积恰好达到了不确定性原理的最小值。这表明当一个自旋分量被精确确定时，另两个垂直分量处于最大程度的不确定之中。

### [自旋动力学](@entry_id:146095)：[拉莫尔进动](@entry_id:143131)与[拉比振荡](@entry_id:137940)

当自旋1/2粒子与[磁场](@entry_id:153296)相互作用时，其自旋态会随时间演化。这个动力学过程由薛定谔方程描述，其核心是[哈密顿算符](@entry_id:144286) $\hat{H}$。对于一个磁矩为 $\vec{\mu} = \gamma \vec{S}$（$\gamma$ 是[旋磁比](@entry_id:149290)）的粒子，在[磁场](@entry_id:153296) $\vec{B}$ 中的[哈密顿量](@entry_id:172864)是：

$\hat{H} = -\vec{\mu} \cdot \vec{B} = -\gamma \vec{S} \cdot \vec{B}$

#### [拉莫尔进动](@entry_id:143131)

最简单的情形是当[磁场](@entry_id:153296)是沿 $z$ 轴的[匀强磁场](@entry_id:263817) $\vec{B} = B_0 \hat{k}$。此时[哈密顿量](@entry_id:172864)为 $\hat{H} = -\gamma B_0 \hat{S}_z$。[时间演化算符](@entry_id:196774) $\hat{U}(t) = \exp(-i\hat{H}t/\hbar)$ 在 $S_z$ 基底下是对角的，因为 $|\uparrow\rangle$ 和 $|\downarrow\rangle$ 是 $\hat{H}$ 的[本征态](@entry_id:149904)。定义[拉莫尔频率](@entry_id:149912) $\omega_0 = \gamma B_0$，[能量本征值](@entry_id:144381)为 $E_\uparrow = -\frac{\hbar\omega_0}{2}$ 和 $E_\downarrow = +\frac{\hbar\omega_0}{2}$。[演化算符](@entry_id:182628)的矩阵形式为 [@problem_id:2122137]：

$\hat{U}(t) = \begin{pmatrix} \exp(-iE_\uparrow t/\hbar)  0 \\ 0  \exp(-iE_\downarrow t/\hbar) \end{pmatrix} = \begin{pmatrix} \exp(i\omega_0 t/2)  0 \\ 0  \exp(-i\omega_0 t/2) \end{pmatrix}$

这种演化导致自旋的[期望值](@entry_id:153208)绕着[磁场](@entry_id:153296)方向进动，称为**拉莫爾进动 (Larmor precession)**。在海森堡图像中，算符随时间演化，其[运动方程](@entry_id:170720)为 $\frac{d\hat{S}_i}{dt} = \frac{i}{\hbar}[\hat{H}, \hat{S}_i]$。对于 $\hat{H} = -\omega_0 \hat{S}_z$，我们得到 [@problem_id:2122101]：

$\frac{d\hat{S}_x}{dt} = \frac{i}{\hbar}[-\omega_0 \hat{S}_z, \hat{S}_x] = -\frac{i\omega_0}{\hbar}(i\hbar \hat{S}_y) = \omega_0 \hat{S}_y$
$\frac{d\hat{S}_y}{dt} = \frac{i}{\hbar}[-\omega_0 \hat{S}_z, \hat{S}_y] = -\frac{i\omega_0}{\hbar}(-i\hbar \hat{S}_x) = -\omega_0 \hat{S}_x$
$\frac{d\hat{S}_z}{dt} = \frac{i}{\hbar}[-\omega_0 \hat{S}_z, \hat{S}_z] = 0$

这组方程描述了自旋矢量在 $xy$ 平面内以[角频率](@entry_id:261565) $\omega_0$ 绕 $z$ 轴的经典进动。如果粒子初始时处于 $\hat{S}_x$ 的本征态，$\langle S_x(0) \rangle = \hbar/2$，那么在 $t$ 时刻，$\langle S_y(t) \rangle = -\frac{\hbar}{2}\sin(\omega_0 t)$。

#### [拉比振荡](@entry_id:137940)

当[哈密顿量](@entry_id:172864)与初始态的[基矢](@entry_id:199546)不对易时，会发生更有趣的现象。例如，考虑一个[哈密顿量](@entry_id:172864) $\hat{H} = \omega \hat{S}_x$，其中 $\omega$ 是一个频率常数。如果系统初始态为 $|\psi(0)\rangle = |\uparrow_z\rangle$ [@problem_id:2122106]。此时，初始态不是[哈密顿量](@entry_id:172864)的[本征态](@entry_id:149904)，因此它不是[定态](@entry_id:137260)，会随时间演化。

[时间演化算符](@entry_id:196774)为 $\hat{U}(t) = \exp(-i\omega t \hat{S}_x/\hbar) = \exp(-i\frac{\omega t}{2} \sigma_x)$。利用泡利矩阵的指数展开公式 $\exp(-ia\sigma_k) = I\cos(a) - i\sigma_k\sin(a)$，我们得到：

$\hat{U}(t) = I\cos(\frac{\omega t}{2}) - i\sigma_x\sin(\frac{\omega t}{2})$

作用在初始态上：

$|\psi(t)\rangle = \hat{U}(t)|\uparrow_z\rangle = \cos(\frac{\omega t}{2})|\uparrow_z\rangle - i\sin(\frac{\omega t}{2})\sigma_x|\uparrow_z\rangle = \cos(\frac{\omega t}{2})|\uparrow_z\rangle - i\sin(\frac{\omega t}{2})|\downarrow_z\rangle$

$z$ 方向自旋的[期望值](@entry_id:153208)随时间的变化为：

$\langle S_z(t) \rangle = \langle\psi(t)| \hat{S}_z |\psi(t)\rangle = \frac{\hbar}{2}(\cos^2(\frac{\omega t}{2}) - \sin^2(\frac{\omega t}{2})) = \frac{\hbar}{2}\cos(\omega t)$

这表明，自旋的[期望值](@entry_id:153208)在 $+\hbar/2$ 和 $-\hbar/2$ 之間[振荡](@entry_id:267781)。系统在自旋向上和自旋向下两个状态之间周期性地转换，这种现象称为**[拉比振荡](@entry_id:137940) (Rabi oscillation)**。类似的动力学行为也发生在其他形式的[哈密顿量](@entry_id:172864)下，例如 $H = \alpha \sigma_y$ [@problem_id:2122138]，它驱动了自旋态在 Hilbert 空间中的另一种旋转。

### 多[粒子自旋](@entry_id:142910)系统

当系统包含多个自旋1/2粒子时，其 Hilbert 空间是各个粒子 Hilbert 空间的**[张量积](@entry_id:140694) (tensor product)**。对于 $N$ 个粒子，总的 Hilbert 空间维度为 $2^N$ [@problem_id:2122133]。

#### 双自旋系统：[单重态](@entry_id:154728)与[三重态](@entry_id:156705)

考虑两个自旋1/2粒子，总 Hilbert 空间是 $2 \times 2=4$ 维。总[自旋算符](@entry_id:155419)定义为 $\vec{S} = \vec{S}_1 + \vec{S}_2$。根据[角动量相加](@entry_id:145967)法则，总自旋量子数 $S$ 可以取值为 $S=1$ 或 $S=0$。
- $S=1$ 的态构成一个**[三重态](@entry_id:156705) (triplet state)**，是自旋对称的。
- $S=0$ 的态是一个**[单重态](@entry_id:154728) (singlet state)**，是自旋反对稱的。

这两种状态在许多物理系统中具有不同的能量，特别是在存在交换相互作用时。一个常见的模型是**[海森堡哈密顿量](@entry_id:146333)** [@problem_id:2122147]：

$\hat{H} = J \vec{S}_1 \cdot \vec{S}_2$

其中 $J$ 是[交换耦合](@entry_id:154848)常数。为了找到[能量本征值](@entry_id:144381)，我们使用一个技巧。总自旋的平方为：

$\vec{S}^2 = (\vec{S}_1 + \vec{S}_2)^2 = \vec{S}_1^2 + \vec{S}_2^2 + 2\vec{S}_1 \cdot \vec{S}_2$

因此，$\vec{S}_1 \cdot \vec{S}_2 = \frac{1}{2}(\vec{S}^2 - \vec{S}_1^2 - \vec{S}_2^2)$。$\hat{H}$ 的本征态就是[总自旋](@entry_id:153335)的本征态。我们知道 $\vec{S}_1^2$ 和 $\vec{S}_2^2$ 的[本征值](@entry_id:154894)为 $s(s+1)\hbar^2 = \frac{1}{2}(\frac{1}{2}+1)\hbar^2 = \frac{3}{4}\hbar^2$。$\vec{S}^2$ 的[本征值](@entry_id:154894)为 $S(S+1)\hbar^2$。

对于[三重态](@entry_id:156705) ($S=1$)，能量为：
$E_{\text{triplet}} = \frac{J}{2} \left(1(1+1)\hbar^2 - \frac{3}{4}\hbar^2 - \frac{3}{4}\hbar^2\right) = \frac{J}{2} \left(2\hbar^2 - \frac{3}{2}\hbar^2\right) = \frac{J\hbar^2}{4}$

对于[单重态](@entry_id:154728) ($S=0$)，能量为：
$E_{\text{singlet}} = \frac{J}{2} \left(0(0+1)\hbar^2 - \frac{3}{4}\hbar^2 - \frac{3}{4}\hbar^2\right) = -\frac{3J\hbar^2}{4}$

因此，三重态与单重态之间的[能隙](@entry_id:191975)为 $\Delta E = E_{\text{triplet}} - E_{\text{singlet}} = \frac{J\hbar^2}{4} - (-\frac{3J\hbar^2}{4}) = J\hbar^2$。这个[能隙](@entry_id:191975)的大小和符号决定了材料的磁性：如果 $J0$（反[铁磁耦合](@entry_id:153346)），单重态能量更低；如果 $J0$（[铁磁耦合](@entry_id:153346)），三重态能量更低。

#### 多体态的测量

在[多粒子系统](@entry_id:192694)中，测量可以作用于整个系统，也可以只作用于其中一个子系统。例如，考虑一个三粒子系统，其状态可能是一个复杂的[纠缠态](@entry_id:152310)，如 $|\psi\rangle = \frac{1}{\sqrt{6}} ( |\uparrow\downarrow\downarrow\rangle + 2i |\downarrow\uparrow\downarrow\rangle - |\downarrow\downarrow\uparrow\rangle )$ [@problem_id:2122112]。如果我们只测量第一个粒子的 $x$ 方向自旋，得到 $+\frac{\hbar}{2}$ 的概率是多少？

这需要将作用于第一个粒子[子空间](@entry_id:150286)的[投影算符](@entry_id:154142) $P_{1,+} = |\uparrow_x\rangle_1\langle\uparrow_x|_1$ 应用于整个系统。其中 $|\uparrow_x\rangle = \frac{1}{\sqrt{2}}(|\uparrow\rangle + |\downarrow\rangle)$。概率由 $P = \langle\psi| (P_{1,+} \otimes I_2 \otimes I_3) |\psi\rangle$ 给出。

计算过程为：
$(\langle\uparrow_x|_1 \otimes I_2 \otimes I_3) |\psi\rangle = \frac{1}{\sqrt{6}} \left( \langle\uparrow_x|\uparrow\rangle |\downarrow\downarrow\rangle + 2i \langle\uparrow_x|\downarrow\rangle |\uparrow\downarrow\rangle - \langle\uparrow_x|\downarrow\rangle |\downarrow\uparrow\rangle \right)$
$= \frac{1}{\sqrt{6}} \left( \frac{1}{\sqrt{2}}|\downarrow\downarrow\rangle + \frac{2i}{\sqrt{2}}|\uparrow\downarrow\rangle - \frac{1}{\sqrt{2}}|\downarrow\uparrow\rangle \right)$
$= \frac{1}{\sqrt{12}} (|\downarrow\downarrow\rangle + 2i|\uparrow\downarrow\rangle - |\downarrow\uparrow\rangle)$

概率是这个合成态的范数平方：
$P = \frac{1}{12} \left( \langle\downarrow\downarrow|\downarrow\downarrow\rangle + |2i|^2\langle\uparrow\downarrow|\uparrow\downarrow\rangle + |-1|^2\langle\downarrow\uparrow|\downarrow\uparrow\rangle \right) = \frac{1}{12}(1+4+1) = \frac{6}{12} = \frac{1}{2}$

这个例子展示了如何处理对纠纏多体系统一部分的测量，这是[量子信息](@entry_id:137721)和[量子计算](@entry_id:142712)中的一项基本操作。同样，我们也可以测量整个系统的集体属性，例如[总自旋](@entry_id:153335)。一个处于特定乘积态，如 $|\uparrow\uparrow\downarrow\rangle$ 的三粒子系统，本身并不是总自旋 $S^2$ 的本征态，而是不同总自旋值的叠加。通过将该态分解到[总自旋](@entry_id:153335)本征基底上（一个涉及[Clebsch-Gordan系数](@entry_id:142551)的过程），可以计算出测量得到特定[总自旋](@entry_id:153335)值（如 $S=1/2$ 或 $S=3/2$）的概率 [@problem_id:2122133]。

自旋1/2系统虽然简单，但它完美地封装了量子力学的许多核心概念：量子化、态叠加、非对易性、不确定性、动力学演化和纠缠。对它的深入理解是掌握更复杂量子系统的基石。