## Introduction
In the world of competitive events, from sports leagues to academic contests, the round-robin tournament is a fundamental format ensuring every participant faces every other. At the end of such a tournament, we are left with a simple but powerful summary: the [score sequence](@entry_id:272688), a list of total wins for each competitor. But can any list of numbers represent a valid tournament outcome? This question reveals a significant challenge. Simple intuition tells us no—a player in an n-player tournament cannot win n games. While basic rules about the sum of scores and the range of individual scores can filter out some impossible sequences, they are not enough. A more rigorous framework is needed to provide a complete and certain answer.

This article provides that framework through a comprehensive exploration of Landau's Theorem on score sequences. The first chapter, "Principles and Mechanisms," lays the groundwork by defining score sequences and their basic properties, before introducing the full, elegant conditions of Landau's Theorem and its connection to tournament structure. The second chapter, "Applications and Interdisciplinary Connections," delves into the theorem's practical utility, showing how it is used to analyze tournament outcomes, characterize special competitive structures, and connect to broader mathematical concepts like optimization and [majorization](@entry_id:147350). Finally, "Hands-On Practices" offers opportunities to solidify your understanding by applying the theorem to solve specific problems. We begin by examining the core principles that govern the scores of any tournament, setting the stage for the complete characterization provided by Landau's Theorem.

## Principles and Mechanisms

In the study of tournaments, we move from the abstract concept of a directed graph to a concrete representation of competitive outcomes. A [tournament graph](@entry_id:267858) on $n$ vertices models a round-robin competition among $n$ players, where every player competes against every other player exactly once, and each game results in a distinct winner and loser. The direction of the edge $(u,v)$ signifies that player $u$ defeated player $v$. A fundamental descriptor of a tournament's outcome is its **[score sequence](@entry_id:272688)**, which is the list of scores for all players. The **score** of a player is simply their total number of wins, which corresponds to the out-degree of their vertex in the [tournament graph](@entry_id:267858).

A central question arises: given an arbitrary sequence of $n$ integers, can it represent the scores of a valid $n$-player tournament? Not every sequence is possible. For instance, in a 4-player tournament, could one player win 4 games? This is impossible, as they only play 3 games. This simple observation leads us to the core principles that govern valid score sequences.

### Fundamental Necessary Conditions

Before delving into a complete characterization, we can establish several foundational rules that any valid [score sequence](@entry_id:272688) must obey. These conditions are necessary, and their violation immediately disqualifies a sequence.

First, consider the possible range for any individual score. In a tournament with $n$ players, each player participates in $n-1$ games. The maximum possible score is therefore $n-1$, achieved by defeating every other opponent. The minimum score is 0, corresponding to losing every game. Thus, for any score $s_i$ in a [score sequence](@entry_id:272688) of an $n$-player tournament, it must satisfy the condition $0 \le s_i \le n-1$ [@problem_id:1518348]. Any sequence containing a negative number or a number greater than or equal to $n$ cannot be a [score sequence](@entry_id:272688).

Second, let us consider the total number of wins across all players. Every game played in the tournament contributes exactly one win to one player and one loss to another. Therefore, the sum of all scores, $\sum_{i=1}^{n} s_i$, must equal the total number of games played. In a round-robin tournament with $n$ players, the number of games is the number of ways to choose a pair of players from the set of $n$, which is given by the [binomial coefficient](@entry_id:156066) $\binom{n}{2}$. This leads to a crucial conservation law for scores [@problem_id:1518347]:

$$ \sum_{i=1}^{n} s_i = \binom{n}{2} = \frac{n(n-1)}{2} $$

For example, in a tournament with $N=21$ participants, the total sum of scores must be $\binom{21}{2} = \frac{21 \times 20}{2} = 210$. Any purported [score sequence](@entry_id:272688) for 21 players whose elements do not sum to 210 is invalid. It is also important to note that score sequences can contain repeated values. For instance, in a 3-player tournament where player 1 beats 2, 2 beats 3, and 3 beats 1, the [score sequence](@entry_id:272688) is $(1, 1, 1)$, which is perfectly valid [@problem_id:1518348].

These conditions—the score range and the total sum—are powerful initial filters. However, they are not sufficient to guarantee a sequence is valid. For example, in a 4-player tournament, the sum of scores must be $\binom{4}{2} = 6$. The sequence $(0, 0, 3, 3)$ has the correct sum and its scores are within the valid range $[0, 3]$, yet it is not a valid [score sequence](@entry_id:272688), a fact we will be able to prove shortly. To establish both necessity and sufficiency, we need a more profound result.

### Landau's Theorem: A Complete Characterization

