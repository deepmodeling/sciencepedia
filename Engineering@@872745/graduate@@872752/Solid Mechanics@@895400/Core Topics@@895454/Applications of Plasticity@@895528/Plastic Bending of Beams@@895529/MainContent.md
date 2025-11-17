## Introduction
Understanding how structural beams behave beyond their [elastic limit](@entry_id:186242) is fundamental to modern engineering design, ensuring both safety and material efficiency. While elastic analysis predicts how structures deform under service loads, it fails to capture their true ultimate strength and post-yield behavior. The theory of [plastic bending](@entry_id:197427) addresses this gap, providing the tools to analyze the ultimate load-carrying capacity of ductile structures by accounting for permanent deformation and [stress redistribution](@entry_id:190225). This article offers a comprehensive exploration of this critical topic, guiding you from foundational principles to advanced applications.

This study is structured to build your expertise progressively. In the first chapter, **"Principles and Mechanisms,"** we will lay the groundwork, deriving the essential [moment-curvature relationship](@entry_id:180260) from core assumptions about stress states and [kinematics](@entry_id:173318), and introducing the pivotal concept of the [plastic hinge](@entry_id:200267). Next, in **"Applications and Interdisciplinary Connections,"** we will apply these principles to solve practical problems, such as determining the collapse load of structures using [limit analysis](@entry_id:188743) and exploring the interaction of bending with other forces and its connections to materials science. Finally, **"Hands-On Practices"** will provide opportunities to apply your knowledge through curated analytical and computational problems, solidifying your grasp of the material.

## Principles and Mechanisms

The transition of a structural beam from a state of purely elastic response to one involving [plastic deformation](@entry_id:139726) is a cornerstone of modern [structural engineering](@entry_id:152273). It governs not only the ultimate load-[carrying capacity](@entry_id:138018) of structures but also phenomena such as energy dissipation, permanent deformation, and the formation of residual stresses. This chapter delves into the fundamental principles and mechanisms that dictate the behavior of beams undergoing [plastic bending](@entry_id:197427). We will begin by establishing the foundational assumptions that simplify the analysis, proceed to derive the essential [moment-curvature relationship](@entry_id:180260) that characterizes sectional response, and then apply these concepts to understand structural collapse, springback, and the influence of [material memory](@entry_id:187722) effects.

### Foundational Assumptions and Their Limits

The analysis of [plastic bending](@entry_id:197427) is made tractable through a series of well-established idealizations. The most crucial of these relate to the state of stress within the beam and the kinematics of its deformation.

#### The Uniaxial Stress State in Pure Bending

For a slender, prismatic beam subjected to [pure bending](@entry_id:202969), the dominant stress component is the axial normal stress, $\sigma_{xx}$, acting parallel to the beam's axis. According to Saint-Venant's principle, far from points of load application or geometric discontinuity, all other stress components—transverse [normal stresses](@entry_id:260622) ($\sigma_{yy}$, $\sigma_{zz}$) and shear stresses ($\tau_{xy}$, $\tau_{xz}$, $\tau_{yz}$)—are negligible in comparison to $\sigma_{xx}$ [@problem_id:2670340]. While transverse strains ($\epsilon_{yy}$, $\epsilon_{zz}$) exist due to the Poisson effect, the [traction-free boundary](@entry_id:197683) conditions on the beam's lateral surfaces prevent these strains from generating significant transverse stresses in a slender member. Consequently, the stress state at any given material point, or "fiber," along the beam's length can be approximated as **uniaxial**.

This simplification is profound because it allows for the application of complex, three-dimensional [yield criteria](@entry_id:178101) in a one-dimensional form. The two most common criteria for ductile metals are the **Tresca (maximum shear stress) criterion** and the **von Mises (distortional energy) criterion**.

- The **Tresca criterion** posits that yielding occurs when the maximum shear stress, $\tau_{\max} = \frac{1}{2}(\sigma_{\max} - \sigma_{\min})$, reaches the value it has in a [uniaxial tension test](@entry_id:195375) at yield, which is $\frac{1}{2}\sigma_{y}$. Here, $\sigma_{\max}$ and $\sigma_{\min}$ are the maximum and minimum [principal stresses](@entry_id:176761), and $\sigma_{y}$ is the uniaxial [yield stress](@entry_id:274513) [@problem_id:2670340].

