## 引言
[等离激元](@entry_id:146184)（Plasmon）是金属或[半导体](@entry_id:141536)中[自由电子气](@entry_id:145649)的[集体振荡](@entry_id:158973)，是光与物质在纳米尺度上相互作用的核心媒介。通过激发和调控[等离激元](@entry_id:146184)，科学家们能够将光能束缚在远小于[衍射极限](@entry_id:193662)的空间内，产生巨大的局域场增强和新颖的光学效应。理解这些集体激发如何产生、如何被操控，以及它们独特的物理性质如何转化为颠覆性技术，是现代凝聚态物理与[纳米光子学](@entry_id:137892)的核心课题。

本文旨在系统性地构建[等离激元](@entry_id:146184)物理的知识框架，带领读者从基本原理走向前沿应用。在“**原理与机制**”一章中，我们将从经典的Drude模型出发，逐步建立[体等离激元](@entry_id:143484)、表面等离激元（SPP）和[局域表面等离激元](@entry_id:270427)（LSPR）的物理图像，并探讨[空间色散](@entry_id:141344)、混合模式等高级概念。接着，在“**应用与交叉学科联系**”一章中，我们将展示这些基本原理如何在[纳米光子学](@entry_id:137892)、[生物传感](@entry_id:274809)、[材料科学](@entry_id:152226)乃至[量子信息](@entry_id:137721)等前沿领域中催生出多样化的应用。最后，“**动手实践**”部分将通过一系列计算问题，巩固和深化读者对核心概念的理解。通过这一结构化的学习路径，读者将能够全面掌握[等离激元学](@entry_id:142222)的理论基础和应用前景。

## 原理与机制

### [自由电子气](@entry_id:145649)的介电函数：Drude 模型

理解等离激元物理的出发点是建立一个描述金属中传导电子对[电磁场](@entry_id:265881)响应的模型。最基础且富有洞察力的模型是 **Drude 模型**，它将金属中的传导电子（或称电子气）视为一种经典粒子气体，这些粒子在固定的正离子[晶格](@entry_id:196752)背景中自由运动，并会与[晶格缺陷](@entry_id:270099)、[声子](@entry_id:140728)或其他电子发生碰撞。

在交变[电场](@entry_id:194326) $\mathbf{E}(t) = \mathbf{E}_0 e^{-i\omega t}$ 的驱动下，一个电子的经典运动方程可以写作：
$$ m \frac{d\mathbf{v}}{dt} = -e\mathbf{E} - m\gamma \mathbf{v} $$
其中 $m$ 是电子[有效质量](@entry_id:142879)，$-e$ 是电子[电荷](@entry_id:275494)，$\mathbf{v}$ 是电子相对于[晶格](@entry_id:196752)的平均[漂移速度](@entry_id:262489)，$\gamma$ 是一个唯象的**阻尼率**或**[碰撞频率](@entry_id:138992)**，它描述了电子动量因碰撞而弛豫的速率。在[稳态](@entry_id:182458)下，速度的解为 $\mathbf{v}(t) = \mathbf{v}_0 e^{-i\omega t}$，代入上式可得：
$$ \mathbf{v} = \frac{-e\mathbf{E}}{m(-i\omega + \gamma)} = \frac{ie\mathbf{E}}{m(\omega + i\gamma)} $$
由此产生的电流密度 $\mathbf{J} = -ne\mathbf{v}$（其中 $n$ 是电子数密度）与[电场](@entry_id:194326)通过电导率 $\sigma(\omega)$ 联系起来，$\mathbf{J} = \sigma(\omega)\mathbf{E}$，因此频率依赖的电导率为：
$$ \sigma(\omega) = \frac{ne^2}{m(\gamma - i\omega)} = \frac{ne^2\tau}{m(1 - i\omega\tau)} $$
其中 $\tau = 1/\gamma$ 是平均[碰撞时间](@entry_id:261390)。

