## Introduction
Quasi-Newton methods represent a cornerstone of modern [nonlinear optimization](@entry_id:143978), offering a powerful compromise between the rapid convergence of Newton's method and the simplicity of [gradient descent](@entry_id:145942). By avoiding the explicit computation of the expensive and often intractable Hessian matrix, these algorithms have become indispensable tools across science and engineering. At the heart of this family lie the DFP (Davidon-Fletcher-Powell) and BFGS (Broyden-Fletcher-Goldfarb-Shanno) update formulas, which provide an elegant mechanism for building and refining an approximation of the function's curvature with each step. This article bridges the theory and practice of these celebrated methods.

Over the next chapters, you will gain a comprehensive understanding of how these algorithms work.
- The **Principles and Mechanisms** chapter will derive the DFP and BFGS formulas from first principles, including the [secant condition](@entry_id:164914) and the least-change principle. We will explore their remarkable duality, their place within the unified Broyden family, and the crucial stability conditions that ensure their success.
- In **Applications and Interdisciplinary Connections**, we will see these methods in action, exploring their role as workhorse optimizers in machine learning, large-scale computational science, data assimilation, and robotics, with a special focus on the highly effective L-BFGS variant.
- Finally, the **Hands-On Practices** section provides an opportunity to solidify your understanding by working through concrete numerical examples that highlight the practical performance differences between DFP and BFGS.

We begin by examining the fundamental [secant condition](@entry_id:164914) that forms the basis for all quasi-Newton updates.

## Principles and Mechanisms

Following the introduction to quasi-Newton methods as a powerful class of algorithms for [unconstrained optimization](@entry_id:137083), this chapter delves into the principles that govern their construction and the specific mechanisms of the most celebrated update formulas: the Davidon-Fletcher-Powell (DFP) and Broyden-Fletcher-Goldfarb-Shanno (BFGS) methods. We will derive these methods from fundamental concepts, explore their intimate relationship, and analyze the conditions required for their successful and stable implementation.

### The Secant Condition: The Core of Quasi-Newton Methods

Quasi-Newton methods are designed to mimic Newton's method for minimizing a function $f(\mathbf{x})$ without computing the true Hessian matrix, $\nabla^2 f(\mathbf{x})$. Recall that the Newton step $\mathbf{p}_k$ is found by solving the linear system $\nabla^2 f(\mathbf{x}_k) \mathbf{p}_k = -\nabla f(\mathbf{x}_k)$. A quasi-Newton method replaces the true Hessian $\nabla^2 f(\mathbf{x}_k)$ with an approximation, which we will denote as $B_k$. The step is then computed as $\mathbf{p}_k = -B_k^{-1} \nabla f(\mathbf{x}_k)$. After taking a step, $\mathbf{x}_{k+1} = \mathbf{x}_k + \mathbf{s}_k$ (where $\mathbf{s}_k = \alpha_k \mathbf{p}_k$ for some step length $\alpha_k$), we gain new information about the function's curvature. The central challenge is to use this information to update $B_k$ to a new, better approximation $B_{k+1}$.

The fundamental principle guiding this update is the **[secant condition](@entry_id:164914)**. To understand its origin, let us consider a first-order Taylor expansion of the gradient $\nabla f$ around $\mathbf{x}_{k+1}$. For a point $\mathbf{x}$ near $\mathbf{x}_{k+1}$, we have:
$$
\nabla f(\mathbf{x}) \approx \nabla f(\mathbf{x}_{k+1}) + \nabla^2 f(\mathbf{x}_{k+1}) (\mathbf{x} - \mathbf{x}_{k+1})
$$
If we evaluate this approximation at the previous point $\mathbf{x} = \mathbf{x}_k$, we get:
$$
\nabla f(\mathbf{x}_k) \approx \nabla f(\mathbf{x}_{k+1}) + \nabla^2 f(\mathbf{x}_{k+1}) (\mathbf{x}_k - \mathbf{x}_{k+1})
$$
Rearranging this gives an approximation for the change in the gradient:
$$
\nabla f(\mathbf{x}_{k+1}) - \nabla f(\mathbf{x}_k) \approx \nabla^2 f(\mathbf{x}_{k+1}) (\mathbf{x}_{k+1} - \mathbf{x}_k)
$$
Let us define the step vector as $\mathbf{s}_k = \mathbf{x}_{k+1} - \mathbf{x}_k$ and the gradient difference vector as $\mathbf{y}_k = \nabla f(\mathbf{x}_{k+1}) - \nabla f(\mathbf{x}_k)$. The relationship becomes $\mathbf{y}_k \approx \nabla^2 f(\mathbf{x}_{k+1}) \mathbf{s}_k$. More formally, the [fundamental theorem of calculus](@entry_id:147280) gives an exact relationship involving an integral of the Hessian:
$$
\mathbf{y}_k = \left( \int_0^1 \nabla^2 f(\mathbf{x}_k + \tau \mathbf{s}_k) \, d\tau \right) \mathbf{s}_k
$$
Quasi-Newton methods enforce a simplified version of this relationship. They require the *new* Hessian approximation, $B_{k+1}$, to satisfy the equation exactly for the most recent step:
$$
B_{k+1} \mathbf{s}_k = \mathbf{y}_k
$$
This is the celebrated **[secant condition](@entry_id:164914)**, or [secant equation](@entry_id:164522) . It ensures that the quadratic model of the function corresponding to $B_{k+1}$ correctly reproduces the observed change in the gradient along the direction of the last step, $\mathbf{s}_k$. It is a first-order consistency requirement that aligns the model with the most recent measurement of the function's behavior.

