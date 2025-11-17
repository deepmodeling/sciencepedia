## 引言
在[材料力学](@entry_id:201885)和工程设计中，许多关键部件（如压力容器、旋转盘、带孔或裂纹的结构）都具有圆形或轴对称的几何特征。使用传统的笛卡尔坐标系来分析这些问题往往会导致边界条件异常复杂，从而使求解变得异常困难。因此，掌握如何在更自然的极[坐标系](@entry_id:156346)下建立和求解弹性力学问题，成为高级力学分析的一项核心技能。本文旨在系统性地解决这一问题，即如何将弹性力学的基本控制方程从笛卡尔坐标系转换到极[坐标系](@entry_id:156346)，并介绍求解这些新形式方程的经典方法。

通过学习本文，您将深入理解[坐标系](@entry_id:156346)变换的几何本质，并掌握一套强大的分析工具。在“原理与机制”一章中，我们将从几何基础出发，详细推导极[坐标系](@entry_id:156346)下的[应变-位移关系](@entry_id:173321)、平衡方程和[本构关系](@entry_id:186508)，并引入[艾里应力函数](@entry_id:191331)法，最终将问题归结为求解一个优雅的[双调和方程](@entry_id:165706)。接着，在“应用与跨学科联系”一章中，我们将展示这些理论如何应用于解决工程中的经典问题，如[厚壁圆筒](@entry_id:189222)、旋转盘的[应力分析](@entry_id:168804)、孔口应力集中以及断裂力学中的裂纹尖端场分析。最后，“动手实践”部分将提供具体的计算问题，帮助您巩固所学知识，将理论应用于实际计算。

## 原理与机制

从笛卡尔坐标系到极[坐标系](@entry_id:156346)的转换，不仅仅是变量的代换，更是对描述物理定律的几何框架的根本性重塑。在[材料力学](@entry_id:201885)中，尤其是在处理具有圆形边界、孔洞或裂纹等[轴对称](@entry_id:173333)或近轴对称几何特征的问题时，极[坐标系](@entry_id:156346)提供了无与伦比的便利性。然而，这种便利性的代价是，控制方程的形式会变得更加复杂，因为它们必须反映[坐标系](@entry_id:156346)的内在曲率。本章旨在系统地阐述弹性力学在极[坐标系](@entry_id:156346)下的基本原理和控制方程，并介绍求解这些方程的经典方法。

### 几何基础：极[坐标系](@entry_id:156346)

在二维平面中，一个点的位置可以通过其在笛卡尔坐标系中的坐标 $(x, y)$ 来描述，或者通过其在极[坐标系](@entry_id:156346)中的坐标 $(r, \theta)$ 来描述。两者之间的关系为 $x = r\cos\theta$ 和 $y = r\sin\theta$。位置向量 $\mathbf{r}$ 可以表示为 $\mathbf{r} = x\,\mathbf{i} + y\,\mathbf{j} = (r\cos\theta)\,\mathbf{i} + (r\sin\theta)\,\mathbf{j}$，其中 $\mathbf{i}$ 和 $\mathbf{j}$ 是[笛卡尔坐标系](@entry_id:169789)的固定[基向量](@entry_id:199546)。

与[基向量](@entry_id:199546)在整个空间中保持不变的笛卡尔坐标系不同，极[坐标系](@entry_id:156346)的自然[基向量](@entry_id:199546)是随位置变化的。为了构建这些[基向量](@entry_id:199546)，我们首先定义[协变基](@entry_id:198968)向量 $\mathbf{a}_i = \partial\mathbf{r}/\partial q^i$，其中 $q^1 = r, q^2 = \theta$。

$$
\mathbf{a}_r = \frac{\partial \mathbf{r}}{\partial r} = \cos\theta\,\mathbf{i} + \sin\theta\,\mathbf{j}
$$

$$
\mathbf{a}_\theta = \frac{\partial \mathbf{r}}{\partial \theta} = -r\sin\theta\,\mathbf{i} + r\cos\theta\,\mathbf{j}
$$

度量张量（metric tensor）的分量 $g_{ij} = \mathbf{a}_i \cdot \mathbf{a}_j$ 描述了[坐标系](@entry_id:156346)的局部几何。计算可得：

$$
g_{rr} = \mathbf{a}_r \cdot \mathbf{a}_r = \cos^2\theta + \sin^2\theta = 1
$$

