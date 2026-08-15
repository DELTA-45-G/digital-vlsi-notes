# 4-Variable K-Map ⭐⭐⭐⭐⭐

This is **one of the most important K-map topics for VLSI placement exams**.

Most placement questions involving K-map simplification use **3 or 4 variables**, so you should become very comfortable with the 4-variable map.

---

## 1. How Many Cells?

For 4 variables:

```text
2⁴ = 16
```

Therefore:

```text
16 cells
```

We'll use:

```text
A,B,C,D
```

---

# 2. 4-Variable K-Map Layout ⭐⭐⭐⭐⭐

We divide the variables:

* AB → rows
* CD → columns

Both use Gray code.

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

### ⭐ Memorize this layout.

The order is:

```text
00
01
11
10
```

for **both rows and columns**.

---

# 3. Why This Order?

Because adjacent cells must differ by only one bit.

For rows:

```text
00 → 01
```

```text
01 → 11
```

```text
11 → 10
```

For columns:

```text
00 → 01
```

```text
01 → 11
```

```text
11 → 10
```

Therefore every horizontal or vertical neighbor differs in exactly one variable.

---

# 4. Valid Group Sizes

There are 16 cells, so possible group sizes are:

```text
1,2,4,8,16
```

Remember:

> ⭐ **Never make groups of 3, 5, 6, 7, 10, etc.**

---

# 5. Variables Remaining

For a 4-variable K-map:

| Group size | Variables remaining |
| ---------: | ------------------: |
|          1 |                   4 |
|          2 |                   3 |
|          4 |                   2 |
|          8 |                   1 |
|         16 |                   0 |

Formula:

```text
4−log2(group size)
```

### Example

Group of 4:

```text
4−log2(4) =4−2 =2
```

So a group of 4 produces a **2-variable term**.

---

# 6. Example 1 — Group of 4

Consider:

```text
F=Σm(0,1,2,3)
```

Place the 1s:

```text
                  CD

             00   01   11   10

          ┌────┬────┬────┬────┐

 AB = 00  │ 1  │ 1  │ 1  │ 1  │

          ├────┼────┼────┼────┤

 AB = 01  │ 0  │ 0  │ 0  │ 0  │

          ├────┼────┼────┼────┤

 AB = 11  │ 0  │ 0  │ 0  │ 0  │

          ├────┼────┼────┼────┤

 AB = 10  │ 0  │ 0  │ 0  │ 0  │

          └────┴────┴────┴────┘
```

All four cells in the first row are grouped.

Look at A,B,C,D:

```text
A = 0 → constant
```

B = 0 → constant

C changes

D changes

Therefore:

```text
F=A′B′
```

---

# 7. Example 2 — Vertical Group

Consider:

```text
F=Σm(0,1,4,5)
```

Map:

```text
                  CD

             00   01   11   10

          ┌────┬────┬────┬────┐

 AB = 00  │ 1  │ 1  │ 0  │ 0  │

          ├────┼────┼────┼────┤

 AB = 01  │ 1  │ 1  │ 0  │ 0  │

          ├────┼────┼────┼────┤

 AB = 11  │ 0  │ 0  │ 0  │ 0  │

          ├────┼────┼────┼────┤

 AB = 10  │ 0  │ 0  │ 0  │ 0  │

          └────┴────┴────┴────┘
```

Group:

```text
[1][1]
[1][1]
```

Constants:

```text
A = 0
```

C = 0

B changes.

D changes.

Therefore:

```text
F=A′C′
```

---

# 8. The Most Important Concept: Wrap-Around ⭐⭐⭐⭐⭐

In a 4×4 K-map:

```text
First column ↔ Last column
```

and:

```text
First row ↔ Last row
```

are adjacent.

So this:

```text
┌───┐           ┌───┐
│ 1 │           │ 1 │
└───┘           └───┘
```

can form a group if they are on opposite edges.

---

# 9. Four Corners ⭐⭐⭐⭐⭐

