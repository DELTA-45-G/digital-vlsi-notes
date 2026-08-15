# Placement Interview Questions & Answers

## Boolean Algebra + Logic Gates ⭐⭐⭐⭐⭐

Below is a **placement-focused question bank** from everything covered in Phase 2. I've prioritized questions that commonly appear in **digital electronics/VLSI technical rounds, MCQs, and written tests**.

---

# 🔥 SECTION 1 — Logic Gates

### Q1. What are the basic logic gates?

**Answer:**

The basic gates are:

* AND
* OR
* NOT

NAND, NOR, XOR, and XNOR are also commonly used logic gates.

---

### Q2. What is an AND gate?

**Answer:**

An AND gate produces `1` only when **all inputs are 1**.

```text
Y = AB
```

---

### Q3. What is an OR gate?

**Answer:**

An OR gate produces `1` when **at least one input is 1**.

```text
Y = A+B
```

---

### Q4. What is a NOT gate?

**Answer:**

A NOT gate produces the complement of the input.

```text
Y = A′
```

---

### Q5. What is a NAND gate?

**Answer:**

NAND is the complement of AND.

```text
Y = (AB)′
```

---

### Q6. What is a NOR gate?

**Answer:**

NOR is the complement of OR.

```text
Y = (A+B)′
```

---

### Q7. Why are NAND and NOR called universal gates? ⭐⭐⭐⭐⭐

**Answer:**

Because **any Boolean function can be implemented using only NAND gates or only NOR gates**.

For example, NOT, AND, and OR can all be constructed using only NAND gates.

---

### Q8. How do you implement NOT using NAND?

**Answer:**

Connect both inputs of the NAND gate together.

```text
Y = (AA)′ = A′
```

```text
       ┌─────
A ─────┤
       │ NAND ── Y
A ─────┤
       └─────
```

---

### Q9. How do you implement AND using NAND?

**Answer:**

First NAND the inputs and then invert the result using another NAND.

```text
X = (AB)′
Y = X′ = AB
```

So **2 NAND gates** are required.

---

### Q10. How do you implement OR using NAND? ⭐⭐⭐⭐⭐

Using DeMorgan:

```text
A+B = (A′B′)′
```

So:

1. NAND A with itself → A′
2. NAND B with itself → B′
3. NAND the results → A+B

Therefore, **3 NAND gates**.

---

# 🔥 SECTION 2 — XOR & XNOR

### Q11. When does XOR output 1? ⭐⭐⭐⭐⭐

**Answer:**

XOR outputs `1` when the inputs are **different**.

```text
A⊕B = 1 when A ≠ B
```

---

### Q12. When does XNOR output 1?

**Answer:**

XNOR outputs `1` when the inputs are **same**.

```text
A⊙B = 1 when A = B
```

---

### Q13. What is the difference between OR and XOR? ⭐⭐⭐⭐⭐

| A | B | OR    | XOR   |
| - | - | ----- | ----- |
| 0 | 0 | 0     | 0     |
| 0 | 1 | 1     | 1     |
| 1 | 0 | 1     | 1     |
| 1 | 1 | **1** | **0** |

**Answer:**

OR gives `1` when at least one input is `1`.

XOR gives `1` only when the inputs are different.

---

### Q14. What is the Boolean expression for XOR?

**Answer:**

```text
A⊕B = A′B + AB′
```

---

### Q15. What is the Boolean expression for XNOR?

**Answer:**

```text
A⊙B = AB + A′B′
```

---

### Q16. Which gate is commonly used as an equality detector? ⭐⭐⭐⭐⭐

**Answer:**

**XNOR gate.**

Because XNOR outputs `1` when two inputs are equal.

---

### Q17. What is `A⊕A`?

**Answer:**

```text
0
```

---

### Q18. What is `A⊕0`?

**Answer:**

```text
A
```

---

### Q19. What is `A⊕1`?

**Answer:**

```text
A′
```

---

### Q20. What is `A⊕A′`?

**Answer:**

```text
1
```

---

# 🔥 SECTION 3 — Half Adder

### Q21. What is a half adder? ⭐⭐⭐⭐⭐

**Answer:**

A half adder is a combinational circuit that adds **two 1-bit binary numbers**.

It has:

* 2 inputs: A, B
* 2 outputs: Sum, Carry

```text
Sum = A⊕B
Carry = AB
```

---

### Q22. Which gates are required to implement a half adder?

**Answer:**

* XOR → Sum
* AND → Carry

---

