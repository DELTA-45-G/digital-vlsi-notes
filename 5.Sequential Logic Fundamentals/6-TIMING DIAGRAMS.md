# TIMING DIAGRAMS ⭐⭐⭐⭐⭐

This is a **very important VLSI placement topic**.

So far, we've looked at flip-flops using truth tables. Now we need to understand **how their inputs and outputs behave with respect to time**.

---

# 1. What is a Timing Diagram?

A timing diagram shows how digital signals change with **time**.

For example:

```text
Time ─────────────────────────►
```

```text
CLK   \_\_\_|‾‾‾|\_\_\_|‾‾‾|\_\_\_|‾‾‾|\_\_\_

          ↑       ↑       ↑

D     \_\_\_\_‾‾‾‾\_\_\_\_\_\_\_\_‾‾‾‾\_\_\_\_\_\_\_\_

Q     \_\_\_\_\_\_‾‾‾‾\_\_\_\_\_\_\_\_‾‾‾‾\_\_\_\_\_\_
```

It helps us understand:

* When the clock changes
* When input changes
* When output changes
* Which edge captures data
* Timing relationships between signals

---

# 2. What is a Clock Signal?

A clock is a periodic digital signal used to synchronize sequential circuits.

It usually alternates between:

**0→1→0→1...**

Example:

```text
CLK

     ┌───┐     ┌───┐     ┌───┐
─────┘   └─────┘   └─────┘   └────
     ↑         ↑         ↑
```

---

# 3. Rising Edge ⭐⭐⭐⭐⭐

A rising edge is:

**0→1**

Also called:

* Positive edge
* Positive transition

Symbolically:

**↑**

Example:

```text
      │
──────┘
      ↑
  Rising edge
```

---

# 4. Falling Edge ⭐⭐⭐⭐⭐

A falling edge is:

**1→0**

Also called:

* Negative edge
* Negative transition

Symbolically:

**↓**

---

# 5. Positive-Edge-Triggered Flip-Flop

A positive-edge-triggered flip-flop captures data at:

**0→1**

clock transition.

```text
CLK

      ↑       ↑       ↑

──────┘───────┘───────┘

      │       │

    Capture Capture
```

If:

**D=1**

at the rising edge:

**Qnext=1**

---

# 6. Negative-Edge-Triggered Flip-Flop

A negative-edge-triggered flip-flop captures data at:

**1→0**

```text
CLK

──────┐───────┐───────┐

      ↓       ↓       ↓

    Capture Capture
```

---

# 7. Important: D Can Change Between Edges

Consider a positive-edge-triggered D flip-flop.

Suppose:

```text
CLK:   ↑           ↑
```

```
   │           │
```

D:     1─────0─────1

At the first rising edge:

**D=1**

Therefore:

**Q=1**

Then D changes to 0.

Does Q immediately become 0?

No

Q waits until the next active edge.

At the next rising edge:

**D=1**

so:

**Q=1**

---

# 8. The Key Timing Rule ⭐⭐⭐⭐⭐

For an edge-triggered D flip-flop:

> **Only the value of D around the active clock edge is captured.**

This is fundamental.

---

# 9. Clock Period ⭐⭐⭐⭐⭐

The clock period T is the time for one complete clock cycle.

```text
       ←── T ──→
```

CLK    ┌────┐

───────┘    └───────

Frequency and period are related by:

**f=1/T**

and:

**T=1/f**

---

# 10. Example

Suppose:

**f=100MHz**

Then:

**T=1/(100×10⁶)**

**T=10ns**

Therefore:

**T=10ns**

---

# 11. Duty Cycle ⭐⭐⭐⭐

Duty cycle describes the percentage of one clock period for which the signal is HIGH.

**Duty Cycle = (T<sub>HIGH</sub>/T<sub>PERIOD</sub>) × 100%**

For a 50% duty-cycle clock:

**T<sub>HIGH</sub>=T<sub>LOW</sub>**

Example:

If:

**T=10ns**

and:

**T<sub>HIGH</sub>=5ns**

then:

**Duty Cycle = (5/10) × 100 = 50%**

---

# 12. Propagation Delay ⭐⭐⭐⭐⭐

Real circuits don't change output instantaneously.

There is a small delay between an input/clock event and the corresponding output change.

For a flip-flop, one important delay is:

**Clock-to-Q delay**

---

# 13. Clock-to-Q Delay

Suppose the clock edge occurs at:

**10ns**

and Q changes at:

**10.5ns**

Then:

**tCQ=10.5−10**

**tCQ=0.5ns**

This becomes extremely important when we study **setup and hold timing**.

---

# 14. Setup and Hold — Preview ⭐⭐⭐⭐⭐

Don't worry about these yet; we'll study them in detail next.

For correct operation, D must be stable around the active clock edge.

```text
       Setup       Hold
       <───>       <──>

D ────────████████████────

                ↑

              Clock
```

### Setup time

D must be stable **before** the clock edge.

### Hold time

D must remain stable **after** the clock edge.

These are among the most important concepts in VLSI timing analysis.

---

# 15. Clock Skew — Preview

Suppose the same clock reaches two flip-flops at different times.

```text
Clock source
     │
     ├────────► FF1
     │
     └──────────────► FF2
```

If FF1 receives the clock at 2 ns and FF2 at 2.2 ns:

**Clock Skew=0.2ns**

We'll study this in detail later.

---

# 16. Timing Diagram for D Flip-Flop

Let's consider:

```text
CLK:  ___|‾‾‾|___|‾‾‾|___|‾‾‾|___
```

```
      ↑       ↑       ↑
```

D:    ___‾‾‾‾____‾‾‾‾‾‾____

Q:    ______‾‾‾‾____‾‾‾‾‾‾____

```
      ↑       ↑

    Sample  Sample
```

At each rising edge, the flip-flop samples D.

The Q output then changes after a small clock-to-Q delay.

---

# 17. Timing Diagram Questions ⭐⭐⭐⭐⭐

In placement exams, you may get something like:

```text
CLK:  ↑       ↑       ↑
```

D:    1       0       1

For a positive-edge-triggered D flip-flop:

```text
Q:    1       0       1
```

because:

**Qnext=D**

at each rising edge.

---

# 18. Common Trap ⭐⭐⭐⭐⭐

### Question:

D changes from 0 → 1 halfway between two rising clock edges.

Does Q immediately become 1?

### Answer:

No

It waits for the next active clock edge, assuming timing requirements are satisfied.

This is a very common conceptual question.

---

# 19. Another Common Trap

### Question:

A positive-edge-triggered flip-flop responds to which transition?

Correct:

**0→1**

Not the entire HIGH level.

This is the key distinction between:

**Latch vs Flip-Flop**

---

# 🧠 QUICK REVISION

```text
TIMING DIAGRAMS
────────────────────────

Rising edge:

0 → 1

↑

Falling edge:

1 → 0

↓

Positive-edge FF:

Captures at rising edge

Negative-edge FF:

Captures at falling edge

Clock period:

T = 1/f

Frequency:

f = 1/T

Duty cycle:

THIGH / T × 100%

Clock-to-Q delay:

Time from active clock edge

to Q transition

Important:

D changes between edges

→ Q does NOT immediately follow D

Setup:

D stable BEFORE edge

Hold:

D stable AFTER edge

Clock skew:

Difference in clock arrival

times at different elements
```
