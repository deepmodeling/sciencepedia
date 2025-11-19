## 引言
在[李代数](@entry_id:137954)的宏伟殿堂中，[表示论](@entry_id:137998)是连接[抽象代数](@entry_id:145216)与具体物理世界的关键桥梁。然而，一旦构建了一个表示空间，我们如何在其内部进行探索，理解不同状态之间的关系？这个问题的答案在于[李代数表示论](@entry_id:190569)的动态核心——与根相关联的[升降算符](@entry_id:197899)。这些算符不仅是[代数结构](@entry_id:137052)的体现，更是操纵和理解[量子态](@entry_id:146142)、粒子态及其对称性的基本工具，其重要性贯穿了从基础量子力学到前沿[弦论](@entry_id:145688)的广阔领域。

本文旨在填补从知晓表示存在到掌握其内部运作之间的知识鸿沟。我们将系统性地揭示这些算符如何作为“阶梯”，让我们在[表示的权](@entry_id:204286)重空间中上下移动，以及如何通过精确的计算来量化这一过程。通过学习这些机制，读者将能从被动的观察者转变为主动的构建者，能够从第一性原理出发构造表示并计算其关键性质。

为了实现这一目标，本文将分为三个紧密相连的部分。在第一章 **“原理与机制”** 中，我们将深入剖析[升降算符](@entry_id:197899)的定义、代数关系以及作用于任意权重态的范数计算主公式。随后的第二章 **“应用与跨学科联系”** 将视野拓宽，展示这些算符如何在粒子物理的[夸克模型](@entry_id:147763)、量子系统的[角动量耦合](@entry_id:145967)以及[量子群](@entry_id:146711)、[仿射李代数](@entry_id:186784)等现代数学结构中发挥关键作用。最后，在 **“动手实践”** 部分，读者将通过解决一系列精心设计的问题，将理论知识转化为实际的计算技能。让我们首先从这些算符的基本原理开始，揭开它们在表示空间中导航的奥秘。

## 原理与机制

在介绍完[李代数表示论](@entry_id:190569)的基本框架之后，本章将深入探讨其动态核心：与根相关联的升、降算符。这些算符不仅是[代数结构](@entry_id:137052)的生成元，更是连接表示中不同权重态的桥梁。理解它们的原理与作用机制，是掌握[李代数表示论](@entry_id:190569)、构建具体表示以及将其应用于物理学（如粒子物理中的[味对称性](@entry_id:152851)）的关键。

### [升降算符](@entry_id:197899)：在表示空间中导航

对于一个[半单李代数](@entry_id:190073) $\mathfrak{g}$，其[Cartan-Weyl基](@entry_id:192652)包含[Cartan子代数](@entry_id:191259) $\mathfrak{h}$ 的元素以及与每个根 $\alpha \in \Delta$ 相关联的**根向量** $E_\alpha$。这些根向量通常被称为**[阶梯算符](@entry_id:199991)**（ladder operators）。对于任意[正根](@entry_id:199264) $\alpha \in \Delta_+$，我们将 $E_\alpha$ 称为**升算符**，而 $E_{-\alpha}$ 称为**降算符**。

这些算符的主要功能是在一个不可约表示的权重空间中移动。当一个升算符 $E_\alpha$ 作用于一个权重为 $\mu$ 的态矢量 $|\mu\rangle$ 上时，它会产生一个权重为 $\mu+\alpha$ 的新态矢量（或者[零矢量](@entry_id:155273)）：
$$ E_\alpha |\mu\rangle \propto |\mu+\alpha\rangle $$
类似地，降算符 $E_{-\alpha}$ 会将权重降低 $\alpha$：
$$ E_{-\alpha} |\mu\rangle \propto |\mu-\alpha\rangle $$
因此，通过连续作用这些算符，我们可以从表示中的任何一个权重态出发，“行走”到所有其他权重态，从而探索整个表示的结构。