This is a **very common placement question**.

Suppose:

```text
              CD

           00  01  11  10

        ┌────┬────┬────┬────┐

 AB 00  │ 1  │ 0  │ 0  │ 1  │

        ├────┼────┼────┼────┤

 AB 01  │ 0  │ 0  │ 0  │ 0  │

        ├────┼────┼────┼────┤

 AB 11  │ 0  │ 0  │ 0  │ 0  │

        ├────┼────┼────┼────┤

 AB 10  │ 1  │ 0  │ 0  │ 1  │

        └────┴────┴────┴────┘
```

The four corners can be grouped.

Why?

Because:

* top ↔ bottom
* left ↔ right

are adjacent.

The four cells are:

```text
m0,m2,m8,m10
```

Binary:

```text
0000
```

```text
0010

1000

1010
```

Constant variables:

```text
A = 0
```

C = 0

B changes.

D changes.

Therefore:

```text
F=A′C′
```

⭐⭐⭐⭐⭐ **Remember the four-corners grouping.**

---

# 10. Group of 8

A group of 8 in a 4-variable K-map leaves only **one variable**.

For example:

```text
F=Σm(0,1,2,3,4,5,6,7)
```

These occupy the first two rows:

```text
┌────┬────┬────┬────┐
│ 1  │ 1  │ 1  │ 1  │
├────┼────┼────┼────┤
│ 1  │ 1  │ 1  │ 1  │
├────┼────┼────┼────┤
│ 0  │ 0  │ 0  │ 0  │
├────┼────┼────┼────┤
│ 0  │ 0  │ 0  │ 0  │
└────┴────┴────┴────┘
```

Here:

```text
A = 0
```

B changes

C changes

D changes

Therefore:

```text
F=A′
```

---

# 11. Group of 16

If every cell is `1`:

```text
F=Σm(0,1,2,…,15)
```

Group all 16 cells.

All variables change.

Therefore:

```text
F=1
```

---

# 12. ⭐ Extremely Important Pattern

For a 4-variable K-map:

```text
Group 1  → 4 variables
```

Group 2  → 3 variables

Group 4  → 2 variables

Group 8  → 1 variable

Group 16 → 0 variables → 1

This is one of the easiest placement questions.

---

# 13. Placement Shortcut

If the minterms represent all combinations where one variable remains fixed, identify that variable directly.

For example:

```text
Σm(0,1,2,3,4,5,6,7)
```

Binary values:

```text
0000
```

```text
0001

0010

0011

0100

0101

0110

0111
```

First bit is always:

```text
0
```

Therefore:

```text
A′
```

No need to draw the map.

---

# 14. Another Example

```text
Σm(8,9,10,11,12,13,14,15)
```

All numbers from 8 to 15 have first bit:

```text
1
```

Therefore:

```text
A
```

---

# 15. ⭐ Placement Thinking

When you see a K-map, don't immediately start grouping randomly.

Use this order:

```text
1️⃣ Look for a group of 16
```

↓

```text
2️⃣ Look for groups of 8
```

↓

```text
3️⃣ Look for groups of 4
```

↓

```text
4️⃣ Look for groups of 2
```

↓

```text
5️⃣ Single cells only if necessary
```

This helps you find the minimum expression.

---

# 16. Important Warning ⚠️

**Largest group does not mean "one group only."**

Sometimes you need multiple groups.

Example:

```text
You may need:
```

```text
Group of 8

+

Group of 4
```

rather than several groups of 2.

The goal is:

```text
Minimum final expression
```

not simply the fewest groups.

---

# 🧠 Quick Revision

```text
4 variables → 16 cells
```

Rows:

```text
00
01
11
10
```

Columns:

```text
00
01
11
10
```

Valid groups:

```text
1, 2, 4, 8, 16
```

Larger group → fewer literals

Wrap-around:

```text
left ↔ right
top ↔ bottom
```

Four corners → valid group of 4

SOP → group 1s

Keep constant variables.

Remove changing variables.
