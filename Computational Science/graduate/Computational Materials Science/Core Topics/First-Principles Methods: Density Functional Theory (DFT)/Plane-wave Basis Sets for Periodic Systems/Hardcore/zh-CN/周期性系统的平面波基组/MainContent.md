## 引言
在现代[计算材料科学](@entry_id:145245)中，从第一性原理出发预测和理解[材料性质](@entry_id:146723)的能力至关重要。其核心挑战在于如何为具有无限周期性[晶格](@entry_id:196752)的固体求解薛定谔方程。选择一个既高效又精确的[基组](@entry_id:160309)来表示电子[波函数](@entry_id:147440)是解决此问题的关键。虽然局域[原子轨道](@entry_id:140819)[基组](@entry_id:160309)在[量子化学](@entry_id:140193)中取得了巨大成功，但它们在周期性体系中会引入[基组](@entry_id:160309)叠加误差等难题。[平面波基组](@entry_id:178287)，作为周期函数的自然展开基，为解决这一挑战提供了优雅而强大的框架。本文旨在全面解析[平面波基组](@entry_id:178287)方法，为研究生及研究人员提供坚实的理论和实践基础。

在接下来的内容中，我们将分三步深入探索：首先，在“原理与机制”一章中，我们将从[晶体对称性](@entry_id:198772)出发，推导[布洛赫定理](@entry_id:137461)，阐明[倒易空间](@entry_id:754151)的概念，并详细讨论[动能截断](@entry_id:186065)与赝势这两个使平面波方法在计算上切实可行的核心技术。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示如何运用该方法计算材料的力学、电学等宏观性质，如何通过超[晶胞](@entry_id:143489)方法处理缺陷与表面等复杂体系，并探讨如何从离域的计算结果中提取局域化的化学图像。最后，通过“动手实践”部分提供的一系列思考题，您将有机会将理论知识应用于解决具体的数值和概念问题，从而加深对该方法的掌握。

## 原理与机制

本章在前一章介绍的基础上，深入探讨在周期性体系的量子力学计算中，作为核心工具的[平面波基组](@entry_id:178287)所涉及的基本原理和关键机制。我们将从晶体周期性所蕴含的深刻对称性出发，推导出[波函数](@entry_id:147440)的基本形式，进而阐述如何构建和使用[平面波基组](@entry_id:178287)，并最终讨论如何从这一框架中精确地计算出材料的各种物理性质。

### 周期势中的[波函数](@entry_id:147440)：[布洛赫定理](@entry_id:137461)

晶体最显著的特征是其原子排布在空间中呈现的周期性。这种周期性由一个布拉维[晶格](@entry_id:196752)来描述，其格点由一组[基矢](@entry_id:199546) $\{\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3\}$ 生成，任意格矢可以表示为 $\mathbf{R} = n_1\mathbf{a}_1 + n_2\mathbf{a}_2 + n_3\mathbf{a}_3$，其中 $n_i$ 为整数。在单电子近似下，例如在[密度泛函理论](@entry_id:139027)的科恩-尚 (Kohn-Sham) 方程中，电子所感受到的[有效势](@entry_id:142581) $V(\mathbf{r})$ 也具有与[晶格](@entry_id:196752)相同的周期性，即 $V(\mathbf{r} + \mathbf{R}) = V(\mathbf{r})$。

这种周期性对体系的[哈密顿算符](@entry_id:144286) $\hat{H} = -\frac{\hbar^2}{2m}\nabla^2 + V(\mathbf{r})$ 有着深刻的影响。我们可以定义一个**[晶格](@entry_id:196752)[平移算符](@entry_id:756122)** $\hat{T}_{\mathbf{R}}$，其作用于任意函数 $\psi(\mathbf{r})$ 的效果是将其平移一个格矢 $\mathbf{R}$：$\hat{T}_{\mathbf{R}}\psi(\mathbf{r}) = \psi(\mathbf{r}+\mathbf{R})$。由于[哈密顿算符](@entry_id:144286)本身在[晶格](@entry_id:196752)平移下保持不变，它必然与所有[平移算符](@entry_id:756122)对易，即 $[\hat{H}, \hat{T}_{\mathbf{R}}] = 0$。此外，所有[平移算符](@entry_id:756122)自身也构成一个[阿贝尔群](@entry_id:150284)（[交换群](@entry_id:145145)），因为平移的次序无关紧要：$\hat{T}_{\mathbf{R}_1}\hat{T}_{\mathbf{R}_2} = \hat{T}_{\mathbf{R}_2}\hat{T}_{\mathbf{R}_1}$。

