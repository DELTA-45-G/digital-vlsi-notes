# COMPLETE QUICK REVISION NOTES

## Timing & Digital Design Concepts ⭐⭐⭐⭐⭐

---

## 8.1 — Propagation Delay

**Propagation delay** is the time taken for a change at the input of a circuit to produce a corresponding valid change at the output.

tpd = Time taken for input change to affect output

### Remember

* Smaller propagation delay → faster circuit
* Important for **maximum operating frequency**
* Affects **setup timing**

---

## 8.2 — Contamination Delay

**Contamination delay** is the minimum time after an input change before the output can begin to change.

tcd = Minimum delay before output can start changing

### Remember

* Related strongly to **hold timing**
* tcd is generally less than or equal to tpd

---

## 8.3 — Propagation vs Contamination Delay

| Propagation Delay                          | Contamination Delay               |
| ------------------------------------------ | --------------------------------- |
| Maximum/valid output response delay        | Minimum output-change delay       |
| Important for setup                        | Important for hold                |
| Determines how long output takes to settle | Determines earliest output change |
| tpd                                        | tcd                               |

### Memory

tpd → Setup
tcd → Hold

---

# 8.4 — Setup Time

**Setup time** is the minimum time for which data must be stable **before the active clock edge**.

```text
DATA ────────────────
```

```
          │

          │ Setup

          │
```

CLOCK ────────↑──────

If data arrives too late:

Setup violation

### Setup violation → Data is too late.

---

# 8.5 — Hold Time

**Hold time** is the minimum time for which data must remain stable **after the active clock edge**.

```text
CLOCK ─────────↑──────
```

```
          │

          │ Hold

          │
```

DATA ────────────────

If data changes too early:

Hold violation

### Hold violation → Data changes too early.

---

# 8.6 — Setup Time vs Hold Time ⭐⭐⭐⭐⭐

| Setup                             | Hold                               |
| --------------------------------- | ---------------------------------- |
| Before clock edge                 | After clock edge                   |
| Data arrives too late → violation | Data changes too early → violation |
| Related to maximum delay          | Related to minimum delay           |
| Speed up path to improve          | Slow down path to improve          |

### Memory

Setup → Before
Hold → After

---

# 8.7 — Clock-to-Q Delay

**Clock-to-Q delay** is the time between the active clock edge and the corresponding change at the flip-flop output Q.

```text
CLK ───────↑────────
```

```
         │

         │ tCQ

         ↓
```

Q   ────────────↑────

tCQ = Clock edge → Q transition

Important in register-to-register timing.

---

# 8.8 — Register-to-Register Timing ⭐⭐⭐⭐⭐

Basic path:

```text
Launch FF
```

↓

Clock-to-Q

↓

Combinational Logic

↓

Routing

↓

Capture FF

Total data-path delay includes:

tCQ + tcomb + troute

### Important factors

* Clock-to-Q delay
* Combinational delay
* Routing delay
* Setup time
* Clock skew
* Clock uncertainty

---

# 8.9 — Clock Skew

**Clock skew** is the difference in clock arrival time between two sequential elements.

Clock Skew = tcapture − tlaunch

Example:

```text
Launch clock = 1.0 ns
```

Capture clock = 1.2 ns

Skew = 0.2 ns

### Remember

Clock skew can affect both:

* Setup timing
* Hold timing

---

# 8.10 — Clock Jitter & Uncertainty

### Clock Jitter

Variation of clock edge position from its ideal position.

```text
Ideal:
```

|    |    |    |

Actual:

|   |     |   |

### Clock Uncertainty

Timing margin reserved for uncertainties such as:

* Jitter
* Clock variation
* Other timing uncertainties

### Memory

Jitter → Clock edge variation
Uncertainty → Timing margin

---

# 8.11 — Metastability ⭐⭐⭐⭐⭐

Metastability occurs when a flip-flop cannot immediately resolve to a valid logic `0` or `1`.

Often caused when setup/hold requirements are violated.

```text
Input
```

↓

Flip-Flop

↓

Metastable state

↓

Uncertain output

### Common situation

Asynchronous signal entering a clock domain

### Important

