## Introduction
In the world of computational fluid dynamics (CFD), the ultimate goal is to create simulations that are not just numerically accurate, but physically trustworthy. Standard numerical methods can inadvertently violate the fundamental laws of physics, such as the conservation of energy or the Second Law of Thermodynamics, leading to unstable or non-physical results. This article addresses this critical gap by introducing a powerful class of numerical methods designed from the ground up to respect these physical principles: Summation-by-Parts (SBP) operators that are either entropy-stable or kinetic-energy-preserving. By embedding the laws of physics directly into the algebraic structure of the simulation, these schemes offer unparalleled robustness and reliability.

Across the following chapters, we will embark on a comprehensive journey into this advanced framework. First, in "Principles and Mechanisms," we will dissect the core mathematical machinery, from the discrete integration-by-parts rule to the concepts of convex entropy and energy-preserving split forms. Next, "Applications and Interdisciplinary Connections" will demonstrate how these theories are translated into practice to tackle complex challenges like boundary conditions, curved grids, viscosity, and shock waves. Finally, "Hands-On Practices" will provide opportunities to apply and verify these concepts directly. This structured exploration will equip you with the knowledge to build and trust simulations that behave like the physical world they are meant to represent.

## Principles and Mechanisms

To build a numerical simulation that you can trust, you must teach it the laws of physics. Not just approximately, but in a deep, structural way. Computers think in terms of numbers and algebra, while physics speaks the language of calculus. Our first challenge is to bridge this gap. How can we translate the fundamental principles of calculus, which underpin all conservation laws, into the discrete world of a computational grid?

### The Soul of Conservation: Discrete Integration by Parts

Let's begin with a cornerstone of calculus: **integration by parts**. For any two smooth functions $u(x)$ and $v(x)$, it tells us that the integral of $u$ times the derivative of $v$ is related to the integral of $v$ times the derivative of $u$:
$$
\int_a^b u \frac{dv}{dx} \,dx = [uv]_a^b - \int_a^b v \frac{du}{dx} \,dx
$$
This identity is not just a mathematical trick; it's the heart of conservation of energy, momentum, and more. The change inside a domain is balanced by what happens at the boundary. If we want our numerical schemes to respect conservation, they must respect a discrete version of this rule. This is the central idea behind **Summation-by-Parts (SBP)** operators.

An SBP operator isn't just any [finite difference stencil](@entry_id:636277). It's a carefully constructed triplet of matrices $(D, H, Q)$ with a special relationship. For a grid of $N$ points, $D$ is the $N \times N$ matrix that acts as our derivative operator. But it's defined in a very specific way: $D = H^{-1}Q$. Here, $H$ is a symmetric, [positive-definite matrix](@entry_id:155546) that defines a discrete inner product, or "norm." You can think of it as the matrix of [quadrature weights](@entry_id:753910) that defines how we sum things up on our grid, our discrete version of integrating with $dx$. The magic lies in the third matrix, $Q$, which is constrained by the SBP property:
$$
Q + Q^T = B
$$
where $B$ is a simple boundary matrix, typically $B = \mathrm{diag}(-1, 0, \dots, 0, 1)$, which only has non-zero entries at the first and last points of the domain .

This seemingly abstract algebraic condition is, in fact, the discrete version of integration by parts in disguise! Let's see how. Consider the discrete inner product of a grid function $u$ with the derivative of another grid function $v$, which is written as $u^T H (D v)$. Using the SBP definitions:
$$
u^T H D v = u^T H (H^{-1} Q) v = u^T Q v
$$
What about the other way around, $v^T H D u$? A similar calculation gives $v^T Q u$, which is a scalar and thus equal to its transpose, $u^T Q^T v$. Now, watch what happens when we add them together:
$$
u^T H D v + v^T H D u = u^T Q v + u^T Q^T v = u^T (Q + Q^T) v = u^T B v
$$
Rearranging this gives us the beautiful Summation-by-Parts formula:
$$
u^T H D v = -v^T H D u + u^T B v
$$
This is a perfect algebraic mirror of the continuous integration-by-parts rule! The term $u^T H D v$ is our discrete integral $\int u v' dx$, and the term $u^T B v = u_N v_N - u_1 v_1$ is the boundary evaluation $[uv]_a^b$.

