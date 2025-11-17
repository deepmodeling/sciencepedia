## Introduction
In the study of stochastic processes, absorbing Markov chains represent a critically important class of models. They describe systems that evolve through a series of temporary states before inevitably reaching a permanent, terminal state from which there is no escape. This concept is fundamental to modeling countless real-world phenomena, from a gambler going bankrupt and a mechanical component failing to a species going extinct or a student graduating. While the idea is intuitive, a formal framework is needed to answer crucial quantitative questions: How long, on average, will the process last before being absorbed? If there are multiple terminal outcomes, what is the probability of ending in each one?

This article addresses this need by providing a detailed guide to the theory and application of absorbing Markov chains. It equips you with the analytical tools to dissect these processes and extract meaningful predictions. Over the next three chapters, you will build a robust understanding of this topic.

The first chapter, **"Principles and Mechanisms,"** establishes the mathematical foundation. You will learn how to structure an absorbing chain's transition matrix into its canonical form and discover the power of the [fundamental matrix](@entry_id:275638) for calculating expected times and absorption probabilities. The second chapter, **"Applications and Interdisciplinary Connections,"** showcases the remarkable versatility of these models by exploring their use in diverse fields such as economics, [population genetics](@entry_id:146344), web analytics, and [statistical physics](@entry_id:142945). Finally, the third chapter, **"Hands-On Practices,"** allows you to apply your knowledge to solve concrete problems, solidifying your grasp of the concepts and methods discussed.

## Principles and Mechanisms

In the study of Markov chains, a particularly important and widely applicable class of processes are those that contain **absorbing states**. An absorbing state is a state that, once entered, cannot be left. The process is "absorbed" into this state permanently. Such models are ubiquitous in science and engineering, describing phenomena such as a mechanical component failing, a particle being trapped, a subject in an experiment quitting, a gambler going bankrupt, or a population lineage going extinct. This chapter delineates the fundamental principles governing absorbing Markov chains and presents the matrix-based mechanisms for their [quantitative analysis](@entry_id:149547).

### The Structure of Absorbing Chains

Formally, a state $i$ in a Markov chain is an **absorbing state** if the probability of transitioning from state $i$ to itself is 1, i.e., $P_{ii} = 1$. Consequently, for any other state $j \neq i$, $P_{ij} = 0$. A Markov chain is called an **absorbing Markov chain** if it has at least one absorbing state, and from every non-absorbing state, it is possible to reach an [absorbing state](@entry_id:274533) in a finite number of steps. States that are not absorbing are called **transient states**. By definition, a process in a transient state will not remain there forever; it will eventually transition to another state, with some probability path leading to absorption.

To analyze an absorbing chain, the first and most crucial step is to structure its [transition probability matrix](@entry_id:262281), $P$, into a standardized or **canonical form**. This is achieved by reordering the states such that all absorbing states are listed first, followed by all transient states. This partitioning reveals the underlying dynamics of the system.

If there are $r$ absorbing states and $t$ transient states, the reordered transition matrix $P$ can be written in the following [block matrix](@entry_id:148435) form:

$$
P = \begin{pmatrix} I_r & \mathbf{0} \\ R & Q \end{pmatrix}
$$

Here, the components are:
- $I_r$ is the $r \times r$ identity matrix. This block represents the transitions between absorbing states. The ones on the diagonal signify that once the process is in an absorbing state, it stays there.
- $\mathbf{0}$ is an $r \times t$ matrix of zeros. This block represents the (impossible) transitions from an absorbing state to a transient state.
- $R$ is a $t \times r$ matrix of [transition probabilities](@entry_id:158294) from the transient states to the absorbing states. The entry $R_{ij}$ is the one-step probability of moving from transient state $i$ to absorbing state $j$.
- $Q$ is a $t \times t$ matrix of transition probabilities between the transient states. The entry $Q_{ij}$ is the one-step probability of moving from transient state $i$ to transient state $j$.

