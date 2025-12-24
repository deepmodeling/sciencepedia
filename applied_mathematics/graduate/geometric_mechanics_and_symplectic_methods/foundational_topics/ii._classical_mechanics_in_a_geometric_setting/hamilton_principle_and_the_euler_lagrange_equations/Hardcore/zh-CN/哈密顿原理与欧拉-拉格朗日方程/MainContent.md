## 引言
[哈密顿原理](@entry_id:175601)，或称[平稳作用量原理](@entry_id:151723)，是[分析力学](@entry_id:166738)乃至整个理论物理学的基石。它以一个极其优美和深刻的视角重塑了我们对运动定律的理解，将复杂的矢量力学问题转化为一个求解标量泛函[极值](@entry_id:145933)的[变分问题](@entry_id:756445)。这种方法不仅在概念上更为根本，在实践中也为处理复杂[约束系统](@entry_id:164587)提供了无与伦比的威力。然而，仅仅掌握其在局部坐标下的推导，尚不足以领会其全部的内涵。本文旨在弥合这一知识鸿沟，带领读者从基础的变分演算出发，逐步深入其背后的几何结构，并最终领略其在广阔科学领域中的统一力量。

为实现这一目标，本文将分为三个核心部分。第一章“原理与机制”将系统阐述如何从[作用量原理](@entry_id:154742)出发，通过[变分法](@entry_id:166033)推导出[欧拉-拉格朗日方程](@entry_id:137827)，并将其从传统的坐标表述提升至切丛上的[内蕴几何](@entry_id:158788)语言，揭示其与辛几何的深刻联系。第二章“应用与跨学科联系”将把视野拓宽，展示这一原理如何作为一种统一的语言，应用于经典力学高等专题、连续介质、相对论、[场论](@entry_id:155241)乃至指导现代计算科学中结构保持算法的设计。最后，第三章“动手实践”将通过一系列精心设计的问题，帮助读者巩固对[勒让德变换](@entry_id:142214)、[约束系统](@entry_id:164587)和变分边界条件等关键概念的实际操作和理解。

通过这一趟从原理到应用、从具体到抽象的旅程，读者将对[哈密顿原理](@entry_id:175601)建立一个系统而深入的认识。现在，让我们从其最核心的数学表述开始。

## 原理与机制

继前一章介绍之后，本章将深入探讨[拉格朗日力学](@entry_id:147054)的核心——[哈密顿原理](@entry_id:175601)，并由此推导出运动的数学描述，即[欧拉-拉格朗日方程](@entry_id:137827)。我们将从经典的变分演算出发，逐步过渡到[微分](@entry_id:158422)流形上的[内蕴几何](@entry_id:158788)表述，揭示该理论深刻的几何结构。此外，我们还将探讨该原理的几个关键应用与推广，包括[诺特定理](@entry_id:145690)、时间相关系统以及高阶理论，旨在为读者构建一个系统、严谨且深入的理论框架。

### [作用量原理](@entry_id:154742)

