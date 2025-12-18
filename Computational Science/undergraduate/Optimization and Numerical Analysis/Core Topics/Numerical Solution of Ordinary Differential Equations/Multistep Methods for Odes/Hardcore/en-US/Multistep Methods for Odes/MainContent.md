## Introduction
When [solving ordinary differential equations](@entry_id:635033) (ODEs) numerically, the most intuitive approaches are [one-step methods](@entry_id:636198), which advance the solution using only information from the current point in time. However, a more powerful class of techniques, known as [linear multistep methods](@entry_id:139528) (LMMs), leverages a "memory" of several past solution points to achieve greater accuracy and computational efficiency. This reliance on historical data is their greatest strength, but it also introduces unique challenges related to stability and initialization that are not present in simpler methods. This article provides a comprehensive guide to understanding and applying these essential numerical tools.

Throughout this guide, you will journey from foundational theory to practical application. The first chapter, **Principles and Mechanisms**, will deconstruct the general formula of LMMs and introduce the critical theoretical pillars of consistency and [zero-stability](@entry_id:178549), which together form Dahlquist's Equivalence Theorem for convergence. We will also explore advanced stability concepts like A-stability, which are vital for tackling a challenging class of problems. The second chapter, **Applications and Interdisciplinary Connections**, shifts focus to the practitioner's perspective, exploring how to choose between methods, the power of [predictor-corrector schemes](@entry_id:637533), and the indispensable role of LMMs in solving [stiff systems](@entry_id:146021) across science and engineering. Finally, in **Hands-On Practices**, you will have the opportunity to apply this knowledge to solve concrete problems, reinforcing your understanding of these versatile methods.

## Principles and Mechanisms

While [one-step methods](@entry_id:636198) for [solving ordinary differential equations](@entry_id:635033) (ODEs) compute the next state approximation, $y_{n+1}$, using only information from the current state, $(t_n, y_n)$, a vast and powerful class of methods known as **[linear multistep methods](@entry_id:139528) (LMMs)** leverages a longer history of the solution to achieve higher efficiency. The fundamental distinction lies in the "memory" of the method; [one-step methods](@entry_id:636198) are memoryless concerning past solution points, whereas [multistep methods](@entry_id:147097) explicitly utilize a sequence of previous approximations to advance the solution . This reliance on past data allows for the construction of highly accurate and efficient schemes, but it also introduces new theoretical complexities regarding their stability and convergence.

### The General Form of Linear Multistep Methods

A [linear multistep method](@entry_id:751318) is defined by a [difference equation](@entry_id:269892) that connects several consecutive solution approximations. For an initial value problem $y'(t) = f(t, y(t))$, a general **$k$-step LMM** is given by the formula:

$$ \sum_{j=0}^{k} \alpha_j y_{n+j} = h \sum_{j=0}^{k} \beta_j f_{n+j} $$

Here, $h$ is the constant step size, $y_{n+j}$ is the [numerical approximation](@entry_id:161970) of the solution $y(t)$ at time $t_{n+j} = t_0 + (n+j)h$, and $f_{n+j}$ is an abbreviation for the derivative evaluation $f(t_{n+j}, y_{n+j})$. The constants $\alpha_j$ and $\beta_j$ are real coefficients that uniquely define a specific method. By convention, the method is normalized such that $\alpha_k = 1$. The integer $k$ is the **step number** of the method, indicating it requires information from $k$ previous points to compute the next value.

For instance, consider the method given by the formula $y_{n+2} + 3y_n = 4y_{n+1} - 2h f_{n+1}$. To analyze it within the standard framework, we rearrange it to match the general form:

$$ y_{n+2} - 4y_{n+1} + 3y_n = h (0 \cdot f_{n+2} - 2f_{n+1} + 0 \cdot f_n) $$

By comparing this to the general equation, we can identify this as a $2$-step method ($k=2$) with coefficients $\alpha_2=1, \alpha_1=-4, \alpha_0=3$ and $\beta_2=0, \beta_1=-2, \beta_0=0$ .

A critical classification of LMMs is based on the coefficient $\beta_k$:

*   **Explicit Methods**: If $\beta_k = 0$, the formula for $y_{n+k}$ does not involve $f_{n+k} = f(t_{n+k}, y_{n+k})$. The right-hand side of the equation depends only on previously computed values. Thus, $y_{n+k}$ can be calculated directly.

*   **Implicit Methods**: If $\beta_k \neq 0$, the unknown value $y_{n+k}$ appears on both sides of the equation (once on the left, and implicitly within $f_{n+k}$ on the right). This creates an equation, often nonlinear, that must be solved for $y_{n+k}$ at each time step, typically using a [root-finding algorithm](@entry_id:176876) like Newton's method.

For example, the well-known **trapezoidal rule**, $y_{n+1} = y_n + \frac{h}{2}(f_{n+1} + f_n)$, is an **implicit, 1-step** method. It is implicit because $y_{n+1}$ appears within the $f_{n+1}$ term, and it is 1-step because it only uses information from the single previous point, $y_n$ . While computationally more demanding per step, [implicit methods](@entry_id:137073) often possess superior stability properties, making them indispensable for certain types of problems.

A practical challenge for any $k$-step method with $k>1$ is the **startup problem**. To compute $y_k$ using the LMM, we need the $k$ preceding values $y_0, y_1, \ldots, y_{k-1}$. However, an initial value problem only provides $y_0$. The necessary additional starting values, $y_1, \ldots, y_{k-1}$, must be generated by another means. This is typically done using a one-step method, such as a Runge-Kutta method, of at least the same order as the LMM to ensure the overall accuracy is not compromised .

### Derivation and Order of Accuracy

The coefficients $\alpha_j$ and $\beta_j$ are not arbitrary; they are carefully chosen to ensure the method accurately approximates the true solution. A powerful technique for deriving these coefficients is the **[method of undetermined coefficients](@entry_id:165061)**, where we require the method to be exact for polynomials up to the highest possible degree.

A method is defined as "exact" for a function $y(t)$ if, assuming all past values are on the true solution curve (i.e., $y_{n+j} = y(t_{n+j})$ for $j  k$), the formula produces the exact next value, $y_{n+k} = y(t_{n+k})$. Let's derive the coefficients for a two-step explicit method of the form:

$$ y_{n+1} = y_n + h (b_1 f_n + b_0 f_{n-1}) $$

Here, we correspond $y_{n+1}$ with the highest index $y_{n+k}$, so we shift the indices of the general form. This is equivalent to setting $n \to n-1$ in the general form, resulting in $y_{n+1} = -\sum_{j=0}^{1} \frac{\alpha_j}{\alpha_2} y_{n+j-1} + h \sum_{j=0}^{1} \frac{\beta_j}{\alpha_2} f_{n+j-1}$. This is a common representation for Adams-type methods. For our method, the underlying recurrence is $y_{n+1} - y_n = h(b_1 f_n + b_0 f_{n-1})$.

We [test for exactness](@entry_id:168683) with monomials $y(t) = t^p$. For simplicity, let $t_n=0$, so $t_{n+1}=h$ and $t_{n-1}=-h$. The [exactness](@entry_id:268999) condition is $y(t_{n+1}) = y(t_n) + h(b_1 y'(t_n) + b_0 y'(t_{n-1}))$.

1.  **Exactness for $y(t)=1$ (degree 0):** $y'(t)=0$. The condition becomes $1 = 1 + h(0)$, which is always true.
2.  **Exactness for $y(t)=t$ (degree 1):** $y'(t)=1$. The condition is $t_{n+1} = t_n + h(b_1 \cdot 1 + b_0 \cdot 1)$, which simplifies to $h = 0 + h(b_1+b_0)$, yielding our first equation: $b_1+b_0=1$.
3.  **Exactness for $y(t)=t^2$ (degree 2):** $y'(t)=2t$. The condition is $t_{n+1}^2 = t_n^2 + h(b_1 \cdot 2t_n + b_0 \cdot 2t_{n-1})$, which simplifies to $h^2 = 0 + h(b_1 \cdot 0 + b_0 \cdot 2(-h))$. This gives $h^2 = -2b_0h^2$, yielding our second equation: $b_0 = -1/2$.

Solving this system gives $b_0 = -1/2$ and $b_1 = 3/2$. The resulting method is the well-known second-order **Adams-Bashforth method**:

$$ y_{n+1} = y_n + h \left( \frac{3}{2} f_n - \frac{1}{2} f_{n-1} \right) $$

This method is exact for polynomials up to degree 2. It is not exact for $y(t)=t^3$, so its **[order of accuracy](@entry_id:145189)** is $p=2$ . In general, a method has order $p$ if its [local truncation error](@entry_id:147703), the error made in a single step assuming the past was exact, is $O(h^{p+1})$.

### The Theory of Convergence: Dahlquist's Equivalence Theorem

The ultimate goal of a numerical method is **convergence**: for any fixed time $T$, the [numerical approximation](@entry_id:161970) $y_n$ at $t_n=T$ must approach the true solution $y(T)$ as the step size $h \to 0$. For [linear multistep methods](@entry_id:139528), this property is governed by one of the most fundamental results in numerical analysis, **Dahlquist's Equivalence Theorem**. The theorem states that convergence is not a monolithic property but is equivalent to two simpler, independent, and algebraically verifiable conditions: **consistency** and **[zero-stability](@entry_id:178549)** .

 **Dahlquist's Equivalence Theorem:** A [linear multistep method](@entry_id:751318) is convergent if and only if it is consistent and zero-stable.

This theorem is profound because it decouples the analysis of convergence. Consistency ensures the [difference equation](@entry_id:269892) faithfully represents the differential equation in the limit $h \to 0$. Zero-stability ensures that the numerical scheme itself is stable and does not allow for the amplification of errors. We now examine each of these conditions in detail.

#### Consistency: Faithfulness to the ODE

A method is consistent if it accurately reflects the differential equation as the step size becomes infinitesimally small. This property can be checked using two **characteristic polynomials** derived from the method's coefficients:

*   **First Characteristic Polynomial:** $\rho(z) = \sum_{j=0}^{k} \alpha_j z^j$
*   **Second Characteristic Polynomial:** $\sigma(z) = \sum_{j=0}^{k} \beta_j z^j$

A [linear multistep method](@entry_id:751318) is **consistent** if and only if the following two conditions hold:

1.  $\rho(1) = 0$
2.  $\rho'(1) = \sigma(1)$

The first condition, $\rho(1)=0$, can be understood by considering the trivial ODE $y'(t)=0$, whose solution is $y(t)=C$. For the method to be exact for this case, it must hold that $\sum \alpha_j C = h \sum \beta_j \cdot 0$, which simplifies to $C \sum \alpha_j = 0$, or $\rho(1)=0$. The second condition, $\rho'(1)=\sigma(1)$, arises from requiring the method to be exact for $y(t)=t$, ensuring it correctly captures linear behavior, which is the local nature of any differentiable function. A method satisfying these conditions is said to have at least order 1.

For example, let's determine the value of $\gamma$ that makes the method $y_{n+2} - y_{n+1} = h (\gamma f_{n+2} + \frac{2}{3} f_{n+1} - \frac{1}{12} f_{n})$ consistent. Here, the coefficients are $\alpha_2=1, \alpha_1=-1, \alpha_0=0$ and $\beta_2=\gamma, \beta_1=2/3, \beta_0=-1/12$. The characteristic polynomials are:

$$ \rho(z) = z^2 - z \quad \text{and} \quad \sigma(z) = \gamma z^2 + \frac{2}{3}z - \frac{1}{12} $$

We check the [consistency conditions](@entry_id:637057):
1.  $\rho(1) = 1^2 - 1 = 0$. The first condition is satisfied for any $\gamma$.
2.  We need $\rho'(1) = \sigma(1)$. First, $\rho'(z) = 2z - 1$, so $\rho'(1) = 1$. Next, $\sigma(1) = \gamma(1)^2 + \frac{2}{3}(1) - \frac{1}{12} = \gamma + \frac{8}{12} - \frac{1}{12} = \gamma + \frac{7}{12}$.
Setting them equal: $1 = \gamma + \frac{7}{12}$, which gives $\gamma = 5/12$. The method is consistent if and only if $\gamma = 5/12$ .

#### Zero-Stability: Controlling Error Propagation

