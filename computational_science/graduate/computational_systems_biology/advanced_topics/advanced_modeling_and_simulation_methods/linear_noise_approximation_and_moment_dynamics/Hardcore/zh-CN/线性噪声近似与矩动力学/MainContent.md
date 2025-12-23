## 引言
在细胞内部，许多关键[生物过程](@entry_id:164026)都由数量稀少的分子所驱动，其动力学行为因而表现出固有的随机性或“噪声”。精确描述这种随机性的[化学主方程](@entry_id:161378)（CME）往往难以求解，这为我们定量理解噪声在生物功能中的作用带来了巨大挑战。为了弥合这一知识鸿沟，[线性噪声近似](@entry_id:190628)（[LNA](@entry_id:150014)）应运而生，它提供了一个强大而灵活的分析框架，用于近似和分析这些随机生化系统。本文旨在全面介绍[LNA](@entry_id:150014)理论及其在[计算系统生物学](@entry_id:747636)中的应用。在接下来的章节中，我们将首先在“原理与机制”中，从第一性原理出发，系统地推导出[LNA](@entry_id:150014)，并阐明其核心思想——将动力学分解为确定性部分和高斯涨落部分。接着，在“应用与[交叉](@entry_id:147634)学科联系”中，我们将展示[LNA](@entry_id:150014)如何被用来分析[基因表达噪声](@entry_id:160943)、指导合成线路设计，并与信息论、[控制论](@entry_id:262536)等学科[交叉](@entry_id:147634)融合。最后，在“动手实践”部分，读者将通过具体的编码练习，亲手实现并比较[LNA](@entry_id:150014)与其他近似方法，从而巩固理论知识并获得实践技能。

## 原理与机制

本章旨在阐述[线性噪声近似](@entry_id:190628)（Linear Noise Approximation, [LNA](@entry_id:150014)）的核心原理与机制。我们将从[化学反应网络](@entry_id:151643)的随机性描述出发，系统地推导出[线性噪声近似](@entry_id:190628)，并展示如何利用它来分析生化系统中分子数量的涨落及其[矩动力学](@entry_id:752137)。我们将从基本的第一性原理出发，逐步构建起一个严谨的理论框架，并通过具体的例子来说明其应用和局限性。

### 从[主方程](@entry_id:142959)到确[定性动力学](@entry_id:263136)

在细胞这样的小体积环境中，许多分子种类（如[转录因子](@entry_id:137860)、[信使RNA](@entry_id:262893)）的数量可能非常少，导致它们的动力学行为具有显著的随机性。描述这类随机[化学反应](@entry_id:146973)系统的最基本和精确的数学工具是**[化学主方程](@entry_id:161378)**（Chemical Master Equation, CME）。

考虑一个包含 $n$ 种分子和 $R$ 个反应通道的充分混合系统。系统的状态可以用一个包含每种分子数量的向量 $x \in \mathbb{Z}_{\ge 0}^n$ 来描述。每个反应 $r$ 都与一个**化学计量向量**（stoichiometry vector）$\nu_r \in \mathbb{Z}^n$ 相关联，该[向量表示](@entry_id:166424)反应 $r$ 发生一次后，各种分子数量的变化。在状态 $x$ 下，反应 $r$ 在一个无穷小的时间间隔 $[t, t+\mathrm{d}t)$ 内发生的概率由其**[倾向函数](@entry_id:181123)**（propensity function）$a_r(x)$ 决定，即该概率为 $a_r(x)\mathrm{d}t$。

系统的状态随[时间演化](@entry_id:153943)，其[概率分布](@entry_id:146404) $P(x,t)$ 的变化由[化学主方程](@entry_id:161378)描述。该方程基于概率守恒原理，即某一状态的概率变化率等于从所有其他状态流入该状态的总概率流率减去从该状态流向所有其他状态的总概率流率。

