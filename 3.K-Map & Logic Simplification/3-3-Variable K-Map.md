# 3-Variable K-Map ⭐⭐⭐⭐⭐

Now we'll move from 2 variables to **3 variables**.

This is very important for placement tests because **3-variable and 4-variable K-maps** are frequently asked.

---

# 1. How Many Cells?

For n variables:

```text
Number of cells = 2ⁿ
```

For 3 variables:

```text
2³ = 8
```

So a 3-variable K-map has:

```text
8 cells
```

---

# 2. 3-Variable K-Map Layout

Let's use:

* A → row
* B,C → columns

The columns use **Gray code**:

```text
00 → 01 → 11 → 10
```

So:

```text
                 BC

              00   01   11   10

           ┌────┬────┬────┬────┐

 A = 0     │ m0 │ m1 │ m3 │ m2 │

           ├────┼────┼────┼────┤

 A = 1     │ m4 │ m5 │ m7 │ m6 │

           └────┴────┴────┴────┘
```

⭐ **Memorize this layout.**

Notice the column order:

```text
00
01
11
10
```

NOT:

```text
00
01
10
11   ❌
```

---

# 3. Why Are the Minterm Numbers Not Sequential?

Look at the top row:

```text
BC = 00 → m0
```

```text
BC = 01 → m1
```

```text
BC = 11 → m3
```

```text
BC = 10 → m2
```

Because:

```text
001₂ = 1
011₂ = 3
010₂ = 2
```

So the physical order is:

```text
0,1,3,2
```

This is because of **Gray code ordering**.

---

# 4. Example 1 — Two Adjacent Cells

Suppose:

```text
F=Σm(1,3)
```

Place the 1s:

```text
                 BC

              00   01   11   10

           ┌────┬────┬────┬────┐

 A = 0     │ 0  │ 1  │ 1  │ 0  │

           ├────┼────┼────┼────┤

 A = 1     │ 0  │ 0  │ 0  │ 0  │

           └────┴────┴────┴────┘
```

The group is:

```text
m1 ↔ m3
```

Compare:

```text
m1 = 001
```

```text
m3 = 011
```

A:

```text
0 → 0   constant
```

B:

```text
0 → 1   changes
```

C:

```text
1 → 1   constant
```

Therefore:

```text
F=A′C
```

---

# 5. The "Keep Constant" Method ⭐⭐⭐⭐⭐

For every group, make a small table.

Example:

```text
       A B C
```

```text
m1     0 0 1
m3     0 1 1
       ─────
       same change same
```

Therefore:

```text
A = 0 → A′
```

B = changes → remove

C = 1 → C

Answer:

```text
A′C
```

This method is extremely reliable when you're learning.

---

# 6. Example 2 — Four-Cell Group

Suppose:

```text
F=Σm(1,3,5,7)
```

Place them:

```text
                 BC

              00   01   11   10

           ┌────┬────┬────┬────┐

 A = 0     │ 0  │ 1  │ 1  │ 0  │

           ├────┼────┼────┼────┤

 A = 1     │ 0  │ 1  │ 1  │ 0  │

           └────┴────┴────┴────┘
```

Group these 4 cells:

```text
        [1] [1]
        [1] [1]
```

Now examine the variables.

A changes:

```text
0 → 1
```

So A disappears.

B changes:

```text
0 → 1
```

So B disappears.

C remains:

```text
1
```

Therefore:

```text
F=C
```

---

# 7. Group Size → Variables Remaining

For a 3-variable K-map:

| Group size | Variables remaining |
| ---------: | ------------------: |
|          1 |                   3 |
|          2 |                   2 |
|          4 |                   1 |
|          8 |                   1 |

So:

```text
1 cell → 3 variables
```

```text
2 cells → 2 variables
```

```text
4 cells → 1 variable
```

```text
8 cells → 1
```

⭐ Remember:

```text
3−log2(group size)
```

---

# 8. Wrap-Around in 3-Variable K-Map ⭐⭐⭐⭐⭐

This is extremely important.

Look at the columns:

```text
00   01   11   10
```

The first and last columns are adjacent:

```text
00  ↔  10
```

