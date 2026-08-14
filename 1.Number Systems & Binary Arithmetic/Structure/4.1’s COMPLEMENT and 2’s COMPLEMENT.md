# 1’s COMPLEMENT and 2’s COMPLEMENT ⭐⭐⭐

This is one of the MOST IMPORTANT topics for interviews.

If you understand this well, then signed numbers, subtraction, overflow, ALU design, and Verilog arithmetic become much easier.

## 1. Why do we need complements?

Suppose we want to do:

### `7 − 5`

Computers prefer addition, not subtraction.

Hardware designers discovered:

### `A − B = A + (complement of B)`

This allows one adder circuit to perform both addition and subtraction.

So complements are used to represent negative numbers and perform subtraction using addition hardware.

---

## 2. 1’s Complement

### What is it?

Invert every bit.

| Original   | 1’s complement |
| ---------- | -------------- |
| `10110010` | `01001101`     |

### Rule ⭐

* `0 → 1`
* `1 → 0`

### Example

Find 1’s complement of `00101100`.

```text
00101100
11010011
```

✅ `11010011`

---

## 3. 2’s Complement ⭐⭐⭐

### What is it?

Take 1’s complement and add 1.

| Step     | Value      |
| -------- | ---------- |
| Original | `00101100` |
| 1’s comp | `11010011` |
| +1       | `00000001` |
| 2’s comp | `11010100` |

✅ `11010100`

### Memory Trick ⭐

**1’s**

Invert

**2’s**

Invert + 1

---

## 4. Fast Shortcut for 2’s Complement ⭐⭐⭐

Instead of inverting all bits and adding 1:

### Step 1: Start from the right.

### Step 2: Copy all bits up to and including the first 1.

### Step 3: Invert the remaining left bits.

Example: `00101100`

From right:

`00101100`

First 1 from right is highlighted mentally:

`00101100`

Copy from that 1 to the end:

```text
00000100
```

Invert remaining left part:

```text
11010100
```

✅ Same answer.

This is very fast in interviews.

---

## 5. Why 2’s Complement is Preferred ⭐⭐⭐

| Feature            | 1’s | 2’s |
| ------------------ | --- | --- |
| Single zero        | ❌   | ✅   |
| Easy hardware      | ❌   | ✅   |
| Used in processors | ❌   | ✅   |

---

## 6. Signed Numbers Using 2’s Complement ⭐⭐⭐

For 4 bits:

| Binary | Decimal |
| ------ | ------: |
| `0000` |       0 |
| `0001` |       1 |
| `0010` |       2 |
| `0011` |       3 |
| `0100` |       4 |
| `0101` |       5 |
| `0110` |       6 |
| `0111` |       7 |
| `1000` |      -8 |
| `1001` |      -7 |
| `1010` |      -6 |
| `1011` |      -5 |
| `1100` |      -4 |
| `1101` |      -3 |
| `1110` |      -2 |
| `1111` |      -1 |

---

## 7. Range Formula ⭐⭐⭐

For n bits in 2’s complement:

### Minimum

```text
−2ⁿ⁻¹
```

### Maximum

```text
2ⁿ⁻¹ − 1
```

### Example: 8 bits

* Minimum = −128
* Maximum = +127

⭐ Very frequently asked

---

## 8. Converting Negative Decimal to Binary ⭐⭐⭐

Convert `−5` to 8-bit binary.

### Step 1: Write +5

```text
00000101
```

### Step 2: 1’s complement

```text
11111010
```

### Step 3: Add 1

```text
11111011
```

✅ `−5 = 11111011`

---

## 9. Convert 2’s Complement to Decimal ⭐⭐⭐

Convert `11111011` to decimal.

### Step 1: MSB is 1 → negative

### Step 2: Take 2’s complement

```text
11111011
00000101
```

### Step 3: Decimal = 5

Answer:

### `−5`

---

## 10. Subtraction Using 2’s Complement ⭐⭐⭐

Compute `7 − 5` using 4 bits.

### Step 1: 7

```text
0111
```

### Step 2: 5

```text
0101
```

### Step 3: 2’s complement of 5

```text
1011
```

### Step 4: Add

```text
  0111
+ 1011
------
1 0010
```

Discard carry:

```text
0010
```

✅ **2**

---

## 11. Another Example: 5 − 7

```text
0101 + 1001 = 1110
```

MSB = 1 → negative.

Take 2’s complement of `1110`:

```text
0010
```

Result = **−2**.

---

## 12. Carry vs Overflow ⭐⭐⭐

Students confuse these constantly.

### Carry

* For unsigned arithmetic

### Overflow

* For signed arithmetic

### Example (4-bit signed)

```text
0111 (+7)
+0001 (+1)
-----------
1000
```

Mathematically: `7 + 1 = 8`

But 4-bit signed range is −8 to +7.

Result became `1000 = −8`.

🚨 **Overflow occurred**

### Overflow Rule ⭐⭐⭐

### Signed addition overflow occurs when:

**Positive + Positive → Negative**

**Negative + Negative → Positive**

No overflow when signs are different.

---

## 13. Common Mistakes ❌

* Forgetting +1 in 2’s complement
* Treating carry as overflow
* Using unsigned range for signed numbers
* Not checking MSB first when decoding

---

## 14. Placement Interview Questions ⭐⭐⭐

### Q1. Why do processors use 2’s complement?

**Answer:** Single zero, simpler addition/subtraction hardware, easy overflow detection.

### Q2. What is the range of a 16-bit signed number?

* Min = −32768
* Max = +32767

### Q3. Find 2’s complement of `10110000`.

Fast method:

* Copy from rightmost 1 → `00010000`
* Invert remaining left bits → `01010000`

✅ `01010000`

---

## 15. MCQs

### Q1. 2’s complement of `00001111` is:

* A) `11110000`
* B) `11110001` ✅
* C) `00010000`
* D) `11111111`

### Q2. 8-bit signed range is:

* A) −255 to 255
* B) −128 to 127 ✅
* C) −127 to 128
* D) 0 to 255

### Q3. Overflow occurs in:

* A) `5 + (−3)`
* B) `7 + 1` (4-bit signed) ✅
* C) `−2 + 1`
* D) `3 + (−4)`

---

## 16. Numerical Problems

### Easy

Find 1’s complement of `10101010`

✅ `01010101`

### Medium

Find 2’s complement of `01100100`

```text
1’s: 10011011
+1 → 10011100
```

### Placement Level ⭐⭐⭐

Compute `−25` in 8-bit 2’s complement.

```text
25 = 00011001
```

```text
1’s = 11100110
```

```text
+1 = 11100111
```

✅ `−25 = 11100111`

---

## 17. Verilog Relevance ⭐⭐⭐

```verilog
reg signed [7:0] a;
a = -5;
```

Stored as:

```text
11111011
```

Important interview point:

```text
8'hFF
```

* Unsigned = 255
* Signed = −1

Depends on signed/unsigned declaration.

---

## 18. One-Page Quick Revision

### 1’s complement

Invert

### 2’s complement

Invert + 1 ⭐

### n-bit signed range

```text
−2ⁿ⁻¹ to 2ⁿ⁻¹−1 ⭐
```

### Overflow rule ⭐

```text
+ + → −
− − → +
```

### Carry

Unsigned arithmetic

### Overflow

Signed arithmetic

### Fast 2’s complement ⭐

Copy from rightmost 1

Invert remaining left bits
