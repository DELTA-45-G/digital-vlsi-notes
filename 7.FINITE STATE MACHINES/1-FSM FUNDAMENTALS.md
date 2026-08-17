## 7.1 FSM FUNDAMENTALS ⭐⭐⭐⭐⭐

Let's start Phase 7 **from the basics**, just like we did for the previous phases.

---

# 1. What is an FSM?

**FSM (Finite State Machine)** is a sequential logic model that has a **finite number of states** and changes from one state to another based on **inputs and clock signals**.

In simple words:

> An FSM is a digital system that remembers its current state and decides its next state based on the input.

### Basic structure

```text id="d9m3r7"
             ┌───────────────┐
Input ──────►│               │
             │      FSM      │───► Output
Clock ──────►│               │
             └───────┬───────┘
                     │
                     ▼
                Next State
```

---

# 2. Why Do We Need FSMs?

FSMs are used when a digital system needs to perform **different operations depending on its current condition/state**.

Examples:

* Traffic light controller
* Vending machine
* Elevator controller
* Digital lock
* Sequence detector
* Communication protocols
* CPU control logic
* Washing machine controller

---

# 3. FSM vs Combinational Circuit ⭐⭐⭐⭐⭐

This is important.

### Combinational Circuit

Output depends only on the **current input**.

**Output=f(Input)**

Example:

```text id="b4k8m2"
Input ──► Logic ──► Output
```

No memory.

---

### Sequential Circuit / FSM

Output depends on the **current input and/or current state**.

**Next State=f(Current State,Input)**

Therefore, FSMs contain **memory elements**, usually flip-flops.

```text id="c6p1x9"
              ┌──────────────┐
Input ───────►│ Combinational│────► Output
              │    Logic     │
              └──────┬───────┘
                     │
                  Next State
                     │
                     ▼
                 ┌───────┐
                 │  FFs  │
                 └───┬───┘
                     │
                Current State
                     │
                     └──────────► Logic
```

---

# 4. Main Components of an FSM ⭐⭐⭐⭐⭐

An FSM generally contains:

### 1. State Register

Stores the **current state**.

Usually implemented using flip-flops.

### 2. Next-State Logic

Determines what the next state should be.

**Next State=f(Current State,Input)**

### 3. Output Logic

Determines the output.

Depending on the FSM type:

**Moore:**

**Output=f(Current State)**

**Mealy:**

**Output=f(Current State,Input)**

---

# 5. What is a State?

A **state** represents the current condition or situation of the system.

For example, consider a traffic light:

```text id="f5n2k8"
RED
```

↓

GREEN

↓

YELLOW

↓

RED

The states are:

**RED, GREEN, YELLOW**

Each state represents a particular condition of the system.

---

# 6. Present State

The state in which the FSM is **currently operating** is called the **present state**.

Example:

```text id="x7c4p1"
Current State = RED
```

Therefore:

**Present State=RED**

---

# 7. Next State

The state that the FSM will enter after the next clock transition is called the **next state**.

Example:

```text id="m8q3v6"
Present State
```

```
 RED

  ↓
```

Next State

```
GREEN
```

Therefore:

**Present State=RED**

**Next State=GREEN**

---

# 8. State Transition ⭐⭐⭐⭐⭐

A **state transition** is the movement from one state to another based on an input/event.

Example:

```text id="r2y6k4"
        input = 1
```

┌───────────────►

│

┌───────┐       ┌───────┐
│  S0   │       │  S1   │
└───────┘       └───────┘

If input = 1:

**S0→S1**

If input = 0, it may remain in S0, depending on the design.

---

# 9. State Transition Diagram

A **state diagram** is a graphical representation of the states and transitions of an FSM.

### States

Represented using circles:

```text id="k3v8n1"
   ┌─────┐
   │ S0  │
   └─────┘
```

### Transitions

Represented using arrows:

```text id="p6w4m9"
S0 ─────────► S1
```

The arrow may contain the input condition.

---

# 10. State Table ⭐⭐⭐⭐⭐

A state table represents FSM behavior in tabular form.

A typical state table contains:

| Present State | Input | Next State | Output |
| ------------- | ----- | ---------- | ------ |
| S0            | 0     | S0         | 0      |
| S0            | 1     | S1         | 0      |
| S1            | 0     | S0         | 0      |
| S1            | 1     | S1         | 1      |

The exact output relationship depends on whether the FSM is **Moore or Mealy**.

---

# 11. Clock in an FSM ⭐⭐⭐⭐⭐

FSM state transitions normally occur according to a **clock edge**.

For example:

```text id="t9z5q2"
Current State
```

```
  ↓
```

Combinational

```
  Logic

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

Current State

At the active clock edge:

**Current State←Next State**

This is why FSMs are sequential circuits.

---

# 12. FSM Mathematical Representation

An FSM can be represented as:

**FSM=(S,I,O,δ,λ)**

where:

* S = set of states
* I = set of inputs
* O = set of outputs
* δ = state transition function
* λ = output function

For placement interviews, understanding the concepts is more important than memorizing the notation.

---

# 13. Number of Flip-Flops Required ⭐⭐⭐⭐⭐

If an FSM has N states, the minimum number of state bits required is:

**n=⌈log₂N⌉**

### Example

FSM has 4 states:

**2²=4**

Therefore:

**2 flip-flops**

### Example

FSM has 5 states:

**2²=4<5**

**2³=8≥5**

Therefore:

**3 flip-flops**

---

# 14. FSM Example — Simple Door Controller

Suppose a door has two states:

```text id="v6k2r8"
CLOSED
```

OPEN

Input:

```text id="j4p9m3"
X = 1 → Open request
```

X = 0 → No request

State transition:

```text id="c1n5x7"
          X=1

 CLOSED ───────► OPEN

    ▲             │
    │             │ X=0
    └─────────────┘
```

The FSM remembers whether the door is currently **OPEN or CLOSED**.

---

# 15. Why FSM is Important in VLSI ⭐⭐⭐⭐⭐

FSMs are heavily used in digital hardware because many systems require **control logic**.

Examples:

```text id="q8m2v5"
Processor Control
```

```
   ↓
```

Communication Controller

```
   ↓
```

Memory Controller

```
   ↓
```

Protocol Controller

```
   ↓
```

Peripheral Controller

FSMs are therefore a **very important VLSI placement topic**.

---

# 🧠 QUICK REVISION — 7.1

```text id="h5r7k3"
FSM

→ Finite State Machine

→ Sequential system

→ Has finite states

→ Uses memory/state registers


Present State

→ Current state


Next State

→ State after next clock transition


State Transition

→ Movement from one state to another


State Diagram

→ Graphical representation


State Table

→ Tabular representation


State Register

→ Stores current state


Next-State Logic

→ Determines next state


Output Logic

→ Determines output


N states

→ Minimum FFs = ceil(log₂N)


Moore:

→ Output depends on state


Mealy:

→ Output depends on state + input
```
