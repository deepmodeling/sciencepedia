## 引言
在凝聚态物理的宏伟画卷中，超导电性无疑是最迷人的现象之一。传统的[BCS理论](@entry_id:144185)成功解释了常规金属中的[超导现象](@entry_id:142943)，描绘了一幅由[声子](@entry_id:140728)媒介形成的各向同性、$s$波库珀对的美好图景。然而，自高温[铜氧化物超导体](@entry_id:146531)发现以来，一大批新奇的超导材料，包括[铁基超导体](@entry_id:138849)、[重费米子系统](@entry_id:202711)等，展现出了远超BCS框架的复杂行为。这些材料的许多奇异性质——例如在低温下反常的[热力学](@entry_id:141121)和输运特性——都指向一个核心问题：它们的[库珀对](@entry_id:143370)[配对机制](@entry_id:145844)和对称性与[常规超导体](@entry_id:275247)有着本质的不同。

这正是本文所要深入探讨的核心：**非规整[配对对称性](@entry_id:139531)**。理解这些非传统[超导体](@entry_id:191025)的关键，在于放弃各向同性$s$波的假设，转而探究在[动量空间](@entry_id:148936)中具有复杂结构（如节点和符号反转）的配对[波函数](@entry_id:147440)。本文旨在填补从基础BCS理论到前沿非规整超导研究之间的知识鸿沟，为读者构建一个系统、深入的理论框架，以理解、分类和预测这些复杂量子物态的性质。

为了实现这一目标，本文的结构如下。**“原理与机制”**部分将从最基本的对称性原理（泡利原理、[晶格](@entry_id:196752)对称性）出发，建立起对配对态进行分类的系统方法，并介绍描述超导[准粒子](@entry_id:136584)的Bogoliubov-de Gennes形式，同时探讨驱动非规整配对的微观物理机制。接下来的**“应用与交叉学科联系”**部分将理论与实验紧密结合，系统介绍如何通过[热力学](@entry_id:141121)、[光谱学](@entry_id:141940)和相位敏感实验等手段来“验明”配对的真实对称性，并探索由此产生的拓扑超导等前沿物理现象。最后，附录中的**“动手实践”**部分提供了一系列计算练习，帮助读者将理论知识转化为解决实际问题的能力。下面，让我们首先深入学习非规整配对的对称性原理与微观机制。

## 原理与机制

在上一章介绍超导电性的基本概念之后，本章将深入探讨决定超导态丰富物理性质的核心——配对[波函数](@entry_id:147440)的对称性。传统[BCS理论](@entry_id:144185)所描述的[常规超导体](@entry_id:275247)具有各向同性的$s$波配对，其[能隙](@entry_id:191975)在[费米面](@entry_id:137798)上处处为常数。然而，许多现代凝聚态物理中发现的[超导体](@entry_id:191025)，如[铜氧化物](@entry_id:142665)、[铁基超导体](@entry_id:138849)和[重费米子系统](@entry_id:202711)，展现出更为复杂的配对行为，即**非规整配对 (unconventional pairing)**。这些超导态的[能隙](@entry_id:191975)函数在动量空间中具有非平庸的结构，包括符号改变和零点（节点）。理解这些非规整配对态的原理与机制，对于揭示这些材料中的奇异物理现象以及探索新的超导应用至关重要。

### 配对态的[基本对称性](@entry_id:161256)

[库珀对](@entry_id:143370)的[波函数](@entry_id:147440)必须满足[费米子](@entry_id:146235)交换的反对称性原理。这一基本原理对配对态的[自旋结构](@entry_id:161662)和[轨道](@entry_id:137151)（动量）结构施加了强有力的约束。对于一个由动量为$\mathbf{k}$和$-\mathbf{k}$、自旋分别为$\alpha$和$\beta$的两个电子组成的[库珀对](@entry_id:143370)，其配对振幅（或[能隙](@entry_id:191975)矩阵）$\Delta_{\alpha\beta}(\mathbf{k})$必须满足反对称条件：
$$
\Delta_{\alpha\beta}(\mathbf{k}) = -\Delta_{\beta\alpha}(-\mathbf{k})
$$
这个关系意味着交换两个电子（即$(\mathbf{k}, \alpha) \leftrightarrow (-\mathbf{k}, \beta)$）会使配对振幅反号。

