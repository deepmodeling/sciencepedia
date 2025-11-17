## Introduction
The analysis of stability is a cornerstone of control theory and dynamical systems, yet for nonlinear systems, it presents a formidable challenge. While Lyapunov's direct method provides a universal framework, its application hinges on the discovery of a suitable Lyapunov function—a task that is often more art than science, relying on intuition or restriction to simple quadratic forms. This frequently leaves a gap between the theoretical guarantee of stability and a practical, systematic means of demonstrating it.

The Krasovskii method emerges as an elegant and powerful solution to this problem. Instead of postulating a function of the state $x$, Krasovskii's insight was to construct a candidate function directly from the system's dynamics, the vector field $f(x)$. This article provides a graduate-level exploration of this constructive technique, guiding you from its foundational principles to its advanced applications and interdisciplinary significance.

The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork. We will delve into the construction of the Krasovskii Lyapunov function, $V(x) = f(x)^{\top} P f(x)$, derive its time derivative, and establish the crucial link between stability and the system's Jacobian matrix. We will explore its use for both local and global stability, and the role of LaSalle's Invariance Principle when the derivative is only semidefinite.

Next, in **Applications and Interdisciplinary Connections**, we will move from theory to practice. This chapter demonstrates how the method is used to estimate regions of attraction, design robust feedback controllers, and serves as a conceptual link to diverse fields. We will uncover its deep connections to optimization theory through [gradient flows](@entry_id:635964), computational methods via Sum-of-Squares programming, and differential geometry through the lens of contraction analysis.

Finally, the **Hands-On Practices** section provides a curated set of problems designed to solidify your understanding and build practical skill in applying the Krasovskii method to concrete examples. By navigating through these chapters, you will gain not just a tool for analysis, but a unifying perspective on the structure and behavior of [nonlinear systems](@entry_id:168347).

## Principles and Mechanisms

The Krasovskii method provides a systematic, constructive approach to finding Lyapunov functions for autonomous nonlinear systems of the form $\dot{x} = f(x)$, where $f: \mathbb{R}^n \to \mathbb{R}^n$ is a vector field with an equilibrium at the origin, i.e., $f(0) = 0$. Instead of seeking a Lyapunov function in the state $x$ directly, such as the common [quadratic form](@entry_id:153497) $V(x) = x^{\top}Px$, Krasovskii's insight was to construct a candidate function based on the system's vector field itself. This chapter elucidates the principles behind this construction, its requirements, and its application in both local and global stability analysis.

### The Krasovskii Lyapunov Function Candidate

The central object in the Krasovskii method is the candidate Lyapunov function:
$$
V(x) = f(x)^{\top} P f(x)
$$
where $P \in \mathbb{R}^{n \times n}$ is a constant matrix to be chosen. For $V(x)$ to serve as a valid Lyapunov function, it must satisfy several fundamental properties.

First, a Lyapunov function must be continuously differentiable. The function $V(x)$ is a composition of the vector field $f(x)$ and the quadratic form defined by $P$. The quadratic form itself is infinitely differentiable. Therefore, by the [chain rule](@entry_id:147422), $V(x)$ is guaranteed to be continuously differentiable (class $C^1$) provided that the vector field $f(x)$ is also continuously differentiable [@problem_id:2716041]. This is a standing assumption for the application of the method.

Second, for stability analysis, $V(x)$ must be [positive definite](@entry_id:149459), meaning $V(0)=0$ and $V(x) > 0$ for all $x \neq 0$ in a neighborhood of the origin. Since $f(0)=0$, we have $V(0)=0$. For the positivity condition, we turn to the matrix $P$. The quadratic form $y^{\top}Py$ depends only on the symmetric part of $P$, $\frac{1}{2}(P+P^{\top})$. Thus, without loss of generality, we can assume $P$ is a **[symmetric matrix](@entry_id:143130)** from the outset [@problem_id:2716046]. If we choose $P$ to be **symmetric and [positive definite](@entry_id:149459)** ($P \succ 0$), the quadratic form $y^{\top}Py$ is positive for any non-[zero vector](@entry_id:156189) $y$. Consequently, $V(x) = f(x)^{\top}Pf(x)$ will be non-negative, and it will be strictly positive if and only if $f(x) \neq 0$.

