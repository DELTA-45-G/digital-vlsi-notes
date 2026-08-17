# VERILOG COMPILER DIRECTIVES & PREPROCESSOR DIRECTIVES

## ⭐⭐⭐⭐ Placement Important

Compiler directives are instructions given to the **Verilog preprocessor/compiler** that control how the Verilog source code is processed.

They are identified by a **backtick (`)**.

Examples:

```text
`define
`include
`ifdef
`ifndef
`else
`endif
`timescale
```

---

# 1. What is a Compiler Directive?

A compiler directive is a command that affects how Verilog code is interpreted or processed.

Example:

```verilog
`timescale 1ns/1ps
```

This does not describe hardware directly.

Instead, it tells the simulator how to interpret:

* simulation time units
* simulation time precision

---

# 2. Important Compiler Directives

For placement preparation, focus on:

| Directive             | Purpose                               |
| --------------------- | ------------------------------------- |
| `` `define``          | Define macro                          |
| `` `undef``           | Remove macro definition               |
| `` `include``         | Include another Verilog file          |
| `` `ifdef``           | Compile if macro is defined           |
| `` `ifndef``          | Compile if macro is not defined       |
| `` `else``            | Alternative conditional section       |
| `` `elsif``           | Else-if condition                     |
| `` `endif``           | End conditional compilation           |
| `` `timescale``       | Define simulation time unit/precision |
| `` `default_nettype`` | Control default net type              |

---

# 3. `` `define``

Used to define a macro.

Example:

```verilog
`define WIDTH 8
```

Usage:

```verilog
reg [`WIDTH-1:0] data;
```

The preprocessor replaces:

```text
`WIDTH
```

with:

```text
8
```

---

# 4. `` `undef``

Used to **remove an existing macro definition**.

Example:

```verilog
`define WIDTH 8
```

```verilog
`undef WIDTH
```

After:

```verilog
`undef WIDTH
```

the macro `WIDTH` is no longer defined.

### Placement point ⭐

```text
`define → define macro
`undef  → remove macro
```

---

# 5. `` `include`` ⭐⭐⭐⭐⭐

Used to include the contents of another source file.

Example:

```verilog
`include "definitions.v"
```

The preprocessor effectively inserts the contents of:

```text
definitions.v
```

into the current source file.

---

# 6. Why Use `` `include``?

It helps share:

* Macro definitions
* Common constants
* Common declarations
* Testbench utilities

Example:

```text
project/
│
├── design.v
├── definitions.v
└── testbench.v
```

Inside `design.v`:

```verilog
`include "definitions.v"
```

---

# 7. `` `include`` vs Module Instantiation ⭐⭐⭐⭐⭐

These are completely different.

### `` `include``

```verilog
`include "file.v"
```

means:

> Insert the contents of the file during preprocessing.

### Module instantiation

```verilog
alu u1 (...);
```

means:

> Instantiate a hardware module.

### Memory trick:

```text
`include → source-code inclusion
module instantiation → hardware hierarchy
```

---

# 8. `` `ifdef`` ⭐⭐⭐⭐⭐

`ifdef means:

> Compile the code only if the specified macro is defined.

Example:

```verilog
`define DEBUG

`ifdef DEBUG

$display("Debug mode");

`endif
```

Because `DEBUG` is defined, the code is included.

---

# 9. `` `ifndef``

`ifndef means:

> Compile the code only if the specified macro is NOT defined.

Example:

```verilog
`ifndef DEBUG

$display("Debug disabled");

`endif
```

If `DEBUG` is not defined, the code is included.

---

# 10. `` `else``

Used with conditional compilation.

Example:

```verilog
`ifdef DEBUG

$display("Debug mode");

`else

$display("Normal mode");

`endif
```

If `DEBUG` exists:

```text
Debug mode
```

Otherwise:

```text
Normal mode
```

---

# 11. `` `elsif``

Used for an additional conditional branch.

Example:

```verilog
`ifdef MODE_A

// Mode A

`elsif MODE_B

// Mode B

`else

// Default mode

`endif
```

Think of it as:

```text
if
else if
else
```

but for preprocessor conditions.

---

# 12. `` `endif``

Marks the end of a conditional compilation block.

Example:

```verilog
`ifdef DEBUG

$display("Debug");

`endif
```

The structure is:

```text
`ifdef
   ↓
code
   ↓
`endif
```

---

# 13. Conditional Compilation Example ⭐⭐⭐⭐⭐

```verilog
`define SIMULATION

module test;

`ifdef SIMULATION

initial begin
    $display("Simulation mode");
end

`endif

endmodule
```

If `SIMULATION` is defined, the initial block is included.

---

# 14. Simulation vs Synthesis

Conditional compilation is often used to separate:

```text
Simulation code
```

from:

```text
Synthesizable RTL
```

Example:

```verilog
`ifndef SYNTHESIS

initial begin
    $display("Simulation only");
end

`endif
```

The intent is to exclude that code when a synthesis tool defines `SYNTHESIS`.

---

# 15. What is `` `timescale``? ⭐⭐⭐⭐⭐

`timescale specifies:

```text
time unit
time precision
```

Syntax:

```verilog
`timescale time_unit / time_precision
```

Example:

```verilog
`timescale 1ns/1ps
```

Meaning:

```text
1 ns → simulation time unit
1 ps → simulation time precision
```

---

# 16. Understanding `1ns/1ps`

Consider:

```verilog
`timescale 1ns/1ps
```

### Time unit

```text
1ns
```

means a delay of:

```text
#1
```

represents:

```text
1 ns
```

### Precision

```text
1ps
```

means simulation time can be represented with a precision of 1 ps.

---

# 17. Example of `timescale`

```verilog
`timescale 1ns/1ps

module test;

initial begin
    #10;
end

endmodule
```

Here:

```text
#10 = 10 ns
```

---

# 18. Another `timescale` Example

```verilog
`timescale 10ns/1ns
```

Then:

```text
#2
```

means:

```text
2 × 10ns = 20ns
```

---

# 19. Time Unit vs Precision ⭐⭐⭐⭐⭐

This is frequently asked.

For:

```verilog
`timescale 1ns/1ps
```

```text
1ns → time unit
1ps → time precision
```

### Easy memory:

```text
`timescale UNIT / PRECISION
```

---

# 20. Why Is Time Precision Important?

Suppose:

```verilog
`timescale 1ns/1ps
```

and you specify:

```text
#0.001
```

The simulator handles the delay according to the specified time precision.

The precision determines how finely simulation time is represented/rounded.

---

# 21. `` `default_nettype`` ⭐⭐⭐⭐

This directive controls the default net type for undeclared identifiers.

Historically, Verilog can implicitly create a wire when an undeclared signal is used.

Example:

```verilog
assign y = a & b;
```

If `y` wasn't explicitly declared, Verilog may implicitly treat it as a net under the default rules.

This can cause accidental signal declarations.

---

# 22. Preventing Implicit Nets

A common practice is:

```verilog
`default_nettype none
```

This disables implicit net declarations.

Then signals should be explicitly declared.

Example:

```verilog
`default_nettype none

module test(
    input wire a,
    input wire b,
    output wire y
);

assign y = a & b;

endmodule
```

---

# 23. Why Use `` `default_nettype none``? ⭐⭐⭐⭐⭐

It helps catch:

* Typographical mistakes
* Misspelled signal names
* Undeclared signals
* Accidental implicit wires

Example:

```verilog
assign output_signal = input_singal;
```

Suppose the actual signal is:

```text
input_signal
```

Without strict net checking, a typo may accidentally create a new implicit net.

With:

```verilog
`default_nettype none
```

the compiler can report the undeclared signal.

---

# 24. Restoring Default Net Type

After using:

```verilog
`default_nettype none
```

you can restore the default behavior using:

```verilog
`default_nettype wire
```

Example:

```verilog
`default_nettype none

module test;
    ...
endmodule

`default_nettype wire
```

This is useful when included files or other source code depend on the default net behavior.

---

# 25. `` `default_nettype none`` — Interview Question

### Why do designers use it?

**Answer:**

To prevent accidental implicit nets caused by undeclared or misspelled signal names.

---

# 26. Compiler Directives Don't Usually Create Hardware

For example:

```verilog
`define WIDTH 8
```

does not create an 8-bit hardware block.

Similarly:

```verilog
`ifdef DEBUG
```

does not itself create hardware.

These directives control **source-code processing**.

---

# 27. Preprocessor Flow ⭐⭐⭐⭐⭐

A simplified flow is:

```text
Verilog Source
      ↓
Preprocessor
      ↓
`define
`include
`ifdef
`timescale
      ↓
Processed Verilog
      ↓
Compiler
      ↓
Simulation / Synthesis
```

This is why compiler directives are conceptually different from RTL statements.

---

# 28. Macro vs Compiler Directive

A macro such as:

```verilog
`define WIDTH 8
```

is itself a compiler/preprocessor directive.

The macro name:

```text
WIDTH
```

can then be substituted throughout the source.

---

# 29. Common Mistake — Single Quote vs Backtick

### Correct:

```verilog
`define WIDTH 8
```

### Backtick:

```text
`
```

### Not:

```text
'
```

This distinction is frequently important when writing Verilog.

---

# 30. Example Combining Multiple Directives

```verilog
`timescale 1ns/1ps

`default_nettype none

`define WIDTH 8

module adder(
    input  wire [`WIDTH-1:0] a,
    input  wire [`WIDTH-1:0] b,
    output wire [`WIDTH:0] sum
);

