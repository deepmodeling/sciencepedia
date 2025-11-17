## Introduction
The interaction between a liquid and a solid surface—the phenomenon of wetting—governs processes as diverse as a raindrop on a leaf and the fabrication of advanced microchips. While the concept of a contact angle is familiar, a deeper understanding requires bridging the gap between idealized models and the complexities of real-world materials and dynamic conditions. This article provides a comprehensive exploration of [wetting phenomena](@entry_id:201207), designed for a graduate-level audience across the physical sciences and engineering. The journey begins in the **Principles and Mechanisms** chapter, where we establish the thermodynamic and mechanical foundations, starting with Young's equation for an ideal surface and progressively introducing complexities like surface roughness, chemical heterogeneity, and the dynamics of moving contact lines. Next, the **Applications and Interdisciplinary Connections** chapter demonstrates the profound utility of these principles, showcasing how they are harnessed to engineer [superhydrophobic surfaces](@entry_id:148368), optimize industrial processes, and understand biological systems. Finally, the **Hands-On Practices** section allows you to apply this theoretical knowledge to solve quantitative problems. Let us begin by delving into the core principles that dictate equilibrium and motion at the three-phase contact line.

## Principles and Mechanisms

The phenomenon of [wetting](@entry_id:147044), where a liquid makes contact with a solid surface, is governed by a delicate interplay of [molecular forces](@entry_id:203760) at the interfaces between the three phases involved: solid (S), liquid (L), and vapor (V). Understanding the principles that dictate the equilibrium shape of a liquid droplet and the mechanisms that drive its motion or the rupture of a thin film is fundamental to numerous applications in polymer science, materials engineering, and biology. This chapter elucidates these core principles, beginning with the idealized equilibrium at a three-phase contact line and progressively incorporating the complexities of real surfaces, substrate compliance, and dynamic processes.

### The Ideal Equilibrium: Young's Equation

The cornerstone of static [wetting phenomena](@entry_id:201207) is the concept of **[interfacial tension](@entry_id:271901)**, denoted by the symbol $\gamma$. Interfacial tension can be conceptualized from two equivalent perspectives. Thermodynamically, it is the excess Gibbs free energy per unit area associated with creating an interface between two immiscible phases. Mechanically, it can be viewed as a force per unit length acting tangentially along the interface, tending to minimize its area. For a system comprising a solid, a liquid, and its vapor, we define three such tensions: $\gamma_{sv}$ for the solid-vapor interface, $\gamma_{sl}$ for the [solid-liquid interface](@entry_id:201674), and $\gamma_{lv}$ for the liquid-vapor interface.

When a liquid droplet is placed on a solid surface, it forms a **three-phase contact line** where the solid, liquid, and vapor meet. The equilibrium shape of the droplet, specifically the angle it makes with the substrate, is determined by the balance of these interfacial tensions. Let us consider an idealized system: a small liquid droplet on a rigid, perfectly smooth, and chemically homogeneous solid substrate, where gravitational effects are negligible [@problem_id:2937801].

The equilibrium condition can be derived by considering the mechanical force balance on an infinitesimal segment of the contact line. The tension $\gamma_{sv}$ pulls the contact line along the dry substrate, promoting spreading. This is counteracted by the solid-liquid tension $\gamma_{sl}$, which pulls the contact line inward under the droplet, and the horizontal component of the liquid-vapor tension, which also pulls inward. The liquid-vapor interface meets the solid at the **[contact angle](@entry_id:145614)**, $\theta$, defined as the angle within the liquid phase. The horizontal component of the force exerted by the liquid-vapor interface is therefore $\gamma_{lv}\cos\theta$ per unit length. For the contact line to be in static equilibrium, the net horizontal force must be zero:

$\gamma_{sv} - \gamma_{sl} - \gamma_{lv}\cos\theta = 0$

Rearranging this force balance yields the celebrated **Young's equation**:

$\gamma_{sv} = \gamma_{sl} + \gamma_{lv}\cos\theta$

Alternatively, we can write:

$\cos\theta = \frac{\gamma_{sv} - \gamma_{sl}}{\gamma_{lv}}$

This fundamental equation dictates that the equilibrium contact angle on an ideal surface is determined solely by the three interfacial tensions. The vertical component of the liquid-vapor tension, $\gamma_{lv}\sin\theta$, exerts an upward pull on the substrate. In our idealized rigid solid, this force is simply balanced by an elastic reaction from the solid and does not influence the [contact angle](@entry_id:145614).

