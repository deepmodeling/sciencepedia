## 引言
[经典场论](@entry_id:149475)是现代物理学的支柱，但其传统的[哈密顿表述](@entry_id:276227)常常以牺牲时空[协变](@entry_id:634097)性为代价，将时间视为一个特殊的维度。为了解决这一根本问题，并为场论提供一个统一、内蕴的几何描述，[多辛几何](@entry_id:1128349)应运而生。它将标准辛几何从[处理时间](@entry_id:196496)演化的粒子力学推广到描述时空演化的[场论](@entry_id:155241)，将空间和时间置于同等地位。本文旨在系统性地介绍[射流丛](@entry_id:158903)上的多[辛形式](@entry_id:165896)主义，揭示其如何为[经典场论](@entry_id:149475)构建一个优雅而强大的[协变](@entry_id:634097)框架。

在接下来的内容中，我们将分三部分深入探索这一理论。第一章“原理与机制”将从基本概念入手，介绍作为场论运动学空间的[射流丛](@entry_id:158903)，构建拉格朗日和哈密顿形式主义中的核心几何对象，如[庞加莱-嘉当形式](@entry_id:1129851)与多[辛形式](@entry_id:165896)，并阐明两者之间的[勒让德变换](@entry_id:142214)联系。第二章“应用与交叉学科联系”将展示该理论的实践价值，通过谐和映照、[规范场](@entry_id:159627)论等实例，探讨[协变](@entry_id:634097)的诺特定理和约束系统的处理，并揭示其与连续介质力学、计算科学等领域的深刻联系。最后，“实践练习”部分将提供一系列精选问题，帮助读者将理论知识转化为解决实际问题的能力。

## 原理与机制

本章旨在系统性地阐述[多辛几何](@entry_id:1128349)形式主义的核心原理与机制，该理论为[经典场论](@entry_id:149475)提供了一个严谨而优美的几何框架。我们将从描述场及其导[数的几何](@entry_id:192990)空间——[射流丛](@entry_id:158903)（jet bundle）开始，逐步构建拉格朗日和哈密顿两种形式，并最终揭示它们之间的深刻联系。

### 第一[射流丛](@entry_id:158903)：场的运动学空间

在几何物理中，一个**场 (field)** 通常被描述为一个光滑[纤维丛](@entry_id:159565) $\pi:E \to M$ 的**[截面](@entry_id:154995) (section)**，即一个[光滑映射](@entry_id:203730) $\sigma:M \to E$ 使得 $\pi \circ \sigma = \mathrm{id}_M$。其中，$M$ 是一个 $n$ 维[时空流形](@entry_id:262092)，称为基底流形；$E$ 称为总空间；对于 $M$ 中的每一点 $x$，其[原像](@entry_id:150899) $E_x = \pi^{-1}(x)$ 称为 $x$ 点的纤维。场的[经典动力学](@entry_id:177360)，如[欧拉-拉格朗日方程](@entry_id:137827)，通常涉及场的一阶甚至更高阶的偏导数。为了将这些导数内蕴地、坐标无关地纳入几何框架，我们需要引入**[射流丛](@entry_id:158903)**的概念。

**第一[射流丛](@entry_id:158903) (first jet bundle)** $J^1E$ 是一个其元素能够同时编码场在某点的值及其一阶偏导数的空间。更精确地说，$J^1E$ 中的一个元素，称为一点 $x \in M$ 的 **1-射流 (1-jet)**，是所有在 $x$ 点具有相同值和相同一阶[偏导数](@entry_id:146280)的局部[截面](@entry_id:154995)的[等价类](@entry_id:156032)。给定一个[截面](@entry_id:154995) $\sigma: M \to E$，其**第一射流延长 (first jet prolongation)** 是一个从 $M$ 到 $J^1E$ 的新[截面](@entry_id:154995)，记为 $j^1\sigma$，它将每一点 $x \in M$ 映到 $\sigma$ 在 $x$ 点的 1-射流。