assign sum = a + b;

endmodule

`default_nettype wire
```

Here we use:

```text
`timescale
`default_nettype
`define
```

together.

---

# ⭐ Frequently Asked Placement Questions

## Q1. What is a compiler directive in Verilog?

**Answer:** A compiler directive is an instruction beginning with a backtick that controls how Verilog source code is processed.

---

## Q2. What symbol identifies a compiler directive?

**Answer:**

```text
`
```

The **backtick**.

---

## Q3. What does `` `define`` do?

**Answer:** It defines a preprocessor macro.

---

## Q4. What does `` `undef`` do?

**Answer:** It removes a previously defined macro.

---

## Q5. What does `` `include`` do?

**Answer:** It inserts the contents of another source file during preprocessing.

---

## Q6. Difference between `` `include`` and module instantiation?

**Answer:**

```text
`include → source-code inclusion
Instantiation → hardware module hierarchy
```

---

## Q7. What does `` `ifdef`` mean?

**Answer:** Compile the following code if the specified macro is defined.

---

## Q8. What does `` `ifndef`` mean?

**Answer:** Compile the following code if the specified macro is not defined.

---

## Q9. What does `` `endif`` do?

**Answer:** It marks the end of a conditional compilation block.

---

## Q10. What is `` `timescale``?

