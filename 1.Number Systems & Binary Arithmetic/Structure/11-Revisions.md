# PHASE 1 — NUMBER SYSTEMS & BINARY ARITHMETIC

## ⭐ Placement Revision Notes

---

# 1. NUMBER SYSTEMS ⭐⭐⭐

### Decimal

* Base = **10**
* Digits = `0–9`
* Positional weights = `10⁰, 10¹, 10²...`

### Binary

* Base = **2**
* Digits = `0, 1`
* Positional weights = `2⁰, 2¹, 2²...`

### Octal

* Base = **8**
* Digits = `0–7`

### Hexadecimal

* Base = **16**
* Digits = `0–9, A–F`

### Hexadecimal values ⭐

```text
A=10
B=11
C=12
D=13
E=14
F=15
```

---

# 2. BINARY ↔ HEX ↔ OCTAL ⭐⭐⭐

### Most important shortcut

**1 hex digit = 4 binary bits**

Example:

```text
A = 1010
F = 1111
```

---

**1 octal digit = 3 binary bits**

Example:

```text
5 = 101
7 = 111
```

### Binary → Hex

Group bits in **4s from the RIGHT**.

```text
10110110

→ 1011 0110

→ B6
```

### Binary → Octal

Group bits in **3s from the RIGHT**.

---

# 3. IMPORTANT POWERS OF 2 ⭐⭐⭐

Memorize:

```text
2⁰ = 1
2¹ = 2
2² = 4
2³ = 8
2⁴ = 16
2⁵ = 32
2⁶ = 64
2⁷ = 128
2⁸ = 256
2⁹ = 512
2¹⁰ = 1024
```

Very useful for aptitude questions.

---

# 4. DECIMAL ↔ BINARY

### Binary → Decimal

Multiply each bit by its power of 2 and add.

```text
10101

= 16 + 4 + 1

= 21
```

### Decimal → Binary

Repeatedly divide by 2 and read remainders **bottom → top**.

### Fast placement method ⭐

Use powers of 2.

Example:

```text
26 = 16 + 8 + 2
```

Therefore:

```text
26 = 11010₂
```

---

# 5. NUMBER OF VALUES REPRESENTED BY n BITS ⭐⭐⭐

```text
2ⁿ
```

Examples:

* 4 bits → `16 values`
* 5 bits → `32 values`
* 8 bits → `256 values`
* 16 bits → `65536 values`

---

# 6. UNSIGNED NUMBERS ⭐⭐⭐

For **n bits**:

```text
0 to 2ⁿ−1
```

Examples:

### 4-bit unsigned

`0 to 15`

### 8-bit unsigned

`0 to 255`

### Important

```text
11111111₂ = 255 unsigned
```

---

# 7. 1's COMPLEMENT ⭐⭐⭐

### Rule

**Invert every bit**

```text
0 → 1
1 → 0
```

Example:

```text
10110010

→ 01001101
```

### Memory trick

**1's = Invert**

---

# 8. 2's COMPLEMENT ⭐⭐⭐

### Rule

```text
1’s complement + 1
```

Example:

```text
00101100
```

1's complement:

```text
11010011
```

+1:

```text
11010100
```

### Fast method ⭐

From the **right**:

1. Copy bits up to and including the **first 1**
2. Invert everything to the left

This is much faster in placement exams.

### Memory trick

**2's = Invert + 1**

---

# 9. SIGNED NUMBERS — 2's COMPLEMENT ⭐⭐⭐

For n-bit signed number:

```text
−2ⁿ⁻¹ to 2ⁿ⁻¹−1
```

### Important ranges

| Bits | Signed range       |
| ---: | ------------------ |
|    4 | `-8 to +7`         |
|    5 | `-16 to +15`       |
|    6 | `-32 to +31`       |
|    8 | `-128 to +127`     |
|   16 | `-32768 to +32767` |

### MSB

```text
0 → Positive
1 → Negative
```

---

# 10. IMPORTANT SIGNED VALUES ⭐⭐⭐

For 8-bit signed:

```text
00000000 = 0

01111111 = +127

10000000 = -128

11111111 = -1
```

### Important trap

`10000000` is:

* Unsigned = **128**
* Signed = **−128**

`11111111` is:

* Unsigned = **255**
* Signed = **−1**

The bit pattern alone is **not enough**; you must know whether it is signed or unsigned.

---

# 11. SIGN EXTENSION ⭐⭐⭐

When increasing the width of a signed number:

### Positive

Fill with `0`

```text
0101 → 00000101
```

