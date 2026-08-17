## Quick Revision Notes — All 24 Topics

---

# 9.1 — Introduction to Verilog HDL

### What is Verilog?

**Verilog HDL (Hardware Description Language)** is used to describe, simulate, and synthesize digital hardware.

### Key points

* Verilog describes **hardware behavior and structure**.
* Used for **RTL design, simulation, and synthesis**.
* Supports:

  * Gate-level modeling
  * Dataflow modeling
  * Behavioral modeling
  * Structural modeling

### Remember

```text
Verilog
   ↓
Describe Hardware
   ↓
Simulation + Synthesis
```

---

# 9.2 — Verilog Design Flow & RTL

### Basic flow

```text
Design Specification
        ↓
      RTL
        ↓
 Verilog Code
        ↓
   Simulation
        ↓
   Synthesis
        ↓
Gate-Level Netlist
        ↓
Physical Design
```

### RTL

**RTL = Register Transfer Level**

Describes:

* Data transfer between registers
* Combinational logic between registers
* Clocked storage elements

### Remember

```text
RTL = Registers + Combinational Logic + Data Transfers
```

---

# 9.3 — Verilog Modeling Styles

Four important modeling styles:

| Style      | Main Idea                     |
| ---------- | ----------------------------- |
| Gate-level | Gates                         |
| Dataflow   | Equations                     |
| Behavioral | Algorithm/procedure           |
| Structural | Connecting modules/components |

### Example

```text
Gate-level → and, or, not
Dataflow   → assign
Behavioral → always
Structural → module instantiation
```

---

# 9.4 — Gate-Level Modeling

Describes hardware using primitive gates.

### Common gates

```text
and
or
not
nand
nor
xor
xnor
buf
```

### Example

```verilog
and (y, a, b);
```

Conceptually:

```text
a ──┐
    AND ── y
b ──┘
```

### Key point

> Gate-level modeling is closest to the actual gate structure.

---

# 9.5 — Dataflow Modeling

Describes how data flows using Boolean expressions.

Main construct:

```verilog
assign
```

Example:

```verilog
assign y = a & b;
```

### Key point

```text
Dataflow
   ↓
Boolean expression
   ↓
Continuous assignment
```

---

# 9.6 — Behavioral Modeling

Describes **what the hardware should do** rather than explicitly describing gates.

Main construct:

```verilog
always
```

Example:

```verilog
always @(*) begin
    if (sel)
        y = a;
    else
        y = b;
end
```

### Used for

* ALU
* FSM
* Counters
* MUX
* Control logic

---

# 9.7 — Structural Modeling

Describes hardware by connecting smaller components/modules.

Example:

```verilog
module top(...);

module1 u1(...);
module2 u2(...);

endmodule
```

### Key idea

```text
Small blocks
     ↓
Connected together
     ↓
Larger system
```

### Remember

> Structural modeling describes **how components are connected**.

---

# 9.8 — Verilog Modules & Ports

A **module** is the basic building block of a Verilog design.

Example:

```verilog
module and_gate (
    input  a,
    input  b,
    output y
);

assign y = a & b;

endmodule
```

### Port directions

```text
input
output
inout
```

### Remember

```text
module = hardware block
```

---

# 9.9 — Verilog Data Types

Important types:

```text
wire
reg
integer
parameter
```

### `wire`

Used for nets/connections.

```verilog
wire y;
```

### `reg`

Used for values assigned inside procedural blocks in traditional Verilog.

```verilog
reg y;
```

> Important: `reg` does **not automatically mean a physical register**.

### 4-state logic

```text
0 → Logic 0
1 → Logic 1
X → Unknown
Z → High impedance
```

### Remember

```text
0, 1, X, Z
```

---

# 9.10 — Verilog Operators

### Arithmetic

```text
+  -  *  /  %
```

### Relational

```text
<  >  <=  >=
```

### Equality

