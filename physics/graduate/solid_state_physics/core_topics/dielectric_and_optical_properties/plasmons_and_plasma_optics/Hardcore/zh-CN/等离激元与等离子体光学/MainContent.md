## 引言
等离激元（Plasmon）是金属或半导体中自由电子气的集体振荡，是光与物质在纳米尺度上相互作用的核心媒介。通过激发和调控等离激元，科学家们能够将光能束缚在远小于衍射极限的空间内，产生巨大的局域场增强和新颖的光学效应。理解这些集体激发如何产生、如何被操控，以及它们独特的物理性质如何转化为颠覆性技术，是现代凝聚态物理与纳米光子学的核心课题。

本文旨在系统性地构建等离激元物理的知识框架，带领读者从基本原理走向前沿应用。在“**原理与机制**”一章中，我们将从经典的Drude模型出发，逐步建立体等离激元、表面等离激元（SPP）和局域表面等离激元（LSPR）的物理图像，并探讨空间色散、混合模式等高级概念。接着，在“**应用与交叉学科联系**”一章中，我们将展示这些基本原理如何在纳米光子学、生物传感、材料科学乃至量子信息等前沿领域中催生出多样化的应用。最后，“**动手实践**”部分将通过一系列计算问题，巩固和深化读者对核心概念的理解。通过这一结构化的学习路径，读者将能够全面掌握等离激元学的理论基础和应用前景。

## 原理与机制

### 自由电子气的介电函数：Drude 模型

理解等离激元物理的出发点是建立一个描述金属中传导电子对电磁场响应的模型。最基础且富有洞察力的模型是 **Drude 模型**，它将金属中的传导电子（或称电子气）视为一种经典粒子气体，这些粒子在固定的正离子晶格背景中自由运动，并会与晶格缺陷、声子或其他电子发生碰撞。

在交变电场 $\mathbf{E}(t) = \mathbf{E}_0 e^{-i\omega t}$ 的驱动下，一个电子的经典运动方程可以写作：
$$ m \frac{d\mathbf{v}}{dt} = -e\mathbf{E} - m\gamma \mathbf{v} $$
其中 $m$ 是电子有效质量，$-e$ 是电子电荷，$\mathbf{v}$ 是电子相对于晶格的平均漂移速度，$\gamma$ 是一个唯象的**阻尼率**或**碰撞频率**，它描述了电子动量因碰撞而弛豫的速率。在稳态下，速度的解为 $\mathbf{v}(t) = \mathbf{v}_0 e^{-i\omega t}$，代入上式可得：
$$ \mathbf{v} = \frac{-e\mathbf{E}}{m(-i\omega + \gamma)} = \frac{ie\mathbf{E}}{m(\omega + i\gamma)} $$
由此产生的电流密度 $\mathbf{J} = -ne\mathbf{v}$（其中 $n$ 是电子数密度）与电场通过电导率 $\sigma(\omega)$ 联系起来，$\mathbf{J} = \sigma(\omega)\mathbf{E}$，因此频率依赖的电导率为：
$$ \sigma(\omega) = \frac{ne^2}{m(\gamma - i\omega)} = \frac{ne^2\tau}{m(1 - i\omega\tau)} $$
其中 $\tau = 1/\gamma$ 是平均碰撞时间。

在电动力学中，材料的光学响应通常由其介电函数 $\epsilon(\omega)$ 描述，它通过关系式 $\epsilon(\omega) = \epsilon_b + \frac{i\sigma(\omega)}{\omega\epsilon_0}$ 与电导率相关联。这里的 $\epsilon_0$ 是真空介电常数，$\epsilon_b$ 是由束缚的芯层电子贡献的背景介电常数，通常在感兴趣的频率范围内近似为常数，记作 $\epsilon_\infty$。将 Drude 电导率代入，我们得到 Drude 介电函数：
$$ \epsilon(\omega) = \epsilon_\infty - \frac{ne^2}{m\epsilon_0} \frac{1}{\omega(\omega + i\gamma)} $$
我们定义**体等离激元频率** (bulk plasma frequency) $\omega_p$ 为：
$$ \omega_p^2 = \frac{ne^2}{m\epsilon_0} $$
$\omega_p$ 是电子气集体振荡的自然频率，是一个仅由电子密度和有效质量决定的内禀材料参数。于是，Drude 介电函数可以紧凑地写作：
$$ \epsilon(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega(\omega + i\gamma)} $$
该复数函数可以分解为实部 $\epsilon'$ 和虚部 $\epsilon''$：
$$ \epsilon'(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega^2 + \gamma^2} $$
$$ \epsilon''(\omega) = \frac{\gamma\omega_p^2}{\omega(\omega^2 + \gamma^2)} $$
$\epsilon'(\omega)$ 描述了材料的极化响应，而 $\epsilon''(\omega)$ 描述了能量的吸收或耗散。在低频极限下 ($\omega \to 0$)，$\epsilon'(\omega)$ 趋于一个大的负值，而 $\epsilon''(\omega)$ 发散，这反映了金属的直流电导特性。在高频极限下 ($\omega \to \infty$)，$\epsilon'(\omega) \to \epsilon_\infty$，$\epsilon''(\omega) \to 0$，金属变得像透明的电介质。

