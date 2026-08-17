# MOD-N COUNTERS ⭐⭐⭐⭐⭐

This is a **very frequently asked placement topic**.

## 1. What is a MOD-N Counter?

A **MOD-N counter** has exactly **N distinct states** before repeating.

**MOD=N**

### Example: MOD-4

```text
00
```

01

10

11

00

There are 4 states:

**MOD-4**

---

## 2. Normal Binary Counter

An n-bit binary counter has:

**2ⁿ states**

Therefore:

| Flip-Flops | States | MOD    |
| ---------- | -----: | ------ |
| 1          |      2 | MOD-2  |
| 2          |      4 | MOD-4  |
| 3          |      8 | MOD-8  |
| 4          |     16 | MOD-16 |
| 5          |     32 | MOD-32 |

---

## 3. Number of Flip-Flops Required ⭐⭐⭐⭐⭐

For a MOD-N counter, choose the smallest n such that:

**2ⁿ≥N**

### Example: MOD-10

**2³=8<10**

**2⁴=16≥10**

Therefore:

**4 flip-flops**

---

# 4. Unused States ⭐⭐⭐⭐⭐

A 4-bit counter has:

**2⁴=16**

possible states.

But a MOD-10 counter needs only:

**10**

states.

Therefore:

**16−10=6**

states are unused.

Used states:

```text
0000 → 0001 → 0010 → ... → 1001
```

Then the counter returns to:

```text
0000
```

---

# 5. MOD-6 Counter

A MOD-6 counter needs 6 states:

```text
000
```

001

010

011

100

101

Then:

```text
101 → 000
```

How many flip-flops?

**2²=4<6**

**2³=8≥6**

Therefore:

**3 flip-flops**

Unused states:

**8−6=2**

---

# 6. MOD-5 Counter

Need:

**5 states**

Check:

**2²=4<5**

**2³=8≥5**

Therefore:

**3 flip-flops**

Unused states:

**8−5=3**

---

# 7. MOD-16 Counter

Since:

**2⁴=16**

we need:

**4 flip-flops**

There are **no unused states**.

---

# 8. MOD-20 Counter

Check powers of 2:

**2⁴=16<20**

**2⁵=32≥20**

Therefore:

**5 flip-flops**

Unused states:

**32−20=12**

---

# 9. General Formula ⭐⭐⭐⭐⭐

### Flip-flops required:

**n=⌈log₂N⌉**

Equivalent condition:

**2ⁿ≥N**

### Unused states:

**2ⁿ−N**

---

# 10. MOD-10 / Decade Counter ⭐⭐⭐⭐⭐

A **MOD-10 counter** is also called a:

**Decade counter**

It counts:

```text
0 → 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 → 0
```

It requires:

**4 flip-flops**

because:

**2³<10≤2⁴**

---

# 🧠 Quick Revision

```text
MOD-N COUNTER
────────────────────────

MOD-N:

→ N distinct states

Normal n-bit counter:

→ 2^n states

→ MOD = 2^n

FFs required:

→ 2^n ≥ N

→ n = ceil(log2 N)

Unused states:

→ 2^n - N

MOD-10:

→ Decade counter

→ 4 FFs

MOD-6:

→ 3 FFs

MOD-20:

→ 5 FFs
```
