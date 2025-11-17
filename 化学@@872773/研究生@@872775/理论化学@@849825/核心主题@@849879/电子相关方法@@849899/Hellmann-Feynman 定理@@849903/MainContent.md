## 引言
[赫尔曼-费曼定理](@entry_id:173798)是[理论化学](@entry_id:199050)和[量子物理学](@entry_id:137830)中的一块基石，它以其惊人的简洁性和深刻的物理内涵，为我们理解量子世界提供了一个强有力的分析工具。该定理的核心思想在于，它建立了一座桥梁，将一个量子体系的总能量对其[哈密顿量](@entry_id:172864)中某个连续参数的响应，与该[哈密顿量](@entry_id:172864)算符本身对该参数之导数的[量子力学期望值](@entry_id:155063)直接等同起来。这一关系的重要性在于，它常常能将一个看似复杂的能量求导问题，转化为一个更易于计算和物理解释的[期望值](@entry_id:153208)问题，从而使我们能够“窥探”到诸如[原子核](@entry_id:167902)上的力、分子的电学性质等关键物理量。

本文旨在系统性地剖析[赫尔曼-费曼定理](@entry_id:173798)。我们首先将追溯其根源，阐明其背后的问题：我们如何量化一个量子体系的能量如何随着其环境或内部结构参数的变化而变化？通过三章的篇幅，我们将带领读者从理论走向实践。第一章“原理与机制”将深入探讨该定理的严格推导、适用条件，以及在实际近似计算中遇到的关键挑战，如[普莱力](@entry_id:167194)的出现。第二章“应用与[交叉](@entry_id:147634)学科联系”将展示该定理的广泛威力，从计算[分子力](@entry_id:203760)到探测材料性质，再到其在凝聚态物理、核物理等前沿领域的应用。最后，在“动手实践”部分，我们将通过一系列精心设计的问题，将理论知识转化为可操作的计算技能。通过本次学习，您将对[赫尔曼-费曼定理](@entry_id:173798)建立起一个全面而深刻的理解。

## 原理与机制

在本章中，我们将深入探讨[赫尔曼-费曼定理](@entry_id:173798) (Hellmann-Feynman theorem) 的基本原理及其在[理论化学](@entry_id:199050)中的深远影响。该定理为我们提供了一个强大的工具，将量子体系能量对某个参数的响应，与[哈密顿量](@entry_id:172864)算符对该参数之导数的[期望值](@entry_id:153208)直接联系起来。我们将从其基本推导和适用条件出发，逐步揭示其在计算分子性质（如分子内作用力）时的核心作用与微妙之处，并最终展示其在[理论化学](@entry_id:199050)及相关科学领域的广泛应用。

### 基本定理：推导与条件

