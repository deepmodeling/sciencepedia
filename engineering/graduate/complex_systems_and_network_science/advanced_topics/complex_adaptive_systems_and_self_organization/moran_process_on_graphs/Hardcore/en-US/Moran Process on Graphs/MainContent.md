## Introduction
The Moran process is a cornerstone model in [evolutionary dynamics](@entry_id:1124712), offering a stochastic framework for understanding how new traits spread through a population. While classical formulations assume a "well-mixed" population where any individual can interact with any other, this assumption rarely holds in the real world. From social networks to cellular microenvironments, interactions are constrained by an underlying structure. This article addresses this critical gap by extending the Moran process to graphs, exploring how network topology profoundly influences evolutionary outcomes. By moving beyond the mean-field approximation of complete graphs, we uncover a rich landscape of dynamics where the structure itself can amplify, suppress, or even neutralize the effects of selection.

This article will guide you through the theoretical foundations and practical applications of the Moran process on graphs. In "Principles and Mechanisms," you will learn the mathematical machinery behind different update rules, the concept of fixation probability, and the duality between evolutionary processes and [random walks](@entry_id:159635). Following this, "Applications and Interdisciplinary Connections" will demonstrate how these principles play out on various network structures, from regular graphs to highly heterogeneous ones, and reveal connections to fields like [evolutionary game theory](@entry_id:145774), [population genetics](@entry_id:146344), and translational medicine. Finally, "Hands-On Practices" will provide you with the opportunity to apply these concepts through targeted exercises, solidifying your understanding and building your analytical toolkit.

## Principles and Mechanisms

This chapter delves into the core principles and mathematical machinery of the Moran process, a fundamental model in [evolutionary dynamics](@entry_id:1124712). We begin by formalizing the classical Moran process in a well-mixed population and then extend this framework to structured populations represented by graphs. We will explore how graph topology interacts with different update rules to shape evolutionary outcomes, introducing key concepts such as [fixation probability](@entry_id:178551), update rule taxonomies, and the duality with [random walks](@entry_id:159635). Finally, we will examine advanced topics, including the role of network structure in amplifying or suppressing selection and the impact of mutation on long-term dynamics.

### The Classical Moran Process in Well-Mixed Populations

The simplest setting for an [evolutionary process](@entry_id:175749) is a **well-mixed population**, where every individual is equally likely to interact with every other individual. In network terms, this corresponds to a **complete graph** $K_N$, where $N$ is the constant population size. The classical Moran process models the stochastic evolution of types within such a population.

Let us consider two types of individuals: a **mutant** type with [relative fitness](@entry_id:153028) $r > 0$ and a **resident** type with a baseline fitness of $1$. The state of the system can be described by the number of mutants, denoted by $i$, which can range from $0$ to $N$. The states $i=0$ (extinction of mutants) and $i=N$ (fixation of mutants) are **[absorbing states](@entry_id:161036)**: once the process reaches either of these states, it remains there indefinitely in the absence of mutation.

A single time step in the Moran process consists of one birth and one death event. The specific sequence defines the update rule. The canonical version is a **birth-death (Bd)** process :
1.  **Birth:** An individual is chosen to reproduce with a probability proportional to its fitness.
2.  **Death:** An individual is chosen to die uniformly at random from the entire population.
3.  **Replacement:** The offspring of the reproducing individual replaces the individual chosen to die.

Let's quantify the dynamics of this process. When there are $i$ mutants and $N-i$ residents, the total fitness of the population is $F = i \cdot r + (N-i) \cdot 1$.

The probability of choosing a mutant to reproduce is the ratio of the total fitness of mutants to the total fitness of the population:
$P(\text{mutant reproduces}) = \frac{ri}{ri + N - i}$.

Similarly, the probability of choosing a resident to reproduce is:
$P(\text{resident reproduces}) = \frac{N-i}{ri + N - i}$.

Since death is uniform, the probability of a specific individual being chosen to die is $1/N$. Thus, the probability of choosing a mutant to die is $i/N$, and the probability of choosing a resident to die is $(N-i)/N$.

From these probabilities, we can define the one-step [transition probabilities](@entry_id:158294) for the number of mutants, $i$. The number of mutants can increase by one, decrease by one, or stay the same.

