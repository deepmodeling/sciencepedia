## 引言
原子核平均场理论在描述原子核的集体特性（如形变）方面取得了巨大成功，但它也引入了一个基本问题：其解（内禀态）通常会破坏哈密顿量固有的旋转对称性。这意味着由平均场理论直接得到的形变态，本身并不是具有确定角动量量子数的物理态，无法直接与实验观测的能级谱进行比较。本文旨在系统性地解决这一知识鸿沟，详细阐述角动量投影这一核心技术，它能够从对称性破缺的内禀态中精确恢复对称性，并提取出具有良好角动量的物理态。

在本文中，读者将踏上一段从理论基础到实际应用的完整学习之旅。在“原理与机制”一章中，我们将深入探讨自发对称性破缺的根源，构建角动量投影算符，并推导计算投影能量和矩阵元的具体公式。接着，在“应用与跨学科连接”一章中，我们将展示该方法在描述原子核转动带、形状共存以及与其他理论模型（如摇摆模型和GCM）结合中的强大能力，并探索其在超冷原子等其他量子系统中的应用。最后，通过“动手实践”部分，读者将有机会通过编程练习，亲手实现和验证投影计算中的关键数值算法，从而将理论知识转化为实践技能。

## 原理与机制

在上一章中，我们介绍了原子核平均场理论的基本概念，特别是它在描述原子核集体性质（如形变）方面的成功。然而，平均场近似本身引入了一个深刻的理论问题：它破坏了原子核[哈密顿量](@entry_id:172864)所固有的基本对称性。本章将深入探讨这一问题的根源，并系统地阐述如何通过**角动量投影 (angular momentum projection)** 这一关键技术来恢复旋转对称性，从而能够从对称性破缺的内禀态中提取出具有良好角动量量子数的物理态，并计算其性质。

### 平均场理论中的自发对称性破缺

描述原子核的多体哈密顿量 $\hat{H}$ 是一个标量，它在三维空间的所有转动操作下保持不变。这意味着 $\hat{H}$ 与任何转动算符 $\hat{R}(\Omega)$ 对易，即 $[\hat{H}, \hat{R}(\Omega)]=0$，其中 $\Omega$ 代表欧拉角。一个直接的推论是，哈密顿量也与总角动量平方算符 $\hat{J}^2$ 对易，$[\hat{H}, \hat{J}^2]=0$。根据量子力学基本原理，这意味着哈密顿量的本征态必须同时是 $\hat{J}^2$ 的本征态，因此可以用总角动量量子数 $J$ 来标记。例如，一个偶偶核的基态总是一个 $J=0$ 的态。

然而，在诸如Hartree-Fock-Bogoliubov (HFB)之类的平均场理论中，我们并非直接求解多体薛定谔方程，而是采用变分法，在一个受限的态空间（通常是准粒子真空态的集合）中寻找能量泛函 $\langle\Phi|\hat{H}|\Phi\rangle$ 的最小值。对于远离幻数的原子核，能量最低的平均场解——我们称之为**内禀态 (intrinsic state)** $|\Phi\rangle$——通常对应一个非球形的核子密度分布 $\rho(\mathbf{r}) = \langle\Phi|\hat{\rho}(\mathbf{r})|\Phi\rangle$。这种状态被称为**形变态 (deformed state)**。

这种形变解的出现，即使在旋转不变的哈密顿量下，也是**自发对称性破缺 (spontaneous symmetry breaking)** 的一个典型例子。变分过程允许系统通过牺牲旋转对称性来获得更低的能量。一个具有静态形变（例如，非零的四极矩 $\langle\Phi|\hat{Q}_{20}|\Phi\rangle \neq 0$）的内禀态，通过其密度分布定义了一个与原子核固连的**体坐标系 (body-fixed frame)**。[@problem_id:3542224]

