## 引言
在寻求对物理定律进行更深刻、更几何化描述的征途中，哈密顿力学以其优雅的相空间结构和对对称性的深刻洞察，扮演了核心角色。然而，当从[质点力学](@entry_id:170420)推广到[场论](@entry_id:155241)时，标准的哈密顿形式主义通过将时间从空间坐标中特殊分离出来，破坏了[狭义相对论](@entry_id:275552)所要求的[洛伦兹协变性](@entry_id:161987)。这一理论上的不协调催生了一个核心问题：我们能否构建一个完全协变的哈密顿[场论](@entry_id:155241)，以统一和对称的方式处理时空？

德东德尔-外尔（De Donder-Weyl, DDW）[哈密顿表述](@entry_id:276227)正是对这一问题的有力回答。它为[经典场论](@entry_id:149475)提供了一个强大而优美的[协变](@entry_id:634097)哈密顿框架，不仅再现了正确的动力学，还揭示了深刻的几何与[代数结构](@entry_id:137052)。本文旨在系统地介绍DDW理论，并展示其在现代物理学和相关学科中的广泛应用。

在接下来的内容中，我们将分三步深入探索DDW的世界。首先，在“原则与机制”一章中，我们将剖析该理论的核心构造，从定义[多重动量](@entry_id:1129922)的[协变](@entry_id:634097)勒让德变换开始，推导其动力学方程，并揭示其背后的[多辛几何](@entry_id:1128349)基础。接着，在“应用与交叉学科联系”一章，我们将展示DDW理论的实际威力，看它如何优雅地描述从基础[场论](@entry_id:155241)到[约束规范](@entry_id:635836)理论的各类系统，并与连续介质力学、[几何积分](@entry_id:261978)等领域建立联系。最后，通过“动手实践”部分，你将有机会通过具体计算来巩固所学知识，将抽象的理论转化为切实的技能。

## 原则与机制

在引言中，我们已经探讨了建立一种协变哈密顿形式主义的动机，即一种不因将时间从空间坐标中分离出来而破坏[时空对称性](@entry_id:179029)的框架。De Donder-Weyl (DDW) 理论正是实现这一目标的核心方法。本章将深入探讨其基本原则和核心机制，从[协变](@entry_id:634097)[勒让德变换](@entry_id:142214)开始，构建其动力学方程，揭示其深层的[多辛几何](@entry_id:1128349)结构，并阐明其在处理约束系统和与其他[哈密顿表述](@entry_id:276227)的联系中的作用。

### [协变](@entry_id:634097)勒让德变换：[从拉格朗日到哈密顿](@entry_id:164887)

经典力学的哈密顿形式主义始于一个勒让德变换，它将基于[位形空间](@entry_id:149531)及其[切丛](@entry_id:161294)（包含速度）的[拉格朗日描述](@entry_id:1127015)，转换为基于相空间（包含动量）的哈密顿描述。为了将这一思想推广到[场论](@entry_id:155241)，我们需要一种能够同等对待所有时空坐标的“协变”勒让德变换。

考虑一个[经典场论](@entry_id:149475)，其位形由一个[纤维丛](@entry_id:159565) $\pi: Y \to X$ 描述，其中 $X$ 是一个 $n$ 维[时空流形](@entry_id:262092)，而 $Y$ 的纤维代表场的内部自由度。场的动力学由一个[拉格朗日量](@entry_id:174593) $\mathcal{L}$ 决定，它是一个依赖于时空点 $x^\mu$、场值 $y^i$ 及其[一阶导数](@entry_id:749425) $\partial_\mu y^i$ 的 $n$-形式。局部地，这可以写成 $\mathcal{L} = L(x^\mu, y^i, \partial_\mu y^i) \omega$，其中 $L$ 是拉格朗日密度，$\omega$ 是时空上的[体积形式](@entry_id:203000)。描述场及其一阶导数的空间被称为**一阶[射流丛](@entry_id:158903)** (first jet bundle) $J^1Y$，其局部坐标为 $(x^\mu, y^i, y^i_\mu)$，其中 $y^i_\mu$ 代表 $\partial_\mu y^i$。

De Donder-Weyl 理论的核心步骤是引入**[多重动量](@entry_id:1129922)** (polymomenta) $p_i^\mu$，它们被定义为拉格朗日密度 $L$ 相对于“速度”分量 $y^i_\mu$ 的偏导数：

