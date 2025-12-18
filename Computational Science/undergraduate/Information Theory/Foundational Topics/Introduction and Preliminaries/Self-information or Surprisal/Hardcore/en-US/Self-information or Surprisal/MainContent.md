## Introduction
How much information is in a single message? At its core, information theory seeks to answer this question. We intuitively understand that learning about a rare, unexpected event is more "informative" than learning about a common, predictable one. The concept of [self-information](@entry_id:262050), or [surprisal](@entry_id:269349), provides the rigorous mathematical foundation for this intuition, allowing us to quantify the "surprise" associated with any given outcome. This article addresses the fundamental challenge of formalizing this measure, moving from a qualitative feeling to a quantitative tool.

To build a comprehensive understanding, our exploration is structured across three key chapters. In "Principles and Mechanisms," we will derive the formula for [self-information](@entry_id:262050) from a set of desirable properties and explore its fundamental characteristics. Next, "Applications and Interdisciplinary Connections" will showcase the remarkable utility of this concept, demonstrating how it provides a common language for analyzing phenomena in fields from physics and genetics to computer science and finance. Finally, "Hands-On Practices" will give you the opportunity to solidify your knowledge by applying the principles of [surprisal](@entry_id:269349) to solve concrete problems. We begin by establishing the foundational principles that allow us to measure information itself.

## Principles and Mechanisms

In our exploration of information theory, we begin by addressing a fundamental question: how can we quantify the amount of information conveyed by the occurrence of a single event? Intuitively, we understand that learning about a highly predictable outcome is not particularly informative, whereas learning about a rare or unexpected outcome provides a significant amount of new information. The formalization of this intuition is the concept of **[self-information](@entry_id:262050)**, also known as **[surprisal](@entry_id:269349)**. This chapter will develop this concept from first principles, establish its mathematical definition, and explore its properties and applications through a series of illustrative examples.

### From Intuition to a Mathematical Measure

Consider the act of receiving a message or observing an event. The "information" we gain is intrinsically linked to the reduction of our uncertainty. Before the event, there are multiple possibilities, each with a certain likelihood. After the event, one of these possibilities is realized, and our uncertainty is resolved. The more unlikely an event was, the greater the resolution of uncertainty, and thus, the greater the [information content](@entry_id:272315).

Let us consider a few scenarios:
- A fair coin is tossed. The outcome is "heads". This is not particularly surprising.
- A heavily biased coin, which lands on "heads" 99.9% of the time, is tossed. The outcome is "tails". This is extremely surprising.
- In a secure communication protocol, an agent correctly guesses a secret key on their first attempt from a vast number of possibilities . The information gained by this single correct guess is immense, as it overcomes tremendous uncertainty.

To build a mathematical measure of information, let us denote the [self-information](@entry_id:262050) associated with an event $x$ that occurs with probability $P(x)$ as $I(x)$. We can propose a set of desirable properties for this function:

1.  **Dependence on Probability:** The information content should only depend on the probability of the event, not its specific nature. Thus, $I(x)$ can be written as a function $I(P(x))$.
2.  **Non-negativity:** The amount of information gained cannot be negative. $I(p) \ge 0$ for any probability $p \in [0, 1]$.
3.  **Monotonicity:** As an event becomes less probable, its [self-information](@entry_id:262050) must increase. If $p_1 \lt p_2$, then $I(p_1) \gt I(p_2)$.
4.  **Certainty:** An event that is certain to happen ($p=1$) provides no information. $I(1) = 0$.
5.  **Additivity for Independent Events:** If two [independent events](@entry_id:275822), $x$ and $y$, occur, their [joint probability](@entry_id:266356) is $P(x, y) = P(x)P(y)$. The total information gained from observing both should be the sum of the information from each individual event. That is, $I(P(x)P(y)) = I(P(x)) + I(P(y))$.

The only mathematical function (up to a scaling constant) that satisfies these properties, particularly the additivity requirement, is the logarithm. This leads us to the formal definition of [self-information](@entry_id:262050).

### The Definition of Self-Information

The **[self-information](@entry_id:262050)**, or **[surprisal](@entry_id:269349)**, of an outcome $x$ with probability $P(x)$ is defined as:

$$
I(x) = -\log(P(x)) = \log\left(\frac{1}{P(x)}\right)
$$

