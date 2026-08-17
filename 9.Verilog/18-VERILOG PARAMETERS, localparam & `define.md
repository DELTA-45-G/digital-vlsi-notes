# VERILOG PARAMETERS, `localparam` & `` `define``

## ⭐⭐⭐⭐⭐ Placement Important

Parameters and macros are used to make Verilog designs **configurable, reusable, and easier to maintain**.

The three important concepts are:

```text
parameter
localparam
`define
```

---

# 1. What is a Parameter?

A **parameter** is a constant value that can be used to configure a module.

Unlike a normal variable, a parameter does not change during simulation.

Example:

```verilog
module counter #(
    parameter WIDTH = 8
)(
    input clk,
    input reset,
    output reg [WIDTH-1:0] count
);

always @(posedge clk) begin
    if (reset)
        count <= 0;
    else
        count <= count + 1;
end

endmodule
```

Here:

```text
WIDTH = 8
```

determines the counter size.

---

# 2. Why Use Parameters?

Without parameters:

```verilog
reg [7:0] count;
```

The counter is fixed at 8 bits.

With:

```verilog
parameter WIDTH = 8;
```

you can create:

```text
8-bit counter
16-bit counter
32-bit counter
64-bit counter
```

using the same module.

### Main advantage:

> **Parameterization allows one RTL module to be reused with different configurations.**

---

# 3. Parameterized Module ⭐⭐⭐⭐⭐

Example:

```verilog
module adder #(
    parameter WIDTH = 8
)(
    input  [WIDTH-1:0] a,
    input  [WIDTH-1:0] b,
    output [WIDTH:0] sum
);

assign sum = a + b;

endmodule
```

Default:

```text
WIDTH = 8
```

So:

```text
a   → 8 bits
b   → 8 bits
sum → 9 bits
```

---

# 4. Overriding a Parameter

Suppose:

```verilog
module counter #(
    parameter WIDTH = 8
);
```

You can instantiate it with a different width.

Example:

```verilog
counter #(.WIDTH(16)) c1 (
    .clk(clk),
    .reset(reset),
    .count(count)
);
```

Now:

```text
WIDTH = 16
```

instead of the default 8.

---

# 5. Why Parameter Override Is Useful

One module:

```text
Counter
```

can be configured as:

```text
WIDTH = 8
WIDTH = 16
WIDTH = 32
```

without rewriting the module.

This is very important in reusable RTL design.

---

# 6. Parameter vs Variable ⭐⭐⭐⭐⭐

| Parameter                              | Variable                  |
| -------------------------------------- | ------------------------- |
| Constant                               | Can change                |
| Used for configuration                 | Used for runtime behavior |
| Generally determined before simulation | Changes during simulation |
| Commonly controls widths/depths        | Stores changing data      |
| Used heavily in parameterized RTL      | Used in procedural logic  |

### Memory trick:

```text
parameter → design configuration
variable  → changing value
```

---

# 7. Parameter Is Not a Register

Consider:

```verilog
parameter WIDTH = 8;
```

This does **not** create:

```text
8-bit register
```

It simply provides a constant value that can be used during elaboration/RTL construction.

---

# 8. Parameter and Hardware ⭐⭐⭐⭐⭐

Consider:

```verilog
module mux #(
    parameter WIDTH = 8
);
```

The parameter may determine the width of the hardware.

For example:

```text
WIDTH = 8
   ↓
8-bit MUX

WIDTH = 32
   ↓
32-bit MUX
```

The parameter itself is not runtime hardware.

---

# 9. Parameter for Memory Depth

Example:

```verilog
module memory #(
    parameter DATA_WIDTH = 8,
    parameter DEPTH = 256
);

reg [DATA_WIDTH-1:0] mem [0:DEPTH-1];

endmodule
```

This makes both:

```text
Data width
Memory depth
```

configurable.

---

# 10. Address Width Using Parameter

Suppose:

```verilog
parameter DEPTH = 256;
```

Address width can be calculated using:

```verilog
$clog2(DEPTH)
```

Example:

```verilog
parameter DEPTH = 256;
localparam ADDR_WIDTH = $clog2(DEPTH);
```

Then:

```verilog
input [ADDR_WIDTH-1:0] addr;
```

For:

```text
DEPTH = 256
```

we get:

```text
ADDR_WIDTH = log2(256) = 8
```

---

# 11. What is `localparam`?

`localparam` is a parameter whose value **cannot normally be overridden from outside the module**.

Example:

```verilog
module counter #(
    parameter WIDTH = 8
);

