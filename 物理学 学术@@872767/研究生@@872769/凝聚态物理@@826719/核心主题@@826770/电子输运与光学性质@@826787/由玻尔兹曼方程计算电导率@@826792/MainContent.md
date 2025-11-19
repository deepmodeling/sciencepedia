## 引言
固体中的[电荷输运](@entry_id:194535)是凝聚态物理学的核心议题之一，它不仅决定了材料的电学功能，也深刻反映了其内部的微观电子结构和动力学过程。然而，如何从电子的量子力学行为出发，建立一个能够准确预测宏观输运性质（如[电导率](@entry_id:137481)）的理论框架，始终是一个关键的科学问题。半经典的[玻尔兹曼输运方程](@entry_id:140472)（BTE）正是在这一背景下应运而生，它成功地在微观的量子能带论与宏观的经典[输运现象](@entry_id:147655)之间架起了一座坚实的桥梁。

本文旨在系统性地阐述如何运用玻尔兹曼方程来理解和计算[电导率](@entry_id:137481)。读者将学习到连接微观[散射机制](@entry_id:136443)与宏观响应的完整理论链条。在“原理与机制”一章中，我们将从[玻尔兹曼方程](@entry_id:141554)的基本形式出发，引入关键的[弛豫时间近似](@entry_id:138429)，并推导出[电导率张量](@entry_id:155827)、[霍尔系数](@entry_id:145549)和热电系数等核心输运量。随后的“应用与交叉学科联系”一章将展示该理论的强大威力，通过分析从[半导体](@entry_id:141536)、[超导体](@entry_id:191025)到[石墨烯](@entry_id:143512)乃至[中子星](@entry_id:147259)等多样化体系中的实际案例，揭示BTE在材料诊断、前沿研究和交叉学科中的广泛应用。最后，在“动手实践”部分，读者将有机会通过解决具体问题来巩固和深化对理论的理解。现在，让我们首先进入理论的核心，深入探讨玻尔兹曼方程的原理与机制。

## 原理与机制

在导论章节之后，我们现在深入探讨描述固体中[电荷输运](@entry_id:194535)的理论框架。本章的核心是半经典[玻尔兹曼输运方程](@entry_id:140472)（Boltzmann Transport Equation, BTE），这是一个强大的工具，它在量子力学能带论和经典粒子动力学之间架起了一座桥梁。我们将从[玻尔兹曼方程](@entry_id:141554)的基本形式出发，推导[电导率张量](@entry_id:155827)，并探讨各向异性、[散射机制](@entry_id:136443)、温度以及外加[磁场](@entry_id:153296)等因素如何影响材料的电学特性。

### 半经典[玻尔兹曼输运方程](@entry_id:140472)

为了描述固体中大量电子的集体行为，我们引入了分布函数 $f(\mathbf{r}, \mathbf{k}, t)$。该函数描述了在时间 $t$，位于空间位置 $\mathbf{r}$ 的电子，占据[动量空间](@entry_id:148936)中波矢为 $\mathbf{k}$ 的[量子态](@entry_id:146142)的概率。在相空间 $(\mathbf{r}, \mathbf{k})$ 中，[分布函数](@entry_id:145626) $f$ 的[全微分](@entry_id:171747)等于零，这反映了相空间中粒子数的守恒。然而，电子会受到外场驱动（漂移）和与[晶格缺陷](@entry_id:270099)、[声子](@entry_id:140728)等相互作用（散射），这两者都会改变[分布函数](@entry_id:145626)。因此，[玻尔兹曼输运方程](@entry_id:140472)可以写作：

$$
\frac{df}{dt} = \left(\frac{\partial f}{\partial t}\right)_{\text{drift}} + \left(\frac{\partial f}{\partial t}\right)_{\text{coll}} = 0
$$

漂移项描述了在外力作用下，电子在相空间中的连续演化。根据链式法则，它可以展开为：

