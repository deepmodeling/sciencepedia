## Introduction
When we reason about the world, we rarely start from scratch. Our existing knowledge and intuition instinctively guide our judgments, narrowing the field of possibilities long before we see new evidence. In Bayesian statistics, this foundational knowledge is formally captured in a **prior distribution**, and the rigorous process of creating it is known as **prior elicitation**. This practice addresses a fundamental challenge in [scientific modeling](@entry_id:171987): how to make our initial assumptions transparent, justifiable, and testable, rather than hidden or arbitrary. This article provides a comprehensive overview of this crucial process. First, in the **Principles and Mechanisms** chapter, we will delve into the core concepts, exploring how to distinguish between different types of uncertainty and translate expert opinion into mathematical language. Subsequently, the **Applications and Interdisciplinary Connections** chapter will demonstrate how these methods are applied to solve critical problems in fields ranging from medicine and engineering to ecology and economics, revealing the profound impact of structured belief on scientific discovery.

## Principles and Mechanisms

Before we conduct an experiment, we are not blank slates. If I were to ask you to guess the temperature of the room you're in, you wouldn't start by considering absolute zero or the surface of the sun. Your mind would instantly narrow the possibilities to a plausible range, say between $15^{\circ}\text{C}$ and $25^{\circ}\text{C}$. This intuitive act of using background knowledge to frame a question is the very heart of what we do, more formally, in Bayesian statistics. The mathematical expression of this "plausible range" is called a **prior distribution**, and the art and science of crafting it is known as **prior elicitation**.

Prior elicitation is the structured process of translating human knowledge—from expert opinion, historical data, or physical principles—into the language of probability [@problem_id:4442689]. It’s a crucial first step in any Bayesian analysis, a way of "telling the model what we know" before it sees the new data. This isn't about fabricating beliefs; it's about making our starting assumptions transparent, quantifiable, and open to scrutiny. To do this, we must first appreciate what kind of uncertainty we are trying to capture.

### The Two Faces of Uncertainty

In science, we grapple with two fundamental types of uncertainty [@problem_id:3807473]. The first is **[aleatoric uncertainty](@entry_id:634772)**, from the Latin *alea* for "dice". This is the inherent randomness in a system, the variability that would persist even if we knew everything about its underlying parameters. Think of the roll of a fair die; even knowing it's fair doesn't tell you the outcome of the next roll. This is irreducible chance.

The second type is **[epistemic uncertainty](@entry_id:149866)**, from the Greek *episteme* for "knowledge". This is uncertainty due to our own lack of knowledge about a fixed, true quantity. What is the precise mass of the planet Jupiter? It has a single, true value, but our measurement is uncertain. The true long-term success rate of a new surgical procedure is a fixed number, but we don't know it. Epistemic uncertainty can, in principle, be reduced by gathering more data.

Prior distributions are the tool we use to represent our epistemic uncertainty. When we elicit a prior for the success rate of that surgery, we are not saying the rate itself is random. We are making a precise statement about the limits of our own knowledge *about* that rate.

### From Words to Numbers: The Mechanics of Elicitation

So, how do we have this conversation with an expert and translate their knowledge into a mathematical formula? We can't just ask a clinician, "What are the parameters $\alpha$ and $\beta$ of your Beta prior for the patient response rate?" The question would be meaningless. Instead, we must ask questions in a language they understand.

A powerful and common technique is the **quantile method**. We ask for a range of plausible values. For instance, we might ask a team of engineers designing a new material [@problem_id:3807473]: "Give us a value for the material's tensile strength that you are 97.5% sure the true value is below," and "Give us a value you are 2.5% sure the true value is below." These two numbers define a central 95% [credible interval](@entry_id:175131) for their belief.

Let's imagine the experts tell us this interval is $[2, 8]$ gigapascals for a parameter $\theta$ [@problem_id:4853304]. If we decide to model our belief with a bell-shaped Normal distribution, $\theta \sim \mathcal{N}(\mu, \sigma^2)$, we have just been given two powerful clues. A symmetric 95% interval for a Normal distribution is given by the mean plus or minus about 1.96 standard deviations. So we can write a simple system of equations:

$$
\begin{align*}
\mu - 1.96\sigma  = 2 \\
\mu + 1.96\sigma  = 8
\end{align*}
$$

Solving this is straightforward: adding the two equations gives $2\mu = 10$, so the mean of our prior, $\mu$, is $5$. Subtracting the first from the second gives $2 \times 1.96\sigma = 6$, which means our prior standard deviation, $\sigma$, is approximately $1.53$. We have successfully translated a qualitative statement ("it's probably between 2 and 8") into a precise mathematical object: $\theta \sim \mathcal{N}(5, 1.53^2)$.

