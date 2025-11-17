## 引言
频率相关[介电函数 ε(ω)](@entry_id:141637) 是凝聚态物理学的基石，它描述了材料如何响应时变[电磁场](@entry_id:265881)，是连接微观[电荷](@entry_id:275494)动力学与宏观光学、电学性质的核心物理量。然而，在许多入门级讨论中，[介电常数](@entry_id:146714)常被简化为一个静态值，这掩盖了其背后丰富的动态物理过程。本文旨在填补这一认知空白，系统性地揭示 ε(ω) 如何编码物质内部从电子到晶格振动的复杂响应机制。

在接下来的内容中，我们将踏上一段从基础到前沿的探索之旅。第一章“原理与机制”将从经典的Drude和[Lorentz模型](@entry_id:144803)出发，建立[介电函数](@entry_id:136859)的微观图像，并深入探讨等离激元等[集体激发](@entry_id:145026)以及因果律施加的普适约束。第二章“应用与[交叉](@entry_id:147634)学科联系”将展示 ε(ω) 作为一个强大工具，如何解释从材料光学到生物物理的广泛现象。最后，在“动手实践”部分，读者将通过具体的计算问题来巩固所学知识。

## 原理与机制

本章旨在深入探讨材料的[频率相关介电函数](@entry_id:139439) $\epsilon(\omega)$ 背后的基本原理和微观机制。介电函数是连接物质内部[电荷](@entry_id:275494)动力学与宏观电磁响应的关键桥梁，它决定了材料如何与[电磁场](@entry_id:265881)相互作用。我们将从描述不同类型材料（金属和绝缘体）中电子响应的经典模型出发，逐步深入到等离激元等[集体激发](@entry_id:145026)，并最终讨论由因果律等基本物理原理所施加的普适性约束。

### 微观动力学模型

材料对[时变电场](@entry_id:197741)的响应本质上源于其内部[电荷](@entry_id:275494)（主要是电子）在外场驱动下的运动。通过对这些微观动力学过程建立模型，我们可以推导出宏观的介电函数。

#### Drude模型：金属中自由电子的响应

20世纪初，Paul Drude 提出了一个简洁而成功的模型来描述[金属中的电子输运](@entry_id:147204)和光学性质。该模型将金属中的导电电子视为一种[自由电子气](@entry_id:145649)体，它们在[晶格](@entry_id:196752)中自由运动，但会与离子实或杂质发生碰撞，从而产生一种等效的阻尼力。

考虑一个质量为 $m^*$（[有效质量](@entry_id:142879)）、[电荷](@entry_id:275494)为 $-e$ 的电子，在时谐[电场](@entry_id:194326) $\vec{E}(t) = \vec{E}_0 \exp(-i\omega t)$ 的驱动下运动。其运动方程可以写为：
$$ m^* \frac{d\vec{v}}{dt} + m^* \gamma \vec{v} = -e\vec{E}(t) $$
其中 $\vec{v}$ 是电子的漂移速度，$\gamma$ 是一个唯象的阻尼率，代表了动量弛豫的速率，它与电子两次碰撞之间的平均时间 $\tau$ 呈反比关系，即 $\gamma = 1/\tau$。[@problem_id:64010] [@problem_id:2991608]

