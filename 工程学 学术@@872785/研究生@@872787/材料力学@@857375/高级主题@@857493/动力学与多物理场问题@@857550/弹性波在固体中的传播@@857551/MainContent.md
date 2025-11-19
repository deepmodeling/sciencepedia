## 引言
固体中的[弹性波传播](@entry_id:201422)是联系[材料力学](@entry_id:201885)、物理学与工程应用的桥梁，它描述了机械扰动如何在材料内部传输能量和信息。从地球深处传来的[地震波](@entry_id:164985)到检测飞机部件微小裂纹的超声波，理解其传播机制对于科学探索和技术创新至关重要。然而，初学者往往难以将抽象的数学方程与丰富多样的物理现象和工程应用联系起来。本文旨在弥合这一差距，通过系统化的讲解和实例分析，建立从第一性原理到实际应用的完整知识体系。

本文将分为三个核心部分。首先，在“原理与机制”一章中，我们将从[连续介质力学](@entry_id:155125)出发，严谨推导[弹性动力学](@entry_id:175818)的基础方程，并深入分析在各向同性及[各向异性介质](@entry_id:187796)中波的类型、特性和[能量传播](@entry_id:202589)规律。接着，“应用与跨学科联系”一章将展示这些理论如何在地球物理学、[无损检测](@entry_id:273209)和[材料科学](@entry_id:152226)等领域大放异彩，揭示[弹性波](@entry_id:196203)作为强大探测工具的价值。最后，“动手实践”部分将通过一系列精心设计的问题，引导读者运用所学知识解决具体的物理和工程问题，巩固理解。通过这一结构化的学习路径，读者将不仅掌握[弹性波传播](@entry_id:201422)的数学物理基础，更能领会其在现代科技中的核心作用，为进一步的研究和创新打下坚实的基础。

## 原理与机制

本章旨在系统地阐述固体中[弹性波传播](@entry_id:201422)的基本原理和核心机制。我们将从连续介质力学的基础出发，推导[弹性波](@entry_id:196203)的控制方程，进而分析在不同类型介质（各向同性与各向异性）中存在的波型、它们的传播特性以及[能量输运](@entry_id:183081)规律。最后，我们将探讨波与边界和界面的相互作用，这些是理解更复杂波动现象的关键。

### [弹性动力学](@entry_id:175818)的基础方程

任何关于[弹性波](@entry_id:196203)的严谨讨论都必须建立在[弹性动力学](@entry_id:175818)的三大支柱之上：运动学关系、[动量平衡](@entry_id:193575)和本构关系。这些方程共同构成了描述弹性体在外力作用下如何运动和变形的数学框架。

#### [运动学](@entry_id:173318)：应变与位移

[弹性波](@entry_id:196203)的本质是固体中质点的集体[振动](@entry_id:267781)，这种[振动](@entry_id:267781)通过材料的弹性变形进行传播。为了描述这种变形，我们首先引入[位移场](@entry_id:141476) $\mathbf{u}(\mathbf{X}, t)$，它表示位于参考构型中位置 $\mathbf{X}$ 的物质点在时刻 $t$ 相对于其初始位置的移动。当前位置 $\mathbf{x}$ 与[参考位](@entry_id:754187)置 $\mathbf{X}$ 的关系为 $\mathbf{x} = \mathbf{X} + \mathbf{u}(\mathbf{X}, t)$。

变形的局部度量由[应变张量](@entry_id:193332)描述。在有限变形理论中，[格林-拉格朗日应变张量](@entry_id:187745) $\mathbf{E}$ 精确地描述了物质点邻域内线段长度的平方变化：
$$ \mathbf{E} = \frac{1}{2}(\mathbf{F}^{\mathsf{T}}\mathbf{F} - \mathbf{I}) $$
其中 $\mathbf{F} = \partial \mathbf{x} / \partial \mathbf{X} = \mathbf{I} + \nabla \mathbf{u}$ 是变形梯度张量，$\mathbf{I}$ 是单位张量。将 $\mathbf{F}$ 的表达式代入，可以得到应变与[位移梯度](@entry_id:165352)的精确关系：
$$ E_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i}) + \frac{1}{2}u_{k,i}u_{k,j} $$
这里，$u_{i,j} = \partial u_i / \partial X_j$ 表示[位移梯度](@entry_id:165352)分量。