Of course, the world isn't always so straightforward. What if the parameter is a probability, which must lie between 0 and 1? A Normal distribution, with its infinite tails, is no longer appropriate. Here, we can be clever. We might ask an expert for their 95% interval on a mortality probability, say $[0.1, 0.3]$ [@problem_id:4853304]. We can then transform these probabilities to a scale that *does* stretch to infinity: the **[log-odds](@entry_id:141427)** or **logit scale**, where $\text{logit}(p) = \ln(p/(1-p))$. On this new scale, we can fit our Normal prior. This ensures our prior respects the fundamental constraints of the parameter. After the analysis, we can transform back to the probability scale to see what our model implies. This "sanity check"—of translating the implications of a prior back into a readily interpretable scale—is a critical part of the process [@problem_id:4912542]. Different problems call for different families of distributions, like the **Beta distribution** for probabilities or the **Gamma distribution** for rates, each with properties suited to the parameter in question [@problem_id:4780741] [@problem_id:4530915].

### The Wisdom (and Madness) of Crowds

Often, we don't consult just one expert; we consult a team. But combining judgments is fraught with peril. Unstructured group discussions are a well-known recipe for cognitive biases. The first opinion stated can create an **anchoring bias**; the most senior person's opinion can be over-weighted due to **authority bias**; and a desire for harmony can lead to **groupthink**, where dissenting opinions are suppressed [@problem_id:4370766].

To navigate this minefield, structured protocols are essential. One of the most effective is a version of the **Delphi method**. In this process:

1.  Experts provide their initial ratings and rationales anonymously and independently.
2.  A facilitator collates these judgments, calculates a summary (like the median and the range of opinions), and shares it back with the group, along with the anonymized rationales.
3.  Experts then review the group's thinking and are given a chance to revise their own estimates.

This iterative, anonymous feedback loop allows the group to benefit from shared information and diverse perspectives without the distorting effects of social pressure [@problem_id:4370766].

Once we have refined individual judgments, we can combine them mathematically. A common approach is a **linear opinion pool**, which is essentially a weighted average of the individual expert's prior distributions [@problem_id:4530915]. The weights can be equal, or, in more sophisticated setups, they can be performance-based. We can **calibrate** our experts by first asking them to provide intervals for "seed questions" whose answers are known (e.g., "What is the population of Brazil?"). Experts whose 95% intervals contain the true value about 95% of the time are considered well-calibrated and can be given more weight [@problem_id:4530915].

For situations with deep, fundamental disagreements, advanced nonparametric methods like **Dirichlet Process Mixtures** can even create a pooled prior that is multimodal—having multiple peaks—thereby faithfully representing distinct schools of thought without forcing an artificial consensus [@problem_id:4215240].

### The Moment of Truth: When Priors Meet Data

A prior is not dogma. It is a hypothesis, and like any scientific hypothesis, it must be held accountable to evidence. What happens when the data we collect seem to tell a very different story from our prior? Suppose our experts believe a new therapy will have only a modest effect, but the initial trial results show a surprisingly large benefit. This is a **prior-data conflict**, and it is one of the most important diagnostic signals in a Bayesian analysis [@problem_id:4442689].

We can formally test for this using a **prior predictive check**. The logic is simple: "If our prior beliefs were an accurate representation of the world, what kind of data would we expect to see?" Using our model, we can simulate thousands of hypothetical datasets based on the prior alone. We then look at our *actual*, observed data and see where it falls within this simulated landscape. If our real data is an extreme outlier—something that would happen less than 1% of the time if our prior was correct—then we have a significant conflict [@problem_id:3807473] [@problem_id:4442689].

The response to such a conflict is never to discard the data. The data are the data. The correct response is to investigate. Was the prior too strong or misguided? Or perhaps the model itself is wrong? A prior-data conflict is a discovery. The responsible path is to conduct a **[sensitivity analysis](@entry_id:147555)**. We re-run the analysis with different priors—for example, a **skeptical prior** centered at zero effect, or a **weakly informative prior** that is much broader and lets the data speak more freely—and we report how the conclusions change [@problem_id:4442689]. This transparently communicates the extent to which our conclusions depend on our initial assumptions.

This dynamic interplay shows that prior elicitation is not a one-off task but the beginning of a dialogue. It's a conversation between existing knowledge and new evidence, a process that brings structure to our reasoning and forces us to confront the assumptions that all too often remain hidden. By making our beliefs explicit, we make them testable, refinable, and ultimately, more scientific. It is through this disciplined process that we can stand on the shoulders of previous work [@problem_id:5015031] and allow our knowledge to evolve in a coherent, cumulative way.