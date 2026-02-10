## 引言
科学和工程领域的许多最重要问题——从寻找最优设计参数到预测系统的[临界点](@keyword=critical_points|lang=zh-CN|style=Feynman)——最终都可归结为求解形如 $f(x)=0$ 的方程。虽然简单的方程可以用代数方法求解，但大多数现实世界的问题所产生的函数都过于复杂，无法手动求解。[数值求根](@keyword=numerical_root_finding_2|lang=zh-CN|style=Feynman)方法弥合了我们待解问题与分析数学局限之间的鸿沟，这是一套强大而精妙的[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)，旨在以惊人的精度搜寻解答。

本文将带领读者进入这些关键计算工具的世界。本文将分为两章，探索驱动这些方法的核心思想，以及它们帮助我们解决的广阔问题领域。
在第一章 **“原理与机制”** 中，我们将深入探讨这些[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)背后的基本理念。我们将对比像[二分法](@keyword=bisection_method|lang=zh-CN|style=Feynman)这类[区间法](@keyword=bracketing_methods|lang=zh-CN|style=Feynman)的谨慎确定性与像著名的[牛顿法](@keyword=newton_method|lang=zh-CN|style=Feynman)这类开放法的迅猛速度，考察它们的[收敛率](@keyword=rates_of_convergence|lang=zh-CN|style=Feynman)，揭示其潜在的失效点，并探索集两者之长的先进技术。
随后，在 **“应用与跨学科联系”** 中，我们将见证这些抽象[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)如何应用于实践。我们将看到[求根](@keyword=root_finding_2|lang=zh-CN|style=Feynman)法如何在工程设计、物理系统仿真、[生态稳定性](@keyword=ecological_stability|lang=zh-CN|style=Feynman)分析，乃至[量子化学](@keyword=quantum_chemistry|lang=zh-CN|style=Feynman)中的[分子性](@keyword=molecularity|lang=zh-CN|style=Feynman)质计算中扮演着无名英雄的角色。通过探索这些方法的适用范围及其失效之处，我们将更深刻地理解它们的力量以及所解决问题背后的底层结构。我们的旅程始于探索驱动这些方法的基本思想，对比确定性与速度这两种理念。

## 原理与机制

想象一下，你正在浓雾中徒步，试图找到一个特定的海拔高度——比如说，海平面。你的[高度计](@keyword=altimeter|lang=zh-CN|style=Feynman)能告诉你当前的高度。求“根”的问题恰好就是如此：找到一个精确的位置 $x$，使得函数 $f(x)$ 等于零。你会怎么做呢？我们为此发明的各种方法不仅仅是公式的集合，它们是不同理念的体现，讲述了一个关于谨慎、智慧与微积分强大力量之间相互作用的精彩故事。

### [区间法](@keyword=bracketing_methods|lang=zh-CN|style=Feynman)的确定性

最基本，或许也最让人安心的想法是首先**框定**根。假设在 $a$ 点你处于海平面以上（$f(a) > 0$），而在 $b$ 点你处于海平面以下（$f(b)  0$）。如果你的路径是连续的（你没有瞬移），那么你一定在 $a$ 和 $b$ 之间的某处穿过了海平面。这就是著名的**[介值定理](@keyword=intermediate_value_theorem|lang=zh-CN|style=Feynman)**，它是所有[区间法](@keyword=bracketing_methods|lang=zh-CN|style=Feynman)的核心。

利用这一事实的最简单方法是**[二分法](@keyword=bisection_method|lang=zh-CN|style=Feynman)**。它美妙地“愚笨”。你检查中点 $c = \frac{a+b}{2}$ 的海拔。如果你仍高于海平面，你就知道根一定在你路径的后半段，即 $c$ 和 $b$ 之间。如果你低于海平面，根就在前半段，即 $a$ 和 $c$ 之间。你舍弃另一半并重复此过程。你必然能将包含根的区间越缩越小，就像一个侦探在稳步缩小搜查范围。这个过程很慢，但结果必然。

但我们能更聪明些吗？与其只看 $f(a)$ 和 $f(b)$ 的*符号*，我们何不看看它们的*值*？假设 $f(a)$ 是 100 米，而 $f(b)$ 是 -1 米。根似乎更有可能离 $b$ 更近，而不是 $a$。**[试位法](@keyword=method_of_false_position|lang=zh-CN|style=Feynman)**（Regula Falsi，或称“伪位置法”）正是基于这种直觉。它暂时假设函数是一条直线——一条连接点 $(a, f(a))$ 和 $(b, f(b))$ 的**割线**。然后，它计算这条想象中的直[线与](@keyword=wired_and|lang=zh-CN|style=Feynman) x 轴的交点。这个新点 $c$ 就成了它对根的猜测 [@problem_id:2157487]。

