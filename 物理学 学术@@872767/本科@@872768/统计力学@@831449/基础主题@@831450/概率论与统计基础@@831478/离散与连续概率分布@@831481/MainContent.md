## 引言
在[统计力](@entry_id:194984)学的宏伟画卷中，概率论并非仅仅扮演数学配角，它本身就是描绘物理世界的根本语言。面对由海量粒子构成的系统，我们无法也不必去追踪每一个微观组分的精确轨迹。取而代之，我们运用概率来描述系统处于某一微观状态的可能性，或是一个粒子拥有特定能量与速度的几率。离散与[连续概率分布](@entry_id:636595)，正是构筑这套语言的两块核心基石，它们为我们从微观世界的内在随机性，过渡到宏观世界的可预测规律提供了关键的桥梁。

本文将带领读者踏上一段从理论到应用的探索之旅。首先，在“**原理与机制**”一章中，我们将从物理第一性原理出发，系统推导[二项分布](@entry_id:141181)、泊松分布、[高斯分布](@entry_id:154414)等基本概率模型，揭示它们与组合学、玻尔兹曼因子及量子统计的深刻联系。接着，在“**应用与跨学科联系**”一章，我们将视野拓宽，展示这些[分布](@entry_id:182848)如何统一解释气体动力学、[化学反应](@entry_id:146973)、生物进化等多样化现象，彰显统计思想的普适力量。最后，通过“**动手实践**”部分，您将有机会将抽象理论应用于具体问题，从而真正掌握这一连接微观与宏观世界的强大工具。

## 原理与机制

在[统计力](@entry_id:194984)学中，概率论不仅是一种数学工具，更是描述物理系统的基本语言。由于我们无法、也无需追踪宏观系统中每个粒子的精确轨迹，我们转而使用概率来描述系统处于某个特定微观状态的可能性，或者一个粒子拥有特定属性（如能量、速度）的可能性。本章将系统地介绍[统计力](@entry_id:194984)学中两种基本的[概率分布](@entry_id:146404)——[离散分布](@entry_id:193344)和连续分布——并阐明它们如何从物理第一性原理中推导出来，以及如何应用于解释各种物理现象。

### [离散概率分布](@entry_id:166565)

当一个系统的可及状态或一个可观测的物理量只能取一系列分立的数值时，我们使用[离散概率分布](@entry_id:166565)来描述其统计行为。在孤立系统中，一个基本假设是**等概率先验原理**（principle of equal a priori probability），即所有能量相同的微观状态都是等可能出现的。

#### [二项分布](@entry_id:141181)

在众多[离散分布](@entry_id:193344)中，**二项分布**（Binomial Distribution）最为基础，它描述了一系列独立、重复的二选一（“成功”或“失败”）事件中，“成功”出现特定次数的概率。

想象一个由 $N$ 个无相互作用的、全同的子系统组成的体系，每个子系统只有两种可能的状态。一个经典的例子是无外[磁场](@entry_id:153296)下的自旋-$1/2$ [粒子系统](@entry_id:180557)。每个粒子的[自旋磁矩](@entry_id:272337)可以指向“上”或“下”，分别对总磁化强度贡献 $+\mu$ 和 $-\mu$。在没有能量偏好的情况下（例如，在高温极限下），每个自旋向上或向下的概率都是 $1/2$。

为了具体说明，让我们考虑一个由 $N=10$ 个独立原子组成的[磁畴](@entry_id:147690)模型。一个特定的微观状态由 10 个自旋的具体朝向（例如，“上上上上上上上上上上”或“下上上下上上下上”）所定义。总共有 $2^{10}$ 种可能的微观状态，根据等概率原理，每种状态出现的概率都是 $(1/2)^{10}$。

现在，我们关心的是系统的宏观性质，例如总磁化强度 $M$，而不是具体的微观[排列](@entry_id:136432)。假设我们想知道总磁化强度 $M = -2\mu$ 的概率 [@problem_id:1962014]。总磁化强度由“上”自旋数 $n_{\uparrow}$ 和“下”自旋数 $n_{\downarrow}$ 决定：
$$
M = n_{\uparrow}(+\mu) + n_{\downarrow}(-\mu) = (n_{\uparrow} - n_{\downarrow})\mu
$$
由于[总自旋](@entry_id:153335)数为 $N = n_{\uparrow} + n_{\downarrow} = 10$，我们可以将 $n_{\downarrow}$ 替换为 $10 - n_{\uparrow}$，得到：
$$
M = (n_{\uparrow} - (10 - n_{\uparrow}))\mu = (2n_{\uparrow} - 10)\mu
$$
要使 $M = -2\mu$，我们必须有 $2n_{\uparrow} - 10 = -2$，解得 $n_{\uparrow} = 4$。因此，宏观状态 $M = -2\mu$ 对应于任何包含 4 个“上”自旋和 6 个“下”自旋的微观状态。

