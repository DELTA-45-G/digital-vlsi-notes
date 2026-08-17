# 5.1 — What is Sequential Logic?

Before learning latches and flip-flops, you need to understand one fundamental difference:

### Combinational Logic

Output depends only on **current inputs**.

```text id="4m2p8t"
Y=f(X)
```

Example:

```text id="0m3k7p"
A ──┐
    ├──► AND ──► Y
B ──┘
```

If A or B changes, Y changes according to the current inputs.

There is **no memory**.

---

# Sequential Logic ⭐⭐⭐⭐⭐

A sequential circuit's output depends on:

1. Current inputs
2. Previous state

```text id="2c7v9m"
Output=f(Current Inputs, Previous State)
```

### Simple idea

Imagine a circuit that needs to **remember** whether something happened previously.

```text id="7p4k2x"
Input ──► Sequential Circuit ──► Output
```

```text id="5n8q1r"
                    ▲
                    │
                Previous state
```

That ability to remember is called **memory**.

---

# 5.1.1 Why Do We Need Sequential Logic?

Consider a traffic-light controller.

It might have states:

```text id="9v2c6m"
RED → GREEN → YELLOW → RED
```

The next state depends on the **current state**.

If the circuit has no memory, it cannot know:

> "What state was I in previously?"

Therefore, we need sequential logic.

### Real hardware examples ⭐

Sequential circuits are used in:

* Counters
* Registers
* CPU control units
* State machines
* Memory
* Communication interfaces
* Digital clocks
* UART/SPI/I²C controllers

---

# 5.1.2 The Basic Building Block: Memory

The fundamental idea is:

> **A sequential circuit must somehow store a state.**

The two fundamental storage elements we will study are:

```text id="4s9m2k"
Latch
```

and

```text id="8x3q7v"
Flip-Flop
```

---

# 5.1.3 Latch vs Flip-Flop — The Core Idea ⭐⭐⭐⭐⭐

This distinction is **extremely important in VLSI interviews**.

### Latch

A latch is generally **level-sensitive**.

It can respond to input while its enable/control signal is active.

Think:

> **"The door is open for a period of time."**

```text id="1k8p5z"
Enable = 1
```

───────────────

Input can affect output

---

### Flip-Flop

A flip-flop is generally **edge-triggered**.

It captures the input at a particular clock edge.

For example:

```text id="6q2m8v"
        ↑
```

```text id="r4z7k1"
Clock ──┘

        Capture!
```

It may trigger on:

* Rising edge ↑
* Falling edge ↓

Think:

> **"Take a photograph at one exact instant."**

---

# ⭐ Best Memory Trick

### Latch:

```text
Level sensitive
```

**Think:** Door stays open.

### Flip-Flop:

```text
Edge sensitive
```

**Think:** Camera takes one snapshot.

---

# 5.1.4 Level Sensitive vs Edge Sensitive

### Level Sensitive

The circuit can respond throughout a particular clock/control **level**.

For example:

```text id="z3m6p8"
Enable
```

┌────────────┐

───┘            └────

<------------>

```
  Active
```

During the active period, the latch can be transparent.

---

### Edge Sensitive

The circuit responds only around an edge:

```text id="j5k2n9"
Clock
```

───────┐

```
   │

   ↑

 Capture
```

The flip-flop captures data at that edge.

---

# 5.1.5 Transparent Latch ⭐⭐⭐⭐

Suppose we have a D latch.

```text id="w7m3q5"
       ┌─────────┐
D ────►│ D Latch │────► Q
       │         │
EN ───►│         │
       └─────────┘
```

When:

```text id="c9p4x2"
EN=1
```

the latch is **transparent**.

That means:

```text id="k2v8m5"
Q≈D
```

while enable is active.

When:

```text id="n6q1z4"
EN=0
```

the latch holds its previous value.

```text id="u4m7p2"
Q=Qprevious
```

---

# Example

Suppose:

```text id="d8x2m5"
EN = 1
```

D = 0

Then:

```text id="q3v7n1"
Q=0
```

If D changes:

```text id="a9m4k6"
D: 0 → 1
```

while:

```text id="r2x8p5"
EN=1
```

then Q can also change:

```text id="h7m3q9"
Q: 0 → 1
```

But once:

```text id="c4n8v1"
EN=0
```

the latch stops tracking D and holds its value.

---

# 5.1.6 Flip-Flop Example

Consider a positive-edge-triggered D flip-flop:

```text id="x5m2q8"
          ┌─────────┐
D ───────►│ D       │────► Q
          │   FF    │
CLK ──↑──►│         │
          └─────────┘
```

The important point:

> Q changes based on D at the **active clock edge**.

Suppose:

```text id="q9v3m6"
D=1
```

at the rising edge.

Then:

```text id="k4p7x2"
Q←1
```

If D changes immediately after that edge, Q does **not** immediately follow D.

It waits for the next active edge.

---

# ⭐ Latch vs Flip-Flop

| Feature        | Latch                           | Flip-Flop                      |
| -------------- | ------------------------------- | ------------------------------ |
| Sensitivity    | Level                           | Edge                           |
| Control        | Enable                          | Clock                          |
| Data capture   | During active level             | At clock edge                  |
| Basic behavior | Transparent during active level | Samples at edge                |
| Timing         | More timing-sensitive           | Easier synchronous design      |
| Common use     | Specialized/storage structures  | Registers, pipelines, counters |

### Placement answer:

> **A latch is level-sensitive, while a flip-flop is edge-triggered.**

Memorize this sentence. ⭐⭐⭐⭐⭐

---

# 5.1.7 Why Are Flip-Flops Important in VLSI?

Flip-flops are fundamental storage elements in synchronous digital systems.

For example, a register:

```text id="m7q2x5"
D0 ─► FF ─► Q0
D1 ─► FF ─► Q1
D2 ─► FF ─► Q2
D3 ─► FF ─► Q3

          ▲
          │
        Common
         Clock
```

Four flip-flops can store:

```text id="p4n8v2"
4 bits
```

This concept becomes important when we study **registers and counters in Phase 6**.

---

# 5.1.8 ⭐ Why Does the Clock Matter?

A clock provides a common timing reference.

```text id="x8m4q1"
CLK

    ↑       ↑       ↑

────┘───────┘───────┘

    │       │       │

    ▼       ▼       ▼

  Capture Capture Capture
```

This allows different parts of a digital system to operate in a coordinated manner.

This is why most modern processors and digital ICs use **synchronous design**.

---

# 5.1.9 Important Terminology

### State

The stored information of a sequential circuit.

### Clock

A periodic signal used to coordinate state changes.

### Enable

A control signal that determines whether a storage element is active.

### Edge

A transition of a clock signal.

Rising edge:

```text id="t5n2x9"
0→1
```

Falling edge:

```text id="z7m4q3"
1→0
```

---

# ⭐ Placement Interview Questions

### Q1. What is a sequential circuit?

A circuit whose output depends on the **present input and previous state**.

---

### Q2. Does a sequential circuit have memory?

Yes

---

### Q3. What is the basic difference between combinational and sequential logic?

```text
Combinational: no memory
```

```text
Sequential: memory/state
```

---

### Q4. What is a latch?

A **level-sensitive storage element**.

---

### Q5. What is a flip-flop?

An **edge-triggered storage element**.

---

### Q6. Which is level-sensitive: latch or flip-flop?

Latch

---

### Q7. Which is edge-sensitive?

Flip−flop

---

### Q8. What is a positive edge?

```text id="q3m7n1"
0→1
```

---

### Q9. What is a negative edge?

```text id="k5x8p2"
1→0
```

---

### Q10. Why are flip-flops used in registers?

Because they can store individual bits synchronously with a clock.

---

# ⭐ Quick Placement Shortcut

Whenever you see:

**"Level-sensitive"**

immediately think:

```text id="n2v6m8"
LATCH
```

Whenever you see:

**"Edge-triggered"**

think:

```text id="p7q4x1"
FLIP-FLOP
```

---

# 🧠 QUICK REVISION

```text id="y6m3q8"
SEQUENTIAL LOGIC
```

────────────────────────────

### Output depends on:

Current input + Previous state

### Sequential logic:

✓ Has memory

✓ Stores state

✓ Often uses clock

### Basic storage elements:

1. Latch
2. Flip-Flop

### LATCH:

✓ Level-sensitive

✓ Transparent during active level

✓ Controlled by Enable

### FLIP-FLOP:

✓ Edge-triggered

✓ Captures data at clock edge

✓ Used extensively in registers

### Clock edges:

```text id="m4x8q2"
Rising  = 0 → 1

Falling = 1 → 0
```

### MEMORY TRICK:

```text id="z7n3p5"
Latch     → Level

Flip-Flop → Edge
```
