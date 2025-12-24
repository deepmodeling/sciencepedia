## Introduction
In the study of dynamic systems, many phenomena manifest as sequences of [discrete events](@entry_id:273637) in time, from the firing of neurons to the occurrence of earthquakes or financial trades. While simple models like the Poisson process treat these events as independent, a vast number of real-world systems exhibit a crucial property: memory. The occurrence of an event can influence the probability of subsequent events, creating clusters, cascades, and complex temporal patterns. The Hawkes [self-exciting point process](@entry_id:1131409) provides a powerful and elegant mathematical framework to capture precisely this kind of history-dependent, self-propagating behavior. It addresses the fundamental gap left by memoryless models, allowing us to quantify how past events excite future activity.

This article provides a thorough exploration of the Hawkes process, designed to build a robust theoretical and practical understanding. The following chapters will guide you through its core concepts and diverse applications. First, in **Principles and Mechanisms**, we will deconstruct the mathematical foundations of the model, starting with the pivotal concept of the [conditional intensity function](@entry_id:1122850), exploring its interpretation as a branching process, and examining the conditions for its stability. We will also cover crucial extensions to model [complex networks](@entry_id:261695) with both excitatory and inhibitory connections. Next, in **Applications and Interdisciplinary Connections**, we will see the theory in action, exploring its primary role in computational neuroscience for modeling spike trains and inferring [neural connectivity](@entry_id:1128572), as well as its utility in fields like [seismology](@entry_id:203510), epidemiology, and finance. Finally, the **Hands-On Practices** section offers a chance to solidify this knowledge through targeted exercises on deriving key properties and understanding parameter estimation.

## Principles and Mechanisms

The Hawkes [self-exciting process](@entry_id:1131410) provides a rich mathematical framework for modeling event sequences where the occurrence of an event makes subsequent events more likely. This chapter elucidates the fundamental principles and mechanisms of these processes, beginning with their formal definition and progressing to their statistical properties, their interpretation as [branching processes](@entry_id:276048), and their extensions to model complex network dynamics involving both excitation and inhibition.

### The Conditional Intensity of a Point Process

At the heart of modern [point process](@entry_id:1129862) theory is the concept of the **[conditional intensity function](@entry_id:1122850)**, denoted $\lambda(t)$. To understand this, we first represent a sequence of discrete events in time, such as neuronal spikes, as a **[counting process](@entry_id:896402)**, $N(t)$, which records the total number of events that have occurred up to and including time $t$. We assume the process is **simple**, meaning that events are distinct and no two events occur at exactly the same time. The path of $N(t)$ is therefore a right-continuous, non-decreasing step function with jumps of unit size.

The entire history of events up to time $t$ is captured by the [filtration](@entry_id:162013) $\mathcal{H}_t$, which represents all information available about the process's past. The conditional intensity $\lambda(t)$ is a non-negative process that leverages this history to specify the instantaneous likelihood of a new event. Formally, it is defined as the history-dependent, expected rate of events at time $t$ . This is expressed as the limit of the [conditional expectation](@entry_id:159140) of the event rate in a small future interval:

$$
\lambda(t) \equiv \lim_{h \downarrow 0} \frac{1}{h}\,\mathbb{E}\left[N(t+h)-N(t)\,\middle|\,\mathcal{H}_{t}\right]
$$

A crucial requirement for $\lambda(t)$ is that it must be **predictable**, meaning its value at time $t$ is determined solely by the history *strictly before* time $t$. This ensures that the occurrence of an event at time $t$ does not influence its own rate of generation.

From this definition, the [conditional intensity](@entry_id:1122849) directly gives the infinitesimal probability of observing a new event. For an infinitesimally small interval $[t, t+dt)$, the probability of an event occurring, given the past, is:

$$
\mathbb{P}\left(N(t+dt)-N(t)=1\,\middle|\,\mathcal{H}_{t}\right) = \lambda(t)\,dt + o(dt)
$$

