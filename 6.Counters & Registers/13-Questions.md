# &#x20;FREQUENTLY ASKED PLACEMENT QUESTIONS

## 6.1 Registers ⭐⭐⭐⭐⭐

### Q1. What is a register?

**Answer:**

A register is a group of flip-flops used to store multiple bits of binary data.

---

### Q2. How many flip-flops are required for an 8-bit register?

**Answer:**

**8 flip-flops**

Each flip-flop stores one bit.

---

### Q3. What is the difference between a flip-flop and a register?

**Answer:**

* Flip-flop → stores **1 bit**
* Register → group of flip-flops that stores **multiple bits**

---

### Q4. What is parallel loading?

**Answer:**

Parallel loading means loading **all bits of a register simultaneously** using a common clock.

---

### Q5. What happens when the register's enable signal is disabled?

**Answer:**

The register **holds its previous data**.

---

# 6.2 Shift Registers ⭐⭐⭐⭐⭐

### Q6. What is a shift register?

**Answer:**

A shift register is a group of flip-flops used to **store and shift binary data**.

---

### Q7. What happens during a right shift?

**Answer:**

The bits move toward the **right**, and a new bit enters from the left side.

---

### Q8. What happens during a left shift?

**Answer:**

The bits move toward the **left**, and a new bit enters from the right side.

---

### Q9. How many clock pulses are required to shift 8 bits through a serial shift register?

**Answer:**

**8 clock pulses**

assuming one bit is shifted per clock pulse.

---

### Q10. What are the applications of shift registers?

**Answer:**

* Serial-to-parallel conversion
* Parallel-to-serial conversion
* Data storage
* Data transfer
* Digital delay
* Sequence generation

---

# 6.3 SISO, SIPO, PISO, PIPO ⭐⭐⭐⭐⭐

### Q11. What does SISO stand for?

**Answer:**

**Serial In Serial Out**

---

### Q12. What does SIPO stand for?

**Answer:**

**Serial In Parallel Out**

Used for:

**Serial → Parallel conversion**

---

### Q13. What does PISO stand for?

**Answer:**

**Parallel In Serial Out**

Used for:

**Parallel → Serial conversion**

---

### Q14. What does PIPO stand for?

**Answer:**

**Parallel In Parallel Out**

---

### Q15. Which shift register is commonly used for serial-to-parallel conversion?

**Answer:**

**SIPO**

---

### Q16. Which shift register is commonly used for parallel-to-serial conversion?

**Answer:**

**PISO**

---

# 6.4 Universal Shift Register ⭐⭐⭐⭐⭐

### Q17. What is a universal shift register?

**Answer:**

A universal shift register can perform:

* Hold
* Shift right
* Shift left
* Parallel load

---

### Q18. Why is a MUX used in a universal shift register?

**Answer:**

A MUX selects which data source should be connected to the flip-flop input based on the control/select signals.

---

### Q19. What are the four operations of a universal shift register?

**Answer:**

| S1 | S0 | Operation     |
| -- | -- | ------------- |
| 00 |    | Hold          |
| 01 |    | Shift Right   |
| 10 |    | Shift Left    |
| 11 |    | Parallel Load |

---

### Q20. How many select lines are required to select 4 operations?

**Answer:**

**2ⁿ≥4**

**n=2**

Therefore:

**2 select lines**

---

# 6.5 Counters — Basics ⭐⭐⭐⭐⭐

### Q21. What is a counter?

**Answer:**

A counter is a sequential circuit that goes through a predetermined sequence of states in response to clock pulses.

---

### Q22. How many states does an n-bit binary counter have?

**Answer:**

**2ⁿ**

---

### Q23. How many states does a 4-bit binary counter have?

**Answer:**

**2⁴=16**

---

### Q24. What is the MOD value of a 5-bit binary counter?

**Answer:**

**2⁵=32**

Therefore it is a **MOD-32 counter**.

---

### Q25. What is an up counter?

**Answer:**

An up counter counts in increasing order.

Example:

```text id="z6w0l7"
000 → 001 → 010 → 011 → ...
```

---

### Q26. What is a down counter?

**Answer:**

A down counter counts in decreasing order.

Example:

```text id="c8m4q2"
111 → 110 → 101 → 100 → ...
```

---

### Q27. What is an up/down counter?

**Answer:**

An up/down counter can count either upward or downward depending on a control signal.

---

# 6.6 Asynchronous / Ripple Counter ⭐⭐⭐⭐⭐

### Q28. What is an asynchronous counter?

**Answer:**

A counter in which the flip-flops do **not receive the external clock simultaneously**.

---

### Q29. Why is an asynchronous counter called a ripple counter?

**Answer:**

Because the output transition propagates from one flip-flop to the next like a ripple.

---

### Q30. Does every flip-flop in a ripple counter receive the external clock?

**Answer:**

No

Only the first flip-flop receives the external clock directly.

---

### Q31. What is the major disadvantage of a ripple counter?

**Answer:**

**Accumulated propagation delay**

---

### Q32. Why is a ripple counter slower?

**Answer:**

Because each flip-flop waits for the transition from the previous flip-flop, causing propagation delays to accumulate.

---

### Q33. What is the main advantage of an asynchronous counter?

**Answer:**

**Simple hardware / simple design**

---

# 6.7 Synchronous Counter ⭐⭐⭐⭐⭐

### Q34. What is a synchronous counter?

**Answer:**

A counter in which **all flip-flops receive the same clock signal simultaneously**.

---

### Q35. Which is faster: synchronous or asynchronous counter?

**Answer:**

**Synchronous counter**

---

### Q36. Why is a synchronous counter faster?

**Answer:**

