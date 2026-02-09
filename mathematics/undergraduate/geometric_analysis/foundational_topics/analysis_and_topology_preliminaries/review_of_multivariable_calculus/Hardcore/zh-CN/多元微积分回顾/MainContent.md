## 引言
多元微积分是连接代数、几何与分析的桥梁，是现代科学与工程领域的通用语言。它将单变量微积分中关于变化率和累积的思想推广到更高维度，为我们描述和理解复杂的、多因素相互作用的系统提供了强大的数学工具。然而，学习者常常在掌握了孤立的计算技巧后，对其背后统一的几何思想和深刻的跨学科联系感到困惑。本文旨在填补这一知识鸿沟，为读者提供一个连贯而深入的复习框架。

本文将引导读者重温多元微积分的壮丽图景。在第一章“**原理与机制**”中，我们将从欧几里得空间的几何基础出发，重新审视全微分的本质，探讨梯度、散度、旋度等关键算子的几何意义，并深入理解隐函数定理和广义斯托克斯定理等核心理论。随后，在第二章“**应用与跨学科联系**”中，我们将展示这些抽象的原理如何应用于物理学、工程学、数据科学和机器学习等前沿领域，揭示数学理论的现实效用。最后，通过第三章“**动手实践**”中的精选问题，读者将有机会亲手运用所学知识解决具体问题，从而巩固和深化理解。通过这一结构化的学习路径，我们期望读者不仅能“会算”，更能“理解”，真正掌握多元微积分的思想精髓。

## 原理与机制

本章旨在回顾多元微积分的核心原理与机制。我们假定读者已对该主题有初步了解，本章的目标是深化理解，并揭示这些概念之间深刻的内在联系。我们将从欧几里得空间的基本几何结构出发，系统地探讨微分、积分以及连接它们的宏伟定理。

### 欧几里得空间的几何与分析结构

在深入研究多变量函数的微积分之前，我们必须首先明确我们工作所在的空间——欧几里得空间 $\mathbb{R}^n$——的结构。我们如何测量其中向量的“长度”和点之间的“距离”？这些基本概念都源于**内积** (inner product) 的定义。

#### 内积、范数与度量

在实向量空间 $\mathbb{R}^n$ 上，一个内积是一个函数 $\langle \cdot, \cdot \rangle: \mathbb{R}^n \times \mathbb{R}^n \to \mathbb{R}$，它对于任意向量 $\mathbf{x}, \mathbf{y}, \mathbf{z} \in \mathbb{R}^n$ 和标量 $a, b \in \mathbb{R}$ 满足以下三个公理 [@problem_id:3060423]：

1.  **对称性 (Symmetry):** $\langle \mathbf{x}, \mathbf{y} \rangle = \langle \mathbf{y}, \mathbf{x} \rangle$。
2.  **双线性性 (Bilinearity):** 内积在每个参数上都是线性的。即 $\langle a\mathbf{x} + b\mathbf{y}, \mathbf{z} \rangle = a\langle \mathbf{x}, \mathbf{z} \rangle + b\langle \mathbf{y}, \mathbf{z} \rangle$。结合对称性，可知其在第二个参数上也是线性的。
3.  **正定性 (Positive-definiteness):** $\langle \mathbf{x}, \mathbf{x} \rangle \ge 0$，且等号成立当且仅当 $\mathbf{x} = \mathbf{0}$。

最常见的内积是标准点积（dot product），但上述公理化的定义允许更广泛的几何结构。一旦定义了内积，向量的**范数** (norm) 或长度便自然产生，定义为 $\Vert\mathbf{x}\Vert = \sqrt{\langle \mathbf{x}, \mathbf{x} \rangle}$。这个由内积诱导的范数满足成为一个范数所需的三个条件：

