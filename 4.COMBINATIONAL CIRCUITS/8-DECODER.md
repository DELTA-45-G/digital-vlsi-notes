# DECODER ⭐⭐⭐⭐⭐

A **Decoder** is essentially the opposite of an encoder.

---

## 1. What is a Decoder?

A decoder converts:

```text
n input bits → 2ⁿ output lines
```

For example, a **2-to-4 decoder** has:

* 2 inputs
* 4 outputs

```text
          ┌────────────┐
A ────────►            │──► Y0
B ────────►  DECODER   │──► Y1
          │            │──► Y2
          └────────────┘──► Y3
```

Because:

```text
2²=4
```

---

# 2. Encoder vs Decoder ⭐⭐⭐⭐⭐

This is a very common placement MCQ.

| Encoder                       | Decoder                        |
| ----------------------------- | ------------------------------ |
| Many → Few                    | Few → Many                     |
| 2ⁿ→n                          | n→2ⁿ                           |
| Converts active input to code | Converts code to active output |

### 🧠 Memory trick

> **Encoder: compresses**

> **Decoder: expands**

---

# 3. 2-to-4 Decoder

Inputs:

```text
A,B
```

Outputs:

```text
Y0,Y1,Y2,Y3
```

Only one output is active for each input combination.

---

## 4. Truth Table ⭐⭐⭐⭐⭐

| A | B | Y0 | Y1 | Y2 | Y3 |
| - | - | -- | -- | -- | -- |
| 0 | 0 | 1  | 0  | 0  | 0  |
| 0 | 1 | 0  | 1  | 0  | 0  |
| 1 | 0 | 0  | 0  | 1  | 0  |
| 1 | 1 | 0  | 0  | 0  | 1  |

So:

```text
AB = 00 → Y0 = 1
```

```text
AB = 01 → Y1 = 1
```

```text
AB = 10 → Y2 = 1
```

```text
AB = 11 → Y3 = 1
```

---

# 5. Decoder Equations ⭐⭐⭐⭐⭐

From the truth table:

### Y0

Active when:

```text
A=0,B=0
```

Therefore:

```text
Y0=A′B′
```

---

### Y1

Active when:

```text
A=0,B=1
```

Therefore:

```text
Y1=A′B
```

---

### Y2

Active when:

```text
A=1,B=0
```

Therefore:

```text
Y2=AB′
```

---

### Y3

Active when:

```text
A=1,B=1
```

Therefore:

```text
Y3=AB
```

---

# 6. ⭐ Decoder Produces Minterms

This is an extremely important connection to your **Phase 2 Boolean Algebra**.

For a 2-to-4 decoder:

```text
Y0=A′B′
Y1=A′B
Y2=AB′
Y3=AB
```

These correspond to:

```text
m0,m1,m2,m3
```

Therefore:

> **A decoder can generate all minterms of its input variables.**

⭐ This is frequently used to implement Boolean functions.

---

# 7. Decoder as a Minterm Generator ⭐⭐⭐⭐⭐

Suppose we want:

```text
F(A,B)=Σm(1,3)
```

The decoder generates:

```text
Y0 = m0
```

```text
Y1 = m1
```

```text
Y2 = m2
```

```text
Y3 = m3
```

We need:

```text
m1+m3
```

Therefore:

```text
F=Y1+Y3
```

So a Boolean function can be implemented using:

```text
Decoder + OR gate
```

This is a very important placement concept.

---

# 8. Enable Input ⭐⭐⭐⭐⭐

Practical decoders often have an **Enable (E)** input.

The decoder operates only when enabled.

Conceptually:

```text
             Enable
                │
                ▼

A ─────────► ┌─────────┐

B ─────────► │ DECODER │

             └─────────┘
```

If:

```text
E=1
```

the decoder works.

If:

```text
E=0
```

the outputs are disabled.

⚠️ The exact active level depends on the decoder design. Some decoders have **active-high enable**, while others use **active-low enable**.

---

# 9. Real Hardware Applications ⭐⭐⭐⭐

Decoders are used in:

* Memory address decoding
* Instruction decoding
* Chip selection
* Demultiplexing
* Control logic
* CPU/ALU control
* Display systems

### Important VLSI example:

When a processor accesses a memory address, decoder logic can determine **which memory location/chip should be selected**.

---

# 10. Decoder vs Demultiplexer

These two are often confused.

### Decoder

```text
n inputs → 2ⁿ outputs
```

Used primarily for **code-to-one-hot-line conversion**.

### Demultiplexer

```text
1 data input → 2ⁿ outputs
```

Uses select lines to route data to one output.

We'll cover MUX/DEMUX separately.

---

# 11. Verilog Relevance ⭐⭐⭐⭐

A simple 2-to-4 decoder:

```verilog
always_comb begin
    case ({A, B})
        2'b00: Y = 4'b0001;
        2'b01: Y = 4'b0010;
        2'b10: Y = 4'b0100;
        2'b11: Y = 4'b1000;
    endcase
end
```

Notice the output is **one-hot**:

```text
0001
```

```text
0010
```

```text
0100
```

```text
1000
```

⭐ **One-hot output** is a useful term to remember.

---

# 12. Decoder Quick Revision 🧠

```text
DECODER
```

────────────────────────

### n inputs → 2ⁿ outputs

### Example:

2-to-4 decoder

```text
00 → Y0
01 → Y1
10 → Y2
11 → Y3
```

### Only one output active

(for an enabled active-high decoder)

### Outputs correspond to:

```text
MINTERMS
```

### Can implement:

Boolean function

using Decoder + OR

### Common uses:

Memory address decoding

Instruction decoding

Chip selection

Control logic

### Memory:

```text
Encoder → Many → Few

Decoder → Few → Many
```