$$
\left(\frac{\partial f}{\partial t}\right)_{\text{drift}} = \frac{\partial f}{\partial t} + \dot{\mathbf{r}} \cdot \nabla_{\mathbf{r}} f + \dot{\mathbf{k}} \cdot \nabla_{\mathbf{k}} f
$$

这里，$\dot{\mathbf{r}}$ 和 $\dot{\mathbf{k}}$ 是电子的[半经典运动方程](@entry_id:138500)，由[能带结构](@entry_id:139379) $\epsilon(\mathbf{k})$ 决定。电子的群速度为 $\mathbf{v}(\mathbf{k}) = \dot{\mathbf{r}} = \frac{1}{\hbar}\nabla_{\mathbf{k}}\epsilon(\mathbf{k})$，其波矢的变化率由外力 $\mathbf{F}_{\text{ext}}$ 决定：$\hbar\dot{\mathbf{k}} = \mathbf{F}_{\text{ext}}$。对于一个仅受[电场](@entry_id:194326) $\mathbf{E}$ 和[磁场](@entry_id:153296) $\mathbf{B}$ 作用的[电荷](@entry_id:275494)为 $-e$ 的电子，洛伦兹力为 $\mathbf{F}_{\text{ext}} = -e(\mathbf{E} + \mathbf{v}(\mathbf{k}) \times \mathbf{B})$。

碰撞项 $(\frac{\partial f}{\partial t})_{\text{coll}}$ 描述了散射过程如何使分布函数弛豫到[平衡态](@entry_id:168134)。一个极其有用的近似是**[弛豫时间近似](@entry_id:138429) (Relaxation-Time Approximation, RTA)**。该近似假设，任何对[平衡分布](@entry_id:263943) $f_0$ 的偏离都会以一个特征时间 $\tau$ 指数衰减。[平衡分布](@entry_id:263943)通常是[费米-狄拉克分布](@entry_id:138909) $f_0(\epsilon) = [1+\exp((\epsilon-\mu)/(k_B T))]^{-1}$。因此，碰撞项可以写作：

$$
\left(\frac{\partial f}{\partial t}\right)_{\text{coll}} = -\frac{f(\mathbf{r}, \mathbf{k}, t) - f_0(\epsilon(\mathbf{k}))}{\tau}
$$

弛豫时间 $\tau$ 本身可能依赖于能量 $\epsilon$、波矢 $\mathbf{k}$，甚至温度 $T$。这个近似的有效性在于它极大地简化了复杂的散射积分，同时抓住了输运现象的核心物理。

### 线性响应与[直流电导率](@entry_id:273370)张量

现在，我们运用[玻尔兹曼方程](@entry_id:141554)来计算材料对一个弱的、静态均匀[电场](@entry_id:194326) $\mathbf{E}$ 的响应。我们考虑一个稳定（$\partial f / \partial t = 0$）且空间均匀（$\nabla_{\mathbf{r}} f = 0$）的系统，且无[磁场](@entry_id:153296)（$\mathbf{B} = 0$）。此时，BTE 简化为：

$$
-\frac{e\mathbf{E}}{\hbar} \cdot \nabla_{\mathbf{k}} f = -\frac{f - f_0}{\tau}
$$

由于[电场](@entry_id:194326)很弱，[分布函数](@entry_id:145626) $f$ 只是对[平衡分布](@entry_id:263943) $f_0$ 的一个微小扰动，我们可以写成 $f \approx f_0 + \delta f$。将此式代入 BTE 并只保留 $\mathbf{E}$ 的一阶项（线性响应），我们得到：

$$
-\frac{e\mathbf{E}}{\hbar} \cdot \nabla_{\mathbf{k}} f_0 \approx -\frac{\delta f}{\tau}
$$

注意到 $f_0$ 只通过能量 $\epsilon(\mathbf{k})$ 依赖于 $\mathbf{k}$，我们可以使用[链式法则](@entry_id:190743) $\nabla_{\mathbf{k}} f_0 = (\partial f_0 / \partial \epsilon) \nabla_{\mathbf{k}} \epsilon = (\partial f_0 / \partial \epsilon) \hbar \mathbf{v}(\mathbf{k})$。于是，非平衡部分的[分布函数](@entry_id:145626)为：