### 集体激发：体等离激元

电磁波在介质中的传播模式由麦克斯韦方程组决定。对于纵向波（电场平行于波矢 $\mathbf{q}$），亥姆霍兹方程要求 $\epsilon(\mathbf{q}, \omega) \mathbf{E} = 0$。要存在非平庸解 ($\mathbf{E} \neq 0$)，必须满足条件 $\epsilon(\mathbf{q}, \omega) = 0$。在 Drude 模型的长波极限下（$q \to 0$，介电函数不依赖于 $q$），纵向集体激发的条件简化为 $\epsilon(\omega) = 0$。

让我们首先考虑一个理想的无碰撞电子气，即阻尼 $\gamma = 0$。此时介电函数为实数：
$$ \epsilon(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega^2} $$
设置 $\epsilon(\omega) = 0$ 给出：
$$ \epsilon_\infty - \frac{\omega_p^2}{\omega^2} = 0 \implies \omega^2 = \frac{\omega_p^2}{\epsilon_\infty} $$
这个解，$\omega_L = \omega_p / \sqrt{\epsilon_\infty}$，就是**纵向体等离激元**的频率。它代表了整个电子气相对于正离子背景的一种刚性、相干的集体振荡。这种振荡是纵向的，意味着它不直接与横向光波耦合，因此不会自发辐射。然而，它可以通过纵向探针来激发，例如快速电子穿过金属。

当带电粒子（如电子）穿过材料时，其能量损失由**能量损失函数** $L(\omega)$ 描述，定义为：
$$ L(\omega) = \text{Im}\left[-\frac{1}{\epsilon(\omega)}\right] $$
这个函数在等离激元共振频率处出现峰值，标志着外部探针的能量被有效地转移给电子气的集体振荡。在有阻尼的情况下 ($\gamma > 0$)，等离激元共振不再是一个尖锐的delta函数，而是一个具有一定宽度的洛伦兹型峰。峰值频率 $\omega_{peak}$ 会因阻尼的存在而发生偏移。通过计算 $L(\omega)$ 对 $\omega$ 的导数并令其为零，可以找到这个峰值频率 [@problem_id:185635]。对于 $\epsilon(\omega) = 1 - \frac{\omega_p^2}{\omega(\omega+i\gamma)}$（即 $\epsilon_\infty=1$），能量损失函数为：
$$ L(\omega) = \frac{\gamma\omega\omega_p^2}{(\omega^2 - \omega_p^2)^2 + \gamma^2\omega^2} $$
其峰值频率 $\omega_{peak}$ 的精确表达式比 $\omega_p$ 更复杂，它依赖于 $\gamma$ 和 $\omega_p$ 的相对大小。只有在弱阻尼极限下 ($\gamma \ll \omega_p$)，峰值频率才约等于 $\omega_p$。

介电函数的[零点和极点](@entry_id:177073)结构深刻地揭示了介质中的元激发。对于离子晶体，Lyddane-Sachs-Teller (LST) 关系式 $\omega_L^2 / \omega_T^2 = \epsilon(0) / \epsilon(\infty)$ 将纵向光学声子频率 $\omega_L$（$\epsilon$ 的零点）和横向光学声子频率 $\omega_T$（$\epsilon$ 的极点）与静态和高频介电常数联系起来。我们可以为 Drude 金属构建一个类似的表述 [@problem_id:185677]。纵向等离激元频率 $\omega_L$ 依然是无损介电函数的零点，即 $\omega_L^2 = \omega_p^2/\epsilon_\infty$。高频介电常数为 $\epsilon(\infty) = \epsilon_\infty$。由于理想 Drude 模型在直流下发散，我们定义一个特征“静态”介电常数 $\epsilon_{st}$ 为有阻尼介电函数在 $\omega \to 0$ 时的实部极限，即 $\epsilon_{st} = \lim_{\omega\to 0} \text{Re}[\epsilon(\omega)] = \epsilon_\infty - \omega_p^2/\gamma^2$。将这些量组合起来，我们得到一个等离激元版本的 LST 关系：
$$ \frac{\epsilon_{st}}{\epsilon_\infty} = 1 - \frac{\omega_L^2}{\gamma^2} $$
这个关系式优雅地将材料的宏观介电响应（$\epsilon_{st}, \epsilon_\infty$）与其微观集体激发的特征（$\omega_L, \gamma$）联系起来。

