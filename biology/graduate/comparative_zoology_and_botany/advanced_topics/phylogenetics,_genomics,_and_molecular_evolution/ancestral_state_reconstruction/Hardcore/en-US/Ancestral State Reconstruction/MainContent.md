## Introduction
Reconstructing the traits of extinct ancestors is a central goal in evolutionary biology, transforming [phylogenetic trees](@entry_id:140506) from static diagrams of relationships into dynamic historical narratives. But how do we scientifically infer the characteristics of organisms that lived millions of years ago? How do we choose between competing methods, and what are the critical assumptions and potential pitfalls underlying these inferences?

This article addresses these questions by providing a comprehensive guide to Ancestral State Reconstruction (ASR). We will begin by exploring the foundational principles and mechanisms of the three major inferential frameworks: [parsimony](@entry_id:141352), maximum likelihood, and Bayesian inference. Next, we will survey the wide-ranging applications of these methods in fields from molecular evolution to [biogeography](@entry_id:138434), illustrating how ASR is used to test major evolutionary hypotheses. Finally, we will solidify this knowledge through a series of hands-on practices designed to build practical skills in applying these powerful techniques. To begin our journey, we must first understand the formal models that provide the logical and mathematical basis for reconstructing the past.

## Principles and Mechanisms

### Foundations of Character-State Models

The inference of ancestral [character states](@entry_id:151081) is predicated on a formal, quantitative model of how those characters evolve through time along the branches of a phylogenetic tree. The initial, and perhaps most critical, step in any such analysis is the precise definition of the character itself and its possible states.

#### Defining Characters and States

In a phylogenetic context, a **character** is a feature of an organism that is considered to be homologous across the group of taxa under study. Homology implies a shared ancestry, ensuring that we are comparing equivalent features (e.g., the forelimb of a bat and a human) rather than analogous ones that arose independently (e.g., the wing of a bat and the wing of an insect). For a character to be phylogenetically informative, it must also be heritable and exhibit variation among the taxa.

The different forms that a character can take are called its **states**. For a discrete character, these states must be defined as a [finite set](@entry_id:152247) of mutually exclusive conditions. For example, if we are studying the evolution of leaf margins in a plant group, "leaf margin" is the character. We might define its states as "entire," "serrate," and "lobed." A given taxon in our dataset would be assigned one, and only one, of these states. This careful partitioning of continuous biological variation into discrete, homologous states is a foundational act of abstraction in [comparative biology](@entry_id:166209).

#### Ordered versus Unordered Multistate Characters

When a character has more than two states, we must make a crucial modeling decision: should the states be treated as **ordered** or **unordered**? This choice imposes a specific hypothesis about the allowable pathways of evolutionary change.

An **unordered character** model assumes that a direct transition is possible between any pair of distinct states. This is the most general and conservative assumption. For instance, considering flower symmetry with states "radial," "bilateral," and "asymmetric," an unordered model would permit direct evolution from radial to asymmetric, or any other pairing, in a single conceptual step. This is the default assumption in the absence of strong evidence to the contrary, as imposing an order without justification can bias the reconstruction by disallowing potentially real evolutionary transitions.

An **ordered character** model, by contrast, constrains evolution to a specific, linear path. If we were to code our flower symmetry states as $0$ (radial), $1$ (bilateral), and $2$ (asymmetric), an ordered model might only permit transitions between adjacent states: $0 \leftrightarrow 1$ and $1 \leftrightarrow 2$. A change from state $0$ to state $2$ would be required to pass through the intermediate state $1$. This choice should only be made if there is compelling external evidence—for example, from [developmental genetics](@entry_id:263218)—that suggests such a constrained pathway is biologically necessary.

This decision has profound consequences for both major classes of reconstruction methods. In a **maximum parsimony** framework, an unordered model (Fitch [parsimony](@entry_id:141352)) assigns a cost of one step to any change, so a transition from state $0$ to state $2$ costs $1$. An ordered model (Wagner [parsimony](@entry_id:141352)) defines the cost as the number of steps along the path, so a change from $0$ to $2$ costs $|2-0| = 2$. In a **likelihood** framework based on Continuous-Time Markov Chains (CTMCs), an unordered model allows the [instantaneous rate of change](@entry_id:141382), $q_{ij}$, to be positive for any pair of states $i \neq j$. An ordered model explicitly sets the rates for non-adjacent transitions to zero (e.g., $q_{02} = q_{20} = 0$), forcing evolution between non-adjacent states to occur over time via the intermediate state(s).

