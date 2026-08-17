# TIMING DERATING & OCV ⭐⭐⭐⭐⭐

This is the next topic in the **Phase 8 order**. It builds directly on **PVT corners + STA**.

---

# 1. Why Do We Need OCV?

Previously, we assumed that all transistors/cells on a chip behave according to the same PVT corner.

But in a real chip, different parts of the same chip can have slightly different characteristics.

For example:

```text id="q5m8v2"
Same chip
```

Region A → slightly faster

Region B → slightly slower

Region C → slightly faster

This is called:

**On-Chip Variation (OCV)**

---

# 2. What is OCV? ⭐⭐⭐⭐⭐

**OCV = On-Chip Variation**

It represents variations in timing characteristics between different locations or components **on the same chip**.

### Placement definition:

> **OCV is the variation in cell and interconnect timing across different parts of the same chip due to manufacturing and operating variations.**

---

# 3. PVT vs OCV

This distinction is important.

### PVT

Describes overall operating conditions:

```text id="m4n7x1"
Process
```

Voltage

Temperature

### OCV

Accounts for variations **within the same chip**.

Memory:

**PVT → Global condition**

**OCV → On-chip variation**

---

# 4. Why Does OCV Matter?

Suppose:

```text id="v8r2k5"
Launch path → slightly slow
```

Capture path → slightly fast

This combination can make setup timing worse.

Or:

```text id="x3m7q9"
Launch path → slightly fast
```

Capture path → slightly slow

This can affect hold timing.

Therefore, STA needs to account for these variations.

---

# 5. What is Timing Derating?

**Timing derating** means applying a factor to nominal timing values to account for variations and uncertainties.

For example:

Suppose nominal cell delay:

**10ns**

and derating factor:

**1.10**

Then:

**10×1.10=11ns**

So the derated delay becomes:

**11ns**

---

# 6. Why Use Derating?

Because actual silicon may not behave exactly like nominal timing models.

Derating provides timing margin for variation.

Conceptually:

```text id="u2m6q8"
Nominal delay
```

```
  ↓
```

Apply derating

```
  ↓
```

More conservative delay

```
  ↓
```

STA

---

# 7. Early and Late Derates ⭐⭐⭐⭐⭐

Timing analysis can use different derates.

### Late derate

Makes a path effectively **slower**.

Used when analyzing situations where a later arrival is worse.

### Early derate

Makes a path effectively **faster**.

Used when analyzing situations where an earlier arrival is worse.

Memory:

**Late → Slower**

**Early → Faster**

---

# 8. Setup and OCV

Setup timing is concerned with data arriving too late.

Worst-case intuition:

```text id="d7p3m9"
Launch clock → late
```

Data path    → slow

Capture clock → early

This makes the available setup time smaller.

Therefore:

**Setup analysis uses pessimistic late/early combinations**

---

# 9. Hold and OCV

Hold timing is concerned with data arriving too early.

Worst-case intuition:

```text id="k4x8n2"
Launch clock → early
```

Data path    → fast

Capture clock → late

This makes hold more difficult.

Therefore:

**Hold analysis uses the opposite pessimistic combination**

---

# 10. 🔥 Important Memory

### Setup worst case

```text id="n5m2v7"
Data → SLOW
```

Arrival → LATE

### Hold worst case

```text id="p8q3r6"
Data → FAST
```

Arrival → EARLY

So:

**Setup → Late**

**Hold → Early**

---

# 11. Simple OCV Example

Suppose nominal data delay:

**8ns**

Late derating factor:

**1.10**

Then:

**8×1.10=8.8ns**

Therefore:

**Late derated delay=8.8ns**

---

# 12. Early Derating Example

Suppose:

**Delay=8ns**

Early derating factor:

**0.90**

Then:

**8×0.90=7.2ns**

Therefore:

**Early derated delay=7.2ns**

---

# 13. OCV and Clock Paths ⭐⭐⭐⭐⭐

OCV can affect both:

* Data paths
* Clock paths

Example:

```text id="t4m9x1"
Launch Clock
```

```
 ↓
```

FF1

```
 ↓
```

Data Logic

```
 ↓
```

FF2

```
 ↑
```

Capture Clock

The launch and capture clock paths may experience different variations.

This can change the effective timing relationship.

---

# 14. OCV and Clock Skew

Remember:

**Clock Skew=tcapture−tlaunch**

If OCV causes different clock-path delays, effective skew can change.

Therefore:

**OCV can affect timing through clock variation**

---

# 15. Why OCV is Important in Advanced VLSI

As technology becomes smaller:

* Variations become more significant
* Timing margins become tighter
* Manufacturing differences matter more

Therefore:

**Variation-aware STA becomes important**

---

# 16. AOCV ⭐⭐⭐⭐

You may encounter:

**AOCV**

which stands for:

**Advanced On-Chip Variation**

AOCV provides more refined derating than basic OCV.

Instead of using a single simple derating factor everywhere, AOCV can account for factors such as:

* Path depth
* Distance
* Variation characteristics

For placement preparation:

**AOCV → More accurate variation modeling**

---

# 17. POCV ⭐⭐⭐⭐

Another term you may encounter:

**POCV**

**POCV = Parametric On-Chip Variation**

It uses statistical/parametric variation models rather than simple fixed derating factors.

