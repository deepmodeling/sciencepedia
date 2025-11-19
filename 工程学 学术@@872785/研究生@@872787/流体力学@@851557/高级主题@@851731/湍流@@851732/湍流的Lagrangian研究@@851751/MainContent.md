## 引言
[湍流](@entry_id:151300)，作为自然界和工程应用中无处不在的现象，其混沌与不可预测性给科学研究带来了巨大挑战。传统的欧拉方法在固定空间点上观测[流体性质](@entry_id:200256)，而[拉格朗日方法](@entry_id:142825)则另辟蹊径，通过追踪单个流体[质点](@entry_id:186768)或粒子的运动轨迹，为理解物质在[湍流](@entry_id:151300)中的输运、混合与弥散等核心问题提供了更直接、更物理的视角。这种“随波逐流”的观点，对于预测[污染物扩散](@entry_id:195534)、理解云中水滴的形成、乃至浮游生物的生态[分布](@entry_id:182848)都至关重要。

本文旨在系统性地介绍[湍流](@entry_id:151300)的拉格朗日研究方法。我们将从根本上回答一个问题：在看似随机的[湍流](@entry_id:151300)场中，粒子的运动背后隐藏着怎样的统计规律？通过本文的学习，读者将掌握分析[粒子轨迹](@entry_id:204827)的核心工具，并理解这些工具如何揭示[湍流](@entry_id:151300)的深层物理机制。

为此，本文将分为三个核心章节。在“原理与机制”一章中，我们将奠定理论基础，详细阐述描述粒子运动的拉格朗-日统计量、谱分析方法以及与[欧拉框架](@entry_id:749109)的内在联系。接下来的“应用与跨学科联系”一章，我们将展示这些原理如何应用于解决从颗粒动力学到生物流体等多样化的实际问题，彰显其跨学科的重要性。最后，“动手实践”部分将提供具体的计算练习，帮助读者巩固所学知识，将理论应用于实践。

## 原理与机制

本章深入探讨了[湍流](@entry_id:151300)[拉格朗日描述](@entry_id:264498)的核心原理与机制。在前一章介绍基本概念的基础上，我们将系统地阐述描述流体质点运动的关键统计量，分析其在[频域](@entry_id:160070)中的表现，并探索[粒子加速](@entry_id:158202)度和相对[扩散](@entry_id:141445)的物理规律。最后，我们将建立[拉格朗日框架](@entry_id:751113)与更为传统的[欧拉框架](@entry_id:749109)之间的深刻联系，揭示[湍流](@entry_id:151300)现象在不同观测视角下的统一性。

### [拉格朗日基](@entry_id:751105)本统计量

在[拉格朗日视角](@entry_id:265471)下，我们追踪单个流体质点的轨迹 $\mathbf{X}(t)$，其速度为 $\mathbf{V}(t) = d\mathbf{X}/dt$，加速度为 $\mathbf{A}(t) = d\mathbf{V}/dt$。为了描述[湍流](@entry_id:151300)的随机性，我们采用统计方法。其中最核心的统计量之一是**[拉格朗日速度自相关](@entry_id:199450)函数**，定义为：
$$
R_L(\tau) = \frac{\langle \mathbf{V}(t) \cdot \mathbf{V}(t+\tau) \rangle}{\langle |\mathbf{V}(t)|^2 \rangle}
$$
这里，$\langle \cdot \rangle$ 表示对大量[粒子轨迹](@entry_id:204827)的系综平均。$R_L(\tau)$ 度量了流体质点在时刻 $t$ 的速度与其在 $\tau$ 时间之后的速度之间的关联程度。当 $\tau=0$ 时，$R_L(0)=1$。随着 $\tau$ 的增大，由于[湍流](@entry_id:151300)的混沌特性，粒子会逐渐“忘记”其初始速度，因此 $R_L(\tau)$ 会趋向于零。

