# VERILOG MODULES & PORTS ⭐⭐⭐⭐⭐

Verilog modules are the **basic building blocks of a Verilog design**.

A module defines:

* Inputs
* Outputs
* Internal signals
* Logic
* Connections

---

# 1. What is a Verilog Module?

A **module** is a basic design unit in Verilog that describes a hardware block.

Example:

```verilog
module and_gate (
input a,
input b,
output y
);

assign y = a & b;

endmodule
```

Here:

```text
module     → Module keyword
```

and_gate   → Module name

a, b       → Inputs

y          → Output

assign     → Logic description

endmodule  → End of module

### Memory

Module = Basic building block of Verilog

---

# 2. Basic Module Syntax

```verilog
module module_name (
input  ...,
output ...,
inout  ...
);

// Internal logic

endmodule
```

Example:

```verilog
module mux (
input a,
input b,
input sel,
output y
);

assign y = sel ? b : a;

endmodule
```

---

# 3. `module` Keyword

Every Verilog module starts with:

```verilog
module
```

Example:

```verilog
module counter;
```

The module ends with:

```verilog
endmodule
```

---

# 4. Module Name

The identifier immediately following `module` is the module name.

```verilog
module full_adder;
```

Here:

```text
full_adder → Module name
```

---

# 5. Module Ports

Ports are the **external connections** of a module.

Three main port directions are:

```text
input
```

output

inout

---

# 6. `input`

An `input` port receives a signal from outside the module.

Example:

```verilog
module and_gate (
input a,
input b,
output y
);
```

Here:

```text
a → Input
```

b → Input

---

# 7. `output`

An `output` port sends a signal outside the module.

Example:

```verilog
output y
```

Here:

```text
y → Output
```

---

# 8. `inout`

`inout` represents a **bidirectional port**.

The signal can be used for both:

```text
Input
```

Output

Example:

```verilog
module io_block (
inout data
);
```

`inout` ports are commonly associated with **bidirectional buses/pins**, especially at interfaces.

---

# 9. Input Direction

Conceptually:

```text
Outside
```

↓

input

↓

Module

Example:

```verilog
input a;
```

---

# 10. Output Direction

Conceptually:

```text
Module
```

↓

output

↓

Outside

Example:

```verilog
output y;
```

---

# 11. Inout Direction

Conceptually:

```text
Outside ↔ Module
```

Example:

```verilog
inout data;
```

---

# 12. Scalar Ports

A scalar port represents **one bit**.

Example:

```verilog
input a;
```

output y;

Each is 1 bit.

Scalar = 1 bit

---

# 13. Vector Ports ⭐⭐⭐⭐⭐

A vector port contains multiple bits.

Example:

```verilog
input [3:0] a;
```

This is a **4-bit vector**:

```text
a[3] a[2] a[1] a[0]
```

Therefore:

[3:0]=4 bits

---

# 14. 8-bit Input

```verilog
input [7:0] data;
```

This contains:

```text
data[7]
```

data[6]

data[5]

data[4]

data[3]

data[2]

data[1]

data[0]

Total:

8 bits

---

# 15. 16-bit Input

```verilog
input [15:0] data;
```

Total:

16 bits

---

# 16. General Vector Width

For:

```text
[MSB:LSB]
```

Number of bits is:

|MSB−LSB|+1

Example:

```text
[7:4]
```

Number of bits:

7−4+1=4

So:

```text
[7:4] → 4 bits
```

---

# 17. MSB and LSB ⭐⭐⭐⭐⭐

Consider:

```verilog
input [7:0] data;
```

```text
data[7] → MSB
```

data[0] → LSB

### MSB

**Most Significant Bit**

### LSB

**Least Significant Bit**

---

# 18. Packed Vector

A declaration such as:

```verilog
reg [7:0] data;
```

defines an 8-bit packed vector in Verilog.

The bits are indexed:

```text
7 6 5 4 3 2 1 0
```

---

# 19. Port Declaration Example

```verilog
module alu (
input [7:0] a,
input [7:0] b,
input [2:0] sel,
output [7:0] y
);

endmodule
```

Here:

```text
a   → 8 bits
```

b   → 8 bits

sel → 3 bits

y   → 8 bits

---

# 20. Why Does `sel` Need 3 Bits?

A 3-bit select signal can represent:

23=8

different combinations.

```text
000
```

001

010

011

100

101

110

111

So it can select among up to 8 choices, depending on the design.

---

# 21. ANSI-Style Port Declaration ⭐⭐⭐⭐⭐

Modern Verilog commonly uses:

```verilog
module and_gate (
input a,
input b,
output y
);
```

This is called **ANSI-style port declaration**.

The port direction and declaration are written directly in the module header.

---

# 22. Non-ANSI Port Declaration

Older Verilog style:

```verilog
module and_gate (a, b, y);

input a;

input b;

output y;

assign y = a & b;

endmodule
```

Both styles are valid Verilog.

### Placement point

ANSI style is generally cleaner and more commonly seen in modern RTL.

---

# 23. Port Mapping

When a module is instantiated, its ports need to be connected.

Example:

```verilog
and_gate U1 (
    .a(x),
    .b(y),
    .y(z)
);
```

Here:

```text
Module port    Signal
```

---

a              x

b              y

y              z

---

# 24. Named Port Mapping

Example:

```verilog
and_gate U1 (
    .a(x),
    .b(y),
    .y(z)
);
```

The syntax:

```text
.port(signal)
```

is named port mapping.

---

# 25. Positional Port Mapping

Suppose:

```verilog
module and_gate (
input a,
input b,
output y
);
```

Instantiation:

```verilog
and_gate U1 (x, y, z);
```

Mapping:

```text
x → a
```

y → b

z → y

because connections follow the declared order.

---

# 26. Named vs Positional Mapping

| Named               | Positional                       |
| ------------------- | -------------------------------- |
| `.a(x)`             | `x`                              |
| Explicit            | Order-dependent                  |
| Easier to read      | Shorter                          |
| Less error-prone    | Can be confusing with many ports |
| Generally preferred | Useful for simple cases          |

---

# 27. Unconnected Ports

A port can sometimes be intentionally left unconnected.

For example:

```verilog
module_name U1 (
    .a(a),
    .b(b),
    .unused()
);
```

The empty connection:

```text
.unused()
```

means the port is intentionally left unconnected.

---

# 28. `wire` vs `reg` ⭐⭐⭐⭐⭐

This is one of the most important Verilog placement topics.

### `wire`

Represents a **net** driven by something else.

Example:

```verilog
wire y;

assign y = a & b;
```

### `reg`

A Verilog `reg` is a **procedural variable** that can hold a value assigned inside an `always` or other procedural block.

Example:

```verilog
reg y;

always @(*) begin
y = a & b;
end
```

---

# 29. Important Correction

A common misconception is:

> "`reg` means physical hardware register."

**Not necessarily.**

`reg` is a Verilog data type for a procedural variable.

Depending on how it is used, synthesis can infer:

```text
Combinational logic
```

Latch

Flip-flop

So:

reg does NOT automatically mean flip-flop

---

# 30. Example: `reg` Inferring Combinational Logic

```verilog
reg y;

always @(*) begin
y = a & b;
end
```

This can synthesize as an AND gate.

It does **not** imply a physical register.

---

# 31. Example: `reg` Inferring Flip-Flop

```verilog
reg q;

always @(posedge clk) begin
q <= d;
end
```

This can synthesize to a flip-flop.

So the **coding structure**, not merely the keyword `reg`, determines the hardware.

---

# 32. Output Port and `reg`

In traditional Verilog, if an output is assigned inside an `always` block, it is commonly declared as:

```verilog
output reg y;
```

Example:

```verilog
module mux (
input a,
input b,
input sel,
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

---

# 33. Output Driven by `assign`

If an output is driven by a continuous assignment:

```verilog
output y;

assign y = a & b;
```

then it is commonly a net.

In traditional Verilog:

```verilog
output wire y;
```

can be used explicitly.

---

# 34. Important Verilog Rule

Traditional Verilog:

```text
wire → continuous assignment
```

reg  → procedural assignment

Memory:

assign → wire
always → reg

This is a useful placement shortcut, though SystemVerilog provides more flexible types such as `logic`.

---

# 35. What is `logic`?

In SystemVerilog, `logic` is commonly used for signals that are assigned procedurally or otherwise as a variable.

Example:

```systemverilog
logic y;

always_comb begin
    y = a & b;
end
```

For your current **Verilog HDL** learning, focus first on:

```text
wire
```

reg

and understand that SystemVerilog later introduces `logic` and other improvements.

---

# 36. Input Ports Are Normally Read-Only

Inside a module, an input is used to receive data.

Example:

```verilog
input a;
```

You normally do not assign a value to an input from inside the module.

---

# 37. Output Ports

Outputs send data outside the module.

Example:

```verilog
output y;
```

The output may be driven by:

```text
continuous assignment
```

procedural block

module/gate connection

depending on how it is declared and used.

---

# 38. Bidirectional `inout`

Example:

```verilog
module io (
inout data,
input enable,
input out_data,
output in_data
);

assign data = enable ? out_data : 1'bz;

assign in_data = data;

endmodule
```

The special value:

```text
1'bz
```

means **high impedance**.

When the output driver is disabled, the shared line can be released.

---

# 39. What is High Impedance `Z`?

`Z` represents a **high-impedance state**.

It is commonly used with tri-state/bidirectional interfaces.

Example:

```verilog
assign data = enable ? out_data : 1'bz;
```

Meaning:

```text
enable = 1 → drive data
```

enable = 0 → release data

---

# 40. Four-State Logic ⭐⭐⭐⭐⭐

Verilog uses four basic logic states:

```text
0
```

1

X

Z

### `0`

Logic zero.

### `1`

Logic one.

### `X`

Unknown.

### `Z`

High impedance.

---

# 41. Why is `X` Important?

`X` represents an unknown value during simulation.

It can occur because of:

* Uninitialized variables
* Conflicting drivers
* Unknown hardware conditions
* Incomplete simulation information

Example:

```verilog
q = X
```

means the simulator does not currently know whether `q` is `0` or `1`.

---

# 42. Why is `Z` Important?

`Z` represents a high-impedance or disconnected driver state.

It is particularly relevant for:

```text
Tri-state buses
```

Bidirectional I/O

---

# 43. Module Example — 4-bit Adder

```verilog
module adder4 (
input [3:0] a,
input [3:0] b,
output [3:0] sum
);

