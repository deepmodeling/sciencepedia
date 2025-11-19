## 引言
在科学与工程的众多领域中，我们所关心的量往往不是基础的测量值本身，而是由多个随机因素共同决定的复杂函数。例如，系统的总误差是多个独立噪声源的叠加，一项投资组合的回报是各资产收益的加权和，一个物理系统的能量是其粒子速度的函数。理解这些派生量的统计特性，对于预测系统行为、评估风险和制定决策至关重要。然而，从已知[随机变量](@entry_id:195330)的联合分布推导出其函数的新[分布](@entry_id:182848)，需要一套系统而严谨的数学工具，这正是本章旨在解决的核心问题。

本文将带领读者系统地学习处理多[随机变量变换](@entry_id:164667)的强大技术。在“原理与机制”一章中，我们将从基础出发，详细介绍离散和连续情况下的核心方法，包括卷积、分布函数法以及强大的[雅可比](@entry_id:264467)变换。随后的“应用与跨学科联系”一章将展示这些理论工具如何在工程、物理、生物及计算科学等不同领域中解决实际问题，将抽象概念与具体实践联系起来。最后，“动手实践”部分将提供精选的练习，帮助您巩固所学知识，并将其应用于解决具体问题。通过本章的学习，您将掌握量化和驾驭复杂随机现象的核心能力。

## 原理与机制

在概率论的研究中，我们常常需要分析由已知[随机变量](@entry_id:195330)通过[函数变换](@entry_id:141095)得到的新[随机变量](@entry_id:195330)的统计特性。例如，一个系统的总噪声可能是由多个独立噪声源叠加而成；一个物体的动能由其质量和速度决定；或者在金融模型中，一项资产的未来回报可能是多个随机因子的复杂函数。本章旨在系统性地阐述处理多[随机变量](@entry_id:195330)函数（或称变换）的基本原理和核心方法，帮助读者掌握从原始变量的[联合分布](@entry_id:263960)推导出新变量[分布](@entry_id:182848)的严谨技术。

我们将从[离散随机变量](@entry_id:163471)的[简单函数](@entry_id:137521)开始，逐步过渡到[连续随机变量](@entry_id:166541)的复杂变换，并介绍一系列强大的分析工具，包括卷积、分布函数法以及[雅可比](@entry_id:264467)变换法。

### 离散型[随机变量函数的分布](@entry_id:748601)

处理[离散随机变量的函数](@entry_id:184970)，其核心思想是识别所有可能导致新[随机变量](@entry_id:195330)取特定值的原始变量组合，并将这些[互斥事件](@entry_id:265118)的概率相加。

一个基本且重要的问题是两个[独立随机变量](@entry_id:273896)之和的[分布](@entry_id:182848)。假设 $X$ 和 $Y$ 是两个独立的[离散随机变量](@entry_id:163471)，我们想求其和 $Z = X+Y$ 的[概率质量函数](@entry_id:265484) (PMF)。事件 $\{Z=z\}$ 可以分解为一系列[互斥事件](@entry_id:265118)的并集：$\{X=x_i, Y=z-x_i\}$，其中 $x_i$ 是 $X$ 的所有可能取值。由于 $X$ 和 $Y$ 相互独立，我们可以得到 $Z$ 的 PMF，即**卷积公式**：

$P(Z=z) = \sum_{i} P(X=x_i, Y=z-x_i) = \sum_{i} P(X=x_i)P(Y=z-x_i)$

这个求和遍历所有可能的 $x_i$ 值。

一个经典的例子是两个独立的泊松分布[随机变量](@entry_id:195330)之和。[泊松分布](@entry_id:147769)常用于模拟在固定时间间隔或空间区域内发生事件的次数。考虑一个数据中心的邮件服务器，其在上午接收的邮件数 $X$ 服从参数为 $\lambda_M$ 的[泊松分布](@entry_id:147769)，下午接收的邮件数 $Y$ 服从参数为 $\lambda_A$ 的[泊松分布](@entry_id:147769)，且 $X$ 和 $Y$ [相互独立](@entry_id:273670) [@problem_id:1408044]。一整天接收的总邮件数 $Z = X+Y$ 的[分布](@entry_id:182848)是什么？