This leads to a crucial prerequisite for the method: for $V(x)$ to be positive definite with respect to the state $x$, we must have $f(x) \neq 0$ for all $x \neq 0$ in the domain of interest. This means the origin must be the **unique equilibrium** in that domain [@problem_id:2716046] [@problem_id:2716025]. If this condition holds, choosing $P \succ 0$ ensures that $V(x)$ is a valid, [positive definite](@entry_id:149459) candidate.

### Geometric Interpretation

The choice of $V(x) = f(x)^{\top} P f(x)$ carries a distinct geometric meaning that contrasts with the standard quadratic form $W(x) = x^{\top} P x$. The [sublevel sets](@entry_id:636882) of $W(x)$, defined by $\{x : x^{\top} P x \le c\}$, are ellipsoids in the state space centered at the origin. These sets define regions where the norm of the state vector $x$ is small [@problem_id:2715977].

In contrast, the [sublevel sets](@entry_id:636882) of the Krasovskii function, $\{x : f(x)^{\top} P f(x) \le c\}$, define regions where the norm of the vector field $f(x)$—the "velocity" vector—is small. Geometrically, these sets are the preimages under the map $f$ of ellipsoids in the codomain of $f$. Their shape in the state space is determined by the global properties of the function $f(x)$. Unlike the level sets of $W(x)$, they are not necessarily simple ellipsoids centered at the origin. If the system has other equilibria besides the origin, the [level sets](@entry_id:151155) of $V(x)$ will contain neighborhoods around each of these points, and thus may not be localized to the origin at all [@problem_id:2715977].

### The Time Derivative and Stability Conditions

The power of the method lies in the structure of the time derivative of $V(x)$ along system trajectories. Applying the [chain rule](@entry_id:147422), we find:
$$
\dot{V}(x) = \frac{d}{dt} \left( f(x(t))^{\top} P f(x(t)) \right) = f(x)^{\top} \left( Df(x)^{\top} P + P Df(x) \right) f(x)
$$
where $Df(x)$ is the Jacobian matrix of $f(x)$. Let us define the symmetric matrix field $S(x) = Df(x)^{\top} P + P Df(x)$. The time derivative then takes the compact [quadratic form](@entry_id:153497):
$$
\dot{V}(x) = f(x)^{\top} S(x) f(x)
$$
To establish [asymptotic stability](@entry_id:149743), we must show that $\dot{V}(x)$ is [negative definite](@entry_id:154306). This expression reveals that $\dot{V}(x)$ will be negative if the matrix $S(x)$ is [negative definite](@entry_id:154306) and the vector $f(x)$ is non-zero. The central task of the Krasovskii method is therefore to find a single constant matrix $P \succ 0$ such that the state-dependent matrix $S(x)$ is [negative definite](@entry_id:154306) (or at least negative semidefinite) over the domain of interest [@problem_id:2721563].

A [sufficient condition](@entry_id:276242) for $\dot{V}(x) \le -\alpha \|f(x)\|^2$ for some $\alpha > 0$ is the [matrix inequality](@entry_id:181828) $S(x) \preceq -\alpha I$, where $I$ is the identity matrix [@problem_id:2721563]. If this condition holds and we additionally have that the origin is the unique equilibrium, then $\dot{V}(x)$ is [negative definite](@entry_id:154306), and by Lyapunov's direct method, the origin is asymptotically stable [@problem_id:2715982].

### Local Stability and the Link to Linearization