这些算符的代数性质由它们的[对易关系](@entry_id:136780)决定。其中最核心的关系是：
$$ [E_\alpha, E_{-\alpha}] = H_\alpha $$
这里，$H_\alpha$ 是与根 $\alpha$ 相关联的**[余根](@entry_id:193338)**（coroot）。$H_\alpha$ 是[Cartan子代数](@entry_id:191259)的一个元素，它在一个权重为 $\mu$ 的态矢量 $|\mu\rangle$ 上的作用是给出一个正比于该态矢量的数值：
$$ H_\alpha |\mu\rangle = \frac{2(\mu, \alpha)}{(\alpha, \alpha)} |\mu\rangle $$
其中 $(\cdot, \cdot)$ 是权重空间中的[内积](@entry_id:158127)。这个数值 $\frac{2(\mu, \alpha)}{(\alpha, \alpha)}$ 是一个重要的量，它将几何（权重和根的相对方向与长度）与代数（算符的作用）联系起来。对于每一个根 $\alpha$，算符 $\{E_\alpha, E_{-\alpha}, H_\alpha\}$ 构成一个 $\mathfrak{su}(2)$ 或 $\mathfrak{sl}(2, \mathbb{C})$ 子代数，这是[李代数表示论](@entry_id:190569)中反复出现的一个基本结构。

### 算符的作用：计算态的模长

知道了[升降算符](@entry_id:197899)会产生什么权重的新态，下一个自然的问题是：这个新态的“大小”是多少？在量子力学的框架下，表示的态矢量位于一个希尔伯特空间中。我们通常将态矢量归一化，并要求对应于不同权重的态矢量相互正交。一个关键的任务是计算由[升降算符](@entry_id:197899)产生的新态的范数（或范数的平方），因为它决定了表示的[矩阵元](@entry_id:186505)。

#### 在最高权重态上的作用

让我们从最简单也最重要的情形开始：算符作用于一个不可约表示的**最高权重矢量** $|\Lambda\rangle$。根据定义，[最高权](@entry_id:202808)重矢量被所有升算符湮灭：
$$ E_\alpha |\Lambda\rangle = 0 \quad (\text{for all positive roots } \alpha \in \Delta_+) $$
现在考虑一个降算符 $E_{-\alpha}$（其中 $\alpha$ 是[正根](@entry_id:199264)）作用于 $|\Lambda\rangle$。新态 $|\psi\rangle = E_{-\alpha} |\Lambda\rangle$ 的权重为 $\Lambda-\alpha$。其平方模长为：
$$ \langle\psi|\psi\rangle = \| E_{-\alpha} |\Lambda\rangle \|^2 = \langle \Lambda | (E_{-\alpha})^\dagger E_{-\alpha} |\Lambda\rangle $$
在物理学中常用的幺正表示中，我们有 $(E_{-\alpha})^\dagger = E_{\alpha}$。因此，
$$ \| E_{-\alpha} |\Lambda\rangle \|^2 = \langle \Lambda | E_{\alpha} E_{-\alpha} |\Lambda\rangle $$
利用对易子 $[E_{\alpha}, E_{-\alpha}] = E_{\alpha}E_{-\alpha} - E_{-\alpha}E_{\alpha}$ 和 $E_{\alpha}|\Lambda\rangle = 0$，我们可以将 $E_{\alpha}E_{-\alpha}$ 替换为对易子本身：
$$ \| E_{-\alpha} |\Lambda\rangle \|^2 = \langle \Lambda | [E_{\alpha}, E_{-\alpha}] |\Lambda\rangle = \langle \Lambda | H_{\alpha} |\Lambda\rangle $$
由于 $H_\alpha$ 的作用是数乘，我们得到一个简洁而深刻的结果：
$$ \| E_{-\alpha} |\Lambda\rangle \|^2 = \frac{2(\Lambda, \alpha)}{(\alpha, \alpha)} \langle \Lambda | \Lambda \rangle $$
如果我们假设最高权重矢量是归一化的，即 $\langle \Lambda | \Lambda \rangle = 1$，那么这个平方模长恰好等于与根 $\alpha$ 相关的**Dynkin标签** $m_\alpha = \frac{2(\Lambda, \alpha)}{(\alpha, \alpha)}$。

