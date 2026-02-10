## Introduction
In the world of electronics, every circuit faces a fundamental challenge: distinguishing the faint, intended signal it must process from the ever-present noise of its own power source. No power supply provides perfectly clean energy; fluctuations, ripple, and interference are inevitable. The ability of a circuit to ignore this electrical "background noise" is a crucial measure of its performance, known as Power Supply Rejection. This article explores this vital characteristic, addressing the gap between ideal circuit theory and real-world performance limited by noisy power. First, in "Principles and Mechanisms," we will dissect the fundamental concepts behind Power Supply Rejection, from the behavior of a single transistor to the elegant power of symmetry and feedback. Following this, "Applications and Interdisciplinary Connections" will demonstrate how PSRR is a cornerstone of precision in analog instruments, data converters, and even high-speed digital systems. We begin by examining the core principles that allow a circuit to become deaf to the noise of its own lifeblood.

## Principles and Mechanisms

Imagine you are trying to have a whispered conversation in a roaring factory. To understand your friend, your brain must perform a remarkable feat: it must reject the overwhelming background noise and isolate the faint, important signal of your friend's voice. An electronic amplifier faces precisely this challenge. The "conversation" is the signal it needs to amplify—perhaps the faint music from a vinyl record or a delicate biosignal from a medical sensor. The "roaring factory" is its own power supply.

No power supply is a perfect, unwavering source of energy. It is inevitably contaminated with small, unwanted fluctuations—ripple from the mains power, noise from other digital components, or interference picked up by the wires. The ability of a circuit to ignore this cacophony on its power line and faithfully amplify only the desired signal is one of its most critical [figures of merit](@entry_id:202572): the **Power Supply Rejection Ratio**, or **PSRR**. It is, in essence, a measure of the circuit's deafness to the noise of its own lifeblood.

### A Measure of Deafness: The Decibel

At its core, PSRR is a simple ratio: how much larger is the noise on the power supply line compared to the noise that manages to leak through to the circuit's output?

$$
\text{PSRR} = \frac{\text{Amplitude of Supply Noise}}{\text{Amplitude of Output Noise}} = \frac{\Delta V_{\text{supply}}}{\Delta V_{\text{out}}}
$$

Consider a common voltage regulator, the LM7805, whose job is to provide a steady 5-volt supply. If we feed it a voltage that has a 1.5 V ripple, and its datasheet specifies a PSRR of 78 decibels (dB), what does that mean? Calculating this tells us that the rejection ratio as a number is about 7,943. This means the 1.5 V ripple at the input is squashed down to a mere 0.189 millivolts at the output . The regulator is nearly 8,000 times "deafer" to the supply noise than it is to a signal it's supposed to pass.

These ratios are often so large that expressing them on a linear scale is cumbersome. This is why engineers use the **decibel (dB) scale**, a logarithmic language that tames enormous numbers. The conversion is $PSRR_{dB} = 20 \log_{10}(\text{PSRR})$. On this scale, every 20 dB increase represents a tenfold improvement in [noise rejection](@entry_id:276557). So, a device with 100 dB PSRR is ten times better than one with 80 dB PSRR. This logarithmic nature maps much better to our intuition about performance—improving from 80 to 100 dB is a much more significant engineering achievement than improving from 20 to 40 dB.

### The Leaky Tap: Where Does Noise Get In?

How does a circuit accomplish this rejection? And more importantly, where are the weak points where noise can leak through? The answer lies in the very components that give the circuit life: the transistors.

Let's look at one of the simplest amplifying building blocks, a **[common-emitter amplifier](@entry_id:272876)**. A transistor takes a small input signal and creates a large copy of it at its output. The output is connected to the positive power supply, $V_{DD}$, through a load resistor, $R_C$. In a perfect world, the transistor would act as a [current source](@entry_id:275668) controlled only by the input, and fluctuations in $V_{DD}$ would be irrelevant. But transistors are not perfect. Due to a phenomenon called the **Early effect**, a transistor has a finite internal output resistance, which we can call $r_o$. This non-ideal resistance creates an unintended pathway from the power supply to the output. The supply rail, the load resistor $R_C$, and the transistor's internal resistance $r_o$ form a simple voltage divider. When the supply voltage $v_{dd}$ wiggles, this voltage divider ensures that the output voltage $v_{out}$ wiggles right along with it.

A careful analysis reveals a beautifully simple result for the PSRR of this humble stage: it is simply the product of the transistor's transconductance $g_m$ (a measure of its amplifying power) and the [load resistance](@entry_id:267991) $R_C$ .

$$
\text{PSRR} = g_m R_C
$$

This tells us that to build a "deaf" amplifier, we want a transistor with high amplifying power ($g_m$) and a large load resistance ($R_C$). The beauty here is that PSRR is not some magical property; it emerges directly from the fundamental physics of the device.

### The Power of Symmetry

A single-transistor amplifier is inherently vulnerable. A much more elegant and powerful solution is the **[differential pair](@entry_id:266000)**. This circuit, which forms the input stage of nearly every operational amplifier ([op-amp](@entry_id:274011)), uses two transistors in a symmetric arrangement. The genius of this design is that any disturbance that affects both sides equally—a "common-mode" disturbance—is cancelled out.