$$
g_{\theta\theta} = \mathbf{a}_\theta \cdot \mathbf{a}_\theta = r^2\sin^2\theta + r^2\cos^2\theta = r^2
$$

$$
g_{r\theta} = \mathbf{a}_r \cdot \mathbf{a}_\theta = 0
$$

由于非对角项 $g_{r\theta}=0$，极[坐标系](@entry_id:156346)是一个**[正交坐标](@entry_id:166074)系**。在实际应用中，我们更常使用归一化的**标准正交基向量** $\mathbf{e}_r$ 和 $\mathbf{e}_\theta$，它们通过[协变基](@entry_id:198968)向量除以其模长（即[尺度因子](@entry_id:266678) $h_i = \sqrt{g_{ii}}$）得到：

$$
\mathbf{e}_r = \frac{\mathbf{a}_r}{\sqrt{g_{rr}}} = \cos\theta\,\mathbf{i} + \sin\theta\,\mathbf{j}
$$

$$
\mathbf{e}_\theta = \frac{\mathbf{a}_\theta}{\sqrt{g_{\theta\theta}}} = -\sin\theta\,\mathbf{i} + \cos\theta\,\mathbf{j}
$$

这里的核心要点是，$\mathbf{e}_r$ 和 $\mathbf{e}_\theta$ 的方向取决于角坐标 $\theta$。当一个观察点在平面内移动时，这两个[基向量](@entry_id:199546)会随之旋转。这意味着它们对坐标的导数不为零 [@problem_id:2889560]：

$$
\frac{\partial \mathbf{e}_r}{\partial \theta} = \mathbf{e}_\theta, \quad \frac{\partial \mathbf{e}_\theta}{\partial \theta} = -\mathbf{e}_r
$$

$$
\frac{\partial \mathbf{e}_r}{\partial r} = \mathbf{0}, \quad \frac{\partial \mathbf{e}_\theta}{\partial r} = \mathbf{0}
$$

[基向量](@entry_id:199546)的这种位置依赖性是极[坐标系](@entry_id:156346)与笛卡尔坐标系的根本几何差异。在对向量或张量场进行[微分](@entry_id:158718)运算（如求梯度或散度）时，必须通过链式法则考虑[基向量](@entry_id:199546)自身的变化。这些额外的项在形式上由[克里斯托费尔符号](@entry_id:159831)（Christoffel symbols）捕捉，它们是控制方程中出现“曲率”修正项的根本原因。

### 弹性力学控制方程

与在任何[坐标系](@entry_id:156346)中一样，求解弹性力学问题需要三个基本要素：[运动学方程](@entry_id:173032)（[应变-位移关系](@entry_id:173321)）、[动力学方程](@entry_id:751029)（[平衡方程](@entry_id:172166)）和[本构关系](@entry_id:186508)（[应力-应变关系](@entry_id:274093)）。我们将逐一建立它们在极坐标下的形式。

#### 运动学：[应变-位移关系](@entry_id:173321)

在[小变形理论](@entry_id:174991)中，应变张量 $\boldsymbol{\varepsilon}$ 定义为[位移梯度](@entry_id:165352) $\nabla\mathbf{u}$ 的对称部分：$\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T)$。位移场在极坐标中表示为 $\mathbf{u} = u_r(r,\theta)\mathbf{e}_r + u_\theta(r,\theta)\mathbf{e}_\theta$。极坐标中的[梯度算子](@entry_id:275922)为 $\nabla = \mathbf{e}_r \frac{\partial}{\partial r} + \mathbf{e}_\theta \frac{1}{r} \frac{\partial}{\partial \theta}$。

计算[位移梯度](@entry_id:165352)时，我们必须对位移分量和[基向量](@entry_id:199546)同时求导。例如，对[位移场](@entry_id:141476)沿 $\theta$ 方向求导时：

$$
\frac{\partial \mathbf{u}}{\partial \theta} = \frac{\partial (u_r \mathbf{e}_r + u_\theta \mathbf{e}_\theta)}{\partial \theta} = \frac{\partial u_r}{\partial \theta}\mathbf{e}_r + u_r \frac{\partial \mathbf{e}_r}{\partial \theta} + \frac{\partial u_\theta}{\partial \theta}\mathbf{e}_\theta + u_\theta \frac{\partial \mathbf{e}_\theta}{\partial \theta}
$$

