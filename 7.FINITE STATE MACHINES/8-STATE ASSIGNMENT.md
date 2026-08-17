# STATE ASSIGNMENT ⭐⭐⭐⭐⭐

State assignment is the process of assigning a **binary code to each state** of an FSM.

It is an important step between the **state table** and the actual hardware implementation.

---

# 1. What is State Assignment?

Suppose an FSM has four states:

```text id="q4m8v2"
S0
```

S1

S2

S3

We need to represent these states using binary values.

One possible assignment is:

| State | Binary Code |
| ----- | ----------- |
| S0    | 00          |
| S1    | 01          |
| S2    | 10          |
| S3    | 11          |

This process is called:

**State Assignment**

---

# 2. Why Do We Need State Assignment?

Flip-flops store **binary values**, not names like `S0`, `S1`, etc.

For example:

```text id="k7p2n5"
S0 → 00
```

S1 → 01

S2 → 10

S3 → 11

The flip-flops store these binary values.

Therefore:

**State assignment converts symbolic states into binary codes**

---

# 3. Number of Flip-Flops Required ⭐⭐⭐⭐⭐

For N states:

**n=⌈log₂N⌉**

flip-flops are required for binary state encoding.

### Example 1

4 states:

**⌈log₂4⌉=2**

Therefore:

**2 flip-flops**

### Example 2

5 states:

**⌈log₂5⌉=3**

Therefore:

**3 flip-flops**

### Example 3

10 states:

**⌈log₂10⌉=4**

Therefore:

**4 flip-flops**

---

# 4. Binary State Assignment ⭐⭐⭐⭐⭐

This is the most straightforward approach.

For 4 states:

```text id="m3q8v1"
S0 → 00
```

S1 → 01

S2 → 10

S3 → 11

For 5 states:

```text id="c6n2r9"
S0 → 000
```

S1 → 001

S2 → 010

S3 → 011

S4 → 100

### Advantage

Requires relatively few flip-flops:

**⌈log₂N⌉**

---

# 5. One-Hot State Assignment ⭐⭐⭐⭐⭐

In **one-hot encoding**, each state gets its own flip-flop.

For 4 states:

```text id="x5k9p3"
S0 → 0001
```

S1 → 0010

S2 → 0100

S3 → 1000

Only **one bit is HIGH (`1`)** at a time.

Therefore:

**N states → N flip-flops**

---

# 6. Example: Binary vs One-Hot

Suppose:

**N=8**

### Binary encoding

**⌈log₂8⌉=3**

So:

**3 flip-flops**

### One-hot encoding

**8 flip-flops**

Huge difference.

---

# 7. Why Use One-Hot Encoding? ⭐⭐⭐⭐⭐

Although one-hot uses more flip-flops, it can simplify the combinational logic.

For example:

```text id="v8m1q6"
S0 = 0001
```

S1 = 0010

S2 = 0100

S3 = 1000

Each state has a dedicated bit.

Therefore state decoding can become simpler.

### Important placement idea:

**One-hot → More flip-flops, potentially simpler/faster logic**

---

# 8. Where Is One-Hot Commonly Used?

One-hot encoding is particularly common in **FPGA-based FSM implementations**, because FPGAs generally have abundant flip-flops and the encoding can simplify logic.

For ASICs, binary or other optimized encodings may often be preferred depending on area, power, timing, and synthesis results.

---

# 9. Gray-Code State Assignment ⭐⭐⭐⭐

In Gray-code encoding, adjacent states differ by **only one bit**.

Example:

```text id="n4c7x2"
00
```

01

11

10

Compare:

```text id="g8r3m5"
00 → 01
```

Only one bit changes.

```text id="t6p2v9"
01 → 11
```

Only one bit changes.

```text id="w5k1q4"
11 → 10
```

Only one bit changes.

---

# 10. Why Use Gray Code?

The main idea is to reduce the number of state bits changing during transitions.

This can help reduce:

* Switching activity
* Glitches
* Dynamic power in suitable designs

Therefore:

**Gray code → one-bit change between adjacent states**

---

# 11. Binary vs One-Hot vs Gray

