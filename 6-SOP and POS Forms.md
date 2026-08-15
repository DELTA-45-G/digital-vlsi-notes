# SOP and POS Forms ⭐⭐⭐⭐⭐

This is a **very important topic** because SOP/POS connects:

**Boolean Algebra → Truth Tables → K-Maps → Digital Circuit Design**

For VLSI placements, you should be comfortable converting between these forms.

---

# 1. First Understand the Names

### SOP

**SOP = Sum of Products**

### POS

**POS = Product of Sums**

Here:

* **Sum** → OR (`+`)
* **Product** → AND (`·`)

So don't think about normal arithmetic.

---

# 2. SOP — Sum of Products ⭐⭐⭐⭐⭐

An SOP expression consists of **AND terms connected by OR**.

Example:

```text id="y20yuj"
Y = AB + AC + BC
```

Break it down:

```text id="f7wzjo"
AB        → Product term
```

```text id="e4r1gt"
A'C       → Product term
```

```text id="5b2twt"
BC        → Product term
```

```text id="mgd0lr"
+         → OR
```

Therefore:

```text id="o3f4q0"
Product + Product + Product
```

↓

SOP

---

# 3. Why is it Called "Sum of Products"?

Look at:

```text id="m4q1vv"
Y = AB + A′C + BC
```

Each individual term is a **product**:

```text id="s3a2mj"
AB
A′C
BC
```

Then we OR them together:

```text id="l9w2kk"
AB + A′C + BC
```

Therefore:

**Sum of Products**

---

# 4. SOP Circuit Representation

For:

```text id="2s1g1r"
Y = AB + A′C + BC
```

Conceptually:

```text id="jv9ikg"
A ───┐
     AND ───┐
B ───┘      │
            │
A ── NOT ─┐ │
           AND ──┐
C ────────┘      │
                 OR ─── Y
B ───┐           │
     AND ────────┘
C ───┘
```

So SOP naturally maps to:

```text id="e8udqr"
AND gates
```

↓

OR gate

---

# 5. POS — Product of Sums ⭐⭐⭐⭐⭐

POS consists of **OR terms connected by AND**.

Example:

```text id="f9x1nq"
Y = (A+B)(A′+C)(B+C)
```

Each bracket is a **sum term**:

```text id="7xw2cl"
(A+B)
(A′+C)
(B+C)
```

Then the terms are ANDed.

Therefore:

```text id="v6ue0k"
Sum × Sum × Sum
```

↓

POS

---

# 6. Why is it Called "Product of Sums"?

Take:

```text id="yupk6v"
Y = (A+B)(A′+C)(B+C)
```

Each bracket contains an OR:

```text id="d8sp7v"
A+B
```

```text id="d6zwqp"
A'+C
```

```text id="r6d6g1"
B+C
```

So each bracket is a **Sum**.

Then the brackets are ANDed:

```text id="c9oqoj"
(A+B) · (A'+C) · (B+C)
```

Therefore:

**Product of Sums**

---

# 7. POS Circuit Representation

For:

```text id="nhh6uw"
Y = (A+B)(A′+C)(B+C)
```

Conceptually:

```text id="0r5k4a"
A ───┐
     OR ───┐
B ───┘     │
           │
A ─ NOT ─┐ │
         OR ───┐
C ───────┘     │
               AND ─── Y
B ───┐         │
     OR ───────┘
C ───┘
```

So:

```text id="p6md3u"
OR gates
```

↓

AND gate

---

# 8. SOP vs POS ⭐⭐⭐⭐⭐

| SOP                               | POS                               |
| --------------------------------- | --------------------------------- |
| Sum of Products                   | Product of Sums                   |
| AND first                         | OR first                          |
| Product terms                     | Sum terms                         |
| AND gates → OR gate               | OR gates → AND gate               |
| Commonly associated with minterms | Commonly associated with maxterms |

### Memory trick 🧠

**SOP:**

> **AND → OR**

**POS:**

> **OR → AND**

---

# 9. What is a Literal?

A **literal** is a variable or its complement.

For example:

`A`

is a literal.

`A′`

is also a literal.

Therefore:

```text id="ejtw9v"
AB′C
```

contains **3 literals**:

```text id="e5a1om"
A
B'
C
```

---

# 10. Product Term

A product term is a group of literals connected by AND.

Examples:

```text id="yyj4ya"
AB
A′BC
AB′C′D
```

These are all product terms.

---

# 11. Sum Term

A sum term is a group of literals connected by OR.

Examples:

```text id="4h3b20"
A+B
A′+B+C
A+B′+C+D′
```

These are sum terms.

---

# 12. Standard SOP vs Canonical SOP ⭐⭐⭐⭐⭐

This distinction is important.

Consider:

```text id="7o4v1q"
Y = AB + A′C
```

This is an SOP expression.

But it is **not necessarily canonical SOP**.

Why?

Because each product term doesn't necessarily contain **every variable**.

Suppose variables are:

```text id="3iy1nh"
A, B, C
```

Then:

```text id="50ocjp"
AB
```

doesn't contain C.

---

# 13. Canonical SOP ⭐⭐⭐⭐⭐

In **canonical SOP**, every product term contains **every variable exactly once**, either complemented or uncomplemented.

For three variables:

```text id="d22jql"
ABC
```

```text id="wsojtd"
AB'C
```

```text id="t5r8m9"
A'BC
```

```text id="oylqul"
A'B'C
```

Every term contains:

```text id="g6v1ou"
A
```

```text id="dwbp5p"
B
```

```text id="i2s2e6"
C
```

---

# 14. Minterm ⭐⭐⭐⭐⭐

A canonical SOP term is called a **minterm**.

For three variables, examples:

```text id="f9d1fa"
ABC
AB′C
A′BC
A′B′C
```

Each minterm corresponds to exactly **one row of the truth table**.

---

# 15. Why Are Minterms Important?

Because we can represent a Boolean function as:

```text id="rvjlp6"
F = Σm(minterm numbers)
```

Example:

```text id="uy74p9"
F(A,B,C) = Σm(1,3,5,7)
```

This means the function is `1` for minterms:

```text id="w1fhph"
1
```

```text id="9ld1st"
3
```

```text id="8y0i5z"
5
```

```text id="5f9n5n"
7
```

You'll use this heavily when learning **K-maps**.

---

# 16. How Do We Find a Minterm Number? ⭐⭐⭐⭐⭐

Use the binary combination.

Suppose:

```text id="e0vqta"
A B C = 101
```

Binary `101` = decimal `5`.

Therefore the corresponding minterm is:

```text id="0r5u6y"
m5
```

The actual minterm expression is:

```text id="u8j7oi"
AB′C
```

Why?

```text id="q9pgtd"
A = 1 → A
```

```text id="9kpp0g"
B = 0 → B'
```

```text id="m8o4cl"
C = 1 → C
```

So:

```text id="7j26c3"
101 → AB′C
```

---

# 17. Minterm Memory Rule ⭐⭐⭐⭐⭐

For SOP/minterms:

### If variable = 1

Use the variable normally.

### If variable = 0

Complement it.

Example:

```text id="dphuh2"
A B C
1 0 1
```

gives:

```text id="87pq7l"
AB′C
```

---

# 18. Canonical POS ⭐⭐⭐⭐⭐

Now the opposite.

Canonical POS consists of **maxterms**.

Every sum term contains every variable exactly once.

Example:

```text id="6s14sy"
(A+B+C)
(A+B′+C)
(A′+B+C′)
```

---

# 19. Maxterm

A canonical POS term is called a **maxterm**.

We write:

```text id="2r9nqf"
F = ΠM(maxterm numbers)
```

For example:

```text id="3g3gzw"
F = ΠM(0,2,4,6)
```

means the function is `0` at those maxterm indices.

---

# 20. Minterm vs Maxterm ⭐⭐⭐⭐⭐

This is extremely important.

| Minterm        | Maxterm  |
| -------------- | -------- |
| Form           | AND term |
| Used in        | SOP      |
| Symbol         | m        |
| Function value | 1        |
| Notation       | Σm       |
| Form           | OR term  |
| Used in        | POS      |
| Symbol         | M        |
| Function value | 0        |
| Notation       | ΠM       |

### Memory trick