### Negative

Fill with `1`

```text
1101 → 11111101
```

### Memory trick

**Copy the sign bit.**

---

# 12. BINARY ADDITION ⭐⭐⭐

### Basic rules

```text
0 + 0 = 0

0 + 1 = 1

1 + 0 = 1

1 + 1 = 10
```

Most important:

```text
1+1=10
```

Meaning:

* Sum = `0`
* Carry = `1`

### With carry

```text
1 + 1 + 1 = 11
```

Sum = `1`

Carry = `1`

---

# 13. HALF ADDER ⭐⭐⭐

For two inputs `A` and `B`:

### Sum

```text
A⊕B
```

### Carry

```text
A⋅B
```

So:

**Sum = XOR**

**Carry = AND**

This becomes very important in **Phase 4**.

---

# 14. BINARY SUBTRACTION ⭐⭐⭐

Basic rules:

```text
0 - 0 = 0

1 - 0 = 1

1 - 1 = 0

0 - 1 → Borrow
```

### Hardware shortcut ⭐⭐⭐

Instead of direct subtraction:

```text
A−B = A + 2’s complement of B
```

This is the key idea behind digital subtractors.

---

# 15. 2's COMPLEMENT SUBTRACTION ⭐⭐⭐

Example:

```text
7 - 5
```

```text
0111
```

2's complement of `0101`:

```text
1011
```

Add:

```text
0111 + 1011 = 1 0010
```

Discard end carry:

```text
0010 = 2
```

### Rule

**End carry = 1 → discard it**

---

# 16. NEGATIVE RESULT IN SUBTRACTION ⭐⭐⭐

Example:

```text
5 - 7
```

```text
0101 + 1001 = 1110
```

No end carry.

Result is negative.

Take 2's complement:

```text
1110 → 0010
```

Therefore:

```text
−2
```

### Key rule

**No end carry → negative result**

Then take 2's complement to find magnitude.

---

# 17. CARRY vs OVERFLOW ⭐⭐⭐⭐⭐

This is one of the **most important interview concepts in Phase 1**.

### Carry

Relevant to **unsigned arithmetic**.

### Overflow

Relevant to **signed arithmetic**.

---

## Signed overflow rule

### Positive + Positive → Negative

**Overflow**

Example:

```text
0111 + 0001 = 1000
```

`+7 + +1 = +8`, but 4-bit signed max is +7.

So overflow.

---

### Negative + Negative → Positive

**Overflow**

Example:

```text
1100 + 1011
```

`-4 + -5 = -9`

Outside 4-bit range.

Overflow.

---

### Different signs

**No signed overflow**

Example:

```text
0101 + 1100
```

`+5 + -4 = +1`

No overflow.

---

# 18. MOST IMPORTANT CARRY/OVERFLOW TRAP ⭐⭐⭐⭐⭐

### Carry can occur without signed overflow

Example:

```text
1111 + 0001
```

* Carry = 1
* Signed overflow = No

### Overflow can occur without carry

Example:

```text
0111 + 0001
```

* Carry = 0
* Signed overflow = Yes

Therefore:

```text
Carry ≠ Overflow
```

Never use carry alone to detect signed overflow.

---

# 19. BINARY MULTIPLICATION ⭐⭐

### Basic rules

```text
0×0=0
0×1=0
1×0=0
1×1=1
```

### Hardware idea

```text
Shift + Add
```

### Example

```text
101 × 11
```

Partial products are shifted and added.

---

# 20. MULTIPLICATION WIDTH ⭐⭐⭐

For:

```text
n-bit × m-bit
```

maximum product may require:

```text
n+m bits
```

Examples:

* 4 × 4 → **8 bits**
* 8 × 8 → **16 bits**
* 16 × 16 → **32 bits**

---

# 21. LEFT SHIFT ⭐⭐⭐

### Basic rule

For unsigned values when width/overflow is not an issue:

```text
A << n = A × 2ⁿ
```

Examples:

```text
<<1 → ×2

<<2 → ×4

<<3 → ×8
```

### Example

```text
001101

001101 << 2

110100
```

13 × 4 = 52

---

# 22. RIGHT SHIFT ⭐⭐⭐

For **unsigned integers**:

```text
A >> n = ⌊A/2ⁿ⌋
```

Examples:

```text
>>1 → ÷2

>>2 → ÷4

>>3 → ÷8
```

### Important

Right shifting performs **integer division**.

The discarded remainder is lost.

Example:

```text
1011 >> 1
```

`1011 = 11`

Result = `0101 = 5`

