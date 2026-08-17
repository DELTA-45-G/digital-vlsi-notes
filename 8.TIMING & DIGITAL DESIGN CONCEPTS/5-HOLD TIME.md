# &#x20;HOLD TIME ⭐⭐⭐⭐⭐

Now we continue in the correct order.

---

## 1. What is Hold Time?

**Hold time** is the minimum amount of time for which the input data must remain stable **after the active clock edge**.

**thold=minimum time data must remain stable after the clock edge**

### Placement definition

> **Hold time is the minimum time for which data must remain stable after the active clock edge for reliable capture.**

---

# 2. Setup vs Hold — First Remember This 🔥

```text id="j2k8m4"
SETUP → BEFORE clock edge
```

HOLD  → AFTER clock edge

Think:

> **Setup = prepare before**

> **Hold = keep holding after**

---

# 3. Timing Diagram

```text id="m5q1v9"
                 │←── Hold Time ──→│
                 │                  │
Data ────────────████████████████████────
                 │                  │
                 ↑                  │
              Clock edge            │
```

At the active clock edge, the flip-flop captures the data.

The data must **not change immediately afterward**.

---

# 4. Why is Hold Time Required?

The flip-flop needs some time after the clock edge to complete the internal capture process.

Therefore:

**Data must remain stable after the clock edge**

---

# 5. Hold Violation ⭐⭐⭐⭐⭐

A hold violation occurs when the input data changes **too soon after the active clock edge**.

Example:

**thold=3ns**

But data changes only:

**2ns**

after the clock edge.

Since:

**2ns<3ns**

**Hold violation**

---

# 6. Hold Timing Equation ⭐⭐⭐⭐⭐

For a basic zero-skew register-to-register path:

**tCQ(min)+tcd≥thold**

Where:

* tCQ(min) = minimum clock-to-Q delay
* tcd = contamination delay
* thold = hold time

---

# 7. Example — Hold Timing Pass

Given:

**tCQ(min)=2ns**

**tcd=4ns**

**thold=5ns**

Check:

**2+4=6ns**

Since:

**6≥5**

**Hold timing passes**

---

# 8. Example — Hold Violation

Given:

**tCQ(min)=1ns**

**tcd=2ns**

**thold=5ns**

Then:

**1+2=3ns**

But:

**3<5**

Therefore:

**Hold violation**

---

# 9. Why Does Hold Use Contamination Delay?

Because hold analysis is concerned with the **earliest possible arrival of new data**.

The earliest output change is determined by:

**tcd**

Therefore:

**HOLD → minimum delay → tcd**

---

# 10. Hold Violation — Intuition ⭐⭐⭐⭐⭐

Consider:

```text id="q4r8n2"
FF1                  FF2
```

│                    │

└──► Fast Logic ────►│

```
                   ↑

                Capture
```

````

If the combinational path is **too fast**, new data can reach FF2 too quickly.

That can overwrite/change the data before FF2 has completed its hold requirement.

Therefore:

**Very short path → possible hold violation**

---

# 11. How to Fix Hold Violation? ⭐⭐⭐⭐⭐

Unlike setup violations, we generally want to **increase the minimum data-path delay**.

For example:

```text id="w6m3p9"
Before:
````

FF1 ──► Logic ──► FF2

After:

FF1 ──► Logic ──► Buffer ──► FF2

The buffer adds delay.

Therefore:

**tcd↑**

and hold timing improves.

### Memory:

**HOLD violation → slow down the data path**

---

# 12. Very Important Trap 🔥

### Q.

Does increasing clock frequency necessarily cause a hold violation?

**Answer:**

Not in the same direct way as setup timing.

For a basic zero-skew hold check:

**tCQ(min)+tcd≥thold**

There is **no clock-period term** in this basic equation.

Therefore, increasing clock frequency directly makes setup harder, but it does not automatically create a hold violation in the simple zero-skew model.

---

# 13. Setup vs Hold — Complete Comparison ⭐⭐⭐⭐⭐

| Feature        | Setup           | Hold                           |
| -------------- | --------------- | ------------------------------ |
| Data stability | Before clock    | After clock                    |
| Main delay     | tpd             | tcd                            |
| Path           | Longest         | Shortest                       |
| Problem        | Data too late   | Data too early                 |
| Fix            | Speed up path   | Slow down path                 |
| Clock period   | Important       | Not directly in basic equation |
| Violation      | Setup violation | Hold violation                 |

---

# 14. Hold Slack ⭐⭐⭐⭐⭐

A simple hold slack expression is:

**Slackhold=tCQ(min)+tcd−thold**

### Positive slack

**Hold timing passes**

### Zero slack

**Exactly meets timing**

### Negative slack

**Hold violation**

---

# 15. Hold Slack Example

Given:

**tCQ(min)=2ns**

**tcd=3ns**

**thold=4ns**

Then:

**Slack=2+3−4**

**+1ns**

Therefore:

**Hold passes**

---

# 16. Negative Hold Slack

Given:

**tCQ(min)=1ns**

**tcd=2ns**

**thold=5ns**

Then:

**Slack=1+2−5**

**−2ns**

Therefore:

**Hold violation**

---

# 17. 🔥 Setup and Hold Timing Together

```text id="d8c2m7"
                CLOCK
                  ↑
                  │
       ┌──────────┼──────────┐
       │          │          │
       │← SETUP →│←─ HOLD ─→│
       │          │          │
───────███████████│███████████────── Data
                  ↑
             Active edge
```

### Before clock:

**Setup**

### After clock:

**Hold**

---

# 18. Placement Questions ⭐⭐⭐⭐⭐

### Q1.

What is hold time?

**Answer:**

The minimum time for which data must remain stable after the active clock edge.

---

### Q2.

Which delay is mainly used in hold analysis?

**tcd**

---

### Q3.

Which path is dangerous for hold timing?

**Shortest/fastest path**

---

### Q4.

If data changes too soon after the clock edge, what occurs?

**Hold violation**

---

### Q5.

What happens if:

**tCQ(min)+tcd<thold**

?

**Hold violation**

---

### Q6.

Given:

**tCQ(min)=2ns**

**tcd=5ns**

**thold=4ns**

Pass or fail?

**2+5=7ns**

**7>4**

**PASS**

---

### Q7.

Given:

**tCQ(min)=2ns**

**tcd=1ns**

**thold=5ns**

Pass or fail?

**2+1=3ns**

**3<5**

**FAIL — Hold violation**

---

### Q8.

How can you generally fix a hold violation?

**Increase minimum data-path delay**

---

### Q9.

How can you generally fix a setup violation?

**Decrease maximum data-path delay**

---

# 🧠 QUICK REVISION

```text id="r6n2v8"
HOLD TIME
══════════════════════════

Data must remain stable

AFTER the active clock edge.


Hold equation:

tCQ(min) + tcd ≥ thold


HOLD VIOLATION:

tCQ(min) + tcd < thold


Hold problem:

→ Data arrives TOO EARLY

→ Short/fast path

→ Increase minimum path delay


SETUP:

→ Data arrives TOO LATE

→ Long/slow path

→ Decrease maximum path delay
```

## 🔥 One-line memory

**SETUP → BEFORE → MAX → tpd**

**HOLD → AFTER → MIN → tcd**
