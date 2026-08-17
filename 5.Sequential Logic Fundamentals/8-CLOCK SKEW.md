# CLOCK SKEW ⭐⭐⭐⭐⭐

Now we move to **Clock Skew**, another important VLSI placement topic.

---

## 1. What is Clock Skew?

Ideally, the clock should reach all flip-flops at exactly the same time.

In a real circuit, this doesn't happen.

The difference in clock arrival time between two sequential elements is called:

**Clock Skew**

---

## 2. Simple Example

Consider two flip-flops:

```text
             ┌────► FF1
Clock ───────┤
             └────────► FF2
```

Suppose the clock reaches:

* FF1 at **2 ns**
* FF2 at **2.5 ns**

Then:

**Clock Skew = 2.5 − 2 = 0.5 ns**

---

# 3. Why Does Clock Skew Occur?

Because the clock signal travels through a physical network.

Different paths can have different:

* Wire lengths
* Buffers
* Gates
* Capacitances
* Routing delays

Example:

```text
                    ┌──── Buffer ────► FF1
CLK ───── Buffer ───┤
                    │
                    └──── Buffer ── Buffer ──► FF2
```

The two flip-flops may receive the clock at different times.

---

# 4. Positive and Negative Clock Skew ⭐⭐⭐⭐⭐

Suppose:

* Launch flip-flop = FF1
* Capture flip-flop = FF2

### Positive skew

Capture clock arrives **later** than launch clock.

**tcapture > tlaunch**

Example:

```text
FF1 clock = 2 ns
FF2 clock = 2.5 ns
```

Skew = +0.5 ns

### Negative skew

Capture clock arrives **earlier** than launch clock.

**tcapture < tlaunch**

Example:

```text
FF1 clock = 2.5 ns
FF2 clock = 2 ns
```

Skew = -0.5 ns

---

# 5. Effect of Clock Skew on Setup Timing ⭐⭐⭐⭐⭐

This is important.

Consider:

```text
FF1 ───► Combinational Logic ───► FF2
```

↑                                  ↑

Launch                           Capture

If the capture clock arrives **later**, FF2 gets more time to receive the data.

Therefore:

**Positive skew generally helps setup timing**

---

# 6. Effect on Hold Timing ⭐⭐⭐⭐⭐

But there's a trade-off.

If FF2's clock arrives later, FF2 may capture/hold the previous data for a longer relative interval, making the receiving flip-flop more vulnerable to new data arriving too early.

Therefore:

**Positive skew generally hurts hold timing**

So remember:

| Clock Skew    | Setup | Hold  |
| ------------- | ----- | ----- |
| Positive skew | Helps | Hurts |
| Negative skew | Hurts | Helps |

⭐ This table is **very important for VLSI interviews**.

---

# 7. Why Positive Skew Helps Setup

Suppose:

**Tclk=10ns**

Without skew, FF2 captures at:

10ns

Now suppose positive skew is:

+1ns

FF2 captures at:

11ns

The data has an extra:

1ns

to reach FF2.

Therefore setup timing improves.

---

# 8. Why Positive Skew Hurts Hold

Now consider the same situation.

FF2's clock arrives later.

The new data from FF1 can arrive during the hold window of FF2.

Therefore the later capture edge can make it harder to satisfy hold timing.

So:

**Positive skew → Setup better, Hold worse**

---

# 9. Negative Skew

If the capture clock arrives earlier:

**Negative skew**

then FF2 gets less time to receive the data.

Therefore:

**Setup becomes harder**

But the earlier capture edge gives more protection against new data changing too soon after the capture event:

**Hold generally improves**

---

# 10. Clock Skew vs Clock Jitter ⭐⭐⭐⭐⭐

These are different.

### Clock Skew

Difference in clock arrival time between **different locations/elements**.

**Spatial difference**

### Clock Jitter

Variation in the clock edge timing from cycle to cycle.

**Temporal variation**

Example:

### Skew

```text
FF1 clock → 2.0 ns
```

FF2 clock → 2.5 ns

Difference = 0.5 ns.

### Jitter

Expected clock edge:

10ns

Actual edges:

9.9ns, 10.1ns, 9.95ns, 10.05ns

The edge moves around its expected position.

---

# 11. Clock Skew in VLSI ⭐⭐⭐⭐⭐

In physical design, the clock network is carefully designed so that clock arrival times are controlled.

A common structure is a:

**Clock Tree**

The process of designing the clock tree to distribute the clock properly is called:

**Clock Tree Synthesis (CTS)**

CTS tries to control:

* Clock skew
* Clock latency
* Slew
* Clock power

We'll study CTS more deeply later if your VLSI roadmap includes physical design concepts.

---

# 12. Clock Latency vs Clock Skew

Another common interview distinction.

### Clock latency

Time taken for the clock to travel from the clock source to a particular flip-flop.

Example:

**Clock source → FF = 2ns**

Latency:

2ns

### Clock skew

Difference between arrival times at two flip-flops.

Example:

**FF1=2ns FF2=2.5ns**

Skew:

0.5ns

---

# 13. Important Interview Table ⭐⭐⭐⭐⭐

| Concept         | Meaning                    |
| --------------- | -------------------------- |
| Clock period    | Time for one clock cycle   |
| Clock frequency | Cycles per second          |
| Clock latency   | Source → flip-flop delay   |
| Clock skew      | Difference in arrival time |
| Clock jitter    | Variation in edge timing   |
| Clock-to-Q      | Clock edge → Q delay       |

---

# 14. Placement Questions

### Q1. What is clock skew?

Difference in clock arrival time between two sequential elements.

**tcapture − tlaunch**

---

### Q2. What is positive clock skew?

Capture clock arrives later than launch clock.

---

### Q3. What is negative clock skew?

Capture clock arrives earlier than launch clock.

---

### Q4. Does positive skew generally help setup?

Yes

---

### Q5. Does positive skew generally hurt hold?

Yes

---

### Q6. What is the difference between skew and jitter?

**Skew:** Difference between clock arrival times at different elements.

**Jitter:** Variation of clock edge timing over time.

---

### Q7. What is clock latency?

Time taken for the clock to travel from its source to a particular sequential element.

---

### Q8. What is CTS?

**Clock Tree Synthesis**

It is used to build the clock distribution network and control clock timing characteristics such as skew.

---

# 🧠 QUICK REVISION

```text
CLOCK SKEW
────────────────────────────

Clock skew:

Difference in clock arrival

time between two elements.

Positive skew:

Capture clock arrives later.

Negative skew:

Capture clock arrives earlier.

Positive skew:

✓ Setup → Better

✗ Hold  → Worse

Negative skew:

✗ Setup → Worse

✓ Hold  → Better

Skew:

Spatial difference

Jitter:

Temporal variation

Latency:

Clock source → element delay

CTS:

Clock Tree Synthesis
```
