# SYNTHESIZABLE vs NON-SYNTHESIZABLE VERILOG

## ⭐⭐⭐⭐⭐ Placement Very Important

This is the **final topic of Phase 9**.

A very common VLSI interview question is:

> **"What is the difference between synthesizable and non-synthesizable Verilog?"**

Understanding this is important because **Verilog can describe both hardware and simulation behavior**, but not every Verilog construct can be converted into physical hardware.

---

# 1. What is Synthesis?

**Synthesis** is the process of converting RTL/Verilog code into a hardware representation, typically a **gate-level netlist**.

Basic flow:

```text
Verilog RTL
```

↓

Synthesis

↓

Gate-Level Netlist

↓

Technology Mapping

↓

Physical Hardware

For an FPGA, synthesis ultimately maps logic into FPGA resources.

For an ASIC, synthesis maps RTL into standard-cell logic.

---

# 2. What is Synthesizable Verilog?

**Synthesizable Verilog** is Verilog code that can be converted by a synthesis tool into actual hardware.

Examples:

```verilog
assign y = a & b;
```

```verilog
always @(*) begin
    y = a | b;
end
```

```verilog
always @(posedge clk) begin
    q <= d;
end
```

These can represent real hardware.

---

# 3. What is Non-Synthesizable Verilog?

**Non-synthesizable Verilog** contains constructs that generally cannot be directly converted into physical hardware.

They are primarily used for:

* Simulation
* Testbenches
* Verification
* Modeling simulation behavior

Examples include:

```verilog
#10
```

and:

```verilog
$display(...)
```

---

# 4. Why Can't Everything Be Synthesized?

Hardware must physically exist.

For example:

```verilog
#10;
```

means:

> Wait for 10 simulation time units.

A synthesis tool cannot simply create a generic hardware component called:

```text
"wait exactly 10 simulation units"
```

without knowing the target technology, clock, delays, process characteristics, etc.

Therefore explicit simulation delays are generally non-synthesizable.

---

# 5. Synthesizable vs Non-Synthesizable

| Synthesizable                | Non-Synthesizable                   |
| ---------------------------- | ----------------------------------- |
| Can be converted to hardware | Mainly simulation behavior          |
| Used in RTL                  | Commonly used in testbenches        |
| Produces hardware structures | Doesn't directly represent hardware |
| `assign`                     | `#delay`                            |
| `always @(*)`                | `$display`                          |
| `always @(posedge clk)`      | `$monitor`                          |
| `if` / `case`                | `$finish`                           |
| Synthesizable loops          | Many testbench constructs           |

---

# 6. `assign` Is Synthesizable

Example:

```verilog
assign y = a & b;
```

Synthesis can create an AND gate.

Conceptually:

```text
a ───┐
     AND ─── y
b ───┘
```

Therefore:

```text
assign → synthesizable
```

---

# 7. `always @(*)` Is Synthesizable

Example:

```verilog
always @(*) begin
    y = a & b;
end
```

Synthesis recognizes this as combinational logic.

It can produce:

```text
AND gate
```

---

# 8. Clocked `always` Is Synthesizable

Example:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

This can synthesize to a flip-flop.

Conceptually:

```text
       ┌─────┐
d ────►│  D  │
clk ──►│ FF  │───► q
       └─────┘
```

---

# 9. `if-else` Is Synthesizable

Example:

```verilog
always @(*) begin

    if (sel)
        y = a;
    else
        y = b;

end
```

This can synthesize to a:

```text
2:1 Multiplexer
```

---

# 10. `case` Is Synthesizable

Example:

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

This can synthesize to combinational selection logic such as a multiplexer.

---

# 11. Arithmetic Operators Are Synthesizable

For example:

```verilog
assign y = a + b;
```

can synthesize into an adder.

Similarly:

```verilog
assign y = a - b;
```

can synthesize into subtraction hardware.

And:

```verilog
assign y = a * b;
```

may synthesize into multiplier hardware, depending on the target technology and constraints.

---

# 12. Relational Operators

Example:

```verilog
assign y = (a > b);
```

This can synthesize into comparison logic.

Similarly:

```verilog
assign y = (a == b);
```

can synthesize into equality-comparison hardware.

---

# 13. Loops Can Be Synthesizable ⭐⭐⭐⭐⭐

A common misconception is:

> "Loops are non-synthesizable."

That is **not always true**.

Some loops can be synthesized.

Example:

```verilog
integer i;

always @(*) begin

    y = 0;

    for (i = 0; i < 8; i = i + 1)
        y = y + a[i];

end
```

A synthesis tool can **unroll** the loop and create hardware corresponding to the repeated operations.

---