在[电动力学](@entry_id:158759)中，材料的光学响应通常由其[介电函数](@entry_id:136859) $\epsilon(\omega)$ 描述，它通过关系式 $\epsilon(\omega) = \epsilon_b + \frac{i\sigma(\omega)}{\omega\epsilon_0}$ 与[电导率](@entry_id:137481)相关联。这里的 $\epsilon_0$ 是[真空介电常数](@entry_id:204253)，$\epsilon_b$ 是由束缚的芯层电子贡献的背景[介电常数](@entry_id:146714)，通常在感兴趣的频率范围内近似为常数，记作 $\epsilon_\infty$。将 Drude [电导率](@entry_id:137481)代入，我们得到 Drude 介电函数：
$$ \epsilon(\omega) = \epsilon_\infty - \frac{ne^2}{m\epsilon_0} \frac{1}{\omega(\omega + i\gamma)} $$
我们定义**[体等离激元](@entry_id:143484)频率** (bulk plasma frequency) $\omega_p$ 为：
$$ \omega_p^2 = \frac{ne^2}{m\epsilon_0} $$
$\omega_p$ 是电子气[集体振荡](@entry_id:158973)的自然频率，是一个仅由电子密度和[有效质量](@entry_id:142879)决定的内禀材料参数。于是，Drude [介电函数](@entry_id:136859)可以紧凑地写作：
$$ \epsilon(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega(\omega + i\gamma)} $$
该复数函数可以分解为实部 $\epsilon'$ 和虚部 $\epsilon''$：
$$ \epsilon'(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega^2 + \gamma^2} $$
$$ \epsilon''(\omega) = \frac{\gamma\omega_p^2}{\omega(\omega^2 + \gamma^2)} $$
$\epsilon'(\omega)$ 描述了[材料的极化](@entry_id:271610)响应，而 $\epsilon''(\omega)$ 描述了能量的吸收或耗散。在低频极限下 ($\omega \to 0$)，$\epsilon'(\omega)$ 趋于一个大的负值，而 $\epsilon''(\omega)$ 发散，这反映了金属的直流[电导](@entry_id:177131)特性。在高频极限下 ($\omega \to \infty$)，$\epsilon'(\omega) \to \epsilon_\infty$，$\epsilon''(\omega) \to 0$，金属变得像透明的[电介质](@entry_id:147163)。

### 集体激发：[体等离激元](@entry_id:143484)

[电磁波](@entry_id:269629)在介质中的传播模式由麦克斯韦方程组决定。对于纵向波（[电场](@entry_id:194326)平行于[波矢](@entry_id:178620) $\mathbf{q}$），亥姆霍兹方程要求 $\epsilon(\mathbf{q}, \omega) \mathbf{E} = 0$。要存在非平庸解 ($\mathbf{E} \neq 0$)，必须满足条件 $\epsilon(\mathbf{q}, \omega) = 0$。在 Drude 模型的长波极限下（$q \to 0$，介电函数不依赖于 $q$），纵向集体激发的条件简化为 $\epsilon(\omega) = 0$。

让我们首先考虑一个理想的无碰撞[电子气](@entry_id:140692)，即阻尼 $\gamma = 0$。此时[介电函数](@entry_id:136859)为实数：
$$ \epsilon(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega^2} $$
设置 $\epsilon(\omega) = 0$ 给出：
$$ \epsilon_\infty - \frac{\omega_p^2}{\omega^2} = 0 \implies \omega^2 = \frac{\omega_p^2}{\epsilon_\infty} $$
这个解，$\omega_L = \omega_p / \sqrt{\epsilon_\infty}$，就是**纵向[体等离激元](@entry_id:143484)**的频率。它代表了整个[电子气](@entry_id:140692)相对于正离子背景的一种刚性、相干的集体振荡。这种[振荡](@entry_id:267781)是纵向的，意味着它不直接与横向光[波耦合](@entry_id:198588)，因此不会自发辐射。然而，它可以通过纵向探针来激发，例如快速电子穿过金属。

