## 引言
在广义相对论的宏伟画卷中，[度规张量](@entry_id:160222) $g_{\mu\nu}$ 描绘了时空因物质与能量而弯曲的壮丽几何。然而，这一经典描述在面对量子世界的基本粒子——如具有自旋的电子——时遇到了根本性的困难。描述这些粒子所用的数学对象“旋量”（spinor），其定义根植于局域的洛伦兹对称性，而非广义的坐标变换。如何将[旋量](@entry_id:158054)的微观物理无缝地融入宏观的[弯曲时空](@entry_id:159822)？这便是标架场（Vielbein）形式体系应运而生的核心问题，它构成了连接这两个世界的关键桥梁。

本文旨在系统性地阐释标架场这一强大而优美的理论工具。在第一章“原理与机制”中，我们将深入探讨标架场如何作为[度规张量](@entry_id:160222)的“平方根”在时空各点建立[局域惯性系](@entry_id:198325)，并由此定义出自旋[联络与曲率](@entry_id:158520)等核心几何量。随后的第二章“应用与跨学科联系”将展示标架场在物理学中的广泛应用，从广义相对论中的局部观测者和[黑洞](@entry_id:158571)物理，到[量子场论](@entry_id:138177)中的[安鲁效应](@entry_id:146787)，再到凝聚态物理中的晶体缺陷理论，乃至弦论等前沿领域。最后，在“动手实践”部分，读者将通过具体问题演练，将理论知识转化为解决实际问题的能力。

## 原理与机制

在广义相对论的数学框架中，我们用度规张量 $g_{\mu\nu}$ 来描述[弯曲时空](@entry_id:159822)的几何结构。然而，[度规张量](@entry_id:160222)及其关联的[列维-奇维塔联络](@entry_id:161107)（Levi-Civita connection）虽然足以描述[标量场](@entry_id:151443)和矢量场等[张量场](@entry_id:190170)的动力学，但在处理旋量场（spinor fields）时却显得力不从心。旋量，作为描述电子等自旋为 $1/2$ 粒子的数学对象，其定义根植于[洛伦兹群](@entry_id:139964)的[旋量表示](@entry_id:141362)，而非[广义坐标](@entry_id:156576)变换。因此，为了将旋量物理一致地融入[弯曲时空](@entry_id:159822)中，我们必须在时空的每一点上建立一个局域[惯性参考系](@entry_id:276742)，即一个可以应用[狭义相对论](@entry_id:275552)物理定律的切空间。这正是“标架场”（vielbein）形式体系的核心动机 [@problem_id:1814638]。本章将深入探讨标架场的原理与机制，阐明其如何成为连接宏观弯曲几何与微观局域平直时空物理的桥梁。

### 标架场：几何的“平方根”

标架场（德语：Vielbein，意为“多腿”）提供了一套在[流形](@entry_id:153038)每一点上的[基矢](@entry_id:199546)。在四维时空中，这套[基矢](@entry_id:199546)被称为“四足体”（tetrad）或“四标架”（vierbein）。我们将用拉丁字母索引 $a, b, c, \dots$（取值为 $0, 1, 2, 3$）来标记这个局域[参考系](@entry_id:169232)中的分量，这个[参考系](@entry_id:169232)在局部是平直的，其度规为[闵可夫斯基度规](@entry_id:154660) $\eta_{ab} = \text{diag}(-1, 1, 1, 1)$。与之对应，我们将继续使用希腊字母索引 $\mu, \nu, \lambda, \dots$ 来标记在一般[坐标系](@entry_id:156346)下的分量，其度规为[时空度规](@entry_id:202650) $g_{\mu\nu}(x)$。

标架场 $e^a_\mu(x)$ 是一组依赖于时空点 $x$ 的系数，它将宏观的[坐标基](@entry_id:270149)矢 $dx^\mu$ 与局域的平直[基矢](@entry_id:199546)（作为1-形式）$e^a$ 联系起来，即 $e^a = e^a_\mu dx^\mu$。这组 $e^a$ 被称为协标架场（co-vielbein）。标架场的核心作用在于它建立了两个度规之间的联系，其基本关系式为：