这个公式揭示了一个基本联系：一个降算符作用在最高权重态上产生的态的模长，直接由[最高权](@entry_id:202808)重 $\Lambda$ 在根 $\alpha$ 方向上的“分量”决定。如果 $m_\alpha = 0$，那么 $\| E_{-\alpha} |\Lambda\rangle \|^2 = 0$，这意味着 $E_{-\alpha}|\Lambda\rangle = 0$，即权重 $\Lambda-\alpha$ 不属于该表示。

**示例 1：作用于 $\mathfrak{so}(5)$ 的最高权重**
考虑[李代数](@entry_id:137954) $\mathfrak{so}(5)$（也记作 $B_2$），其单根为 $\alpha_1, \alpha_2$。我们来看其5维不可约表示，其[最高权](@entry_id:202808)重 $\Lambda$ 的Dynkin标签为 $(m_1, m_2) = (1, 0)$。现在，我们想计算由非单根 $\beta = \alpha_1+\alpha_2$ 对应的降算符 $E_{-\beta}$ 作用于归一化的[最高权](@entry_id:202808)重态 $|\Lambda\rangle$ 后所产生的新态的平方模长 [@problem_id:750833]。

根据我们的公式，
$$ \| E_{-\beta} |\Lambda\rangle \|^2 = \frac{2(\Lambda, \beta)}{(\beta, \beta)} $$
我们需要计算 $(\Lambda, \beta)$ 和 $(\beta, \beta)$。从Dynkin标签的定义可知：
$m_1 = \frac{2(\Lambda, \alpha_1)}{(\alpha_1, \alpha_1)} = 1$ 和 $m_2 = \frac{2(\Lambda, \alpha_2)}{(\alpha_2, \alpha_2)} = 0$。
对于 $B_2$ 标准的[内积](@entry_id:158127)规定 $(\alpha_1, \alpha_1) = 2, (\alpha_2, \alpha_2) = 1, (\alpha_1, \alpha_2) = -1$，我们可以解出 $(\Lambda, \alpha_1)=1$ 和 $(\Lambda, \alpha_2)=0$。
因此，$(\Lambda, \beta) = (\Lambda, \alpha_1+\alpha_2) = (\Lambda, \alpha_1) + (\Lambda, \alpha_2) = 1+0=1$。
同时，$(\beta, \beta) = (\alpha_1+\alpha_2, \alpha_1+\alpha_2) = (\alpha_1, \alpha_1) + 2(\alpha_1, \alpha_2) + (\alpha_2, \alpha_2) = 2 + 2(-1) + 1 = 1$。
代入公式，我们得到：
$$ \| E_{-(\alpha_1+\alpha_2)} |\Lambda\rangle \|^2 = \frac{2(1)}{1} = 2 $$
这个结果在构建整个5维表示时至关重要。同样的方法也适用于其他代数，例如计算 $\mathfrak{su}(4)$ 的6维表示中 $E_{-\theta}|\omega_2\rangle$ 的模长 [@problem_id:750997]。

