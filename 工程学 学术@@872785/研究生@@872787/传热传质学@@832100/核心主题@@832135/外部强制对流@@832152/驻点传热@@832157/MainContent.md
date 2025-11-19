## 引言
[驻点](@entry_id:136617)传热是[流体力学](@entry_id:136788)和传热学领域的一个经典而又至关重要的问题。当流体正面冲击一个物体时，在物体表面的[驻点](@entry_id:136617)区域，[流体速度](@entry_id:267320)降为零，动能大量转化为热能和压力能，从而产生极高的局部压力和剧烈的热交换。这种现象在航空航天（如航天器[再入大气层](@entry_id:152511)）、工业制造（如冲击射流冷却和材料加工）以及日常生活中都扮演着核心角色。精确预测和控制[驻点](@entry_id:136617)区域的极端热负荷，对于确保设备安全、优化工艺效率至关重要。

然而，描述这一现象的物理过程极其复杂，涉及惯性、黏性、[压力梯度](@entry_id:274112)和热量传递之间的精妙平衡。本文旨在为这一复杂问题建立一个清晰、系统的理论框架。我们将从最基本的物理原理出发，揭示驻点传热背后的核心机制，并展示如何将这些理论应用于解决前沿的工程挑战。

在接下来的内容中，读者将循序渐进地掌握[驻点](@entry_id:136617)传热的完整知识体系。在“原理与机制”一章中，我们将建立驻点流的数学模型，推导并求解著名的希门兹[相似解](@entry_id:171590)，从而量化动量和热量的传递过程。随后，在“应用与跨学科联系”一章中，我们将把视野扩展到真实的工程世界，探讨该理论如何在航空航天、工业传热和[湍流](@entry_id:151300)研究等领域发挥关键作用。最后，通过“动手实践”环节，你将有机会运用所学知识解决具体问题，从而巩固和深化理解。

## 原理与机制

在上一章中，我们介绍了驻点区域传热的重要性，它在航空航天、材料加工和[电子冷却](@entry_id:150853)等众多工程领域中都扮演着核心角色。本章将深入探讨驻点流动的基本原理及其[传热机制](@entry_id:142474)。我们将从[理想流体](@entry_id:161909)的运动学分析出发，逐步引入黏性效应和[边界层](@entry_id:139416)的概念，推导并求解控制方程，最终建立一个能够精确描述和预测驻点传热的理论框架。

### 驻点流的运动学

为了理解驻点附近的[复杂流动](@entry_id:747569)，我们首先从一个简化的理想模型入手：一个二维、稳定、不可压缩的无黏、无[旋流](@entry_id:153202)体正交冲击一个无限大的平壁。我们将[驻点](@entry_id:136617)设在坐标原点 $(0,0)$，壁面位于 $y=0$ 处，流体占据 $y>0$ 的空间。

在驻点附近的一个小邻域内，我们可以对光滑的无黏外部流场 $\vec{V}_e(x, y) = (U_e(x, y), V_e(x, y))$ 进行一阶[泰勒级数展开](@entry_id:138468)。根据驻点的定义，该点的速度为零，即 $U_e(0,0) = 0$ 和 $V_e(0,0) = 0$。因此，速度场的线性近似为：
$$
U_e(x, y) \approx x \left.\frac{\partial U_e}{\partial x}\right|_{(0,0)} + y \left.\frac{\partial U_e}{\partial y}\right|_{(0,0)}
$$
$$
V_e(x, y) \approx x \left.\frac{\partial V_e}{\partial x}\right|_{(0,0)} + y \left.\frac{\partial V_e}{\partial y}\right|_{(0,0)}
$$

该流动受两个基本物理定律约束。首先，**[不可压缩性](@entry_id:274914)**要求流场散度为零，即 $\nabla \cdot \vec{V}_e = 0$，这在驻点处意味着：
$$
\left.\frac{\partial U_e}{\partial x}\right|_{(0,0)} + \left.\frac{\partial V_e}{\partial y}\right|_{(0,0)} = 0
$$

