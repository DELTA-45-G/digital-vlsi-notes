# STATIC TIMING ANALYSIS (STA) — BASICS ⭐⭐⭐⭐⭐

This is another **very important VLSI placement topic**. STA is especially relevant for interviews at companies working with digital IC/VLSI design.

---

# 1. What is Static Timing Analysis?

**Static Timing Analysis (STA)** is a method used to verify whether a digital design satisfies its timing requirements **without applying functional input vectors**.

### Placement definition ⭐

> **STA analyzes all relevant timing paths in a digital circuit and checks whether timing constraints such as setup and hold are satisfied.**

---

# 2. Why is STA Needed?

A circuit may be logically correct but still fail at high frequency.

Example:

```text id="j8k4m2"
RTL Simulation
```

```
  ↓
```

Functionally correct ✅

```
  ↓
```

STA

```
  ↓
```

Setup violation ❌

STA checks whether signals arrive within the required time.

---

# 3. STA vs Simulation ⭐⭐⭐⭐⭐

This is frequently asked.

### Simulation

Uses:

* Input test vectors
* Clock signals
* Functional scenarios

It checks:

**Functional behavior**

### STA

Does not need functional input vectors.

It checks:

**Timing behavior**

### Memory:

**Simulation → Function**

**STA → Timing**

---

# 4. What Does STA Check?

STA commonly checks:

### Setup timing

**Data arrives before required capture edge**

### Hold timing

**Data remains stable after capture edge**

It can also consider:

* Clock skew
* Clock latency
* Clock uncertainty
* Propagation delays
* Cell delays
* Interconnect delays

---

# 5. Timing Paths ⭐⭐⭐⭐⭐

STA analyzes timing paths through the design.

A basic register-to-register path:

```text id="8n3v6q"
FF1
```

│

│ Launch

▼

Combinational Logic

│

▼

FF2

│

│ Capture

▼

STA determines:

* When data launches
* How long data takes to propagate
* When data must arrive
* Whether timing is satisfied

---

# 6. Four Common Timing Path Types

This is important for VLSI interviews.

### 1. Register → Register

```text id="r4m7x1"
FF → Logic → FF
```

### 2. Input → Register

```text id="q9c2n5"
Input → Logic → FF
```

### 3. Register → Output

```text id="v6p3k8"
FF → Logic → Output
```

### 4. Input → Output

```text id="m1x8r4"
Input → Logic → Output
```

These are timing paths that STA can analyze depending on the design and constraints.

---

# 7. Launch and Capture ⭐⭐⭐⭐⭐

For a register-to-register path:

```text id="w5n2q7"
         Launch                Capture
```

```
       ↓                     ↓
```

Clock ────↑─────────────────────↑────

```
       FF1                  FF2

        │                    │

        └── Logic ───────────┘
```

````

### Launch flip-flop

FF1 launches the data.

### Capture flip-flop

FF2 captures the data.

Therefore:

**FF1 = Launch**

**FF2 = Capture**

---

# 8. Arrival Time ⭐⭐⭐⭐⭐

**Arrival time** is the time at which data actually reaches the endpoint.

Example:

```text id="k7m3p9"
Data arrives at FF2 = 8 ns
````

Therefore:

**Arrival Time=8ns**

---

# 9. Required Time

**Required time** is the latest time at which data is allowed to arrive while still satisfying the timing requirement.

Example:

```text id="x2v8c4"
Required arrival = 10 ns
```

Actual arrival   = 8 ns

The data arrives early enough.

---

# 10. Slack ⭐⭐⭐⭐⭐

The basic idea:

**Slack=Required Time−Arrival Time**

Example:

**Required=10ns**

**Arrival=8ns**

Therefore:

**Slack=10−8**

**+2ns**

Timing passes.

---

# 11. Negative Slack

Suppose:

**Required=8ns**

**Arrival=10ns**

Then:

**Slack=8−10**

**−2ns**

Therefore:

**Timing violation**

---

# 12. Setup Slack

For setup analysis:

```text id="p5n8m3"
Required arrival time
```

```
      │

      ▼

   Compare

      ▲

      │
