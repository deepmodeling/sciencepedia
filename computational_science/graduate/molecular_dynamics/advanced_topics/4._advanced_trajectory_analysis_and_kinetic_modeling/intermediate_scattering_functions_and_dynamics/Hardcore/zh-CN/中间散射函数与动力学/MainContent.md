## 引言
在探索物质世界的奥秘时，理解其静态结构固然重要，但要真正把握物质的本质，我们必须深入其动态演化的核心。[静态结构因子](@entry_id:141682) $S(k)$ 描绘了原子或分子的空间[排列](@entry_id:136432)快照，然而，物质并非静止不动。粒子总是在不断运动、重组和弛豫，这些过程共同决定了材料的流动性、粘度、响应速度乃至[玻璃化](@entry_id:151669)等宏观性质。当前知识的空白在于如何建立一座从微观粒子瞬时运动到这些宏观动力学行为的桥梁。

本文旨在系统性地介绍填补这一空白的核心工具——**[中间散射函数](@entry_id:159928) (Intermediate Scattering Function, ISF)**。它是一种强大的时间关联函数，能够精确追踪特定空间尺度上的密度涨落是如何随[时间演化](@entry_id:153943)和衰减的。通过学习本文，读者将全面掌握ISF的理论与实践。

我们将分三个章节展开讨论。第一章“**原理与机制**”将从第一性原理出发，详细阐述ISF的定义、物理意义及其与均方位移等基本量之间的关系，并探讨[高斯近似](@entry_id:636047)、de Gennes窄化等基础模型。第二章“**应用与跨学科交叉**”将展示ISF在凝聚态物理、软物质和[材料科学](@entry_id:152226)等领域的广泛应用，揭示其如何用于研究[玻璃化转变](@entry_id:142461)、[高分子动力学](@entry_id:146985)以及[非平衡现象](@entry_id:198484)。最后，在“**动手实践**”部分，我们将通过具体的计算练习，指导读者如何从分子动力学模拟数据中提取ISF，并将其用于验证物理定律，从而将理论知识转化为实际的分析技能。

## 原理与机制

在深入探讨了液体和非晶态物质的静态结构之后，我们现在转向一个更具挑战性也更为丰富的主题：动力学。[静态结构因子](@entry_id:141682) $S(k)$ 揭示了粒子在空间中的平均排布，但它无法告诉我们这些结构是如何随[时间演化](@entry_id:153943)、重组或弛豫的。为了描述这些时间依赖的过程，我们需要引入一组新的工具，其核心是**[中间散射函数](@entry_id:159928) (Intermediate Scattering Function, ISF)**。本章将从第一性原理出发，系统地阐述[中间散射函数](@entry_id:159928)的定义、物理意义，以及它如何作为一座桥梁，连接微观粒子运动与宏观动力学性质。我们将探讨从简单的理想气体到复杂的[过冷液体](@entry_id:158222)和玻璃等不同系统中，ISF 所揭示的丰富动力学行为。

### 定义[散射函数](@entry_id:190527)：[密度关联](@entry_id:157860)的语言

研究动力学最自然也最强大的方法，是追踪系统密度在时间和空间上的起伏。一个系统的微观粒子[数密度](@entry_id:268986)场可以表示为在空间位置 $\mathbf{r}$ 和时间 $t$ 的狄拉克 $\delta$ 函数之和：
$$
\rho(\mathbf{r}, t) = \sum_{j=1}^{N} \delta(\mathbf{r} - \mathbf{r}_j(t))
$$
其中 $\mathbf{r}_j(t)$ 是第 $j$ 个粒子在时间 $t$ 的位置，系统共有 $N$ 个粒子。