具体来说，进入状态 $x$ 的唯一方式是通过某个反应 $r$ 从状态 $x - \nu_r$ 跃迁而来。因此，从状态 $x - \nu_r$ 流入状态 $x$ 的速率为 $a_r(x - \nu_r) P(x - \nu_r, t)$。另一方面，如果系统处于状态 $x$，任何反应 $r$ 的发生都会使其离开该状态，流出的总速率为 $(\sum_{r=1}^R a_r(x)) P(x,t)$。综合流入和流出，我们得到[化学主方程](@entry_id:161378)的精确形式 ：

$$
\frac{\partial P(x,t)}{\partial t} = \sum_{r=1}^R \left[ a_r(x - \nu_r) P(x - \nu_r, t) - a_r(x) P(x,t) \right]
$$

尽管[化学主方程](@entry_id:161378)是精确的，但它是一个（通常是无限维的）耦合[常微分方程组](@entry_id:266774)，除了极少数简单系统外，很难获得其解析解。因此，我们需要寻找有效的近似方法。

在宏观尺度上，当系统体积 $\Omega$ 和分子数 $x$ 都很大，使得浓度 $c = x/\Omega$ 保持有限时，随机涨落相对于平均值变得可以忽略不计。这被称为**[热力学极限](@entry_id:143061)**（thermodynamic limit）。在此极限下，我们可以从[化学主方程](@entry_id:161378)推导出描述宏观浓度演化的确定性**[反应速率](@entry_id:139813)方程**（Reaction Rate Equations, RREs）。

通过对[化学主方程](@entry_id:161378)求平均值，我们可以得到平均分子数 $\langle x_i \rangle$ 的[演化方程](@entry_id:268137)：$\frac{\mathrm{d}\langle x_i \rangle}{\mathrm{d}t} = \sum_{r=1}^R \nu_{ri} \langle a_r(x) \rangle$。在[热力学极限](@entry_id:143061)下，[分布](@entry_id:182848)变得极其尖锐，我们可以用均值的函数来近似函数的均值，即 $\langle a_r(x) \rangle \approx a_r(\langle x \rangle)$。将平均分子数 $\langle x(t) \rangle$ 等同于宏观变量 $\Omega c(t)$，我们得到：

$$
\frac{\mathrm{d}c(t)}{\mathrm{d}t} = \sum_{r=1}^R \nu_r \alpha_r(c(t))
$$

其中，宏观[反应速率](@entry_id:139813) $\alpha_r(c)$ 与微观[倾向函数](@entry_id:181123) $a_r(x)$ 的关系通过系统体积 $\Omega$ 进行尺度变换得到 ：

$$
\alpha_r(c) = \frac{a_r(\Omega c)}{\Omega}
$$

这个关系确保了从微观的、基于分子计数的随机模型到宏观的、基于浓度的确定性模型的平滑过渡。例如，对于一个[双分子反应](@entry_id:165027) $X_1 + X_2 \to \dots$，其[倾向函数](@entry_id:181123)通常定义为 $a_r(x) = k \frac{x_1 x_2}{\Omega}$。根据上述尺度关系，其宏观速率为 $\alpha_r(c) = \frac{1}{\Omega} \left( k \frac{(\Omega c_1)(\Omega c_2)}{\Omega} \right) = k c_1 c_2$，这正是我们熟悉的[质量作用定律](@entry_id:144659)表达式。

### 系统尺寸展开：分解均值与涨落

[反应速率](@entry_id:139813)方程描述了系统的平均行为，但完全忽略了噪声。为了在保留确定性描述的同时分析噪声的特性，荷兰物理学家 Nicolaas van Kampen 提出了**系统尺寸展开**（system-size expansion）方法。其核心思想是将系统的状态变量分解为一个宏观的确定性部分和一个较小的随机涨落部分。

该方法基于两个物理洞察 ：
1.  分子数量 $x(t)$ 是一个**广延量**（extensive quantity），它与系统尺寸 $\Omega$（如体积）成正比。相反，浓度 $c(t) = x(t)/\Omega$ 是一个**强度量**（intensive quantity），在宏观极限下应与系统尺寸无关。
2.  [化学反应](@entry_id:146973)作为独立的随机事件，其统计特性类似于泊松过程。对于大量的事件，根据中心极限定理，涨落的[标准差](@entry_id:153618)与平均事件数的平方根成正比。由于平均分子数与 $\Omega$ 成正比，即 $O(\Omega)$，其涨落的[标准差](@entry_id:153618)应与 $\Omega^{1/2}$ 成正比，即 $O(\Omega^{1/2})$。

