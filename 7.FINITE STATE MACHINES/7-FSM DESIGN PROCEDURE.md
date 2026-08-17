# FSM DESIGN PROCEDURE ⭐⭐⭐⭐⭐

This is one of the **most important Phase 7 topics for VLSI placements**.

So far, you learned how to **understand** an FSM. Now we'll learn how to **design** one from a problem statement.

---

# 1. What is FSM Design?

FSM design means converting a required system behavior into a sequential digital circuit.

For example:

> Design a circuit that detects the sequence `101`.

We need to go from:

```text
Problem Statement
```

```
   ↓
```

Identify States

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

Circuit

This complete flow is extremely important.

---

# 2. Step 1 — Understand the Problem ⭐⭐⭐⭐⭐

First identify:

* What is the input?
* What is the output?
* What sequence/behavior is required?
* Is overlap allowed?
* Is it Moore or Mealy?
* What should happen after reset?

### Example

> Design a sequence detector for `101`.

We identify:

```text
Input  → X
```

Output → Y

Pattern → 101

---

# 3. Step 2 — Identify the States ⭐⭐⭐⭐⭐

States should represent the **progress of the system**.

For detecting `101`, we can track how much of the sequence has been matched.

### State S0

Nothing matched.

```text
Matched = ""
```

### State S1

We received:

```text
1
```

So:

```text
Matched = "1"
```

### State S2

We received:

```text
10
```

So:

```text
Matched = "10"
```

For a Moore detector, we may need:

### State S3

Complete sequence detected:

```text
Matched = "101"
```

Therefore:

```text
S0 → Nothing
```

S1 → 1

S2 → 10

S3 → 101

---

# 4. Step 3 — Draw the State Diagram ⭐⭐⭐⭐⭐

For a Moore sequence detector:

```text
                 1
```

```
      ┌────────────►

      │

   ┌──────┐

   │ S0/0 │

   └──────┘

      │

      │ 1

      ▼

   ┌──────┐

   │ S1/0 │

   └──────┘

      │

      │ 0

      ▼

   ┌──────┐

   │ S2/0 │

   └──────┘

      │

      │ 1

      ▼

   ┌──────┐

   │ S3/1 │

   └──────┘
```

````

The exact transitions for all inputs must be completed based on the desired overlap behavior.

The key idea is:

> **Each state represents how much of the desired pattern has already been recognized.**

---

# 5. Step 4 — Create the State Table ⭐⭐⭐⭐⭐

Once the state diagram is complete, convert it into a table.

For example:

| Present State | Input | Next State | Output |
|---|---|---|---|
| S0 | 0 | S0 | 0 |
| S0 | 1 | S1 | 0 |
| S1 | 0 | S2 | 0 |
| S1 | 1 | S1 | 0 |
| S2 | 0 | S0 | 0 |
| S2 | 1 | S3 | 0 |
| S3 | 0 | S2/S0* | 1 |
| S3 | 1 | S1* | 1 |

The exact recovery transitions depend on whether **overlapping detection** is required.

---

# 6. Step 5 — State Assignment ⭐⭐⭐⭐⭐

Now assign binary values to the states.

For 4 states, we need:

**⌈log₂4⌉=2**

flip-flops.

One possible assignment:

| State | Binary |
|---|---|
| S0 | 00 |
| S1 | 01 |
| S2 | 10 |
| S3 | 11 |

Therefore:

```text
S0 = 00
````

S1 = 01

S2 = 10

S3 = 11

---

# 7. Step 6 — Choose the Flip-Flop Type

Common choices:

* D flip-flop
* JK flip-flop
* T flip-flop

For basic FSM design, **D flip-flops are often easiest** because:

**D=Qnext**

So if the next-state table tells us:

```text
Qnext = 1
```

then:

```text
D = 1
```

---

# 8. Step 7 — Create the Excitation Table ⭐⭐⭐⭐⭐

If using a T flip-flop:

**T=Q⊕Qnext**

If using a D flip-flop:

**D=Qnext**

If using a JK flip-flop, use the JK excitation table.

---

# 9. D Flip-Flop Excitation

For a D flip-flop:

| Present Q | Next Q | D |
| --------- | ------ | - |
| 0         | 0      | 0 |
| 0         | 1      | 1 |
| 1         | 0      | 0 |
| 1         | 1      | 1 |

Therefore:

**D=Qnext**

Very easy.

---

# 10. T Flip-Flop Excitation

| Q | Qnext | T |
| - | ----- | - |
| 0 | 0     | 0 |
| 0 | 1     | 1 |
| 1 | 0     | 1 |
| 1 | 1     | 0 |

Therefore:

**T=Q⊕Qnext**

---

# 11. Step 8 — Derive Boolean Equations ⭐⭐⭐⭐⭐

After obtaining the excitation table, derive equations for the flip-flop inputs.

For example:

**D1=f(Q1,Q0,X)**

**D0=f(Q1,Q0,X)**

And output:

**Y=f(Q1,Q0,X)**

depending on Moore/Mealy.

Then simplify the equations using:

* Boolean algebra
* K-map

---

# 12. Step 9 — Implement the Circuit

Finally, connect:

```text
Input
```

↓

Next-State Logic

↓

D/JK/T Flip-Flops

↓

State Register

↓

Output Logic

↓

Output

The FSM is now implemented as hardware.

---

# 13. Complete FSM Design Flow ⭐⭐⭐⭐⭐

This is **placement-important**.

```text
1. Problem Specification
```

```
      ↓
```

2. Identify Inputs & Outputs

```
      ↓
```

3. Identify States

```
      ↓
```

4. Draw State Diagram

```
      ↓
```

5. Create State Table

```
      ↓
```

6. State Assignment

```
      ↓
```

7. Select Flip-Flop

```
      ↓
```

8. Excitation Table

```
      ↓
```

9. Boolean Equations

```
      ↓
```

10. Simplification

```
      ↓
```

11. Circuit Implementation

### 🔥 Memorize this sequence.

---

# 14. Why State Assignment Matters

Suppose we have 4 states.

There are different possible assignments:

### Binary

```text
S0 = 00
```

S1 = 01

S2 = 10

S3 = 11

### Another assignment

```text
S0 = 00
```

S1 = 10

S2 = 11

S3 = 01

Different assignments can produce different logic complexity.

This leads directly to our next topic:

> **State Assignment techniques**

---

# 15. Moore FSM Design

For Moore:

**Y=f(Q)**

Therefore, after state assignment, output is determined from the state bits.

Example:

```text
S0 → Y=0
```

S1 → Y=0

S2 → Y=0

S3 → Y=1

Then:

**Y=Q1Q0**

for the assignment:

```text
S3 = 11
```

---

# 16. Mealy FSM Design

For Mealy:

**Y=f(Q,X)**

So the output logic uses:

* State bits
* Input

Example:

**Y=Q1X**

This means output can change based on the current input even while the state remains the same.

---

# 17. Common Placement Question ⭐⭐⭐⭐⭐

### Q: What is the first step in FSM design?

**Answer:**

**Understand/specify the required behavior**

Not K-map.

Not choosing flip-flops.

Not drawing the circuit.

First understand the required behavior and identify inputs, outputs, and states.

---

# 18. Common Placement Question

### Q: What comes after the state diagram?

**State Table**

---

### Q: What comes after state assignment?

Usually:

**Choose flip-flop / derive excitation requirements**

---

### Q: Which flip-flop is easiest for FSM implementation?

Common answer:

**D flip-flop**

because:

**D=Qnext**

---

# 19. Important Design Mistakes

### Mistake 1 — Missing input conditions

Every state should account for the required input combinations.

### Mistake 2 — Wrong state assignment

Incorrect encoding can produce incorrect transitions.

### Mistake 3 — Confusing Moore and Mealy outputs

Remember:

```text
Moore → State
```

Mealy → State + Input

### Mistake 4 — Ignoring reset

The FSM should normally have a defined starting state.

### Mistake 5 — Ignoring unused states

If the number of state bits gives more binary combinations than required, unused states should be considered.

---

# 🧠 QUICK REVISION — FSM DESIGN

```text
Specification
```

```
 ↓
```

Inputs / Outputs

```
 ↓
```

States

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

Choose FF

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

K-map / Simplification

```
 ↓
```

Circuit

### Important equations:

**D=Qnext**

**T=Q⊕Qnext**

**Moore:Y=f(Q)**

**Mealy:Y=f(Q,X)**