The term $o(dt)$ denotes a quantity that becomes negligible compared to $dt$ as $dt \to 0$. The simplicity of the process ensures that the probability of two or more events in this infinitesimal window is also $o(dt)$. Therefore, the [conditional intensity function](@entry_id:1122850) $\lambda(t)$ completely characterizes the dynamics of the [point process](@entry_id:1129862). Different models of point processes are distinguished by the specific functional form they assume for $\lambda(t)$.

### The Linear Hawkes Process: A Model of Self-Excitation

The Hawkes process models the phenomenon of self-excitation, where past events increase the probability of future events. This is captured by defining the [conditional intensity](@entry_id:1122849) as the sum of a constant baseline rate and contributions from all past events. For a univariate (single) process, the linear Hawkes model specifies the intensity as:

$$
\lambda(t) = \mu + \sum_{t_i  t} \phi(t - t_i)
$$

Here, $\mu \ge 0$ is the **baseline intensity**, representing a background rate of spontaneous events, analogous to exogenous inputs to a system. The sum is taken over all past event times $t_i$ that occurred strictly before the present time $t$. The function $\phi(\cdot)$ is the **excitation kernel** or **memory kernel**, a non-negative, causal function ($\phi(u)=0$ for $u \le 0$) that describes the influence of a past event on the present intensity. The term $\phi(t-t_i)$ quantifies the increase in intensity at time $t$ caused by the event that occurred at time $t_i$.

This summation form can be expressed more compactly using a Lebesgue-Stieltjes integral with respect to the [counting process](@entry_id:896402) $N(s)$ . This integral representation is fundamental:

$$
\lambda(t) = \mu + \int_0^{t^-} \phi(t-s)\,dN(s)
$$

The integral effectively "picks out" the values of the function $\phi(t-s)$ at the past event times $s=t_i$ and sums them. The upper integration limit of $t^-$ (denoting integration over the [open interval](@entry_id:144029) $[0,t)$) is critical, as it mathematically enforces the predictability of $\lambda(t)$ by ensuring only events strictly prior to $t$ contribute to the intensity at $t$.

This history-dependent structure distinguishes the Hawkes process from simpler models. For instance, if $\phi(t) \equiv 0$, the intensity becomes constant, $\lambda(t) = \mu$, and the process reduces to a memoryless **homogeneous Poisson process** . If the intensity depended only on the time elapsed since the most recent event, $\lambda(t) = h(t - t_{N(t)})$, the process would be a **[renewal process](@entry_id:275714)**, whose inter-event intervals are [independent and identically distributed](@entry_id:169067). A Hawkes process, by contrast, has a richer memory structure where the entire history, not just the last event, shapes the future .

### The Branching Process Interpretation

A powerful and intuitive way to understand the Hawkes process is through its equivalence to a **Poisson cluster process**, also known as a [branching process](@entry_id:150751) with immigration . In this view:

1.  **Immigrants**: "Parent" or "immigrant" events are generated by an external source according to a homogeneous Poisson process with rate $\mu$. These events initiate new clusters.

2.  **Offspring**: Each event in the process (whether an immigrant or an offspring) can itself become a parent, generating a new set of "offspring" events. The rate at which a parent at time $t_i$ generates offspring at a later time $t$ is given by the kernel $\phi(t-t_i)$.

The total observed process $N(t)$ is the superposition of all events from all clusters. This construction precisely recovers the self-exciting intensity definition.

Within this framework, a crucial quantity is the **[branching ratio](@entry_id:157912)**, denoted by $\eta$. It is defined as the total integral of the kernel:

$$
\eta = \int_0^\infty \phi(u)\,du
$$

The branching ratio has a clear physical interpretation: it is the expected number of direct offspring generated by any single event . In fact, for a given parent event, the number of direct offspring it generates follows a Poisson distribution with mean $\eta$.

### Stability and Stationary Properties

The branching process interpretation provides immediate insight into the stability of the Hawkes process. The long-term behavior of the system depends critically on the value of the branching ratio, $\eta$.

