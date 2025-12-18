## Introduction
In any strategic interaction, from a business negotiation to a simple board game, the central challenge is anticipating the actions of others. While finding the single "best" move can be impossibly complex, game theory offers a more fundamental starting point: identifying what a rational player would *never* do. This article explores the powerful concept of rationalizability, which addresses the gap between simple intuition and formal strategic prediction. It provides a formal logic for deducing the entire set of sensible outcomes based on the minimal assumption that players will not choose obviously inferior options. In the following chapters, we will first delve into the "Principles and Mechanisms," exploring how the iterative elimination of dominated strategies works and defining its relationship to core [game theory](@article_id:140236) concepts. We will then witness this theory in action in the "Applications and Interdisciplinary Connections" chapter, revealing its surprising power to explain phenomena in economics, social policy, and even evolutionary biology.

## Principles and Mechanisms

Imagine you are playing a game—perhaps a business negotiation, a financial market trade, or even just deciding which route to take in traffic. How do you make a choice? A powerful starting point, championed by [game theory](@article_id:140236), is to first figure out what you *shouldn't* do. The principle of rationalizability is a beautiful, cascading logic that flows from this simple idea. It’s not just about finding the "best" move, but about understanding the entire landscape of sensible actions.

### The Art of Not Playing a Stupid Move

Let's begin with a cornerstone of rational decision-making: you should never, ever choose an action that is **strictly dominated**. What does this mean? A strategy is strictly dominated if there's another strategy available to you that gives you a better payoff, no matter what your opponents do. It's like having two buttons to press, where pressing the first button *always* gives you more money than pressing the second, regardless of any other circumstance. A rational person would simply never press the second button.

Consider a practical scenario faced by two competing firms . They have to decide whether to "Innovate" by spending money on R&D to lower their production costs, or to "Imitate" and stick with their current, higher costs. After making this choice, they compete on the market. Once we do the math, we might find a situation where innovating always yields a higher profit than imitating, whether the competitor chooses to innovate or imitate. For instance, the extra profit from having a lower cost might always outweigh the initial R&D expense. In this situation, "Imitate" is a strictly [dominated strategy](@article_id:138644).

For a rational firm, the choice is clear: eliminate "Imitate" from the list of possible actions. It's a "stupid" move. If both firms are rational, they both eliminate this option, and suddenly, the outcome of the game becomes certain: both will choose to "Innovate". The complex strategic landscape collapses to a single, predictable point, all by applying this one simple rule.

### The Unraveling: Thinking About What They're Thinking

This is where things get truly interesting. The process doesn’t stop after a single step. This is the world of **iterated elimination of strictly dominated strategies (IESDS)**. The logic is as follows: if I am rational, I won’t play my dominated strategies. If you are rational, you won't play yours. But if I know you are rational, I can also assume you won't play your dominated strategies. That new knowledge—that a whole set of your potential actions are now off the table—might make some of *my* strategies, which looked sensible before, suddenly look stupid.

This iterative reasoning is what economists call **[common knowledge of rationality](@article_id:138878)**: I am rational, I know that you are rational, I know that you know that I am rational, and so on, ad infinitum.

The classic "Guess 2/3 of the Average" game is the quintessential example of this unraveling . Imagine a large group of people, each asked to pick a number between 0 and 100. The winner is the person whose guess is closest to $\frac{2}{3}$ of the average of all guesses. What number should you choose?

A first-level thinker might reason: "The numbers are between 0 and 100, so the average could be around 50. Two-thirds of 50 is about 33." But a second-level thinker would say, "Wait. If everyone is a first-level thinker, they'll all pick around 33. The average will be 33, and $\frac{2}{3}$ of that is 22."

A third-level thinker anticipates this: "If everyone is a second-level thinker, they'll all choose 22. The average will be 22, and $\frac{2}{3}$ of that is about 15."

Do you see the pattern? Each level of thinking makes the highest possible rational guess smaller. In the first round of elimination, any guess above $\frac{2}{3} \times 100 \approx 66.67$ is strictly dominated, because it's impossible for such a high number to be $\frac{2}{3}$ of the average. But once everyone knows this, no one will guess above 66.67. So in the second round, the maximum possible average is 66.67, and any guess above $\frac{2}{3} \times 66.67 \approx 44.44$ is now dominated. This process continues, with the upper bound of rational guesses shrinking relentlessly, until it converges to the only number that can survive infinite levels of this logic: **zero**. This is the stunning power of iterating a very simple rule.

Of course, the real world is rarely populated by infinitely rational logicians. We can model this using the concept of **[bounded rationality](@article_id:138535)** . What if you, a fully rational player, are playing against someone you know will only perform, say, two rounds of this elimination? You would perform the two rounds of elimination with them, see what strategies they are left with, and then choose your [best response](@article_id:272245) assuming they will pick one of those remaining options. Your sophistication gives you an edge by allowing you to precisely predict the cognitive limits of your opponent.

