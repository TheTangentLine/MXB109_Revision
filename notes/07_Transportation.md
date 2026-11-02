# 7. Transportation Problems

> **In one sentence:** ship goods from sources (with **supply**) to destinations (with **demand**) as cheaply as possible. Start with any plan, check whether an unused route would save money, move goods onto it around a loop, and repeat until no route saves money.

---

## 7.1 The big idea

Factories have **supply**, cities have **demand**, and each route has a **cost per unit**. Decide how much to send on each route so every factory sends out its supply and every city gets its demand, for the **least total cost**.

**The five steps:**

1. **Balance it:** total supply must equal total demand.
2. **Get a starting plan:** the northwest corner rule.
3. **Check it:** for each unused route, would using it save money? (That number is called **c̄**.)
4. **Improve it:** if a route saves money, move as many units as possible onto it, around a loop. Then go back to step 3.
5. **Stop** when no unused route saves money.

It's simplex on a grid:

| Simplex (note 3) | Transportation |
|---|---|
| start at a corner | start with the northwest corner plan |
| z row: is a neighbour better? | **c̄** on each unused route: would it save money? |
| most negative → enters | most negative c̄ → that route **enters** |
| ratio test: first to hit 0 leaves | **θ** = smallest "−" cell on the loop; that cell **leaves** |
| pivot | move θ units around the loop |
| stop: no negatives | stop: every c̄ ≥ 0 |

### How to read the grids in this note

So you never have to scroll back up, **every grid shows everything you need**:

| You'll see | Meaning |
|---|---|
| `$3 → 50` | this route costs **$3 per unit**, and we send **50** units on it |
| `$5 → –` | this route costs $5 per unit, and it's **unused** |
| `c̄ −3` | in an unused cell: using this route would change the total cost by **−3 per unit** |
| **(+)** / **(−)** | this cell is on the loop: it gains / loses units |
| `u₁ = 0`, `v₁ = 3` | the row and column numbers used to work out c̄ (step 3) |

---

## 7.2 Small example, step by step (revision 2 Q9)

### Step 1: balance it

|  | Z1 | Z2 | Z3 | Supply |
|---|---|---|---|---|
| R1 | $3 | $6 | $5 | 70 |
| R2 | $7 | $4 | $6 | 80 |
| **Demand** | 50 | 40 | 60 | |

Supply 70 + 80 = 150. Demand 50 + 40 + 60 = 150. **Balanced** ✓.
(If not, add a dummy row or column with $0 on every route. See section 7.4.)

---

### Step 2: starting plan (northwest corner)

Start in the **top-left** cell and send as much as you can: **min(supply left, demand left)**. Whichever runs out, move **right** (if the row still has supply) or **down** (if the row is finished).

| Move | Cell | Send | What runs out |
|---|---|---|---|
| 1 | R1, Z1 | min(70, 50) = **50** | Z1 is full. R1 has 20 left. Move **right** |
| 2 | R1, Z2 | min(20, 40) = **20** | R1 is empty. Z2 still needs 20. Move **down** |
| 3 | R2, Z2 | min(80, 20) = **20** | Z2 is full. R2 has 60 left. Move **right** |
| 4 | R2, Z3 | min(60, 60) = **60** | both. Done |

**Starting plan:**

|  | Z1 | Z2 | Z3 | Sent |
|---|---|---|---|---|
| R1 | $3 → **50** | $6 → **20** | $5 → – | 70 ✓ |
| R2 | $7 → – | $4 → **20** | $6 → **60** | 80 ✓ |
| **Received** | 50 ✓ | 40 ✓ | 60 ✓ | |

**Cost** = 3×50 + 6×20 + 4×20 + 6×60 = 150 + 120 + 80 + 360 = **710**
**Check:** used cells should be m + n − 1 = 2 + 3 − 1 = **4** ✓

The northwest corner rule ignores cost completely, so this is only a starting point.

---

### Step 3: would an unused route save money?

Two routes are unused: **R1→Z3** and **R2→Z1**.

#### "Just try it" breaks the totals