```text
==  !=
=== !==
```

### Logical

```text
&&  ||  !
```

### Bitwise

```text
&  |  ^  ~
```

### Shift

```text
<<  >>
```

### Conditional

```text
condition ? true_value : false_value
```

### Important

```text
==  → logical equality
=== → case equality, considers X/Z
```

---

# 9.11 — Continuous Assignment

Main keyword:

```verilog
assign
```

Example:

```verilog
assign y = a & b;
```

### Properties

* Continuous
* Used mainly for combinational logic
* Typically drives nets

### Remember

```text
assign → continuous assignment
```

---

# 9.12 — Procedural Blocks

Main procedural blocks:

```text
always
initial
```

### `always`

Used for repeatedly executing RTL behavior.

Example:

```verilog
always @(*) begin
    y = a & b;
end
```

### `initial`

Starts once at simulation time zero.

Generally used for:

* Testbenches
* Simulation initialization

### Remember

```text
always  → repeatedly executes
initial → executes once
```

---

# 9.13 — Blocking vs Nonblocking

## Blocking

```text
=
```

Statements execute sequentially.

Commonly used for:

```text
Combinational logic
```

Example:

```verilog
always @(*) begin
    y = a;
end
```

---

## Nonblocking

```text
<=
```

Updates occur without immediately affecting subsequent statements in the same procedural block.

Commonly used for:

```text
Sequential/clocked logic
```

Example:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

### Golden rule

```text
Combinational → =
Sequential   → <=
```

---

# 9.14 — Conditional Statements

### `if`

```verilog
if (condition)
    statement;
```

### `if-else`

```verilog
if (condition)
    y = a;
else
    y = b;
```

### `case`

```verilog
case (sel)
    2'b00: y = a;
    2'b01: y = b;
endcase
```

### Important

Incomplete assignments in combinational logic can infer latches.

---

# 9.15 — Loops

Common loops:

```text
for
while
repeat
forever
```

### `for`

Most commonly used for synthesizable repetitive hardware.

```verilog
for (i = 0; i < 8; i = i + 1)
```

### Important

A **static/bounded loop can be synthesized** by unrolling it into hardware.

### Remember

> Loops are not automatically non-synthesizable.

---

# 9.16 — Arrays & Memories

Arrays are used to represent collections of values.

Example:

```verilog
reg [7:0] memory [0:255];
```

This represents:

```text
256 locations
×
8 bits
```

### Important

```text
reg [7:0] → each element is 8 bits
[0:255]   → 256 elements
```

### Memory concept

```text
Address
   ↓
Memory
   ↓
Data
```

---

# 9.17 — Functions & Tasks

## Function

Used to perform a calculation and return a value.

```verilog
function [3:0] add;
input [3:0] a;
input [3:0] b;

begin
    add = a + b;
end

endfunction
```

### Function

* Returns a value
* Traditionally executes without timing controls
* Useful for reusable calculations

---

## Task

Used for reusable procedural operations.

```text
Task
```

→ can have multiple outputs

→ can contain timing controls

→ does not have to return a single value

### Remember

```text
Function → returns value
Task     → procedural operation
```

---

# 9.18 — Parameters & `localparam`

### Parameter

Used to define configurable constants.

```verilog
parameter WIDTH = 8;
```

Example:

```verilog
module counter #(parameter WIDTH = 8);
```

### `localparam`

Used for internal constants that should not be overridden externally.

Example:

```verilog
localparam IDLE = 2'b00;
```

### Difference

```text
parameter
→ can generally be overridden

localparam
→ cannot normally be overridden externally
```

---

# 9.19 — Compiler / Preprocessor Directives

Common directives:

```text
`define
`include
`ifdef
`ifndef
`else
`endif
```

### Example

