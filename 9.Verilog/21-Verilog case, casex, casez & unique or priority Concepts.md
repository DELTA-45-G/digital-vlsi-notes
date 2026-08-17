# `case`, `casex`, `casez` & `unique/priority`

## ⭐⭐⭐⭐⭐ Placement Important

The `case` statement is widely used in Verilog for **multi-way decision making**, especially in:

* Multiplexers
* ALUs
* FSMs
* Decoders
* Control logic

The important variants are:

```verilog
case
```

```verilog
casez
```

```verilog
casex
```

and in SystemVerilog:

```verilog
unique
```

```verilog
priority
```

---

# 1. What is a `case` Statement?

A `case` statement compares an expression against multiple possible values.

Syntax:

```verilog
case (expression)

value1: statement;
value2: statement;
value3: statement;

default: statement;

endcase
```

Example:

```verilog
always @(*) begin

    case (sel)

        2'b00: y = a;
        2'b01: y = b;
        2'b10: y = c;
        2'b11: y = d;

    endcase

end
```

This describes a:

```text
4:1 Multiplexer
```

---

# 2. Why Use `case`?

`case` is useful when there are multiple possible conditions.

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

This is often clearer for:

* FSMs
* Decoders
* MUXes
* Control logic

---

# 3. `default` Case ⭐⭐⭐⭐⭐

A `default` branch handles values that don't match the listed cases.

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

The `default` is especially important in combinational logic because it helps ensure the output receives an assignment for all possible conditions.

---

# 4. Why Is `default` Important?

Suppose:

```verilog
always @(*) begin

    case (sel)

        2'b00: y = a;
        2'b01: y = b;

    endcase

end
```

What happens when:

```text
sel = 2'b10
```

or:

```text
sel = 2'b11
```

No assignment occurs.

The previous value of `y` may need to be retained, potentially causing **latch inference**.

Better:

```verilog
always @(*) begin

    y = 0;

    case (sel)

        2'b00: y = a;
        2'b01: y = b;

    endcase

end
```

or use an appropriate `default`.

---

# 5. `case` Uses Exact Matching

Traditional Verilog `case` uses **case equality** semantics for matching.

That means:

```text
0 → matches 0
1 → matches 1
x → matches x
z → matches z
```

This is different from ordinary logical equality.

Example:

```verilog
case (sel)

    2'b1x: ...

endcase
```

The `x` is treated as an actual `x` value for matching.

---

# 6. `case` vs `if`

| `case`                            | `if`                              |
| --------------------------------- | --------------------------------- |
| Multiple discrete choices         | Conditions evaluated sequentially |
| Good for FSMs                     | Good for ranges/conditions        |
| Good for decoders                 | Good for comparisons              |
| Can have `default`                | Uses `else`                       |
| Matches expression against values | Evaluates Boolean conditions      |

---

# 7. Example — Decoder Using `case`

```verilog
always @(*) begin

    case (sel)

        2'b00: y = 4'b0001;
        2'b01: y = 4'b0010;
        2'b10: y = 4'b0100;
        2'b11: y = 4'b1000;

        default: y = 4'b0000;

    endcase

end
```

This describes a decoder.

---

# 8. Example — ALU Using `case`

```verilog
always @(*) begin

    case (op)

        2'b00: result = a + b;
        2'b01: result = a - b;
        2'b10: result = a & b;
        2'b11: result = a | b;

        default: result = 0;

    endcase

end
```

This is a common RTL coding style for an ALU.

---

# 9. `casez`

`casez` treats:

```text
z
```

```text
?
```

as don't-care bits for matching.

Example:

```verilog
casez (opcode)

    4'b1???: instruction = 1;
    4'b01??: instruction = 2;
    4'b001?: instruction = 3;

endcase
```

---

# 10. Why Use `casez`?

`casez` is particularly useful for:

* Priority encoders
* Pattern matching
* Decoder logic
* Address decoding

Example:

```verilog
casez (request)

    4'b1???: grant = 4'b1000;
    4'b01??: grant = 4'b0100;
    4'b001?: grant = 4'b0010;
    4'b0001: grant = 4'b0001;

endcase
```

---

# 11. What Does `?` Mean?

In `casez`, `?` represents a don't-care position.