-   **正定性:** 由内积的正定性直接得到，$\Vert\mathbf{x}\Vert \ge 0$ 且 $\Vert\mathbf{x}\Vert = 0 \iff \mathbf{x} = \mathbf{0}$。
-   **绝对齐次性 (Absolute Homogeneity):** 对于任意标量 $\alpha \in \mathbb{R}$，$\Vert\alpha\mathbf{x}\Vert = \sqrt{\langle \alpha\mathbf{x}, \alpha\mathbf{x} \rangle} = \sqrt{\alpha^2 \langle \mathbf{x}, \mathbf{x} \rangle} = |\alpha| \sqrt{\langle \mathbf{x}, \mathbf{x} \rangle} = |\alpha|\Vert\mathbf{x}\Vert$。
-   **三角不等式 (Triangle Inequality):** $\Vert\mathbf{x} + \mathbf{y}\Vert \le \Vert\mathbf{x}\Vert + \Vert\mathbf{y}\Vert$。其证明是内积结构的一个优美应用。我们考察其平方：
    $$ \Vert\mathbf{x} + \mathbf{y}\Vert^2 = \langle \mathbf{x} + \mathbf{y}, \mathbf{x} + \mathbf{y} \rangle = \langle \mathbf{x}, \mathbf{x} \rangle + 2\langle \mathbf{x}, \mathbf{y} \rangle + \langle \mathbf{y}, \mathbf{y} \rangle = \Vert\mathbf{x}\Vert^2 + 2\langle \mathbf{x}, \mathbf{y} \rangle + \Vert\mathbf{y}\Vert^2 $$
    应用源于内积公理的**柯西-施瓦茨不等式** (Cauchy-Schwarz inequality)，即 $|\langle \mathbf{x}, \mathbf{y} \rangle| \le \Vert\mathbf{x}\Vert \Vert\mathbf{y}\Vert$，我们有 $\langle \mathbf{x}, \mathbf{y} \rangle \le \Vert\mathbf{x}\Vert \Vert\mathbf{y}\Vert$。代入上式得到：
    $$ \Vert\mathbf{x} + \mathbf{y}\Vert^2 \le \Vert\mathbf{x}\Vert^2 + 2\Vert\mathbf{x}\Vert \Vert\mathbf{y}\Vert + \Vert\mathbf{y}\Vert^2 = (\Vert\mathbf{x}\Vert + \Vert\mathbf{y}\Vert)^2 $$
    两边取平方根即得三角不等式。

有了范数，两点 $\mathbf{x}$ 和 $\mathbf{y}$ 之间的**度量** (metric) 或距离就可被定义为它们差向量的范数：$d(\mathbf{x}, \mathbf{y}) = \Vert\mathbf{x} - \mathbf{y}\Vert$。可以验证，这个定义满足度量空间的所有公理（非负性、同一性、对称性和三角不等式），这些性质均直接继承自范数的性质 [@problem_id:3060423]。因此，内积是构建欧几里得空间几何结构的基石。

### 多变量微分

单变量微积分的核心思想是用一条切线来近似函数。在多变量世界中，这个思想被推广为用一个**线性映射**来近似一个（通常是更复杂的）函数在某点附近的行为。

#### 全微分的概念

考虑一个函数 $f: \mathbb{R}^n \to \mathbb{R}^m$。我们说 $f$ 在点 $\mathbf{a} \in \mathbb{R}^n$ **可微** (differentiable)，如果存在一个线性映射 $Df(\mathbf{a}): \mathbb{R}^n \to \mathbb{R}^m$，使得对于一个无穷小位移向量 $\mathbf{h}$，函数值的变化可以被近似为：
$$ f(\mathbf{a}+\mathbf{h}) = f(\mathbf{a}) + Df(\mathbf{a})\mathbf{h} + r(\mathbf{h}) $$
其中余项 $r(\mathbf{h})$ 比 $\mathbf{h}$ 的长度更快地趋于零，即 $r(\mathbf{h}) = o(\Vert\mathbf{h}\Vert)$，或者更精确地说：
$$ \lim_{\mathbf{h}\to \mathbf{0}} \frac{\Vert r(\mathbf{h})\Vert}{\Vert\mathbf{h}\Vert} = 0 $$
这个线性映射 $Df(\mathbf{a})$ 被称为 $f$ 在点 $\mathbf{a}$ 的**全微分** (total derivative) 或弗雷歇导数 (Fréchet derivative)。它捕捉了函数在点 $\mathbf{a}$ 附近所有方向上变化的一阶信息，是单变量导数概念的真正推广 [@problem_id:3060428]。

#### 可微性与连续性

一个基本且重要的定理是：**可微性蕴含连续性**。如果一个函数在一点可微，那么它在该点必定连续。证明这个定理的过程揭示了全微分定义的威力 [@problem_id:3060428]。要证明 $f$ 在 $\mathbf{a}$ 点连续，我们需要证明 $\lim_{\mathbf{x}\to \mathbf{a}} f(\mathbf{x}) = f(\mathbf{a})$，这等价于证明 $\lim_{\mathbf{h}\to \mathbf{0}} \Vert f(\mathbf{a}+\mathbf{h}) - f(\mathbf{a}) \Vert = 0$。