localparam MAX_COUNT = (1 << WIDTH) - 1;

endmodule
```

Here:

```text
WIDTH → externally configurable
MAX_COUNT → internally defined
```

---

# 12. Parameter vs `localparam` ⭐⭐⭐⭐⭐

| `parameter`                    | `localparam`                  |
| ------------------------------ | ----------------------------- |
| Can be overridden              | Cannot normally be overridden |
| Used for module configuration  | Used for internal constants   |
| External customization allowed | Internal design constant      |
| Example: WIDTH                 | Example: state encoding       |

### Memory trick:

```text
parameter  → outside can configure
localparam → local/internal constant
```

---

# 13. Why Use `localparam`?

Suppose you define FSM states:

```verilog
localparam IDLE  = 2'b00;
localparam START = 2'b01;
localparam DONE  = 2'b10;
```

You don't want another module to accidentally override these state values.

Therefore:

```text
localparam
```

is appropriate.

---

# 14. `localparam` in FSMs ⭐⭐⭐⭐⭐

Example:

```verilog
localparam IDLE = 2'b00;
localparam LOAD = 2'b01;
localparam EXEC = 2'b10;
localparam DONE = 2'b11;
```

These are internal constants.

Typical use:

```verilog
case (state)
    IDLE:  ...
    LOAD:  ...
    EXEC:  ...
    DONE:  ...
endcase
```

---

# 15. What is `` `define``?

`` `define`` is a **Verilog preprocessor macro directive**.

Example:

```verilog
`define WIDTH 8
```

Then:

```verilog
reg [`WIDTH-1:0] data;
```

The preprocessor substitutes:

```text
`WIDTH
```

with:

```text
8
```

before compilation.

---

# 16. Important: Backtick Symbol

The syntax is:

```text
`define
```

Notice the character:

```text
`
```

This is a **backtick**, not a single quote.

Correct:

```verilog
`define WIDTH 8
```

Incorrect:

```text
#define WIDTH 8
```

---

# 17. `define` Example

```verilog
`define DATA_WIDTH 8

module test;

reg [`DATA_WIDTH-1:0] data;

endmodule
```

The preprocessor effectively substitutes:

```text
`DATA_WIDTH
```

with:

```text
8
```

---

# 18. `define` Can Define Expressions

Example:

```verilog
`define MAX_VALUE 255
```

Then:

```verilog
if (data == `MAX_VALUE)
```

can be used.

---

# 19. `define` Can Define Macros

It doesn't have to be just a number.

Example:

```verilog
`define ADD(a,b) ((a)+(b))
```

Then:

```verilog
assign y = `ADD(a,b);
```

The preprocessor expands the macro.

---

# 20. `define` Is Textual Substitution ⭐⭐⭐⭐⭐

This is an important difference.

When you write:

```verilog
`define WIDTH 8
```

the preprocessor performs **text substitution**.

It is not the same concept as a parameter.

### Memory trick:

```text
parameter → elaboration/configuration
`define   → preprocessor text substitution
```

---

# 21. Parameter vs `define` ⭐⭐⭐⭐⭐

| Parameter                                             | `` `define``                                               |
| ----------------------------------------------------- | ---------------------------------------------------------- |
| Module/design parameter                               | Preprocessor macro                                         |
| Can be overridden during module instantiation         | Textual substitution                                       |
| Scope is associated with parameter declaration/module | Preprocessor scope rules                                   |
| Commonly used for configurable hardware               | Commonly used for constants/macros/conditional compilation |
| More suitable for module configuration                | More general text substitution                             |

---

# 22. Example — Parameter

```verilog
module adder #(
    parameter WIDTH = 8
);
```

Instantiation:

```verilog
adder #(.WIDTH(16)) a1 (...);
```

The module can be customized.

---

# 23. Example — `define

```verilog
`define WIDTH 8

module adder (...);

