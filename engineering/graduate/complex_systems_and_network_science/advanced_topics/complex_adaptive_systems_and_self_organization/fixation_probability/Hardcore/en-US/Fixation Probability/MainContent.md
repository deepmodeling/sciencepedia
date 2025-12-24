## Introduction
When a new trait emerges in a population, what is its ultimate fate? Will it disappear, a transient blip in the [gene pool](@entry_id:267957), or will it spread to every individual, becoming a permanent feature? This question of 'fixation' is a central problem in [evolutionary dynamics](@entry_id:1124712), governing processes from the spread of a [beneficial mutation](@entry_id:177699) to the emergence of [drug resistance](@entry_id:261859) in cancer. Predicting the outcome is challenging, as it hinges on a delicate balance between deterministic [selective pressures](@entry_id:175478) and the inherent randomness of reproduction in a finite population, a phenomenon known as [genetic drift](@entry_id:145594).

This article provides a comprehensive guide to understanding and calculating the probability of fixation. We will navigate the theoretical landscape, starting with first principles and building towards advanced, real-world applications. The first chapter, **Principles and Mechanisms**, establishes the mathematical foundation. We will derive the classic fixation probability formula using the Moran process and then generalize these ideas with the powerful diffusion approximation framework, extending our analysis to structured populations and stochastic environments.

Building on this theoretical core, the second chapter, **Applications and Interdisciplinary Connections**, demonstrates the remarkable versatility of fixation probability. We will explore how these concepts provide critical insights into [evolutionary dynamics](@entry_id:1124712) on [complex networks](@entry_id:261695), the spatial spread of alleles in ecology, the progression of diseases like cancer, and even the behavior of computational [genetic algorithms](@entry_id:172135).

Finally, to translate theory into practice, the **Hands-On Practices** chapter offers a curated set of problems. These exercises will challenge you to apply the learned concepts, from solving fundamental models to implementing numerical solutions for complex, structured systems, solidifying your grasp of this essential tool for analyzing stochastic processes.

## Principles and Mechanisms

This chapter delineates the fundamental principles governing the probability of fixation. We begin by introducing a [canonical model](@entry_id:148621), the Moran process, to formally define fixation probability and derive its exact analytical form. We then transition to the powerful framework of diffusion approximations, which allows for the analysis of more complex scenarios involving [frequency-dependent selection](@entry_id:155870). Subsequently, we explore advanced topics, including large-deviation theory for rare events, the influence of [population structure](@entry_id:148599), and the impact of stochastic environments. Throughout this exploration, we will connect the theoretical concepts to tangible examples, clarifying the intricate interplay between selection, drift, and population size.

### The Moran Process and the Definition of Fixation Probability

A cornerstone of theoretical [population genetics](@entry_id:146344) is the **Moran process**, a stochastic model that describes the evolution of a finite population with overlapping generations. Consider a well-mixed population of fixed size $N$. In this population, there are two types of individuals: **mutants** and **residents**. Let us denote the number of mutants by $k$, where $k$ can range from $0$ to $N$. The remaining $N-k$ individuals are residents.

The state of the system is entirely described by the number of mutants, $k$. The states $k=0$ and $k=N$ are special. If $k=0$, all individuals are residents, and no mutants can be born. This is the **extinction** state. Conversely, if $k=N$, the entire population consists of mutants, and no residents can be born. This is the **fixation** state. Both extinction and fixation are **[absorbing states](@entry_id:161036)**: once the process enters one of these states, it can never leave. The states $k \in \{1, 2, \dots, N-1\}$ are **transient**.

The dynamics of the Moran process proceed in discrete time steps. At each step, two events occur: a birth and a death.
1.  An individual is chosen for reproduction with a probability proportional to its **fitness**.
2.  An individual is chosen for death uniformly at random, and is replaced by the offspring from the first step.

Let the fitness of a mutant be $r$ and the fitness of a resident be $1$. Here, $r$ is the **[relative fitness](@entry_id:153028)** of the mutant. If $r>1$, the mutant is advantageous; if $r<1$, it is deleterious; and if $r=1$, it is neutral.

Given this [stochastic process](@entry_id:159502), we can now precisely define the central quantity of this chapter. The **fixation probability**, denoted $\rho_k$, is the probability that the population eventually reaches the fixation state ($k=N$), given that it starts with $k$ mutants. Formally, it is the probability that the random walk on the state space $\{0, 1, \dots, N\}$ hits the [absorbing boundary](@entry_id:201489) at $N$ before hitting the [absorbing boundary](@entry_id:201489) at $0$.

It is crucial to distinguish the fixation probability from the **fixation time**. The fixation probability $\rho_k$ is a dimensionless value between $0$ and $1$. In contrast, the fixation time is the number of steps (or generations) it takes for the process to reach an [absorbing state](@entry_id:274533). It has units of time and is a distinct random variable with its own expected value and distribution. There is no simple, universal relationship between the two quantities .

