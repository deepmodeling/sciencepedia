## 引言
[流体动力学](@entry_id:136788)的基本方程，如欧拉方程和纳维-斯托克斯方程，是现代科学与工程的基石，它们以惊人的精度描述了从天气系统到飞机机翼周围气流等各种宏观现象。然而，这些基于连续介质假设的方程与构成流体的离散原子和分子的微观世界之间，存在着一条深刻的概念鸿沟。我们如何从遵循[哈密顿力学](@entry_id:146202)的、时间可逆的粒子运动，过渡到包含粘性耗散等不[可逆过程](@entry_id:276625)的宏观流体行为？

本文旨在系统地回答这一问题，通过构建一个从微观到宏观的理论桥梁，阐明[流体动力学](@entry_id:136788)中各基本方程的层次结构。我们将揭示不同描述层次之间的逻辑联系、各自的物理假设以及它们的[适用范围](@entry_id:636189)。通过这趟理论之旅，读者将深刻理解宏观现象是如何从微观相互作用中“涌现”出来的。

在第一章“原理与机制”中，我们将从经典[统计力](@entry_id:194984)学的N粒子[刘维尔方程](@entry_id:156422)出发，经由BBGKY体系，最终聚焦于描述稀薄气体的玻尔兹曼方程。我们将深入探讨其核心物理假设、不可逆性的起源（[H定理](@entry_id:149078)），并展示如何通过Chapman-Enskog方法从中推导出宏观的[流体力学](@entry_id:136788)方程。随后的“应用与跨学科联系”章节将展示这一理论框架的强大威力，解释粘度、[热导率](@entry_id:147276)等宏观输运性质的微观起源，并探索其在等离子体物理、凝聚态物理乃至相对论等领域的广泛联系。最后，在“动手实践”部分，我们将通过具体的计算练习，巩固从微观定义到宏观系数的关键推导步骤。

## 原理与机制

本章旨在系统地阐述[流体动力学](@entry_id:136788)基本方程的层次结构，从描述[多粒子系统](@entry_id:192694)的微观基础出发，逐步推导至宏观连续介质模型。我们将揭示这些不同层次描述之间的联系、各自的[适用范围](@entry_id:636189)以及它们背后的核心物理原理。

### 从哈密顿力学到[刘维尔方程](@entry_id:156422)：[统计力](@entry_id:194984)学基础

[流体动力学](@entry_id:136788)的最终根源在于其构成粒子（原子或分子）的微观动力学。在经典力学框架下，一个由 $N$ 个粒子组成的孤立系统的状态，在任意时刻 $t$，可以由一个位于 $6N$ 维**相空间**（phase space）中的点完全确定。该相空间的坐标由所有粒子的[广义坐标](@entry_id:156576) $\mathbf{q}_i$ 和[广义动量](@entry_id:165699) $\mathbf{p}_i$ ($i=1, \dots, N$) 构成。

单个系统的演化遵循**[哈密顿方程](@entry_id:156213)**：
$$
\dot{\mathbf{q}}_i = \frac{\partial H}{\partial \mathbf{p}_i}, \quad \dot{\mathbf{p}}_i = - \frac{\partial H}{\partial \mathbf{q}_i}
$$
其中 $H = H(\mathbf{q}_1, \dots, \mathbf{q}_N, \mathbf{p}_1, \dots, \mathbf{p}_N)$ 是系统的[哈密顿量](@entry_id:172864)。这些方程定义了相空间中的一个“速度场” $\mathbf{v}_{\Gamma} = (\dot{\mathbf{q}}_1, \dots, \dot{\mathbf{q}}_N, \dot{\mathbf{p}}_1, \dots, \dot{\mathbf{p}}_N)$。

然而，对于一个宏观系统（$N \sim 10^{23}$），追踪这样一个点的轨迹既无可能也无必要。取而代之，[统计力](@entry_id:194984)学采用系综（ensemble）的方法，即考虑大量处于相同宏观条件下、结构完全相同的系统的集合。系统的[分布](@entry_id:182848)由 $N$ 粒子**[分布函数](@entry_id:145626)** $f_N(\mathbf{q}_1, \dots, \mathbf{p}_N, t)$ 描述，使得 $f_N d\Gamma$ 表示在相空间[体积元](@entry_id:267802) $d\Gamma = \prod_{i=1}^{N} d^3\mathbf{q}_i d^3\mathbf{p}_i$ 内找到的系统数量。

