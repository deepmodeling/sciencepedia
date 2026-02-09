## 引言
当材料进入超导态时，其电子系统会经历一场深刻的量子相变，形成由库珀对构成的宏观相干基态。一个自然而然的问题随之而来：这个新基态的基本激发是什么？与正常金属中通过产生电子-空穴对来激发系统不同，超导体中的最低能激发涉及打断库珀对，从而催生出一种全新的实体——准粒子。理解这些准粒子的性质是揭开超导现象神秘面纱的钥匙，从经典的迈斯纳效应到前沿的拓扑量子计算，其影响无处不在。

本文旨在系统性地构建超导准粒子的物理图像，填补从单电子图像到多体凝聚态激发的认知鸿沟。我们将带领读者深入探索准粒子的理论、实验和应用，内容涵盖以下三个核心部分：

首先，在 **“原理与机制”** 一章中，我们将奠定理论基础。通过引入关键的玻戈留波夫变换，我们将从BCS哈密顿量出发，推导出准粒子的色散关系，揭示超导能隙的起源。此外，我们还将探讨准粒子的电荷、速度等物理属性，并介绍处理非均匀和强耦合体系的格林函数及BdG方程等高级方法。

接着，在 **“应用与跨学科交叉”** 一章中，我们将理论与实践相结合。我们将展示如何通过隧道谱学、热容测量等实验手段直接观测准粒子谱，并探讨它们在安德烈夫反射、约瑟夫森效应等介观物理现象中的关键作用。本章还将触及物理学前沿，讨论准粒子在d波超导体和拓扑超导中的奇异行为，例如马约拉纳费米子的形成。

最后，**“动手实践”** 部分将提供一系列精心设计的问题，旨在通过实际计算加深读者对准粒子概念的理解，例如对角化BCS哈密顿量、求解YSR束缚态以及计算比热跳变等，从而将理论知识转化为解决问题的能力。

## 原理与机制

在超导态中，费米子系统经历了一次深刻的重构。电子不再是独立的实体，而是两两配对形成库珀对，并凝聚成一个宏观的量子基态。因此，系统的低能激发不再是向费米海之上添加单个电子或从中取走一个电子（即产生一个空穴）。相反，最基本的激发过程是打断一个库珀对，这必然同时涉及到电子和空穴的自由度。这种新的激发模式被称为 **玻戈留波夫准粒子** (Bogoliubov quasiparticle)，它是超导物理学的核心概念。本章将系统地阐述这些准粒子的基本原理和内在机制。

### 玻戈留波夫变换与准粒子代数

为了精确描述超导态中的激发，我们从 Bardeen-Cooper-Schrieffer (BCS) 理论的平均场哈密顿量出发。对于一个自旋单态配对的系统，该哈密顿量可以写为：
$$
H_{\mathrm{MF}} = \sum_{\mathbf{k},\sigma} \xi_{\mathbf{k}} c_{\mathbf{k}\sigma}^{\dagger} c_{\mathbf{k}\sigma} + \sum_{\mathbf{k}} \left( \Delta_{\mathbf{k}} c_{\mathbf{k}\uparrow}^{\dagger} c_{-\mathbf{k}\downarrow}^{\dagger} + \Delta_{\mathbf{k}}^{*} c_{-\mathbf{k}\downarrow} c_{\mathbf{k}\uparrow} \right)
$$
其中 $c_{\mathbf{k}\sigma}^{\dagger}$ 和 $c_{\mathbf{k}\sigma}$ 分别是动量为 $\mathbf{k}$、自旋为 $\sigma$ 的电子的产生和湮灭算符。$\xi_{\mathbf{k}} = \varepsilon_{\mathbf{k}} - \mu$ 是相对于化学势 $\mu$ 的单电子能量。$\Delta_{\mathbf{k}}$ 是超导序参量或能隙函数，它源于非零的电子对反常平均值 $\langle c_{-\mathbf{k}\downarrow} c_{\mathbf{k}\uparrow} \rangle$。

