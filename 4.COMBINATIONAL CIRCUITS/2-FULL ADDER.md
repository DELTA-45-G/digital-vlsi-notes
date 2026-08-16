# FULL ADDER ⭐⭐⭐⭐⭐

A **Full Adder** is one of the most important combinational circuits for VLSI placements.

---

## 1. What is a Full Adder?

A Full Adder is a combinational circuit that adds **three 1-bit inputs**:

```text id="lq1f6k"
A, B, Cin
```

and produces two outputs:

```text id="aj4mnl"
Sum, Cout
```

```text id="9jfx5x"
             ┌─────────────┐

A ──────────►│             │

B ──────────►│ FULL ADDER  │───► Sum

Cin ────────►│             │───► Cout

             └─────────────┘
```

### ⭐ Main difference

Half Adder:

```text id="k6k7v5"
2 inputs
```

Full Adder:

```text id="0dgj5r"
3 inputs
```

The third input is:

```text id="v74jpw"
Cin = Carry-in
```

---

# 2. Why Do We Need a Full Adder?

Consider adding two multi-bit binary numbers:

```text id="e7gq4y"
      1011
    + 0110
    ------
      10001
```

When we add each bit, a carry can come from the previous bit.

For example:

```text id="1s3r7x"
       carry
         ↓

       A B
```

The circuit must consider:

* Current bit of first number
* Current bit of second number
* Carry from previous position

That's exactly what a Full Adder does.

---

# 3. Full Adder Inputs and Outputs ⭐⭐⭐⭐⭐

### Inputs

```text id="jbzj3y"
A, B, Cin
```

### Outputs

```text id="0o8r7h"
Sum, Cout
```

So:

```text id="2d7fli"
3 inputs, 2 outputs
```

---

# 4. Full Adder Truth Table ⭐⭐⭐⭐⭐

There are three inputs, so:

```text id="zvdrf4"
2³=8
```

possible combinations.

| A | B | Cin | Sum | Cout |
| - | - | --- | --- | ---- |
| 0 | 0 | 0   | 0   | 0    |
| 0 | 0 | 1   | 1   | 0    |
| 0 | 1 | 0   | 1   | 0    |
| 0 | 1 | 1   | 0   | 1    |
| 1 | 0 | 0   | 1   | 0    |
| 1 | 0 | 1   | 0   | 1    |
| 1 | 1 | 0   | 0   | 1    |
| 1 | 1 | 1   | 1   | 1    |

---

# 5. Understanding the Truth Table

Let's take:

```text id="mq2ag0"
A=1, B=0, Cin=1
```

We calculate:

```text id="w0xy4i"
1+0+1=2
```

Binary:

```text id="fo1h8h"
2=10₂
```

Therefore:

```text id="0vmh2n"
Sum  = 0
```

```text id="66h0m8"
Cout = 1
```

---

Another example:

```text id="g4v4q0"
1+1+1=3
```

Binary:

```text id="y3s6z7"
3=11₂
```

Therefore:

```text id="iv2vo6"
Sum  = 1
```

Cout = 1

---

# 6. Full Adder Sum Equation ⭐⭐⭐⭐⭐

The Sum is:

```text id="l0r15f"
Sum=A⊕B⊕Cin
```

This is one of the **most important formulas** to memorize.

---

# 7. Why XOR?

XOR produces `1` when an **odd number of inputs are 1**.

```text id="k8upng"
Number of 1s | XOR result
--------------------------
0             | 0
1             | 1
2             | 0
3             | 1
```

The Sum column follows exactly this pattern.

Therefore:

```text id="3n55zr"
Sum=A⊕B⊕Cin
```

---

# 8. Full Adder Carry Equation ⭐⭐⭐⭐⭐

The Carry output is:

```text id="up59ei"
Cout=AB+BCin+ACin
```

This is another very important placement formula.

---

## 9. Understanding the Carry Equation

Carry becomes `1` whenever **at least two of the three inputs are 1**.

For example:

### Case 1

```text id="0bgd0p"
A=1,B=1,Cin=0
```

Then:

```text id="w9e6vv"
AB=1
```

Therefore:

```text id="0pyj0r"
Cout=1
```

---

### Case 2

```text id="3hy3m5"
A=1,B=0,Cin=1
```

Then:

```text id="bp84id"
ACin=1
```

Therefore:

```text id="y1q0u7"
Cout=1
```

---

### Case 3

```text id="3z3z3o"
A=0,B=1,Cin=1
```

Then:

```text id="a1v5cr"
BCin=1
```

Therefore:

```text id="qf4udq"
Cout=1
```

---

### Case 4

```text id="o8j9d7"
A=B=Cin=1
```

All three products are 1:

```text id="zj1j4d"
AB=1
BCin=1
ACin=1
```

Therefore:

```text id="38a0ym"
Cout=1
```

---

# 10. ⭐ Majority Function

The Full Adder Carry is essentially a **majority function**.

Why?

Because:

> If at least **two out of three inputs are 1**, Carry = 1.

