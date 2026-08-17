# PROPAGATION DELAY & CONTAMINATION DELAY ⭐⭐⭐⭐⭐

This is another important timing concept for VLSI placements.

These two are often confused, so we'll keep the distinction very clear.

---

# 1. Why Do We Need These Delays?

Real logic gates don't change their outputs instantly.

Suppose:

```text id="x1"
A ───► AND ───► Y
```

If A changes, Y takes some amount of time to respond.

There are two important delay parameters:

**tpd = Propagation Delay**

**tcd = Contamination Delay**

---

# 2. Propagation Delay ⭐⭐⭐⭐⭐

### Definition

Propagation delay is the **maximum time** from an input transition to the corresponding output becoming valid.

Think:

> **How long can the circuit take to produce the new correct output?**

Symbol:

**tpd**

---

# 3. Example

Suppose input changes at:

**10ns**

and output becomes valid at:

**12ns**

Then:

**tpd=12−10**

**tpd=2ns**

---

# 4. Contamination Delay ⭐⭐⭐⭐⭐

Contamination delay is the **minimum time** after an input changes before the output can begin to change.

Symbol:

**tcd**

Think:

> **How soon can the old output become invalid?**

---

# 5. Example

Suppose input changes at:

**10ns**

The output can start changing as early as:

**10.5ns**

Therefore:

**tcd=10.5−10**

**tcd=0.5ns**

---

# 6. The Most Important Difference ⭐⭐⭐⭐⭐

| Propagation Delay          | Contamination Delay                  |
| -------------------------- | ------------------------------------ |
| Maximum delay              | Minimum delay                        |
| Time until output is valid | Time until output can begin changing |
| tpd                        | tcd                                  |
| Related to setup timing    | Related to hold timing               |

### Memory trick:

> **Propagation = How late?**

> **Contamination = How early?**

---

# 7. Timing Diagram

```text id="dyq4"
Input:
```

```
   ───────┐
          │
          └────────────
          ↑
         Input
        transition
```

Output:

```
   ───────────────┐
                  │
                  └────────
                  ↑
             Can start changing
             after tcd

             ↑
             Output guaranteed
             valid after tpd
```

````

After the input changes:

### First:

Output **may begin changing** after:

**tcd**

### Later:

Output is guaranteed to have reached its correct value after:

**tpd**

So:

**tcd≤tpd**

---

# 8. Why Contamination Delay Matters for Hold Time ⭐⭐⭐⭐⭐

Consider:

```text id="4e8b"
FF1 ──► Logic ──► FF2
````

FF1 launches new data.

If the logic path is **too fast**, the new data can reach FF2 too soon.

This can cause a **hold violation**.

The minimum delay through the path is therefore important.

That's why:

**Contamination delay is closely related to hold timing**

---

# 9. Why Propagation Delay Matters for Setup Time ⭐⭐⭐⭐⭐

If the logic path is too slow, the new data may not reach FF2 before the next clock edge.

That causes a **setup violation**.

Therefore:

**Propagation delay is closely related to setup timing**

---

# 10. Simple Relationship

Remember:

```text id="m2e5"
Setup → maximum delay → tpd
```

Hold → minimum delay → tcd

This is an excellent placement shortcut.

---

# 11. Example

Suppose a combinational circuit has:

**tcd=2ns**

**tpd=8ns**

Input changes at:

**10ns**

Then:

### Earliest output can change:

**10+2=12ns**

### Output guaranteed valid:

**10+8=18ns**

Therefore:

**12ns≤Output change≤18ns**

The exact transition depends on the circuit and input/output paths.

---

# 12. Critical Path ⭐⭐⭐⭐⭐

Now connect this to setup timing.

Suppose:

```text id="g0b6"
FF1 → Gate → Gate → Gate → FF2
```

The path with the **largest propagation delay** is often called the:

**Critical Path**

The critical path determines the maximum operating frequency of a synchronous circuit.

---

# 13. Why Critical Path Matters

Suppose there are two paths:

### Path A

**tpd=3ns**

### Path B

**tpd=8ns**

Path B is slower.

Therefore Path B is the critical path.

The clock period must be large enough to allow this path to complete.

So approximately:

**Tclk≥tCQ+tcritical+tsetup**

---

# 14. Example

Suppose:

**tCQ=1ns**

**tcritical=6ns**

**tsetup=1ns**

Then:

**Tclk≥1+6+1**

**Tclk≥8ns**

Maximum frequency:

**fmax=1/8ns**

**fmax=125MHz**

---

# 15. What Happens if We Reduce Critical Path Delay?

Suppose we optimize:

**6ns→4ns**

Then:

**Tclk≥1+4+1**

**Tclk≥6ns**

Therefore:

**fmax=1/6ns**

**fmax≈166.7MHz**

So reducing critical path delay allows a higher clock frequency.

---

# 16. Common Ways to Reduce Propagation Delay

In digital/VLSI design, techniques can include:

* Reducing logic depth
* Optimizing gate sizing
* Using faster cells
* Reducing fanout
* Optimizing routing
* Better physical placement

The exact technique depends on the design stage.

---

# 17. Fanout ⭐⭐⭐⭐

Fanout is the number of gate inputs driven by one output.

Example:

```text id="q5gp"
              ┌──► Gate 1
              │
Output ───────┼──► Gate 2
              │
              ├──► Gate 3
              │
              └──► Gate 4
```

Here the output drives:

**4 inputs**

So fanout = 4.

High fanout can increase load and delay.

---

# 18. Why High Fanout Matters

More loads mean greater capacitance.

Greater capacitance generally means:

**More delay**

Therefore high fanout can hurt timing.

Buffers may be inserted to help drive large loads.

---

# 19. Placement Questions ⭐⭐⭐⭐⭐

### Q1. What is propagation delay?

Maximum time from input transition until output becomes valid.

---

### Q2. What is contamination delay?

Minimum time after an input transition before the output can begin changing.

---

### Q3. Which is larger?

Generally:

**tpd≥tcd**

---

### Q4. Which delay is mainly associated with setup timing?

**Propagation delay**

---

### Q5. Which delay is mainly associated with hold timing?

**Contamination delay**

---

### Q6. What is a critical path?

The longest/highest-delay timing path that limits the maximum operating frequency.

---

### Q7. Why is the critical path important?

It determines the minimum feasible clock period and therefore approximately the maximum clock frequency.

---

### Q8. What happens if critical-path delay decreases?

**fmax increases**

---

### Q9. What is fanout?

Number of inputs/load elements driven by a gate output.

---

### Q10. Can high fanout increase delay?

Yes

because the output sees a larger load.

---

# 🧠 QUICK REVISION

```text id="r4p4"
PROPAGATION & CONTAMINATION
──────────────────────────────

Propagation delay (tpd):

Maximum delay.

Input → output becomes valid.

Contamination delay (tcd):

Minimum delay.

Input → output can BEGIN changing.

Generally:

tcd ≤ tpd

MEMORY:

Propagation → "How late?"

Contamination → "How early?"

Setup:

Related to maximum delay / tpd

Hold:

Related to minimum delay / tcd

Critical path:

Longest/highest-delay path.

Critical path limits:

→ Minimum clock period

→ Maximum frequency

High fanout:

More load → generally more delay
```