### Q23. What is the difference between Sum and Carry in a half adder?

For:

```text
1+1=10
```

Therefore:

```text
Sum   = 0
Carry = 1
```

---

# 🔥 SECTION 4 — Boolean Algebra

### Q24. What is Boolean algebra?

**Answer:**

Boolean algebra is a mathematical system used to represent and manipulate **binary variables and logic operations**.

Variables can have only:

```text
0 or 1
```

---

### Q25. What is `A+0`?

```text
A
```

Identity law.

---

### Q26. What is `A⋅1`?

```text
A
```

Identity law.

---

### Q27. What is `A+1`?

```text
1
```

Dominance law.

---

### Q28. What is `A⋅0`?

```text
0
```

Dominance law.

---

### Q29. What is `A+A`?

```text
A
```

Idempotent law.

---

### Q30. What is `A⋅A`?

```text
A
```

Idempotent law.

---

### Q31. What is `A+A′`?

```text
1
```

Complement law.

---

### Q32. What is `A⋅A′`?

```text
0
```

Complement law.

---

### Q33. What is `(A′)′`?

```text
A
```

Involution law.

---

# 🔥 SECTION 5 — Boolean Simplification

### Q34. Simplify:

```text
A+AB
```

**Answer:**

```text
A
```

Using absorption law.

---

### Q35. Simplify:

```text
A(A+B)
```

**Answer:**

```text
A
```

---

### Q36. Simplify:

```text
A+AB+AC
```

**Answer:**

Factor A:

```text
A(1+B+C)
```

Since:

```text
1+B+C=1
```

Therefore:

```text
A
```

---

### Q37. Simplify:

```text
AB+AB′
```

**Answer:**

Factor A:

```text
A(B+B′) = A(1)
```

Therefore:

```text
A
```

⭐ This is a very common Boolean simplification question.

---

### Q38. Simplify:

```text
(A+B)(A+B′)
```

**Answer:**

Using:

```text
(X+Y)(X+Z)=X+YZ
```

```text
= (A+BB′)
= A+0
```

Therefore:

```text
A
```

---

# 🔥 SECTION 6 — DeMorgan's Theorem

### Q39. State DeMorgan's theorems. ⭐⭐⭐⭐⭐

**Answer:**

```text
(AB)′ = A′+B′
```

and:

```text
(A+B)′ = A′B′
```

---

### Q40. Simplify:

```text
(AB)′
```

**Answer:**

```text
A′+B′
```

---

### Q41. Simplify:

```text
(A+B)′
```

**Answer:**

```text
A′B′
```

---

### Q42. Simplify:

```text
(ABC)′
```

**Answer:**

```text
A′+B′+C′
```

---

### Q43. Simplify:

```text
(A+B+C)′
```

**Answer:**

```text
A′B′C′
```

---

### Q44. Simplify:

```text
(A+BC)′
```

**Answer:**

First:

```text
(A+BC)′ = A′(BC)′
```

Then:

```text
(BC)′ = B′+C′
```

Therefore:

```text
A′(B′+C′)
```

---

### Q45. What happens to AND and OR under DeMorgan's theorem?

**Answer:**

They interchange:

```text
AND ↔ OR
```

and every variable is complemented.

---

# 🔥 SECTION 7 — SOP & POS

### Q46. What is SOP? ⭐⭐⭐⭐⭐

**Answer:**

SOP stands for **Sum of Products**.

It consists of product terms connected using OR.

Example:

```text
AB+A′C+BC
```

---

### Q47. What is POS?

**Answer:**

POS stands for **Product of Sums**.

It consists of sum terms connected using AND.

Example:

```text
(A+B)(A′+C)
```

---

### Q48. How do you quickly identify SOP vs POS?

**Answer:**

```text
SOP → AND terms + OR
```

```text
POS → OR terms × AND
```

Or:

> **SOP → AND first, OR later**

> **POS → OR first, AND later**

---

### Q49. What is a literal?

**Answer:**

A variable or its complement.

Examples:

```text
A, A′, B, B′
```

---

### Q50. What is a product term?

**Answer:**

Variables/literals connected using AND.

Examples:

```text
AB
A′BC
```

---

### Q51. What is a sum term?

**Answer:**

Variables/literals connected using OR.

Examples:

```text
A+B
A′+B+C
```

---

# 🔥 SECTION 8 — Minterms & Maxterms

### Q52. What is a minterm? ⭐⭐⭐⭐⭐

**Answer:**