从可微性的定义出发，我们有：
$$ \Vert f(\mathbf{a}+\mathbf{h}) - f(\mathbf{a}) \Vert = \Vert Df(\mathbf{a})\mathbf{h} + r(\mathbf{h}) \Vert \le \Vert Df(\mathbf{a})\mathbf{h} \Vert + \Vert r(\mathbf{h}) \Vert $$
现在我们分析右侧的两项。首先，有限维赋范空间上的任何线性映射（如此处的 $Df(\mathbf{a})$）都是有界的，即存在一个常数 $C \ge 0$ 使得 $\Vert Df(\mathbf{a})\mathbf{h} \Vert \le C\Vert\mathbf{h}\Vert$ 对于所有 $\mathbf{h}$ 成立。因此，当 $\mathbf{h} \to \mathbf{0}$ 时，这一项也趋于 $0$。其次，根据余项的定义，$\Vert r(\mathbf{h}) \Vert$ 本身也趋于 $0$（实际上比 $\Vert\mathbf{h}\Vert$ 更快）。因此，不等式右侧两项之和趋于 $0$，从而证明了 $\Vert f(\mathbf{a}+\mathbf{h}) - f(\mathbf{a}) \Vert \to 0$。

#### 偏导数与雅可比矩阵

全微分作为一个抽象的线性映射，如何与具体计算联系起来？答案是**偏导数** (partial derivatives)。$f$ 对第 $j$ 个变量 $x_j$ 的偏导数是在其他变量保持不变时，函数沿 $x_j$ 坐标轴方向的变化率。

然而，一个常见的误区是认为所有偏导数存在就足以保证函数可微。事实并非如此。考虑函数族 [@problem_id:3060402]：
$$ f_{\alpha}(x,y)= \begin{cases} \dfrac{x y}{(x^2+y^2)^{\alpha/2}},  & (x,y) \neq (0,0), \\ 0, & (x,y)=(0,0). \end{cases} $$
通过定义可以计算出，在原点 $(0,0)$，对于任何实数 $\alpha$，其偏导数 $\frac{\partial f_{\alpha}}{\partial x}(0,0)$ 和 $\frac{\partial f_{\alpha}}{\partial y}(0,0)$ 都存在且等于 $0$。如果仅凭偏导数存在来判断，我们可能会错误地认为函数在原点可微，且其微分为零映射。然而，要检验可微性，我们必须回到全微分的定义，即考察极限 $\lim_{(h_1,h_2)\to(0,0)} \frac{f_{\alpha}(h_1,h_2)}{\sqrt{h_1^2+h_2^2}}$ 是否为零。通过转换为极坐标，这个表达式变为 $r^{1-\alpha}\cos\theta\sin\theta$。当 $\alpha \ge 1$ 时，这个极限要么依赖于路径（$\theta$），要么发散，总之不为零。因此，对于 $\alpha \ge 1$，尽管所有偏导数在原点都存在，函数 $f_{\alpha}$ 在原点并不可微。

这个例子深刻地表明，可微性是一个比所有方向导数存在更强的条件。可微性要求函数在某点附近能被一个**单一**的线性映射很好地近似，而不仅仅是在各个坐标轴方向上。

当函数 $f: \mathbb{R}^n \to \mathbb{R}^m$ 确实可微时，其全微分 $Df(\mathbf{a})$ 这个线性映射可以用一个矩阵来表示。在 $\mathbb{R}^n$ 和 $\mathbb{R}^m$ 的标准基下，这个 $m \times n$ 矩阵被称为**雅可比矩阵** (Jacobian matrix)，记作 $J_f(\mathbf{a})$。它的第 $(i,j)$ 个元素恰好是函数第 $i$ 个分量 $f_i$ 对第 $j$ 个变量 $x_j$ 的偏导数，即 $(J_f(\mathbf{a}))_{ij} = \frac{\partial f_i}{\partial x_j}(\mathbf{a})$ [@problem_id:3060447]。

重要的是要区分抽象的线性映射 $Df(\mathbf{a})$ 和它的矩阵表示 $J_f(\mathbf{a})$。前者是内在的、不依赖于坐标系的对象，而后者则依赖于基的选择。如果我们在定义域和到达域选择不同的基，雅可比矩阵也会相应地通过一个变换公式而改变 [@problem_id:3060447]。

### 关键微分算子及其几何意义

在向量微积分中，梯度、散度和旋度是三个核心的微分算子，它们具有深刻的物理和几何意义。

