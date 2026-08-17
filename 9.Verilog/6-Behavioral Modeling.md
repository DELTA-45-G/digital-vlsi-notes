# &#x20;BEHAVIORAL MODELING ⭐⭐⭐⭐⭐

Behavioral modeling is one of the **most important Verilog topics for VLSI placements** because most practical RTL designs use behavioral/procedural constructs.

It describes **what the circuit should do** rather than explicitly describing every gate.

---

# 1. What is Behavioral Modeling?

**Behavioral modeling** describes the behavior of a digital circuit using procedural statements.

Common constructs are:

```text
always
```

if

else

case

for

while

Example:

```text
always @(*) begin
```

y = a & b;

end

Instead of explicitly writing:

```text
and (y, a, b);
```

we describe the required behavior.

---

# 2. Main Keyword — `always`

The most important construct in behavioral modeling is:

```text
always
```

Example:

```text
always @(*) begin
```

y = a & b;

end

The `always` block describes behavior that is repeatedly evaluated according to its sensitivity/event control.

---

# 3. Basic Syntax

```text
always @(sensitivity_list) begin
```

// procedural statements

end

Example:

```text
always @(*) begin
```

y = a & b;

end

---

# 4. What is a Sensitivity List?

The sensitivity list specifies **which signals cause the** **`always`** **block to execute**.

Example:

```text
always @(a or b)
```

The block executes when `a` or `b` changes.

For combinational logic, the commonly used form is:

```text
always @(*)
```

This automatically includes signals read by the block.

---

# 5. `always @(*)` ⭐⭐⭐⭐⭐

For combinational logic:

```text
always @(*) begin
```

y = a & b;

end

`@(*)` means the simulator automatically considers the signals referenced by the block.

### Memory trick

```text
@(*) → Combinational logic
```

---

# 6. Behavioral AND Gate

```text
module and_gate (
```

input a,

input b,

output reg y

);

always @(*) begin

y = a & b;

end

endmodule

Notice:

```text
always → procedural block
```

reg    → traditional Verilog variable type for procedural assignment

---

# 7. Behavioral OR Gate

```text
always @(*) begin
```

y = a | b;

end

---

# 8. Behavioral NOT Gate

```text
always @(*) begin
```

y = ~a;

end

---

# 9. `if-else` in Behavioral Modeling

Example:

```text
always @(*) begin
```

if (sel)

y = b;

else

y = a;

end

This describes a **2:1 MUX**.

---

# 10. 2:1 MUX Using Behavioral Modeling

```text
module mux2to1 (
```

input a,

input b,

input sel,

output reg y

);

always @(*) begin

if (sel == 1'b0)

y = a;

else

y = b;

end

endmodule

### Operation

```text
sel = 0 → y = a
```

sel = 1 → y = b

---

# 11. `if-else if-else`

Behavioral modeling can describe multiple conditions.

Example:

```text
always @(*) begin
```

if (a > b)

y = 2'b01;

else if (a < b)

y = 2'b10;

else

y = 2'b00;

end

This can describe a comparator.

---

# 12. `case` Statement ⭐⭐⭐⭐⭐

`case` is extremely important for placements.

Basic syntax:

```text
always @(*) begin
```

case (sel)

2'b00: y = a;

2'b01: y = b;

2'b10: y = c;

2'b11: y = d;

endcase

end

This is commonly used to describe a **MUX, decoder, FSM, etc.**

---

# 13. 4:1 MUX Using `case`

```text
module mux4to1 (
```

input [1:0] sel,

input a,

input b,

input c,

input d,

output reg y

);

always @(*) begin

case (sel)

2'b00: y = a;

2'b01: y = b;

2'b10: y = c;

2'b11: y = d;

endcase

end

endmodule

---

# 14. `default` Case ⭐⭐⭐⭐⭐

A good practice is to provide a `default`.

```text
always @(*) begin
```

case (sel)

2'b00: y = a;

2'b01: y = b;

2'b10: y = c;

2'b11: y = d;

default: y = 1'b0;

endcase

end

Why?

It helps ensure that the output receives a defined value for unexpected/unknown conditions and can help avoid unintended incomplete assignments.

---

# 15. Why Can Missing Assignments Cause a Latch?

Consider:

```text
always @(*) begin
```

if (en)

y = a;

end

What happens when:

```text
en = 0
```

There is no assignment to `y`.

The previous value must be retained.

This implies storage behavior, potentially resulting in a **latch** after synthesis.

---

# 16. How to Avoid an Unintended Latch

Provide a default assignment.

```text
always @(*) begin
```

y = 1'b0;

if (en)

y = a;

end

Now `y` always gets a value.

### Memory trick

```text
Combinational block
```

```
    ↓
```