我们研究的核心问题是：对于一个受参数 $\lambda$ 调控的[哈密顿量](@entry_id:172864) $H(\lambda)$，其[能量本征值](@entry_id:144381) $E_n(\lambda)$ 如何随 $\lambda$ 的变化而改变？为了回答这个问题，我们考虑一个非简并的、归一化的[精确本征态](@entry_id:138620) $\ket{\psi_n(\lambda)}$，它满足定态薛定谔方程：
$$
H(\lambda)\ket{\psi_n(\lambda)} = E_n(\lambda)\ket{\psi_n(\lambda)}
$$
根据量子力学的基本假设，[能量本征值](@entry_id:144381) $E_n(\lambda)$ 可以通过[哈密顿量](@entry_id:172864)的[期望值](@entry_id:153208)计算得到：
$$
E_n(\lambda) = \bra{\psi_n(\lambda)} H(\lambda) \ket{\psi_n(\lambda)}
$$
为了求得能量对参数 $\lambda$ 的导数 $\frac{\mathrm{d}E_n}{\mathrm{d}\lambda}$，我们对上式应用乘法法则进行[微分](@entry_id:158718)：
$$
\frac{\mathrm{d}E_n}{\mathrm{d}\lambda} = \left( \frac{\mathrm{d}\bra{\psi_n}}{\mathrm{d}\lambda} \right) H \ket{\psi_n} + \bra{\psi_n} \frac{\partial H}{\partial \lambda} \ket{\psi_n} + \bra{\psi_n} H \left( \frac{\mathrm{d}\ket{\psi_n}}{\mathrm{d}\lambda} \right)
$$
此处为了简洁，我们暂时省略了对 $\lambda$ 的显式依赖。由于 $\ket{\psi_n}$ 是 $H$ 的[本征态](@entry_id:149904)，且 $H$ 是厄米算符（[能量本征值](@entry_id:144381) $E_n$ 为实数），我们有 $H\ket{\psi_n} = E_n\ket{\psi_n}$ 以及其共轭形式 $\bra{\psi_n}H = E_n\bra{\psi_n}$。将这两个关系代入上式，得到：
$$
\frac{\mathrm{d}E_n}{\mathrm{d}\lambda} = E_n \left( \frac{\mathrm{d}\bra{\psi_n}}{\mathrm{d}\lambda} \right) \ket{\psi_n} + \bra{\psi_n} \frac{\partial H}{\partial \lambda} \ket{\psi_n} + E_n \bra{\psi_n} \left( \frac{\mathrm{d}\ket{\psi_n}}{\mathrm{d}\lambda} \right)
$$
$$
\frac{\mathrm{d}E_n}{\mathrm{d}\lambda} = \bra{\psi_n} \frac{\partial H}{\partial \lambda} \ket{\psi_n} + E_n \left[ \left( \frac{\mathrm{d}\bra{\psi_n}}{\mathrm{d}\lambda} \right) \ket{\psi_n} + \bra{\psi_n} \left( \frac{\mathrm{d}\ket{\psi_n}}{\mathrm{d}\lambda} \right) \right]
$$
方括号中的项正是[波函数归一化](@entry_id:152806)[内积](@entry_id:158127) $\braket{\psi_n|\psi_n}$ 对 $\lambda$ 的导数。由于[波函数](@entry_id:147440)对于所有 $\lambda$ 值都保持归一化，即 $\braket{\psi_n(\lambda)|\psi_n(\lambda)} = 1$，其导数恒为零：
$$
\frac{\mathrm{d}}{\mathrm{d}\lambda}\braket{\psi_n|\psi_n} = \frac{\mathrm{d}}{\mathrm{d}\lambda}(1) = 0
$$
因此，包含[波函数](@entry_id:147440)导数的两项恰好相互抵消。这一抵消是整个推导过程的关键，它最终引出了[赫尔曼-费曼定理](@entry_id:173798)的简洁形式 [@problem_id:2814488] [@problem_id:2930790]：
$$
\frac{\mathrm{d}E_n}{\mathrm{d}\lambda} = \bra{\psi_n(\lambda)} \frac{\partial H}{\partial \lambda} \ket{\psi_n(\lambda)}
$$
该定理的深刻之处在于，它表明能量的[一阶导数](@entry_id:749425)可以通过对[哈密顿量](@entry_id:172864)算符的导数求[期望值](@entry_id:153208)得到，而**无需**计算复杂的[波函数](@entry_id:147440)导数项 $\frac{\mathrm{d}\ket{\psi_n}}{\mathrm{d}\lambda}$。

值得强调的是，这个优雅的公式成立需要满足几个严格的前提条件：
1.  **[精确本征态](@entry_id:138620)**：[波函数](@entry_id:147440) $\ket{\psi_n}$ 必须是[哈密顿量](@entry_id:172864) $H(\lambda)$ 的[精确本征态](@entry_id:138620)。这是确保 $H\ket{\psi_n}$ 可以被 $E_n\ket{\psi_n}$ 替换，从而使[波函数](@entry_id:147440)导数项能够被因子 $E_n$ 提出并最终抵消的关键。
2.  **非简并性**：所考虑的能级 $E_n$ 必须是非简并的。我们将在后续章节探讨简并情况下的修正。
3.  **参数无关的算符定义域**：此标准推导隐式地假设了算符的定义域或积分边界条件不依赖于参数 $\lambda$。如果边界条件随 $\lambda$ 变化（例如，盒子中粒子的盒长是参数 $\lambda$），则会产生额外的边界项 [@problem_id:2814488]。

