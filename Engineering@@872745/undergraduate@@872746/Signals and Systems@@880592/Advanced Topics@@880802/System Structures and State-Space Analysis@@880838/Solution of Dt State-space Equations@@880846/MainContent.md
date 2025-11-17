## Introduction
The [state-space representation](@entry_id:147149) offers a powerful framework for modeling dynamic systems, but its true utility lies in our ability to solve the underlying equations to predict system behavior over time. This article bridges the gap between representing a system and analyzing its complete trajectory, providing a comprehensive guide to solving discrete-time linear time-invariant (LTI) [state-space equations](@entry_id:266994). You will learn to decompose the system's response, analyze its inherent stability, and understand its reaction to external inputs. The first chapter, **Principles and Mechanisms**, will systematically derive the solution by separating it into the zero-input and zero-state responses, introducing the critical role of the [state-transition matrix](@entry_id:269075) and its connection to system eigenvalues. Following this, **Applications and Interdisciplinary Connections** will demonstrate the practical power of these methods in diverse fields such as digital signal processing, control engineering, and economics. Finally, **Hands-On Practices** will provide targeted exercises to solidify your understanding and apply these theoretical concepts to concrete problems, moving from foundational simulation to advanced analysis.

## Principles and Mechanisms

Having established the framework of discrete-time [state-space representation](@entry_id:147149), we now turn our attention to the central task of solving these equations. The solution provides a complete description of the system's trajectory over time, driven by its initial conditions and any external inputs. This chapter will systematically develop the methods for finding this solution, explore its fundamental properties, and connect the mathematical results to the physical behavior of the system, such as stability and oscillation.

### The Total Response: Superposition of Causes

A discrete-time linear time-invariant (LTI) system is described by the state and output equations:
$$
\begin{align}
x[n+1] = A x[n] + B u[n] \\
y[n] = C x[n] + D u[n]
\end{align}
$$
The evolution of the [state vector](@entry_id:154607) $x[n]$ from one time step to the next is influenced by two distinct factors: the current state $x[n]$ and the current input $u[n]$. Due to the principle of **superposition**, a cornerstone of LTI systems, we can analyze the effects of these two factors separately. The [total response](@entry_id:274773) of the system can be expressed as the sum of two components:

1.  **The Zero-Input Response (ZIR):** This is the system's response generated solely by its initial state, $x[0]$, assuming the input is zero for all time ($u[n] = 0$). It represents the natural evolution of the system as its internal energy dissipates or is redistributed. The ZIR [state vector](@entry_id:154607) is denoted as $x_{zi}[n]$.

2.  **The Zero-State Response (ZSR):** This is the system's response driven exclusively by the input signal $u[n]$, assuming the system starts from a state of rest ($x[0] = \mathbf{0}$). It represents the system's reaction to external stimuli. The ZSR state vector is denoted as $x_{zs}[n]$.

The total state response is therefore the sum $x[n] = x_{zi}[n] + x_{zs}[n]$. Consequently, the total output response is also a sum:
$$
\begin{align}
y[n] = C x[n] + D u[n] \\
= C(x_{zi}[n] + x_{zs}[n]) + D u[n] \\
= \underbrace{C x_{zi}[n]}_{\text{Zero-Input Output}} + \underbrace{(C x_{zs}[n] + D u[n])}_{\text{Zero-State Output}} \\
= y_{zi}[n] + y_{zs}[n]
\end{align}
$$
This decomposition is not merely a mathematical convenience; it provides profound insight into system behavior. For instance, in analyzing a control system, we might be interested in how quickly the system returns to equilibrium from a disturbance (a zero-input problem) versus how it tracks a command signal (a zero-state problem) [@problem_id:1753419].

### The Zero-Input Response and the State-Transition Matrix