The negative sign ensures that the measure is non-negative, since probabilities are between 0 and 1, and their logarithms are consequently non-positive. The base of the logarithm determines the unit of information. In information theory and computer science, the standard is to use the base-2 logarithm, and the unit is called the **bit**. The term "bit" in this context is a measure of information, which should not be confused with its use as a binary digit in computing, though the two are deeply related. One bit is the amount of information gained when one of two equally likely possibilities is realized, such as the flip of a fair coin:

$$
I(\text{Heads}) = -\log_2(0.5) = -\log_2\left(\frac{1}{2}\right) = \log_2(2) = 1 \text{ bit}
$$

Throughout this text, unless otherwise specified, all logarithms for information measurement will be base-2, and [self-information](@entry_id:262050) will be expressed in bits. The formula is thus:

$$
I(x) = -\log_2(P(x))
$$

This definition elegantly captures our intuition. For a highly probable event, $P(x) \to 1$, and $I(x) \to -\log_2(1) = 0$ bits. For a very rare event, $P(x) \to 0$, and $I(x) \to \infty$. This reflects the infinite surprise associated with an event we considered impossible.

For instance, in a [quantum key distribution](@entry_id:138070) (QKD) system, if a vertically polarized photon is transmitted with a very low probability of $p = 0.005$, observing this event yields $I(\text{vertical}) = -\log_2(0.005) \approx 7.644$ bits of information. In contrast, observing the much more common horizontally polarized photon, with $p = 0.995$, yields only $I(\text{horizontal}) = -\log_2(0.995) \approx 0.0072$ bits . The difference in [information content](@entry_id:272315) is stark and quantifies the relative surprisingness. We can even calculate the exact analytical difference in information between observing a rare event versus a common one. For a biological event with probability $p=0.05$, the extra information from observing it ('1') versus not observing it ('0', with probability $1-p=0.95$) is $\Delta I = I(1) - I(0) = -\log_2(p) - (-\log_2(1-p)) = \log_2(\frac{1-p}{p})$. For $p=0.05$, this difference is exactly $\log_2(19)$ bits .

### Properties and Applications of Self-Information

The power of [self-information](@entry_id:262050) lies in its wide applicability, from simple games of chance to complex physical and computational systems. The key is always to first determine the probability of the event in question, and then apply the definition.

#### Information Content of Simple and Compound Events

Let's examine a system with more than two outcomes, such as a quantum [random number generator](@entry_id:636394) designed to simulate a six-sided die. Suppose a flaw results in a bias where the outcome '1' occurs with probability $P(1) = 1/3$, and the other five outcomes are equally likely. The total remaining probability is $1 - 1/3 = 2/3$, which is distributed among five outcomes, so for any $k \in \{2, 3, 4, 5, 6\}$, the probability is $P(k) = (2/3)/5 = 2/15$. The [self-information](@entry_id:262050) of observing the biased outcome '1' is $I(1) = -\log_2(1/3) \approx 1.585$ bits. The [self-information](@entry_id:262050) of observing a '4' is $I(4) = -\log_2(2/15) \approx 2.907$ bits . As expected, the less probable event carries significantly more information.

The additivity property is particularly powerful when analyzing sequences of events. If a series of events are statistically independent, the probability of observing a specific sequence is the product of the individual probabilities. Consequently, the total [self-information](@entry_id:262050) of the sequence is the sum of the individual self-informations.

Consider a biased source generating a stream of independent bits, with $P(0) = 0.6$ and $P(1) = 0.4$. What is the [surprisal](@entry_id:269349) of observing the specific 16-bit sequence `0100110100010100`? This sequence contains 10 zeros and 6 ones. The probability of this specific sequence is $P(\text{sequence}) = (0.6)^{10} (0.4)^6$. The total [self-information](@entry_id:262050) is:

$$
I(\text{sequence}) = -\log_2\left((0.6)^{10} (0.4)^6\right) = -10\log_2(0.6) - 6\log_2(0.4) \approx 15.30 \text{ bits}
$$


This additive principle applies even if the [independent events](@entry_id:275822) are not identically distributed. For a satellite whose state is reported in independent packets, the total information of a sequence of states is the sum of the information of each state report. For a sequence of states ('Nominal', 'Nominal', 'Warning', 'Nominal', 'Error') with respective probabilities $P(N)=0.95$, $P(W)=0.04$, and $P(E)=0.01$, the total [surprisal](@entry_id:269349) is $I(\text{total}) = 3 \times I(N) + I(W) + I(E) = -3\log_2(0.95) - \log_2(0.04) - \log_2(0.01) \approx 11.5$ bits . Notice that the highly probable 'Nominal' states contribute very little to the total [surprisal](@entry_id:269349), which is dominated by the rare 'Warning' and 'Error' states.

