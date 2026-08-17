# &#x20;STRUCTURAL MODELING ⭐⭐⭐⭐⭐

Structural modeling is the **fourth major Verilog modeling style**.

It describes a circuit by specifying:

> **What components are present and how they are connected.**

This is very important for VLSI placements because it tests whether you understand **hierarchical design, module instantiation, ports, and interconnections**.

---

# 1. What is Structural Modeling?

In structural modeling, a larger circuit is constructed using **smaller modules/components**.

For example:

```text
        Half Adder
```

```
         ↓

    Half Adder

         ↓

    Full Adder
```

Instead of describing the complete full adder using one equation, we can build it from two half adders.

### Memory trick

Structural = Components + Connections

---

# 2. Basic Concept

Suppose we already have:

```text
module half_adder (...);
```

We can use that module inside another module.

This is called **module instantiation**.

Example:

```text
half_adder HA1 (
```

```
.a(a),

.b(b),

.sum(sum1),

.carry(carry1)
```

);

Here:

```text
half_adder → Module being instantiated
```

HA1        → Instance name

.a(a)      → Port connection

---

# 3. What is Module Instantiation?

**Module instantiation** means creating an instance of an existing module inside another module.

Example:

```text
module top;
```

half_adder HA1 (

```
    .a(a),

    .b(b),

    .sum(sum),

    .carry(carry)

);
```

endmodule

Think of it as:

```text
Module = Blueprint
```

Instance = Actual component created from blueprint

---

# 4. Example — Half Adder

First define the half adder:

```text
module half_adder (
```

input a,

input b,

output sum,

output carry

);

assign sum = a ^ b;

assign carry = a & b;

endmodule

Now another module can instantiate it.

---

# 5. Full Adder Using Two Half Adders ⭐⭐⭐⭐⭐

A full adder can be constructed using:

```text
2 Half Adders
```

1 OR gate

Block diagram:

```text
       A ─────┐
```

```
          │

      ┌─────────┐

   B ─│ Half    │

      │ Adder 1 │

      └─────────┘

         │   │

        S1   C1

         │

         ↓

      ┌─────────┐
```

Cin ────→│ Half    │

```
      │ Adder 2 │

      └─────────┘

         │   │

        Sum  C2

             │

      C1 ─── OR ─── Cout
```

---

# 6. Structural Full Adder

```text
module full_adder (
```

input a,

input b,

input cin,

output sum,

output cout

);

wire s1;

wire c1;

wire c2;

half_adder HA1 (

```
.a(a),

.b(b),

.sum(s1),

.carry(c1)
```

);

half_adder HA2 (

```
.a(s1),

.b(cin),

.sum(sum),

.carry(c2)
```

);

assign cout = c1 | c2;

endmodule

This is structural because the full adder is constructed from **submodules and their connections**.

---

# 7. Why Do We Use `wire`?

Look at:

```text
wire s1;
```

wire c1;

wire c2;

These are internal connections between components.

For example:

```text
HA1
```

↓

s1

↓

HA2

Therefore:

wire → commonly used for connections between modules

---

# 8. Structural Modeling with Multiple Instances

You can instantiate the same module multiple times.

Example:

```text
half_adder HA1 (...);
```

half_adder HA2 (...);

half_adder HA3 (...);

Each is a separate instance.

```text
half_adder → HA1
```

half_adder → HA2

half_adder → HA3

---

# 9. Instance Name

Consider:

```text
half_adder HA1 (
```

```
.a(a),

.b(b),

.sum(s),

.carry(c)
```

);

There are three important parts:

```text
half_adder → Module name
```

HA1        → Instance name

(...)      → Port connections

### Placement question

> What is `HA1`?

**Answer:** It is the **instance name** of the `half_adder` module.

---

# 10. Named Port Mapping ⭐⭐⭐⭐⭐

The example:

```text
half_adder HA1 (
```

```
.a(a),

.b(b),

.sum(s),

.carry(c)
```

);

uses **named port mapping**.

Syntax:

```text
.module_port(signal);
```

For example:

```text
.a(a)
```

means:

```text
.a → Port of instantiated module
```

(a) → Signal in current module

---

# 11. Positional Port Mapping

You can also connect ports by their position.

Suppose:

```text
module half_adder (
```

input a,

input b,

output sum,

output carry

);

Then:

```text
half_adder HA1 (
```

a,

b,

s,

c

);