### The Principle of Maximum Parsimony

Maximum parsimony is a character-based method of inference that operates on a simple but powerful principle: prefer the hypothesis of evolutionary relationships and ancestral states that requires the minimum number of evolutionary changes. It is an application of Occam's razor to phylogenetics.

To reconstruct an ancestral state, [parsimony](@entry_id:141352) seeks the [state assignment](@entry_id:172668) for an internal node that minimizes the total count of character state changes (the [parsimony](@entry_id:141352) score) across the entire tree. A critical element for this process is a [rooted tree](@entry_id:266860). An **outgroup**—a taxon or group of taxa known to be less closely related to the group of interest (the ingroup) than its members are to each other—is used to place the root of the tree. The state of the outgroup provides the most parsimonious estimate for the state at the root of the ingroup, thereby polarizing the direction of character change.

Consider a phylogeny of mammals where a lizard is the outgroup. We are interested in the state of [lactation](@entry_id:155279) and reproductive mode in the last common ancestor of mammals. Suppose we observe that the lizard lacks [lactation](@entry_id:155279) (state 0), while all mammals in our study (platypus, kangaroo, human) possess it (state 1). Under [parsimony](@entry_id:141352), the most likely ancestral state for all mammals is [lactation](@entry_id:155279) present (state 1), as this requires only a single evolutionary change on the branch leading to the mammalian clade. The alternative, an ancestor without [lactation](@entry_id:155279), would require three independent gains of [lactation](@entry_id:155279) within the mammals, a far less parsimonious scenario of three changes. If the platypus is oviparous (egg-laying) like the lizard, while kangaroos and humans are viviparous (live-bearing), the same logic suggests the mammalian ancestor was oviparous. This requires only a single change to [viviparity](@entry_id:173921) on the branch leading to the kangaroo-human clade, whereas an ancestral state of [viviparity](@entry_id:173921) would require two changes: one to explain the platypus and another to explain the lizard.

#### The Fitch Algorithm

The [parsimony principle](@entry_id:173298) can be operationalized through a formal algorithm. For unordered characters, the most common is the **Fitch algorithm**, which determines the minimum number of changes and the set of possible ancestral states for each node. The algorithm involves a "bottom-up" pass (a [post-order traversal](@entry_id:273478)) from the tips of the tree to the root. For any internal node, we consider the preliminary state sets of its two immediate descendants, $S_1$ and $S_2$:

1.  If the intersection of the descendant state sets is non-empty ($S_1 \cap S_2 \neq \varnothing$), the state set for the parent node is this intersection. This implies that there is at least one state shared by both descendant lineages, making it possible to assign that state to the parent without invoking any change. The number of changes for this node is $0$.

2.  If the intersection of the descendant state sets is empty ($S_1 \cap S_2 = \varnothing$), the state set for the parent node is the union of the two sets. In this case, no state can explain both descendant lineages without a change. One change is required, and the [parsimony](@entry_id:141352) score is incremented by $1$.

This procedure is applied recursively up the tree. The sum of all increments is the total parsimony score for the character. This first pass determines the set of all possible states at each node that are compatible with a most parsimonious reconstruction. A second, "top-down" pass ([pre-order traversal](@entry_id:263452)) is then used to resolve any ambiguities and assign a specific state to each node from its set of possibilities.

### Probabilistic Models of Character Evolution

While parsimony provides a powerful and intuitive framework, it has a significant limitation: it treats all changes as equally likely, regardless of the amount of evolutionary time that has passed. Probabilistic methods address this by explicitly modeling evolution as a [random process](@entry_id:269605) that unfolds along the branches of a [phylogeny](@entry_id:137790).

#### The Mk Model for Discrete Characters