### Thermodynamic Classification of Wetting Regimes

While Young's equation provides the [contact angle](@entry_id:145614) for a stable droplet, it does not predict whether a droplet will form in the first place. A more general thermodynamic criterion is provided by the **spreading parameter**, $S$. The spreading parameter is defined as the negative of the change in Gibbs free energy per unit area when a dry solid surface is covered by a thin [liquid film](@entry_id:260769). Initially, we have a unit area of solid-vapor interface with energy $\gamma_{sv}$. In the final state, this is replaced by a unit area of [solid-liquid interface](@entry_id:201674) (energy $\gamma_{sl}$) and a unit area of liquid-vapor interface (energy $\gamma_{lv}$). Thus, $S$ is given by:

$S = \gamma_{sv} - (\gamma_{sl} + \gamma_{lv})$

The sign of the spreading parameter dictates the wetting regime [@problem_id:2937762]:

1.  **Complete Wetting**: If $S > 0$, the free energy of the system is lowered by replacing the solid-vapor interface with a solid-liquid and a liquid-vapor interface. Spreading is thermodynamically spontaneous, and the liquid will form a thin film that covers the entire substrate. The macroscopic [contact angle](@entry_id:145614) is $\theta=0$. This corresponds to the case in Young's equation where $(\gamma_{sv} - \gamma_{sl})/\gamma_{lv} > 1$, which has no solution for a real angle $\theta$. The spreading force can never be balanced by the surface tension component, leading to continuous spreading. The boundary condition $S=0$ corresponds to $\theta=0$.

2.  **Partial Wetting**: If $S \le 0$, it is energetically unfavorable for the liquid to spread into a film. Instead, the liquid forms a discrete droplet with a finite equilibrium [contact angle](@entry_id:145614) $\theta > 0$, as described by Young's equation. For the partial wetting regime, we can substitute $\gamma_{sv} - \gamma_{sl}$ from Young's equation into the definition of $S$ to find a direct relationship between $S$ and $\theta$:

    $S = (\gamma_{lv}\cos\theta + \gamma_{sl}) - (\gamma_{sl} + \gamma_{lv}) = \gamma_{lv}(\cos\theta - 1)$

    Since $\gamma_{lv} > 0$ and $\cos\theta \le 1$ for any real angle, this confirms that partial [wetting](@entry_id:147044) (where $\theta > 0$) is associated with $S  0$. The limit of non-[wetting](@entry_id:147044) is approached as $\theta \to \pi$, where $S$ approaches its most negative value, $-2\gamma_{lv}$.

As an illustrative example, consider a polymer melt with $\gamma_{lv} = 30\,\mathrm{mN/m}$ on two different substrates. For substrate X with $\gamma_{sv} = 54\,\mathrm{mN/m}$ and $\gamma_{sl} = 22\,\mathrm{mN/m}$, the spreading parameter is $S_X = 54 - (22 + 30) = +2\,\mathrm{mN/m}$. Since $S_X > 0$, the melt will completely wet substrate X. For substrate Y with $\gamma_{sv} = 20\,\mathrm{mN/m}$ and $\gamma_{sl} = 16\,\mathrm{mN/m}$, the spreading parameter is $S_Y = 20 - (16 + 30) = -26\,\mathrm{mN/m}$. Since $S_Y  0$, the melt will partially wet substrate Y, forming a droplet with a contact angle given by $\cos\theta_Y = (20-16)/30 \approx 0.133$, or $\theta_Y \approx 82.3^\circ$ [@problem_id:2937762].

### Deviations from Ideality I: Surface Heterogeneity and Hysteresis

Real surfaces are never perfectly smooth or chemically uniform. These imperfections, or defects, give rise to the phenomenon of **[contact angle hysteresis](@entry_id:148697)**. On a real surface, the [contact angle](@entry_id:145614) is not a single value but can exist within a range. This is observed when, for example, the volume of a droplet is slowly increased and then decreased. The contact line may remain "pinned" by [surface defects](@entry_id:203559), and the contact angle will change until a critical value is reached, at which point the contact line suddenly advances or recedes.

