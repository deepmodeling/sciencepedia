## 引言
当材料进入超导态时，其电子系统会经历一场深刻的[量子相变](@entry_id:146027)，形成由库珀对构成的宏观相干[基态](@entry_id:150928)。一个自然而然的问题随之而来：这个新[基态](@entry_id:150928)的基本激发是什么？与正常金属中通过产生电子-空穴对来激发系统不同，[超导体](@entry_id:191025)中的最低能激发涉及打断库珀对，从而催生出一种全新的实体——[准粒子](@entry_id:136584)。理解这些[准粒子](@entry_id:136584)的性质是揭开[超导现象](@entry_id:142943)神秘面纱的钥匙，从经典的[迈斯纳效应](@entry_id:273600)到前沿的拓扑量子计算，其影响无处不在。

本文旨在系统性地构建超导[准粒子](@entry_id:136584)的物理图像，填补从单电[子图](@entry_id:273342)像到多体凝聚态激发的认知鸿沟。我们将带领读者深入探索[准粒子](@entry_id:136584)的理论、实验和应用，内容涵盖以下三个核心部分：

首先，在 **“原理与机制”** 一章中，我们将奠定理论基础。通过引入关键的玻戈留波夫变换，我们将从BCS[哈密顿量](@entry_id:172864)出发，推导出[准粒子](@entry_id:136584)的色散关系，揭示超导[能隙的起源](@entry_id:187265)。此外，我们还将探讨[准粒子](@entry_id:136584)的[电荷](@entry_id:275494)、速度等物理属性，并介绍处理非均匀和强耦合体系的[格林函数](@entry_id:147802)及BdG方程等高级方法。

接着，在 **“应用与跨学科交叉”** 一章中，我们将理论与实践相结合。我们将展示如何通过[隧道谱学](@entry_id:139081)、[热容](@entry_id:137594)测量等实验手段直接观测[准粒子](@entry_id:136584)谱，并探讨它们在[安德烈夫反射](@entry_id:146699)、[约瑟夫森效应](@entry_id:141683)等介观物理现象中的关键作用。本章还将触及物理学前沿，讨论[准粒子](@entry_id:136584)在[d波超导体](@entry_id:139318)和拓扑超导中的奇异行为，例如马约拉纳费米子的形成。

最后，**“动手实践”** 部分将提供一系列精心设计的问题，旨在通过实际计算加深读者对[准粒子](@entry_id:136584)概念的理解，例如[对角化](@entry_id:147016)BCS[哈密顿量](@entry_id:172864)、求解YSR束缚态以及计算比热跳变等，从而将理论知识转化为解决问题的能力。

## 原理与机制

在超导态中，[费米子](@entry_id:146235)系统经历了一次深刻的重构。电子不再是独立的实体，而是两两配对形成[库珀对](@entry_id:143370)，并凝聚成一个宏观的量子基态。因此，系统的低能激发不再是向[费米海](@entry_id:136725)之上添加单个电子或从中取走一个电子（即产生一个空穴）。相反，最基本的激发过程是打断一个库珀对，这必然同时涉及到[电子和空穴](@entry_id:274534)的自由度。这种新的激发模式被称为 **玻戈留波夫[准粒子](@entry_id:136584)** (Bogoliubov quasiparticle)，它是超导物理学的核心概念。本章将系统地阐述这些[准粒子](@entry_id:136584)的基本原理和内在机制。

### 玻戈留波夫变换与[准粒子](@entry_id:136584)代数