Let us first analyze the zero-input case, where the system is isolated from external inputs. The state equation simplifies to a homogeneous first-order [difference equation](@entry_id:269892):
$$
x_{zi}[n+1] = A x_{zi}[n]
$$
with a given initial state $x_{zi}[0] = x[0]$. We can solve this equation by simple iteration:
$$
\begin{align}
x_{zi}[1] = A x_{zi}[0] = A x[0] \\
x_{zi}[2] = A x_{zi}[1] = A(A x[0]) = A^2 x[0] \\
x_{zi}[3] = A x_{zi}[2] = A(A^2 x[0]) = A^3 x[0] \\
\vdots
\end{align}
$$
The pattern is clear. The state at any time $n$ is found by repeatedly applying the matrix $A$. The solution to the zero-input problem is:
$$
x_{zi}[n] = A^n x[0]
$$
This equation introduces a matrix of paramount importance: the **[state-transition matrix](@entry_id:269075)**, denoted by $\Phi[n]$. For a discrete-time LTI system, it is defined as:
$$
\Phi[n] = A^n
$$
The [state-transition matrix](@entry_id:269075) $\Phi[n]$ maps the initial state at time $0$ to the state at time $n$. It encapsulates the entire natural dynamics of the system. The $j$-th column of $\Phi[n]$ represents the [state vector](@entry_id:154607) $x[n]$ that results from starting the system with an initial condition where only the $j$-th state variable is unity and all others are zero, i.e., $x[0] = e_j$, where $e_j$ is the $j$-th standard basis vector [@problem_id:1753384].

#### Computing the State-Transition Matrix $A^n$

Calculating the $n$-th power of a matrix is the key to finding the [zero-input response](@entry_id:274925). The method depends on the properties of the matrix $A$.

**Case 1: Diagonalizable Matrix**

If the $N \times N$ matrix $A$ has $N$ [linearly independent](@entry_id:148207) eigenvectors, it is **diagonalizable**. This means it can be written as $A = P D P^{-1}$, where $P$ is the matrix whose columns are the eigenvectors of $A$, and $D$ is the diagonal matrix of corresponding eigenvalues.
$$
P = \begin{pmatrix} |   | \\ v_1  \dots  v_N \\ |   | \end{pmatrix}, \quad D = \begin{pmatrix} \lambda_1   0 \\  \ddots  \\ 0   \lambda_N \end{pmatrix}
$$
The power $A^n$ is then remarkably simple to compute:
$$
A^n = (P D P^{-1})^n = (P D P^{-1})(P D P^{-1})\dots(P D P^{-1}) = P D (P^{-1}P) D \dots D P^{-1} = P D^n P^{-1}
$$
Since $D$ is diagonal, $D^n$ is simply the diagonal matrix of the eigenvalues raised to the $n$-th power:
$$
D^n = \begin{pmatrix} \lambda_1^n   0 \\  \ddots  \\ 0   \lambda_N^n \end{pmatrix}
$$
This method provides a [closed-form expression](@entry_id:267458) for $A^n$ and is fundamental to the analysis of many systems [@problem_id:1753375].

**Case 2: Non-Diagonalizable Matrix (Repeated Eigenvalues)**

