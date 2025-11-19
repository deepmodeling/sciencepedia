## Introduction
In the landscape of calculus, the derivative stands as a pillar, quantifying the rate of change for single-variable functions. However, when we venture into higher dimensions with functions mapping from $\mathbb{R}^n$ to $\mathbb{R}^m$, the simple notion of a slope becomes inadequate. How can we capture the intricate way a function changes in all directions simultaneously? This challenge is met by the **[total derivative](@entry_id:137587)**, a powerful generalization that replaces the [tangent line](@entry_id:268870) with a tangent linear transformation. This article provides a comprehensive exploration of this fundamental concept. The first chapter, **Principles and Mechanisms**, will build the formal definition of the [total derivative](@entry_id:137587), introduce its concrete representation as the Jacobian matrix, and explore its core properties and rules. Following this, **Applications and Interdisciplinary Connections** will journey through diverse fields like physics, engineering, and machine learning to reveal the [total derivative](@entry_id:137587)'s profound utility in modeling real-world phenomena. Finally, **Hands-On Practices** will offer a set of guided problems to solidify your understanding. We begin by laying the groundwork, defining what it means for a multivariable function to be differentiable.

## Principles and Mechanisms

In single-variable calculus, the derivative of a function at a point is a single number that represents the slope of the [tangent line](@entry_id:268870), encapsulating the function's local rate of change. Extending this concept to functions of multiple variables, $f: \mathbb{R}^n \to \mathbb{R}^m$, requires a more sophisticated object. A single number is no longer sufficient to capture the rates of change in all possible directions. The correct generalization is the **[total derivative](@entry_id:137587)**, a linear transformation that serves as the best [local linear approximation](@entry_id:263289) to the function. This chapter elucidates the formal definition of the [total derivative](@entry_id:137587), its concrete representation as the Jacobian matrix, its fundamental properties, and its profound applications in geometry and science.

### The Definition of Differentiability

The core idea of differentiation is approximation by a simpler function. For a function of one variable, this is approximation by a line. For a function $f: \mathbb{R}^n \to \mathbb{R}^m$, the simplest non-constant functions are [linear transformations](@entry_id:149133). A function $f$ is said to be **differentiable** at a point $\mathbf{a} \in \mathbb{R}^n$ if there exists a linear map $L: \mathbb{R}^n \to \mathbb{R}^m$ such that the change in $f$, $f(\mathbf{a} + \mathbf{h}) - f(\mathbf{a})$, is well-approximated by $L(\mathbf{h})$.

Formally, we say $f$ is differentiable at $\mathbf{a}$ if there exists a linear transformation $L: \mathbb{R}^n \to \mathbb{R}^m$ that satisfies:
$$
\lim_{\mathbf{h} \to \mathbf{0}} \frac{\|f(\mathbf{a} + \mathbf{h}) - f(\mathbf{a}) - L(\mathbf{h})\|}{\|\mathbf{h}\|} = 0
$$
where $\|\cdot\|$ denotes the standard Euclidean norm in the appropriate space. The linear map $L$ is unique and is called the **[total derivative](@entry_id:137587)** or **Fréchet derivative** of $f$ at $\mathbf{a}$, denoted by $Df(\mathbf{a})$. The expression $f(\mathbf{a}) + Df(\mathbf{a})(\mathbf{h})$ is referred to as the **best affine approximation** to $f(\mathbf{a}+\mathbf{h})$ for small displacement vectors $\mathbf{h}$.

This definition is powerful but abstract. Let's explore its meaning. The numerator, $\|f(\mathbf{a} + \mathbf{h}) - f(\mathbf{a}) - Df(\mathbf{a})(\mathbf{h})\|$, is the error in approximating the change in $f$ by the linear map $Df(\mathbf{a})$. The definition demands that this error tends to zero *faster* than the magnitude of the displacement $\|\mathbf{h}\|$.

