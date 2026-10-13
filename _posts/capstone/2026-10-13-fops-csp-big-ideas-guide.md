---
toc: true
layout: post
title: "AP CSP, Every Topic, Built Into Our Capstone"
description: "Team Triple T's full study guide to every College Board AP CSP topic (Big Ideas 1 to 5, topics 1.1 to 5.6), with College Board pseudocode, working Python, exam traps, and how each one shows up in our Friends of Poway Seniors capstone."
permalink: /capstone/fops-2026-2027/csp-guide/
author: Aaditya Prem, Chetan Tiduwar, Kashyap Tubati
comments: false
---

**Team Triple T:** Chetan Tiduwar, Aaditya Prem, Kashyap Tubati. Capstone: [Friends of Poway Seniors 2026–2027](/capstone/fops-2026-2027/).

After our practice MCQ we only wrote about the questions we missed, and we went through the test too fast to learn much from each question. This guide fixes that. It covers **every topic in the College Board Course and Exam Description**, not only the ones we got wrong. Each topic has:

- **What it is**, in plain words.
- **College Board pseudocode** (the language the exam uses), when the topic has code.
- **Python** that does the same thing and actually runs.
- **Exam traps**: what the question is really testing, and how people get it wrong.
- **In our capstone**: where we already use it, or will, on the FOPS site.

The last three sections connect everything to our capstone page: which topics help which part of the site, how we will integrate them sprint by sprint, and what we learned.

| Big Idea | Topics | Exam weight |
|---|---|---|
| 1. Creative Development | 1.1–1.4 | 10–13% |
| 2. Data | 2.1–2.4 | 17–22% |
| 3. Algorithms and Programming | 3.1–3.18 | 30–35% |
| 4. Computer Systems and Networks | 4.1–4.3 | 11–15% |
| 5. Impact of Computing | 5.1–5.6 | 21–26% |

---

## College Board pseudocode cheat sheet

The exam gives you a reference sheet, but you lose time if you have to look everything up. These are the rules that cause the most mistakes.

| Pseudocode | Meaning | Python |
|---|---|---|
| `a ← expression` | store a value | `a = expression` |
| `a = b`, `a ≠ b` | compare (true/false) | `a == b`, `a != b` |
| `a MOD b` | remainder | `a % b` |
| `DISPLAY(x)` | print, followed by a space | `print(x, end=" ")` |
| `INPUT()` | read a value from the user | `input()` |
| `RANDOM(a, b)` | random integer from a to b, **both included** | `random.randint(a, b)` |
| `aList[i]` | element at index i, **first element is index 1** | `a_list[i - 1]` |
| `APPEND(aList, v)` | add v to the end | `a_list.append(v)` |
| `INSERT(aList, i, v)` | put v at index i, shift the rest right | `a_list.insert(i - 1, v)` |
| `REMOVE(aList, i)` | remove the element at index i | `a_list.pop(i - 1)` |
| `LENGTH(aList)` | number of elements | `len(a_list)` |
| `REPEAT n TIMES` | loop exactly n times | `for _ in range(n):` |
| `REPEAT UNTIL(condition)` | loop while the condition is **false** | `while not condition:` |
| `FOR EACH item IN aList` | visit every element | `for item in a_list:` |
| `PROCEDURE name(p)` / `RETURN(x)` | define a procedure / send a value back | `def name(p):` / `return x` |
| `MOVE_FORWARD()`, `ROTATE_LEFT()`, `ROTATE_RIGHT()`, `CAN_MOVE(dir)` | robot on a grid | (exam only) |

Two rules cost the most points: **lists start at 1**, and **`REPEAT UNTIL` stops when the condition becomes true**. If a list index is ever 0 or bigger than `LENGTH(list)`, the program ends with an error.

---

# Big Idea 1: Creative Development

## 1.1 Collaboration

**What it is.** Computing innovations are built by teams, and teams that include people with different backgrounds and perspectives catch problems a single person would miss. Collaboration tools include version control, shared documents, and issue trackers. Pair programming means one person writes code (driver) while the other reviews it as it is written (navigator).

**Exam traps.** Questions ask for the *benefit* of collaboration. The correct answer is almost always about diverse perspectives reducing bias or catching errors, not "it's faster." Collaboration can also mean gathering feedback from users, not only teammates.

**In our capstone.** Our team splits work by game (Scam Defense, Bingo, Head Nod) and shares the site and Size It Up. We track work in GitHub Issues and a kanban board with sub-issues for each feature, and our older-adult users are the most important "collaborators": we design for their feedback, like larger text and fewer menus.

## 1.2 Program Function and Purpose

**What it is.** Every program has a **purpose** (the problem it solves) and a **function** (what it does). Programs take **input** (from a user, a sensor, or another program), produce **output** (text, sound, visuals), and are often **event-driven**: code runs when an event happens, like a click or a key press.

```text
WHEN the "Start" button is clicked
    DISPLAY("Round 1")
```

```python
def on_start_clicked():
    print("Round 1")

on_start_clicked()   # in a real app the button calls this, not us
```

**Exam traps.** "Which of these is an input?" includes things like a mouse click, a GPS location, or a value read from a file. Event-driven code doesn't run top to bottom; it waits.