Every output should get a value

```
    ↓
```

No unintended latch

---

# 17. Behavioral Sequential Logic

Behavioral modeling is also commonly used for sequential circuits.

Example D flip-flop:

```text
always @(posedge clk) begin
```

q <= d;

end

This describes:

> On every rising edge of the clock, capture `d` into `q`.

---

# 18. Why `posedge`?

```text
@(posedge clk)
```

means the block executes when the clock changes:

```text
0 → 1
```

This is called a **positive/rising edge**.

Similarly:

```text
@(negedge clk)
```

means:

```text
1 → 0
```

which is the **negative/falling edge**.

---

# 19. D Flip-Flop with Reset

Example synchronous reset:

```text
always @(posedge clk) begin
```

if (reset)

q <= 1'b0;

else

q <= d;

end

This means:

```text
At rising edge:
```

```
reset = 1 → q = 0

reset = 0 → q = d
```

---

# 20. Asynchronous Reset

An asynchronous reset is included in the sensitivity list.

```text
always @(posedge clk or posedge reset) begin
```

if (reset)

q <= 1'b0;

else

q <= d;

end

Here the reset can affect `q` without waiting for the clock edge.

### Important interview difference

```text
Synchronous reset
```

→ reset checked at clock edge

Asynchronous reset

→ reset can act independently of clock

---

# 21. Blocking vs Non-Blocking Assignment ⭐⭐⭐⭐⭐

This is one of the **most frequently asked Verilog placement questions**.

There are two major assignment operators:

```text
=   Blocking
```

<=  Non-blocking

---

# 22. Blocking Assignment `=`

Example:

```text
always @(*) begin
```

y = a & b;

end

Blocking assignment executes immediately in procedural order.

It is commonly used for **combinational logic**.

---

# 23. Non-Blocking Assignment `<=`

Example:

```text
always @(posedge clk) begin
```

q <= d;

end

Non-blocking assignments schedule updates so that sequential state changes model clocked hardware correctly.

It is commonly used for **sequential logic**.

---

# 24. Important Memory Rule

Combinational → usually = Sequential → usually <=

This is a very useful RTL coding rule.

---

# 25. Example: Combinational Logic

```text
always @(*) begin
```

y = a & b;

end

Use:

```text
=
```

---

# 26. Example: Sequential Logic

```text
always @(posedge clk) begin
```

q <= d;

end

Use:

```text
<=
```

---

# 27. Why Not Use `=` for Sequential Logic?

Using blocking assignments in clocked logic can cause simulation-ordering problems and can produce behavior that does not accurately model intended flip-flop interactions.

For standard RTL coding:

```text
Clocked logic → non-blocking <=
```

is the preferred style.

---

# 28. Why Not Use `<=` Everywhere?

You can encounter different coding styles, but standard RTL guidelines generally recommend:

```text
Combinational → blocking =
```

Sequential → non-blocking <=

This makes the intended hardware behavior clearer and avoids many simulation-ordering issues.

---

# 29. Behavioral Modeling of a Counter

Example 4-bit up counter:

```text
module counter (
```

input clk,

input reset,

output reg [3:0] q

);

always @(posedge clk) begin

if (reset)

q <= 4'b0000;

else

q <= q + 1'b1;

end

endmodule

Each rising clock edge increments the counter.

---

# 30. Behavioral Modeling of a Register

4-bit register:

```text
always @(posedge clk) begin
```

q <= d;

end

Here:

```text
d → input data
```

q → stored data

clk → clock

---

# 31. Behavioral Modeling of an FSM

FSMs are commonly described using behavioral constructs:

```text
always
```

case

if

Typical structure:

```text
always @(posedge clk) begin
```

state <= next_state;

end

and:

```text
always @(*) begin
```

case (state)

// state transitions

endcase

end

This becomes extremely important in practical RTL design.

---

# 32. `always` Blocks Are Procedural

Statements inside an `always` block execute **procedurally** in the order written.

But separate `always` blocks operate concurrently.

Example:

```text
always @(*) begin
```

y1 = a & b;

end

always @(*) begin

y2 = c | d;

end

These represent separate concurrent hardware processes.

---

# 33. One Important Concept: Behavioral ≠ Software

Verilog behavioral code may look like programming code:

```text
if
```

else

case

for

But synthesis interprets synthesizable RTL as **hardware**.

For example:

```text
if (sel)
```

y = b;

else

y = a;

doesn't mean software is running an `if`.

It describes hardware equivalent to a MUX.

---

# 34. Behavioral vs Dataflow

### Dataflow

```text
assign y = a & b;
```

### Behavioral

```text
always @(*) begin
```

y = a & b;

end

Both can synthesize to equivalent combinational hardware.

Main difference:

| DataflowBehavioral            |                                         |
| ----------------------------- | --------------------------------------- |
| Uses `assign`                 | Uses `always`                           |
| Continuous assignment         | Procedural block                        |
| Expression-oriented           | Behavior-oriented                       |
| Very convenient for equations | Very convenient for conditions/case/FSM |

---

# 35. Behavioral vs Gate-Level

### Gate-level

```text
and (y, a, b);
```

### Behavioral

```text
always @(*) begin
```

y = a & b;

end

Gate-level explicitly describes a gate primitive.

Behavioral describes the desired behavior.

---

# ⭐ Frequently Asked Placement Questions

## Q1. What is behavioral modeling?

**Answer:** Behavioral modeling describes the functionality or behavior of a circuit using procedural constructs such as `always`, `if`, and `case`.

---

## Q2. Which keyword is mainly associated with behavioral modeling?

**Answer:**

```text
always
```

---

## Q3. What is `always @(*)` used for?

**Answer:** It is commonly used to describe combinational logic because the simulator automatically includes signals read inside the block in the sensitivity set.

---

## Q4. What is the difference between `=` and `<=`?

**Answer:**

```text
=  → Blocking assignment
```

<= → Non-blocking assignment

Blocking assignments are commonly used in combinational procedural logic, while non-blocking assignments are commonly used in clocked sequential logic.

---

## Q5. Which assignment is preferred for sequential logic?

**Answer:**

```text
<=
```

Non-blocking assignment.

---

## Q6. Which assignment is commonly preferred for combinational logic?

**Answer:**

```text
=
```

Blocking assignment.

---

## Q7. What is a latch?

**Answer:** A latch is a level-sensitive storage element.

In RTL, an unintended latch can be inferred when a combinational procedural block does not assign an output for every possible condition.

---

## Q8. How can you avoid an unintended latch?

**Answer:** Ensure every output receives an assignment for every possible condition, often by providing a default assignment at the beginning of the combinational block.

Example:

```text
always @(*) begin
```

y = 1'b0;

if (en)

y = a;

end

---

## Q9. What is the difference between `posedge` and `negedge`?

**Answer:**

```text
posedge → 0 → 1
```

negedge → 1 → 0

---

## Q10. How do you describe a D flip-flop?

```text
always @(posedge clk) begin
```

q <= d;

end

---

## Q11. How do you describe a synchronous reset?

```text
always @(posedge clk) begin
```

if (reset)

q <= 0;

else

q <= d;

end

---

## Q12. How do you describe an asynchronous reset?

```text
always @(posedge clk or posedge reset) begin
```

if (reset)

q <= 0;

else

q <= d;

end

---

## Q13. What is the difference between synchronous and asynchronous reset?

**Answer:**

| Synchronous ResetAsynchronous Reset           |                                         |
| --------------------------------------------- | --------------------------------------- |
| Checked with clock                            | Can act independently of clock          |
| Reset included in logic checked at clock edge | Reset event appears in sensitivity list |
| `@(posedge clk)`                              | `@(posedge clk or posedge reset)`       |

---

## Q14. Can behavioral modeling describe combinational circuits?

**Answer:** Yes.

Example:

```text
always @(*) begin
```

y = a & b;

end

---

## Q15. Can behavioral modeling describe sequential circuits?

**Answer:** Yes.

Example:

```text
always @(posedge clk) begin
```

q <= d;

end

---

# 🔥 Placement Rapid-Fire

**Behavioral modeling → ?**

→ `always`, `if`, `case`

**Combinational sensitivity → ?**

→ `@(*)`

**Sequential sensitivity → ?**

→ `@(posedge clk)`

**Blocking operator → ?**

→ `=`

**Non-blocking operator → ?**

→ `<=`

**Combinational logic → usually?**

→ `=`

**Sequential logic → usually?**

→ `<=`

**Rising edge → ?**

→ `posedge`

**Falling edge → ?**

→ `negedge`

**Missing assignment in combinational block can infer?**

→ Latch

**MUX commonly uses?**

→ `if-else` or `case`

**FSM commonly uses?**

→ `always` + `case`

---

# 🧠 9.6 QUICK REVISION

```text
              BEHAVIORAL MODELING
```

```
                  ↓

                always

                  ↓

      ┌───────────┼───────────┐

      ↓           ↓           ↓

     if          case        loops

      ↓           ↓

   MUX/etc.      FSM/etc.
```

### Combinational

```text
always @(*) begin
```

y = a & b;

end

### Sequential

```text
always @(posedge clk) begin
```

q <= d;

end

### Main assignment rule

Combinational → = Sequential → <=

### Main memory trick

```text
Behavioral
```

↓

always

↓

if / case

↓

Combinational + Sequential + FSM