If a matrix has [repeated eigenvalues](@entry_id:154579), it may not have a full set of linearly independent eigenvectors. Such a matrix is not diagonalizable. A common example is an [upper-triangular matrix](@entry_id:150931) with identical diagonal entries. Consider the matrix:
$$
A = \begin{pmatrix} \lambda  \alpha \\ 0  \lambda \end{pmatrix}
$$
This matrix has a repeated eigenvalue $\lambda$, but only one eigenvector (up to scaling). To find $A^n$, we can decompose $A$ into a diagonal part and a **nilpotent** part (a matrix $N$ for which $N^k = \mathbf{0}$ for some integer $k$).
$$
A = \begin{pmatrix} \lambda  0 \\ 0  \lambda \end{pmatrix} + \begin{pmatrix} 0  \alpha \\ 0  0 \end{pmatrix} = \lambda I + N
$$
Since the identity matrix $I$ commutes with any matrix ($\lambda I \cdot N = N \cdot \lambda I$), we can use the [binomial theorem](@entry_id:276665):
$$
A^n = (\lambda I + N)^n = \sum_{k=0}^{n} \binom{n}{k} (\lambda I)^{n-k} N^k = \sum_{k=0}^{n} \binom{n}{k} \lambda^{n-k} N^k
$$
For our specific $N$, we find $N^2 = \begin{pmatrix} 0  \alpha \\ 0  0 \end{pmatrix} \begin{pmatrix} 0  \alpha \\ 0  0 \end{pmatrix} = \begin{pmatrix} 0  0 \\ 0  0 \end{pmatrix}$. Thus, all terms in the [binomial expansion](@entry_id:269603) for $k \ge 2$ vanish. The sum truncates to:
$$
A^n = \binom{n}{0} \lambda^n N^0 + \binom{n}{1} \lambda^{n-1} N^1 = 1 \cdot \lambda^n I + n \lambda^{n-1} N
$$
Substituting the matrices for $I$ and $N$ gives the [closed-form solution](@entry_id:270799) [@problem_id:1753355]:
$$
\Phi[n] = A^n = \begin{pmatrix} \lambda^n  n \alpha \lambda^{n-1} \\ 0  \lambda^n \end{pmatrix}
$$
This result is crucial, as it shows that [repeated eigenvalues](@entry_id:154579) can introduce polynomial terms in $n$ (like $n\lambda^{n-1}$) into the system's [natural response](@entry_id:262801).

### Stability and Modal Analysis of the Unforced System

The expression $x[n] = A^n x[0]$ reveals that the long-term behavior of the unforced system is determined entirely by the properties of $A^n$ as $n \to \infty$. This behavior is what we call **stability**.

A system is **asymptotically stable** if, for any initial condition $x[0]$, the state converges to the origin: $\lim_{n\to\infty} x[n] = \mathbf{0}$. A system is **marginally stable** if, for any initial condition, the state remains bounded for all $n$ (i.e., $\|x[n]\| \le M$ for some constant $M$). If the state is unbounded for some initial condition, the system is **unstable**.

The behavior of $A^n$ is governed by the eigenvalues $\lambda_i$ of $A$. For a scalar system $p[n+1] = a p[n]$, the solution is $p[n] = a^n p[0]$. The response remains bounded if and only if $|a| \le 1$. If $|a|  1$, the response decays to zero. If $|a|1$, it grows without bound [@problem_id:1753359].

This concept extends directly to matrix systems. The state $x[n]$ converges to zero if and only if all eigenvalues of $A$ have a magnitude strictly less than 1. The maximum magnitude among all eigenvalues is called the **[spectral radius](@entry_id:138984)**, $\rho(A) = \max_i |\lambda_i|$.
- **Asymptotic Stability:** The system is asymptotically stable if and only if $\rho(A)  1$.
- **Marginal Stability:** The system is marginally stable if $\rho(A) \le 1$, and any eigenvalues with magnitude 1 are [simple roots](@entry_id:197415) of the [minimal polynomial](@entry_id:153598) of A.
- **Instability:** The system is unstable if $\rho(A)  1$ or if there are [repeated eigenvalues](@entry_id:154579) on the unit circle.

The nature of the eigenvalues also dictates the qualitative shape of the response:
- **Real Eigenvalues:** A real eigenvalue $\lambda$ corresponds to a mode that decays or grows monotonically, with its magnitude changing by a factor of $\lambda$ at each step.
- **Complex-Conjugate Eigenvalues:** A pair of complex-conjugate eigenvalues $\lambda = r e^{\pm j\theta}$ corresponds to an oscillatory mode. The magnitude of the oscillation is scaled by $r^n$ at each step, and the oscillation has a period related to the angle $\theta$. If $r  1$, the system exhibits a **[damped oscillation](@entry_id:270584)**, spiraling towards the origin [@problem_id:1753383] [@problem_id:1753382].

