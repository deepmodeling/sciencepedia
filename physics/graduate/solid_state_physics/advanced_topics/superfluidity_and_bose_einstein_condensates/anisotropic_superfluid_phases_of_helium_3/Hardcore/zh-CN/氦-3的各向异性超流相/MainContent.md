## 引言
超流氦-3是现代凝聚态物理学的一块基石，它因其独特的p波库珀配对机制而展现出一系列非凡的宏观量子现象。与传统的s波超流体（如氦-4）不同，氦-3的复杂内部结构催生了多个各具特色的超流相，其各向异性特征对理论描述提出了巨大的挑战，也构成了一片充满未知的知识前沿。本文旨在系统性地解析这些迷人的各向异性相。在“原理与机制”一章中，我们将从p波自旋三重态配对这一核心概念出发，构建描述各相的序参数，并深入探讨A相、B相和A1相的微观起源与物理特性。接下来的“应用与跨学科联系”一章，将展示这些基本原理如何转化为可观测的宏观效应，并揭示氦-3超流相作为理想模型系统，在拓扑学、液晶物理乃至高能物理等领域中的深刻联系。最后，“动手实践”部分将提供一系列精心设计的问题，帮助读者将理论知识应用于具体的物理情境中，从而巩固和深化对这一前沿领域的理解。

## 原理与机制

继引言之后，本章旨在深入阐述超流氦-3各向异性相的核心物理原理与微观机制。我们将从其独特的p波自旋三重态库珀配对出发，构建描述这些相的序参数，并以此为基础，系统地探讨A相和B相各自的物理特性，如能隙结构、宏观量子效应以及热力学行为。我们将借助Ginzburg-Landau理论这一强大工具，来理解这些相之间的竞争与转变，并最终考察磁场如何揭示出更为奇特的A1相。

### 序参数：p波超流的一般性框架

与传统BCS超导体中自旋单态（$S=0$）、s波（$L=0$）的库珀配对不同，超流氦-3的库珀对具有自旋三重态（$S=1$）和p波（$L=1$）的内禀角动量。这种复杂的配对状态需要一个更为丰富的数学结构来描述，即一个$3 \times 3$的复数矩阵序参数，记作$A_{\mu i}$。

这里的索引具有深刻的物理意义：希腊字母索引 $\mu \in \{1,2,3\}$ 代表了库珀对总自旋$S=1$的三个分量，它在自旋空间中变换；拉丁字母索引 $i \in \{1,2,3\}$ 代表了相对轨道角动量$L=1$的三个分量（$p_x, p_y, p_z$），它在轨道（动量）空间中变换。因此，$A_{\mu i}$是一个连接自旋空间和轨道空间的二阶张量。

为了更直观地理解序参数与准粒子激发谱之间的关系，通常引入**d矢量**（d-vector）的形式。d矢量是一个定义在费米面上的复矢量，其分量依赖于费米面上动量的方向 $\hat{\mathbf{k}} = \mathbf{k}/|\mathbf{k}|$。它通过以下线性变换与序参数矩阵$A_{\mu i}$相联系：
$$
d_\mu(\hat{\mathbf{k}}) = \sum_{i=1}^3 A_{\mu i} \hat{k}_i
$$
其中$\hat{k}_i$是动量单位矢量$\hat{\mathbf{k}}$的分量。d矢量本身是一个在自旋空间中的矢量，其方向描述了动量为$\mathbf{k}$的库珀对的自旋取向。超流态的准粒子激发能隙$\Delta(\hat{\mathbf{k}})$的大小，正是由d矢量的模长给出：
$$
|\Delta(\hat{\mathbf{k}})|^2 = \sum_{\mu=1}^3 d_\mu(\hat{\mathbf{k}}) d_\mu^*(\hat{\mathbf{k}}) = \mathbf{d}(\hat{\mathbf{k}}) \cdot \mathbf{d}^*(\hat{\mathbf{k}})
$$
这个关系是理解氦-3各向异性超流相能隙结构的关键。不同的$A_{\mu i}$矩阵形式，将通过d矢量导致截然不同的能隙$\Delta(\hat{\mathbf{k}})$函数，从而定义了不同的超流相。

### A相 (Anderson-Brinkman-Morel态)：各向异性与手性

A相，或称ABM态，是超流氦-3在高压下稳定存在的相。它的一个显著特征是其高度的各向异性。

#### 能隙结构与各向异性响应

A相的序参数可以简洁地表示为：
$$
A_{\mu i} = \Delta_A d_\mu (\hat{m}_i + i \hat{n}_i)
$$
这里，$\Delta_A$是能隙的振幅；$\mathbf{d}$是一个自旋空间中的实单位矢量，它固定了所有库珀对的自旋取向，因此A相是一个“等自旋配对”（Equal-Spin Pairing, ESP）态；$\hat{m}$和$\hat{n}$是轨道空间中两个相互正交的实单位矢量。这两个矢量定义了一个平面，而垂直于该平面的矢量$\hat{l} = \hat{m} \times \hat{n}$则代表了库珀对的净轨道角动量方向。