这种“记忆”的持续时间可以通过一个积分量来量化，即**拉格朗日积分时间尺度** $T_L$：
$$
T_L = \int_0^\infty R_L(\tau) d\tau
$$
$T_L$ 表征了[粒子速度](@entry_id:196946)保持相关的典型时间。它是理解湍流混合和[扩散](@entry_id:141445)等过程的关键参数。

在充分发展的均匀[各向同性湍流](@entry_id:199323)中，这些[拉格朗日量](@entry_id:174593)与流动的宏观欧拉统计量之间存在着基本关系。流动的两个关键欧拉参数是单位质量的湍动能 $k = \frac{1}{2} \langle |\mathbf{u}|^2 \rangle$（这里 $\mathbf{u}$ 是欧拉[速度场](@entry_id:271461)）和单位质量的平均能量耗散率 $\epsilon$。在高雷诺数下，决定 $T_L$ 和 $k$ 的大尺度运动被认为主要由能量的供给速率（在统计定常态下等于[耗散率](@entry_id:748577) $\epsilon$）和能量本身的尺度 $k$ 控制，而与流体的粘性无关。基于这一物理思想，我们可以通过量纲分析来推断它们之间的关系。

我们假设 $T_L$ 是 $k$ 和 $\epsilon$ 的[幂律](@entry_id:143404)函数，形式为 $T_L = C_L k^a \epsilon^b$，其中 $C_L$ 是一个无量纲常数。各个物理量的量纲为：
- 时间尺度 $[T_L] = T$
- 单位质量湍动能 $[k] = L^2 T^{-2}$
- 单位质量能量耗散率 $[\epsilon] = [k]/T = L^2 T^{-3}$

根据[量纲一致性](@entry_id:271193)原则，我们有：
$$
T^1 = (L^2 T^{-2})^a (L^2 T^{-3})^b = L^{2a+2b} T^{-2a-3b}
$$
通过匹配两侧各[基本量纲](@entry_id:273221)（长度L，时间T）的指数，我们得到一个[方程组](@entry_id:193238)：
$$
\begin{align*}
2a + 2b  = 0 \\
-2a - 3b  = 1
\end{align*}
$$
解这个[方程组](@entry_id:193238)可得 $a=1$ 和 $b=-1$。因此，我们得到了拉格朗日积分时间尺度与湍动能和耗散率之间的基本关系 [@problem_id:555919]：
$$
T_L = C_L \frac{k}{\epsilon}
$$
这个结果意义深远：它表明流体[质点](@entry_id:186768)的“记忆时间”正比于其携带的能量，反比于该能量被耗散的速率。这为[湍流建模](@entry_id:151192)提供了一个基石，将拉格朗日时间尺度与更容易测量的欧拉量联系起来。

另一个重要的统计量是**二阶拉格朗日速度[结构函数](@entry_id:161908)**，$D_{LL}(\tau) = \langle |\mathbf{V}(t+\tau) - \mathbf{V}(t)|^2 \rangle$。对于统计定常过程，它与[自相关函数](@entry_id:138327)的关系为 $D_{LL}(\tau) = 2[\langle |\mathbf{V}|^2 \rangle - \langle \mathbf{V}(t) \cdot \mathbf{V}(t+\tau) \rangle] = 2\langle |\mathbf{V}|^2 \rangle [1 - R_L(\tau)]$。[结构函数](@entry_id:161908)描述了[速度增量](@entry_id:176263)的统计特性，在研究[湍流](@entry_id:151300)的尺度行为时尤为重要。

### [频域分析](@entry_id:265642)：拉格朗日谱

