## 引言
在[量子场论](@entry_id:138177)的微扰计算中，处理由圈图积分产生的无穷大（即发散）是一个核心挑战。维度正则化作为一种极其强大和优雅的技术应运而生，它通过将时空维度从整数[解析延拓](@entry_id:147225)至复数平面，系统地“驯服”了这些发散。而这一强大框架的数学基石，正是欧拉伽马函数。伽马函数的独特[解析性](@entry_id:140716)质不仅使维度延拓成为可能，更将物理发散的复杂结构清晰地编码为其自身的极点。本文旨在深入剖析伽马函数在维度正则化中扮演的关键角色。

在接下来的内容中，我们将首先在“原理与机制”一章中，奠定数学基础，探索伽马函数如何从 $d$ 维积分中自然涌现，并成为处理发散的核心工具。随后，“应用与跨学科联系”一章将通过[量子电动力学](@entry_id:150740)、统计物理乃至弦论中的具体实例，展示这一理论框架在解决前沿物理问题时的巨大威力。最后，“动手实践”部分将提供一系列计算练习，帮助读者将理论知识转化为解决实际问题的能力，从而真正掌握这一现代[理论物理学](@entry_id:154070)家的必备技能。

## 原理与机制

在上一章中，我们介绍了维度正则化作为一种处理[量子场论](@entry_id:138177)中[紫外发散](@entry_id:183379)的强大技术。其核心思想是将时空维度 $d$ 从物理上的整数（如4）[解析延拓](@entry_id:147225)为复数。通过这种方式，原本发散的圈图积分被转化为一个关于 $d$ 的解析函数，其发散性表现为当 $d$ 取物理维度时出现的极点。实现这一过程的关键数学工具是欧拉伽马函数，记为 $\Gamma(z)$。本章将深入探讨伽马函数在维度正则化框架中的基本原理和关键机制。我们将看到，伽马函数不仅为 $d$ 维空间中的积分提供了必要的数学语言，还系统地揭示了发散的结构，并为重整化过程奠定了基础。

### 维度正则化的主积分

在微扰[量子场论](@entry_id:138177)中，经过[费曼参数化](@entry_id:201953)和动量移位等标准步骤后，大量的[圈图](@entry_id:149287)积分可以被归结为几种“主积分”形式。这些积分的求解构成了维度正则化计算的核心。伽马函数在这些主积分的解析表达式中扮演着中心角色。

#### d 维高斯积分与超球体体积

理解伽马函数作用的最自然起点是 $d$ 维欧几里得空间中的[高斯积分](@entry_id:187139)。考虑积分：
$$ I_d(\alpha) = \int_{\mathbb{R}^d} d^d\mathbf{x} \, \exp(-\alpha \mathbf{x}^2) $$
其中 $\mathbf{x}$ 是一个 $d$ 维向量，$\mathbf{x}^2 = \sum_{i=1}^d x_i^2$，$\alpha > 0$ 是一个正常量。

一方面，我们可以在笛卡尔坐标系下直接计算这个积分。由于积分可以分解为 $d$ 个独立的一维[高斯积分](@entry_id:187139)的乘积，我们得到：
$$ I_d(\alpha) = \left( \int_{-\infty}^{\infty} dx_i \, \exp(-\alpha x_i^2) \right)^d = \left( \sqrt{\frac{\pi}{\alpha}} \right)^d = \left(\frac{\pi}{\alpha}\right)^{d/2} $$