**示例 2：何时结果为零？**
这个公式也解释了为什么某些降算符会湮灭[最高权](@entry_id:202808)重态。考虑[例外李代数](@entry_id:202996) $G_2$，其单根为 $\alpha_1$（短）和 $\alpha_2$（长）。它的7维[基本表示](@entry_id:157678)的[最高权](@entry_id:202808)重是第一个[基本权](@entry_id:200855)重 $\lambda_1$。根据基本权重的定义，$\frac{2(\lambda_i, \alpha_j)}{(\alpha_j, \alpha_j)} = \delta_{ij}$。
如果我们想计算 $E_{-\alpha_2}|\lambda_1\rangle$ 的模长，我们需要Dynkin标签 $m_2 = \frac{2(\lambda_1, \alpha_2)}{(\alpha_2, \alpha_2)}$。根据定义，这个值为 $\delta_{12} = 0$。因此，
$$ \| E_{-\alpha_2} |\lambda_1\rangle \|^2 = 0 $$
这意味着 $E_{-\alpha_2}|\lambda_1\rangle$ 是一个[零矢量](@entry_id:155273) [@problem_id:750867]。权重 $\lambda_1 - \alpha_2$ 不在该[表示的权](@entry_id:204286)重集合中。这说明，从最高权重出发，我们并不能随意沿任意负根方向下降；路径是由[代数结构](@entry_id:137052)严格限定的。

#### 一般情况：根弦与主公式

现在，让我们把目光从[最高权](@entry_id:202808)重态移开，考虑算符 $E_{\pm\alpha}$ 作用于表示中任意一个权重为 $\mu$ 的态 $|\mu\rangle$。这种情况更为复杂，因为 $|\mu\rangle$ 不再被所有升算符湮灭。

这里的关键概念是**$\alpha$-根弦**（$\alpha$-root string）。给定一个权重 $\mu$ 和一个根 $\alpha$，$\alpha$-根弦是指表示中所有形如 $\mu+k\alpha$（其中 $k$ 为整数）的权重的集合。这个集合必然是一个连续的序列：
$$ \{ \mu-q\alpha, \mu-(q-1)\alpha, \dots, \mu, \dots, \mu+p\alpha \} $$
其中 $p$ 和 $q$ 是非负整数，它们标志着这个弦的“末端”；即 $\mu+(p+1)\alpha$ 和 $\mu-(q+1)\alpha$ 不再是该[表示的权](@entry_id:204286)重。

这些态矢量构成了与根 $\alpha$ 关联的 $\mathfrak{su}(2)$ 子代数的一个不可约表示。弦的长度为 $p+q+1$。权重 $\mu$ 在这个弦中的相对位置由一个基本恒等式确定：
$$ q-p = \frac{2(\mu, \alpha)}{(\alpha, \alpha)} $$
这个关系将弦的不对称性 ($q-p$) 与权重 $\mu$ 在 $\alpha$ 上的投影直接联系起来。

基于这个 $\mathfrak{su}(2)$ 结构，可以推导出作用于任意权重态的[升降算符](@entry_id:197899)的矩阵元的通用公式。在一种常见的归一化约定下（[基态](@entry_id:150928)归一化，且满足前面给出的[对易关系](@entry_id:136780)），新态的平方模长为：
$$ \| E_{\alpha} |\mu\rangle \|^2 = p(q+1) $$
$$ \| E_{-\alpha} |\mu\rangle \|^2 = q(p+1) $$
注意当 $|\mu\rangle=|\Lambda\rangle$ 时，$p=0$，且 $q = \frac{2(\Lambda, \alpha)}{(\alpha, \alpha)}$。此时，关于 $E_{-\alpha}$ 的通用公式退化为 $\| E_{-\alpha} |\Lambda\rangle \|^2 = q(p+1) = \frac{2(\Lambda, \alpha)}{(\alpha, \alpha)}(0+1) = \frac{2(\Lambda, \alpha)}{(\alpha, \alpha)}$，这与我们之前为最高权重态导出的结果完全吻合。(注意：不同文献的归一化约定可能导致公式系数不同，但物理本质相同)。