$$g_{\mu\nu} = e^a_\mu e^b_\nu \eta_{ab}$$

这个方程是整个形式体系的基石。从这个角度看，标架场 $e^a_\mu$ 仿佛是[度规张量](@entry_id:160222) $g_{\mu\nu}$ 的“平方根”。给定一个度规 $g_{\mu\nu}$，我们就可以通过求解上述方程来找到一个相应的标架场。

考虑一个由平坦的弗里德曼-罗伯逊-沃尔克（FRW）度规描述的宇宙，其时空间隔为：
$$ds^2 = -dt^2 + a(t)^2 (dx^2 + dy^2 + dz^2)$$

其中 $a(t)$ 是随时间变化的宇宙[尺度因子](@entry_id:266678)。对于一个随[宇宙膨胀](@entry_id:161474)而动的“共动”观测者，他们保持空间坐标 $(x, y, z)$ 不变。我们可以为这样的观测者构建一个最自然的[局域惯性系](@entry_id:198325)。我们希望找到一组 $e^a_\mu$，使得 $g_{\mu\nu} = \eta_{ab} e^a_\mu e^b_\nu$ 成立。通过比较 FRW 度规与[闵可夫斯基度规](@entry_id:154660) $ds^2 = \eta_{ab} (e^a_\mu dx^\mu)(e^b_\nu dx^\nu)$，我们可以直接读出标架场的分量。一个简单的对角化选择是 [@problem_id:1853740]：

$e^0_t = 1, \quad e^1_x = a(t), \quad e^2_y = a(t), \quad e^3_z = a(t)$

所有其他分量为零。我们可以将这组系数写成一个矩阵 $e^a_\mu$，其中 $a$ 为行索引，$\mu$ 为列索引：

$$e^a_\mu = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & a(t) & 0 & 0 \\ 0 & 0 & a(t) & 0 \\ 0 & 0 & 0 & a(t) \end{pmatrix}$$

反之，如果我们已知标架场，也可以重构出度规张量。标架场 $e^a_\mu$ 的逆 $e^\mu_a$ 满足 $e^a_\mu e^\mu_b = \delta^a_b$ 和 $e^a_\mu e^\nu_a = \delta^\nu_\mu$。利用逆标架场，我们可以得到[逆度规](@entry_id:273874)的关系：

$$g^{\mu\nu} = e^\mu_a e^\nu_b \eta^{ab}$$

其中 $\eta^{ab}$ 是逆[闵可夫斯基度规](@entry_id:154660)，其分量与 $\eta_{ab}$ 相同。例如，在一个由常数哈勃参数 $H$ 描述的德西特（de Sitter）宇宙中，一个可能的逆标架场（contravariant vierbein）为 [@problem_id:1853751]：

$$e^\mu_a = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & \exp(-Ht) & 0 & 0 \\ 0 & 0 & \exp(-Ht) & 0 \\ 0 & 0 & 0 & \exp(-Ht) \end{pmatrix}$$

利用上述关系，我们可以计算出[逆度规](@entry_id:273874)的各个分量。例如，$g^{00} = \eta^{ab} e^0_a e^0_b = \eta^{00} (e^0_0)^2 = (-1)(1)^2 = -1$。对于空间分量，如 $g^{11} = \eta^{ab} e^1_a e^1_b = \eta^{11} (e^1_1)^2 = (1)(\exp(-Ht))^2 = \exp(-2Ht)$。最终得到的[逆度规](@entry_id:273874)矩阵为：

$$g^{\mu\nu} = \begin{pmatrix} -1 & 0 & 0 & 0 \\ 0 & \exp(-2Ht) & 0 & 0 \\ 0 & 0 & \exp(-2Ht) & 0 \\ 0 & 0 & 0 & \exp(-2Ht) \end{pmatrix}$$

这正好对应于一个尺度因子为 $a(t) = \exp(Ht)$ 的平坦 FRW 度规的逆。

### 标架场：不同标架之间的转换器

