## Introduction
How has the vast diversity of life on Earth been generated and maintained over geological time? Answering this fundamental question requires a quantitative understanding of the two processes that govern the number of species in a [clade](@entry_id:171685): speciation, which gives rise to new lineages, and extinction, which removes them. Diversification rate analysis provides the statistical and theoretical framework for inferring these deep-time processes from contemporary and fossil data. By modeling the branching patterns of the Tree of Life, we can test hypotheses about the [tempo and mode of evolution](@entry_id:202710), uncovering the drivers of major evolutionary radiations and the causes of biotic crises.

This article provides a graduate-level introduction to the core principles, applications, and practical implementation of [diversification rate](@entry_id:186659) analysis. It bridges the gap between the theoretical underpinnings of macroevolutionary models and their real-world application in biological research. The content is structured to guide you from foundational concepts to the research frontier.

The first chapter, **Principles and Mechanisms**, lays the mathematical groundwork. We will begin with the simple constant-rate [birth-death process](@entry_id:168595) and progressively build complexity, exploring models that account for time-varying rates, trait-dependence (SSE models), and the integration of fossil data (the FBD process). The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these models are used as a powerful toolkit to address major questions in evolutionary biology, paleontology, and [macroecology](@entry_id:151485)—from testing the role of key innovations to detecting mass extinctions. Finally, the **Hands-On Practices** section offers a set of challenges designed to translate theoretical knowledge into practical skills, from deriving key estimators to simulating the diversification process itself.

## Principles and Mechanisms

The analysis of diversification rates seeks to understand the macroevolutionary processes of speciation and extinction that have generated the diversity of life. The primary tools for this endeavor are mathematical models that describe how lineages proliferate and disappear over geological time. This chapter details the principles and mechanisms of the most foundational and widely used of these models, building from the simple constant-rate [birth-death process](@entry_id:168595) to more complex frameworks that accommodate time-variation, trait-dependence, and fossil evidence.

### The Constant-Rate Birth-Death Process: Foundational Parameters

The cornerstone of [diversification rate](@entry_id:186659) analysis is the **constant-rate birth–death process**, a stochastic model that treats the evolution of a clade as a population of lineages. In its simplest form, it assumes that at any point in time, every extant lineage is independent and has the same constant probabilities of either splitting into two (a speciation or "birth" event) or disappearing (an extinction or "death" event).

This process is formally a continuous-time Markov chain where the state of the system is the number of lineages, $N(t)$. The dynamics are governed by two fundamental parameters [@problem_id:2567020]:

*   The **[speciation rate](@entry_id:169485)**, denoted by $\lambda$, is the instantaneous per-lineage rate of speciation.
*   The **extinction rate**, denoted by $\mu$, is the instantaneous per-lineage rate of extinction.

As instantaneous rates, or hazards, both $\lambda$ and $\mu$ have units of events per lineage per unit time, typically expressed as $\text{Myr}^{-1}$ (per million years). The interpretation is that for any single lineage over a very small interval of time $\Delta t$, the probability of it speciating is approximately $\lambda \Delta t$, and the probability of it going extinct is approximately $\mu \Delta t$. It is crucial to recognize that these are *per-lineage* rates. The total rate of speciation for a clade of size $N$ is $\lambda N$, which increases as the [clade](@entry_id:171685) grows, even though the underlying per-lineage parameter $\lambda$ is constant.

From these two basic parameters, we derive two important composite parameters that describe the overall dynamics of the clade [@problem_id:2567020]:

*   The **[net diversification rate](@entry_id:162682)**, $r = \lambda - \mu$. This parameter represents the expected proportional growth rate of the number of lineages. The expected number of lineages in the [clade](@entry_id:171685), $\mathbb{E}[N(t)]$, grows (or shrinks) exponentially according to the equation $\mathbb{E}[N(t)] = N_0 \exp(rt)$, where $N_0$ is the initial number of lineages. Like $\lambda$ and $\mu$, $r$ has units of $\text{time}^{-1}$.

