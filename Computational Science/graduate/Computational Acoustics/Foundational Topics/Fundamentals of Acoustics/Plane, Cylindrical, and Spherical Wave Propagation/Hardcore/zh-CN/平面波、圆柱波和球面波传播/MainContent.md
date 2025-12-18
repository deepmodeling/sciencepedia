## 引言
声波的传播是声学、物理学乃至众多工程领域中的核心现象。从音乐厅的设计到水下声纳的探测，再到医学超声成像，对波如何从声源产生、在介质中行进并与障碍[物相](@entry_id:196677)互作用的深刻理解至关重要。然而，要将这些物理直觉转化为精确的预测和强大的技术，我们需要一个坚实的[数学物理](@entry_id:265403)框架。本文旨在系统性地填补这一认知空白，为读者构建一个关于基本波形——平面波、[柱面波](@entry_id:1123342)与[球面波](@entry_id:200471)——从理论到应用的完整知识体系。

本文分为三个核心部分。在“原理与机制”一章中，我们将从最基本的[波动方程](@entry_id:139839)出发，推导时谐声学的基石——亥姆霍兹方程，并详细解析其在不同坐标系下的[基本解](@entry_id:184782)，揭示[几何扩散](@entry_id:1125610)与介质衰减等物理机制。接着，在“应用与交叉学科联系”一章中，我们将展示这些看似抽象的理论如何应用于解决实际问题，探讨波在边界、波导和散射体环境中的复杂行为，并揭示其在地球物理、医学成像等领域的深刻联系。最后，在“动手实践”一章中，我们提供了一系列精心设计的计算问题，旨在帮助读者将理论知识转化为解决实际[数值模拟](@entry_id:146043)挑战的能力。通过这一结构化的学习路径，读者将能够掌握波传播的核心原理，并将其应用于前沿的科学研究与工程实践中。

## 原理与机制

本章旨在系统性地阐述声波在均匀介质中传播的基本原理与核心机制。在前一章介绍性内容的基础上，我们将从[波动方程](@entry_id:139839)出发，推导出适用于[时谐场](@entry_id:755985)的亥姆霍兹方程，并深入探讨其在不同几何构型下的解析解。通过分析能量守恒、[几何扩散](@entry_id:1125610)及介质衰减等物理过程，我们将揭示波幅随距离变化的规律。最后，本章将构建一个完整的[边值问题](@entry_id:1121801)框架，涵盖[角谱法](@entry_id:1121014)、倏逝波、无穷远处的[索末菲辐射条件](@entry_id:168772)以及有限边界上的物理条件，为[计算声学](@entry_id:172112)中的数值建模奠定坚实的理论基础。

### 从波动方程到亥姆霍兹方程

在无粘、均匀、静止的流体介质中，小幅度的声扰动由线性的流体[动力学方程组](@entry_id:202106)描述。这些方程包括质量守恒（连续性方程）和动量守恒（[欧拉方程](@entry_id:177914)）。对于声压扰动$p'(\mathbf{x}, t)$和质点速度$\mathbf{v}(\mathbf{x}, t)$，它们的形式如下：

- **线性化[动量方程](@entry_id:197225)**: $\rho_0 \frac{\partial \mathbf{v}}{\partial t} = -\nabla p'$
- **线性化连续性与状态方程**: $\frac{\partial p'}{\partial t} = - \rho_0 c^2 \nabla \cdot \mathbf{v}$

此处，$\rho_0$是介质的平衡密度，$c$是声速。通过对动量方程求散度并代入连续性方程的时间导数（或反之），我们可以消去其中一个变量，得到一个仅含压力或速度的[二阶偏微分方程](@entry_id:175326)。针对声压，这个过程导出了经典的**标量波动方程** (scalar wave equation)：

$$
\nabla^2 p' - \frac{1}{c^2} \frac{\partial^2 p'}{\partial t^2} = 0
$$

在计算声学中，我们常常关注在特定频率下[稳态](@entry_id:139253)振动的场，即**[时谐场](@entry_id:755985)** (time-harmonic field)。假设声压场具有$e^{-i\omega t}$的时间依赖性，其中$\omega$是角频率，$i$是虚数单位。我们可以将瞬时声压表示为其[复振幅](@entry_id:164138)$P(\mathbf{x})$的实部：$p'(\mathbf{x}, t) = \Re\{P(\mathbf{x}) e^{-i\omega t}\}$。在这种**相量** (phasor) 表示下，时间导数算子$\frac{\partial}{\partial t}$可以被代数乘法$-i\omega$替代。将此时谐形式代入[波动方程](@entry_id:139839)，二阶时间导数变为$(-i\omega)^2 = -\omega^2$，我们便得到了控制复声压振幅$P(\mathbf{x})$在空间中分布的方程——**亥姆霍兹方程** (Helmholtz equation)  ：