当[带电粒子](@entry_id:160311)（如电子）穿过材料时，其能量损失由**[能量损失](@entry_id:159152)函数** $L(\omega)$ 描述，定义为：
$$ L(\omega) = \text{Im}\left[-\frac{1}{\epsilon(\omega)}\right] $$
这个函数在[等离激元共振](@entry_id:197204)频率处出现峰值，标志着外部探针的能量被有效地转移给[电子气](@entry_id:140692)的[集体振荡](@entry_id:158973)。在有阻尼的情况下 ($\gamma > 0$)，[等离激元共振](@entry_id:197204)不再是一个尖锐的delta函数，而是一个具有一定宽度的洛伦兹型峰。峰值频率 $\omega_{peak}$ 会因阻尼的存在而发生偏移。通过计算 $L(\omega)$ 对 $\omega$ 的导数并令其为零，可以找到这个峰值频率 [@problem_id:185635]。对于 $\epsilon(\omega) = 1 - \frac{\omega_p^2}{\omega(\omega+i\gamma)}$（即 $\epsilon_\infty=1$），[能量损失](@entry_id:159152)函数为：
$$ L(\omega) = \frac{\gamma\omega\omega_p^2}{(\omega^2 - \omega_p^2)^2 + \gamma^2\omega^2} $$
其峰值频率 $\omega_{peak}$ 的精确表达式比 $\omega_p$ 更复杂，它依赖于 $\gamma$ 和 $\omega_p$ 的相对大小。只有在弱阻尼极限下 ($\gamma \ll \omega_p$)，峰值频率才约等于 $\omega_p$。

介电[函数的[零](@entry_id:180934)点和极点](@entry_id:177073)结构深刻地揭示了介质中的[元激发](@entry_id:140859)。对于离子晶体，Lyddane-Sachs-Teller (LST) 关系式 $\omega_L^2 / \omega_T^2 = \epsilon(0) / \epsilon(\infty)$ 将[纵向光学声子](@entry_id:140641)频率 $\omega_L$（$\epsilon$ 的零点）和[横向光学声子](@entry_id:139212)频率 $\omega_T$（$\epsilon$ 的极点）与静态和高频[介电常数](@entry_id:146714)联系起来。我们可以为 Drude 金属构建一个类似的表述 [@problem_id:185677]。纵向等离激元频率 $\omega_L$ 依然是无损介电[函数的零点](@entry_id:180934)，即 $\omega_L^2 = \omega_p^2/\epsilon_\infty$。高频[介电常数](@entry_id:146714)为 $\epsilon(\infty) = \epsilon_\infty$。由于理想 Drude 模型在直流下发散，我们定义一个特征“静态”[介电常数](@entry_id:146714) $\epsilon_{st}$ 为有阻尼[介电函数](@entry_id:136859)在 $\omega \to 0$ 时的实部极限，即 $\epsilon_{st} = \lim_{\omega\to 0} \text{Re}[\epsilon(\omega)] = \epsilon_\infty - \omega_p^2/\gamma^2$。将这些量组合起来，我们得到一个等离激元版本的 LST 关系：
$$ \frac{\epsilon_{st}}{\epsilon_\infty} = 1 - \frac{\omega_L^2}{\gamma^2} $$
这个关系式优雅地将材料的宏观[介电响应](@entry_id:140146)（$\epsilon_{st}, \epsilon_\infty$）与其微观集体激发的特征（$\omega_L, \gamma$）联系起来。

### [空间色散](@entry_id:141344)：依赖于[波矢](@entry_id:178620)的[等离激元](@entry_id:146184)