我们可以将任何$2 \times 2$的[能隙](@entry_id:191975)矩阵$\Delta(\mathbf{k})$分解为自旋单态和自旋[三重态](@entry_id:156705)部分。一个通用的参数化形式是：
$$
\Delta(\mathbf{k}) = (\psi(\mathbf{k})\mathbb{I} + \mathbf{d}(\mathbf{k})\cdot\boldsymbol{\sigma}) (i\sigma_y)
$$
其中$\psi(\mathbf{k})$是一个[复标量](@entry_id:272141)函数，代表**自旋单态 (spin-singlet)** 部分，其[自旋波函数](@entry_id:190161)是反对称的（[总自旋](@entry_id:153335)$S=0$）。$\mathbf{d}(\mathbf{k})$是一个复矢量函数，通常称为**d-矢量 (d-vector)**，代表**自旋三重态 (spin-triplet)** 部分，其[自旋波函数](@entry_id:190161)是对称的（总自旋$S=1$）。$\boldsymbol{\sigma} = (\sigma_x, \sigma_y, \sigma_z)$是[泡利矩阵](@entry_id:139493)，而$i\sigma_y$是自旋单态的反对称矩阵。

将这个分解代入[费米子反对称性](@entry_id:749292)约束，我们可以推导出[轨道](@entry_id:137151)[波函数](@entry_id:147440)$\psi(\mathbf{k})$和$\mathbf{d}(\mathbf{k})$的宇称性质[@problem_id:3023183]。

对于**自旋单态**情况，$\mathbf{d}(\mathbf{k}) = \mathbf{0}$，[能隙](@entry_id:191975)矩阵为$\Delta(\mathbf{k}) = \psi(\mathbf{k}) (i\sigma_y)$。反对称约束$\Delta(\mathbf{k}) = -\Delta^T(-\mathbf{k})$给出：
$$
\psi(\mathbf{k}) (i\sigma_y) = -[\psi(-\mathbf{k}) (i\sigma_y)]^T = -\psi(-\mathbf{k}) (i\sigma_y)^T = \psi(-\mathbf{k}) (i\sigma_y)
$$
这要求[轨道](@entry_id:137151)[波函数](@entry_id:147440)$\psi(\mathbf{k})$必须是**偶宇称 (even parity)** 的，即$\psi(-\mathbf{k}) = \psi(\mathbf{k})$。

对于**自旋三重态**情况，$\psi(\mathbf{k}) = \mathbf{0}$，[能隙](@entry_id:191975)矩阵为$\Delta(\mathbf{k}) = (\mathbf{d}(\mathbf{k})\cdot\boldsymbol{\sigma}) (i\sigma_y)$。经过类似的推导，可以证明反对称约束要求d-矢量必须是**[奇宇称](@entry_id:147965) (odd parity)** 的，即$\mathbf{d}(-\mathbf{k}) = -\mathbf{d}(\mathbf{k})$。

总结起来，泡利原理将配对态分为两大类：
1.  **自旋单态，偶宇称配对**：[自旋波函数](@entry_id:190161)反对称，[轨道](@entry_id:137151)[波函数](@entry_id:147440)对称。
2.  **自旋三重态，[奇宇称](@entry_id:147965)配对**：[自旋波函数](@entry_id:190161)对称，[轨道](@entry_id:137151)[波函数](@entry_id:147440)反对称。

这一 fundamental 的分类规则在弱自旋-轨道耦合的[中心对称](@entry_id:144242)晶体中是严格成立的[@problem_id:3023143]。