标架场 $e^a_\mu$ 及其逆 $e^\mu_a$ 不仅仅是代数上的构造，它们在操作上扮演着“翻译官”的角色，使得张量分量可以在弯曲的坐标标架（希腊索引）和局域的平直标架（拉丁索引）之间来回转换。

对于一个矢量场 $V$，其分量转换关系为：
$V^\mu = e^\mu_a V^a$
$V^a = e^a_\mu V^\mu$

对于一个协矢量场（[1-形式](@entry_id:270392)）$\omega$，其分量转换关系为：
$\omega_\mu = e^a_\mu \omega_a$
$\omega_a = e^\mu_a \omega_\mu$

这种转换能力是[标架场形式体系](@entry_id:161077)的一大优势。在局域的平直标架中，张量索引的升降是通过简单的[闵可夫斯基度规](@entry_id:154660) $\eta_{ab}$ 完成的，这远比使用依赖于时空坐标的 $g_{\mu\nu}(x)$ 要方便得多。

让我们通过一个具体的例子来理解这一过程 [@problem_id:1060264]。考虑一个由柱坐标 $x^\mu = (t, \rho, \phi, z)$ 描述的四维时空，其几何由以下协标架场定义：
$e^0 = dt$
$e^1 = d\rho$
$e^2 = \rho d\phi$
$e^3 = dz + k \rho^2 d\phi$
其中 $k$ 是一个常数。从这些表达式中，我们可以读出协标架场 $e^a_\mu$ 的非零分量，例如 $e^2_\phi = \rho$ 和 $e^3_\phi = k\rho^2$。

假设在该时空中存在一个矢量场 $V$，其在局域洛伦兹标架中的分量为 $V^a = (\alpha, \beta, \gamma/\rho, \delta)$，其中 $\alpha, \beta, \gamma, \delta$ 是常数。我们想求出与该矢量场对应的协矢量场 $V_\mu$ 在[坐标基](@entry_id:270149)矢下的 $\phi$ 分量，即 $V_\phi$。

整个过程分为三步：
1.  **在局域标架中降低索引**：我们首先计算协矢量在局域标架中的分量 $V_a$。这通过[闵可夫斯基度规](@entry_id:154660)完成：$V_a = \eta_{ab} V^b$。
    $V_0 = \eta_{0b} V^b = -V^0 = -\alpha$
    $V_1 = \eta_{1b} V^b = V^1 = \beta$
    $V_2 = \eta_{2b} V^b = V^2 = \gamma/\rho$
    $V_3 = \eta_{3b} V^b = V^3 = \delta$
    所以，$V_a = (-\alpha, \beta, \gamma/\rho, \delta)$。

2.  **转换到坐标标架**：接下来，我们使用转换公式 $\omega_\mu = e^a_\mu \omega_a$ 来找到坐标分量。对于 $V_\phi$：
    $V_\phi = \sum_{a=0}^{3} e^a_\phi V_a = e^0_\phi V_0 + e^1_\phi V_1 + e^2_\phi V_2 + e^3_\phi V_3$

3.  **代入分量计算**：从给定的协标架场定义中，我们知道 $e^0_\phi=0$, $e^1_\phi=0$, $e^2_\phi = \rho$, $e^3_\phi = k\rho^2$。代入这些值和我们算出的 $V_a$ 分量：
    $V_\phi = (0)(-\alpha) + (0)(\beta) + (\rho)(\gamma/\rho) + (k\rho^2)(\delta) = \gamma + k\delta\rho^2$

这个例子清晰地展示了标架场如何作为中介，让我们能够在两种不同的语言（坐标语言和[局域惯性系](@entry_id:198325)语言）之间进行精确的转换。

### 标架场的[规范自由度](@entry_id:160491)

对于给定的度规 $g_{\mu\nu}$，满足 $g_{\mu\nu} = e^a_\mu e^b_\nu \eta_{ab}$ 的标架场 $e^a_\mu$ 并不是唯一的。在任何一个时空点 $x$，我们都可以对局域的 orthonormal [基矢](@entry_id:199546)进行一次洛伦兹变换（旋转或加速），得到的新[基矢](@entry_id:199546)仍然是 orthonormal 的。这意味着，如果 $e^a_\mu(x)$ 是一个合法的标架场，那么通过一个依赖于时空点的洛伦兹变换 $\Lambda^a{}_b(x)$，我们可以构造出一个新的、物理上同样合法的标架场 $e'^{\,a}_\mu(x)$：

