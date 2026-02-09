## Introduction
In the world of Digital Twins and Cyber-Physical Systems (CPS), guaranteeing that a system operates correctly is paramount. From autonomous vehicles to medical devices, we need formal assurances that they will not only avoid catastrophic failures but also achieve their intended goals. Reachability analysis provides the computational backbone for this verification, offering a rigorous framework to answer two fundamental questions: Can a system ever enter a "bad" state (a safety question)? And is it guaranteed to eventually reach a "good" state (a liveness question)? This article addresses the knowledge gap between the abstract need for safety and the concrete computational methods used to certify it.

This article will guide you through the theory and practice of reachability analysis in three parts. In **Principles and Mechanisms**, we will dissect the core concepts, from the formal definitions of safety and liveness properties to the algorithms for computing forward and backward reachable sets. Next, in **Applications and Interdisciplinary Connections**, we will explore how these methods are deployed to solve real-world problems in robotics, control engineering, and even systems biology, translating abstract logic into verifiable system designs. Finally, the **Hands-On Practices** section provides concrete exercises to implement and experiment with these powerful techniques, solidifying your understanding of how to build certifiably safe and reliable systems.

## Principles and Mechanisms

In the verification of Cyber-Physical Systems (CPS) and their Digital Twins, reachability analysis serves as the computational engine for determining whether a system can ever enter an undesirable state or is guaranteed to achieve a desired objective. This chapter delves into the foundational principles and core mechanisms that underpin this analysis, moving from the formal definition of system properties to the algorithms that compute and reason about reachable states.

### Formalizing System Properties: Safety and Liveness

The correctness of a CPS is not a monolithic concept; it is a composite of multiple properties that its behavior must satisfy. The behavior of a system over time can be mathematically abstracted as a **trace**, which is an infinite sequence of states or observations $\sigma = s_0, s_1, s_2, \dots$. A property is then formally defined as a set of allowed traces. Within this framework, two fundamental classes of properties, first rigorously distinguished by Alpern and Schneider, are safety and liveness.

A **safety property** stipulates that "something bad never happens." Formally, a property $S$ is a safety property if any trace $\sigma$ that violates it (i.e., $\sigma \notin S$) has a finite "bad prefix" $\pi$. This bad prefix is an irremediable witness to the violation; any infinite trace that begins with $\pi$ also violates the property. Topologically, safety properties correspond to closed sets in the space of all infinite traces. Their defining characteristic is that they can be falsified by a finite observation. For example, in an autonomous vehicle platoon, a critical safety property is collision freedom [@problem_id:4238600]. This can be specified as an invariant that must hold at all times: the distance $d_i(t)$ between any two consecutive vehicles must always be greater than or equal to some minimum safe distance $d_{\min}$. If at any time $t_k$, we observe $d_i(t_k) \lt d_{\min}$, the safety property is violated, and no future action can erase this fact.

In contrast, a **liveness property** stipulates that "something good eventually happens." Formally, a property $L$ is a liveness property if every finite trace can be extended into an infinite trace that satisfies $L$. This means a liveness property can never be irremediably violated by any finite behavior; to prove a violation, one must analyze the entire infinite trace. Topologically, liveness properties correspond to dense sets. In the vehicle platoon example, a liveness property could be the eventual convergence of the platoon to a desired formation, such as regulating each vehicle's speed to a reference $v_{\mathrm{ref}}$ and its spacing to a policy like $h \cdot v_i(t) + d_0$ within some tolerance [@problem_id:4238600]. After any finite amount of time, one cannot conclude that the platoon will *never* converge; it may simply take longer.

These two property classes form the semantic basis for what we aim to prove with reachability analysis. Safety analysis seeks to prove that the set of all reachable states is a subset of a predefined safe set, while liveness analysis often seeks to prove that the set of reachable states has a non-empty intersection with a goal set.

### The Forward Reachable Set: Characterizing All Possible Futures

The central object in our analysis is the **reachable set**: the collection of all states that a system can attain from a given set of initial conditions under all admissible inputs and disturbances.

#### Continuous-Time Systems

For a continuous-time control system modeled by an ordinary differential equation (ODE) $\dot{x} = f(x,u)$, where $x \in \mathbb{R}^n$ is the state and $u \in U$ is the control input, the state at time $t$ is given by the **flow map** $\varphi(t; x_0, u(\cdot))$, representing the solution to the ODE starting from initial state $x_0$ under a specific input signal $u(\cdot)$.