除了宇称，**[时间反演对称性](@entry_id:138094) (Time-Reversal Symmetry, TRS)** 也对配对态施加了重要约束。[时间反演](@entry_id:182076)操作 $\Theta$ 包含[复共轭](@entry_id:174690) $K$ 和对自旋部分的作用。对于自旋$1/2$的粒子，$\Theta$的反幺正作用导致[能隙](@entry_id:191975)振幅有如下变换规律[@problem_id:3023183]：
-   自旋单态： $\psi(\mathbf{k}) \xrightarrow{\text{TRS}} \psi^*(-\mathbf{k})$
-   自旋三重态： $\mathbf{d}(\mathbf{k}) \xrightarrow{\text{TRS}} -\mathbf{d}^*(-\mathbf{k})$

如果一个超导态是时间反演不变的，那么它的[能隙](@entry_id:191975)函数在TRS操作下应该保持不变（最多相差一个总体规范相位）。结合宇称性质，这意味着：
-   对于[时间反演](@entry_id:182076)不变的单态，$\psi(\mathbf{k}) = \psi^*(-\mathbf{k}) = \psi^*(\mathbf{k})$，所以$\psi(\mathbf{k})$必须是实函数。
-   对于时间反演不变的[三重态](@entry_id:156705)，$\mathbf{d}(\mathbf{k}) = -\mathbf{d}^*(-\mathbf{k}) = -(-\mathbf{d}(\mathbf{k}))^* = \mathbf{d}^*(\mathbf{k})$，所以$\mathbf{d}(\mathbf{k})$必须是实矢量。

如果[能隙](@entry_id:191975)函数是复数（例如，$\mathbf{d}(\mathbf{k})$的各分量之间有非平庸的[相对相位](@entry_id:148120)，或者$\psi(\mathbf{k})$本身是复函数），则该超导态可能**破坏时间反演对称性**。

### [晶格](@entry_id:196752)对称性的作用

在真实的晶体材料中，[库珀对](@entry_id:143370)的[轨道](@entry_id:137151)[波函数](@entry_id:147440)$\Delta(\mathbf{k})$还必须遵从[晶格](@entry_id:196752)的[点群对称性](@entry_id:141230)。这意味着$\Delta(\mathbf{k})$必须能被分类为该[点群](@entry_id:142456)的某个**[不可约表示](@entry_id:263310) (irreducible representation, irrep)** 的[基函数](@entry_id:170178)[@problem_id:3023143]。这一原则是理解和分类非规整超导态的核心。

配对态通常用类比于原子轨道的角动量标签来命名，如**$s$波** ($l=0$)、**$p$波** ($l=1$)、**$d$波** ($l=2$)、**$f$波** ($l=3$)等。这些标签描述了[能隙](@entry_id:191975)函数$\Delta(\mathbf{k})$在动量空间中的主要角向依赖特征。在[晶格](@entry_id:196752)中，这些连续空间的对称性被离散的[晶格](@entry_id:196752)对称性所取代，但这些标签仍被用来指代具有相似对称性的[不可约表示](@entry_id:263310)。
-   $s$波和$d$波具有偶宇称，因此在[中心对称](@entry_id:144242)晶体中对应于**自旋单态**。
-   $p$波和$f$波具有[奇宇称](@entry_id:147965)，因此在中心对称晶体中对应于**自旋三重态**。

让我们以具有$D_{4h}$（四方）或$D_{6h}$（六方）[点群](@entry_id:142456)的晶体为例：
-   **$s$波态**: 对应于完全对称的[不可约表示](@entry_id:263310)，通常记为$A_{1g}$。在这种状态下，[能隙](@entry_id:191975)函数在所有[点群](@entry_id:142456)操作下都保持不变，即$\Delta(g\mathbf{k}) = \Delta(\mathbf{k})$。这是[常规超导体](@entry_id:275247)的对称性[@problem_id:3023143]。
-   **$d$波态**: 在四方[晶格](@entry_id:196752)中，一个重要的$d$波态是$d_{x^2-y^2}$波，其[能隙](@entry_id:191975)函数形式类似于$\Delta(\mathbf{k}) \propto \cos k_x - \cos k_y$。它属于$B_{1g}$[不可约表示](@entry_id:263310)。在六方[晶格](@entry_id:196752)中，$d$波态可以属于二维的$E_{2g}$[不可约表示](@entry_id:263310)，其[基函数](@entry_id:170178)类似于$\{k_x^2-k_y^2, 2k_xk_y\}$。这些[基函数](@entry_id:170178)可以线性组合形成所谓的**手性$d$波态 (chiral $d$-wave state)**，如$\Delta(\mathbf{k}) \propto (k_x+ik_y)^2$。这种复数[能隙](@entry_id:191975)函数破坏了时间反演对称性[@problem_id:3023143]。
-   **$p$波态**: 属于[奇宇称](@entry_id:147965)的不可约表示，例如，在六方[晶格](@entry_id:196752)中，[基函数](@entry_id:170178)为$k_x$或$k_y$的配对态属于$E_{1u}$[不可约表示](@entry_id:263310)[@problem_id:3023143]。