*   The **turnover rate**, $\epsilon = \mu / \lambda$. This is a dimensionless quantity that measures the relative importance of extinction compared to speciation. A turnover of $\epsilon = 0$ signifies a process with no extinction, while $\epsilon = 1$ indicates that speciation and extinction rates are equal, leading to a [net diversification rate](@entry_id:162682) of $r=0$ and an expected clade size that remains constant over time.

### The Pure-Birth (Yule) Process: A Foundational Case Study

A particularly simple and historically important special case of the [birth-death process](@entry_id:168595) is the **pure-birth** or **Yule process**, which assumes the [extinction rate](@entry_id:171133) is zero ($\mu=0$) [@problem_id:2567066]. In this model, lineages only accumulate, providing a baseline expectation for diversification in the absence of extinction.

For a Yule process starting with a single lineage at time $t=0$, the number of lineages $N_t$ at a future time $t$ follows a [geometric distribution](@entry_id:154371). The probability of having exactly $n$ lineages is given by:
$$p_n(t) = \Pr(N_t = n) = \exp(-\lambda t) (1-\exp(-\lambda t))^{n-1} \quad \text{for } n \ge 1$$
The expected number of lineages grows as $\mathbb{E}[N_t] = \exp(\lambda t)$, and the variance is $\operatorname{Var}(N_t) = \exp(2\lambda t) - \exp(\lambda t)$.

The simplicity of the Yule model allows for straightforward estimation of the [speciation rate](@entry_id:169485). If we observe a clade with $n$ species that arose from a single common ancestor $T$ million years ago, the maximum likelihood estimate (MLE) for the [speciation rate](@entry_id:169485) is remarkably simple [@problem_id:2567066]:
$$\widehat{\lambda} = \frac{\ln(n)}{T}$$
For instance, if a zoological clade is observed to have $n = 57$ extant species and is known to have originated from a single ancestor $T = 12$ million years ago, the estimated [speciation rate](@entry_id:169485) would be $\widehat{\lambda} = \ln(57) / 12 \approx 0.3369 \text{ Myr}^{-1}$. It is important to note that this specific formula applies when diversification starts from a single lineage (a stem age). If one starts from a crown group diversification (i.e., at the first split, with two initial lineages), the formula becomes $\widehat{\lambda} = \ln(n/2) / T$.

### Likelihood and Inference from Phylogenetic Trees

While simple counts of species and age provide some insight, modern diversification analysis leverages the full information contained in a time-calibrated [phylogeny](@entry_id:137790)—the [tree topology](@entry_id:165290) and its branch lengths. The likelihood of a set of diversification parameters is the probability of observing the given phylogenetic tree under the model.

#### The Challenge of Identifiability from Extant-Only Trees

A fundamental challenge arises when we only have data for extant species. The phylogenies we reconstruct from modern DNA, known as **reconstructed trees**, are blind to lineages that went extinct without leaving any surviving descendants. This "pruning" effect of extinction complicates [parameter estimation](@entry_id:139349).

A key consequence is that different combinations of $\lambda$ and $\mu$ can produce statistically similar reconstructed trees. Specifically, for a constant-rate process, the distribution of branching times in an extant-only tree depends much more strongly on the difference $r = \lambda - \mu$ than on the individual values of $\lambda$ and $\mu$. An infinite set of parameter pairs—for instance, $(\lambda=0.2, \mu=0.1)$ and $(\lambda=0.3, \mu=0.2)$—share the same [net diversification rate](@entry_id:162682) ($r=0.1$) and can be difficult or impossible to distinguish based on the branching times of living species alone. Consequently, the [net diversification rate](@entry_id:162682) $r$ is generally considered more **identifiable** from neontological data than its constituent speciation and extinction rates [@problem_id:2567016]. Without additional information, such as from the [fossil record](@entry_id:136693), estimates of $\lambda$ and $\mu$ individually should be treated with considerable caution.

#### Lineage-Through-Time (LTT) Plots

