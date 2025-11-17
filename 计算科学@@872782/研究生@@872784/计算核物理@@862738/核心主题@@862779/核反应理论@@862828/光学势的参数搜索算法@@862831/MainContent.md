## 引言
在[核物理](@entry_id:136661)研究中，[光学模型](@entry_id:161345)是一个极其成功的理论工具，它将复杂的[核子](@entry_id:158389)-[原子核](@entry_id:167902)多体散射问题简化为一个粒子在复数平均场（即[光学势](@entry_id:156352)）中的运动。尽[管模型](@entry_id:140303)概念上很简洁，但其真正的预测能力取决于[势函数](@entry_id:176105)中十几个甚至更多的参数。这些参数，如势深、半径和弥散度，并没有先验的精确值，必须通过将模型计算结果与高精度的实验数据（如弹性散射[微分截面](@entry_id:137333)）进行比较来仔细确定。这一过程本质上是一个复杂的[多维优化](@entry_id:147413)问题，即如何在庞大的[参数空间](@entry_id:178581)中找到一组“最佳”参数，使得理论与实验的差异最小化。这正是本文要解决的核心知识缺口：系统介绍并阐释用于执行这种高维、[非线性](@entry_id:637147)参数搜索的计算算法与统计策略。

本文旨在为读者提供一个关于[光学势](@entry_id:156352)参数[搜索算法](@entry_id:272182)的全面指南。在接下来的章节中，我们将分步展开：
- **原理与机制**：我们将深入探讨参数搜索的数学基础，从构建基于最小二乘法的卡方（χ²）[目标函数](@entry_id:267263)开始，详细讲解如[高斯-牛顿法](@entry_id:173233)和[Levenberg-Marquardt算法](@entry_id:172092)等核心局部优化器的工作原理，并分析[参数估计](@entry_id:139349)中的相关性挑战与[不确定性量化方法](@entry_id:756298)。
- **应用与交叉学科联系**：我们将展示这些算法如何应用于真实的物理问题，例如区分不同势分量、处理更复杂的非局域势，并探索贝叶斯推断、模型选择以及与机器学习等前沿领域的交叉。
- **动手实践**：最后，通过一系列精心设计的计算练习，你将有机会亲手实现和应用本章学到的关键概念，从而将理论知识转化为实践技能。

通过学习本文，你将不仅掌握参数搜索的“操作手册”，更将深刻理解其背后的统计原理和物理内涵，为你未来的[计算核物理](@entry_id:747629)研究打下坚实的基础。

## 原理与机制

本章在前一章介绍[光学模型](@entry_id:161345)基本概念的基础上，深入探讨其参数化、与实验数据的联系，以及用于确定这些参数的计算方法。我们将从构建描述散射过程的物理模型出发，系统地建立用于参数搜索的统计框架，详细阐述核心的局部[优化算法](@entry_id:147840)，分析[参数估计](@entry_id:139349)过程中遇到的关键挑战，并最终介绍如何量化和传播参数的不确定性。

### [光学势](@entry_id:156352)的物理内涵与[参数化](@entry_id:272587)

核反应理论中的[光学模型](@entry_id:161345)将复杂的[核子](@entry_id:158389)-原子[核[多体问](@entry_id:161400)题](@entry_id:138087)简化为一个[单体](@entry_id:136559)问题，其中入射[核子](@entry_id:158389)在一个复数平均场——即**[光学势](@entry_id:156352) (optical potential)** $U(\mathbf{r})$——中运动。该势通常表示为实部和虚部之和：$U(\mathbf{r}) = V(\mathbf{r}) + iW(\mathbf{r})$。

