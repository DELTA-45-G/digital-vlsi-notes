RING COUNTER ⭐⭐⭐⭐

A Ring Counter is a shift-register-based counter in which the output of the last flip-flop is fed back to the input of the first flip-flop.

It is also called a:

One-hot counter
	​

1. Basic Structure

A 4-bit ring counter:

        ┌─────────────────────────────┐
        │                             │
        │                             ▼
      ┌────┐    ┌────┐    ┌────┐    ┌────┐
 ────►│ FF0│───►│ FF1│───►│ FF2│───►│ FF3│
      └────┘    └────┘    └────┘    └────┘
        ▲                             │
        └─────────────────────────────┘

The output of the last flip-flop is fed back to the first.

2. 4-Bit Ring Counter Sequence ⭐⭐⭐⭐⭐

Suppose the initial state is:

1000

The 1 circulates through the flip-flops:

1000
 ↓
0100
 ↓
0010
 ↓
0001
 ↓
1000

Notice that there is only one 1 at any time.

That's why it is called a:

One-hot counter
	​

3. MOD Value ⭐⭐⭐⭐⭐

For a ring counter with n flip-flops:

MOD=n
	​

Example

4-bit ring counter:

MOD−4
	​


8-bit ring counter:

MOD−8
	​


This is different from a normal binary counter.

Normal 4-bit counter:
MOD=2
4
=16
4-bit ring counter:
MOD=4

⭐ Very important placement comparison.

4. Number of Flip-Flops

For a ring counter:

n flip-flops→MOD−n
	​


So for a MOD-8 ring counter:

8 flip-flops
	​

5. Initialization ⭐⭐⭐⭐⭐

A ring counter generally needs to be initialized to a valid one-hot state.

For example:

1000

is valid.

But:

0000

is problematic because the 1 can never circulate if there is no 1 initially.

Similarly:

1010

is not a normal one-hot state.

Therefore proper initialization is important.

6. Ring Counter Advantages
Simple decoding
Each state has one active output
Useful for sequence generation
Useful in control circuits
7. Ring Counter Disadvantages

The major disadvantage is:

Requires more flip-flops
	​


For example:

Ring counter

MOD-8:

8 FFs
Binary counter

MOD-8:

3 FFs

because:

2
3
=8

So ring counters are hardware inefficient compared with binary counters when only a small number of states is needed.

8. Ring Counter vs Binary Counter ⭐⭐⭐⭐⭐
Feature	Ring Counter	Binary Counter
FFs for MOD-8	8	3
MOD with n FFs	n	2
n

State representation	One-hot	Binary
Decoding	Simple	More logic often needed
Hardware efficiency	Lower	Higher
🧠 Quick Revision
RING COUNTER
────────────────────────


→ Shift-register based counter
→ Last FF output fed back to first FF
→ One-hot counter


n FFs:
→ MOD-n


4-bit ring counter:
→ MOD-4


Sequence:
1000 → 0100 → 0010 → 0001 → 1000


Important:
→ Requires proper initialization
→ Uses more FFs than binary counter