A primary method for visualizing diversification patterns in a [phylogeny](@entry_id:137790) is the **Lineage-Through-Time (LTT) plot**. This graph shows the number of reconstructed lineages that exist at each point in time, from the root of the tree to the present. By comparing an empirical LTT plot from a real [phylogeny](@entry_id:137790) to the expected LTT plot under a given model, we can assess the model's fit.

For a Yule process, we can derive the expected number of lineages through time, conditioned on observing a [clade](@entry_id:171685) of age $T$ with $n$ species that originated from a crown node (two initial lineages). Measuring time $s$ backward from the present (so $s=0$ is the present and $s=T$ is the crown age), the expected number of lineages $L(s)$ at time $s$ is [@problem_id:2567070]:
$$ \mathbb{E}[L(s) \mid \text{age}=T, \text{richness}=n] = 2 + (n-2)\frac{\exp(\lambda(T-s)) - 1}{\exp(\lambda T) - 1} $$
This expression provides a theoretical curve against which an observed LTT plot can be compared to evaluate whether a constant-rate pure-birth process is a plausible explanation for the observed pattern of branching events.

### Extending the Models: Incorporating More Complexity and Data

The constant-rate [birth-death model](@entry_id:169244) is a powerful [null hypothesis](@entry_id:265441), but real-world diversification is often more complex. Rates may change over time, depend on organismal traits, or be better informed by integrating different data types.

#### Time-Varying Diversification

A straightforward extension of the basic model allows speciation and extinction rates to be functions of time, $\lambda(t)$ and $\mu(t)$. A common approach is to model these functions as piecewise-constant, with different rate regimes in different time intervals.

If we possess a complete record of a [clade](@entry_id:171685)'s history—including every speciation and extinction event and the precise duration of every lineage—the likelihood of the parameters can be calculated directly. In a given time interval $j$ with constant rates $\lambda_j$ and $\mu_j$, the number of speciation events ($B_j$) and extinction events ($D_j$) can be modeled as outcomes of two independent Poisson processes. The expected number of events is the rate multiplied by the total time lived by all lineages in that interval, a quantity known as the **lineage-time exposure**, $E_j = \int_{t_{j-1}}^{t_j} L(t) dt$. The [joint likelihood](@entry_id:750952) for the interval is the product of two Poisson probabilities [@problem_id:2567031]:
$$ L_j(\lambda_j, \mu_j \mid B_j, D_j, E_j) = \frac{(\lambda_j E_j)^{B_j}}{B_j!} \exp(-\lambda_j E_j) \cdot \frac{(\mu_j E_j)^{D_j}}{D_j!} \exp(-\mu_j E_j) $$
The total [log-likelihood](@entry_id:273783) is the sum of the log-likelihoods from all intervals. For example, given an interval with $E_1 = 12.4$ Myr of lineage exposure, $B_1 = 7$ speciations, and $D_1 = 3$ extinctions, the [log-likelihood](@entry_id:273783) contribution for proposed rates $\lambda_1 = 0.60$ and $\mu_1 = 0.20$ can be computed from this formula. Summing across all time intervals (e.g., across the three intervals specified in [@problem_id:2567031]) provides the total [log-likelihood](@entry_id:273783) of the diversification scenario, which in that case is $\ell \approx -10.79$.

#### Integrating Fossil Data: The Fossilized Birth-Death Process

The fossil record provides direct, albeit imperfect, evidence of past life and extinction events. The **fossilized birth–death (FBD) process** formally integrates this evidence into a unified likelihood framework. It extends the [birth-death model](@entry_id:169244) by adding a third parameter, $\psi$, the instantaneous rate of fossil discovery and preservation per lineage [@problem_id:2566995].

Under the FBD model, any given lineage is subject to three independent event types: speciation ($\lambda$), extinction ($\mu$), and fossil sampling ($\psi$). The total rate of *any* event occurring on a lineage is the sum of these rates, $\lambda + \mu + \psi$. The likelihood of observing a particular reconstructed tree containing both extant species and fossil occurrences is constructed from the contributions of all observed events and non-events:
*   Each of the $n_b$ speciation events (internal nodes) contributes a factor of $\lambda$.
*   Each of the $n_f$ fossil occurrences contributes a factor of $\psi$.
*   The total duration of all branches in the tree, $L_{\text{total}}$, represents time during which no speciation, extinction, or fossilization occurred on those specific lineages. This contributes a survival probability term of $\exp[-(\lambda+\mu+\psi)L_{\text{total}}]$.

