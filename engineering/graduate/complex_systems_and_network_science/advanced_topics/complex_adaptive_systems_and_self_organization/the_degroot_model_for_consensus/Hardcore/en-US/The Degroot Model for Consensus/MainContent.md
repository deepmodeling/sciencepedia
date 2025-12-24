## Introduction
How do diverse opinions within a group converge into a single, collective agreement? From social networks to teams of autonomous robots, the emergence of consensus from local interactions is a fundamental phenomenon. The DeGroot model provides a simple yet powerful mathematical framework for understanding this process. It addresses the core question of how individual beliefs, when repeatedly averaged among neighbors, evolve over time. This article will unpack the DeGroot model, providing a comprehensive overview for graduate-level students in complex systems and network science.

Across the following chapters, you will gain a deep understanding of this foundational model. The first chapter, **"Principles and Mechanisms,"** dissects the linear update rule, the role of the influence matrix, and the precise mathematical conditions—both spectral and graph-theoretic—that guarantee consensus. Building on this foundation, the second chapter, **"Applications and Interdisciplinary Connections,"** explores how the model illuminates real-world phenomena in sociology, political science, and network engineering, from the spread of beliefs to the design of robust [multi-agent systems](@entry_id:170312). Finally, **"Hands-On Practices"** will solidify your knowledge by guiding you through practical problems that connect the model's theory to concrete calculations of consensus outcomes and agent influence.

## Principles and Mechanisms

The DeGroot model provides a foundational framework for understanding how a group of interacting agents can reach a collective agreement, or **consensus**. This process is governed by a simple yet powerful linear update rule, the properties of which determine whether, to what value, and how quickly opinions will converge. In this chapter, we dissect the core principles and mathematical mechanisms that underpin these dynamics.

### The Linear Averaging Update Rule

The DeGroot model describes the evolution of a set of $n$ scalar opinions, collected in an opinion vector $x(t) \in \mathbb{R}^n$ at [discrete time](@entry_id:637509) steps $t = 0, 1, 2, \dots$. The central mechanism is a linear update rule:

$x(t+1) = W x(t).$

Here, $W \in \mathbb{R}^{n \times n}$ is a non-negative matrix, often called the **influence matrix** or **weight matrix**. The entry $w_{ij}$ represents the weight or influence that agent $j$'s opinion at time $t$, $x_j(t)$, has on agent $i$'s opinion at time $t+1$, $x_i(t+1)$. The update for a single agent $i$ is thus a [linear combination](@entry_id:155091) of all opinions in the network at the previous time step:

$x_i(t+1) = \sum_{j=1}^{n} w_{ij} x_j(t).$

For this process to be interpreted as a social averaging dynamic, we impose a crucial constraint on $W$. We require that each agent's new opinion is a **convex combination** of the existing opinions. A convex combination is a weighted average where the weights are non-negative and sum to one. Since the entries of $W$ are already assumed to be non-negative ($w_{ij} \ge 0$), this requires that the weights each agent $i$ applies must sum to unity. This leads to the defining property of the influence matrix in the DeGroot model .

A matrix $W$ is **row-stochastic** if all its entries are non-negative and the sum of the entries in each row is equal to 1. That is, for all $i \in \{1, \dots, n\}$:

$\sum_{j=1}^{n} w_{ij} = 1.$

This condition ensures that the [opinion dynamics](@entry_id:137597) are self-contained; no "opinion" is created or destroyed, but rather redistributed and averaged among the agents. In vector notation, the row-stochastic property is equivalent to the condition $W\mathbf{1} = \mathbf{1}$, where $\mathbf{1}$ is the column vector of all ones. This reveals that $\lambda=1$ is always an eigenvalue of a [row-stochastic matrix](@entry_id:1131129), with $\mathbf{1}$ as a corresponding right eigenvector.

It is instructive to contrast this with related properties. A matrix is **column-stochastic** if its non-negative entries in each column sum to 1 ($\sum_{i=1}^{n} w_{ij} = 1$ for all $j$), which can be written as $\mathbf{1}^\top W = \mathbf{1}^\top$. A matrix that is both row-stochastic and column-stochastic is called **doubly stochastic**. While row-stochasticity is fundamental to the DeGroot model's averaging interpretation, the other properties have important implications for conservation laws within the system .

### Conservation Laws and Average Consensus

