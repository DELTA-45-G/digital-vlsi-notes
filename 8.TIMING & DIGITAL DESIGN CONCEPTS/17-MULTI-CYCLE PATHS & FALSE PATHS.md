# &#x20;MULTI-CYCLE PATHS & FALSE PATHS ⭐⭐⭐⭐⭐

This topic is very important because it connects **STA, timing constraints, setup/hold, and real VLSI design**.

---

# 1. Why Do We Need Timing Exceptions?

Normally, STA assumes that a register-to-register path must transfer data within **one clock cycle**.

Example:

```text id="c5m8v2"
Clock 1                    Clock 2
```

↓                          ↓

FF1 ─── Combinational ────> FF2

Normally:

**1 clock cycle available**

But sometimes the design intentionally behaves differently.

Two important timing exceptions are:

1. **False Path**
2. **Multi-Cycle Path**

---

# 2. False Path ⭐⭐⭐⭐⭐

A **false path** is a path that is **not functionally required to meet the normal timing relationship**.

In simple terms:

> The path exists physically, but it is not a valid functional path for the timing scenario being analyzed.

Therefore, STA can exclude that path from normal timing analysis.

---

# 3. Example of a False Path

Suppose:

```text id="q7n3m1"
        ┌───────────────┐
```

```
    │               │
```

FF1 ───> Logic ───────> FF2

```
    │               │

    └───────────────┘
```

If FF1 and FF2 are controlled such that this path can **never actually be active**, then timing analysis of that path may not be meaningful.

It can be constrained as a false path.

---

# 4. Important Warning ⚠️

A false path should **not** be used just because a path has a timing violation.

Wrong approach:

```text id="r8m4q2"
Timing violation
```

```
  ↓
```

Mark path as false

```
  ↓
```

Violation disappears ❌

Correct approach:

```text id="v2p7x5"
Determine actual functionality
```

```
  ↓
```

Path is genuinely impossible

```
  ↓
```

Apply false-path constraint

---

# 5. False Path Memory Trick

**False Path = Physically exists, functionally irrelevant**

---

# 6. Multi-Cycle Path ⭐⭐⭐⭐⭐

A **multi-cycle path** is a path that is intentionally allowed to take **more than one clock cycle**.

Normally:

**1 cycle**

Multi-cycle:

**2 or more cycles**

---

# 7. Normal Single-Cycle Path

Example:

```text id="m6q2v9"
Clock 1                  Clock 2
```

↓                        ↓

FF1 ─── Logic ──────────> FF2

The data must reach FF2 within one cycle.

If:

**TCLK=10ns**

then approximately:

**10ns**

is available for the path, subject to clock-to-Q, setup, skew, uncertainty, etc.

---

# 8. Two-Cycle Path

Suppose the design intentionally allows two cycles:

```text id="p4n8x1"
Clock 1        Clock 2        Clock 3
```

↓              ↓              ↓

FF1 ───────── Logic ─────────> FF2

Now the path can use approximately:

**2TCLK**

for the intended multi-cycle relationship, subject to the exact constraints.

If:

**TCLK=10ns**

then:

**2TCLK=20ns**

---

# 9. Why Use Multi-Cycle Paths?

Some operations naturally require more than one clock cycle.

For example:

```text id="k3m7v5"
FF
```

↓

Complex combinational logic

↓

FF

If the architecture intentionally allows the calculation to complete over two cycles, treating it as a one-cycle path would create a false timing requirement.

Therefore:

**Multi-cycle constraint = Tell STA more cycles are allowed**

---

# 10. False Path vs Multi-Cycle Path ⭐⭐⭐⭐⭐

| Feature                 | False Path                     | Multi-Cycle Path      |
| ----------------------- | ------------------------------ | --------------------- |
| Path physically exists? | Yes                            | Yes                   |
| Functionally used?      | Not for specified relationship | Yes                   |
| Timing analyzed?        | Excluded                       | Yes                   |
| Number of cycles        | Not applicable                 | 2 or more             |
| Purpose                 | Remove irrelevant path         | Allow additional time |

### Memory:

**False → Don’t analyze**

**Multi-cycle → Analyze, but allow more cycles**

---

# 11. 🔥 Very Important Difference

Suppose a path takes:

**15ns**

and clock period is:

**10ns**

### Case 1: Normal path

Allowed:

**10ns**

Actual:

**15ns**

Therefore:

**Setup violation**

---

### Case 2: Legitimate 2-cycle path

Allowed:

**20ns**

Actual:

**15ns**

Therefore:

**Timing can pass**

---

# 12. Multi-Cycle Path and Setup

This is where things become important.

Suppose:

**TCLK=10ns**

and a path is allowed **2 cycles**.

The setup requirement is extended.

Simplified:

**Required Time≈2TCLK**

Therefore:

**2×10=20ns**

---

# 13. Multi-Cycle Path and Hold ⚠️

This is a commonly missed interview point.

Changing the setup relationship for a multi-cycle path does **not automatically mean the hold relationship should be ignored**.

The hold relationship must also be constrained appropriately.

For example, if a path is made a 2-cycle setup path, the corresponding hold relationship often needs an explicit multi-cycle hold adjustment.

### Placement-level memory:

**Multi-cycle setup and hold constraints are related**

---

# 14. Why is This Important?

Suppose you only tell STA:

```text id="z6m2p8"
Allow 2 cycles for setup
```

but don't properly specify the corresponding hold relationship.

You can end up with an incorrect timing analysis.

