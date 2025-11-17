## Introduction
What is the straightest possible path between two points on a curved surface? In Euclidean space, the answer is a straight line, but on a sphere or a more complex Riemannian manifold, the answer is a "geodesic." Identifying these shortest paths is a central problem in geometry. While the most intuitive approach is to minimize a path's total length, the mathematics involved can be challenging. A more powerful and elegant solution lies in studying a related quantity: the path's energy. This article demonstrates how minimizing the [energy functional](@entry_id:170311) provides a more direct route to finding geodesics.

This article is structured into three chapters to guide you from foundational theory to practical application. In "Principles and Mechanisms," we will introduce the length and energy functionals, analyze their properties, and use the [calculus of variations](@entry_id:142234) to derive the fundamental [geodesic equation](@entry_id:136555). Following this, "Applications and Interdisciplinary Connections" will showcase the broad impact of these ideas, revealing how geodesics describe phenomena in classical geometry, the motion of particles in physics, and the pathways of chemical reactions. Finally, "Hands-On Practices" will provide a set of guided problems to solidify your understanding by applying these concepts to concrete examples. We begin by defining the core mathematical tools for measuring paths on manifolds.

## Principles and Mechanisms

In the study of geometry, a fundamental question is how to identify the "straightest" or "shortest" path between two points on a curved space, such as a sphere or a more general Riemannian manifold. These paths, known as **geodesics**, are the analogues of straight lines in Euclidean space. The primary method for identifying them is through the calculus of variations, by finding paths that are critical points of a functional that measures some aspect of the path, typically its length. This chapter introduces the two most important functionals in this context—the **[length functional](@entry_id:203503)** and the **energy functional**—and explores the profound and fruitful relationship between them. We will find that while our ultimate interest lies in minimizing length, the mathematically more tractable energy functional provides a more direct route to the same goal.

### Measuring Paths on Manifolds: The Length and Energy Functionals

Let $(M,g)$ be a smooth $n$-dimensional Riemannian manifold, where $g$ is a Riemannian metric that equips each tangent space $T_pM$ with an inner product $g_p$. Consider a smooth path, which is a map $\gamma: [a, b] \to M$. The velocity of this path at a time $t$ is the [tangent vector](@entry_id:264836) $\dot{\gamma}(t) \in T_{\gamma(t)}M$. The metric $g$ allows us to define the **speed** of the path, which is simply the norm of the velocity vector:

$$
|\dot{\gamma}(t)|_g := \sqrt{g_{\gamma(t)}(\dot{\gamma}(t), \dot{\gamma}(t))}
$$

To compute this in practice, we often work in [local coordinates](@entry_id:181200). Let $(U, (x^1, \dots, x^n))$ be a [coordinate chart](@entry_id:263963) covering the path's image. The velocity vector can be expressed in the [coordinate basis](@entry_id:270149) $\{\frac{\partial}{\partial x^i}\}$ as $\dot{\gamma}(t) = \sum_{i=1}^n \dot{\gamma}^i(t) \frac{\partial}{\partial x^i}|_{\gamma(t)}$, where the components are given by the chain rule: $\dot{\gamma}^i(t) = \frac{d}{dt}(x^i \circ \gamma)(t)$. The components of the metric tensor in this chart are $g_{ij}(p) = g_p(\frac{\partial}{\partial x^i}, \frac{\partial}{\partial x^j})$. Substituting these into the definition of speed, and employing the Einstein [summation convention](@entry_id:755635), we find the squared speed is:

$$
|\dot{\gamma}(t)|_g^2 = g_{ij}(\gamma(t)) \dot{\gamma}^i(t) \dot{\gamma}^j(t)
$$

This expression makes it clear that the speed depends fundamentally on the metric $g$. It is not, in general, equal to the Euclidean norm of the coordinate velocities, $\sqrt{\sum_i (\dot{\gamma}^i)^2}$. However, a special choice of coordinates, known as **[normal coordinates](@entry_id:143194)** centered at a point $p \in M$, can simplify this calculation locally. By construction, at the point $p$, the metric tensor in [normal coordinates](@entry_id:143194) is the identity matrix, i.e., $g_{ij}(p) = \delta_{ij}$ (the Kronecker delta). Consequently, for a path passing through $p$ at time $t_0$ (so $\gamma(t_0)=p$), the squared speed at that specific instant simplifies to the Euclidean form: $|\dot{\gamma}(t_0)|_g^2 = \sum_{i=1}^n (\dot{\gamma}^i(t_0))^2$ [@problem_id:3068815].