在[弹性波](@entry_id:196203)分析中，通常假设波的振幅很小，这使得我们可以对上述精确的[运动学](@entry_id:173318)关系进行线性化。线性化的核心假设是 **[位移梯度](@entry_id:165352)** 的所有分量都远小于1，即 $|u_{i,j}| \ll 1$。在此条件下，方程中的二次项 $u_{k,i}u_{k,j}$ 与一次项相比是高阶小量，可以忽略。这个近似被称为 **[小应变近似](@entry_id:754971)**，但更准确地说是 **小[位移梯度](@entry_id:165352)近似**，因为它不仅要求应变小，还要求[质点](@entry_id:186768)的[刚体转动](@entry_id:191086)也必须是微小的 [@problem_id:2676954]。

经过线性化，我们得到了 **[无穷小应变张量](@entry_id:167211)** $\boldsymbol{\varepsilon}$：
$$ \varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i}) $$
这个对称张量是[位移梯度张量](@entry_id:748571) $\nabla\mathbf{u}$ 的对称部分，它线性地将应变与位移场联系起来，极大地简化了后续的分析。对于一个振幅为 $|\mathbf{A}|$、[波数](@entry_id:172452)为 $|\mathbf{k}|$ 的平面[谐波](@entry_id:181533)，小[位移梯度](@entry_id:165352)条件的物理意义是振幅必须远小于波长，即 $|\mathbf{k}||\mathbf{A}| \ll 1$ [@problem_id:2676954]。

#### 动力学：应力与[动量平衡](@entry_id:193575)

描述物质运动的普适定律是[动量守恒](@entry_id:149964)。对于一个连续体，其局部形式（即[微分形式](@entry_id:146747)）由 **[柯西动量方程](@entry_id:187010)** 或柯西第一运动定律给出。在没有体力（如重力）的情况下，或者[体力](@entry_id:174230)可以忽略不计时，该方程表述为：
$$ \nabla \cdot \boldsymbol{\sigma} = \rho \frac{\partial^2 \mathbf{u}}{\partial t^2} $$
其中 $\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973)，$\rho$ 是材料的质量密度，$\ddot{\mathbf{u}}$ 是质点加速度。该方程的物理意义是，作用于一个无限小[体积元](@entry_id:267802)上的[表面力](@entry_id:188034)（由应力[张量的散度](@entry_id:191736) $\nabla \cdot \boldsymbol{\sigma}$ 表示）等于该[体积元](@entry_id:267802)的质量与加速度之积。

#### [本构关系](@entry_id:186508)：[胡克定律](@entry_id:149682)

运动学和[动力学方程](@entry_id:751029)是普适的，而连接它们的桥梁——本构关系——则描述了特定材料的力学响应。对于线弹性材料，应力与应变之间存在线性关系，即 **胡克定律**。

对于最一般的线性 **各向异性** 材料，[胡克定律](@entry_id:149682)写作：
$$ \sigma_{ij} = C_{ijkl} \varepsilon_{kl} $$
其中 $C_{ijkl}$ 是四阶[弹性刚度张量](@entry_id:170728)，包含了材料所有的弹性信息。