根据量子力学的基本原理，一组相互对易的算符拥有共同的本征函数。因此，[哈密顿算符](@entry_id:144286)的本征函数 $\psi(\mathbf{r})$ 也必然是所有[平移算符](@entry_id:756122) $\hat{T}_{\mathbf{R}}$ 的共同本征函数。这意味着：

$$ \hat{T}_{\mathbf{R}}\psi(\mathbf{r}) = \psi(\mathbf{r}+\mathbf{R}) = c(\mathbf{R})\psi(\mathbf{r}) $$

其中 $c(\mathbf{R})$ 是 $\hat{T}_{\mathbf{R}}$ 的[本征值](@entry_id:154894)。由于 $\hat{T}_{\mathbf{R}}$ 是幺正算符，其[本征值](@entry_id:154894)的模必须为1。利用平移的群性质 $c(\mathbf{R}_1+\mathbf{R}_2) = c(\mathbf{R}_1)c(\mathbf{R}_2)$，可以证明[本征值](@entry_id:154894)必须具有 $c(\mathbf{R}) = e^{i\mathbf{k}\cdot\mathbf{R}}$ 的形式，其中 $\mathbf{k}$ 是一个向量，被称为**[晶体动量](@entry_id:136369)**。这便引出了**布洛赫定理 (Bloch's Theorem)** 的第一种表述：在周期性势场中，[哈密顿算符](@entry_id:144286)的[本征函数](@entry_id:154705)在[晶格](@entry_id:196752)平移 $\mathbf{R}$ 下，仅仅是获得一个相位因子 $e^{i\mathbf{k}\cdot\mathbf{R}}$。

通过定义一个新函数 $u_{\mathbf{k}}(\mathbf{r}) = e^{-i\mathbf{k}\cdot\mathbf{r}}\psi_{\mathbf{k}}(\mathbf{r})$（此处我们用 $\mathbf{k}$ 标记对应的[本征函数](@entry_id:154705)），我们可以检验它的周期性：

$$ u_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) = e^{-i\mathbf{k}\cdot(\mathbf{r}+\mathbf{R})}\psi_{\mathbf{k}}(\mathbf{r}+\mathbf{R}) = e^{-i\mathbf{k}\cdot\mathbf{r}}e^{-i\mathbf{k}\cdot\mathbf{R}} (e^{i\mathbf{k}\cdot\mathbf{R}}\psi_{\mathbf{k}}(\mathbf{r})) = e^{-i\mathbf{k}\cdot\mathbf{r}}\psi_{\mathbf{k}}(\mathbf{r}) = u_{\mathbf{k}}(\mathbf{r}) $$

这表明函数 $u_{\mathbf{k}}(\mathbf{r})$ 具有与[晶格](@entry_id:196752)完全相同的周期性。由此，我们得到布洛赫定理的第二种、也是更常用的表述：[哈密顿算符](@entry_id:144286)的本征函数（称为**[布洛赫态](@entry_id:147552)**）可以写成一个平面波 $e^{i\mathbf{k}\cdot\mathbf{r}}$ 与一个具有[晶格](@entry_id:196752)周期性的函数 $u_{n\mathbf{k}}(\mathbf{r})$ 的乘积。

$$ \psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r}) $$

在这里，我们加入了能带指标 $n$，因为对于同一个晶体动量 $\mathbf{k}$，通常存在一系列离散的[能量本征值](@entry_id:144381)和对应的本征态。

