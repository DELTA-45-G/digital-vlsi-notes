# SHIFT OPERATIONS (LEFT SHIFT & RIGHT SHIFT) ⭐⭐⭐

## 1. What is a Shift Operation?

A shift operation moves all bits of a binary number left or right by some positions.

Think of bits sitting in boxes:

```text
Before: [1][0][1][1]
```

### Left shift by 1

```text
[0][1][1][0]
```

### Right shift by 1

```text
[0][1][0][1]
```

## 2. Why Are Shifts Important?

Shifts are much cheaper in hardware than multiplication or division.

| Operation      | Hardware cost |
| -------------- | ------------- |
| Addition       | Low           |
| Shift          | Very low ⭐    |
| Multiplication | Higher        |
| Division       | Highest       |

## 3. LEFT SHIFT (`<<`) ⭐⭐⭐

### What happens?

All bits move left.

New bits on the right become `0`.

### Example: 4-bit

```text
1011
0110
```

The leftmost bit is discarded.

### Why does it multiply by 2?

Take `1011₂`.

| Bit | Weight |
| --: | -----: |
|   1 |      8 |
|   0 |      4 |
|   1 |      2 |
|   1 |      1 |

Value = 11

After left shift:

```text
10110
```

```text
16 + 4 + 2 = 22
```

✅ `22 = 11 × 2`

## 4. General Rule ⭐⭐⭐

```text
A << n = A × 2ⁿ
```

Examples:

```text
13 << 1 = 26
13 << 2 = 52
13 << 3 = 104
```

## 5. Detailed Example (Left Shift)

### Example: `13 << 2`

### Step 1: Write binary

```text
13 = 00001101
```

### Step 2: Shift left by 2

```text
00001101
00110100
```

### Step 3: Convert back

```text
32 + 16 + 4 = 52
```

✅ `13 × 4 = 52`

## 6. RIGHT SHIFT (`>>`) ⭐⭐⭐

### What happens?

Bits move right.

For unsigned numbers, new left bits become `0`.

### Example

```text
10110
01011
```

### Why does it divide by 2?

Take `10110₂`.

* 16 + 4 + 2 = 22

After right shift:

```text
01011
```

* 8 + 2 + 1 = 11

✅ `11 = 22 ÷ 2`

## 7. General Rule ⭐⭐⭐

For unsigned integers:

```text
A >> n = floor(A / 2ⁿ)
```

Examples:

```text
22 >> 1 = 11
22 >> 2 = 5
22 >> 3 = 2
```

Notice the remainder is discarded.

## 8. Detailed Example (Right Shift)

### Example: `45 >> 3`

### Step 1: Binary

```text
45 = 00101101
```

### Step 2: Shift right by 3

```text
00101101
00000101
```

### Step 3: Decimal

`5`

Why not 5.625?

Because binary right shift performs integer division.

## 9. What Happens to Discarded Bits? ⭐⭐

Example:

```text
10111 >> 2
00101
```

Discarded bits = `11`

These bits represent the remainder.

* 23 ÷ 4 = 5 remainder 3
* Remainder 3 = `11₂`

## 10. Visual Understanding ⭐⭐⭐

### Left Shift by 1

```text
0 1 1 0 1
↓ ↓ ↓ ↓ ↓
1 1 0 1 0
```

Equivalent to ×2.

### Right Shift by 1

```text
0 1 1 0 1
↓ ↓ ↓ ↓ ↓
0 0 1 1 0
```

Equivalent to ÷2 (integer).

## 11. Signed Numbers: Important Caution ⭐⭐⭐

There are two kinds of right shift.

### Logical Right Shift

Fill with `0`.

Example:

```text
10110000
01011000
```

Used for unsigned.

### Arithmetic Right Shift

Fill with the sign bit.

Example (signed negative):

```text
10110000
11011000
```

The leading `1` is preserved.

## 12. Why Arithmetic Right Shift? ⭐⭐⭐

Take −16 in 8-bit:

```text
11110000
```

Arithmetic right shift by 1:

```text
11111000
```

This equals −8.

So arithmetic right shift approximately performs signed division by 2.

## 13. Left Shift Overflow ⚠️

Example (8-bit):

```text
11110000 << 1
11100000
```

The leftmost 1 is lost.

Value changes unexpectedly.

### Interview point

Left shift can cause overflow/truncation.

## 14. Verilog Relevance ⭐⭐⭐

### Logical left shift

```verilog
y = a << 2;
```

### Logical right shift

```verilog
y = a >> 2;
```

### Arithmetic right shift

```verilog
y = a >>> 2;
```

🚨 `>>>` is very important for signed numbers.

## 15. Comparison Table ⭐⭐⭐

| Operation | Effect |
| --------- | ------ |
| `<< 1`    | ×2     |
| `<< 2`    | ×4     |
| `<< 3`    | ×8     |
| `>> 1`    | ÷2     |
| `>> 2`    | ÷4     |
| `>> 3`    | ÷8     |

For unsigned integers.

## 16. Placement Interview Questions ⭐⭐⭐

### Q1. Why are shifts faster than multiplication/division?

Because they are implemented by simple wiring, not complex arithmetic circuits.

### Q2. What is the difference between `>>` and `>>>` in Verilog?

* `>>` : logical right shift
* `>>>` : arithmetic right shift

### Q3. Can left shift overflow?

✅ Yes, if significant bits are discarded.

### Q4. What happens to the remainder in right-shift division?

It is discarded.

## 17. Quick Practice

### Q1

`00110110 << 1`

Answer:

```text
01101100
```

(54 × 2 = 108)

### Q2

`00110110 >> 2`

Answer:

```text
00001101
```

(54 ÷ 4 = 13)

### Q3 (Signed)

`11111100 >>> 1`

* `11111100` = −4
* Result = `11111110` = −2

## 18. One-Page Revision Sheet ⭐⭐⭐

### Shift Operations Quick Notes

### LEFT SHIFT (`<<`)

* Move bits left
* Fill right with 0
* Multiply by 2ⁿ
* May overflow

### RIGHT SHIFT (`>>`)

* Move bits right
* Fill left with 0 (unsigned)
* Divide by 2ⁿ (integer)
* Remainder discarded

### ARITHMETIC RIGHT SHIFT (`>>>`)

* Preserve sign bit
* Used for signed numbers

### Examples

```text
13 << 2 = 52
45 >> 3 = 5
−4 >>> 1 = −2
```

### Verilog

```text
<<   left shift
>>   logical right shift
>>>  arithmetic right shift ⭐
```

## Final Memory Trick ⭐⭐⭐

Think of binary point movement.

```text
LEFT  SHIFT → number becomes BIGGER → ×2
RIGHT SHIFT → number becomes SMALLER → ÷2
```

For n shifts:

```text
<< n → ×2ⁿ
>> n → ÷2ⁿ  (integer)
```