由于系综中的系统总数是守恒的，[分布函数](@entry_id:145626) $f_N$ 必须满足一个连续性方程。我们可以将系综想象成在相空间中流动的一种“相流体”，其密度为 $f_N$，速度为 $\mathbf{v}_{\Gamma}$。其连续性方程写作：
$$
\frac{\partial f_N}{\partial t} + \nabla_{\Gamma} \cdot (f_N \mathbf{v}_{\Gamma}) = 0
$$
[哈密顿力学](@entry_id:146202)的一个深刻结论是，相流体是不可压缩的，即其速度场的散度为零。这被称为**刘维尔定理**。我们可以直接验证这一点：
$$
\nabla_{\Gamma} \cdot \mathbf{v}_{\Gamma} = \sum_{i=1}^{N} \left( \frac{\partial}{\partial \mathbf{q}_i} \cdot \dot{\mathbf{q}}_i + \frac{\partial}{\partial \mathbf{p}_i} \cdot \dot{\mathbf{p}}_i \right) = \sum_{i=1}^{N} \left( \frac{\partial^2 H}{\partial \mathbf{q}_i \partial \mathbf{p}_i} - \frac{\partial^2 H}{\partial \mathbf{p}_i \partial \mathbf{q}_i} \right) = 0
$$
由于相流体不可压缩，连续性方程简化为[物质导数](@entry_id:172646)（convective derivative）形式。将哈密顿方程代入，我们便得到描述 $f_N$ 演化的**[刘维尔方程](@entry_id:156422)**（Liouville equation）[@problem_id:531605]：
$$
\frac{\partial f_N}{\partial t} + \sum_{i=1}^{N} \left( \dot{\mathbf{q}}_i \cdot \frac{\partial f_N}{\partial \mathbf{q}_i} + \dot{\mathbf{p}}_i \cdot \frac{\partial f_N}{\partial \mathbf{p}_i} \right) = \frac{\partial f_N}{\partial t} + \sum_{i=1}^{N} \left( \frac{\partial H}{\partial \mathbf{p}_i} \cdot \frac{\partial f_N}{\partial \mathbf{q}_i} - \frac{\partial H}{\partial \mathbf{q}_i} \cdot \frac{\partial f_N}{\partial \mathbf{p}_i} \right) = 0
$$
[刘维尔方程](@entry_id:156422)是经典[统计力](@entry_id:194984)学的基石。它是一个确定性的、时间可逆的方程，原则上包含了系统的全部动力学信息。然而，由于其极高的维度，直接求解该方程对于任何实际系统都是不可能的。因此，我们必须寻求更简化的描述。

### BBGKY 体系：通往简化描述的桥梁

为了获得一个在计算上可行的理论，我们通常对描述少数几个粒子（例如一个或两个）的低阶[分布函数](@entry_id:145626)更感兴趣。这些**简约分布函数**（reduced distribution functions）$f_s$ ($s \ll N$) 是通过对 $f_N$ 的其余 $N-s$ 个粒子的坐标进行积分得到的。例如，[单粒子分布函数](@entry_id:150211) $f_1(\mathbf{r}_1, \mathbf{p}_1, t)$ 和双[粒子分布函数](@entry_id:753202) $f_2(\mathbf{r}_1, \mathbf{p}_1, \mathbf{r}_2, \mathbf{p}_2, t)$ 定义了在相空间的特定位置找到一个或两个粒子的概率。

通过对[刘维尔方程](@entry_id:156422)进行积分，我们可以推导出一个关于这些简约分布函数的耦合[方程组](@entry_id:193238)，即 **BBGKY 体系**（以 Bogoliubov, Born, Green, Kirkwood, Yvon 的名字命名）。该体系的结构具有一个普遍特征：$f_s$ 的[演化方程](@entry_id:268137)依赖于更高一阶的[分布函数](@entry_id:145626) $f_{s+1}$。例如，第一个方程（$s=1$）的形式为：
$$
\left( \frac{\partial}{\partial t} + \frac{\mathbf{p}_1}{m} \cdot \frac{\partial}{\partial \mathbf{r}_1} \right) f_1 = \int d^3\mathbf{r}_2 d^3\mathbf{p}_2 \, \mathbf{F}_{12} \cdot \frac{\partial f_2}{\partial \mathbf{p}_1}
$$
其中 $\mathbf{F}_{12}$ 是粒子 2 对粒子 1 施加的力。这个方程本身是不封闭的，因为求解 $f_1$ 需要知道 $f_2$，而 $f_2$ 的方程又会依赖于 $f_3$，以此类推。这就是所谓的**封闭问题**（closure problem）。