-   The number of mutants increases by one ($i \to i+1$) if a mutant reproduces and a resident dies. The probability of this transition, denoted $T_i^{+}$, is:
    $T_i^{+} = P(\text{mutant reproduces}) \times P(\text{resident dies}) = \frac{ri}{ri + N - i} \cdot \frac{N-i}{N}$

-   The number of mutants decreases by one ($i \to i-1$) if a resident reproduces and a mutant dies. The probability of this transition, denoted $T_i^{-}$, is:
    $T_i^{-} = P(\text{resident reproduces}) \times P(\text{mutant dies}) = \frac{N-i}{ri + N - i} \cdot \frac{i}{N}$

-   The number of mutants remains unchanged ($i \to i$) if the type of the reproducing individual is the same as the type of the dying one. The probability of this [self-loop](@entry_id:274670), $T_i^{0}$, is simply $1 - T_i^{+} - T_i^{-}$.

These [transition probabilities](@entry_id:158294) define a discrete-time Markov chain on the states $\{0, 1, \dots, N\}$. Starting from a single mutant ($i=1$), this process will eventually reach one of the [absorbing states](@entry_id:161036), $i=0$ or $i=N$. The probability of reaching $i=N$ is known as the **[fixation probability](@entry_id:178551)**.

A crucial conceptual point is the distinction between absolute and [relative fitness](@entry_id:153028). If we were to scale the [absolute fitness](@entry_id:168875) of both types by a positive constant $\lambda$, such that the mutant fitness becomes $\lambda r$ and the resident fitness becomes $\lambda$, the total fitness would be $F' = i(\lambda r) + (N-i)\lambda = \lambda F$. The [transition probabilities](@entry_id:158294) remain unchanged, as the factor $\lambda$ cancels out from the numerator and denominator in the reproduction probability calculation. This demonstrates that for this class of models, the [evolutionary dynamics](@entry_id:1124712) depend only on the **[relative fitness](@entry_id:153028)** $r$ .

### Moran Process on General Graphs: A Taxonomy of Update Rules

Real-world populations are rarely well-mixed. Their structure can be represented by a graph $G=(V, E)$, where vertices $V$ represent individuals and edges $E$ represent potential pathways for interaction. The Moran process on graphs extends the classical model by making reproduction and replacement events local. The specific way in which locality is implemented defines the **update rule**, and different rules can lead to dramatically different outcomes. Three of the most common update rules are Birth-death (Bd), Death-birth (dB), and Link Dynamics (LD) .

#### Birth-Death (Bd) Updating
In Bd updating, selection acts globally on birth, while competition for replacement is local and neutral.
1.  **Birth:** An individual $i \in V$ is chosen to reproduce with probability proportional to its fitness, $f_i / \sum_{k \in V} f_k$. This selection is global.
2.  **Death:** The offspring replaces one of the parent's neighbors, $j \in N(i)$, chosen uniformly at random. This competition is local and neutral.

#### Death-Birth (dB) Updating
In dB updating, death occurs globally and neutrally, while competition to fill the resulting vacancy is local and fitness-dependent.
1.  **Death:** A vertex $j \in V$ is chosen to be replaced uniformly at random (with probability $1/N$).
2.  **Birth:** The vacant site at $j$ is filled by an offspring from one of its neighbors, $i \in N(j)$. The competing neighbors are chosen with probability proportional to their fitness, $f_i / \sum_{\ell \in N(j)} f_\ell$.

#### Link Dynamics (LD) or Imitation Updating
In LD, the entire update event is localized to a single edge.
1.  **Link Selection:** An edge $\{i, j\} \in E$ is chosen uniformly at random.
2.  **Competition:** The two individuals at the ends of the edge compete. Individual $i$ replaces $j$ with probability $f_i / (f_i + f_j)$, and $j$ replaces $i$ with probability $f_j / (f_i + f_j)$.

The choice of update rule is a critical modeling decision, as it defines the "effective competition set" for each event and thereby alters the [evolutionary dynamics](@entry_id:1124712) .

### Formalizing Transition Probabilities on Graphs