### 空间色散：依赖于波矢的等离激元

简单的 Drude 模型预测等离激元频率 $\omega_p$ (或 $\omega_L$) 是一个常数，不随波矢 $q$ 变化。这意味着等离激元的群速度 $v_g = d\omega/dq$ 为零，它是一种纯粹的时间振荡，不能在空间中传播。这在物理上是不完全的，因为它忽略了电子气内部的相互作用和压力。

为了引入空间依赖性，即**空间色散**，我们可以采用更复杂的模型。
一个半经典的方法是**流体动力学模型** (hydrodynamic model)，它将电子气视为一种可压缩的带电液体。除了电场力，电子的运动还受到内部压力梯度 $\nabla P$ 的影响。对于简并的费米气体，压力的变化与密度的变化成正比，$\delta P = m\beta^2 \delta n$，其中 $\beta$ 是一个与电子气可压缩性相关的特征速度（对于费米气体，$\beta^2 \approx v_F^2/3$，其中 $v_F$ 是费米速度）。通过线性化流体力学方程（欧拉方程、连续性方程）和麦克斯韦方程组，可以推导出体等离激元的色散关系 [@problem_id:185611]：
$$ \omega^2(q) = \omega_p^2 + \beta^2 q^2 $$
这个结果表明，对于有限的波矢 $q$，等离激元频率会增加。这种正向的色散关系意味着等离激元现在可以作为一种具有非零群速度的波在材料中传播。物理上，压力项提供了一种恢复力，当电子气被压缩时（对应于较短的波长或较大的 $q$），这种额外的恢复力使得振荡频率更高。

一个更严格的量子力学方法是**随机相近似** (Random Phase Approximation, RPA)。RPA 计算了无相互作用电子气对外部扰动势的线性响应函数 $\chi_0(q, \omega)$，并通过考虑电子之间的库仑相互作用来构建总的介电函数 $\epsilon(q, \omega) = 1 - v_q \chi_0(q, \omega)$，其中 $v_q = e^2/(\epsilon_0 q^2)$ 是库仑相互作用的傅里叶变换。在长波长 ($q \ll k_F$) 和高频 ($\hbar\omega \gg \epsilon_F$) 极限下，可以对 $\chi_0(q, \omega)$ 进行展开。利用等离激元条件 $\epsilon(q, \omega) = 0$，可以推导出等离激元的色散关系 [@problem_id:185734]。对于小的 $q$，该色散关系可以近似为：
$$ \omega(q) \approx \omega_p + \alpha q^2 $$
其中色散系数 $\alpha$ 被证明为：
$$ \alpha = \frac{3}{10} \frac{v_F^2}{\omega_p} $$
这与流体动力学模型预测的 $\omega(q) \approx \omega_p(1 + \frac{\beta^2}{2\omega_p^2}q^2)$ 在形式上是一致的，并给出了色散系数与费米速度 $v_F$ 这一基本量子参数的直接联系。这两种模型都证实了体等离激元具有正的二次色散关系，这是**非局域效应** (non-local effects) 的一个直接后果——材料在某一点的响应不仅取决于该点的电场，还取决于其邻近区域的场分布。

### 限制几何 I：表面等离激元极化子 (SPP)

当金属与电介质形成一个平坦界面时，一种新型的电磁模式可以在该界面上存在和传播，这就是**表面等离激元极化子** (Surface Plasmon Polariton, SPP)。SPP 是一种混合模式，它由沿界面传播的电磁波与金属表面电子的集体振荡（即表面等离激元）耦合而成。

