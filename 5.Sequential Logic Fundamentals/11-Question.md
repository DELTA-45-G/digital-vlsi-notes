# 📘 PHASE 5 — FREQUENTLY ASKED PLACEMENT QUESTIONS

## 1. LATCHES ⭐⭐⭐⭐⭐

### Q1. What is a latch?

A latch is a **level-triggered sequential circuit** that stores one bit of information.

### Q2. What is the main difference between a latch and a flip-flop?

| Latch                                 | Flip-Flop                |
| ------------------------------------- | ------------------------ |
| Level triggered                       | Edge triggered           |
| Responds while enable level is active | Responds at a clock edge |
| Transparent during active level       | Samples at an edge       |

**Placement answer:**

> A latch is level-triggered, whereas a flip-flop is edge-triggered.

---

### Q3. What does "transparent" mean in a latch?

When the latch is enabled, the output can follow the input.

---

### Q4. How many bits can one latch store?

**1 bit**

---

### Q5. Why are latches called level-sensitive?

Because their operation depends on the **level of the enable/control signal**, rather than only on an edge.

---

# 2. SR FLIP-FLOP ⭐⭐⭐⭐⭐

### Q6. What does SR stand for?

**Set-Reset**

---

### Q7. What happens when S = 1 and R = 0?

**Q=1**

The flip-flop is **set**.

---

### Q8. What happens when S = 0 and R = 1?

**Q=0**

The flip-flop is **reset**.

---

### Q9. What happens when S = 0 and R = 0?

**No change**

The previous state is retained.

---

### Q10. What is the forbidden condition of a basic SR flip-flop?

For the common NOR-based active-high SR implementation:

**S=1, R=1**

This produces an invalid/forbidden condition.

**Important:** The forbidden input combination depends on the particular SR implementation (NOR vs NAND), so always check the circuit's active polarity.

---

### Q11. Why is the forbidden condition a problem?

Because it can lead to an invalid state and potentially unpredictable behavior when the inputs return to normal.

---

# 3. JK FLIP-FLOP ⭐⭐⭐⭐⭐

### Q12. What is the main advantage of JK over SR?

JK removes the forbidden condition of the basic SR flip-flop.

---

### Q13. What happens when J = 0, K = 0?

**No change**

---

### Q14. What happens when J = 0, K = 1?

**Reset**

---

### Q15. What happens when J = 1, K = 0?

**Set**

---

### Q16. What happens when J = 1, K = 1?

**Toggle**

---

### Q17. Write the JK characteristic equation.

**Qnext=JQ̅+K̅Q**

---

### Q18. Why is JK called a universal flip-flop?

Because it can be configured to perform functions such as set, reset, hold, and toggle, and can be used to realize other flip-flop behaviors.

---

### Q19. What is race-around condition?

In a level-triggered JK flip-flop, when:

**J=K=1**

the output can toggle repeatedly during the active clock level if the clock pulse is sufficiently long.

This is called:

**Race-around condition**

---

### Q20. How can race-around be avoided?

Common approaches include:

* Edge-triggered JK flip-flop
* Master-slave JK flip-flop
* Making the active clock pulse sufficiently short

---

# 4. D FLIP-FLOP ⭐⭐⭐⭐⭐

### Q21. What does D stand for?

Usually:

**Data**

It is also sometimes called a **Delay** flip-flop.

---

### Q22. What is the characteristic equation of D flip-flop?

**Qnext=D**

---

### Q23. What happens when D = 1 at the active clock edge?

**Qnext=1**

---

### Q24. What happens when D = 0?

**Qnext=0**

---

### Q25. What is the main use of a D flip-flop?

It is widely used for:

* Data storage
* Registers
* Shift registers
* Pipeline stages
* Sequential circuits

---

### Q26. Why is D flip-flop widely used in registers?

Because one D flip-flop stores exactly one input bit:

**Qnext=D**

This makes it simple to store data.

---

# 5. T FLIP-FLOP ⭐⭐⭐⭐⭐

### Q27. What does T stand for?

**Toggle**

---

### Q28. What happens when T = 0?

**No change**

---

### Q29. What happens when T = 1?

**Toggle**

---

### Q30. Write the characteristic equation of T flip-flop.

**Qnext=T⊕Q**

---

### Q31. What is an important application of T flip-flop?

Frequency division.

A T flip-flop configured to toggle every active clock edge divides the clock frequency by 2:

**fQ=fCLK/2**

---

# 6. SETUP & HOLD TIME ⭐⭐⭐⭐⭐

### Q32. What is setup time?

The minimum time for which data must be stable **before the active clock edge**.

---

### Q33. What is hold time?

The minimum time for which data must remain stable **after the active clock edge**.

---

### Q34. What happens if setup time is violated?

The flip-flop may capture incorrect data and can potentially become metastable.

---

### Q35. What happens if hold time is violated?

The flip-flop may capture incorrect data and can potentially become metastable.

---

### Q36. Difference between setup and hold time?

> **Setup → before clock edge**
> **Hold → after clock edge**

Easy memory trick:

```text
SETUP → Set data UP before clock
```

HOLD  → HOLD data after clock

---

# 7. TIMING VIOLATIONS ⭐⭐⭐⭐⭐

### Q37. Data arrives too late before the clock edge. What violation is this?

**Setup violation**

---

### Q38. Data changes too soon after the clock edge. What violation is this?

**Hold violation**

---

### Q39. Which type of delay is mainly associated with setup timing?

**Propagation delay**

