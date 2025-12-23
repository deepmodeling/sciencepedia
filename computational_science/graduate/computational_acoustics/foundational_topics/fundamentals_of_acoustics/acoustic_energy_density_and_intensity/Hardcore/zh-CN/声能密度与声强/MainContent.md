## 引言
声波的传播不仅是压力的扰动，更是能量在空间中的传递与分布过程。理解[声能密度](@entry_id:1120696)与[声强](@entry_id:1120700)——即单位体积的能量及其流动的速率与方向——是声学研究与工程应用的核心。仅仅测量声压大小往往不足以解答关键问题：一个扬声器辐射了多少有效功率？噪声能量是如何被吸声材料耗散的？[聚焦超声](@entry_id:893960)又是如何将能量精确传递到治疗靶区的？这些问题的答案深植于对声能流动的深刻理解之中，特别是区分真正用于传播的“有功”能量与在声源附近振荡的“无功”能量。

本文旨在系统性地构建从基础理论到前沿应用的完整知识框架。我们将在第一章**「原理与机制」**中，从[流体动力](@entry_id:750449)学的第一性原理出发，严谨推导[声能守恒](@entry_id:1122903)定律，并建立瞬时与时间平均的能量量，重点阐明有功强度与无功强度的物理内涵。随后，在第二章**「应用与交叉学科联系」**中，我们将展示这些理论工具在解决实际问题中的威力，应用领域横跨换能器设计、[声学超材料](@entry_id:174319)、医学[HIFU治疗](@entry_id:924619)以及[燃烧不稳定性](@entry_id:1122676)分析。最后，第三章**「动手实践」**将通过一系列精心设计的解析与计算练习，引导读者亲手实践，将抽象的理论转化为具体的分析能力。

现在，让我们从构建这一强大分析框架的基石——[声能守恒](@entry_id:1122903)的基本定律开始。

## 原理与机制

在理解声波的传播时，一个核心议题是能量如何被携带、传递和分布。本章将深入探讨声能的基本原理和机制，从局域能量守恒定律的推导开始，逐步建立瞬时和时间平均的能量量，并最终引入有功和无功强度的概念，以区分能量的净传输和局域存储。这些原理不仅是理论声学的基础，也在计算声学、换能器设计和声学测量等领域具有至关重要的应用价值。

### [声能守恒](@entry_id:1122903)基本定律

声波的能量描述根植于流体动力学的基本方程。在无粘、均匀、静止的流体中，小振幅声扰动由一组线性化的控制方程描述：[质量守恒](@entry_id:204015)方程、动量守恒方程（或线性化的[欧拉方程](@entry_id:177914)）以及[状态方程](@entry_id:274378)。我们将从这些第一性原理出发，推导声能的[局域守恒定律](@entry_id:261997)  。

设流体的平衡密度为 $\rho_0$，平衡压力为 $p_0$。声扰动导致密度产生微小变化 $\rho'$，压力产生微小变化 $p$（声压），并引起流体质点以速度 $\mathbf{v}$（质点速度）运动。线性化的控制方程为：