这个哈密顿量不是对角的，因为它包含了 $c^{\dagger}c^{\dagger}$ 和 $cc$ 这样的项，这些项不保持粒子数守恒。这反映了超导基态是不同粒子数态的相干叠加。为了找到系统的本征激发，我们需要对哈密顿量进行对角化。这一任务通过 **玻戈留波夫变换** (Bogoliubov transformation) 来完成。该变换定义了一组新的费米子算符 $\gamma$，它们是原有电子和空穴算符的线性组合。对于自旋单态配对，这个变换的形式如下 [@problem_id:3012925]：
$$
\gamma_{\mathbf{k}\uparrow} = u_{\mathbf{k}} c_{\mathbf{k}\uparrow} - v_{\mathbf{k}} c_{-\mathbf{k}\downarrow}^{\dagger}
$$
$$
\gamma_{-\mathbf{k}\downarrow}^{\dagger} = u_{\mathbf{k}}^{*} c_{-\mathbf{k}\downarrow}^{\dagger} + v_{\mathbf{k}}^{*} c_{\mathbf{k}\uparrow}
$$
这里的 $\gamma_{\mathbf{k}\uparrow}$ 和 $\gamma_{-\mathbf{k}\downarrow}^{\dagger}$ 所对应的激发就是玻戈留波夫准粒子。$u_{\mathbf{k}}$ 和 $v_{\mathbf{k}}$ 是复数系数，被称为 **相干因子** (coherence factors)，它们的具体形式将通过对角化哈密顿量的要求来确定。从这个定义可以直观地看到，一个准粒子既有电子的成分（由 $c$ 算符代表），也有空穴的成分（由 $c^{\dagger}$ 算符代表）。

为了使这些新的准粒子成为良定义的费米子，它们的算符必须满足标准的费米子反对易关系：$\{\gamma_{\alpha}, \gamma_{\beta}^{\dagger}\} = \delta_{\alpha\beta}$ 以及 $\{\gamma_{\alpha}, \gamma_{\beta}\} = \{\gamma_{\alpha}^{\dagger}, \gamma_{\beta}^{\dagger}\} = 0$。通过将上述变换代入并利用电子算符的反对易关系，我们可以直接进行验证 [@problem_id:3012925]。例如，计算 $\{\gamma_{\mathbf{k}\uparrow}, \gamma_{\mathbf{k}\uparrow}^{\dagger}\}$：
$$
\begin{align}
\{\gamma_{\mathbf{k}\uparrow}, \gamma_{\mathbf{k}\uparrow}^{\dagger}\}  = \{u_{\mathbf{k}} c_{\mathbf{k}\uparrow} - v_{\mathbf{k}} c_{-\mathbf{k}\downarrow}^{\dagger}, u_{\mathbf{k}}^{*} c_{\mathbf{k}\uparrow}^{\dagger} - v_{\mathbf{k}}^{*} c_{-\mathbf{k}\downarrow}\} \\
 = |u_{\mathbf{k}}|^2 \{c_{\mathbf{k}\uparrow}, c_{\mathbf{k}\uparrow}^{\dagger}\} + |v_{\mathbf{k}}|^2 \{c_{-\mathbf{k}\downarrow}^{\dagger}, c_{-\mathbf{k}\downarrow}\} \\
 = |u_{\mathbf{k}}|^2 \cdot 1 + |v_{\mathbf{k}}|^2 \cdot 1
\end{align}
$$
为了使这个反对易子等于 $1$，我们必须要求相干因子满足归一化条件：
$$
|u_{\mathbf{k}}|^2 + |v_{\mathbf{k}}|^2 = 1
$$
进一步的计算表明，只要满足这个条件，所有其他的反对易关系也都能正确满足。这个条件至关重要，它保证了从电子到准粒子的变换是幺正的，保持了系统的费米子特性。这可以被看作是在粒子-空穴空间中的一次旋转。

### 准粒子能谱：能隙与色散

有了玻戈留波夫变换，我们现在可以确定准粒子的能量。这等价于找到相干因子 $u_{\mathbf{k}}$ 和 $v_{\mathbf{k}}$ 的具体形式，使得 $H_{\mathrm{MF}}$ 在新的准粒子基底下是对角的，即 $H_{\mathrm{MF}} = E_0 + \sum_{\mathbf{k}\sigma} E_{\mathbf{k}} \gamma_{\mathbf{k}\sigma}^{\dagger} \gamma_{\mathbf{k}\sigma}$。

