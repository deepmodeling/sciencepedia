## 引言
在探索[原子核](@entry_id:167902)这一复杂[量子多体系统](@entry_id:141221)的奥秘时，静态模型为我们理解其结构提供了坚实基础。然而，[原子核](@entry_id:167902)并非静止不变，其内部的集体激发、以及[原子核](@entry_id:167902)之间的剧烈碰撞，都涉及到复杂的[实时演化](@entry_id:199067)过程。如何从第一性原理出发，在微观层面描述这些丰富的动力学现象，是[计算核物理](@entry_id:747629)面临的核心挑战。含时Hartree-Fock（TDHF）理论正是为解决这一问题而生的强大理论框架，它将静态平均场的概念推广到动力学领域，为我们提供了一扇观察[原子核](@entry_id:167902)[实时演化](@entry_id:199067)的窗口。

本文旨在全面而深入地介绍TDH[F理论](@entry_id:184208)及其应用。我们将首先在“原理与机制”一章中，从Dirac-Frenkel[变分原理](@entry_id:198028)出发，建立TDHF的数学形式，探讨其核心概念如[单体密度矩阵](@entry_id:161726)和自洽平均场，并阐明其与静态HF及随机相近似（RPA）的深刻联系。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示TDHF如何被用来模拟[原子核](@entry_id:167902)的[巨共振](@entry_id:159268)、[重离子碰撞](@entry_id:160663)等关键物理过程，并探讨其思想如何延伸至凝聚态物理和[量子化学](@entry_id:140193)等领域。最后，“动手实践”部分将提供一系列计算练习，引导读者从理论走向实践，亲手构建TDHF模拟的核心模块。通过这三章的学习，读者将对TDH[F理论](@entry_id:184208)的微观基础、计算实现和物理应用建立起一个完整而系统的认识。

## 原理与机制

继引言之后，本章将深入探讨含时[Hartree-Fock](@entry_id:142303)（Time-Dependent Hartree-Fock, TDHF）理论的核心原理与动力学机制。我们将从其变分基础出发，建立起描述多体系统平均场动力学的数学框架，并探讨其基本性质、守恒律，及其与静态平均场理论和[集体激发](@entry_id:145026)模式的联系。

### TDHF的变分基础

TDH[F理论](@entry_id:184208)的根基是Dirac-Frenkel含时变分原理。该原理为在受限的试探波函数[流形](@entry_id:153038)内近似求解[含时薛定谔方程](@entry_id:137898)提供了一个严谨的途径。对于一个由[哈密顿量](@entry_id:172864) $\hat{H}$ 描述的量子系统，其真实的时间演化由[含时薛定谔方程](@entry_id:137898) $i\hbar \partial_t |\Psi(t)\rangle = \hat{H} |\Psi(t)\rangle$ 决定。然而，精确求解此方程对于多体系统而言通常是不可行的。

TDH[F理论](@entry_id:184208)的核心思想是将[多体波函数](@entry_id:203043) $|\Psi(t)\rangle$ 的[演化限制](@entry_id:152522)在一个特定的、相对简单的[试探波函数](@entry_id:142892)[流形](@entry_id:153038) $\mathcal{M}$ 之内。具体而言，该[流形](@entry_id:153038)由所有归一化的、由 $A$ 个单粒子[轨道](@entry_id:137151)构成的Slater行列式组成。当我们将一个Slater行列式试探态 $|\Phi(t)\rangle$ 代入薛定谔方程时，方程通常不会被精确满足。其残差 $(i\hbar \partial_t - \hat{H})|\Phi(t)\rangle$ 不为零，并且通常指向[流形](@entry_id:153038)之外。

Dirac-Frenkel[变分原理](@entry_id:198028)指出，最优的动力学路径是使得薛定谔方程的残差在每时每刻都与[流形](@entry_id:153038)在该点的[切空间](@entry_id:199137)正交。换言之，对于切空间内的任意允许的无穷小变分 $|\delta\Phi\rangle$，都必须满足以下条件：

$$
\langle \delta\Phi | i\hbar \frac{\partial}{\partial t} - \hat{H} | \Phi(t) \rangle = 0
$$