为了精确描述超导态中的激发，我们从 Bardeen-Cooper-Schrieffer (BCS) 理论的[平均场哈密顿量](@entry_id:751814)出发。对于一个自旋单态配对的系统，该[哈密顿量](@entry_id:172864)可以写为：
$$
H_{\mathrm{MF}} = \sum_{\mathbf{k},\sigma} \xi_{\mathbf{k}} c_{\mathbf{k}\sigma}^{\dagger} c_{\mathbf{k}\sigma} + \sum_{\mathbf{k}} \left( \Delta_{\mathbf{k}} c_{\mathbf{k}\uparrow}^{\dagger} c_{-\mathbf{k}\downarrow}^{\dagger} + \Delta_{\mathbf{k}}^{*} c_{-\mathbf{k}\downarrow} c_{\mathbf{k}\uparrow} \right)
$$
其中 $c_{\mathbf{k}\sigma}^{\dagger}$ 和 $c_{\mathbf{k}\sigma}$ 分别是动量为 $\mathbf{k}$、自旋为 $\sigma$ 的电子的产生和[湮灭算符](@entry_id:165390)。$\xi_{\mathbf{k}} = \varepsilon_{\mathbf{k}} - \mu$ 是相对于化学势 $\mu$ 的单电子能量。$\Delta_{\mathbf{k}}$ 是超导[序参量](@entry_id:144819)或[能隙](@entry_id:191975)函数，它源于非零的电子对反常平均值 $\langle c_{-\mathbf{k}\downarrow} c_{\mathbf{k}\uparrow} \rangle$。

这个[哈密顿量](@entry_id:172864)不是对角的，因为它包含了 $c^{\dagger}c^{\dagger}$ 和 $cc$ 这样的项，这些项不保持粒子数守恒。这反映了超导[基态](@entry_id:150928)是不同[粒子数态](@entry_id:155105)的相干叠加。为了找到系统的本征激发，我们需要对[哈密顿量](@entry_id:172864)进行对角化。这一任务通过 **玻戈留波夫变换** (Bogoliubov transformation) 来完成。该变换定义了一组新的[费米子算符](@entry_id:149120) $\gamma$，它们是原有[电子和空穴](@entry_id:274534)算符的[线性组合](@entry_id:154743)。对于自旋单态配对，这个变换的形式如下 [@problem_id:3012925]：
$$
\gamma_{\mathbf{k}\uparrow} = u_{\mathbf{k}} c_{\mathbf{k}\uparrow} - v_{\mathbf{k}} c_{-\mathbf{k}\downarrow}^{\dagger}
$$
$$
\gamma_{-\mathbf{k}\downarrow}^{\dagger} = u_{\mathbf{k}}^{*} c_{-\mathbf{k}\downarrow}^{\dagger} + v_{\mathbf{k}}^{*} c_{\mathbf{k}\uparrow}
$$
这里的 $\gamma_{\mathbf{k}\uparrow}$ 和 $\gamma_{-\mathbf{k}\downarrow}^{\dagger}$ 所对应的激发就是玻戈留波夫[准粒子](@entry_id:136584)。$u_{\mathbf{k}}$ 和 $v_{\mathbf{k}}$ 是复数系数，被称为 **[相干因子](@entry_id:147178)** (coherence factors)，它们的具体形式将通过对角化[哈密顿量](@entry_id:172864)的要求来确定。从这个定义可以直观地看到，一个[准粒子](@entry_id:136584)既有电子的成分（由 $c$ 算符代表），也有空穴的成分（由 $c^{\dagger}$ 算符代表）。

为了使这些新的[准粒子](@entry_id:136584)成为良定义的[费米子](@entry_id:146235)，它们的算符必须满足标准的[费米子](@entry_id:146235)[反对易关系](@entry_id:153815)：$\{\gamma_{\alpha}, \gamma_{\beta}^{\dagger}\} = \delta_{\alpha\beta}$ 以及 $\{\gamma_{\alpha}, \gamma_{\beta}\} = \{\gamma_{\alpha}^{\dagger}, \gamma_{\beta}^{\dagger}\} = 0$。通过将上述变换代入并利用电子算符的[反对易关系](@entry_id:153815)，我们可以直接进行验证 [@problem_id:3012925]。例如，计算 $\{\gamma_{\mathbf{k}\uparrow}, \gamma_{\mathbf{k}\uparrow}^{\dagger}\}$：
$$
\begin{align}
\{\gamma_{\mathbf{k}\uparrow}, \gamma_{\mathbf{k}\uparrow}^{\dagger}\}  = \{u_{\mathbf{k}} c_{\mathbf{k}\uparrow} - v_{\mathbf{k}} c_{-\mathbf{k}\downarrow}^{\dagger}, u_{\mathbf{k}}^{*} c_{\mathbf{k}\uparrow}^{\dagger} - v_{\mathbf{k}}^{*} c_{-\mathbf{k}\downarrow}\} \\
 = |u_{\mathbf{k}}|^2 \{c_{\mathbf{k}\uparrow}, c_{\mathbf{k}\uparrow}^{\dagger}\} + |v_{\mathbf{k}}|^2 \{c_{-\mathbf{k}\downarrow}^{\dagger}, c_{-\mathbf{k}\downarrow}\} \\
 = |u_{\mathbf{k}}|^2 \cdot 1 + |v_{\mathbf{k}}|^2 \cdot 1
