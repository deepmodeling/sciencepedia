## 引言
在现代控制理论与信号处理中，状态估计是一个核心问题，而[卡尔曼滤波器](@entry_id:145240)无疑是处理[线性高斯系统](@entry_id:200183)的王者。然而，从[机器人导航](@entry_id:263774)到[化学反应](@entry_id:146973)过程，现实世界充满了复杂的[非线性](@entry_id:637147)动态。当系统模型不再是简单的线性方程时，标准卡尔曼滤波器的最优性便不复存在，我们迫切需要一种更强大的工具来应对这一挑战。扩展卡尔曼滤波器（EKF）正是为解决这一问题而生，它通过一种巧妙的[局部线性化](@entry_id:169489)思想，成功地将卡尔曼滤波的强大框架延伸至[非线性](@entry_id:637147)领域。

本文将作为一份全面的指南，系统地引导您掌握EKF的理论精髓与实践应用。在“原理与机制”一章中，我们将深入探讨EKF的数学基础，从[雅可比矩阵](@entry_id:264467)的推导到完整的预测-更新算法周期。接着，在“应用与跨学科联系”一章中，我们将穿越不同学科，见证EKF如何在目标跟踪、SLAM、乃至化学工程等领域大放异彩。最后，“动手实践”部分将通过具体的编程练习，巩固您对理论知识的理解，并提升解决实际问题的能力。让我们一同开启探索EKF的旅程，揭开其处理[非线性](@entry_id:637147)世界之谜的奥秘。

## 原理与机制
### 从线性到[非线性](@entry_id:637147)：扩展[卡尔曼滤波器](@entry_id:145240)的必要性

标准的卡尔曼滤波器 (Kalman Filter, KF) 在处理[线性系统](@entry_id:147850)时，是[状态估计](@entry_id:169668)的最优解。其模型假设系统动态和测量过程可以用[线性方程](@entry_id:151487)来描述：
$$
\mathbf{x}_k = F_k \mathbf{x}_{k-1} + B_k \mathbf{u}_{k-1} + \mathbf{w}_{k-1}
$$
$$
\mathbf{z}_k = H_k \mathbf{x}_k + \mathbf{v}_k
$$
其中，[状态转移矩阵](@entry_id:269075) $F_k$ 和观测矩阵 $H_k$ 捕捉了系统的线性特性。然而，现实世界中的许多系统本质上是[非线性](@entry_id:637147)的。当系统的动态或测量过程不能用简单的线性方程来描述时，标准卡尔曼滤波器的核心假设就被打破了，其最优性也就不复存在。

考虑一个一般的非线性系统，其状态演化和测量过程可以表示为：
$$
\mathbf{x}_k = f(\mathbf{x}_{k-1}, \mathbf{u}_{k-1}) + \mathbf{w}_{k-1}
$$
$$
\mathbf{z}_k = h(\mathbf{x}_k) + \mathbf{v}_k
$$
这里的 $f(\cdot)$ 和 $h(\cdot)$ 是[非线性](@entry_id:637147)函数。例如，一个简单的[振荡](@entry_id:267781)部件的角度位置可能会遵循一个[非线性](@entry_id:637147)的动态规律，如 $x_{k+1} = \cos(x_k) + w_k$ [@problem_id:1574768]。这里的 $\cos(\cdot)$ 函数显然不是线性的，因此无法用一个恒定的[状态转移矩阵](@entry_id:269075) $F$ 来表示。同样，在参数估计问题中，非[线性关系](@entry_id:267880)也常常出现。例如，在估计一个物体的温度 $T_k$ 和其未知的冷却系数 $\lambda_k$ 时，根据[牛顿冷却定律](@entry_id:142531)，温度的[演化方程](@entry_id:268137)为 $T_{k+1} = T_{env} + (T_k - T_{env}) \exp(-\lambda_k \Delta t)$。这个模型中，状态变量 $T_k$ 和 $\lambda_k$ 之间存在乘积和指数关系，导致状态[转移函数](@entry_id:273897) $f(\cdot)$ 成为[非线性](@entry_id:637147)函数 [@problem_id:1574743]。