另一方面，我们可以转换到 $d$ 维超[球坐标系](@entry_id:167517)下计算。在这种[坐标系](@entry_id:156346)中，体积元写作 $d^d\mathbf{x} = r^{d-1} dr \, d\Omega_{d-1}$，其中 $r = |\mathbf{x}|$ 是[径向坐标](@entry_id:165186)，$d\Omega_{d-1}$ 是 $(d-1)$ 维单位超球面上的[立体角](@entry_id:154756)元。积分变为：
$$ I_d(\alpha) = \left( \int d\Omega_{d-1} \right) \int_0^\infty dr \, r^{d-1} \exp(-\alpha r^2) $$
角向部分的积分是 $(d-1)$ 维单位超球面的表面积，我们记为 $S_{d-1}$。[径向积分](@entry_id:202320)可以通过[变量替换](@entry_id:141386) $t = \alpha r^2$ (因此 $r = (\frac{t}{\alpha})^{1/2}$ 且 $dr = \frac{1}{2\alpha} (\frac{t}{\alpha})^{-1/2} dt$) 来求解：
$$ \int_0^\infty dr \, r^{d-1} \exp(-\alpha r^2) = \int_0^\infty dt \, \frac{1}{2\alpha^{1/2}} t^{-1/2} \left(\frac{t}{\alpha}\right)^{(d-1)/2} \exp(-t) = \frac{1}{2} \alpha^{-d/2} \int_0^\infty dt \, t^{d/2-1} \exp(-t) $$
根据[伽马函数的积分定义](@entry_id:165070) $\Gamma(z) = \int_0^\infty t^{z-1} e^{-t} dt$，我们发现[径向积分](@entry_id:202320)为 $\frac{1}{2} \alpha^{-d/2} \Gamma(d/2)$。

将两部分合在一起，我们得到：
$$ I_d(\alpha) = S_{d-1} \cdot \frac{1}{2} \alpha^{-d/2} \Gamma(d/2) $$
将这个结果与我们在笛卡尔坐标下得到的结果 $(\pi/\alpha)^{d/2}$ 等同起来，我们可以解出 $d$ 维超球面的表面积公式：
$$ S_{d-1} = \frac{2\pi^{d/2}}{\Gamma(d/2)} $$
这个推导清晰地表明，伽马函数是描述任意维度空间几何性质（如体积和表面积）的自然语言。它将维数 $d$ 从整数推广到复数，为维度正则化提供了坚实的几何基础。

#### 广义[高斯积分](@entry_id:187139)与伽马函数[递推关系](@entry_id:189264)

我们可以进一步推广[高斯积分](@entry_id:187139)，考虑形如 [@problem_id:764574] [@problem_id:764542] 的积分：
$$ I_{n}(d, \alpha) = \int d^d k \, (k^2)^n e^{-\alpha k^2} $$
其中 $n$ 是一个非负整数。使用超球坐标，并利用上述 $S_{d-1}$ 的表达式，该积分变为：
$$ I_{n}(d, \alpha) = S_{d-1} \int_0^\infty dr \, r^{d-1} (r^2)^n e^{-\alpha r^2} = \frac{2\pi^{d/2}}{\Gamma(d/2)} \int_0^\infty dr \, r^{d+2n-1} e^{-\alpha r^2} $$
[径向积分](@entry_id:202320)可以通过与之前类似的[变量替换](@entry_id:141386) $t = \alpha r^2$ 来计算，得到：
$$ \int_0^\infty dr \, r^{d+2n-1} e^{-\alpha r^2} = \frac{1}{2} \alpha^{-(d/2+n)} \Gamma(d/2+n) $$
将所有部分组合起来，我们得到该积分的通解：
$$ I_{n}(d, \alpha) = \frac{\pi^{d/2}}{\Gamma(d/2)} \alpha^{-(d/2+n)} \Gamma(d/2+n) = \left(\frac{\pi}{\alpha}\right)^{d/2} \frac{\Gamma(d/2+n)}{\Gamma(d/2)} \alpha^{-n} $$
这个结果揭示了伽马函数的一个至关重要的性质。我们可以通过对基本[高斯积分](@entry_id:187139) $I_0(d, \alpha) = (\pi/\alpha)^{d/2}$ 关于参数 $\alpha$ 求导来得到相同的结果：
$$ I_{n}(d, \alpha) = (-1)^n \frac{\partial^n}{\partial \alpha^n} I_0(d, \alpha) = (-1)^n \frac{\partial^n}{\partial \alpha^n} \left( \pi^{d/2} \alpha^{-d/2} \right) $$
计算这个导数得到：
$$ I_{n}(d, \alpha) = \pi^{d/2} \left(\frac{d}{2}\right)\left(\frac{d}{2}+1\right)\dots\left(\frac{d}{2}+n-1\right) \alpha^{-d/2-n} $$
通过比较这两种方法得到的结果 [@problem_id:764542]，我们可以推导出伽马函数的一个核心恒等式。令 $z=d/2$，我们得到：
$$ \frac{\Gamma(z+n)}{\Gamma(z)} = z(z+1)\dots(z+n-1) = \prod_{k=0}^{n-1}(z+k) $$
这个被称为递推关系或升[阶乘](@entry_id:266637)的表达式是伽马函数最重要的代数性质之一。它允许我们将 $\Gamma(z+n)$ 与 $\Gamma(z)$ 联系起来，这在展开含有伽马函数的表达式时至关重要。例如，通过这个关系，我们可以计算高斯权重下的动量矩，如 $\langle k^2 \rangle$ 和 $\langle (k^2)^2 \rangle$，进而求得其[方差](@entry_id:200758) [@problem_id:764574]。