根据卷积公式，对于任意非负整数 $n$，总邮件数为 $n$ 的概率为：
$P(Z=n) = \sum_{k=0}^{n} P(X=k, Y=n-k)$
由于独立性，$P(X=k, Y=n-k) = P(X=k)P(Y=n-k)$。代入泊松分布的 PMF $P(K=k) = \frac{\lambda^k \exp(-\lambda)}{k!}$，我们得到：
$P(Z=n) = \sum_{k=0}^{n} \frac{\lambda_M^k \exp(-\lambda_M)}{k!} \frac{\lambda_A^{n-k} \exp(-\lambda_A)}{(n-k)!}$
$P(Z=n) = \exp(-(\lambda_M + \lambda_A)) \sum_{k=0}^{n} \frac{\lambda_M^k \lambda_A^{n-k}}{k!(n-k)!}$

通过在求和项中乘以并除以 $n!$，我们可以利用[二项式定理](@entry_id:276665)：
$P(Z=n) = \frac{\exp(-(\lambda_M + \lambda_A))}{n!} \sum_{k=0}^{n} \frac{n!}{k!(n-k)!} \lambda_M^k \lambda_A^{n-k} = \frac{\exp(-(\lambda_M + \lambda_A))}{n!} (\lambda_M + \lambda_A)^n$

这正是参数为 $\lambda_M + \lambda_A$ 的泊松分布的 PMF。这个重要的结论表明，**独立泊松[随机变量](@entry_id:195330)的和仍然是泊松[随机变量](@entry_id:195330)，其参数为各参数之和**。

更有趣的是，我们可以反过来提出一个条件概率问题 [@problem_id:1408044]。如果已知一天总共收到了 $n$ 封邮件，那么其中 $k$ 封是在上午收到的概率是多少？即求 $P(X=k | X+Y=n)$。根据[条件概率](@entry_id:151013)的定义：
$P(X=k | X+Y=n) = \frac{P(X=k, X+Y=n)}{P(X+Y=n)} = \frac{P(X=k, Y=n-k)}{P(X+Y=n)}$
将我们之前计算得到的分子和分母代入，经过化简，可以得到一个出人意料而又优美的结果：
$P(X=k | X+Y=n) = \binom{n}{k} \left(\frac{\lambda_M}{\lambda_M + \lambda_A}\right)^k \left(\frac{\lambda_A}{\lambda_M + \lambda_A}\right)^{n-k}$
这正是二项分布 $B(n, p)$ 的 PMF，其中成功概率 $p = \frac{\lambda_M}{\lambda_M + \lambda_A}$。这个结果直观地解释为：已知总共有 $n$ 个事件发生，每个事件独立地以概率 $p$ “属于”上午，或以概率 $1-p$ “属于”下午。

### 连续型[随机变量函数的分布](@entry_id:748601)：[分布函数](@entry_id:145626)法

对于连续型[随机变量](@entry_id:195330)，我们通常通过求其[累积分布函数 (CDF)](@entry_id:264700)，然后求导得到其[概率密度函数](@entry_id:140610) (PDF)。对于一个变换后的变量 $Z=g(X,Y)$，其CDF为 $F_Z(z) = P(Z \le z) = P(g(X,Y) \le z)$。计算这个概率需要对 $(X,Y)$ 的[联合密度函数](@entry_id:263624)在满足 $g(x,y) \le z$ 的区域上进行积分。

[分布函数](@entry_id:145626)法在处理[随机变量](@entry_id:195330)的最小值或最大值时尤其有效。考虑一个由两个独立部件组成的系统，其寿命为两个部件寿命中较短的那个。这种“[串联](@entry_id:141009)系统”的寿命是 $T = \min(T_A, T_B)$。

假设在一个卫星动力系统的仿真测试中，两个独立控制器 A 和 B 的寿命 $T_A$ 和 $T_B$ 分别服从参数为 $1/\alpha$ 和 $1/\beta$ 的指数分布 [@problem_id:1407979]。系统整体的寿命 $T$ 是 $T_A$ 和 $T_B$ 中的较小值。为了求 $T$ 的 PDF，我们先求其生存函数 $S_T(t) = P(T > t)$，这比直接求 CDF 更为方便。
$P(T > t) = P(\min(T_A, T_B) > t)$

事件 $\{\min(T_A, T_B) > t\}$ 等价于事件 $\{T_A > t \text{ and } T_B > t\}$。由于 $T_A$ 和 $T_B$ [相互独立](@entry_id:273670)，我们有：
$P(T > t) = P(T_A > t) P(T_B > t)$

