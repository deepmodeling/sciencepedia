## 引言
在科学与工程领域，从复杂的、高维的时空数据中提取有意义的动态信息是一项核心挑战。无论是流体涡旋的演化，还是流行病的传播，理解其背后的主导模式和时间规律对于预测和控制至关重要。动态[模态分解](@entry_id:637725)（Dynamic Mode Decomposition, DMD）正是在这一背景下应运而生的一种强大的数据驱动方法。它无需系统的控制方程，仅通过一系列数据快照，就能揭示系统的内在动力学特性，将其分解为一组具有特定频率和增长/衰减率的[相干结构](@entry_id:182915)，即“动态模态”。

本文旨在全面介绍DMD的理论与实践。我们将从三个层面展开：第一章“原理与机制”将深入其数学核心，揭示它与[库普曼算子理论](@entry_id:266030)的深刻联系，并详解算法的实现与关键考量；第二章“应用与[交叉](@entry_id:147634)学科联系”将展示DMD在[流体力学](@entry_id:136788)、[系统辨识](@entry_id:201290)乃至[网络科学](@entry_id:139925)和流行病学等前沿领域的广泛应用，突显其作为分析工具的强大威力；最后，在“动手实践”部分，我们将通过具体的编程练习，巩固理论知识并解决数据分析中的实际挑战。通过这一结构化的学习路径，读者不仅能掌握DMD的计算方法，更能深刻理解其作为连接经典谱分析与现代数据科学的桥梁所扮演的重要角色，从而有能力将其应用于自己的研究领域。

## 原理与机制

本章旨在深入阐述动态[模态分解](@entry_id:637725)（Dynamic Mode Decomposition, DMD）背后的核心原理与关键机制。我们将从动力系统的[算子理论](@entry_id:139990)视角出发，建立DMD的数学基础，随后详细介绍其算法实现、结果解读，并探讨在实际应用中遇到的高级问题，如[非正规性](@entry_id:752585)、[数值误差](@entry_id:635587)和[测量噪声](@entry_id:275238)的影响。

### [库普曼算子](@entry_id:183136)：非线性动力学的线性视角

理解DMD的关键在于认识到它是一种旨在逼近**[库普曼算子](@entry_id:183136) (Koopman operator)** 谱特性的数据驱动方法。[库普曼算子理论](@entry_id:266030)为分析非[线性动力系统](@entry_id:150282)提供了一个强大的线性框架。

考虑一个由自治[偏微分方程](@entry_id:141332)（PDE）描述的动力系统，其状态 $u$ 在一个巴拿赫空间 $E$ 中演化。系统的解定义了一个连续时间流映射 $\Phi_t: E \to E$，它将初始状态 $u_0$ 演化到时间 $t$ 时的状态 $u(t) = \Phi_t(u_0)$。这个流映射具有[半群性质](@entry_id:271012)：$\Phi_0 = \mathrm{id}$ （恒等映射）且 $\Phi_{t+s} = \Phi_t \circ \Phi_s$。尽[管流](@entry_id:189531)映射 $\Phi_t$ 本身通常是高度[非线性](@entry_id:637147)的，但我们可以通过考察它对“可观测量”的作用来获得一个线性描述。

一个**[可观测量](@entry_id:267133) (observable)** 是一个函数 $g: E \to \mathbb{C}$，它从系统状态中提取某个量值。[库普曼算子](@entry_id:183136)族 $\{K^t\}_{t \ge 0}$ 正是作用在这些[可观测量](@entry_id:267133)构成的[函数空间](@entry_id:143478)上的[线性算子](@entry_id:149003)。其定义如下：
$$
(K^t g)(u) = g(\Phi_t(u))
$$
该定义意味着，算子 $K^t$ 作用于可观测量 $g$ 得到的新可观测量 $K^t g$，在状态 $u$ 处的值等于 $g$ 在 $u$ 演化了时间 $t$ 之后的状态 $\Phi_t(u)$ 处的值。无论动力系统 $\Phi_t$ 如何[非线性](@entry_id:637147)，$K^t$ 对可观测量空间的作用始终是线性的，即 $K^t(c_1 g_1 + c_2 g_2) = c_1 K^t g_1 + c_2 K^t g_2$。