基于这些原则，van Kampen 提出了如下的**展开拟设**（ansatz）：

$$
x(t) = \Omega\phi(t) + \Omega^{1/2}\xi(t)
$$

在这个表达式中：
- $\Omega$ 是系统尺寸参数，是一个大的[无量纲数](@entry_id:136814)或具有体积量纲的量。
- $\phi(t)$ 是一个与浓度量纲相同的确定性向量，描述了系统的宏观行为。它正是由上一节讨论的[反应速率](@entry_id:139813)方程所决定的轨迹。
- $\xi(t)$ 是一个量级为 $O(1)$ 的[随机变量](@entry_id:195330)，代表了围绕宏观轨迹的**标准化涨落**。

这个[拟设](@entry_id:184384)巧妙地将涨落的[尺度分离](@entry_id:270204)出来。$x(t)$ 的均值主要由 $\Omega\phi(t)$ 贡献，为 $O(\Omega)$。$x(t)$ 的[方差](@entry_id:200758)则由 $\Omega^{1/2}\xi(t)$ 贡献：

$$
\mathrm{Var}[x(t)] = \mathrm{Var}[\Omega\phi(t) + \Omega^{1/2}\xi(t)] = \mathrm{Var}[\Omega^{1/2}\xi(t)] = \Omega \mathrm{Var}[\xi(t)]
$$

由于 $\xi(t)$ 的量级为 $O(1)$，其[方差](@entry_id:200758) $\mathrm{Var}[\xi(t)]$ 也是 $O(1)$。因此，分子数 $x(t)$ 的[方差](@entry_id:200758)是 $O(\Omega)$，标准差是 $O(\Omega^{1/2})$，这与我们的物理直觉完全一致。通过这种方式，van Kampen 的展开将[随机动力学](@entry_id:187867)问题转化为研究一个量级为一的涨落变量 $\xi(t)$ 的动力学问题。

### [线性噪声近似](@entry_id:190628)：涨落的动力学

将 van Kampen 展开拟设代入[化学主方程](@entry_id:161378)，并对[倾向函数](@entry_id:181123)和[概率分布](@entry_id:146404)进行[泰勒展开](@entry_id:145057)，然后按照 $\Omega^{-1/2}$ 的幂次整理方程，我们可以得到一个关于涨落变量 $\xi(t)$ 的动力学方程。在系统尺寸展开中，保留到 $\Omega^0$ 阶的项，便得到了**[线性噪声近似](@entry_id:190628)**（Linear Noise Approximation, [LNA](@entry_id:150014)）。

[LNA](@entry_id:150014) 的核心结论是，围绕确定性轨迹 $\phi(t)$ 的涨落 $\xi(t)$ 的动力学可以用一个线性的**福克-普朗克方程**（[Fokker-Planck](@entry_id:635508) Equation, FPE）来描述 ：

$$
\frac{\partial p(\xi, t)}{\partial t} = - \sum_{i,j} \frac{\partial}{\partial \xi_i} [A_{ij}(t) \xi_j p(\xi, t)] + \frac{1}{2} \sum_{i,j} \frac{\partial^2}{\partial \xi_i \partial \xi_j} [D_{ij}(t) p(\xi, t)]
$$

其中 $p(\xi, t)$ 是涨落变量 $\xi$ 在时刻 $t$ 的概率密度函数。这个方程等价于一个线性的**[随机微分方程](@entry_id:146618)**（Stochastic Differential Equation, SDE），也称为**郎之万方程**（Langevin equation）：

$$
\mathrm{d}\xi(t) = A(\phi(t))\xi(t)\mathrm{d}t + \sqrt{D(\phi(t))}\mathrm{d}W(t)
$$