**In our capstone.** Every game is event-driven: button clicks in Scam Defense, the camera detecting a nod in Head Nod, dragging the corner handle in Size It Up.

## 1.3 Program Design and Development

**What it is.** Development is **iterative** (build, test, improve, repeat) and **incremental** (add one small working piece at a time). Design starts by investigating what users need (surveys, interviews, observation), then planning with diagrams or storyboards. Programs should be documented with comments, and code from others must be credited.

**Exam traps.** Iterative means *repeating the cycle with feedback*; incremental means *building in pieces*. Documentation is useful during development, not only at the end. Using someone else's code without credit is a problem even if it works.

**In our capstone.** We started from the 2025–2026 team's FOPS site, listed what stops an older adult from using it, and fixed it in small working pieces. Each game shipped in steps: rules first, then the page, then saved progress.

## 1.4 Identifying and Correcting Errors

**What it is.** Four kinds of error:

| Error | What happens | Example |
|---|---|---|
| Syntax | the code breaks the language rules and won't run | missing `)` |
| Logic | it runs but gives the wrong answer | `<` where `≤` was needed |
| Run-time | it crashes while running | index past the end of a list, dividing by zero |
| Overflow | a number is too big for the bits that store it | adding 1 to the largest 8-bit value |

Ways to find errors: test cases (including the edge cases), hand tracing, extra output statements, and debuggers.

```python
def average(scores):
    total = 0
    for s in scores:
        total += s
    return total / len(scores)   # run-time error if scores is empty

print(average([90, 80]))        # 85.0
# print(average([]))            # ZeroDivisionError: an edge case to test for
```

**Exam traps.** If the program *ran* and gave a wrong result, it is a **logic** error, not a syntax error. A good test case is one that would catch the bug, usually at a boundary (0, 1, empty list, the last element).

**In our capstone.** We found a real logic error in Size It Up: France came out 15% too big because French Guiana was counted as part of France. The code ran fine; it just gave the wrong area. We fixed it by leaving out far-away territories, then found Indonesia was now 23% too small, and fixed that too. That's iterative testing.

---

# Big Idea 2: Data

## 2.1 Binary Numbers