除了在时域中分析相关性，我们还可以在[频域](@entry_id:160070)中考察粒子运动的能量[分布](@entry_id:182848)。根据[维纳-辛钦定理](@entry_id:188017)（Wiener-Khinchin theorem），[拉格朗日速度自相关](@entry_id:199450)函数 $R_{ij}(\tau) = \langle V_i(t) V_j(t+\tau) \rangle$ 的[傅里叶变换](@entry_id:142120)是**拉格朗日[频率谱](@entry_id:276824)张量** $E_{ij}(\omega)$：
$$
E_{ij}(\omega) = \frac{1}{2\pi} \int_{-\infty}^{\infty} R_{ij}(\tau) e^{-i\omega\tau} d\tau
$$
其[逆变](@entry_id:192290)换为 $R_{ij}(\tau) = \int_{-\infty}^{\infty} E_{ij}(\omega) e^{i\omega\tau} d\omega$。谱[张量的迹](@entry_id:190669) $\text{Tr}(E(\omega))$ 描述了在[角频率](@entry_id:261565) $\omega$ 附近，单位频率间隔内流体[质点](@entry_id:186768)所携带的动能。

总湍动能 $k$ 可以通过对谱进行积分得到。注意到 $k = \frac{1}{2}\langle \mathbf{V}(t) \cdot \mathbf{V}(t) \rangle = \frac{1}{2} R_{ii}(0)$。利用逆变换关系，在 $\tau=0$ 时我们有 $R_{ii}(0) = \int_{-\infty}^{\infty} E_{ii}(\omega) d\omega = \int_{-\infty}^{\infty} \text{Tr}(E(\omega)) d\omega$。因此，
$$
k = \frac{1}{2} \int_{-\infty}^{\infty} \text{Tr}(E(\omega)) d\omega
$$
拉格朗日积[分时](@entry_id:274419)间尺度 $T_L$ 也与谱在零频率处的值直接相关。对于[各向同性湍流](@entry_id:199323)中的单个速度分量，$\langle V_1^2 \rangle = \frac{2}{3}k$，且 $T_L = \frac{1}{\langle V_1^2 \rangle} \int_0^\infty R_{11}(\tau)d\tau$。由[傅里叶变换的性质](@entry_id:265641)可知 $\int_0^\infty R_{11}(\tau)d\tau = \pi E_{11}(0)$。在各向同性条件下，$E_{11}(\omega) = \frac{1}{3}\text{Tr}(E(\omega))$，综合这些关系可以得到：
$$
T_L = \frac{\pi E_{11}(0)}{\langle V_1^2 \rangle} = \frac{\pi \left( \frac{1}{3}\text{Tr}(E(0)) \right)}{\frac{2}{3}k} = \frac{\pi \text{Tr}(E(0))}{2k}
$$
这个关系式表明，积[分时](@entry_id:274419)间尺度由零频率处的谱密度决定，这合乎物理直觉，因为长时间的记忆对应于低频行为。

为了具体说明这些关系，我们可以考虑一个假设的谱模型 [@problem_id:555959]。例如，假设谱的迹为一个[高斯函数](@entry_id:261394) $\text{Tr}(E(\omega)) = C e^{-D\omega^2}$，其中 $C$ 和 $D$ 为正常数。利用上述公式，我们可以计算出 $k = \frac{C}{2} \sqrt{\frac{\pi}{D}}$ 和 $\text{Tr}(E(0))=C$。将它们代入 $T_L$ 的表达式中，我们发现常数 $C$ 和[湍动能](@entry_id:262712) $k$ 被消去，最终得到 $T_L = \sqrt{\pi D}$。这表明，对于一个给定的谱形状，积分时间尺度由谱的宽度（由参数 $D$ 控制）唯一确定。