#### Information in Complex Probabilistic Models

The concept of [self-information](@entry_id:262050) extends seamlessly to more complex scenarios where the probability of an event must be derived from an underlying statistical model. The core principle remains: first, calculate the probability of the event of interest.

A classic example is a random walk. Imagine a particle starting at $x=0$ that moves right with probability $p=0.75$ and left with probability $1-p=0.25$ at each step. What is the [self-information](@entry_id:262050) of finding the particle at position $x=+2$ after exactly $N=6$ steps? To be at $x=+2$ after 6 steps, the particle must have taken $R$ steps to the right and $L$ steps to the left, where $R+L=6$ and the final position is $R-L = +2$. Solving this system gives $R=4$ and $L=2$. The event is "4 right steps and 2 left steps in any order". The number of ways this can happen is given by the binomial coefficient $\binom{6}{4} = 15$. The probability of any single such path (e.g., RRRRLL) is $(0.75)^4(0.25)^2$. Therefore, the total probability of the event is:

$$
P(X_6=+2) = \binom{6}{4} (0.75)^4 (0.25)^2 = \frac{1215}{4096}
$$

The [self-information](@entry_id:262050) is then $I(X_6=+2) = -\log_2(1215/4096) \approx 1.753$ bits . This illustrates that the calculation is not about a single outcome path but about the probability of an aggregate event.

This principle is also applicable in physics. The decay of radioactive nuclei is a [random process](@entry_id:269605). For a large number of atoms and a short observation time, the number of decays can be modeled by a **Poisson distribution**. Consider an experiment monitoring one mole of Bismuth-209 for one second. Given its extremely long half-life, the expected number of decays, $\mu$, is very small (on the order of $10^{-4}$). The probability of observing exactly one decay is given by the Poisson formula $P(k=1) = \mu e^{-\mu}$. Calculating this probability and then its [self-information](@entry_id:262050) reveals that observing this single decay event provides approximately $10.57$ bits of information . This shows how information theory provides a quantitative measure for the significance of observing rare physical phenomena.

### From Self-Information to Entropy: The Concept of Average Surprisal

We have established how to measure the information of a single, specific outcome. However, we are often interested in the characteristics of the random process itself. A crucial question arises: on average, how much information can we expect to receive from one trial of a random experiment?

This question leads us to calculate the **expected value** of the [self-information](@entry_id:262050). Let $X$ be a random variable representing the outcome of an experiment. The [self-information](@entry_id:262050) is itself a function of the random variable, $I(X) = -\log_2(P(X))$. The expected [self-information](@entry_id:262050) is calculated by summing the [self-information](@entry_id:262050) of each possible outcome, weighted by its probability of occurrence:

$$
E[I(X)] = \sum_{x \in \mathcal{X}} P(x) I(x) = \sum_{x \in \mathcal{X}} P(x) \left(-\log_2(P(x))\right)
$$

where $\mathcal{X}$ is the set of all possible outcomes.

Let's compute this for the simplest non-trivial case: a binary source (a Bernoulli trial) where $P(X=1) = p$ and $P(X=0) = 1-p$ . The expected [self-information](@entry_id:262050) is:

$$
E[I(X)] = P(1)I(1) + P(0)I(0) = p(-\log_2 p) + (1-p)(-\log_2(1-p))
$$

$$
E[I(X)] = -p\log_2(p) - (1-p)\log_2(1-p)
$$

This fundamental quantity is known as the **Shannon entropy** of the random variable $X$, denoted $H(X)$. It represents the average [surprisal](@entry_id:269349), or average information content, per outcome from the source. It can also be interpreted as a measure of the uncertainty inherent in the [random process](@entry_id:269605) before an outcome is known. If the source is highly predictable (e.g., $p$ is close to 0 or 1), the entropy is low, signifying little uncertainty and low average [information gain](@entry_id:262008). If the outcomes are equally likely ($p=0.5$), the uncertainty is maximal, and so is the entropy, which reaches its peak value of 1 bit for a binary source.

The concept of entropy is a cornerstone of information theory, providing the foundation for understanding [data compression](@entry_id:137700), channel capacity, and the fundamental limits of communication. We have seen how it emerges naturally from the idea of averaging the [surprisal](@entry_id:269349) of individual events. In the subsequent chapter, we will delve deeper into the properties and profound implications of entropy.