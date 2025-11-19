## Introduction
In the landscape of modern communication, from cellular networks to the Internet of Things, a common scenario arises: multiple independent users attempting to transmit information to a single, shared destination. How do we quantify the ultimate limits of such a system? The answer lies in the study of the **Multiple-Access Channel (MAC)**, a foundational model in multi-user information theory that captures the essence of this shared communication problem. The central challenge is not merely to avoid interference but to understand its structure and exploit it, determining the maximum simultaneous data rates at which all users can reliably communicate. This set of achievable rates forms a multi-dimensional space known as the [capacity region](@entry_id:271060).

This article provides a comprehensive exploration of the MAC [capacity region](@entry_id:271060). It demystifies the theoretical bounds that define these limits and connects them to practical engineering realities. Over the three chapters, you will gain a deep understanding of this cornerstone concept. The first chapter, **Principles and Mechanisms**, will lay the mathematical groundwork, defining the [capacity region](@entry_id:271060) for both discrete and Gaussian channels and introducing the powerful decoding technique of Successive Interference Cancellation (SIC). The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the model's vast utility, from designing wireless systems and analyzing network protocols to its surprising connections with physical layer security and quantum information theory. Finally, the **Hands-On Practices** section will offer a chance to apply these principles to concrete problems, solidifying your knowledge. By navigating these concepts, you will uncover why simultaneous transmission is superior to taking turns and how the abstract shape of the [capacity region](@entry_id:271060) dictates the design of our most advanced [communication systems](@entry_id:275191).

## Principles and Mechanisms

In the study of multi-user information theory, the **Multiple-Access Channel (MAC)** represents a foundational scenario where multiple transmitters communicate simultaneously with a single receiver. This model is central to understanding the fundamental limits of uplink communication in wireless systems, [sensor networks](@entry_id:272524), and various other shared-medium environments. This chapter delineates the principles that define the capacity of a MAC and the mechanisms by which this capacity can be achieved.

### Defining the MAC Capacity Region

A discrete memoryless $K$-user MAC is characterized by $K$ input alphabets $\mathcal{X}_1, \dots, \mathcal{X}_K$, a single output alphabet $\mathcal{Y}$, and a channel transition probability $p(y|x_1, \dots, x_K)$. The inputs $X_1, \dots, X_K$ are chosen independently by the respective users. The central challenge is to determine the set of all [achievable rate](@entry_id:273343) tuples $(R_1, \dots, R_K)$ at which the users can reliably transmit their information. This set is known as the **[capacity region](@entry_id:271060)**.

For conceptual clarity, we focus on the two-user case ($K=2$). A rate pair $(R_1, R_2)$ is achievable if there exist codes for both users that allow the receiver to decode both messages with an arbitrarily small probability of error, provided the block length is sufficiently long. The [capacity region](@entry_id:271060) $\mathcal{C}$ is the closure of the set of all [achievable rate](@entry_id:273343) pairs. A cornerstone result of information theory states that the [capacity region](@entry_id:271060) of a two-user discrete memoryless MAC is the [convex hull](@entry_id:262864) of all rate pairs $(R_1, R_2)$ satisfying the following inequalities for some product input distribution $p(x_1)p(x_2)$:

$R_1 \ge 0, R_2 \ge 0$
$R_1 \leq I(X_1; Y | X_2)$
$R_2 \leq I(X_2; Y | X_1)$
$R_1 + R_2 \leq I(X_1, X_2; Y)$

The individual rate bounds, $I(X_1; Y | X_2)$ and $I(X_2; Y | X_1)$, represent the maximum rate for one user given that the other user's message has already been successfully decoded and is thus known to the receiver. The [sum-rate bound](@entry_id:270110), $I(X_1, X_2; Y)$, represents the total amount of information about the input pair that the output provides.