### Derivation of the Fixation Probability Formula

To calculate the fixation probability, we analyze the Moran process as a one-dimensional absorbing Markov chain. We first need the one-step [transition probabilities](@entry_id:158294). Let's denote the probability of the number of mutants increasing from $k$ to $k+1$ as $T_k^+$, and the probability of it decreasing to $k-1$ as $T_k^-$.

The total fitness of the population when there are $k$ mutants is $F_{\text{total}} = k \cdot r + (N-k) \cdot 1$.
A transition from $k$ to $k+1$ occurs if a mutant is chosen to reproduce and a resident is chosen to die. The probability of this is:
$$
T_k^+ = \left( \frac{kr}{kr + N-k} \right) \left( \frac{N-k}{N} \right)
$$
A transition from $k$ to $k-1$ occurs if a resident is chosen to reproduce and a mutant is chosen to die. The probability of this is:
$$
T_k^- = \left( \frac{N-k}{kr + N-k} \right) \left( \frac{k}{N} \right)
$$
The probability that the number of mutants remains unchanged, $T_k^0$, is $1 - T_k^+ - T_k^-$.

The fixation probability $\rho_k$ must satisfy a [consistency condition](@entry_id:198045). By conditioning on the outcome of the first step, the probability of eventually fixing from state $k$ is the weighted average of the fixation probabilities from the states reachable in one step. This gives the **backward Kolmogorov equation** for the stationary quantity $\rho_k$:
$$
\rho_k = T_k^+ \rho_{k+1} + T_k^- \rho_{k-1} + T_k^0 \rho_k
$$
This equation holds for all transient states $k \in \{1, \dots, N-1\}$. Rearranging, we get a simpler [recurrence relation](@entry_id:141039) for the differences between fixation probabilities of adjacent states:
$$
T_k^+ (\rho_{k+1} - \rho_k) = T_k^- (\rho_k - \rho_{k-1})
$$
Let's examine the ratio $\gamma_k = T_k^- / T_k^+$:
$$
\gamma_k = \frac{ \frac{(N-k)k}{N(kr + N-k)} }{ \frac{kr(N-k)}{N(kr + N-k)} } = \frac{1}{r}
$$
Remarkably, this ratio is independent of the state $k$ and depends only on the [relative fitness](@entry_id:153028) $r$. The [recurrence relation](@entry_id:141039) becomes $\rho_{k+1} - \rho_k = (1/r) (\rho_k - \rho_{k-1})$. This shows that the differences $\rho_{k+1} - \rho_k$ form a [geometric progression](@entry_id:270470) with [common ratio](@entry_id:275383) $1/r$.

We can solve this system using the boundary conditions derived from the [absorbing states](@entry_id:161036): $\rho_0 = 0$ (extinction is certain with no mutants) and $\rho_N = 1$ (fixation is certain with only mutants) . The solution is given by the ratio of two geometric sums:
$$
\rho_k = \frac{\sum_{i=0}^{k-1} (1/r)^i}{\sum_{i=0}^{N-1} (1/r)^i}
$$
Evaluating this expression leads to two important cases:

1.  **Neutral Evolution ($r=1$):** When the mutant is selectively neutral, the ratio $\gamma_k = 1$. The sums become simple counts, yielding the intuitive result that the fixation probability is equal to the initial fraction of mutants:
    $$
    \rho_k = \frac{k}{N}
    $$

2.  **Selective Evolution ($r \neq 1$):** For advantageous or deleterious mutants, we use the formula for the sum of a finite [geometric series](@entry_id:158490), which gives the celebrated formula for fixation probability in the Moran process:
    $$
    \rho_k = \frac{1 - r^{-k}}{1 - r^{-N}}
    $$
This formula is a cornerstone of [population genetics](@entry_id:146344), quantifying the delicate balance between selection (captured by $r$) and [genetic drift](@entry_id:145594) (captured by the finite population size $N$) .

### The Diffusion Approximation

While the Moran model provides an exact solution, its discrete nature can be cumbersome, especially for large populations or more complex [fitness landscapes](@entry_id:162607). The **[diffusion approximation](@entry_id:147930)** provides a powerful alternative by modeling the change in mutant frequency as a continuous [stochastic process](@entry_id:159502). This is typically described by a **[stochastic differential equation](@entry_id:140379) (SDE)** or the equivalent **Fokker-Planck equation** (for the probability density) and **Kolmogorov equations** (for hitting probabilities and other properties).

The core idea is to approximate the discrete jumps in mutant frequency, $\Delta x = \pm 1/N$, by a continuous process in the limit of large population size, $N \to \infty$. To do this requires careful scaling of time and the [selection coefficient](@entry_id:155033).

