# 🚀 9.22 — COMBINATIONAL & SEQUENTIAL RTL CODING STYLES

## ⭐⭐⭐⭐⭐ Placement Important

This topic is **very important for VLSI placements** because interviewers frequently ask how to identify, code, and differentiate **combinational logic and sequential logic** in Verilog.

---

# 1. What is RTL Coding?

**RTL (Register Transfer Level)** describes:

* How data moves between registers
* What combinational logic operates on that data
* When registers capture data

A simplified RTL structure is:

```text
Input
  ↓
Combinational Logic
  ↓
Register
  ↓
Combinational Logic
  ↓
Register
  ↓
Output
```

---

# 2. Two Major RTL Coding Styles

RTL logic is broadly classified into:

```text
1. Combinational RTL
2. Sequential RTL
```

---

# 3. What is Combinational Logic?

In combinational logic, the output depends **only on the current inputs**.

```text
Output = f(Current Inputs)
```

There is no memory of previous inputs.

Examples:

* AND gate
* OR gate
* MUX
* Decoder
* Encoder
* Adder
* Comparator
* ALU

---

# 4. Combinational Logic Example

```verilog
always @(*) begin
    y = a & b;
end
```

Here:

```text
a, b → current inputs
y    → current output
```

There is no clock.

---

# 5. Continuous Assignment for Combinational Logic

Simple combinational logic can be written using:

```verilog
assign y = a & b;
```

This is also combinational logic.

---

# 6. Combinational `always` Block ⭐⭐⭐⭐⭐

The traditional Verilog style is:

```verilog
always @(*) begin

    // combinational logic

end
```

The `*` means the simulator automatically includes signals read inside the block in the sensitivity list.

Example:

```verilog
always @(*) begin
    y = a & b;
end
```

---

# 7. Why Use `always @(*)`?

Consider:

```verilog
always @(a or b or c or d)
```

You must manually list every signal that affects the block.

Instead:

```verilog
always @(*)
```

automatically includes the relevant signals.

This reduces sensitivity-list mistakes.

---

# 8. Combinational MUX Example

```verilog
always @(*) begin

    case (sel)

        2'b00: y = a;
        2'b01: y = b;
        2'b10: y = c;
        2'b11: y = d;

        default: y = 0;

    endcase

end
```

This describes a:

```text
4:1 MUX
```

---

# 9. Combinational ALU Example

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

No clock is required.

---

# 10. Important Rule for Combinational Logic ⭐⭐⭐⭐⭐

Every output must receive an assignment for **all possible conditions**.

Otherwise, the synthesis tool may infer a:

```text
Latch
```

Example of problematic code:

```verilog
always @(*) begin

    if (enable)
        y = a;

end
```

What happens when:

```text
enable = 0
```

There is no assignment to `y`.

Therefore the tool may infer storage.

---

# 11. Safe Combinational Coding Style

A common approach is to assign default values first:

```verilog
always @(*) begin

    y = 0;

    if (enable)
        y = a;

end
```

Now `y` always receives a value.

---

# 12. Another Safe Method — `else`

```verilog
always @(*) begin

    if (enable)
        y = a;
    else
        y = 0;

end
```

Both branches assign `y`.

---

# 13. What is Sequential Logic?

Sequential logic depends on:

* Current inputs
* Previous state

Therefore:

```text
Output = f(Current Inputs, Previous State)
```

Sequential logic contains **memory/storage**.

Examples:

* Flip-flops
* Registers
* Counters
* Shift registers
* FSMs
* Memories

---

# 14. Clock in Sequential Logic ⭐⭐⭐⭐⭐

Sequential logic is commonly controlled by a clock.

Example:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

This describes a flip-flop.

At every rising edge:

```text
d → q
```

---

# 15. Why Use `posedge`?

```text
posedge clk
```

means:

> Execute the sequential block when the clock changes from 0 to 1.

This is called the:

```text
Positive/rising edge
```

---

# 16. Negative-Edge Sequential Logic

You can also use:

```verilog
always @(negedge clk) begin
    q <= d;
end
```

This triggers when:

```text
1 → 0
```

This is the:

```text
Falling/negative edge
```

---

# 17. Sequential Logic Uses Nonblocking Assignment ⭐⭐⭐⭐⭐

Typical sequential RTL:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

Notice:

```text
<=
```

This is the **nonblocking assignment** operator.

It is normally preferred for clocked sequential logic.

---

# 18. Why Use Nonblocking Assignment?

Consider:

```verilog
always @(posedge clk) begin

    q1 <= d;
    q2 <= q1;

end
```

At the same clock edge:

```text
q1 gets old d
q2 gets old q1
```

This correctly models flip-flop behavior.

---

# 19. Example — Two Flip-Flops

```verilog
always @(posedge clk) begin

    q1 <= d;
    q2 <= q1;

end
```

Hardware:

```text
        ┌─────┐       ┌─────┐
d ─────►│ FF1 │──────►│ FF2 │────► q2
        └─────┘       └─────┘
           ↑             ↑
           └──── clk ────┘
```

This represents two sequential storage elements.

---

# 20. Combinational vs Sequential RTL ⭐⭐⭐⭐⭐

| Feature           | Combinational     | Sequential                      |
| ----------------- | ----------------- | ------------------------------- |
| Memory            | ❌                 | ✅                               |
| Depends on        | Current inputs    | Current inputs + previous state |
| Clock             | Usually ❌         | Usually ✅                       |
| Typical block     | `always @(*)`     | `always @(posedge clk)`         |
| Assignment        | Usually `=`       | Usually `<=`                    |
| Examples          | MUX, ALU, decoder | FF, counter, FSM                |
| Latch possibility | If incomplete     | Intentional storage may exist   |

---

# 21. Golden Coding Rule

Remember:

```text
COMBINATIONAL
     ↓
always @(*)
     ↓
blocking =
```

and:

```text
SEQUENTIAL
     ↓
always @(posedge clk)
     ↓
nonblocking <=
```

This is one of the most important interview rules.

---

# 22. Combinational Logic with Blocking Assignment

Example:

```verilog
always @(*) begin

    temp = a + b;
    y = temp & c;

end
```

Blocking assignment:

```text
=
```

allows the statements to execute sequentially in the procedural description.

---

# 23. Sequential Logic with Nonblocking Assignment

Example:

```verilog
always @(posedge clk) begin

    q1 <= d;
    q2 <= q1;

end
```

This models simultaneous state updates.

---

# 24. Can Blocking Assignment Be Used in Sequential Logic?

Technically, Verilog allows it.

Example:

```verilog
always @(posedge clk) begin
    q = d;
end
```

But for synthesizable clocked RTL, **nonblocking assignment is the standard recommended style**.

Use:

```verilog
q <= d;
```

---

# 25. Can Nonblocking Assignment Be Used in Combinational Logic?

It can be syntactically valid in some situations, but it is generally **not the recommended style** for combinational RTL.

Prefer:

```verilog
always @(*) begin
    y = a & b;
end
```

rather than:

```verilog
always @(*) begin
    y <= a & b;
end
```

---

# 26. Why Mixing `=` and `<=` Can Be Dangerous

Example:

```verilog
always @(posedge clk) begin

    q1 <= d;
    q2 = q1;

end
```

Mixing assignment types can produce confusing simulation behavior and make RTL harder to understand.

For clean RTL:

```text
Combinational → =
Sequential   → <=
```

---

# 27. Combinational Next-State Logic in FSM

FSMs commonly use two different types of logic.

### Next-state combinational logic

```verilog
always @(*) begin

    case (state)

        IDLE: next_state = RUN;
        RUN:  next_state = DONE;
        DONE: next_state = IDLE;

        default: next_state = IDLE;

    endcase

end
```

### State register

```verilog
always @(posedge clk) begin
    state <= next_state;
end
```

This is a very important RTL structure.

---

# 28. FSM RTL Structure ⭐⭐⭐⭐⭐

```text
             ┌────────────────────┐
             │ Combinational Logic │
             │   Next-State Logic  │
             └─────────┬──────────┘
                       │
                       ▼
                 ┌──────────┐
                 │ Register │
                 │  State   │
                 └────┬─────┘
                      │
                      ▼
                Current State
                      │
                      └──────────► Combinational Logic
```

---

# 29. Three-Block FSM Coding Style

A common FSM implementation uses:

### Block 1 — State register

```verilog
always @(posedge clk) begin
    state <= next_state;
end
```

### Block 2 — Next-state logic

```verilog
always @(*) begin

    case (state)

        ...

    endcase

end
```

### Block 3 — Output logic

```verilog
always @(*) begin

    case (state)

        ...

    endcase

end
```

This is called a:

```text
Three-process / three-block FSM style
```

---

# 30. Two-Block FSM Style

Another common style uses:

### Block 1

State register:

```verilog
always @(posedge clk) begin
    state <= next_state;
end
```

### Block 2

Next-state + output logic:

```verilog
always @(*) begin
    ...
end
```

This is called:

```text
Two-process FSM style
```

---

# 31. One-Block FSM Style

An FSM can also be coded in one sequential block:

```verilog
always @(posedge clk) begin

    case (state)

        IDLE: begin
            ...
        end

        RUN: begin
            ...
        end

        DONE: begin
            ...
        end

    endcase

end
```

This is:

```text
One-process FSM style
```

---

# 32. Combinational vs Sequential Sensitivity

### Combinational:

```verilog
always @(*)
```

### Positive-edge sequential:

```verilog
always @(posedge clk)
```

### Negative-edge sequential:

```verilog
always @(negedge clk)
```

### Flip-flop with asynchronous reset:

```verilog
always @(posedge clk or posedge reset)
```

---

# 33. Asynchronous Reset Example

