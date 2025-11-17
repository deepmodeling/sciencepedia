## 引言
在理论物理的宏伟画卷中，[流体动力学](@entry_id:136788)以其普适性和复杂性占据着核心地位。从微观的细胞质流动到宏观的[星系演化](@entry_id:158840)，流体的行为由一组[偏微分方程](@entry_id:141332)所支配。然而，在传统的矢量微积分表述下，这些方程（如[质量守恒](@entry_id:204015)、纳维-斯托克斯方程）形式各异，其内在的统一性和深刻的几何结构往往被复杂的坐标运算所掩盖。本文旨在解决这一问题，引入微分形式——现代微分几何的语言——作为一种强大的分析工具，以一种前所未有的优雅和深刻的方式重塑我们[对流](@entry_id:141806)体行为的理解。

本文将带领读者踏上一段从基本原理到前沿应用的旅程。在“原理与机制”一章中，我们将学习如何将速度、[涡量](@entry_id:142747)、应力等物理量翻译成微分形式，并利用外微分、[霍奇星算子](@entry_id:197539)等工具，将宏观的积分[守恒定律](@entry_id:269268)转化为点态的、坐标无关的[微分方程](@entry_id:264184)，从而揭示[流体运动](@entry_id:182721)的内在几何本质。随后的“应用与跨学科联系”一章将展示这一形式体系的强大威力，通过一系列从经典水动力学到地球物理、等离子体物理乃至宇宙学的实例，证明微分形式不仅是优美的记法，更是连接不同物理学分支的共同语言。最后，“动手实践”部分将通过具体的计算问题，帮助读者巩固所学，将抽象的理论转化为解决实际问题的能力。

## 原理与机制

本章旨在系统阐述流体行为方程的[微分形式](@entry_id:146747)表述。我们将采用[外代数](@entry_id:201164)和[微分几何](@entry_id:145818)的语言，这套强大的数学工具能够以极为优雅和深刻的方式统一[流体动力学](@entry_id:136788)的基本方程。通过将速度、涡量、应力等物理量表示为微分形式，我们可以利用外微分、[内积](@entry_id:158127)和[霍奇星算子](@entry_id:197539)等工具，将积分[守恒定律](@entry_id:269268)转化为点态的[偏微分方程](@entry_id:141332)，并以一种坐标无关的方式揭示[流体运动](@entry_id:182721)的内在几何结构。

### 从积分守恒到局域[微分方程](@entry_id:264184)

物理学的基本定律通常首先以积分形式出现，描述有限区域内某个物理量的总变化。[微分形式](@entry_id:146747)和[广义斯托克斯定理](@entry_id:159620)为我们提供了一座桥梁，将这些宏观的[守恒定律](@entry_id:269268)转化为描述流场每一点行为的局域[微分方程](@entry_id:264184)。

我们以一个标量场（如浓度或温度）$c$ 的[输运过程](@entry_id:177992)为例来说明这一核心思想 [@problem_id:485024]。考虑一个 $n$ 维[欧几里得空间](@entry_id:138052)中的标量浓度场，表示为一个0-形式 $c(x, t)$。在任意一个固定的 $n$ 维区域 $\Omega$ 内，其总量的守恒可以表示为：
$$
\frac{d}{dt} \int_{\Omega} c (\star 1) = - \oint_{\partial\Omega} j + \int_{\Omega} S (\star 1)
$$
这里，$\star 1$ 是 $n$ 维[体积形式](@entry_id:203000)，因此 $\int_{\Omega} c (\star 1)$ 代表了区域 $\Omega$ 内浓度的总量。方程的左边是该总量的变化率。右边第一项 $\oint_{\partial\Omega} j$ 代表通过边界 $\partial\Omega$ 的通量，其中 $j$ 是一个 $(n-1)$-形式的[扩散通量](@entry_id:748422)流。第二项 $\int_{\Omega} S (\star 1)$ 代表区域内源或汇的贡献，其中 $S$ 是一个0-形式的源率。

