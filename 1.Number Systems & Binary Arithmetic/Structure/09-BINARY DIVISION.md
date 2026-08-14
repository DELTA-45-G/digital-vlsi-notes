# BINARY DIVISION ⭐⭐

This topic is less frequently asked than addition/subtraction, but it is still important for:

* Digital arithmetic understanding
* ALU concepts
* Computer architecture
* Placement MCQs

## 1. What is Binary Division?

Dividing one binary number by another.

Example:

### `1100 ÷ 10`

`12 ÷ 2 = 6`

## 2. Why is it needed?

Processors perform division for:

* Percentage calculations
* Address computations
* DSP algorithms
* Arithmetic instructions

## 3. Basic Idea

Binary division works exactly like decimal long division.

You repeatedly:

* Compare
* Subtract
* Bring down the next bit

## 4. Division Rules ⭐

| Operation | Result       |
| --------- | ------------ |
| `0 ÷ 1`   | `0`          |
| `1 ÷ 1`   | `1`          |
| `0 ÷ 0`   | Undefined    |
| `1 ÷ 0`   | Undefined ⚠️ |

## 5. Easy Example ⭐

Compute:

### `1010 ÷ 10`

`10 ÷ 2 = 5`

Result:

### `101`

## 6. Long Division Example ⭐⭐

Compute:

```text
      101
    -------
10 ) 1010
```

### Step-by-step

* 10 goes into 10 → 1
* Bring down 1 → 01
* 10 does not go into 01 → 0
* Bring down 0 → 10
* 10 goes into 10 → 1

Result:

### `101`

Remainder = 0

## 7. Example with Remainder ⭐⭐

Compute:

### `1110 ÷ 11`

`14 ÷ 3`

### Long division

* 11 into 11 → 1
* Subtract → 00
* Bring down 1 → 1
* 11 into 1 → 0
* Bring down 0 → 10
* 11 into 10 → 0

Quotient:

### `100₂`

Remainder = `10₂`

Check:

* Quotient = 4
* Remainder = 2
* 4×3 + 2 = 14 ✔️

## 8. The Most Important Check ⭐

```text
Dividend = Divisor × Quotient + Remainder
```

## 9. Division by Powers of 2 ⭐⭐⭐

This is the interview shortcut.

### Right shift

| Operation | Shortcut      |
| --------- | ------------- |
| ÷2        | Right shift 1 |
| ÷4        | Right shift 2 |
| ÷8        | Right shift 3 |

Example:

```text
110100 ÷ 1000
```

```text
110100 >> 3 = 110
```

* 52 ÷ 8 = 6 remainder 4
* Integer quotient = `110₂`

## 10. Hardware Intuition ⭐⭐⭐

Division is often implemented using:

* Shift
* Compare
* Subtract
* Restore (in restoring division)

Much more complex than an adder.

## 11. Placement-Level Example ⭐⭐⭐

Compute:

### `101101 ÷ 101`

45 ÷ 5

Expected answer: 9

Binary quotient:

### `1001`

Remainder = 0

## 12. Common Mistakes ❌

* Forgetting leading zeros in quotient
* Wrong remainder check
* Confusing right shift with exact division
* Ignoring discarded bits

## 13. Right Shift Nuance ⭐⭐

For unsigned integers:

### `1011 >> 1 = 0101`

11 ÷ 2 = 5 (integer)

The remainder is discarded.

## 14. Interview Questions ⭐⭐⭐

### Q1. Why is division slower than multiplication?

Because it requires iterative compare-subtract-shift operations.

### Q2. What is the shortcut for division by 2ⁿ?

Right shift by n.

### Q3. What happens to the remainder during right shift?

It is discarded.

## 15. MCQs

### Q1. `1000 ÷ 10 =`

* A) 10
* B) 100 ✅
* C) 1000
* D) 1

### Q2. Right shift by 2 means:

* A) ÷2
* B) ÷4 ✅
* C) ÷8
* D) ×4

### Q3. `1 ÷ 0` is:

* A) 0
* B) 1
* C) Undefined ✅
* D) Infinity

## 16. Verilog Relevance ⭐⭐

```verilog
assign q = a / b;
```

Synthesis may create a large divider circuit.

Division is usually more expensive than:

* `+`
* `-`
* `<<`
* `>>`

For powers of 2, use shifts:

```verilog
assign q = a >> 3;  // divide by 8
```

## 17. One-Page Quick Revision

### Binary Division Quick Sheet

```text
1÷1=1
0÷1=0
1÷0 = Undefined ⚠️
```

### Long division

```text
Compare → Subtract → Bring down
```

### Check ⭐

```text
Dividend = Divisor×Quotient + Remainder
```

### Power-of-2 shortcut ⭐⭐⭐

```text
>>1 → ÷2
>>2 → ÷4
>>3 → ÷8
```

### Hardware

```text
Shift + Compare + Subtract
```