A general SDE for the mutant frequency $x(t)$ is written as:
$$
dX_t = m(X_t) dt + \sqrt{v(X_t)} dW_t
$$
Here, $m(x)$ is the **drift coefficient**, representing the deterministic force of selection, and $v(x)$ is the **diffusion coefficient**, representing the stochastic noise from [random sampling](@entry_id:175193) in a finite population ([genetic drift](@entry_id:145594)). $dW_t$ is a standard Wiener process.

The specific forms of $m(x)$ and $v(x)$ depend on the underlying discrete model and the [time scaling](@entry_id:260603). For instance, if we analyze the Moran process by rescaling discrete time steps by $N^2$ and assuming a weak [selection coefficient](@entry_id:155033) $w_N = s/N$, a Taylor expansion of the master equation generator leads to a [diffusion process](@entry_id:268015) with drift $b(x) = s x(1-x)$ and a diffusion term $a(x) = 2x(1-x)$, where the SDE is conventionally written with diffusion term $\sqrt{a(x)}$ .

A more common framework, often associated with the **Wright-Fisher model**, measures time in generations and leads to a diffusion coefficient $v(x) = x(1-x)/N$. This framework is highly versatile. For instance, it can readily accommodate **[frequency-dependent selection](@entry_id:155870)**, where fitness is not constant but depends on the composition of the population. If the fitness difference between types is driven by an underlying payoff difference $a(x) = \pi_A(x) - \pi_B(x)$ under weak selection intensity $\beta$, the drift term becomes:
$$
m(x) = \beta x(1-x) a(x)
$$
The factor $x(1-x)$ naturally arises from the interaction between the two types; selection has no effect if either type is absent. In this framework, the stochastic dynamics of the mutant frequency are captured by the interplay of the drift $m(x)$ and diffusion $v(x) = x(1-x)/N$ .

Once the drift and diffusion coefficients are known, the fixation probability $u(x)$ starting from an initial frequency $x$ can be found by solving the stationary **backward Kolmogorov equation**, which is a second-order ordinary differential equation:
$$
m(x) \frac{du}{dx} + \frac{1}{2} v(x) \frac{d^2u}{dx^2} = 0
$$
This equation is solved with the [absorbing boundary conditions](@entry_id:164672) $u(0)=0$ and $u(1)=1$. This equation is a powerful and general tool for calculating fixation probabilities in a wide range of evolutionary scenarios.

### Advanced Topics and Extensions

Building on the foundation of the Moran process and the [diffusion approximation](@entry_id:147930), we can now explore more complex and realistic evolutionary scenarios.

#### Large Deviations and the WKB Approximation

The standard diffusion approximation is most accurate when selection is weak compared to drift (e.g., $Ns \sim \mathcal{O}(1)$). In the regime of strong selection relative to drift ($Ns \gg 1$), fixation or extinction can become a **rare event**. This happens, for example, when selection creates a [stable equilibrium](@entry_id:269479) at an intermediate frequency, meaning both fixation and extinction require the population to overcome a selective barrier via random fluctuations.

To analyze such rare events, we turn to [large deviation theory](@entry_id:153481), often employing the **Wentzel–Kramers–Brillouin (WKB)** method. This approach starts from the master equation and assumes the probability distribution takes the form $P(x) \sim \exp(-N S(x))$, where $S(x)$ is the **action** or potential function. In the large-$N$ limit, the master equation transforms into a **Hamilton-Jacobi equation** for the action, of the form $H(x, p) = 0$, where $p = dS/dx$ is a "[canonical momentum](@entry_id:155151)". For the Moran process with constant fitness $r=1+s$, this procedure yields the Hamiltonian :
$$
H(x, p) = \frac{x(1-x)}{1+xs} \left[ (1+s)e^p + e^{-p} - s - 2 \right]
$$
The WKB method provides a framework for calculating the "cost" of different evolutionary trajectories, with the most probable path for a rare event being the one that minimizes the action.

A practical application of this is analyzing the impact of an **Allee effect**, a form of [positive frequency-dependent selection](@entry_id:165001) where a mutant's fitness is suppressed at low frequencies. For example, consider a mutant with [relative fitness](@entry_id:153028) $w_A(x) = 1 + s(x - x_A)$, where $x_A \in (0,1)$ is a critical threshold. A mutant starting at a low frequency $x_0  x_A$ is deleterious. It can only fix if [genetic drift](@entry_id:145594) allows it to randomly cross the "fitness valley" and surpass the threshold $x_A$, after which selection becomes positive. In the large deviation regime ($Ns \gg 1$), this crossing is a rare event. The fixation probability is exponentially small and can be calculated using the backward equation, which in this limit is solved by WKB-like methods. The result shows an exponential suppression :
$$
\phi(x_0) \sim \exp(-Ns(x_A - x_0)^2)
$$
This demonstrates how a fitness barrier translates into an exponential suppression of the fixation probability.