Combining these components, the core of the FBD likelihood is proportional to:
$$ \mathcal{L}(\text{tree, fossils} \mid \lambda, \mu, \psi) \propto \lambda^{n_b} \psi^{n_f} \exp[-(\lambda+\mu+\psi)L_{\text{total}}] $$
This formulation elegantly demonstrates how different types of data inform different parameters: branching events in the tree primarily inform $\lambda$, fossil occurrences inform $\psi$, and the lengths of all branches collectively inform the total event rate $\lambda+\mu+\psi$.

#### Identifiability Revisited: Pulled Diversification Rates

The identifiability problem becomes even more acute for time-varying models based solely on extant phylogenies. It has been shown that an infinite number of different time-varying scenarios $(\lambda(t), \mu(t))$ can generate the exact same likelihood for a given reconstructed tree, making it impossible to disentangle the true speciation and extinction histories. These sets of statistically indistinguishable scenarios are known as [congruence classes](@entry_id:635978).

However, certain combinations of parameters *are* identifiable. These are the **pulled [speciation rate](@entry_id:169485)**, $\lambda_p(t)$, and the **pulled [diversification rate](@entry_id:186659)**, $r_p(t)$ [@problem_id:2567057]. If we measure time $t$ backward from the present ($t=0$) and let $E(t)$ be the probability that a lineage alive at time $t$ leaves no sampled descendants at the present, these identifiable quantities are defined as:
$$ \lambda_p(t) = \lambda(t)[1 - E(t)] $$
$$ r_p(t) = \lambda(t) - \mu(t) + \frac{1}{\lambda(t)}\frac{d\lambda(t)}{dt} = \lambda(t) - \mu(t) + \frac{d}{dt}[\ln \lambda(t)] $$
The likelihood of any reconstructed tree depends only on the function $\lambda_p(t)$ over time. Because $r_p(t)$ can be expressed entirely in terms of $\lambda_p(t)$ and its derivative, it too is identifiable. This profound result reveals the fundamental limits of what can be inferred from extant phylogenies alone: we can estimate the "pulled" rates of diversification, but not the true underlying speciation and extinction rates, without making strong simplifying assumptions or incorporating external data like fossils.

### Trait-Dependent Diversification

A central goal in [comparative biology](@entry_id:166209) is to understand whether organismal traits influence diversification. State-dependent speciation and extinction (SSE) models are designed to test such hypotheses.

#### The BiSSE Model

The first and most influential of these models is the **Binary State Speciation and Extinction (BiSSE) model**, designed for a binary character (e.g., presence/absence of a feature, coded as states 0 and 1) [@problem_id:2567052]. BiSSE models the joint evolution of the trait and the [phylogeny](@entry_id:137790). It is defined by a set of six parameters:
*   State-dependent speciation rates: $\lambda_0$ and $\lambda_1$.
*   State-dependent extinction rates: $\mu_0$ and $\mu_1$.
*   Anagenetic trait [transition rates](@entry_id:161581): $q_{01}$ (for $0 \to 1$) and $q_{10}$ (for $1 \to 0$).

Inference with BiSSE requires a rooted, time-calibrated phylogeny and the [character states](@entry_id:151081) of the species at the tips. The model's likelihood is computed by integrating over all possible character state histories at the internal nodes of the tree. To avoid bias, it is also crucial to account for incomplete sampling, often by incorporating known state-specific sampling fractions, $\rho_0$ and $\rho_1$.

#### The Problem of False Positives and HiSSE

While powerful, BiSSE models were found to have a high rate of false positives. They could incorrectly infer a link between a trait and diversification if some other, unmeasured factor was the true cause of [rate heterogeneity](@entry_id:149577) and this factor happened to be correlated with the observed trait.