为了进行有效的谱分析，我们需要这个算子族构成一个**[强连续半群](@entry_id:272133)（$C_0$-semigroup）**。这意味着对于可观测量巴拿赫空间 $X$ 中的任意元素 $g$，映射 $t \mapsto K^t g$ 都是连续的。这要求 $\lim_{t \to 0^+} \|K^t g - g\|_X = 0$。这个条件的成立与否，极大地依赖于函数空间 $X$ 的选择和流 $\Phi_t$ 的性质。一个确保强连续性的充分条件如下 [@problem_id:3383123]：

假设 $M \subset E$ 是一个紧致的、正向不变的集合（即对所有 $t \ge 0$，有 $\Phi_t(M) \subseteq M$）。我们选择[可观测量](@entry_id:267133)空间为 $X=C(M)$，即 $M$ 上的复值连续函数空间，其范数为[上确界范数](@entry_id:145717) $\|g\|_\infty = \sup_{u \in M} |g(u)|$。如果流映射 $(t, u) \mapsto \Phi_t(u)$ 在 $[0, \infty) \times M$ 上是联合连续的，那么 $\{K^t\}_{t \ge 0}$ 就在 $X$ 上构成一个[强连续半群](@entry_id:272133)。这是因为在紧集 $M$ 上，[连续函数](@entry_id:137361) $g$ 是[一致连续](@entry_id:140948)的，而流的联合连续性保证了当 $t \to 0$ 时，$\Phi_t(u)$ 一致地趋近于 $u$，从而确保了 $\|K^t g - g\|_\infty \to 0$。

[强连续半群](@entry_id:272133) $\{K^t\}_{t \ge 0}$ 可以由其**[无穷小生成元](@entry_id:270424) (infinitesimal generator)** $\mathcal{K}$ 来刻画，定义为 $\mathcal{K}g = \lim_{t \to 0^+} \frac{K^t g - g}{t}$。形式上，我们可以写成 $K^t = \exp(\mathcal{K}t)$。这个生成元 $\mathcal{K}$ 的谱（即其[特征值](@entry_id:154894)集合）包含了关于[系统动力学](@entry_id:136288)行为的深刻信息，如[振荡频率](@entry_id:269468)和增长/衰减率。

### [库普曼算子](@entry_id:183136)的谱分析

对[库普曼算子](@entry_id:183136)的谱分析旨在寻找其**特征函数 (eigenfunctions)** 和**[特征值](@entry_id:154894) (eigenvalues)**。一个[可观测量](@entry_id:267133) $g_\omega$ 如果是无穷小生成元 $\mathcal{K}$ 的[特征函数](@entry_id:186820)，对应[特征值](@entry_id:154894)为 $\omega \in \mathbb{C}$，即 $\mathcal{K} g_\omega = \omega g_\omega$，那么它在动力系统[演化过程](@entry_id:175749)中具有简单的指数标度行为。具体而言，它也是算子 $K^t$ 的特征函数，对应[特征值](@entry_id:154894)为 $\mu = \exp(\omega t)$：
$$
K^t g_\omega = \exp(\omega t) g_\omega
$$
这意味着，在状态 $u_0$ 演化时，可观测量 $g_\omega$ 的值以[复指数形式](@entry_id:265806)演化：$g_\omega(u(t)) = g_\omega(u_0) \exp(\omega t)$。[特征值](@entry_id:154894) $\omega$ 的实部 $\Re(\omega)$ 决定了[可观测量](@entry_id:267133)值的增长或衰减率，而虚部 $\Im(\omega)$ 则代表了其[振荡](@entry_id:267781)的[角频率](@entry_id:261565)。

