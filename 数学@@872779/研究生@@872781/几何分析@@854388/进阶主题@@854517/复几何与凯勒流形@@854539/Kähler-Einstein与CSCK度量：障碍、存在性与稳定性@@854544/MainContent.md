## 引言
在现代微分几何与代数几何的交汇处，一个核心且持久的追求是在给定的几何空间上寻找“最佳”或“典范”的度量。这些度量，如凯勒-爱因斯坦 (Kähler-Einstein, KE) 度量和[常标量曲率](@entry_id:186408)凯勒 (cscK) 度量，不仅因其内在的几何美感而备受推崇，更因其深刻地编码了[流形的拓扑](@entry_id:267834)和[代数结构](@entry_id:137052)而至关重要。然而，一个根本性的问题随之而来：这些理想的度量在何时存在？其存在性又受到何种条件的制约？

本文旨在系统性地解答这一核心问题，深入探讨KE和cscK度量的存在性理论、相关的障碍以及最终将微分几何与[代数几何](@entry_id:156300)完美统一的稳定性概念。我们将填补从度量的定义到其[存在性证明](@entry_id:267253)之间的知识鸿沟，揭示一个看似纯粹的分析问题如何转化为一个深刻的代数稳定性问题。

为实现这一目标，本文将分为三个部分。首先，在“原理与机制”一章中，我们将奠定理论基础，详细阐述KE和cscK度量的定义、基本性质，并介绍经典的松岛定理等存在性障碍，最终引出作为现代研究核心的[丘-田-唐纳森猜想](@entry_id:198774)和K-稳定性概念。接着，“应用与跨学科关联”一章将展示这些理论的强大生命力，我们将探讨连续法、Kähler-Ricci流等强大的分析工具如何被用于证明存在性，并揭示该理论与[辛几何](@entry_id:160783)、[变分原理](@entry_id:198028)乃至弦理论的紧密联系。最后，“动手实践”部分将通过具体的计算练习，帮助读者将抽象理论转化为可操作的技能，亲手构造[典范度量](@entry_id:266957)并检验其稳定性。通过这一系列的学习，读者将对这一连接[几何分析](@entry_id:157700)与代数几何的宏伟理论框架获得一个全面而深刻的理解。

## 原理与机制

在介绍性章节之后，我们现在深入探讨[常标量曲率](@entry_id:186408)凯勒 (cscK) 度量和凯勒-爱因斯坦 (KE) 度量的核心理论。本章将阐述这些[典范度量](@entry_id:266957)的基本性质、它们存在性所必须满足的拓扑和代数障碍，并最终引出将度量存在性与代数[几何稳定性](@entry_id:193596)联系起来的宏伟框架——丘-田-唐纳森 (Yau-Tian-Donaldson) 猜想。

### [凯勒几何](@entry_id:160314)中的[典范度量](@entry_id:266957)

在紧[凯勒流形](@entry_id:161192)上寻找“最佳”或“典范”度量的追求，是几何分析中的一个中心主题。[凯勒-爱因斯坦度量](@entry_id:270601)和[常标量曲率](@entry_id:186408)凯勒度量是这一追求中最重要的两个概念。

#### 凯勒-爱因斯坦条件

一个凯勒度量 $\omega$ 被称为**凯勒-爱因斯坦 (KE) 度量**，如果其里奇 (Ricci) 形式 $\mathrm{Ric}(\omega)$ 与度量形式本身成正比，即满足方程：
$$
\mathrm{Ric}(\omega) = \lambda \omega
$$
其中 $\lambda$ 是一个实常数，称为爱因斯坦常数。这个方程看似简单，却深刻地将[流形](@entry_id:153038)的曲率与度量本身联系起来，是一种强有力的几何约束。

一个基本的事实是，任何凯勒度量的[里奇形式](@entry_id:183612)在德拉姆 (de Rham) 上同调中都代表了该[流形](@entry_id:153038)[切丛](@entry_id:161294)的[第一陈类](@entry_id:201400) $c_1(X)$ 的 $2\pi$ 倍。具体来说，我们有[上同调](@entry_id:160558)关系：
$$
[\mathrm{Ric}(\omega)] = 2\pi c_1(X) \in H^2(X, \mathbb{R})
$$
由于 $\mathrm{Ric}(\omega)$ 是一个实 $(1,1)$-形式，其上同调类实际上位于 $H^{1,1}(X, \mathbb{R})$ 中。

