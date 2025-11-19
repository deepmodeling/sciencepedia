## Introduction
Iterative algorithms like the power method are powerful tools for finding a matrix's [dominant eigenvalue](@entry_id:142677), but many problems in science and engineering require knowledge of multiple eigenpairs to fully characterize a system. The central challenge, then, is how to find subdominant eigenvalues after the first has been identified. The answer lies in deflation methods—a class of techniques designed to systematically remove the influence of a known eigenpair from a matrix, thereby revealing the next one. This process allows for the sequential discovery of a system's full spectral properties.

This article provides a comprehensive overview of deflation methods for [eigenvalue problems](@entry_id:142153). You will first explore the core theoretical concepts in **Principles and Mechanisms**, which details the mechanics of Hotelling's deflation for [symmetric matrices](@entry_id:156259) and the more general Wielandt's deflation, along with critical numerical stability considerations. Next, in **Applications and Interdisciplinary Connections**, you will see how these techniques are applied in fields ranging from [computational mechanics](@entry_id:174464) to quantum chemistry and serve as the foundation for advanced algorithms. Finally, **Hands-On Practices** will offer a series of guided exercises to solidify your understanding of how to implement and interpret deflation in practical scenarios.

## Principles and Mechanisms

Iterative algorithms for computing eigenvalues, such as the [power method](@entry_id:148021) and its variants, are exceptionally effective at isolating a single eigenpair of a matrix—typically the one corresponding to the eigenvalue of largest magnitude (the dominant eigenvalue). However, in many scientific and engineering applications, a more complete understanding of a system's behavior requires knowledge of multiple eigenvalues, not just the dominant one. For instance, understanding the [vibrational modes](@entry_id:137888) of a structure or the stability of a dynamical system often depends on subdominant eigenvalues. This raises a fundamental question: how can we extend the power of these iterative methods to find other eigenvalues after the first has been identified?

The answer lies in a class of techniques known as **deflation**. The core principle of deflation is to sequentially modify a matrix to "remove" a known eigenpair, allowing an iterative method to converge to a different eigenpair of the modified system. In essence, once we have found an eigenvalue $\lambda_1$ and its corresponding eigenvector $v_1$, we construct a new, "deflated" matrix whose spectrum is systematically related to that of the original matrix but with $\lambda_1$'s influence nullified.

### Hotelling's Deflation for Symmetric Matrices

For the important class of real [symmetric matrices](@entry_id:156259), the most straightforward deflation technique is **Hotelling's deflation**. A symmetric matrix $A \in \mathbb{R}^{n \times n}$ possesses a full set of $n$ real eigenvalues and a corresponding set of orthonormal eigenvectors. This orthogonality is the key property that makes Hotelling's deflation particularly elegant and easy to analyze.

Suppose we have computed the [dominant eigenvalue](@entry_id:142677) $\lambda_1$ and its corresponding normalized eigenvector $v_1$ (i.e., $v_1^T v_1 = 1$). The Hotelling-deflated matrix, which we will call $A_1$, is constructed via a [rank-one update](@entry_id:137543):

$$ A_1 = A - \lambda_1 v_1 v_1^T $$

Here, the term $v_1 v_1^T$ is an [outer product](@entry_id:201262), which forms an $n \times n$ matrix. This matrix is a [projection operator](@entry_id:143175) that projects any vector onto the one-dimensional subspace spanned by $v_1$. The formula for $A_1$ essentially subtracts the influence of the first eigenpair from the original matrix $A$.

This construction has two fundamental and desirable properties.

First, the deflated matrix $A_1$ maps the eigenvector $v_1$ to the zero vector. We can verify this directly [@problem_id:2165917]:
$$ A_1 v_1 = (A - \lambda_1 v_1 v_1^T) v_1 = A v_1 - \lambda_1 v_1 (v_1^T v_1) $$
Since $A v_1 = \lambda_1 v_1$ and $v_1$ is normalized such that $v_1^T v_1 = 1$, the expression simplifies to:
$$ A_1 v_1 = \lambda_1 v_1 - \lambda_1 v_1 (1) = 0 $$
This confirms that $v_1$ is an eigenvector of $A_1$ with a corresponding eigenvalue of $0$. Thus, the eigenvalue $\lambda_1$ has been "deflated" to zero, and the original eigenvector $v_1$ becomes the eigenvector associated with this new zero eigenvalue [@problem_id:2165908].