A natural question to ask is whether any aggregate quantity of the system remains constant over time. Consider the [arithmetic mean](@entry_id:165355) of all opinions, $\bar{x}(t) = \frac{1}{n} \sum_{i=1}^{n} x_i(t) = \frac{1}{n}\mathbf{1}^\top x(t)$. Let us examine how this quantity evolves:

$\bar{x}(t+1) = \frac{1}{n}\mathbf{1}^\top x(t+1) = \frac{1}{n}\mathbf{1}^\top (W x(t)) = \frac{1}{n}(\mathbf{1}^\top W) x(t).$

For the mean to be preserved, i.e., $\bar{x}(t+1) = \bar{x}(t)$, we require that $\frac{1}{n}(\mathbf{1}^\top W) x(t) = \frac{1}{n}\mathbf{1}^\top x(t)$. Since this must hold for any arbitrary opinion vector $x(t)$, the condition simplifies to $\mathbf{1}^\top W = \mathbf{1}^\top$. This is precisely the definition of a **column-stochastic** matrix.

Therefore, the arithmetic mean of opinions is a conserved quantity if and only if the influence matrix $W$ is column-stochastic. Since the DeGroot model requires $W$ to be row-stochastic, the mean is conserved if and only if $W$ is **doubly stochastic** . If such a system reaches consensus, the final opinion must be equal to the initial average, $c = \bar{x}(0)$. This special case is known as **average consensus**.

### Conditions for Reaching Consensus

The primary goal of the DeGroot process is for all agents to reach a consensus. Formally, we say that **consensus** is reached if for any initial opinion vector $x(0)$, the system evolves such that all opinions converge to the same value:

$\lim_{t\to\infty} x_i(t) = c \quad \text{for all } i \in \{1, \dots, n\}.$

This is equivalent to the condition $\lim_{t\to\infty} x(t) = c\mathbf{1}$. Since $x(t) = W^t x(0)$, this requires that the limit of the [matrix powers](@entry_id:264766), $W^\infty = \lim_{t\to\infty} W^t$, exists and is a [rank-one matrix](@entry_id:199014) whose columns are all proportional to $\mathbf{1}$. Such a matrix can be written as $W^\infty = \mathbf{1}\pi^\top$ for some vector $\pi \in \mathbb{R}^n$ . The convergence of the system to a single consensus state depends critically on the spectral and structural properties of the influence matrix $W$.

#### The Spectral Perspective

The long-term behavior of the system is determined by the eigenvalues of $W$. For the limit $W^\infty = \lim_{t\to\infty} W^t$ to exist and result in consensus for any starting condition, two spectral conditions must be met :

1.  **Dominance of the Consensus Eigenvalue:** The eigenvalue $\lambda=1$ must be strictly dominant in magnitude over all other eigenvalues. That is, for any other eigenvalue $\lambda_k \neq 1$, it must be that $|\lambda_k|  1$.
2.  **Simplicity of the Consensus Eigenspace:** The eigenvalue $\lambda=1$ must have an [algebraic multiplicity](@entry_id:154240) of one.

If there were another eigenvalue $\lambda_k$ on the unit circle ($|\lambda_k|=1, \lambda_k \neq 1$), the term $\lambda_k^t$ would oscillate indefinitely, preventing convergence. If the [algebraic multiplicity](@entry_id:154240) of $\lambda=1$ were greater than its [geometric multiplicity](@entry_id:155584), the dynamics would involve terms that grow with $t$, causing divergence. If the [geometric multiplicity](@entry_id:155584) of $\lambda=1$ were greater than one, there would be multiple independent vectors that are fixed points of the dynamics, and the final state would depend on the initial condition in a way that does not guarantee all agents agree.

Therefore, the necessary and [sufficient condition](@entry_id:276242) for global consensus in a time-invariant DeGroot model is that $\lambda=1$ is a simple eigenvalue and all other eigenvalues of $W$ lie strictly inside the [unit disk](@entry_id:172324) in the complex plane.

#### The Graph and Matrix Perspective: Primitivity

While the spectral conditions are precise, they are not always easy to check directly. Fortunately, the **Perron-Frobenius theorem** for non-negative matrices provides a powerful link between the structural properties of $W$ and its spectrum. These properties are often expressed in the language of the directed graph $G(W)$ associated with the matrix $W$, where an edge $j \to i$ exists if $w_{ij} > 0$.

