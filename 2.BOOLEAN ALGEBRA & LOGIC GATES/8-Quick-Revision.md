# PHASE 2 — QUICK REVISION NOTES

## Boolean Algebra & Logic Gates ⭐⭐⭐⭐⭐

> **Goal:** Use these notes for a quick revision before placements or before starting K-Maps.

---

# 1. Logic Gates ⭐⭐⭐⭐⭐

### NOT

```text
Y = A̅
```

| A | Y |
| - | - |
| 0 | 1 |
| 1 | 0 |

**Memory:** NOT → reverses the input.

---

### AND

```text
Y = A⋅B
```

Output = `1` **only when all inputs are 1**.

```text
00 → 0
01 → 0
10 → 0
11 → 1
```

**Memory:** AND = **All 1 → 1**

---

### OR

```text
Y = A+B
```

Output = `1` when **at least one input is 1**.

```text
00 → 0
01 → 1
10 → 1
11 → 1
```

**Memory:** OR = **Any 1 → 1**

---

# 2. Universal Gates ⭐⭐⭐⭐⭐

## NAND

```text
Y = (AB)̅
```

NAND = **NOT + AND**

NAND alone can implement:

* NOT
* AND
* OR
* Any Boolean function

---

## NOR

```text
Y = (A+B)̅
```

NOR = **NOT + OR**

NOR alone can implement:

* NOT
* AND
* OR
* Any Boolean function

### ⭐ Placement key

> **NAND and NOR are universal gates.**

---

# 3. XOR ⭐⭐⭐⭐⭐

```text
Y = A⊕B
```

Output = `1` when inputs are **different**.

```text
00 → 0
01 → 1
10 → 1
11 → 0
```

### Important formula

```text
A⊕B = A′B + AB′
```

### Memory:

> **XOR → Different = 1**

---

# 4. XNOR ⭐⭐⭐⭐⭐

```text
Y = (A⊕B)′
```

Output = `1` when inputs are **same**.

```text
00 → 1
01 → 0
10 → 0
11 → 1
```

### Memory:

> **XNOR → Same = 1**

### Application

**Equality comparator**

---

# 5. XOR Important Properties ⭐⭐⭐⭐

```text
A⊕0 = A
A⊕1 = A′
A⊕A = 0
A⊕A′ = 1
```

For multiple inputs:

> **Odd number of 1s → XOR = 1**

---

# 6. Half Adder ⭐⭐⭐⭐⭐

A half adder adds two binary bits.

```text
A ──┬── XOR ── SUM
B ──┘
```

```text
A ──┬── AND ── CARRY
B ──┘
```

### Equations

```text
SUM = A⊕B
CARRY = AB
```

### Memory

> **XOR → SUM**
> **AND → CARRY**

---

# 7. Boolean Algebra Basics ⭐⭐⭐⭐⭐

Boolean variables have only:

```text
0,1
```

### Operators

```text
+     → OR
```

```text
·     → AND
```

```text
'     → NOT
```

Example:

```text
AB+C′
```

means:

```text
(A AND B) OR (NOT C)
```

---

# 8. Important Boolean Laws ⭐⭐⭐⭐⭐

### Identity

```text
A+0=A
A⋅1=A
```

### Dominance / Null

```text
A+1=1
A⋅0=0
```

### Idempotent

```text
A+A=A
A⋅A=A
```

### Complement

```text
A+A′=1
A⋅A′=0
```

### Involution

```text
(A′)′=A
```

### Absorption ⭐⭐⭐⭐⭐

```text
A+AB=A
A(A+B)=A
```

### Distributive

```text
A(B+C)=AB+AC
A+BC=(A+B)(A+C)
```

---

# 9. DeMorgan's Theorems ⭐⭐⭐⭐⭐

### Theorem 1

```text
(AB)′=A′+B′
```

### Theorem 2

```text
(A+B)′=A′B′
```

### Shortcut

When the NOT/bar moves inside:

```text
AND ↔ OR
```

**AND becomes OR**

**OR becomes AND**

**Every variable gets complemented**

Example:

```text
(ABC)′=A′+B′+C′
```

---

# 10. SOP ⭐⭐⭐⭐⭐

**SOP = Sum of Products**

Example:

```text
F=AB+A′C+BC
```

Structure:

```text
AND terms
```

↓

```text
OR
```

### Memory

> **SOP → AND first, OR later**

---

# 11. POS ⭐⭐⭐⭐⭐

**POS = Product of Sums**

Example:

```text
F=(A+B)(A′+C)(B+C)
```

Structure:

```text
OR terms
```

↓

```text
AND
```

### Memory

> **POS → OR first, AND later**

---

# 12. Minterms ⭐⭐⭐⭐⭐

Canonical SOP uses **minterms**.

Notation:

```text
Σm
```

Minterms correspond to rows where:

```text
F=1
```

### Minterm rule

```text
1 → normal
0 → complement
```

Example:

```text
A B C = 101
```

```text
m5=AB′C
```

because:

```text
101₂=5
```

---

# 13. Maxterms ⭐⭐⭐⭐⭐

Canonical POS uses **maxterms**.

Notation:

```text
ΠM
```

Maxterms correspond to rows where:

```text
F=0
```

### Maxterm rule

```text
1 → complement
0 → normal
```

Example:

```text
A B C = 101
```

```text
M5=(A′+B+C′)
```

---

# 14. Minterm vs Maxterm ⭐⭐⭐⭐⭐

| Minterm        | Maxterm    |
| -------------- | ---------- |
| Form           | Product    |
| Used in        | SOP        |
| Symbol         | m          |
| Function value | **1**      |
| Notation       | Σm         |
| 1 input        | Normal     |
| 0 input        | Complement |

| Minterm        | Maxterm    |
| -------------- | ---------- |
| Form           | Sum        |
| Used in        | POS        |
| Symbol         | M          |
| Function value | **0**      |
| Notation       | ΠM         |
| 1 input        | Complement |
| 0 input        | Normal     |

### 🔥 Most important memory line:

```text
Σm → 1s
ΠM → 0s
```

---

# 15. Canonical vs Standard ⭐⭐⭐⭐

### SOP

A sum of product terms.

Example:

```text
AB+A′C
```

### Canonical SOP

Every product term contains **every variable exactly once**.

Example:

```text
AB′C+A′BC
```

---

### POS

A product of sum terms.

Example:

```text
(A+B)(A′+C)
```

### Canonical POS

Every sum term contains **every variable exactly once**.

---

# 16. Truth Table → SOP/POS ⭐⭐⭐⭐⭐

### To get SOP:

1. Find rows where **F = 1**
2. Convert them to **minterms**
3. OR the minterms

```text
F = 1
```

↓

```text
Minterms
```

↓

```text
Σm
```

---

### To get POS:

1. Find rows where **F = 0**
2. Convert them to **maxterms**
3. AND the maxterms

```text
F = 0
```

↓

```text
Maxterms
```

↓

```text
ΠM
```

---

# 🧠 MASTER MEMORY SHEET

```text
AND      → All 1 → 1

OR       → Any 1 → 1

XOR      → Different → 1

XNOR     → Same → 1
```

```text
NAND     → Universal

NOR      → Universal
```

### Half Adder:

```text
SUM      → XOR

CARRY    → AND
```

### DeMorgan:

```text
AND ↔ OR
```

**Complement every variable**

```text
SOP      → AND → OR

POS      → OR → AND
```

```text
Σm       → SOP → 1s

ΠM       → POS → 0s
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
