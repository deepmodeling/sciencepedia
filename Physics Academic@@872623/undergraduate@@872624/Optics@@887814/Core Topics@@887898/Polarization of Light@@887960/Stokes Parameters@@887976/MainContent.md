## Introduction
The polarization of light is a fundamental property that describes the orientation of its oscillating electric field. While simple models like the Jones calculus are effective for describing perfectly polarized, [coherent light](@entry_id:170661), they fall short when confronted with the complexities of the real world. Light from most natural and artificial sources—from distant stars and scattered sunlight to LEDs and incandescent bulbs—is often partially polarized or completely unpolarized. To analyze and manipulate these general states of light, a more robust and comprehensive framework is required.

This article introduces the Stokes parameters, a powerful formalism developed by Sir George Gabriel Stokes that provides a complete description of any polarization state. Unlike methods based on electric field amplitudes, the Stokes parameters are defined by directly measurable, time-averaged intensities, making them an indispensable tool in experimental optics and engineering.

Across the following chapters, you will gain a thorough understanding of this essential topic. The **Principles and Mechanisms** chapter will lay the groundwork, defining the Stokes parameters from both an operational and mathematical perspective and showing how they are used to classify polarization. The **Applications and Interdisciplinary Connections** chapter will then explore the vast utility of this formalism, from designing LCD screens and analyzing astronomical data to its surprising link with quantum mechanics. Finally, the **Hands-On Practices** section will solidify your knowledge by guiding you through practical problems that demonstrate the power of the Stokes formalism in real-world scenarios.

## Principles and Mechanisms

While the previous chapter introduced the concept of [light polarization](@entry_id:272135), a complete description requires a framework that can handle not only perfectly [polarized light](@entry_id:273160) but also partially polarized and unpolarized light. The Jones calculus, which uses two-component [complex vectors](@entry_id:192851), is powerful but fundamentally limited to coherent, fully polarized waves. Many real-world light sources, from incandescent bulbs and LEDs to distant stars, are either unpolarized or partially polarized. To describe these, we need a more general formalism rooted in observable, time-averaged intensities rather than phase-dependent electric field amplitudes. The Stokes parameters provide exactly this framework.

### Defining the Stokes Parameters

The Stokes parameters, introduced by Sir George Gabriel Stokes in 1852, form a set of four real values that completely characterize the polarization state of an electromagnetic wave. These parameters, collectively forming the **Stokes vector** $S = [S_0, S_1, S_2, S_3]^T$, have the crucial advantage of being directly related to measurable intensities.

#### The Operational Definition: A Basis in Measurement

The power of the Stokes formalism lies in its operational definition. The four parameters are defined by a series of intensity measurements performed on a light beam using different types of polarizers.

Let us consider the intensity of a beam transmitted through a set of ideal polarizers:
- $I_H$ and $I_V$: Intensities transmitted by horizontal and vertical linear polarizers.
- $I_{45}$ and $I_{135}$: Intensities transmitted by linear polarizers oriented at $+45^\circ$ and $+135^\circ$ (or $-45^\circ$).
- $I_R$ and $I_L$: Intensities transmitted by right- and left-circular [polarizers](@entry_id:269119).

The Stokes parameters are defined as follows:

*   **$S_0$**: Represents the **total intensity** of the light beam. It is the sum of intensities measured for any pair of orthogonal [polarization states](@entry_id:175130). For example, $S_0 = I_H + I_V$. This parameter is always positive and carries units of intensity (e.g., $\text{W/m}^2$).

*   **$S_1$**: Describes the preponderance of horizontal linear polarization over vertical [linear polarization](@entry_id:273116). It is defined as the difference $S_1 = I_H - I_V$. A positive $S_1$ indicates a horizontal tendency, a negative $S_1$ indicates a vertical tendency, and $S_1 = 0$ indicates no preference between the two.