#### 梯度和方向导数

对于一个标量场 $f: \mathbb{R}^n \to \mathbb{R}$，其**梯度** (gradient) $\nabla f$ 是一个向量场，定义为包含所有偏导数的向量：$\nabla f = (\frac{\partial f}{\partial x_1}, \dots, \frac{\partial f}{\partial x_n})$。在矩阵表示中，梯度向量是雅可比矩阵（此时是一个 $1 \times n$ 的行向量，也称为 $f$ 的微分 $df$）的转置 [@problem_id:3060447]。

梯度 $\nabla f(\mathbf{p})$ 在点 $\mathbf{p}$ 处具有两个核心的几何解释：

1.  **最速上升方向**：$\nabla f(\mathbf{p})$ 指向函数 $f$ 在点 $\mathbf{p}$ 增长最快的方向，其模长 $|\nabla f(\mathbf{p})|$ 等于这个最大增长率 [@problem_id:3060408]。
2.  **法向量**：$\nabla f(\mathbf{p})$ 与函数 $f$ 通过点 $\mathbf{p}$ 的**等值面** (level set) $\Sigma = \{\mathbf{x} \in \mathbb{R}^n \mid f(\mathbf{x}) = c\}$ 正交。也就是说，梯度是等值面的法向量。

第二个性质的证明非常直观 [@problem_id:3060465]。考虑等值面 $\Sigma$ 上一条穿过点 $\mathbf{p}$ 的任意平滑曲线 $\gamma(t)$，且 $\gamma(0)=\mathbf{p}$。由于曲线在等值面上，我们有 $f(\gamma(t)) = c$（常数）。根据链式法则，对时间 $t$ 求导得到：
$$ \frac{d}{dt}f(\gamma(t)) = \nabla f(\gamma(t)) \cdot \gamma'(t) = 0 $$
在 $t=0$ 时，我们得到 $\nabla f(\mathbf{p}) \cdot \gamma'(0) = 0$。由于 $\gamma'(0)$ 是曲线在 $\mathbf{p}$ 点的切向量，而曲线是任意选择的，这表明梯度 $\nabla f(\mathbf{p})$ 与等值面在点 $\mathbf{p}$ 的任何切向量都正交。

这个性质非常有用，例如，它可以用来构造等值面的切平面（或切线）。切平面是在点 $\mathbf{p}$ 处与等值面相切的平面，其上任意一点 $\mathbf{x}$ 与点 $\mathbf{p}$ 的连线向量 $\mathbf{x}-\mathbf{p}$ 必与法向量 $\nabla f(\mathbf{p})$ 正交。因此，切平面的方程为 $\nabla f(\mathbf{p}) \cdot (\mathbf{x}-\mathbf{p}) = 0$。例如，对于函数 $f(x,y) = x^2+y^2$ 和其等值线 $f=1$（单位圆），在点 $p=(\frac{1}{\sqrt{2}}, \frac{1}{\sqrt{2}})$ 处，梯度为 $\nabla f(p) = (2x, 2y)|_p = (\sqrt{2}, \sqrt{2})$。因此，该点的切线方程为 $(\sqrt{2}, \sqrt{2}) \cdot (x-\frac{1}{\sqrt{2}}, y-\frac{1}{\sqrt{2}}) = 0$，化简后得到 $x+y-\sqrt{2}=0$ [@problem_id:3060465]。

#### 散度与旋度

对于一个向量场 $\mathbf{v}: \mathbb{R}^3 \to \mathbb{R}^3$，其中 $\mathbf{v} = (v_1, v_2, v_3)$，我们定义两个重要的算子：

-   **散度 (Divergence):** $\text{div}\,\mathbf{v} = \nabla \cdot \mathbf{v} = \frac{\partial v_1}{\partial x} + \frac{\partial v_2}{\partial y} + \frac{\partial v_3}{\partial z}$。它是一个标量场。
-   **旋度 (Curl):** $\text{curl}\,\mathbf{v} = \nabla \times \mathbf{v} = \left(\frac{\partial v_3}{\partial y} - \frac{\partial v_2}{\partial z}, \frac{\partial v_1}{\partial z} - \frac{\partial v_3}{\partial x}, \frac{\partial v_2}{\partial x} - \frac{\partial v_1}{\partial y}\right)$。它是一个向量场。

这些算子有不依赖于坐标系的物理和几何意义 [@problem_id:3060408]。想象向量场 $\mathbf{v}$ 代表流体的速度场：