Consistency alone is not enough for convergence. The method must also be stable in the sense that small perturbations (like round-off errors) do not grow and overwhelm the true solution. **Zero-stability** is the property that governs this behavior in the limit as $h \to 0$. It depends only on the coefficients $\alpha_j$ through the first [characteristic polynomial](@entry_id:150909), $\rho(z)$.

A method is **zero-stable** if all roots of its first [characteristic polynomial](@entry_id:150909) $\rho(z)$ satisfy the **root condition**:
1.  All roots $z_i$ must have magnitude less than or equal to 1: $|z_i| \le 1$.
2.  Any root with magnitude exactly 1 must be a simple (non-repeated) root.

The reason for this condition is that the numerical solution $y_n$ generated by the LMM satisfies a homogeneous recurrence relation determined by the $\alpha_j$ coefficients. The general solution to this recurrence is a [linear combination](@entry_id:155091) of terms of the form $c_i z_i^n$ (for [simple roots](@entry_id:197415)) or $P(n)z_i^n$ where $P(n)$ is a polynomial (for multiple roots). If any root has $|z_i| > 1$, the corresponding component $z_i^n$ will grow exponentially. If a root with $|z_i|=1$ is repeated, the solution will grow polynomially (e.g., like $n z_i^n$). Zero-stability ensures that none of these unbounded growth modes are present.

As an example, let's examine the [zero-stability](@entry_id:178549) of the method defined by $3y_{n+2} - 2y_{n+1} - y_n = h(\dots)$. The stability depends only on the left-hand side coefficients: $\alpha_2=3, \alpha_1=-2, \alpha_0=-1$. The first [characteristic polynomial](@entry_id:150909) is:

$$ \rho(z) = 3z^2 - 2z - 1 $$

To find the roots, we solve $3z^2 - 2z - 1 = 0$. Factoring gives $(3z+1)(z-1)=0$. The roots are $z_1=1$ and $z_2 = -1/3$ . Let's check the root condition:
*   $|z_1|=1$ and $|z_2|=|-1/3|=1/3 \le 1$. The magnitude condition is met.
*   The root on the unit circle, $z_1=1$, is simple.

Since both parts of the root condition are satisfied, this method is zero-stable.

### Stability for Stiff Systems: A-Stability

While [zero-stability](@entry_id:178549) guarantees convergence as $h \to 0$, it does not describe the method's behavior for a fixed, non-zero step size $h$. This is particularly important for **stiff ODEs**, which are systems involving processes that decay at vastly different rates. For such problems, explicit methods are often forced to take prohibitively small steps to remain stable, even when the rapidly decaying components are no longer significant to the solution.

To analyze this behavior, we apply the method to **Dahlquist's test equation**, $y' = \lambda y$, where $\lambda$ is a complex constant. The true solution is $y(t) = y_0 \exp(\lambda t)$, which decays to zero if $\text{Re}(\lambda)  0$. A desirable numerical method should replicate this decaying behavior. This leads to the concept of **A-stability**.

A numerical method is said to be **A-stable** if, when applied to the test equation $y'=\lambda y$, the numerical solution sequence $\{y_n\}$ is non-increasing in magnitude (i.e., $|y_{n+1}| \le |y_n|$) for all complex numbers $\lambda$ with $\text{Re}(\lambda)  0$ and for any step size $h > 0$ . This means the method's **region of [absolute stability](@entry_id:165194)**—the set of complex numbers $z=h\lambda$ for which the numerical solution does not grow—contains the entire open left-half of the complex plane.

A-stability is a powerful property, as it allows for the use of large step sizes on [stiff problems](@entry_id:142143) without the numerical solution becoming unstable. However, for the class of [linear multistep methods](@entry_id:139528), there is a severe restriction known as the **First Dahlquist Barrier**:

 **First Dahlquist Barrier:** An A-stable [linear multistep method](@entry_id:751318) cannot have an [order of convergence](@entry_id:146394) greater than two.

This theorem has profound consequences. It tells us that it is impossible to construct an LMM that is both A-stable and has an order of three or more. If one requires an LMM with order higher than two, the property of A-stability must be compromised . The theorem further states that the second-order A-stable LMM with the smallest error constant is the trapezoidal rule. This barrier motivates the use of other classes of methods, such as implicit Runge-Kutta methods, when seeking high-order, A-stable integrators for [stiff differential equations](@entry_id:139505).