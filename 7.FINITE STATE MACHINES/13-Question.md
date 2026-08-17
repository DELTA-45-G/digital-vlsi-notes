FREQUENTLY ASKED PLACEMENT QUESTIONS + ANSWERS
FSM — Topic-wise ⭐⭐⭐⭐⭐

This is your Phase 7 placement question bank. I’ll focus on the questions most likely to appear in ECE/VLSI/Embedded/Digital placement tests and interviews, from basic → conceptual → numerical → interview level.

7.1 FSM FUNDAMENTALS
Q1. What is an FSM?

Answer:
A Finite State Machine (FSM) is a sequential digital system that operates using a finite number of states and transitions between those states based on inputs.

Q2. Why is an FSM called a sequential circuit?

Answer:
Because its output/behavior depends on the present input and previous state, and the state provides memory.

Present State + Input→Next State
	​

Q3. What are the main components of an FSM?

Answer:

Inputs
Outputs
Present state
Next-state logic
State memory/flip-flops
Output logic
Clock
Q4. What stores the current state?

Answer:

Flip-flops
	​

Q5. What is a state?

Answer:
A state represents the stored information about the past behavior of the system that is necessary to determine its future behavior.

Q6. What is a state transition?

Answer:
A state transition is the movement from the present state to the next state based on the input.

PS+Input→NS
	​

Q7. What is the difference between combinational and sequential circuits?
Combinational	Sequential
Output depends on present input	Output depends on present input + previous state
No memory	Has memory
Usually no clock required	Usually clocked
Example: MUX	Example: FSM
7.2 MOORE FSM ⭐⭐⭐⭐⭐
Q8. What is a Moore machine?

Answer:
A Moore machine is an FSM whose output depends only on the present state.

Y=f(Q)
	​

Q9. Where is output represented in a Moore state diagram?

Answer:

Inside the state.

Example:

S0 / 0
S1 / 1
Q10. What is the main advantage of a Moore machine?

Answer:

Its output depends only on the state, so it is generally less sensitive to input glitches.

Q11. What is the disadvantage of Moore FSM?

Answer:

It may require more states and may respond one state transition later than a Mealy implementation.

7.3 MEALY FSM ⭐⭐⭐⭐⭐
Q12. What is a Mealy machine?

Answer:
A Mealy machine is an FSM whose output depends on both the present state and input.

Y=f(Q,X)
	​

Q13. Where is output represented in a Mealy state diagram?

Answer:

On the transition.

Example:

S0 ── 1/0 ──► S1

Here:

Input = 1
Output = 0
Q14. What is the main advantage of Mealy FSM?

Answer:

Generally fewer states
Faster response to input changes
Output can be generated on the transition receiving the final input
Q15. What is the major disadvantage of Mealy FSM?

Answer:

Its output directly depends on input, so it can be more susceptible to glitches.

7.4 MOORE vs MEALY ⭐⭐⭐⭐⭐
Q16. What is the main difference?

Answer:

Moore: Output = State
	​

Mealy: Output = State + Input
	​

Q17. Which generally requires fewer states?
Mealy
	​

Q18. Which is generally more glitch-sensitive?
Mealy
	​

Q19. Which generally has more stable outputs?
Moore
	​

Q20. Which is generally faster to respond?
Mealy
	​

7.5 STATE DIAGRAM ⭐⭐⭐⭐⭐
Q21. What is a state diagram?

Answer:
A graphical representation of states and transitions of an FSM.

Q22. What does an arrow represent?

Answer:

State transition
	​

Q23. What does a self-loop represent?

Answer:
A transition from a state back to itself.

Example:

S0 ──0──► S0
Q24. What does this Mealy transition mean?
S1 ── 0/1 ──► S2

Answer:

Input = 0
Output = 1
Next state = S2
Q25. What does S1/0 mean in a Moore diagram?

Answer:

State = S1
Output = 0
7.6 STATE TABLE ⭐⭐⭐⭐⭐
Q26. What information does a state table contain?

Answer:

Present state
Input
Next state
Output
Q27. What is the basic FSM relationship?
PS+Input→NS+Output
	​

Q28. An FSM has 4 states and 2 input bits. How many state/input combinations exist?
4×2
2
16
	​

Q29. An FSM has 8 states and 3 input bits. How many rows are needed in a fully specified state table?
8×2
3
=64
64
	​

7.7 STATE ASSIGNMENT ⭐⭐⭐⭐⭐
Q30. What is state assignment?

Answer:
Assigning binary codes to symbolic FSM states.

Example:

S0 → 00
S1 → 01
S2 → 10
S3 → 11
Q31. How many flip-flops are required for N states using binary encoding?
⌈log
2
	​

N⌉
	​

Q32. How many flip-flops are required for 5 states?
⌈log
2
	​

5⌉=3
3
	​

Q33. How many flip-flops are required for 16 states?
log
2
	​

16=4
4
	​

Q34. How many flip-flops are required for 17 states?
⌈log
2
	​

17⌉=5
5
	​

7.8 ONE-HOT ENCODING ⭐⭐⭐⭐⭐
Q35. What is one-hot encoding?

Answer:
Each FSM state is represented using a separate flip-flop, with normally only one flip-flop active at a time.

Example:

S0 → 0001
S1 → 0010
S2 → 0100
S3 → 1000
Q36. How many flip-flops are required for 8 states using one-hot encoding?
8
	​

Q37. What is the main advantage?

Answer:

Simpler state decoding and potentially simpler next-state logic.

Q38. What is the main disadvantage?

