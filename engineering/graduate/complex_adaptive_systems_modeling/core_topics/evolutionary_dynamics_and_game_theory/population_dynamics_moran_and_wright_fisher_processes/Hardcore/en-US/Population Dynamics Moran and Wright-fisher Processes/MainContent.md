## Introduction
The evolution of populations is a process governed by both deterministic forces and random chance. While natural selection provides a clear direction, the finite size of any real population introduces an element of [stochasticity](@entry_id:202258) known as [genetic drift](@entry_id:145594), where [allele frequencies](@entry_id:165920) can fluctuate and be lost or fixed by pure chance. Understanding the interplay between these forces is a central challenge in evolutionary biology. This article delves into the mathematical heart of this problem by exploring two foundational models: the Wright-Fisher process and the Moran process. These elegant frameworks provide the basis for quantifying the effects of drift and selection.

This article is structured to build your understanding from the ground up. In the "Principles and Mechanisms" chapter, we will rigorously derive the mathematical formulations of both models, explore their key properties like [fixation probability](@entry_id:178551), and introduce the powerful diffusion approximation. Next, in "Applications and Interdisciplinary Connections," we will see how these core models are extended and adapted to provide critical insights into diverse fields, from [cancer biology](@entry_id:148449) and [microbial evolution](@entry_id:166638) to [community ecology](@entry_id:156689). Finally, the "Hands-On Practices" section offers a chance to apply these theoretical concepts to solve canonical problems in [population genetics](@entry_id:146344), solidifying your grasp of the material.

## Principles and Mechanisms

In this chapter, we transition from a general introduction to a rigorous examination of the core principles and mathematical mechanisms that govern [stochastic population dynamics](@entry_id:187351). We will focus on two foundational models—the Wright-Fisher process and the Moran process—which, despite their simplicity, provide profound insights into the effects of random [genetic drift](@entry_id:145594) and natural selection in finite populations. Our approach will be to build these models from first principles, derive their key properties, and explore their behavior under various conditions, culminating in the powerful diffusion approximation that bridges the gap between discrete, finite systems and continuous, large-scale dynamics.

### Stochastic Processes in Population Genetics: A Markov Chain Framework

The evolution of [allele frequencies](@entry_id:165920) in a finite population is an intrinsically [stochastic process](@entry_id:159502). Even in the absence of [selective pressures](@entry_id:175478), the [random sampling](@entry_id:175193) of individuals who contribute to the next generation causes [allele frequencies](@entry_id:165920) to fluctuate. This phenomenon, known as **[genetic drift](@entry_id:145594)**, can lead to the random loss or fixation of alleles over time.

To model this process mathematically, we can represent the population state by the number of individuals carrying a specific [allele](@entry_id:906209). Consider a [haploid](@entry_id:261075) population of constant size $N$ with two alleles, $A$ and $a$. The state of the system at any [discrete time](@entry_id:637509) point $t$ can be fully described by the integer $X_t$, representing the count of [allele](@entry_id:906209) $A$, where $X_t \in \{0, 1, \dots, N\}$. The states $X_t = 0$ and $X_t = N$ are of special importance; they are **[absorbing states](@entry_id:161036)**, representing the complete loss (extinction) or complete takeover (fixation) of [allele](@entry_id:906209) $A$, respectively. Once the system enters one of these states, it cannot leave.

A key assumption in many [population genetics models](@entry_id:192722) is that the process is memoryless: the probability distribution of future states depends only on the current state, not on the path taken to reach it. This is the **Markov property**. Furthermore, if the rules governing the transition from one state to the next do not change over time, the process is said to be **time-homogeneous**. Under these assumptions, the evolution of the allele count can be modeled as a time-homogeneous Markov chain. The entire dynamics of the system are encapsulated in a matrix of **one-step [transition probabilities](@entry_id:158294)**, $P_{ij}$, defined as:

$P_{ij} = \Pr(X_{t+1} = j \mid X_t = i)$

The Markov property is then formally expressed as:

$\Pr(X_{t+1} = j \mid X_t = i, X_{t-1}, \dots, X_0) = P_{ij}$

Different models of population dynamics, such as the Wright-Fisher and Moran processes, are distinguished by their specific definitions of these [transition probabilities](@entry_id:158294), which arise from different assumptions about the population's life cycle and reproductive mechanics .

