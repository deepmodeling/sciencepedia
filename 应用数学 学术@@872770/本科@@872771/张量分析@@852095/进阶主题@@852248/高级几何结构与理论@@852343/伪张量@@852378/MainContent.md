## 引言
在物理学和数学中，张量是描述物理定律在不同[坐标系](@entry_id:156346)下保持形式不变的关键工具。然而，除了我们所熟知的“真张量”外，还存在一类行为略有不同的重要对象——[伪张量](@entry_id:193048)（pseudotensors）。它们在处理涉及旋转、手性和定向的物理现象时至关重要，但其独特的变换性质常常成为初学者的困惑点。本文旨在系统地揭开[伪张量](@entry_id:193048)的神秘面纱，弥合对这一基本概念的理解差距。在接下来的内容中，我们将首先在“原理与机制”一章中深入探讨[伪张量](@entry_id:193048)的严格定义、其与真张量的根本区别，以及[Levi-Civita符号](@entry_id:155382)作为其原型的核心作用。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将通过经典力学、电磁学、凝聚态物理乃至广义相对论中的丰富实例，展示[伪张量](@entry_id:193048)如何成为描述角动量、[磁场](@entry_id:153296)和[引力能](@entry_id:193726)量等关键物理量的必要工具。最后，通过“动手实践”部分，读者将有机会通过具体计算来巩固对伪[张量变换](@entry_id:183453)特性的理解。

## 原理与机制

在对[张量变换](@entry_id:183453)性质的初步研究中，我们专注于那些在坐标变换下表现“良好”的物理量。一个真张量（true tensor），无论其阶数如何，其分量在新[坐标系](@entry_id:156346)中的表达都可以通过旧[坐标系](@entry_id:156346)中的分量与[坐标变换](@entry_id:172727)[偏导数](@entry_id:146280)的乘积精确得出。这种协变性是物理定律在不同[参考系](@entry_id:169232)下保持形式不变（即[协变性原理](@entry_id:275808)）的数学基石。然而，物理学和几何学中存在一类同样重要的对象，它们在[坐标变换](@entry_id:172727)下的行为与真张量略有不同，它们被称为**[伪张量](@entry_id:193048)（pseudotensors）**，或称[张量密度](@entry_id:191194)。本章旨在深入阐述[伪张量](@entry_id:193048)的定义、核心原理及其在物理学中的重要作用。

### [伪张量](@entry_id:193048)的定义：变换法则中的额外因子

让我们首先回顾一个[逆变](@entry_id:192290)$n$阶**真张量** $T^{i_1 \dots i_n}$ 的变换法则。在从[坐标系](@entry_id:156346) $x$ 到 $x'$ 的变换中，其分量变换如下：
$$ T'^{i_1 \dots i_n}(x') = \frac{\partial x'^{i_1}}{\partial x^{j_1}} \dots \frac{\partial x'^{i_n}}{\partial x^{j_n}} T^{j_1 \dots j_n}(x) $$
这里我们遵循了爱因斯坦求和约定。相应地，一个[协变](@entry_id:634097) $n$ 阶真张量的变换法则为：
$$ T'_{i_1 \dots i_n}(x') = \frac{\partial x^{j_1}}{\partial x'^{i_1}} \dots \frac{\partial x^{j_n}}{\partial x'^{i_n}} T_{j_1 \dots j_n}(x) $$
这些法则的本质在于，变换完全由雅可比矩阵 $J^i_j = \frac{\partial x'^i}{\partial x^j}$ 及其逆矩阵的元素决定。

现在，我们引入**[伪张量](@entry_id:193048)**的定义。一个[伪张量](@entry_id:193048)（更准确地说是权重为 $W=+1$ 的[张量密度](@entry_id:191194)）的变换法则，是在真[张量变换法则](@entry_id:185176)的基础上，额外乘上一个因子——雅可比[矩阵的[行列](@entry_id:148198)式](@entry_id:142978) $\det(J)$。例如，一个[逆变](@entry_id:192290) $n$ 阶[伪张量](@entry_id:193048) $P^{i_1 \dots i_n}$ 的变换法则是：
$$ P'^{i_1 \dots i_n}(x') = \det(J) \frac{\partial x'^{i_1}}{\partial x^{j_1}} \dots \frac{\partial x'^{i_n}}{\partial x^{j_n}} P^{j_1 \dots j_n}(x) $$
这个额外的因子 $\det(J)$ 包含了关于[坐标变换](@entry_id:172727)如何影响空间“定向”或“手性”的信息。如果一个变换保持定向（例如，从[右手坐标系](@entry_id:166669)变换到另一个[右手坐标系](@entry_id:166669)），那么 $ \det(J) > 0 $。如果变换反转了定向（例如，从[右手坐标系](@entry_id:166669)变换到左手[坐标系](@entry_id:156346)），则 $ \det(J)  0 $。

