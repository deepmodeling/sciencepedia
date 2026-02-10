## Introduction
In classical mechanics, angular momentum is inextricably linked to physical rotation—a spinning planet or a turning wheel. The idea that a system of completely stationary charges and magnets could possess angular momentum seems to violate this fundamental intuition. This apparent paradox, however, reveals a deeper truth about the nature of reality: the electromagnetic field is not merely empty space but a physical entity capable of storing energy, momentum, and angular momentum. This "[hidden momentum](@keyword=hidden_momentum|lang=en-US|style=Feynman)" is essential for upholding one of physics' most fundamental tenets, the law of [conservation of angular momentum](@keyword=conservation_of_angular_momentum|lang=en-US|style=Feynman).

This article demystifies this fascinating concept. The first chapter, "Principles and Mechanisms," will uncover the theoretical foundations of [field angular momentum](@keyword=field_angular_momentum|lang=en-US|style=Feynman), explaining how crossed electric and magnetic fields give rise to [momentum density](@keyword=momentum_density|lang=en-US|style=Feynman) via the Poynting vector. We will explore this principle through concrete examples and the famous Feynman disk thought experiment, which proves that this [field momentum](@keyword=field_momentum|lang=en-US|style=Feynman) is physically real and interchangeable with [mechanical momentum](@keyword=mechanical_momentum|lang=en-US|style=Feynman). Following this, the chapter "Applications and Interdisciplinary Connections" will broaden our perspective, revealing how this concept is not just a theoretical curiosity but a crucial factor in [particle accelerators](@keyword=particle_accelerators|lang=en-US|style=Feynman), a key to understanding [fundamental symmetries](@keyword=fundamental_symmetries|lang=en-US|style=Feynman), and a bridge to profound ideas in quantum mechanics and general relativity, including the mystery of [charge quantization](@keyword=charge_quantization|lang=en-US|style=Feynman) and the properties of black holes.

## Principles and Mechanisms

### Momentum in Stillness: A Paradox?

Let’s begin with a curious thought. We learn in introductory physics that angular momentum is about things that are spinning or revolving—a planet orbiting the sun, a spinning top, a figure skater pulling in her arms. It's the [product of inertia](@keyword=product_of_inertia|lang=en-US|style=Feynman) and rotation, a measure of "quantity of rotational motion." So, what would you say if I told you that a system of completely stationary objects—a static electric charge and a static magnet—can have angular momentum? It seems nonsensical. How can something have angular momentum if nothing is moving?

This isn't a riddle; it's a profound feature of the universe, hidden within the laws of [electricity and magnetism](@keyword=electricity_and_magnetism|lang=en-US|style=Feynman). The paradox dissolves when we expand our view of what "things" can carry momentum and angular momentum. It's not just matter. The electromagnetic field itself—the very fabric of electric and magnetic influence that fills the space between objects—is a physical entity. It carries energy, it carries momentum, and, as we shall see, it can carry angular momentum, even when its sources are perfectly still. This "[hidden momentum](@keyword=hidden_momentum|lang=en-US|style=Feynman)" is essential for one of physics' most sacred laws to hold true: the [conservation of angular momentum](@keyword=conservation_of_angular_momentum|lang=en-US|style=Feynman).

### The Recipe for Field Angular Momentum

So, how do we cook up this strange beast? The recipe is surprisingly simple, rooted in the fundamentals of electromagnetism. First, we need a momentum. The momentum of the electromagnetic field is described by the famous **Poynting vector**, $\vec{S}$. While we usually meet $\vec{S}$ as the flow of energy per unit area, it has a secret identity: the momentum density of the field, $\vec{g}$, is simply the Poynting vector divided by the speed of light squared:

$$
\vec{g} = \frac{\vec{S}}{c^2} = \epsilon_0 (\vec{E} \times \vec{B})
$$

This equation is our key. It tells us that wherever we have both an electric field $\vec{E}$ and a magnetic field $\vec{B}$ that are not parallel to each other, there is momentum stored in the space occupied by those fields.