#### 通用主积分公式

在实际的[圈图计算](@entry_id:751472)中，最常遇到的积分形式是 [@problem_id:764523]：
$$ I(a, b, d, \Delta) = \int \frac{d^d k}{(2\pi)^d} \frac{(k^2)^a}{(k^2 + \Delta)^b} $$
这里 $a, b$ 是实数参数，$\Delta > 0$ 通常与[粒子质量](@entry_id:156313)平方有关。这个积分可以通过与前面类似的方法求解。首先转换到超[球坐标](@entry_id:146054)：
$$ I(a, b, d, \Delta) = \frac{S_{d-1}}{(2\pi)^d} \int_0^\infty dk \, \frac{k^{d-1} (k^2)^a}{(k^2 + \Delta)^b} = \frac{2\pi^{d/2}}{(2\pi)^d \Gamma(d/2)} \int_0^\infty dk \, \frac{k^{2a+d-1}}{(k^2 + \Delta)^b} $$
为了求解[径向积分](@entry_id:202320)，我们进行[变量替换](@entry_id:141386) $t = k^2/\Delta$，即 $k = \sqrt{\Delta t}$。经过整理，积分变为：
$$ \int_0^\infty \frac{k^{2a+d-1}}{(k^2 + \Delta)^b} dk = \frac{1}{2} \Delta^{a+d/2-b} \int_0^\infty dt \, \frac{t^{a+d/2-1}}{(1+t)^b} $$
右侧的积分是[欧拉贝塔函数](@entry_id:178774) $B(x, y)$ 的一种积分表示：
$$ B(x, y) = \int_0^\infty \frac{t^{x-1}}{(1+t)^{x+y}} dt = \frac{\Gamma(x)\Gamma(y)}{\Gamma(x+y)} $$
通过比较指数，我们确定 $x = a+d/2$ 和 $y = b-a-d/2$。将所有部分组合并化简系数，我们最终得到这个通用主积分的表达式：
$$ I(a, b, d, \Delta) = \frac{1}{(4\pi)^{d/2}} \Delta^{a-b+d/2} \frac{\Gamma(a+d/2)\Gamma(b-a-d/2)}{\Gamma(b)\Gamma(d/2)} $$
这个公式是维度正则化中的基石。它将复杂的动量积分转化为了伽马函数的代数组合。几乎所有标量圈图积分最终都可以通过这个公式求解。

### [圈图计算](@entry_id:751472)中的实用技术

有了主积分公式，下一步就是学习如何将实际的[费曼积分](@entry_id:186814)转化为这种标准形式。伽马函数在这些转化技术中同样扮演着不可或缺的角色。

#### [费曼参数化](@entry_id:201953)

当一个圈图积分包含多个分母（[传播子](@entry_id:139558)）时，我们需要一种方法将它们合并。[费曼参数化](@entry_id:201953)就是为此而生。其通用形式为：
$$ \frac{1}{\prod_{i=1}^{N} A_i^{n_i}} = C(n_1, \dots, n_N) \int_{\Delta_N} d\mu(x) \frac{\prod_{i=1}^{N} x_i^{n_i-1}}{\left(\sum_{j=1}^{N} x_j A_j\right)^{\sum_{k=1}^{N} n_k}} $$
这里的关键在于系数 $C$ 的确定。这个系数可以通过引入每个分母的施温格参数（Schwinger parameter）表示来推导 [@problem_id:764416]：
$$ \frac{1}{A^n} = \frac{1}{\Gamma(n)} \int_0^\infty d\alpha \, \alpha^{n-1} e^{-\alpha A} $$
将乘积中的每一项都用此形式代替，然后通过巧妙的变量替换（将多个施温格参数 $\alpha_i$ 换为一个总[尺度参数](@entry_id:268705) $\lambda$ 和一组[费曼参数](@entry_id:195073) $x_i = \alpha_i / \lambda$），积分可以被重新组合。在这个过程中，对总[尺度参数](@entry_id:268705) $\lambda$ 的积分会再次产生一个伽马函数。最终，通过比较形式，可以确定系数 $C$ 完全由伽马函数构成：
$$ C(n_1, \dots, n_N) = \frac{\Gamma\left(\sum_{i=1}^N n_i\right)}{\prod_{i=1}^N \Gamma(n_i)} $$
这个结果再次展示了伽马函数如何作为一种“计数”工具，在组合不同项时保持正确的归一化。例如，对于包含四个不同幂次传播子的积分，其[费曼参数化](@entry_id:201953)系数可以直接用此公式计算 [@problem_id:764416]。

