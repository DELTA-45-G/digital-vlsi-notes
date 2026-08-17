# &#x20;CLOCK GATING & LOW-POWER DIGITAL DESIGN ⭐⭐⭐⭐⭐

This topic is important for **VLSI placements** because interviewers frequently connect **clock gating, dynamic power, leakage power, DVFS, power gating, and low-power design**.

---

# 1. Why Low-Power Design?

Modern chips contain millions or billions of transistors.

Power consumption affects:

* Battery life
* Heat
* Reliability
* Performance
* Packaging
* Cooling requirements

Therefore:

**Low-power design is a major VLSI design goal**

---

# 2. Two Main Types of Power ⭐⭐⭐⭐⭐

Digital CMOS power is commonly divided into:

1. **Dynamic Power**
2. **Static Power**

---

# 3. Dynamic Power

Dynamic power is consumed when signals switch.

The basic equation is:

**Pdynamic=αCVDD²f**

where:

* α = switching activity
* C = capacitance
* VDD = supply voltage
* f = frequency

---

# 4. What Does the Equation Tell Us?

### Switching activity increases

**α↑⇒P↑**

### Capacitance increases

**C↑⇒P↑**

### Voltage increases

Because of V²:

**V↑⇒P↑↑**

### Frequency increases

**f↑⇒P↑**

---

# 5. Static Power

Static power is power consumed even when the circuit is not switching.

A major component is leakage power.

Simplified:

**Pstatic≈IleakVDD**

Therefore:

**Static power → Leakage related**

---

# 6. Dynamic vs Static Power ⭐⭐⭐⭐⭐

| Dynamic Power             | Static Power                  |
| ------------------------- | ----------------------------- |
| Mainly due to switching   | Mainly due to leakage         |
| Depends strongly on f     | Exists even without switching |
| αCV²f                     | Related to leakage current    |
| Reduce switching activity | Reduce leakage                |

Memory:

**Switching → Dynamic**

**Leakage → Static**

---

# 7. Clock Gating ⭐⭐⭐⭐⭐

Clock gating reduces unnecessary clock switching.

Suppose a block is inactive:

```text
Without Clock Gating:
```

Clock → Block

↓

Clock keeps switching

↓

Unnecessary dynamic power

With clock gating:

```text
Clock
```

↓

Clock Gating

↓

Inactive Block

↓

Clock switching disabled

Therefore:

**Clock Gating → Dynamic Power Reduction**

---

# 8. Why Clock Gating Is Effective

The clock:

* Runs continuously
* Drives many flip-flops
* Has high switching activity
* Has significant capacitance

Therefore:

**Reducing unnecessary clock activity saves power**

---

# 9. Integrated Clock Gating (ICG) Cell ⭐⭐⭐⭐⭐

Practical designs commonly use an:

**ICG = Integrated Clock Gating Cell**

Conceptually:

```text
             ┌─────────────┐
```

Clock ──────>│             │

```
         │     ICG     │────> Gated Clock
```

Enable ─────>│             │

```
         └─────────────┘
```

The ICG cell ensures clock gating is performed safely.

---

# 10. Why Not Use a Simple AND Gate?

Consider:

```text
Clock ─────┐
```

```
       AND ───> Gated Clock
```

Enable ────┘

If `Enable` changes while the clock is active, it can produce a **glitch** or malformed clock pulse.

That can cause incorrect sequential behavior.

Therefore:

**Use proper clock-gating structures**

---

# 11. Latch-Based Clock Gating ⭐⭐⭐⭐⭐

A common conceptual structure is:

```text
Enable
```

│

▼

Latch

│

├───────┐

```
      AND ───> Gated Clock
```

Clock ────┘

The latch captures the enable during the safe phase of the clock.

This prevents the enable from changing at an unsafe point and creating glitches on the gated clock.

---

# 12. Clock Gating Memory Trick

**Clock Gating → Stop unnecessary clock switching**

**Main benefit → Dynamic power reduction**

---

# 13. Power Gating ⭐⭐⭐⭐⭐

Clock gating and power gating are **not the same**.