### 定理的实践：近似[波函数](@entry_id:147440)与[普莱力](@entry_id:167194)

在实际的[量子化学](@entry_id:140193)计算中，我们几乎无法获得任何非平凡体系的[精确本征态](@entry_id:138620)。我们通常使用[变分法](@entry_id:163656)在有限[基组](@entry_id:160309)中得到的近似[波函数](@entry_id:147440)。[赫尔曼-费曼定理](@entry_id:173798)在这种情况下会发生什么变化呢？

#### 变分优化[波函数](@entry_id:147440)（广义[赫尔曼-费曼定理](@entry_id:173798)）

考虑一个近似[波函数](@entry_id:147440) $\ket{\Psi}$，它依赖于一组变分参数 $\{c_i\}$，这些参数被优化以最小化[能量泛函](@entry_id:170311) $E = \bra{\Psi}H\ket{\Psi}$。根据[变分原理](@entry_id:198028)，在能量最小值处，能量对所有变分参数的一阶导数均为零，即 $\frac{\partial E}{\partial c_i} = 0$。

现在，如果[哈密顿量](@entry_id:172864) $H(\lambda)$ 依赖于一个外部参数 $\lambda$，而**[基组](@entry_id:160309)本身不依赖于 $\lambda$**，那么能量 $E$ 的[全导数](@entry_id:137587)为：
$$
\frac{\mathrm{d}E}{\mathrm{d}\lambda} = \frac{\partial E}{\partial \lambda} + \sum_i \frac{\partial E}{\partial c_i} \frac{\mathrm{d}c_i}{\mathrm{d}\lambda}
$$
由于变分条件 $\frac{\partial E}{\partial c_i} = 0$，上式中的求和项为零。$\frac{\partial E}{\partial \lambda}$ 这一项是在固定[波函数](@entry_id:147440)参数 $\{c_i\}$ 的情况下对[能量泛函](@entry_id:170311)求导，这直接得到 $\bra{\Psi}\frac{\partial H}{\partial \lambda}\ket{\Psi}$。因此，对于在**参数无关[基组](@entry_id:160309)**中变分优化的[波函数](@entry_id:147440)，[赫尔曼-费曼定理](@entry_id:173798)的形式依然成立。这被称为**广义[赫尔曼-费曼定理](@entry_id:173798)** [@problem_id:2930790]。

#### 参数依赖[基组](@entry_id:160309)与[普莱力](@entry_id:167194)的起源

在[量子化学](@entry_id:140193)计算中，最常见的情况是[基函数](@entry_id:170178)本身就依赖于我们感兴趣的参数。一个典型的例子是原子中心[基组](@entry_id:160309)（如[高斯基组](@entry_id:198430)），其中[基函数](@entry_id:170178) $\chi_\mu(\mathbf{r} - \mathbf{R}_I)$ 的位置依赖于[原子核](@entry_id:167902)坐标 $\mathbf{R}_I$。当我们想计算[原子核](@entry_id:167902)上的力时，参数 $\lambda$ 就是某个核坐标分量。

