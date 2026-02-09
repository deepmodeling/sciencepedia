## 引言
在深度学习领域，我们不断追求构建能够理解和生成复杂数据的模型，而这一切的核心都离不开一个根本性的数学语言——概率论。概率质量函数（PMF）与概率密度函数（PDF）正是这门语言的基石，它们不仅用于描述模型输出，更是量化不确定性、定义学习目标和构建高级生成模型的关键。然而，许多实践者仅停留在应用层面，对“为何使用交叉熵损失？”或“GAN与VAE在概率建模上有何本质区别？”等问题缺乏深刻理解。本文旨在填补这一知识鸿沟。我们将系统性地剖析PMF和PDF在现代深度学习中的角色，帮助你从第一性原理出发，建立坚实的理论根基。在接下来的章节中，我们将首先在“原理与机制”中深入探讨这些概率函数如何与神经网络的架构和损失函数设计紧密相连；随后，在“应用与跨学科联系”中，我们将展示这些理论在不确定性量化、模型校准和强化学习等领域的实际应用；最后，通过“动手实践”，你将有机会亲手实现和验证这些核心概念，将理论知识转化为实践能力。

## 原理与机制

在深度学习中，概率分布是描述模型输出和量化不确定性的核心语言。无论是处理分类任务中的离散标签，还是生成模型中的连续数据，概率质量函数（Probability Mass Functions, PMFs）和概率密度函数（Probability Density Functions, PDFs）都为我们提供了严谨的数学框架。本章将深入探讨这些基本概念在深度学习模型中的应用原理和关键机制。

### 使用概率质量函数建模离散结果

在分类问题中，模型的目标是为每个输入预测一个类别标签。这本质上是为一组离散的、互斥的结果分配概率。概率质量函数（PMF）是描述这种离散型随机变量分布的数学工具。

#### 概率质量函数与指数族

一个典型的分类任务是二元分类，其结果可以用伯努利（Bernoulli）分布来描述。一个随机变量 $Y$ 服从参数为 $p$ 的伯努利分布，其PMF为：
$$
P(Y=y) = p^y(1-p)^{1-y}, \quad \text{for } y \in \{0, 1\}
$$
其中 $p$ 代表“成功”（即 $y=1$）的概率。在广义线性模型（GLMs）和现代深度学习的框架中，将此PMF重写为**指数族（exponential family）**的标准形式具有重要意义。指数族的标准形式为：
$$
f(y|\theta) = h(y) \exp(y\theta - b(\theta))
$$
这里，$\theta$ 被称为**自然参数（natural parameter）**。

为了将伯努利PMF转换为这种形式，我们对其进行代数变换 [@problem_id:1930959]：
$$
\begin{align*}
p^y(1-p)^{1-y}  = \exp\left( \ln\left( p^y(1-p)^{1-y} \right) \right) \\
 = \exp\left( y \ln(p) + (1-y) \ln(1-p) \right) \\
 = \exp\left( y \ln(p) - y \ln(1-p) + \ln(1-p) \right) \\
 = \exp\left( y \ln\left(\frac{p}{1-p}\right) + \ln(1-p) \right)
\end{align*}
$$
通过与指数族的标准形式对比，我们可以识别出自然参数 $\theta$：
$$
\theta = \ln\left(\frac{p}{1-p}\right)
$$
这个函数被称为**logit**函数。在神经网络中，未经激活的原始输出值通常被称为**logits**，这个推导为其提供了理论依据：模型的原始输出可以直接建模自然参数。

此外，我们还可以解出 $p$ 与 $\theta$ 的关系，得到 $p = \frac{\exp(\theta)}{1+\exp(\theta)}$，这正是**sigmoid**函数。因此，$\ln(1-p) = -\ln(1+\exp(\theta))$。这使得我们可以确定指数族形式中的 $b(\theta) = \ln(1+\exp(\theta))$。

在GLM理论中，将分布的均值 $\mu = E[Y]$ 与自然参数 $\theta$ 直接关联的函数 $g(\mu) = \theta$ 被称为**典范连接函数（canonical link function）**。对于伯努利分布，其均值为 $\mu = E[Y] = p$。因此，其典范连接函数正是logit函数：
$$
g(\mu) = \ln\left(\frac{\mu}{1-\mu}\right)
$$
这一发现解释了为什么在二元分类模型（如逻辑回归）中，我们通常使用一个线性模型来预测logit值，然后通过sigmoid函数将其转换为概率。