```

Actual arrival time

If:

**Arrival≤Required**

then:

**Setup passes**

If:

**Arrival>Required**

then:

**Setup violation**

---

# 13. Hold Slack

For hold, the idea is slightly different.

The new data must **not arrive too early**.

Simplified:

**Slackhold=Arrivaldata−Requiredhold**

Positive:

**Hold passes**

Negative:

**Hold violation**

---

# 14. 🔥 Important: STA Does Not Apply Test Vectors

A common interview question:

### Q.

Does STA require millions of input test vectors?

No

STA analyzes timing paths mathematically using:

* Cell timing information
* Interconnect delays
* Clock definitions
* Timing constraints

Therefore:

**STA is vectorless**

at the conceptual placement level.

---

# 15. Timing Libraries

STA needs timing information about standard cells.

For example:

```text id="e1m4q8"
AND gate
```

──────────────

Input → Output delay

Setup

Hold

Transition

etc.

This information typically comes from **standard-cell timing libraries**.

A common format is:

**.lib**

---

# 16. What is a .lib File?

A Liberty `.lib` file contains timing and power information for cells.

For example:

```text id="z7c2p5"
AND2
```

├── Cell delay

├── Output transition

├── Setup

├── Hold

└── Other timing information

For placement preparation, remember:

**.lib → Cell timing information**

---

# 17. SDC — Timing Constraints ⭐⭐⭐⭐⭐

STA needs to know the timing requirements of the design.

These are commonly specified using:

**SDC = Synopsys Design Constraints**

Typical constraints include:

* Clock definitions
* Input delays
* Output delays
* Timing exceptions

---

# 18. create_clock

A common SDC command is:

```text id="c6m9r2"
create_clock
```

It defines the clock.

Conceptually:

```text id="n3x8v4"
Clock period = 10 ns
```

This means:

**f=1/10ns**

**100MHz**

---

# 19. Input and Output Delays

STA also needs to know when external signals are expected to arrive or be required.

For example:

```text id="k4p2m8"
External Source
```

```
  ↓
```

Input Port

```
  ↓

Logic

  ↓

 FF