在这种情况下，[波函数](@entry_id:147440) $\ket{\Psi(\lambda)} = \sum_\mu C_\mu(\lambda) \ket{\chi_\mu(\lambda)}$ 对 $\lambda$ 的依赖性有两个来源：变分系数 $C_\mu$ 的变化，以及[基函数](@entry_id:170178) $\chi_\mu$ 本身的变化。[波函数](@entry_id:147440)的[全导数](@entry_id:137587)可以分解为：
$$
\left\lvert \frac{\mathrm{d} \Psi}{\mathrm{d} \lambda} \right\rangle = \sum_{\mu} \frac{\mathrm{d} C_\mu}{\mathrm{d} \lambda}\lvert \chi_\mu \rangle + \sum_{\mu} C_\mu \left\lvert \frac{\mathrm{d} \chi_\mu}{\mathrm{d} \lambda} \right\rangle = \left\lvert \frac{\mathrm{d} \Psi}{\mathrm{d} \lambda} \right\rangle_{\text{coeff}} + \left\lvert \frac{\mathrm{d} \Psi}{\mathrmd \lambda} \right\rangle_{\text{basis}}
$$
正如我们前面所见，[能量导数](@entry_id:170468)中的额外项为 $2\,\mathrm{Re} \bra{\frac{\mathrm{d}\Psi}{\mathrm{d}\lambda}} H-E \ket{\Psi}$。由于变分条件保证了[残差向量](@entry_id:165091) $(H-E)\ket{\Psi}$ 与[基函数](@entry_id:170178)张成的空间正交，所以系数导数部分的贡献为零：$2\,\mathrm{Re} \bra{(\frac{\mathrm{d}\Psi}{\mathrm{d}\lambda})_\text{coeff}} H-E \ket{\Psi} = 0$。然而，[基函数](@entry_id:170178)导数 $\ket{\frac{\mathrm{d}\chi_\mu}{\mathrm{d}\lambda}}$ 通常位于基函数空间之外，因此其贡献不为零。这个非零的贡献项就是**[普莱力](@entry_id:167194) (Pulay force)** 或普莱项 [@problem_id:2814507]。
$$
F_{\text{Pulay}} = - 2\,\mathrm{Re} \left\langle \left(\frac{\mathrm{d} \Psi}{\mathrm{d} \lambda}\right)_{\text{basis}} \middle\vert H-E \middle\vert \Psi \right\rangle = - 2\,\mathrm{Re} \sum_\mu C_\mu^* \left\langle \frac{\mathrm{d} \chi_\mu}{\mathrmd \lambda} \middle\vert H-E \middle\vert \Psi \right\rangle
$$
[普莱力](@entry_id:167194)源于有限[基组](@entry_id:160309)的不完备性以及[基组](@entry_id:160309)对参数的显式依赖。

我们可以通过一个简单的思想实验来清晰地理解[普莱力](@entry_id:167194)的本质 [@problem_id:1406925]。考虑一个一维[非谐振子](@entry_id:142760)，其[哈密顿量](@entry_id:172864) $\hat{H}$ **不依赖**于任何参数 $\lambda$。现在，我们使用一个中心位于 $\lambda$ 的[高斯函数](@entry_id:261394) $\phi(x; \lambda)$ 作为变分[试探波函数](@entry_id:142892)来近似[基态能量](@entry_id:263704) $E(\lambda) = \bra{\phi(x; \lambda)} \hat{H} \ket{\phi(x; \lambda)}$。根据[赫尔曼-费曼定理](@entry_id:173798)，由于 $\frac{\partial \hat{H}}{\partial \lambda} = 0$，我们可能会错误地认为 $\frac{\mathrm{d}E}{\mathrm{d}\lambda}$ 永远为零。然而，直接计算表明 $\frac{\mathrm{d}E}{\mathrm{d}\lambda}$ 并不为零，除非势能是对称的且[高斯函数](@entry_id:261394)位于对称中心。这个非零的导数 $\frac{\mathrm{d}E}{\mathrmd\lambda}$ 完全来自于[基函数](@entry_id:170178)对 $\lambda$ 的依赖，它是一个纯粹的[普莱力](@entry_id:167194)。

这种区别在实践中至关重要。例如，在*ab initio*[分子动力学](@entry_id:147283)中，使用原子中心[基组](@entry_id:160309)（如[高斯基组](@entry_id:198430)）时，必须包含[普莱力](@entry_id:167194)才能得到正确的总力并确保[能量守恒](@entry_id:140514)。相反，如果使用[平面波基组](@entry_id:178287)，由于[基函数](@entry_id:170178)（形如 $e^{i\mathbf{G}\cdot\mathbf{r}}$）仅由模拟盒子定义，不随原子位置移动，因此不存在由[基组](@entry_id:160309)产生的[普莱力](@entry_id:167194) [@problem_id:2814480]。

### 应用一：分子力与[第一性原理分子动力学](@entry_id:138903)