A simple yet illustrative case is a linear function itself. Consider a linear signal amplifier modeled by the function $f(\mathbf{x}) = A\mathbf{x}$, where $A$ is a constant $m \times n$ matrix [@problem_id:2330076]. Let's test for its derivative at an arbitrary point $\mathbf{x}_0$. We need to find a linear map $L$ that satisfies the definition. Let's compute the change in $f$:
$$
f(\mathbf{x}_0 + \mathbf{h}) - f(\mathbf{x}_0) = A(\mathbf{x}_0 + \mathbf{h}) - A\mathbf{x}_0 = A\mathbf{x}_0 + A\mathbf{h} - A\mathbf{x}_0 = A\mathbf{h}
$$
If we propose the linear map $L(\mathbf{h}) = A\mathbf{h}$, the error term becomes $f(\mathbf{x}_0 + \mathbf{h}) - f(\mathbf{x}_0) - L(\mathbf{h}) = A\mathbf{h} - A\mathbf{h} = \mathbf{0}$. The limit in the definition is then trivially zero. Thus, the [total derivative](@entry_id:137587) of the linear map $f(\mathbf{x}) = A\mathbf{x}$ is the map itself, $Df(\mathbf{x}_0)(\mathbf{h}) = A\mathbf{h}$, for any point $\mathbf{x}_0$. The derivative is constant. A special case is a scalar-valued function $f(x, y) = \alpha x - \beta y + \gamma$ [@problem_id:2330056]. Its derivative is the linear map represented by the row matrix $\begin{pmatrix} \alpha  -\beta \end{pmatrix}$.

The definition of differentiability imposes a strict condition on a function's local behavior. Consider the function $f(\mathbf{x}) = \|\mathbf{x}\|^\alpha$ for $\mathbf{x} \in \mathbb{R}^n$ and $\alpha > 0$ [@problem_id:2330083]. For this function to be differentiable at the origin $\mathbf{0}$, there must be a [linear map](@entry_id:201112) $L$ such that $\lim_{\mathbf{h}\to \mathbf{0}} \frac{|\|\mathbf{h}\|^\alpha - L(\mathbf{h})|}{\|\mathbf{h}\|} = 0$. If such an $L$ exists, it must be the zero map, $L=0$, because the function is symmetric around the origin. The condition then simplifies to $\lim_{\mathbf{h}\to \mathbf{0}} \|\mathbf{h}\|^{\alpha-1} = 0$. This limit is zero if and only if the exponent $\alpha-1$ is positive, meaning $\alpha > 1$. For $\alpha=1$, the function $f(\mathbf{x})=\|\mathbf{x}\|$ (a cone) is not differentiable at the origin. For $0 \lt \alpha \lt 1$, the function is even "sharper" at the origin and fails differentiability more dramatically. This establishes that the set of $\alpha$ for which $f$ is differentiable at the origin is $(1, \infty)$, whose [infimum](@entry_id:140118) is $1$.

### The Jacobian Matrix: A Concrete Representation

The [total derivative](@entry_id:137587) $Df(\mathbf{a})$ is an abstract linear transformation. To perform computations, we need a concrete representation. For [finite-dimensional spaces](@entry_id:151571), any linear map $L: \mathbb{R}^n \to \mathbb{R}^m$ can be represented by an $m \times n$ matrix with respect to the standard bases. The matrix representation of the [total derivative](@entry_id:137587) $Df(\mathbf{a})$ is called the **Jacobian matrix** of $f$ at $\mathbf{a}$, denoted $J_f(\mathbf{a})$.

If $f(\mathbf{x}) = (f_1(\mathbf{x}), f_2(\mathbf{x}), \dots, f_m(\mathbf{x}))$ where $\mathbf{x} = (x_1, x_2, \dots, x_n)$, the entries of the Jacobian matrix are given by the [partial derivatives](@entry_id:146280) of the component functions:
$$
(J_f(\mathbf{a}))_{ij} = \frac{\partial f_i}{\partial x_j}(\mathbf{a})
$$
The Jacobian matrix is thus structured as:
$$
J_f(\mathbf{a}) = \begin{pmatrix}
\frac{\partial f_1}{\partial x_1}(\mathbf{a}) & \frac{\partial f_1}{\partial x_2}(\mathbf{a}) & \cdots & \frac{\partial f_1}{\partial x_n}(\mathbf{a}) \\
\frac{\partial f_2}{\partial x_1}(\mathbf{a}) & \frac{\partial f_2}{\partial x_2}(\mathbf{a}) & \cdots & \frac{\partial f_2}{\partial x_n}(\mathbf{a}) \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial f_m}{\partial x_1}(\mathbf{a}) & \frac{\partial f_m}{\partial x_2}(\mathbf{a}) & \cdots & \frac{\partial f_m}{\partial x_n}(\mathbf{a})
\end{pmatrix}
$$
The action of the [total derivative](@entry_id:137587) on a vector $\mathbf{h}$ is then given by [matrix-vector multiplication](@entry_id:140544): $Df(\mathbf{a})(\mathbf{h}) = J_f(\mathbf{a})\mathbf{h}$.

