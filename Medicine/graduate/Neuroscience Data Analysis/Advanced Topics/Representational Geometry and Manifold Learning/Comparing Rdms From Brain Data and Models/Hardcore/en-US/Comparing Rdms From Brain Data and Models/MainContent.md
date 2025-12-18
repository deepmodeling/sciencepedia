## Introduction
How can we forge a quantitative link between the intricate patterns of brain activity, the complex states of computational models, and the subtleties of behavior? This fundamental challenge lies at the heart of modern neuroscience. Representational Similarity Analysis (RSA) offers a powerful and elegant solution, providing a common language to describe and compare the '[representational geometry](@entry_id:1130876)'—the structure of relationships between mental representations—across these disparate domains. By abstracting away from the specific implementation details of individual neurons or model units, RSA allows us to test deep hypotheses about how information is processed and transformed in the mind and brain.

This article provides a comprehensive guide to understanding and applying RSA. It addresses the knowledge gap between theoretical concepts and practical implementation, equipping you with the tools to rigorously compare representations. Across three chapters, you will embark on a journey from first principles to cutting-edge applications. First, the **Principles and Mechanisms** chapter will deconstruct the core components of RSA, explaining how to build Representational Dissimilarity Matrices (RDMs) and the statistical foundations for comparing them. Next, the **Applications and Interdisciplinary Connections** chapter will showcase the versatility of RSA, demonstrating how it is used to test computational theories, link brain to behavior, and map the [spatiotemporal dynamics](@entry_id:201628) of cognition. Finally, the **Hands-On Practices** section provides practical exercises to solidify your understanding of key concepts, such as choosing dissimilarity metrics and performing correct statistical inference. By the end, you will be prepared to use RSA to ask and answer your own questions about the nature of neural representation.

## Principles and Mechanisms

This chapter delves into the principles and mechanisms that underpin Representational Similarity Analysis (RSA). We will systematically unpack the core components of this framework, from the definition and construction of its central data structure—the Representational Dissimilarity Matrix (RDM)—to the statistical methods used for comparing RDMs and interpreting the results. Our focus will be on understanding not only *how* these methods are applied but also *why* they are designed as they are, exploring the theoretical rationale and mathematical properties that make RSA a powerful tool for linking brain, behavior, and computational models.

### Defining the Core Object: The Representational Dissimilarity Matrix

At the heart of RSA lies the **Representational Dissimilarity Matrix (RDM)**. An RDM is a comprehensive summary of the [representational geometry](@entry_id:1130876) within a given system, be it a brain region, a layer of a computational model, or a set of behavioral responses.

Formally, for a set of $n$ experimental conditions or stimuli, the RDM, denoted by $D$, is an $n \times n$ matrix where each entry $D_{ij}$ quantifies the dissimilarity between the system's responses to stimulus $i$ and stimulus $j$. By definition, an RDM has several key properties :

1.  **Hollow:** The dissimilarity of any stimulus's representation to itself is zero. Thus, all diagonal entries are zero: $D_{ii} = 0$.
2.  **Symmetric:** The dissimilarity from stimulus $i$ to $j$ is the same as from $j$ to $i$. Thus, the matrix is symmetric: $D_{ij} = D_{ji}$.
3.  **Non-negative:** Dissimilarity values are non-negative real numbers: $D_{ij} \ge 0$.

It is crucial to distinguish an RDM from a **similarity matrix**, $S$. While both summarize pairwise relationships, a similarity matrix assigns large values to similar pairs. For instance, if similarity is measured by the inner product of response vectors $x_i$ and $x_j$, the resulting matrix $S$ (with entries $S_{ij} = x_i^\top x_j$) is a Gram matrix. Such a matrix is positive semidefinite, and its diagonal entries $S_{ii} = x_i^\top x_i = \|x_i\|^2$ represent the squared norm of each pattern, which are generally non-zero. In contrast, an RDM is not required to be positive semidefinite and is defined by its zero diagonal .

### Constructing RDMs: From Raw Data to Dissimilarities

The first step in any RSA is to obtain the neural response patterns that will be used to compute dissimilarities. In functional Magnetic Resonance Imaging (fMRI), this is a non-trivial estimation problem that is typically addressed using the **General Linear Model (GLM)**.

