# Frequently Asked Placement Questions + Answers

## Timing & Digital Design Concepts ⭐⭐⭐⭐⭐

Below is a **topic-wise placement question bank covering all 24 Phase 8 topics**, in the **same order** as your Phase 8 roadmap.

---

# 8.1 — Propagation Delay

### Q1. What is propagation delay?

**Answer:** Propagation delay is the time taken for a change at the input of a circuit to produce a corresponding valid change at the output.

### Q2. Why is propagation delay important?

**Answer:** It determines how quickly a circuit can respond and directly affects the maximum operating speed of a digital circuit.

### Q3. What happens if propagation delay increases?

**Answer:** The circuit becomes slower, and timing violations can occur at higher operating frequencies.

### Q4. Which timing check is strongly related to maximum path delay?

**Answer:** **Setup timing.**

---

# 8.2 — Contamination Delay

### Q1. What is contamination delay?

**Answer:** It is the minimum time after an input changes before the output can begin to change.

### Q2. Why is contamination delay important?

**Answer:** It is important for determining the earliest time at which new data can propagate through a circuit and is therefore important in hold-time analysis.

### Q3. Which is generally smaller: propagation delay or contamination delay?

**Answer:**

$$
t_{cd} \leq t_{pd}
$$

### Q4. Which timing check is strongly related to minimum path delay?

**Answer:** **Hold timing.**

---

# 8.3 — Propagation vs Contamination Delay

### Q1. What is the main difference?

**Answer:**

* Propagation delay → maximum/valid output response delay
* Contamination delay → minimum delay before output starts changing

### Q2. Which affects setup timing?

**Answer:** Propagation delay.

### Q3. Which affects hold timing?

**Answer:** Contamination delay.

### Q4. Why should contamination delay not be ignored?

**Answer:** Because a very fast data path can cause the next flip-flop to receive new data too early, resulting in a hold violation.

---

# 8.4 — Setup Time

### Q1. What is setup time?

**Answer:** Setup time is the minimum amount of time for which data must remain stable before the active clock edge.

### Q2. What causes a setup violation?

**Answer:** Data arrives too late before the capturing clock edge.

### Q3. How can setup violations generally be fixed?

**Answer:**

* Reduce combinational delay
* Upsize cells
* Reduce load
* Optimize logic
* Improve routing
* Optimize the critical path

### Q4. Setup time is related to which type of path?

**Answer:** **Maximum-delay path.**

---

# 8.5 — Hold Time

### Q1. What is hold time?

**Answer:** Hold time is the minimum amount of time for which data must remain stable after the active clock edge.

### Q2. What causes a hold violation?

**Answer:** Data changes too early after the capturing clock edge.

### Q3. How is a hold violation generally fixed?

**Answer:** By increasing the minimum delay of the data path, commonly by adding delay buffers.

### Q4. Is increasing the clock frequency generally the solution for hold violations?

**Answer:** **No.** Hold violations are primarily related to minimum path delay and clock relationships, not simply the clock period.

---

# 8.6 — Setup Time vs Hold Time ⭐⭐⭐⭐⭐

### Q1. What is the difference?

| Setup                 | Hold                   |
| --------------------- | ---------------------- |
| Before clock edge     | After clock edge       |
| Data arrives too late | Data changes too early |
| Maximum delay         | Minimum delay          |
| Speed up path         | Slow down path         |

### Q2. Which violation can be fixed by adding delay buffers?

**Answer:** Hold violation.

### Q3. Why can fixing setup create a hold violation?

**Answer:** If we make a data path faster to fix setup, data may arrive too early and reduce hold margin.

### Q4. Why can fixing hold affect setup?

**Answer:** Adding delay to fix hold increases the data-path delay and may reduce setup margin.

---

# 8.7 — Clock-to-Q Delay

### Q1. What is clock-to-Q delay?

**Answer:** It is the time between the active clock edge and the corresponding change at the flip-flop's Q output.

### Q2. Why is clock-to-Q delay important?

**Answer:** It contributes to the total register-to-register path delay.

### Q3. In a register-to-register path, what are the major delay components?

**Answer:**

$$
t_{CQ}+t_{comb}+t_{route}
$$

### Q4. If clock-to-Q delay increases, what happens to setup timing?

**Answer:** The available time for combinational logic decreases, making setup timing harder to meet.

---

# 8.8 — Register-to-Register Timing

### Q1. What is a register-to-register path?

**Answer:** A path from the Q output of a launching flip-flop through combinational logic and routing to the D input of a capturing flip-flop.

```text
Launch FF
```

↓

Clock-to-Q

↓

Logic

↓

Routing

↓