[赫尔曼-费曼定理](@entry_id:173798)最直接和重要的应用之一是在玻恩-奥本海默 (Born-Oppenheimer, BO) 近似下计算[原子核](@entry_id:167902)上的力。在BO近似中，电子在一个由[原子核](@entry_id:167902)位置 $\mathbf{R}$ 固定的[势场](@entry_id:143025)中运动，其能量 $E(\mathbf{R})$ 成为[原子核](@entry_id:167902)运动的[势能面](@entry_id:147441)。作用在第 $I$ 个[原子核](@entry_id:167902)上的经典力定义为势能的负梯度：$\mathbf{F}_I = -\nabla_I E_{\text{BO}}(\mathbf{R})$。

总的BO能量 $E_{\text{BO}}(\mathbf{R})$ 是电子能量 $E_e(\mathbf{R})$ 和核-核排斥能 $E_{nn}(\mathbf{R})$ 之和。因此，力也分为两部分：
$$
\mathbf{F}_I = -\nabla_I E_e(\mathbf{R}) - \nabla_I E_{nn}(\mathbf{R})
$$
核-核排斥力 $-\nabla_I E_{nn}(\mathbf{R})$ 是一个简单的经典静电问题。电子部分的力 $-\nabla_I E_e(\mathbf{R})$ 则可以通过[赫尔曼-费曼定理](@entry_id:173798)计算。将参数 $\lambda$ 视为[原子核](@entry_id:167902)坐标分量 $R_{I\alpha}$，我们得到：
$$
F_{I\alpha, \text{elec}} = -\frac{\partial E_e}{\partial R_{I\alpha}} = -\bra{\Psi(\mathbf{R})} \frac{\partial \hat{H}_e(\mathbf{R})}{\partial R_{I\alpha}} \ket{\Psi(\mathbf{R})}
$$
这里 $\ket{\Psi(\mathbf{R})}$ 是[电子哈密顿量](@entry_id:177588) $\hat{H}_e(\mathbf{R})$ 的[精确本征态](@entry_id:138620) [@problem_id:2814501]。

Feynman本人对该定理给出了一个极为深刻的物理解释 [@problem_id:2814480]：**作用在[原子核](@entry_id:167902)上的力，就是在该[原子核](@entry_id:167902)处的经典[静电力](@entry_id:203379)，这个[静电力](@entry_id:203379)由体系中所有其他[原子核](@entry_id:167902)以及由量子力学决定的电子电荷密度[分布](@entry_id:182848)共同产生。** 算符 $\frac{\partial \hat{H}_e}{\partial R_{I\alpha}}$ 正是描述了当[原子核](@entry_id:167902) $I$ 移动时，电子-核吸引[势能](@entry_id:748988)的变化率，其[期望值](@entry_id:153208)就是作用在[原子核](@entry_id:167902) $I$ 上的[电场](@entry_id:194326)。

综上所述，对于使用参数依赖[基组](@entry_id:160309)的近似计算，作用在[原子核](@entry_id:167902)上的总力可以表示为三个部分的和：
**总力 = 赫尔曼-费曼项 + 普莱项 + 核-核排斥项**

精确计算这些力是进行[几何优化](@entry_id:151817)和[第一性原理分子动力学](@entry_id:138903)（AIMD）模拟的基础，它使得我们能够预测[分子结构](@entry_id:140109)、[反应路径](@entry_id:163735)以及材料的动态行为。

### 应用二：量子力学[维里定理](@entry_id:146441)

[赫尔曼-费曼定理](@entry_id:173798)的威力远不止于计算力。通过巧妙地选择参数 $\lambda$，它可以用来推导其他重要的物理关系。一个经典例子是量子力学[维里定理](@entry_id:146441)的推导 [@problem_id:1406881]。

考虑一个粒子在齐次势 $V(\mathbf{r})$ 中运动，[势函数](@entry_id:176105)满足 $V(\alpha \mathbf{r}) = \alpha^n V(\mathbf{r})$，其中 $n$ 是齐次次数。例如，对于[库仑势](@entry_id:154276)，$V \propto r^{-1}$，$n=-1$。我们构造一个含参[哈密顿量](@entry_id:172864) $H(\lambda) = T + V(\lambda \mathbf{r})$，其中 $T$ 是[动能算符](@entry_id:265633)。原始[哈密顿量](@entry_id:172864)对应于 $\lambda=1$。

