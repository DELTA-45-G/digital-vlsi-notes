# CLOCK-TO-Q DELAY ⭐⭐⭐⭐⭐

Now we continue in the exact Phase 8 order.

---

## 1. What is Clock-to-Q Delay?

When a clock edge arrives at a flip-flop, the output **Q does not change instantaneously**.

The time between the active clock edge and the corresponding change in Q is called **clock-to-Q delay**.

**tCQ=delay between clock edge and Q output transition**

### Placement definition

> **Clock-to-Q delay is the time taken by a flip-flop to produce a valid output after the active clock edge.**

---

# 2. Simple Example

Consider a positive-edge-triggered flip-flop:

```text
        ┌─────────┐
D ─────►│         │────► Q
CLK ───►│   D FF  │
        └─────────┘
```

Suppose the clock edge occurs at:

**t=10ns**

and Q changes at:

**t=12ns**

Then:

**tCQ=12−10**

**tCQ=2ns**

---

# 3. Timing Diagram

```text
Clock

───────────────↑────────────────────

               │

               │

               │←── tCQ ──→│

               │            │

Q              ─────────────↑────────

                            Q changes
```

So:

**Clock edge → Q change = tCQ**

---

# 4. Why Does Clock-to-Q Delay Exist?

A flip-flop contains internal transistors and storage nodes.

When the clock edge arrives:

```text
Clock edge
```

```
↓
```

Internal FF operation

```
↓
```

Storage changes

```
↓
```

Q changes

This process requires a finite amount of time.

Therefore:

**tCQ>0**

for a real circuit.

---

# 5. Clock-to-Q vs Propagation Delay ⭐⭐⭐⭐⭐

Do not confuse these.

### Clock-to-Q delay

Delay **through a flip-flop**:

**Clock→Q**

### Propagation delay

Delay through **combinational logic**:

**Input→Output**

Example:

```text
Clock
```

↓

FF1

↓

Q

↓

Combinational Logic

↓

FF2

There are two different delays:

**tCQ**

and

**tpd**

---

# 6. Register-to-Register Path ⭐⭐⭐⭐⭐

This is extremely important.

```text
       Combinational Logic

FF1 ─────────────────────────► FF2
 │                              │
 │                              │
 └── Clock-to-Q                 └── Setup
```

After the launch clock edge:

```text
Clock edge
```

↓

FF1 Q changes after tCQ

↓

Combinational logic

↓

Data arrives at FF2

↓

Must satisfy setup time

↓

Next clock edge

Therefore the setup equation contains:

**tCQ+tpd+tsetup**

---

# 7. Setup Timing Equation

For a simple zero-skew register-to-register path:

**TCLK≥tCQ(max)+tpd+tsetup**

This is one of the most important equations in Phase 8.

---

# 8. Example

Given:

**tCQ(max)=2ns**

**tpd=5ns**

**tsetup=2ns**

Then:

**TCLK(min)=2+5+2**

**9ns**

Maximum frequency:

**fmax=1/9ns**

**111.11MHz**

---

# 9. Why Do We Use Maximum tCQ for Setup?

Setup analysis is a **maximum-delay problem**.

We are worried about data arriving **too late**.

Therefore we use:

**tCQ(max)**

and:

**tpd(max)**

---

# 10. Why Do We Use Minimum tCQ for Hold?

Hold analysis is a **minimum-delay problem**.

We are worried about data arriving **too early**.

Therefore:

**tCQ(min)**

is used.

The basic hold equation is:

**tCQ(min)+tcd≥thold**

---

# 11. 🔥 Very Important Table

| Timing | Clock-to-Q | Combinational Delay |
| ------ | ---------- | ------------------- |
| Setup  | tCQ(max)   | tpd(max)            |
| Hold   | tCQ(min)   | tcd(min)            |

### Memory:

```text
SETUP → MAX + MAX
```

HOLD  → MIN + MIN

---

# 12. Clock-to-Q Rise and Fall

Similar to propagation delay, clock-to-Q can differ depending on whether Q changes:

* Low → High
* High → Low

You may encounter:

**tCQ,LH**

and

**tCQ,HL**

For basic placement preparation, remember the concept rather than focusing heavily on notation.

---

# 13. Placement Numerical ⭐⭐⭐⭐⭐

### Q1.

A flip-flop receives an active clock edge at:

**20ns**

Q changes at:

**23ns**

Find tCQ.

**tCQ=23−20**

**3ns**

---

# 14. Placement Numerical

### Q2.

Given:

**tCQ=3ns**

**tpd=6ns**

**tsetup=2ns**

Find minimum clock period.

**TCLK(min)=3+6+2**

**11ns**

---

# 15. Maximum Frequency

For:

**TCLK=11ns**

**fmax=1/(11×10⁻⁹)**

**90.91MHz**

---

# 16. Placement Trap 🔥

### Question:

A circuit has:

**tCQ=4ns**

**tpd=5ns**

**tsetup=2ns**

What is the total data-path timing requirement?

Wrong:

**5+2=7ns**

You must include clock-to-Q:

**4+5+2**

**11ns**

---

# 17. Another Placement Trap

### Q.

Does clock-to-Q delay belong to the combinational logic delay?

No

It is the delay of the **launch flip-flop**.

```text
FF1
```

↓

tCQ

↓

Combinational Logic

↓

tpd

↓

FF2

---

# 18. Critical Path Connection ⭐⭐⭐⭐⭐

Suppose:

```text
FF1
```

↓

tCQ = 2ns

↓

Gate 1 = 3ns

↓

Gate 2 = 4ns

↓

Gate 3 = 2ns

↓

FF2

Total timing requirement:

**2+3+4+2**

plus setup time.

If:

**tsetup=1ns**

Then:

**TCLK(min)=2+3+4+2+1**

**12ns**

---

# 19. What Happens If tCQ Increases?

Suppose:

**tCQ:2ns→4ns**

Then more time is consumed before data enters the combinational path.

Therefore:

**TCLK(min)↑**

and:

**fmax↓**

So:

**Higher tCQ→lower maximum frequency**

---

# 20. Interview Questions ⭐⭐⭐⭐⭐

### Q1. What is clock-to-Q delay?

**Answer:**

The time between the active clock edge and the corresponding change in the flip-flop's Q output.

---

### Q2. Why is clock-to-Q delay important?

**Answer:**

Because it consumes part of the available clock period in a register-to-register path and therefore affects maximum operating frequency.

---

### Q3. Which tCQ is used for setup analysis?

**tCQ(max)**

---

### Q4. Which tCQ is used for hold analysis?

**tCQ(min)**

---

### Q5. What happens to fmax if tCQ increases?

**fmax decreases**

---

# 🧠 QUICK REVISION

```text
CLOCK-TO-Q DELAY
══════════════════════════

Clock edge

    ↓

  tCQ

    ↓

Q changes


SETUP PATH:

Clock

 ↓

FF1

 ↓ tCQ(max)

Combinational Logic

 ↓ tpd(max)

FF2

 ↓

Setup requirement


Equation:

TCLK ≥ tCQ(max) + tpd(max) + tsetup


HOLD:

tCQ(min) + tcd(min) ≥ thold


Memory:

SETUP → MAX tCQ + MAX tpd

HOLD  → MIN tCQ + MIN tcd
```