$$e'^{\,a}_\mu(x) = \Lambda^a{}_b(x) e^b_\mu(x)$$

其中 $\Lambda^a{}_b(x)$ 满足[洛伦兹群](@entry_id:139964)的条件 $\eta_{cd}\Lambda^c{}_a(x)\Lambda^d{}_b(x) = \eta_{ab}$。这种在每一点独立选择局域洛伦兹标架的自由度是一种**局域[洛伦兹规范](@entry_id:153650)自由度**。

让我们以[史瓦西时空](@entry_id:161500)为例来说明这一点 [@problem_id:1853717]。[史瓦西度规](@entry_id:159484)为：
$$ds^2 = -\left(1 - \frac{r_s}{r}\right) c^2 dt^2 + \left(1 - \frac{r_s}{r}\right)^{-1} dr^2 + r^2 (d\theta^2 + \sin^2\theta d\phi^2)$$

一个简单的对角协标架场是：
$e^{\hat{t}}{}_{t} = c \sqrt{1 - \frac{r_s}{r}}$, $e^{\hat{r}}{}_{r} = \left(1 - \frac{r_s}{r}\right)^{-1/2}$, $e^{\hat{\theta}}{}_{\theta} = r$, $e^{\hat{\phi}}{}_{\phi} = r \sin\theta$

现在，我们考虑对这个局域标架进行一次绕径向（$\hat{r}$ 方向）的依赖于位置的旋转，角度为 $\psi(t, r, \theta, \phi)$。这次变换的洛伦兹矩阵为：
$$\Lambda^{\hat{a}}{}_{\hat{b}} = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & \cos\psi & \sin\psi \\ 0 & 0 & -\sin\psi & \cos\psi \end{pmatrix}$$

我们可以计算新的标架场 $e'^{\hat{a}}_\mu$ 的分量。例如，我们来计算 $e'^{\hat{\theta}}_\phi$：
$e'^{\hat{\theta}}_\phi = \sum_{\hat{b}} \Lambda^{\hat{\theta}}{}_{\hat{b}} e^{\hat{b}}_\phi = \Lambda^{\hat{\theta}}{}_{\hat{t}} e^{\hat{t}}_\phi + \Lambda^{\hat{\theta}}{}_{\hat{r}} e^{\hat{r}}_\phi + \Lambda^{\hat{\theta}}{}_{\hat{\theta}} e^{\hat{\theta}}_\phi + \Lambda^{\hat{\theta}}{}_{\hat{\phi}} e^{\hat{\phi}}_\phi$

由于原始标架是对角的，在 $\mu=\phi$ 列只有 $e^{\hat{\phi}}_\phi = r\sin\theta$ 非零。因此，上式简化为：
$e'^{\hat{\theta}}_\phi = \Lambda^{\hat{\theta}}{}_{\hat{\phi}} e^{\hat{\phi}}_\phi$

从 $\Lambda$ 矩阵中，我们读出 $\Lambda^{\hat{\theta}}{}_{\hat{\phi}} = \sin\psi$。所以，
$e'^{\hat{\theta}}_\phi = (\sin\psi)(r \sin\theta) = r \sin\theta \sin\psi$

类似地，我们也可以计算出 $e'^{\hat{\phi}}_\phi = r \sin\theta \cos\psi$。这个新的标架场 $e'^{\hat{a}}_\mu$ 虽然不是对角的，但它同样能完美地重构出[史瓦西度规](@entry_id:159484)，因此是一个完全合法的标架场。这种选择标架的自由度在处理带有自旋的场时至关重要。

### [标架形式](@entry_id:192197)体系中的[联络与曲率](@entry_id:158520)