这里的核心矛盾在于，一个密度分布依赖于角度的量子态不可能是 $\hat{J}^2$ 的本征态。反之，任何 $\hat{J}^2$ 的本征态都必须具有球对称的密度分布。因此，一个形变的HFB真空态 $|\Phi\rangle$ 必然不具有良好的总角动量量子数 $J$。它实际上是一个**波包 (wave packet)**，可以看作是哈密顿量不同角动量 $J$ 的精确本征态的相干叠加：
$$
|\Phi\rangle = \sum_{J,M,k} c_{JMK} |E_{Jk}, J, M\rangle
$$
其中 $|E_{Jk}, J, M\rangle$ 是哈密顿量的精确本征态。由于 $|\Phi\rangle$ 是形变的，这个展开式中必须包含多个不同的 $J$ 值。[@problem_id:3542224]

因此，形变的内禀态本身并非一个可与实验直接比较的物理态。为了计算形变核的转动谱等可观测量，我们必须从这个“混合”的内禀态中“筛选”出具有特定角动量 $J$ 的成分。实现这一目标的数学工具就是角动量投影。

### 核心工具：角动量投影算符

角动量投影的数学基础源于群论和旋转群 $SO(3)$ 的表示理论。其核心是**角动量投影算符 (angular momentum projection operator)**，它利用了旋转算符及其矩阵表示（维格纳D函数）的正交性。

三维空间中的任意转动可以通过三个欧拉角 $\Omega \equiv (\alpha, \beta, \gamma)$ 来参数化。相应的量子力学转动算符 $\hat{R}(\Omega)$ 是由总角动量算符 $\hat{\mathbf{J}}=(\hat{J}_x, \hat{J}_y, \hat{J}_z)$ 生成的。采用 $z$-$y$-$z$ 约定，转动算符可以写成三个基本转动的乘积：
$$
\hat{R}(\Omega) = e^{-i\alpha \hat{J}_z} e^{-i\beta \hat{J}_y} e^{-i\gamma \hat{J}_z}
$$
其中我们设定 $\hbar=1$。该算符在角动量共同本征基 $\{|JM\rangle\}$ 中的矩阵元定义了**维格纳D函数 (Wigner D-function)**：
$$
D^J_{MK}(\Omega) = \langle JM | \hat{R}(\Omega) | JK \rangle = e^{-iM\alpha} d^J_{MK}(\beta) e^{-iK\gamma}
$$
其中 $d^J_{MK}(\beta) = \langle JM | e^{-i\beta \hat{J}_y} | JK \rangle$ 是维格纳小d函数。$M$ 和 $K$ 分别是角动量在实验室坐标系和体坐标系 $z$ 轴上的投影。[@problem_id:3542243]

维格纳D函数构成了旋转群上的一个完备正交函数集。它们的正交性关系，即**群论大正交定理 (Great Orthogonality Theorem)** 在 $SO(3)$ 上的具体体现为：
$$
\int d\Omega \, D^{J*}_{MK}(\Omega) D^{J'}_{M'K'}(\Omega) = \frac{8\pi^2}{2J+1} \delta_{JJ'} \delta_{MM'} \delta_{KK'}
$$
这里的积分测度是哈尔测度 $d\Omega = d\alpha \sin\beta d\beta d\gamma$，积分范围为 $\alpha \in [0, 2\pi)$, $\beta \in [0, \pi]$, $\gamma \in 0, 2\pi)$，其总体积为 $\int d\Omega = 8\pi^2$。