#### 从对数几率到概率：Softmax变换

对于具有 $K$ 个类别的多分类问题，伯努利分布被推广为类别（Categorical）分布。类似地，logit/sigmoid的组合也被推广。模型的神经网络部分输出一个 $K$ 维的logit向量 $\mathbf{z} = [z_0, z_1, \dots, z_{K-1}]$，然后通过**softmax**函数将其转换为一个合法的PMF，即一个概率分布向量 $\mathbf{p}$：
$$
p_i = \frac{\exp(z_i)}{\sum_{j=0}^{K-1} \exp(z_j)}
$$
$p_i$ 表示模型预测为类别 $i$ 的概率，满足 $p_i \ge 0$ 且 $\sum_i p_i = 1$。

我们可以从统计物理学的角度更深入地理解softmax函数 [@problem_id:3166229]。在物理学中，一个处于热平衡状态的系统在不同能量状态 $E_i$ 的概率分布由**吉布斯分布（Gibbs distribution）**给出：
$$
p_i \propto \exp(-\beta E_i)
$$
其中 $\beta$ 是与系统温度相关的**逆温度（inverse temperature）**参数。如果我们将模型的logits $z_i$ 解释为对应状态的**负能量**，即 $E_i = -z_i$，那么softmax函数就完全等价于一个带有温度参数的吉布斯分布：
$$
p_i(\beta) = \frac{\exp(\beta z_i)}{\sum_{j=0}^{K-1} \exp(\beta z_j)}
$$
标准softmax函数对应于 $\beta=1$ 的情况。这个参数 $\beta$ 极大地影响着模型预测的置信度。
*   当 $\beta \to 0$（高温极限）时，所有 $\exp(\beta z_i)$ 都趋近于1，PMF变成一个均匀分布 $p_i = 1/K$。此时，模型的不确定性最大，其**香农熵（Shannon entropy）** $H(\mathbf{p}) = -\sum_i p_i \ln p_i$ 达到最大值 $\ln(K)$。
*   当 $\beta \to \infty$（低温极限）时，$\exp(\beta z_i)$ 项将被具有最大logit值的项完全主导。概率质量将集中在最可能的类别上，PMF趋近于一个**one-hot**向量。此时，模型的不确定性最小，熵趋近于0。

通过调整 $\beta$，我们可以在模型的准确性（倾向于选择最可能的类别）和不确定性（保留对其他可能类别的概率）之间进行权衡。例如，在探索性任务中，较低的 $\beta$ 值可以鼓励模型生成更多样化的预测。

#### 评估与训练：恰当评分规则

选择损失函数是训练深度学习模型的关键一步。对于分类任务，最常用的损失函数是**交叉熵（cross-entropy）**，它等价于**负对数似然（negative log-likelihood）**。其优秀的性能并非偶然，而是源于一个深刻的统计学性质：它是一个**恰当评分规则（proper scoring rule）**。

给定一个真实的条件PMF $q(\cdot|x)$ 和模型预测的PMF $p(\cdot|x)$，一个评分规则 $s(p, y)$（其中 $y$ 是观测到的标签）如果在其期望值 $\mathbb{E}_{Y \sim q}[s(p, Y)]$ 在 $p=q$ 时达到最小值，则称其为**恰当的（proper）**。如果 $p=q$是唯一的最小值点，则称其为**严格恰当的（strictly proper）** [@problem_id:3166214]。

我们来分析两个常用的评分规则：
1.  **对数分数（Log Score）**：$s_{\log}(p, y) = -\ln p_y$。其期望值为：
    $$
    \mathbb{E}_{Y \sim q}[s_{\log}(p, Y)] = -\sum_{k=1}^K q_k \ln p_k
    $$
    这正是 $q$ 和 $p$ 之间的交叉熵。这个值可以通过引入KL散度 $D_{KL}(q \| p)$ 来分析。由于 $D_{KL}(q \| p) = \sum q_k \ln(q_k/p_k) = \sum q_k \ln q_k - \sum q_k \ln p_k \ge 0$，且仅在 $p=q$ 时等号成立，因此交叉熵在 $p=q$ 时取得唯一最小值。所以，对数分数是严格恰当的。