It is crucial to recognize that the [secant condition](@entry_id:164914) provides only $n$ [linear constraints](@entry_id:636966) on the elements of the $n \times n$ matrix $B_{k+1}$. If we also require $B_{k+1}$ to be symmetric, it has $\frac{n(n+1)}{2}$ degrees of freedom. For any dimension $n > 1$, this system is underdetermined, meaning there are infinitely many matrices $B_{k+1}$ that satisfy the [secant equation](@entry_id:164522) . This is in contrast to the one-dimensional [secant method](@entry_id:147486), where the condition uniquely defines the new approximation of the derivative. To define a unique update formula in higher dimensions, we need additional principles.

### Uniqueness Through the Least-Change Principle

To resolve the underdetermined nature of the [secant condition](@entry_id:164914), we introduce a sensible guiding principle: the new approximation $B_{k+1}$ should be a minimal modification of the current approximation $B_k$. The idea is that $B_k$ contains accumulated knowledge about the function's curvature from all previous steps, and we should preserve this information as much as possible, making only the necessary changes to satisfy the new information embodied in the [secant equation](@entry_id:164522).

This is formalized as the **least-change principle**. It states that among all symmetric matrices that satisfy the [secant condition](@entry_id:164914), we should choose the one that is closest to the current matrix $B_k$ . The notion of "closeness" is defined by a [matrix norm](@entry_id:145006). The optimization problem can be stated as:
$$
\min_{B} \| B - B_k \| \quad \text{subject to} \quad B = B^\top \text{ and } B \mathbf{s}_k = \mathbf{y}_k
$$
Different quasi-Newton formulas arise from different choices of the [matrix norm](@entry_id:145006). The DFP and BFGS formulas are derived by solving this problem using a specific weighted Frobenius norm. This principle provides a rigorous foundation for deriving unique update formulas that are not just arbitrary but are, in a specific sense, the most conservative and information-preserving. The resulting updates for DFP and BFGS are **rank-two updates**, meaning the correction matrix $B_{k+1} - B_k$ has a rank of two. This is in contrast to simpler updates like the Symmetric Rank-One (SR1) formula, which, as its name suggests, applies a rank-one correction .

### The Davidon-Fletcher-Powell (DFP) Update

The DFP update, one of the first and most influential quasi-Newton formulas, is typically expressed as an update for the *inverse* Hessian approximation, which we denote by $H_k = B_k^{-1}$. This is computationally convenient because it allows for direct calculation of the search direction $\mathbf{p}_k = -H_k \nabla f(\mathbf{x}_k)$ without solving a linear system.

To derive the [secant condition](@entry_id:164914) for the inverse Hessian, we start with the standard form $B_{k+1} \mathbf{s}_k = \mathbf{y}_k$. Assuming $B_{k+1}$ is invertible, we can left-multiply by its inverse $H_{k+1}$:
$$
H_{k+1} (B_{k+1} \mathbf{s}_k) = H_{k+1} \mathbf{y}_k
$$
$$
(H_{k+1} B_{k+1}) \mathbf{s}_k = H_{k+1} \mathbf{y}_k
$$
$$
I \mathbf{s}_k = H_{k+1} \mathbf{y}_k
$$
This gives us the **inverse [secant equation](@entry_id:164522)**, which the DFP update is designed to satisfy :
$$
H_{k+1} \mathbf{y}_k = \mathbf{s}_k
$$
The DFP update formula, which arises from applying the least-change principle to $H_k$, is a rank-two update given by:
$$
H_{k+1}^{\text{DFP}} = H_k + \frac{\mathbf{s}_k \mathbf{s}_k^\top}{\mathbf{s}_k^\top \mathbf{y}_k} - \frac{H_k \mathbf{y}_k \mathbf{y}_k^\top H_k}{\mathbf{y}_k^\top H_k \mathbf{y}_k}
$$
The first correction term, $\frac{\mathbf{s}_k \mathbf{s}_k^\top}{\mathbf{s}_k^\top \mathbf{y}_k}$, is a [rank-one matrix](@entry_id:199014) that ensures the inverse [secant equation](@entry_id:164522) is met. The second term, $-\frac{H_k \mathbf{y}_k \mathbf{y}_k^\top H_k}{\mathbf{y}_k^\top H_k \mathbf{y}_k}$, is also a [rank-one matrix](@entry_id:199014) that serves to maintain symmetry and other desirable properties.