First, for information to be able to spread between all agents, the graph $G(W)$ must be **strongly connected**. This means that for any [ordered pair](@entry_id:148349) of agents $(i, j)$, there is a directed path of influence from $j$ to $i$. The matrix-theoretic equivalent of [strong connectivity](@entry_id:272546) is **irreducibility**. For an irreducible [row-stochastic matrix](@entry_id:1131129) $W$, the Perron-Frobenius theorem guarantees that $\lambda=1$ is a simple eigenvalue and that there exists a unique left eigenvector $\pi$ corresponding to this eigenvalue that has strictly positive entries and can be normalized to be a probability vector ($\sum_i \pi_i = 1$) . This vector $\pi$ is known as the **[stationary distribution](@entry_id:142542)**.

However, [strong connectivity](@entry_id:272546) alone is not sufficient for consensus. A [strongly connected graph](@entry_id:273185) can be **periodic**. For example, consider a set of $n$ agents arranged in a directed cycle, where each agent is influenced only by its immediate predecessor . The influence matrix is a [permutation matrix](@entry_id:136841). The graph is strongly connected, but the opinions will simply rotate around the network, returning to their initial state every $n$ steps. The eigenvalues are the $n$-th [roots of unity](@entry_id:142597), all of which have magnitude 1, violating the spectral condition for consensus.

To guarantee consensus, we need a stronger condition: the matrix $W$ must be **primitive**. A non-negative matrix $W$ is primitive if there exists some integer $k \ge 1$ such that all entries of the matrix power $W^k$ are strictly positive. This means that after $k$ steps, every agent has some influence on every other agent. In graph-theoretic terms, a matrix is primitive if its corresponding graph is both strongly connected and **aperiodic** (the [greatest common divisor](@entry_id:142947) of the lengths of all simple directed cycles is 1) .

The Perron-Frobenius theorem for primitive matrices guarantees that the spectral radius (which is 1 for a [row-stochastic matrix](@entry_id:1131129)) is a simple eigenvalue and all other eigenvalues have a strictly smaller magnitude. This is exactly the spectral condition required for consensus. Therefore, if $W$ is a primitive [row-stochastic matrix](@entry_id:1131129), the DeGroot dynamics are guaranteed to converge to a unique consensus for any initial condition [@problem_id:4308903, @problem_id:4308850].

A simple way to ensure [aperiodicity](@entry_id:275873) in a [strongly connected graph](@entry_id:273185) is to introduce at least one [self-loop](@entry_id:274670) (a cycle of length 1). For instance, in the periodic directed cycle example, if each agent retains an infinitesimally small fraction of their own opinion, the resulting matrix becomes primitive and consensus is restored .

### The Consensus Value and Agent Influence

If the matrix $W$ is primitive, we know consensus is reached. But what is the final opinion value $c$? As noted earlier, convergence implies $\lim_{t\to\infty} W^t = \mathbf{1}\pi^\top$, where $\pi$ is the unique [stationary distribution](@entry_id:142542). The final opinion vector is then:

$x(\infty) = \lim_{t\to\infty} W^t x(0) = (\mathbf{1}\pi^\top) x(0) = \mathbf{1} (\pi^\top x(0)).$

The consensus value $c$ is the [scalar product](@entry_id:175289) $\pi^\top x(0)$:

$c = \pi^\top x(0) = \sum_{i=1}^{n} \pi_i x_i(0).$

This elegant result reveals that the final consensus is a weighted average of the initial opinions. The weights are not uniform but are given by the components of the stationary distribution vector $\pi$. Each component $\pi_i$ can be interpreted as the long-run influence, or **social power**, of agent $i$ on the group's final decision . This value is conserved throughout the process, as $\pi^\top x(t+1) = (\pi^\top W) x(t) = \pi^\top x(t)$.

In the special case where $W$ is doubly stochastic (and primitive), the stationary distribution is uniform: $\pi_i = 1/n$ for all $i$. The consensus value then simplifies to the [arithmetic mean](@entry_id:165355) of the initial opinions, $c = \frac{1}{n}\sum_{i=1}^n x_i(0)$ .

**Example: A Two-Agent System** 

Let's illustrate these concepts with a simple two-agent system. Suppose the influence matrix and initial opinions are:

$W = \begin{pmatrix} 0.6  0.4 \\ 0.3  0.7 \end{pmatrix}, \quad x(0) = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$

The matrix $W$ has all positive entries, so it is primitive. Consensus is guaranteed. To find the consensus value, we first compute the stationary distribution $\pi = (\pi_1, \pi_2)^\top$ by solving $\pi^\top W = \pi^\top$ subject to $\pi_1 + \pi_2 = 1$.