在[湍流理论](@entry_id:264896)中，Kolmogorov 1941年理论 (K41) 对**[惯性子区](@entry_id:273327)**内的统计行为做出了重要预测。在[惯性子区](@entry_id:273327)对应的时间尺度内（比 $T_L$ 小，但比耗散时间尺度大），流体[质点](@entry_id:186768)的统计行为仅由[能量耗散](@entry_id:147406)率 $\epsilon$ 决定。这导致二阶拉格朗日[结构函数](@entry_id:161908)具有如下[标度律](@entry_id:139947) [@problem_id:556013]：
$$
D_{LL}(\tau) = C_0 \epsilon |\tau|
$$
其中 $C_0$ 是一个普适的无量纲常数。这个[线性关系](@entry_id:267880)是[拉格朗日框架](@entry_id:751113)下[惯性区](@entry_id:273327)的一个标志性特征。利用 $D_{LL}(\tau)$ 与 $R_L(\tau)$ 的关系，这意味着在小 $\tau$ 时，$R_L(\tau) \approx 1 - \frac{C_0 \epsilon |\tau|}{2\langle |\mathbf{V}|^2 \rangle}$。

这个在小时域的行为决定了谱在高[频域](@entry_id:160070)的行为。通过对 $R_L(\tau)$ 进行[傅里叶变换](@entry_id:142120)，可以推导出在高频极限下，单边拉格朗日能谱 $E_L(\omega)$ 的形式 [@problem_id:556013]：
$$
E_L(\omega) \sim \frac{C_0\epsilon}{\pi\omega^2}
$$
这个 $\omega^{-2}$ 标度律是[湍流](@entry_id:151300)拉格朗日理论的一个经典结果，它深刻地揭示了能量从低频向高频的级联过程在粒子运动谱上的体现。

### 拉格朗日加速度统计

流体[质点](@entry_id:186768)的加速度 $\mathbf{A}(t)$ 反映了作用在[质点](@entry_id:186768)上的合力，是理解[湍流](@entry_id:151300)中动力学过程（如粒子混合、[液滴破碎](@entry_id:748676)）的关键。根据[Navier-Stokes方程](@entry_id:161487)，对于不可压缩[牛顿流体](@entry_id:263796)，拉格朗日[加速度场](@entry_id:266595) $\mathbf{a}(\mathbf{x}, t)$ 可以分解为来自[压力梯度](@entry_id:274112)的贡献 $\mathbf{a}_p = -\frac{1}{\rho}\nabla p$ 和来自粘性力的贡献 $\mathbf{a}_v = \nu \nabla^2 \mathbf{u}$：
$$
\mathbf{a} = \mathbf{a}_p + \mathbf{a}_v
$$
均方加速度 $\langle |\mathbf{a}|^2 \rangle$ 因此可以分解为 $\langle |\mathbf{a}_p|^2 \rangle + \langle |\mathbf{a}_v|^2 \rangle + 2\langle \mathbf{a}_p \cdot \mathbf{a}_v \rangle$。其中[交叉](@entry_id:147634)项 $\langle \mathbf{a}_p \cdot \mathbf{a}_v \rangle$ 描述了压力和粘性力贡献之间的相关性。

一个重要的基本结果是，在统计均匀的不可压缩[湍流](@entry_id:151300)中，这个[交叉](@entry_id:147634)项恒等于零 [@problem_id:556011]。该证明依赖于均匀场中空间导数平均值为零的性质以及不可压缩条件 $\nabla \cdot \mathbf{u} = 0$。
$$
\langle \mathbf{a}_p \cdot \mathbf{a}_v \rangle = -\frac{\nu}{\rho} \langle (\nabla p) \cdot (\nabla^2 \mathbf{u}) \rangle = -\frac{\nu}{\rho} \left\langle \frac{\partial p}{\partial x_i} \nabla^2 u_i \right\rangle
$$
利用矢量恒等式和分部积分（在平均意义下），可以证明 $\langle \frac{\partial p}{\partial x_i} \nabla^2 u_i \rangle = -\langle p \nabla^2(\frac{\partial u_i}{\partial x_i}) \rangle$。由于[不可压缩性](@entry_id:274914)，$\frac{\partial u_i}{\partial x_i}=0$，因此整个表达式为零。
$$
\langle \mathbf{a}_p \cdot \mathbf{a}_v \rangle = 0
$$
这意味着在统计平均的意义上，由[压力梯度](@entry_id:274112)和[粘性力](@entry_id:263294)产生的加速度分量是**不相关**的。这极大地简化了对加速度统计特性的分析，使得总的均方加速度就是各项均方加速度之和。

