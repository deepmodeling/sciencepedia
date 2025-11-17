## Introduction
In the study of [directed graphs](@entry_id:272310), tournaments represent a special and richly structured class, modeling outcomes where every pair of participants has a clear winner and loser. While a simple count of victories, or out-degree, provides a basic measure of strength, it often fails to capture more subtle forms of influence within a competitive network. A player might be more powerful not by winning the most games, but by defeating key opponents who, in turn, hold sway over others. This article addresses this gap by introducing the concept of a "king," a vertex that embodies this idea of two-step dominance.

This exploration will guide you through the fundamental theory and diverse applications of kings in tournaments. In the first chapter, **Principles and Mechanisms**, you will learn the formal definition of a king, walk through an elegant proof that guarantees their existence in any tournament, and analyze the relationship between kingship and out-degree. Next, in **Applications and Interdisciplinary Connections**, we will examine how this theoretical concept serves as a powerful model for social hierarchies and market competition, and explore its deeper connections to graph structure, computational complexity, and [random processes](@entry_id:268487). Finally, the **Hands-On Practices** chapter will provide an opportunity to solidify your understanding by working through concrete examples and computational problems.

## Principles and Mechanisms

Having established the foundational concept of a [tournament graph](@entry_id:267858), we now delve into one of its most fascinating structural properties: the notion of a "king." This concept moves beyond simple wins and losses to capture a more nuanced form of influence or dominance within the network. In this chapter, we will formally define what it means for a vertex to be a king, prove their guaranteed existence, and explore the rich structure of the set of all kings within any given tournament.

### Defining a King

In a tournament, which represents the outcomes of a round-robin competition, a simple victory count ([out-degree](@entry_id:263181)) does not tell the whole story. A player might have a modest number of direct wins but exert significant influence by having defeated players who, in turn, defeated many others. The concept of a king formalizes this idea of two-step dominance.

Formally, a vertex $k$ in a tournament $T$ is defined as a **king** if for every other vertex $j$ in $T$ ($j \neq k$), there exists a directed path from $k$ to $j$ of length at most two. This means one of two conditions must hold:
1.  The arc $(k, j)$ exists (a path of length 1). This is a direct victory.
2.  There exists an intermediate vertex $m$ such that the arcs $(k, m)$ and $(m, j)$ both exist (a path of length 2). This represents an indirect victory.

Let $N^{+}(v)$ denote the **out-neighborhood** of a vertex $v$, which is the set of all vertices defeated by $v$. Let $N^{++}(v)$ denote the set of all vertices reachable from $v$ by a path of length exactly two. This can be expressed as $N^{++}(v) = \bigcup_{m \in N^{+}(v)} N^{+}(m)$. Using this notation, a vertex $k$ is a king if and only if the set of all other vertices is a subset of the union of its one-step and two-step out-neighborhoods: $V \setminus \{k\} \subseteq N^{+}(k) \cup N^{++}(k)$.

To illustrate this, consider a tournament on four vertices $\{1, 2, 3, 4\}$ with the arc set $A = \{(1,2), (1,4), (2,3), (2,4), (3,1), (4,3)\}$. Let's determine if vertex 1 is a king [@problem_id:1516476].
First, we identify its out-neighborhood: $N^{+}(1) = \{2, 4\}$. These are the vertices it reaches in one step.
Next, we find the vertices it can reach in two steps by looking at the out-neighborhoods of the vertices in $N^{+}(1)$:
- $N^{+}(2) = \{3, 4\}$
- $N^{+}(4) = \{3\}$
The set of vertices reachable in two steps is $N^{++}(1) = N^{+}(2) \cup N^{+}(4) = \{3, 4\} \cup \{3\} = \{3, 4\}$.
Finally, we combine the sets: $N^{+}(1) \cup N^{++}(1) = \{2, 4\} \cup \{3, 4\} = \{2, 3, 4\}$.
Since this set includes all vertices other than 1, vertex 1 is a king. A similar analysis would show that vertices 2 and 3 are also kings, but vertex 4 is not, as it cannot reach vertex 2 in one or two steps.