*   **$S_2$**: Describes the preponderance of $+45^\circ$ [linear polarization](@entry_id:273116) over $+135^\circ$ [linear polarization](@entry_id:273116). It is defined as the difference $S_2 = I_{45} - I_{135}$. A positive $S_2$ indicates a $+45^\circ$ tendency, while a negative $S_2$ indicates a $+135^\circ$ tendency.

*   **$S_3$**: Describes the preponderance of right-[circular polarization](@entry_id:261702) over left-circular polarization. It is defined as the difference $S_3 = I_R - I_L$. A positive $S_3$ indicates a right-circular tendency, a negative $S_3$ indicates a left-circular tendency, and $S_3 = 0$ indicates no net circular polarization (i.e., the light is linearly or unpolarized).

From these definitions, we can derive the intensity transmitted by any single [polarizer](@entry_id:174367) in terms of the Stokes parameters. For instance, since $S_0 = I_H + I_V$ and $S_1 = I_H - I_V$, we can solve for the individual intensities: $I_H = \frac{1}{2}(S_0 + S_1)$ and $I_V = \frac{1}{2}(S_0 - S_1)$. Similar relations hold for the other pairs.

To illustrate, consider an experimental scenario where a measurement reveals that the intensity transmitted through a horizontal [polarizer](@entry_id:174367) is one-third of that through a vertical polarizer, i.e., $I_H = \frac{1}{3}I_V$ [@problem_id:2256964]. In this case, $S_1 = \frac{1}{3}I_V - I_V = -\frac{2}{3}I_V$, and $S_0 = \frac{1}{3}I_V + I_V = \frac{4}{3}I_V$. The **normalized Stokes parameter** $s_1 = S_1/S_0$ is then $-\frac{2}{3}I_V / \frac{4}{3}I_V = -1/2$. This dimensionless value concisely captures the beam's strong vertical polarization preference, independent of its total intensity.

#### The Mathematical Foundation: Connection to the Electric Field

While the operational definition is paramount for measurement, the Stokes parameters also have a rigorous mathematical basis rooted in the complex electric field components of a [monochromatic plane wave](@entry_id:263295). For a wave propagating in the $z$-direction, the electric field components in the $xy$-plane can be written as $\tilde{E}_x$ and $\tilde{E}_y$. The Stokes parameters are defined in terms of these complex amplitudes as:

$S_0 = |\tilde{E}_x|^2 + |\tilde{E}_y|^2$

$S_1 = |\tilde{E}_x|^2 - |\tilde{E}_y|^2$

$S_2 = 2 \text{Re}(\tilde{E}_x^* \tilde{E}_y) = \tilde{E}_x^* \tilde{E}_y + \tilde{E}_x \tilde{E}_y^*$

$S_3 = 2 \text{Im}(\tilde{E}_x^* \tilde{E}_y) = i(\tilde{E}_x \tilde{E}_y^* - \tilde{E}_x^* \tilde{E}_y)$

Here, the asterisk ($*$) denotes the [complex conjugate](@entry_id:174888). This formulation applies strictly to fully [polarized light](@entry_id:273160), for which the Jones vector $(\tilde{E}_x, \tilde{E}_y)$ is well-defined. For partially polarized or unpolarized light, the parameters are understood as time-averages of these expressions, denoted $\langle \dots \rangle$.

As a direct application of these formulas, consider a light beam whose electric field is described by the Jones vector components $\tilde{E}_x = 3$ and $\tilde{E}_y = 2i$ [@problem_id:2256991]. We first calculate the squared magnitudes: $|\tilde{E}_x|^2 = 3^2 = 9$ and $|\tilde{E}_y|^2 = |2i|^2 = 4$. Then we compute the cross-term: $\tilde{E}_x^* \tilde{E}_y = (3)(2i) = 6i$. From these, we can directly find the unnormalized Stokes parameters:

$S_0 = 9 + 4 = 13$

$S_1 = 9 - 4 = 5$