拉格朗日力学的基石是**[哈密顿原理](@entry_id:175601) (Hamilton's principle)**，也常被称为**[平稳作用量原理](@entry_id:151723) (principle of stationary action)**。该原理断言，一个力学系统从一个位形到另一个位形的真实物理轨迹，是使某个称为**作用量 (action)** 的泛函取**平稳值 (stationary value)** 的那条路径。

对于一个由位形流形 $Q$ 上的局部坐标 $q(t)$ 描述的系统，其[拉格朗日量](@entry_id:174593) $L$ 是一个依赖于位形、速度和时间的实值函数，即 $L(q(t), \dot{q}(t), t)$。在给定的时间区间 $[t_0, t_1]$ 内，[作用量泛函](@entry_id:169216) $S[q]$ 定义为拉格朗日量对时间的积分：

$$
S[q] = \int_{t_0}^{t_1} L(q(t), \dot{q}(t), t) \, dt
$$

“平稳”意味着，对于物理轨迹 $q(t)$ 的任意无穷小变分 $\delta q(t)$，作用量的一阶变分 $\delta S$ 为零。为了使这个[变分问题](@entry_id:756445)是良定义的，我们必须明确允许哪些路径参与“竞争”。标准的做法是，我们考虑所有连接相同初始位形 $q(t_0)=q_0$ 和终止位形 $q(t_1)=q_1$ 的光滑路径。这意味着所有容许的路径变分 $\delta q(t)$ 都必须在端点处为零，即 $\delta q(t_0) = 0$ 和 $\delta q(t_1) = 0$。

现在，我们来计算作用量的一阶变分：
$$
\delta S = \delta \int_{t_0}^{t_1} L \, dt = \int_{t_0}^{t_1} \delta L \, dt = \int_{t_0}^{t_1} \left( \frac{\partial L}{\partial q^i} \delta q^i + \frac{\partial L}{\partial \dot{q}^i} \delta \dot{q}^i \right) dt
$$
注意到变分与[微分](@entry_id:158422)运算可交换，即 $\delta \dot{q}^i = \frac{d}{dt}(\delta q^i)$。对第二项进行分部积分：
$$
\int_{t_0}^{t_1} \frac{\partial L}{\partial \dot{q}^i} \frac{d}{dt}(\delta q^i) \, dt = \left[ \frac{\partial L}{\partial \dot{q}^i} \delta q^i \right]_{t_0}^{t_1} - \int_{t_0}^{t_1} \frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}^i}\right) \delta q^i \, dt
$$
将此结果代回 $\delta S$ 的表达式，得到：
$$
\delta S = \int_{t_0}^{t_1} \left( \frac{\partial L}{\partial q^i} - \frac{d}{dt}\frac{\partial L}{\partial \dot{q}^i} \right) \delta q^i \, dt + \left[ \frac{\partial L}{\partial \dot{q}^i} \delta q^i \right]_{t_0}^{t_1}
$$
由于我们考虑的变分在端点处为零，即 $\delta q^i(t_0) = \delta q^i(t_1) = 0$，边界项自动消失。为了让 $\delta S=0$ 对任意在区间 $(t_0, t_1)$ 内的变分 $\delta q^i(t)$ 都成立，根据变分法基本引理，积分号内的表达式必须恒为零。这就给出了系统的[运动方程](@entry_id:264286)，即**[欧拉-拉格朗日方程](@entry_id:137827) (Euler-Lagrange equations)**：
$$
\frac{\partial L}{\partial q^i} - \frac{d}{dt}\frac{\partial L}{\partial \dot{q}^i} = 0
$$
值得强调的是，固定端点位形是确保边界项消失从而得到[欧拉-拉格朗日方程](@entry_id:137827)的标准且充分的条件。

一个常见的误解源于“最小作用量原理”这一历史名称。[哈密顿原理](@entry_id:175601)要求的仅仅是作用量的[平稳性](@entry_id:143776)（即一阶变分为零），而非必然是最小值。平稳点可以是极大值、极小值或鞍点。要判断其类型，需要考察作用量的二阶变分 $\delta^2 S$。

考虑一个简单的例子：一维谐振子，其拉格朗日量为 $L = \frac{1}{2} m \dot{q}^2 - \frac{1}{2} m \omega^2 q^2$。对于边界条件 $q(0)=0$ 和 $q(T)=0$，一个明显的极值路径是 $q(t) \equiv 0$。计算关于此路径的二阶变分可得：
$$
\delta^2 S[\eta] = \int_0^T \left( m \dot{\eta}^2 - m\omega^2 \eta^2 \right) dt
$$
其中 $\eta(t)$ 是满足 $\eta(0)=\eta(T)=0$ 的任意变分。为了检验 $q(t)\equiv 0$ 是否为作用量的极小值，我们需要检查 $\delta^2 S[\eta]$ 是否对所有非零 $\eta$ 都为正。然而，如果我们选取一个特定的变分，例如 $\eta(t) = \sin(\frac{\pi t}{T})$，代入计算可得：
$$
\delta^2 S = \frac{mT}{2} \left( \left(\frac{\pi}{T}\right)^2 - \omega^2 \right)
$$
当时间间隔 $T > \pi/\omega$ 时，$\delta^2 S$ 会变为负值。这意味着对于足够长的时间间隔，静止在原点的平凡路径并非作用量的最小值，而是一个鞍点。这清晰地表明，物理轨迹对应的是“平稳”作用量，而非总是“最小”作用量。

### 切丛上的几何表述