对于一个参数为 $\lambda$ 的[指数分布](@entry_id:273894)[随机变量](@entry_id:195330)，其生存函数为 $P(\text{lifetime} > t) = \exp(-\lambda t)$。因此，$P(T_A > t) = \exp(-(1/\alpha)t)$，$P(T_B > t) = \exp(-(1/\beta)t)$。代入上式，我们得到：
$P(T > t) = \exp(-(1/\alpha)t) \exp(-(1/\beta)t) = \exp\left(-\left(\frac{1}{\alpha} + \frac{1}{\beta}\right)t\right)$

这表明 $T$ 的生存函数形式与[指数分布](@entry_id:273894)完全相同。因此，$T$ 也服从[指数分布](@entry_id:273894)，其参数为两个原始[分布](@entry_id:182848)的参数之和：$\lambda_T = \frac{1}{\alpha} + \frac{1}{\beta}$。$T$ 的 CDF 为 $F_T(t) = 1 - P(T > t) = 1 - \exp(-\lambda_T t)$，其 PDF 为对 CDF 求导：
$f_T(t) = \lambda_T \exp(-\lambda_T t) = \left(\frac{1}{\alpha} + \frac{1}{\beta}\right) \exp\left(-\left(\frac{1}{\alpha} + \frac{1}{\beta}\right)t\right), \quad \text{for } t > 0$

这个结果揭示了[指数分布](@entry_id:273894)的一个重要特性：**独立指数[随机变量](@entry_id:195330)的最小值仍然服从指数分布，其[失效率](@entry_id:266388)（参数 $\lambda$）是各分量失效率之和**。

### 特殊变换：和、差与线性组合

对于[连续随机变量](@entry_id:166541)的和，与离散情况类似，我们也可以使用卷积公式，只不过求和变成了积分：
$f_{X+Y}(z) = \int_{-\infty}^{\infty} f_{X,Y}(x, z-x) \,dx$
如果 $X$ 和 $Y$ 相互独立，则 $f_{X,Y}(x,y) = f_X(x)f_Y(y)$，公式简化为：
$f_{X+Y}(z) = \int_{-\infty}^{\infty} f_X(x)f_Y(z-x) \,dx$

[正态分布](@entry_id:154414)在线性组合下具有优良的**封闭性**。也就是说，独立正态[随机变量](@entry_id:195330)的任意线性组合仍然服从[正态分布](@entry_id:154414)。这是一个非常强大且应用广泛的性质。

假设 $X_1 \sim \mathcal{N}(\mu_1, \sigma_1^2)$ 和 $X_2 \sim \mathcal{N}(\mu_2, \sigma_2^2)$ 是两个独立的[随机变量](@entry_id:195330)，它们的[线性组合](@entry_id:154743) $Z = aX_1 + bX_2$ 的[分布](@entry_id:182848)是什么？
$Z$ 仍然是一个正态[随机变量](@entry_id:195330)，其均值和[方差](@entry_id:200758)分别为：
$E[Z] = E[aX_1 + bX_2] = aE[X_1] + bE[X_2] = a\mu_1 + b\mu_2$
$\text{Var}(Z) = \text{Var}(aX_1 + bX_2) = a^2\text{Var}(X_1) + b^2\text{Var}(X_2) = a^2\sigma_1^2 + b^2\sigma_2^2$
（注意[方差](@entry_id:200758)计算中系数是平方的，且利用了独立性使得协[方差](@entry_id:200758)项为零）。

例如，一个[生物传感器](@entry_id:182252)测量的总噪声电压 $V_{noise}$ 来自两个独立的内部组件 $N_1$ 和 $N_2$ [@problem_id:1408034]。假设 $N_1 \sim \mathcal{N}(\mu_1=1, \sigma_1^2=1)$，$N_2 \sim \mathcal{N}(\mu_2=1, \sigma_2^2=7/4)$，总噪声是它们的加权组合 $V_{noise} = 3N_1 - 2N_2$。根据上述法则，$V_{noise}$ 服从正态分布，其均值为：
$\mu_V = 3\mu_1 - 2\mu_2 = 3(1) - 2(1) = 1$
其[方差](@entry_id:200758)为：
$\sigma_V^2 = 3^2\sigma_1^2 + (-2)^2\sigma_2^2 = 9(1) + 4(7/4) = 9 + 7 = 16$
因此，$V_{noise} \sim \mathcal{N}(1, 16)$。利用这个结果，我们就可以计算任何关于 $V_{noise}$ 的概率，例如它超过某一阈值的可能性。

