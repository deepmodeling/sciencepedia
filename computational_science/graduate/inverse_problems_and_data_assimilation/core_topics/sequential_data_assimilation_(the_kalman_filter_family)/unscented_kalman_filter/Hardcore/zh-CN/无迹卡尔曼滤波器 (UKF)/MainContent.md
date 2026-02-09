## 引言
在众多科学与工程领域，从动态系统中准确估计其不可见的内部状态是一项核心任务。经典的卡尔曼滤波器为线性高斯系统提供了最优解，然而，现实世界中的系统——无论是机器人的运动、生物细胞的内部活动，还是金融市场的波动——普遍存在非线性。这种非线性使得传统方法（如扩展卡尔曼滤波器EKF）因线性化近似而精度受限，从而催生了对更先进估计技术的需求。

无迹卡尔曼滤波器（Unscented Kalman Filter, UKF）正是为应对这一挑战而生的一种强大而优雅的解决方案。它创造性地提出“近似概率分布比近似非线性函数更容易”，通过一种名为无迹变换的确定性采样策略，实现了对非线性系统状态的高精度估计，且无需计算复杂的雅可比矩阵。本文旨在为读者提供一份关于UKF的全面指南，从其深刻的理论基础到其广泛的实践应用。

我们的探索之旅将分为三个部分。首先，在“原理与机制”一章中，我们将深入UKF的数学核心，从贝叶斯滤波的根基出发，详细阐述无迹变换的精髓，并推导完整的UKF算法流程与数值稳定化技术。接着，在“应用与跨学科连接”一章中，我们将展示UKF如何从一个理论模型转变为解决实际问题的利器，探讨其在参数估计、约束处理、以及在生物学、物理学和机器人学等前沿领域的应用。最后，通过“动手实践”部分，您将通过具体的编程练习，亲手实现并对比不同的滤波器，从而真正巩固所学知识，并洞察其在特定场景下的优势与局限。现在，让我们一同踏上这段揭示非线性世界动态奥秘的旅程。

## 原理与机制

在“引言”部分，我们已经确立了状态估计在诸多科学与工程领域中的核心地位，并初步探讨了非线性系统带来的挑战。本章将深入剖析无迹卡尔曼滤波器（Unscented Kalman Filter, UKF）的根本原理与内在机制。我们将从贝叶斯滤波的理论基础出发，揭示标准卡尔曼滤波器在线性高斯假设下的最优性及其在非线性场景中的局限性。随后，我们将系统地阐述作为UKF核心的无迹变换（Unscented Transform, UT），包括其sigma点和权重的生成方法、其在高阶矩匹配中的作用，以及它如何精确地近似非线性函数下的概率分布传播。最后，我们将整合这些构件，完整地推导UKF的预测与更新步骤，并探讨在实际应用中确保数值稳定性的高级技术，如平方根滤波。

### 非线性挑战：从精确递推到近似求解

所有滤波问题的理论核心是贝叶斯滤波框架，它为我们提供了一个在给定观测序列的条件下，递归地推断系统状态后验概率密度函数（PDF）的数学蓝图。对于一个离散时间的非线性状态空间模型，其形式通常如下：

- **状态方程**: $\boldsymbol{x}_k = f(\boldsymbol{x}_{k-1}) + \boldsymbol{w}_{k-1}$
- **观测方程**: $\boldsymbol{y}_k = h(\boldsymbol{x}_k) + \boldsymbol{v}_k$

其中，$\boldsymbol{x}_k \in \mathbb{R}^n$ 是系统在时间步 $k$ 的状态向量，$\boldsymbol{y}_k \in \mathbb{R}^m$ 是对应的观测向量。函数 $f$ 和 $h$ 分别代表非线性的状态转移函数和观测函数。$\boldsymbol{w}_{k-1}$ 和 $\boldsymbol{v}_k$ 分别是过程噪声和观测噪声，通常假设为零均值、协方差已知且相互独立的白噪声序列。

贝叶斯滤波通过一个两步递推过程来更新状态的概率分布 [@problem_id:3429758]。

