# ENCODER ⭐⭐⭐⭐⭐

Now we move to **Encoder and Priority Encoder**.

## 1. What is an Encoder?

An **encoder** is a combinational circuit that converts **one active input out of many inputs into a binary code**.

For example, a **4-to-2 encoder** has:

* 4 inputs
* 2 outputs

because:

```text id="h7xq4r"
2²=4
```

```text id="qv7g1m"
D0 ──┐

D1 ──┤

D2 ──┤──► 4-to-2 ENCODER ──► Y1 Y0

D3 ──┘
```

### ⭐ Memory trick

> **Encoder: Many inputs → Fewer outputs**

For a normal 2ⁿ-to-n encoder:

```text id="0slf6k"
2ⁿ inputs → n outputs
```

---

## 2. 4-to-2 Encoder Truth Table

Assuming **only one input is HIGH at a time**:

| D3 | D2 | D1 | D0 | Y1 | Y0 |
| -- | -- | -- | -- | -- | -- |
| 0  | 0  | 0  | 1  | 0  | 0  |
| 0  | 0  | 1  | 0  | 0  | 1  |
| 0  | 1  | 0  | 0  | 1  | 0  |
| 1  | 0  | 0  | 0  | 1  | 1  |

So:

```text id="s3f0w6"
D0 → 00
D1 → 01
D2 → 10
D3 → 11
```

---

## 3. Encoder Equations

From the truth table:

```text id="7p3q6g"
Y1=D2+D3
```

and:

```text id="6v7o1r"
Y0=D1+D3
```

These are important for understanding the circuit.

---

# 4. The BIG Problem With a Normal Encoder ⭐⭐⭐⭐⭐

What happens if **more than one input is 1**?

Example:

```text id="u8r5q0"
D3 D2 D1 D0
```

```text id="h2c7j4"
0  1  1  0
```

Which input should the encoder represent?

Should it output:

```text id="j7n3p2"
D2 → 10
```

or:

```text id="5h1t1g"
D1 → 01
```

There is ambiguity.

Therefore:

```text id="w4p8x2"
Normal encoder assumes only one input is active
```

This limitation leads to the **Priority Encoder**.

---

# 5. Priority Encoder ⭐⭐⭐⭐⭐

A **Priority Encoder** can handle multiple active inputs.

It assigns a priority to the inputs.

For example:

```text id="9n0k6w"
D3>D2>D1>D0
```

means:

> D3 has the highest priority.

If multiple inputs are `1`, the highest-priority input wins.

---

## Example

Suppose:

```text id="k2d8m1"
D3 D2 D1 D0
```

```text id="w7f3q4"
0  1  1  0
```

Both D2 and D1 are active.

But:

```text id="n3g6r1"
D2>D1
```

So the output represents D2:

```text id="v5y2p8"
Y=10
```

---

## ⭐ Key Difference

| Encoder                                | Priority Encoder              |
| -------------------------------------- | ----------------------------- |
| Normally one input active              | Multiple inputs can be active |
| Multiple active inputs cause ambiguity | Priority resolves ambiguity   |
| No priority                            | Has priority                  |

### Memory trick:

> **Encoder = one active input**

> **Priority Encoder = multiple possible, highest wins**

---

## 6. Real Hardware Applications

Encoders are used in:

* Keyboard encoding
* Interrupt controllers
* CPU control logic
* Data compression
* Priority-based arbitration
* Digital communication

A particularly important hardware example is a **priority encoder in interrupt handling**, where multiple requests may arrive simultaneously and the highest-priority request must be serviced first.

---

## 7. Verilog Relevance ⭐⭐⭐⭐

A priority encoder is commonly described using `if-else`:

```verilog
always_comb begin
    if (D3)
        Y = 2'b11;
    else if (D2)
        Y = 2'b10;
    else if (D1)
        Y = 2'b01;
    else
        Y = 2'b00;
end
```

Notice the order:

```text id="r5t8x2"
D3
```

↓

```text id="n8p4k1"
D2
```

↓

```text id="q2m7v3"
D1
```

↓

```text id="c6w1z9"
D0
```

Because `D3` has the highest priority.

⭐ This is a good placement connection between **digital logic** and **Verilog RTL coding**.

---

# 🧠 Quick Revision

```text id="p4r8x1"
ENCODER
```

────────────────────

### Many inputs → fewer outputs

### Normal encoder:

```text id="x7m2q5"
2^n inputs → n outputs
```

### Example:

```text id="z3k6v9"
4-to-2 encoder
```

```text id="h5n1w8"
D0 → 00

D1 → 01

D2 → 10

D3 → 11
```

### Assumption:

Only ONE input active

### Problem:

Multiple inputs active

→ ambiguous

### Priority Encoder:

Multiple inputs allowed

→ highest-priority input wins

### Memory:

```text id="a8d3f6"
Encoder = Many → Few

Decoder = Few → Many
```