因此，我们有了两种方法的故事。二分法是谨慎的，只依赖于符号改变的保证。[试位法](@keyword=method_of_false_position|lang=zh-CN|style=Feynman)则更为乐观，它基于函数的线性近似做出有根据的猜测。它将[二分法](@keyword=bisection_method|lang=zh-CN|style=Feynman)区间的安全性与[割线法](@keyword=secant_method|lang=zh-CN|style=Feynman)更智能的步进相结合，使其成为两种理念的绝佳混合体 [@problem_id:2217526]。

### 当机智失灵时

你可能会认为，凭借其“更聪明”的猜测，[试位法](@keyword=method_of_false_position|lang=zh-CN|style=Feynman)总是优于步履蹒跚的[二分法](@keyword=bisection_method|lang=zh-CN|style=Feynman)。然而，大自然总有办法让我们简单的假设显得渺小。

想象一下，我们的函数不是一条直线，而是有明显的曲线——例如，如果它是**[凸函数](@keyword=convex_functions|lang=zh-CN|style=Feynman)**（向上弯曲，像一个碗）。假设我们正在计算一项投资的**[内部收益率 (IRR)](@keyword=internal_rate_of_return_(irr)|lang=zh-CN|style=Feynman)**，这通常涉及为凸函数求解一个[求根问题](@keyword=root_finding_problem|lang=zh-CN|style=Feynman) [@problem_id:2443625]。我们连接点 $(a, f(a))$ 和 $(b, f(b))$ 的割线将总是位于函数真实曲线的*上方*。因此，它的 x 轴截距（我们的猜测）将始终落在真实根的一侧。

这对[试位法](@keyword=method_of_false_position|lang=zh-CN|style=Feynman)意味着什么？假设我们的新猜测点 $c$ 的函数值 $f(c)$ 与 $f(b)$ 的符号相同。该方法随后用 $c$ 替换 $b$，形成一个新的区间 $[a, c]$。但由于[凸性](@keyword=convexity|lang=zh-CN|style=Feynman)，*下一次*猜测仍将落在根的同一侧，我们又会替换掉同一个端点。结果呢？我们最初的一个端点，比如 $a$，变得“固定”了。我们不断更新另一个端点，但区间的收缩速度却慢得令人痛苦。这个本应聪明的办法突然以蜗牛般的速度收敛，有时甚至比[二分法](@keyword=bisection_method|lang=zh-CN|style=Feynman)还要慢。这是数值科学中一个至关重要的教训：每种[算法](@keyword=algorithm|lang=zh-CN|style=Feynman)都有其隐含的假设，其性能取决于现实世界在多大程度上符合该假设。

### 追求速度：开放法

“卡住”的[试位法](@keyword=method_of_false_position|lang=zh-CN|style=Feynman)的迟缓促使我们产生一个激进的想法：如果我们放弃区间的安全性会怎样？这就引出了**开放法**。

**[割线法](@keyword=secant_method|lang=zh-CN|style=Feynman)**是解除了束缚的[试位法](@keyword=method_of_false_position|lang=zh-CN|style=Feynman)。它使用穿过*最近两个点*的[割线](@keyword=secant_line|lang=zh-CN|style=Feynman)来计算下一个点，而不管这两个点是否框定了根。通过摆脱区间约束，它通常能更快地收敛。但这种自由是有代价的：没有了区间的安全保障，迭代可能会失控并完全发散。

现在，让我们把利用局部信息的想法推向逻辑的极致。割线法使用两个点来近似函数的斜率。但如果我们懂微积分，我们有一个工具可以找到*一个点*的*精确*斜率：[导数](@keyword=derivative|lang=zh-CN|style=Feynman)。这就是**牛顿法**的精妙之处。