我们引入标架场的初衷是为了在弯曲时空中定义旋量及其导数。一个矢量场在局域标架中的分量 $V^a(x)$ 的变化，可能源于矢量场本身的变化，也可能源于我们选择的局域标架从一点到另一点时发生了“转动”。为了分离这两种效应，我们需要引入一个新的联络——**[自旋联络](@entry_id:161745)**（spin connection）$\omega_\mu{}^a{}_b$。

[自旋联络](@entry_id:161745)的作用是补偿局域标架的转动，从而定义一个对[局域洛伦兹变换](@entry_id:158544)[协变](@entry_id:634097)的导数。我们可以通过两种等价的途径来确定[自旋联络](@entry_id:161745)。

#### 通过标架约定（Tetrad Postulate）

第一种方法是要求标架场本身在协变导数下为零，这被称为**标架约定**。它表达了这样一个物理思想：标架场本身不是一个“动力学场”，它只是我们测量几何的工具，这个工具在从一点移动到另一点时应该是“平行”的。这个条件的数学表达式为：

$$\nabla_\mu e^a_\nu = \partial_\mu e^a_\nu - \Gamma^\lambda_{\mu\nu} e^a_\lambda + \omega_{\mu}{}^a{}_c e^c_\nu = 0$$

这里，$\nabla_\mu$ 是作用在所有索引上的完全[协变导数](@entry_id:152476)，$\Gamma^\lambda_{\mu\nu}$ 是标准的[克里斯托费尔符号](@entry_id:159831)（Levi-Civita connection），而 $\omega_{\mu}{}^a{}_c$ 是我们待求的[自旋联络](@entry_id:161745)，它只作用在拉丁索引上。通过重新整理上式，并利用逆标架场，我们可以解出 $\omega_{\mu}{}^a{}_b$：

$$\omega_{\mu}{}^a{}_b = e^a_\nu ( \partial_\mu e^\nu_b + \Gamma^\nu_{\mu\lambda} e^\lambda_b )$$

从这个表达式可以看出，[自旋联络](@entry_id:161745)包含了两种“转动”的信息：一部分来自标架场自身随坐标的变化（$\partial_\mu e^\nu_b$），另一部分来自[坐标系](@entry_id:156346)本身的弯曲（$\Gamma^\nu_{\mu\lambda}$）。

在一个最简单的情形中，即平直的闵可夫斯基时空和[笛卡尔坐标系](@entry_id:169789)，我们可以选择一个常数标架场 $e^\mu_a = \delta^\mu_a$。在这种情况下，克里斯托费尔符号 $\Gamma^\nu_{\mu\lambda}$ 全部为零，标架场的导数 $\partial_\mu e^\nu_b$ 也为零。因此，[自旋联络](@entry_id:161745)的所有分量都为零：$\omega_{\mu}{}^a{}_b = 0$ [@problem_id:1853739]。这符合我们的直觉：在一个全局[惯性系](@entry_id:266190)中，我们不需要“转动”我们的局域[参考系](@entry_id:169232)来保持它的方向。

然而，在[弯曲时空](@entry_id:159822)中，情况就不同了。考虑一个半径为 $R$ 的[二维球面](@entry_id:269890)，其度规为 $ds^2 = R^2 d\theta^2 + R^2 \sin^2\theta d\phi^2$。一个自然的协标架场选择是 $e^1_\theta = R$ 和 $e^2_\phi = R \sin\theta$。即使这个标架场看起来很简单，但由于球面是弯曲的，[自旋联络](@entry_id:161745)并不会为零。我们可以使用上述公式，先计算球面的非零克里斯托费尔符号（例如 $\Gamma^\theta_{\phi\phi} = -\sin\theta\cos\theta$），然后代入求解。例如，要计算 $\omega_{\phi}{}^1{}_2$，我们可以使用标架约定方程 [@problem_id:1853745]：

$$\nabla_\phi e^1_\phi = \partial_\phi e^1_\phi - \Gamma^\lambda_{\phi\phi} e^1_\lambda + \omega_{\phi}{}^1{}_c e^c_\phi = 0$$

