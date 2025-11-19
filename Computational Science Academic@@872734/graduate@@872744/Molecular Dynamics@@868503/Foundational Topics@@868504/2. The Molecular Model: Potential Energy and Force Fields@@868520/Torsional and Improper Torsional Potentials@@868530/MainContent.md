## Introduction
The three-dimensional structure of a molecule is not static. Rotations around single bonds give rise to a multitude of spatial arrangements, or conformations, each with a distinct energy. While bond and angle potentials define a molecule's basic connectivity, they fail to capture the subtle energetic preferences that govern its shape and flexibility. This is the domain of torsional and improper torsional potentials, which are essential components of [classical force fields](@entry_id:747367) that dictate everything from the folding of a protein to the [stereochemistry](@entry_id:166094) of a reaction. This article provides a comprehensive exploration of these crucial energy terms, bridging fundamental theory with practical application in molecular simulation.

The journey begins in **Principles and Mechanisms**, where we will dissect the geometric and mathematical foundations of [dihedral angles](@entry_id:185221). You will learn how proper and improper torsions are defined and how they are modeled using functional forms like Fourier series and harmonic potentials. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these theoretical models are put into practice. We will explore their role in [conformational analysis](@entry_id:177729), their [parameterization](@entry_id:265163) from quantum mechanical data, and their use in advanced simulations of complex biomolecules, connecting classical mechanics to the broader fields of quantum and statistical mechanics. Finally, **Hands-On Practices** will allow you to apply these concepts to solve quantitative problems, solidifying your understanding of how torsional potentials are used to analyze [molecular stability](@entry_id:137744), dynamics, and thermodynamics.

## Principles and Mechanisms

While the previous chapters have established the roles of [bond stretching](@entry_id:172690) and angle bending potentials in defining the basic covalent architecture of a molecule, these terms alone are insufficient to capture the subtle yet crucial energetic variations that govern three-dimensional molecular shape, or conformation. Rotations around single bonds are typically low-energy processes that allow a molecule to explore a vast landscape of different spatial arrangements. The energetic preferences for certain arrangements over others are governed by torsional potentials. Furthermore, the local geometry of specific atomic centers, such as their planarity or [chirality](@entry_id:144105), must be actively maintained. This is the role of improper torsional potentials. This chapter elucidates the fundamental principles behind the geometric definition and mathematical representation of both proper and improper torsions.

### Defining Torsional Coordinates

The foundation of any [torsional potential](@entry_id:756059) is a geometric coordinate that quantifies the rotational state around a bond or the out-of-plane distortion of a center. This coordinate is the dihedral angle. It is essential to distinguish between two types of [dihedral angles](@entry_id:185221) based on the [molecular topology](@entry_id:178654) they describe.

#### Proper and Improper Dihedral Angles

A **proper [dihedral angle](@entry_id:176389)**, often simply called a **torsion angle**, describes the rotation about a central chemical bond. It is defined by a sequence of four consecutively bonded atoms, which we may label $i-j-k-l$. The rotation of the terminal bond $k-l$ relative to the initial bond $i-j$ occurs around the axis of the central bond $j-k$. The proper [dihedral angle](@entry_id:176389), denoted by $\phi$, measures the twist around this central bond [@problem_id:3456981].

Geometrically, the angle $\phi$ is the angle between two intersecting planes. The first plane, $P_{ijk}$, is defined by the positions of the first three atoms $(i, j, k)$. The second plane, $P_{jkl}$, is defined by the positions of the last three atoms $(j, k, l)$. Both planes share the line segment connecting atoms $j$ and $k$, which serves as their axis of intersection. The proper [dihedral angle](@entry_id:176389) is the angle between these two planes [@problem_id:3456981].

