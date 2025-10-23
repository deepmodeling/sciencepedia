## Introduction
In any control strategy with a finite look-ahead, a fundamental paradox exists: how can we be sure that a series of locally optimal decisions will not lead to a long-term dead end? This is the central challenge for Model Predictive Control (MPC), where a controller repeatedly plans the best course of action over a limited future horizon. Without a guarantee of future viability, a plan that seems brilliant now might steer the system into a state from which no safe move is possible, causing a catastrophic failure.

This article tackles this problem by introducing the core concept of **recursive feasibility**. It provides an ironclad promise that if a feasible plan exists now, a feasible plan will exist at every moment in the future. We will explore how this powerful guarantee is constructed and why it is the bedrock of safe and stable [predictive control](@article_id:265058). The article is divided into two main parts. In "Principles and Mechanisms," we will dissect the theoretical machinery behind recursive feasibility, including the critical roles of the [terminal set](@article_id:163398) and terminal cost. Following that, "Applications and Interdisciplinary Connections" will demonstrate how this elegant theory is adapted to solve complex real-world problems and builds bridges to diverse fields like economics, robotics, and artificial intelligence.

## Principles and Mechanisms

Imagine you are captaining a ship through a treacherous archipelago, with a map that only shows you the next few miles. At every moment, you plot what seems to be the "optimal" course for the next hour—the fastest, most fuel-efficient path you can find. But here's the catch: what if that locally optimal path leads you into a dead-end strait, from which no safe passage exists? Your brilliant short-term plan has led to long-term disaster. This is the central dilemma of any predictive controller with a finite "sight" into the future. How can we trust a myopic planner to navigate a world of constraints without eventually trapping itself?

### The Planner's Paradox: How to Avoid Painting Yourself into a Corner

In the language of Model Predictive Control (MPC), this dilemma highlights a crucial distinction. For any given starting position, or **state**, we can define the set of all states from which it's *possible* to plot at least one safe course over our short [prediction horizon](@article_id:260979). Let's call this the **Set of Feasible Initial States**. It feels like a good start; if you're in this set, you can at least make your next move.

However, there's a more exclusive, and far more important, club: the **Region of Attraction (ROA)**. This is the set of all starting states from which our MPC-piloted ship is *guaranteed* to reach its final destination (the origin) safely, without ever running aground (violating constraints) along the way.

Why are these two sets not the same? The reason is profound and lies at the very heart of receding-horizon control. Just because you can find a feasible plan *now* doesn't mean that after you take the first step of that plan, you will still be able to find a feasible plan *from your new position*. You might have navigated yourself onto a proverbial sandbar. The initial plan was feasible, but it led to a state of future infeasibility. The Region of Attraction, therefore, excludes all those tempting but ultimately treacherous starting points [@problem_id:1583563].

The guarantee that feasibility at one moment implies feasibility at the next, and the next, and so on forever, is the solution to our paradox. It’s a property so vital that it has its own name: **recursive feasibility**. It's the promise that our controller will never, ever get stuck. But how can we make such a powerful promise?

### The "Get Out of Jail Free" Card: A Safe Harbor in State Space

The genius of modern MPC lies in a simple but powerful idea: ensure that every short-term plan, no matter what, ends in a pre-defined "safe harbor." This safe harbor is a region in the state space known as the **[terminal set](@article_id:163398)**, denoted $\mathcal{X}_f$. Think of it as a designated base camp for a mountain climber. No matter what route you plan for the next hour, it absolutely must end at this known, safe location.

What makes a set "safe"? It must obey a few commonsense rules. Let's imagine we have a very simple, reliable backup plan for when we're in this base camp: a simple feedback controller, say $u = Kx$. This is our **terminal controller**. For the [terminal set](@article_id:163398) $\mathcal{X}_f$ to be a true safe harbor, it must satisfy three conditions [@problem_id:2736421]:

1.  **It must be within bounds.** The [terminal set](@article_id:163398) must be a subset of the overall allowed state space, $\mathcal{X}_f \subseteq \mathcal{X}$. (Your base camp must actually be on the mountain).

2.  **The backup plan must be usable.** For any state $x$ inside the [terminal set](@article_id:163398) $\mathcal{X}_f$, our simple terminal controller must produce a control input $u = Kx$ that respects the input constraints, $Kx \in \mathcal{U}$. (The path leading from the base camp must be easy enough for you to follow without special equipment).

3.  **The backup plan must keep you safe.** For any state $x$ inside the [terminal set](@article_id:163398) $\mathcal{X}_f$, applying the terminal controller must result in a next state that is *also* inside $\mathcal{X}_f$. This property is called **positive invariance**. Mathematically, $(A+BK)x \in \mathcal{X}_f$. (Following the marked path from the base camp guarantees you stay on safe trails).

Choosing such a set is not trivial. Consider a simple system where we want to define a [terminal set](@article_id:163398) as a square, $\mathcal{X}_f = \{x \in \mathbb{R}^2 : \|x\|_{\infty} \le c\}$ for some constant $c$. If we choose $c$ too large, say $c=1.5$, we might find a state on the boundary of this square where our simple controller $u=Kx$ demands an input that violates its limits (e.g., requires an input of norm $0.9$ when the limit is $0.6$). This "safe harbor" turns out to have a cliff at its edge! Only by choosing a smaller square, say with $c=1$, can we ensure all three conditions hold, creating a truly valid [terminal set](@article_id:163398) [@problem_id:2736421]. This careful construction is the first step toward our guarantee.

### The Chain of Guarantees: The Magic of the Shift-and-Append

Now we can connect the dots. How does having a [terminal set](@article_id:163398) guarantee recursive feasibility? Through an elegant inductive argument known as the **"shift-and-append"** strategy [@problem_id:2746593].