$$
p_i^\mu := \frac{\partial L}{\partial y^i_\mu}
$$

这里，每个时空方向 $\mu$ 和每个场分量 $i$ 都对应一个动量分量。这组坐标 $(x^\mu, y^i, p_i^\mu)$ 定义了一个新的空间，我们称之为**[多重动量](@entry_id:1129922)相空间** (polymomentum phase space)。

有了[多重动量](@entry_id:1129922)，我们就可以通过**勒让德变换** (Legendre transform) 来定义 **De Donder-Weyl (DW) 哈密顿密度** $H$：

$$
H(x^\mu, y^i, p_i^\mu) := p_i^\mu y^i_\mu - L(x^\mu, y^i, y^i_\mu)
$$

为了使 $H$ 成为[多重动量](@entry_id:1129922)相空间上的[良定义函数](@entry_id:146846)，我们必须能够将速度 $y^i_\mu$ 表示为动量 $p_i^\mu$ 的函数。这要求[勒让德变换](@entry_id:142214)是可逆的，该条件被称为**超正则性** (hyperregularity)，它要求矩阵 $\frac{\partial^2 L}{\partial y^i_\mu \partial y^j_\nu}$ 是可逆的。

为了具体理解这一过程，让我们考虑一个具有度规的[场论](@entry_id:155241)。假设拉格朗日密度具有动能项和势能项的形式，如在问题  中给出的：
$$
\mathcal{L}(x,y,v) = \frac{1}{2}h_{ab}(y)g^{\mu\nu}(x)v_{\mu}^{a}v_{\nu}^{b} - U(y)
$$
其中 $v_\mu^a$ 是速度坐标 $\partial_\mu y^a$，$g^{\mu\nu}$ 是[时空度规](@entry_id:202650)，$h_{ab}$ 是纤维（场空间）上的度规，$U(y)$ 是势能。

首先，我们计算[多重动量](@entry_id:1129922)：
$$
p_{a}^{\mu} := \frac{\partial \mathcal{L}}{\partial v_{\mu}^{a}} = \frac{1}{2}h_{cb}(y)g^{\sigma\nu}(x) \left( \delta^\mu_\sigma \delta^a_c v_\nu^b + v_\sigma^c \delta^\mu_\nu \delta^b_a \right) = h_{ab}(y)g^{\mu\nu}(x)v_{\nu}^{b}
$$
假设度规 $g^{\mu\nu}$ 和 $h_{ab}$ 是非退化的，我们可以反解出速度 $v_\mu^a$：
$$
v_{\mu}^{a} = h^{ab}(y)g_{\mu\nu}(x)p_{b}^{\nu}
$$
其中 $g_{\mu\nu}$ 和 $h^{ab}$ 分别是 $g^{\mu\nu}$ 和 $h_{ab}$ 的逆。

现在，我们可以执行[勒让德变换](@entry_id:142214)来构造 DW 哈密顿密度 $H$。对于这种动能是速度的二次齐次函数的[拉格朗日量](@entry_id:174593)，有一个通用结果：$p_a^\mu v_\mu^a = 2 \times (\text{动能项})$。因此，
$$
H = p_{a}^{\mu} v_{\mu}^{a} - \mathcal{L} = p_{a}^{\mu} v_{\mu}^{a} - \left( \frac{1}{2}p_{a}^{\mu} v_{\mu}^{a} - U(y) \right) = \frac{1}{2}p_{a}^{\mu} v_{\mu}^{a} + U(y)
$$
最后，我们将 $v_\mu^a$ 的表达式代入，得到完全用动量变量表示的 $H$：
$$
H(x,y,p) = \frac{1}{2}p_{a}^{\mu} \left( h^{ab}(y)g_{\mu\nu}(x)p_{b}^{\nu} \right) + U(y) = \frac{1}{2}g_{\mu\nu}(x)h^{ab}(y)p_{a}^{\mu}p_{b}^{\nu} + U(y)
$$
这个结果  展示了如何从一个给定的拉格朗日量系统地构建出其协变的 DW [哈密顿量](@entry_id:144286)。最终的 $H$ 是一个在[多重动量](@entry_id:1129922)相空间上定义的[标量密度](@entry_id:161438)，它编码了系统的动力学信息。