For interviews:

```text id="s6k2m8"
OCV
```

↓

AOCV

↓

POCV

Think:

> Increasingly refined approaches to modeling on-chip variation.

---

# 18. OCV vs AOCV vs POCV

| Method | Basic idea                                         |
| ------ | -------------------------------------------------- |
| OCV    | Basic on-chip variation derating                   |
| AOCV   | More refined, considers factors such as path depth |
| POCV   | Parametric/statistical variation modeling          |

You don't need to memorize detailed mathematical models for basic placement interviews unless specifically asked.

---

# 19. Why Does Path Depth Matter?

Consider:

```text id="w3m7q2"
Path A:
```

FF → Gate → FF

Path B:

FF → Gate → Gate → Gate → Gate → Gate → FF

The number of cells differs.

Variation behavior can therefore differ between paths.

AOCV can account for such effects more accurately than a simple fixed derate.

---

# 20. OCV and Timing Pessimism

OCV analysis can sometimes make timing analysis overly pessimistic.

For example:

```text id="v9n4x6"
Launch clock → slow assumption
```

Capture clock → fast assumption

Even though the actual chip may not experience those exact extremes simultaneously.

This can produce unnecessary pessimism.

---

# 21. CPPR ⭐⭐⭐⭐⭐

To reduce unnecessary clock pessimism, STA uses:

**CPPR**

**CPPR = Common Path Pessimism Removal**

---

# 22. What is Common Path?

Consider:

```text id="k8m3p1"
             Common Clock Path
```

```
                │

          ┌─────┴─────┐

          ↓           ↓

      Launch       Capture

       Clock         Clock

          ↓           ↓

         FF1         FF2
```

````

Part of the clock path is common to both launch and capture clocks.

---

# 23. Why Does Pessimism Occur?

Suppose the common clock path is assumed:

```text id="f6r2v8"
Slow for one side
````

Fast for another side

during worst-case analysis.

But the common physical path cannot simultaneously have completely independent characteristics in the same real condition.

Therefore, STA can remove this unnecessary pessimism.

**CPPR reduces common-path pessimism**

---

# 24. 🔥 Placement Definition

> **CPPR removes excessive pessimism caused by applying different clock delays to a common portion of the launch and capture clock paths.**

---

# 25. Simple CPPR Diagram

```text id="q7m4n2"
                    Clock
```

```
                  │

                  ▼

             Common Path

                  │

          ┌───────┴───────┐

          ↓               ↓

      Launch Path      Capture Path

          ↓               ↓

         FF1             FF2
```

The shared portion is the:

**Common clock path**

CPPR compensates for pessimism associated with that shared portion.

---

# 26. 🔥 Frequently Asked Questions

### Q1. What does OCV stand for?

**On-Chip Variation**

---

### Q2. Why is OCV needed?

To account for variations in timing between different parts of the same chip.

---

### Q3. What is timing derating?

Applying factors to nominal timing values to account for variations and uncertainty.

---

### Q4. What does a late derate do?

Generally makes the delay larger.

**Late → Slower**

---

### Q5. What does an early derate do?

Generally makes the delay smaller.

**Early → Faster**

---

### Q6. What is AOCV?

**Advanced On-Chip Variation**

---

### Q7. What is POCV?

**Parametric On-Chip Variation**

---

### Q8. What is CPPR?

**Common Path Pessimism Removal**

---

### Q9. Why is CPPR used?

To remove unnecessary pessimism caused by the common portion of launch and capture clock paths.

---

# 27. 🔥 Placement MCQs

### Q1.

OCV stands for:

A. Output Clock Variation
B. On-Chip Variation
C. Operating Circuit Voltage
D. On-Clock Verification

**B**

---

### Q2.

Which is generally associated with late timing?

A. Faster delay
B. Slower delay

**B**

---

### Q3.

Which is generally associated with early timing?

A. Faster delay
B. Slower delay

**A**

---

### Q4.

CPPR is used to:

A. Increase clock frequency
B. Remove common-path pessimism
C. Generate clocks
D. Reduce supply voltage

**B**

---

### Q5.

Which technique is more refined than basic OCV?

A. AOCV
B. CMOS
C. RTL
D. UART

**A**

---

# 🧠 ONE-MINUTE REVISION

```text id="c8m5v1"
══════════════════════════════════════

          OCV & DERATING

══════════════════════════════════════


OCV:

On-Chip Variation


PVT:

Global operating conditions


OCV:

Variation within the chip


DERATING:

Apply factor to nominal delay


LATE:

→ Slower

→ Larger delay


EARLY:

→ Faster

→ Smaller delay


SETUP:

→ Late data is bad

→ Slow path is bad


HOLD:

→ Early data is bad

→ Fast path is bad


AOCV:

Advanced On-Chip Variation


POCV:

Parametric On-Chip Variation


CPPR:

Common Path Pessimism Removal


CPPR:

→ Removes unnecessary pessimism

  from common clock path
```

---

# 🔥 Final Memory Map

**PVT → Overall operating conditions**

**OCV → Variation within chip**

**Derating → Modify nominal delay**

**Late → Slow**

**Early → Fast**

**AOCV → Advanced OCV**

**POCV → Parametric OCV**

**CPPR → Remove common-path pessimism**
