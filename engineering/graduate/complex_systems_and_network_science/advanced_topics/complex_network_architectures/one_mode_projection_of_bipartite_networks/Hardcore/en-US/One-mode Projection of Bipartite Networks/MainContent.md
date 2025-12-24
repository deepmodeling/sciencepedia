## Introduction
Bipartite networks, which connect two distinct types of nodes, are common across many scientific domains. However, a primary analytical goal is often to understand the relationships *within* one of those node sets—for example, how scientists are connected through co-authorship, or how drugs are related through common protein targets. These relationships are implicit in the bipartite structure, posing a challenge for direct analysis. One-mode projection is the fundamental method for making these implicit connections explicit. It systematically transforms a bipartite graph into a standard one-mode network, where nodes of the same type are directly linked based on their shared affiliations.

While powerful, this transformation is not a simple [data reduction](@entry_id:169455). Naive projection can introduce significant biases and artifacts, such as creating artificially dense cliques and obscuring the true community structure, leading to potentially misleading conclusions. Understanding and mitigating these effects is critical for sound analysis. This article provides a comprehensive guide to [one-mode projection](@entry_id:911765). In **"Principles and Mechanisms"**, we will dissect the core mathematical framework, explore the structural consequences of projection, and introduce advanced weighting schemes to correct for biases. Following this, **"Applications and Interdisciplinary Connections"** will demonstrate how these methods are applied in fields from biology to economics, examining extensions for signed, directed, and temporal data. Finally, **"Hands-On Practices"** will offer the opportunity to solidify your understanding by tackling practical problems and deriving key formulas.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanics of transforming [bipartite networks](@entry_id:1121658) into one-mode projections. We will begin by establishing the basic mathematical framework for this transformation, then explore the profound structural consequences and analytical pitfalls inherent in the process, and finally, introduce a range of advanced weighting schemes designed to mitigate these issues and tailor projections for specific analytical goals.

### The Basic Projection: From Shared Neighbors to Matrix Products

A bipartite network consists of two [disjoint sets](@entry_id:154341) of nodes, which we will denote as $U$ and $V$, where edges only exist between nodes from different sets. A common example is a network of actors ($U$) and the films they have appeared in ($V$). While the bipartite structure is informative, we are often interested in the relationships *between* actors, which are implicitly defined by their shared film appearances. The **[one-mode projection](@entry_id:911765)** is the primary tool for making these implicit relationships explicit.

The simplest projection onto the set $U$ creates a new network where the nodes are the elements of $U$. A connection, or **tie**, is established between two nodes, $u_i$ and $u_j$, if they share at least one common neighbor in the set $V$. The strength of this tie is often quantified by the number of these shared neighbors.

This process can be formalized using linear algebra. Let the bipartite network be represented by an **[incidence matrix](@entry_id:263683)** (or [biadjacency matrix](@entry_id:1121539)) $B$, a $|U| \times |V|$ matrix where the entry $B_{ik}$ is $1$ if an edge exists between node $u_i \in U$ and node $v_k \in V$, and $0$ otherwise. The [one-mode projection](@entry_id:911765) onto $U$ is a [weighted graph](@entry_id:269416) whose structure is captured by a weighted [adjacency matrix](@entry_id:151010), let's call it $W^{(U)}$. The weight of the tie between $u_i$ and $u_j$, denoted $w_{ij}$, is the count of their [common neighbors](@entry_id:264424) in $V$. A node $v_k$ is a common neighbor if both $u_i$ and $u_j$ are connected to it, meaning $B_{ik} = 1$ and $B_{jk} = 1$. The total number of [common neighbors](@entry_id:264424) is the sum over all possible neighbors in $V$:

$$ w_{ij} = \sum_{k=1}^{|V|} B_{ik} B_{jk} $$

This formula is precisely the definition of the $(i,j)$-th entry of the matrix product $BB^{\top}$, where $B^{\top}$ is the transpose of $B$. Therefore, the weighted [adjacency matrix](@entry_id:151010) of the [one-mode projection](@entry_id:911765) onto $U$ can be computed as:

$$ W^{(U)} = BB^{\top} $$

Symmetrically, the projection onto the set $V$ is given by the $|V| \times |V|$ matrix:

$$ W^{(V)} = B^{\top}B $$

The dimensions of these products are crucial. If $B$ is a $|U| \times |V|$ matrix, then $B^{\top}$ is a $|V| \times |U|$ matrix. The product $BB^{\top}$ has dimensions $(|U| \times |V|) \times (|V| \times |U|)$, resulting in a $|U| \times |U|$ matrix, which correctly represents a network on the nodes of $U$. Similarly, $B^{\top}B$ results in a $|V| \times |V|$ matrix for the projection onto $V$ .

For networks where the initial associations are not binary but weighted (e.g., the amount of time a person spent on a project), the entries of $B$ can be real numbers. The matrix product $W = BB^{\top}$ still holds, but the entry $w_{ij} = \sum_{k} B_{ik} B_{jk}$ is now interpreted as a **weighted co-occurrence**, aggregating the products of interaction strengths across all shared affiliations in $V$ .

An alternative and insightful algebraic perspective reveals that the projection matrices are embedded within the powers of the full bipartite graph's [adjacency matrix](@entry_id:151010). If we order the nodes such that all of $U$ come first, followed by all of $V$, the adjacency matrix $A$ of the bipartite graph has a distinctive block structure:

$$ A = \begin{pmatrix} 0 & B \\ B^{\top} & 0 \end{pmatrix} $$

The zero blocks on the diagonal represent the absence of edges within $U$ and within $V$. Squaring this matrix yields:

$$ A^2 = \begin{pmatrix} 0 & B \\ B^{\top} & 0 \end{pmatrix} \begin{pmatrix} 0 & B \\ B^{\top} & 0 \end{pmatrix} = \begin{pmatrix} BB^{\top} & 0 \\ 0 & B^{\top}B \end{pmatrix} $$

This shows that the [one-mode projection](@entry_id:911765) matrices $W^{(U)} = BB^{\top}$ and $W^{(V)} = B^{\top}B$ are the diagonal blocks of $A^2$. The entries of $A^2$ count the number of paths of length two between nodes. Thus, the weight $w_{ij}$ in the projection onto $U$ is precisely the number of paths of length 2 between $u_i$ and $u_j$, each of which must pass through a node in $V$ .

A final but critical detail concerns the diagonal entries of the [projection matrix](@entry_id:154479). The formula for a diagonal entry $w_{ii}$ is:

$$ w_{ii} = \sum_{k=1}^{|V|} B_{ik} B_{ik} = \sum_{k=1}^{|V|} B_{ik}^2 $$

For a binary incidence matrix, where $B_{ik} \in \{0, 1\}$, we have $B_{ik}^2 = B_{ik}$. The expression thus simplifies to:

$$ w_{ii} = \sum_{k=1}^{|V|} B_{ik} = k_i $$

The diagonal entry $w_{ii}$ is simply the **degree** of node $u_i$ in the original [bipartite graph](@entry_id:153947). It represents the number of paths of length 2 from node $i$ back to itself. Since one-mode projections are typically used to study relationships *between distinct* nodes, these self-loops are often considered artifacts of the [projection method](@entry_id:144836). Their presence can inflate measures of a node's importance (like weighted degree or strength) by an amount equal to its original bipartite degree. Therefore, it is standard practice to set the diagonal entries to zero after computing the initial $BB^{\top}$ matrix. However, as we will see, these diagonal values are crucial for certain normalization schemes  .

### Structural Consequences and Analytical Traps

While [one-mode projection](@entry_id:911765) is a powerful tool for simplifying network data, it is a **lossy transformation** that can profoundly alter the network's structure. Understanding these consequences is critical for avoiding misinterpretation of the resulting one-mode graph.

#### Clique Formation

The most dramatic structural effect of projection is the formation of dense, fully connected subgraphs, or **cliques**. Consider a single event node $v \in V$ that is connected to $s_v$ different participant nodes in $U$. These $s_v$ participants form the neighborhood of $v$. In the [one-mode projection](@entry_id:911765) onto $U$, any two of these participants are connected because they share $v$ as a common neighbor. Since this is true for every pair among the $s_v$ participants, they form a [clique](@entry_id:275990) of size $s_v$ in the projected graph.

