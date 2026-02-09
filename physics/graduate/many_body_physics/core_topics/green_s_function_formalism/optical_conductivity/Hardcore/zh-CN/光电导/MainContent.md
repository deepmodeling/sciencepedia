## 引言
光电导率是描述物质如何与电磁场相互作用的核心物理量，它不仅决定了材料的光学外观，如颜色和透明度，更深刻地反映了其内部的微观电子结构和动力学过程。理解光电导率是连接凝聚态物理基础理论与光电子技术应用的关键。然而，从微观的量子态和相互作用出发，推导出宏观可测量的光学响应，并反过来利用光谱来解读复杂的材料性质，是该领域的核心挑战。本文旨在系统地阐明这一联系，为读者提供一个从理论到应用的完整视角。

为了实现这一目标，本文将分为三个核心部分。在“原理与机制”一章中，我们将建立光电导率的理论基础，从经典的Drude-Lorentz模型到量子力学的Kramers-Kronig关系和f-求和规则。接下来，“应用与交叉学科联系”一章将展示这些原理如何应用于表征各类材料，从传统半导体中的声子和带隙，到石墨烯、超导体等量子材料中的奇异激发。最后，“动手实践”部分将通过具体的计算问题，指导读者亲手应用理论，加深对光电导率谱的理解。通过这一结构化的学习路径，读者将能够掌握光电导率这一强大工具，从而洞悉物质的光学奥秘。

## 原理与机制

本章旨在深入探讨光电导率的物理原理和其背后的微观机制。我们将从电导率与介电函数之间的基本关系出发，构建描述不同类型材料中载流子响应的理论模型，并阐明如何通过光电导率探测材料中的元激发。最后，我们将介绍由因果律和守恒律决定的普适性原理，如Kramers-Kronig关系和f-求和规则，并简要讨论该领域的一些前沿进展。

### 基本关系：电导率与介电函数

在宏观电动力学中，材料对时谐电磁场 $\mathbf{E}(t) = \text{Re}[\mathbf{E}(\omega)e^{-i\omega t}]$ 的线性响应可以通过两种等价的方式来描述。一种是通过复介电函数 $\epsilon(\omega)$，它将电位移矢量 $\mathbf{D}(\omega)$ 与电场 $\mathbf{E}(\omega)$ 联系起来，即 $\mathbf{D}(\omega) = \epsilon_0 \epsilon(\omega) \mathbf{E}(\omega)$。这里，$\epsilon_0$ 是真空介电常数，而 $\epsilon(\omega)$ 描述了材料内部所有电荷（包括束缚电荷和自由电荷）的极化和传导效应的总和。

另一种描述方式是引入复光电导率 $\sigma(\omega)$，它定义了由外电场驱动的自由载流子所形成的传导电流密度 $\mathbf{J}_{\text{free}}(\omega)$ 与电场的关系：$\mathbf{J}_{\text{free}}(\omega) = \sigma(\omega) \mathbf{E}(\omega)$。

这两种描述通过麦克斯韦-安培定律联系在一起。在频域中，该定律写作：
$$ \nabla \times \mathbf{H}(\omega) = \mathbf{J}_{\text{free}}(\omega) - i\omega \mathbf{D}(\omega) $$
如果我们希望将所有材料响应都吸收到一个有效的介电函数 $\epsilon(\omega)$ 中，我们可以定义一个总的位移场 $\mathbf{D}_{\text{tot}}(\omega) = \epsilon_0 \epsilon(\omega) \mathbf{E}(\omega)$，此时安培定律的形式变为 $\nabla \times \mathbf{H}(\omega) = -i\omega \mathbf{D}_{\text{tot}}(\omega)$。将两种形式进行比较，我们得到：
$$ -i\omega \epsilon_0 \epsilon(\omega) \mathbf{E}(\omega) = \sigma(\omega) \mathbf{E}(\omega) - i\omega \mathbf{D}_{\text{bound}}(\omega) $$
其中 $\mathbf{D}_{\text{bound}}(\omega)$ 是由束缚电荷极化产生的位移场。在许多情况下，特别是在研究特定频率范围内的自由载流子响应时，将束缚电荷的贡献视为一个与频率无关或缓慢变化的背景是方便的。例如，在红外到可见光频段，远离晶格振动和高能带间跃迁的频率，束缚电子的极化贡献可以近似为一个常数，即高频介电常数 $\epsilon_\infty$ [@problem_id:3008363]。此时，我们可以将总的介电函数分解为背景项和自由载流子电导贡献项：
$$ \epsilon(\omega) = \epsilon_\infty + i \frac{\sigma(\omega)}{\epsilon_0 \omega} $$
这个关系是理解材料光学性质的基石。它表明，电导率的实部（代表吸收）贡献于介电函数的虚部，而电导率的虚部（代表电感或电容性响应）贡献于介电函数的实部。这个关系允许我们根据一个响应函数推导出另一个 [@problem_id:1759024] [@problem_id:1796629]。例如，给定一个具有背景介电常数 $\epsilon_b$ 的材料，其自由电子响应由电导率 $\sigma(\omega)$ 描述，总的相对介电函数就是 $\epsilon_r(\omega) = \epsilon_b + i \sigma(\omega)/(\omega\epsilon_0)$ [@problem_id:608244]。