简单的 Drude 模型预测等离激元频率 $\omega_p$ (或 $\omega_L$) 是一个常数，不随波矢 $q$ 变化。这意味着等离激元的[群速度](@entry_id:147686) $v_g = d\omega/dq$ 为零，它是一种纯粹的时间[振荡](@entry_id:267781)，不能在空间中传播。这在物理上是不完全的，因为它忽略了[电子气](@entry_id:140692)内部的相互作用和压力。

为了引入空间依赖性，即**[空间色散](@entry_id:141344)**，我们可以采用更复杂的模型。
一个半经典的方法是**[流体动力学](@entry_id:136788)模型** (hydrodynamic model)，它将[电子气](@entry_id:140692)视为一种可压缩的带电液体。除了[电场](@entry_id:194326)力，电子的运动还受到内部压力梯度 $\nabla P$ 的影响。对于简并的费米气体，压力的变化与密度的变化成正比，$\delta P = m\beta^2 \delta n$，其中 $\beta$ 是一个与电子气[可压缩性](@entry_id:144559)相关的[特征速度](@entry_id:165394)（对于[费米气体](@entry_id:145305)，$\beta^2 \approx v_F^2/3$，其中 $v_F$ 是费米速度）。通过线性化[流体力学](@entry_id:136788)方程（[欧拉方程](@entry_id:177914)、[连续性方程](@entry_id:195013)）和麦克斯韦方程组，可以推导出[体等离激元](@entry_id:143484)的色散关系 [@problem_id:185611]：
$$ \omega^2(q) = \omega_p^2 + \beta^2 q^2 $$
这个结果表明，对于有限的[波矢](@entry_id:178620) $q$，等离激元频率会增加。这种正向的色散关系意味着等离激元现在可以作为一种具有非零[群速度](@entry_id:147686)的波在材料中传播。物理上，压力项提供了一种恢复力，当电子气被压缩时（对应于较短的波长或较大的 $q$），这种额外的恢复力使得振荡频率更高。

一个更严格的量子力学方法是**随机相近似** (Random Phase Approximation, RPA)。RPA 计算了无相互作用电子气对外部扰动势的[线性响应函数](@entry_id:160418) $\chi_0(q, \omega)$，并通过考虑电子之间的[库仑相互作用](@entry_id:747947)来构建总的介电函数 $\epsilon(q, \omega) = 1 - v_q \chi_0(q, \omega)$，其中 $v_q = e^2/(\epsilon_0 q^2)$ 是[库仑相互作用](@entry_id:747947)的[傅里叶变换](@entry_id:142120)。在长波长 ($q \ll k_F$) 和高频 ($\hbar\omega \gg \epsilon_F$) 极限下，可以对 $\chi_0(q, \omega)$ 进行展开。利用[等离激元](@entry_id:146184)条件 $\epsilon(q, \omega) = 0$，可以推导出等离激元的[色散关系](@entry_id:140395) [@problem_id:185734]。对于小的 $q$，该色散关系可以近似为：
$$ \omega(q) \approx \omega_p + \alpha q^2 $$
其中[色散](@entry_id:263750)系数 $\alpha$ 被证明为：
$$ \alpha = \frac{3}{10} \frac{v_F^2}{\omega_p} $$
这与[流体动力学](@entry_id:136788)模型预测的 $\omega(q) \approx \omega_p(1 + \frac{\beta^2}{2\omega_p^2}q^2)$ 在形式上是一致的，并给出了[色散](@entry_id:263750)系数与费米速度 $v_F$ 这一基本量子参数的直接联系。这两种模型都证实了[体等离激元](@entry_id:143484)具有正的二次色散关系，这是**非局域效应** (non-local effects) 的一个直接后果——材料在某一点的响应不仅取决于该点的[电场](@entry_id:194326)，还取决于其邻近区域的场[分布](@entry_id:182848)。

### 限制几何 I：表面等离激元[极化子](@entry_id:191083) (SPP)