Capture FF

### Q2. What determines the maximum operating frequency?

**Answer:** The longest/most timing-critical register-to-register path, together with clock and timing constraints.

### Q3. What happens if the combinational path becomes longer?

**Answer:** Data-path delay increases, reducing setup margin.

### Q4. What happens if the path is extremely short?

**Answer:** It may create a hold-time problem.

---

# 8.9 — Clock Skew ⭐⭐⭐⭐⭐

### Q1. What is clock skew?

**Answer:** Clock skew is the difference in clock arrival time between the launching and capturing sequential elements.

### Q2. Is clock skew always bad?

**Answer:** No. Depending on its direction and magnitude, skew can improve one timing check while worsening another.

### Q3. Can clock skew affect setup?

**Answer:** Yes.

### Q4. Can clock skew affect hold?

**Answer:** Yes.

### Q5. Why is clock skew important in CTS?

**Answer:** CTS attempts to distribute the clock while controlling skew, insertion delay, and signal quality.

---

# 8.10 — Clock Jitter & Uncertainty

### Q1. What is clock jitter?

**Answer:** Clock jitter is the variation of clock-edge timing from its ideal or expected position.

### Q2. What is clock uncertainty?

**Answer:** Clock uncertainty is timing margin used to account for effects such as clock jitter and other clock variations.

### Q3. How does jitter affect timing?

**Answer:** It reduces the available timing margin and can contribute to setup or hold violations.

### Q4. What is the difference?

**Answer:**

* **Jitter** → variation in clock-edge timing
* **Uncertainty** → timing margin accounting for clock-related uncertainty

---

# 8.11 — Metastability ⭐⭐⭐⭐⭐

### Q1. What is metastability?

**Answer:** Metastability is a temporary uncertain state of a flip-flop in which its output is neither reliably 0 nor 1.

### Q2. What commonly causes metastability?

**Answer:** Violating setup/hold requirements, especially when an asynchronous signal is sampled.

### Q3. Where is metastability commonly encountered?

**Answer:** In clock-domain crossings and asynchronous inputs.

### Q4. How can metastability risk be reduced?

**Answer:** Using synchronizer circuits, commonly a two-flip-flop synchronizer for a single-bit control signal.

### Q5. Can metastability be completely eliminated?

**Answer:** No. Its probability can be reduced to a sufficiently low level.

---

# 8.12 — Clock Domain Crossing (CDC) ⭐⭐⭐⭐⭐

### Q1. What is CDC?

**Answer:** CDC occurs when a signal transfers from one clock domain to another clock domain.

### Q2. Why is CDC dangerous?

**Answer:** The receiving clock may sample the signal asynchronously, potentially causing metastability.

### Q3. What is commonly used for a single-bit CDC signal?

**Answer:** A **2-flop synchronizer**.

### Q4. Is a simple 2-flop synchronizer suitable for arbitrary multi-bit data buses?

**Answer:** Not generally. Multi-bit CDC requires appropriate techniques such as handshake protocols, asynchronous FIFOs, or other CDC architectures depending on the application.

### Q5. What is the purpose of a synchronizer?

**Answer:** To reduce the probability that metastability propagates into downstream logic.

---

# 8.13 — Timing Closure & Critical Path ⭐⭐⭐⭐⭐

### Q1. What is timing closure?

**Answer:** Timing closure is the process of optimizing the design until all required timing constraints are satisfied.

### Q2. What is a critical path?

**Answer:** It is the path that most severely limits timing, typically the path with the worst slack for the relevant timing check.

### Q3. How can a critical path be improved?

**Answer:**

* Optimize logic
* Upsize cells
* Reduce load
* Improve buffering
* Improve routing
* Reduce interconnect delay

### Q4. What happens when the critical path is improved?

**Answer:** Timing slack can improve and the maximum achievable frequency may increase.

---

# 8.14 — Static Timing Analysis (STA) ⭐⭐⭐⭐⭐

### Q1. What does STA stand for?

**Answer:**

Static Timing Analysis

### Q2. What does STA do?

**Answer:** STA analyzes timing paths and checks whether timing constraints are satisfied without requiring exhaustive functional simulation.

### Q3. What does STA check?

**Answer:**

* Setup
* Hold
* Clock relationships
* Input/output timing
* False paths
* Multicycle paths

### Q4. Why is STA important?

**Answer:** It provides systematic timing verification across many timing paths and operating conditions.

### Q5. Is STA the same as functional simulation?

**Answer:** No.

**STA** checks timing constraints, while **functional simulation** checks behavior under specific input scenarios.

---

# 8.15 — PVT Corners ⭐⭐⭐⭐⭐