在处理周期性系统（如[分子动力学模拟](@entry_id:160737)中常见的）或分析对特定长度尺度敏感的实验（如中子和[X射线散射](@entry_id:152296)）时，使用密度的[空间傅里叶变换](@entry_id:176346)，即**密度模式 (density mode)** $\hat{\rho}(\mathbf{k}, t)$，会更加便捷。对于给定的波矢 $\mathbf{k}$，其定义为：
$$
\hat{\rho}(\mathbf{k}, t) = \int_V e^{-i\mathbf{k} \cdot \mathbf{r}} \rho(\mathbf{r}, t) d\mathbf{r} = \sum_{j=1}^{N} e^{-i\mathbf{k} \cdot \mathbf{r}_j(t)}
$$
$\hat{\rho}(\mathbf{k}, t)$ 描述了系统中与波长 $\lambda = 2\pi/k$ (其中 $k=|\mathbf{k}|$) 相对应的密度波动的幅度和相位。

动力学的核心在于关联。一个在时间 $0$ 存在的密度起伏，在经过时间 $t$ 后还剩下多少？为了回答这个问题，我们定义了**[中间散射函数](@entry_id:159928)** $F(\mathbf{k}, t)$，它是密度模式的[时间自相关函数](@entry_id:145679)：
$$
F(\mathbf{k}, t) = \frac{1}{N} \langle \hat{\rho}(\mathbf{k}, t) \hat{\rho}(-\mathbf{k}, 0) \rangle
$$
其中尖括号 $\langle \cdot \rangle$ 表示系综平均。由于 $\mathbf{r}_j(t)$ 是实数，我们可以证明 $\hat{\rho}(-\mathbf{k}, t) = \hat{\rho}(\mathbf{k}, t)^*$，其中 $*$ 表示复共轭。因此，$F(\mathbf{k}, t)$ 也可以写为 $F(\mathbf{k}, t) = \frac{1}{N} \langle \hat{\rho}(\mathbf{k}, t) \hat{\rho}(\mathbf{k}, 0)^* \rangle$。此函数描述了具有[波矢](@entry_id:178620) $\mathbf{k}$ 的集体密度起伏随时间 $t$ 的弛豫过程。当 $t=0$ 时，该函数退化为[静态结构因子](@entry_id:141682) $S(\mathbf{k}) = F(\mathbf{k}, 0) = \frac{1}{N} \langle |\hat{\rho}(\mathbf{k}, 0)|^2 \rangle$。

为了更深入地理解微观运动，将 $F(\mathbf{k}, t)$ 分解为其**自部分 (self part)** 和**互异部分 (distinct part)** 是非常有益的 。
$$
F(\mathbf{k}, t) = \frac{1}{N} \left\langle \sum_{j=1}^{N} \sum_{l=1}^{N} e^{-i\mathbf{k} \cdot \mathbf{r}_j(t)} e^{i\mathbf{k} \cdot \mathbf{r}_l(0)} \right\rangle
$$
当 $j=l$ 时，我们得到**[自中间散射函数](@entry_id:754669) (self-intermediate scattering function)**, $F_s(\mathbf{k}, t)$，它只追踪同一个粒子在不同时间的关联：
$$
F_s(\mathbf{k}, t) = \frac{1}{N} \left\langle \sum_{j=1}^{N} e^{-i\mathbf{k} \cdot [\mathbf{r}_j(t) - \mathbf{r}_j(0)]} \right\rangle = \langle e^{-i\mathbf{k} \cdot \Delta\mathbf{r}(t)} \rangle
$$
上式中，由于所有粒子是全同的，我们对单个[代表性](@entry_id:204613)粒子的位移 $\Delta\mathbf{r}(t) = \mathbf{r}(t) - \mathbf{r}(0)$ 进行系综平均。$F_s(\mathbf{k}, t)$ 测量的是单个粒子运动如何导致其自身在 $t=0$ 时贡献的密度场相位因子 $e^{i\mathbf{k} \cdot \mathbf{r}(0)}$ 发生“去相位”(dephasing)。它[直接探测](@entry_id:748463)单粒子动力学。

