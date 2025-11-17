## Introduction
From predicting consumer market shares to ranking webpages and modeling population growth, many real-world systems evolve through a series of probabilistic steps. Markov chains offer a powerful mathematical framework for describing such processes, characterized by a unique "memoryless" property where the future depends only on the present state. While these systems can appear random and unpredictable, the language of linear algebra—specifically state vectors and [stochastic matrices](@entry_id:152441)—provides a surprisingly elegant and effective way to analyze their behavior, forecast future outcomes, and understand their long-term equilibrium.

This article provides a comprehensive introduction to Markov chains through the lens of linear algebra. In the first chapter, **Principles and Mechanisms**, we will define the core components of a Markov chain, including state vectors and transition matrices, and explore how to model a system's short-term evolution and long-term convergence to a steady state. Next, in **Applications and Interdisciplinary Connections**, we will showcase the versatility of this framework by examining its use in diverse fields from network analysis with Google's PageRank to [population biology](@entry_id:153663). Finally, the **Hands-On Practices** section will allow you to apply these concepts to solve concrete problems. Let us begin by establishing the fundamental principles that govern these fascinating systems.

## Principles and Mechanisms

A Markov chain is a mathematical model that describes a sequence of events in which the probability of each event depends only on the state attained in the previous event. This "memoryless" property, known as the Markov property, makes these chains a powerful yet tractable tool for modeling a vast array of real-world systems, from [population dynamics](@entry_id:136352) and economic markets to algorithm behavior and quantum mechanics. In this chapter, we will establish the fundamental principles and mechanisms that govern these systems, using the language of linear algebra.

### Defining the System: States and State Vectors

At the core of any Markov chain is a system that can exist in one of a finite number of distinct conditions, or **states**. For a system with $n$ possible states, we can describe its configuration at any given time step $k$ by a **[state vector](@entry_id:154607)**. A [state vector](@entry_id:154607), denoted $\mathbf{p}_k$, is a column vector in $\mathbb{R}^n$:

$$
\mathbf{p}_k = \begin{pmatrix} p_1 \\ p_2 \\ \vdots \\ p_n \end{pmatrix}
$$

The entries of this vector represent the probability that the system is in each of the $n$ states. For instance, $p_1$ is the probability that the system is in state 1, $p_2$ is the probability that it is in state 2, and so on. Because the entries are probabilities, they must satisfy two fundamental conditions:
1.  **Non-negativity**: $p_i \ge 0$ for all $i=1, 2, \dots, n$.
2.  **Normalization**: The sum of the probabilities must be 1, i.e., $\sum_{i=1}^n p_i = 1$.

A vector that satisfies these two conditions is called a **probability vector**. For example, if a music recommendation algorithm categorizes songs into Pop, Rock, and Electronic, the state of a user's listening session can be described by a 3-entry [state vector](@entry_id:154607) $\mathbf{p}_k = (p_P, p_R, p_E)^T$. If a user is known to be listening to a Rock song at the first step, the initial state vector is $\mathbf{p}_1 = (0, 1, 0)^T$, indicating a 100% probability of being in the "Rock" state [@problem_id:1375574].

### The Engine of Change: Stochastic Matrices

The evolution of a Markov chain from one state to the next is governed by a set of fixed probabilistic rules. These rules are neatly encapsulated in a square matrix known as the **transition matrix**, which we will denote by $T$. If the system is in state $\mathbf{p}_k$ at time step $k$, the state at the next time step, $\mathbf{p}_{k+1}$, is found by a simple [matrix-vector multiplication](@entry_id:140544):

$$
\mathbf{p}_{k+1} = T \mathbf{p}_k
$$

The structure of the transition matrix $T$ is critical. We adopt a common convention where the entry $T_{ij}$ represents the probability that the system transitions *to* state $i$ *from* state $j$. This leads to specific properties that any valid transition matrix must possess.

First, since every entry $T_{ij}$ is a probability, it must be non-negative. A matrix containing negative entries cannot be a transition matrix because a negative probability is a meaningless concept. Consider a model of labor migration between industrial and agricultural sectors. A proposed transition matrix like $P = \begin{pmatrix} 0.95 & 0.15 \\ -0.05 & 0.85 \end{pmatrix}$ is fundamentally invalid. The entry $P_{21} = -0.05$ would imply a -5% chance of moving from the industrial to the agricultural sector, which is physically and probabilistically impossible [@problem_id:1375569]. Thus, for any transition matrix $T$, we must have:

$$
T_{ij} \ge 0 \quad \text{for all } i, j
$$

Second, if the system is in state $j$, it must transition to *some* state in the next time step. The sum of probabilities of transitioning from state $j$ to all possible states $i$ must therefore be 1. Since $T_{ij}$ is the probability of going from $j$ to $i$, summing over all possible destination states $i$ for a fixed starting state $j$ corresponds to summing the entries of the $j$-th column of $T$. This gives us the second condition:

$$
\sum_{i=1}^n T_{ij} = 1 \quad \text{for all } j=1, 2, \dots, n
$$

A square matrix whose entries are all non-negative and whose columns each sum to 1 is known as a **left [stochastic matrix](@entry_id:269622)** or, more commonly, a **column-[stochastic matrix](@entry_id:269622)**. This is the convention we will use throughout this text.

It is worth noting that some authors define $T_{ij}$ as the probability of transitioning from state $i$ to state $j$. In that case, the *rows* of the matrix would sum to 1, and the matrix is called a **row-[stochastic matrix](@entry_id:269622)**. The system's evolution is then typically written with row vectors, $\boldsymbol{\pi}_{k+1} = \boldsymbol{\pi}_k P$. Both conventions describe the same underlying processes, but require careful and consistent application of linear algebraic operations. For instance, to ensure a matrix with an unknown entry $x$ is row-stochastic, one would enforce the condition that each row sums to 1. For a matrix like $P = \begin{pmatrix} 0.7 & 0.1 & 0.2 \\ x & 0.6 & 0.15 \\ 0.25 & 0.25 & 0.5 \end{pmatrix}$, the second row must sum to 1, which implies $x + 0.6 + 0.15 = 1$, yielding $x = 0.25$ [@problem_id:1375559].

### Modeling System Evolution

With the state vector $\mathbf{p}$ and the transition matrix $T$ defined, we can now model the system's dynamics over time.

#### Short-Term Dynamics

The state of the system after a single time step, starting from an initial state $\mathbf{p}_0$, is $\mathbf{p}_1 = T\mathbf{p}_0$. The state after two steps is $\mathbf{p}_2 = T\mathbf{p}_1 = T(T\mathbf{p}_0) = T^2\mathbf{p}_0$. By extension, the [state vector](@entry_id:154607) after $k$ steps is given by:

$$
\mathbf{p}_k = T^k \mathbf{p}_0
$$

This elegant formula demonstrates the power of the [matrix representation](@entry_id:143451): the entire $k$-step evolution of the system is captured by the $k$-th power of the transition matrix.

As an example [@problem_id:1375574], consider a music recommendation system with genres Pop (P), Rock (R), and Electronic (E). Let the transition matrix be $T = \begin{pmatrix} 0.5 & 0.2 & 0.3 \\ 0.3 & 0.6 & 0.1 \\ 0.2 & 0.2 & 0.6 \end{pmatrix}$, where $T_{ij}$ is the probability of the next song being of genre $i$ if the current one is of genre $j$. If a user starts with a Rock song, the initial state is $\mathbf{p}_0 = (0, 1, 0)^T$. The probability distribution for the second song is:

$$
\mathbf{p}_1 = T \mathbf{p}_0 = \begin{pmatrix} 0.5 & 0.2 & 0.3 \\ 0.3 & 0.6 & 0.1 \\ 0.2 & 0.2 & 0.6 \end{pmatrix} \begin{pmatrix} 0 \\ 1 \\ 0 \end{pmatrix} = \begin{pmatrix} 0.2 \\ 0.6 \\ 0.2 \end{pmatrix}
$$

The distribution for the third song is $\mathbf{p}_2 = T \mathbf{p}_1$:

$$
\mathbf{p}_2 = \begin{pmatrix} 0.5 & 0.2 & 0.3 \\ 0.3 & 0.6 & 0.1 \\ 0.2 & 0.2 & 0.6 \end{pmatrix} \begin{pmatrix} 0.2 \\ 0.6 \\ 0.2 \end{pmatrix} = \begin{pmatrix} 0.5(0.2)+0.2(0.6)+0.3(0.2) \\ 0.3(0.2)+0.6(0.6)+0.1(0.2) \\ 0.2(0.2)+0.2(0.6)+0.6(0.2) \end{pmatrix} = \begin{pmatrix} 0.28 \\ 0.44 \\ 0.28 \end{pmatrix} = \begin{pmatrix} 7/25 \\ 11/25 \\ 7/25 \end{pmatrix}
$$