问题转化为：从 10 个自旋中选出 4 个为“上”自旋有多少种方式？这个数目由组合数给出：
$$
\binom{10}{4} = \frac{10!}{4!(10-4)!} = \frac{10 \times 9 \times 8 \times 7}{4 \times 3 \times 2 \times 1} = 210
$$
这 210 种微观状态中的每一种都有相同的概率 $(1/2)^{10}$。因此，观测到 $M = -2\mu$ 的总概率是这些微观状态概率的总和：
$$
P(n_{\uparrow}=4) = \binom{10}{4} \left(\frac{1}{2}\right)^{4} \left(\frac{1}{2}\right)^{10-4} = 210 \times \left(\frac{1}{2}\right)^{10} = \frac{210}{1024} \approx 0.205
$$
这正是[二项分布](@entry_id:141181)的一般形式 $P(k) = \binom{N}{k} p^k (1-p)^{N-k}$，其中 $N=10$, $k=4$, $p=1/2$。

#### [泊松分布](@entry_id:147769)

当试验次数 $N$ 非常大，而单次事件的成功概率 $p$ 非常小时，二项分布可以近似为一个更简单的[分布](@entry_id:182848)——**[泊松分布](@entry_id:147769)**（Poisson Distribution）。这个极限在物理学中非常普遍，特别适用于描述稀有事件的计数问题。

一个典型的例子是[放射性衰变](@entry_id:142155)。考虑一个包含极大数量 $N$ 的放射性[原子核](@entry_id:167902)的样品。每个[原子核](@entry_id:167902)在单位时间内发生衰变的概率是一个常数 $\lambda$，称为[衰变常数](@entry_id:149530)。在一段很短的时间间隔 $\Delta t$ 内，单个[原子核衰变](@entry_id:140740)的概率 $p = \lambda \Delta t$ 非常小。我们想知道在这段时间内观测到恰好 $k$ 个衰变事件的概率 $P(k)$ 是多少 [@problem_id:1961989]。

我们可以将每个[原子核](@entry_id:167902)视为进行一次独立的“[伯努利试验](@entry_id:268355)”，其中“成功”代表衰变。因此，这个问题可以用[二项分布](@entry_id:141181)来精确描述：
$$
P(k) = \binom{N}{k} p^k (1-p)^{N-k} = \binom{N}{k} (\lambda \Delta t)^k (1 - \lambda \Delta t)^{N-k}
$$
由于 $N$ 极大，$p$ 极小，直接计算二项分布会非常困难。然而，当 $N \to \infty$ 且 $p \to 0$，而它们的乘积——平均成功次数 $\mu = Np = N\lambda\Delta t$ 保持为一个有限的常数时，[二项分布](@entry_id:141181)收敛于[泊松分布](@entry_id:147769)。

推导过程如下：
1.  对于固定的 $k$ 和极大的 $N$，组[合数](@entry_id:263553) $\binom{N}{k} = \frac{N(N-1)\cdots(N-k+1)}{k!}$ 近似为 $\frac{N^k}{k!}$。
2.  $(1-p)^{N-k} = (1 - \frac{\mu}{N})^{N-k} \approx (1 - \frac{\mu}{N})^N$。根据[指数函数](@entry_id:161417)的定义，当 $N \to \infty$ 时，$(1 - \frac{\mu}{N})^N \to \exp(-\mu)$。

将这些近似代入[二项分布公式](@entry_id:269272)：
$$
P(k) \approx \frac{N^k}{k!} (\frac{\mu}{N})^k \exp(-\mu) = \frac{N^k \mu^k}{k! N^k} \exp(-\mu) = \frac{\mu^k \exp(-\mu)}{k!}
$$
将 $\mu = N\lambda\Delta t$ 代回，我们得到在时间 $\Delta t$ 内观测到 $k$ 次衰变的概率：
$$
P(k) = \frac{(N\lambda\Delta t)^k \exp(-N\lambda\Delta t)}{k!}
$$
泊松分布简洁地描述了在给定时间或空间区域内，独立随机事件发生的次数。除了放射性衰变，它还被用来模拟[光子](@entry_id:145192)探测器接收到的[光子](@entry_id:145192)数、气体中的分子碰撞次数等众多物理过程。