Consider an fMRI experiment with $K$ distinct stimuli presented across multiple independent runs. The goal is to estimate a single, stable multivoxel pattern vector for each stimulus. A robust GLM approach involves several critical components :

*   **Design Matrix ($X$):** The model must account for the slow nature of the fMRI signal. This is achieved by creating regressors for each stimulus condition, where stimulus onset times are convolved with a canonical **Hemodynamic Response Function (HRF)**.
*   **Nuisance Regressors:** To obtain clean estimates, the GLM must include regressors to capture sources of noise and artifact. Standard [nuisance regressors](@entry_id:1128955) include motion parameters (to account for subject movement), run-wise intercepts (to model baseline shifts between scanning runs), and [high-pass filter](@entry_id:274953) regressors (e.g., a discrete cosine basis set) to remove low-frequency scanner drift.
*   **Estimation:** The noise in fMRI time series is not independent; it is temporally autocorrelated. Assuming independent noise and using Ordinary Least Squares (OLS) is therefore suboptimal. A more accurate approach is to model the temporal noise covariance matrix $C$ and use **Generalized Least Squares (GLS)**. This is often implemented by [pre-whitening](@entry_id:185911) the data and design matrix before applying OLS.

The output of this carefully constructed GLM is a matrix of estimated [regression coefficients](@entry_id:634860), $\hat{\beta}$. Each row of this matrix corresponding to a stimulus regressor can be taken as the estimated neural response pattern for that stimulus—a vector in $\mathbb{R}^V$, where $V$ is the number of voxels. With these patterns in hand, we can proceed to compute the RDM.

### Choosing a Dissimilarity Measure: The Geometry of Representation

The choice of dissimilarity measure is a critical decision that defines the specific geometric properties of the representational space being quantified. Different measures are sensitive to different aspects of the patterns. To make an informed choice, it is useful to understand their mathematical properties, which are formalized by the axioms of a [metric space](@entry_id:145912) .

A function $d(i, j)$ is a **metric** if it satisfies four properties for all patterns $i, j, k$:
1.  **Non-negativity:** $d(i, j) \ge 0$.
2.  **Identity of Indiscernibles:** $d(i, j) = 0$ if and only if $i=j$.
3.  **Symmetry:** $d(i, j) = d(j, i)$.
4.  **Triangle Inequality:** $d(i, k) \le d(i, j) + d(j, k)$.

If a measure satisfies the first three properties but not necessarily the [triangle inequality](@entry_id:143750), it is termed a **semimetric**. Many dissimilarities used in RSA fall into this category.

Let's examine some common choices :

*   **Euclidean Distance ($d_E$):** The familiar straight-line distance between two pattern vectors, $d_E(x_i, x_j) = \|x_i - x_j\|_2$. This is a true metric.
*   **Squared Euclidean Distance ($d_{E^2}$):** $d_{E^2}(x_i, x_j) = \|x_i - x_j\|_2^2$. This measure satisfies non-negativity, identity, and symmetry, but can violate the [triangle inequality](@entry_id:143750). For example, for three points on a line at positions 0, 1, and 2, the squared distances are $d_{E^2}(0,1)=1$, $d_{E^2}(1,2)=1$, and $d_{E^2}(0,2)=4$. Since $4 \not\le 1+1$, the inequality fails. It is thus a semimetric.
*   **Correlation Distance ($d_C$):** Defined as $1 - r$, where $r$ is the Pearson correlation between two pattern vectors. This popular measure is also a semimetric. While it satisfies the first three properties, it can violate the [triangle inequality](@entry_id:143750).
*   **Angular Distance ($d_A$):** The angle between two pattern vectors, computed as $d_A(x_i, x_j) = \arccos(r)$. This corresponds to the great-circle distance between the vectors on the surface of a unit hypersphere and is a true metric.

#### Invariance Properties: What Does a Dissimilarity Measure "See"?

The choice of measure is also guided by its **invariance properties**—that is, the transformations of the pattern space that leave the dissimilarity values unchanged .