The maximum angle observed just before the contact line advances is the **advancing contact angle**, $\theta_A$. The minimum angle observed just before the contact line recedes is the **receding contact angle**, $\theta_R$. The difference, $\Delta\theta = \theta_A - \theta_R$, is the [contact angle hysteresis](@entry_id:148697).

The physical origin of this phenomenon can be understood by considering the balance between the thermodynamic driving force for contact line motion and the pinning force exerted by defects [@problem_id:2937798]. The capillary driving force per unit length, $f_{cap}$, which pushes the contact line outward, can be derived from the variation of the total [interfacial free energy](@entry_id:183036):

$f_{cap} = \gamma_{sv} - \gamma_{sl} - \gamma_{lv}\cos\theta$

Using the ideal Young's angle, $\theta_Y$, which would be observed on a defect-free surface of the same average chemistry ($\gamma_{sv} - \gamma_{sl} = \gamma_{lv}\cos\theta_Y$), this force can be rewritten as:

$f_{cap} = \gamma_{lv}(\cos\theta_Y - \cos\theta)$

Surface defects (topographical or chemical) create local energy barriers that resist the motion of the contact line. This can be modeled as a rate-independent threshold or **pinning force** per unit length, $f_p$. The contact line will remain pinned and the droplet is in a metastable state as long as the magnitude of the capillary driving force does not exceed this pinning force:

$|f_{cap}| \le f_p \quad \Rightarrow \quad \gamma_{lv}|\cos\theta_Y - \cos\theta| \le f_p$

The limits of this metastable range are defined by the depinning conditions. The advancing angle $\theta_A$ is reached when the outward driving force just overcomes pinning, $\gamma_{lv}(\cos\theta_Y - \cos\theta_A) = f_p$. The receding angle $\theta_R$ is reached when the inward driving force overcomes pinning, $\gamma_{lv}(\cos\theta_R - \cos\theta_Y) = f_p$. Thus, [hysteresis](@entry_id:268538) provides a direct measure of the pinning strength of the surface heterogeneities.

### Deviations from Ideality II: The Role of Surface Topography

Geometric roughness has a profound and predictable effect on the apparent contact angle. The nature of this effect depends on whether the liquid fully penetrates the [surface texture](@entry_id:185258) or rests on top of it, trapping pockets of vapor.

#### Homogeneous Wetting: The Wenzel State

When a liquid completely impregnates the rough features of a chemically homogeneous surface, the system is said to be in the **Wenzel state**. The key parameter is the **roughness factor**, $r$, defined as the ratio of the actual surface area to the projected planar area ($r = A_{actual}/A_{projected}$). By definition, $r \ge 1$, with $r=1$ representing a perfectly smooth surface.

To find the apparent [contact angle](@entry_id:145614), $\theta_W$, we can again use an energy minimization argument [@problem_id:2937780]. Consider a virtual advance of the contact line over a projected area $\delta A_p$. The actual solid-liquid area increases by $r\delta A_p$, and the solid-vapor area decreases by the same amount. The liquid-vapor area changes according to the macroscopic geometry, by $\delta A_p \cos\theta_W$. The change in total free energy, $dG$, is:

$dG = (\gamma_{sl} \cdot r\delta A_p) - (\gamma_{sv} \cdot r\delta A_p) + (\gamma_{lv} \cdot \delta A_p \cos\theta_W)$

Setting $dG=0$ at equilibrium and dividing by $\delta A_p$ gives:

$r(\gamma_{sv} - \gamma_{sl}) = \gamma_{lv}\cos\theta_W$

Substituting the expression for $\gamma_{sv} - \gamma_{sl}$ from Young's equation, we arrive at **Wenzel's equation**:

$\cos\theta_W = r\cos\theta_Y$

Since $r > 1$, Wenzel's equation predicts that roughness amplifies the intrinsic [wettability](@entry_id:190960) of the surface. If the smooth surface is hydrophilic ($\theta_Y  90^\circ$, so $\cos\theta_Y > 0$), roughness makes it more hydrophilic ($\cos\theta_W > \cos\theta_Y$, so $\theta_W  \theta_Y$). If the smooth surface is hydrophobic ($\theta_Y > 90^\circ$, so $\cos\theta_Y  0$), roughness makes it more hydrophobic ($\cos\theta_W  \cos\theta_Y$, so $\theta_W > \theta_Y$) [@problem_id:2937803]. Note that in the Wenzel state, a hydrophilic surface always remains hydrophilic, and a hydrophobic one remains hydrophobic.