为了具体理解其结构，我们可以引入[局部坐标](@entry_id:181200)。若 $(x^\mu)$ 是基底流形 $M$ 上的[局部坐标](@entry_id:181200)，$(y^i)$ 是纤维上的坐标，那么在 $E$ 上我们有局部[纤维化](@entry_id:203334)[坐标图](@entry_id:156506) $(x^\mu, y^i)$。这些坐标自然地在 $J^1E$ 上诱导出一套坐标系 $(x^\mu, y^i, y^i_\mu)$，其中新增的坐标 $y^i_\mu$ 正是用来编码[一阶导数](@entry_id:749425)的。如果一个[截面](@entry_id:154995) $\sigma$ 的局部表达式为 $y^i = \sigma^i(x^\mu)$，那么其第一射流延长 $j^1\sigma$ 在 $J^1E$ 中的[局部坐标](@entry_id:181200)表达式为：
$$
j^1\sigma(x) = \left(x^\mu, \sigma^i(x^\nu), \frac{\partial \sigma^i}{\partial x^\mu}(x^\nu)\right)
$$
因此，在 $j^1\sigma$ 的像上，坐标函数 $y^i_\mu$ 的取值恰好等于[截面](@entry_id:154995)分量的一阶[偏导数](@entry_id:146280)，即 $y^i_\mu \circ j^1\sigma = \frac{\partial\sigma^i}{\partial x^\mu}$ 。

$J^1E$ 具有丰富的几何结构。首先，存在自然的投影 $\pi_1: J^1E \to M$ 和 $\pi_{1,0}: J^1E \to E$。重要的是，投影 $\pi_{1,0}: J^1E \to E$ 赋予了 $J^1E$ 一个**仿射丛 (affine bundle)** 的结构。对于 $E$ 中任意一点 $e \in E_x$，其上的纤维 $(\pi_{1,0})^{-1}(e)$ 是一个[仿射空间](@entry_id:152906)。该[仿射空间](@entry_id:152906)所建模的[向量空间](@entry_id:151108)是所有从切空间 $T_xM$ 到 $e$ 点的垂直子空间 $V_eE = \ker(d\pi_e)$ 的[线性映射](@entry_id:185132)构成的空间 $L(T_xM, V_eE)$。这个[向量空间](@entry_id:151108)本身同构于 $T_x^*M \otimes V_eE$。因此，从整体上看，$J^1E \to E$ 是一个以向量丛 $\pi^*T^*M \otimes VE$ 为模型的仿射丛 。