其次，**无旋性**要求流场[涡量](@entry_id:142747)为零，$\nabla \times \vec{V}_e = 0$。对于[二维流](@entry_id:266853)动，这简化为 $\frac{\partial V_e}{\partial x} - \frac{\partial U_e}{\partial y} = 0$，因此在[驻点](@entry_id:136617)处：
$$
\left.\frac{\partial V_e}{\partial x}\right|_{(0,0)} = \left.\frac{\partial U_e}{\partial y}\right|_{(0,0)}
$$

此外，由于流动是正交冲击壁面，关于 $y$ 轴（即 $x=0$ 线）对称。这种对称性要求 $x=0$ 线上没有横向流动，即 $U_e(0, y) = 0$。这进一步导致 $\left.\frac{\partial U_e}{\partial y}\right|_{(0,0)} = 0$。结合无旋条件，我们得到 $\left.\frac{\partial V_e}{\partial x}\right|_{(0,0)} = 0$。

将这些条件代回[泰勒展开](@entry_id:145057)式，我们得到[驻点](@entry_id:136617)附近外部流场的标准形式 [@problem_id:2525064]：
$$
U_e(x, y) \approx a x
$$
$$
V_e(x, y) \approx -a y
$$
这里，我们定义了一个常数 $a = \left.\frac{\partial U_e}{\partial x}\right|_{(0,0)}$，其单位为时间倒数（$s^{-1}$）。这个常数 $a$ 被称为**[应变率](@entry_id:154778)**（strain rate），它完全刻画了[驻点](@entry_id:136617)附近流场的强度。从不可压缩条件可知，$a = -\left.\frac{\partial V_e}{\partial y}\right|_{(0,0)}$。这个[速度场](@entry_id:271461)描述了一种纯粹的[拉伸流](@entry_id:198535)动：流体沿 $x$ 方向被拉伸，同时沿 $y$ 方向被压缩。

[应变率](@entry_id:154778) $a$ 的值由远离驻点的宏观流动几何和速度决定。一个经典的例子是均匀流 $U_{\infty}$ 绕流一个半径为 $R$ 的圆柱体。根据[势流理论](@entry_id:267452)，可以计算出圆柱体前端[驻点](@entry_id:136617)处的[应变率](@entry_id:154778)为 $a = \frac{2 U_{\infty}}{R}$ [@problem_id:2525064]。这表明，自由来流速度越快或圆柱体半径越小，[驻点](@entry_id:136617)处的流动变形就越剧烈。

为了更深入地理解这种流动的运动学特性，我们可以计算其涡量和[应变率张量](@entry_id:266108) [@problem_id:2525103]。涡量 $\omega_z$ 定义为：
$$
\omega_z = \frac{\partial v}{\partial x} - \frac{\partial u}{\partial y} = \frac{\partial(-ay)}{\partial x} - \frac{\partial(ax)}{\partial y} = 0 - 0 = 0
$$
涡量为零证实了该[理想流](@entry_id:261917)动是无旋的。应变率张量 $S_{ij} = \frac{1}{2}\left(\frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i}\right)$ 的分量为：
$$
S_{xx} = \frac{\partial u}{\partial x} = a
$$
$$
S_{yy} = \frac{\partial v}{\partial y} = -a
$$
$$
S_{xy} = \frac{1}{2}\left(\frac{\partial u}{\partial y} + \frac{\partial v}{\partial x}\right) = \frac{1}{2}(0 + 0) = 0
$$
因此，[应变率张量](@entry_id:266108)为 $\boldsymbol{S} = \begin{pmatrix} a  & 0 \\ 0 & -a \end{pmatrix}$。这是一个[对角矩阵](@entry_id:637782)，表明坐标轴 $x$ 和 $y$ 是该流场的[主应变](@entry_id:197797)轴。[主应变率](@entry_id:264248)分别为 $a$ 和 $-a$，它们大小相等、符号相反，这是不可压缩流动的典型特征。这种运动被称为**纯应变**（pure strain）或无旋[拉伸流](@entry_id:198535)。

### [驻点](@entry_id:136617)[边界层](@entry_id:139416)：独特的标度律

