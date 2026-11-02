# 10. Exam Cheat Sheet

> Everything you need in the exam on one page per topic: **which method**, **the rules**, **the formulas**, and **the sentence to write**.
> Each topic links back to its full note if you need the "why".

**Contents**
0. [The routine for every question](#0-the-routine-for-every-question)
1. [Formulation](#1-formulation)
2. [Standard form: slack, excess, artificial](#2-standard-form-slack-excess-artificial)
3. [Graphical method](#3-graphical-method)
4. [Simplex](#4-simplex)
5. [Big M](#5-big-m)
6. [Special cases: the four tells](#6-special-cases-the-four-tells)
7. [Sensitivity: shadow price, reduced cost, ranges](#7-sensitivity-shadow-price-reduced-cost-ranges)
8. [Duality](#8-duality)
9. [Transportation](#9-transportation)
10. [Game theory](#10-game-theory)
11. [Networks](#11-networks)
12. [Short-answer bank](#12-short-answer-bank)
13. [Your personal traps](#13-your-personal-traps)

---

## 0. The routine for every question

1. **Diagnose:** "This is a ___ problem because ___." (1 line, usually worth marks)
2. **Run the method:** show every table, entering/leaving variable, row operations.
3. **Answer in words, with units:** "Make 20 chairs and 10 shelves for $13,000 profit. Timber and finishing are fully used; 10 labour days are spare."

### Which method?

| The question has… | Method | Note |
|---|---|---|
| supplies, demands, a cost grid | Transportation | [7](07_Transportation.md) |
| two opponents, a payoff table | Game theory | [8](08_Game_Theory.md) |
| nodes and roads/pipes, "quickest route" | Shortest path | [9](09_Networks.md) |
| nodes and roads, "connect everything, least cable" | Minimum spanning tree | [9](09_Networks.md) |
| an LP with **2 variables** | Graphical | [2](02_Graphical_Method.md) |
| an LP, all `≤`, RHS ≥ 0 (origin works) | Simplex | [3](03_Simplex_Method.md) |
| an LP with `≥` or `=` (origin fails) | Big M, then simplex | [4](04_BigM_and_Special_Cases.md) |
| "one more unit worth", "binding", "range" | Shadow price | [5](05_Sensitivity_Shadow_Price_Reduced_Cost.md) |
| "not produced", "how much must profit rise", "new product" | Reduced cost | [5](05_Sensitivity_Shadow_Price_Reduced_Cost.md) |
| "dual", "bound", "certify optimal", "value of resources" | Duality | [6](06_Duality.md) |

---

## 1. Formulation

**Three parts, always:**
1. **Decision variables**, with units: "x₁ = kg of brand A per week". Never call a variable z.
2. **Objective:** max profit or min cost, with units ("z in $100s").
3. **Constraints**, one per limit/requirement, each labelled, plus **xⱼ ≥ 0**.

| Words | Symbol |
|---|---|
| "at most", "no more than", "up to", "available", "capacity" | `≤` |
| "at least", "no less than", "minimum", "requirement" | `≥` |
| "exactly", "all of", "must total" | `=` |
| "A is at least 30% of the total" | x_A ≥ 0.3(x_A + x_B + x_C) → **0.7x_A − 0.3x_B − 0.3x_C ≥ 0** |
| "at least twice as many A as B" | x_A ≥ 2x_B → **x_A − 2x_B ≥ 0** |

Reading it: always move every variable to the left-hand side so the RHS is a plain number.

**Check every coefficient against the table in the question** (your Exam 2 typo: 0.01 instead of 0.10 cost you two parts).

---

## 2. Standard form: slack, excess, artificial

| Constraint | Add | Name | Formula | Meaning |
|---|---|---|---|---|
| `≤` | **+ s** | slack | **s = RHS − LHS** | how much is **left over / unused** |
| `≥` | **− e** (+ a) | excess (surplus) | **e = LHS − RHS** | how much you went **over** the requirement |
| `=` | **+ a** | artificial only | none (an equality has **no slack**) | nothing real; must be 0 at the end |

Reading it: slack and excess are always ≥ 0. A negative one means the plan **breaks** that constraint (infeasible).

| Value | Word | Sentence for the exam |
|---|---|---|
| s or e = 0 | **binding** | "All 18 kiln hours are used up; kiln time is what limits the plan." |
| s or e > 0 | **non-binding** | "4 litres of glaze are left over; glaze isn't limiting anything." |

**Explain without the words "slack" or "binding"** (asked in Exam 1): "There are 4 kiln hours left over, so we could make more mugs and earn more. So this plan can't be the best."

**Before you start:**
* **Negative RHS:** multiply the row by −1 (flips `≤` ↔ `≥`).
* **Min problem:** max z′ = −z. At the end, **z = −z′**.
* **How many artificials?** Plug the origin into every row. Every row that **fails** (a `≥` with positive RHS, or an `=`) gets one. Say which rows and why.

**Basic solutions:** n variables (after adding slacks) and m equations → **n − m variables are 0** at a basic solution; there are at most **C(n, m)** of them. Set the chosen ones to 0, solve for the rest; feasible only if all are ≥ 0.

---

## 3. Graphical method

1. Draw each constraint line (find both intercepts), shade the allowed side, label the lines.
2. List **every corner** and its z value in a table. (Missing z values = lost marks.)
3. Pick the best z. Or slide the isoprofit line: max → furthest out, min → closest in.

**Slope of ax + by = c is −a/b.**

**Objective coefficient range** (how far a price can move before the plan changes):
1. Find the two **binding** lines at the optimal corner.
2. Their slopes −a/b.
3. Require the profit slope −c₁/c₂ to sit **between** them; solve for the changing price.

| Picture | Meaning |
|---|---|
| objective parallel to a binding edge | **alternative optima**: every point on that edge (give the segment, e.g. 2x₁ + x₂ = 16, 3 ≤ x₁ ≤ 6) |
| region open in the improving direction | **unbounded** |
| no overlapping region | **infeasible** |
| min problem, open region, positive costs | still has an optimum: cost only grows as you move further out, so the minimum is at a corner |

**Shadow price graphically:** RHS + 1, re-solve, **new z − old z**.

---

## 4. Simplex

| Step | Rule |
|---|---|
| Start | slacks are basic; you're at the origin |
| **Enter** | most negative number in the z row (variable columns only) |
| **Leave** | ratio RHS ÷ entering-column entry, **positive entries only**, smallest wins |
| Pivot | divide the pivot row by the pivot; then **new row = old row − (its entry in pivot column) × new pivot row** |
| Stop | no negatives in the z row (max) |

**Write the row ops** every pivot: `R₂′ = R₂/3`, `R₁′ = R₁ − R₂′`, `Rz′ = Rz + 4R₂′`.

**Checks after every pivot:** entering column = 1 with 0s elsewhere (z row too); all RHS ≥ 0; z never gets worse.

**Reading any table:**

| Look at | It tells you |
|---|---|
| Basis column + RHS | the basic variables' values |
| variables not in the Basis column | **= 0** |
| z row, RHS | current z (remember the units, and z = −z′ for a min) |
| final z row, under a slack/excess | **shadow price** (section 7) |
| final z row, under a non-basic decision variable | **reduced cost** |
| final z row, **0** under a **non-basic** variable | **alternative optima** |

**Basis** = the list of variables in the Basis column, e.g. {x₁, x₂, s₃}.

Ratio test tie → pick either; the next table has a basic variable equal to 0 (degenerate). Carry on as normal.

---

## 5. Big M

1. **Test the origin** in every row. Rows that fail get an artificial.
2. Standard form: +s, −e, +a.
3. **Penalise:** max → **−Maᵢ** in the objective, for **every** artificial. (Min: turn into max z′ = −z first, then −Maᵢ.)
4. Write the z row: `z − c₁x₁ − … + Ma₁ = 0` (so **+M under each artificial**).
5. **Clear the M's: Rz − M × (each artificial's row).**

| Try | Entry under a | Result |
|---|---|---|
| Rz **+** M·R | M + M = 2M | wrong |
| Rz **−** M·R | M − M = **0** | right |

Reading it: a basic variable must have 0 in the z row, so **subtract**. Only the artificial rows are used, so only their RHS appears (e.g. −12M).

6. Run simplex. **Comparing M terms:** the bigger number in front of −M is more negative (−4 − 3M beats −2 − M). Unsure? Put M = 1000.
7. Once an artificial leaves, ignore its column.

**End of Big M:**
* artificial still basic with value > 0 → **infeasible**
* otherwise read the answer as normal (min: cost = −z′)

---

## 6. Special cases: the four tells

| Situation | The tell in the table | What to write |
|---|---|---|
| **Infeasible** | stopped, but an **artificial is still basic with value > 0** | "no plan satisfies every constraint; they contradict each other" |
| **Unbounded** | entering column has **no positive entry**, so no ratio test | "profit can grow forever; the model is missing a limit" |
| **Alternative optima** | final z row has **0 under a non-basic variable** | "pivot it in to find a second best corner; every point between them is also optimal" |
| **Degenerate** | a basic variable = 0 (ratio tie) | "still fine; simplex may pivot without z changing" |

**"Already optimal" at the origin with an artificial basic** = the M's were never cleared (Exam 2 Q5).

---

## 7. Sensitivity: shadow price, reduced cost, ranges

### Where to look (final table)

| Number under… | Name | Meaning |
|---|---|---|
| a slack s (`≤` constraint) | **shadow price** | z change per **+1** of that RHS |
| an excess e (`≥` constraint) | shadow price, **sign flipped** for a max | see the table below |
| a non-basic decision variable xⱼ | **reduced cost** | how much z drops per unit if xⱼ is forced in |
| a **basic** slack (resource has spare) | 0 | shadow price **0**, more of it is worthless |

### Shadow price signs

| Problem | Constraint | Look under | RHS + 1 does |
|---|---|---|---|
| max | `≤` limit | s | profit **rises** by the number |
| max | `≥` requirement | e | profit **falls** by the number |
| min (solved as max z′ = −z) | `≥` requirement | e | cost **rises** by the number |
| min (solved as max z′ = −z) | `≤` limit | s | cost **falls** by the number |
| any | non-binding | – | **0** |

Reading it: loosening a limit helps; tightening a requirement hurts. **Unsure? Re-solve with RHS + 1: shadow price = new z − old z.**

**Units:** if z is in $100s, a shadow price of 1 means **$100**. Always convert.

### RHS range (where the shadow price stays valid)

Change constraint i's RHS by Δ. Use **its slack column** (for a `≥`, use **minus** its excess column):
```
new basic value = (current RHS value) + Δ × (entry in that column)   ≥ 0   for every basic variable
```
Furniture, timber, s₁ column (2, −2, −3):
```
x₁ = 20 + 2Δ ≥ 0  →  Δ ≥ −10
s₂ = 10 − 2Δ ≥ 0  →  Δ ≤ 5
x₃ = 10 − 3Δ ≥ 0  →  Δ ≤ 10/3
⇒ −10 ≤ Δ ≤ 10/3  ⇒  40 ≤ timber ≤ 53⅓      (convert Δ back to the RHS!)
```
* **Inside the range:** new z = old z + Δ × shadow price. Say "inside the range" first.
* **Outside the range:** the formula is wrong. The basis changes, so **re-solve**.
* **"Buy k extra units at $P total?"** Check k is inside the range; gain = k × shadow price; **accept if gain > P**.

### Reduced cost (a product not made)

```
reduced cost = (its resources valued at shadow prices) − (its profit)
```
* Positive → losing money, don't make it. Its profit must rise **by the reduced cost** before it's worth making.
* **New product?** Same formula. **Negative → make it** (it earns more than its resources are worth elsewhere). This says *whether*, not *how many*: re-solve for that.
* Products you **do** make have reduced cost **0**.

| Change | Plan (x values) | z |
|---|---|---|
| RHS (amount of a resource) | **moves** (same binding constraints, inside the range) | + shadow price × Δ |
| profit of a product you make | **stays** (inside its range) | + Δ × its amount |
| profit of a product you don't make | stays until the rise passes the reduced cost | unchanged |

### Excel Solver report

| Column | Meaning |
|---|---|
| Final Value (variables) | the optimal plan |
| Reduced Cost | loss per unit if forced in (Solver shows it **negative** for a max) |
| Allowable Increase / Decrease (variables) | how far the profit coefficient can move with the **same plan** |
| Shadow Price | z change per +1 RHS |
| Allowable Increase / Decrease (constraints) | the RHS **range** where the shadow price holds |

### Sentences to write

* **Binding:** "Timber has shadow price $100 per m³: each extra m³ adds $100 of profit, valid between 40 and 53⅓ m³."
* **Non-binding:** "Labour has 10 days spare, so its shadow price is $0; extra labour adds nothing."
* **`≥` requirement:** "Each extra kg the contract requires lowers profit by $1."
* **Reduced cost:** "Tables have reduced cost $300: forcing one in loses $300, so a table's profit must rise from $400 to at least $700."
* **Which resource to buy:** the one with the **largest shadow price**, if it costs less than that.

---

## 8. Duality

### Writing the dual (max with `≤` ↔ min with `≥`)

| Primal (max) | Dual (min) |
|---|---|
| one constraint per resource | **one variable yᵢ per constraint** (value of that resource) |
| one variable per product | **one constraint per product** |
| RHS amounts | dual objective coefficients: **min w = Σ RHSᵢ yᵢ** |
| profits | dual RHS |
| a product's **column** (what it uses) | its dual constraint: **column · y ≥ profit** |
| `≤`, xⱼ ≥ 0 | `≥`, yᵢ ≥ 0 |
| (rare) `≥` row / `=` row in a max | yᵢ ≤ 0 / yᵢ free |

Reading it: **read DOWN the columns**, not across. Call the dual objective **w**. Write 0 coefficients explicitly.

**Meaning to write:** "yᵢ = the value of one unit of resource i, e.g. what a buyer would have to offer for it."

### The theorems

| Name | Statement | Use |
|---|---|---|
| **Weak duality** | any feasible z ≤ any feasible w | a dual-feasible y gives a **ceiling** on profit, without solving |
| **Strong duality** | optimal z\* = optimal w\* | **certify optimal**: a feasible plan and a dual-feasible y with z = w are **both** optimal |
| **Dual values = shadow prices** | y\* = final primal z row under the slacks | read y\* straight off the tableau |

**Check a y is dual-feasible:** plug it into every dual constraint (≥ profit for each product) and y ≥ 0. Then w = Σ RHS × y is an upper bound.

### Complementary slackness

| If… | then… | why |
|---|---|---|
| a resource has spare (slack > 0) | **yᵢ = 0** | more of something you already have spare is worthless |
| yᵢ > 0 | that constraint is **binding** | a resource only has value if you're short of it |
| a product is made (xⱼ > 0) | its dual constraint is **tight** (=) | made products break even at the shadow prices |
| a dual constraint has a **gap** | **xⱼ = 0**, and gap = **reduced cost** | it loses the gap on every unit, so don't make it |

Rule in one line: **(slack) × y = 0** and **(amount made) × (gap) = 0**.

**Finding y\* from x\* (no tableau):** furniture x\* = (20, 0, 10), labour has spare.
```
labour spare           →  y₂ = 0
chairs made (tight)    →  2y₁ + 4y₂ + 3y₃ = 5  →  2y₁ + 3y₃ = 5
shelves made (tight)   →   y₁ + 2y₂ + 2y₃ = 3  →   y₁ + 2y₃ = 3
solve                  →  y₃ = 1, y₁ = 1      ⇒  y* = (1, 0, 1),  w = 50 + 80 = 130 = z* ✓
```

**Why solve the dual?** 400 products, 3 resources: primal = 400 variables, dual = **3 variables**. Much smaller, same optimal value, and it gives the shadow prices.

---

## 9. Transportation

1. **Balance:** total supply vs total demand.
   * supply > demand → **dummy destination**, cost 0 ("left at the source")
   * demand > supply → **dummy source**, cost 0 ("demand not met")
2. **Northwest corner:** start top-left, fill as much as possible, move right if the column is satisfied, down if the row is used up. Write the table and the **cost**.
3. **Check cells = m + n − 1** (count the dummy). Too few (degenerate)? Put a 0 in a cell next to the corner where a row and column finished together.
4. **u, v:** set u₁ = 0; on **used** cells **uᵢ + vⱼ = cᵢⱼ**.
5. **Reduced costs** on **empty** cells: **c̄ᵢⱼ = cᵢⱼ − uᵢ − vⱼ**.
   * all c̄ ≥ 0 → **optimal**; a c̄ = 0 → **alternative optimum**
   * else the **most negative** enters
6. **Loop:** from the entering cell, turn only at **used** cells, signs + − + −.
7. **θ = smallest amount on a − cell.** Add θ to +, subtract from −. The cell hitting 0 leaves.
8. **New cost = old cost + θ × c̄.** Recheck the arithmetic by summing the new plan.

Draw the grid like this so you never flip back:

|  | S1 (v=7) | S2 (v=8) | Dummy (v=5) |
|---|---|---|---|
| Q1 (u=0) | $7 → 40 | $4 [−4] | $0 [−5] |
| Q2 (u=−2) | $5 → 10 | $6 → 40 | $0 [−3] |

Reading it: "$cost → amount" for used cells, [c̄] for empty ones, u and v in the headers.

**Why the loop works:** each + in a row/column is cancelled by a − in the same row/column, so all totals stay right; the cost change per unit = the c̄.

---

## 10. Game theory

1. **Dominance first** (repeat until nothing changes):
   * **Rows** (row player wants **big**): row A ≥ row B in every column → delete B.
   * **Columns** (column player wants **small**): column A ≤ column B in every row → delete **B**.
2. **Saddle point test:**
   * **maximin** = biggest of the **row minimums**
   * **minimax** = smallest of the **column maximums**
   * equal → saddle point: the entry that is the **smallest in its row AND largest in its column**. Both play pure strategies, value = that number.
   * not equal → mixed strategy.
3. **Mixed, 2 rows:** x₁ = P(R1), x₂ = 1 − x₁. Set the payoffs against the two remaining columns **equal**, solve, then v = either side.
4. **Write the LP** (needed when asked, or for 3+ choices):
```
max v
s.t. (column 1 numbers) · x ≥ v      ← one constraint per OPPONENT column
     (column 2 numbers) · x ≥ v
     x₁ + … + xₘ = 1,  x ≥ 0          (v any sign)
```
* Column player: **min w**, one constraint per **row**, row · y ≤ w. It's the **dual** of the row player's LP, so **v = w** = value of the game.
* **Check:** the deleted column gives the row player ≥ v at your x.
* Answer with probabilities **and** the value **in words**: "R plays R1 4/9 of the time and R2 5/9; R gains 2/3 a point per game on average."

---

## 11. Networks

### Shortest path (label-setting / Dijkstra)

1. Box A = 0. Label its neighbours (distance, via).
2. Box the **unboxed node with the smallest total distance**.
3. From it, update each neighbour if (its distance + edge) is **smaller**. Write rejected ones with ✗.
4. Repeat until the destination is boxed. Trace back through "via".

| Round | Box | Updates |
|---|---|---|
| 1 | A = 0 | B 4 (A), C 3 (A) |
| 2 | C = 3 | B 5 ✗, D 11 (C), E 9 (C) |
| … | … | … |

Reading it: one row per boxed node, so the marker can follow. Give the **route and its length**.

### Minimum spanning tree (Prim)

Start anywhere; repeatedly add the **cheapest edge reaching a new node**; never close a loop. n nodes → **n − 1 edges**. Give the edges with their lengths and the total.

| | Shortest path | MST |
|---|---|---|
| Question | one route A → B | connect **all** nodes |
| Lock in each step | closest **node** (total distance) | cheapest **edge** to a new node |

### The LP behind shortest path

x_ij = 1 if edge i→j is used. min Σ length × x_ij, s.t. (out − in) = +1 at the start, −1 at the end, 0 everywhere else (**conservation of flow**), x ≥ 0.

---

## 12. Short-answer bank

| Question | Answer |
|---|---|
| Why is the optimum at a corner? | The objective is **linear** (a flat plane, no interior peak). From any interior point you can move uphill until a constraint stops you, then along the edge until another stops you: a corner (or a whole edge if parallel). |
| Shadow price 0 means? | The constraint is **non-binding**: there's spare at the optimum, so one more unit can't help (complementary slackness). |
| 0 in the z row under a non-basic **decision** variable? | **Alternative optima.** Pivot it in for a second optimal corner; report both and every point between. |
| Why solve the dual? | Fewer variables (dual of 400 × 3 has 3 variables); same optimal value (strong duality); gives shadow prices. |
| Why Big M / artificials? | `≥` and `=` rows fail at the origin, so simplex has no starting corner. Artificials give a fake start; the −M penalty forces them to 0. |
| Why must the M's be cleared? | Basic variables must have 0 in the z row; otherwise the z row is wrong and can falsely look optimal. |
| Why can a min have an optimum on an unbounded region? | With positive costs and x ≥ 0, cost only grows as you move further out, so the minimum is reached at a corner of the region. |
| Why does a shadow price have a range? | Past the range a different constraint becomes binding, the corner changes, so the rate changes. |
| Why does the transportation starting plan need m + n − 1 cells? | One of the m + n supply/demand equations is redundant (totals balance), so a basic solution has m + n − 1 basic cells. |
| What is a reduced cost, in words? | How much the objective worsens per unit if a product not being made is forced into the plan; equivalently, how much its profit must rise to be worth making. |

---

## 13. Your personal traps

From marking your Practice Exam 2 (see `work/ans2_fixed.md`). Check these before handing in.

| Trap | Fix |
|---|---|
| z in **$100s**, wrote "$1" | multiply: **1 → $100**, 130 → $13,000 |
| binding / non-binding backwards | **basic slack > 0 → spare**; **non-basic slack = 0 → fully used** |
| clearing M with + | **Rz − M·(artificial row)** |
| forgot −M for one artificial | one **−Mᵢ per artificial** |
| only the final tableau | every tableau + entering/leaving + row ops |
| left out the "interpret / for the owner" part | finish every part with a sentence in words |
| "strong duality" with no numbers | read y\*, check feasibility, show w = z |
| checked x when asked about y | y is the **dual**: plug into **dual** constraints |
| saddle point from a matching number | must be **row min AND column max** |
| optimal set included infeasible points | limit the edge: e.g. 3 ≤ x₁ ≤ 6 |
| Δ range left as Δ | convert to the RHS range (40 ≤ timber ≤ 53⅓) and say "inside the range" |
| transcribed a coefficient wrong | re-check every number against the question's table |