为了截断这个无限的体系，必须引入物理近似。一个常见的封闭方案是**平均场近似**（mean-field approximation），它忽略了粒子间的关联，即假设双[粒子分布函数](@entry_id:753202)可以分解为两个[单粒子分布函数](@entry_id:150211)的乘积：
$$
f_2(\mathbf{r}_1, \mathbf{p}_1, \mathbf{r}_2, \mathbf{p}_2, t) \approx f_1(\mathbf{r}_1, \mathbf{p}_1, t) f_1(\mathbf{r}_2, \mathbf{p}_2, t)
$$
在这种近似下，BBGKY 体系的第一个方程变为一个封闭的方程，称为**[弗拉索夫方程](@entry_id:161066)**（Vlasov equation）。碰撞项可以被解释为一个作用在粒子上的**平均场力**（mean-field force）$F_{MF}$ [@problem_id:531713]。例如，对于一个一维系统，若粒子间相互作用力为 $F(x_1-x_2)$，则平均场力为：
$$
F_{MF}(x_1, t) = \int dx_2 \, dp_2 \, F(x_1 - x_2) f_1(x_2, p_2, t) = \int dx_2 \, F(x_1 - x_2) \rho(x_2, t)
$$
其中 $\rho(x_2, t)$ 是空间[数密度](@entry_id:268986)。[弗拉索夫方程](@entry_id:161066)在描述由长程力主导的系统（如等离子体和[自引力](@entry_id:271015)星系）时非常成功，因为在这些系统中，单个的、成对的碰撞效应远不如集体平均场的效应重要。

### 玻尔兹曼方程：稀薄气体的动理学理论

对于由[短程力](@entry_id:142823)主导的稀薄气体，[平均场近似](@entry_id:144121)不再适用。在这种情况下，粒子的动力学主要由一系列孤立的、瞬时的**二体碰撞**（binary collisions）决定。[路德维希·玻尔兹曼](@entry_id:155209)（[Ludwig Boltzmann](@entry_id:155209)）基于这一物理图像，提出了一个描述[单粒子分布函数](@entry_id:150211) $f(\mathbf{r}, \mathbf{v}, t)$ 演化的方程。

[玻尔兹曼方程](@entry_id:141554)可以写作：
$$
\frac{\partial f}{\partial t} + \mathbf{v} \cdot \nabla_{\mathbf{r}} f + \frac{\mathbf{F}}{m} \cdot \nabla_{\mathbf{v}} f = C[f]
$$
方程左边描述了粒子在相空间中因自由运动（streaming）和外力 $\mathbf{F}$ 作用下的连续漂移。右边的 $C[f]$ 是**玻尔兹曼[碰撞积分](@entry_id:152100)**（Boltzmann collision integral），它描述了由于粒子间碰撞导致的 $f$ 的不连续变化。这个碰撞项的推导依赖于一个核心的物理假设——**[分子混沌假设](@entry_id:154531)**（Stosszahlansatz）。该假设认为，在一次碰撞发生前，两个粒子的速度是完全不相关的。这个假设有效地在二粒子水平上对 BBGKY 体系进行了封闭，并为方程引入了不[可逆性](@entry_id:143146)。

#### [碰撞不变量](@entry_id:150405)

