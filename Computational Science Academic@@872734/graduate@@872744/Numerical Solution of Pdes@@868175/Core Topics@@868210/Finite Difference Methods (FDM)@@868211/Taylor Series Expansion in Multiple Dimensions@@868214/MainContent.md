## Introduction
The Taylor series expansion is a cornerstone of calculus, providing a powerful way to approximate functions locally using polynomials. While its single-variable form is a staple of introductory analysis, its generalization to multiple dimensions is what truly unlocks the systematic design and rigorous analysis of numerical methods for partial differential equations (PDEs). Many students and practitioners struggle to bridge the conceptual gap between the familiar one-dimensional series and the more abstract multivariate formulation, which is essential for tackling real-world, multi-dimensional problems. This article addresses this challenge by providing a clear, structured exploration of the multivariate Taylor series and its applications.

Over the next three chapters, you will build a comprehensive understanding of this vital tool. The journey begins in **Principles and Mechanisms**, where we derive the multivariate expansion from first principles, introduce the elegant and powerful [multi-index notation](@entry_id:752245), and examine the crucial [remainder term](@entry_id:159839) used for [error analysis](@entry_id:142477). Next, **Applications and Interdisciplinary Connections** demonstrates the theory in action, showing how Taylor series are the engine behind the derivation and analysis of [finite difference schemes](@entry_id:749380), and exploring its connections to fields like control theory, statistics, and physics. Finally, **Hands-On Practices** will allow you to apply these concepts to solve concrete problems in numerical methods. We begin by laying the theoretical groundwork for this indispensable mathematical technique.

## Principles and Mechanisms

The analysis and construction of numerical methods for [partial differential equations](@entry_id:143134) (PDEs) rely profoundly on our ability to approximate functions locally. The Taylor [series expansion](@entry_id:142878), a cornerstone of calculus, provides the fundamental tool for this task. While the one-dimensional Taylor series is a familiar concept, its extension to multiple dimensions unlocks the systematic analysis of multi-dimensional [differential operators](@entry_id:275037) and their discrete approximations. This chapter elucidates the principles and mechanisms of the multivariate Taylor expansion, beginning with its theoretical foundations and culminating in its application to the [error analysis](@entry_id:142477) of [finite difference schemes](@entry_id:749380).

### From One Dimension to Many: A Directional Approach

The most intuitive path to understanding the multivariate Taylor series is by reducing it to the familiar single-variable case. Consider a scalar-valued function $f: \mathbb{R}^n \to \mathbb{R}$ that is sufficiently smooth in a neighborhood of a point $\boldsymbol{x}_0 \in \mathbb{R}^n$. To understand the behavior of $f$ at a nearby point $\boldsymbol{x} = \boldsymbol{x}_0 + \boldsymbol{h}$, where $\boldsymbol{h}$ is a [displacement vector](@entry_id:262782), we can examine the function's values along the straight line segment connecting $\boldsymbol{x}_0$ and $\boldsymbol{x}$.