---

### Q40. Which type of delay is mainly associated with hold timing?

**Contamination delay**

---

# 8. CLOCK SKEW ⭐⭐⭐⭐⭐

### Q41. What is clock skew?

The difference in arrival time of the same clock edge at two different flip-flops.

**Clock Skew=tcapture−tlaunch**

---

### Q42. What is positive clock skew?

When the capture clock arrives **later** than the launch clock.

---

### Q43. What is negative clock skew?

When the capture clock arrives **earlier** than the launch clock.

---

### Q44. How does positive skew affect setup timing?

Generally:

**Positive skew helps setup**

because the capture edge occurs later.

---

### Q45. How does positive skew affect hold timing?

Generally:

**Positive skew hurts hold**

because the capture edge occurs later, increasing the time during which new data can arrive before the capture flip-flop's hold requirement is satisfied.

---

# 9. PROPAGATION & CONTAMINATION DELAY ⭐⭐⭐⭐⭐

### Q46. What is propagation delay?

The maximum time from an input transition until the corresponding output becomes valid.

**tpd**

---

### Q47. What is contamination delay?

The minimum time after an input transition before the output can begin changing.

**tcd**

---

### Q48. Which is generally larger?

**tpd≥tcd**

---

### Q49. Why is contamination delay important?

It is important for **minimum-delay analysis and hold-time checking**.

---

### Q50. Why is propagation delay important?

It is important for **maximum-delay analysis and setup-time checking**.

---

### Q51. A circuit has tcd=2ns and tpd=8ns. What does 2 ns represent?

The earliest time after the input changes that the output can begin to change.

**2ns**

---

### Q52. A circuit has tpd=10ns. What does this mean?

The output is guaranteed to have responded correctly within a maximum delay of 10 ns, under the specified conditions.

---

# 10. CRITICAL PATH ⭐⭐⭐⭐⭐

### Q53. What is a critical path?

The path with the **largest relevant maximum propagation delay** in a synchronous timing path, which limits the achievable clock frequency.

---

### Q54. Why is the critical path important?

It determines the minimum clock period and therefore limits:

**fmax**

---

### Q55. Two paths have delays of 4 ns and 9 ns. Which is the critical path?

**9ns**

---

### Q56. If critical path delay decreases, what happens to maximum frequency?

Generally:

**fmax increases**

---

# 11. METASTABILITY ⭐⭐⭐⭐⭐

### Q57. What is metastability?

A temporary unstable condition in a flip-flop where the output may take an unpredictable amount of time to settle to a valid 0 or 1.

---

### Q58. What commonly causes metastability?

Sampling data too close to the active clock edge, often due to setup/hold violations.

---

### Q59. When is metastability especially important?

When an **asynchronous signal crosses into a synchronous clock domain**.

---

### Q60. How can metastability propagation be reduced?

Using a synchronizer, commonly a:

**2-flip-flop synchronizer**

for a single-bit signal.

---

### Q61. Does a 2-FF synchronizer eliminate metastability?

No

It greatly reduces the probability that metastability propagates to downstream logic.

---

### Q62. What is MTBF?

**Mean Time Between Failures**

It is a measure of the expected reliability of the synchronization scheme.

---

### Q63. How can MTBF generally be improved?

Increase the time available for the metastable first-stage flip-flop to resolve, such as by adding synchronization stages.

---

### Q64. What is CDC?

**Clock Domain Crossing**

It refers to transferring signals between different clock domains.

---

### Q65. Can a simple 2-FF synchronizer safely transfer an arbitrary multi-bit bus?

No

Multi-bit CDC generally requires techniques such as handshaking or asynchronous FIFOs, depending on the design.

---

# 🔥 HIGH-PRIORITY QUESTIONS TO MEMORIZE

If your placement preparation time is limited, **definitely know these**:

| #  | Question            | Key Answer                       |
| -- | ------------------- | -------------------------------- |
| 1  | Latch vs FF         | Level vs Edge                    |
| 2  | JK advantage        | No forbidden condition           |
| 3  | JK = 11             | Toggle                           |
| 4  | D FF equation       | Qnext=D                          |
| 5  | T FF = 1            | Toggle                           |
| 6  | T FF application    | Divide-by-2                      |
| 7  | Setup time          | Before clock                     |
| 8  | Hold time           | After clock                      |
| 9  | Late data           | Setup violation                  |
| 10 | Early data          | Hold violation                   |
| 11 | Clock skew          | Difference in clock arrival      |
| 12 | Positive skew       | Setup better, Hold worse         |
| 13 | tpd                 | Maximum delay                    |
| 14 | tcd                 | Minimum delay                    |
| 15 | Setup related delay | tpd                              |
| 16 | Hold related delay  | tcd                              |
| 17 | Critical path       | Longest max-delay path           |
| 18 | Metastability       | Unstable FF state                |
| 19 | 2-FF synchronizer   | Reduce metastability propagation |
| 20 | MTBF                | Mean Time Between Failures       |
| 21 | CDC                 | Clock Domain Crossing            |

### 🎯 Phase 5 Placement Priority

```text
⭐⭐⭐⭐⭐ MUST KNOW
```

Latches vs Flip-Flops

SR / JK / D / T

Setup & Hold

Timing violations

Clock skew

Propagation / Contamination delay

Metastability

2-FF synchronizer

CDC

```text
⭐⭐⭐⭐ SHOULD KNOW
```

Critical path

MTBF

Race-around condition

Frequency division using T FF