reg [`WIDTH-1:0] data;

endmodule
```

The macro is replaced by the preprocessor.

You don't normally override it through:

```verilog
adder #(...);
```

---

# 24. Parameter vs `localparam` vs `define`

### `parameter`

```text
Configurable constant
```

### `localparam`

```text
Internal non-overridable constant
```

### `` `define``

```text
Preprocessor macro/text substitution
```

---

# 25. Very Important Interview Question ⭐⭐⭐⭐⭐

### Which one should be used for configurable module width?

Prefer:

```text
parameter
```

Example:

```verilog
parameter WIDTH = 8;
```

---

# 26. Which One for FSM State Constants?

Prefer:

```text
localparam
```

Example:

```verilog
localparam IDLE = 2'b00;
```

---

# 27. Which One for Preprocessor Macros?

Use:

```text
`define
```

Example:

```verilog
`define TRUE 1'b1
```

---

# 28. `$clog2` ⭐⭐⭐⭐⭐

`$clog2` returns the ceiling of the base-2 logarithm.

Example:

```verilog
$clog2(8)
```

gives:

```text
3
```

because:

```text
2³ = 8
```

---

# 29. `$clog2` Examples

```text
$clog2(2)   = 1
$clog2(4)   = 2
$clog2(8)   = 3
$clog2(16)  = 4
$clog2(32)  = 5
```

For a non-power-of-two:

```text
$clog2(5) = 3
```

because:

```text
2² = 4 < 5
```

and:

```text
2³ = 8 ≥ 5
```

---

# 30. Parameterized Memory Example ⭐⭐⭐⭐⭐

```verilog
module memory #(
    parameter DATA_WIDTH = 8,
    parameter DEPTH = 256
)(
    input [DATA_WIDTH-1:0] data_in,
    input [$clog2(DEPTH)-1:0] addr,
    input clk,
    input we
);

reg [DATA_WIDTH-1:0] mem [0:DEPTH-1];

always @(posedge clk) begin
    if (we)
        mem[addr] <= data_in;
end

endmodule
```

Now the same module can represent different memories.

Example:

```text
DATA_WIDTH = 8
DEPTH = 256
```

or:

```text
DATA_WIDTH = 32
DEPTH = 1024
```

---

# 31. Parameterized Counter Example

```verilog
module counter #(
    parameter WIDTH = 8
)(
    input clk,
    input reset,
    output reg [WIDTH-1:0] count
);

always @(posedge clk) begin
    if (reset)
        count <= 0;
    else
        count <= count + 1;
end

endmodule
```

Instantiation:

```verilog
counter #(.WIDTH(16)) c1 (
    .clk(clk),
    .reset(reset),
    .count(count)
);
```

This produces a:

```text
16-bit counter
```

---

# 32. Parameterized FIFO Concept

A FIFO can have:

```text
DATA_WIDTH
DEPTH
```

as parameters.

Example:

```verilog
module fifo #(
    parameter DATA_WIDTH = 8,
    parameter DEPTH = 16
);
```

Now the same FIFO architecture can be reused with different configurations.

This is a major real-world RTL design technique.

---

# 33. Can a Parameter Change During Simulation?

❌ No.

A parameter is a constant used to configure the design.

It is not a runtime variable.

---

# 34. Can `localparam` Be Overridden?

Normally:

❌ No.

That is one of the main reasons to use `localparam`.

---

# 35. Is `define` a Runtime Constant?

❌ No.

`` `define`` is processed by the **preprocessor** before compilation.

---

# 36. Conditional Compilation with `define`

One important use of `` `define`` is conditional compilation.

Example:

```verilog
`define DEBUG
```

Then:

```verilog
`ifdef DEBUG

$display("Debug mode");

`endif
```

If `DEBUG` is defined, the code between:

```text
`ifdef
```

and:

```text
`endif
```

is included.

---

# 37. `ifdef` ⭐⭐⭐⭐

`ifdef` means:

> Compile the following code if the specified macro is defined.

Example:

```verilog
`ifdef DEBUG

$display("Debug enabled");

`endif
```

---

# 38. `ifndef`

`ifndef` means:

> Compile the following code if the specified macro is **not** defined.

Example:

```verilog
`ifndef SYNTHESIS

$display("Simulation only");

`endif
```

---

# 39. `else` with Conditional Compilation

Example:

```verilog
`ifdef DEBUG

$display("Debug mode");

`else

$display("Normal mode");

`endif
```

This is handled by the preprocessor.

---

# 40. Why Conditional Compilation Is Useful

It can be used to:

* Enable debug code
* Select simulation-only code
* Control compilation options
* Support different configurations
* Exclude code from synthesis

Example:

```verilog
`ifndef SYNTHESIS
// simulation-only code
`endif
```

---

# ⭐ Frequently Asked Placement Questions

## Q1. What is a parameter?

**Answer:** A parameter is a constant used to configure a Verilog module and make the design reusable.

---

## Q2. Can a parameter be changed during simulation?

**Answer:** No. It is a design/elaboration-time constant.

---

## Q3. Why are parameters used?

**Answer:**

* Parameterize hardware
* Reuse modules
* Change width/depth/configuration
* Avoid duplicated RTL

---

## Q4. What is `localparam`?

**Answer:** `localparam` defines a local constant that cannot normally be overridden from outside the module.

---

## Q5. Difference between parameter and localparam?

**Answer:**

```text
parameter  → externally configurable
localparam → internally fixed
```

---

## Q6. Where is `localparam` commonly used?

**Answer:** FSM state definitions, internal constants, calculated widths, and other constants that should not be externally configurable.

---

## Q7. What is `` `define``?

**Answer:** It is a Verilog preprocessor directive used for textual macro substitution.

---

## Q8. What is the difference between `parameter` and `` `define``?

**Answer:**

```text
parameter → module/design configuration
`define   → preprocessor text substitution
```

---

## Q9. Which is preferred for configurable module width?

**Answer:**

```text
parameter
```

---

## Q10. Which is preferred for FSM state constants?

**Answer:**

```text
localparam
```

---

## Q11. What does `$clog2` do?

**Answer:** It returns the ceiling of the base-2 logarithm of its argument.

---

## Q12. What is `$clog2(16)`?

**Answer:**

```text
4
```

---

## Q13. What is `$clog2(10)`?

**Answer:**

```text
2³ = 8 < 10
2⁴ = 16 ≥ 10
```

Therefore:

```text
4
```

---

## Q14. What is `$clog2(256)`?

**Answer:**

```text
8
```

---

## Q15. What is the purpose of `ifdef`?

**Answer:** It conditionally includes code when a specified macro is defined.

---

## Q16. What does `ifndef` mean?

**Answer:** Include the code only if the specified macro is not defined.

---

## Q17. What is conditional compilation?

**Answer:** It is the process of including or excluding source code based on preprocessor directives such as `ifdef and `ifndef.

---

## Q18. Does a parameter itself create hardware?

**Answer:** No. It configures the hardware description; the resulting RTL determines the synthesized hardware.

---

# 🔥 Placement Rapid-Fire

**Configurable module constant?**

→ `parameter`

**Internal fixed constant?**

→ `localparam`

**Preprocessor macro?**

→ `` `define``

**Parameter can change at runtime?**

→ ❌ No

**`localparam` externally overrideable?**

→ ❌ Normally no

**`$clog2(8)`?**

→ 3

**`$clog2(10)`?**

→ 4

**`$clog2(16)`?**

→ 4

**`$clog2(256)`?**

→ 8

**FSM state constants?**

→ `localparam`

**Parameterized counter width?**

→ `parameter`

**Hex/binary constants using macro?**

→ `` `define`` can be used

**Conditional compilation?**

→ `` `ifdef / `ifndef``

**Preprocessor operates before compilation?**

→ ✅ Yes

---

# 🧠 9.18 QUICK REVISION

```text
                CONSTANTS & CONFIGURATION
                          │
          ┌───────────────┼────────────────┐
          ↓               ↓                ↓
      parameter       localparam        `define
          │               │                │
     configurable      internal        preprocessor
       constant         constant           macro
          │               │                │
     module width      FSM states       text substitution
     memory depth      fixed values      conditional code
```

### ⭐ Remember

```text
parameter
    ↓
Can configure module
```

```text
localparam
    ↓
Internal constant
```

```text
`define
    ↓
Preprocessor macro
```

```text
$clog2(N)
    ↓
ceil(log2(N))
```

### Golden Rules

```text
parameter → configurable constant
localparam → internal constant
`define → preprocessor macro
$clog2(N) = ⌈log2(N)⌉
Parameter ≠ runtime variable
```