Therefore:

> **A multi-cycle path must be constrained carefully for both setup and hold.**

---

# 15. False Path and CDC ⭐⭐⭐⭐⭐

False paths are frequently relevant to **Clock Domain Crossing (CDC)**.

Example:

```text id="q1m6v3"
Clock A domain
```

```
 │

 ▼
```

FF A

```
 │

 ▼
```

Synchronizer

```
 │

 ▼
```

FF B

```
 │
```

Clock B domain

Signals crossing unrelated clock domains cannot always be analyzed using ordinary synchronous timing assumptions.

Depending on the architecture and constraints, certain CDC paths may be excluded from conventional timing analysis while being checked separately using CDC methodology.

---

# 16. Asynchronous Signals

Example:

```text id="x8p4n2"
Clock A
```

│

▼

Domain A

│

│

▼

Domain B

│

▼

Clock B

If the clocks are asynchronous/unrelated, there is no fixed phase relationship.

Therefore:

**Normal synchronous timing assumptions may not apply**

---

# 17. Timing Exception Types

The most important timing exceptions for placement interviews:

### 1. False Path

**Exclude path from timing analysis**

### 2. Multi-Cycle Path

**Allow multiple clock cycles**

You may also encounter:

### 3. Max Delay

Places a maximum delay requirement.

### 4. Min Delay

Places a minimum delay requirement.

For your placement preparation, the first two are the most important.

---

# 18. SDC Commands ⭐⭐⭐⭐⭐

Timing exceptions are commonly specified using SDC commands.

### False path

```text id="d4m8q1"
set_false_path
```

### Multi-cycle path

```text id="v7n2x5"
set_multicycle_path
```

These are very common interview keywords.

---

# 19. Example: False Path Constraint

Conceptually:

```text id="n5m3q8"
set_false_path -from A -to B
```

Meaning:

> Do not perform normal timing analysis from A to B.

You don't need to memorize every option for basic placement interviews.

Remember:

**set_false_path**

---

# 20. Example: Multi-Cycle Constraint

Conceptually:

```text id="k2v6p4"
set_multicycle_path 2
```

This indicates a two-cycle timing relationship, with the exact `-from`, `-to`, setup/hold details specified according to the design.

For placements, remember:

**set_multicycle_path**

---

# 21. False Path vs Slow Path ⚠️

Suppose a path has:

```text id="m7x3q9"
WNS = -2ns
```

You cannot simply declare it false.

Ask:

> Is this path genuinely functionally impossible?

If:

**No**

→ Fix the timing violation.

If:

**Yes**

→ A false-path constraint may be appropriate.

---

# 22. Multi-Cycle Path vs Timing Violation

Suppose:

```text id="y4m8v2"
Clock = 10 ns
```

Path delay = 15 ns

Normal path:

**15>10**

**Violation**

But if architecture intentionally allows 2 cycles:

**15<20**

then:

**Can meet timing**

---

# 23. 🔥 Interview Question

### Q.

What is the difference between a false path and a multi-cycle path?

### Answer:

> A false path is a path that is not functionally required to meet the specified timing relationship and can therefore be excluded from timing analysis. A multi-cycle path is a valid functional path that is intentionally allowed more than one clock cycle to complete.

---

# 24. 🔥 Interview Question

### Q.

Why are timing exceptions necessary?

### Answer:

> Because the default STA assumptions may not correctly represent the functional behavior of every path. Timing exceptions allow the timing analysis to reflect actual design intent.

---

# 25. 🔥 Interview Question

### Q.

What happens if an invalid false-path constraint is applied?

### Answer:

It can hide a real timing violation and potentially cause a silicon failure.

Therefore:

**Timing constraints must reflect actual design intent**

---

# 26. 🔥 Interview Question

### Q.

Can a false path still physically exist?

Yes

It may physically exist in the netlist but not be functionally relevant for the specified timing relationship.

---

# 27. 🔥 Interview Question

### Q.

Does a multi-cycle path mean the path is unused?

No

It is a **valid functional path**.

It is simply allowed more than one clock cycle.

---

# 28. 🔥 MCQ

A path has a delay of `18 ns`. Clock period is `10 ns`. The path is intentionally designed as a 2-cycle path. What is the basic timing conclusion?

A. Automatically false path
B. Timing can satisfy the 2-cycle requirement
C. Always a hold violation
D. Path must be removed

**B**

---

# 29. 🔥 MCQ

Which command is associated with false-path constraints?

A. `set_clock`
B. `set_false_path`
C. `set_delay`
D. `set_path_false`

**B**

---

# 30. 🔥 MCQ

Which command is associated with multi-cycle paths?

A. `set_multicycle_path`
B. `set_multiple_clock`
C. `set_cycle_path`
D. `set_multi_delay`

**A**

---

# 🧠 ONE-MINUTE REVISION

```text id="x7m2q5"
══════════════════════════════════════

     TIMING EXCEPTIONS

══════════════════════════════════════


FALSE PATH

→ Physically exists

→ Functionally irrelevant for

  specified timing relationship

→ Excluded from normal STA


Command:

set_false_path


MULTI-CYCLE PATH

→ Valid functional path

→ Allowed >1 clock cycle


Command:

set_multicycle_path


MEMORY:

FALSE

→ Don't analyze normally


MULTI-CYCLE

→ Analyze

→ Give more cycles


IMPORTANT:

Don't use false path to hide

real timing violations.


Multi-cycle constraints must be

handled correctly for setup AND hold.
```
