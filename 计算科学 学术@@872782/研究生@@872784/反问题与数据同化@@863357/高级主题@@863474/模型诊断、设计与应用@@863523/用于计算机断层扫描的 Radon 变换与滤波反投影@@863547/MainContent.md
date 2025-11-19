## 引言
[计算机断层扫描](@entry_id:747638)（Computed Tomography, CT）技术彻底改变了[医学诊断](@entry_id:169766)和[无损检测](@entry_id:273209)，其核心在于一个精妙的数学逆问题：如何从一系列穿过物体的[X射线](@entry_id:187649)投影数据中，精确地重建出其内部的二维或三维结构图像。这一过程不仅是工程技术的壮举，更是[应用数学](@entry_id:170283)理论的辉煌胜利。长期以来，滤波[反投影](@entry_id:746638)（Filtered Back-Projection, FBP）算法作为解决这一问题的经典方法，以其高效性和精确性在临床和工业领域占据主导地位。

然而，理解FBP算法远不止于掌握一个计算流程。它涉及对[数据采集](@entry_id:273490)物理过程的深刻洞察、对[傅里叶分析](@entry_id:137640)的巧妙运用，以及对算法在真实世界中局限性的清醒认识。本文旨在系统性地剖析[Radon变换](@entry_id:754021)与FBP算法的完整理论体系与应用[范式](@entry_id:161181)，填补纯理论推导与实际工程应用之间的知识鸿沟。

本文将通过以下三个章节，引领读者逐步深入这一领域：
*   **第一章：原理与机制**，将从[X射线](@entry_id:187649)衰减的物理模型出发，建立[Radon变换](@entry_id:754021)的数学框架，并详细推导FBP算法的核心——[傅里叶切片定理](@entry_id:192235)与[斜坡滤波器](@entry_id:754034)，最后探讨实际应用中的离散化与扩展问题。
*   **第二章：应用与跨学科联系**，将展示FBP如何作为分析工具来评估CT系统性能（如分辨率与噪声），并阐明其与统计学、优化理论及现代迭代重建方法（MBIR）的深刻联系，揭示其作为连接经典与现代方法的桥梁作用。
*   **第三章：动手实践**，将提供一系列编程练习，引导读者亲手实现前向/反投影算子、分析[噪声传播](@entry_id:266175)，并探索FBP与迭代算法的关系，将理论知识转化为实践能力。

通过这一结构化的学习路径，读者不仅将掌握FBP的“如何做”，更将深刻理解其“为什么”，为进一步研究高级成像技术和解决复杂的[逆问题](@entry_id:143129)奠定坚实的数学与工程基础。

## 原理与机制

本章旨在系统性地阐述[计算机断层扫描](@entry_id:747638)（Computed Tomography, CT）中[图像重建](@entry_id:166790)的核心数学原理与机制。我们将从[数据采集](@entry_id:273490)的物理模型出发，建立其数学抽象——[Radon变换](@entry_id:754021)，然后重点剖析从投影数据中恢[复图](@entry_id:199480)像的[逆问题](@entry_id:143129)求解方法，即滤波[反投影](@entry_id:746638)（Filtered Back-Projection, FBP）算法。我们将不仅推导其理论基础，还将探讨其实际应用中的离散化、[采样策略](@entry_id:188482)以及对更复杂采集几何的扩展。

### 前向问题：[数据采集](@entry_id:273490)的数学模型

[CT重建](@entry_id:747640)的起点是理解[X射线](@entry_id:187649)穿过物体时其强度的衰减过程。这一物理过程为我们提供了重建所需的数据，即投影。

#### [X射线](@entry_id:187649)衰减的物理模型与投影数据

