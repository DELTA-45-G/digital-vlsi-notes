# LOOPS IN VERILOG

## `for`, `while`, `repeat`, and `forever` ⭐⭐⭐⭐⭐

Loops are used in Verilog to **repeat a set of statements** multiple times.

They are especially important for:

* RTL coding
* Testbenches
* Register arrays
* Memory initialization
* Generate structures
* Repetitive hardware descriptions

> ⚠️ **Important placement point:** A Verilog loop does **not automatically mean sequential hardware**. Depending on where and how the loop is used, synthesis can create **parallel hardware** rather than a software-style loop.

---

# 1. What is a Loop?

A loop repeatedly executes a block of statements according to a condition or count.

Common Verilog loops are:

```verilog
for
```

```verilog
while
```

```verilog
repeat
```

```verilog
forever
```

Memory trick:

```text
for     → known number of iterations
while   → condition-controlled
repeat  → fixed number of repetitions
forever → infinite repetition
```

---

# 2. `for` Loop ⭐⭐⭐⭐⭐

The `for` loop is the most commonly used loop in synthesizable Verilog.

Syntax:

```verilog
for (initialization; condition; increment)
```

```verilog
statement;
```

Example:

```verilog
integer i;

always @(*) begin
    for (i = 0; i < 4; i = i + 1)
        y[i] = a[i] & b[i];
end
```

The loop executes for:

```text
i = 0
i = 1
i = 2
i = 3
```

So the body executes **4 times**.

---

# 3. Structure of a `for` Loop

```verilog
for (i = 0; i < 4; i = i + 1)
```

has three parts:

### 1. Initialization

```verilog
i = 0
```

Executed first.

### 2. Condition

```verilog
i < 4
```

Checked before each iteration.

### 3. Increment

```verilog
i = i + 1
```

Executed after each iteration.

---

# 4. Example — Print Numbers

```verilog
integer i;

initial begin
    for (i = 0; i < 5; i = i + 1)
        $display("%d", i);
end
```

Output:

```text
0
1
2
3
4
```

---

# 5. How Many Times Does It Execute?

Question:

```verilog
for (i = 0; i < 10; i = i + 1)
```

How many iterations?

**Answer:**

```text
10 iterations
```

Values:

```text
0 → 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9
```

---

# 6. `for` Loop with Decrement

A `for` loop does not have to increment.

Example:

```verilog
for (i = 7; i >= 0; i = i - 1)
```

This iterates:

```text
7
6
5
4
3
2
1
0
```

Total:

```text
8 iterations
```

---

# 7. `for` Loop for Bit Operations

Example:

```verilog
integer i;

always @(*) begin
    for (i = 0; i < 8; i = i + 1)
        y[i] = a[i];
end
```

This copies:

```text
a[0] → y[0]
a[1] → y[1]
...
a[7] → y[7]
```

It describes parallel bit connections rather than a processor executing one bit at a time.

---

# 8. `for` Loop in Hardware ⭐⭐⭐⭐⭐

Consider:

```verilog
always @(*) begin
    for (i = 0; i < 4; i = i + 1)
        y[i] = a[i] & b[i];
end
```

Conceptually this creates:

```text
a[0] ──AND──→ y[0]
b[0] ──AND──→

a[1] ──AND──→ y[1]
b[1] ──AND──→

a[2] ──AND──→ y[2]
b[2] ──AND──→

a[3] ──AND──→ y[3]
b[3] ──AND──→
```

So four AND operations can be synthesized as parallel hardware.

---

# 9. `while` Loop

Syntax:

```verilog
while (condition)
```

```verilog
statement;
```

The loop continues as long as the condition is true.

Example:

```verilog
integer i;

initial begin
    i = 0;

    while (i < 5) begin
        $display("%d", i);
        i = i + 1;
    end
end
```

Output:

```text
0
1
2
3
4
```

---

# 10. Important Difference: `for` vs `while`