实部势 $V(\mathbf{r})$ 主要描述[弹性散射](@entry_id:152152)过程，即入射粒子在平均场中的形状[弹性散射](@entry_id:152152)。而虚部势 $W(\mathbf{r})$ 则扮演着一个至关重要的角色：它唯象地描述了从弹性通道到所有非弹性通道（如非弹性散射、[转移反应](@entry_id:159934)、俘获反应等）的粒子数损失。我们可以通过分析概率守恒来精确理解其物理意义。描述粒子运动的薛定谔方程为：
$$i\hbar \frac{\partial \psi}{\partial t} = \left( -\frac{\hbar^2}{2\mu}\nabla^2 + V(\mathbf{r}) + iW(\mathbf{r}) \right) \psi$$
其中 $\mu$ 是[约化质量](@entry_id:152420)。通过该方程及其[复共轭](@entry_id:174690)，可以推导出含[源项](@entry_id:269111)的概率密度[连续性方程](@entry_id:195013) [@problem_id:3578605]：
$$\frac{\partial \rho}{\partial t} + \nabla \cdot \mathbf{j} = \frac{2W(\mathbf{r})}{\hbar}\rho$$
其中 $\rho = |\psi|^2$ 是概率密度，$\mathbf{j}$ 是[概率流密度](@entry_id:152013)。当势为实数时（$W(\mathbf{r})=0$），该方程简化为标准的[概率守恒](@entry_id:149166)定律。然而，当 $W(\mathbf{r})$ 非零时，方程右边的项 $\frac{2W(\mathbf{r})}{\hbar}\rho$ 充当了[概率密度](@entry_id:175496)的源或汇。为了描述弹性通道中粒子数的净吸收，该项必须为负，这意味着在粒子存在的区域（$|\psi|^2 > 0$），必须有 $W(\mathbf{r}) \le 0$。因此，一个负的虚部势代表了从弹性通道到其他反应通道的通量损失。

在唯象[光学模型](@entry_id:161345)中，势的实部和虚部通常采用**伍兹-撒克逊 (Woods-Saxon)** 函数形式进行参数化，因为它能很好地模拟原子[核密度[分](@entry_id:752698)布](@entry_id:182848)的特征：中心区域近似恒定，表面区域则平滑过渡到零。一个典型的局域[中心势](@entry_id:148563)可以写成：
$$ U(r) = -V_0 f_{\text{WS}}(r; R_V, a_V) - i W_V f_{\text{WS}}(r; R_W, a_W) + 4ia_S W_S \frac{d}{dr}f_{\text{WS}}(r; R_S, a_S) + \dots $$
其中 $f_{\text{WS}}(r; R, a) = \left[1 + \exp\left(\frac{r-R}{a}\right)\right]^{-1}$ 是标准的伍兹-撒克逊[形状因子](@entry_id:152312)。这里的参数包括：
- **势深** ($V_0, W_V, W_S$)：决定势的强度，单位为 MeV。
- **半径** ($R$)：通常与核[质量数](@entry_id:142580) $A$ 相关，通过 $R = r_0 A^{1/3}$ 定义，其中 $r_0$ 是半径参数。
- **弥散度** ($a$)：描述核“表面”的厚度或模糊程度。

方程中的第一项是实部体势，第二项是虚部体吸收势，而第三项是虚部表面吸收势，其形式是伍茲-撒克遜形状的导数，使其峰值位于[原子核](@entry_id:167902)表面 [@problem_id:3578632]。这些参数（$V_0, r_0, a$ 等）通常是能量的函数，需要通[过拟合](@entry_id:139093)实验数据来确定。

这种唯象方法与**微观[光学势](@entry_id:156352) (microscopic optical potential)** 形成对比。后者试图从更基本的[核子](@entry_id:158389)-[核子](@entry_id:158389) (NN) 相互作用出发构建[光学势](@entry_id:156352)，例如通过将 NN 作用的 $g$-矩阵与靶核的密度[分布](@entry_id:182848)进行折叠。另一类是**弥散[光学模型](@entry_id:161345) (Dispersive Optical Model, DOM)**，它利用因果律所要求的[色散关系](@entry_id:140395)将不同能量下的实部势 $V(E)$ 和虚部势 $W(E)$ 联系起来。微观和弥散模型由于其更强的理论约束，通常具有较少的可调参数，但其参数的物理意义更明确 [@problem_id:3578610]。