物理上，[扩散通量](@entry_id:748422)由菲克定律描述，即通量与[浓度梯度](@entry_id:136633)成正比。在[微分形式](@entry_id:146747)的语言中，这被优雅地表达为：
$$
j = -\kappa \star dc
$$
这里，$\kappa$ 是一个正常数，称为[扩散](@entry_id:141445)系数。$d$ 是外微分算子，当它作用于一个0-形式（标量函数）$c$ 时，$dc$ 是一个1-形式，代表了 $c$ 的梯度。[霍奇星算子](@entry_id:197539) $\star$ 将这个[1-形式](@entry_id:270392)映射到一个 $(n-1)$-形式，正好对应于通量流的维度。

为了从积分定律得到[微分](@entry_id:158718)定律，我们使用**[广义斯托克斯定理](@entry_id:159620)**，它指出 $\int_{\Omega} d\omega = \oint_{\partial\Omega} \omega$ 对于任何 $(n-1)$-形式 $\omega$ 都成立。将此应用于通量项：
$$
-\oint_{\partial\Omega} j = -\oint_{\partial\Omega} (-\kappa \star dc) = \kappa \oint_{\partial\Omega} \star dc = \kappa \int_{\Omega} d(\star dc)
$$
此时，[守恒定律](@entry_id:269268)变为一个在同一区域 $\Omega$ 上的积分等式：
$$
\int_{\Omega} \frac{\partial c}{\partial t} (\star 1) = \int_{\Omega} \kappa d(\star dc) + \int_{\Omega} S (\star 1)
$$
在这里，我们定义了[标量场](@entry_id:151443)上的**[拉普拉斯算子](@entry_id:146319)** $\nabla^2$。对于任意0-形式 $f$，其拉普拉斯 $\nabla^2 f$ 由关系式 $d(\star df) = (\nabla^2 f) (\star 1)$ 定义。因此，我们可以写出 $d(\star dc) = (\nabla^2 c) (\star 1)$。

将所有项合并到一个积分下：
$$
\int_{\Omega} \left( \frac{\partial c}{\partial t} - \kappa \nabla^2 c - S \right) (\star 1) = 0
$$
由于这个等式对于任意区域 $\Omega$ 都必须成立，被积函数本身必须处处为零。这就给出了我们所熟悉的**[扩散](@entry_id:141445)-反应方程**的偏微分形式：
$$
\frac{\partial c}{\partial t} = \kappa \nabla^2 c + S
$$
这个过程清晰地展示了如何利用微分形式的运算，将一个基于边界通量的宏观[守恒定律](@entry_id:269268)，系统地转化为一个描述场在每一点如何演化的局域方程。

### [流动运动](@entry_id:184094)学：速度、涡量与加速度

在用微分几何描述[流体运动](@entry_id:182721)时，关键的运动学量被赋予了新的身份。流体的速度场是一个矢量场 $U$，通过度规张量 $g$ 的作用（“[降指标](@entry_id:272166)”运算 $U^\flat$），我们可以得到与之对应的**速度1-形式** $u$。这个[1-形式](@entry_id:270392)的作用是测量其他矢量场在流速方向上的投影。

流场的另一个核心特征是涡量。**涡量2-形式** $\Omega$ 被自然地定义为速度[1-形式](@entry_id:270392)的外微分：
$$
\Omega = du
$$
这个定义的美妙之处在于，对于一个无[旋流](@entry_id:153202)（[势流](@entry_id:159985)），其速度1-形式 $u$ 是某个[势函数](@entry_id:176105)（0-形式）$\phi$ 的梯度，即 $u=d\phi$。根据外微分的一个基本性质 $d^2=0$，我们立即得到无[旋流](@entry_id:153202)的[涡量](@entry_id:142747)为零：$\Omega = d(d\phi) = 0$。