在[稳态](@entry_id:182458)下，我们寻找一个同样以[角频率](@entry_id:261565) $\omega$ [振荡](@entry_id:267781)的解 $\vec{v}(t) = \vec{v}(\omega)\exp(-i\omega t)$。将此解代入运动方程，时间导数 $\frac{d}{dt}$ 变为因子 $-i\omega$，我们得到：
$$ (-i\omega m^* + m^*\gamma) \vec{v}(\omega) = -e\vec{E}(\omega) $$
由此可解出[频域](@entry_id:160070)中的速度幅值：
$$ \vec{v}(\omega) = \frac{-e}{m^*(\gamma - i\omega)} \vec{E}(\omega) $$
[宏观电流](@entry_id:203974)密度 $\vec{J}$ 由所有 $n$ 个单位体积内的导电电子贡献，$\vec{J} = -ne\vec{v}$。因此，[频域](@entry_id:160070)中的电流密度为：
$$ \vec{J}(\omega) = -ne\vec{v}(\omega) = \frac{ne^2}{m^*(\gamma - i\omega)} \vec{E}(\omega) $$
根据欧姆定律的推广形式 $\vec{J}(\omega) = \sigma(\omega)\vec{E}(\omega)$，我们得到复电导率 $\sigma(\omega)$：
$$ \sigma(\omega) = \frac{ne^2}{m^*(\gamma - i\omega)} = \frac{ne^2\tau}{m^*(1 - i\omega\tau)} $$
[介电函数](@entry_id:136859) $\epsilon(\omega)$ 与电导率 $\sigma(\omega)$ 之间存在普遍关系。考虑总电流密度（包括[位移电流](@entry_id:190231)）和[电位移矢量](@entry_id:197092) $\vec{D}$ 的关系，我们可以推导出 $\vec{D}(\omega) = \epsilon_0\epsilon(\omega)\vec{E}(\omega)$。在包含自由载流子的情况下，总的[介电响应](@entry_id:140146)由两部分组成：一部分来自高频[带间跃迁](@entry_id:138793)等过程贡献的背景[介电常数](@entry_id:146714) $\epsilon_\infty$，另一部分来自自由载流子的贡献。后者可以通过电导率来描述。它们之间的关系为：
$$ \epsilon(\omega) = \epsilon_\infty + \frac{i\sigma(\omega)}{\epsilon_0 \omega} $$
将我们得到的 Drude [电导率](@entry_id:137481)代入上式，便可得到 Drude 模型的介电函数：
$$ \epsilon(\omega) = \epsilon_\infty + \frac{i}{\epsilon_0 \omega} \frac{ne^2}{m^*(\gamma - i\omega)} = \epsilon_\infty - \frac{ne^2}{m^*\epsilon_0} \frac{1}{\omega(\omega + i\gamma)} $$
这里我们引入一个极其重要的物理量——**等离子体频率 (plasma frequency)** $\omega_p$，其定义为：
$$ \omega_p^2 = \frac{ne^2}{m^*\epsilon_0} $$
[等离子体频率](@entry_id:137429)代表了[电子气](@entry_id:140692)体相对于正离子背景发生[集体振荡](@entry_id:158973)的固有频率。利用此定义，Drude [介电函数](@entry_id:136859)可以写成更紧凑的形式：
$$ \epsilon(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega^2 + i\gamma\omega} $$
我们可以将其分解为实部 $\epsilon_1(\omega)$ 和虚部 $\epsilon_2(\omega)$：
$$ \epsilon_1(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega^2 + \gamma^2} $$
$$ \epsilon_2(\omega) = \frac{\gamma\omega_p^2}{\omega(\omega^2 + \gamma^2)} $$
介电函数的实部和虚部各自承载着不同的物理意义。$\epsilon_1(\omega)$ 描述了[材料的极化](@entry_id:271610)和屏蔽能力。当 $\epsilon_1(\omega)  0$ 时，[电磁波](@entry_id:269629)无法在材料内部传播，导致高的[反射率](@entry_id:155393)，这是金属在低频（例如可见光频段）不透明并呈现[金属光泽](@entry_id:274936)的原因。当 $\epsilon_1(\omega) > 0$ 时，材料原则上可以变得透明。而 $\epsilon_2(\omega)$ 则描述了能量的吸收或损耗，它与阻尼率 $\gamma$ 直接相关，反映了电子在运动中通过碰撞将从[电磁场](@entry_id:265881)获得的能量耗散掉的过程。

#### [Lorentz模型](@entry_id:144803)：绝缘体中束缚电子的响应

与金属不同，理想绝缘体或[半导体](@entry_id:141536)在低能量下没有自由电子。电子被束缚在[原子核](@entry_id:167902)周围，只能在原子内部发生极化。当外[电场](@entry_id:194326)作用时，这些束缚电子的响应可以被模拟为一个受驱动的[阻尼谐振子](@entry_id:276848)。这就是 **Lorentz 模型** 的核心思想，它对于理解绝缘体的[介电常数](@entry_id:146714)和[吸收光谱](@entry_id:144611)至关重要。[@problem_id:2991599]

考虑一个被[原子核](@entry_id:167902)束缚的电子，其在平衡位置附近的运动可以用一个[谐振子](@entry_id:155622)来描述。在外加[电场](@entry_id:194326) $\vec{E}(t)$ 的驱动下，其[运动方程](@entry_id:170720)为：
$$ m\ddot{\vec{x}} + m\gamma_j \dot{\vec{x}} + m\omega_j^2 \vec{x} = -e\vec{E}(t) $$
这里，$\vec{x}$ 是电子相对于其平衡位置的位移，$\omega_j$ 是谐振子的固有[共振频率](@entry_id:265742)，对应于原子或分子中的某个[电子跃迁](@entry_id:152949)能级，$\gamma_j$ 是该跃迁的阻尼率。

