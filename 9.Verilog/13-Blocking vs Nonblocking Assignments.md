# BLOCKING (`=`) vs NONBLOCKING (`<=`) ASSIGNMENTS ⭐⭐⭐⭐⭐

This is one of the **most frequently asked Verilog interview topics** because it is directly related to **combinational logic, sequential logic, simulation behavior, and RTL coding style**.

---

# 1. What is a Blocking Assignment?

A blocking assignment uses:

```verilog
=
```

Example:

```verilog
always @(*) begin
    y = a & b;
end
```

The assignment executes **immediately** and the next statement waits until it completes.

### Memory trick:

> **Blocking = execute now, then move to the next statement.**

---

# 2. What is a Nonblocking Assignment?

A nonblocking assignment uses:

```verilog
<=
```

Example:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

The update is scheduled rather than taking effect immediately within the current procedural execution.

### Memory trick:

> **Nonblocking = schedule the update, then continue.**

---

# 3. Basic Difference ⭐⭐⭐⭐⭐

| Blocking `=`                            | Nonblocking `<=`                        |
| --------------------------------------- | --------------------------------------- |
| Uses `=`                                | Uses `<=`                               |
| Executes immediately                    | Update is scheduled                     |
| Next statement sees updated value       | Next statement generally sees old value |
| Common for combinational logic          | Common for sequential logic             |
| Models step-by-step procedural behavior | Models simultaneous register updates    |

---

# 4. Simple Example

Consider:

```verilog
always @(*) begin
    a = b;
    c = a;
end
```

Suppose:

```text
b = 1
```

First:

```text
a = 1
```

Then:

```text
c = a
```

Therefore:

```text
a = 1
c = 1
```

Because blocking assignment updates `a` immediately.

---

# 5. Nonblocking Example

Now:

```verilog
always @(posedge clk) begin
    a <= b;
    c <= a;
end
```

Suppose before the clock:

```text
a = 0
b = 1
c = 0
```

After the clock:

```text
a = 1
c = 0
```

Why?

Because `c <= a` uses the **old value of** **`a`** from before the clock event.

---

# 6. Why is This Important?

This behavior allows nonblocking assignments to correctly model flip-flops.

Consider:

```verilog
always @(posedge clk) begin
    q1 <= d;
    q2 <= q1;
end
```

Hardware:

```text
D → FF1 → FF2
```

At each clock edge:

```text
FF1 captures D
FF2 captures previous Q1
```

That is exactly what nonblocking assignment models.

---

# 7. Blocking Assignment for Combinational Logic ⭐⭐⭐⭐⭐

Typical coding style:

```verilog
always @(*) begin
    y = a & b;
end
```

Here:

```text
combinational logic
        ↓
blocking =
```

---

# 8. Nonblocking Assignment for Sequential Logic ⭐⭐⭐⭐⭐

Typical coding style:

```verilog
always @(posedge clk) begin
    q <= d;
end
```

Here:

```text
sequential logic
        ↓
nonblocking <=
```

### Placement memory rule:

```text
Combinational → =
Sequential    → <=
```

---

# 9. Example — Blocking in Combinational Logic

```verilog
always @(*) begin
    x = a & b;
    y = x | c;
end
```

Because `x` is updated immediately:

```text
x = a & b
```

```text
y = x | c
```

So `y` uses the newly calculated `x`.

---

# 10. What if Nonblocking is Used Here?

```verilog
always @(*) begin
    x <= a & b;
    y <= x | c;
end
```

Now `y` may use the **previous value of** **`x`** during the current evaluation.

This can introduce simulation behavior that does not match the intended simple combinational calculation.

Therefore, for ordinary combinational procedural logic:

```text
Use =
```

---

# 11. Sequential Example

Consider:

```verilog
always @(posedge clk) begin
    q1 <= d;
    q2 <= q1;
end
```

This represents:

```text
        ┌─────┐      ┌─────┐
D ─────→│ FF1 │─────→│ FF2 │
        └─────┘      └─────┘

           Q1           Q2
```

At clock edge:

```text
Q1 ← D
Q2 ← old Q1
```

This is exactly the behavior desired for a two-stage pipeline.

---

# 12. What Happens If Blocking Is Used?

```verilog
always @(posedge clk) begin
    q1 = d;
    q2 = q1;
end
```

Suppose:

```text
d = 1
q1 = 0
q2 = 0
```

After the clock:

```text
q1 = 1
q2 = 1
```

because:

```text
q1 = d
```

updates immediately, and then:

```text
q2 = q1
```

sees the new value.

This does **not** model two independent flip-flops correctly.

