# 4-Variable K-Map: Multiple Groups & Minimum Expression ⭐⭐⭐⭐⭐

Now we reach the part that matters most in placement questions: **choosing the correct groups to obtain the minimum SOP**.

The key idea is:

> **Don't just find valid groups. Find the best combination of groups.**

---

## 1. Example: Two Groups

Consider:

```text
F=Σm(0,1,4,5,10,11,14,15)
```

Map:

```text
                CD

             00  01  11  10

          ┌────┬────┬────┬────┐

 AB = 00  │ 1  │ 1  │ 0  │ 0  │

          ├────┼────┼────┼────┤

 AB = 01  │ 1  │ 1  │ 0  │ 0  │

          ├────┼────┼────┼────┤

 AB = 11  │ 0  │ 0  │ 1  │ 1  │

          ├────┼────┼────┼────┤

 AB = 10  │ 0  │ 0  │ 1  │ 1  │

          └────┴────┴────┴────┘
```

There are two obvious groups of 4.

### Group 1

```text
m0,m1,m4,m5
```

Constant:

* A=0
* C=0

Therefore:

```text
A′C′
```

### Group 2

```text
m10,m11,m14,m15
```

Constant:

* A=1
* C=1

Therefore:

```text
AC
```

Final:

```text
F=A′C′+AC
```

---

# 2. Why Not Make Smaller Groups?

You could make groups of 2, but that would produce more literals and a more complicated expression.

For example:

```text
Group of 4 → 2 literals
```

```text
Group of 2 → 3 literals
```

```text
Group of 1 → 4 literals
```

So larger groups generally produce simpler terms.

---

# 3. Essential Prime Implicant ⭐⭐⭐⭐⭐

Now an important placement concept.

Suppose a `1` can be covered by only **one possible largest group**.

That group is an:

```text
Essential Prime Implicant
```

It **must** be selected.

### Simple idea

```text
        1

        ↓

only one possible useful group

        ↓

must select it
```

---

# 4. Example of an Essential Group

Imagine:

```text
┌────┬────┬────┬────┐
│ 1  │ 1  │ 0  │ 0  │
├────┼────┼────┼────┤
│ 1  │ 1  │ 1  │ 1  │
├────┼────┼────┼────┤
│ 0  │ 0  │ 1  │ 1  │
├────┼────┼────┼────┤
│ 0  │ 0  │ 0  │ 0  │
└────┴────┴────┴────┘
```

The exact essential-group identification depends on the available larger groups, but the principle is:

> A group containing a `1` that no other candidate group covers is essential.

---

# 5. Overlapping Groups ⭐⭐⭐⭐⭐

Suppose:

```text
┌────┬────┬────┬────┐
│ 1  │ 1  │ 1  │ 0  │
├────┼────┼────┼────┤
│ 1  │ 1  │ 1  │ 0  │
├────┼────┼────┼────┤
│ 0  │ 0  │ 0  │ 0  │
├────┼────┼────┼────┤
│ 0  │ 0  │ 0  │ 0  │
└────┴────┴────┴────┘
```

You may need two groups of 4:

```text
Group 1 → columns 00,01
```

```text
Group 2 → columns 01,11
```

The `01` cells are used twice.

✅ That's allowed.

### Rule

> **Overlap is allowed when it reduces the final expression.**

---

# 6. The Goal Is Not "Fewest Groups"

This is a subtle but important point.

Suppose you have:

```text
Option A:
```

2 groups of 4

```text
Option B:
```

1 group of 8 + 1 group of 2

Option B may be better even though it has more/less groups depending on the literals.

You should minimize:

### **Number of literals / overall expression complexity**

not blindly count groups.

---

# 7. Group Size and Literal Count ⭐⭐⭐⭐⭐

For a 4-variable K-map:

| Group size | Literal count |
| ---------: | ------------: |
|          1 |             4 |
|          2 |             3 |
|          4 |             2 |
|          8 |             1 |
|         16 |             0 |

