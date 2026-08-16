# PHASE 4 — COMBINATIONAL CIRCUITS

## Placement Questions + Answers ⭐⭐⭐⭐⭐

---

# PART A — BASIC COMBINATIONAL LOGIC

### Q1. What is a combinational circuit?

**Answer:**

A combinational circuit is a digital circuit whose output depends only on the **present inputs**.

```text
Output=f(Present Inputs)
```

Examples:

* Adder
* Subtractor
* MUX
* DEMUX
* Encoder
* Decoder
* Comparator

---

### Q2. Does a combinational circuit have memory?

**Answer:** No.

It does not store previous input information.

---

### Q3. What is the difference between combinational and sequential circuits?

| Combinational                    | Sequential                                 |
| -------------------------------- | ------------------------------------------ |
| Output depends on present inputs | Output depends on present + previous state |
| No memory                        | Has memory                                 |
| Usually no clock                 | Usually clock-controlled                   |
| MUX, adder, decoder              | Flip-flop, counter, register               |

⭐ **Placement shortcut:**

> Combinational → No memory
> Sequential → Memory

---

# PART B — HALF ADDER ⭐⭐⭐⭐⭐

### Q4. What is a Half Adder?

**Answer:**

A Half Adder adds two 1-bit binary numbers.

Inputs:

```text
A,B
```

Outputs:

```text
Sum,Carry
```

---

### Q5. What is the Half Adder Sum equation?

```text
Sum=A⊕B
```

---

### Q6. What is the Half Adder Carry equation?

```text
Carry=AB
```

---

### Q7. How many inputs and outputs does a Half Adder have?

**Answer:**

```text
2 inputs, 2 outputs
```

---

### Q8. Which gates are required to implement a Half Adder?

**Answer:**

* 1 XOR → Sum
* 1 AND → Carry

---

### Q9. What is the output of a Half Adder when A = 1 and B = 1?

```text
Sum=1⊕1=0
Carry=1⋅1=1
```

Therefore:

```text
Sum=0, Carry=1
```

---

### Q10. Why is it called a "Half" Adder?

**Answer:**

Because it does **not accept carry-in** from a previous bit.

---

# PART C — FULL ADDER ⭐⭐⭐⭐⭐

### Q11. What is a Full Adder?

A Full Adder adds:

```text
A+B+Cin
```

It has:

```text
3 inputs, 2 outputs
```

---

### Q12. What are the Full Adder equations?

```text
Sum=A⊕B⊕Cin
Cout=AB+BCin+ACin
```

---

### Q13. Why do we need a Full Adder?

**Answer:**

Because when adding multiple-bit numbers, an intermediate bit may receive a **carry from the previous bit**.

---

### Q14. Can a Full Adder be built using Half Adders?

**Answer:** Yes.

```text
2 Half Adders + 1 OR gate
```

---

### Q15. How many Half Adders are required to construct one Full Adder?

```text
2
```

plus one OR gate.

---

### Q16. What happens when A=B=Cin=1?

```text
Sum=1⊕1⊕1=1
Cout=1
```

Therefore:

```text
Sum=1, Carry=1
```

---

# PART D — RIPPLE CARRY ADDER ⭐⭐⭐⭐⭐

### Q17. What is a Ripple Carry Adder?

A Ripple Carry Adder is formed by connecting multiple Full Adders in cascade.

For an n-bit addition:

```text
n Full Adders
```

are used.

---

### Q18. Why is it called Ripple Carry?

Because the carry propagates from one Full Adder to the next.

```text
FA0 → FA1 → FA2 → FA3
```

```text
 C0     C1     C2     C3
```

The carry "ripples" through the stages.

---

### Q19. What is the major disadvantage of RCA?

```text
Large propagation delay
```

because each stage waits for the previous carry.

---

### Q20. How many Full Adders are required for a 16-bit RCA?

```text
16
```

---

### Q21. What happens to delay as the number of bits increases?

The worst-case carry propagation delay increases approximately with the number of stages.

Therefore:

```text
More bits → More delay
```

---

# PART E — CARRY LOOK-AHEAD ADDER ⭐⭐⭐⭐⭐

### Q22. Why is Carry Look-Ahead Adder faster than Ripple Carry Adder?

**Answer:**

CLA calculates carries using **Generate and Propagate logic**, rather than waiting for carry to ripple through every Full Adder.

---

### Q23. Define Generate and Propagate.

For bit i:

```text
Gi=AiBi
Pi=Ai⊕Bi
```

---

### Q24. What does Generate mean?

If:

```text
Gi=1
```