*   **Euclidean distance** is invariant to translations (adding a constant vector to all patterns) and rotations/reflections (orthonormal transformations). However, it is sensitive to scaling and shearing of the response space.
*   **Cosine distance** ($1 - \text{cosine similarity}$) is invariant to positive scalar rescaling of the patterns (i.e., changing their length but not direction) and to rotations. It is *not* invariant to translations, which can change the angles between vectors.
*   **Correlation distance** is invariant to shifting and scaling of the components *within* each pattern vector (e.g., adding a constant to all voxels or multiplying all voxels by a constant). It is generally *not* invariant to spatial rotations of the voxel space.

#### Accounting for Noise Structure: The Mahalanobis Distance

A major challenge in analyzing neural data is that the noise is rarely uniform or independent across measurement channels (e.g., voxels). It is often **heteroscedastic** ([unequal variances](@entry_id:895761)) and correlated. In this scenario, Euclidean distance is suboptimal because it treats all dimensions equally, effectively overweighting noisy channels and ignoring their covariance.

The **Mahalanobis distance** provides a principled solution to this problem. The squared Mahalanobis distance is defined as:
$d_M^2(x_i, x_j) = (x_i - x_j)^\top \Sigma^{-1} (x_i - x_j)$

Here, $\Sigma$ is the covariance matrix of the noise. This metric can be understood as the squared Euclidean distance computed in a "whitened" space, where the data has been transformed such that the noise becomes isotropic (identity covariance). The Mahalanobis distance is powerfully invariant to any invertible linear [reparameterization](@entry_id:270587) of the feature space, making it a robust measure of dissimilarity .

In practice, the true patterns and their noise covariance are unknown. A direct calculation of distance on noisy pattern estimates is biased; noise will always increase the average distance. To address this, we use the **cross-validated Mahalanobis distance**, often called **crossnobis**. This involves estimating the pattern difference $(x_i - x_j)$ from two independent partitions of the data (e.g., odd vs. even runs). The dissimilarity is then computed as the product of these two independent estimates, projected onto the whitened space:
$\hat{d}_{\times}(x_i, x_j) = (\hat{\delta}_{ij}^{(1)})^\top \hat{\Sigma}^{-1} \hat{\delta}_{ij}^{(2)}$
where $\hat{\delta}_{ij}^{(k)}$ is the estimated difference from partition $k$. This cross-validated estimator is an unbiased estimate of the true squared Mahalanobis distance. A notable feature is that, due to sampling noise, these estimates can sometimes be negative, meaning this measure fails the non-negativity property and is thus neither a metric nor a semimetric . Nevertheless, its [unbiasedness](@entry_id:902438) makes it a superior choice for statistical inference .

### Comparing Representational Geometries: The Core of RSA

The ultimate goal of RSA is to compare RDMs from different sources, such as a brain region and a computational model. This comparison quantifies the extent to which the two systems share a common representational geometry.

#### Preparing RDMs for Comparison: Vectorization

To compare two RDMs using standard statistical tools like correlation, we must first convert them from square matrices into vectors. Since an RDM is symmetric ($D_{ij} = D_{ji}$) with a constant diagonal of zeros, including all $n^2$ entries would be redundant and statistically inappropriate. It would violate the independence assumption of the correlation test by double-counting each dissimilarity and would artificially inflate the correlation by including pairs of zeros from the diagonals.

The correct procedure is to extract only the unique dissimilarity values. This is achieved by taking all the elements in the strict upper (or lower) triangle of the matrix. This process, which we can denote $\mathrm{vec}_{\mathrm{ut}}(D)$, produces a vector of length $m = \binom{n}{2} = \frac{n(n-1)}{2}$. It is essential that the same consistent ordering (e.g., row-major or column-major) is used to vectorize all RDMs being compared to ensure that the elements of the resulting vectors are properly aligned .

#### Choosing a Comparison Metric: Spearman's Rank Correlation

Once we have our vectorized RDMs, $v^{\mathrm{brain}}$ and $v^{\mathrm{model}}$, we need to choose a method to quantify their relationship. A key insight of RSA is that we may not want to assume a linear relationship between the dissimilarity values from two different systems. For example, the mapping from a model's dissimilarity scale to the brain's dissimilarity scale might be nonlinear but still monotonic (i.e., consistently order-preserving).

