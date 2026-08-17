# PROCEDURAL BLOCKS: `always` & `initial` ⭐⭐⭐⭐⭐

Procedural blocks are a **very important Verilog topic for VLSI placements**.

The two main procedural blocks are:

```verilog
always
initial
```

They are used in **behavioral modeling** and are especially important for understanding combinational logic, sequential logic, testbenches, and simulation.

---

# 1. What is a Procedural Block?

A procedural block contains statements that execute according to a specified procedure or event.

The two main types are:

```verilog
always
initial
```

---

# 2. `always` Block

The `always` block executes repeatedly.

Basic syntax:

```verilog
always @(event) begin
    statements;
end
```

Example:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

This means:

> Whenever a positive edge of `clk` occurs, execute the statements inside the block.

---

# 3. Why is it Called `always`?

Because the block keeps waiting for its triggering event and executes again whenever that event occurs.

Conceptually:

```text
        ┌──────────────┐
        │  Wait for    │
        │    event     │
        └──────┬───────┘
               ↓
          Execute block
               ↓
        ┌──────┴───────┐
        │  Wait again  │
        └──────────────┘
```

---

# 4. `initial` Block

The `initial` block executes **once**, starting at the beginning of simulation.

Syntax:

```verilog
initial begin
    statements;
end
```

Example:

```verilog
initial begin
    a = 0;
    b = 0;
end
```

It executes once and then terminates.

---

# 5. `always` vs `initial` ⭐⭐⭐⭐⭐

| `always`                      | `initial`                         |
| ----------------------------- | --------------------------------- |
| Repeats                       | Executes once                     |
| Waits for events              | Starts at simulation time 0       |
| Common for RTL behavior       | Commonly used in testbenches      |
| Can model combinational logic | Mainly simulation/testbench usage |
| Can model sequential logic    | Used for initialization/stimulus  |

### Memory trick

```text
always  → again and again
initial → once at the beginning
```

---

# 6. `always` with Sensitivity List

Example:

```verilog
always @(a or b) begin
    y = a & b;
end
```

The block executes whenever:

```text
a changes
OR
b changes
```

---

# 7. `always @(*)` ⭐⭐⭐⭐⭐

For combinational logic, a common style is:

```verilog
always @(*) begin
    y = a & b;
end
```

`@(*)` tells the simulator to automatically include signals read by the block in its sensitivity list.

This avoids manually writing:

```verilog
always @(a or b)
```

---

# 8. Why Use `always @(*)`?

Suppose:

```verilog
always @(a or b or c or d) begin
    y = (a & b) | (c & d);
end
```

If you forget one input:

```verilog
always @(a or b or c) begin
    y = (a & b) | (c & d);
end
```

simulation can behave incorrectly because changes in `d` won't trigger the block.

Using:

```verilog
always @(*) begin
    y = (a & b) | (c & d);
end
```

avoids this manual sensitivity-list mistake.

---

# 9. `always @(posedge clk)` ⭐⭐⭐⭐⭐

This is commonly used for sequential logic.

Example:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

The block executes when:

```text
0 → 1
```

transition occurs on `clk`.

This is called a **positive edge** or **rising edge**.

---

# 10. `always @(negedge clk)`

Example:

```verilog
always @(negedge clk) begin
    q <= d;
end
```

The block executes on:

```text
1 → 0
```

transition.

This is called a **negative edge** or **falling edge**.

---

# 11. Positive vs Negative Edge

```text
Positive edge:

0 ──────┐
        └──── 1


Negative edge:

1 ──────┐
        └──── 0
```

Memory:

```text
posedge → 0 → 1
negedge → 1 → 0
```

---

# 12. `always` for Combinational Logic

Example:

```verilog
always @(*) begin
    y = a & b;
end
```

This describes combinational logic.

Equivalent dataflow:

```verilog
assign y = a & b;
```

---

# 13. `always` for Sequential Logic

Example:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

This describes clocked storage behavior.

Conceptually:

```text
       ┌─────────┐
D ────→│   D FF  │────→ Q
CLK ──→│         │
       └─────────┘
```

---

# 14. Same `always` Keyword, Different Hardware