当金属与[电介质](@entry_id:147163)形成一个平坦界面时，一种新型的[电磁模式](@entry_id:260856)可以在该界面上存在和传播，这就是**[表面等离激元](@entry_id:145851)[极化子](@entry_id:191083)** (Surface Plasmon Polariton, SPP)。SPP 是一种混合模式，它由沿界面传播的[电磁波](@entry_id:269629)与金属表面电子的[集体振荡](@entry_id:158973)（即表面等离激元）耦合而成。

SPP 具有以下关键特征：
1.  它是一种**横磁 (TM)** 波，意味着其[磁场](@entry_id:153296)矢量垂直于传播方向和界面[法线](@entry_id:167651)方向。
2.  它的场强在远离界面时向两边介质中呈**指数衰减**，因此是一种被束缚在界面上的[表面波](@entry_id:755682)。
3.  它的存在要求两种介质的介电函数实部符号相反，即 $\epsilon_m' \cdot \epsilon_d  0$。对于金属（$\epsilon_m'  0$）和[电介质](@entry_id:147163)（$\epsilon_d  0$）的界面，这个条件在金属的 $\epsilon_m'  -\epsilon_d$ 的频率范围内得到满足。

通过在界面两侧求解[麦克斯韦方程组](@entry_id:150940)，并应用[电磁场](@entry_id:265881)的边界连续性条件（切向 $\mathbf{E}$ 和 $\mathbf{H}$ 场，以及法向 $\mathbf{D}$ 场连续），我们可以推导出 SPP 的[色散关系](@entry_id:140395)。对于一个隔开[介电常数](@entry_id:146714)为 $\epsilon_d$ 的[电介质](@entry_id:147163)和[介电函数](@entry_id:136859)为 $\epsilon_m(\omega)$ 的金属的界面，其色散关系为 [@problem_id:185637]：
$$ k_{sp}^2 = \left(\frac{\omega}{c}\right)^2 \frac{\epsilon_d \epsilon_m(\omega)}{\epsilon_d + \epsilon_m(\omega)} $$
其中 $k_{sp}$ 是 SPP 沿界面的波矢，$\omega$ 是其频率，$c$ 是[真空中的光速](@entry_id:272753)。将无损 Drude 模型 $\epsilon_m(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega^2}$ 代入，我们得到：
$$ k_{sp}^2 = \left(\frac{\omega}{c}\right)^2 \frac{\epsilon_d \left( \epsilon_\infty - \frac{\omega_p^2}{\omega^2} \right)}{\epsilon_d + \epsilon_\infty - \frac{\omega_p^2}{\omega^2}} $$
SPP 的色散曲线位于真空中光线 $\omega = ck$ 和[电介质](@entry_id:147163)中光线 $\omega = ck/\sqrt{\epsilon_d}$ 的右侧，表明 SPP 的波矢总大于同频率下在[电介质](@entry_id:147163)中传播的[光子](@entry_id:145192)的波矢。这意味着自由空间中的光不能直接激发 SPP，因为存在动量失配。需要特殊的技术，如棱镜耦合（Kretschmann 或 Otto 构造）或光栅耦合来提供额外的动量。

在波矢 $k_{sp}$ 很大时（对应于非推迟极限 $c \to \infty$），分母趋于零，即 $\epsilon_d + \epsilon_m(\omega) \to 0$。这给出了一个渐近频率，称为**表面等离激元频率** $\omega_{sp}$：
$$ \omega_{sp} = \frac{\omega_p}{\sqrt{\epsilon_d + \epsilon_\infty}} $$
就像非局域效应导致[体等离激元](@entry_id:143484)具有[色散](@entry_id:263750)一样，它也会影响表面等离激元。在[流体动力学](@entry_id:136788)模型中，即使在非推迟极限下，表面等离激元的频率也不再是一个常数，而是随[波矢](@entry_id:178620) $k_x$ 线性增加 [@problem_id:185697]：
$$ \omega(k_x) \approx \omega_{sp} + C k_x $$
其中 $C$ 是一个正的系数（例如，对于金属-真空界面，$\omega_{sp}=\omega_p/\sqrt{2}$，$C = \beta/4$）。这再次说明了电子压力如何影响[等离激元](@entry_id:146184)的动力学，为表面模式赋予了正的[色散](@entry_id:263750)。

