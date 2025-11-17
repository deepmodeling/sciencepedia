## Introduction
Predicting the failure of composite laminas is a cornerstone of modern [structural engineering](@entry_id:152273), essential for safely harnessing the high performance of advanced materials. Unlike simple [isotropic materials](@entry_id:170678), the directional nature of composites means their strength is highly dependent on the loading direction relative to the fiber orientation. This anisotropy creates a significant challenge, rendering traditional failure theories inadequate and necessitating specialized models to prevent catastrophic structural collapse. This article provides a comprehensive guide to these critical analytical tools. The first chapter, "Principles and Mechanisms," establishes the theoretical foundation, explaining why analysis must occur in the material coordinate system and introducing a hierarchy of [failure criteria](@entry_id:195168), from Maximum Stress to Tsai-Wu and Hashin. The second chapter, "Applications and Interdisciplinary Connections," bridges theory and practice, showcasing how these criteria are used in design, [progressive failure analysis](@entry_id:203451), and even to understand biological structures. Finally, "Hands-On Practices" offers exercises to reinforce these concepts, ensuring a practical command of the material.

## Principles and Mechanisms

The prediction of failure in a [composite lamina](@entry_id:200309) represents a foundational challenge in the [mechanics of materials](@entry_id:201885). Unlike [isotropic materials](@entry_id:170678), whose failure can often be characterized by a single scalar criterion, the pronounced anisotropy of composite laminas necessitates a more nuanced approach. This chapter elucidates the core principles and mechanisms governing lamina failure, establishing the theoretical framework upon which practical engineering analysis is built. We will progress from fundamental definitions of stress and strength in an [anisotropic medium](@entry_id:187796) to a systematic evaluation of the major [failure criteria](@entry_id:195168), highlighting their physical basis and inherent limitations.

### The Material Coordinate System and State of Stress

To analyze a [composite lamina](@entry_id:200309), we must first establish a coordinate system that reflects its intrinsic [material symmetry](@entry_id:173835). For a **unidirectional (UD) lamina**, which is the fundamental building block of many composite structures, the material is **orthotropic**. This means its [mechanical properties](@entry_id:201145) are symmetric with respect to three mutually orthogonal planes. The lines of intersection of these planes define the **principal material axes**, denoted as 1, 2, and 3. By universal convention [@problem_id:2885626]:

-   The **1-axis** is aligned with the fiber direction, representing the direction of maximum stiffness and strength.
-   The **2-axis** is perpendicular to the fibers but lies within the plane of the lamina. It is known as the in-plane transverse direction.
-   The **3-axis** is normal to the lamina plane, referred to as the through-the-thickness direction.

Because laminas are typically thin relative to their in-plane dimensions, it is standard practice to assume a state of **[plane stress](@entry_id:172193)** for in-plane loading. This assumption posits that the stress components acting on the faces normal to the 3-axis are negligible. In the material coordinate system, this implies:
$ \sigma_{33} = \tau_{13} = \tau_{23} = 0 $

Consequently, the state of stress within the lamina is fully described by the in-[plane stress](@entry_id:172193) components. For analytical convenience, these are arranged into a stress vector:
$ \{\sigma\} = \begin{pmatrix} \sigma_{11} \\ \sigma_{22} \\ \tau_{12} \end{pmatrix} $

The corresponding in-plane strains are assembled into a strain vector, which, by engineering convention, uses the **engineering shear strain** $\gamma_{12}$ rather than the tensorial shear strain $\epsilon_{12}$:
$ \{\epsilon\} = \begin{pmatrix} \epsilon_{11} \\ \epsilon_{22} \\ \gamma_{12} \end{pmatrix} $
where the engineering shear strain is defined as $\gamma_{12} = 2\epsilon_{12}$. This convention is critical as it is embedded in the standard formulation of the lamina's [constitutive equations](@entry_id:138559).

### The Imperative of Analysis in the Material Frame

A common point of confusion for those new to composite analysis is why [failure criteria](@entry_id:195168) are not applied directly to the stresses in the global coordinate system of the structure (e.g., the $x-y$ axes of a plate). The answer lies in the fundamental nature of anisotropy [@problem_id:2885623].

The strength of an orthotropic lamina is inherently directional. Material strength parameters are determined through experiments where loads are applied precisely along the principal material axes. These fundamental strengths are:

-   $X_t$: Longitudinal tensile strength (in the 1-direction)
-   $X_c$: Longitudinal compressive strength (in the 1-direction)
-   $Y_t$: Transverse tensile strength (in the 2-direction)
-   $Y_c$: Transverse compressive strength (in the 2-direction)
-   $S$: In-plane [shear strength](@entry_id:754762) (in the 1-2 plane)