$$
\delta f(\mathbf{k}) \approx e\tau(\epsilon) (\mathbf{E} \cdot \mathbf{v}(\mathbf{k})) \left(-\frac{\partial f_0}{\partial \epsilon}\right)
$$

这个表达式极具启发性。它表明，偏离平衡的程度正比于[弛豫时间](@entry_id:191572) $\tau$（散射越弱，偏离越大）和[电场](@entry_id:194326)在速度方向上的投影（驱动力）。关键因子 $(-\frac{\partial f_0}{\partial \epsilon})$ 在低温下是一个在[费米能](@entry_id:143977) $\epsilon_F$ 附近达到峰值的尖锐函数。这意味着只有能量在费米面附近的电子才对[电荷输运](@entry_id:194535)有显著贡献。

[电流密度](@entry_id:190690) $\mathbf{j}$ 是由所有电子的运动产生的，计入自旋简并度 $g_s$ 后，其表达式为：

$$
\mathbf{j} = g_s \int (-e)\mathbf{v}(\mathbf{k}) f(\mathbf{k}) \frac{d^3k}{(2\pi)^3} = -e g_s \int \mathbf{v}(\mathbf{k}) (f_0 + \delta f) \frac{d^3k}{(2\pi)^3}
$$

由于在大多数晶体中 $\epsilon(-\mathbf{k})=\epsilon(\mathbf{k})$，所以 $\mathbf{v}(-\mathbf{k})=-\mathbf{v}(\mathbf{k})$。因此，包含 $f_0$ 的积分项 $\int \mathbf{v}(\mathbf{k}) f_0(\epsilon(\mathbf{k})) d^3k$ 因为被积函数是奇函数而等于零。这意味着平衡态本身不产生净电流。电流完全来自于[电场](@entry_id:194326)引起的微小扰动 $\delta f$。

将 $\delta f$ 的表达式代入，我们得到[电流密度](@entry_id:190690)的第 $i$ 个分量 $j_i$：

$$
j_i = -e g_s \int v_i \left[ e\tau(\epsilon) \sum_j E_j v_j \left(-\frac{\partial f_0}{\partial \epsilon}\right) \right] \frac{d^3k}{(2\pi)^3} = \sum_j \left[ e^2 g_s \int \tau(\epsilon) v_i v_j \left(-\frac{\partial f_0}{\partial \epsilon}\right) \frac{d^3k}{(2\pi)^3} \right] E_j
$$

根据[欧姆定律](@entry_id:276027)的张量形式 $j_i = \sum_j \sigma_{ij} E_j$，我们立即可以识别出[电导率张量](@entry_id:155827) $\boldsymbol{\sigma}$ 的分量 [@problem_id:2985043] [@problem_id:2985041]：

$$
\sigma_{ij} = e^2 g_s \int \tau(\epsilon) v_i(\mathbf{k}) v_j(\mathbf{k}) \left(-\frac{\partial f_0}{\partial \epsilon}\right) \frac{d^3k}{(2\pi)^3}
$$

这个公式是利用玻尔兹曼方程计算线性响应[电导率](@entry_id:137481)的基石。它将宏观的输运系数 $\sigma_{ij}$ 与微观的电子性质——能带结构（通过 $v_i(\mathbf{k})$）、[散射机制](@entry_id:136443)（通过 $\tau(\epsilon)$）和电子占据情况（通过 $f_0(\epsilon)$）联系了起来。

### 各向同性与各向异性体系的应用

#### 各向同性体系：Drude 公式的再现