### 限制几何 II：[局域表面等离激元共振 (LSPR)](@entry_id:200559)

当金属结构的尺寸在所有三个维度上都远小于光的波长时，[传导电子](@entry_id:145260)的[集体振荡](@entry_id:158973)会被限制在纳米颗粒的边界内，形成不传播的**[局域表面等离激元共振](@entry_id:157595)** (Localized Surface Plasmon Resonance, LSPR)。

在这种**[准静态近似](@entry_id:264812)** (quasistatic approximation) 下，入射[电磁波](@entry_id:269629)的[电场](@entry_id:194326)可以被视为一个随时间变化的均匀[静电场](@entry_id:268546) $\mathbf{E}_{ext}$。这个场会极化纳米颗粒，在其表面感应出[电荷](@entry_id:275494)，从而产生一个与外场方向相反的**退[极化场](@entry_id:197617)** $\mathbf{E}_{depol}$。颗粒内部的总场为 $\mathbf{E}_{in} = \mathbf{E}_{ext} + \mathbf{E}_{depol}$。

当内部总场被极大增强时，即发生共振。这发生在退[极化场](@entry_id:197617)几乎完全抵消了内部[极化场](@entry_id:197617)与外场的总和时。对于一个浸润在[介电常数](@entry_id:146714)为 $\epsilon_d$ 的介质中、由[介电函数](@entry_id:136859)为 $\epsilon_m(\omega)$ 的金属构成的纳米颗粒，共振条件通常可以表示为分母的最小化。

以一个无限长的金属纳米圆柱为例，其半径 $a$ 远小于波长，当外加[电场](@entry_id:194326)垂直于圆柱轴线时，可以[求解拉普拉斯方程](@entry_id:188506)并应用边界条件，得到圆柱内部的[电场](@entry_id:194326)为 [@problem_id:185736]：
$$ \mathbf{E}_{in} = \frac{2\epsilon_d}{\epsilon_m(\omega) + \epsilon_d} \mathbf{E}_{ext} $$
场增强因子 $|\mathbf{E}_{in}/\mathbf{E}_{ext}|$ 在分母 $|\epsilon_m(\omega) + \epsilon_d|$ 最小时达到最大。忽略金属的损耗（即 $\epsilon_m''$ 很小），共振条件简化为分母的实部为零：
$$ \text{Re}[\epsilon_m(\omega_{sp})] + \epsilon_d = 0 \quad \text{或} \quad \epsilon_m'(\omega_{sp}) = -\epsilon_d $$
这个简单的条件揭示了 LSPR 频率强烈地依赖于金属的介电性质和周围环境的[介电常数](@entry_id:146714)。

对于更复杂的形状，如[椭球体](@entry_id:165811)，退[极化场](@entry_id:197617)变得各向异性。其响应取决于[电场](@entry_id:194326)相对于粒子主轴的方向。对于一个主轴与坐标轴对齐的椭球体，其内部[电场](@entry_id:194326)为：
$$ E_{in, i} = \frac{1}{1 + N_i (\epsilon_m(\omega)/\epsilon_d - 1)} E_{ext, i} $$
其中 $i \in \{x, y, z\}$，$N_i$ 是沿 $i$ 轴的**几何退极化因子**，它只依赖于颗粒的形状。共振条件变为 $1 + N_i (\epsilon_m(\omega)/\epsilon_d - 1) = 0$，或等价地 $\epsilon_m(\omega) = \epsilon_d(1 - 1/N_i)$。由于不同轴的 $N_i$ 值不同，LSPR 频率会随颗粒的形状和入射[光的偏振](@entry_id:262080)方向而变化。