2.  **布里尔分数（Brier Score）**：$s_{\mathrm{Br}}(p, y) = \sum_{k=1}^K (p_k - \mathbb{1}\{k=y\})^2$。其期望值为：
    $$
    \begin{align*}
    \mathbb{E}_{Y \sim q}[s_{\mathrm{Br}}(p, Y)]  = \sum_{y=1}^K q_y \sum_{k=1}^K (p_k - \mathbb{1}\{k=y\})^2 \\
     = \sum_{k=1}^K (p_k - q_k)^2 + \left(1 - \sum_{k=1}^K q_k^2\right)
    \end{align*}
    $$
    由于第二项与 $p$ 无关，最小化期望布里尔分数等价于最小化 $p$ 和 $q$ 之间的平方欧氏距离 $\sum_k (p_k - q_k)^2$。这个距离的唯一最小值在 $p=q$ 时取到，为0。因此，布里尔分数也是严格恰当的。

严格恰当性是损失函数设计的黄金标准。它确保了当模型有足够的能力并且数据量足够大时，最小化损失函数的优化过程会激励模型学习真实的条件概率分布 $q(y|x)$。一个预测其PMF等于真实PMF的模型，被称为是**良好校准的（well-calibrated）**。因此，使用交叉熵等严格恰当的损失函数是训练能够提供可靠概率估计的深度学习模型的理论基础。

### 使用概率密度函数建模连续结果

当目标变量是连续的（例如，物体的价格、图像的像素强度），我们使用概率密度函数（PDF）来描述其分布。深度学习模型不再是输出一个概率向量，而是输出一个参数化的PDF的参数。

#### 概率回归：超越点估计

传统的回归任务通常最小化**均方误差（Mean Squared Error, MSE）**，这等价于只预测目标变量的条件均值。然而，这忽略了预测中的不确定性。一个更强大的方法是进行**概率回归（probabilistic regression）**，即预测目标变量的完整条件分布 $p(y|x)$。

最常见的选择是高斯（正态）分布，其PDF由均值 $\mu$ 和标准差 $\sigma$ (或方差 $\sigma^2$) 参数化：
$$
p(y | \mu, \sigma) = \frac{1}{\sqrt{2\pi}\sigma} \exp\left(-\frac{(y - \mu)^2}{2\sigma^2}\right)
$$
为了训练一个预测此分布的模型，我们使用**最大似然估计（Maximum Likelihood Estimation, MLE）**，这等价于最小化**负对数似然（Negative Log-Likelihood, NLL）**损失。对于单个数据点 $(x_i, y_i)$，NLL为 [@problem_id:3166259]：
$$
\mathcal{L}_{\text{NLL}}(y_i, \mu_\theta(x_i), \sigma_\theta(x_i)) = \frac{1}{2}\log(2\pi) + \log(\sigma_\theta(x_i)) + \frac{(y_i - \mu_\theta(x_i))^2}{2\sigma_\theta(x_i)^2}
$$
其中，$\mu_\theta(x_i)$ 和 $\sigma_\theta(x_i)$ 是由神经网络（参数为 $\theta$）为输入 $x_i$ 预测的均值和标准差。

将此NLL损失与MSE进行比较，我们发现：如果假设 $\sigma_\theta(x)$ 是一个与输入无关的常数 $\sigma_{const}$，则NLL损失简化为：
$$
\mathcal{L}_{\text{NLL}} = \text{const} + \frac{1}{2\sigma_{const}^2} \sum_{i=1}^N (y_i - \mu_\theta(x_i))^2
$$
最小化这个表达式等价于最小化MSE。因此，**MSE是高斯NLL损失在噪声方差恒定（同方差性，homoscedasticity）假设下的一个特例**。

然而，在许多现实场景中，数据表现出**异方差性（heteroscedasticity）**，即噪声的方差随输入 $x$ 的变化而变化。例如，在某个输入区域，预测可能比其他区域更不确定。在这种情况下，MSE模型由于其固定的方差假设而表现不佳。相比之下，一个通过最小化NLL训练的、能够同时预测 $\mu_\theta(x)$ 和 $\sigma_\theta(x)$ 的模型，可以学习到这种依赖于输入的方差结构，从而提供更准确的概率预测和更可靠的不确定性估计 [@problem_id:3166259]。