为了将这些抽象概念具体化，我们考虑一个线性[平流-扩散方程](@entry_id:746317) [@problem_id:3383180]：
$$
\partial_t u = \nu \partial_{xx} u - c \partial_x u \equiv L u
$$
该方程定义在 $x \in [0, 2\pi]$ 的周期性区域上。系统算子 $L$ 的特征函数是[傅里叶基](@entry_id:201167)函数 $\varphi_m(x) = \exp(imx)$，对应的[特征值](@entry_id:154894)为 $\lambda_m = -\nu m^2 - icm$。

现在，我们考虑作用在此系统上的[库普曼算子](@entry_id:183136)。选择一类特殊的线性[可观测量](@entry_id:267133)，即[傅里叶系数](@entry_id:144886)提取器 $g_m(u) = \frac{1}{2\pi} \int_0^{2\pi} u(x) \exp(-imx) dx$。这些 $g_m$ 是[库普曼算子](@entry_id:183136)的特征函数吗？为了验证，我们施加 $K^t$ 于 $g_m$：
$$
(K^t g_m)(u_0) = g_m(u(\cdot, t))
$$
$u(\cdot, t)$ 的第 $m$ 个[傅里叶系数](@entry_id:144886) $\hat{u}_m(t)$ 的演化由[常微分方程](@entry_id:147024) $\frac{d\hat{u}_m}{dt} = \lambda_m \hat{u}_m$ 决定，其解为 $\hat{u}_m(t) = \hat{u}_m(0) \exp(\lambda_m t)$。由于 $g_m(u(\cdot, t)) = \hat{u}_m(t)$ 且 $g_m(u_0) = \hat{u}_m(0)$，我们得到：
$$
(K^t g_m)(u_0) = \hat{u}_m(0) \exp(\lambda_m t) = g_m(u_0) \exp(\lambda_m t)
$$
由于此式对任意初始条件 $u_0$ 均成立，我们有算子关系 $K^t g_m = \exp(\lambda_m t) g_m$。这表明，[可观测量](@entry_id:267133) $g_m$ 确实是[库普曼算子](@entry_id:183136) $K^t$ 的[特征函数](@entry_id:186820)，其对应的离散时间[特征值](@entry_id:154894)为 $\mu_m(t) = \exp(\lambda_m t)$。因此，连续时间库普曼[特征值](@entry_id:154894)（即[无穷小生成元](@entry_id:270424) $\mathcal{K}$ 的[特征值](@entry_id:154894)）恰好是系统算子 $L$ 的[特征值](@entry_id:154894)，即 $\omega_m = \lambda_m = -\nu m^2 - icm$。

这个例子揭示了一个基本联系：对于[线性系统](@entry_id:147850)，其[状态空间](@entry_id:177074)算子（如 $L$）的谱与作用于线性[可观测量](@entry_id:267133)的[库普曼算子](@entry_id:183136)生成元的谱是相同的。DMD的核心思想正是基于此，即通过数据驱动的方式来估计[库普曼算子](@entry_id:183136)的谱信息，从而揭示系统的动力学特性。与[特征函数](@entry_id:186820) $g_m$ 相关的空间结构（在此例中为[傅里叶基](@entry_id:201167)函数 $\varphi_m(x)$）被称为**库普曼模态 (Koopman mode)**。

### 动态[模态分解](@entry_id:637725)（DMD）：[库普曼算子](@entry_id:183136)的[数值逼近](@entry_id:161970)

DMD 是一种从一系列按时间顺序[排列](@entry_id:136432)的系统快照数据 $\{x_0, x_1, \dots, x_N\}$ 中提取动态相关结构（模态）及其[时间演化](@entry_id:153943)特性（频率和增长率）的算法。其根本目标是逼近[库普曼算子](@entry_id:183136) $K^{\Delta t}$ 的谱，其中 $\Delta t$ 是快照之间的时间间隔。

#### 标准[DMD算法](@entry_id:748617)