代入[基向量](@entry_id:199546)的导数 $\frac{\partial \mathbf{e}_r}{\partial \theta} = \mathbf{e}_\theta$ 和 $\frac{\partial \mathbf{e}_\theta}{\partial \theta} = -\mathbf{e}_r$，并整理各项，最终可以得到[应变张量](@entry_id:193332)的三个独立分量 [@problem_id:2889564]：

径向[正应变](@entry_id:204633) $\varepsilon_{rr}$：
$$
\varepsilon_{rr} = \frac{\partial u_r}{\partial r}
$$

环向（或周向）[正应变](@entry_id:204633) $\varepsilon_{\theta\theta}$：
$$
\varepsilon_{\theta\theta} = \frac{1}{r}\frac{\partial u_\theta}{\partial \theta} + \frac{u_r}{r}
$$

[剪应变](@entry_id:175241) $\varepsilon_{r\theta}$：
$$
\varepsilon_{r\theta} = \frac{1}{2} \left( \frac{1}{r}\frac{\partial u_r}{\partial \theta} + \frac{\partial u_\theta}{\partial r} - \frac{u_\theta}{r} \right)
$$

观察这些表达式，我们可以清晰地看到曲率效应。例如，在 $\varepsilon_{\theta\theta}$ 中，即使环向位移分量 $u_\theta$ 没有变化，仅有径向位移 $u_r > 0$ 也会导致环向的拉伸，其大小为 $u_r/r$。这可以直观地理解为，一个半径为 $r$ 的[圆环](@entry_id:163678)，在径向均匀膨胀了 $u_r$ 后，其周长从 $2\pi r$ 增加到 $2\pi (r+u_r)$，单位长度的伸长量即为 $(2\pi (r+u_r) - 2\pi r) / (2\pi r) = u_r/r$。同样，在 $\varepsilon_{r\theta}$ 中的 $-u_\theta/r$ 项，是由于环向位移 $u_\theta$ 引起了径向[线元](@entry_id:196833)（$\mathbf{e}_r$ 方向的线元）的刚性转动，从而产生了[剪切变形](@entry_id:170920)。

#### 动力学：[平衡方程](@entry_id:172166)

在静态或准静态条件下，物体的任何一部分都必须处于力平衡状态。这一原理的[微分形式](@entry_id:146747)是应力[张量的散度](@entry_id:191736)为零（假设体力为零）：$\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$。为了得到其在极坐标下的分量形式，我们可以考虑一个微小的扇形单元，其边界由 $r$, $r+dr$, $\theta$, 和 $\theta+d\theta$ 围成。

通过对作用在该单元上的所有面力（由应力 $\sigma_{rr}, \sigma_{\theta\theta}, \sigma_{r\theta}$ 产生）进行平衡分析，并考虑因坐标线弯曲和[基向量](@entry_id:199546)变化带来的几何效应，我们可以推导出两个平衡方程。若存在体力 $\mathbf{b} = b_r \mathbf{e}_r + b_\theta \mathbf{e}_\theta$，则方程为 [@problem_id:2889545]：

径向平衡方程：
$$
\frac{\partial \sigma_{rr}}{\partial r} + \frac{1}{r}\frac{\partial \sigma_{r\theta}}{\partial \theta} + \frac{\sigma_{rr}-\sigma_{\theta\theta}}{r} + b_r = 0
$$

[环向平衡](@entry_id:756055)方程：
$$
\frac{\partial \sigma_{r\theta}}{\partial r} + \frac{1}{r}\frac{\partial \sigma_{\theta\theta}}{\partial \theta} + \frac{2\sigma_{r\theta}}{r} + b_\theta = 0
$$

与[笛卡尔坐标系](@entry_id:169789)下的平衡方程 $\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} = 0$ 相比，这里的额外项 $\frac{\sigma_{rr}-\sigma_{\theta\theta}}{r}$ 和 $\frac{2\sigma_{r\theta}}{r}$ 同样是曲率的体现。第一项说明，即使应力分量处处均匀，如果[径向应力](@entry_id:197086)不等于[环向应力](@entry_id:190931)，也会因几何形状而产生一个净径向力。第二项中的因子“2”则源于剪应力随半径的变化以及径向[线元](@entry_id:196833)随角度的转动两个效应的叠加。

#### 本构关系：[胡克定律](@entry_id:149682)