与 Drude 模型类似，我们求解在时谐[电场](@entry_id:194326)驱动下的[稳态响应](@entry_id:173787)，得到电子位移的[复振幅](@entry_id:164138)：
$$ \vec{x}(\omega) = \frac{-e/m}{\omega_j^2 - \omega^2 - i\omega\gamma_j} \vec{E}(\omega) $$
每个电子的位移会产生一个感生电偶极矩 $\vec{p}(\omega) = -e\vec{x}(\omega)$。材料的[宏观极化](@entry_id:141855)强度 $\vec{P}(\omega)$ 是单位体积内所有偶极矩的总和。如果单位体积内有 $N$ 个可极化的原子，且每个原子对特定跃迁 $j$ 的贡献由一个无量纲的**[振子强度](@entry_id:147221) (oscillator strength)** $f_j$ 来加权，则总的[极化强度](@entry_id:188176)为：
$$ \vec{P}(\omega) = \sum_j N f_j (-e\vec{x}_j(\omega)) = \left( \frac{Ne^2}{m} \sum_j \frac{f_j}{\omega_j^2 - \omega^2 - i\omega\gamma_j} \right) \vec{E}(\omega) $$
[介电函数](@entry_id:136859)与极化率 $\chi(\omega)$（定义为 $\vec{P}(\omega) = \epsilon_0 \chi(\omega) \vec{E}(\omega)$）的关系是 $\epsilon(\omega) = 1 + \chi(\omega)$。同样考虑到其他更高频率跃迁贡献的背景[介电常数](@entry_id:146714) $\epsilon_\infty$，我们得到 Lorentz 模型的[介电函数](@entry_id:136859)：
$$ \epsilon(\omega) = \epsilon_\infty + \frac{Ne^2}{\epsilon_0 m} \sum_j \frac{f_j}{\omega_j^2 - \omega^2 - i\omega\gamma_j} $$
该表达式清楚地显示，当驱动频率 $\omega$ 接近某个固有[共振频率](@entry_id:265742) $\omega_j$ 时，介电函数会出现共振行为。特别是虚部 $\epsilon_2(\omega)$ 会在每个 $\omega_j$ 附近出现一个峰值，对应于材料对特定频率光波的强烈吸收。这正是材料呈现不同颜色的物理根源。

### [集体激发](@entry_id:145026)：等离激元

在 Drude 模型中，我们引入了[等离子体频率](@entry_id:137429) $\omega_p$ 作为一个参数。然而，它的物理意义远不止于此。$\omega_p$ 描述的是[电子气](@entry_id:140692)的一种基本**[集体激发](@entry_id:145026) (collective excitation)** 模式，称为**等离激元 (plasmon)**。

#### 等离激元的起源：介电[函数的零点](@entry_id:180934)

纵向的集体激发模式，如[等离激元](@entry_id:146184)，其存在的条件是系统可以在没有外部驱动场的情况下维持自身[电荷密度](@entry_id:144672)的[振荡](@entry_id:267781)。在[频域](@entry_id:160070)和[波矢](@entry_id:178620)空间中，这意味着总[电势](@entry_id:267554) $\phi_{\text{tot}}(\mathbf{q}, \omega)$ 可以与外部[电势](@entry_id:267554) $\phi_{\text{ext}}(\mathbf{q}, \omega)$ 无关。根据[线性响应理论](@entry_id:145737)，$\phi_{\text{tot}}(\mathbf{q}, \omega) = \phi_{\text{ext}}(\mathbf{q}, \omega) / \epsilon(\mathbf{q}, \omega)$。因此，[自持振荡](@entry_id:269112)的条件就是介电函数为零：
$$ \epsilon(\mathbf{q}, \omega) = 0 $$
这个方程的解给出了[集体激发](@entry_id:145026)模式的[色散关系](@entry_id:140395) $\omega(\mathbf{q})$。