```verilog
`define WIDTH 8
```

Then:

```verilog
reg [`WIDTH-1:0] data;
```

### Conditional compilation

```verilog
`ifdef DEBUG
    ...
`endif
```

### Remember

> Directives are processed before normal compilation/synthesis.

---

# 9.20 — Generate Blocks

Generate constructs are used to create hardware **during elaboration**.

Example:

```verilog
genvar i;

generate
    for (i = 0; i < 8; i = i + 1) begin
        ...
    end
endgenerate
```

### Common uses

* Repeated hardware
* Parameterized designs
* Multiple instances
* Conditional hardware generation

### Key distinction

```text
generate loop
→ hardware generation/elaboration

procedural loop
→ procedural behavior
```

---

# 9.21 — `case`, `casez`, `casex`, `unique`, `priority`

## `case`

Exact matching.

```verilog
case (sel)
```

---

## `casez`

Treats `Z` and often `?` as don't-care matching bits.

Useful for:

```text
Priority/decoder-style logic
```

---

## `casex`

Treats `X` and `Z` as don't-care.

⚠️ Generally discouraged in RTL because it can hide unknown (`X`) values during simulation.

---

## `unique`

Indicates that the designer expects a unique matching case item.

---

## `priority`

Indicates priority behavior among matching conditions.

### Quick comparison

| Construct  | Main idea                |
| ---------- | ------------------------ |
| `case`     | Exact matching           |
| `casez`    | Z/? don't-care matching  |
| `casex`    | X/Z don't-care matching  |
| `unique`   | Expect one matching item |
| `priority` | Priority among matches   |

### Placement tip

> **Avoid** **`casex`** **in robust RTL because X values can be masked.**

---

# 9.22 — Combinational & Sequential RTL Coding

## Combinational

Output depends on current inputs.

```verilog
always @(*) begin
    y = a & b;
end
```

### Typical

```text
always @(*)
=
```

Examples:

* MUX
* Decoder
* Encoder
* Adder
* ALU
* Comparator

---

## Sequential

Depends on current inputs and stored state.

```verilog
always @(posedge clk) begin
    q <= d;
end
```

### Typical

```text
clock
+
<=
```

Examples:

* Flip-flop
* Register
* Counter
* Shift register
* FSM

### Golden rule

```text
Combinational → always @(*) + =
Sequential   → posedge clk + <=
```

---

# 9.23 — Latch Inference & Avoiding Unintended Latches

### What is latch inference?

When RTL implies that a signal must retain its previous value, synthesis may create a latch.

Problem:

```verilog
always @(*) begin
    if (enable)
        y = a;
end
```

When:

```text
enable = 0
```

`y` has no new assignment.

Therefore it must retain its previous value.

→ **Latch**

---

## Fix 1 — `else`

```verilog
always @(*) begin
    if (enable)
        y = a;
    else
        y = 0;
end
```

## Fix 2 — Default assignment

```verilog
always @(*) begin
    y = 0;

    if (enable)
        y = a;
end
```

## Fix 3 — `default` in case

```verilog
case (sel)
    2'b00: y = a;
    2'b01: y = b;
    default: y = 0;
endcase
```

### Remember

```text
Incomplete combinational assignment
                ↓
        Possible latch
```

### Latch vs FF

```text
Latch     → level-sensitive
Flip-flop → edge-triggered
```

---

# 9.24 — Synthesizable vs Non-Synthesizable Verilog

## Synthesizable

Can be converted into hardware.

Examples:

```text
assign
always @(*)
always @(posedge clk)
if/else
case
static for loops
arithmetic
comparisons
generate
module instantiation
```

---

## Non-synthesizable

Primarily used for simulation/verification.

Examples:

```text
#delay
$display
$monitor
$finish
file operations
wait
fork...join
```

### `initial`

Generally non-synthesizable for ASIC RTL, though some FPGA tools support certain initialization constructs.

### Golden rule

```text
Synthesizable
      ↓
Hardware

Non-synthesizable
      ↓
Simulation / Verification
```

---

# 🔥 PHASE 9 — MOST IMPORTANT INTERVIEW RULES

Memorize these:

### 1. Combinational RTL

```verilog
always @(*) begin
    ...
end
```

Use:

```text
blocking =
```

---

### 2. Sequential RTL

```verilog
always @(posedge clk) begin
    ...
end
```

Use:

```text
nonblocking <=
```

---

### 3. Latch

```text
Level-sensitive storage
```

---

### 4. Flip-flop

```text
Edge-triggered storage
```

---

### 5. Latch inference

```text
Incomplete combinational assignment
```

---

### 6. Avoid latch

```text
Default assignment
```

*

else

*

case default

---

### 7. Continuous assignment

```verilog
assign y = expression;
```

---

### 8. `reg` does NOT mean register

In traditional Verilog:

```text
reg = procedural variable
```

It becomes physical combinational or sequential hardware depending on how it is used.

---

### 9. `for` loop can be synthesizable

Static bounded loops can be **unrolled into hardware**.

---

### 10. `casex`

Avoid when possible because it can mask unknown `X` values.

---

### 11. `parameter` vs `localparam`

```text
parameter  → configurable
localparam → internal constant
```

---

### 12. RTL vs Testbench

```text
RTL
```

→ describes hardware

```text
Testbench
```

→ verifies hardware

---

# ⚡ 30-SECOND PHASE 9 REVISION

```text
VERILOG
│
├── Modeling
│   ├── Gate-level
│   ├── Dataflow
│   ├── Behavioral
│   └── Structural
│
├── Combinational
│   ├── always @(*)
│   ├── blocking =
│   └── MUX / ALU / Decoder / Adder
│
├── Sequential
│   ├── posedge/negedge
│   ├── nonblocking <=
│   └── FF / Register / Counter / FSM
│
├── Latch
│   ├── Level-sensitive
│   └── Incomplete assignment
│
├── FSM
│   ├── State register
│   ├── Next-state logic
│   └── Output logic
│
├── Parameters
│   ├── parameter
│   └── localparam
│
├── Generate
│   └── Hardware generation
│
└── Synthesis
    ├── Synthesizable → Hardware
    └── Non-synthesizable → Simulation
```

# ⭐ Ultimate Placement Cheat Sheet

| Question                  | Answer                              |
| ------------------------- | ----------------------------------- |
| Verilog is?               | HDL                                 |
| RTL means?                | Register Transfer Level             |
| Continuous assignment?    | `assign`                            |
| Combinational block?      | `always @(*)`                       |
| Sequential block?         | `always @(posedge clk)`             |
| Combinational assignment? | `=`                                 |
| Sequential assignment?    | `<=`                                |
| MUX?                      | Combinational                       |
| Counter?                  | Sequential                          |
| Flip-flop?                | Edge-triggered                      |
| Latch?                    | Level-sensitive                     |
| Latch caused by?          | Incomplete combinational assignment |
| Latch prevention?         | Complete assignments/default        |
| `casez`?                  | Z/? matching                        |
| `casex`?                  | X/Z treated as don't-care           |
| `parameter`?              | Configurable constant               |
| `localparam`?             | Internal constant                   |
| `generate`?               | Elaborates/generates hardware       |
| `#10`?                    | Generally non-synthesizable         |
| `$display`?               | Simulation                          |
| `$finish`?                | Simulation                          |
| Static `for`?             | Can be synthesizable                |
| `reg` means register?     | ❌ No                                |
| RTL describes?            | Hardware                            |
| Testbench describes?      | Verification                        |
| Synthesis produces?       | Gate-level netlist                  |

## 🏆 Phase 9 Final Memory Formula

```text
RTL
→ Simulation
→ Synthesis
→ Hardware

Combinational
→ always @(*)
→ =

Sequential
→ posedge clk
→ <=

Incomplete assignment
→ Latch

Synthesizable RTL
→ Hardware
```