流体质点的加速度是理解动力学的基础。一个流体[质点](@entry_id:186768)的加速度矢量场 $A$ 由[速度矢量](@entry_id:269648)场 $U$ 的物质导数给出，即 $A = \frac{DU}{Dt} = \frac{\partial U}{\partial t} + \nabla_U U$，其中 $\nabla_U U$ 是 $U$ 沿自身的协变导数。

为了在[微分形式](@entry_id:146747)的框架下进行分析，我们关注**加速度[1-形式](@entry_id:270392)** $\alpha = A^\flat$。一个至关重要的[运动学](@entry_id:173318)恒等式将加速度与速度、涡量和动能联系起来 [@problem_id:485113]。单位质量的动能是一个0-形式（标量函数）$K = \frac{1}{2}g(U, U)$。通过一系列基于卡当恒等式 $\mathcal{L}_U u = i_U du + d(i_U u)$ 的推导，可以证明加速度1-形式可以表示为：
$$
\alpha = \frac{\partial u}{\partial t} + i_U \Omega + dK
$$
这个表达式极具启发性。它将加速度分解为三个部分：
1.  $\frac{\partial u}{\partial t}$：速度场的局域（欧拉）变化率。
2.  $i_U \Omega$：[对流](@entry_id:141806)项的一部分，由速度场与涡量场的相互作用产生。它描述了质点因在具有涡量的流场中运动而感受到的加速度。
3.  $dK$：由动能的空间变化（梯度）引起的加速度。[质点](@entry_id:186768)从高动能区域流向低动能区域时会减速，反之则加速。

这个运动学关系是推导欧拉方程和[纳维-斯托克斯方程](@entry_id:142275)[微分形式](@entry_id:146747)版本的基石。

### 流动动力学：运动方程的建立

流体的动力学由动量守恒定律（柯西第一运动定律）支配。利用微分形式，我们可以将这个定律从其积分形式转化为一个优雅的[微分方程](@entry_id:264184)。

#### [动量守恒](@entry_id:149964)与应力2-形式

柯西定律指出，一个物质体积 $V(t)$ 内的总动量变化率，等于作用在该体积边界上的面力和作用在体积内部的[体力](@entry_id:174230)的总和。在积分形式下，这可以写为：
$$
\frac{D}{Dt} \int_{V(t)} \rho \mathbf{u} \, dV = \oint_{\partial V(t)} \boldsymbol{\sigma} + \int_{V(t)} \rho \mathbf{f} \, dV
$$
这里，$\rho$ 是密度，$\mathbf{u}$ 是[速度矢量](@entry_id:269648)，$\mathbf{f}$ 是单位质量的体力。关键的新概念是**应力[2-形式](@entry_id:188008)** $\boldsymbol{\sigma}$ [@problem_id:485010]。这是一个矢量值的[2-形式](@entry_id:188008)，当它在一个[曲面](@entry_id:267450) $\mathcal{S}$ 上积分时，结果是作用在该[曲面](@entry_id:267450)上的总力矢量 $\mathbf{F}_{\mathcal{S}}$。例如，其 $x$ 分量 $\sigma_x$ 定义为：
$$
\sigma_x = \sigma_{xx} dy \wedge dz + \sigma_{xy} dz \wedge dx + \sigma_{xz} dx \wedge dy
$$
其中 $\sigma_{ij}$ 是柯西应力张量的分量。