$S_2 = 2 \text{Re}(6i) = 2 \cdot 0 = 0$

$S_3 = 2 \text{Im}(6i) = 2 \cdot 6 = 12$

The resulting Stokes vector is $S = [13, 5, 0, 12]^T$. This example provides a clear bridge from the abstract Jones vector formalism to the physically measurable Stokes parameters.

### Characterizing the State of Polarization

With the Stokes parameters defined, we can now establish a quantitative basis for classifying any state of polarization.

#### The Degree of Polarization

For any physically realizable light beam, the Stokes parameters obey the inequality:

$S_0^2 \ge S_1^2 + S_2^2 + S_3^2$

This relationship is fundamental. The case of equality corresponds to perfectly [polarized light](@entry_id:273160), while the inequality holds for partially polarized or unpolarized light. This leads to the definition of a crucial dimensionless quantity, the **Degree of Polarization (DOP)**, denoted by $P$:

$P = \frac{\sqrt{S_1^2 + S_2^2 + S_3^2}}{S_0}$

The value of $P$ ranges from 0 to 1 and provides a quantitative measure of the degree of order in the light's polarization:

*   **$P=1$**: The light is **fully polarized**. In this case, $S_0^2 = S_1^2 + S_2^2 + S_3^2$. This is the condition met by ideal laser beams or light passed through a perfect polarizer.
*   **$P=0$**: The light is **completely unpolarized**. This requires $S_1 = S_2 = S_3 = 0$. The Stokes vector for such light is simply $[S_0, 0, 0, 0]^T$. Sunlight and light from an incandescent bulb are common approximations.
*   **$0 \lt P \lt 1$**: The light is **partially polarized**. This is the most general case, representing a statistical mixture of polarized and [unpolarized light](@entry_id:176162). Light scattered from the atmosphere or from distant nebulae often falls into this category [@problem_id:1606711].

The identity for fully polarized light is particularly useful. Suppose a beam of fully polarized light has a total intensity $S_0 = 25.0 \text{ W/m}^2$, with measured values $S_1 = -15.0 \text{ W/m}^2$ and $S_3 = 16.0 \text{ W/m}^2$ [@problem_id:2256937]. We can determine the magnitude of $S_2$:

$S_2^2 = S_0^2 - S_1^2 - S_3^2 = (25.0)^2 - (-15.0)^2 - (16.0)^2 = 625 - 225 - 256 = 144$

Thus, $|S_2| = 12.0 \text{ W/m}^2$. If we are further told that the intensity transmitted through a $+45^\circ$ polarizer is less than through a $+135^\circ$ [polarizer](@entry_id:174367) ($I_{45} \lt I_{135}$), then by definition $S_2 = I_{45} - I_{135}$ must be negative. Therefore, we find $S_2 = -12.0 \text{ W/m}^2$. Similarly, if we knew $S_0=25.0$, $S_1=12.0$, and $S_2=-15.0$ for a fully polarized beam with a net right-hand circular component, we could deduce $S_3$ [@problem_id:2256976]. The calculation gives $S_3^2 = 256$, so $S_3 = \pm 16.0$. Since right-hand [circular polarization](@entry_id:261702) corresponds to $S_3 > 0$, we must have $S_3 = 16.0 \text{ W/m}^2$.

#### Classifying Polarization Forms

Once the DOP is determined, we can further classify the nature of the polarization. For a fully polarized beam ($P=1$), the specific form of polarization—linear, circular, or elliptical—is determined by the values of $S_1, S_2,$ and $S_3$ [@problem_id:2256994]:

*   **Linear Polarization**: Occurs when there is no circular component, i.e., $S_3 = 0$. The orientation of the linear polarization depends on the ratio of $S_2$ to $S_1$.
*   **Circular Polarization**: Occurs when there is no preferred linear axis, i.e., $S_1 = S_2 = 0$. If $S_3 > 0$, the light is right-circularly polarized; if $S_3  0$, it is left-circularly polarized.
*   **Elliptical Polarization**: The most general case, occurring when none of the above special conditions are met (i.e., $S_3 \neq 0$ and at least one of $S_1$ or $S_2$ is non-zero). The handedness of the ellipse is determined by the sign of $S_3$: positive for right-elliptical, negative for left-elliptical.

Let's apply this classification to an example. An engineer measures a laser beam and obtains the Stokes vector $S = [13.0, 3.0, 4.0, -12.0]^T$ W/m$^2$ [@problem_id:2256994].
First, we compute the DOP:
$\sqrt{S_1^2 + S_2^2 + S_3^2} = \sqrt{3.0^2 + 4.0^2 + (-12.0)^2} = \sqrt{9 + 16 + 144} = \sqrt{169} = 13.0$.
$P = \frac{13.0}{S_0} = \frac{13.0}{13.0} = 1$.
The beam is fully polarized.
Next, we check the conditions. Since $S_3 = -12.0 \neq 0$, it is not linear. Since $S_1 = 3.0 \neq 0$ and $S_2 = 4.0 \neq 0$, it is not circular. Therefore, the polarization must be elliptical. Finally, because $S_3  0$, the beam is **left-elliptically polarized**.

### Superposition and Decomposition of Light Beams

A major strength of the Stokes formalism is its ability to handle combinations of light beams and to deconstruct a beam into its fundamental components.

#### Incoherent Superposition

When two light beams are **incoherent**, meaning their electric field phase relationship varies randomly and rapidly, their intensities add. A profound consequence is that their Stokes vectors also add, component by component. This property is what allows the Stokes formalism to describe [partially polarized light](@entry_id:267467), which the phase-sensitive Jones calculus cannot.

Consider a composite beam formed by combining an unpolarized beam of intensity $I_U$ with a perfectly linearly polarized beam of intensity $I_P$, whose polarization axis is at an angle $\theta$ to the horizontal [@problem_id:2256983] [@problem_id:2256957].

The Stokes vector for the unpolarized beam is $S_U = [I_U, 0, 0, 0]^T$.
The Stokes vector for the linearly polarized beam is $S_P = [I_P, I_P\cos(2\theta), I_P\sin(2\theta), 0]^T$.

Since the beams are incoherent, the Stokes vector of the combined beam is the sum $S = S_U + S_P$:
$S = [I_U + I_P, I_P\cos(2\theta), I_P\sin(2\theta), 0]^T$.

The [degree of polarization](@entry_id:276690) of this composite beam is:
$P = \frac{\sqrt{(I_P\cos(2\theta))^2 + (I_P\sin(2\theta))^2 + 0^2}}{I_U + I_P} = \frac{\sqrt{I_P^2(\cos^2(2\theta) + \sin^2(2\theta))}}{I_U + I_P} = \frac{I_P}{I_U + I_P}$.

This elegant result shows that the [degree of polarization](@entry_id:276690) is simply the fraction of the total intensity that comes from the polarized source. Notably, the result is independent of the polarization angle $\theta$.

#### The Polarized and Unpolarized Components of Light

The principle of incoherent superposition leads to a powerful concept: any [partially polarized light](@entry_id:267467) beam can be uniquely decomposed into the sum of a completely unpolarized component and a completely polarized component [@problem_id:1606711].

Let a beam be described by the Stokes vector $S = [S_0, S_1, S_2, S_3]^T$. The total intensity $S_0$ can be seen as the sum of the intensity of its polarized part, $I_{pol}$, and its unpolarized part, $I_{unpol}$.
$S_0 = I_{pol} + I_{unpol}$.

The intensity of the polarized part is given by the magnitude of the polarization components of the vector:
$I_{pol} = \sqrt{S_1^2 + S_2^2 + S_3^2}$.