Example:

```verilog
4'b1???
```

means:

```text
MSB must be 1
```

remaining three bits don't matter

So all of these can match:

```text
1000
1001
1010
1011
1100
1101
1110
1111
```

---

# 12. `casex`

`casex` treats:

```text
x
z
?
```

as don't-care values during matching.

Example:

```verilog
casex (sel)

    4'b1xxx: y = a;
    4'b01xx: y = b;
    4'b001x: y = c;

endcase
```

---

# 13. `casez` vs `casex` ⭐⭐⭐⭐⭐

| `casez`                          | `casex`                                |
| -------------------------------- | -------------------------------------- |
| Treats `z` and `?` as don't-care | Treats `x`, `z`, and `?` as don't-care |
| Safer for unknown `x` detection  | Can hide unknown values                |
| Commonly preferred over `casex`  | Generally discouraged in RTL           |

### Important placement point:

**Avoid `casex` in synthesizable RTL when possible**, because it can hide unknown (`X`) conditions and make debugging difficult.

---

# 14. Why Can `casex` Be Dangerous?

Suppose a signal unexpectedly becomes:

```text
1'bx
```

With `casex`, the `x` may be treated as a don't-care.

Therefore the simulation may select a case that hides the underlying problem.

This can make:

```text
Simulation
```

look correct while masking an RTL/design issue.

---

# 15. `casez` Is Generally Safer

`casez` only treats `z` and `?` as don't-care, rather than treating `x` as don't-care.

Therefore unknown `x` values can remain visible during simulation.

---

# 16. What is Priority in `case`?

Normally, if multiple patterns can match, the behavior depends on the case construct and matching conditions.

For ordinary `case`, each case item is compared, and a matching item is selected.

When designing logic where **priority matters**, SystemVerilog provides:

```verilog
priority case
```

---

# 17. `priority case`

SystemVerilog:

```verilog
priority case (sel)

    2'b00: y = a;
    2'b01: y = b;
    2'b10: y = c;
    default: y = d;

endcase
```

The `priority` keyword indicates that the case items are intended to have priority semantics and enables tools to check for missing matches.

---

# 18. What is `unique case`?

SystemVerilog provides:

```verilog
unique case
```

It indicates that **at most one case item should match**.

Example:

```verilog
unique case (state)

    IDLE: ...
    LOAD: ...
    DONE: ...

endcase
```

Tools can warn if multiple or no items match when the coding implies uniqueness.

---

# 19. `unique` vs `priority` ⭐⭐⭐⭐⭐

### `unique`

Means:

> At most one case item should match.

### `priority`

Means:

> Case items are intended to have priority, and an earlier matching condition takes precedence in the appropriate construct.

Memory:

```text
unique   → one match
priority → priority order
```

---

# 20. `case`, `casez`, `casex`

Easy memory:

```text
case
 ↓
exact matching
```

```text
casez
 ↓
z / ? don't-care
```

```text
casex
 ↓
x / z / ? don't-care
```

---

# 21. Priority Encoder Example

Suppose:

```text
request[3:0]
```

and the highest-priority request should win.

A `casez` can be used:

```verilog
always @(*) begin

    casez (request)

        4'b1???: grant = 4'b1000;
        4'b01??: grant = 4'b0100;
        4'b001?: grant = 4'b0010;
        4'b0001: grant = 4'b0001;

        default: grant = 4'b0000;

    endcase

end
```

The first matching pattern represents the highest priority.

---

# 22. Case Statement in FSMs ⭐⭐⭐⭐⭐

A very common RTL pattern is:

```verilog
always @(*) begin

    case (state)

        IDLE: begin
            ...
        end

        LOAD: begin
            ...
        end

        EXEC: begin
            ...
        end

        DONE: begin
            ...
        end

        default: begin
            ...
        end

    endcase

end
```

This is frequently asked in VLSI interviews.

---

# 23. Case and Latch Inference

Consider:

```verilog
always @(*) begin

    case (sel)

        2'b00: y = a;
        2'b01: y = b;

    endcase

end
```

For:

```text
sel = 10
sel = 11
```

`y` isn't assigned.

This can infer a latch.

Better:

```verilog
always @(*) begin

    y = 0;

    case (sel)

        2'b00: y = a;
        2'b01: y = b;

    endcase

end
```

---

# 24. Case vs Casex vs Casez

| Feature                    | `case` | `casez`       | `casex`            |
| -------------------------- | ------ | ------------- | ------------------ |
| Exact matching             | ✅      | ❌             | ❌                  |
| `?` as don't-care          | ❌      | ✅             | ✅                  |
| `z` as don't-care          | ❌      | ✅             | ✅                  |
| `x` as don't-care          | ❌      | ❌             | ✅                  |
| Recommended for normal RTL | ✅      | ✅ when needed | ⚠️ Generally avoid |

---

# ⭐ Frequently Asked Placement Questions

## Q1. What is a `case` statement?

**Answer:** A `case` statement compares an expression against multiple possible values and executes the matching branch.

---

## Q2. Where is `case` commonly used?

**Answer:**

* FSMs
* ALUs
* Multiplexers
* Decoders
* Control logic

---

## Q3. What is `default` in a case statement?

**Answer:** It handles situations where none of the specified case items match.

---

## Q4. Why is `default` important in combinational logic?

**Answer:** It ensures outputs receive defined values for unmatched conditions and helps prevent unintended latch inference.

---

## Q5. What is `casez`?

**Answer:** `casez` is a case variant that treats `z` and `?` as don't-care values during matching.

---

## Q6. What is `casex`?

**Answer:** `casex` treats `x`, `z`, and `?` as don't-care values during matching.

---

## Q7. Which is safer: `casez` or `casex`?

**Answer:** `casez` is generally safer because it does not treat `x` as a don't-care.

---

## Q8. Why is `casex` generally discouraged?

**Answer:** It can hide unknown `X` values and mask design bugs during simulation.

---

## Q9. What is `unique case`?

**Answer:** `unique case` indicates that at most one case item is expected to match and enables additional tool checking.

---

## Q10. What is `priority case`?

**Answer:** `priority case` indicates that the case items have priority semantics and enables tools to check for missing matches.

---

## Q11. Difference between `unique` and `priority`?

**Answer:**

```text
unique   → one case item should match
priority → matching follows intended priority
```

---

## Q12. What is the difference between `case` and `if-else`?

**Answer:** `case` is convenient for matching one expression against multiple discrete values, while `if-else` is more suitable for general Boolean conditions and ranges.

---

## Q13. Can a case statement infer a latch?

**Answer:** Yes. If a combinational output is not assigned for every possible condition, latch inference can occur.

---

## Q14. How can you avoid latch inference in a case statement?

**Answer:**

* Provide a `default`
* Or provide default assignments before the case statement

Example:

```verilog
always @(*) begin

    y = 0;

    case (sel)
        ...
    endcase

end
```

---

## Q15. What does `?` mean in `casez`?

**Answer:** It represents a don't-care bit for matching.

---

# 🔥 Placement Rapid-Fire

**Multiple-choice RTL construct?**

→ `case`

**FSM state decoding?**

→ `case`

**Normal exact matching?**

→ `case`

**Wildcard with `z`/`?`?**

→ `casez`

**Wildcard with `x`/`z`/`?`?**

→ `casex`

**Generally avoid which one?**

→ `casex`

**Default branch?**

→ Handles unmatched cases

**Can missing case assignments infer latch?**

→ ✅ Yes

**`unique case`?**

→ At most one match expected

**`priority case`?**

→ Priority semantics

**`casez` safer than `casex`?**

→ ✅ Generally

**4:1 MUX using?**

→ `case`

**FSM using?**

→ `case`

**Priority encoder?**

→ `casez` can be useful

---

# 🧠 9.21 QUICK REVISION

```text
                 CASE STATEMENTS
                       │
          ┌────────────┼────────────┐
          ↓            ↓            ↓
        case         casez        casex
          │            │            │
       exact       z / ? don't   x / z / ?
       match          care          don't care
                                     │
                                  avoid when
                                possible in RTL
```

### Golden Rules

```text
case     → normal/exact matching
casez    → z, ? can be don't-care
casex    → x, z, ? can be don't-care
unique   → at most one match expected
priority → priority semantics
Always ensure complete assignments in combinational case logic
```