### Clock gating

Stops clock switching.

**Reduces dynamic power**

### Power gating

Disconnects or reduces the supply to an inactive block.

**Reduces leakage/static power**

---

# 14. Power Gating Concept

```text
          VDD
```

```
       │

   Power Switch

       │

       ▼

    Logic Block

       │

      GND
```

When the block is inactive, the power switch can disconnect it from the supply.

---

# 15. Sleep Transistor

The power switch is often implemented using a transistor sometimes called a:

**Sleep transistor**

Conceptually:

```text
VDD
```

│

Sleep Transistor

│

Logic Block

│

GND

When the block is shut down, leakage can be significantly reduced.

---

# 16. Clock Gating vs Power Gating ⭐⭐⭐⭐⭐

| Clock Gating          | Power Gating                            |
| --------------------- | --------------------------------------- |
| Stops clock           | Disconnects/reduces power               |
| Mainly dynamic power  | Mainly leakage/static power             |
| State may be retained | State may be lost unless retention used |
| Easier to resume      | Wake-up may require recovery            |

Memory:

**Clock → Dynamic**

**Power → Leakage**

---

# 17. Power Domains

Large SoCs may be divided into different power domains.

```text
             SoC
```

```
          │

  ┌───────┼────────┐

  ↓       ↓        ↓
```

Domain A Domain B Domain C

Different domains can have different:

* Supply voltages
* Power states
* Clock states

---

# 18. Voltage Scaling ⭐⭐⭐⭐⭐

Reducing supply voltage can greatly reduce dynamic power.

Recall:

**Pdynamic=αCV²f**

Therefore:

**V↓⇒Pdynamic↓**

Because voltage is squared.

---

# 19. DVFS ⭐⭐⭐⭐⭐

**DVFS = Dynamic Voltage and Frequency Scaling**

The system dynamically changes:

* Voltage
* Frequency

depending on workload.

Example:

```text
High workload
```

```
↓
```

High frequency

High voltage

Low workload

```
↓
```

Low frequency

Low voltage

This can reduce power when high performance is not required.

---

# 20. Voltage-Frequency Relationship

Generally:

**V↑⇒higher possible frequency**

and:

**V↓⇒lower possible frequency**

because reducing voltage generally slows transistor switching.

Therefore DVFS trades:

**Performance ↔ Power**

---

# 21. Multi-Vt Design ⭐⭐⭐⭐⭐

Another low-power technique involves transistor threshold voltage.

**VT = Threshold Voltage**

Common categories:

* Low-VT
* Standard-VT
* High-VT

---

# 22. Low-Vt Cells

Low-VT cells generally switch faster.

**Low VT → Higher speed**

But they generally have:

**Higher leakage**

Therefore:

```text
Low Vt
```

↓

Fast

↓

Higher leakage

---

# 23. High-Vt Cells

High-VT cells generally have:

**Lower leakage**

but are slower.

```text
High Vt
```

↓

Lower leakage

↓

Slower

---

# 24. Multi-Vt Optimization

A design can use:

```text
Critical paths
```

```
 ↓
```

Low-Vt cells

```
 ↓
```

Speed

Non-critical paths

```
 ↓
```

High-Vt cells

```
 ↓
```

Lower leakage

Therefore:

**Multi-Vt → Speed + Leakage tradeoff**

---

# 25. Power Optimization Techniques ⭐⭐⭐⭐⭐

Important techniques:

### 1. Clock gating

Reduce switching activity.

### 2. Power gating

Reduce leakage.

### 3. Voltage scaling

Reduce V² power component.

### 4. Frequency scaling

Reduce switching frequency.

### 5. Multi-Vt

Balance speed and leakage.

### 6. Reduce capacitance

Reduce switched load.

---

# 26. Power Optimization Summary

```text
              LOW POWER
```

```
              │

   ┌──────────┼──────────┐

   ↓          ↓          ↓
```

Dynamic      Static     Both

```
 Power       Power

   │          │

   ↓          ↓
```

Clock Gating  Power Gating

Voltage       High-Vt