Why?

Compare:

```text
00
10
```

Only one bit changes.

Therefore:

**First and last columns are adjacent**

---

# 9. Example — Wrap-Around Pair

Suppose:

```text
F=Σm(0,2)
```

K-map:

```text
                 BC

              00   01   11   10

           ┌────┬────┬────┬────┐

 A = 0     │ [1]│ 0  │ 0  │ [1]│

           ├────┼────┼────┼────┤

 A = 1     │ 0  │ 0  │ 0  │ 0  │

           └────┴────┴────┴────┘
```

Although the cells look far apart, they are adjacent through wrap-around.

Compare:

```text
m0 = 000
```

```text
m2 = 010
```

A:

```text
0 → 0  same
```

B:

```text
0 → 1  changes
```

C:

```text
0 → 0  same
```

Therefore:

```text
F=A′C′
```

---

# 10. ⭐ Very Important K-Map Concept

Don't judge adjacency based on **physical distance on the page**.

Judge it according to **K-map adjacency rules**.

So:

```text
left edge ↔ right edge
```

```text
top edge  ↔ bottom edge
```

are adjacent.

---

# 11. Example — Four Cells Across Wrap-Around

Suppose:

```text
F=Σm(0,2,4,6)
```

K-map:

```text
                 BC

              00   01   11   10

           ┌────┬────┬────┬────┐

 A = 0     │ [1]│ 0  │ 0  │ [1]│

           ├────┼────┼────┼────┤

 A = 1     │ [1]│ 0  │ 0  │ [1]│

           └────┴────┴────┴────┘
```

The four corner/edge cells form one group.

Compare all four:

```text
A → changes
```

B → changes

C → 0 always

Therefore:

```text
F=C′
```

---

# 12. Why Does This Work?

The four minterms are:

```text
A′B′C′
A′BC′
AB′C′
ABC′
```

Factor C′:

```text
C′(A′B′+A′B+AB′+AB)
```

The expression inside becomes:

```text
1
```

Therefore:

```text
F=C′
```

Again, K-map is simply performing Boolean simplification visually.

---

# 13. ⭐ Placement Shortcut

If you see:

```text
Σm(0,2,4,6)
```

Don't immediately expand it.

Convert the minterms to binary:

```text
0 = 000
```

```text
2 = 010
```

```text
4 = 100
```

```text
6 = 110
```

Look at the last bit:

```text
0
0
0
0
```

It is always 0.

Therefore:

```text
F=C′
```

This can save a lot of time in aptitude/MCQ tests.

---

# 14. Another Shortcut

Suppose:

```text
F=Σm(1,3,5,7)
```

Binary:

```text
1 = 001
```

```text
3 = 011
```

```text
5 = 101
```

```text
7 = 111
```

Last bit:

```text
1
1
1
1
```

Therefore:

```text
F=C
```

No K-map drawing is even necessary.

---

# 🧠 Important Pattern

For 3 variables:

### Even minterms:

```text
0,2,4,6
```

all have:

```text
LSB = 0
```

So:

```text
Σm(0,2,4,6)=C′
```

### Odd minterms:

```text
1,3,5,7
```

all have:

```text
LSB = 1
```

So:

```text
Σm(1,3,5,7)=C
```

⭐ **Very useful placement shortcut.**

---

# 15. 3-Variable K-Map Rules

Keep these:

```text
3 variables → 8 cells
```

Layout:

```text
00  01  11  10
```

Group sizes:

```text
1, 2, 4, 8
```

Largest group preferred.

Adjacent:

```text
Left ↔ Right

Top ↔ Bottom
```

Diagonal → NOT adjacent.

Overlapping → allowed.

SOP → group 1s.

Keep constant variables.

Remove changing variables.

---

# ⭐ Placement Focus

For 3-variable K-maps, make sure you can quickly recognize:

* ⭐ Gray-code ordering
* ⭐ Minterm placement
* ⭐ Groups of 2
* ⭐ Groups of 4
* ⭐ Wrap-around groups
* ⭐ Variables that remain constant
* ⭐ Variables that disappear
* ⭐ Odd/even minterm shortcuts