#### Heterogeneous Wetting: The Cassie-Baxter State

On many textured surfaces, particularly those designed for water repellency, the liquid does not penetrate the roughness but rests on the "peaks" of the texture, trapping vapor in the "valleys." This is known as the **Cassie-Baxter state** or a composite state. The surface seen by the droplet is a mosaic of solid and vapor.

Let $f_s$ be the area fraction of the solid tops in contact with the liquid, and $f_v = 1-f_s$ be the area fraction of the trapped vapor. The apparent [contact angle](@entry_id:145614), $\theta_{CB}$, is then a weighted average of the contact angles on the two components. The contact angle on the solid is $\theta_Y$, and the contact angle on the trapped vapor (a liquid-vapor interface) is effectively $180^\circ$. **Cassie-Baxter's equation** is:

$\cos\theta_{CB} = f_s \cos\theta_Y + f_v \cos(180^\circ) = f_s \cos\theta_Y - (1-f_s)$

This equation reveals the principle behind superhydrophobicity. Even if a material is intrinsically only mildly hydrophobic or even hydrophilic ($\theta_Y \le 90^\circ$), if the texture is designed such that the solid fraction $f_s$ is very small, the second term, $-(1-f_s)$, dominates. This term is large and negative, driving $\cos\theta_{CB}$ to be strongly negative and thus pushing $\theta_{CB}$ to values well above $150^\circ$. For example, for a surface with $\theta_Y = 80^\circ$ and a solid fraction $f_s = 0.1$, the predicted Cassie-Baxter angle is $\theta_{CB} \approx 152^\circ$, a state of extreme water repellency [@problem_id:2937803].

#### Stability of Wetting States

For a given textured surface, both the Wenzel and Cassie-Baxter states may be possible. The thermodynamically stable state is the one with the lower global free energy. However, the Cassie-Baxter state, even if it is only metastable, is often the desired state for applications like [self-cleaning surfaces](@entry_id:147929). The transition from the Cassie-Baxter to the Wenzel state requires the liquid to overcome a pressure barrier and impregnate the texture. This barrier can be made very large by using **re-entrant geometry** (e.g., mushroom-shaped posts). Such a geometry creates an overhang that forces the liquid meniscus to adopt a highly unfavorable shape to penetrate, creating a large positive [capillary entry pressure](@entry_id:747114) barrier, $\Delta P_c \sim \gamma_{lv}/a$, where $a$ is the characteristic size of the opening. This pressure barrier can kinetically trap the system in the composite Cassie-Baxter state, even on intrinsically hydrophilic surfaces [@problem_id:2937803].

### Advanced Topics in Static Wetting

The classical model of [wetting](@entry_id:147044) can be extended by relaxing its core assumptions. Two important extensions involve including the energetic cost of the contact line itself and considering the deformability of the substrate.

#### Line Tension

Young's equation treats the contact line as a geometric entity with no energy of its own. However, at the molecular level, the environment of a molecule at the three-[phase line](@entry_id:269561) is different from that at any of the three pairwise interfaces. This gives rise to an excess free energy per unit length of the contact line, known as **line tension**, $\tau$. If $\tau$ is positive, the system must pay an energetic penalty to create a longer contact line.

This additional energy term modifies the [force balance](@entry_id:267186) at the contact line. For a curved contact line, the line tension creates a force per unit length, analogous to Laplace pressure, that acts towards the [center of curvature](@entry_id:270032) to shrink the line. For a circular contact line of radius $a$, the curvature is $1/a$, and this force is $\tau/a$. This force acts radially inward, aiding the solid-liquid tension. The modified Young's equation becomes [@problem_id:2937790]:

$\gamma_{sv} = \gamma_{sl} + \gamma_{lv}\cos\theta + \frac{\tau}{a}$

or, rearranged:

$\gamma_{lv}\cos\theta = \gamma_{sv} - \gamma_{sl} - \frac{\tau}{a}$

A key consequence is that the [contact angle](@entry_id:145614) becomes dependent on the droplet size (or contact line radius $a$). For a positive line tension, smaller droplets (smaller $a$) will exhibit larger contact angles as the system tries to minimize the energetic cost of the contact line. The effect of [line tension](@entry_id:271657) is typically negligible for macroscopic droplets but can become significant at the nano- or micro-scale.

#### Wetting on Soft Substrates: Elastocapillarity