This isn't just a curiosity. It has profound consequences. Consider the simple [linear advection equation](@entry_id:146245), $\partial_t u + a \partial_x u = 0$, which describes something moving at a constant speed $a$. If we discretize it as $\frac{d\vec{u}}{dt} + a D \vec{u} = 0$, what happens to the total "kinetic energy," which we can define as $E = \frac{1}{2} \vec{u}^T H \vec{u}$? The rate of change of this energy is:
$$
\frac{dE}{dt} = \vec{u}^T H \frac{d\vec{u}}{dt} = -\vec{u}^T H (a D \vec{u}) = -a (\vec{u}^T H D \vec{u})
$$
By setting $v=u$ in our SBP formula, we find that $\vec{u}^T H D \vec{u} + \vec{u}^T H D \vec{u} = \vec{u}^T B \vec{u}$, which means $\vec{u}^T H D \vec{u} = \frac{1}{2} \vec{u}^T B \vec{u}$. So, the rate of change of energy becomes:
$$
\frac{dE}{dt} = -\frac{a}{2} \vec{u}^T B \vec{u} = -\frac{a}{2} (u_N^2 - u_1^2)
$$
This is remarkable. The SBP property guarantees that the total energy inside our domain changes *only* due to energy flowing through the boundaries. If the domain is periodic (like a circle), there are no boundaries, so $B=0$, and energy is perfectly, exactly conserved. This property is known as **kinetic-energy-preserving (KEP)**, and it emerges naturally from the SBP structure .

### The Law of the Boundary

The SBP framework not only handles energy conservation but also total mass conservation with similar elegance. If we integrate our semi-[discrete conservation](@entry_id:1123819) law $\frac{d\boldsymbol{u}}{dt} + \boldsymbol{D}\boldsymbol{f}(\boldsymbol{u}) = \boldsymbol{0}$ over the entire domain using our [discrete measure](@entry_id:184163) $H$, we want to see how the total quantity $U_{total} = \boldsymbol{1}^T \boldsymbol{H} \boldsymbol{u}$ changes. A direct application of the SBP rules reveals another beautiful result:
$$
\frac{dU_{total}}{dt} = f_1 - f_N
$$
This means the total amount of a substance in the domain changes only by the amount of flux entering at the left boundary ($f_1$) minus the flux exiting at the right boundary ($f_N$). The derivation shows that the SBP framework automatically enforces this discrete version of the Fundamental Theorem of Calculus with boundary flux weights of exactly 1 . This isn't an approximation; it's a discrete law that the scheme is built to obey.

Of course, in most real problems, we need to impose specific conditions at the boundaries. This is where the **Simultaneous Approximation Term (SAT)** method comes in. SATs are like little penalty terms we add to the equations right at the boundary. They act like springs, gently but firmly pulling the numerical solution towards the desired physical boundary condition. The beauty is that they can be designed to be compatible with the SBP framework, so that while they enforce the boundary condition, we can still precisely track their effect on global conservation. The conservation "error" introduced by these terms is not some unknown numerical sludge, but a well-defined quantity that depends only on how much the solution at the boundary differs from the imposed data .

### Taming the Chaos: Nonlinearity and the Entropy Principle

Moving from the clean world of [linear advection](@entry_id:636928) to the messy, fascinating world of gas dynamics, governed by the compressible Euler equations, presents a new challenge. In this world, smooth flows can suddenly develop sharp discontinuities called shocks. Across a shock, kinetic energy is *not* conserved. It gets converted into heat, and a more fundamental quantity, the **[thermodynamic entropy](@entry_id:155885)**, must not decrease, according to the Second Law of Thermodynamics.

A numerical scheme that fails to respect this can produce all sorts of unphysical nonsense, like "expansion shocks" where a gas spontaneously cools and orders itself. To prevent this, we need our schemes to be **entropy-stable**. This means we need to find a discrete version of the Second Law.

The first step is to identify the right quantity to track. It turns out that to enforce the physical law that [thermodynamic entropy](@entry_id:155885) $s$ is non-decreasing ($\partial_t(\rho s) + \dots \ge 0$), we must build our scheme around a related **mathematical entropy** $U$. The standard choice, pioneered by Harten, is $U(u) = -\rho s$. By requiring our scheme to satisfy $\partial_t U + \dots \le 0$, we get the correct physical behavior. But there's a catch: for this to work, the mathematical entropy $U(u)$ must be a **[convex function](@entry_id:143191)** of the conserved state variables $u = (\rho, \rho u, \rho E)^T$ . This [convexity](@entry_id:138568) is the mathematical bedrock upon which the entire theory of [entropy stability](@entry_id:749023) is built. Just as a ball released in a convex bowl will roll to the bottom and stay there, a numerical scheme built on a convex entropy will be stable and not blow up. Any positive scaling of a valid entropy function, say $cU(u)$, results in an equally valid entropy function that leads to the same physical conclusions and stability properties .