这里的 $\mathrm{d}W(t)$ 是一个标准[维纳过程](@entry_id:137696)（[高斯白噪声](@entry_id:749762)）的增量。这个方程描述了一个**[奥恩斯坦-乌伦贝克过程](@entry_id:140047)**（Ornstein-Uhlenbeck process）。

从这个方程的结构，我们可以立即得出关于涨落的两个重要性质 ：
1.  **涨落是高斯的**：由[高斯白噪声](@entry_id:749762)驱动的线性SDE的解是一个高斯过程。因此，[LNA](@entry_id:150014) 预测分子数量的[分布](@entry_id:182848)（在变换到 $\xi$ 变量后）是一个多元高斯分布。
2.  **涨落的均值为零**：对上述SDE取期望，并利用 $\mathbb{E}[\mathrm{d}W(t)]=0$，我们得到涨落均值 $\langle\xi(t)\rangle$ 的[演化方程](@entry_id:268137)：$\frac{\mathrm{d}\langle\xi(t)\rangle}{\mathrm{d}t} = A(t)\langle\xi(t)\rangle$。如果系统初始时没有涨落（或涨落均值为零），即 $\langle\xi(0)\rangle=0$，那么对于所有 $t>0$，其解都将是 $\langle\xi(t)\rangle=0$。这意味着涨落是对称地[分布](@entry_id:182848)在宏观轨迹 $\phi(t)$ 周围的。

方程中的两个关键矩阵 $A(\phi)$ 和 $D(\phi)$ 分别为：
- **漂移矩阵**（Drift Matrix）$A(\phi)$：也称为**[雅可比矩阵](@entry_id:264467)**（Jacobian matrix），它描述了涨落如何被确[定性动力学](@entry_id:263136)“[拉回](@entry_id:160816)”到宏观轨迹。它由宏观速率向量场 $F(\phi) = S f(\phi)$ （其中 $S$ 是化学计量矩阵，$f(\phi)$ 是宏观速率向量）对浓度 $\phi$求偏导得到：
  $$
  A(\phi) = \frac{\partial F(\phi)}{\partial \phi}
  $$
  对于包含[非线性](@entry_id:637147)反应（如[双分子反应](@entry_id:165027)）的系统，[雅可比矩阵](@entry_id:264467) $A$ 将依赖于系统的状态 $\phi$。例如，在一个包含反应 $X_1 + X_2 \to X_3$ 的系统中，其宏观速率为 $k_1 \phi_1 \phi_2$，这是一个[非线性](@entry_id:637147)项。这导致[雅可比矩阵](@entry_id:264467)的元素中包含 $\phi_1$ 和 $\phi_2$ 等状态变量，使得漂移项是状态依赖的 。

- **[扩散矩阵](@entry_id:182965)**（Diffusion Matrix）$D(\phi)$：它量化了由离散的[化学反应](@entry_id:146973)事件产生的内在噪声的强度。它由化学计量矩阵 $S$ 和宏观[反应速率](@entry_id:139813) $f(\phi)$ 共同决定：
  $$
  D(\phi) = S \cdot \mathrm{diag}(f(\phi)) \cdot S^\top
  $$
  其中 $\mathrm{diag}(f(\phi))$ 是一个[对角矩阵](@entry_id:637782)，其对角元为各个反应的宏观速率。这个形式反映了各个反应事件作为独立的泊松过程对噪声的贡献。例如，对于一个消耗两个分子的反应（[化学计量](@entry_id:137450)为-2），它对[扩散矩阵](@entry_id:182965)的贡献将与 $(-2)^2=4$ 和该反应的速率成正比，这显示了反应的分子数变化如何影响噪声的幅度 。

### [线性噪声近似](@entry_id:190628)下的[矩动力学](@entry_id:752137)

[LNA](@entry_id:150014) 最强大的应用之一是它能够为系统涨落的[统计矩](@entry_id:268545)（特别是均值和协[方差](@entry_id:200758)）提供一组封闭的常微分方程。

