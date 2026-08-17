# FSM STATE REDUCTION / STATE MINIMIZATION ⭐⭐⭐⭐⭐

This is the next topic in your **Phase 7 order**.

The main goal is simple:

> **Reduce the number of states in an FSM without changing its external behavior.**

This is important because fewer states can mean fewer flip-flops and potentially simpler logic.

---

# 1. What is State Reduction?

**State reduction** is the process of eliminating **equivalent states** from an FSM.

Suppose an FSM has:

```text id="m7q3v1"
S0
```

S1

S2

S3

S4

If two states behave identically for all possible future inputs, they may be combined.

Example:

```text id="x5c8n2"
S2 ≡ S4
```

Then we can replace them with one state:

```text id="j3r6p9"
S2
```

So:

**5 states → 4 states**

---

# 2. Why Is State Reduction Used? ⭐⭐⭐⭐⭐

State reduction can help reduce:

* Number of states
* Number of flip-flops
* Combinational logic
* Circuit area
* Potential power consumption

### Important:

**Fewer states → potentially simpler hardware**

---

# 3. Equivalent States ⭐⭐⭐⭐⭐

Two states are **equivalent** if they produce the same observable behavior for every possible input sequence.

In practical FSM minimization, this means their outputs must match appropriately and their transitions must lead to equivalent states.

---

# 4. Simple Example

Consider a Moore FSM:

| State | Input 0 | Input 1 | Output |
| ----- | ------- | ------- | ------ |
| S0    | S1      | S2      | 0      |
| S1    | S1      | S3      | 0      |
| S2    | S1      | S3      | 0      |
| S3    | S3      | S3      | 1      |

Compare S1 and S2:

```text id="f8k2m5"
S1:
```

0 → S1

1 → S3

Output = 0

S2:

0 → S1

1 → S3

Output = 0

They have:

* Same output
* Same next states for every input

Therefore:

**S1≡S2**

They can be merged.

---

# 5. Important Rule ⭐⭐⭐⭐⭐

For two states to be equivalent, you cannot simply check whether their names or one transition are the same.

You need to consider their behavior for **all possible inputs**.

### For a Moore machine:

Equivalent states must have:

1. Same output
2. Equivalent next states for every input

---

# 6. Moore State Equivalence

For Moore:

**Same output + equivalent next states**

Example:

| State | X=0 | X=1 | Y |
| ----- | --- | --- | - |
| A     | B   | C   | 0 |
| D     | B   | C   | 0 |

Therefore:

**A≡D**

if B and C are themselves equivalent/valid corresponding states.

---

# 7. Mealy State Equivalence

For Mealy, outputs are associated with transitions.

Two states are equivalent when, for every input:

* Their outputs are the same
* Their next states are equivalent

Example:

| State | X=0 | X=1 |
| ----- | --- | --- |
| A     | B/0 | C/1 |
| D     | B/0 | C/1 |

Then:

**A≡D**

assuming the corresponding destination states are equivalent.

---

# 8. Why Outputs Matter ⭐⭐⭐⭐⭐

Suppose:

| State | X=0 | X=1 | Output |
| ----- | --- | --- | ------ |
| S1    | S2  | S3  | 0      |
| S4    | S2  | S3  | 1      |

Even though the transitions are identical:

```text id="r5m1x8"
S1:
```

0 → S2

1 → S3

S4:

0 → S2

1 → S3

they **cannot** be merged in a Moore FSM because:

```text id="n2c7q4"
S1 output = 0
```

S4 output = 1

Therefore:

**Different outputs → Not equivalent**

---

# 9. State Minimization Example ⭐⭐⭐⭐⭐

Consider:

| State | 0 | 1 | Output |
| ----- | - | - | ------ |
| A     | B | C | 0      |
| B     | A | D | 0      |
| C     | B | D | 0      |
| D     | D | D | 1      |

First compare states with different outputs.

```text id="k6p3v9"
Output 0:
```

A, B, C

Output 1:

D

So D cannot be equivalent to A/B/C.

Now compare A, B and C.

```text id="w4n8q2"
A:
```

0 → B

1 → C

B:

0 → A

1 → D

C:

0 → B

1 → D

Their transition behavior differs, so they are not all immediately equivalent.

This illustrates why minimization requires systematically checking transition behavior.

---

# 10. Partition Method ⭐⭐⭐⭐⭐

A common method for state minimization is **partitioning**.

Start by dividing states according to their outputs.

For a Moore machine:

```text id="p7m2x5"
Output 0 → Group 1
```

Output 1 → Group 2

Then examine where each state's transitions go.

