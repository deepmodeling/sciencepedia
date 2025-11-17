## 引言
在工程与科学计算领域，轴对称实体单元是一种极其高效的分析工具，它能将复杂的三维旋转体问题简化为二维模型，从而大幅节省计算资源。然而，这种简化并非简单的降维，其背后蕴含着独特的力学假设和数学公式，与标准的平面应力或[平面应变](@entry_id:167046)模型存在本质差异。许多工程师和研究人员虽然会使用相关软件，但对其核心原理的理解尚有欠缺，这可能导致模型的误用和结果的错误解读。

本文旨在填补这一知识鸿沟，为读者提供一个关于轴对称实体单元的全面而深入的指南。通过本文的学习，您将不仅理解其“如何”工作，更能洞悉其“为何”如此。

在第一章“原理与机制”中，我们将从最基本的[运动学](@entry_id:173318)假设出发，系统推导[应变-位移关系](@entry_id:173321)、[本构矩阵](@entry_id:164908)以及包含关键权重因子的弱形式，并探讨数值实现中的挑战与解决方案。随后，在第二章“应用与跨学科交叉”中，我们将展示该方法如何扩展到高级载荷、[多物理场耦合](@entry_id:171389)（如热力、[多孔介质](@entry_id:154591)、[压电效应](@entry_id:138222)）以及[非线性](@entry_id:637147)分析等前沿领域。最后，在第三章“动手实践”中，您将通过具体的计算练习，将理论知识转化为解决实际问题的能力。

让我们一同开始这段探索之旅，彻底掌握轴对称有限元分析的精髓。

## 原理与机制

本章在前一章介绍[轴对称](@entry_id:173333)分析的背景和应用的基础上，深入探讨其核心的力学原理和有限元表述机制。我们将从轴对称假设的精确条件出发，系统地推导运动学关系、[本构模型](@entry_id:174726)、变分原理和有限元离散格式。本章的目标是为读者提供一个坚实的理论基础，使其能够理解并正确应用[轴对称](@entry_id:173333)实体单元，同时洞察其在数值实现中所涉及的关键技术细节和挑战。

### 轴对称理想化：运动学与适用条件

将一个三维问题简化为二维[轴对称](@entry_id:173333)模型，是工程分析中降低计算成本的强大工具，但这必须建立在严格的物理假设之上。一个二维轴对称模型能够精确地代表完整的三维问题，其必要且充分的条件是：问题的几何、材料属性、[体力](@entry_id:174230)以及所有边界条件（包括指定的位移和面力）在[柱坐标系](@entry_id:266798) $(r, \theta, z)$ 中均不依赖于环向坐标 $\theta$。此外，所有施加的载荷和[位移边界条件](@entry_id:203261)必须没有环向分量。只有当这些条件全部满足时，三维物体的响应才具有纯粹的轴对称性，即位移场不含环向分量 $u_\theta$，并且径向位移 $u_r$ 和轴向位移 $u_z$ 仅是 $r$ 和 $z$ 的函数。违反这些条件中的任何一条，都将导致解依赖于 $\theta$，从而使得标准的二维[轴对称](@entry_id:173333)模型失效。一个典型的反例是，在一个圆柱壳的侧表面特定[方位角](@entry_id:164011) $\theta_0$ 处施加一个集中的径向力，这种载荷破坏了轴对称性，其产生的应力与位移场必然随 $\theta$ 变化，无法用二维模型精确捕捉 [@problem_id:2542338]。