#### [张量积](@entry_id:140694)分的约化

许多[费曼积分](@entry_id:186814)在分子中包含圈动量，形成张量结构，例如：
$$ T_{\mu\nu\rho\sigma} = \int \frac{d^d k}{(2\pi)^d} \frac{k_\mu k_\nu k_\rho k_\sigma}{(k^2 + m^2)^3} $$
由于积分测度 $d^d k$ 是旋转不变的，积分的结果必须是一个由度规张量 $\delta_{\mu\nu}$ 构成的、具有相同对称性的张量。对于上述[四阶张量](@entry_id:181350)积分，其一般形式必定为 [@problem_id:764439]：
$$ T_{\mu\nu\rho\sigma} = C (\delta_{\mu\nu}\delta_{\rho\sigma} + \delta_{\mu\rho}\delta_{\nu\sigma} + \delta_{\mu\sigma}\delta_{\nu\rho}) $$
我们的任务是确定标量系数 $C$。这可以通过对张量指标进行缩并来完成。例如，用 $\delta^{\mu\nu}$ 缩并上式，等式的一边会得到一个与维度 $d$ 和系数 $C$ 相关的项，另一边则是一个新的、阶数更低的动量积分。通过反复使用这种缩并技巧，并结合诸如 $k^2 = (k^2+m^2)-m^2$ 的代数恒等式，最终可以将系数 $C$ 表示为一系列标量主积分的组合。这些[标量积](@entry_id:138996)分可以用我们之前导出的主积分公式来计算，其结果自然包含伽马函数。这个过程虽然繁琐，但非常系统，它展示了如何将复杂的[张量积](@entry_id:140694)分一步步约化为我们已经掌握的[标准形式](@entry_id:153058)。

### 发散作为[伽马函数的极点](@entry_id:188704)

维度正则化的真正威力在于它处理发散的方式。在 $d$ 维空间中计算完毕后，紫外（UV）发散被编码为伽马函数在特定维度值下的极点。

#### 极点的显现与劳伦级数展开

让我们以最简单的一圈“蝌蚪图”积分为例 [@problem_id:764564]。在欧几里得空间中，其形式为：
$$ I_E(d, m^2) = \int \frac{d^d k}{(2\pi)^d} \frac{1}{k^2 + m^2} $$
这符合我们的主积分公式 $I(a, b, d, \Delta)$，其中 $a=0$, $b=1$, $\Delta=m^2$。代入公式得到：
$$ I_E(d, m^2) = \frac{1}{(4\pi)^{d/2}} (m^2)^{d/2-1} \frac{\Gamma(d/2)\Gamma(1-d/2)}{\Gamma(1)\Gamma(d/2)} = \frac{(m^2)^{d/2-1}}{(4\pi)^{d/2}} \Gamma(1-d/2) $$
我们感兴趣的是物理维度 $d=4$ 附近的行为。为此，我们设置 $d=4-2\epsilon$，其中 $\epsilon$ 是一个小的复数参数，物理极限对应于 $\epsilon \to 0$。代入上式，伽马函数的宗量变为 $1-d/2 = 1-(2-\epsilon) = -1+\epsilon$。因此，积分表达式为：
$$ I_E(4-2\epsilon, m^2) \approx \frac{(m^2)^{1-\epsilon}}{(4\pi)^{2-\epsilon}} \Gamma(-1+\epsilon) $$
我们知道伽马函数 $\Gamma(z)$ 在所有非正整数 $z=0, -1, -2, \dots$ 处都有简单极点。在 $z=-1$ 附近，它有如下的劳伦[级数展开](@entry_id:142878)：
$$ \Gamma(-1+\epsilon) = -\frac{1}{\epsilon} - \gamma + \mathcal{O}(\epsilon) $$
其中 $\gamma \approx 0.577$ 是[欧拉-马歇罗尼常数](@entry_id:146205)。同时，将表达式中的其他项对 $\epsilon$ 做[泰勒展开](@entry_id:145057)：
$$ (m^2)^{1-\epsilon} = m^2 \exp(-\epsilon \ln m^2) = m^2(1 - \epsilon \ln m^2 + \dots) $$
$$ (4\pi)^{-(2-\epsilon)} = \frac{1}{16\pi^2} \exp(\epsilon \ln(4\pi)) = \frac{1}{16\pi^2}(1 + \epsilon \ln(4\pi) + \dots) $$
将这些展开式相乘，我们就能得到积分在 $\epsilon \to 0$ 时的行为：
$$ I_E(4-2\epsilon, m^2) = \frac{m^2}{16\pi^2} \left(-\frac{1}{\epsilon} - \gamma + \ln(4\pi) - \ln m^2 + \mathcal{O}(\epsilon)\right) $$
这个结果清楚地展示了维度正则化的核心机制：原始积分在 $d=4$ 时的[紫外发散](@entry_id:183379)，现在被转化为一个显式的 $1/\epsilon$ 极点。所有发散的部分都被清晰地分离出来。