This is important.

### Combinational

```verilog
always @(*) begin
    y = a & b;
end
```

→ Combinational logic

### Sequential

```verilog
always @(posedge clk) begin
    q <= d;
end
```

→ Sequential logic / flip-flop

So the hardware depends on **how the procedural block is written**.

---

# 15. Sensitivity List ⭐⭐⭐⭐⭐

A sensitivity list specifies events that cause an `always` block to execute.

Example:

```verilog
always @(a or b) begin
    y = a & b;
end
```

The block executes when:

```text
a changes
OR
b changes
```

---

# 16. Multiple Events

You can specify multiple events.

Example:

```verilog
always @(posedge clk or posedge reset) begin
    ...
end
```

The block executes when either:

```text
posedge clk
```

or:

```text
posedge reset
```

occurs.

This is commonly used for an **asynchronous reset**.

---

# 17. Asynchronous Reset Example ⭐⭐⭐⭐⭐

```verilog
always @(posedge clk or posedge reset) begin
    if (reset)
        q <= 1'b0;
    else
        q <= d;
end
```

Here:

```text
reset → asynchronous
clk   → clock
```

The reset can affect `q` without waiting for a clock edge.

---

# 18. Synchronous Reset

Example:

```verilog
always @(posedge clk) begin
    if (reset)
        q <= 1'b0;
    else
        q <= d;
end
```

Here reset is checked only on:

```text
posedge clk
```

Therefore it is a **synchronous reset**.

---

# 19. Synchronous vs Asynchronous Reset

| Synchronous Reset               | Asynchronous Reset                            |
| ------------------------------- | --------------------------------------------- |
| Reset checked on clock edge     | Reset can act independently of clock          |
| Sensitivity list contains clock | Sensitivity list contains clock + reset event |
| Example: `@(posedge clk)`       | Example: `@(posedge clk or posedge reset)`    |

### Memory trick

```text
Synchronous reset
→ waits for clock

Asynchronous reset
→ does not wait for clock
```

---

# 20. `initial` Example

```verilog
initial begin
    reset = 1;
    #10 reset = 0;
end
```

At simulation start:

```text
reset = 1
```

After 10 time units:

```text
reset = 0
```

This is commonly used in a testbench.

---

# 21. Delays in `initial`

Example:

```verilog
initial begin
    a = 0;
    #10 a = 1;
    #10 a = 0;
end
```

Timeline:

```text
t = 0   → a = 0
t = 10  → a = 1
t = 20  → a = 0
```

---

# 22. `initial` for Testbench Stimulus

Example:

```verilog
initial begin
    a = 0;
    b = 0;

    #10 a = 1;
    #10 b = 1;

    #10 $finish;
end
```

This generates input stimulus for simulation.

---

# 23. Can `initial` Be Synthesized?

For traditional RTL placement knowledge:

> `initial` is primarily associated with simulation and testbenches.

Some FPGA tools support synthesis of certain `initial` constructs for initialization, but for ASIC-oriented RTL interviews, do not treat `initial` as the normal way to describe synthesizable sequential hardware.

---

# 24. Can `always` Be Synthesized?

**Yes.**

For example:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

can synthesize to a flip-flop.

And:

```verilog
always @(*) begin
    y = a & b;
end
```

can synthesize to combinational logic.

---

# 25. `always` and Blocking Assignment

Combinational logic commonly uses:

```verilog
=
```

Example:

```verilog
always @(*) begin
    y = a & b;
end
```

This is called a **blocking assignment**.

---

# 26. `always` and Nonblocking Assignment

Sequential logic commonly uses:

```verilog
<=
```

Example:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

This is called a **nonblocking assignment**.

### Important placement rule

```text
Combinational → generally =
Sequential    → generally <=
```

---

# 27. Why Nonblocking for Sequential Logic?

Consider:

```verilog
always @(posedge clk) begin
    q1 <= d;
    q2 <= q1;
end
```

Both updates occur based on the values that existed before the clock event.

This correctly models flip-flop behavior.

---

# 28. Blocking vs Nonblocking ⭐⭐⭐⭐⭐