With the concept of speed established, we can define our two primary functionals. The most intuitive is the **[length functional](@entry_id:203503)**, $L(\gamma)$, which is obtained by integrating the speed along the path. This gives the total arc length of the curve:

$$
L(\gamma) = \int_a^b |\dot{\gamma}(t)|_g \, dt
$$

A closely related but distinct functional is the **energy functional**, $E(\gamma)$, defined by integrating half of the squared speed:

$$
E(\gamma) = \frac{1}{2} \int_a^b |\dot{\gamma}(t)|_g^2 \, dt = \frac{1}{2} \int_a^b g_{ij}(\gamma(t)) \dot{\gamma}^i(t) \dot{\gamma}^j(t) \, dt
$$

At first glance, the energy functional might seem like an unnecessary complication. The square root in the integrand of $L(\gamma)$ makes it non-differentiable if the speed is zero and generally non-linear, which poses challenges for the calculus of variations. In contrast, the integrand of $E(\gamma)$ is a simple quadratic form in the velocity components $\dot{\gamma}^i$, making it significantly easier to analyze. This distinction is the key to the entire theory.

### The Influence of Parametrization

A geometric curve is an object independent of how we trace it. We can traverse a given path at different speeds, which corresponds to **reparametrizing** the curve. A smooth, **orientation-preserving [reparametrization](@entry_id:176404)** is a smooth bijective map $\phi: [c, d] \to [a, b]$ with $\phi'(s) > 0$ for all $s \in [c, d]$. The new, reparametrized curve is $\tilde{\gamma} = \gamma \circ \phi: [c, d] \to M$ [@problem_id:3068779].

By the [chain rule](@entry_id:147422), the velocity of the new curve is $\dot{\tilde{\gamma}}(s) = \dot{\gamma}(\phi(s)) \phi'(s)$. The speed is therefore $|\dot{\tilde{\gamma}}(s)|_g = |\phi'(s)| |\dot{\gamma}(\phi(s))|_g$. Since $\phi'(s) > 0$, this simplifies to $|\dot{\tilde{\gamma}}(s)|_g = \phi'(s) |\dot{\gamma}(\phi(s))|_g$.

Let's see how our two functionals behave under this [reparametrization](@entry_id:176404). For the [length functional](@entry_id:203503), a change of variables $t = \phi(s)$ (so $dt = \phi'(s) ds$) shows that length is completely unaffected:

$$
L(\tilde{\gamma}) = \int_c^d |\dot{\tilde{\gamma}}(s)|_g \, ds = \int_c^d |\dot{\gamma}(\phi(s))|_g \phi'(s) \, ds = \int_a^b |\dot{\gamma}(t)|_g \, dt = L(\gamma)
$$

This fundamental result confirms that **arc length is a geometric invariant**, depending only on the image of the curve and not on the specific [parametrization](@entry_id:272587) used to trace it [@problem_id:3068805] [@problem_id:3068762].

The situation for the energy functional is strikingly different. Performing the same analysis:

$$
E(\tilde{\gamma}) = \frac{1}{2} \int_c^d |\dot{\tilde{\gamma}}(s)|_g^2 \, ds = \frac{1}{2} \int_c^d (|\dot{\gamma}(\phi(s))|_g \phi'(s))^2 \, ds = \frac{1}{2} \int_c^d |\dot{\gamma}(\phi(s))|_g^2 (\phi'(s))^2 \, ds
$$

This integral is generally not equal to $E(\gamma)$. In fact, using the same change of variables $t=\phi(s)$, we can express the new energy as an integral over the original interval $[a,b]$:

$$
E(\tilde{\gamma}) = \frac{1}{2} \int_a^b |\dot{\gamma}(t)|_g^2 \phi'(\phi^{-1}(t)) \, dt
$$

This shows that the **energy functional is not invariant under [reparametrization](@entry_id:176404)** [@problem_id:3068814]. Its value is sensitive to the speed at which the curve is traversed, as captured by the factor $\phi'(\phi^{-1}(t))$. For instance, if the [reparametrization](@entry_id:176404) is a simple [linear scaling](@entry_id:197235), $\phi(s) = k s$ for some constant $k > 0$, then $\phi'(s) = k$, and the [energy scales](@entry_id:196201) accordingly: $E(\tilde{\gamma}) = k E(\gamma)$ [@problem_id:3068779].