Connections are based on order:

```text
1st → a
```

2nd → b

3rd → sum

4th → carry

---

# 12. Named vs Positional Mapping

### Named

```text
half_adder HA1 (
```

```
.a(a),

.b(b),

.sum(s),

.carry(c)
```

);

### Positional

```text
half_adder HA1 (
```

a,

b,

s,

c

);

---

# 13. Which Is Safer?

**Named port mapping is generally preferred** because it is clearer and less prone to errors when module ports change or when there are many ports.

Example:

```text
.a(a),
```

.b(b),

.sum(s)

immediately shows which signal connects to which port.

---

# 14. Hierarchical Design ⭐⭐⭐⭐⭐

Structural modeling is closely related to **hierarchical design**.

A large design can be broken into smaller modules.

Example:

```text
                    CPU
```

```
                 │

    ┌────────────┼────────────┐

    ↓            ↓            ↓

   ALU       Register File   Control

    │
```

┌────┴────┐

↓         ↓

Adder       MUX

Each block can itself contain smaller blocks.

---

# 15. Why Use Hierarchical Design?

Advantages:

* Easier to understand
* Easier to test
* Easier to debug
* Reusable modules
* Better organization
* Supports large designs

### Memory

Large design → Small modules → Reusable blocks

---

# 16. Example — 4-bit Ripple Carry Adder

A 4-bit ripple carry adder can be constructed using four full adders.

```text
FA0 → FA1 → FA2 → FA3
```

Connections:

```text
A0,B0 → FA0 → C1
```

A1,B1 → FA1 → C2

A2,B2 → FA2 → C3

A3,B3 → FA3 → C4

Structural Verilog:

```text
module ripple_adder (
```

input [3:0] a,

input [3:0] b,

input cin,

output [3:0] sum,

output cout

);

wire c1, c2, c3;

full_adder FA0 (

```
.a(a[0]),

.b(b[0]),

.cin(cin),

.sum(sum[0]),

.cout(c1)
```

);

full_adder FA1 (

```
.a(a[1]),

.b(b[1]),

.cin(c1),

.sum(sum[1]),

.cout(c2)
```

);

full_adder FA2 (

```
.a(a[2]),

.b(b[2]),

.cin(c2),

.sum(sum[2]),

.cout(c3)
```

);

full_adder FA3 (

```
.a(a[3]),

.b(b[3]),

.cin(c3),

.sum(sum[3]),

.cout(cout)
```

);

endmodule

This is a very good example of structural modeling.

---

# 17. Structural Modeling Using Gate Primitives

Structural descriptions can also contain primitive gates.

Example:

```text
module circuit (
```

input a,

input b,

input c,

output y

);

wire x;

and (x, a, b);

or  (y, x, c);

endmodule

This describes the structure using primitive gates.

However, when discussing the **four modeling styles**, remember the usual distinction:

```text
Gate-level → primitive gates
```

Structural → modules/components and their interconnections

---

# 18. Structural Modeling vs Gate-Level

This is a very common placement question.

### Gate-level

```text
and (y, a, b);
```

Directly uses a Verilog primitive.

### Structural

```text
half_adder HA1 (...);
```

Uses a module as a building block.

### Memory trick

Gate primitive → Gate-Level
Module instance → Structural

---

# 19. Structural Modeling vs Dataflow

### Structural

```text
half_adder HA1 (...);
```

Focus:

> Components and connections.

### Dataflow

```text
assign y = a & b;
```

Focus:

> Data relationship/equation.

---

# 20. Structural Modeling vs Behavioral

### Structural

```text
full_adder FA1 (...);
```

Focus:

> How the circuit is built.

### Behavioral

```text
always @(*) begin
```

```
...
```

end

Focus:

> What the circuit does.

---

# 21. Top-Level Module

In a hierarchical design, the highest-level module is commonly called the **top-level module**.

Example:

```text
Top Module
```

```
↓
```

Subsystem 1

```
↓
```

Module A

Module B

The top module connects major blocks together.

---

# 22. Port Connection Example

Suppose:

```text
module adder (
```

input a,

input b,

output sum

);

Instantiate it:

```text
adder A1 (
```

```
.a(x),

.b(y),

.sum(z)
```

);

Connection:

```text
Current module signal → Instantiated module port
```

x → a

y → b

z → sum

---

# 23. Can One Module Instantiate Another?

**Yes.**

Example:

```text
module top;
```

submodule U1 (...);

endmodule

This is one of the fundamental ideas behind hierarchical structural design.

---

# 24. Can a Module Have Multiple Instances?

**Yes.**

Example:

```text
adder A1 (...);
```

adder A2 (...);

adder A3 (...);

adder A4 (...);

All four are separate instances of the same module.

---

# 25. Why Is Structural Modeling Useful?

Structural modeling is useful when:

* Building large systems from smaller blocks
* Reusing verified modules
* Creating hierarchical designs
* Connecting IP blocks
* Building datapaths
* Describing component-level architecture

---

# ⭐ Frequently Asked Placement Questions

## Q1. What is structural modeling?

**Answer:** Structural modeling describes a circuit in terms of components/modules and the connections between them.

---

## Q2. What is module instantiation?

**Answer:** Module instantiation is the process of creating an instance of an existing module inside another module.

---

## Q3. What is an instance?

Example:

```text
half_adder HA1 (...);
```

**Answer:** `HA1` is the instance name of the `half_adder` module.

---

## Q4. What is named port mapping?

**Answer:** Named port mapping connects signals to module ports explicitly by port name.

Example:

```text
.a(a),
```

.b(b)

---

## Q5. What is positional port mapping?

**Answer:** Positional port mapping connects signals to ports according to their order in the module declaration.

Example:

```text
half_adder HA1 (a, b, sum, carry);
```

---

## Q6. Which is generally preferred: named or positional mapping?

**Answer:** Named mapping is generally preferred because it is clearer and less error-prone.

---

## Q7. Why is `wire` commonly used in structural modeling?

**Answer:** `wire` is commonly used to represent connections between module instances and other hardware elements.

---

## Q8. What is hierarchical design?

**Answer:** Hierarchical design breaks a large system into smaller modules and connects those modules together at higher levels.

---

## Q9. Can a module be instantiated multiple times?

**Answer:** Yes. Multiple instances of the same module can be created.

---

## Q10. What is the difference between a module and an instance?

**Answer:**

```text
Module   → Blueprint/design definition
```

Instance → Actual occurrence of that module

Example:

```text
half_adder HA1 (...);
```

`half_adder` is the module and `HA1` is its instance.

---

## Q11. Can structural modeling use primitive gates?

**Answer:** Yes, structural descriptions can include primitive gates, but the standard distinction in modeling-style questions is that gate-level modeling focuses directly on primitive gates while structural modeling emphasizes component/module interconnections.

---

## Q12. What is the top-level module?

**Answer:** The top-level module is the highest-level module in a hierarchical design and typically connects the major submodules of the system.

---

# 🔥 Placement Rapid-Fire

**Structural modeling → ?**

→ Components + connections

**Module instance → ?**

→ An occurrence of a module

**`HA1`** **→ ?**

→ Instance name

**`.a(a)`** **→ ?**

→ Named port mapping

**`(a,b,sum,carry)`** **→ ?**

→ Positional mapping

**Common internal connection type → ?**

→ `wire`

**Large design broken into modules → ?**

→ Hierarchical design

**Can same module have multiple instances?**

→ Yes

**Blueprint → ?**

→ Module

**Actual occurrence → ?**

→ Instance

---

# 🧠 9.7 QUICK REVISION

```text
              STRUCTURAL MODELING
```

```
                   ↓

         Modules / Components

                   ↓

              Instantiation

                   ↓

              Connections

                   ↓

            Hierarchical Design
```

### Most important syntax

```text
module_name instance_name (
```

```
.port1(signal1),

.port2(signal2)
```

);

### Example

```text
half_adder HA1 (
```

```
.a(a),

.b(b),

.sum(s),

.carry(c)
```

);

Remember:

```text
half_adder → Module
```

HA1        → Instance

.a(a)      → Port connection

---

# ⭐ FOUR MODELING STYLES — FINAL MEMORY

```text
┌─────────────────────────────────────┐
```

│       VERILOG MODELING STYLES       │

├─────────────────────────────────────┤

│                                     │

│ Gate-Level → Primitive gates        │

│              and, or, not...        │

│                                     │

│ Dataflow   → assign + expressions   │

│                                     │

│ Behavioral → always + if/case       │

│                                     │

│ Structural → Modules + connections  │

│                                     │

└─────────────────────────────────────┘

Gate → Gates
Data → assign
Behavior → always
Structure → connections