### The Broyden-Fletcher-Goldfarb-Shanno (BFGS) Update

The BFGS update is arguably the most successful and widely used quasi-Newton method. It is typically expressed as an update for the direct Hessian approximation $B_k$:
$$
B_{k+1}^{\text{BFGS}} = B_k + \frac{\mathbf{y}_k \mathbf{y}_k^\top}{\mathbf{y}_k^\top \mathbf{s}_k} - \frac{B_k \mathbf{s}_k \mathbf{s}_k^\top B_k}{\mathbf{s}_k^\top B_k \mathbf{s}_k}
$$
Like DFP, the BFGS update is also a rank-two correction . It is constructed to directly satisfy the [secant equation](@entry_id:164522) $B_{k+1} \mathbf{s}_k = \mathbf{y}_k$. Although it updates $B_k$, the search direction is still found by solving $B_k \mathbf{p}_k = -\nabla f(\mathbf{x}_k)$ or by updating the inverse $H_k$ using the corresponding BFGS inverse formula.

Although the DFP and BFGS formulas appear similar, they produce different sequences of approximations. To illustrate this, consider a hypothetical first step from an initial approximation $B_0 = I$, with a step vector $\mathbf{s}_0 = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$ and gradient change $\mathbf{y}_0 = \begin{pmatrix} -1 \\ 1 \end{pmatrix}$. A direct calculation yields distinct matrices for the next Hessian approximation :
$$
B_{1}^{\text{BFGS}} = \begin{pmatrix} 1.8  & -1.4 \\ -1.4  & 1.2 \end{pmatrix} \quad \text{and} \quad B_{1}^{\text{DFP}} = \begin{pmatrix} 9  & -5 \\ -5  & 3 \end{pmatrix}
$$
This demonstrates that the choice of update formula has a tangible impact on the trajectory of the optimization algorithm.

### The Duality between DFP and BFGS

A remarkable and elegant property connecting DFP and BFGS is **duality**. A close inspection of the two update formulas reveals a deep symmetry. The BFGS formula for the direct Hessian $B_k$ can be obtained directly from the DFP formula for the inverse Hessian $H_k$ by making the following substitutions :
1.  Replace the inverse Hessian approximation $H_k$ with the direct Hessian approximation $B_k$.
2.  Swap the roles of the vectors $\mathbf{s}_k$ and $\mathbf{y}_k$.

Let's see this in action. Starting with the DFP formula for $H_k$:
$$
H_{k+1}^{\text{DFP}} = H_k + \frac{\mathbf{s}_k \mathbf{s}_k^\top}{\mathbf{s}_k^\top \mathbf{y}_k} - \frac{H_k \mathbf{y}_k \mathbf{y}_k^\top H_k}{\mathbf{y}_k^\top H_k \mathbf{y}_k}
$$
Performing the substitutions ($H_k \to B_k$, $\mathbf{s}_k \leftrightarrow \mathbf{y}_k$), we get:
$$
B_{k+1} = B_k + \frac{\mathbf{y}_k \mathbf{y}_k^\top}{\mathbf{y}_k^\top \mathbf{s}_k} - \frac{B_k \mathbf{s}_k \mathbf{s}_k^\top B_k}{\mathbf{s}_k^\top B_k \mathbf{s}_k}
$$
This is precisely the BFGS update formula for $B_k$. Because of this duality, BFGS is sometimes referred to as the "dual DFP" update. This relationship is not just a cosmetic similarity; it can be proven rigorously. Using the **Sherman-Morrison-Woodbury formula** for [matrix inversion](@entry_id:636005), one can derive the BFGS update for $B_k$ by algebraically inverting the DFP update formula for $H_k$ . Duality implies that any theoretical property of one method can be translated into a corresponding property for the other.