the bit position generates a carry regardless of the incoming carry.

---

### Q25. What does Propagate mean?

A bit propagates an incoming carry to the next stage when the propagate condition is satisfied.

---

### Q26. What is the main advantage of CLA?

```text
Higher speed / lower carry propagation delay
```

---

### Q27. RCA vs CLA?

| RCA              | CLA                    |
| ---------------- | ---------------------- |
| Simple           | More complex           |
| Slower           | Faster                 |
| Carry ripples    | Carry calculated ahead |
| Smaller hardware | More hardware          |

⭐ Placement question:

> **Why don't we always use CLA?**

**Answer:** Because CLA requires more hardware and more complex logic, increasing area and wiring complexity.

---

# PART F — SUBTRACTORS ⭐⭐⭐⭐⭐

### Q28. What is a Half Subtractor?

It subtracts two 1-bit numbers.

Inputs:

```text
A,B
```

Outputs:

```text
Difference,Borrow
```

---

### Q29. Half Subtractor equations?

```text
D=A⊕B
Borrow=A′B
```

---

### Q30. When does a Half Subtractor generate Borrow?

When:

```text
A=0, B=1
```

---

### Q31. What is a Full Subtractor?

It performs:

```text
A−B−Bin
```

It has:

```text
3 inputs, 2 outputs
```

---

### Q32. Full Subtractor Difference equation?

```text
D=A⊕B⊕Bin
```

---

### Q33. Full Subtractor Borrow equation?

```text
Bout=A′B+A′Bin+BBin
```

---

### Q34. How can binary subtraction be performed using addition?

Using 2's complement:

```text
A−B=A+B+1
```

More precisely:

```text
A−B=A+2′s complement(B)
```

---

# PART G — ADDER-SUBTRACTOR ⭐⭐⭐⭐⭐

### Q35. How can one circuit perform both addition and subtraction?

Use:

* XOR gates on the B inputs
* Mode/control signal M
* M as initial carry-in

---

### Q36. What happens when M=0?

```text
A+B
```

---

### Q37. What happens when M=1?

```text
A−B
```

because:

```text
B⊕1=B′
```

and:

```text
Cin=1
```

giving:

```text
A+B′+1
```

---

### Q38. Why is an adder-subtractor useful in hardware?

**Answer:**

One hardware structure can perform both operations, reducing duplicated arithmetic hardware.

---

# PART H — COMPARATOR ⭐⭐⭐⭐⭐

### Q39. What is a digital comparator?

A comparator compares two binary numbers and determines:

```text
A>B, A=B, A<B
```

---

### Q40. Is a comparator combinational or sequential?

```text
Combinational
```

---

### Q41. What is the equation for A>B for a 1-bit comparator?

```text
A>B=AB′
```

---

### Q42. What is the equation for A<B?

```text
A<B=A′B
```

---

### Q43. What gate is commonly used for equality detection?

```text
XNOR
```

---

### Q44. Why is XNOR used for equality?

Because XNOR outputs 1 when its inputs are equal.

---

### Q45. What is the most important rule when comparing multi-bit numbers?

```text
Compare from MSB to LSB
```

The **first unequal bit** determines the result.

---

### Q46. Compare:

```text
A=1010,B=1001
```

Answer:

At the first unequal bit:

```text
1>0
```

Therefore:

```text
A>B
```

---

### Q47. Can a comparator be constructed using XNOR gates?

Yes.

For equality:

```text
A=B=AND of all corresponding XNORs
```

---

# PART I — ENCODER ⭐⭐⭐⭐⭐

### Q48. What is an Encoder?

An encoder converts:

```text
Many inputs → fewer outputs
```

---

### Q49. What is a 4-to-2 Encoder?

It has:

```text
4 inputs, 2 outputs
```

because:

```text
2²=4
```

---

### Q50. What is the main assumption of a normal encoder?

```text
Only one input should be active
```

---

### Q51. What happens if multiple inputs are active?

The output becomes ambiguous.

---

### Q52. What is a Priority Encoder?

A priority encoder assigns priority to inputs and produces the code of the **highest-priority active input**.

---

### Q53. What is the major advantage of a Priority Encoder?

It can handle:

```text
Multiple active inputs
```

---

### Q54. If D3 has highest priority and D3=D1=1, which is selected?

```text
D3
```

---

### Q55. Where are priority encoders commonly used?

* Interrupt controllers
* Arbitration logic
* CPU control
* Resource selection

---

# PART J — DECODER ⭐⭐⭐⭐⭐

### Q56. What is a Decoder?

A decoder converts:

```text
n inputs→2ⁿ outputs
```