### Bogoliubov-de Gennes 形式

为了描述[超导体](@entry_id:191025)中的低能激发（[准粒子](@entry_id:136584)），**Bogoliubov-de Gennes (BdG) 形式** 是一个强有力的理论工具。该方法通过引入**[南部旋量](@entry_id:145326) (Nambu spinor)** 将[电子和空穴](@entry_id:274534)自由度统一起来。对于自旋$1/2$的电子，一个常用的4分量[南部旋量](@entry_id:145326)定义为：
$$
\Psi_{\mathbf{k}} = \begin{pmatrix} c_{\mathbf{k}\uparrow} & c_{\mathbf{k}\downarrow} & c^\dagger_{-\mathbf{k}\uparrow} & c^\dagger_{-\mathbf{k}\downarrow} \end{pmatrix}^T
$$
其中$c_{\mathbf{k}\sigma}$是消灭算符，$c^\dagger_{-\mathbf{k}\sigma}$是[产生算符](@entry_id:191512)。利用这个旋量，BCS[平均场哈密顿量](@entry_id:751814)可以写成一个紧凑的二次型：
$$
H = \frac{1}{2}\sum_{\mathbf{k}} \Psi_{\mathbf{k}}^\dagger H_{\mathrm{BdG}}(\mathbf{k}) \Psi_{\mathbf{k}} + \text{const.}
$$
其中$H_{\mathrm{BdG}}(\mathbf{k})$是一个$4 \times 4$的矩阵，称为[BdG哈密顿量](@entry_id:145387)。通过系统的推导，可以得到其块结构[@problem_id:3023193]：
$$
H_{\mathrm{BdG}}(\mathbf{k}) = \begin{pmatrix} h(\mathbf{k}) & \Delta(\mathbf{k}) \\ \Delta^\dagger(\mathbf{k}) & -h^T(-\mathbf{k}) \end{pmatrix}
$$
这里，$h(\mathbf{k})$是正常态的$2 \times 2$[哈密顿量](@entry_id:172864)（在自旋空间中），而$\Delta(\mathbf{k})$是前面讨论过的$2 \times 2$[能隙](@entry_id:191975)矩阵。[对角化](@entry_id:147016)$H_{\mathrm{BdG}}(\mathbf{k})$可以得到系统的[准粒子](@entry_id:136584)能谱。这个[哈密顿量](@entry_id:172864)具有内在的[粒子-空穴对称性](@entry_id:142469)，表现为$E(\mathbf{k}) = -E(-\mathbf{k})$。

根据前述的自旋单态和三重态分类，[能隙](@entry_id:191975)矩阵$\Delta(\mathbf{k})$的具体形式为[@problem_id:3023193]：
-   **自旋单态**: $\Delta_s(\mathbf{k}) = \psi(\mathbf{k}) i\sigma_y$，其中$\psi(\mathbf{k})$是偶宇称标量。
-   **自旋三重态**: $\Delta_t(\mathbf{k}) = i(\mathbf{d}(\mathbf{k})\cdot\boldsymbol{\sigma}) i\sigma_y$，其中$\mathbf{d}(\mathbf{k})$是[奇宇称](@entry_id:147965)矢量。

