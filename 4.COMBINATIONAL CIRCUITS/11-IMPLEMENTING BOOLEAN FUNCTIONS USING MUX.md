# IMPLEMENTING BOOLEAN FUNCTIONS USING MUX ⭐⭐⭐⭐⭐

This is one of the **most important placement topics in Phase 4**.

You may get questions like:

> "Implement F(A,B,C)=Σm(1,2,5,7) using a 4:1 MUX."

The key is learning **how to choose select lines and determine the MUX inputs**.

---

# 1. Why Can a MUX Implement a Boolean Function?

A MUX selects one of its inputs based on the select lines.

Therefore, if we connect:

* `0`
* `1`
* a variable
* or its complement

to the data inputs appropriately, the MUX can produce a desired Boolean function.

### ⭐ Core idea

> **MUX can act as a programmable Boolean function generator.**

---

# 2. Easiest Case: Number of Variables = Select Lines

Suppose:

```text
F(A,B)=Σm(1,2)
```

There are **2 variables**.

A 4:1 MUX has:

```text
2 select lines
```

So use:

```text
S1=A,S0=B
```

---

# 3. Step-by-Step Example ⭐⭐⭐⭐⭐

Implement:

```text
F(A,B)=Σm(1,2)
```

### Step 1: Write truth table

| A | B | Minterm | F |
| - | - | ------- | - |
| 0 | 0 | m0      | 0 |
| 0 | 1 | m1      | 1 |
| 1 | 0 | m2      | 1 |
| 1 | 1 | m3      | 0 |

---

### Step 2: Select lines

Use:

```text
S1=A
S0=B
```

---

### Step 3: Assign MUX inputs

Because:

```text
AB = 00 → I0
```

```text
AB = 01 → I1
```

```text
AB = 10 → I2
```

```text
AB = 11 → I3
```

Look at F:

```text
I0 = 0
```

```text
I1 = 1
```

```text
I2 = 1
```

```text
I3 = 0
```

Therefore:

```text
I0=0, I1=1, I2=1, I3=0
```

Done.

---

# 4. General Method ⭐⭐⭐⭐⭐

When implementing an n-variable function using a 2ⁿ:1 MUX:

### Step 1

Choose all variables as select lines.

### Step 2

Write the truth table.

### Step 3

Map each input combination to the corresponding MUX input.

### Step 4

Connect each MUX input to `0` or `1`.

### Memory trick:

> **Truth table → Select lines → Data inputs**

---

# 5. Example With 3 Variables

Implement:

```text
F(A,B,C)=Σm(1,3,5,7)
```

Use an:

```text
8:1 MUX
```

because:

```text
2³=8
```

Select lines:

```text
S2=A, S1=B, S0=C
```

---

### MUX input table

| ABC | MUX input | F |
| --- | --------- | - |
| 000 | I0        | 0 |
| 001 | I1        | 1 |
| 010 | I2        | 0 |
| 011 | I3        | 1 |
| 100 | I4        | 0 |
| 101 | I5        | 1 |
| 110 | I6        | 0 |
| 111 | I7        | 1 |

Therefore:

```text
I0=0, I1=1, I2=0, I3=1,I4=0, I5=1, I6=0, I7=1
```

Notice:

```text
F=C
```

But the MUX implementation still works.

---

# 6. ⭐ More Interesting Case

Now suppose:

```text
F(A,B,C)=Σm(1,2,6,7)
```

Use a **4:1 MUX** instead of an 8:1 MUX.

Why?

A 4:1 MUX has only:

```text
2
```

select lines.

We have:

```text
3
```

variables.

So we use **two variables as select lines**, and the remaining variable appears in the data inputs.

---

# 7. Choose Select Lines

Let's choose:

```text
S1=A,S0=B
```

The remaining variable is:

```text
C
```

Now examine each AB combination.

---

# 8. Determine I0

For:

```text
AB=00
```

Possible combinations:

```text
ABC = 000 → m0 → F=0
```

```text
ABC = 001 → m1 → F=1
```

As C changes:

```text
C=0 → F=0
```

```text
C=1 → F=1
```

Therefore:

```text
I0=C
```

---

# 9. Determine I1

For:

```text
AB=01
```

Possible:

```text
010 → m2 → F=1
```

```text
011 → m3 → F=0
```

So:

```text
C=0 → F=1
```

```text
C=1 → F=0
```

Therefore:

```text
I1=C
```

---

# 10. Determine I2

For:

```text
AB=10
```

Possible:

```text
100 → m4 → F=0
```

```text
101 → m5 → F=0
```

Therefore:

```text
I2=0
```

---

# 11. Determine I3

For:

```text
AB=11
```

Possible:

```text
110 → m6 → F=1
```

```text
111 → m7 → F=1
```

Therefore:

```text
I3=1
```

---

# 12. Final Answer ⭐⭐⭐⭐⭐

For:

```text
F(A,B,C)=Σm(1,2,6,7)
```

using a 4:1 MUX:

```text
S1=A, S0=B
```

and:

```text
I0=C
I1=C
I2=0
I3=1
```

This type of question is **very important for placement exams**.

---

# 13. ⭐ The Four Possible MUX Data Inputs

When implementing a 3-variable function using a 4:1 MUX, the data input will generally become one of:

```text
0, 1, C, C
```

This is an excellent shortcut.

### Memory trick:

For the remaining variable C:

| F when C=0 | F when C=1 | MUX input |
| ---------: | ---------: | --------- |
|          0 |          0 | 0         |
|          0 |          1 | C         |
|          1 |          0 | C         |
|          1 |          1 | 1         |

⭐ **Memorize this table.**

---

# 14. Another Important Shortcut ⭐⭐⭐⭐⭐

For a 4:1 MUX implementing a 3-variable function:

```text
00 → I0
```

```text
01 → I1
```

```text
10 → I2
```

```text
11 → I3
```

For each row, inspect the remaining variable.

Then determine whether that MUX input should be:

```text
0, 1, X, X′
```

---

# 15. MUX Function Implementation — Exam Strategy

When you see:

> Implement F(A,B,C)=Σm(...) using 4:1 MUX

Immediately think:

```text
1. 4:1 → 2 select lines
```

```text
2. Choose 2 variables as select lines
```

```text
3. Remaining variable = data variable
```

```text
4. Group truth-table rows according to select values
```

```text
5. Determine each I0-I3
```

```text
6. Each input becomes 0, 1, X or X'
```

⭐ This is a **high-value placement shortcut**.

---

# 16. Verilog Relevance ⭐⭐⭐⭐

A MUX-based Boolean function can also be represented in RTL.

For example:

```verilog
always_comb begin
    case ({A,B})
        2'b00: Y = C;
        2'b01: Y = ~C;
        2'b10: Y = 1'b0;
        2'b11: Y = 1'b1;
    endcase
end
```

This corresponds to:

```text
I0=C,I1=C,I2=0,I3=1
```

---

# 🧠 FINAL MUX FUNCTION REVISION

```text
BOOLEAN FUNCTION USING MUX
```

────────────────────────────────

### Case 1:

Number of variables = select lines

Use:

```text
2^n : 1 MUX
```

Connect:

MUX inputs directly to 0/1

according to truth table.

---

### Case 2:

Variables > select lines

Use remaining variable(s)

as MUX data inputs.

For 3 variables using 4:1 MUX:

Data input can be:

```text
0
1
X
X'
```

---

### IMPORTANT SHORTCUT:

```text
F(C=0), F(C=1)
```

```text
0,0 → 0
```

```text
0,1 → C
```

```text
1,0 → C'
```

```text
1,1 → 1
```
