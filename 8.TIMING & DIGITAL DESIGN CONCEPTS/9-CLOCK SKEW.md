# &#x20;CLOCK SKEW ⭐⭐⭐⭐⭐

Now we continue in the same order.

Clock skew is **very frequently asked in VLSI interviews and placement tests**, especially questions involving setup/hold violations.

---

# 1. What is Clock Skew?

**Clock skew** is the difference in arrival time of the clock signal at two different sequential elements.

For a register-to-register path:

```text id="u6n3p8"
                 Clock
                   │
          ┌────────┴────────┐
          ↓                 ↓
         FF1               FF2
      Launch clock      Capture clock
```

The clock may not reach FF1 and FF2 at exactly the same time.

Therefore:

**Clock Skew=difference in clock arrival times**

---

# 2. Example

Suppose:

* Clock reaches FF1 at **5 ns**
* Clock reaches FF2 at **7 ns**

Then:

**Skew=7−5**

**2ns**

FF2 receives the clock **2 ns later** than FF1.

---

# 3. Positive and Negative Clock Skew ⭐⭐⭐⭐⭐

This is extremely important.

Define:

**tskew=tcapture−tlaunch**

---

## Positive Clock Skew

Capture clock arrives **later** than launch clock.

```text id="g1q7m4"
FF1 clock → 5 ns
```

FF2 clock → 7 ns

Skew = +2 ns

**Positive skew**

---

## Negative Clock Skew

Capture clock arrives **earlier** than launch clock.

```text id="x5n2k8"
FF1 clock → 7 ns
```

FF2 clock → 5 ns

Skew = -2 ns

**Negative skew**

---

# 4. Memory Trick 🔥

```text id="m8r3v1"
Capture LATE
```

```
 ↓
```

Positive skew

Capture EARLY

```
 ↓
```

Negative skew

---

# 5. Effect of Clock Skew on Setup Timing ⭐⭐⭐⭐⭐

This is one of the most important questions.

For a simple setup equation:

**TCLK≥tCQ(max)+tpd(max)+tsetup−tskew**

where:

**tskew=tcapture−tlaunch**

---

## Positive Skew

Capture clock arrives later.

Therefore more time is available for data to reach FF2.

So positive skew generally:

**Improves setup timing**

---

## Negative Skew

Capture clock arrives earlier.

Less time is available.

Therefore:

**Negative skew worsens setup timing**

---

# 6. Example — Positive Skew

Given:

**tCQ=2ns**

**tpd=6ns**

**tsetup=2ns**

**tskew=+1ns**

Then:

**TCLK(min)=2+6+2−1**

**9ns**

Without skew:

**2+6+2=10ns**

So positive skew improves setup timing by:

**1ns**

---

# 7. Effect on Hold Timing ⭐⭐⭐⭐⭐

This is where many placement questions try to confuse you.

For a basic hold equation:

**tCQ(min)+tcd(min)+tskew≥thold**

---

## Positive Skew

Capture clock arrives later.

This gives the new data **less restriction?**

Actually, for hold timing, a later capture edge extends the period during which the old data must remain stable.

Therefore:

**Positive skew worsens hold timing**

---

## Negative Skew

Capture clock arrives earlier.

The hold requirement is effectively easier to satisfy.

Therefore:

**Negative skew improves hold timing**

---

# 8. 🔥 Golden Rule

This is extremely important:

**Positive skew→Setup better→Hold worse**

**Negative skew→Setup worse→Hold better**

### Memory trick:

```text id="b6k2q9"
Positive skew:
```

SETUP 👍

HOLD  👎

Negative skew:

SETUP 👎

HOLD  👍

---

# 9. Why Does Positive Skew Help Setup?

Imagine:

```text id="v3m8x5"
Launch edge       Capture edge
```

```
 ↑                  ↑

 │                  │

 └────── MORE ──────┘

        TIME
```

The capture clock arrives later.

Therefore the data has more time to travel.

---

# 10. Why Does Positive Skew Hurt Hold?

The capture edge is later.

Therefore FF2 must continue seeing stable old data for longer.

If new data arrives too quickly:

**Hold violation**

can occur.

---

# 11. Numerical — Setup with Skew

Given:

**TCLK=10ns**

**tCQ=2ns**

**tpd=6ns**

**tsetup=2ns**

**tskew=+1ns**

Required:

**2+6+2−1=9ns**

Available:

**10ns**

Setup slack:

**10−9**

**+1ns**

Therefore:

**Setup passes**

---

# 12. Numerical — Hold with Skew

Given:

**tCQ(min)=1ns**

**tcd=2ns**

**thold=3ns**

**tskew=+1ns**

Check:

**1+2+1=4ns**

Since:

**4≥3**

Hold passes in this example.

But notice something important:

Without skew:

**1+2=3ns**

It was exactly at the limit.

Positive skew increased the required hold margin and can therefore make marginal hold paths worse.

---

# 13. Placement Trap ⭐⭐⭐⭐⭐

### Q.

Positive clock skew generally:

A. Improves setup and hold
B. Worsens setup and hold
C. Improves setup but worsens hold
D. Worsens setup but improves hold

Correct:

**C**

---

# 14. Another Common Question

### Q.

Negative clock skew generally:

**Worsens setup but improves hold**

---

# 15. Zero Clock Skew

If clock arrives at both flip-flops at the same time:

**tcapture=tlaunch**

Then:

**tskew=0**

This is called:

**Zero skew**

---

# 16. Why Does Clock Skew Occur?

Real clock networks contain:

* Different wire lengths
* Different routing paths
* Buffer delays
* Clock-tree structure
* Load differences
* Process variation
* Voltage variation
* Temperature variation

Therefore clock edges may reach different flip-flops at different times.

---

# 17. Clock Tree ⭐⭐⭐⭐

A clock signal is distributed through a **clock distribution network**.

A simplified structure:

```text id="z7m4q1"
                    Clock Source
                         │
                    Clock Buffer
                         │
              ┌──────────┴──────────┐
              ↓                     ↓
           Buffer                 Buffer
              │                     │
              ↓                     ↓
             FF1                   FF2
```

The goal of clock-tree design is to distribute the clock with controlled:

**Skew**

and delay.

---

# 18. Clock Skew vs Clock Jitter

Do not confuse these.

### Clock Skew

Difference in clock arrival time between **different sequential elements**.

**FF1 clock arrival vs FF2 clock arrival**

### Clock Jitter

Variation of a clock edge's timing from its ideal/expected position, often across cycles.

**Clock edge timing variation**

---

# 19. Interview Question ⭐⭐⭐⭐⭐

### Q. Is clock skew always bad?

Not necessarily.

Clock skew can sometimes be intentionally managed to improve timing.

For example:

**Positive skew can improve setup timing**

But it can simultaneously hurt hold timing.

Therefore clock-tree design tries to control skew carefully.

---

# 20. Important Placement Summary

```text id="k5n2v8"
                 CLOCK SKEW
                     │
          ┌──────────┴──────────┐
          ↓                     ↓
       Positive              Negative
          │                     │
    Capture LATE           Capture EARLY
          │                     │
      SETUP 👍                SETUP 👎
      HOLD  👎                HOLD  👍
```

---

# 🧠 QUICK REVISION

**tskew=tcapture−tlaunch**

### Positive skew:

**Capture later**

**Setup improves**

**Hold worsens**

### Negative skew:

**Capture earlier**

**Setup worsens**

**Hold improves**

### Basic equations:

**TCLK≥tCQ(max)+tpd(max)+tsetup−tskew**

**tCQ(min)+tcd(min)+tskew≥thold**