根据 van Kampen 展开[拟设](@entry_id:184384) $x(t) = \Omega\phi(t) + \Omega^{1/2}\xi(t)$，我们可以计算分子数 $x(t)$ 的均值和协[方差](@entry_id:200758)。
- **均值动力学**：
  $$
  \mathbb{E}[x(t)] = \mathbb{E}[\Omega\phi(t) + \Omega^{1/2}\xi(t)] = \Omega\phi(t) + \Omega^{1/2}\mathbb{E}[\xi(t)]
  $$
  由于 $\mathbb{E}[\xi(t)] = 0$，我们得到 $\mathbb{E}[x(t)] = \Omega\phi(t)$。对其求时间导数，并利用宏观方程 $\frac{\mathrm{d}\phi}{\mathrm{d}t} = S f(\phi)$，可得均值的[演化方程](@entry_id:268137) ：
  $$
  \frac{\mathrm{d}}{\mathrm{d}t}\mathbb{E}[x(t)] = \Omega \frac{\mathrm{d}\phi(t)}{\mathrm{d}t} = \Omega S f(\phi(t))
  $$

- **协[方差](@entry_id:200758)动力学**：
  分子数的协方差矩阵为：
  $$
  \mathrm{Cov}(x(t)) = \mathrm{Cov}(\Omega\phi(t) + \Omega^{1/2}\xi(t)) = \Omega \mathrm{Cov}(\xi(t)) = \Omega \Sigma(t)
  $$
  其中 $\Sigma(t) = \mathrm{Cov}(\xi(t))$ 是[标准化](@entry_id:637219)涨落 $\xi$ 的[协方差矩阵](@entry_id:139155)。利用 [LNA](@entry_id:150014) 的 SDE，可以推导出 $\Sigma(t)$ 满足的**李雅普诺夫[微分方程](@entry_id:264184)**（Lyapunov differential equation）：
  $$
  \frac{\mathrm{d}\Sigma(t)}{\mathrm{d}t} = A(\phi(t))\Sigma(t) + \Sigma(t)A(\phi(t))^\top + D(\phi(t))
  $$

这组方程构成了[矩动力学](@entry_id:752137)的核心。它们允许我们直接计算均值和协[方差](@entry_id:200758)随时间的演化，而无需解复杂的[化学主方程](@entry_id:161378)。

#### 应用示例1：一个简单的[生灭过程](@entry_id:168595)

为了具体理解 [LNA](@entry_id:150014) 的应用，我们考虑一个简单的[生灭过程](@entry_id:168595)：$\emptyset \xrightarrow{\alpha} X$ 和 $X \xrightarrow{k} \emptyset$。其[倾向函数](@entry_id:181123)分别为 $a_1(n) = \alpha\Omega$ 和 $a_2(n) = kn$ 。
1.  **宏观方程**：$\frac{\mathrm{d}\phi}{\mathrm{d}t} = \alpha - k\phi$。其[稳态解](@entry_id:200351)为 $\phi^* = \alpha/k$。
2.  **[LNA](@entry_id:150014) 参数**：雅可比矩阵（这里是标量）为 $A(\phi) = \frac{\mathrm{d}}{\mathrm{d}\phi}(\alpha - k\phi) = -k$。[扩散](@entry_id:141445)项为 $D(\phi) = (+1)^2(\alpha) + (-1)^2(k\phi) = \alpha + k\phi$。在[稳态](@entry_id:182458)时，$D(\phi^*) = \alpha + k(\alpha/k) = 2\alpha$。
3.  **[稳态](@entry_id:182458)[方差](@entry_id:200758)**：在[稳态](@entry_id:182458)下，[李雅普诺夫方程](@entry_id:165178)变为一个[代数方程](@entry_id:272665)：$A\Sigma + \Sigma A^\top + D = 0$。对于这个单变量系统，即 $2A\Sigma + D = 0$。代入[稳态](@entry_id:182458)值：$2(-k)\Sigma_{ss} + 2\alpha = 0$，解得[标准化](@entry_id:637219)涨落的[方差](@entry_id:200758)为 $\Sigma_{ss} = \alpha/k$。
4.  **分子数[方差](@entry_id:200758)**：[稳态](@entry_id:182458)分子数的[方差](@entry_id:200758)为 $\mathrm{Var}(n)_{ss} = \Omega \Sigma_{ss} = \Omega \alpha/k$。这个结果恰好与均值为 $\langle n \rangle = \Omega \phi^* = \Omega \alpha/k$ 的[泊松分布](@entry_id:147769)的[方差](@entry_id:200758)完全相同，这证实了对于这个线性系统，[LNA](@entry_id:150014) 给出了精确的[稳态](@entry_id:182458)结果。