处理这个问题的一个更优雅的工具是 **南部-戈尔科夫** (Nambu-Gor'kov) 形式。我们定义一个两分量的 **南部旋量** (Nambu spinor) [@problem_id:3012944]：
$$
\Psi_{\mathbf{k}} = \begin{pmatrix} c_{\mathbf{k}\uparrow} \\ c_{-\mathbf{k}\downarrow}^{\dagger} \end{pmatrix}
$$
利用这个旋量，BCS 哈密顿量可以被重写成一个紧凑的矩阵形式（忽略一个常数项）：
$$
H_{\mathrm{MF}} = \frac{1}{2} \sum_{\mathbf{k}} \Psi_{\mathbf{k}}^{\dagger} \mathcal{H}_{\mathbf{k}} \Psi_{\mathbf{k}}
$$
其中 $\mathcal{H}_{\mathbf{k}}$ 是一个 $2 \times 2$ 的矩阵，被称为 **玻戈留波夫-德热纳** (Bogoliubov-de Gennes, BdG) 哈密顿量 [@problem_id:3012917]：
$$
\mathcal{H}_{\mathbf{k}} = \begin{pmatrix} \xi_{\mathbf{k}} & \Delta_{\mathbf{k}} \\ \Delta_{\mathbf{k}}^{*} & -\xi_{\mathbf{k}} \end{pmatrix}
$$
这个矩阵清晰地展示了超导态的本质：对角线上的 $\xi_{\mathbf{k}}$ 和 $-\xi_{\mathbf{k}}$ 分别代表电子和空穴的能量，而非对角线上的能隙函数 $\Delta_{\mathbf{k}}$ 则耦合了电子和空穴。正是这种 **粒子-空穴混合** (particle-hole mixing) 导致了准粒子的形成。

准粒子的能量 $E_{\mathbf{k}}$ 就是 BdG 哈密顿量 $\mathcal{H}_{\mathbf{k}}$ 的本征值。通过求解本征方程 $\det(\mathcal{H}_{\mathbf{k}} - E_{\mathbf{k}}I) = 0$，我们得到：
$$
(\xi_{\mathbf{k}} - E_{\mathbf{k}})(-\xi_{\mathbf{k}} - E_{\mathbf{k}}) - |\Delta_{\mathbf{k}}|^2 = 0
$$
解得 $E_{\mathbf{k}}^2 = \xi_{\mathbf{k}}^2 + |\Delta_{\mathbf{k}}|^2$。取正的能量解，我们得到了著名的准粒子色散关系：
$$
E_{\mathbf{k}} = \sqrt{\xi_{\mathbf{k}}^2 + |\Delta_{\mathbf{k}}|^2}
$$
这个结果是超导理论的基石之一 [@problem_id:3012917]。与正常态的激发能 $|\xi_{\mathbf{k}}|$ 不同，准粒子能谱在费米面上（$\xi_{\mathbf{k}}=0$）打开了一个宽度为 $2|\Delta_{\mathbf{k}}|$ 的 **超导能隙**。激发一个准粒子所需的最小能量是 $|\Delta_{\mathbf{k}}|$。在能隙之内，不存在任何单粒子激发态，这正是超导体许多独特性质（如无耗散电流）的根源。

BdG 哈密顿量的本征向量 $(u_{\mathbf{k}}, v_{\mathbf{k}})^{\mathrm{T}}$ 则给出了相干因子的具体形式。求解本征方程可以得到：
$$
|u_{\mathbf{k}}|^2 = \frac{1}{2} \left( 1 + \frac{\xi_{\mathbf{k}}}{E_{\mathbf{k}}} \right), \quad |v_{\mathbf{k}}|^2 = \frac{1}{2} \left( 1 - \frac{\xi_{\mathbf{k}}}{E_{\mathbf{k}}} \right)
$$
这些表达式揭示了准粒子的深刻物理内涵。当电子态远离费米面，处于高能级时（$\xi_{\mathbf{k}} \gg |\Delta_{\mathbf{k}}|$），$E_{\mathbf{k}} \approx \xi_{\mathbf{k}}$，此时 $|u_{\mathbf{k}}|^2 \to 1$，$|v_{\mathbf{k}}|^2 \to 0$。这意味着准粒子几乎完全是电子。相反，当电子态处于费米面下方很深处时（$\xi_{\mathbf{k}} \ll -|\Delta_{\mathbf{k}}|$），$E_{\mathbf{k}} \approx -\xi_{\mathbf{k}} = |\xi_{\mathbf{k}}|$，此时 $|u_{\mathbf{k}}|^2 \to 0$，$|v_{\mathbf{k}}|^2 \to 1$。这意味着准粒子几乎完全是空穴。而在费米面附近（$\xi_{\mathbf{k}} \approx 0$），$|u_{\mathbf{k}}|^2 \approx |v_{\mathbf{k}}|^2 \approx 1/2$，准粒子是电子和空穴的等权重叠加。

对于各向异性的超导体，能隙函数 $\Delta_{\mathbf{k}}$ 依赖于动量方向。在某些方向上，能隙可能为零，即存在 **能隙节点**。在这些节点方向上，$\Delta_{\mathbf{k}}=0$，准粒子能谱退化为 $E_{\mathbf{k}} = |\xi_{\mathbf{k}}|$，系统表现出无能隙的行为 [@problem_id:3012917]。这在非常规超导体中是常见的。

### 玻戈留波夫准粒子的物理性质

理解了准粒子的代数结构和能量色散后，我们可以进一步探究它们的物理性质，如电荷和速度。

#### 有效电荷

一个准粒子是电子和空穴的叠加，那么它携带的有效电荷是多少？我们可以通过计算创建一个准粒子后系统总电荷数的变化来定义其 **有效电荷** $q_{\mathbf{k}}$。这个变化等于电子部分贡献的电荷（$-e|u_{\mathbf{k}}|^2$）和空穴部分贡献的电荷（$+e|v_{\mathbf{k}}|^2$）之和。更严格地，通过计算单准粒子态 $|1_{\mathbf{k}}\rangle = \gamma_{\mathbf{k}\uparrow}^{\dagger}|\text{BCS}\rangle$ 与BCS基态 $|\text{BCS}\rangle$ 之间总电荷算符 $\hat{Q}$ 的期望值之差得到 [@problem_id:3012913]：
$$
q_{\mathbf{k}} = \langle 1_{\mathbf{k}}|\hat{Q}|1_{\mathbf{k}}\rangle - \langle \text{BCS}|\hat{Q}|\text{BCS}\rangle = -e(|u_{\mathbf{k}}|^2 - |v_{\mathbf{k}}|^2)
$$
将相干因子的表达式代入，我们得到一个简洁而深刻的结果：
$$
q_{\mathbf{k}} = -e \frac{\xi_{\mathbf{k}}}{E_{\mathbf{k}}} = -e \frac{\xi_{\mathbf{k}}}{\sqrt{\xi_{\mathbf{k}}^2 + |\Delta_{\mathbf{k}}|^2}}
$$
这个结果表明：
- 在费米面上 ($\xi_{\mathbf{k}}=0$)，准粒子的有效电荷 $q_{\mathbf{k}}=0$。这意味着处于能隙边缘的最低能激发是电中性的。
- 远离费米面时，若 $\xi_{\mathbf{k}} > 0$，则 $q_{\mathbf{k}} \to -e$，准粒子表现为电子；若 $\xi_{\mathbf{k}} < 0$，则 $q_{\mathbf{k}} \to +e$，准粒子表现为空穴。

在低温下 ($k_B T \ll \Delta$)，热激发的准粒子主要集中在能隙边缘，即 $\xi_{\mathbf{k}} \approx 0$。因此，这些准粒子几乎不携带电荷，对电导的贡献很小。然而，它们携带能量 $E_{\mathbf{k}} \approx \Delta$，可以有效地传导热量。这就解释了超导体中一个著名的现象：在低温极限下，热导和电导的输运机制发生分离，维德曼-弗朗茨定律失效 [@problem_id:3012913]。

#### 群速度

准粒子的传播速度由其群速度 $v_g(\mathbf{k}) = \frac{1}{\hbar} \nabla_{\mathbf{k}} E_{\mathbf{k}}$ 决定。利用链式法则和在费米面附近的线性色散近似 $\xi_{\mathbf{k}} \approx \hbar v_F(k-k_F)$，我们可以推导出 [@problem_id:3012911]：
$$
v_g(\mathbf{k}) = \frac{1}{\hbar} \frac{\partial E_{\mathbf{k}}}{\partial \xi_{\mathbf{k}}} \nabla_{\mathbf{k}} \xi_{\mathbf{k}} = \frac{\xi_{\mathbf{k}}}{E_{\mathbf{k}}} \frac{1}{\hbar} \nabla_{\mathbf{k}} \xi_{\mathbf{k}} \approx \mathbf{v}_F \frac{\xi_{\mathbf{k}}}{E_{\mathbf{k}}}
$$
其中 $\mathbf{v}_F$ 是正常态的费米速度。这个表达式告诉我们：
- 在能隙边缘 ($\xi_{\mathbf{k}}=0$)，$v_g = 0$。这与色散关系 $E_{\mathbf{k}}$ 在此处有极小值（斜率为零）的图像一致。
- 远离能隙时 ($|\xi_{\mathbf{k}}| \gg \Delta$)，$|v_g| \to |\mathbf{v}_F|$，准粒子的速度恢复到正常态电子的费米速度。

群速度在能隙边缘的消失，意味着这些低能准粒子是“重”或“慢”的，这深刻地影响了超导体的动力学和响应特性。

#### 库珀对的关联长度

准粒子是超导基态的激发，而基态本身是由大量交叠的库珀对构成的。一个库珀对在动量空间中的波函数由反常平均值 $\Phi(\mathbf{k}) = \langle c_{-\mathbf{k}\downarrow}c_{\mathbf{k}\uparrow}\rangle = u_{\mathbf{k}}^{*}v_{\mathbf{k}} = \frac{\Delta_{\mathbf{k}}}{2E_{\mathbf{k}}}$ 描述 [@problem_id:3012886]。在弱耦合的BCS理论中，$\Delta \ll E_F$，这个函数只在费米面附近一个很窄的动量壳层内有显著数值，其宽度 $\delta k \sim \Delta / (\hbar v_F)$。根据不确定性原理，动量空间中的窄分布对应于实空间中的宽分布。这定义了库珀对的尺寸，即 **相干长度** $\xi_0$：
$$
\xi_0 \sim \frac{1}{\delta k} \sim \frac{\hbar v_F}{\Delta}
$$
在BCS极限下，由于 $\Delta \ll E_F \sim \hbar v_F k_F$，我们有 $\xi_0 \gg k_F^{-1}$，其中 $k_F^{-1}$ 是电子的平均间距。这意味着BCS库珀对是非常大的、松散束缚的扩展物体，每个库珀对的空间范围内都包含了大量其他库珀对的中心，它们是高度重叠的 [@problem_id:3012886]。这与由强相互作用形成的、尺寸小于粒子间距的紧束缚分子（Bose-Einstein凝聚极限）形成鲜明对比。

### 超出平均场理论：形式与前沿

BCS平均场理论为我们提供了准粒子的基本图像。然而，更精确的描述和对更复杂现象的研究需要更强大的理论工具。

#### 格林函数与实空间方法

**南部-戈尔科夫格林函数** 形式是研究超导体的标准场论工具。它将正常和反常传播子统一在一个 $2 \times 2$ 矩阵中。在松原频率表象下，该格林函数 $\mathcal{G}(\mathbf{k}, i\omega_n)$ 可以通过对 BdG 哈密顿量求逆得到 [@problem_id:3012944]：
$$
\mathcal{G}(\mathbf{k},i\omega_{n}) = (i\omega_n I - \mathcal{H}_{\mathbf{k}})^{-1} = \frac{1}{(i\omega_{n})^{2}-E_{\mathbf{k}}^{2}}
\begin{pmatrix}
i\omega_{n}+\xi_{\mathbf{k}} & \Delta_{\mathbf{k}} \\
\Delta_{\mathbf{k}}^{*} & i\omega_{n}-\xi_{\mathbf{k}}
\end{pmatrix}
$$
这个格林函数包含了系统的全部谱信息，是计算各种物理响应函数（如电导率、核磁共振弛豫率等）的出发点。

对于非均匀系统，如存在磁通涡旋或界面的情况，动量不再是好量子数。此时，我们需要在实空间求解 **玻戈留波夫-德热纳 (BdG) 方程**。这是一个薛定谔方程的矩阵形式 [@problem_id:3012936]：
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
其中 $H_0 = \frac{1}{2m}(-i\hbar\nabla - e\mathbf{A})^2+V(\mathbf{r})$ 是单电子哈密顿量，$\Delta(\mathbf{r})$ 是空间依赖的序参量。本征函数 $(u_n(\mathbf{r}), v_n(\mathbf{r}))^{\mathrm{T}}$ 描述了第 $n$ 个准粒子态的粒子和空穴分量的空间波函数，并满足归一化条件 $\int d^3r (|u_n(\mathbf{r})|^2 + |v_n(\mathbf{r})|^2) = 1$。BdG方程是研究超导纳米结构、安德烈夫反射和马约拉纳束缚态等现象的核心工具。

#### 准粒子寿命与强耦合效应

在真实的材料中，准粒子会与其他激发（如声子、其他准粒子或磁涨落）发生非弹性散射，从而获得有限的 **寿命**。这在格林函数形式中表现为准粒子具有了复数能量，其虚部代表衰减率。这个衰减来源于 **自能** (self-energy) $\Sigma$ 的虚部。对于一个能量为 $E$ 的准粒子，其寿命 $\tau(E)$ 与自能的关系可以近似为 [@problem_id:3012895]：
$$
\tau^{-1}(E) = -\frac{Z(E)}{\hbar} \operatorname{Im} \Sigma^{R}(\mathbf{k}, E)
$$
其中 $\Sigma^{R}$ 是推迟自能，而 $Z(E) = [1 - \partial_{\omega}\operatorname{Re}\Sigma^{R}]^{-1}$ 是准粒子权重或质量重整化因子。

对于由电-声子相互作用主导的常规超导体，**Eliashberg 理论** 提供了超越BCS的强耦合描述。在该理论中，能隙 $\Delta$ 和重整化因子 $Z$ 本身都成为能量（频率）的函数，并由一组自洽的积分方程决定 [@problem_id:3012873]。这些 **Eliashberg 方程** 的核心是 **Eliashberg 谱函数** $\alpha^2F(\Omega)$，它精确地量化了在不同频率 $\Omega$ 的声子对电子配对的贡献强度。Eliashberg 理论成功地解释了许多强耦合超导体（如铅和铌）的实验现象，是现代超导理论的重要组成部分。

#### 拓扑超导与马约拉纳费米子

近年来，准粒子激发的概念在一个激动人心的新领域——**拓扑超导**——中扮演了核心角色。在特定的超导体系中（例如，手性p波超导体），BdG哈密顿量具有特殊的对称性，允许在系统的边界或拓扑缺陷（如磁通涡旋）中存在能量严格为零的束缚态。

根据 Altland-Zirnbauer 分类，一类重要的拓扑超导体属于对称性类别 D，它具有粒子-空穴对称性 (PHS) 但没有时间反演对称性。PHS算符 $\Xi$ 满足 $\Xi \mathcal{H}_{\mathrm{BdG}} \Xi^{-1} = -\mathcal{H}_{\mathrm{BdG}}$ 和 $\Xi^2=+1$ [@problem_id:3012897]。这个对称性保证了如果 $E$ 是一个本征能量，那么 $-E$ 也是。因此，零能态 $E=0$ 在粒子-空穴谱中占据了一个特殊的位置。

对于一个孤立的零能本征态 $\Phi = (u, v)^{\mathrm{T}}$，由于 $\Xi^2=+1$，我们可以选择一个合适的相位使得该态是 PHS 的本征态，即 $\Xi \Phi = \Phi$。在自旋无相互作用的情况下，$\Xi$ 的作用是 $\Xi (u,v)^{\mathrm{T}} = (v^*, u^*)^{\mathrm{T}}$，因此该条件转化为对波函数分量的约束：$v(\mathbf{r}) = u^*(\mathbf{r})$。

现在考虑与这个零能态相对应的准粒子算符 $\gamma = \int d^2r [u^*(\mathbf{r})\psi(\mathbf{r}) + v^*(\mathbf{r})\psi^{\dagger}(\mathbf{r})]$。它的厄米共轭是 $\gamma^{\dagger} = \int d^2r [u(\mathbf{r})\psi^{\dagger}(\mathbf{r}) + v(\mathbf{r})\psi(\mathbf{r})]$。将约束条件 $v=u^*$ 代入，我们发现：
$$
\gamma = \gamma^{\dagger}
$$
这个算符等于其自身的厄米共轭！这种粒子就是它自身的反粒子的费米子，被称为 **马约拉纳费米子** (Majorana fermion)。在凝聚态物理中，一个马约拉纳零能模对应一个非局域的、受拓扑保护的量子比特，它对局域扰动免疫，具有潜在的容错量子计算应用价值。指标定理进一步指出，在一个陈数为 $C$ 的二维p波超导体中，一个涡旋度为 $n_v$ 的磁通涡旋会束缚 $|n_v||C|$ 个马约拉纳零能模 [@problem_id:3012897]。寻找和操控这些奇异的准粒子激发，是当前凝聚态物理学的最前沿之一。