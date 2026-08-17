## REGISTERS ⭐⭐⭐⭐⭐

We'll start from the basics.

---

# 1. What is a Register?

A **register** is a group of flip-flops used to store multiple bits of binary information.

Since one flip-flop stores:

**1 bit**

an n-bit register requires:

**n flip-flops**

### Example

A 4-bit register:

```text
        ┌─────┐
D3 ────►│ DFF │──► Q3
        └─────┘

        ┌─────┐
D2 ────►│ DFF │──► Q2
        └─────┘

        ┌─────┐
D1 ────►│ DFF │──► Q1
        └─────┘

        ┌─────┐
D0 ────►│ DFF │──► Q0
        └─────┘
```

Therefore:

**4-bit register = 4 flip-flops**

---

# 2. Why Are Registers Used?

Registers are used to:

* Store binary data
* Temporarily hold data
* Transfer data
* Synchronize data
* Store intermediate results
* Build larger digital systems

Registers are fundamental building blocks of processors and digital systems.

---

# 3. Register Using D Flip-Flops ⭐⭐⭐⭐⭐

D flip-flops are commonly used to construct registers.

For a 4-bit register:

```text
D3 ──► DFF ──► Q3
D2 ──► DFF ──► Q2
D1 ──► DFF ──► Q1
D0 ──► DFF ──► Q0

          ▲
          │
        CLOCK
```

All flip-flops receive the **same clock**.

At the active clock edge, the four input bits are stored simultaneously.

---

# 4. Example

Suppose:

```text
D = 1011
```

Before the clock edge:

```text
D3 D2 D1 D0

 1  0  1  1
```

At the active clock edge:

```text
Q3 Q2 Q1 Q0

 1  0  1  1
```

Therefore:

**Q=1011**

The register has stored the 4-bit value.

---

# 5. Parallel Loading ⭐⭐⭐⭐⭐

When all bits are loaded into a register **simultaneously**, it is called:

**Parallel loading**

Example:

```text
Input:     1011
```

```
         │

         ▼

   ┌───────────┐

   │ 4-bit     │

   │ Register  │

   └───────────┘

         │

         ▼
```

Stored:    1011

All four bits enter at the same time.

---

# 6. Register vs Flip-Flop ⭐⭐⭐⭐⭐

This is a common interview question.

| Flip-Flop                | Register               |
| ------------------------ | ---------------------- |
| Stores 1 bit             | Stores multiple bits   |
| Single storage element   | Group of flip-flops    |
| Basic sequential element | Built using flip-flops |

### Example

**1 FF=1 bit**

**8-bit register=8 FFs**

---

# 7. Register Size

An n-bit register stores:

**n bits**

and generally requires:

**n flip-flops**

### Examples

| Register | Flip-Flops |
| -------- | ---------: |
| 4-bit    |          4 |
| 8-bit    |          8 |
| 16-bit   |         16 |
| 32-bit   |         32 |
| 64-bit   |         64 |

---

# 8. Register With Enable ⭐⭐⭐⭐⭐

A register may have an **enable** signal.

The enable determines whether new data should be loaded.

For example:

### Enable = 1

Load new data:

**Qnext=D**

### Enable = 0

Hold previous data:

**Qnext=Q**

So:

**Enable controls whether the register loads or holds**

---

# 9. Register With Reset

A register can also have a reset input.

When reset is activated:

**Q=0**

For a 4-bit register:

```text
Q3 Q2 Q1 Q0

 0  0  0  0
```

Reset can be:

* Synchronous
* Asynchronous

We will encounter these concepts again in later digital design topics.

---

# 10. Important Concept: Register vs Memory

Don't confuse them.

### Register

* Very small storage
* Very fast
* Located close to processing logic/CPU
* Built from flip-flops

### Memory

* Much larger storage
* Used to store larger amounts of data
* Includes structures such as SRAM/DRAM

Memory concepts are **Phase 10**, not Phase 6.

---

# 11. Register Applications ⭐⭐⭐⭐

Registers are commonly used in:

* CPUs
* Datapaths
* ALUs
* Pipelines
* Temporary data storage
* Data transfer
* Control systems

---

# 🧠 Quick Revision

```text
REGISTER
────────────────────────────

Register:

→ Group of flip-flops

→ Stores multiple bits

1 Flip-Flop:

→ 1 bit

n-bit Register:

→ n flip-flops

→ Stores n bits

D Flip-Flops:

→ Commonly used to build registers

Parallel Loading:

→ All bits loaded simultaneously

Enable = 1:

→ Load new data

Enable = 0:

→ Hold previous data

Reset:

→ Clears register

→ Q = 0

Register:

→ Small + fast

Memory:

→ Larger storage

→ Phase 10
```