Send 1 unit on R1→Z3. Now R1 sends 71 (it only has 70) and Z3 receives 61 (it only needs 60). So every unit you add somewhere has to be taken away somewhere else, and so on, until all the totals are right again.

#### Do it by hand for R1→Z3

|  | Z1 | Z2 | Z3 |
|---|---|---|---|
| R1 | $3 → 50 | $6 → 20 **(−)** | $5 → – **(+)** |
| R2 | $7 → – | $4 → 20 **(+)** | $6 → 60 **(−)** |

| Change | Why | Cost |
|---|---|---|
| **+1** on R1→Z3 | try the new route | +5 |
| **−1** on R2→Z3 | Z3 now gets too much, so take 1 off its other route | −6 |
| **+1** on R2→Z2 | R2 now sends too little, so add 1 to its other route | +4 |
| **−1** on R1→Z2 | Z2 now gets too much, so take 1 off its other route | −6 |

Every row and column now has one + and one −, so all the totals are right again.
**Net change: 5 − 6 + 4 − 6 = −3.** Each unit sent this way **saves $3**. ✅

#### Do it by hand for R2→Z1

|  | Z1 | Z2 | Z3 |
|---|---|---|---|
| R1 | $3 → 50 **(−)** | $6 → 20 **(+)** | $5 → – |
| R2 | $7 → – **(+)** | $4 → 20 **(−)** | $6 → 60 |

| Change | Why | Cost |
|---|---|---|
| **+1** on R2→Z1 | try it | +7 |
| **−1** on R1→Z1 | Z1 gets too much | −3 |
| **+1** on R1→Z2 | R1 sends too little | +6 |
| **−1** on R2→Z2 | Z2 gets too much | −4 |

**Net change: 7 − 3 + 6 − 4 = +6.** It would **cost $6 more** per unit. ❌

> **c̄ = the change in total cost per unit if you start using an unused route** (after fixing all the totals).
> Negative = saves money. All ≥ 0 = nothing saves money, so the plan is **optimal**.

#### The shortcut: u and v

Drawing a loop for **every** unused cell gets slow on a big grid. u (one per row) and v (one per column) give the same c̄ with no loops.

**Rule:** on every **used** cell, **u + v = its cost**. Start with **u₁ = 0**. Then each time, pick a used cell where only one of u or v is still unknown:

| Used cell | Its cost | Equation | Gives |
|---|---|---|---|
| R1, Z1 | $3 | 0 + v₁ = 3 | v₁ = 3 |
| R1, Z2 | $6 | 0 + v₂ = 6 | v₂ = 6 |
| R2, Z2 | $4 | u₂ + 6 = 4 | u₂ = −2 |
| R2, Z3 | $6 | −2 + v₃ = 6 | v₃ = 8 |

Then for each **unused** cell: **c̄ = cost − u − v**. Everything is on one grid:

|  | Z1 (v₁ = 3) | Z2 (v₂ = 6) | Z3 (v₃ = 8) |
|---|---|---|---|
| **R1 (u₁ = 0)** | $3 → **50** | $6 → **20** | $5 → – &nbsp; c̄ = 5 − 0 − 8 = **−3** |
| **R2 (u₂ = −2)** | $7 → – &nbsp; c̄ = 7 + 2 − 3 = **+6** | $4 → **20** | $6 → **60** |

**Reading it:** the same −3 and +6 as the loops by hand ✓. R1→Z3 saves money, so it **enters**.

* **What u + v means:** think of it as what the current plan "thinks" that route is worth. If the real cost is lower, the route is a bargain and c̄ is negative.
* **Why u₁ = 0?** There's one more unknown than there are equations, so you get to fix one. Any starting value gives the same c̄. (u and v can be negative. That's fine.)

---

### Step 4: move goods around the loop

The loop for R1→Z3, from step 3:

|  | Z1 | Z2 | Z3 |
|---|---|---|---|
| R1 | $3 → 50 | $6 → 20 **(−)** | $5 → – **(+)** |
| R2 | $7 → – | $4 → 20 **(+)** | $6 → 60 **(−)** |