Let's consider a simplified climate model for a semi-arid region with three states: Normal ($T_1$), Drought-Warning ($T_2$), and Drought ($A_1$). The 'Drought' state is absorbing. The one-step [transition probabilities](@entry_id:158294) are given as follows: from Normal, the system remains Normal with probability 0.7, moves to Drought-Warning with probability 0.2, and enters Drought with probability 0.1. From Drought-Warning, it returns to Normal with probability 0.5, remains in Drought-Warning with probability 0.3, and enters Drought with probability 0.2. Once in Drought, it stays there. [@problem_id:1280263]

To find the [canonical form](@entry_id:140237), we identify the transient states {Normal, Drought-Warning} and the [absorbing state](@entry_id:274533) {Drought}. We reorder the states to (Drought, Normal, Drought-Warning). The corresponding transition matrix is:

$$
P = \begin{pmatrix} 1 & 0 & 0 \\ 0.1 & 0.7 & 0.2 \\ 0.2 & 0.5 & 0.3 \end{pmatrix}
$$

From this [canonical form](@entry_id:140237), we can directly identify the submatrices $Q$ and $R$:

$$
Q = \begin{pmatrix} 0.7 & 0.2 \\ 0.5 & 0.3 \end{pmatrix}, \quad R = \begin{pmatrix} 0.1 \\ 0.2 \end{pmatrix}
$$

The matrix $Q$ encapsulates all the dynamics of the system *before* absorption, and it is the key to answering most quantitative questions about the process.

### The Fundamental Matrix and Expected Visits

A central property of an absorbing chain is that absorption is inevitable. A process starting in any transient state will eventually reach an absorbing state with probability 1. This has a profound implication for the matrix $Q$. The entry $(Q^k)_{ij}$ gives the probability of moving from transient state $i$ to transient state $j$ in exactly $k$ steps, while remaining within the set of transient states. As $k \to \infty$, the probability of not being absorbed must go to zero. This means that every entry of $Q^k$ must approach zero as $k$ becomes large:

$$
\lim_{k \to \infty} Q^k = \mathbf{0}
$$

This mathematical property is equivalent to stating that the **spectral radius** of $Q$, denoted $\rho(Q)$, is strictly less than 1. The [spectral radius](@entry_id:138984) is the maximum absolute value of the eigenvalues of $Q$. Since all eigenvalues $\lambda$ of $Q$ satisfy $|\lambda|  1$, it is impossible for 1 to be an eigenvalue of $Q$. This guarantees that the matrix $(I - Q)$ has a non-zero determinant and is therefore invertible. [@problem_id:1280294]

The inverse of this matrix is of paramount importance and is called the **[fundamental matrix](@entry_id:275638)**, denoted by $N$:

$$
N = (I - Q)^{-1}
$$

The invertibility of $(I - Q)$ allows for the use of the [geometric series](@entry_id:158490) expansion for matrices:

$$
N = (I - Q)^{-1} = \sum_{k=0}^{\infty} Q^k = I + Q + Q^2 + Q^3 + \dots
$$

This expansion provides a powerful interpretation for the entries of $N$. Let's consider the entry $N_{ij}$. It is the sum of probabilities of being at state $j$ after $k$ steps, starting from $i$, for all $k \ge 0$. This sum is precisely the **expected number of times the process is in transient state $j$, given that it started in transient state $i$**. Note that this includes the initial step if $i=j$ (from the $I$ term in the series).

For instance, imagine a badger whose movement is tracked between two foraging territories ($T_1, T_2$) before it gets caught in a trap in a third territory ($A_1$). We might ask for the expected number of days the badger spends in Territory 1, given it starts in Territory 2. [@problem_id:1280265] This value corresponds directly to the entry $N_{21}$ of the [fundamental matrix](@entry_id:275638) for this system. Similarly, in a model of a Mars rover with operational states {Exploring, Communicating, Hibernating} and an absorbing 'Failure' state, the [fundamental matrix](@entry_id:275638) $N$ would provide the expected number of Martian sols the rover spends in each operational mode before the mission ends. [@problem_id:1280274]

### Expected Time to Absorption

One of the most practical questions is to determine the expected time until the process is absorbed. This is often referred to as the **[expected lifetime](@entry_id:274924)** or **mean time to failure**. We can calculate this directly from the [fundamental matrix](@entry_id:275638) $N$.