这个条件在几何上意味着，我们将真实的薛定谔演化投影到Slater行列式[流形](@entry_id:153038)的切空间上，从而得到在[流形](@entry_id:153038)内部的“最佳”演化路径。对于Slater行列式[流形](@entry_id:153038)，其在点 $|\Phi\rangle$ 处的切空间由所有的单粒子-单空穴 (1p-1h) [激发态](@entry_id:261453) $|\Phi_{hp}\rangle = \hat{a}_p^\dagger \hat{a}_h |\Phi\rangle$ 张成，其中 $\hat{a}_h$ 湮灭一个已占据[轨道](@entry_id:137151)（产生一个空穴），而 $\hat{a}_p^\dagger$ 在一个未占据[轨道](@entry_id:137151)上产生一个粒子。因此，动力学的本质是通过[粒子-空穴激发](@entry_id:137289)来驱动[Slater行列式](@entry_id:139034)在[流形](@entry_id:153038)上的演化。将这一原理应用于[Slater行列式](@entry_id:139034)[流形](@entry_id:153038)，并引入拉格朗日乘子以保证单粒子[轨道](@entry_id:137151)的正交归一性，便可以导出TDHF方程 [@problem_id:3609670]。

### 态矢量与[单体密度矩阵](@entry_id:161726)

在TDHF框架中，多体系统的状态由一个随时间演化的[Slater行列式](@entry_id:139034) $|\Phi(t)\rangle$ 来近似。作为[费米子](@entry_id:146235)系统的[波函数](@entry_id:147440)，它天然地满足反对称性要求：交换任意两个粒子的坐标（在[行列式](@entry_id:142978)中对应于交换两列）会使[波函数](@entry_id:147440)反号。这一性质是[泡利不相容原理](@entry_id:141850)的直接体现，即两个[费米子](@entry_id:146235)不能占据完全相同的[量子态](@entry_id:146142)。如果试图用两个相同的单粒子[轨道](@entry_id:137151)构建Slater行列式，[行列式](@entry_id:142978)的值将为零 [@problem_id:3609658]。

虽然[Slater行列式](@entry_id:139034)是理论的基础，但TDHF的动力学通常用一个更简洁的对象来描述：**[单体](@entry_id:136559)[密度算符](@entry_id:138151)**（或其矩阵表示，即[单体密度矩阵](@entry_id:161726)），定义为：

$$
\hat{\rho}(t) = \sum_{i=1}^{A} |\phi_i(t)\rangle \langle\phi_i(t)|
$$

其中 $\{|\phi_i(t)\rangle\}_{i=1}^{A}$ 是构成Slater行列式的 $A$ 个正交归一的已占据单粒子[轨道](@entry_id:137151)。从这个定义可以看出，$\hat{\rho}(t)$ 是一个[投影算符](@entry_id:154142)，它将整个单粒子[希尔伯特空间](@entry_id:261193)投影到由已占据[轨道](@entry_id:137151)张成的[子空间](@entry_id:150286)上。

作为[投影算符](@entry_id:154142)，$\hat{\rho}(t)$ 具有两个关键的数学性质：

1.  **[幂等性](@entry_id:190768) (Idempotency)**：[投影算符](@entry_id:154142)的平方等于其自身。利用[轨道](@entry_id:137151)的正交归一性 $\langle\phi_i(t)|\phi_j(t)\rangle = \delta_{ij}$，我们可以直接证明：
    $$
    \hat{\rho}^2(t) = \left( \sum_{i=1}^{A} |\phi_i(t)\rangle \langle\phi_i(t)| \right) \left( \sum_{j=1}^{A} |\phi_j(t)\rangle \langle\phi_j(t)| \right) = \sum_{i,j=1}^{A} |\phi_i(t)\rangle \langle\phi_i(t)|\phi_j(t)\rangle \langle\phi_j(t)| = \sum_{i=1}^{A} |\phi_i(t)\rangle \langle\phi_i(t)| = \hat{\rho}(t)
    $$
    这一性质是状态为单一[Slater行列式](@entry_id:139034)的标志。对于包含超越平均场关联的更复杂状态（例如，多个[Slater行列式](@entry_id:139034)的叠加），其[单体密度矩阵](@entry_id:161726)通常不满足[幂等性](@entry_id:190768) [@problem_id:3609644]。