Thus, after starting with a Rock song, there is a 28% chance the third song is Pop, a 44% chance it is Rock, and a 28% chance it is Electronic.

#### Probabilistic Interpretation of $T^k$

The equation $\mathbf{p}_k = T^k \mathbf{p}_0$ also provides a profound interpretation of the entries of the matrix power $T^k$. The entry $(T^k)_{ij}$ is the probability that the system will be in state $i$ after exactly $k$ steps, given that it started in state $j$.

For instance, consider a CPU with three power states: Active ($S_1$), Idle ($S_2$), and Sleep ($S_3$), governed by a transition matrix $T$ [@problem_id:1375589]. To find the probability that a CPU starting in the Active state ($S_1$) will be in the Idle state ($S_2$) after exactly three time steps, we need to calculate the entry $(T^3)_{21}$. This is the entry in the second row and first column of the matrix $T^3$. This calculation, while potentially tedious by hand, directly answers the question about the multi-step [transition probability](@entry_id:271680).

### The Long-Term View: Steady States and Equilibrium

One of the most important questions in the study of Markov chains is about the long-term behavior of the system. Does the state vector $\mathbf{p}_k$ settle down as $k \to \infty$? For many systems, the answer is yes: $\mathbf{p}_k$ converges to a specific probability vector known as the **[steady-state vector](@entry_id:149079)** or **equilibrium vector**, which we denote $\mathbf{p}_{\infty}$.

This equilibrium vector has the defining property that it is unchanged by the application of the transition matrix:

$$
T \mathbf{p}_{\infty} = \mathbf{p}_{\infty}
$$

This equation reveals a deep connection to the concepts of [eigenvalues and eigenvectors](@entry_id:138808). A [steady-state vector](@entry_id:149079) is simply an eigenvector of the transition matrix $T$ corresponding to an eigenvalue $\lambda = 1$.

A fundamental theorem of Markov chains states that every [stochastic matrix](@entry_id:269622) has an eigenvalue of $\lambda=1$. We can prove this by showing that the matrix $(T-I)$ is singular. For a column-[stochastic matrix](@entry_id:269622) $T$, the sum of the entries in each column is 1. Consider the matrix $T-I$. The sum of the entries in any column $j$ is $(\sum_{i=1}^n T_{ij}) - 1 = 1 - 1 = 0$. This means that the sum of all row vectors of $T-I$ results in a [zero vector](@entry_id:156189). Consequently, the rows of $T-I$ are linearly dependent, which guarantees that the matrix is singular and its determinant is zero. A singular matrix $(T-I)$ implies, by definition, that there exists a non-zero vector $\mathbf{p}$ such that $(T-I)\mathbf{p} = \mathbf{0}$, or $T\mathbf{p}=\mathbf{p}$. This confirms that $\lambda=1$ is always an eigenvalue [@problem_id:1375590]. The corresponding eigenvector(s), when normalized to be a probability vector, constitute the [steady-state distribution](@entry_id:152877)(s).

#### Calculating the Steady State

To find the [steady-state vector](@entry_id:149079) $\mathbf{p}_{\infty}$, we solve the [system of linear equations](@entry_id:140416) $(T-I)\mathbf{p} = \mathbf{0}$, subject to the constraint that the entries of $\mathbf{p}$ sum to 1.

Let's take a simple model of two web browsers, QuantumLeap (Q) and NexusFlow (N) [@problem_id:1375564]. Suppose 85% of Q users stay and 15% switch to N, while 70% of N users stay and 30% switch to Q. The column-stochastic transition matrix is:
$$
T = \begin{pmatrix} 0.85 & 0.30 \\ 0.15 & 0.70 \end{pmatrix}
$$
We seek a vector $\mathbf{p} = (q, n)^T$ such that $T\mathbf{p} = \mathbf{p}$ and $q+n=1$. The equation $T\mathbf{p} = \mathbf{p}$ gives:
$$
\begin{cases} 0.85q + 0.30n = q \\ 0.15q + 0.70n = n \end{cases} \implies \begin{cases} 0.30n = 0.15q \\ 0.15q = 0.30n \end{cases}
$$
Both equations simplify to $q = 2n$. Combining this with the [normalization condition](@entry_id:156486) $q+n=1$, we get $2n+n=1$, which yields $n=1/3$. Consequently, $q=2/3$. The long-term equilibrium is a market share of $2/3$ for QuantumLeap and $1/3$ for NexusFlow. The [steady-state vector](@entry_id:149079) is $\mathbf{p}_{\infty} = (2/3, 1/3)^T$.