如果 $\omega$ 是一个[凯勒-爱因斯坦度量](@entry_id:270601)，那么取其定义方程两边的上同调类，我们得到 $[\mathrm{Ric}(\omega)] = \lambda [\omega]$。结合上述陈-韦尔 (Chern-Weil) 理论的结果，我们立即获得一个深刻的拓扑约束：
$$
2\pi c_1(X) = \lambda [\omega]
$$
这里 $[\omega]$ 是一个凯勒类，它位于 $H^{1,1}(X, \mathbb{R})$ 的[凯勒锥](@entry_id:750987)内，这是一个由所有凯勒度量类组成的开[凸锥](@entry_id:635652)。凯勒类的关键性质是其“正性”。这个[上同调](@entry_id:160558)约束导致了关于爱因斯坦常数 $\lambda$ 符号的一个著名三分法 [@problem_id:3031571]：

1.  **$c_1(X) > 0$（法诺情形）**: 如果[第一陈类](@entry_id:201400) $c_1(X)$ 本身是一个凯勒类（即它可以由某个凯勒形式代表），我们称 $X$ 为法诺 (Fano) [流形](@entry_id:153038)。在这种情况下，由于 $[\omega]$ 和 $c_1(X)$ 都位于[凯勒锥](@entry_id:750987)内，为了使等式成立，常数 $\lambda$ 必须为正，即 $\lambda > 0$。此时，凯勒类 $[\omega]$ 必须与 $c_1(X)$ 成比例。

2.  **$c_1(X) = 0$（卡拉比-丘情形）**: 如果[第一陈类](@entry_id:201400)在实上同调中为零，即 $c_1(X) = 0 \in H^2(X, \mathbb{R})$，那么约束方程变为 $\lambda [\omega] = 0$。由于凯勒类 $[\omega]$ 非零（例如，其 $n$ 次幂的积分，即体积，为正），这必然要求 $\lambda=0$。因此，任何具有零[第一陈类](@entry_id:201400)的紧凯勒流形上的[凯勒-爱因斯坦度量](@entry_id:270601)必须是[里奇平坦](@entry_id:159097)的 ($\mathrm{Ric}(\omega)=0$)。著名的卡拉比-丘 (Calabi-Yau) 定理断言，在这种情况下，任何凯勒类中都存在一个唯一的[里奇平坦度量](@entry_id:159418)。

3.  **$c_1(X)  0$（一般型情形）**: 如果 $-c_1(X)$ 是一个凯勒类，我们称 $X$ 为一般型[流形](@entry_id:153038)。此时，约束方程 $2\pi c_1(X) = \lambda [\omega]$ 意味着一个负类（从 $-c_1(X)$ 的角度看）等于一个正类 $[\omega]$ 的 $\lambda$ 倍。这迫使 $\lambda$ 必须为负，即 $\lambda  0$。

此外，通过在凯勒-爱因斯坦方程两边与 $\omega^{n-1}$ 作楔积并积分，我们可以得到 $\lambda$ 的一个积分表达式 [@problem_id:3031571]：
$$
\lambda = \frac{2\pi \int_X c_1(X) \wedge \omega^{n-1}}{\int_X \omega^n}
$$
由于分母（体积）为正，$\lambda$ 的符号直接由积分 $\int_X c_1(X) \wedge \omega^{n-1}$ 的符号决定。这个积分的符号对于给定[流形](@entry_id:153038)上的所有凯勒类都是不变的，从而为上述三分法提供了计算上的依据。

#### 归一化与尺度变换性质

在研究凯勒-爱因斯坦方程时，理解度量尺度变换的影响至关重要。假设 $\omega$ 是一个凯勒形式，我们考虑一个新的凯勒形式 $\omega' = c\omega$，其中 $c$ 是一个正的实常数。与 $\omega$ 和 $\omega'$ 相关联的度量张量分别为 $g$ 和 $g'$，它们满足 $g' = cg$。