### [连续概率分布](@entry_id:636595)

当一个物理量（如位置、动量或能量）可以在一个连续的区间内取任何值时，我们使用**[概率密度函数](@entry_id:140610)**（Probability Density Function, PDF）$p(x)$ 来描述其[分布](@entry_id:182848)。$p(x)$ 本身不是概率，但 $p(x)dx$ 表示该物理量的值落在无穷小区间 $[x, x+dx]$ 内的概率。一个合法的概率密度函数必须是非负的，并且在其整个定义域上的积分为 1，即 $\int p(x)dx = 1$。

#### 指数分布

考虑单个放射性[原子核](@entry_id:167902)的寿命问题。与泊松分布描述“在给定时间内发生多少次事件”不同，我们现在关心的是“发生第一次事件需要等待多长时间”。假设[原子核](@entry_id:167902)在任何无限小时间间隔 $dt$ 内发生衰变的概率是 $\lambda dt$，且这个概率不随[原子核](@entry_id:167902)的“年龄”而改变——这就是所谓的**无记忆性**（memoryless property）。

我们可以推导出[原子核](@entry_id:167902)存活到时间 $t$ 之后的概率，即**生存函数** $S(t)$。[原子核](@entry_id:167902)存活到时间 $t+dt$ 的概率，等于它存活到时间 $t$ 的概率乘以它在接下来的 $dt$ 时间内不衰变的概率：
$$
S(t+dt) = S(t) \times (1 - \lambda dt)
$$
整理后得到[微分方程](@entry_id:264184)：
$$
\frac{S(t+dt) - S(t)}{dt} = -\lambda S(t) \implies \frac{dS}{dt} = -\lambda S(t)
$$
考虑到初始条件 $S(0)=1$（在 $t=0$ 时[原子核](@entry_id:167902)肯定存活），该方程的解为：
$$
S(t) = \exp(-\lambda t)
$$
衰变时间 $T$ 的[概率密度函数](@entry_id:140610) $p(t)$ 与生存函数的关系是 $p(t) = - \frac{dS}{dt}$。因此，我们得到**[指数分布](@entry_id:273894)**（Exponential Distribution） [@problem_id:1962001]：
$$
p(t) = \lambda \exp(-\lambda t), \quad t \ge 0
$$
[衰变常数](@entry_id:149530) $\lambda$ 通常通过更直观的**[半衰期](@entry_id:144843)** $t_{1/2}$ 来表征，即[原子核](@entry_id:167902)有 $1/2$ 的概率存活的时间。由 $S(t_{1/2}) = \exp(-\lambda t_{1/2}) = 1/2$，可得 $\lambda = \frac{\ln 2}{t_{1/2}}$。因此，用半衰期表示的[概率密度函数](@entry_id:140610)为：
$$
p(t) = \frac{\ln 2}{t_{1/2}} \exp\left(-\frac{\ln 2}{t_{1/2}} t\right)
$$

#### [高斯分布](@entry_id:154414)

**高斯分布**（Gaussian Distribution），或称正态分布，是自然科学中无处不在的最重要的[概率分布](@entry_id:146404)。其普遍性的一个深层原因与[热力学](@entry_id:141121)中的涨落理论有关：一个处于稳定平衡态的系统，其微小涨落的[概率分布](@entry_id:146404)通常是高斯的。

[高斯分布](@entry_id:154414)的概率密度函数形式为：
$$
p(x) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)
$$
其中 $\mu$ 是[分布](@entry_id:182848)的均值（峰值位置），$\sigma^2$ 是[方差](@entry_id:200758)，它衡量了[分布](@entry_id:182848)的宽度。

在[统计力](@entry_id:194984)学中，高斯分布的出现常常源于能量与某个变量的平方成正比，并通过[玻尔兹曼因子](@entry_id:141054) $\exp(-E/k_B T)$ 决定其概率。
- **气体分子的速度**：对于处于热平衡温度为 $T$ 的[理想气体](@entry_id:200096)，单个分子沿 $x$ 轴运动的动能为 $E_x = \frac{1}{2}mv_x^2$。根据[玻尔兹曼分布](@entry_id:142765)，其速度分量 $v_x$ 的概率密度与 $\exp(-E_x / k_B T)$ 成正比：
$$
f(v_x) \propto \exp\left(-\frac{mv_x^2}{2k_B T}\right)
$$
这是一个以 $v_x=0$ 为中心的高斯分布。[分布](@entry_id:182848)的宽度直接与温度有关。我们可以通过计算其**半峰全宽**（Full Width at Half Maximum, FWHM）来量化这一关系 [@problem_id:1962004]。FWHM 是指[分布](@entry_id:182848)高度为其最大值一半处的宽度。通过求解 $f(v_h) = \frac{1}{2}f(0)$，可以得到 $v_h = \sqrt{\frac{2 k_B T \ln 2}{m}}$。因此，FWHM 为 $2v_h = 2\sqrt{\frac{2 k_B T \ln 2}{m}}$，表明温度越高，速度[分布](@entry_id:182848)越宽。