### The Variational Principle: Minimizing Energy via Constant Speed

The fact that energy depends on [parametrization](@entry_id:272587), while seeming like a drawback, is actually a feature we can exploit. For a fixed geometric path, we can ask: which parametrization minimizes the energy? This question is answered by a powerful inequality relating length and energy.

Using the Cauchy-Schwarz inequality for integrals on the functions $f(t)=1$ and $h(t)=|\dot{\gamma}(t)|_g$ over the interval $[a,b]$, we have:

$$
\left(\int_a^b 1 \cdot |\dot{\gamma}(t)|_g \, dt\right)^2 \le \left(\int_a^b 1^2 \, dt\right) \left(\int_a^b |\dot{\gamma}(t)|_g^2 \, dt\right)
$$

Recognizing the terms as our functionals, this inequality becomes:

$$
L(\gamma)^2 \le (b-a) \cdot (2 E(\gamma))
$$

Rearranging this gives a fundamental relationship:

$$
E(\gamma) \ge \frac{L(\gamma)^2}{2(b-a)}
$$

[@problem_id:3068785]. For any set of reparametrizations of a given curve image over a fixed time interval $[a,b]$, the length $L(\gamma)$ is constant. Therefore, the energy has a fixed lower bound. The Cauchy-Schwarz equality condition states that this minimum is achieved if and only if $h(t)$ is a constant multiple of $f(t)$—that is, if and only if the speed $|\dot{\gamma}(t)|_g$ is constant.

This leads to a central principle: **Among all possible parametrizations of a given curve over a fixed time interval, the [energy functional](@entry_id:170311) is minimized precisely by the constant-speed parametrization** [@problem_id:3068805] [@problem_id:3068814]. This provides a physical intuition for the [energy functional](@entry_id:170311): it favors smooth, steady motion.

### First Variation and the Geodesic Equation

To find geodesics—the [critical points](@entry_id:144653) of the [length functional](@entry_id:203503)—we will instead find the critical points of the energy functional. The tool for this is the [first variation](@entry_id:174697). We consider a **smooth variation** of a curve $\gamma(t)$, which is a family of curves $\Gamma(s, t)$ where $s$ is the variation parameter, such that $\Gamma(0, t) = \gamma(t)$. To find the shortest path between two points $p$ and $q$, we require the variation to have **fixed endpoints**: $\Gamma(s, a) = p$ and $\Gamma(s, b) = q$ for all $s$.

The infinitesimal change of the curve at $s=0$ is captured by the **variation vector field** $V(t) = \frac{\partial}{\partial s}|_{s=0} \Gamma(s, t)$. The fixed-endpoint condition means that the curves do not move at their ends, which implies that the variation vector field must vanish at the boundaries: $V(a) = 0$ and $V(b) = 0$ [@problem_id:3068799].

The [first variation](@entry_id:174697) of the energy is the derivative of $E(\Gamma(s, \cdot))$ with respect to $s$ at $s=0$. A standard calculation involving [differentiation under the integral](@entry_id:185718), the [metric compatibility](@entry_id:265910) of the Levi-Civita connection ($\nabla g = 0$), and its torsion-freeness, yields:

$$
\left.\frac{d}{ds}\right|_{s=0} E(\Gamma(s,\cdot)) = \int_a^b g(\nabla_t V(t), \dot{\gamma}(t)) \, dt
$$

Here, $\nabla_t V$ is the [covariant derivative](@entry_id:152476) of the vector field $V$ along the curve $\gamma$. To make this expression more useful, we integrate by parts. The product rule for the covariant derivative states $\frac{d}{dt} g(V, \dot{\gamma}) = g(\nabla_t V, \dot{\gamma}) + g(V, \nabla_t \dot{\gamma})$. This allows us to write:

$$
\int_a^b g(\nabla_t V, \dot{\gamma}) \, dt = \left[g(V(t), \dot{\gamma}(t))\right]_a^b - \int_a^b g(V(t), \nabla_t \dot{\gamma}(t)) \, dt
$$

