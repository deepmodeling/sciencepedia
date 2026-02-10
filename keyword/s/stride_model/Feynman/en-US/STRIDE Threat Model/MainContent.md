## Introduction
In an era defined by technology, from medical AI to critical infrastructure, ensuring the security of our digital systems is not just a technical requirement—it is a foundation of public trust. Yet, how can we proactively defend against malicious attacks? The challenge lies in our ability to anticipate them. Simply relying on ad-hoc brainstorming is not enough; we need a structured, systematic way to view our own creations through the eyes of an adversary.

This article introduces the STRIDE model, a foundational framework for [threat modeling](@entry_id:924842) that transforms this challenge into a manageable process. We will first delve into the "Principles and Mechanisms" of STRIDE, breaking down its six core threat categories and the methodology for applying them. Following this, the "Applications and Interdisciplinary Connections" chapter will showcase the model's versatility, revealing how it serves as a crucial bridge between abstract security concepts and their tangible consequences in fields like healthcare, industrial engineering, and even law.

## Principles and Mechanisms

How do we build systems that we can trust? Whether it’s an artificial intelligence predicting sepsis in a hospital, an app on your phone delivering therapy, or a complex control system running a power plant, the question is the same. Before we can protect a system, we must first imagine how it could fail. Not just how it might break by accident, but how it could be broken on purpose, by a clever adversary. This is the art and science of **threat modeling**: a systematic, imaginative process of looking at your own creation through the eyes of an attacker.

But imagination needs a guide. If you simply ask a team of engineers to "think of bad things," they might miss entire categories of attack. We need a structured language, a set of lenses to focus our creativity. This is where the beauty of a simple yet powerful model called **STRIDE** comes into play. It doesn't tell us the answers, but it teaches us to ask the right questions.

### A Language for Threats: The Six Questions of STRIDE

At its heart, security engineering is about protecting fundamental properties of a system. You want to keep secrets (**Confidentiality**), ensure information isn't changed illicitly (**Integrity**), and make sure the system is working when you need it (**Availability**). This is the famous **CIA triad**. But there are other, equally crucial properties: we need to know who we are talking to (**Authentication**), what they are allowed to do (**Authorization**), and have proof of what they've done (**Non-repudiation**).

STRIDE, a mnemonic developed by security researchers at Microsoft, is a brilliant trick for turning these desired properties on their heads. It gives us six categories of threats, one for each property we seek to protect. It transforms the vague goal of "making the system secure" into a concrete checklist of questions to ask about every single part of our system.

The six STRIDE categories are:

*   **Spoofing**: Can someone or something pretend to be someone or something else? This attacks **Authentication**.
*   **Tampering**: Can an attacker modify data or code they shouldn't? This attacks **Integrity**.
*   **Repudiation**: If an attacker does something, can they deny it? This attacks **Non-repudiation**.
*   **Information Disclosure**: Can an attacker see information they're not supposed to? This attacks **Confidentiality**.
*   **Denial of Service**: Can an attacker prevent legitimate users from using the system? This attacks **Availability**.
*   **Elevation of Privilege**: Can an attacker gain abilities they weren't meant to have? This attacks **Authorization**.

These six simple questions form the foundation of our entire investigation. They are our toolkit for systematically dissecting a system's weaknesses.

### The Art of Seeing: Mapping Your System

Before we can ask our STRIDE questions, we need to know *where* to ask them. A system isn't a monolithic block; it's a collection of components talking to each other. We must first draw a map. In security, this map is often a **Data Flow Diagram (DFD)**. A DFD shows the processes, the data stores, the external entities, and, most importantly, the data flows between them.

The most critical feature on this map is the **trust boundary**. A trust boundary is any line where data passes from a less-trusted environment to a more-trusted one. Think of the jump from the public internet to your clinic's internal network, or from a guest Wi-Fi network to the core Electronic Health Record (EHR) system . These boundaries are the system's "attack surface"—the places where an adversary is most likely to knock. Threat modeling with STRIDE is the process of walking along these boundaries and, at every interface, every flow, asking our six questions.

### A Walk Through the Attack Surface

Let's make this concrete. Imagine a modern cyber-physical plant, where a controller $C$ adjusts a physical process based on sensor readings $y(t)$ to match a setpoint $r(t)$. A cloud-based **Digital Twin** monitors the system and can provide updates. Now, let's put on our attacker's hat and use STRIDE to see where the weaknesses lie .

**Can I Spoof something?** An attacker could place a counterfeit pressure sensor on the plant that looks identical to the real one on the network. This fake sensor reports a safe, steady pressure $y(t)$ while the real pressure builds to dangerous levels. The controller, none the wiser, is making decisions based on a complete fiction . Or, in a less physical domain, an attacker who steals a clinician's authentication token can use it to send messages *as that clinician*, completely undermining the system's trust in who is giving orders . A particularly insidious form of spoofing is a **replay attack**, where an attacker records a valid, authenticated message (e.g., "system status is normal") and simply plays it back over and over again, making a frozen, old reality masquerade as the live one .

