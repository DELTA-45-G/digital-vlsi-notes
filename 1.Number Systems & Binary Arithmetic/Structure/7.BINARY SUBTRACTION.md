# BINARY SUBTRACTION ⭐⭐⭐

## 1. What is Binary Subtraction?

Subtracting one binary number from another.

Example:

### `1010 − 0011`

`10 − 3 = 7`

## 2. Why is it needed?

Processors must perform:

* A − B
* Comparisons
* Address calculations
* Loop counters
* Pointer arithmetic

## 3. Real Hardware Insight ⭐⭐⭐

Modern CPUs do not build a separate subtractor.

They use:

### Subtraction = Addition of 2’s complement

```text
A − B = A + (2’s complement of B)
```

This is a very common interview question.

## 4. Direct Subtraction Rules

Similar to decimal.

| Operation | Result          |
| --------- | --------------- |
| `0 − 0`   | `0`             |
| `1 − 0`   | `1`             |
| `1 − 1`   | `0`             |
| `0 − 1`   | Borrow needed ⭐ |

## 5. Understanding Borrow

Decimal:

```text
10 - 7
```

Borrow from the next digit.

Binary:

```text
0 - 1
```

Borrow 1 binary unit, which equals 2 decimal.

So:

### `10₂ − 1₂ = 1₂`

After borrowing

## 6. Easy Example

Compute:

```text
 101
-011
----
 010
```

Check:

* 5 − 3 = 2 ✔️

## 7. Borrow Example ⭐⭐

Compute:

```text
 1000
-0001
-----
 0111
```

Why?

* Rightmost: 0−1 → borrow
* Borrow propagates through zeros

Result:

### `0111`

8 − 1 = 7

## 8. Medium Example

Compute:

```text
 1101
-0110
-----
 0111
```

Check:

* 13 − 6 = 7 ✔️

## 9. The VLSI Method: 2’s Complement Subtraction ⭐⭐⭐

This is the most important method.

### Example: 13 − 6

### Step 1: A

```text
1101
```

### Step 2: B

```text
0110
```

### Step 3: 2’s complement of B

* 1’s → `1001`
* +1 → `1010`

### Step 4: Add

```text
 1101
+1010
-----
1 0111
```

Discard carry:

### `0111`

Result = 7

## 10. Why Do We Discard the Carry? ⭐

In fixed-width arithmetic (4-bit here), the extra carry is outside the register width.

This is called end carry.

## 11. Negative Result Example ⭐⭐⭐

Compute 5 − 7 using 4 bits.

### Step 1: 5

```text
0101
```

### Step 2: 7

```text
0111
```

### Step 3: 2’s complement of 7

* `1000`
* +1 → `1001`

### Step 4: Add

```text
 0101
+1001
-----
 1110
```

No end carry.

MSB=1 → negative.

Take 2’s complement of 1110:

* `0001`
* +1 → `0010`

Magnitude = 2.

### `−2`

## 12. Shortcut to Interpret Result ⭐⭐⭐

After subtraction:

**End carry = 1**

Result is positive

Discard the carry.

**End carry = 0**

Result is negative

Take 2’s complement of the result.

## 13. Placement-Level Example ⭐⭐⭐

Compute 23 − 45 using 8 bits.

### Step 1: 23

```text
00010111
```

### Step 2: 45

```text
00101101
```

### Step 3: 2’s complement of 45

* `11010010`
* +1 → `11010011`

### Step 4: Add

```text
 00010111
+11010011
---------
 11101010
```

No carry → negative.

Take 2’s complement:

* `00010101`
* +1 → `00010110` = 22

### `−22`

Correct: 23 − 45 = −22 ✔️

## 14. Borrow vs Carry ⭐⭐⭐

Students confuse these.

| Operation                  | Indicator |
| -------------------------- | --------- |
| Direct subtraction         | Borrow    |
| 2’s complement subtraction | End carry |
| Addition                   | Carry     |

## 15. Interview Question ⭐⭐⭐

### Why is borrow avoided in hardware?

Because borrow propagation is inconvenient.

Using 2’s complement allows subtraction to be implemented with the same adder hardware.

## 16. Common Mistakes ❌

* Forgetting +1 after 1’s complement
* Not discarding end carry
* Treating no-carry as zero
* Using unsigned interpretation for negative result

## 17. MCQs

### Q1. 2’s complement subtraction uses:

* A) Borrow circuit
* B) Adder circuit ✅
* C) Comparator
* D) Decoder

### Q2. `1000 − 0001 =`

* A) 1001
* B) 0111 ✅
* C) 1111
* D) 0001

### Q3. In 2’s complement subtraction, no end carry means:

* A) Positive
* B) Negative ✅
* C) Overflow
* D) Zero

## 18. Verilog Relevance ⭐⭐⭐

```verilog
assign diff = a - b;
```

Synthesizer typically implements:

```text
a + (~b + 1)
```

For signed arithmetic:

```verilog
reg signed [7:0] a, b;
reg signed [7:0] diff;
```

## 19. One-Page Quick Revision

### Binary Subtraction Quick Sheet

```text
0−0=0
1−0=1
1−1=0
0−1 → borrow ⭐
```

### Hardware method ⭐

```text
A − B = A + (2’s complement of B)
```

### Positive result

**End carry = 1**

Discard carry

### Negative result

**End carry = 0**

Take 2’s complement of result

### Borrow vs Carry ⭐

```text
Borrow → direct subtraction
Carry  → addition / 2’s complement subtraction
```
