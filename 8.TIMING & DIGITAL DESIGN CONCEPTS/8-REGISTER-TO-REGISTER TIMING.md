# REGISTER-TO-REGISTER TIMING ⭐⭐⭐⭐⭐

This is one of the **most important Phase 8 topics for VLSI placements**, because it combines everything you've learned so far:

* Clock-to-Q delay
* Propagation delay
* Setup time
* Hold time
* Clock period
* Maximum frequency
* Contamination delay

---

# 1. What is Register-to-Register Timing?

A typical synchronous digital path looks like:

```text id="x7p3m8"
        Combinational Logic

FF1 ───────────────────────────► FF2

 │                                │

 │ Launch                         │ Capture

 │                                │

 └──────────── Clock ─────────────┘
```

* **FF1** = launching/source flip-flop
* **FF2** = capturing/destination flip-flop

Data travels:

**FF1→Combinational Logic→FF2**

---

# 2. Complete Timing Path ⭐⭐⭐⭐⭐

After the clock edge:

```text id="m2q8v5"
Clock edge
```

```
↓
```

FF1

```
↓
```

Clock-to-Q delay

```
↓
```

Combinational logic

```
↓
```

Propagation delay

```
↓
```

FF2

```
↓
```

Setup/Hold check

So there are two separate timing checks:

```text id="r6n3k9"
          REGISTER-TO-REGISTER
```

```
               │

      ┌────────┴────────┐

      ↓                 ↓

    SETUP              HOLD

      ↓                 ↓

  Maximum path       Minimum path

      ↓                 ↓

   tCQ(max)          tCQ(min)

      +                 +

   tpd(max)          tcd(min)

      +                 │

   tsetup              │
```

````

---

# 3. Setup Timing Path ⭐⭐⭐⭐⭐

For setup:

**TCLK≥tCQ(max)+tpd(max)+tsetup**

Therefore:

**TCLK(min)=tCQ(max)+tpd(max)+tsetup**

---

# 4. Example — Setup Check

Given:

**tCQ(max)=2ns**

**tpd(max)=6ns**

**tsetup=2ns**

Then:

**TCLK(min)=2+6+2**

**10ns**

Maximum frequency:

**fmax=1/10ns**

**100MHz**

---

# 5. Hold Timing Path ⭐⭐⭐⭐⭐

For hold:

**tCQ(min)+tcd(min)≥thold**

Notice:

### Setup:

**TCLK is involved**

### Hold:

**TCLK is not directly involved in the basic zero-skew equation**

---

# 6. Example — Hold Check

Given:

**tCQ(min)=1ns**

**tcd(min)=3ns**

**thold=2ns**

Check:

**1+3=4ns**

Since:

**4≥2**

**Hold timing passes**

---

# 7. Complete Example ⭐⭐⭐⭐⭐

Suppose:

**tCQ(max)=2ns**

**tCQ(min)=1ns**

**tpd=5ns**

**tcd=2ns**

**tsetup=2ns**

**thold=3ns**

### Setup:

**TCLK(min)=2+5+2**

**9ns**

Therefore:

**fmax=1/9ns**

**111.11MHz**

### Hold:

**1+2=3ns**

**3≥3**

**Hold timing passes**

So this circuit:

**Passes both setup and hold**

---

# 8. Setup Violation Example

Given:

**TCLK=8ns**

**tCQ(max)=2ns**

**tpd=5ns**

**tsetup=2ns**

Required:

**2+5+2=9ns**

Available:

**8ns**

Therefore:

**8<9**

**Setup violation**

---

# 9. Hold Violation Example

Given:

**tCQ(min)=1ns**

**tcd=1ns**

**thold=3ns**

Then:

**1+1=2ns**

Since:

**2<3**

**Hold violation**

---

# 10. 🔥 The Most Important Table

| Parameter | Setup | Hold |
|---|---|---|
| Check | Data arrives in time for next edge | Data doesn't change too soon |
| Problem | Too late | Too early |
| tCQ | Maximum | Minimum |
| Combinational delay | tpd | tcd |
| Path | Longest | Shortest |
| Clock period | Important | Not directly in basic equation |
| Fix | Speed up | Slow down |

---

# 11. Critical Path ⭐⭐⭐⭐⭐

Suppose a design has:

```text id="y4m8q2"
Path A = 5 ns
````

Path B = 9 ns

Path C = 6 ns

For setup timing, the critical path is:

**Path B**

because:

**9ns**

is the largest delay.

The critical path limits:

**fmax**

---

# 12. Shortest Path

For hold timing, the shortest path is dangerous.

Suppose:

```text id="k2p6n9"
Path A = 5 ns
```

Path B = 2 ns

Path C = 7 ns

The minimum path is:

**Path B**

because:

**2ns**

is the smallest delay.

---

# 13. Setup Slack ⭐⭐⭐⭐⭐

Simplified:

**Slacksetup=TCLK−(tCQ(max)+tpd(max)+tsetup)**

### Positive:

**PASS**

### Zero:

**Meets timing exactly**

### Negative:

**Setup violation**

---

# 14. Hold Slack

**Slackhold=tCQ(min)+tcd(min)−thold**

### Positive:

**PASS**

### Zero:

**Meets timing exactly**

### Negative:

**Hold violation**

---

# 15. Placement Numerical ⭐⭐⭐⭐⭐

Given:

**TCLK=12ns**

**tCQ(max)=2ns**

**tpd=7ns**

**tsetup=2ns**

Find setup slack.

Required:

**2+7+2=11ns**

Slack:

**12−11**

**+1ns**

Therefore:

**Setup passes**

---

# 16. Placement Numerical

Given:

**tCQ(min)=2ns**

**tcd=2ns**

**thold=5ns**

Find hold slack.

**Slack=2+2−5**

**−1ns**

Therefore:

**Hold violation**

---

# 17. How Clock Frequency Affects Timing

If:

**fCLK↑**

then:

**TCLK↓**

Therefore less time is available for:

**tCQ+tpd+tsetup**

So:

**Higher frequency → setup becomes harder**

---

# 18. Important Concept: Hold Doesn't Depend Directly on Clock Period

In the basic zero-skew model:

**tCQ(min)+tcd≥thold**

There is no:

**TCLK**

Therefore:

**Changing clock frequency alone does not directly fix a basic hold violation**

---

# 19. 🔥 Placement Trap

### Q.

A designer reduces the clock period to increase the operating frequency.

Which timing problem is more likely to become difficult?

**Setup**

Because:

**TCLK↓**

---

# 20. 🔥 Another Trap

### Q.

A designer adds buffers to a short data path.

Why?

**To increase minimum delay and improve hold timing**

---

# 21. 🔥 Another Trap

### Q.

Which path determines maximum operating frequency?

**Longest register-to-register path**

More precisely, the path with the largest total maximum timing delay.

---

# 22. Complete Mental Model 🧠

Memorize this:

```text id="8q3m5v"
                  CLOCK
                    │
                    ↓
                   FF1
                    │
             tCQ(max/min)
                    │
                    ↓
          Combinational Logic
                    │
              tpd / tcd
                    │
                    ↓
                   FF2
```

### Setup:

```text id="r6n2k8"
FF1
```

↓

tCQ(max)

↓

Longest combinational path

↓

tpd(max)

↓

FF2

↓

tsetup

### Hold:

```text id="p4v7m1"
FF1
```

↓

tCQ(min)

↓

Shortest combinational path

↓

tcd(min)

↓

FF2

↓

thold

```
```