These values represent the material's intrinsic capacity to resist specific modes of loading relative to its own [microstructure](@entry_id:148601). A failure criterion is essentially a mathematical representation of a failure surface in [stress space](@entry_id:199156), and its coefficients are calibrated using these fundamental strength values. Therefore, the failure surface is fixed relative to the material axes.

When a lamina is oriented at an off-axis angle $\theta$ within a laminate, a simple global load, such as [uniaxial tension](@entry_id:188287) $\sigma_x$, induces a complex, multiaxial state of stress $(\sigma_{11}, \sigma_{22}, \tau_{12})$ in the lamina's material frame. This transformation from global axes $(x,y)$ to material axes $(1,2)$ is governed by the standard [stress transformation](@entry_id:184474) equations:
$ \sigma_{11} = \sigma_x \cos^2\theta + \sigma_y \sin^2\theta + 2\tau_{xy} \sin\theta \cos\theta $
$ \sigma_{22} = \sigma_x \sin^2\theta + \sigma_y \cos^2\theta - 2\tau_{xy} \sin\theta \cos\theta $
$ \tau_{12} = -(\sigma_x - \sigma_y) \sin\theta \cos\theta + \tau_{xy} (\cos^2\theta - \sin^2\theta) $

Consider a lamina with a transverse tensile strength $Y_t = 40\,\mathrm{MPa}$ oriented at $\theta = 45^\circ$ and subjected to a global uniaxial stress $\sigma_x = 100\,\mathrm{MPa}$. A naive comparison of the applied stress to, for instance, the longitudinal strength $X_t$ (e.g., $1500\,\mathrm{MPa}$) would suggest the lamina is safe. However, the [stress transformation](@entry_id:184474) yields $\sigma_1 = 50\,\mathrm{MPa}$, $\sigma_2 = 50\,\mathrm{MPa}$, and $\tau_{12} = -50\,\mathrm{MPa}$ in the material frame. Comparing the transverse stress $\sigma_2 = 50\,\mathrm{MPa}$ to the transverse strength $Y_t = 40\,\mathrm{MPa}$ reveals that the lamina has, in fact, failed [@problem_id:2885623].

This example demonstrates a critical principle: **Failure analysis must be conducted in the material coordinate system by comparing the transformed stress components to the fundamental strengths defined in that same system.** Any other approach constitutes a physically meaningless comparison of quantities defined in incompatible [reference frames](@entry_id:166475).

### Micromechanical Origins of Failure Modes

The anisotropic strengths of a UD lamina are a direct consequence of its two-phase [microstructure](@entry_id:148601): stiff, strong fibers embedded in a relatively soft, weak matrix. The way loads are shared between these constituents dictates the failure mechanism [@problem_id:2638157]. This understanding justifies the physical separation of failure into **fiber-dominated** and **matrix-dominated** modes.

-   **Longitudinal Loading ($\sigma_{11}$):** Under loading parallel to the fibers, the kinematic assumption of [isostrain](@entry_id:184570) ($\epsilon_{11, \text{fiber}} \approx \epsilon_{11, \text{matrix}}$) is a reasonable approximation. Due to the vast difference in modulus ($E_f \gg E_m$), the stiff fibers carry the overwhelming majority of the load. Failure is therefore governed by fiber fracture in tension or fiber microbuckling in compression. This is a **fiber-dominated** mode, and its strength is characterized by $X_t$ and $X_c$.

-   **Transverse and Shear Loading ($\sigma_{22}, \tau_{12}$):** Under loading perpendicular to the fibers or in-plane shear, the load must be transferred through the compliant matrix. The matrix and the [fiber-matrix interface](@entry_id:200592) become the "weak links" in the system. Failure occurs via matrix cracking, interfacial debonding, or matrix shear yielding at stress levels far below the fiber strength. These are **matrix-dominated** modes, and their strengths are characterized by $Y_t, Y_c,$ and $S$.

Furthermore, the behavior of the polymer matrix itself leads to significant differences between tensile and compressive strengths. Under transverse tension ($\sigma_2 > 0$), tensile hydrostatic stresses in the matrix promote the opening and growth of microcracks and interfacial debonds, leading to a relatively low strength $Y_t$. In contrast, under transverse compression ($\sigma_2  0$), microcracks are forced closed, and the compressive hydrostatic stress state increases the matrix's resistance to shear yielding (a phenomenon known as pressure sensitivity). This results in a significantly higher compressive strength, so it is common to find $Y_c \gg Y_t$ [@problem_id:2885627]. This inherent [tension-compression asymmetry](@entry_id:201728) is a key feature that any robust failure criterion must be able to capture.