当具有黏性的真实流体冲击固[体壁](@entry_id:272571)面时，由于**[无滑移条件](@entry_id:275670)**（no-slip condition），流体在壁面处的速度必须为零。这导致在壁面附近形成一个[速度梯度](@entry_id:261686)极大的薄层，即**[边界层](@entry_id:139416)**（boundary layer）。[边界层](@entry_id:139416)内的流动物理与外部的无黏流动截然不同。

[驻点](@entry_id:136617)[边界层](@entry_id:139416)的一个显著特征是其厚度在流向方向上保持恒定。这与在平板上发展的**布拉修斯[边界层](@entry_id:139416)**（Blasius boundary layer）形成鲜明对比，后者的厚度会随着离前缘距离的增加而增长。我们可以通过量级分析来理解这一根本差异 [@problem_id:2525060]。

在[边界层](@entry_id:139416)中，黏性力与[惯性力](@entry_id:169104)[相平衡](@entry_id:136822)。对于沿平板的布拉修斯流，外部速度为常数 $U_\infty$。流体微团流过距离 $x$ 所需的特征时间（或停留时间）为 $t_c \sim x/U_\infty$。在这段时间内，动量通过黏性[扩散](@entry_id:141445)穿透的距离，即[边界层厚度](@entry_id:269100) $\delta(x)$，满足[扩散](@entry_id:141445)关系 $\delta^2 \sim \nu t_c$。因此，我们得到：
$$
\delta(x) \sim \sqrt{\nu \frac{x}{U_\infty}}
$$
这表明[边界层厚度](@entry_id:269100)随 $\sqrt{x}$ 增长。

然而，在[驻点](@entry_id:136617)流中，流场由外部[应变率](@entry_id:154778) $a$ 控制。这个[应变率](@entry_id:154778)本身提供了一个内在的[特征时间尺度](@entry_id:276738) $t_a \sim 1/a$。这个时间尺度与流体微团的具体位置 $x$ 无关，它代表了流场变形的速率。将这个时间尺度代入黏性[扩散](@entry_id:141445)关系 $\delta_v^2 \sim \nu t_a$，我们得到驻点流的黏性[边界层厚度](@entry_id:269100) $\delta_v$ [@problem_id:2525060]：
$$
\delta_v \sim \sqrt{\frac{\nu}{a}}
$$
由于 $a$ 和 $\nu$ 都是常数，驻点[边界层](@entry_id:139416)的厚度 $\delta_v$ 在流向（$x$ 方向）上是均匀的。正是外部流场中线性增加的速度 $U_e(x) = ax$ 所产生的恒定应变，导致了[边界层厚度](@entry_id:269100)的恒定。

类似地，我们可以分析热边界层的厚度 $\delta_T$。热边界层的发展由[对流](@entry_id:141806)和[热扩散](@entry_id:148740)之间的平衡决定。将黏性[扩散](@entry_id:141445)系数 $\nu$ 替换为热扩散系数 $\alpha$，我们得到[热边界层](@entry_id:147903)的厚度标度：
$$
\delta_T \sim \sqrt{\frac{\alpha}{a}}
$$
因此，[热边界层](@entry_id:147903)和速度[边界层](@entry_id:139416)的厚度之比仅依赖于流体的物性，即**普朗特数**（Prandtl number） $Pr = \nu/\alpha$：
$$
\frac{\delta_T}{\delta_v} \sim \frac{\sqrt{\alpha/a}}{\sqrt{\nu/a}} = \sqrt{\frac{\alpha}{\nu}} = Pr^{-1/2}
$$

### [动量传递](@entry_id:147714)的希门兹[相似解](@entry_id:171590)

量级分析为我们提供了物理图像和标度关系，但要获得定量的解，我们需要求解[边界层方程](@entry_id:202817)。对于驻点流，存在一个优雅的**[相似解](@entry_id:171590)**（similarity solution），它能将[偏微分方程组](@entry_id:172573)转化为一个[常微分方程](@entry_id:147024)。这个解由 Karl Hiemenz 于1911年首次发现。