$$
(\nabla^2 + k^2) P = 0
$$

[亥姆霍兹方程](@entry_id:149977)是椭圆型[偏微分](@entry_id:194612)方程，是波动物理中最为核心的方程之一。方程中的参数$k$被称为**波数** (wavenumber)。通过对比推导过程，我们发现$k^2 = (\omega/c)^2$。对于向外传播的波，我们通常取其[正根](@entry_id:199264)，从而得到声学中最基本的**色散关系** (dispersion relation)：

$$
k = \frac{\omega}{c}
$$

进行[量纲分析](@entry_id:140259)可以加深对这些参数物理意义的理解。拉普拉斯算子$\nabla^2$的量纲是$[长度]^{-2}$ (例如 $\mathrm{m}^{-2}$)。为了保证[亥姆霍兹方程](@entry_id:149977)中两项可以相加，$k^2$必须具有相同的量纲，这意味着波数$k$的量纲是$[长度]^{-1}$ (例如 $\mathrm{m}^{-1}$)。[角频率](@entry_id:261565)$\omega$的单位是弧度/秒 (rad/s)，其量纲为$[时间]^{-1}$；声速$c$的量纲为$[长度][时间]^{-1}$。因此，$k = \omega/c$的量纲为$([时间]^{-1}) / ([长度][时间]^{-1}) = [长度]^{-1}$，与从[亥姆霍兹方程](@entry_id:149977)直接推断的结果完全一致。

从物理上看，波数$k$是**角[空间频率](@entry_id:270500)** (angular spatial frequency)。考虑一个沿$x$轴传播的简单[波函数](@entry_id:201714)，其相位因子为$e^{ikx}$。相位$\phi(x) = kx$对空间位置的变化率$\frac{d\phi}{dx} = k$，表示[波的相位](@entry_id:171303)每沿传播方向前进一个单位长度所增加的弧度数。因此，波数$k$量化了波在空间上的振荡密度 。

### 典型几何构型中的[基本解](@entry_id:184782)

[亥姆霍兹方程](@entry_id:149977)的解描述了声波在空间中的形态。最基本、最重要的解对应于三种典型的几何构型：平面波、[柱面波](@entry_id:1123342)和[球面波](@entry_id:200471)。

#### [拉普拉斯算子](@entry_id:146319)在[曲线坐标系](@entry_id:172561)下的形式

为了在非[笛卡尔坐标系](@entry_id:169789)中求解[亥姆霍兹方程](@entry_id:149977)，我们首先需要知道[拉普拉斯算子](@entry_id:146319)$\nabla^2$在这些坐标系下的具体形式。它们可以从度规张量严格推导得出 。

对于**[柱坐标系](@entry_id:266798)** $(r, \theta, z)$，拉普拉斯算子作用于一个[标量场](@entry_id:151443) $f(r, \theta, z)$ 的表达式为：
$$
\nabla^2 f = \frac{1}{r}\frac{\partial}{\partial r}\left(r \frac{\partial f}{\partial r}\right) + \frac{1}{r^2}\frac{\partial^2 f}{\partial \theta^2} + \frac{\partial^2 f}{\partial z^2} = \frac{\partial^2 f}{\partial r^2} + \frac{1}{r}\frac{\partial f}{\partial r} + \frac{1}{r^2}\frac{\partial^2 f}{\partial \theta^2} + \frac{\partial^2 f}{\partial z^2}
$$