```

The input delay tells STA about the timing relationship between the external source and the design.

Similarly, output delay specifies requirements at the output interface.

---

# 20. Timing Exceptions ⭐⭐⭐⭐

Sometimes certain paths should not be analyzed using normal timing assumptions.

Common timing exceptions include:

### False Path

A path that does not need timing analysis for the specified relationship.

### Multicycle Path

A path that is intentionally allowed more than one clock cycle.

For placements, remember:

**False Path**

and

**Multicycle Path**

are important STA concepts.

---

# 21. False Path ⭐⭐⭐⭐⭐

A false path is a path that is not functionally required to meet normal timing between the specified endpoints.

Example concept:

```text id="h6n3q9"
FF1 ─────────► FF2
```

│              │

│  Functionally

│  never active

▼              ▼

If the path is genuinely impossible during operation, it can be constrained as a false path.

### Important:

Do **not** use false-path constraints simply to hide a timing violation.

---

# 22. Multicycle Path ⭐⭐⭐⭐⭐

Normally:

```text id="q2m7v5"
FF1 → Logic → FF2
```

Allowed = 1 clock cycle

A multicycle path intentionally allows:

```text id="x8p4n1"
FF1 → Long Logic → FF2
```

Allowed = multiple clock cycles

For example:

**2-cycle path**

means the path is intentionally given two clock periods.

---

# 23. Why Are Timing Constraints Important?

Without correct constraints:

```text id="m5c9r2"
STA
```

↓

Incorrect assumptions

↓

Incorrect timing results

Therefore:

**Good STA requires correct timing constraints**

---

# 24. Setup Timing in STA

STA conceptually calculates:

```text id="p7x3n8"
Launch
```

↓

Clock-to-Q

↓

Combinational delay

↓

Arrival time

↓

Compare with required time

↓

Setup PASS / FAIL

---

# 25. Hold Timing in STA

```text id="v1m6q4"
Launch
```

↓

Minimum clock-to-Q

↓

Minimum combinational delay

↓

Arrival time

↓

Compare with hold requirement

↓

Hold PASS / FAIL

---

# 26. Worst Negative Slack — WNS ⭐⭐⭐⭐⭐

You may see:

**WNS**

which means:

> **Worst Negative Slack**

It indicates the worst setup/hold slack among the analyzed paths, depending on the report/context.

If:

**WNS=−0.5ns**

there is a worst timing violation of:

**0.5ns**

---

# 27. Total Negative Slack — TNS ⭐⭐⭐⭐⭐

**TNS=Total Negative Slack**

It represents the aggregate negative slack across violating paths in the relevant timing analysis.

Example:

```text id="u4n8k2"
Path 1 = -1 ns
```

Path 2 = -2 ns

Path 3 = -0.5 ns

Then conceptually:

**TNS=−1−2−0.5**

**−3.5ns**

---

# 28. WNS vs TNS

| Metric | Meaning                                |
| ------ | -------------------------------------- |
| WNS    | Worst individual negative slack        |
| TNS    | Total negative slack across violations |

Memory:

**WNS→Worst**

**TNS→Total**

---

# 29. 🔥 Placement Question

### Q.

If WNS = `-2 ns`, what does it indicate?

**At least one analyzed timing path violates timing by 2 ns**

---

# 30. 🔥 Another Question

### Q.

If WNS = `0 ns` and there are no other negative-slack paths:

**Timing meets the requirement**

---

# 31. STA Flow

A simplified flow:

```text id="s2m7x5"
RTL
```

↓

Synthesis

↓

Gate-Level Netlist

↓

Standard Cell Libraries (.lib)

↓

Timing Constraints (SDC)

↓

STA

↓

Timing Reports

↓

Find Violations

↓

Optimize

↓

STA Again

---

# 32. STA vs Timing Simulation

### STA

```text
Vectorless
```

Timing paths

Mathematical analysis

Fast for large designs

### Timing Simulation

```text
Uses simulation vectors
```

Models actual simulated behavior

Can observe waveform timing

For large digital designs, STA is essential because exhaustive simulation cannot realistically cover every possible timing path and operating condition.

---

# 33. 🔥 Placement Quick Questions

### Q1.

What does STA stand for?

**Static Timing Analysis**

### Q2.

Does STA require functional input vectors?

No

### Q3.

What does STA primarily verify?

**Timing constraints**

### Q4.

What is `.lib`?

**Standard-cell timing/power library format**

### Q5.

What is SDC?

**Synopsys Design Constraints**

### Q6.

What is a false path?

**A path excluded from normal timing analysis because it is not functionally required for that timing relationship**

### Q7.

What is a multicycle path?

**A path intentionally allowed multiple clock cycles**

### Q8.

What is WNS?

**Worst Negative Slack**

### Q9.

What is TNS?

**Total Negative Slack**

### Q10.

What does negative slack indicate?

**Timing violation**

---

# 🧠 ONE-MINUTE STA REVISION

```text id="l4p8n2"
══════════════════════════════════════

       STATIC TIMING ANALYSIS

══════════════════════════════════════


STA:

→ Checks timing without functional vectors


Main checks:

→ Setup

→ Hold


Timing path:

→ Launch → Logic → Capture


Arrival Time:

→ When data actually arrives


Required Time:

→ Latest/earliest acceptable timing

  depending on the check


Slack:

→ Required vs Arrival


Positive slack → PASS

Negative slack → FAIL


.lib:

→ Cell timing information


SDC:

→ Timing constraints


False Path:

→ Excluded timing path


Multicycle Path:

→ More than one clock cycle allowed


WNS:

→ Worst Negative Slack


TNS:

→ Total Negative Slack
```

---

# 🔥 Memory Tricks

**STA → Timing, not Function**

**.lib → Cell information**

**SDC → Timing constraints**

**WNS → Worst**

**TNS → Total**

**False Path → Don’t analyze normally**

**Multicycle → More cycles allowed**