代入已知量 ($e^1_\phi=0$, $e^1_\theta=R$, $\Gamma^\theta_{\phi\phi}=-\sin\theta\cos\theta$, $e^2_\phi=R\sin\theta$)，经过计算可得 $\omega_{\phi}{}^1{}_2 = -\cos\theta$。这个非零结果表明，当我们在球面上沿着 $\phi$ 方向移动时，为了保持标架的正交性，我们必须“转动”局域[参考系](@entry_id:169232)。

#### 通过[嘉当结构方程](@entry_id:162100)

第二种方法是使用[微分形式](@entry_id:146747)，这是一种更优雅且强大的工具。在这种语言中，协标架场是1-形式 $e^a = e^a_\mu dx^\mu$，[自旋联络](@entry_id:161745)也是[1-形式](@entry_id:270392) $\omega^a{}_b = \omega_{\mu}{}^a{}_b dx^\mu$。它们由**[嘉当第一结构方程](@entry_id:186381)**联系起来：

$$T^a \equiv de^a + \omega^a{}_b \wedge e^b = 0$$

这里，$d$ 是外微分算子，$\wedge$ 是楔积。$T^a$ 被称为挠率2-形式（torsion 2-form）。在广义相对论中，我们通常假设时空是[无挠的](@entry_id:161664)（torsion-free），即 $T^a=0$。这个方程为求解[自旋联络](@entry_id:161745) $\omega^a{}_b$ 提供了一组代数方程。此外，对于度规相容的联络，[自旋联络](@entry_id:161745)必须是反对称的（在降低一个拉丁索引后）：$\omega_{ab} = \eta_{ac}\omega^c{}_b = -\omega_{ba}$。

让我们用这个方法重新计算[二维球面](@entry_id:269890)上的[自旋联络](@entry_id:161745) [@problem_id:1084771]。协标架为：
$e^{\hat{1}} = R d\theta$
$e^{\hat{2}} = R \sin\theta d\phi$
（这里用带帽的数字索引强调它们是平直标架索引）。

首先计算它们的外微分：
$de^{\hat{1}} = d(R d\theta) = 0$
$de^{\hat{2}} = d(R \sin\theta d\phi) = R \cos\theta d\theta \wedge d\phi$

然后应用[嘉当第一结构方程](@entry_id:186381)。由于反对称性，$\omega^{\hat{1}}{}_{\hat{1}} = \omega^{\hat{2}}{}_{\hat{2}} = 0$ 且 $\omega^{\hat{1}}{}_{\hat{2}} = -\omega^{\hat{2}}{}_{\hat{1}}$。
对于 $\hat{a}=\hat{1}$：$de^{\hat{1}} + \omega^{\hat{1}}{}_{\hat{2}} \wedge e^{\hat{2}} = 0 \implies 0 + \omega^{\hat{1}}{}_{\hat{2}} \wedge (R \sin\theta d\phi) = 0$。
对于 $\hat{a}=\hat{2}$：$de^{\hat{2}} + \omega^{\hat{2}}{}_{\hat{1}} \wedge e^{\hat{1}} = 0 \implies R \cos\theta d\theta \wedge d\phi + \omega^{\hat{2}}{}_{\hat{1}} \wedge (R d\theta) = 0$。

从第一个方程可知，$\omega^{\hat{1}}{}_{\hat{2}}$ 不能包含 $d\theta$ 分量，因此它必然正比于 $d\phi$。设 $\omega^{\hat{1}}{}_{\hat{2}} = f(\theta, \phi) d\phi$。代入第二个方程（并使用 $\omega^{\hat{2}}{}_{\hat{1}} = -\omega^{\hat{1}}{}_{\hat{2}}$）：
$R \cos\theta d\theta \wedge d\phi - (f(\theta,\phi)d\phi) \wedge (R d\theta) = 0$
$R \cos\theta d\theta \wedge d\phi + f(\theta,\phi) R d\theta \wedge d\phi = 0$
$(R \cos\theta + f R) d\theta \wedge d\phi = 0$
这要求 $f = -\cos\theta$。因此，$\omega^{\hat{1}}{}_{\hat{2}} = -\cos\theta d\phi$，而我们想求的 $\omega^{\hat{2}}{}_{\hat{1}} = \cos\theta d\phi$。

