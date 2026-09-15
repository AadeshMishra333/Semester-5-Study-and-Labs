Assume throughout **Σ = {0,1}**.
I’ll use **→** for the start state and ***** for final states.
No state diagrams—only transition tables.

---

# TOPIC 1 — First symbol fixed

### Exam question

Construct a DFA for all binary strings whose **first symbol is 0**.

### Why this category?

Only the **first input symbol** matters permanently.

### Memory

Remember whether the first symbol was `0` or `1`.

### States

* `q0`: nothing read yet
* `q1`: first symbol was `0`
* `q2`: first symbol was `1`

### Transition table

| State | 0   | 1  |
| ----- | --- | -- |
| → q0  | *q1 | q2 |
| *q1   | q1  | q1 |
| q2    | q2  | q2 |

Accepted: `01011`
Rejected: `10100`

### Common mistake

Accepting `ε`, or allowing later symbols to change the decision.

---

# TOPIC 2 — K-th symbol from left

### Exam question

Construct a DFA for strings whose **third symbol from the left is 1**.

### Why?

We must count the first three positions.

### Memory

Remember how many symbols have been consumed until position 3, then remember whether position 3 was `1`.

### States

* `q0`: read 0 symbols
* `q1`: read 1 symbol
* `q2`: read 2 symbols
* `q3`: third symbol was `1`
* `q4`: third symbol was `0`
* `qd`: dead state for strings too short

### Transition table

| State | 0  | 1   |
| ----- | -- | --- |
| → q0  | q1 | q1  |
| q1    | q2 | q2  |
| q2    | q4 | *q3 |
| *q3   | q3 | q3  |
| q4    | q4 | q4  |
| qd    | qd | qd  |

Accepted: `00101`
Rejected: `00011`

### Common mistake

Counting from the **right** instead of the left.

---

# TOPIC 3 — Condition on first k symbols

### Exam question

Construct a DFA for strings where **at least one of the first three symbols is 1**.

### Why?

Only the first three positions are inspected.

### Memory

Whether a `1` has appeared among positions 1–3.

### States

* `q0`: no symbols read
* `q1`: first symbol was `0`, no `1` yet
* `qA`: a `1` has occurred in first 3
* `qD`: first 3 symbols are all `0`

### Transition table

| State | 0  | 1   |
| ----- | -- | --- |
| → q0  | q1 | *qA |
| q1    | qD | *qA |
| qD    | qD | *qA |
| *qA   | qA | qA  |

Accepted: `0010`
Rejected: `0001`

### Common mistake

Checking the **entire string** for a `1` instead of only the first three positions.

---

# TOPIC 4 — Relationship among first few symbols

### Exam question

Construct a DFA for strings whose **first two symbols are identical**.

### Why?

The second symbol must be compared with the first.

### Memory

Store the first symbol until the second arrives.

### States

* `q0`: nothing read
* `q0x`: first symbol was `0`
* `q1x`: first symbol was `1`
* `qA`: first two equal
* `qD`: first two different

### Transition table

| State | 0   | 1   |
| ----- | --- | --- |
| → q0  | q0x | q1x |
| q0x   | *qA | qD  |
| q1x   | qD  | *qA |
| *qA   | qA  | qA  |
| qD    | qD  | qD  |

Accepted: `00101`
Rejected: `01101`

### Common mistake

Thinking later symbols can repair unequal first two symbols.

---

# TOPIC 5 — Last symbol fixed

### Exam question

Construct a DFA for strings **ending in 1**.

### Why?

The answer depends only on the most recent symbol.

### Memory

Remember the current last symbol.

### States

* `q0`: last symbol is `0` / no useful `1`
* `q1`: last symbol is `1`

### Transition table

| State | 0  | 1   |
| ----- | -- | --- |
| → q0  | q0 | *q1 |
| *q1   | q0 | q1  |

Accepted: `1101`
Rejected: `1100`

### Common mistake

Counting occurrences of `1` instead of remembering the final symbol.

---

# TOPIC 6 — Second-last symbol fixed

### Exam question

Construct a DFA for strings whose **second-last symbol is 1**.