### Q1. What does PVT stand for?

**Answer:**

Process, Voltage, Temperature

### Q2. Why are PVT corners important?

**Answer:** Cell and interconnect behavior changes with manufacturing process, supply voltage, and temperature.

### Q3. What happens when supply voltage decreases?

**Answer:** Cell drive strength generally decreases and delay can increase.

### Q4. Why are multiple PVT corners analyzed?

**Answer:** To ensure the design works reliably across relevant manufacturing and operating conditions.

---

# 8.16 — Timing Derating & OCV

### Q1. What is OCV?

**Answer:**

On-Chip Variation

It represents variations between different parts of the same chip.

### Q2. Why is OCV considered?

**Answer:** Real chips have process and environmental variations, so different cells and paths may not behave identically.

### Q3. What is timing derating?

**Answer:** Timing derating applies a factor to nominal timing values to account for variation and uncertainty.

### Q4. What is the purpose of OCV and derating?

**Answer:** To make timing analysis more realistic and robust against on-chip variations.

---

# 8.17 — Multi-Cycle & False Paths ⭐⭐⭐⭐⭐

### Q1. What is a false path?

**Answer:** A false path is a path that does not have a valid timing relationship for the timing analysis being performed and therefore should not be analyzed as a normal timing path.

### Q2. Why are false paths specified?

**Answer:** To prevent STA from reporting meaningless timing violations on paths that are not functionally required to meet that timing relationship.

### Q3. What is a multicycle path?

**Answer:** A multicycle path is a path intentionally allowed more than one clock cycle to transfer data.

### Q4. Difference between false path and multicycle path?

**Answer:**

**False Path** → Not timed normally

**Multicycle Path** → Timed over multiple cycles

### Q5. Why is incorrectly constraining these paths dangerous?

**Answer:** Incorrect constraints can either produce false timing violations or hide real timing problems.

---

# 8.18 — CTS & Clock Distribution ⭐⭐⭐⭐⭐

### Q1. What is CTS?

**Answer:**

Clock Tree Synthesis

### Q2. Why is CTS required?

**Answer:** To distribute the clock signal to sequential elements while controlling skew, insertion delay, transition, and clock-tree quality.

### Q3. What is clock insertion delay?

**Answer:** The delay from the clock source to the clock pin of a sequential element.

### Q4. What is clock skew?

**Answer:** Difference in clock arrival time between two sequential elements.

### Q5. What are the main goals of CTS?

**Answer:**

* Control skew
* Control insertion delay
* Maintain acceptable slew
* Provide balanced clock distribution

---

# 8.19 — Clock Gating & Low Power ⭐⭐⭐⭐⭐

### Q1. What is clock gating?

**Answer:** Clock gating disables the clock to an inactive block to reduce unnecessary switching activity.

### Q2. What type of power does clock gating mainly reduce?

**Answer:**

Dynamic power

### Q3. Why does clock gating save power?

**Answer:** It prevents unnecessary clock transitions from propagating through inactive sequential logic.

### Q4. What is a disadvantage of clock gating?

**Answer:** It introduces additional clock-control logic and must be implemented carefully to avoid glitches and timing problems.

---

# 8.20 — PPA ⭐⭐⭐⭐⭐

### Q1. What does PPA stand for?

**Answer:**

Power, Performance, Area

### Q2. Why is PPA important?

**Answer:** A practical VLSI design must balance speed, power consumption, and silicon area.

### Q3. What happens when you upsize a cell?

Generally:

```text
Drive strength ↑
```

Delay ↓

Performance ↑

Area ↑

Power may ↑

### Q4. Why is PPA called a trade-off?

**Answer:** Improving one parameter can negatively affect another.

---

# 8.21 — IR Drop & Power Integrity ⭐⭐⭐⭐⭐

### Q1. What is IR drop?

**Answer:** IR drop is the voltage drop caused by current flowing through resistance in the power-delivery network.

$$
V=IR
$$

### Q2. How does IR drop affect timing?

**Answer:** Reduced local supply voltage can reduce cell drive strength and increase cell delay, potentially causing timing violations.

### Q3. What is dynamic IR drop?

**Answer:** A temporary voltage drop caused by high switching activity and increased current demand.

### Q4. How can IR drop be reduced?

**Answer:**

* Strengthen the power grid
* Add power straps
* Add vias
* Use wider power routes
* Reduce localized current demand

### Q5. What is electromigration?

**Answer:** Electromigration is the movement/degradation of metal caused by high current density over time, creating a reliability concern.

---

# 8.22 — Signal Integrity & Crosstalk ⭐⭐⭐⭐⭐

### Q1. What is signal integrity?