```text id="g9j3ll"
A B Cin | Cout
----------------
0 0  0  | 0
0 0  1  | 0
0 1  0  | 0
0 1  1  | 1
1 0  0  | 0
1 0  1  | 1
1 1  0  | 1
1 1  1  | 1
```

This is a useful interview observation.

---

# 11. Full Adder Using Two Half Adders ⭐⭐⭐⭐⭐

This is **very frequently asked**.

A Full Adder can be constructed using:

```text id="08mhq7"
2 Half Adders + 1 OR gate
```

### Structure

```text id="73bld9"
                 ┌──────────────┐

A ──────────────►│ Half Adder 1 │

B ──────────────►│              │

                 └──────┬───────┘

                        │

                  S1    │ C1

                   │    │

                   ▼    │

              ┌─────────┴───┐

Cin ─────────►│ Half Adder 2│

              │             │

              └──────┬──────┘

                     │ C2

                     ▼

                 ┌───────┐

C1 ─────────────►│  OR   │───► Cout

C2 ─────────────►│       │

                 └───────┘



                S2 ─────────► Sum
```

Let's understand it.

---

## 12. First Half Adder

Inputs:

```text id="w9xg8x"
A,B
```

Outputs:

```text id="7tq3yk"
S1=A⊕B
C1=AB
```

---

## 13. Second Half Adder

Inputs:

```text id="4d3a7q"
S1,Cin
```

Therefore:

```text id="h3z1jh"
Sum=S1⊕Cin
```

Substitute:

```text id="xvjsnq"
Sum=A⊕B⊕Cin
```

---

## 14. Carry from the Two Half Adders

First Half Adder:

```text id="db6d7w"
C1=AB
```

Second Half Adder:

```text id="4c3e4t"
C2=S1Cin
```

Therefore:

```text id="j8hr9m"
Cout=C1+C2
```

```text id="g6n1mb"
Cout=AB+(A⊕B)Cin
```

This can be simplified to:

```text id="j7mz5c"
Cout=AB+ACin+BCin
```

---

# 15. ⭐ Important Full Adder Equations

Memorize these:

### Sum

```text id="psq7ao"
S=A⊕B⊕Cin
```

### Carry

```text id="8qk6c9"
Cout=AB+ACin+BCin
```

Alternative form:

```text id="z8x5s4"
Cout=AB+(A⊕B)Cin
```

Both are correct.

---

# 16. Half Adder vs Full Adder ⭐⭐⭐⭐⭐

| Feature            | Half Adder | Full Adder   |
| ------------------ | ---------- | ------------ |
| Inputs             | 2          | 3            |
| Carry-in           | ❌          | ✅            |
| Outputs            | 2          | 2            |
| Sum                | A⊕B        | A⊕B⊕Cin      |
| Carry              | AB         | AB+ACin+BCin |
| Basic construction | XOR + AND  | 2 HA + OR    |

---

# 17. Full Adder Hardware Importance

Full Adders are fundamental building blocks of:

* Ripple Carry Adders
* Carry Look-Ahead Adders
* ALUs
* Arithmetic circuits
* CPUs
* DSP hardware

⭐ This is why Full Adder questions are extremely common in VLSI interviews.

---

# 18. Verilog Relevance ⭐⭐⭐⭐

A basic Verilog implementation:

```verilog id="n9wqf4"
module full_adder(
    input  A,
    input  B,
    input  Cin,
    output Sum,
    output Cout
);

assign Sum  = A ^ B ^ Cin;
assign Cout = (A & B) | (A & Cin) | (B & Cin);

endmodule
```

The important operators:

```text id="ahd1i6"
^  → XOR
```

```text id="j5dygr"
&  → AND
```

```text id="i3y8pa"
|  → OR
```

---

# 19. Placement Shortcut 🧠

For a Full Adder:

### Sum

Think:

> **Odd number of 1s → Sum = 1**

### Carry

Think:

> **Two or more 1s → Carry = 1**

This lets you answer many MCQs without calculating the entire expression.

---

# 20. Example

Given:

```text id="g2v5uz"
A=1,B=0,Cin=1
```

There are two `1`s.

Therefore:

```text id="d0qf4g"
Sum=0
```

and:

```text id="6e8xdi"
Cout=1
```

---

# 🧠 FULL ADDER — QUICK REVISION

```text id="ly7g1v"
FULL ADDER
```

────────────────────────────

### Inputs:

```text id="60swkw"
A, B, Cin
```

### Outputs:

```text id="g7xkgk"
Sum, Cout
```

### Number of combinations:

```text id="f3rd0j"
2³ = 8
```

### SUM:

```text id="i1ryp9"
A ⊕ B ⊕ Cin
```

### CARRY:

```text id="4s2pyl"
AB + ACin + BCin
```

### Alternative Carry:

```text id="xglxcu"
AB + (A ⊕ B)Cin
```

### Construction:

```text id="7pk1th"
2 Half Adders + 1 OR gate
```

### Key idea:

```text id="0j7yy2"
Sum   → odd number of 1s
```

```text id="5d6r7j"
Carry → at least two 1s
```

### Half Adder:

```text id="f7zj9v"
2 inputs, no Cin
```

### Full Adder:

```text id="h5o4mi"
3 inputs, has Cin
```