区分[布洛赫态](@entry_id:147552)和自由电子的平面波态 $e^{i\mathbf{q}\cdot\mathbf{r}}$ 至关重要 。自由电子态是[动量算符](@entry_id:151743) $\hat{\mathbf{p}} = -i\hbar\nabla$ 的[本征态](@entry_id:149904)，具有确定的动量 $\hbar\mathbf{q}$；而[布洛赫态](@entry_id:147552)由于周期性部分 $u_{n\mathbf{k}}(\mathbf{r})$ 的存在，通常不是[动量算符](@entry_id:151743)的[本征态](@entry_id:149904)。因此，$\mathbf{k}$ 并非真实的动量，而是描述[波函数](@entry_id:147440)在[晶格](@entry_id:196752)平移下变换性质的[量子数](@entry_id:145558)。此外，自由电子态是连续平移对称性的本征态，而[布洛赫态](@entry_id:147552)仅仅是离散[晶格](@entry_id:196752)平移对称性的本征态。

### 倒易空间：周期体系的自然语言

布洛赫定理揭示，周期性函数 $u_{n\mathbf{k}}(\mathbf{r})$ 是理解晶体电子结构的关键。任何一个具有[晶格](@entry_id:196752)周期性的函数，都可以自然地展开成傅里叶级数。这个级数的[基函数](@entry_id:170178)是一组特殊的平面波 $e^{i\mathbf{G}\cdot\mathbf{r}}$，其[波矢](@entry_id:178620) $\mathbf{G}$ 必须满足一个条件：在任何[晶格](@entry_id:196752)平移 $\mathbf{R}$ 下，这个平面波的值都保持不变。

$$ e^{i\mathbf{G}\cdot(\mathbf{r}+\mathbf{R})} = e^{i\mathbf{G}\cdot\mathbf{r}} \implies e^{i\mathbf{G}\cdot\mathbf{R}} = 1 $$

这个条件等价于 $\mathbf{G}\cdot\mathbf{R}$ 是 $2\pi$ 的整数倍。所有满足这一条件的向量 $\mathbf{G}$ 构成的集合，自身也形成一个布拉维[晶格](@entry_id:196752)，被称为**倒易晶格 (reciprocal lattice)** 。

与实空间[晶格](@entry_id:196752)由[基矢](@entry_id:199546) $\{\mathbf{a}_i\}$ 定义类似，[倒易晶格](@entry_id:136718)也由一组[基矢](@entry_id:199546) $\{\mathbf{b}_j\}$ 定义。它们与实空间[基矢](@entry_id:199546)的关系通过以下正交归一条件确定：

$$ \mathbf{a}_i \cdot \mathbf{b}_j = 2\pi\delta_{ij} $$

其中 $\delta_{ij}$ 是克罗内克符号。任何倒易格矢 $\mathbf{G}$ 都可以表示为 $\mathbf{G} = m_1\mathbf{b}_1 + m_2\mathbf{b}_2 + m_3\mathbf{b}_3$，其中 $m_j$ 为整数。

现在，我们可以将[周期函数](@entry_id:139337) $u_{n\mathbf{k}}(\mathbf{r})$ 展开为[傅里叶级数](@entry_id:139455)：

$$ u_{n\mathbf{k}}(\mathbf{r}) = \sum_{\mathbf{G}} C_{n\mathbf{k}}(\mathbf{G}) e^{i\mathbf{G}\cdot\mathbf{r}} $$

代入[布洛赫态](@entry_id:147552)的表达式，我们得到了[布洛赫函数](@entry_id:189422)在[平面波基组](@entry_id:178287)下的自然展开：

$$ \psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} \sum_{\mathbf{G}} C_{n\mathbf{k}}(\mathbf{G}) e^{i\mathbf{G}\cdot\mathbf{r}} = \sum_{\mathbf{G}} C_{n\mathbf{k}}(\mathbf{G}) e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{r}} $$

这个表达式是[平面波](@entry_id:189798)方法的核心。它表明，任何一个晶体中的电子态，都可以被表示为一系列具有特定波矢 $\mathbf{k}+\mathbf{G}$ 的[平面波](@entry_id:189798)的线性叠加。这些[平面波](@entry_id:189798) $e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{r}}$ 构成了求解薛定谔方程的**[平面波基组](@entry_id:178287)** 。

