# SYNCHRONOUS COUNTER ⭐⭐⭐⭐⭐

Now we move to the **next topic in the exact Phase 6 order**.

## 1. What is a Synchronous Counter?

A **synchronous counter** is a counter in which **all flip-flops receive the same clock signal simultaneously**.

```text
                 CLOCK
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
      ┌────┐     ┌────┐     ┌────┐
      │ FF0│     │ FF1│     │ FF2│
      └────┘     └────┘     └────┘
```

Therefore:

**All FFs receive the common clock**

---

## 2. Why is it Faster?

In a synchronous counter, the flip-flops don't wait for the output of the previous flip-flop to trigger.

Instead, all flip-flops are clocked together.

Therefore, the **ripple delay problem is avoided**.

---

## 3. 3-Bit Synchronous Up Counter

The counting sequence is still:

```text
000
```

001

010

011

100

101

110

111

000

But the clocking method is different from a ripple counter.

### Ripple counter

```text
CLK → FF0 → FF1 → FF2
```

### Synchronous counter

```text
       ┌→ FF0
CLK ───┼→ FF1
       └→ FF2
```

All flip-flops receive the same clock.

---

# 4. Additional Logic ⭐⭐⭐⭐⭐

A synchronous counter generally requires **combinational logic** to determine which flip-flops should toggle.

For example, in a 3-bit synchronous binary up counter using T flip-flops:

### FF0

FF0 toggles every clock:

**T0=1**

### FF1

FF1 toggles when Q0 is 1:

**T1=Q0**

### FF2

FF2 toggles when both lower bits are 1:

**T2=Q1Q0**

This is a very important placement concept.

---

# 5. Why Does FF2 Toggle Only When Q1Q0 = 11?

Consider the counting sequence:

```text
000
```

001

010

011

100

FF2 changes from:

**0→1**

when:

**011→100**

At that moment:

**Q1=1,Q0=1**

Therefore:

**T2=Q1Q0=1**

So FF2 toggles.

---

# 6. Synchronous vs Asynchronous Counter ⭐⭐⭐⭐⭐

| Feature                           | Asynchronous | Synchronous  |
| --------------------------------- | ------------ | ------------ |
| Clock                             | Rippled      | Common       |
| Flip-flops clocked simultaneously | ❌            | ✅            |
| Speed                             | Lower        | Higher       |
| Ripple delay                      | Present      | Avoided      |
| Additional logic                  | Less         | More         |
| Design                            | Simpler      | More complex |

### Remember:

> **Asynchronous → simple but slower**

> **Synchronous → faster but requires more logic**

---

# 7. Major Advantage

The biggest advantage is:

**Higher speed**

because the flip-flops receive the clock simultaneously.

---

# 8. Major Disadvantage

The main disadvantage is:

**More combinational logic**

which makes the circuit more complex than a basic ripple counter.

---

# 🧠 QUICK REVISION

```text
SYNCHRONOUS COUNTER
────────────────────────────

→ All FFs receive same clock

→ FFs change synchronously

→ No ripple clock propagation

→ Faster than asynchronous counter

→ Requires additional combinational logic


3-bit binary up counter using T FF:

T0 = 1

T1 = Q0

T2 = Q1·Q0
```