为了清晰地揭示真张量与[伪张量](@entry_id:193048)之间的根本差异，让我们考虑一个在三维欧几里得空间中最具启发性的变换：**空间反演（parity transformation）**，即 $x'^i = -x^i$。这个变换将每个点的坐标都反号，相当于通过原点进行镜像反射。

对于这个变换，雅可比矩阵为 $J^i_j = \frac{\partial x'^i}{\partial x^j} = -\delta^i_j$。这是一个对角线上元素均为 $-1$ 的对角矩阵。在三维空间中，其[行列式](@entry_id:142978)为 $\det(J) = (-1)^3 = -1$。

现在，我们来考察一个三阶逆变真张量 $T^{ijk}$ 和一个三阶[逆变](@entry_id:192290)[伪张量](@entry_id:193048) $P^{ijk}$ 在此变换下的行为 [@problem_id:1532727]。

对于真张量 $T^{ijk}$：
$$ T'^{ijk} = \frac{\partial x'^i}{\partial x^p} \frac{\partial x'^j}{\partial x^q} \frac{\partial x'^k}{\partial x^r} T^{pqr} = (-\delta^i_p)(-\delta^j_q)(-\delta^k_r) T^{pqr} = (-1)^3 T^{ijk} = -T^{ijk} $$
可见，这个奇数阶的真张量在空间反演下会反号。

而对于[伪张量](@entry_id:193048) $P^{ijk}$：
$$ P'^{ijk} = \det(J) \frac{\partial x'^i}{\partial x^p} \frac{\partial x'^j}{\partial x^q} \frac{\partial x'^k}{\partial x^r} P^{pqr} = (-1) \cdot (-\delta^i_p)(-\delta^j_q)(-\delta^k_r) P^{pqr} = (-1) \cdot (-1)^3 P^{ijk} = P^{ijk} $$
令人惊讶的是，这个奇数阶的[伪张量](@entry_id:193048)在空间反演下保持不变。

这个简单的例子深刻地揭示了[伪张量](@entry_id:193048)的本质：它们携带了关于[坐标系](@entry_id:156346)定向的信息，这使得它们在處理与旋转、手性和体积相关的物理量时不可或缺。值得注意的是，如果一个[伪张量](@entry_id:193048) $P^{ij}$ 在某个[坐标系](@entry_id:156346)下是对称的（即 $P^{ij} = P^{ji}$），那么在空间反演后，其新分量 $P'^{ij} = -P^{ij}$ 仍然保持对称性，因为 $P'^{ji} = -P^{ji} = -P^{ij} = P'^{ij}$ [@problem_id:1532755]。这表明对称性这类内在的代数属性在变换中是稳健的。

### Levi-Civita 符号：[伪张量](@entry_id:193048)的原型

理解[伪张量](@entry_id:193048)的关键在于认识一个 omnipresent 的数学工具：**Levi-Civita 符号** $\epsilon_{ijk}$（在三维情况下）。它被定义为：
- 如果 $(i,j,k)$ 是 $(1,2,3)$ 的偶[排列](@entry_id:136432)，则 $\epsilon_{ijk} = +1$。
- 如果 $(i,j,k)$ 是 $(1,2,3)$ 的奇[排列](@entry_id:136432)，则 $\epsilon_{ijk} = -1$。
- 如果任何两个索引相同，则 $\epsilon_{ijk} = 0$。

尽管 Levi-Civita 符号带有索引，但它本身**不是一个真张量**。它的分量在所有[坐标系](@entry_id:156346)下都被定义为相同的数值（+1, -1, 0）。如果它是一个真张量，它的分量会根据标准张量法则进行变换，从而在新的[坐标系](@entry_id:156346)中取到不同的值。

