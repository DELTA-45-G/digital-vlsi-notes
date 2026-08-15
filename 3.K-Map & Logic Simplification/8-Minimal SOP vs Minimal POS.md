# Minimal SOP vs Minimal POS ⭐⭐⭐⭐⭐

This is the **last major K-map concept** before we finish Phase 3 with placement shortcuts and revision.

---

# 1. SOP — Sum of Products

SOP means:

> **OR of AND terms**

Example:

```text id="9o7z3f"
F=A′B+AC+BC′
```

Each individual term is a **product term** because variables are ANDed.

```text id="7z24ua"
A'B
```

```text id="u6e5p1"
AC
```

```text id="f99f1b"
BC'
```

Then they are ORed:

```text id="3v2guz"
A′B+AC+BC′
```

So:

**SOP = AND terms connected by OR**

---

# 2. POS — Product of Sums

POS means:

> **AND of OR terms**

Example:

```text id="d46ybd"
F=(A+B)(A′+C)(B+C′)
```

Each bracket is a **sum term** because variables are ORed.

Then the brackets are ANDed.

So:

**POS = OR terms connected by AND**

---

# 3. The Most Important K-Map Rule ⭐⭐⭐⭐⭐

### SOP

Group:

```text id="1h0z4z"
1s
```

### POS

Group:

```text id="29b8s6"
0s
```

This is extremely important.

```text id="r0ylz0"
SOP → group 1s → AND terms → OR them
```

```text id="7a3g5h"
POS → group 0s → OR terms → AND them
```

---

# 4. Example — SOP

Suppose:

```text id="7b26na"
F=Σm(1,3)
```

The K-map contains:

```text id="z93gag"
0 1 1 0
```

We group the `1`s.

Suppose the result is:

```text id="jdl1tb"
A′C
```

That's a **SOP expression**.

---

# 5. Example — POS

Instead of grouping the `1`s, suppose we group the `0`s.

For example:

```text id="vvz9k3"
F=ΠM(0,2)
```

This means the function has zeros at:

```text id="f1e5ji"
0,2
```

We group those zeros.

The resulting expression will be in POS form.

---

# 6. Minterm vs Maxterm ⭐⭐⭐⭐⭐

This is frequently asked in placement MCQs.

### Minterm

Corresponds to a function value of:

```text id="c8er0q"
1
```

Therefore:

```text id="g3nq7q"
Σm
```

means **sum of minterms**.

---

### Maxterm

Corresponds to a function value of:

```text id="zx1k3h"
0
```

Therefore:

```text id="i4h9ps"
ΠM
```

means **product of maxterms**.

---

# 7. Easy Memory Trick 🧠

Remember:

> **m → minterm → 1**

> **M → maxterm → 0**

Or:

```text id="u8j6a8"
Σm → 1s
```

```text id="i2a0n0"
ΠM → 0s
```

⭐⭐⭐⭐⭐ Memorize this.

---

# 8. Example

Suppose:

```text id="8t0jv5"
F(A,B,C)=Σm(1,3,5,7)
```

This tells us:

```text id="r1yevp"
F = 1 at:
```

```text id="4a8c2z"
1,3,5,7
```

So we group those `1`s.

Result:

```text id="e0u0ga"
F=C
```

---

# 9. Complementary View

The same function could be described using the locations where it is `0`.

There are 8 total minterms:

```text id="by4j6g"
0,1,2,3,4,5,6,7
```

If the function is 1 at:

```text id="o0u86m"
1,3,5,7
```

then it is 0 at:

```text id="2m8u1v"
0,2,4,6
```

So:

```text id="6l4vvo"
F=ΠM(0,2,4,6)
```

This represents the same function.

---

# 10. ⭐ SOP vs POS Table

| Feature           | SOP             | POS             |
| ----------------- | --------------- | --------------- |
| Full form         | Sum of Products | Product of Sums |
| K-map grouping    | `1`s            | `0`s            |
| Uses              | Minterms        | Maxterms        |
| Notation          | Σm              | ΠM              |
| Basic operation   | AND first       | OR first        |
| Final combination | OR              | AND             |

---

# 11. How to Read a Group for SOP

Suppose a group contains:

```text id="n5q2i5"
A = 0
B = 1
C = changes
D = 0
```

For SOP:

* A = 0 → A′
* B = 1 → B
* C changes → eliminate C
* D = 0 → D′

Therefore:

```text id="0s3mvd"
A′BD′
```

---

# 12. How to Read a Group for POS ⭐⭐⭐⭐⭐

This is where students commonly make mistakes.

Suppose a group of **zeros** has:

```text id="j8j6ko"
A = 0
B = 1
C = changes
D = 0
```

For POS, the corresponding sum term is:

```text id="8t3p3w"
(A+B′+D)
```

Notice the reversal!

### For POS:

If variable is:

```text id="l9u3k6"
0 → variable appears normally
```

```text id="0q5y7d"
1 → variable appears complemented
```

---

# 13. Why Does POS Reverse?

Let's understand rather than memorize.

For SOP:

```text
constant 0 → complemented
```

```text
constant 1 → normal
```

For POS:

```text
constant 0 → normal
```

```text
constant 1 → complemented
```

So:

| Constant | SOP | POS |
| -------- | --- | --- |
| 0        | A′  | A   |
| 1        | A   | A′  |

⭐ This is very important.

---

# 14. Example — POS

Suppose a zero-group has:

```text id="h9fh5f"
A = 0
```

```text id="bpjz5n"
B = 1
```

```text id="e1hjf0"
C = changes
```

Then:

### A = 0

POS → A

### B = 1

POS → B′

### C changes

Remove C.

So:

```text id="mae47f"
(A+B′)
```

---

# 15. Group Size Still Matters ⭐⭐⭐⭐⭐

For a 4-variable K-map:

### Group of 1

Leaves 4 variables.

### Group of 2

Leaves 3 variables.

### Group of 4

Leaves 2 variables.

### Group of 8

Leaves 1 variable.

### Group of 16

Leaves 0 variables.

This applies to both SOP and POS.

---

# 16. Placement Shortcut ⭐⭐⭐⭐⭐

If the question says:

### "Find minimal SOP"

Immediately think:

```text id="ch5q1n"
GROUP 1s
```

If it says:

### "Find minimal POS"

Immediately think:

```text id="3fn6an"
GROUP 0s
```

This should become automatic.

---

# 17. Common Placement Trap ⚠️

Question:

> Find the minimal POS for F.

Student sees the `1`s and starts grouping them.

❌ Wrong.

For POS:

```text id="h6gpcd"
Group the 0s
```

---

# 18. Another Common Trap

Question:

```text id="u7y21p"
F=ΠM(1,3,5)
```

Students sometimes think these are `1` locations.

❌ Wrong.

```text id="9jc9m5"
ΠM
```

means:

```text id="1xmveb"
zeros at those locations
```

---

# 19. ⭐ Super-Fast Memory Table

```text id="wr4tre"
Σm → 1s → SOP
```

```text id="8xdq6s"
ΠM → 0s → POS
```

### SOP:

```text id="dx0aql"
0 → complemented

1 → normal
```

### POS:

```text id="0qj9ty"
0 → normal

1 → complemented
```

---

# 20. One More Important Concept

A function can have:

* a minimal SOP
* a minimal POS

and they don't necessarily look similar.

For example:

```text id="bxirb9"
F=AB+A′C
```

might be minimal SOP, while the corresponding POS could be something completely different.

Both represent the **same logic function**.

---