SPP 具有以下关键特征：
1.  它是一种**横磁 (TM)** 波，意味着其磁场矢量垂直于传播方向和界面法线方向。
2.  它的场强在远离界面时向两边介质中呈**指数衰减**，因此是一种被束缚在界面上的表面波。
3.  它的存在要求两种介质的介电函数实部符号相反，即 $\epsilon_m' \cdot \epsilon_d  0$。对于金属（$\epsilon_m'  0$）和电介质（$\epsilon_d  0$）的界面，这个条件在金属的 $\epsilon_m'  -\epsilon_d$ 的频率范围内得到满足。

通过在界面两侧求解麦克斯韦方程组，并应用电磁场的边界连续性条件（切向 $\mathbf{E}$ 和 $\mathbf{H}$ 场，以及法向 $\mathbf{D}$ 场连续），我们可以推导出 SPP 的色散关系。对于一个隔开介电常数为 $\epsilon_d$ 的电介质和介电函数为 $\epsilon_m(\omega)$ 的金属的界面，其色散关系为 [@problem_id:185637]：
$$ k_{sp}^2 = \left(\frac{\omega}{c}\right)^2 \frac{\epsilon_d \epsilon_m(\omega)}{\epsilon_d + \epsilon_m(\omega)} $$
其中 $k_{sp}$ 是 SPP 沿界面的波矢，$\omega$ 是其频率，$c$ 是真空中的光速。将无损 Drude 模型 $\epsilon_m(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega^2}$ 代入，我们得到：
$$ k_{sp}^2 = \left(\frac{\omega}{c}\right)^2 \frac{\epsilon_d \left( \epsilon_\infty - \frac{\omega_p^2}{\omega^2} \right)}{\epsilon_d + \epsilon_\infty - \frac{\omega_p^2}{\omega^2}} $$
SPP 的色散曲线位于真空中光线 $\omega = ck$ 和电介质中光线 $\omega = ck/\sqrt{\epsilon_d}$ 的右侧，表明 SPP 的波矢总大于同频率下在电介质中传播的光子的波矢。这意味着自由空间中的光不能直接激发 SPP，因为存在动量失配。需要特殊的技术，如棱镜耦合（Kretschmann 或 Otto 构造）或光栅耦合来提供额外的动量。

在波矢 $k_{sp}$ 很大时（对应于非推迟极限 $c \to \infty$），分母趋于零，即 $\epsilon_d + \epsilon_m(\omega) \to 0$。这给出了一个渐近频率，称为**表面等离激元频率** $\omega_{sp}$：
$$ \omega_{sp} = \frac{\omega_p}{\sqrt{\epsilon_d + \epsilon_\infty}} $$
就像非局域效应导致体等离激元具有色散一样，它也会影响表面等离激元。在流体动力学模型中，即使在非推迟极限下，表面等离激元的频率也不再是一个常数，而是随波矢 $k_x$ 线性增加 [@problem_id:185697]：
$$ \omega(k_x) \approx \omega_{sp} + C k_x $$
其中 $C$ 是一个正的系数（例如，对于金属-真空界面，$\omega_{sp}=\omega_p/\sqrt{2}$，$C = \beta/4$）。这再次说明了电子压力如何影响等离激元的动力学，为表面模式赋予了正的色散。

### 限制几何 II：局域表面等离激元共振 (LSPR)

当金属结构的尺寸在所有三个维度上都远小于光的波长时，传导电子的集体振荡会被限制在纳米颗粒的边界内，形成不传播的**局域表面等离激元共振** (Localized Surface Plasmon Resonance, LSPR)。

在这种**准静态近似** (quasistatic approximation) 下，入射电磁波的电场可以被视为一个随时间变化的均匀静电场 $\mathbf{E}_{ext}$。这个场会极化纳米颗粒，在其表面感应出电荷，从而产生一个与外场方向相反的**退极化场** $\mathbf{E}_{depol}$。颗粒内部的总场为 $\mathbf{E}_{in} = \mathbf{E}_{ext} + \mathbf{E}_{depol}$。

当内部总场被极大增强时，即发生共振。这发生在退极化场几乎完全抵消了内部极化场与外场的总和时。对于一个浸润在介电常数为 $\epsilon_d$ 的介质中、由介电函数为 $\epsilon_m(\omega)$ 的金属构成的纳米颗粒，共振条件通常可以表示为分母的最小化。