[非线性](@entry_id:637147)不仅可以存在于过程模型 $f(\cdot)$ 中，也可以存在于测量模型 $h(\cdot)$ 中。一个常见的例子是使用雷达测量目标距离。如果状态是目标的[笛卡尔坐标](@entry_id:167698) $(p_x, p_y)$，那么雷达测量到的距离是 $z_k = \sqrt{p_x^2 + p_y^2}$，这是一个[非线性](@entry_id:637147)函数。另一个例子是传感器的响应可能是[非线性](@entry_id:637147)的，比如一个污染传感器的读数可能与污染物浓度的对数成正比，即 $z_k = \ln(x_k^B) + v_k$ [@problem_id:1574760]。在这些情况下，由于测量模型 $h(\cdot)$ 是[非线性](@entry_id:637147)的，标准卡尔曼滤波器同样不适用。

面对这些[非线性系统](@entry_id:168347)，我们需要一种新的方法。**扩展卡尔曼滤波器 (Extended Kalman Filter, EKF)** 的核心思想就是：**[局部线性化](@entry_id:169489) (local linearization)**。它不是试图找到一个全局的线性模型，而是在每个时间步，围绕当前的最佳[状态估计](@entry_id:169668)值，将[非线性](@entry_id:637147)[函数近似](@entry_id:141329)为一个线性函数。通过这种方式，EKF 巧妙地将[非线性](@entry_id:637147)问题转化为一系列可以在局部应用标准卡尔曼滤波器框架的线性问题。

### 线性化的数学工具：[雅可比矩阵](@entry_id:264467)

EKF 实现[局部线性化](@entry_id:169489)的数学基础是泰勒级数展开。对于一个[非线性](@entry_id:637147)向量函数 $\mathbf{f}(\mathbf{x})$，我们可以在一个点 $\mathbf{a}$ 附近，用其一阶泰勒展开来近似它：
$$
\mathbf{f}(\mathbf{x}) \approx \mathbf{f}(\mathbf{a}) + \frac{\partial \mathbf{f}}{\partial \mathbf{x}}\bigg|_{\mathbf{x}=\mathbf{a}} (\mathbf{x}-\mathbf{a})
$$
这个展开式中的偏导数矩阵 $\frac{\partial \mathbf{f}}{\partial \mathbf{x}}$ 就是**雅可比矩阵 (Jacobian matrix)**。它是一个包含了函数所有一阶偏导数的矩阵，描述了函数在某一点的[最佳线性近似](@entry_id:164642)。对于状态[转移函数](@entry_id:273897) $\mathbf{f}(\mathbf{x})$，其[雅可比矩阵](@entry_id:264467)通常记为 $F$；对于测量函数 $\mathbf{h}(\mathbf{x})$，其雅可比矩阵记为 $H$。

让我们通过几个例子来具体了解如何计算雅可比矩阵。

**状态转移雅可比矩阵 $F_k$**

假设一个系统的状态演化由以下非线性方程描述 [@problem_id:1574740]：
$$
\mathbf{x}_{k+1} = \mathbf{f}(\mathbf{x}_k) = \begin{pmatrix} x_{1,k} + \Delta t \cdot x_{2,k} \\ x_{2,k} + \Delta t \cdot (\alpha \cos(x_{1,k}) - \beta x_{2,k}^2) \end{pmatrix}
$$
雅可比矩阵 $F_k$ 是 $\mathbf{f}$ 关于状态 $\mathbf{x} = [x_1, x_2]^T$ 的[偏导数](@entry_id:146280)矩阵：
$$
F_k = \frac{\partial \mathbf{f}}{\partial \mathbf{x}} = \begin{pmatrix} \frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} \\ \frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2} \end{pmatrix} = \begin{pmatrix} 1 & \Delta t \\ -\alpha \Delta t \sin(x_1) & 1 - 2\beta \Delta t x_2 \end{pmatrix}
$$
关键在于，这个[雅可比矩阵](@entry_id:264467) $F_k$ 的值取决于状态 $\mathbf{x}$。在 EKF 中，我们在每一步都用当前的[状态估计](@entry_id:169668)值 $\hat{\mathbf{x}}_{k|k}$ 来计算它，从而得到一个随时间变化的、适应性的[线性模型](@entry_id:178302)。