All flip-flops are triggered by the same clock, so the clock transition does not ripple through the flip-flops.

---

### Q37. What is the disadvantage of a synchronous counter?

**Answer:**

**More combinational logic and hardware complexity**

---

### Q38. For a 3-bit synchronous binary up counter using T flip-flops, find T0,T1,T2.

**Answer:**

**T0=1**

**T1=Q0**

**T2=Q1Q0**

---

# 6.8 MOD-N Counters ⭐⭐⭐⭐⭐

### Q39. What is a MOD-N counter?

**Answer:**

A MOD-N counter has exactly **N distinct states** before repeating.

---

### Q40. How many flip-flops are required for a MOD-10 counter?

**Answer:**

**2³=8<10**

**2⁴=16≥10**

Therefore:

**4 flip-flops**

---

### Q41. How many flip-flops are required for MOD-12?

**Answer:**

**2³<12≤2⁴**

**4 FFs**

---

### Q42. How many flip-flops are required for MOD-25?

**Answer:**

**2⁴<25≤2⁵**

**5 FFs**

---

### Q43. How many unused states are there in a MOD-10 counter using 4 FFs?

**Answer:**

**2⁴−10=16−10**

**6**

---

### Q44. What is another name for a MOD-10 counter?

**Answer:**

**Decade counter**

---

### Q45. What is the formula for the number of flip-flops required for MOD-N?

**Answer:**

**n=⌈log₂N⌉**

or equivalently:

**2ⁿ≥N**

---

# 6.9 Ring Counter ⭐⭐⭐⭐⭐

### Q46. What is a ring counter?

**Answer:**

A ring counter is a shift-register-based counter where the output of the last flip-flop is fed directly back to the first flip-flop.

---

### Q47. What is another name for a ring counter?

**Answer:**

**One-hot counter**

---

### Q48. What is the MOD value of an n-bit ring counter?

**Answer:**

**MOD−n**

---

### Q49. How many flip-flops are required for a MOD-8 ring counter?

**Answer:**

**8 FFs**

---

### Q50. What is the main disadvantage of a ring counter?

**Answer:**

It requires more flip-flops compared with a binary counter for the same number of states.

---

### Q51. What is the sequence of a 4-bit ring counter?

**Answer:**

```text id="b3g4m6"
1000
```

0100

0010

0001

1000

---

### Q52. Why is initialization important in a ring counter?

**Answer:**

The counter must start with a valid one-hot state. If it starts at `0000`, there is no `1` to circulate.

---

# 6.10 Johnson Counter ⭐⭐⭐⭐⭐

### Q53. What is a Johnson counter?

**Answer:**

A Johnson counter is a modified ring counter in which the **complement of the last flip-flop output** is fed back to the first flip-flop.

---

### Q54. What is another name for a Johnson counter?

**Answer:**

**Twisted Ring Counter**

---

### Q55. What is the MOD value of an n-bit Johnson counter?

**Answer:**

**MOD=2n**

---

### Q56. What is the MOD value of a 4-bit Johnson counter?

**Answer:**

**2(4)=8**

---

### Q57. What is the MOD value of a 5-bit Johnson counter?

**Answer:**

**2(5)=10**

---

### Q58. What is the difference between a ring and Johnson counter?

**Answer:**

| Ring              | Johnson                  |
| ----------------- | ------------------------ |
| Direct Q feedback | Complemented Q̅ feedback |
| MOD-n             | MOD-2n                   |
| One-hot sequence  | Twisted-ring sequence    |

---

### Q59. How many unused states does a 4-bit Johnson counter have?

**Answer:**

Total:

**2⁴=16**

Used:

**2(4)=8**

Unused:

**16−8=8**

---

# 6.11 Counter Design ⭐⭐⭐⭐⭐

### Q60. What are the basic steps in counter design?

**Answer:**

1. Determine required states
2. Determine number of flip-flops
3. Create state table
4. Determine next states
5. Use excitation table
6. Derive flip-flop input equations
7. Simplify equations
8. Draw the circuit

---

### Q61. What is the relationship between D and next state?

**Answer:**

**D=Qnext**

---

### Q62. What is the excitation equation for a T flip-flop?

**Answer:**

**T=Q⊕Qnext**

---

### Q63. When does a T flip-flop toggle?

**Answer:**

**T=1**

---

### Q64. When does a T flip-flop hold its state?

**Answer:**

**T=0**

---

### Q65. What is the purpose of an excitation table?

**Answer:**

An excitation table determines the required flip-flop inputs to achieve a desired transition from the present state to the next state.

---

# 🔥 TOP 15 QUESTIONS YOU MUST KNOW

If you're short on time before a placement test, **memorize these first**:

1. What is a register?
2. SISO vs SIPO vs PISO vs PIPO?
3. What is a universal shift register?
4. How many states does an n-bit counter have?
5. Ripple vs synchronous counter?
6. Why is ripple counter slower?
7. Which counter is faster?
8. How many FFs for MOD-N?
9. What are unused states?
10. MOD-10 is called what?
11. Ring counter: MOD value?
12. Johnson counter: MOD value?
13. Ring vs Johnson feedback?
14. D=Qnext and T=Q⊕Qnext
15. How is a counter designed using an excitation table?

---

## 🧠 Final Phase 6 Memory Map

```text id="f4j9q7"
REGISTERS
```

↓

SHIFT REGISTERS

↓

SISO / SIPO / PISO / PIPO

↓

UNIVERSAL SHIFT REGISTER

↓

UP / DOWN COUNTERS

↓

ASYNCHRONOUS (RIPPLE)

↓

SYNCHRONOUS

↓

MOD-N

↓

RING

↓

JOHNSON

↓

COUNTER DESIGN