对于许多工程材料和地球物理学中的模型，我们可以假设材料是 **各向同性** 的，即其弹性性质不随方向改变。在这种情况下，复杂的[刚度张量](@entry_id:176588)可以由两个独立的弹性常数来表征。最常用于理论推导的是拉梅参数 (Lamé parameters) $\lambda$ 和 $\mu$：
$$ \boldsymbol{\sigma} = \lambda (\text{tr}(\boldsymbol{\varepsilon})) \mathbf{I} + 2\mu\boldsymbol{\varepsilon} $$
或用分量形式表示为：
$$ \sigma_{ij} = \lambda \delta_{ij} \varepsilon_{kk} + 2\mu \varepsilon_{ij} $$
其中 $\text{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{kk}$ 是[应变张量](@entry_id:193332)的迹，代表[体积应变](@entry_id:267252)；$\mu$ 被称为[剪切模量](@entry_id:167228)，它关联了剪应力与[剪应变](@entry_id:175241)；$\lambda$ 没有直接的物理名称，但与材料的压缩性有关。

这些理论参数可以与工程中更常见的[弹性常数](@entry_id:146207)——杨氏模量 $E$ 和泊松比 $\nu$——联系起来。通过考虑一个简单的单轴应力状态（例如，只有 $\sigma_{11}$ 非零），我们可以推导出它们之间的转换关系 [@problem_id:2882126]：
$$ \mu = \frac{E}{2(1+\nu)} $$
$$ \lambda = \frac{E\nu}{(1+\nu)(1-2\nu)} $$
这些关系对于将理论预测与实验测量联系起来至关重要。

### 均匀各向同性介质中的波传播

将上述三个基础方程——[运动学](@entry_id:173318)、[动量平衡](@entry_id:193575)和各向同性本构关系——结合起来，我们就能推导出支配[各向同性弹性](@entry_id:203237)体中位移场演化的波动方程。

#### 控制[波动方程](@entry_id:139839)：[纳维-柯西方程](@entry_id:189211)

我们的目标是得到一个只包含[位移场](@entry_id:141476) $\mathbf{u}$ 的单一控制方程。为此，我们首先将[无穷小应变](@entry_id:197162) $\boldsymbol{\varepsilon}$ 的定义代入胡克定律，得到应力-位移关系：
$$ \boldsymbol{\sigma} = \lambda (\nabla \cdot \mathbf{u}) \mathbf{I} + \mu (\nabla \mathbf{u} + (\nabla \mathbf{u})^{\mathsf{T}}) $$
接着，将此表达式代入[动量平衡](@entry_id:193575)方程 $\nabla \cdot \boldsymbol{\sigma} = \rho \ddot{\mathbf{u}}$。计算应力[张量的散度](@entry_id:191736)（假设材料均匀，即 $\lambda$ 和 $\mu$ 是常数），我们得到：
$$ \nabla \cdot \boldsymbol{\sigma} = (\lambda + \mu) \nabla(\nabla \cdot \mathbf{u}) + \mu \nabla^2 \mathbf{u} $$
于是，最终的波动方程，即 **[纳维-柯西方程](@entry_id:189211)**，为 [@problem_id:2676930]：
$$ (\lambda + \mu) \nabla(\nabla \cdot \mathbf{u}) + \mu \nabla^2 \mathbf{u} = \rho \ddot{\mathbf{u}} $$
这是一个矢量[波动方程](@entry_id:139839)，描述了位移场 $\mathbf{u}$ 在空间和时间上的演化。

#### [P波与S波](@entry_id:177682)的解耦

[纳维-柯西方程](@entry_id:189211)是一个耦合的矢量[偏微分方程](@entry_id:141332)，直接求解通常很困难。幸运的是，通过适当的数学变换，我们可以将其分解为两种更简单、物理意义更明确的波。

一种优雅的解耦方法是利用 **[亥姆霍兹分解](@entry_id:181767) (Helmholtz decomposition)**。任何足够光滑的矢量场 $\mathbf{u}$ 都可以分解为一个[无旋场](@entry_id:183486)（标量势 $\phi$ 的梯度）和一个[无散场](@entry_id:260932)（矢量势 $\boldsymbol{\Psi}$ 的旋度）之和 [@problem_id:2882154]：
$$ \mathbf{u} = \nabla \phi + \nabla \times \boldsymbol{\Psi}, \quad \text{其中 } \nabla \cdot \boldsymbol{\Psi} = 0 $$
将此分解代入[纳维-柯西方程](@entry_id:189211)，并利用矢量恒等式，方程可以被分离为两个独立的[波动方程](@entry_id:139839)：
$$ \nabla^2\phi = \frac{1}{c_p^2} \frac{\partial^2 \phi}{\partial t^2}, \quad \text{其中 } c_p = \sqrt{\frac{\lambda + 2\mu}{\rho}} $$
$$ \nabla^2\boldsymbol{\Psi} = \frac{1}{c_s^2} \frac{\partial^2 \boldsymbol{\Psi}}{\partial t^2}, \quad \text{其中 } c_s = \sqrt{\frac{\mu}{\rho}} $$
第一个是描述标量势 $\phi$ 传播的标准标量[波动方程](@entry_id:139839)，它对应的[位移场](@entry_id:141476) $\mathbf{u}_p = \nabla \phi$ 是无旋的（$\nabla \times \mathbf{u}_p = \mathbf{0}$），[质点](@entry_id:186768)[振动](@entry_id:267781)方向平行于波的传播方向。这种波被称为 **[P波](@entry_id:178440)**（Primary or Pressure wave，纵波或压缩波），其相速度为 $c_p$。

第二个是描述矢量势 $\boldsymbol{\Psi}$ 传播的矢量[波动方程](@entry_id:139839)，它对应的位移场 $\mathbf{u}_s = \nabla \times \boldsymbol{\Psi}$ 是无散的（$\nabla \cdot \mathbf{u}_s = 0$），[质点](@entry_id:186768)[振动](@entry_id:267781)方向垂直于[波的传播](@entry_id:144063)方向。这种波被称为 **S波**（Secondary or Shear wave，[横波](@entry_id:269527)或剪切波），其相速度为 $c_s$。

因此，在无限大的均匀[各向同性弹性](@entry_id:203237)介质中，只存在两种基本体波类型：[纵波](@entry_id:172335)和[横波](@entry_id:269527)。由于对所有稳定材料 $\lambda > 0, \mu > 0$，所以总有 $c_p > c_s$。这解释了在[地震学](@entry_id:203510)中，地震检波器总是先接收到[P波](@entry_id:178440)，后接收到S波。

P波和S波的速度比值仅依赖于材料的[泊松比](@entry_id:158876) $\nu$ [@problem_id:2882154]：
$$ \frac{c_p}{c_s} = \sqrt{\frac{\lambda+2\mu}{\mu}} = \sqrt{\frac{2(1-\nu)}{1-2\nu}} $$
这个关系在地球物理和[无损检测](@entry_id:273209)中有重要应用，通过测量两种波的走时差，可以反演出材料的泊松比。

#### [平面波](@entry_id:189798)分析与[克里斯托费尔方程](@entry_id:180126)

另一种分析[波动方程](@entry_id:139839)的方法是假设一个 **平面[谐波](@entry_id:181533)解 (plane wave ansatz)** [@problem_id:2676930] [@problem_id:2676974]。我们寻找形如 $\mathbf{u}(\mathbf{x},t) = \mathbf{A}\,\exp(\mathrm{i}(\mathbf{k}\cdot\mathbf{x} - \omega t))$ 的解，其中 $\mathbf{A}$ 是偏振矢量（振幅和方向），$\mathbf{k}$ 是[波矢](@entry_id:178620)（方向为传播方向 $\mathbf{n}$，大小为[波数](@entry_id:172452) $k=|\mathbf{k}|$），$\omega$ 是角频率。

将该解代入[纳维-柯西方程](@entry_id:189211)，经过[微分](@entry_id:158718)运算和化简，会得到一个关于偏振矢量 $\mathbf{A}$ 的[代数方程](@entry_id:272665)，称为 **[克里斯托费尔方程](@entry_id:180126) (Christoffel equation)**：
$$ [(\lambda + \mu) (\mathbf{k} \otimes \mathbf{k}) + \mu |\mathbf{k}|^2 \mathbf{I}] \mathbf{A} = \rho \omega^2 \mathbf{A} $$
这是一个[特征值问题](@entry_id:142153)。为了得到非零的振幅 $\mathbf{A}$，我们必须寻找该方程的特征解。

- **情况1：纵波 (P-wave)**
如果偏振矢量 $\mathbf{A}$ 平行于传播方向 $\mathbf{k}$（即 $\mathbf{A} \parallel \mathbf{k}$），方程化为 $(\lambda + 2\mu)|\mathbf{k}|^2 = \rho \omega^2$。这给出了纵[波的色散](@entry_id:275520)关系 $\omega = c_p k$，其中相速度 $c_p = \sqrt{(\lambda+2\mu)/\rho}$，与[亥姆霍兹分解](@entry_id:181767)得到的结果一致。

- **情况2：横波 (S-wave)**
如果偏振矢量 $\mathbf{A}$ 垂直于传播方向 $\mathbf{k}$（即 $\mathbf{A} \perp \mathbf{k}$），则 $\mathbf{k} \cdot \mathbf{A} = 0$。[克里斯托费尔方程](@entry_id:180126)简化为 $\mu |\mathbf{k}|^2 = \rho \omega^2$。这给出了横[波的色散](@entry_id:275520)关系 $\omega = c_s k$，其中相速度 $c_s = \sqrt{\mu/\rho}$，也与之前的结果一致。这个分析[直接证明](@entry_id:141172)了[S波](@entry_id:174890)的[质点](@entry_id:186768)运动必须与传播方向正交 [@problem_id:2676963]。

对于给定的传播方向 $\mathbf{k}$，存在一个二维平面垂直于 $\mathbf{k}$，S[波的偏振](@entry_id:262733)可以是在这个平面内的任意方向。通常，我们会根据参考[坐标系](@entry_id:156346)选择两个正交的偏振方向，例如 **SH波**（水平剪切波）和 **SV波**（垂直剪切波）。在均匀各向同性介质中，这两种S波速度相同，可以任意耦合。然而，在某些[非均匀介质](@entry_id:750241)中，例如性质仅随深度变化的层状介质（一种特殊的各向异性），如果波在包含变化方向的平面（矢状面）内传播，SH波可以与P-SV波系统[解耦](@entry_id:637294)，形成独立的动力学系统 [@problem_id:2676963]。

### [各向异性介质](@entry_id:187796)中的波传播

尽管各向同性模型在许多情况下是有效的，但自然界和工程中的许多重要材料（如晶体、[复合材料](@entry_id:139856)、木材等）都表现出 **各向异性**，即它们的弹性性质依赖于方向。

#### [各向异性介质](@entry_id:187796)中的[克里斯托费尔方程](@entry_id:180126)

对于均匀的[各向异性介质](@entry_id:187796)，我们从其一般形式的纳维方程出发：
$$ C_{ijkl} u_{k,lj} = \rho \ddot{u}_i $$
同样采用平面[谐波](@entry_id:181533)解 $u_i = A_i \exp(i(k_m x_m - \omega t))$，其中[波矢](@entry_id:178620) $\mathbf{k}$ 的方向由单位矢量 $\mathbf{n}$ 给出，即 $k_m = k n_m$。代入并求导后，我们得到一般形式的[克里斯托费尔方程](@entry_id:180126) [@problem_id:2676964]：
$$ \Gamma_{ik} A_k = \rho c^2 A_i $$
其中 $c=\omega/k$ 是相速度，$\mathbf{\Gamma}$ 是二阶 **[克里斯托费尔声学张量](@entry_id:186595)**，其分量为：
$$ \Gamma_{ik}(\mathbf{n}) = C_{ijkl} n_j n_l $$
该张量依赖于传播方向 $\mathbf{n}$，并包含了材料刚度张量 $C_{ijkl}$ 的信息。由于[弹性刚度张量](@entry_id:170728)具有主次对称性 ($C_{ijkl} = C_{klij}$)，可以证明克里斯托费尔张量是对称的 ($\Gamma_{ik} = \Gamma_{ki}$)。

这个对称性保证了对于任何给定的传播方向 $\mathbf{n}$，特征值问题总有三个实数[特征值](@entry_id:154894) $\rho c^2$，对应三个正交的[特征向量](@entry_id:151813)（偏振矢量 $\mathbf{A}$）。这意味着在任意方向上，总存在三种速度不同、偏振相互垂直的[弹性波](@entry_id:196203)。

与各向同性情况不同，在一般的[各向异性介质](@entry_id:187796)中，这三种[波的偏振](@entry_id:262733)方向通常既不严格平行于也不严格垂直于传播方向 $\mathbf{n}$。它们被称为 **准[纵波](@entry_id:172335) (quasi-longitudinal, qL)** 和两种 **准横波 (quasi-transverse, qS1, qS2)**。准纵[波的偏振](@entry_id:262733)方向最接近传播方向，通常速度最快；两种准[横波的偏振](@entry_id:196824)方向大致垂直于传播方向。

例如，在[立方晶体](@entry_id:198932)中，对于沿 `$[110]$` 方向的传播，可以求解[克里斯托费尔方程](@entry_id:180126)，得到准[纵波](@entry_id:172335)的速度为 $c_{\mathrm{QL}} = \sqrt{(C_{11}+C_{12}+2C_{44})/(2\rho)}$ [@problem_id:2676964]。

#### [慢度面](@entry_id:189732)与[群速度](@entry_id:147686)

为了更直观地理解[各向异性介质](@entry_id:187796)中的波速如何随方向变化，我们引入 **慢度矢量** $\mathbf{s} = \mathbf{n}/c$。它的方向与[波的传播](@entry_id:144063)方向相同，大小是相速度的倒数。将慢度矢量代入[克里斯托费尔方程](@entry_id:180126)的[特征值](@entry_id:154894)条件 $\det(\mathbf{\Gamma} - \rho c^2 \mathbf{I}) = 0$，可以得到一个关于慢度矢量分量 $s_1, s_2, s_3$ 的[代数方程](@entry_id:272665)。

这个方程在慢度空间中定义的[曲面](@entry_id:267450)被称为 **[慢度面](@entry_id:189732) (slowness surface)**。它由三个嵌套的[曲面](@entry_id:267450)（或称为“壳”）组成，分别对应 qL、qS1 和 qS2 三种波模态。从原点到[慢度面](@entry_id:189732)上某一点的距离，就等于该波在该方向上传播的慢度（相速度的倒数）[@problem_id:2676964]。

在[各向异性介质](@entry_id:187796)中，波的[能量传播](@entry_id:202589)方向（由 **群速度** $\mathbf{v}_g = \nabla_{\mathbf{k}} \omega$ 定义）通常与相速度方向 $\mathbf{n}$ 不同。群[速度矢量](@entry_id:269648)在几何上总是垂直于[慢度面](@entry_id:189732)。这意味着波的能量会“偏离”波前法线的方向，这种现象在声学和光学中称为波束偏折 (beam steering)。

### 能量与边界

#### [能量守恒](@entry_id:140514)与能流

弹性[波的传播](@entry_id:144063)伴随着能量的输运。在任意一点，总的[机械能](@entry_id:162989)密度 $E$ 是动能密度和[应变能密度](@entry_id:200085) $W$ 的总和：
$$ E = \frac{1}{2}\rho |\dot{\mathbf{u}}|^2 + W(\boldsymbol{\varepsilon}) $$
对于线弹性材料，$W(\boldsymbol{\varepsilon}) = \frac{1}{2}\sigma_{ij}\varepsilon_{ij}$。

通过对能量密度求时间导数，并结合[动量平衡](@entry_id:193575)方程和运动学关系，可以推导出一个局部的[能量守恒](@entry_id:140514)定律 [@problem_id:2676993]：
$$ \frac{\partial E}{\partial t} + \nabla \cdot \mathbf{Q} = 0 $$
这个方程表明，一个固定体积内能量的变化率等于通过该体积边界的能量通量。这里的 $\mathbf{Q}$ 是[能量通量](@entry_id:266056)矢量，也称为 **乌莫夫-坡印亭矢量 (Umov-Poynting vector)**，它描述了单位时间内通过单位面积的[能量流](@entry_id:142770)：
$$ \mathbf{Q} = -\boldsymbol{\sigma} \cdot \dot{\mathbf{u}} $$
对于周期性波，瞬时能流可能是[振荡](@entry_id:267781)的。一个更有用的量是能流在一个周期内的 **时间平均值**。例如，对于一个在 $x_1$ 方向传播的[纵波](@entry_id:172335) $u_1 = U_0 \cos(kx_1 - \omega t)$，其时间平均能流大小为 [@problem_id:2676993]：
$$ \langle |\mathbf{Q}| \rangle = \frac{1}{2} \sqrt{(\lambda+2\mu)\rho} U_0^2 \omega^2 = \frac{1}{2} \rho c_p (U_0 \omega)^2 $$
这表明，能流强度与材料的[声阻抗](@entry_id:267232) ($\rho c_p$)、振幅的平方和频率的平方成正比。

#### 边界与[界面条件](@entry_id:750725)

实际问题中的弹性介质总是有限的，波会与自由表面、固定边界或不同材料的界面相互作用，产生反射、透射和[模式转换](@entry_id:197482)等复杂现象。正确处理这些现象需要施加恰当的 **边界条件** 或 **[界面条件](@entry_id:750725)**。这些条件源于物理上的基本要求。

1.  **自由表面 (Free Surface)**：
    指固体与真空或压力可忽略的流体（如空气）接触的表面。由于外部没有施加任何力，根据柯西应力原理，表面的牵[引力](@entry_id:175476)矢量 $\mathbf{t} = \boldsymbol{\sigma} \cdot \mathbf{n}$ 必须为零，其中 $\mathbf{n}$ 是表面的外法线。这要求牵[引力](@entry_id:175476)矢量的所有分量（法向和切向）都为零 [@problem_id:2882142]。
    $$ \mathbf{t} = \boldsymbol{\sigma} \cdot \mathbf{n} = \mathbf{0} $$

2.  **刚性固定边界 (Clamped Boundary)**：
    指固体与一个完全刚性的固定体相连的边界。在这种情况下，边界上的任何质点都不能移动。因此，这是一个[运动学](@entry_id:173318)约束，要求[位移矢量](@entry_id:262782)在边界上处处为零 [@problem_id:2882142]。
    $$ \mathbf{u} = \mathbf{0} $$
    在这种情况下，边界上的反作用牵[引力](@entry_id:175476)是未知的，需要作为求解的一部分来确定。

3.  **完美焊接界面 (Perfectly Bonded Interface)**：
    指两种不同的弹性介质被牢固地连接在一起，没有滑移和脱开。这施加了两种条件 [@problem_id:2882142] [@problem_id:2676926]：
    -   **位移连续性**：为了保证材料的连续性（无缝隙、无重叠），界面两侧的位移必须相等。
        $$ \llbracket \mathbf{u} \rrbracket \equiv \mathbf{u}^{(2)} - \mathbf{u}^{(1)} = \mathbf{0} $$
    -   **[牵引力连续性](@entry_id:756091)**：根据[牛顿第三定律](@entry_id:166652)（作用力与[反作用](@entry_id:203910)力），界面一侧对另一侧施加的力必须大小相等、方向相反。通过对一个跨越界面的“药盒”形微元应用[动量平衡](@entry_id:193575)，可以证明在界面上没有奇异质量或力的前提下，牵[引力](@entry_id:175476)矢量必须是连续的。
        $$ \llbracket \mathbf{t} \rrbracket \equiv \boldsymbol{\sigma}^{(2)} \cdot \mathbf{n} - \boldsymbol{\sigma}^{(1)} \cdot \mathbf{n} = \mathbf{0} $$
    其中 $\mathbf{n}$ 是从介质1指向介质2的法线。值得注意的是，需要连续的是牵[引力](@entry_id:175476)矢量，而非整个应力张量。由于两侧[材料性质](@entry_id:146723)不同，[应力张量](@entry_id:148973)的某些分量在界面上通常是不连续的。

这些基本原理和机制构成了[弹性波](@entry_id:196203)理论的核心。掌握它们是分析和解决从[地震波](@entry_id:164985)勘探到超声[无损检测](@entry_id:273209)，再到声学器件设计等广泛领域中复杂波动问题的基础。