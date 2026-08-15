# XOR & XNOR Gates ⭐⭐⭐⭐

These two gates are extremely important because they appear frequently in:

* Adders
* Comparators
* Error detection
* Parity circuits
* ALUs
* Digital VLSI interviews

---

# 1. XOR Gate

XOR = **Exclusive OR**

The output is `1` when the inputs are **different**.

### Symbolic expression

```text
Y = A⊕B
```

---

# 2. XOR Truth Table ⭐⭐⭐

| A | B | XOR   |
| - | - | ----- |
| 0 | 0 | **0** |
| 0 | 1 | **1** |
| 1 | 0 | **1** |
| 1 | 1 | **0** |

### Memory trick ⭐

> **XOR = Inputs are DIFFERENT → 1**

```text
Different → 1
Same      → 0
```

---

# 3. XOR vs OR

This is a very common placement trap.

### OR

Output is `1` when **at least one input is 1**.

```text
0 OR 0 = 0
0 OR 1 = 1
1 OR 0 = 1
1 OR 1 = 1
```

### XOR

Output is `1` when **exactly one input is 1**.

```text
0 XOR 0 = 0
0 XOR 1 = 1
1 XOR 0 = 1
1 XOR 1 = 0
```

### Key difference ⭐⭐⭐⭐⭐

| A | B | OR    | XOR   |
| - | - | ----- | ----- |
| 0 | 0 | 0     | 0     |
| 0 | 1 | 1     | 1     |
| 1 | 0 | 1     | 1     |
| 1 | 1 | **1** | **0** |

Therefore:

> **OR allows both inputs to be 1. XOR does not.**

---

# 4. XOR Boolean Expression

XOR can be written using AND, OR and NOT:

```text
A⊕B = AB + AB
```

Read it as:

> A is 0 and B is 1 **OR** A is 1 and B is 0.

That's exactly the condition where the inputs are different.

---

# 5. Real-Life Intuition

Imagine a staircase light controlled by **two switches**.

The light is ON when the switch positions are different.

| Switch A | Switch B | Light |
| -------: | -------: | ----: |
|        0 |        0 |     0 |
|        0 |        1 |     1 |
|        1 |        0 |     1 |
|        1 |        1 |     0 |

That's XOR behavior.

---

# 6. XOR in a Half Adder ⭐⭐⭐⭐⭐

This is extremely important.

A half adder adds two binary bits.

```text
A ───┐
     ├── XOR ── SUM
B ───┘
```

```text
A ───┐
     ├── AND ── CARRY
B ───┘
```

Therefore:

```text
SUM   = A⊕B
CARRY = A⋅B
```

### Memorize this ⭐⭐⭐⭐⭐

> **Half Adder = XOR + AND**

You will use this again in **Phase 4**.

---

# 7. XNOR Gate

XNOR = **Exclusive NOR**

It is the **opposite of XOR**.

```text
Y = A⊕B
```

The output is `1` when the inputs are **the same**.

---

# 8. XNOR Truth Table ⭐⭐⭐

| A | B | XOR | XNOR  |
| - | - | --- | ----- |
| 0 | 0 | 0   | **1** |
| 0 | 1 | 1   | **0** |
| 1 | 0 | 1   | **0** |
| 1 | 1 | 0   | **1** |

### Memory trick

**XNOR = Same → 1**

```text
Same      → 1
Different → 0
```

---

# 9. XNOR as an Equality Detector ⭐⭐⭐⭐⭐

This is one of the most important applications.

If:

```text
A = 0
```

```text
B = 0
```

XNOR = 1.

If:

```text
A = 1
```

```text
B = 1
```

XNOR = 1.

Therefore:

```text
XNOR = 1 when A = B
```

So XNOR can be used as a **1-bit equality comparator**.

---

# 10. XOR and XNOR Relationship ⭐⭐⭐⭐⭐

They are complements:

```text
XNOR = XOR
```

and:

```text
XOR = XNOR
```

---

# 11. Important Applications

### XOR ⭐⭐⭐⭐⭐