### De Donder-Weyl 场方程

一旦我们获得了 DW 哈密顿量 $H$，场的动力学就由一组[一阶偏微分方程](@entry_id:178306)——**De Donder-Weyl (DW) 场方程**——所支配：
$$
\partial_\mu y^i = \frac{\partial H}{\partial p_i^\mu}
$$
$$
\partial_\mu p_i^\mu = -\frac{\partial H}{\partial y^i}
$$
第一组方程通常重现了速度和动量之间的关系（即逆[勒让德变换](@entry_id:142214)）。第二组方程则描述了[多重动量](@entry_id:1129922)的“散度”如何与哈密顿量对场变量的梯度相关联，这是动力学的核心。

一个至关重要的问题是，这个新的方程组是否与我们从变分原理得到的标准[欧拉-拉格朗日方程](@entry_id:137827)等价。答案是肯定的（对于超正则系统）。正如在问题  的分析中所揭示的，这种等价性对任何超[正则拉格朗日量](@entry_id:1130808)都成立，而不仅限于二次形式。我们可以通过对 $H = p_j^\nu y^j_\nu - L$ 求关于 $y^i$ 的偏导数来证明这一点：
$$
\frac{\partial H}{\partial y^i} = \frac{\partial p_j^\nu}{\partial y^i} y^j_\nu + p_j^\nu \frac{\partial y^j_\nu}{\partial y^i} - \frac{\partial L}{\partial y^i} - \frac{\partial L}{\partial y^j_\nu}\frac{\partial y^j_\nu}{\partial y^i}
$$
使用 $p_j^\nu = \frac{\partial L}{\partial y^j_\nu}$，第二项和第四项相互抵消。同时，由于动量 $p_j^\nu$ 是 $y^k_\sigma$ 的函数，而不是 $y^i$ 的显式函数，$\frac{\partial p_j^\nu}{\partial y^i}=0$。因此，我们得到 $\frac{\partial H}{\partial y^i} = -\frac{\partial L}{\partial y^i}$。
将此代入第二个 DW 方程，并使用动量的定义，我们得到：
$$
\partial_\mu \left( \frac{\partial L}{\partial y^i_\mu} \right) = - \left( -\frac{\partial L}{\partial y^i} \right) = \frac{\partial L}{\partial y^i}
$$
这正是[欧拉-拉格朗日方程](@entry_id:137827)。因此，DW 形式主义忠实地再现了拉格朗日理论的动力学内容。

让我们以一个具体的物理系统——[克莱因-戈登场](@entry_id:152627)（Klein-Gordon field）——为例，如问题  所示。其拉格朗日密度为：
$$
\mathcal{L} = \frac{1}{2}\left((\partial_{x}\phi)^{2} + (\partial_{y}\phi)^{2}\right) - \frac{1}{2} m^{2}\phi^{2}
$$
[多重动量](@entry_id:1129922)为 $p^x = \partial_x\phi$ 和 $p^y = \partial_y\phi$。DW 哈密顿密度为：
$$
H = p^x \partial_x\phi + p^y \partial_y\phi - \mathcal{L} = \frac{1}{2}\left((p^{x})^{2} + (p^{y})^{2}\right) + \frac{1}{2} m^{2}\phi^{2}
$$
对应的 DW 方程组是：
$$
\partial_x\phi = \frac{\partial H}{\partial p^x} = p^x
$$
$$
\partial_y\phi = \frac{\partial H}{\partial p^y} = p^y
$$
$$
\partial_x p^x + \partial_y p^y = -\frac{\partial H}{\partial \phi} = -m^2 \phi
$$
这个一阶方程组完全等价于二阶的[克莱因-戈登方程](@entry_id:153831) $(\partial_x^2 + \partial_y^2 - m^2)\phi = 0$。这个例子清晰地表明，DW 形式主义将一个[二阶偏微分方程](@entry_id:175326)转化为一个[一阶偏微分方程](@entry_id:178306)组，这在数学和数值分析中通常更易于处理。例如，在问题  中，通过限制场对 $y$ 坐标无依赖性（$\partial_y \phi=0$），该方程组沿着 $x$ 方向的特征线简化为一个常微分方程组 $\frac{d\phi}{ds} = p^x$ 和 $\frac{dp^x}{ds} = -m^2 \phi$，这恰好描述了一个[简谐振子](@entry_id:145764)。