#### 对数配分函数与矩生成

许多重要的概率分布，包括高斯分布和伯努利分布，都属于更广泛的指数族。对于单参数指数族，其PDF或PMF可以写为：
$$
p(x|\eta) = h(x) \exp(\eta T(x) - A(\eta))
$$
其中 $\eta$ 是自然参数，$T(x)$ 是**充分统计量（sufficient statistic）**，$A(\eta)$ 是**对数配分函数（log-partition function）**，它确保分布的积分为1。

$A(\eta)$ 具有一个非凡的性质：它的导数可以生成充分统计量 $T(X)$ 的矩（moments）[@problem_id:1623445]。通过对归一化条件 $\int p(x|\eta) dx = 1$ 进行微分，可以证明：
*   $A'(\eta) = \frac{d A(\eta)}{d \eta} = \mathbb{E}_{\eta}[T(X)]$
*   $A''(\eta) = \frac{d^2 A(\eta)}{d \eta^2} = \mathbb{E}_{\eta}[T(X)^2] - (\mathbb{E}_{\eta}[T(X)])^2 = \text{Var}_{\eta}[T(X)]$

即，对数配分函数的一阶导数是充分统计量的期望值，二阶导数是其方差。这个优雅的结论统一了许多分布的矩计算，并揭示了指数族分布深刻的内在结构。

### 复杂高维概率密度函数的建模

在图像、音频和文本等高维数据的生成建模中，我们需要能够表示极其复杂和多模态的概率密度函数。深度学习通过几种不同的范式来应对这一挑战。

#### 基于变量变换的显式密度模型

这类模型的核心思想是，从一个简单的基础分布（如标准正态分布）开始，通过一个可逆的、可微的变换将其“扭曲”成一个复杂的分布。这依赖于概率论中的**变量变换公式**。如果一个随机向量 $\mathbf{z} \sim p_Z(\mathbf{z})$ 通过一个可逆函数 $\mathbf{x} = f(\mathbf{z})$ 变换，那么新向量 $\mathbf{x}$ 的PDF为：
$$
p_X(\mathbf{x}) = p_Z(f^{-1}(\mathbf{x})) \cdot \left| \det J_{f^{-1}}(\mathbf{x}) \right|
$$
等价地，其对数形式为 $\log p_X(\mathbf{x}) = \log p_Z(\mathbf{z}) - \log |\det J_f(\mathbf{z})|$，其中 $J_f$ 是变换 $f$ 的雅可比矩阵。

**归一化流（Normalizing Flows）**模型就是基于这一原理构建的，它将一系列可逆变换 $f_1, f_2, \dots, f_K$ 串联起来。为了使模型实用，$\log |\det J_f|$ 的计算必须高效。直接计算一个 $d \times d$ 矩阵的行列式通常需要 $O(d^3)$ 的计算复杂度，这对于高维数据是不可接受的。

因此，归一化流的设计关键在于构造具有易于计算的雅可比行列式的变换。一个典型的例子是**仿射耦合层（affine coupling layer）**[@problem_id:3166273]。这种层将输入维度划分为两部分 $\mathbf{x}_A$ 和 $\mathbf{x}_B$。一部分保持不变，另一部分则根据第一部分进行仿射变换：
$$
\mathbf{y}_A = \mathbf{x}_A
$$
$$
\mathbf{y}_B = \mathbf{x}_B \odot \exp(s(\mathbf{x}_A)) + t(\mathbf{x}_A)
$$
其中 $s$ 和 $t$ 是由神经网络计算的缩放和平移函数。这个变换的雅可比矩阵具有块三角结构，其行列式可以被证明恰好是缩放项的指数和：
$$
\det J_f(\mathbf{x}) = \exp\left( \sum_i (s(\mathbf{x}_A))_i \right)
$$
因此，其对数行列式可以简单地通过对缩放网络的输出求和得到，计算复杂度为 $O(d)$。通过堆叠这类结构简单的层，归一化流能够构建出既灵活又具有可计算的精确似然的复杂模型。