| Feature                            | Binary              | One-Hot         | Gray                  |
| ---------------------------------- | ------------------- | --------------- | --------------------- |
| Flip-flops                         | Few                 | Many            | Few                   |
| For N states                       | ⌈log₂N⌉             | N               | Usually ⌈log₂N⌉       |
| Logic                              | Can be more complex | Often simpler   | Depends on design     |
| Adjacent states differ by one bit? | Not necessarily     | Not necessarily | Yes                   |
| Common use                         | General             | FPGA FSMs       | Low-switching designs |

---

# 12. Example: 4-State FSM

Suppose:

```text id="b2m7p5"
S0 → S1 → S2 → S3
```

### Binary

```text id="j9q4x1"
S0 → 00
```

S1 → 01

S2 → 10

S3 → 11

Notice:

```text id="r6n3k8"
01 → 10
```

Both bits change.

---

### Gray

```text id="p1v8m4"
S0 → 00
```

S1 → 01

S2 → 11

S3 → 10

Now:

```text id="z5c2q7"
00 → 01 → 11 → 10
```

Only one bit changes at each adjacent transition.

---

# 13. State Assignment Can Affect Circuit Performance ⭐⭐⭐⭐⭐

This is an important VLSI interview concept.

Different state assignments can result in different:

* Combinational logic
* Area
* Power
* Timing
* Number of gates

Therefore:

**State encoding can affect FSM implementation**

Modern synthesis tools can often choose or optimize state encoding automatically, but understanding the underlying methods is important for interviews.

---

# 14. State Assignment Example

Suppose we have:

```text id="m8x2r5"
S0 → S1 → S2 → S3
```

### Binary:

```text id="v4k7n1"
S0 = 00
```

S1 = 01

S2 = 10

S3 = 11

### Gray:

```text id="c3p9q6"
S0 = 00
```

S1 = 01

S2 = 11

S3 = 10

### One-hot:

```text id="w7m2x8"
S0 = 0001
```

S1 = 0010

S2 = 0100

S3 = 1000

All three represent the same logical states, but the hardware implementation differs.

---

# 15. 🔥 Placement Questions

### Q1. What is state assignment?

**Answer:**

Assigning binary codes to the symbolic states of an FSM.

---

### Q2. How many flip-flops are required for 16 states using binary encoding?

**log₂16=4**

**4**

---

### Q3. How many flip-flops are required for 10 states?

**⌈log₂10⌉=4**

**4**

---

### Q4. How many flip-flops does a one-hot FSM with 10 states require?

**10**

---

### Q5. What is the main characteristic of one-hot encoding?

**One flip-flop corresponds to each state**

and normally only one state bit is asserted at a time.

---

### Q6. What is the main characteristic of Gray-code encoding?

**Adjacent states differ by one bit**

---

### Q7. Which encoding uses the minimum number of flip-flops among these three?

Generally:

**Binary**

for the same number of states, with the same ⌈log₂N⌉ storage requirement as Gray encoding.

---

### Q8. Which encoding is commonly associated with FPGA FSM implementation?

**One-hot**

---

### Q9. Why can one-hot encoding be faster despite using more flip-flops?

Because state decoding and next-state logic can become simpler.

---

### Q10. Why can Gray encoding reduce switching activity?

Because adjacent states differ by only one bit.

---

# 16. 🔥 Important Numerical Questions

### Q11.

An FSM has **25 states**. How many flip-flops are required using binary encoding?

**⌈log₂25⌉**

Since:

**2⁴=16**

**2⁵=32**

Therefore:

**5**

---

### Q12.

An FSM has 25 states and uses one-hot encoding.

**25 flip-flops**

---

### Q13.

An FSM has 7 states.

Binary:

**⌈log₂7⌉=3**

One-hot:

**7**

Therefore:

```text id="u4m9q2"
Binary → 3 FFs
```

One-hot → 7 FFs

---

# 🧠 QUICK REVISION

```text id="x7c3n8"
STATE ASSIGNMENT
────────────────────────

Purpose:

Symbolic states → Binary codes

Binary:

N states → ceil(log₂N) FFs

One-hot:

N states → N FFs

One-hot:

→ One state per flip-flop

→ More FFs

→ Simpler decoding

→ Common in FPGA FSMs

Gray:

→ Adjacent states differ by 1 bit

→ Can reduce switching activity

Encoding affects:

→ Area

→ Power

→ Timing

→ Logic complexity

###

### 🔥 Remember these three:

Binary → Minimum FFs

One-Hot → One FF per state

Gray → One-bit transition
```