Used in:

* Half adder
* Full adder
* Parity generator
* Parity checker
* Controlled inversion
* ALU circuits

### XNOR ⭐⭐⭐⭐⭐

Used in:

* Equality comparator
* Bit comparison
* Digital comparison circuits

---

# 12. XOR as Controlled Inverter ⭐⭐⭐⭐

Consider:

```text
Y = A⊕B
```

If `B = 0`:

```text
A⊕0 = A
```

So output is unchanged.

If `B = 1`:

```text
A⊕1 = A
```

So XOR can either:

* Pass A unchanged
* Invert A

depending on the control input.

This is called **controlled inversion**.

---

# 13. Important XOR Properties ⭐⭐⭐⭐⭐

These are useful later for Boolean simplification.

### Property 1

```text
A⊕0 = A
```

### Property 2

```text
A⊕1 = A
```

### Property 3

```text
A⊕A = 0
```

### Property 4

```text
A⊕A = 1
```

### Property 5 — Commutative

```text
A⊕B = B⊕A
```

---

# 14. XOR Multiple Inputs ⭐⭐⭐

For multiple inputs, XOR outputs `1` when the number of `1`s is **odd**.

Example:

```text
A B C
1 0 0
```

Number of 1s = 1 → XOR = 1.

Another:

```text
1 1 1
```

Number of 1s = 3 → XOR = 1.

But:

```text
1 1 0
```

Number of 1s = 2 → XOR = 0.

### Memory trick ⭐

> **XOR = Odd number of 1s → 1**

This is very useful for **parity**.

---

# 15. XNOR Multiple Inputs

XNOR is associated with **even parity**.

For multiple inputs:

> Even number of 1s → XNOR = 1

Conceptually:

```text
Number of 1s

Odd  → XOR = 1

Even → XNOR = 1
```

---

# 16. Placement Questions ⭐⭐⭐⭐⭐

### Q1. When does XOR output 1?

**When the inputs are different.**

---

### Q2. When does XNOR output 1?

**When the inputs are the same.**

---

### Q3. Which gate is used as an equality detector?

**XNOR.**

---

### Q4. Which gate is used in the sum output of a half adder?

**XOR.**

---

### Q5. What are the half-adder gates?

**XOR for Sum + AND for Carry.**

---

### Q6. What is `A XOR A`?

```text
0
```

---

### Q7. What is `A XOR 0`?

```text
A
```

---

### Q8. What is `A XOR 1`?

```text
A
```

---

# 17. Common Mistakes ❌

### Mistake 1

Thinking XOR and OR are the same.

❌ They differ when:

```text
A = 1
B = 1
```

OR = 1

XOR = 0

---

### Mistake 2

Confusing XOR and XNOR.

Remember:

```text
XOR  → Different → 1
```

```text
XNOR → Same → 1
```

---

### Mistake 3

Forgetting the half-adder relationship.

⭐ **SUM = XOR**

⭐ **CARRY = AND**

---

# 18. Quick Revision ⭐⭐⭐⭐⭐

```text
XOR = Exclusive OR
```

```text
A XOR B = 1 when A ≠ B
```

```text
XNOR = NOT XOR
```

```text
A XNOR B = 1 when A = B
```

### Important equations

```text
A⊕B = AB + AB
XNOR = A⊕B
```

### Half Adder

```text
SUM = A⊕B
CARRY = AB
```

### XOR shortcuts

```text
A⊕0 = A
A⊕1 = A
A⊕A = 0
A⊕A = 1
```

---

# ⭐ VLSI PLACEMENT PRIORITY

Memorize these **5 points**:

1. ⭐⭐⭐⭐⭐ **XOR = different inputs → 1**
2. ⭐⭐⭐⭐⭐ **XNOR = same inputs → 1**
3. ⭐⭐⭐⭐⭐ **XNOR is used for equality comparison**
4. ⭐⭐⭐⭐⭐ **Half Adder: XOR = Sum, AND = Carry**
5. ⭐⭐⭐⭐ **XOR of multiple bits relates to parity**