In contrast, an **[improper dihedral angle](@entry_id:750575)**, denoted by $\omega$ or $\xi$, is not associated with a rotation about a central bond but rather with maintaining the geometry at a central atom. It is typically defined for a central atom bonded to three other atoms, a common topology for sp²-hybridized centers (e.g., in carbonyl groups or aromatic rings) or for maintaining the [stereochemistry](@entry_id:166094) of a [chiral center](@entry_id:171814). For a set of four atoms where atom $j$ is the central atom bonded to substituents $i, k,$ and $l$, an [improper dihedral angle](@entry_id:750575) can be defined to measure the out-of-plane displacement. A common convention constructs this angle as the dihedral between the plane defined by atoms $(i, j, k)$ and the plane defined by atoms $(i, j, l)$. This construction effectively measures the "pyramidalization" at atom $j$ by quantifying the rotation of the $j-l$ bond out of the plane formed by $i, j, k$ [@problem_id:3456981].

#### Mathematical Formulation of the Signed Dihedral Angle

To be useful in a [force field](@entry_id:147325), the dihedral angle must be a signed quantity, allowing the distinction between, for example, right-handed and left-handed helical twists. The sign convention is established using vector algebra and a right-hand rule.

Consider a proper dihedral for atoms $i, j, k, l$ with [position vectors](@entry_id:174826) $\mathbf{r}_i, \mathbf{r}_j, \mathbf{r}_k, \mathbf{r}_l$. The two planes of interest are $P_{ijk}$ and $P_{jkl}$. A normal vector to the first plane, $\mathbf{n}_1$, can be constructed from the cross product of the two bond vectors residing in that plane: $\mathbf{n}_1 = (\mathbf{r}_i - \mathbf{r}_j) \times (\mathbf{r}_k - \mathbf{r}_j)$. Similarly, a normal to the second plane is $\mathbf{n}_2 = (\mathbf{r}_j - \mathbf{r}_k) \times (\mathbf{r}_l - \mathbf{r}_k)$. For a numerically robust definition, these normals are normalized to [unit vectors](@entry_id:165907), $\hat{\mathbf{n}}_1$ and $\hat{\mathbf{n}}_2$.

The cosine of the angle $\phi$ between the planes is given by the dot product of their normals: $\cos(\phi) = \hat{\mathbf{n}}_1 \cdot \hat{\mathbf{n}}_2$. However, this expression is unsigned, as $\cos(\phi) = \cos(-\phi)$. To obtain the sign, we must define a direction of observation. The standard convention uses the direction of the central bond vector, $\mathbf{b}_2 = \mathbf{r}_k - \mathbf{r}_j$. The sign of the angle is positive if the rotation from plane $P_{ijk}$ to $P_{jkl}$ is counter-clockwise when viewed along the vector $\mathbf{b}_2$. This directional information is captured by the [scalar triple product](@entry_id:152997) involving the two normals and the bond vector. Specifically, the sine of the angle is given by $\sin(\phi) = \hat{\mathbf{b}}_2 \cdot (\hat{\mathbf{n}}_1 \times \hat{\mathbf{n}}_2)$, where $\hat{\mathbf{b}}_2$ is the [unit vector](@entry_id:150575) along the central bond [@problem_id:3457001].

With expressions for both $\cos(\phi)$ and $\sin(\phi)$, the complete signed angle in the range $(-\pi, \pi]$ can be unambiguously determined using the two-argument arctangent function, `atan2`:

$$
\phi = \operatorname{atan2} \! \left( \hat{\mathbf{b}}_2 \cdot (\hat{\mathbf{n}}_1 \times \hat{\mathbf{n}}_2), \; \hat{\mathbf{n}}_1 \cdot \hat{\mathbf{n}}_2 \right)
$$

This definition is invariant to translations and rotations of the entire molecule and provides a continuous and differentiable coordinate, except at singular geometries. The fundamental $2\pi$ periodicity of $\phi$ is a direct consequence of its geometric nature as a rotation angle; rotating by any integer multiple of $2\pi$ returns the [molecular geometry](@entry_id:137852) to an identical configuration, and thus the potential energy must also be $2\pi$-periodic [@problem_id:3457001].