以一个无限长的金属纳米圆柱为例，其半径 $a$ 远小于波长，当外加电场垂直于圆柱轴线时，可以求解拉普拉斯方程并应用边界条件，得到圆柱内部的电场为 [@problem_id:185736]：
$$ \mathbf{E}_{in} = \frac{2\epsilon_d}{\epsilon_m(\omega) + \epsilon_d} \mathbf{E}_{ext} $$
场增强因子 $|\mathbf{E}_{in}/\mathbf{E}_{ext}|$ 在分母 $|\epsilon_m(\omega) + \epsilon_d|$ 最小时达到最大。忽略金属的损耗（即 $\epsilon_m''$ 很小），共振条件简化为分母的实部为零：
$$ \text{Re}[\epsilon_m(\omega_{sp})] + \epsilon_d = 0 \quad \text{或} \quad \epsilon_m'(\omega_{sp}) = -\epsilon_d $$
这个简单的条件揭示了 LSPR 频率强烈地依赖于金属的介电性质和周围环境的介电常数。

对于更复杂的形状，如椭球体，退极化场变得各向异性。其响应取决于电场相对于粒子主轴的方向。对于一个主轴与坐标轴对齐的椭球体，其内部电场为：
$$ E_{in, i} = \frac{1}{1 + N_i (\epsilon_m(\omega)/\epsilon_d - 1)} E_{ext, i} $$
其中 $i \in \{x, y, z\}$，$N_i$ 是沿 $i$ 轴的**几何退极化因子**，它只依赖于颗粒的形状。共振条件变为 $1 + N_i (\epsilon_m(\omega)/\epsilon_d - 1) = 0$，或等价地 $\epsilon_m(\omega) = \epsilon_d(1 - 1/N_i)$。由于不同轴的 $N_i$ 值不同，LSPR 频率会随颗粒的形状和入射光的偏振方向而变化。

例如，对于一个长短轴之比为 $R=a/b  1$ 的长椭球，沿长轴的退极化因子 $N_a$ 小于沿短轴的 $N_b$。这导致了两个不同的共振频率：对应电场平行于长轴的**纵向模式** $\omega_L$ 和对应电场平行于短轴的**横向模式** $\omega_T$。可以证明 $\omega_L  \omega_T$。通过控制颗粒的宽高比 $R$，可以系统地调节 LSPR 的频率，这使得 LSPR 在传感、光谱学和光子学等领域具有极大的应用价值 [@problem_id:185641]。

### 混合等离激元系统与强耦合

等离激元作为一种基本的元激发，可以与其他类型的元激发（如声子、激子）发生相互作用，形成新的**混合量子态**。当相互作用强度超过系统中各个组分的衰减速率时，系统便进入了**强耦合**区域，其特征是能级的分裂和反交叉行为。

一个经典的例子是**等离激元-声子极化子**。在掺杂的极性半导体（如 GaAs）中，自由载流子的等离激元可以与晶格的纵向光学 (LO) 声子耦合。材料的总介电函数包含来自声子和等离激元的贡献。耦合后的纵向模式频率由总介电函数 $\epsilon_{total}(\omega) = 0$ 决定 [@problem_id:185608]。求解该方程会得到两个新的模式分支，$\omega_+$ 和 $\omega_-$。当未耦合的等离激元频率 $\omega_p$ 和 LO 声子频率 $\omega_{LO}$ 接近时，两条色散曲线发生反交叉，形成能量上的劈裂，这是模式杂化的明确标志。

近年来，将等离激元与量子发射体（如量子点或分子）耦合的系统引起了极大关注。当一个金属纳米颗粒的 LSPR 模式与附近量子点的激子（电子-空穴对）发生强耦合时，会形成称为**丛集激子** (plexciton) 的混合光-物质态。该系统可以用一个有效哈密顿量来描述，其对角元是未耦合的等离激元和激子的复数能量（包含能量和线宽），非对角元是它们的耦合强度 $g$。

考虑一个等离激元模式与两个相同的、不相互作用的量子点耦合的系统。当系统处于共振状态（$\omega_{sp} = \omega_{ex} = \omega_0$），并且耦合强度足够大时（满足强耦合条件），原始的三个能级会重新组合。其中一个组合态是与等离激元解耦的“暗态”，而另外两个则形成“亮态”，其能量发生劈裂。这个能量劈裂 $\Delta E$ 是 Rabi 劈裂的类似物，其大小为 [@problem_id:185660]：
$$ \Delta E = \sqrt{8g^2 - \frac{(\Gamma_{sp} - \Gamma_{ex})^2}{4}} $$
其中 $\Gamma_{sp}$ 和 $\Gamma_{ex}$ 分别是等离激元和激子的线宽。这种能量劈裂的现象是强耦合的直接证据，它为在纳米尺度上操控光与物质相互作用开辟了新的途径，是量子等离激元学领域的核心研究内容。