对于线弹性、各向同性材料，[应力与应变](@entry_id:137374)之间的关系由[胡克定律](@entry_id:149682)描述。其普适的张量形式为：
$$
\sigma_{ij} = \lambda \varepsilon_{kk} \delta_{ij} + 2\mu \varepsilon_{ij}
$$
其中，$\lambda$ 和 $\mu$ 是拉梅（Lamé）常数，$\varepsilon_{kk} = \varepsilon_{rr} + \varepsilon_{\theta\theta} + \varepsilon_{zz}$ 是[体积应变](@entry_id:267252)，$\delta_{ij}$ 是克罗内克符号。

由于这个本构关系是一个张量方程，它在任何[正交坐标](@entry_id:166074)系下都具有相同的分量形式。因此，在极[坐标系](@entry_id:156346)中，我们只需将下标 $(i, j)$ 替换为 $(r, \theta, z)$ 即可。

在二维问题中，我们常常处理**平面应变**或**平面应力**状态。以[平面应变](@entry_id:167046)（plane strain）为例，其定义是所有平面外（$z$ 方向）的应变分量均为零，即 $\varepsilon_{zz} = \varepsilon_{rz} = \varepsilon_{\theta z} = 0$。在这种情况下，[体积应变](@entry_id:267252)简化为 $\varepsilon_{kk} = \varepsilon_{rr} + \varepsilon_{\theta\theta}$。将此代入[胡克定律](@entry_id:149682)，我们得到平面应变下的[本构关系](@entry_id:186508) [@problem_id:2889573]：

$$
\sigma_{rr} = \lambda(\varepsilon_{rr} + \varepsilon_{\theta\theta}) + 2\mu \varepsilon_{rr}
$$

$$
\sigma_{\theta\theta} = \lambda(\varepsilon_{rr} + \varepsilon_{\theta\theta}) + 2\mu \varepsilon_{\theta\theta}
$$

$$
\sigma_{r\theta} = 2\mu \varepsilon_{r\theta}
$$

值得注意的是，为了维持 $\varepsilon_{zz}=0$ 的约束，通常需要一个非零的平面外[正应力](@entry_id:260622) $\sigma_{zz}$：
$$
\sigma_{zz} = \lambda(\varepsilon_{rr} + \varepsilon_{\theta\theta})
$$

### 求解方法：应力函数法

拥有了运动学、动力学和本构关系这三组方程后，我们就有了一个完备的[边值问题](@entry_id:193901)。然而，直接求解这个由位移和应力分量构成的[偏微分方程组](@entry_id:172573)是相当复杂的。

#### 平衡与协调的角色

在弹性力学问题的求解中，**平衡（equilibrium）**和**协调（compatibility）**是两个核心且[相互独立](@entry_id:273670)的概念 [@problem_id:2889580]。
- **平衡**要求应[力场](@entry_id:147325)必须满足力的平衡，即 $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$。
- **协调**则要求应变场必须能从一个连续、单值的位移场中导出。这意味着应变分量之间必须满足一定的[微分](@entry_id:158718)约束关系，即圣维南（Saint-Venant）协调方程。

在以位移为基本未知量的求解方法中，协调性是自动满足的，因为应变直接由位移求导得到。我们只需将应力用位移表示，再代入平衡方程，即可得到关于位移的纳维-柯西（Navier-Cauchy）方程。

而在以应力为基本未知量的求解方法中，情况则相反。我们有 3 个独立的应力分量（$\sigma_{rr}, \sigma_{\theta\theta}, \sigma_{r\theta}$），但只有 2 个平衡方程。这是一个**[静不定](@entry_id:178116)**问题 [@problem_id:2889580]。这意味着存在无穷多个满足平衡方程和给定边界条件的应[力场](@entry_id:147325)。为了从中挑选出那个唯一真实的、物理上可能的解，我们必须额外施加**协调条件**。协调条件确保了应[力场](@entry_id:147325)通过本构关系得到的应变场是“几何上可能”的，即不会在连续体内部产生不合理的间隙或重叠。在极坐标下，这个复杂的[二阶偏微分方程](@entry_id:175326)形式的协调条件为 [@problem_id:2889592]：
$$
\frac{\partial^2 \varepsilon_{rr}}{\partial \theta^2} + r \frac{\partial}{\partial r}\left(r \frac{\partial \varepsilon_{\theta\theta}}{\partial r}\right) - r \frac{\partial \varepsilon_{rr}}{\partial r} + \varepsilon_{rr} - \varepsilon_{\theta\theta} - 2 \frac{\partial}{\partial \theta}\left(r \frac{\partial \varepsilon_{r\theta}}{\partial r} + \varepsilon_{r\theta}\right) = 0
$$