2.  **迹 (Trace)**：[密度算符](@entry_id:138151)的迹等于粒子数 $A$。
    $$
    \mathrm{Tr}\,\hat{\rho}(t) = \sum_{i=1}^{A} \mathrm{Tr}(|\phi_i(t)\rangle \langle\phi_i(t)|) = \sum_{i=1}^{A} \langle\phi_i(t)|\phi_i(t)\rangle = \sum_{i=1}^{A} 1 = A
    $$
    这反映了粒子数守恒的基本事实 [@problem_id:3609658]。

[单体密度矩阵](@entry_id:161726)是TDH[F理论](@entry_id:184208)的核心变量，其重要性在于它包含了计算所有[单体](@entry_id:136559)可观测量[期望值](@entry_id:153208)所需的全部信息。更深刻的是，对于Slater行列式而言，[单体密度矩阵](@entry_id:161726) $\hat{\rho}$ 能够唯一确定多体态 $|\Phi\rangle$，误差仅为一个总体相位因子。任何两个具有相同[单体密度矩阵](@entry_id:161726)的Slater行列式，其占据的单粒[子空间](@entry_id:150286)是相同的，它们之间的差别仅在于所选取的占据态[基矢](@entry_id:199546)不同，而这等价于一个作用在占据态空间内部的幺正变换，最终导致整个Slater行列式仅相差一个相位因子 $e^{i\theta}$ [@problem_id:3609658]。这使得我们可以完全用 $\hat{\rho}(t)$ 的演化来描述系统的动力学，而无需关心单个[轨道](@entry_id:137151)的具体形式。

### 运动方程

通过Dirac-Frenkel[变分原理](@entry_id:198028)或直接对[密度算符](@entry_id:138151)的定义式求导，可以得到[单体密度矩阵](@entry_id:161726)的[运动方程](@entry_id:170720)，这被称为TDHF方程：

$$
i\hbar \frac{d\hat{\rho}(t)}{dt} = [\hat{h}[\rho(t)], \hat{\rho}(t)]
$$

这个方程形式上是一个刘维-冯诺依曼方程。其中，$\hat{h}[\rho(t)]$ 是单粒子[Hartree-Fock哈密顿量](@entry_id:196141)，它本身是[密度矩阵](@entry_id:139892) $\rho(t)$ 的一个泛函。$\hat{h}[\rho]$ 通常包括动能项和自洽的[平均场势](@entry_id:158256)，后者通过系统的[能量密度泛函](@entry_id:161351)（如[Skyrme泛函](@entry_id:754940)）或有效相互作用对密度求泛函导数得到。这种依赖性——[哈密顿量](@entry_id:172864)决定了密度的演化，而密度又反过来决定了[哈密顿量](@entry_id:172864)——体现了理论的**自洽性**，是平均场理论的共同特征 [@problem_id:3609644]。

尽管TDHF方程通常以密度矩阵的形式给出，但实际计算中往往需要演化单粒子[轨道](@entry_id:137151)。单个[轨道](@entry_id:137151)的[演化方程](@entry_id:268137)可以写为：

$$
i\hbar \frac{d}{dt}|\phi_i(t)\rangle = \hat{h}[\rho(t)] |\phi_i(t)\rangle
$$

然而，这个方程并不完整。为了在演化过程中始终保持已占据[轨道](@entry_id:137151)的正交性，需要引入一个[拉格朗日乘子](@entry_id:142696)矩阵 $\lambda_{ij}(t)$，它是一个厄米矩阵。完整的[轨道](@entry_id:137151)[演化方程](@entry_id:268137)是：

$$
i\hbar \frac{d}{dt}|\phi_i(t)\rangle = \hat{h}[\rho(t)]|\phi_i(t)\rangle - \sum_{j=1}^{A} |\phi_j(t)\rangle \lambda_{ji}(t)
$$