### 从势到观测量：[散射截面](@entry_id:140322)的计算与敏感性

[光学势](@entry_id:156352)的参数最终必须通过与实验观测量（如弹性散射[微分截面](@entry_id:137333) $d\sigma/d\Omega$、总[反应截面](@entry_id:191218) $\sigma_R$ 等）的比较来确定。这些观测量是通过求解带有[光学势](@entry_id:156352)的薛定谔方程得到的。

[微分截面](@entry_id:137333) $d\sigma/d\Omega$ 对[光学势](@entry_id:156352)的形状非常敏感。在定性层面，我们可以借鉴[第一玻恩近似](@entry_id:201729)的观点，即散射振幅 $f(\theta)$ 近似为势 $U(r)$ 的[傅里叶变换](@entry_id:142120)。[截面](@entry_id:154995)中的衍射图样（极大值和极小值）直接反映了势的径向形状。具体来说 [@problem_id:3578632]：
- **半径参数 $r_0$**：增大 $r_0$ 会使[原子核](@entry_id:167902)的有效作用范围变大。根据[傅里叶变换](@entry_id:142120)的尺度不变性，空间域的拉伸对应于动量转移域的压缩。因此，增大 $r_0$ 会使衍射图样向更小的散射角（即更小的动量转移 $q = 2k \sin(\theta/2)$）移动。
- **弥散度参数 $a$**：增大 $a$ 使势的边缘变得更平滑、更模糊。一个更平滑的函数其[傅里叶变换](@entry_id:142120)在高频（大 $q$）部分会衰减得更快。因此，增大 $a$ 会抑制大角度的[振荡](@entry_id:267781)，使得衍射极小值变浅（被“填充”），对比度下降。

此外，不同的实验观测量[对势](@entry_id:753090)的不同部分敏感。例如，$d\sigma/d\Omega$ 主要对势的整体形状和表面区域敏感，而**总[反应截面](@entry_id:191218)** $\sigma_R$ 则直接与虚部势 $W(\mathbf{r})$ 相关。由[连续性方程](@entry_id:195013)可知，$\sigma_R$ 是对整个空间中概率吸收率的积分，可以表示为 [@problem_id:3578605]：
$$ \sigma_R = -\frac{2\mu}{\hbar^2 k} \int W(\mathbf{r})|\psi(\mathbf{r})|^2 d^3\mathbf{r} $$
这个积分约束为确定虚部势的大小和形状提供了至关重要的信息，有助于解决仅靠弹性散射数据无法解决的模糊性。

### 目标函数：从[最大似然](@entry_id:146147)到最小二乘

参数搜索的核心是定义一个**[目标函数](@entry_id:267263) (objective function)**，该函数量化了模型预测与实验数据之间的“不匹配”程度，然后通过[调整参数](@entry_id:756220)来最小化该函数。最常用和理论上最稳固的方法是**最大似然估计 (Maximum Likelihood Estimation, MLE)**。