For a scalar-valued function $f: \mathbb{R}^n \to \mathbb{R}$, the Jacobian is a $1 \times n$ row matrix. This matrix is the transpose of the **[gradient vector](@entry_id:141180)**, $\nabla f$, which is defined as the column vector of [partial derivatives](@entry_id:146280):
$$
\nabla f(\mathbf{a}) = \begin{pmatrix} \frac{\partial f}{\partial x_1}(\mathbf{a}) \\ \vdots \\ \frac{\partial f}{\partial x_n}(\mathbf{a}) \end{pmatrix}, \quad \text{so} \quad J_f(\mathbf{a}) = (\nabla f(\mathbf{a}))^T
$$

**Example:** Consider a transformation from a 2D system $(u, v)$ to a 3D system $(x, y, z)$ given by $\mathbf{f}(u, v) = (u\cos(v), v\sin(u), e^{uv})$ [@problem_id:37775]. Here $f: \mathbb{R}^2 \to \mathbb{R}^3$. The Jacobian matrix will be a $3 \times 2$ matrix. Computing the partial derivatives gives:
$$
\mathbf{J}_{\mathbf{f}}(u, v) = \begin{pmatrix}
\frac{\partial x}{\partial u} & \frac{\partial x}{\partial v} \\
\frac{\partial y}{\partial u} & \frac{\partial y}{\partial v} \\
\frac{\partial z}{\partial u} & \frac{\partial z}{\partial v}
\end{pmatrix}
= \begin{pmatrix}
\cos(v) & -u\sin(v) \\
v\cos(u) & \sin(u) \\
v e^{uv} & u e^{uv}
\end{pmatrix}
$$
Similarly, for a map from $\mathbb{R}^2$ to $\mathbb{R}^2$, such as the [coordinate transformation](@entry_id:138577) $F(x,y) = (x \cos(ay), y \sin(bx))$ [@problem_id:37787], the Jacobian is a $2 \times 2$ matrix:
$$
J_{F}(x,y) = \begin{pmatrix} \cos(ay) & -a x\sin(ay) \\ b y\cos(bx) & \sin(bx) \end{pmatrix}
$$
The determinant of this square Jacobian matrix, $\det(J_F)$, is a crucial quantity that measures how the transformation locally scales areas. For example, for the function $F(x,y) = (\cos(x) \sinh(y), \sin(x) \cosh(y))$, the determinant of its Jacobian evaluates to $\sin^2(x) - \cosh^2(y)$ [@problem_id:2330057].

### Properties and Consequences of Differentiability

The definition of the [total derivative](@entry_id:137587) has several profound consequences that shape multivariable calculus.

**Differentiability implies Continuity:** If a function $f$ is differentiable at a point $\mathbf{a}$, then it must be continuous at $\mathbf{a}$. This can be seen from the definition. The difference $f(\mathbf{a}+\mathbf{h}) - f(\mathbf{a}) = Df(\mathbf{a})(\mathbf{h}) + \text{error}(\mathbf{h})$, where both the linear term and the error term approach $\mathbf{0}$ as $\mathbf{h} \to \mathbf{0}$. Thus, $\lim_{\mathbf{h}\to\mathbf{0}} f(\mathbf{a}+\mathbf{h}) = f(\mathbf{a})$.

**Relationship with Directional Derivatives:** The **directional derivative** of a scalar field $f: \mathbb{R}^n \to \mathbb{R}$ at $\mathbf{a}$ in the direction of a unit vector $\mathbf{u}$ is defined as $D_{\mathbf{u}}f(\mathbf{a}) = \lim_{t\to 0} \frac{f(\mathbf{a}+t\mathbf{u}) - f(\mathbf{a})}{t}$, if the limit exists. If $f$ is differentiable at $\mathbf{a}$, then the [directional derivative](@entry_id:143430) exists in *every* direction $\mathbf{u}$ and is given by the action of the [total derivative](@entry_id:137587) on $\mathbf{u}$:
$$
D_{\mathbf{u}}f(\mathbf{a}) = Df(\mathbf{a})(\mathbf{u}) = \nabla f(\mathbf{a}) \cdot \mathbf{u}
$$
This formula provides a powerful link between the [total derivative](@entry_id:137587) and the rates of change along specific lines. For instance, if the [directional derivatives](@entry_id:189133) of a function at a point are known in two [linearly independent](@entry_id:148207) directions, the [gradient vector](@entry_id:141180) at that point can be uniquely determined, which then allows for the calculation of the directional derivative in any other direction [@problem_id:2330061].