值得注意的是，[晶体动量](@entry_id:136369) $\mathbf{k}$ 的定义存在冗余。如果我们用 $\mathbf{k}' = \mathbf{k} + \mathbf{G}_0$（其中 $\mathbf{G}_0$ 是任意一个倒易格矢）来标记同一个态，其平移性质 $e^{i\mathbf{k}'\cdot\mathbf{R}} = e^{i(\mathbf{k}+\mathbf{G}_0)\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}e^{i\mathbf{G}_0\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}$ 保持不变。这意味着 $\mathbf{k}$ 和 $\mathbf{k}+\mathbf{G}_0$ 描述的是同一个物理状态。因此，为了唯一地标记所有不等价的电子态，我们只需考虑一个倒易空间的[原胞](@entry_id:159354)内的 $\mathbf{k}$ 向量即可。这个特殊的原胞通常选择为[倒易晶格](@entry_id:136718)的维格纳-赛兹 (Wigner-Seitz) [原胞](@entry_id:159354)，即空间中离原点 $\mathbf{G}=\mathbf{0}$ 比离任何其他倒易格点更近的区域，这被称为**[第一布里渊区](@entry_id:269110) (first Brillouin zone)** 。

### 计算实现：截断与收敛性

理论上，将[布洛赫函数](@entry_id:189422)展开为[平面波](@entry_id:189798)级数需要无穷多个倒易格矢 $\mathbf{G}$，这在实际计算中是不可行的。因此，必须对[基组](@entry_id:160309)进行截断，只保留有限数量的平面波。

一个物理上和计算上都十分合理的截断方案是基于[平面波](@entry_id:189798)的动能。单个[平面波](@entry_id:189798) $e^{i\mathbf{q}\cdot\mathbf{r}}$ 的动能正比于 $|\mathbf{q}|^2$。因此，我们可以设定一个**[动能截断](@entry_id:186065)值** $E_{\text{cut}}$，只将那些动能小于该值的平面波包含在[基组](@entry_id:160309)中。对于一个给定的[布洛赫波矢](@entry_id:746866) $\mathbf{k}$，[基组](@entry_id:160309)由所有满足以下条件的[平面波](@entry_id:189798)构成 ：

$$ \frac{\hbar^2}{2m} |\mathbf{k}+\mathbf{G}|^2 \le E_{\text{cut}} $$

（在[原子单位](@entry_id:166762)制中，$\hbar=m=1$，条件简化为 $\frac{1}{2}|\mathbf{k}+\mathbf{G}|^2 \le E_{\text{cut}}$）。这个截断方案的物理意义在于，高动能的[平面波](@entry_id:189798)对应于[波函数](@entry_id:147440)中快速[振荡](@entry_id:267781)的短波长分量。如果[波函数](@entry_id:147440)本身是光滑的，这些高频分量的系数 $C_{n\mathbf{k}}(\mathbf{G})$ 会很小，可以被忽略。

[平面波基组](@entry_id:178287)的一个极其重要的特性是，它提供了一种系统性改善计算精度的方法。根据量子力学的**[变分原理](@entry_id:198028) (variational principle)**，对于一个给定的[哈密顿算符](@entry_id:144286)，在任何一个不完备的有限[基组](@entry_id:160309)中求解得到的[基态能量](@entry_id:263704)，都必然是真实基态能量的一个上界。当 $E_{\text{cut}}$ 增加时，[平面波基组](@entry_id:178287)的集合会不断扩大（一个较低[截断能](@entry_id:177594)的[基组](@entry_id:160309)是较高[截断能](@entry_id:177594)[基组](@entry_id:160309)的[子集](@entry_id:261956)）。这意味着，随着 $E_{\text{cut}}$ 的增加，我们为[波函数](@entry_id:147440)提供了更大的变分自由度，计算得到的总能量会单调地降低（或保持不变），并系统地收敛到[完备基组极限](@entry_id:200862)下的精确值  。这种可控的收敛性是平面波方法最强大的优点之一。