The **forward reachable set at time $t$** from an initial set $X_0$ is the set of all states that can be reached at precisely that time, by starting from any state in $X_0$ and applying any admissible control signal. Formally, this is defined as [@problem_id:4238601]:
$$
\mathcal{R}^{+}(t; X_0) = \{ \varphi(t; x_0, u(\cdot)) \mid x_0 \in X_0, u(\cdot) \in \mathcal{U} \}
$$
where $\mathcal{U}$ is the set of all admissible input signals over the time horizon. It is crucial to distinguish this from the **forward reach tube**, which is the union of all reachable sets over a time interval, $\bigcup_{\tau \in [0,t]} \mathcal{R}^{+}(\tau; X_0)$. The reach tube characterizes all states visited at *any* time up to $t$.

#### Discrete-Time Systems

For discrete-time systems, or continuous-time systems analyzed at discrete sampling instants, the dynamics are given by a state update equation $x_{t+1} = F(x_t, u_t)$. Reachable sets are constructed iteratively. The fundamental building block is the **one-step successor operator**, denoted $\mathrm{Post}(X)$, which computes the set of all states reachable in exactly one step from a set of states $X$:
$$
\mathrm{Post}(X) = \{ F(x, u) \mid x \in X, u \in \mathcal{U} \}
$$
This operator embodies the existential nature of forward reachability: a state $x'$ is a successor if there *exists* a predecessor $x \in X$ and an input $u \in \mathcal{U}$ that generate it [@problem_id:4238626].

Using this operator, we can define multi-step reachable sets. The set of states reachable in **exactly $k$ steps**, denoted $R^{(k)}$, is computed by recursively applying the Post operator:
$$
R^{(0)} = X_0, \quad R^{(k+1)} = \mathrm{Post}(R^{(k)})
$$
This is equivalent to $R^{(k)} = \mathrm{Post}^k(X_0)$, where $\mathrm{Post}^k$ denotes the $k$-fold composition of the operator. The set of states reachable in **up to $k$ steps**, denoted $R_{\le k}$, is simply the union of all exactly-$i$ step reachable sets for $i=0, \dots, k$:
$$
R_{\le k} = \bigcup_{i=0}^{k} R^{(i)} = \bigcup_{i=0}^{k} \mathrm{Post}^i(X_0)
$$

### The Challenge of Computation: Approximation and Verification Logic

For most systems of interest—those with nonlinear dynamics, continuous-time evolution, or high-dimensional state spaces—the exact reachable set is impossible to compute analytically or numerically. Reachability analysis tools therefore rely on computing **approximations**. A sound analysis requires these approximations to have a well-defined relationship to the true reachable set, $R_{\text{exact}}$.

An **over-approximation**, denoted $R^\supset$, is a set that is guaranteed to contain the exact reachable set: $R_{\text{exact}} \subseteq R^\supset$. An **under-approximation**, denoted $R^\subset$, is a set that is guaranteed to be contained within the exact reachable set: $R^\subset \subseteq R_{\text{exact}}$. An analysis is **sound** if it provides these guarantees. It is **complete** only in the ideal case where the approximations are exact, i.e., $R^\subset = R_{\text{exact}} = R^\supset$ [@problem_id:4238572].

The type of approximation used determines the conclusions that can be soundly drawn about safety and liveness properties [@problem_id:4238572]:

*   **Proving Safety:** To prove that a system never enters an unsafe set $U$, we use an over-approximation. If we can show that the over-approximation $R^\supset$ is entirely disjoint from the unsafe set ($R^\supset \cap U = \emptyset$), then since the true reachable set is smaller ($R_{\text{exact}} \subseteq R^\supset$), it must also be disjoint from $U$. The system is verifiably safe. An intersection ($R^\supset \cap U \neq \emptyset$) is inconclusive; it could be a true safety violation or a **spurious alarm** caused by approximation error.

*   **Proving Liveness (Falsification):** To prove that a system *can* reach a target set $L$, we use an under-approximation. If we find that the under-approximation $R^\subset$ has a non-empty intersection with the target ($R^\subset \cap L \neq \emptyset$), then since every state in $R^\subset$ is a true reachable state, we have found a concrete, witnessable behavior that satisfies the liveness goal. This is often used for falsification, where we prove a system is unsafe by showing $R^\subset$ intersects the unsafe set $U$.