为了更深刻地理解拉格朗日力学的结构，我们必须将其从[局部坐标](@entry_id:181200)的束缚中解放出来，采用[微分几何](@entry_id:145818)的内蕴语言。此时，[位形空间](@entry_id:149531) $Q$ 是一个[光滑流形](@entry_id:160799)，而系统的状态（位形和速度）则由[切丛](@entry_id:161294) $TQ$ 上的一个点来描述。

路径的变分可以被看作是由一个沿着基准路径 $q(t)$ 的**变分向量场 (variational vector field)** $\eta(t) \in T_{q(t)}Q$ 生成的。速度的变分则不再是简单的求导，因为不同时刻的速度向量位于不同的[切空间](@entry_id:199137)中。我们需要借助一个[仿射联络](@entry_id:160152) $\nabla$ (通常是[无挠的](@entry_id:161664)) 来定义速度变分，即 $\nabla_t \eta(t)$，它是对向量场 $\eta(t)$ 沿着曲线 $q(t)$ 的**[协变导数](@entry_id:152476) (covariant derivative)**。

在这种几何设定下，[作用量泛函](@entry_id:169216)的一阶变分可以优雅地写成：
$$
\delta S(q)[\eta] = \int_{t_0}^{t_1} \Big( \langle d_q L, \eta \rangle + \langle d_{\dot{q}}L, \nabla_t \eta \rangle \Big)\, dt
$$
这里，$d_q L$ 是 $L$ 在底流形 $Q$ 方向上的[微分](@entry_id:158422)（一个余[切向量](@entry_id:265494)），而 $d_{\dot{q}}L$ 是 $L$ 在[切空间](@entry_id:199137)纤维方向上的[微分](@entry_id:158422)，即**纤维导数 (fiber derivative)**，$\langle \cdot, \cdot \rangle$ 表示余[切向量](@entry_id:265494)与[切向量](@entry_id:265494)之间的自然配对。通过对第二项进行协变形式的[分部积分](@entry_id:136350)，并利用边界条件 $\eta(t_0) = \eta(t_1) = 0$，我们得到**[无坐标形式](@entry_id:1123057)的[欧拉-拉格朗日方程](@entry_id:137827) (coordinate-free Euler-Lagrange equations)**：
$$
d_q L(q,\dot{q}) - \nabla_t \big(d_{\dot{q}}L(q,\dot{q})\big) = 0
$$
这个方程是一个关于沿路径 $q(t)$ 的余切向量场的方程，它优美地表达了“[广义力](@entry_id:169699)”（左项）等于“[广义动量](@entry_id:165699)变化率”（右项）的物理内涵，且完全不依赖于任何特定的坐标系。

为了进一步揭示 $TQ$ 上的几何结构，我们引入几个核心对象。**纤维导数** $\mathcal{F}L: TQ \to T^*Q$，也称为**勒让德变换 (Legendre transform)**，是描述从拉格朗日图像到哈密顿图像的关键映射。对于任意速度向量 $v_q \in T_qQ$，它给出一个对应的动量余切向量 $p \in T_q^*Q$，其定义为：
$$
\langle \mathcal{F}L(v_q), w_q \rangle = \left.\frac{d}{d\varepsilon}\right|_{\varepsilon=0} L(v_q + \varepsilon w_q), \quad \forall w_q \in T_qQ
$$
[局部坐标](@entry_id:181200)下，这对应于我们熟悉的 $p_i = \frac{\partial L}{\partial \dot{q}^i}$。

另一个核心对象是**拉格朗日能量 (Lagrangian energy)** $E_L: TQ \to \mathbb{R}$，定义为：
$$
E_L(v_q) = \langle \mathcal{F}L(v_q), v_q \rangle - L(v_q)
$$
它对应于哈密顿量在[切丛](@entry_id:161294)上的表达。

借助勒让德变换，我们可以从[余切丛](@entry_id:185138) $T^*Q$ 上拉回其固有的几何结构。$T^*Q$ 上存在一个**[典范1-形式](@entry_id:1132867) (canonical 1-form)** $\theta_{\mathrm{can}}$。将其通过 $\mathcal{F}L$ 拉回到 $TQ$ 上，我们得到**庞加莱-嘉当[1-形式](@entry_id:270392) (Poincaré-Cartan 1-form)** $\theta_L = (\mathcal{F}L)^*\theta_{\mathrm{can}}$。然后，我们定义**庞加莱-嘉当[2-形式](@entry_id:188008) (Poincaré-Cartan 2-form)** $\omega_L = -d\theta_L$。这个[2-形式](@entry_id:188008)赋予了 $TQ$ 一个（准）辛结构。