#### [非完整性](@entry_id:175408)与结构系数

标架场的另一个重要几何特性是它们的对易子（或李括号）。对于一个[坐标基](@entry_id:270149)矢，我们总是有 $[\partial_\mu, \partial_\nu] = 0$。但对于一个一般的标架场[基矢](@entry_id:199546) $e_a = e^\mu_a \partial_\mu$，它们的对易子不一定为零：

$$[e_a, e_b] = C_{ab}{}^c e_c$$

系数 $C_{ab}{}^c$ 被称为**结构系数**或**[非完整性](@entry_id:175408)系数**（anholonomy coefficients）。它们衡量了沿着[基矢](@entry_id:199546)方向的[无穷小位移](@entry_id:202209)路径是否能构成一个闭合的四边形。如果这些系数不为零，则该标架被称为“非完整的”（anholonomic）。

例如，在描述恒定加速观测者的林德勒（Rindler）[坐标系](@entry_id:156346)中，一个自然的标架选择是 $e_{\hat{0}} = \frac{1}{g\xi} \partial_\tau$ 和 $e_{\hat{1}} = \partial_\xi$。计算它们的[李括号](@entry_id:636461) [@problem_id:1084911]：
$[e_{\hat{0}}, e_{\hat{1}}] = [\frac{1}{g\xi} \partial_\tau, \partial_\xi] = (\frac{1}{g\xi} \partial_\tau) \partial_\xi - \partial_\xi (\frac{1}{g\xi} \partial_\tau) = - (\partial_\xi \frac{1}{g\xi}) \partial_\tau = \frac{1}{g\xi^2} \partial_\tau$
将结果用标架[基矢](@entry_id:199546) $e_{\hat{0}}$ 表示：
$[e_{\hat{0}}, e_{\hat{1}}] = \frac{1}{g\xi^2} (g\xi e_{\hat{0}}) = \frac{1}{\xi} e_{\hat{0}}$
这表明 $C_{\hat{0}\hat{1}}{}^{\hat{0}} = 1/\xi$。即使在平直的闵可夫斯基时空中，一个加速观测者选择的自然标架也是非完整的。结构系数与[自旋联络](@entry_id:161745)密切相关，在[无挠的](@entry_id:161664)情况下，它们之间有直接的代数关系。

### 从[自旋联络](@entry_id:161745)到曲率

一旦我们求出了[自旋联络](@entry_id:161745)，我们就可以计算曲率。**[嘉当第二结构方程](@entry_id:196278)**将[曲率2-形式](@entry_id:187677) $R^a{}_b$ 定义为：

$$R^a{}_b = d\omega^a{}_b + \omega^a{}_c \wedge \omega^c{}_b$$

这与从列维-奇维塔联络计算[黎曼张量](@entry_id:160847)的方式完全平行。[曲率2-形式](@entry_id:187677) $R^a{}_b$ 包含了关于时空弯曲的所有信息，它与[黎曼曲率张量](@entry_id:160189)在局域标架中的分量 $R^a{}_{bcd}$ 的关系为：

$$R^a{}_b = \frac{1}{2} R^a{}_{bcd} e^c \wedge e^d$$

得到 $R^a{}_{bcd}$ 后，计算[里奇张量](@entry_id:159336) $R_{ab}$ 和[里奇标量](@entry_id:158934) $R$ 就非常简单了，因为所有的收缩都是通过平直的 $\eta_{ab}$ 或 $\delta_{ab}$ 完成的：

$R_{ab} = R^c{}_{acb}$
$R = \eta^{ab} R_{ab}$ (在[黎曼几何](@entry_id:160508)中用 $\delta^{ab}$)

让我们以二维球面为例，走完从标架场到[里奇标量](@entry_id:158934)的完[整流](@entry_id:197363)程 [@problem_id:1084929]。我们已经求出，对于半径为 $A$ 的球面，其非零的[自旋联络](@entry_id:161745)是 $\omega^{\hat{1}}{}_{\hat{2}} = -\cos\theta d\phi$。

