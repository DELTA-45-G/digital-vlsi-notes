# VERILOG DESIGN FLOW & RTL

This topic explains **where Verilog fits into the complete VLSI design flow** and what happens to your Verilog code before it becomes actual hardware.

---

# 1. What is the Verilog Design Flow?

The basic flow is:

```text
Design Specification
```

↓

```text
RTL Design
```

↓

```text
Verilog Code
```

↓

```text
Simulation
```

↓

```text
Synthesis
```

↓

```text
Gate-Level Netlist
```

↓

```text
Physical Design
```

↓

```text
Signoff
```

↓

```text
Tapeout
```

### Memory

`RTL → Simulation → Synthesis → Netlist → Physical Design → Signoff`

---

# 2. Design Specification

Before writing Verilog, we first define **what the circuit should do**.

For example:

> Design a 4-bit up counter with synchronous reset.

The specification defines:

* Inputs
* Outputs
* Functionality
* Clock
* Reset
* Timing requirements
* Other constraints

---

# 3. RTL Design ⭐⭐⭐⭐⭐

RTL stands for:

`Register Transfer Level`

RTL describes:

* Registers
* Data transfers
* Combinational logic
* Control logic

Example:

```text
Register A
```

↓

```text
Combinational Logic
```

↓

```text
Register B
```

The RTL describes what happens to the data between these registers.

---

# 4. Example of RTL

Consider:

```verilog
module counter (
```

```verilog
input clk,

input reset,

output reg [3:0] count

);
```

```verilog
always @(posedge clk) begin

if (reset)

count <= 4'b0000;

else

count <= count + 1;

end
```

```verilog
endmodule
```

This RTL describes a 4-bit counter.

Conceptually:

```text
             ┌──────────────┐
             │              │
             │  +1 Logic    │
             │              │
             └──────┬───────┘
                    ↓
                 Register
                    ↑
                   CLK
```

---

# 5. RTL vs Gate-Level

This is an important interview distinction.

### RTL

Describes the design at a higher abstraction level.

```verilog
assign y = (a & b) | c;
```

### Gate-level

Describes the actual gates/cells.

```text
a ──┐
    AND ──┐
b ──┘     │
          OR ── y
c ────────┘
```

### Memory

`RTL → What hardware should do`

`Gate-level → How it is implemented with gates/cells`

---

# 6. RTL Coding

RTL coding means writing synthesizable HDL that represents the intended hardware.

Common RTL constructs:

```text
module
```

```text
assign

always

if

else

case
```

Sequential RTL commonly uses:

```verilog
always @(posedge clk)
```

---

# 7. RTL Simulation ⭐⭐⭐⭐⭐

Before synthesis, we normally simulate the RTL to verify functionality.

```text
Verilog RTL
```

↓

```text
Testbench
```

↓

```text
Simulator
```

↓

```text
Waveform
```

↓

```text
Check output
```

Example:

```text
Input       Output
  0           0
  1           1
```

The simulation helps identify functional bugs.

---

# 8. What is a Testbench?

A **testbench** is a simulation environment used to apply inputs to the Design Under Test (DUT) and check its outputs.

```text
        Testbench
            │
            ↓
           DUT
            │
            ↓
         Outputs
```

DUT:

`Design Under Test`

We will study testbenches in detail later in **Phase 9**.

---

# 9. RTL Simulation vs Synthesis

### RTL Simulation

Answers:

> **Does my design behave correctly?**

### Synthesis

Answers:

> **What hardware can implement this RTL?**

Therefore:

```text
Simulation → Functional verification
```

```text
Synthesis → Hardware implementation
```

---

# 10. Synthesis ⭐⭐⭐⭐⭐

Synthesis converts synthesizable RTL into a gate-level representation.

```text
RTL
```

↓

```text
Synthesis
```

↓

```text
Gate-Level Netlist
```

For example:

```verilog
assign y = a & b;
```

can synthesize into an AND gate.

---

# 11. What Does Synthesis Do?

Synthesis performs several tasks:

* Converts RTL to gates/cells
* Performs logic optimization
* Maps logic to available library cells
* Attempts to meet design constraints

Conceptually:

```text
RTL
```

↓

```text
Logic Optimization
```

↓

```text
Technology Mapping
```

↓

```text
Gate-Level Netlist
```

---

# 12. Technology Library

Synthesis uses a technology library containing available standard cells.

Examples:

```text
AND
OR
NAND
NOR
INV
MUX
DFF
```

Each cell has characteristics such as:

* Delay
* Area
* Power

Therefore synthesis is not simply "convert Verilog directly into gates"; it maps the logic to cells available in a target technology.

---

# 13. Constraints

Synthesis and timing analysis need design constraints.

Important constraints include:

* Clock definition
* Input delays
* Output delays
* Timing requirements
* Clock uncertainty
* Operating conditions

A common timing constraint is the clock period.

For example:

`Tclock = 10ns`

corresponds to:

`fmax = 100MHz`

assuming an ideal 10 ns period.

---

# 14. Gate-Level Netlist

After synthesis:

```text
RTL
```

↓

```text
Synthesis
```

↓

```text
Netlist
```

The netlist contains instances of cells and their connections.

Example:

```text
       INV
        │
        ↓
a ── NAND ── y
b ─────┘
```

---

# 15. What is Technology Mapping?

Technology mapping means mapping logical functions to cells available in a specific technology library.

Example:

```text
Logical function
```

↓

```text
Technology mapping
```

↓

```text
Available library cells
```

A synthesizer may choose different implementations depending on:

* Timing
* Area
* Power
* Constraints

---

# 16. Logic Optimization

Synthesis can optimize the RTL implementation.

For example:

```text
Original logic
```

↓

```text
Optimization
```

↓

```text
Reduced logic
```

Possible goals:

* Reduce area
* Improve timing
* Reduce power

This is another example of the **PPA trade-off** you studied in Phase 8.

---

# 17. Physical Design

After synthesis, the design enters physical implementation.

Simplified flow:

```text
Gate-Level Netlist
```

↓

```text
Floorplanning
```

↓

```text
Placement
```

↓

```text
Clock Tree Synthesis
```

↓

```text
Routing
```

↓

```text
Parasitic Extraction
```

↓

```text
STA / Signoff
```

---

# 18. Placement

Placement determines where standard cells are physically located on the chip.

```text
┌─────────────────────────┐
│ FF   NAND    MUX        │
│                         │
│ INV       AND     FF    │
│                         │
│ MUX    NOR       FF     │
└─────────────────────────┘
```

Placement affects:

* Wire length
* Timing
* Congestion
* Power

---

# 19. Clock Tree Synthesis

CTS distributes the clock to sequential elements.

```text
Clock Source
     │
     ↓
   Buffer
  /      \
 ↓        ↓
FF       FF
```

Main goals:

* Control skew
* Control insertion delay
* Maintain acceptable clock quality

---

# 20. Routing

Routing connects the placed cells using metal interconnect.

```text
Cell A ───────────── Cell B
```

Metal wire

Routing affects:

* Delay
* Congestion
* Crosstalk
* Power
* Signal integrity

---

# 21. Parasitic Extraction

Real wires have parasitic:

* Resistance
* Capacitance

After routing, these parasitics can be extracted for more accurate timing analysis.

```text
Routing
```

↓

```text
Parasitic Extraction
```

↓

```text
RC information
```

↓

```text
Timing Analysis
```

---

# 22. STA After Physical Design

After physical implementation, timing analysis uses more realistic information.

```text
Netlist
```

*

```text
Parasitics
```

*

```text
Timing Constraints
```

↓

```text
STA
```

It checks:

* Setup
* Hold
* Clock timing
* Timing paths

---

# 23. Timing Violation

Suppose STA reports:

```text
Setup Slack = -0.25 ns
```

This means:

`Setup timing violation`

The design needs optimization/ECO.

```text
STA
```

↓

```text
Violation
```

↓

```text
Analyze
```

↓

```text
ECO
```

↓

```text
STA again
```

This is the **timing-closure loop** from Phase 8.

---

# 24. Signoff

Before tapeout, multiple checks are performed.

Conceptually:

```text
Timing
```

```text
Power
```

```text
Signal Integrity
```

```text
Physical Verification
```

```text
Reliability
```

↓

```text
Signoff
```

Only after required signoff checks pass can the design proceed to tapeout.

---

# 25. Tapeout

Tapeout is the release of final design data for semiconductor manufacturing.

Simplified:

```text
RTL
```

↓

```text
Synthesis
```

↓

```text
Physical Design
```

↓

```text
Signoff
```

↓

```text
Tapeout
```

↓

```text
Manufacturing
```

---

