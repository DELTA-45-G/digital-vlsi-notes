# SEQUENCE DETECTORS ⭐⭐⭐⭐⭐

Sequence detectors are one of the **most important FSM applications** for ECE/VLSI placements.

You should be comfortable with:

* What a sequence detector is
* Moore sequence detector
* Mealy sequence detector
* Overlapping detection
* Non-overlapping detection
* State diagrams
* State tables
* `101`, `110`, etc.

---

# 1. What is a Sequence Detector?

A **sequence detector** is a sequential circuit that detects a specific pattern in a stream of input bits.

For example, suppose we want to detect:

```text id="2h5s8f"
101
```

Input stream:

```text id="7k3m1q"
1 0 1
```

When `101` occurs, the output becomes:

```text id="9n4x6c"
1
```

Otherwise:

```text id="p2v7r5"
0
```

So:

**Sequence Detector → Detects a specific input pattern**

---

# 2. Why Do We Need an FSM?

The circuit needs to remember previous input bits.

For example, if the current input is:

```text id="m8c2y4"
1
```

we don't know whether `101` will occur until future bits arrive.

Therefore the circuit needs **memory**.

That's why sequence detectors are implemented using:

**FSMs**

---

# 3. Example: Detect `101`

Suppose input is:

```text id="x6q1w9"
1 0 1
```

We need to remember:

```text id="r5n8k2"
First bit → 1
```

Second bit → 0

Third bit → 1

Therefore states can represent the progress:

```text id="u3m7p1"
S0 → Nothing matched
```

S1 → 1 matched

S2 → 10 matched

When the next `1` arrives:

```text id="v4c9x6"
10 + 1 = 101
```

Sequence detected.

---

# 4. Moore Sequence Detector ⭐⭐⭐⭐⭐

In a Moore machine:

**Output=f(State)**

Therefore we generally need a separate state representing:

> "The complete sequence has been detected."

For `101`:

```text id="n7p2r8"
S0 → Nothing
```

S1 → 1

S2 → 10

S3 → 101 detected

The output is:

```text id="k5m1q3"
S0 → 0
```

S1 → 0

S2 → 0

S3 → 1

So:

**S3/1**

---

# 5. Mealy Sequence Detector ⭐⭐⭐⭐⭐

In a Mealy machine:

**Output=f(State,Input)**

The output can be generated directly when the final input arrives.

For `101`:

```text id="f3x8v2"
S0 ──1/0──► S1
```

S1 ──0/0──► S2

S2 ──1/1──► ...

The final transition:

```text id="b6m4n9"
1/1
```

means:

```text id="w2q7k5"
Input = 1
```

Output = 1

Therefore the sequence has been detected.

---

# 6. Moore vs Mealy Sequence Detector

| Feature            | Moore                                | Mealy                      |
| ------------------ | ------------------------------------ | -------------------------- |
| Output depends on  | State                                | State + Input              |
| Detection output   | Detection state                      | Detection transition       |
| States             | Generally more                       | Generally fewer            |
| Response           | Generally one state transition later | Can respond on final input |
| Glitch sensitivity | Lower                                | Higher                     |

### 🔥 Placement memory:

```text id="c8p3v6"
Moore → Detection STATE
```

Mealy → Detection TRANSITION

---

# 7. Overlapping Sequence Detection ⭐⭐⭐⭐⭐

This is **very frequently asked**.

Suppose we detect:

```text id="e4m9q1"
101
```

Input:

```text id="k7v2n5"
10101
```

There are **two occurrences**:

```text id="r6x3p8"
10101
^^^

  ^^^
```

The sequences are:

```text id="w5c1m7"
101
```

101

The second occurrence overlaps the first.

Therefore:

**Overlapping detection allows previously detected bits to participate in a new sequence**

---

# 8. Non-Overlapping Detection

In non-overlapping detection, after detecting the sequence, the FSM effectively starts looking for a **new sequence without reusing the detected sequence's overlapping bits**.

For:

```text id="z2n8q4"
10101
```

detecting `101`:

```text id="m5r7x1"
First detection → 101
```

Remaining input → 01

The overlapping occurrence is not counted as another detection.

Therefore:

**Non-overlapping → detected sequence is not reused for the next detection**

---

# 9. Example: `10101`

### Overlapping

Pattern:

```text id="k3v8p6"
101
```

Input:

```text id="n4m1q9"
10101
```

Detected:

```text id="x7c2r5"
101
```

101

So:

**2 detections**

---

### Non-overlapping

First:

```text id="h6p3v8"
101
```

Remaining:

```text id="q2m7n4"
01
```

Therefore:

**1 detection**

---

# 10. Important FSM Concept

For overlapping detection, after detecting the pattern, you **do not necessarily return to S0**.

Instead, you move to a state representing the longest suffix that is also a prefix of the pattern.

This is a very important interview concept.

---

# 11. Example — Overlapping `101`

Pattern:

```text id="m1x7q4"
101
```

After detecting:

```text id="c8v2n5"
101
```

the last `1` can serve as the first `1` of another `101`.

Therefore the FSM can return to:

```text id="r6k3p9"
S1
```

instead of S0.

Conceptually:

```text id="w4m8x2"
S2 ──1/1──► S1
```

The `1` that completed the first pattern is reused as the beginning of the next pattern.

---

# 12. Non-Overlapping `101`

After detecting:

```text id="q5n1v7"
101
```

the FSM can return to:

```text id="c3m8r2"
S0
```

so the next detection begins from scratch.

Conceptually:

```text id="x7p4k6"
S2 ──1/1──► S0
```

The exact transition depends on whether you're using a Moore or Mealy implementation, but the key distinction is the handling of the matched suffix.

---

# 13. Common Placement Question ⭐⭐⭐⭐⭐

### Q: What is the difference between overlapping and non-overlapping sequence detection?

**Answer:**

> In overlapping detection, bits from a previously detected sequence can also be used as part of the next sequence. In non-overlapping detection, the detected sequence is not reused for another detection.

---

# 14. Example: Detect `110`

Suppose input:

```text id="y6m2q8"
110
```

States:

```text id="p4x7n1"
S0 → Nothing matched
```

S1 → 1 matched

S2 → 11 matched

Then:

```text id="v8c3r5"
S2 + 0
```

produces:

```text id="m7k1q4"
110 detected
```

---

# 15. Sequence Detector State Concept

For pattern:

```text id="z2p6m8"
1101
```

we can create states representing:

```text id="c5n9x3"
S0 → ""
```

S1 → "1"

S2 → "11"

S3 → "110"

When final `1` arrives:

```text id="r4v7k2"
110 + 1 = 1101
```

Detection occurs.

### General idea:

**States represent the amount of pattern matched so far**

---

# 16. How Many States?

For a pattern of length N:

### Mealy

Often can be designed using approximately:

**N**

states.

### Moore

Often needs approximately:

**N+1**

states because of the separate detection state.

This is a **general design pattern**, not an absolute rule for every optimized FSM.

---

# 17. 🔥 Placement Numerical

### Q1.

A sequence has length 5.

How many states are commonly needed for a Mealy sequence detector?

**5**

### Q2.

How many states are commonly needed for a Moore sequence detector?

**6**

Again, this is the usual straightforward construction.

---

# 18. Sequence Detector Design Flow

Suppose the question is:

> Design an FSM to detect `1011`.

Follow:

```text id="g8m3v6"
Problem
```

↓

Pattern = 1011

↓

Identify partial matches

↓

Create states

↓

Draw state diagram

↓

Create state table

↓

Assign binary states

↓

Choose flip-flops

↓

Derive equations

↓

Implement circuit

---

# 19. 🔥 Very Important Interview Question

### Why is Mealy often preferred for sequence detection?

Because:

1. It generally requires fewer states.
2. Output can be generated on the transition receiving the final bit.
3. It can respond immediately to the final input.

Therefore:

**Mealy → fewer states + faster detection**

But remember the trade-off:

**Mealy → more sensitive to glitches**

---

# 20. Common Placement MCQs

### Q1. A sequence detector is generally implemented using:

A. Multiplexer
B. FSM
C. Encoder
D. Comparator

**Answer: B — FSM**

---

### Q2. A sequence detector needs memory because:

A. Input is analog
B. Previous inputs affect current detection
C. Clock is absent
D. Output is always zero

**Answer: B**

---

### Q3. Which generally uses fewer states for sequence detection?

A. Moore
B. Mealy
C. Both always equal
D. Neither

**Answer: B — Mealy**

---

### Q4. In a Moore sequence detector, detection output is generally associated with:

A. Input
B. Transition
C. Detection state
D. Clock

**Answer: C**

---

### Q5. In a Mealy sequence detector, detection output is generally generated on:

A. State only
B. Transition
C. Reset
D. Flip-flop initialization

**Answer: B**

---

### Q6. What does overlapping detection mean?

**Answer:**

Previously detected bits can participate in the next detected sequence.

---

### Q7. For pattern `101`, how many times does it occur in `10101` with overlapping detection?

**2**

---

### Q8. For pattern `101`, how many times does it occur in `10101` with non-overlapping detection?

**1**

---

# 🧠 QUICK REVISION

```text id="s3k8m5"
SEQUENCE DETECTOR

→ Detects a specific bit pattern

→ Usually implemented using FSM


Example:

Pattern = 101


Moore:

→ Detection state

→ Generally more states


Mealy:

→ Detection transition

→ Generally fewer states

→ Faster response

→ More glitch-sensitive


Overlapping:

→ Reuse matched suffix

→ Example: 10101 contains 2 occurrences of 101


Non-overlapping:

→ Don't reuse detected sequence

→ 10101 gives 1 detection


Key idea:

→ States represent partial pattern matches
```