为了得到微分形式的方程，我们再次应用[雷诺输运定理](@entry_id:191217)和[广义斯托克斯定理](@entry_id:159620)。[雷诺输运定理](@entry_id:191217)允许我们将物质导数移到积分号内，而[斯托克斯定理](@entry_id:264534)将边界上的[面积分](@entry_id:275394)转换成[体积分](@entry_id:171119)：
$$
\oint_{\partial V} \boldsymbol{\sigma} = \int_V d\boldsymbol{\sigma}
$$
$d\boldsymbol{\sigma}$ 是应力2-形式的外微分，它代表了应力[张量的散度](@entry_id:191736)。例如，对 $\sigma_x$ 进行[外微分](@entry_id:161900)计算可得：
$$
d\sigma_x = \left( \frac{\partial\sigma_{xx}}{\partial x} + \frac{\partial\sigma_{yx}}{\partial y} + \frac{\partial\sigma_{zx}}{\partial z} \right) dx \wedge dy \wedge dz
$$
（假设[应力张量](@entry_id:148973)是对称的，即 $\sigma_{xy}=\sigma_{yx}$ 等）。将这些代入[动量守恒](@entry_id:149964)积分方程，并利用积分区域的任意性，我们得到点态的**[柯西动量方程](@entry_id:187010)**：
$$
\rho \frac{D\mathbf{u}}{Dt} = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{f}
$$
在分量形式下，例如 $x$ 方向的动量方程为：
$$
\rho \frac{Du_x}{Dt} = \frac{\partial\sigma_{xx}}{\partial x} + \frac{\partial\sigma_{xy}}{\partial y} + \frac{\partial\sigma_{xz}}{\partial z} + \rho f_x
$$
这正是我们通过微分形式的系统推导得到的结果。

#### 欧拉与纳维-斯托克斯方程

对于无粘的**理想流体**，应力是各向同性的，仅由压力 $p$ 贡献：$\sigma_{ij} = -p\delta_{ij}$。此时，应力[张量的散度](@entry_id:191736)变为压力的负梯度 $-\nabla p$。将此与前述的加速度[1-形式](@entry_id:270392)表达式结合，我们便得到了**欧拉方程**的[1-形式](@entry_id:270392)版本。假设体力是保守的，即来自一个势 $\Phi$（$\mathbf{f}=-\nabla\Phi$），则加速度1-形式 $\alpha$ 为：
$$
\alpha = -\frac{1}{\rho}dp - d\Phi
$$
结合[运动学](@entry_id:173318)恒等式 $\alpha = \frac{\partial u}{\partial t} + i_U \Omega + dK$，我们得到：
$$
\frac{\partial u}{\partial t} + i_U du + d\left(\frac{1}{2}|U|^2 + \frac{p}{\rho} + \Phi\right) = 0
$$
这里我们用了 $\Omega = du$ 和 $K = \frac{1}{2}|U|^2$。这个方程优雅地包含了流体运动的所有动力学信息。

对于**[粘性流](@entry_id:136330)体**，我们需要包含由[粘性耗散](@entry_id:143708)引起的应力。对于不可压缩的牛顿流体，可以证明粘性力项对应的1-形式可以简洁地表示为 $-\nu \delta \omega$ [@problem_id:485105]，其中 $\nu$ 是运动粘度，$\omega$ 是涡量2-形式，$\delta$ 是**[余微分算子](@entry_id:191334)**（codifferential）。因此，**不[可压缩纳维-斯托克斯](@entry_id:747591)方程**的[1-形式](@entry_id:270392)为：
$$
\frac{\partial u}{\partial t} + i_U \omega + d\left(\frac{p}{\rho} + \frac{1}{2}|U|^2\right) = -\nu \delta \omega
$$
这个方程是现代[流体动力学](@entry_id:136788)几何表述的核心。

### [流体运动](@entry_id:182721)的基本定理

微分形式的框架不仅能优雅地表述运动方程，还能极其清晰地推导出[流体力学](@entry_id:136788)中的一些基本定理。

#### [涡量](@entry_id:142747)动力学

