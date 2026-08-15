# Subtopic 1: What is a K-Map? ⭐⭐⭐⭐⭐

We are now starting **Phase 3** in the original order.

The first thing to understand is **why K-Maps exist**. Don't start memorizing grouping rules yet.

---

# 1. What is a K-Map?

**K-Map = Karnaugh Map**

It is a **graphical method for simplifying Boolean expressions**.

Instead of doing a long Boolean-algebra simplification, we arrange the truth-table values in a special map and **group adjacent 1s or 0s**.

The goal is:

```text
Minimum Boolean expression
```

---

# 2. Why Do We Need K-Maps? ⭐⭐⭐⭐⭐

Suppose we have:

```text
F=A′BC+A′BC′+ABC+ABC′
```

You could simplify this using Boolean algebra.

But for larger expressions, this becomes difficult and error-prone.

A K-map lets us visually identify common variables and eliminate unnecessary variables.

For example, the above expression simplifies to:

```text
F=B
```

That's a huge simplification.

---

# 3. Why Is This Important in VLSI? ⭐⭐⭐⭐⭐

A simpler Boolean expression usually means fewer logic gates.

For example:

```text
Before:
```

```text
Many AND gates

     ↓

   Large OR
```

After simplification:

```text
Few gates
```

↓

Simpler circuit

This can reduce:

* ⭐ Gate count
* ⭐ Transistor count
* ⭐ Area
* ⭐ Power
* ⭐ Delay

Therefore:

> **K-map is a fundamental digital-design optimization technique.**

---

# 4. Basic Idea

A K-map is basically a rearranged truth table.

For a 2-variable function:

Variables:

```text
A,B
```

There are:

```text
2²=4
```

possible combinations.

So the K-map has **4 cells**.

```text
       B
```

```text
       0   1

      ┌───┬───┐

 A 0  │   │   │

      ├───┼───┤

 A 1  │   │   │

      └───┴───┘
```

Each cell represents one possible input combination.

---

# 5. Why Are K-Map Cells Ordered Differently? ⭐⭐⭐⭐⭐

This is one of the most important things to understand.

Normal binary order is:

```text
00
01
10
11
```

But K-map uses:

```text
00
01
11
10
```

This is called **Gray code ordering**.

### Why?

Because adjacent cells must differ in **only ONE variable**.

Look:

```text
00 → 01
```

Only B changes.

```text
01 → 11
```

Only A changes.

```text
11 → 10
```

Only B changes.

Therefore:

> **Adjacent K-map cells differ in exactly one variable.**

⭐⭐⭐⭐⭐ This is critical.

---

# 6. Gray Code ⭐⭐⭐⭐⭐

For 2 bits:

```text
00
01
11
10
```

Notice:

```text
00 → 01  = 1 bit changes
```

```text
01 → 11  = 1 bit changes
```

```text
11 → 10  = 1 bit changes
```

This allows us to group adjacent cells and eliminate variables.

---

# 7. 2-Variable K-Map

Let's construct it properly.

Variables:

* A = row
* B = column

```text
          B
```

```text
         0     1

       ┌─────┬─────┐

 A = 0 │ m0  │ m1  │

       ├─────┼─────┤

 A = 1 │ m2  │ m3  │

       └─────┴─────┘
```

Therefore:

| A | B | Minterm |
| - | - | ------- |
| 0 | 0 | m0      |
| 0 | 1 | m1      |
| 1 | 0 | m2      |
| 1 | 1 | m3      |

---

# 8. Putting Boolean Terms into K-Map

Suppose:

```text
F=Σm(1,3)
```

This means:

```text
F=1
```

at cells 1 and 3.

So:

```text
          B
```

```text
         0     1

       ┌─────┬─────┐

 A = 0 │  0  │  1  │

       ├─────┼─────┤

 A = 1 │  0  │  1  │

       └─────┴─────┘
```

We have two adjacent `1`s.

---

# 9. Grouping ⭐⭐⭐⭐⭐

We group adjacent `1`s.

```text
          B
```

```text
         0     1

       ┌─────┬─────┐

 A = 0 │  0  │ [1] │

       ├─────┼─────┤

 A = 1 │  0  │ [1] │

       └─────┴─────┘
```

These two cells have:

```text
B = 1
```

while A changes:

```text
A = 0
A = 1
```

Therefore A disappears.

The simplified expression is:

```text
F=B
```

---

# 10. Why Does A Disappear?

This is the heart of K-map simplification.

The two minterms are:

```text
m1=A′B
m3=AB
```

Therefore:

```text
F=A′B+AB
```

Factor B:

```text
F=B(A′+A)
```

Since:

```text
A′+A=1
```

we get:

```text
F=B
```

So K-map is essentially performing Boolean simplification **visually**.

---

# 11. The Main K-Map Principle ⭐⭐⭐⭐⭐

When two adjacent cells are grouped:

> **The variable that changes gets eliminated.**

Example:

```text
A = 0
A = 1
```

A changes → **A disappears**.

If:

```text
B = 1
B = 1
```

B remains constant → **B stays**.

---

# 12. Group Size Rules ⭐⭐⭐⭐⭐

K-map groups must contain a number of cells that is a **power of 2**.

