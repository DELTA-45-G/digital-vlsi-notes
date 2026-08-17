# MOORE MACHINE ⭐⭐⭐⭐⭐

A **Moore machine** is one of the two basic types of FSMs.

The two types are:

1. **Moore Machine**
2. **Mealy Machine**

We'll learn Moore first.

---

# 1. What is a Moore Machine?

A **Moore machine** is an FSM in which the **output depends only on the present state**.

**Output=f(Present State)**

The current input does **not directly determine the output**.

---

# 2. Basic Structure

```text id="q5m2v8"
              ┌─────────────────┐
Input ───────►│  Next-State     │
              │     Logic       │
              └────────┬────────┘
                       │
                    Next State
                       │
                    ┌──▼──┐
Clock ─────────────►│ FFs │
                    └──┬──┘
                       │
                 Present State
                       │
              ┌────────▼────────┐
              │  Output Logic   │
              └────────┬────────┘
                       │
                     Output
```

The important point is:

**Output→Present State**

---

# 3. Moore Machine Equation ⭐⭐⭐⭐⭐

### Next State

**Next State=f(Present State,Input)**

### Output

**Output=f(Present State)**

This distinction is **very important for placements**.

---

# 4. Moore State Diagram ⭐⭐⭐⭐⭐

In a Moore machine, the output is written **inside the state**.

For example:

```text id="s8n3k1"
        ┌─────────┐
        │ S0 / 0  │
        └─────────┘
```

Here:

* State = `S0`
* Output = `0`

Another state:

```text id="r6p2m9"
        ┌─────────┐
        │ S1 / 1  │
        └─────────┘
```

Output = `1`.

### Memory Trick

**Moore → Output inside State**

---

# 5. Example

Consider:

```text id="w3c7j5"
        1
```

┌──────────►

│

┌───────┐      ┌───────┐
│ S0/0  │      │ S1/1  │
└───────┘      └───────┘
▲              │
│              │ 0
└──────────────┘

````

The output depends on the current state:

```text id="n4h8q2"
S0 → Output 0
````

S1 → Output 1

Even if the input changes, the output is determined by the current state.

---

# 6. Moore State Table ⭐⭐⭐⭐⭐

A Moore state table generally looks like:

| Present State | Input | Next State | Output |
| ------------- | ----- | ---------- | ------ |
| S0            | 0     | S0         | 0      |
| S0            | 1     | S1         | 0      |
| S1            | 0     | S0         | 1      |
| S1            | 1     | S1         | 1      |

Notice something important:

For a particular state, the output is the **same regardless of input**.

For `S0`:

```text id="e2y6p9"
Input 0 → Output 0
```

Input 1 → Output 0

For `S1`:

```text id="c5m1r7"
Input 0 → Output 1
```

Input 1 → Output 1

That's because:

**Output=f(State)**

---

# 7. Key Characteristic ⭐⭐⭐⭐⭐

Suppose:

**State=S1**

and:

**Output=1**

If the input changes from `0` to `1`, the output **doesn't directly change** just because of that input change.

The output changes when the FSM transitions to a different state.

Therefore, Moore output is generally **more stable**.

---

# 8. Advantages of Moore Machine ⭐⭐⭐⭐

### 1. More stable output

Since output depends only on the state:

**Output=f(State)**

input glitches do not directly affect the output.

### 2. Easier to design and debug

Output behavior is directly associated with states.

### 3. Less prone to input glitches

The input does not directly control the output.

---

# 9. Disadvantages of Moore Machine ⭐⭐⭐⭐

### 1. May require more states

A Moore machine sometimes needs additional states to generate the desired output sequence.

### 2. Output response can be delayed

Since the output depends on the state, the FSM may need to transition to another state before the output changes.

---

# 10. Moore vs Combinational Logic

### Combinational:

**Output=f(Input)**

### Moore:

**Output=f(State)**

### Mealy:

**Output=f(State,Input)**

This three-way distinction is worth remembering.

---

# 11. Moore Machine in Sequence Detection ⭐⭐⭐⭐⭐

Suppose we want to detect:

```text id="k7v3p4"
101
```

In a Moore sequence detector, we generally create a separate state representing:

> "The complete sequence has been detected."

For example:

```text id="y2m8c6"
S0 → S1 → S2 → S3
```

where:

```text id="r5x1n9"
S0 = nothing detected
```

S1 = 1 detected

S2 = 10 detected

S3 = 101 detected

Outputs:

```text id="b6q4w2"
S0 → 0
```

S1 → 0

S2 → 0

S3 → 1

Notice:

**Detection output is associated with a state**

---

# 12. Important Placement Question ⭐⭐⭐⭐⭐

### Which FSM generally requires more states: Moore or Mealy?

Usually:

**Moore**

because outputs are associated with states, and additional states may be required to represent output conditions.

However, don't treat this as an absolute rule for every possible specification.

---

# 13. Moore Output Timing ⭐⭐⭐⭐⭐

A common placement concept:

### Moore

Output changes when the **state changes**.

Since state changes normally occur at the clock edge:

**Moore output is generally clock/state dependent**

### Mealy

Output can respond directly to input changes because:

**Output=f(State,Input)**

Therefore Mealy can respond **faster**.

---

# 🧠 MOORE MACHINE — QUICK REVISION

```text id="p8k2m5"
MOORE MACHINE
────────────────────────

Output:

→ Depends ONLY on present state

Equation:

→ Output = f(State)

Next state:

→ Next State = f(State, Input)

State diagram:

→ Output written INSIDE state

Advantages:

→ Stable output

→ Less sensitive to input glitches

→ Easier output interpretation

Disadvantages:

→ May require more states

→ Output may respond one clock/state transition later

Memory trick:

→ MOORE = MORE state-dependent

→ Output INSIDE the state
```