**The Subtlety of Differentiability:** A common misconception is that the existence of all [partial derivatives](@entry_id:146280) (or even all [directional derivatives](@entry_id:189133)) at a point is enough to guarantee differentiability. This is false. Differentiability is a stronger condition. Consider the function [@problem_id:2330087]:
$$
f(x, y) = \begin{cases} \frac{x^2 y}{x^4 + y^2} & \text{if } (x, y) \neq (0, 0) \\ 0 & \text{if } (x, y) = (0, 0) \end{cases}
$$
At the origin, one can calculate that the directional derivative exists for all unit vectors $\mathbf{u}=(a,b)$. In fact, $D_{\mathbf{u}}f(0,0)$ is $a^2/b$ if $b \neq 0$ and $0$ if $b=0$. In particular, the [partial derivatives](@entry_id:146280) (for $\mathbf{u}=(1,0)$ and $\mathbf{u}=(0,1)$) both exist and are zero. However, the function is not even continuous at the origin—approaching along the path $y=mx^2$ gives a limit of $\frac{m}{1+m^2}$, which depends on the path. Since the function is not continuous at the origin, it cannot be differentiable there. This demonstrates that the existence of all [directional derivatives](@entry_id:189133) is not a [sufficient condition](@entry_id:276242) for [differentiability](@entry_id:140863). A similar counterexample is the function $f(x,y) = \frac{xy^2}{x^2+y^4}$ [@problem_id:2330091]. These examples underscore that the [total derivative](@entry_id:137587)'s definition, which accounts for approximation across all directions simultaneously, is the correct and necessary concept for a robust theory of differentiation in higher dimensions.

**A Sufficient Condition for Differentiability:** While the existence of [partial derivatives](@entry_id:146280) is not enough, their continuity is. A cornerstone theorem states that if all [partial derivatives](@entry_id:146280) $\frac{\partial f_i}{\partial x_j}$ exist in an open set containing a point $\mathbf{a}$ and are continuous at $\mathbf{a}$, then $f$ is differentiable at $\mathbf{a}$. A function whose partial derivatives are continuous is called **continuously differentiable**, or of class **$C^1$**. This theorem provides the most common practical method for establishing differentiability.

### The Algebra of Derivatives

Just like in single-variable calculus, there are rules for differentiating combinations of functions. These rules follow directly from the definition of the derivative as a [linear approximation](@entry_id:146101). Let $f, g: \mathbb{R}^n \to \mathbb{R}^m$ be differentiable at $\mathbf{a}$.

**Linearity:** The derivative operator is linear.
*   **Sum Rule:** The sum $f+g$ is differentiable at $\mathbf{a}$, and $D(f+g)(\mathbf{a}) = Df(\mathbf{a}) + Dg(\mathbf{a})$. In terms of Jacobian matrices, $J_{f+g}(\mathbf{a}) = J_f(\mathbf{a}) + J_g(\mathbf{a})$. This property is illustrated by finding the [linear approximation](@entry_id:146101) of a sum of functions [@problem_id:2330046].
*   **Scalar Multiple Rule:** For any scalar $c \in \mathbb{R}$, the function $cf$ is differentiable at $\mathbf{a}$, and $D(cf)(\mathbf{a}) = c \, Df(\mathbf{a})$.