当一束具有特定能量$E$的[X射线](@entry_id:187649)[光子](@entry_id:145192)穿过一个二维物体时，其强度$I$会根据**[比尔-朗伯定律](@entry_id:192870)**（Beer–Lambert law）发生指数衰减。若光束沿直线路径$\gamma$传播，其出射强度$I$与入射强度$I_{in}$的关系为：
$$ I = I_{in} \exp\left(-\int_{\gamma} \mu(\mathbf{x}, E) \, \mathrm{d}\ell\right) $$
其中，$\mu(\mathbf{x}, E)$是物体在空间位置$\mathbf{x}$处对能量为$E$的[光子](@entry_id:145192)的**[线性衰减](@entry_id:198935)系数**，它是待重建的物理量。

在理想的CT模型中，我们希望测量到的是衰减系数沿路径$\gamma$的[线积分](@entry_id:141417)，即$\int_{\gamma} \mu(\mathbf{x}, E) \, \mathrm{d}\ell$。通过对上式取对数，我们可以得到：
$$ -\ln\left(\frac{I}{I_{in}}\right) = \int_{\gamma} \mu(\mathbf{x}, E) \, \mathrm{d}\ell $$
$I_{in}$通常通过一次没有放置物体的“空气扫描”（air scan）来标定。

然而，实际的CT系统面临两个主要挑战。首先，[X射线源](@entry_id:268482)通常是**[多谱](@entry_id:200847)段**（polyenergetic）的，即它会发射一个能量范围内的[光子](@entry_id:145192)。由于衰减系数$\mu$依赖于能量$E$，探测器测得的总强度是所有能量分量的积分。取对数操作与[能量积分](@entry_id:166228)操作不可交换，这导致对数处理后的数据不再是任何单一[标量场](@entry_id:151443)的精确[线积分](@entry_id:141417)。这种效应被称为**束流硬化**（beam hardening），因为它会导致低能量[光子](@entry_id:145192)被优先吸收，从而使得穿过物体的[X射线](@entry_id:187649)束的[平均能量](@entry_id:145892)“变硬”[@problem_id:3416054]。其次，[X射线](@entry_id:187649)与物质的相互作用还会产生**散射**（scatter），这会给探测器读数增加一个与路径积分无直接关系的背景信号。

为了建立一个可解的数学模型，我们首先考虑一个理想化的情景：[X射线源](@entry_id:268482)是**单色**（monochromatic）的（能量为$E_0$），且散射可以忽略不计。在这种情况下，对数处理后的测量数据$p_{\gamma}$精确地等于物体在$E_0$能量下的衰减系数$\mu(\mathbf{x}, E_0)$沿路径$\gamma$的线积分。令$f(\mathbf{x}) = \mu(\mathbf{x}, E_0)$，则有：
$$ p_{\gamma} = \int_{\gamma} f(\mathbf{x}) \, \mathrm{d}\ell $$
这正是**[X射线](@entry_id:187649)变换**（X-ray Transform）的定义，在二维情况下，它等同于[Radon变换](@entry_id:754021)。尽管现实世界更为复杂，例如需要通过物质分解模型和校正算法来处理[多谱](@entry_id:200847)段效应[@problem_id:3416054]，但这个理想化的模型构成了经典FBP算法的基石。

#### [Radon变换](@entry_id:754021)

**[Radon变换](@entry_id:754021)**（Radon transform）为CT中的投影采集过程提供了严谨的数学框架。在二维平行束采集中，一条直线可以由其[法向量](@entry_id:264185)方向$\theta \in [0, \pi)$和该直线到坐标原点的有符号距离$s \in \mathbb{R}$唯一确定。这条直线上的点$\mathbf{x}=(x_1, x_2)$满足方程$\mathbf{x} \cdot \mathbf{n}(\theta) = s$，其中$\mathbf{n}(\theta) = (\cos\theta, \sin\theta)$是[单位法向量](@entry_id:178851)。