With a convex entropy $U$ in hand, the next question is how to design a numerical flux that respects it. This leads to the work of Tadmor and the concept of an **entropy potential**, $\psi$. It turns out that for any given physical flux $f(u)$ and a chosen entropy $U(u)$, one can define a set of entropy variables $v = \nabla_u U$ and a corresponding entropy potential $\psi(u)$. This potential is defined such that the entropy flux can be written as $F(u) = v(u)^T f(u) - \psi(u)$.

The incredible payoff is that this allows for the construction of special two-point [numerical fluxes](@entry_id:752791), $f^*(u_L, u_R)$, which are **entropy-conservative**. They satisfy the remarkable identity:
$$
(v_R - v_L)^T f^*(u_L, u_R) = \psi(u_R) - \psi(u_L)
$$
When used with an SBP operator, the interior derivative terms in the discrete entropy equation form a [telescoping sum](@entry_id:262349) that cancels out perfectly, meaning the scheme produces zero numerical entropy. To get the physically correct dissipation at shocks, one then adds a carefully controlled amount of dissipation. For the complex Euler equations, the derivation is involved, but the final result for the entropy potential is breathtakingly simple: it's just the [momentum density](@entry_id:271360), $\psi(u) = m$ . This profound simplicity hidden within a complex nonlinear system is a hallmark of deep physical principles at work.

### The Unifying Dance of Energy and Entropy

So far, we have two big ideas: schemes that preserve kinetic energy (KEP) and schemes that are stable with respect to entropy. Are they related? Can a scheme be both? The answer lies in how we choose to write down and discretize the nonlinear convective terms of the fluid equations.

Instead of just naively discretizing a term like $\partial_x(\rho u^2)$, we can write it in an equivalent "split form" before discretizing. For example, using the [product rule](@entry_id:144424), $\partial_x(\rho u^2) = \partial_x((\rho u) u) = u \partial_x(\rho u) + (\rho u)\partial_x u$. We can discretize a blend of these equivalent forms. A particular class of **skew-symmetric split forms**, when combined with a skew-symmetric SBP operator (like on a periodic domain), has a magical property. When you compute the total rate of change of kinetic energy, the contributions from these convective terms cancel out *identically*. The algebra works out perfectly, leaving no residual terms. The convective process neither creates nor destroys kinetic energy; it only moves it around .

This provides a powerful way to construct KEP schemes. What's more, these split-form constructions can be shown to be algebraically equivalent to a two-point flux differencing approach. The necessary and [sufficient condition](@entry_id:276242) for a two-point flux to be KEP is beautifully simple: the convective momentum flux between two points, $f^{m, conv}_{ij}$, must be equal to the [average velocity](@entry_id:267649) times the mass flux between those same two points, $f^{\rho}_{ij}$ :
$$
f^{m, \mathrm{conv}}_{ij} = \frac{u_i + u_j}{2} f^{\rho}_{ij}
$$
Different KEP schemes, like those of Morinishi or Pirozzoli, are ultimately different ways of choosing the mass flux $f^{\rho}_{ij}$ and then building the momentum flux to satisfy this identity . For simpler systems like the isentropic Euler equations, the connection is even more direct: the [total mechanical energy](@entry_id:167353) can itself be used as a convex entropy function, and a scheme that conserves this "entropy" is, by definition, kinetic-energy-preserving .

### The Devil in the Details: Real Operators and Their Behavior

These principles are not just abstract mathematics; they translate into concrete [matrix operators](@entry_id:269557). For instance, one can construct an SBP operator using a simple **diagonal norm matrix** $H$. These operators are computationally efficient, but to satisfy the SBP property, they must often sacrifice accuracy at the boundary points . Alternatively, one can use a dense, **full-norm matrix** $H$. These are more complex but can achieve higher-order accuracy all the way to the boundary, which can be critical for some problems. Both constructions, however, are built on the same foundational SBP property .

What are the practical consequences of using a scheme that perfectly preserves a quantity like kinetic energy? A von Neumann stability analysis of a simple KEP scheme provides the answer. It shows that such schemes have zero numerical dissipation . This is a double-edged sword. On one hand, it's wonderful for simulating phenomena like turbulence, where you want to resolve a wide range of scales without the simulation artificially damping them out. On the other hand, it means the scheme cannot dissipate high-frequency noise that might arise from unresolved features or boundary interactions. Furthermore, while the amplitudes of waves are preserved, their speeds are generally not. This **[numerical dispersion](@entry_id:145368)** can cause waves of different frequencies to travel at different incorrect speeds, leading to trailing oscillations and a distorted solution.

The art and science of modern CFD, therefore, is not just about finding a scheme that is "accurate." It is about designing schemes from first principles—like Summation-by-Parts—that inherit the deep structural properties of the underlying physics. By building schemes that are provably entropy-stable or kinetic-energy-preserving, we create simulations that are not only robust but that also respect the fundamental laws of nature.