这些表达式与[BdG哈密顿量](@entry_id:145387)的结合，为研究任意[配对对称性](@entry_id:139531)的[超导体](@entry_id:191025)的[准粒子激发](@entry_id:138475)和[热力学](@entry_id:141121)、电磁响应等性质提供了完整的理论框架。

### [节点结构](@entry_id:151019)与[准粒子激发](@entry_id:138475)

非规整配对的一个最显著的特征是其[能隙](@entry_id:191975)函数在费米面上可能存在**节点 (nodes)**，即[能隙](@entry_id:191975)为零的点或线。这些节点的存在对[超导体](@entry_id:191025)的低能物理性质有着决定性的影响。

#### 对称性保护的节点与偶然节点

[能隙节点](@entry_id:144519)可以分为两类：**对称性保护的节点 (symmetry-protected nodes)** 和**偶然节点 (accidental nodes)**[@problem_id:3023175]。

**对称性保护的节点**是由配对态的对称性所决定的，因此它们对于保持该对称性的小微扰是稳定的。其产生机制如下：如果[晶体点群](@entry_id:183880)中存在一个[对称操作](@entry_id:143398)$g$，它使[动量空间](@entry_id:148936)中的某个子流形（点、[线或](@entry_id:170208)面）保持不变，并且[能隙](@entry_id:191975)函数$\Delta(\mathbf{k})$在该操作下的不可约[表示的特征标](@entry_id:198072)为$-1$，那么在那个不变的[子流形](@entry_id:159439)上，[能隙](@entry_id:191975)必须为零。

考虑一个动量$\mathbf{k}_0$位于被$g$固定的[子流形](@entry_id:159439)上，即$g\mathbf{k}_0 = \mathbf{k}_0$。根据群论，[能隙](@entry_id:191975)函数必须满足$\Delta(g\mathbf{k}_0) = \chi(g)\Delta(\mathbf{k}_0)$。如果特征标$\chi(g)=-1$，则有$\Delta(\mathbf{k}_0) = -\Delta(\mathbf{k}_0)$，这必然导致$\Delta(\mathbf{k}_0)=0$。

以下是一些重要的例子[@problem_id:3023175][@problem_id:3023185]：
-   对于四方[晶格](@entry_id:196752)($D_{4h}$)中的$d_{x^2-y^2}$波（$B_{1g}$表示），[能隙](@entry_id:191975)函数在对角线[镜面反射](@entry_id:270785)（如$k_x \leftrightarrow k_y$）下是奇的。这些镜面反射固定的平面是$k_x=\pm k_y$。因此，[能隙](@entry_id:191975)函数必须在这些平面上为零，形成**线节点 (line nodes)**。这些节点的位置由对称性决定，是稳固的。
-   对于奇宇称配对（如$p$波或$f$波），[能隙](@entry_id:191975)在空间反演操作$I$下是奇的，$\Delta(-\mathbf{k}) = -\Delta(\mathbf{k})$。在布里渊区的某些[时间反演](@entry_id:182076)不变动量点（TRIMs），如$\Gamma$点，满足$\mathbf{k}_\star = -\mathbf{k}_\star$（模一个[倒格矢](@entry_id:263351)）。如果[费米面](@entry_id:137798)恰好穿过这样的点，那么[能隙](@entry_id:191975)在该点必须为零，形成**点节点 (point nodes)**。
-   对于水平$E_g$态（例如，[基函数](@entry_id:170178)为$k_x k_z, k_y k_z$），[能隙](@entry_id:191975)在水平[镜面反射](@entry_id:270785)$\sigma_h$ ($k_z \to -k_z$)下为奇。因此，在$k_z=0$平面上，[能隙](@entry_id:191975)必须为零，形成一个水平的线节点[@problem_id:3023175]。

**偶然节点**则不同，它们的出现并非源于对称性的强制要求，而是由于[能隙](@entry_id:191975)函数的具体形式或参数的巧合。例如，一个常规的$A_{1g}$（$s$波）[能隙](@entry_id:191975)可以由多个该表示的[基函数](@entry_id:170178)叠加而成，例如$\Delta(\mathbf{k}) = c_0 + c_1(\cos k_x + \cos k_y)$。通过[调节系数](@entry_id:151152)$c_0$和$c_1$，这个[能隙](@entry_id:191975)函数可能在[费米面](@entry_id:137798)上出现节点。然而，这些节点的位置不固定，并且对任何保持对称性但改变系数的微扰（如压力、掺杂）都不稳定，通常会移动或消失[@problem_id:3023175]。