#### 隐式密度模型：生成对抗网络

与归一化流不同，**生成对抗网络（Generative Adversarial Networks, GANs）**采用了一种**隐式（implicit）**的方式来定义概率分布 [@problem_id:3166194]。GAN的生成器 $G_\theta$ 是一个从低维潜空间（例如，$z \sim \mathcal{N}(0, I)$）到高维数据空间的映射 $\mathbf{x} = G_\theta(\mathbf{z})$。这个过程被称为**前推（pushforward）**，它在数据空间中诱导出模型分布 $p_\theta(\mathbf{x})$。

然而，我们通常无法写出 $p_\theta(\mathbf{x})$ 的显式PDF。其主要原因有二：
1.  **映射不可逆**：典型的GAN生成器是复杂的神经网络，通常不是一个可逆的双射函数。即使维度匹配（$m=n$），我们也无法计算 $G_\theta^{-1}(\mathbf{x})$ 或其雅可比行列式，因此无法使用变量变换公式。
2.  **维度不匹配**：在大多数应用中，潜变量维度 $m$ 远小于数据维度 $n$。这意味着生成器 $G_\theta$ 的输出被限制在一个位于 $\mathbb{R}^n$ 空间内的低维**流形（manifold）**上。这样的分布在整个 $\mathbb{R}^n$ 空间上是奇异的，其相对于标准的 $n$ 维勒贝格测度的密度函数不存在（或者说在流形之外处处为零，在流形上为无穷大）。

由于无法直接计算 $p_\theta(\mathbf{x})$，GANs无法通过最大似然进行训练。取而代之的是，GANs引入了一个**判别器（discriminator）** $D_\psi(\mathbf{x})$，其任务是区分真实数据和生成数据。理论可以证明，最优的判别器学习到了一个与**密度比（density ratio）** $p_{\text{data}}(\mathbf{x})/p_\theta(\mathbf{x})$ 相关的函数。例如，在标准的GAN中，最优判别器为 $D^*(\mathbf{x}) = \frac{p_{\text{data}}(\mathbf{x})}{p_{\text{data}}(\mathbf{x}) + p_\theta(\mathbf{x})}$。这个密度比为生成器的训练提供了梯度信号，而无需显式地计算任何一个密度。

#### 潜变量模型与变分推断

**变分自编码器（Variational Autoencoders, VAEs）**是另一类重要的生成模型。它假设数据 $x$ 是由一个不可观测的潜变量 $z$ 生成的，其联合概率为 $p(x, z) = p(x|z)p(z)$。我们希望最大化数据的边际对数似然 $\log p(x) = \log \int p(x|z)p(z) dz$。这个积分通常是难以计算的。

VAEs通过引入一个**近似后验（approximate posterior）**分布 $q_\phi(z|x)$ 来解决这个问题，并最大化**证据下界（Evidence Lower Bound, ELBO）**。利用**琴生不等式（Jensen's inequality）**，我们可以推导出这个下界 [@problem_id:3166279]：
$$
\begin{align*}
\log p(x)  = \log \int q_\phi(z|x) \frac{p(x,z)}{q_\phi(z|x)} dz \\
 \ge \int q_\phi(z|x) \log \frac{p(x,z)}{q_\phi(z|x)} dz \\
 = \mathbb{E}_{z \sim q_\phi(z|x)}[\log p(x|z)] - D_{KL}(q_\phi(z|x) \| p(z))
\end{align*}
$$
这个ELBO由两部分组成：第一项是**重构项**，它鼓励解码器 $p(x|z)$ 能够从潜变量中很好地重构数据；第二项是**KL散度正则项**，它迫使近似后验 $q_\phi(z|x)$ 接近于先验 $p(z)$。

ELBO的质量取决于近似后验 $q_\phi(z|x)$ 的灵活性。如果真实的后验分布 $p(z|x)$ 具有复杂的结构，而我们选择了一个过于简单的 $q_\phi$（例如，单峰的高斯分布），那么 $q_\phi$ 将无法完美匹配 $p(z|x)$。例如，在一个模型中，由于对称性，真实的后验 $p(z|x)$ 可能是**双峰的（bimodal）**。一个单峰的高斯 $q_\phi$ 只能捕捉其中一个峰，导致 $D_{KL}(q_\phi(z|x) \| p(z|x)) > 0$。这个KL散度正是 $\log p(x)$ 和ELBO之间的差距，被称为**变分差距（variational gap）**。这揭示了在变分推断中模型表达能力和计算可行性之间的根本权衡。