二维[Radon变换](@entry_id:754021)$\mathcal{R}f$将一个定义在$\mathbb{R}^2$上的函数$f(\mathbf{x})$映射为其在所有直线上的积分。其定义如下：
$$ (\mathcal{R}f)(\theta, s) = \int_{\mathbf{x} \cdot \mathbf{n}(\theta) = s} f(\mathbf{x}) \, \mathrm{d}\ell $$
其中$\mathrm{d}\ell$是沿该直线的[线元](@entry_id:196833)。所有这些[线积分](@entry_id:141417)的集合$(\mathcal{R}f)(\theta, s)$构成了一个定义在[参数空间](@entry_id:178581)$(\theta, s)$上的函数，称为**[正弦图](@entry_id:754926)**（sinogram）。

[Radon变换](@entry_id:754021)有一个等价且在理论分析中极为有用的表示形式，即利用**狄拉克$\delta$[分布](@entry_id:182848)**（Dirac delta distribution）[@problem_id:3416053]。$\delta$函数的作用是从积分中“筛选”出满足特定条件的点。[Radon变换](@entry_id:754021)可以写成一个在整个$\mathbb{R}^2$平面上的积分：
$$ (\mathcal{R}f)(\theta, s) = \int_{\mathbb{R}^2} f(\mathbf{x}) \, \delta(s - \mathbf{x} \cdot \mathbf{n}(\theta)) \, \mathrm{d}\mathbf{x} $$
这里，$\delta(s - \mathbf{x} \cdot \mathbf{n}(\theta))$确保了只有当点$\mathbf{x}$位于直线$\mathbf{x} \cdot \mathbf{n}(\theta) = s$上时，被积函数才非零。

[正弦图](@entry_id:754926)具有一个重要的几何对称性。将[法向量](@entry_id:264185)旋转$\pi$（即$\theta \to \theta + \pi$）并同时反转距离符号（$s \to -s$），所描述的是同一条直线。因此，它们的线积分值必然相等：
$$ (\mathcal{R}f)(\theta + \pi, s) = (\mathcal{R}f)(\theta, -s) $$
这个性质意味着，为了避免[数据冗余](@entry_id:187031)，我们只需在$\theta \in [0, \pi)$和$s \in \mathbb{R}$的参[数域](@entry_id:155558)内采集投影数据即可唯一地表示所有穿过物体的直线[@problem_id:3416053]。

### [逆问题](@entry_id:143129)：从投影重建图像

[CT重建](@entry_id:747640)的核心任务是从测量的[正弦图](@entry_id:754926)$(\mathcal{R}f)(\theta, s)$出发，求解原始的二维函数$f(\mathbf{x})$。这是一个典型的**逆问题**。滤波[反投影](@entry_id:746638)算法正是解决这一逆问题的经典方法。

#### [傅里叶切片定理](@entry_id:192235)

连接测量数据（[正弦图](@entry_id:754926)）与待重建图像（$f(\mathbf{x})$）的关键桥梁是**[傅里叶切片定理](@entry_id:192235)**（Fourier Slice Theorem）。该定理指出，一个投影的一维[傅里叶变换](@entry_id:142120)等于[原始图](@entry_id:262918)像的[二维傅里叶变换](@entry_id:273583)在一条穿过原点的“切片”上的值。