### The Wright-Fisher Model: A Generational Approach

The Wright-Fisher model is a cornerstone of [population genetics](@entry_id:146344), characterized by discrete, non-overlapping generations. The core assumption is that the $N$ individuals of a new generation are produced by [sampling with replacement](@entry_id:274194) from the individuals of the parent generation.

#### The Neutral Wright-Fisher Process

In the simplest, or **neutral**, version of the model, every individual in the parent generation has an equal chance of being a progenitor. If the parent generation has $i$ individuals of type $A$, the frequency of allele $A$ is $x = i/N$. When forming the next generation, each of the $N$ "draws" is an independent Bernoulli trial with a success probability (drawing an $A$ allele) of $p = i/N$.

Therefore, the number of $A$ alleles in the next generation, $X_{t+1}$, given that $X_t=i$, follows a [binomial distribution](@entry_id:141181) with parameters $N$ and $p=i/N$. The [transition probability](@entry_id:271680) from state $i$ to state $j$ is given by the binomial probability [mass function](@entry_id:158970) :

$P_{ij} = \binom{N}{j} \left(\frac{i}{N}\right)^j \left(1 - \frac{i}{N}\right)^{N-j}$

This equation fully defines the dynamics of the neutral Wright-Fisher process. Note that if $i=0$, the probability of drawing an $A$ [allele](@entry_id:906209) is 0, so $P_{00} = 1$. Similarly, if $i=N$, the probability is 1, so $P_{NN} = 1$, confirming that 0 and $N$ are [absorbing states](@entry_id:161036).

#### Wright-Fisher Process with Selection

Natural selection can be incorporated into the Wright-Fisher framework by assuming that individuals have different **fitnesses**, which affect their contribution to the next generation's [gene pool](@entry_id:267957). Consider the case of genic selection, where [allele](@entry_id:906209) $A$ confers a [relative fitness](@entry_id:153028) of $w_A = 1+s$ and [allele](@entry_id:906209) $a$ has a [relative fitness](@entry_id:153028) of $w_a = 1$. Here, $s$ is the **[selection coefficient](@entry_id:155033)**.

If the frequency of [allele](@entry_id:906209) $A$ in the parent generation is $x_t=i/N$, selection acts before [random sampling](@entry_id:175193). The frequency of [allele](@entry_id:906209) $A$ in the conceptual "gamete pool" from which the next generation is drawn is no longer $x_t$, but a post-selection frequency, $p_t$. This frequency is calculated by weighting each [allele](@entry_id:906209) by its fitness and normalizing by the mean fitness of the population, $\bar{w}_t$:

$\bar{w}_t = x_t w_A + (1-x_t)w_a = x_t(1+s) + (1-x_t) = 1+sx_t$

$p_t = \frac{x_t w_A}{\bar{w}_t} = \frac{x_t(1+s)}{1+sx_t}$

Once this post-selection frequency is determined, the formation of the next generation proceeds as before: by $N$ independent draws from this pool. The [transition probability](@entry_id:271680), conditioned on $X_t=i$, is therefore given by the binomial probability with success parameter $p_i = \frac{i(1+s)}{N+si}$ :

$\Pr(X_{t+1} = j \mid X_t = i) = \binom{N}{j} \left(\frac{i(1+s)}{N+si}\right)^j \left(\frac{N-i}{N+si}\right)^{N-j}$

This formulation elegantly combines the deterministic pressure of selection with the stochastic nature of [genetic drift](@entry_id:145594).

### The Moran Process: A Birth-Death Approach

The Moran process offers an alternative modeling framework based on overlapping generations. In each discrete time step, only one individual reproduces and one individual dies. This creates a continuous birth-death chain, where the population size remains constant.

#### The Neutral Moran Process

In the neutral Moran process, one individual is chosen uniformly at random to reproduce, and, independently, one individual is chosen uniformly at random to die. The offspring of the first individual replaces the second. Let's analyze the transitions when the population has $i$ individuals of type $A$ and $N-i$ of type $a$.

The number of $A$ individuals increases by one ($i \to i+1$) only if an $A$ individual reproduces (probability $i/N$) and an $a$ individual dies (probability $(N-i)/N$). The [transition probability](@entry_id:271680) is:

$P_{i,i+1} = \left(\frac{i}{N}\right) \left(\frac{N-i}{N}\right) = \frac{i(N-i)}{N^2}$

Conversely, the number of $A$ individuals decreases by one ($i \to i-1$) if an $a$ individual reproduces (probability $(N-i)/N$) and an $A$ individual dies (probability $i/N$):

$P_{i,i-1} = \left(\frac{N-i}{N}\right) \left(\frac{i}{N}\right) = \frac{i(N-i)}{N^2}$

A striking feature of the neutral Moran process is that the probabilities of moving up or down are identical: $P_{i,i+1} = P_{i,i-1}$. If the chosen reproducer and the chosen casualty are of the same type, the state does not change. The probability of remaining at state $i$ is $P_{i,i} = 1 - P_{i,i+1} - P_{i,i-1} = 1 - \frac{2i(N-i)}{N^2}$ .

#### The Moran Process with Selection

Selection is typically introduced into the Moran process by making the reproduction step fitness-dependent. In the standard **birth-death (BD) Moran process**, an individual is chosen to reproduce with probability proportional to its fitness. Assume type $A$ has fitness $f_A$ and type $a$ has fitness $f_a$. The total fitness in the population is $F_{total} = i f_A + (N-i)f_a$.

The probability of an $A$ individual reproducing is $\frac{i f_A}{F_{total}}$, and the probability of an $a$ individual dying remains $\frac{N-i}{N}$. The [transition probability](@entry_id:271680) for an increase in $A$ is :

$P_{i \to i+1} = \left(\frac{i f_A}{i f_A + (N-i)f_a}\right) \left(\frac{N-i}{N}\right) = \frac{i(N-i)f_A}{N(i f_A + (N-i)f_a)}$

Similarly, the probability of a decrease is:

$P_{i \to i-1} = \left(\frac{(N-i) f_a}{i f_A + (N-i)f_a}\right) \left(\frac{i}{N}\right) = \frac{i(N-i)f_a}{N(i f_A + (N-i)f_a)}$

These probabilities define the dynamics of the Moran process with selection acting on birth.

#### Microscopic Rules Matter: Birth-Death versus Death-Birth

The precise implementation of the update step can have subtle but important consequences. Consider an alternative, the **death-birth (DB) Moran process**, where selection acts on survival. First, an individual is chosen to die with probability inversely proportional to its fitness. Then, a parent is chosen uniformly from the remaining $N-1$ individuals to fill the vacancy.

This seemingly small change in the microscopic rules alters the individual [transition probabilities](@entry_id:158294). However, a deeper analysis reveals a surprising invariance. The [fixation probability](@entry_id:178551) of an allele depends critically on the ratio of the downward to upward [transition probabilities](@entry_id:158294), $\gamma_i = P_{i \to i-1} / P_{i \to i+1}$. Let's calculate this ratio for both models, using a [relative fitness](@entry_id:153028) $r = f_A / f_a$.

For the [birth-death model](@entry_id:169244) :
$\gamma_i^{\text{BD}} = \frac{P_{i \to i-1}}{P_{i \to i+1}} = \frac{i(N-i)f_a / (N F_{total})}{i(N-i)f_A / (N F_{total})} = \frac{f_a}{f_A} = \frac{1}{r}$

For the death-birth model, after deriving its [transition probabilities](@entry_id:158294), the same calculation yields :
$\gamma_i^{\text{DB}} = \frac{1}{r}$

The fact that this crucial ratio is identical and, remarkably, independent of the state $i$, means that both the BD and DB models predict the exact same fixation probabilities. However, the sum of [transition probabilities](@entry_id:158294), $P_{i \to i+1} + P_{i \to i-1}$, which governs the speed of the process, is generally different for the two models. This illustrates a key principle in modeling complex systems: different microscopic update rules can lead to identical outcomes for some [macroscopic observables](@entry_id:751601) (like [fixation probability](@entry_id:178551)) but different outcomes for others (like fixation time).

### Fixation Probability: The Ultimate Fate of an Allele

One of the most important questions in [population genetics](@entry_id:146344) is: what is the probability that a new mutant allele will eventually spread through the entire population and reach fixation? This quantity, the **[fixation probability](@entry_id:178551)**, depends on the initial frequency of the allele, the population size, and the strength of selection.