# 14. What Does Loop Unrolling Mean?

Suppose:

```verilog
for (i = 0; i < 4; i = i + 1)
```

A synthesis tool can conceptually expand it into repeated hardware operations.

Instead of physically creating:

```text
software loop
```

it creates:

```text
hardware corresponding to each iteration
```

Therefore:

```text
Synthesizable loop

→ compile-time/static iteration

→ hardware expansion
```

---

# 15. Important Rule for Synthesizable Loops

A loop is generally synthesizable when the synthesis tool can determine the iteration behavior statically.

For example:

```verilog
for (i = 0; i < 8; i = i + 1)
```

is straightforward.

But a loop that depends on an unknown runtime condition may not synthesize as intended.

---

# 16. `initial` Block ⭐⭐⭐⭐⭐

This is an important interview topic.

Example:

```verilog
initial begin
    a = 0;
    b = 0;
end
```

In general ASIC RTL:

```text
initial → generally non-synthesizable
```

However, there are **technology-specific exceptions**, particularly in some FPGA flows where initialization can be synthesized into device configuration resources.

For placement interviews, the safest answer is:

> `initial` blocks are generally considered non-synthesizable for ASIC RTL, though some FPGA tools support limited synthesis of initialization constructs.

---

# 17. Delay `#` Is Generally Non-Synthesizable

Example:

```verilog
#10 y = a;
```

The `#10` represents a simulation delay.

Generally:

```text
#delay → non-synthesizable
```

In real hardware, timing is determined by:

* Gate delays
* Routing delays
* Clock period
* Technology
* PVT conditions
* Timing constraints

rather than arbitrary RTL `#` delays.

---

# 18. `$display` Is Non-Synthesizable

Example:

```verilog
$display("Value = %d", y);
```

This prints information during simulation.

It does not describe hardware.

Therefore:

```text
$display → non-synthesizable
```

It is commonly used in:

```text
Testbenches
```

---

# 19. `$monitor`

Example:

```verilog
$monitor("a=%b b=%b y=%b", a, b, y);
```

This continuously monitors signal values during simulation.

It does not represent hardware.

Therefore:

```text
$monitor → non-synthesizable
```

---

# 20. `$finish`

Example:

```verilog
$finish;
```

This terminates simulation.

There is no physical hardware equivalent.

Therefore:

```text
$finish → non-synthesizable
```

---

# 21. Testbench Constructs

A typical testbench may contain:

```verilog
initial begin

    a = 0;
    b = 0;

    #10 a = 1;
    #10 b = 1;

    $display("Result = %b", y);

    #20 $finish;

end
```

This is intended to:

```text
Generate stimulus
```

↓

Observe behavior

↓

Finish simulation

It is not intended to become hardware.

---

# 22. Testbench vs RTL

### RTL

```text
Describes hardware
```

### Testbench

```text
Tests hardware behavior
```

Conceptually:

```text
             Verilog
                │
        ┌───────┴────────┐
        ↓                ↓
       RTL            Testbench
        ↓                ↓
    Synthesis        Simulation
        ↓
    Hardware
```

---

# 23. `wait` Statement

Example:

```verilog
wait (done);
```

This is commonly used in testbench/simulation code.

In general RTL coding:

```text
wait → generally non-synthesizable
```

Avoid using such constructs in normal synthesizable RTL unless the target synthesis tool explicitly supports the particular construct.

---

# 24. Event Controls

Example:

```verilog
@(posedge clk);
```

Event controls can be synthesizable in appropriate clocked RTL contexts.

For example:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

is standard synthesizable RTL.

But arbitrary event-control constructs used for testbench synchronization are not necessarily synthesizable.

---

# 25. `fork...join`

Example:

```verilog
fork
    statement1;
    statement2;
join
```

This is commonly used for parallel simulation processes.

It is generally:

```text
Non-synthesizable
```

and is primarily used in testbenches.

---

# 26. File Operations

Examples:

```verilog
$fopen
$fclose
$fread
$fwrite
$fscanf
```

These interact with files during simulation.

They are generally:

```text
Non-synthesizable
```

because physical hardware cannot directly perform arbitrary simulator file operations.

---

# 27. System Tasks

Common system tasks include:

```verilog
$display
$monitor
$finish
$fopen
$fwrite
$fread
```

These are primarily simulation/verification constructs.

---

# 28. Synthesizable Constructs — Important List ⭐⭐⭐⭐⭐

Common synthesizable Verilog constructs include:

```text
assign
always @(*)
always @(posedge clk)
if
else
case
for
while (under synthesis restrictions)
arithmetic operators
logical operators
bitwise operators
comparisons
parameters
generate
module instantiation
```