让我们首先将上述普遍公式应用于最简单的情景：一个具有各向同性能带 $\epsilon = \hbar^2 k^2 / (2m)$ 和恒定弛豫时间 $\tau$ 的三维[自由电子气](@entry_id:145649)。在这种情况下，速度为 $\mathbf{v} = \hbar\mathbf{k}/m$。由于对称性，非对角项 $\sigma_{ij}$ ($i \neq j$) 中的积分 $\int k_i k_j d^3k$ 为零。对角项是相等的，例如：

$$
\sigma_{xx} = e^2 \tau \int \left(\frac{\hbar k_x}{m}\right)^2 \left(-\frac{\partial f_0}{\partial \epsilon}\right) g_s \frac{d^3k}{(2\pi)^3}
$$

利用各向同性 $\langle v_x^2 \rangle = \langle v_y^2 \rangle = \langle v_z^2 \rangle = \frac{1}{3}v^2$，我们可以将积分简化。在低温极限下，$(-\partial f_0 / \partial \epsilon) \approx \delta(\epsilon-\epsilon_F)$。经过标准推导，我们最终可以得到一个简洁而著名的结果：

$$
\sigma = \frac{ne^2\tau}{m}
$$

其中 $n$ 是电子[数密度](@entry_id:268986)。这正是经典的 **Drude 公式**。我们的[半经典理论](@entry_id:189246)不仅重现了这个结果，而且赋予了其中各量明确的量子力学含义：$m$ 是有效质量，$n$ 是由费米面大小决定的载流子浓度。

#### 各向异性体系

真实晶体的[能带结构](@entry_id:139379)往往是各向异性的。一个常见的模型是各向异性抛物形能带：

$$
\epsilon(\mathbf{k}) = \frac{\hbar^2 k_x^2}{2m_x} + \frac{\hbar^2 k_y^2}{2m_y} + \frac{\hbar^2 k_z^2}{2m_z}
$$

其中 $m_x, m_y, m_z$ 是沿主轴方向的[有效质量](@entry_id:142879)分量。速度分量相应为 $v_i = \hbar k_i / m_i$。当我们计算[电导率张量](@entry_id:155827)时，由于 $\epsilon(\mathbf{k})$ 关于 $k_x, k_y, k_z$ 的分量都是偶函数，积分 $\int v_i v_j \dots d^3k \propto \int k_i k_j \dots d^3k$ 对于 $i \neq j$ 仍然为零。因此，在晶体主轴[坐标系](@entry_id:156346)中，[电导率张量](@entry_id:155827)是**对角的** [@problem_id:2985041]。

对角分量 $\sigma_{ii}$ 的计算表明，电导率与有效质量成反比。例如，对于二维系统 [@problem_id:83223]，可以清晰地证明：

$$
\frac{\sigma_{xx}}{\sigma_{yy}} = \frac{m_y}{m_x}
$$

这个结果直观地表明，电子在有效质量较小（即“较轻”）的方向上更容易被加速，从而贡献更大的[电导率](@entry_id:137481)。对于三维系统，采用类似的推导，并结合[态密度](@entry_id:147894) $g(\epsilon) = \frac{\sqrt{2}(m_x m_y m_z)^{1/2}}{2\pi^2\hbar^3}\epsilon^{1/2}$，可以得到对角分量的完整表达式 [@problem_id:2985041]：

$$
\sigma_{ii} = \frac{\sqrt{2} g_s e^2 (m_x m_y m_z)^{1/2}}{3\pi^2\hbar^3 m_i} \int_0^\infty \epsilon^{3/2} \tau(\epsilon) \left(-\frac{\partial f_0}{\partial \epsilon}\right) d\epsilon
$$

#### 更普适的能带结构

BTE 框架的强大之处在于它不局限于抛物形能带。例如，我们可以考虑一个假设性的二维系统，其[色散关系](@entry_id:140395)为 $\epsilon(\mathbf{k}) = A|\mathbf{k}|^\alpha$ [@problem_id:83212]。通过从第一性原理出发，计算[群速度](@entry_id:147686) $v(k) \propto k^{\alpha-1}$，并在 $k$ 空间中对费米面进行积分，可以推导出电导率与[载流子浓度](@entry_id:143028) $n$ 之间存在一个非平凡的依赖关系 $\sigma \propto n^{\alpha/2}$。这展示了能带结构的细节如何直接反映在可测量的输运性质中。