加速度还与流场的局部几何结构密切相关。例如，在均匀[湍流](@entry_id:151300)中，一个有用的恒等式将速度场的一个[二阶相关](@entry_id:190427)量与能量耗散率联系起来。通过对 $\langle v_i \nabla^2 v_i \rangle$ 进行[分部积分](@entry_id:136350)并利用均匀场的性质，可以证明 [@problem_id:555963]：
$$
\langle v_i \nabla^2 v_i \rangle = -\langle (\partial_j v_i)(\partial_j v_i) \rangle = -\frac{\epsilon}{\nu}
$$
这里我们使用了 $\epsilon = \nu \langle (\partial_j v_i)(\partial_j v_i) \rangle$ 这个关于[耗散率](@entry_id:748577)的定义。

在高雷诺数下，粘性项通常很小，加速度主要由压力梯度决定，即 $\mathbf{a} \approx -\frac{1}{\rho}\nabla p$。这表明粒子的加速度直接探测了当地的压力梯度。更进一步，我们可以探究加速度与压[力场](@entry_id:147325)更[高阶导数](@entry_id:140882)（如压力Hessian矩阵 $H_{ij} = \partial_i \partial_j p$）之间的关系。由于[湍流](@entry_id:151300)的非高斯性，压力梯度 $\mathbf{G}=\nabla p$ 和Hessian矩阵 $H_{ij}$ 并非统计独立。一个合理的闭合模型可以假设给定梯度 $\mathbf{G}$ 下Hessian的条件期望具有各向同性的形式 [@problem_id:555945]：
$$
\langle H_{ij} | \mathbf{G} \rangle = \alpha(G) \delta_{ij} + \beta(G) \frac{G_i G_j}{G^2}
$$
其中 $G = |\mathbf{G}|$，$ \alpha$ 和 $\beta$ 是 $G$ 的标量函数。利用这个模型和关系 $G=\rho a$，我们可以推导出在给定加速度大小 $a$ 的条件下，条件平均的压力拉普拉斯算子 $\langle \nabla^2 p | a \rangle = \langle H_{ii} | a \rangle$ 为：
$$
\langle \nabla^2 p | a \rangle = 3\alpha(\rho a) + \beta(\rho a)
$$
这个结果展示了如何通过理论模型将可测量的[拉格朗日量](@entry_id:174593)（加速度）与流场[精细结构](@entry_id:140861)的不可测量统计特性（条件平均的压力曲率）联系起来。

### [湍流](@entry_id:151300)[扩散](@entry_id:141445)：粒子对的相对运动

除了单个粒子的运动，[湍流](@entry_id:151300)研究的另一个核心问题是粒子对的相对运动，这直接关系到污染物云团的扩展、混合过程等。我们考虑一对初始位置非常接近的粒子，其[分离矢量](@entry_id:268468)为 $\mathbf{r}(t)$，分离距离为 $R(t)=|\mathbf{r}(t)|$。

L. F. Richardson 的开创性工作表明，粒子对的[扩散](@entry_id:141445)行为与经典的布朗运动（Fickian[扩散](@entry_id:141445)）有本质区别。在[湍流](@entry_id:151300)[惯性子区](@entry_id:273327)内，粒子对的分离不是由一个恒定的[扩散](@entry_id:141445)系数决定的，而是由一个依赖于分离尺度 $R$ 本身的**尺度依赖[涡动扩散系数](@entry_id:196515)** $K(R)$ 控制。根据[Kolmogorov理论](@entry_id:200055)，其形式为：
$$
K(R) = C_K \epsilon^{1/3} R^{4/3}
$$
其中 $C_K$ 是一个无量纲常数。物理上，这意味着大尺度的涡旋对远距离粒子对的[扩散](@entry_id:141445)起主导作用，而小尺度涡旋则影响近距离的粒子对。