# 26. Complete Verilog-to-Chip Flow ⭐⭐⭐⭐⭐

This is the **most important diagram to remember**:

```text
              Specification
                    ↓
                  RTL
                    ↓
             Verilog/SystemVerilog
                    ↓
               RTL Simulation
                    ↓
                Synthesis
                    ↓
           Gate-Level Netlist
                    ↓
              Floorplanning
                    ↓
                Placement
                    ↓
                   CTS
                    ↓
                 Routing
                    ↓
           Parasitic Extraction
                    ↓
                   STA
                    ↓
          Timing / Power / SI
                    ↓
              ECO / Optimize
                    ↓
                 Signoff
                    ↓
                 Tapeout
```

---

# 27. Important Interview Difference

### Q: Where does Verilog fit into the VLSI flow?

**Answer:**

Verilog is primarily used to describe the digital design at the RTL/HDL level. The RTL is simulated for functional verification and then synthesized into a gate-level netlist, which proceeds to physical design and signoff.

---

# 28. Frequently Asked Placement Questions

### Q1. What is RTL?

**Answer:** RTL stands for Register Transfer Level and describes data transfers between registers along with the combinational logic operating on that data.

---

### Q2. What is synthesis?

**Answer:** Synthesis converts synthesizable RTL into a gate-level netlist using a target technology library and design constraints.

---

### Q3. What is the output of synthesis?

**Answer:** A gate-level netlist consisting of library cells and their interconnections.

---

### Q4. What is a netlist?

**Answer:** A netlist is a representation of hardware in terms of cells/gates and their connections.

---

### Q5. What is technology mapping?

**Answer:** Technology mapping maps logical functions into cells available in a specific technology library.

---

### Q6. What is the difference between RTL and gate-level design?

**Answer:**

**RTL** describes hardware at a higher abstraction level, while **gate-level design** represents the implementation using gates or technology-library cells.

---

### Q7. What is RTL simulation?

**Answer:** RTL simulation verifies the functional behavior of the RTL before synthesis.

---

### Q8. What is a testbench?

**Answer:** A testbench is a simulation environment that applies stimulus to the DUT and observes/checks its outputs.

---

### Q9. What is DUT?

**Answer:**

`DUT = Design Under Test`

---

### Q10. What is the difference between simulation and synthesis?

**Answer:**

| Simulation                       | Synthesis                |
| -------------------------------- | ------------------------ |
| Verifies behavior                | Converts RTL to hardware |
| Produces simulation results      | Produces netlist         |
| Used for functional verification | Used for implementation  |

---

### Q11. Why are timing constraints needed?

**Answer:** Timing constraints tell synthesis and timing-analysis tools about requirements such as clock periods, input/output timing, and other timing relationships.

---

### Q12. What happens after synthesis?

**Answer:** The gate-level netlist proceeds to physical design, including floorplanning, placement, CTS, routing, extraction, and signoff analysis.

---

### Q13. What happens after routing?

**Answer:** Parasitics are extracted and timing/power/signal-integrity analyses are performed. Violations may require optimization or ECOs before signoff.

---

### Q14. What is technology library?

**Answer:** A technology library contains characterized cells and their relevant properties such as timing, power, and area information.

---

### Q15. What is the purpose of synthesis optimization?

**Answer:** To produce an implementation that satisfies design constraints while optimizing factors such as timing, power, and area.

---

# 🧠 9.2 QUICK REVISION

```text
SPECIFICATION
```

↓

```text
RTL
```

↓

```text
VERILOG
```

↓

```text
RTL SIMULATION
```

↓

```text
SYNTHESIS
```

↓

```text
GATE-LEVEL NETLIST
```

↓

```text
FLOORPLAN
```

↓

```text
PLACEMENT
```

↓

```text
CTS
```

↓

```text
ROUTING
```

↓

```text
PARASITIC EXTRACTION
```

↓

```text
STA
```

↓

```text
ECO / OPTIMIZATION
```

↓

```text
SIGNOFF
```

↓

```text
TAPEOUT
```

### Remember these 10 points:

```text
1. RTL = Register Transfer Level
```

2. Verilog describes digital hardware

3. Simulation → functional verification

4. Synthesis → RTL to netlist

5. Netlist → cells + connections

6. Technology mapping → library cells

7. Placement → physical cell locations

8. CTS → clock distribution

9. Routing → physical interconnections

10. Signoff → final verification before tapeout
