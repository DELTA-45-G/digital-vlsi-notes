## &#x20;Quick Revision Notes

> **Phase 6 scope:** Registers, Shift Registers, Universal Shift Registers, Counters, Ripple/Synchronous Counters, MOD-N, Ring, Johnson, and Counter Design.

---

# 6.1 REGISTERS ⭐⭐⭐⭐⭐

### Register

A **register** is a group of flip-flops used to store multiple bits.

**n-bit register=n flip-flops**

Example:

**8-bit register=8 FFs**

### Register vs Flip-Flop

| Flip-Flop              | Register             |
| ---------------------- | -------------------- |
| Stores 1 bit           | Stores multiple bits |
| Single storage element | Group of FFs         |

### Parallel Loading

All bits are loaded simultaneously.

### Enable

**Enable=1→Load**

**Enable=0→Hold**

### Reset

Clears the register:

**Q=0**

---

# 6.2 SHIFT REGISTERS ⭐⭐⭐⭐⭐

A **shift register** is a group of flip-flops that stores and shifts binary data.

### Shift Right

Bits move toward the right.

### Shift Left

Bits move toward the left.

### Important

Usually:

**1 active clock edge→1 shift**

### Applications

* Data transfer
* Data storage
* Serial/parallel conversion
* Delay elements

---

# 6.3 TYPES OF SHIFT REGISTERS ⭐⭐⭐⭐⭐

| Type     | Input    | Output   | Main Application  |
| -------- | -------- | -------- | ----------------- |
| **SISO** | Serial   | Serial   | Serial transfer   |
| **SIPO** | Serial   | Parallel | Serial → Parallel |
| **PISO** | Parallel | Serial   | Parallel → Serial |
| **PIPO** | Parallel | Parallel | Data storage      |

### Memory Trick

**First two letters describe input/output:**

```text
SISO → Serial → Serial
```

SIPO → Serial → Parallel

PISO → Parallel → Serial

PIPO → Parallel → Parallel

---

# 6.4 UNIVERSAL SHIFT REGISTER ⭐⭐⭐⭐⭐

A universal shift register can:

1. Hold
2. Shift right
3. Shift left
4. Parallel load

### Control Table

| S1 | S0 | Operation     |
| -- | -- | ------------- |
| 0  | 0  | Hold          |
| 0  | 1  | Shift Right   |
| 1  | 0  | Shift Left    |
| 1  | 1  | Parallel Load |

### Implementation

Commonly uses:

**MUX + D Flip-Flops**

MUX selects the required input/operation based on the select lines.

---

# 6.5 COUNTERS ⭐⭐⭐⭐⭐

A **counter** is a sequential circuit that follows a predetermined sequence of states according to clock pulses.

### n-bit binary counter

**2ⁿ states**

and:

**MOD=2ⁿ**

Example:

3-bit counter:

**2³=8**

Therefore:

**MOD−8**

---

## Up Counter

Counts upward:

```text
000 → 001 → 010 → 011 → 100 → ...
```

**Up = Increment**

## Down Counter

Counts downward:

```text
111 → 110 → 101 → 100 → ...
```

**Down = Decrement**

## Up/Down Counter

Can count in either direction depending on a control input.

---

# 6.6 ASYNCHRONOUS / RIPPLE COUNTER ⭐⭐⭐⭐⭐

In an asynchronous counter:

* Only the **first FF** receives the external clock.
* Subsequent FFs are triggered by previous FF outputs.
* Clock effect **ripples** through the FFs.

```text
CLK → FF0 → FF1 → FF2
```

### Main Advantage

**Simple hardware**

### Main Disadvantage

**Propagation delay**

Because delays accumulate through the flip-flop chain.

### Important

**Ripple counter = Asynchronous counter**

---

# 6.7 SYNCHRONOUS COUNTER ⭐⭐⭐⭐⭐

In a synchronous counter:

**All FFs receive the same clock**

```text
          ┌→ FF0
```

CLK ──────┼→ FF1

```
      └→ FF2
```

### Advantage

**Higher speed**

because ripple clock propagation is avoided.

### Disadvantage

**More combinational logic**

---

## 3-bit Synchronous Binary Up Counter Using T FFs

**T0=1**

**T1=Q0**

**T2=Q1·Q0**

General pattern:

**Tn=Qn−1Qn−2⋯Q0**

---

# 6.8 MOD-N COUNTERS ⭐⭐⭐⭐⭐

A **MOD-N counter** has exactly **N states** before repeating.

**MOD=N**

### Flip-Flops Required