#### Convergence to Equilibrium

For a large class of Markov chains, the system will converge to a unique [steady-state vector](@entry_id:149079) regardless of the initial state $\mathbf{p}_0$. Such chains are called **regular**. A [stochastic matrix](@entry_id:269622) $T$ is regular if some power $T^k$ contains only strictly positive entries. This condition ensures that it is possible to get from any state to any other state (irreducibility) and that the chain does not get stuck in deterministic cycles ([aperiodicity](@entry_id:275873)).

When a chain is regular, the limit $\lim_{k\to\infty} T^k$ exists and is a matrix $L$ whose columns are all identical and equal to the unique [steady-state vector](@entry_id:149079) $\mathbf{p}_{\infty}$. This means that for any initial state $\mathbf{p}_0$, the long-term state is:
$$
\lim_{k\to\infty} \mathbf{p}_k = \lim_{k\to\infty} T^k \mathbf{p}_0 = L \mathbf{p}_0 = \mathbf{p}_{\infty} \left(\sum p_i\right) = \mathbf{p}_{\infty}
$$
The system's "memory" of its initial state fades completely over time. We can even quantify the rate of this convergence by examining the distance between a [state vector](@entry_id:154607) $\mathbf{p}_k$ and the final equilibrium $\mathbf{p}_{\infty}$ [@problem_id:1375568].

### A Deeper Look at Chain Structure: Periodicity and Absorption

Not all Markov chains are regular, and their long-term behavior can be more complex. The structure of the chain, often visualized as a directed graph where nodes are states and edges are transitions, determines its long-term properties.

#### Periodic Chains

Some irreducible chains do not converge to a single steady state but instead cycle through a sequence of distributions. This behavior is characterized by the **period** of the chain. The period of a state is the [greatest common divisor](@entry_id:142947) (GCD) of all possible numbers of steps it takes to return to that state. In an [irreducible chain](@entry_id:267961), all states have the same period.

Consider an AI assistant that cycles through states `Idle` ($S_1$), `Parsing` ($S_2, S_3$), and `Action` ($S_4, S_5$) [@problem_id:1375579]. If the transitions are strictly structured such that from an `Idle` state it must go to a `Parsing` state, from `Parsing` to `Action`, and from `Action` back to `Idle`, the system follows a cyclic pattern.
A path from `Idle` back to `Idle` might be $S_1 \to S_2 \to S_4 \to S_1$. This takes 3 steps. Any path that returns to $S_1$ must complete an integer number of full laps around this cycle of state-sets. Therefore, the number of steps for any return to $S_1$ must be a multiple of 3. The GCD of all possible return times is 3, so the chain has a period of 3. For such a chain, $T^k$ does not converge as $k \to \infty$. Instead, the sequence $T, T^2, T^3, T^4, \dots$ will exhibit a repeating pattern.

#### Absorbing Chains

Another important class of non-regular chains are **[absorbing chains](@entry_id:144693)**. An **absorbing state** is a state that, once entered, can never be left. In the transition matrix $T$, state $i$ is absorbing if $T_{ii}=1$. Consequently, all other entries in that column, $T_{ji}$ for $j \neq i$, must be 0.

A classic example is a board game with "win" or "lose" squares that end the game [@problem_id:1375581]. If a player lands on the "Finish" square $S_5$ or a "Trap" square $S_3$, the game stops. These are [absorbing states](@entry_id:161036). Once the system enters $S_3$ or $S_5$, it remains there for all future time steps. The other states, from which it is possible to move, are called **transient states**. For an absorbing chain, the primary long-term question is not about a [dynamic equilibrium](@entry_id:136767), but rather: what is the probability that the system will eventually end up in each of the different [absorbing states](@entry_id:161036), given its starting state? This involves a different set of analytical tools, which build upon the principles established here.