- The **von Mises criterion** states that yielding begins when the second invariant of the [deviatoric stress tensor](@entry_id:267642), $J_2$, reaches a critical value. This is equivalent to the von Mises effective stress, $\sigma_{vM} = \sqrt{\frac{3}{2} \boldsymbol{s}:\boldsymbol{s}}$, equaling the uniaxial yield stress $\sigma_{y}$, where $\boldsymbol{s}$ is the [deviatoric stress tensor](@entry_id:267642) [@problem_id:2670340]. This criterion is independent of [hydrostatic pressure](@entry_id:141627), reflecting the observation that pressure does not cause yielding in most metals.

For the essentially uniaxial stress state in a beam under [pure bending](@entry_id:202969), where the [principal stresses](@entry_id:176761) are $(\sigma_{xx}, 0, 0)$, both criteria elegantly reduce to the same simple condition: yielding occurs when $|\sigma_{xx}| = \sigma_{y}$ [@problem_id:2670340]. This remarkable result justifies modeling the beam as a bundle of independent, one-dimensional fibers, each following a simple uniaxial stress-strain law.

#### The Euler-Bernoulli Kinematic Hypothesis

The second foundational pillar is the kinematic assumption of **Euler-Bernoulli beam theory**, which states that **plane [cross-sections](@entry_id:168295) initially normal to the beam's axis remain plane and normal to the deflected axis after bending**. This hypothesis is a direct kinematic consequence of neglecting transverse [shear strain](@entry_id:175241), i.e., assuming $\gamma_{xz} = 0$. From the small-strain [compatibility relations](@entry_id:184577), this assumption enforces a linear distribution of [axial strain](@entry_id:160811) $\epsilon_{xx}$ through the beam's depth, $y$:
$$ \epsilon_{xx}(y) = \epsilon_{0} - y \kappa $$
where $\epsilon_{0}$ is the [axial strain](@entry_id:160811) at the reference axis ($y=0$) and $\kappa$ is the curvature of the beam. For [pure bending](@entry_id:202969) without axial force, $\epsilon_{0}=0$.

Crucially, this kinematic statement is independent of the material's [constitutive law](@entry_id:167255). It arises from geometric constraints, not from material response. Therefore, the assumption that plane sections remain plane and that [axial strain](@entry_id:160811) varies linearly across the depth remains valid even after the material begins to yield and enters the plastic regime, provided the underlying conditions for Euler-Bernoulli theory hold [@problem_id:2670386].

#### The Limits of Applicability: Shear Deformation and Instability

The elegant simplicity of the Euler-Bernoulli framework is not universally applicable. Its validity breaks down under two primary conditions: significant [shear deformation](@entry_id:170920) and cross-sectional instability.

1.  **Shear Deformation (Timoshenko Effects)**: The Euler-Bernoulli assumption of $\gamma_{xz}=0$ is valid for slender beams, where bending deformation dominates. For **short, deep beams**, the contribution of [transverse shear deformation](@entry_id:176673) to the overall compliance becomes significant. In such cases, **Timoshenko [beam theory](@entry_id:176426)** is more appropriate. It relaxes the "remain normal" constraint, allowing plane sections to rotate relative to the deflected axis, thereby accounting for shear deformation. The importance of shear can be quantified by the beam's **[slenderness ratio](@entry_id:188096)**, typically defined as the span-to-depth ratio ($L/h$). As this ratio decreases, shear effects become more pronounced [@problem_id:2670317].

    Furthermore, in very short beams, the maximum shear stress (which occurs at the neutral axis for a rectangular section) can become large enough to cause yielding. Using the von Mises criterion, it can be shown that for a simply supported rectangular beam under a central point load, shear yielding at the neutral axis will precede bending yield at the extreme fibers if the [slenderness ratio](@entry_id:188096) falls below a critical value, $L/h \le \sqrt{3}/2 \approx 0.866$ [@problem_id:2670317]. For such cases, a plastic analysis must account for the interaction between shear and bending stresses.

2.  **Local Buckling**: The "plane sections remain plane" hypothesis assumes the cross-section deforms as a rigid two-dimensional shape. This holds for solid or "compact" sections. However, for beams with **[thin-walled sections](@entry_id:193971)** (e.g., I-beams or box sections), the thin plate elements in compression can buckle locally before the full [plastic moment](@entry_id:182387) capacity of the section is reached. This **local buckling** involves out-of-plane deformation of parts of the cross-section, which constitutes a violation of the plane-section assumption [@problem_id:2670386]. Structural design codes specify compactness limits (e.g., width-to-thickness ratios for flanges and webs) to ensure that a section can reach its [plastic moment](@entry_id:182387) and sustain rotation without premature local failure.

### The Moment-Curvature Relationship for an Elastic-Perfectly Plastic Material