在[轴对称](@entry_id:173333)假设下，我们可以从三维[柱坐标系](@entry_id:266798)中的一般[应变-位移关系](@entry_id:173321)出发，推导其简化形式。通用的三维[小应变张量](@entry_id:754968) $\boldsymbol{\varepsilon}$ 定义为[位移梯度](@entry_id:165352) $\nabla\mathbf{u}$ 的对称部分。在[柱坐标系](@entry_id:266798)中，其分量为：
$$
\begin{aligned}
\varepsilon_{rr} &= \frac{\partial u_r}{\partial r} \\
\varepsilon_{zz} &= \frac{\partial u_z}{\partial z} \\
\varepsilon_{\theta\theta} &= \frac{1}{r}\frac{\partial u_\theta}{\partial \theta} + \frac{u_r}{r} \\
\gamma_{rz} &= 2\varepsilon_{rz} = \frac{\partial u_r}{\partial z} + \frac{\partial u_z}{\partial r} \\
\gamma_{r\theta} &= 2\varepsilon_{r\theta} = \frac{1}{r}\frac{\partial u_r}{\partial \theta} - \frac{u_\theta}{r} + \frac{\partial u_\theta}{\partial r} \\
\gamma_{\theta z} &= 2\varepsilon_{\theta z} = \frac{\partial u_\theta}{\partial z} + \frac{1}{r}\frac{\partial u_z}{\partial \theta}
\end{aligned}
$$
其中 $\gamma_{ij}$ 是工程[剪应变](@entry_id:175241)。对于标准的无扭转[轴对称](@entry_id:173333)问题，我们有 $u_\theta = 0$ 且所有场量对 $\theta$ 的偏导数为零。将这些条件代入上述通用公式，涉及 $\theta$ 的剪切应变 $\gamma_{r\theta}$ 和 $\gamma_{\theta z}$ 立即消失。非零的应变分量只剩下四个，它们构成了轴对称分析的核心[运动学](@entry_id:173318)关系 [@problem_id:2542274]：

- **径向应变 (Radial Strain)**: $\varepsilon_{rr} = \frac{\partial u_r}{\partial r}$，描述了材料沿径向的伸缩。
- **[轴向应变](@entry_id:160811) (Axial Strain)**: $\varepsilon_{zz} = \frac{\partial u_z}{\partial z}$，描述了材料沿轴向的伸缩。
- **[环向应变](@entry_id:174548) (Hoop Strain)**: $\varepsilon_{\theta\theta} = \frac{u_r}{r}$，这是一个至关重要的应变分量，具有独特的几何来源。
- **面内[剪应变](@entry_id:175241) (In-plane Shear Strain)**: $\gamma_{rz} = \frac{\partial u_r}{\partial z} + \frac{\partial u_z}{\partial r}$，描述了 $r-z$ 平面内的[剪切变形](@entry_id:170920)。

这四个应变分量 $\varepsilon_{rr}, \varepsilon_{zz}, \varepsilon_{\theta\theta}, \gamma_{rz}$ 完全由径向位移 $u_r(r,z)$ 和轴向位移 $u_z(r,z)$ 决定。

其中，**[环向应变](@entry_id:174548)** $\varepsilon_{\theta\theta}$ 值得特别关注。它的物理意义是材料圆周的相对伸长率。考虑一个初始半径为 $r$ 的材料[圆环](@entry_id:163678)，其[周长](@entry_id:263239)为 $C_0 = 2\pi r$。在发生径向位移 $u_r$ 后，其半径变为 $r' = r + u_r$，新[周长](@entry_id:263239)为 $C_f = 2\pi(r+u_r)$。根据工程应变的定义，[环向应变](@entry_id:174548)即为 $\varepsilon_{\theta\theta} = (C_f - C_0) / C_0 = (2\pi u_r) / (2\pi r) = u_r / r$ [@problem_id:2542354]。这个关系纯粹由变形几何决定，与材料属性或应力状态无关。

将轴对称模型与二维笛卡尔坐标系下的[平面应变](@entry_id:167046)和平面应力模型进行对比，有助于加深理解。在**平面应变**中，我们假设平面外（如 $z$ 方向）的应变 $\varepsilon_{zz}$ 为零。有人可能会错误地类推，认为在轴对称的 $r-z$ 平面分析中，"平面外"的[环向应变](@entry_id:174548) $\varepsilon_{\theta\theta}$ 也应为零。然而，这是完全错误的。强制 $\varepsilon_{\theta\theta} = u_r/r = 0$ 将意味着在 $r>0$ 的所有地方 $u_r$ 都必须为零，这会不切实际地禁止任何径向变形，从而扼杀了问题的核心物理。相比之下，**[平面应力](@entry_id:172193)**假设（例如，在薄板中）强制平面外应力 $\sigma_{zz}=0$，但平面外应变 $\varepsilon_{zz}$ 由于[泊松效应](@entry_id:158876)通常非零。这种类比在轴对称中更为贴切：即使在某些情况下（如薄盘）可以假设 $\sigma_{zz}=0$，但运动学关系 $\varepsilon_{\theta\theta}=u_r/r$ 依然成立。任何非零的径向位移都会产生[环向应变](@entry_id:174548)，这一几何约束无法通过应力假设来消除 [@problem_id:2542354]。