**示例 3：在 $\mathfrak{sp}(6)$ 表示的中间态上的作用**
考虑[李代数](@entry_id:137954) $\mathfrak{sp}(6)$（类型 $C_3$）的6维[基本表示](@entry_id:157678)，其[最高权](@entry_id:202808)重为 $\omega_1$。我们要计算 $\| E_{-\alpha_2}|\omega_1-\alpha_1\rangle \|^2$ [@problem_id:750941]。
这里的算符是 $E_{-\alpha_2}$，作用的态是 $|\mu\rangle = |\omega_1-\alpha_1\rangle$。
首先，确定相关的参数：根 $\alpha = \alpha_2$，权重 $\mu = \omega_1-\alpha_1$。
在 $C_3$ 的标准实现中，$\omega_1 = \epsilon_1, \alpha_1 = \epsilon_1-\epsilon_2, \alpha_2 = \epsilon_2-\epsilon_3$。所以，作用的权重是 $\mu = \epsilon_2$。
我们需要寻找通过 $\mu=\epsilon_2$ 的 $\alpha_2$-根弦。首先计算 $q-p$：
$$ q-p = \frac{2(\mu, \alpha_2)}{(\alpha_2, \alpha_2)} = \frac{2(\epsilon_2, \epsilon_2-\epsilon_3)}{(\epsilon_2-\epsilon_3, \epsilon_2-\epsilon_3)} = \frac{2(1)}{2} = 1 $$
所以 $q=p+1$。接下来，我们需要通过检查6维[表示的权](@entry_id:204286)重集 $\Phi(\omega_1) = \{\pm\epsilon_1, \pm\epsilon_2, \pm\epsilon_3\}$ 来确定 $p$ 和 $q$ 的具体值。
我们从 $\mu=\epsilon_2$ 开始，沿着 $\alpha_2$ 方向向上（增加 $\alpha_2$）和向下（减去 $\alpha_2$）寻找：
- 向上：$\mu+\alpha_2 = \epsilon_2 + (\epsilon_2-\epsilon_3) = 2\epsilon_2-\epsilon_3$。这个权重不属于 $\Phi(\omega_1)$。因此，弦在 $\mu$ 之上就终止了，这意味着 $p=0$。
- 向下：既然 $p=0$，那么 $q=p+1=1$。我们可以验证：$\mu-\alpha_2 = \epsilon_2 - (\epsilon_2-\epsilon_3) = \epsilon_3$，这在 $\Phi(\omega_1)$ 中。而 $\mu-2\alpha_2 = \epsilon_3 - (\epsilon_2-\epsilon_3) = 2\epsilon_3-\epsilon_2$，这不在 $\Phi(\omega_1)$ 中。所以 $q=1$ 是正确的。
现在，我们将 $p=0, q=1$ 代入主公式：
$$ \| E_{-\alpha_2}|\epsilon_2\rangle \|^2 = q(p+1) = 1 \cdot (0+1) = 1 $$

#### SU(2)子代数视角

根弦方法虽然通用，但有时通过 $\mathfrak{su}(2)$ 的自旋表示理论来思考会更直观。$\alpha$-根弦中的 $p+q+1$ 个态构成了 $\mathfrak{su}(2)_\alpha$ 的一个自旋为 $j=(p+q)/2$ 的不可约表示。在这个表示中，态 $|\mu+k\alpha\rangle$ 对应于磁量子数 $m_k = k + \frac{p-q}{2}$ 的态 $|j, m_k\rangle$。[升降算符](@entry_id:197899) $E_{\pm\alpha}$ 的作用就等同于标准角动量理论中的 $J_{\pm}$ 算符。