事实上，Levi-Civita 符号的行为正是[伪张量](@entry_id:193048)的“原型”。考虑一个从右手标准正交基 $(\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_3)$ 到一个新的正交基 $(\mathbf{e}'_1, \mathbf{e}'_2, \mathbf{e}'_3)$ 的变换，这个变换由一个正交矩阵 $R$ 描述。可以证明，Levi-Civita 符号的变换满足如下关系：
$$ \epsilon_{pqr} R_{ip} R_{jq} R_{kr} = \det(R) \epsilon_{ijk} $$
这意味着如果我们试图将 $\epsilon_{ijk}$ 作为一个张量进行变换，我们会得到 $\epsilon'_{ijk} = \det(R) \epsilon_{ijk}$。

让我们通过一个具体的例子来理解这一点。假设新[坐标系](@entry_id:156346) $S'$ 是通过反射其中一个轴得到的，例如 $x'_1=x_1$, $x'_2=x_2$, $x'_3=-x_3$。这是一个从[右手系](@entry_id:166669)到左手系的变换，其变换矩阵为 $R = \mathrm{diag}(1,1,-1)$，[行列式](@entry_id:142978) $\det(R)=-1$。如果我们计算新[坐标系](@entry_id:156346)下的 $\epsilon'_{123}$ 分量，我们会发现：
$$ \epsilon'_{123} = \det(R) \epsilon_{123} = (-1)(1) = -1 $$
[@problem_id:1532733]。这个结果说明，为了保持 Levi-Civita 符号与叉乘和[行列式](@entry_id:142978)的内在联系，它的分量必须在定向反转的[坐标系](@entry_id:156346)中改变符号。

更普遍地，Levi-Civita 符号 $\epsilon_{i_1 \dots i_n}$ 被视为一个 $n$ 阶全[协变](@entry_id:634097)**[伪张量](@entry_id:193048)**，其权重为 $W=+1$。这意味着它的变换法则精确地为：
$$ \epsilon'_{j_1 \dots j_n} = (\det J) \frac{\partial x^{i_1}}{\partial x'^{j_1}} \dots \frac{\partial x^{i_n}}{\partial x'^{j_n}} \epsilon_{i_1 \dots i_n} $$
我们可以验证这个法则。根据[行列式](@entry_id:142978)的一个基本恒等式，我们有 $\sum \epsilon_{i_1 \dots i_n} M^{i_1}_{j_1} \dots M^{i_n}_{j_n} = (\det M) \epsilon_{j_1 \dots j_n}$。令 $M$ 为逆雅可比矩阵 $M_{ij} = \frac{\partial x^i}{\partial x'^j}$，其[行列式](@entry_id:142978)为 $(\det J)^{-1}$。根据其作为权重+1的[协变](@entry_id:634097)[伪张量](@entry_id:193048)的变换法则，并结合上述[行列式恒等式](@entry_id:635080)，我们发现变换后的分量为 $(\det J) \times ((\det J)^{-1} \epsilon_{j_1 \dots j_n}) = \epsilon_{j_1 \dots j_n}$，这与 $\epsilon$ 在所有[坐标系](@entry_id:156346)下分量恒定的事实相符，从而证实了其权重为+1的[伪张量](@entry_id:193048)特性 [@problem_id:1532756] [@problem_id:1532714]。

### 物理世界中的[伪张量](@entry_id:193048)

[伪张量](@entry_id:193048)的概念远非数学上的抽象。许多重要的物理量本质上就是[伪张量](@entry_id:193048)。

#### [伪标量](@entry_id:196696)：有向体积与手性度量

一个零阶[伪张量](@entry_id:193048)被称为**[伪标量](@entry_id:196696) (pseudoscalar)**。它在坐标变换下遵循 $\Phi' = \det(J) \Phi$。在空间反演下，由于 $\det(J)=-1$，[伪标量](@entry_id:196696)会反号，即 $\Phi' = -\Phi$，而真标量则保持不变。

一个典型的[伪标量](@entry_id:196696)是在三维空间中由三个矢量 $\vec{A}$, $\vec{B}$, $\vec{C}$ 构成的**[标量三重积](@entry_id:177480)** [@problem_id:1532744]：
$$ \Phi = \vec{A} \cdot (\vec{B} \times \vec{C}) = \epsilon_{ijk} A^i B^j C^k $$
这个量代表了由这三个矢量张成的平行六面体的**有向体积** [@problem_id:1532758]。如果 $(\vec{A}, \vec{B}, \vec{C})$构成一个[右手系](@entry_id:166669)，体积为正；如果构成左手系，体积为负。在空间反演下，三个矢量都反号 $\vec{A} \to -\vec{A}$, etc.，因此体积变为：
$$ \Phi' = (-\vec{A}) \cdot ((-\vec{B}) \times (-\vec{C})) = -\vec{A} \cdot (\vec{B} \times \vec{C}) = -\Phi $$
这正是[伪标量](@entry_id:196696)的标志性行为。类似地，在二维空间中，由两个矢量 $\vec{A}$ 和 $\vec{B}$ 定义的量 $S = A^1 B^2 - A^2 B^1$（即它们所张成的平行四边形的[有向面积](@entry_id:169588)）也是一个[伪标量](@entry_id:196696) [@problem_id:1532738]。

#### [伪矢量](@entry_id:196296)：旋转的代表

一阶[伪张量](@entry_id:193048)被称为**伪矢量 (pseudovector)** 或**[轴矢量](@entry_id:196296) (axial vector)**。它们通常与旋转、角动量和[磁场](@entry_id:153296)相关。一个典型的[伪矢量](@entry_id:196296)是由两个[真矢量](@entry_id:190731)（也称[极矢量](@entry_id:184542), polar vector）的**叉乘**生成的。例如，$\vec{C} = \vec{A} \times \vec{B}$。

在空间反演下，[真矢量](@entry_id:190731)反号（如位置 $\vec{r} \to -\vec{r}$，速度 $\vec{v} \to -\vec{v}$）。因此，叉乘的结果变换为：
$$ \vec{C}' = \vec{A}' \times \vec{B}' = (-\vec{A}) \times (-\vec{B}) = \vec{A} \times \vec{B} = \vec{C} $$
可见，[伪矢量](@entry_id:196296)在空间反演下不改变方向，这与[真矢量](@entry_id:190731)截然相反。物理学中的重要例子包括：
- **角动量** $\vec{L} = \vec{r} \times \vec{p}$ ([真矢量](@entry_id:190731) $\times$ [真矢量](@entry_id:190731) = 伪矢量)
- **[磁场](@entry_id:153296)** $\vec{B}$ (其产生与电流和运动[电荷](@entry_id:275494)的叉乘关系有关)
- **力矩** $\vec{\tau} = \vec{r} \times \vec{F}$

#### 物理定律的[宇称守恒](@entry_id:160454)

[伪张量](@entry_id:193048)的概念对于检验物理定律的对称性至关重要，特别是**[宇称守恒](@entry_id:160454) (parity conservation)**。[宇称守恒](@entry_id:160454)要求物理定律在空间反演下保持形式不变。这意味着定律方程的每一项都必须具有相同的变换属性（都是真标量，或都是[伪标量](@entry_id:196696)等）。

我们可以构建不同类型的标量 [@problem_id:1532703]：
- **[真矢量](@entry_id:190731) $\cdot$ [真矢量](@entry_id:190731) $\to$ 真标量**: 例如，动能 $\frac{1}{2}m\vec{v}\cdot\vec{v}$。在反演下 $(-\vec{v})\cdot(-\vec{v}) = \vec{v}\cdot\vec{v}$，不变。
- **[伪矢量](@entry_id:196296) $\cdot$ 伪矢量 $\to$ 真标量**: 例如，$\vec{L}\cdot\vec{L}$。在反演下 $(\vec{L})\cdot(\vec{L}) = \vec{L}\cdot\vec{L}$，不变。
- **[真矢量](@entry_id:190731) $\cdot$ [伪矢量](@entry_id:196296) $\to$ [伪标量](@entry_id:196696)**: 例如，粒子在[磁场](@entry_id:153296)中的[相互作用项](@entry_id:637283) $\vec{v} \cdot \vec{B}$。在反演下 $(-\vec{v})\cdot(\vec{B}) = -(\vec{v}\cdot\vec{B})$，反号。这类项在描述[弱相互作用](@entry_id:157579)等[宇称不守恒](@entry_id:160658)的过程中至关重要。

### [广义坐标](@entry_id:156576)与度规空间中的[伪张量](@entry_id:193048)

当我们将讨论从[欧几里得空间](@entry_id:138052)推广到一般的弯曲[流形](@entry_id:153038)时，[伪张量](@entry_id:193048)的概念变得更加深刻，并与空间的几何结构紧密相连。此时，我们引入**[张量密度](@entry_id:191194)**的概念，一个对象的变换法则包含因子 $(\det J)^W$，其中 $W$ 称为**权重**。[伪张量](@entry_id:193048)是权重为 $W=+1$ 或 $W=-1$ 的[张量密度](@entry_id:191194)（不同文献约定可能不同）。

在具有[度规张量](@entry_id:160222) $g_{\mu\nu}$ 的[黎曼流形](@entry_id:261160)上，两个重要的量是[张量密度](@entry_id:191194)：
1.  **Levi-Civita 符号 $\epsilon_{i_1 \dots i_n}$**：如前所述，这是一个权重为 $W=+1$ 的[协变张量](@entry_id:634493)密度。
2.  **度规[行列式](@entry_id:142978)的平方根 $\sqrt{g}$**：其中 $g = \det(g_{\mu\nu})$。[度规张量](@entry_id:160222) $g_{\mu\nu}$ 的变换法则是 $g'_{\alpha\beta} = \frac{\partial x^\mu}{\partial x'^\alpha} \frac{\partial x^\nu}{\partial x'^\beta} g_{\mu\nu}$。取[行列式](@entry_id:142978)可得 $g' = (\det(\frac{\partial x}{\partial x'}))^2 g = (\det J)^{-2} g$。因此，$\sqrt{g'} = |\det J|^{-1} \sqrt{g}$。对于保持定向的变换（$\det(J)>0$），我们有 $\sqrt{g'} = (\det J)^{-1} \sqrt{g}$。这表明 $\sqrt{g}$ 是一个权重为 $W=-1$ 的**[标量密度](@entry_id:161438)** [@problem_id:1532714]。

这两个发现引出了一个至关重要的结论。考虑对象 $\mathcal{E}_{i_1 \dots i_n} = \sqrt{g} \epsilon_{i_1 \dots i_n}$。它的变换权重是其各组成部分权重之和：$W_{\mathcal{E}} = W_{\sqrt{g}} + W_{\epsilon} = (-1) + (+1) = 0$。

这意味着 $\mathcal{E}_{i_1 \dots i_n}$ 是一个**真张量**！它被称为 **Levi-Civita 张量**。这一构造在广义相对论和微分几何中是基本操作，因为它允许我们以一种[协变](@entry_id:634097)的方式定义积分和[体积元](@entry_id:267802) ($d^n x \sqrt{g}$ 是一个不变的[体积元](@entry_id:267802))。

最后，即使在[广义坐标](@entry_id:156576)中，我们也可以从[伪张量](@entry_id:193048)构造出标量。然而，需要注意的是，一个[伪矢量](@entry_id:196296) $P^i$ 的“长度平方” $g_{ij} P^i P^j$ 通常不是一个真标量，而是一个权重为 $W=+2$ 的[标量密度](@entry_id:161438)。这是因为[伪矢量](@entry_id:196296) $P^i$ 变换时获得的 $\det(J)$ 因子在平方后变为 $(\det(J))^2$，该因子通常不为1。只有在限制于 $\det(J)=\pm 1$ 的变换（如[洛伦兹变换](@entry_id:176827)）时，这个量才表现为[不变量](@entry_id:148850) [@problem_id:1532764]。这再次凸显了[度规张量](@entry_id:160222)在“消除”伪[张量变换](@entry_id:183453)的特殊性、揭示其内在[几何不变量](@entry_id:178611)方面的核心作用。

总之，[伪张量](@entry_id:193048)是[张量分析](@entry_id:161423)框架的自然延伸。它们通过捕捉[坐标系](@entry_id:156346)的定向信息，为我们提供了描述和理解自然界中与手性、旋转和体积相关的各种现象所必需的数学语言。从基本粒子物理中的[对称性破缺](@entry_id:158994)到广义相对论中的[时空几何](@entry_id:139497)，[伪张量](@entry_id:193048)的原理和机制无处不在。