收敛的速度取决于被描述的[波函数](@entry_id:147440)的光滑程度。从[数值分析](@entry_id:142637)的角度看，如果一个赝化[波函数](@entry_id:147440)属于索伯列夫空间 $H^s(\Omega)$（$s$ 越大表示函数越光滑，其[傅里叶系数衰减](@entry_id:274275)越快），那么总能量的[离散化误差](@entry_id:748522) $\Delta E$ 会随着 $E_{\text{cut}}$ 呈代数衰减 ：

$$ \Delta E = \mathcal{O}(E_{\text{cut}}^{-(s-1)}) $$

这个关系明确地将[波函数](@entry_id:147440)的[光滑性](@entry_id:634843)（由 $s$ 表征）与计算收敛的效率联系起来。

### 芯态电子的挑战：赝势

尽管变分原理保证了收敛性，但对于真实的原子，直接使用[平面波基组](@entry_id:178287)会面临一个巨大的障碍。在[原子核](@entry_id:167902)附近，由于强大的库仑吸引，电子[波函数](@entry_id:147440)（尤其是芯态电子）会剧烈[振荡](@entry_id:267781)。此外，价电子[波函数](@entry_id:147440)为了与芯态电子[波函数](@entry_id:147440)保持正交，在[原子核](@entry_id:167902)区域也会表现出快速的[振荡](@entry_id:267781)。要精确描述这些剧烈[振荡](@entry_id:267781)的[波函数](@entry_id:147440)，需要包含具有极大波矢 $\mathbf{G}$ 的平面波，这对应着一个在计算上无法承受的极高的 $E_{\text{cut}}$。

解决方案是**赝势 (pseudopotential)** 近似。其核心思想是，固体材料的大部分物理和化学性质（如成键、[晶格常数](@entry_id:158935)、[声子谱](@entry_id:753408)等）主要由价电子决定，而深束缚的芯态电子则像“冻结”了一样，几乎不参与化学过程。因此，我们可以将[原子核](@entry_id:167902)和其周围的芯态电子一起视为一个离子实，用一个更平滑、更弱的有效势——即[赝势](@entry_id:170389)——来取代它们对价电子的复杂作用。这个赝势被精心设计，使得在[原子核](@entry_id:167902)区域外（通常定义一个核心半径 $r_c$），它对价电子产生的散射效应与原始的全电子势完全相同。而在核心区域内，[赝势](@entry_id:170389)取代了奇异的库仑势，其对应的赝[波函数](@entry_id:147440)也被构造成平滑、无节点的形态。

**模守恒[赝势](@entry_id:170389) (Norm-conserving pseudopotentials)** 是[赝势](@entry_id:170389)构建中的一个里程碑 。除了要求在核心半径 $r_c$ 之外赝[波函数](@entry_id:147440)与全电子[波函数](@entry_id:147440)完全匹配外，它还增加了一个关键条件：在核心区域内，赝[波函数](@entry_id:147440)的归一化积分（即[电荷](@entry_id:275494)）必须与全电子[波函数](@entry_id:147440)的完全相等。

$$ \int_{0}^{r_{c}} |u_{l}^{\text{ps}}(r)|^{2} r^2 dr = \int_{0}^{r_{c}} |u_{l}^{\text{AE}}(r)|^{2} r^2 dr $$

这个“模守恒”条件确保了赝势不仅能在参考能量上正确描述散射，其对能量的[一阶导数](@entry_id:749425)也是正确的，从而大大提高了赝势在不同化学环境中的**可移植性 (transferability)**。

赝势的光滑程度决定了计算所需的 $E_{\text{cut}}$。特征尺寸为 $r_c$ 的实空间结构需要[动能截断](@entry_id:186065)值 $E_{\text{cut}} \propto r_c^{-2}$。因此，一个具有较小核心半径 $r_c$ 的[赝势](@entry_id:170389)，通常被称为“**硬 (hard)**”赝势，因为它需要更高的 $E_{\text{cut}}$ 来收敛。反之，具有较大 $r_c$ 的赝势则被称为“**软 (soft)**”[赝势](@entry_id:170389)。元素的[周期性趋势](@entry_id:139783)也影响着赝势的硬度。例如，对于同样处理 $2s, 2p$ 壳层为价电子的氮和氧，由于氧有更大的核[电荷](@entry_id:275494)，其 $2s/2p$ [轨道](@entry_id:137151)被更紧地拉向[原子核](@entry_id:167902)，导致其波[函数[振](@entry_id:160838)荡](@entry_id:267781)更快。因此，为了获得同样质量的模守恒赝势，氧通常需要比氮更小的核心半径，从而成为一个更硬的赝势，要求更高的 $E_{\text{cut}}$ 。