1.  **预测（时间更新）**: 这一步利用Chapman-Kolmogorov方程，将上一时刻 $k-1$ 的后验知识 $p(\boldsymbol{x}_{k-1} \mid \boldsymbol{y}_{1:k-1})$ 向前传播，以获得当前时刻 $k$ 的先验分布 $p(\boldsymbol{x}_k \mid \boldsymbol{y}_{1:k-1})$：
    $$
    p(\boldsymbol{x}_k \mid \boldsymbol{y}_{1:k-1}) = \int p(\boldsymbol{x}_k \mid \boldsymbol{x}_{k-1}) p(\boldsymbol{x}_{k-1} \mid \boldsymbol{y}_{1:k-1}) \mathrm{d}\boldsymbol{x}_{k-1}
    $$
    此处的 $p(\boldsymbol{x}_k \mid \boldsymbol{x}_{k-1})$ 是由状态方程 $f$ 和过程噪声 $\boldsymbol{w}_{k-1}$ 的统计特性决定的状态转移概率。

2.  **更新（量测更新）**: 当获得新的观测 $\boldsymbol{y}_k$ 后，我们利用贝叶斯定理，将先验分布与观测的似然函数 $p(\boldsymbol{y}_k \mid \boldsymbol{x}_k)$ 相结合，得到更新后的后验分布 $p(\boldsymbol{x}_k \mid \boldsymbol{y}_{1:k})$：
    $$
    p(\boldsymbol{x}_k \mid \boldsymbol{y}_{1:k}) = \frac{p(\boldsymbol{y}_k \mid \boldsymbol{x}_k) p(\boldsymbol{x}_k \mid \boldsymbol{y}_{1:k-1})}{p(\boldsymbol{y}_k \mid \boldsymbol{y}_{1:k-1})}
    $$
    其中，分母 $p(\boldsymbol{y}_k \mid \boldsymbol{y}_{1:k-1})$ 是归一化常数，也称为证据或边缘似然。

理论上，这个递推关系是精确且最优的。然而，在实际应用中，它几乎总是难以处理的。对于一般的非线性函数 $f$ 和 $h$，即使初始分布是高斯分布，经过非线性变换和卷积后，预测分布和后验分布通常会变成无法用有限参数描述的复杂非高斯分布。

唯一的例外是**线性高斯（Linear-Gaussian, LG）模型**。当状态转移函数 $f$ 和观测函数 $h$ 均为线性，且初始状态、过程噪声和观测噪声均服从高斯分布时，上述贝叶斯递推中的所有概率分布在每一步都将保持为高斯分布。这个关键属性被称为**高斯封闭性**。在这种情况下，一个高斯分布完全由其均值和协方差决定，而**卡尔曼滤波器（Kalman Filter, KF）**正是为精确计算这两个矩的递推演化而生的解析解。因此，对于LG系统，卡尔曼滤波器并非一个近似，而是最优贝叶斯滤波器的精确实现 [@problem_id:3429763]。

然而，一旦系统存在非线性（即 $f$ 或 $h$ 为非线性函数），或者噪声为非高斯分布，或者噪声以非加性的方式（如乘性噪声）进入系统，高斯封闭性便被打破 [@problem_id:3429763]。例如，将一个高斯随机变量输入一个非线性函数，其输出的分布通常不再是高斯分布。这就意味着真实的后验分布不再能仅用均值和协方差来完整描述，标准卡尔曼滤波器因此失效，只能提供一个次优的近似。这正是诸如无迹卡尔曼滤波器这类高级滤波算法被提出的根本动因。它们的核心任务，就是以一种高效且精确的方式来近似这个在数学上难以处理的贝叶斯递推过程。

### 无迹变换：一种确定性采样方法

与通过对非线性函数本身进行线性化来近似（如扩展卡尔曼滤波器 EKF）的思路不同，无迹卡尔曼滤波器的核心思想是，**用一组精心挑选的样本点（sigma点）来近似概率分布，然后将这些点通过真实的非线性函数进行传播，最后根据传播后的点的统计特性来重构输出分布的均值和协方差**。这一过程被称为**无迹变换（Unscented Transform, UT）**。其精髓在于：“近似分布比近似函数更容易”。

#### Sigma点的生成与权重

假设我们有一个 $n$ 维的随机向量 $\boldsymbol{x}$，其均值为 $\boldsymbol{m}$，协方差为 $\boldsymbol{P}$。UT的目标是构造一个包含 $2n+1$ 个**sigma点** $\mathcal{X}_i$ 和相应权重 $W_i$ 的集合，使得这些点的加权均值和协方差精确匹配原始分布的均值和协方差。