Suppose at time $k$, we are at state $x(k)$ and our MPC optimizer finds a beautiful, optimal plan—a sequence of inputs $\{u_{0|k}^\star, u_{1|k}^\star, \dots, u_{N-1|k}^\star\}$. This plan is feasible by definition, and its last state, $x_{N|k}^\star$, lands squarely in our [terminal set](@article_id:163398) $\mathcal{X}_f$. We apply the first input, $u(k) = u_{0|k}^\star$, and the system moves to a new state, $x(k+1)$.

Now it's time $k+1$. The world has changed. Do we know for sure that a feasible plan exists from $x(k+1)$? Yes! We can prove it by constructing one. We don't need to be clever; we just need to show that *at least one* feasible plan exists. Here’s the recipe:

1.  **Shift:** Take the tail of our previous optimal plan: $\{u_{1|k}^\star, \dots, u_{N-1|k}^\star\}$. This sequence is already known to be feasible in terms of state and input constraints.

2.  **Append:** We have a one-step gap at the end. We fill it using our simple, reliable terminal controller. Since the state at the end of the shifted sequence is $x_{N|k}^\star$, which is in the safe harbor $\mathcal{X}_f$, we append the input $u_{N-1|k+1}^c = K x_{N|k}^\star$.

This newly constructed "candidate" sequence is guaranteed to be feasible. Why? The "shift" part is feasible because it was part of a feasible plan a moment ago. The "append" part is feasible because our [terminal set](@article_id:163398) was specifically designed to ensure that for any $x \in \mathcal{X}_f$, the control $Kx$ is admissible and the next state $(A+BK)x$ lands back in $\mathcal{X}_f$.

So, at time $k+1$, we hand this perfectly valid, if perhaps a bit clumsy, plan to our optimizer. The optimizer is guaranteed to find a solution that is at least as good as this one, and likely much better. The key is, it will *always* find a solution. The chain of feasibility is never broken. This is the simple, beautiful mechanism that provides the ironclad guarantee of recursive feasibility [@problem_id:2746593] [@problem_id:2746570].

### From Survival to Success: The Deeper Role of the Terminal Cost

We've ensured our ship never runs aground. But we also want to ensure it actually reaches its destination. This is the role of the cost function, and in particular, the **terminal cost**, $V_f(x_N) = x_N^\top P x_N$. This isn't just an arbitrary penalty tacked on at the end; it's a proxy for the entire cost of the journey from the edge of our map to the final destination.

What is the "right" terminal cost? In a stroke of mathematical elegance, it turns out that the perfect choice for the matrix $P$ is the solution to the **Discrete-time Algebraic Riccati Equation (DARE)** from the unconstrained infinite-horizon LQR problem [@problem_id:2736392]. This is a deep result. It means that the terminal cost $x_N^\top P x_N$ is not an approximation—it is the *exact* optimal cost-to-go from state $x_N$ to the origin, assuming no constraints are active from that point on. Our myopic planner, upon reaching the [terminal set](@article_id:163398), is suddenly imbued with the wisdom of an infinite-horizon planner. This aligns the short-term objective with the true long-term goal, dramatically improving performance [@problem_id:2724661].

This choice of terminal cost, paired with the [terminal set](@article_id:163398), does something remarkable: it turns the MPC's optimal cost into a **Lyapunov function** for the [closed-loop system](@article_id:272405) [@problem_id:2884357] [@problem_id:2746605]. The logic is a beautiful extension of our shift-and-append argument. When we compare the optimal cost at time $k+1$ with the optimal cost at time $k$, we find that the cost is guaranteed to decrease at every step. The decrease comes from the fact that our "backup plan" (rolling out the terminal controller) is guaranteed to decrease the terminal cost. Since the true optimizer can do at least as well as the backup plan, the total cost must go down.

This dual role is the cornerstone of stabilizing MPC: the **[terminal set](@article_id:163398)** $\mathcal{X}_f$ guarantees we can always keep playing the game (recursive feasibility), and the **terminal cost** $V_f(x)$ guarantees we are always winning it ([asymptotic stability](@article_id:149249)) [@problem_id:2724726].

### Embracing the Storm: Feasibility in an Uncertain World

Our discussion so far has assumed a perfect world—our ship moves exactly as our model predicts. What happens when a disturbance hits, like a gust of wind or an ocean current?

Imagine we used a very rigid [terminal constraint](@article_id:175994): our plan *must* end at a single point, $x_N = 0$. This seems reasonable. But if a disturbance knocks our ship slightly off course, the new position might be one from which it's physically impossible to reach the target point in the remaining time with our limited engine power. The optimization becomes infeasible; our controller throws up its hands and fails [@problem_id:2724796].

The remedy, once again, is to build in flexibility. Instead of aiming for a single point, we must aim for a region. But not just any region. In a stormy world, we need a **robustly positively invariant (RPI) set**. This is a special kind of [terminal set](@article_id:163398) designed to be a safe harbor against the *worst-case* disturbance. For any state inside this set, and for *any* possible disturbance from the bounded set $\mathcal{W}$, our terminal controller can keep the next state within the set [@problem_id:2746570].

By forcing our predictive plan to terminate inside this "fattened," robust set, we can once again construct a candidate solution for the next time step that is feasible no matter what the disturbance was. We have recovered our guarantee of recursive feasibility, but now it's a much stronger promise—a promise kept not just in calm weather, but in a storm. This robust approach, often realized through "tube-based MPC," shows the beautiful unity and adaptability of the core principle: to ensure long-term success, every short-term plan must end in a provably safe region, designed with the challenges of the real world in mind [@problem_id:2724796].