```text id="q7cz1v"
SOP → Σm → minterms → 1s
```

```text id="m0q5t9"
POS → ΠM → maxterms → 0s
```

⭐⭐⭐⭐⭐ **Memorize this.**

---

# 21. Minterm Example

Suppose:

```text id="un9lnq"
A B C = 110
```

Binary:

```text id="gq5w3m"
110₂ = 6
```

For minterm:

```text id="92zyh3"
1 → A
```

```text id="0k4sqe"
1 → B
```

```text id="4etq0i"
0 → C'
```

Therefore:

```text id="xgf8h4"
m6 = ABC′
```

---

# 22. Maxterm Example ⭐⭐⭐⭐⭐

Now use the same input:

```text id="vs2q8u"
A B C = 110
```

For a **maxterm**, the rule is reversed:

### If variable = 0 → normal variable

### If variable = 1 → complemented variable

So:

```text id="g4x2c0"
A = 1 → A'
```

```text id="ev2b5j"
B = 1 → B'
```

```text id="h0g6wd"
C = 0 → C
```

Therefore:

```text id="0lxu2n"
M6 = (A′+B′+C)
```

Why does this work?

Evaluate at `A=1,B=1,C=0`:

```text id="f7lxxo"
A′+B′+C = 0+0+0 = 0
```

That's exactly what a maxterm should do.

---

# 23. ⭐ Minterm vs Maxterm Shortcut

For:

```text id="m0l8ml"
A B C = 1 0 1
```

### Minterm

```text id="jv4g7f"
1 → normal
```

```text id="6hh4km"
0 → complement
```

So:

```text id="d1zj3k"
AB′C
```

### Maxterm

```text id="2v1fjp"
1 → complement
```

```text id="xg6y0a"
0 → normal
```

So:

```text id="s2l7ek"
(A′+B+C′)
```

---

# 24. Placement Example

Question:

> Find the minterm corresponding to `A B C = 101`.

Binary:

```text id="hsq4zn"
101₂ = 5
```

Therefore:

```text id="w3phj2"
m5 = AB′C
```

---

Another:

> Find the maxterm corresponding to `A B C = 101`.

For maxterm:

```text id="h4gjzi"
1 → complement
```

```text id="u6w6a6"
0 → normal
```

Therefore:

```text id="rb7ay4"
M5 = (A′+B+C′)
```

---

# 25. Why SOP/POS Matter in VLSI ⭐⭐⭐⭐⭐

Boolean functions can be represented in different forms.

For example:

```text id="m9h8u8"
F = AB + A′C
```

can be implemented using:

```text id="x27wvr"
AND gates
```

↓

OR gate

Another function may be easier using POS:

```text id="fckq58"
OR gates
```

↓

AND gate

K-map helps us find the **minimal SOP or POS**, reducing:

* Gate count
* Transistor count
* Area
* Power
* Delay

This becomes very important in actual digital VLSI design.

---

# 26. Quick Revision ⭐⭐⭐⭐⭐

```text id="zwp7f3"
SOP = Sum of Products
```

**AND terms connected by OR**

Example:

```text id="d8tuq5"
AB + A'C + BC
```

```text id="opqg2k"
POS = Product of Sums
```

**OR terms connected by AND**

Example:

```text id="j1f8pp"
(A+B)(A'+C)(B+C)
```

### Canonical forms

```text id="6rxk8r"
Canonical SOP → Minterms → Σm → 1s
```

```text id="f7w7nh"
Canonical POS → Maxterms → ΠM → 0s
```

### Minterm rule

```text id="1crh5p"
1 → normal
```

```text id="u6z8j6"
0 → complement
```

### Maxterm rule

```text id="sdm2kq"
1 → complement
```

```text id="8z7c1a"
0 → normal
```

---

# ⭐ Placement Must-Know

Memorize these:

```text id="gca2nl"
SOP = AND terms ORed together
```

```text id="rkl2e6"
POS = OR terms ANDed together
```

```text id="dy7u9n"
Σm = minterms = 1
```

```text id="5id3i8"
ΠM = maxterms = 0
```

And:

> **Minterm → 1 means normal, 0 means complement.**

> **Maxterm → 1 means complement, 0 means normal.**