---

# 13. Nonblocking Gives Simultaneous Register Behavior

Consider:

```verilog
always @(posedge clk) begin
    q1 <= d;
    q2 <= q1;
    q3 <= q2;
end
```

This models:

```text
D → FF1 → FF2 → FF3
```

At every clock:

```text
q1 ← old d
q2 ← old q1
q3 ← old q2
```

This is a very important RTL pattern.

---

# 14. Blocking Assignment — Execution Order

Consider:

```verilog
a = b;
c = a;
d = c;
```

The execution is:

```text
a gets b
   ↓
c gets new a
   ↓
d gets new c
```

Therefore statement order matters.

---

# 15. Nonblocking Assignment — Update Scheduling

Consider:

```verilog
a <= b;
c <= a;
d <= c;
```

Conceptually:

```text
All RHS values are evaluated
        ↓
Updates are scheduled
        ↓
Values update together
```

Therefore:

```text
a ← old b
c ← old a
d ← old c
```

---

# 16. Important Interview Question ⭐⭐⭐⭐⭐

### What is the main difference between blocking and nonblocking assignments?

**Answer:**

> A blocking assignment updates the left-hand side immediately before proceeding to the next statement, while a nonblocking assignment schedules the update so that sequential assignments can model simultaneous register behavior.

---

# 17. Why is `<=` Preferred for Flip-Flops?

Because flip-flops update their outputs based on the input values captured at the clock edge.

For example:

```verilog
always @(posedge clk) begin
    q1 <= d;
    q2 <= q1;
end
```

Both flip-flops effectively capture their inputs at the same clock edge.

Thus:

```text
q1 → new d
q2 → old q1
```

Nonblocking assignment naturally models this behavior.

---

# 18. Why is `=` Preferred for Combinational Logic?

Combinational logic has no clocked storage.

If intermediate values are calculated sequentially inside a procedural block:

```verilog
always @(*) begin
    x = a & b;
    y = x | c;
end
```

blocking assignments allow the next statement to use the newly calculated value immediately.

---

# 19. Blocking vs Nonblocking — Hardware View

### Blocking

```text
Statement 1
    ↓
Update
    ↓
Statement 2
    ↓
Update
```

### Nonblocking

```text
Evaluate RHS values
        ↓
Schedule updates
        ↓
Update together
```

---

# 20. Example — Counter

A synchronous counter is normally written:

```verilog
always @(posedge clk) begin
    count <= count + 1;
end
```

Why `<=`?

Because `count` represents a register.

---

# 21. Example — Register with Reset

```verilog
always @(posedge clk) begin
    if (reset)
        q <= 1'b0;
    else
        q <= d;
end
```

This is the standard sequential coding style:

```text
posedge clk
      ↓
   if reset
      ↓
q <= ...
```

---

# 22. Example — Combinational MUX

```verilog
always @(*) begin
    if (sel)
        y = b;
    else
        y = a;
end
```

Here:

```text
always @(*) → combinational
=           → blocking
```

---

# 23. Mixing Blocking and Nonblocking

It is possible to use both in the same procedural block, but careless mixing can create confusing simulation behavior.

For normal RTL coding:

```text
Combinational block → blocking
Sequential block    → nonblocking
```

is the safest and most important placement rule.

---

# 24. Blocking in Sequential Logic?

Technically, blocking assignments can sometimes synthesize and certain coding styles use them deliberately.

However, for placement/interview preparation:

> **Use nonblocking assignments for clocked sequential logic.**

This avoids many simulation-order problems and better represents simultaneous register updates.

---

# 25. Nonblocking in Combinational Logic?

It can be used in some cases, but it is generally **not the preferred coding style** for ordinary combinational logic.

For combinational RTL:

```verilog
always @(*) begin
    y = a & b;
end
```

is preferred.

---

# 26. Common Interview Trap ⭐⭐⭐⭐⭐

Question:

```verilog
always @(posedge clk) begin
    a <= b;
    b <= a;
end
```

What happens?

Suppose initially:

```text
a = 0
b = 1
```

After the clock:

```text
a = 1
b = 0
```

They **swap**.

Why?

```text
a gets old b
b gets old a
```

---

# 27. Same Example with Blocking

```verilog
always @(posedge clk) begin
    a = b;
    b = a;
end
```

Initially:

```text
a = 0
b = 1
```

After the clock:

```text
a = 1
b = 1
```

Because:

```text
a = b → a becomes 1
b = a → b sees new a = 1
```

This is a classic interview question.

---

# 28. Pipeline Interview Question

Given:

```verilog
always @(posedge clk) begin
    q1 <= d;
    q2 <= q1;
    q3 <= q2;
end
```

How many registers?

**Answer:**

```text
3 registers
```

Because:

```text
q1 → register
q2 → register
q3 → register
```

---

# 29. Blocking vs Nonblocking Quick Table

| Feature             | Blocking `=`    | Nonblocking `<=`                      |
| ------------------- | --------------- | ------------------------------------- |
| Update              | Immediate       | Scheduled                             |
| Next statement sees | New value       | Old value                             |
| Typical use         | Combinational   | Sequential                            |
| Clocked logic       | Generally avoid | Preferred                             |
| Pipeline modeling   | Not preferred   | Preferred                             |
| Statement order     | Important       | RHS evaluation happens before updates |
| Common block        | `always @(*)`   | `always @(posedge clk)`               |

---

# ⭐ Frequently Asked Placement Questions

## Q1. What is a blocking assignment?

**Answer:** An assignment using `=` where the left-hand side is updated immediately before the next procedural statement executes.

---

## Q2. What is a nonblocking assignment?

**Answer:** An assignment using `<=` where the update is scheduled, allowing sequential register behavior to be modeled correctly.

---

## Q3. Which assignment is preferred for combinational logic?

**Answer:**

```text
Blocking `=`
```

---

## Q4. Which assignment is preferred for sequential logic?

**Answer:**

```text
Nonblocking `<=`
```

---

## Q5. Why is nonblocking used for flip-flops?

**Answer:** Because it models simultaneous register updates and ensures the right-hand sides use the values from before the clock event.

---

## Q6. What happens with blocking assignment?

**Answer:** The left-hand side is updated immediately, so subsequent statements can see the new value.

---

## Q7. What happens with nonblocking assignment?

**Answer:** The right-hand side is evaluated and the left-hand-side update is scheduled for later in the simulation time step.

---

## Q8. What does this code do?

```verilog
always @(posedge clk) begin
    q1 <= d;
    q2 <= q1;
end
```

**Answer:** It describes two registers in series, forming a two-stage pipeline.

---

## Q9. What happens here?

```verilog
always @(posedge clk) begin
    a <= b;
    b <= a;
end
```

If:

```text
a = 0
b = 1
```

after the clock:

```text
a = 1
b = 0
```

They swap.

---

## Q10. What happens with blocking?

```verilog
always @(posedge clk) begin
    a = b;
    b = a;
end
```

If:

```text
a = 0
b = 1
```

then after execution:

```text
a = 1
b = 1
```

---

## Q11. Why is mixing blocking and nonblocking assignments discouraged?

**Answer:** It can create confusing simulation-order and race-related behavior, making RTL harder to understand and verify.

---

## Q12. Does blocking mean the hardware itself is sequential?

**Answer:** No. Blocking vs nonblocking primarily describes **simulation/procedural assignment semantics**. The synthesized hardware depends on the overall RTL structure.

---

## Q13. Does nonblocking automatically mean flip-flop?

**Answer:** No. Hardware inference depends on the surrounding procedural block and event controls.

---

## Q14. What is the standard coding rule?

**Answer:**

```text
Combinational → always @(*) + =
Sequential    → always @(posedge clk) + <=
```

---

# 🔥 Placement Rapid-Fire

**Blocking operator?**

→ `=`

**Nonblocking operator?**

→ `<=`

**Blocking update?**

→ Immediate

**Nonblocking update?**

→ Scheduled

**Combinational?**

→ `=`

**Sequential?**

→ `<=`

**Flip-flop?**

→ `always @(posedge clk)` + `<=`

**MUX?**

→ `always @(*)` + `=`

**Pipeline?**

→ Nonblocking assignments

**Why `<=` for registers?**

→ Models simultaneous updates

**Why `=` for combinational?**

→ Immediate procedural evaluation

---

# 🧠 QUICK REVISION

```text
        BLOCKING vs NONBLOCKING
                 │
        ┌────────┴────────┐
        ↓                 ↓
       `=`               `<=`
        ↓                 ↓
   Immediate           Scheduled
        ↓                 ↓
 Combinational        Sequential
        ↓                 ↓
 always @(*)       always @(posedge clk)
```

### Combinational

```verilog
always @(*) begin
    y = a & b;
end
```

### Sequential

```verilog
always @(posedge clk) begin
    q <= d;
end
```

### Pipeline

```verilog
always @(posedge clk) begin
    q1 <= d;
    q2 <= q1;
    q3 <= q2;
end
```

### ⭐ Golden Rule

```text
Combinational → blocking (=)
Sequential    → nonblocking (<=)
```