Let $t_i$ be the expected number of steps until absorption, given the process starts in transient state $i$. This total time is simply the sum of the expected number of times the process spends in *each* of the transient states before absorption. Therefore, $t_i$ is the sum of the entries in the $i$-th row of the [fundamental matrix](@entry_id:275638) $N$:

$$
t_i = \sum_{j=1}^{t} N_{ij}
$$

If we represent the expected absorption times as a column vector $\mathbf{t} = (t_1, t_2, \dots, t_t)^T$, this relationship can be expressed compactly as:

$$
\mathbf{t} = N\mathbf{1}
$$

where $\mathbf{1}$ is a column vector of ones of the appropriate dimension.

Consider a [critical power](@entry_id:176871) grid component that can be 'Functioning' ($T_1$), 'Standby' ($T_2$), or 'Failed' ($A_1$). The 'Failed' state is absorbing. [@problem_id:1280281] The transient submatrix $Q$ for the states {Functioning, Standby} might be $Q = \begin{pmatrix} 0.8  0.15 \\ 0.6  0.3 \end{pmatrix}$. To find the expected number of operational cycles until failure, we first compute the [fundamental matrix](@entry_id:275638) $N$:

$$
I - Q = \begin{pmatrix} 1  0 \\ 0  1 \end{pmatrix} - \begin{pmatrix} 0.8  0.15 \\ 0.6  0.3 \end{pmatrix} = \begin{pmatrix} 0.2  -0.15 \\ -0.6  0.7 \end{pmatrix}
$$

$$
N = (I - Q)^{-1} = \frac{1}{(0.2)(0.7) - (-0.15)(-0.6)} \begin{pmatrix} 0.7  0.15 \\ 0.6  0.2 \end{pmatrix} = \frac{1}{0.05} \begin{pmatrix} 0.7  0.15 \\ 0.6  0.2 \end{pmatrix} = \begin{pmatrix} 14  3 \\ 12  4 \end{pmatrix}
$$

The expected number of cycles until failure, starting from the 'Functioning' state ($T_1$), is the sum of the first row of $N$: $t_1 = 14 + 3 = 17$. The interpretation is that, on average, a component starting in the 'Functioning' state will spend 14 cycles 'Functioning' and 3 cycles on 'Standby' before it fails. Similarly, starting from 'Standby' ($T_2$), the [expected lifetime](@entry_id:274924) is $t_2 = 12 + 4 = 16$ cycles.

This matrix method is powerful, but these expected times can also be found using **first-step analysis**. For each transient state $i$, we can write a linear equation for the expected [time to absorption](@entry_id:266543) $t_i$: $t_i = 1 + \sum_{j} P_{ij} t_j$. The '1' represents the first step taken, and the sum is the expected future time from the next state. For a participant in a psychology experiment who can be 'learning' or 'distracted' before 'quitting', this method yields a [system of linear equations](@entry_id:140416) for the expected number of trials before quitting, providing an alternative to [matrix inversion](@entry_id:636005). [@problem_id:1280270]

### Absorption Probabilities

Beyond knowing *how long* a process will last, we often need to know *where* it will end. If there are multiple absorbing states, what is the probability of ending up in each one?

Let $B$ be a $t \times r$ matrix where the entry $B_{ij}$ is the probability that the process, starting in transient state $i$, is eventually absorbed in absorbing state $j$. This matrix $B$ can be calculated with a remarkably elegant formula involving the [fundamental matrix](@entry_id:275638) $N$ and the transient-to-absorbing transition matrix $R$:

$$
B = NR
$$

The reasoning behind this formula is intuitive. Consider the probability of being absorbed into state $j$ starting from state $i$. The process can transition from $i$ to $j$ in one step (with probability found in $R$), or it can move to another transient state $k$ (with probability in $Q$) and then eventually be absorbed in $j$ from there. Summing over all possible paths and numbers of intermediate steps leads to the formula. The term $(Q^k R)_{ij}$ represents the probability of being absorbed in state $j$ at step $k+1$, having started in state $i$. Summing over all possible steps $k=0, 1, 2, \dots$ gives the total probability: $\sum_{k=0}^{\infty} Q^k R = (\sum_{k=0}^{\infty} Q^k) R = NR$. [@problem_id:1280279]