So:

```text
Bigger group ⇒ fewer literals
```

This is the main reason we prefer larger groups.

---

# 8. Example: Group of 8 + Group of 4

Suppose:

```text
F=Σm(0,1,2,3,4,5,6,7,8,9,10,11)
```

First 12 minterms are 1.

You can make:

### Group of 8

```text
0−7
```

This gives:

```text
A′
```

### Remaining cells

```text
8,9,10,11
```

These form a group of 4:

```text
AB′C?
```

Let's inspect them carefully:

```text
1000
1001
1010
1011
```

Constants:

* A=1
* B=0

C and D vary.

So the second term is:

```text
AB′
```

Therefore:

```text
F=A′+AB′
```

Using absorption/distribution:

```text
A′+AB′=A′+B′
```

So:

```text
F=A′+B′
```

This demonstrates an important point:

> Sometimes the K-map gives a valid expression that can undergo additional Boolean simplification, though a properly minimized K-map expression is usually already minimal.

---

# 9. Don't Force a Group to Cover Only Once

Suppose one `1` is already covered but including it in a second group allows a much larger group.

✅ Use it again.

This is one of the most common beginner mistakes.

---

# 10. Prime Implicant vs Essential Prime Implicant

### Prime implicant

A group that **cannot be enlarged further** without including a 0.

### Essential prime implicant

A prime implicant that covers at least one `1` **not covered by any other prime implicant**.

### Placement memory

> **Prime = cannot expand**

> **Essential = must choose**

---

# 11. Don't-Care Preview ⭐⭐⭐⭐

Soon we'll cover don't-care conditions.

They are represented by:

```text
X
```

A don't-care cell can be treated as:

* `1` when it helps make a larger group
* `0` when it doesn't help

This can produce a simpler expression.

We'll study this properly next.

---

# 12. Placement-Level Grouping Strategy ⭐⭐⭐⭐⭐

When solving a 4-variable K-map:

### Step 1

Look for a group of **16**.

### Step 2

Then groups of **8**.

### Step 3

Then groups of **4**.

### Step 4

Then groups of **2**.

### Step 5

Use single cells only if absolutely necessary.

### Step 6

Make sure **every required 1 is covered**.

### Step 7

Check whether overlap can reduce literals.

### Step 8

Check whether any essential prime implicant exists.

---

# 13. A Very Important Placement Trap ⚠️

Suppose you see:

```text
1 1 1 1
```

You might be tempted to make two groups of 2.

Don't.

Make:

```text
[1][1][1][1]
```

as **one group of 4**.

Because:

```text
4 cells > 2 cells
```

and the larger group eliminates more variables.

---

# 14. Another Placement Trap ⚠️

Suppose:

```text
1 0
0 1
```

Don't group them.

They are diagonal.

```text
Diagonal cells are NOT adjacent
```

---

# 15. Wrap-Around Trap ⚠️

Suppose:

```text
1 0 0 1
```

The two `1`s at the edges **can be grouped**.

Many students miss this because they think only physically touching cells are adjacent.

Remember:

```text
K-map edges wrap around
```

---

# 🧠 4-Variable K-Map Master Rules

```text
16 cells
```

Gray order:

```text
00 01 11 10
```

Valid groups:

```text
1, 2, 4, 8, 16
```

Larger group → fewer literals

SOP → group 1s

Rectangular groups only

No diagonal grouping

Wrap-around allowed

Overlap allowed

Every 1 must be covered

Essential prime implicants must be selected

---

# ⭐ Placement Focus

At this point, you should be able to recognize:

* Group of 16 → constant 1
* Group of 8 → 1 literal
* Group of 4 → 2 literals
* Group of 2 → 3 literals
* Group of 1 → 4 literals
* Wrap-around groups
* Corner groups
* Overlapping groups
* Essential groups