对于**[球坐标系](@entry_id:167517)** $(r, \theta, \phi)$，表达式为：
$$
\nabla^2 f = \frac{1}{r^2}\frac{\partial}{\partial r}\left(r^2 \frac{\partial f}{\partial r}\right) + \frac{1}{r^2 \sin\theta}\frac{\partial}{\partial \theta}\left(\sin\theta \frac{\partial f}{\partial \theta}\right) + \frac{1}{r^2 \sin^2\theta}\frac{\partial^2 f}{\partial \phi^2}
$$
这个表达式可以被巧妙地分解为一个径向[部分和](@entry_id:162077)一个角向部分。我们可以将其写为：
$$
\nabla^2 f = \left(\frac{\partial^2 f}{\partial r^2} + \frac{2}{r}\frac{\partial f}{\partial r}\right) + \frac{1}{r^2} \Delta_{\mathbb{S}^2} f
$$
其中$\Delta_{\mathbb{S}^2}$是作用于[单位球](@entry_id:142558)面$\mathbb{S}^2$上的角函数的**[拉普拉斯-贝尔特拉米算子](@entry_id:267002)** (Laplace-Beltrami operator)，其定义为：
$$
\Delta_{\mathbb{S}^2} = \frac{1}{\sin\theta}\frac{\partial}{\partial \theta}\left(\sin\theta \frac{\partial}{\partial \theta}\right) + \frac{1}{\sin^2\theta}\frac{\partial^2}{\partial \phi^2}
$$
这个算子的[本征函数](@entry_id:154705)是[球谐函数](@entry_id:178380)，它们构成了球面上函数空间的[标准正交基](@entry_id:147779)。

#### 平面波

**平面波** (plane wave) 是最简单的波动形式，其等相位面是相互平行的平面。其[复振幅](@entry_id:164138)可以表示为：
$$
P(\mathbf{r}) = P_0 e^{i\mathbf{k}\cdot\mathbf{r}}
$$
其中$P_0$是复常数振幅，$\mathbf{r}$是位置矢量，而$\mathbf{k}$是**[波矢](@entry_id:178620)量** (wave vector)，其方向指向波的传播方向。将此解代入[亥姆霍兹方程](@entry_id:149977)$(\nabla^2 + k^2)P = 0$，我们得到：
$$
\nabla P = i\mathbf{k} P \implies \nabla^2 P = (i\mathbf{k})\cdot(i\mathbf{k}P) = -|\mathbf{k}|^2 P
$$
因此，方程变为$(-|\mathbf{k}|^2 + k^2)P=0$。对于非零解，必须满足$|\mathbf{k}|^2 = k^2$，即波矢量的大小等于介质的波数$k=\omega/c$。这表明，对于一个给定的频率$\omega$，所有可能的[平面波](@entry_id:189798)的波矢量$\mathbf{k}$的端点都落在一个半径为$k$的球面上，这个球面在倒易空间中被称为**等频率面**。对于无衰减介质中的传播波，波矢量$\mathbf{k}$是实矢量 。

[平面波](@entry_id:189798)的[质点](@entry_id:186768)速度振幅$\mathbf{V}$可以通过线性化[动量方程](@entry_id:197225)的频域形式$\mathbf{V} = \frac{1}{i\omega\rho_0}\nabla P$来求得。代入[平面波解](@entry_id:195230)，我们有：
$$
\mathbf{V} = \frac{1}{i\omega\rho_0} (i\mathbf{k}P) = \frac{\mathbf{k}}{\omega\rho_0} P
$$
由于$\mathbf{k} = k\hat{\mathbf{k}} = (\omega/c)\hat{\mathbf{k}}$（其中$\hat{\mathbf{k}}$是传播方向的单位矢量），上式可简化为：
$$
\mathbf{V} = \frac{(\omega/c)\hat{\mathbf{k}}}{\omega\rho_0} P = \frac{1}{\rho_0 c} \hat{\mathbf{k}} P
$$
这表明，对于平面波，[质点](@entry_id:186768)[速度矢量](@entry_id:269648)与波的传播方向平行，且其振幅与声压振幅成正比。压力与同相[质点](@entry_id:186768)速度之比定义了**[比声阻抗](@entry_id:921125)** (specific acoustic impedance)。对于平面波，这个值是一个常数$Z_{plane} = P/V = \rho_0 c$，它被称为介质的**特性阻抗** (characteristic impedance) 。

#### [柱面波](@entry_id:1123342)与[球面波](@entry_id:200471)

当声源具有特定对称性时，产生的波自然地用相应的坐标系来描述。