Let us define a single-variable function $g: [0, 1] \to \mathbb{R}$ by $g(t) = f(\boldsymbol{x}_0 + t\boldsymbol{h})$. This function captures the profile of $f$ along the direction $\boldsymbol{h}$. We have $g(0) = f(\boldsymbol{x}_0)$ and $g(1) = f(\boldsymbol{x})$. The one-dimensional Maclaurin series for $g(t)$ is:
$$ g(t) = g(0) + g'(0)t + \frac{g''(0)}{2!}t^2 + \cdots = \sum_{k=0}^{\infty} \frac{g^{(k)}(0)}{k!} t^k $$
By setting $t=1$, we can express $f(\boldsymbol{x})$ in terms of the derivatives of $g$ evaluated at $t=0$:
$$ f(\boldsymbol{x}) = f(\boldsymbol{x}_0 + \boldsymbol{h}) = g(1) = \sum_{k=0}^{\infty} \frac{g^{(k)}(0)}{k!} $$
The central task is to relate the derivatives of $g$ to the [partial derivatives](@entry_id:146280) of $f$. Using the [multivariate chain rule](@entry_id:635606), the first derivative of $g(t)$ is:
$$ g'(t) = \frac{d}{dt} f(\boldsymbol{x}_0 + t\boldsymbol{h}) = \sum_{i=1}^n \frac{\partial f}{\partial x_i}(\boldsymbol{x}_0 + t\boldsymbol{h}) \frac{d(x_{0,i} + th_i)}{dt} = \sum_{i=1}^n h_i \frac{\partial f}{\partial x_i}(\boldsymbol{x}_0 + t\boldsymbol{h}) $$
This can be written compactly using the **gradient** operator, $\nabla = (\partial/\partial x_1, \dots, \partial/\partial x_n)^T$. At $t=0$, we have $g'(0) = \sum_{i=1}^n h_i \frac{\partial f}{\partial x_i}(\boldsymbol{x}_0) = \nabla f(\boldsymbol{x}_0) \cdot \boldsymbol{h}$. This expression is the **directional derivative** of $f$ at $\boldsymbol{x}_0$ in the direction $\boldsymbol{h}$, often denoted $\partial_{\boldsymbol{h}} f(\boldsymbol{x}_0)$. If $f$ is differentiable at $\boldsymbol{x}_0$, this relationship always holds. For a vector-valued function $f: \mathbb{R}^n \to \mathbb{R}^m$, the gradient is replaced by the **Jacobian matrix** $J_f$, and the [directional derivative](@entry_id:143430) becomes the matrix-vector product $\partial_{\boldsymbol{h}} f(\boldsymbol{x}_0) = J_f(\boldsymbol{x}_0) \boldsymbol{h}$ [@problem_id:3452725].

Continuing to the second derivative of $g(t)$:
$$ g''(t) = \frac{d}{dt} \left( \sum_{i=1}^n h_i \frac{\partial f}{\partial x_i}(\boldsymbol{x}_0 + t\boldsymbol{h}) \right) = \sum_{i=1}^n \sum_{j=1}^n h_i h_j \frac{\partial^2 f}{\partial x_j \partial x_i}(\boldsymbol{x}_0 + t\boldsymbol{h}) $$
We can represent this using a symbolic [differential operator](@entry_id:202628), $(\boldsymbol{h} \cdot \nabla) = \sum_{i=1}^n h_i \frac{\partial}{\partial x_i}$. The derivatives of $g$ are then:
$$ g^{(k)}(t) = \left( \sum_{i=1}^n h_i \frac{\partial}{\partial x_i} \right)^k f(\boldsymbol{x}_0 + t\boldsymbol{h}) = (\boldsymbol{h} \cdot \nabla)^k f(\boldsymbol{x}_0 + t\boldsymbol{h}) $$
Evaluating at $t=0$, the Taylor expansion for $f(\boldsymbol{x}_0 + \boldsymbol{h})$ becomes:
$$ f(\boldsymbol{x}_0 + \boldsymbol{h}) = \sum_{k=0}^{\infty} \frac{1}{k!} (\boldsymbol{h} \cdot \nabla)^k f(\boldsymbol{x}_0) $$
The existence of these derivatives requires sufficient smoothness of $f$. For example, the existence of $g''(0)$ requires $f$ to be twice differentiable at $\boldsymbol{x}_0$. If $f$ is only guaranteed to be once differentiable (or $C^1$), $g''(0)$ may not exist [@problem_id:3452725].

### The Language of Multi-indices

Expanding the operator $(\boldsymbol{h} \cdot \nabla)^k$ is cumbersome. For instance, when $k=2$ and $n=2$, $(\boldsymbolh \cdot \nabla)^2 = (h_1 \partial_{x_1} + h_2 \partial_{x_2})^2 = h_1^2 \partial_{x_1x_1} + 2h_1h_2 \partial_{x_1x_2} + h_2^2 \partial_{x_2x_2}$. The general expansion is given by the Multinomial Theorem. To write this compactly and systematically, we introduce **[multi-index notation](@entry_id:752245)** [@problem_id:3452696].

A **multi-index** is an $n$-tuple of non-negative integers, $\alpha = (\alpha_1, \alpha_2, \dots, \alpha_n) \in \mathbb{N}_0^n$. We define the following operations:
-   The **magnitude** (or [total order](@entry_id:146781)): $|\alpha| = \alpha_1 + \alpha_2 + \cdots + \alpha_n$.
-   The **[factorial](@entry_id:266637)**: $\alpha! = \alpha_1! \alpha_2! \cdots \alpha_n!$.
-   The **power**: For a vector $\boldsymbol{h} = (h_1, \dots, h_n)$, $\boldsymbol{h}^\alpha = h_1^{\alpha_1} h_2^{\alpha_2} \cdots h_n^{\alpha_n}$.
-   The **partial derivative**: $D^\alpha f = \frac{\partial^{|\alpha|} f}{\partial x_1^{\alpha_1} \partial x_2^{\alpha_2} \cdots \partial x_n^{\alpha_n}}$.