**Answer:** Signal integrity is the ability of a signal to maintain acceptable voltage, waveform, and timing characteristics as it propagates.

### Q2. What is crosstalk?

**Answer:** Crosstalk is unwanted interference between nearby interconnects caused by electrical coupling.

### Q3. What is an aggressor?

**Answer:** The switching signal that causes interference.

### Q4. What is a victim?

**Answer:** The signal affected by the aggressor.

### Q5. What is coupling capacitance?

**Answer:** Parasitic capacitance between nearby interconnects that allows switching activity on one wire to affect another.

### Q6. What is crosstalk noise?

**Answer:** An unwanted voltage disturbance induced on a victim net by coupling from nearby switching nets.

### Q7. What is crosstalk delay?

**Answer:** A change in the victim's propagation delay caused by coupling from neighboring signals.

### Q8. How can crosstalk be reduced?

**Answer:**

* Increase wire spacing
* Reduce parallel run length
* Shield sensitive signals
* Optimize routing/buffering

---

# 8.23 — ECO & Timing Closure ⭐⭐⭐⭐⭐

### Q1. What does ECO stand for?

**Answer:**

Engineering Change Order

### Q2. Why are ECOs used?

**Answer:** To make targeted modifications to an existing design, especially for late-stage timing, functional, power, or physical issues.

### Q3. How is a setup violation generally fixed?

**Answer:** Make the data path faster.

Examples:

* Upsize cells
* Reduce load
* Optimize logic
* Improve routing

### Q4. How is a hold violation generally fixed?

**Answer:** Increase the minimum data-path delay, commonly using delay buffers.

### Q5. What is timing closure?

**Answer:** The iterative process of fixing timing violations until the design meets required timing constraints.

### Q6. Why can ECOs affect PPA?

**Answer:** Cell upsizing and additional buffers can increase area and power.

---

# 8.24 — Final Integration ⭐⭐⭐⭐⭐

### Q1. What are the three components of PPA?

**Answer:**

Power + Performance + Area

### Q2. What is the relationship between timing and power?

**Answer:** Techniques used to improve timing, such as upsizing cells or adding buffers, can increase power consumption.

### Q3. What is the relationship between timing and area?

**Answer:** Timing optimization can require larger cells or additional buffers, increasing area.

### Q4. What is signoff?

**Answer:** Signoff is the final verification stage in which the design is checked against required timing, power, physical, signal-integrity, and reliability requirements before tapeout.

### Q5. What is tapeout?

**Answer:** Tapeout is the release of the final design data for semiconductor manufacturing.

### Q6. What is the overall timing-closure flow?

**Answer:**

```text
STA
```

↓

Find violation

↓

Analyze critical path

↓

Apply optimization/ECO

↓

Re-run STA

↓

Check WNS/TNS

↓

Repeat

↓

Signoff

↓

Tapeout

---

# 🔥 TOP 30 QUESTIONS YOU MUST KNOW

If you have limited time before a placement interview, **do not skip these**:

1. What is propagation delay?
2. What is contamination delay?
3. Propagation vs contamination delay?
4. What is setup time?
5. What is hold time?
6. Setup vs hold violation?
7. How do you fix setup violation?
8. How do you fix hold violation?
9. What is clock-to-Q delay?
10. What is clock skew?
11. What is clock jitter?
12. What is metastability?
13. What is CDC?
14. Why is a 2-FF synchronizer used?
15. What is a critical path?
16. What is timing closure?
17. What is STA?
18. What is slack?
19. What are WNS and TNS?
20. What is PVT?
21. What is OCV?
22. What is a false path?
23. What is a multicycle path?
24. What is CTS?
25. What is clock gating?
26. What is PPA?
27. What is IR drop?
28. What is crosstalk?
29. What is ECO?
30. What is signoff/tapeout?

---

# 🧠 FINAL PHASE 8 INTERVIEW MEMORY MAP

```text
                    PHASE 8
```

```text
                   │

    ┌──────────────┼──────────────┐

    ↓              ↓              ↓

  TIMING          CLOCK          POWER

    │              │              │
```

Setup/Hold       Skew/Jitter      PPA

Prop/Contam      CTS              IR Drop

Clock-to-Q       CDC              EM

Critical Path    Metastability

```text
    │

    ↓

   STA

    │
```

```text
┌────┴────┐

↓         ↓

Setup      Hold

│         │

Speed Up   Slow Down

│         │

└────┬────┘
```

```text
    ↓

   ECO

    │

    ↓
```

SI / Crosstalk

```text
    │

    ↓

 SIGNOFF

    │

    ↓

 TAPEOUT
```
