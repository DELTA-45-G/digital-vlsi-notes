# &#x20;JOHNSON COUNTER ⭐⭐⭐⭐

A **Johnson counter** is a modified ring counter in which the **complement of the last flip-flop's output is fed back to the first flip-flop**.

It is also called:

**Twisted Ring Counter**

---

## 1. Basic Idea

### Normal Ring Counter

The last output is fed back directly:

```text id="g1d8w4"
Q_last ─────────► First FF
```

### Johnson Counter

The **complement** of the last output is fed back:

```text id="r5m2k9"
Q_last
   │
   ▼
 NOT
   │
   └────────────► First FF
```

Therefore:

**Johnson = Complemented feedback**

---

# 2. Why "Twisted Ring Counter"?

Because the feedback connection is "twisted" by adding an inversion.

Hence:

**Johnson Counter = Twisted Ring Counter**

---

# 3. MOD Value ⭐⭐⭐⭐⭐

For an n-bit Johnson counter:

**MOD=2n**

This is extremely important.

### Example

4 flip-flops:

**MOD=2(4)=8**

Therefore:

**4-bit Johnson counter = MOD-8**

---

# 4. State Sequence — 4-bit Johnson Counter ⭐⭐⭐⭐⭐

Starting from:

**0000**

A typical sequence is:

```text id="c9p1x6"
0000
```

↓

1000

↓

1100

↓

1110

↓

1111

↓

0111

↓

0011

↓

0001

↓

0000

There are:

**8 states**

Therefore:

**MOD=8**

for a 4-bit Johnson counter.

---

# 5. Why Does It Have 2n States?

A Johnson counter with n flip-flops generates:

**2n**

states.

For example:

### 3 FFs

**2(3)=6**

So:

**MOD-6**

### 5 FFs

**2(5)=10**

So:

**MOD-10**

---

# 6. Ring vs Johnson Counter ⭐⭐⭐⭐⭐

This is a **very common placement question**.

| Feature     | Ring Counter | Johnson Counter |
| ----------- | ------------ | --------------- |
| Feedback    | Direct       | Complemented    |
| Also called | One-hot      | Twisted ring    |
| n FFs       | MOD-n        | MOD-2n          |
| 4 FFs       | MOD-4        | MOD-8           |
| States      | n            | 2n              |

### ⭐ Memory trick

```text id="s7k3n8"
Ring:
```

n FF → n states

Johnson:

n FF → 2n states

---

# 7. Advantages

Johnson counters provide:

* More states than a ring counter using the same number of flip-flops
* Simple decoding
* Simple sequence generation
* Useful timing/control applications

---

# 8. Disadvantage

For n flip-flops, there are:

**2n**

possible binary states, but Johnson counter uses only:

**2n**

states.

So there are unused states when n>2.

Unused states:

**2n−2n**

### Example: 4-bit Johnson counter

Possible states:

**2⁴=16**

Used:

**2(4)=8**

Unused:

**16−8=8**

---

# 🧠 Quick Revision

```text id="v4y6m2"
JOHNSON COUNTER
────────────────────────

→ Modified ring counter

→ Complement of last FF output

  is fed back to first FF


Also called:

→ Twisted Ring Counter


n FFs:

→ MOD = 2n


4 FFs:

→ MOD-8


3 FFs:

→ MOD-6


Ring:

→ n FF → MOD-n


Johnson:

→ n FF → MOD-2n
```