The Krasovskii method establishes a powerful connection between the stability of the [nonlinear system](@entry_id:162704) and its [linearization](@entry_id:267670) at the origin, $\dot{z} = Df(0)z$. Since $Df(x)$ is continuous, if we can ensure that $S(0)$ is [negative definite](@entry_id:154306), it will remain so in a small neighborhood of the origin. The condition at the origin is:
$$
S(0) = Df(0)^{\top} P + P Df(0) \prec 0
$$
This is the well-known Lyapunov inequality for the linear [system matrix](@entry_id:172230) $A = Df(0)$. A fundamental result from [linear systems theory](@entry_id:172825) states that such a [symmetric matrix](@entry_id:143130) $P \succ 0$ exists if and only if the matrix $A = Df(0)$ is **Hurwitz** (i.e., all its eigenvalues have strictly negative real parts) [@problem_id:2716015].

This provides a profound insight: if the [linearization](@entry_id:267670) of the system at the origin is asymptotically stable, then the Krasovskii method guarantees the existence of a local Lyapunov function of the form $V(x) = f(x)^{\top}Pf(x)$ that can prove the local [asymptotic stability](@entry_id:149743) of the [nonlinear system](@entry_id:162704). The task reduces to solving the Lyapunov equation $Df(0)^{\top} P + P Df(0) = -Q$ for some chosen $Q \succ 0$ to find a suitable $P$.

Furthermore, if the Jacobian $Df(0)$ is nonsingular (a consequence of it being Hurwitz), the geometries of the Krasovskii function $V(x)$ and a standard quadratic function $W(x) = x^{\top}\tilde{P}x$ become locally equivalent near the origin. This means that in a small neighborhood, the [level sets](@entry_id:151155) of $V(x)$ are also approximately ellipsoidal, and $V(x)$ is quadratically bounded both above and below by $\|x\|^2$ [@problem_id:2715977].

### Semidefinite Derivative and Invariance Principles

In many cases, it is only possible to find a $P \succ 0$ such that $S(x)$ is negative semidefinite ($S(x) \preceq 0$), but not [negative definite](@entry_id:154306). This implies that $\dot{V}(x) = f(x)^{\top}S(x)f(x) \le 0$. A non-positive derivative only proves that $V(x)$ is non-increasing along trajectories, which is sufficient for Lyapunov stability but not for [asymptotic stability](@entry_id:149743) [@problem_id:2716007].

Asymptotic stability requires that trajectories converge to the origin. If $\dot{V}(x)$ can be zero for states other than the origin, trajectories might "get stuck" on these states without converging to the origin. The set where the derivative vanishes is $E = \{x \mid \dot{V}(x) = 0\}$. From the expression for $\dot{V}(x)$, this set includes all equilibria of the system (where $f(x)=0$) and potentially other points where $f(x)$ is in the [nullspace](@entry_id:171336) of $S(x)$ [@problem_id:2715982].

To proceed, we must invoke **LaSalle's Invariance Principle**. This principle states that if solutions are bounded, they must converge to the largest [invariant set](@entry_id:276733) contained within $E$. An [invariant set](@entry_id:276733) is a set of states such that any trajectory starting in the set remains in the set for all time. To prove [asymptotic stability](@entry_id:149743) of the origin, we must analyze the dynamics on the set $E$ and show that the only trajectory that can stay within $E$ forever is the trivial trajectory $x(t) \equiv 0$. In other words, the largest invariant subset of $E$ must be the singleton $\{0\}$ [@problem_id:2716025] [@problem_id:2716007].

Consider the simple linear system $\dot{x}_1 = -x_1, \dot{x}_2 = 0$. Using the Krasovskii method, one can show that $\dot{V}(x) = -2p_{11}x_1^2 \le 0$ (assuming a diagonal $P$). The set where $\dot{V}(x)=0$ is the entire $x_2$-axis ($x_1=0$). The dynamics on this axis are $\dot{x}_2=0$, meaning any point on the axis is an equilibrium. Thus, the $x_2$-axis is an [invariant set](@entry_id:276733). Trajectories starting on this axis (e.g., at $(0,c)$) stay there and do not converge to the origin. This system is stable but not asymptotically stable, illustrating why an invariance analysis is indispensable when $\dot{V}$ is only semidefinite [@problem_id:2716007].