正是这种仿射而非向量丛的结构，导致了坐标 $y^i_\mu$ 在[纤维化](@entry_id:203334)[坐标变换](@entry_id:172727)下的复杂变换规则。若进行[坐标变换](@entry_id:172727) $(x^\mu, y^i) \mapsto (x'^\nu, y'^j)$，新的射流坐标 $y'^j_\nu$ 将根据[链式法则](@entry_id:190743)变换为：
$$
y'^j_{\nu} = \frac{\partial x^\mu}{\partial x'^{\nu}}\left(\frac{\partial y'^j}{\partial y^i}\,y^i_{\mu}+\frac{\partial y'^j}{\partial x^\mu}\right)
$$
由于变换式中存在仿射部分（即不含 $y^i_\mu$ 的项 $\frac{\partial y'^j}{\partial x^\mu}$），这意味着不存在一个规范的“零导数”点。换言之，在一个坐标系中 $y^i_\mu=0$ 的点，在另一个坐标系中通常不再为零。这从根本上说明了为什么 $J^1E$ 的纤维不是典型的向量空间 。

在 $J^1E$ 的几何结构中，**接触1-形式 (contact 1-forms)** $\theta^i$ 扮演着至关重要的角色。在局部坐标中，它们被定义为：
$$
\theta^i = dy^i - y^i_\mu dx^\mu
$$
这些[1-形式](@entry_id:270392)的根本几何意义在于，它们恰好在由真实[截面](@entry_id:154995)的射流延长所构成的子流形（称为**完整子流形 (holonomic submanifolds)**）上为零。对任意[截面](@entry_id:154995) $\sigma$，其射流延长 $j^1\sigma$ 满足 $(j^1\sigma)^*\theta^i = 0$。这是因为，当我们将 $\theta^i$ 拉回到 $M$ 上时，根据定义，$d(y^i \circ \sigma) = \frac{\partial \sigma^i}{\partial x^\mu}dx^\mu$，而 $y^i_\mu \circ j^1\sigma$ 也等于 $\frac{\partial \sigma^i}{\partial x^\mu}$，两者恰好抵消 。反之，一个维度为 $n$ 的[子流形](@entry_id:159439) $S \subset J^1E$，如果它上面的所有接触形式都为零（$\theta^i|_S = 0$），并且它能[微分同胚](@entry_id:147249)地投影到基底流形 $M$ 的一个开集上，那么这个子流形 $S$ 必定是某个局部[截面](@entry_id:154995)的第一射流延长的像。这为我们提供了一个判别子流形是否“完整”的内在判据 。

### [拉格朗日形式](@entry_id:145697)与[庞加莱-嘉当形式](@entry_id:1129851)

[经典场论](@entry_id:149475)的[拉格朗日形式](@entry_id:145697)始于一个[作用量泛函](@entry_id:169216)，其被积函数是**拉格朗日密度 (Lagrangian density)**。在几何语言中，一个一阶拉格朗日密度是在第一[射流丛](@entry_id:158903) $J^1E$ 上定义的一个水平 $n$-形式，记为 $\mathcal{L}$。在[局部坐标](@entry_id:181200)中，它可以写作 $\mathcal{L} = L(x^\mu, y^i, y^i_\mu) \eta$，其中 $L$ 是一个标量函数，称为拉格朗日函数，而 $\eta$ 是基底流形 $M$ 上的一个体积元（例如，$\eta = dx^1 \wedge \dots \wedge dx^n$）。

为了以几何方式导出[运动方程](@entry_id:264286)，我们构造一个核心对象——**庞加莱-嘉当 $n$-形式 (Poincaré–Cartan $n$-form)** $\Theta_L$。这个在 $J^1E$ 上定义的 $n$-形式具有一个关键性质：当它被拉回到任意一个完整[截面](@entry_id:154995) $j^1\sigma$ 上时，它还原为原始的拉格朗日密度，即 $(j^1\sigma)^*\Theta_L = \mathcal{L}|_{j^1\sigma}$。为了满足这个要求，$\Theta_L$ 的构造必须巧妙地利用接触形式 $\theta^i$ 的性质。其标准定义为 ：
$$
\Theta_L = \frac{\partial L}{\partial y^i_\mu} \theta^i \wedge \eta_\mu + L \eta
$$
其中 $\eta_\mu = i_{\partial/\partial x^\mu} \eta$ 是通过[内积](@entry_id:750660)从体积元 $\eta$ 构造的 $(n-1)$-形式。由于在完整[截面](@entry_id:154995)上 $(j^1\sigma)^*\theta^i=0$，第一项在拉回时消失，只剩下第二项 $(j^1\sigma)^*(L\eta) = (L \circ j^1\sigma)\eta$，这正是我们所期望的。

通过代数变形，将 $\theta^i = dy^i - y^i_\nu dx^\nu$ 代入并利用恒等式 $dx^\nu \wedge \eta_\mu = \delta^\nu_\mu \eta$，[庞加莱-嘉当形式](@entry_id:1129851)可以被重写为另一个等价的形式 ：
$$
\Theta_L = \frac{\partial L}{\partial y^i_\mu} dy^i \wedge \eta_\mu + \left(L - y^i_\mu \frac{\partial L}{\partial y^i_\mu}\right) \eta
$$
这个形式在向哈密顿形式的过渡中非常有用，因为它显式地包含了[正则动量](@entry_id:155151)和哈密顿函[数密度](@entry_id:895657)的雏形。

### 多辛形式与[欧拉-拉格朗日方程](@entry_id:137827)

从庞加莱-嘉当 $n$-形式出发，我们可以定义**多辛 $(n+1)$-形式 (multisymplectic $(n+1)$-form)** $\Omega_L$，它是在 $J^1E$ 上定义的 $(n+1)$-形式：
$$
\Omega_L = -d\Theta_L
$$
由于 $d^2 = 0$，$\Omega_L$ 自动是[闭形式](@entry_id:272960)，即 $d\Omega_L = 0$。这个形式蕴含了系统的全部动力学信息。[变分原理](@entry_id:198028)（[最小作用量原理](@entry_id:138921)）的几何版本可以通过 $\Omega_L$ 来表述。一个[截面](@entry_id:154995) $\sigma$ 是作用量的[临界点](@entry_id:144653)，当且仅当对于 $J^1E$ 上的任意一个垂直向量场 $V$（即在投影 $\pi_1: J^1E \to M$ 下的[切向量](@entry_id:265494)为零的向量场），以下方程成立：
$$
(j^1\sigma)^* (i_V \Omega_L) = 0
$$
这便是几何形式的**[欧拉-拉格朗日方程](@entry_id:137827) (Euler-Lagrange equations)**。它将[分析力学](@entry_id:166738)中的[偏微分方程组](@entry_id:172573)转化为了一个关于微分形式和向量场的优雅的[代数方程](@entry_id:272665)。

### 哈密顿形式：[多重动量](@entry_id:1129922)相空间

[拉格朗日形式](@entry_id:145697)的[对偶理论](@entry_id:143133)是哈密顿形式。在场论中，这对应于从[射流丛](@entry_id:158903) $J^1E$ 过渡到一个新的相空间，即**[多重动量](@entry_id:1129922)丛 (multimomentum bundle)** $J^1E^*$。

首先，我们需要定义从“速度” $y^i_\mu$ 到“动量”的映射。**[多重动量](@entry_id:1129922) (polymomenta)** 被定义为[拉格朗日函数](@entry_id:174593)对射流速度的偏导数：
$$
p^\mu_i = \frac{\partial L}{\partial y^i_\mu}
$$
这个映射 $(x^\mu, y^i, y^i_\mu) \mapsto (x^\mu, y^i, p^\mu_i)$ 称为**勒让德变换 (Legendre transformation)**，记为 $\mathbb{F}L$。为了使哈密顿理论良定义，我们需要能够从动量反解出速度，即 $y^i_\mu$ 应该是 $(x^\nu, y^j, p^\nu_j)$ 的函数。这要求[勒让德变换](@entry_id:142214)是可逆的。

- **正则性 (Regularity)**：如果 $L$ 对速度变量的黑塞矩阵 (Hessian matrix) $W_{(i\mu)(j\nu)} = \frac{\partial^2 L}{\partial y^i_\mu \partial y^j_\nu}$ 在每一点都是非奇异的（即可逆的），则称拉格朗日量是**正则的 (regular)**。根据[反函数定理](@entry_id:275014)，这保证了[勒让德变换](@entry_id:142214) $\mathbb{F}L$ 是一个局部[微分](@entry_id:158422)同构 。

- **超正则性 (Hyperregularity)**：如果 $\mathbb{F}L$ 是一个全局[微分](@entry_id:158422)同构，则称[拉格朗日量](@entry_id:174593)是**超正则的 (hyperregular)**。这需要比局部非奇异性更强的全局条件，例如全局[单射性](@entry_id:147722)和妥当性 (properness) 。

如果[拉格朗日量](@entry_id:174593)不是正则的（即退化的），勒让德变换将不是满射，其像将落在[多重动量](@entry_id:1129922)空间的一个[子流形](@entry_id:159439)上。这意味着动量分量 $p^\mu_i$ 之间存在不依赖于[运动方程](@entry_id:264286)的代数关系，称为**主约束 (primary constraints)**。例如，对于一个[拉格朗日量](@entry_id:174593) $L = \frac{1}{2}(y^1_0+y^2_0)^2$，其关于速度 $(y^1_0, y^2_0)$ 的黑塞矩阵 $\begin{pmatrix} 1  1 \\ 1  1 \end{pmatrix}$ 是奇异的。对应的动量为 $p^0_1 = y^1_0+y^2_0$ 和 $p^0_2 = y^1_0+y^2_0$。这立即导致了主约束 $\phi(p^0_1, p^0_2) = p^0_1 - p^0_2 = 0$ 。

在正则性的假设下，我们可以定义[多重动量](@entry_id:1129922)丛 $J^1E^*$。这个空间可以被等价地看作是 $J^1E$ 的仿射对偶丛 $\mathrm{Aff}(J^1E, \Lambda^n T^*M)$，或者一个由特定类型的 $n$-形式构成的丛 $\Lambda^n_2 T^*E$ 。在其上，存在一个典范的 $n$-形式 $\Theta$，有时称为刘维尔-[嘉当形式](@entry_id:1122109)，其局部坐标表达式为：
$$
\Theta = p^\mu_i dy^i \wedge \eta_\mu + p \eta
$$
其中 $(x^\mu, y^i, p^\mu_i, p)$ 是扩展[多重动量](@entry_id:1129922)丛的局部坐标。与拉格朗日方面类似，我们定义**典范多辛形式 (canonical multisymplectic form)** 为 $\Omega = -d\Theta$。这个形式赋予了[多重动量](@entry_id:1129922)丛一个重要的几何结构。

### n-辛几何与[哈密顿动力学](@entry_id:156273)

[多重动量](@entry_id:1129922)丛上的典范形式 $\Omega$ 是一个更广泛的几何结构的实例，即 **$n$-[辛流形](@entry_id:161608) ($n$-plectic manifold)**。一个 $n$-[辛流形](@entry_id:161608) $(P, \Omega)$ 是一个装备了一个闭合的、非退化的 $(n+1)$-形式 $\Omega$ 的流形 。
- **[闭合性](@entry_id:1122501) (Closedness)**：$d\Omega = 0$。
- **非退化性 (Non-degeneracy)**：对于每一点 $p \in P$，由[内积](@entry_id:750660)定义的[线性映射](@entry_id:185132) $\flat: T_pP \to \Lambda^n T_p^*P$，$v \mapsto i_v\Omega_p$，是[单射](@entry_id:183792)的。这意味着如果 $i_v\Omega_p = 0$，则必有 $v=0$。

值得注意的是，非退化性只要求[单射](@entry_id:183792)，而不要求同构。因为 $T_pP$ 的维数通常不等于 $\Lambda^n T_p^*P$ 的维数 $\binom{\dim P}{n}$，所以该映射一般不是满射 。[多重动量](@entry_id:1129922)丛 $J^1E^*$ 配备其典范形式 $\Omega=-d\Theta$ 是一个 $n$-[辛流形](@entry_id:161608)，这是多辛哈密顿[场论](@entry_id:155241)的基石 。

在哈密顿框架中，动力学由一个**德东德尔-外尔哈密顿函数 (De Donder–Weyl Hamiltonian)** $H$ 控制，它通过[勒让德变换](@entry_id:142214)定义：
$$
H(x^\mu, y^i, p^\mu_i) = p^\mu_i y^i_\mu - L(x^\mu, y^i, y^i_\mu)
$$
其中 $y^i_\mu$ 被看作是 $(x, y, p)$ 的函数 。[场方程](@entry_id:1124935)可以从一个统一的“主方程” $i_{X_H}\Omega = dH$ 中导出，其中 $X_H$ 是一个与哈密顿量 $H$ 相关的**哈密顿[多重向量](@entry_id:203525)场 (Hamiltonian multivector field)**。对于一个可分解的水平 $n$-向量场 $X_H = \bigwedge_{\mu=1}^n X_\mu$，这个主方程可以解出场分量 $y^i$ 和动量分量 $p^\mu_i$ 所满足的**多辛[哈密顿方程](@entry_id:156213) (multisymplectic Hamilton's equations)**  ：
$$
\frac{\partial y^i}{\partial x^\mu} = \frac{\partial H}{\partial p^\mu_i}
$$
$$
\sum_\mu \frac{\partial p^\mu_i}{\partial x^\mu} = -\frac{\partial H}{\partial y^i}
$$
这些方程构成了拉格朗日[场方程](@entry_id:1124935)的一阶形式，并且它们是描述场演化的一个等价方式。哈密顿[多重向量](@entry_id:203525)场 $X_H$ 也可以被显式地计算出来，它编码了场的时空演化方向 。

### 与标准[辛力学](@entry_id:192937)的联系

当基底流形维数 $n=1$ 时，多辛形式主义优美地退化为我们所熟悉的标准[哈密顿力学](@entry_id:146202)。此时，基底流形是时间轴 $\mathbb{R}$，坐标为 $t$。
- [射流丛](@entry_id:158903) $J^1Y$ 的坐标为 $(t, q^i, v^i)$，其中 $q^i$ 是[广义坐标](@entry_id:156576)，$v^i = \dot{q}^i$ 是[广义速度](@entry_id:178456)。
- [庞加莱-嘉当形式](@entry_id:1129851) $\Theta_L$ 成为一个[1-形式](@entry_id:270392) $\Theta = p_i dq^i - H dt$，其中 $p_i = \partial L / \partial v^i$ 是正则动量，$H = p_i v^i - L$ 是标准的哈密顿函数。这个 $\Theta$ 定义在**[扩展相空间](@entry_id:1124790)** $\mathbb{R} \times T^*Q$ 上。
- 多辛 $(1+1)=2$-形式 $\Omega = d\Theta$ 变为 $\Omega = dp_i \wedge dq^i - dH \wedge dt$。

现在，我们考察这个2-形式在一个固定的**时间切片 (time slice)** $\{t=t_0\}$ 上的行为。时间切片是标准哈密顿力学中的“相空间” $T^*Q$。将 $\Omega$ 拉回到这个时间切片上，由于 $dt$ 在该切片上为零，第二项 $dH \wedge dt$ 消失，我们得到：
$$
\Omega|_{\{t=t_0\}} = dp_i \wedge dq^i
$$
这正是相空间 $T^*Q$ 上的**典范辛[2-形式](@entry_id:188008) (canonical symplectic 2-form)** $\omega_0$ 。

更重要的是，多辛形式的[闭合性](@entry_id:1122501) $d\Omega=0$ 在这里意味着哈密顿动力学流形是保辛的。也就是说，由哈密顿方程生成的时间演化映射 $\Phi_t: T^*Q \to T^*Q$ 是一个辛同构，它保持[典范辛形式](@entry_id:180641)不变：$\Phi_t^* \omega_0 = \omega_0$。这揭示了[辛结构](@entry_id:1132759)的守恒性是多[辛形式](@entry_id:165896)主义[闭合性](@entry_id:1122501)的一个直接推论，从而将场论的几何结构与粒子力学的几何结构无缝地统一起来 。