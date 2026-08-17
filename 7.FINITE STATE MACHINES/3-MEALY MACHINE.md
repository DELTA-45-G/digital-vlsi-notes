# MEALY MACHINE ⭐⭐⭐⭐⭐

Now we move to the **second type of FSM: Mealy Machine**.

---

# 1. What is a Mealy Machine?

A **Mealy machine** is an FSM in which the output depends on:

**Present State + Current Input**

Therefore:

**Output=f(State,Input)**

This is the **most important definition** to remember.

---

# 2. Basic Structure

```text id="q8m2v5"
                    ┌─────────────────┐
Input ─────────────►│  Next-State     │
                    │     Logic       │
                    └────────┬────────┘
                             │
                          Next State
                             │
                         ┌───▼───┐
Clock ──────────────────►│  FFs  │
                         └───┬───┘
                             │
                       Present State
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
           State ───────────────► Output Logic ◄── Input
```

The important difference from Moore:

**Input directly participates in output generation**

---

# 3. Mealy Equations ⭐⭐⭐⭐⭐

### Next State

**Next State=f(Present State,Input)**

### Output

**Output=f(Present State,Input)**

Notice that **both** next state and output can depend on the input.

---

# 4. Mealy State Diagram ⭐⭐⭐⭐⭐

In a Mealy machine, the output is written **on the transition arrow**.

Usually the notation is:

**Input/Output**

Example:

```text id="n6c3r9"
             1/1
```

```
   ┌──────────────►

   │
```

┌───────┐
│  S0   │
└───────┘

Here:

* `1` = input
* `1` = output

### Memory Trick

**Mealy → Output on transition**

---

# 5. Moore vs Mealy Diagram

### Moore

```text id="k4p8m2"
┌─────────┐
│ S0 / 0  │
└─────────┘
```

Output is **inside the state**.

### Mealy

```text id="w3x7c5"
S0 ──── 1/0 ────► S1
```

Output is **on the transition**.

### ⭐ Most important memory trick

```text id="r5v9m1"
MOORE  → Output inside STATE
```

MEALY  → Output on EDGE/TRANSITION

---

# 6. Example of Mealy Machine

Suppose we want:

> Output `1` whenever the input `1` arrives while the FSM is in state S1.

We can represent it as:

```text id="y2q6n8"
S0 ────── 1/0 ──────► S1
```

```
                     │

                     │ 1/1

                     ▼

                    S1
```

The output is determined by both:

* Current state
* Current input

Therefore:

**Output=f(State,Input)**

---

# 7. Main Advantage of Mealy Machine ⭐⭐⭐⭐⭐

### Faster response

Because output depends directly on the current input:

**Output=f(State,Input)**

the output can change as soon as the input changes, without necessarily waiting for a state transition.

Therefore:

**Mealy generally responds faster than Moore**

---

# 8. Main Disadvantage ⭐⭐⭐⭐⭐

Because the input directly affects the output, **input glitches can propagate to the output**.

Therefore:

**Mealy output can be less stable**

This is one of the most frequently asked Moore-vs-Mealy concepts.

---

# 9. Number of States

Generally:

**Mealy requires fewer states than Moore**

Why?

Because the output can be generated directly on a transition.

A separate state is often not needed just to represent an output condition.

### Typical comparison

```text id="m7k3p1"
Moore  → More states
```

Mealy  → Fewer states

But remember: this is a **general design tendency**, not an absolute rule for every FSM specification.

---

# 10. Mealy vs Moore — Response

Suppose the input changes:

```text id="p4n8v2"
Input:
```

───────┐

```
   │

   └────────
```

### Mealy

Output can respond directly to input:

**Faster response**

### Moore

Output depends on the state:

**Usually changes after state transition**

---

# 11. Mealy in Sequence Detection ⭐⭐⭐⭐⭐

Suppose we want to detect:

```text id="x6q2m9"
101
```

A Mealy machine can generate the output on the transition that receives the final `1`.

Conceptually:

```text id="c8v5r3"
S0 ──1/0──► S1
```

```
         │

         │ 0/0

         ▼

        S2

         │

         │ 1/1

         ▼

        S1
```

The final transition can produce:

**Output=1**

So Mealy can often detect a sequence using **fewer states** than the corresponding Moore implementation.

---

# 12. Important Placement Question ⭐⭐⭐⭐⭐

### Which machine is generally faster: Moore or Mealy?

**Mealy**

Because the output depends directly on the input.

---

# 13. Another Common Question

### Which machine is more susceptible to input glitches?

**Mealy**

Because:

**Output=f(State,Input)**

The input directly influences the output.

---

# 14. Moore vs Mealy — Complete Comparison ⭐⭐⭐⭐⭐

| Feature            | Moore                | Mealy              |
| ------------------ | -------------------- | ------------------ |
| Output depends on  | State                | State + Input      |
| Output location    | Inside state         | On transition      |
| Response           | Usually slower       | Usually faster     |
| States             | Generally more       | Generally fewer    |
| Glitch sensitivity | Lower                | Higher             |
| Output stability   | More stable          | Less stable        |
| Sequence detector  | May need more states | Often fewer states |

---

# 🧠 Easy Memory Trick

Remember:

### **MOORE**

> **M**achine **O**utput depends on **R**egister/state

More importantly:

**Moore→State**

### **MEALY**

**Mealy→State+Input**

And:

```text id="z5k1p7"
MOORE → OUTPUT INSIDE STATE
```

MEALY → OUTPUT ON TRANSITION