**示例 4：利用 $\mathfrak{su}(2)$ 图像计算**
在 $\mathfrak{su}(5)$ 的一个15维表示（[最高权](@entry_id:202808)重 $2\omega_1$）中，考虑态 $|\mu\rangle=|\epsilon_3+\epsilon_4\rangle$。我们要计算 $\| E_{\alpha_3}|\mu\rangle \|^2$，其中 $\alpha_3 = \epsilon_3-\epsilon_4$ [@problem_id:751008]。
我们关注通过 $\mu$ 的 $\alpha_3$-根弦。该[表示的权](@entry_id:204286)重形如 $\epsilon_i+\epsilon_j$ ($i \le j$)。通过 $\mu$ 的弦包含以下权重：
- $\mu-\alpha_3 = (\epsilon_3+\epsilon_4) - (\epsilon_3-\epsilon_4) = 2\epsilon_4$
- $\mu = \epsilon_3+\epsilon_4$
- $\mu+\alpha_3 = (\epsilon_3+\epsilon_4) + (\epsilon_3-\epsilon_4) = 2\epsilon_3$
这个弦共有3个态，因此它构成一个自旋 $j=1$ 的 $\mathfrak{su}(2)$ 表示。
态 $|\mu\rangle$ 在这个[三重态](@entry_id:156705)中的位置由其 $H_{\alpha_3}$ 的[本征值](@entry_id:154894)决定，其磁量子数 $m$ (对应于 $J_z$ 的[本征值](@entry_id:154894)) 为 $0$ (因为它是[三重态](@entry_id:156705)的中间态)。所以，态 $|\mu\rangle$ 对应于 $|j=1, m=0\rangle$。我们要求的是 $E_{\alpha_3}$ 作用后的模方，这对应于 $J_+$ 的作用。根据角动量理论：
$$ \| J_+|j,m\rangle \|^2 = (j-m)(j+m+1) $$
代入 $j=1, m=0$：
$$ \| E_{\alpha_3}|\mu\rangle \|^2 \propto (1-0)(1+0+1) = 2 $$
在本文的归一化约定下，这个比例系数为1，因此模方就是2。这种方法将复杂计算转化为熟悉的[量子力学角动量](@entry_id:192447)问题。

### [结构常数](@entry_id:157960)与伴随表示

[升降算符](@entry_id:197899)不仅在表示中移动，它们之间的[对易关系](@entry_id:136780)定义了李代数本身的结构。
$$ [E_\alpha, E_\beta] = N_{\alpha, \beta} E_{\alpha+\beta} \quad (\text{if } \alpha+\beta \text{ is a root}) $$
这里的系数 $N_{\alpha, \beta}$ 称为**[结构常数](@entry_id:157960)**。这些常数的值依赖于基的选择和归一化，但它们的平方 $|N_{\alpha, \beta}|^2$ 是内禀的。

伴随表示（adjoint representation）提供了一个计算这些[结构常数](@entry_id:157960)的舞台。在伴随表示中，李代数本身就是表示空间，权重就是代数的根（以及零权重），而权重为 $\alpha$ 的态矢量可以被等同于根向量 $E_\alpha$。因此，算符 $E_\alpha$ 在伴随表示中作用于态 $| \beta \rangle$ 就等价于[李代数](@entry_id:137954)中的对易子 $[E_\alpha, E_\beta]$。
$$ E_\alpha |\beta\rangle \equiv \text{ad}(E_\alpha) (E_\beta) = [E_\alpha, E_\beta] = N_{\alpha, \beta} |\alpha+\beta\rangle $$
取模长的平方，我们得到一个重要的关系：
$$ \| E_\alpha |\beta\rangle \|^2 = |N_{\alpha, \beta}|^2 $$
这意味着我们可以使用前面为[表示论](@entry_id:137998)推导的通用范数公式来计算[李代数](@entry_id:137954)的[结构常数](@entry_id:157960)！我们只需将公式中的权重 $\mu$ 替换为根 $\beta$，并在伴随表示（即整个根系统）中寻找根弦。