With this notation, the multinomial expansion of the operator becomes:
$$ (\boldsymbol{h} \cdot \nabla)^k f(\boldsymbol{x}_0) = \left(\sum_{i=1}^n h_i \frac{\partial}{\partial x_i}\right)^k f(\boldsymbol{x}_0) = \sum_{|\alpha|=k} \frac{k!}{\alpha!} \boldsymbol{h}^\alpha D^\alpha f(\boldsymbol{x}_0) $$
Substituting this into the Taylor series, the $k!$ term cancels, yielding a remarkably elegant expression. The **multivariate Taylor polynomial of order $m$** for $f$ about $\boldsymbol{x}_0$ is:
$$ T_m f(\boldsymbol{x}) = \sum_{|\alpha| \le m} \frac{D^\alpha f(\boldsymbol{x}_0)}{\alpha!} (\boldsymbol{x}-\boldsymbol{x}_0)^\alpha $$
The full Taylor series is obtained by letting $m \to \infty$. This compact formula is the bedrock of theoretical analysis in the numerical solution of PDEs [@problem_id:3452696].

### The Remainder Term and Rigorous Bounds

For numerical applications, we must control the error of the Taylor approximation. The **[remainder term](@entry_id:159839)** is defined as $R_m(\boldsymbol{x}; \boldsymbol{x}_0) = f(\boldsymbol{x}) - T_m f(\boldsymbol{x})$. Its form can be derived by applying the one-dimensional remainder formulas to our auxiliary function $g(t) = f(\boldsymbol{x}_0 + t\boldsymbol{h})$.

The one-dimensional Taylor theorem provides two common forms for the remainder: the integral form and the Lagrange (or mean-value) form. These translate directly into the multivariate setting [@problem_id:3452703].

1.  **The Integral Form:** The remainder can be expressed as an integral of the next derivative over the path:
    $$ R_m(\boldsymbol{x}; \boldsymbol{x}_0) = \int_0^1 \frac{(1-t)^m}{m!} g^{(m+1)}(t) \, dt = \sum_{|\alpha|=m+1} \frac{(\boldsymbol{x}-\boldsymbol{x}_0)^\alpha}{\alpha!} \int_0^1 (m+1)(1-t)^m D^\alpha f(\boldsymbol{x}_0 + t(\boldsymbol{x}-\boldsymbol{x}_0)) \, dt $$
2.  **The Lagrange Form:** The remainder can be written in terms of the next derivative evaluated at a single, unknown intermediate point on the line segment:
    $$ R_m(\boldsymbol{x}; \boldsymbol{x}_0) = \frac{g^{(m+1)}(\xi)}{(m+1)!} = \sum_{|\alpha|=m+1} \frac{D^\alpha f(\boldsymbol{x}_0 + \xi(\boldsymbol{x}-\boldsymbol{x}_0))}{\alpha!} (\boldsymbol{x}-\boldsymbol{x}_0)^\alpha, \quad \text{for some } \xi \in (0,1) $$

While the Lagrange form is often simpler to write, the **integral form is generally more powerful for the rigorous analysis of [finite difference schemes](@entry_id:749380)**. When constructing a discrete operator, one combines function values from several points, leading to a [linear combination](@entry_id:155091) of remainder terms. With the Lagrange form, each remainder has its own unknown intermediate point $\xi$, making it difficult to analyze cancellations. The integral form, however, expresses the total error as a single integral of a weighted combination of derivatives (a structure known as a Peano kernel), which allows for precise [error analysis](@entry_id:142477) and the derivation of sharp bounds [@problem_id:3452703].

