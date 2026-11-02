# 8. Two-Player Zero-Sum Games

> **In one sentence:** two opponents choose at the same time. If there's a choice neither of them wants to move away from, they both play it (a **saddle point**). If not, each should pick at random with the right probabilities, chosen so the opponent can't take advantage.

---

## 8.1 The story

**Two cafés next door (revision 2 Q2).** Every morning, each café chooses to run a special on **coffee** or **pastry**. They decide at the same time, without knowing what the other picked.

The table shows how many customers (in hundreds) **café 1 wins from café 2**:

|  | Rival: coffee | Rival: pastry |
|---|---|---|
| **Café 1: coffee** | 2 | 5 |
| **Café 1: pastry** | 6 | 1 |

**Reading it:** if café 1 does coffee and the rival does pastry, café 1 wins 500 customers from the rival.

**Zero-sum:** every customer café 1 gains, café 2 loses. So:
* **café 1 (rows) wants BIG numbers**
* **the rival (columns) wants SMALL numbers**

Keep those two lines in your head. Everything below comes from them.

---

## 8.2 Play it out: does anyone want to switch?

Imagine they play every day and each learns what the other usually does.

### The café game: they go round in circles

| Today they play | Number | Who's unhappy? | They switch to… |
|---|---|---|---|
| coffee, coffee | 2 | café 1: pastry would give 6 instead of 2 | pastry, coffee |
| pastry, coffee | 6 | rival: pastry would give 1 instead of 6 | pastry, pastry |
| pastry, pastry | 1 | café 1: coffee would give 5 instead of 1 | coffee, pastry |
| coffee, pastry | 5 | rival: coffee would give 2 instead of 5 | coffee, coffee ← back to the start |

**Reading it:** whatever they do, someone wants to switch, so they chase each other around forever. **There's no stable choice.** Anything predictable gets taken advantage of.

### A different game: they settle down

Change the numbers:

|  | Rival: coffee | Rival: pastry |
|---|---|---|
| **Café 1: coffee** | **3** | 4 |
| **Café 1: pastry** | 1 | 2 |

Look at (coffee, coffee) = 3:
* **Café 1:** switching to pastry gives 1, which is worse than 3. Stays.
* **Rival:** switching to pastry gives 4, which is worse for the rival (it wants small). Stays.

**Nobody wants to switch, so it's stable.** That cell is a **saddle point**. Both play coffee every day, and café 1 wins 3 each time. That 3 is called the **value of the game**.