[碰撞积分](@entry_id:152100) $C[f]$ 有一个至关重要的性质，它与[守恒定律](@entry_id:269268)直接相关。如果某个只依赖于粒子速度的物理量 $\psi(\mathbf{v})$ 在任何一次弹性二体碰撞中，其总和保持不变，即：
$$
\psi(\mathbf{v}_1) + \psi(\mathbf{v}_2) = \psi(\mathbf{v}_1') + \psi(\mathbf{v}_2')
$$
其中 $(\mathbf{v}_1, \mathbf{v}_2)$ 和 $(\mathbf{v}_1', \mathbf{v}_2')$ 分别是碰撞前后的速度，那么 $\psi(\mathbf{v})$ 就被称为**[碰撞不变量](@entry_id:150405)**（collisional invariant）。对于任何[碰撞不变量](@entry_id:150405) $\psi$，其宏观平均值的变化不受碰撞影响：
$$
\int \psi(\mathbf{v}) C[f] \, d^3v = 0
$$
对于[弹性碰撞](@entry_id:188584)，质量（常数 1）、动量 ($m\mathbf{v}$) 和动能 ($\frac{1}{2}m v^2$) 显然是守恒的，因此它们是[碰撞不变量](@entry_id:150405)。一个深刻的结果是，任何连续可微的[碰撞不变量](@entry_id:150405)都必须是这五个量的[线性组合](@entry_id:154743) [@problem_id:531609]。这一结论奠定了[流体动力学](@entry_id:136788)中宏观[守恒定律](@entry_id:269268)（质量、动量、能量）的基础，因为只有这些量的宏观方程不包含未知的碰撞项。

#### H 定理与[平衡态](@entry_id:168134)

玻尔兹曼方程最深刻的推论之一是 **H 定理**。玻尔兹曼定义了一个量 $H(t) = \int f \ln f \, d^3v d^3r$，它与系统的熵 $S$ 密切相关（$S = -k_B H$）。H 定理指出，对于一个孤立系统，由于碰撞，$H$ 函数永远不会增加：$\frac{dH}{dt} \le 0$。这意味着系统的熵永远不会减少。

熵的产生率仅与[碰撞积分](@entry_id:152100)有关。通过对[碰撞积分](@entry_id:152100)进行对称化处理，可以证明熵的碰撞产生项总是非负的 [@problem_id:531665]：
$$
\left(\frac{\partial s}{\partial t}\right)_{\text{coll}} = \frac{k_B}{4} \int d^3v \, d^3v_1 \int d\Omega \, g \, \sigma(g, \Omega) \, (f'f_1' - ff_1) \ln\frac{f'f_1'}{ff_1} \ge 0
$$
其中 $s$ 是熵密度，表达式 $(x-y)\ln(x/y)$ 对于所有正实数 $x,y$ 都是非负的。这揭示了玻尔兹曼方程的不[可逆性](@entry_id:143146)，为宏观世界中的时间之箭提供了微观解释。

当且仅当[熵产生](@entry_id:141771)率为零时，系统[达到平衡](@entry_id:170346)态。这要求 $\ln f' + \ln f_1' = \ln f + \ln f_1$ 对所有碰撞都成立。这意味着 $\ln f$ 必须是一个[碰撞不变量](@entry_id:150405)。因此，[平衡分布](@entry_id:263943)函数 $f_{eq}$ 必须具有以下形式：
$$
\ln f_{eq} = A + \mathbf{B} \cdot (m\mathbf{v}) + C (\tfrac{1}{2}m v^2)
$$
通过适当的变量代换，可以证明这正是**麦克斯韦-玻尔兹曼分布**。

### 从[动理学](@entry_id:136901)理论到[流体动力学](@entry_id:136788)：Chapman-Enskog 展开

[玻尔兹曼方程](@entry_id:141554)虽然比[刘维尔方程](@entry_id:156422)简单，但仍是一个复杂的积分-[微分方程](@entry_id:264184)。然而，在特定极限下，我们可以从中推导出更简单的宏观[流体动力学](@entry_id:136788)方程，如[纳维-斯托克斯方程](@entry_id:142275)。这一过程的关键在于**[克努森数](@entry_id:139772)**（Knudsen number），$Kn = \lambda/L_c$，它定义为粒子[平均自由程](@entry_id:139563) $\lambda$ 与系统宏观特征长度 $L_c$ 之比。

通过对[玻尔兹曼方程](@entry_id:141554)进行[无量纲化](@entry_id:136704)，可以发现碰撞项的系数与 $Kn$ 的倒数成正比 [@problem_id:531680]：
$$
\frac{\partial f'}{\partial t'} + \dots = \frac{1}{Kn} C'[f']
$$
**[流体动力学极限](@entry_id:141281)**对应于 $Kn \to 0$。这意味着碰撞非常频繁，系统在宏观尺度上发生显著变化之前，已经通过大量碰撞达到了[局部平衡](@entry_id:156295)。