\end{align}
$$
为了使这个[反对易子](@entry_id:139754)等于 $1$，我们必须要求[相干因子](@entry_id:147178)满足[归一化条件](@entry_id:156486)：
$$
|u_{\mathbf{k}}|^2 + |v_{\mathbf{k}}|^2 = 1
$$
进一步的计算表明，只要满足这个条件，所有其他的[反对易关系](@entry_id:153815)也都能正确满足。这个条件至关重要，它保证了从电子到[准粒子](@entry_id:136584)的变换是幺正的，保持了系统的[费米子](@entry_id:146235)特性。这可以被看作是在粒子-空穴空间中的一次旋转。

### [准粒子](@entry_id:136584)能谱：[能隙](@entry_id:191975)与[色散](@entry_id:263750)

有了玻戈留波夫变换，我们现在可以确定[准粒子](@entry_id:136584)的能量。这等价于找到[相干因子](@entry_id:147178) $u_{\mathbf{k}}$ 和 $v_{\mathbf{k}}$ 的具体形式，使得 $H_{\mathrm{MF}}$ 在新的[准粒子](@entry_id:136584)基底下是对角的，即 $H_{\mathrm{MF}} = E_0 + \sum_{\mathbf{k}\sigma} E_{\mathbf{k}} \gamma_{\mathbf{k}\sigma}^{\dagger} \gamma_{\mathbf{k}\sigma}$。