### 本构关系

在确定了[运动学](@entry_id:173318)关系后，我们需要一个[本构模型](@entry_id:174726)来关联[应力与应变](@entry_id:137374)。对于一个均匀、各向同性的线弹性材料，其三维[本构关系](@entry_id:186508)（[胡克定律](@entry_id:149682)）由拉梅参数 $\lambda$ 和 $\mu$ ([剪切模量](@entry_id:167228) $G$) 描述：
$$
\sigma_{ij} = \lambda \varepsilon_v \delta_{ij} + 2\mu \varepsilon_{ij}
$$
其中 $\varepsilon_v = \varepsilon_{kk}$ 是[体积应变](@entry_id:267252)，$\delta_{ij}$ 是克罗内克符号。

在轴对称情况下，[应力张量和应变张量](@entry_id:755512)都简化了。由于 $\varepsilon_{r\theta} = \varepsilon_{\theta z} = 0$，对应的[剪切应力](@entry_id:137139)也为零：$\tau_{r\theta} = \tau_{\theta z} = 0$。非零的应力分量为 $\sigma_{rr}, \sigma_{zz}, \sigma_{\theta\theta}$ 和 $\tau_{rz}$。体积应变为 $\varepsilon_v = \varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}$。将这些代入三维胡克定律，我们可以得到轴对称[应力-应变关系](@entry_id:274093)：
$$
\begin{aligned}
\sigma_{rr} &= \lambda(\varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}) + 2\mu\varepsilon_{rr} \\
\sigma_{zz} &= \lambda(\varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}) + 2\mu\varepsilon_{zz} \\
\sigma_{\theta\theta} &= \lambda(\varepsilon_{rr} + \varepsilon_{zz} + \varepsilon_{\theta\theta}) + 2\mu\varepsilon_{\theta\theta} \\
\tau_{rz} &= 2\mu\varepsilon_{rz} = \mu\gamma_{rz}
\end{aligned}
$$
在有限元分析中，通常将这些关系写成矩阵形式 $\boldsymbol{\sigma} = \mathbf{D} \boldsymbol{\varepsilon}$。为此，我们将应力向量和应变向量按特定顺序[排列](@entry_id:136432)，例如 $\boldsymbol{\sigma} = \{\sigma_{rr}, \sigma_{zz}, \sigma_{\theta\theta}, \tau_{rz}\}^\mathsf{T}$ 和 $\boldsymbol{\varepsilon} = \{\varepsilon_{rr}, \varepsilon_{zz}, \varepsilon_{\theta\theta}, \gamma_{rz}\}^\mathsf{T}$。通过整理上述方程的系数，并用杨氏模量 $E$ 和[泊松比](@entry_id:158876) $\nu$ 替换拉梅参数，我们可以得到轴对称问题的 $4 \times 4$ **[本构矩阵](@entry_id:164908)** $\mathbf{D}$ [@problem_id:2542313]：
$$
\mathbf{D} = \frac{E}{(1+\nu)(1-2\nu)}
\begin{pmatrix}
1-\nu & \nu & \nu & 0 \\
\nu & 1-\nu & \nu & 0 \\
\nu & \nu & 1-\nu & 0 \\
0 & 0 & 0 & \frac{1-2\nu}{2}
\end{pmatrix}
$$
这个矩阵是后续有限元公式的核心组成部分，它将离散的应变场与应[力场](@entry_id:147325)联系起来。

### 弱形式与有限元离散