#### 零阶近似：[局部平衡](@entry_id:156295)与[欧拉方程](@entry_id:177914)

在 $Kn \to 0$ 的极限下，为了使方程有意义，碰撞项必须在零阶近似下为零，即 $C[f^{(0)}] = 0$。根据 H 定理，这要求零阶[分布函数](@entry_id:145626) $f^{(0)}$ 必须是一个**局部麦克斯韦[分布](@entry_id:182848)**（local Maxwellian distribution）[@problem_id:531593]：
$$
f^{(0)}(\mathbf{r}, \mathbf{v}, t) = n(\mathbf{r}, t) \left(\frac{m}{2\pi k_B T(\mathbf{r}, t)}\right)^{3/2} \exp\left(-\frac{m |\mathbf{v} - \mathbf{u}(\mathbf{r}, t)|^2}{2 k_B T(\mathbf{r}, t)}\right)
$$
这个[分布](@entry_id:182848)的参数——[数密度](@entry_id:268986) $n$、宏观速度 $\mathbf{u}$ 和温度 $T$——不再是全局常数，而是随空间和时间变化的宏观场。

将[分布函数](@entry_id:145626)近似为 $f \approx f^{(0)}$，并取玻尔兹曼方程关于[碰撞不变量](@entry_id:150405)（质量、动量、能量）的矩，由于 $\int \psi C[f] d^3v = 0$，碰撞项消失。这样得到的[方程组](@entry_id:193238)就是描述无粘性、无热传导的[理想流体](@entry_id:161909)的**欧拉方程**（Euler equations）。

#### 一阶近似：[本构关系](@entry_id:186508)与[纳维-斯托克斯方程](@entry_id:142275)

为了描述粘性和[热传导](@entry_id:147831)等耗散现象，我们需要考虑对 $Kn$ 的[一阶修正](@entry_id:155896)，即 $f \approx f^{(0)} + f^{(1)}$，其中 $f^{(1)} \sim Kn$。这一修正项 $f^{(1)}$ 描述了系统对[局部平衡](@entry_id:156295)的偏离，正是这种偏离导致了宏观输运现象。

**Chapman-Enskog 方法**提供了一个系统性的程序来求解 $f^{(1)}$。其核心思想是，耗散通量（如[粘性应力](@entry_id:261328)张量 $\Pi_{ij}$ 和热流矢量 $\mathbf{q}$）是由宏观量的梯度驱动的。为了简化推导并抓住物理本质，我们常常使用模型碰撞算子，例如 **BGK (Bhatnagar-Gross-Krook) 模型**：
$$
C[f] \approx -\nu (f - f^{(0)})
$$
其中 $\nu$ 是碰撞频率，它描述了分布函数 $f$ 向[局部平衡](@entry_id:156295) $f^{(0)}$ 弛豫的速率。这个模型虽然简化，但保留了正确的守恒性质，并能有效地用于推导[输运系数](@entry_id:136790)。

例如，我们可以通过取[玻尔兹曼方程](@entry_id:141554)的二阶矩（[压力张量](@entry_id:147910) $P_{ij} = \int m c_i c_j f d^3\mathbf{c}$，其中 $\mathbf{c} = \mathbf{v}-\mathbf{u}$ 是热运动速度）来推导[粘性应力](@entry_id:261328)张量的本构关系。在一阶 Chapman-Enskog 近似下，并使用 BGK 模型，我们发现[粘性应力](@entry_id:261328)张量 $\Pi_{ij} = P_{ij} - p\delta_{ij}$（$p$ 为[热力学](@entry_id:141121)压力）与应变率张量 $S_{ij} = \frac{1}{2}(\frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i})$ 成正比，这正是**牛顿粘性定律** [@problem_id:531704]。
$$
\Pi_{ij} = -2\mu \left( S_{ij} - \frac{1}{3} (\nabla \cdot \mathbf{u}) \delta_{ij} \right)
$$
更重要的是，这个推导给出了[剪切粘度](@entry_id:141046) $\mu$ 的一个微观表达式，例如在 BGK 模型下，$\mu = p\tau$，其中 $\tau = 1/\nu$ 是[碰撞弛豫](@entry_id:160961)时间。类似地，通过取能量的三阶矩，可以推导出**[傅里叶热传导定律](@entry_id:138911)** $\mathbf{q} = -\kappa \nabla T$，并得到[热导率](@entry_id:147276) $\kappa$ 的微观表达式。

