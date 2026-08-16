# MULTIPLEXER (MUX) ⭐⭐⭐⭐⭐

The **Multiplexer** is one of the **most important combinational circuits for VLSI placements**.

You should be very comfortable with:

* MUX structure
* Select lines
* Truth table
* Boolean equation
* 2:1 MUX
* 4:1 MUX
* MUX as a universal function-implementation tool

---

# 1. What is a Multiplexer?

A **Multiplexer**, commonly called a **MUX**, is a circuit that selects **one of many input signals** and sends the selected signal to a **single output**.

### Memory trick:

> **MUX = Many → One**

```text id="i7qk2z"
I0 ─────┐
I1 ─────┤
I2 ─────┤──► MUX ───► Y
I3 ─────┤
        │
       Select
```

The select lines decide **which input reaches the output**.

---

# 2. Why Do We Need a MUX?

Suppose four different data signals exist:

```text id="v6w3kz"
Data A ──┐
Data B ──┤
Data C ──┤──► ? ──► CPU
Data D ──┘
```

We don't want all four connected to the output simultaneously.

We need to choose **one**.

A MUX does exactly that.

For example:

```text id="9x6k3v"
Select = 10
```

```text id="x2f8q5"
Data C ─────────► Output
```

---

# 3. 2:1 MUX ⭐⭐⭐⭐⭐

A **2:1 MUX** has:

* 2 data inputs
* 1 select line
* 1 output

```text id="h5m2q8"
I0 ─────┐
        │
        ├──► MUX ───► Y
        │
I1 ─────┘

          ▲
          │
          S
```

Why only one select line?

Because:

```text id="m8p3z1"
2¹=2
```

Therefore:

```text id="k4r7y2"
1 select line → 2 inputs
```

---

# 4. 2:1 MUX Truth Table ⭐⭐⭐⭐⭐

| S | Y  |
| - | -- |
| 0 | I0 |
| 1 | I1 |

Very simple:

```text id="v3q8m1"
S=0⇒Y=I0
```

```text id="n7p2k5"
S=1⇒Y=I1
```

### 🧠 Memory trick

> **Select 0 → Input 0**

> **Select 1 → Input 1**

---

# 5. 2:1 MUX Boolean Equation ⭐⭐⭐⭐⭐

The equation is:

```text id="z8q4m6"
Y=S′I0+SI1
```

Let's understand it.

### When S = 0:

```text id="q6m2b9"
Y=0I0+1I1
Y=I0+0
Y=I0
```

### When S = 1:

```text id="r3k8w2"
Y=1I0+0I1
Y=0+I1
Y=I1
```

Perfect.

---

# 6. Internal Gate Implementation

A 2:1 MUX can be built using:

* 1 NOT gate
* 2 AND gates
* 1 OR gate

```text id="k5v1z8"
          ┌── NOT ──┐
          │         │
          │         ▼
S ────────┤        S'

          │

I0 ───────AND──────┐
                   │
I1 ───────AND──────┤
                   OR ───► Y
                   │
S ─────────────────┘
```

Because:

```text id="p7y2m4"
Y=S′I0+SI1
```

---

# 7. 4:1 MUX ⭐⭐⭐⭐⭐

A 4:1 MUX has:

* 4 data inputs
* 2 select lines
* 1 output

```text id="w6q3n9"
I0 ─────┐
I1 ─────┤
I2 ─────┤──► 4:1 MUX ───► Y
I3 ─────┘

         ▲

       S1 S0
```

Why 2 select lines?

Because:

```text id="c5m9x2"
2²=4
```

Therefore:

```text id="z7k3p1"
2 select lines → 4 inputs
```

---

# 8. 4:1 MUX Truth Table ⭐⭐⭐⭐⭐

| S1 | S0 | Output |
| -- | -- | ------ |
| 0  | 0  | I0     |
| 0  | 1  | I1     |
| 1  | 0  | I2     |
| 1  | 1  | I3     |

### Memory:

```text id="r8v3m1"
S1 S0
─────

00 → I0
01 → I1
10 → I2
11 → I3
```

---

# 9. 4:1 MUX Equation

The Boolean equation is:

```text id="p4n8x7"
Y=S1′S0′I0+S1′S0I1+S1S0′I2+S1S0I3
```

You don't necessarily need to derive this from memory every time.

Use the truth table.

---

# 10. Number of Select Lines ⭐⭐⭐⭐⭐

This is a **very common aptitude/placement question**.

For N inputs:

```text id="h7m2q4"
Select lines=log₂N
```

Examples:

### 2:1 MUX

