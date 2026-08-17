# CONDITIONAL STATEMENTS IN VERILOG

## `if`, `if-else`, `else-if`, and `case` ⭐⭐⭐⭐⭐

Conditional statements are used to make **decisions in Verilog RTL**.

They are extremely important for placements because they are commonly used to describe:

* Multiplexers
* Decoders
* Priority logic
* Control logic
* FSMs
* Registers with enable/reset
* Combinational logic

---

# 1. What is a Conditional Statement?

A conditional statement selects which statement or block should execute based on a condition.

The most common constructs are:

```text
if
if-else
else-if
case
casez
casex
```

---

# 2. `if` Statement

Basic syntax:

```verilog
if (condition)
    statement;
```

Example:

```verilog
if (en)
    y = a;
```

Meaning:

```text
en = 1 → y = a
en = 0 → no assignment
```

⚠️ In combinational logic, the second case can cause a latch if `y` retains its previous value.

---

# 3. `if-else` Statement ⭐⭐⭐⭐⭐

Syntax:

```verilog
if (condition)
    statement1;
else
    statement2;
```

Example:

```verilog
if (sel)
    y = b;
else
    y = a;
```

This describes a **2:1 multiplexer**.

```text
sel = 0 → y = a
sel = 1 → y = b
```

---

# 4. `if-else` MUX

```verilog
always @(*) begin
    if (sel)
        y = b;
    else
        y = a;
end
```

Hardware:

```text
       ┌─────┐
a ────→│     │
       │ MUX ├──→ y
b ────→│     │
       └──┬──┘
          ↑
         sel
```

---

# 5. `if-else-if` ⭐⭐⭐⭐⭐

Used when there are multiple conditions.

Syntax:

```verilog
if (condition1)
    statement1;
else if (condition2)
    statement2;
else
    statement3;
```

Example:

```verilog
always @(*) begin
    if (a)
        y = 1;
    else if (b)
        y = 2;
    else
        y = 0;
end
```

---

# 6. Priority Behavior of `if-else-if`

Consider:

```verilog
if (a)
    y = 1;
else if (b)
    y = 2;
else
    y = 0;
```

If both:

```text
a = 1
b = 1
```

then:

```text
y = 1
```

because the first true condition has priority.

Therefore:

```text
if-else-if → priority behavior
```

This is a very important interview concept.

---

# 7. Example — Priority Encoder

```verilog
always @(*) begin
    if (d3)
        y = 2'b11;
    else if (d2)
        y = 2'b10;
    else if (d1)
        y = 2'b01;
    else if (d0)
        y = 2'b00;
    else
        y = 2'bxx;
end
```

If multiple inputs are `1`, the highest-priority condition is selected.

---

# 8. Nested `if`

An `if` can be placed inside another `if`.

Example:

```verilog
if (en) begin
    if (sel)
        y = a;
    else
        y = b;
end
```

Nested conditions can create complex control logic.

---

# 9. Importance of `begin` and `end`

Without `begin/end`, an `if` controls only **one statement**.

Example:

```verilog
if (en)
    y = a;

z = b;
```

Only:

```text
y = a;
```

belongs to the `if`.

`z = b;` executes regardless of `en`.

---

# 10. Using `begin/end`

To include multiple statements:

```verilog
if (en) begin
    y = a;
    z = b;
end
```

Now both statements belong to the `if`.

### Memory trick:

```text
if + one statement → begin/end not required
if + multiple statements → use begin/end
```

---

# 11. `case` Statement ⭐⭐⭐⭐⭐

The `case` statement is used to select one of multiple alternatives based on an expression.

Syntax:

```verilog
case (expression)
    value1: statement1;
    value2: statement2;
    value3: statement3;
    default: statement4;
endcase
```

Example:

```verilog
case (sel)
    2'b00: y = a;
    2'b01: y = b;
    2'b10: y = c;
    2'b11: y = d;
endcase
```

This describes a **4:1 multiplexer**.

---

# 12. `case` Example — 4:1 MUX