利用此正交性，我们可以构建一个算符，它能从任意态中提取出具有特定角动量 $(J, M)$ 的分量。这个算符就是**[投影算符** $\hat{P}^J_{MK}$：
$$
\hat{P}^J_{MK} = \frac{2J+1}{8\pi^2} \int d\Omega \, D^{J*}_{MK}(\Omega) \hat{R}(\Omega)
$$
这个算符的作用是，当它作用于一个角动量本征态 $|J'M'\rangle$ 的任意线性组合时，它会“消灭”所有角动量不等于 $J$ 的分量，并从具有角动量 $J$ 的分量中挑选出特定的 $M, K$ 组合。因此，将 $\hat{P}^J_{MK}$ 作用于形变的内禀态 $|\Phi\rangle$，我们就能得到一个具有良好角动量量子数 $J$ 和实验室投影 $M$ 的态。[@problem_id:3542243]

### 计算投影态能量：核与积分

获得了具有良好角动量的投影态 $|\Psi^J_{MK}\rangle = \hat{P}^J_{MK}|\Phi\rangle$ 后，我们就可以计算其物理性质，其中最重要的是能量。投影态的能量由瑞利商 (Rayleigh quotient) 给出：
$$
E^J = \frac{\langle\Psi^J_{MK}|\hat{H}|\Psi^J_{MK}\rangle}{\langle\Psi^J_{MK}|\Psi^J_{MK}\rangle} = \frac{\langle\Phi|\hat{H} \hat{P}^J_{MM}|\Phi\rangle}{\langle\Phi|\hat{P}^J_{MM}|\Phi\rangle}
$$
这里我们使用了投影算符的性质 $(\hat{P}^J_{MK})^\dagger = \hat{P}^J_{KM}$ 和 $\hat{P}^J_{MK}\hat{P}^J_{K'M'} = \delta_{KK'} \hat{P}^J_{MM'}$，并假设我们对角投影 ($M=K$)。由于哈密顿量是旋转不变的，能量 $E^J$ 不依赖于实验室坐标系中的投影 $M$。

为了进行实际计算，我们将投影算符的积分形式代入上式。这引出了两个核心的计算量：**核仁 (kernel)**。
1.  **模核 (Norm kernel)**: $n(\Omega) \equiv \langle\Phi|\hat{R}(\Omega)|\Phi\rangle$
2.  **哈密顿量核 (Hamiltonian kernel)**: $h(\Omega) \equiv \langle\Phi|\hat{H}\hat{R}(\Omega)|\Phi\rangle$

这两个核是内禀态 $|\Phi\rangle$ 与其旋转后的版本 $\hat{R}(\Omega)|\Phi\rangle$ 之间的交叠矩阵元。它们包含了关于系统动力学和结构的所有信息。使用这两个核，投影能量的分子和分母可以分别写成：
$$
\langle\Phi|\hat{H}\hat{P}^J_{MM}|\Phi\rangle = \frac{2J+1}{8\pi^2} \int d\Omega \, D^{J*}_{MM}(\Omega) \langle\Phi|\hat{H}\hat{R}(\Omega)|\Phi\rangle = \frac{2J+1}{8\pi^2} \int d\Omega \, D^{J*}_{MM}(\Omega) h(\Omega)
$$
$$
\langle\Phi|\hat{P}^J_{MM}|\Phi\rangle = \frac{2J+1}{8\pi^2} \int d\Omega \, D^{J*}_{MM}(\Omega) \langle\Phi|\hat{R}(\Omega)|\Phi\rangle = \frac{2J+1}{8\pi^2} \int d\Omega \, D^{J*}_{MM}(\Omega) n(\Omega)
$$
因此，投影能量 $E^J$ 的最终表达式为：
$$
E^J = \frac{\int d\Omega \, D^{J*}_{MM}(\Omega) h(\Omega)}{\int d\Omega \, D^{J*}_{MM}(\Omega) n(\Omega)}
$$
对于一个具有轴对称性且时间反演不变的偶偶核内禀态，其内禀角动量投影为 $K=0$。在这种常见情况下，我们通常选择 $M=K=0$ 来进行计算，表达式简化为：[@problem_id:3542225]
$$
E^J = \frac{\int d\Omega \, D^{J*}_{00}(\Omega) h(\Omega)}{\int d\Omega \, D^{J*}_{00}(\Omega) n(\Omega)} = \frac{\int_0^\pi d\beta \sin\beta \, P_J(\cos\beta) h(\beta)}{\int_0^\pi d\beta \sin\beta \, P_J(\cos\beta) n(\beta)}
$$
其中 $D^J_{00}(\Omega) = P_J(\cos\beta)$ 是勒让德多项式，并且由于轴对称性，核 $h$ 和 $n$ 只依赖于角度 $\beta$。这个公式将抽象的投影操作转化为了一个具体的、可以通过数值积分求解的问题。

### 内禀对称性与K量子数

在投影公式中自然出现的量子数 $K$——角动量在体坐标系 $z$ 轴上的投影——其物理意义和处理方式与内禀态 $|\Phi\rangle$ 的对称性密切相关。

#### 轴对称情形

如果内禀态 $|\Phi\rangle$ 具有**轴对称性 (axial symmetry)**，即它在围绕体坐标系 $z$ 轴的任意旋转下保持不变（最多相差一个相位），那么它就是算符 $\hat{J}_z$ 的本征态。其本征值就是 $K$。
$$
\hat{R}_z(\phi)|\Phi\rangle = e^{-iK\phi}|\Phi\rangle
$$
在这种情况下，$K$ 是内禀态的一个好量子数。
- 对于一个保持时间反演不变的偶偶核HFB真空态，所有核子成对占据，每个 $(m, -m)$ 对的总角动量投影为零，因此整个内禀态的 $K=0$。[@problem_id:3542296]
- 对于奇A核，其低激发态通常通过在偶偶核芯上阻塞一个准粒子来描述，即 $|\Phi_\mu\rangle = \hat{\beta}^\dagger_\mu |\Phi_0\rangle$。如果核芯是轴对称的，那么整个态的 $K$ 值就由被阻塞的准粒子的角动量投影 $\Omega_\mu$ 决定，即 $K = \Omega_\mu$。[@problem_id:3542296]
当 $K$ 是好量子数时，从单个内禀态 $|\Phi\rangle$ 投影出的态构成一个具有固定 $K$ 值的转动带。

#### 三轴不对称情形与K混合

当内禀态不具有轴对称性，而是**三轴不对称 (triaxial)** 时，它不再是 $\hat{J}_z$ 的本征态。这意味着 $K$ 不再是内禀态的好量子数，内禀态本身可以看作是不同 $K$ 值分量的叠加。
$$
|\Phi\rangle = \sum_K c_K |\Phi_K\rangle
$$
因此，一个具有良好总角动量 $J$ 的物理态，也必须是这些不同 $K$ 分量投影结果的线性组合，这一现象称为 **K混合 (K-mixing)**。一个一般的投影态可以写成：
$$
|\Psi^J_M\rangle = \sum_{K=-J}^{J} f_K \hat{P}^J_{MK} |\Phi\rangle
$$
其中系数 $f_K$ 需要通过变分法（如求解Hill-Wheeler-Griffin方程）来确定。该态的归一化模方为：[@problem_id:3542234]
$$
\langle\Psi^J_M|\Psi^J_M\rangle = \sum_{K, K'=-J}^J f_K^* f_{K'} \langle\Phi|\hat{P}^J_{KK'}|\Phi\rangle = \sum_{K, K'=-J}^J f_K^* f_{K'} N^J_{KK'}
$$
其中 $N^J_{KK'} \equiv \langle\Phi|\hat{P}^J_{KK'}|\Phi\rangle$ 是模核矩阵元。

尽管在三轴形变中 $K$ 不再是好量子数，但内禀态可能仍然具有某些离散对称性。例如，许多三轴形变态具有 **$D_2$ 对称性**，即在绕三个主轴旋转 $\pi$ 角时保持不变。这种对称性会带来重要的简化：[@problem_id:3542279] [@problem_id:3542296]
1.  **K值选择定则**：$\hat{R}_z(\pi)$ 不变性导致哈密顿量和模核矩阵元 $\mathcal{H}^J_{K'K}, \mathcal{N}^J_{K'K}$ 只有在 $K-K'$ 为偶数时才非零。这意味着基态转动带（包含 $J=0$ 态）只能由偶数 $K$ 值 ($K=0, 2, 4, \dots$) 的分量混合而成。
2.  **积分区域缩减**：$D_2$ 对称性使得核 $n(\Omega)$ 和 $h(\Omega)$ 在欧拉角空间中具有更高的周期性。这使得计算这些核所需的积分范围可以从整个欧拉角空间（体积 $8\pi^2$）缩减到其八分之一，即 $\alpha, \gamma \in [0, \pi)$, $\beta \in [0, \pi/2]$，极大地节约了计算成本。

### 变分原理：变分前投影或变分后投影？

既然我们能够从任意给定的内禀态 $|\Phi\rangle$ 计算出投影能量 $E^J$，一个自然的问题是：我们应该如何选择最优的内禀态？这引出了两种主要的计算策略。

#### 变分后投影(PAV)与变分前投影(VAP)

- **变分后投影 (Projection-After-Variation, PAV)**：这是计算上最简单的方法。首先，通过最小化平均场能量 $E_{\text{MF}}[\Phi] = \langle\Phi|\hat{H}|\Phi\rangle$ 来确定唯一的内禀态 $|\Phi_{\text{MF}}\rangle$。然后，将这个固定的 $|\Phi_{\text{MF}}\rangle$ 作为所有不同角动量 $J$ 的投影计算的出发点，得到一系列能量 $E^J[|\Phi_{\text{MF}}\rangle]$。PAV的优点是计算量小，但它并非对每个 $J$ 都严格满足变分原理，因为用于投影的内禀态是为了最小化平均场能量，而非特定 $J$ 的投影能量。[@problem_id:3542306]

- **变分前投影 (Variation-After-Projection, VAP)**：这是一个更严格但也更耗时的方法。其目标是为每一个角动量 $J$ 单独最小化其投影能量 $E^J[|\Phi\rangle]$。
$$
E^J_{\text{VAP}} = \min_{|\Phi\rangle} E^J[|\Phi\rangle] = \min_{|\Phi\rangle} \frac{\langle\Phi|\hat{H}\hat{P}^J|\Phi\rangle}{\langle\Phi|\hat{P}^J|\Phi\rangle}
$$
这意味着对于不同的 $J$ 值，最优的内禀态 $|\Phi^J_{\text{VAP}}\rangle$ 可能是不同的（例如，随着 $J$ 增大，原子核可能会被拉伸，最优形变会改变）。根据瑞利-里兹变分原理，对于一个真正的哈密顿量 $\hat{H}$，VAP方法给出的能量总是低于或等于PAV方法给出的能量，即 $E^J_{\text{VAP}} \le E^J[\Phi_{\text{MF}}]$，因此它是一个更优的近似。[@problem_id:3542306]

如果一个内禀态碰巧已经是 $\hat{J}^2$ 的本征态（例如，球形核的 $J=0$ 平均场基态），那么投影操作是多余的，PAV和VAP会给出完全相同的结果。[@problem_id:3542306]

#### 产生子坐标方法(GCM)与自然基

VAP方法可以被推广到更一般框架，即**产生子坐标方法 (Generator Coordinate Method, GCM)**。在GCM中，我们不仅限于单个内禀态，而是构建一个由“产生子坐标” $q$（例如，形变参数）标记的一系列内禀态 $\{|\Phi(q)\rangle\}$。一个物理态 $|\Psi^J_\alpha\rangle$ 被构造为这些投影态的线性叠加：
$$
|\Psi^J_\alpha\rangle = \sum_q \sum_K f^J_{\alpha}(q, K) \hat{P}^J_{MK} |\Phi(q)\rangle
$$
通过对能量 $\langle\Psi^J_\alpha|\hat{H}|\Psi^J_\alpha\rangle$ 进行变分，可以导出著名的**Hill-Wheeler-Griffin (HWG) 方程**，这是一个广义厄米本征方程：[@problem_id:3542307]
$$
\sum_{q', K'} \mathcal{H}^J(q,K; q',K') f^J_\alpha(q', K') = E^J_\alpha \sum_{q', K'} \mathcal{N}^J(q,K; q',K') f^J_\alpha(q', K')
$$
其中 $\mathcal{H}^J$ 和 $\mathcal{N}^J$ 是哈密顿量和模核矩阵。由于投影后的基底 $\{ \hat{P}^J_{MK}|\Phi(q)\rangle \}$ 通常是非正交的，模矩阵 $\mathcal{N}^J$ 不是单位矩阵。

数值求解HWG方程的一个关键步骤是处理模矩阵 $\mathcal{N}^J$ 的近奇异性。由于不同产生子坐标对应的态可能存在线性冗余，$\mathcal{N}^J$ 的某些本征值可能非常接近于零。直接求解广义本征问题会非常不稳定。标准做法是通过构建**自然基 (natural basis)** 来解决此问题：[@problem_id:3542307]
1.  对角化模矩阵 $\mathcal{N}^J$。
2.  舍弃那些本征值小于某个阈值 $\varepsilon$ 的本征矢，从而消除线性冗余，并将问题限制在一个稳定的、物理相关的子空间内。
3.  利用保留下来的本征矢和本征值的平方根倒数，构建一个变换矩阵 $X$。
4.  使用 $X$ 将HWG方程变换为一个标准的厄米本征问题 $\tilde{\mathcal{H}} c = E c$，其中 $\tilde{\mathcal{H}} = X^\dagger \mathcal{H} X$。这个标准本征问题可以被稳定地数值求解。

### 高级专题：理论挑战与实践考量

#### 能量密度泛函的投影问题

现代核结构计算中广泛使用的许多能量密度泛函 (EDF)，如Skyrme或Gogny泛函的某些变体，包含对核子密度 $\rho(\mathbf{r})$ 的显式依赖项，例如 $C[\rho]\rho^\alpha$ 形式的项。当我们将投影方法应用于这类泛函时，会出现严重的理论困难。

问题源于如何定义非对角的能量核 $h(\Omega)$。一个看似自然的方法是使用所谓的**跃迁密度 (transition density)** $\rho^{\text{trans}}(\mathbf{r};\Omega) = \langle\Phi|\hat{\rho}(\mathbf{r})\hat{R}(\Omega)|\Phi\rangle/n(\Omega)$ 来计算能量泛函。然而，这种做法破坏了哈密顿量算符应有的线性、双线性的算符结构。它导致能量核 $h(\Omega)$ 对模核 $n(\Omega)$ 表现出非物理的依赖关系，例如 $h(\Omega) \propto n(\Omega)^{-\alpha}$。当 $n(\Omega) \to 0$ 时（对应于大角度旋转），这会导致投影能量的被积函数发散。这种**非变分行为**破坏了能量最小化原理的根基。这种效应也被称为**赝自相互作用 (spurious self-interaction)**。[@problem_id:3542264]

为了解决这个问题，必须采取**正则化 (regularization)** 措施。一个被广泛接受的方案是，在计算非对角能量核 $h(\Omega)$ 时，将泛函中所有密度依赖的部分（如耦合常数 $C[\rho]$）“冻结”在由某个参考态（通常是未旋转的内禀态 $|\Phi\rangle$）的密度 $\rho_0(\mathbf{r})$ 计算出的值上。这相当于从单参考态的计算中导出一个固定的、与状态无关的有效哈密顿量，然后用这个哈密顿量来计算所有的跃迁矩阵元。这种方法恢复了能量核的正确标度行为，从而保证了变分计算的稳定性。[@problem_id:3542264]

#### 投影算符的对易性

在理论上，产生不同对称性（如粒子数和角动量）的投影算符是相互对易的，例如 $[\hat{P}^N, \hat{P}^J]=0$。这意味着投影的顺序无关紧要。然而，在数值实现中，我们用有限的求积格点来近似连续积分。这些离散化的投影算符通常不再严格对易。因此，在实践中，先做粒子数投影再做角动量投影 ($P^J P^N |\Phi\rangle$)，与先做角动量投影再做粒子数投影 ($P^N P^J |\Phi\rangle$)，可能会得到略微不同的能量。这种差异的大小取决于求积格点的密度，当格点越来越密，积分越来越精确时，这种差异会趋于零。[@problem_id:3542220] 对于一个本身就具有良好角动量的内禀态，角动量投影是多余的，这种非对易性效应自然消失。