# NAND & NOR — Universal Gates ⭐⭐⭐⭐⭐

This is **very important for VLSI placements**. NAND and NOR are called **universal gates** because we can construct **any Boolean logic function** using only NAND gates or only NOR gates.

---

## 1. What is NAND?

NAND means:

> **NOT + AND**

First perform AND, then invert the result.

### Boolean expression

```text id="k3p6dj"
Y = A⋅B
```

### Diagram

```text id="5qx4ht"
A ───┐
     │ AND ── NOT ── Y
B ───┘
```

Or symbolically:

```text id="z7w8q0"
A ───┐
     │ AND ○── Y
B ───┘

        ↑

      bubble
```

The small circle/bubble represents **NOT/inversion**.

---

# 2. NAND Truth Table ⭐⭐⭐

| A | B | AND | NAND  |
| - | - | --- | ----- |
| 0 | 0 | 0   | **1** |
| 0 | 1 | 0   | **1** |
| 1 | 0 | 0   | **1** |
| 1 | 1 | 1   | **0** |

### Memory trick

AND:

> All 1 → 1

NAND:

> All 1 → **0**

Therefore:

```text id="z8qetp"
NAND = NOT(AND)
```

---

# 3. Why is NAND Important?

NAND is called a **universal gate**.

That means we can build:

* NOT
* AND
* OR
* XOR
* Any Boolean function

using only NAND gates.

⭐⭐⭐⭐⭐ **Very common interview question:**

> Why is NAND called a universal gate?

**Answer:**

Because any Boolean logic function can be implemented using only NAND gates.

---

# 4. Making NOT Using NAND ⭐⭐⭐⭐⭐

Connect both inputs together.

```text id="8o6d6b"
       ┌──── NAND
A ─────┤
       └────
```

Both inputs receive `A`.

Therefore:

```text id="4ey3ky"
Y = A⋅A
```

Using Boolean identity:

```text id="tvz9eq"
A⋅A = A
```

So:

```text id="w2x4ty"
Y = A
```

Therefore:

**NAND + tied inputs = NOT**

---

# 5. Making AND Using NAND ⭐⭐⭐⭐⭐

First NAND:

```text id="6x2mzc"
X = A⋅B
```

Then invert X using another NAND.

```text id="i9q3r0"
A ───┐
     NAND ─── X ───┐
B ───┘             NAND ─── Y
                   ↑
                   │
                   └── X
```

Therefore:

```text id="q1j9x0"
Y = X
```

Since:

```text id="mnxv1o"
X = AB
```

we get:

```text id="nqf0lf"
Y = AB
```

So:

**2 NAND gates → AND**

---

# 6. Making OR Using NAND ⭐⭐⭐⭐⭐

This is very important because it uses **DeMorgan's theorem**, which we'll study deeply later.

We want:

```text id="f5kjp3"
Y = A+B
```

Using DeMorgan:

```text id="d4f8u9"
A+B = A⋅B
```

So:

1. NAND A with itself → `NOT A`
2. NAND B with itself → `NOT B`
3. NAND those two outputs

```text id="q0z0j8"
       ┌── NAND ── A̅ ──┐
A ─────┤                │
       └────────────────┤
                        NAND ── Y
       ┌── NAND ── B̅ ──┤
B ─────┤                │
       └────────────────┘
```

Result:

```text id="y6gq9s"
Y = A+B
```

So:

**3 NAND gates → OR**

---

# 7. NAND Universal Gate Summary ⭐⭐⭐⭐⭐

Using only NAND:

```text id="5l7ezi"
NOT → 1 NAND
```

```text id="k4j1nj"
AND → 2 NAND

OR  → 3 NAND
```

Memorize this.

---

# 8. What is NOR?

NOR means:

> **NOT + OR**

First perform OR, then invert the result.

### Boolean expression

```text id="7j7brf"
Y = A+B
```

### Diagram

```text id="f5acp9"
A ───┐
     │ OR ── NOT ── Y
B ───┘
```

---

# 9. NOR Truth Table ⭐⭐⭐

| A | B | OR | NOR   |
| - | - | -- | ----- |
| 0 | 0 | 0  | **1** |
| 0 | 1 | 1  | **0** |
| 1 | 0 | 1  | **0** |
| 1 | 1 | 1  | **0** |

### Memory trick

OR:

> At least one 1 → 1

NOR:

> Any 1 → **0**

Therefore:

```text id="9dgf70"
NOR = NOT(OR)
```

---

# 10. Why is NOR Important?

NOR is also a **universal gate**.

Any Boolean function can be implemented using only NOR gates.

⭐⭐⭐⭐⭐

This is a very common placement question:

> Which gates are universal?

### Answer:

```text id="d9e3vn"
NAND and NOR
```

---

# 11. Making NOT Using NOR ⭐⭐⭐⭐⭐

Connect both inputs together.

```text id="7s4f1w"
       ┌──── NOR
A ─────┤
       └────
```

Then:

```text id="7s1v1g"
Y = A+A
```

Since:

```text id="c9e8vj"
A+A = A
```

Therefore:

```text id="amrmch"
Y = A
```