标准[DMD算法](@entry_id:748617)假设快照之间存在一个线性的映射关系。设有两个快照矩阵：
$$
X = \begin{pmatrix} |  |   | \\ x_0  x_1  \dots  x_{N-1} \\ |  |   | \end{pmatrix}, \quad X' = \begin{pmatrix} |  |   | \\ x_1  x_2  \dots  x_{N} \\ |  |   | \end{pmatrix}
$$
算法的目标是寻找一个最佳的线性算子 $A$（在最小二乘意义下），使得 $X' \approx AX$。这个算子 $A$ 可被视为[库普曼算子](@entry_id:183136) $K^{\Delta t}$ 在快照数据所张成的[子空间](@entry_id:150286)上的一个有限维近似。该问题的解由下式给出：
$$
A_{DMD} = X' X^\dagger
$$
其中 $X^\dagger$ 是 $X$ 的**摩尔-彭若斯[伪逆](@entry_id:140762) (Moore-Penrose pseudoinverse)**。$A_{DMD}$ 的[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)（即**DMD[特征值](@entry_id:154894)**和**DMD模态**）分别近似了[库普曼算子](@entry_id:183136)的[特征值](@entry_id:154894)和模态。

在实际计算中，特别是当[状态空间](@entry_id:177074)维数很高而快照数量较少时，直接计算 $A_{DMD}$ 是不切实际的。一种更稳定且高效的方法是基于[奇异值分解](@entry_id:138057)（SVD）。算法步骤如下 [@problem_id:3383155]：
1.  对快照矩阵 $X$ 进行SVD分解：$X = U \Sigma V^*$，其中 $U$ 和 $V$ 是酉矩阵，$\Sigma$ 是[对角矩阵](@entry_id:637782)，包含了奇异值。
2.  构建一个低维的**降阶算子 (reduced operator)** $\tilde{A}$：
    $$
    \tilde{A} = U^* X' V \Sigma^{-1}
    $$
    这个算子 $\tilde{A}$ 的维度由 $X$ 的秩决定，通常远小于原始[状态空间](@entry_id:177074)的维度。重要的是，$\tilde{A}$ 的非零[特征值](@entry_id:154894)与高维算子 $A_{DMD}$ 的非零[特征值](@entry_id:154894)完全相同。
3.  求解 $\tilde{A}$ 的[特征值问题](@entry_id:142153)：$\tilde{A}W = W\Lambda$，其中 $\Lambda$ 是包含DMD[特征值](@entry_id:154894) $\lambda_j$ 的对角矩阵，$W$ 的列是 $\tilde{A}$ 的[特征向量](@entry_id:151813)。
4.  重构高维的DMD模态。DMD模态 $\phi_j$ 是高维算子 $A_{DMD}$ 的近似[特征向量](@entry_id:151813)，它们可以通过将低维[特征向量](@entry_id:151813) $w_j$（$W$的列）投影回高维空间来计算。DMD模态矩阵 $\Phi$ 可由下式计算：
    $$
    \Phi = U W
    $$

#### 示例计算与模态归一化

让我们通过一个简单的例子来走查这个过程 [@problem_id:3383155]。假设我们有以下快照矩阵：
$$
X = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix}, \quad X' = \begin{pmatrix} 0  -2 \\ 1  3 \end{pmatrix}
$$
由于 $X=I$ 是[单位矩阵](@entry_id:156724)，其SVD是平凡的：$U=I, \Sigma=I, V=I$。
降阶算子 $\tilde{A} = U^* X' V \Sigma^{-1} = I X' I I^{-1} = X'$。
我们计算 $\tilde{A} = \begin{pmatrix} 0  -2 \\ 1  3 \end{pmatrix}$ 的[特征值](@entry_id:154894)和[特征向量](@entry_id:151813)。特征方程为 $\lambda^2 - 3\lambda + 2 = 0$，解得DMD[特征值](@entry_id:154894)为 $\lambda_1=1$ 和 $\lambda_2=2$。对应的[特征向量](@entry_id:151813)（$W$的列）为 $w_1 = \begin{pmatrix} -2 \\ 1 \end{pmatrix}$ 和 $w_2 = \begin{pmatrix} -1 \\ 1 \end{pmatrix}$。
DMD模态矩阵为 $\Phi = U W = I W = W$。因此，DMD模态就是$\tilde{A}$的[特征向量](@entry_id:151813)：
$$
\Phi = \begin{pmatrix} -2 & -1 \\ 1 & 1 \end{pmatrix}
$$
因此，DMD模态为 $\phi_1 = \begin{pmatrix} -2 \\ 1 \end{pmatrix}$ 和 $\phi_2 = \begin{pmatrix} -1 \\ 1 \end{pmatrix}$。