[有限元法](@entry_id:749389)建立在[变分原理](@entry_id:198028)或[弱形式](@entry_id:142897)之上。轴对称问题的[弱形式](@entry_id:142897)可以从三维**[虚功原理](@entry_id:138749) (Principle of Virtual Work, PVW)** 推导得出。三维PVW表明，对于任意满足[位移边界条件](@entry_id:203261)的[虚位移](@entry_id:168781)场 $\delta\boldsymbol{u}$，[内力](@entry_id:167605)所做的[虚功](@entry_id:176403)等于外力所做的[虚功](@entry_id:176403)：
$$
\int_{\Omega^{(3\mathrm{D})}} \boldsymbol{\sigma} : \delta \boldsymbol{\varepsilon}\,\mathrm{d}V = \int_{\Omega^{(3\mathrm{D})}} \delta \boldsymbol{u} \cdot \boldsymbol{b}\,\mathrm{d}V + \int_{\Gamma_{t}^{(3\mathrm{D})}} \delta \boldsymbol{u} \cdot \boldsymbol{t}\,\mathrm{d}S
$$
为了将其简化为轴对称形式，我们必须在[柱坐标系](@entry_id:266798)下对环向坐标 $\theta$ 进行积分。三维体积微元 $\mathrm{d}V$ 可以表示为 $\mathrm{d}V = r\,\mathrm{d}r\,\mathrm{d}\theta\,\mathrm{d}z = r\,\mathrm{d}\theta\,\mathrm{d}A$，其中 $\mathrm{d}A = \mathrm{d}r\,\mathrm{d}z$ 是子午平面 ($r-z$ 平面) 上的面积微元。同样，由子午平面上的线段 $\mathrm{d}\Gamma$ 绕 $z$ 轴旋转生成的面积微元为 $\mathrm{d}S = r\,\mathrm{d}\theta\,\mathrm{d}\Gamma$。

由于[轴对称](@entry_id:173333)问题的所有场量（如 $\boldsymbol{\sigma}:\delta\boldsymbol{\varepsilon}$）都与 $\theta$ 无关，我们可以将对 $\theta$ 的积分从 $0$ 到 $2\pi$ 提前进行。这个积分产生一个常数因子 $2\pi$。因此，三维积分可以转化为在二维子午域 $\Omega$ 上的积分，但每个积分项都必须乘以一个几何权重因子 [@problem_id:2542349]：
$$
\int_{\Omega} (\boldsymbol{\sigma}^\mathsf{T} \delta \boldsymbol{\varepsilon}) \, (2\pi r) \, \mathrm{d}A = \int_{\Omega} (\delta \boldsymbol{u}^\mathsf{T} \boldsymbol{b}) \, (2\pi r) \, \mathrm{d}A + \int_{\Gamma_{t}} (\delta \boldsymbol{u}^\mathsf{T} \boldsymbol{t}) \, (2\pi r) \, \mathrm{d}\Gamma
$$
这里的关键点在于，所有积分中都出现了一个**权重因子** $\boldsymbol{2\pi r}$。这个因子源于[柱坐标系](@entry_id:266798)的[雅可比行列式](@entry_id:137120)，它解释了随着半径的增加，单位子午面积所代表的三维体积或表面积也在增加。