A similar formulation applies to [improper dihedral](@entry_id:177625) angles. For an [improper torsion](@entry_id:168912) centered at atom $j$ with substituents $i, k, l$, defined by the angle between planes $(i,j,k)$ and $(i,j,l)$, the axis of rotation is the bond vector $\mathbf{a} = \mathbf{r}_i - \mathbf{r}_j$. The plane normals are $\mathbf{n}_1 = (\mathbf{r}_i - \mathbf{r}_j) \times (\mathbf{r}_k - \mathbf{r}_j)$ and $\mathbf{n}_2 = (\mathbf{r}_i - \mathbf{r}_j) \times (\mathbf{r}_l - \mathbf{r}_j)$. The signed improper angle $\omega$ is then computed analogously [@problem_id:3457012]:

$$
\omega = \operatorname{atan2} \! \left( \hat{\mathbf{a}} \cdot (\mathbf{n}_1 \times \mathbf{n}_2), \; \mathbf{n}_1 \cdot \mathbf{n}_2 \right)
$$

This definition ensures that the angle correctly measures out-of-plane distortion with a consistent sign convention based on the ordering of atoms.

### Functional Forms of Torsional Potentials

Once the dihedral coordinate is defined, a [potential energy function](@entry_id:166231) is required to describe the energetic cost of deviations from preferred conformations.

#### Proper Torsion Potentials: The Fourier Series

Since the potential energy $V(\phi)$ of a proper torsion must be periodic with period $2\pi$, it is natural to represent it using a Fourier series. Any well-behaved $2\pi$-[periodic function](@entry_id:197949) can be written as a sum of sine and cosine terms:

$$
V(\phi) = \frac{A_0}{2} + \sum_{n=1}^{\infty} \left[ A_n \cos(n\phi) + B_n \sin(n\phi) \right]
$$

Using the trigonometric identity $A_n \cos(n\phi) + B_n \sin(n\phi) = K_n \cos(n\phi - \delta_n)$, where $K_n = \sqrt{A_n^2 + B_n^2}$ is the amplitude and $\delta_n$ is the [phase angle](@entry_id:274491), we can rewrite the series in a more physically intuitive form. In practice, this series is truncated. A common functional form used in many force fields (e.g., CHARMM) is [@problem_id:3457055]:

$$
V(\phi) = \sum_{n} K_n \left[ 1 + \cos(n\phi - \delta_n) \right]
$$

In this expression, each parameter has a clear physical meaning:
*   **Multiplicity ($n$)**: An integer that determines the [periodicity](@entry_id:152486) of the term. The $n$-th term has $n$ minima in the interval $[0, 2\pi)$. The overall shape of the potential is determined by the superposition of terms with different multiplicities.
*   **Amplitude ($K_n$)**: A parameter in units of energy that determines the height of the energy barrier associated with the $n$-th term. The total barrier height is a combination of all $K_n$ values.
*   **Phase Angle ($\delta_n$)**: An angle that shifts the potential along the $\phi$ axis. It determines the location of the minima and maxima. For example, a term with $\delta_n = 0$ has maxima at $\phi = \frac{\pi}{n}, \frac{3\pi}{n}, \dots$ and minima at $\phi = 0, \frac{2\pi}{n}, \dots$. A phase of $\delta_n = \pi$ inverts this.
The constant `1` inside the bracket simply adds an energy offset, which does not affect the forces or torques as they depend on the derivative of the potential [@problem_id:3457055].

#### Case Study: The Rotational Barrier in Ethane

The ethane molecule provides a classic example of how physical principles dictate the form of the [torsional potential](@entry_id:756059). The rotation around the C-C bond in ethane exhibits a threefold symmetry, as rotating the molecule by $120^\circ$ ($2\pi/3$ radians) about this bond results in an indistinguishable configuration. This symmetry imposes a strict constraint on the Fourier series: only terms where the [multiplicity](@entry_id:136466) $n$ is a multiple of 3 (i.e., $n=3, 6, 9, \dots$) can have non-zero coefficients. Furthermore, because the molecule is [achiral](@entry_id:194107), the potential must be an [even function](@entry_id:164802), $V(\phi) = V(-\phi)$, which eliminates all sine terms. Thus, the potential for ethane can be written as $V(\phi) = \sum_k a_{3k} \cos(3k\phi)$ [@problem_id:3457038].