#### 未归一化密度模型：基于能量的模型

**基于能量的模型（Energy-Based Models, EBMs）**直接定义一个未归一化的PDF，形式为 $\tilde{p}_\theta(x) = \exp(-E_\theta(x))$，其中 $E_\theta(x)$ 是一个由神经网络计算的能量函数 [@problem_id:3166256]。归一化的PDF为 $p_\theta(x) = \tilde{p}_\theta(x) / \mathcal{Z}(\theta)$，其中**配分函数** $\mathcal{Z}(\theta) = \int \exp(-E_\theta(x)) dx$ 是一个通常难以计算的高维积分。

尽管 $\mathcal{Z}(\theta)$ 难以精确计算，但存在多种有原则的近似方法：
*   **重要性采样（Importance Sampling）**：从一个已知的、易于采样的提议分布 $q(x)$ 中采样，并通过加权平均来估计积分 $\mathcal{Z}(\theta) \approx \frac{1}{N} \sum_i \frac{\exp(-E_\theta(x_i))}{q(x_i)}$。
*   **拉普拉斯近似（Laplace Approximation）**：如果能量函数 $E_\theta(x)$ 在其最小值点 $x^\star$ 附近表现得像一个二次函数，我们可以用一个高斯分布来近似 $\exp(-E_\theta(x))$，从而得到 $\mathcal{Z}(\theta)$ 的解析近似解。
*   **退火重要性采样（Annealed Importance Sampling, AIS）**：这是一种更高级的蒙特卡洛方法，它通过构建一系列从简单分布到目标分布的“桥梁”分布，来稳健地估计配分函数的比值，并最终得到 $\mathcal{Z}(\theta)$ 的估计。

这些方法使得即使在配分函数未知的情况下，也能够对EBMs进行分析和训练。

#### 连接连续与离散：去量化似然

在许多实际应用中，例如对8位图像建模，数据本身是离散的（像素值在$\{0, \dots, 255\}$），但我们常常希望用一个连续的PDF模型来捕捉其潜在的生成过程。一个标准的技术是**去量化（dequantization）**。我们将一个离散值 $k$ 视为是从一个连续区间 $k\Delta, (k+1)\Delta)$ 中均匀采样得到的，其中 $\Delta$ 是量化区间的宽度。

在这种假设下，一个离散观测值 $k$ 在[连续模型 $p_c(y)$ 下的概率（即似然）是模型PDF在该区间上的积分：
$$
p_d(k) = \int_{k\Delta}^{(k+1)\Delta} p_c(y) dy
$$
训练模型时，我们最大化对数似然 $\log p_d(k)$。如果区间 $\Delta$ 很小，我们可以近似 $p_c(y)$ 在该区间内为常数 $p_c(k\Delta)$，得到 $\log p_d(k) \approx \log(p_c(k\Delta) \cdot \Delta) = \log p_c(k\Delta) + \log \Delta$。这解释了为什么在一些生成模型的实现中，损失函数看起来像是连续对数似然加上一个常数项。

更有趣的是，我们可以分析去量化模型下的**连续交叉熵**与离散模型下的**离散交叉熵**之间的关系 [@problem_id:3166250]。去量化模型对应的有效PDF是 $p_{\text{deq}}(y) = p_d(k) / \Delta$（对于 $y \in k\Delta, (k+1)\Delta)$）。可以证明，在真实数据[分布 $q_c(y)$ 下，连续交叉熵 $H_{\text{cont}}(q_c, p_{\text{deq}})$ 与离散交叉熵 $H_{\text{disc}}(q_d, p_d)$ 之间存在一个非常简洁的关系：
$$
H_{\text{cont}}(q_c, p_{\text{deq}}) = H_{\text{disc}}(q_d, p_d) + \log \Delta
$$
这个恒等式为在离散数据上使用连续密度模型提供了坚实的理论基础，并阐明了两种不同视角下的损失函数是如何关联的。