| `for`                                            | `while`                                   |
| ------------------------------------------------ | ----------------------------------------- |
| Initialization, condition, increment in one line | Usually written separately                |
| Convenient for known iteration counts            | Convenient for condition-based repetition |
| Common in synthesizable RTL                      | More commonly seen in testbenches         |
| Compact                                          | More flexible                             |

---

# 11. `while` Loop Condition

Example:

```verilog
while (count < 10)
```

The condition is checked **before** executing the loop body.

If the condition is initially false:

```text
count >= 10
```

the loop executes **zero times**.

---

# 12. `repeat` Loop ⭐⭐⭐⭐⭐

The `repeat` loop executes a statement a fixed number of times.

Syntax:

```verilog
repeat (number)
```

```verilog
statement;
```

Example:

```verilog
repeat (5)
    $display("Hello");
```

This executes:

```text
5 times
```

---

# 13. `repeat` Example

```verilog
initial begin
    repeat (4)
        #10 clk = ~clk;
end
```

The statement:

```verilog
#10 clk = ~clk;
```

is executed four times.

This type of construct is particularly common in **testbenches**.

---

# 14. `repeat` vs `for`

### `for`

```verilog
for (i = 0; i < 5; i = i + 1)
```

Uses a loop variable and condition.

### `repeat`

```verilog
repeat (5)
```

Simply repeats the statement a specified number of times.

Memory trick:

```text
for    → iteration variable
repeat → repetition count
```

---

# 15. `forever` Loop ⭐⭐⭐⭐⭐

The `forever` loop executes continuously.

Syntax:

```verilog
forever
```

```verilog
statement;
```

Example:

```verilog
initial begin
    forever
        #5 clk = ~clk;
end
```

This continuously toggles the clock.

---

# 16. Clock Generation Using `forever`

Very common testbench example:

```verilog
initial begin
    clk = 0;

    forever begin
        #5 clk = ~clk;
    end
end
```

Waveform behavior:

```text
clk: 0 → 1 → 0 → 1 → 0 → ...
```

This continues indefinitely.

---

# 17. Why is `forever` Common in Testbenches?

A clock must continuously operate during simulation.

Therefore:

```verilog
forever
```

is useful for generating a periodic clock.

---

# 18. Can a `forever` Loop End?

Not by itself.

It runs indefinitely unless the simulation is terminated or the procedural flow is otherwise stopped.

For example:

```verilog
initial begin
    forever begin
        #5 clk = ~clk;
    end
end
```

continues until simulation termination.

---

# 19. `break` and `continue`

In modern SystemVerilog, loops can use:

```verilog
break
```

```verilog
continue
```

### `break`

Terminates the current loop.

### `continue`

Skips the remaining statements of the current iteration and proceeds to the next iteration.

For basic Verilog placement preparation, focus primarily on:

```verilog
for
```

```verilog
while
```

```verilog
repeat
```

```verilog
forever
```

---

# 20. Nested Loops

A loop can contain another loop.

Example:

```verilog
integer i, j;

initial begin
    for (i = 0; i < 3; i = i + 1) begin
        for (j = 0; j < 2; j = j + 1) begin
            $display("%d %d", i, j);
        end
    end
end
```

Outer loop:

```text
3 iterations
```

Inner loop:

```text
2 iterations
```

Total executions:

```text
3 × 2 = 6
```

---

# 21. Infinite `while` Loop

Example:

```verilog
while (1) begin
    ...
end
```

Because:

```text
1 = true
```

the condition never becomes false.

Therefore it is an infinite loop.

In simulation, this can cause problems if the loop does not contain a timing control or otherwise allow simulation progress.

---

# 22. Important Interview Trap ⭐⭐⭐⭐⭐

Consider:

```verilog
initial begin
    while (1)
        $display("Hello");
end
```

What happens?

The loop is infinite and contains no timing control.

It can prevent simulation from advancing normally and can cause the simulator to hang.

---

# 23. Loop in Combinational RTL

Example:

```verilog
integer i;

always @(*) begin
    y = 0;

    for (i = 0; i < 4; i = i + 1)
        y = y | a[i];
end
```

This can be used to describe combinational logic.

The loop is **unrolled during synthesis**.

Conceptually:

```text
y = a[0] | a[1] | a[2] | a[3]
```

---

# 24. What Does "Loop Unrolling" Mean?

Suppose:

```verilog
for (i = 0; i < 4; i = i + 1)
    y[i] = a[i] & b[i];
```

The synthesis tool can conceptually expand it into:

```text
y[0] = a[0] & b[0];
y[1] = a[1] & b[1];
y[2] = a[2] & b[2];
y[3] = a[3] & b[3];
```

This is called **loop unrolling**.

---

# 25. Does a `for` Loop Create Four Clock Cycles?

❌ No.

Consider:

```verilog
always @(posedge clk) begin
    for (i = 0; i < 4; i = i + 1)
        q[i] <= d[i];
end
```

This does **not** mean:

```text
Clock 1 → q0
Clock 2 → q1
Clock 3 → q2
Clock 4 → q3
```

Instead, all four register bits can be updated at the **same clock edge**.

---

# 26. Very Important Placement Concept ⭐⭐⭐⭐⭐

### Software loop:

```text
iteration 1
    ↓
iteration 2
    ↓
iteration 3
```

### Synthesized hardware:

A synthesis loop may represent:

```text
hardware 1
hardware 2
hardware 3
```

operating in parallel.

Therefore:

> **A Verilog `for` loop is a description mechanism, not necessarily a sequential execution mechanism in hardware.**

---

# 27. Loop Variables

A common loop variable declaration is:

```verilog
integer i;
```

Example:

```verilog
integer i;

always @(*) begin
    for (i = 0; i < 8; i = i + 1)
        y[i] = a[i];
end
```

In SystemVerilog, an integer loop variable can also be declared directly in the loop.

---

# 28. Synthesizable vs Simulation-Oriented Loops

### Commonly synthesizable:

```verilog
for
```

when the iteration bounds are static and synthesis can determine the hardware structure.

### Commonly used in testbenches:

```verilog
while
```

```verilog
repeat
```

```verilog
forever
```

especially when they involve simulation timing.

This is a general coding guideline, not an absolute restriction.

---

# 29. `for` Loop in Register Reset

Example:

```verilog
integer i;

always @(posedge clk) begin
    if (reset) begin
        for (i = 0; i < 8; i = i + 1)
            q[i] <= 1'b0;
    end
end
```

This can describe resetting an 8-bit register.

Conceptually:

```text
q[0] ← 0
q[1] ← 0
...
q[7] ← 0
```

at the same clock edge.

---

# 30. `for` Loop in Memory Initialization

Loops are often used in testbenches to initialize arrays or memories.

Example:

```verilog
integer i;

initial begin
    for (i = 0; i < 16; i = i + 1)
        memory[i] = 0;
end
```

This initializes 16 memory locations.

---

# 31. Loop and Timing Control

A testbench can use:

```verilog
repeat (10) begin
    #10 clk = ~clk;
end
```

The `#10` introduces simulation time delay.

Important:

```text
Loop itself → repetition
#delay → simulation time advancement
```

---

# 32. Common Mistake

Do not assume:

```verilog
for (...)
```

means:

```text
one iteration per clock
```

It does not.

To create clock-by-clock behavior, you need appropriate sequential logic and clock/event control.

---

# ⭐ Frequently Asked Placement Questions

## Q1. What are the looping constructs in Verilog?

**Answer:**

```text
for
while
repeat
forever
```

---

## Q2. Which loop is most commonly used for synthesizable RTL?

**Answer:**

```text
for loop
```

especially when the number of iterations is statically determinable.

---

## Q3. What is the difference between `for` and `repeat`?

**Answer:**

`for` uses initialization, condition, and increment, while `repeat` executes a statement a specified number of times.

---

## Q4. What is a `while` loop?

