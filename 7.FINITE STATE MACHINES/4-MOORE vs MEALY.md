# MOORE vs MEALY ⭐⭐⭐⭐⭐

This is one of the **most frequently asked FSM topics in VLSI/ECE placements**.

You should be able to answer the basic comparison in **20–30 seconds** during an interview.

---

# 1. Fundamental Difference ⭐⭐⭐⭐⭐

### Moore Machine

Output depends **only on present state**.

**Y=f(Q)**

### Mealy Machine

Output depends on **present state and input**.

**Y=f(Q,X)**

### 🔥 Memory Trick

```text id="t4x7p2"
MOORE → STATE
```

MEALY → STATE + INPUT

---

# 2. Output Location in State Diagram ⭐⭐⭐⭐⭐

### Moore

Output is written **inside the state**.

```text id="k8m3q1"
┌─────────┐
│ S0 / 0  │
└─────────┘
```

### Mealy

Output is written **on the transition**.

```text id="v5n2r9"
S0 ───── 1/0 ─────► S1
```

Here:

* `1` = input
* `0` = output

---

# 3. Response Speed ⭐⭐⭐⭐⭐

### Mealy

Output can respond immediately to an input change.

**Generally faster**

### Moore

Output depends on the state, so it generally changes after a state transition.

**Generally slower**

### Placement Question

**Which FSM responds faster to input changes?**

**Mealy**

---

# 4. Number of States ⭐⭐⭐⭐⭐

Generally:

**Moore → More states**

**Mealy → Fewer states**

### Why?

In Moore, output is associated with states.

Sometimes an additional state is required just to generate a particular output.

In Mealy, output can be generated directly on a transition.

---

# 5. Glitch Sensitivity ⭐⭐⭐⭐⭐

### Moore

Output depends only on state.

Therefore it is generally:

**More stable**

### Mealy

Output depends directly on input.

Therefore an input glitch can potentially appear at the output.

**More susceptible to glitches**

---

# 6. Output Stability

| Moore                            | Mealy           |
| -------------------------------- | --------------- |
| More stable                      | Less stable     |
| State-dependent                  | Input-dependent |
| Less sensitive to input glitches | More sensitive  |

---

# 7. Sequence Detector Comparison ⭐⭐⭐⭐⭐

This is **very commonly asked**.

Suppose we want to detect:

```text id="m6q2y8"
101
```

### Moore

Usually requires a separate detection state:

```text id="c4v9p1"
S0 → S1 → S2 → S3
```

Output becomes `1` in the detection state.

### Mealy

The output can be generated directly on the transition that receives the final bit:

```text id="r8k3x5"
S0 → S1 → S2
```

```
      │

    1/1
```

Therefore, Mealy generally requires **fewer states**.

---

# 8. Output Timing — Important Trick Question ⭐⭐⭐⭐⭐

### Question:

**Can a Mealy output change without a clock edge?**

Potentially **yes**, because output depends directly on the input.

**Y=f(State,Input)**

If the input changes, the output can change.

### Moore:

Output is state-dependent:

**Y=f(State)**

so state changes generally occur at the clock edge.

---

# 9. Which One Is Easier to Design? ⭐⭐⭐⭐

In many basic designs:

**Moore is easier to understand and debug**

because each state has an associated output.

However, actual design complexity depends on the specific specification.

---

# 10. Which One Uses More Hardware?

There isn't a universal answer for total hardware because it depends on the implementation.

But generally:

* Moore → potentially more states → potentially more state storage/logic
* Mealy → potentially fewer states

For placement questions, remember:

**Moore generally uses more states**

rather than claiming it **always** uses more hardware.

---

# 11. Complete Comparison Table ⭐⭐⭐⭐⭐

| Feature                             | Moore             | Mealy               |
| ----------------------------------- | ----------------- | ------------------- |
| Output                              | State             | State + Input       |
| Equation                            | Y=f(Q)            | Y=f(Q,X)            |
| Output location                     | Inside state      | On transition       |
| Response                            | Generally slower  | Generally faster    |
| States                              | Generally more    | Generally fewer     |
| Glitch sensitivity                  | Lower             | Higher              |
| Output stability                    | Higher            | Lower               |
| Sequence detector                   | More states       | Fewer states        |
| Output can react directly to input? | No                | Yes                 |
| Design/debugging                    | Generally simpler | Can be more complex |

---

# 12. Very Common Placement MCQs ⭐⭐⭐⭐⭐

### Q1. In a Moore machine, output depends on:

A. Input only
B. Present state only
C. Present state and input
D. Previous state only

**Answer: B**

---

### Q2. In a Mealy machine, output depends on:

A. State only
B. Input only
C. State and input
D. Clock only

**Answer: C**

---

### Q3. In a Moore state diagram, output is generally written:

A. On transition
B. Inside state
C. Outside diagram
D. On clock

**Answer: B**

---

### Q4. In a Mealy state diagram, transition labels are usually:

A. State/Output
B. Input/Output
C. Output/Input
D. State/Input

**Answer: B**

---

### Q5. Which generally has faster response?

A. Moore
B. Mealy
C. Both always identical
D. Neither

**Answer: B**

---

### Q6. Which is generally more susceptible to input glitches?

A. Moore
B. Mealy
C. Both equally
D. Neither

**Answer: B**

---

### Q7. Which generally requires fewer states?

A. Moore
B. Mealy
C. Both always equal
D. Depends only on clock frequency

**Answer: B**

---

# 13. 🔥 Interview Question

### "Explain Moore vs Mealy in 30 seconds."

A good placement answer:

> **A Moore machine generates output based only on the present state, while a Mealy machine generates output based on both the present state and current input. Moore outputs are generally more stable and may require more states, whereas Mealy machines generally respond faster and often require fewer states but can be more sensitive to input glitches.**

That is a strong interview-level answer.

---

# 🧠 10-SECOND REVISION

```text id="z2n7c4"
MOORE

→ Output = State

→ Output inside state

→ Generally more states

→ Generally slower response

→ More stable

→ Less glitch-sensitive


MEALY

→ Output = State + Input

→ Output on transition

→ Generally fewer states

→ Generally faster response

→ Less stable

→ More glitch-sensitive
```