The WKB and standard diffusion approximations are thus complementary tools. The WKB method is accurate in the large deviation regime ($Ns \gg 1$), where the dynamics are characterized by rare escapes from metastable states. The diffusion approximation, on the other hand, is most suitable for the weak selection regime ($Ns \lesssim \mathcal{O}(1)$), where drift and selection are of comparable magnitude .

#### Evolution on Graphs

Populations are rarely well-mixed. Spatial or social structure can be represented by a graph, where individuals can only interact with their neighbors. This structure fundamentally alters [evolutionary dynamics](@entry_id:1124712). Consider the Moran process on a graph $G$, where at each step, an individual is chosen for reproduction (proportional to fitness), and its offspring replaces a randomly chosen neighbor. This is known as the **Birth-Death (BD) update rule**.

Under [neutral evolution](@entry_id:172700) ($r=1$) on a graph, the fixation probability of a single mutant is no longer simply $1/N$. Instead, it depends on the starting position of the mutant. The fixation probability from a node $i$, $\rho_i(1)$, is equal to its **[reproductive value](@entry_id:191323)**, a measure of its expected long-term contribution to the population's [gene pool](@entry_id:267957). For the BD update rule on an undirected graph, the [reproductive value](@entry_id:191323) of a node $i$ is proportional to its degree $d_i$. The neutral fixation probability is thus :
$$
\rho_i(1) = \frac{d_i}{\sum_{j=1}^N d_j}
$$
Mutants starting in highly connected "hub" nodes have a greater chance of fixing.

When weak selection is introduced ($r = 1+\delta$ for small $\delta$), a remarkable result known as the **isothermal theorem** emerges. It states that for any **[regular graph](@entry_id:265877)** (where all nodes have the same degree) under the BD update rule, the fixation probability is identical to that of a well-mixed population of the same size, for any value of $r$. This means that for a single mutant, the first-order expansion in $\delta$ is :
$$
\rho(1+\delta) = \frac{1}{N} + \frac{N-1}{2N^2}\delta + O(\delta^2)
$$
This result connects the dynamics on a large class of structured populations back to the fundamental well-mixed model.

#### Stochastic Environments

Fitness is not always constant; it can fluctuate over time due to changing environmental conditions. Consider a scenario where the mutant fitness $r(t)$ is itself a stochastic process. A naive approach might be to use the average fitness $\bar{r} = \mathbb{E}[r(t)]$ in the standard formula. This is generally incorrect because the fixation probability is a nonlinear function of fitness, and the expectation of a nonlinear function is not the function of the expectation (a consequence of Jensen's inequality). A short period of highly deleterious fitness can lead to rapid extinction, an effect that is missed by averaging.

The rigorous approach is to model the evolution as a joint Markov process on the combined state space of the population configuration $S_t$ and the environmental state $r_t$. The generator of this joint process, $\mathcal{G}$, is the sum of the population generator $L_r$ and the environment generator $A$, i.e., $\mathcal{G} = L_r + A$. The fixation probability $u(S,r)$ is then the solution to the backward equation for this joint process:
$$
(\mathcal{G}u)(S,r) = (L_r u)(S,r) + (A u)(S,r) = 0
$$
with boundary conditions $u(\text{extinction}, r)=0$ and $u(\text{fixation}, r)=1$. The final expected fixation probability, or **annealed probability**, is obtained by averaging this solution $u(S,r)$ over the stationary distribution of the environmental states .

### Concluding Remarks on Asymptotic Limits

The interplay between selection strength ($r$), population size ($N$), and [population structure](@entry_id:148599) is a central theme in [evolutionary dynamics](@entry_id:1124712). The order in which mathematical limits are taken can reveal profound differences in evolutionary regimes. For the well-mixed Moran model, the limits are well-behaved. The fixation probability of a single mutant, $\rho_N(r,1)$, tends to zero whether we first let the population size become infinite ($N \to \infty$) and then consider neutral fitness ($r \to 1$), or vice versa. In both cases, the limit is zero :
$$
\lim_{N\to\infty} \lim_{r\to 1} \rho_{N}(r,1) = \lim_{N\to\infty} \frac{1}{N} = 0
$$
$$
\lim_{r\to 1} \lim_{N\to\infty} \rho_{N}(r,1) = \lim_{r\to 1} \left( 1 - \frac{1}{r} \right) = 0 \quad (\text{for } r1)
$$
The commutation of limits in this simple case reflects a robust result. However, for structured populations, the order of limits can matter. The limit of weak selection on a large graph can yield different outcomes from the limit of a large graph with fixed selection, highlighting the rich and complex behavior that emerges from the principles and mechanisms explored in this chapter.