To analyze the Moran process on a general graph, we must move from tracking the number of mutants to tracking the full configuration of types on the graph. A configuration can be represented by the set $S \subseteq V$ of vertices occupied by mutants. The state space is thus the set of all $2^N$ possible configurations.

#### Transition Probabilities for Birth-Death (Bd)
Let's derive the probability of a single resident at vertex $v \in V \setminus S$ becoming a mutant, a transition from state $S$ to $S \cup \{v\}$ . This occurs if a mutant neighbor of $v$ reproduces and its offspring replaces the individual at $v$. We must sum over all possible mutant neighbors $u \in S \cap N(v)$ that could cause this event.

For each such reproducing mutant $u$, the sequence of events is:
1.  Parent $u$ is chosen: probability $\frac{r}{F(S)}$, where $F(S) = r|S| + (N-|S|)$ is the total fitness.
2.  Neighbor $v$ is chosen for replacement: probability $\frac{1}{d(u)}$, where $d(u)$ is the degree of $u$.

The total [transition probability](@entry_id:271680) is the sum over all possible parents $u$:
$P(S \to S \cup \{v\}) = \sum_{u \in S \cap N(v)} \frac{r}{F(S)} \cdot \frac{1}{d(u)}$.

Similarly, the probability of a mutant at vertex $v \in S$ being replaced by a resident (transition $S \to S \setminus \{v\}$) is found by summing over all its resident neighbors $w \in (V \setminus S) \cap N(v)$:
$P(S \to S \setminus \{v\}) = \sum_{w \in (V \setminus S) \cap N(v)} \frac{1}{F(S)} \cdot \frac{1}{d(w)}$.

Notice the explicit dependence on the degree of the *reproducing* individual ($d(u)$ or $d(w)$).

#### Transition Probabilities for Death-Birth (dB)
Now, let's derive the same [transition probability](@entry_id:271680), $P(S \to S \cup \{v\})$, for the dB update rule . Here, the event unfolds differently:
1.  Vertex $v$ is chosen to die: probability $1/N$.
2.  The vacant site at $v$ is filled by a neighbor. For the new type to be mutant, a mutant neighbor must be chosen. The neighbors of $v$ compete based on fitness. The probability of a mutant winning this competition is $\frac{\text{total fitness of mutant neighbors}}{\text{total fitness of all neighbors}}$.

Let $N(v)$ be the set of neighbors of $v$. The total fitness of these competing neighbors is $W_v = r|N(v) \cap S| + |N(v) \setminus S|$. The probability of a mutant neighbor being chosen is $\frac{r|N(v) \cap S|}{W_v}$.

Combining these steps, the total [transition probability](@entry_id:271680) is:
$P(S \to S \cup \{v\}) = \frac{1}{N} \cdot \frac{r|N(v) \cap S|}{r|N(v) \cap S| + |N(v) \setminus S|}$.

Similarly, the probability of losing a mutant at $v \in S$ is:
$P(S \to S \setminus \{v\}) = \frac{1}{N} \cdot \frac{|N(v) \setminus S|}{r|N(v) \cap S| + |N(v) \setminus S|}$.

A direct comparison of the Bd and dB rules reveals their fundamental differences . In Bd, the dynamics are influenced by the degree of the *reproducer*, $d(u)$. In dB, the dynamics depend on the composition and degree of the neighborhood of the *dying* vertex, $d(v)$. Because of this, the two update rules are not equivalent, even under neutral selection ($r=1$), unless the graph is regular (all vertices have the same degree).

### Duality, Selection, and Advanced Concepts

#### Duality with Coalescing Random Walks
For the neutral Moran process ($r=1$), a powerful analytical tool known as **duality** exists. Specifically, the neutral death-birth process on a graph is dual to a system of [coalescing random walks](@entry_id:1122581) . To find the fixation probability of an initial set of mutants $S$, we can trace the ancestry of the entire population backward in time. This is equivalent to starting one "ancestral lineage" (or random walker) at each vertex and letting them move and coalesce.

At each backward step, one vertex $u$ is chosen uniformly. The walker at $u$ jumps to a random neighbor $v$. If the destination $v$ is already occupied by another walker, they coalesce into one. This process continues until only one walker remains. The [fixation probability](@entry_id:178551) of the mutant type, $\rho(S)$, is the probability that this single common ancestor originated in the set $S$.

