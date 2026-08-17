# VERILOG OPERATORS ⭐⭐⭐⭐⭐

Verilog operators are used to **perform operations on signals and values**.

For VLSI placements, you should be comfortable with:

```text
Arithmetic
```

Relational

Equality

Logical

Bitwise

Reduction

Shift

Concatenation

Replication

Conditional

---

# 1. Arithmetic Operators

Arithmetic operators perform mathematical operations.

| Operator | Meaning        |
| -------- | -------------- |
| `+`      | Addition       |
| `-`      | Subtraction    |
| `*`      | Multiplication |
| `/`      | Division       |
| `%`      | Modulus        |

Example:

```text
assign y = a + b;
```

---

# 2. Addition

```text
assign sum = a + b;
```

Example:

```text
a = 5
```

b = 3

sum = 8

---

# 3. Subtraction

```text
assign y = a - b;
```

Example:

```text
8 - 3 = 5
```

---

# 4. Multiplication

```text
assign y = a * b;
```

Example:

```text
4 × 3 = 12
```

In synthesizable RTL, multiplication can result in significant hardware depending on the operands and synthesis technology.

---

# 5. Division

```text
assign y = a / b;
```

Example:

```text
10 / 2 = 5
```

Division by zero is invalid.

---

# 6. Modulus `%`

The modulus operator returns the remainder.

```text
assign y = a % b;
```

Example:

```text
10 % 3 = 1
```

because:

10=3×3+1

---

# 7. Relational Operators ⭐⭐⭐⭐⭐

Relational operators compare two values.

| Operator | Meaning               |
| -------- | --------------------- |
| `<`      | Less than             |
| `>`      | Greater than          |
| `<=`     | Less than or equal    |
| `>=`     | Greater than or equal |

Example:

```text
assign y = (a > b);
```

The result is generally a **1-bit logical result**.

---

# 8. Example of Relational Operators

```text
a = 5;
```

b = 3;

Then:

```text
a > b  → 1
```

a < b  → 0

a >= b → 1

a <= b → 0

---

# 9. Equality Operators ⭐⭐⭐⭐⭐

Verilog has two important pairs of equality operators.

### Logical equality

```text
==
```

!=

### Case equality

```text
===
```

!==

---

# 10. `==` Logical Equality

Example:

```text
assign y = (a == b);
```

It compares operands while allowing unknown/high-impedance behavior to affect the result according to Verilog's 4-state equality rules.

---

# 11. `!=` Not Equal

```text
assign y = (a != b);
```

Returns true when the operands are logically unequal.

---

# 12. `===` Case Equality ⭐⭐⭐⭐⭐

Case equality compares all four states:

```text
0
```

1

X

Z

Example:

```text
a === b
```

It checks exact 4-state matching.

For example:

```text
1'bx === 1'bx
```

returns:

```text
1
```

---

# 13. `!==` Case Inequality

```text
a !== b
```

Returns `1` when the operands are not exactly equal, including differences involving:

```text
X
```

Z

---

# 14. `==` vs `===` ⭐⭐⭐⭐⭐

This is a **frequently asked placement question**.

| `==`                        | `===`                                     |
| --------------------------- | ----------------------------------------- |
| Logical equality            | Case equality                             |
| X/Z can make result unknown | X/Z are compared explicitly               |
| Common in RTL conditions    | Commonly useful in simulation/testbenches |
| 4-state uncertainty matters | Exact 4-state matching                    |

### Memory trick

```text
==  → normal equality
```

=== → exact 4-state equality

---

# 15. Logical Operators ⭐⭐⭐⭐⭐

Logical operators are:

```text
&&
```

||

!

| Operator | Meaning     |   |            |
| -------- | ----------- | - | ---------- |
| `&&`     | Logical AND |   |            |
| `        |             | ` | Logical OR |
| `!`      | Logical NOT |   |            |

---

# 16. Logical AND `&&`

Example:

```text
assign y = a && b;
```

Truth table:

| a | b | `a && b` |
| - | - | -------- |
| 0 | 0 | 0        |
| 0 | 1 | 0        |
| 1 | 0 | 0        |
| 1 | 1 | 1        |

