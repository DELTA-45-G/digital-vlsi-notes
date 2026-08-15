# PHASE 3 — LOGIC SIMPLIFICATION

## K-Map Revision Notes ⭐⭐⭐⭐⭐

---

# 1. K-Map Basics

A **Karnaugh Map (K-Map)** is a graphical method used to simplify Boolean expressions.

### Main purpose

* Minimize Boolean expressions
* Reduce number of gates
* Reduce number of literals
* Make digital circuits simpler and faster

### Number of cells

For n variables:

```text
Cells = 2ⁿ
```

| Variables | Cells |
| --------: | ----: |
|         2 |     4 |
|         3 |     8 |
|         4 |    16 |
|         5 |    32 |

---

# 2. Gray Code Ordering ⭐⭐⭐⭐⭐

K-map rows and columns are arranged using **Gray code**.

Correct order:

```text
00, 01, 11, 10
```

❌ Not:

```text
00, 01, 10, 11
```

### Why?

Adjacent cells must differ in **only one bit**.

```text
00 → 01 → 11 → 10
```

---

# 3. 2-Variable K-Map

For A,B:

```text
       B

       0   1

     ┌───┬───┐

 A=0 │m0 │m1 │

     ├───┼───┤

 A=1 │m2 │m3 │

     └───┴───┘
```

Total:

```text
2²=4
```

cells.

---

# 4. 3-Variable K-Map ⭐⭐⭐⭐⭐

For A,B,C:

```text
                 BC

              00  01  11  10

           ┌────┬────┬────┬────┐

 A = 0     │ m0 │ m1 │ m3 │ m2 │

           ├────┼────┼────┼────┤

 A = 1     │ m4 │ m5 │ m7 │ m6 │

           └────┴────┴────┴────┘
```

Total:

```text
2³=8
```

cells.

---

# 5. 4-Variable K-Map ⭐⭐⭐⭐⭐

For A,B,C,D:

```text
                  CD

             00   01   11   10

          ┌────┬────┬────┬────┐

 AB = 00  │ m0 │ m1 │ m3 │ m2 │

          ├────┼────┼────┼────┤

 AB = 01  │ m4 │ m5 │ m7 │ m6 │

          ├────┼────┼────┼────┤

 AB = 11  │m12 │m13 │m15 │m14 │

          ├────┼────┼────┼────┤

 AB = 10  │ m8 │ m9 │m11 │m10 │

          └────┴────┴────┴────┘
```

Total:

```text
2⁴=16
```

cells.

### ⭐ Memorize this layout.

---

# 6. K-Map Grouping Rules ⭐⭐⭐⭐⭐

Valid group sizes must be powers of 2:

```text
1,2,4,8,16,…
```

### Valid

```text
1
2
4
8
16
```

### Invalid

```text
3 ❌
5 ❌
6 ❌
7 ❌
10 ❌
```

---

# 7. Group Size vs Variables Remaining

For n variables:

```text
Variables remaining = n−log₂(group size)
```

### 4-variable K-map

| Group | Variables remaining |
| ----: | ------------------: |
|     1 |                   4 |
|     2 |                   3 |
|     4 |                   2 |
|     8 |                   1 |
|    16 |                   0 |

### ⭐ Golden Rule

> **Larger group → fewer variables → simpler expression**

---

# 8. What Makes Cells Adjacent?

### Adjacent:

* Left ↔ Right
* Top ↔ Bottom
* Horizontal neighbors
* Vertical neighbors

### Not adjacent:

* Diagonal cells ❌

---

# 9. Wrap-Around ⭐⭐⭐⭐⭐

K-map edges wrap around.

Therefore:

```text
First column ↔ Last column
```

and:

```text
First row ↔ Last row
```

are adjacent.

### Important example

```text
┌───┬───┬───┬───┐
│ 1 │ 0 │ 0 │ 1 │
└───┴───┴───┴───┘
```

```text
  ↑               ↑

  └── adjacent ───┘
```

---

# 10. Four-Corner Group ⭐⭐⭐⭐⭐

The four corners of a 4-variable K-map can form a valid group.

```text
1  0  0  1
```

```text
0  0  0  0
```

```text
0  0  0  0
```

```text
1  0  0  1
```

Because of wrap-around:

* Top ↔ Bottom
* Left ↔ Right