### [散射机制](@entry_id:136443)与温度依赖性

到目前为止，我们主要关注能带结构的影响。现在，我们将注意力转向弛豫时间 $\tau(\epsilon)$，它包含了所有关于散射过程的信息。

#### Matthiessen 法则

在许多情况下，电子会同时与多种类型的散射体发生作用，例如静态的杂质和[热激发](@entry_id:275697)的[声子](@entry_id:140728)。如果这些散射过程是[相互独立](@entry_id:273670)的，那么总的[散射率](@entry_id:143589) $1/\tau_{\text{total}}$ 就是各个独立散射率之和：

$$
\frac{1}{\tau_{\text{total}}(\epsilon)} = \sum_i \frac{1}{\tau_i(\epsilon)}
$$

这就是**Matthiessen 法则**。它意味着总电阻率（与总[散射率](@entry_id:143589)成正比）是各个[散射机制](@entry_id:136443)贡献的电阻率之和。例如，一个体系同时存在与能量无关的[杂质散射](@entry_id:267814)（$\tau_1 = c_1$）和与能量有关的[声子散射](@entry_id:140674)（例如 $\tau_2 = c_2/\epsilon$），那么总弛豫时间为 $\tau_{\text{total}}(\epsilon) = (1/c_1 + \epsilon/c_2)^{-1}$ [@problem_id:83184]。

#### [电阻率的温度依赖性](@entry_id:266964)

材料[电阻率的温度依赖性](@entry_id:266964)主要源于[弛豫时间](@entry_id:191572) $\tau(\epsilon)$ 的能量依赖关系，并通过 $(-\partial f_0/\partial \epsilon)$ 这个热展宽窗口进行能量平均。在低温下（$k_B T \ll \epsilon_F$），我们可以使用 **Sommerfeld 展开**来计算电导率积分：

$$
\int_0^\infty H(\epsilon) \left(-\frac{\partial f_0}{\partial \epsilon}\right) d\epsilon \approx H(\epsilon_F) + \frac{\pi^2}{6}(k_B T)^2 \left. \frac{d^2 H}{d\epsilon^2} \right|_{\epsilon=\epsilon_F} + \mathcal{O}(T^4)
$$

这里，$H(\epsilon)$ 是积分中除 $(-\partial f_0/\partial \epsilon)$ 之外的所有项的乘积，例如 $H(\epsilon) \propto \epsilon^{3/2}\tau(\epsilon)$。零温电导率由 $H(\epsilon_F)$ 决定，而对温度的第一个修正项则依赖于 $H(\epsilon)$ 在费米能处的[二阶导数](@entry_id:144508)。这说明，电导率对温度的敏感性取决于输运[相关函数](@entry_id:146839)在[费米面](@entry_id:137798)附近的“曲率”。

例如，若弛豫时间在[费米能](@entry_id:143977)附近可以近似为[幂律](@entry_id:143404)形式 $\tau(\epsilon) \propto \epsilon^r$ [@problem_id:2985040]，则[电导率的温度依赖性](@entry_id:143339)将表现为：

$$
\sigma(T) = \sigma_0 \left[ 1 + \frac{\pi^2}{6} C(r) \left(\frac{k_B T}{\epsilon_F}\right)^2 \right]
$$

其中 $\sigma_0$ 是零温[电导率](@entry_id:137481)，系数 $C(r)$ 取决于 $r$ 和能带的维度。这解释了为何在低温下许多金属的[电阻率](@entry_id:266481)呈现 $\rho(T) = \rho_0 + A T^2$ 的行为，其中 $\rho_0$ 是由[杂质散射](@entry_id:267814)决定的残余电阻率，而 $T^2$ 项则源于[电子-电子散射](@entry_id:152847)或特定的[电子-声子相互作用](@entry_id:140708)机制。