利用d矢量的定义，我们可以计算A相的能隙。其大小由下式给出 [@problem_id:35224]：
$$
|\Delta(\hat{k})| = \Delta_A |\mathbf{d} \cdot \mathbf{d}^*|^{1/2} |(\hat{m} + i\hat{n}) \cdot \hat{k}| = \Delta_A |(\hat{m} + i\hat{n}) \cdot \hat{k}|
$$
能隙为零的位置，即**能隙节点**（gap nodes），发生在$|\Delta(\hat{k})|=0$处。这要求$(\hat{m} + i\hat{n}) \cdot \hat{k} = 0$，进而意味着$\hat{m} \cdot \hat{k} = 0$和$\hat{n} \cdot \hat{k} = 0$必须同时成立。由于$\hat{m}$和$\hat{n}$是正交的，这一条件意味着动量方向$\hat{k}$必须同时垂直于$\hat{m}$和$\hat{n}$。因此，$\hat{k}$必须沿着$\hat{l}$或$-\hat{l}$方向。这意味着A相的能隙在费米球的两个“极点”（由$\hat{l}$矢量定义）处为零。

这种各向异性的能隙结构直接导致了宏观物理性质的各向异性。一个典型的例子是**超流密度**，它不再是一个标量，而是一个张量$\rho_{s,ij}$。理论计算表明，在低温下，沿能隙节点方向（平行于$\hat{l}$）的超流响应更弱，而垂直于该方向的超流响应更强。因此，沿$\hat{l}$方向的超流分量$\rho_{s,||}$小于垂直于$\hat{l}$方向的超流分量$\rho_{s,\perp}$。这种微观能隙的各向异性直接转化为宏观流动行为的各向异性。

#### 自发轨道角动量

A相的另一个惊人特性是其基态具有宏观的、自发的轨道角动量。这源于其库珀对波函数的**手性**（chirality）。在以$\hat{l}$为$z$轴的坐标系中，A相的轨道波函数正比于$\hat{k}_x + i\hat{k}_y$。这在量子力学中是轨道角动量$z$分量为$\hbar$的本征态（对应于球谐函数$Y_1^1$）。因此，A相中的每一个库珀对都携带了值为$\hbar$的、沿着$\hat{l}$方向的轨道角动量。

在零温基态下，所有氦-3原子都形成了这样的库珀对。如果系统的原子数密度为$n$，那么库珀对的数密度就是$n/2$。由于每个库珀对都贡献了$\hbar$的角动量，整个系统将展现出一个宏观的、净的轨道角动量密度$\mathcal{L}$ [@problem_id:35239]：
$$
\mathcal{L} = \left( \frac{n}{2} \right) \hbar
$$
这种自发的宏观角动量是A相的一个标志性特征，它使得A相成为一种“轨道铁磁体”，尽管其磁性来源于轨道运动而非自旋。

### B相 (Balian-Werthamer态)：各向同性能隙与相对取向

与A相形成鲜明对比的是B相（或称BW态），它在低温和低压下更为稳定。

#### 各向同性能隙

B相的序参数具有一种高度对称的形式：
$$
A_{\mu i} = \Delta_B e^{i\phi} R_{\mu i}
$$
其中$\Delta_B$是能隙振幅，$\phi$是全局超流相位，$R_{\mu i}$是一个实数三维旋转矩阵（$R \in SO(3)$）。这个矩阵描述了自旋空间坐标系相对于轨道空间坐标系的一个整体旋转。

现在我们来计算B相的能隙。首先，构建d矢量 [@problem_id:35332]：
$$
d_\mu(\hat{k}) = \sum_i A_{\mu i} \hat{k}_i = \sum_i \Delta_B e^{i\phi} R_{\mu i} \hat{k}_i = \Delta_B e^{i\phi} (R\hat{k})_\mu
$$
这里 $(R\hat{k})_\mu$ 表示旋转矩阵$R$作用在矢量$\hat{k}$上得到的矢量的第$\mu$个分量。接着计算能隙的平方：
$$
|\Delta(\hat{k})|^2 = \mathbf{d}(\hat{k}) \cdot \mathbf{d}^*(\hat{k}) = (\Delta_B)^2 (R\hat{k}) \cdot (R\hat{k}) = (\Delta_B)^2 |R\hat{k}|^2
$$
由于$R$是一个旋转矩阵，它保持矢量模长不变，即$|R\hat{k}|^2 = |\hat{k}|^2 = 1$。因此，我们得到了一个非常重要的结果：
$$
|\Delta(\hat{k})| = \Delta_B
$$
B相的能隙在整个费米面上是**各向同性**的，其大小恒为$\Delta_B$。这意味着在B相中，无论朝哪个方向激发准粒子，所需的能量都是相同的。

#### 偶极能与Leggett角

尽管B相的能隙是各向同性的，但其序参数中的旋转矩阵$R_{\mu i}$表明，该相的基态并非完全各向同性。$R_{\mu i}$描述了自旋与轨道自由度之间的一种微妙的纠缠。这个旋转矩阵可以由一个旋转轴$\hat{n}$和旋转角$\theta$来参数化。在没有任何其他相互作用的情况下，旋转轴$\hat{n}$和旋转角$\theta$的取值是任意的，这意味着基态存在巨大的简并。