The final [capacity region](@entry_id:271060) is the union of all such regions over all possible independent input distributions $p(x_1)$ and $p(x_2)$, followed by a convex hull operation. The [convexity](@entry_id:138568) of the region is operationally guaranteed by a strategy known as **[time-sharing](@entry_id:274419)**. If a rate pair $\vec{R}_A$ is achievable with one coding strategy and another pair $\vec{R}_B$ is achievable with a different strategy, then any rate pair on the line segment connecting them, $\vec{R} = \alpha \vec{R}_A + (1-\alpha) \vec{R}_B$ for $\alpha \in [0,1]$, can be achieved by using the first strategy for a fraction $\alpha$ of the transmission time and the second strategy for the remaining $1-\alpha$ fraction [@problem_id:1608094]. This property ensures that the boundary of the [capacity region](@entry_id:271060) does not have any "inward dents." The resulting shape is typically a pentagon in the first quadrant of the $(R_1, R_2)$ plane.

### Case Studies in Discrete Memoryless MACs

To build intuition, we examine the capacity regions of several canonical [discrete channels](@entry_id:267374). For deterministic channels, where the output $Y$ is a fixed function of the inputs $(X_1, X_2)$, the [conditional entropy](@entry_id:136761) $H(Y|X_1, X_2)$ is zero. This greatly simplifies the [mutual information](@entry_id:138718) bounds:
$I(X_1, X_2; Y) = H(Y) - H(Y|X_1, X_2) = H(Y)$
$I(X_1; Y | X_2) = H(Y|X_2) - H(Y|X_1, X_2) = H(Y|X_2)$
Furthermore, if $Y = f(X_1, X_2)$ and $f$ is invertible in $X_1$ for any fixed $X_2$, then $H(Y|X_2) = H(X_1)$. The capacity bounds thus become $R_1 \leq H(X_1)$, $R_2 \leq H(X_2)$, and $R_1 + R_2 \leq H(Y)$.

#### The Binary Adder Channel

Consider a two-user MAC where both users transmit a binary symbol, $X_1, X_2 \in \{0, 1\}$, and the receiver observes their arithmetic sum, $Y = X_1 + X_2$. The output alphabet is $\mathcal{Y} = \{0, 1, 2\}$. To find the [capacity region](@entry_id:271060), we must find the outer boundary by maximizing the entropy bounds over all independent Bernoulli input distributions, $\Pr[X_1=1] = p_1$ and $\Pr[X_2=1] = p_2$.

The individual rate constraints are maximized when the inputs are uniformly distributed ($p_1=0.5, p_2=0.5$), yielding $R_1 \leq H(X_1) = 1$ bit and $R_2 \leq H(X_2) = 1$ bit. The [sum-rate](@entry_id:260608) is limited by $H(Y)$. The distribution of $Y$ is determined by $p_1$ and $p_2$. It can be shown that $H(Y)$ is maximized when the inputs are uniform ($p_1=p_2=0.5$). In this case, the output distribution is $\Pr[Y=0]=0.25$, $\Pr[Y=1]=0.5$, $\Pr[Y=2]=0.25$, which yields a maximum entropy of $H(Y) = -0.25\log_2(0.25) - 0.5\log_2(0.5) - 0.25\log_2(0.25) = 1.5$ bits.

The [capacity region](@entry_id:271060) is therefore the pentagon defined by $R_1 \geq 0$, $R_2 \geq 0$, $R_1 \leq 1$, $R_2 \leq 1$, and $R_1 + R_2 \leq 1.5$. The two non-axis corner points occur at the intersection of the [sum-rate](@entry_id:260608) limit with the individual rate limits. As explored in [@problem_id:1608084], these points are $(R_1, R_2) = (1, 0.5)$ and $(R_1, R_2) = (0.5, 1)$.

#### The Binary XOR Channel

A related example is the binary XOR channel, where $Y = X_1 \oplus X_2$ [@problem_id:1663797]. The output $Y$ is also binary. Following a similar analysis, the individual rate bounds are $R_1 \leq H(X_1)$ and $R_2 \leq H(X_2)$, which are maximized at 1 bit for uniform inputs. The [sum-rate](@entry_id:260608) is bounded by $H(Y)$. Since $Y$ is a binary random variable, its entropy is at most 1 bit, i.e., $H(Y) \leq 1$. This maximum is achieved if at least one of the inputs is uniformly distributed. The [capacity region](@entry_id:271060) is therefore the set of rate pairs satisfying $R_1 \ge 0, R_2 \ge 0,$ and $R_1 + R_2 \le 1$. This is a simple triangular region, smaller than that of the adder channel, intuitively because the modulo-2 sum $X_1 \oplus X_2$ conceals more information about the individual inputs than the arithmetic sum $X_1+X_2$.