#### 低能激发：狄拉克[准粒子](@entry_id:136584)

在节[点的邻域](@entry_id:144055)，[准粒子](@entry_id:136584)能谱表现出独特的色散关系。我们可以通过在节点$\mathbf{k}_0$（满足$\xi_{\mathbf{k}_0}=0$和$\Delta(\mathbf{k}_0)=0$）附近线性展开[BdG哈密顿量](@entry_id:145387)来研究这一点[@problem_id:3023165]。

对角化一般的$2 \times 2$ [BdG哈密顿量](@entry_id:145387)可以得到[准粒子](@entry_id:136584)[能谱](@entry_id:181780)$E(\mathbf{k}) = \pm\sqrt{\xi_{\mathbf{k}}^2 + |\Delta(\mathbf{k})|^2}$。在节点附近，令$\mathbf{q} = \mathbf{k} - \mathbf{k}_0$，$\xi_{\mathbf{k}}$和$\Delta(\mathbf{k})$可以线性展开：
$$
\xi_{\mathbf{k}} \approx \mathbf{q} \cdot \nabla_{\mathbf{k}}\xi_{\mathbf{k}}\big|_{\mathbf{k}_0} = v_F q_1
$$
$$
\Delta(\mathbf{k}) \approx \mathbf{q} \cdot \nabla_{\mathbf{k}}\Delta(\mathbf{k})\big|_{\mathbf{k}_0} = v_\Delta q_2
$$
这里，$q_1$和$q_2$是沿着[费米面](@entry_id:137798)法向和切向的动量分量。$v_F=|\nabla_{\mathbf{k}}\xi_{\mathbf{k}}|$是**费米速度**，$v_\Delta=|\nabla_{\mathbf{k}}\Delta(\mathbf{k})|$是**[能隙](@entry_id:191975)速度**。对于$d$波[超导体](@entry_id:191025)，这两个梯度方向通常是正交的。代入[能谱](@entry_id:181780)公式，我们得到：
$$
E(\mathbf{q}) \approx \pm \sqrt{(v_F q_1)^2 + (v_\Delta q_2)^2}
$$
这个能谱描述了一个无质量、相对论性的**[狄拉克锥](@entry_id:144336) (Dirac cone)**，但速度是各向异性的。这些“狄拉克[准粒子](@entry_id:136584)”的存在，是节点[超导体](@entry_id:191025)的标志性特征。它们导致了与全[能隙](@entry_id:191975)[常规超导体](@entry_id:275247)截然不同的低温柔性，例如，态密度$N(E) \propto E$（对于线节点）或$N(E) \propto E^2$（对于点节点），而不是指数抑制。

### 非规整配对的微观机制

什么物理机制能够导致吸引相互作用在非$s$波通道中占主导？与[常规超导体](@entry_id:275247)中由[声子](@entry_id:140728)介导的各向同性吸引不同，非规整超导往往源于电子之间的排斥相互作用。

#### 排斥相互作用驱动的超导：Kohn-Luttinger 机制

一个令人惊讶的理论结果是，即使是纯粹的短程排斥相互作用，也可能导致超导配对。这一机制最早由W. Kohn和J. M. Luttinger提出。其核心思想是，电子之间的有效相互作用会被费米海中其他电子的**屏蔽 (screening)** 效应所修正。

在[动量空间](@entry_id:148936)中，这种[屏蔽效应](@entry_id:136974)体现在[粒子-空穴激发](@entry_id:137289)对有效相互作用的修正上。考虑一个短程排斥相互作用$U_0 > 0$，在[二阶微扰理论](@entry_id:192858)中，其有效相互作用$V_{\text{eff}}$会包含一个与[电子气响应函数](@entry_id:188597)$\chi_0(q)$相关的项：$V_{\text{eff}}(q) \approx U_0 + U_0^2 \chi_0(q)$。$\chi_0(q)$在$q=2k_F$处存在一个非解析点，这正是著名的**[弗里德尔振荡](@entry_id:146905) (Friedel oscillations)** 的[动量空间](@entry_id:148936)体现[@problem_id:3023169]。