### Global Stability

To extend the analysis to prove [global asymptotic stability](@entry_id:187629) (GAS), the Lyapunov function $V(x)$ must be **radially unbounded**, meaning $V(x) \to \infty$ as $\|x\| \to \infty$. This property ensures that the [sublevel sets](@entry_id:636882) of $V(x)$ are compact, which is a key requirement for applying global [stability theorems](@entry_id:195621).

For the Krasovskii function $V(x) = f(x)^{\top}Pf(x)$, the condition of radial unboundedness translates into a condition on the vector field $f(x)$. Since $V(x) \ge \lambda_{\min}(P)\|f(x)\|^2$, a sufficient condition for $V(x)$ to be radially unbounded is that $\|f(x)\| \to \infty$ as $\|x\| \to \infty$. Such a map $f$ is known as a **[proper map](@entry_id:158587)**. This can be expressed more formally by requiring that $\|f(x)\|$ is lower-bounded by a class-$\mathcal{K}_\infty$ function of $\|x\|$, i.e., there exists a continuous, strictly increasing function $\gamma$ with $\gamma(0)=0$ and $\gamma(r)\to\infty$ as $r\to\infty$, such that $\|f(x)\| \ge \gamma(\|x\|)$ for all $x$ [@problem_id:2716034].

Therefore, to prove GAS using this method, one typically needs to establish three main properties:
1.  The origin is the unique equilibrium: $f(x)=0 \iff x=0$.
2.  The vector field is proper: $\|f(x)\| \to \infty$ as $\|x\| \to \infty$.
3.  A global [negative definite](@entry_id:154306) condition on the derivative, such as $Df(x)^{\top} P + P Df(x) \preceq -\alpha I$ for all $x \in \mathbb{R}^n$.

### Scope and Limitations

It is crucial to understand that the Krasovskii method is a *constructive* tool that proposes a candidate function with a very specific algebraic structure. Its success is not guaranteed for every stable system. **Converse Lyapunov theorems** guarantee that if a system is asymptotically stable, a smooth Lyapunov function *exists*, but they do not guarantee it will have the Krasovskii form [@problem_id:2716018].

Indeed, there are simple systems that are globally asymptotically stable, yet for which no constant matrix $P \succ 0$ can make $V(x) = f(x)^{\top}Pf(x)$ a valid global Lyapunov function. For example, the scalar system $\dot{x} = -x/(1+x^2)$ is GAS. However, the derivative of the corresponding Krasovskii function, $\dot{V}(x) = -2p x^2(1-x^2)/(1+x^2)^4$, becomes positive for $|x|>1$. This shows that the method, in its basic form with constant $P$, can be restrictive and may only yield local results even for globally stable systems [@problem_id:2716018].

This limitation does not apply to linear time-invariant (LTI) systems $\dot{x}=Ax$. For a Hurwitz matrix $A$, the Krasovskii candidate becomes $V(x) = (Ax)^{\top}P(Ax) = x^{\top}(A^{\top}PA)x$. The search for a suitable $P \succ 0$ is equivalent to solving the standard Lyapunov inequality, which is known to have a solution. In this sense, for LTI systems, the method is not restrictive and successfully recovers the standard quadratic Lyapunov [function theory](@entry_id:195067) [@problem_id:2716018]. This highlights that the method is most naturally suited for systems where the "velocity" $f(x)$ behaves somewhat linearly with respect to the state $x$. Extensions to state-dependent matrices $P(x)$ exist to broaden the applicability of this powerful and elegant method.