For example, if a piece of machinery can be 'Operational' or 'Under Maintenance' (transient) before being either 'Decommissioned' or 'Sold' (absorbing), the matrix $B=NR$ will tell us the ultimate fate of the equipment. The entry $B_{12}$ would be the probability that an initially 'Operational' machine is eventually 'Sold'. [@problem_id:1280279]

As with expected times, absorption probabilities can also be found using first-step analysis. Let $b_{i,j}$ be the probability of absorption in state $j$ starting from transient state $i$. We can set up a system of linear equations:

$$
b_{i,j} = \sum_{k \in \text{transient}} P_{ik} b_{k,j} + \sum_{l \in \text{absorbing}} P_{il} \delta_{lj}
$$

where $\delta_{lj}$ is 1 if $l=j$ and 0 otherwise. This reflects that absorption in $j$ can happen either in the next step (the second term) or after further transitions among transient states (the first term). Solving this system is often practical for smaller models, such as determining whether an AI agent will 'Solve' a puzzle or get 'Stuck' [@problem_id:1280284], or whether an individual hearing a rumor will become a 'Confirmed Believer' or 'Confirmed Disbeliever'. [@problem_id:1280288]

### Applications to Rewards and Costs

The framework of [absorbing chains](@entry_id:144693) can be extended to analyze systems where different outcomes carry different values, rewards, or costs. Suppose that upon entering [absorbing state](@entry_id:274533) $A_j$, a reward of $V_j$ is obtained. Since the path to absorption is a random process, the final reward is a random variable. We can use the tools developed to calculate its statistical properties, such as its [expectation and variance](@entry_id:199481).

For a process starting in transient state $T_i$, the probability of receiving reward $V_j$ is precisely the [absorption probability](@entry_id:265511) $B_{ij}$. The expected reward, $\mathbb{E}[V]$, is then the weighted average of all possible rewards, where the weights are the absorption probabilities:

$$
\mathbb{E}[V | \text{start in } T_i] = \sum_{j=1}^{r} B_{ij} V_j
$$

Similarly, the expected squared reward is:

$$
\mathbb{E}[V^2 | \text{start in } T_i] = \sum_{j=1}^{r} B_{ij} V_j^2
$$

With these two quantities, the variance of the reward can be readily calculated using the standard formula:

$$
\mathrm{Var}(V) = \mathbb{E}[V^2] - (\mathbb{E}[V])^2
$$

Consider a validation process for a software component in a self-driving car. The process involves several transient testing states ('Initial Queue', 'Simulation Test', 'Hardware Review') and can end in one of two absorbing states: 'Certified' (value = 5) or 'Failed' (value = -6). [@problem_id:1280273] To find the variance of the final value for a component starting in the 'Initial Queue', one must first calculate the probabilities of being certified versus failing. Let's say we find these to be $p_{\text{cert}} = 12/23$ and $p_{\text{fail}} = 11/23$.

The expected final value is:
$$
\mathbb{E}[V] = (5) \cdot \frac{12}{23} + (-6) \cdot \frac{11}{23} = \frac{60 - 66}{23} = -\frac{6}{23}
$$

The expected squared value is:
$$
\mathbb{E}[V^2] = (5^2) \cdot \frac{12}{23} + ((-6)^2) \cdot \frac{11}{23} = \frac{25 \cdot 12 + 36 \cdot 11}{23} = \frac{300 + 396}{23} = \frac{696}{23}
$$

Finally, the variance is:
$$
\mathrm{Var}(V) = \frac{696}{23} - \left(-\frac{6}{23}\right)^2 = \frac{696}{23} - \frac{36}{529} = \frac{16008 - 36}{529} = \frac{15972}{529}
$$

This example demonstrates the power of absorbing chain analysis. By structuring the problem correctly, we can move from simple transition rules to a sophisticated understanding of the process's duration, ultimate outcome, and the uncertainty surrounding that outcome.