```text id="w3k9p1"
log₂2=1
```

### 4:1 MUX

```text id="c8m4v6"
log₂4=2
```

### 8:1 MUX

```text id="z2q7n5"
log₂8=3
```

### 16:1 MUX

```text id="p6r3x8"
log₂16=4
```

### Memory trick:

```text id="m4k8z2"
2ⁿ inputs ⇒ n select lines
```

---

# 11. MUX vs DEMUX ⭐⭐⭐⭐⭐

Don't confuse these.

### MUX

```text id="a7p3y6"
Many inputs → One output
```

### DEMUX

```text id="n2v8k4"
One input → Many outputs
```

Think:

```text id="q5m1x9"
MUX:

Many ───► One
```

```text id="s8k4p2"
DEMUX:

One ───► Many
```

---

# 12. MUX as a Function Implementer ⭐⭐⭐⭐⭐

This is **extremely important for placements**.

A MUX can be used to implement Boolean functions.

For example:

```text id="v6p2m8"
F(A,B)=Σm(1,2)
```

A 4:1 MUX can directly implement this function by using:

```text id="k3q7n5"
A,B
```

as select lines.

---

# 13. Example: Implement F(A,B)=Σm(1,2)

Truth table:

| A | B | F |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Use:

```text id="x4m8p2"
S1=A,S0=B
```

Then:

```text id="r7k3v9"
AB = 00 → I0 = 0
```

```text id="j2q5m8"
AB = 01 → I1 = 1
```

```text id="c8v4n6"
AB = 10 → I2 = 1
```

```text id="p3y7k1"
AB = 11 → I3 = 0
```

Therefore:

```text id="w6m2q9"
I0=0,I1=1,I2=1,I3=0
```

This implements:

```text id="h4n8x3"
F=Σm(1,2)
```

---

# 14. ⭐ General MUX Function Shortcut

If the number of variables equals the number of select-line variables:

> **Use those variables as select lines and connect each MUX data input to 0 or 1 according to the truth table.**

Example:

```text id="q7m3x8"
F(A,B,C)=Σm(1,3,5,7)
```

Use an **8:1 MUX**.

Select lines:

```text id="n5p2k7"
S2=A,S1=B,S0=C
```

Then:

```text id="v8q4m1"
I0 = 0
I1 = 1
I2 = 0
I3 = 1
I4 = 0
I5 = 1
I6 = 0
I7 = 1
```

---

# 15. ⭐ Another Important MUX Shortcut

You don't always need 2ⁿ:1 MUX.

For an n-variable function, you can use a smaller MUX and connect the remaining variable(s) to the data inputs.

This is a common interview problem.

We'll practice this carefully after completing the basic MUX concepts.

---

# 16. Real Hardware Applications ⭐⭐⭐⭐

MUXes are used extensively in:

* CPU datapaths
* ALUs
* Register selection
* Bus selection
* Communication systems
* Control logic
* Processor pipelines
* FPGA logic

For example, a CPU may need to choose whether an ALU input comes from:

```text id="z3q7m5"
Register
   │
   ├────► MUX ───► ALU
   │
Memory
```

The select signal determines the source.

---

# 17. Verilog Relevance ⭐⭐⭐⭐⭐

A 2:1 MUX:

```verilog
assign Y = S ? I1 : I0;
```

This means:

```text id="j5p8x2"
S = 0 → I0
```

```text id="k7m3q9"
S = 1 → I1
```

Equivalent `if` form:

```verilog
always_comb begin
    if (S)
        Y = I1;
    else
        Y = I0;
end
```

⭐ Knowing how to recognize a MUX from RTL is useful in VLSI interviews.

---

# 🧠 MUX QUICK REVISION

```text id="p4m8x1"
MULTIPLEXER
```

────────────────────────────

### MUX = Many → One

### 2:1 MUX:

```text id="z7q2m5"
2 inputs
1 select
1 output
```

### Equation:

```text id="c4n8x6"
Y = S'I0 + SI1
```

### 4:1 MUX:

```text id="w3p7k2"
4 inputs
2 selects
1 output
```

### Selection:

```text id="n6m2q9"
00 → I0
01 → I1
10 → I2
11 → I3
```

### General:

```text id="x5k8p3"
2^n inputs → n select lines
```

### Select lines:

```text id="r7m4q1"
log₂(number of inputs)
```

### Applications:

CPU datapath

ALU

Bus selection

Register selection

### Important:

MUX can implement Boolean functions.

### Memory:

```text id="v2q6m8"
MUX → Many to One

DEMUX → One to Many
```