Each unit moved around this loop saves $3, so move **as many as possible**.

#### θ: how many can we move?

Every **(−)** cell **loses** units, and no cell can go below 0:
* R1Z2 has **20**, so it can lose at most 20
* R2Z3 has **60**, so it can lose at most 60

**θ = the smallest (−) cell = 20.** Same idea as the ratio test: stop when the first thing hits 0.

#### Move 20: add to the (+) cells, take from the (−) cells

|  | Z1 | Z2 | Z3 | Sent |
|---|---|---|---|---|
| R1 | $3 → **50** | $6 → ~~20~~ **0** ← leaves | $5 → **20** (0 + 20) | 70 ✓ |
| R2 | $7 → – | $4 → **40** (20 + 20) | $6 → **40** (60 − 20) | 80 ✓ |
| **Received** | 50 ✓ | 40 ✓ | 60 ✓ | |

**New cost** = old cost + θ × c̄ = 710 + 20 × (−3) = **650**
Check: 3×50 + 5×20 + 4×40 + 6×40 = 150 + 100 + 160 + 240 = 650 ✓

---

### Back to step 3: check the new plan

u, v from the used cells: u₁ = 0 → v₁ = 3 (R1Z1, $3) and v₃ = 5 (R1Z3, $5) → u₂ = 6 − 5 = 1 (R2Z3, $6) → v₂ = 4 − 1 = 3 (R2Z2, $4).

|  | Z1 (v₁ = 3) | Z2 (v₂ = 3) | Z3 (v₃ = 5) |
|---|---|---|---|
| **R1 (u₁ = 0)** | $3 → **50** | $6 → – &nbsp; c̄ = 6 − 0 − 3 = **+3** | $5 → **20** |
| **R2 (u₂ = 1)** | $7 → – &nbsp; c̄ = 7 − 1 − 3 = **+3** | $4 → **40** | $6 → **40** |

**Reading it:** both c̄ are positive, so no unused route saves money. **Optimal.**

**Answer in words:** R1 sends 50 to Z1 and 20 to Z3. R2 sends 40 to Z2 and 40 to Z3. **Total cost $650.**

### The loop rules, and why

| Rule | Why |
|---|---|
| Signs alternate + − + − | every + in a row or column is cancelled by a − in that same row or column, so the totals stay right |
| Apart from the new cell, every corner must be a **used** cell | you can only take units away from a route that has some |
| Move only along rows and columns, turning at used cells | each turn fixes one row total or one column total |
| It starts and ends at the new cell | it's a closed loop, so everything balances |

![Transportation prices, reduced costs, loop](img/transport_loop.png)

---

## 7.3 Bigger example: Powerco (lecture), same steps

Each round shows **one grid with everything on it**: costs, amounts, u, v, c̄, and the loop.

### Step 1 and 2: balance and northwest corner

|  | C1 | C2 | C3 | C4 | Supply |
|---|---|---|---|---|---|
| P1 | $8 | $6 | $10 | $9 | 35 |
| P2 | $9 | $12 | $13 | $7 | 50 |
| P3 | $14 | $9 | $16 | $5 | 40 |
| **Demand** | 45 | 20 | 30 | 30 | 125 = 125 ✓ |

| Move | Cell | Send | What runs out |
|---|---|---|---|
| 1 | P1, C1 | min(35, 45) = **35** | P1. Move down |
| 2 | P2, C1 | min(50, 10) = **10** | C1. Move right |
| 3 | P2, C2 | min(40, 20) = **20** | C2. Move right |
| 4 | P2, C3 | min(20, 30) = **20** | P2. Move down |
| 5 | P3, C3 | min(40, 10) = **10** | C3. Move right |
| 6 | P3, C4 | min(30, 30) = **30** | both. Done |

6 used cells = 3 + 4 − 1 ✓. Cost = 8×35 + 9×10 + 12×20 + 13×20 + 16×10 + 5×30 = **1180**.

---

### Round 1 (cost 1180)