#### The Neutral Case: A Gambler's Ruin Analogy

Let us first consider a neutral [allele](@entry_id:906209). The dynamics of the neutral Moran process provide a beautiful analogy to the classic **Gambler's Ruin problem**. The state $i$ can be thought of as a gambler's fortune, with the game ending when the fortune reaches 0 or the house's total capital, $N$.

As we saw, in the Moran process, the state $i$ can increase, decrease, or stay the same. However, if we only consider the time steps where a change occurs, we create an **embedded Markov chain**. In this embedded chain, the probability of moving from $i$ to $i+1$ is $\frac{P_{i,i+1}}{P_{i,i+1}+P_{i,i-1}} = \frac{1}{2}$, and the probability of moving to $i-1$ is likewise $\frac{1}{2}$. This is an unbiased random walk.

Let $\pi_i$ be the fixation probability starting from state $i$. For this unbiased walk, $\pi_i$ must satisfy the [recurrence relation](@entry_id:141039):

$\pi_i = \frac{1}{2} \pi_{i+1} + \frac{1}{2} \pi_{i-1}$

This relation implies that the sequence of fixation probabilities forms an [arithmetic progression](@entry_id:267273). With the [absorbing boundary conditions](@entry_id:164672) $\pi_0 = 0$ (fixation is impossible if the allele is already lost) and $\pi_N = 1$ (fixation is certain if the allele is already fixed), the unique solution to this recurrence is remarkably simple :

$\pi_i = \frac{i}{N}$

This fundamental result states that for a neutral allele, its probability of fixation is simply its initial frequency. A single new mutant ($i=1$) has a $1/N$ chance of taking over the entire population. This result, while derived here for the Moran process, also holds for the Wright-Fisher model.

#### The Influence of Selection

When selection is present, the random walk becomes biased. The direction of the bias is determined by the ratio $\gamma_i = 1/r$. Let $\rho_i$ be the fixation probability starting with $i$ mutants of [relative fitness](@entry_id:153028) $r$. The [recurrence relation](@entry_id:141039) for $\rho_i$ becomes:

$\rho_{i+1} - \rho_i = \gamma_i (\rho_i - \rho_{i-1}) = \frac{1}{r}(\rho_i - \rho_{i-1})$

This shows that the differences $\rho_{i+1} - \rho_i$ form a [geometric progression](@entry_id:270470). Summing these differences from the boundary condition $\rho_0 = 0$ up to state $i$, and solving for the unknown constant using the second boundary condition $\rho_N=1$, yields the celebrated formula for the [fixation probability](@entry_id:178551) under selection  :

$\rho_i = \frac{1 - (1/r)^i}{1 - (1/r)^N} = \frac{1 - r^{-i}}{1 - r^{-N}}$

This powerful equation quantifies the interplay between selection and drift. If the [allele](@entry_id:906209) is advantageous ($r>1$), its [fixation probability](@entry_id:178551) is higher than its initial frequency $i/N$. If it is disadvantageous ($r1$), its [fixation probability](@entry_id:178551) is lower. One can verify using L'Hôpital's rule that as $r \to 1$, this formula correctly limits to the neutral result $\rho_i = i/N$ .

### The Diffusion Approximation: A Continuous Perspective

While exact for any population size, the discrete Markov chain models can be cumbersome. For large populations, it is often advantageous to approximate the discrete [allele](@entry_id:906209) count with a continuous frequency variable $x \in [0,1]$ and model its evolution using a stochastic differential equation (SDE). This is known as the **diffusion approximation**.

The probability of fixation $u(x)$ starting from an initial frequency $x$ can be found by solving the **Kolmogorov backward equation**, a second-order [ordinary differential equation](@entry_id:168621) whose coefficients are determined by the drift and diffusion properties of the process. For a process with drift $m(x)$ and variance $v(x)$, the equation for the [fixation probability](@entry_id:178551) $u(x)$ is:

$0 = m(x)u'(x) + \frac{1}{2}v(x)u''(x)$

with boundary conditions $u(0)=0$ and $u(1)=1$.

#### Neutral Fixation Revisited