### Why?

We need to know the symbol immediately before the final symbol.

### Memory

Effectively remember the **last two symbols**.

### States

Represent the current suffix of length ≤2.

### Transition table

| State | 0   | 1   |
| ----- | --- | --- |
| → qε  | q0  | q1  |
| q0    | q00 | q01 |
| q1    | q10 | q11 |
| q00   | q00 | q01 |
| q01   | q10 | q11 |
| *q10  | q00 | q01 |
| *q11  | q10 | q11 |

Accepted: `101` — second-last = `0` actually **rejected**.
Accepted example: `110` — second-last = `1`.
Rejected: `100` — second-last = `0`.

**Important:** `q10` and `q11` are final because their first suffix symbol is `1`.

### Common mistake

Checking the **last** symbol instead of the second-last.

---

# TOPIC 7 — K-th symbol from right

### Exam question

Construct a DFA whose **third symbol from the right is 0**.

### Why?

Unlike Topic 2, we cannot decide until the end.

### Memory

Keep the **last three symbols**.

### States

For compactness, after at least 3 symbols, state `qabc` means the current last three symbols are `abc`.

### Transition table

| State | 0    | 1    |
| ----- | ---- | ---- |
| → qε  | q0   | q1   |
| q0    | q00  | q01  |
| q1    | q10  | q11  |
| q00   | q000 | q001 |
| q01   | q010 | q011 |
| q10   | q100 | q101 |
| q11   | q110 | q111 |
| *q000 | q000 | q001 |
| *q001 | q010 | q011 |
| *q010 | q100 | q101 |
| *q011 | q110 | q111 |
| q100  | q000 | q001 |
| q101  | q010 | q011 |
| q110  | q100 | q101 |
| q111  | q110 | q111 |

Final states are those whose **first bit is 0**: `q000,q001,q010,q011`.

Accepted: `1001` → last 3 = `001`, third-from-right = `0`
Rejected: `1110` → last 3 = `110`, third-from-right = `1`

### Common mistake

Trying to determine the third-from-right symbol before knowing where the string ends.

---

# TOPIC 8 — Last two symbols relation

### Exam question

Construct a DFA for strings whose **last two symbols are equal**.

### Why?

We need to compare the final two symbols.

### Memory

Remember the last two-symbol suffix.

### States

Use suffix states `q00,q01,q10,q11`.

### Transition table

| State | 0    | 1    |
| ----- | ---- | ---- |
| → qε  | q0   | q1   |
| q0    | *q00 | q01  |
| q1    | q10  | *q11 |
| *q00  | q00  | q01  |
| q01   | q10  | q11  |
| q10   | q00  | q01  |
| *q11  | q10  | q11  |

Accepted: `10011`
Rejected: `10010`

### Common mistake

Comparing the first two symbols instead of the last two.

---

# TOPIC 9 — Ends with a specific pattern

### Exam question

Construct a DFA for strings that **end with `101`**.

### Why?

Only the suffix `101` matters.

### Memory

Track the longest suffix matching a prefix of `101`.

### States

* `q0`: no useful match
* `q1`: suffix `1`
* `q2`: suffix `10`
* `q3`: suffix `101`

### Transition table

| State | 0  | 1   |
| ----- | -- | --- |
| → q0  | q0 | q1  |
| q1    | q2 | q1  |
| q2    | q0 | *q3 |
| *q3   | q2 | q1  |

Accepted: `1101`
Rejected: `1010`

### Common mistake

Using a "contains 101" DFA instead of an "ends with 101" DFA.

---

# TOPIC 10 — Contains pattern vs Ends with pattern

### Exam question

Construct a DFA for strings that **contain `101` somewhere but do NOT necessarily end with `101`**.

### Why this is commonly confused

`Contains` means the pattern can occur **anywhere**.
`Ends with` means it must occur at the **final three positions**.

### Memory

For "contains", once `101` has occurred, we never need to forget that fact.

### States

* `q0`: no partial match
* `q1`: suffix `1`
* `q2`: suffix `10`
* `qA`: `101` has occurred