Choose the smallest n satisfying:

**2ⁿ≥N**

or:

**n=⌈log₂N⌉**

### Unused States

**2ⁿ−N**

### Examples

| Counter | FFs | Unused States |
| ------- | --: | ------------: |
| MOD-5   |   3 |             3 |
| MOD-6   |   3 |             2 |
| MOD-10  |   4 |             6 |
| MOD-12  |   4 |             4 |
| MOD-20  |   5 |            12 |
| MOD-25  |   5 |             7 |

### MOD-10

Also called:

**Decade Counter**

Counts:

**0→9→0**

---

# 6.9 RING COUNTER ⭐⭐⭐⭐

A ring counter is a shift-register-based counter where the **last FF output is directly fed back** to the first FF.

Also called:

**One-hot counter**

### Example: 4-bit Ring Counter

```text
1000
```

0100

0010

0001

1000

Only one `1` circulates.

### MOD

For n FFs:

**MOD=n**

Example:

**8 FFs→MOD−8**

### Disadvantage

Requires many flip-flops.

For MOD-8:

* Ring → 8 FFs
* Binary → 3 FFs

### Important

Proper initialization is required.

---

# 6.10 JOHNSON COUNTER ⭐⭐⭐⭐⭐

A Johnson counter is a modified ring counter where the **complement of the last FF output** is fed back to the first FF.

Also called:

**Twisted Ring Counter**

### Feedback

Ring:

**Q→feedback**

Johnson:

**Q̅→feedback**

### MOD

For n FFs:

**MOD=2n**

Example:

4 FFs:

**MOD=2(4)=8**

### 4-bit Johnson Sequence

```text
0000
```

1000

1100

1110

1111

0111

0011

0001

0000

### Unused States

**2ⁿ−2n**

For 4 FFs:

**16−8=8**

unused states.

---

# 6.11 COUNTER DESIGN ⭐⭐⭐⭐⭐

### General Design Procedure

```text
1. Determine required states
```

↓

2. Determine number of FFs

↓

3. Create state table

↓

4. Determine next states

↓

5. Use excitation table

↓

6. Derive input equations

↓

7. Simplify

↓

8. Draw circuit

---

## D Flip-Flop

Very important:

**D=Qnext**

---

## T Flip-Flop

**T=Q⊕Qnext**

Remember:

```text
Q → Qnext
```

0 → 0 : T=0

0 → 1 : T=1

1 → 0 : T=1

1 → 1 : T=0

So:

**T=0→Hold**

**T=1→Toggle**

---

## JK Flip-Flop Excitation Table

| Q | Q(next) | J | K |
| - | ------- | - | - |
| 0 | 0       | 0 | X |
| 0 | 1       | 1 | X |
| 1 | 0       | X | 1 |
| 1 | 1       | X | 0 |

X = Don't Care.

---

# ⭐ MOST IMPORTANT PHASE 6 FORMULAS

### Register

**n-bit register=n FFs**

### Binary Counter

**States=2ⁿ**

### MOD-N FF Requirement

**2ⁿ≥N**

### Unused States

**2ⁿ−N**

### Ring Counter

**n FF→MOD−n**

### Johnson Counter

**n FF→MOD−2n**

### Johnson Unused States

**2ⁿ−2n**

### D FF

**D=Qnext**

### T FF

**T=Q⊕Qnext**

### 3-bit Synchronous Up Counter

**T0=1**

**T1=Q0**

**T2=Q1·Q0**

---

# 🧠 PHASE 6 — ONE-MINUTE REVISION

```text
REGISTER

→ Group of FFs

→ n FFs = n bits


SHIFT REGISTER

→ Stores + shifts data


SISO → Serial → Serial

SIPO → Serial → Parallel

PISO → Parallel → Serial

PIPO → Parallel → Parallel


UNIVERSAL

→ Hold

→ Shift Right

→ Shift Left

→ Parallel Load


COUNTER

→ Counts clock pulses

→ n-bit = 2^n states


UP

→ Increment


DOWN

→ Decrement


RIPPLE

→ Asynchronous

→ Clock ripples

→ Simple but slower


SYNCHRONOUS

→ Common clock

→ Faster

→ More logic


MOD-N

→ N states

→ 2^n ≥ N


RING

→ Q feedback

→ n FF = MOD-n

→ One-hot


JOHNSON

→ Q̅ feedback

→ n FF = MOD-2n

→ Twisted ring


COUNTER DESIGN

→ State table

→ Excitation table

→ Equations

→ Circuit
```

###