**u, v** (u + v = cost on used cells): u₁ = 0 → v₁ = 8 → u₂ = 9 − 8 = 1 → v₂ = 12 − 1 = 11, v₃ = 13 − 1 = 12 → u₃ = 16 − 12 = 4 → v₄ = 5 − 4 = 1

|  | C1 (v = 8) | C2 (v = 11) | C3 (v = 12) | C4 (v = 1) |
|---|---|---|---|---|
| **P1 (u = 0)** | $8 → **35** | $6 → – &nbsp; c̄ −5 | $10 → – &nbsp; c̄ −2 | $9 → – &nbsp; c̄ +8 |
| **P2 (u = 1)** | $9 → **10** | $12 → **20** **(−)** | $13 → **20** **(+)** | $7 → – &nbsp; c̄ +5 |
| **P3 (u = 4)** | $14 → – &nbsp; c̄ +2 | $9 → – &nbsp; c̄ **−6** **(+)** | $16 → **10** **(−)** | $5 → **30** |

**Reading it:**
* Most negative c̄ is **−6** at P3→C2, so it **enters**.
* Loop: + P3C2 → − P2C2 (same column) → + P2C3 (same row) → − P3C3 (same column, back to row P3).
* Check by hand: +9 − 12 + 13 − 16 = **−6** ✓
* (−) cells hold 20 and 10, so **θ = 10**. P3C3 leaves.
* New cost = 1180 + 10 × (−6) = **1120**

---

### Round 2 (cost 1120)

**u, v:** u₁ = 0 → v₁ = 8 → u₂ = 1 → v₂ = 11, v₃ = 12 → u₃ = 9 − 11 = −2 → v₄ = 5 + 2 = 7

|  | C1 (v = 8) | C2 (v = 11) | C3 (v = 12) | C4 (v = 7) |
|---|---|---|---|---|
| **P1 (u = 0)** | $8 → **35** **(−)** | $6 → – &nbsp; c̄ **−5** **(+)** | $10 → – &nbsp; c̄ −2 | $9 → – &nbsp; c̄ +2 |
| **P2 (u = 1)** | $9 → **10** **(+)** | $12 → **10** **(−)** | $13 → **30** | $7 → – &nbsp; c̄ −1 |
| **P3 (u = −2)** | $14 → – &nbsp; c̄ +8 | $9 → **10** | $16 → – &nbsp; c̄ +6 | $5 → **30** |

**Reading it:**
* Most negative is **−5** at P1→C2, so it **enters**.
* Loop: + P1C2 → − P2C2 → + P2C1 → − P1C1. Check: 6 − 12 + 9 − 8 = **−5** ✓
* (−) cells hold 10 and 35, so **θ = 10**. P2C2 leaves.
* New cost = 1120 + 10 × (−5) = **1070**

---

### Round 3 (cost 1070)

**u, v:** u₁ = 0 → v₁ = 8, v₂ = 6 → u₂ = 9 − 8 = 1 → v₃ = 13 − 1 = 12 → u₃ = 9 − 6 = 3 → v₄ = 5 − 3 = 2

|  | C1 (v = 8) | C2 (v = 6) | C3 (v = 12) | C4 (v = 2) |
|---|---|---|---|---|
| **P1 (u = 0)** | $8 → **25** **(−)** | $6 → **10** | $10 → – &nbsp; c̄ **−2** **(+)** | $9 → – &nbsp; c̄ +7 |
| **P2 (u = 1)** | $9 → **20** **(+)** | $12 → – &nbsp; c̄ +5 | $13 → **30** **(−)** | $7 → – &nbsp; c̄ +4 |
| **P3 (u = 3)** | $14 → – &nbsp; c̄ +3 | $9 → **10** | $16 → – &nbsp; c̄ +1 | $5 → **30** |

**Reading it:**
* The only negative is **−2** at P1→C3, so it **enters**.
* Loop: + P1C3 → − P2C3 → + P2C1 → − P1C1. Check: 10 − 13 + 9 − 8 = **−2** ✓
* (−) cells hold 30 and 25, so **θ = 25**. P1C1 leaves.
* New cost = 1070 + 25 × (−2) = **1020**