**示例 5：计算 $\mathfrak{so}(7)$ 的[结构常数](@entry_id:157960)**
我们要计算[李代数](@entry_id:137954) $\mathfrak{so}(7)$（类型 $B_3$）的[结构常数](@entry_id:157960) $|N_{\alpha, \beta}|^2$，其中 $\alpha = \alpha_1$, $\beta = \alpha_2+\alpha_3$ [@problem_id:750906]。
我们使用公式 $\| E_{\alpha_1} |\beta\rangle \|^2 = |N_{\alpha_1, \beta}|^2$。这需要我们计算 $\alpha_1$-根弦穿过根 $\beta$ 的 $p,q$ 值。
首先，我们利用恒等式计算 $q-p$。对于 $B_3$，[Cartan矩阵](@entry_id:185184)元素为 $A_{12}=-1, A_{13}=0$。
$$ q-p = \frac{2(\beta, \alpha)}{(\alpha, \alpha)} = \frac{2(\alpha_2+\alpha_3, \alpha_1)}{(\alpha_1, \alpha_1)} = \frac{2(\alpha_1, \alpha_2)}{(\alpha_1, \alpha_1)} + \frac{2(\alpha_1, \alpha_3)}{(\alpha_1, \alpha_1)} = A_{12} + A_{13} = -1 + 0 = -1 $$
接下来，通过检查 $B_3$ 的[根系](@entry_id:198970)统来确定 $p,q$ 的具体值。根弦由形如 $\beta+k\alpha_1$ 的根构成。
- 向上（加 $\alpha_1$）：$\beta+\alpha_1$ 是一个根，但 $\beta+2\alpha_1$ 不是。因此，向上的步数 $p=1$。
- 向下（减 $\alpha_1$）：$\beta-\alpha_1$ 不是一个根。因此，向下的步数 $q=0$。
我们得到的 $p=1, q=0$ 与 $q-p = 0-1 = -1$ 的结果相符。
现在，我们将这些值代入升算符 $E_{\alpha_1}$ 的范数公式：
$$ |N_{\alpha_1, \beta}|^2 = \| E_{\alpha_1} |\beta\rangle \|^2 = p(q+1) = 1(0+1) = 1 $$

### 高级应用与相关概念

掌握了[升降算符](@entry_id:197899)的基本作用后，我们可以探索更复杂的场景。

#### 算符的顺序作用

当多个不同的降算符相继作用于[最高权](@entry_id:202808)重态时，如计算 $\| E_{-\alpha_i} E_{-\alpha_j} |\Lambda\rangle \|^2$，我们需要分步进行。
首先，计算中间态 $|\psi_1\rangle = E_{-\alpha_j} |\Lambda\rangle$ 及其平方模长 $\|\psi_1\|^2 = \frac{2(\Lambda, \alpha_j)}{(\alpha_j, \alpha_j)}$。
然后，计算最终态 $|\psi_2\rangle = E_{-\alpha_i} |\psi_1\rangle$。这一步需要使用通用公式，因为 $|\psi_1\rangle$ 不再是最高权重态。其权重为 $\mu = \Lambda-\alpha_j$。我们需要找到通过 $\mu$ 的 $\alpha_i$-根弦的 $p, q$ 值，然后应用公式 $\| E_{-\alpha_i}|\mu\rangle \|^2 = q(p+1)$。最终结果为 $\|\psi_2\|^2 = \|\psi_1\|^2 \cdot q(p+1)$。
一个重要的简化出现在 $[E_{\alpha_i}, E_{-\alpha_j}]=0$ 时（例如当 $i,j$ 对应的单根在Dynkin图中不相邻时）。在这种情况下，计算作用于 $|\psi_1\rangle$ 的 $E_{\alpha_i}$ 时，$E_{\alpha_i}|\psi_1\rangle = E_{\alpha_i}E_{-\alpha_j}|\Lambda\rangle = E_{-\alpha_j}E_{\alpha_i}|\Lambda\rangle = 0$。这意味着对于第二步计算，它的 $p$ 值始终为0，这大大简化了计算 [@problem_id:750870]。

#### 对易子与线性组合