The macroscopic response of a beam section in bending is captured by its **moment-curvature ($M-\kappa$) relationship**. This relationship is derived by integrating the stress distribution over the cross-section, where the stress at each point is determined by the strain (from [kinematics](@entry_id:173318)) and the material's [constitutive law](@entry_id:167255). Let us derive this relationship for a rectangular cross-section of width $b$ and height $h$, made of an **elastic-perfectly plastic (EPP)** material with yield stress $\sigma_y$. This material behaves elastically up to yield and then deforms plastically at a constant stress $\sigma_y$ (zero [strain hardening](@entry_id:160233)).

The analysis proceeds through three distinct regimes as the applied bending moment, and thus the curvature, increases monotonically [@problem_id:2670345] [@problem_id:2908781].

#### Regime 1: Purely Elastic Bending

For small curvatures, the strain at every point across the section is less than the yield strain, $\epsilon_y = \sigma_y / E$. The stress is linearly proportional to the strain, $\sigma_{x}(y) = E \epsilon_{x}(y)$. Given the kinematic relation $\epsilon_{x}(y) = -\kappa y$ (for bending about the z-axis, with y positive upwards), the stress distribution is also linear: $\sigma_{x}(y) = -E\kappa y$.

The [bending moment](@entry_id:175948) $M$ is the resultant of these stresses:
$$ M = -\int_{A} y \sigma_{x}(y) \,dA = \int_{A} y (E\kappa y) \,dA = E\kappa \int_{A} y^2 \,dA = EI\kappa $$
where $I = bh^3/12$ is the [second moment of area](@entry_id:190571) for the rectangular section. The response is linear, with stiffness $EI$. This regime ends when the stress at the extreme fibers ($y = \pm h/2$) reaches the [yield stress](@entry_id:274513) $\sigma_y$. This occurs at the **[yield moment](@entry_id:182231)**, $M_y$:
$$ M_y = \frac{\sigma_y I}{h/2} = \frac{\sigma_y (bh^3/12)}{h/2} = \frac{1}{6}\sigma_y b h^2 $$
The corresponding curvature is the yield curvature, $\kappa_y = M_y / (EI) = 2\sigma_y / (Eh)$.

#### Regime 2: Elastic-Plastic Bending

Once the curvature exceeds $\kappa_y$, the strain at the outer fibers surpasses $\epsilon_y$. These regions yield, forming **plastic zones**. However, an **elastic core** persists in the central part of the beam, where $|y|  y_e$ and the strain magnitude is still below $\epsilon_y$. The boundary of this core, $y_e$, is defined by the condition $|\epsilon_x(y_e)| = \kappa y_e = \epsilon_y$, which gives $y_e = \epsilon_y / \kappa = \sigma_y / (E\kappa)$. As curvature $\kappa$ increases, the elastic core shrinks.

The stress distribution in this regime is piecewise [@problem_id:2670345]:
- **Elastic core ($|y| \le y_e$)**: $\sigma_{x}(y) = -E\kappa y$
- **Plastic zones ($y_e  |y| \le h/2$)**: $\sigma_{x}(y) = -\text{sign}(y)\sigma_y$

The bending moment is found by integrating this composite stress profile:
$$ M = -\int_{A} y \sigma_{x}(y) \,dA = 2b \left[ \int_{0}^{y_e} y(E\kappa y) \,dy + \int_{y_e}^{h/2} y(\sigma_y) \,dy \right] $$
Evaluating the integrals and substituting $y_e = \sigma_y/(E\kappa)$ yields the nonlinear [moment-curvature relation](@entry_id:181076) for the elastic-plastic regime:
$$ M(\kappa) = \frac{\sigma_y b h^2}{4} - \frac{b \sigma_y^3}{3E^2\kappa^2} $$
This expression shows that as curvature increases, the moment asymptotically approaches an upper limit.

#### Regime 3: Fully Plastic Bending

The theoretical limit as curvature approaches infinity ($\kappa \to \infty$) corresponds to the elastic core shrinking to zero ($y_e \to 0$). At this point, the entire cross-section has yielded. The stress distribution becomes a simple rectangular block: $\sigma_x(y) = -\sigma_y$ for $y > 0$ and $\sigma_x(y) = +\sigma_y$ for $y  0$.

The moment corresponding to this state is the **fully [plastic moment](@entry_id:182387)**, $M_p$. It can be found either by taking the limit of the elastic-plastic expression as $\kappa \to \infty$ or by direct integration of the fully plastic stress distribution [@problem_id:2908781]:
$$ M_p = \lim_{\kappa \to \infty} \left( \frac{\sigma_y b h^2}{4} - \frac{b \sigma_y^3}{3E^2\kappa^2} \right) = \frac{1}{4}\sigma_y b h^2 $$
At this stage, the section can no longer sustain additional moment; it deforms at a constant moment $M_p$, acting as a "hinge".

