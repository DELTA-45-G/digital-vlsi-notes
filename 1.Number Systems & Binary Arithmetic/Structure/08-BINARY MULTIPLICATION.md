# BINARY MULTIPLICATION ⭐⭐

## 1. What is Binary Multiplication?

Multiplying two binary numbers.

Example:

### `101 × 11`

`5 × 3 = 15`

## 2. Why is it needed?

Processors multiply numbers for:

* DSP operations
* Graphics
* AI/ML
* Address calculations
* Signal processing

## 3. Basic Rules ⭐

Very simple.

| Operation | Result |
| --------- | ------ |
| `0 × 0`   | `0`    |
| `0 × 1`   | `0`    |
| `1 × 0`   | `0`    |
| `1 × 1`   | `1`    |

Notice: No carry is generated during a single-bit multiplication.

## 4. Decimal Analogy

Decimal:

```text
  23 × 12
```

Binary works the same way, but digits are only 0 or 1.

## 5. Easy Example ⭐

Compute:

```text
  101
×  10
-----
 000
1010
-----
1010
```

Result:

### `1010₂`

`5 × 2 = 10`

## 6. Medium Example ⭐⭐

Compute:

```text
   101
×   11
------
   101
  1010
------
  1111
```

Check:

* 101 = 5
* 11 = 3
* 15 = 1111 ✔️

## 7. Placement-Level Example ⭐⭐⭐

Compute:

```text
    1101
×   1011
--------
    1101
   11010
  000000
 1101000
--------
10001111
```

Check:

* 1101 = 13
* 1011 = 11
* 13 × 11 = 143

143 in binary:

`10001111`

✅ Correct.

## 8. The Shift-and-Add Method ⭐⭐⭐

This is how hardware thinks.

Suppose:

### `13 × 11`

`1101 × 1011`

Look at multiplier bits from right to left.

| Multiplier bit | Action          |
| -------------- | --------------- |
| 1              | Add `1101`      |
| 1              | Add `1101 << 1` |
| 0              | Add nothing     |
| 1              | Add `1101 << 3` |

This becomes:

```text
00001101
00011010
00000000
01101000
---------
10001111
```

## 9. Why Shifts Matter ⭐⭐⭐

### Left shift by 1

Multiply by 2.

```text
1011 → 10110
```

`11 × 2 = 22`

### Left shift by 2

Multiply by 4.

```text
1011 → 101100
```

`11 × 4 = 44`

## 10. Interview Shortcut ⭐

To multiply by powers of 2:

| Operation | Shortcut     |
| --------- | ------------ |
| ×2        | Left shift 1 |
| ×4        | Left shift 2 |
| ×8        | Left shift 3 |

Example:

```text
00110101 × 8 = 110101000
```

## 11. Multiplication by 0 and 1

```text
A × 0
0

A × 1
A
```

These are common MCQs.

## 12. Signed Multiplication (Basic Idea) ⭐⭐

For placements, usually they ask:

* Convert to decimal
* Multiply
* Convert back

Example:

* `1110` = −2 (4-bit signed)
* `0011` = +3

Result:

`−2 × 3 = −6`

Binary (4-bit signed):

```text
1010
```

We will revisit signed arithmetic later in VLSI/Verilog phases.

## 13. Common Mistakes ❌

* Not shifting partial products
* Adding instead of multiplying bits
* Forgetting zeros in partial rows
* Ignoring result width

## 14. Result Width ⭐⭐⭐

Very important for Verilog.

If:

### `n-bit × m-bit`

Result can be **(n+m) bits**

Examples:

* 4×4 → 8 bits
* 8×8 → 16 bits
* 16×16 → 32 bits

## 15. Placement Interview Questions ⭐⭐⭐

### Q1. Why is multiplication slower than addition?

Because it requires multiple additions and shifts.

### Q2. What is shift-and-add multiplication?

Generate partial products using multiplier bits and add shifted versions of the multiplicand.

### Q3. What is the maximum width of an 8×8 multiplication?

✅ 16 bits

## 16. MCQs

### Q1. `101 × 10 =`

* A) 101
* B) 1010 ✅
* C) 111
* D) 1001

### Q2. Left shift by 3 means:

* A) ×2
* B) ×4
* C) ×8 ✅
* D) ×16

### Q3. 4-bit × 4-bit result width:

* A) 4
* B) 5
* C) 7
* D) 8 ✅

## 17. Verilog Relevance ⭐⭐⭐

```verilog
wire [7:0] p;
assign p = a * b;
```

For 4-bit inputs:

```verilog
wire [3:0] a, b;
wire [7:0] p;
```

If you write:

```verilog
wire [3:0] p = a * b;
```

Upper bits are truncated ⚠️

## 18. One-Page Quick Revision

### Binary Multiplication Quick Sheet

```text
0×0=0
0×1=0
1×0=0
1×1=1
```

### Shift rules ⭐

```text
<<1 → ×2
<<2 → ×4
<<3 → ×8
```

### Hardware method ⭐

**Shift and Add**

### Width rule ⭐

`n-bit × m-bit → (n+m) bits`

### Common trap

**Don’t forget shifting partial products**