点的构造通常基于协方差矩阵的平方根。设 $\boldsymbol{S}$ 是一个满足 $\boldsymbol{P} = \boldsymbol{S}\boldsymbol{S}^\top$ 的矩阵（例如，通过**Cholesky分解**得到的下三角矩阵 $\boldsymbol{S}$）。sigma点的生成规则如下 [@problem_id:3429765] [@problem_id:3429776]：
$$
\begin{aligned}
\mathcal{X}_0 = \boldsymbol{m} \\
\mathcal{X}_i = \boldsymbol{m} + \gamma (\boldsymbol{S})_i, \quad i = 1, \dots, n \\
\mathcal{X}_{i+n} = \boldsymbol{m} - \gamma (\boldsymbol{S})_i, \quad i = 1, \dots, n
\end{aligned}
$$
其中 $(\boldsymbol{S})_i$ 表示矩阵 $\boldsymbol{S}$ 的第 $i$ 列。中心点 $\mathcal{X}_0$ 位于均值处，其余 $2n$ 个点对称地分布在均值两侧，其方向由协方差矩阵的平方根的列向量决定，其散布程度由缩放因子 $\gamma$ 控制。

这个缩放因子 $\gamma$ 与一组用户可调的参数 $\alpha, \kappa$ 有关。首先定义一个复合缩放参数 $\lambda$：
$$
\lambda = \alpha^2 (n+\kappa) - n
$$
然后，$\gamma$ 被定义为 $\gamma = \sqrt{n+\lambda}$。参数 $\alpha$ 控制sigma点的散布范围，通常取一个接近0的小正数（如 $10^{-3}$ 到 $1$）；$\kappa$ 是一个次要的缩放参数，通常取 $0$ 或 $3-n$。

与sigma点相对应，有两组权重：一组用于计算均值（**均值权重** $W_i^{(m)}$），另一组用于计算协方差（**协方差权重** $W_i^{(c)}$）。它们的定义如下 [@problem_id:3429765]：
$$
\begin{aligned}
W_0^{(m)} = \frac{\lambda}{n+\lambda} \\
W_i^{(m)} = \frac{1}{2(n+\lambda)}, \quad i = 1, \dots, 2n \\
\\
W_0^{(c)} = \frac{\lambda}{n+\lambda} + (1 - \alpha^2 + \beta) \\
W_i^{(c)} = \frac{1}{2(n+\lambda)}, \quad i = 1, \dots, 2n
\end{aligned}
$$
通过这个构造，可以验证这组sigma点和权重精确地满足了前两阶矩的匹配条件：$\sum_{i=0}^{2n} W_i^{(m)} \mathcal{X}_i = \boldsymbol{m}$ 和 $\sum_{i=0}^{2n} W_i^{(c)} (\mathcal{X}_i - \boldsymbol{m})(\mathcal{X}_i - \boldsymbol{m})^\top = \boldsymbol{P}$ [@problem_id:3429776]。

#### 参数 $\beta$ 与高阶矩匹配

协方差权重中的参数 $\beta$ 用于引入关于分布高阶矩（特别是四阶矩，即峰度）的先验知识。对于高斯分布，一个重要的结论是，选择 $\beta=2$ 是最优的。这个选择可以使得UT对二次非线性变换的方差估计达到精确。

我们可以通过一个具体的例子来理解这一点。考虑一个一维高斯随机变量 $x \sim \mathcal{N}(\mu, \sigma^2)$ 和一个二次变换 $y=x^2$。该变换的真实方差为 $\text{Var}(y) = 4\mu^2\sigma^2 + 2\sigma^4$。如果我们使用UT来估计这个方差，经过推导可以发现，UT给出的估计值为 $\text{Var}_{\text{UT}}(y) = 4\mu^2\sigma^2 + \beta\sigma^4$。为了使UT估计值与真实值完全相等，必须设定 $\beta=2$ [@problem_id:3429777]。这一选择使得UT能够精确捕捉高斯分布在二次变换下的部分四阶矩信息，从而获得比简单线性化更高的近似精度。

### UKF算法流程：预测与更新

装备了无迹变换之后，我们就可以构建完整的无迹卡尔曼滤波器算法。UKF的每一个循环同样包含预测和更新两个步骤。

假设在 $k-1$ 时刻，我们已经获得了后验均值 $\boldsymbol{m}_{k-1|k-1}$ 和后验协方差 $\boldsymbol{P}_{k-1|k-1}$。

#### 1. 预测步骤