The exact supported subset depends on the synthesis tool and target technology.

---

# 29. Non-Synthesizable Constructs — Important List ⭐⭐⭐⭐⭐

Common examples:

```text
#delay
$display
$monitor
$finish
$fopen
$fclose
$fread
$fwrite
wait
fork...join
many testbench-only constructs
```

Also remember:

```text
initial
```

is generally non-synthesizable in ASIC RTL, with technology-specific FPGA exceptions.

---

# 30. Synthesizable vs Simulation-Only

A useful interview rule is:

> **If a construct describes something that can be physically implemented as hardware, it may be synthesizable. If it mainly describes simulator behavior, it is usually non-synthesizable.**

Examples:

```text
AND operation
```

→ hardware → synthesizable

```text
Flip-flop
```

→ hardware → synthesizable

```text
MUX
```

→ hardware → synthesizable

```text
Simulation delay
```

→ simulator behavior → non-synthesizable

```text
Print message
```

→ simulator behavior → non-synthesizable

```text
End simulation
```

→ simulator behavior → non-synthesizable

---

# 31. Important: Synthesizable Does Not Mean Efficient

A construct can be synthesizable but still produce **bad hardware**.

Example:

```verilog
assign y = a * b;
```

It may synthesize successfully.

But depending on:

* operand width
* target technology
* timing constraints
* area constraints

it may create a large or slow multiplier.

Therefore:

```text
Synthesizable ≠ optimal
```

---

# 32. Important Placement Concept ⭐⭐⭐⭐⭐

Synthesis converts **behavioral intent** into hardware.

For example:

```verilog
assign y = a & b;
```

becomes approximately:

```text
AND gate
```

And:

```verilog
always @(posedge clk)
    q <= d;
```

becomes approximately:

```text
Flip-flop
```

Therefore the synthesis tool interprets the RTL and builds an equivalent hardware structure.

---

# 33. Example — Synthesizable RTL

```verilog
module mux2to1 (
    input  a,
    input  b,
    input  sel,
    output reg y
);

always @(*) begin

    if (sel)
        y = b;
    else
        y = a;

end

endmodule
```

This is synthesizable and represents a:

```text
2:1 MUX
```

---

# 34. Example — Non-Synthesizable Testbench

```verilog
initial begin

    a = 0;
    b = 0;

    #10 a = 1;
    #10 b = 1;

    $display("y = %b", y);

    #10 $finish;

end
```

This is simulation code.

It:

```text
generates stimulus
```

↓

waits

↓

prints result

↓

ends simulation

It does not directly represent hardware.

---

# 35. Synthesizable vs Non-Synthesizable Table

| Construct                | Typical Status          | Purpose                    |
| ------------------------ | ----------------------- | -------------------------- |
| `assign`                 | ✅ Synthesizable         | Combinational logic        |
| `always @(*)`            | ✅ Synthesizable         | Combinational RTL          |
| `always @(posedge clk)`  | ✅ Synthesizable         | Sequential RTL             |
| `if/else`                | ✅                       | Logic selection            |
| `case`                   | ✅                       | MUX/decoder/FSM logic      |
| `for` with static bounds | ✅                       | Repeated hardware          |
| Arithmetic operators     | ✅                       | Arithmetic hardware        |
| `parameter`              | ✅                       | Compile-time configuration |
| `generate`               | ✅                       | Structural generation      |
| `#10`                    | ❌ Generally             | Simulation delay           |
| `$display`               | ❌                       | Simulation output          |
| `$monitor`               | ❌                       | Simulation monitoring      |
| `$finish`                | ❌                       | End simulation             |
| `$fopen`                 | ❌                       | File operations            |
| `wait`                   | ❌ Generally             | Simulation synchronization |
| `fork...join`            | ❌ Generally             | Parallel simulation        |
| `initial`                | ❌ Generally in ASIC RTL | Initialization/simulation  |

---

# 36. Common Interview Trap

### Question:

> Are loops synthesizable?

Wrong answer:

> No, loops are non-synthesizable.

Correct answer:

> **Some loops are synthesizable.** Static, bounded loops can be unrolled by synthesis tools into hardware. The exact synthesis support depends on the construct and tool.

---

# 37. Another Interview Trap

### Question:

> Is `initial` always non-synthesizable?

Better answer:

> `initial` is generally considered non-synthesizable for ASIC RTL, but some FPGA synthesis tools support limited initialization constructs. Therefore the answer depends on the target technology and tool.

---

# 38. Another Interview Trap

### Question:

> Is every Verilog statement synthesizable?

Answer:

**No.**

Verilog supports both:

```text
Hardware description
```

*

```text
Simulation/verification behavior
```

