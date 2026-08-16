# COMBINATIONAL CIRCUITS — BIG PICTURE REVISION ⭐⭐⭐⭐⭐

Before we move further, let's connect everything you've learned so far.

## 1. Half Adder

```text
Sum=A⊕B
Carry=AB
```

---

## 2. Full Adder

```text
Sum=A⊕B⊕Cin
Cout=AB+BCin+ACin
```

---

## 3. Half Subtractor

```text
D=A⊕B
Borrow=AB
```

---

## 4. Full Subtractor

```text
D=A⊕B⊕Bin
Bout=AB+ABin+BBin
```

---

## 5. Comparator

For 1-bit:

```text
A>B=AB
A=B=A XNOR B
A<B=AB
```

Multi-bit:

```text
Compare MSB → LSB
```

---

## 6. Encoder

```text
Many → Few
```

Example:

```text
4→2
```

Normal encoder assumes **one active input**.

---

## 7. Priority Encoder ⭐

Multiple inputs can be active.

Highest-priority input wins.

---

## 8. Decoder

```text
Few → Many
```

Example:

```text
2→4
```

A decoder generates **minterms**.

---

## 9. MUX ⭐⭐⭐⭐⭐

```text
Many → One
```

For N inputs:

```text
Select lines=log₂N
```

2:1:

```text
Y=S′I0+SI1
```

---

## 10. DEMUX

```text
One → Many
```

Select lines determine which output receives the data.

---

# ⭐ VERY IMPORTANT COMBINATIONAL CIRCUIT MEMORY MAP

```text
                    COMBINATIONAL
                         │
       ┌─────────────────┼─────────────────┐
       │                 │                 │
    Arithmetic        Selection         Conversion
       │                 │                 │
   ┌───┴────┐        ┌───┴────┐       ┌────┴────┐
   │        │        │        │       │         │
 Adder  Subtractor   MUX     DEMUX  Encoder  Decoder
                       │
                       │
                  Boolean Function
                  Implementation
```

And:

```text
MUX     → Many → One
```

```text
DEMUX   → One → Many
```

```text
Encoder → Many → Few
```

```text
Decoder → Few → Many
```