我们可以从更基本的层面推导出 $\omega_p$。例如，在一个简化的[流体力学](@entry_id:136788)模型中，将[电子气](@entry_id:140692)视为一种带电流体，通过线性化的连续性方程和欧拉方程（[牛顿第二定律](@entry_id:274217)），可以推导出在长波极限（即波矢 $\mathbf{q} \to 0$）下的[介电函数](@entry_id:136859)为：[@problem_id:2991603]
$$ \epsilon(\omega) = 1 - \frac{ne^2}{m\epsilon_0\omega^2} $$
令其为零，$1 - \frac{ne^2}{m\epsilon_0\omega^2} = 0$，我们立即得到 $\omega^2 = \frac{ne^2}{m\epsilon_0}$，这正是等离子体频率 $\omega_p$ 的平方。

一个更严谨的量子力学推导是基于**随机相近似 (Random Phase Approximation, RPA)**。RPA的核心物理假设是，每个电子响应的不是复杂的[多体相互作用](@entry_id:751663)场，而是外部场与由所有电子感生出的平均电荷密度所产生的自洽场的总和。[@problem_id:1772796] 在这个框架下，可以计算出与频率和波矢相关的[介电函数](@entry_id:136859) $\epsilon_{\text{RPA}}(\mathbf{q}, \omega)$。在长波极限 ($\mathbf{q} \to 0$) 下，求解 $\epsilon_{\text{RPA}}(\mathbf{q}, \omega) = 0$ 同样可以得到 $\omega = \omega_p$。[@problem_id:92117] 这表明，[体等离激元](@entry_id:143484)是[电子气](@entry_id:140692)在长波极限下的一种稳定的、能量确定的集体振荡模式。

#### 等离激元的观测：能量损失谱

理论上预言的[等离激元](@entry_id:146184)如何在实验上被观测到？一种强大的技术是**[电子能量损失谱](@entry_id:142352) (Electron Energy Loss Spectroscopy, EELS)**。当一束高能电子穿过薄膜样品时，它会与材料中的电子相互作用，并可能激发集体模式（如[等离激元](@entry_id:146184)）而损失一部分能量。通过分析出射电子的能量[分布](@entry_id:182848)，就可以得到材料的激发谱。

与[能量损失](@entry_id:159152)过程直接相关的物理量是**损失函数 (loss function)**，其定义为：
$$ L(\omega) = -\text{Im}\left[\frac{1}{\epsilon(\omega)}\right] $$
这个量的物理意义是，它正比于[电场](@entry_id:194326)在材料中单位体积、单位时间内所做的功，即能量耗散的速率。因此，[损失函数](@entry_id:634569)的峰值对应于材料中最有效的能量吸收通道。[@problem_id:2991595]

对于一个 Drude 金属，将 $\epsilon(\omega) = \epsilon_\infty - \frac{\omega_p^2}{\omega^2+i\gamma\omega}$ 代入，可以推导出损失函数的形式。分析表明，损失函数 $L(\omega)$ 是一个在[等离子体频率](@entry_id:137429)附近的洛伦兹型峰。这个峰的峰位 $\omega_{\text{peak}}$ 在哪里？

一个直观的想法是，[集体激发](@entry_id:145026)最强时，$\epsilon(\omega)$ 应该“接近”于零。在无阻尼的理想情况下 ($\gamma=0$)，$\epsilon(\omega)=0$ 给出 $\omega = \omega_p/\sqrt{\epsilon_\infty}$，我们称之为**屏蔽[等离子体频率](@entry_id:137429)** $\omega_{\text{pl}}$。在有阻尼的真实情况下，人们通常以实部为零的位置来近似定义[等离激元](@entry_id:146184)频率，即 $\epsilon_1(\omega_{\text{pl}}) = 0$。求解这个条件给出：[@problem_id:2991608]
$$ \omega_{\text{pl}}^2 = \frac{\omega_p^2}{\epsilon_\infty} - \gamma^2 $$
然而，通过严格计算损失函数 $L(\omega)$ 的极大值，可以发现其峰位 $\omega_{\text{peak}}$ 与 $\omega_{\text{pl}}$ 并不完全重合。在弱阻尼极限 ($\gamma \ll \omega_p$) 下，可以证明：[@problem_id:2991595]
$$ \omega_{\text{peak}}^2 \approx \frac{\omega_p^2}{\epsilon_\infty} - \frac{1}{4}\gamma^2 $$
这意味着损失谱的峰值[频率比](@entry_id:202730)[介电函数](@entry_id:136859)实部过零点的频率要高，它们之间的差值为：
$$ \Delta = \omega_{\text{peak}}^2 - \omega_{\text{pl}}^2 = \frac{3}{4}\gamma^2 $$
这个结果精妙地揭示了阻尼对[等离激元共振](@entry_id:197204)峰位置的细微影响。在 EELS 实验中测量到的正是 $\omega_{\text{peak}}$。