**Product Rule:** For two scalar-valued functions $f, g: \mathbb{R}^n \to \mathbb{R}$, their product $h(\mathbf{x}) = f(\mathbf{x})g(\mathbf{x})$ is differentiable, and its derivative follows a rule analogous to the single-variable case:
$$
Dh(\mathbf{a})(\mathbf{v}) = g(\mathbf{a}) Df(\mathbf{a})(\mathbf{v}) + f(\mathbf{a}) Dg(\mathbf{a})(\mathbf{v})
$$
In terms of gradients, this is $\nabla h(\mathbf{a}) = g(\mathbf{a})\nabla f(\mathbf{a}) + f(\mathbf{a})\nabla g(\mathbf{a})$. This can be used, for example, to find the Jacobian of a profit density function which is a product of market potential and logistics efficiency scalar fields [@problem_id:2330072].

**The Chain Rule:** The [chain rule](@entry_id:147422) is one of the most powerful tools in [multivariable calculus](@entry_id:147547). If $g: \mathbb{R}^p \to \mathbb{R}^n$ is differentiable at $\mathbf{a}$, and $f: \mathbb{R}^n \to \mathbb{R}^m$ is differentiable at $g(\mathbf{a})$, then the [composite function](@entry_id:151451) $h = f \circ g: \mathbb{R}^p \to \mathbb{R}^m$ is differentiable at $\mathbf{a}$, and its derivative is the composition of the individual derivatives:
$$
D(f \circ g)(\mathbf{a}) = Df(g(\mathbf{a})) \circ Dg(\mathbf{a})
$$
In terms of Jacobian matrices, this [composition of linear maps](@entry_id:154187) becomes a matrix product:
$$
J_{f \circ g}(\mathbf{a}) = J_f(g(\mathbf{a})) \, J_g(\mathbf{a})
$$
This rule is indispensable in physics, engineering, and computer graphics, where systems are often described by composing multiple transformations. For example, in generating a texture, one might map parametric coordinates $(u,v)$ to Cartesian coordinates $(x,y)$ via a function $g$, and then map $(x,y)$ to an RGB color via a function $f$. The chain rule allows us to directly calculate the rate of change of color with respect to the initial parameters, e.g., $\frac{\partial R}{\partial u}$, by multiplying the Jacobian matrices [@problem_id:2330075]. Another application involves [coordinate transformations](@entry_id:172727), such as converting Cartesian [partial derivatives](@entry_id:146280) to polar partial derivatives [@problem_id:2330058].

### Geometric and Physical Applications

The [total derivative](@entry_id:137587) is not merely a computational tool; it provides profound insight into the geometry of functions and surfaces.

**Tangent Planes and Linear Approximations:** For a differentiable scalar function $f: \mathbb{R}^2 \to \mathbb{R}$, the graph $z = f(x, y)$ is a surface in $\mathbb{R}^3$. The [total derivative](@entry_id:137587) at a point $(a, b)$ defines the **[tangent plane](@entry_id:136914)** to this surface at the point $(a, b, f(a,b))$. The equation of the tangent plane is the graph of the best affine approximation:
$$
z = f(a,b) + \frac{\partial f}{\partial x}(a,b)(x-a) + \frac{\partial f}{\partial y}(a,b)(y-b)
$$
This plane is the unique plane that "just touches" the surface at the point, representing the local geometry of the surface. Applications include analyzing the local behavior of physical surfaces, like a flexible membrane described by $z(x,y)=\sin(x)\cos(y)$ [@problem_id:2330084]. More generally for vector functions $f: \mathbb{R}^n \to \mathbb{R}^m$, the best affine approximation is given by $L(\mathbf{x}) = f(\mathbf{a}) + J_f(\mathbf{a})(\mathbf{x}-\mathbf{a})$ [@problem_id:2330068].

**Gradients and Level Sets:** A **level set** of a function $F: \mathbb{R}^n \to \mathbb{R}$ is a set of points $\{\mathbf{x} \in \mathbb{R}^n \mid F(\mathbf{x}) = c\}$ for some constant $c$. For $n=2$, these are level curves; for $n=3$, they are [level surfaces](@entry_id:196027). A fundamental geometric property is that the [gradient vector](@entry_id:141180) $\nabla F$ at a point $\mathbf{p}$ on a level set is orthogonal to the [level set](@entry_id:637056) at that point. This means $\nabla F(\mathbf{p})$ is orthogonal to the velocity vector of any smooth curve lying on the [level set](@entry_id:637056) and passing through $\mathbf{p}$ [@problem_id:2330093]. To see this, let $\mathbf{c}(t)$ be such a curve. Then $F(\mathbf{c}(t)) = c$ for all $t$. Differentiating with respect to $t$ using the chain rule gives:
$$
\frac{d}{dt}F(\mathbf{c}(t)) = \nabla F(\mathbf{c}(t)) \cdot \mathbf{c}'(t) = 0
$$
This shows the gradient is orthogonal to the [tangent vector](@entry_id:264836) $\mathbf{c}'(t)$. This principle is crucial in physics, for example, in determining the trajectory of a probe constrained to an isobaric (constant pressure) surface in a storm system [@problem_id:2330093].