**测量[雅可比矩阵](@entry_id:264467) $H_k$**

现在考虑一个雷达跟踪问题，状态为 $\mathbf{x}_k = [p_x, p_y, v_x, v_y]^T$，测量的是距离 $z_k = h(\mathbf{x}_k) = \sqrt{p_x^2 + p_y^2}$ [@problem_id:1574769]。测量雅可比矩阵 $H_k$ 是 $h$ 关于状态 $\mathbf{x}_k$ 的梯度：
$$
H_k = \frac{\partial h}{\partial \mathbf{x}_k} = \begin{pmatrix} \frac{\partial h}{\partial p_x} & \frac{\partial h}{\partial p_y} & \frac{\partial h}{\partial v_x} & \frac{\partial h}{\partial v_y} \end{pmatrix}
$$
计算各个偏导数，我们得到：
$$
H_k = \begin{pmatrix} \frac{p_x}{\sqrt{p_x^2 + p_y^2}} & \frac{p_y}{\sqrt{p_x^2 + p_y^2}} & 0 & 0 \end{pmatrix}
$$
同样，这个矩阵的值也依赖于当前的状态（具体来说是位置 $p_x$ 和 $p_y$）。与标准卡尔曼滤波器中的固定或预先知道的 $F_k$ 和 $H_k$ 矩阵不同，EKF中的雅可比矩阵是在线计算的，这赋予了它处理[非线性系统](@entry_id:168347)的能力。

### 扩展[卡尔曼滤波器](@entry_id:145240)算法周期

与标准卡尔曼滤波器一样，EKF 算法也包含两个基本步骤：**预测 (Prediction)** 和 **更新 (Update)**。

#### 预测（时间更新）

预测步骤利用过程模型将状态估计和其不确定性（协[方差](@entry_id:200758)）从上一时刻 $k-1$ 投射到当前时刻 $k$。

**状态预测**

一个非常关键且容易混淆的点是，EKF 使用**原始的[非线性](@entry_id:637147)函数 $f(\cdot)$** 来传播[状态估计](@entry_id:169668)本身，而不是使用它的线性化近似。这样做能保留[非线性模型](@entry_id:276864)的大部分信息，得到更准确的状态预测值。[雅可比矩阵](@entry_id:264467)的作用是传播不确定性，而非状态均值 [@problem_id:1574749]。
$$
\hat{\mathbf{x}}_{k|k-1} = f(\hat{\mathbf{x}}_{k-1|k-1}, \mathbf{u}_{k-1})
$$
例如，对于一个在二维平面上移动的机器人，其[运动学](@entry_id:173318)模型为[非线性](@entry_id:637147)的 [@problem_id:1574763]：
$$
\begin{cases}
x_k = x_{k-1} + v_{k-1} \cos(\theta_{k-1}) \Delta t \\
y_k = y_{k-1} + v_{k-1} \sin(\theta_{k-1}) \Delta t \\
\theta_k = \theta_{k-1} + \omega_{k-1} \Delta t
\end{cases}
$$
给定上一时刻的估计值 $\hat{\mathbf{x}}_{k-1|k-1} = [\hat{x}_{k-1|k-1}, \hat{y}_{k-1|k-1}, \hat{\theta}_{k-1|k-1}]^T$，预测的状态 $\hat{\mathbf{x}}_{k|k-1}$ 就是直接将这些值代入上述[非线性方程](@entry_id:145852)得到的结果。

**协[方差](@entry_id:200758)预测**

