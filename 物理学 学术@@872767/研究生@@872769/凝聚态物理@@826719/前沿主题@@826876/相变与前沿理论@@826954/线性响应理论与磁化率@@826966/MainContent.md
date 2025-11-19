## 引言
[线性响应理论](@entry_id:145737)是现代凝聚态物理的基石之一，它提供了一个强大的理论框架，用于理解物质如何对外部施加的微弱刺激（如[电场](@entry_id:194326)、[磁场](@entry_id:153296)或应力）做出反应。其核心思想在于，当微扰足够小时，系统的响应与微扰的强度成线性关系。这一看似简单的假设，却能建立起连接微观量子力学定律与宏观可观测物理量（如电导率、磁化率和[介电常数](@entry_id:146714)）的桥梁，解决了如何从第一性原理出发系统地计算和预测材料性质这一根本问题。

本文旨在全面而深入地探讨[线性响应理论](@entry_id:145737)及其在多体物理中的广泛应用。我们将从第一章“原理与机制”开始，推导核心的[久保公式](@entry_id:144041)，阐明因果性、克拉默-克罗尼格关系以及涨落-耗散定理等普适原理。接着，在第二章“应用与[交叉](@entry_id:147634)学科联系”中，我们将展示该理论如何被用于解释金属的电磁性质、电子集体模式、[超导体](@entry_id:191025)的[迈斯纳效应](@entry_id:273600)以及[量子自旋液体](@entry_id:136269)中的奇异激发等前沿现象。最后，第三章“动手实践”将通过精选的计算问题，引导读者将理论知识应用于具体模型的分析中。通过本次学习，读者将掌握利用感受系数这一关键工具，来剖析和理解复杂物质世界背后的物理规律。

## 原理与机制

本章深入探讨了[线性响应理论](@entry_id:145737)的核心原理与机制。我们将从第一性原理出发，建立系统的响应与微扰之间的普适关系，并由此推导出[响应函数](@entry_id:142629)的一系列基本性质。这些性质不仅深刻揭示了物理系统在微扰下的行为规律，也为实际计算和理解实验现象提供了坚实的理论框架。

### 感受系数的定义：[久保公式](@entry_id:144041)

在探索系统如何响应外部微扰时，我们的出发点是量子力学的基本演化方程。考虑一个处于温度 $T$（对应[逆温](@entry_id:140086) $\beta = 1/(k_B T)$）的热平衡态系统，其未受扰动的[哈密顿量](@entry_id:172864)为 $H_0$。在初始时刻 $t_0 \to -\infty$，系统由[平衡态](@entry_id:168134)密度矩阵 $\rho_0 = e^{-\beta H_0} / Z$ 描述，其中 $Z = \mathrm{Tr}(e^{-\beta H_0})$ 是[配分函数](@entry_id:193625)。从某一时刻起，系统受到一个微弱、时变的外部场 $f(t)$ 的作用，该场通过一个[厄米算符](@entry_id:153410) $B$ 与系统耦合。总[哈密顿量](@entry_id:172864)变为 $H(t) = H_0 + H'(t)$，其中微扰项为 $H'(t) = -f(t)B$。

我们的目标是计算另一个厄米算符（可观测量）$A$ 的[期望值](@entry_id:153208)的变化 $\delta\langle A(t) \rangle$。系统的[密度矩阵](@entry_id:139892) $\rho(t)$ 的时间演化由刘维尔-冯诺依曼方程描述：$i\hbar \frac{d\rho(t)}{dt} = [H(t), \rho(t)]$。为了求解这个方程，我们转换到[相互作用绘景](@entry_id:198213)。在[相互作用绘景](@entry_id:198213)中，算符按 $H_0$ 演化，而态（密度矩阵）则在微扰[哈密顿量](@entry_id:172864) $H'_I(t)$ 的驱动下演化。