让我们来推导这一定理。令$\hat{p}(\theta, \omega)$为投影$p(\theta, s) = (\mathcal{R}f)(\theta, s)$关于变量$s$的一维[傅里叶变换](@entry_id:142120)：
$$ \hat{p}(\theta, \omega) = \int_{-\infty}^{\infty} p(\theta, s) e^{-i\omega s} \, \mathrm{d}s $$
使用[Radon变换](@entry_id:754021)的$\delta$[分布](@entry_id:182848)形式代入$p(\theta, s)$：
$$ \hat{p}(\theta, \omega) = \int_{-\infty}^{\infty} \left( \int_{\mathbb{R}^2} f(\mathbf{x}) \delta(s - \mathbf{x} \cdot \mathbf{n}(\theta)) \, \mathrm{d}\mathbf{x} \right) e^{-i\omega s} \, \mathrm{d}s $$
[交换积分次序](@entry_id:200463)（这对于性质良好的函数是允许的）：
$$ \hat{p}(\theta, \omega) = \int_{\mathbb{R}^2} f(\mathbf{x}) \left( \int_{-\infty}^{\infty} \delta(s - \mathbf{x} \cdot \mathbf{n}(\theta)) e^{-i\omega s} \, \mathrm{d}s \right) \, \mathrm{d}\mathbf{x} $$
内部关于$s$的积分可利用$\delta$函数的[筛选性质](@entry_id:265662)求解，结果为$e^{-i\omega (\mathbf{x} \cdot \mathbf{n}(\theta))}$。于是：
$$ \hat{p}(\theta, \omega) = \int_{\mathbb{R}^2} f(\mathbf{x}) e^{-i\mathbf{x} \cdot (\omega \mathbf{n}(\theta))} \, \mathrm{d}\mathbf{x} $$
上式右侧正是$f(\mathbf{x})$的[二维傅里叶变换](@entry_id:273583)$\hat{f}(\boldsymbol{\xi})$在[频域](@entry_id:160070)向量$\boldsymbol{\xi} = \omega \mathbf{n}(\theta)$处的取值。$\boldsymbol{\xi} = \omega \mathbf{n}(\theta)$描述了一条穿过傅里叶空间原点、方向与[投影法](@entry_id:144836)向量方向$\theta$一致、频率大小为$|\omega|$的径向线。因此，我们得到了[傅里叶切片定理](@entry_id:192235)[@problem_id:3416052]：
$$ \hat{p}(\theta, \omega) = \hat{f}(\omega \mathbf{n}(\theta)) $$

#### 傅里叶域反演与[斜坡滤波器](@entry_id:754034)

[傅里叶切片定理](@entry_id:192235)似乎提供了一个直接的重建策略：
1.  对每个角度$\theta$的投影$p(\theta, s)$做一维[傅里叶变换](@entry_id:142120)，得到$\hat{p}(\theta, \omega)$。
2.  根据定理，将这些$\hat{p}(\theta, \omega)$的值填充到二维[傅里叶平面](@entry_id:172317)的相应极坐标位置$(\omega, \theta)$上，从而获得$\hat{f}(\boldsymbol{\xi})$的采样。
3.  对填充好的二维傅里叶空间数据执行二维[逆傅里叶变换](@entry_id:178300)，得到$f(\mathbf{x})$。

然而，这一策略存在一个严重问题。二维逆傅里叶变换的公式为：
$$ f(\mathbf{x}) = \frac{1}{(2\pi)^2} \int_{\mathbb{R}^2} \hat{f}(\boldsymbol{\xi}) e^{i\mathbf{x} \cdot \boldsymbol{\xi}} \, \mathrm{d}\boldsymbol{\xi} $$
若我们在极坐标$(\omega, \theta)$下计算此积分，面积微元$\mathrm{d}\boldsymbol{\xi}$变为$|\omega| \, \mathrm{d}\omega \, \mathrm{d}\theta$。于是，反演公式写作：
$$ f(\mathbf{x}) = \frac{1}{(2\pi)^2} \int_{0}^{2\pi} \int_{0}^{\infty} \hat{f}(\omega \mathbf{n}(\theta)) e^{i\mathbf{x} \cdot (\omega \mathbf{n}(\theta))} |\omega| \, \mathrm{d}\omega \, \mathrm{d}\theta $$
（考虑到对称性，积分区间可以调整）。关键在于$|\omega|$这一项。它表明，直接将投影的[傅里叶变换](@entry_id:142120)值填充到[傅里叶平面](@entry_id:172317)是不正确的；我们必须对每个频率分量$\omega$乘以一个权重$|\omega|$。这个权重因子$|\omega|$在[频域](@entry_id:160070)中形似一个斜坡，因此被称为**[斜坡滤波器](@entry_id:754034)**（ramp filter）。这个滤波器本质上是对傅里叶空间中因极坐标采样导致的密度不均（在原点附近[过采样](@entry_id:270705)，在高频区域[欠采样](@entry_id:272871)）的一种校正。它通过放大高频分量来补偿这种不[均匀性](@entry_id:152612)。