这里的厄米矩阵 $\Lambda(t)$ 体现了一种**规范自由度**。我们可以通过选择不同的 $\Lambda(t)$ 来获得不同的[轨道](@entry_id:137151)演化路径。这等价于在已占据[轨道空间](@entry_id:148658)中进行任意的、随时间变化的幺正变换 $|\phi'_i(t)\rangle = \sum_j U_{ij}(t) |\phi_j(t)\rangle$。然而，正如我们前面所讨论的，这种变换不会改变物理上可观測的量，因为它们都对应于同一个[密度矩阵](@entry_id:139892) $\hat{\rho}(t)$ 和同一个多体[Slater行列式](@entry_id:139034)（仅相差一个总体相位）。因此，所有与 $\hat{\rho}(t)$ 相关的可观测量，如能量、[均方根半径](@entry_id:146552)以及任何[单体](@entry_id:136559)算符的[期望值](@entry_id:153208)，在这种变换下都是不变的。这个[规范自由度](@entry_id:160491)意味着，在TDHF中，单个[轨道](@entry_id:137151)的物理意义是模糊的，只有整个已占据[子空间](@entry_id:150286)及其对应的密度矩阵才具有明确的物理意义 [@problem_id:3609641]。

### 基本性质与守恒律

TDHF动力学内在地保持了[平均场近似](@entry_id:144121)的一致性，并遵守 underlying [哈密顿量](@entry_id:172864)的对称性所要求的守恒律。

首先，TDHF演化保持了Slater行列式状态的基本结构。由厄米[哈密顿量](@entry_id:172864) $\hat{h}[\rho]$ 生成的演化是幺正的，它保持了单粒子[轨道](@entry_id:137151)间的[内积](@entry_id:158127)。因此，如果初始[轨道](@entry_id:137151)集是正交归一的，它们在整个演化过程中将始终保持正交归一性。这直接保证了两个关键性质的守恒 [@problem_id:3609667]：

-   **粒子数守恒**：如前所述，$\mathrm{Tr}\,\hat{\rho}(t) = A$ 始终成立。
-   **[幂等性](@entry_id:190768)守恒**：如果初始[密度矩阵](@entry_id:139892)是幂等的，即 $\hat{\rho}(0)^2 = \hat{\rho}(0)$，那么在演化过程中 $\hat{\rho}(t)^2 = \hat{\rho}(t)$ 也将始终成立。这保证了系统在[演化过程](@entry_id:175749)中始终停留在[Slater行列式](@entry_id:139034)[流形](@entry_id:153038)上 [@problem_id:3609644] [@problem_id:3609658]。

其次，根据诺特定理在TDHF[变分原理](@entry_id:198028)中的体现（通常称为TDHF的[埃伦费斯特定理](@entry_id:151868)），如果系统的多体[哈密顿量](@entry_id:172864) $\hat{H}$ 具有某个连续对称性，并且该对称性由一个[单体](@entry_id:136559)算符 $\hat{Q}$生成（即 $[\hat{H}, \hat{Q}]=0$），那么在TDHF演化过程中，该算符的[期望值](@entry_id:153208) $\langle\Phi(t)|\hat{Q}|\Phi(t)\rangle$ 是守恒的。对于一个孤立的、相互作用仅依赖于相对坐标和自旋的[原子核](@entry_id:167902)系统，以下量的[期望值](@entry_id:153208)是守恒的 [@problem_id:3609667]：

-   **总能量**：如果[哈密顿量](@entry_id:172864)不显含时间，则总能量 $E(t) = \langle\Phi(t)|\hat{H}|\Phi(t)\rangle$ 是一个守恒量。
-   **总线性动量**：由于[平移不变性](@entry_id:195885)，[总动量](@entry_id:173071) $\langle\hat{\mathbf{P}}\rangle$ 守恒。
-   **[总角动量](@entry_id:155748)**：由于转动不变性，总角动量 $\langle\hat{\mathbf{J}}\rangle$ 守恒。

需要注意的是，即使多体态本身可能破坏了某些对称性（例如，一个形变的[原子核](@entry_id:167902)破坏了转动对称性），其相应物理量的[期望值](@entry_id:153208)在TDHF演化中依然是守恒的。同时，并非所有算符的[期望值](@entry_id:153208)都守恒。一个常见的例子是质心位置算符 $\hat{\mathbf{R}}_{\mathrm{cm}}$。其[期望值](@entry_id:153208)的时间导数正比于[总动量](@entry_id:173071)的[期望值](@entry_id:153208)：$\frac{d}{dt}\langle\hat{\mathbf{R}}_{\mathrm{cm}}\rangle = \frac{1}{M}\langle\hat{\mathbf{P}}\rangle$。因此，除非系统总动量为零，否则[质心](@entry_id:265015)位置的[期望值](@entry_id:153208)会随时间线性变化，而不是一个守恒量 [@problem_id:3609667]。