协[方差](@entry_id:200758)的传播则依赖于线性化。状态转移雅可比矩阵 $F_k$ 描述了上一时刻状态的微小扰动如何通过系统动态传播到当前时刻，从而决定了先验不确定性如何影响预测的不确定性 [@problem_id:2706002]。预测协[方差](@entry_id:200758)的方程为：
$$
P_{k|k-1} = F_k P_{k-1|k-1} F_k^T + Q_{k-1}
$$
这里的 $F_k$ 是在上一时刻的后验估计值 $\hat{\mathbf{x}}_{k-1|k-1}$ 处计算的雅可比矩阵：
$$
F_k = \frac{\partial f}{\partial \mathbf{x}} \bigg|_{\mathbf{x}=\hat{\mathbf{x}}_{k-1|k-1}, \mathbf{u}=\mathbf{u}_{k-1}}
$$
而 $Q_{k-1}$ 是**[过程噪声协方差](@entry_id:186358)矩阵**。它在方程中的作用至关重要：它量化了由于过程模型本身的不精确性和不可预测性（例如，未建模的力、随机扰动）而给状态估计增加的不确定性。作为一个[半正定矩阵](@entry_id:155134)，$Q_{k-1}$ 的加入会“膨胀”预测的协[方差](@entry_id:200758)，反映了我们对模型预测随时间推移而信心下降的现实 [@problem_id:1574766]。

#### 更新（测量更新）

更新步骤利用当前时刻 $k$ 的实际测量值 $\mathbf{z}_k$ 来修正预测步骤得到的[先验估计](@entry_id:186098) $\hat{\mathbf{x}}_{k|k-1}$。

**测量预测与新息**

首先，我们使用**原始的[非线性](@entry_id:637147)测量函数 $h(\cdot)$** 来计算预测的测量值：
$$
\hat{\mathbf{z}}_k = h(\hat{\mathbf{x}}_{k|k-1})
$$
然后，计算**新息 (innovation)** 或测量残差，即实际测量值与预测测量值之差：
$$
\mathbf{y}_k = \mathbf{z}_k - \hat{\mathbf{z}}_k
$$

**[雅可比矩阵](@entry_id:264467)与[卡尔曼增益](@entry_id:145800)**

接下来，我们需要计算测量[雅可比矩阵](@entry_id:264467) $H_k$。它描述了状态在[先验估计](@entry_id:186098)附近的微小扰动如何影响测量值，从而决定了新息如何在状态修正中发挥作用 [@problem_id:2706002]。需要特别注意的是，$H_k$ 是在**当前时刻的先验（预测）估计值 $\hat{\mathbf{x}}_{k|k-1}$** 处进行线性化的：
$$
H_k = \frac{\partial h}{\partial \mathbf{x}} \bigg|_{\mathbf{x}=\hat{\mathbf{x}}_{k|k-1}}
$$
在得到 $H_k$ 后，就可以计算新息协[方差](@entry_id:200758) $S_k$ 和[卡尔曼增益](@entry_id:145800) $K_k$：
$$
S_k = H_k P_{k|k-1} H_k^T + R_k
$$
$$
K_k = P_{k|k-1} H_k^T S_k^{-1}
$$
其中，$R_k$ 是测量噪声[协方差矩阵](@entry_id:139155)，代表了传感器测量的不确定性。

**状态与协[方差](@entry_id:200758)更新**

最后，利用[卡尔曼增益](@entry_id:145800) $K_k$ 和新息 $\mathbf{y}_k$ 来修正[先验估计](@entry_id:186098)，得到当前时刻的后验（最终）估计：
$$
\hat{\mathbf{x}}_{k|k} = \hat{\mathbf{x}}_{k|k-1} + K_k \mathbf{y}_k
$$
$$
P_{k|k} = (I - K_k H_k) P_{k|k-1}
$$
至此，一个完整的 EKF 算法周期完成。得到的 $\hat{\mathbf{x}}_{k|k}$ 和 $P_{k|k}$ 将作为下个时间步 $k+1$ 的输入。

#### 完整计算示例

让我们通过一个机器人定位的例子来走一遍完整的预测-更新流程 [@problem_id:1574791]。