#### 滤波[反投影](@entry_id:746638)（FBP）算法

直接在傅里叶域中进行插值和[逆变](@entry_id:192290)换（即上述策略的修正版）是可行的，但这并非FBP算法的经典形式。FBP通过巧妙地重排积分次序，将重建过程分为两个直观的步骤：**滤波**和**[反投影](@entry_id:746638)**。

让我们从带有[斜坡滤波器](@entry_id:754034)的反演公式出发。利用正弦[图的对称性](@entry_id:178762)，我们可以将角度积分范围改为$[0, \pi)$并将径向频率$\omega$的范围扩展到$\mathbb{R}$：
$$ f(\mathbf{x}) = \frac{1}{4\pi^2} \int_{0}^{\pi} \left( \int_{-\infty}^{\infty} \hat{f}(\omega \mathbf{n}(\theta)) |\omega| e^{i\omega (\mathbf{x} \cdot \mathbf{n}(\theta))} \, \mathrm{d}\omega \right) \, \mathrm{d}\theta $$
括号内的部分可以被看作是一个关于变量$t = \mathbf{x} \cdot \mathbf{n}(\theta)$的函数，它是一维逆傅里叶变换的形式。具体来说，它是在[频域](@entry_id:160070)中将投影的[傅里叶变换](@entry_id:142120)$\hat{p}(\theta, \omega) = \hat{f}(\omega \mathbf{n}(\theta))$乘以[斜坡滤波器](@entry_id:754034)$|\omega|$，然后再进行一维[逆傅里叶变换](@entry_id:178300)的结果。我们称这个结果为**滤波后的投影**（filtered projection），记为$p_F(\theta, t)$：
$$ p_F(\theta, t) = \frac{1}{2\pi} \int_{-\infty}^{\infty} \hat{p}(\theta, \omega) |\omega| e^{i\omega t} \, \mathrm{d}\omega $$
将此定义代回$f(\mathbf{x})$的表达式中，得到：
$$ f(\mathbf{x}) = \frac{1}{2\pi} \int_{0}^{\pi} p_F(\theta, \mathbf{x} \cdot \mathbf{n}(\theta)) \, \mathrm{d}\theta $$
这个积分操作被称为**[反投影](@entry_id:746638)**（back-projection）。它对于图像中的每个点$\mathbf{x}$，累加所有穿过该点的直线所对应的滤波后投影值。

总结起来，FBP算法流程如下：
1.  **滤波**：对每个角度$\theta$的投影数据$p(\theta, s)$，在[频域](@entry_id:160070)中乘以[斜坡滤波器](@entry_id:754034)$|\omega|$，然后通过[逆傅里叶变换](@entry_id:178300)得到滤波后的投影$p_F(\theta, s)$。
2.  **[反投影](@entry_id:746638)**：对于图像中的每个像素$\mathbf{x}$，通过计算$\int_{0}^{\pi} p_F(\theta, \mathbf{x} \cdot \mathbf{n}(\theta)) \, \mathrm{d}\theta$来重建其灰度值。

从[算子理论](@entry_id:139990)的角度看，我们可以定义反投影算子$\mathcal{R}^*$为[Radon变换](@entry_id:754021)算子$\mathcal{R}$的[伴随算子](@entry_id:140236)：
$$ (\mathcal{R}^* g)(\mathbf{x}) = \int_0^{\pi} g(\theta, \mathbf{x} \cdot \mathbf{n}(\theta)) \, \mathrm{d}\theta $$
FBP算法可以表示为滤波算子$\mathcal{H}$与反[投影算子](@entry_id:154142)$\mathcal{R}^*$的复合。通过严谨的傅里叶分析可以证明，这一复合算子$\mathcal{B} = \mathcal{R}^* \mathcal{H}$（乘以一个常数因子）正是[Radon变换](@entry_id:754021)$\mathcal{R}$的逆算子。具体来说，可以证明对于性质足够好的函数$f$，有$\mathcal{B}(\mathcal{R}f) = 2\pi f$ [@problem_id:3416052]。这为FBP算法提供了坚实的数学基础，表明它在理想条件下可以精确地重建原始图像。