Since the variation has fixed endpoints, $V(a)=V(b)=0$, and the boundary term vanishes. This leaves the final form of the **[first variation of energy](@entry_id:635793)**:

$$
\left.\frac{d}{ds}\right|_{s=0} E(\Gamma(s,\cdot)) = - \int_a^b g(V(t), \nabla_t \dot{\gamma}(t)) \, dt
$$

[@problem_id:3068774]. For $\gamma$ to be a critical point of the energy functional, its [first variation](@entry_id:174697) must be zero for *any* choice of variation field $V$ (with fixed endpoints). By the fundamental lemma of the calculus of variations, this can only be true if the other term in the inner product is identically zero. This gives us the celebrated **[geodesic equation](@entry_id:136555)**:

$$
\nabla_t \dot{\gamma}(t) = 0
$$

This equation states that a path is a critical point of the [energy functional](@entry_id:170311) if and only if its acceleration vector is zero at all times. Such a path is defined to be a **geodesic**. Furthermore, we can check the speed of any such path. Differentiating the squared speed, we get $\frac{d}{dt} |\dot{\gamma}|^2 = \frac{d}{dt}g(\dot{\gamma}, \dot{\gamma}) = 2g(\nabla_t\dot{\gamma}, \dot{\gamma})$. If $\nabla_t\dot{\gamma} = 0$, then this derivative is zero, which means the speed must be constant. Thus, **[critical points](@entry_id:144653) of the [energy functional](@entry_id:170311) are precisely geodesics parametrized with constant speed** [@problem_id:3068769].

For completeness, the [first variation](@entry_id:174697) of the [length functional](@entry_id:203503) can be computed similarly, yielding $\delta L = \int_a^b \frac{g(\nabla_t V, \dot{\gamma})}{|\dot{\gamma}|} dt$ [@problem_id:3068774]. The appearance of $|\dot{\gamma}|$ in the denominator makes this expression difficult to work with, especially for non-constant speed paths or paths where the speed might become zero. This reinforces our strategy of using the energy functional. A tangential variation $V=f\dot{\gamma}$ on a [unit-speed curve](@entry_id:635194) can be shown to produce no first-order change in length; this is geometrically intuitive, as a tangential push simply reparametrizes the curve, and length is invariant to [reparametrization](@entry_id:176404) [@problem_id:3068780].

### Equivalence of Length and Energy Critical Points

We can now state the central conclusion that justifies our entire approach. While we set out to find paths that are [critical points](@entry_id:144653) of length, we have instead analyzed the critical points of energy. The two problems are, in fact, equivalent in the most important sense.

A curve that minimizes length between two points is a geodesic. What is remarkable is that the converse also holds under the energy minimization framework. If a curve $\gamma$ on a fixed interval $[0, T]$ minimizes the [energy functional](@entry_id:170311) among all paths connecting two points, it must also minimize the [length functional](@entry_id:203503) among all such paths.

We can prove this by contradiction. Suppose $\gamma$ is an energy-minimizer but not a length-minimizer. This means there exists another path $\eta$ connecting the same points on $[0, T]$ with $L(\eta)  L(\gamma)$. From our analysis of the Cauchy-Schwarz inequality, we know that for any path, $E(\sigma) \ge L(\sigma)^2 / (2T)$, and that the minimum energy for a given length $L$ is achieved by a constant-speed parametrization. Let's reparametrize $\eta$ to a new curve $\tilde{\eta}$ with constant speed over $[0, T]$. This new curve still has length $L(\tilde{\eta}) = L(\eta)$. Its energy will be the minimum possible for that length: $E(\tilde{\eta}) = L(\tilde{\eta})^2 / (2T) = L(\eta)^2 / (2T)$. Since $\gamma$, as an energy-minimizer, must also have constant speed, its energy is $E(\gamma) = L(\gamma)^2 / (2T)$. Given our assumption that $L(\eta)  L(\gamma)$, it follows that:

$$
E(\tilde{\eta}) = \frac{L(\eta)^2}{2T}  \frac{L(\gamma)^2}{2T} = E(\gamma)
$$

This contradicts our initial premise that $\gamma$ was an energy-minimizer. Therefore, an energy-minimizing curve must also be a length-minimizing curve [@problem_id:3068769]. This elegant result provides the crucial link, allowing us to find paths of shortest length by studying the simpler, more regular energy functional.