我们可以通过一个简化的[Fokker-Planck](@entry_id:635508)型方程来描述[分离矢量](@entry_id:268468) $\mathbf{r}$ 的[概率密度函数](@entry_id:140610) $P(\mathbf{r}, t)$ 的演化 [@problem_id:555910]：
$$
\frac{\partial P(\mathbf{r}, t)}{\partial t} = \nabla \cdot [K(R) \nabla P(\mathbf{r}, t)]
$$
通过求解该方程的二阶矩 $\langle R^2(t) \rangle = \int R^2 P(\mathbf{r}, t) d^3\mathbf{r}$ 的演化方程，可以推导出均方分离距离随时间的增长规律。这个推导过程需要一个闭合近似，如 $\langle R^{4/3} \rangle \approx (\langle R^2 \rangle)^{2/3}$。最终得到的结果是著名的**Richardson定律**：
$$
\langle R^2(t) \rangle \propto \epsilon t^3
$$
更精确的推导给出了系数 [@problem_id:555910]，例如，对于所给的模型，$\langle R^2(t) \rangle = (\frac{26}{9})^3 C_K^3 \epsilon t^3$。

$\langle R^2(t) \rangle \propto t^3$ 这一结果表明，粒子对的均方分离距离随时间的三次方增长，这是一种**[超扩散](@entry_id:155498)**行为，远快于布朗运动的[线性增长](@entry_id:157553)（$\langle R^2(t) \rangle \propto t$）。这形象地描述了[湍流](@entry_id:151300)中“分离的分离会加速”的现象：随着粒子对分得越来越开，它们会感受到越来越大尺度的涡旋的作用，从而以更快的速度分离。

### 连接[拉格朗日与欧拉](@entry_id:270774)框架

[湍流理论](@entry_id:264896)的一个核心挑战是在拉格朗日和欧拉这两种描述之间建立定量的桥梁。

一个经典的理论工具是**科尔辛独立性近似**（Corrsin Independence Approximation, CIA）。该近似假设，[拉格朗日速度自相关](@entry_id:199450)函数 $R_L(\tau)$ 可以通过对两点、两时的欧拉[相关函数](@entry_id:146839) $R_E(\mathbf{r}, \tau)$ 在粒子位移的[概率分布](@entry_id:146404)上进行平均来得到 [@problem_id:555991]：
$$
R_L(\tau) = \int_{-\infty}^{\infty} R_E(\mathbf{r}, \tau) P(\mathbf{r}, \tau) d^3\mathbf{r}
$$
这里的 $P(\mathbf{r}, \tau)$ 是粒子在时间 $\tau$ 内发生位移 $\mathbf{r}$ 的[概率密度函数](@entry_id:140610)。这个近似的物理思想是，粒子的速度是其当前所在位置的欧拉速度，而其位移本身是一个[随机过程](@entry_id:159502)。

通过使用简化的模型，例如“冻结[湍流](@entry_id:151300)”假设（$R_E$ 不依赖于 $\tau$）并为欧拉空间相关和粒子位移概率密度采用高斯模型，我们可以利用CIA推导出拉格朗日和[欧拉积分](@entry_id:271845)尺度之间的关系。经过一系列推导，包括求解一个由G.I. Taylor[扩散](@entry_id:141445)理论和CIA共同构成的[微分方程](@entry_id:264184)，可以得到一个非常简洁而深刻的结果 [@problem_id:555991]：
$$
T_L = \frac{L_E}{u_{rms}}
$$
其中 $L_E$ 是[欧拉积分](@entry_id:271845)长度尺度，$u_{rms}$ 是速度脉动的[均方根值](@entry_id:276804)。这个关系直观地表明，一个流体质点穿越一个典型大涡旋（尺度为 $L_E$）所需要的时间（以其典型速度 $u_{rms}$），正是其速度保持相关的拉格朗日积分时间。