The definitive test for score sequences was provided by H.G. Landau in 1953. **Landau's Theorem** gives a complete set of [necessary and sufficient conditions](@entry_id:635428) for a sequence of integers to be the [score sequence](@entry_id:272688) of a tournament.

The theorem states that a sequence of integers $S = (s_1, s_2, \ldots, s_n)$ is a valid [score sequence](@entry_id:272688) if and only if, when its elements are sorted in non-decreasing order, let's call this sorted sequence $S'=(s'_1, s'_2, \ldots, s'_n)$ where $s'_1 \le s'_2 \le \ldots \le s'_n$, the following conditions hold:

1.  For every integer $k$ from $1$ to $n-1$, the sum of the $k$ smallest scores is greater than or equal to the number of games played among those $k$ players:
    $$ \sum_{i=1}^{k} s'_i \ge \binom{k}{2} $$

2.  For $k=n$, the sum of all scores is exactly equal to the total number of games played in the tournament:
    $$ \sum_{i=1}^{n} s'_i = \binom{n}{2} $$

It is crucial to sort the sequence into **non-decreasing order** before applying these tests [@problem_id:1518372]. The theorem is formulated to check the collective strength of the weakest players. The intuition is that if even the $k$ players with the lowest scores have collectively won at least enough games to account for the matches played among themselves, then it is plausible the sequence is realizable.

Let's explore the reasoning behind the primary inequality. Consider any subset of $k$ players from the tournament. The sum of their scores, $\sum s_i$, can be broken into two parts: wins from games played *among* themselves, and wins from games played against the other $n-k$ players. Within the subset of $k$ players, exactly $\binom{k}{2}$ games are played, and each of these games results in one win for a player within that subset. Therefore, the sum of scores from these internal games is exactly $\binom{k}{2}$. The number of wins against players outside the subset is some non-negative integer. Consequently, the total sum of the scores for these $k$ players must be at least $\binom{k}{2}$ [@problem_id:1518326]. This establishes that the partial sum inequalities are a necessary condition for any [score sequence](@entry_id:272688).

The final equality condition for $k=n$ is not redundant. The partial sum inequalities alone are insufficient. For instance, consider the sequence $(1, 1, 2, 3)$ for a 4-player tournament. It is already sorted. The [partial sums](@entry_id:162077) are $1 \ge \binom{1}{2}=0$, $1+1=2 \ge \binom{2}{2}=1$, and $1+1+2=4 \ge \binom{3}{2}=3$. All inequalities are satisfied. However, the total sum is $1+1+2+3=7$, which does not equal $\binom{4}{2}=6$. This violation of the total sum rule means the sequence is not realizable, demonstrating the critical role of the equality condition for $k=n$ [@problem_id:1518321].

### Applying Landau's Theorem: Worked Examples

Let's solidify our understanding by applying the theorem to determine the validity of a few proposed sequences for a 5-player tournament, where the required sum of scores is $\binom{5}{2}=10$.

Consider the sequence $(3, 2, 1, 3, 1)$ [@problem_id:1518372].
1.  **Sort the sequence:** The non-decreasing order is $(1, 1, 2, 3, 3)$.
2.  **Check the total sum:** $1+1+2+3+3 = 10$. This equals $\binom{5}{2}$, so the final condition is met.
3.  **Check the [partial sums](@entry_id:162077):**
    *   For $k=1$: $s'_1 = 1 \ge \binom{1}{2}=0$. (True)
    *   For $k=2$: $s'_1 + s'_2 = 1+1=2 \ge \binom{2}{2}=1$. (True)
    *   For $k=3$: $s'_1 + s'_2 + s'_3 = 1+1+2=4 \ge \binom{3}{2}=3$. (True)
    *   For $k=4$: $s'_1 + s'_2 + s'_3 + s'_4 = 1+1+2+3=7 \ge \binom{4}{2}=6$. (True)

Since all conditions of Landau's Theorem are satisfied, the sequence $(1, 1, 2, 3, 3)$ is a valid [score sequence](@entry_id:272688) for a 5-player tournament.

Now, consider the sequence $(4, 1, 0, 4, 1)$.
1.  **Sort the sequence:** $(0, 1, 1, 4, 4)$.
2.  **Check the total sum:** $0+1+1+4+4 = 10 = \binom{5}{2}$. The condition for $k=5$ holds.
3.  **Check the [partial sums](@entry_id:162077):**
    *   For $k=1$: $0 \ge \binom{1}{2}=0$. (True)
    *   For $k=2$: $0+1=1 \ge \binom{2}{2}=1$. (True)
    *   For $k=3$: $0+1+1=2 \ge \binom{3}{2}=3$. (False)
The condition fails for $k=3$. Therefore, $(0, 1, 1, 4, 4)$ is not a valid [score sequence](@entry_id:272688). This reveals a structural impossibility: the three players with the fewest wins do not have enough wins between them to even account for the games they must have played against each other.

A common pitfall is to assume that a subsequence of scores from a valid tournament must itself be a valid [score sequence](@entry_id:272688) for a smaller tournament. This is generally false. Consider a 7-team tournament with the valid [score sequence](@entry_id:272688) $(2, 2, 2, 3, 4, 4, 4)$. An analyst might select four teams with scores $(2, 2, 2, 3)$ and ask if this is a valid [score sequence](@entry_id:272688) for a 4-team tournament. Applying Landau's Theorem, the sum is $2+2+2+3=9$. For a 4-team tournament, the sum must be $\binom{4}{2}=6$. Since $9 \ne 6$, the sequence is not valid for a self-contained 4-team tournament [@problem_id:1518318]. The error lies in forgetting that the original scores of '2' and '3' included wins against the other three teams not included in the subsequence.

### Score Sequences and Tournament Structure

Landau's Theorem does more than just validate sequences; it provides deep insights into the structure of the corresponding tournaments. The nature of the inequalities—whether they are strict or hold with equality—reveals properties like [transitivity](@entry_id:141148) and competitiveness.

A tournament is **transitive** if the "beats" relation is transitive: if $i$ beats $j$ and $j$ beats $k$, then $i$ beats $k$. This implies a complete and unambiguous ranking of all players. There is a "best" player who beats everyone, a second-best who beats everyone but the best, and so on, down to a "worst" player who loses to everyone. The scores of such a tournament on $n$ players will be $n-1, n-2, \ldots, 1, 0$. The unique non-decreasing [score sequence](@entry_id:272688) for a [transitive tournament](@entry_id:267486) is therefore $(0, 1, 2, \ldots, n-1)$ [@problem_id:1518343]. For this sequence, a remarkable thing happens: the partial sum condition holds with equality for *every* value of $k$:
$$ \sum_{i=1}^{k} (i-1) = \frac{(k-1)k}{2} = \binom{k}{2} $$
This indicates that for the $k$ weakest players, all of their wins came from playing against each other; none of them defeated any of the top $n-k$ players.

This observation can be generalized. A tournament is called **decomposable** (or not strongly connected) if its set of players $V$ can be partitioned into two non-empty subsets, $S$ and $T$, such that every player in $T$ beats every player in $S$. No player in $S$ wins a game against any player in $T$. This describes a clean structural division in the tournament. Such a set $S$ is sometimes called a "Sovereign Bloc" whose influence is entirely internal [@problem_id:1550244]. This structural property has a precise algebraic signature in the [score sequence](@entry_id:272688): a tournament is decomposable if and only if there exists a proper non-empty subset of its players, $S$, whose scores (when summed) exactly equal the number of games played within that subset. That is, for a sorted [score sequence](@entry_id:272688), equality holds in Landau's condition for some $k  n$:
$$ \sum_{i=1}^{k} s'_i = \binom{k}{2} $$

A tournament that is not decomposable is called **strong** or **non-decomposable**. In such a tournament, for every partition of players into two sets $S$ and $T$, there is at least one player in $S$ who beats a player in $T$. These are considered more "competitive" as no subset of players is universally dominated by another. A [score sequence](@entry_id:272688) corresponds to a strong tournament if and only if all of Landau's inequalities are strict for $k=1, \ldots, n-1$.

For example, with $n=5$, the transitive sequence $(0, 1, 2, 3, 4)$ is decomposable, as equality holds for all $k$. In contrast, the sequence $(1, 1, 2, 3, 3)$ has strict inequalities for all $k5$ and thus can only be realized by a strong, non-decomposable tournament [@problem_id:1518358]. This demonstrates how the arithmetic of score sequences is intimately linked to the graph-theoretic topology of competition.

Finally, it is worth noting the distinction between a tournament [score sequence](@entry_id:272688) and the more general concept of a [degree sequence](@entry_id:267850) of a [simple graph](@entry_id:275276) [@problem_id:1518354]. A [score sequence](@entry_id:272688) is the out-degree sequence of a tournament—a complete directed graph. A [degree sequence](@entry_id:267850) for a simple (undirected) graph is governed by different rules, such as the Erdős–Gallai theorem. For example, for $n=5$, the sequence $(0, 1, 2, 3, 4)$ is a valid [score sequence](@entry_id:272688) (of a [transitive tournament](@entry_id:267486)), but it cannot be the [degree sequence](@entry_id:267850) of a [simple graph](@entry_id:275276) on 5 vertices. A vertex with degree 4 must be connected to all other four vertices, making it impossible for another vertex to have degree 0. The constraints on tournaments are much tighter, and Landau's Theorem provides the precise tool for their analysis.