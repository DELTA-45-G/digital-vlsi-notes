# Logic Levels & Digital Signals ⭐⭐⭐

We are starting **Phase 2 from absolute zero**.

Before learning AND, OR, NAND, etc., you need to understand **what 0 and 1 actually mean in physical hardware**.

---

# 1. What is a Digital Signal?

A **digital signal** represents information using a limited number of discrete levels.

The most common digital system uses:

* **0 → LOW**
* **1 → HIGH**

So instead of continuously varying values, digital circuits work mainly with two logical states.

```text
Digital logic
```

```text
HIGH  ───────────  1

LOW   ───────────  0
```

⭐ **Important:** `0` and `1` are **logic values**, not necessarily exactly `0 V` and `5 V`.

---

# 2. Why Do We Use 0 and 1?

Digital circuits need a reliable way to represent information.

For example:

```text
0 → OFF
```

`1 → ON`

A computer can represent:

```text
Numbers
```

Characters

Images

Instructions

Sensor data

using combinations of 0s and 1s.

For example:

```text
101101
```

is simply a sequence of digital bits.

---

# 3. What is a Bit? ⭐⭐⭐

**Bit = Binary Digit**

A bit can have one of two logical values:

```text
0
```

`1`

Examples:

```text
1 bit  → 0 or 1
```

```text
2 bits → 00
          01
          10
          11
```

With `n` bits:

```text
2ⁿ possible combinations
```

For example:

```text
3 bits → 2³ = 8 combinations
```

They are:

```text
000
```

```text
001

010

011

100

101

110

111
```

This connects directly to what you learned in **Phase 1**.

---

# 4. What Does Logic 0 Physically Mean? ⭐⭐⭐

Here's an important VLSI concept.

A digital circuit works with **voltages**.

For example, imagine a particular technology where:

```text
LOW voltage  → Logic 0
```

```text
HIGH voltage → Logic 1
```

Conceptually:

```text
Voltage
```

```text
HIGH ───────────────  Logic 1

       |

       |

       |

LOW  ───────────────  Logic 0
```

But there is usually a **range of acceptable voltages**, not one exact voltage.

---

# 5. Important: Logic 0 ≠ Always 0 V ⭐⭐⭐⭐⭐

This is a common interview trap.

You might think:

> Logic 0 = exactly 0 V
> Logic 1 = exactly 5 V

❌ Not necessarily.

The actual voltage ranges depend on the **logic family and technology**.

For example, in a simplified digital system:

```text
0 V ─────────────── LOW
```

```text
        undefined/
        
        transition region
```

```text
VDD ─────────────── HIGH
```

In modern CMOS VLSI, the supply voltage may be much lower than 5 V.

For example:

* 5 V logic
* 3.3 V logic
* 1.8 V logic
* ~1 V-class modern CMOS

So:

```text
Logic level depends on the technology
```

---

# 6. What is VDD? ⭐⭐⭐

You will see **VDD** everywhere in VLSI.

### VDD = positive supply voltage

Conceptually:

```text
       VDD
```

```text
        |

        |

     Digital

     Circuit

        |

       GND
```

`VDD` provides the positive supply.

`GND` represents the reference/ground level.

---

# 7. Logic HIGH and LOW

In a simplified CMOS circuit:

```text
VDD  → HIGH → 1
```

```text
GND  → LOW  → 0
```

But remember:

**This is the conceptual model.**

Actual input/output voltage specifications define valid HIGH and LOW ranges.

---

# 8. Noise Margin ⭐⭐⭐⭐⭐

This is an important **VLSI interview concept**.

Suppose one circuit sends a logic `1` to another circuit.

The receiving circuit must be able to recognize it as `1` even if some unwanted noise is added.

That's where **noise margin** becomes important.

---

# 9. What is Noise?

Noise is an unwanted electrical disturbance that can change or disturb a signal.

Imagine:

```text
Expected:
```

```text
HIGH ─────────────────────
```

```text
Actual:
```

```text
HIGH ────────╲╱──╲───────
```

The signal may fluctuate because of:

* Crosstalk
* Power supply noise
* Electromagnetic interference
* Switching activity

A good digital circuit should tolerate some amount of noise.

---

# 10. Noise Margin — Basic Intuition ⭐⭐⭐⭐⭐

Noise margin tells us roughly:

> **How much unwanted voltage disturbance can be tolerated before a logic value may be interpreted incorrectly.**

For now, remember the intuition.

We will study the exact formulas later in **Phase 10: Digital VLSI**.

---

# 11. Logic Gates ⭐⭐⭐⭐⭐

Now we are ready to introduce **logic gates**.

A logic gate is a digital circuit that performs a logical operation on one or more inputs and produces an output.

Example:

```text
A ────┐
      │ AND ─── Y
B ────┘
```

Inputs:

`A, B`

Output:

`Y`

---

# 12. Why Are Logic Gates Important?

Every digital circuit is constructed from combinations of logic gates.

For example:

```text
Logic gates
```

```text
     ↓

Adders

     ↓

ALU

     ↓

Processor
```

And:

```text
Logic gates
```

```text
     ↓

Flip-flops

     ↓

Registers

     ↓

FSM

     ↓

Digital system
```

So gates are the **building blocks of digital electronics**.

---

# 13. Types of Gates We Will Learn

### Basic gates ⭐⭐⭐

* NOT
* AND
* OR

### Universal gates ⭐⭐⭐⭐⭐

* NAND
* NOR

### Exclusive gates ⭐⭐⭐

* XOR
* XNOR

These gates are extremely important for VLSI placements.

---

# 14. NOT Gate ⭐⭐⭐

The NOT gate has **one input and one output**.

```text
A ─── NOT ─── Y
```

