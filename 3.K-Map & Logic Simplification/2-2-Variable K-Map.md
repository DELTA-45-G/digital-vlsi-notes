# 2-Variable K-Map: Actual Simplification ⭐⭐⭐⭐⭐

Now let's start solving K-map problems.

---

## 1. Basic 2-Variable K-Map

For variables A,B:

```text
          B

         0     1

       ┌─────┬─────┐

 A = 0 │ m0  │ m1  │

       ├─────┼─────┤

 A = 1 │ m2  │ m3  │

       └─────┴─────┘
```

Remember:

```text
m0 = A′B′
m1 = A′B
m2 = AB′
m3 = AB
```

---

# 2. Example 1 — Single 1

Given:

```text
F=Σm(3)
```

Put `1` in cell m3:

```text
          B

         0     1

       ┌─────┬─────┐

 A = 0 │  0  │  0  │

       ├─────┼─────┤

 A = 1 │  0  │  1  │

       └─────┴─────┘
```

There is only one `1`.

So the group size is:

```text
1
```

The corresponding minterm is:

```text
m3=AB
```

Therefore:

```text
F=AB
```

### Important

A group containing one cell does **not eliminate any variable**.

---

# 3. Example 2 — Two Adjacent 1s

Given:

```text
F=Σm(2,3)
```

K-map:

```text
          B

         0     1

       ┌─────┬─────┐

 A = 0 │  0  │  0  │

       ├─────┼─────┤

 A = 1 │ [1] │ [1] │

       └─────┴─────┘
```

The two cells are adjacent.

The corresponding minterms are:

```text
m2=AB′
m3=AB
```

So:

```text
F=AB′+AB
```

Factor A:

```text
F=A(B′+B)
B′+B=1
```

Therefore:

```text
F=A
```

---

# 4. What Happened?

Originally:

```text
AB'
AB
```

Notice:

```text
A → constant
B → changes
```

Therefore:

```text
B disappears
```

and:

```text
A remains
```

### ⭐ K-map shortcut

> **Keep what stays the same. Remove what changes.**

This is one of the most important K-map rules.

---

# 5. Example 3 — Vertical Pair

Given:

```text
F=Σm(1,3)
```

```text
          B

         0     1

       ┌─────┬─────┐

 A = 0 │  0  │ [1] │

       ├─────┼─────┤

 A = 1 │  0  │ [1] │

       └─────┴─────┘
```

Here:

```text
A changes
```

B stays 1

Therefore:

```text
F=B
```

---

# 6. Example 4 — All Four Cells

Given:

```text
F=Σm(0,1,2,3)
```

K-map:

```text
          B

         0     1

       ┌─────┬─────┐

 A = 0 │ [1]│ [1] │

       ├─────┼─────┤

 A = 1 │ [1]│ [1] │

       └─────┴─────┘
```

Group all 4 cells.

Both A and B change.

Therefore both variables disappear.

```text
F=1
```

---

# 7. Why Does a Group of 4 Become 1?

Because all possible combinations of A and B are present:

```text
00
01
10
11
```

So the output is always 1.

Therefore:

```text
F=1
```

---

# 8. K-Map Grouping Formula ⭐⭐⭐⭐⭐

For an n-variable K-map:

```text
Remaining variables=n−log2(group size)
```

For a 2-variable K-map:

| Group | Variables remaining |
| ----: | ------------------: |
|     1 |                   2 |
|     2 |                   1 |
|     4 |                   0 |

So:

```text
1 cell → AB
```

```text
2 cells → A or B
```

```text
4 cells → 1
```

---

# 9. Important Shortcut ⭐⭐⭐⭐⭐

Suppose you see:

```text
Two adjacent 1s
```

Ask:

> **Which variable changes?**

That variable disappears.

Example:

```text
A B
0 1
1 1
```

A changes.

B remains 1.

Therefore:

```text
B
```

---

# 10. What About POS?

For now, focus on **SOP**.

For SOP:

```text
Group 1s
```

Later we'll learn:

```text
POS → Group 0s
```

The rules are slightly different when writing the resulting POS expression, so we'll handle that separately.

---

# 🧠 K-Map Shortcut

Whenever you make a group:

### Step 1

Look at the variables.

### Step 2

Find which variables remain constant.

### Step 3

Discard variables that change.

### Step 4

Write the remaining variables.

Example:

```text
A B
0 1
1 1
```

Constant:

```text
B = 1
```

Answer:

```text
B
```

---

# ⭐ Placement Tip

A common interview question is:

> "Why does grouping adjacent cells eliminate a variable?"

Good answer:

> Adjacent K-map cells differ in only one variable. When the cells are combined, that variable appears in both complemented and uncomplemented forms and cancels using X+X′=1.

That's a **much stronger interview answer** than simply saying "the variable disappears."
