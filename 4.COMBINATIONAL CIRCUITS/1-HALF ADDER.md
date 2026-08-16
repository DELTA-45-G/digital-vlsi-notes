# HALF ADDER ⭐⭐⭐⭐⭐

## 1. What is a Half Adder?

A **Half Adder** is a combinational circuit that adds **two 1-bit binary numbers**.

It has:

### Inputs

```text
A, B
```

### Outputs

```text
Sum, Carry
```

---

## 2. Why is it called "Half" Adder?

Because it adds only **two input bits**.

It does **not have a carry input** from a previous stage.

```text
       A ─────┐
              │
              ▼

          ┌─────────┐

       B ─► HALF    │

          │ ADDER   │

          └─────────┘

              │

          ┌───┴───┐

          ▼       ▼

         Sum     Carry
```

### ⭐ Important

A Half Adder:

```text
No Carry-in
```

A Full Adder:

```text
Has Carry-in
```

This difference is extremely important in interviews.

---

# 3. Binary Addition

Before understanding the circuit, remember the four possible cases.

| A | B | A + B | Sum | Carry |
| - | - | ----: | --: | ----: |
| 0 | 0 |     0 |   0 |     0 |
| 0 | 1 |     1 |   1 |     0 |
| 1 | 0 |     1 |   1 |     0 |
| 1 | 1 |    10 |   0 |     1 |

The last case is the important one:

```text
1+1=10₂
```

Therefore:

* Sum = `0`
* Carry = `1`

---

# 4. Half Adder Truth Table ⭐⭐⭐⭐⭐

```text
 A   B   |   Sum   Carry
---------|----------------
 0   0   |    0      0

 0   1   |    1      0

 1   0   |    1      0

 1   1   |    0      1
```

Look carefully at the **Sum** column:

```text
0 1 1 0
```

That's exactly the XOR truth table.

Therefore:

```text
Sum = A⊕B
```

---

# 5. Carry Equation ⭐⭐⭐⭐⭐

Look at the Carry column:

```text
0 0 0 1
```

That's the AND truth table.

Therefore:

```text
Carry = A⋅B
```

So the two most important Half Adder equations are:

```text
Sum = A⊕B
Carry = AB
```

🔥 **Memorize these.**

---

# 6. Half Adder Circuit

A Half Adder can be constructed using:

* 1 XOR gate
* 1 AND gate

```text
             ┌─────────┐

A ──────────►│   XOR   │──── Sum

             └─────────┘

       │

       │

       │     ┌─────────┐

       └────►│   AND   │──── Carry

B ──────────►│         │

             └─────────┘
```

Both inputs go to both gates.

---

# 7. Boolean Expressions

### Sum

```text
A⊕B
```

Using basic gates:

```text
Sum = A′B+AB′
```

### Carry

```text
Carry = AB
```

Therefore:

```text
HA = (A⊕B, AB)
```

---

# 8. Why XOR for Sum? ⭐⭐⭐⭐⭐

XOR gives `1` when the two inputs are **different**.

```text
A B | XOR
---------
0 0 |  0

0 1 |  1

1 0 |  1

1 1 |  0
```

For addition:

```text
0 + 0 = 0

0 + 1 = 1

1 + 0 = 1

1 + 1 = 10
```

So XOR naturally produces the Sum bit.

---

# 9. Why AND for Carry?

Carry occurs **only when both inputs are 1**.

```text
A B
```

```text
0 0 → Carry 0

0 1 → Carry 0

1 0 → Carry 0

1 1 → Carry 1
```

That's exactly:

```text
AB
```

Therefore:

```text
Carry = AND
```

---

# 10. ⭐ Most Important Interview Concept

### Half Adder:

```text
Sum = XOR
Carry = AND
```

### Memory trick 🧠

> **XOR gives Sum, AND gives Carry.**

This is one of the most frequently asked basic digital-electronics questions.

---

# 11. Hardware Example

Suppose you have two switches representing binary values:

```text
A = 1
```

```text
B = 1
```

The Half Adder performs:

```text
1+1=10
```

Therefore:

```text
Sum   = 0
```

```text
Carry = 1
```

The Carry would then be passed to the next higher-order bit in a larger adder.

**But:** a Half Adder itself cannot accept that incoming carry.

---

# 12. Half Adder vs Full Adder ⭐⭐⭐⭐⭐

This is a very common placement question.

| Feature      | Half Adder | Full Adder |
| ------------ | ---------- | ---------- |
| Inputs       | 2          | 3          |
| Inputs       | A, B       | A, B, Cin  |
| Carry input  | ❌ No       | ✅ Yes      |
| Sum output   | ✅          | ✅          |
| Carry output | ✅          | ✅          |

### Remember:

```text
HA: 2 inputs
FA: 3 inputs
```

---

# 13. Limitation of Half Adder ⭐⭐⭐⭐⭐

The Half Adder cannot add:

```text
A+B+Cin
```

because it has no Carry-in input.

For example, in multi-bit addition:

```text
       1  ← carry from previous bit

       ↓

      A B
```

The Half Adder has no input to accept that carry.

Therefore, we need a:

```text
Full Adder
```

---

# 14. Half Adder Using Only NAND Gates

Since NAND is a universal gate, a Half Adder can also be implemented using only NAND gates.

This is useful for VLSI interviews because **NAND/NOR are universal gates**.

But for now, remember the standard implementation:

```text
1 XOR + 1 AND
```

We'll discuss gate-level implementations later.

---

# 15. Verilog Relevance ⭐⭐⭐⭐

A Half Adder can be written very simply in Verilog.

```verilog
module half_adder(
    input  A,
    input  B,
    output Sum,
    output Carry
);

assign Sum   = A ^ B;
assign Carry = A & B;

endmodule
```

Notice:

```text
^ → XOR
```

```text
& → AND
```

Therefore:

```text
Sum   = A ^ B
```

```text
Carry = A & B
```

This is exactly the hardware equation.

---

# 16. Placement Questions You Should Know

### Q: How many inputs does a Half Adder have?

```text
2
```

### Q: How many outputs?

```text
2
```

### Q: Sum equation?

```text
A⊕B
```

### Q: Carry equation?

```text
AB
```

### Q: Which gates are required?

```text
XOR + AND
```

### Q: Does Half Adder have Carry-in?

```text
No
```

---

# 🧠 HALF ADDER — QUICK REVISION

```text
HALF ADDER
```

────────────────────────

### Inputs:

```text
A, B
```

### Outputs:

```text
Sum, Carry
```

### Sum:

```text
A ⊕ B
```

### Carry:

```text
A · B
```

### Implementation:

```text
1 XOR + 1 AND
```

### Truth table:

```text
A B | S C
---------
0 0 | 0 0

0 1 | 1 0

1 0 | 1 0

1 1 | 0 1
```

### Important:

```text
No Carry-in
```

### Memory:

```text
XOR → Sum
AND → Carry
```