For discrete characters, the standard modeling framework is the **Continuous-Time Markov Chain (CTMC)**. A CTMC models transitions between $k$ [character states](@entry_id:151081) as a Poisson process. The model is fully specified by a $k \times k$ **rate matrix**, $Q$. Each off-diagonal entry $q_{ij}$ (for $i \neq j$) represents the instantaneous rate of transition from state $i$ to state $j$. The diagonal entries $q_{ii}$ are defined such that each row sums to zero: $q_{ii} = - \sum_{j \neq i} q_{ij}$. The value $-q_{ii}$ can be interpreted as the total rate of leaving state $i$.

The simplest and most widely used CTMC is the **Mk model** (named for Markovan k-states). It is a one-parameter model that assumes complete symmetry: the [instantaneous rate of change](@entry_id:141382) between any two distinct states is the same, denoted by a single parameter $\lambda$. Thus, for the Mk model:
-   $q_{ij} = \lambda$ for all $i \neq j$
-   $q_{ii} = -(k-1)\lambda$

Because this $Q$ matrix is symmetric ($q_{ij} = q_{ji}$), the process is reversible, and its stationary distribution $\boldsymbol{\pi}$ (the [equilibrium frequency](@entry_id:275072) of states after an infinite amount of time) is uniform. That is, $\pi_i = 1/k$ for all $k$ states. This means the model assumes, a priori, that all states are equally probable at equilibrium. It is important to note that more complex, asymmetric models exist where rates are not equal and stationary frequencies are not uniform. The Mk model's symmetry is a simplifying assumption, not a general property of all CTMCs.

The [transition probability matrix](@entry_id:262281) for a branch of length $t$, $P(t)$, is calculated from the rate matrix using the [matrix exponential](@entry_id:139347): $P(t) = \exp(Qt)$. This matrix gives the probability of ending in state $j$ given a starting state of $i$ after time $t$.

#### The Brownian Motion Model for Continuous Traits

A parallel framework exists for continuous traits, such as body size or temperature tolerance. The fundamental model is **Brownian Motion (BM)**. BM models [trait evolution](@entry_id:169508) as a random walk, where changes over any time interval are drawn from a [normal distribution](@entry_id:137477) with a mean of $0$ and a variance proportional to the length of the interval. The key parameter is the variance rate, $\sigma^2$.

A remarkable consequence of the BM model is that the trait values observed at the tips of a phylogeny, $\mathbf{X}$, will follow a **[multivariate normal distribution](@entry_id:267217) (MVN)**. The mean of this distribution is simply the value at the root of the tree (if it is assumed to be known). The covariance matrix, $\mathbf{V}$, captures the [phylogenetic relationships](@entry_id:173391). Specifically, for any two species $i$ and $j$:

-   The variance of the trait in species $i$, $\mathrm{Var}(X_i)$, is proportional to the total time from the root to tip $i$: $\mathrm{Var}(X_i) = \sigma^2 T_i$.
-   The covariance between the traits in species $i$ and $j$, $\mathrm{Cov}(X_i, X_j)$, is proportional to the length of the evolutionary path they share from the root to their [most recent common ancestor](@entry_id:136722) (MRCA): $\mathrm{Cov}(X_i, X_j) = \sigma^2 t_{ij}$.

This elegant result means that the [phylogeny](@entry_id:137790) itself directly parameterizes the expected pattern of trait similarity among relatives. Closely related species, which share a long history, are expected to be more similar (have higher covariance) than distantly related species.

#### The Centrality of the Root and Time-Reversibility

Probabilistic models, like parsimony, require a [rooted tree](@entry_id:266860) to define the direction of evolution from ancestor to descendant. However, there is a profound subtlety related to the properties of the evolutionary model itself. Most commonly used CTMCs, including the Mk and GTR models, are **time-reversible**. A process is time-reversible if the rate of flux from state $i$ to $j$ at equilibrium equals the flux from $j$ to $i$ ($\pi_i q_{ij} = \pi_j q_{ji}$).