This is simply $S_0 \times P$. From this, we can find the intensity of the unpolarized component:
$I_{unpol} = S_0 - I_{pol} = S_0 - \sqrt{S_1^2 + S_2^2 + S_3^2}$.
This expression is vital in fields like observational astronomy for quantifying the depolarizing effects of [interstellar dust](@entry_id:159541).

We can express this decomposition in terms of Stokes vectors [@problem_id:2256970]: $S = S_{pol} + S_{unpol}$.
The unpolarized part has vector $S_{unpol} = [I_{unpol}, 0, 0, 0]^T$.
The polarized part carries all of the polarization information: $S_{pol} = [I_{pol}, S_1, S_2, S_3]^T$.
Note that for $S_{pol}$, the total intensity $I_{pol}$ is equal to $\sqrt{S_1^2 + S_2^2 + S_3^2}$, satisfying the condition for fully [polarized light](@entry_id:273160).

For instance, an astrophysicist measures light from a celestial object and finds its Stokes vector to be $S = [3, 1, 1, 1]^T$ in arbitrary units [@problem_id:2256970]. To analyze its intrinsic polarization, we decompose it.
First, we find the intensity of the polarized part:
$I_{pol} = \sqrt{1^2 + 1^2 + 1^2} = \sqrt{3}$.
The Stokes vector for the completely polarized part is therefore:
$S_{pol} = \begin{pmatrix} \sqrt{3} \\ 1 \\ 1 \\ 1 \end{pmatrix}$.
The intensity of the unpolarized part is $I_{unpol} = S_0 - I_{pol} = 3 - \sqrt{3}$. The corresponding Stokes vector is $S_{unpol} = [3-\sqrt{3}, 0, 0, 0]^T$.

### Transformations of Polarization: An Introduction to Mueller Calculus

The Stokes formalism extends naturally to describe how optical components modify the polarization of light. Each optical element—such as a polarizer, retarder (wave plate), or rotator—can be represented by a $4 \times 4$ real matrix called a **Mueller matrix**, $M$. If a light beam with an initial Stokes vector $S_{in}$ passes through an optical element, the Stokes vector of the emerging light, $S_{out}$, is given by a simple matrix multiplication:

$S_{out} = M S_{in}$

This **Stokes-Mueller calculus** is a powerful tool for designing and analyzing complex optical systems.

Let's examine a specific case to see this principle in action [@problem_id:2256956]. Consider a beam of [partially polarized light](@entry_id:267467) with $S_1 = S_2 = 0$, so its initial Stokes vector is $S_{in} = [I_{total}, 0, 0, k I_{total}]^T$, where $0 \lt k \lt 1$. This represents a mixture of [unpolarized light](@entry_id:176162) and circularly polarized light.

This beam first passes through a **[quarter-wave plate](@entry_id:262260) (QWP)**, an element that introduces a phase shift of $\pi/2$ ($90^\circ$) between two orthogonal field components. If the QWP's fast axis is at $+45^\circ$, it has the specific effect of converting circular polarization into [linear polarization](@entry_id:273116). The Stokes vector emerging from the QWP is found to be $S' = [I_{total}, -k I_{total}, 0, 0]^T$. The initial circular preference ($S_3$) has been transformed into a linear preference ($S_1$), demonstrating how optical elements can interconvert polarization types.

Next, this transformed beam passes through an ideal horizontal [linear polarizer](@entry_id:195509). The intensity transmitted by such a polarizer is given by $I_{out} = \frac{1}{2}(S'_0 + S'_1)$. Substituting the components of $S'$, we find:

$I_{out} = \frac{1}{2}(I_{total} + (-k I_{total})) = \frac{1 - k}{2} I_{total}$.

This example showcases the predictive power of the Mueller calculus. By representing both the light and the optical elements in a consistent mathematical language, we can systematically calculate the outcome of complex interactions, a task essential for applications ranging from [ellipsometry](@entry_id:275454) to the design of LCD screens and astronomical polarimeters.