[里奇形式](@entry_id:183612)由[局部坐标](@entry_id:181200)中的公式 $\mathrm{Ric}(\omega) = -\sqrt{-1}\partial\bar{\partial}\log\det(g)$ 给出。对于尺度变换后的度量，我们有 $\det(g') = \det(c g) = c^n \det(g)$，其中 $n$ 是[流形](@entry_id:153038)的复维数。因此，
$$
\log\det(g') = \log(c^n \det(g)) = n\log(c) + \log\det(g)
$$
由于 $\partial\bar{\partial}$ 算子会消去常数 $n\log(c)$，我们得到一个非常重要的结论 [@problem_id:3031568]：
$$
\mathrm{Ric}(\omega') = \mathrm{Ric}(c\omega) = -\sqrt{-1}\partial\bar{\partial}(\log\det(g)) = \mathrm{Ric}(\omega)
$$
即**[里奇形式](@entry_id:183612)在常数尺度变换下是不变的**。

这个不变性对凯勒-爱因斯坦方程有直接影响。如果 $\omega$ 是一个 KE 度量，满足 $\mathrm{Ric}(\omega) = \lambda\omega$，那么新的度量 $\omega' = c\omega$ 满足：
$$
\mathrm{Ric}(\omega') = \mathrm{Ric}(\omega) = \lambda\omega = \lambda \left(\frac{1}{c}\omega'\right) = \left(\frac{\lambda}{c}\right) \omega'
$$
这意味着 $\omega'$ 也是一个[凯勒-爱因斯坦度量](@entry_id:270601)，但其爱因斯坦常数为 $\lambda' = \lambda/c$。

这一性质允许我们对爱因斯坦常数进行**归一化**。例如，在一个[法诺流形](@entry_id:190177)上，我们知道 $\lambda > 0$。如果我们找到了一个 KE 度量 $\omega$ 具有某个常数 $\lambda$，那么我们可以通过取新的度量 $\omega' = \lambda\omega$ 来得到一个爱因斯坦常数为 $1$ 的 KE 度量。然而，需要强调的是，这个过程改变了凯勒类，因为 $[\omega'] = [\lambda\omega] = \lambda[\omega]$。因此，当我们在一个*固定*的凯勒类中寻找度量时，我们没有尺度变换的自由，爱因斯坦常数 $\lambda$ 由该类唯一确定。而如果我们允许凯勒类变化，我们则可以归一化 $\lambda$ 的值 [@problem_id:3031568]。

#### [常标量曲率](@entry_id:186408) (cscK) 度量

凯勒-爱因斯坦条件是一个非常强的约束，它要求整个[里奇张量](@entry_id:159336)与度量成比例。一个更普遍、更灵活的[典范度量](@entry_id:266957)条件是**[常标量曲率](@entry_id:186408)凯勒 (cscK) 度量**。[标量曲率](@entry_id:157547) $S(\omega)$ 是一个通过收缩里奇张量得到的实值函数。在[凯勒几何](@entry_id:160314)中，它满足恒等式：
$$
S(\omega) \omega^n = n \mathrm{Ric}(\omega) \wedge \omega^{n-1}
$$
一个 cscK 度量就是其标量曲率函数 $S(\omega)$ 在[流形](@entry_id:153038)上为常数的凯勒度量。

从这个定义可以看出，任何[凯勒-爱因斯坦度量](@entry_id:270601)都是 cscK 度量。如果 $\mathrm{Ric}(\omega) = \lambda\omega$，那么代入上述恒等式得到 $S(\omega)\omega^n = n(\lambda\omega) \wedge \omega^{n-1} = n\lambda\omega^n$，这意味着 $S(\omega) = n\lambda$，显然是一个常数 [@problem_id:3031546]。

然而，反之不成立：一个 cscK 度量不一定是[凯勒-爱因斯坦度量](@entry_id:270601)。cscK 条件远比 KE 条件要弱。例如，在两个亏格大于1的紧[黎曼曲面](@entry_id:178613)的乘[积流形](@entry_id:270208)上，可以构造出无穷多个非凯勒-爱因斯坦的 cscK 度量 [@problem_id:3031546]。

如果一个凯勒类 $[\omega]$ 中存在一个 cscK 度量，它的标量曲率常数值是由拓扑决定的。这个常数必须等于该类的平均[标量曲率](@entry_id:157547) $\hat{S}$，其表达式为 [@problem_id:3031546]：
$$
\hat{S} = \frac{\int_X S(\omega) \omega^n}{\int_X \omega^n} = \frac{n \int_X \mathrm{Ric}(\omega) \wedge \omega^{n-1}}{\int_X \omega^n} = \frac{2\pi n (c_1(X) \cdot [\omega]^{n-1})}{[\omega]^n}
$$
这个公式表明，与 KE 问题不同，cscK 问题可以在*任何*凯勒类中提出：对于给定的凯勒类 $[\omega]$，是否存在一个代表元，其标量曲率等于由上式计算出的拓扑常数 $\hat{S}$？

### 解析方法：[蒙日-安培方程](@entry_id:268604)

寻找[典范度量](@entry_id:266957)的现代方法，尤其是卡拉比 (Calabi) 的纲领，是通过求解一个高度[非线性](@entry_id:637147)的[偏微分方程](@entry_id:141332)来实现的。其核心思想是在一个固定的凯勒类 $[\omega_0]$ 中寻找[典范度量](@entry_id:266957)。该类中的任何其他凯勒形式 $\omega$ 都可以写成 $\omega = \omega_0 + \sqrt{-1}\partial\bar{\partial}\varphi$ 的形式，其中 $\varphi$ 是一个光滑的实值函数，称为**[凯勒势](@entry_id:154750)**。这样，寻找一个度量的问题就转化为了寻找一个[势函数](@entry_id:176105) $\varphi$ 的问题。

我们来推导凯勒-爱因斯坦方程对应的势函数方程。利用[里奇形式](@entry_id:183612)的定义，可以推导出两个在同一凯勒类中的度量 $\omega_0$ 和 $\omega_\varphi$ 的[里奇形式](@entry_id:183612)之差为：
$$
\mathrm{Ric}(\omega_\varphi) - \mathrm{Ric}(\omega_0) = -\sqrt{-1}\partial\bar{\partial} \log\left(\frac{\omega_\varphi^n}{\omega_0^n}\right)
$$
假设我们正在寻找一个满足 $\mathrm{Ric}(\omega_\varphi) = \lambda \omega_\varphi$ 的度量。代入 $\omega_\varphi = \omega_0 + \sqrt{-1}\partial\bar{\partial}\varphi$，方程变为：
$$
\mathrm{Ric}(\omega_0) - \sqrt{-1}\partial\bar{\partial} \log\left(\frac{\omega_\varphi^n}{\omega_0^n}\right) = \lambda (\omega_0 + \sqrt{-1}\partial\bar{\partial}\varphi)
$$
背景度量 $\omega_0$ 本身一般不是[凯勒-爱因斯坦度量](@entry_id:270601)。它的“偏差”——形式 $\mathrm{Ric}(\omega_0) - \lambda\omega_0$——在紧[凯勒流形](@entry_id:161192)上是 $\sqrt{-1}\partial\bar{\partial}$-恰当的。因此，存在一个函数 $h_{\omega_0}$，称为**里奇势**，使得 [@problem_id:3031586]：
$$
\mathrm{Ric}(\omega_0) - \lambda\omega_0 = \sqrt{-1}\partial\bar{\partial} h_{\omega_0}
$$
这个[势函数](@entry_id:176105) $h_{\omega_0}$ 精确地衡量了背景度量 $\omega_0$ 离成为一个爱因斯坦常数为 $\lambda$ 的 KE 度量有多“远”。

将此代入方程并整理，我们得到：
$$
\sqrt{-1}\partial\bar{\partial} h_{\omega_0} - \sqrt{-1}\partial\bar{\partial} \log\left(\frac{\omega_\varphi^n}{\omega_0^n}\right) = \sqrt{-1}\partial\bar{\partial} (\lambda\varphi)
$$
这意味着函数 $\log(\omega_\varphi^n / \omega_0^n) + \lambda\varphi - h_{\omega_0}$ 的复黑塞矩阵为零，因此它在紧流形上必为常数 $C$。取指数后，我们得到一个关于 $\varphi$ 的**复[蒙日-安培方程](@entry_id:268604)**：
$$
(\omega_0 + \sqrt{-1}\partial\bar{\partial}\varphi)^n = e^{h_{\omega_0} - \lambda\varphi + C} \omega_0^n
$$
通过适当的归一化，常数 $C$ 可以被吸收或设为零。这个方程是求解凯勒-爱因斯坦问题的核心。里奇势 $h_{\omega_0}$ 在方程中扮演了非齐次项或“源”项的角色，它编码了背景度量的几何信息 [@problem_id:3031586]。

### 存在性的障碍

并非所有紧凯勒流形都容许[凯勒-爱因斯坦度量](@entry_id:270601)或 cscK 度量。在能够证明存在性之前，数学家们首先发现了一系列深刻的障碍。

#### 松岛-利希内罗维茨障碍

一个经典的障碍来自于对[自同构群](@entry_id:139672)的研究。**松岛 (Matsushima) 定理**指出，如果一个紧[凯勒流形](@entry_id:161192)容许[凯勒-爱因斯坦度量](@entry_id:270601)，那么其全纯[自同构群](@entry_id:139672) $\mathrm{Aut}(X)$ 必定是一个**约化 (reductive)** 的复[李群](@entry_id:137659)。

约化性是一个代数概念，粗略地说，它排除了像[上三角矩阵](@entry_id:150931)群那样的“坏”群。该定理的[逆否命题](@entry_id:265332)为：如果 $\mathrm{Aut}(X)$ 是非约化的，那么 $X$ 上不可能存在[凯勒-爱因斯坦度量](@entry_id:270601)。因此，非约化的[自同构群](@entry_id:139672)是 KE 度量存在的一个直接障碍 [@problem_id:3031543]。

对于[法诺流形](@entry_id:190177)（其中 $\lambda  0$），这个定理的证明思路尤为清晰。利用博赫纳 (Bochner) 技巧可以证明，在法诺-爱因斯坦[流形](@entry_id:153038)上，任何全纯向量场（即 $\mathrm{Aut}(X)$ 的[李代数](@entry_id:137954) $\mathfrak{aut}(X)$ 中的元素）的散度都必须为零。而卡拉比的一个结果表明，散度为零的全纯向量场恰好是那些其实部为基灵 (Killing) 向量场的向量场。[基灵向量场](@entry_id:161770)是度量 $\omega$ 的等距诱导的无穷小运动，它们构成了[等距群](@entry_id:161661)李代数 $\mathfrak{k}$。因此，我们得出结论 $\mathfrak{aut}(X) = \mathfrak{k}^{\mathbb{C}}$，即全纯向量场李代数是[基灵向量场](@entry_id:161770)[李代数](@entry_id:137954)的[复化](@entry_id:260775)。由于 $\mathfrak{k}$ 是一个[紧李群](@entry_id:146703)的李代数，它本身是约化的，其[复化](@entry_id:260775) $\mathfrak{k}^{\mathbb{C}}$ 也是约化的。这就证明了 $\mathfrak{aut}(X)$ 必须是约化的 [@problem_id:3031543]。

#### [几何不变量](@entry_id:178611)理论 (GIT) 的启示

更深层次的障碍，特别是对 cscK 度量和在任意凯勒类中的 KE 度量，其发现受到了与[代数几何](@entry_id:156300)中**[几何不变量](@entry_id:178611)理论 (GIT)** 的深刻类比的启发。这个由唐纳森 (Donaldson) 和藤木 (Fujiki) 发展的类比框架如下 [@problem_id:3031579]：

- 无穷维的[凯勒势](@entry_id:154750)空间 $\mathcal{H}$ ↔︎ 有限维的、有[群作用](@entry_id:268812)的凯勒流形 $M$。
- 哈密顿辛[同胚群](@entry_id:152166) $\mathcal{G}$ ↔︎ [紧李群](@entry_id:146703) $K$。
- [标量曲率](@entry_id:157547)映射 $\varphi \mapsto S(\omega_\varphi)$ ↔︎ 动量映射 $\mu$。
- cscK 度量（动量映射的零点） ↔︎ 动量映射为零的点。
- 马渕 (Mabuchi) K-[能量泛函](@entry_id:170311) ↔︎ Kempf-Ness 泛函。

在有限维 GIT 中，Kempf-Ness 定理指出，一个[轨道](@entry_id:137151)是**多稳定 (polystable)** 的当且仅当它包含一个动量映射为零的点。希尔伯特-芒福德 (Hilbert-Mumford) 判据则通过检查所有[单参数子群](@entry_id:181957)的“权”的符号来判断稳定性。这个类比强烈暗示，cscK 度量的存在性应该等价于某种代数几何意义下的“稳定性”，而其障碍应该可以通过研究[流形](@entry_id:153038)的某种“代数退化”来发现。

### 代数稳定性与[丘-田-唐纳森猜想](@entry_id:198774)

受 GIT 类比的启发，田刚和唐纳森各自独立地提出了一个纯代数的稳定性概念，现在称为 K-稳定性，它被猜想是 cscK 和 KE 度量存在的充要条件。

#### 测试构型：代数退化

为了在代数上研究[流形](@entry_id:153038)的“退化”，我们使用**测试构型 (test configuration)** 的概念。对于一个极化[流形](@entry_id:153038) $(X,L)$（其中 $L$ 是一个丰沛线丛），一个测试构型 $(\mathcal{X}, \mathcal{L})$ [实质](@entry_id:149406)上是一个以 $\mathbb{C}$ 为基底的平坦族，它带有一个相容的 $\mathbb{C}^*$-作用，使得在 $\mathbb{C}^* = \mathbb{C} \setminus \{0\}$ 上的纤维都同构于 $(X, L^{\otimes r})$（对于某个指数 $r$），而在原点 $t=0$ 处的中心纤维 $(\mathcal{X}_0, \mathcal{L}_0)$ 则是一个可能奇异的、带有 $\mathbb{C}^*$-作用的退化版本 [@problem_id:3031593]。每个测试构型都代表了将 $(X,L)$ 朝一个特定方向进行代数退化的一种方式。

#### K-稳定性：代数判据

与每个测试构型相关联，可以计算一个[数值不变量](@entry_id:752800)，称为**唐纳森-二木 (Donaldson-Futaki) [不变量](@entry_id:148850)** $\mathrm{DF}(\mathcal{X}, \mathcal{L})$。这个[不变量](@entry_id:148850)是通过分析 $\mathbb{C}^*$-作用在中心纤维[截面](@entry_id:154995)空间上的权重的渐进行为得到的，它正是希尔伯特-芒福德权的无穷维模拟 [@problem_id:3031579]。基于此，可以定义 K-稳定性的不同层次：

- **K-半稳定性 (K-semistability)**：如果对所有非平凡的测试构型，都有 $\mathrm{DF}(\mathcal{X}, \mathcal{L}) \ge 0$。
- **K-稳定性 (K-stability)**：如果对所有非平凡的测试构型，都有 $\mathrm{DF}(\mathcal{X}, \mathcal{L})  0$ [@problem_id:3031587]。
- **K-多稳定性 (K-polystability)**：如果 $(X,L)$ 是 K-半稳定的，并且 $\mathrm{DF}(\mathcal{X}, \mathcal{L}) = 0$ 当且仅当该测试构型是一个**乘积构型**（即由 $\mathrm{Aut}(X,L)$ 中的一个[单参数子群](@entry_id:181957)诱导的平凡退化）。

K-多稳定性是三者中概念最精妙也最重要的。如果[流形](@entry_id:153038)存在非平凡的[自同构](@entry_id:155390)，那么这些自同构会诱导 DF [不变量](@entry_id:148850)为零的测试构型。在这种情况下，[流形](@entry_id:153038)不可能是 K-稳定的。然而，这些“平凡”的零不影响度量的存在性，只是反映了度量解的不唯一性（相差一个[自同构](@entry_id:155390)）。K-多稳定性恰好允许这些由[自同构](@entry_id:155390)导致的零，同时排除了所有其他“坏”的退化。因此，它被认为是与 cscK 度量存在性等价的正确稳定性概念 [@problem_id:3031597]。

还有一个更强的概念是**一致 K-稳定性 (uniform K-stability)**，它要求 $\mathrm{DF}(\mathcal{X}, \mathcal{L})$ 不仅为正，而且能被测试构型的某个“范数”（如非阿基米德 $J$-泛函）从下方线性控制。这个更强的条件被证明与马渕 K-能量的强制性（coercivity）等价，从而在解析上保证了[典范度量](@entry_id:266957)的存在性 [@problem_id:3031597]。

#### [丘-田-唐纳森猜想](@entry_id:198774)与定理

所有这些概念最终汇集于**丘-田-唐纳森 (Yau-Tian-Donaldson, YTD) 猜想**。其一般形式断言：

 **YTD 猜想**：一个极化[流形](@entry_id:153038) $(X,L)$ 在凯勒类 $c_1(L)$ 中容许一个 cscK 度量，当且仅当 $(X,L)$ 是 K-多稳定的。

这个猜想的“存在性 $\implies$ 稳定性”部分现在已基本被证明，它构成了[典范度量](@entry_id:266957)存在性的代数[障碍理论](@entry_id:161880)。反方向，即“稳定性 $\implies$ 存在性”，是现代几何分析中最深刻和最活跃的研究领域之一。

对于一类特殊且重要的情形——[法诺流形](@entry_id:190177)，这个猜想已经被完全证明，成为一个定理，通常也称为 YTD 定理。

 **YTD 定理 (法诺情形)**：一个[法诺流形](@entry_id:190177) $X$ 容许一个[凯勒-爱因斯坦度量](@entry_id:270601)，当且仅当极化对 $(X, -K_X)$ 是 K-多稳定的 [@problem_id:3031561]。

这个定理是几何分析与代数几何几十年发展的结晶，它完美地实现了 GIT 类比所预言的深刻联系：一个微分几何中关于[偏微分方程解](@entry_id:166250)存在性的问题，被完全转化为一个[代数几何](@entry_id:156300)中关于稳定性的纯代数问题。