**Answer:** A loop that repeatedly executes while its condition remains true.

---

## Q5. What is a `forever` loop?

**Answer:** A loop that executes indefinitely until simulation or procedural execution is terminated.

---

## Q6. Where is `forever` commonly used?

**Answer:** In testbenches, especially for continuous clock generation.

---

## Q7. How can you generate a clock using `forever`?

**Answer:**

```verilog
initial begin
    clk = 0;
    forever
        #5 clk = ~clk;
end
```

---

## Q8. How many times does this execute?

```verilog
for (i = 0; i < 8; i = i + 1)
```

**Answer:**

```text
8 times
```

---

## Q9. How many times does this execute?

```verilog
repeat (10)
```

**Answer:**

```text
10 times
```

---

## Q10. Does a `for` loop necessarily create sequential hardware?

**Answer:** No. A synthesizable loop is generally a way of describing repetitive hardware, and the synthesis tool may unroll it into parallel hardware.

---

## Q11. What is loop unrolling?

**Answer:** Loop unrolling is the process of expanding loop iterations into individual hardware operations during synthesis.

---

## Q12. Can a `for` loop be used inside `always @(posedge clk)`?

**Answer:** Yes.

Example:

```verilog
always @(posedge clk) begin
    for (i = 0; i < 8; i = i + 1)
        q[i] <= d[i];
end
```

All register bits can update at the same clock edge.

---

## Q13. What happens if a `while` condition is initially false?

**Answer:** The loop executes zero times.

---

## Q14. What happens with an infinite loop having no timing control in a testbench?

**Answer:** It can prevent simulation from advancing and may cause the simulator to hang.

---

## Q15. What is a nested loop?

**Answer:** A loop placed inside another loop.

---

## Q16. How many times does the inner body execute?

```verilog
for (i = 0; i < 4; i = i + 1)
    for (j = 0; j < 3; j = j + 1)
        ...
```

**Answer:**

```text
4 × 3 = 12
```

times.

---

## Q17. Which loop is commonly used for clock generation?

**Answer:**

```verilog
forever
```

---

## Q18. Which loop is convenient when the number of repetitions is known?

**Answer:**

```verilog
for
```

or `repeat`, depending on the coding requirement.

---

# 🔥 Placement Rapid-Fire

**Four main Verilog loops?**

→ `for`, `while`, `repeat`, `forever`

**Most common synthesizable loop?**

→ `for`

**Fixed repetition count?**

→ `repeat`

**Condition-controlled loop?**

→ `while`

**Infinite loop?**

→ `forever`

**Clock generation?**

→ `forever`

**Known iteration count?**

→ `for`

**Loop hardware behavior?**

→ May be unrolled into hardware

**Four iterations mean four clocks?**

→ ❌ No

**Nested loops?**

→ Loop inside another loop

**`for (i=0; i<8; i=i+1)` iterations?**

→ 8

**`repeat(5)` iterations?**

→ 5

**Missing timing control in infinite simulation loop?**

→ Can hang simulation

---

# 🧠 9.15 QUICK REVISION

```text
                 VERILOG LOOPS
                      │
        ┌─────────────┼─────────────┐
        ↓             ↓             ↓
       for          while         repeat
        │             │             │
   known count     condition     fixed count
        │             │
        └─────────────┴──────┐
                              ↓
                           forever
                              │
                        infinite loop
```

### `for`

```verilog
for (i = 0; i < 8; i = i + 1)
```

→ Known iteration count.

### `while`

```verilog
while (condition)
```

→ Executes while condition is true.

### `repeat`

```verilog
repeat (10)
```

→ Executes 10 times.

### `forever`

```verilog
forever
```

→ Executes indefinitely.

### ⭐ Golden Rules

```text
for     → commonly used for synthesizable repetitive RTL
repeat  → fixed number of repetitions
while   → condition-controlled repetition
forever → infinite repetition
Verilog loop ≠ one hardware cycle per iteration
```