| Blocking `=`                             | Nonblocking `<=`                     |
| ---------------------------------------- | ------------------------------------ |
| Executes immediately in procedural order | Updates are scheduled                |
| Common for combinational logic           | Common for sequential logic          |
| Statement order matters                  | Models simultaneous register updates |
| Example: `y = a & b`                     | Example: `q <= d`                    |

---

# 29. Important Example

```verilog
always @(posedge clk) begin
    q1 <= d;
    q2 <= q1;
end
```

Suppose initially:

```text
q1 = 0
q2 = 0
d  = 1
```

After the clock:

```text
q1 = 1
q2 = 0
```

On the next clock:

```text
q1 = 1
q2 = 1
```

This models a two-stage register pipeline.

---

# 30. Combinational Example

```verilog
always @(*) begin
    if (sel)
        y = b;
    else
        y = a;
end
```

This describes a 2:1 MUX.

Equivalent:

```verilog
assign y = sel ? b : a;
```

---

# 31. Incomplete Assignment and Latch ⭐⭐⭐⭐⭐

Consider:

```verilog
always @(*) begin
    if (en)
        y = a;
end
```

What happens when:

```text
en = 0
```

There is no assignment to `y`.

The previous value of `y` must be retained.

This can infer a **latch**.

---

# 32. Avoiding Unwanted Latches

Give `y` a default assignment.

```verilog
always @(*) begin
    y = 0;

    if (en)
        y = a;
end
```

Now `y` receives a value for every condition.

Therefore no latch is inferred from this logic.

---

# 33. `always @(*)` and Latch Prevention

Remember:

```verilog
always @(*)
```

automatically handles sensitivity.

But it **does not automatically prevent latches**.

You must ensure that all outputs are assigned in every possible path for combinational logic.

---

# 34. `always` Block Rules

For placement preparation:

### Combinational

```verilog
always @(*) begin
    ...
end
```

Usually:

```text
blocking =
```

### Sequential

```verilog
always @(posedge clk) begin
    ...
end
```

Usually:

```text
nonblocking <=
```

---

# 35. `always` Block Cannot Execute in Parallel Internally?

The statements **inside one procedural block execute sequentially in simulation order**.

Example:

```verilog
always @(*) begin
    a = b;
    c = a;
end
```

The first statement executes before the second.

However, separate `always` blocks can execute concurrently as independent processes.

---

# 36. Multiple `always` Blocks

Example:

```verilog
always @(posedge clk)
    q1 <= d1;

always @(posedge clk)
    q2 <= d2;
```

Both blocks respond to the clock event independently.

This is useful for describing separate pieces of hardware.

---

# 37. Parallel Nature of Hardware

Although procedural statements inside a block execute in order during simulation, the synthesized hardware operates concurrently.

For example:

```verilog
always @(posedge clk)
    q1 <= d1;

always @(posedge clk)
    q2 <= d2;
```

represents two flip-flops operating in parallel.

---

# 38. Common Mistake

### Incorrect combinational style:

```verilog
always @(a) begin
    y = a & b;
end
```

If `b` changes, the block doesn't execute.

Better:

```verilog
always @(*) begin
    y = a & b;
end
```

---

# 39. Common Sequential Style

```verilog
always @(posedge clk) begin
    q <= d;
end
```

This is the standard pattern for a positive-edge-triggered flip-flop.

---

# 40. Common Asynchronous Reset Style

```verilog
always @(posedge clk or posedge reset) begin
    if (reset)
        q <= 1'b0;
    else
        q <= d;
end
```

Very important for interviews.

---

# ⭐ Frequently Asked Placement Questions

## Q1. What are the two main procedural blocks in Verilog?

**Answer:**

```verilog
always
initial
```

---

## Q2. What is the difference between `always` and `initial`?

**Answer:**

```text
always  → repeatedly executes based on events
initial → executes once at simulation start
```

---

## Q3. What is a sensitivity list?

**Answer:** A sensitivity list specifies the event or signals that trigger execution of an `always` block.

Example:

```verilog
always @(posedge clk)
```

---

## Q4. What does `posedge` mean?

**Answer:**

```text
0 → 1
```

transition.

---