#### [艾里应力函数](@entry_id:191331)

为了巧妙地同时处理平衡和协调，对于二维问题（平面应力或[平面应变](@entry_id:167046)），我们可以引入一个称为**[艾里应力函数](@entry_id:191331)（Airy stress function）**的[标量势](@entry_id:276177)函数 $\Phi(r, \theta)$。通过将应力分量定义为 $\Phi$ 的[二阶导数](@entry_id:144508)，可以自动满足平衡方程（在无体力情况下）[@problem_id:2889543]。在极坐标中，这些定义是：

$$
\sigma_{rr} = \frac{1}{r}\frac{\partial \Phi}{\partial r} + \frac{1}{r^2}\frac{\partial^2 \Phi}{\partial \theta^2}
$$

$$
\sigma_{\theta\theta} = \frac{\partial^2 \Phi}{\partial r^2}
$$

$$
\sigma_{r\theta} = -\frac{\partial}{\partial r}\left(\frac{1}{r}\frac{\partial \Phi}{\partial \theta}\right) = \frac{1}{r^2}\frac{\partial \Phi}{\partial \theta} - \frac{1}{r}\frac{\partial^2 \Phi}{\partial r \partial \theta}
$$

这样一来，平衡方程就被恒等地满足了。接下来，我们将协调条件应用于这个由 $\Phi$ 生成的应[力场](@entry_id:147325)。对于各向同性材料，协调条件可以简化为应力分量的迹的拉普拉斯为零，即 $\nabla^2(\sigma_{rr} + \sigma_{\theta\theta}) = 0$。将上述应力表达式代入，可以发现 $\sigma_{rr} + \sigma_{\theta\theta} = \nabla^2 \Phi$。于是，协调条件最终归结为一个关于 $\Phi$ 的单一[四阶偏微分方程](@entry_id:176247)——**[双调和方程](@entry_id:165706)（biharmonic equation）** [@problem_id:2889543]：

$$
\nabla^4 \Phi = \nabla^2(\nabla^2 \Phi) = 0
$$

其中 $\nabla^2 = \frac{\partial^2}{\partial r^2} + \frac{1}{r}\frac{\partial}{\partial r} + \frac{1}{r^2}\frac{\partial^2}{\partial \theta^2}$ 是极坐标下的[拉普拉斯算子](@entry_id:146319)。弹性力学平面问题的求解，至此被转化为求解带有适当边界条件的[双调和方程](@entry_id:165706)。

### [双调和方程](@entry_id:165706)的通解：[米歇尔解](@entry_id:187222)

求解[双调和方程](@entry_id:165706) $\nabla^4 \Phi = 0$ 的一个强有力的方法是分离变量法。我们假定解的形式为 $\Phi(r, \theta) = R(r) \Theta(\theta)$。由于物理场在几何上必须是单值的，$\Theta(\theta)$ 必须是周期函数，可以展开为[傅里叶级数](@entry_id:139455)，其[基函数](@entry_id:170178)为 $\cos(n\theta)$ 和 $\sin(n\theta)$（其中 $n$ 为整数）。

对于每一个傅里叶模式 $n$，代入[双调和方程](@entry_id:165706)后会得到一个关于径向函数 $R(r)$ 的[常微分方程](@entry_id:147024)。该方程的解的形式取决于 $n$ 的取值。将所有可能的解组合起来，便得到了[双调和方程](@entry_id:165706)在极坐标下的通解，即**[米歇尔解](@entry_id:187222)（Michell solution）** [@problem_id:2889579]。

#### 通解形式与特殊情形

[米歇尔解](@entry_id:187222)可以表示为一个级数，其每一项都对应一个特定的角[谐波](@entry_id:181533) $n$。对于一般的 $n \ge 2$，径向函数有四个独立的[幂律](@entry_id:143404)解。然而，在 $n=0$ 和 $n=1$ 时，常微分方程的特征根会出现重根，导致对数项的出现 [@problem_id:2889555]。完整的[米歇尔解](@entry_id:187222)形式如下 [@problem_id:2889579]：