The **Hidden-State Speciation and Extinction (HiSSE) model** was developed to address this critical issue [@problem_id:2567036]. HiSSE extends BiSSE by augmenting each observed state $i$ with a "hidden" state $h$ (e.g., A, B). A lineage is now in a compound state $(i, h)$, such as (state 0, [hidden state](@entry_id:634361) A) or (state 1, [hidden state](@entry_id:634361) B), each with its own [diversification rate](@entry_id:186659), e.g., $\lambda_{0,A}$, $\mu_{1,B}$.

The key innovation of HiSSE is that it allows for the construction of more plausible null models. Instead of comparing the full BiSSE model to a simple model with no rate variation at all, HiSSE allows for a **character-independent (CID)** [null model](@entry_id:181842). In a CID model, diversification rates can vary, but their variation is tied only to the hidden state, not the observed trait [@problem_id:2567036]. Formally, this [null model](@entry_id:181842) imposes the constraints $\lambda_{0,h} = \lambda_{1,h}$ and $\mu_{0,h} = \mu_{1,h}$ for all hidden states $h$, while still allowing rates to differ between hidden states (e.g., $\lambda_A \neq \lambda_B$). By comparing the fit of a full trait-dependent model to this more flexible null, HiSSE provides a much more rigorous test for trait-dependent diversification.

At the tips of the phylogeny, where only the observed state $i$ is known, the model accommodates the uncertainty in the [hidden state](@entry_id:634361) by **marginalizing**—summing the likelihoods across all possible hidden states [@problem_id:2567036]. This mechanism allows the model to explain rapid diversification in a [clade](@entry_id:171685) with trait 0 not by attributing it to trait 0 itself, but perhaps by inferring a high probability that those lineages are in a fast-evolving hidden state. By accounting for background [rate heterogeneity](@entry_id:149577) in this way, HiSSE reduces the risk of false positives while retaining the [statistical power](@entry_id:197129) to detect true trait-diversification correlations when they exist [@problem_id:2567036].

### Practical Considerations: The Impact of Sampling

The theoretical models described above rest on assumptions, and one of the most critical is how taxa are sampled for inclusion in the phylogeny. Violations of these assumptions can severely bias results.

A common assumption is **[random sampling](@entry_id:175193)**, where every extant species in a [clade](@entry_id:171685) has an equal and independent probability of being included in the study. In practice, sampling is often non-random. One common form of non-random sampling is **diversified sampling**, where researchers intentionally select species to maximize [phylogenetic diversity](@entry_id:138979), often by avoiding the inclusion of very closely related species [@problem_id:2567029].

Diversified sampling systematically alters the structure of the resulting [phylogeny](@entry_id:137790). By construction, it prunes away the most recent branching events, creating an artificial deficit of nodes near the present. This gives the tree a "stemmy" appearance, with longer-than-expected terminal branches. The distribution of branching times is therefore stochastically older compared to a randomly sampled tree of the same size [@problem_id:2567029].

If a tree generated by diversified sampling is analyzed using a likelihood method that assumes random sampling, the parameter estimates will be biased. The model will attempt to explain the anomalous lack of recent nodes in one of two ways [@problem_id:2567029]:
1.  By inferring a lower [speciation rate](@entry_id:169485) ($\lambda$), since fewer branching events are observed overall.
2.  By inferring a spuriously high [extinction rate](@entry_id:171133) ($\mu$), as extinction preferentially prunes recent lineages and can thus create a similar pattern of node deficit near the present.

This highlights a critical lesson for practitioners: understanding the sampling process is not a peripheral detail but a central component of robust diversification analysis. The biases induced by non-[random sampling](@entry_id:175193) can be substantial, potentially leading to incorrect conclusions about the [tempo and mode of evolution](@entry_id:202710). Notably, as the sampling fraction approaches completeness ($f \to 1$), the distinction between random and diversified sampling disappears, and the bias vanishes [@problem_id:2567029].