我们也可以研究由算符的对易子或线性组合产生的态。
例如，态 $|[F_S, F_L]|\Lambda\rangle$（其中 $F_i \equiv E_{-\alpha_i}$）的模长计算，直接与[李代数](@entry_id:137954)的Serre关系相关。如果某个Dynkin标签为零，例如 $m_S=0$，则 $F_S|\Lambda\rangle=0$，对易子作用简化为 $F_S F_L |\Lambda\rangle$，之后可以按顺序作用的方法计算 [@problem_id:750854]。

对于[线性组合](@entry_id:154743)产生的态，例如 $|\psi\rangle = (E_{-\alpha_1} + E_{-\alpha_2})|\theta\rangle$（其中 $|\theta\rangle$ 是伴随表示的最高权重态），其平方模长为：
$$ \|\psi\|^2 = \langle\psi|\psi\rangle = \|E_{-\alpha_1}|\theta\rangle\|^2 + \|E_{-\alpha_2}|\theta\rangle\|^2 + 2\text{Re}\langle\theta|E_{\alpha_1}E_{-\alpha_2}|\theta\rangle $$
[交叉](@entry_id:147634)项 $\langle\theta|E_{\alpha_1}E_{-\alpha_2}|\theta\rangle$ 涉及到一个权重为 $\theta-\alpha_2+\alpha_1$ 的中间态。由于不同权重的态矢量是正交的，而初态和末态都是权重为 $\theta$ 的态，只有当 $\theta-\alpha_2+\alpha_1 = \theta$（即 $\alpha_1=\alpha_2$）时，该项才可能非零。在 $\mathfrak{su}(3)$ 的例子中，$\alpha_1 \neq \alpha_2$，因此[交叉](@entry_id:147634)项为零，平方模长就是两个单独模长之和 [@problem_id:750978]。这清晰地展示了量子力学中叠加与[正交性原理](@entry_id:153755)在[李代数表示论](@entry_id:190569)中的体现。

#### [Freudenthal递归公式](@entry_id:198599)：权重多重性的计算

[升降算符](@entry_id:197899)的原理最终被封装在一个极为强大的工具中：**[Freudenthal递归公式](@entry_id:198599)**。该公式用于计算[不可约表示](@entry_id:263310)中任意权重 $\lambda$ 的多重性 $m(\lambda)$。其形式为：
$$ \left( (\|\Lambda + \delta\|^2 - \|\lambda + \delta\|^2) \right) m(\lambda) = 2 \sum_{\alpha \in \Delta_+} \sum_{k=1}^{\infty} m(\lambda + k\alpha) (\lambda + k\alpha, \alpha) $$
这里 $\Lambda$ 是最高权重，$\delta$ 是Weyl矢量（所有[正根](@entry_id:199264)和的一半）。这个公式的右边本质上是对所有能通过升算符“到达” $\lambda$ 的“更高”权重的贡献求和。每个贡献项都包含了升算符作用的[矩阵元](@entry_id:186505)信息（通过[内积](@entry_id:158127) $(\lambda+k\alpha, \alpha)$ 体现）。这是一个从高权重向低权重逐级计算[多重性](@entry_id:136466)的递归方法。例如，可以用它来计算 $\mathfrak{su}(3)$ 伴随表示中零权重的[多重性](@entry_id:136466)，结果为2，这与[Cartan子代数](@entry_id:191259)的维数（即[李代数的秩](@entry_id:184833)）相符 [@problem_id:750917]。

总之，与根相关联的[升降算符](@entry_id:197899)是[李代数表示论](@entry_id:190569)的引擎。它们的作用由根与权重的几何关系精确控制，其[矩阵元](@entry_id:186505)可以通过根弦方法或等效的 $\mathfrak{su}(2)$ 图像计算。这些计算不仅是构建具体表示的基础，也揭示了[李代数](@entry_id:137954)本身的深刻结构，并为计算权重[多重性](@entry_id:136466)等更高级的问题提供了理论基石。