The leading and most [dominant term](@entry_id:167418) is for $n=3$. The physical origin of this barrier lies in a combination of two quantum mechanical effects. First, **[steric repulsion](@entry_id:169266)** (or Pauli exclusion repulsion) between the electron clouds of the C-H bonds is maximized in the [eclipsed conformation](@entry_id:180121) ($\phi = 0^\circ, 120^\circ, 240^\circ$), destabilizing it. Second, **[hyperconjugation](@entry_id:263927)**, a stabilizing electronic interaction between a filled C-H $\sigma$ bonding orbital on one carbon and the empty C-H $\sigma^*$ anti-[bonding orbital](@entry_id:261897) on the adjacent carbon, is maximized in the [staggered conformation](@entry_id:200836) ($\phi = 60^\circ, 180^\circ, 300^\circ$), where these orbitals are [anti-periplanar](@entry_id:184523). Both effects make the [staggered conformation](@entry_id:200836) more stable (lower energy) than the eclipsed one [@problem_id:3457038].

To model this, the potential $V(\phi)$ must have maxima at the eclipsed angles and minima at the staggered angles. The function $\cos(3\phi)$ is equal to $+1$ at the eclipsed angles and $-1$ at the staggered angles. Therefore, the leading term in the potential must be of the form $+K_3 \cos(3\phi)$ (relative to an offset), where the coefficient $K_3$ is positive. This ensures that the potential energy is highest for the eclipsed geometry and lowest for the staggered one, correctly capturing the threefold [rotational barrier](@entry_id:153477).

#### Alternative Functional Forms: The Ryckaert-Bellemans Potential

While the Fourier series is the most common representation, other functional forms exist. The **Ryckaert-Bellemans (RB) potential**, used for [alkanes](@entry_id:185193) in force fields like GROMOS, expresses the [torsional energy](@entry_id:175781) as a polynomial in $\cos(\phi)$ [@problem_id:3456994]:

$$
V(\phi) = \sum_{n=0}^{5} C_n \cos^n(\phi)
$$

At first glance, this appears different from a Fourier series. However, the two are mathematically related. Through trigonometric power-reduction formulas (related to Chebyshev polynomials), any power $\cos^n(\phi)$ can be expressed as a [linear combination](@entry_id:155091) of cosine terms of multiple angles, $\cos(k\phi)$, where $k \le n$. For instance, $\cos^2(\phi) = \frac{1}{2}(1 + \cos(2\phi))$ and $\cos^3(\phi) = \frac{1}{4}(3\cos(\phi) + \cos(3\phi))$. Therefore, a finite polynomial in $\cos(\phi)$ is mathematically equivalent to a finite cosine Fourier series. Because $\cos(\phi)$ is an even, $2\pi$-[periodic function](@entry_id:197949), any polynomial of it automatically shares these properties, making it a suitable choice for modeling symmetric torsions [@problem_id:3456994]. The coefficients $C_n$ are fitted to reproduce experimental data or quantum [mechanical energy](@entry_id:162989) profiles.

### Functional Forms and Applications of Improper Torsional Potentials

The physical role of improper torsions—to act as a [penalty function](@entry_id:638029) maintaining local geometry—leads to a different choice of functional form.

#### The Harmonic Potential

Improper torsions are designed to keep a group of atoms planar or to maintain the chirality of a [stereocenter](@entry_id:194773). The desired geometry corresponds to a specific equilibrium angle, $\omega_0$. For small deviations from this equilibrium, the potential energy surface $V(\omega)$ can be approximated by a Taylor series expansion around $\omega_0$. Since $\omega_0$ is a [stable equilibrium](@entry_id:269479), the first derivative of the potential must be zero, $\left(\frac{dV}{d\omega}\right)_{\omega_0} = 0$, and the second derivative must be positive. This means the leading non-constant term in the expansion is quadratic [@problem_id:3457016]:

