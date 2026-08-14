# BINARY ADDITION ⭐⭐⭐

## 1. What is Binary Addition?

It is the process of adding numbers written in base 2.

Just like decimal addition, but using only 0 and 1.

## 2. Why is it needed?

Every arithmetic operation inside a processor is ultimately performed using binary adders.

Even subtraction is converted into addition using 2’s complement.

## 3. Real Hardware Example ⭐

`5`

When your CPU calculates:

### `25 + 17`

Converted to binary

### `11001 + 10001`

Added using full adders

## 4. The Four Basic Rules ⭐⭐⭐

These must be memorized.

| Operation | Result |
| --------- | ------ |
| `0 + 0`   | `0`    |
| `0 + 1`   | `1`    |
| `1 + 0`   | `1`    |
| `1 + 1`   | `10` ⭐ |

Notice:

### `1 + 1 = 10`

Sum = 0, Carry = 1

This is the most important rule in digital arithmetic.

## 5. Understanding Carry

Decimal:

```text
9 + 8 = 17
```

Write 7, carry 1.

Binary:

```text
1 + 1 = 10
```

Write 0, carry 1.

Same concept.

## 6. Adding Two Bits (Half Adder Intuition) ⭐

|  A |  B | Sum | Carry |
| -: | -: | --: | ----: |
|  0 |  0 |   0 |     0 |
|  0 |  1 |   1 |     0 |
|  1 |  0 |   1 |     0 |
|  1 |  1 |   0 |     1 |

Observe:

* Sum = XOR
* Carry = AND

We will use this in Phase 4.

## 7. Multi-bit Addition ⭐⭐⭐

Example:

```text
  1011
+ 0110
------
 10001
```

### Step-by-step

From right to left.

### Bit 0

* 1 + 0 = 1

### Bit 1

* 1 + 1 = 10
* Write 0, carry 1

### Bit 2

* 0 + 1 + carry1 = 10
* Write 0, carry 1

### Bit 3

* 1 + 0 + carry1 = 10
* Write 0, carry 1

### Final carry

* Write 1

Result:

### `10001₂`

Check:

* 1011 = 11
* 0110 = 6
* 17 = 10001 ✔️

## 8. Addition with Three Inputs ⭐⭐⭐

This is what a Full Adder does.

Possible inputs: A, B, Cin.

Important cases:

|  A |  B | Cin | Result     |
| -: | -: | --: | ---------- |
|  0 |  0 |   0 | 0 carry0   |
|  0 |  1 |   0 | 0 carry1   |
|  1 |  0 |   0 | 0 carry1   |
|  1 |  1 |   0 | 0 carry1   |
|  1 |  1 |   1 | 1 carry1 ⭐ |

Remember:

### `1 + 1 + 1 = 11₂`

Sum = 1, Carry = 1

## 9. Easy Numerical

Add:

```text
 101
+011
----
1000
```

Check:

* 5 + 3 = 8 ✔️

## 10. Medium Numerical

Add:

```text
 1101
+1011
-----
11000
```

Check:

* 13 + 11 = 24 ✔️

## 11. Placement-Level Numerical ⭐⭐⭐

Add (8-bit):

```text
 10110110
+01101101
---------
1 00100011
```

Discard carry for 8-bit result:

### `00100011`

Carry out = 1

Unsigned values:

* 182 + 109 = 291
* 291 mod 256 = 35 ✔️

## 12. Carry Propagation ⭐⭐⭐

Consider:

```text
 1111
+0001
-----
10000
```

The carry travels through all four stages.

### Carry propagation delay

This is why Ripple Carry Adders are slower.

## 13. Common Mistakes ❌

* Forgetting incoming carry
* Writing 2 in binary addition
* Dropping final carry unintentionally
* Confusing carry with overflow

## 14. Carry vs Overflow Revisited ⭐⭐⭐

### Unsigned Example

```text
1111 (15)
+0001 (1)
-----------
10000
```

* Result = 0 (4-bit)
* Carry = 1
* Unsigned overflow = Yes

### Signed Example

```text
0111 (+7)
+0001 (+1)
-----------
1000 (−8)
```

* Carry = 0
* Signed overflow = Yes

## 15. Interview Questions ⭐⭐⭐

### Q1. What is the difference between Half Adder and Full Adder?

* Half Adder: no carry input
* Full Adder: has carry input

### Q2. Why is Ripple Carry Adder slow?

Because carry must propagate through every bit.

### Q3. Can carry be 1 without overflow?

✅ Yes.

Example: unsigned 15 + 1.

### Q4. Can overflow occur without carry?

✅ Yes.

Example: signed 7 + 1.

## 16. MCQs

### Q1. `1 + 1 + 1` equals:

* A) 10
* B) 11 ✅
* C) 100
* D) 101

### Q2. Carry in a Half Adder is:

* A) XOR
* B) OR
* C) AND ✅
* D) NAND

### Q3. `1010 + 0101 =`

* A) 1111 ✅
* B) 10000
* C) 10101
* D) 1100

## 17. Verilog Relevance ⭐⭐⭐

```verilog
assign sum = a + b;
```

Synthesizer creates an adder circuit.

For wider adders:

```verilog
wire [7:0] sum;
assign sum = a + b;
```

Carry can be captured as:

```verilog
wire [8:0] temp;
assign temp = a + b;
assign carry = temp[8];
```

## 18. One-Page Quick Revision

### Binary Addition Quick Sheet

```text
0+0=0
0+1=1
1+0=1
1+1=10 ⭐
```

```text
1+1+1=11 ⭐
```

### Half Adder

```text
Sum   = A XOR B
Carry = A AND B
```

### Full Adder

Inputs: A, B, Cin

### Carry propagation

```text
1111 + 0001 → carry ripples through all bits
```

### Carry vs Overflow ⭐

```text
Carry   → Unsigned
Overflow → Signed
```