For a neutral process, the drift term $m(x)$ is zero, as there is no systematic pressure on the [allele frequency](@entry_id:146872). The backward equation simplifies dramatically to $\frac{1}{2}v(x)u''(x)=0$. Since the variance term $v(x)$ (which for Wright-Fisher models is proportional to $x(1-x)$) is non-zero inside the interval $(0,1)$, this requires that $u''(x)=0$ . The general solution is a linear function, $u(x) = c_1 x + c_2$. Applying the boundary conditions $u(0)=0$ and $u(1)=1$ immediately gives $c_2=0$ and $c_1=1$. Thus, the diffusion approximation recovers the exact result from the discrete models with elegant simplicity :

$u(x) = x$

#### Fixation with Weak Selection

The [diffusion approximation](@entry_id:147930) is particularly powerful for analyzing weak selection, where the [selection coefficient](@entry_id:155033) $s$ is small (on the order of $1/N$). For the Wright-Fisher model with genic selection, the drift and variance coefficients are $m(x) = sx(1-x)$ and $v(x) = x(1-x)/N$. Substituting these into the backward equation gives :

$0 = sx(1-x) u'(x) + \frac{x(1-x)}{2N} u''(x)$

For $x \in (0,1)$, we can divide by $x(1-x)$ to get the simpler ODE: $u''(x) + 2Ns u'(x) = 0$. This is a linear ODE that can be solved by [reduction of order](@entry_id:140559). The general solution is $u(x) = A \exp(-2Nsx) + B$. Applying the boundary conditions $u(0)=0$ and $u(1)=1$ allows us to solve for the constants $A$ and $B$, yielding Kimura's celebrated formula for the fixation probability under weak selection:

$u(x) = \frac{1 - \exp(-2Nsx)}{1 - \exp(-2Ns)}$

This result is one of the pillars of modern [population genetics](@entry_id:146344), quantifying how selection efficacy (encapsulated in the term $2Ns$) modulates the probability of a new [allele](@entry_id:906209)'s success.

### The Concept of Effective Population Size ($N_e$)

The Wright-Fisher and Moran models rely on idealized assumptions, such as equal [reproductive success](@entry_id:166712) for all individuals in the neutral case. Real populations violate these assumptions in many ways: some individuals have more offspring than others, population sizes fluctuate, etc. The concept of **[effective population size](@entry_id:146802)**, denoted $N_e$, was developed to bridge this gap. $N_e$ is the size of an idealized Wright-Fisher population that would experience the same magnitude of [genetic drift](@entry_id:145594) as the actual census population.

One common way to define $N_e$ is through the variance in [allele frequency](@entry_id:146872) change per generation. The **variance [effective population size](@entry_id:146802)** is defined such that the variance in [allele frequency](@entry_id:146872) matches that of an idealized [diploid](@entry_id:268054) Wright-Fisher population :

$\mathrm{Var}(\Delta p \mid p) = \frac{p(1-p)}{2N_e}$

If a real population of [census size](@entry_id:173208) $N$ has a higher variance in [reproductive success](@entry_id:166712) than the Poisson distribution assumed by the ideal model, its effective size $N_e$ will be smaller than $N$. For a [diploid](@entry_id:268054) population with constant [census size](@entry_id:173208) $N$ and variance in offspring number $V_k$, the effective size is given by the classic formula:

$N_e = \frac{4N-2}{V_k+2}$

When population size itself fluctuates over time, the long-term effective size is not the arithmetic average. Because [genetic drift](@entry_id:145594) is stronger in smaller populations, periods of small size have a disproportionate impact on the overall loss of [genetic variation](@entry_id:141964). The appropriate long-term average is the **harmonic mean** of the per-generation effective sizes. If the effective size over $T$ generations is $N_{e,t}$ for generation $t$, the overall effective size $N_e$ is given by:

$\frac{1}{N_e} = \frac{1}{T} \sum_{t=1}^{T} \frac{1}{N_{e,t}}$

Substituting our expression for $N_{e,t}$ when the variance in offspring number $V_{k,t}$ also changes over time, we find that the long-term [effective population size](@entry_id:146802) is :

$N_e = \frac{T(4N-2)}{2T + \sum_{t=1}^{T} V_{k,t}}$

The concept of [effective population size](@entry_id:146802) is crucial, allowing the powerful theoretical results derived from idealized models to be applied to the complexities of natural populations.