A particularly instructive example is the directed 3-cycle, such as a tournament on vertices $\{A, B, C\}$ with arcs $A \to B$, $B \to C$, and $C \to A$ [@problem_id:1516494]. In this "rock-paper-scissors" scenario, every vertex is a king. For instance, $A$ defeats $B$ directly (length 1) and reaches $C$ via the path $A \to B \to C$ (length 2). By symmetry, the same holds for $B$ and $C$. This demonstrates that a tournament can have multiple kings, and indeed, every vertex can be a king. This simple 3-vertex tournament is also the smallest possible tournament that can contain two kings where one defeats the other [@problem_id:1516505].

### The Existence and Identification of Kings

A natural question arises: does every tournament necessarily contain a king? The answer is yes, and the proof is elegantly tied to the concept of [out-degree](@entry_id:263181). The **out-degree** of a vertex $v$, denoted $od(v)$, is the number of outgoing arcs from $v$, corresponding to the number of direct wins. In tournament theory, this is often called the **score** of the vertex.

First, consider the extreme cases. A vertex $z$ with an [out-degree](@entry_id:263181) of 0 has defeated no other vertex. Consequently, there can be no path of length 1 or 2 originating from $z$. Such a vertex can never be a king in a tournament with more than one vertex [@problem_id:1516500] [@problem_id:1516493]. Conversely, a vertex $u$ with an in-degree of 0 (and thus an out-degree of $n-1$ in an $n$-vertex tournament) has defeated every other vertex. It reaches all other vertices via a path of length 1, trivially satisfying the king definition [@problem_id:1516493]. Such a universally winning vertex is sometimes called a **Condorcet winner**.

While a Condorcet winner is always a king, most tournaments do not have one. The following theorem, however, provides a powerful guarantee.

**Theorem:** In any tournament, any vertex with maximum [out-degree](@entry_id:263181) is a king.

**Proof:** Let $k$ be a vertex in a tournament $T$ with maximum out-degree. To show $k$ is a king, we must demonstrate that it can reach every other vertex $j$ in at most two steps. If the arc $(k, j)$ exists, the condition is met.

Now, consider the case where the arc $(k, j)$ does not exist. Since $T$ is a tournament, the arc must be $(j, k)$. We need to find a path of length 2 from $k$ to $j$. Let's assume for the sake of contradiction that no such path exists. This would mean that for every vertex $m$ in the out-neighborhood of $k$ (i.e., for all $m$ such that $k \to m$), there is no arc from $m$ to $j$. In a tournament, this implies that the arc $(j, m)$ must exist for all $m \in N^{+}(k)$.

This puts vertex $j$ in a dominant position. It defeats $k$ (by our initial assumption), and it defeats every vertex $m$ that $k$ defeats. Therefore, the out-degree of $j$ includes $k$ and all of $N^{+}(k)$. This gives:
$od(j) \geq |N^{+}(k)| + 1 = od(k) + 1$.
This inequality, $od(j) > od(k)$, contradicts our initial premise that $k$ has the maximum out-degree in the tournament. Therefore, our assumption that no path of length 2 exists must be false. There must be at least one vertex $m \in N^{+}(k)$ such that $(m, j)$ is an arc, forming the path $k \to m \to j$.

Since every finite, non-empty tournament has at least one vertex of maximum [out-degree](@entry_id:263181), this theorem proves that **every tournament has at least one king**. This elegant result is a cornerstone of tournament theory [@problem_id:1516493] [@problem_id:1516477].

### The Relationship Between Kingship and Out-Degree

The previous theorem establishes that having a maximum [out-degree](@entry_id:263181) is a *sufficient* condition for a vertex to be a king. Is it also a *necessary* condition? That is, must every king have the maximum [out-degree](@entry_id:263181)?