This leads to the powerful concept of **[modal decomposition](@entry_id:637725)**. For a [diagonalizable matrix](@entry_id:150100) $A$, any initial state $x[0]$ can be written as a unique [linear combination](@entry_id:155091) of its eigenvectors:
$$
x[0] = c_1 v_1 + c_2 v_2 + \dots + c_N v_N
$$
The [zero-input response](@entry_id:274925) is then:
$$
x[n] = A^n x[0] = A^n (c_1 v_1 + \dots + c_N v_N) = c_1 (A^n v_1) + \dots + c_N (A^n v_N)
$$
Since $v_i$ is an eigenvector, $A v_i = \lambda_i v_i$, which implies $A^n v_i = \lambda_i^n v_i$. Therefore,
$$
x[n] = \underbrace{c_1 \lambda_1^n v_1}_{\text{Mode 1}} + \underbrace{c_2 \lambda_2^n v_2}_{\text{Mode 2}} + \dots + \underbrace{c_N \lambda_N^n v_N}_{\text{Mode N}}
$$
The [total system response](@entry_id:183364) is a superposition of its **natural modes**. Each mode is a vector that maintains its direction (along an eigenvector) while its magnitude scales by $\lambda_i^n$. The rate of decay of a mode is determined entirely by the magnitude of its associated eigenvalue. The mode with the [smallest eigenvalue](@entry_id:177333) magnitude is the fastest-decaying mode [@problem_id:1753396].

### The Zero-State Response: The Convolution Sum

We now turn to the [zero-state response](@entry_id:273280), which describes the system's reaction to an input $u[n]$ when starting from rest, $x[0] = \mathbf{0}$. The governing equation is:
$$
x_{zs}[n+1] = A x_{zs}[n] + B u[n]
$$
Let's find the solution by iterating from $n=0$:
$$
\begin{align}
x_{zs}[0] = \mathbf{0} \\
x_{zs}[1] = A x_{zs}[0] + B u[0] = B u[0] \\
x_{zs}[2] = A x_{zs}[1] + B u[1] = A(B u[0]) + B u[1] = A B u[0] + B u[1] \\
x_{zs}[3] = A x_{zs}[2] + B u[2] = A(A B u[0] + B u[1]) + B u[2] = A^2 B u[0] + A B u[1] + B u[2]
\end{align}
$$
This iterative process provides a direct way to compute the state at any given time step for a known input sequence [@problem_id:1753428].

By observing the pattern, we can derive a general formula for $x_{zs}[n]$. The state at time $n$ is a weighted sum of the effects of all past inputs:
$$
x_{zs}[n] = A^{n-1} B u[0] + A^{n-2} B u[1] + \dots + A B u[n-2] + B u[n-1]
$$
This can be written more compactly as a summation, known as the **[discrete convolution](@entry_id:160939) sum**:
$$
x_{zs}[n] = \sum_{k=0}^{n-1} A^{n-1-k} B u[k]
$$
This formula is the state-space equivalent of the convolution integral or sum seen in input-output analysis. It shows that the state at time $n$ is a superposition of responses to the input at all previous times $k  n$. The term $A^{n-1-k}B$ represents the response of the state at time $n$ to a [unit impulse](@entry_id:272155) applied to the input at time $k$.

### The Complete Solution

By combining the zero-input and zero-state responses, we arrive at the complete solution for the state vector of a discrete-time LTI system:
$$
x[n] = \underbrace{A^n x[0]}_{\text{Zero-Input Response}} + \underbrace{\sum_{k=0}^{n-1} A^{n-1-k} B u[k]}_{\text{Zero-State Response}}
$$
This is one of the most important results in the theory of [linear systems](@entry_id:147850). It explicitly shows how the state at any time $n$ is determined by the initial state $x[0]$ and the entire history of the input $u[k]$ for $0 \le k  n$.

Once the [state vector](@entry_id:154607) $x[n]$ is known, the system output $y[n]$ is found by a simple algebraic substitution into the output equation:
$$
y[n] = C x[n] + D u[n] = C \left( A^n x[0] + \sum_{k=0}^{n-1} A^{n-1-k} B u[k] \right) + D u[n]
$$
This final expression provides a complete characterization of the system's behavior, linking its inputs and initial conditions to its internal states and final outputs [@problem_id:1753420]. Mastering the principles and mechanisms outlined in this chapter is essential for the analysis, design, and control of [discrete-time systems](@entry_id:263935).