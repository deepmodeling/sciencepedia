## Introduction
In the dynamic world of [stochastic analysis](@entry_id:188809), controlling the erratic behavior of random processes over time is a central challenge. From predicting the peak of a stock price to ensuring the stability of a numerical simulation, we need rigorous tools to bound the maximum value a process might attain. This need gives rise to some of the most elegant and powerful results in modern probability theory: Doob's maximal inequalities and the concept of [uniform integrability](@entry_id:199715). These concepts provide the critical link between a process's value at a single moment and its behavior over an entire trajectory. This article delves into the theoretical heart of these tools and their far-reaching implications, bridging the gap between abstract definitions and practical application.

The journey begins in the **Principles and Mechanisms** chapter, where we will rigorously define Doob's weak $L^1$ and strong $L^p$ inequalities, explore the counterexamples that highlight their limitations, and introduce [uniform integrability](@entry_id:199715) as the crucial property needed for convergence and extended optional stopping. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate how these theoretical pillars support foundational results like the Doob-Meyer decomposition and the Burkholder-Davis-Gundy inequalities, and how they are applied in [mathematical finance](@entry_id:187074), [stochastic control](@entry_id:170804), and [numerical analysis](@entry_id:142637). Finally, the **Hands-On Practices** section provides curated problems to solidify your understanding, challenging you to construct key counterexamples and apply the theory to concrete stochastic processes.

## Principles and Mechanisms

In the study of stochastic processes, a central challenge is to understand and control the behavior of a process over an entire interval of time, not just at a single point. This often translates into a need for quantitative bounds on the maximum value a process is likely to attain. For instance, in [financial modeling](@entry_id:145321), one might want to know the probability that a stock price, modeled as a [stochastic process](@entry_id:159502), will exceed a certain critical threshold. Doob's maximal inequalities provide a powerful and elegant set of tools for exactly this purpose. They connect the overall maximum of a [submartingale](@entry_id:263978) to its value at the final time. This chapter will explore the principles behind these inequalities, the crucial role of [uniform integrability](@entry_id:199715) in extending their underlying logic, and the technical foundations upon which these theories are built.

### Controlling the Maximum: Doob's Maximal Inequalities

Let us consider a [submartingale](@entry_id:263978) $(X_t)_{t \in [0,T]}$ adapted to a filtration $(\mathcal{F}_t)_{t \in [0,T]}$. We are interested in its **running [supremum](@entry_id:140512)** (or **maximal process**), defined as:

$$X_t^* := \sup_{0 \le s \le t} X_s$$

The maximal inequalities provide bounds on the distribution and moments of $X_T^*$ in terms of the distribution and moments of $X_T$.

#### The Weak $L^1$ Inequality

The most fundamental of these bounds is the weak $L^1$ maximal inequality. In its simplest form, it applies to nonnegative submartingales.

