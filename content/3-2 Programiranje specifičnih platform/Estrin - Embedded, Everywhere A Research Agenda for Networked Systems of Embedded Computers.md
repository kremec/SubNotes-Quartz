### Introduction and Overview
Information Technology (IT) is undergoing a revolution where computing and communication devices are being embedded into a vast range of physical objects and networked together. The report calls these **Networked Systems of Embedded Computers (EmNets)**.
* **Evolution and Departure:** While the trend toward smaller, more powerful computers is a natural evolution, EmNets represent a **radical departure**. Traditional computers interact with human operators (keyboard, screen), whereas EmNets interact directly with the **physical world** through sensors and actuators.
* **Vision:** This aligns with the vision of **ubiquitous or pervasive computing**, where technology blends invisibly into the environment (a concept pioneered by Mark Weiser).
### Examples of EmNets
The report uses three distinct examples to illustrate the potential and variety of EmNets:
1. **Automotive Telematics:** Modern cars are already "rolling networks" with dozens of microprocessors. The future involves integrating the separate safety-critical (engine, brakes) and non-safety-critical (entertainment) networks. The car will become a "node in a much larger network" for services like remote diagnostics, software updates, traffic management, and context-aware directions (e.g., GM's OnStar).
2. **Precision Agriculture:** EmNets enable fine-grained sensing and actuation to optimize the use of water, fertilizer, and pesticides based on local soil conditions and microclimates. This leads to higher yields, lower costs, and reduced environmental impact. These systems must be adaptive, learn over time, and can also be applied to livestock management.
3. **Defense Systems:** Applications include battlespace surveillance (using dispersed, disposable sensors), asset management (condition-based monitoring of vehicles), and personnel health monitoring. These EmNets must be highly interoperable, secure, robust against jamming, and able to function in ad hoc, unpredictable environments.
### Core Characteristics and Challenges of EmNets
The report identifies several general characteristics and dichotomies that define EmNets and the research challenges they present.
**General Characteristics:**
* Consist of **multiple interacting nodes**, often numbering in the thousands or millions.
* Operate largely **without direct human intervention** as part of an automated control loop.
* Are **tightly coupled to the physical world**, operating in real-time.
* Are deployed in both natural (environment) and engineered (aircraft, buildings) contexts.

**Key Distinguishing Challenges (How EmNets Differ from Traditional Systems):**
The main research challenge arises from the unique *combination* of the following constraints:
1. **Tightly Coupled to the Physical World:** Failures can have direct physical consequences (e.g., equipment damage, safety risks), not just lost data or productivity.
2. **Resource-Constrained:** Nodes are often untethered, mobile, and battery-powered, creating strict limits on energy, processing power, memory, and bandwidth. Energy is a critical, non-renewable resource.
3. **Long Lifetimes:** EmNets are embedded in long-lasting structures (buildings, vehicles). The system's lifetime will far exceed the component lifetime, demanding forward compatibility, upgradability, and interoperability between old and new technologies.
4. **Significant Size and Scale:** Systems designed for a small number of nodes may fail unexpectedly or exhibit dangerous "emergent behaviors" when scaled to thousands or millions of nodes.
5. **Used by Non-Experts:** Users will interact with the objects EmNets are embedded in (e.g., a "smart" sprinkler system), not the computer itself. They will have little or no systems training, meaning the systems must be inherently safe, reliable, and adapt to the user, not the other way around.
### Why a New Research Agenda is Needed
*  **Existing Solutions are Inadequate:** Solutions from general-purpose computing often assume readily available energy, high bandwidth, and static configurations, which do not apply to EmNets.
*  **High Stakes:** Because EmNets will be pervasive and invisible, failures in critical infrastructure (transportation, power, healthcare) could be disastrous. Privacy and security are also major concerns.
*  **Urgency:** It is critical to research these systems *now*. Once widely deployed, it will be incredibly difficult and costly to make fundamental changes or "call them back." Research must guide the initial design to maximize benefits and mitigate risks.