Its job is to **invert** the input.

```text
A = 0 → Y = 1
```

```text
A = 1 → Y = 0
```

Therefore:

```text
Y = A̅
```

---

# 15. NOT Gate Truth Table

| A | Y = NOT A |
| - | --------- |
| 0 | 1         |
| 1 | 0         |

### Memory trick

**NOT = Opposite**

---

# 16. AND Gate ⭐⭐⭐

The AND gate has two or more inputs.

For two inputs:

```text
A ───┐
     │ AND ─── Y
B ───┘
```

The output is `1` **only when ALL inputs are 1**.

```text
Y = A⋅B
```

---

# 17. AND Truth Table

| A | B | Y = A·B |
| - | - | ------- |
| 0 | 0 | 0       |
| 0 | 1 | 0       |
| 1 | 0 | 0       |
| 1 | 1 | **1**   |

### Memory trick ⭐

## AND = ALL must be 1

Think:

> "Everyone must agree."

---

# 18. Real-Life Example

Imagine two switches connected in series:

```text
Battery
```

```text
  |

Switch A

  |

Switch B

  |

Bulb

  |

GND
```

The bulb turns ON only when:

```text
A = ON
```

AND

`B = ON`

That's AND behavior.

---

# 19. OR Gate ⭐⭐⭐

The OR gate produces `1` when **at least one input is 1**.

```text
A ───┐
     │ OR ─── Y
B ───┘
```

```text
Y = A+B
```

⚠️ In Boolean algebra, `+` means **OR**, not normal arithmetic addition.

---

# 20. OR Truth Table

| A | B | Y = A+B |
| - | - | ------- |
| 0 | 0 | 0       |
| 0 | 1 | **1**   |
| 1 | 0 | **1**   |
| 1 | 1 | **1**   |

### Memory trick ⭐

## OR = At least one

---

# 21. Real-Life Example

Imagine two switches connected in parallel:

```text
       ┌── Switch A ──┐
```

```text
Battery┤              ├── Bulb
```

```text
       └── Switch B ──┘
```

If **either switch** is ON, the bulb can turn ON.

That's OR behavior.

---

# 22. AND vs OR — Very Important ⭐⭐⭐⭐⭐

| Condition | AND | OR |
| --------- | --: | -: |
| 0,0       |   0 |  0 |
| 0,1       |   0 |  1 |
| 1,0       |   0 |  1 |
| 1,1       |   1 |  1 |

### Memory trick

**AND → all**

**OR → at least one**

---

# 23. Boolean Symbols You Must Know

### NOT

```text
A̅
```

### AND

```text
A⋅B
```

### OR

```text
A+B
```

For example:

```text
Y=A⋅B+C
```

means:

1. AND `A` and `B`
2. OR that result with `C`

---

# 24. Operator Priority ⭐⭐⭐

When evaluating a Boolean expression:

### Priority

**NOT**

↓

**AND**

↓

**OR**

So:

```text
Y=A̅⋅B+C
```

means:

1. NOT A
2. AND with B
3. OR with C

This becomes very important when solving Boolean expressions and K-maps.

---

# 25. Placement Interview Questions ⭐⭐⭐

### Q1. What is a logic gate?

A digital circuit that performs a logical operation on one or more inputs to produce an output.

### Q2. Which gate gives 1 only when all inputs are 1?

**AND gate.**

### Q3. Which gate gives 1 when at least one input is 1?

**OR gate.**

### Q4. Which gate has only one input?

**NOT gate.**

### Q5. What is the Boolean expression for an AND gate?

```text
Y=A⋅B
```

### Q6. What is the Boolean expression for an OR gate?

```text
Y=A+B
```

---

# 26. Common Mistakes ❌

### Mistake 1

Thinking:

`A + B`

means normal arithmetic addition.

In Boolean algebra:

```text
A+B=OR
```

---

### Mistake 2

Thinking AND produces 1 whenever one input is 1.

❌ Wrong.

AND requires **all inputs = 1**.

---

### Mistake 3

Thinking OR requires both inputs to be 1.

❌ Wrong.

OR requires **at least one input = 1**.

---

### Mistake 4

Thinking logic 1 always means exactly 5 V.

❌ Wrong.

Logic levels depend on the technology.

---

# 27. ⭐ VLSI Connection

At transistor level, logic gates are built using **MOSFETs**.

For example, CMOS technology uses:

* PMOS
* NMOS

to construct logic gates.

Conceptually:

```text
Boolean logic
```

```text
      ↓

Logic gates

      ↓

CMOS transistor networks

      ↓

Digital circuits

      ↓

Processors / SoCs
```

We'll study the actual **CMOS implementation** much later in Phase 10.

---

# 28. Quick Revision — Subtopic 1 ⭐⭐⭐

```text
Bit = Binary Digit
```

```text
0 = LOW

1 = HIGH
```

```text
Logic 0/1 are voltage ranges, not necessarily
exactly 0V/5V.
```

```text
VDD = positive supply

GND = reference/ground
```

```text
Logic gate = basic digital building block
```

### NOT

```text
Y = A̅

0 → 1

1 → 0
```

### AND

```text
Y = A·B

ALL inputs must be 1
```

### OR

```text
Y = A+B

AT LEAST ONE input must be 1
```

### Boolean priority

**NOT → AND → OR**

---

# ⭐ VLSI PLACEMENT PRIORITY

For this subtopic, remember these **5 points**:

1. ⭐ **Logic 0/1 represent voltage ranges**
2. ⭐ **AND → all inputs must be 1**
3. ⭐ **OR → at least one input must be 1**
4. ⭐ **NOT → inversion**
5. ⭐ **Boolean priority = NOT → AND → OR**