### Transition table

| State | 0  | 1   |
| ----- | -- | --- |
| → q0  | q0 | q1  |
| q1    | q2 | q1  |
| q2    | q0 | *qA |
| *qA   | qA | qA  |

Accepted: `10100`
Rejected: `10011`

**Contrast:** `10100` is accepted for **contains 101**, but rejected for **ends with 101**.

### Common mistake

Making the accepting state non-absorbing when solving "contains".

---

# TOPIC 11 — First symbol equals last symbol

### Exam question

Construct a DFA where the **first symbol equals the last symbol**.

### Memory

Store the first symbol and continuously update the last symbol.

### States

`q00,q01,q10,q11`, where the first digit is remembered and the second digit is current last digit.

### Transition table

| State | 0   | 1   |
| ----- | --- | --- |
| → qε  | q00 | q11 |
| q00   | q00 | q01 |
| *q01  | q00 | q01 |
| q10   | q10 | q11 |
| *q11  | q10 | q11 |

Final: `q00,q11`.

Accepted: `1010`
Rejected: `1011`

### Common mistake

Forgetting that the **first symbol must be preserved forever**.

---

# TOPIC 12 — First symbol differs from last symbol

### Exam question

Construct a DFA where the **first symbol differs from the last symbol**.

### Memory

Store first symbol + current last symbol.

### Transition table

| State | 0    | 1    |
| ----- | ---- | ---- |
| → qε  | q00  | q11  |
| q00   | q00  | *q01 |
| *q01  | q00  | q01  |
| *q10  | q10  | q11  |
| q11   | *q10 | q11  |

Final: `q01,q10`.

Accepted: `1011`
Rejected: `1010`

### Common mistake

Accepting when **any pair** differs rather than first vs last.

---

# TOPIC 13 — First symbol compared with second-last

### Exam question

Construct a DFA where the **first symbol equals the second-last symbol**.

### Memory

We need:

1. first symbol permanently;
2. enough recent history to identify the second-last symbol.

### State meaning

`qabc` can be interpreted as:

* first symbol = `a`
* current last two symbols = `bc`

### Transition table

| State | 0    | 1    |
| ----- | ---- | ---- |
| → qε  | q00  | q11  |
| q00   | q000 | q001 |
| q01   | q010 | q011 |
| q10   | q100 | q101 |
| q11   | q110 | q111 |

For states `qabc`, transition by dropping `b` and appending new symbol.

**Final states:** second-last = first.

Thus:
`q000,q001,q110,q111` are final.

Accepted: `1010` → first `1`, second-last `1`
Rejected: `1000` → first `1`, second-last `0`

### Common mistake

Comparing first with the **last** symbol.

---

# TOPIC 14 — First two symbols equal last two symbols

### Exam question

Construct a DFA where the **first two symbols equal the last two symbols**.

### Memory

Store the first two symbols permanently + current last two symbols.

### State meaning

`qAB/CD` = first two symbols are `AB`, current last two are `CD`.

### Transition table

| State  | 0      | 1      |
| ------ | ------ | ------ |
| → qε   | q0     | q1     |
| q0     | q00/00 | q00/01 |
| q1     | q01/10 | q01/11 |
| q00/00 | q00/00 | q00/01 |
| q00/01 | q00/10 | q00/11 |
| q01/00 | q01/00 | q01/01 |
| q01/01 | q01/10 | q01/11 |
| q10/00 | q10/00 | q10/01 |
| q10/01 | q10/10 | q10/11 |
| q11/00 | q11/00 | q11/01 |
| q11/01 | q11/10 | q11/11 |

Final states are where the two pairs match:

`q00/00, q01/01, q10/10, q11/11`.

Accepted: `0110`
Rejected: `0111`

### Common mistake

Comparing the first two with the **second two**, rather than the final two.

---

# TOPIC 15 — First k symbols equal last k symbols

### Exam question

Construct a DFA where the **first 3 symbols equal the last 3 symbols**.

### Memory

Store:

* first 3 symbols permanently;
* rolling last 3 symbols.

### State meaning

`q(P,S)` where:

* `P` = stored first 3 symbols;
* `S` = current last 3 symbols.

### Transition rule

For every `P ∈ {000,...,111}`:

| Current state | Input 0    | Input 1    |
| ------------- | ---------- | ---------- |
| `q(P,abc)`    | `q(P,bc0)` | `q(P,bc1)` |

Final states:

`q(P,P)` for every 3-bit `P`.

### Accepted

`001001` → first 3 = last 3 = `001`.

### Rejected

`001011` → first 3 = `001`, last 3 = `011`.

### Common mistake

Trying to store only the first 3 symbols and forgetting that the **last 3 must continuously update**.

---

# TOPIC 16 — Sliding window condition

### Exam question

Construct a DFA where **every substring of length 4 contains at most two 0s**.

### Why?

Every newly completed window of length 4 must be checked.

### Memory

Keep the **last 3 symbols**. When a new symbol arrives, they form the next length-4 window.

### States

`qabc` = last three symbols are `abc`.

### Transition table

| State  | 0    | 1    |
| ------ | ---- | ---- |
| `q000` | D    | q001 |
| `q001` | D    | q011 |
| `q010` | D    | q101 |
| `q011` | q110 | q111 |
| `q100` | D    | q001 |
| `q101` | q010 | q011 |
| `q110` | q100 | q101 |
| `q111` | q110 | q111 |

`D` = violation/dead state.

For strings shorter than 4, use the corresponding prefix states.

### Final states

All non-dead states.

Accepted: `0101` → window has two 0s.
Rejected: `0001` → window has three 0s.

### Common mistake

Checking only the total number of zeros instead of **each length-4 window**.

---

# TOPIC 17 — Pending obligation condition

### Exam question

Construct a DFA where **every occurrence of `00` must be immediately followed by `1`**.

### Why?

Seeing `00` creates an obligation: **the next symbol must be 1**.

### Memory

Remember whether we are currently waiting for a required `1`.

### States

* `q0`: no pending obligation
* `q1`: one trailing `0`
* `q2`: just saw `00`; must receive `1`
* `D`: violation

### Transition table

| State | 0  | 1  |
| ----- | -- | -- |
| → q0  | q1 | q0 |
| q1    | q2 | q0 |
| q2    | D  | q0 |
| D     | D  | D  |

Final: `q0,q1,q2`.

Accepted: `00101`
Rejected: `0001`

### Common mistake

Allowing `000`: the first `00` is immediately followed by `0`, violating the rule.

---

# TOPIC 18 — Contains P but not Q

### Exam question

Construct a DFA that **contains `000` but does not contain `0000`**.

### Why?

We need two pieces of information:

1. Has `000` appeared?
2. Has `0000` appeared?

### Memory

Track consecutive zeros.

### States

* `q0`: no trailing 0
* `q1`: one trailing 0
* `q2`: two trailing 0s
* `q3`: `000` has occurred, currently three trailing 0s
* `D`: `0000` occurred

### Transition table

| State | 0   | 1  |
| ----- | --- | -- |
| → q0  | q1  | q0 |
| q1    | q2  | q0 |
| q2    | *q3 | q0 |
| *q3   | D   | q0 |
| D     | D   | D  |

Final: `q3`.

Accepted: `10001`
Rejected: `0000`

### Common mistake

Thinking `0000` should be accepted because it **contains `000`**. The "but not 0000" condition overrides that.

---

# TOPIC 19 — Length condition + positional condition

### Exam question

Construct a DFA for strings of **length at least 5 whose third symbol from the right is 1**.

### Why?

This combines:

* minimum length;
* suffix positional condition.

### Memory

Need at least five symbols and ultimately the **last three symbols**.

### States

Store enough information to know length and the last 3 symbols.

For `n ≥ 3`, use suffix states `qabc`; acceptance requires:

* length ≥ 5;
* `a = 1`.

### Transition table

| State  | 0    | 1    |
| ------ | ---- | ---- |
| `qε`   | q0   | q1   |
| `q0`   | q00  | q01  |
| `q1`   | q10  | q11  |
| `q00`  | q000 | q001 |
| `q01`  | q010 | q011 |
| `q10`  | q100 | q101 |
| `q11`  | q110 | q111 |
| `qabc` | qbc0 | qbc1 |

