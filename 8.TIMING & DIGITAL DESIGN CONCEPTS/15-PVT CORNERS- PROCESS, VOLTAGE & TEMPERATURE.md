# PVT CORNERS: PROCESS, VOLTAGE & TEMPERATURE ⭐⭐⭐⭐⭐

This is an important **VLSI placement topic** because circuit timing does not remain the same under every manufacturing, voltage, and temperature condition.

---

# 1. What is PVT?

PVT stands for:

* **P → Process**
* **V → Voltage**
* **T → Temperature**

So:

**PVT = Process + Voltage + Temperature**

These three factors affect:

* Delay
* Power
* Timing
* Reliability
* Performance

---

# 2. Why Do We Need PVT Analysis?

A chip manufactured today will not be exactly identical to another chip manufactured tomorrow.

Also:

* Supply voltage can vary
* Temperature can vary
* Manufacturing parameters vary

Therefore, a design that works at one condition may fail at another.

Example:

```text
Normal condition
```

```
  ↓
```

Timing PASS ✅

Different PVT condition

```
  ↓
```

Timing FAIL ❌

Therefore:

**Design must work across required PVT conditions**

---

# 3. Process Variation ⭐⭐⭐⭐⭐

**Process** represents variations caused during semiconductor manufacturing.

Examples:

* Transistor dimensions
* Doping concentration
* Oxide thickness
* Threshold voltage
* Channel length

These variations affect transistor characteristics.

---

# 4. Process Corners

Common process corners include:

**TT, SS, FF**

### TT

**Typical-Typical**

Both NMOS and PMOS are approximately typical.

---

### SS

**Slow-Slow**

Both NMOS and PMOS are slow.

---

### FF

**Fast-Fast**

Both NMOS and PMOS are fast.

---

# 5. SF and FS Corners ⭐⭐⭐⭐

You may also see:

**SF**

and

**FS**

### SF

* NMOS → Slow
* PMOS → Fast

### FS

* NMOS → Fast
* PMOS → Slow

Memory:

```text
First letter  → NMOS
```

Second letter → PMOS

---

# 6. Voltage Variation ⭐⭐⭐⭐⭐

Supply voltage can vary around its nominal value.

Example:

```text
Nominal VDD = 1.0 V
```

Low voltage  = 0.9 V

Nominal      = 1.0 V

High voltage = 1.1 V

Generally:

### Lower voltage

Transistors become slower.

**VDD↓⇒Delay↑**

### Higher voltage

Transistors generally become faster.

**VDD↑⇒Delay↓**

But:

**VDD↑⇒Power↑**

So increasing voltage can improve speed but increases power and may impact reliability.

---

# 7. Temperature Variation ⭐⭐⭐⭐⭐

Temperature also affects transistor performance.

In many conventional CMOS timing situations:

**Temperature↑⇒Delay↑**

because carrier mobility decreases as temperature increases.

Therefore:

```text
Temperature ↑
```

```
  ↓
```

Mobility ↓

```
  ↓
```

Drive strength ↓

```
  ↓
```

Delay ↑

However, modern technology nodes can exhibit more complex temperature behavior, so avoid assuming one temperature is always worst for every timing characteristic.

---

# 8. Fast and Slow Conditions

For placement preparation, remember the simplified model:

### Slow condition

```text
Low voltage
```

High temperature

Slow process

```
  ↓
```

Larger delay

### Fast condition

```text
High voltage
```

Low temperature

Fast process

```
  ↓
```

Smaller delay

These are useful intuition-level rules.

---

# 9. Which Corner is Worst for Setup? ⭐⭐⭐⭐⭐

Setup timing is concerned with **maximum delay**.

Therefore, the worst setup condition is generally associated with a **slow corner**.

Simplified:

**Setup → Slow Corner**

Think:

```text
Slow process
```

* Low voltage

* High temperature

  ```
    ↓
  ```

Large delay

```
    ↓
```

Setup becomes difficult

---

# 10. Which Corner is Worst for Hold? ⭐⭐⭐⭐⭐

Hold timing is concerned with **minimum delay**.

Therefore, the worst hold condition is generally associated with a **fast corner**.

**Hold → Fast Corner**

Think:

```text
Fast process
```

* High voltage

* Low temperature

  ```
    ↓
  ```

Small delay

```
    ↓
```

Hold becomes difficult

---

# 11. 🔥 Most Important Memory

**SETUP → SLOW**

**HOLD → FAST**

This is a very common VLSI interview concept.

---

# 12. PVT and Timing

Timing analysis is performed across required PVT scenarios.

Example:

```text
PVT Corner
```

```
↓
```

Cell delay

```
↓
```

Path delay

```
↓
```