If two states transition to different groups for the same input, they must be separated.

Repeat until no further splitting is possible.

---

# 11. Initial Partition

Suppose:

| State | Output |
| ----- | ------ |
| A     | 0      |
| B     | 0      |
| C     | 1      |
| D     | 1      |

Initial partition:

**P0={A,B},{C,D}**

States with different outputs are placed in different groups.

---

# 12. Refine the Partition

Now check transitions.

Suppose:

```text id="c4q8m1"
A:
```

0 → A

1 → C

B:

0 → B

1 → C

Both A and B transition into the same **groups**:

```text id="h9v3r6"
Input 0 → group {A,B}
```

Input 1 → group {C,D}

So they may remain equivalent.

If instead:

```text id="y5k2n8"
A:
```

0 → A

1 → C

B:

0 → C

1 → C

Then:

```text id="m7p4x2"
A, input 0 → Group {A,B}
```

B, input 0 → Group {C,D}

Therefore they must be separated.

---

# 13. 🔥 Placement Concept

State minimization is not simply:

> "Find states with the same output."

That's incomplete.

The correct idea is:

**Same output + equivalent future behavior**

---

# 14. State Reduction and Flip-Flops ⭐⭐⭐⭐⭐

Suppose an FSM initially has:

**N=8**

states.

Binary encoding requires:

**⌈log₂8⌉=3**

flip-flops.

If state minimization reduces it to:

**N=5**

then:

**⌈log₂5⌉=3**

flip-flops are still required.

So **fewer states do not always mean fewer flip-flops**.

This is an important placement trap.

---

# 15. Example Where Flip-Flops Actually Reduce

Suppose:

**N=9**

Initially:

**⌈log₂9⌉=4**

flip-flops.

After minimization:

**N=7**

Now:

**⌈log₂7⌉=3**

Therefore:

**4→3 flip-flops**

---

# 16. State Reduction vs State Assignment

Don't confuse them.

### State Reduction

Removes equivalent states.

```text id="q3m8v5"
8 states → 6 states
```

### State Assignment

Assigns binary codes to the states.

```text id="z6c2n9"
S0 → 000
```

S1 → 001

...

### Memory Trick

```text id="k1x7p4"
Reduction → Remove
```

Assignment → Encode

---

# 17. State Minimization vs State Encoding

| State Reduction             | State Encoding                              |
| --------------------------- | ------------------------------------------- |
| Removes equivalent states   | Assigns codes                               |
| Changes number of states    | Doesn't necessarily change number of states |
| Reduces FSM complexity      | Determines hardware representation          |
| Done before/around encoding | Done after states are established           |

---

# 18. Common Placement Questions ⭐⭐⭐⭐⭐

### Q1. What is state minimization?

**Answer:**

Reducing the number of states in an FSM while preserving its external behavior.

---

### Q2. What are equivalent states?

**Answer:**

States that produce identical observable behavior for all possible input sequences.

---

### Q3. Can two Moore states with different outputs be equivalent?

No

---

### Q4. Can two Mealy states be equivalent if their outputs differ for the same input?

No

---

### Q5. What is the purpose of partitioning?

**Answer:**

To systematically divide states into groups of potentially equivalent states and refine those groups until equivalence is determined.

---

### Q6. Does reducing states always reduce the number of flip-flops?

No

It depends on whether the reduced state count crosses a power-of-two boundary.

---

### Q7. What is the first step in Moore state minimization?

**Partition states according to their outputs**

---

# 19. 🔥 Numerical Placement Questions

### Q8.

An FSM has 15 states.

How many binary state flip-flops?

**⌈log₂15⌉=4**

4

If minimization reduces it to 8 states:

**⌈log₂8⌉=3**

Therefore:

**3**

---

### Q9.

An FSM has 7 states and is reduced to 5 states.

Before:

**⌈log₂7⌉=3**

After:

**⌈log₂5⌉=3**

Therefore:

**Number of binary state FFs remains 3**

---

# 🧠 QUICK REVISION

```text id="e5r2m8"
STATE MINIMIZATION
────────────────────────

Goal:

Reduce FSM states without changing behavior


Equivalent states:

→ Same observable behavior

→ Same outputs

→ Equivalent future transitions


Moore:

→ Same output

→ Equivalent next states


Mealy:

→ Same transition outputs

→ Equivalent next states


Partitioning:

1. Group by output

2. Check transitions

3. Split groups if needed

4. Repeat until stable


Important:

Fewer states ≠ always fewer FFs

### 🔥 Remember:

Reduction = Remove equivalent states

Assignment = Give states binary codes
```