[涡量](@entry_id:142747)的演化是[流体动力学](@entry_id:136788)研究的中心问题之一。我们可以通过对[纳维-斯托克斯方程](@entry_id:142275)（[1-形式](@entry_id:270392)）两边取外微分 $d$ 来推导**[涡量输运方程](@entry_id:139098)** [@problem_id:485105]。
$$
d\left(\frac{\partial u}{\partial t}\right) + d(i_U \omega) + d^2\left(\frac{p}{\rho} + \frac{1}{2}|U|^2\right) = d(-\nu \delta \omega)
$$
利用 $d$ 与时间偏导可交换、$\omega=du$ 以及 $d^2=0$ 的性质，方程简化为：
$$
\frac{\partial \omega}{\partial t} + d(i_U \omega) = -\nu d\delta \omega
$$
根据[外微分](@entry_id:161900)的基本性质 $d^2=0$，由速度[1-形式](@entry_id:270392)定义的[涡量](@entry_id:142747)2-形式 $\omega = du$ 必然满足 $d\omega = d(du) = 0$。这个性质（被称为“闭合性”）对任何涡量场都成立，与流体是否可压缩无关。利用卡当恒等式 $\mathcal{L}_U \omega = i_U d\omega + d(i_U \omega)$，我们发现 $d(i_U \omega)$ 正好是在 $d\omega=0$ 条件下的**[李导数](@entry_id:171745)** $\mathcal{L}_U \omega$ [@problem_id:485080]。[李导数](@entry_id:171745)描述了2-形式 $\omega$ 如何被[速度场](@entry_id:271461) $U$ "拖曳" 和 "拉伸"。

同时，我们引入**[霍奇-拉普拉斯算子](@entry_id:261049)** $\Delta = d\delta + \delta d$。当作用于一个满足 $d\omega=0$ 的[2-形式](@entry_id:188008) $\omega$ 时，由于 $\delta d \omega = \delta(d^2 u) = 0$，[拉普拉斯算子](@entry_id:146319)简化为 $\Delta\omega = d\delta\omega$。因此，[涡量输运方程](@entry_id:139098)最终可以写成：
$$
\frac{\partial \omega}{\partial t} + \mathcal{L}_U \omega = -\nu \Delta \omega
$$
这个方程优美地描述了[涡量](@entry_id:142747)的演化：涡量的物质导数（左边两项，即随流输运和拉伸）等于粘性[扩散](@entry_id:141445)项（右边）。在理想流体中（$\nu=0$），我们得到 $\frac{D\omega}{Dt} = 0$（在李导数的意义上），这正是亥姆霍兹[涡量](@entry_id:142747)守恒定理的体现。

#### [环量守恒](@entry_id:189127)（开尔文定理）

开尔文定理指出，在理想、正压、且[体力](@entry_id:174230)保守的流体中，沿任一闭合物质回路的环量是守恒的。环量 $\Gamma$ 定义为[速度场](@entry_id:271461)沿闭合回路 $C(t)$ 的线积分，用1-形式表示即 $\Gamma(t) = \oint_{C(t)} u$。

环量的时间变化率由一个[输运定理](@entry_id:176504)给出：$\frac{d\Gamma}{dt} = \oint_{C(t)} \alpha$，其中 $\alpha$ 是加速度1-形式 [@problem_id:485068]。对于一个正压（$p=p(\rho)$）的理想流体，存在一个比焓函数 $h$ 使得 $dh = dp/\rho$。若体力也是保守的（$\mathbf{F}=-\nabla\Phi$），那么欧拉方程给出的加速度1-形式为：
$$
\alpha = -\frac{1}{\rho}dp - d\Phi = -d(h+\Phi)
$$
这表明加速度1-形式是一个**恰当形式**（exact form）。根据[斯托克斯定理](@entry_id:264534)，一个恰当形式沿任何闭合回路的积分恒为零。因此：
$$
\frac{d\Gamma}{dt} = \oint_{C(t)} (-d(h+\Phi)) = 0
$$
这便是开尔文定理的优雅证明。环量之所以守恒，根本原因在于驱动流体加速的力（[压力梯度](@entry_id:274112)和体力）都是保守的（即梯度场）。

#### 伯努利定理