$$
V(\omega) \approx V(\omega_0) + \frac{1}{2} \left( \frac{d^2V}{d\omega^2} \right)_{\omega_0} (\omega - \omega_0)^2
$$

By setting the reference energy $V(\omega_0)$ to zero and defining a force constant $k_{\text{imp}}$, we arrive at the simple **harmonic potential**:

$$
V_{\text{imp}}(\omega) = \frac{1}{2} k_{\text{imp}} (\omega - \omega_0)^2
$$

This parabolic, non-[periodic potential](@entry_id:140652) effectively creates a stiff spring that penalizes any deviation from the target angle $\omega_0$, making it an ideal and computationally simple choice for a geometric restraint.

#### Application: Enforcing Chirality

A crucial application of the harmonic improper potential is the preservation of [stereochemistry](@entry_id:166094) at a [chiral center](@entry_id:171814) during a simulation. Consider a tetrahedral stereogenic center $X$ bonded to four distinct groups $A, B, C, D$. An [improper dihedral angle](@entry_id:750575), say $\omega(A,X,B,C)$, can be defined. Its sign will be different for the $R$ and $S$ [enantiomers](@entry_id:149008).

To maintain a specific enantiomer, for example the $R$ configuration which corresponds to a positive equilibrium angle $\omega_0 > 0$, we can apply the harmonic potential $V_{\text{imp}}(\omega) = \frac{1}{2} k_{\text{imp}} (\omega - \omega_0)^2$. The minimum of this potential is at $\omega = \omega_0$, stabilizing the $R$ form. Racemization, or the inversion of the [stereocenter](@entry_id:194773), must proceed through a high-energy planar transition state where the improper angle $\omega$ is approximately zero. The energy of this transition state is $V_{\text{imp}}(0) = \frac{1}{2} k_{\text{imp}} \omega_0^2$. This creates an energy barrier to inversion, equal to $\Delta U = \frac{1}{2} k_{\text{imp}} \omega_0^2$, which prevents the molecule from spontaneously racemizing during a simulation. For typical [force field](@entry_id:147325) parameters, such as $k_{\text{imp}} = 280 \,\mathrm{kJ\,mol^{-1}\,rad^{-2}}$ and $|\omega_0| = 0.65 \,\mathrm{rad}$, this barrier is substantial, approximately $59.15 \,\mathrm{kJ\,mol^{-1}}$, effectively locking the [chirality](@entry_id:144105) [@problem_id:3457037].

#### Limitations of the Harmonic Model

Despite its utility, the [harmonic approximation](@entry_id:154305) has significant limitations. Its single-well, parabolic shape is qualitatively incorrect for systems that can physically invert, such as the nitrogen atom in ammonia. The true potential for such an inversion is a **double-well potential**, with two minima corresponding to the two pyramidal ground states and an energy barrier at the planar transition state. A [harmonic potential](@entry_id:169618) cannot describe this [barrier crossing](@entry_id:198645) or inversion process [@problem_id:3457016].

Furthermore, for large distortions from equilibrium, the [harmonic approximation](@entry_id:154305) breaks down. Two factors contribute to this failure. First, **[anharmonicity](@entry_id:137191)**: the true potential is not perfectly parabolic, and higher-order terms in the Taylor expansion (e.g., cubic and quartic) become significant. Second, **coupling**: at large distortions, the [improper torsion](@entry_id:168912) coordinate is not independent of other [internal coordinates](@entry_id:169764). For example, a large out-of-plane pucker will cause associated bond lengths and angles to change. Simple, uncoupled [force fields](@entry_id:173115) that sum individual harmonic terms neglect these cross-terms, leading to inaccuracies far from the equilibrium geometry [@problem_id:3457016].

### Advanced Topics and Practical Considerations

The implementation and [parameterization](@entry_id:265163) of torsional potentials involve several subtleties that are critical for the accuracy and stability of [molecular simulations](@entry_id:182701).

#### Parameterization and the Problem of Double Counting

