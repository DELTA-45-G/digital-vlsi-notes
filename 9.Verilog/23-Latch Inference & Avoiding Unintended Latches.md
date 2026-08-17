# LATCH INFERENCE & AVOIDING UNINTENDED LATCHES

## ⭐⭐⭐⭐⭐ Placement Very Important

This is one of the **most frequently asked Verilog/RTL interview topics** because unintended latches are a common RTL coding problem.

---

# 1. What is a Latch?

A **latch** is a storage element that is **level-sensitive**.

It can hold its previous value when its enable/control condition is inactive.

For example, an enabled D-latch behaves conceptually as:

```text
Enable = 1 → Q follows D
Enable = 0 → Q holds previous value
```

---

# 2. What is Latch Inference?

**Latch inference** means the synthesis tool creates a latch because the RTL code implies that a signal must **remember its previous value**.

Example:

```verilog
always @(*) begin

    if (enable)
        q = d;

end
```

What happens when:

```text
enable = 1 → q = d
enable = 0 → q must retain old q
```

The requirement to retain the old value implies storage.

Therefore synthesis may infer a latch.

---

# 3. Why Does a Latch Get Inferred?

The most common reason is:

> **Incomplete assignment in combinational logic.**

Example:

```verilog
always @(*) begin

    if (sel)
        y = a;

end
```

When `sel = 0`, there is no assignment to `y`.

Therefore:

```text
y must remember its previous value
```

which requires storage.

---

# 4. Unintended Latch ⭐⭐⭐⭐⭐

An unintended latch occurs when the designer wanted:

```text
Combinational logic
```

but the coding style accidentally describes:

```text
Latch
```

Example:

```verilog
always @(*) begin

    if (enable)
        y = a;

end
```

If the intention was simply:

```text
enable = 1 → y = a
enable = 0 → y = 0
```

then the RTL is incomplete.

---

# 5. How to Fix the Latch?

### Method 1 — Add `else`

```verilog
always @(*) begin

    if (enable)
        y = a;
    else
        y = 0;

end
```

Now `y` is assigned in both conditions.

---

# 6. Method 2 — Give Default Assignment ⭐⭐⭐⭐⭐

A very common RTL coding style is:

```verilog
always @(*) begin

    y = 0;

    if (enable)
        y = a;

end
```

The default assignment guarantees that `y` receives a value.

Then:

```text
enable = 1 → y = a
enable = 0 → y = 0
```

No latch is required.

---

# 7. Latch in `case` Statement

Consider:

```verilog
always @(*) begin

    case (sel)

        2'b00: y = a;
        2'b01: y = b;

    endcase

end
```

What happens for:

```text
sel = 2'b10
sel = 2'b11
```

There is no assignment.

Therefore a latch may be inferred.

---

# 8. Fixing Latch in `case`

Use `default`:

```verilog
always @(*) begin

    case (sel)

        2'b00: y = a;
        2'b01: y = b;

        default: y = 0;

    endcase

end
```

Now every possible condition has an assignment.

---

# 9. Another Safe Style

You can also assign a default before the case:

```verilog
always @(*) begin

    y = 0;

    case (sel)

        2'b00: y = a;
        2'b01: y = b;

    endcase

end
```

This is often convenient when there are many outputs.

---

# 10. Multiple Outputs and Latches

Consider:

```verilog
always @(*) begin

    if (enable) begin

        y = a;
        z = b;

    end

end
```

Both:

```text
y
z
```

can infer latches because neither is assigned when:

```text
enable = 0
```

Fix:

```verilog
always @(*) begin

    y = 0;
    z = 0;

    if (enable) begin

        y = a;
        z = b;

    end

end
```

---

# 11. Latch Inference in Nested `if`

Problem:

```verilog
always @(*) begin

    if (a) begin

        if (b)
            y = 1;

    end

end
```

What happens when:

```text
a = 1, b = 0
```

No assignment to `y`.

Also when:

```text
a = 0
```

No assignment.

Therefore latch inference is possible.

---

# 12. Fix Nested `if`

```verilog
always @(*) begin

    y = 0;

    if (a) begin

        if (b)
            y = 1;

    end

end
```

Now:

```text
y = 0
```

is the default.

---

# 13. Latch vs Flip-Flop ⭐⭐⭐⭐⭐

This is a common placement question.

| Latch                                                     | Flip-Flop                          |
| --------------------------------------------------------- | ---------------------------------- |
| Level-sensitive                                           | Edge-triggered                     |
| Transparent during active level                           | Captures at clock edge             |
| Can be enabled by a level                                 | Usually triggered by edge          |
| Can be inferred from incomplete combinational assignments | Usually described using clock edge |

---

# 14. Latch Example

Conceptually:

```text
Enable = 1
    ↓
Q follows D

Enable = 0
    ↓
Q holds previous value
```

---

# 15. Flip-Flop Example