假设我们有一组实验数据点 $\{y_i^{\text{exp}}\}$（例如在不同角度测得的[微分截面](@entry_id:137333)），其对应的[测量不确定度](@entry_id:202473)（标准差）为 $\{\sigma_i\}$。我们进一步假设[测量误差](@entry_id:270998)是独立的、无偏的，并服从[高斯分布](@entry_id:154414)。那么，对于给定的参数集 $\boldsymbol{p}$，模型预测值为 $y_i^{\text{th}}(\boldsymbol{p})$，第 $i$ 个数据点出现的概率（[似然](@entry_id:167119)）为：
$$ P(y_i^{\text{exp}}|\boldsymbol{p}) = \frac{1}{\sqrt{2\pi\sigma_i^2}} \exp\left( -\frac{(y_i^{\text{exp}} - y_i^{\text{th}}(\boldsymbol{p}))^2}{2\sigma_i^2} \right) $$
由于数据点是独立的，整个数据集的总[似然函数](@entry_id:141927)是各项概率的乘积。在实践中，我们通常最大化[对数似然函数](@entry_id:168593) $\ln L(\boldsymbol{p})$，这等价于最小化负[对数似然函数](@entry_id:168593) $-\ln L(\boldsymbol{p})$ [@problem_id:3578690]：
$$ -\ln L(\boldsymbol{p}) = \text{const} + \frac{1}{2} \sum_{i=1}^{N} \left( \frac{y_i^{\text{exp}} - y_i^{\text{th}}(\boldsymbol{p})}{\sigma_i} \right)^2 $$
忽略与参数 $\boldsymbol{p}$ 无关的常数项后，最小化[负对数似然](@entry_id:637801)就等价于最小化**卡方 ($\chi^2$) 函数**：
$$ \chi^2(\boldsymbol{p}) = \sum_{i=1}^{N} \left( \frac{y_i^{\text{exp}} - y_i^{\text{th}}(\boldsymbol{p})}{\sigma_i} \right)^2 $$
这就是**[加权最小二乘法](@entry_id:177517) (weighted least squares)** 的目标函数。每一项的权重为 $w_i = 1/\sigma_i^2$，即数据点的不确定度越小，其在拟合中的权重就越大。

如果[实验误差](@entry_id:143154)之间存在相关性，这一框架可以推广。此时，误差由一个协方差矩阵 $\mathbf{C}$ 描述，$\chi^2$ 函数变为 [@problem_id:3578690]：
$$ \chi^2(\boldsymbol{p}) = \boldsymbol{r}(\boldsymbol{p})^{\top} \mathbf{C}^{-1} \boldsymbol{r}(\boldsymbol{p}) $$
其中 $\boldsymbol{r}(\boldsymbol{p}) = \boldsymbol{y}^{\text{exp}} - \boldsymbol{y}^{\text{th}}(\boldsymbol{p})$ 是残差向量。

### 局部优化算法

一旦定义了 $\chi^2(\boldsymbol{p})$，参数搜索就变成了一个在多维[参数空间](@entry_id:178581)中寻找其最小值的[数值优化](@entry_id:138060)问题。由于[光学模型](@entry_id:161345)相对于其参数通常是高度[非线性](@entry_id:637147)的，我们需要[迭代算法](@entry_id:160288)来逐步逼近最小值。

#### [高斯-牛顿法](@entry_id:173233)

**[高斯-牛顿法](@entry_id:173233) (Gauss-Newton method)** 是求解[非线性](@entry_id:637147)[最小二乘问题](@entry_id:164198)的经典算法。其核心思想是在当前参数点 $\boldsymbol{p}_k$ 附近，用线性函数来近似模型预测，从而将[非线性](@entry_id:637147)问题转化为一系列线性[最小二乘问题](@entry_id:164198)。

定义[残差向量](@entry_id:165091) $\boldsymbol{r}(\boldsymbol{p})$，其分量为 $r_i(\boldsymbol{p}) = (y_i^{\text{th}}(\boldsymbol{p}) - y_i^{\text{exp}})/\sigma_i$。在当前点 $\boldsymbol{p}_k$ 附近对残差进行一阶[泰勒展开](@entry_id:145057)：
$$ \boldsymbol{r}(\boldsymbol{p}_k + \Delta\boldsymbol{p}) \approx \boldsymbol{r}(\boldsymbol{p}_k) + \boldsymbol{J}(\boldsymbol{p}_k) \Delta\boldsymbol{p} $$
其中 $\Delta\boldsymbol{p}$ 是待求的参数更新步长，$\boldsymbol{J}$ 是[残差向量](@entry_id:165091)的**雅可比矩阵 (Jacobian matrix)**，其元素为 $J_{ij} = \partial r_i / \partial p_j$。这个[雅可比矩阵](@entry_id:264467)也常被称为**敏感性矩阵 (sensitivity matrix)**，因为它量化了每个[可观测量](@entry_id:267133)对每个参数变化的敏感程度。