When a liquid wets a soft, compliant solid like a polymer gel, the assumption of a rigid substrate breaks down. The vertical component of the liquid-vapor tension, $\gamma_{lv}\sin\theta$, is no longer balanced by a passive elastic reaction but actively deforms the substrate, pulling up a "[wetting](@entry_id:147044) ridge" at the contact line. This coupling of elasticity and capillarity is known as **[elastocapillarity](@entry_id:190262)**.

A crucial parameter in this regime is the **[elastocapillary length](@entry_id:203090)**, $L_{ec}$. This [intrinsic length scale](@entry_id:750789) arises from balancing the capillary energy driving the deformation with the elastic energy cost of storing strain in the solid. By minimizing the total energy, which scales as $\Delta U_{total} \sim E u^2 - \gamma_{lv} u$ (where $E$ is the Young's modulus and $u$ is the vertical deformation), we find that the characteristic deformation size is $u \sim \gamma_{lv}/E$. This defines the [elastocapillary length](@entry_id:203090) [@problem_id:2937778]:

$L_{ec} = \frac{\gamma_{lv}}{E}$

For a soft material, this length scale can be substantial. For instance, for a water droplet ($\gamma_{lv} \approx 72\,\mathrm{mN/m}$) on a soft polymer gel with $E = 3\,\mathrm{kPa}$, the [elastocapillary length](@entry_id:203090) is $L_{ec} = (72 \times 10^{-3} \mathrm{N/m}) / (3 \times 10^3 \mathrm{N/m^2}) = 24\,\mu\mathrm{m}$. The [elastocapillary length](@entry_id:203090) sets the scale of the wetting ridge. At observation scales smaller than or comparable to $L_{ec}$, the substrate deformation is significant and alters the local geometry at the contact line. However, for a droplet whose radius $R$ is much larger than $L_{ec}$, this localized deformation is a small perturbation to the overall droplet shape. Consequently, the apparent macroscopic contact angle, measured far from the ridge, remains well-described by the classical force balance of Neumann's triangle, which is equivalent to Young's equation for the horizontal components.

### Dynamics of Wetting and Dewetting

The principles discussed so far describe static equilibrium. The dynamics of how this equilibrium is approached, involving moving contact lines and evolving films, introduce new and profound physical challenges.

#### The Moving Contact Line and the Huh-Scriven Paradox

Consider a liquid spreading on a solid surface. This requires the contact line to move. A fundamental problem arises when one combines the standard **[no-slip boundary condition](@entry_id:186229)** of [fluid mechanics](@entry_id:152498) (which states that the fluid velocity at a solid boundary is zero relative to the boundary) with the continuum description of the flow. In a reference frame moving with the contact line, the solid substrate moves with velocity $U$, while the liquid far from the substrate is at rest. The no-slip condition requires the fluid molecules at the contact line to simultaneously have the velocity of the solid and the velocity of the bulk liquid, a clear contradiction.

This kinematic incompatibility leads to a dynamic catastrophe: the **Huh-Scriven paradox**. A [scaling analysis](@entry_id:153681) of the incompressible Stokes flow in the wedge-shaped region near the moving contact line shows that the velocity gradients, and thus the shear rate $\dot{\gamma}$, must diverge as $1/r$, where $r$ is the distance to the contact line. The rate of [viscous dissipation](@entry_id:143708) per unit volume, which scales as $\eta \dot{\gamma}^2$ (where $\eta$ is viscosity), therefore diverges as $1/r^2$. The total power dissipated, found by integrating the dissipation density over the volume, diverges logarithmically: $\Phi \sim \eta U^2 \ln(L/r_{min})$, where $L$ is a macroscopic outer cutoff and $r_{min}$ is a microscopic inner cutoff [@problem_id:2937776]. An infinite dissipation implies an infinite force is needed to move the contact line, which is unphysical.

This paradox signals a breakdown of the continuum model with the no-slip condition at the contact line. The singularity must be regularized by new physics at a small inner length scale. One of the most common regularization mechanisms is to relax the [no-slip condition](@entry_id:275670) and allow for fluid slip at the solid boundary. In the **Navier slip model**, the slip velocity is proportional to the shear rate at the wall, with the proportionality constant being the **[slip length](@entry_id:264157)**, $b$. This modification effectively cuts off the divergence of the shear rate at length scales $r \lesssim b$. The total dissipation becomes finite and scales as $\Phi \sim \eta U^2 \ln(L/b)$, replacing the unphysical cutoff $r_{min}$ with a physical material parameter, the [slip length](@entry_id:264157) $b$.

#### Physical Origins of Dissipation and Cutoff Scales

The logarithmic dependence on the ratio of length scales, $\ln(L/\ell)$, is a robust feature of moving contact line problems [@problem_id:2937783]. It arises because the viscous dissipation per decade of distance from the contact line is roughly constant. The key question then becomes: what physical mechanism sets the microscopic inner cutoff length, $\ell$? Several mechanisms are plausible, especially in polymeric liquids:
*   **Navier Slip**: As discussed, a finite [slip length](@entry_id:264157) $\ell \sim b$ provides a natural cutoff.
*   **Precursor Films**: In many [wetting](@entry_id:147044) systems, the macroscopic droplet is preceded by a molecularly thin "precursor film". The existence of this film, stabilized by [disjoining pressure](@entry_id:199520), removes the mathematical contact line altogether. The [cutoff scale](@entry_id:748127) becomes the precursor film thickness, $\ell \sim h_*$.
*   **Diffuse Interfaces**: Phase-field models (e.g., Cahn-Hilliard) describe interfaces not as sharp boundaries but as regions of finite thickness, $\xi$. This diffuse interface provides another natural cutoff, $\ell \sim \xi$.
*   **Rheological Effects**: For polymer melts, which are often viscoelastic, the Newtonian fluid approximation can break down near the contact line where shear rates are high. The Deborah number, $\mathrm{De} = \lambda \dot{\gamma}$ (where $\lambda$ is the polymer relaxation time), can become of order one. This defines a length scale $\ell \sim U\lambda$ below which the fluid response is predominantly elastic, not viscous, providing a speed-dependent regularization of the Newtonian singularity [@problem_id:2937783].

#### Thin Film Instability and Dewetting

Wetting dynamics also encompass the stability and rupture of thin liquid films. A thin polymer film on a non-wettable substrate is often in a metastable state. The evolution of this film is governed by the interplay of capillary forces, which tend to smooth out the surface, and long-range [intermolecular forces](@entry_id:141785) (e.g., van der Waals), which can be either stabilizing or destabilizing. These [long-range forces](@entry_id:181779) are captured by the **[disjoining pressure](@entry_id:199520)**, $\Pi(h)$, defined as the [excess pressure](@entry_id:140724) in a film of thickness $h$ relative to the bulk liquid. It is related to the effective interface potential $\phi(h)$ by $\Pi(h) = -d\phi/dh$.

The stability of the film to infinitesimal thickness fluctuations is determined by the sign of the derivative of the [disjoining pressure](@entry_id:199520), $\Pi'(h) = - \phi''(h)$ [@problem_id:2937765].
*   **Spinodal Dewetting**: If $\Pi'(h_0) > 0$ for a film of initial thickness $h_0$, the free energy is at a local maximum, and the film is linearly unstable. Small thermal fluctuations in a specific band of wavelengths will grow exponentially, leading to spontaneous rupture of the film. This process, known as [spinodal dewetting](@entry_id:182958), results in a characteristic, often bicontinuous, pattern with a well-defined length scale determined by the competition between destabilizing [intermolecular forces](@entry_id:141785) and stabilizing surface tension.
*   **Nucleated Dewetting**: If $\Pi'(h_0) \le 0$, the film is linearly stable or metastable. Rupture requires overcoming a finite energy barrier to form a dry patch or hole. This process is typically initiated at defects (dust, scratches, chemical impurities) that lower the [nucleation barrier](@entry_id:141478), a process called [heterogeneous nucleation](@entry_id:144096). In this case, the spatial pattern of dewetting is determined not by an [intrinsic length scale](@entry_id:750789) but by the random distribution of [surface defects](@entry_id:203559).

Crucially, the kinetic pathway—be it spinodal or nucleated—determines the morphology and timescale of dewetting, but not the final [equilibrium state](@entry_id:270364). Once the film has ruptured and the liquid has collected into macroscopic droplets, their final shape is governed by thermodynamic equilibrium. The equilibrium contact angle of these droplets will be the same regardless of the dewetting mechanism, as it is uniquely determined by the interfacial tensions via Young's equation [@problem_id:2937765].