A major challenge in [force field development](@entry_id:188661) is the overlap between different energy terms. The [torsional potential](@entry_id:756059) $V(\phi)$ describes the energy profile of rotation around the $j-k$ bond. However, the nonbonded Lennard-Jones and Coulomb interactions between the first and fourth atoms, the so-called **[1-4 interactions](@entry_id:746136)**, also vary as a function of the dihedral angle $\phi$. If both a [torsional potential](@entry_id:756059) and a 1-4 nonbonded potential are included, there is a significant risk of **[double counting](@entry_id:260790)** the same physical effect.

Standard [force fields](@entry_id:173115) address this by applying a scaling factor (e.g., 0.5 or 0.833) to the 1-4 [nonbonded interactions](@entry_id:189647), but a more rigorous approach is needed during parameterization to properly disentangle the two contributions. One sophisticated strategy is to enforce mathematical orthogonality between the fitted [torsional potential](@entry_id:756059) and the 1-4 nonbonded energy profile [@problem_id:3456991].

Given a set of quantum mechanical (QM) reference energies from a [dihedral scan](@entry_id:166741) and the corresponding 1-4 nonbonded energies $E_{14}(\phi)$ calculated from the classical model, the goal is to fit a [torsional potential](@entry_id:756059) $U_{\text{tor}}(\phi)$ such that it is orthogonal to $E_{14}(\phi)$. This can be achieved by solving a [constrained least-squares](@entry_id:747759) problem, where the coefficients of the torsional basis functions are optimized to fit the QM data subject to the linear constraint that their inner product with the $E_{14}$ vector is zero. Alternatively, one can first construct a new set of basis functions that are explicitly orthogonal to the $E_{14}$ profile (e.g., via a Gram-Schmidt process) and then perform an unconstrained fit using this new basis. Both methods guarantee by construction that the final [torsional potential](@entry_id:756059) does not contain any component that mimics the pre-defined 1-4 interaction, thus avoiding [double counting](@entry_id:260790) in a mathematically robust manner [@problem_id:3456991].

#### Numerical Stability and Pathological Geometries

The calculation of [dihedral angles](@entry_id:185221) and their associated forces relies on cross products to define plane normals. This procedure encounters a numerical singularity when the atoms defining a plane become **collinear**. For a proper torsion $i-j-k-l$, this occurs if the bond angle $\angle ijk$ or $\angle jkl$ approaches $180^\circ$. In this case, the magnitude of the corresponding normal vector, e.g., $\|\mathbf{n}_1\| = \|(\mathbf{r}_i - \mathbf{r}_j) \times (\mathbf{r}_k - \mathbf{r}_j)\|$, approaches zero [@problem_id:3457023].

Standard formulas for the dihedral angle and its gradient involve division by the magnitude of these normal vectors. As the geometry approaches [collinearity](@entry_id:163574), these denominators approach zero, leading to floating-point exceptions or, just as dangerously, extremely large and unphysical forces that can destabilize or crash a simulation.

Robust molecular dynamics programs must include safeguards to handle these pathological geometries. A common approach involves:
1.  **Detection**: The code first checks if the magnitude of a normal vector (or its square) falls below a small numerical threshold, indicating near-[collinearity](@entry_id:163574).
2.  **Fallback Calculation**: If [collinearity](@entry_id:163574) is detected, the program switches to a special, numerically stable routine to compute the torsion and its force. One such method involves projecting the terminal bond vectors (e.g., $\mathbf{r}_i - \mathbf{r}_j$ and $\mathbf{r}_l - \mathbf{r}_k$) onto the plane perpendicular to the central bond vector $(\mathbf{r}_k - \mathbf{r}_j)$ and calculating the angle between these projected vectors. The analytical gradient of this fallback calculation is well-behaved in the collinear limit.
3.  **Force Capping**: As a final precaution, some algorithms may cap the magnitude of the resulting torsional force to prevent any residual numerical issues from generating extreme values.

These safeguards ensure that the simulation remains stable even when molecules transiently sample highly strained or linear geometries, which is essential for the robustness of long-timescale [molecular dynamics simulations](@entry_id:160737) [@problem_id:3457023].