Final states are `q100,q101,q110,q111`, **but only after length ≥5**.

Accepted: `00110` → length 5, third-from-right = 1.
Rejected: `00100` → length 5, third-from-right = 0.

### Common mistake

Checking the third-from-right condition but forgetting `length ≥ 5`.

---

# TOPIC 20 — Combined memory condition

### Exam question

Construct a DFA where the **first symbol differs from the third symbol from the right**.

### Why?

This requires two different memories:

* prefix memory: first symbol;
* suffix memory: last 3 symbols.

### Memory

Store first symbol + rolling last three symbols.

### State meaning

`q(P,abc)`:

* `P` = first symbol;
* `abc` = current last three symbols.

### Transition table

| Current state | 0          | 1          |
| ------------- | ---------- | ---------- |
| `q(P,abc)`    | `q(P,bc0)` | `q(P,bc1)` |

### Final condition

Accept iff:

`P ≠ a`

where `a` is the first bit of the final 3-symbol suffix.

Accepted: `1000` → first = 1, third-from-right = 0.
Rejected: `0110` → first = 0, third-from-right = 1 actually **accepted**.

Better rejected example: `1001` → first = 1, third-from-right = 0 → accepted.
`0111` → first = 0, third-from-right = 1 → accepted.

A rejected example is `0001`: first = 0, third-from-right = 0.

### Common mistake

Comparing first symbol with the **last** symbol instead of third-from-right.

---

# TOPIC 21 — Distance-based condition

### Exam question

Construct a DFA for strings containing **two `1`s separated by exactly three symbols**.

Equivalent pattern:

`1 _ _ _ 1`

### Why?

The DFA must remember how far we are from a previously seen `1`.

### Memory

Track an active `1` and its distance.

### States

* `q0`: no relevant previous `1`
* `q1`: just saw `1`
* `q2`: one symbol after that `1`
* `q3`: two symbols after
* `q4`: three symbols after
* `qA`: condition satisfied

### Transition table

| State | 0  | 1   |
| ----- | -- | --- |
| → q0  | q0 | q1  |
| q1    | q2 | q1  |
| q2    | q3 | q1  |
| q3    | q4 | q1  |
| q4    | q0 | *qA |
| *qA   | qA | qA  |

Accepted: `10001`
Rejected: `1001` — only two symbols between the 1s? `1 00 1` = 2 symbols.

### Common mistake

Confusing **three symbols between** with **distance 3**. Here there must be exactly **three symbols in between**, so positions differ by 4.

---

# TOPIC 22 — Recent-history condition

### Exam question

Construct a DFA for strings where **there is a `1` within the last three positions**.

### Why?

Only recent history matters.

### Memory

Distance since the most recent `1`.

### States

* `q0`: no `1` in last 3 positions
* `q1`: last symbol is `1`
* `q2`: last `1` was 2 positions ago
* `q3`: last `1` was 3 positions ago

### Transition table

| State | 0   | 1   |
| ----- | --- | --- |
| → q0  | q0  | *q1 |
| *q1   | *q2 | *q1 |
| *q2   | *q3 | *q1 |
| *q3   | q0  | *q1 |

Final: `q1,q2,q3`.

Accepted: `0010` → last 3 = `010`, contains `1`.
Rejected: `0000`.

### Common mistake

Interpreting it as "the string contains a `1` somewhere." An old `1` eventually leaves the last-three-position window.

---

# FINAL SUMMARY

## 1. Which topics use suffix memory?

Primarily:

* **5** — last symbol
* **6** — second-last
* **7** — kth from right
* **8** — last two relation
* **9** — ends with pattern
* **10** — ends-with part
* **16** — sliding window
* **19** — third from right
* **20** — third from right
* **22** — recent history

**Rule:** If the condition talks about the **end/right side**, think **suffix memory**.

---

## 2. Which use prefix memory?