Now, how do we get angular momentum from momentum? The same way we always do: we take the "[lever arm](@keyword=lever_arm|lang=en-US|style=Feynman)" $\vec{r}$ (the position vector from our chosen origin) and cross it with the momentum. The angular momentum density, $\vec{\mathcal{l}}$, is thus:

$$
\vec{\mathcal{l}} = \vec{r} \times \vec{g} = \vec{r} \times \left( \epsilon_0 (\vec{E} \times \vec{B}) \right)
$$

To find the [total angular momentum](@keyword=total_angular_momentum|lang=en-US|style=Feynman) $\vec{L}_{\text{em}}$ in the field, we just sum this up—that is, we integrate it—over all of space.

Let's build a concrete example. Imagine a very long solenoid, which is just a coil of wire, that produces a nice, [uniform magnetic field](@keyword=uniform_magnetic_field|lang=en-US|style=Feynman) $\vec{B}$ pointing straight up along its axis (let's call it the z-axis). Now, let's place a uniformly charged, non-conducting cylinder coaxially inside the solenoid [@problem_id:1808797]. This cylinder produces an electric field $\vec{E}$ that points radially outwards, like the spokes of a wheel.

Look at the ingredients. We have a $\vec{B}$ field pointing up ($\hat{z}$) and an $\vec{E}$ field pointing out ($\hat{r}$). They are perpendicular! The cross product $\vec{E} \times \vec{B}$ gives a momentum density $\vec{g}$ that points azimuthally—it circulates around the z-axis. It's like the fields are trying to flow in a circle inside the device. Since this circulating momentum is at a distance $r$ from the axis, it possesses an angular [momentum density](@keyword=momentum_density|lang=en-US|style=Feynman) $\vec{r} \times \vec{g}$. When we add it all up, we find a net angular momentum stored in the static, unmoving fields, pointing along the axis of the cylinder. Nothing is mechanically rotating, yet the system possesses angular momentum, locked away in the field.

A simpler arrangement leading to a similar conclusion involves a point charge $q$ near a [magnetic dipole](@keyword=magnetic_dipole|lang=en-US|style=Feynman) $\vec{m}$ [@problem_id:1796241]. The charge produces a [radial electric field](@keyword=radial_electric_field|lang=en-US|style=Feynman), and the dipole produces a more complex magnetic field. Again, in the space around them, both fields exist simultaneously, and their [cross product](@keyword=cross_product|lang=en-US|style=Feynman) results in a momentum density that, when integrated, gives a total [field angular momentum](@keyword=field_angular_momentum|lang=en-US|style=Feynman). For static situations like this, there's a beautiful shortcut: the total angular momentum is the negative of the charge $q$ multiplied by the cross product of its position $\vec{r}_q$ and the magnetic vector potential $\vec{A}$ at that position: $\vec{L}_{\text{em}} = -q \vec{r}_q \times \vec{A}(\vec{r}_q)$. This formula elegantly captures the interaction that gives rise to the field's hidden angular momentum.

### The Proof is in the Spin: The Feynman Disk

You might still be skeptical. This "[field angular momentum](@keyword=field_angular_momentum|lang=en-US|style=Feynman)" feels like a mathematical ghost, a clever accounting trick. How can we be sure it's physically real? We can be sure because we can convert it into good old-fashioned mechanical angular momentum.

This leads us to a famous thought experiment, often called the **Feynman disk paradox**. Imagine a thin, non-conducting ring of mass $M$ and charge $Q$, initially at rest. Let's immerse it in a uniform magnetic field $\vec{B}$ that points along the ring's axis [@problem_id:71509]. Just like in our [solenoid](@keyword=solenoid|lang=en-US|style=Feynman) example, the combination of the ring's [radial electric field](@keyword=radial_electric_field|lang=en-US|style=Feynman) and the axial magnetic field stores angular momentum in the surrounding space. We can calculate it, and it turns out to be $\vec{L}_{\text{em, initial}} = \frac{Q B_0 R^2}{2} \hat{z}$, where $R$ is the ring's radius.