---

### Q57. How many outputs does a 3-to-8 decoder have?

```text
8
```

---

### Q58. How many outputs does a 4-to-16 decoder have?

```text
16
```

---

### Q59. What is a 2-to-4 decoder?

It has:

```text
2 inputs, 4 outputs
```

---

### Q60. What is the output of a 2-to-4 decoder for AB=10?

```text
Y2=1
```

All other outputs are 0.

---

### Q61. What are the 2-to-4 decoder equations?

```text
Y0=A′B′
Y1=A′B
Y2=AB′
Y3=AB
```

---

### Q62. Why is a decoder called a minterm generator?

Each output corresponds to exactly one minterm.

For example:

```text
Y2=AB′=m2
```

---

### Q63. How can a decoder implement a Boolean function?

Use:

```text
Decoder + OR gate
```

For:

```text
F=Σm(1,3)
```

connect:

```text
Y1,Y3
```

to an OR gate.

---

### Q64. What is the purpose of an Enable input?

It controls whether the decoder is active.

---

### Q65. Where are decoders commonly used?

* Memory address decoding
* Chip selection
* Instruction decoding
* Control circuits

---

# PART K — MULTIPLEXER ⭐⭐⭐⭐⭐

### Q66. What is a Multiplexer?

A MUX selects one input from multiple inputs and sends it to one output.

```text
Many → One
```

---

### Q67. How many select lines does a 4:1 MUX have?

```text
2
```

because:

```text
2²=4
```

---

### Q68. How many select lines does an 8:1 MUX have?

```text
3
```

---

### Q69. General formula for MUX select lines?

```text
n=log₂N
```

where N is the number of inputs.

---

### Q70. What is the equation of a 2:1 MUX?

```text
Y=S′I0+SI1
```

---

### Q71. For a 2:1 MUX, what happens when S=0?

```text
Y=I0
```

---

### Q72. What happens when S=1?

```text
Y=I1
```

---

### Q73. In a 4:1 MUX, what is selected for S1S0=11?

```text
I3
```

---

### Q74. What is selected for S1S0=10?

```text
I2
```

---

### Q75. Why is a MUX important in VLSI?

Because it is extensively used for:

* Datapath selection
* ALUs
* Register selection
* Bus routing
* Control logic

---

# PART L — MUX AS FUNCTION IMPLEMENTER ⭐⭐⭐⭐⭐

### Q76. Can a MUX implement Boolean functions?

Yes.

This is one of the most important MUX applications.

---

### Q77. How do you implement a 3-variable function using an 8:1 MUX?

Use all three variables as select lines.

For:

```text
F(A,B,C)
```

use:

```text
S2=A,S1=B,S0=C
```

Then connect each data input to 0 or 1 according to the truth table.

---

### Q78. How do you implement a 3-variable function using a 4:1 MUX?

Use two variables as select lines.

The remaining variable becomes the data-input variable.

---

### Q79. What are the possible data inputs when one variable C remains?

```text
0,1,C,C′
```

---

### Q80. Memorize this table:

| F(C=0) | F(C=1) | Input |
| -----: | -----: | ----- |
|      0 |      0 | 0     |
|      0 |      1 | C     |
|      1 |      0 | C′    |
|      1 |      1 | 1     |

⭐ This is a **high-value placement shortcut**.

---

### Q81. Implement:

```text
F(A,B)=Σm(1,2)
```

using 4:1 MUX.

**Answer:**

```text
S1=A,S0=B
```

and:

```text
I0=0, I1=1, I2=1, I3=0
```

---

### Q82. Implement:

```text
F(A,B,C)=Σm(1,2,6,7)
```

using 4:1 MUX with:

```text
S1=A, S0=B
```

**Answer:**

```text
I0=C
I1=C′
I2=0
I3=1
```

---

# PART M — DEMUX ⭐⭐⭐⭐

### Q83. What is a DEMUX?

A DEMUX routes one data input to one of multiple outputs.

```text
One → Many
```

---

### Q84. How many select lines does a 1-to-8 DEMUX have?

```text
3
```

---

### Q85. In a 1-to-4 DEMUX, if S1S0=10, where does the data go?

```text
Y2=D
```

---

### Q86. What happens to non-selected outputs?

They are normally:

```text
0
```

for an active-high implementation.

---

### Q87. What is the main difference between MUX and DEMUX?

```text
MUX: Many→One
DEMUX: One→Many
```

---

### Q88. What is the difference between Decoder and DEMUX?

**Decoder:**

```text
n inputs→2ⁿ outputs
```

**DEMUX:**