预测步骤的目标是计算先验均值 $\boldsymbol{m}_{k|k-1}$ 和先验协方差 $\boldsymbol{P}_{k|k-1}$。

a. **生成Sigma点**: 基于 $\boldsymbol{m}_{k-1|k-1}$ 和 $\boldsymbol{P}_{k-1|k-1}$，使用上一节描述的方法生成 $2n+1$ 个sigma点 $\mathcal{X}_{i, k-1|k-1}$。

b. **传播Sigma点**: 将每个sigma点代入非线性状态转移函数 $f$ 中，以获得传播后的点云：
$$
\mathcal{X}^*_{i, k|k-1} = f(\mathcal{X}_{i, k-1|k-1})
$$

c. **计算预测均值和协方差**: 利用权重 $W_i^{(m)}$ 和 $W_i^{(c)}$ 对传播后的点云进行加权平均和加权协方差计算，并加上过程噪声的协方差 $Q_{k-1}$：
$$
\boldsymbol{m}_{k|k-1} = \sum_{i=0}^{2n} W_i^{(m)} \mathcal{X}^*_{i, k|k-1}
$$
$$
\boldsymbol{P}_{k|k-1} = \sum_{i=0}^{2n} W_i^{(c)} (\mathcal{X}^*_{i, k|k-1} - \boldsymbol{m}_{k|k-1})(\mathcal{X}^*_{i, k|k-1} - \boldsymbol{m}_{k|k-1})^\top + \boldsymbol{Q}_{k-1}
$$
至此，我们得到了状态在 $k$ 时刻的先验估计。

#### 2. 更新步骤

更新步骤利用 $k$ 时刻的观测值 $\boldsymbol{y}_k$ 来修正先验估计，得到后验估计。这一步的核心是再次使用UT来处理非线性观测函数 $h$。

a. **传播Sigma点至观测空间**: 将预测步骤中生成的先验sigma点（注意，不是传播后的 $\mathcal{X}^*$）代入非线性观测函数 $h$：
$$
\mathcal{Y}_{i, k|k-1} = h(\mathcal{X}_{i, k|k-1})
$$
这些点 $\mathcal{Y}_{i, k|k-1}$ 构成了预测观测的分布近似。

b. **计算预测观测的均值和协方差**: 对这些观测空间的点云进行加权统计，得到预测观测均值 $\hat{\boldsymbol{y}}_k$ 和其协方差，然后加上观测噪声的协方差 $\boldsymbol{R}_k$ 得到**新息协方差（innovation covariance）** $\boldsymbol{S}_k$ [@problem_id:3429778]：
$$
\hat{\boldsymbol{y}}_k = \sum_{i=0}^{2n} W_i^{(m)} \mathcal{Y}_{i, k|k-1}
$$
$$
\boldsymbol{S}_k = \sum_{i=0}^{2n} W_i^{(c)} (\mathcal{Y}_{i, k|k-1} - \hat{\boldsymbol{y}}_k)(\mathcal{Y}_{i, k|k-1} - \hat{\boldsymbol{y}}_k)^\top + \boldsymbol{R}_k
$$

c. **计算互协方差（cross-covariance）**: 计算状态和观测之间的**互协方差矩阵** $\boldsymbol{P}_{xy,k}$，这在卡尔曼增益的计算中至关重要 [@problem_id:3429818]：
$$
\boldsymbol{P}_{xy,k} = \sum_{i=0}^{2n} W_i^{(c)} (\mathcal{X}_{i, k|k-1} - \boldsymbol{m}_{k|k-1})(\mathcal{Y}_{i, k|k-1} - \hat{\boldsymbol{y}}_k)^\top
$$

d. **计算卡尔曼增益**: 卡尔曼增益 $\boldsymbol{K}_k$ 的计算公式在形式上与标准KF类似，但其构成部分都是通过UT得到的 [@problem_id:3429836]：
$$
\boldsymbol{K}_k = \boldsymbol{P}_{xy,k} \boldsymbol{S}_k^{-1}
$$