### The Shape Factor and Plastic Reserve Capacity

The ability of a cross-section to resist [bending moment](@entry_id:175948) beyond its initial yield is a crucial aspect of plastic design. This reserve capacity is quantified by the **shape factor**, $k$ (or $\phi$ in some literature), defined as the ratio of the fully [plastic moment](@entry_id:182387) to the [yield moment](@entry_id:182231) [@problem_id:2670374].

$$ k = \frac{M_p}{M_y} $$

Using our derived expressions for a rectangular section:
$$ k_{\text{rect}} = \frac{\frac{1}{4}\sigma_y b h^2}{\frac{1}{6}\sigma_y b h^2} = \frac{6}{4} = 1.5 $$
This means a rectangular beam can withstand a 50% increase in moment from the point of first yield until it becomes fully plastic. The [shape factor](@entry_id:149022) is a purely geometric property, independent of the material's [yield stress](@entry_id:274513). For a solid circular section, a similar derivation yields $k_{\text{circ}} = \frac{16}{3\pi} \approx 1.70$ [@problem_id:2670374].

The calculation of $M_p$ relies on identifying the **Plastic Neutral Axis (PNA)**. The PNA is the axis that divides the cross-sectional area into two equal halves, one in tension ($A_t$) and one in compression ($A_c$), to satisfy the zero axial force condition ($N = \sigma_y A_t - \sigma_y A_c = 0$). For sections that are symmetric about the bending axis, the PNA coincides with the centroidal (elastic) neutral axis [@problem_id:2670374]. For asymmetric sections, the PNA shifts away from the [centroid](@entry_id:265015).

It is critical to note that a large [shape factor](@entry_id:149022), while indicating a significant reserve of strength, does not necessarily guarantee high rotational [ductility](@entry_id:160108) at the [plastic hinge](@entry_id:200267). As mentioned earlier, [thin-walled sections](@entry_id:193971) with high shape factors may be susceptible to local [buckling](@entry_id:162815), which can limit their ability to sustain [large rotations](@entry_id:751151) before losing strength [@problem_id:2670374].

### The Plastic Hinge: Idealization and Application

The concept of the **[plastic hinge](@entry_id:200267)** is central to the simplified analysis of structural collapse, known as **[limit analysis](@entry_id:188743)**.

#### The Idealized Hinge and the Plastic Zone

For an EPP material, the $M-\kappa$ curve becomes horizontal at $M=M_p$. This implies that once a section reaches its fully [plastic moment](@entry_id:182387), it can undergo indefinitely large curvature (and thus rotation) with no increase in moment. Now, consider a beam where the [bending moment](@entry_id:175948) $M(x)$ varies along its length, with a single peak. As the load increases, the moment at the peak location will reach $M_p$. Due to the moment gradient ($dM/dx \neq 0$), adjacent sections will have moments less than $M_p$ and thus finite curvature. All inelastic rotation becomes concentrated at the single point where $M(x)=M_p$. This idealization of finite rotation occurring over an infinitesimal length is the **zero-length [plastic hinge](@entry_id:200267)** [@problem_id:2670332].

This idealized hinge should not be confused with the **[plastic zone](@entry_id:191354) length**. The plastic zone is the finite region of the beam over which yielding has occurred, i.e., the region where $M(x) \ge M_y$. The idealized [plastic hinge](@entry_id:200267) of [limit analysis](@entry_id:188743) is a point, while the [physical region](@entry_id:160106) of yielding has a finite length [@problem_id:2670332].

In contrast, for a material that exhibits **[strain hardening](@entry_id:160233)** ($E_t > 0$), the $M-\kappa$ curve never becomes perfectly horizontal. The moment capacity continues to increase with curvature. Consequently, infinite curvature is not possible at any finite moment. The plastic rotation is "smeared" over a finite region of concentrated inelastic curvature, and no zero-length hinge forms. The "hinge" is now a diffuse zone [@problem_id:2670332].

#### Limit Analysis Theorems and Structural Collapse

The [plastic hinge](@entry_id:200267) model enables the prediction of the ultimate collapse load of a structure through the **theorems of [limit analysis](@entry_id:188743)**. For a structure made of a [rigid-perfectly plastic](@entry_id:195711) material, these theorems state [@problem_id:2670349]:

1.  **Lower Bound (Static) Theorem**: Any load calculated from a bending moment distribution that is in equilibrium with the external loads and does not exceed the [plastic moment](@entry_id:182387) capacity at any point ($|M(x)| \le M_p$) is less than or equal to the true collapse load. It provides a "safe" estimate of the load capacity.

2.  **Upper Bound (Kinematic) Theorem**: Any load calculated by equating the external work done by the loads to the internal energy dissipated in an assumed, kinematically admissible collapse mechanism is greater than or equal to the true collapse load. It provides an "unsafe" estimate.

A structure becomes a **mechanism** when a sufficient number of plastic hinges form to permit [rigid-body motion](@entry_id:265795). For a statically indeterminate beam of degree $n$, collapse typically requires the formation of $n+1$ hinges.

As a practical example, consider a propped [cantilever beam](@entry_id:174096) of span $L$ under a uniformly distributed load $w$. This beam is statically indeterminate to the first degree, so two hinges are required for collapse. One will form at the fixed support (maximum negative moment), and the other will form in the span (maximum positive moment). By assuming a mechanism and using the [upper bound theorem](@entry_id:185343), one can find the position of the span hinge that minimizes the calculated collapse load. For this case, the in-span hinge forms at $x = (2-\sqrt{2})L$ from the fixed support, and the unique collapse load is found to be $w_c = \frac{(6+4\sqrt{2})M_p}{L^2}$ [@problem_id:2670349]. This exact solution is confirmed when the [lower bound theorem](@entry_id:186840) yields the same load for a statically admissible moment field that reaches $\pm M_p$ at the hinge locations.

### Unloading, Residual Stresses, and the Bauschinger Effect

Plastic deformation is, by definition, permanent. However, the process of unloading and the state of the material after loading are governed by elastic principles and reveal further complexities of material behavior.

#### Springback and Residual Stresses

When a beam that has been plastically deformed is unloaded, it does not retrace its loading path on the $M-\kappa$ diagram. Instead, the unloading is assumed to be purely **elastic**, with a stiffness of $EI$. This means the change in moment, $\Delta M = -M_{\text{applied}}$, induces a corresponding linear change in curvature, $\Delta \kappa = \Delta M / (EI)$ [@problem_id:2670326].

This elastic recovery of curvature results in **springback**, a partial recovery of the beam's deformation. The total deformation at peak load is the sum of elastic and plastic parts. Upon unloading, only the elastic portion is recovered. The springback rotation at the end of a cantilever, for instance, can be calculated by integrating the elastic change in curvature along the beam's length [@problem_id:2670326].

After the external load is fully removed, the net moment on any cross-section is zero. However, this does not mean the stress is zero everywhere. The stress distribution from [plastic loading](@entry_id:753518), superimposed with the linear elastic stress distribution from unloading, results in a self-equilibrating **[residual stress](@entry_id:138788)** field. These internal stresses can be significant, with some fibers in compression and others in tension, and can have a major influence on the subsequent fatigue life and buckling strength of the member.

#### The Bauschinger Effect and Kinematic Hardening

The standard EPP model assumes the yield stress $\sigma_y$ is a fixed material constant. However, for many real materials, [plastic deformation](@entry_id:139726) in one direction affects the yield strength in the reverse direction. This phenomenon is known as the **Bauschinger effect**: after being pulled into the plastic range in tension, a material will exhibit a reduced [yield stress](@entry_id:274513) when subsequently loaded in compression.

This behavior is captured by more sophisticated material models, such as those incorporating **[kinematic hardening](@entry_id:172077)**. In these models, the yield surface in [stress space](@entry_id:199156) does not just expand ([isotropic hardening](@entry_id:164486)) but also translates. The center of the yield surface is described by a **backstress** tensor, $\alpha$. The yield condition becomes $|\sigma - \alpha| = \sigma_y$. The [backstress](@entry_id:198105) $\alpha$ evolves with plastic strain, effectively tracking the history of deformation.

During reverse loading of a beam, the presence of a backstress developed during forward loading causes yielding to initiate earlier than it would in a virgin material. For a beam section, this means the reverse-[yield moment](@entry_id:182231) is altered. It can be shown that the change in the reverse-[yield moment](@entry_id:182231) due solely to the Bauschinger effect, as captured by a [backstress](@entry_id:198105) $\alpha$ at the extreme fiber, is given by $\Delta M_{\text{rev}} = \alpha S$, where $S$ is the elastic section modulus [@problem_id:2670344]. This earlier onset of reverse plasticity has a significant impact on the [residual stress](@entry_id:138788) distribution and is a critical consideration in applications involving [cyclic loading](@entry_id:181502), such as seismic design and [metal forming](@entry_id:188560).