### 通用方法：[变量替换](@entry_id:141386)法（[雅可比行列式](@entry_id:137120)）

当变换更为复杂时，例如[非线性变换](@entry_id:636115)或多对多变量的变换，我们需要一个更通用的工具——**变量替换法**。该方法源于[多变量微积分](@entry_id:147547)中的[换元积分法](@entry_id:144683)，其核心是**雅可比行列式 (Jacobian determinant)**。

假设我们有一对[连续随机变量](@entry_id:166541) $(X_1, X_2)$，其联合 PDF 为 $f_{X_1, X_2}(x_1, x_2)$。我们通过一组函数定义了新的[随机变量](@entry_id:195330) $(Y_1, Y_2)$：
$y_1 = g_1(x_1, x_2)$
$y_2 = g_2(x_1, x_2)$
为了找到 $(Y_1, Y_2)$ 的联合 PDF $f_{Y_1, Y_2}(y_1, y_2)$，我们需要找到这个变换的[反函数](@entry_id:141256)：
$x_1 = h_1(y_1, y_2)$
$x_2 = h_2(y_1, y_2)$

新变量的联合 PDF 由以下公式给出：
$f_{Y_1, Y_2}(y_1, y_2) = f_{X_1, X_2}(h_1(y_1, y_2), h_2(y_1, y_2)) \cdot |J|$
其中，$|J|$ 是**雅可比行列式**的[绝对值](@entry_id:147688)，它度量了在变换过程中无穷小[面积元](@entry_id:263205)素的缩放比例。[雅可比行列式](@entry_id:137120)定义为[反函数](@entry_id:141256)的偏导数组成的[矩阵的行列式](@entry_id:148198)：
$J = \det \begin{pmatrix} \frac{\partial x_1}{\partial y_1} & \frac{\partial x_1}{\partial y_2} \\ \frac{\partial x_2}{\partial y_1} & \frac{\partial x_2}{\partial y_2} \end{pmatrix}$

这个方法威力强大，可以处理线性和[非线性变换](@entry_id:636115)。

#### [线性变换](@entry_id:149133)的应用

考虑两个独立的随机信号 $X$ 和 $Y$，它们都服从 $[0,1]$ 上的[均匀分布](@entry_id:194597) [@problem_id:1408018]。我们测量它们的和 $U=X+Y$ 与差 $V=X-Y$。[原始变量](@entry_id:753733) $(X,Y)$ 的联合 PDF 在单位正方形 $[0,1]\times[0,1]$ 上为 $f_{X,Y}(x,y)=1$，在其他地方为 0。

变换是 $u=x+y, v=x-y$。其反变换是 $x = (u+v)/2, y = (u-v)/2$。计算雅可比行列式：
$J = \det \begin{pmatrix} \frac{\partial x}{\partial u} & \frac{\partial x}{\partial v} \\ \frac{\partial y}{\partial u} & \frac{\partial y}{\partial v} \end{pmatrix} = \det \begin{pmatrix} 1/2 & 1/2 \\ 1/2 & -1/2 \end{pmatrix} = -\frac{1}{4} - \frac{1}{4} = -\frac{1}{2}$
因此，$|J| = 1/2$。
新变量 $(U,V)$ 的联合 PDF 是 $f_{U,V}(u,v) = f_{X,Y}((u+v)/2, (u-v)/2) \cdot |J| = 1 \cdot \frac{1}{2} = \frac{1}{2}$。

重要的是，我们还需要确定新变量的支撑域。原始约束 $0 \le x \le 1$ 和 $0 \le y \le 1$ 变换为 $0 \le (u+v)/2 \le 1$ 和 $0 \le (u-v)/2 \le 1$。这个不等式组定义了在 $(u,v)$ 平面上的一个旋转了45度的正方形（菱形）。因此，$(U,V)$ 的联合 PDF 在这个菱形区域内为 $1/2$，在区域外为 0。

