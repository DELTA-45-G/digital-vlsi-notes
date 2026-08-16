# RIPPLE CARRY ADDER (RCA) ⭐⭐⭐⭐⭐

Now we move from **one-bit addition** to **multi-bit addition**.

---

## 1. What is a Ripple Carry Adder?

A **Ripple Carry Adder** is a combinational circuit used to add **two multi-bit binary numbers**.

It is constructed by connecting multiple **Full Adders** in series.

For an N-bit adder:

```text
N Full Adders
```

are required.

---

# 2. Why Do We Need RCA?

A Half Adder adds:

```text
A+B
```

A Full Adder adds:

```text
A+B+Cin
```

But real processors need to add numbers containing many bits.

For example:

```text
      1011

+ 0110

------

 10001
```

We need to add each bit while passing the carry from one position to the next.

That's where the Ripple Carry Adder is used.

---

# 3. Basic Structure ⭐⭐⭐⭐⭐

For a 4-bit RCA:

```text
 A0 ─────┐
 B0 ─────┤
 Cin ────┤ FA0 ├── S0
         └──┬──┘
            │ C1
            ▼

 A1 ─────┐
 B1 ─────┤
         │ FA1 ├── S1
 C1 ─────┤
         └──┬──┘
            │ C2
            ▼

 A2 ─────┐
 B2 ─────┤
         │ FA2 ├── S2
 C2 ─────┤
         └──┬──┘
            │ C3
            ▼

 A3 ─────┐
 B3 ─────┤
         │ FA3 ├── S3
 C3 ─────┤
         └──┬──┘
            │
           Cout
```

Each Full Adder passes its carry to the next Full Adder.

---

# 4. Why is it called "Ripple Carry"?

The carry propagates from one stage to the next:

```text
C0→C1→C2→C3→C4
```

The carry appears to **ripple** through the circuit.

Hence:

```text
Ripple Carry Adder
```

---

# 5. Example: 4-Bit Addition

Let's add:

```text
     1011

+ 0110

------

```

Start from the **LSB**.

### Bit 0

```text
1+0=1
```

```text
S0 = 1
```

```text
C1 = 0
```

### Bit 1

```text
1+1+0=10
```

```text
S1 = 0
```

```text
C2 = 1
```

### Bit 2

```text
0+1+1=10
```

```text
S2 = 0
```

```text
C3 = 1
```

### Bit 3

```text
1+0+1=10
```

```text
S3 = 0
```

```text
C4 = 1
```

Therefore:

```text
     1011

+ 0110

------

10001
```

Result:

```text
10001
```

---

# 6. ⭐ Most Important RCA Concept

The major disadvantage of RCA is:

```text
Carry propagation delay
```

The next Full Adder cannot determine its final result until the previous carry arrives.

Therefore:

```text
FA0 → FA1 → FA2 → FA3
```

↑       ↑       ↑

carry propagates

This makes RCA relatively slow for large bit widths.

---

# 7. Propagation Delay ⭐⭐⭐⭐⭐

Suppose one Full Adder takes some time to generate its carry.

For an N-bit RCA:

```text
Carry must propagate through multiple stages
```

So approximately:

```text
Tdelay ∝ N
```

The exact delay depends on the implementation and which output is being considered, but the key placement idea is:

> **RCA delay increases approximately linearly with the number of bits.**

---

# 8. Why is RCA Slow?

Consider an 8-bit RCA:

```text
FA0 → FA1 → FA2 → FA3 → FA4 → FA5 → FA6 → FA7
```

Suppose FA0 produces a carry.

FA1 has to wait.

Then FA2 waits.

Then FA3 waits.

...

The final stage may have to wait for the carry to ripple through all preceding stages.

---

# 9. ⭐ RCA vs CLA

This leads directly to the next topic: **Carry Look-Ahead Adder**.

| Feature           | RCA                    | CLA                 |
| ----------------- | ---------------------- | ------------------- |
| Carry calculation | Sequential propagation | Parallel/look-ahead |
| Speed             | Slower                 | Faster              |
| Hardware          | Simpler                | More complex        |
| Area              | Lower                  | Higher              |
| Carry delay       | High                   | Lower               |
| Design complexity | Low                    | Higher              |

### Memory trick:

> **RCA = Simple but Slow**

> **CLA = Complex but Fast**

---

# 10. Number of Full Adders

### 4-bit RCA

```text
4 Full Adders
```

### 8-bit RCA

```text
8 Full Adders
```

### 16-bit RCA

```text
16 Full Adders
```

Therefore:

```text
N-bit RCA requires N Full Adders
```

⭐ Very common MCQ.

---

# 11. Carry Input

An RCA can have an external carry input:

```text
C0=Cin
```

Then:

```text
C0→C1→C2→⋯→CN
```

If no initial carry is present:

```text
C0=0
```

---

# 12. Hardware Example

Suppose a CPU needs to add two 4-bit numbers:

```text
A = 1010
```

```text
B = 0011
```

A 4-bit RCA can perform:

```text
1010+0011=1101
```

Internally, four Full Adders process the four bit positions.

---

# 13. Verilog Relevance ⭐⭐⭐⭐

A structural 4-bit RCA can be built using four Full Adders.

Conceptually:

```verilog
full_adder FA0 (...);
full_adder FA1 (...);
full_adder FA2 (...);
full_adder FA3 (...);
```

The important part is:

```text
FA0.Cout → FA1.Cin
```

```text
FA1.Cout → FA2.Cin
```

```text
FA2.Cout → FA3.Cin
```

This represents the ripple.

---

# 14. ⭐ Placement Questions

### Q1. How many Full Adders are required for an 8-bit RCA?

8

### Q2. What is the main disadvantage of RCA?

```text
Carry propagation delay
```

### Q3. Why is it called Ripple Carry?

Because carry propagates/ripples from one stage to the next.

### Q4. Is RCA faster or slower than CLA?

Slower

### Q5. What is the main advantage of RCA?

```text
Simple design and low hardware complexity
```

---

# 🧠 RCA QUICK REVISION

```text
RIPPLE CARRY ADDER
```

────────────────────────────

### Purpose:

```text
Multi-bit binary addition
```

### N-bit RCA:

```text
N Full Adders
```

### Structure:

```text
FA0 → FA1 → FA2 → ... → FAN-1
```

### Carry:

```text
C0 → C1 → C2 → C3 → ...
```

### Why "Ripple"?

Carry propagates from one stage

to the next.

### Main advantage:

Simple

Low complexity

Less hardware

### Main disadvantage:

Carry propagation delay

### Speed:

Slower than CLA

### Memory:

```text
RCA = Simple + Slow

CLA = Complex + Fast
```
