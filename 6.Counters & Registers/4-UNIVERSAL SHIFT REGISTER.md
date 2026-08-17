# UNIVERSAL SHIFT REGISTER ⭐⭐⭐⭐⭐

A **universal shift register** is a shift register that can perform **multiple operations**.

It can typically:

1. **Hold** data
2. **Shift right**
3. **Shift left**
4. **Parallel load**

Therefore:

**Universal Shift Register = Hold + Shift Left + Shift Right + Parallel Load**

---

## 1. Why is it called "Universal"?

Because it can perform both:

* Serial operations
* Parallel operations

and can shift in **both directions**.

So it is more flexible than an ordinary shift register.

---

# 2. Basic Block Diagram

A simplified 4-bit universal shift register:

```text
          ┌──────────────────────┐
Parallel  │                      │
Inputs ──►│                      │
          │  Universal Shift     │──► Parallel Outputs
Serial ──►│     Register         │
Inputs    │                      │
          └──────────────────────┘
                ▲
                │
             Control
             Inputs
```

The control inputs determine which operation is performed.

---

# 3. Four Operations ⭐⭐⭐⭐⭐

Typically two control inputs are used.

Let them be:

**S1, S0**

A common control table is:

| S1 | S0 | Operation     |
| -- | -- | ------------- |
| 0  | 0  | Hold          |
| 0  | 1  | Shift Right   |
| 1  | 0  | Shift Left    |
| 1  | 1  | Parallel Load |

### ⭐ Memorize this table.

---

# 4. Hold

When:

**S1S0=00**

the register retains its previous value.

Example:

```text
Before: 1011
```

After:  1011

Therefore:

**Qnext=Q**

---

# 5. Shift Right

When:

**S1S0=01**

the data shifts toward the right.

Example:

```text
Before:
```

Q3 Q2 Q1 Q0

1  0  1  1

After:

0  1  0  1

A new serial bit enters from the left.

---

# 6. Shift Left

When:

**S1S0=10**

the data shifts toward the left.

Example:

```text
Before:
```

Q3 Q2 Q1 Q0

1  0  1  1

After:

0  1  1  0

A new serial bit enters from the right.

---

# 7. Parallel Load

When:

**S1S0=11**

all input bits are loaded simultaneously.

Suppose:

**D3D2D1D0=1101**

After the active clock edge:

**Q3Q2Q1Q0=1101**

Therefore:

**Parallel load → all bits loaded simultaneously**

---

# 8. Universal Shift Register Using Multiplexers ⭐⭐⭐⭐⭐

A common implementation uses a **MUX before each flip-flop**.

For a 4-bit universal shift register, each D flip-flop can select among different inputs:

```text
              ┌─────┐
Hold ────────►│     │
Shift Right ─►│ MUX │──► DFF
Shift Left ──►│     │
Parallel ────►│     │
              └─────┘
```

The control signals determine which input reaches the flip-flop.

This is why multiplexers are very important in universal shift-register design.

---

# 9. Why Is It Useful?

A universal shift register can perform several operations using one hardware block.

Applications include:

* Data transfer
* Serial/parallel conversion
* Temporary storage
* Data manipulation
* Digital communication

---

# 🧠 Quick Revision

```text
UNIVERSAL SHIFT REGISTER
────────────────────────────

Operations:

S1 S0

─────

00 → HOLD

01 → SHIFT RIGHT

10 → SHIFT LEFT

11 → PARALLEL LOAD

Can:

→ Hold

→ Shift right

→ Shift left

→ Parallel load

Common implementation:

→ MUX + D Flip-Flops
```

#Multiplexers are used because they select which input/data path should be connected to each flip-flop based on the control/select signals