同样的方法可以应用于一个有趣的物理模型中。一个简化的双通道[通信系统](@entry_id:265921)状态可以用一个 $2 \times 2$ 对称[随机矩阵](@entry_id:269622) $M$ 来描述 [@problem_id:1408009]。其中 $X, Y$ 是独立的标准正态[随机变量](@entry_id:195330)。该矩阵的[特征值](@entry_id:154894) $\Lambda_1, \Lambda_2$ 被证明为 $\Lambda_1 = X+Y$ 和 $\Lambda_2 = X-Y$。这与我们刚刚的变换完全相同！只是现在 $X, Y \sim \mathcal{N}(0,1)$。

由于 $X, Y$ 独立，其联合 PDF 为 $f_{X,Y}(x,y) = \frac{1}{2\pi} \exp(-(x^2+y^2)/2)$。雅可比行列式的[绝对值](@entry_id:147688)仍然是 $1/2$。我们将 $x = (\lambda_1+\lambda_2)/2, y = (\lambda_1-\lambda_2)/2$ 代入指数部分：
$x^2+y^2 = \frac{(\lambda_1+\lambda_2)^2}{4} + \frac{(\lambda_1-\lambda_2)^2}{4} = \frac{\lambda_1^2+\lambda_2^2}{2}$
因此，[特征值](@entry_id:154894)的联合 PDF 为：
$f_{\Lambda_1, \Lambda_2}(\lambda_1, \lambda_2) = f_{X,Y}(x,y) |J| = \frac{1}{2\pi} \exp\left(-\frac{\lambda_1^2+\lambda_2^2}{4}\right) \cdot \frac{1}{2} = \frac{1}{4\pi} \exp\left(-\frac{\lambda_1^2+\lambda_2^2}{4}\right)$
这个结果可以分解为两个独立的正态分布 PDF 的乘积：$f(\lambda_1) \propto \exp(-\lambda_1^2/4)$ 和 $f(\lambda_2) \propto \exp(-\lambda_2^2/4)$。这表明，两个[特征值](@entry_id:154894) $\Lambda_1$ 和 $\Lambda_2$ 也是[相互独立](@entry_id:273670)的，并且均服从均值为 0、[方差](@entry_id:200758)为 2 的正态分布，即 $\mathcal{N}(0,2)$。

#### [非线性变换](@entry_id:636115)的应用

[雅可比方法](@entry_id:270947)在[非线性变换](@entry_id:636115)中更显威力。

**变量之比：** 在[流体力学](@entry_id:136788)模型中，一个[质点](@entry_id:186768)的速度分量 $V_x$ 和 $V_y$ 可能被建模为独立的标准正态[随机变量](@entry_id:195330)。我们可能对速度矢量的斜率 $S = V_y/V_x$ 感兴趣 [@problem_id:1407993]。这是一个[非线性变换](@entry_id:636115)。为了使用双变量变换法，我们需要引入一个辅助变量，例如 $W=V_x$。

变换为 $s = y/x, w = x$。反变换为 $x=w, y=sw$。[雅可比行列式](@entry_id:137120)为：
$J = \det \begin{pmatrix} \frac{\partial x}{\partial s} & \frac{\partial x}{\partial w} \\ \frac{\partial y}{\partial s} & \frac{\partial y}{\partial w} \end{pmatrix} = \det \begin{pmatrix} 0 & 1 \\ w & s \end{pmatrix} = -w$
因此 $|J| = |w|$。
$(S,W)$ 的联合 PDF 为：
$f_{S,W}(s,w) = f_{X,Y}(w, sw) |J| = \frac{1}{2\pi} \exp\left(-\frac{w^2+(sw)^2}{2}\right) |w| = \frac{|w|}{2\pi} \exp\left(-\frac{w^2(1+s^2)}{2}\right)$

为了得到 $S$ 的边际 PDF，我们需要将联合 PDF 对 $w$ 在 $(-\infty, \infty)$ 上积分：
$f_S(s) = \int_{-\infty}^{\infty} \frac{|w|}{2\pi} \exp\left(-\frac{w^2(1+s^2)}{2}\right) dw$
通过计算这个积分（利用其偶函数特性和 u-代换），我们得到一个惊人的结果：
$f_S(s) = \frac{1}{\pi(1+s^2)}$
这是**标准[柯西分布](@entry_id:266469)**的 PDF。柯西分布是一个奇特的[分布](@entry_id:182848)，其期望和[方差](@entry_id:200758)均不存在（积分不收敛）。这表明，即使是由行为良好（有界矩）的正态变量构造出的变量，其性质也可能截然不同。