在[相互作用绘景](@entry_id:198213)中，密度矩阵 $\rho_I(t)$ 的演化方程为 $i\hbar \frac{d\rho_I(t)}{dt} = [H'_I(t), \rho_I(t)]$，其中 $H'_I(t) = e^{iH_0 t/\hbar} H'(t) e^{-iH_0 t/\hbar} = -f(t) B_I(t)$。这里 $B_I(t)$ 是在[相互作用绘景](@entry_id:198213)（等价于相对于 $H_0$ 的[海森堡绘景](@entry_id:141162)）中的算符。对此方程进行积分，并考虑到微扰 $f(t)$ 的微弱性，我们可以进行线性近似，即用零阶密度矩阵 $\rho_0$ 替代积分内的 $\rho_I(t')$。经过推导，我们得到可观测量 $A$ [期望值](@entry_id:153208)的线性变化为：

$$
\delta\langle A(t) \rangle = \int_{-\infty}^{t} dt' f(t') \frac{i}{\hbar} \langle [A_I(t), B_I(t')] \rangle_0
$$

其中 $\langle \cdots \rangle_0$ 表示在未受扰动的平衡态 $\rho_0$ 下的系综平均。由于平衡态是定态，关联函数只依赖于时间差 $t-t'$。因此，上式可以写成一个卷积形式：

$$
\delta\langle A(t) \rangle = \int_{-\infty}^{\infty} dt' \chi_{AB}(t-t') f(t')
$$

这里的核心量 $\chi_{AB}(t)$ 被定义为**[线性响应函数](@entry_id:160418)**或**感受系数**（susceptibility）。它的具体形式，即著名的**[久保公式](@entry_id:144041)** (Kubo formula)，是 [@problem_id:3001048] [@problem_id:3001082]：

$$
\chi_{AB}(t) = \frac{i}{\hbar} \theta(t) \langle [A_H(t), B_H(0)] \rangle_0
$$

其中 $\theta(t)$ 是亥维赛德阶跃函数，它保证了**因果性**（响应不会发生在微扰之前）。算符 $A_H(t)$ 和 $B_H(0)$ 是相对于未扰动[哈密顿量](@entry_id:172864) $H_0$ 的[海森堡绘景](@entry_id:141162)算符。这个公式是现代[多体理论](@entry_id:169452)的基石之一，它将一个宏观的响应现象（由 $\chi_{AB}$ 描述）与系统在微观层面上的[平衡态](@entry_id:168134)量子涨落（由算符的对易子关联函数描述）直接联系起来。这个公式的成立依赖于几个关键假设：微扰足够弱（线性近似成立）、系统初始处于热平衡态，以及微扰是从遥远过去绝热地开启的。

### [因果性与解析性](@entry_id:196090)质

[久保公式](@entry_id:144041)中阶跃函数 $\theta(t)$ 的存在是**[因果性原理](@entry_id:163284)**的直接体现：在 $t$ 时刻的响应 $\delta\langle A(t) \rangle$ 只能依赖于过去及现在（$t' \le t$）的微扰 $f(t')$。这意味着，对于 $t0$，$\chi_{AB}(t)$ 必然为零。这个看似简单的时域性质，在[频域](@entry_id:160070)中却有着深刻的物理和数学含义。

我们通过[傅里叶变换](@entry_id:142120)进入[频域](@entry_id:160070)，定义 $\chi_{AB}(\omega) = \int_{-\infty}^{\infty} dt\, e^{i\omega t} \chi_{AB}(t)$。由于 $\chi_{AB}(t0)=0$，积分下限实际上是从 0 开始的 [@problem_id:3001073]：

$$
\chi_{AB}(\omega) = \int_{0}^{\infty} dt\, e^{i\omega t} \chi_{AB}(t)
$$

现在，我们将频率 $\omega$ 推广到复平面。积分项中的指数因子变为 $e^{i\omega t} = e^{i(\text{Re}\,\omega)t} e^{-(\text{Im}\,\omega)t}$。当 $\omega$ 位于复平面的[上半平面](@entry_id:199119)（即 $\text{Im}\,\omega > 0$）时，因子 $e^{-(\text{Im}\,\omega)t}$ 是一个随 $t$ 增大的指数衰减项。对于任何物理上稳定的系统，其响应函数 $\chi_{AB}(t)$ 在 $t \to \infty$ 时不会[指数增长](@entry_id:141869)，因此这个衰减因子确保了傅里叶[积分的收敛](@entry_id:187300)性。这意味着，**由因果性决定的响应函数 $\chi_{AB}(\omega)$ 在整个[复频率](@entry_id:266400)上半平面是解析的**。[@problem_id:3001073]

系统的稳定性进一步要求，响应函数的任何[奇点](@entry_id:137764)（如极点或[分支切割](@entry_id:174657)，对应于系统的共振吸收频率）都必须位于[实轴](@entry_id:148276)或下半平面。如果在[上半平面](@entry_id:199119)存在[奇点](@entry_id:137764)，其对[时域响应](@entry_id:271891)的贡献将随时间指数增长，意味着系统不稳定。

此外，由于 $A$ 和 $B$ 是厄米算符，且外场 $f(t)$ 是实数，因此响应 $\delta\langle A(t) \rangle$ 也必须是实数。这要求响应函数 $\chi_{AB}(t)$ 本身是一个实值函数。一个实值函数的[傅里叶变换](@entry_id:142120)具有对称性：$\chi_{AB}(-\omega) = [\chi_{AB}(\omega)]^*$。将 $\chi_{AB}(\omega)$ 分解为实部和虚部 $\chi_{AB}(\omega) = \text{Re}\,\chi_{AB}(\omega) + i\,\text{Im}\,\chi_{AB}(\omega)$，这个对称性意味着 $\text{Re}\,\chi_{AB}(\omega)$ 是 $\omega$ 的[偶函数](@entry_id:163605)，而 $\text{Im}\,\chi_{AB}(\omega)$ 是 $\omega$ 的[奇函数](@entry_id:173259)。[@problem_id:3001073]

### 克拉默-克罗尼格关系

感受系数 $\chi_{AB}(\omega)$ 在[上半平面](@entry_id:199119)的解析性是一个非常强的约束，它导致了其真实部和虚部之间存在一个普适的数学关系，即**克拉默-克罗尼格关系** (Kramers-Kronig relations)。该关系本质上是[柯西积分定理](@entry_id:194141)的应用，它表明，如果我们知道了 $\chi_{AB}(\omega)$ 在整个[实轴](@entry_id:148276)上的虚部（或实部），我们就可以通过一个[积分变换](@entry_id:186209)唯一地确定其在整个[实轴](@entry_id:148276)上的实部（或虚部）。

其一般形式为 [@problem_id:3001081]：

$$
\text{Re}\,\chi_{AB}(\omega) = \frac{1}{\pi} \mathcal{P} \int_{-\infty}^{\infty} d\omega' \frac{\text{Im}\,\chi_{AB}(\omega')}{\omega' - \omega}
$$

$$
\text{Im}\,\chi_{AB}(\omega) = -\frac{1}{\pi} \mathcal{P} \int_{-\infty}^{\infty} d\omega' \frac{\text{Re}\,\chi_{AB}(\omega')}{\omega' - \omega}
$$

其中 $\mathcal{P}$ 表示[柯西主值](@entry_id:192761)积分。这些关系的成立只需满足线性和因果性，以及[响应函数](@entry_id:142629)在无穷高频时趋于零的物理要求。

利用前一节讨论的对称性（实部为[偶函数](@entry_id:163605)，虚部为奇函数），我们可以将积分区间折叠到正半轴，得到在实验和理论中更常用的形式 [@problem_id:3001081]：

$$
\text{Re}\,\chi_{AB}(\omega) = \frac{2}{\pi} \mathcal{P} \int_{0}^{\infty} d\omega' \frac{\omega' \text{Im}\,\chi_{AB}(\omega')}{\omega'^2 - \omega^2}
$$

$$
\text{Im}\,\chi_{AB}(\omega) = -\frac{2\omega}{\pi} \mathcal{P} \int_{0}^{\infty} d\omega' \frac{\text{Re}\,\chi_{AB}(\omega')}{\omega'^2 - \omega^2}
$$

克拉默-克罗尼格关系的重要性在于它连接了系统的**[色散](@entry_id:263750)**（由 $\text{Re}\,\chi$ 描述）和**吸收/耗散**（由 $\text{Im}\,\chi$ 描述）。例如，在光学中，它连接了材料的[折射率](@entry_id:168910)和[吸收系数](@entry_id:156541)。

### 涨落-耗散定理

[线性响应理论](@entry_id:145737)最深刻的成果之一是**涨落-耗散定理** (Fluctuation-Dissipation Theorem, FDT)。该定理揭示了两个看似无关的物理过程之间的内在联系：
1.  **涨落** (Fluctuation)：系统在没有外部微扰的[热平衡](@entry_id:141693)状态下，其物理量围绕平均值的自发、随机的起伏。这些涨落由平衡态关联函数描述，例如 $\langle A(t)A(0) \rangle$。其[傅里叶变换](@entry_id:142120) $S_{AA}(\omega) = \int_{-\infty}^{\infty} dt\, e^{i\omega t} \langle A(t)A(0) \rangle$ 被称为**噪声[功率谱](@entry_id:159996)**。
2.  **耗散** (Dissipation)：系统在受到外部周期性驱动时，从外部场吸收能量并转化为内能（热）的过程。能量耗散的速率正比于感受系数的虚部 $\text{Im}\,\chi_{AA}(\omega)$（通常记作 $\chi''_{AA}(\omega)$）。

量子涨落-耗散定理给出了这两者之间的精确关系。而在[经典极限](@entry_id:148587)下，即热能远大于量子[能量子](@entry_id:145536)（$k_B T \gg \hbar\omega$），该定理具有一个非常简洁的形式 [@problem_id:2990590]：

$$
S_{AA}(\omega) = \frac{2k_B T}{\omega} \chi''_{AA}(\omega)
$$

这个**经典涨落-耗散定理**表明，在给定频率下，系统的[平衡态](@entry_id:168134)热涨落强度（噪声谱）与系统在该频率下对外界微扰的耗散能力成正比，[比例因子](@entry_id:266678)为热能 $k_B T$。这个定理的适用条件是：系统处于热平衡态，外场是线性的弱微扰，并且处于[经典极限](@entry_id:148587)。这一定理是连接非平衡响应和平衡统计物理的桥梁，例如，它解释了导体中的热噪声（约翰逊-奈奎斯特噪声）和其[电导](@entry_id:177131)（耗散）之间的关系。

### 感受系数的计算与应用

#### [静态极限](@entry_id:262480)

当外部微扰是静态的（与时间无关）时，我们关心的是**静态感受系数** $\chi_{AB}(0)$。它描述了系统在一个恒定外场 $h$ 作用下的平衡态响应。根据定义，它是响应[期望值](@entry_id:153208)对场强的[热力学](@entry_id:141121)导数 [@problem_id:3001087]：

$$
\chi_{AB}(0) = \left. \frac{\partial \langle A \rangle_h}{\partial h} \right|_{h=0}
$$

其中 $\langle \cdot \rangle_h$ 表示在[哈密顿量](@entry_id:172864) $H(h) = H_0 - hB$ 下的平衡平均。通过对系综平均的表达式求导，可以得到静态感受系数的一般[久保公式](@entry_id:144041)，它是一个虚时积分：

$$
\chi_{AB}(0) = \int_{0}^{\beta} d\lambda\, \left( \langle A_H(i\hbar\lambda) B_H(0) \rangle_0 - \langle A \rangle_0 \langle B \rangle_0 \right)
$$

这里 $A_H(i\hbar\lambda) = e^{-\lambda H_0} A e^{\lambda H_0}$ 是虚时海森堡算符。这个形式在不假设任何算符对易性的情况下普遍成立。[@problem_id:3001087]

一个重要的特例是，如果算符 $B$ 是一个守恒量，即它与未扰动[哈密顿量](@entry_id:172864)对易（$[H_0, B] = 0$），那么上述积分可以被立即求出，静态感受系数简化为一个静态的协[方差](@entry_id:200758) [@problem_id:3001087]：

$$
\chi_{AB}(0) = \beta \left( \langle AB \rangle_0 - \langle A \rangle_0 \langle B \rangle_0 \right)
$$

这个关系式在[热力学](@entry_id:141121)中非常有用。例如，如果我们考虑对外场（化学势 $\mu$）的响应，对应的算符 $B$ 是[粒子数算符](@entry_id:153568) $N$。由于 $[H_0, N]=0$，我们可以用这个简化公式计算各种与[粒子数涨落](@entry_id:151853)相关的[热力学](@entry_id:141121)量。一个典型的例子是，系统的**[等温压缩率](@entry_id:140894)** $\kappa_T$ 与系统的[粒子数涨落](@entry_id:151853)直接相关 [@problem_id:3001087]：

$$
\kappa_T = \frac{\beta V}{\langle N \rangle^2} (\langle N^2 \rangle_0 - \langle N \rangle_0^2)
$$

这个结果将一个宏观[热力学](@entry_id:141121)量（压缩率）与微观的[粒子数涨落](@entry_id:151853)联系起来，是静态[响应理论](@entry_id:188225)的有力证明。

#### 屏蔽与介电函数

[线性响应理论](@entry_id:145737)在理解多体系统（如[金属中的电子](@entry_id:138687)气）中的**屏蔽** (screening) 现象时至关重要。当一个外加[电势](@entry_id:267554) $V_{\text{ext}}$ 施加到[电子气](@entry_id:140692)上时，电子会重新[分布](@entry_id:182848)以试图“屏蔽”这个外场，导致系统内部的电子感受到的**总[电势](@entry_id:267554)** $V_{\text{tot}}$ 与外加[电势](@entry_id:267554)不同。

为了精确描述这个过程，我们引入三个关键的[响应函数](@entry_id:142629) [@problem_id:3001063]：
1.  **可约（或全）密度-密度感受系数** $\chi_{nn}(\mathbf{q}, \omega)$：它描述了由**外部**[电势](@entry_id:267554) $\delta V_{\text{ext}}(\mathbf{q}, \omega)$ 引起的感生[电荷密度](@entry_id:144672) $\delta n(\mathbf{q}, \omega)$ 的响应：$\delta n = \chi_{nn} \delta V_{\text{ext}}$。
2.  **不可约极化率** $\Pi(\mathbf{q}, \omega)$：它描述了由**总**[电势](@entry_id:267554) $\delta V_{\text{tot}}(\mathbf{q}, \omega)$ 引起的感生[电荷密度](@entry_id:144672)的响应：$\delta n = \Pi \delta V_{\text{tot}}$。$\Pi$ 被称为“不可约”是因为它不包含通过库仑相互作用传递的内部[屏蔽效应](@entry_id:136974)。
3.  **介电函数** $\epsilon(\mathbf{q}, \omega)$：它量化了屏蔽的程度，定义为外部[电势](@entry_id:267554)与总[电势](@entry_id:267554)之比：$\epsilon = \delta V_{\text{ext}} / \delta V_{\text{tot}}$。

通过联立这些定义以及总[电势](@entry_id:267554)的构成（$\delta V_{\text{tot}} = \delta V_{\text{ext}} + v_c \delta n$，其中 $v_c(\mathbf{q})$ 是[库仑相互作用](@entry_id:747947)的傅里叶分量），我们可以推导出这些响应函数之间的重要关系：

$$
\epsilon(\mathbf{q}, \omega) = 1 - v_c(\mathbf{q}) \Pi(\mathbf{q}, \omega)
$$

$$
\chi_{nn}(\mathbf{q}, \omega) = \frac{\Pi(\mathbf{q}, \omega)}{1 - v_c(\mathbf{q}) \Pi(\mathbf{q}, \omega)} = \frac{\Pi(\mathbf{q}, \omega)}{\epsilon(\mathbf{q}, \omega)}
$$

这些关系是多体物理中**随机相近似** (Random Phase Approximation, RPA) 的核心。在 RPA 中，人们通过计算更简单的不可约极化率 $\Pi$（通常用无相互作用电子气的响应来近似），然后利用上述公式来获得描述了复杂屏蔽效应的全感受系数 $\chi_{nn}$ 和[介电函数](@entry_id:136859) $\epsilon$。

#### [林哈德函数](@entry_id:147872)：一个具体的计算实例

为了使讨论更具体，我们考虑计算一个无相互作用的[费米气体](@entry_id:145305)的不可约极化率 $\Pi_0(\mathbf{q}, \omega)$。这个量被称为**[林哈德函数](@entry_id:147872)** (Lindhard function)。它描述了无相互作用的电子如何响应它们所感受到的**总**[电势](@entry_id:267554)。其计算可以从[久保公式](@entry_id:144041)出发，通过对所有可能的电子-空穴对激发求和来完成。[林哈德函数](@entry_id:147872)的表达式为 [@problem_id:3001052]：

$$
\Pi_0(\mathbf{q}, \omega) = g_s \sum_{\mathbf{k}} \frac{f(\epsilon_{\mathbf{k}}) - f(\epsilon_{\mathbf{k}+\mathbf{q}})}{\hbar\omega + i0^+ + \epsilon_{\mathbf{k}} - \epsilon_{\mathbf{k}+\mathbf{q}}}
$$

其中 $g_s$ 是自旋简并度（对电子为2），$f(\epsilon_{\mathbf{k}})$ 是[费米-狄拉克分布](@entry_id:138909)函数，$\epsilon_{\mathbf{k}}$ 是电子的色散关系。分母中的能量差 $\epsilon_{\mathbf{k}+\mathbf{q}} - \epsilon_{\mathbf{k}}$ 对应于将一个动量为 $\mathbf{k}$ 的电子激发到动量为 $\mathbf{k}+\mathbf{q}$ 的状态所需的能量。分子的费米函数之差 $f(\epsilon_{\mathbf{k}}) - f(\epsilon_{\mathbf{k}+\mathbf{q}})$ 则保证了只有从占据态到非占据态的跃迁才对响应有贡献，这体现了[泡利不相容原理](@entry_id:141850)。[林哈德函数](@entry_id:147872)是理解金属电子性质，如等离激元、屏蔽和超导电性的理论基础。

### 高级形式与守恒律

#### 松原形式

在有限温度的[量子多体问题](@entry_id:146763)中，直接计算实时[格林函数](@entry_id:147802)（如 retarded susceptibility）通常很困难。**虚时（或松原）形式** (imaginary-time or Matsubara formalism) 为此提供了一个强大的计算框架。其核心思想是将时间变量 $t$ [解析延拓](@entry_id:147225)到[虚轴](@entry_id:262618) $t \to -i\tau$，其中虚时 $\tau$ 在区间 $[0, \beta\hbar]$ 内取值。

在此框架下，我们定义**松原感受系数** [@problem_id:3001038]：

$$
\chi_{AB}(\tau) = - \langle T_\tau A(\tau) B(0) \rangle_c
$$

其中 $T_\tau$ 是虚时排序算符，它将算符按照虚时 $\tau$ 的大小进行排序。对于[玻色算符](@entry_id:148361)，关联函数在虚时上具有周期性 $\chi_{AB}(\tau) = \chi_{AB}(\tau+\beta\hbar)$，这导致其[傅里叶级数](@entry_id:139455)只包含离散的**玻色[松原频率](@entry_id:197724)** $\omega_n = 2\pi n / (\beta\hbar)$。

松原形式的巨大优势在于，物理上可观测的**推迟感受系数** $\chi^R_{AB}(\omega)$ 可以通过对计算出的松原感受系数 $\chi_{AB}(i\omega_n)$ 进行**解析延拓** (analytic continuation) 得到 [@problem_id:3001038]：

$$
\chi^R_{AB}(\omega) = \chi_{AB}(i\omega_n \to \omega + i0^+)
$$

这种方法将复杂的实时动力学计算转化为一个相对更易处理的、在虚时下的[平衡态](@entry_id:168134)计算，是现代[凝聚态理论](@entry_id:141958)中不可或缺的工具。

#### [自能](@entry_id:145608)、[顶点修正](@entry_id:146982)与守恒律

在微扰论的图示语言中，相互作用对系统的影响体现在两个方面：
1.  **[自能](@entry_id:145608)** (Self-energy, $\Sigma$)：它修正了单[粒子传播子](@entry_id:195036)（[费米子](@entry_id:146235)线），描述了一个粒子在运动过程中与其周围环境相互作用而“着装” (dressed) 的效应，如有效质量的改变和有限的寿命。
2.  **[顶点修正](@entry_id:146982)** (Vertex correction, $\Gamma$)：它修正了粒子与外场的相互作用顶点，描述了相互作用如何改变粒子响应外场的方式。

一个常见的、但往往是错误的近似是，只考虑[自能修正](@entry_id:754667)（即使用“着装”的传播子）而忽略[顶点修正](@entry_id:146982)（使用裸顶点）。这种近似通常会破坏系统的基本对称性，导致违反诸如[电荷守恒](@entry_id:264158)、[动量守恒](@entry_id:149964)等基本物理定律的非物理结果。[@problem_id:3001034]

电荷守恒在微观层面上的精确表述是**[沃德-高桥恒等式](@entry_id:145721)** (Ward-Takahashi identity)。这个恒等式严格地将全[顶点函数](@entry_id:145137) $\Gamma$，全[格林函数](@entry_id:147802) $G$（包含自能 $\Sigma$）联系在一起。它揭示了，任何引入了依赖于动量或能量的[自能](@entry_id:145608) $\Sigma$ 的近似，都必须同时引入一个与之相洽的[顶点修正](@entry_id:146982) $\Gamma$，才能保证[沃德恒等式](@entry_id:147000)成立，从而保证电荷守恒。[@problem_id:3001034]

满足这种洽性的近似被称为**[守恒近似](@entry_id:139611)**。例如，基于[Luttinger-Ward泛函](@entry_id:138202)的Baym-Kadanoff构造能够系统地产生自能和[顶点修正](@entry_id:146982)，从而确保物理守恒律得到满足。在[杂质散射](@entry_id:267814)导致的直流[电导](@entry_id:177131)问题中，[顶点修正](@entry_id:146982)（对应于“梯[子图](@entry_id:273342)”）与[自能修正](@entry_id:754667)同等重要，二者共同作用才能得到正确的Drude[电导率](@entry_id:137481)，并满足电荷守恒。忽略[顶点修正](@entry_id:146982)将导致错误的结果。[@problem_id:3001034] 因此，在处理相互作用系统的响应问题时，深刻理解[自能](@entry_id:145608)和[顶点修正](@entry_id:146982)的角色以及它们之间的内在联系是至关重要的。