# BINARY MULTIPLICATION — STEP BY STEP ⭐⭐⭐

Absolutely! This is where many students get confused. I’ll explain binary multiplication exactly like school decimal multiplication, but step by step.

## First remember the rule

When multiplying by a single binary digit:

| Bit | Result          |
| --- | --------------- |
| `0` | Write all 0s    |
| `1` | Copy the number |

And each new row is shifted left by one position.

---

## Example 1: Easy

Compute `101 × 10`

### Step 1: Write the numbers

```text
   101
×   10
```

* Top number = `101`
* Bottom number = `10`

We multiply using the bottom bits from right to left.

### Step 2: Multiply by the rightmost bit (0)

Rightmost bit is `0`.

Rule: multiplying by 0 gives all 0s.

```text
   101
×   10
------
   000
```

### Step 3: Multiply by the next bit (1)

Now move one position left, so the result is shifted left by 1.

Copy `101` and add one zero at the end:

```text
101 → 1010
```

```text
   101
×   10
------
   000
  1010
```

Why `1010`?

Because shifting left by 1 means:

```text
101 → 1010
```

which is multiplying by 2.

### Step 4: Add the partial products

```text
   000
+ 1010
------
  1010
```

✅ Final answer:

```text
1010₂
```

Check in decimal:

* `101₂ = 5`
* `10₂ = 2`
* `5 × 2 = 10`
* `10₁₀ = 1010₂` ✔️

---

## Example 2: Medium

Compute `101 × 11`

### Step 1: Write the numbers

```text
   101
×   11
```

Bottom number has two bits: `1` and `1`.

### Step 2: Multiply by the rightmost 1

Copy `101`.

```text
   101
×   11
------
   101
```

### Step 3: Multiply by the next 1

Move one position left, so shift left by 1.

```text
101 → 1010
```

Write it under the first row:

```text
   101
×   11
------
   101
  1010
```

### Step 4: Add them carefully

Align the digits:

```text
   0101
+  1010
-------
   1111
```

Bit by bit:

* `1 + 0 = 1`
* `0 + 1 = 1`
* `1 + 0 = 1`
* `0 + 1 = 1`

Result:

```text
1111
```

Check:

* `101₂ = 5`
* `11₂ = 3`
* `5 × 3 = 15`
* `15₁₀ = 1111₂` ✔️

---

## Example 3: Placement-Level (step by step)

Compute `1101 × 1011`

This is `13 × 11`.

### Step 1: Write the numbers

```text
    1101
×   1011
```

We process the multiplier bits from right to left.

The multiplier is:

```text
1011
```

Bits are:

| 8s | 4s | 2s | 1s |
| -: | -: | -: | -: |
|  1 |  0 |  1 |  1 |

### Step 2: Multiply by the rightmost bit (1)

Copy `1101`.

```text
    1101
×   1011
--------
    1101
```

### Step 3: Multiply by the next bit (1)

Shift left by 1.

```text
1101 → 11010
```

```text
    1101
×   1011
--------
    1101
   11010
```

### Step 4: Multiply by the next bit (0)

Anything × 0 = 0.

Shift left by 2, but still all zeros:

```text
    1101
×   1011
--------
    1101
   11010
  000000
```

(You may also write just `0`; I wrote all zeros to show the alignment.)

### Step 5: Multiply by the last bit (1)

Shift left by 3.

Start with `1101` and add three zeros:

```text
1101 → 1101000
```

```text
    1101
×   1011
--------
    1101
   11010
  000000
 1101000
```

### Step 6: Add all partial products

Align them properly:

```text
   0001101
+  0011010
+  0000000
+  1101000
----------
   10001111
```

Let’s add column by column from the right.

| Column | Bits             | Result     |
| -----: | ---------------- | ---------- |
|      0 | `1+0+0+0`        | `1`        |
|      1 | `0+1+0+0`        | `1`        |
|      2 | `1+0+0+0`        | `1`        |
|      3 | `1+1+0+1`        | `1 carry1` |
|      4 | `0+1+0+0+carry1` | `0 carry1` |
|      5 | `0+0+0+1+carry1` | `0 carry1` |
|      6 | `0+0+0+1+carry1` | `0 carry1` |
|      7 | `carry1`         | `1`        |

Final:

```text
10001111
```

### Check in decimal

### Convert `10001111` to decimal

Weights:

```text
128  64  32  16  8  4  2  1
```

Bits:

```text
  1    0   0    0  1  1  1  1
```

Add:

```text
128 + 8 + 4 + 2 + 1 = 143
```

And:

```text
13 × 11 = 143
```

✅ Correct.

---

## The Pattern You Should Remember ⭐⭐⭐

For each multiplier bit:

### Multiplier bit = 0

Write `0` row

### Multiplier bit = 1

Copy multiplicand

### Position

Shift left by that position

### Final step

Add all rows

---

## Visual Memory Trick ⭐

Think of `1011` as:

```text
8   4   2   1
1   0   1   1
```

So:

```text
13 × 1011
= 13×8 + 13×0 + 13×2 + 13×1
= 104 + 0 + 26 + 13
= 143
```

Binary multiplication is doing exactly the same thing automatically with shifts.