To obtain a practical error bound from the remainder formula, we can use [operator norms](@entry_id:752960). For example, a bound derived from the Lagrange form is:
$$ |R_m(\boldsymbol{x}; \boldsymbol{x}_0)| \le \frac{\|\boldsymbol{x}-\boldsymbol{x}_0\|^{m+1}}{(m+1)!} \sup_{\boldsymbol{z} \in K} \|D^{m+1} f(\boldsymbol{z})\| $$
where $\|D^{m+1} f\|$ is the operator norm of the $(m+1)$-st derivative tensor and $K$ is a convex set containing the line segment from $\boldsymbol{x}_0$ to $\boldsymbol{x}$. The tightness of this bound depends on the choice of the domain $K$ over which the supremum is taken. A smaller domain, such as a rectangle enclosing the points, can yield a tighter bound than a larger one, like a ball, if the maximum of the derivative norm occurs outside the smaller domain [@problem_id:3452815].

### Application: Truncation Error of Finite Difference Schemes

The primary use of Taylor series in numerical PDEs is to determine the **[local truncation error](@entry_id:147703)** of a [finite difference](@entry_id:142363) scheme. The truncation error is the discrepancy that arises when the exact solution of the PDE is substituted into the discrete approximation. It measures how faithfully the discrete operator mimics the continuous one.

Let's analyze the standard **5-point discrete Laplacian** on a uniform Cartesian grid with spacing $h$ [@problem_id:3452801]:
$$ \Delta_h u(x,y) = \frac{u(x+h,y)+u(x-h,y)+u(x,y+h)+u(x,y-h)-4u(x,y)}{h^2} $$
To find its truncation error, $\tau(x,y;h) = \Delta_h u(x,y) - \Delta u(x,y)$, we expand each term in a Taylor series around $(x,y)$. For $u(x+h,y)$ and $u(x-h,y)$:
$$ u(x\pm h, y) = u \pm h u_x + \frac{h^2}{2} u_{xx} \pm \frac{h^3}{6} u_{xxx} + \frac{h^4}{24} u_{xxxx} + \mathcal{O}(h^5) $$
Adding these and subtracting $2u$ gives the centered second difference approximation in $x$:
$$ \frac{u(x+h,y) + u(x-h,y) - 2u(x,y)}{h^2} = u_{xx} + \frac{h^2}{12}u_{xxxx} + \mathcal{O}(h^4) $$
An analogous expression holds for the $y$-direction. Combining them for $\Delta_h u$:
$$ \Delta_h u = (u_{xx} + \frac{h^2}{12}u_{xxxx}) + (u_{yy} + \frac{h^2}{12}u_{yyyy}) + \mathcal{O}(h^4) $$
The continuous Laplacian is $\Delta u = u_{xx} + u_{yy}$. The truncation error is therefore:
$$ \tau(h) = \Delta_h u - \Delta u = \frac{h^2}{12}(u_{xxxx} + u_{yyyy}) + \mathcal{O}(h^4) $$
Since the leading error term is proportional to $h^2$, we say the scheme is **second-order accurate**. The scheme is **consistent** because $\tau(h) \to 0$ as $h \to 0$.

This analysis highlights two key aspects [@problem_id:3452701]:
1.  **The role of $|\alpha|$:** On an isotropic grid ($h_x = h_y = h$), a derivative term $D^\alpha u$ in the Taylor expansion is multiplied by powers of $h$ that sum to $|\alpha|$. The order of accuracy is thus determined by the smallest magnitude $|\alpha|$ of the non-canceling error terms.
2.  **The role of $\alpha$:** The specific multi-index $\alpha$ determines the structure of the derivative itself (e.g., $u_{xxxx}$ vs. $u_{xxyy}$). The coefficients of the stencil are chosen to make desired low-order derivative terms match the target operator and to cancel other terms.

Because the leading error term for the 5-point Laplacian involves fourth-order derivatives, the scheme is exact (i.e., $\tau(h)=0$) for any polynomial of degree three or less. In fact, since $u_{xxxx}$ and $u_{yyyy}$ are both zero for a quadratic polynomial, the scheme is exact for quadratics as well [@problem_id:3452801].