我们可以通过两种不同途径计算[能量导数](@entry_id:170468) $\frac{\mathrm{d}E}{\mathrm{d}\lambda}|_{\lambda=1}$：

1.  **应用[赫尔曼-费曼定理](@entry_id:173798)**：
    $$
    \frac{\mathrm{d}E}{\mathrm{d}\lambda} = \left\langle \frac{\partial H}{\partial \lambda} \right\rangle = \left\langle \frac{\partial V(\lambda\mathbf{r})}{\partial \lambda} \right\rangle = \langle \mathbf{r} \cdot \nabla_\mathbf{x}V(\mathbf{x}) \rangle |_{\mathbf{x}=\lambda\mathbf{r}}
    $$
    根据[欧拉齐次函数定理](@entry_id:186434)，对于 $n$ 次齐次函数，我们有 $\mathbf{r} \cdot \nabla V(\mathbf{r}) = n V(\mathbf{r})$。因此，在 $\lambda=1$ 处：
    $$
    \left.\frac{\mathrm{d}E}{\mathrm{d}\lambda}\right|_{\lambda=1} = \langle nV \rangle = n\langle V \rangle
    $$

2.  **通过坐标缩放分析**：
    考虑一个坐标缩放变换。我们可以证明，$H(\lambda)$ 的[本征值](@entry_id:154894) $E(\lambda)$ 与另一个[哈密顿量](@entry_id:172864) $\lambda^2 T + V$ 的[本征值](@entry_id:154894)谱相同。对这个新[哈密顿量](@entry_id:172864)关于 $\lambda$ 应用[赫尔曼-费曼定理](@entry_id:173798)，我们得到：
    $$
    \frac{\mathrm{d}E}{\mathrm{d}\lambda} = \left\langle \frac{\partial}{\partial\lambda}(\lambda^2 T + V) \right\rangle = \langle 2\lambda T \rangle
    $$
    在 $\lambda=1$ 处，这给出：
    $$
    \left.\frac{\mathrm{d}E}{\mathrm{d}\lambda}\right|_{\lambda=1} = 2\langle T \rangle
    $$

联立以上两个结果，我们得到了量子力学[维里定理](@entry_id:146441)的普适形式：
$$
2\langle T \rangle = n\langle V \rangle
$$
对于束缚于库仑势 ($n=-1$) 的电子，我们得到了著名的 $2\langle T \rangle = -\langle V \rangle$ 或 $E = \langle T \rangle + \langle V \rangle = -\langle T \rangle = \frac{1}{2}\langle V \rangle$。这个例子完美地展示了[赫尔曼-费曼定理](@entry_id:173798)作为一个强大理论工具的灵活性和深刻性。

### 复杂情况与高等专题

#### 简并与能级交叉

[赫尔曼-费曼定理](@entry_id:173798)的标准形式要求所考虑的能级是非简并的。当在某个参数值 $\lambda_0$ 处出现[能量简并](@entry_id:203091)时，情况变得复杂 [@problem_id:2930729] [@problem_id:2814488]。

问题在于，在简并点，任何属于简并[子空间](@entry_id:150286)的态的[线性组合](@entry_id:154743)都是一个有效的[本征态](@entry_id:149904)。然而，只有一个特定的“正确”[基组](@entry_id:160309)能够平滑地演化为 $\lambda \ne \lambda_0$ 时的非简并[本征态](@entry_id:149904)。简单地在简并[子空间](@entry_id:150286)中任意选取一个态 $\ket{\phi}$ 并计算 $\bra{\phi} \frac{\partial H}{\partial \lambda} \ket{\phi}$ 通常会得到一个无物理意义的、错误的能量斜率。