#### 与标准哈密顿形式主义的联系

将 DW 哈密顿密度与学生们更熟悉的标准（非[协变](@entry_id:634097)）哈密顿密度进行比较是很有启发性的。[标准形式](@entry_id:153058)主义通过只对时间导数 $\partial_0\phi$ 进行[勒让德变换](@entry_id:142214)来定义[共轭动量](@entry_id:172203) $\pi = \partial \mathcal{L} / \partial(\partial_0\phi)$ 和哈密顿密度 $\mathcal{H}_{\mathrm{can}} = \pi(\partial_0\phi) - \mathcal{L}$。

问题  探讨了这两者之间的精确关系。对于一个[标量场](@entry_id:151443)，我们有 DW 哈密顿量 $\mathcal{H}_{\mathrm{DW}} = \pi^\mu \partial_\mu \phi - \mathcal{L}$ 和标准[哈密顿量](@entry_id:144286) $\mathcal{H}_{\mathrm{can}} = \pi^0 \partial_0 \phi - \mathcal{L}$（因为标[准动量](@entry_id:143609) $\pi$ 就是[多重动量](@entry_id:1129922)的时间分量 $\pi^0$）。它们之间的差值为：
$$
\Delta = \mathcal{H}_{\mathrm{DW}} - \mathcal{H}_{\mathrm{can}} = (\pi^0 \partial_0\phi + \sum_{i=1}^{n-1} \pi^i \partial_i\phi - \mathcal{L}) - (\pi^0 \partial_0\phi - \mathcal{L}) = \sum_{i=1}^{n-1} \pi^i \partial_i\phi
$$
对于[闵可夫斯基时空](@entry_id:156421)中的[标量场](@entry_id:151443) $\mathcal{L} = \frac{1}{2}\eta^{\mu\nu}\partial_\mu\phi\partial_\nu\phi - V(\phi)$，空间动量分量为 $\pi^i = \eta^{i\nu}\partial_\nu\phi = -\partial_i\phi$。因此，差值变为：
$$
\Delta = \sum_{i=1}^{n-1} (-\partial_i\phi)(\partial_i\phi) = -\sum_{i=1}^{n-1} (\partial_i\phi)^2
$$
这个简洁的结果表明，DW 哈密顿密度与标准哈密顿密度之差恰好是空间动能密度的负值。在[标准形式](@entry_id:153058)主义中，空间导数 $\partial_i\phi$ 被视为位形变量的一部分，而它们的“动能”贡献保留在哈密顿量中。相比之下，DW 形式主义将所有时空导数同等对待，并将它们都通过勒让德变换转化为动量。因此，$\mathcal{H}_{\mathrm{DW}}$ 通常被称为**协变能量密度** (covariant energy density)。

### 几何基础：多辛与多重[辛结构](@entry_id:1132759)

De Donder-Weyl 理论的优雅之处不仅在于其方程的协变性，更在于其丰富的几何结构。这些结构为[场论](@entry_id:155241)提供了一个类似于经典力学中辛几何的框架。

在[多重动量](@entry_id:1129922)相空间 $Z$ 上，我们可以定义一个典范的 $n$-形式，称为**庞加莱-嘉当 $n$-形式** (Poincaré-Cartan $n$-form) $\Theta$：
$$
\Theta = p_i^\mu dy^i \wedge \omega_\mu - H \omega
$$
其中 $\omega$ 是时空[体积形式](@entry_id:203000)，$\omega_\mu := i_{\partial/\partial x^\mu} \omega$ 是通过将 $\omega$ 与[坐标向量](@entry_id:153319)场 $\partial/\partial x^\mu$ 进行[内积](@entry_id:750660)得到的 $(n-1)$-形式。例如，在平直时空中，若 $\omega = dx^0 \wedge \dots \wedge dx^{n-1}$，则 $\omega_\mu = (-1)^\mu dx^0 \wedge \dots \wedge \widehat{dx^\mu} \wedge \dots \wedge dx^{n-1}$（其中 $\widehat{\cdot}$ 表示省略该项）。