在重建动力学时，任何快照都可以近似为DMD模态的[线性组合](@entry_id:154743)：$x_k \approx \sum_j b_j \phi_j \lambda_j^k$。这里存在一个尺度模糊性：我们可以将模态 $\phi_j$ 乘以一个常数 $g$，同时将相应的振幅 $b_j$ 除以 $g$，而其乘积保持不变。为了获得物理解释清晰的模态和振幅，通常采用**模态归一化**。一个自然的选择是将每个DMD模态的[欧几里得范数](@entry_id:172687)归一化为1，即 $\|\phi_j\|_2 = 1$。在这种约定下，模态代表了一个具有单位能量的纯空间结构，而其振幅的模 $|b_j|$ 则直接量化了该模态对系统总能量的贡献 [@problem_id:3383155]。

### 解读DMD结果及与其他方法的比较

[DMD算法](@entry_id:748617)的输出是DMD[特征值](@entry_id:154894) $\lambda_j$ 和DMD模态 $\phi_j$。这些量需要被正确地解释。

- **连续时间谱**: 离散时间[特征值](@entry_id:154894) $\lambda_j$ 与连续时间库普曼[特征值](@entry_id:154894) $\omega_j$ 通过关系 $\lambda_j = \exp(\omega_j \Delta t)$ 相关联。因此，我们可以通过复数对数来恢复连续时间[特征值](@entry_id:154894)：
  $$
  \omega_j = \frac{\ln(\lambda_j)}{\Delta t} = \frac{\ln|\lambda_j|}{\Delta t} + i \frac{\arg(\lambda_j)}{\Delta t}
  $$
  其中，实部 $\Re(\omega_j)$ 是模态的增长率（正值）或衰减率（负值），虚部 $\Im(\omega_j)$ 是其[振荡](@entry_id:267781)的角频率。

- **[采样与混叠](@entry_id:268188)**: 在从离散数据中恢复连续频率时，必须考虑**[奈奎斯特-香农采样定理](@entry_id:262499) (Nyquist-Shannon sampling theorem)**。复数对数是多值的，$\arg(\lambda_j)$ 只能在 $(-\pi, \pi]$ 的[主值](@entry_id:189577)区间内确定。这意味着可唯一辨识的角频率范围为 $(-\frac{\pi}{\Delta t}, \frac{\pi}{\Delta t}]$。如果真实频率 $|\omega|$ 超出了这个范围，即 $|\omega| > \omega_{\text{Nyquist}} = \frac{\pi}{\Delta t}$，就会发生**混叠 (aliasing)**。DMD会报告一个被“折叠”到[主值](@entry_id:189577)区间内的混叠频率 $\omega_{\text{aliased}} = \omega + m \frac{2\pi}{\Delta t}$，其中整数 $m$ 使得 $\omega_{\text{aliased}}$ 位于该区间内 [@problem_id:3383178]。因此，确保采样率足够高以避免感兴趣的频率发生混叠是至关重要的。