当 $j \neq l$ 时，我们得到**互异[中间散射函数](@entry_id:159928) (distinct intermediate scattering function)**, $F_d(\mathbf{k}, t)$，它描述了不同粒子在不同时间的关联。因此，总的（或称相干的）[中间散射函数](@entry_id:159928)是这两部分的和：$F(\mathbf{k}, t) = F_s(\mathbf{k}, t) + F_d(\mathbf{k}, t)$。

### [高斯近似](@entry_id:636047)：一个基础模型

对于许多简单的动力学过程，粒子的位移[分布](@entry_id:182848)可以被一个[高斯分布](@entry_id:154414)很好地近似。这个**[高斯近似](@entry_id:636047) (Gaussian approximation)** 提供了一个强大而直观的框架来理解 $F_s(k,t)$  。

在一个各向同性的三维系统中，我们假设粒子位移 $\Delta\mathbf{r}(t)$ 的每个笛卡尔分量 $\Delta x, \Delta y, \Delta z$ 都是独立的、均值为零的高斯[随机变量](@entry_id:195330)，其[方差](@entry_id:200758)均为 $\sigma^2(t)$。$F_s(\mathbf{k}, t)$ 的定义式是一个[特征函数](@entry_id:186820)，利用高斯[随机变量](@entry_id:195330)的性质 $\langle e^{i\xi X} \rangle = e^{-\frac{1}{2}\xi^2 \langle X^2 \rangle}$，我们可以进行如下推导：
$$
F_s(\mathbf{k}, t) = \langle e^{i(k_x \Delta x + k_y \Delta y + k_z \Delta z)} \rangle = \langle e^{ik_x \Delta x} \rangle \langle e^{ik_y \Delta y} \rangle \langle e^{ik_z \Delta z} \rangle
$$
$$
F_s(\mathbf{k}, t) = e^{-\frac{1}{2} k_x^2 \sigma^2(t)} e^{-\frac{1}{2} k_y^2 \sigma^2(t)} e^{-\frac{1}{2} k_z^2 \sigma^2(t)} = e^{-\frac{1}{2} (k_x^2+k_y^2+k_z^2) \sigma^2(t)} = e^{-\frac{1}{2} k^2 \sigma^2(t)}
$$
系统的**[均方位移](@entry_id:159665) (mean-squared displacement, MSD)** $\langle \Delta r^2(t) \rangle$ 与各分量的[方差](@entry_id:200758)之间的关系为 $\langle \Delta r^2(t) \rangle = \langle \Delta x^2 \rangle + \langle \Delta y^2 \rangle + \langle \Delta z^2 \rangle = 3\sigma^2(t)$。因此，我们可以将分量[方差](@entry_id:200758)替换为可直接测量的均方位移：
$$
F_s(k, t) = \exp\left(-\frac{k^2 \langle \Delta r^2(t) \rangle}{6}\right)
$$
这个关系式是连接单粒子宏观[扩散](@entry_id:141445)行为（由 $\langle \Delta r^2(t) \rangle$ 体现）与微观[散射函数](@entry_id:190527)（由 $F_s(k,t)$ 体现）的核心桥梁。它表明，只要我们知道一个系统的[均方位移](@entry_id:159665)，并且[高斯近似](@entry_id:636047)成立，我们就可以预测其[自中间散射函数](@entry_id:754669)。