我们引入一个**相似变量**（similarity variable） $\eta$，它将法向坐标 $y$ 用[特征长度](@entry_id:265857) $\delta_v \sim \sqrt{\nu/a}$ 进行无量纲化：
$$
\eta = y \sqrt{\frac{a}{\nu}}
$$
同时，我们引入一个**[流函数](@entry_id:266505)**（streamfunction） $\psi(x,y)$，它能自动满足不可压缩流动的连续性方程（$\partial u/\partial x + \partial v/\partial y = 0$）。流函数与速度分量的关系为 $u = \partial\psi/\partial y$ 和 $v = - \partial\psi/\partial x$。基于流动特性，我们假设[流函数](@entry_id:266505)具有如下的相似形式 [@problem_id:2525084]：
$$
\psi(x,y) = \sqrt{a\nu} \, x \, f(\eta)
$$
其中 $f(\eta)$ 是一个待定的无量纲函数。从这个[流函数](@entry_id:266505)，我们可以推导出速度分量：
$$
u = \frac{\partial\psi}{\partial y} = \sqrt{a\nu} \, x \, f'(\eta) \frac{\partial\eta}{\partial y} = \sqrt{a\nu} \, x \, f'(\eta) \sqrt{\frac{a}{\nu}} = a x f'(\eta)
$$
$$
v = -\frac{\partial\psi}{\partial x} = -\sqrt{a\nu} \, f(\eta)
$$
这里的撇号表示对 $\eta$ 的[微分](@entry_id:158718)。注意，$f'(\eta)$ 代表了无量纲的速度剖面 $u/U_e(x)$。而无量纲函数 $f(\eta)$ 本身与法向速度 $v$ 成正比，可以看作是无量纲流函数的幅值 [@problem_id:2525038]。