- **与[本征正交分解](@entry_id:165074) (POD) 的比较**: DMD常与另一种流行的[降维](@entry_id:142982)方法——[本征正交分解](@entry_id:165074)（Proper Orthogonal Decomposition, POD）相比较。两者虽有联系，但目标截然不同 [@problem_id:3383145]。
    - **优化目标**: POD（也称为主成分分析, PCA）旨在寻找一个正交基，使得数据投影到该基上的[方差](@entry_id:200758)（或能量）最大化。因此，POD模态在数据压缩和表示方面是最优的。相比之下，DMD旨在寻找描述[相干时间](@entry_id:176187)演化的结构，每个DMD模态都与一个固定的振荡频率和增长/衰减率相关联。
    - **模态性质**: POD模态根据其能量贡献排序，并且总是相互正交的。DMD模态通常是非正交的，因为它们是通常非正规的动力学算子 $A_{DMD}$ 的[特征向量](@entry_id:151813)。
    - **联系**: 在一个特殊情况下，即当数据仅由一个单一的空间结构按纯指数规律演化时（例如 $x_k = \mathbf{v} \lambda^k$），系统的秩为1。此时，唯一的非平凡POD模态和DMD模态会重合，都等于 $\mathbf{v}$ [@problem_id:3383145]。这个例子清晰地揭示了POD关注空间结构本身，而DMD关注按指数规律演化的结构。

### 高级主题与实践考量

在将DMD应用于源自PDE的复杂系统时，一些更深层次的问题会显现出来。

#### [非正规系统](@entry_id:270295)与伪谱

许多物理系统，特别是[流体动力学](@entry_id:136788)中的系统，经离散化后由**非正规 (non-normal)** 矩阵 $A$（即 $AA^* \neq A^*A$）描述。对于这类系统，仅凭[特征值](@entry_id:154894)不足以完全刻画其动力学行为。即使所有[特征值](@entry_id:154894)都表明系统是稳定的（例如，所有 $|\lambda_j| < 1$），系统的解范数也可能在最终衰减之前经历显著的**[瞬时增长](@entry_id:263654) (transient growth)**。

这种现象可以通过**$\epsilon$-[伪谱](@entry_id:138878) ($\epsilon$-pseudospectrum)** 的概念来理解 [@problem_id:3383150]。矩阵 $A$ 的 $\epsilon$-[伪谱](@entry_id:138878) $\Lambda_\epsilon(A)$ 是复平面上的一个区域，其中包含了 $A$ 的[特征值](@entry_id:154894)以及那些在微小扰动下可能成为[特征值](@entry_id:154894)的点。它有两个等价的定义：
1.  基于分辨率范数：$\Lambda_\epsilon(A) = \{ z \in \mathbb{C} : \|(zI-A)^{-1}\| > 1/\epsilon \}$。
2.  基于奇异值：$\Lambda_\epsilon(A) = \{ z \in \mathbb{C} : \sigma_{\min}(zI-A) < \epsilon \}$。

对于[非正规矩阵](@entry_id:752668)，其伪谱可能远远超出其谱（[特征值](@entry_id:154894)集合）。如果[伪谱](@entry_id:138878)区域延伸到[单位圆](@entry_id:267290)外，即使所有[特征值](@entry_id:154894)都在单位圆内，也预示着可能发生[瞬时增长](@entry_id:263654)。这是因为解的范数 $\|A^k\|$ 可以通过围绕谱的围[线积分](@entry_id:141417)来界定，其大小与分辨率范数 $\|(zI-A)^{-1}\|$ 直接相关 [@problem_id:3383150]。当分辨率范数在单位圆附近很大时，$\|A^k\|$ 的[上界](@entry_id:274738)也会很大。

DMD作为一种投影方法，其计算出的[特征值](@entry_id:154894)（称为[里兹值](@entry_id:145862)）对[非正规性](@entry_id:752585)很敏感。可能会出现“伪”[特征值](@entry_id:154894)，它们并不靠近任何真实的库普曼[特征值](@entry_id:154894)，但位于伪谱区域内。这并非算法失败，而是[非正规系统](@entry_id:270295)内在的谱不稳定性的一种体现 [@problem_id:3383150]。

#### 数值积分方案的影响