一个[高斯近似](@entry_id:636047)完全成立的例子是处在谐波[势阱](@entry_id:151413)中的经典粒子 。对于一个质量为 $m$ 的粒子在角频率为 $\omega$ 的三维各向同性[谐波](@entry_id:181533)势 $U(\mathbf{r}) = \frac{1}{2}m\omega^2\mathbf{r}^2$ 中运动，其运动方程的解为 $\mathbf{r}(t) = \mathbf{r}(0)\cos(\omega t) + \frac{\mathbf{v}(0)}{\omega}\sin(\omega t)$。在[正则系综](@entry_id:142391)中，初始位置 $\mathbf{r}(0)$ 和速度 $\mathbf{v}(0)$ 是独立的零均值[高斯变量](@entry_id:276673)。因此，位移 $\Delta\mathbf{r}(t) = \mathbf{r}(0)(\cos(\omega t) - 1) + \frac{\mathbf{v}(0)}{\omega}\sin(\omega t)$ 也是一个零均值[高斯变量](@entry_id:276673)。通过运用[能量均分定理](@entry_id:136972)计算其[方差](@entry_id:200758)，可以得到该体系精确的[自中间散射函数](@entry_id:754669)：
$$
F_s(k, t) = \exp\left(-\frac{k^2 k_B T}{m\omega^2} (1 - \cos(\omega t))\right)
$$
这精确地符合 $e^{-\frac{1}{2}\langle (\mathbf{k} \cdot \Delta\mathbf{r}(t))^2 \rangle}$ 的形式，验证了[高斯近似](@entry_id:636047)在该[线性系统](@entry_id:147850)中的精确性。

### 跨越时间尺度的动力学探测

[中间散射函数](@entry_id:159928)是一个强大的工具，因为它能够在不同时间尺度上揭示不同的物理过程。

#### 短时动力学：弹道运动与矩展开

在极短的时间尺度上，粒子尚未与邻居发生显著碰撞，其运动近似为匀速[直线运动](@entry_id:165142)，即**弹道运动 (ballistic motion)**。此时，$\Delta\mathbf{r}(t) \approx \mathbf{v}(0)t$，[均方位移](@entry_id:159665)为 $\langle \Delta r^2(t) \rangle = \langle v^2 \rangle t^2 = \frac{3k_B T}{m} t^2$。

研究短时行为的一个系统方法是进行[泰勒级数展开](@entry_id:138468)。由于平衡态动力学具有时间反演对称性，$F(\mathbf{k}, t)$ 是关于时间 $t$ 的偶函数，其展开式只包含 $t^2$ 的偶数次幂：
$$
F(k, t) = F(k, 0) + \frac{1}{2} \ddot{F}(k, 0) t^2 + \mathcal{O}(t^4)
$$
其中 $\ddot{F}(k,0)$ 是 $F(k,t)$ 在 $t=0$ 处的二阶时间导数。通过对 $F(k,t)$ 的定义式求导两次并利用[能量均分定理](@entry_id:136972)，可以推导出这个初始曲率的一个重要结果  ：
$$
\ddot{F}(k, 0) = -\frac{k^2 k_B T}{m}
$$
这个结果与相互作用势的具体形式无关，只依赖于质量和温度。现在，我们可以定义一个归一化[散射函数](@entry_id:190527) $\Phi(k,t) = F(k,t)/S(k)$ 的初始[弛豫率](@entry_id:150136)，即特征频率的平方 $\omega_k^2$：
$$
\omega_k^2 = - \frac{\ddot{\Phi}(k,0)}{\Phi(k,0)} = -\frac{\ddot{F}(k,0)}{F(k,0)} = \frac{k^2 k_B T}{m S(k)}
$$
这个关系被称为**德热纳窄化 (de Gennes narrowing)**。它揭示了一个深刻的物理现象：在[静态结构因子](@entry_id:141682) $S(k)$ 出现峰值的[波矢](@entry_id:178620)处（即系统存在显著空间有序性的地方），动力学弛豫会变慢（$\omega_k^2$ 变小）。这表明结构有序性会抑制相应尺度上的动力学起伏。

对于自部分 $F_s(k,t)$，由于 $F_s(k,0)=1$，其初始曲率直接为 $\ddot{F}_s(k,0) = -k^2 k_B T/m$。

#### 长时动力学：[扩散](@entry_id:141445)、遍历性与[玻璃化](@entry_id:151669)