将这些表达式代入[边界层](@entry_id:139416)动量方程，并利用[伯努利方程](@entry_id:204262)在[边界层](@entry_id:139416)外部给出的压力梯度关系 $- \frac{1}{\rho}\frac{dp}{dx} = U_e \frac{dU_e}{dx} = a^2x$，经过一系列代数运算，所有与 $x$ 相关的项都可以被消去，最终得到一个关于 $f(\eta)$ 的三阶[非线性常微分方程](@entry_id:142950)，即**希门兹方程**（Hiemenz equation）[@problem_id:2525084]：
$$
f''' + f f'' - (f')^2 + 1 = 0
$$

这个方程的物理意义可以逐项解读：
-   $f'''$：源于黏性力项 $\nu \frac{\partial^2 u}{\partial y^2}$，代表动量的**黏性[扩散](@entry_id:141445)**。
-   $f f'' - (f')^2$：源于[惯性力](@entry_id:169104)项 $u\frac{\partial u}{\partial x} + v\frac{\partial u}{\partial y}$，代表流体微团的**惯性加速度**。
-   $+1$：源于压力梯度项 $- \frac{1}{\rho}\frac{dp}{dx}$，代表由外部无黏流场的均匀应变施加在[边界层](@entry_id:139416)上的**驱动力**。

方程的边界条件由物理约束决定：
1.  壁面处的[无滑移条件](@entry_id:275670)：$u(y=0) = 0 \implies f'(0)=0$。
2.  壁面处的[无穿透条件](@entry_id:191795)：$v(y=0) = 0 \implies f(0)=0$。
3.  [边界层](@entry_id:139416)与外部流场的匹配条件：$u(y\to\infty) = U_e(x) \implies f'(\infty)=1$。

这个三阶常微分方程的[边值问题](@entry_id:193901)并不存在解析解，但可以通过数值方法（如**打靶法**，shooting method）求解。理论分析和数值结果都表明，存在一个唯一的、物理上合理的解 [@problem_id:2525065]。该解对应的初始壁面剪应力参数 $f''(0)$ 约为 $1.2326$。其[速度剖面](@entry_id:266404) $f'(\eta)$ 从0开始单调递增，并渐近地趋于1，没有任何超调。这种平滑的剖面反映了在强大的有利[压力梯度](@entry_id:274112)下，[边界层](@entry_id:139416)流动非常稳定，不会发生分离。

### 驻点流中的传热

现在我们将注意力转向传热问题。考虑壁面温度为 $T_w$，[远场](@entry_id:269288)流体温度为 $T_\infty$ 的情况。我们假设物性恒定且忽略黏性耗散。[边界层](@entry_id:139416)内的能量方程为：
$$
u \frac{\partial T}{\partial x} + v \frac{\partial T}{\partial y} = \alpha \frac{\partial^2 T}{\partial y^2}
$$

与[动量方程](@entry_id:197225)类似，温度场也存在[相似解](@entry_id:171590)。我们引入一个无量纲温度 $\theta(\eta)$：
$$
\theta(\eta) = \frac{T(x,y) - T_w}{T_\infty - T_w}
$$
这个定义使得壁面处 $\theta(0)=0$，远场处 $\theta(\infty)=1$。将[相似变换](@entry_id:152935)代入能量方程，一个重要的简化随之出现 [@problem_id:2525038]。由于我们假设壁面温度 $T_w$ 恒定，且相似变量 $\eta$ 仅是 $y$ 的函数，所以无量纲温度 $\theta$ 也仅是 $\eta$ 的函数。这意味着温度场在流向 $x$ 方向上没有梯度，即 $\partial T/\partial x = 0$。因此，能量方程中的流向[对流](@entry_id:141806)项 $u \partial T/\partial x$ 精确地为零。

这意味着，即使流向速度 $u$ 远大于法向速度 $v$，热量的[对流输运](@entry_id:149512)也完全由法向速度 $v$ 控制。能量方程的平衡简化为法向[对流](@entry_id:141806)与法向热扩散之间的平衡。将速度和温度的相似形式代入后，我们得到一个关于 $\theta(\eta)$ 的[二阶线性常微分方程](@entry_id:189146) [@problem_id:2525038]：
$$
\theta'' + Pr f(\eta) \theta' = 0
$$
其中 $Pr = \nu/\alpha$ 是[普朗特数](@entry_id:143303)，它表征了[动量扩散](@entry_id:157895)与[热扩散](@entry_id:148740)能力的相对大小。这个方程的边界条件为 $\theta(0)=0$ 和 $\theta(\infty)=1$。

这个方程的解为 $\theta'(\eta) = C_1 \exp\left(-Pr \int_0^\eta f(s) ds\right)$，其中 $C_1 = \theta'(0)$ 是待定常数。再次积分并应用边界条件，可以求得 $\theta(\eta)$ 的完整解。

工程上，我们最关心的是壁面热流密度 $q''_w$ 和**传热系数**（heat transfer coefficient） $h$。根据傅里叶定律和传热系数的定义 $q''_w = h(T_w - T_\infty)$，我们有：
$$
h = \frac{-k \left.\frac{\partial T}{\partial y}\right|_{y=0}}{T_w - T_\infty}
$$
利用相似变换，我们可以将壁面[温度梯度](@entry_id:136845)与[相似解](@entry_id:171590)联系起来 [@problem_id:2525099]：
$$
\left.\frac{\partial T}{\partial y}\right|_{y=0} = (T_\infty - T_w) \left.\frac{d\theta}{d\eta}\right|_{\eta=0} \left.\frac{\partial\eta}{\partial y}\right|_{y=0} = (T_\infty - T_w) \theta'(0) \sqrt{\frac{a}{\nu}}
$$
代入 $h$ 的表达式，得到驻点处的[传热系数](@entry_id:155200) $h_0$：
$$
h_0 = \frac{-k (T_\infty - T_w) \theta'(0) \sqrt{a/\nu}}{T_w - T_\infty} = k \sqrt{\frac{a}{\nu}} \theta'(0)
$$
其中 $\theta'(0)$ 是一个仅依赖于[普朗特数](@entry_id:143303)的常数。这表明驻点[传热系数](@entry_id:155200) $h_0$ 在驻点处是一个有限的、非零的常数。这与[平板边界层](@entry_id:749449)形成了鲜明对比 [@problem_id:2525120]。对于平板，[传热系数](@entry_id:155200) $h_x$ 在前缘处 ($x \to 0$) 会趋于无穷大 ($h_x \sim x^{-1/2}$)，因为那里的[边界层厚度](@entry_id:269100)为零。[驻点](@entry_id:136617)流的恒定[边界层厚度](@entry_id:269100)导致了有限且通常非常高的传热率。

### 应用与进阶主题

驻点传热理论在许多实际问题中都有直接应用，并且可以推广到更复杂的[湍流](@entry_id:151300)情况。

#### 冲击射流传热

一个典型的应用是**冲击射流**（impinging jet）冷却。当一股直径为 $D$、速度为 $U_j$ 的流体射流垂直冲击一个表面时，其中心区域的流动可以很好地用[驻点](@entry_id:136617)流模型来描述 [@problem_id:2525055]。这里的关键步骤是将射流的宏观参数与[驻点](@entry_id:136617)流的[应变率](@entry_id:154778) $a$ 联系起来。基于[运动学](@entry_id:173318)考虑，[应变率](@entry_id:154778) $a$ 的量级为 $U_j/D$。

利用我们之前得到的[传热系数](@entry_id:155200)公式 $h_0 \sim k\sqrt{a/\nu}$，我们可以推导出中心线**努塞尔数**（Nusselt number） $Nu_0 = h_0 D/k$ 的标度律：
$$
h_0 \sim k \sqrt{\frac{U_j/D}{\nu}} \implies Nu_0 = \frac{h_0 D}{k} \sim \sqrt{\frac{U_j D}{\nu}} = Re_j^{1/2}
$$
其中 $Re_j = U_j D / \nu$ 是基于射流参数的[雷诺数](@entry_id:136372)。更精确的分析和实验表明，努塞尔数还依赖于[普朗特数](@entry_id:143303)。对于 $Pr \gtrsim 1$ 的流体，一个被广泛接受的标度关系是：
$$
Nu_0 \sim Re_j^{1/2} Pr^{1/3}
$$
这个关系式清晰地展示了射流速度和流体物性如何共同决定冲击传热的强度，为射流冷却系统的设计提供了理论基础。

#### [湍流](@entry_id:151300)驻点流与雷诺比拟

当雷诺数很高时，驻点[边界层](@entry_id:139416)可能转捩为**[湍流](@entry_id:151300)**。[湍流](@entry_id:151300)的引入极大地增强了动量和热量的输运，但也使得理论分析变得异常复杂。一个经典的概念是**雷诺比拟**（Reynolds analogy），它假设动量和热量的[湍流输运](@entry_id:150198)机制相似，从而在 $Pr \approx 1$ 且压力梯度为零时，建立了 Stanton 数 $St$（无量纲传热系数）和摩阻系数 $C_f$ 之间的简单关系：$St \approx C_f/2$。

然而，在[湍流](@entry_id:151300)驻点流中，这个经典的雷诺比拟失效了 [@problem_id:2525108]。其根本原因在于驻点流的强应变率 $a$ 对[湍流](@entry_id:151300)结构产生了剧烈的**快速畸变**（rapid distortion）。我们可以用无量纲应变参数 $S^* = ak/\varepsilon$（其中 $k$ 是[湍动能](@entry_id:262712)，$\varepsilon$ 是其耗散率）来衡量这种畸变的相对强度。在驻点流中，$S^*$ 通常远大于1。

[快速畸变理论](@entry_id:754077)（RDT）预测，这种强烈的[拉伸应变](@entry_id:183817)对不同的雷诺应力分量和[湍流](@entry_id:151300)通量有不同的影响。具体而言，它对产生[动量输运](@entry_id:139628)的[雷诺切应力](@entry_id:148861) $\langle u'v' \rangle$ 的抑制作用，要远强于[对产生](@entry_id:154125)热量输运的法向[热通量](@entry_id:138471) $\langle v'T' \rangle$ 的抑制作用。

这种差异性抑制打破了动量和热量输运的相似性。其结果是，相对于[动量输运](@entry_id:139628)，热量输运被显著增强。在模型上，这表现为**[湍流普朗特数](@entry_id:153739)** $Pr_t$ 的减小（即 $Pr_t  1$）。因此，在[驻点](@entry_id:136617)流中，Stanton 数与摩阻系数的比值会远大于经典比拟的预测值，即 $St/(C_f/2) > 1$。这一现象已被实验和[直接数值模拟](@entry_id:149543)证实，它凸显了在[复杂流动](@entry_id:747569)中，必须谨慎使用基于平衡态[湍流](@entry_id:151300)假设的简单模型。