伯努利定理描述了流线上能量的守恒。对于定常、理想、正压流，我们可以定义**伯努利函数**（0-形式）$B = \frac{1}{2}|U|^2 + h + \Phi$。定常欧拉方程可以写作一个简洁的几何关系 [@problem_id:485025]：
$$
i_U \Omega + dB = 0
$$
将此方程与速度矢量场 $U$ 做[内积](@entry_id:158127)，得到 $i_U(i_U \Omega) + i_U(dB) = 0$。由于[内积](@entry_id:158127)的反对称性，$i_U(i_U \Omega)=0$。而 $i_U(dB)$ 正是伯努利函数沿流线方向的[方向导数](@entry_id:189133) $U \cdot \nabla B$。因此我们立即得到 $U \cdot \nabla B = 0$，这说明伯努利函数 $B$ 沿流线保持不变。

这个几何关系揭示了更深刻的结构。它表明 $dB = -i_U \Omega$。这意味着 $B$ 的梯度垂直于由速度 $U$ 和涡量 $\Omega$ 张成的平面。更进一步，对于任何属于[涡量](@entry_id:142747)2-形式的核（kernel）的矢量场 $X$（即满足 $i_X \Omega = 0$ 的矢量场），我们有：
$$
\mathcal{L}_X B = i_X dB = i_X(-i_U \Omega) = i_U (i_X \Omega) = i_U(0) = 0
$$
这表明伯努利函数不仅沿流线守恒，而且在由速度矢量和[涡量矢量](@entry_id:187667)共同生成的二维[曲面](@entry_id:267450)上也是常数。

#### [压力泊松方程](@entry_id:137996)

对于不可压缩流，压[力场](@entry_id:147325)并非一个独立的动力学变量，而是起到了一个拉格朗日乘子的作用，以维持流场的无散（即不可压缩）约束 $\delta u=0$。我们可以通过对[运动方程](@entry_id:170720)应用[余微分算子](@entry_id:191334) $\delta$ 来导出一个确定压力的辅助方程 [@problem_id:485051]。

对不[可压缩欧拉方程](@entry_id:747588)（1-形式）作用 $\delta$ 算子：
$$
\delta\left(\frac{\partial u}{\partial t}\right) + \delta(i_U du) + \delta d\left(\frac{1}{2}|U|^2 + \frac{p}{\rho}\right) = 0
$$
由于 $\delta u=0$，第一项为零。利用 $\Delta f = \delta d f$ 的定义，最后一项包含 $\frac{1}{\rho}\Delta p$。整理后我们得到**[压力泊松方程](@entry_id:137996)**:
$$
\Delta p = -\rho \left[ \delta(i_U du) + \frac{1}{2}\Delta(|U|^2) \right]
$$
这个方程表明，在任意时刻，压[力场](@entry_id:147325)的[分布](@entry_id:182848)是由[速度场](@entry_id:271461)的空间结构（通过 $\delta(i_U du)$ 和 $\Delta(|U|^2)$ 项体现）唯一确定的，以保证流场在下一时刻依然满足不可压缩条件。这个过程可以看作是将运动方程通过霍奇-[德拉姆分解](@entry_id:184695)，提取出其中的恰当形式部分。

### 应用：边界、输运与冻结场

[微分形式](@entry_id:146747)的语言在处理流固边界、物质输运和更广泛的场论问题（如[磁流体动力学](@entry_id:264274)）时也显示出其威力。

#### [运动学](@entry_id:173318)边界条件