此外，这些近似下的输运关系也满足宏观非[平衡热力学](@entry_id:139780)的要求。例如，可以证明在近平衡条件下，非[对流](@entry_id:141806)熵流 $\mathbf{j}_s^{\text{nc}}$ 与热流 $\mathbf{q}$ 之间存在简单的正比关系 $\mathbf{j}_s^{\text{nc}} = \mathbf{q}/T$ [@problem_id:531633]，这与经典非[平衡热力学](@entry_id:139780)的结论相符。

### 超越稀薄气体和[纳维-斯托克斯方程](@entry_id:142275)

[动理学](@entry_id:136901)理论的框架远比[纳维-斯托克斯方程](@entry_id:142275)更为广阔，它可以被推广以描述更复杂的物理情境。

#### 稠密流体：[分子间势](@entry_id:146849)的作用

[玻尔兹曼方程](@entry_id:141554)仅适用于稀薄气体。对于稠密液体，粒子体积不可忽略，且多体碰撞和持续的[分子间相互作用](@entry_id:263767)力变得至关重要。在这种情况下，压力不仅来源于粒子动量的输运（动理学部分），还包含一个由分子间作用力直接贡献的**位形部分**（potential part）。根据 **Irving-Kirkwood 公式**，总的[压力张量](@entry_id:147910) $\mathbf{P}$ 是[动理学](@entry_id:136901)部分 $\mathbf{P}_K$ 和位形部分 $\mathbf{P}_U$ 的和。对于一个均匀、各向同性的平衡流体，其标量压力 $P$ 可以表示为 [@problem_id:531674]：
$$
P = n k_B T - \frac{2\pi n^2}{3} \int_0^\infty r^3 \frac{d\phi(r)}{dr} g(r) \, dr
$$
这里，$g(r)$ 是**对关联函数**（pair correlation function），描述了在一个粒子周围找到另一个粒子的[概率分布](@entry_id:146404)，$\phi(r)$ 是粒子间的[对势](@entry_id:753090)。这个结果（称为**位力状态方程**）明确地将宏观[热力学性质](@entry_id:146047)（压力）与微观[分子间作用力](@entry_id:203760)联系起来。

#### 超越[一阶近似](@entry_id:147559)：[矩方法](@entry_id:752140)

Chapman-Enskog 展开在 $Kn$ 很小时非常有效，但当 $Kn$ 不再是小量时（如在高空[稀薄气体动力学](@entry_id:144408)或微尺度流动中），纳维-斯托克斯方程会失效。此时需要更高阶的[流体动力学](@entry_id:136788)模型。

除了 Chapman-Enskog 方法，还有一种重要的替代理论，即**[矩方法](@entry_id:752140)**（moment methods），其中最著名的是 **Grad [矩方法](@entry_id:752140)**。该方法不是将分布函数 $f$ 按 $Kn$ 展开，而是将其在一个由**[埃尔米特多项式](@entry_id:153594)**构成的正交基上展开。展开的系数正是 $f$ 的各阶矩，如密度、速度、温度、[应力张量](@entry_id:148973)、热流等。

通过在某个有限阶数截断这个展开，就可以得到一个封闭的[矩方程](@entry_id:149666)组。例如，**Grad 13-矩近似** 保留了前 13 个矩（1个标量 $n$，3个速度分量 $u_i$，1个标量 $T$，5个独立的应力分量 $\sigma_{ij}$，3个热流分量 $q_k$），并给出了 $f$ 的一个显式近似表达式 $f_{13}$。这个近似的分布函数可以用来封闭[矩方程](@entry_id:149666)体系，即将更高阶的矩用这 13 个基本矩表示出来。例如，动能的通量 $R_j = \int m C_j C^2 f d\mathbf{C}$ 可以表示为热流的两倍，$R_j = 2q_j$ [@problem_id:531661]。

这种方法得到的方程（如 Grad 方程或 Burnett 方程）比纳维-斯托克斯方程更复杂，但能描述更广泛的现象，例如非牛顿应力弛豫 [@problem_id:531683] 和非傅里叶热传导，为连接[动理学](@entry_id:136901)理论和[广义连续介质力学](@entry_id:186593)提供了另一条重要的途径。