assign sum = a + b;

endmodule
```

Ports:

```text
a   → 4-bit input
```

b   → 4-bit input

sum → 4-bit output

---

# 44. Module Example — 4-bit Register

```verilog
module register4 (
input clk,
input [3:0] d,
output reg [3:0] q
);

always @(posedge clk) begin
q <= d;
end

endmodule
```

Here:

```text
clk → 1-bit input
```

d   → 4-bit input

q   → 4-bit output

---

# ⭐ Frequently Asked Placement Questions

## Q1. What is a module in Verilog?

**Answer:** A module is the basic design unit in Verilog used to describe a hardware block.

---

## Q2. What are the three main port directions?

**Answer:**

```text
input
```

output

inout

---

## Q3. What is an input port?

**Answer:** An input port receives a signal from outside the module.

---

## Q4. What is an output port?

**Answer:** An output port sends a signal from the module to the outside.

---

## Q5. What is an `inout` port?

**Answer:** An `inout` port is bidirectional and can be used to both receive and drive a signal, typically for shared/bidirectional interfaces.

---

## Q6. What is the difference between scalar and vector?

**Answer:**

```text
Scalar → 1 bit
```

Vector → Multiple bits

Example:

```verilog
input a;        // 1 bit
input [7:0] a;  // 8 bits
```

---

## Q7. How many bits are in `[7:0]`?

7−0+1=8

**Answer: 8 bits.**

---

## Q8. What is the MSB of `[7:0]`?

**Answer:**

```text
bit 7
```

---

## Q9. What is the LSB of `[7:0]`?

**Answer:**

```text
bit 0
```

---

## Q10. What is named port mapping?

**Answer:** Connecting signals to module ports explicitly using port names.

Example:

```text
.a(signal_a)
```

---

## Q11. What is positional port mapping?

**Answer:** Connecting signals according to the order of ports in the module declaration.

---

## Q12. Which port mapping is generally preferred?

**Answer:** Named port mapping, because it is clearer and less error-prone.

---

## Q13. What is `wire`?

**Answer:** `wire` is a Verilog net type commonly used for signals driven by continuous assignments or module/gate outputs.

---

## Q14. What is `reg`?

**Answer:** `reg` is a Verilog procedural variable type that can be assigned inside procedural blocks such as `always`.

---

## Q15. Does `reg` mean a physical register?

**Answer:** **No.**

`reg` is a Verilog data type. The actual hardware depends on how it is used.

---

## Q16. What does `1'bz` mean?

**Answer:** It represents a **1-bit high-impedance (`Z`) value**.

---

## Q17. What are the four Verilog logic states?

**Answer:**

```text
0 → Logic 0
```

1 → Logic 1

X → Unknown

Z → High impedance

---

## Q18. What is the difference between `wire` and `reg`?

**Answer:**

| `wire`                                     | `reg`                                     |
| ------------------------------------------ | ----------------------------------------- |
| Net                                        | Procedural variable                       |
| Commonly driven by `assign`                | Commonly assigned in `always`             |
| Does not store procedural values by itself | Can hold a procedural value               |
| Often used for connections                 | Often used for procedural outputs/signals |

---

# 🔥 Placement Rapid-Fire

**Basic Verilog design unit?**

→ Module

**Module starts with?**

→ `module`

**Module ends with?**

→ `endmodule`

**Three port directions?**

→ `input`, `output`, `inout`

**Scalar?**

→ 1 bit

**`[7:0]`?**

→ 8 bits

**MSB of `[7:0]`?**

→ 7

**LSB of `[7:0]`?**

→ 0

**Bidirectional port?**

→ `inout`

**High impedance?**

→ `Z`

**Unknown?**

→ `X`

**Continuous assignment commonly drives?**

→ `wire`

**Procedural assignment commonly uses?**

→ `reg`

**Does `reg` mean physical register?**

→ No

**Named mapping?**

→ `.port(signal)`

**Positional mapping?**

→ Based on port order

---

# 🧠 9.8 QUICK REVISION

```text
                 VERILOG MODULE
```

```
                   ↓

          ┌────────┼────────┐

          ↓        ↓        ↓

        input    output    inout

          ↓        ↓        ↓

       Receive    Send    Bidirectional
```

### Port width

```text
a             → 1 bit
```

[3:0]         → 4 bits

[7:0]         → 8 bits

[15:0]        → 16 bits

### Important types

```text
wire → net
```

reg  → procedural variable

### Four-state logic

```text
0 → Logic 0
```

1 → Logic 1

X → Unknown

Z → High impedance

### Port mapping

```text
Named:
```

.a(signal)

Positional:

(signal1, signal2, ...)
