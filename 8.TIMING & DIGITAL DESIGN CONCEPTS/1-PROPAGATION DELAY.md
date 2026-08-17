# PROPAGATION DELAY ⭐⭐⭐⭐⭐

We’ll continue in the same pattern: **concept → formulas → placement points → questions**.

---

# 1. What is Propagation Delay?

When an input of a digital circuit changes, the output **does not change instantly**.

There is a small time delay between:

```text
Input changes
```

```
 ↓
```

Circuit processes signal

```
 ↓
```

Output changes

This delay is called:

**Propagation Delay (tpd)**

### Placement definition

> **Propagation delay is the time required for a change at the input of a digital circuit to produce the corresponding change at its output.**

---

# 2. Why Does Propagation Delay Exist?

Real digital gates are not ideal.

They contain physical components such as:

* Transistors
* Interconnects
* Capacitances
* Resistances

Therefore, when an input changes, the internal nodes need some time to charge or discharge.

So:

**Input change ≠ instantaneous output change**

---

# 3. Example

Consider:

```text id="r5m8k2"
A ──► NOT Gate ──► Y
```

Suppose:

```text id="x3q7n1"
A: 0 → 1
```

Ideally:

```text id="m6v2p9"
Y: 1 → 0
```

But practically:

```text id="t8c4r5"
A changes
```

↓

small delay

↓

Y changes

That delay is:

**tpd**

---

# 4. Propagation Delay in a Waveform ⭐⭐⭐⭐⭐

```text id="k7m2x4"
Input

      ┌────────
      │
──────┘
      ↑
      │ Input changes
      │
      └───────────────


                 tpd

                  ↓

Output

      ┌────────
      │
──────┘
      ↑
      │ Output changes
```

The time between the corresponding input and output transitions is the propagation delay.

---

# 5. Rise and Fall Propagation Delays

There are usually two propagation delays.

### Low → High output

Called:

**tPLH**

### High → Low output

Called:

**tPHL**

Where:

* tPLH = propagation delay for output Low → High
* tPHL = propagation delay for output High → Low

---

# 6. Average Propagation Delay ⭐⭐⭐⭐⭐

A commonly used average is:

**tpd=(tPLH+tPHL)/2**

### Example

Suppose:

**tPLH=4ns**

**tPHL=6ns**

Then:

**tpd=(4+6)/2**

**tpd=5ns**

---

# 7. Very Important Difference

Don't confuse:

**tPLH**

with:

**tPHL**

### Memory trick:

```text id="c4n8q1"
PLH → Propagation Low → High
```

PHL → Propagation High → Low

---

# 8. Propagation Delay Through Multiple Gates ⭐⭐⭐⭐⭐

Suppose:

```text id="y5m1r7"
A
```

↓

Gate 1

↓

Gate 2

↓

Gate 3

↓

Y

Each gate has delay:

```text id="w8p3k6"
Gate 1 = 2 ns
```

Gate 2 = 3 ns

Gate 3 = 4 ns

Total propagation delay:

**tpd,total=2+3+4**

**9ns**

### Important:

For a **serial path**, delays add.

**ttotal=∑tpd**

---

# 9. Placement Numerical ⭐⭐⭐⭐⭐

### Q1.

A signal passes through three gates having delays:

**2ns, 5ns, 3ns**

Find total propagation delay.

### Answer:

**2+5+3=10ns**

**10ns**

---

# 10. Critical Path ⭐⭐⭐⭐⭐

Consider:

```text id="n4q7v2"
Path A:
```

2ns → 3ns → 4ns

Path B:

1ns → 2ns

Path C:

3ns → 5ns

Calculate:

### Path A

**2+3+4=9ns**

### Path B

**1+2=3ns**

### Path C

**3+5=8ns**

Longest path:

**9ns**

Therefore Path A is the **critical path**.

---

# 11. Why Is Critical Path Important?

The critical path determines the **maximum speed** at which a synchronous circuit can operate.

Longer critical path:

**Lower maximum frequency**

Shorter critical path:

**Higher maximum frequency**

---

# 12. Propagation Delay and Clock Frequency ⭐⭐⭐⭐⭐

If the minimum clock period is approximately:

**TCLK=10ns**

Then:

**fmax=1/TCLK**

Since:

**10ns=10×10⁻⁹s**

**fmax=1/(10×10⁻⁹)**

**100MHz**

---

# 13. Important Relationship

Generally:

**More propagation delay → slower circuit**

and:

**Less propagation delay → faster circuit**

---

# 14. Propagation Delay vs Contamination Delay

You will study contamination delay next, but know this basic distinction now.

### Propagation delay

Maximum/settling delay concept:

> How long until the output has responded to the input change.

### Contamination delay

Minimum delay concept:

> The earliest time at which the output can begin responding to an input change.

Memory:

```text id="p6r2m8"
tpd → Maximum delay
```

tcd → Minimum delay

And generally:

**tcd≤tpd**

---

# 15. Gate Delay vs Path Delay

### Gate delay

Delay through one logic gate.

Example:

**tgate=3ns**

### Path delay

Total delay through multiple gates.

Example:

```text id="x7n3q5"
2ns + 3ns + 5ns
```

**tpath=10ns**

---

# 16. 🔥 Placement Trap

### Question:

A circuit contains 5 gates, each having 2 ns propagation delay.

What is the total delay?

Don't answer:

**2ns**

The signal passes through all five gates.

Therefore:

**5×2=10ns**

**10ns**

---

# 17. Parallel Paths

Suppose:

```text id="m8v4c1"
       ┌── Gate A: 3ns ──┐
Input ─┤                  ├── Output
       └── Gate B: 7ns ──┘
```

The longest relevant path is:

**7ns**

For timing analysis, the **maximum-delay path** is important for propagation/maximum-delay constraints.

---

# 18. Placement Questions

### Q2.

What is propagation delay?

**Answer:**

The time between an input transition and the corresponding output transition.

---

### Q3.

What is tPLH?

**Answer:**

Propagation delay when the output changes:

**Low→High**

---

### Q4.

What is tPHL?

**Answer:**

Propagation delay when the output changes:

**High→Low**

---

### Q5.

If:

**tPLH=8ns**

and

**tPHL=12ns**

find average propagation delay.

**Answer:**

**tpd=(8+12)/2**

**10ns**

---

### Q6.

Four gates have delays:

```text id="f9k2m7"
2 ns
```

3 ns

4 ns

1 ns

Total delay?

**Answer:**

**2+3+4+1**

**10ns**

---

### Q7.

Why is propagation delay important in VLSI?

**Answer:**

Because it limits how quickly a digital circuit can operate and therefore affects the **maximum operating frequency**.

---

### Q8.

What is the critical path?

**Answer:**

The path having the **largest propagation delay** among relevant timing paths.

---

### Q9.

Does reducing propagation delay generally increase or decrease circuit speed?

**Answer:**

**Increase speed**

---

# 19. 🔥 Interview Questions

### Q10. Why are tPLH and tPHL sometimes different?

**Answer:**

Because the rising and falling transitions can have different transistor charging/discharging behavior, resistance, capacitance, and circuit characteristics.

---

### Q11. Is propagation delay zero in an ideal digital gate?

**Answer:**

In an idealized model, it may be treated as zero, but real physical gates have non-zero propagation delay.

---

### Q12. Why does a chain of gates have larger delay?

**Answer:**

Because the signal passes through each gate sequentially, so the individual delays accumulate.

---

# 🧠 QUICK REVISION

```text id="d3m7q1"
PROPAGATION DELAY
════════════════════════

Input changes

      ↓

   Delay

      ↓

Output changes


tpd = Propagation Delay


tPLH → Output Low → High

tPHL → Output High → Low


Average:

tpd = (tPLH + tPHL)/2


Multiple serial gates:

Total delay = Sum of delays


Critical path:

Longest delay path


More delay → Lower speed

Less delay → Higher speed


Generally:

tcd ≤ tpd
```
