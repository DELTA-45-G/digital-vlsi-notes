# COUNTERS ⭐⭐⭐⭐⭐

Now we start **Counters**.

Counters are very important for ECE/VLSI placements because questions frequently involve **count sequence, MOD number, number of flip-flops, frequency division, ripple vs synchronous counters**, etc.

---

# 1. What is a Counter?

A **counter** is a sequential circuit that goes through a predetermined sequence of states in response to clock pulses.

In simple words:

> A counter counts clock pulses.

Example of a 3-bit binary up counter:

```text id="q3t8m1"
000
```

↓

001

↓

010

↓

011

↓

100

↓

101

↓

110

↓

111

↓

000

Each clock pulse causes the counter to move to the next state.

---

# 2. Counter Uses

Counters are used for:

* Counting events
* Frequency division
* Timers
* Digital clocks
* Address generation
* Control circuits
* Sequence generation

---

# 3. Number of States in an n-bit Counter ⭐⭐⭐⭐⭐

An n-bit binary counter can represent:

**2ⁿ**

different states.

### Example

A 3-bit counter:

**2³=8**

states:

**000→111**

Therefore:

**8 states**

---

# 4. 2-Bit Counter

A 2-bit counter has:

**2²=4**

states.

The sequence is:

```text id="j8v2n5"
00
```

↓

01

↓

10

↓

11

↓

00

Therefore:

**MOD−4**

---

# 5. 3-Bit Counter

A 3-bit counter has:

**2³=8**

states.

```text id="c4m7x9"
000
```

001

010

011

100

101

110

111

000

Therefore:

**MOD−8**

---

# 6. What is MOD? ⭐⭐⭐⭐⭐

**MOD** represents the number of distinct states through which a counter cycles before repeating.

For a normal n-bit binary counter:

**MOD=2ⁿ**

### Example

4-bit binary counter:

**MOD=2⁴=16**

So it counts:

**0→15**

and then returns to:

**0**

---

# 7. Up Counter ⭐⭐⭐⭐⭐

An **up counter** counts in increasing order.

Example:

```text id="z5r1p8"
000
```

001

010

011

100

101

110

111

In decimal:

```text id="k7n3q2"
0
```

1

2

3

4

5

6

7

Then it returns to 0.

Therefore:

**Up counter → increasing count**

---

# 8. Down Counter ⭐⭐⭐⭐⭐

A **down counter** counts in decreasing order.

Example of a 3-bit down counter:

```text id="v2s6m4"
111
```

110

101

100

011

010

001

000

111

In decimal:

```text id="a8k1w5"
7
```

6

5

4

3

2

1

0

7

Therefore:

**Down counter → decreasing count**

---

# 9. Up/Down Counter ⭐⭐⭐⭐⭐

An **up/down counter** can count in either direction.

A control input determines the direction.

For example:

**Control=1→Up**

**Control=0→Down**

The exact polarity depends on the circuit design.

Example:

```text id="m6c9x3"
UP:
```

**000 → 001 → 010 → 011 → ...**

DOWN:

**111 → 110 → 101 → 100 → ...**

---

# 10. Counter and Flip-Flops ⭐⭐⭐⭐⭐

An n-bit binary counter generally requires:

**n flip-flops**

### Example

4-bit counter:

**4 flip-flops**

Number of states:

**2⁴=16**

---

# 11. Counter as Frequency Divider ⭐⭐⭐⭐⭐

A counter can be used to divide the clock frequency.

For a binary counter, each successive bit toggles at half the frequency of the previous bit.

For example, if:

**fCLK=100MHz**

then the first divided output is approximately:

**50MHz**

the next:

**25MHz**

the next:

**12.5MHz**

So:

**fQn=fCLK/2ⁿ⁺¹**

for the n-th bit when counting bit positions starting at 0.

More generally, the k-th bit divides the clock by:

**2ᵏ⁺¹**

---

# 12. MOD-N Counter ⭐⭐⭐⭐⭐

A counter that has exactly N states is called a:

**MOD-N counter**

### Example

MOD-10 counter:

```text id="y8p4c6"
0
```

1

2

3

4

5

6

7

8

9

0

It has:

**10 states**

---

# 13. How Many Flip-Flops for MOD-N? ⭐⭐⭐⭐⭐

We need the smallest n satisfying:

**2ⁿ≥N**

### Example: MOD-10

**2³=8<10**

**2⁴=16≥10**

Therefore:

**4 flip-flops**

There will be:

**16−10=6**

unused states.

---

# 14. Important Difference

Don't confuse:

### Number of flip-flops

with

### Number of states

For a 4-bit counter:

**4 flip-flops**

but:

**16 states**

because:

**2⁴=16**

---

# 15. Counter Types We'll Study

Phase 6 will cover:

```text id="f6w2j9"
Counters
   │
   ├── Up Counter
   ├── Down Counter
   ├── Up/Down Counter
   │
   ├── Asynchronous Counter
   │
   ├── Synchronous Counter
   │
   ├── MOD-N Counter
   │
   ├── Ring Counter
   │
   ├── Johnson Counter
   │
   └── Counter Design
```

We will study them **in this order**.

---

# 🧠 Quick Revision

```text id="r5q8n2"
COUNTER
────────────────────────

Counter:

→ Sequential circuit

→ Counts clock pulses

n-bit binary counter:

→ n flip-flops

→ 2^n states

Up counter:

→ Increasing sequence

Down counter:

→ Decreasing sequence

Up/Down counter:

→ Can count both directions

MOD-N:

→ N states

Flip-flops required for MOD-N:

2^n ≥ N

Normal n-bit binary counter:

MOD = 2^n
```