* **1** — first symbol
* **2** — kth from left
* **3** — first k symbols
* **4** — relationship among first symbols
* **11** — first = last
* **12** — first ≠ last
* **13** — first vs second-last
* **14** — first two = last two
* **15** — first k = last k

**Rule:** If something about the beginning must be remembered until later, store a **prefix**.

---

## 3. Which use rolling-window memory?

* **7** — last 3
* **8** — last 2
* **9** — pattern matching
* **16** — last 3 to check every length-4 window
* **19** — last 3
* **20** — last 3
* **22** — last 3 / distance from last `1`

**Core idea:**

> To determine a property involving the last `k` symbols, remember the current last `k` symbols.

---

## 4. Which use product-state construction?

Most importantly:

* **11** — first symbol × current last symbol
* **12** — first symbol × current last symbol
* **13** — first symbol × last-two memory
* **14** — first-two memory × last-two memory
* **15** — first-k memory × last-k memory
* **20** — first-symbol memory × last-3 memory
* **19** — length memory × suffix memory

### Product-state rule

If you need two independent memories:

> **DFA state = Memory A × Memory B**

Example:

`first symbol` has 2 possibilities
`last 3 symbols` has 8 possibilities

So roughly:

**2 × 8 = 16 states**

before minimization/short-string handling.

---

# 5. Most common university-exam categories

If you're preparing specifically for DFA construction questions, prioritize:

| Priority        | Topics                                      |
| --------------- | ------------------------------------------- |
| ⭐⭐⭐ Very common | First/last symbol, kth from left/right      |
| ⭐⭐⭐ Very common | Ends with pattern / contains pattern        |
| ⭐⭐⭐ Very common | First = last / first ≠ last                 |
| ⭐⭐⭐ Very common | Last two equal/different                    |
| ⭐⭐ Common       | First k = last k                            |
| ⭐⭐ Common       | Pattern constraints                         |
| ⭐⭐ Common       | Length + positional condition               |
| ⭐⭐ Common       | "Every substring..." / window constraints   |
| ⭐⭐ Common       | "Every occurrence..." obligation conditions |
| ⭐ Harder        | Combined prefix + suffix memory             |
| ⭐ Harder        | Multiple simultaneous constraints           |

---

# 6. State-count estimation rules

| Category                      |                          Rough memory/state count |
| ----------------------------- | ------------------------------------------------: |
| First symbol                  |                                           `2 + 1` |
| kth from left                 |                 `k + 1` plus decision/dead states |
| First k symbols               |                  up to `2^k` prefix possibilities |
| First two relation            |                 few states; remember first symbol |
| Last symbol                   |                                               `2` |
| kth from right                |                            roughly `2^k` suffixes |
| Last k relation               |                            roughly `2^k` suffixes |
| Ends with pattern of length m |                                     roughly `m+1` |
| Contains pattern length m     |                                     roughly `m+1` |
| First = last                  |                                           `2 × 2` |
| First k = last k              |                         roughly `2^k × 2^k = 4^k` |
| Sliding window length k       |           up to `2^(k-1)` useful recent histories |
| Pending obligation            | usually a small number of "waiting" states + dead |
| Contains P but not Q          |                   product of memories for P and Q |
| Length + positional           |             **length memory × positional memory** |
| Prefix + suffix               |                 **prefix states × suffix states** |
| Distance condition            |                   one state per relevant distance |
| Recent-history k              |                     roughly `k+1` distance states |

### The exam-design shortcut

When you see a DFA question, ask:

**1. What information about the past can affect the future?**
→ That is your **memory**.

**2. How many different versions of that memory are possible?**
→ Those become **states**.

**3. Does the condition concern the beginning, ending, or both?**

* Beginning → **prefix memory**
* Ending → **suffix memory**
* Every recent window → **rolling memory**
* Beginning + ending → **product construction**
* "Must happen next" → **pending obligation**
* "Exactly k positions apart" → **distance memory**

**Most important mindset:** don't start by drawing states. Start by writing:

> **"What must the DFA remember after reading an arbitrary prefix?"**

That sentence usually tells you exactly what your states need to mean.