Second, and just as importantly, the Hotelling deflation preserves all other eigenpairs of the original [symmetric matrix](@entry_id:143130) $A$. Let $(\lambda_k, v_k)$ be any other eigenpair of $A$, where $k \neq 1$. For a symmetric matrix, eigenvectors corresponding to distinct eigenvalues are orthogonal, so $v_1^T v_k = 0$. Applying $A_1$ to $v_k$ yields [@problem_id:2165907] [@problem_id:2165886]:
$$ A_1 v_k = (A - \lambda_1 v_1 v_1^T) v_k = A v_k - \lambda_1 v_1 (v_1^T v_k) $$
Because of the orthogonality, the second term vanishes:
$$ A_1 v_k = \lambda_k v_k - \lambda_1 v_1 (0) = \lambda_k v_k $$
This remarkable result shows that $v_k$ remains an eigenvector of $A_1$ with its original eigenvalue $\lambda_k$ unchanged. More generally, for any vector $w$ that is orthogonal to $v_1$, the action of $A_1$ is identical to the action of $A$, since $A_1 w = A w - \lambda_1 v_1 (v_1^T w) = A w$ [@problem_id:2165876].

Consequently, if the eigenvalues of $A$ are $\lambda_1, \lambda_2, \dots, \lambda_n$, the eigenvalues of $A_1$ are $0, \lambda_2, \dots, \lambda_n$. If $|\lambda_2| > |\lambda_j|$ for all $j > 2$, then $\lambda_2$ is the [dominant eigenvalue](@entry_id:142677) of $A_1$. We can therefore apply the [power method](@entry_id:148021) to $A_1$ to find $\lambda_2$ and $v_2$. This process can be repeated, constructing $A_2 = A_1 - \lambda_2 v_2 v_2^T$, and so on, to find subsequent eigenvalues sequentially [@problem_id:2165893].

### Wielandt's Deflation for General Matrices

The elegant simplicity of Hotelling's deflation hinges on the orthogonality of eigenvectors, a property not guaranteed for [non-symmetric matrices](@entry_id:153254). For a general matrix $A$, which may have complex eigenvalues or a non-orthogonal set of eigenvectors, a more general approach is required. This is provided by **Wielandt's deflation**.

Let $A$ be a general $n \times n$ matrix, and suppose we have found a right eigenpair $(\lambda_1, v_1)$, where $A v_1 = \lambda_1 v_1$. Wielandt's method also constructs a deflated matrix $B$ via a [rank-one update](@entry_id:137543):

$$ B = A - v_1 c^T $$

Here, $c$ is an auxiliary vector that must be chosen to achieve deflation. To ensure that $v_1$ becomes an eigenvector of $B$ with eigenvalue 0, we require:
$$ B v_1 = A v_1 - v_1 (c^T v_1) = \lambda_1 v_1 - (c^T v_1) v_1 = (\lambda_1 - c^T v_1) v_1 = 0 $$
This implies that the vector $c$ must satisfy the condition $c^T v_1 = \lambda_1$.

Unlike Hotelling's method, the choice of $c$ is not unique. However, a judicious choice is crucial for ensuring that the other eigenvalues of $A$ are preserved in $B$. The optimal choice for $c$ involves the corresponding **left eigenvector** of $A$. A left eigenvector $u_1$ is a row vector (or the [conjugate transpose](@entry_id:147909) of a column vector $u_1$) satisfying $u_1^H A = \lambda_1 u_1^H$. If we choose $c$ to be proportional to $u_1$, such that $c = \alpha u_1$, the condition $c^T v_1 = \lambda_1$ becomes $\alpha (u_1^T v_1) = \lambda_1$, which gives $\alpha = \lambda_1 / (u_1^T v_1)$. The deflated matrix is then:
$$ B = A - \frac{\lambda_1}{u_1^H v_1} v_1 u_1^H $$
(using the conjugate transpose $H$ for generality, which is equivalent to the transpose $T$ for real vectors).

