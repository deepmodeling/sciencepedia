## Introduction
In the complex world of strategic interactions, from corporate competition to international relations, how can we predict the choices of rational individuals? The fundamental assumption of [game theory](@entry_id:140730) is that decision-makers act in their own best interest, but untangling the web of interdependent choices can be daunting. The core problem lies in simplifying this complexity to reveal a set of logical, defensible outcomes. Iterated Elimination of Dominated Strategies (IEDS) provides a powerful and intuitive method to do just that, by formalizing a simple idea: a rational player will never choose an option that is demonstrably inferior.

This article provides a comprehensive exploration of this foundational solution concept. Across three chapters, you will learn to master both the theory and application of IEDS. First, in "Principles and Mechanisms," we will dissect the core concepts of strategic dominance, explore the iterative elimination process, and uncover its deep connection to the idea of [common knowledge of rationality](@entry_id:139372). Next, "Applications and Interdisciplinary Connections" will showcase the remarkable versatility of IEDS, demonstrating how it provides critical insights into problems in economics, political science, and even biology. Finally, "Hands-On Practices" will offer you the chance to apply these principles to solve concrete problems, solidifying your understanding and building your analytical toolkit. We begin by laying the theoretical groundwork, defining what makes a strategy truly inferior and how this simple observation becomes a powerful tool for prediction.

## Principles and Mechanisms

In the study of strategic interactions, our primary goal is to predict the behavior of rational decision-makers. The most [fundamental solution](@entry_id:175916) concept, and the starting point for our analysis, is built on a simple yet powerful idea: a rational player will never choose an option that is unambiguously inferior to another available option. This chapter delves into the principles of strategic dominance and the mechanism through which this simple idea, when applied iteratively, becomes a potent tool for solving and simplifying complex games: the Iterated Elimination of Dominated Strategies (IEDS).

### The Foundation: Strategic Dominance

At its core, a strategic game involves players choosing actions, with outcomes determined by the profile of actions chosen by all. A player's choice is guided by their payoffs, which represent their preferences over these outcomes. The concept of dominance formalizes the idea of one strategy being "better" than another, regardless of what other players do.