将此线性近似代入 $\chi^2$ 目标函数 $\chi^2 = \boldsymbol{r}^{\top}\boldsymbol{r}$，我们得到一个关于 $\Delta\boldsymbol{p}$ 的二次型。通过令该二次型对 $\Delta\boldsymbol{p}$ 的导数为零，可以求得使近似 $\chi^2$ 最小化的步长。这导出了[高斯-牛顿法](@entry_id:173233)的核心方程，即**[正规方程](@entry_id:142238) (normal equations)** [@problem_id:3578661]：
$$ (\boldsymbol{J}^{\top} \boldsymbol{W} \boldsymbol{J}) \Delta\boldsymbol{p} = -\boldsymbol{J}^{\top} \boldsymbol{W} \boldsymbol{r}_{\text{orig}} $$
此处为更通用的加权形式，$\boldsymbol{W}$ 是权重矩阵（对角阵元素为 $1/\sigma_i^2$），$\boldsymbol{r}_{\text{orig}}$ 是原始的物理[残差向量](@entry_id:165091) $y^{\text{th}}-y^{\text{exp}}$。求解这个[线性方程组](@entry_id:148943)，我们得到更新步长：
$$ \Delta\boldsymbol{p} = -(\boldsymbol{J}^{\top} \boldsymbol{W} \boldsymbol{J})^{-1} \boldsymbol{J}^{\top} \boldsymbol{W} \boldsymbol{r}_{\text{orig}} $$
通过迭代更新 $\boldsymbol{p}_{k+1} = \boldsymbol{p}_k + \Delta\boldsymbol{p}$，算法逐步收敛到 $\chi^2$ 的一个局部最小值。

[高斯-牛顿法](@entry_id:173233)实际上是用 $\boldsymbol{J}^{\top}\boldsymbol{W}\boldsymbol{J}$ 来近似 $\chi^2$ 函数的真实**海森矩阵 (Hessian matrix)**。这个近似在模型接近线性或残差很小的情况下是准确的。然而，当模型高度[非线性](@entry_id:637147)或[拟合质量](@entry_id:637026)差时，$\boldsymbol{J}^{\top}\boldsymbol{W}\boldsymbol{J}$ 可能奇异或病态，导致算法不稳定或发散。

#### [Levenberg-Marquardt算法](@entry_id:172092)

**Levenberg-Marquardt (LM) 算法** 是对[高斯-牛顿法](@entry_id:173233)的一个重要改进，它通过引入一个阻尼项来提高算法的稳定性和[全局收敛性](@entry_id:635436)。LM 算法修改了正规方程，将其变为 [@problem_id:3578627]：
$$ (\boldsymbol{J}^{\top} \boldsymbol{W} \boldsymbol{J} + \lambda \boldsymbol{D}) \Delta\boldsymbol{p} = -\boldsymbol{J}^{\top} \boldsymbol{W} \boldsymbol{r}_{\text{orig}} $$
其中 $\lambda$ 是一个非负的**阻尼参数 (damping parameter)**，$\boldsymbol{D}$ 通常是一个正定对角矩阵（例如，[单位矩阵](@entry_id:156724) $\boldsymbol{I}$ 或 $\boldsymbol{J}^{\top}\boldsymbol{W}\boldsymbol{J}$ 的对角部分）。

$\lambda$ 的作用是在两个极端之间插值：
- 当 $\lambda \to 0$ 时，LM 算法恢复为[高斯-牛顿法](@entry_id:173233)，利用其在最小值附近的快速二次收敛性。
- 当 $\lambda \to \infty$ 时，左侧的 $\lambda \boldsymbol{D}$ 项占主导，更新步长近似为 $\Delta\boldsymbol{p} \approx -\frac{1}{\lambda} \boldsymbol{D}^{-1} (\boldsymbol{J}^{\top}\boldsymbol{W}\boldsymbol{r}_{\text{orig}})$。这是一个沿着负梯度方向的短步长，即**最速下降法 (gradient descent)**，它保证了在远离最小值时也能使目标函数下降，尽管[收敛速度](@entry_id:636873)较慢。