11 ÷ 2 = 5 remainder 1

The remainder is discarded.

---

# 23. LOGICAL vs ARITHMETIC RIGHT SHIFT ⭐⭐⭐⭐⭐

### Logical right shift

Fill left side with `0`.

Used for unsigned data.

```text
10110000 >> 2

→ 00101100
```

### Arithmetic right shift

Fill left side with the **sign bit**.

Used for signed data.

```text
11110000 >>> 2

→ 11111100
```

This preserves the negative sign.

---

# 24. VERILOG SHIFT OPERATORS ⭐⭐⭐

### Left shift

```text
a << 2
```

### Logical right shift

```text
a >> 2
```

### Arithmetic right shift

```text
a >>> 2
```

### Placement interview favorite

`>> vs >>>`

* `>>` → logical right shift
* `>>>` → arithmetic right shift

---

# 25. BINARY DIVISION ⭐⭐

Binary division follows long division:

**Compare → Subtract → Bring down**

### Important formula ⭐

```text
Dividend = Divisor × Quotient + Remainder
```

### Division by powers of 2

```text
>>1 → ÷2

>>2 → ÷4

>>3 → ÷8
```

---

# 26. COMMON PLACEMENT SHORTCUTS ⭐⭐⭐

### Powers of 2

```text
×2 → <<1

×4 → <<2

×8 → <<3
```

---

```text
÷2 → >>1

÷4 → >>2

÷8 → >>3
```

---

### Signed range

```text
−2ⁿ⁻¹ to 2ⁿ⁻¹−1
```

### Unsigned range

```text
0 to 2ⁿ−1
```

### Number of values

```text
2ⁿ
```

---

# 27. TOP INTERVIEW TRAPS ⭐⭐⭐⭐⭐

### Trap 1

```text
11111111
```

Unsigned → **255**

Signed → **−1**

---

### Trap 2

```text
10000000
```

Unsigned → **128**

Signed → **−128**

---

### Trap 3

**Carry ≠ Overflow**

---

### Trap 4

**1's complement = invert**

**2's complement = invert + 1**

---

### Trap 5

**Positive + Positive → Negative**

→ Signed overflow

---

### Trap 6

**Negative + Negative → Positive**

→ Signed overflow

---

### Trap 7

Right shift is not always exact division.

```text
11 >> 1 = 5
```

not 5.5.

---

### Trap 8

For signed right shift, distinguish:

```text
>> and >>>
```

---

# 28. VERILOG CONNECTION ⭐⭐⭐

### Number representations

```verilog
8'b10101010   // binary
```

```verilog
8'd170        // decimal
```

```verilog
8'hAA         // hexadecimal
```

```verilog
8'o252        // octal
```

### Signed declaration

```verilog
reg [7:0] a;          // unsigned
```

```verilog
reg signed [7:0] b;   // signed
```

### Arithmetic

```text
a + b
```

```text
a - b
```

```text
a * b
```

```text
a / b
```

### Shifts

```text
a << 2
```

```text
a >> 2
```

```text
a >>> 2
```

---

# PHASE 1 — MUST MEMORIZE ⭐⭐⭐⭐⭐

Before moving to Phase 2, these should be automatic:

```text
Binary base = 2

Octal base = 8

Decimal base = 10

Hex base = 16
```

```text
1 hex digit = 4 bits

1 octal digit = 3 bits
```

```text
n-bit unsigned range = 0 to 2^n - 1

n-bit signed range   = -2^(n-1) to 2^(n-1)-1
```

```text
1's complement = invert

2's complement = invert + 1
```

```text
1+1 = 10

1+1+1 = 11
```

```text
A-B = A + 2's complement(B)
```

```text
Carry → unsigned

Overflow → signed
```

```text
Positive + Positive → Negative → overflow

Negative + Negative → Positive → overflow
```

```text
<<1 = ×2

<<2 = ×4

<<3 = ×8
```

```text
>>1 = integer ÷2

>>2 = integer ÷4

>>3 = integer ÷8
```

```text
>>  = logical right shift

>>> = arithmetic right shift
```

```text
n-bit × m-bit → up to n+m bits
```

## ⭐⭐⭐ Phase 1 Priority

**Must know extremely well:**

**2's complement**

**Signed/unsigned ranges**

**Carry vs overflow**

**Binary addition/subtraction**

**Shift operations**

**Binary ↔ Hex conversion**

These are the strongest foundation for the **Boolean algebra, K-map, adders, Verilog, FSM, timing, and VLSI topics** that follow.