---

### Round 4 (cost 1020): check

**u, v:** u₁ = 0 → v₂ = 6, v₃ = 10 → u₂ = 13 − 10 = 3 → v₁ = 9 − 3 = 6 → u₃ = 9 − 6 = 3 → v₄ = 5 − 3 = 2

|  | C1 (v = 6) | C2 (v = 6) | C3 (v = 10) | C4 (v = 2) |
|---|---|---|---|---|
| **P1 (u = 0)** | $8 → – &nbsp; c̄ +2 | $6 → **10** | $10 → **25** | $9 → – &nbsp; c̄ +7 |
| **P2 (u = 3)** | $9 → **45** | $12 → – &nbsp; c̄ +3 | $13 → **5** | $7 → – &nbsp; c̄ +2 |
| **P3 (u = 3)** | $14 → – &nbsp; c̄ +5 | $9 → **10** | $16 → – &nbsp; c̄ +3 | $5 → **30** |

**Reading it:** every c̄ is positive, so no route saves money. **Optimal.** ✓

**Answer in words:** P1 sends 10 to C2 and 25 to C3. P2 sends 45 to C1 and 5 to C3. P3 sends 10 to C2 and 30 to C4. **Total cost $1020** (down from 1180).

| Round | Entering cell | θ | Cost |
|---|---|---|---|
| start | – | – | 1180 |
| 1 | P3, C2 (−6) | 10 | 1120 |
| 2 | P1, C2 (−5) | 10 | 1070 |
| 3 | P1, C3 (−2) | 25 | **1020** |

---

## 7.4 Other exam questions

### Unbalanced (revision 2 Q6)

Supply 60 + 70 + 80 = 210, demand 50 + 80 = 130. Add a **dummy city** with demand 210 − 130 = **80** and $0 on every route. Whatever goes to the dummy is just left at the factory.
(If demand > supply, add a **dummy factory** instead. What it "sends" is demand that doesn't get met.)

### "Is this plan optimal?" (revision 2 Q7)

1. Check it has m + n − 1 used cells.
2. Work out u and v from the used cells.
3. Work out c̄ on every unused cell. All ≥ 0 means optimal.
4. A **c̄ = 0** on an unused cell means there's **another plan with the same cost** (alternative optimum): moving goods onto it changes the cost by 0.

### Where u and v come from (link to notes 5–6)

u and v are the **shadow prices** (dual values) of each factory and city. c̄ is the **reduced cost** of each unused route: how much the total cost changes per unit if you force it in. It's the same idea as the z row in simplex.

---

## Common mistakes

1. Forgetting to balance first.
2. Not having m + n − 1 used cells.
3. Working out u and v from **unused** cells. Only use **used** cells.
4. A loop corner on an unused cell (other than the new one).
5. Taking θ from a "(+)" cell. θ is the smallest amount on a **"(−)"** cell.

**Exam tip:** draw your grid the way this note does, with the cost and amount in each cell and u and v around the edges. Then you never have to flip back to the cost table.

---

## Check yourself

<details><summary>1. In Powerco's Round 1 grid, check c̄ for P1→C2 = −5 by drawing the loop by hand.</summary>

Loop: **+** P1C2 ($6), **−** P2C2 ($12) (same column), **+** P2C1 ($9) (same row), **−** P1C1 ($8) (same column, back to row P1).
6 − 12 + 9 − 8 = **−5** ✓
</details>

<details><summary>2. After the u, v step, every c̄ is positive except one, which is 0. Is the plan optimal? What does the 0 mean?</summary>

**Yes, optimal**: no route saves money. The 0 means using that route changes the cost by 0, so there's **another plan with the same cost** (alternative optimum).
</details>

<details><summary>3. Supply 40, 50. Demand 30, 30, 20. What do you add before starting?</summary>

Supply 90, demand 80. Add a **dummy city** with demand **10** and $0 on both routes.
</details>