```text
1 data input+n select lines→2ⁿ outputs
```

A DEMUX routes actual data; a decoder primarily activates a line based on the input code.

---

# PART N — MIXED PLACEMENT QUESTIONS ⭐⭐⭐⭐⭐

### Q89. Which circuit is called a data selector?

```text
MUX
```

---

### Q90. Which circuit is called a data distributor/router?

```text
DEMUX
```

---

### Q91. Which circuit converts binary code to one-of-many outputs?

```text
Decoder
```

---

### Q92. Which circuit converts one-of-many input into binary code?

```text
Encoder
```

---

### Q93. Which circuit gives priority when multiple inputs are active?

```text
Priority Encoder
```

---

### Q94. Which gate is commonly used for equality detection?

```text
XNOR
```

---

### Q95. Which circuit is used for arithmetic addition?

```text
Adder
```

---

### Q96. Which circuit is used to compare two numbers?

```text
Comparator
```

---

### Q97. Which circuit can implement arbitrary Boolean functions conveniently?

```text
MUX
```

---

### Q98. Which circuit can generate all minterms?

```text
Decoder
```

---

### Q99. What is the difference between carry and overflow?

**Carry:** carry out from the most significant bit.

**Overflow:** signed arithmetic result exceeds the representable signed range.

⭐ They are **not the same thing**.

---

### Q100. Is carry-out alone sufficient to detect signed overflow?

No.

For two's-complement addition:

```text
Overflow=Cin,MSB⊕Cout,MSB
```

Another useful condition:

> Adding two positive numbers and getting a negative result → overflow.

> Adding two negative numbers and getting a positive result → overflow.

---

# 🔥 TOP 25 QUESTIONS TO MEMORIZE

If your placement test is tomorrow, prioritize these:

|  # | Question                        | Key Answer               |
| -: | ------------------------------- | ------------------------ |
|  1 | Half Adder Sum                  | A⊕B                      |
|  2 | Half Adder Carry                | AB                       |
|  3 | Full Adder Sum                  | A⊕B⊕Cin                  |
|  4 | Full Adder Carry                | AB+BCin+ACin             |
|  5 | RCA disadvantage                | Propagation delay        |
|  6 | CLA advantage                   | Faster carry calculation |
|  7 | Half Subtractor Difference      | A⊕B                      |
|  8 | Half Subtractor Borrow          | A′B                      |
|  9 | Full Subtractor Difference      | A⊕B⊕Bin                  |
| 10 | Subtraction technique           | 2's complement           |
| 11 | Comparator equality             | XNOR                     |
| 12 | Multi-bit comparison            | MSB → LSB                |
| 13 | Encoder                         | Many → Few               |
| 14 | Priority Encoder                | Highest priority wins    |
| 15 | Decoder                         | Few → Many               |
| 16 | Decoder outputs                 | 2ⁿ                       |
| 17 | Decoder application             | Address decoding         |
| 18 | MUX                             | Many → One               |
| 19 | DEMUX                           | One → Many               |
| 20 | MUX select lines                | log₂N                    |
| 21 | 2:1 MUX equation                | S′I0+SI1                 |
| 22 | MUX application                 | Function implementation  |
| 23 | Decoder function implementation | Decoder + OR             |
| 24 | Encoder limitation              | Multiple active inputs   |
| 25 | MUX remaining variable inputs   | 0,1,X,X′                 |

---

# ⭐ VLSI PLACEMENT MUST-KNOW LIST

For **Intel / Qualcomm / AMD / Synopsys / Cadence-type digital/VLSI interviews**, I would especially make sure you can solve these **without looking at notes**:

### Arithmetic

* Half Adder
* Full Adder
* RCA
* CLA
* Half Subtractor
* Full Subtractor
* 2's-complement subtraction
* Adder-subtractor

### Data selection

* 2:1 MUX
* 4:1 MUX
* MUX equations
* MUX implementation of Boolean functions
* DEMUX

### Code conversion

* Encoder
* Priority Encoder
* Decoder
* Decoder → Boolean function

### Comparison

* 1-bit comparator
* Multi-bit comparator
* XNOR-based equality

### ⭐ Integration

You should be able to look at a circuit and identify:

```text
Adder? Subtractor? MUX? Decoder? Encoder? Comparator?
```

and explain **why**.

---

## Where You Are Now

You've covered the complete **Phase 4 theory**:

```text
Combinational Circuits ≈ COMPLETE
```

And you've answered the quick checks correctly throughout the phase. Your next useful step is **not more theory**—it's to test whether you can solve these concepts under placement conditions.