### 光电导率模型

为了计算光电导率，我们需要建立描述材料中载流子在外场驱动下运动的微观模型。

#### Drude模型（自由载流子）

最简单的模型是Drude模型，它将金属中的传导电子视为经典的、在离子实构成的背景中自由运动的气体。电子在电场作用下加速，并通过与晶格缺陷、杂质或声子的碰撞而损失动量。这种碰撞过程被唯象地描述为一个弛豫时间 $\tau$。一个电子的平均运动方程为：
$$ m \frac{d\mathbf{v}(t)}{dt} + \frac{m}{\tau} \mathbf{v}(t) = q\mathbf{E}(t) $$
其中 $m$ 和 $q$ 分别是电子的有效质量和电荷。对于时谐电场 $\mathbf{E}(t) = \mathbf{E}(\omega) e^{-i\omega t}$，我们可以求得稳态解 $\mathbf{v}(t) = \mathbf{v}(\omega) e^{-i\omega t}$。将该解代入运动方程，得到：
$$ (-i\omega m + \frac{m}{\tau}) \mathbf{v}(\omega) = q\mathbf{E}(\omega) $$
由此可得速度的复振幅 $\mathbf{v}(\omega) = \frac{q\tau/m}{1-i\omega\tau}\mathbf{E}(\omega)$。电流密度由 $\mathbf{J}(\omega) = nq\mathbf{v}(\omega)$ 给出，其中 $n$ 是电子数密度。因此，我们得到Drude模型的复电导率 [@problem_id:814678]：
$$ \sigma(\omega) = \frac{nq^2\tau/m}{1-i\omega\tau} = \frac{\sigma_0}{1-i\omega\tau} $$
其中 $\sigma_0 = nq^2\tau/m$ 是直流($\omega=0$)电导率。

Drude电导率的实部，$\sigma_1(\omega) = \text{Re}[\sigma(\omega)]$，与能量吸收直接相关：
$$ \sigma_1(\omega) = \frac{\sigma_0}{1 + (\omega\tau)^2} $$
这是一个洛伦兹型的函数，在 $\omega=0$ 时取最大值 $\sigma_0$，并随着频率增加而单调下降。吸收的半高全宽由弛豫速率 $1/\tau$ 决定。例如，在频率 $\omega = 2/\tau$ 处，吸收会下降到直流值的五分之一 [@problem_id:1776391]。

尽管Drude模型非常成功地解释了金属的直流导电性和低频光学性质，但它有一个显著的缺陷：它预测吸收随频率单调递减，无法解释在许多金属中观察到的位于特定高频处的尖锐吸收峰。这些吸收峰源于电子在不同能带之间的量子跃迁（即**带间跃迁**），这是Drude模型的经典图像所无法描述的 [@problem_id:1776391]。

#### Lorentz模型（束缚载流子）

为了描述束缚电荷的响应，例如绝缘体中原子内的电子或极性晶体中的离子，我们可以使用Lorentz模型。该模型将每个束缚单元视为一个受阻尼的谐振子。以极性晶体中的一个光学声子模式为例，正负离子的相对位移 $u$ 在外电场 $E$ 作用下的运动方程可以写为 [@problem_id:1176950]：
$$ \mu \left( \frac{d^2u}{dt^2} + \gamma \frac{du}{dt} + \omega_{TO}^2 u \right) = q^* E(t) $$
这里，$\mu$ 是离子对的约化质量，$q^*$ 是有效电荷，$\omega_{TO}$ 是横向光学（TO）声子的固有谐振频率，$\gamma$ 是唯象的阻尼系数。