So:

**NOR + tied inputs = NOT**

---

# 12. Making OR Using NOR ⭐⭐⭐⭐⭐

First NOR:

```text id="a3j7ii"
X = A+B
```

Then invert X using another NOR.

```text id="fv4k0t"
A ───┐
     NOR ─── X ───┐
B ───┘            NOR ─── Y
                  ↑
                  └── X
```

Therefore:

```text id="dsh5bp"
Y = A+B
```

So:

**2 NOR gates → OR**

---

# 13. Making AND Using NOR ⭐⭐⭐⭐⭐

Using DeMorgan:

```text id="h8o11f"
AB = A+B
```

Therefore:

1. NOR A with itself → `A̅`
2. NOR B with itself → `B̅`
3. NOR `A̅` and `B̅`

Result:

```text id="x8q0qv"
Y = AB
```

So:

**3 NOR gates → AND**

---

# 14. NOR Universal Gate Summary ⭐⭐⭐⭐⭐

Using only NOR:

```text id="l1y7b8"
NOT → 1 NOR
```

```text id="5a0q4r"
OR  → 2 NOR

AND → 3 NOR
```

---

# 15. NAND vs NOR ⭐⭐⭐⭐⭐

| Feature          | NAND    | NOR      |
| ---------------- | ------- | -------- |
| Meaning          | NOT AND | NOT OR   |
| Expression       | `(AB)'` | `(A+B)'` |
| Universal?       | ✅       | ✅        |
| NOT using itself | 1 gate  | 1 gate   |
| AND using itself | 2 gates | 3 gates  |
| OR using itself  | 3 gates | 2 gates  |

---

# 16. Important Shortcut 🧠

Remember:

### NAND

```text id="kpv0j3"
NAND → naturally gives AND
```

To get AND:

**NAND + NAND**

---

### NOR

```text id="m56e0x"
NOR → naturally gives OR
```

To get OR:

**NOR + NOR**

---

# 17. NAND/NOR in CMOS VLSI ⭐⭐⭐⭐⭐

This is where this becomes especially relevant to your VLSI preparation.

CMOS circuits use:

* **PMOS**
* **NMOS**

NAND and NOR gates can be directly implemented using transistor networks.

Conceptually:

```text id="ak2rju"
Boolean expression
```

```text id="1d2e4h"
        ↓

     NAND/NOR

        ↓

   CMOS transistor
      network

        ↓

      VLSI
```

You don't need transistor-level design yet.

We'll study that properly in **Phase 10**.

---

# 18. Placement Questions ⭐⭐⭐⭐⭐

### Q1. Why is NAND called a universal gate?

**Answer:** Because any Boolean function can be implemented using only NAND gates.

---

### Q2. Why is NOR called a universal gate?

**Answer:** Because any Boolean function can be implemented using only NOR gates.

---

### Q3. Which two gates are universal gates?

**Answer:**

```text id="w5uw6f"
NAND, NOR
```

---

### Q4. How can you make NOT using NAND?

**Answer:** Connect both NAND inputs together.

```text id="knf0ze"
Y = A⋅A = A
```

---

### Q5. How can you make NOT using NOR?

**Answer:** Connect both NOR inputs together.

```text id="h8j0m4"
Y = A+A = A
```

---

### Q6. How many NAND gates are needed to make an AND gate?

**Answer:** **2 NAND gates.**

---

### Q7. How many NOR gates are needed to make an OR gate?

**Answer:** **2 NOR gates.**

---

# 19. Common Mistakes ❌

### Mistake 1

Thinking NAND means:

`NOT A AND B`

❌ Wrong.

NAND means:

```text id="p78f6b"
AB
```

The **entire AND result is inverted**.

---

### Mistake 2

Thinking NOR means:

`NOT A OR B`

❌ Wrong.

NOR means:

```text id="bylvyf"
A+B
```

The **entire OR result is inverted**.

---

### Mistake 3

Forgetting that NAND/NOR are universal.

⭐⭐⭐⭐⭐ **Memorize this.**

---

# 20. Quick Revision ⭐⭐⭐⭐⭐

```text id="d8z6dh"
NAND = NOT(AND)
```

```text id="1d1o7y"
Y = (A·B)'
```

```text id="6rf7xa"
NOR = NOT(OR)
```

```text id="nf7kes"
Y = (A+B)'
```

### NAND-only

```text id="sp2k9o"
NOT = 1 NAND
```

```text id="4l6m5v"
AND = 2 NAND
```

```text id="5dql5e"
OR  = 3 NAND
```

### NOR-only

```text id="u8l7ig"
NOT = 1 NOR
```

```text id="7r5h2s"
OR  = 2 NOR
```

```text id="n2z7oa"
AND = 3 NOR
```

### Universal gates

```text id="g2j19j"
NAND ⭐⭐⭐⭐⭐
```

```text id="7fiz3m"
NOR  ⭐⭐⭐⭐⭐
```

---

# 🧠 Memory Trick

Think:

**NAND → AND's opposite**

**NOR → OR's opposite**

And:

> **NAND naturally builds AND; NOR naturally builds OR.**
