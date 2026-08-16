# SUBTRACTORS ⭐⭐⭐⭐⭐

Now we move from **binary addition** to **binary subtraction**.

We will cover:

1. Half Subtractor
2. Full Subtractor
3. How subtraction is implemented using 2's complement
4. Adder-subtractor concept

---

# 1. Why Do We Need a Subtractor?

Digital systems need to perform operations such as:

```text id="p0bq6w"
A−B
```

Examples:

* ALUs
* CPUs
* Digital calculators
* Arithmetic circuits

A subtractor is a **combinational circuit** that performs binary subtraction.

---

# 2. Binary Subtraction Basics

Remember these four cases:

| A | B | Result        |
| - | - | ------------- |
| 0 | 0 | 0             |
| 0 | 1 | 1 with Borrow |
| 1 | 0 | 1             |
| 1 | 1 | 0             |

The important case is:

```text id="9wv2fa"
0−1
```

We cannot directly subtract `1` from `0`.

So we need a **Borrow**.

---

# 3. Half Subtractor ⭐⭐⭐⭐⭐

A **Half Subtractor** subtracts two 1-bit numbers.

Inputs:

```text id="b7b6j1"
A, B
```

Outputs:

```text id="f6t6rr"
Difference, Borrow
```

Here:

* A = minuend
* B = subtrahend

```text id="zq9h0v"
       A ─────┐
              │
              ▼

          ┌─────────────┐

       B ─► HALF        │

          │ SUBTRACTOR  │

          └─────────────┘

              │

          ┌───┴────┐

          ▼        ▼

     Difference   Borrow
```

---

# 4. Half Subtractor Truth Table ⭐⭐⭐⭐⭐

| A | B | Difference | Borrow |
| - | - | ---------- | ------ |
| 0 | 0 | 0          | 0      |
| 0 | 1 | 1          | 1      |
| 1 | 0 | 1          | 0      |
| 1 | 1 | 0          | 0      |

Notice the Difference column:

```text id="p7z4tq"
0 1 1 0
```

That's XOR.

Therefore:

```text id="j7n3k5"
D=A⊕B
```

---

# 5. Borrow Equation ⭐⭐⭐⭐⭐

Look at the Borrow column:

```text id="1x53cp"
0
1
0
0
```

Borrow occurs only when:

```text id="w2h8r5"
A=0,B=1
```

Therefore:

```text id="y9f6g9"
Borrow=A′B
```

### ⭐ Half Subtractor equations

```text id="c1c9p4"
D=A⊕B
Borrow=A′B
```

---

# 6. Why is Difference XOR?

The Difference is `1` when the two inputs are different:

```text id="qckg6z"
A B | Difference
----------------
0 0 |     0
0 1 |     1
1 0 |     1
1 1 |     0
```

Exactly XOR:

```text id="xg8b4f"
D=A⊕B
```

---

# 7. Why is Borrow A′B?

Borrow occurs only when:

```text id="h4i6wp"
A=0,B=1
```

Therefore:

```text id="2o1p4l"
A′=1
```

and:

```text id="0qv8fl"
B=1
```

So:

```text id="2b2x0m"
Borrow=A′B
```

---

# 8. Example

Suppose:

```text id="2x2p1u"
A=0,B=1
```

Then:

```text id="f77jkr"
0−1
```

We need to borrow.

Therefore:

```text id="v6n7z1"
Difference = 1
```

```text id="b1l5zo"
Borrow = 1
```

So:

```text id="9zuz4t"
D=1, Borrow=1
```

---

# 9. Half Adder vs Half Subtractor ⭐⭐⭐⭐⭐

| Feature       | Half Adder | Half Subtractor    |
| ------------- | ---------- | ------------------ |
| Operation     | Addition   | Subtraction        |
| Inputs        | A, B       | A, B               |
| Outputs       | Sum, Carry | Difference, Borrow |
| First output  | A⊕B        | A⊕B                |
| Second output | AB         | A′B                |

### 🧠 Memory trick

Addition:

```text id="r1j2p5"
Carry=AB
```

Subtraction:

```text id="x73fyd"
Borrow=A′B
```

---

# 10. Full Subtractor ⭐⭐⭐⭐⭐

A Full Subtractor subtracts **three 1-bit inputs**:

```text id="t0ybgc"
A−B−Bin
```

Inputs:

```text id="qyxqcv"
A, B, Bin
```

Outputs:

```text id="vh2d1r"
Difference, Bout
```

Here:

* Bin = Borrow-in
* Bout = Borrow-out

---

# 11. Full Subtractor Truth Table

| A | B | Bin | Difference | Bout |
| - | - | --- | ---------- | ---- |
| 0 | 0 | 0   | 0          | 0    |
| 0 | 0 | 1   | 1          | 1    |
| 0 | 1 | 0   | 1          | 1    |
| 0 | 1 | 1   | 0          | 1    |
| 1 | 0 | 0   | 1          | 0    |
| 1 | 0 | 1   | 0          | 0    |
| 1 | 1 | 0   | 0          | 0    |
| 1 | 1 | 1   | 1          | 1    |

---

# 12. Full Subtractor Difference ⭐⭐⭐⭐⭐

The Difference equation is:

```text id="ae8j3u"
D=A⊕B⊕Bin
```

Notice the similarity with Full Adder:

### Full Adder

```text id="53t1aw"
Sum=A⊕B⊕Cin
```

