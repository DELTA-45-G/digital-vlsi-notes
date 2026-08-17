# STATE DIAGRAM ⭐⭐⭐⭐⭐

Now we move to **State Diagrams**, one of the most important practical FSM topics for placements.

---

# 1. What is a State Diagram?

A **state diagram** is a graphical representation of an FSM.

It shows:

* States
* Transitions
* Inputs
* Outputs
* Direction of state changes

In simple terms:

> **State diagram = visual representation of how an FSM moves between states.**

---

# 2. Basic State Representation

A state is usually represented by a **circle**.

```text id="p7r2m5"
      ┌───────┐
      │  S0   │
      └───────┘
```

Here:

**S0=State**

---

# 3. State Transition

An arrow between states represents a **transition**.

```text id="m4q8v1"
┌───────┐       ┌───────┐
│  S0   │──────►│  S1   │
└───────┘       └───────┘
```

This means:

**S0→S1**

The FSM moves from S0 to S1 when the specified transition condition occurs.

---

# 4. Self-Loop

A state can transition back to itself.

```text id="k6n3x9"
       ┌───────┐
       │  S0   │
       └───┬───┘
           │
           └──────► S0
```

This is called a:

**Self-loop**

Example:

If:

**Input=0**

the FSM may remain in S0.

---

# 5. Moore State Diagram ⭐⭐⭐⭐⭐

In a Moore machine, the output is associated with the **state**.

Typical notation:

**State/Output**

Example:

```text id="z8c2m4"
┌─────────┐
│  S0 / 0 │
└─────────┘
```

Here:

* State = S0
* Output = 0

Another state:

```text id="t3p7y5"
┌─────────┐
│  S1 / 1 │
└─────────┘
```

Therefore:

```text id="h5r1q8"
S0 → output 0
```

S1 → output 1

### 🔥 Remember

**Moore → Output inside state**

---

# 6. Mealy State Diagram ⭐⭐⭐⭐⭐

In a Mealy machine, the output is associated with the **transition**.

The common notation is:

**Input/Output**

Example:

```text id="n2v6k9"
S0 ───── 1/0 ─────► S1
```

Here:

* `1` = Input
* `0` = Output

### 🔥 Remember

**Mealy → Output on transition**

---

# 7. Moore vs Mealy Diagram

### Moore

```text id="c7m3p1"
┌─────────┐
│ S0 / 0  │
└─────────┘
```

### Mealy

```text id="x4q8n6"
S0 ───── 1/0 ─────► S1
```

This is one of the **most common FSM placement questions**.

---

# 8. Reading a State Diagram

Suppose we have:

```text id="w9k2r5"
          1
```

```
  ┌───────►

  │
```

┌─────┴─┐       ┌───────┐
│  S0   │──────►│  S1   │
└───────┘   0   └───────┘

If the arrow from S0 to S1 is labeled `0`, then:

**Input=0**

causes:

**S0→S1**

---

# 9. Multiple Transitions

A state can have different transitions for different inputs.

Example:

```text id="m6c1v8"
             1
```

```
    ┌──────────► S1

    │

  S0

    │

    └──────────► S2

         0
```

Therefore:

```text id="a5r7k3"
Input = 1 → S1
```

Input = 0 → S2

---

# 10. Complete State Diagram Example

Consider a simple FSM with two states:

```text id="q8n4x2"
                    1
```

```
          ┌─────────────►

          │

      ┌───┴───┐       ┌───────┐

      │  S0   │──────►│  S1   │

      └───────┘   0   └───────┘

          ▲               │

          │               │

          └────── 0 ──────┘
```

````

The exact transition behavior depends on the specified design.

The important point is that every transition should specify the condition under which the FSM changes state.

---

# 11. State Diagram → State Table ⭐⭐⭐⭐⭐

This is a **very common placement/design question**.

Suppose:

```text id="v3p9m2"
S0 --0--> S0
````

S0 --1--> S1

S1 --0--> S0

S1 --1--> S1

We can convert it into:

| Present State | Input | Next State |
| ------------- | ----- | ---------- |
| S0            | 0     | S0         |
| S0            | 1     | S1         |
| S1            | 0     | S0         |
| S1            | 1     | S1         |

For a Moore machine, add the output associated with each state.

---

# 12. State Table → State Diagram

The reverse is also possible.

Given:

| Present State | Input | Next State |
| ------------- | ----- | ---------- |
| S0            | 0     | S0         |
| S0            | 1     | S1         |
| S1            | 0     | S0         |
| S1            | 1     | S1         |

Draw:

```text id="j5k2r8"
S0 ──1──► S1
```

▲         │

│         │ 1

│         ▼

└───0──── S1

S0 ──0──► S0

S1 ──0──► S0

The key skill is understanding that the table and diagram represent the **same FSM behavior**.

---

# 13. Initial State ⭐⭐⭐⭐

An FSM generally starts from a known state after reset.

For example:

```text id="b7m4q1"
RESET
```

↓

S0

The reset establishes the initial state.

---

# 14. State Diagram and Clock ⭐⭐⭐⭐⭐

State transitions normally occur at the active clock edge in a synchronous FSM.

Conceptually:

```text id="c9x2n5"
Present State
```

```
  ↓
```

Input

```
  ↓
```

Next-State Logic

```
  ↓
```

Next State

```
  ↓
```

Clock Edge

```
  ↓
```

New Present State

---

# 15. Important Placement Concept: Every Input Combination

For a properly specified FSM, every possible input condition should have a defined next state.

For a **1-bit input**, there are:

**2¹=2**

possible input combinations:

```text id="r6v3k8"
0
```

1

For a **2-bit input**:

**2²=4**

possible combinations:

```text id="p4m9y2"
00
```

01

10

11

---

# 16. Number of Transitions

For an FSM with:

* N states
* M binary input bits

Each state can have up to:

**2ᴹ**

input combinations.

Therefore, a fully specified FSM can have up to:

**N×2ᴹ**

state-transition entries.

### Example

4 states and 2 input bits:

**4×2²=4×4=16**

possible state/input combinations.

---

# 17. State Diagram — Common Interview Questions

### Q1. What does a circle represent?

**Answer:**

**State**

### Q2. What does an arrow represent?

**Answer:**

**State transition**

### Q3. What does a self-loop represent?

**Answer:**

The FSM remains in the same state under a particular input condition.

### Q4. Where is output written in Moore?

**Answer:**

**Inside the state**

### Q5. Where is output written in Mealy?

**Answer:**

**On the transition**

---

# 18. 🔥 Placement Trap

Suppose you see:

```text id="n8q4c6"
S0 ───── 1/0 ─────► S1
```

Don't confuse:

```text id="x2m7v5"
1 = output
```

0 = input

The standard notation is:

**Input/Output**

Therefore:

```text id="f3k9r1"
1 = Input
```

0 = Output

This is a **Mealy transition**.

---

# 🧠 QUICK REVISION — STATE DIAGRAM

```text id="q6m2x8"
STATE DIAGRAM

→ Graphical FSM representation


Circle

→ State


Arrow

→ Transition


Self-loop

→ Remain in same state


Moore

→ State/Output


Mealy

→ Input/Output


State Diagram ↔ State Table


1-bit input

→ 2 input combinations


2-bit input

→ 4 input combinations


N states + M inputs

→ Maximum N × 2^M transition entries
```