- **[热力学](@entry_id:141121)涨落**：[高斯分布](@entry_id:154414)也是描述宏观量在平衡态附近涨落的通用模型。例如，一个与大热源接触的小系统，其能量会围绕平均值 $\langle E \rangle$ 涨落。通过对熵 $S$ 在能量 $E$ 的[平衡点](@entry_id:272705)附近进行[泰勒展开](@entry_id:145057)，可以证明小[能量涨落](@entry_id:148029) $\delta E = E - \langle E \rangle$ 的[概率分布](@entry_id:146404)是高斯的 [@problem_id:1961997]：
$$
P(\delta E) \propto \exp\left(-\frac{(\delta E)^2}{2k_B T^2 C_V}\right)
$$
这里的 $C_V$ 是系统的[定容热容](@entry_id:147536)。这个结果非常深刻：涨落[分布](@entry_id:182848)的宽度（[方差](@entry_id:200758) $\sigma_E^2 = k_B T^2 C_V$）直接由一个宏观可测量的响应函数（[热容](@entry_id:137594)）决定。热容越大，系统[能量涨落](@entry_id:148029)越剧烈。

- **[相变](@entry_id:147324)临界现象**：在描述[二级相变](@entry_id:154877)的[朗道理论](@entry_id:138967)中，序参量 $\phi$ 的涨落也遵循高斯分布。在临界温度 $T_c$ 之上，系统的自由能 $F$ 对小的序参量涨落可以近似为二次形式 $F \approx F_0 + \frac{1}{2}\alpha(T-T_c)\phi^2$。因此，涨落的[概率分布](@entry_id:146404)为 [@problem_id:1961979]：
$$
P(\phi) \propto \exp\left(-\frac{F(\phi)}{k_B T}\right) \propto \exp\left(-\frac{\alpha(T-T_c)}{2k_B T} \phi^2\right)
$$
这是一个中心在 $\phi=0$ 的[高斯分布](@entry_id:154414)，其[方差](@entry_id:200758) $\sigma^2 = \frac{k_B T}{\alpha(T-T_c)}$。可以看到，当温度 $T$ 趋近于[临界温度](@entry_id:146683) $T_c$ 时，[方差](@entry_id:200758)发散，意味着序参量的涨落变得极其剧烈，这是[临界现象](@entry_id:144727)的标志性特征。

### [概率分布](@entry_id:146404)的变换与推导

在物理问题中，我们常常知道一个变量的[概率分布](@entry_id:146404)，并希望求出另一个与之相关的变量的[分布](@entry_id:182848)。这需要通过**变量代换**（change of variables）的方法来实现。

如果变量 $x$ 的[概率密度](@entry_id:175496)为 $p_X(x)$，变量 $y$ 与 $x$ 的关系为 $y=g(x)$，那么 $y$ 的概率密度 $p_Y(y)$ 可以通过保持概率元不变得到：
$$
p_Y(y) |dy| = p_X(x) |dx|
$$
由此可得：
$$
p_Y(y) = p_X(x(y)) \left| \frac{dx}{dy} \right|
$$
其中 $\left| \frac{dx}{dy} \right|$ 是雅可比行列式（在一维情况下是导数的[绝对值](@entry_id:147688)）。如果从 $x$到$y$的映射不是一对一的，我们需要对所有贡献到同一点 $y$ 的 $x_i$ 值进行求和：$p_Y(y) = \sum_i p_X(x_i(y)) \left| \frac{dx_i}{dy} \right|$。

#### 从动量分布到能量[分布](@entry_id:182848)

考虑一个被限制在[一维运动](@entry_id:190890)的经典气体粒子。其动量 $p_x$ 服从[高斯分布](@entry_id:154414) $f(p_x) \propto \exp\left(-\frac{p_x^2}{2mk_B T}\right)$。我们想求其动能 $E = \frac{p_x^2}{2m}$ 的[概率分布](@entry_id:146404) $P(E)$ [@problem_id:1962007]。