For this reason, the standard metric for comparing RDMs is **Spearman's [rank correlation](@entry_id:175511) ($r_s$)**. Spearman's correlation is defined as the Pearson product-moment correlation computed on the rank-transformed data. That is, each value in $v^{\mathrm{brain}}$ and $v^{\mathrm{model}}$ is replaced by its rank within its respective vector. Then, the standard Pearson formula is applied to these ranks:
$r_s = \frac{\sum_{i=1}^{n} (R_i - \overline{R})(S_i - \overline{S})}{\sqrt{\sum_{i=1}^{n} (R_i - \overline{R})^2} \sqrt{\sum_{i=1}^{n} (S_i - \overline{S})^2}}$
where $R_i$ and $S_i$ are the ranks of the corresponding dissimilarities.

By operating on ranks, $r_s$ assesses the strength of the [monotonic relationship](@entry_id:166902) between the two RDMs. It is invariant to any strictly monotonic transformation applied to either RDM, making it robust and perfectly suited for situations where only the ordinal structure of the dissimilarities is considered reliable .

### Statistical Inference and Interpretation

A significant correlation between a brain RDM and a model RDM suggests that the model captures some aspect of the brain's representational structure. However, proper interpretation requires careful statistical consideration of noise and potential confounds.

#### The Impact of Noise: Reliability and the Noise Ceiling

Neural measurements are inherently noisy. This noise attenuates, or weakens, the observed correlation between a brain RDM and a model RDM. The true underlying correlation will always be higher than what is measured. The degree of this attenuation depends on the **reliability** of the measurement. Reliability ($\rho$) is the proportion of a measurement's variance that is attributable to the true, underlying signal, as opposed to noise variance.

Under a simple [additive noise model](@entry_id:197111) ($x = t + \varepsilon$, where $x$ is the observed RDM, $t$ is the true RDM, and $\varepsilon$ is noise), the expected observed correlation between a noisy brain RDM ($x$) and a noiseless model RDM ($m$) is attenuated by the square root of the brain data's reliability, $\rho_b$ :
$\operatorname{Corr}(x,m) = \operatorname{Corr}(t,m) \times \sqrt{\rho_{b}}$

Since the true correlation $\operatorname{Corr}(t,m)$ cannot exceed 1, the observed correlation is bounded by $\sqrt{\rho_{b}}$. This upper bound is known as the **noise ceiling**. It represents the maximum possible correlation any model can achieve, given the noise level in the data. For example, if the reliability of a brain RDM is estimated to be $\rho_b = 0.62$, and a perfect model has a true correlation of $r_{\mathrm{true}}=1$, we would still only expect to observe a correlation of $1 \times \sqrt{0.62} \approx 0.7874$. If an imperfect model has a true correlation of $r_{\mathrm{true}} = 0.83$, the expected observed correlation would be attenuated to $0.83 \times \sqrt{0.62} \approx 0.6535$ .

#### Correcting for Attenuation: Estimating the True Correlation

The attenuation formula can be rearranged to estimate the "true" correlation, corrected for the unreliability of our measurements. Since not only the brain RDM but also the model RDM may be noisy (e.g., if the model is stochastic), we must account for the reliability of both. The full **correction for attenuation** formula is :
$\rho_{true} = \frac{\rho_{observed}}{\sqrt{\rho_{brain} \rho_{model}}}$

Here, $\rho_{true}$ is the estimated correlation between the true, noise-free RDMs. $\rho_{observed}$ is the measured correlation, and $\rho_{brain}$ and $\rho_{model}$ are the reliabilities of the brain and model RDMs, respectively.

Reliability is typically estimated using a **split-half** procedure. The data is split into two independent halves, an RDM is computed for each half, and the correlation between the two resulting RDMs is calculated. This split-half correlation, $r_{half}$, is the reliability of a measurement that is half the size of the full dataset. To estimate the reliability of the full dataset, we use the **Spearman-Brown prophecy formula** for $k=2$ (doubling the length):
$\rho_{full} = \frac{2 r_{half}}{1 + r_{half}}$

For instance, if we observe a brain-model correlation of $r_{\text{obs}} = 0.42$, and estimate the full-data reliabilities to be $\rho_{brain} = 0.734$ (from a split-half correlation of 0.58) and $\rho_{model} = 0.925$ (from a split-half correlation of 0.86), the attenuation-corrected correlation would be $r_{\text{corrected}} = \frac{0.42}{\sqrt{0.734 \times 0.925}} \approx 0.5097$. This value provides a better estimate of the true relationship, disattenuated from measurement error .