### [磁场](@entry_id:153296)中的[输运现象](@entry_id:147655)

当外加[磁场](@entry_id:153296) $\mathbf{B}$ 存在时，电子的运动轨迹会因[洛伦兹力](@entry_id:145104)而弯曲，从而导致一系列新的输运现象。此时，BTE 中的漂移项包含 $\mathbf{v} \times \mathbf{B}$ 项。

#### [霍尔效应](@entry_id:136243)

考虑一个标准的霍尔效应测量装置：电流 $\mathbf{j}$ 沿 $x$ 方向流动，[磁场](@entry_id:153296) $\mathbf{B}$ 沿 $z$ 方向施加。洛伦兹力 $(-e) \mathbf{v}_x \times \mathbf{B}_z$ 会使电子向 $y$ 方向偏转，导致[电荷](@entry_id:275494)在样品侧面积累，从而产生一个横向的霍尔[电场](@entry_id:194326) $E_y$。在[稳态](@entry_id:182458)下，这个霍尔[电场](@entry_id:194326)产生的电力恰好平衡了洛伦兹力，使得净的横向电流 $j_y$ 为零。

通过求解包含[磁场](@entry_id:153296)的线性化 BTE，我们可以得到[电导率张量](@entry_id:155827) $\boldsymbol{\sigma}(\mathbf{B})$。与无[磁场](@entry_id:153296)时不同，此时张量会出现非对角元 $\sigma_{xy}$ 和 $\sigma_{yx}$。通过施加条件 $j_y=0$，可以推导出霍尔[电场](@entry_id:194326)与纵向电流和[磁场](@entry_id:153296)的关系，从而定义**[霍尔系数](@entry_id:145549)** $R_H = E_y / (j_x B_z)$。

一个非常重要的结果是，对于一个仅包含单一类型载流子（电子或空穴）的能带，无论其有效质量是否各向异性，只要弛豫时间是各向同性的，[霍尔系数](@entry_id:145549)都等于 [@problem_id:83237]：

$$
R_H = -\frac{1}{ne}
$$

这个结果的意义非凡：它表明霍尔效应直接测量的是[载流子浓度](@entry_id:143028) $n$，且与复杂的散射细节（$\tau$）和[能带结构](@entry_id:139379)细节（[有效质量](@entry_id:142879) $m_i$）无关。这使得霍尔测量成为确定材料[载流子浓度](@entry_id:143028)和类型的最基本和最可靠的实验技术之一。

#### [磁阻](@entry_id:260621)

[磁阻](@entry_id:260621)是指材料电阻率随外加[磁场](@entry_id:153296)变化的现象。我们可以区分两种基本构型：

1.  **纵向磁阻**：电场和磁场方向平行（$\mathbf{E} \parallel \mathbf{B}$）。对于一个简单的各向同性费米面（球形费米面）和能量无关的[弛豫时间](@entry_id:191572)，理论计算表明纵向磁阻为零 [@problem_id:83232]。其物理原因是洛伦兹力 $\mathbf{v} \times \mathbf{B}$ 始终垂直于速度 $\mathbf{v}$，因此当 $\mathbf{v}$ 主要沿 $\mathbf{B}$ 方向时，[洛伦兹力](@entry_id:145104)非常小，并且不影响电子沿场方向的加速。在更真实的模型中，纵向[磁阻](@entry_id:260621)的存在通常暗示了复杂（非球形）的[费米面](@entry_id:137798)结构或多种载流子的存在。

2.  **横向磁阻**：电场和磁场方向垂直（$\mathbf{E} \perp \mathbf{B}$）。即使在简单的 Drude 模型中，横向[磁阻](@entry_id:260621)也非零，[电阻率](@entry_id:266481)会随 $B^2$ 增加。

### 超越[直流电导率](@entry_id:273370)

BTE 框架的应用远不止于直流[电导](@entry_id:177131)。