### A Hierarchy of Lamina Failure Criteria

A variety of [failure criteria](@entry_id:195168) have been developed, ranging from simple stress limits to complex tensor polynomials. They can be broadly categorized by whether they account for stress interactions and whether they distinguish between failure modes.

#### Non-Interactive Criteria: Maximum Stress and Maximum Strain

The simplest approaches treat each stress or strain component independently.

The **Maximum Stress Criterion** posits that failure occurs if any stress component in the material axes exceeds its corresponding strength. The failure conditions are a set of independent inequalities [@problem_id:2885660]:
- If $\sigma_{11}  0$, failure occurs if $\sigma_{11} \ge X_t$.
- If $\sigma_{11}  0$, failure occurs if $|\sigma_{11}| \ge X_c$.
- If $\sigma_{22}  0$, failure occurs if $\sigma_{22} \ge Y_t$.
- If $\sigma_{22}  0$, failure occurs if $|\sigma_{22}| \ge Y_c$.
- Failure occurs if $|\tau_{12}| \ge S$.

The primary virtue of this criterion is its simplicity and its clear link to the fundamental strengths. However, its major drawback is the complete neglect of stress interactions. For example, it predicts that the presence of a high shear stress $\tau_{12}$ has no effect on the transverse stress $\sigma_{22}$ required to cause failure, which is physically unrealistic. As illustrated by a case with applied stresses $\sigma_x=100\,\mathrm{MPa}$, $\sigma_y=30\,\mathrm{MPa}$, and $\tau_{xy}=230\,\mathrm{MPa}$ on a $30^\circ$ ply, the transformed stresses might be such that only the shear component exceeds its limit, predicting a pure shear failure even while [normal stresses](@entry_id:260622) are present [@problem_id:2885660].

The **Maximum Strain Criterion** is analogous, but compares the strain components $\{\epsilon_{11}, \epsilon_{22}, \gamma_{12}\}$ to their ultimate values (e.g., $\epsilon_{1t}^u = X_t/E_1$). Due to Poisson's effect and the anisotropic constitutive law, the stress and strain components are not simply proportional. Consequently, the Maximum Stress and Maximum Strain criteria are not equivalent and will generally predict failure at different load levels [@problem_id:2885640].

#### Interactive, Mode-Independent Criteria

To address the shortcomings of non-interactive criteria, several theories have been proposed that combine stress components into a single scalar failure index. These are typically [quadratic forms](@entry_id:154578).

The **Tsai-Hill Criterion** was developed as an extension of the von Mises [yield criterion](@entry_id:193897) for isotropic metals to [anisotropic materials](@entry_id:184874). For [plane stress](@entry_id:172193), its form is [@problem_id:2885653]:
$ \left(\frac{\sigma_{11}}{X}\right)^2 - \frac{\sigma_{11}\sigma_{22}}{X^2} + \left(\frac{\sigma_{22}}{Y}\right)^2 + \left(\frac{\tau_{12}}{S}\right)^2 = 1 $

Here, $X$ and $Y$ are the principal strengths. A crucial limitation arises from the criterion's purely quadratic nature. Because all stress terms are of degree two, the failure surface is centro-symmetric. This means it predicts the same strength in tension and compression (e.g., if $X=X_t$ is used, it predicts a compressive strength of $-X_t$). This contradicts the known asymmetry of composites, where $X_c \neq X_t$ and $Y_c \neq Y_t$. Additionally, for states with $\sigma_{11}  0$ and $\sigma_{22}  0$, the negative interaction term $(-\sigma_{11}\sigma_{22}/X^2)$ has a non-physical strengthening effect, often leading to non-conservative (overly optimistic) failure predictions compared to more physically-based models [@problem_id:2885640].

The **Tsai-Wu Criterion** is a more general and powerful theory based on a tensor polynomial formulation. In [plane stress](@entry_id:172193), it takes the form [@problem_id:2885662]:
$ F_1 \sigma_{11} + F_2 \sigma_{22} + F_{11} \sigma_{11}^2 + F_{22} \sigma_{22}^2 + F_{66} \tau_{12}^2 + 2F_{12} \sigma_{11} \sigma_{22} = 1 $

The coefficients are related to the engineering strengths:
$ F_1 = \frac{1}{X_t} - \frac{1}{X_c} \quad ; \quad F_{11} = \frac{1}{X_t X_c} $
$ F_2 = \frac{1}{Y_t} - \frac{1}{Y_c} \quad ; \quad F_{22} = \frac{1}{Y_t Y_c} $
$ F_{66} = \frac{1}{S^2} $