### 从静态到动态：HF的联系与小振幅极限

TDH[F理论](@entry_id:184208)不仅描述动力学，它还与静态的[Hartree-Fock](@entry_id:142303)（HF）理论有着深刻的联系。静态HF方法通过[变分原理](@entry_id:198028)最小化[能量泛函](@entry_id:170311) $E[\rho]$ 来寻找系统的[基态](@entry_id:150928)。这一过程最终会得到一组满足自洽HF方程 $h[\rho_0] |\phi_i\rangle = \epsilon_i |\phi_i\rangle$ 的单粒子[轨道](@entry_id:137151)。

从这个结果可以看出，基态[密度矩阵](@entry_id:139892) $\rho_0 = \sum_i |\phi_i\rangle\langle\phi_i|$ 的[本征态](@entry_id:149904)就是HF[哈密顿量](@entry_id:172864) $h[\rho_0]$ 的[本征态](@entry_id:149904)。这意味着这两个算符可以[同时对角化](@entry_id:196036)，因此它们相互对易：$[h[\rho_0], \rho_0] = 0$。将这个[对易关系](@entry_id:136780)代入TDHF方程 $i\hbar \dot{\rho} = [h[\rho], \rho]$，我们立即得到 $\dot{\rho}=0$。这表明，**静态HF[基态](@entry_id:150928)是TDHF方程的一个驻定解** [@problem_id:3609645]。此时，单个[轨道](@entry_id:137151)会演化一个相位因子 $e^{-i\epsilon_i t/\hbar}$，但[密度矩阵](@entry_id:139892)和所有[可观测量](@entry_id:267133)都保持不变。

TDHF的威力在于描述系统偏离[平衡态](@entry_id:168134)的动力学。一个特别重要的极限是**小振幅极限**，它研究的是系统在HF[基态](@entry_id:150928)附近的微小[振动](@entry_id:267781)。通过将TDHF方程在静态HF解 $\rho_0$ 附近进行线性化，即设 $\rho(t) = \rho_0 + \delta\rho(t)$，我们可以推导出描述这些[振动](@entry_id:267781)模式的方程。这个线性化的TDH[F理论](@entry_id:184208)，正是著名的**随机相近似（Random Phase Approximation, RPA）** [@problem_id:3609675]。

在线性化过程中，可以证明[密度矩阵](@entry_id:139892)的微扰 $\delta\rho(t)$ 只在粒子-空穴（ph）和空穴-粒子（hp）块中具有非零矩阵元。换句话说，微小的集体[振动](@entry_id:267781)是由粒子-空穴对的[相干叠加](@entry_id:170209)构成的。RPA方程最终可以写成一个非厄米的矩阵本征值问题：

$$
\begin{pmatrix} A  B \\ B^*  A^* \end{pmatrix}
\begin{pmatrix} X \\ Y \end{pmatrix}
= \hbar\omega
\begin{pmatrix} I  0 \\ 0  -I \end{pmatrix}
\begin{pmatrix} X \\ Y \end{pmatrix}
$$

其中，$X$ 和 $Y$ 分别是激发（前向）和退激发（后向）振幅的矢量。矩阵 $A$ 和 $B$ 的元素由HF[单粒子能量](@entry_id:160812)和[剩余相互作用](@entry_id:159129)的粒子-空穴矩阵元决定。这个方程的解 $\hbar\omega$ 对应于系统的集体激发[能谱](@entry_id:181780)，例如[巨共振](@entry_id:159268)。如果忽略后向振幅 $Y$（即令 $B=0$），RPA就简化为[Tamm-Dancoff近似](@entry_id:178323)（TDA）。如果进一步忽略所有[剩余相互作用](@entry_id:159129)，RPA的[激发能](@entry_id:190368)就退化为纯粹的、非相干的粒子-空穴能量差 $\epsilon_p - \epsilon_h$ [@problem_id:3609675] [@problem_id:1187405]。