[庞加莱-嘉当形式](@entry_id:1129851)的外微分（在符号上可能相差一个负号）定义了**多辛 $(n+1)$-形式** (multisymplectic $(n+1)$-form) $\Omega$:
$$
\Omega = -d\Theta = dp_i^\mu \wedge dy^i \wedge \omega_\mu + dH \wedge \omega
$$
根据构造，$\Omega$ 是一个[闭形式](@entry_id:272960)（$d\Omega = -d(d\Theta) = 0$），同时也是一个恰当形式。$\Omega$ 是 De Donder-Weyl 形式主义的中心几何对象。动力学方程可以通过 $\Omega$ 以一种非常几何化的方式来表述。存在一个唯一的**哈密顿[多重向量](@entry_id:203525)场** (Hamiltonian multivector field) $X_H$——这是一个 $n$-重向量场（即 $\Lambda^n TZ$ 的一个[截面](@entry_id:154995)）——它满足如下的[哈密顿方程](@entry_id:156213)：
$$
i_{X_H} \Omega = dH
$$
这个方程是经典力学中哈密顿向量场定义 $i_X \omega = dH$ 的直接推广。[场方程](@entry_id:1124935)的解恰好是这个[多重向量](@entry_id:203525)场 $X_H$ 的[积分流形](@entry_id:270062) 。

除了多辛形式 $\Omega$ 之外，还存在另一种相关的几何结构，即**多重辛结构** (polysymplectic structure)。这是一个向量丛值的 2-形式 $\hat{\Omega}$，定义在[多重动量](@entry_id:1129922)相空间上，其值域为 $\Lambda^{n-1}T^*X$。其局部表达式为：
$$
\hat{\Omega} = dy^i \wedge dp_i^\mu \otimes \omega_\mu
$$
这个结构在[多重动量](@entry_id:1129922)相空间的每个“垂直”方向（即固定时空点 $x$ 的纤维）上都定义了一个[辛结构](@entry_id:1132759)。它可以被看作是为每个时空方向 $\mu$ 都配备了一个[辛形式](@entry_id:165896) $\omega_\mu$。$\hat{\Omega}$ 在某种意义上是“非退化”的：任何非零的垂直向量 $v$（即没有 $\partial/\partial x^\mu$ 分量的向量）与 $\hat{\Omega}$ 的[内积](@entry_id:750660)都不会为零 。

总结一下，多辛形式 $\Omega$ 是一个标量值的 $(n+1)$-形式，它通过哈密顿[多重向量](@entry_id:203525)场统一编码了所有[动力学方程](@entry_id:751029)。而多重辛形式 $\hat{\Omega}$ 则是一个丛值 2-形式，它在相空间的纤维上提供了辛几何的结构。

### 应用与联系

DW 形式主义的价值不仅在于其理论的优美，还在于它与其他物理和数学概念的深刻联系。

#### 与协变相空间的关系

另一个著名的处理场论哈密顿动力学的方法是**[协变](@entry_id:634097)相空间** (Covariant Phase Space, CPS) 形式主义。CPS 的核心思想是在所有[场方程](@entry_id:1124935)解的无限维空间上直接定义一个[辛结构](@entry_id:1132759)。这个辛 2-形式 $\omega_{CPS}$ 是通过在一个柯西[超曲面](@entry_id:159491) $\Sigma$ 上对一个守恒的**前辛流** (presymplectic current) $J^\mu$ 进行积分得到的。

问题  探讨了 DW 和 CPS 之间的基本联系。这个联系正是通过多[辛形式](@entry_id:165896) $\Omega$ 建立的。考虑两个独立的场变分 $\delta_1$ 和 $\delta_2$，它们可以被看作是场历史空间中的[切向量](@entry_id:265494)。这些变分可以被提升为[多重动量](@entry_id:1129922)相空间上的垂直向量场。将多辛形式 $\Omega$ 与这两个提升后的向量场进行[内积](@entry_id:750660)，得到一个 $(n-1)$-形式。令人惊奇的是，这个 $(n-1)$-形式恰好就是协变相空间中的前辛流 $J = J^\mu \omega_\mu$。具体来说：
$$
i_{\delta_2}i_{\delta_1}\Omega \propto (\delta_1 p_a^\mu \wedge \delta_2 y^a) \omega_\mu
$$
右侧正是前辛流密度 $J^\mu = \delta_1 p_a^\mu \wedge \delta_2 y^a$ 的表达式。因此，[协变](@entry_id:634097)相空间的[辛形式](@entry_id:165896)可以被看作是 De Donder-Weyl 多辛形式在场[解空间](@entry_id:200470)上的“投影”。