In a seminal 1981 paper, Joseph Felsenstein showed that for any time-reversible model, the total likelihood of the observed tip data on an **[unrooted tree](@entry_id:199885)** is the same regardless of where the root is placed. The data themselves contain no information about the location of the root. While this is a convenient property for inferring [tree topology](@entry_id:165290), it poses a fundamental problem for ancestral state reconstruction. The posterior probability of a state at an internal node, $P(\text{ancestral state} \mid \text{data})$, explicitly depends on the location of the root because the root defines which nodes are ancestors and which are descendants.

Therefore, for any time-reversible model, ancestral states are not identifiable from the tip data and an [unrooted tree](@entry_id:199885) alone. To perform ASR, one must provide external information to root the tree, such as designating an outgroup or using a non-reversible model of evolution. Without a specified root, the concept of an "ancestral" state is ill-defined.

#### Parsimony versus Likelihood: A Critical Comparison

The most significant difference between parsimony and likelihood is that likelihood-based methods explicitly incorporate branch lengths as a measure of evolutionary time. This allows for a more nuanced inference that can avoid known pitfalls of parsimony, such as **[long-branch attraction](@entry_id:141763) (LBA)**.

LBA is a phenomenon where parsimony can erroneously group two distantly related lineages that happen to share a character state due to convergent evolution. Consider a four-taxon tree where two distantly related taxa, A and C, are on very long branches, and they share state 1. The other two taxa, B and O, are on short branches and share state 0. Parsimony, ignoring branch lengths, sees only the states. To explain the pattern, it can either postulate two independent changes to state 1 (on the branches to A and C) or postulate a single common origin of state 1 for A and C with subsequent reversals. Often, the latter is more parsimonious, leading to the incorrect inference that A and C share a more recent common ancestor with state 1.

A likelihood-based method, using a model like Mk, behaves very differently. The probability of a character change is a function of [branch length](@entry_id:177486). On a very long branch, the state at the end of the branch is nearly independent of the state at the beginning; the probability of change approaches the stationary frequency (e.g., 0.5 in a symmetric binary model). On a very short branch, change is highly improbable. The likelihood calculation correctly assesses that two independent changes on the two long branches leading to A and C is a relatively probable event. In contrast, the alternative scenario required by the parsimonious grouping (which would involve changes on short branches) is extremely improbable. Likelihood will therefore favor the correct reconstruction, concluding that the shared state in A and C is a product of convergence, thereby overcoming the LBA artifact.

### Bayesian Ancestral State Reconstruction

Bayesian inference extends the likelihood framework by treating not only the data but also the model parameters as random variables. Instead of finding the single parameter values that maximize the likelihood, the goal is to compute the **posterior probability distribution** of the ancestral states and parameters, given the data.

This is accomplished via Bayes' theorem. The full specification of a Bayesian model requires defining:
1.  **A likelihood function**: This is the probability of the observed tip data and latent ancestral states given the model parameters, $P(S, D \mid Q, \boldsymbol{\tau}, \pi)$. This is derived from the CTMC model, as in the maximum likelihood framework.
2.  **Prior distributions**: These express our beliefs about the model parameters ($Q$, branch lengths $\boldsymbol{\tau}$, stationary frequencies $\pi$, etc.) before observing the data. For instance, a common setup for a General Time-Reversible (GTR) model would use a Dirichlet prior for the stationary base frequencies $\pi$, Gamma priors for the [exchangeability](@entry_id:263314) rates in the $Q$ matrix, and an Exponential prior for the branch lengths.

The joint posterior distribution is proportional to the likelihood multiplied by the priors. From this, we can obtain the **marginal [posterior distribution](@entry_id:145605)** for the ancestral states by integrating out all the "nuisance" parameters. This process, typically performed using numerical methods like Markov Chain Monte Carlo (MCMC), has the advantage of accounting for uncertainty in all aspects of the model.

#### Interpreting Bayesian Reconstructions: Joint vs. Marginal

The output of a Bayesian ASR is a rich posterior distribution over all possible evolutionary histories. Summarizing this distribution requires care. There are two common approaches that are often confused:

1.  **Marginal Reconstruction**: This is the most common summary. For each individual node, we calculate its marginal posterior probability for each state by averaging over the states of all other nodes and all parameter values. We might then report the state with the highest [marginal probability](@entry_id:201078) for each node (the "marginal MAP").