[赝势](@entry_id:170389)算符具有非定域性，即它对不同角动量 $l$ 的[波函数](@entry_id:147440)分量作用不同。一个通用的非定域[赝势](@entry_id:170389)可以表示为**可分离的克莱曼-拜兰德 (Kleinman-Bylander, KB) 形式**，这极大地提高了计算效率 。KB[赝势](@entry_id:170389)算符分解为一个定域部分 $V_{\text{loc}}(\mathbf{r})$ 和一个非定域部分 $\hat{V}_{\text{NL}}$：

$$ \hat{V}^{\text{KB}} = V_{\text{loc}}(\mathbf{r}) + \sum_{lm} |\beta_{lm}\rangle D_{l} \langle\beta_{lm}| $$

其中，$V_{\text{loc}}(\mathbf{r})$ 是一个在[实空间](@entry_id:754128)中简单的[乘性](@entry_id:187940)势，而 $\hat{V}_{\text{NL}}$ 则是一系列[投影算符](@entry_id:154142)的和。在[平面波基组](@entry_id:178287)中，定域部分的[矩阵元](@entry_id:186505) $\langle \mathbf{k}+\mathbf{G} | V_{\text{loc}} | \mathbf{k}+\mathbf{G}' \rangle$ 只依赖于动量转移 $\mathbf{G}-\mathbf{G}'$，而非定域部分的矩阵元则可以高效地分解为[波函数](@entry_id:147440)与投影函数 $\beta_{lm}$ 的两次[内积](@entry_id:158127)。

为了进一步降低计算成本，**[超软赝势](@entry_id:144509) (ultrasoft pseudopotentials, USPP)** 和**投影缀加波 (projector augmented-wave, PAW)** 方法被发展出来。它们通过放松模守恒的限制，允许在核心区域内赝[波函数](@entry_id:147440)与真实电荷密度之间存在差值。这个差值通过额外的局域化增广[电荷](@entry_id:275494)来补偿。这样做的结果是赝[波函数](@entry_id:147440)可以被做得异常平滑，从而可以用非常低的 $E_{\text{cut}}$ 来描述。然而，这种方法的代价是形式上更为复杂，并且需要一个独立的、更高的[能量截断](@entry_id:177594)来描述高频的增广[电荷密度](@entry_id:144672) 。

### 从[基组](@entry_id:160309)到[物理可观测量](@entry_id:154692)

拥有了描述电子[波函数](@entry_id:147440)的[基组](@entry_id:160309)后，我们便可以着手计算各种物理性质。

#### 静电势：[泊松方程](@entry_id:143763)的求解

在[自洽场](@entry_id:136549)计算中，一个关键步骤是求解由总电荷密度 $\rho_{\text{tot}}(\mathbf{r})$（包括电子和离子）产生的静电（哈特里）势 $V_H(\mathbf{r})$。这通过求解[泊松方程](@entry_id:143763)来完成：

$$ \nabla^2 V_H(\mathbf{r}) = -4\pi \rho_{\text{tot}}(\mathbf{r}) $$

在倒易空间中，由于 $\nabla^2$ 作用于平面波 $e^{i\mathbf{G}\cdot\mathbf{r}}$ 仅仅是乘以 $-|\mathbf{G}|^2$，这个[偏微分方程](@entry_id:141332)变成了一个简单的[代数方程](@entry_id:272665)：

$$ -|\mathbf{G}|^2 V_H(\mathbf{G}) = -4\pi \rho_{\text{tot}}(\mathbf{G}) $$

对于所有非零的倒易格矢 $\mathbf{G} \neq \mathbf{0}$，解是显而易见的：

$$ V_H(\mathbf{G}) = \frac{4\pi}{|\mathbf{G}|^2} \rho_{\text{tot}}(\mathbf{G}) $$