#### 边界结构与辛通量

这种联系在研究边界效应和[守恒量](@entry_id:161475)时尤为重要。前辛流 $J^\mu$ 的守恒律 $\partial_\mu J^\mu=0$（在解上成立）保证了通过对它在一个闭合时空区域的边界上积分所定义的“辛通量”是守恒的。

问题  提供了一个计算这种通量的具体例子。对于[克莱因-戈登场](@entry_id:152627)，前辛流密度为 $\omega^\mu = (\delta_1 p^\mu)\delta_2\phi - (\delta_2 p^\mu)\delta_1\phi$。考虑两个[平面波解](@entry_id:195230)的微扰 $\delta_1\phi$ 和 $\delta_2\phi$，我们可以计算出流过一个时空区域边界的辛通量。例如，流过 $x=0$ 这条边界线的通量为：
$$
\Phi_{x=0} = \int \omega^\mu n_\mu dt = \int (-\omega^1) dt = \int \left[ (\partial_x\delta_2\phi)\delta_1\phi - (\partial_x\delta_1\phi)\delta_2\phi \right] dt
$$
对于给定的[平面波](@entry_id:189798)微扰，这个积分给出了一个与场振幅和相位差相关的具体数值，例如 $-ABkT\sin(\varphi)$ 。这个量是守恒的，并且在[量子场论](@entry_id:138177)中与粒子数的定义密切相关。

#### 线性化与微扰的[辛结构](@entry_id:1132759)

在物理学中，我们常常研究在一个已知的经典背景解（如真空或一个[孤子](@entry_id:145656)）附近的微小扰动。DW 形式主义可以很自然地应用于这个情景。我们可以将 DW 方程在背景解附近线性化，得到关于微扰 $\delta\phi$ 和 $\delta p^\mu$ 的[线性方程组](@entry_id:148943)。

更重要的是，协变相空间的[辛结构](@entry_id:1132759)可以直接应用于这个线性化的微扰空间。如问题  所示，我们可以通过在一个固定的时间切片上对辛流的时间分量 $\omega^t$ 进[行空间](@entry_id:148831)积分，来定义微扰空间上的辛形式 $\Omega(\delta_1, \delta_2)$：
$$
\Omega(\delta_1, \delta_2) = \int \omega^t(\delta_1, \delta_2) d^{n-1}x = \int \left[ (\partial_t\delta_1\phi)\delta_2\phi - (\partial_t\delta_2\phi)\delta_1\phi \right] d^{n-1}x
$$
这个[辛形式](@entry_id:165896)是微扰动力学的基础，它为场的量子化（例如，通过定义创生和[湮灭算符](@entry_id:165390)的[对易关系](@entry_id:136780)）提供了经典对应物。计算特定模式（例如空间均匀模式）的[辛形式](@entry_id:165896)，可以得到如 $-ABmL$ 这样的结果 ，这揭示了不同振荡模式之间的辛[正交关系](@entry_id:145540)。

### 高等主题：[代数结构](@entry_id:137052)与约束系统

De Donder-Weyl 形式主义的威力也体现在它能够优雅地处理更复杂的系统和结构。

#### 泊松-盖尔斯滕哈伯代数

多辛形式 $\Omega$ 不仅定义了动力学，还在微分形式的空间上诱导了丰富的[代数结构](@entry_id:137052)。这是一种分级的[泊松括号](@entry_id:151133)，称为**泊松-盖尔斯滕哈伯括号** (Poisson-Gerstenhaber bracket)。