1.  **计算[曲率2-形式](@entry_id:187677)**：
    $R^{\hat{1}}{}_{\hat{2}} = d\omega^{\hat{1}}{}_{\hat{2}} + \omega^{\hat{1}}{}_{\hat{c}} \wedge \omega^{\hat{c}}{}_{\hat{2}}$
    因为是二维的，所以求和项中只有 $\omega^{\hat{1}}{}_{\hat{2}} \wedge \omega^{\hat{2}}{}_{\hat{2}}$，而 $\omega^{\hat{2}}{}_{\hat{2}}=0$，所以求和项为零。
    $R^{\hat{1}}{}_{\hat{2}} = d(-\cos\theta d\phi) = \sin\theta d\theta \wedge d\phi$

2.  **用标架场表示**：
    我们知道 $e^{\hat{1}} = A d\theta$ 和 $e^{\hat{2}} = A \sin\theta d\phi$，因此 $e^{\hat{1}} \wedge e^{\hat{2}} = A^2 \sin\theta d\theta \wedge d\phi$。
    所以，$d\theta \wedge d\phi = \frac{1}{A^2 \sin\theta} e^{\hat{1}} \wedge e^{\hat{2}}$。
    代入 $R^{\hat{1}}{}_{\hat{2}}$ 的表达式：
    $R^{\hat{1}}{}_{\hat{2}} = \sin\theta \left(\frac{1}{A^2 \sin\theta} e^{\hat{1}} \wedge e^{\hat{2}}\right) = \frac{1}{A^2} e^{\hat{1}} \wedge e^{\hat{2}}$

3.  **提取[黎曼张量分量](@entry_id:188469)**：
    将结果与 $R^{\hat{1}}{}_{\hat{2}} = \frac{1}{2} R^{\hat{1}}{}_{\hat{2}cd} e^c \wedge e^d = R^{\hat{1}}{}_{\hat{2}\hat{1}\hat{2}} e^{\hat{1}} \wedge e^{\hat{2}}$ 进行比较（考虑到反对称性），我们得到：
    $R^{\hat{1}}{}_{\hat{2}\hat{1}\hat{2}} = \frac{1}{A^2}$

4.  **计算[里奇张量](@entry_id:159336)和里奇标量**：
    里奇张量的分量为 $R_{\hat{a}\hat{b}} = R^c{}_{\hat{a}c\hat{b}}$。
    $R_{\hat{1}\hat{1}} = R^{\hat{2}}{}_{\hat{1}\hat{2}\hat{1}} = -R^{\hat{2}}{}_{\hat{1}\hat{1}\hat{2}} = \delta^{\hat{2}\hat{2}} R_{\hat{2}\hat{1}\hat{1}\hat{2}} = R_{\hat{1}\hat{2}\hat{1}}{}^{\hat{2}} = -R_{\hat{1}\hat{2}\hat{2}}{}^{\hat{1}} = -g_{\hat{2}\hat{2}} R^{\hat{1}}{}_{\hat{2}\hat{1}}{}^{\hat{2}} = R^{\hat{1}}{}_{\hat{2}\hat{1}\hat{2}} = \frac{1}{A^2}$。
    同样地，$R_{\hat{2}\hat{2}} = R^{\hat{1}}{}_{\hat{2}\hat{1}\hat{2}} = \frac{1}{A^2}$。
    [里奇标量](@entry_id:158934)为 $R = \delta^{ab} R_{ab} = R_{\hat{1}\hat{1}} + R_{\hat{2}\hat{2}} = \frac{1}{A^2} + \frac{1}{A^2} = \frac{2}{A^2}$。

这个结果 $R=2/A^2$ 是二维球面的标准曲率，它展示了[标架场形式体系](@entry_id:161077)如何系统地、几乎是机械地从度规的“平方根”导出时空的[内蕴曲率](@entry_id:161701)。这个强大而优美的框架不仅是耦合[旋量](@entry_id:158054)与[引力](@entry_id:175476)的必要工具，也为研究广义相对论中的几何与拓扑问题提供了深刻的洞见。