Only the synthesizable subset can be converted into hardware.

---

# 39. Golden Rule

Remember:

```text
RTL
```

↓

Must describe hardware

↓

Synthesis

↓

Hardware

Simulation-only code:

```text
Testbench
```

↓

Simulation

↓

No hardware

---

# ⭐ Frequently Asked Placement Questions

## Q1. What is synthesis?

**Answer:** Synthesis is the process of converting synthesizable RTL into a hardware representation such as a gate-level netlist.

---

## Q2. What is synthesizable Verilog?

**Answer:** Verilog constructs that can be translated by a synthesis tool into hardware.

---

## Q3. What is non-synthesizable Verilog?

**Answer:** Verilog constructs that primarily describe simulation or verification behavior and cannot generally be directly converted into hardware.

---

## Q4. Give examples of synthesizable constructs.

**Answer:**

* `assign`
* `always @(*)`
* `always @(posedge clk)`
* `if/else`
* `case`
* Static `for` loops
* Arithmetic operators
* Parameters
* Generate constructs

---

## Q5. Give examples of non-synthesizable constructs.

**Answer:**

* `#` delays
* `$display`
* `$monitor`
* `$finish`
* File operations
* `wait`
* `fork...join`
* Many testbench-only constructs

---

## Q6. Is `#10` synthesizable?

**Answer:** Generally no. `#10` is a simulation delay.

---

## Q7. Is `$display` synthesizable?

**Answer:** No. `$display` is used to print information during simulation.

---

## Q8. Is `for` loop synthesizable?

**Answer:** Yes, when written in a form supported by synthesis, especially with statically determinable iteration bounds. The loop is generally unrolled into hardware.

---

## Q9. Is `case` synthesizable?

**Answer:** Yes. A `case` statement can synthesize into combinational selection logic, decoder logic, FSM logic, etc.

---

## Q10. Is `if-else` synthesizable?

**Answer:** Yes. It can synthesize into multiplexing and other conditional logic.

---

## Q11. Is `initial` synthesizable?

**Answer:** In ASIC RTL, it is generally considered non-synthesizable. Some FPGA tools support certain initialization uses.

---

## Q12. Can synthesizable Verilog contain a clock?

**Answer:** Yes. Clocked `always` blocks such as `always @(posedge clk)` are standard synthesizable RTL for sequential logic.

---

## Q13. Does synthesizable code always produce efficient hardware?

**Answer:** No. Synthesizable code can still produce hardware that is inefficient in area, power, or timing.

---

## Q14. What is the difference between RTL and testbench?

**Answer:**

```text
RTL
```

→ describes hardware

```text
Testbench
```

→ stimulates and verifies hardware

---

## Q15. Why are simulation delays generally non-synthesizable?

**Answer:** Because `#` delays represent simulator time rather than a specific physical hardware structure.

---

# 🔥 Placement Rapid-Fire

**Can** **`assign`** **be synthesized?**

→ ✅ Yes

**Can** **`always @(*)`** **be synthesized?**

→ ✅ Yes

**Can** **`always @(posedge clk)`** **be synthesized?**

→ ✅ Yes

**Can** **`if-else`** **be synthesized?**

→ ✅ Yes

**Can** **`case`** **be synthesized?**

→ ✅ Yes

**Can a static** **`for`** **loop be synthesized?**

→ ✅ Yes

**Is** **`#10`** **generally synthesizable?**

→ ❌ No

**Is** **`$display`** **synthesizable?**

→ ❌ No

**Is** **`$finish`** **synthesizable?**

→ ❌ No

**Are file operations synthesizable?**

→ ❌ Generally no

**Are all loops non-synthesizable?**

→ ❌ No

**Is synthesizable code always optimized?**

→ ❌ No

**Does** **`initial`** **have exceptions?**

→ ✅ Yes, especially in some FPGA flows

**RTL describes?**

→ Hardware

**Testbench describes?**

→ Simulation/verification

---

# 🧠 9.24 QUICK REVISION

```text
                 VERILOG
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
     SYNTHESIZABLE       NON-SYNTHESIZABLE
          │                   │
          ↓                   ↓
       HARDWARE            SIMULATION
          │                   │
          ↓                   ↓
       assign              #delay
       always              $display
       if/else             $monitor
       case                $finish
       registers           file I/O
       arithmetic          wait
       static loops        fork/join
```

### ⭐ Golden Rules

```text
Synthesizable Verilog → Hardware
Non-synthesizable Verilog → Simulation/Verification
#delay → Generally non-synthesizable
$display → Simulation only
Static bounded loops can be synthesizable
Synthesizable ≠ necessarily optimal
```
