# SR LATCH ⭐⭐⭐⭐⭐

Now we move to the **first actual memory circuit**.

Understanding the SR latch is important because it helps you understand **how a circuit can store 1 bit**.

---

# 1. What is an SR Latch?

**SR** stands for:

* **S = Set**
* **R = Reset**

An SR latch is a basic memory circuit that can store **one bit**.

It has:

* Set input S
* Reset input R
* Output Q
* Complementary output Q̅

```text
       ┌───────────┐
S ────►│           │────► Q
       │ SR Latch  │
R ────►│           │────► Q̅
       └───────────┘
```

---

# 2. Why Do We Need an SR Latch?

Combinational circuits cannot remember previous values.

The SR latch introduces **feedback**, allowing the circuit to maintain a state.

### Key idea ⭐

**Feedback + gates → Memory**

---

# 3. Basic NOR-Based SR Latch ⭐⭐⭐⭐⭐

One common SR latch is made using **two cross-coupled NOR gates**.

```text
              ┌───────┐
    S ───►    │  NOR  │──────► Q
              └───┬───┘       │
                  ▲            │
                  │            ▼
              ┌───┴───┐
    R ───►    │  NOR  │◄──────┘
              └───────┘
```

The outputs are fed back into each other.

This **feedback** is what allows the circuit to remember its previous state.

---

# 4. NOR SR Latch Truth Table ⭐⭐⭐⭐⭐

For a NOR-based SR latch, inputs are **active-high**.

| S | R | Q(next)    | Operation     |
| - | - | ---------- | ------------- |
| 0 | 0 | Previous Q | **Hold**      |
| 0 | 1 | 0          | **Reset**     |
| 1 | 0 | 1          | **Set**       |
| 1 | 1 | Invalid    | **Forbidden** |

This table is extremely important.

---

# 5. Understand Each Condition

## Case 1: S=0, R=0 → HOLD ⭐

The latch keeps its previous state.

If:

Q=1

it remains:

Q=1

If:

Q=0

it remains:

Q=0

Therefore:

**S=0, R=0 ⇒ Q=Qprevious**

### Memory trick:

> **00 = Hold**

---

# Case 2: S=1, R=0 → SET ⭐

Set means:

Q=1

Therefore:

**S=1, R=0 ⇒ Q=1**

### Memory trick:

> **S = Set → Q becomes 1**

---

# Case 3: S=0, R=1 → RESET ⭐

Reset means:

Q=0

Therefore:

**S=0, R=1 ⇒ Q=0**

### Memory trick:

> **R = Reset → Q becomes 0**

---

# Case 4: S=1, R=1 → INVALID ⭐⭐⭐⭐⭐

This is the forbidden condition for the basic NOR SR latch.

Why?

Both NOR gates are forced to produce:

Q=0

and:

Q̅=0

But normally we expect:

Q̅ = Q̅

If:

Q=0

then:

Q̅

should be 1.

Instead, both become 0.

Therefore the state is invalid.

---

# ⭐ NOR SR Latch Memory Trick

Memorize:

```text
S R
──────
0 0 → HOLD
0 1 → RESET
1 0 → SET
1 1 → INVALID
```

Or:

> **00 Hold, 01 Reset, 10 Set, 11 Bad**

This is extremely useful for MCQs.

---

# 6. Why Is It Called a Latch?

Because it is **level-sensitive / asynchronous storage** rather than an edge-triggered device.

The basic NOR SR latch does not require a clock.

That is important:

**Basic SR latch has no clock**

---

# 7. The Feedback Concept ⭐⭐⭐⭐⭐

This is one of the most important concepts to understand.

Imagine:

```text
       ┌─────┐
S ────►│ NOR │───► Q
       └──┬──┘    │
          ▲       │
          │       ▼
       ┌──┴──┐    │
R ────►│ NOR │◄───┘
       └─────┘
```

The output of one gate influences the other gate.

This creates a **stable state**.

Once the latch is set:

Q=1

it can maintain that value even after the Set input is removed.

That's the fundamental idea of memory.

---

# 8. Example

Suppose initially:

Q=0

Apply:

S=1,R=0

The latch becomes:

Q=1

Now return inputs to:

S=0,R=0

What happens?

The latch **holds**:

Q=1

This demonstrates memory.

---

# 9. NOR vs NAND SR Latch ⭐⭐⭐⭐⭐

This is a common placement question.

There are two common implementations:

### NOR-based SR latch

Inputs are **active-high**.

```text
S=1 → Set
```

R=1 → Reset

### NAND-based SR latch

Inputs are generally **active-low**.

Often written:

S̅,R̅

For NAND:

```text
S̅ = 0 → Set
```

R̅ = 0 → Reset

### ⭐ Important

Don't memorize only the letters S and R.

Look at whether the inputs are **active-high or active-low**.

---

# 10. NOR vs NAND Quick Comparison

| Feature      | NOR SR Latch | NAND SR Latch |
| ------------ | ------------ | ------------- |
| Active input | High         | Low           |
| Set          | S=1          | S̅=0          |
| Reset        | R=1          | R̅=0          |
| Hold         | 00           | 11            |
| Forbidden    | 11           | 00            |

⭐ This table is very frequently tested.

---

# 11. Why Is the Invalid State Dangerous?

For the NOR latch:

S=R=1

forces both outputs low.

When the inputs return to the normal condition simultaneously, the final state can become uncertain due to differences in gate delays.

Therefore:

**Avoid the forbidden condition**

This concept will connect later to **metastability and timing problems**.

---

# 12. Real Hardware Relevance ⭐⭐⭐⭐

SR-type storage concepts appear in:

* Control circuits
* Set/reset logic
* Asynchronous control
* Simple memory elements
* Control flags

In modern VLSI, you usually won't build large systems directly from basic NOR SR latches, but understanding the principle is essential for understanding more advanced storage structures.

---

# 13. Placement Questions

### Q1. What does SR stand for?

Set-Reset

### Q2. How many bits can an SR latch store?

1 bit

### Q3. What is the hold condition of a NOR SR latch?

S=0,R=0

### Q4. What is the set condition?

S=1,R=0

### Q5. What is the reset condition?

S=0,R=1

### Q6. What is the invalid condition?

S=1,R=1

### Q7. Does a basic SR latch require a clock?

No

### Q8. Why does an SR latch have memory?

Because of:

**Cross-coupled feedback**

### Q9. Which SR latch uses active-low inputs?

NAND-based SR latch

### Q10. Which condition is forbidden for a NAND SR latch?

S=R=0

---

# ⭐ Quick Revision

```text
SR LATCH
────────────────────────────

S = Set

R = Reset

Stores:

1 bit

NOR SR Latch:

Active HIGH

S R

0 0 → HOLD

0 1 → RESET

1 0 → SET

1 1 → INVALID

NAND SR Latch:

Active LOW

S̅ R̅

1  1 → HOLD

1  0 → SET

0  1 → RESET

0  0 → INVALID

KEY IDEA:

Cross-coupled feedback creates memory.

Memory trick:

NOR:

00 Hold

01 Reset

10 Set

11 Invalid
```