### 实际应用中的离散化与考量

将理论上的FBP算法应用于实际的CT系统，需要处理离散采样带来的各种问题。

#### 采样要求

为了无失真地重建图像，投影数据必须满足**奈奎斯特采样准则**。这包括空间采样和角度采样两个方面。

1.  **探测器采样 ($\Delta s$)**：为了重建出包含最高角频率$\omega_c$的图像细节，根据[傅里叶切片定理](@entry_id:192235)，投影数据$p(\theta, s)$本身也必须包含高达$\omega_c$的频率分量。根据奈奎斯特准则，对$s$的采样频率必须至少是最高信号频率的两倍。这意味着探测器单元的间距$\Delta s$必须满足：
    $$ \Delta s \le \frac{\pi}{\omega_c} $$
    其中$\omega_c$通常由目标[图像分辨率](@entry_id:165161)$\Delta x$决定，例如$\omega_c = \pi/\Delta x$。因此，探测器必须足够密集，才能捕捉到重建高分辨率图像所需的高频信息 [@problem_id:3416093] [@problem_id:3416098]。

2.  **角度采样 ($\Delta \theta$)**：角度采样的要求更为微妙。它取决于物体的大小和期望的分辨率。在傅里叶空间中，角度采样不足会在[切线](@entry_id:268870)方向上导致[混叠](@entry_id:146322)。一个常用的准则是，在傅里叶空间中感兴趣区域的边缘（即频率为$\omega_c$处），由角度步长$\Delta \theta$造成的[弧长](@entry_id:191173)间隔$\omega_c \Delta\theta$不应超过径向频率的采样间隔（大致由物体半径$R$决定，约为$\pi/R$）。这导出了对角度数量$N_\theta = \pi / \Delta\theta$的要求：
    $$ \omega_c \Delta\theta \le \frac{\pi}{R} \implies \Delta\theta \le \frac{\pi}{\omega_c R} \implies N_\theta \ge \omega_c R $$
    这意味着，要重建一个大物体或实现高分辨率，就需要采集更多的投影角度 [@problem_id:3416093] [@problem_id:3416098]。

#### 离散滤波器与[窗函数](@entry_id:139733)

理想的[斜坡滤波器](@entry_id:754034)$|\omega|$在[频域](@entry_id:160070)是无界的，会无限放大高频成分。由于实际测量数据总是含有噪声，这种无限制的高频放大会导致重建图像中出现严重的噪声伪影。因此，在实践中，必须对[斜坡滤波器](@entry_id:754034)进行修改，引入一个**[窗函数](@entry_id:139733)**（window function）$W(\omega)$来平滑地将滤波器在高频处截断。

$$ H(\omega) = |\omega| W(\omega) $$

常用的[窗函数](@entry_id:139733)包括Ram-Lak窗（即简单的[矩形窗](@entry_id:262826)，在某个[截止频率](@entry_id:276383)$\omega_c$处硬截断）、Shepp-Logan窗和Hann窗等。这些窗函数通过抑制高频噪声来换取[图像分辨率](@entry_id:165161)的轻微损失。例如，对于带有Hann窗的滤波器，其脉冲响应在原点处不再是奇异的，而是一个有限值，这反映了其平滑特性[@problem_id:3416067]。选择合适的窗函数是在[噪声抑制](@entry_id:276557)和细节保留之间进行权衡的关键。

#### 数值实现与插值伪影