A common method for computing over-approximations for hybrid systems involves iterating a set-based version of a numerical integration scheme [@problem_id:4238610]. For a time step $h$, the successor set is over-approximated by taking the Minkowski sum of the current set $\hat{R}_k$, the set of all possible vector field evaluations $h \cdot F_\ell(\hat{R}_k)$, and a bloating term $E_k$ that accounts for the linearization error over the set (the "wrapping effect"), which can be bounded using the Lipschitz constant of the dynamics. For discrete jumps, the successor set is the image of the intersection of the current set and the guard region under the reset map. The soundness guarantee of such an algorithm is that it has **no false negatives** for safety: if a true violation exists ($R_k \cap U_s \neq \emptyset$), the algorithm will report a potential violation ($\hat{R}_k \cap U_s \neq \emptyset$).

### Backward Reachability and Invariance: Synthesizing Safe Controllers

While forward reachability answers "Where can the system go?", backward analysis answers "From where can the system come?" and "From where can safety be guaranteed?". This perspective is essential for control synthesis.

#### Controlled Invariant Sets

A cornerstone of safety synthesis is the concept of a **controlled invariant set**. A set $\mathcal{K}$ is controlled forward invariant if for every state within it, there exists a control strategy to keep the system's trajectory inside $\mathcal{K}$ for all future time [@problem_id:4238606]. If we can find such a set $\mathcal{K}$ that is also a subset of our designated safe set $\mathcal{S}$, then any trajectory starting in $\mathcal{K}$ can be kept safe forever.

The largest such set within $\mathcal{S}$ is called the **viability kernel** (or invariance kernel) of $\mathcal{S}$. This set represents the complete set of "safe" initial conditions from which a safety-enforcing controller can be synthesized. The existence of a controlled invariant set is deeply connected to the geometry of the system's dynamics at the set's boundary. The **Viability Theorem** provides a powerful, infinitesimal condition: a closed set $\mathcal{K}$ is controlled invariant if and only if for every state $x$ on its boundary, the set of possible velocity vectors $\{f(x,u) \mid u \in \mathcal{U}\}$ has a non-empty intersection with the **tangent cone** of $\mathcal{K}$ at $x$. In essence, at every boundary point, there must be at least one available control action that points the velocity vector "inward" or "along" the boundary [@problem_id:4238606].

#### Backward Reachability for Robust Safety

When systems are subject to uncontrollable disturbances or uncertainties, $s_{k+1} = F(s_k, u_k, w_k)$, safety becomes a game. The controller chooses $u_k$ to enforce safety, while the disturbance $w_k$ acts as an adversary trying to force the system into an unsafe state. Here, backward reachability is the natural tool.

We define the **one-step robust predecessor operator**, $\mathrm{Pre}(X)$, as the set of all states $s$ from which the controller can *force* the system into a target set $X$ in the next step, regardless of the disturbance. The quantifier order is critical:
$$
\mathrm{Pre}(X) = \{ s \in \mathcal{S} \mid \exists u \in \mathcal{U} \; \forall w \in \mathcal{W} : F(s,u,w) \in X \}
$$
This captures the controller's ability to make a move $u$ that guarantees entry into $X$ for *any* possible adversarial move $w$ [@problem_id:4238618].

Using this operator, the set of all states from which safety can be guaranteed indefinitely—the **safety-winning set** $\mathcal{W}_{\text{safe}}$—can be computed. A state is in $\mathcal{W}_{\text{safe}}$ if it is currently safe and the controller can force the next state to also be in $\mathcal{W}_{\text{safe}}$. This defines a recursive relationship: $\mathcal{W}_{\text{safe}} = (\mathcal{S} \setminus \mathcal{U}_{\mathrm{ns}}) \cap \mathrm{Pre}(\mathcal{W}_{\text{safe}})$. The winning set is the **greatest fixed point** of this mapping, which can be found by starting with the entire safe set and iteratively pruning away states from which the disturbance can force an exit.

### Advanced Certificate-Based Methods

Instead of computing reachable sets explicitly, an alternative approach is to search for a "certificate" function that mathematically proves a desired property.

#### Barrier Certificates for Safety