处理这个问题的一个更优雅的工具是 **南部-戈尔科夫** (Nambu-Gor'kov) 形式。我们定义一个两分量的 **[南部旋量](@entry_id:145326)** (Nambu spinor) [@problem_id:3012944]：
$$
\Psi_{\mathbf{k}} = \begin{pmatrix} c_{\mathbf{k}\uparrow} \\ c_{-\mathbf{k}\downarrow}^{\dagger} \end{pmatrix}
$$
利用这个旋量，BCS [哈密顿量](@entry_id:172864)可以被重写成一个紧凑的矩阵形式（忽略一个常数项）：
$$
H_{\mathrm{MF}} = \frac{1}{2} \sum_{\mathbf{k}} \Psi_{\mathbf{k}}^{\dagger} \mathcal{H}_{\mathbf{k}} \Psi_{\mathbf{k}}
$$
其中 $\mathcal{H}_{\mathbf{k}}$ 是一个 $2 \times 2$ 的矩阵，被称为 **玻戈留波夫-德热纳** (Bogoliubov-de Gennes, BdG) [哈密顿量](@entry_id:172864) [@problem_id:3012917]：
$$
\mathcal{H}_{\mathbf{k}} = \begin{pmatrix} \xi_{\mathbf{k}} & \Delta_{\mathbf{k}} \\ \Delta_{\mathbf{k}}^{*} & -\xi_{\mathbf{k}} \end{pmatrix}
$$
这个矩阵清晰地展示了超导态的本质：对角线上的 $\xi_{\mathbf{k}}$ 和 $-\xi_{\mathbf{k}}$ 分别代表[电子和空穴](@entry_id:274534)的能量，而非对角线上的[能隙](@entry_id:191975)函数 $\Delta_{\mathbf{k}}$ 则耦合了电子和空穴。正是这种 **粒子-空穴混合** (particle-hole mixing) 导致了[准粒子](@entry_id:136584)的形成。

[准粒子](@entry_id:136584)的能量 $E_{\mathbf{k}}$ 就是 BdG [哈密顿量](@entry_id:172864) $\mathcal{H}_{\mathbf{k}}$ 的[本征值](@entry_id:154894)。通过求解本征方程 $\det(\mathcal{H}_{\mathbf{k}} - E_{\mathbf{k}}I) = 0$，我们得到：
$$
(\xi_{\mathbf{k}} - E_{\mathbf{k}})(-\xi_{\mathbf{k}} - E_{\mathbf{k}}) - |\Delta_{\mathbf{k}}|^2 = 0
$$
解得 $E_{\mathbf{k}}^2 = \xi_{\mathbf{k}}^2 + |\Delta_{\mathbf{k}}|^2$。取正的能量解，我们得到了著名的[准粒子色散](@entry_id:161746)关系：
$$
E_{\mathbf{k}} = \sqrt{\xi_{\mathbf{k}}^2 + |\Delta_{\mathbf{k}}|^2}
$$
这个结果是超导理论的基石之一 [@problem_id:3012917]。与正常态的[激发能](@entry_id:190368) $|\xi_{\mathbf{k}}|$ 不同，[准粒子](@entry_id:136584)能谱在[费米面](@entry_id:137798)上（$\xi_{\mathbf{k}}=0$）打开了一个宽度为 $2|\Delta_{\mathbf{k}}|$ 的 **[超导能隙](@entry_id:145058)**。激发一个[准粒子](@entry_id:136584)所需的最小能量是 $|\Delta_{\mathbf{k}}|$。在[能隙](@entry_id:191975)之内，不存在任何单粒子[激发态](@entry_id:261453)，这正是[超导体](@entry_id:191025)许多独特性质（如无耗散电流）的根源。

BdG [哈密顿量](@entry_id:172864)的[本征向量](@entry_id:151813) $(u_{\mathbf{k}}, v_{\mathbf{k}})^{\mathrm{T}}$ 则给出了[相干因子](@entry_id:147178)的具体形式。求解本征方程可以得到：
$$
|u_{\mathbf{k}}|^2 = \frac{1}{2} \left( 1 + \frac{\xi_{\mathbf{k}}}{E_{\mathbf{k}}} \right), \quad |v_{\mathbf{k}}|^2 = \frac{1}{2} \left( 1 - \frac{\xi_{\mathbf{k}}}{E_{\mathbf{k}}} \right)
$$
这些表达式揭示了[准粒子](@entry_id:136584)的深刻物理内涵。当电子态远离[费米面](@entry_id:137798)，处于高能级时（$\xi_{\mathbf{k}} \gg |\Delta_{\mathbf{k}}|$），$E_{\mathbf{k}} \approx \xi_{\mathbf{k}}$，此时 $|u_{\mathbf{k}}|^2 \to 1$，$|v_{\mathbf{k}}|^2 \to 0$。这意味着[准粒子](@entry_id:136584)几乎完全是电子。相反，当电子态处于费米面下方很深处时（$\xi_{\mathbf{k}} \ll -|\Delta_{\mathbf{k}}|$），$E_{\mathbf{k}} \approx -\xi_{\mathbf{k}} = |\xi_{\mathbf{k}}|$，此时 $|u_{\mathbf{k}}|^2 \to 0$，$|v_{\mathbf{k}}|^2 \to 1$。这意味着[准粒子](@entry_id:136584)几乎完全是空穴。而在费米面附近（$\xi_{\mathbf{k}} \approx 0$），$|u_{\mathbf{k}}|^2 \approx |v_{\mathbf{k}}|^2 \approx 1/2$，[准粒子](@entry_id:136584)是电子和空穴的等权重叠加。

对于各向异性的[超导体](@entry_id:191025)，[能隙](@entry_id:191975)函数 $\Delta_{\mathbf{k}}$ 依赖于动量方向。在某些方向上，[能隙](@entry_id:191975)可能为零，即存在 **[能隙节点](@entry_id:144519)**。在这些节点方向上，$\Delta_{\mathbf{k}}=0$，[准粒子](@entry_id:136584)能谱退化为 $E_{\mathbf{k}} = |\xi_{\mathbf{k}}|$，系统表现出[无能](@entry_id:201612)隙的行为 [@problem_id:3012917]。这在[非常规超导体](@entry_id:141195)中是常见的。

### 玻戈留波夫[准粒子](@entry_id:136584)的物理性质

理解了[准粒子](@entry_id:136584)的[代数结构](@entry_id:137052)和能量[色散](@entry_id:263750)后，我们可以进一步探究它们的物理性质，如[电荷](@entry_id:275494)和速度。

#### 有效电荷

一个[准粒子](@entry_id:136584)是[电子和空穴](@entry_id:274534)的叠加，那么它携带的有效电荷是多少？我们可以通过计算创建一个[准粒子](@entry_id:136584)后系统总[电荷](@entry_id:275494)数的变化来定义其 **有效电荷** $q_{\mathbf{k}}$。这个变化等于电子部分贡献的[电荷](@entry_id:275494)（$-e|u_{\mathbf{k}}|^2$）和空穴部分贡献的[电荷](@entry_id:275494)（$+e|v_{\mathbf{k}}|^2$）之和。更严格地，通过计算单[准粒子](@entry_id:136584)态 $|1_{\mathbf{k}}\rangle = \gamma_{\mathbf{k}\uparrow}^{\dagger}|\text{BCS}\rangle$ 与[BCS基态](@entry_id:136275) $|\text{BCS}\rangle$ 之间总[电荷](@entry_id:275494)算符 $\hat{Q}$ 的[期望值](@entry_id:153208)之差得到 [@problem_id:3012913]：
$$
q_{\mathbf{k}} = \langle 1_{\mathbf{k}}|\hat{Q}|1_{\mathbf{k}}\rangle - \langle \text{BCS}|\hat{Q}|\text{BCS}\rangle = -e(|u_{\mathbf{k}}|^2 - |v_{\mathbf{k}}|^2)
$$
将[相干因子](@entry_id:147178)的表达式代入，我们得到一个简洁而深刻的结果：
$$
q_{\mathbf{k}} = -e \frac{\xi_{\mathbf{k}}}{E_{\mathbf{k}}} = -e \frac{\xi_{\mathbf{k}}}{\sqrt{\xi_{\mathbf{k}}^2 + |\Delta_{\mathbf{k}}|^2}}
$$
这个结果表明：
- 在费米面上 ($\xi_{\mathbf{k}}=0$)，[准粒子](@entry_id:136584)的[有效电荷](@entry_id:748807) $q_{\mathbf{k}}=0$。这意味着处于[能隙](@entry_id:191975)边缘的最低能激发是电中性的。
- 远离[费米面](@entry_id:137798)时，若 $\xi_{\mathbf{k}} > 0$，则 $q_{\mathbf{k}} \to -e$，[准粒子](@entry_id:136584)表现为电子；若 $\xi_{\mathbf{k}} < 0$，则 $q_{\mathbf{k}} \to +e$，[准粒子](@entry_id:136584)表现为空穴。

在低温下 ($k_B T \ll \Delta$)，[热激发](@entry_id:275697)的[准粒子](@entry_id:136584)主要集中在[能隙](@entry_id:191975)边缘，即 $\xi_{\mathbf{k}} \approx 0$。因此，这些[准粒子](@entry_id:136584)几乎不携带[电荷](@entry_id:275494)，对[电导](@entry_id:177131)的贡献很小。然而，它们携带能量 $E_{\mathbf{k}} \approx \Delta$，可以有效地传导热量。这就解释了[超导体](@entry_id:191025)中一个著名的现象：在低温极限下，[热导](@entry_id:189019)和[电导](@entry_id:177131)的输运机制发生分离，维德曼-弗朗茨定律失效 [@problem_id:3012913]。

#### [群速度](@entry_id:147686)

[准粒子](@entry_id:136584)的[传播速度](@entry_id:189384)由其群速度 $v_g(\mathbf{k}) = \frac{1}{\hbar} \nabla_{\mathbf{k}} E_{\mathbf{k}}$ 决定。利用链式法则和在[费米面](@entry_id:137798)附近的线性[色散](@entry_id:263750)近似 $\xi_{\mathbf{k}} \approx \hbar v_F(k-k_F)$，我们可以推导出 [@problem_id:3012911]：
$$
v_g(\mathbf{k}) = \frac{1}{\hbar} \frac{\partial E_{\mathbf{k}}}{\partial \xi_{\mathbf{k}}} \nabla_{\mathbf{k}} \xi_{\mathbf{k}} = \frac{\xi_{\mathbf{k}}}{E_{\mathbf{k}}} \frac{1}{\hbar} \nabla_{\mathbf{k}} \xi_{\mathbf{k}} \approx \mathbf{v}_F \frac{\xi_{\mathbf{k}}}{E_{\mathbf{k}}}
$$
其中 $\mathbf{v}_F$ 是正常态的费米速度。这个表达式告诉我们：
- 在[能隙](@entry_id:191975)边缘 ($\xi_{\mathbf{k}}=0$)，$v_g = 0$。这与色散关系 $E_{\mathbf{k}}$ 在此处有极小值（斜率为零）的图像一致。
- 远离[能隙](@entry_id:191975)时 ($|\xi_{\mathbf{k}}| \gg \Delta$)，$|v_g| \to |\mathbf{v}_F|$，[准粒子](@entry_id:136584)的速度恢复到正常态电子的费米速度。

群速度在[能隙](@entry_id:191975)边缘的消失，意味着这些低能[准粒子](@entry_id:136584)是“重”或“慢”的，这深刻地影响了[超导体](@entry_id:191025)的动力学和响应特性。

#### 库珀对的关联长度

[准粒子](@entry_id:136584)是超导[基态](@entry_id:150928)的激发，而[基态](@entry_id:150928)本身是由大量交叠的[库珀对](@entry_id:143370)构成的。一个[库珀对](@entry_id:143370)在动量空间中的[波函数](@entry_id:147440)由反常平均值 $\Phi(\mathbf{k}) = \langle c_{-\mathbf{k}\downarrow}c_{\mathbf{k}\uparrow}\rangle = u_{\mathbf{k}}^{*}v_{\mathbf{k}} = \frac{\Delta_{\mathbf{k}}}{2E_{\mathbf{k}}}$ 描述 [@problem_id:3012886]。在弱耦合的[BCS理论](@entry_id:144185)中，$\Delta \ll E_F$，这个函数只在费米面附近一个很窄的动量壳层内有显著数值，其宽度 $\delta k \sim \Delta / (\hbar v_F)$。根据[不确定性原理](@entry_id:141278)，动量空间中的窄[分布](@entry_id:182848)对应于实空间中的宽[分布](@entry_id:182848)。这定义了[库珀对](@entry_id:143370)的尺寸，即 **[相干长度](@entry_id:139128)** $\xi_0$：
$$
\xi_0 \sim \frac{1}{\delta k} \sim \frac{\hbar v_F}{\Delta}
$$
在BCS极限下，由于 $\Delta \ll E_F \sim \hbar v_F k_F$，我们有 $\xi_0 \gg k_F^{-1}$，其中 $k_F^{-1}$ 是电子的平均间距。这意味着BCS库珀对是非常大的、松散束缚的扩展物体，每个[库珀对](@entry_id:143370)的空间范围内都包含了大量其他库珀对的中心，它们是高度重叠的 [@problem_id:3012886]。这与由[强相互作用](@entry_id:159198)形成的、尺寸小于粒子间距的[紧束缚](@entry_id:142573)分子（Bose-Einstein凝聚极限）形成鲜明对比。

### 超出平均场理论：形式与前沿

BCS平均场理论为我们提供了[准粒子](@entry_id:136584)的[基本图](@entry_id:160617)像。然而，更精确的描述和对更复杂现象的研究需要更强大的理论工具。

#### [格林函数](@entry_id:147802)与[实空间](@entry_id:754128)方法

**[南部-戈尔科夫格林函数](@entry_id:145547)** 形式是研究[超导体](@entry_id:191025)的标准场论工具。它将正常和反常[传播子](@entry_id:139558)统一在一个 $2 \times 2$ 矩阵中。在[松原频率](@entry_id:197724)表象下，该[格林函数](@entry_id:147802) $\mathcal{G}(\mathbf{k}, i\omega_n)$ 可以通过对 BdG [哈密顿量](@entry_id:172864)求逆得到 [@problem_id:3012944]：
$$
\mathcal{G}(\mathbf{k},i\omega_{n}) = (i\omega_n I - \mathcal{H}_{\mathbf{k}})^{-1} = \frac{1}{(i\omega_{n})^{2}-E_{\mathbf{k}}^{2}}
\begin{pmatrix}
i\omega_{n}+\xi_{\mathbf{k}} & \Delta_{\mathbf{k}} \\
\Delta_{\mathbf{k}}^{*} & i\omega_{n}-\xi_{\mathbf{k}}
\end{pmatrix}
$$
这个格林函数包含了系统的全部谱信息，是计算各种物理响应函数（如[电导率](@entry_id:137481)、[核磁共振弛豫](@entry_id:178526)率等）的出发点。

对于非均匀系统，如存在[磁通](@entry_id:191239)涡旋或界面的情况，动量不再是[好量子数](@entry_id:262514)。此时，我们需要在实空间求解 **玻戈留波夫-德热纳 (BdG) 方程**。这是一个薛定谔方程的矩阵形式 [@problem_id:3012936]：
$$
\begin{pmatrix}
H_0-\mu & \Delta(\mathbf{r}) \\
\Delta^*(\mathbf{r}) & -(H_0^*-\mu)
\end{pmatrix}
\begin{pmatrix}
u_n(\mathbf{r}) \\
v_n(\mathbf{r})
\end{pmatrix}
=
E_n
\begin{pmatrix}
u_n(\mathbf{r}) \\
v_n(\mathbf{r})
\end{pmatrix}
$$
其中 $H_0 = \frac{1}{2m}(-i\hbar\nabla - e\mathbf{A})^2+V(\mathbf{r})$ 是单[电子哈密顿量](@entry_id:177588)，$\Delta(\mathbf{r})$ 是空间依赖的[序参量](@entry_id:144819)。本征函数 $(u_n(\mathbf{r}), v_n(\mathbf{r}))^{\mathrm{T}}$ 描述了第 $n$ 个[准粒子](@entry_id:136584)态的粒子和空穴分量的空间[波函数](@entry_id:147440)，并满足[归一化条件](@entry_id:156486) $\int d^3r (|u_n(\mathbf{r})|^2 + |v_n(\mathbf{r})|^2) = 1$。BdG方程是研究超导纳米结构、[安德烈夫反射](@entry_id:146699)和马约拉纳束缚态等现象的核心工具。

#### [准粒子寿命](@entry_id:145453)与强耦合效应

在真实的材料中，[准粒子](@entry_id:136584)会与其他激发（如[声子](@entry_id:140728)、其他[准粒子](@entry_id:136584)或磁涨落）发生非弹性散射，从而获得有限的 **寿命**。这在[格林函数](@entry_id:147802)形式中表现为[准粒子](@entry_id:136584)具有了复数能量，其虚部代表衰减率。这个衰减来源于 **[自能](@entry_id:145608)** (self-energy) $\Sigma$ 的虚部。对于一个能量为 $E$ 的[准粒子](@entry_id:136584)，其寿命 $\tau(E)$ 与自能的关系可以近似为 [@problem_id:3012895]：
$$
\tau^{-1}(E) = -\frac{Z(E)}{\hbar} \operatorname{Im} \Sigma^{R}(\mathbf{k}, E)
$$
其中 $\Sigma^{R}$ 是推迟自能，而 $Z(E) = [1 - \partial_{\omega}\operatorname{Re}\Sigma^{R}]^{-1}$ 是[准粒子权重](@entry_id:140100)或[质量重整化](@entry_id:139777)因子。

对于由电-[声子](@entry_id:140728)相互作用主导的[常规超导体](@entry_id:275247)，**Eliashberg 理论** 提供了超越BCS的强耦合描述。在该理论中，[能隙](@entry_id:191975) $\Delta$ 和重整化因子 $Z$ 本身都成为能量（频率）的函数，并由一组自洽的[积分方程](@entry_id:138643)决定 [@problem_id:3012873]。这些 **Eliashberg 方程** 的核心是 **Eliashberg 谱函数** $\alpha^2F(\Omega)$，它精确地量化了在不同频率 $\Omega$ 的[声子](@entry_id:140728)对电子配对的贡献强度。Eliashberg 理论成功地解释了许多[强耦合超导体](@entry_id:140567)（如铅和铌）的实验现象，是现代超导理论的重要组成部分。

#### 拓扑超导与马约拉纳费米子

近年来，[准粒子激发](@entry_id:138475)的概念在一个激动人心的新领域——**拓扑超导**——中扮演了核心角色。在特定的[超导体](@entry_id:191025)系中（例如，手性[p波超导体](@entry_id:141724)），[BdG哈密顿量](@entry_id:145387)具有特殊的对称性，允许在系统的边界或拓扑缺陷（如磁通涡旋）中存在能量严格为零的束缚态。

根据 [Altland-Zirnbauer 分类](@entry_id:138394)，一类重要的[拓扑超导体](@entry_id:146785)属于对称性类别 D，它具有[粒子-空穴对称性](@entry_id:142469) (PHS) 但没有时间反演对称性。PHS算符 $\Xi$ 满足 $\Xi \mathcal{H}_{\mathrm{BdG}} \Xi^{-1} = -\mathcal{H}_{\mathrm{BdG}}$ 和 $\Xi^2=+1$ [@problem_id:3012897]。这个对称性保证了如果 $E$ 是一个本征能量，那么 $-E$ 也是。因此，零能态 $E=0$ 在粒子-空穴谱中占据了一个特殊的位置。

对于一个孤立的零能本征态 $\Phi = (u, v)^{\mathrm{T}}$，由于 $\Xi^2=+1$，我们可以选择一个合适的相位使得该态是 PHS 的本征态，即 $\Xi \Phi = \Phi$。在自旋无相互作用的情况下，$\Xi$ 的作用是 $\Xi (u,v)^{\mathrm{T}} = (v^*, u^*)^{\mathrm{T}}$，因此该条件转化为对[波函数](@entry_id:147440)分量的约束：$v(\mathbf{r}) = u^*(\mathbf{r})$。

现在考虑与这个零能态相对应的[准粒子](@entry_id:136584)算符 $\gamma = \int d^2r [u^*(\mathbf{r})\psi(\mathbf{r}) + v^*(\mathbf{r})\psi^{\dagger}(\mathbf{r})]$。它的[厄米共轭](@entry_id:191215)是 $\gamma^{\dagger} = \int d^2r [u(\mathbf{r})\psi^{\dagger}(\mathbf{r}) + v(\mathbf{r})\psi(\mathbf{r})]$。将约束条件 $v=u^*$ 代入，我们发现：
$$
\gamma = \gamma^{\dagger}
$$
这个算符等于其自身的[厄米共轭](@entry_id:191215)！这种粒子就是它自身的反粒子的[费米子](@entry_id:146235)，被称为 **[马约拉纳费米子](@entry_id:137199)** (Majorana fermion)。在凝聚态物理中，一个马约拉纳[零能模](@entry_id:172472)对应一个非局域的、受拓扑保护的[量子比特](@entry_id:137928)，它对局域扰动免疫，具有潜在的[容错量子计算](@entry_id:142498)应用价值。[指标定理](@entry_id:637636)进一步指出，在一个陈数为 $C$ 的二维[p波超导体](@entry_id:141724)中，一个涡旋度为 $n_v$ 的磁通涡旋会束缚 $|n_v||C|$ 个马约拉纳[零能模](@entry_id:172472) [@problem_id:3012897]。寻找和操控这些奇异的[准粒子激发](@entry_id:138475)，是当前凝聚态物理学的最前沿之一。