Metastability cannot be completely eliminated, but its probability can be greatly reduced using synchronizers.

---

# 8.12 — Clock Domain Crossing (CDC)

CDC occurs when a signal moves between different clock domains.

```text
Clock Domain A
```

↓

CDC

↓

Clock Domain B

### Main problem

Different clocks may have different:

* Frequencies
* Phases
* Timing relationships

### Common solution

For a single-bit control signal:

2-FF Synchronizer

---

# 8.13 — Timing Closure & Critical Path

### Timing Closure

Making sure all required timing constraints are satisfied.

### Critical Path

The path that most severely limits timing, typically the path with the worst slack for the relevant timing check.

```text
Timing Analysis
```

↓

Find violation

↓

Optimize

↓

Re-analyze

↓

Timing closure

### Memory

Critical path → Most timing-critical path

---

# 8.14 — Static Timing Analysis (STA) ⭐⭐⭐⭐⭐

STA = **Static Timing Analysis**

It analyzes timing paths and checks whether timing constraints are satisfied without exhaustive functional simulation.

STA checks:

* Setup
* Hold
* Clock relationships
* Input/output timing
* False paths
* Multicycle paths

### Important

STA is one of the most important tools/concepts in VLSI timing analysis.

---

# 8.15 — PVT Corners

PVT:

Process + Voltage + Temperature

### Process

Manufacturing variation.

### Voltage

Supply voltage variation.

### Temperature

Operating temperature variation.

Different PVT conditions produce different delays and timing behavior.

### Memory

PVT = P + V + T

---

# 8.16 — Timing Derating & OCV

### OCV

On-Chip Variation

It accounts for variations that can occur across different parts of the same chip.

### Derating

Applying a factor to account for uncertainty/variation in timing.

Conceptually:

```text
Nominal delay
```

↓

Variation / Derating

↓

More realistic timing

### Why?

Real chips are not perfectly uniform.

---

# 8.17 — Multi-Cycle & False Paths ⭐⭐⭐⭐⭐

## False Path

A path that is not required to meet a normal timing relationship.

Example:

```text
Path exists physically
```

↓

But not functionally exercised

↓

False path

STA can be told to ignore it.

---

## Multi-Cycle Path

A path intentionally allowed to take more than one clock cycle.

Example:

```text
Launch
```

↓

Cycle 1

↓

Cycle 2

↓

Capture

### Memory

False Path → Ignore timing relationship
Multi-Cycle → More than one cycle

---

# 8.18 — CTS & Clock Distribution ⭐⭐⭐⭐⭐

CTS:

Clock Tree Synthesis

CTS distributes the clock from the source to sequential elements.

```text
              Clock
```

```
            │

          Buffer

         /     \

      Buffer   Buffer

      /  \       /  \

     FF  FF     FF  FF
```

### Goals

* Control clock skew
* Control insertion delay
* Maintain clock quality
* Manage clock transition/slew

---

# 8.19 — Clock Gating & Low Power

**Clock gating** disables the clock to inactive blocks.

```text
Clock
```

↓

Clock Gate

↓

Register

When the block is inactive:

Clock switching → OFF

This reduces dynamic power.

### Memory

Clock gating → Dynamic power reduction

---

# 8.20 — PPA

PPA:

Power + Performance + Area

### Power

Energy consumption.

### Performance

Speed/timing.

### Area

Silicon area.

### Important

PPA involves trade-offs.

Example:

```text
Cell upsizing
```

↓

Delay ↓

Performance ↑

But:

Area ↑

Power ↑

---

# 8.21 — IR Drop & Power Integrity ⭐⭐⭐⭐⭐

IR drop:

Vdrop = I × R

It is the voltage drop caused by current flowing through resistance in the power-delivery network.

### Effects

```text
IR Drop
```

↓

VDD ↓

↓

Cell delay ↑

↓

Timing margin ↓

### Reduce IR drop

* Wider power wires
* More power straps
* More vias
* Better power grid
* Reduce localized current demand

---

# 8.22 — Signal Integrity & Crosstalk ⭐⭐⭐⭐⭐

### Signal Integrity

Maintaining acceptable:

* Voltage
* Waveform
* Timing

during signal propagation.

### Crosstalk

Unwanted coupling between nearby wires.

```text
Aggressor
```

────────────

↓

Coupling

↓

Victim

────────────

### Aggressor

Causes interference.

### Victim

Receives interference.

### Crosstalk can cause

* Noise
* Delay variation
* Timing violations

### Reduce crosstalk

* Increase spacing
* Reduce parallel run length
* Shield sensitive signals
* Appropriate buffering/routing

---

# 8.23 — ECO & Timing Closure ⭐⭐⭐⭐⭐

ECO:

Engineering Change Order

A targeted modification to an existing design.

### Common reasons

* Setup violation
* Hold violation
* Functional bug
* Power issue
* Physical issue
* SI issue

### Setup ECO

Generally:

Speed up data path

Examples:

* Upsize cells
* Reduce load
* Optimize logic
* Improve routing

### Hold ECO

Generally:

Slow down data path

Example:

* Add delay buffers

---

# 8.24 — Final Integration ⭐⭐⭐⭐⭐

The complete picture:

```text
                    DIGITAL VLSI
```

```
                     │

      ┌──────────────┼──────────────┐

      ↓              ↓              ↓

    TIMING          POWER          AREA

      │              │              │

      ↓              ↓              ↓

     STA           IR Drop         PPA

      │              │

      ↓              ↓

  Setup/Hold         EM

      │

      ↓

   Critical

     Path

      │

      ↓

   Violations

      │

      ↓

     ECO

      │

      ↓

 Re-run Analysis

      │

      ↓

   SIGNOFF

      │

      ↓

   TAPEOUT
```

---

# 🔥 PHASE 8 — MOST IMPORTANT FORMULAS

### 1. IR Drop

Vdrop = IR

### 2. Current Density

J = I/A

### 3. Slack

Slack = Required − Arrival

### 4. Clock Skew

Skew = tcapture − tlaunch

### 5. Register-to-register data path

tpath ≈ tCQ + tcomb + troute

---

# 🧠 PHASE 8 — TOP 20 MEMORY POINTS

|  # | Remember                                         |
| -: | ------------------------------------------------ |
|  1 | Propagation delay → maximum/valid response delay |
|  2 | Contamination delay → earliest output change     |
|  3 | Propagation delay → setup                        |
|  4 | Contamination delay → hold                       |
|  5 | Setup → data stable before clock                 |
|  6 | Hold → data stable after clock                   |
|  7 | Clock-to-Q → clock edge to Q                     |
|  8 | Clock skew → difference in clock arrival         |
|  9 | Jitter → clock-edge variation                    |
| 10 | Metastability → uncertain FF output              |
| 11 | CDC → signal between clock domains               |
| 12 | STA → static timing analysis                     |
| 13 | PVT → Process, Voltage, Temperature              |
| 14 | OCV → On-Chip Variation                          |
| 15 | CTS → Clock Tree Synthesis                       |
| 16 | Clock gating → dynamic power reduction           |
| 17 | IR drop → IR voltage drop                        |
| 18 | Crosstalk → coupling between nearby wires        |
| 19 | ECO → Engineering Change Order                   |
| 20 | Signoff → final verification before tapeout      |

---

# 🎯 PHASE 8 — PLACEMENT RAPID-FIRE

If an interviewer asks:

**"Setup violation?"**

→ Data arrives too late.

**"Hold violation?"**

→ Data changes too early.

**"How to fix setup?"**

→ Generally speed up data path.

**"How to fix hold?"**

→ Generally add delay to data path.

**"What is critical path?"**

→ Most timing-critical path / worst-slack path.

**"What is STA?"**

→ Static Timing Analysis.

**"What is PVT?"**

→ Process, Voltage, Temperature.

**"What is CTS?"**

→ Clock Tree Synthesis.

**"What is IR drop?"**

→ V=IR voltage drop in the power network.

**"What is crosstalk?"**

→ Coupling between nearby interconnects.

**"What is ECO?"**

→ Engineering Change Order.

**"What is PPA?"**

→ Power, Performance, Area.

**"What is signoff?"**

→ Final verification before tapeout.