This duality also means we can write the BFGS update for the inverse Hessian $H_k$ by applying the dual transformation to the DFP update for the direct Hessian $B_k$. The result is:
$$
H_{k+1}^{\text{BFGS}} = H_k + \left(1 + \frac{\mathbf{y}_k^\top H_k \mathbf{y}_k}{\mathbf{s}_k^\top \mathbf{y}_k}\right) \frac{\mathbf{s}_k \mathbf{s}_k^\top}{\mathbf{s}_k^\top \mathbf{y}_k} - \frac{\mathbf{s}_k \mathbf{y}_k^\top H_k + H_k \mathbf{y}_k \mathbf{s}_k^\top}{\mathbf{s}_k^\top \mathbf{y}_k}
$$
This form is often used in implementations to avoid solving a linear system at each step.

### Unification: The Broyden Family of Updates

The duality between DFP and BFGS suggests they are two poles of a larger continuum. This continuum is captured by the **Broyden family** of updates, which defines a spectrum of rank-two quasi-Newton methods parameterized by a scalar $\phi$. The update for the inverse Hessian $H_k$ can be written as a convex combination of the DFP and BFGS updates:
$$
H_{k+1}^{\phi} = (1-\phi) H_{k+1}^{\text{DFP}} + \phi H_{k+1}^{\text{BFGS}}
$$
A more common representation is :
$$
H_{k+1}^{\phi} = H_{k+1}^{\text{DFP}} + \phi (\mathbf{y}_k^\top H_k \mathbf{y}_k) \mathbf{w}_k \mathbf{w}_k^\top \quad \text{where} \quad \mathbf{w}_k = \left( \frac{\mathbf{s}_k}{\mathbf{s}_k^\top \mathbf{y}_k} - \frac{H_k \mathbf{y}_k}{\mathbf{y}_k^\top H_k \mathbf{y}_k} \right)
$$
In this formulation, setting $\phi=0$ recovers the DFP update formula. Setting $\phi=1$ recovers the BFGS update formula . This elegant unification shows that DFP and BFGS are not entirely disparate algorithms but are siblings within a larger class of methods that satisfy the [secant equation](@entry_id:164522).

### The Curvature Condition and Preservation of Positive Definiteness

For a quasi-Newton method to be effective, the search direction $\mathbf{p}_k = -B_k^{-1} \nabla f(\mathbf{x}_k)$ must be a **descent direction**, meaning it must make an angle of more than 90 degrees with the gradient vector. This ensures that a small step along $\mathbf{p}_k$ will decrease the function value. This condition, $\nabla f(\mathbf{x}_k)^\top \mathbf{p}_k  0$, is guaranteed if the Hessian approximation $B_k$ (and thus its inverse $H_k$) is **[positive definite](@entry_id:149459)**.

A crucial question, therefore, is: if we start with a [positive definite matrix](@entry_id:150869) $B_k$ (e.g., $B_0=I$), what conditions must be met for the updated matrix $B_{k+1}$ to also be positive definite? The answer lies in the **curvature condition**:
$$
\mathbf{s}_k^\top \mathbf{y}_k > 0
$$
This condition has a clear geometric interpretation. Recalling that $\mathbf{y}_k = \nabla f(\mathbf{x}_{k+1}) - \nabla f(\mathbf{x}_k)$, the condition can be written as $\mathbf{s}_k^\top \nabla f(\mathbf{x}_{k+1}) > \mathbf{s}_k^\top \nabla f(\mathbf{x}_k)$. Since $\mathbf{s}_k$ points from $\mathbf{x}_k$ to $\mathbf{x}_{k+1}$, this means the directional derivative along the step direction must be less negative (i.e., larger) at the new point than at the old point. This indicates that the function's surface is curving upwards in the direction of the step, which is the behavior we expect when approaching a minimizer.

It is a cornerstone theorem of quasi-Newton methods that for the entire Broyden family (including DFP and BFGS), the updated matrix $B_{k+1}$ is positive definite if and only if $B_k$ is positive definite and the curvature condition $\mathbf{s}_k^\top \mathbf{y}_k > 0$ is satisfied .