Imagine the supply voltage suddenly increases. In a perfectly symmetric [differential pair](@entry_id:266000), this change will try to push the output of both transistors up by the exact same amount. But since we are interested in the *difference* between the two outputs, this common push becomes invisible. The difference remains zero. In this idealized case, the PSRR is infinite.

Of course, the real world is never perfect. The two transistors might not be perfectly identical. The two load resistors might have slightly different values ($\Delta R \neq 0$). The [current source](@entry_id:275668) that biases the pair might itself be sensitive to the supply voltage ($g_{ps} \neq 0$). Each of these small imperfections breaks the symmetry. Now, when the supply voltage wiggles, it affects one side slightly more than the other. This imbalance no longer cancels out and manifests as noise at the differential output . It is this inevitable conversion of common-mode supply noise into a differential-mode output signal that ultimately limits the PSRR of a differential amplifier. This highlights a deep principle in analog design: **symmetry is the enemy of noise**. This same principle is what gives a differential amplifier its ability to reject noise appearing at its inputs (**Common-Mode Rejection Ratio**, or CMRR), but it's crucial to remember that PSRR relates to noise from the power supply, not the inputs .

### The Op-Amp and the Miracle of Feedback

When we use an operational amplifier ([op-amp](@entry_id:274011)), we are using a device whose designers have already gone to great lengths to create a highly symmetric differential input stage. The PSRR of the op-amp itself—its "open-loop" PSRR—is a specification of how well they succeeded. For a modern op-amp, this can be very high, often 100 dB or more.

It is often more convenient to think of this noise not at the output, but as an equivalent tiny noise source at the input. For an [op-amp](@entry_id:274011) with a PSRR of 105 dB, a 15 mV ripple on the power supply has the same effect as a tiny, phantom noise signal of just 0.0844 microvolts appearing at the [op-amp](@entry_id:274011)'s input . This **[input-referred noise](@entry_id:1126527)** is then amplified by the gain of the circuit.

But here is where a true miracle of electronics happens: **negative feedback**. By taking a fraction of the output signal and feeding it back to the input, we create a closed-loop system that can dramatically improve performance. If a disturbance from the power supply appears at the output, the feedback network immediately senses it and instructs the amplifier to create an opposing signal that cancels the disturbance out.

The result is astonishing. An op-amp with a respectable open-loop PSRR of 80 dB can be configured in a circuit with negative feedback to achieve a closed-loop PSRR of 154 dB . This corresponds to an improvement in rejection by a factor of about 5,000! The amount of improvement is directly related to the amount of feedback in the circuit (the "loop gain"). This principle—that negative feedback suppresses disturbances—is one of the most powerful and fundamental concepts in all of engineering.

### The Battle in the Real World

Achieving good power supply rejection isn't just about clever internal circuit design; it's a battle fought on multiple fronts.

First, **frequency matters**. An amplifier's ability to react and cancel noise diminishes at higher frequencies. The very same parasitic capacitances within the transistors that limit their speed also provide new, sneaky paths for high-frequency noise to couple from the power supply to the output. As a result, PSRR is not a single number; it is a function of frequency. An op-amp boasting a 100 dB PSRR at DC might have its rejection capability fall dramatically as the frequency of the noise increases. A 30 kHz noise signal on the supply might be rejected far less effectively than a 120 Hz ripple, leading to significant unwanted noise at the output .

This reality leads to the first line of defense in any practical circuit design: the **[bypass capacitor](@entry_id:273909)**. By placing a small capacitor right next to the power pin of an integrated circuit, we create a local reservoir of charge. For high-frequency noise coming down the power line, this capacitor provides an easy path to ground. Instead of flowing into the chip and causing trouble, the noise current is shunted away. This simple RC low-pass filter, formed by the capacitor and the [intrinsic resistance](@entry_id:166682) of the power supply traces, is a cheap and profoundly effective way to improve the effective PSRR of a system before the amplifier even has to do any work .

Even with these defenses, subtleties abound. In sophisticated circuits, a **Common-Mode Feedback (CMFB)** loop is used to actively enforce the symmetry of the [differential pair](@entry_id:266000). But if the voltage reference for this CMFB loop is itself derived from the noisy power supply, the CMFB system can end up injecting the very noise it's supposed to help eliminate ! Furthermore, it is critical to distinguish between AC rejection (PSRR) and DC stability, often called **[line regulation](@entry_id:267089)** ($\Lambda$). A circuit might have excellent PSRR in the audio band but still have its DC operating point drift if the supply voltage slowly changes. This can happen due to static leakage paths, for instance from startup circuitry, that are negligible for AC signals but provide a DC path from the supply to the output. The two concepts are deeply linked at zero frequency: $PSRR(0) = |\Lambda|^{-1}$ . Perfect DC stability ($\Lambda = 0$) implies infinite PSRR at DC.

From the leaky physics of a single transistor to the elegant power of symmetry and feedback, the principle of power supply rejection reveals the constant struggle between the ideal and the real. It is a testament to engineering ingenuity that in a world awash with electrical noise, we can build devices that perform their tasks with such breathtaking precision and fidelity.