Logical operators treat operands as logical conditions rather than performing bit-by-bit operations.

---

# 17. Logical OR `||`

```text
assign y = a || b;
```

Truth table:

| a | b | `a || b` |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

---

# 18. Logical NOT `!`

```text
assign y = !a;
```

For known 0/1 values:

```text
a = 0 → !a = 1
```

a = 1 → !a = 0

---

# 19. Bitwise Operators ⭐⭐⭐⭐⭐

Bitwise operators operate **bit-by-bit**.

Main operators:

```text
&
```

|

^

~

^~

~^

---

# 20. Bitwise AND `&`

Example:

```text
assign y = a & b;
```

If:

```text
a = 4'b1010
```

b = 4'b1100

Then:

```text
  1010
```

& 1100

---

1000

Therefore:

```text
y = 1000
```

---

# 21. Bitwise OR `|`

```text
assign y = a | b;
```

Example:

```text
  1010
```

| 1100

---

1110

---

# 22. Bitwise XOR `^`

```text
assign y = a ^ b;
```

Example:

```text
  1010
```

^ 1100

---

0110

XOR produces `1` when the corresponding bits are different.

---

# 23. Bitwise NOT `~`

```text
assign y = ~a;
```

For:

```text
a = 4'b1010
```

then:

```text
~a = 4'b0101
```

---

# 24. XNOR

XNOR can be written as:

```text
^~
```

or:

```text
~^
```

Example:

```text
assign y = a ^~ b;
```

XNOR produces `1` when corresponding bits are equal.

---

# 25. Logical vs Bitwise Operators ⭐⭐⭐⭐⭐

This is extremely important.

### Logical

```text
&&
```

||

!

### Bitwise

```text
&
```

|

^

~

Example:

```text
a = 4'b1010;
```

b = 4'b1100;

### Bitwise AND

```text
a & b
```

gives:

```text
1000
```

### Logical AND

```text
a && b
```

gives a **1-bit logical result** because both operands are non-zero.

```text
1
```

---

# 26. Memory Trick

```text
&& → logical AND
```

&  → bitwise AND

```text
|| → logical OR
```

|  → bitwise OR

```text
!  → logical NOT
```

~  → bitwise NOT

---

# 27. Reduction Operators ⭐⭐⭐⭐⭐

Reduction operators reduce an entire vector to **one bit**.

Operators:

```text
&
```

|

^

~&

~|

~^

^~

---

# 28. Reduction AND

```text
assign y = &a;
```

If:

```text
a = 4'b1111
```

then:

```text
& a = 1
```

because:

```text
1 & 1 & 1 & 1 = 1
```

If:

```text
a = 4'b1110
```

then:

```text
& a = 0
```

---

# 29. Reduction OR

```text
assign y = |a;
```

If:

```text
a = 4'b0001
```

then:

```text
|a = 1
```

because at least one bit is `1`.

If:

```text
a = 4'b0000
```

then:

```text
|a = 0
```

---

# 30. Reduction XOR

```text
assign y = ^a;
```

It performs XOR across all bits.

Example:

```text
a = 4'b1011
```

Then:

```text
1 ^ 0 ^ 1 ^ 1 = 1
```

So:

```text
^a = 1
```

---

# 31. Reduction XNOR

```text
assign y = ~^a;
```

or:

```text
assign y = ^~a;
```

This produces the complement of reduction XOR.

---

# 32. Reduction NAND

```text
assign y = ~&a;
```

It is:

∼(&a)

---

# 33. Reduction NOR

```text
assign y = ~|a;
```

It is:

∼(|a)

---

# 34. Bitwise vs Reduction ⭐⭐⭐⭐⭐

Another major placement question.

### Bitwise

```text
a & b
```

If `a` and `b` are 4-bit:

```text
4-bit output
```

### Reduction

```text
&a
```

If `a` is 4-bit:

```text
1-bit output
```

### Memory trick

Bitwise → bit-by-bit

Reduction → whole vector → 1 bit

---

# 35. Shift Operators

Shift operators:

```text
<<
```

> >

<<<

> > >

Basic logical shifts:

```text
<< → left shift
```