**Theorem (Doob's Weak $L^1$ Maximal Inequality):** Let $(X_t)_{t \in [0,T]}$ be a right-continuous, nonnegative, integrable [submartingale](@entry_id:263978). Then for any constant $\lambda > 0$, we have:

$$\mathbb{P}(X_T^* \ge \lambda) \le \frac{1}{\lambda} \mathbb{E}[X_T]$$

This inequality is remarkably powerful. It states that the probability of the process ever reaching a high level $\lambda$ is constrained by the average value of the process at the terminal time $T$.

The proof of this theorem is instructive as it introduces a technique that is central to [martingale theory](@entry_id:266805): the use of [stopping times](@entry_id:261799). Consider the first time the process $X_t$ reaches or exceeds $\lambda$, defined as the [stopping time](@entry_id:270297) $\tau = \inf\{t \in [0,T] : X_t \ge \lambda\}$. The event we want to bound, $\{X_T^* \ge \lambda\}$, is precisely the event $\{\tau \le T\}$. By the Optional Sampling Theorem, for this bounded stopping time, we have $\mathbb{E}[X_\tau] \le \mathbb{E}[X_T]$. We can then write:

$\mathbb{E}[X_T] \ge \mathbb{E}[X_\tau] = \int_{\{\tau \le T\}} X_\tau d\mathbb{P} + \int_{\{\tau > T\}} X_\tau d\mathbb{P}$

On the event $\{\tau \le T\}$, by the definition of $\tau$ and [right-continuity](@entry_id:170543), we have $X_\tau \ge \lambda$. Since $X_t$ is a nonnegative process, the second integral is nonnegative. This gives:

$\mathbb{E}[X_T] \ge \int_{\{\tau \le T\}} \lambda d\mathbb{P} + 0 = \lambda \mathbb{P}(\tau \le T) = \lambda \mathbb{P}(X_T^* \ge \lambda)$

Rearranging this gives the inequality. The assumption of nonnegativity is critical here. It is what allows us to discard the integral over $\{\tau > T\}$. Moreover, in more advanced proofs extending this result to continuous time without assuming [uniform integrability](@entry_id:199715), nonnegativity is essential for applying Fatou's Lemma to justify the optional sampling step itself [@problem_id:2973876].

The inequality can be generalized to any integrable [submartingale](@entry_id:263978) (not necessarily nonnegative) by applying it to the nonnegative [submartingale](@entry_id:263978) $X_t^+ = \max(X_t, 0)$. This yields the general form:

$$\mathbb{P}(X_T^* \ge \lambda) \le \frac{1}{\lambda} \mathbb{E}[X_T^+]$$

For a nonnegative process, $X_T^+ = X_T$, and we recover the original statement [@problem_id:2973876].

The assumption of [integrability](@entry_id:142415), $\mathbb{E}[|X_T|]  \infty$, is not a mere technicality. If it fails, the inequality can become vacuous, providing no useful information. For example, one can construct an [adapted process](@entry_id:196563) $(X_t)_{t \in [0,T]}$ that is a [submartingale](@entry_id:263978) but for which $\mathbb{E}[X_T]=\infty$. Applying the inequality via an approximation argument yields $\mathbb{P}(X_T^* \ge \lambda) \le \infty$, a trivial statement [@problem_id:2973852].

#### The $L^p$ Inequalities for $p > 1$

For moments higher than $p=1$, Doob established a stronger set of inequalities that bound the $L^p$ norm of the maximal process.

**Theorem (Doob's $L^p$ Maximal Inequality):** Let $(X_t)_{t \in [0,T]}$ be a right-continuous [submartingale](@entry_id:263978) and let $p>1$. Then:

$$\mathbb{E}[(|X_T^*|)^p] \le \left(\frac{p}{p-1}\right)^p \mathbb{E}[|X_T|^p]$$

If $X_t$ is a nonnegative [submartingale](@entry_id:263978), the inequality holds without the [absolute values](@entry_id:197463). This result shows that if the terminal value $X_T$ has a finite $p$-th moment, then so does the entire path's [supremum](@entry_id:140512) $X_T^*$, and it provides a quantitative relationship between them. The constant $(\frac{p}{p-1})^p$ is sharp.

To see this inequality in action, consider a process $X_t = \int_0^t \sigma(s) dW_s$ where $W_t$ is a standard Brownian motion. This process is a [continuous martingale](@entry_id:185466). Since the [absolute value function](@entry_id:160606) $x \mapsto |x|$ is convex, the process $|X_t|$ is a [submartingale](@entry_id:263978), by Jensen's inequality for conditional expectations. We can therefore apply the $L^p$ inequality to get a bound on the [expected maximum](@entry_id:265227) deviation of the process from its starting point of zero [@problem_id:2973843]:

$$\mathbb{E}\left[\left(\sup_{0 \le t \le 1} |X_t|\right)^p\right] \le \left(\frac{p}{p-1}\right)^p \mathbb{E}[|X_1|^p]$$

For a specific choice like $\sigma(t) = \sqrt{2}t^\alpha$, the term $\mathbb{E}[|X_1|^p]$ can be computed explicitly, as $X_1$ is a Gaussian random variable whose variance is determined by the Itô [isometry](@entry_id:150881), $\mathbb{E}[X_1^2] = \int_0^1 \sigma(s)^2 ds$. This allows for a concrete, closed-form bound on the $p$-th moment of the [maximal function](@entry_id:198115), illustrating how abstract inequalities translate into tangible estimates for specific models [@problem_id:2973843].

#### The Gap at $p=1$: Failure of the Strong $L^1$ Inequality

An observant student might ask what happens as $p \to 1$ in the $L^p$ inequality. The constant $C_p = (\frac{p}{p-1})^p$ diverges to infinity. This suggests that a "strong" $L^1$ inequality of the form $\mathbb{E}[|X_T^*|] \le C \mathbb{E}[|X_T|]$ might not exist for any universal constant $C$.

This is indeed the case. We can construct a simple [discrete-time martingale](@entry_id:191523) that serves as a powerful [counterexample](@entry_id:148660). Consider a process that starts at $X_0=1$. At each step, it either doubles in value with probability $0.5$ or drops to zero permanently with probability $0.5$. This can be written as $X_{n+1} = 2X_n Y_{n+1}$ where $Y_{n+1}$ are i.i.d. Bernoulli$(0.5)$ random variables. One can verify that this is a martingale with $\mathbb{E}[X_n]=1$ for all $n$. However, the maximum value attained, $X_n^* = \sup_{k \le n} X_k$, has an infinite expectation in the limit. With probability $(0.5)^{k+1}$, the process follows the path $1, 2, 4, \dots, 2^k, 0, \dots$, for which the maximum is $2^k$. Summing over all possible paths reveals that $\mathbb{E}[X_\infty^*] = \sum_{k=0}^\infty 2^k \cdot (1/2)^{k+1} = \infty$.

Here we have a process whose $L^1$ norm is uniformly bounded ($\sup_n \mathbb{E}[|X_n|] = 1$), yet the expectation of its [supremum](@entry_id:140512) is infinite [@problem_id:2973850]. This demonstrates a fundamental gap between the weak control over tail probabilities given by the weak $L^1$ inequality and the strong control over moments for $p>1$. To bridge this gap and understand convergence properties for $p=1$, we need a stronger condition than simple $L^1$-[boundedness](@entry_id:746948). This condition is [uniform integrability](@entry_id:199715).

### Uniform Integrability: The Key to Convergence and Optional Stopping

Uniform [integrability](@entry_id:142415) is arguably one of the most important concepts in modern probability theory. It is the precise condition needed to, among other things, interchange limits and expectations, and to extend the [optional stopping theorem](@entry_id:267890) to a much wider class of [stopping times](@entry_id:261799).

#### Defining Uniform Integrability

A family of integrable random variables $\mathcal{X} \subset L^1(\Omega, \mathcal{F}, \mathbb{P})$ is said to be **[uniformly integrable](@entry_id:202893) (UI)** if the amount of mass in the collective "tails" of their distributions can be made arbitrarily small, uniformly over the entire family. Formally:

$$\lim_{K\to\infty} \sup_{X\in\mathcal{X}} \mathbb{E}\big[|X|\mathbf{1}_{\{|X|K\}}\big] = 0$$

where $\mathbf{1}_{\{\cdot\}}$ is the indicator function.

This is a stronger condition than simple $L^1$-boundedness (i.e., $\sup_{X \in \mathcal{X}} \mathbb{E}[|X|]  \infty$). For instance, the sequence of random variables $X_n = n \mathbf{1}_{[0, 1/n]}$ on the unit interval with Lebesgue measure is $L^1$-bounded, as $\mathbb{E}[|X_n|] = n \cdot (1/n) = 1$ for all $n$. However, it is not [uniformly integrable](@entry_id:202893), because for any $K$, we can find an $n>K$ such that the entire mass of $X_n$ lies in its tail beyond $K$ [@problem_id:2973879]. Uniform integrability rules out this kind of behavior, where probability mass can "[escape to infinity](@entry_id:187834)".

An alternative and useful characterization is that a family $\mathcal{X}$ is [uniformly integrable](@entry_id:202893) if and only if for any sequence $(X_n)$ from $\mathcal{X}$ and any sequence of events $(A_n)$ with $\mathbb{P}(A_n) \to 0$, we have $\mathbb{E}[|X_n|\mathbf{1}_{A_n}] \to 0$ [@problem_id:2973879]. This property is sometimes called uniform [absolute continuity](@entry_id:144513) with respect to the measure $\mathbb{P}$.

#### Criteria for Uniform Integrability

While the definition is fundamental, it can be difficult to check directly. Fortunately, there are several powerful criteria.

The most general is the **de la Vallée-Poussin Theorem**, which states that a family $\mathcal{X}$ is [uniformly integrable](@entry_id:202893) if and only if there exists a convex, increasing function $\Phi: [0, \infty) \to [0, \infty)$ with [superlinear growth](@entry_id:167375) (i.e., $\lim_{x\to\infty} \Phi(x)/x = \infty$) such that the family is bounded in "$\Phi$-mean":

$$\sup_{X\in\mathcal{X}} \mathbb{E}\big[\Phi(|X|)\big]  \infty$$
[@problem_id:2973848] [@problem_id:2973879]

A direct and extremely useful corollary of this theorem arises by choosing $\Phi(x)=x^p$ for some $p>1$. This function satisfies the conditions of the theorem. This gives us a simple and practical test:

**A family of random variables that is bounded in $L^p$ for some $p>1$ is [uniformly integrable](@entry_id:202893).**

The proof is straightforward. If $\sup_X \mathbb{E}[|X|^p] \le C  \infty$, then for any $X$ in the family:
$\mathbb{E}[|X|\mathbf{1}_{\{|X|K\}}] = \mathbb{E}[|X|^p |X|^{1-p} \mathbf{1}_{\{|X|K\}}] \le K^{1-p} \mathbb{E}[|X|^p] \le C K^{1-p}$
Since $p>1$, the term $K^{1-p}$ goes to zero as $K \to \infty$, which proves [uniform integrability](@entry_id:199715) [@problem_id:2973879].

This criterion forms a crucial bridge back to Doob's $L^p$ inequalities. If we have a sequence of martingales $(M_t^{(n)})$ whose terminal values are bounded in $L^p$ for $p>1$ (i.e., $\sup_n \mathbb{E}[|M_T^{(n)}|^p]  \infty$), we can conclude that the family $\{M_T^{(n)}\}$ is [uniformly integrable](@entry_id:202893). By Doob's $L^p$ inequality, this also implies that the family of running suprema, $\{\sup_t |M_t^{(n)}|\}$, is bounded in $L^p$ and therefore also [uniformly integrable](@entry_id:202893) [@problem_id:2973848] [@problem_id:2973879].

#### Uniform Integrability and Martingale Theory

The true power of [uniform integrability](@entry_id:199715) is revealed in its connection to [martingale convergence](@entry_id:262440) and optional stopping.

A cornerstone result is the **Martingale Convergence Theorem**. It states that a right-continuous [submartingale](@entry_id:263978) $(M_t)_{t \ge 0}$ converges [almost surely](@entry_id:262518) to a random variable $M_\infty$ as $t \to \infty$ if and only if $\sup_t \mathbb{E}[|M_t|]  \infty$. The convergence also happens in $L^1$ (i.e., $\mathbb{E}[|M_t - M_\infty|] \to 0$) if and only if the [martingale](@entry_id:146036) is [uniformly integrable](@entry_id:202893). The counterexample from [@problem_id:2973850] is a non-UI martingale which converges [almost surely](@entry_id:262518) to $0$, but not in $L^1$, since $\mathbb{E}[|X_n|] = 1$ for all $n$.

Perhaps the most profound application is in the **Optional Stopping Theorem (OST)**. The elementary version of the theorem requires the stopping time to be bounded. Uniform integrability allows us to extend it to a vast class of unbounded [stopping times](@entry_id:261799).

**Theorem (Optional Stopping):** Let $(M_t)_{t \ge 0}$ be a [uniformly integrable](@entry_id:202893) right-[continuous martingale](@entry_id:185466). Then for any two [stopping times](@entry_id:261799) $S$ and $T$ with $S \le T$, we have:

$$\mathbb{E}[M_T | \mathcal{F}_S] = M_S$$

In particular, $\mathbb{E}[M_T] = \mathbb{E}[M_S]$, and for any stopping time $\tau$, $\mathbb{E}[M_\tau] = \mathbb{E}[M_0]$.

The assumption of [uniform integrability](@entry_id:199715) is essential. To see why, consider a stopping time $T$ that is not necessarily bounded. A standard proof technique involves approximating $T$ by the sequence of bounded [stopping times](@entry_id:261799) $T_n = T \wedge n$. For each $n$, the elementary OST applies: $\mathbb{E}[M_{T_n}] = \mathbb{E}[M_0]$. We want to take the limit as $n \to \infty$. We know that $T_n \to T$ [almost surely](@entry_id:262518), and by path continuity, $M_{T_n} \to M_T$ almost surely. However, to conclude that $\lim_{n\to\infty} \mathbb{E}[M_{T_n}] = \mathbb{E}[M_T]$, we need $L^1$ convergence, not just [almost sure convergence](@entry_id:265812). A fundamental theorem of measure theory states that [almost sure convergence](@entry_id:265812) implies $L^1$ convergence if and only if the sequence is [uniformly integrable](@entry_id:202893). Thus, the [uniform integrability](@entry_id:199715) of the family $\{M_{T_n}\}$ is precisely the condition required to justify passing the limit through the expectation [@problem_id:2973856].

The failure of OST without [uniform integrability](@entry_id:199715) can be starkly illustrated. Consider a standard Brownian motion $(W_t)_{t \ge 0}$ starting at $W_0=0$. This is a [martingale](@entry_id:146036), but it is not [uniformly integrable](@entry_id:202893) as its variance grows with time. Let $T = \inf\{t \ge 0 : W_t = 1\}$ be the first time it hits the level 1. It is a classic result that $T$ is finite [almost surely](@entry_id:262518), but $\mathbb{E}[T]=\infty$. By the definition of $T$ and path continuity, $W_T = 1$. Therefore, $\mathbb{E}[W_T] = 1$. However, $\mathbb{E}[W_0]=0$. The conclusion of OST, $1=0$, is false [@problem_id:2973861]. The theorem does not apply because the underlying martingale is not [uniformly integrable](@entry_id:202893).

Conversely, when the conditions are met, the OST is a powerful tool for calculation. Consider the geometric Brownian motion $X_t = \exp(\theta W_t - \frac{1}{2}\theta^2 t)$, which is a martingale with $X_0=1$. One can show this process is bounded in $L^p$ for $p>1$ on any finite interval $[0,T]$, and is therefore [uniformly integrable](@entry_id:202893). Applying the OST to the bounded stopping time $\tau \wedge T$, where $\tau$ is the first time $X_t$ hits a level $\lambda > 1$, allows for a straightforward derivation of the weak $L^1$ inequality for this specific process: $\mathbb{P}(\sup_{0\le t \le T} X_t \ge \lambda) \le 1/\lambda$ [@problem_id:2973866]. This demonstrates a beautiful synergy between SDEs, [uniform integrability](@entry_id:199715), and optional stopping.

### Technical Foundations: Measurability and Path Properties

Underlying all these powerful theorems is a subtle but crucial technical point: for the objects we discuss to be well-defined, they must be measurable. For instance, in an expression like $\mathbb{E}[X_t^*]$, the running supremum $X_t^*$ must be a random variable, meaning it is a measurable function from the [sample space](@entry_id:270284) $\Omega$ to the real numbers.

The running [supremum](@entry_id:140512) is defined as $X_t^* = \sup_{0 \le s \le t} X_s$. For $X_t^*$ to be $\mathcal{F}_t$-measurable, the set $\{\omega \in \Omega : X_t^*(\omega) > c\}$ must be in $\mathcal{F}_t$ for every constant $c$. This event can be written as $\bigcup_{s \in [0,t]} \{X_s > c\}$. A $\sigma$-algebra is closed under countable unions, but this is an uncountable union. This presents a potential problem.

The standard resolution relies on two key assumptions about the process and the filtration, often referred to as the **usual conditions**.

1.  **Path Regularity:** If the process $(X_t)$ has [sample paths](@entry_id:184367) that are [almost surely](@entry_id:262518) right-continuous with left limits (càdlàg), we can replace the supremum over the uncountable set $[0,t]$ with a supremum over a [countable dense subset](@entry_id:147670), such as the rational numbers $\mathbb{Q} \cap [0,t]$. Since $X_q$ is $\mathcal{F}_q$-measurable (and thus $\mathcal{F}_t$-measurable) for each rational $q$, the [supremum](@entry_id:140512) over a [countable set](@entry_id:140218) of these variables is also $\mathcal{F}_t$-measurable. More robustly, it can be shown that an [adapted process](@entry_id:196563) with [càdlàg paths](@entry_id:638012) is progressively measurable, which directly implies its running supremum is adapted [@problem_id:2973880].

2.  **Filtration Regularity:** A standard argument used in many texts shows that for a càdlàg [adapted process](@entry_id:196563), the supremum $X_t^*$ is always measurable with respect to $\mathcal{F}_{t+} := \bigcap_{u > t} \mathcal{F}_u$. If we impose the standard assumption that the [filtration](@entry_id:162013) is **right-continuous**, meaning $\mathcal{F}_t = \mathcal{F}_{t+}$ for all $t$, this "upgrades" the [measurability](@entry_id:199191) to $\mathcal{F}_t$-[measurability](@entry_id:199191) [@problem_id:2973880].

In summary, the usual conditions of a complete, [right-continuous filtration](@entry_id:200130), combined with the assumption of [càdlàg paths](@entry_id:638012) for the [submartingale](@entry_id:263978), ensure that all the random variables involved in Doob's inequalities and the Optional Stopping Theorem, particularly the running [supremum](@entry_id:140512) $X_t^*$, are well-defined and have the appropriate measurability properties. This provides the rigorous foundation upon which these powerful principles and mechanisms rest [@problem_id:2973880].