The equation $\pi^\top W = \pi^\top$ gives $0.6\pi_1 + 0.3\pi_2 = \pi_1$, which simplifies to $0.3\pi_2 = 0.4\pi_1$, or $3\pi_2 = 4\pi_1$. Combining this with $\pi_1 + \pi_2 = 1$, we solve to find $\pi_1 = 3/7$ and $\pi_2 = 4/7$. The [stationary distribution](@entry_id:142542) is $\pi = (3/7, 4/7)^\top$.

The consensus value $c$ is then computed as a weighted average of the initial opinions, using $\pi$ as the weights:

$c = \pi^\top x(0) = \frac{3}{7}(2) + \frac{4}{7}(1) = \frac{6}{7} + \frac{4}{7} = \frac{10}{7}.$

Despite agent 1 starting with a higher opinion, agent 2 has slightly more influence in this network ($\pi_2 > \pi_1$), pulling the final consensus closer to its initial opinion.

### The Rate of Convergence

Knowing that the system converges, the next question is how quickly it does so. The [rate of convergence](@entry_id:146534) is determined by how fast the non-consensus part of the opinion vector decays. This is governed by the eigenvalues of $W$ that are not equal to 1. The slowest part of the decay is determined by the eigenvalue with the largest magnitude less than 1.

We define the **Second Largest Eigenvalue Modulus (SLEM)** of $W$ as:

$|\lambda_2| = \max \{ |\lambda| : \lambda \in \text{spec}(W), \lambda \ne 1 \}.$

The **spectral gap** of the matrix is defined as $1 - |\lambda_2|$. According to Gelfand's formula for the spectral radius, the asymptotic [rate of convergence](@entry_id:146534) of $W^t$ to the consensus matrix $\mathbf{1}\pi^\top$ is given by the SLEM, independent of the chosen [operator norm](@entry_id:146227) :

$\limsup_{t \to \infty} \big\| W^t - \mathbf{1}\pi^{\top} \big\|^{1/t} = |\lambda_2|.$

This means that for large $t$, the distance to consensus decreases roughly by a factor of $|\lambda_2|$ at each step. A smaller SLEM (and thus a larger [spectral gap](@entry_id:144877)) implies faster convergence. The design of networks and weighting schemes that maximize this [spectral gap](@entry_id:144877) is a central problem in the study of fast consensus. For instance, for the perturbed [cycle graph](@entry_id:273723) with matrix $W_{\varepsilon} = (1-\varepsilon)W + \varepsilon I$, the SLEM can be calculated as $|\lambda_2| = \sqrt{1 - 4\varepsilon(1-\varepsilon)\sin^2(\pi/n)}$, showing explicitly how the convergence rate depends on the network size $n$ and the perturbation parameter $\varepsilon$ .

### Extension to Time-Varying Networks

The classic DeGroot model assumes a static influence network. However, in many real-world systems, relationships and influences change over time. This can be modeled with a time-varying influence matrix, $W(t)$:

$x(t+1) = W(t)x(t).$

In this case, the conditions for consensus become more complex, as there is no single set of eigenvalues to analyze. The system's convergence depends on the properties of the entire sequence of matrices $\{W(t)\}$. A well-known set of [sufficient conditions](@entry_id:269617) for consensus in this time-varying setting requires that influence is both persistent and non-vanishing :

1.  **Uniform Row-Stochasticity:** Each matrix $W(t)$ is row-stochastic.
2.  **Uniform Self-Confidence:** There is a constant $\alpha > 0$ such that all agents maintain a minimum level of self-confidence at all times, i.e., $w_{ii}(t) \ge \alpha$ for all $i$ and $t$. This also ensures [aperiodicity](@entry_id:275873) at every step.
3.  **Uniform Joint Connectivity:** There exists an integer $B \ge 1$ such that for any time $t_0$, the union of the interaction graphs over the interval $[t_0, t_0+B-1]$ is strongly connected (or, more weakly, contains a spanning tree). This ensures that information is continually mixed across the entire network over bounded time intervals.

Under these conditions, it can be shown that the product of influence matrices is contracting, forcing the difference between the maximum and minimum opinions in the network to zero, thereby achieving consensus. This demonstrates the robustness of the consensus-seeking mechanism, extending its applicability beyond static networks to a much broader class of dynamic social and technological systems.