这是一个二对一的映射：动量 $+p_x$ 和 $-p_x$ 对应同一个能量 $E > 0$，其中 $p_x = \sqrt{2mE}$。因此，我们需要将两个动量值的贡献相加：
$$
P(E) dE = f(p_x) dp_x + f(-p_x) d(-p_x) = 2 f(\sqrt{2mE}) dp_x
$$
由于 $E = p_x^2 / (2m)$，我们有 $dE = \frac{p_x}{m} dp_x$，即 $dp_x = \frac{m}{p_x} dE = \frac{m}{\sqrt{2mE}} dE$。代入归一化后的动量分布 $f(p_x) = \frac{1}{\sqrt{2\pi m k_B T}} \exp\left(-\frac{p_x^2}{2mk_B T}\right)$，可得：
$$
P(E) = 2 f(\sqrt{2mE}) \frac{m}{\sqrt{2mE}} = 2 \frac{1}{\sqrt{2\pi m k_B T}} \exp\left(-\frac{E}{k_B T}\right) \frac{\sqrt{m}}{\sqrt{2E}}
$$
化简后得到：
$$
P(E) = \frac{1}{\sqrt{\pi k_B T E}} \exp\left(-\frac{E}{k_B T}\right)
$$
这个结果显示，即使[动量分布](@entry_id:162113)是高斯的，其对应的能量[分布](@entry_id:182848)由于 $p_x \to E$ 的平方关系而呈现出不同的形式，并在 $E \to 0$ 时发散。

#### 从速度[分布](@entry_id:182848)到能量[分布](@entry_id:182848)

对于三维[理想气体](@entry_id:200096)，分子的速率 $v$ 服从**[麦克斯韦-玻尔兹曼速率分布](@entry_id:195533)**：
$$
f(v) = 4\pi \left( \frac{m}{2\pi k_B T} \right)^{3/2} v^2 \exp\left(-\frac{mv^2}{2k_B T}\right)
$$
我们希望得到其[平动能](@entry_id:170705) $\epsilon = \frac{1}{2}mv^2$ 的[分布](@entry_id:182848) $P(\epsilon)$ [@problem_id:1962003]。这是一个从 $v \ge 0$ 到 $\epsilon \ge 0$ 的一对一映射。我们使用变量代换法则 $P(\epsilon) = f(v(\epsilon)) \left| \frac{dv}{d\epsilon} \right|$。
我们有 $v = \sqrt{2\epsilon/m}$，以及 $\frac{dv}{d\epsilon} = \frac{1}{m} \sqrt{\frac{m}{2\epsilon}} = \frac{1}{\sqrt{2m\epsilon}}$。代入 $f(v)$ 的表达式：
$$
P(\epsilon) = 4\pi \left( \frac{m}{2\pi k_B T} \right)^{3/2} \left(\frac{2\epsilon}{m}\right) \exp\left(-\frac{\epsilon}{k_B T}\right) \frac{1}{\sqrt{2m\epsilon}}
$$
经过一系列代数化简，最终得到能量[分布](@entry_id:182848)：
$$
P(\epsilon) = \frac{2}{\sqrt{\pi} (k_B T)^{3/2}} \sqrt{\epsilon} \exp\left(-\frac{\epsilon}{k_B T}\right)
$$
这个[分布](@entry_id:182848)在物理学中非常重要，它描述了处于热平衡的气体中分子的能量是如何[分布](@entry_id:182848)的。

#### 从几何均匀性到坐标[分布](@entry_id:182848)

[概率分布](@entry_id:146404)也可能源于几何约束。考虑一个被限制在半径为 $R$ 的球面上的粒子，其在球面任何区域被发现的概率正比于该区域的面积 [@problem_id:1961968]。我们想求其极角坐标 $\theta \in [0, \pi]$ 的概率密度函数 $p(\theta)$。