#### [交流电导率](@entry_id:263771)

当外加[电场](@entry_id:194326)是随时间变化的谐波场 $\mathbf{E}(t) = \mathbf{E}_0 e^{-i\omega t}$ 时，我们需要在 BTE 中保留时间导数项 $\partial f / \partial t$。假设扰动也具有相同的[谐波](@entry_id:181533)形式 $\delta f(t) = \delta f_0 e^{-i\omega t}$，线性化的 BTE 变为：

$$
(-i\omega + 1/\tau)\delta f_0 = e(\mathbf{E}_0 \cdot \mathbf{v})(-\partial f_0 / \partial \epsilon)
$$

求解这个方程并计算电流，可以得到频率依赖的复数[电导率](@entry_id:137481) $\sigma(\omega)$ [@problem_id:83318]。对于简单的 Drude 模型，结果为：

$$
\sigma(\omega) = \frac{ne^2\tau/m}{1-i\omega\tau} = \frac{\sigma_0}{1-i\omega\tau}
$$

其中 $\sigma_0$ 是[直流电导率](@entry_id:273370)。其实部 $\text{Re}[\sigma(\omega)]$ 描述了[能量耗散](@entry_id:147406)（[焦耳热](@entry_id:150496)），虚部 $\text{Im}[\sigma(\omega)]$ 描述了无耗散的电感性响应。实部为：

$$
\text{Re}[\sigma(\omega)] = \frac{\sigma_0}{1 + (\omega\tau)^2}
$$

这个结果是描述[金属光学](@entry_id:268790)性质的 Drude-Lorentz 模型的核心。它解释了为何在低频（$\omega\tau \ll 1$）时金属是良导体，而在高频（$\omega\tau \gg 1$）时其[导电性](@entry_id:137481)下降，并变得更具介电性。

#### [热电效应](@entry_id:141235)：Seebeck 效应

当材料两端存在温差时，即使没有外加[电场](@entry_id:194326)，也可能产生电流（热流驱动电流）或电势差（开路情况）。在开路条件下（$\mathbf{j}=0$），由温度梯度 $\nabla T$ 驱动产生的内部[电场](@entry_id:194326) $\mathbf{E}$ 与温度梯度成正比，比例系数被称为**Seebeck 系数** $S$（或[温差电动势](@entry_id:201717)）：$\mathbf{E} = -S \nabla T$。

通过在 BTE 框架中同时考虑[电场](@entry_id:194326)和温度梯度作为驱动力，可以推导出 Seebeck 系数。对于金属，在低温下，$S$ 可以由著名的**Mott 公式**给出：

$$
S = -\frac{\pi^2 k_B^2 T}{3e} \left[ \frac{d}{d\epsilon} \ln(\sigma(\epsilon)) \right]_{\epsilon=\epsilon_F}
$$

这里的 $\sigma(\epsilon)$ 是一个与能量相关的“准电导率”，正比于 $D(\epsilon)v(\epsilon)^2\tau(\epsilon)$，其中 $D(\epsilon)$ 是态密度。Mott 公式表明，Seebeck 系数正比于温度 $T$，并且其符号和大小取决于电导率函数在[费米能级](@entry_id:143215)附近的能量依赖关系的非对称性。例如，如果[弛豫时间](@entry_id:191572)是能量的强增函数（如[电离杂质散射](@entry_id:201067)，$\tau(\epsilon) \propto \epsilon^{3/2}$），结合[自由电子气](@entry_id:145649)的 $D(\epsilon) \propto \epsilon^{1/2}$ 和 $v(\epsilon)^2 \propto \epsilon$，则 $\sigma(\epsilon) \propto \epsilon^3$。代入 Mott 公式，得到 $S = -\pi^2 k_B^2 T / (e\epsilon_F)$ [@problem_id:83338]。Seebeck 系数因此成为一个探测费米面附近电子态和[散射机制](@entry_id:136443)能量依赖性的敏感探针。