在足够长的时间后，液体中的粒子经历了多次碰撞，其运动轨迹变为[随机游走](@entry_id:142620)，即**[扩散](@entry_id:141445)运动 (diffusive motion)**。此时，均方位移与时间成正比：$\langle \Delta r^2(t) \rangle = 6Dt$，其中 $D$ 是[扩散](@entry_id:141445)系数。在[高斯近似](@entry_id:636047)下，[自中间散射函数](@entry_id:754669)呈指数衰减：
$$
F_s(k,t) = \exp(-D k^2 t)
$$

对于液体而言，系统是**遍历的 (ergodic)**，这意味着在足够长的时间里，粒子可以探索所有可及的[构型空间](@entry_id:149531)。因此，任何初始的密度起伏（对于 $k \neq 0$）最终都会完全消失。这表现为：
$$
\lim_{t \to \infty} F(k, t) = 0 \quad (\text{对于液体})
$$

然而，当液体被快速冷却到其[玻璃化转变温度](@entry_id:152253) $T_g$ 以下时，系统会进入一个**玻璃态 (glassy state)**。在玻璃态中，粒子被其邻居形成的“笼子”所困，只能在平衡位置附近[振动](@entry_id:267781)，无法进行长程[扩散](@entry_id:141445)。系统的结构被“冻结”了。这种状态是**非遍历的 (non-ergodic)**，因为在实验或模拟的时间尺度内，系统无法探索整个相空间。这种动力学上的“逮捕” (arrest) 直接反映在[中间散射函数](@entry_id:159928)的长时行为上 。由于粒子被局域化，密度起伏不会完全衰减到一个零值，而是趋于一个有限的平台值。我们定义**非遍历性参数 (non-ergodicity parameter)** $f_k$ 为归一化ISF的长时极限：
$$
f_k = \lim_{t \to \infty} \frac{F(k, t)}{S(k)}
$$
对于玻璃态，在对应于粒子间主要距离的[波矢](@entry_id:178620) $k$ 处，$0  f_k  1$。这个非零的 $f_k$ 是玻璃态的一个关键动力学标志，它量化了在无限长时间后仍然“幸存”的弹性（或冻结）结构组分的比例。

### 玻璃形成液体的复杂动力学

[过冷液体](@entry_id:158222)在接近[玻璃化转变](@entry_id:142461)时表现出的动力学行为远比简单的弹道或[扩散](@entry_id:141445)运动复杂。[中间散射函数](@entry_id:159928)是揭示这种复杂性的关键。

#### [两步弛豫](@entry_id:756266)过程

在[过冷液体](@entry_id:158222)中，$F_s(k,t)$ 通常表现出一种特征性的**[两步弛豫](@entry_id:756266) (two-step relaxation)** 行为 。
1.  **短时 $\beta$ 弛豫**：在皮秒（$10^{-12}$ s）量级的时间内，$F_s(k,t)$ 快速下降。这对应于粒子在其邻居形成的“笼子”内的[振动](@entry_id:267781)和局域运动。
2.  **平台区 (Plateau)**：随后，函数进入一个近似的平台区。在这个时间尺度上，粒子被“笼子”暂时困住，其运动受到极大限制。平台的高度 $f_k^{(\beta)}$ 对应于粒子被局域化的程度，其值与非遍历性参数 $f_k$ 密切相关。
3.  **长时 $\alpha$ 弛豫**：在更长的时间尺度（$\tau_\alpha$，可以从纳秒到数小时甚至更长）后，笼子最终会发生重构，粒子得以“逃逸”并进行[结构重排](@entry_id:268377)。这导致 $F_s(k,t)$ 的第二次、通常是非指数形式的衰减，最终趋于零。这个过程被称为 **$\alpha$ 弛豫**，其时间尺度 $\tau_\alpha$ 定义了系统的[结构弛豫](@entry_id:263707)时间。