Answer:

It requires more flip-flops.

7.9 GRAY ENCODING
Q39. What is Gray state encoding?

Answer:
An encoding where adjacent states differ by only one bit.

Example:

00 → 01 → 11 → 10
Q40. What is the main advantage?

Answer:

It can reduce switching activity between adjacent states.

7.10 SEQUENCE DETECTORS ⭐⭐⭐⭐⭐
Q41. What is a sequence detector?

Answer:
An FSM that detects a specific pattern in a serial input stream.

Example:

Pattern = 101
Q42. Why does a sequence detector require memory?

Answer:
Because it needs to remember previous input bits to determine whether the required sequence is being received.

Q43. Which FSM types can be used to design sequence detectors?
Moore and Mealy
	​

Q44. Which generally requires fewer states for sequence detection?
Mealy
	​

7.11 OVERLAPPING SEQUENCE DETECTION ⭐⭐⭐⭐⭐
Q45. What is overlapping detection?

Answer:
A previously detected sequence can share bits with the next sequence.

Q46. Pattern = 101, input = 10101. How many overlapping occurrences?
10101
^^^
  ^^^
2
	​

Q47. Why can the FSM return to the state representing 1 after detecting 101?

Answer:
Because the final 1 can also serve as the first bit of the next 101.

7.12 NON-OVERLAPPING DETECTION
Q48. What is non-overlapping detection?

Answer:
The already detected sequence is not reused as part of another detection.

Q49. Pattern = 101, input = 10101. Number of non-overlapping detections?
1
	​

Q50. Main difference?
Overlapping
→ Reuse matched bits


Non-overlapping
→ Don't reuse detected sequence
7.13 STATE MINIMIZATION ⭐⭐⭐⭐⭐
Q51. What is state minimization?

Answer:
Reducing the number of states by combining equivalent states without changing the external behavior of the FSM.

Q52. What are equivalent states?

Answer:
States that have identical observable behavior for all possible input sequences.

Q53. Can two Moore states with different outputs be equivalent?
No
	​

Q54. What is the first step in Moore state minimization?

Answer:

Partition states according to their outputs.

Q55. What is the partition method?

Answer:

1. Group states according to output
2. Examine next-state transitions
3. Split groups when behavior differs
4. Repeat until no further splitting is needed
Q56. Does state reduction always reduce flip-flops?
No
	​


Example:

7 states → 5 states

Both require:

3 binary FFs
7.14 FSM + FLIP-FLOPS ⭐⭐⭐⭐⭐
Q57. For a D flip-flop, what is the excitation equation?
D=Q
next
	​

	​

Q58. For a T flip-flop?
T=Q⊕Q
next
	​

	​

Q59. If Q=0 and Qnext=1, what is D?
1
	​

Q60. If Q=1 and Qnext=1, what is T?
1⊕1=0
0
	​

7.15 UNUSED STATES ⭐⭐⭐⭐
Q61. An FSM has 5 states using 3 flip-flops. How many unused states?

Available:

2
3
=8

Used:

5

Therefore:

8−5=3
3
	​

Q62. Why are unused states important?

Answer:

To ensure the FSM has predictable recovery behavior if it enters an unused state.

7.16 FSM DESIGN PROCEDURE ⭐⭐⭐⭐⭐
Q63. What is the general FSM design flow?

Answer:

Specification
↓
Inputs / Outputs
↓
States
↓
State Diagram
↓
State Table
↓
State Assignment
↓
Select Flip-Flop
↓
Excitation Table
↓
Boolean Equations
↓
Simplification
↓
Circuit
Q64. Why is state assignment performed?

Answer:

To convert symbolic states into binary representations suitable for hardware implementation.

7.17 PLACEMENT NUMERICALS ⭐⭐⭐⭐⭐
Q65.

An FSM has 12 states. Number of binary FFs?

⌈log
2
	​

12⌉=4
4
	​

Q66.

An FSM has 32 states. Number of binary FFs?

log
2
	​

32=5
5
	​

Q67.

An FSM has 33 states. Number of binary FFs?

⌈log
2
	​

33⌉=6
6
	​

Q68.

An FSM has 6 states and 2 input bits. Number of state/input combinations?

6×2
2
24
	​

Q69.

A 4-state FSM uses binary encoding. How many unused binary states exist?

4 states require:

2 FFs

Available states:

2
2
=4

Therefore:

0
	​

Q70.

A 6-state FSM uses 3 FFs. How many unused states?

2
3
−6=8−6
2
	​

🔥 TOP 20 MUST-KNOW QUESTIONS

If you're short on time before a placement test, prioritize these:

#	Question	Answer
1	What is FSM?	Sequential system with finite states
2	Moore output?	Y=f(Q)
3	Mealy output?	Y=f(Q,X)
4	Fewer states?	Mealy
5	More glitch-sensitive?	Mealy
6	State stored by?	Flip-flops
7	Binary FFs for N states?	⌈log
2
	​

N⌉
8	One-hot FFs for N states?	N
9	Gray code property?	Adjacent states differ by 1 bit
10	State minimization?	Remove equivalent states
11	First Moore minimization step?	Group by output
12	Sequence detector?	Detects input pattern
13	Overlapping?	Reuse matched bits
14	Non-overlapping?	Don't reuse detected sequence
15	D FF equation?	D=Q
next
	​


16	T FF equation?	T=Q⊕Q
next
	​


17	Available states with n FFs?	2
n

18	Unused states?	2
n
−N
19	State table combinations?	N2
m

20	State assignment?	Assign codes to states