## Q5. What does `negedge` mean?

**Answer:**

```text
1 → 0
```

transition.

---

## Q6. What is `always @(*)`?

**Answer:** It is an `always` block whose sensitivity list automatically includes signals referenced in the block, commonly used for combinational logic.

---

## Q7. Which block is commonly used for combinational logic?

**Answer:**

```verilog
always @(*)
```

---

## Q8. Which block is commonly used for sequential logic?

**Answer:**

```verilog
always @(posedge clk)
```

or another clock-edge-based procedural block.

---

## Q9. Which assignment is generally used for combinational logic?

**Answer:**

```verilog
blocking assignment `=`
```

---

## Q10. Which assignment is generally used for sequential logic?

**Answer:**

```verilog
nonblocking assignment `<=`
```

---

## Q11. What happens if a combinational `always` block does not assign an output in every path?

**Answer:** It can infer a **latch**.

---

## Q12. How can unwanted latches be avoided?

**Answer:** Ensure every output gets an assignment for every possible input/control condition, often by providing a default assignment.

---

## Q13. Can `always` describe both combinational and sequential logic?

**Answer:** **Yes.**

```verilog
always @(*)           → combinational
always @(posedge clk) → sequential
```

---

## Q14. Can `initial` describe normal ASIC sequential hardware?

**Answer:** `initial` is primarily used for simulation/testbench purposes in traditional ASIC RTL.

---

## Q15. Can `always` be synthesized?

**Answer:** Yes, when written using synthesizable constructs.

---

## Q16. What is the difference between synchronous and asynchronous reset?

**Answer:**

```text
Synchronous → reset checked on clock edge
Asynchronous → reset can act independently of clock
```

---

## Q17. How do you write an asynchronous reset?

```verilog
always @(posedge clk or posedge reset)
```

---

## Q18. How do you write a synchronous reset?

```verilog
always @(posedge clk)
```

with reset checked inside the block.

---

## Q19. What hardware does this code represent?

```verilog
always @(posedge clk)
    q <= d;
```

**Answer:** A positive-edge-triggered D flip-flop.

---

## Q20. What hardware can this code represent?

```verilog
always @(*) begin
    if (sel)
        y = b;
    else
        y = a;
end
```

**Answer:** A 2:1 multiplexer.

---

# 🔥 Placement Rapid-Fire

**Repeated procedural block?**

→ `always`

**One-time procedural block?**

→ `initial`

**Combinational sensitivity?**

→ `@(*)`

**Positive edge?**

→ `posedge`

**Negative edge?**

→ `negedge`

**Combinational assignment?**

→ `=`

**Sequential assignment?**

→ `<=`

**Flip-flop template?**

→ `always @(posedge clk)`

**Asynchronous reset?**

→ `posedge clk or posedge reset`

**Synchronous reset?**

→ reset checked inside `@(posedge clk)`

**Incomplete combinational assignment?**

→ Can infer latch

**`always` can model both?**

→ Yes, combinational and sequential logic

---

# 🧠 QUICK REVISION

```text
              PROCEDURAL BLOCKS
                     │
          ┌──────────┴──────────┐
          ↓                     ↓
       always                initial
          │                     │
     repeated                 once
          │                     │
    ┌─────┴─────┐         simulation
    ↓           ↓          /testbench
combinational sequential
```

### Combinational

```verilog
always @(*) begin
    y = a & b;
end
```

### Sequential

```verilog
always @(posedge clk) begin
    q <= d;
end
```

### Synchronous reset

```verilog
always @(posedge clk) begin
    if (reset)
        q <= 0;
    else
        q <= d;
end
```

### Asynchronous reset

```verilog
always @(posedge clk or posedge reset) begin
    if (reset)
        q <= 0;
    else
        q <= d;
end
```

### Testbench stimulus

```verilog
initial begin
    reset = 1;
    #10 reset = 0;
end
```

---

# ⭐ MOST IMPORTANT RULES

```text
always @(*)           → Combinational
always @(posedge clk) → Sequential

=  → generally combinational
<= → generally sequential

initial → mainly simulation/testbench

Incomplete combinational assignment
→ possible latch
```
