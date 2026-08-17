# COUNTER DESIGN ⭐⭐⭐⭐⭐

This is the **final major topic of Phase 6**.

Here we move from simply understanding counters to **designing a counter from a required sequence**.

This is important for written tests and VLSI interviews.

---

# 1. What is Counter Design?

Counter design means creating a sequential circuit that follows a **specific required sequence of states**.

For example, instead of:

```text id="s5f2k9"
000 → 001 → 010 → 011 → ...
```

we may want:

```text id="m7q3v1"
000 → 001 → 011 → 010 → 000
```

We need to determine:

* Number of flip-flops
* State transitions
* Flip-flop inputs
* Required combinational logic

---

# 2. General Counter Design Steps ⭐⭐⭐⭐⭐

Remember this process:

```text id="x4c8n6"
1. Determine required states
```

↓

2. Determine number of flip-flops

↓

3. Create state table

↓

4. Find next states

↓

5. Use excitation table

↓

6. Derive flip-flop input equations

↓

7. Simplify logic

↓

8. Draw the circuit

---

# 3. Step 1 — Determine Number of Flip-Flops

Suppose we need a MOD-6 counter.

We need:

**2ⁿ≥6**

**2²=4<6**

**2³=8≥6**

Therefore:

**3 flip-flops**

---

# 4. Step 2 — Create State Sequence

For a MOD-6 counter:

```text id="y9h4p2"
000
```

001

010

011

100

101

000

The unused states are:

```text id="z3r6m8"
110
```

111

---

# 5. Step 3 — State Table

A state table shows:

* Present state
* Next state

For MOD-6:

| Present State | Next State |
| ------------- | ---------- |
| 000           | 001        |
| 001           | 010        |
| 010           | 011        |
| 011           | 100        |
| 100           | 101        |
| 101           | 000        |

This tells us how the counter must behave.

---

# 6. Using Flip-Flop Excitation Tables ⭐⭐⭐⭐⭐

The next step depends on which flip-flop we use.

We may design counters using:

* SR flip-flops
* JK flip-flops
* D flip-flops
* T flip-flops

For placements, **JK, D and T flip-flops** are particularly important.

---

# 7. D Flip-Flop Counter Design ⭐⭐⭐⭐⭐

The D flip-flop has a very simple relationship:

**D=Qnext**

Therefore, when designing a counter using D flip-flops:

> Simply connect the required next-state value to D.

### Example

If:

**Qnext=1**

then:

**D=1**

If:

**Qnext=0**

then:

**D=0**

This makes D flip-flops relatively straightforward for counter design.

---

# 8. T Flip-Flop Counter Design ⭐⭐⭐⭐⭐

T flip-flop behavior:

| T | Operation |
| - | --------- |
| 0 | Hold      |
| 1 | Toggle    |

The excitation relationship is:

**T=Q⊕Qnext**

Therefore:

* If Q stays the same → T=0
* If Q changes → T=1

### Example

**Q=0,Qnext=1**

Then:

**T=0⊕1=1**

So the flip-flop toggles.

---

# 9. JK Flip-Flop Counter Design ⭐⭐⭐⭐⭐

JK flip-flop excitation table:

| Q | Q(next) | J | K |
| - | ------- | - | - |
| 0 | 0       | 0 | X |
| 0 | 1       | 1 | X |
| 1 | 0       | X | 1 |
| 1 | 1       | X | 0 |

Here X means **don't care**.

This table is used to determine the required J and K inputs for each state transition.

---

# 10. Example — Binary Up Counter Using T Flip-Flops

For a 3-bit synchronous binary up counter:

**T0=1**

**T1=Q0**

**T2=Q1Q0**

So:

```text id="c8m2r5"
       ┌─────┐
1 ────►│ T FF│──► Q0
       └─────┘

Q0 ───►│ T FF│──► Q1
       └─────┘

Q0·Q1 ►│ T FF│──► Q2
       └─────┘

       Common CLOCK
```

This is a standard counter-design pattern.

---

# 11. Self-Correcting Counters ⭐⭐⭐⭐

A counter may have unused states.

For example, MOD-6 using 3 flip-flops has:

```text id="p6n3x9"
000
```

001

010

011

100

101

Unused:

```text id="q4v7m1"
110
```

111

A well-designed counter can be made **self-correcting**, meaning that if it somehow enters an unused state, the circuit eventually returns to a valid counting sequence.

This is useful for reliable sequential circuit design.

---

# 12. Important Placement Concepts

You should know these distinctions:

### Counter

Sequential circuit that follows a counting sequence.

### State

Current condition of the counter.

### Present State

Current flip-flop outputs.

### Next State

State after the next active clock edge.

### State Table

Shows present state → next state.

### Excitation Table

Determines required flip-flop inputs for a desired transition.
