FSM DESIGN PROBLEMS / COMMON PLACEMENT QUESTIONS ⭐⭐⭐⭐⭐

Now we'll combine the Phase 7 concepts into placement-style problems with answers.

This section is important because interviewers often don't ask only definitions. They give a small FSM problem and test whether you can reason through states, transitions, outputs, and flip-flops.

1. Sequence Detector — 101 ⭐⭐⭐⭐⭐
Q1. What type of circuit is commonly used to detect a sequence such as 101?

Answer:

FSM
	​


Because the circuit needs to remember previous input bits.

Q2. For a 101 sequence detector, what can the states represent?

Answer:

S0 → Nothing matched
S1 → 1 matched
S2 → 10 matched

For a straightforward Moore implementation:

S3 → 101 detected
Q3. In a Moore 101 detector, why is an additional state generally required?

Answer:

Because Moore output depends only on the state.

Therefore, a separate state can represent:

101 detected

with:

Y=1
Q4. In a Mealy 101 detector, where can the detection output be generated?

Answer:

On the transition that receives the final 1.

Conceptually:

S2 ──1/1──► next state
2. Overlapping Sequence Detector ⭐⭐⭐⭐⭐
Q5. How many overlapping occurrences of 101 exist in:
10101

Answer:

Two:

10101
^^^
  ^^^
2
	​

Q6. Why is this called overlapping?

Answer:

Because the last 1 of the first 101 is also the first 1 of the second 101.

Q7. After detecting 101 in an overlapping detector, why might the FSM return to the state representing 1?

Answer:

Because the final 1 can be reused as the beginning of the next 101 sequence.

3. Moore vs Mealy ⭐⭐⭐⭐⭐
Q8. Output equation of Moore?
Y=f(Q)
	​

Q9. Output equation of Mealy?
Y=f(Q,X)
	​

Q10. Which generally uses fewer states?
Mealy
	​

Q11. Which is generally more susceptible to input glitches?
Mealy
	​


because its output directly depends on the input.

Q12. Which generally provides more stable outputs?
Moore
	​

4. State Diagram Questions ⭐⭐⭐⭐⭐

Suppose:

S0 ──1──► S1
S0 ──0──► S0
Q13. What happens when the FSM is in S0 and input is 1?

Answer:

S0→S1
	​

Q14. What happens when the FSM is in S0 and input is 0?

Answer:

S0→S0
	​


The FSM remains in S0.

Q15. What is the S0 → S0 transition called?

Answer:

Self-loop
	​

5. State Table Questions ⭐⭐⭐⭐⭐

Suppose:

Present State	X	Next State
S0	0	S1
S0	1	S0
S1	0	S1
S1	1	S0
Q16. What is the next state for S0 when X=0?
S1
	​

Q17. What is the next state for S1 when X=1?
S0
	​

Q18. How many state/input combinations are listed?
4
	​


because:

2 states×2
1
=4
6. State Encoding Questions ⭐⭐⭐⭐⭐
Q19. How many flip-flops are required for 8 states using binary encoding?
log
2
	​

8=3
3
	​

Q20. How many flip-flops for 9 states?
⌈log
2
	​

9⌉=4
4
	​

Q21. How many flip-flops for 8 states using one-hot encoding?
8
	​

Q22. What is the major advantage of one-hot encoding?

Answer:

It can simplify state decoding and next-state logic, although it requires more flip-flops.

7. State Minimization ⭐⭐⭐⭐⭐
Q23. What is state minimization?

Answer:

Reducing the number of equivalent states while preserving the FSM's external behavior.

Q24. Can two Moore states with different outputs be equivalent?
No
	​

Q25. What is the first step in Moore state minimization?

Answer:

Partition states according to their outputs.

Q26. Does reducing 10 states to 7 necessarily reduce the number of binary flip-flops?

Answer:

No.

Before:

⌈log
2
	​

10⌉=4

After:

⌈log
2
	​

7⌉=3

In this case it does reduce.

But, for example:

7→5

gives:

3→3

So the flip-flop count does not always decrease.

8. FSM Design Flow ⭐⭐⭐⭐⭐
Q27. Put these in the correct order:
State Table
State Assignment
Problem Specification
Circuit
State Diagram
Flip-Flop Selection
Boolean Equations
Answer:
1. Problem Specification
2. State Diagram
3. State Table
4. State Assignment
5. Flip-Flop Selection
6. Boolean Equations
7. Circuit

A more complete practical flow is:

Specification
 ↓