```verilog
always @(*) begin
    case (sel)
        2'b00: y = a;
        2'b01: y = b;
        2'b10: y = c;
        2'b11: y = d;
        default: y = 1'b0;
    endcase
end
```

Selection:

```text
sel = 00 → a
sel = 01 → b
sel = 10 → c
sel = 11 → d
```

---

# 13. Why Use `case`?

`case` is often cleaner than writing many `if-else-if` conditions.

Instead of:

```verilog
if (sel == 2'b00)
    y = a;
else if (sel == 2'b01)
    y = b;
else if (sel == 2'b10)
    y = c;
else
    y = d;
```

you can write:

```verilog
case (sel)
    2'b00: y = a;
    2'b01: y = b;
    2'b10: y = c;
    2'b11: y = d;
endcase
```

---

# 14. `default` ⭐⭐⭐⭐⭐

A `default` branch handles values that do not match any explicit case item.

Example:

```verilog
case (sel)
    2'b00: y = a;
    2'b01: y = b;
    2'b10: y = c;
    2'b11: y = d;
    default: y = 0;
endcase
```

### Why is `default` important?

It helps ensure that an output gets a value for all possible conditions and can prevent unintended latch inference in combinational logic.

---

# 15. `case` vs `if-else`

| `if-else`                         | `case`                              |
| --------------------------------- | ----------------------------------- |
| Evaluates conditions sequentially | Compares expression with case items |
| Naturally represents priority     | Often used for selection            |
| Good for priority logic           | Good for decoders/MUX/FSM           |
| First true condition wins         | Matching case item selected         |

---

# 16. `case` Does Not Automatically Mean Priority

Consider:

```verilog
case (sel)
    2'b00: y = a;
    2'b01: y = b;
    2'b10: y = c;
    2'b11: y = d;
endcase
```

The selector values are mutually exclusive.

Therefore it naturally represents selection rather than a priority chain.

---

# 17. `case` Statement with Multiple Statements

Use `begin/end` when a case item contains multiple statements.

```verilog
case (sel)

    2'b00: begin
        y = a;
        z = b;
    end

    2'b01: begin
        y = c;
        z = d;
    end

endcase
```

---

# 18. `case` for FSMs ⭐⭐⭐⭐⭐

`case` is commonly used in state-machine logic.

Example:

```verilog
case (state)

    IDLE:
        next_state = START;

    START:
        next_state = RUN;

    RUN:
        next_state = DONE;

    DONE:
        next_state = IDLE;

    default:
        next_state = IDLE;

endcase
```

This is extremely common in RTL design.

---

# 19. `casez`

`casez` treats `z` and `?` as don't-care bits during matching.

Example:

```verilog
casez (in)
    4'b1???: y = 2'b11;
    4'b01??: y = 2'b10;
    4'b001?: y = 2'b01;
    default: y = 2'b00;
endcase
```

This can be useful for priority encoding and wildcard matching.

---

# 20. `casex`

`casex` treats `x` and `z` as don't-care values during matching.

Example:

```verilog
casex (in)
    4'b1xxx: y = 2'b11;
    4'b01xx: y = 2'b10;
    default: y = 2'b00;
endcase
```

⚠️ `casex` should be used carefully because it can hide unknown (`X`) values during simulation.

For interview purposes:

```text
case  → exact matching
casez → Z / ? wildcard matching
casex → X / Z wildcard matching
```

---

# 21. `case` Matching

A normal `case` uses exact 4-state matching.

Possible Verilog values include:

```text
0
1
X
Z
```

Example:

```verilog
case (a)
    2'b00: y = 0;
    2'b01: y = 1;
    2'b10: y = 2;
    2'b11: y = 3;
endcase
```

---

# 22. `case` and `X/Z`

Normal `case` does not treat `X` or `Z` as ordinary don't-care values.

For example:

```verilog
case (sel)
    2'b00: y = a;
    2'b01: y = b;
endcase
```

If:

```text
sel = 2'b0x
```

it doesn't match `00` or `01` because the `x` is significant in normal case matching.