### A Deeper Look: The Power of the Portfolio

So far, we've only considered a strategy being dominated by another *single* strategy. But the concept is even more powerful. Sometimes, a strategy isn't worse than any one alternative, but it's worse than a *portfolio* or a **[mixed strategy](@article_id:144767)**.

Imagine you have three investment options: A, B, and C. In a rising market, A does best. In a falling market, B does best. C is mediocre in both. So, neither A nor B strictly dominates C. But what if you could put half your money in A and half in B? It might be that this 50/50 portfolio approach gives you a better return than C *both* in a rising market and a falling market. In this case, your pure strategy C is strictly dominated by a [mixed strategy](@article_id:144767). A rational player would never choose C.

This insight is the final key to unlocking the formal definition of rationalizability. A strategy is called **rationalizable** if it can be justified as a [best response](@article_id:272245) to some rational belief about what your opponents might do. And what are those rational beliefs? They are beliefs that place weight only on the opponents' own rationalizable strategies. This may sound circular, but it's the same iterative logic we saw before.

The fundamental theorem here is a thing of beauty: **the set of strategies that survive the iterated elimination of strictly dominated strategies (where domination by [mixed strategies](@article_id:276358) is allowed) is precisely the set of rationalizable strategies**  . The mechanical process of IESDS and the epistemic concept of [common knowledge of rationality](@article_id:138878) are two sides of the same coin.

### Rationality in Action: From Static Games to Dynamic Strategies

This potent idea isn't confined to simple, one-shot decisions. It is a fundamental tool for navigating complex, multi-stage interactions. Consider a business scenario that unfolds over time: Player 1 makes a move, then Player 2 observes it and makes a move, which might lead to a final, simultaneous negotiation between Players 2 and 3 .

How does Player 1 decide what to do at the very beginning? By thinking ahead. They look at the final stage negotiation and ask, "What strategies will rational players eliminate there?" By applying IESDS to that final subgame, Player 1 can predict its likely outcome. This predicted outcome determines the value of reaching that point in the game tree. Working backward, Player 1 can then determine the value of their initial choice, having filtered out the "stupid" plays that would never happen at the end. IESDS, applied within a framework of [backward induction](@article_id:137373), allows players to prune the sprawling tree of future possibilities down to a manageable and predictable path.

### The Human Element: What Are We Rationalizing?

It’s tempting to think of "rationality" as cold, calculating, and purely selfish profit-maximization. But the framework is far more flexible and human. "Rationality" simply means you are acting consistently to maximize your **utility**—and your utility can include anything you care about.

Let's revisit the duopoly of firms setting prices, but this time, suppose one firm's owner isn't just a profit-maximizer. Their utility might be a combination of their own profit and the other firm's profit, weighted by a factor, $\alpha$ .
$$ U_1 = \pi_1 + \alpha \pi_2 $$
If $\alpha$ is positive, the player is **altruistic**; they get some satisfaction from the other player's success. If $\alpha$ is negative, they are **spiteful**; they enjoy seeing their competitor do poorly.

How does this change what is a "dominated" strategy? A strategy that might seem foolish for a purely selfish player (like setting a price that helps the competitor) could be perfectly rational for an altruist. Conversely, a spiteful player might rationally choose a strategy that hurts themselves, as long as it hurts their rival more. The principles of IESDS and rationalizability work just the same; we just need to correctly define the utility that each player is trying to maximize.

### Rationalizability and the Landscape of Prediction

Finally, it's useful to place rationalizability in context. How does it relate to the most famous concept in [game theory](@article_id:140236), the **Nash Equilibrium**? A Nash Equilibrium is a profile of strategies where each player's choice is a [best response](@article_id:272245) to the others' choices. It's a point of stability, where no one has a unilateral incentive to deviate.

Every Nash equilibrium is, by definition, rationalizable. But the reverse is not always true. Consider the simple game of "Matching Pennies," where one player wins if their choices match (e.g., Heads-Heads) and the other wins if they don't  . In this game, no strategy is strictly dominated. IESDS eliminates nothing. All strategies are rationalizable. However, there is no Nash equilibrium in pure strategies—in any outcome, one player always wishes they had chosen differently.

This tells us that rationalizability is a more permissive, or weaker, solution concept than Nash Equilibrium. It doesn't try to pinpoint a single stable outcome. Instead, it tells us the set of *all possible outcomes* that could emerge under the minimal assumption of [common knowledge of rationality](@article_id:138878). It provides the boundaries of strategic reason, and within those boundaries, other forces—convention, communication, or chance—may lead to a specific equilibrium. It is the first and most fundamental step in understanding the logic of strategic interaction.