有了这些几何工具，整个拉格朗日动力学可以被浓缩为一个极其简洁而深刻的方程。系统的动力学由 $TQ$ 上的一个[二阶微分方程](@entry_id:269365)向量场 (SODE) $\Gamma_L$ 描述，它满足：
$$
\iota_{\Gamma_L} \omega_L = dE_L
$$
其中 $\iota$ 表示[内积](@entry_id:750660)。这个方程表明，动力学向量场 $\Gamma_L$ 就是在[辛流形](@entry_id:161608) $(TQ, \omega_L)$ 上由能量函数 $E_L$ 生成的哈密顿向量场。[欧拉-拉格朗日方程](@entry_id:137827)的所有信息都蕴含在这个[几何方程](@entry_id:173321)之中。

### 正则性与[哈密顿动力学](@entry_id:156273)

[勒让德变换](@entry_id:142214) $\mathcal{F}L: TQ \to T^*Q$ 在[拉格朗日力学](@entry_id:147054)与[哈密顿力学](@entry_id:146202)的转换中扮演着核心角色。这种转换能否顺利进行，取决于拉格朗日量的一个关键性质：**正则性 (regularity)**。

一个[拉格朗日量](@entry_id:174593) $L$ 被称为**正则的 (regular)**，如果其关于速度的纤维[海森矩阵](@entry_id:139140) (fiber Hessian) $W_{ij}(q,v) = \frac{\partial^2 L}{\partial v^i \partial v^j}$ 在每一点都非奇异（即可逆）。根据[反函数定理](@entry_id:275014)，这个[正则性条件](@entry_id:166962)确保了[勒让德变换](@entry_id:142214) $\mathcal{F}L$ 是一个[局部微分同胚](@entry_id:203529)。如果 $\mathcal{F}L$ 是一个全局[微分同胚](@entry_id:147249)，则称 $L$ 是**超正则的 (hyperregular)**。

当 $L$ 正则时，我们可以唯一地从动量 $p$ 反解出速度 $v(q,p)$。这使得我们能够定义[哈密顿量](@entry_id:144286) $H: T^*Q \to \mathbb{R}$：
$$
H(q,p) = p_i v^i(q,p) - L(q, v(q,p))
$$
[欧拉-拉格朗日方程](@entry_id:137827)的流可以被 $\mathcal{F}L$ 映到 $T^*Q$ 上，成为由哈密顿量 $H$ 和 $T^*Q$ 上的[典范辛形式](@entry_id:180641) $\omega_{\mathrm{can}}$ 所决定的哈密顿流。勒让德变换此时扮演了**辛同构 (symplectomorphism)** 的角色（在适当的定义域上），它将 $(TQ, \omega_L)$ 上的拉格朗日动力学与 $(T^*Q, \omega_{\mathrm{can}})$ 上的[哈密顿动力学](@entry_id:156273)等价地联系起来。 

然而，当拉格朗日量是**退化的 (degenerate)** 或**奇异的 (singular)** 时，即纤维[海森矩阵](@entry_id:139140)的秩小于 $n$，情况就变得复杂。此时，[2-形式](@entry_id:188008) $\omega_L$ 也是退化的，它的核 (kernel) 非平凡。这样的流形 $(TQ, \omega_L)$ 被称为一个**前[辛流形](@entry_id:161608) (presymplectic manifold)**。动力学方程 $\iota_{\Gamma_L}\omega_L = dE_L$ 的解的存在性不再得到保证。解若要存在，必须满足一个[相容性条件](@entry_id:637057)：$dE_L$ 在 $\ker\omega_L$ 的任何向量场上的取值都必须为零，即 $i_Z dE_L = 0$ 对所有 $Z \in \ker\omega_L$ 成立。这个条件将动力学限制在一个称为**约束子流形 (constraint submanifold)** 的空间上。此外，即使解存在，它也不是唯一的，因为我们总可以在一个解上添加任何属于 $\ker\omega_L$ 的向量场而得到另一个解。这种退化拉格朗日系统是狄拉克-贝尔格曼[约束理论](@entry_id:1122946)的基础，在[规范场](@entry_id:159627)论等现代物理领域中至关重要。