- **系统模型**：一个机器人在二维平面上[随机游走](@entry_id:142620)。过程模型是线性的 $x_k = x_{k-1} + w_{k-1}$，所以 $F_k=I$。[过程噪声](@entry_id:270644) $Q = \text{diag}(0.1, 0.1)$。
- **测量模型**：一个位于原点的传感器测量机器人距离，$z_k = \sqrt{p_x^2 + p_y^2} + v_k$。[测量噪声](@entry_id:275238)[方差](@entry_id:200758) $R=0.01$。
- **初始状态** ($k=0$)：$\hat{x}_{0|0} = \begin{pmatrix} 10.0 \\ 0.0 \end{pmatrix}$, $P_{0|0} = \text{diag}(1.0, 1.0)$。
- **新测量** ($k=1$)：$z_1 = 5.0$。

**1. 预测步骤**
- 状态预测：$\hat{x}_{1|0} = F_0 \hat{x}_{0|0} = I \cdot \begin{pmatrix} 10 \\ 0 \end{pmatrix} = \begin{pmatrix} 10 \\ 0 \end{pmatrix}$。
- 协[方差](@entry_id:200758)预测：$P_{1|0} = F_0 P_{0|0} F_0^T + Q_0 = I \cdot \text{diag}(1,1) \cdot I^T + \text{diag}(0.1, 0.1) = \text{diag}(1.1, 1.1)$。

**2. 更新步骤**
- 测量雅可比计算：在 $\hat{x}_{1|0} = \begin{pmatrix} 10 \\ 0 \end{pmatrix}$ 处线性化 $h(x) = \sqrt{p_x^2 + p_y^2}$。
  $H_1 = \begin{pmatrix} \frac{p_x}{\sqrt{p_x^2+p_y^2}} & \frac{p_y}{\sqrt{p_x^2+p_y^2}} \end{pmatrix}_{\hat{x}_{1|0}} = \begin{pmatrix} \frac{10}{\sqrt{10^2+0^2}} & \frac{0}{\sqrt{10^2+0^2}} \end{pmatrix} = \begin{pmatrix} 1 & 0 \end{pmatrix}$。
- 新息计算：
  预测测量值 $\hat{z}_1 = h(\hat{x}_{1|0}) = \sqrt{10^2+0^2} = 10$。
  新息 $y_1 = z_1 - \hat{z}_1 = 5 - 10 = -5$。
- [卡尔曼增益](@entry_id:145800)计算：
  新息协[方差](@entry_id:200758) $S_1 = H_1 P_{1|0} H_1^T + R = \begin{pmatrix} 1 & 0 \end{pmatrix} \begin{pmatrix} 1.1 & 0 \\ 0 & 1.1 \end{pmatrix} \begin{pmatrix} 1 \\ 0 \end{pmatrix} + 0.01 = 1.1 + 0.01 = 1.11$。
  [卡尔曼增益](@entry_id:145800) $K_1 = P_{1|0} H_1^T S_1^{-1} = \begin{pmatrix} 1.1 & 0 \\ 0 & 1.1 \end{pmatrix} \begin{pmatrix} 1 \\ 0 \end{pmatrix} (1.11)^{-1} = \begin{pmatrix} 1.1 \\ 0 \end{pmatrix} \frac{1}{1.11} \approx \begin{pmatrix} 0.991 \\ 0 \end{pmatrix}$。
- 状态与协[方差](@entry_id:200758)更新：
  更新后状态 $\hat{x}_{1|1} = \hat{x}_{1|0} + K_1 y_1 = \begin{pmatrix} 10 \\ 0 \end{pmatrix} + \begin{pmatrix} 0.991 \\ 0 \end{pmatrix}(-5) = \begin{pmatrix} 10 - 4.955 \\ 0 \end{pmatrix} = \begin{pmatrix} 5.045 \\ 0 \end{pmatrix}$。
  (这里我们使用更精确的分数计算结果 $\hat{x}_{1|1} = \begin{pmatrix} \frac{560}{111} \\ 0 \end{pmatrix} \approx \begin{pmatrix} 5.045 \\ 0.0 \end{pmatrix}$)
  更新后协[方差](@entry_id:200758) $P_{1|1} = (I - K_1 H_1) P_{1|0}$。