These principles can be extended to more users. For a three-user [binary adder channel](@entry_id:265650) $Y = X_1 + X_2 + X_3$, the maximum [sum-rate](@entry_id:260608) is again found by maximizing $H(Y)$ over all independent input distributions. The maximum is achieved for uniform inputs, resulting in a [sum-rate capacity](@entry_id:267947) of $R_{sum} = 3 - \frac{3}{4}\log_2(3) \approx 1.811$ bits/use [@problem_id:1608088]. Channel impairments, such as erasures, predictably shrink the [capacity region](@entry_id:271060). For an adder channel that is erased with probability $p$, all mutual information terms, and thus the achievable rates, are scaled by a factor of $(1-p)$ [@problem_id:1608119].

### The Gaussian Multiple-Access Channel (GMAC)

A highly important continuous-alphabet model is the **Gaussian Multiple-Access Channel (GMAC)**. Here, the received signal is $Y = X_1 + X_2 + Z$, where $X_1$ and $X_2$ are the signals from the two users, subject to [average power](@entry_id:271791) constraints $E[X_1^2] \le P_1$ and $E[X_2^2] \le P_2$. The term $Z$ represents additive white Gaussian noise (AWGN) with power $N$. For [reliable communication](@entry_id:276141) over a bandwidth of $W$ Hertz, the [capacity region](@entry_id:271060) is given by the set of all rate pairs $(R_1, R_2)$ in bits per second satisfying:

$R_1 \leq W \log_2\left(1 + \frac{P_1}{N}\right)$
$R_2 \leq W \log_2\left(1 + \frac{P_2}{N}\right)$
$R_1 + R_2 \leq W \log_2\left(1 + \frac{P_1 + P_2}{N}\right)$

This region is achieved when the inputs $X_1$ and $X_2$ are independent Gaussian random variables.

#### The Superiority of Non-Orthogonal Access

A fundamental question in multi-user systems is whether it is better for users to share the channel by transmitting simultaneously or by taking turns (e.g., via Time-Division Multiplexing, TDM). The GMAC provides a clear answer. In a TDM scheme, one user transmits with power $P_1$ over the full bandwidth for a fraction of the time, and then the other transmits with power $P_2$. The maximum [sum-rate](@entry_id:260608) via TDM is $\max\{ W\log_2(1+P_1/N), W\log_2(1+P_2/N) \}$.

In contrast, the GMAC allows for simultaneous transmission, with a [sum-rate capacity](@entry_id:267947) of $C_{sum} = W\log_2(1+(P_1+P_2)/N)$. Due to the strict concavity of the logarithm function, it is always true that $\log_2(1+a+b) > \max\{\log_2(1+a), \log_2(1+b)\}$ for positive $a, b$. This proves that the [sum-rate](@entry_id:260608) achievable by treating interference intelligently in a MAC is strictly greater than what can be achieved by orthogonalizing users [@problem_id:1608101]. Simultaneous transmission is fundamentally more efficient.

#### Sum-Rate and Power Allocation

The [sum-rate bound](@entry_id:270110) $R_1 + R_2 \le W \log_2(1 + \frac{P_1 + P_2}{N})$ reveals another profound property of the GMAC. The maximum total throughput depends only on the *sum* of the user powers, $P_{total} = P_1 + P_2$, and not on how that power is distributed among the users [@problem_id:1663805]. Any [power allocation](@entry_id:275562) $(P_1, P_2)$ that uses the full budget, i.e., $P_1+P_2 = P_{total}$, achieves the same maximum [sum-rate](@entry_id:260608). This gives system designers considerable flexibility: for maximizing total data throughput, a single high-power user is equivalent to multiple low-power users whose powers sum to the same total.

### The Mechanism of Achievability: Successive Interference Cancellation