e. **更新状态均值和协方差**: 最后，利用卡尔曼增益和实际观测与预测观测的差（即**新息** $\boldsymbol{y}_k - \hat{\boldsymbol{y}}_k$）来更新状态估计 [@problem_id:3429772]：
$$
\boldsymbol{m}_{k|k} = \boldsymbol{m}_{k|k-1} + \boldsymbol{K}_k (\boldsymbol{y}_k - \hat{\boldsymbol{y}}_k)
$$
$$
\boldsymbol{P}_{k|k} = \boldsymbol{P}_{k|k-1} - \boldsymbol{K}_k \boldsymbol{S}_k \boldsymbol{K}_k^\top
$$
这一对公式给出了 $k$ 时刻的后验均值 $\boldsymbol{m}_{k|k}$ 和后验协方差 $\boldsymbol{P}_{k|k}$，它们将作为下一轮递推的起点。

### 实践考量与数值稳定性

尽管上述算法在理论上是完备的，但在有限精度计算机上实现时，协方差的更新公式 $\boldsymbol{P}_{k|k} = \boldsymbol{P}_{k|k-1} - \boldsymbol{K}_k \boldsymbol{S}_k \boldsymbol{K}_k^\top$ 存在一个严重的数值问题。这个公式是一个减法运算，当观测信息非常精确时（例如观测噪声协方差 $\boldsymbol{R}_k$ 很小），被减去的项 $\boldsymbol{K}_k \boldsymbol{S}_k \boldsymbol{K}_k^\top$ 在数值上可能非常接近先验协方差 $\boldsymbol{P}_{k|k-1}$。这会导致“灾难性抵消”，即两个大数相减得到一个小数，从而损失大量有效数字。更严重的是，由于浮点误差的累积，计算出的后验协方差 $\boldsymbol{P}_{k|k}$ 可能会失去其必须具备的对称性和正定性，导致滤波器发散或在下一步的Cholesky分解中失败 [@problem_id:3429772]。

为了解决这个问题，**平方根无迹卡尔曼滤波器（Square-Root UKF, SR-UKF）**应运而生。其核心思想是直接对协方差矩阵的平方根因子（如Cholesky因子 $\boldsymbol{S}$）进行递推，而不是对协方差矩阵 $\boldsymbol{P}$ 本身。这样做有几个关键优势 [@problem_id:3429776]：

1.  **更好的数值条件**: 矩阵平方根的条件数是原始矩阵条件数的平方根。因此，对 $\boldsymbol{S}$ 的操作比对 $\boldsymbol{P}$ 的操作在数值上更稳定。
2.  **保证正定性**: 只要平方根因子 $\boldsymbol{S}$ 是非奇异的，重构的协方差 $\boldsymbol{P} = \boldsymbol{S}\boldsymbol{S}^\top$ 就天然是对称半正定的。平方根算法通过使用数值稳定的正交变换（如QR分解或Givens旋转）来更新因子，从而避免了协方差失去正定性的风险。
3.  **避免重复分解**: 在标准UKF中，每一步预测都需要对协方差矩阵进行Cholesky分解来生成sigma点，这是一项计算成本为 $\mathcal{O}(n^3)$ 的操作。SR-UKF直接传播因子，避免了这种重复分解。

即使在SR-UKF中，也可能出现一些微妙的数值问题，尤其是在使用某些参数组合（如 $\lambda  0$）导致中心协方差权重 $W_0^{(c)}$ 为负时。此时，协方差的更新会包含“降秩（downdate）”操作，这比增秩（update）操作更具数值挑战性。先进的SR-UKF实现会采用多种策略来确保鲁棒性 [@problem_id:3429779]：

- **选择稳健的参数**: 一种直接的方法是调整参数（如设置 $\kappa \ge 0$）以确保所有协方差权重 $W_i^{(c)}$ 均为非负，从而从根本上避免降秩操作 [@problem_id:3429779]。
- **使用高级矩阵分解**: 采用基于QR分解或U-D分解的更新方法，这些方法在处理降秩时比Cholesky分解更稳健。
- **Joseph形式的协方差更新**: 在更新步骤中，采用等价的、但数值上更稳定的Joseph形式协方差更新，该形式只涉及矩阵的加法，从而避免了灾难性抵消。
- **最小对角加载**: 在检测到数值问题（如因子即将变为奇异）时，向协方差矩阵中添加一个极小的对角矩阵 $\epsilon\boldsymbol{I}$（即协方差膨胀），以强制保持其正定性。

综上所述，无迹卡尔曼滤波器通过巧妙的确定性采样策略，在非线性估计问题中实现了对贝叶斯递推的高精度近似。虽然其基本形式简洁优雅，但要构建一个在实际应用中真正稳健可靠的滤波器，还必须深入理解并妥善处理与有限精度计算相关的数值稳定性问题。