对于一个位于原点的**[点源](@entry_id:196698)**，其辐射的声场具有[球对称性](@entry_id:272852)。在这种情况下，[亥姆霍兹方程](@entry_id:149977)简化为只含径向分量$r$的[常微分方程](@entry_id:147024)。向外传播的**[球面波](@entry_id:200471)** (spherical wave) 解具有以下精确形式 (对于$r>0$) ：
$$
P(r) = A \frac{e^{ikr}}{r}
$$
其中$A$是一个复常数，代表声源的强度。这个解包含两个关键部分：相位项$e^{ikr}$和振幅项$1/r$。相位项表明波的相位以每米$k$弧度的速率沿径向传播。振幅项$1/r$则描述了**[几何扩散](@entry_id:1125610)** (geometric spreading) 效应，我们将在下一节详细讨论。

对于一个沿$z$轴无限长的**线源**，其辐射的声场在$xy$平面内具有[柱对称性](@entry_id:269179)。[亥姆霍兹方程](@entry_id:149977)在[柱坐标](@entry_id:271645)下简化为零阶[贝塞尔方程](@entry_id:164013)。其向外传播的**[柱面波](@entry_id:1123342)** (cylindrical wave) 解由第一类汉克尔函数 (Hankel function of the first kind) $H_0^{(1)}(kr)$给出。在离声源较远的[远场区](@entry_id:185115)域($kr \gg 1$)，汉克尔函数有如下的渐近形式  ：
$$
P(r) \sim A \frac{e^{ikr}}{\sqrt{r}}
$$
这里的振幅[衰减因子](@entry_id:1121239)是$1/\sqrt{r}$，这反映了二维情况下的[几何扩散](@entry_id:1125610)规律。无论是[球面波](@entry_id:200471)还是[柱面波](@entry_id:1123342)，波数$k$的物理意义——作为空间相位变化率——保持不变 。

### 波传播的物理机制

波在传播过程中，其振幅会发生变化。这种变化主要源于两个独立的物理机制：[几何扩散](@entry_id:1125610)和介质吸收。

#### [几何扩散](@entry_id:1125610)与能量守恒

[几何扩散](@entry_id:1125610)是由于波阵面随传播距离扩大，能量分布在越来越大的面积上而导致的振幅下降。这个过程可以从能量守恒定律严格推导出来 。

声波的能量流由**[声强](@entry_id:1120700)** (acoustic intensity) 矢量$\mathbf{I}$描述，它代表单位时间内通过单位面积的声能。对于[时谐场](@entry_id:755985)，我们更关心其[时间平均](@entry_id:267915)值$\langle \mathbf{I} \rangle$。其径向分量可表示为$\langle I_r \rangle = \frac{1}{2}\Re\{P U_r^*\}$，其中$U_r$是径向质点速度的[复振幅](@entry_id:164138)。在远离声源的远场，声场局部近似为平面波，因此$U_r \approx P / (\rho_0 c)$。代入后得到：
$$
\langle I_r \rangle \approx \frac{|P|^2}{2\rho_0 c}
$$
这表明，远场声强与声压振幅的平方成正比。

在一个无损耗的介质中，由声源辐射出的总功率必须恒定，即通过任何包围声源的封闭曲面的总[能量通量](@entry_id:266056)是相同的。

-   在**三维空间**中，我们考虑一个半径为$r$的球面。球的总表面积为$A_{3D} = 4\pi r^2$。[总辐射功率](@entry_id:756065)$W_{3D} = \langle I_r \rangle \cdot A_{3D} = \text{常数}$。由于$A_{3D} \propto r^2$，声强必须满足$\langle I_r \rangle \propto 1/r^2$。因为$|P|^2 \propto \langle I_r \rangle$，所以声压振幅的衰减规律为$|P| \propto 1/r$。这与我们之前看到的[球面波](@entry_id:200471)解$e^{ikr}/r$的振幅部分完全吻合。

-   在**二维空间**中（等效于三维中的无限长线源），我们考虑一个半径为$r$、单位长度的圆柱面。其侧面积（即圆[周长](@entry_id:263239)）为$A'_{2D} = 2\pi r$。单位长度的辐射功率$W'_{2D} = \langle I_r \rangle \cdot A'_{2D} = \text{常数}$。由于$A'_{2D} \propto r$，[声强](@entry_id:1120700)必须满足$\langle I_r \rangle \propto 1/r$。因此，声压振幅的衰减规律为$|P| \propto 1/\sqrt{r}$。这同样与[柱面波](@entry_id:1123342)[远场](@entry_id:269288)解$e^{ikr}/\sqrt{r}$的振幅部分一致。

这个基于能量守恒的论证，清晰地解释了不同维度下[几何扩散](@entry_id:1125610)导致的不同振幅衰减率 。