**Can I Tamper with something?** Of course. An attacker could breach the controller and change the setpoint $r(t)$ from a safe value to a dangerous one. Or they could intercept the actuation signal $u(t)$ and alter it, causing a valve to open when it should be closed. In an AI system, this could be even more subtle. Imagine an attacker who manages to inject maliciously crafted records into the training data for a sepsis prediction model. By altering the labels, they tamper with the very "brain" of the AI, teaching it the wrong lessons and corrupting its future judgments . At the most fundamental level, an attack that overwrites parts of a program's memory to hijack its execution, like a **[return-oriented programming](@entry_id:754319) (ROP)** attack, is a profound form of tampering with the machine's control flow .

**Can I Repudiate something?** Suppose a rogue operator manually overrides a safety system, causing an incident. Later, they claim, "It wasn't me." If the system does not have immutable, signed audit logs, there is no way to prove who performed the action. The action becomes repudiable. This is why a lack of good logging is not just an operational headache; it's a critical security flaw that undermines accountability  .

**Can I cause Information Disclosure?** An attacker might not want to break the plant, but simply to steal its secrets. By hacking into the Digital Twin, they could exfiltrate the model parameters $\theta$ and historian data, revealing proprietary process recipes worth millions . In a healthcare setting, this is even more critical. A misconfigured cloud storage bucket might expose "de-identified" patient datasets. While the names are gone, an adversary could combine this with other public data to re-identify individuals, causing a massive privacy breach. This highlights a crucial point: de-identification is not a guarantee of confidentiality .

**Can I cause a Denial of Service?** An attacker could flood the industrial network with junk traffic, preventing the controller's commands $u(t)$ from ever reaching the actuators. The physical process is left flying blind, deprived of control. The system is still "on," but its availability for its core purpose has been destroyed . Similarly, a botnet could flood a hospital's inference API with so many requests that legitimate calls from clinicians time out, forcing them to revert to slower, manual workflows in a time-critical situation .

**Can I Elevate my Privilege?** This is the classic "hacker" goal. An attacker might exploit a vulnerability on an operator's workstation to gain the more powerful privileges of an engineer. With this elevated status, they can now perform actions they were never authorized for, like pushing a malicious [firmware](@entry_id:164062) update that disables critical safety interlocks . In some cases, a simple misconfiguration is all it takes—a software component in an AI pipeline, due to an incorrect role setting, suddenly finds it has administrative rights on the entire training cluster, allowing it to steal the model itself .

### From Possibilities to Priorities: Quantifying Risk

After walking the system's boundaries with STRIDE, we will have a list of potential threats. But we can't fix everything at once. We need to prioritize. The most common way to do this is to estimate the **risk** associated with each threat. A simple and powerful formula for risk is:

$R = p \times I$

Here, $p$ is the probability (or likelihood) of the threat occurring, and $I$ is the impact (or severity) if it does. This transforms our qualitative list of "what-ifs" into a quantitative ranking that can guide our engineering efforts .

But what is "impact"? In the world of medical devices, this question has a profound ethical dimension. The impact isn't just about financial loss; it's about patient harm. A proper risk analysis must connect the cybersecurity threat to a clinical outcome. For example, a **Spoofing** attack on a Continuous Glucose Monitor (CGM) isn't just a "loss of data integrity." It's an initiating event in a causal chain that could lead to an AI commanding a massive insulin overdose, resulting in severe hypoglycemia and potential death. The "impact" is the severity of that harm to the patient. By tracing this chain—from threat to system malfunction to hazardous situation to patient harm—we can apply risk controls where they matter most, like building better anomaly detectors that can catch the spoofed data before it leads to a dangerous command .

### The Elegant Unity of STRIDE

The true beauty of the STRIDE model lies in its elegant unity and versatility. It is simple enough to be remembered as a mnemonic, yet comprehensive enough to cover the fundamental ways that security can be compromised. It provides a common language that allows a diverse team of engineers, security experts, and even clinicians to reason together about risk.

As we've seen, the same six questions can be applied to an AI data pipeline , a clinical information workflow , a digital therapeutic app , an industrial plant , and even an implantable pacemaker . It helps us see that an attack that hijacks the code inside a medical device and an attack that forges sensor readings in a factory are both expressions of the same fundamental threats: Tampering and Spoofing.

STRIDE is not the only tool; other frameworks exist to analyze different facets of trustworthiness, such as privacy (with models like LINDDUN) . But as a foundational model for security, its power is undeniable. It doesn't give you the answers, but it gives you a light to see the questions, revealing the hidden cracks and fissures in a system before they are ever exploited. It is the first, and most crucial, step in the journey of building systems worthy of our trust.