-   **散度** $\text{div}\,\mathbf{v}$ 在一点的数值衡量了流体在该点附近单位体积的净流出率。如果 $\text{div}\,\mathbf{v} > 0$，该点就像一个“源头”，流体在此处膨胀或产生；如果 $\text{div}\,\mathbf{v}  0$，该点就像一个“汇”，流体在此处压缩或消失。如果处处有 $\text{div}\,\mathbf{v} = 0$，则称该流场是**不可压缩的** (incompressible)。
-   **旋度** $\text{curl}\,\mathbf{v}$ 在一点的向量描述了流体微元在该点附近的瞬时旋转。该向量的方向是旋转轴的方向（遵循右手法则），其大小是旋转角速度的两倍。如果处处有 $\text{curl}\,\mathbf{v} = \mathbf{0}$，则称该流场是**无旋的** (irrotational)。

考虑一个线性向量场 $\mathbf{v}(x,y,z) = (ax, by, cz)$ [@problem_id:3060408]。其散度为常数 $a+b+c$，表示流场以均匀的速率在各向异性地膨胀或收缩。其旋度恒为零，说明这是一个无旋流场，流体质点只会被拉伸或压缩，但不会发生旋转。

### 多元微积分基本定理

单变量微积分基本定理将微分和积分联系起来。在多维空间中，这一思想被一系列深刻的定理所继承和推广，它们共同构成了现代几何分析的基石。

#### 隐函数与反函数定理

在分析中，我们经常遇到形如 $F(x,y)=0$ 的方程，并希望从中解出 $y$ 作为 $x$ 的函数，即 $y=\phi(x)$。**隐函数定理** (Implicit Function Theorem) 提供了这种可解性的一个强有力的局部保证 [@problem_id:3060411]。

定理指出：设 $F: \mathbb{R}^{n+k} \to \mathbb{R}^k$ 是一个 $C^1$ 函数，并且在点 $(x_0, y_0)$ 处有 $F(x_0, y_0)=0$。如果在该点，关于“因变量” $y$ 的偏导数矩阵 $D_y F(x_0, y_0)$（一个 $k \times k$ 矩阵）是可逆的，那么在 $x_0$ 的一个邻域 $U$ 内，存在一个唯一的 $C^1$ 函数 $\phi: U \to \mathbb{R}^k$，使得 $\phi(x_0)=y_0$ 并且对于所有 $x \in U$，都有 $F(x, \phi(x)) = 0$。

这个定理的证明本身就是多元分析方法的一个典范，它巧妙地利用了**反函数定理** (Inverse Function Theorem)。其核心思想是构造一个辅助函数 $G: \mathbb{R}^{n+k} \to \mathbb{R}^{n+k}$，定义为 $G(x,y) = (x, F(x,y))$。$D_y F$ 可逆的条件恰好保证了 $G$ 在 $(x_0, y_0)$ 点的雅可比矩阵是可逆的。根据反函数定理，$G$ 在该点附近存在一个 $C^1$ 的局部逆 $G^{-1}$。我们所求的函数 $\phi(x)$ 正是这个逆映射在 $v=0$ 平面上的分量，即 $\phi(x) = Y(x,0)$，其中 $G^{-1}(u,v)=(u,Y(u,v))$。

此外，通过对恒等式 $F(x, \phi(x))=0$ 使用链式法则进行隐式微分，我们可以求出隐函数 $\phi$ 的导数：
$$ D\phi(x) = -\left(D_y F(x, \phi(x))\right)^{-1} D_x F(x, \phi(x)) $$

#### 积分与变量替换公式

在多重积分中，正如在单重积分中一样，**变量替换** (change of variables) 是一个关键的计算工具。其公式为 [@problem_id:3060463]：
$$ \int_{\Omega} f(x) \,dx = \int_{\tilde{\Omega}} f(\Phi(u)) |\det D\Phi(u)| \,du $$
这里，$\Phi: \tilde{\Omega} \to \Omega$ 是一个 $C^1$ 微分同胚（即一个可微且有可微逆的 bijective map），它将 $u$-坐标空间中的区域 $\tilde{\Omega}$ 映射到 $x$-坐标空间中的区域 $\Omega$。