我们可以使用一个唯象的[均方位移](@entry_id:159665)模型来捕捉这些特征 。例如，一个包含弹道项、笼蔽项和[扩散](@entry_id:141445)项的MSD模型，通过[高斯近似](@entry_id:636047)，可以直接再现 $F_s(k,t)$ 的[两步弛豫](@entry_id:756266)形态，并允许我们定量地定义和提取如平台高度 $f_k^{(\beta)} = \exp(-k^2 r_{\text{loc}}^2)$（其中 $r_{\text{loc}}$ 是[局域化长度](@entry_id:146276)或笼子尺寸）以及 $\beta$ 和 $\alpha$ 弛豫时间等关键物理量。

#### 动力学非均匀性与非高斯行为

[高斯近似](@entry_id:636047)虽然是一个有用的起点，但它无法捕捉[过冷液体](@entry_id:158222)动力学的一个核心特征：**动力学非均匀性 (dynamical heterogeneity)**。这一现象指的是，在任何给定时刻，液体中不同区域的动力学速率可能存在巨大差异：一些区域的粒子像固体一样几乎不动（“冷”区），而另一些区域的粒子则高度活跃（“热”区）。

这种空间上的动力学涨落导致了粒子位移[分布](@entry_id:182848)偏离高斯分布。具体来说，少数“热”区中的粒子会发生远大于平均水平的位移，使得位移分布函数 $G_s(r,t)$ 在大 $r$ 处出现“肥尾”或指数尾，而不是[高斯函数](@entry_id:261394)的快速衰减 。

为了量化这种偏离，我们引入了**非高斯参数 (non-Gaussian parameter)** $\alpha_2(t)$ ：
$$
\alpha_2(t) = \frac{3 \langle \Delta r^4(t) \rangle}{5 \langle \Delta r^2(t) \rangle^2} - 1
$$
对于一个完美的三维高斯过程，$\langle \Delta r^4 \rangle = \frac{5}{3}\langle \Delta r^2 \rangle^2$，因此 $\alpha_2(t) \equiv 0$。在[过冷液体](@entry_id:158222)中，$\alpha_2(t)$ 在短时和长时都接近于零（因为弹道运动和[扩散](@entry_id:141445)运动都是近似高斯的），但在对应于 $\alpha$ [弛豫时间](@entry_id:191572)尺度的中间时刻会出现一个正的峰值。这个峰值的高度是衡量动力学非均匀性强弱的直接指标。

一个理解非高斯性起源的简单模型是考虑一个由两种不同[扩散](@entry_id:141445)速率的粒子组成的混合物  。即使每种粒子自身的运动是高斯的，整个体系的平均位移[分布](@entry_id:182848)也会是非高斯的，因为它是两个不同[方差](@entry_id:200758)的[高斯分布](@entry_id:154414)的加权和。在这种模型中，只要两种[扩散](@entry_id:141445)系数不同，计算得到的 $\alpha_2(t)$ 就会大于零。

非高斯行为也可以通过对 $F_s(k,t)$ 进行更精确的展开来捕捉。对 $\ln F_s(k,t)$ 进行**[累积量展开](@entry_id:141980) (cumulant expansion)** ，可以得到：
$$
\ln F_s(k,t) = -\frac{k^2}{6} \langle \Delta r^2(t) \rangle + \frac{k^4}{120} \langle \Delta r^4(t) \rangle_c + \mathcal{O}(k^6)
$$
其中，$\langle \Delta r^4(t) \rangle_c = \langle \Delta r^4(t) \rangle - \frac{5}{3}\langle \Delta r^2(t) \rangle^2$ 是四阶关联径向矩，它正比于非高斯参数 $\alpha_2(t)$。这个展开式表明，[高斯近似](@entry_id:636047)实际上是[累积量展开](@entry_id:141980)的第一项，而非高斯效应则表现为 $k^4$ 及更高阶的修正项。

### 从[分子动力学轨迹](@entry_id:752118)计算[散射函数](@entry_id:190527)

