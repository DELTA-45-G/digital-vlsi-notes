# FSM QUICK REVISION SHEET ⭐⭐⭐⭐⭐

This is your **last-minute placement revision sheet** for Phase 7.

---

# 1. FSM FUNDAMENTALS

### FSM = Finite State Machine

A sequential digital system that has:

* Finite number of states
* Inputs
* Outputs
* State transitions
* Memory

### Core idea

**Present State + Input → Next State + Output**

---

# 2. FSM BLOCK DIAGRAM

```text id="f5x1m8"
                 ┌─────────────────┐
Input ──────────►│ Combinational   │
                 │ Next-State Logic│
                 └────────┬────────┘
                          │
                          ▼
                    ┌───────────┐
              ┌────►│ Flip-Flops│
              │     └─────┬─────┘
              │           │
              │           ▼
              │      Present State
              │
              └────────────────────
```

The flip-flops store the **current state**.

---

# 3. MOORE vs MEALY ⭐⭐⭐⭐⭐

| Feature                | Moore                      | Mealy                   |
| ---------------------- | -------------------------- | ----------------------- |
| Output depends on      | State                      | State + Input           |
| Equation               | Y=f(Q)                     | Y=f(Q,X)                |
| Output associated with | State                      | Transition              |
| States                 | Generally more             | Generally fewer         |
| Response               | Generally one state change | Can respond immediately |
| Glitch sensitivity     | Lower                      | Higher                  |

### 🔥 Memory Trick

**Moore → State**

**Mealy → State + Input**

---

# 4. STATE DIAGRAM ⭐⭐⭐⭐⭐

A state diagram represents FSM behavior graphically.

### Moore:

```text id="w2m7q4"
S0 / 0
```

State is usually represented as:

```text id="p8c3n6"
State / Output
```

### Mealy:

```text id="y4r9k1"
S0 ── Input / Output ──► S1
```

Example:

```text id="m6v2x8"
S0 ──1/0──► S1
```

means:

```text
Input = 1
```

Output = 0

Next state = S1

---

# 5. STATE TABLE

A state table contains:

| Present State | Input | Next State | Output |
| ------------- | ----- | ---------- | ------ |
| S0            | 0     | S1         | 0      |
| S0            | 1     | S0         | 0      |
| S1            | 0     | S1         | 1      |
| S1            | 1     | S0         | 0      |

### Core relationship:

**PS+Input→NS+Output**

---

# 6. STATE TRANSITION

A transition describes movement:

```text id="q3k8p5"
Current State + Input → Next State
```

Example:

```text id="r7m2v9"
S0 + 1 → S1
```

Means:

> When the FSM is in S0 and input is 1, it moves to S1.

---

# 7. SELF-LOOP

When a state transitions back to itself:

```text id="c5n1x7"
      ┌───────┐
      │       ▼
     S0 ──────┘
```

Example:

**S0 0 S0**

This is called a:

**Self-loop**

---

# 8. STATE ASSIGNMENT ⭐⭐⭐⭐⭐

Converts symbolic states into binary codes.

Example:

```text id="k4p9m6"
S0 → 00
```

S1 → 01

S2 → 10

S3 → 11

### Number of binary FFs:

**n=⌈log₂N⌉**

where N = number of states.

---

# 9. QUICK FLIP-FLOP VALUES

| States | Binary FFs |
| -----: | ---------: |
|      2 |          1 |
|    3–4 |          2 |
|    5–8 |          3 |
|   9–16 |          4 |
|  17–32 |          5 |
|  33–64 |          6 |

### 🔥 Remember:

**2ⁿ≥N**

---

# 10. ONE-HOT ENCODING ⭐⭐⭐⭐⭐

For N states:

**N flip-flops**

Example:

```text id="j7q2v8"
S0 → 0001
```

S1 → 0010

S2 → 0100

S3 → 1000

### Advantages:

* Simple decoding
* Potentially simpler next-state logic
* Commonly useful in FPGA implementations

### Disadvantage:

**Requires more flip-flops**

---

# 11. GRAY STATE ENCODING

Adjacent states differ by only **one bit**.

Example:

```text id="x9m3k5"
00 → 01 → 11 → 10
```

### Main advantage:

Can reduce switching activity in suitable designs.

**Adjacent states → 1-bit change**

---

# 12. STATE MINIMIZATION ⭐⭐⭐⭐⭐

State minimization means:

> Removing equivalent states without changing external behavior.

### Equivalent states:

States with identical observable behavior for all possible input sequences.

### Moore:

Same:

* Output
* Equivalent next-state behavior

### Mealy:

Same:

* Transition outputs
* Equivalent next-state behavior

---

# 13. PARTITION METHOD

For Moore FSM:

### Step 1

Group states according to outputs.

```text id="f1v6q3"
Output 0 → Group A
```

Output 1 → Group B

### Step 2

Check where transitions go.

### Step 3

Split groups if their transition behavior differs.

### Step 4

Repeat until no more splitting is required.

---

# 14. STATE REDUCTION vs STATE ASSIGNMENT

| State Reduction           | State Assignment          |
| ------------------------- | ------------------------- |
| Removes equivalent states | Gives binary codes        |
| Reduces state count       | Represents states         |
| Simplifies FSM            | Enables hardware encoding |

### Memory trick:

**Reduction → Remove**

**Assignment → Encode**

---

# 15. SEQUENCE DETECTOR ⭐⭐⭐⭐⭐