接下来，我们引入有限元离散。在一个单元内，[位移场](@entry_id:141476)由节点位移 $\mathbf{d}$ 和形函数 $\mathbf{N}$ 插值得到：$\mathbf{u}(r,z) = \mathbf{N}(r,z)\mathbf{d}$。应变场则通过**[应变-位移矩阵](@entry_id:163451)** $\mathbf{B}$ 与节点位移关联：$\boldsymbol{\varepsilon} = \mathbf{B}\mathbf{d}$。为了推导 $\mathbf{B}$ 矩阵，我们将插值位移代入轴对称[运动学](@entry_id:173318)关系中。对于一个具有 $n$ 个节点的单元，其位移场为 $u_r = \sum_{i=1}^n N_i u_{ri}$ 和 $u_z = \sum_{i=1}^n N_i u_{zi}$。将这些代入应变公式，并整理成矩阵形式，可得到 $4 \times 2n$ 的 $\mathbf{B}$ 矩阵 [@problem_id:2542299]：
$$
\mathbf{B} = 
\begin{bmatrix}
\mathbf{B}_1 & \mathbf{B}_2 & \dots & \mathbf{B}_n
\end{bmatrix}
$$
其中，与节点 $i$ 相关的子矩阵 $\mathbf{B}_i$ 为（对应于应变向量 $\boldsymbol{\varepsilon} = \{\varepsilon_{rr}, \varepsilon_{zz}, \varepsilon_{\theta\theta}, \gamma_{rz}\}^\mathsf{T}$）：
$$
\mathbf{B}_i = \begin{bmatrix}
\frac{\partial N_i}{\partial r} & 0 \\
0 & \frac{\partial N_i}{\partial z} \\
\frac{N_i}{r} & 0 \\
\frac{\partial N_i}{\partial z} & \frac{\partial N_i}{\partial r}
\end{bmatrix}
$$
请注意 $\mathbf{B}$ 矩阵的第三行，即对应于[环向应变](@entry_id:174548) $\varepsilon_{\theta\theta}$ 的那一行，它包含了 $N_i/r$ 这一项。正是这一项，给[轴对称单元](@entry_id:163652)的数值实现带来了独特的挑战。

将离散化的应变 $\boldsymbol{\varepsilon} = \mathbf{B}\mathbf{d}$ 和应力 $\boldsymbol{\sigma} = \mathbf{D}\boldsymbol{\varepsilon} = \mathbf{D}\mathbf{B}\mathbf{d}$ 代入弱形式的左端项（内力[虚功](@entry_id:176403)），我们得到单元的**刚度矩阵** $\mathbf{k}_e$ 的表达式：
$$
\mathbf{k}_e = \int_{\Omega_e} \mathbf{B}^\mathsf{T} \mathbf{D} \mathbf{B} \, (2\pi r) \, \mathrm{d}A
$$
这个积分是在单元的子午面积 $\Omega_e$ 上进行的，并且包含了关键的 $2\pi r$ 权重。

### 数值实现与特殊考虑

#### [对称轴](@entry_id:177299)上的边界条件

当分析的物体是实心体，即其域包含[对称轴](@entry_id:177299) $r=0$ 时，必须施加正确的边界条件以确保解的物理合理性。这些条件源于对称性和正则性要求 [@problem_id:2542353]。

1.  **径向位移 $u_r = 0$**：为了使[环向应变](@entry_id:174548) $\varepsilon_{\theta\theta} = u_r/r$ 在 $r=0$ 处保持有限，分子 $u_r$ 必须为零。物理上，[对称轴](@entry_id:177299)上的点不能有径向位移，否则会导致材料撕裂或自穿透。这是一个必须施加的**本质边界条件**。

2.  **剪切应变 $\gamma_{rz} = 0$**：由于对称性，子午平面内的剪切应变在[对称轴](@entry_id:177299)上必须为零。从运动学关系 $\gamma_{rz} = \partial u_r/\partial z + \partial u_z/\partial r$ 出发，由于在 $r=0$ 上 $u_r$ 对所有 $z$ 均为零，因此 $\partial u_r/\partial z = 0$。这就要求 $\frac{\partial u_z}{\partial r} = 0$。这个条件意味着轴向位移剖面在[对称轴](@entry_id:177299)处的径向斜率为零，这与 $u_z(r,z)$ 是一个关于 $r$ 的光滑偶函数相符。在标准的 $C^0$ 连续有限元中，这个条件是作为自然边界条件满足的，通常不需要显式强制。

3.  **环向位移 $u_\theta = 0$**：如前所述，这是标准无扭转[轴对称](@entry_id:173333)问题的基本假设。

在典型的有限元程序中，对于位于对称轴上的节点，会直接施加本质边界条件 $u_r=0$。

#### 数值积分