**Derivatives on Manifolds:** The concept of [differentiability](@entry_id:140863) can be extended to functions defined on curved surfaces, or **manifolds**, like a sphere. For a function $T$ defined on the unit sphere $S^2 \subset \mathbb{R}^3$, the rate of change in a direction tangent to the sphere cannot be computed using an ambient gradient alone. If $T$ is the restriction of a differentiable ambient function $\tilde{T}: \mathbb{R}^3 \to \mathbb{R}$, the directional derivative of $T$ at a point $p \in S^2$ in a tangent direction $\mathbf{v}$ is given by the dot product of the ambient gradient $\nabla \tilde{T}(p)$ with the tangent vector $\mathbf{v}$. This is equivalent to projecting the ambient gradient onto the tangent plane at $p$ and then taking the dot product. This technique allows us to analyze phenomena constrained to surfaces, such as the temperature variation experienced by a probe on a spherical moon [@problem_id:2330053].

### Higher-Order Derivatives and Advanced Topics

**The Hessian Matrix:** For a twice-differentiable [scalar field](@entry_id:154310) $f: \mathbb{R}^n \to \mathbb{R}$, we can take derivatives of its [partial derivatives](@entry_id:146280). These second-order partial derivatives can be organized into an $n \times n$ matrix called the **Hessian matrix**, $H_f(\mathbf{a})$:
$$
(H_f(\mathbf{a}))_{ij} = \frac{\partial^2 f}{\partial x_i \partial x_j}(\mathbf{a})
$$
The Hessian matrix defines the quadratic part of the function's Taylor expansion around a point $\mathbf{a}$. The change in $f$ can be approximated as:
$$
f(\mathbf{a} + \mathbf{h}) - f(\mathbf{a}) \approx \nabla f(\mathbf{a}) \cdot \mathbf{h} + \frac{1}{2} \mathbf{h}^T H_f(\mathbf{a}) \mathbf{h}
$$
The Hessian is fundamental to optimization problems, as it is used to classify critical points (as local minima, maxima, or [saddle points](@entry_id:262327)) by analyzing the definiteness of this [quadratic form](@entry_id:153497) [@problem_id:2330069].

**Symmetry of Mixed Partials:** For a function of class $C^2$ (twice continuously differentiable), the order of differentiation does not matter. This is **Clairaut's Theorem**:
$$
\frac{\partial^2 f}{\partial x_i \partial x_j} = \frac{\partial^2 f}{\partial x_j \partial x_i}
$$
This implies that the Hessian matrix of a $C^2$ function is always a symmetric matrix. This property can have surprising consequences. For example, if the gradient of a function $f(x,y)$ has the form $\nabla f(x,y) = (P(y), Q(x))$, Clairaut's theorem implies $P'(y) = Q'(x)$. Since the left side depends only on $y$ and the right side only on $x$, both must be equal to a constant, which severely constrains the form of the function $f$ [@problem_id:2330074].

**Differentiation in Abstract Spaces:** The definition of the Fréchet derivative is not limited to functions on $\mathbb{R}^n$. It applies to functions between any two [normed vector spaces](@entry_id:274725). A prime example is [matrix calculus](@entry_id:181100). Consider the space $M_n(\mathbb{R})$ of $n \times n$ matrices and the function $f(X) = X^{-1}$ defined on the set of [invertible matrices](@entry_id:149769) $GL(n, \mathbb{R})$. One can show that this map is differentiable, and its derivative at an invertible matrix $A$ acting on a "displacement" matrix $H$ is given by [@problem_id:2330048]:
$$
Df(A)(H) = -A^{-1}HA^{-1}
$$
This elegant result is crucial in areas like optimization on matrix manifolds, [perturbation theory](@entry_id:138766), and physics. It highlights the power and generality of the [total derivative](@entry_id:137587) as the unifying concept of differentiation.