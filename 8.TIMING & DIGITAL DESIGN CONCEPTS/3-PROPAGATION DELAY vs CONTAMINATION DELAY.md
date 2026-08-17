# PROPAGATION DELAY vs CONTAMINATION DELAY ⭐⭐⭐⭐⭐

This topic is extremely important because placement questions often try to confuse **maximum delay vs minimum delay**.

---

## 1. Core Difference

### Propagation Delay tpd

The **maximum/settling delay** of a combinational circuit.

It tells us approximately:

> How long it takes for the output to respond/settle after an input change.

**tpd=maximum propagation delay**

---

### Contamination Delay tcd

The **minimum delay** before the output can start changing.

**tcd=minimum propagation delay**

---

# 2. The Most Important Memory Trick 🔥

```text
tpd → How LATE?
```

tcd → How EARLY?

Or:

```text
SETUP → tpd → Maximum delay
```

HOLD  → tcd → Minimum delay

This is one of the most useful shortcuts for VLSI placement questions.

---

# 3. Comparison Table

| Feature              | Propagation Delay      | Contamination Delay     |
| -------------------- | ---------------------- | ----------------------- |
| Symbol               | tpd                    | tcd                     |
| Meaning              | Maximum/settling delay | Minimum delay           |
| Output               | Has responded/settled  | Can begin changing      |
| Timing analysis      | Setup                  | Hold                    |
| Path                 | Longest path           | Shortest path           |
| Concern              | Data arriving too late | Data arriving too early |
| Typical relationship | tpd≥tcd                | tcd≤tpd                 |

---

# 4. Example

Suppose:

**tcd=2ns**

**tpd=7ns**

Input changes at:

**t=0**

Then conceptually:

```text
0 ns
```

│

│ Input changes

│

├──── 2 ns ────► Output can BEGIN changing

│

│

├──── 7 ns ────► Output has responded/settled

│

Therefore:

**tcd=2ns**

**tpd=7ns**

---

# 5. Why Does Setup Use Maximum Delay?

Consider:

```text
FF1 ──► Combinational Logic ──► FF2
```

FF1 launches new data.

We need to make sure the data reaches FF2 **before its next active clock edge**.

The worst case is when the data takes the **longest possible time**.

Therefore:

**Setup analysis → maximum delay**

---

# 6. Why Does Hold Use Minimum Delay?

After the clock edge, FF2 requires the old data to remain stable for some time.

The dangerous case is when the new data travels through the combinational logic **as quickly as possible**.

Therefore:

**Hold analysis → minimum delay**

---

# 7. Setup Timing

For a simple zero-skew register-to-register path:

**TCLK≥tCQ(max)+tpd+tsetup**

The maximum combinational delay is used.

---

### Example

Given:

**tCQ=2ns**

**tpd=6ns**

**tsetup=2ns**

Then:

**TCLK(min)=2+6+2**

**10ns**

Therefore:

**fmax=1/10ns**

**100MHz**

---

# 8. Hold Timing

For a simple zero-skew case:

**tCQ(min)+tcd≥thold**

---

### Example

Given:

**tCQ(min)=2ns**

**tcd=3ns**

**thold=4ns**

Check:

**2+3=5ns**

Since:

**5≥4**

**No hold violation**

---

# 9. 🔥 Placement Trap

### Question:

Which delay is used when calculating maximum clock frequency?

Some students answer:

> Contamination delay.

❌ Wrong.

Correct:

**tpd**

because maximum clock frequency is limited by the **longest timing path**.

---

# 10. 🔥 Another Trap

### Question:

Which delay is used to check whether new data arrives too early?

Correct:

**tcd**

because hold timing is a **minimum-delay problem**.

---

# 11. Setup vs Hold — Complete Picture

```text
                 CLOCK
                   ↑
                   │
          Capture clock edge
                   │
───────────────────┼──────────────────► Time
                   │
        ← Setup →  │  ← Hold →
```

### Setup:

Data must be stable **before** the clock edge.

### Hold:

Data must remain stable **after** the clock edge.

---

# 12. Setup Violation

Suppose data arrives:

**too late**

Then:

**Setup violation**

Typical fix:

**Reduce maximum data-path delay**

---

# 13. Hold Violation

Suppose new data arrives:

**too early**

Then:

**Hold violation**

Typical fix:

**Increase minimum data-path delay**

---

# 14. 🔥 Most Important Relationship

```text
SETUP
```

↓

Maximum delay

↓

tpd

↓

Longest path

↓

Maximum frequency

```text
HOLD
```

↓

Minimum delay

↓

tcd

↓

Shortest path

↓

Hold violation

Memorize this chain.

---

# 15. Placement Questions

### Q1.

Which is generally greater?

A. tpd
B. tcd

**Answer:**

**tpd≥tcd**

---

### Q2.

Which delay is associated with the **minimum-delay path**?

**tcd**

---

### Q3.

Which delay is associated with the **maximum-delay path**?

**tpd**

---

### Q4.

Which delay is primarily important for setup analysis?

**tpd**

---

### Q5.

Which delay is primarily important for hold analysis?

**tcd**

---

### Q6.

A circuit has:

**tCQ(max)=3ns**

**tpd=7ns**

**tsetup=2ns**

Find minimum clock period.

**TCLK(min)=3+7+2**

**12ns**

---

### Q7.

Using the previous question, find maximum clock frequency.

**fmax=1/12ns**

**83.33MHz**

---

### Q8.

Given:

**tCQ(min)=1ns**

**tcd=2ns**

**thold=4ns**

Does hold timing pass?

**1+2=3ns**

**3<4**

Therefore:

**Hold violation**

---

# 16. Interview Question ⭐⭐⭐⭐⭐

### Q9. Can increasing combinational delay fix a setup violation?

**Answer:**

No.

Increasing the maximum data-path delay makes setup timing worse.

For setup, we generally want:

**Lower maximum delay**

---

### Q10. Can increasing combinational delay help a hold violation?

**Answer:**

Yes.

Increasing the **minimum data-path delay** can prevent the new data from arriving too early.

**More minimum delay → better hold timing**

---

# 🧠 FINAL REVISION

```text
             DIGITAL TIMING
                  │
       ┌──────────┴──────────┐
       ↓                     ↓
    SETUP                   HOLD
       ↓                     ↓
 Maximum delay           Minimum delay
       ↓                     ↓
     tpd                   tcd
       ↓                     ↓
 Longest path            Shortest path
       ↓                     ↓
Data too late           Data too early
       ↓                     ↓
Setup violation         Hold violation
```

### 🔥 One-line memory

**SETUP = MAX = tpd**

**HOLD = MIN = tcd**
