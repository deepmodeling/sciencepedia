## Introduction
Beyond describing forces between charges, Maxwell's equations reveal a deeper reality: electric and magnetic fields are physical entities that store and transport energy and momentum. While the concept of energy in fields is a cornerstone of electromagnetism, the idea that fields themselves possess momentum is far more subtle and profound. This property is not a mere theoretical curiosity; it is essential for upholding the fundamental law of [momentum conservation](@entry_id:149964) and has tangible consequences that are observable from microscopic scales to astrophysical phenomena. This article delves into the theory and application of momentum in [electromagnetic fields](@entry_id:272866).

This article unpacks this fascinating topic across three chapters. First, in **"Principles and Mechanisms"**, we will establish the fundamental definition of momentum density and explore the surprising fact that even static fields can store momentum. We will then examine how this concept resolves apparent paradoxes in classical mechanics through the idea of "[hidden momentum](@entry_id:266575)." Next, in **"Applications and Interdisciplinary Connections"**, we will see how [field momentum](@entry_id:267786) manifests as real-world forces, driving technologies like [optical tweezers](@entry_id:157699) and [solar sails](@entry_id:273839) and reshaping our understanding of energy flow in simple circuits. Finally, the **"Hands-On Practices"** section will provide a set of guided problems to solidify your understanding by applying these principles to concrete physical scenarios.

## Principles and Mechanisms

One of the most profound insights of Maxwell's theory is that [electromagnetic fields](@entry_id:272866) are not mere mathematical constructs but physical entities that carry energy and momentum. While the energy stored in fields is a familiar concept, the idea that fields can possess momentum—that they can exert pressure and store impetus—is perhaps less intuitive. This chapter explores the principles governing [electromagnetic momentum](@entry_id:268129), from its fundamental definition to its role in resolving apparent paradoxes in mechanics.

### The Momentum Density of the Electromagnetic Field

The foundation of [electromagnetic momentum](@entry_id:268129) is the concept of **[momentum density](@entry_id:271360)**, a vector field denoted by $\vec{g}$ that represents the amount of momentum stored per unit volume at any point in space. This density is directly proportional to the Poynting vector $\vec{S}$, which describes the flow of energy in the electromagnetic field. The Poynting vector is defined as:

$\vec{S} = \frac{1}{\mu_0}(\vec{E} \times \vec{B})$

where $\vec{E}$ is the electric field, $\vec{B}$ is the magnetic field, and $\mu_0$ is the [permeability of free space](@entry_id:276113). The relationship between momentum density and energy flux is one of the fundamental results of [relativistic physics](@entry_id:188332), and for electromagnetic fields, it takes the form:

$\vec{g} = \frac{\vec{S}}{c^2} = \epsilon_0 (\vec{E} \times \vec{B})$

Here, $c = 1/\sqrt{\epsilon_0 \mu_0}$ is the speed of light in vacuum, and $\epsilon_0$ is the [permittivity of free space](@entry_id:272823). This equation tells us that wherever non-parallel electric and magnetic fields coexist, there is momentum stored in the space they occupy. The total [electromagnetic momentum](@entry_id:268129) $\vec{P}_{em}$ in a given volume $V$ is found by integrating the [momentum density](@entry_id:271360) over that volume:

$\vec{P}_{em} = \int_V \vec{g} \, d\tau = \int_V \epsilon_0 (\vec{E} \times \vec{B}) \, d\tau$

### Momentum in Static Fields

A surprising consequence of the definition of $\vec{g}$ is that even completely static (time-independent) systems can store momentum in their fields. This occurs in any region where a static electric field and a static magnetic field are both present and are not parallel to each other.

Consider, for instance, a system composed of an infinitely long, straight wire along the $z$-axis carrying a steady current $I$, and a stationary point charge $q$ located at a position $(a, 0, 0)$ [@problem_id:1593265]. Let us determine the momentum density at a point $P$ located at $(0, b, 0)$.