---

# 23. `casez` Wildcards

Example:

```verilog
casez (a)
    4'b1???: y = 1;
    default: y = 0;
endcase
```

The `?` bits are treated as don't-care for matching.

So:

```text
1000
1010
1101
1111
```

can all match:

```text
1???
```

---

# 24. Priority with `casez`

Consider:

```verilog
casez (in)
    4'b1???: y = 3;
    4'b01??: y = 2;
    4'b001?: y = 1;
    4'b0001: y = 0;
    default: y = 0;
endcase
```

The order of case items matters when multiple wildcard patterns can match.

The first matching item is selected.

---

# 25. `if` vs `case` — Placement Question

### Question:

When would you use `if-else` instead of `case`?

**Answer:**

Use `if-else` when conditions naturally have **priority or relational expressions**, while `case` is convenient when selecting based on a particular expression's value.

---

# 26. Relational Conditions

`if` can easily use conditions such as:

```verilog
if (a > b)
```

or:

```verilog
if (count == 4'd10)
```

or:

```verilog
if (enable && valid)
```

Example:

```verilog
if (count > 10)
    y = 1;
else
    y = 0;
```

---

# 27. `case` Uses One Main Expression

Example:

```verilog
case (opcode)
    4'b0000: y = a + b;
    4'b0001: y = a - b;
    4'b0010: y = a & b;
    4'b0011: y = a | b;
endcase
```

This is a common ALU-style control structure.

---

# 28. Conditional Operator `?:`

Another conditional construct is the ternary operator.

Syntax:

```verilog
condition ? true_value : false_value
```

Example:

```verilog
assign y = sel ? b : a;
```

This is equivalent to:

```verilog
always @(*) begin
    if (sel)
        y = b;
    else
        y = a;
end
```

---

# 29. Ternary Operator

The ternary operator has three operands:

```text
condition
    ?
true expression
    :
false expression
```

Example:

```verilog
assign y = enable ? data : 8'b0;
```

Meaning:

```text
enable = 1 → y = data
enable = 0 → y = 0
```

---

# 30. Nested Ternary

You can use multiple ternary operators:

```verilog
assign y = sel1 ? a :
           sel2 ? b :
           c;
```

This represents priority-like selection.

However, excessive nesting can reduce readability.

---

# 31. Conditional Statements and Hardware

### `if-else`

Can infer:

```text
MUX
```

### `case`

Can infer:

```text
MUX / Decoder / Control Logic
```

### Nested `if`

Can infer:

```text
Priority logic
```

### Ternary

Can infer:

```text
MUX
```

---

# 32. Important Latch Example ⭐⭐⭐⭐⭐

Bad combinational code:

```verilog
always @(*) begin
    if (sel)
        y = a;
end
```

What if:

```text
sel = 0
```

There is no assignment to `y`.

Therefore `y` needs to retain its previous value.

This can infer a latch.

---

# 33. Correct Version

```verilog
always @(*) begin
    if (sel)
        y = a;
    else
        y = b;
end
```

Now every condition assigns `y`.

No latch is inferred from this logic.

---

# 34. `case` and Latch

Bad:

```verilog
always @(*) begin
    case (sel)
        2'b00: y = a;
        2'b01: y = b;
    endcase
end
```

What happens for:

```text
10
11
```

No assignment occurs.

Potential latch inference.

---

# 35. Correct `case`

```verilog
always @(*) begin
    case (sel)
        2'b00: y = a;
        2'b01: y = b;
        default: y = 0;
    endcase
end
```

Now all possible values have an assignment.

---

# 36. Default Assignment Technique

Another common style:

```verilog
always @(*) begin

    y = 0;

    if (sel)
        y = a;

end
```

The default assignment ensures `y` always has a value.

---

# ⭐ Frequently Asked Placement Questions

## Q1. What is the purpose of an `if` statement?

**Answer:** It conditionally executes statements based on whether a condition is true.

---

## Q2. What does `if-else` commonly represent in hardware?