This single event $v$ thus induces a highly dense structure. The number of edges created by this event alone is $\binom{s_v}{2}$. More complex structures, like triangles, also proliferate. A triangle consists of three nodes that are all mutually connected. Within the [clique](@entry_id:275990) of size $s_v$, any three nodes form a triangle. The number of distinct triangles induced solely by this single event is the number of ways to choose 3 nodes from the $s_v$ participants, which is given by the [binomial coefficient](@entry_id:156066):

$$ \text{Number of triangles} = \binom{s_v}{3} = \frac{s_v(s_v-1)(s_v-2)}{6} $$

This formula reveals that the number of triangles grows cubically with the event size $s_v$. A single large event (e.g., a blockbuster movie with a large cast, a highly cited paper with many authors) can therefore introduce a massive number of triangles and other dense motifs into the projection, potentially overwhelming more subtle structural patterns  .

#### Information Loss and Spurious Ties

The process of projection discards significant information. The resulting weight $w_{ij}$ is simply a scalar count (or sum) of shared affiliations. The identity of *which* nodes in $V$ mediated the tie is lost. For example, knowing $w_{ij}=2$ does not tell us whether the tie is due to shared neighbors $\{v_1, v_2\}$ or $\{v_3, v_4\}$. Consequently, the original [bipartite graph](@entry_id:153947) generally cannot be uniquely reconstructed from its [one-mode projection](@entry_id:911765)(s) .

This leads to the creation of what are often called **spurious ties**. This term does not imply the ties are erroneous, but rather that they represent indirect relationships that did not exist as direct edges in the original bipartite graph. In the projection, a path of length 2 (e.g., $u_i \rightarrow v_k \rightarrow u_j$) is collapsed into a direct edge of length 1. This systematically halves the shortest path distances between nodes in the projected set, distorting the topological landscape of the network.

The most dangerous consequence of this structural distortion is the potential to **merge distinct communities**. Consider a scenario with two distinct groups of actors, $U_1$ and $U_2$. Let $U_1$ be the cast of horror films ($V_1$) and $U_2$ be the cast of romantic comedies ($V_2$). If there is a set of "crossover" films ($V_s$) that feature actors from both genres, these shared films will create links between actors in $U_1$ and $U_2$ in the projection. If the number of shared films $m_s = |V_s|$ is large enough compared to the number of exclusive films $m_e = |V_1| = |V_2|$, the density of inter-community ties can become so high that [community detection algorithms](@entry_id:1122700), such as those based on [modularity maximization](@entry_id:752100), may fail to resolve the two original groups. The projection effectively erases the boundary, merging them into a single, large community. This phenomenon, where the projection machinery itself creates misleading community structures, is a critical pitfall for any analysis that relies on community detection in projected networks .

### Advanced Weighting Schemes: Normalization and Context

The simple co-occurrence count $w_{ij} = \sum_k B_{ik} B_{jk}$ suffers from a significant bias: it favors nodes that are highly connected. A very popular actor (high degree in $U$) or a very large film project (high degree in $V$) will naturally contribute to higher co-occurrence counts, which may not reflect a specific or meaningful relationship. To address this, a variety of advanced weighting schemes have been developed to normalize the projection weights.

#### Cosine Similarity

One of the most common [normalization techniques](@entry_id:1128890) is **[cosine similarity](@entry_id:634957)**. This approach treats each node $u_i \in U$ as a vector $\mathbf{b}_i$ in a $|V|$-dimensional space, where the $k$-th component of the vector is $B_{ik}$. The similarity between two nodes $u_i$ and $u_j$ is then measured by the cosine of the angle between their vectors, $\mathbf{b}_i$ and $\mathbf{b}_j$. The formula is:

$$ w_{ij}^{(\text{cos})} = \frac{\mathbf{b}_i \cdot \mathbf{b}_j}{\|\mathbf{b}_i\| \|\mathbf{b}_j\|} $$

The numerator, the dot product $\mathbf{b}_i \cdot \mathbf{b}_j$, is exactly the simple co-occurrence count, $\sum_k B_{ik} B_{jk}$. The denominator involves the Euclidean norms of the vectors. The squared norm of $\mathbf{b}_i$ is $\|\mathbf{b}_i\|^2 = \sum_k B_{ik}^2 = \sum_k B_{ik} = k_i$, which is the degree of node $u_i$. The final expression for the weight is thus:

$$ w_{ij}^{(\text{cos})} = \frac{\sum_k B_{ik} B_{jk}}{\sqrt{k_i k_j}} $$

This weight is normalized to the range $[0, 1]$. It effectively discounts the raw number of shared neighbors by the [geometric mean](@entry_id:275527) of the participants' degrees. Two actors who have only worked on two films together might have a very high similarity if those are the only two films they have ever been in, whereas two superstars who share two films out of hundreds would have a very low similarity. This method directly corrects for the "popularity" of the nodes in $U$ .

#### Jaccard Index

Another popular set-based measure is the **Jaccard index**. Instead of just counting the number of shared neighbors (the intersection of their neighborhoods), it normalizes this count by the total number of unique neighbors they have between them (the union of their neighborhoods). If $N(i)$ is the set of neighbors of node $i$ in $V$, the Jaccard weight is:

$$ w_{ij}^{(\text{jacc})} = \frac{|N(i) \cap N(j)|}{|N(i) \cup N(j)|} $$

Using the [principle of inclusion-exclusion](@entry_id:276055), $|N(i) \cup N(j)| = |N(i)| + |N(j)| - |N(i) \cap N(j)|$. In terms of the incidence matrix entries and degrees, this becomes:

$$ w_{ij}^{(\text{jacc})} = \frac{\sum_k B_{ik} B_{jk}}{k_i + k_j - \sum_k B_{ik} B_{jk}} $$

Like [cosine similarity](@entry_id:634957), the Jaccard index produces a value between $0$ and $1$ and controls for the size of the nodes' neighborhoods .

#### Normalization by Event Size

The aforementioned methods correct for the degrees of nodes in $U$. An alternative approach is to correct for the size of the "events" in $V$. The rationale is that a shared affiliation with a small, exclusive event (e.g., a niche workshop) is more indicative of a strong tie than a shared affiliation with a massive, promiscuous event (e.g., a major international conference).

A prominent example is the **Newman collaboration weight**. This scheme is designed such that the total weighted degree (strength) of any actor $i$ in the projected network is exactly equal to the number of events they participated in. This is achieved with the following weight definition, where $s_p = \sum_u B_{up}$ is the size of event $p$:

$$ w_{ij}^{(\text{newman})} = \sum_{p \in V, s_p \ge 2} \frac{B_{ip} B_{jp}}{s_p - 1} $$

For each shared event $p$, the pair $(i, j)$ receives a contribution of $1/(s_p - 1)$. This term precisely ensures that when summed over all of actor $i$'s collaborators, each event $p$ contributes exactly $1$ to actor $i$'s total strength. This elegantly down-weights contributions from larger events .

A similar idea is found in weighting schemes inspired by **Term Frequency-Inverse Document Frequency (TF-IDF)** from information retrieval. Here, each event (or "attribute") $v_k$ is assigned a weight that is inversely related to its prevalence. A common choice for this weight is the Inverse Document Frequency:

$$ \mathrm{idf}_k = \ln\left(\frac{|U|}{n_k}\right) $$

where $n_k$ is the degree of node $v_k$ (the number of users connected to attribute $k$). The projected weight $w_{ij}$ is then the sum of the IDF scores of all shared attributes:

$$ w_{ij}^{(\text{idf})} = \sum_{k=1}^{|V|} B_{ik} B_{jk} \cdot \mathrm{idf}_k $$

This can be expressed compactly in matrix form. If we define $\Lambda$ as a diagonal matrix with the IDF weights on its diagonal, the full weighted [projection matrix](@entry_id:154479) is $W = B \Lambda B^{\top}$. This highlights the flexibility of the linear algebraic framework, which can accommodate various context-specific weighting schemes by modifying the matrix sandwiched between $B$ and $B^{\top}$ .

The choice of [projection method](@entry_id:144836) and weighting scheme is not trivial; it is a critical modeling decision that should be guided by the research question and a clear understanding of the underlying assumptions and potential artifacts of each approach.