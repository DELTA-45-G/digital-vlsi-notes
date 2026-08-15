# Standard vs Canonical Forms ⭐⭐⭐⭐⭐

This is the **last major theory section** of Phase 2 before we wrap up the phase.

There is an important distinction between:

* SOP
* Standard SOP
* Canonical SOP
* POS
* Standard POS
* Canonical POS

Let's make this very clear.

---

## 1. SOP vs Canonical SOP

Consider:

```text id="xyv7oj"
F = AB + A′C
```

This is **SOP** because:

```text id="u6n1c6"
AB + A'C
```

is a sum of product terms.

But suppose the variables are:

```text id="xif9q8"
A,B,C
```

The term `AB` does **not contain C**.

The term `A'C` does **not contain B**.

Therefore, this is **not canonical SOP**.

---

# 2. Canonical SOP ⭐⭐⭐⭐⭐

In canonical SOP:

> **Every product term must contain every variable exactly once.**

For three variables, every term must contain:

```text id="kbg4q8"
A, B, C
```

Examples:

```text id="w3f6ln"
ABC
AB′C
A′BC
A′B′C
```

These are all minterms.

---

# 3. Converting SOP → Canonical SOP

Suppose:

```text id="s8x5hy"
F = AB
```

Variables are:

```text id="5j5t6s"
A, B, C
```

The term `AB` is missing `C`.

Use:

```text id="q4z0ev"
C+C′=1
```

Therefore:

```text id="ag6vla"
AB = AB(C+C′)
```

Distribute:

```text id="b5q5og"
AB = ABC + ABC′
```

Now every term contains:

```text id="fcbw4c"
A B C
```

So this is canonical SOP.

---

# 4. Another Example ⭐⭐⭐⭐⭐

Suppose:

```text id="d5j0hf"
F = A+B
```

Variables:

```text id="7fxyy0"
A, B
```

Both terms are missing one variable.

For `A`:

```text id="7f9j8x"
A = A(B+B′) = AB+AB′
```

For `B`:

```text id="3wq0qj"
B = B(A+A′) = AB+A′B
```

Therefore:

```text id="s5b6ih"
A+B=AB+AB′+A′B
```

After removing the duplicate `AB`:

```text id="3osz92"
F=AB′+AB+A′B
```

This is canonical SOP.

---

# 5. Why Do We Need Canonical SOP?

Because it gives us a direct connection to **truth tables and K-maps**.

For example:

```text id="74wypa"
F=Σm(1,3,5,7)
```

immediately tells us:

> Function = 1 for rows 1, 3, 5 and 7.

This makes K-map construction easy.

---

# 6. Canonical POS ⭐⭐⭐⭐⭐

Canonical POS follows the opposite rule:

> **Every sum term must contain every variable exactly once.**

For variables `A,B,C`:

```text id="k24gf4"
(A+B+C)
(A+B′+C)
(A′+B+C′)
```

etc.

Each is a **maxterm**.

---

# 7. Standard POS

Consider:

```text id="s5h0vj"
F=(A+B)(A′+C)
```

This is POS.

But if variables are:

```text id="1u3r6q"
A, B, C
```

each bracket is missing a variable.

So it is **not canonical POS**.

Canonical POS requires every bracket to contain:

```text id="6p6f3x"
A, B, C
```

---

# 8. SOP vs POS vs Canonical Forms

| Form          | Structure      | Every variable present? |
| ------------- | -------------- | ----------------------- |
| SOP           | AND terms ORed | ❌ Not necessarily       |
| Canonical SOP | Minterms ORed  | ✅ Yes                   |
| POS           | OR terms ANDed | ❌ Not necessarily       |
| Canonical POS | Maxterms ANDed | ✅ Yes                   |

⭐ **This table is placement-important.**

---

# 9. Truth Table → SOP ⭐⭐⭐⭐⭐

Suppose:

| A | B | F     |
| - | - | ----- |
| 0 | 0 | 0     |
| 0 | 1 | **1** |
| 1 | 0 | 0     |
| 1 | 1 | **1** |

For SOP, select rows where:

```text id="c05x3n"
F=1
```

Rows:

```text id="z1ftid"
01
```