FBP的数值实现涉及[离散傅里叶变换](@entry_id:144032)（DFT/FFT）和插值。特别是在[反投影](@entry_id:746638)步骤中，对于每个图像像素$\mathbf{x}$和每个投影角度$\theta_m$，需要计算投影坐标$t = \mathbf{x} \cdot \mathbf{n}(\theta_m)$。这个$t$值通常不会恰好落在离散的探测器采样点$s_n$上，因此需要从已知的滤波后投影值$p_F(\theta_m, s_n)$中**插值**得到$p_F(\theta_m, t)$。常用的方法是[线性插值](@entry_id:137092)。

或者，可以采用完全基于傅里叶域的方法，将极坐标下的傅里叶样本插值到笛卡尔网格上（这个过程称为**gridding**），然后进行一次二维逆FFT。这两种方法中的插值步骤——无论是空间域的[线性插值](@entry_id:137092)还是[频域](@entry_id:160070)的插值——都非完美，会引入系统性的误差，即**插值伪影**，表现为重建图像的模糊或微小的结构失真[@problem_id:3416073]。

### 扩展与变体

平行束几何和标准的[Radon变换](@entry_id:754021)模型是理论分析的基础，但实际的CT系统和应用场景常常需要更复杂的模型。

#### 扇束与锥束几何

现代[CT扫描](@entry_id:747639)仪大多采用**扇束**（fan-beam，用于2D）或**锥束**（cone-beam，用于3D）几何。在这种设置下，[X射线](@entry_id:187649)从一个[点源](@entry_id:196698)发出，形成扇形或锥形射[线束](@entry_id:167936)。扇束数据可以通过一个称为**重排**（rebinning）的过程转换为等效的平行束数据，然后应用标准的FBP算法。这个转换过程涉及到坐标变换和[雅可比行列式](@entry_id:137120)的加权。从扇束坐标（源角度$\beta$，扇角$\gamma$）到平行束坐标（投影角度$\theta$，距离$s$）的变换，其雅可比行列式为$R \cos\gamma$（其中$R$是源到旋转中心的距离），这个因子必须在重建中加以考虑以保证灰度值的准确性[@problem_id:3416063]。

对于三维锥束CT，一个著名的近似重建算法是**Feldkamp-Davis-Kress (FDK)算法**。在小锥角的情况下，FDK算法可以看作是二维FBP算法向三维的直接推广。在理论上，它与三维[Radon变换](@entry_id:754021)（对平面积分）及其反演公式密切相关。对于奇数维空间（如三维），Radon反演公式具有“局部”性质，即某一点的重建值仅依赖于穿过该点的那些平面的投影数据。这使得精确重建在理论上成为可能，并且FDK算法正是这一思想的近似实现[@problem_id:3416062]。

#### 衰减[Radon变换](@entry_id:754021)

在[核医学](@entry_id:138217)成像（如SPECT）中，从体内[放射性药物](@entry_id:149628)发出的[光子](@entry_id:145192)在到达探测器前会被人体组织衰减。如果衰减系数$\mu$为常数，则其物理模型由**衰减[Radon变换](@entry_id:754021)**（Attenuated Radon Transform）描述：
$$ G_{\mu} f(\theta,s)=\int_{-\infty}^{\infty}\exp(-\mu D(\mathbf{x}, \theta))\,f(\mathbf{x}) \, \mathrm{d}\ell $$
其中$D(\mathbf{x}, \theta)$是从点$\mathbf{x}$沿射线方向到物体边界的距离。如果将为标准CT设计的FBP算法错误地应用于这类衰减数据，重建结果将出现严重的定量不准和结构性伪影（如典型的“杯状伪影”，即中心区域[强度降低](@entry_id:755509)）。这强调了一个核心原则：重建算法必须与其所描述的[数据采集](@entry_id:273490)物理模型相匹配。对衰减[Radon变换](@entry_id:754021)的反演需要专门设计的、更为复杂的算法[@problem_id:3416068]。

本章概述了从CT[数据采集](@entry_id:273490)的物理基础到经典FBP重建算法的完整理论链条，并探讨了实际应用中的关键考量和模型扩展。理解这些原理与机制，是深入学习更高级的迭代重建方法、伪影校正技术以及现代CT成像新进展的必要前提。