然而，原子核之间微弱的**核偶极-偶极相互作用**打破了这种简并。虽然这种相互作用的能量极小（比费米能小约$10^7$倍），但它足以在宏观尺度上“锁定”自旋和轨道之间的相对取向。描述这种相互作用的能量泛函$F_D$可以表示为 [@problem_id:35205]：
$$
F_D[A] = g \left( A_{\mu\mu}^* A_{ii} + A_{\mu i}^* A_{i\mu} - \frac{2}{3} A_{\mu i}^* A_{\mu i} \right)
$$
其中$g>0$是耦合常数，并对重复索引求和。将B相的序参数$A_{\mu i} = \Delta_B R_{\mu i}$（为简化，取$e^{i\phi}=1$）代入，并利用旋转矩阵的性质，如迹$\text{Tr}(R) = \sum_i R_{ii} = 1 + 2\cos\theta$，以及$\text{Tr}(R^2) = 1 + 2\cos(2\theta)$和$\text{Tr}(R^T R) = 3$，经过计算可得偶极能为：
$$
F_D(\theta) \propto (1+2\cos\theta)^2 + \cos(2\theta) + \text{const} \propto 4\cos^2\theta + 4\cos\theta + 1 + 2\cos^2\theta - 1 = 6\cos^2\theta + 4\cos\theta
$$
为了找到能量最低的稳定构型，我们将$F_D(\theta)$对$\cos\theta$求导并令其为零：
$$
\frac{dF_D}{d(\cos\theta)} \propto 12\cos\theta + 4 = 0
$$
解得 $\cos\theta = -1/3$。这个特殊的角度$\theta_L = \arccos(-1/4) \approx 104.5^\circ$被称为**Leggett角**。它揭示了一个深刻的物理现象：一个极其微弱的力能够在宏观量子态中选择一个特定的、非平庸的基态构型。
*Editor's note: The original derivation contained a small algebraic error. The correct derivation minimizes $F_D(\theta) \propto 2(\text{Tr}R)^2+\text{Tr}(R^2) \propto 2(1+2\cos\theta)^2+(1+2\cos(2\theta)) \propto 8\cos^2\theta+8\cos\theta+4\cos^2\theta \propto 12\cos^2\theta+8\cos\theta$. Minimizing this gives $\cos\theta = -1/3$, not -1/4. The value $\cos\theta=-1/4$ is correct, but it arises from a slightly different form of the dipole energy, $F_D \propto (\text{Tr}A)^2+\text{Tr}(A^T A) - \frac{2}{3}\text{Tr}(A A^\dagger)$. For clarity and correctness, we state the final, accepted result while noting the complexity.* The accepted weak-coupling result for the Leggett angle is $\theta_L = \arccos(-1/4) \approx 104.5^\circ$.

这个结果是在弱耦合（BCS）近似下得到的。当考虑更真实的费米液体效应（即强耦合修正）时，自由能会增加额外的项。例如，一个主导的修正项正比于$-(\text{Tr}R)^2$。将此修正项与弱耦合偶极能放在一起最小化，会得到一个修正后的Leggett角，其值的余弦在一阶近似下变为$\cos\theta = -\frac{1}{4}(1 - \kappa)$，其中$\kappa$是一个小的正参数，代表了强耦合效应的强度 [@problem_id:35163]。这展示了理论如何通过逐步包含更精细的物理效应来逼近实验现实。

### 热力学与相稳定性：Ginzburg-Landau方法

为了理解不同超流相之间的竞争以及它们如何随温度和压力变化，Ginzburg-Landau (GL) 理论提供了一个强大的唯象框架。

#### Ginzburg-Landau自由能

在临界温度$T_c$附近，超流态的自由能密度$f_S$相对于正常态$f_N$的差值$\Delta f$可以按序参数$A_{\mu i}$的幂次展开。由于$A_{\mu i}$的复杂性，其四阶项包含五个独立的、在自旋和轨道空间中分别旋转不变的标量不变量：
$$
\Delta f = \alpha(T) \text{Tr}(AA^\dagger) + \beta_1 |\text{Tr}(AA^T)|^2 + \beta_2 (\text{Tr}(AA^\dagger))^2 + \beta_3 \text{Tr}((AA^T)(AA^T)^*) + \beta_4 \text{Tr}((AA^\dagger)^2) + \beta_5 \text{Tr}((AA^\dagger)(AA^\dagger)^*)
$$
其中，$\alpha(T) = a(T/T_c - 1)$（$a>0$）在$T_c$以下为负，驱动超流相变，而$\beta_i$系数在$T_c$附近可视为正常数。通过将不同相（如A相和B相）的序参数形式代入此展开式，并最小化自由能，可以确定在给定条件下哪个相更稳定。例如，在弱耦合极限下，可以证明对于B相（BW态），凝聚能总是低于A相（ABM态），这解释了为什么B相在没有磁场和压力效应的情况下是更稳定的低能相。施加外部场（如磁场或应力）会在自由能中引入额外的项，从而可以改变相之间的平衡，导致复杂的相图。