1.  **动量守恒**: $\rho_0 \frac{\partial \mathbf{v}}{\partial t} = -\nabla p$
2.  **质量守恒**: $\frac{\partial \rho'}{\partial t} + \rho_0 \nabla \cdot \mathbf{v} = 0$
3.  **状态方程**: 对于[等熵过程](@entry_id:137496)，$p = c^2 \rho'$，其中 $c$ 是声速，定义为 $c^2 = (\partial p / \partial \rho)_s$。

我们的目标是找到一个形如 $\frac{\partial e}{\partial t} + \nabla \cdot \mathbf{I} = 0$ 的守恒定律，其中 $e$ 是单位体积内的总[声能密度](@entry_id:1120696)，$\mathbf{I}$ 是能流密度矢量，即声强。

我们首先考察流体运动的动能。单位体积内流体[质点](@entry_id:186768)运动的动能密度为 $e_k = \frac{1}{2} \rho_0 |\mathbf{v}|^2$。其随时间的变化率为：
$$
\frac{\partial e_k}{\partial t} = \frac{\partial}{\partial t} \left( \frac{1}{2} \rho_0 |\mathbf{v}|^2 \right) = \rho_0 \mathbf{v} \cdot \frac{\partial \mathbf{v}}{\partial t}
$$
利用动量方程，我们可以用压力梯度替换 $\rho_0 \frac{\partial \mathbf{v}}{\partial t}$：
$$
\frac{\partial e_k}{\partial t} = \mathbf{v} \cdot (-\nabla p) = - \mathbf{v} \cdot \nabla p
$$
这个表达式的物理意义是动能密度的变化率等于压力梯度对流体所做的功的速率。为了得到守恒形式，我们使用矢量恒等式 $\nabla \cdot (p\mathbf{v}) = (\nabla p) \cdot \mathbf{v} + p(\nabla \cdot \mathbf{v})$，从而得到：
$$
\frac{\partial e_k}{\partial t} = p(\nabla \cdot \mathbf{v}) - \nabla \cdot (p\mathbf{v})
$$
移项后，我们有：
$$
\frac{\partial e_k}{\partial t} + \nabla \cdot (p\mathbf{v}) = p(\nabla \cdot \mathbf{v})
$$
方程左侧已经呈现出守恒律的形式。现在我们来处理右侧的 $p(\nabla \cdot \mathbf{v})$ 项，它代[表压力](@entry_id:147760)在压缩或膨胀流体微元时所做的功的速率。利用[质量守恒](@entry_id:204015)方程，$\nabla \cdot \mathbf{v} = -\frac{1}{\rho_0}\frac{\partial \rho'}{\partial t}$。再结合状态方程 $p = c^2 \rho'$，我们可以得到 $\frac{\partial \rho'}{\partial t} = \frac{1}{c^2}\frac{\partial p}{\partial t}$。代入后可得：
$$
p(\nabla \cdot \mathbf{v}) = p \left( -\frac{1}{\rho_0 c^2} \frac{\partial p}{\partial t} \right) = -\frac{1}{\rho_0 c^2} p \frac{\partial p}{\partial t} = -\frac{\partial}{\partial t} \left( \frac{p^2}{2\rho_0 c^2} \right)
$$
这一项的负时间导数形式表明，$\frac{p^2}{2\rho_0 c^2}$ 是一个与流体压缩相关的能量密度。我们将其定义为**瞬时声学势能密度** $e_p$。它代表了流体在[等熵压缩](@entry_id:138727)过程中存储的[弹性势能](@entry_id:168893)。

将此结果代回动能变化方程，我们得到：
$$
\frac{\partial}{\partial t} \left( \frac{1}{2} \rho_0 |\mathbf{v}|^2 \right) + \nabla \cdot (p\mathbf{v}) = -\frac{\partial}{\partial t} \left( \frac{p^2}{2\rho_0 c^2} \right)
$$
整理后，我们便得到了声能的[局域守恒定律](@entry_id:261997)：
$$
\frac{\partial}{\partial t} \left( \frac{p^2}{2\rho_0 c^2} + \frac{1}{2} \rho_0 |\mathbf{v}|^2 \right) + \nabla \cdot (p\mathbf{v}) = 0
$$
通过与标准守恒形式 $\frac{\partial e}{\partial t} + \nabla \cdot \mathbf{I} = 0$ 对比，我们可以清晰地辨认出**瞬时[声能密度](@entry_id:1120696)** $e$ 和**瞬时声强** $\mathbf{I}$  ：

-   **瞬时[声能密度](@entry_id:1120696)**: $e(t, \mathbf{x}) = e_p + e_k = \frac{p^2}{2\rho_0 c^2} + \frac{1}{2} \rho_0 |\mathbf{v}|^2$
-   **瞬时声强**: $\mathbf{I}(t, \mathbf{x}) = p\mathbf{v}$

[声能密度](@entry_id:1120696) $e$ 是单位体积内声场的总能量，由势能和动能两部分组成。声强 $\mathbf{I}$ 是一个矢量，表示单位时间内通过垂直于其方向的单位面积的能量，即能流密度。它的方向代表了声能传播的方向。

为了加深理解，我们可以进行[量纲分析](@entry_id:140259) 。能量密度的单位应为[焦耳](@entry_id:147687)/立方米 ($\mathrm{J/m^3}$)，[声强](@entry_id:1120700)的单位应为瓦特/平方米 ($\mathrm{W/m^2}$)。以[国际单位制](@entry_id:172547)（MKS）为基础，其中质量（M）、长度（L）、时间（T）为[基本量纲](@entry_id:273221)：
-   压力 $p$: $[p] = \mathrm{ML^{-1}T^{-2}}$
-   密度 $\rho_0$: $[\rho_0] = \mathrm{ML^{-3}}$
-   速度 $c, \mathbf{v}$: $[c] = [\mathbf{v}] = \mathrm{LT^{-1}}$

[声能密度](@entry_id:1120696) $e$ 的量纲为：
$$
[e] = [\rho_0 |\mathbf{v}|^2] = (\mathrm{ML^{-3}})(\mathrm{LT^{-1}})^2 = \mathrm{ML^{-1}T^{-2}}
$$
这与能量/体积的量纲（$[\mathrm{J/m^3}] = (\mathrm{ML^2T^{-2}})/\mathrm{L^3} = \mathrm{ML^{-1}T^{-2}}$）一致。
[声强](@entry_id:1120700) $\mathbf{I}$ 的量纲为：
$$
[\mathbf{I}] = [p\mathbf{v}] = (\mathrm{ML^{-1}T^{-2}})(\mathrm{LT^{-1}}) = \mathrm{MT^{-3}}
$$
这与功率/面积的量纲（$[\mathrm{W/m^2}] = (\mathrm{ML^2T^{-3}})/\mathrm{L^2} = \mathrm{MT^{-3}}$）一致。量纲的一致性验证了我们所推导表达式的物理正确性。

此外，能量守恒定律也决定了边界上的能量交换。例如，在一个刚性壁上，质点速度的法向分量为零，即 $\mathbf{v} \cdot \mathbf{n} = 0$。因此，通过该壁面的能量通量（[声强](@entry_id:1120700)的法向分量）也为零：
$$
\mathbf{I} \cdot \mathbf{n} = (p\mathbf{v}) \cdot \mathbf{n} = p(\mathbf{v} \cdot \mathbf{n}) = 0
$$
这表明，在无损情况下，声能不能穿透刚性壁 。

### 简谐场中的能量

在声学问题中，我们经常处理简谐波，即声学量随时间按正弦或余弦规律变化。在这种情况下，瞬时量通常在每个周期内快速振荡，而我们更关心的是其时间平均效应。

考虑一个沿 $x$ 轴正方向传播的一维简谐平面[行波](@entry_id:1133416)。其声压可以表示为 $p(x,t) = |p_0| \cos(kx - \omega t)$，其中 $|p_0|$ 是声压幅值，$\omega$ 是[角频率](@entry_id:261565)，$k$ 是波数。对于平面行波，声压和[质点](@entry_id:186768)速度之间存在一个简单的关系，即 $p(x,t) = \rho_0 c v(x,t)$，其中 $\rho_0 c$ 被称为介质的**特性声阻抗**。因此，质点速度为 $v(x,t) = \frac{|p_0|}{\rho_0 c} \cos(kx - \omega t)$。

瞬时[声强](@entry_id:1120700)为：
$$
I(x,t) = p(x,t)v(x,t) = \frac{|p_0|^2}{\rho_0 c} \cos^2(kx - \omega t)
$$
利用[三角恒等式](@entry_id:165065) $\cos^2\theta = \frac{1}{2}(1 + \cos(2\theta))$，我们可以将上式改写为：
$$
I(x,t) = \frac{|p_0|^2}{2\rho_0 c} (1 + \cos(2(kx - \omega t)))
$$
这个表达式揭示了两个重要特征 ：
1.  对于平面[行波](@entry_id:1133416)，瞬时强度 $I(x,t)$ 始终是非负的，这意味着能量始终朝一个方向（$+x$ 方向）净传输。
2.  瞬时强度由一个恒定部分和一个以两倍频率（$2\omega$）振荡的部分组成。这意味着能流不是平滑的，而是以声波频率的两倍脉动。

在实际测量和应用中，我们更关心的是在一个周期 $T=2\pi/\omega$ 内的**时间平均声强**，记为 $\langle I \rangle$。由于 $\cos(2\omega t)$ 项在一个周期内的平均值为零，我们得到一个极为重要的关系 ：
$$
\langle I \rangle = \frac{1}{T} \int_0^T I(x,t) dt = \frac{|p_0|^2}{2\rho_0 c}
$$
这个公式将可测量的声压幅值与声波的平均能量传输速率直接联系起来。它表明，对于给定的介质，平均[声强](@entry_id:1120700)与声压幅值的平方成正比。

### 有功强度与无功强度：复数表示法

为了更深刻地理解简谐声场中的能量动态，特别是在存在反射和散射的复杂声场中，使用复数表示法非常有效。设声压和[质点](@entry_id:186768)速度的[复振幅](@entry_id:164138)（[相量](@entry_id:270266)）分别为 $\tilde{p}(\mathbf{x})$ 和 $\tilde{\mathbf{v}}(\mathbf{x})$，并采用 $e^{j\omega t}$ 的时间因子约定，则瞬时物理量为 $p(\mathbf{x}, t) = \operatorname{Re}\{\tilde{p}(\mathbf{x})e^{j\omega t}\}$ 和 $\mathbf{v}(\mathbf{x}, t) = \operatorname{Re}\{\tilde{\mathbf{v}}(\mathbf{x})e^{j\omega t}\}$。

在这种表示法下，[时间平均](@entry_id:267915)声强可以方便地通过一个公式计算，即任意两个简谐量 $A(t)$ 和 $B(t)$ 的乘积的时间平均值为 $\langle A(t)B(t) \rangle = \frac{1}{2}\operatorname{Re}\{\tilde{A}\tilde{B}^*\}$，其中 $*$ 表示[复共轭](@entry_id:174690)。因此，[时间平均](@entry_id:267915)[声强](@entry_id:1120700)为：
$$
\langle \mathbf{I} \rangle = \langle p\mathbf{v} \rangle = \frac{1}{2}\operatorname{Re}\{\tilde{p}\tilde{\mathbf{v}}^*\}
$$
这个量被称为**有功强度**（Active Intensity），因为它代表了在一个周期内不可逆的、净的能量传输。

为了完整地描述能量行为，我们定义**复[声强](@entry_id:1120700)矢量** $\mathbf{S}$ ：
$$
\mathbf{S} = \frac{1}{2}\tilde{p}\tilde{\mathbf{v}}^*
$$
显然，有功强度就是复声强的实部：$\mathbf{I}_{\text{act}} = \operatorname{Re}\{\mathbf{S}\}$。

那么，复[声强](@entry_id:1120700)的虚部代表什么呢？我们将其定义为**无功强度**（Reactive Intensity） ：
$$
\mathbf{I}_{\text{react}} = \operatorname{Im}\{\mathbf{S}\} = \frac{1}{2}\operatorname{Im}\{\tilde{p}\tilde{\mathbf{v}}^*\}
$$
无功强度描述的是能量的局域往复交换，它不产生净的能量传输。当声压和[质点](@entry_id:186768)速度之间存在相位差时，无功强度就不为零。在每个周期的部分时间内，能量从势能形式转换到动能形式，然后又流回，如同弹簧振子在动能和势能之间转换一样。这种在声场中“晃荡”而不传播的能量流动，其幅度由无功强度来度量。

从控制方程出发，可以推导出复[声强](@entry_id:1120700)散度与[时间平均](@entry_id:267915)的动能密度 $\bar{E}_k = \frac{1}{4}\rho_0|\tilde{\mathbf{v}}|^2$ 和势能密度 $\bar{E}_p = \frac{1}{4}|\tilde{p}|^2/(\rho_0 c^2)$ 之间的关系 ：
$$
\nabla \cdot \mathbf{S} = j\omega(2\bar{E}_p - 2\bar{E}_k)
$$
分离此方程的实部和虚部，我们得到：
-   $\nabla \cdot \mathbf{I}_{\text{act}} = 0$ (在无源、无损区域)
-   $\nabla \cdot \mathbf{I}_{\text{react}} = 2\omega(\bar{E}_p - \bar{E}_k)$

第一个方程表明，在没有声源或[能量耗散](@entry_id:147406)的[稳态](@entry_id:139253)声场中，有功强度的通量是守恒的。第二个方程则揭示了无功强度的物理本质：其散度（源或汇）与[时间平均](@entry_id:267915)的势能和动能密度之差成正比。当 $\bar{E}_p \neq \bar{E}_k$ 时，意味着在一个周期内，动能和势能的转换存在不平衡，能量在空间中局域地“存储”和“释放”，这就是无功场的特征。

### 典型声场中的能量动态

通过分析几种典型的声场，我们可以更具体地理解有功和无功强度的概念。

#### [行波](@entry_id:1133416)场
在前面讨论的无损平面[行波](@entry_id:1133416)中，声压 $\tilde{p}$ 和[质点](@entry_id:186768)速度 $\tilde{v}$ 是同相位的。因此，乘积 $\tilde{p}\tilde{v}^*$ 是一个实数。这意味着 ：
-   **无功强度** $\mathbf{I}_{\text{react}} = \mathbf{0}$。
-   **有功强度** $\mathbf{I}_{\text{act}} = \frac{1}{2}\frac{|\tilde{p}|^2}{\rho_0 c} \hat{\mathbf{k}}$，其中 $\hat{\mathbf{k}}$ 是传播方向。
同时，对于平面[行波](@entry_id:1133416)，动能密度和势能密度的时间平均值是相等的，即 $\bar{E}_k = \bar{E}_p$。这与 $\nabla \cdot \mathbf{I}_{\text{react}} = 0$ 的结论一致。在行波场中，所有能量都被有效地用于向前传播。

#### 驻波场
纯驻波场是理解无功强度的绝佳例子。考虑一个由两列振[幅相](@entry_id:269870)等、方向相反的平面波叠加形成的驻波 。总声压和[质点](@entry_id:186768)速度可以表示为：
$$
p(x,t) = 2p_a \cos(kx)\cos(\omega t)
$$
$$
v(x,t) = \frac{2p_a}{\rho_0 c} \sin(kx)\sin(\omega t)
$$
我们可以看到，声压和质点速度在时间上相位相差 $90^\circ$（一个为 $\cos(\omega t)$，一个为 $\sin(\omega t)$）。它们的[复振幅](@entry_id:164138)分别为 $\tilde{p}(x) = 2p_a\cos(kx)$ 和 $\tilde{v}(x) = -j\frac{2p_a}{\rho_0 c}\sin(kx)$。

计算复[声强](@entry_id:1120700)：
$$
S_x = \frac{1}{2}\tilde{p}\tilde{v}^* = \frac{1}{2} (2p_a\cos(kx)) \left( j\frac{2p_a}{\rho_0 c}\sin(kx) \right) = j \frac{2p_a^2}{\rho_0 c}\cos(kx)\sin(kx) = j \frac{p_a^2}{\rho_0 c}\sin(2kx)
$$
复声强 $S_x$ 是一个纯虚数，这意味着  ：
-   **有功强度** $\langle I_x \rangle = \operatorname{Re}\{S_x\} = 0$。驻波不产生净的能量传输。
-   **无功强度** $I_{\text{react}, x} = \operatorname{Im}\{S_x\} = \frac{p_a^2}{\rho_0 c}\sin(2kx)$。无功强度在空间上呈正弦分布，在[波节和波腹](@entry_id:186674)处为零。

尽管没有净能量流动，驻波场中依然存在能量。其时间平均能量密度为：
$$
\langle e \rangle(x) = \langle \frac{p^2}{2\rho_0 c^2} + \frac{\rho_0 v^2}{2} \rangle = \frac{p_a^2}{\rho_0 c^2} (\cos^2(kx) + \sin^2(kx)) = \frac{p_a^2}{\rho_0 c^2}
$$
有趣的是，对于这种理想驻波，时间平均能量密度在空间上是均匀的 。这说明能量被“囚禁”在声场中。瞬时声强 $I(x,t) = p(x,t)v(x,t) = \frac{p_a^2}{\rho_0 c}\sin(2kx)\sin(2\omega t)$ 描述了这种被囚禁的能量在[波节和波腹](@entry_id:186674)之间来回“晃荡”的过程，但其[时间平均](@entry_id:267915)为零。

#### 声源的[近场与远场](@entry_id:262874)
在声源附近，声场通常兼具[行波](@entry_id:1133416)和驻波的特性。例如，一个简单的点声源（[单极子](@entry_id:1128137)）产生的声场，其声压 $\tilde{p} \propto \frac{e^{-jkr}}{r}$，而径向速度 $\tilde{v}_r \propto (\frac{1}{r} + \frac{1}{jkr^2})e^{-jkr}$。
-   在**远场**（$kr \gg 1$），$\tilde{v}_r$ 中 $1/r$ 项占主导，声压和速度近似同相，声场表现为向外传播的[球面波](@entry_id:200471)。有功强度按 $1/r^2$ 衰减（能量通过球面面积守恒），而无功强度衰减得更快。
-   在**[近场](@entry_id:269780)**（$kr \ll 1$），$\tilde{v}_r$ 中 $1/(jkr^2)$ 项占主导，声压和速度近似相差 $90^\circ$。这导致了强大的无功场 。这部分近场能量与被声源周期性推拉但并未有效辐射出去的流体质量有关。有功强度按 $1/r^2$ 衰减，而无功强度按 $1/r^3$ 衰减，表明其局域性更强。

因此，无功强度是诊断声源[近场](@entry_id:269780)行为和 evanescent wave (倏逝波) 的一个重要工具。

### [非均匀介质](@entry_id:750241)中的能量传输

最后，我们将能量守恒的概念应用于更复杂的情形：声波在缓慢变化的非均匀介质中传播，例如[水下声学](@entry_id:1129046)或大气声学中的情形。在高频极限下，我们可以使用[几何声学](@entry_id:1125600)的近似，此时声能沿着弯曲的**声线**传播。

在无损[稳态](@entry_id:139253)条件下，我们有 $\nabla \cdot \langle \mathbf{I} \rangle = 0$。考虑由一束相邻声线组成的细**声线管**。将上式在一个声线管段上积分并应用[高斯散度定理](@entry_id:188065)，可以证明通过声线管的能量通量是守恒的 。设 $A(s)$ 是沿声线路径长度 $s$ 处的声线管[横截面](@entry_id:154995)积，则：
$$
|\langle \mathbf{I}(s) \rangle| A(s) = \text{常数}
$$
在[高频近似](@entry_id:1126066)下，声场局域上可被视为[平面波](@entry_id:189798)，此时时间平均声强的大小与[时间平均](@entry_id:267915)能量密度的关系为 $|\langle \mathbf{I} \rangle| = \langle e \rangle c(\mathbf{x})$，其中 $c(\mathbf{x})$ 是局域声速。将此关系代入通量守恒定律，我们得到：
$$
\langle e(s) \rangle c(s) A(s) = \text{常数}
$$
这个重要的结果被称为**声能沿声线管的守恒律**。它表明，[时间平均](@entry_id:267915)[声能密度](@entry_id:1120696) $\langle e(s) \rangle$ 会随着声速 $c(s)$ 和声线管面积 $A(s)$ 的变化而变化：
$$
\langle e(s) \rangle = \frac{\text{常数}}{c(s)A(s)}
$$
当声线因折射而汇聚时，$A(s)$ 减小，导致[声能密度](@entry_id:1120696) $\langle e(s) \rangle$ 增加，形成焦散区。反之，当声线发散时，$A(s)$ 增大，能量被分散到更广的区域，导致[声能密度](@entry_id:1120696)降低。这一定律是理解和预测声波在海洋、大气等复杂环境中能量聚焦和衰减效应的基础。