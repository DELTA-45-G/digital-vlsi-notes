# IR DROP & POWER INTEGRITY ⭐⭐⭐⭐⭐

This is an important **physical-design/VLSI interview topic**. It connects **power distribution, voltage, current, timing, and reliability**.

---

# 1. What is IR Drop?

**IR drop** is the voltage drop caused by current flowing through the resistance of the power-delivery network.

Basic relationship:

**Vdrop=I×R**

where:

* I = current
* R = resistance

---

# 2. Simple Example

Suppose:

**I=2A**

and:

**R=0.1Ω**

Then:

**Vdrop=I×R**

**=2×0.1**

**=0.2V**

If the supply is:

**VDD=1V**

the circuit may effectively receive:

**1−0.2=0.8V**

---

# 3. Why Does IR Drop Matter? ⭐⭐⭐⭐⭐

The circuit is designed assuming a certain supply voltage.

For example:

```text
Expected:
```

VDD = 1.0 V

But because of IR drop:

```text
Actual:
```

VDD = 0.85 V

Lower voltage can cause:

* Increased delay
* Timing violations
* Functional failures
* Reduced performance
* Reliability problems

Therefore:

**IR Drop can affect timing**

---

# 4. Power Distribution Network (PDN)

The chip needs to distribute:

* VDD
* VSS/GND

to different parts of the design.

This network is called the:

**Power Distribution Network**

Conceptually:

```text
             VDD
```

```
          │

   ┌──────┼──────┐

   ↓      ↓      ↓

 Block  Block  Block

   │      │      │

   └──────┼──────┘

          │

         GND
```

---

# 5. Why Does the PDN Have Resistance?

Physical wires are not ideal.

They have resistance because of:

* Wire length
* Wire width
* Material
* Vias
* Contacts

Therefore:

**R≠0**

and when current flows:

**Vdrop=IR**

---

# 6. Static vs Dynamic IR Drop ⭐⭐⭐⭐⭐

Two important categories:

### 1. Static IR Drop

Caused by relatively steady current demand.

### 2. Dynamic IR Drop

Caused by changing/switching current demand.

---

# 7. Static IR Drop

Consider:

```text
VDD
```

│

│

Resistance

│

▼

Logic Block

The block continuously draws current.

Therefore:

**Vdrop=IR**

remains relatively steady.

Memory:

**Static IR → relatively steady current**

---

# 8. Dynamic IR Drop ⭐⭐⭐⭐⭐

Dynamic IR drop occurs when many circuits switch simultaneously.

Example:

```text
Many gates switch
```

```
   ↓
```

Current demand ↑

```
   ↓
```

IR drop ↑

```
   ↓
```

Local supply voltage ↓

Therefore:

**Dynamic IR → switching-dependent current demand**

---

# 9. Why Simultaneous Switching Is Dangerous

Suppose:

```text
Block A ─┐
```

Block B ─┤

Block C ─┼──> Switch simultaneously

Block D ─┤

Block E ─┘

Current demand suddenly increases.

This causes:

**I↑**

Therefore:

**Vdrop=IR**

also increases.

---

# 10. IR Drop and Timing ⭐⭐⭐⭐⭐

Suppose nominal supply:

**VDD=1V**

Due to IR drop:

**VDDactual=0.9V**

Lower supply voltage generally makes CMOS gates slower.

Therefore:

```text
IR Drop
```

↓

VDD ↓

↓

Gate delay ↑

↓

Timing margin ↓

↓

Possible setup violation

Very important:

**IR Drop can cause timing degradation**

---

# 11. IR Drop and Setup Timing

Setup timing is sensitive to increased data-path delay.

If IR drop slows the combinational path:

```text
IR Drop
```

↓

Delay ↑

↓

Data arrives late

↓

Setup violation

Therefore:

**IR drop can worsen setup timing**

---

# 12. IR Drop and Hold Timing

At placement level, remember that IR drop can affect both data and clock paths depending on where and how the voltage droops occur.

The simplest interview intuition is:

> **Supply-voltage variations change cell delays, which can alter timing margins.**

Do not memorize the oversimplification that IR drop always causes only setup violations.

---

# 13. Power Integrity ⭐⭐⭐⭐⭐