[单元刚度矩阵](@entry_id:139369)的积分通常采用**[高斯积分](@entry_id:187139)**。对于从自然坐标 $(\xi, \eta)$ 映射到物理坐标 $(r,z)$ 的[等参单元](@entry_id:173863)，积分变为：
$$
\mathbf{k}_e = \int_{-1}^{1}\int_{-1}^{1} \mathbf{B}^\mathsf{T}(\xi, \eta) \mathbf{D} \mathbf{B}(\xi, \eta) \, r(\xi, \eta) \, (2\pi \det\mathbf{J}) \, \mathrm{d}\xi\mathrm{d}\eta
$$
其中 $\mathbf{J}$ 是[坐标变换](@entry_id:172727)的雅可比矩阵。为了保持[变分一致性](@entry_id:756438)，被积函数中的每一项，包括半径 $r$，都必须在每个[高斯积分](@entry_id:187139)点 $(\xi_g, \eta_g)$ 处进行计算。在[等参单元](@entry_id:173863)中，半径 $r$ 本身也由形函数插值得到：$r(\xi, \eta) = \sum N_i(\xi, \eta) r_i$。因此，在每个[高斯点](@entry_id:170251)，我们都必须使用这个插值公式计算当前的半径值，并将其代入积分核中。任何简化处理，例如使用单元的平均半径，都会引入不一致性并降低精度 [@problem_id:2542359]。

此外，权重因子 $r(\xi, \eta)$ 的存在提高了被积函数的总多项式次数。对于一个双线性[四边形单元](@entry_id:176937)，如果待积函数（不含 $r$）在每个方向上的最高次数为 $k$，那么乘以线性的 $r(\xi, \eta)$ 后，被积函数在每个方向上的次数将变为 $k+1$。一个 $n$ 点的高斯积分规则能精确积分 $2n-1$ 次多项式。因此，为了精确积分，需要满足 $2n-1 \ge k+1$，即 $n \ge (k+2)/2$。这意味着[轴对称单元](@entry_id:163652)通常需要比相应的平面单元更高阶的积分规则才能达到相同的积分精度 [@problem_id:2542301]。

#### [对称轴](@entry_id:177299)附近的数值稳定性

尽管在对称轴上施加了 $u_r=0$ 的边界条件，但对于靠近[对称轴](@entry_id:177299)的单元，标准的有限元格式仍会遇到严重的数值问题。问题根源在于 $\mathbf{B}$ 矩阵中的 $1/r$ 项。当 $r \to 0$ 时，$\mathbf{B}$ 矩阵的某些项会趋于无穷。虽然刚度矩阵积分中的 $2\pi r$ 权重部分抵消了这种奇异性，但最终的被积函数 $\mathbf{B}^\mathsf{T} \mathbf{D} \mathbf{B} \cdot r$ 中仍然包含 $1/r$ 形式的项（因为 $\mathbf{B}^\mathsf{T} \mathbf{B}$ 中有 $1/r^2$ 的项），这使得积分在 $r \to 0$ 时仍然是奇异的。使用标准高斯积分计算这种[奇异积分](@entry_id:167381)会导致刚度矩阵的条件数急剧恶化，甚至产生错误的数值结果。

一个严谨且有效的解决方案是修改径向位移的插值[基函数](@entry_id:170178)，以先验地满足 $u_r(0,z)=0$ 的物理约束，并消除奇异性。具体做法是，令径向位移的近似形式为 $u_r(r,z) = r \cdot \tilde{u}_r(r,z)$，其中 $\tilde{u}_r$ 是用标准形函数插值的场。在这个新的近似下，[环向应变](@entry_id:174548)变为 $\varepsilon_{\theta\theta} = u_r/r = \tilde{u}_r$，这是一个非奇异的量。其他应变分量（如 $\varepsilon_{rr} = \tilde{u}_r + r \frac{\partial \tilde{u}_r}{\partial r}$）也都是非奇异的。这种**正则化[基函数](@entry_id:170178)**的方法从根本上移除了 $\mathbf{B}$ 矩阵中的 $1/r$ 项，使得刚度矩阵的被积函数在 $r=0$ 附近是良态的，从而大大改善了数值稳定性和计算精度 [@problem_id:2542325]。