```verilog
always @(posedge clk or posedge reset) begin

    if (reset)
        q <= 0;
    else
        q <= d;

end
```

Here:

```text
posedge clk → normal operation
posedge reset → immediate reset
```

The reset does not wait for the clock edge.

---

# 34. Synchronous Reset Example

```verilog
always @(posedge clk) begin

    if (reset)
        q <= 0;
    else
        q <= d;

end
```

Here reset is checked only at:

```text
clock edge
```

---

# 35. Important Difference

### Asynchronous reset

```verilog
always @(posedge clk or posedge reset)
```

Reset is in the sensitivity list.

### Synchronous reset

```verilog
always @(posedge clk)
```

Reset is checked inside the clocked block.

---

# 36. Combinational RTL Checklist

When writing combinational RTL:

```text
✓ Use always @(*)
✓ Use blocking assignment =
✓ Assign every output in every condition
✓ Use default assignments where useful
✓ Avoid unintended latches
```

---

# 37. Sequential RTL Checklist

When writing sequential RTL:

```text
✓ Use clock edge
✓ Use nonblocking assignment <=
✓ Define reset behavior when required
✓ Maintain proper state/register behavior
✓ Avoid multiple drivers
```

---

# ⭐ Frequently Asked Placement Questions

## Q1. What is combinational logic?

**Answer:** Logic whose output depends only on the current inputs.

---

## Q2. What is sequential logic?

**Answer:** Logic whose output/state depends on current inputs and stored previous state.

---

## Q3. Give examples of combinational circuits.

**Answer:**

* MUX
* Decoder
* Encoder
* Adder
* Comparator
* ALU

---

## Q4. Give examples of sequential circuits.

**Answer:**

* Flip-flop
* Register
* Counter
* Shift register
* FSM
* Memory

---

## Q5. Which assignment is preferred for combinational logic?

**Answer:**

```text
Blocking assignment =
```

---

## Q6. Which assignment is preferred for sequential logic?

**Answer:**

```text
Nonblocking assignment <=
```

---

## Q7. Why is nonblocking assignment preferred for sequential logic?

**Answer:** It models simultaneous updates of clocked storage elements and prevents ordering-dependent behavior between registers.

---

## Q8. What is the standard combinational block?

**Answer:**

```verilog
always @(*) begin
    ...
end
```

---

## Q9. What is the standard sequential block?

**Answer:**

```verilog
always @(posedge clk) begin
    ...
end
```

---

## Q10. What happens if a combinational output isn't assigned in every condition?

**Answer:** An unintended latch may be inferred.

---

## Q11. How can you prevent latch inference?

**Answer:**

* Assign default values
* Ensure every `if` has appropriate `else`
* Ensure every `case` has appropriate coverage/default

---

## Q12. What is the difference between synchronous and asynchronous reset?

**Answer:**

```text
Synchronous reset
→ reset takes effect at the active clock edge
```

```text
Asynchronous reset
→ reset can take effect independently of the clock
```

---

## Q13. What is a three-block FSM?

**Answer:** An FSM implementation with separate blocks for:

1. State register
2. Next-state logic
3. Output logic

---

## Q14. What is a two-block FSM?

**Answer:** One block contains the state register and another contains next-state/output combinational logic.

---

## Q15. What is a one-block FSM?

**Answer:** State, transitions, and outputs are implemented in a single sequential block.

---

## Q16. Can combinational logic have a clock?

**Answer:** A purely combinational block does not require a clock.

---

## Q17. Does sequential logic always require a clock?

**Answer:** Most synchronous sequential logic uses a clock, although sequential/storage behavior can also involve asynchronous controls.

---

# 🔥 Placement Rapid-Fire

**Current inputs only?**

→ Combinational

**Current + previous state?**

→ Sequential

**Combinational block?**

→ `always @(*)`

**Sequential block?**

→ `always @(posedge clk)`

**Combinational assignment?**

→ `=`

**Sequential assignment?**

→ `<=`

**MUX?**

→ Combinational

**Counter?**

→ Sequential

**Register?**

→ Sequential

**Adder?**

→ Combinational

**FSM?**

→ Sequential + combinational logic

**Incomplete combinational assignment?**

→ Possible latch

**Asynchronous reset?**

→ Reset included in sensitivity list

**Synchronous reset?**

→ Reset checked inside clocked block

---

# 🧠 9.22 QUICK REVISION

```text
             RTL CODING
                  │
        ┌─────────┴─────────┐
        ↓                   ↓
 COMBINATIONAL          SEQUENTIAL
        │                   │
 Current inputs       Current + state
        │                   │
 always @(*)          posedge/negedge
        │                   │
      =                    <=
        │                   │
 MUX, ALU, Decoder    FF, Register,
 Adder, Comparator    Counter, FSM
```

### ⭐ Golden Rules

```text
Combinational → always @(*) + =
Sequential → clocked block + <=
Incomplete combinational assignment → possible latch
FSM = combinational next-state logic + sequential state register
```