例如，对于一个长短轴之比为 $R=a/b  1$ 的[长椭球](@entry_id:176438)，沿长轴的退极化因子 $N_a$ 小于沿短轴的 $N_b$。这导致了两个不同的[共振频率](@entry_id:265742)：对应[电场](@entry_id:194326)平行于长轴的**纵向模式** $\omega_L$ 和对应[电场](@entry_id:194326)平行于短轴的**[横向模式](@entry_id:163265)** $\omega_T$。可以证明 $\omega_L  \omega_T$。通过控制颗粒的宽高比 $R$，可以系统地调节 LSPR 的频率，这使得 LSPR 在传感、[光谱学](@entry_id:141940)和[光子](@entry_id:145192)学等领域具有极大的应用价值 [@problem_id:185641]。

### 混合等离激元系统与强耦合

等离激元作为一种基本的[元激发](@entry_id:140859)，可以与其他类型的[元激发](@entry_id:140859)（如[声子](@entry_id:140728)、激子）发生相互作用，形成新的**[混合量子态](@entry_id:262127)**。当相互作用强度超过系统中各个组分的衰减速率时，系统便进入了**强耦合**区域，其特征是能级的分裂和反交叉行为。

一个经典的例子是**[等离激元](@entry_id:146184)-[声子](@entry_id:140728)极化子**。在掺杂的极性[半导体](@entry_id:141536)（如 GaAs）中，自由载流子的[等离激元](@entry_id:146184)可以与[晶格](@entry_id:196752)的纵向光学 (LO) [声子](@entry_id:140728)耦合。材料的总介电函数包含来自[声子](@entry_id:140728)和等离激元的贡献。耦合后的纵向模式频率由总[介电函数](@entry_id:136859) $\epsilon_{total}(\omega) = 0$ 决定 [@problem_id:185608]。求解该方程会得到两个新的模式分支，$\omega_+$ 和 $\omega_-$。当未耦合的等离激元频率 $\omega_p$ 和 LO [声子频率](@entry_id:753407) $\omega_{LO}$ 接近时，两条色散曲线发生反交叉，形成能量上的劈裂，这是模式杂化的明确标志。

近年来，将[等离激元](@entry_id:146184)与量子发射体（如[量子点](@entry_id:143385)或分子）耦合的系统引起了极大关注。当一个金属纳米颗粒的 LSPR 模式与附近[量子点](@entry_id:143385)的[激子](@entry_id:147299)（电子-空穴对）发生强耦合时，会形成称为**丛集激子** (plexciton) 的混合光-物质态。该系统可以用一个[有效哈密顿量](@entry_id:748813)来描述，其对角元是未耦合的等离激元和激子的复数能量（包含能量和[线宽](@entry_id:199028)），非对角元是它们的耦合强度 $g$。

考虑一个[等离激元](@entry_id:146184)模式与两个相同的、不相互作用的[量子点](@entry_id:143385)耦合的系统。当系统处于共振状态（$\omega_{sp} = \omega_{ex} = \omega_0$），并且[耦合强度](@entry_id:275517)足够大时（满足强耦合条件），原始的三个能级会重新组合。其中一个组合态是与[等离激元](@entry_id:146184)解耦的“暗态”，而另外两个则形成“[亮态](@entry_id:189717)”，其能量发生劈裂。这个能量劈裂 $\Delta E$ 是 Rabi 劈裂的类似物，其大小为 [@problem_id:185660]：
$$ \Delta E = \sqrt{8g^2 - \frac{(\Gamma_{sp} - \Gamma_{ex})^2}{4}} $$
其中 $\Gamma_{sp}$ 和 $\Gamma_{ex}$ 分别是等离激元和激子的线宽。这种能量劈裂的现象是强耦合的直接证据，它为在纳米尺度上操控光与物质相互作用开辟了新的途径，是[量子等离激元学](@entry_id:184780)领域的核心研究内容。