#### 应用示例2：[稳态](@entry_id:182458)协[方差](@entry_id:200758)的计算

对于更复杂的系统，求解[稳态](@entry_id:182458)时的代数[李雅普诺夫方程](@entry_id:165178) $A\Sigma + \Sigma A^\top + D = 0$ 是 [LNA](@entry_id:150014) 的一个核心应用。这通常涉及到一个线性方程组的求解。考虑一个简单的信号通路模型，其中包含物种 $R$ 和 $S$ 。通过计算[稳态](@entry_id:182458)点 $\phi^*$、[雅可比矩阵](@entry_id:264467) $A(\phi^*)$ 和[扩散矩阵](@entry_id:182965) $D(\phi^*)$，然后代入上述[李雅普诺夫方程](@entry_id:165178)，就可以解出[稳态](@entry_id:182458)[协方差矩阵](@entry_id:139155) $\Sigma$ 的所有元素，包括物种 $S$ 的[方差](@entry_id:200758) $\Sigma_{SS}$ 和 $R$ 与 $S$ 之间的协[方差](@entry_id:200758) $\Sigma_{RS}$。这个过程展示了 [LNA](@entry_id:150014) 如何被用来预测[基因表达噪声](@entry_id:160943)或信号传导通路中不同组分之间涨落的相关性。

#### 应用示例3：时变协[方差](@entry_id:200758)的计算

[LNA](@entry_id:150014) 不仅限于[稳态分析](@entry_id:271474)。李雅普诺夫[微分方程](@entry_id:264184)描述了协方差矩阵如何随[时间演化](@entry_id:153943)。对于一个常数 $A$ 和 $D$（例如，在[稳定不动点](@entry_id:262720)附近），该方程的解可以写成解析形式 ：

$$
\Sigma(t) = e^{At}\Sigma(0)e^{A^{\top}t} + \int_0^t e^{A(t-s)} D e^{A^{\top}(t-s)} \mathrm{d}s
$$

其中 $e^{At}$ 是矩阵指数。这个公式描述了协[方差](@entry_id:200758)如何从初始状态 $\Sigma(0)$ 演化到其最终的[稳态](@entry_id:182458)值。第一项代表初始协[方差](@entry_id:200758)的衰减，第二项代表由系统内在噪声不断产生的新的协[方差](@entry_id:200758)。通过计算这个积分，我们可以精确地追踪例如两种蛋白质之间涨落相关性随时间的变化，这对于理解动态系统（如对刺激的响应）中的[噪声传播](@entry_id:266175)至关重要。

### [线性噪声近似](@entry_id:190628)的有效性与局限性

尽管 [LNA](@entry_id:150014) 是一个强大的工具，但它是一个近似方法，有其明确的[适用范围](@entry_id:636189)和失效条件。理解这些局限性对于正确应用该理论至关重要。