LM 算法的精妙之处在于它能根据每一步的拟合效果自适应地调整 $\lambda$。这通过计算**增益比 (gain ratio)** $\rho$ 来实现：
$$ \rho = \frac{\text{实际下降量}}{\text{模型预测下降量}} = \frac{\chi^2(\boldsymbol{p}) - \chi^2(\boldsymbol{p}+\Delta\boldsymbol{p})}{m(\boldsymbol{0}) - m(\Delta\boldsymbol{p})} $$
其中分母是基于当前步长 $\Delta\boldsymbol{p}$ 的二次模型所预测的 $\chi^2$ 下降量。
- 如果 $\rho$ 接近 1，说明二次模型近似良好，可以接受当前步长并减小 $\lambda$，以期在下一步更接近[高斯-牛顿法](@entry_id:173233)。
- 如果 $\rho$ 是小的正数，说明模型近似较差，但仍有改进。可以接受步长但增大 $\lambda$，使下一步更保守。
- 如果 $\rho$ 为负数或非常小，说明当前步长导致 $\chi^2$ 上升，应拒绝此步，并显著增大 $\lambda$，以缩小搜索范围并更偏向梯度下降方向。

通过这种方式，LM 算法巧妙地结合了[高斯-牛顿法](@entry_id:173233)的速度和[最速下降法](@entry_id:140448)的稳定性，使其成为[非线性](@entry_id:637147)最小二乘问题的标准求解器之一。

### [参数估计](@entry_id:139349)中的挑战：[可辨识性](@entry_id:194150)与相关性

即使拥有强大的优化算法，参数搜索也常常面临固有的挑战，主要源于参数的**[可辨识性](@entry_id:194150) (identifiability)** 和**相关性 (correlation)**。

**结构可辨识性** 是一个理论概念，指的是在给定无噪声、完备的数据下，模型参数是否能被唯一确定。如果不同的参数组合能够产生完全相同的模型输出，那么这些参数就是结构上不可辨识的 [@problem_id:3578654]。**实践[可辨识性](@entry_id:194150)** 则更为重要，它关注在面对有限且有噪声的数据时，我们能在多大程度上精确地估计参数。

在[光学模型](@entry_id:161345)拟合中，常常出现某些参数组合的效应相似，导致它们难以被独立确定的情况。这种现象被称为**[参数相关性](@entry_id:274177)**或**模糊性 (ambiguity)**。
- 一个经典的例子是实部势深 $V_0$ 和半径参数 $r_0$ 之间的模糊性。在单一能量下，弹性散射主要[对势](@entry_id:753090)的**[体积分](@entry_id:171119) (volume integral)** $J_V = 4\pi \int V(r) r^2 dr$ 敏感。对于[伍兹-撒克逊势](@entry_id:756747)，[体积分](@entry_id:171119)近似正比于 $V_0 R^3 \propto V_0 r_0^3$ [@problem_id:3578654]。这意味着，同时增大 $r_0$ 并减小 $V_0$ 以保持 $V_0 r_0^3$ 近似不变，可以产生非常相似的[散射截面](@entry_id:140322)。
- 另一个例子是实部势深 $V$ 和虚部表面势强度 $W_s$ 之间的相关性，这在某些能量区域也很显著 [@problem_id:3578622]。

这种强相关性在 $\chi^2$ [曲面](@entry_id:267450)上表现为狭长、平坦的“山谷”。优化算法在这样的地形中难以导航，容易在山谷的陡峭两侧来回[振荡](@entry_id:267781)，而沿着谷底的平坦方向前进缓慢，导致收敛困难和数值不稳定 [@problem_id:3578622]。