**Answer:** It specifies the simulation time unit and time precision.

---

## Q11. What does `` `timescale 1ns/1ps`` mean?

**Answer:**

```text
Time unit      = 1 ns
Time precision = 1 ps
```

---

## Q12. In `` `timescale 1ns/1ps``, what does `#10` represent?

**Answer:**

```text
10 ns
```

---

## Q13. What is `` `default_nettype none``?

**Answer:** It prevents implicit declaration of nets and forces signals to be explicitly declared.

---

## Q14. Why use `` `default_nettype none``?

**Answer:** To catch undeclared or misspelled signal names and prevent accidental implicit wires.

---

## Q15. How do you restore the default net type?

**Answer:**

```verilog
`default_nettype wire
```

---

## Q16. What is conditional compilation?

**Answer:** It is the process of selectively including or excluding source code using directives such as `ifdef, `ifndef, `else, and `endif.

---

## Q17. What is `` `elsif``?

**Answer:** It provides an additional conditional branch in preprocessor conditional compilation.

---

## Q18. Do compiler directives directly represent hardware?

**Answer:** No. They control source-code preprocessing or compilation.

---

# 🔥 Placement Rapid-Fire

**Compiler directive symbol?**

→ Backtick `` ` ``

**Define macro?**

→ `` `define``

**Remove macro?**

→ `` `undef``

**Include file?**

→ `` `include``

**Compile if defined?**

→ `` `ifdef``

**Compile if not defined?**

→ `` `ifndef``

**Alternative branch?**

→ `` `else``

**Else-if branch?**

→ `` `elsif``

**End conditional block?**

→ `` `endif``

**Simulation time unit/precision?**

→ `` `timescale``

**Prevent implicit nets?**

→ `` `default_nettype none``

**Restore default net behavior?**

→ `` `default_nettype wire``

**`timescale syntax?**

→ `` `timescale UNIT/PRECISION``

**`timescale 1ns/1ps?**

→ 1 ns unit, 1 ps precision

**Include another source file?**

→ `` `include``

**Hardware hierarchy?**

→ Module instantiation, not `` `include``

---

# 🧠 9.19 QUICK REVISION

```text
             VERILOG DIRECTIVES
                    │
        ┌───────────┼────────────┐
        ↓           ↓            ↓
    Macros      Conditional    Timing
        │         compile         │
   `define       `ifdef       `timescale
   `undef        `ifndef
                 `else
                 `elsif
                 `endif
        │
        └──────────────┐
                       ↓
                 File / Nets
                       │
                  `include
              `default_nettype
```

### ⭐ Golden Rules

```text
`define → define macro
`include → include source file
`ifdef → compile if defined
`ifndef → compile if not defined
`timescale → time unit/precision
`default_nettype none → disable implicit nets
```