```text id="5qlw9r"
11
```

Convert them to minterms.

### Row `01`

```text id="9a2h43"
A′B
```

### Row `11`

```text id="iviv05"
AB
```

Therefore:

```text id="1t1j4y"
F=A′B+AB
```

Or:

```text id="e6w36b"
F=Σm(1,3)
```

---

# 10. Truth Table → POS ⭐⭐⭐⭐⭐

For POS, select rows where:

```text id="mmk4wt"
F=0
```

From the same table:

```text id="fxa9a4"
00
```

```text id="7lg4tc"
10
```

Now create maxterms.

### Row `00`

For maxterm:

```text id="03o5yr"
0 → normal
```

```text id="k8l2c7"
0 → normal
```

```text id="rt88jh"
(A+B)
```

### Row `10`

```text id="j3g1v6"
1 → complement
```

```text id="ye4h7s"
0 → normal
```

```text id="6u6k1l"
(A′+B)
```

Therefore:

```text id="bohzzf"
F=(A+B)(A′+B)
```

Or:

```text id="io0sp2"
F=ΠM(0,2)
```

---

# 11. ⭐ Very Important: SOP Uses 1s

When converting a truth table:

### SOP

Look at:

```text id="z6p4jr"
F=1
```

Then create **minterms**.

---

### POS

Look at:

```text id="z4d2n6"
F=0
```

Then create **maxterms**.

---

# 🧠 Memory Trick

```text id="xn3x0l"
SOP → 1s → minterms → Σm
```

```text id="z8sfiy"
POS → 0s → maxterms → ΠM
```

This single line will save you a lot of time in placement questions.

---

# 12. Minterm Number Shortcut

Suppose:

```text id="6qncyh"
A B C
1 0 1
```

Binary:

```text id="r0xmcz"
101₂ = 5
```

Therefore:

```text id="iz18c5"
m5
```

Minterm:

```text id="i7zyr5"
AB′C
```

---

# 13. Maxterm Number Shortcut

Same row:

```text id="x0p1vf"
A B C = 101
```

Binary:

```text id="ip6nxl"
101₂ = 5
```

Therefore:

```text id="m5u7ls"
M5
```

Maxterm:

```text id="l5m1z8"
(A′+B+C′)
```

⭐ **Minterm and maxterm have the SAME index.**

The expression is different.

---

# 14. Complement Relationship ⭐⭐⭐⭐⭐

For an `n`-variable function:

```text id="l8d2l8"
Σm(1 locations)
```

and:

```text id="19uwko"
ΠM(0 locations)
```

together cover all possible rows.

For 3 variables:

```text id="p4mbv5"
0,1,2,3,4,5,6,7
```

If:

```text id="j2d5h8"
F=Σm(1,3,5,7)
```

then the zero locations are:

```text id="6i4b7z"
0,2,4,6
```

Therefore:

```text id="xvvm3i"
F=ΠM(0,2,4,6)
```

---

# 15. Placement Shortcut ⭐⭐⭐⭐⭐

If a question gives:

```text id="pyh0ki"
F(A,B,C)=Σm(1,2,5,7)
```

You immediately know:

### Function = 1 at:

```text id="8az83h"
1,2,5,7
```

### Function = 0 at:

```text id="n0o7qi"
0,3,4,6
```

Therefore:

```text id="o3p51p"
F=ΠM(0,3,4,6)
```

No truth table is required.

---

# 16. VLSI Relevance ⭐⭐⭐⭐⭐

Why do we care about canonical forms?

Because they provide a systematic method to go from:

```text id="t8q4s7"
Truth table
```

```text id="3x0ndk"
     ↓
```

```text id="kqydj5"
Boolean expression
```

```text id="n1i1wu"
     ↓
```

```text id="y6m0wd"
Canonical SOP/POS
```

```text id="gf9pg0"
     ↓
```

```text id="gd8gc9"
K-map
```

```text id="9g0i1n"
     ↓
```

```text id="u0b7iz"
Simplified logic
```

```text id="q5b1hu"
     ↓
```

```text id="47s0vq"
Gates
```

```text id="8z0r88"
     ↓
```

```text id="6e0xv1"
CMOS implementation
```