**What it is.** Computers store everything as **bits** (0 or 1). A group of 8 bits is a **byte**. Each binary place is a power of 2, so `1011` is 8 + 0 + 2 + 1 = 11. With **n bits you can store 2ⁿ different values**: 8 bits gives 256 values (0 to 255). Using a fixed number of bits causes **overflow** (the number is too big) and **rounding errors** (real numbers can't all be stored exactly). The same bits can mean a number, a letter, a color, or part of a sound, depending on how they are read: that's **abstraction**.

```text
PROCEDURE toDecimal(bits)        { bits is a list of 0s and 1s }
{
    value ← 0
    FOR EACH b IN bits
    {
        value ← value * 2 + b
    }
    RETURN(value)
}
```

```python
def to_decimal(bits):
    value = 0
    for b in bits:
        value = value * 2 + b
    return value

def to_binary(n, width=8):
    return format(n, f"0{width}b")

print(to_decimal([1, 0, 1, 1]))  # 11
print(to_binary(200))            # 11001000
print(0.1 + 0.2)                 # 0.30000000000000004 (a rounding error)
```

**Exam traps.** Adding 1 bit **doubles** the number of values; it doesn't add one. Comparing a binary number to a decimal one means converting first. Hexadecimal isn't on the exam, but binary-to-decimal conversions always are.

**In our capstone.** Our Bingo engine's random generator (mulberry32) works directly on 32-bit numbers and uses `>>> 0` to keep results inside 32 bits, which is exactly the fixed-bits idea that causes overflow.

## 2.2 Data Compression

**What it is.** Compression makes data smaller by using fewer bits. **Lossless** compression can rebuild the original exactly (needed for text, code, and spreadsheets). **Lossy** compression throws some data away for a much smaller file (fine for photos, music, and video when people won't notice). A simple lossless method is **run-length encoding**: store repeated values once with a count.

```python
def run_length_encode(text):
    out = []
    i = 0
    while i < len(text):
        j = i
        while j < len(text) and text[j] == text[i]:
            j += 1
        out.append(f"{text[i]}{j - i}")
        i = j
    return "".join(out)

print(run_length_encode("AAAABBBCCD"))   # A4B3C2D1
```

**Exam traps.** Lossy is not "worse"; the question asks what fits the *situation*. If the original must come back exactly (a bank record, a program), only lossless works. If size matters most (streaming video), lossy is the right choice. Compression saves storage *and* transmission time.

**In our capstone.** The world map in Size It Up uses the TopoJSON format, a compressed map format where shared borders are stored once, and we convert it back to shapes in the browser. Our photos for the FOPS site should use lossy compression (JPEG/WebP) so pages load quickly for seniors on slow connections.

## 2.3 Extracting Information from Data

**What it is.** Data can show trends, patterns, and correlations. **Metadata** is data about data (a photo's date and location); changing metadata doesn't change the data itself. Big datasets need computers to process them, and data often has to be **cleaned** first (fixing inconsistent spelling, removing duplicates and invalid values). **Correlation does not mean causation**, and a dataset can't answer a question it has no data for.

```python
events = [
    {"name": "Bingo", "month": "Oct", "attendance": 42},
    {"name": "bingo", "month": "Oct", "attendance": 38},
    {"name": "Tech Help", "month": "Oct", "attendance": 15},
]
by_event = {}
for e in events:
    key = e["name"].strip().title()          # cleaning: "bingo" and "Bingo" are the same
    by_event[key] = by_event.get(key, 0) + e["attendance"]
print(by_event)                              # {'Bingo': 80, 'Tech Help': 15}
```

**Exam traps.** "Which question can be answered with this data?" The answer must use only fields that exist. If the dataset has no ages, it can't tell you what age group attends most. Collecting more data doesn't remove bias if the new data comes from the same skewed source.

**In our capstone.** The FOPS events page is a dataset. Grouping attendance by event type tells us which events to promote. Our saved game progress (how often each scam type is caught or missed) tells us which scams seniors struggle with most.

## 2.4 Using Programs with Data

**What it is.** Programs **filter** data (keep only some rows), **transform** it (change each row), **combine** datasets, and **visualize** it (charts). Spreadsheets and databases do this at scale.

```text
seniorEvents ← []
FOR EACH event IN events
{
    IF (event.audience = "seniors")
    {
        APPEND(seniorEvents, event)
    }
}
```

```python
events = [{"name": "Bingo", "audience": "seniors"},
          {"name": "Teen Coding", "audience": "teens"},
          {"name": "Tech Help", "audience": "seniors"}]
senior_events = [e["name"] for e in events if e["audience"] == "seniors"]
print(senior_events)   # ['Bingo', 'Tech Help']
```

**Exam traps.** Know which operation answers the question: filtering removes rows, sorting reorders them, and neither changes the values. A chart can mislead if the axis doesn't start at zero.

**In our capstone.** The Scam Defense "weak spots" feature filters the scam types a player still misses and sorts them worst first, so the player sees exactly what to practice.

---

# Big Idea 3: Algorithms and Programming

## 3.1 Variables and Assignments

**What it is.** A variable is a named place to store a value. Assignment replaces the old value. The right side is evaluated **first**, then stored.

```text
a ← 1
b ← a
a ← 2
DISPLAY(b)          { displays 1, not 2 }
```

```python
a = 1
b = a
a = 2
print(b)            # 1
x, y = 3, 5
x, y = y, x         # swap; in pseudocode you need a temp variable
print(x, y)         # 5 3
```

**Exam traps.** Assignment copies the *value at that moment*. Swapping two variables in pseudocode needs a third variable (`temp ← a`, `a ← b`, `b ← temp`); doing `a ← b` then `b ← a` makes both the same.

**In our capstone.** Every game tracks state in variables: the round number, the score, the current scenario. Good names (`roundNumber`, not `r`) make the code readable for our teammates.

## 3.2 Data Abstraction

**What it is.** A **list** stores many values under one name, so the program can handle any number of items without a variable for each. That's data abstraction: you work with "the list of scores" instead of `score1`, `score2`, `score3`. Strings are like lists of characters.

```text
scores ← [90, 75, 88]
DISPLAY(scores[1])          { 90: the first element }
```

```python
scores = [90, 75, 88]
print(scores[0])            # 90 (Python starts at 0)
print(len(scores))          # 3
```

**Exam traps.** Pseudocode starts at index 1. The benefit of a list is managing complexity: the code stays the same whether there are 3 items or 3,000.

**In our capstone.** `SCENARIOS` in Scam Defense is one list of 10 scenario pairs. Adding an 11th scam needs one new item, not new code. Bingo cards are a 5×5 list of lists.

## 3.3 Mathematical Expressions

**What it is.** Arithmetic operators `+ - * /` and `MOD` (remainder), with normal order of operations (MOD has the same priority as `*` and `/`). An **algorithm** is a finite set of instructions; every algorithm can be built from **sequencing** (steps in order), **selection** (if), and **iteration** (loops).

```text
DISPLAY(17 MOD 5)           { 2 }
DISPLAY(2 + 3 * 4)          { 14 }
```

```python
print(17 % 5)               # 2
print(2 + 3 * 4)            # 14
print(10 % 2 == 0)          # True: MOD 2 checks even/odd
```

**Exam traps.** `a MOD b` is always between 0 and b−1 for positive numbers. `MOD 2 = 0` means even. Sequencing matters: the same steps in a different order can give a different result.

**In our capstone.** Size It Up's scoring is math: accuracy = smaller area ÷ larger area × 100, so guessing half or double both score 50%. Bingo uses `Math.floor((n - 1) / 15)` to turn a ball number into its letter (1–15 is B, 16–30 is I, and so on).

## 3.4 Strings

**What it is.** A string is an ordered sequence of characters. **Concatenation** joins strings; a **substring** is part of a string. Strings have a length and can be compared.

```text
first ← "Poway"
DISPLAY(CONCAT(first, " Seniors"))     { the exam may write string joins as a procedure }
```

```python
first = "Poway"
full = first + " Seniors"
print(full)              # Poway Seniors
print(full[0:5])         # Poway (substring)
print(len(full))         # 13
print(full.lower().count("o"))   # 2
```

**Exam traps.** Concatenation doesn't add spaces for you. `"5" + "5"` is `"55"`, not 10. Read how the question defines its string procedures; the exam describes them in the question.

**In our capstone.** Bingo's `spoken()` builds strings like "B 7" for the caller. Scam Defense teaches people to read sender addresses closely as strings: the real bank is `alerts@coastalfederal.example`, while the scam uses `security@coastal-federal-verify.example`.

## 3.5 Boolean Expressions

**What it is.** A Boolean value is true or false. Relational operators (`=`, `≠`, `<`, `≤`, `>`, `≥`) produce Booleans. Logical operators combine them: `NOT`, `AND` (both true), `OR` (at least one true). **De Morgan's laws**: `NOT (a AND b)` equals `NOT a OR NOT b`, and `NOT (a OR b)` equals `NOT a AND NOT b`.

```python
age, member = 70, False
print(age >= 65 and member)        # False
print(age >= 65 or member)         # True
a, b = True, False
print((not (a and b)) == ((not a) or (not b)))   # True: De Morgan
```

**Exam traps.** "Which expression is equivalent?" Test it with values just below, at, and above the boundary. `NOT (x > 5)` is `x ≤ 5`, not `x < 5`.

**In our capstone.** A senior discount check: `age ≥ 65 OR isMember`. Size It Up's bot difficulty and win checks are Boolean conditions.

## 3.6 Conditionals

**What it is.** Selection: run a block only if a condition is true (`IF`), optionally with an alternative (`ELSE`).

```text
IF (score ≥ 90)
{
    DISPLAY("Great job")
}
ELSE
{
    DISPLAY("Keep practicing")
}
```

```python
score = 82
if score >= 90:
    print("Great job")
else:
    print("Keep practicing")
```

**Exam traps.** An `IF` without `ELSE` may do nothing at all, and that's a logic error if something was supposed to happen. Watch `<` vs `≤` at the boundary value.

**In our capstone.** Scam Defense: `IF` the player picked the trustworthy message, the round counts as caught; `ELSE` the scam type drops back to box 1.

## 3.7 Nested Conditionals

**What it is.** Conditionals inside conditionals, for decisions with more than two outcomes. Order matters: once a branch runs, the others are skipped.

```text
IF (accuracy ≥ 90)
{
    DISPLAY("Perfect")
}
ELSE
{
    IF (accuracy ≥ 60)
    {
        DISPLAY("Close")
    }
    ELSE
    {
        DISPLAY("Way off")
    }
}
```

```python
def rating(accuracy):
    if accuracy >= 90:
        return "Perfect"
    elif accuracy >= 60:
        return "Close"
    else:
        return "Way off"

for a in [95, 90, 75, 30]:
    print(a, rating(a))
```

**Exam traps.** If the checks are in the wrong order (`≥ 60` first), the `≥ 90` branch never runs. Trace each test value through every branch.

**In our capstone.** Size It Up's `roundWinner` is a three-way decision: a tie if the two accuracies are equal, otherwise player A or player B. Scam Defense's scheduler is a chain of conditions in a set order: missed and due, then never seen, then due, then a weighted pick.

## 3.8 Iteration

**What it is.** Repeating code: `REPEAT n TIMES`, `REPEAT UNTIL(condition)`, and `FOR EACH`. A loop that never reaches its stopping condition is an **infinite loop**.

```text
count ← 0
REPEAT UNTIL (count = 3)
{
    count ← count + 1
    DISPLAY(count)
}
{ displays 1 2 3 }
```

```python
count = 0
while not count == 3:     # REPEAT UNTIL runs while the condition is false
    count += 1
    print(count, end=" ")
print()
total = 0
for n in range(1, 6):     # 1 to 5
    total += n
print(total)              # 15
```

**Exam traps.** Off-by-one errors: count the passes on paper with a table. `REPEAT UNTIL` checks *before* each pass, so if the condition is already true it runs zero times.

**In our capstone.** Bingo's caller loops through the shuffled calling order one ball at a time; Size It Up loops through 5 rounds; our Leitner scheduler loops through scam types to find the one that's due.

## 3.9 Developing Algorithms

**What it is.** Different algorithms can solve the same problem, and some are clearer or faster. Algorithms can be built from existing ones (finding a max or min, a sum or average, checking divisibility). Two algorithms that look different can still produce the same result.

```text
PROCEDURE findMax(numList)
{
    max ← numList[1]
    FOR EACH n IN numList
    {
        IF (n > max)
        {
            max ← n
        }
    }
    RETURN(max)
}
```

```python
def find_max(nums):
    best = nums[0]          # start with a real value, not 0
    for n in nums:
        if n > best:
            best = n
    return best

print(find_max([-5, -2, -9]))   # -2 (starting at 0 would wrongly return 0)
```

**Exam traps.** Starting `max` at 0 breaks when every value is negative. "Do these two code segments always produce the same result?" means test edge cases, not just one normal input.

**In our capstone.** Our Leitner scheduler is an algorithm we designed: missed types that are due come first, then new types, then the most overdue review, otherwise a weighted random pick.

## 3.10 Lists

**What it is.** List operations (`APPEND`, `INSERT`, `REMOVE`, `LENGTH`) and **traversal**: visiting every element, completely or partially. **Linear search** checks each element in order.

```text
names ← ["Ann", "Bo"]
APPEND(names, "Cy")          { ["Ann", "Bo", "Cy"] }
INSERT(names, 1, "Al")       { ["Al", "Ann", "Bo", "Cy"] }
REMOVE(names, 3)             { ["Al", "Ann", "Cy"] }
DISPLAY(LENGTH(names))       { 3 }
```

```python
names = ["Ann", "Bo"]
names.append("Cy")
names.insert(0, "Al")
names.pop(2)
print(names, len(names))     # ['Al', 'Ann', 'Cy'] 3

def linear_search(items, target):
    for i, item in enumerate(items):
        if item == target:
            return i
    return -1

print(linear_search(names, "Cy"))   # 2
```

**Exam traps.** `INSERT` and `REMOVE` shift the indexes of every later element. Removing items while looping forward through the same list skips elements.

**In our capstone.** Bingo checks 12 winning lines (5 rows, 5 columns, 2 diagonals), each a list of 5 squares, using `every()` on each line: a traversal inside a traversal.

## 3.11 Binary Search

**What it is.** Binary search finds a value in a **sorted** list by checking the middle and throwing away half the list each step. For n items it takes about log₂(n) checks: 1,000 items take at most 10, while linear search may take 1,000.

```python
def binary_search(sorted_items, target):
    low, high = 0, len(sorted_items) - 1
    steps = 0
    while low <= high:
        steps += 1
        mid = (low + high) // 2
        if sorted_items[mid] == target:
            return mid, steps
        if sorted_items[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1, steps

data = list(range(1, 1001))
print(binary_search(data, 737))   # (736, 10): found in 10 steps
```

**Exam traps.** Binary search **requires sorted data**. On unsorted data it can miss the value. Know the number of steps: doubling the list adds only one step.

**In our capstone.** Not needed yet: our lists are small. If FOPS grows a searchable list of hundreds of events or resources, we'd sort it by date and search it this way.

## 3.12 Calling Procedures

**What it is.** A procedure is a named group of instructions. Calling it runs the code with **arguments** (the values passed in) that fill the **parameters**. Some procedures **return** a value; others just do something, like displaying.

```python
def area_of_rectangle(width, height):
    return width * height

result = area_of_rectangle(3, 4)   # 3 and 4 are arguments
print(result)                      # 12
print(print("hi"))                 # prints hi, then None: print returns nothing
```

**Exam traps.** `DISPLAY` shows a value; `RETURN` sends it back to the caller. A procedure stops at the first `RETURN` it reaches.

**In our capstone.** Every game calls shared procedures: `loadProgress("scam-trainer")` and `saveProgress("bingo", data)` from `progress.js`.

## 3.13 Developing Procedures

**What it is.** Writing your own procedures is **procedural abstraction**: you can use a procedure by knowing *what* it does, not *how*. Procedures reduce repeated code, and parameters make them general enough to reuse. Changing a procedure's inside doesn't break callers as long as it does the same job.

```text
PROCEDURE isEven(n)
{
    RETURN(n MOD 2 = 0)
}
```

```python
def is_even(n):
    return n % 2 == 0

print([n for n in range(1, 11) if is_even(n)])   # [2, 4, 6, 8, 10]
```

**Exam traps.** "Which procedure works for all inputs?" Test the edge cases. A procedure that uses a variable from outside instead of a parameter is less reusable.

**In our capstone.** `recordResult(state, type, caught)` hides the Leitner box logic. The trainer page just calls it, and we could change the box gaps without touching the page.

## 3.14 Libraries

**What it is.** A **library** is a collection of procedures someone else wrote. An **API** (application programming interface) is the documentation that says how to use them. Libraries save time and are usually well tested.

```python
import math
import statistics

print(math.sqrt(144))                    # 12.0
print(statistics.mean([3, 4, 5]))        # 4
```

**Exam traps.** You don't need to know how a library procedure works inside, only what its documentation says it does: inputs, outputs, and side effects.

**In our capstone.** We use MediaPipe for face tracking in Head Nod, d3-geo for equal-area map projections and real country areas in Size It Up, and topojson-client to read map data. Flask and SQLAlchemy run our backend.

## 3.15 Random Values

**What it is.** `RANDOM(a, b)` returns a random integer from a to b, **including both ends**. Every value is equally likely. Random values make programs less predictable (games, simulations).

```python
import random

roll = random.randint(1, 6)      # 1 to 6 inclusive, like RANDOM(1, 6)
print(1 <= roll <= 6)            # True

rng = random.Random(42)          # a seeded generator: same seed, same results
print([rng.randint(1, 75) for _ in range(5)])
```

**Exam traps.** `RANDOM(1, 6)` can return 1 *and* 6. "Which code simulates a 25% chance?" `RANDOM(1, 4) = 1` works; `RANDOM(1, 100) ≤ 25` also works; `RANDOM(1, 100) < 25` is 24%.

**In our capstone.** Bingo uses a **seeded** generator (mulberry32), so the same seed always gives the same card and calling order. That makes games fair, repeatable, and testable, and the backend can check a claimed win.

## 3.16 Simulations

**What it is.** A simulation is a simplified model of something real, used when the real thing is too slow, expensive, or dangerous to test. Simulations leave out details (abstraction), so results can differ from reality, and the assumptions can introduce bias. They often use random values.

```python
import random

def simulate_bingo_wait(trials=2000, seed=1):
    rng = random.Random(seed)
    total = 0
    for _ in range(trials):
        balls = list(range(1, 76))
        rng.shuffle(balls)
        mine = set(rng.sample(range(1, 76), 5))     # a simplified "line" of 5 numbers
        for calls, ball in enumerate(balls, start=1):
            mine.discard(ball)
            if not mine:
                total += calls
                break
    return total / trials

print(round(simulate_bingo_wait(), 1))   # average calls until those 5 are all called
```

**Exam traps.** A simulation can be repeated many times cheaply, but it's only as good as its model. Adding detail can make it more accurate but slower.

**In our capstone.** Size It Up's bot is a small simulation of a person guessing: its error follows a bell curve (Box-Muller), with a wider spread on Easy and a narrower one on Hard.

## 3.17 Algorithmic Efficiency

**What it is.** Efficiency is how the number of steps grows as the input grows. **Reasonable time** means polynomial growth (n, n², n³). **Unreasonable time** means exponential or factorial growth (2ⁿ, n!), which becomes impossible for big inputs. A **heuristic** gives a good-enough answer quickly when the exact answer would take too long.

```python
from itertools import permutations

def count_routes(n):
    return sum(1 for _ in permutations(range(n)))   # n! routes: unreasonable

for n in [3, 5, 8]:
    print(n, count_routes(n))    # 6, 120, 40320
```

**Exam traps.** Unreasonable doesn't mean unsolvable; it means too slow for large inputs. A heuristic doesn't guarantee the best answer.

**In our capstone.** Our scheduler picks the next scam by scanning a short list of types (linear time), which is instant. Planning a "best possible" order of all scenarios would be a permutation problem, so we use simple rules (a heuristic) instead.

## 3.18 Undecidable Problems

**What it is.** A **decidable** problem has an algorithm that always gives a correct yes/no answer. An **undecidable** problem has no algorithm that works for *every* input. The classic example is the **halting problem**: no program can always tell whether any other program will eventually stop.

**Exam traps.** Undecidable is different from unreasonable time. Unreasonable problems can be solved, just slowly. Undecidable ones can't be solved in general by any algorithm. Some inputs of an undecidable problem can still be answered.

**In our capstone.** We can't write a checker that proves any piece of new code will never freeze the page, so we rely on testing instead: running each game and tracing the edge cases.

---

# Big Idea 4: Computer Systems and Networks

## 4.1 The Internet

**What it is.** The internet is a network of networks. Devices send data in **packets**, which can take different routes and arrive out of order. **Protocols** are agreed rules:

| Protocol | Job |
|---|---|
| IP | addresses devices and routes packets |
| TCP | guarantees all packets arrive and puts them back in order |
| UDP | faster, no guarantee (video calls, games) |
| DNS | turns names like `opencodingsociety.com` into IP addresses |
| HTTP / HTTPS | how the web asks for and sends pages (HTTPS is encrypted) |

The **World Wide Web** is one system that runs *on* the internet; they are not the same thing. The internet is **scalable** because its protocols are open and anyone can follow them.

```python
from urllib.parse import urlparse

url = urlparse("https://flask.opencodingsociety.com/api/fops/progress/bingo")
print(url.scheme, url.hostname, url.path)
# https flask.opencodingsociety.com /api/fops/progress/bingo
```

**Exam traps.** Packets may arrive out of order; TCP fixes the order, IP doesn't. The internet and the web are different.

**In our capstone.** Saving progress is a real HTTP request: the browser sends `PUT /api/fops/progress/<game>` to our Flask backend with JSON in the body, the browser's JWT cookie proves who you are, and the server's CORS settings decide which websites are allowed to call it.

## 4.2 Fault Tolerance

**What it is.** A network is **fault tolerant** if it keeps working when parts fail. **Redundancy** (extra paths) makes this possible: if one connection breaks, packets go another way.

```python
links = {("A", "B"), ("B", "D"), ("A", "C"), ("C", "D")}

def connected(start, end, links):
    seen, frontier = {start}, [start]
    while frontier:
        node = frontier.pop()
        for a, b in links:
            for x, y in [(a, b), (b, a)]:
                if x == node and y not in seen:
                    seen.add(y)
                    frontier.append(y)
    return end in seen

print(connected("A", "D", links))                  # True
print(connected("A", "D", links - {("B", "D")}))   # still True: path through C
```

**Exam traps.** "How many connections can fail before A and D can't communicate?" Cross out connections on paper and look for any remaining path.

**In our capstone.** `progress.js` is fault tolerant by design: progress is always saved in the browser first, so if the backend is down or the player is signed out, nothing is lost.

## 4.3 Parallel and Distributed Computing

**What it is.** **Sequential**: one step after another. **Parallel**: steps split across processors at the same time. **Distributed**: many computers work on one problem. **Speedup** = sequential time ÷ parallel time. Parallel time is set by the **longest** branch, and some steps can't be split, so speedup has a limit.

```python
def parallel_time(task_times, processors):
    loads = [0] * processors
    for t in sorted(task_times, reverse=True):
        loads[loads.index(min(loads))] += t     # give each task to the least busy processor
    return max(loads)                           # finish time = the busiest processor

tasks = [40, 30, 50]
seq = sum(tasks)
par = parallel_time(tasks, 2)
print(seq, par, round(seq / par, 2))   # 120 70 1.71
```

**Exam traps.** Don't add the parallel tasks; take the longest path. More processors stop helping once one task is the bottleneck.

**In our capstone.** The browser and the Flask server already work as a small distributed system. Size It Up loads the world map and US states map at the same time instead of one after the other, so the game starts sooner.

---

# Big Idea 5: Impact of Computing

## 5.1 Beneficial and Harmful Effects

**What it is.** The same innovation can help and harm, often in ways nobody intended. Social media connects families and spreads misinformation; location data helps maps and enables tracking.

**Exam traps.** Questions ask for an effect that was *not intended*, or for the *most likely* harm. Several choices may be true statements; pick the one that answers the exact question.

**In our capstone.** Online services help seniors stay connected, but the same channels deliver scams. Our Scam Defense trainer exists because of that harmful effect.

## 5.2 Digital Divide

**What it is.** Unequal access to computing and the internet, because of income, location (rural areas), age, disability, or education. It's also about *skills*, not just devices.

**Exam traps.** Solutions can widen the divide if they assume everyone already has fast internet or a new phone. Policies that put services online-only can shut people out.

**In our capstone.** This is our whole audience. We cut the menu down to a few large links, added text-size buttons that remember the choice, made touch targets big, and made every game playable without an account.

## 5.3 Computing Bias

**What it is.** Bias in computing comes from **people and data**, not from the computer itself: training data that leaves groups out, or design choices that assume one kind of user.

**Exam traps.** "Use more data" only helps if the new data includes the missing groups. Bias can be unintentional.

**In our capstone.** Face tracking can work worse for some faces, lighting, or glasses, so Head Nod needs to be tested on many people. Our scam examples should include scams that target older adults specifically (grandparent scams, fake Medicare calls), not only scams aimed at younger people.

## 5.4 Crowdsourcing

**What it is.** Getting help, ideas, data, or funding from many people online. **Citizen science** lets the public collect data for research. Open source projects are crowdsourced code.

**Exam traps.** Crowdsourced data can be large and cheap but needs checking for quality and bias.

**In our capstone.** FOPS volunteers and members could report new scams they've received, which we'd review and add as training scenarios.

## 5.5 Legal and Ethical Concerns

**What it is.** Intellectual property and **copyright**, **Creative Commons** licenses (let others reuse with conditions), **open source** (code anyone can use and modify under a license), plagiarism, and ethical data collection.

**Exam traps.** Content being online doesn't make it free to use. A Creative Commons license still has conditions, like giving credit.

**In our capstone.** We use open-source libraries under their licenses and credit our data sources: Natural Earth map data in Size It Up. We don't use real people's names or messages in scam scenarios.

## 5.6 Safe Computing

**What it is.** **PII** (personally identifiable information) can identify you. **Phishing** tricks you into giving information; **keylogging** records keystrokes; **malware** is harmful software; a **rogue access point** is a fake Wi-Fi network. Defenses: strong passwords, **multi-factor authentication** (something you know, have, and are), **encryption**, and updates. **Symmetric** encryption uses one shared key; **public key** encryption uses a public key to encrypt and a private key to decrypt.

```python
def caesar(text, shift):
    out = ""
    for ch in text:
        if ch.isalpha():
            base = ord("A") if ch.isupper() else ord("a")
            out += chr((ord(ch) - base + shift) % 26 + base)
        else:
            out += ch
    return out

secret = caesar("Meet at noon", 3)
print(secret)                  # Phhw dw qrrq
print(caesar(secret, -3))      # Meet at noon: the same key decrypts (symmetric)
```

**Exam traps.** MFA protects you even when a password leaks. Public key encryption lets strangers send you encrypted data without sharing a secret first. Phishing works on people, not computers.

**In our capstone.** Scam Defense trains exactly this: lookalike sender addresses, urgent pressure, requests for gift cards or passwords, fake links. Our backend stores only hashed passwords, uses an HTTP-only JWT cookie, and our site never asks for a Social Security number or bank details.

---

# How this helps our capstone page

The topics above aren't just exam material. This table maps them to specific parts of the FOPS site and code.

| Capstone part | Topics it uses | Where it is |
|---|---|---|
| Scam Defense trainer | 3.2 lists, 3.6 conditionals, 3.9 algorithms, 3.13 procedures, 2.4 filtering, 5.6 safe computing | `assets/js/fops/scam/scheduler.js`, `trainer.js`, `scenarios.js` |
| Bingo | 3.10 list traversal, 3.15 random values, 2.1 binary (32-bit math), 3.3 math | `assets/js/fops/bingo/engine.js` |
| Size It Up | 3.3 math, 3.7 nested conditionals, 3.14 libraries, 3.16 simulation, 1.4 debugging | `assets/js/fops/geography/rules.js`, `places.js` |
| Head Nod | 1.2 event-driven input, 3.14 libraries (MediaPipe), 5.3 bias | `assets/js/fops/movement/nod.js` |
| Saved progress | 4.1 HTTP and the internet, 4.2 fault tolerance, 5.6 safe computing | `assets/js/fops/progress.js`, Flask `api/fops_progress.py` |
| Site design | 5.2 digital divide, 1.1 collaboration, 1.3 iterative design | `_layouts/fops.html`, `assets/js/fops/site.js` |

Three examples of the code, and the topics inside them:

**Procedures, conditionals, and math (3.6, 3.13, 3.3): recording a Scam Defense round.**

```javascript
export function recordResult(state, type, caught) {
  const t = typeState(state, type);
  state.round += 1;
  t.seen += 1;
  if (caught) {
    t.caught += 1;
    t.box = Math.min(3, t.box + 1);   // caught: move up a Leitner box
  } else {
    t.missed += 1;
    t.box = 1;                          // missed: back to box 1, due again soon
  }
  t.due = state.round + BOX_GAP[t.box];
  return t;
}
```

**List traversal (3.10): checking Bingo's 12 winning lines.**

```javascript
export function winningLines(card, called) {
  const has = (col, row) => card[col][row] === FREE || called.has(card[col][row]);
  return LINES.filter((line) => line.every(([c, r]) => has(c, r)));
}
```

**The internet and fault tolerance (4.1, 4.2): saving progress.**

```javascript
export function saveProgress(game, data) {
  writeLocal(game, data);   // always saved in this browser first
  fetch(`${pythonURI}/api/fops/progress/${encodeURIComponent(game)}`, {
    ...fetchOptions,
    method: 'PUT',
    body: JSON.stringify({ data }),
  }).catch(() => { /* signed out or offline: the browser copy is enough */ });
}
```

---

# How we are going to integrate it

This is how we'll use the topics on our capstone page over the next sprints, from most important to least.

| Next step | What we'll build | CSP topics | How we'll know it works |
|---|---|---|---|
| 1. Show progress to the player | A "My Progress" panel: scams caught vs. missed per type, Bingo games played, best Size It Up score, read from the saved progress | 2.3, 2.4, 3.10 | A signed-in player sees the same numbers on two different computers |
| 2. Seniors-first scam set | Add scam types that target older adults (grandparent call, fake Medicare, tech-support pop-up), with every scenario reviewed by the team | 5.1, 5.3, 5.6, 3.2 | Each new scenario has a "trusted" and a "scam" version and appears in the scheduler |
| 3. Explain the "why" after each answer | After every Scam Defense round, highlight the red flags (sender, urgency, link) in plain words | 5.6, 3.6, 1.2 | Players can name the red flag in a quick hallway test |
| 4. Fair, checkable Bingo rooms | Our backend (`api/fops_bingo.py`) already rebuilds the calling order from the room's seed and checks claimed wins with the same math; next we connect a live room page to it so seniors can play together | 3.15, 4.1, 3.12 | The server confirms a real win and rejects a fake one in a test game |
| 5. Accessibility pass | 200% zoom check, keyboard-only play, larger targets, alt text, high contrast | 5.2, 1.3 | Every game is playable with only the keyboard and at 200% zoom |
| 6. Test and debug log | A short test list per game with edge cases (empty progress, signed-out play, camera denied) | 1.4, 4.2 | All edge cases pass before each demo |
| 7. Hosting the backend | Deploy the Flask backend so the live site saves progress, not just localhost | 4.1, 4.3, 5.6 | Progress saves from the live GitHub Pages site |

---

# What we learned

**About the exam.** We rushed the practice MCQ and learned less than we should have. Going topic by topic showed us how much is underneath each question. Most of our risk wasn't hard concepts; it was small details we skipped: index 1, `REPEAT UNTIL` running while false, `RANDOM` including both ends, the longest branch in parallel time, and NOT/EXCEPT in the question. Next time we'll trace on paper, flag every guess, and review the questions we got right too.

**About our own code.** We've already used most of the CSP topics without naming them. The scam scheduler is a list-and-procedure algorithm; Bingo is list traversal with seeded random values; Size It Up is math, simulation, and debugging with real data; saving progress is the internet, fault tolerance, and safe computing in about 20 lines. Naming the topics makes it easier to explain our code and to see what's missing.

**About our audience.** Big Idea 5 is our capstone. The digital divide, bias, and safe computing aren't just exam vocabulary for us; they're why Friends of Poway Seniors needs a site that's simple, large, forgiving, and teaches people to spot scams.

**What we'll do differently.** We'll take the next practice MCQ slowly, compare the score report against this guide topic by topic, and keep this page updated as we build the integration steps above.
