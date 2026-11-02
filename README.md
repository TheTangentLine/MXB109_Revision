# MXB109 Introductory Operations Research: Revision Guide

> **The whole unit is one idea:** you choose some things, you want the best result, and you have limits. That's a **linear program (LP)**.
> Each topic is a different *shape* of LP, and the shape tells you which method to use.
>
> **In the exam:** (1) say what kind of problem it is, (2) run the method and show every step, (3) explain the answer in words.

This page is the **summary**. Each section links to a full note that explains it from the beginning, with a worked example done step by step.

---

## Contents

0. [How to use these notes](#0-how-to-use-these-notes)
1. [Which method? The decision map](#1-which-method-the-decision-map)
2. [Writing the LP and standard form](#2-writing-the-lp-and-standard-form)
3. [Slack, excess and artificial variables](#3-slack-excess-and-artificial-variables)
4. [Graphical method](#4-graphical-method)
5. [Simplex method](#5-simplex-method)
6. [Big M and the special cases](#6-big-m-and-the-special-cases)
7. [Shadow prices and reduced costs](#7-shadow-prices-and-reduced-costs)
8. [Duality](#8-duality)
9. [Transportation](#9-transportation)
10. [Game theory](#10-game-theory)
11. [Networks](#11-networks)
12. [Glossary in plain words](#12-glossary-in-plain-words)
13. [Mistakes that lose marks](#13-mistakes-that-lose-marks)
14. [Exam-day checklist](#14-exam-day-checklist)
15. [Revision plan](#15-revision-plan)

---

## 0. How to use these notes

**Start with [notes/00_START_HERE.md](notes/00_START_HERE.md)**, then read the notes in order. Notes 1–5 are one connected story.

| Note | What it's about, in plain words | Lecture | Exam weight |
|---|---|---|---|
| [01 Formulation & Standard Form](notes/01_Formulation_and_Standard_Form.md) | turning words into maths; slack, excess, artificial | Wks 1–2 | ✅ |
| [02 Graphical Method](notes/02_Graphical_Method.md) | drawing a 2-variable problem; why the answer is at a corner | Wk 3 | ✅ |
| [03 Simplex Method](notes/03_Simplex_Method.md) | walking from corner to corner using tables | Wks 5–6 | ✅✅ |
| [04 Big M & Special Cases](notes/04_BigM_and_Special_Cases.md) | when you can't start at (0, 0); no answer / many answers | Wk 7 | ✅✅ |
| [05 Sensitivity](notes/05_Sensitivity_Shadow_Price_Reduced_Cost.md) | what's one more unit worth? why don't we make X? | Wk 8 | ✅✅✅ |
| [06 Duality](notes/06_Duality.md) | the partner problem whose answer is the shadow prices | Wk 9 | ✅✅ |
| [07 Transportation](notes/07_Transportation.md) | shipping from factories to cities as cheaply as possible | Wk 11 | ✅✅ |
| [08 Game Theory](notes/08_Game_Theory.md) | two opponents choosing at the same time | Wk 12 | ✅✅ |
| [09 Networks](notes/09_Networks.md) | shortest route; connecting everything cheaply | Wk 13 | ✅ |
| [10 Exam Cheat Sheet](notes/10_Cheat_Sheet.md) | every rule, formula and exam sentence in one place | all | for the exam |

Every note follows the same pattern: **the big idea → a worked example step by step → common mistakes → check yourself** (answers hidden until you click).

**Practice exams** (60 marks, 2 hours, every topic):

| Exam | Paper | Solutions |
|---|---|---|
| 1 | [Practice_Exam_1.md](practice_exams/Practice_Exam_1.md) | [Practice_Exam_1_Solutions.md](practice_exams/Practice_Exam_1_Solutions.md) |
| 2 | [Practice_Exam_2.md](practice_exams/Practice_Exam_2.md) | [Practice_Exam_2_Solutions.md](practice_exams/Practice_Exam_2_Solutions.md) |
| 3 | [Practice_Exam_3.md](practice_exams/Practice_Exam_3.md) | [Practice_Exam_3_Solutions.md](practice_exams/Practice_Exam_3_Solutions.md) |

**Viewing:** in VS Code press `Cmd+Shift+V`. The pictures are in [`notes/img/`](notes/img/).

---

## 1. Which method? The decision map

Ask these questions in order:

1. **A grid of supplies, demands and costs per route?** → [Transportation](#9-transportation)
2. **Two opponents and a payoff table?** → [Game theory](#10-game-theory)
3. **Points joined by roads, pipes or cables?** → [Networks](#11-networks)
   * route from A to B → shortest path
   * connect everything → minimum spanning tree
4. **Otherwise, it's a plain LP:**
   * **2 variables** → [graphical method](#4-graphical-method)
   * more variables, and (0, 0) is allowed (all `≤`) → [simplex](#5-simplex-method)
   * more variables, and (0, 0) is **not** allowed (`≥` or `=`) → [Big M](#6-big-m-and-the-special-cases), then simplex
   * then the "what if" questions → [shadow prices](#7-shadow-prices-and-reduced-costs), [duality](#8-duality)

### Words in the question → method

| The question says… | Use |
|---|---|
| "maximise / minimise … subject to …", resources | write the LP → graphical / simplex |
| "at least", "minimum requirement", "exactly" | `≥` / `=` constraints → **Big M** |
| "one more unit", "worth", "how much would you pay", "binding" | **shadow price** |
| "not produced", "how much must its profit rise" | **reduced cost** |
| "how much can the profit change before the plan changes" | **profit range** (graphical) |
| "partner problem", "bound", "buyer of your resources", "offer you can't refuse", "prove it's optimal" | **duality** |
| "supply", "demand", "depots", "routes", cost table | **transportation** |
| "opponent", "zero-sum", "payoff", "at the same time" | **game theory** |
| "quickest / shortest route from A to B" | **shortest path** |
| "connect all", "least cable / pipe" | **minimum spanning tree** |

---

## 2. Writing the LP and standard form

→ Full note: [01_Formulation_and_Standard_Form.md](notes/01_Formulation_and_Standard_Form.md)

**Three questions:**
1. **What do I choose?** → the variables (always with units)
2. **What am I making biggest / smallest?** → the objective
3. **What's stopping me?** → the constraints. "at most" → `≤`, "at least" → `≥`, "exactly" → `=`

**Farmer (week 1):**
```
P = ha pineapples, B = ha bananas
max z = 100P + 30B
s.t.   P +  B ≤ 7     land (ha)
     10P + 4B ≤ 40    labour (h)
          10B ≥ 30    café contract (kg)
       P, B ≥ 0
Answer: P = 2.8, B = 3, profit $370 (labour and contract fully used)
```

**Standard form** (needed for simplex): every constraint becomes an `=`, every RHS ≥ 0 (if one is negative, multiply the row by −1 and flip the sign), every variable ≥ 0.
**Minimising?** Maximise z′ = −z instead, and flip the sign back at the end.

---

## 3. Slack, excess and artificial variables

| Constraint | Add | Name | Plain meaning |
|---|---|---|---|
| `≤` limit | **+ s** | slack | how much is **left over** |
| `≥` requirement | **− e** | excess | how much you went **over** the requirement |
| `≥` or `=` | **+ a** | artificial | a **temporary helper** so simplex can start. Not real; must end at 0 |

![Slack and excess](notes/img/slack_excess.png)

* slack / excess = **0** → used up exactly → **binding** (it's what's holding you back)
* slack / excess **> 0** → room to spare → **non-binding** (more of it is worth nothing)

**Which rows need an artificial?** Put all the decision variables at 0. Any row that breaks needs one.

---

## 4. Graphical method

→ Full note: [02_Graphical_Method.md](notes/02_Graphical_Method.md)

1. Draw each constraint line (find where it crosses each axis).
2. Shade the allowed side (test the point (0, 0)). The overlap is the **feasible region**.
3. Find every corner (solve the two lines that meet there).
4. Work out z at each corner and pick the best. (Or slide the profit line outwards until it last touches the region.)

![Graphical method](notes/img/graphical_method.png)

**The best plan is always at a corner.** If the profit line is parallel to an edge, the whole edge ties.

**"How far can a price change before the plan changes?"** The profit line's slope must stay between the slopes of the two binding lines. Slope of ax + by = c is **−a/b**.
Biofuel: −2 ≤ −c₁/2 ≤ −1 ⇒ **2 ≤ c₁ ≤ 4**. Inside that range the plan stays the same; only z changes.

---

## 5. Simplex method

→ Full note: [03_Simplex_Method.md](notes/03_Simplex_Method.md) (full dry run of the co-op problem)

**The idea:** start at a corner and keep stepping to a better neighbouring corner. Stop when no neighbour is better.

**The key fact:** at each corner, some variables are 0 (**non-basic**) and the rest are not (**basic**: the ones in the Basis column). Each step **swaps one**: a zero variable becomes non-zero (**enters**), and a non-zero one becomes zero (**leaves**).

| Step | Rule | Why |
|---|---|---|
| Start | slacks are the basis, so you're at (0, 0) | slack = everything unused |
| Enter | **most negative** number in the z row | biggest gain in z per unit |
| Leave | ratio test: RHS ÷ entering-column number (positive numbers only), **smallest** wins | the first thing to run out stops you |
| Pivot | make the pivot 1, then clear the rest of its column (z row too) | rewrites the table for the new corner |
| Stop | **no negatives** in the z row | no neighbour is better |

![Simplex path](notes/img/simplex_path.png)

**Co-op** (max 3b + 2a, b + a ≤ 8, 3b + a ≤ 12) walks (0, 0) → (4, 0) → (2, 6). Final table:

| Basis | b | a | s₁ | s₂ | RHS |
|---|---|---|---|---|---|
| a | 0 | 1 | 3/2 | −1/2 | 6 |
| b | 1 | 0 | −1/2 | 1/2 | 2 |
| z | 0 | 0 | 3/2 | 1/2 | 18 |

**Reading it:** b = 2, a = 6, z = 18. The slacks aren't in the basis, so rooftops and installer-days are all used. Shadow prices: rooftop **3/2**, installer-day **1/2**.

---

## 6. Big M and the special cases

→ Full note: [04_BigM_and_Special_Cases.md](notes/04_BigM_and_Special_Cases.md) (full dry run of the grain problem)

**Why:** with a `≥` or `=` row, (0, 0) isn't allowed, so simplex has nowhere to start. Add an **artificial** to each broken row as a fake starting point ("how far short we are"), and charge a huge penalty **M** so simplex gets rid of it.

1. Test (0, 0). Every row that breaks gets + aᵢ.
2. Penalty: max → **−Maᵢ** in the objective. Min → **+Maᵢ** (or switch to max z′ = −z and use −Maᵢ).
3. ⚠️ **Clear the M's** from the z row (z row − M × each artificial row) **before** the first pivot.
4. Run simplex. To compare M-expressions, put M = 1000.

![Big M path](notes/img/bigm_path.png)

**The four tells in a final table:**

| Situation | Tell | Meaning |
|---|---|---|
| Infeasible | an artificial is **still in the basis, > 0** | the constraints contradict each other |
| Unbounded | the entering column has **no positive number** | z grows forever; a limit is missing |
| Alternative optima | **0 in the z row under a non-basic variable** | another plan is just as good |
| Normal | none of these | read off the answer |

![Special cases](notes/img/special_cases.png)

---

## 7. Shadow prices and reduced costs

→ Full note: [05_Sensitivity_Shadow_Price_Reduced_Cost.md](notes/05_Sensitivity_Shadow_Price_Reduced_Cost.md)

> **Every number in the final z row = how much z drops if you force that variable up by 1.**

| z-row number under… | Name | Plain meaning |
|---|---|---|
| a basic variable | – | always 0 |
| a non-basic **slack** | **shadow price** | what one more unit of that resource is worth |
| a non-basic **excess** | shadow price **with the sign flipped** (max) | what one more unit of a requirement costs you |
| a non-basic **decision variable** | **reduced cost** | loss per unit if forced in = how much its profit must rise to be worth making |
| a slack in the basis | shadow price **0** | there's spare, so more is worth nothing |

**When in doubt (resource sheet):** shadow price = (new best z) − (old best z) when the RHS goes up by 1.

![Binding vs non-binding](notes/img/shadow_binding_vs_nonbinding.png)

**A shadow price only holds over a range** (while the same constraints stay binding). Bakery: oven-slot shadow price **$3**, valid for **8 to 16** slots. Inside: new z = old z + Δ × shadow price. Outside: re-solve.

![Shadow price range](notes/img/shadow_price_range.png)

**Signs:**

| Problem | Binding constraint | Shadow price |
|---|---|---|
| max | `≤` limit | ≥ 0 (more is good) |
| max | `≥` requirement | ≤ 0 (a tougher requirement hurts) |
| min | `≥` requirement | ≥ 0 (cost goes up) |
| min | `≤` limit | ≤ 0 |
| any | non-binding | 0 |

**Reduced cost** = (resources one unit uses × their shadow prices) − (its profit).
Water works: advanced batch = 1 tank-day × 4 + 3 chemicals × 0 − 3 = **1**.

![Reduced cost](notes/img/reduced_cost.png)

| What changes | Plan | z |
|---|---|---|
| a resource amount (RHS), inside its range | the corner slides; same constraints binding | + shadow price × Δ |
| a profit per unit, inside its range | **stays the same** | + Δ × that variable's value |

---

## 8. Duality

→ Full note: [06_Duality.md](notes/06_Duality.md)

**The meaning:** the original problem asks "what should I make?". The dual asks "**what is each of my resources worth?**" (y = value per unit). A value is fair only if, for every product, the resources it uses are worth at least what that product earns. **The lowest fair total value = your best profit**, because profit is just resources turned into money. The y's are the shadow prices.

```
ORIGINAL                              DUAL
max 5x₁ + 4x₂                         min 10y₁ + 14y₂
s.t. 2x₁ +  x₂ ≤ 10   (y₁)            s.t. 2y₁ +  y₂ ≥ 5   (from x₁'s column)
      x₁ + 2x₂ ≤ 14   (y₂)                  y₁ + 2y₂ ≥ 4   (from x₂'s column)
answer (2, 6), z = 34                 answer (2, 1), w = 34
```

**Recipe:** one y per constraint; one dual constraint per variable (read **down** its column); RHS ↔ profits; max ↔ min; `≤` ↔ `≥`.

![Duality bounds](notes/img/duality_bounds.png)

* **Weak duality:** any real profit ≤ any allowed w (every w is a ceiling).
* **Strong duality:** best z = best w. If you find a z and a w that are equal, both are optimal.
* **The y's are the shadow prices.**
* **Complementary slackness:** spare resource ⇒ its y = 0. Product not made ⇒ its dual constraint has a gap equal to its reduced cost.

---

## 9. Transportation

→ Full note: [07_Transportation.md](notes/07_Transportation.md) (full Powerco dry run)

1. **Balance:** total supply = total demand? If not, add a dummy row or column with cost 0.
2. **Start:** northwest corner. Fill from the top-left with min(supply left, demand left). Check for **m + n − 1** filled cells.
3. **Prices:** u₁ = 0, then **u + v = cost** on every **filled** cell.
4. **Savings:** **c̄ = cost − u − v** on every **empty** cell. All ≥ 0 → optimal.
5. **Improve:** the most negative c̄ enters. Draw the **+ − + − loop** through filled cells. θ = smallest "−" amount. Move θ around the loop. New cost = old + θ × c̄. Go to step 3.

![Transportation loop](notes/img/transport_loop.png)

Powerco: 1180 → 1120 → 1070 → **1020** (optimal).

---

## 10. Game theory

→ Full note: [08_Game_Theory.md](notes/08_Game_Theory.md)

**Row player wants BIG numbers; column player wants SMALL numbers.**

1. **Delete dominated choices:** a row that's ≤ another row everywhere; a column that's ≥ another column everywhere (opposite direction for columns).
2. **Saddle point test:** maximin (best of the row minimums) vs minimax (best of the column maximums). **Equal** → each player picks one choice every time; that number is the value.
3. **Not equal** → randomise. Row player's LP:

```
max v
s.t. (each opponent column's numbers × my probabilities) ≥ v
     probabilities add to 1, all ≥ 0
```

![Mixed strategy](notes/img/game_mixed.png)

**2×2 shortcut:** set the two averages equal. Cafe game: x = (5/8, 3/8), **v = 3.5**.

---

## 11. Networks

→ Full note: [09_Networks.md](notes/09_Networks.md)

![Networks](notes/img/networks.png)

| | **Shortest path** | **Minimum spanning tree** |
|---|---|---|
| Question | quickest route A → B | connect **every** node with the least total |
| Method | spread out from the start; each round, lock in the unfinished node with the smallest total distance, then update its neighbours | each round, add the cheapest edge that reaches a **new** node |
| Seervada | O–B–E–T = **14** | 6 edges, total **22** |
| Output | one route (trace back through "via") | n − 1 edges, no loops |

---

## 12. Glossary in plain words

| Term | Plain meaning |
|---|---|
| Decision variable | something you choose (how much to make, ship, plant) |
| Objective | what you're making biggest or smallest (profit, cost) |
| Constraint | a limit or requirement |
| Feasible | allowed by every constraint |
| Feasible region | all the allowed plans (the shaded shape) |
| Optimal | the best allowed plan |
| RHS | right-hand side: the number after `≤`, `≥` or `=` |
| Binding | used up exactly at the best plan (slack/excess = 0) |
| Non-binding | some to spare at the best plan |
| Slack (s) | unused amount of a `≤` resource |
| Excess / surplus (e) | amount over a `≥` requirement |
| Artificial (a) | temporary helper to start simplex; must end at 0 |
| Basic variable | listed in the Basis column; its value is in the RHS |
| Non-basic variable | not in the Basis column; it's 0 |
| Basic feasible solution (BFS) | a corner of the region |
| Pivot column / row / element | entering variable / leaving row / the number where they meet |
| Ratio test | RHS ÷ positive entering-column number; the smallest says who leaves |
| Shadow price | change in best z per +1 of a resource (= the dual variable) |
| Reduced cost | loss per unit if you force in a product you're not making |
| Opportunity cost | what you give up by not using something on the next best option |
| Range (allowable increase/decrease) | how far a number can move before the answer changes |
| Dual | the partner LP; its answer = the shadow prices; best values are equal |
| Complementary slackness | spare resource ⇔ zero price; product not made ⇔ gap in its dual constraint |
| Balanced | total supply = total demand |
| Dummy | an extra zero-cost row or column added to balance |
| Zero-sum | one player's gain = the other's loss |
| Saddle point | a cell that's the smallest in its row and the biggest in its column |
| Mixed strategy | picking choices at random with set probabilities |
| Value of the game (v) | the average payoff guaranteed with best play |
| MST | minimum spanning tree: n − 1 edges connecting every node at least total cost |

---

## 13. Mistakes that lose marks

1. **Not clearing M** from the z row in Big M, then calling the table optimal too early.
2. **Ratio test on a 0 or negative number.** Skip those rows.
3. **Picking the most negative from the RHS** instead of the variable columns.
4. **Reading a shadow price under a basic slack.** That constraint has spare, so its shadow price is 0.
5. **Wrong sign for a `≥` shadow price.** For a max it's ≤ 0. If unsure, re-solve with RHS + 1.
6. **Using a shadow price outside its range.** Re-solve instead.
7. **Wrong dominance direction for columns.** The column player wants **small** numbers.
8. **Not checking m + n − 1** filled cells in transportation.
9. **Loop corners on empty cells.** Apart from the entering cell, every corner must be a filled cell.
10. **MST vs shortest path mix-up.** Read the question: route or connect-all?
11. **Not explaining the answer in words.** Always finish with a sentence using the problem's units.
12. **Negative RHS left in standard form.** Multiply by −1 and flip the sign.

---

## 14. Exam-day checklist

- [ ] For each question, **name the kind of problem first**: "This is a … problem because …"
- [ ] Define every variable **with units**
- [ ] Standard form: slack (`≤`), excess + artificial (`≥`), artificial (`=`), every RHS ≥ 0
- [ ] Before simplex: is (0, 0) allowed? If not, Big M, and **clear the M's**
- [ ] At each pivot, show **who enters, who leaves**, and the **row operations**
- [ ] After each pivot, check every RHS is ≥ 0
- [ ] At the end, check for the tells (stuck artificial, no positive number, 0 under a non-basic)
- [ ] Sensitivity: name the binding constraints, give the shadow prices, mention the range
- [ ] Dual: one y per constraint, one constraint per variable, max ↔ min, `≤` ↔ `≥`, check z = w
- [ ] Transportation: balanced? m + n − 1 cells? u₁ = 0, c̄ on every empty cell, θ from the "−" cells
- [ ] Games: dominance → maximin/minimax → saddle point or LP
- [ ] Networks: right method, a table of steps, the route/tree **and its total**
- [ ] **Final answer in words**

---

## 15. Revision plan

| Session | Do this | Practice from |
|---|---|---|
| 1 | Notes 01–02. Redo the farmer and biofuel problems by hand | Wk 1–3 pracs |
| 2 | Note 03. Redo the co-op dry run without looking, then revision prac Q5 | Revision prac Q5, Q7 |
| 3 | Note 04. Redo the grain problem; match each tell to its special case | Wk 6 prac, revision Q4, Q6, Q8, Q9 |
| 4 | **Note 05.** For each final table, say what every z-row number means; find one shadow price by re-solving; find one range | Wk 8 prac (bakery, Part E) |
| 5 | Note 06. Write the dual of 3 problems; check z = w | Wk 9 prac, revision Q2, Q10 |
| 6 | Notes 07–09 | Revision prac 2 (all) |
| 7 | **Mixed practice:** take random questions and name the kind of problem before solving | PST questions, both revision pracs |
| 8 | **Timed:** Practice Exam 1 (2 h), then mark it with the solutions | [practice_exams/](practice_exams/) |
| 9 | Revisit weak topics, then Practice Exam 2 (2 h) | [practice_exams/](practice_exams/) |

> *"You came in able to solve equations. You leave able to model a decision."* (week 13 revision lecture)
>
> Good luck! 🍀