Now for the magic. What happens if we slowly turn the magnetic field off? Faraday's Law of Induction tells us that a changing magnetic flux creates a circulating electric field. This [induced electric field](@keyword=induced_electric_field|lang=en-US|style=Feynman) will push on the charges in the ring, exerting a torque. This torque will make the ring start to spin!

When the magnetic field is completely gone, the ring is left spinning with some final angular velocity $\omega_f$. Where did its mechanical angular momentum, $L_{\text{mech, final}} = I \omega_f = MR^2 \omega_f$, come from? It appeared out of nowhere!

Or did it? The total angular momentum of the *entire [isolated system](@keyword=isolated_system|lang=en-US|style=Feynman)* (ring + field) must be conserved. Initially, the ring was at rest ($L_{\text{mech, initial}} = 0$), but the field had angular momentum. Finally, the magnetic field is gone ($L_{\text{em, final}} = 0$), but the ring is spinning. Conservation of angular momentum demands that:

$$
L_{\text{mech, initial}} + L_{\text{em, initial}} = L_{\text{mech, final}} + L_{\text{em, final}}
$$
$$
0 + \frac{Q B_0 R^2}{2} = MR^2 \omega_f + 0
$$

Solving for the final [angular velocity](@keyword=angular_velocity|lang=en-US|style=Feynman) gives a wonderfully simple result: $\omega_f = \frac{Q B_0}{2M}$. The "hidden" angular momentum stored in the initial static field has been completely converted into the visible, tangible mechanical angular momentum of the rotating ring. This is the smoking gun. Field angular momentum is not a mathematical fiction; it is a real, physical quantity that can be exchanged with the mechanical world.

### Conservation's Crystal Ball

The principle of conservation of [total angular momentum](@keyword=total_angular_momentum|lang=en-US|style=Feynman) is an incredibly powerful tool. It allows us to deduce things about a system that would otherwise be monstrously difficult to calculate.

Consider a bizarre contraption: a rigid, massless square with four masses at its corners, with alternating charges $+q, -q, +q, -q$ [@problem_id:2092544]. The whole thing starts at rest in empty space. Its [total angular momentum](@keyword=total_angular_momentum|lang=en-US|style=Feynman)—mechanical plus field—is zero. Now, an internal motor whirs to life and spins the square up to a final angular speed $\omega$. The masses are now rotating and have a definite mechanical angular momentum, $L_{\text{mech}}$, which is easy to calculate.

But the system is isolated. Its total angular momentum must still be zero. So, where is the balancing angular momentum? The charges are moving, creating complicated, time-varying [electric and magnetic fields](@keyword=electric_and_magnetic_fields|lang=en-US|style=Feynman). Calculating the angular momentum stored in these fields directly would be a nightmare. But we don't have to! By the simple and elegant logic of conservation, we know *exactly* what it must be:

$$
L_{\text{field}} = - L_{\text{mech}}
$$

The field *must* acquire an angular momentum that is equal and opposite to the mechanical angular momentum of the spinning masses. The conservation law acts like a crystal ball, giving us the answer without forcing us to trudge through the messy details.

### A Relativistic Illusion?

The existence of this [field angular momentum](@keyword=field_angular_momentum|lang=en-US|style=Feynman) is deeply tied to the [theory of relativity](@keyword=theory_of_relativity|lang=en-US|style=Feynman). Let's see how. Imagine two stationary point charges, $q_1$ and $q_2$, sitting in space in your [laboratory frame](@keyword=laboratory_frame|lang=en-US|style=Feynman) $S$ [@problem_id:902513]. In this frame, you only see a static electric field. There is no magnetic field, so $\vec{E} \times \vec{B}$ is zero everywhere. The [field momentum](@keyword=field_momentum|lang=en-US|style=Feynman) is zero. The [field angular momentum](@keyword=field_angular_momentum|lang=en-US|style=Feynman) is zero. Simple enough.