If $\eta  1$, each event produces, on average, less than one new event. This means each cluster of descendants is guaranteed to eventually die out. The process is **subcritical** and can achieve a stationary state with a finite mean rate. The expected total size of a cluster initiated by a single immigrant (including the immigrant itself) can be calculated as a [geometric series](@entry_id:158490) over generations, yielding $1 + \eta + \eta^2 + \dots = \frac{1}{1-\eta}$ . The stationary mean intensity of the overall process, $\bar{\lambda}$, is then the rate of immigrants multiplied by the expected size of each cluster:

$$
\bar{\lambda} = \frac{\mu}{1-\eta}
$$

If $\eta \ge 1$, each event produces, on average, one or more new events, leading to a chain reaction where the number of events can grow indefinitely. The process is **critical** ($\eta=1$) or **supercritical** ($\eta > 1$), and it will not converge to a stationary state with a finite rate; it is said to "explode" .

The self-exciting nature of the Hawkes process induces characteristic statistical signatures in its event times. Unlike a Poisson or renewal process, the inter-event intervals (IEIs) are not independent. The occurrence of an event raises the intensity, making subsequent events more likely to occur sooner. This leads to temporal clustering and a positive serial correlation between successive IEIs . This clustering also results in a variance of the event count that is larger than its mean, a property known as **overdispersion**. A common measure of this is the asymptotic **Fano factor**, the ratio of the count variance to the count mean over long time windows. For a stationary Hawkes process, this factor is greater than $1$, whereas for a Poisson process it is exactly $1$. For a process with an exponential kernel $\phi(t) = \alpha e^{-\beta t}$, the branching ratio is $\eta = \alpha/\beta$, and the asymptotic Fano factor can be shown to be $F = \frac{1}{(1-\eta)^2}$ .

### Criticality and Neural Avalanches

The critical point $\eta=1$ holds special significance in computational neuroscience due to its connection with the **[criticality hypothesis](@entry_id:1123194)**, which posits that cortical networks operate near a phase transition to optimize information processing. In the context of a Hawkes process, this [critical state](@entry_id:160700) gives rise to dynamics that closely resemble "[neural avalanches](@entry_id:1128565)" observed in experiments.

At $\eta=1$, the expected cluster size diverges, and the process is no longer stationary . A key result from branching process theory states that for a critical process, the distribution of the total cluster size, $S$, follows a **power law** for large sizes, typically of the form:

$$
P(S=s) \sim s^{-3/2}
$$

This [heavy-tailed distribution](@entry_id:145815) means that while most clusters are small, arbitrarily large cascades of events are possible and occur with a non-negligible probability. This mathematical result provides a canonical model for the power-law distributions of avalanche sizes reported in cortical recordings.

In the slightly subcritical regime ($\eta \lesssim 1$), the process exhibits behavior that is "nearly critical." The avalanche size distribution still follows a power law over a wide range but is ultimately suppressed by an exponential cutoff for very large sizes. The characteristic scale of this cutoff diverges as $\eta \to 1$, meaning the system displays critical-like behavior over increasingly large scales as it approaches the transition point .

### Extensions: Networks and Inhibition

The basic Hawkes model can be extended in crucial ways to better capture the complexity of biological neural networks.

#### Multivariate Hawkes Processes

To model a population of $d$ interacting neurons, we use a multivariate Hawkes process, described by a vector of [counting processes](@entry_id:260664) $\{N_i(t)\}_{i=1}^d$. The conditional intensity for each neuron $i$ depends on its own past and the past activity of all other neurons $j$ in the network :

$$
\lambda_i(t) = \mu_i + \sum_{j=1}^d \int_0^{t^-} \phi_{ij}(t-s)\,dN_j(s)
$$

Here, $\phi_{ij}(u)$ is the interaction kernel describing the influence of a spike from neuron $j$ on the future intensity of neuron $i$. The stability of such a network is governed by the **influence matrix**, $A$, whose entries are the $L^1$ norms of the kernels, $A_{ij} = \int_0^\infty \phi_{ij}(u)\,du$. The entry $A_{ij}$ represents the total expected number of spikes in neuron $i$ directly caused by a single spike in neuron $j$. The network process is stable and admits a stationary solution if and only if the **spectral radius** of this matrix, $\rho(A)$, is less than $1$. In this case, the vector of stationary mean rates, $\mathbf{m}$, is given by the linear system $\mathbf{m} = (I-A)^{-1}\boldsymbol{\mu}$.