通过求解这个受迫振动方程，我们可以得到位移 $u(\omega)$，并进一步计算出由离子振动产生的极化电流密度 $J(\omega) = N q^* (-i\omega u(\omega))$，其中 $N$ 是单位体积内的离子对数目。最终得到声子贡献的电导率：
$$ \sigma_{\text{ph}}(\omega) = \frac{-i\omega N (q^*)^2 / \mu}{\omega_{TO}^2 - \omega^2 - i\omega\gamma} = \frac{-i\omega \epsilon_0 \omega_p^2}{\omega_{TO}^2 - \omega^2 - i\omega\gamma} $$
其中 $\omega_p^2 = N(q^*)^2/(\mu\epsilon_0)$ 是离子等离子体频率。与Drude模型不同，Lorentz模型的电导率（及其对应的吸收）在固有频率 $\omega \approx \omega_{TO}$ 处表现出明显的共振增强。这成功地描述了红外波段的声子吸收峰。

#### 推广与量子模型

经典模型可以通过引入更复杂的相互作用来推广。例如，我们可以考虑阻尼力不仅与当前速度有关，还与过去的速度历史有关，这导致了带有**记忆核函数** $\Gamma(t-t')$ 的广义运动方程 [@problem_id:1058802]：
$$ m \frac{d\mathbf{v}(t)}{dt} + m \int_{-\infty}^{t} \Gamma(t-t') \mathbf{v}(t') dt' = q \mathbf{E}(t) $$
求解这类方程会得到更复杂的频率依赖性，能够描述非马尔可夫过程。

然而，对材料光学性质的完整描述最终需要量子力学。在量子理论中，光电导率是通过计算在外场微扰下系统状态之间的跃迁矩阵元来获得的。一个核心的量子工具是**Lindhard函数**，它在随机相近似（RPA）的框架下描述了电子气的密度响应函数 $\chi_0(\mathbf{q}, \omega)$。通过这个函数，我们可以计算出与波矢 $\mathbf{q}$ 和频率 $\omega$ 相关的电导率。例如，在长波极限（$\mathbf{q} \to 0$）下，三维电子气的纵向电导率可以被推导出来，其结果为 $\sigma_L(\omega) = i n e^2/(m \omega)$ [@problem_id:1176923]。这个结果与无碰撞Drude模型 ($\tau \to \infty$) 的结果一致，展示了量子与经典描述在特定极限下的对应关系。

### 探测元激发

光电导率是研究材料中元激发的强大探针，不同的实验技术可以揭示不同类型的激发。

#### 纵向与横向响应：等离激元与光学吸收

理解不同实验探测何种响应至关重要。光（横向电磁波）与材料相互作用，其吸收主要由电导率实部 $\sigma_1(\omega)$ 或等价地，介电函数虚部 $\epsilon_2(\omega)$ 决定。因此，光学吸收实验探测的是**横向响应**。

另一方面，像电子能量损失谱（EELS）这样的技术，入射的带电粒子主要激发材料中的**纵向**电场波动。一个自持的纵向集体振荡模式存在的条件是介电函数为零，即 $\epsilon(\mathbf{q}, \omega) = 0$。这是因为在没有外部源的情况下，纵向高斯定律 $\nabla \cdot \mathbf{D} = 0$ 在傅里叶空间中变为 $\mathbf{q} \cdot \mathbf{D}(\mathbf{q}, \omega) = \epsilon(\mathbf{q}, \omega) \mathbf{q} \cdot \mathbf{E}(\mathbf{q}, \omega) = 0$。要存在非零的纵向电场，必须满足 $\epsilon(\mathbf{q}, \omega) = 0$ [@problem_id:3010224]。

EELS实验测量的物理量是**能量损失函数** $L(\omega) = \text{Im}[-1/\epsilon(\omega)]$。我们可以将其展开为：
$$ L(\omega) = \text{Im}\left[-\frac{1}{\epsilon_1(\omega) + i\epsilon_2(\omega)}\right] = \frac{\epsilon_2(\omega)}{\epsilon_1(\omega)^2 + \epsilon_2(\omega)^2} $$
从这个表达式可以看出，当 $\epsilon_1(\omega)$ 趋于零且 $\epsilon_2(\omega)$ 很小时，能量损失函数会出现一个尖锐的峰。这个峰就对应着纵向集体激发，即**等离激元** (plasmon)。

对于一个简单的金属，其介电函数可以用包含背景极化 $\epsilon_\infty$ 的Drude模型描述 [@problem_id:1176973]：
$$ \epsilon(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega^2 + i\gamma\omega} $$
其中 $\omega_p$ 是等离子体频率。其实部为 $\epsilon_1(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega^2 + \gamma^2}$。在阻尼 $\gamma$ 很小的情况下，$\epsilon_1(\omega) = 0$ 的解约为 $\omega^2 \approx \omega_p^2 / \epsilon_\infty$。这个频率，即**体等离激元频率**，正是能量损失函数的峰值所在 [@problem_id:608244] [@problem_id:3010224]。值得强调的是，光学吸收谱（正比于 $\sigma_1(\omega)$ 或 $\epsilon_2(\omega)$）在等离激元频率处通常没有峰值，反而由于 $\epsilon_1  0$ 而表现出高反射率。

当考虑波矢 $q$ 的依赖性时，等离激元的频率会发生变化，即存在**色散关系** $\omega(q)$。利用流体动力学方法，并考虑费米气体的量子压力，可以推导出一维电子气的等离激元色散关系，它包含了与 $q^2$ 成正比的量子压力修正项 [@problem_id:1121079]。

#### 声子与Lyddane-Sachs-Teller关系

在离子晶体中，介电函数在红外波段由声子主导。一个简化的无阻尼模型为：
$$ \epsilon(\omega) = \epsilon_\infty + \frac{\Omega_p^2}{\omega_T^2 - \omega^2} $$
其中 $\omega_T$ 是横向光学（TO）声子频率，$\Omega_p$ 是离子等离子体频率。TO声子是横向模式，能与光子直接耦合，因此 $\epsilon(\omega)$ 在 $\omega = \omega_T$ 处发散，对应一个吸收峰。

纵向光学（LO）声子是纵向模式，其频率 $\omega_L$ 满足纵向模式的条件 $\epsilon(\omega_L) = 0$。将此条件代入上式，我们可以求解出 $\Omega_p^2$ [@problem_id:1121128]：
$$ 0 = \epsilon_\infty + \frac{\Omega_p^2}{\omega_T^2 - \omega_L^2} \implies \Omega_p^2 = \epsilon_\infty (\omega_L^2 - \omega_T^2) $$
将这个结果代回 $\epsilon(\omega)$ 的表达式，并考虑静态介电常数 $\epsilon_s = \epsilon(0) = \epsilon_\infty + \Omega_p^2/\omega_T^2$，经过简单的代数运算，我们可以得到一个深刻的关系：
$$ \frac{\omega_L^2}{\omega_T^2} = \frac{\epsilon_s}{\epsilon_\infty} $$
这就是著名的**Lyddane-Sachs-Teller (LST) 关系**。它将晶体中两种基本晶格振动模式的频率与两个宏观的介电常数联系起来，是固体物理学中的一个经典成果。

### 基本原理：因果律与求和规则

光电导率作为线性响应函数，必须遵循一些由物理基本定律决定的普适性规则。

#### 因果律与Kramers-Kronig关系

一个基本的物理原理是**因果律**：系统的响应不能先于施加的微扰。在时域中，这意味着响应函数 $R(t-t')$ 对于 $t  t'$ 必须为零。这个看似简单的物理要求在频域中具有深刻的数学后果。根据Titchmarsh定理，一个满足因果律的响应函数，其傅里叶变换（如 $\sigma(\omega)$ 或 $\epsilon(\omega)$）在复频率平面的上半平面必须是解析的 [@problem_id:814678]。

一个复变函数在上半平面的解析性意味着它的实部和虚部不是独立的，而是通过积分变换相互关联。这种关系就是**Kramers-Kronig (KK) 关系**。对于介电函数 $\epsilon(\omega) = \epsilon_1(\omega) + i\epsilon_2(\omega)$，其关系式为：
$$ \epsilon_1(\omega) - 1 = \frac{2}{\pi} \mathcal{P} \int_0^{\infty} \frac{\omega' \epsilon_2(\omega')}{\omega'^2 - \omega^2} d\omega' $$
$$ \epsilon_2(\omega) = -\frac{2\omega}{\pi} \mathcal{P} \int_0^{\infty} \frac{\epsilon_1(\omega')-1}{\omega'^2 - \omega^2} d\omega' $$
其中 $\mathcal{P}$ 表示柯西主值积分。这些关系表明，如果我们知道了材料在所有频率下的吸收谱（$\epsilon_2(\omega)$），原则上我们就可以计算出它在任意频率下的色散（$\epsilon_1(\omega)$），反之亦然。

作为一个实际应用，我们可以利用KK关系从一个理想化的吸收谱计算静态介电常数 $\epsilon_s = \epsilon_1(0)$。假设一个半导体的吸收谱由一个激子吸收的$\delta$函数和一个带间吸收的矩形函数组成，通过对 $\epsilon_2(\omega)/\omega$ 进行积分，就可以得到 $\epsilon_1(0)$ 的值 [@problem_id:1121130]。

#### f-求和规则

求和规则是关于响应函数积分的另一个基本约束，它通常与系统的守恒律有关。对于光电导率，最重要的求和规则是**f-求和规则**（或光学求和规则），它关联了电导率实部的总积分与系统中的载流子密度和质量。该规则可以写作：
$$ \int_0^\infty \sigma_1(\omega) d\omega = \frac{\pi n e^2}{2m} $$
这个积分面积，被称为**光谱权重**，是一个不依赖于相互作用细节的常数，仅由系统中总的载流子数密度 $n$ 决定。

f-求和规则可以通过多种方式导出。一种严谨的方法是考察Kramers-Kronig关系在 $\omega \to \infty$ 极限下的行为。在高频极限下，任何系统的介电函数都趋近于自由电子气的形式：$\epsilon(\omega) \approx 1 - \omega_p^2/\omega^2$，其中 $\omega_p^2 = ne^2/(m\epsilon_0)$。将此渐近行为与KK关系相结合，就可以推导出上述积分值 [@problem_id:1159033]。

我们也可以通过对具体模型直接积分来验证该规则。例如，对Lorentz振子模型的 $\sigma_1(\omega)$ 进行积分，尽管被积函数形式复杂，依赖于共振频率 $\omega_0$ 和阻尼 $\gamma$，但积分的最终结果却神奇地与这些参数无关，精确地等于求和规则给出的值 [@problem_id:1121127]。这清晰地展示了求和规则的普适性。

在量子模型中，f-求和规则同样成立，并能提供深刻的物理洞见。例如，对于一维紧束缚模型，光谱权重与系统哈密顿量的基态期望值 $\langle H \rangle_0$ 直接相关：$\int_0^\infty \sigma_1(\omega) d\omega = -C \langle H \rangle_0$，其中 $C$ 是一个常数。这表明，通过测量总的光学吸收，可以获得关于系统基态能量的信息 [@problem_id:1176924]。

### 高级与前沿主题

光电导的研究领域不断发展，涌现出许多超出Drude-Lorentz图像的前沿方向。

#### 乱序系统：普适介电响应

在玻璃、非晶半导体等结构无序的材料中，载流子的输运机制是**跳跃电导**。实验发现，这类材料的交流电导率在很宽的频率范围内遵循一个经验性的幂律，即**Jonscher普适介电响应 (UDR)**：
$$ \sigma'(\omega) = \sigma_0 + A\omega^n $$
其中指数 $n$ 通常在 $0  n  1$ 之间。这种亚线性（sublinear）的频率依赖性与无序系统中载流子的反常扩散（subdiffusion）密切相关。微观上，这可以通过具有幂律形式等待时间分布的连续时间随机行走（CTRW）模型来解释 [@problem_id:2814203]。UDR的一个关键特征是，幂指数 $n$ 对温度依赖很弱，而系数 $A$ 则通常表现出强烈的热激活行为，反映了跳跃率的温度依赖性。

#### 非线性光电导

当外加电场非常强时，材料的响应不再是线性的，需要用高阶电导率或极化率来描述。例如，由电场二次方诱导的极化项 $P^{(2)}$ 与二阶非线性极化率 $\chi^{(2)}$ 相关。一个产生二阶非线性效应的必要条件是材料缺乏中心反演对称性。一个典型的例子是**二次谐波产生 (SHG)**，即频率为 $\omega$ 的入射光在材料中产生频率为 $2\omega$ 的出射光。这种效应的微观根源在于系统势能的非谐性。例如，对于一个具有立方非谐项 $U(x) \propto x^3$ 的量子谐振子，通过微扰论可以计算出其二阶极化率 $\alpha^{(2)}$ [@problem_id:1176936]。

#### 几何与拓扑效应

在现代凝聚态物理中，电子的几何相位（如Berry相位）扮演着越来越重要的角色。在某些具有特定对称性破缺（如时间反演对称但空间反演对称破缺）的材料中，电子能带的**Berry曲率**在动量空间中可以形成非零的**Berry曲率偶极矩 (BCD)**。这个BCD是导致非线性霍尔效应等新奇光电现象的关键。例如，在一个倾斜的、有质量的二维狄拉克费米子体系中，可以计算出其BCD，它依赖于化学势的位置 [@problem_id:1176931]。这个BCD进而决定了一个二阶直流霍尔电导率 $\sigma_{yxx}(0; \omega, -\omega)$，它描述了在交流电场作用下产生横向直流电流的效应。这类由能带几何结构决定的光电响应是当前研究的热点领域。