### 关键应用与推广

[哈密顿原理](@entry_id:175601)的强大之处不仅在于其理论的优美，更在于其广泛的适用性和深刻的物理内涵。

#### [诺特定理](@entry_id:145690)：对称性与守恒律

物理学中最深刻的原理之一是**诺特定理 (Noether's Theorem)**，它建立了系统的连续对称性与[守恒量](@entry_id:161475)之间的[一一对应](@entry_id:143935)关系。在[拉格朗日框架](@entry_id:751113)下，这一定理可以被清晰地表述。

假设一个[李群](@entry_id:137659) $G$ 的作用 $G \curvearrowright Q$ 是系统的一个对称性，意味着拉格朗日量 $L$ 在该作用的切提升下保持不变。对于[李代数](@entry_id:137954) $\mathfrak{g}$ 中的任意元素 $\xi$，它在 $Q$ 上生成一个[无穷小生成元](@entry_id:270424)向量场 $\xi_Q$。诺特定理断言，对于每一个这样的无穷小对称性，都存在一个沿着[运动方程](@entry_id:264286)解守恒的量。这个[守恒量](@entry_id:161475)由**动量映射 (momentum map)** $J_L: TQ \to \mathfrak{g}^*$ 给出，它是一个从[切丛](@entry_id:161294)到李代数[对偶空间](@entry_id:146945) $\mathfrak{g}^*$ 的映射。

对于给定的 $\xi \in \mathfrak{g}$，对应的[守恒量](@entry_id:161475) $J_L^\xi$ 是一个定义在 $TQ$ 上的函数，其表达式为：
$$
J_L^\xi(v_q) = \langle J_L(v_q), \xi \rangle = \langle \mathcal{F}L(v_q), \xi_Q(q) \rangle
$$
也就是说，[守恒量](@entry_id:161475)是[广义动量](@entry_id:165699) $\mathcal{F}L(v_q)$ 与对称性生成元向量场 $\xi_Q(q)$ 的配对。[诺特定理](@entry_id:145690)的数学表述为，如果 $q(t)$ 是[欧拉-拉格朗日方程](@entry_id:137827)的解，那么：
$$
\frac{d}{dt} J_L^\xi(q(t), \dot{q}(t)) = 0
$$
例如，如果拉格朗日量在空间平移下不变，则[动量守恒](@entry_id:149964)；如果在空间旋转下不变，则角动量守恒。

#### 力学系统与[测地线](@entry_id:269969)

一个特别重要且富有启发性的例子是形式为 $L = T - V$ 的“自然”拉格朗日系统，其中势能 $V: Q \to \mathbb{R}$ 仅依赖于位形，而动能 $T$ 由位形流形 $Q$ 上的一个黎曼度规 $g$ 定义：$T(q, \dot{q}) = \frac{1}{2} g_q(\dot{q}, \dot{q})$。

在这种情况下，[无坐标形式](@entry_id:1123057)的[欧拉-拉格朗日方程](@entry_id:137827) $\nabla_t \big(d_{\dot{q}}L\big) = d_q L$ 经过推导，可以写成一个非常直观的形式：
$$
\nabla_{\dot{q}} \dot{q} = - \operatorname{grad} V(q)
$$
这里，$\nabla$ 是与度规 $g$ 相容的[列维-奇维塔联络](@entry_id:161107)，$\nabla_{\dot{q}}\dot{q}$ 是沿路径的加速度向量，而 $\operatorname{grad} V$ 是势能 $V$ 的黎曼梯度。这个方程正是牛顿第二定律 ($F=ma$) 在弯曲空间上的几何推广，其中“力”由势能的负梯度给出。

当势能 $V \equiv 0$ 时，方程简化为：
$$
\nabla_{\dot{q}} \dot{q} = 0
$$
这正是[黎曼流形](@entry_id:261160) $(Q, g)$ 上**[仿射参数](@entry_id:260625)化测地线 (affinely parameterized geodesic)** 的定义方程。因此，在没有外力的情况下，粒子在弯曲空间中的自由运动轨迹就是[测地线](@entry_id:269969)。[哈密顿原理](@entry_id:175601)此时等价于[测地线原理](@entry_id:183219)。同时，由于拉格朗日量不显含时间，能量 $E_L = T+V=T$ 守恒，这意味着粒子沿[测地线](@entry_id:269969)以恒定速率运动。

#### 时间相关系统

[哈密顿原理](@entry_id:175601)也可以优雅地处理[拉格朗日量](@entry_id:174593)显式依赖时间 $L(t, q, \dot{q})$ 的情况。一种强大的处理技巧是将时间 $t$ 提升为与 $q^i$ 同等地位的动态坐标。我们构造一个**扩展[位形空间](@entry_id:149531) (extended configuration space)** $\mathcal{Q} = Q \times \mathbb{R}$，其上的路径由参数 $s$ [参数化](@entry_id:265163)，$\gamma(s) = (q(s), t(s))$。

原始作用量 $S = \int L(t, q, \dot{q}) dt$ 可以重写为一个与参数 $s$ 无关的形式：
$$
S[\gamma] = \int_{s_0}^{s_1} L\left(t(s), q(s), \frac{q'(s)}{t'(s)}\right) t'(s) ds
$$
其中 $q' = dq/ds, t' = dt/ds$。现在，我们可以将 $\mathcal{L}(q, t, q', t') = L(t, q, q'/t')t'$ 视为一个定义在 $T\mathcal{Q}$ 上的新拉格朗日量，并对其应用[欧拉-拉格朗日方程](@entry_id:137827)。对 $q^i$ 坐标的变分重新得到了标准的[欧拉-拉格朗日方程](@entry_id:137827)。而对新增的 $t$ 坐标进行变分，则会得到一个关于能量演化的深刻结果：
$$
\frac{d}{dt} \left( \dot{q}^i \frac{\partial L}{\partial \dot{q}^i} - L \right) = - \frac{\partial L}{\partial t}
$$
左侧是拉格朗日能量 $E_L$ 对时间的导数。这个方程表明，系统的能量变化率恰好等于拉格朗日量对时间的偏导数的负值。这立即给出了一个重要的结论：当且仅当[拉格朗日量](@entry_id:174593)不显含时间（即 $\partial L / \partial t = 0$）时，系统能量守恒。

#### 高阶拉格朗日系统

[变分原理](@entry_id:198028)的思想可以自然地推广到依赖于更[高阶导数](@entry_id:140882)（如加速度 $\ddot{q}$）的[拉格朗日量](@entry_id:174593) $L(q, \dot{q}, \ddot{q}, t)$。这类系统被称为**高阶拉格朗日系统**。

通过对作用量 $S[q] = \int L(q, \dot{q}, \ddot{q}, t) dt$ 进行变分，并对包含 $\delta\dot{q}$ 和 $\delta\ddot{q}$ 的项反复使用[分部积分](@entry_id:136350)，我们可以推导出对应的**[欧拉-泊松方程](@entry_id:749105) (Euler-Poisson equations)**：
$$
\frac{\partial L}{\partial q} - \frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}}\right) + \frac{d^2}{dt^2}\left(\frac{\partial L}{\partial \ddot{q}}\right) = 0
$$
这是一个四阶[常微分方程](@entry_id:147024)。值得注意的是，在推导过程中产生的边界项变为：
$$
\left[ \left(\frac{\partial L}{\partial \dot{q}} - \frac{d}{dt}\frac{\partial L}{\partial \ddot{q}}\right) \delta q + \frac{\partial L}{\partial \ddot{q}} \delta \dot{q} \right]_{t_0}^{t_1}
$$
为了对任意[拉格朗日量](@entry_id:174593)都保证此边界项为零，我们必须对变分施加更强的边界条件。除了要求位形变分在端点为零（$\delta q(t_0)=\delta q(t_1)=0$），还必须要求速度变分也在端点为零（$\delta\dot{q}(t_0)=\delta\dot{q}(t_1)=0$）。这意味着，对于[二阶系统](@entry_id:276555)，一个良定义的狄利克雷型[变分问题](@entry_id:756445)需要固定路径的初始和最终位形以及初始和最终速度。