[LNA](@entry_id:150014) 的有效性基于系统尺寸展开的截断，其基本假设是涨落项 $\Omega^{1/2}\xi(t)$ 远小于宏观项 $\Omega\phi(t)$。这要求涨落 $\xi(t)$ 保持小。这一假设在以下情况下可能会失效  ：
1.  **小系统尺寸（低分子数）**：[LNA](@entry_id:150014) 是一个在 $\Omega \to \infty$ 极限下的[渐近展开](@entry_id:173196)。当 $\Omega$ 很小（例如，分子数只有个位数）时，被忽略的高阶项变得显著，离散的分子特性和非高斯涨落变得重要，[LNA](@entry_id:150014) 就会失效。
2.  **接近[分岔点](@entry_id:187394)**：在分岔点附近，系统的稳定性变弱。这体现在[雅可比矩阵](@entry_id:264467) $A$ 的某个或某些[特征值](@entry_id:154894)的实部趋近于零。系统的最慢[弛豫率](@entry_id:150136) $\lambda_{\text{relax}} = \min(-\Re\lambda_i(A))$ 趋于零。这会导致线性恢复力变得非常弱，涨落的[方差](@entry_id:200758) $\Sigma$（大致与 $1/\lambda_{\text{relax}}$ 成比例）会急剧增大。大的涨落会使得系统状态探索到动力学[非线性](@entry_id:637147)的区域，从而使线性近似失效。
3.  **强[非线性](@entry_id:637147)**：即使系统远离分岔点，如果宏观[速率函数](@entry_id:154177) $f(\phi)$ 的曲率（由其**海森矩阵** $H_f$ 描述）很大，那么即使是中等程度的涨落也可能感受到显著的[非线性](@entry_id:637147)效应，导致 [LNA](@entry_id:150014) 失效。我们可以通过比较[非线性](@entry_id:637147)项和线性项的大小来量化这一点，从而得到一个失效判据。

#### [多稳态](@entry_id:180390)系统中的失效

[LNA](@entry_id:150014) 最显著的局限性之一是在处理具有多个稳定状态的系统（如**[双稳态开关](@entry_id:190716)**）时。[LNA](@entry_id:150014) 是一个**局域**近似，它只能描述在**单个**[稳定不动点](@entry_id:262720)附近的涨落，并给出一个单峰的[高斯分布](@entry_id:154414)。然而，一个双稳态系统的真实[概率分布](@entry_id:146404)是双峰的，每个峰对应一个稳定状态。

噪声可以驱动系统在两个稳定状态之间进行[随机切换](@entry_id:197998)。这种切换是一种**稀有事件**，它依赖于系统跨越一个由[鞍点](@entry_id:142576)分隔的势垒。[LNA](@entry_id:150014) 完全无法描述这种非局域的、大尺度的跃迁过程。它的数学结构（一个二次[势阱](@entry_id:151413)）决定了它看不到势垒和另一个稳定状态的存在 。因此，[LNA](@entry_id:150014) 不能用来计算状态间的切换速率。

#### 超越 [LNA](@entry_id:150014)：WKB 近似

要描述双稳态系统中的切换等稀有事件，需要更高级的理论，如**[WKB近似](@entry_id:756741)**（也称为[大偏差理论](@entry_id:273365)）。与 [LNA](@entry_id:150014) 关注小而频繁的涨落不同，WKB 方法旨在计算大而稀有的涨落的概率。

WKB 方法采用另一种形式的[概率分布](@entry_id:146404)拟设，$P(x) \sim \exp(-\Omega S(x))$，其中 $S(x)$ 被称为**作用量**或**[准势](@entry_id:196547)**。将此拟设代入[化学主方程](@entry_id:161378)，可以得到一个关于 $S(x)$ 的[哈密顿-雅可比方程](@entry_id:145701)。两个稳定状态之间的切换速率 $k$ 主要由它们之间的作用量差（即势垒高度）$\Delta S$ 决定，其形式为 $k \sim \exp(-\Omega \Delta S)$ 。这种方法能够正确捕捉到切换速率随系统尺寸 $\Omega$ 呈指数减小的依赖关系，这是 [LNA](@entry_id:150014) 完全无法做到的。

总之，[LNA](@entry_id:150014) 是一个用于分析[稳定系统](@entry_id:180404)周围小涨落的有效工具，它为[矩动力学](@entry_id:752137)提供了简洁的描述。然而，对于分子数极少、接近不[稳定点](@entry_id:136617)或具有多个稳定状态的系统，[LNA](@entry_id:150014) 的预测可能会严重偏离实际，此时需要采用[化学主方程](@entry_id:161378)的直接模拟或更高级的理论方法。