#### Controlling for Confounds

A significant brain-model correlation could arise not because the model captures the high-level representation of interest, but because both the brain and the model are sensitive to a simpler, confounding property of the stimuli. Common confounds when using natural images include low-level pixel similarity or shared [spatial frequency](@entry_id:270500) content.

To ensure scientific validity, these confounds must be statistically controlled. The standard approach is to construct an RDM for each potential confound and include it as a nuisance regressor in a **[multiple regression](@entry_id:144007) analysis**. The model is formulated with the vectorized brain RDM as the [dependent variable](@entry_id:143677), and the model and confound RDM(s) as predictors:
$\mathbf{r}_{brain} = \beta_0 + \beta_1 \mathbf{r}_{model} + \beta_2 \mathbf{r}_{confound} + \epsilon$

The coefficient $\beta_1$ then reflects the unique contribution of the model RDM, after any variance shared with the confound RDM has been partialled out .

*   A **pixel similarity RDM** can be constructed by representing each image as a vector of its pixel values and computing pairwise dissimilarities (e.g., [correlation distance](@entry_id:634939)) between these vectors.
*   A **spatial frequency RDM** can be constructed by first computing the 2D Discrete Fourier Transform for each image. The [magnitude spectrum](@entry_id:265125), which captures frequency content, can be summarized into a [feature vector](@entry_id:920515) (e.g., by averaging energy in radial frequency bands). Pairwise dissimilarities are then computed on these feature vectors.

### Broader Context: RSA versus Encoding Models

RSA is one of two dominant frameworks for relating computational models to neural data. The other is **encoding modeling**. It is instructive to compare them to understand their complementary strengths .

*   An **encoding model** attempts to build a predictive mapping from a model's features directly to the responses of individual voxels. Typically, this takes the form of a linear model $Y = XW$, where $Y$ is the $n \times p$ matrix of neural responses (stimuli $\times$ voxels), $X$ is the $n \times k$ matrix of model features, and $W$ is a $k \times p$ weight matrix to be learned. The model's success is evaluated by its ability to predict the activity of held-out voxels.

The choice between RSA and [encoding models](@entry_id:1124422) often depends on the scientific question and properties of the data:

*   **When is RSA more informative?**
    *   **Abstract Geometry:** RSA excels at testing hypotheses about the abstract geometry of representations, abstracting away from the spatial layout of voxels.
    *   **Inter-subject Variability:** Neural patterns can be idiosyncratically mixed across subjects (a phenomenon sometimes modeled as an unknown [orthogonal transformation](@entry_id:155650)). Because many [dissimilarity measures](@entry_id:634100) (like Euclidean and [correlation distance](@entry_id:634939)) are invariant to such transformations, RDMs can be more directly comparable across subjects than voxel-wise encoding weights.
    *   **High-dimensional Data:** In typical fMRI studies where the number of voxels and features is much larger than the number of stimuli ($n \ll k \cdot p$), fitting an encoding model is a severely underdetermined problem that risks overfitting without strong regularization. RSA circumvents this by collapsing the high-dimensional voxel space into an $n \times n$ RDM, making the final statistical test more powerful.

*   **When are [encoding models](@entry_id:1124422) more informative?**
    *   **Spatial Localization:** If the goal is to determine *where* specific features are represented in the brain or to quantify the [variance explained](@entry_id:634306) in each individual voxel, [encoding models](@entry_id:1124422) are the tool of choice. Their output (e.g., weight maps or prediction accuracy maps) is inherently spatial.
    *   **Predictive Power:** Encoding models provide a direct, predictive test of a model. A successful model can generate synthetic brain responses to novel stimuli.

In conclusion, RSA and [encoding models](@entry_id:1124422) are not mutually exclusive but are complementary frameworks. While [encoding models](@entry_id:1124422) ask if a model's features can *predict* individual voxel responses, RSA asks if a model's representational *geometry* is similar to the brain's [representational geometry](@entry_id:1130876). Choosing the appropriate tool depends on the specific hypothesis being tested.