> **Saddle point = a cell neither player wants to move away from.**
> Check: it's the **smallest number in its row** (the rival can't push it lower) AND the **biggest number in its column** (café 1 can't push it higher).

---

## 8.3 Shortcut for finding a saddle point: think like a pessimist

Checking every cell for "does anyone want to switch?" is slow. Instead, each player asks:

> **"For each of my choices, what's the worst that could happen? I'll pick the choice whose worst case is best."**

* **Café 1's worst case for each row** is the **smallest** number in that row. Pick the row with the biggest one. This is the **maximin** (max of the row minimums).
* **The rival's worst case for each column** is the **biggest** number in that column. Pick the column with the smallest one. This is the **minimax** (min of the column maximums).

**If maximin = minimax, that cell is a saddle point.** If they're different, there isn't one.

### Café game

|  | coffee | pastry | **Café 1's worst (row min)** |
|---|---|---|---|
| **coffee** | 2 | 5 | **2** ← best worst |
| **pastry** | 6 | 1 | 1 |
| **Rival's worst (column max)** | 6 | **5** ← best worst | |

Maximin = 2, minimax = 5. **Not equal, so no saddle point.** That matches the circle in 8.2.

### Politician game (lecture, 3 × 3)

|  | Both | Big | Mega | **Row's worst (min)** |
|---|---|---|---|---|
| **Both** | −3 | −2 | 6 | −3 |
| **Big** | 2 | **0** | 2 | **0** ← best worst |
| **Mega** | 5 | −2 | −4 | −4 |
| **Column's worst (max)** | 5 | **0** ← best worst | 6 | |

Maximin = 0, minimax = 0. **Equal, so (Big, Big) is a saddle point**, value **0**.
Check: 0 is the smallest in its row (2, 0, 2) ✓ and the biggest in its column (−2, 0, −2) ✓.

---

## 8.4 Before that: cross out choices that are never worth it (dominance)

Do this **first**. It makes the table smaller.

**Rows (café 1 wants big):** if row A is **≥ row B in every column**, café 1 would never pick B, whatever the rival does. Cross out B.

**Columns (rival wants small):** if column A is **≤ column B in every row**, the rival would never pick B. Cross out B.

⚠️ The direction is **opposite** for columns, because the column player wants small numbers.

**Example:** row "Both" = (1, 2, 4) and row "Mega" = (0, 1, −1).
1 ≥ 0, 2 ≥ 1, 4 ≥ −1. "Both" is better in every column, so **cross out Mega**.

Keep going until nothing more can be crossed out. Crossing one out can make a new one appear.

---

## 8.5 No saddle point → mix it up

In the café game, any **fixed** choice gets taken advantage of. So café 1 should **pick at random**: coffee on some days, pastry on others, so the rival can't predict it.

**The question is: how often should it pick coffee?**

### Try it the slow way: count mornings

The game again, so you don't have to scroll:

|  | Rival: coffee | Rival: pastry |
|---|---|---|
| **Café 1: coffee** | 2 | 5 |
| **Café 1: pastry** | 6 | 1 |

**p = the fraction of mornings café 1 runs the coffee special.** p = 0.5 means half the mornings. It's easiest to picture **4 mornings**.

#### One example: p = 0.5 (2 coffee mornings, 2 pastry mornings)

**(a) Suppose the rival runs coffee every morning.** Read down the "Rival: coffee" column:

| Morning | Café 1 runs | Rival runs | Café 1 wins |
|---|---|---|---|
| 1 | coffee | coffee | 2 |
| 2 | coffee | coffee | 2 |
| 3 | pastry | coffee | 6 |
| 4 | pastry | coffee | 6 |
| | | **Average** | (2 + 2 + 6 + 6) ÷ 4 = **4** |

**(b) Suppose the rival runs pastry every morning.** Read down the "Rival: pastry" column:

| Morning | Café 1 runs | Rival runs | Café 1 wins |
|---|---|---|---|
| 1 | coffee | pastry | 5 |
| 2 | coffee | pastry | 5 |
| 3 | pastry | pastry | 1 |
| 4 | pastry | pastry | 1 |
| | | **Average** | (5 + 5 + 1 + 1) ÷ 4 = **3** |

**(c) Which one happens?** The rival wants café 1 to win **as little as possible**, so it picks pastry, holding café 1 to **3**. Café 1 can only **count on the smaller** of the two: **3**.

#### Now every p at once

Each row does exactly what (a), (b) and (c) did above, for a different p:

| p | Café 1's 4 mornings | (a) rival always coffee: average | (b) rival always pastry: average | (c) café 1 can count on (the smaller) |
|---|---|---|---|---|
| 0 | P P P P | (6+6+6+6) ÷ 4 = 6 | (1+1+1+1) ÷ 4 = 1 | 1 |
| 0.25 | C P P P | (2+6+6+6) ÷ 4 = 5 | (5+1+1+1) ÷ 4 = 2 | 2 |
| 0.5 | C C P P | (2+2+6+6) ÷ 4 = 4 | (5+5+1+1) ÷ 4 = 3 | 3 |
| 0.75 | C C C P | (2+2+2+6) ÷ 4 = 3 | (5+5+5+1) ÷ 4 = 4 | 3 |
| 1 | C C C C | (2+2+2+2) ÷ 4 = 2 | (5+5+5+5) ÷ 4 = 5 | 2 |
| **5/8** | 5 C and 3 P **out of 8** | (5×2 + 3×6) ÷ 8 = **3.5** | (5×5 + 3×1) ÷ 8 = **3.5** | **3.5** ← best |

**Reading it:**
* Column (a): more coffee mornings means more 2s and fewer 6s, so it **falls** as p goes up.
* Column (b): more coffee mornings means more 5s and fewer 1s, so it **rises** as p goes up.
* Column (c) is the smaller of the two. Café 1 wants this **as big as possible**, and that happens where (a) and (b) are **equal**: p = 5/8, guaranteed **3.5**.
* Without mixing (p = 0 or 1), the best café 1 could count on was 2.

**As a formula:** column (a) is "p of the mornings give 2, the rest give 6" = **2p + 6(1 − p)**. Column (b) is **5p + 1(1 − p)**. Same calculation, without the mornings.

### Check it with real mornings

p = 5/8 means: over 8 mornings, coffee on 5 and pastry on 3 (in random order).

* Rival always does **coffee**: 5 × 2 + 3 × 6 = 10 + 18 = 28 over 8 days = **3.5 a day**
* Rival always does **pastry**: 5 × 5 + 3 × 1 = 25 + 3 = 28 over 8 days = **3.5 a day**

Either way it's 3.5. **The rival can't do anything about it.** That's the point of mixing correctly.

### The shortcut: set the two averages equal

The best p is where the two averages are equal, so solve that directly:
```
2p + 6(1 − p) = 5p + 1(1 − p)
     6 − 4p   =   1 + 4p
          5   =   8p
          p   =   5/8
```
Value v = 2(5/8) + 6(3/8) = 10/8 + 18/8 = **3.5**.

### See it

![Mixed strategy lower envelope](img/game_mixed.png)

**Reading the picture:** the two lines are columns (a) and (b) of the table above, drawn for every p, not just the six we tried. The rival always holds café 1 to the **lower** line (shaded). The highest point of the shaded part is where the lines **cross**: p = 5/8, value 3.5.

### The rival does the same

The rival picks coffee with probability q, and café 1 will pick whichever **row** is better for itself. Set the two rows equal:
```
coffee row: 2q + 5(1 − q)  =  pastry row: 6q + 1(1 − q)
            5 − 3q         =  1 + 5q
                 q         =  1/2
```
Value = 2(½) + 5(½) = **3.5**, the same number.

**Answer in words:** café 1 should run the coffee special on 5/8 of mornings and pastry on 3/8, at random. The rival should do 50/50. On average café 1 wins 350 customers a day, and **neither can do better** by changing alone.

---

## 8.6 The LP: the same thing, written for any size

The "set them equal" shortcut only works for 2 choices. With 3 or more choices you write an LP. **It says exactly what the slow-way table said:**

```
max v                                ← make the guaranteed amount as big as possible
s.t. 2x₁ + 6x₂ ≥ v                   ← if rival plays coffee, I still get at least v
     5x₁ + 1x₂ ≥ v                   ← if rival plays pastry, I still get at least v
     x₁ + x₂ = 1                     ← the probabilities add up to 1
     x₁, x₂ ≥ 0                      (v can be any sign)
```
* x₁ = chance of coffee (p), x₂ = chance of pastry (1 − p).
* "≥ v" in **every** opponent column means v is the **worst case** (the smaller average).
* "max v" means **make the worst case as good as possible**, which is the "best" row of the slow-way table.

**Recipe for the row player's LP:**
1. One probability per **row** (your choices).
2. One constraint per **column** (the opponent's choices): that column's numbers × your probabilities ≥ v.
3. Probabilities add to 1, all ≥ 0.
4. Maximise v.

### Link to duality (note 6)

The rival's problem is: **min w** such that every **row**'s average (using the rival's probabilities) is **≤ w**. That's the **dual** of café 1's LP. By strong duality, **v = w**: what café 1 can guarantee (3.5) equals what the rival can hold it to (3.5). That shared number is the **value of the game**.

---

## 8.7 The procedure for any game question

1. **Cross out dominated** rows and columns (8.4). Repeat until none are left.
2. **Saddle point test** (8.3): maximin vs minimax.
   * **Equal** → saddle point. Each player always plays that choice. Value = that number. Done.
   * **Not equal** → go to step 3.
3. **Mix** (8.5–8.6): 2 × 2 → set the two averages equal. Bigger → write the LP.

---

## Common mistakes

1. Column dominance the wrong way round. The column player wants **small** numbers.
2. Using the row **maximums** for maximin. It's the biggest of the row **minimums** (the pessimist's choice).
3. In the row player's LP, writing one constraint per **row**. It's one per **column** (one per opponent choice).
4. Forgetting x₁ + x₂ = 1.
5. Giving only probabilities. Also give the **value** and say it in words.

---

## Check yourself

<details><summary>1. Revision 2 Q4: rows A = (5, 9, 3), B = (9, 8, 8), C = (4, 3, 6). Solve.</summary>

**Dominance:** B vs C: 9 ≥ 4, 8 ≥ 3, 8 ≥ 6, so **cross out C**. A vs B: A has 9 > 8 in column 2, so A stays.

|  | col 1 | col 2 | col 3 | row min |
|---|---|---|---|---|
| A | 5 | 9 | 3 | 3 |
| B | 9 | 8 | **8** | **8** ← maximin |
| col max | 9 | 9 | **8** ← minimax | |

Maximin 8 = minimax 8, so the **saddle point is (B, column 3), value 8**. Check: 8 is the smallest in row B and the biggest in column 3 ✓.
</details>

<details><summary>2. Two children play a game: rows (2, −3) and (−3, 4). Saddle point? If not, solve it.</summary>

|  | col 1 | col 2 | row min |
|---|---|---|---|
| row 1 | 2 | −3 | −3 |
| row 2 | −3 | 4 | −3 |
| col max | 2 | 4 | |

Maximin −3, minimax 2. **No saddle point**, so mix.
Set the averages equal, with p = chance of row 1:
2p − 3(1 − p) = −3p + 4(1 − p) → 5p − 3 = 4 − 7p → p = 7/12.
x = (7/12, 5/12), v = 5(7/12) − 3 = **−1/12**. (On average, the row child loses slightly.)
</details>

<details><summary>3. Paper–Scissors–Rock. Rows P = (0, −1, 1), S = (1, 0, −1), R = (−1, 1, 0). Write the row player's LP.</summary>

No dominance. Every row min is −1 and every column max is 1, so there's no saddle point, and the players should mix. With 3 choices, write the LP:
```
max v
s.t. column P:  0xP + 1xS − 1xR ≥ v
     column S: −1xP + 0xS + 1xR ≥ v
     column R:  1xP − 1xS + 0xR ≥ v
     xP + xS + xR = 1, all x ≥ 0
```
Answer: 1/3 each, v = 0. Any lean towards one choice could be taken advantage of.
</details>