The answer is no. A vertex can be a king without having the highest number of wins. Consider the 5-vertex tournament with the following arcs [@problem_id:1516475]:
$A = \{(V_1,V_2), (V_1,V_3), (V_2,V_4), (V_3,V_2), (V_3,V_4), (V_3,V_5), (V_4,V_1), (V_4,V_5), (V_5,V_1), (V_5,V_2)\}$.
The out-degrees are:
- $od(V_1) = 2$
- $od(V_2) = 1$
- $od(V_3) = 3$
- $od(V_4) = 2$
- $od(V_5) = 2$

Here, $V_3$ has the unique maximum [out-degree](@entry_id:263181) of 3, and is therefore guaranteed to be a king. However, let's examine $V_1$, which has a non-maximal [out-degree](@entry_id:263181) of 2.
- $V_1$ reaches $V_2$ and $V_3$ directly.
- $V_1$ reaches $V_4$ via the path $V_1 \to V_2 \to V_4$.
- $V_1$ reaches $V_5$ via the path $V_1 \to V_3 \to V_5$.
Since $V_1$ can reach every other vertex in at most two steps, it is also a king. This demonstrates that the set of kings can include vertices that do not have the maximal out-degree.

This leads to a related question: if a tournament has a unique vertex with the maximum [out-degree](@entry_id:263181), must it be the only king? Again, the answer is no. The example above illustrates this perfectly: $V_3$ is the unique vertex with maximum out-degree, but we have shown that $V_1$ is also a king. Thus, a unique "top scorer" does not imply a unique king [@problem_id:1516493].

### Properties of Non-Kings and the Structure of the King Set

We can also characterize vertices that are *not* kings. A vertex $v$ fails to be a king if there is at least one vertex $j$ that it cannot reach in one or two steps. This means $j \to v$, and for every out-neighbor $m \in N^{+}(v)$, it holds that $j \to m$. This leads to a powerful structural insight.

A vertex $v$ is **not** a king if and only if there exists another vertex $u$ that defeats $v$ and also defeats every vertex in the out-neighborhood of $v$. In other words, $u$ dominates the set $\{v\} \cup N^{+}(v)$.

Consider a **[transitive tournament](@entry_id:267486)** on vertices $\{V_1, V_2, \dots, V_n\}$ where $V_i \to V_j$ if and only if $i  j$. Let's examine $V_3$ in such a tournament (with $n \ge 4$) [@problem_id:1516469]. $V_3$ is not a king because it cannot reach $V_1$ in one or two steps. The out-neighborhood of $V_3$ is $N^{+}(V_3) = \{V_4, V_5, \dots, V_n\}$. The vertex $V_1$ satisfies the condition for the non-kingship of $V_3$: $V_1$ defeats $V_3$ (since $13$) and $V_1$ defeats every vertex in $N^{+}(V_3)$ (since $1$ is less than any index greater than 3).

Finally, we consider the global structure formed by the kings. Let $K$ be the set of all kings in a tournament $T$. The subtournament induced by this set, denoted $T[K]$, has remarkable properties. While a tournament can have "weaker" players who are kings and "stronger" players who are also kings, the relationship between the kings themselves is not arbitrary. A foundational result in tournament theory, sometimes called the King Set Theorem, states the following.

**Theorem (Maurer, 1980):** For any tournament $T$, the subtournament $T[K]$ induced by the set of all kings is strongly connected (unless $|K|=1$).

A tournament is **strongly connected** if for every [ordered pair](@entry_id:148349) of distinct vertices $(u, v)$, there is a directed path from $u$ to $v$. This theorem implies that within the "ruling class" of kings, every king can reach every other king via a path that uses only other kings as intermediate steps. If king $k_1$ does not directly defeat king $k_2$, the fact that $k_1$ is a king guarantees a path $k_1 \to w \to k_2$ for some vertex $w$. The deeper result is that there must exist such a path where the intermediary $w$ is also a king [@problem_id:1516485]. This ensures that the kings form a cohesive, mutually influential subgroup within the broader tournament, a non-obvious and elegant property of these fascinating graph structures.