A sequence detector detects a specific pattern in an input stream.

Example:

```text id="n5r8m2"
Pattern = 101
```

Input:

```text id="w4p1x7"
1 0 1
```

Output becomes:

```text id="q6c3k9"
0 0 1
```

A sequence detector is generally implemented using:

**FSM**

because previous inputs must be remembered.

---

# 16. SEQUENCE DETECTOR STATES

For `101`:

```text id="z8m2v5"
S0 → Nothing matched
```

S1 → 1 matched

S2 → 10 matched

Then the next `1` completes:

```text id="r3q7n1"
101
```

For a straightforward Moore design:

```text id="k5x9p4"
S3 → 101 detected
```

---

# 17. OVERLAPPING DETECTION ⭐⭐⭐⭐⭐

Pattern:

```text id="v2m6q8"
101
```

Input:

```text id="n7c3r1"
10101
```

Occurrences:

```text id="p4x8k5"
10101
```

^^^

^^^

Therefore:

**2 overlapping detections**

The matched suffix can be reused for the next sequence.

---

# 18. NON-OVERLAPPING DETECTION

Pattern:

```text id="m9q2v6"
101
```

Input:

```text id="c5r8n3"
10101
```

First occurrence:

```text id="x7p1k4"
101
```

Remaining:

```text id="z3m6q8"
01
```

Therefore:

**1 non-overlapping detection**

### Memory trick:

```text id="y5n2r7"
Overlapping
```

→ Reuse bits

Non-overlapping

→ Don't reuse detected sequence

---

# 19. FSM DESIGN FLOW ⭐⭐⭐⭐⭐

Memorize this order:

```text id="w1k4m8"
Specification
```

```
  ↓
```

Identify Inputs / Outputs

```
  ↓
```

Define States

```
  ↓
```

State Diagram

```
  ↓
```

State Table

```
  ↓
```

State Assignment

```
  ↓
```

Choose Flip-Flop

```
  ↓
```

Excitation Table

```
  ↓
```

Boolean Equations

```
  ↓
```

Simplification

```
  ↓
```

Circuit

---

# 20. D FLIP-FLOP IN FSM

For a D flip-flop:

**D=Qnext**

Example:

```text id="c9v2p6"
Q = 0
```

Qnext = 1

Therefore:

**D=1**

---

# 21. T FLIP-FLOP IN FSM

**T=Q⊕Qnext**

| Q | Qnext | T |
| - | ----- | - |
| 0 | 0     | 0 |
| 0 | 1     | 1 |
| 1 | 0     | 1 |
| 1 | 1     | 0 |

### Memory:

```text id="r4m7x2"
Same state → T = 0
```

Change state → T = 1

---

# 22. NUMBER OF STATE-TABLE ROWS

If:

* Number of states = N
* Number of input bits = m

Then:

**N×2ᵐ**

possible state/input combinations.

### Example:

4 states, 2 inputs:

**4×2²=16**

---

# 23. UNUSED STATES ⭐⭐⭐⭐

If n flip-flops are used:

**2ⁿ**

possible binary states exist.

If only N states are used:

**2ⁿ−N**

unused states.

### Example:

5 states using 3 FFs:

**2³−5=8−5=3**

**3 unused states**

---

# 24. 🔥 MOST IMPORTANT PLACEMENT FORMULAS

### Binary state encoding:

**FF=⌈log₂N⌉**

### One-hot:

**FF=N**

### Available states:

**2ⁿ**

### Unused states:

**2ⁿ−N**

### State-table combinations:

**N×2ᵐ**

### D FF:

**D=Qnext**

### T FF:

**T=Q⊕Qnext**

---

# 🚨 TOP 15 QUESTIONS TO REMEMBER

### 1. What is FSM?

A sequential system with finite states whose behavior depends on present state and inputs.

### 2. Moore output?

**Y=f(Q)**

### 3. Mealy output?

**Y=f(Q,X)**

### 4. Which generally has fewer states?

**Mealy**

### 5. Which is generally more glitch-sensitive?

**Mealy**

### 6. Binary FFs for N states?

**⌈log₂N⌉**

### 7. One-hot FFs for N states?

**N**

### 8. Gray-code property?

**Adjacent states differ by one bit**

### 9. What is state minimization?

**Removing equivalent states**

### 10. What is state assignment?

**Assigning binary codes to states**

### 11. What is a sequence detector?

**FSM that detects a specified input pattern**

### 12. Overlapping detection?

**Previously matched bits can be reused**

### 13. Non-overlapping detection?

**Detected sequence isn’t reused**

### 14. D FF equation?

**D=Qnext**

### 15. T FF equation?

**T=Q⊕Qnext**

---

# 🧠 30-SECOND PHASE 7 REVISION

```text id="k6v1m9"
FSM
```

│

├── Moore

│     └── Output = State

│

├── Mealy

│     └── Output = State + Input

│

├── State Diagram

│

├── State Table

│

├── State Assignment

│     ├── Binary

│     ├── One-Hot

│     └── Gray

│

├── State Minimization

│     └── Remove equivalent states

│

└── Sequence Detector

```
  ├── Moore

  ├── Mealy

  ├── Overlapping

  └── Non-overlapping
```

```

## ⭐ PHASE 7 MEMORY TRICK

> **FSM → State → Transition → Moore/Mealy → Diagram → Table → Assignment → Sequence Detector → Minimization → Design**
```