For the dB process, it can be shown that the probability of the common ancestor originating at a specific vertex $i$ is given by its weight in the [stationary distribution](@entry_id:142542) of a [simple random walk](@entry_id:270663) on the graph:
$\rho(\{i\}) = \pi_i = \frac{d(i)}{\sum_{j \in V} d(j)} = \frac{d(i)}{2m}$, where $m$ is the number of edges.

This implies that hubs (high-degree nodes) have a higher-than-average [fixation probability](@entry_id:178551) under neutral dB dynamics. For a general initial set $S$, the fixation probability is the sum of the initial probabilities:
$\rho(S) = \sum_{i \in S} \pi_i = \sum_{i \in S} \frac{d(i)}{2m}$.

In the special case of a $k$-[regular graph](@entry_id:265877), where $d(i)=k$ for all $i$, this simplifies to $\rho(S) = \sum_{i \in S} \frac{k}{Nk} = \frac{|S|}{N}$, recovering the intuitive result for well-mixed populations.

#### Amplifiers and Suppressors of Selection
The structure of a graph can either enhance or diminish the effects of natural selection compared to a well-mixed population. A graph $G$ is called an **amplifier of selection** if an advantageous mutant ($r>1$) has a higher fixation probability on $G$ than on the complete graph $K_N$. It is a **suppressor of selection** if the mutant has a lower [fixation probability](@entry_id:178551) .

For the birth-death (Bd) process, this property is closely linked to the concept of **vertex temperature**. The temperature of a vertex $i$ is a measure of its replacement risk. For an unweighted, [undirected graph](@entry_id:263035) under Bd updating, it is defined as:
$$T_i = \sum_{j \in N(i)} \frac{1}{d(j)}$$

This definition captures the fact that vertex $i$ is at risk of being replaced by any of its neighbors $j$, and the likelihood of this happening depends inversely on the degree of neighbor $j$ (since $j$'s offspring are distributed among all $d(j)$ of its neighbors). A vertex surrounded by low-degree neighbors has a high temperature (a "hot spot"), while a vertex surrounded by hubs has a low temperature (a "cold spot").

The **isothermal theorem** states that if the temperature $T_i$ is constant for all vertices in the graph, then the [fixation probability](@entry_id:178551) is identical to that of a well-mixed population. Such graphs are neutral to selection. All regular graphs are isothermal.

It is the *heterogeneity* of vertex temperatures that drives amplification or suppression. For the Bd process, a high variance in $\{T_i\}$ is positively correlated with amplification of selection. Intuitively, "cold spots" act as safe havens where mutants can survive the vulnerable early stages and launch a successful invasion. This benefit outweighs the risk of starting in a "hot spot". A star graph, with one very hot central vertex and many very cold [peripheral vertices](@entry_id:264062), is a canonical example of a strong amplifier of selection under Bd updating.

This concept can be generalized to weighted [directed graphs](@entry_id:272310), where the temperature $T_i$ is simply the sum of all incoming dispersal weights to vertex $i$. Under neutral drift, the probability of vertex $i$ being replaced in a single step is then elegantly given by $T_i/N$ .

#### The Moran Process with Mutation
So far, we have considered models without mutation, where fixation or extinction are the only possible long-term outcomes. Introducing a symmetric **[mutation rate](@entry_id:136737)** $\mu \in (0,1)$, where an offspring adopts the opposite type with probability $\mu$, fundamentally changes the nature of the process .

With mutation, no state is absorbing. A population of all mutants can produce a resident through mutation, and vice versa. This ensures that it is possible to get from any configuration to any other configuration. Consequently, the Markov chain on the $2^N$ configuration states becomes **irreducible**. Furthermore, because a replacement event can result in the same type occupying the vertex (either through non-mutation to the same type or mutation to the same type), every state has a positive probability of a [self-loop](@entry_id:274670), making the chain **aperiodic**.

A finite, irreducible, and aperiodic Markov chain is **ergodic**. This guarantees the existence of a **unique stationary distribution**. Instead of fixating, the system approaches a [statistical equilibrium](@entry_id:186577) where both mutant and resident types coexist, with their frequencies fluctuating around the mean values prescribed by this stationary distribution.