理论概念最终需要通过实验或模拟来验证和应用。[分子动力学](@entry_id:147283) (MD) 模拟为我们提供了计算[中间散射函数](@entry_id:159928)所需的全部微观信息——即所有粒子随时间演化的轨迹 $\{\mathbf{r}_j(t)\}$。

计算过程严格遵循其定义 。假设我们有一系列时间快照下的粒子坐标。

1.  **计算相干[中间散射函数](@entry_id:159928) $F(k,t)$**：
    *   首先，为每个时间快照 $t_m$ 和给定的波矢 $\mathbf{k}$，计算密度模式 $\hat{\rho}(\mathbf{k}, t_m) = \sum_{j=1}^{N} e^{-i\mathbf{k} \cdot \mathbf{r}_j(t_m)}$。在周期性边界条件 (PBC) 的模拟盒子中，[波矢](@entry_id:178620) $\mathbf{k}$ 必须与盒子尺寸 $L$ 相容，例如对于立方盒子，$\mathbf{k} = \frac{2\pi}{L}(n_x, n_y, n_z)$，其中 $n_x, n_y, n_z$ 为整数。
    *   然后，通过计算密度模式的自相关来得到 $F(\mathbf{k}, \Delta t)$。这通常通过对所有可能的时间起点 $t_m$ 进行平均来提高统计精度：
      $$
      F(\mathbf{k}, \Delta t) \approx \frac{1}{N} \frac{1}{M-\Delta m} \sum_{m=0}^{M-\Delta m-1} \hat{\rho}(\mathbf{k}, t_{m+\Delta m}) \hat{\rho}(-\mathbf{k}, t_m)
      $$
      其中 $\Delta t = \Delta m \cdot \delta t$，$\delta t$ 是模拟的时间步长。
    *   通常会将其除以 $F(\mathbf{k},0)=S(\mathbf{k})$ 进行归一化。

2.  **计算[自中间散射函数](@entry_id:754669) $F_s(k,t)$**：
    *   对于每个粒子 $j$ 和时间间隔 $\Delta t$，计算其[位移矢量](@entry_id:262782) $\Delta\mathbf{r}_j = \mathbf{r}_j(t_m+\Delta t) - \mathbf{r}_j(t_m)$。
    *   在处理周期性边界条件时，一个至关重要的步骤是应用**[最小镜像约定](@entry_id:142070) (Minimum Image Convention, MIC)**。如果一个粒子穿过了模拟盒子的边界，其原始位移可能非常大。MIC 通过将位移的每个分量“折叠”回 $[-L/2, L/2]$ 区间来修正这一点，从而得到真实的物理位移。例如，对于 $x$ 分量，修正后的位移为 $\Delta x' = \Delta x - L \cdot \text{round}(\Delta x / L)$。
    *   计算每个粒子修正后位移的相位因子 $e^{-i\mathbf{k} \cdot \Delta\mathbf{r}_j'}$。
    *   最后，对所有粒子和所有时间起点进行平均：
      $$
      F_s(\mathbf{k}, \Delta t) \approx \left\langle \frac{1}{N} \sum_{j=1}^{N} e^{-i\mathbf{k} \cdot \Delta\mathbf{r}_j'(\Delta t)} \right\rangle_{\text{time origins}}
      $$

一个值得注意的特例是 $\mathbf{k}=0$。此时，$e^{-i\mathbf{k}\cdot\mathbf{r}}=1$，因此 $\hat{\rho}(\mathbf{0}, t) = N$。这意味着 $F(0,t) = \frac{1}{N} \langle N \cdot N \rangle = N$，反映了系统总粒子数守恒。类似地，$F_s(0,t)=1$。

通过这些计算，我们可以将模拟产生的海量原子轨迹数据，转化为能够在理论和实验之间进行直接比较的、蕴含丰富动力学信息的[中间散射函数](@entry_id:159928)。