### 高级主题与扩展

#### 伽利略不变性与[能量密度泛函](@entry_id:161351)

在实际的TDHF计算中，尤其是在核物理领域，通常使用如Skyrme力之类的[能量密度泛函](@entry_id:161351)（EDF）。这些泛函的构建必须遵守基本的物理对称性，其中之一就是伽利略[不变性](@entry_id:140168)。为了描述动力学，EDF不仅需要包含静态计算中常见的**[时间反演](@entry_id:182076)偶性**密度（如粒子[数密度](@entry_id:268986) $\rho$、动能密度 $\tau$ 和自旋-[轨道](@entry_id:137151)流 $\mathbf{J}$），还必须包含**时间反演示性**的密度（如流密度 $\mathbf{j}$、自旋密度 $\mathbf{s}$ 和自旋-动能密度 $\mathbf{T}$）。

时间反演示性密度在[时间反演](@entry_id:182076)不变的[基态](@entry_id:150928)（如偶偶[核基态](@entry_id:161082)）中[期望值](@entry_id:153208)为零，但在动力学过程中会变为非零，并且是不可或缺的。例如，流密度 $\mathbf{j}$ 是粒子数守恒的[连续性方程](@entry_id:195013) $\partial_t \rho + \nabla \cdot \mathbf{j} = 0$ 中的关键部分。

伽利略[不变性](@entry_id:140168)要求系统的内部能量在伽利略变换（即切换到匀速运动的[参考系](@entry_id:169232)）下不变。这一要求对EDF中各项的耦合常数施加了严格的约束。例如，它要求动能密度项和流动密度项必须以特定的组合形式 $\rho\tau - (\text{const}) \mathbf{j}^2$ 出现。这导致了与时间偶性项相关的[耦合常数](@entry_id:747980)和与时间奇性项相关的耦合常数之间必须存在确定的关系。不遵守这些约束的泛函会在动力学计算中引入虚假的[质心运动](@entry_id:178374)和[能量不守恒](@entry_id:276143)等问题 [@problem_id:3609621]。

#### 超越平均场：对关联与TDHFB

TDH[F理论](@entry_id:184208)作为一个纯粹的平均场理论，其核心局限在于它忽略了粒子间的[短程关联](@entry_id:158693)，特别是**对关联**。对关联是导致[原子核](@entry_id:167902)出现超流现象的根源。在TDHF的[Slater行列式](@entry_id:139034)框架中，粒子数是一个精确的量子数，这与描述超流体所需的粒子数不守恒的BCS或HFB[波函数](@entry_id:147440)是根本矛盾的。因此，TDHF无法描述对[振动](@entry_id:267781)、对转移、以及对关联起重要作用的低能裂变等动力学过程。

为了克服这一局限，TDH[F理论](@entry_id:184208)被推广为**含时[Hartree-Fock-Bogoliubov](@entry_id:750190)（TDHFB）理论**。TDHFB将[试探波函数](@entry_id:142892)[流形](@entry_id:153038)从Slater行列式扩展到[Bogoliubov准粒子](@entry_id:139560)真空态。这些态是粒子和空穴的线性叠加，因而不再具有确定的粒子数。

TD[HFB理论](@entry_id:750250)的引入带来了新的物理量——**反常密度**（anomalous density）$\kappa_{ij} = \langle\Psi| c_j c_i |\Psi\rangle$。它描述了Cooper对的振幅，是对关联存在的直接标志。在TDHF中，由于粒子数守恒，反常密度恒为零。而在TDHFB中，$\kappa$ 和正常的密度 $\rho$ 一样，成为了一个动力学变量，并与一个反常的平均场（对力场）$\Delta$ 共轭。TDHFB的[运动方程](@entry_id:170720)同时演化正常密度和反常密度，从而能够描述对关联的动力学演化。尽管TDHFB态的粒子数不确定，但其[平均粒子数](@entry_id:151202)在演化中是守恒的，并且理论依然满足[连续性方程](@entry_id:195013)。通过引入反常密度这一额外的集体自由度，TDHFB极大地扩展了平均场理论的应用范围，使其能够对广泛的核超流动力学现象进行微观描述 [@problem_id:3609664]。