To prove the forward invariance of a safe set $\mathcal{S}$, we can search for a **barrier certificate**. If the safe set can be defined as the 0-sublevel set of a function $B(x)$ (i.e., $\mathcal{S} = \{ x \mid B(x) \le 0 \}$), then $\mathcal{S}$ is forward invariant if, for all states on its boundary ($\{x \mid B(x)=0\}$), the time derivative of $B$ along the system's trajectories is non-positive:
$$
\nabla B(x) \cdot f(x) \le 0 \quad \forall x \text{ s.t. } B(x)=0
$$
This condition geometrically ensures that the vector field $f(x)$ does not point out of the set $\mathcal{S}$ at its boundary.

Barrier certificates are related to but distinct from the more familiar **Lyapunov functions** used in stability analysis [@problem_id:4238656]. A Lyapunov function $V(x)$ proves convergence to an equilibrium by requiring its derivative $\dot{V}(x)$ to be strictly negative everywhere, implying trajectories always move "downhill" on the surface of $V(x)$. A barrier certificate only imposes a condition on the boundary and does not require strict decrease, allowing for trajectories to move freely within the safe set. They are complementary tools: Lyapunov functions certify stability (a liveness property of convergence), while barrier certificates certify safety (invariance). For hybrid systems, both certificates must be extended with conditions on the discrete jumps, ensuring that a jump does not move the state out of a safe sublevel set or cause the Lyapunov function to increase.

#### Temporal Logic and Automata for Liveness

Complex liveness specifications, such as "a request is always eventually granted," are elegantly expressed using **Linear Temporal Logic (LTL)**. The automata-theoretic approach to model checking provides a powerful mechanism for verifying such properties. The core idea is to translate the LTL formula $\varphi$ into an equivalent **Nondeterministic Büchi Automaton (NBA)**, $\mathcal{A}_\varphi$ [@problem_id:4238657]. An NBA operates on infinite input words (system traces) and accepts a word if there is a run that visits its set of accepting states *infinitely often*.

This "infinitely often" acceptance condition is precisely what is needed to capture the essence of liveness. For a property like $\mathbf{G}\mathbf{F}p$ ("always eventually p," or "infinitely often p"), the corresponding Büchi automaton will have accepting states that can only be visited when $p$ is true. An accepting run of the automaton on a system trace thus corresponds to a system behavior where $p$ occurs infinitely often. To verify the property, one constructs a product of the system model and the property automaton $\mathcal{A}_\varphi$ and searches for an accepting cycle. The existence of such a cycle demonstrates that the system can exhibit a behavior satisfying the property.

### Pathologies in Hybrid Systems: Zeno Behavior

A unique challenge in hybrid systems is the possibility of **Zeno behavior**, where a system undergoes an infinite number of discrete jumps in a finite amount of time [@problem_id:4238609]. The classic example is a bouncing ball with a coefficient of restitution less than one. The time between successive bounces forms a convergent geometric series, meaning the ball bounces infinitely often before coming to rest at a finite "Zeno time" $T_{\text{Zeno}}$.

Zeno behavior has profound implications for reachability analysis. The state that the system converges to at the Zeno time—e.g., the ball at rest with $(y,v)=(0,0)$—is an **accumulation point** of the trajectory. This point belongs to the *closure* of the reachable set, $\overline{\mathcal{R}(T_{\text{Zeno}})}$, but it is not reachable by any finite number of jumps. If this accumulation point lies in a hazard set, an analysis that only computes the set of states reachable in a finite number of steps will miss the violation, leading to an unsound declaration of safety [@problem_id:4238609].

Furthermore, Zeno behavior can interfere with liveness. Because time "stops" at $T_{\text{Zeno}}$, any liveness property that requires time to diverge to infinity (e.g., visiting a goal set at arbitrarily large times) may be rendered unsatisfiable. In many cases, Zeno behavior is an artifact of an over-idealized model. A common resolution is to refine the model, for instance, by adding a "sticking" mode to the bouncing ball when its kinetic energy drops below a threshold. This regularization eliminates the infinite sequence of jumps, ensures time diverges, and can make certain liveness specifications, such as "eventually always on the ground" ($\mathbf{F}\mathbf{G}(y=0)$), satisfiable [@problem_id:4238609]. Sound verification of hybrid systems must therefore either rule out Zeno behavior or explicitly reason about its consequences.