So the four corners are adjacent through the edges.

---

# 11. SOP — Sum of Products ⭐⭐⭐⭐⭐

SOP means:

> **OR of AND terms**

Example:

```text
F=A′B+AC+BC′
```

### K-map rule:

```text
SOP → Group 1s
```

Notation:

```text
Σm
```

---

# 12. POS — Product of Sums ⭐⭐⭐⭐⭐

POS means:

> **AND of OR terms**

Example:

```text
F=(A+B)(A′+C)(B+C′)
```

### K-map rule:

```text
POS → Group 0s
```

Notation:

```text
ΠM
```

---

# 13. Minterm vs Maxterm ⭐⭐⭐⭐⭐

### Minterm

Represents a location where:

```text
F=1
```

Notation:

```text
Σm
```

### Maxterm

Represents a location where:

```text
F=0
```

Notation:

```text
ΠM
```

### Memory trick

> **m → minterm → 1**

> **M → maxterm → 0**

---

# 14. SOP Variable Rule

When reading a group of `1`s:

| Variable value | SOP term |
| -------------: | -------- |
|              0 | A′       |
|              1 | A        |
|        Changes | Remove   |

### Example

If:

```text
A = 0
B = 1
C = changes
D = 0
```

Then:

```text
A′BD′
```

---

# 15. POS Variable Rule ⭐⭐⭐⭐⭐

When reading a group of `0`s:

| Variable value | POS term |
| -------------: | -------- |
|              0 | A        |
|              1 | A′       |
|        Changes | Remove   |

### Example

If:

```text
A = 0
B = 1
C = changes
```

Then:

```text
(A+B′)
```

### Memory:

```text
SOP:
```

0 → complemented

1 → normal

```text
POS:
```

0 → normal

1 → complemented

---

# 16. Don't-Care Conditions ⭐⭐⭐⭐⭐

Don't-care cells are represented by:

```text
X
```

They represent input combinations where the output doesn't matter.

For SOP:

```text
1 → MUST cover
0 → CANNOT use
X → OPTIONAL
```

### Most important rule

> **Use X only when it helps create a larger/simpler group.**

---

# 17. Don't-Care Example

Suppose:

```text
F=Σm(1,3)
```

and:

```text
d(5,7)
```

Without X:

```text
A′C
```

Using the don't-care cells:

```text
F=C
```

So don't-cares can eliminate variables.

---

# 18. Overlapping Groups ⭐⭐⭐⭐⭐

Overlapping is allowed.

Example:

```text
Group 1:
```

```text
[1][1]
[1][1]
```

```text
Group 2:

   [1][1]
   [1][1]
```

The shared cells can belong to both groups.

### Rule:

> **Overlap when it produces a simpler expression.**

---

# 19. Essential Prime Implicant ⭐⭐⭐⭐⭐

### Prime implicant

A group that cannot be expanded further without including a `0`.

### Essential prime implicant

A prime implicant that covers at least one `1` that **no other prime implicant can cover**.

### Memory trick:

> **Prime = cannot expand**

> **Essential = must select**

---

# 20. Largest Group Rule ⭐⭐⭐⭐⭐

Always look for the largest possible valid groups.

Preferred order:

```text
16→8→4→2→1
```

But remember:

> The goal is the **minimum final expression**, not simply the largest group in isolation.

---

# 21. Common K-Map Mistakes ❌

### ❌ Mistake 1

Using normal binary ordering.

Correct:

```text
00,01,11,10
```

---

### ❌ Mistake 2

Making groups of 3 or 6.

Only powers of 2 are allowed.

---

### ❌ Mistake 3

Grouping diagonally.

Diagonal cells are **not adjacent**.

---

### ❌ Mistake 4

Ignoring wrap-around.

Edges are adjacent.

---

### ❌ Mistake 5

Not using a larger possible group.

Always check whether a group can be expanded.

---

### ❌ Mistake 6

Thinking overlap is forbidden.

Overlap is allowed.

---

### ❌ Mistake 7

Trying to cover `0` in an SOP group.

For SOP, `0` cannot be included.

---

### ❌ Mistake 8

Thinking X must be used.

X is optional.

---

# 22. Placement Shortcuts ⭐⭐⭐⭐⭐

## Shortcut 1 — Full Map

All `1`s:

```text
F=1
```

All `0`s:

```text
F=0
```