#### [重整化方案](@entry_id:154662)：MS 与 $\overline{\text{MS}}$

上述展开式也揭示了不同[重整化方案](@entry_id:154662)的本质。为了得到有限的物理预测，我们必须引入“反常项”来抵消发散。
*   在**最小减除（MS）**方案中，我们只减去纯粹的 $1/\epsilon$ 极点项。
*   在更常用的**修正最小减除（$\overline{\text{MS}}$）**方案中，我们减去 $1/\epsilon$ 极点以及总是与之相伴的特定常数组合，即 $\ln(4\pi) - \gamma$。

这种选择的根源在于，在许多一圈计算中，都会出现形如 $(4\pi)^{\epsilon} \Gamma(\epsilon)$ 或类似的因子 [@problem_id:764441]。例如，对于 $d=4-2\epsilon$ 时的无质量[传播子](@entry_id:139558)[圈图](@entry_id:149287)，其发散结构由 $\Gamma(\epsilon/2)$ 给出。组合因子 $(4\pi)^{\epsilon/2}\Gamma(\epsilon/2)$ 的展开为：
$$ (4\pi)^{\epsilon/2} \Gamma(\epsilon/2) = \left(1 + \frac{\epsilon}{2}\ln(4\pi) + \dots \right) \left( \frac{2}{\epsilon} - \gamma + \dots \right) = \frac{2}{\epsilon} + (\ln(4\pi) - \gamma) + \mathcal{O}(\epsilon) $$
$\overline{\text{MS}}$ 方案的思想就是将这个“通用”的有限部分 $(\ln(4\pi) - \gamma)$ 连同极点一起吸收掉，使得重整化后的参数定义更加简洁。

#### 发散维度的判定

[伽马函数的极点](@entry_id:188704)结构为我们提供了一个强大的预测工具。一个圈图积分是否在某个整数维度 $d$ 上发散，取决于其最终表达式中的伽马函数宗量是否在该维度下等于一个非正整数。
例如，对于一个无质量标量场的[顶点修正](@entry_id:146982)积分 [@problem_id:764454]，经过计算其结果正比于 $\Gamma(2-d/2)$。为了判断该积分在哪些整数维度 $d \ge 2$ 上是[紫外发散](@entry_id:183379)的，我们只需找到使宗量为非正整数的 $d$ 值：
$$ 2 - \frac{d}{2} = n, \quad n \in \{0, -1, -2, \dots\} $$
解此方程得 $d = 4 - 2n$。对于所有非正整数 $n$，我们得到一系列偶数维度 $d=4, 6, 8, \dots$。因此，这个积分在所有大于等于4的偶数维度上都是[紫外发散](@entry_id:183379)的。
此外，通过简单的[幂次计数](@entry_id:158814)（power counting）也可以快速判断一个[积分的收敛](@entry_id:187300)性，并确定首次出现发散的维度 [@problem_id:764464]。维度正则化的结果与[幂次计数](@entry_id:158814)的结果是完全一致的。