对于一个水平 $(n-1)$-形式 $f$（即只含 $dx^\mu$ 的形式），我们可以定义一个与之关联的垂直向量场 $X_f$，其定义关系为 $i_{X_f} \Omega = df$。然后，两个这样的水平形式 $f$ 和 $g$ 之间的括号被定义为：
$$
\{f,g\} := i_{X_f} dg
$$
这个运算的结果仍然是一个水平 $(n-1)$-形式，并且它满足分级的[雅可比恒等式](@entry_id:140480)。问题  提供了一个计算这种括号的例子。对于两个 [1-形式](@entry_id:270392) $f=y\,dx^1$ 和 $g=p^0\,dx^1$，通过计算，我们发现它们的括号是一个非常简单的形式：
$$
\{f, g\} = \{y\,dx^1, p^0\,dx^1\} = dx^1
$$
这揭示了场变量 $y$ 和动量分量 $p^0$ 之间深刻的对偶关系，这种关系被编码在由 $\Omega$ 诱导的代数结构中。

#### [奇异系统](@entry_id:140614)与约束

许多重要的物理理论，如电磁学和[杨-米尔斯理论](@entry_id:137401)，都是**[奇异系统](@entry_id:140614)** (singular systems)，它们的[拉格朗日量](@entry_id:174593)的[勒让德变换](@entry_id:142214)是不可逆的。这意味着我们无法将所有的速度 $y^i_\mu$ 都表示为动量的函数。相反，动量的定义本身就会在[多重动量](@entry_id:1129922)相空间上施加**主约束** (primary constraints)。

问题  使用一个包含乘子场的拉格朗日量 $\mathcal{L} = \lambda_{\mu}(\partial_{\mu} y - C_{\mu}(y))$ 来阐明了这一点。计算其[多重动量](@entry_id:1129922)得到：
- 与 $y$ 共轭的动量：$p^\mu_y = \frac{\partial \mathcal{L}}{\partial(\partial_\mu y)} = \lambda_\mu$。
- 与 $\lambda_\nu$ 共轭的动量：$\pi^{\mu\nu} = \frac{\partial \mathcal{L}}{\partial(\partial_\mu \lambda_\nu)} = 0$。

这两个关系 $p^\mu_y = \lambda_\mu$ 和 $\pi^{\mu\nu}=0$ 正是该系统的主约束。它们定义了[多重动量](@entry_id:1129922)相空间中的一个子流形，所有物理态都必须位于其上。

DW [哈密顿量](@entry_id:144286)的表达式在这种情况下变得特别有启发性：
$$
\mathcal{H} = p^{\mu}_{y}\partial_{\mu} y + \pi^{\mu\nu}\partial_{\mu} \lambda_{\nu} - \mathcal{L} = (p^{\mu}_{y} - \lambda_{\mu})\partial_{\mu} y + \pi^{\mu\nu}\partial_{\mu} \lambda_{\nu} + \lambda_{\mu} C_{\mu}(y)
$$
我们可以看到，[哈密顿量](@entry_id:144286)自然地分成了两部分：一部分是主约束与速度的乘积，另一部分 $\lambda_{\mu} C_{\mu}(y)$ 则不依赖于速度。那些无法被反解的速度（$\partial_\mu y$ 和 $\partial_\mu \lambda_\nu$）的任意性反映了理论的**[规范自由度](@entry_id:160491)** (gauge freedom)。

处理这种情况的系统方法是所谓的**多重狄拉克约化** (multi-Dirac reduction)。我们首先将理论限制在主约束子流形上。在此[子流形](@entry_id:159439)上，哈密顿量中与速度相关的项都为零。剩下的部分是**[约化哈密顿量](@entry_id:1130752)** $\mathcal{H}_{\mathrm{red}}$。在我们的例子中，我们还需要使用约束 $p^\mu_y = \lambda_\mu$ 来消去乘子场 $\lambda_\mu$，最终得到：
$$
\mathcal{H}_{\mathrm{red}}(y, p) = p^\mu_y C_\mu(y)
$$
这个[约化哈密顿量](@entry_id:1130752)只依赖于“物理”的自由度 $(y, p^\mu_y)$，并正确地生成了它们的动力学方程。这个过程展示了 DW 形式主义如何系统地处理具有[规范对称性](@entry_id:136438)的[约束理论](@entry_id:1122946)，这是其在现代[场论](@entry_id:155241)中应用的一个关键优势。

总之，De Donder-Weyl 形式主义为[经典场论](@entry_id:149475)提供了一个强大而优美的[协变](@entry_id:634097)哈密顿框架。它不仅再现了正确的动力学，还揭示了深刻的几何与代数结构，为我们理解场论的对称性、守恒律和量子化提供了坚实的基础。