$$
\begin{aligned}
\Phi(r,\theta) \;=\; (A_0 r^2 \ln r + B_0 r^2 + C_0 \ln r + D_0) \\
+ (a_1 r \ln r + b_1 r^3 + c_1 r^{-1} + d_1 r)\cos\theta + (e_1 r \ln r + f_1 r^3 + g_1 r^{-1} + h_1 r)\sin\theta \\
+ \sum_{n=2}^{\infty} \left[ (a_n r^n + b_n r^{-n} + c_n r^{n+2} + d_n r^{-n+2})\cos(n\theta) \right] \\
+ \sum_{n=2}^{\infty} \left[ (e_n r^n + f_n r^{-n} + g_n r^{n+2} + h_n r^{-n+2})\sin(n\theta) \right]
\end{aligned}
$$
(注意：为了简洁，这里系数的命名可能与标准教科书略有不同，但函数形式是关键。)

- **$n=0$ ([轴对称](@entry_id:173333)项)**: 包含 $r^2, \ln r, r^2 \ln r$ 和常数项。
- **$n=1$**: 包含 $r, r^3, r^{-1}$ 以及对数项 $r \ln r$。
- **$n \ge 2$**: 包含四个独立的[幂律](@entry_id:143404)项 $r^n, r^{-n}, r^{n+2}, r^{-n+2}$。

这个通解构成了求解任意二维弹性力学平面问题的“积木”，具体问题的解就是从这个[无穷级数](@entry_id:143366)中选取适当的项并由边界条件确定其系数。

#### 物理容许性与[正则性条件](@entry_id:166962)

[米歇尔解](@entry_id:187222)是一个纯数学解。要使其成为一个物理上合理的解，它必须满足**[正则性条件](@entry_id:166962)（regularity requirements）**。对于一个包含原点 $r=0$ 的区域（例如一个实心圆盘），物理场必须是良态的，这意味着 [@problem_id:2889578]：

1.  **应力有界**：当 $r \to 0$ 时，所有应力分量 $\sigma_{ij}$ 必须保持有限。材料在没有[物理奇点](@entry_id:260744)（如集中力）的点上不能承受无限大的应力。
2.  **位移单值且有限**：当 $r \to 0$ 时，位移场 $\mathbf{u}$ 必须是有限且单值的。这保证了材料的连续性和完整性。

根据应力由 $\Phi$ 的[二阶导数](@entry_id:144508)给出的关系，我们可以分析[米歇尔解](@entry_id:187222)中各项的物理容许性。一般而言，形如 $\Phi \propto r^m$ 的项产生的应力大致与 $r^{m-2}$ 成正比。为了使应力在 $r=0$ 处有界，需要 $m-2 \ge 0$，即 $m \ge 2$。

基于这个原则，我们必须从解中剔除那些会在原点导致奇性的项 [@problem_id:2889578] [@problem_id:2889555]：

-   **所有负幂次项**：如 $r^{-n}$ 和 $r^{-n+2}$ ($n \ge 2$)，它们在 $r \to 0$ 时发散，导致无限大的应力。
-   **所有对数项**：如 $\ln r$, $r^2 \ln r$, $r \ln r$ 等。这些项不仅会导致对数发散的应力，还会导致多值位移（例如，位移中出现与 $\theta$ 成正比的项），这在单连通域中是不允许的。

经过筛选，对于包含原点的区域，容许的[艾里应力函数](@entry_id:191331)项为：
- 常数项和 $r^2$ 项。
- $r^n$ 和 $r^{n+2}$ 项，其中 $n \ge 2$。
- 一个特殊情况是 $n=1$ 时的 $r\cos\theta$ 和 $r\sin\theta$ 项。虽然它们的径向次幂 $m=1$ 小于2，但它们对应于物体的刚体平移，产生的应力恒为零，因此是物理上容许的。

综上所述，对于一个实心圆盘类的问题，其[艾里应力函数](@entry_id:191331)解必须仅由这些在原点处表现良好的“正则”项构成。而被剔除的那些“奇异”项并非无用，它们恰恰是解决外部问题（如带孔板、含裂纹体）的关键，因为在这些问题中，原点位于材料的空洞或外部，[应力奇异性](@entry_id:166362)是允许甚至必要的，用以描述[应力集中](@entry_id:160987)等重要物理现象。