The key innovation of the Tsai-Wu criterion is the inclusion of **linear terms** ($F_1\sigma_{11}, F_2\sigma_{22}$). Since these terms are [odd functions](@entry_id:173259) of stress, they shift the failure ellipse in [stress space](@entry_id:199156), allowing the criterion to be calibrated to different tensile and compressive strengths. This directly addresses the main weakness of the Tsai-Hill criterion and allows it to model the [tension-compression asymmetry](@entry_id:201728) that originates from micromechanical mechanisms [@problem_id:2885627]. Its primary limitation is that the interaction coefficient $F_{12}$ cannot be determined from uniaxial tests alone and requires at least one biaxial test, introducing a degree of ambiguity if such data is unavailable [@problem_id:2885640].

#### Interactive, Mode-Dependent Criteria: The Hashin Criteria

While Tsai-Wu provides a good mathematical fit to failure data, it does not distinguish between different physical failure modes. A different class of criteria, pioneered by Zvi Hashin, addresses this by postulating separate failure functions for fiber-dominated and matrix-dominated failure. This approach is more physically based and is particularly valuable for [progressive failure analysis](@entry_id:203451).

The **Hashin Criteria** consist of a set of four distinct conditions for plane stress [@problem_id:2885652] [@problem_id:2885603]:

-   **Tensile Fiber Mode** ($\sigma_{11} \ge 0$): Failure is assumed to be an interaction between longitudinal tension and shear.
    $ \left(\frac{\sigma_{11}}{X_t}\right)^2 + \left(\frac{\tau_{12}}{S}\right)^2 \ge 1 $

-   **Compressive Fiber Mode** ($\sigma_{11}  0$): Failure is governed by fiber buckling, which is modeled as a simple compressive stress limit.
    $ |\sigma_{11}| \ge X_c $

-   **Tensile Matrix Mode** ($\sigma_{22} \ge 0$): Failure is an interaction between transverse tension and shear, leading to matrix cracking.
    $ \left(\frac{\sigma_{22}}{Y_t}\right)^2 + \left(\frac{\tau_{12}}{S}\right)^2 \ge 1 $

-   **Compressive Matrix Mode** ($\sigma_{22}  0$): Failure is governed by matrix crushing or shear, with a more complex interaction involving all three stress components. A common form is:
    $ \left(\frac{\sigma_{22}}{2S}\right)^2 + \left[ \left(\frac{Y_c}{2S}\right)^2 - 1 \right] \frac{\sigma_{22}}{Y_c} + \left(\frac{\tau_{12}}{S}\right)^2 \ge 1 $

The strength of the Hashin criteria lies in their direct connection to observable physical mechanisms. They answer not only *if* the lamina fails, but *how* it fails. This distinction is crucial when analyzing the behavior of a laminate after the initial failure of one or more plies.

### From Lamina Failure to Laminate Strength

The [failure criteria](@entry_id:195168) discussed above apply to a single lamina. In a multidirectional laminate, the failure process is more complex. We distinguish between two key events [@problem_id:2885640]:

1.  **First-Ply Failure (FPF):** This is the load at which the first ply within the laminate satisfies a given failure criterion. For typical laminates under in-plane load, FPF is usually a matrix-dominated failure (e.g., transverse cracking) in an off-axis ply, as these modes have the lowest strengths.

2.  **Last-Ply Failure (LPF):** This represents the ultimate failure of the laminate, where it loses its load-[carrying capacity](@entry_id:138018).

For most robust laminate designs, FPF is not a catastrophic event. The failed ply may lose stiffness, but the remaining plies, particularly the primary load-bearing plies (e.g., $0^\circ$ plies in a [uniaxial tension](@entry_id:188287) case), redistribute the load and continue to support the structure. The laminate can often sustain significantly more load beyond FPF. The analysis of this behavior is called **[progressive failure analysis](@entry_id:203451) (PFA)**.

The choice of lamina failure criterion has a profound impact on PFA predictions. A mode-dependent criterion like Hashin's is essential, as the predicted failure mode dictates the appropriate stiffness reduction rule to apply to the failed ply. For instance, matrix cracking would primarily reduce $E_2$ and $G_{12}$, whereas fiber fracture would reduce all stiffness components to near zero. An incorrect mode prediction leads to incorrect [stiffness degradation](@entry_id:202277), altered [stress redistribution](@entry_id:190225), and ultimately, an inaccurate prediction of the laminate's ultimate strength (LPF) [@problem_id:2885640]. This highlights the importance of selecting a failure criterion that is not only mathematically convenient but also physically sound.