2.  **Joint Reconstruction**: This seeks to find the single assignment of states to *all* internal nodes simultaneously that has the highest joint posterior probability (the "joint MAP"). This is the single most probable complete history of the character.

It is a critical error to assume that the vector of marginal MAP states is the same as the joint MAP reconstruction. This is not generally true, because maximization and [marginalization](@entry_id:264637) (summation) are not commutative operations. The states at different ancestral nodes are correlated. The single most probable history might involve a state at a particular node that is not that node's individual most probable state. For example, a joint posterior might give the highest probability to the configuration $(X_r=1, X_v=1)$, while the marginal probabilities for node $r$ might favor $X_r=0$. This can happen if the states are strongly correlated, such that state $1$ at node $r$ is much more likely when node $v$ is also in state $1$, even if state $1$ is marginally less likely for node $r$ overall.

### Complexities and Sources of Systematic Error

Ancestral state reconstruction methods are powerful, but their accuracy depends on the validity of their underlying assumptions. When the model used for inference does not match the true process that generated the data, [systematic errors](@entry_id:755765) can arise.

#### Hemiplasy: The Conflict Between Gene and Species Histories

A core assumption of many ASR methods is that [character evolution](@entry_id:165250) occurs on the [species tree](@entry_id:147678). However, modern genomics has shown that due to a process called **[incomplete lineage sorting](@entry_id:141497) (ILS)**, the evolutionary history of an individual gene (the gene tree) can differ from the history of the species that carry it (the species tree).

This discordance can create misleading character patterns. **Hemiplasy** occurs when a character state pattern appears homoplastic (requiring multiple independent origins) when mapped onto the [species tree](@entry_id:147678), but is actually the result of a single, parsimonious change on a discordant underlying [gene tree](@entry_id:143427). For example, consider a species tree of $((A,B),C)$. A character pattern where A and C share a derived state, while B has the ancestral state, would require two independent changes on the [species tree](@entry_id:147678). However, if ILS is prevalent, a significant fraction of genes may follow the discordant gene tree $((A,C),B)$. A single mutation on the branch leading to the A-C clade in this [gene tree](@entry_id:143427) would perfectly explain the observed pattern with only one change.

Under conditions of low [mutation rate](@entry_id:136737) and high levels of ILS (which occurs when speciation events happen in rapid succession or in species with large effective population sizes), hemiplasy can be a far more probable explanation for an apparently homoplastic pattern than true, multiple-origin homoplasy.

#### State-Dependent Diversification: When Characters Shape the Tree

Another critical assumption of standard models like Mk is that the [character evolution](@entry_id:165250) process is independent of the process of speciation and extinction that generates the tree itself. However, it is biologically plausible that certain traits could influence a lineage's rate of diversification. For example, the evolution of nectar spurs in [flowering plants](@entry_id:192199) may have accelerated speciation rates by promoting specialization with pollinators.

When this occurs, using a simple Mk model for inference on the resulting tree can lead to severe bias. If state 1 is associated with a higher [net diversification rate](@entry_id:162682) ($\text{speciation} - \text{extinction}$), lineages with state 1 will leave more descendants. The observed tips of the [phylogeny](@entry_id:137790) will thus be overwhelmingly dominated by state 1. An Mk model, which is blind to the [state-dependent diversification](@entry_id:174584) process, will observe this overabundance of state 1 tips. To explain this pattern, the model must favor an evolutionary scenario that makes state 1 common. The most likely explanation within the Mk framework is an early origin of the trait. Consequently, the model will infer a high posterior probability for state 1 at the root and other deep ancestral nodes, even if the true [transition rates](@entry_id:161581) were symmetric ($q_{01}=q_{10}$) and the true root state was 0. This artifact, where the prevalence of a state in the present biases inference about the past, is known as the **pull of the present**.

Understanding these principles and potential pitfalls is essential for the rigorous application and critical interpretation of ancestral state reconstruction in [comparative zoology](@entry_id:263663) and botany. The choice of method and model is not merely a technical detail; it is a hypothesis about the fundamental nature of the evolutionary process.