#### 一个特殊规则：[无标度积分](@entry_id:184725)

维度正则化框架中有一个非常重要的规则：任何没有内在质量或动量标度的积分为零。一个典型的例子是 [@problem_id:764541]：
$$ I(d, \alpha) = \int d^d k \, (k^2)^{\alpha} $$
这个积分既没有质量项 $m^2$ 也没有外部动量 $\Delta$。直接计算它会在 $k \to 0$（红外）和 $k \to \infty$（紫外）两端都发散。严格定义它的方法是引入一个正则化标度 $m$，计算一个有标度的积分，然后取 $m \to 0$ 的极限。例如，我们可以计算：
$$ I_m(d, \alpha) = \pi^{d/2} (m^2)^{d/2 + \alpha} \frac{\Gamma(-\alpha-d/2)}{\Gamma(-\alpha)} $$
在 $\text{Re}(\alpha+d/2) > 0$ 的区域，当 $m \to 0$ 时，这个表达式趋于零。根据[解析延拓原理](@entry_id:187941)，一个在某个区域内为零的解析函数，在其整个解析定义域内都恒为零。因此，在维度正则化的框架下，我们严格定义所有[无标度积分](@entry_id:184725)为零。这个规则极大地简化了许多计算。

### 伽马函数恒等式的应用

在计算的最后阶段，我们常常会得到包含复杂伽马函数乘积与比值的表达式。利用伽马函数的各种恒等式来化简这些表达式，是获得最终简洁物理结果的关键一步。
两个最重要的恒等式是：
1.  **[欧拉反射公式](@entry_id:139367)**: $\Gamma(z)\,\Gamma(1-z) = \frac{\pi}{\sin(\pi z)}$
2.  **勒让德[加倍公式](@entry_id:173961)**: $\Gamma(z)\,\Gamma(z+1/2) = 2^{1-2z}\sqrt{\pi}\,\Gamma(2z)$

考虑一个源自[圈图计算](@entry_id:751472)的典型因子 [@problem_id:764604]：
$$ \mathcal{C}(\epsilon) = \frac{\Gamma(1+2\epsilon)\,\Gamma(1-2\epsilon)}{\Gamma(1+\epsilon)\,\Gamma(1-\epsilon)} $$
我们可以利用[反射公式](@entry_id:198841)和[递推关系](@entry_id:189264) $\Gamma(1+z) = z\Gamma(z)$ 来简化它。
分子为：
$$ \Gamma(1+2\epsilon)\,\Gamma(1-2\epsilon) = (2\epsilon)\Gamma(2\epsilon)\,\Gamma(1-2\epsilon) = 2\epsilon \cdot \frac{\pi}{\sin(2\pi\epsilon)} $$
分母为：
$$ \Gamma(1+\epsilon)\,\Gamma(1-\epsilon) = \epsilon\Gamma(\epsilon)\,\Gamma(1-\epsilon) = \epsilon \cdot \frac{\pi}{\sin(\pi\epsilon)} $$
两者相除，并利用[三角函数](@entry_id:178918)[倍角公式](@entry_id:173961) $\sin(2x) = 2\sin(x)\cos(x)$，我们得到一个极为简洁的结果：
$$ \mathcal{C}(\epsilon) = \frac{2\sin(\pi\epsilon)}{\sin(2\pi\epsilon)} = \frac{2\sin(\pi\epsilon)}{2\sin(\pi\epsilon)\cos(\pi\epsilon)} = \frac{1}{\cos(\pi\epsilon)} = \sec(\pi\epsilon) $$
这个例子展示了如何通过伽马函数的恒等式，将复杂的特殊函数表达式转化为我们熟悉的[初等函数](@entry_id:181530)，从而揭示出物理结果的简单结构。

总而言之，伽马函数是维度[正则化方法](@entry_id:150559)的核心。它不仅为在任意维度下进行积分提供了数学框架，还将发散的[奇异结构](@entry_id:260616)系统地编码为其自身的极点。通过研究伽马函数的性质，我们能够精确地计算[圈图](@entry_id:149287)积分、理解不同[重整化方案](@entry_id:154662)之间的关系，并最终提取出有意义的物理预测。