> > → right shift

---

# 36. Left Shift `<<`

Example:

```text
assign y = a << 1;
```

For:

```text
a = 4'b0011
```

then:

```text
0011 << 1
```

= 0110

Bits shift toward the left and zeros are introduced on the right for logical shifting.

---

# 37. Right Shift `>>`

Example:

```text
assign y = a >> 1;
```

For:

```text
a = 4'b1100
```

then:

```text
1100 >> 1
```

= 0110

Zeros are introduced on the left for logical right shifting of an unsigned value.

---

# 38. Arithmetic Shift ⭐⭐⭐⭐⭐

Arithmetic shifts are:

```text
<<<
```

> > >

The important one for signed values is:

```text
>>>
```

Arithmetic right shift preserves the sign by replicating the sign bit.

Example:

```text
1100 >>> 1
```

for a signed value gives:

```text
1110
```

rather than:

```text
0110
```

---

# 39. `<<` vs `<<<`

For left shifts, both can often produce the same bit movement, but the arithmetic operator is intended for signed arithmetic semantics.

For placement preparation, remember:

```text
<<  → logical left shift
```

> > → logical right shift

> > > → arithmetic right shift

<<< → arithmetic left shift

---

# 40. Concatenation Operator ⭐⭐⭐⭐⭐

Concatenation combines multiple signals.

Operator:

```text
{}
```

Example:

```text
assign y = {a, b};
```

If:

```text
a = 4'b1010
```

b = 4'b1100

then:

```text
y = 8'b10101100
```

---

# 41. Concatenation Example

```text
{4'b1010, 4'b0011}
```

gives:

```text
8'b10100011
```

The left operand becomes the more significant portion.

---

# 42. Concatenation with Single Bits

Example:

```text
assign y = {a, b, c};
```

If each is 1 bit:

```text
a = 1
```

b = 0

c = 1

then:

```text
y = 3'b101
```

---

# 43. Replication Operator ⭐⭐⭐⭐⭐

Replication repeats a bit pattern.

Syntax:

```text
{N{expression}}
```

Example:

```text
{4{1'b1}}
```

produces:

```text
1111
```

---

# 44. Replication Example

```text
{4{2'b10}}
```

produces:

```text
10101010
```

Because:

```text
10
```

10

10

10

Total width:

4×2=8 bits

---

# 45. Concatenation vs Replication

### Concatenation

```text
{a, b}
```

Combines different expressions.

### Replication

```text
{4{a}}
```

Repeats an expression four times.

---

# 46. Conditional Operator ⭐⭐⭐⭐⭐

The conditional operator is:

```text
?:
```

Syntax:

```text
condition ? true_value : false_value
```

Example:

```text
assign y = sel ? b : a;
```

Meaning:

```text
sel = 1 → y = b
```

sel = 0 → y = a

This is commonly used to describe a **multiplexer**.

---

# 47. Conditional Operator as MUX

```text
       sel
```

```
    |
```

┌────┴────┐

│   MUX   │

a ─│0      y│

b ─│1       │

└─────────┘

---

# 48. Unary Operators

Operators acting on a single operand are called unary operators.

Examples:

```text
~a
```

!a

&a

|a

^a

They operate on one operand.

---

# 49. Binary Operators

Binary operators operate on two operands.

Examples:

```text
a + b
```

a & b

a == b

a && b

---

# 50. Operator Categories — Quick Table

| Category      | Operators             |
| ------------- | --------------------- |
| Arithmetic    | `+ - * / %`           |
| Relational    | `< > <= >=`           |
| Equality      | `== != === !==`       |
| Logical       | `&& \|\| !`           |
| Bitwise       | `& \| ^ ~ ^~ ~^`      |
| Reduction     | `& \| ^ ~& ~\| ~^ ^~` |
| Shift         | `<< >> <<< >>>`       |
| Concatenation | `{}`                  |
| Replication   | `{{}}`                |
| Conditional   | `?:`                  |

---

# ⭐ Frequently Asked Placement Questions

## Q1. What is the difference between `&` and `&&`?

**Answer:**

```text
&  → Bitwise AND
```

&& → Logical AND