For example, consider a two-neuron network with kernels $\phi_{11}(u)=0.4e^{-2u}$, $\phi_{12}(u)=0.3e^{-3u}$, $\phi_{21}(u)=0.5e^{-1.5u}$, and $\phi_{22}(u)=0$. The influence matrix is calculated as:
$$
A = \begin{pmatrix} \int_{0}^{\infty}0.4e^{-2u}\,du  \int_{0}^{\infty}0.3e^{-3u}\,du \\ \int_{0}^{\infty}0.5e^{-1.5u}\,du  0 \end{pmatrix} = \begin{pmatrix} 0.2  0.1 \\ \frac{1}{3}  0 \end{pmatrix}
$$
The spectral radius of this matrix is $\rho(A) = \frac{3 + \sqrt{39}}{30} \approx 0.308$, which is less than $1$, so this network is stable .

Furthermore, when the kernels are composed of exponential functions, the non-Markovian Hawkes process can be given a finite-dimensional Markovian representation by augmenting the state space with auxiliary "shot-noise" variables that track the decaying influence of past spikes. This property is computationally very convenient for simulation and analysis.

#### Inhibitory Interactions and Nonlinearity

The linear model requires $\lambda(t) \ge 0$. If we strictly use non-negative kernels, this is guaranteed. However, to model inhibitory interactions, we need kernels $\phi_{ij}(u)$ that can be negative. In a linear model, a burst of spikes from an inhibitory source could drive the intensity $\lambda_i(t)$ below zero, which is physically nonsensical .

A [standard solution](@entry_id:183092) is to introduce a **nonlinear link function** $g(\cdot)$ that ensures a non-negative output. The most common choice is the rectifying function $g(x) = [x]_+ = \max\{0, x\}$. The intensity is then defined as:

$$
\lambda_i(t) = g\left( \mu_i + \sum_{j=1}^d \int_0^{t^-} \phi_{ij}(t-s)\,dN_j(s) \right)
$$

This formulation naturally allows for both excitatory ($\phi_{ij}>0$) and inhibitory ($\phi_{ij}  0$) interactions while ensuring $\lambda_i(t) \ge 0$ by construction.

The stability condition for these nonlinear networks must account for the total magnitude of interactions, regardless of sign. The simple influence matrix $A$ is no longer sufficient. Instead, stability is determined by the matrix $\Gamma$ of the absolute norms of the kernels, with entries $\Gamma_{ij} = \int_0^\infty |\phi_{ij}(u)|\,du$. A [sufficient condition](@entry_id:276242) for the existence of a unique stationary solution is that the spectral radius of this new matrix, $\rho(\Gamma)$, is strictly less than $1$ .

### The Likelihood Function

A final core mechanism is the ability to connect the model to data. Given a set of observed event times $\{t_1, t_2, \dots, t_n\}$ in an interval $[0, T]$, the parameters of a Hawkes process are typically estimated by maximizing the **log-likelihood function**. This function can be derived from the [conditional intensity](@entry_id:1122849) and has a general form for any simple [point process](@entry_id:1129862) :

$$
\log \mathcal{L}(\theta) = \sum_{k=1}^n \log \lambda(t_k | \theta) - \int_0^T \lambda(s | \theta) ds
$$

Here, $\theta$ represents the set of model parameters (e.g., $\mu$ and parameters defining $\phi$). The first term is the sum of the log-intensities at the precise moments events occurred. The second term, the integrated intensity over the entire observation window, accounts for the "survival" probability—the probability that no events occurred at all other times. This likelihood provides a principled foundation for statistical inference, allowing us to learn the structure of self-excitation and [network connectivity](@entry_id:149285) from empirical data.