**Answer:** It can represent a multiplexer or conditional combinational logic.

---

## Q3. What is the main characteristic of an `if-else-if` chain?

**Answer:** It naturally creates **priority**, because the first true condition is selected.

---

## Q4. What is the purpose of `case`?

**Answer:** It selects statements based on the value of an expression.

---

## Q5. What is `default` in a case statement?

**Answer:** It handles values that do not match any explicitly listed case item.

---

## Q6. Why is `default` important in combinational logic?

**Answer:** It helps ensure that outputs receive a value for unmatched conditions and can prevent unintended latch inference.

---

## Q7. What is the difference between `case`, `casez`, and `casex`?

**Answer:**

```text
case  → exact matching
casez → Z / ? can act as wildcard
casex → X / Z can act as wildcard
```

---

## Q8. Why should `casex` be used carefully?

**Answer:** Because treating `X` as a don't-care can hide unknown or uninitialized signals during simulation.

---

## Q9. What happens if an output is not assigned in every branch of a combinational `if`?

**Answer:** A latch may be inferred.

---

## Q10. What happens if an output is not assigned in every branch of a combinational `case`?

**Answer:** A latch may be inferred.

---

## Q11. What does this describe?

```verilog
if (sel)
    y = b;
else
    y = a;
```

**Answer:** A 2:1 MUX.

---

## Q12. What does this describe?

```verilog
case (sel)
    2'b00: y = a;
    2'b01: y = b;
    2'b10: y = c;
    2'b11: y = d;
endcase
```

**Answer:** A 4:1 MUX.

---

## Q13. What is the difference between `if-else` and `case`?

**Answer:**

```text
if-else → good for priority/conditional expressions
case    → good for selection based on an expression
```

---

## Q14. What is the ternary operator?

**Answer:**

```text
condition ? true_value : false_value
```

It is a compact way of describing conditional selection.

---

## Q15. What hardware does this describe?

```verilog
assign y = sel ? b : a;
```

**Answer:** A 2:1 multiplexer.

---

## Q16. Can `case` be used in FSM design?

**Answer:** Yes. `case` is commonly used to describe state transitions and output logic in FSMs.

---

## Q17. Why are `begin` and `end` used?

**Answer:** They group multiple procedural statements into a single block controlled by an `if`, `else`, or case item.

---

## Q18. What happens if both conditions are true in an `if-else-if` chain?

**Answer:** The first true condition is executed.

---

# 🔥 Placement Rapid-Fire

**Single condition?**

→ `if`

**Two alternatives?**

→ `if-else`

**Multiple priority conditions?**

→ `if-else-if`

**Multiple value selections?**

→ `case`

**Unmatched case value?**

→ `default`

**Wildcard with Z/?**

→ `casez`

**Wildcard with X/Z?**

→ `casex`

**2:1 MUX using if?**

→ `if-else`

**4:1 MUX using case?**

→ `case`

**Priority logic?**

→ `if-else-if`

**FSM state selection?**

→ `case`

**Compact MUX?**

→ `?:`

**Missing combinational assignment?**

→ Possible latch

---

# 🧠 9.14 QUICK REVISION

```text
             CONDITIONAL CONSTRUCTS
                       │
       ┌───────────────┼───────────────┐
       ↓               ↓               ↓
      if             case             ?:
       │               │               │
   priority       multi-selection      MUX
```

### `if-else`

```verilog
if (sel)
    y = b;
else
    y = a;
```

→ 2:1 MUX

### `case`

```verilog
case (sel)
    2'b00: y = a;
    2'b01: y = b;
    2'b10: y = c;
    2'b11: y = d;
endcase
```

→ 4:1 MUX

### Ternary

```verilog
assign y = sel ? b : a;
```

→ 2:1 MUX

### Priority

```verilog
if (a)
    y = 1;
else if (b)
    y = 2;
```

→ `a` has priority over `b`.

### ⭐ Golden Rules

```text
if-else-if → priority
case → multi-way selection
default → handle unmatched cases
Incomplete combinational assignment → possible latch
```