A minterm is a **canonical product term** containing every variable exactly once.

Each minterm corresponds to one truth-table row where:

```text
F=1
```

---

### Q53. What is a maxterm?

**Answer:**

A maxterm is a **canonical sum term** containing every variable exactly once.

Each maxterm corresponds to one truth-table row where:

```text
F=0
```

---

### Q54. What is the notation for minterms?

```text
Σm
```

---

### Q55. What is the notation for maxterms?

```text
ΠM
```

---

### Q56. What is the minterm for `ABC=101`?

Binary:

```text
101₂=5
```

Therefore:

```text
m5=AB′C
```

---

### Q57. What is the maxterm for `ABC=101`?

```text
M5=(A′+B+C′)
```

---

### Q58. What is the minterm rule?

**Answer:**

```text
1 → normal variable
0 → complemented variable
```

---

### Q59. What is the maxterm rule?

**Answer:**

```text
1 → complemented variable
0 → normal variable
```

---

# 🔥 SECTION 9 — Truth Table Questions

### Q60. How do you obtain SOP from a truth table? ⭐⭐⭐⭐⭐

**Answer:**

1. Select rows where **F = 1**
2. Convert each row into a minterm
3. OR all minterms

```text
F = Σm(rows where F=1)
```

---

### Q61. How do you obtain POS from a truth table?

**Answer:**

1. Select rows where **F = 0**
2. Convert each row into a maxterm
3. AND all maxterms

```text
F = ΠM(rows where F=0)
```

---

### Q62. If:

```text
F=Σm(1,3,5,7)
```

where is F = 1?

**Answer:**

```text
1,3,5,7
```

---

### Q63. If:

```text
F=Σm(1,3,5,7)
```

what is the equivalent POS representation?

For 3 variables, all possible indices are:

```text
0,1,2,3,4,5,6,7
```

Zeros are:

```text
0,2,4,6
```

Therefore:

```text
F=ΠM(0,2,4,6)
```

⭐ Very common MCQ pattern.

---

# 🔥 SECTION 10 — Placement-Level Conceptual Questions

### Q64. Why is Boolean simplification important in VLSI?

**Answer:**

Simplification can reduce:

* Number of gates
* Transistor count
* Area
* Power consumption
* Propagation delay

---

### Q65. Which gate is commonly used for equality checking?

**XNOR**

---

### Q66. Which gate is commonly used to generate the Sum in a half adder?

**XOR**

---

### Q67. Which gates are universal?

**NAND, NOR**

---

### Q68. Which gate produces 1 when inputs are different?

**XOR**

---

### Q69. Which gate produces 1 when inputs are equal?

**XNOR**

---

### Q70. What is the difference between canonical and non-canonical SOP?

**Answer:**

In canonical SOP, **every product term contains every variable exactly once**.

In ordinary/non-canonical SOP, some terms may not contain all variables.

Example:

```text
AB+A′C
```

is SOP but not canonical SOP if variables are A, B, C.

---

# 🔥 TOP 20 — MUST PREPARE BEFORE A VLSI PLACEMENT

If you don't have time to study all 70, make sure you can answer these immediately:

1. ⭐ What are universal gates?
2. ⭐ Why are NAND/NOR universal?
3. ⭐ NAND implementation of NOT?
4. ⭐ NAND implementation of OR?
5. ⭐ XOR vs OR?
6. ⭐ XOR vs XNOR?
7. ⭐ XNOR application?
8. ⭐ Half adder equations?
9. ⭐ Boolean identity laws?
10. ⭐ Absorption laws?
11. ⭐ DeMorgan's theorems?
12. ⭐ Apply DeMorgan to 3 variables.
13. ⭐ What is SOP?
14. ⭐ What is POS?
15. ⭐ SOP vs POS?
16. ⭐ What is a minterm?
17. ⭐ What is a maxterm?
18. ⭐ Σm vs ΠM?
19. ⭐ Truth table → SOP?
20. ⭐ Truth table → POS?

---

## 🧠 One-Line Master Revision

```text
NAND/NOR → Universal
```

```text
XOR → Different = 1
XNOR → Same = 1
```

### Half Adder:

```text
SUM = XOR
CARRY = AND
```

### DeMorgan:

```text
AND ↔ OR + complement
```

```text
SOP → AND → OR → 1s → Σm
```

```text
POS → OR → AND → 0s → ΠM
```

### Minterm:

```text
1 → normal
0 → complement
```

### Maxterm:

```text
1 → complement
0 → normal
```