STA

```
↓
```

Setup / Hold check

A design must satisfy timing at the required corners.

---

# 13. Example

Suppose a path has:

### Fast corner

**tpath=5ns**

### Typical corner

**tpath=7ns**

### Slow corner

**tpath=10ns**

If the clock period is:

**TCLK=8ns**

then at the slow corner:

**10ns>8ns**

Therefore:

**Setup violation**

---

# 14. Why Setup Is Sensitive to Slow Conditions

Setup requires data to arrive **before the capture edge**.

If the circuit becomes slower:

```text
Data
```

↓

takes longer

↓

arrives late

↓

Setup violation

Therefore:

**Setup is sensitive to maximum delay**

---

# 15. Why Hold Is Sensitive to Fast Conditions

Hold requires the old data to remain stable for a certain amount of time after the capture edge.

If the new data propagates extremely quickly:

```text
New data
```

↓

Arrives too early

↓

Can disturb capture

↓

Hold violation

Therefore:

**Hold is sensitive to minimum delay**

---

# 16. PVT Corner Table ⭐⭐⭐⭐⭐

| Corner | Process | Voltage | Temperature | General Speed |
| ------ | ------- | ------- | ----------- | ------------- |
| SS     | Slow    | Low     | High        | Slow          |
| TT     | Typical | Nominal | Nominal     | Typical       |
| FF     | Fast    | High    | Low         | Fast          |

This is a simplified placement-level view.

Actual signoff corners can use more specific combinations and models.

---

# 17. PVT vs STA

These concepts work together.

### PVT

Defines:

**Operating condition**

### STA

Checks:

**Timing under that condition**

Example:

```text
PVT = SS / Low V / High T
```

```
         ↓

    Cell delays

         ↓

        STA

         ↓

   Setup check
```

---

# 18. PVT and Power

PVT does not only affect timing.

It also affects power.

Dynamic power is approximately:

**Pdynamic=αCV²f**

Therefore:

**V↑⇒Pdynamic↑**

because power depends on:

**V²**

---

# 19. Process Variation vs PVT

### Process variation

Variation caused by manufacturing.

### Voltage variation

Variation in supply voltage.

### Temperature variation

Variation in operating temperature.

Together:

**PVT**

---

# 20. 🔥 Placement Question

### Q.

Why are multiple PVT corners analyzed?

### Answer:

> Because transistor speed, delay, power, and timing can vary with manufacturing process, supply voltage, and temperature. The design must satisfy its required specifications across the relevant operating corners.

---

# 21. 🔥 Placement Question

### Q.

Which is generally more difficult for setup timing?

A. Fast corner
B. Slow corner

**B**

---

# 22. 🔥 Placement Question

### Q.

Which is generally more difficult for hold timing?

A. Fast corner
B. Slow corner

**A**

---

# 23. 🔥 Placement Question

### Q.

What does SS mean?

**Slow NMOS + Slow PMOS**

---

# 24. 🔥 Placement Question

### Q.

What does FF mean?

**Fast NMOS + Fast PMOS**

---

# 25. 🔥 Placement Question

### Q.

What does TT mean?

**Typical NMOS + Typical PMOS**

---

# 26. 🔥 Placement Question

### Q.

What does SF mean?

**Slow NMOS + Fast PMOS**

---

# 27. 🔥 Placement Question

### Q.

What does FS mean?

**Fast NMOS + Slow PMOS**

---

# 28. Critical Memory Table

```text
             PVT
```

```
          │

  ┌───────┼───────┐

  ↓       ↓       ↓
```

Process  Voltage Temperature

```
  │       │       │

  └───────┼───────┘

          ↓

       Delay

          ↓

         STA

          ↓

  Setup / Hold
```

---

# 🧠 ONE-MINUTE REVISION

```text
══════════════════════════════════════

              PVT

══════════════════════════════════════


P = Process

V = Voltage

T = Temperature


PROCESS:

SS → Slow-Slow

TT → Typical-Typical

FF → Fast-Fast


SF → Slow NMOS / Fast PMOS

FS → Fast NMOS / Slow PMOS


GENERAL:

Low V  → slower

High V → faster


High T → generally slower

Low T  → generally faster


SETUP:

Maximum delay

→ Slow corner


HOLD:

Minimum delay

→ Fast corner


MAIN MEMORY:

SETUP → SLOW

HOLD  → FAST
```

---

# 🔥 Placement Memory Tricks

### Process

**SS=Slow-Slow**

**TT=Typical-Typical**

**FF=Fast-Fast**

### Timing

**Setup → Slow**

**Hold → Fast**

### Voltage

**V↑→Delay↓, Power↑**

**V↓→Delay↑**