**Box-Muller 变换：** 在计算机模拟中，我们常常需要从易于生成的[均匀分布](@entry_id:194597)随机数来产生其他[分布](@entry_id:182848)的随机数。Box-Muller 变换是一个著名的方法，它通过巧妙的[非线性变换](@entry_id:636115)，将两个独立的 Uniform(0,1) [随机变量](@entry_id:195330) $U_1, U_2$ 转化为两个独立的标准正态[随机变量](@entry_id:195330) $X, Y$ [@problem_id:1408014, @problem_id:16820]。

变换本身是：
$X = \sqrt{-2 \ln U_1} \cos(2\pi U_2)$
$Y = \sqrt{-2 \ln U_1} \sin(2\pi U_2)$

这个变换可以看作是将 $(U_1, U_2)$ 映射到极坐标 $(R, \Theta)$，其中 $R^2 = -2 \ln U_1$ 且 $\Theta = 2\pi U_2$，然后再将极坐标转换为笛卡尔坐标 $(X, Y)$。
我们可以直接应用[雅可比方法](@entry_id:270947)。首先求反变换：
$X^2+Y^2 = -2 \ln U_1 \implies U_1 = \exp(-(X^2+Y^2)/2)$
$Y/X = \tan(2\pi U_2) \implies U_2 = \frac{1}{2\pi} \arctan(Y/X)$
计算这个反变换（从 $(X,Y)$ 到 $(U_1, U_2)$）的雅可比行列式 $|J|$，可以得到 $|J| = \frac{1}{2\pi} \exp(-(X^2+Y^2)/2)$。
由于 $U_1, U_2$ 的联合 PDF 在单位正方形内为 1，根据[变量替换公式](@entry_id:139692)，我们得到 $(X,Y)$ 的联合 PDF：
$f_{X,Y}(x,y) = f_{U_1, U_2}(u_1, u_2) \cdot |J| = 1 \cdot \frac{1}{2\pi} \exp\left(-\frac{x^2+y^2}{2}\right)$
这正是两个独立标准正态[随机变量](@entry_id:195330)的联合 PDF！这个优雅的结果不仅是变量替换法的一个绝佳范例，也为蒙特卡洛模拟提供了基础工具。

反过来，从两个独立标准正态 $X, Y$ 变换到极坐标 $R=\sqrt{X^2+Y^2}, \Theta=\arctan(Y/X)$ [@problem_id:16820]，其[雅可比行列式](@entry_id:137120)（前向变换）为 $r$。因此，$(R, \Theta)$ 的联合 PDF 为：
$f_{R,\Theta}(r,\theta) = f_{X,Y}(r\cos\theta, r\sin\theta) \cdot r = \frac{1}{2\pi} \exp(-r^2/2) \cdot r = \left(\frac{1}{2\pi}\right) \cdot \left(r \exp(-r^2/2)\right)$
这个 PDF 可以分解为 $r$ 的函数和 $\theta$ 的函数（常数），表明径向距离 $R$ 和角度 $\Theta$ 是独立的。其中 $\Theta$ 在 $[0, 2\pi)$ 上[均匀分布](@entry_id:194597)，而 $R$ 服从瑞利(Rayleigh)[分布](@entry_id:182848)。

### 分层模型与[混合分布](@entry_id:276506)

在许多现实场景中，一个[随机过程](@entry_id:159502)的参数本身可能不是固定的，而是另一个[随机过程](@entry_id:159502)的结果。这种模型被称为**分层模型 (Hierarchical Models)** 或 **[混合分布](@entry_id:276506) (Mixture Distributions)**。为了求得最终观测变量的[边际分布](@entry_id:264862)，我们需要用[全概率公式](@entry_id:194231)对其所有可能的参数值进行“平均”。

假设[随机变量](@entry_id:195330) $X$ 的[分布](@entry_id:182848)依赖于参数 $P$，其条件 PMF 或 PDF 为 $f_{X|P}(x|p)$。如果参数 $P$ 本身是一个[随机变量](@entry_id:195330)，其 PDF 为 $f_P(p)$，那么 $X$ 的[边际分布](@entry_id:264862)可以通过对 $p$ 的所有可[能值](@entry_id:187992)积分（或求和）得到：
$f_X(x) = \int f_{X|P}(x|p) f_P(p) dp$