A strategy is **strictly dominated** for a player if there exists another strategy that yields a strictly higher payoff for every possible combination of the opponents' strategies. Let $S_i$ be the set of strategies for player $i$, and $s_{-i}$ be a profile of strategies for all players except $i$. A strategy $s_i' \in S_i$ strictly dominates another strategy $s_i'' \in S_i$ if for every $s_{-i}$, the utility $u_i(s_i', s_{-i}) > u_i(s_i'', s_{-i})$. A rational player would never play a strictly [dominated strategy](@entry_id:139138) because there is an alternative that performs better no matter the circumstances.

A related but distinct concept is that of **[weak dominance](@entry_id:138271)**. A strategy $s_i'$ weakly dominates $s_i''$ if $u_i(s_i', s_{-i}) \ge u_i(s_i'', s_{-i})$ for all $s_{-i}$, and there is at least one $s_{-i}$ for which $u_i(s_i', s_{-i}) > u_i(s_i'', s_{-i})$. While it may seem reasonable to eliminate weakly dominated strategies, this procedure suffers from a critical flaw: the final outcome can depend on the order in which strategies are eliminated.

Consider a game between two firms with the following payoff bimatrix :
$$
\begin{array}{c|ccc}
   & X & Y & Z \\
\hline
A & (5,6) & (1,6) & (4,4)\\
B & (3,5) & (2,1) & (3,4)\\
C & (5,3) & (3,2) & (3,3)
\end{array}
$$
Let's see what happens if we eliminate weakly dominated strategies in two different orders.

- **Order I (Columns First):** The column player notes that strategy $X$ weakly dominates $Y$ (payoffs $(6,5,3)$ for $X$ versus $(6,1,2)$ for $Y$). Eliminating $Y$ reduces the game. In the new $3 \times 2$ game, the row player sees that strategy $C$ weakly dominates $B$. Eliminating $B$ gives a $2 \times 2$ game where row strategy $A$ weakly dominates $C$. After eliminating $C$, the column player chooses $X$ over $Z$ (payoff 6 vs 4). The final outcome is $(A,X)$ with payoffs $(5,6)$.

- **Order II (Rows First):** In the original game, the row player notes that strategy $C$ weakly dominates $B$ (payoffs $(5,3,3)$ for $C$ versus $(3,2,3)$ for $B$). Eliminating $B$ reduces the game. In this new $2 \times 3$ game, the column player sees that $X$ weakly dominates $Z$. After eliminating $Z$, the game is a $2 \times 2$ matrix where row player strategy $C$ now weakly dominates $A$. Eliminating $A$ leaves the column player to choose $X$ over $Y$ (payoff 3 vs 2). The final outcome is $(C,X)$ with payoffs $(5,3)$.

The choice of elimination order leads to different predictions ($(A,X)$ versus $(C,X)$) and significantly different payoffs for the column player ($6$ versus $3$). This ambiguity makes [weak dominance](@entry_id:138271) a less reliable tool for prediction. In contrast, the set of strategies surviving the iterated elimination of *strictly* dominated strategies is always independent of the elimination order. For this reason, our focus will be squarely on the robust and unambiguous implications of [strict dominance](@entry_id:137193).

### The Power of Iteration: Common Knowledge of Rationality

The true power of dominance emerges when we consider its interactive nature. A rational player will not play a [dominated strategy](@entry_id:139138). But a rational player can also assume that *other* players are rational and will likewise avoid their own dominated strategies. This chain of reasoning—"I know you are rational, and you know that I know you are rational, and so on"—is known as **[common knowledge of rationality](@entry_id:139372)**. The **Iterated Elimination of Strictly Dominated Strategies (IESDS)** is the algorithmic procedure that captures this powerful idea.

The process is straightforward:
1. Identify and eliminate all strictly dominated strategies for all players from the original game.
2. In the resulting, smaller game, again identify and eliminate all strictly dominated strategies for all players.
3. Repeat this process until no more strategies can be eliminated.

The strategies that remain are said to survive IEDS. If this process leads to a single, unique strategy profile, the game is called **dominance solvable**. Let's examine a game that is dominance solvable :
$$
\begin{pmatrix}
(6,6) & (5,1) & (2,0) \\
(4,4) & (3,2) & (1,1) \\
(3,3) & (2,1) & (0,0)
\end{pmatrix}
$$
In the first round, the row player compares their strategies. Strategy $R_1$ strictly dominates $R_2$ ($6>4$, $5>3$, $2>1$), and $R_2$ strictly dominates $R_3$ ($4>3$, $3>2$, $1>0$). A rational row player will therefore never play $R_2$ or $R_3$. The column player, knowing the row player is rational, anticipates that the game will effectively be restricted to the first row. In this reduced game, the column player's payoffs for strategies $C_1, C_2, C_3$ are $6, 1, 0$. Clearly, $C_1$ now strictly dominates $C_2$ and $C_3$. Thus, the only surviving outcome is $(R_1, C_1)$.

The iterative aspect is crucial. A strategy might not be dominated in the original game, but can become dominated once a player assumes their opponents are rational. Consider a three-player game where Player 1's strategy $A_1$ is not dominated at the outset. However, Player 2 has a strategy, $B_1$, that is strictly dominated by their alternative, $B_2$. Player 1, assuming Player 2 is rational, can confidently predict that Player 2 will never play $B_1$. Player 1 can then re-evaluate their own choices in a world where $B_1$ is off the table. In this new conceptual game, it may turn out that $A_1$ is now strictly dominated by another of Player 1's strategies, $A_2$ . This demonstrates how beliefs about others' rationality can recursively refine a player's own set of rational choices.

### Expanding the Toolkit: Dominance by Mixed Strategies

Is it possible for a strategy to be inherently poor, yet not be strictly dominated by any *single* alternative pure strategy? The answer is yes, and this leads to a crucial extension of our toolkit. A player can randomize their choice by using a **[mixed strategy](@entry_id:145261)**, which is a probability distribution over their pure strategies.

A pure strategy $s_i''$ is **strictly dominated by a [mixed strategy](@entry_id:145261)** $\sigma_i$ if the [expected utility](@entry_id:147484) from playing $\sigma_i$ is strictly greater than the utility of playing $s_i''$, for every possible combination of opponents' strategies.

This concept is best illustrated with an example . Consider the following [payoff matrix](@entry_id:138771) for the row player:
$$
A^{(1)} = \begin{pmatrix}
1 & 0 \\
0 & 1 \\
0.4 & 0.4
\end{pmatrix}
$$
Let the row player's pure strategies be $S_0, S_1, S_2$.
- Is $S_2$ strictly dominated by $S_0$? No, because if the column player chooses the second column, $S_2$ yields $0.4$ while $S_0$ yields $0$.
- Is $S_2$ strictly dominated by $S_1$? No, because if the column player chooses the first column, $S_2$ yields $0.4$ while $S_1$ yields $0$.

Thus, $S_2$ is not strictly dominated by any *pure* strategy. However, consider a [mixed strategy](@entry_id:145261) $\sigma$ that plays $S_0$ with probability $0.5$ and $S_1$ with probability $0.5$. The expected payoff vector from this mix is:
$0.5 \times (1, 0) + 0.5 \times (0, 1) = (0.5, 0.5)$.
Since $0.5 > 0.4$, this [mixed strategy](@entry_id:145261) yields a strictly higher payoff than $S_2$ regardless of what the column player does. Therefore, strategy $S_2$ is strictly dominated by a [mixed strategy](@entry_id:145261). A rational player would never play $S_2$.

### The Theoretical Pinnacle: Rationalizability

The iterated elimination of strategies strictly dominated by [mixed strategies](@entry_id:276852) leads us to a profound and central concept in game theory: **[rationalizability](@entry_id:143607)**. A strategy is rationalizable if it can be justified as a [best response](@entry_id:272739) to some belief about the opponents' strategies, with the constraint that those beliefs must themselves be over rationalizable strategies. This concept is the formal expression of [common knowledge of rationality](@entry_id:139372).

A fundamental theorem in epistemic [game theory](@entry_id:140730) establishes a precise equivalence  : for any finite game, the set of rationalizable strategies is identical to the set of strategies that survive the iterated elimination of strictly dominated strategies, where domination by [mixed strategies](@entry_id:276852) is permitted. In other words, IEDS is not just a convenient algorithm; it is the operational counterpart to the logical implications of [common knowledge of rationality](@entry_id:139372).

A classic and powerful demonstration of [rationalizability](@entry_id:143607) is the "Guess 2/3 of the Average" game . In this game, $n$ players each choose a number $a_i$ in the interval $[0,100]$. The winner is the player whose guess is closest to $\frac{2}{3}$ of the average of all guesses. What is the rational strategy?
Let's apply iterative reasoning:

- **Round 1:** A player might initially think any number is possible. But, could a rational player guess, say, 70? The highest possible average is 100 (if everyone guesses 100). So, the target number, $\frac{2}{3}\bar{a}$, cannot exceed $\frac{2}{3} \times 100 \approx 66.67$. Any guess above $66.67$ is strictly dominated by guessing $66.67$. So, a rational player will only choose a number in $[0, 66.67]$.

- **Round 2:** Every player knows that every other rational player will only choose a number in $[0, 66.67]$. Now, the highest possible average is $66.67$. The target number cannot exceed $\frac{2}{3} \times 66.67 \approx 44.44$. Any guess above $44.44$ is now seen to be dominated. The set of rationalizable strategies shrinks to $[0, 44.44]$.

- **Iteration:** This process continues. At each step, the upper bound of the rationalizable strategy set is multiplied by $\frac{2}{3}$. As this iteration proceeds infinitely, the interval of rationalizable strategies collapses to a single point: $\{0\}$. The unique rationalizable strategy for every player is to guess $0$.

### Applications and Advanced Contexts

The principles of IEDS are not confined to abstract examples; they provide critical insights across various domains of economics and finance. The key is to remember that dominance applies to players' **utilities**, not necessarily to their monetary profits.

A practical application can be found in a duopoly model where two firms first choose a technology ("Innovate" or "Imitate") and then compete on quantity . While the full analysis involves calculating Cournot equilibrium outcomes for each technology pairing, this analysis ultimately serves to construct a $2 \times 2$ [payoff matrix](@entry_id:138771) for the initial strategic choice. In a well-constructed scenario, applying IEDS to this matrix might reveal that one strategy (e.g., "Innovate") strictly dominates the other for both firms, leading to a clear prediction of the industry's technology path, $(I,I)$.

The distinction between utility and profit is crucial when incorporating more realistic models of human behavior.
- **Social Preferences:** Suppose a player's utility includes a concern for their opponent's payoff, such as $U_1 = \pi_1 + \alpha \pi_2$ . If $\alpha > 0$, the player is altruistic; if $\alpha  0$, the player is spiteful. The [dominance relationships](@entry_id:156670) in the game, and thus the IEDS outcome, can hinge critically on the value of $\alpha$. A strategy might be dominated for a purely selfish player ($\alpha=0$) but become rationalizable for an altruistic one, or vice-versa for a spiteful player. Analysis shows how the predicted outcome can change as $\alpha$ crosses a specific threshold, say $\alpha^\star = \frac{1}{3}$, fundamentally altering a player's rational choice.

- **Risk Aversion:** When [mixed strategies](@entry_id:276852) are involved, a player is choosing between a certain outcome (from a pure strategy) and a lottery (from a [mixed strategy](@entry_id:145261)). A player's attitude toward risk will determine their evaluation of this lottery. Consider a player with a [utility function](@entry_id:137807) $U(\pi) = 1 - \exp(-k\pi)$, where $k$ measures [risk aversion](@entry_id:137406) . For a risk-neutral player ($k=0$), a pure strategy $C$ might be strictly dominated by a mix of $A$ and $B$. However, as [risk aversion](@entry_id:137406) $k$ increases, the utility of the risky lottery offered by the [mixed strategy](@entry_id:145261) decreases. There may exist a critical threshold $k^\star$ such that for all $k > k^\star$, the player is so risk-averse that the lottery is no longer preferable to the safe option, and the dominance relationship disappears. This is a vital consideration in finance, where correctly modeling risk preferences is paramount.

### Scope and Limitations: A Bridge to Nash Equilibrium

While IEDS is a powerful tool, it does not solve every game. Its predictive power depends entirely on the existence of dominated strategies. In many important games, no such strategies exist.

A classic example is "Matching Pennies" , with the [payoff matrix](@entry_id:138771):
$$
\begin{pmatrix}
(1,-1)  (-1,1) \\
(-1,1)  (1,-1)
\end{pmatrix}
$$
Here, neither player has a [dominated strategy](@entry_id:139138). If the row player plays Heads, the column player wants to play Tails. If the row player plays Tails, the column player wants to play Heads. The best action for each player is always dependent on the other's choice, and no strategy is universally better or worse than another. Applying IEDS to this game eliminates nothing. The set of rationalizable strategies is the full set of initial strategies.

The inability of IEDS to make a sharp prediction in such games highlights its limitation. It provides a set of strategies consistent with [common knowledge of rationality](@entry_id:139372), but this set can sometimes be large. To refine our predictions further, we need a solution concept that imposes more structure on players' beliefs. This motivates the concept of **Nash Equilibrium**, where each player's strategy must be a [best response](@entry_id:272739) to the *actual* strategies being played by their opponents. Rationalizability requires a strategy to be justifiable by *some* belief; Nash equilibrium requires it to be justified by the *correct* belief. This next level of analysis will be the subject of the following chapter.