### Full Subtractor

```text id="9r2g4r"
Difference=A⊕B⊕Bin
```

Very easy to remember.

---

# 13. Full Subtractor Borrow Equation ⭐⭐⭐⭐⭐

The Borrow-out equation is:

```text id="pddqgq"
Bout=A′B+A′Bin+BBin
```

This is important for placement questions.

---

# 14. Full Subtractor Using Two Half Subtractors

Just like a Full Adder can be built from two Half Adders:

A Full Subtractor can be built using:

```text id="gq8n2l"
2 Half Subtractors + 1 OR
```

Conceptually:

```text id="sg3k2x"
       A ─────┐
              ▼

          ┌─────────┐

B ───────►│   HS1   │

          └────┬────┘

               │ D1

               ▼

          ┌─────────┐

Bin ─────►│   HS2   │

          └────┬────┘

               │

               D



Borrow1 ──┐

           ├── OR ──► Bout

Borrow2 ──┘
```

---

# 15. ⭐ Addition vs Subtraction

Compare the fundamental equations:

### Half Adder

```text id="zdt8x1"
Sum=A⊕B
Carry=AB
```

### Half Subtractor

```text id="7fm3c4"
Difference=A⊕B
Borrow=A′B
```

Notice:

```text id="ipz12t"
Sum and Difference use XOR
```

but:

```text id="3kgyxg"
Carry and Borrow are different
```

---

# 16. Subtraction Using 2's Complement ⭐⭐⭐⭐⭐

This is **very important for VLSI and digital interviews**.

Instead of building a completely separate subtraction circuit, digital systems commonly perform:

```text id="m9l0na"
A−B=A+(2’s complement of B)
```

Therefore, an adder can be used to perform subtraction.

---

# 17. Example

Calculate:

```text id="6qy6wc"
5−3
```

Using 4 bits:

```text id="wy6l36"
5 = 0101
```

```text id="7wut6o"
3 = 0011
```

Find 2's complement of 3.

### Step 1: 1's complement

```text id="tuj3kp"
0011
```

↓

```text id="1r5euw"
1100
```

### Step 2: Add 1

```text id="5j59y3"
1100
+0001
-----
1101
```

So:

```text id="v0t3v9"
2′s complement(0011)=1101
```

Now add:

```text id="km6dgt"
  0101
+ 1101
------
10010
```

Discard the final carry:

```text id="zjd6q7"
0010
```

Therefore:

```text id="6ro4n0"
5−3=2
```

---

# 18. Why This Is Important in Hardware ⭐⭐⭐⭐⭐

A single adder can be used for both:

```text id="4h8d7m"
A+B
```

and:

```text id="4mwz5h"
A−B
```

This reduces hardware duplication.

That's why the **adder-subtractor circuit** is extremely important.

---

# 19. Adder-Subtractor Concept

A common design uses XOR gates controlled by a mode signal.

Let:

```text id="fxbs07"
M=0→Addition
M=1→Subtraction
```

For each B bit:

```text id="gdf8kk"
Bi′=Bi⊕M
```

And:

```text id="v6j4dj"
Cin=M
```

### When M=0:

```text id="kh34dm"
Bi⊕0=Bi
```

and:

```text id="7a3lso"
Cin=0
```

So:

```text id="0g30o9"
A+B
```

### When M=1:

```text id="btdj5n"
Bi⊕1=Bi′
```

and:

```text id="jj15g9"
Cin=1
```

Therefore:

```text id="8asx3u"
A+B′+1
```

which is:

```text id="07wxns"
A−B
```

---

# 20. ⭐ Adder-Subtractor Diagram

```text id="lo9y7z"
             M

             │

B ──────┐    │
        ▼    ▼

       XOR ◄─┘

        │

        ▼

       B'

        │

        ▼

A ──────────────┐
                │
                ▼

             ┌───────┐
             │  RCA  │──── Result
             └───────┘
                ▲
                │
                M

             (Cin)
```

### Memory:

```text id="d8qoxj"
M = 0 → ADD
```

```text id="k2d7id"
M = 1 → SUBTRACT
```

---

# 🧠 SUBTRACTOR QUICK REVISION

```text id="x4q4ps"
HALF SUBTRACTOR
```

────────────────────────

### Inputs:

```text id="r1q02m"
A, B
```

### Outputs:

```text id="9ch8rr"
Difference, Borrow
```

### Difference:

```text id="zq0lpm"
A ⊕ B
```

### Borrow:

```text id="n6x7g0"
A′B
```

---

```text id="pl0yqt"
FULL SUBTRACTOR
```

────────────────────────

### Inputs:

```text id="23twmj"
A, B, Bin
```

### Outputs:

```text id="e7q7j7"
Difference, Bout
```

### Difference:

```text id="m9g4ag"
A ⊕ B ⊕ Bin
```

### Borrow:

```text id="b49kqd"
A′B + A′Bin + BBin
```

---

### IMPORTANT:

Half Subtractor:

```text id="s8h0ge"
No Borrow-in
```

Full Subtractor:

```text id="r1z9bj"
Has Borrow-in
```

---

### 2's Complement:

```text id="k2h5tb"
A - B = A + (~B + 1)
```

---

### ADDER-SUBTRACTOR:

```text id="c6s0f8"
M=0 → Addition
```

```text id="8q8nb3"
M=1 → Subtraction
```