For multi-bit operands, `&` produces a bit-by-bit result, while `&&` produces a logical result.

---

## Q2. What is the difference between `|` and `||`?

**Answer:**

```text
|  → Bitwise OR
```

|| → Logical OR

---

## Q3. What is the difference between `~` and `!`?

**Answer:**

```text
~ → Bitwise NOT
```

! → Logical NOT

---

## Q4. What is a reduction operator?

**Answer:** A reduction operator operates on all bits of a vector and produces a **single-bit result**.

Example:

```text
&a
```

---

## Q5. What does `&4'b1111` produce?

1&1&1&1=1

**Answer:**

```text
1
```

---

## Q6. What does `|4'b0000` produce?

**Answer:**

```text
0
```

---

## Q7. What does `^4'b1011` produce?

1⊕0⊕1⊕1=1

**Answer:**

```text
1
```

---

## Q8. What is the difference between bitwise and reduction operators?

**Answer:**

```text
Bitwise → operates bit-by-bit
```

Reduction → reduces a vector to one bit

Example:

```text
a & b    // multi-bit result
```

&a       // 1-bit result

---

## Q9. What is the difference between `==` and `===`?

**Answer:**

```text
==  → logical equality
```

=== → case equality, including exact X/Z comparison

---

## Q10. What does `>>>` do?

**Answer:** It performs an **arithmetic right shift**, preserving the sign for signed operands.

---

## Q11. What does `<<` do?

**Answer:** It performs a logical left shift.

---

## Q12. What does `{a,b}` mean?

**Answer:** Concatenation of `a` and `b`.

---

## Q13. What does `{4{1'b1}}` mean?

**Answer:**

```text
1111
```

It replicates `1'b1` four times.

---

## Q14. What does `{4{2'b10}}` produce?

```text
10101010
```

**Answer: 8 bits.**

---

## Q15. What is the conditional operator?

**Answer:**

```text
condition ? true_expression : false_expression
```

It is commonly used to describe multiplexers.

---

## Q16. Which operator is commonly used to implement a 2:1 MUX?

```text
assign y = sel ? b : a;
```

**Answer:**

```text
Conditional operator `?:`
```

---

# 🔥 Placement Rapid-Fire

**Addition?**

→ `+`

**Modulus?**

→ `%`

**Greater than?**

→ `>`

**Equality?**

→ `==`

**Case equality?**

→ `===`

**Logical AND?**

→ `&&`

**Bitwise AND?**

→ `&`

**Logical OR?**

→ `||`

**Bitwise OR?**

→ `|`

**Logical NOT?**

→ `!`

**Bitwise NOT?**

→ `~`

**Reduction AND?**

→ `&a`

**Reduction OR?**

→ `|a`

**Reduction XOR?**

→ `^a`

**Left shift?**

→ `<<`

**Logical right shift?**

→ `>>`

**Arithmetic right shift?**

→ `>>>`

**Concatenation?**

→ `{}`

**Replication?**

→ `{N{expression}}`

**Conditional/MUX operator?**

→ `?:`

---

# 🧠 9.10 QUICK REVISION

```text
ARITHMETIC
```

* * * /  %

RELATIONAL

<  >  <=  >=

EQUALITY

==  !=  ===  !==

LOGICAL

&&  ||  !

BITWISE

&  |  ^  ~  ^~  ~^

REDUCTION

&  |  ^  ~&  ~|  ~^  ^~

SHIFT

<<  >>  <<<  >>>

CONCATENATION

{a,b}

REPLICATION

{N{a}}

CONDITIONAL

condition ? true : false

### ⭐ Most important distinctions

```text
&  → Bitwise AND
```

&& → Logical AND

```text
|  → Bitwise OR
```

|| → Logical OR

```text
~ → Bitwise NOT
```

! → Logical NOT

```text
&a → Reduction AND
```

```text
a & b → Bitwise AND
```

```text
==  → Logical equality
```

=== → Case equality

```text
>>  → Logical right shift
```

> > > → Arithmetic right shift

```text
{a,b}       → Concatenation
```

{4{a}}      → Replication

```text
sel ? b : a → MUX
```
