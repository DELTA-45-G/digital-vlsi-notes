# COMPARATOR ⭐⭐⭐⭐⭐

A **digital comparator** is a combinational circuit that compares two binary numbers.

It determines whether:

```text
A>B
A=B
A<B
```

This is a very common topic in digital/VLSI placement tests.

---

# 1. What is a Comparator?

A comparator compares two binary inputs and produces outputs indicating their relationship.

For a **1-bit comparator**:

```text
       A ─────┐
              ▼

          ┌────────────┐

       B ─► COMPARATOR │

          └─────┬──────┘

                │

        ┌───────┼───────┐

        ▼       ▼       ▼

       A>B     A=B     A<B
```

---

# 2. 1-Bit Comparator ⭐⭐⭐⭐⭐

Inputs:

```text
A,B
```

Outputs:

```text
A>B,A=B,A<B
```

Truth table:

| A | B | A>B | A=B | A<B |
| - | - | --- | --- | --- |
| 0 | 0 | 0   | 1   | 0   |
| 0 | 1 | 0   | 0   | 1   |
| 1 | 0 | 1   | 0   | 0   |
| 1 | 1 | 0   | 1   | 0   |

### Important observation:

Exactly **one** of the three outputs is `1`.

---

# 3. Equality Equation ⭐⭐⭐⭐⭐

When are A and B equal?

They are equal when:

```text
A B

0 0

1 1
```

This is exactly the behavior of **XNOR**.

Therefore:

```text
A=B=A⊙B
```

or:

```text
A=B=AB+AB
```

where ⊙ represents XNOR.

### ⭐ Memory trick

> **XOR → different**

> **XNOR → same**

---

# 4. A > B Equation

For one bit:

A>B occurs only when:

```text
A=1,B=0
```

Therefore:

```text
A>B=AB
```

---

# 5. A < B Equation

A<B occurs only when:

```text
A=0,B=1
```

Therefore:

```text
A<B=AB
```

---

# 6. ⭐ 1-Bit Comparator Equations

Memorize these:

```text
A>B=AB
A=B=AB+AB
A<B=AB
```

Or:

```text
A=B=A XNOR B
```

---

# 7. Why XNOR is Important?

XNOR produces `1` when inputs are equal.

```text
A B | XNOR
----------

0 0 |  1

0 1 |  0

1 0 |  0

1 1 |  1
```

Therefore, XNOR is heavily used in:

* Equality comparators
* Digital comparison circuits
* Error detection
* Address comparison
* Control logic

---

# 8. Multi-Bit Comparator ⭐⭐⭐⭐⭐

Now suppose we compare:

```text
A=A3A2A1A0
```

and:

```text
B=B3B2B1B0
```

The **MSB is the most important bit**.

### Example:

```text
A = 1010
```

```text
B = 1001
```

Compare from the MSB:

```text
A3 = 1
```

```text
B3 = 1
```

Equal.

Next:

```text
A2 = 0
```

```text
B2 = 0
```

Equal.

Next:

```text
A1 = 1
```

```text
B1 = 0
```

Here:

```text
1>0
```

Therefore:

```text
A>B
```

We don't need to examine A0 and B0.

---

# 9. ⭐ Most Important Multi-Bit Rule

When comparing binary numbers:

```text
Compare from MSB to LSB
```

The **first unequal bit** determines the result.

### Example:

```text
A=1101
B=1011
```

Compare:

```text
A: 1 1 0 1
B: 1 0 1 1
      ↑
 first difference
```

At the second bit:

```text
1>0
```

Therefore:

```text
A>B
```

---

# 10. Another Example

Compare:

```text
A=0110
B=1010
```

First bit:

```text
0<1
```

Immediately:

```text
A<B
```

No need to check remaining bits.

---

# 11. Equality for Multi-Bit Numbers

Two numbers are equal only if **every corresponding bit is equal**.

For 4 bits:

```text
A=B
```

when:

```text
A3=B3
```

AND

```text
A2=B2
```

AND

```text
A1=B1
```

AND

```text
A0=B0
```

Therefore, equality can be implemented using XNOR gates followed by AND.

```text
A3 ──┐
     XNOR ──┐
B3 ──┘      │
            │
A2 ──┐      │
     XNOR ──┤
B2 ──┘      │
            AND ──► A = B
A1 ──┐      │
     XNOR ──┤
B1 ──┘      │
            │
A0 ──┐      │
     XNOR ──┘
B0 ──┘
```

---

# 12. Cascading Comparators ⭐⭐⭐⭐

Multi-bit comparators can be constructed by cascading smaller comparators.

For example:

```text
4-bit comparison
```

↓

```text
2-bit comparator
```

*

```text
2-bit comparator
```

The higher-order bits get priority.

---

# 13. Comparator vs Subtractor

This is a useful interview distinction.

### Comparator

Determines:

```text
A>B, A=B, A<B
```

### Subtractor

Calculates:

```text
A−B
```

A comparator may internally use subtraction-like logic, but its output is the **relationship**, not necessarily the arithmetic difference.

---

# 14. Real Hardware Applications ⭐⭐⭐⭐

Comparators are used in:

* CPUs
* ALUs
* Address checking
* Digital control systems
* Sorting hardware
* Timers
* ADCs
* Memory systems
* Conditional operations

For example, a processor might need to perform:

```text
if A > B
```

execute operation

The comparator generates the required control signal.

---

# 15. Verilog Relevance ⭐⭐⭐⭐⭐

A simple comparator can be described using operators:

```verilog
assign greater = (A > B);
```

```verilog
assign equal   = (A == B);
```

```verilog
assign less    = (A < B);
```

For hardware-oriented RTL, these operators are synthesizable, and the synthesis tool generates the required comparison logic.

---

# 16. Placement Questions

### Q1. What type of circuit is a comparator?

```text
Combinational circuit
```

---

### Q2. What are the three outputs of a comparator?

```text
A>B, A=B, A<B
```

---

### Q3. Which gate is commonly used for equality comparison?

```text
XNOR
```

---

### Q4. What does XOR indicate?

```text
Inputs are different
```

---

### Q5. What does XNOR indicate?

```text
Inputs are equal
```

---

### Q6. In multi-bit comparison, which bit has highest priority?

```text
MSB
```

---

### Q7. What determines the result in a multi-bit comparison?

```text
First unequal bit from MSB
```

---

# 🧠 COMPARATOR QUICK REVISION

```text
DIGITAL COMPARATOR
```

────────────────────────────

### Purpose:

Compare two binary numbers

### Outputs:

```text
A > B

A = B

A < B
```

### 1-bit equations:

```text
A > B = A·B'
```

```text
A = B = A XNOR B
```

```text
A < B = A'·B
```

### Equality:

```text
XNOR
```

### Multi-bit:

```text
Compare MSB → LSB
```

### First unequal bit:

```text
Determines result
```

### If all bits equal:

```text
A = B
```

### Type:

```text
Combinational circuit
```

### Memory:

```text
XOR  → Different

XNOR → Equal
```