在[球坐标系](@entry_id:167517)中，面积微元为 $dA = R^2 \sin\theta d\theta d\phi$。粒子出现在 $\theta$ 到 $\theta+d\theta$ 之间的[环带](@entry_id:163678)区域的概率，正比于该环带的面积。这个[环带](@entry_id:163678)的面积是通过对整个方位角 $\phi \in [0, 2\pi)$ 积分得到的：
$$
A_{\text{strip}} = \int_0^{2\pi} R^2 \sin\theta d\theta d\phi = 2\pi R^2 \sin\theta d\theta
$$
因此，概率 $p(\theta)d\theta$ 正比于 $\sin\theta d\theta$，即 $p(\theta) \propto \sin\theta$。为了归一化，我们计算积分：
$$
\int_0^\pi C \sin\theta d\theta = C [-\cos\theta]_0^\pi = 2C = 1 \implies C = \frac{1}{2}
$$
所以，归一化的概率密度函数为：
$$
p(\theta) = \frac{1}{2}\sin\theta, \quad \theta \in [0, \pi]
$$
这个结果表明，即使粒子在球面上是“均匀”[分布](@entry_id:182848)的，其极角坐标的[分布](@entry_id:182848)却不是均匀的。在赤道（$\theta = \pi/2$）附近找到粒子的概率最大，而在两极（$\theta=0, \pi$）附近找到粒子的概率趋于零，这完全是几何效应的体现。

### 源于[量子统计](@entry_id:143815)的[分布](@entry_id:182848)

当处理由[全同粒子](@entry_id:142755)（如电子）组成的稠密系统时，必须考虑量子力学效应，特别是[泡利不相容原理](@entry_id:141850)。这导致了与经典[玻尔兹曼统计](@entry_id:746908)截然不同的[粒子分布](@entry_id:158657)。

考虑一个由 $N$ 个无相互作用的[费米子](@entry_id:146235)（如金属中的[传导电子](@entry_id:145260)）组成的系统。根据量子力学，系统存在一系列分立的单粒子能级。**[态密度](@entry_id:147894)** $g(\epsilon)$ 定义为能量在 $\epsilon$ 附近单位能量区间的[量子态](@entry_id:146142)数目。对于三维空间中的非相对论性[自由粒子](@entry_id:148748)，[态密度](@entry_id:147894)为 $g(\epsilon) = C \epsilon^{1/2}$，其中 $C$ 是一个常数。

在绝对零度（$T=0$）时，根据**[泡利不相容原理](@entry_id:141850)**，[费米子](@entry_id:146235)会从最低能级开始，依次填充所有可用的[量子态](@entry_id:146142)，直到所有 $N$ 个粒子都被安置完毕。最后一个粒子占据的能级能量被称为**[费米能](@entry_id:143977)** $E_F$。因此，在 $T=0$ 时，所有能量 $\epsilon \le E_F$ 的能级都被占据，而所有 $\epsilon > E_F$ 的能级都是空的。

如果我们从这个系统中随机抽取一个[费米子](@entry_id:146235)，它的能量会是多少？找到一个能量为 $\epsilon$ 的粒子的概率，应该正比于该能量处有多少粒子，而在 $T=0$ 时，这又正比于该能量处的态密度 $g(\epsilon)$。因此，单个粒子能量的[概率密度函数](@entry_id:140610) $P(\epsilon)$ 满足 [@problem_id:1961978]：
$$
P(\epsilon) \propto g(\epsilon) = C \epsilon^{1/2}, \quad \text{for } 0 \le \epsilon \le E_F
$$
且在 $\epsilon > E_F$ 时 $P(\epsilon)=0$。通过归一化 $\int_0^{E_F} P(\epsilon) d\epsilon = 1$，我们可以确定归一化常数，得到：
$$
P(\epsilon) = \frac{3}{2 E_F^{3/2}} \epsilon^{1/2}, \quad 0 \le \epsilon \le E_F
$$
利用这个[分布](@entry_id:182848)，可以计算[平均能量](@entry_id:145892) $\langle \epsilon \rangle = \frac{3}{5}E_F$ 和能量的二阶矩 $\langle \epsilon^2 \rangle = \frac{3}{7}E_F^2$。这进一步给出了能量[分布](@entry_id:182848)的标准差与平均值之比 $\frac{\sigma_\epsilon}{\langle \epsilon \rangle} = \frac{\sqrt{12/175}}{3/5} \approx 0.4364$，这个比值反映了[费米子](@entry_id:146235)能量在 $0$ 到 $E_F$ 之间的[分布](@entry_id:182848)特征。这种源于量子统计的[分布](@entry_id:182848)形式，是理解金属、白矮星等[费米子](@entry_id:146235)系统性质的关键。

综上所述，[概率分布](@entry_id:146404)是连接微观物理原理与宏观可观测现象的桥梁。无论是通过组合学分析、极限过程、玻尔兹曼因子、变量变换还是[量子统计](@entry_id:143815)原理，我们都能推导出描述物理系统行为的特定[概率分布](@entry_id:146404)，从而深刻地理解和预测它们的性质。