然而，在 $\mathbf{G}=\mathbf{0}$ 处，这个表达式会遇到 $0/0$ 的不定问题或发散 。$\mathbf{G}=\mathbf{0}$ 分量对应体系的平均值。$\rho_{\text{tot}}(\mathbf{G}=\mathbf{0})$ 正比于原胞中的总净[电荷](@entry_id:275494) $Q_{\text{tot}}$。

*   **对于[电中性](@entry_id:157680)体系** ($Q_{\text{tot}}=0$)：此时 $\rho_{\text{tot}}(\mathbf{G}=\mathbf{0})=0$，[泊松方程](@entry_id:143763)在 $\mathbf{G}=\mathbf{0}$ 处变为 $0 \cdot V_H(\mathbf{0}) = 0$。这意味着 $V_H(\mathbf{0})$，即体系的平均静电势，是无法确定的。这对应于[静电势](@entry_id:188370)的[规范自由度](@entry_id:160491)（势可以任意加上一个常数）。在计算中，我们可以通过选择一个规范来固定这个值，通常简单地设为 $V_H(\mathbf{0})=0$。

*   **对于带电体系** ($Q_{\text{tot}}\neq 0$)：此时 $\rho_{\text{tot}}(\mathbf{G}=\mathbf{0})\neq 0$，方程变为 $0 = (\text{非零值})$，出现矛盾。这在数学上表明，对于一个带有净[电荷](@entry_id:275494)的周期性体系，不存在周期性的泊松方程解。物理上，一个无限的带电[晶格](@entry_id:196752)阵列会产生一个发散的势。为了处理这种情况，标准做法是引入一个均匀的、[电荷](@entry_id:275494)相反的**补偿[背景电荷](@entry_id:142591) (compensating background charge)**，人为地使整个计算单元恢复电中性。这样，问题就转化为了电中性体系的情况，但计算出的总能量需要进行修正，以扣除由于引入这个非物理[背景电荷](@entry_id:142591)而产生的虚假静电相互作用能。

#### 实空间网格与快速傅里叶变换

在计算中，经常需要在[实空间](@entry_id:754128)和[倒易空间](@entry_id:754151)之间来回切换。例如，电子密度是在[实空间](@entry_id:754128)网格上通过对所有占据[轨道](@entry_id:137151)的模平方求和得到的，而非定域[赝势](@entry_id:170389)的计算则在倒易空间中更有效。这种转换通过**快速傅里叶变换 (Fast Fourier Transform, FFT)** 来高效实现。

为此，我们需要在[实空间](@entry_id:754128)定义一个离散的网格。为了能够精确地表示[基组](@entry_id:160309)中所有的[平面波](@entry_id:189798)而不产生混淆（aliasing），这个网格的密度必须足够高，以满足**[奈奎斯特采样定理](@entry_id:268107) (Nyquist sampling theorem)** 。该定理要求，要无失真地表示一个最高频率为 $f_{\max}$ 的信号，[采样频率](@entry_id:264884)必须至少为 $2f_{\max}$。在我们的情况下，这意味着实空间网格的间距 $\Delta x$ 必须足够小，以分辨[平面波基组](@entry_id:178287)中波长最短（即 $|\mathbf{G}|$ 最大）的分量。具体而言，对于沿每个[晶格](@entry_id:196752)方向 $\mathbf{a}_i$ 的网格点数 $N_i$，必须满足 $|m_i| \le \lfloor N_i/2 \rfloor$，其中 $m_i$ 是[基组](@entry_id:160309)中包含的倒易格矢 $\mathbf{G} = \sum_i m_i \mathbf{b}_i$ 的整数系数。这等价于一个关于[实空间](@entry_id:754128)网格间距 $\Delta x_i = \|\mathbf{a}_i\|/N_i$ 和[基组](@entry_id:160309)中沿该方向最大投影分量 $G_{i, \max}$ 的条件：$\Delta x_i \le \pi / G_{i, \max}$。

#### 力与应力：[Hellmann-Feynman定理](@entry_id:173798)及其修正