Scaling       Cells

Frequency

Scaling

---

# 27. Dynamic Power Numerical Example ⭐⭐⭐⭐⭐

Suppose:

**α=0.5**

**C=10pF**

**V=1V**

**f=100MHz**

Then:

**P=αCV²f**

**P=0.5×10pF×1²×100MHz**

**P=0.5mW**

---

# 28. Effect of Voltage Reduction

Suppose voltage changes:

**1V→0.8V**

Since:

**P∝V²**

Power ratio:

**Pnew/Pold=0.8²/1²=0.64**

Therefore:

**Pnew=64% of original**

So dynamic power decreases by approximately:

**36%**

---

# 29. Leakage Power

Leakage can occur even when transistors are not switching.

Major leakage mechanisms include:

* Subthreshold leakage
* Gate leakage
* Junction leakage

For basic placement interviews, remember:

**Leakage → Static Power**

---

# 30. Power vs Performance Trade-off

This is a very important VLSI concept.

```text
Higher Voltage
```

```
  ↓
```

Higher Speed

```
  ↓
```

Higher Power

And:

```text
Lower Voltage
```

```
  ↓
```

Lower Power

```
  ↓
```

Lower Speed

Therefore:

**Power and performance often trade off**

---

# 31. 🔥 Placement Question

### Q.

What is the main difference between clock gating and power gating?

### Answer:

> Clock gating disables unnecessary clock switching and primarily reduces dynamic power, while power gating reduces leakage by disconnecting or reducing the supply to an inactive block.

---

# 32. 🔥 Placement Question

### Q.

Why does reducing voltage reduce dynamic power significantly?

Because:

**Pdynamic∝V²**

Therefore even a moderate voltage reduction can produce a significant reduction in dynamic power.

---

# 33. 🔥 Placement Question

### Q.

What is DVFS?

**Dynamic Voltage and Frequency Scaling**

It dynamically adjusts voltage and frequency based on workload.

---

# 34. 🔥 Placement Question

### Q.

What is the trade-off of low-VT cells?

**Higher speed but higher leakage**

---

# 35. 🔥 Placement Question

### Q.

What is the advantage of high-VT cells?

**Lower leakage**

with the trade-off of lower speed.

---

# 36. 🔥 MCQ

Clock gating primarily reduces:

A. Leakage power
B. Dynamic power
C. Threshold voltage
D. Area

**B**

---

# 37. 🔥 MCQ

Power gating primarily targets:

A. Dynamic power
B. Leakage power
C. Clock skew
D. Setup time

**B**

---

# 38. 🔥 MCQ

Dynamic power is approximately proportional to:

A. V
B. V²
C. 1/V
D. V³

**B**

---

# 39. 🔥 MCQ

Which cell generally has higher leakage?

A. High-VT
B. Low-VT

**B**

---

# 40. 🔥 MCQ

DVFS stands for:

A. Dynamic Voltage and Frequency Scaling
B. Digital Voltage Frequency System
C. Dynamic Variable Frequency System
D. Digital Voltage Flow Scaling

**A**

---

# 🧠 ONE-MINUTE REVISION

```text
══════════════════════════════════════

        LOW-POWER DIGITAL DESIGN

══════════════════════════════════════


DYNAMIC POWER:

P = αCV²f


Caused mainly by switching.


STATIC POWER:

Mainly leakage-related.


CLOCK GATING:

→ Stop unnecessary clock switching

→ Reduce dynamic power


POWER GATING:

→ Disconnect/reduce supply

→ Reduce leakage/static power


DVFS:

Dynamic Voltage and Frequency Scaling

→ Adjust V and f based on workload


LOW-VT:

→ Faster

→ Higher leakage


HIGH-VT:

→ Slower

→ Lower leakage


MULTI-VT:

Critical path → Low-Vt

Non-critical → High-Vt


MEMORY:

Clock → Dynamic

Power → Leakage

Low-Vt → Fast + Leaky

High-Vt → Slow + Low leakage

Voltage ↓

→ Dynamic power ↓ significantly
```
