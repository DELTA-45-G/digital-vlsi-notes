# TYPES OF SHIFT REGISTERS

Now let's study the four types **one by one**, because these are very frequently asked in placements.

## 1. SISO — Serial In Serial Out ⭐⭐⭐⭐⭐

**SISO = Serial In Serial Out**

Data enters **one bit at a time** and leaves **one bit at a time**.

```text id="s7k3n2"
Serial Input
     │
     ▼
   FF1 → FF2 → FF3 → FF4
                    │
                    ▼
              Serial Output
```

Example:

If we want to transfer:

**1011**

the bits enter sequentially:

```text id="x4p8m1"
Clock 1 → 1
```

Clock 2 → 0

Clock 3 → 1

Clock 4 → 1

The data also comes out **serially**, one bit per clock.

### Main application

**Serial data transfer / delay**

---

# 2. SIPO — Serial In Parallel Out ⭐⭐⭐⭐⭐

**SIPO = Serial In Parallel Out**

Data enters **one bit at a time**, but after shifting, all stored bits can be read **simultaneously**.

```text id="m5q9c4"
Serial Input
     │
     ▼
   FF1 → FF2 → FF3 → FF4
     │     │     │     │
     ▼     ▼     ▼     ▼
    Q3    Q2    Q1    Q0
     └──── Parallel Output ────┘
```

### Example

Suppose we serially enter:

**1011**

After the required clock pulses, the register contains the four bits and they are available at the outputs simultaneously.

### Main application

**Serial-to-parallel conversion**

---

# 3. PISO — Parallel In Serial Out ⭐⭐⭐⭐⭐

**PISO = Parallel In Serial Out**

Data is loaded **simultaneously**, but then leaves **one bit at a time**.

```text id="w2r6t8"
Parallel Input
  │   │   │   │
  ▼   ▼   ▼   ▼
 FF1 FF2 FF3 FF4
  │
  └──────────────► Serial Output
```

For example, we can load:

**1011**

in parallel and then shift it out one bit at a time.

### Main application

**Parallel-to-serial conversion**

---

# 4. PIPO — Parallel In Parallel Out ⭐⭐⭐⭐⭐

**PIPO = Parallel In Parallel Out**

Data enters all at once and leaves all at once.

```text id="n8y3v5"
Parallel Input
  │   │   │   │
  ▼   ▼   ▼   ▼
 FF1 FF2 FF3 FF4
  │   │   │   │
  ▼   ▼   ▼   ▼
Parallel Output
```

For example:

**1011**

is loaded simultaneously and becomes available simultaneously at the outputs.

### Main application

**Temporary data storage**

---

# 5. Easy Comparison ⭐⭐⭐⭐⭐

| Type     | Input    | Output   | Main Use            |
| -------- | -------- | -------- | ------------------- |
| **SISO** | Serial   | Serial   | Data transfer/delay |
| **SIPO** | Serial   | Parallel | Serial → Parallel   |
| **PISO** | Parallel | Serial   | Parallel → Serial   |
| **PIPO** | Parallel | Parallel | Data storage        |

### 🧠 Easy Trick

Remember the **first letter = input** and **second letter = output**.

```text id="h6t1q9"
SISO → Serial → Serial
```

SIPO → Serial → Parallel

PISO → Parallel → Serial

PIPO → Parallel → Parallel