通过这个例子，我们看到EKF如何将预测和测量信息结合起来，即使在非[线性测量模型](@entry_id:751316)下也能生成一个修正后的状态估计。

### EKF的局限与陷阱

尽管 EKF 功能强大且应用广泛，但它并非万能药。其基于[局部线性化](@entry_id:169489)的近似方法带来了一些固有的局限性，可能导致滤波器性能下降甚至发散。

#### 线性化带来的次优性

EKF 对于[非线性系统](@entry_id:168347)而言是一个**次优 (suboptimal)** 滤波器。其根本原因在于，当一个[高斯分布](@entry_id:154414)（由均值和协[方差](@entry_id:200758)完全描述）通过一个[非线性](@entry_id:637147)函数时，其结果通常不再是[高斯分布](@entry_id:154414)。EKF 强制将这个非[高斯分布](@entry_id:154414)的结果用一个新的[高斯分布](@entry_id:154414)来近似，这个过程中会丢失信息，并引入误差。

**1. 引入估计偏差 (Bias)**

EKF 的一个主要问题是它可能引入系统性偏差。这是因为对于一个[非线性](@entry_id:637147)函数 $h(x)$，通常 $E[h(x)] \neq h(E[x])$ (这与[詹森不等式](@entry_id:144269)有关)。EKF 使用 $h(\hat{x})$ 作为对 $E[h(x)]$ 的近似，当函数 $h(x)$ 曲率较大且状态不确定性 $P$ 较大时，这种近似会产生显著偏差。

考虑一个简单的二次测量模型 $y_k = x_k^2 + v_k$ [@problem_id:1574746]。EKF 的预测测量是 $\hat{y}_{k|k-1} = h(\hat{x}_{k|k-1}) = \hat{x}_{k|k-1}^2$。然而，真实的期望测量值是 $E[y_k] = E[x_k^2] + E[v_k]$。对于服从[高斯分布](@entry_id:154414)的 $x_k \sim \mathcal{N}(\hat{x}_{k|k-1}, P_{k|k-1})$，我们有 $E[x_k^2] = (\hat{x}_{k|k-1})^2 + P_{k|k-1}$。因此，EKF 预测的系统性偏差为：
$$
B = E[y_k] - \hat{y}_{k|k-1} = ((\hat{x}_{k|k-1})^2 + P_{k|k-1}) - \hat{x}_{k|k-1}^2 = P_{k|k-1}
$$
这个结果清晰地表明，偏差的大小直接等于状态的先验[方差](@entry_id:200758)。不确定性越大，EKF 引入的偏差就越大。

**2. 不准确的[协方差传播](@entry_id:747989)**

同样，通过雅可比矩阵传播协[方差](@entry_id:200758)也是一种近似。当[非线性](@entry_id:637147)程度很高时，这种线性化近似可能严重低估或高估真实的不确定性。

考虑一个二次动态模型 $x_k = \alpha x_{k-1}^2 + w_{k-1}$，假设 $x_{k-1} \sim \mathcal{N}(0, \sigma_0^2)$ [@problem_id:1574784]。EKF 在 $\hat{x}_{k-1|k-1}=0$ 处进行线性化，得到的雅可比矩阵 $F_{k-1} = 2\alpha x | _{x=0} = 0$。因此，EKF 预测的[方差](@entry_id:200758)为 $P_{k|k-1}^{\text{EKF}} = F_{k-1} P_{k-1|k-1} F_{k-1}^T + Q = 0 \cdot \sigma_0^2 \cdot 0 + Q = Q$。