---

## Shortcut 2 — Odd Minterms

Odd numbers have LSB = 1.

For 3 variables:

```text
1,3,5,7
```

Therefore:

```text
F=C
```

For 4 variables:

```text
1,3,5,7,9,11,13,15
```

Therefore:

```text
F=D
```

---

## Shortcut 3 — Even Minterms

Even numbers have LSB = 0.

3 variables:

```text
0,2,4,6
```

Therefore:

```text
F=C′
```

4 variables:

```text
0,2,4,6,8,10,12,14
```

Therefore:

```text
F=D′
```

---

# 23. 3-Variable Important Patterns ⭐⭐⭐⭐⭐

Memorize:

```text
Σm(0,1,2,3)=A′
Σm(4,5,6,7)=A
Σm(0,1,4,5)=B′
Σm(2,3,6,7)=B
Σm(0,2,4,6)=C′
Σm(1,3,5,7)=C
```

---

# 24. 4-Variable Important Patterns ⭐⭐⭐⭐⭐

```text
Σm(0,1,2,3)=A′B′
Σm(4,5,6,7)=A′B
Σm(8,9,10,11)=AB′
Σm(12,13,14,15)=AB
```

Also:

```text
Σm(0 through 7)=A′
Σm(8 through 15)=A
```

---

# 25. Binary Shortcut ⭐⭐⭐⭐⭐

Instead of drawing a K-map, convert minterms into binary.

Example:

```text
Σm(2,3,6,7)
```

```text
2 = 001
3 = 011
6 = 110
7 = 111
```

Look for constant bits.

Here:

```text
A → changes
B → changes
C → 1 always
```

Therefore:

```text
F=C
```

**But:** use this shortcut only when the minterms form a valid complete group.

---

# 26. Fast Placement Strategy

When you see:

```text
F=Σm(...)
```

think:

```text
1️⃣ Identify number of variables
```

↓

```text
2️⃣ Count minterms
```

↓

```text
3️⃣ Is count a power of 2?
```

↓

```text
4️⃣ Can they form one valid group?
```

↓

```text
5️⃣ Find constant variables
```

↓

```text
6️⃣ Write simplified expression
```

If the pattern isn't obvious:

```text
Draw the K-map
```

Don't guess.

---

# 27. K-Map Master Formula 🧠

For n variables:

```text
Remaining literals = n−log₂(group size)
```

Example:

4 variables, group of 4:

```text
4−log₂(4)=4−2=2
```

Therefore:

```text
2 literals
```

---

# 28. ⭐ Final Memory Sheet

```text
K-MAP
```

────────────────────────────

```text
n variables → 2^n cells
```

Gray code:

```text
00 → 01 → 11 → 10
```

Valid group sizes:

```text
1, 2, 4, 8, 16...
```

Larger group

↓

Fewer literals

↓

Simpler expression

```text
SOP → Group 1s
```

```text
POS → Group 0s
```

```text
Σm → Minterms → 1
```

```text
ΠM → Maxterms → 0
```

```text
X → Don't-care → Optional
```

```text
Wrap-around → YES
```

```text
Overlap → YES
```

```text
Diagonal → NO
```

```text
Group of 3 → NO
Group of 5 → NO
Group of 6 → NO
```

Prime implicant:

**Cannot expand**

Essential PI:

**Must select**

Full 1 map → 1

Full 0 map → 0

Odd minterms → last bit 1

Even minterms → last bit 0

---

# ⭐ Phase 3 — What You Must Know for VLSI Placements

If you're short on revision time, prioritize these:

### 🔥⭐⭐⭐⭐⭐ MUST KNOW

1. **Gray-code ordering**
2. **3-variable K-map layout**
3. **4-variable K-map layout**
4. **Group sizes = powers of 2**
5. **Largest-group principle**
6. **Wrap-around**
7. **Four-corner grouping**
8. **Overlap**
9. **SOP → group 1s**
10. **POS → group 0s**
11. **Σm vs ΠM**
12. **Don't-care** **`X`**
13. **Essential prime implicant**
14. **Variables remaining = n−log₂(group size)**
15. **Odd/even minterm shortcuts**
16. **Reading constant variables from binary**

### 🎯 Placement mindset

When solving a K-map, think:

> **Largest valid group → constant variables → remove changing variables → minimum literals.**