更深层次的联系体现在对[湍流](@entry_id:151300)[基本对称性](@entry_id:161256)的探讨上。[湍流](@entry_id:151300)级联的不可逆性（能量从大尺度流向小尺度）导致了统计上的**时间不[可逆性](@entry_id:143146)**。这在[拉格朗日框架](@entry_id:751113)中表现为某些[时间相关函数](@entry_id:144636)的非对称性。例如，加速度-[速度相关函数](@entry_id:196429) $C_{AV}(\tau) = \langle \mathbf{A}(t) \cdot \mathbf{V}(t+\tau) \rangle$ 通常不是 $\tau$ 的偶函数。其时间反对称部分 $C_{AV}^A(\tau) = \frac{1}{2} [C_{AV}(\tau) - C_{AV}(-\tau)]$ 捕捉了这种不可逆性。

这种拉格朗日时间不[可逆性](@entry_id:143146)必须与[欧拉框架](@entry_id:749109)中能量级联的直接标志相关联。这个标志就是非零的**三阶欧拉速度[结构函数](@entry_id:161908)** $S_3(r) = \langle [(\mathbf{u}(\mathbf{x}+\mathbf{r}) - \mathbf{u}(\mathbf{x})) \cdot \frac{\mathbf{r}}{r}]^3 \rangle$。Kolmogorov的4/5定律指出，在[惯性子区](@entry_id:273327)中 $S_3(r) = -\frac{4}{5}\epsilon r$。通过结合关于拉格朗日[结构函数](@entry_id:161908)和位移矩的[标度律](@entry_id:139947)的假设，可以推导出 $C_{AV}^A(\tau)$ 与 $S_3(r)/r$ 成正比 [@problem_id:555938]：
$$
C_{AV}^A(\tau) = \mathcal{C} \frac{S_3(r)}{r}
$$
其中比例常数 $\mathcal{C}$ 可以用其他普适常数（如Kolmogorov常数 $C_2$）表示。这个结果有力地证明了拉格朗日时间反演对称性的破缺是欧拉能量级联[方向性](@entry_id:266095)的直接体现。

最后，流动的基本物理定律，如质量守恒（不可压缩性）和动量守恒，结合各向同性对称性，对可能的[统计相关性](@entry_id:267552)施加了极强的约束。一个精妙的例子是[应变率张量](@entry_id:266108) $S_{ij}$ 与压力Hessian张量 $\partial_k \partial_l p$ 之间的单点相关性 $\langle S_{ij} \partial_k \partial_l p \rangle$。这是一个[四阶张量](@entry_id:181350)，在[各向同性湍流](@entry_id:199323)中，它的形式必须是 $\delta_{ij}$, $\delta_{kl}$ 等的组合。通过利用 $S_{ij}$ 的无迹性（源于[不可压缩性](@entry_id:274914) $\partial_m u_m=0$）和[对相关](@entry_id:203353)量进行[分部积分](@entry_id:136350)并再次使用不可压缩性，可以构建关于其各向同性形式系数的约束方程。最终的推导表明，这些系数必须全部为零 [@problem_id:556012]。
$$
\langle S_{ij} \partial_k \partial_l p \rangle = 0
$$
这个结果表明，尽管[应变率](@entry_id:154778)和压[力场](@entry_id:147325)都是由[速度场](@entry_id:271461)决定的复杂量，但在[各向同性湍流](@entry_id:199323)中，应变率张量和压力Hessian张量在统计上是正交的。这再次彰显了在[湍流](@entry_id:151300)研究中，运用基本原理和对称性约束来简化和理解复杂统计关系的强大威力。