Now, your friend flies past your lab in a spaceship at a high velocity $\vec{v}$. From her perspective, in frame $S'$, your two "stationary" charges are moving. And what do moving charges do? They create magnetic fields! So, in her frame $S'$, she sees both electric *and* magnetic fields. This means she will calculate a non-zero [momentum density](@keyword=momentum_density|lang=en-US|style=Feynman) $\vec{g}' = \epsilon_0 (\vec{E}' \times \vec{B}')$ and a non-zero [total angular momentum](@keyword=total_angular_momentum|lang=en-US|style=Feynman) $\vec{L}'_{\text{em}}$ in the field.

This is astounding. The field's angular momentum literally "appears" just by changing your point of view. It's not an illusion; it's a consequence of the fundamental unity of space and time, and of electricity and magnetism. What one observer sees as pure electrostatic energy, another sees as a combination of [electromagnetic energy](@keyword=electromagnetic_energy|lang=en-US|style=Feynman) and momentum. The energy of the field in one frame gets "mixed" into momentum in another, in precisely the way prescribed by Lorentz transformations. Field angular momentum is not an add-on to Maxwell's theory; it is an inevitable and essential consequence of its compatibility with special relativity.

### The Deepest View: Spacetime and Symmetry

This connection can be made even more precise. In the four-dimensional language of spacetime, energy and momentum are unified into a single object, the **stress-energy tensor** $T^{\mu\nu}$. This tensor tells you everything about the flow of energy and momentum in the field. From this tensor, one can construct the **angular [momentum density](@keyword=momentum_density|lang=en-US|style=Feynman) tensor** $M^{\lambda\mu\nu} = x^\mu T^{\lambda\nu} - x^\nu T^{\lambda\mu}$ [@problem_id:1489903].

The conservation of [total angular momentum](@keyword=total_angular_momentum|lang=en-US|style=Feynman) is then a statement about the divergence of this tensor. Its divergence is not zero, but is instead equal to the torque exerted by the field on the charges. This means that any change in the field's angular momentum is perfectly balanced by a change in the matter's angular momentum, and vice-versa. It's a closed, perfect system of accounting.

Perhaps the most beautiful and strange illustration of [field angular momentum](@keyword=field_angular_momentum|lang=en-US|style=Feynman) comes from a purely hypothetical, but deeply insightful, thought experiment: a system consisting of a single electric charge $q$ and a single magnetic monopole $g$ [@problem_id:1239898]. (A magnetic monopole is a hypothetical particle that is a source of magnetic field, just as an electric charge is a source of electric field.) If we place the charge at the origin and the monopole a distance $d$ away, the charge produces a [radial electric field](@keyword=radial_electric_field|lang=en-US|style=Feynman) ($\vec{E} \propto \vec{r}/r^3$) and the monopole produces a radial magnetic field from its own position ($\vec{B} \propto (\vec{r}-\vec{d})/|\vec{r}-\vec{d}|^3$).

Everywhere in space, $\vec{E}$ and $\vec{B}$ are non-zero and not parallel. The resulting momentum density $\vec{g} = \epsilon_0 (\vec{E} \times \vec{B})$ swirls around the axis connecting the charge and the monopole. When we integrate this over all space, we find a total [field angular momentum](@keyword=field_angular_momentum|lang=en-US|style=Feynman) that is stunningly simple:

$$
\vec{L} = \frac{q g}{4\pi} \hat{d}
$$

where $\hat{d}$ is the unit vector pointing from the charge to the monopole. The very existence of this pair of static particles imbues the space between them with an intrinsic, static angular momentum. This remarkable result, first discovered by J.J. Thomson and later explored by Dirac, forms a cornerstone of the quantum theory of magnetic charge, suggesting a deep and unexpected link between the [quantization of charge](@keyword=quantization_of_charge|lang=en-US|style=Feynman) and the [conservation of angular momentum](@keyword=conservation_of_angular_momentum|lang=en-US|style=Feynman). It's a perfect example of how exploring the consequences of a simple principle can lead us to the very frontiers of physics.