从一个猜测值 $x_n$ 出发，我们站在曲线上的点 $(x_n, f(x_n))$，并画出该点的**切线**。切线是该点处函数最佳的[线性近似](@keyword=tangent_line_approximation|lang=zh-CN|style=Feynman)。然后我们问：这条切线与 x 轴交于何处？我们沿着切线“滑下”，找到我们的下一个、也希望能好得多的猜测值 $x_{n+1}$。这个公式本身就是优雅的化身：
$$
x_{n+1} = x_{n} - \frac{f(x_{n})}{f'(x_{n})}
$$
当牛顿法有效时，其速度是惊人的。二分法的误差每次缩小一个常数因子（$\frac{1}{2}$）（[线性收敛](@keyword=linear_convergence|lang=zh-CN|style=Feynman)），[割线法](@keyword=secant_method|lang=zh-CN|style=Feynman)的误差每次缩小约 $1.618$ 次方（[超线性收敛](@keyword=superlinear_convergence|lang=zh-CN|style=Feynman)），而[牛顿法](@keyword=newton_method|lang=zh-CN|style=Feynman)的误差则以 $2$ 次方缩小。这就是**[二次收敛](@keyword=quadratic_convergence|lang=zh-CN|style=Feynman)**。在实践中，这意味着你的答案中正确数字的位数几乎在每次迭代中都*翻倍*。如果你从一个不错的猜测开始，只需几步就能得到一个达到[机器精度](@keyword=machine_precision|lang=zh-CN|style=Feynman)的答案。预期的速度层级很清晰：牛顿法是王者，其次是[割线法](@keyword=secant_method|lang=zh-CN|style=Feynman)，而稳扎稳打的[二分法](@keyword=bisection_method|lang=zh-CN|style=Feynman)垫后 [@problem_id:2219719]。

### 高级工具箱：应对现实问题

牛顿法似乎是终极武器，但当现实使问题复杂化时会发生什么？如果求[导数](@keyword=derivative|lang=zh-CN|style=Feynman) $f'(x)$ 是一项极其困难甚至在解析上不可能完成的任务怎么办？这是一个非常普遍的问题。我们必须放弃[二次收敛](@keyword=quadratic_convergence|lang=zh-CN|style=Feynman)吗？

令人惊讶的是，不必。**Steffensen 法**是一项非常巧妙的技术，它能在没有[导数](@keyword=derivative|lang=zh-CN|style=Feynman)的情况下为你提供牛顿法的速度。它用一个巧妙的技巧，仅使用函数值来近似[导数](@keyword=derivative|lang=zh-CN|style=Feynman)：
$$
f'(x_n) \approx \frac{f(x_n + h) - f(x_n)}{h}
$$
其神来之笔在于步长 $h$ 的选择。Steffensen 法设置 $h = f(x_n)$。通过将这个近似代入牛顿公式，我们得到一个完全**无需[导数](@keyword=derivative|lang=zh-CN|style=Feynman)**的方法，却保持了牛顿法光辉的[二次收敛](@keyword=quadratic_convergence|lang=zh-CN|style=Feynman)性 [@problem_id:2206189]。

我们也可以问：如果用一条线（一阶多项式）来近似我们的函数效果这么好，为什么不用抛物线（二阶多项式）呢？这正是**Müller 法**所做的。它取三个点，拟合一条唯一的抛物线穿过它们，并找到抛物[线与](@keyword=wired_and|lang=zh-CN|style=Feynman) x 轴的交点。这使得其收敛率约为 $1.84$——比割线法快，但不如牛顿法 [@problem_id:2188389]。使用抛物线的一个奇妙副作用是它们可以有[复数根](@keyword=complex_roots|lang=zh-CN|style=Feynman)，这使得 Müller 法天然地能够寻找函数的[复数根](@keyword=complex_roots|lang=zh-CN|style=Feynman)。我们甚至可以更进一步：**Chebyshev's method**通过将泰勒级数比[牛顿法](@keyword=newton_method|lang=zh-CN|style=Feynman)再展开一项来引入二阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)，以需要 $f''(x)$ 为代价实现了[三次收敛](@keyword=cubic_convergence|lang=zh-CN|style=Feynman)（$p=3$） [@problem_id:2190211]。

但即使是强大的[牛顿法](@keyword=newton_method|lang=zh-CN|style=Feynman)也有其阿喀琉斯之踵：**[重根](@keyword=repeated_roots|lang=zh-CN|style=Feynman)**。如果函数及其前 $m-1$ 阶[导数](@keyword=derivative|lang=zh-CN|style=Feynman)在某点都为零，那么该[根的重数](@keyword=multiplicity_of_roots|lang=zh-CN|style=Feynman)为 $m$。对于[单根](@keyword=simple_roots|lang=zh-CN|style=Feynman)（$m=1$），$f'(x) \neq 0$。对于二重根（$m=2$），例如 $f(x) = (x-1)^2 \sin(x)$ 在 $x=1$ 处的根，我们有 $f(1)=0$ 和 $f'(1)=0$。在这样的点上，切线是水平的，我们“沿切线滑下”的比喻就失效了。公式中涉及除以一个趋近于零的数，神奇的[二次收敛](@keyword=quadratic_convergence|lang=zh-CN|style=Feynman)退化为缓慢的[线性收敛](@keyword=linear_convergence|lang=zh-CN|style=Feynman) [@problem_id:2422751]。然而，并非全无希望。如果我们知道[根的重数](@keyword=multiplicity_of_roots|lang=zh-CN|style=Feynman) $m$，我们可以通过一个简单的修正来恢复[二次收敛](@keyword=quadratic_convergence|lang=zh-CN|style=Feynman)：
$$
x_{n+1} = x_{n} - m \frac{f(x_{n})}{f'(x_{n})}
$$
这个调整修正了根部附近的“平坦”性，展示了这些数值思想美妙的适应性。

### 集大成者与更广阔的世界

那么，你应该使用哪种方法？是谨慎的[二分法](@keyword=bisection_method|lang=zh-CN|style=Feynman)，是聪明但有缺陷的[试位法](@keyword=method_of_false_position|lang=zh-CN|style=Feynman)，是快速但有风险的割线法，还是强大但要求苛刻的牛顿法？在实践中，你通常不必做出选择。

**Brent 法**是实用[算法设计](@keyword=algorithm_design|lang=zh-CN|style=Feynman)的杰作，它是一种旨在集各家之长的混合方法。它是许多科学计算库中的主力。它维持一个区间，像[二分法](@keyword=bisection_method|lang=zh-CN|style=Feynman)一样保证收敛。但在该区间内，它会积极尝试更快的方法，如[割线法](@keyword=secant_method|lang=zh-CN|style=Feynman)或[逆二次插值](@keyword=inverse_quadratic_interpolation|lang=zh-CN|style=Feynman)（Müller 法的近亲）。然而，它非常多疑：在每一步，它都会检查快速方法是否产生了合理的结果。如果步长太大，或者未能充分缩小区间，它就会拒绝这个“聪明”的步骤，退回到可靠的[二分法](@keyword=bisection_method|lang=zh-CN|style=Feynman)步骤。一个稳健的实现首先会检查根是否被框定（$f(a)f(b)  0$）；如果不是，它会带错误退出，拒绝开始一场无望的搜索 [@problem_id:2157790]。它是速度与安全的完美结合。

我们整个旅程都是关于找到一个单一的数 $x$ 使得 $f(x)=0$。但如果我们需要找到一对数 $(x_1, x_2)$ 同时求解两个方程组成的方程组呢？或者一千个方程中的一千个变量呢？这就是天气预报、[电路设计](@keyword=circuit_design|lang=zh-CN|style=Feynman)和[经济建模](@keyword=economic_modeling|lang=zh-CN|style=Feynman)的世界。

我们已经发展的思想可以完美地推广。[牛顿法](@keyword=newton_method|lang=zh-CN|style=Feynman)可以扩展到更高维度，但它需要在每一步计算并求逆*雅可比矩阵*——一个包含所有可能[偏导数](@keyword=partial_derivatives|lang=zh-CN|style=Feynman)的矩阵——这是一项计算量巨大的任务。但割线法的精神提供了一条出路。**Broyden 法**是一种所谓的“拟牛顿”法，它为方程组所做的事情，就像[割线法](@keyword=secant_method|lang=zh-CN|style=Feynman)为单个方程所做的一样。它避免了[从头计算](@keyword=ab_initio_calculations|lang=zh-CN|style=Feynman)完整的雅可比矩阵。相反，它从一个近似开始，并利用每一步的信息对其雅可比矩阵的逆进行一次巧妙、低成本的*更新* [@problem_id:2158099]。这是一个绝佳的例子，说明一个简单而强大的思想——从连续的点来近似[导数](@keyword=derivative|lang=zh-CN|style=Feynman)——如何可以被扩展以解决极其复杂的问题。事实证明，对零的追寻，是一场开启整个计算科学领域的旅程。