With this specific choice, Wielandt's deflation not only maps $\lambda_1$ to $0$ but also preserves the remaining eigenvalues $\lambda_2, \dots, \lambda_n$. This is due to the [biorthogonality](@entry_id:746831) property of [left and right eigenvectors](@entry_id:173562) corresponding to distinct eigenvalues: if $\lambda_k \neq \lambda_1$, then $u_1^H v_k = 0$. Applying $B$ to another right eigenvector $v_k$ gives:
$$ B v_k = A v_k - \frac{\lambda_1}{u_1^H v_1} v_1 (u_1^H v_k) = \lambda_k v_k - 0 = \lambda_k v_k $$
Thus, as with the symmetric case, the other eigenpairs are preserved. The use of a left eigenvector provides the necessary generalization away from the reliance on symmetry and orthogonality [@problem_id:2165929].

We can even generalize further. If we construct $B = A - \lambda_1 v_1 u^T$ with a vector $u$ such that $u^T v_1 = c$ for some constant $c$, the eigenvalue associated with $v_1$ is not deflated to zero but rather shifted to $(1-c)\lambda_1$, while the other eigenvalues remain unchanged [@problem_id:2165915]. The standard Wielandt deflation is the specific case where one chooses $u$ such that $c=1$, thereby mapping $\lambda_1$ to zero.

### Numerical Considerations and Stability

While deflation methods provide a powerful theoretical framework for finding multiple eigenvalues, their practical implementation in [finite-precision arithmetic](@entry_id:637673) reveals significant challenges related to numerical stability.

A primary concern is the **accumulation of errors**. Each step of a sequential deflation process is imperfect. The computed eigenpair $(\tilde{\lambda}_k, \tilde{v}_k)$ contains small numerical errors from the iterative solver and floating-point arithmetic. When we construct the next deflated matrix, $\tilde{A}_k = \tilde{A}_{k-1} - \tilde{\lambda}_k \tilde{v}_k \tilde{v}_k^T$, these errors are "baked into" the matrix. The subsequent calculation for $(\tilde{\lambda}_{k+1}, \tilde{v}_{k+1})$ is performed on a matrix that is already a perturbation of the ideal one. This process continues, with errors from each step accumulating and propagating to all subsequent steps. As a result, the eigenvalues computed later in the sequence tend to be progressively less accurate than those computed earlier [@problem_id:2165905].

The stability of deflation is particularly sensitive to the **separation of eigenvalues**. If two eigenvalues, $\lambda_1$ and $\lambda_2$, are very close, a small error in the computed eigenvector $\tilde{v}_1$ can lead to a large error in the computed value of $\lambda_2$ after deflation. The [error propagation](@entry_id:136644) is complex, but the effect is particularly pronounced when deflating a large-magnitude eigenvalue to find a much smaller one, as the error can be significantly amplified [@problem_id:2165902]. In essence, when eigenvalues are clustered, it becomes numerically difficult to "peel away" one without disturbing its neighbors.

Finally, a special consideration arises for non-symmetric real matrices. If such a matrix $A$ has a non-real eigenvalue $\lambda$, then its complex conjugate $\bar{\lambda}$ must also be an eigenvalue. A naive attempt to deflate only the single complex eigenvalue $\lambda$ using a standard [rank-one update](@entry_id:137543) (e.g., $B = A - \lambda v u^H / (u^H v)$) will invariably produce a deflated matrix $B$ that has complex-valued entries. This is because $A$ is real, but the update term is generally complex. This is problematic, as it forces the subsequent computations into complex arithmetic, which is more costly and may not be supported by the intended algorithms [@problem_id:2165892]. The correct procedure in this case is to deflate the [complex conjugate pair](@entry_id:150139) $(\lambda, \bar{\lambda})$ simultaneously using a **real-valued rank-two update**, which ensures that the deflated matrix remains entirely real.

In summary, deflation methods are indispensable tools for sequential [eigenvalue computation](@entry_id:145559). However, their application requires careful consideration of the matrix properties (symmetric vs. non-symmetric) and an awareness of the inherent numerical stability issues, particularly the accumulation of errors and sensitivity to [eigenvalue clustering](@entry_id:175991).