从数学上看，参数强相关性意味着[雅可比矩阵](@entry_id:264467) $\boldsymbol{J}$ 的列向量（即不同参数的敏感性向量）近似[线性相关](@entry_id:185830)。这导致矩阵 $\boldsymbol{J}^{\top}\boldsymbol{W}\boldsymbol{J}$ 变得**病态 (ill-conditioned)**，即其最大和最小特征值之比（[条件数](@entry_id:145150)）非常大。求解病态的线性方程组对[数值误差](@entry_id:635587)非常敏感，使得参数解不稳定。

处理这些挑战的策略包括：
1.  **增加数据约束**：结合多种类型的实验数据可以打破参数简并。例如，同时拟合多个能量点的 $d\sigma/d\Omega$、总[反应截面](@entry_id:191218) $\sigma_R$、分析能力 $A_y$ 等自旋观测量 [@problem_id:3578605] [@problem_id:3578654]。对于弥散[光学模型](@entry_id:161345)，还可以将负能区的束缚态信息（如单粒子能级）纳入拟合，从而提供更强的约束 [@problem_id:3578610]。
2.  **重新[参数化](@entry_id:272587)**：选择一组关联性更低的参数进行拟合。例如，可以直接拟合[体积分](@entry_id:171119) $J_V$ 和[均方根半径](@entry_id:146552) $\langle r^2 \rangle^{1/2}$ 等矩，而不是原始的 $(V_0, r_0, a)$ [@problem_id:3578632]。
3.  **预处理/正则化**：在数值上，可以通过**[主成分分析](@entry_id:145395) (Principal Component Analysis, PCA)** 来识别参数的强相关组合。这等价于找到协方差矩阵（或[海森矩阵](@entry_id:139140)）的[特征向量](@entry_id:151813)，并转换到一个新的、解耦的参[数基](@entry_id:634389)底下进行优化。在这个新基底下，$\chi^2$ [曲面](@entry_id:267450)的等高线近似为正椭圆，使得优化过程更为高效 [@problem_id:3578622]。

### [参数不确定性](@entry_id:264387)的量化与传播

找到最佳拟合参数 $\boldsymbol{p}^*$ 只是任务的一半，同样重要的是评估这些参数的不确定性。这可以通过分析 $\chi^2$ [曲面](@entry_id:267450)在最小值附近的“曲率”来实现。

**费舍尔信息矩阵 (Fisher Information Matrix, FIM)** 是量化[参数不确定性](@entry_id:264387)的核心工具。在 MLE 框架和高斯误差假设下，FIM 可以直接通过雅可比矩阵计算得到 [@problem_id:3578697]：
$$ \boldsymbol{F} = \boldsymbol{J}^{\top} \boldsymbol{W} \boldsymbol{J} $$
请注意，这与[高斯-牛顿法](@entry_id:173233)中出现的矩阵完全相同。根据**[克拉默-拉奥下界](@entry_id:154412) (Cramér-Rao Lower Bound)** 理论，参数的协方差矩阵 $\boldsymbol{C}_p$ 的[逆矩阵](@entry_id:140380)即为费舍尔信息矩阵（在足够好的条件下近似成立）：
$$ \boldsymbol{C}_p \approx \boldsymbol{F}^{-1} = (\boldsymbol{J}^{\top} \boldsymbol{W} \boldsymbol{J})^{-1} $$
协方差矩阵 $\boldsymbol{C}_p$ 包含了关于[参数不确定性](@entry_id:264387)的全部信息：
- **对角元素** $(C_p)_{ii} = \sigma_{p_i}^2$ 是第 $i$ 个参数的[方差](@entry_id:200758)，其平方根 $\sigma_{p_i}$ 就是该参数的标准差（或“误差”）。
- **非对角元素** $(C_p)_{ij}$ 是参数 $p_i$ 和 $p_j$ 之间的协[方差](@entry_id:200758)，它度量了这两个参数的线性相关程度。
- **[相关系数](@entry_id:147037)矩阵** $\rho_{ij} = \frac{(C_p)_{ij}}{\sigma_{p_i} \sigma_{p_j}}$ 可以从[协方差矩阵](@entry_id:139155)导出，它提供了[标准化](@entry_id:637219)的相关性度量（取值在 -1 到 1 之间）。