生成快照数据所用的[时间积分方法](@entry_id:136323)会直接影响DMD分析的结果。DMD分析的是**数值生成**的动力学，而非底层的**真实连续**动力学。

考虑一个由矩阵 $A$ 控制的[半离散系统](@entry_id:754680) $\dot{\mathbf{u}} = A\mathbf{u}$，其真实解的演化由 $\exp(\lambda \Delta t)$ 决定，其中 $\lambda$ 是 $A$ 的[特征值](@entry_id:154894)。如果我们使用一个[数值积分器](@entry_id:752799)（如经典的[四阶龙格-库塔法](@entry_id:138005), RK4）来生成快照，那么一步演化算子不再是 $\exp(A \Delta t)$，而是由该[积分器](@entry_id:261578)的**[稳定性函数](@entry_id:178107) (stability function)** $R(z)$ 决定的 $R(A \Delta t)$。对于RK4，[稳定性函数](@entry_id:178107)是 $R(z) = 1 + z + \frac{z^2}{2} + \frac{z^3}{6} + \frac{z^4}{24}$。因此，DMD从这些快照中提取的离散时间[特征值](@entry_id:154894)将是 $\mu = R(\lambda \Delta t)$，而不是 $\exp(\lambda \Delta t)$ [@problem_id:3383120]。这一偏差在解释DMD结果时必须予以考虑，尤其是在高精度要求的场合。

#### 测量噪声的影响

标准[DMD算法](@entry_id:748617)对[测量噪声](@entry_id:275238)很敏感。假设我们的测量过程为 $\tilde{X} = X + E$，其中 $E$ 是噪声矩阵。如果只有“输入”快照矩阵 $X$ 受到[噪声污染](@entry_id:188797)，而“输出”矩阵 $Y$ 是无噪声的（即 $Y=AX$），那么DMD估计的算子为 $\tilde{A} = Y \tilde{X}^\dagger$。这是一个经典的**变量含误差 (errors-in-variables)** 回归问题。

可以证明，在这种情况下，即使在大量样本的极限下，估计的算子 $\tilde{A}$ 也是有偏的 [@problem_id:3383172]。对于平稳遍历过程，在大样本极限下，有：
$$
\lim_{n \to \infty} \mathbb{E}[\tilde{A}] = (A \Sigma_{xx}) (\Sigma_{xx} + \sigma^2 I)^{-1}
$$
其中 $\Sigma_{xx}$ 是真实状态的协方差矩阵，$\sigma^2$ 是噪声[方差](@entry_id:200758)。与真实算子 $A$ 的偏差（称为[衰减偏误](@entry_id:746571)）的一阶近似为：
$$
B = \lim_{n \to \infty} \mathbb{E}[\tilde{A}] - A \approx -\sigma^2 A \Sigma_{xx}^{-1}
$$
这个偏差的存在促使了对[DMD算法](@entry_id:748617)的改进。一种重要的变体是**总体最小二乘DMD (Total Least Squares DMD, TLS-DMD)** [@problem_id:3383161]。TLS-DMD假设 $X$ 和 $X'$ 都受到[噪声污染](@entry_id:188797)，并试图寻找一个对数据矩阵的最小范数扰动 $(\Delta X, \Delta X')$，使得修正后的数据满足一个精确的线性关系 $(X'+\Delta X') = A(X+\Delta X)$。

这个问题可以通过对[增广矩阵](@entry_id:150523) $Z = \begin{bmatrix} X \\ X' \end{bmatrix}$ 的SVD来解决。该问题的解对应于 $Z$ 的最佳秩-1近似。对于一维系统，可以证明最优算子 $A$ 由 $Z$ 的主[左奇异向量](@entry_id:751233) $u_1 = \begin{pmatrix} u_{11} \\ u_{21} \end{pmatrix}$ 的分量之比给出：$A = u_{21}/u_{11}$ [@problem_id:3383161]。这种方法通过同时考虑两个数据矩阵中的误差，提供了对噪声更鲁棒的估计。