正确的处理方法源于[简并微扰理论](@entry_id:143587)：我们必须在简ି[子空间](@entry_id:150286)内对微扰算符 $\frac{\partial H}{\partial \lambda}$ 进行[对角化](@entry_id:147016)。该微扰算符的矩阵表示为 $W_{ij} = \bra{\phi_i} \frac{\partial H}{\partial \lambda} \ket{\phi_j}$，其中 $\{\ket{\phi_i}\}$是简并[子空间](@entry_id:150286)的任意一组正交基。这个矩阵的[本征值](@entry_id:154894) $\{\epsilon_k\}$ 给出的是从简并点发出的各个能级分支的真实斜率，即 $\frac{\mathrm{d}E_k}{\mathrm{d}\lambda}|_{\lambda_0} = \epsilon_k$。相应的[本征向量](@entry_id:151813) $\ket{\chi_k}$ 则是正确的零阶[波函数](@entry_id:147440) [@problem_id:2930729]。

在能级[交叉点](@entry_id:147634)，例如分子[势能面](@entry_id:147441)上的[锥形交叉点](@entry_id:202598)，绝热能级 $E_n(\lambda)$ 作为 $\lambda$ 的函数通常是不可微的（形成一个“[尖点](@entry_id:636792)”）。然而，其左、右单边导数通常存在，并且各自满足[赫尔曼-费曼定理](@entry_id:173798) [@problem_id:2930729]。

#### 非[变分方法](@entry_id:163656)中的导数：Z-向量方法

在更高级的[后哈特里-福克](@entry_id:262486) (post-[Hartree-Fock](@entry_id:142303)) 方法中，例如[耦合簇理论](@entry_id:141746) (Coupled Cluster)，情况变得更加复杂。在这些方法中，计算得到的能量通常不是对所有[波函数](@entry_id:147440)参数（例如，[轨道](@entry_id:137151)旋转参数 $\boldsymbol{\kappa}$ 或簇幅 $\mathbf{c}$）都满足变分条件的 [@problem_id:2814479]。这意味着能量对这些参数的导数 $\frac{\partial E}{\partial \mathbf{p}}$ 不为零。

根据[链式法则](@entry_id:190743)，能量的[全导数](@entry_id:137587)包含一个不可忽略的参数响应项：
$$
\frac{\mathrm{d}E}{\mathrm{d}R_{\alpha}} = \frac{\partial E}{\partial R_{\alpha}} + \left(\frac{\partial E}{\partial \mathbf{p}}\right)^{\top} \frac{\mathrm{d}\mathbf{p}}{\mathrm{d}R_{\alpha}}
$$
直接求解参数响应 $\frac{\mathrm{d}\mathbf{p}}{\mathrmd R_{\alpha}}$ 需要求解一套复杂的[线性方程组](@entry_id:148943)，即耦合微扰方程（response equations）。

为了避免这个繁琐的步骤，现代[量子化学](@entry_id:140193)中采用了所谓的**Z-向量方法**。该方法引入[拉格朗日乘子](@entry_id:142696) $\mathbf{z}$ (即Z-向量)，构造一个[拉格朗日函数](@entry_id:174593) $\mathcal{L} = E + \mathbf{z}^\top \mathbf{f}$，其中 $\mathbf{f}(\mathbf{p}, \mathbf{R})=\mathbf{0}$ 是决定[波函数](@entry_id:147440)参数的[方程组](@entry_id:193238)。通过选择合适的 $\mathbf{z}$ 使得 $\mathcal{L}$ 对所有参数 $\mathbf{p}$ 都满足平稳条件 (stationary)，即 $\frac{\partial \mathcal{L}}{\partial \mathbf{p}} = \mathbf{0}$。这样一来，参数响应项就被巧妙地吸收了，总[能量导数](@entry_id:170468)可以简化为[拉格朗日函数](@entry_id:174593)对核坐标的[偏导数](@entry_id:146280)：
$$
\frac{\mathrm{d}E}{\mathrm{d}R_{\alpha}} = \frac{\partial \mathcal{L}}{\partial R_{\alpha}}
$$
这个最终的表达式看起来像一个“赫尔曼-费曼形式”的[期望值](@entry_id:153208)（加上普莱项），但其计算成本隐藏在求解Z-向量所必需的[线性响应](@entry_id:146180)方程（即一个伴随方程）之中 [@problem_id:2814479] [@problem_id:2814507]。这优雅地解决了非变分方法中计算解析梯度的难题。