The electric field at $P$ is produced by the [point charge](@entry_id:274116) $q$. Using Coulomb's law, the displacement vector from the charge to point $P$ is $\vec{r} = (0, b, 0) - (a, 0, 0) = -a\hat{i} + b\hat{j}$. The distance is $R = \sqrt{a^2 + b^2}$. The electric field is therefore:
$\vec{E}(P) = \frac{q}{4\pi\epsilon_0 (a^2+b^2)^{3/2}} (-a\hat{i} + b\hat{j})$

The magnetic field at $P$ is produced by the infinite wire. According to the Biot-Savart law (or Ampere's law), the magnetic field at a distance $\rho=b$ from the wire circles the wire. At point $P=(0, b, 0)$, the direction is along the negative $x$-axis:
$\vec{B}(P) = -\frac{\mu_0 I}{2\pi b} \hat{i}$

Now, we can compute the [momentum density](@entry_id:271360) $\vec{g} = \epsilon_0 (\vec{E} \times \vec{B})$. The cross product is:
$\vec{E} \times \vec{B} = \frac{q}{4\pi\epsilon_0 (a^2+b^2)^{3/2}} (-a\hat{i} + b\hat{j}) \times (-\frac{\mu_0 I}{2\pi b} \hat{i})$

Using the [vector identities](@entry_id:273941) $\hat{i} \times \hat{i} = 0$ and $\hat{j} \times \hat{i} = -\hat{k}$, we find:
$\vec{E} \times \vec{B} = \frac{q \mu_0 I}{8\pi^2 \epsilon_0 b (a^2+b^2)^{3/2}} (b\hat{k}) = \frac{\mu_0 I q}{8\pi^2 \epsilon_0 (a^2+b^2)^{3/2}} \hat{k}$

The [momentum density](@entry_id:271360) at point $P$ is then:
$\vec{g}(P) = \epsilon_0 (\vec{E} \times \vec{B}) = \frac{\mu_0 I q}{8\pi^2 (a^2+b^2)^{3/2}} \hat{k}$

This calculation demonstrates that even in a completely static situation, the overlapping fields contain momentum, directed in this case along the wire. Similar results are found in other static configurations, such as a point charge near a current loop [@problem_id:1808793] or between parallel charged and current-carrying rods [@problem_id:1808796].

A particularly illustrative thought experiment involves a static electric [point charge](@entry_id:274116) $q$ and a hypothetical magnetic monopole $q_m$ [@problem_id:1808784]. If the charge is at the origin and the monopole is on the $z$-axis, the [electric field lines](@entry_id:277009) radiate outwards from the origin, while the magnetic field lines radiate outwards from the monopole. In the $xy$-plane, the $\vec{E}$ field is radial, and the $\vec{B}$ field has both radial and vertical components. The [cross product](@entry_id:156749) $\vec{E} \times \vec{B}$ results in a momentum density $\vec{g}$ that is purely azimuthal, circulating around the $z$-axis. This shows that the momentum in the field can have a rotational character, a precursor to the concept of [field angular momentum](@entry_id:268053).

### Momentum from Moving Charges and Time-Varying Fields

The presence of momentum is more intuitive for systems that are not static. A single [point charge](@entry_id:274116) $q$ moving with a constant, non-relativistic velocity $\vec{v}$ generates both an electric field and a magnetic field. At an instant when the charge is at the origin, its electric field at a position $\vec{R}$ is given by Coulomb's law, $\vec{E} \approx \frac{q}{4\pi\epsilon_0} \frac{\vec{R}}{R^3}$. The magnetic field is given by the Biot-Savart law for a point charge, $\vec{B} \approx \frac{\mu_0 q}{4\pi} \frac{\vec{v} \times \vec{R}}{R^3}$.

Let us calculate the [momentum density](@entry_id:271360) at a point $P$ located at a perpendicular distance $d$ from the line of motion [@problem_id:1808802]. At this point, $\vec{R}$ is perpendicular to $\vec{v}$, so $\vec{R} \cdot \vec{v} = 0$, and $R=d$. The [momentum density](@entry_id:271360) is:
$\vec{g} = \epsilon_0 (\vec{E} \times \vec{B}) = \epsilon_0 \left( \frac{q}{4\pi\epsilon_0} \frac{\vec{R}}{d^3} \right) \times \left( \frac{\mu_0 q}{4\pi} \frac{\vec{v} \times \vec{R}}{d^3} \right) = \frac{\mu_0 q^2}{16\pi^2 d^6} [\vec{R} \times (\vec{v} \times \vec{R})]$

Using the [vector triple product](@entry_id:162942) identity $\vec{A} \times (\vec{B} \times \vec{C}) = \vec{B}(\vec{A} \cdot \vec{C}) - \vec{C}(\vec{A} \cdot \vec{B})$, we get:
$\vec{R} \times (\vec{v} \times \vec{R}) = \vec{v}(\vec{R} \cdot \vec{R}) - \vec{R}(\vec{R} \cdot \vec{v}) = \vec{v}(d^2) - \vec{R}(0) = d^2 \vec{v}$

Substituting this back, we find a remarkably simple result:
$\vec{g} = \frac{\mu_0 q^2}{16\pi^2 d^6} (d^2 \vec{v}) = \frac{\mu_0 q^2}{16\pi^2 d^4} \vec{v}$

The [momentum density](@entry_id:271360) of the field is directed parallel to the charge's velocity. This suggests that the total momentum integrated over all space, $\vec{P}_{em}$, is also proportional to $\vec{v}$, behaving somewhat like a form of electromagnetic inertia.

A more complex dynamic situation arises when fields are explicitly time-dependent, such as in a charging capacitor [@problem_id:1808834]. Consider a parallel-plate capacitor being charged by a steady current $I$. The electric field $E$ between the plates increases with time. According to the Ampere-Maxwell law, this changing electric field induces a circulating magnetic field $B$ between the plates. If the plates are in the $xy$-plane, $\vec{E}$ is in the $z$-direction and $\vec{B}$ is in the azimuthal ($\hat{\phi}$) direction. Their [cross product](@entry_id:156749) $\vec{E} \times \vec{B}$ points radially inward. This means that as the capacitor charges, momentum flows from the surrounding fields into the volume between the plates, where it is stored. By integrating the calculated momentum density $\vec{g}(s)$ over the volume of the capacitor, one can find the total momentum stored in the fields at any given time, which grows as the fields become stronger.

### The Conservation of Momentum and Hidden Momentum

The principle of [momentum conservation](@entry_id:149964) must hold for any closed system. If we include the momentum of the electromagnetic field, the law of [momentum conservation](@entry_id:149964) for a [system of particles](@entry_id:176808) and fields states that the total momentum, $\vec{P}_{total} = \vec{P}_{mech} + \vec{P}_{em}$, is conserved. This inclusion of [field momentum](@entry_id:267786) is essential for resolving several apparent paradoxes.

A classic example is a static [point charge](@entry_id:274116) $q$ placed near an ideal [solenoid](@entry_id:261182) [@problem_id:1808794]. The solenoid produces a [uniform magnetic field](@entry_id:263817) $\vec{B}$ confined to its interior, while the point charge produces a [radial electric field](@entry_id:194700) $\vec{E}$ that permeates all space, including the interior of the solenoid. Inside the solenoid, both $\vec{E}$ and $\vec{B}$ are non-zero, so the momentum density $\vec{g} = \epsilon_0 (\vec{E} \times \vec{B})$ is also non-zero. If one performs the volume integral of $\vec{g}$ over the interior of the solenoid (the only region where $\vec{g}$ is non-zero), the result for the total [field momentum](@entry_id:267786) $\vec{P}_{em}$ is found to be non-zero.

This presents a paradox: the system of the charge and the current-carrying solenoid is entirely static, yet it possesses a net [electromagnetic momentum](@entry_id:268129). How can a system at rest have non-zero momentum? The resolution lies in the realization that there must be an additional, compensating momentum elsewhere in the system. This momentum, which is not due to any macroscopic motion of the components, is called **hidden mechanical momentum**.

The total momentum of the isolated, static system must be zero: $\vec{P}_{total} = \vec{P}_{mech} + \vec{P}_{em} = 0$. Therefore, there must exist a hidden mechanical momentum $\vec{P}_{mech} = - \vec{P}_{em}$.

The physical origin of this [hidden momentum](@entry_id:266575) can be understood by considering the charge carriers that constitute the current in the wires. For a current loop placed in an external electric field $\vec{E}_0$, the moving charges within the wire (e.g., electrons) are subject to the electric force $q_e \vec{E}_0$. For a steady current to be maintained, internal forces within the conductor must counteract this external force. By Newton's third law, the charge carriers must therefore exert a reaction force on the lattice of the conductor. The sum of these relativistic microscopic effects results in a net momentum stored by the charge carriers relative to the stationary wire. For a [magnetic dipole](@entry_id:275765) $\vec{m}$ in a [uniform electric field](@entry_id:264305) $\vec{E}_0$, this hidden mechanical momentum can be shown to be [@problem_id:1808790]:

$\vec{P}_{mech} = \frac{1}{c^2} (\vec{m} \times \vec{E}_0)$

This exactly cancels the [electromagnetic momentum](@entry_id:268129) stored in the fields, $\vec{P}_{em} = \vec{E}_0 \times \vec{m} / c^2$, ensuring that the total momentum of the static system is zero, as it must be.

### Applications and Consequences

Recognizing the existence of [field momentum](@entry_id:267786) is crucial for correctly analyzing dynamic electromagnetic interactions.

Consider a charged, non-conducting ring, initially at rest. If a uniform magnetic field is slowly turned on perpendicular to the plane of the ring, the ring will begin to rotate [@problem_id:1808823]. This phenomenon can be explained in two ways. From a force perspective, the changing magnetic flux induces a tangential electric field (Faraday's Law). This electric field exerts a torque on the charge distributed around the ring, causing it to acquire mechanical angular momentum.

From a momentum conservation perspective, the initial state (ring at rest, no field) has zero [total angular momentum](@entry_id:155748). The final state consists of a rotating ring with mechanical angular momentum $\vec{L}_{mech}$ and a static magnetic field interacting with the moving charges of the ring, a configuration that possesses [field angular momentum](@entry_id:268053) $\vec{L}_{em}$. The conservation of total angular momentum requires that $\vec{L}_{mech} + \vec{L}_{em} = 0$. The torque calculation gives $\vec{L}_{mech} = -\frac{Q R^2}{2} \vec{B}_f$. This implies that the final field must store an equal and opposite angular momentum, $\vec{L}_{em} = +\frac{Q R^2}{2} \vec{B}_f$, demonstrating the transfer of momentum from the field to the mechanical system.

Another subtle application involves analyzing the impulse delivered during an interaction. Imagine a bar magnet passing through a stationary conducting loop in a gravity-free environment [@problem_id:1808819]. As the magnet moves, it induces currents in the loop, which dissipate energy as heat. This energy must come from the magnet's kinetic energy, so the magnet slows down. Its mechanical momentum $\vec{P}_{mag}$ decreases. However, the moving magnet's fields also carry momentum $\vec{P}_{em}$, which is proportional to its velocity. As the magnet slows, $\vec{P}_{em}$ also decreases.

To find the impulse on the loop, we consider the (magnet + field) as our system. The total change in this system's momentum is $\Delta \vec{P}_{mag} + \Delta \vec{P}_{em}$. By the [impulse-momentum theorem](@entry_id:162655), this change is equal to the external impulse exerted by the loop on the magnet, $\vec{J}_{on\_magnet}$. By Newton's third law, the impulse on the loop is $\vec{J}_{on\_loop} = - \vec{J}_{on\_magnet} = -(\Delta \vec{P}_{mag} + \Delta \vec{P}_{em})$. Since both the mechanical and [field momentum](@entry_id:267786) of the magnet decrease (a negative change in the direction of motion), the total term $(\Delta \vec{P}_{mag} + \Delta \vec{P}_{em})$ is a vector pointing opposite to the velocity. The negative of this vector, $\vec{J}_{on\_loop}$, must therefore point *in the same direction* as the magnet's initial velocity. This conclusion, that the net impulse on the loop is downwards, is difficult to see without properly accounting for the change in the field's momentum.