这个非[解析性](@entry_id:140716)导致$V_{\text{eff}}$具有动量依赖性。在实空间中，它对应于一个在短程排斥核心之外、随距离$r$按$\cos(2k_F r)/r^3$（三维情况）衰减的[振荡](@entry_id:267781)尾巴。这个[振荡](@entry_id:267781)的尾巴在某些距离上是吸引的。

对于高角动量（大$l$）的[库珀对](@entry_id:143370)，[离心势垒](@entry_id:147153)使得两个电子天然地保持较远的距离，从而有效地“避开”了短程的排斥核心，而主要感受到长程的、具有吸引部分的[振荡](@entry_id:267781)尾巴。因此，通过将有效相互作用投影到不同的角动量通道（分波），可以发现虽然$s$波通道($l=0$)仍然是强排斥的，但在足够高的$l$通道中，有效相互作用$V_l$可以变为吸引的，其强度随$l$按[幂律衰减](@entry_id:262227)（如$V_l \sim -1/l^4$）[@problem_id:3023169]。[Kohn-Luttinger机制](@entry_id:147502)因此预言，任何具有费米面的金属，只要有排斥相互作用，原则上在足够低的温度下都可能在某个高角动量通道发生[超导相变](@entry_id:141757)。

#### [自旋涨落](@entry_id:141847)媒介的配对与 $s^{\pm}$ 态

在许多非规整[超导体](@entry_id:191025)中，一个更具体的机制被认为是**[自旋涨落](@entry_id:141847) (spin fluctuations)** 介导的配对。特别是在[铁基超导体](@entry_id:138849)中，正常态存在强烈的反铁磁涨落。这些涨落可以像[声子](@entry_id:140728)一样作为媒介，在电子之间传递相互作用。

然而，与[声子](@entry_id:140728)不同，[自旋涨落](@entry_id:141847)介导的相互作用通常在小动量转移时是排斥的，而在大的、连接不同费米面部分的特征动量$\mathbf{Q}$（反铁磁波矢）处也是排斥的。考虑一个具有两个[费米面](@entry_id:137798)的简化模型（例如，一个在[布里渊区](@entry_id:142395)中心的空穴型费米袋和一个在角落的电子型费米袋），它们之间可以通过[波矢](@entry_id:178620)$\mathbf{Q}$联系起来。由[自旋涨落](@entry_id:141847)产生的有效相互作用，其带内部分$V_{11}, V_{22}$是排斥的，而带间部分$V_{12}$（动量转移约为$\mathbf{Q}$）也是强排斥的。

这似乎不利于超导。然而，正如在线性化[BCS能隙方程](@entry_id:184182)中所看到的，带间排斥$V_{12}=+u > 0$可以驱动一种特殊的超导态[@problem_id:3023126]。考虑[能隙方程](@entry_id:141924)：
$$
\Delta_1 \propto -V_{11}N_1\Delta_1 - V_{12}N_2\Delta_2
$$
如果[能隙](@entry_id:191975)在两个费米面上符号相反，即$\text{sgn}(\Delta_1) = -\text{sgn}(\Delta_2)$，那么排斥的带间项$-V_{12}N_2\Delta_2$就会变成一个**有效吸引**，因为它与$\Delta_1$同号，从而增强了配对。这种在不同[费米面](@entry_id:137798)上符号相反，但每个[费米面](@entry_id:137798)上都近似恒定的$s$波能隙，被称为 **$s^{\pm}$波**。这种状态是全[能隙](@entry_id:191975)的，但由于其符号改变的非规整特性，它与常规$s$波（称为$s^{++}$波）有着本质区别。