原子间相互作用力和晶胞的应力分别是总能量对原子坐标和[晶格形变](@entry_id:183354)的一阶导数。根据**赫尔曼-费曼 (Hellmann-Feynman) 定理**，如果[波函数](@entry_id:147440)是[哈密顿算符](@entry_id:144286)的精确[本征函数](@entry_id:154705)（或者在变分法中，能量对于[波函数](@entry_id:147440)系数的导数为零），那么能量对某个参数的导数，就等于[哈密顿算符](@entry_id:144286)对该参数的导数的[期望值](@entry_id:153208) 。对于作用在原子 $I$ 上的力，这意味着：

$$ \mathbf{F}_I^{\text{HF}} = -\left\langle \psi \left| \frac{\partial \hat{H}}{\partial \mathbf{R}_I} \right| \psi \right\rangle $$

在[赝势](@entry_id:170389)框架下，这包括了离子-离子间的直接库仑排斥力，以及电子云与离子实（通过赝势描述）相互作用力的[期望值](@entry_id:153208)。

然而，[赫尔曼-费曼定理](@entry_id:173798)有一个前提：[基组](@entry_id:160309)本身不能依赖于求导的参数。在[平面波](@entry_id:189798)方法中，这引发了几个重要的、有时容易混淆的后果：

*   **[Pulay力](@entry_id:167194) (Pulay force)**：当[基组函数](@entry_id:200082)依赖于原子[坐标时](@entry_id:263720)，力的表达式中会出现一个额外的修正项，称为[Pulay力](@entry_id:167194)。在[平面波](@entry_id:189798)方法中，[基函数](@entry_id:170178) $e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{r}}$ 是由晶胞决定的，与原子在[晶胞](@entry_id:143489)内的具体位置**无关**。因此，在一个固定的计算[晶胞](@entry_id:143489)中，计算原子受力时，**不存在[Pulay力](@entry_id:167194)** 。这是平面波方法相对于原子中心[基组](@entry_id:160309)（如[高斯基组](@entry_id:198430)）的一个巨大优势。

*   **[Pulay应力](@entry_id:753858) (Pulay stress)**：然而，在计算[晶胞](@entry_id:143489)的应力（即能量对[晶格应变](@entry_id:159660)的导数）时，情况则不同。[晶格](@entry_id:196752)的应变会改变[实空间](@entry_id:754128)[基矢](@entry_id:199546) $\mathbf{a}_i$，从而也改变了[倒易空间](@entry_id:754151)[基矢](@entry_id:199546) $\mathbf{b}_j$ 和倒易格矢 $\mathbf{G}$。在一个固定的[动能截断](@entry_id:186065) $E_{\text{cut}}$ 下，满足截断条件的 $\mathbf{G}$ 向量集合会随着应变而改变。这意味着[基组](@entry_id:160309)**依赖于**应变。因此，在计算应力时，会存在一个源于[基组不完备性](@entry_id:193253)的**[Pulay应力](@entry_id:753858)**修正项，它只有在 $E_{\text{cut}} \to \infty$ 的[完备基组极限](@entry_id:200862)下才会消失 。

*   **[基组](@entry_id:160309)叠加误差 (Basis Set Superposition Error, BSSE)**：在描述两个或多个分子片段相互作用时，原子中心[基组](@entry_id:160309)会引入一种被称为BSSE的人为误差。这是因为一个片段可以“借用”另一个片段的[基函数](@entry_id:170178)来更好地描述自己的[波函数](@entry_id:147440)，从而人为地降低了体系的总能量。在[平面波](@entry_id:189798)方法中，[基组](@entry_id:160309)的质量在整个空间中是均匀的，并且完全由计算[晶胞](@entry_id:143489)和 $E_{\text{cut}}$ 决定，与其中是否有原子、有几个原子或原子在哪里无关。因此，平面波方法**从根本上消除了BSSE** 。

综上所述，[平面波基组](@entry_id:178287)不仅为求解周期体系中的薛定谔方程提供了一个系统、精确且高效的数学框架，其独特的性质还在计算力和能量等物理可观测量时，避免了一些在其他[基组](@entry_id:160309)方法中常见的复杂问题。