The pentagonal boundary of the [capacity region](@entry_id:271060) is not merely a theoretical construct; it is achievable through a practical and powerful decoding technique known as **Successive Interference Cancellation (SIC)**. This strategy turns the multi-user detection problem into a sequence of single-user detection problems. For a two-user GMAC, there are two primary SIC decoding orders, each corresponding to one of the non-axis corner points of the [capacity region](@entry_id:271060).

Let us consider the decoding order (1, 2), where the receiver decodes User 1 first, followed by User 2.
1.  **Decode User 1:** The receiver treats the signal from User 2, $X_2$, as additional noise. The total noise plus interference power is $N+P_2$. The maximum [achievable rate](@entry_id:273343) for User 1 is therefore $R_1 \le W \log_2\left(1 + \frac{P_1}{N+P_2}\right)$.
2.  **Decode User 2:** Assuming User 1's message was decoded correctly, the receiver can perfectly reconstruct the signal $X_1$ and subtract it from the received signal $Y$. The remaining signal is $Y' = Y - X_1 = X_2 + Z$. The receiver then decodes User 2's message from this cleaned signal, which is now a simple point-to-point channel with only the background noise $Z$. The maximum rate for User 2 is thus $R_2 \le W \log_2\left(1 + \frac{P_2}{N}\right)$.

This procedure achieves the rate pair $\left( W \log_2(1 + \frac{P_1}{N+P_2}), W \log_2(1 + \frac{P_2}{N}) \right)$, which is a corner point of the [capacity region](@entry_id:271060) [@problem_id:1661407]. By reversing the decoding order—decoding User 2 first (treating $X_1$ as noise) and then User 1—we achieve the other corner point: $\left( W \log_2(1 + \frac{P_1}{N}), W \log_2(1 + \frac{P_2}{N+P_1}) \right)$.

Any rate pair on the [sum-rate](@entry_id:260608) boundary (the line segment connecting these two corner points) can be achieved by [time-sharing](@entry_id:274419) between these two SIC strategies. This provides a clear operational meaning to the entire dominant face of the [capacity region](@entry_id:271060). For instance, if one user requires a fixed rate $R_A$, the maximum possible rate for the other user, $R_B^{max}$, is found on this boundary. This trade-off is governed by the [linear relationship](@entry_id:267880) $R_A + R_B^{max} = C_{sum}$, where $C_{sum} = W \log_2(1 + \frac{P_A + P_B}{N})$ [@problem_id:1658382].

### An Advanced Perspective: State-Dependent Channels

The principles of the MAC can be extended to more complex scenarios, such as channels whose characteristics vary over time according to a state variable. Consider a MAC where the channel law $p(y|x_1, x_2, s)$ depends on a state $s$. If the state sequence is known non-causally to both the transmitters and the receiver, they can adapt their strategies accordingly.

In this scenario, the [capacity region](@entry_id:271060) is the average of the capacity regions corresponding to each state. The [sum-rate capacity](@entry_id:267947) is simply the expectation of the state-dependent [sum-rate](@entry_id:260608) capacities: $C_{sum} = \mathbb{E}_S[C_{sum}(S)]$.

As a concrete example, take a binary XOR MAC where the noise bit $Z_i$ has a probability that depends on a state $S_i \in \{s_a, s_b\}$ [@problem_id:1608073]. Let the [crossover probability](@entry_id:276540) be $p_a$ in state $s_a$ and $p_b$ in state $s_b$, and let the states occur with probabilities $q$ and $1-q$, respectively. For a fixed state $s$, the channel is a binary symmetric MAC with [sum-rate capacity](@entry_id:267947) $1 - H_b(p_s)$, where $H_b(\cdot)$ is the [binary entropy function](@entry_id:269003). Since the state is known everywhere, the overall [sum-rate capacity](@entry_id:267947) is the weighted average:
$C_{sum} = q(1 - H_b(p_a)) + (1-q)(1 - H_b(p_b)) = 1 - \left(q H_b(p_a) + (1-q) H_b(p_b)\right)$.

This result illustrates how the fundamental framework for the MAC [capacity region](@entry_id:271060) can be adapted to incorporate additional information, providing a robust foundation for analyzing a wide array of complex [communication systems](@entry_id:275191).