在带内吸引（如[声子](@entry_id:140728)贡献$V_{ii}^{\text{ep}}  0$）和带间排斥（如[自旋涨落](@entry_id:141847)贡献$V_{ij}^{\text{sf}}  0$）的竞争中，当总的带间相互作用$V_{12} = V_{12}^{\text{ep}} + V_{12}^{\text{sf}}$从吸引转为排斥时，$s^{++}$态会让位于$s^{\pm}$态[@problem_id:3023124]。纯粹的排斥相互作用（例如，只有带间排斥$u0$而没有带内吸引）本身就足以稳定一个$s^{\pm}$超导态[@problem_id:3023126]。

### 探测[配对对称性](@entry_id:139531)：杂质的角色

如何实验上区分常规的$s$波和各种非规整配对态？一个强有力的探针是非磁性杂质的散射效应。

#### [安德森定理](@entry_id:139654)及其失效

对于常规的$s$波[超导体](@entry_id:191025)，**[安德森定理](@entry_id:139654) (Anderson's theorem)** 指出，非磁性杂质不会改变超导临界温度$T_c$。其物理图像是，一个电子被杂质从动量态$\mathbf{k}$散射到$\mathbf{k'}$，由于$s$[波能](@entry_id:164626)隙是各向同性的（$\Delta(\mathbf{k}) = \Delta(\mathbf{k'})$），库珀对的[相干性](@entry_id:268953)没有被破坏。

然而，对于非规整[超导体](@entry_id:191025)，[安德森定理](@entry_id:139654)失效了。考虑一个$d$波[超导体](@entry_id:191025)，其[能隙](@entry_id:191975)$\Delta(\mathbf{k})$在费米面上会改变符号。当一个电子被非磁性杂质从$\mathbf{k}$散射到$\mathbf{k'}$时，如果$\text{sgn}(\Delta(\mathbf{k})) = -\text{sgn}(\Delta(\mathbf{k'}))$，那么这个散射过程就破坏了[库珀对](@entry_id:143370)的相干性。从形式上看，[杂质散射](@entry_id:267814)导致的[自能修正](@entry_id:754667)项中，对[能隙](@entry_id:191975)的平均效应$\langle\Delta(\mathbf{k})\rangle_{\text{FS}}$对于$d$波或$p$波等对称性为零，因此杂质的“平均场”效应无法保护[能隙](@entry_id:191975)。相反，[杂质散射](@entry_id:267814)引入了一个有限的[准粒子寿命](@entry_id:145453)，起到了**破对 (pair-breaking)** 的作用[@problem_id:3023129]。

#### 非规整配对的 Abrikosov-Gor'kov 理论

杂质的破对效应会导致$T_c$的强烈抑制。这一现象可以用**Abrikosov-Gor'kov (AG) 理论**来定量描述。对于一个在洁净极限下临界温度为$T_{c0}$的$d$波[超导体](@entry_id:191025)，引入非磁性杂质后，其临界温度$T_c$与[杂质散射](@entry_id:267814)率$\Gamma$（正比于杂质浓度）之间的关系由以下方程给出[@problem_id:3023129]：
$$
\ln\left(\frac{T_{c0}}{T_c}\right) = \psi\left(\frac{1}{2} + \frac{\Gamma}{2\pi k_B T_c}\right) - \psi\left(\frac{1}{2}\right)
$$
其中$\psi(z)$是digamma函数。这个方程预言，$T_c$会随着$\Gamma$的增加而迅速下降。当[散射率](@entry_id:143589)达到一个临界值$\Gamma_c$时，超导将被完全抑制（$T_c \to 0$）。这个临界[散射率](@entry_id:143589)由一个普适关系给出：
$$
\frac{\Gamma_c}{k_B T_{c0}} = \frac{\pi}{2 e^\gamma} \approx 0.88
$$
其中$\gamma \approx 0.577$是[欧拉-马歇罗尼常数](@entry_id:146205)。因此，测量$T_c$随非磁性杂质浓度的变化，是判断[超导体](@entry_id:191025)是否具有符号改变的非规整[配对对称性](@entry_id:139531)的一个关键实验判据。