一旦获得了参数的[协方差矩阵](@entry_id:139155) $\boldsymbol{C}_p$，我们就可以利用**线性[误差传播](@entry_id:147381) (linear error propagation)** 法则，来计算由这些[参数不确定性](@entry_id:264387)导致的任何其他物理量 $y$ 的不确定性。如果 $y$ 是参数 $\boldsymbol{p}$ 的一个函数 $y(\boldsymbol{p})$，其[方差](@entry_id:200758) $\sigma_y^2$ 可以通过一阶[泰勒展开](@entry_id:145057)近似为 [@problem_id:3578683]：
$$ \sigma_y^2 \approx \boldsymbol{g}^{\top} \boldsymbol{C}_p \boldsymbol{g} $$
其中 $\boldsymbol{g} = \nabla_{\boldsymbol{p}} y$ 是物理量 $y$ 对参数的敏感性向量（梯度），在最佳拟合点 $\boldsymbol{p}^*$ 处计算。

#### 一个计算示例

假设我们通过拟合得到了一个包含三个参数 $\boldsymbol{p}=(V, r_0, a)$ 的[光学势](@entry_id:156352)。在最佳拟合点，计算得到的费舍尔[信息矩阵](@entry_id:750640)为 [@problem_id:3578683]：
$$ \boldsymbol{F} = \begin{pmatrix} 0.050  0  0 \\ 0  3.00  -0.60 \\ 0  -0.60  0.90 \end{pmatrix} $$
首先，我们通过求逆计算参数协方差矩阵 $\boldsymbol{C}_p = \boldsymbol{F}^{-1}$。这是一个[块对角矩阵](@entry_id:145530)，可以分块求逆。
$$ \boldsymbol{C}_p = \begin{pmatrix} (0.050)^{-1}  0  0 \\ 0  \begin{pmatrix} 3.00  -0.60 \\ -0.60  0.90 \end{pmatrix}^{-1} \end{pmatrix} = \begin{pmatrix} 20.0  0  0 \\ 0  \frac{1}{2.34}\begin{pmatrix} 0.90  0.60 \\ 0.60  3.00 \end{pmatrix} \end{pmatrix} \approx \begin{pmatrix} 20.0  0  0 \\ 0  0.3846  0.2564 \\ 0  0.2564  1.2821 \end{pmatrix} $$
现在，我们想计算某个特定观测量（例如 $\theta=30^{\circ}$ 处的[微分截面](@entry_id:137333) $y$）的不确定度。假设我们已经计算出 $y$ 对参数的敏感性向量为：
$$ \boldsymbol{g} = \frac{\partial y}{\partial \boldsymbol{p}} = \begin{pmatrix} -0.15 \\ 8.00 \\ -3.00 \end{pmatrix} $$
利用[误差传播公式](@entry_id:275155)，该观测量的[方差](@entry_id:200758)为：
$$ \sigma_y^2 = \boldsymbol{g}^{\top} \boldsymbol{C}_p \boldsymbol{g} = \begin{pmatrix} -0.15  8.00  -3.00 \end{pmatrix} \begin{pmatrix} 20.0  0  0 \\ 0  0.3846  0.2564 \\ 0  0.2564  1.2821 \end{pmatrix} \begin{pmatrix} -0.15 \\ 8.00 \\ -3.00 \end{pmatrix} $$
经过计算，$\sigma_y^2 \approx 24.296$。因此，该观测量的不确定度（标准差）为 $\sigma_y = \sqrt{24.296} \approx 4.929$（单位与 $y$ 相同）。这个过程清晰地展示了如何从数据拟合得到的[参数不确定性](@entry_id:264387)，系统地传播到模型的任何预测值上。