Allowed:

```text
1,2,4,8,16,…
```

Not allowed:

```text
3 ❌
5 ❌
6 ❌
7 ❌
```

### Memory trick 🧠

> **K-map groups = powers of 2**

---

# 13. Why Bigger Groups Are Better ⭐⭐⭐⭐⭐

Suppose you have:

```text
2 cells → eliminate 1 variable
```

```text
4 cells → eliminate 2 variables
```

```text
8 cells → eliminate 3 variables
```

For an n-variable K-map:

```text
Variables remaining=n−log2(group size)
```

Example for 4 variables:

### Group of 2

```text
4−1=3
```

→ 3-variable term.

### Group of 4

```text
4−2=2
```

→ 2-variable term.

### Group of 8

```text
4−3=1
```

→ 1-variable term.

### Group of 16

```text
4−4=0
```

→ `1`.

---

# 14. ⭐ Golden Rule

> **Always try to make the largest possible valid groups.**

Because:

```text
Larger group ⇒ fewer literals
```

and generally:

```text
fewer literals ⇒ simpler circuit
```

---

# 15. Can a Cell Be Used More Than Once?

### YES! ⭐⭐⭐⭐⭐

This is a common beginner mistake.

A `1` can belong to multiple groups if that helps create a simpler expression.

Example:

```text
     1 1
```

```text
     1 1
```

You may use overlapping groups if necessary.

> **Overlapping is allowed.**

---

# 16. Can Groups Be Diagonal?

### NO. ❌

Adjacent means:

* Left/right
* Up/down

Not diagonal.

```text
1 0
0 1
```

These two `1`s are **not adjacent**.

---

# 17. The Wrap-Around Rule ⭐⭐⭐⭐⭐

This is one of the most important K-map concepts.

The **left and right edges are adjacent**.

Also:

> **Top and bottom edges are adjacent.**

For example:

```text
┌────┬────┬────┬────┐
│ 1  │ 0  │ 0  │ 1  │
├────┼────┼────┼────┤
│ 0  │ 0  │ 0  │ 0  │
└────┴────┴────┴────┘
```

The two `1`s at the extreme left and right can be grouped.

Why?

Because K-map conceptually wraps around.

Think of the map as a **cylinder/loop**, not an ordinary rectangle.

---

# 18. Corners Can Also Be Adjacent ⭐⭐⭐⭐⭐

In a 4×4 K-map, the four corners can form a valid group of 4.

```text
┌────┬────┬────┬────┐
│ 1  │ 0  │ 0  │ 1  │
├────┼────┼────┼────┤
│ 0  │ 0  │ 0  │ 0  │
├────┼────┼────┼────┤
│ 0  │ 0  │ 0  │ 0  │
├────┼────┼────┼────┤
│ 1  │ 0  │ 0  │ 1  │
└────┴────┴────┴────┘
```

These four corners are considered adjacent through wrap-around.

⭐ This is frequently tested in digital MCQs.

---

# 19. K-Map Rules — Memorize These ⭐⭐⭐⭐⭐

```text
1. Group only 1s for SOP.
```

```text
2. Group only 0s for POS.
```

```text
3. Group size must be 1,2,4,8,16...
```

```text
4. Make groups as large as possible.
```

```text
5. Groups must be rectangular.
```

```text
6. No diagonal grouping.
```

```text
7. Wrap-around is allowed.
```

```text
8. Overlapping is allowed.
```

```text
9. Every required 1 must be covered.
```

```text
10. Don't include 0 in an SOP group.
```

We'll study **grouping 0s for POS** separately.

---

# 20. K-Map vs Boolean Algebra

### Boolean algebra

You simplify using equations:

```text
A′B+AB=B(A′+A)=B
```

### K-map

You simplify visually:

```text
1
```

```text
1
```

↓

```text
B
```

Therefore K-map is particularly useful when expressions become complicated.

---

# 21. Placement Questions ⭐⭐⭐⭐⭐

### Q1. What is a K-map?

A graphical technique for simplifying Boolean expressions.

---

### Q2. What is the purpose of K-map?

To obtain a **minimal Boolean expression** and reduce logic complexity.

---

### Q3. What is Gray code ordering?

An ordering where adjacent values differ by exactly **one bit**.

---

### Q4. What are valid group sizes?

```text
1,2,4,8,16,…
```

---

### Q5. Can K-map groups overlap?

**Yes.**

---

### Q6. Can K-map groups wrap around edges?

**Yes.**

---

### Q7. Can diagonal cells be grouped?

**No.**

---

### Q8. For SOP, do we group 1s or 0s?

```text
1s
```

---

### Q9. For POS?

```text
0s
```

---

# 🧠 Quick Revision

```text
K-MAP = Karnaugh Map
```

Purpose:

**Simplify Boolean expressions.**

Key:

**Adjacent cells differ by ONE variable.**

Gray code:

```text
00 → 01 → 11 → 10
```

Group sizes:

```text
1, 2, 4, 8, 16...
```

Larger group → fewer variables

```text
SOP → group 1s
```

```text
POS → group 0s
```

No diagonal grouping.

Wrap-around allowed.

Overlapping allowed.

Every required 1 must be covered.