Inputs/Outputs
 ↓
States
 ↓
State Diagram
 ↓
State Table
 ↓
State Assignment
 ↓
Choose FF
 ↓
Excitation Table
 ↓
Boolean Equations
 ↓
Simplification
 ↓
Circuit
9. D Flip-Flop FSM Questions ⭐⭐⭐⭐⭐
Q28. For a D flip-flop, what is the relationship between D and next state?
D=Q
next
	​

	​

Q29. Present state = 0 and next state = 1. What should D be?
D=1
	​

Q30. Present state = 1 and next state = 0. What should D be?
D=0
	​

10. T Flip-Flop FSM Questions
Q31. What is the T flip-flop excitation equation?
T=Q⊕Q
next
	​

	​

Q32. If Q=0 and Qnext=1, what is T?
0⊕1=1
T=1
	​

Q33. If Q=1 and Qnext=1, what is T?
1⊕1=0
T=0
	​

11. Number of State Table Rows ⭐⭐⭐⭐⭐
Q34.

An FSM has:

4 states
2 input bits

How many state/input combinations?

4×2
2
=4×4
16
	​

Q35.

An FSM has:

8 states
3 input bits

How many combinations?

8×2
3
=8×8
64
	​

12. FSM Trick Question ⭐⭐⭐⭐⭐
Q36.

A Moore FSM has 4 states and a 1-bit input.

Does it necessarily have exactly 8 transitions?

Answer:

No.

There are:

4×2=8

possible state/input combinations, but the actual diagram may contain self-loops or multiple combinations leading to the same destination.

The important point is:

8 possible state/input entries
	​


for a fully specified FSM.

13. Unused States ⭐⭐⭐⭐
Q37.

An FSM requires 5 states.

How many binary states are available with 3 flip-flops?

2
3
=8

Therefore unused states:

8−5=3
3
	​

Q38.

Why should unused states be considered?

Answer:

To ensure predictable and safe behavior if the FSM somehow enters an unused state.

A designer may specify transitions from unused states to a valid recovery state.

14. FSM Interview Scenario ⭐⭐⭐⭐⭐
Q39.

An interviewer asks:

"Why would you choose a Mealy FSM instead of a Moore FSM?"

Strong answer:

I would consider a Mealy FSM when I need faster response to input changes or want to reduce the number of states. However, Mealy outputs depend directly on inputs, so they can be more sensitive to glitches. If output stability is more important, Moore may be preferable.

15. Another Interview Scenario
Q40.

"Why might one-hot encoding be used even though it requires more flip-flops?"

Answer:

One-hot encoding uses one flip-flop per state, which increases the number of flip-flops but can simplify state decoding and next-state logic. This can be particularly attractive in FPGA implementations where flip-flops are relatively abundant.

16. 🔥 Most Important Phase 7 Interview Questions

These are the questions I recommend memorizing:

1.

What is an FSM?

An FSM is a sequential digital system whose behavior is represented using a finite number of states and transitions between them.

2.

Moore vs Mealy?

Moore → Output = State
Mealy → Output = State + Input
3.

Why does an FSM need memory?

Because its next behavior depends on its previous/current state.

4.

What is state minimization?

Removing equivalent states without changing external behavior.

5.

What is state assignment?

Assigning binary codes to symbolic states.

6.

What is one-hot encoding?

Using one flip-flop for each state, with normally one state bit asserted at a time.

7.

What is a sequence detector?

An FSM that detects a specified pattern in an input stream.

8.

Overlapping vs non-overlapping?

Overlapping → reuse matched bits
Non-overlapping → don't reuse detected sequence
9.

How many binary FFs for N states?

⌈log
2
	​

N⌉
	​

10.

D flip-flop FSM equation?

D=Q
next
	​

	​

11.

T flip-flop FSM equation?

T=Q⊕Q
next
	​

	​

🧠 PHASE 7 — COMPLETE REVISION MAP

You have now covered the major Phase 7 topics in order:

PHASE 7 — FINITE STATE MACHINES
════════════════════════════════════


7.1  FSM Fundamentals
       ↓
7.2  States, Inputs & Outputs
       ↓
7.3  State Transitions
       ↓
7.4  Moore vs Mealy
       ↓
7.5  State Diagrams
       ↓
7.6  State Tables
       ↓
7.7  FSM Design Procedure
       ↓
7.8  State Assignment
       ↓
7.9  Sequence Detectors
       ↓
7.10 State Reduction / Minimization
       ↓
7.11 FSM Design & Placement Problem