### 基本约束与普适性质

[介电函数](@entry_id:136859)作为描述物理系统线性响应的函数，必须遵循一些源于基本物理原理的普适性约束，这些约束独立于具体的微观模型。

#### 因果律与Kramers-Kronig关系

一个基本原理是**因果律 (causality)**：响应不能先于驱动。就[介电响应](@entry_id:140146)而言，材料的电极化 $\vec{P}(t)$ 不能在施加[电场](@entry_id:194326) $\vec{E}(t)$ 之前出现。这一看似简单的物理要求，在数学上对[响应函数](@entry_id:142629) $\epsilon(\omega)$ 的[解析性](@entry_id:140716)质施加了强大的约束。它要求 $\epsilon(\omega)$ 作为[复频率](@entry_id:266400) $\omega$ 的函数，在上半复平面是解析的。

这一[解析性](@entry_id:140716)带来的一个深刻结果是**Kramers-Kronig (K-K) 关系**。它将介电函数的实部和虚部通过一个[积分变换](@entry_id:186209)联系起来：
$$ \epsilon_1(\omega) - 1 = \frac{1}{\pi} \mathcal{P} \int_{-\infty}^{\infty} \frac{\epsilon_2(\omega')}{\omega' - \omega} d\omega' $$
$$ \epsilon_2(\omega) = -\frac{1}{\pi} \mathcal{P} \int_{-\infty}^{\infty} \frac{\epsilon_1(\omega')-1}{\omega' - \omega} d\omega' $$
其中 $\mathcal{P}$ 表示[柯西主值](@entry_id:192761)积分。这意味着，如果我们知道了材料在所有频率下的吸收谱（即 $\epsilon_2(\omega)$），我们原则上就可以计算出它在任意频率下的[色散](@entry_id:263750)性质（即 $\epsilon_1(\omega)$），反之亦然。

K-K 关系有许多重要的应用，其中之一是所谓的**求和规则 (sum rule)**。例如，我们可以利用 K-K 关系推导静态[介电常数](@entry_id:146714) $\epsilon(0)$ 与吸收谱之间的关系。考虑到在高频极限下，所有电子都无法跟上[电场](@entry_id:194326)的变化，材料的响应趋于真空，即 $\lim_{\omega\to\infty} \epsilon(\omega) = 1$。在此条件下，可以得到：[@problem_id:1787946]
$$ \epsilon(0) = 1 + \frac{2}{\pi} \int_0^\infty \frac{\epsilon_2(\omega')}{\omega'} d\omega' $$
这个公式表明，材料的[静态屏蔽](@entry_id:262850)能力（由 $\epsilon(0)$ 衡量）是由其在整个[电磁波谱](@entry_id:147565)上的吸收特性（由 $\epsilon_2(\omega)$ 描述）所决定的。

#### 因果律与稳定性

因果律的另一个直接物理推论是系统的**稳定性 (stability)**。一个[因果系统](@entry_id:264914)对于一个微小的扰动，其响应不能随时间无限增长。任何不稳定的模式（其能量随时间指数增长）都将违反因果律，因为它意味着系统可以从无穷远的过去“预知”扰动并放大它。

对于集体激发模式，稳定性要求其复数频率 $\omega = \omega_{\text{real}} - i\omega_{\text{imag}}$ 的虚部必须是正的（按 $e^{-i\omega t}$ 约定）或实的，即 $\text{Im}(\omega) \le 0$。这样，模式的振幅 $e^{-i\omega t} = e^{-\text{Im}(\omega)t} e^{-i\text{Re}(\omega)t}$ 将随时间衰减或保持不变，而不会发散。

这个[稳定性判据](@entry_id:755304)可以用来约束我们构建的[唯象模型](@entry_id:273816)。例如，考虑一个包含[空间色散](@entry_id:141344)效应的模型[介电函数](@entry_id:136859)：[@problem_id:8810]
$$ \epsilon(k, \omega) = 1 - \frac{\omega_p^2}{\omega^2 + i\nu\omega - \beta k^2} $$
其中 $\beta$ 是描述[空间色散](@entry_id:141344)（即对[波矢](@entry_id:178620) $k$ 的依赖性）的实常数。该系统的[集体模](@entry_id:137129)式频率由 $\epsilon(k, \omega) = 0$ 给出，解得：
$$ \omega = -i\frac{\nu}{2} \pm \frac{1}{2}\sqrt{4(\omega_p^2 + \beta k^2) - \nu^2} $$
为了保证对所有可能的实数波矢 $k$，$\text{Im}(\omega) \le 0$ 恒成立，我们必须要求被开方项在为负时不能导致正的虚部。经过分析，这最终要求对所有 $k$ 都有 $\omega_p^2 + \beta k^2 \ge 0$。由于 $\omega_p^20$ 且 $k^2 \ge 0$，要使此式恒成立，唯一的可能是 $\beta$ 不能为负，即：
$$ \beta \ge 0 $$
这个例子清晰地说明了，像因果律这样的基本原理如何为构建物理上合理的理论模型提供强有力的指导和约束。

### 超越均匀模型：晶体中的[局域场效应](@entry_id:141628)

到目前为止，我们主要讨论的是均匀介质模型。然而，真实的晶体材料在原子尺度上是周期性非均匀的。这种非均匀性导致了一个重要而复杂的现象——**[局域场效应](@entry_id:141628) (local field effects)**。其核心思想是，作用在某个特定原子上的**[局域电场](@entry_id:194304)** $\vec{E}_{\text{loc}}$ 与材料中的**宏观平均[电场](@entry_id:194326)** $\vec{E}_{\text{mac}}$ 并不同。局域场还包括了由周围其他被极化的原子所产生的附加[电场](@entry_id:194326)。[@problem_id:2991605]

在周期性体系中，响应函数严格来说是一个矩阵，即**[介电矩阵](@entry_id:144203)** $\epsilon_{\mathbf{G}, \mathbf{G}'}(\mathbf{q}, \omega)$，其中 $\mathbf{G}$ 和 $\mathbf{G}'$ 是[倒易晶格矢量](@entry_id:263351)。这个矩阵的非对角元 ($\mathbf{G} \neq \mathbf{G}'$) 正是[局域场效应](@entry_id:141628)的数学体现，它们耦合了宏观场分量 ($\mathbf{G}=\mathbf{0}$) 和微观场分量 ($\mathbf{G} \neq \mathbf{0}$)。[@problem_id:2991605]

实验上测量的宏观[介电函数](@entry_id:136859) $\epsilon_{\text{M}}(\omega)$ 实际上是从这个复杂的[介电矩阵](@entry_id:144203)中提取出来的。根据 Adler-Wiser 公式，它由[介电矩阵](@entry_id:144203)的逆的“头部”（即 $(\mathbf{0},\mathbf{0})$ 元）给出：
$$ \epsilon_{\text{M}}(\omega) = \left[\epsilon^{-1}_{\mathbf{0}, \mathbf{0}}(\mathbf{q} \to \mathbf{0}, \omega)\right]^{-1} $$
这表明，宏观[介电常数](@entry_id:146714)并不仅仅是微观[介电响应](@entry_id:140146)的简单[空间平均](@entry_id:203499)。

对于具有立方对称性的绝缘体，一个经典的近似模型是 Lorentz [局域场](@entry_id:146504)模型。它给出了宏观[介电常数](@entry_id:146714) $\epsilon_{\text{M}}$ 和单个原子的微观极化率 $\alpha$ 之间的关系，即**Clausius-Mossotti 关系**：
$$ \frac{\epsilon_{\text{M}}(\omega) - 1}{\epsilon_{\text{M}}(\omega) + 2} = \frac{n \alpha(\omega)}{3 \epsilon_0} $$
其中 $n$ 是[原子数](@entry_id:746561)密度。这个关系式明确地包含了[局域场修正](@entry_id:143541)（体现为分母中的 "+2" 项），它深刻地影响着对材料介电性质的理解。

在现代[第一性原理计算](@entry_id:198754)（如基于[含时密度泛函理论](@entry_id:200019) TDDFT）中，[局域场效应](@entry_id:141628)的来源更加丰富，它不仅包括由晶体周期性[波函数](@entry_id:147440)导致的“晶体[局域场效应](@entry_id:141628)”，还包括电子之间的多体交换关联相互作用带来的修正。精确地描述这些效应是准确预测和理解材料光学性质的前沿课题。