How do we ensure this condition holds in practice? This is a primary function of the [line search algorithm](@entry_id:139123). Inexact line searches that satisfy the **Wolfe conditions** are designed precisely for this purpose. The second Wolfe condition (the curvature condition) requires that the step length $\alpha_k$ satisfies:
$$
\nabla f(\mathbf{x}_k + \alpha_k \mathbf{p}_k)^\top \mathbf{p}_k \ge c_2 \nabla f(\mathbfx}_k)^\top \mathbf{p}_k
$$
for some constant $c_2 \in (0,1)$. Since $\mathbf{s}_k = \alpha_k \mathbf{p}_k$, this directly implies $\mathbf{y}_k^\top \mathbf{s}_k = \alpha_k (\nabla f(\mathbf{x}_{k+1}) - \nabla f(\mathbf{x}_k))^\top \mathbf{p}_k \ge \alpha_k (c_2 - 1) \nabla f(\mathbf{x}_k)^\top \mathbf{p}_k$. Because $\alpha_k > 0$, $c_2  1$, and $\nabla f(\mathbf{x}_k)^\top \mathbf{p}_k  0$ for a descent direction, the right-hand side is strictly positive. Thus, a Wolfe line search automatically generates steps that satisfy the curvature condition, thereby guaranteeing that DFP and BFGS maintain positive definite Hessian approximations throughout the optimization process . This synergy between the update formula and the line search is critical for the robustness and theoretical convergence of the methods.

### Practical Performance and Advanced Stability Considerations

While DFP and BFGS share a common theoretical foundation, their practical performance differs significantly. Over decades of numerical experimentation, the **BFGS method has proven to be substantially more robust and efficient than DFP** . BFGS is generally less sensitive to the accuracy of the [line search](@entry_id:141607) and exhibits superior self-correcting properties when the Hessian approximations become poor. For these reasons, BFGS is the default quasi-Newton method used in nearly all modern optimization software.

The sources of DFP's poorer performance are subtle and relate to its [numerical stability](@entry_id:146550). One issue arises from the denominator $\mathbf{y}_k^\top H_k \mathbf{y}_k$ in its update formula. If the inverse Hessian approximation $H_k$ becomes ill-conditioned, it is possible for the vector $H_k \mathbf{y}_k$ to become nearly orthogonal to $\mathbf{y}_k$, causing the denominator to be numerically very close to zero even when it is theoretically positive. This can lead to catastrophic cancellation errors in [finite-precision arithmetic](@entry_id:637673) . While BFGS is not immune to numerical issues, it is observed to be far less susceptible to this type of degradation.

A more fundamental challenge arises when optimizing non-[convex functions](@entry_id:143075), where the true Hessian may not be [positive definite](@entry_id:149459). In such regions, it is possible for a step to yield a negative curvature, $\mathbf{s}_k^\top \mathbf{y}_k \le 0$. As established, this will cause both DFP and BFGS to lose [positive definiteness](@entry_id:178536), and the algorithm may fail. Consider, for example, the function $f(\mathbf{x}) = x_1^2 - x_2^2$, which has a saddle point at the origin. A step in the $x_2$ direction results in negative curvature, and a standard BFGS or DFP update with $H_k = I$ would produce a non-[positive-definite matrix](@entry_id:155546) $H_{k+1}$ .

To handle this, practical implementations incorporate safeguards. A simple strategy is to simply skip the update if $\mathbf{s}_k^\top \mathbf{y}_k \le 0$, reusing $B_k$ for the next iteration. A more sophisticated approach, known as **Powell's damped BFGS update**, modifies the $\mathbf{y}_k$ vector itself. Instead of using $\mathbf{y}_k$, the update is performed with a modified vector $\bar{\mathbf{y}}_k$:
$$
\bar{\mathbf{y}}_k = \theta \mathbf{y}_k + (1-\theta) B_k \mathbf{s}_k
$$
The [damping parameter](@entry_id:167312) $\theta \in [0,1]$ is chosen to enforce a positive curvature condition, for example, $\mathbf{s}_k^\top \bar{\mathbf{y}}_k = c \, \mathbf{s}_k^\top B_k \mathbf{s}_k$ for some small constant $c \in (0,1)$. If $\mathbf{s}_k^\top \mathbf{y}_k$ is already sufficiently positive, one can choose $\theta=1$. If not, $\theta$ is calculated as :
$$
\theta = \frac{(1-c) \mathbf{s}_k^\top B_k \mathbf{s}_k}{\mathbf{s}_k^\top B_k \mathbf{s}_k - \mathbf{s}_k^\top \mathbf{y}_k}
$$
This procedure effectively mixes the observed gradient change $\mathbf{y}_k$ with the change predicted by the current model, $B_k \mathbf{s}_k$, to construct a new vector $\bar{\mathbf{y}}_k$ that exhibits [positive curvature](@entry_id:269220) while deviating minimally from the true measurement. Such stabilization techniques are essential for applying quasi-Newton methods to the complex, non-convex problems frequently encountered in science and engineering.