#### [有损介质](@entry_id:1127459)中的衰减

真实的物理介质几乎都存在[能量耗散](@entry_id:147406)机制，如[粘滞](@entry_id:201265)性或[热传导](@entry_id:143509)，这会导致声能在[传播过程](@entry_id:1132219)中转化为热能，从而使声波振幅衰减。这种现象称为**衰减** (attenuation) 或吸收。

在现象学上，我们可以通过引入一个**[复波数](@entry_id:274896)** (complex wavenumber)来简洁地描述衰减效应 。我们将波数$k$写成复数形式：
$$
k = k' + i\alpha
$$
其中，实部$k' > 0$仍然是角[空间频率](@entry_id:270500)，决定了[波的相位](@entry_id:171303)传播；虚部$\alpha > 0$称为**[衰减系数](@entry_id:920164)** (attenuation coefficient)。考虑一个沿正方向传播的波，其空间依赖因子为$e^{ikr}$。代入[复波数](@entry_id:274896)：
$$
e^{ikr} = e^{i(k' + i\alpha)r} = e^{ik'r} e^{-\alpha r}
$$
这个表达式清晰地显示，除了由$e^{ik'r}$描述的相位振荡外，波的振幅还有一个指数衰减项$e^{-\alpha r}$。衰减系数$\alpha$的单位是奈培/米 (Np/m)，它描述了振幅随距离指数下降的速率。

当同时存在[几何扩散](@entry_id:1125610)和介质衰减时，总的振幅衰减是两者效果的乘积。因此，在[有损介质](@entry_id:1127459)中，三种基本波形的振幅依赖关系变为 ：

-   **[平面波](@entry_id:189798)**: $|P(r)| \propto e^{-\alpha r}$ (无[几何扩散](@entry_id:1125610))
-   **[柱面波](@entry_id:1123342) ([远场](@entry_id:269288))**: $|P(r)| \propto \frac{e^{-\alpha r}}{\sqrt{r}}$
-   **[球面波](@entry_id:200471)**: $|P(r)| \propto \frac{e^{-\alpha r}}{r}$

区分这两种机制至关重要：[几何扩散](@entry_id:1125610)源于能量在更大空间中的重新分布，即使在无损介质中也存在；而衰减则是由于能量从声场中不可逆地损失掉了。

### 作为[边值问题](@entry_id:1121801)的波传播

在实际的计算声学问题中，我们通常不是处理无限空间中的孤立声源，而是在具有复杂边界的域中求解[亥姆霍兹方程](@entry_id:149977)。这构成了一个**边值问题** (boundary value problem)。要获得唯一且物理上正确的解，必须在所有边界上施加适当的条件。

#### [角谱法](@entry_id:1121014)与惠更斯原理

考虑一个声场占据半无限空间$z>0$的情况，并且我们在平面$z=0$上知道声压的分布$P(x,y,0)$。如何确定$z>0$空间中任意点的声压？

**惠更斯原理** (Huygens' principle) 提供了一个直观的物理图像：[波前](@entry_id:197956)上的每一点都可以看作是次级球面子波的新波源，而新的[波前](@entry_id:197956)是所有这些子波的包络。对于线性波动，这可以严格地表述为叠加原理。

**[角谱法](@entry_id:1121014)** (Angular Spectrum Method, ASM) 是惠更斯原理在频域中的一种精确数学实现 。其核心思想是将$z=0$平面上的任意声场分解为一系列无穷多个不同方向传播的平面[波的叠加](@entry_id:166456)。这一分解通过对横向坐标$(x,y)$进行[二维傅里叶变换](@entry_id:273583)来完成：
$$
\hat{P}(k_x, k_y) = \iint_{\mathbb{R}^2} P(x,y,0) e^{-i(k_x x + k_y y)} dx dy
$$
这里的$\hat{P}(k_x, k_y)$就是声场的**[角谱](@entry_id:184925)**，它给出了具有横向[波矢](@entry_id:178620)量$\mathbf{k}_\parallel = (k_x, k_y)$的[平面波](@entry_id:189798)分量的[复振幅](@entry_id:164138)。

根据色散关系$|\mathbf{k}|^2 = k_x^2 + k_y^2 + k_z^2 = k^2$，每个[平面波](@entry_id:189798)分量的纵向波数$k_z$由其横向波矢量唯一确定：
$$
k_z = \sqrt{k^2 - |\mathbf{k}_\parallel|^2}
$$
一旦知道了[角谱](@entry_id:184925)，将声场从$z=0$传播到任意平面$z>0$就变得异常简单：只需将每个平面波分量乘以相应的传播因子$e^{ik_z z}$即可。这是因为$e^{i\mathbf{k}_\parallel \cdot \mathbf{r}_\parallel} e^{ik_z z}$正是[亥姆霍兹方程](@entry_id:149977)的一个精确解。于是，在$z$平面上的[角谱](@entry_id:184925)为$\hat{P}(k_x, k_y, z) = \hat{P}(k_x, k_y) e^{ik_z z}$。最后，通过[傅里叶逆变换](@entry_id:178300)，我们将所有传播后的[平面波](@entry_id:189798)分量重新叠加起来，就得到了$z$平面上的声压场：
$$
P(x,y,z) = \frac{1}{(2\pi)^2} \iint_{\mathbb{R}^2} \hat{P}(k_x, k_y) e^{ik_z z} e^{i(k_x x + k_y y)} dk_x dk_y
$$
这个“分解-传播-重构”的过程，在计算上通常通过[快速傅里叶变换 (FFT)](@entry_id:146372) 高效实现。根据**[卷积定理](@entry_id:264711)**，频域中的乘法等效于空域中的卷积。这意味着[角谱法](@entry_id:1121014)传播等效于将初始声场与一个代表自由空间传播的[核函数](@entry_id:145324)（即自由空间[格林函数](@entry_id:147802)）进行卷积 。

#### 传播波与倏逝波

在[角谱法](@entry_id:1121014)中，根据横向波数$|\mathbf{k}_\parallel|$与介质波数$k$的相对大小，[平面波](@entry_id:189798)分量表现出两种截然不同的行为  。

-   **传播波 (Propagating Waves)**: 当$|\mathbf{k}_\parallel| \le k$时，$k_z^2 = k^2 - |\mathbf{k}_\parallel|^2 \ge 0$，因此$k_z$是实数。这些分量是普通的[平面波](@entry_id:189798)，它们在$z$方向上以振荡形式传播而不衰减（在无损介质中）。它们携带能量，能够传播到远离源的**远场** (far-field) 区域。

-   **[倏逝波](@entry_id:156713) (Evanescent Waves)**: 当$|\mathbf{k}_\parallel| > k$时，$k_z^2  0$，因此$k_z$是纯虚数。我们可令$k_z = i\sqrt{|\mathbf{k}_\parallel|^2 - k^2} = i\alpha$，其中$\alpha$为正实数。此时，传播因子变为$e^{ik_z z} = e^{-\alpha z}$。这些分量在$z$方向上不发生相位振荡，而是呈指数衰减。它们被称为[倏逝波](@entry_id:156713)，因为它们的振幅会随着离开源平面的距离而迅速消失。

[倏逝波](@entry_id:156713)虽然不向[远场辐射](@entry_id:265518)能量（其时间平均的法向声强为零），但它们对于精确构建声源附近的**[近场](@entry_id:269780)** (near-field) 至关重要 。从[傅里叶分析](@entry_id:137640)的角度看，高[空间频率](@entry_id:270500)分量（大的$|\mathbf{k}_\parallel|$）对应于场中的精细空间细节。条件$|\mathbf{k}_\parallel| > k$等价于横向波长$\lambda_\parallel = 2\pi/|\mathbf{k}_\parallel|$小于介质中的波长$\lambda = 2\pi/k$。因此，[倏逝波](@entry_id:156713)正是那些负责描述**亚波长** (subwavelength) 信息的组分。若在计算中忽略它们，将无法准确重构近场的复杂结构 。数值实现时，为了捕捉这些高频倏逝波，[空间采样](@entry_id:903939)必须满足**奈奎斯特准则**，否则会产生**[混叠](@entry_id:146322)** (aliasing) 错误，严重扭曲计算结果。

#### 无穷远处的边界条件：[索末菲辐射条件](@entry_id:168772)

对于开放或无界域中的问题，亥姆霍兹方程的解不唯一。例如，除了从声源向外辐射的波，数学上也允许从无穷远处传入的波。为了得到物理上唯一且有意义的解，我们必须施加一个**[辐射条件](@entry_id:1130495)** (radiation condition) 来排除传入波。

**[索末菲辐射条件](@entry_id:168772)** (Sommerfeld radiation condition) 正是为此而设 。它基于物理事实，即在远离任何声源的[远场](@entry_id:269288)，声场应表现为纯粹的向外传播的波。其数学形式依赖于空间的维度，这与我们之前讨论的[几何扩散](@entry_id:1125610)规律直接相关。

-   在**三维空间**中，声压振幅按$1/r$衰减，向外的[球面波](@entry_id:200471)形式为$P \sim A(\theta, \phi) \frac{e^{ikr}}{r}$。基于此，[索末菲辐射条件](@entry_id:168772)可以写作：
    $$
    \lim_{r\to\infty} r \left( \frac{\partial P}{\partial r} - ikP \right) = 0
    $$

-   在**二维空间**中，声压振幅按$1/\sqrt{r}$衰减，向外的[柱面波](@entry_id:1123342)形式为$P \sim A(\theta) \frac{e^{ikr}}{\sqrt{r}}$（源于汉克尔函数的[渐近行为](@entry_id:160836) ）。这导致了形式略有不同的[辐射条件](@entry_id:1130495)：
    $$
    \lim_{r\to\infty} \sqrt{r} \left( \frac{\partial P}{\partial r} - ikP \right) = 0
    $$

[索末菲辐射条件](@entry_id:168772)保证了能量是单向地从声源流向无穷远，并且[总辐射功率](@entry_id:756065)是一个有限的正常数，而不是零 。在数值计算中，这个条件是构建**[完美匹配层](@entry_id:753330)** (Perfectly Matched Layers, PML) 或其他**[吸收边界条件](@entry_id:164672)** (Absorbing Boundary Conditions, ABC) 的理论基础，用于在有限的计算域上模拟无界空间。

#### 有限边界上的物理条件

在[计算声学](@entry_id:172112)问题中，声场常常与物理表面相互作用。这些相互作用通过在亥姆霍兹方程的边界上施加相应的边界条件来建模 。最常见的三种[理想边界](@entry_id:200849)条件如下：

首先，我们需要建立边界面上声压的法向导数$\frac{\partial P}{\partial n} = \mathbf{n} \cdot \nabla P$（其中$\mathbf{n}$是指向流体域外的[单位法向量](@entry_id:178851)）与质点速度法向分量$U_n = \mathbf{n} \cdot \mathbf{V}$之间的关系。根据线性化[动量方程](@entry_id:197225)的频域形式$\mathbf{V} = \frac{i}{\omega\rho_0}\nabla P$，我们有：
$$
U_n = \frac{i}{\omega\rho_0} \frac{\partial P}{\partial n}
$$

1.  **刚性壁 (Rigid Wall)**：也称硬声场边界。理想的刚性壁是完全不可穿透的，因此其法向质点速度为零，$U_n=0$。这直接导致了声压满足**齐次[诺伊曼条件](@entry_id:165471)** (homogeneous Neumann condition)：
    $$
    \frac{\partial P}{\partial n} = 0
    $$

2.  **压力释放边界 (Pressure-Release Wall)**：也称软声场边界。这种边界不能承受任何压力变化，例如流体与真空的交界面。因此，边界上的声压始终为零，$P=0$。这对应于**齐次[狄利克雷条件](@entry_id:137096)** (homogeneous Dirichlet condition)：
    $$
    P = 0
    $$

3.  **阻抗边界 (Impedance Wall)**：这种边界介于刚性壁和软声场边界之间，它允许一定的能量传入或耗散。其特性通过**[比声阻抗](@entry_id:921125)**$Z_s$来描述，定义为声压与法向质点速度之比$Z_s = P/U_n$。将$U_n$的表达式代入，整理后得到一个**罗宾条件** (Robin condition)：
    $$
    \frac{\partial P}{\partial n} = \frac{i\omega\rho_0}{Z_s} P
    $$
    在实际应用中，通常使用无量纲的**[归一化阻抗](@entry_id:266178)** (normalized impedance) $Z = Z_s/(\rho_0 c)$。利用$k=\omega/c$，上述条件可以写成更简洁的形式：
    $$
    \frac{\partial P}{\partial n} = ikZ^{-1}P
    $$
    这个条件能够模拟具有一定吸声或透射特性的真实材料表面 。

综上所述，从亥姆霍兹方程到其在不同几何构型下的解，再到[能量传播](@entry_id:202589)的物理机制和完整的边值问题框架，我们已经为理解和计算声波传播奠定了必要的理论基础。