然而，真实的[方差](@entry_id:200758)是 $\text{Var}(x_k) = \text{Var}(\alpha x_{k-1}^2 + w_{k-1}) = \alpha^2 \text{Var}(x_{k-1}^2) + \text{Var}(w_{k-1})$。对于均值为零的高斯分布，$E[x^2]=\sigma^2$, $E[x^4]=3\sigma^4$，所以 $\text{Var}(x^2) = E[x^4] - (E[x^2])^2 = 2\sigma^4$。因此，真实[方差](@entry_id:200758)为 $P_{k|k-1}^{\text{True}} = 2\alpha^2 \sigma_0^4 + Q$。

EKF 预测[方差](@entry_id:200758)与真实[方差](@entry_id:200758)的比值为：
$$
\frac{P_{k|k-1}^{\text{True}}}{P_{k|k-1}^{\text{EKF}}} = \frac{2 \alpha^2 \sigma_0^4 + Q}{Q} = 1 + \frac{2 \alpha^2 \sigma_0^4}{Q}
$$
这个比值清楚地表明，EKF 在这种情况下严重低估了真实的不确定性，尤其是当先验不确定性 $\sigma_0$ 很大或[非线性](@entry_id:637147)项系数 $\alpha$ 很大时。

#### [滤波器发散](@entry_id:749356)问题

EKF 的另一个严重问题是**发散 (divergence)**，即估计误差无限增长。这通常发生在：
1.  **强[非线性](@entry_id:637147)**：当系统动态或测量模型[非线性](@entry_id:637147)程度非常高时，一阶[泰勒展开](@entry_id:145057)的近似效果很差。
2.  **糟糕的初始估计**：如果初始状态估计 $\hat{\mathbf{x}}_{0|0}$ 离真实状态太远，那么线性化将在一个完全不具[代表性](@entry_id:204613)的点上进行。这会导致错误的[雅可比矩阵](@entry_id:264467)，进而产生错误的预测和更新，使得估计离真实值越来越远 [@problem_id:1574791]。
3.  **不一致的[噪声模型](@entry_id:752540)**：如果过程噪声 $Q$ 和[测量噪声](@entry_id:275238) $R$ 的设置与实际情况严重不符（例如，设置得过小），滤波器会过于相信自己的模型和测量，无法容忍偏差，最终导致发散。

### 原理总结

本章深入探讨了扩展卡尔曼滤波器的核心原理与机制。关键要点可以总结如下：

-   EKF 是标准卡尔曼滤波器在非线性系统上的扩展，其核心思想是在每个时间步对[非线性系统](@entry_id:168347)进行**[局部线性化](@entry_id:169489)**。
-   线性化的数学工具是**[雅可比矩阵](@entry_id:264467)**，它代表了[非线性](@entry_id:637147)函数在某一点的[最佳线性近似](@entry_id:164642)。EKF 分别为过程模型和测量模型计算[雅可比矩阵](@entry_id:264467) $F_k$ 和 $H_k$。
-   EKF 的算法周期依然是**预测-更新**。一个关键的区别在于：状态（均值）的传播使用**原始的[非线性](@entry_id:637147)函数**，而不确定性（协[方差](@entry_id:200758)）的传播则使用**线性化的[雅可比矩阵](@entry_id:264467)**。
-   EKF 是一种**次优滤波器**。线性化近似会引入偏差和不准确的[协方差估计](@entry_id:145514)，特别是在强[非线性](@entry_id:637147)或高不确定性的情况下。
-   在实际应用中，必须警惕 EKF 的**发散**风险，这通常与强[非线性](@entry_id:637147)、糟糕的初始值或不恰当的噪声参数有关。

尽管存在这些局限，EKF 因其相对简单的概念和计算效率，在导航、机器人、经济学等众多领域仍然是一个非常流行和实用的工具。理解其内在的近似性质和潜在的陷阱，是成功应用 EKF 的关键。正是为了克服 EKF 的这些局限，研究人员发展了更先进的[非线性滤波](@entry_id:201008)技术，如[无迹卡尔曼滤波器 (UKF)](@entry_id:191842) 和[粒子滤波器](@entry_id:181468) (PF)，我们将在后续章节中进行探讨。