描述流体与一个运动或变形的不可穿透表面的相互作用，需要一个[运动学](@entry_id:173318)边界条件。假设这个表面由一个水平集函数 $S(x,y,z,t)=0$ 定义。流体质点一旦处于该表面，就会始终停留在表面上。这意味着质点随流的 $S$ 值的[物质导数](@entry_id:172646)为零：
$$
\frac{DS}{Dt} = \frac{\partial S}{\partial t} + \mathbf{U} \cdot \nabla S = 0
$$
在[微分形式](@entry_id:146747)的语言中，$\mathbf{U} \cdot \nabla S$ 正是1-形式 $dS$ 作用在矢量场 $U$ 上的结果，也就是[内积](@entry_id:158127) $i_U(dS)$ [@problem_id:485027]。因此，这个边界条件可以优雅地写为：
$$
i_U(dS) = -\frac{\partial S}{\partial t}
$$
例如，考虑一个以角速度 $\beta$ 绕z轴旋转的平面 $x\cos(\beta t) + y\sin(\beta t) = x_0$。若它浸没在一个刚体[旋转流](@entry_id:276737)场 $U = -\Omega_0 y \partial_x + \Omega_0 x \partial_y$ 中并作为物质面，通过计算 $i_U(dS)$ 和 $-\partial_t S$ 并令两者相等，可以立即得出 $\beta=\Omega_0$，即该物质面必须以与流体相同的[角速度](@entry_id:192539)旋转。

#### 物质[线元](@entry_id:196833)的演化与冻结场

[李导数](@entry_id:171745)的概念是描述几何对象如何随流“冻结”和变形的核心。例如，一个物质线元（代表两个相邻流体[质点](@entry_id:186768)之间的[位移矢量](@entry_id:262782)）可以由一个[1-形式](@entry_id:270392) $\delta\boldsymbol{l}$ 表示。它的演化由[李导数](@entry_id:171745)决定 [@problem_id:485081]。可以证明，其分量的[物质导数](@entry_id:172646)为：
$$
\frac{D(\delta l_i)}{Dt} = (\Omega_{ij} - S_{ij}) \delta l_j
$$
其中 $S_{ij}$ 和 $\Omega_{ij}$ 分别是速率-[应变张量](@entry_id:193332)（对称部分）和[涡量张量](@entry_id:189621)（反对称部分）的分量。这个方程清晰地表明，物质[线元](@entry_id:196833)既被应变场拉伸或压缩，也被涡量场旋转。

“场线冻结”的概念在等离子体物理中尤为重要。[阿尔文定理](@entry_id:191257)指出，在理想磁流体（MHD）中，[磁感线](@entry_id:268292)就像被“冻结”在导电流体中一样随之运动。这意味着穿过任一物质[曲面](@entry_id:267450)的磁通量是守恒的。然而，在具有有限电阻率的真实等离子体中，这种冻结被打破。

穿过一个随流运动的[曲面](@entry_id:267450) $S$ 的磁通量 $\Phi_B = \int_S \mathbf{B} \cdot d\mathbf{A}$ 的变化率由一个[输运定理](@entry_id:176504)给出。结合电阻性[磁感应方程](@entry_id:751626)，可以得到 [@problem_id:485118]：
$$
\frac{d\Phi_B}{dt} = \int_S \eta_m \nabla^2 \mathbf{B} \cdot d\mathbf{A}
$$
其中 $\eta_m$ 是[磁扩散](@entry_id:187718)系数。这个结果表明，[磁通量](@entry_id:268943)的变化率正比于[磁扩散](@entry_id:187718)系数，并且依赖于[磁场](@entry_id:153296)的曲率（由拉普拉斯算子 $\nabla^2\mathbf{B}$ 体现）。只有在理想导体中（$\eta_m=0$），[磁通量](@entry_id:268943)才会守恒，[磁场](@entry_id:153296)线才被完美冻结。例如，对于一个具有抛物线型轴向[磁场](@entry_id:153296) $B_z(r) = B_0 (1 - r^2/R^2)$ 的旋转[等离子体柱](@entry_id:194522)，我们可以计算出由于电阻效应，穿过其[横截面](@entry_id:154995)的总磁通量以恒定的速率 $\frac{d\Phi_B}{dt} = -4\pi\eta_m B_0$ 减少，这代表了[磁场](@entry_id:153296)的[扩散](@entry_id:141445)和耗散。