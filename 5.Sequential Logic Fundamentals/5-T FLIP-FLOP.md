# T FLIP-FLOP ⭐⭐⭐⭐

The **T flip-flop** is one of the simplest flip-flops and is especially important for understanding **counters and frequency division**.

## 1. What is a T Flip-Flop?

**T** stands for **Toggle**.

Its main purpose is to **toggle the output** when T is active.

```text
             ┌─────────┐
T ──────────►│ T  FF   │────► Q
CLK ────────►│    ↑    │
             └─────────┘
```

---

# 2. T Flip-Flop Truth Table ⭐⭐⭐⭐⭐

| T | Qnext | Operation |
| - | ----- | --------- |
| 0 | Q     | Hold      |
| 1 | Q̅    | Toggle    |

That's all you need to remember.

### Memory trick:

**T=0→Hold**

**T=1→Toggle**

---

# 3. Example

Suppose initially:

**Q=0**

and:

**T=1**

At the active clock edge:

**Qnext=1**

Next clock:

**Qnext=0**

Next:

**Qnext=1**

So:

```text
Clock:  ↑   ↑   ↑   ↑
```

Q:      0 → 1 → 0 → 1

The output continuously toggles.

---

# 4. Characteristic Equation ⭐⭐⭐⭐⭐

The T flip-flop equation is:

**Qnext=T⊕Q**

Let's verify.

### T=0:

**Qnext=0⊕Q=Q**

→ Hold.

### T=1:

**Qnext=1⊕Q=Q̅**

→ Toggle.

---

# 5. T Flip-Flop as a Frequency Divider ⭐⭐⭐⭐⭐

This is one of the most important applications.

Set:

**T=1**

Then the flip-flop toggles on every active clock edge.

Therefore:

**fQ=fCLK/2**

### Example

If:

**fCLK=100MHz**

then:

**fQ=50MHz**

---

# 6. T Flip-Flop and Counters ⭐⭐⭐⭐⭐

T flip-flops are commonly used to construct counters.

For example:

```text
       T=1
```

CLK ──► TFF ──► Q0

The output divides the frequency by 2.

Multiple T flip-flops can produce:

**f/2, f/4, f/8,...**

This leads directly into **binary counters**.

---

# 7. T Flip-Flop from JK Flip-Flop

A JK flip-flop becomes a T flip-flop when:

**J=K=T**

### If T=0:

**J=K=0**

→ Hold.

### If T=1:

**J=K=1**

→ Toggle.

Therefore:

**JK FF + J=K=T ⇒ T FF**

---

# 8. T Flip-Flop from D Flip-Flop

A D flip-flop can also be configured as a T flip-flop.

Since:

**Qnext=D**

and for T:

**Qnext=T⊕Q**

we need:

**D=T⊕Q**

So:

```text
T ──┐
    ├── XOR ──► D
Q ──┘
```

This makes the D flip-flop behave like a T flip-flop.

---

# 9. T Flip-Flop vs D Flip-Flop

| T Flip-Flop         | D Flip-Flop             |
| ------------------- | ----------------------- |
| T=0 → Hold          | D=0 → Q=0               |
| T=1 → Toggle        | D=1 → Q=1               |
| Useful for counters | Useful for data storage |
| Q+=T⊕Q              | Q+=D                    |

---

# 10. T Flip-Flop vs JK Flip-Flop

| T                     | JK                   |
| --------------------- | -------------------- |
| One input             | Two inputs           |
| T=1 → Toggle          | J=K=1 → Toggle       |
| T=0 → Hold            | J=K=0 → Hold         |
| Simple counter design | More general control |

You can think of T as a simplified JK:

**J=K=T**

---

# ⭐ Placement Questions

### Q1. What does T stand for?

**Toggle**

### Q2. What happens when T=0?

**Hold**

### Q3. What happens when T=1?

**Toggle**

### Q4. What is the characteristic equation?

**Qnext=T⊕Q**

### Q5. What is the major application of T flip-flops?

**Counters and frequency division**

### Q6. What happens to frequency when T=1?

**fQ=fCLK/2**

### Q7. How can a JK flip-flop be converted into a T flip-flop?

**J=K=T**

### Q8. How can a D flip-flop be configured as a T flip-flop?

**D=T⊕Q**

---

# 🧠 QUICK REVISION

```text
T FLIP-FLOP
────────────────────

T = Toggle

T=0 → HOLD

T=1 → TOGGLE

Equation:

Q(next) = T ⊕ Q

T=1:

fQ = fCLK / 2

Applications:

✓ Counters

✓ Frequency division

Conversions:

JK → T:

J = K = T

D → T:

D = T ⊕ Q
```