考虑一个通信网络，其中单次传输的成功率 $P$ 受信道条件波动影响，被建模为一个服从 Beta [分布](@entry_id:182848) $B(a,b)$ 的[随机变量](@entry_id:195330)。对于一个给定的成功率 $P=p$，首次成功传输所需的尝试次数 $X$ 服从几何分布 [@problem_id:1408033]。$X$ 的[边际概率质量函数](@entry_id:184224)是什么？

$X$ 的条件 PMF 为 $P(X=k | P=p) = p(1-p)^{k-1}$。$P$ 的 PDF 为 $f_P(p) = \frac{p^{a-1}(1-p)^{b-1}}{B(a,b)}$。
$X$ 的边际 PMF 为：
$P(X=k) = \int_0^1 P(X=k | P=p) f_P(p) dp = \int_0^1 p(1-p)^{k-1} \frac{p^{a-1}(1-p)^{b-1}}{B(a,b)} dp$
$P(X=k) = \frac{1}{B(a,b)} \int_0^1 p^{a} (1-p)^{b+k-2} dp = \frac{1}{B(a,b)} \int_0^1 p^{(a+1)-1} (1-p)^{(b+k-1)-1} dp$
我们发现，积分部分正比于另一个 Beta [分布](@entry_id:182848)的核。根据 Beta 函数的积分定义 $\int_0^1 t^{\alpha-1}(1-t)^{\beta-1} dt = B(\alpha, \beta)$，上述积分等于 $B(a+1, b+k-1)$。
因此，
$P(X=k) = \frac{B(a+1, b+k-1)}{B(a,b)}$
这个结果被称为**贝塔-几何分布**（或贝塔-[负二项分布](@entry_id:262151)的特例），它描述了一个成功概率本身是随机的伯努利试验序列中的等待时间。

### [随机变量函数的期望](@entry_id:194426)

有时，我们关心的不是[随机变量](@entry_id:195330)函数的完整[分布](@entry_id:182848)，而只是它的某些数字特征，如期望。一个极其有用的定理是**“无意识统计学家法则” (Law of the Unconscious Statistician, LOTUS)**。它指出，要计算 $g(X_1, ..., X_n)$ 的期望，我们不需要先求出 $g$ 的[分布](@entry_id:182848)，而是可以直接在原始变量的联合分布上进行积分：
$E[g(X_1, ..., X_n)] = \int \dots \int g(x_1, ..., x_n) f_{X_1, ..., X_n}(x_1, ..., x_n) dx_1 \dots dx_n$

例如，在处理器质量测试中，两个任务的完成时间 $(X,Y)$ [均匀分布](@entry_id:194597)在由 $x \ge 0, y \ge 0, 1 \le x+y \le 3$ 定义的区域 $\mathcal{R}$ 上 [@problem_id:1407985]。我们想计算平均完成时间 $Z = (X+Y)/2$ 的平方的期望 $E[Z^2]$。

首先，该区域 $\mathcal{R}$ 的面积是两个直角三角形面积之差：$\frac{1}{2} \cdot 3^2 - \frac{1}{2} \cdot 1^2 = 4$。由于 $(X,Y)$ 在此区域上[均匀分布](@entry_id:194597)，其联合 PDF 为 $f_{X,Y}(x,y) = 1/\text{Area}(\mathcal{R}) = 1/4$。
我们想求的期望是 $E[Z^2] = E[\frac{(X+Y)^2}{4}] = \frac{1}{4} E[(X+Y)^2]$。
根据 LOTUS，
$E[(X+Y)^2] = \iint_{\mathcal{R}} (x+y)^2 f_{X,Y}(x,y) \,dx\,dy = \frac{1}{4} \iint_{\mathcal{R}} (x+y)^2 \,dx\,dy$
计算这个在梯形区域 $\mathcal{R}$ 上的[二重积分](@entry_id:198869)，最终可得 $E[(X+Y)^2]=5$。因此，$E[Z^2] = 5/4$。

这个例子展示了 LOTUS 的直接性。我们无需费力去推导 $Z$ 或 $Z^2$ 的 PDF，就可以直接计算其[期望值](@entry_id:153208)，这在许多应用中大大简化了问题。