**Power integrity** means maintaining a stable and reliable power supply to all parts of the chip.

A good power network should provide:

```text
Stable VDD
```

Stable GND

Low voltage drop

Low noise

Reliable current delivery

---

# 14. What Can Affect Power Integrity?

Important factors include:

* IR drop
* Electromigration
* Supply noise
* Ground bounce
* Decoupling requirements

---

# 15. IR Drop vs Power Integrity

### IR Drop

A specific voltage-drop phenomenon:

**V=IR**

### Power Integrity

A broader concept concerning the quality and reliability of power delivery.

Therefore:

**IR Drop is one part of Power Integrity**

---

# 16. How to Reduce IR Drop? ⭐⭐⭐⭐⭐

Several techniques can help.

### 1. Wider power wires

Wider wire:

**R↓**

Therefore:

**Vdrop=IR↓**

---

### 2. More power straps

```text
Fewer straps
```

→ Higher resistance

More straps

→ Lower effective resistance

Therefore:

**More power straps → Lower IR drop**

---

### 3. More vias

Vias connect different metal layers.

Adding sufficient vias can reduce resistance and improve current distribution.

---

### 4. Better power-grid design

A stronger power grid provides more reliable current delivery.

---

### 5. Reduce localized current demand

Reducing excessive simultaneous switching can reduce dynamic IR drop.

---

# 17. Power Grid

A chip's power network often contains:

```text
Power Ring
```

```
 ↓
```

Power Straps

```
 ↓
```

Local Power Rails

```
 ↓
```

Standard Cells

---

# 18. Power Ring

A power ring surrounds a region/block and distributes:

* VDD
* GND

Conceptually:

```text
┌─────────────────────────┐
```

│ VDD / GND Power Ring    │

│                         │

│      Standard Cells     │

│                         │

│      Standard Cells     │

│                         │

└─────────────────────────┘

---

# 19. Power Straps

Power straps are wider metal lines used to distribute power across the chip/block.

```text
Power Ring
```

│

├──── Strap ────┐

├──── Strap ────┤

├──── Strap ────┤

└──── Strap ────┘

They help reduce resistance and distribute current.

---

# 20. Decoupling Capacitor ⭐⭐⭐⭐⭐

A **decoupling capacitor**, often called a **decap**, is used to help stabilize local supply voltage.

Conceptually:

```text
          VDD
```

```
       │

    ┌──┴──┐

    │Decap│

    └──┬──┘

       │

      GND
```

It can provide local charge during sudden current demand and help reduce supply fluctuations.

---

# 21. Why Are Decaps Useful?

Suppose many gates suddenly switch:

```text
Current demand ↑ suddenly
```

```
      ↓
```

Supply voltage may dip

```
      ↓
```

Decap can help provide local charge

```
      ↓
```

Supply variation reduced

Therefore:

**Decap → Helps stabilize local supply**

---

# 22. Electromigration ⭐⭐⭐⭐⭐

Another major power-integrity problem is:

**Electromigration (EM)**

Electromigration is the movement of metal atoms caused by high current density.

---

# 23. Why is Electromigration Dangerous?

Over time, excessive current density can cause:

* Voids
* Hillocks
* Increased resistance
* Open circuits
* Reliability failures

Conceptually:

```text
High current density
```

```
   ↓
```

Metal atom movement

```
   ↓
```

Physical damage

```
   ↓
```

Reliability failure

---

# 24. IR Drop vs Electromigration ⭐⭐⭐⭐⭐

Very important distinction.

### IR Drop

**Vdrop=IR**

Problem:

**Voltage reduction**

### Electromigration

Problem:

**Physical metal reliability due to current density**

Memory:

**IR Drop → Voltage**

**EM → Metal Reliability**

---

# 25. Current Density

Current density is approximately:

**J=I/A**

where:

* J = current density
* I = current
* A = cross-sectional area

If current increases:

**I↑⇒J↑**

If wire cross-sectional area increases:

**A↑⇒J↓**

---

# 26. Why Wider Wires Help

From:

**J=I/A**

Increasing wire area reduces current density.

Therefore:

**Wider metal → Lower current density**

which can improve electromigration reliability.

Wider metal also reduces resistance, helping IR drop.