This method of "matching coefficients" can be applied to more complex operators. For instance, to approximate a general [elliptic operator](@entry_id:191407) $\mathcal{L} u = a u_{xx} + 2b u_{xy} + c u_{yy}$, we can propose a more general **[9-point stencil](@entry_id:746178)**. However, the geometry of the stencil imposes constraints. A symmetric [9-point stencil](@entry_id:746178), where points are weighted equally based on their distance from the center, cannot approximate the mixed derivative term $u_{xy}$, as the corresponding Taylor series coefficients for $\partial_{xy}$ will always sum to zero [@problem_id:3452810]. To approximate the $u_{xy}$ term, an asymmetric stencil is required, such as the one used in the following discrete operator [@problem_id:3452728]:
$$ \mathcal{L}_h u = \frac{u_{i+1,j}-2u_{i,j}+u_{i-1,j}}{h^2} + 2\rho \frac{u_{i+1,j+1}-u_{i+1,j-1}-u_{i-1,j+1}+u_{i-1,j-1}}{4h^2} + \frac{u_{i,j+1}-2u_{i,j}+u_{i,j-1}}{h^2} $$
A Taylor expansion confirms that this operator is a consistent, second-order approximation to $\mathcal{L}u = u_{xx} + 2\rho u_{xy} + u_{yy}$.

### Advanced Considerations

#### Coordinate Systems and Averaged Expansions
The choice of coordinate system can affect the appearance of the formulas. In polar coordinates $(r, \theta)$, the Laplacian is $\Delta u = u_{rr} + \frac{1}{r}u_r + \frac{1}{r^2}u_{\theta\theta}$. The terms $\frac{1}{r}$ and $\frac{1}{r^2}$ appear singular at the origin $r=0$. However, for any smooth function $u$, a Taylor expansion in Cartesian coordinates reveals that the derivatives of $u$ are related in such a way that these singular terms must cancel perfectly as $r \to 0$ [@problem_id:3452732].

To create a representation that is numerically stable and well-behaved at the origin, one can consider the circular mean of the function, $\overline{u}(r) = \frac{1}{2\pi}\int_{0}^{2\pi} u(r,\theta)\,d\theta$. By expanding $u$ in a Taylor series at the origin and performing the integration, one can derive a remarkable result known as Pizzetti's formula. The series for the circular mean involves only even powers of $r$ and is elegantly expressed using the iterated Laplacian, $\Delta^n = \Delta(\Delta(\dots\Delta u\dots))$:
$$ \overline{u}(r) = \sum_{n=0}^{\infty} \frac{1}{(n!)^2} \left(\frac{r}{2}\right)^{2n} \Delta^n u(0,0) $$
This provides a "stabilized" expansion near the origin, connecting the local behavior of a function to its average properties and higher-order Laplacians [@problem_id:3452732].

#### Impact of Solution Regularity
The entire framework of Taylor-based truncation error analysis rests on a critical assumption: that the solution $u$ is sufficiently smooth. The derivation of a second-order accurate scheme requires that $u$ is at least four times continuously differentiable ($u \in C^4$). In many practical problems, especially in domains with corners or where boundary data is non-smooth, this assumption fails.

Consider a solution to an elliptic PDE on a polygonal domain that has a **[corner singularity](@entry_id:204242)**, such that the solution has limited regularity, for instance, $u \in C^{1,\alpha}$ for some $\alpha \in (0,1)$ but $u \notin C^2$ [@problem_id:3452822]. This means its first derivatives are Hölder continuous, but its second derivatives are not bounded near the corner. In this case, the Taylor expansion cannot be carried out to second or higher orders. Expanding only to first order with a Hölder remainder reveals that the local truncation error of the 5-point Laplacian no longer behaves as $\mathcal{O}(h^2)$. Instead, near the singularity, it degrades significantly, often scaling like $\mathcal{O}(h^{\alpha-1})$. Since $\alpha-1  0$, the pointwise error does not even converge to zero.

While this local inconsistency is severe, the scheme does not necessarily fail to converge globally. Because the singularity is confined to a small region, the error in a global, integral sense (like the $L^2$ norm) is less catastrophic. A rigorous analysis shows that for such problems, the global error of the discrete solution $u_h$ converges to the true solution $u$, but with a reduced order. Typically, the error in the discrete [energy norm](@entry_id:274966) (a discrete version of the $H^1$ norm) scales as $\mathcal{O}(h^\alpha)$, and the error in the discrete $L^2$ norm scales as $\mathcal{O}(h^{1+\alpha})$. This underscores a fundamental principle: the accuracy of a numerical method is ultimately limited not just by the design of the stencil, but by the intrinsic smoothness of the solution it seeks to approximate [@problem_id:3452822].