这个公式的直观解释是，当坐标从 $u$ 变换到 $x = \Phi(u)$ 时，一个无穷小的体积元 $du$ 被映射到一个无穷小的体积元 $dx$。这个体积变化的比例因子正是由 $\Phi$ 在该点的线性近似（即其微分 $D\Phi(u)$）所决定的。线性代数告诉我们，一个线性变换对体积的缩放因子是其行列式的绝对值。因此，$|\det D\Phi(u)|$（通常称为雅可比行列式）扮演了局部体积缩放因子的角色。一个严格的证明通常通过将积分区域分解为许多小块，在每个小块上用线性变换近似 $\Phi$，然后利用单位分解（partition of unity）将这些局部结果“粘合”起来。

#### 斯托克斯定理与区域的拓扑

所有微积分基本定理的终极推广是广义**斯托克斯定理** (Stokes' Theorem)。在其最优美的现代形式中，它用微分形式的语言表述为 [@problem_id:3060449]：
$$ \int_M d\omega = \int_{\partial M} \omega $$
这里，$M$ 是一个带边界 $\partial M$ 的 $k$ 维可定向流形，$\omega$ 是一个 $(k-1)$-形式，$d\omega$ 是其外微分。这个简洁的公式统一了牛顿-莱布尼茨公式、格林公式、经典斯托克斯公式和高斯散度定理。

这个定理揭示了微分与积分之间深刻的对偶关系，同时也引出了拓扑学在分析中的核心作用。我们定义一个微分形式 $\omega$ 是**闭的** (closed) 如果 $d\omega=0$，是**恰当的** (exact) 如果存在一个更低阶的形式 $\eta$ 使得 $\omega=d\eta$（对于1-形式，即 $\omega = df$）。由于外微分的一个基本性质是 $d^2=0$，我们知道**任何恰当形式都是闭的**。

一个核心问题是：反过来是否成立？一个闭的形式是否一定是恰当的？答案是否定的，而这恰恰与定义域的拓扑性质有关。

考虑定义在“穿孔平面” $U = \mathbb{R}^2 \setminus \{(0,0)\}$ 上的1-形式 [@problem_id:3060420]：
$$ \omega = \frac{-y\,dx + x\,dy}{x^2 + y^2} $$
可以直接计算出 $d\omega=0$，所以它是闭的。但它是恰当的吗？换句话说，是否存在一个定义在整个 $U$ 上的函数 $f$ 使得 $\omega=df$？如果存在，那么根据基本定理，$\omega$ 沿任何闭合路径的积分都应为零。然而，如果我们计算 $\omega$ 沿环绕原点的单位圆 $\gamma$ 的积分，会得到：
$$ \int_{\gamma} \omega = \int_0^{2\pi} 1 \,dt = 2\pi \neq 0 $$
这个非零结果证明了不存在一个全局的、单值的势函数 $f$，因此 $\omega$ 在 $U$ 上不是恰当的。

这里的拓扑障碍在于：闭合曲线 $\gamma$ 在 $U$ 中“圈住”了一个洞。$\gamma$ 所围成的单位圆盘并不完全包含在 $U$ 中，因为它包含了原点。这使得我们无法应用格林公式（斯托克斯定理的二维特例）来断言线积分为零。这个“洞”的存在，正是导致一个闭形式无法成为恰当形式的拓扑原因。这揭示了分析和拓扑之间的深刻联系，是德拉姆上同调理论的起点。

值得注意的是，并非所有在非单连通区域上的闭形式都不是恰当的。例如，在同一个穿孔平面 $U$ 上，形式 $\eta = \frac{x\,dx + y\,dy}{x^2 + y^2}$ 也是闭的，但它却是恰当的，因为它是函数 $f(x,y) = \frac{1}{2}\ln(x^2+y^2)$ 的微分 [@problem_id:3060420]。这表明，非单连通性只是为“闭形式不恰当”提供了可能性，而非必然性。

最后，让我们通过一个具体计算来展示斯托克斯定理的应用。考虑1-形式 $\omega = x\,dy + y\,dz$ 和由 $z=1-x^2-y^2$ 在单位圆盘 $D$ 上方构成的曲面 $M$ [@problem_id:3060449]。计算边界积分 $\int_{\partial M} \omega$ 是困难的。但根据斯托克斯定理，它等于面积分 $\int_M d\omega$。我们首先计算外微分 $d\omega = dx \wedge dy + dy \wedge dz$。然后，我们将曲面 $M$ 参数化，并将这个2-形式拉回到参数域 $D$ 上，得到一个关于 $dx \wedge dy$ 的普通二重积分。计算这个二重积分（例如使用极坐标）最终得到结果 $\pi$，从而轻松获得了原边界积分的值。这展示了斯托克斯定理作为强大计算工具的威力。