So wider power wires can help with both:

* IR drop
* Electromigration

---

# 27. Ground Bounce

When many circuits switch, the ground potential can temporarily change because of parasitic resistance/inductance.

This can cause:

**Ground bounce**

It is another form of supply noise.

For basic placement preparation:

> **Ground bounce = unwanted variation in ground potential due to switching current.**

---

# 28. Supply Noise

Supply noise means unwanted variations on:

* VDD
* GND

Examples:

```text
VDD:
```

───────╲___╱──────

```
     Dip
```

GND:

──────╱‾‾‾╲──────

```
   Bounce
```

This can affect:

* Delay
* Logic levels
* Timing
* Reliability

---

# 29. IR Drop Reduction Summary

```text
             IR DROP REDUCTION
```

```
                 │

    ┌────────────┼────────────┐

    ↓            ↓            ↓
```

Wider Metal   More Straps   More Vias

```
    │            │            │

    └────────────┼────────────┘

                 ↓

          Resistance ↓

                 ↓

            IR Drop ↓
```

---

# 30. 🔥 Placement Question

### Q.

What is IR drop?

### Answer:

> IR drop is the voltage drop caused by current flowing through the resistance of the power-delivery network.

**Vdrop=IR**

---

# 31. 🔥 Placement Question

### Q.

What is the difference between static and dynamic IR drop?

### Answer:

> Static IR drop is associated with relatively steady current demand, while dynamic IR drop is associated with time-varying current demand, especially during switching activity.

---

# 32. 🔥 Placement Question

### Q.

How can IR drop affect timing?

### Answer:

> IR drop lowers the local supply voltage, which can increase cell delay and reduce timing margin.

---

# 33. 🔥 Placement Question

### Q.

How can IR drop be reduced?

Mention:

* Wider power wires
* More power straps
* More vias
* Better power-grid design
* Reduced localized current demand

---

# 34. 🔥 Placement Question

### Q.

What is electromigration?

### Answer:

> Electromigration is the gradual movement of metal atoms caused by high current density, potentially leading to long-term interconnect reliability failures.

---

# 35. 🔥 Placement Question

### Q.

What is the difference between IR drop and electromigration?

### Answer:

> IR drop is primarily a voltage-drop problem caused by resistance and current, while electromigration is a long-term physical reliability problem caused by high current density.

---

# 36. 🔥 Placement Question

### Q.

What is a decoupling capacitor?

### Answer:

> A decoupling capacitor is a capacitor placed near circuitry to help stabilize the local supply voltage and provide charge during rapid changes in current demand.

---

# 37. 🔥 MCQ

IR drop is given by:

A. V=I/R
B. V=IR
C. V=R/I
D. V=I+R

**B**

---

# 38. 🔥 MCQ

Which can reduce IR drop?

A. Narrower power wires
B. Fewer vias
C. Wider power wires
D. Higher resistance

**C**

---

# 39. 🔥 MCQ

Electromigration is primarily related to:

A. Clock frequency
B. Current density
C. Setup time only
D. Logic levels

**B**

---

# 40. 🔥 MCQ

A decoupling capacitor mainly helps:

A. Increase logic depth
B. Stabilize local supply voltage
C. Increase clock skew
D. Reduce transistor count

**B**

---

# 🧠 ONE-MINUTE REVISION

```text
══════════════════════════════════════

       IR DROP & POWER INTEGRITY

══════════════════════════════════════


IR DROP:

Vdrop = I × R


CAUSE:

Current flowing through resistance

of power network.


STATIC IR:

→ Relatively steady current


DYNAMIC IR:

→ Switching-dependent current


IR DROP:

VDD ↓

 ↓

Cell delay ↑

 ↓

Timing margin ↓


REDUCE IR DROP:

→ Wider power wires

→ More power straps

→ More vias

→ Better power grid

→ Reduce localized current demand


POWER INTEGRITY:

→ Stable/reliable VDD and GND


DECAP:

→ Helps stabilize local supply


ELECTROMIGRATION:

→ High current density

→ Metal atom movement

→ Reliability problem


MEMORY:

IR Drop → Voltage problem

EM → Metal reliability problem

Decap → Supply stabilization
```