```verilog
always @(posedge clk) begin
    q <= d;
end
```

The flip-flop updates only on the active clock edge.

---

# 16. Latch vs Combinational Logic

### Combinational:

```text
Output depends only on current input
```

### Latch:

```text
Output can depend on previous value
```

Therefore:

```text
Combinational → no storage
Latch → storage
```

---

# 17. Why Are Unintended Latches Bad? ⭐⭐⭐⭐⭐

Unintended latches can cause:

* Timing problems
* Difficult static timing analysis
* Unexpected storage behavior
* Glitches
* Complex verification
* Difficult timing closure
* Unexpected hardware

Therefore designers usually avoid unintended latches unless a latch is intentionally required.

---

# 18. Latch Inference and Synthesis

Remember:

```text
RTL Code
   ↓
Synthesis
   ↓
Hardware
```

If RTL implies:

```text
"Hold previous value"
```

the synthesis tool may create storage.

That storage could be:

```text
Latch
```

depending on the coding structure.

---

# 19. Example of Intentional Latch

Not every latch is an error.

A latch can be intentionally designed.

Example:

```verilog
always @(*) begin

    if (enable)
        q = d;

end
```

If the actual design requirement is:

```text
enable = 1 → transparent
enable = 0 → hold
```

then this code can intentionally describe a latch.

The problem is only when the designer **wanted combinational logic** but accidentally created storage.

---

# 20. Unintended vs Intentional Latch

```text
Intentional latch
      ↓
Storage is required
      ↓
Correct design
```

```text
Unintended latch
      ↓
Storage was not intended
      ↓
RTL coding mistake
```

---

# 21. Latch Inference from Missing `else`

Classic interview example:

```verilog
always @(*) begin

    if (sel)
        y = a;

end
```

### Question:

Will this infer a latch?

### Answer:

**Yes, potentially.**

Because when:

```text
sel = 0
```

`y` is not assigned and must retain its previous value.

---

# 22. Corrected Version

```verilog
always @(*) begin

    if (sel)
        y = a;
    else
        y = 0;

end
```

Now the output is fully specified.

---

# 23. Another Interview Example

### Code:

```verilog
always @(*) begin

    case (sel)

        2'b00: y = a;
        2'b01: y = b;

    endcase

end
```

### Question:

Can this infer a latch?

**Answer:**

Yes, because `y` has no assignment for:

```text
2'b10
2'b11
```

Add:

```verilog
default: y = 0;
```

---

# 24. Default Assignment Technique ⭐⭐⭐⭐⭐

This is an extremely useful pattern:

```verilog
always @(*) begin

    // Default assignments

    y = 0;
    z = 0;

    // Override when required

    if (enable) begin

        y = a;
        z = b;

    end

end
```

Think:

```text
Default first
     ↓
Override later
```

---

# 25. Latch Inference in Combinational ALU

Bad:

```verilog
always @(*) begin

    case (op)

        2'b00: result = a + b;
        2'b01: result = a - b;
        2'b10: result = a & b;

    endcase

end
```

No case for:

```text
11
```

Potential latch.

---

# 26. Correct ALU

```verilog
always @(*) begin

    case (op)

        2'b00: result = a + b;
        2'b01: result = a - b;
        2'b10: result = a & b;
        2'b11: result = a | b;

        default: result = 0;

    endcase

end
```

---

# 27. Latch Inference in FSM Logic

FSM next-state logic can also accidentally infer latches.

Bad:

```verilog
always @(*) begin

    if (start)
        next_state = RUN;

end
```

What happens when:

```text
start = 0
```

`next_state` retains its previous value.

Potential latch.

---

# 28. Better FSM Coding

Use a default:

```verilog
always @(*) begin

    next_state = IDLE;

    if (start)
        next_state = RUN;

end
```

Or:

```verilog
always @(*) begin

    case (state)

        IDLE: begin

            if (start)
                next_state = RUN;
            else
                next_state = IDLE;

        end

        RUN: begin
            next_state = IDLE;
        end

        default: begin
            next_state = IDLE;
        end

    endcase

end
```

---

# 29. Latch Inference vs Incomplete Sensitivity List

These are related but **not exactly the same problem**.

### Incomplete assignment:

Can cause:

```text
Latch inference
```

### Incomplete sensitivity list:

Can cause:

```text
Simulation mismatch
```

Example:

```verilog
always @(a) begin
    y = a & b;
end
```

If `b` changes, the block may not execute in simulation.

Using:

```verilog
always @(*)
```

avoids this common sensitivity-list problem.

---

# 30. Important Distinction ⭐⭐⭐⭐⭐

```text
Incomplete assignment
        ↓
Possible latch during synthesis
```

```text
Incomplete sensitivity list
        ↓
Incorrect simulation behavior
```

Do not confuse the two.

---

# 31. Latch Warning from Synthesis Tools

Synthesis tools may report messages such as:

```text
Latch inferred for signal y
```

This is a warning that the RTL requires storage behavior.

The designer should then ask:

> Was this latch intentional?

If **yes**, document/design it appropriately.

If **no**, fix the RTL.

---

# 32. How to Avoid Unintended Latches

### Rule 1

Use:

```verilog
always @(*)
```

for combinational logic.

### Rule 2

Assign every output for every possible condition.

### Rule 3

Use `else` where appropriate.

### Rule 4

Use `default` in `case`.

### Rule 5

Use default assignments at the beginning of combinational blocks.

### Rule 6

Review synthesis warnings.

---

# 33. Best-Practice Combinational Template

```verilog
always @(*) begin

    // Default values

    y = 0;
    z = 0;

    // Logic

    case (sel)

        2'b00: begin

            y = a;
            z = b;

        end

        2'b01: begin

            y = c;
            z = d;

        end

        default: begin

            // Keep defaults

        end

    endcase

end
```

This style is highly useful in placement coding questions.

---

# 34. Best-Practice Sequential Template

```verilog
always @(posedge clk) begin

    if (reset)
        q <= 0;
    else
        q <= d;

end
```

This describes a register/flip-flop rather than an unintended latch.

---

# 35. Latch vs Register Coding

### Latch:

```verilog
always @(*) begin

    if (enable)
        q = d;

end
```

### Flip-flop:

```verilog
always @(posedge clk) begin

    q <= d;

end
```

The difference is:

```text
Latch → level-sensitive enable
FF    → clock edge
```

---

# ⭐ Frequently Asked Placement Questions

## Q1. What is latch inference?

**Answer:** Latch inference occurs when synthesis determines from the RTL that a signal must retain its previous value under some conditions, resulting in latch hardware.

---

## Q2. What is the most common cause of unintended latch inference?

**Answer:** Incomplete assignment in combinational logic.

---

## Q3. How can you avoid unintended latches?

**Answer:**

* Assign outputs in all conditions
* Use `else`
* Use `default`
* Use default assignments
* Use proper combinational coding style

---

## Q4. Does every incomplete `if` statement infer a latch?

**Answer:** Not necessarily. It depends on whether the affected signal requires retaining its previous value and whether the surrounding logic provides another complete assignment. In combinational RTL, incomplete assignments commonly lead to latch inference.

---

## Q5. Can a `case` statement infer a latch?

**Answer:** Yes, if an output is not assigned for all possible conditions.

---

## Q6. How do you prevent latch inference in `case`?

**Answer:** Provide a `default` assignment or give the output a default value before the `case`.

---

## Q7. Why is a latch called level-sensitive?

**Answer:** Because it can remain transparent throughout an active enable level rather than capturing data only at a clock edge.

---

## Q8. What is the difference between latch and flip-flop?

**Answer:**

```text
Latch     → level-sensitive
Flip-flop → edge-triggered
```

---

## Q9. Are all latches bad?

**Answer:** No. A latch is not inherently bad. An intentionally designed latch can be valid. The problem is an **unintended latch**.

---

## Q10. What happens if synthesis reports "latch inferred"?

**Answer:** Check whether the latch was intentionally required. If not, inspect the combinational RTL for incomplete assignments.

---

## Q11. Can default assignments prevent latches?

**Answer:** Yes. Giving every output a default value at the beginning of a combinational block is a common technique.

---

## Q12. What is the difference between incomplete assignment and incomplete sensitivity list?

**Answer:**

```text
Incomplete assignment
→ may infer latch
```

```text
Incomplete sensitivity list
→ may cause simulation mismatch
```

---

# 🔥 Placement Rapid-Fire

**Incomplete combinational assignment?**

→ Possible latch

**Missing `else`?**

→ Can cause latch

**Missing `default`?**

→ Can cause latch

**Best combinational sensitivity?**

→ `always @(*)`

**Latch sensitivity?**

→ Level-sensitive

**Flip-flop sensitivity?**

→ Clock edge

**Latch stores data?**

→ ✅ Yes

**Are all latches bad?**

→ ❌ No

**Unintended latch?**

→ Usually an RTL coding problem

**Easy latch prevention technique?**

→ Default assignment

**Case latch prevention?**

→ `default`

**Sequential register?**

→ `always @(posedge clk)`

---

# 🧠 9.23 QUICK REVISION

```text
          COMBINATIONAL RTL
                  │
                  ↓
        Every output assigned?
             /          \
           YES           NO
            │             │
            ↓             ↓
     Combinational     Previous value
         logic            required
                          │
                          ↓
                    LATCH INFERRED
```

### ⭐ Golden Rules

```text
Incomplete combinational assignment → possible latch
Use default assignments to avoid unintended latches
Use else/default for complete combinational coverage
Latch → level-sensitive
Flip-flop → edge-triggered
Unintended latch ≠ intentional latch
```
