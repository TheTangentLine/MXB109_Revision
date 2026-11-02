# 6. Duality

> **In one sentence:** the original problem asks "what should I make?". The dual asks "what is each of my resources worth?". Both give the **same total**, because profit is just your resources turned into money.

---

## 6.1 The big idea: two questions about the same business

**Smoothie bar:**
```
x₁ = smoothie type 1, x₂ = smoothie type 2

max profit = 5x₁ + 4x₂
s.t. 2x₁ +  x₂ ≤ 10     fruit (units)
      x₁ + 2x₂ ≤ 14     blender-minutes
```

**Question 1 (the original problem): "What should I make?"**
→ 2 of smoothie 1 and 6 of smoothie 2, for a profit of **$34**.

**Question 2 (the dual): "What is each of my resources actually worth?"**
→ fruit is worth **$2** a unit and blender-minutes **$1** each.
Add up what you own at those values: 10 fruit × $2 + 14 minutes × $1 = **$34**.

⭐ **The two answers are equal.** That's the main thing duality tells you. Your profit doesn't come from nowhere: it's what your resources are worth once you use them well. "Best profit" and "total value of your resources" are two ways of measuring the same thing.

> The dual's variables (y₁ = value of fruit, y₂ = value of a blender-minute) are the **shadow prices** from note 5.
> So the dual is really **the problem of working out the shadow prices**.

---

## 6.2 What makes a value "fair"? (the dual constraints)

Suppose someone puts a value on each resource: y₁ per unit of fruit and y₂ per blender-minute. That value is only **fair** if it doesn't undervalue anything:

> For **every** product, the resources it uses must be valued at **least** as much as that product earns.

If a value breaks this rule, you'd say: "I can turn those resources into more money than that myself."

* Smoothie 1 uses 2 fruit + 1 minute and earns $5 → need **2y₁ + y₂ ≥ 5**
* Smoothie 2 uses 1 fruit + 2 minutes and earns $4 → need **y₁ + 2y₂ ≥ 4**

Try three different values:

| Values (y₁, y₂) | Smoothie 1: 2y₁ + y₂ vs $5 | Smoothie 2: y₁ + 2y₂ vs $4 | Total value 10y₁ + 14y₂ | Verdict |
|---|---|---|---|---|
| (1, 1) | 3 < 5 ❌ | 3 < 4 ❌ | 24 | **Too low.** Undervalued: you'd rather make smoothies |
| (3, 1) | 7 ≥ 5 ✓ | 5 ≥ 4 ✓ | 44 | **Fair but generous.** Overvalued: nobody could actually make $44 from these resources |
| **(2, 1)** | 5 ≥ 5 ✓ | 4 ≥ 4 ✓ | **34** | **Just right.** The lowest fair value, and it equals the best profit |

**That's the dual problem:**
```
min w = 10y₁ + 14y₂          total value of everything you own
s.t. 2y₁ +  y₂ ≥ 5           fair to smoothie 1
      y₁ + 2y₂ ≥ 4           fair to smoothie 2
      y₁, y₂ ≥ 0
```

**Why min?** Push the values down as far as they can go while staying fair. They stop at 34: any lower and some smoothie would be worth more to make than its resources are valued at.

**Reading the last row:** at the right values, both smoothies are worth **exactly** what their resources are valued at (5 = 5 and 4 = 4). They're both "break-even" at these values, and that's why both are in the best plan.

---

## 6.3 Where 10y₁ + 14y₂ comes from

**10 and 14 are the RHS numbers**, the amounts of each resource you have:
* 10 units of fruit at y₁ each = **10y₁**
* 14 blender-minutes at y₂ each = **14y₂**

Like buying 10 apples at $2 and 14 oranges at $1: 10 × 2 + 14 × 1 = $34.

### The same thing in maths: add up the constraints

Multiply each constraint by its value and add them. With y₁ = 2 and y₂ = 1:

```
2 × (2x₁ +  x₂ ≤ 10)   →   4x₁ + 2x₂ ≤ 20
1 × ( x₁ + 2x₂ ≤ 14)   →    x₁ + 2x₂ ≤ 14
                           ─────────────────
                    add:   5x₁ + 4x₂ ≤ 34
```

The left side, **5x₁ + 4x₂, is exactly the profit**. So **the profit can never be more than 34**, whatever plan you pick.

The right side came out as 10 × 2 + 14 × 1. With general values it's **10y₁ + 14y₂**.

So every fair value gives a **ceiling** on the profit. The dual looks for the **lowest ceiling**, and the lowest ceiling touches the real best profit exactly.

**Why the dual constraints are needed here:** adding up only gives a ceiling on the profit if the left side **covers** the profit, i.e. at least 5 in front of x₁ and at least 4 in front of x₂. That's 2y₁ + y₂ ≥ 5 and y₁ + 2y₂ ≥ 4: the same "fair value" rule as section 6.2.

![Weak and strong duality](img/duality_bounds.png)

**Reading the picture:** every profit you can actually reach sits **below** every ceiling. The highest profit and the lowest ceiling meet at 34.

---

## 6.4 The buyer story (the same idea in a costume)

Lectures often tell it like this: a competitor wants to **buy all your resources**. y₁ and y₂ are the prices they offer.
* They want to pay as **little** as possible → **min** 10y₁ + 14y₂
* You'll only sell if, for every product, the resources it uses are paid at least what that product earns → the **≥ constraints**

**The cheapest offer you can't refuse = your best profit.** It's sections 6.1–6.2 again: the offer is a fair value for each resource.

---

## 6.5 Writing the dual: step by step

Start from a **max problem with `≤` constraints**:
```
max z = 5x₁ + 4x₂
s.t. 2x₁ +  x₂ ≤ 10     ← give this row y₁
      x₁ + 2x₂ ≤ 14     ← give this row y₂
      x₁, x₂ ≥ 0
```

**Step 1: one dual variable per constraint** (one value per resource). Two constraints, so y₁ and y₂.

**Step 2: the dual objective = RHS × values.** min w = **10**y₁ + **14**y₂.

**Step 3: one dual constraint per product. Read DOWN that product's column** (what it uses), ≥ its profit.

| Product | What it uses (its column) | Its profit | Dual constraint |
|---|---|---|---|
| x₁ | 2 fruit, 1 minute | 5 | **2**y₁ + **1**y₂ ≥ **5** |
| x₂ | 1 fruit, 2 minutes | 4 | **1**y₁ + **2**y₂ ≥ **4** |

**Step 4: flip.** max → min, `≤` → `≥`, and y ≥ 0.

### The swap table

| Original (max) | Dual (min) |
|---|---|
| max profit | min total value |
| each constraint (resource) | a dual variable y (its value) |
| each variable x (product) | a dual constraint (fair to that product) |
| RHS numbers (amounts you have) | dual objective numbers |
| profit numbers | dual RHS numbers |
| rows of numbers | become columns |
| m constraints, n variables | n constraints, m variables |

### Example with three products (week 9 prac Q3)

```
max 3x₁ + 4x₂ + 2x₃
s.t. x₁ + 2x₂ + x₃ ≤ 14    (y₁)
    2x₁ +  x₂ + x₃ ≤ 10    (y₂)
```
* 2 resources → 2 values y₁, y₂
* 3 products → 3 "fair" constraints, reading down each column:
  * x₁ uses (1, 2), earns 3 → y₁ + 2y₂ ≥ 3
  * x₂ uses (2, 1), earns 4 → 2y₁ + y₂ ≥ 4
  * x₃ uses (1, 1), earns 2 → y₁ + y₂ ≥ 2

**Dual: min 14y₁ + 10y₂ s.t. y₁ + 2y₂ ≥ 3, 2y₁ + y₂ ≥ 4, y₁ + y₂ ≥ 2, y ≥ 0.**

---

## 6.6 Weak and strong duality

| Name | What it says | In plain words |
|---|---|---|
| **Weak duality** | any allowed z ≤ any allowed w | you can't make more money than your resources are worth at any fair value |
| **Strong duality** | best z = best w | at the right values, profit = total value of your resources |

### Why you'd use them

* **Proving an answer is optimal (revision Q10, "two analysts"):** someone gives you a plan with z = 34, and someone else gives you fair values with w = 34. A profit can't beat a ceiling, so 34 can't be beaten. **Both are optimal**, and you don't have to check anyone's working.
* **Quick ceiling:** any fair values give an instant upper limit on the profit, without solving anything.

---

## 6.7 Dual values = shadow prices

Increase fruit from 10 to 11. The total value 10y₁ + 14y₂ goes up by exactly y₁ = **2**. Best profit = best total value, so the profit also goes up by 2. That's the definition of the **shadow price of fruit**.

> Note 5 read shadow prices off the final table. **The dual gives them directly.**
> They also appear in the original problem's **final z row, under the slack columns**. Solve one problem and you have the answer to both.

### It works for the farmer too

Farmer (note 1): best profit $370. Shadow prices from note 5: land **$0**, labour **$10**, contract **−$1** (a requirement is a burden, so its value is negative). Value everything the farmer has:
```
7 ha × $0  +  40 hours × $10  +  30 kg × (−$1)  =  0 + 400 − 30  =  $370   ✓
```
Total value of the resources = best profit, as strong duality says.

---

## 6.8 Complementary slackness: why the rules make sense

| Fact | ⇔ | Why it makes sense |
|---|---|---|
| a resource has **spare** (slack > 0) | its value **y = 0** | if you already have leftover fruit, one more unit is worth nothing to you |
| a product is **not made** (x = 0) | its resources are worth **more** than its profit (a gap in its dual constraint = its **reduced cost**) | it isn't worth making, because its resources earn more elsewhere |
| a resource has value y > 0 | it's fully used (binding) | it's only valuable because you're short of it |
| a product **is** made (x > 0) | its resources are worth **exactly** its profit | it's break-even at these values |

### Example

```
max 4x₁ + 2x₂
s.t. x₁ +  x₂ ≤ 6
     x₁ + 2x₂ ≤ 8
→ best x = (6, 0), z = 24
```
* **Resource 2:** the plan uses 6 + 0 = 6 of 8, so 2 are spare. Therefore **y₂ = 0**, and you know that **before** solving the dual.
* The dual answer is y = (4, 0), w = 6×4 + 8×0 = 24 ✓.
* **Product 2 isn't made.** It uses 1 of resource 1 + 2 of resource 2, worth 1×4 + 2×0 = **4**, but only earns **2**. It ties up $4 of resources to earn $2, so **don't make it**. The gap 4 − 2 = **2** is its **reduced cost**.

### Example 2: "explain the gap in a dual constraint" (practice exam 2, Q6d)

Furniture workshop (z in $100s): max 5x₁ + 4x₂ + 3x₃ (chairs, tables, shelves), with timber (2, 3, 1) ≤ 50, labour (4, 1, 2) ≤ 110, finishing (3, 4, 2) ≤ 80. Optimum: 20 chairs, 0 tables, 10 shelves, z = 130, y\* = (1, 0, 1).

**Step 1: plug y\* into every product's dual constraint.**

| Product | Uses (timber, labour, finishing) | Resources worth at y\* = (1, 0, 1) | Profit | Gap | Made? |
|---|---|---|---|---|---|
| Chair | (2, 4, 3) | 2 + 0 + 3 = 5 | 5 | **0** | yes, 20 |
| Table | (3, 1, 4) | 3 + 0 + 4 = 7 | 4 | **3** | **no, 0** |
| Shelf | (1, 2, 2) | 1 + 0 + 2 = 3 | 3 | **0** | yes, 10 |

Reading it: the **only** product with a gap is the one that **isn't made**.

**Step 2: what the gap means.** A table uses up resources that earn **$700** in the current plan, and gives back only **$400**. Each table loses **$300**.

**Step 3: check by actually making one table.** The x₂ column of the final tableau, (2, −5, −1), says how the plan rebalances: 2 fewer chairs, 5 more spare labour days, 1 more shelf.

| Plan | Chairs | Tables | Shelves | Timber (of 50) | Labour (of 110) | Finishing (of 80) | Profit ($100s) |
|---|---|---|---|---|---|---|---|
| Optimal | 20 | 0 | 10 | 40 + 0 + 10 = 50 | 80 + 0 + 20 = 100 | 60 + 0 + 20 = 80 | 100 + 0 + 30 = **130** |
| Force 1 table | 18 | 1 | 11 | 36 + 3 + 11 = 50 | 72 + 1 + 22 = 95 | 54 + 4 + 22 = 80 | 90 + 4 + 33 = **127** |

Reading it: the plan still fits, and profit drops by **3 → $300**, the gap exactly. So **gap in a dual constraint = reduced cost**.

**Step 4: the rule.** For every product, **(amount made) × (gap) = 0**: chairs 20 × 0, tables 0 × 3, shelves 10 × 0. A product with a gap loses money on every unit, so the optimal plan makes none. A product that is made sits at exactly break-even.

---

## 6.9 Why bother with the dual?

* **Smaller problem:** 500 products and 3 resources gives an original problem with 500 variables, but a dual with only **3 variables**. Solve the small one.
* It gives the **shadow prices** directly.
* It **proves** an answer is optimal.
* In games (note 8), the two players' problems are duals of each other.

## 6.10 Solving a dual by hand

The dual is a **min with `≥` constraints**, so (0, 0) isn't allowed. You need **Big M** (note 4), or the graphical method if it has two variables.

**Week 9 prac Q1:**
```
Dual:     min 8y₁ + 6y₂   s.t. 2y₁ + y₂ ≥ 6,  y₁ + y₂ ≥ 5
→ Big M (excess + artificial on each row; clear the M's from the z row)
→ y = (1, 4), w = 8 + 24 = 32

Original: max 6x₁ + 5x₂   s.t. 2x₁ + x₂ ≤ 8,  x₁ + x₂ ≤ 6
→ x = (2, 4), z = 12 + 20 = 32     ✓ equal, as strong duality says
```

**Graphically (2 dual variables):** plot the `≥` lines, find the corners of the open region, and work out w at each. Revision Q2: corners (0, 4) → 24, (3, 0) → 30, **(1, 2) → 22** ← smallest, so that's the answer.

---

## The whole idea in three lines

1. **Original problem:** what should I make? → the plan.
2. **Dual:** what is each resource worth? → the shadow prices.
3. **Same total**, because profit is just resources turned into money.

---

## Common mistakes

1. Reading **across** rows instead of **down** columns for the dual constraints.
2. Forgetting to flip `≤` to `≥` and max to min.
3. Leaving out a variable whose number is 0 in a row. Write it with a 0 so you don't lose track.
4. Thinking the dual gives a different number. Best z = best w, always.

---

## Check yourself

<details><summary>1. Write the dual of max 5x₁ + 6x₂ s.t. x₁ + x₂ ≤ 8, 3x₁ + 2x₂ ≤ 18, x₁ ≤ 5.</summary>

3 constraints → 3 values. 2 products → 2 "fair" constraints.
* x₁ uses (1, 3, 1), earns 5 → y₁ + 3y₂ + y₃ ≥ 5
* x₂ uses (1, 2, 0), earns 6 → y₁ + 2y₂ ≥ 6 (x₁ ≤ 5 is x₁ + 0x₂ ≤ 5, so there's no y₃ here)

**min 8y₁ + 18y₂ + 5y₃ s.t. y₁ + 3y₂ + y₃ ≥ 5, y₁ + 2y₂ ≥ 6, y ≥ 0.**
</details>

<details><summary>2. A plan has z = 40, and someone shows fair values y with w = 40. What can you conclude?</summary>

A profit can never be above a ceiling (weak duality), so 40 can't be beaten and 40 can't be lowered. **Both are optimal.**
</details>

<details><summary>3. At the best plan, resource 3 has 7 units left over. What is y₃, and why does that make sense?</summary>

**0.** You already have 7 spare, so one more unit is worth nothing to you.
</details>

<details><summary>4. Smoothie bar: someone offers y = (3, 0). Is that a fair value? What ceiling does it give?</summary>

Smoothie 1: 2(3) + 0 = 6 ≥ 5 ✓. Smoothie 2: 3 + 0 = 3 ≥ 4 ✗. **Not fair**: it undervalues smoothie 2, so it doesn't give a ceiling.
</details>
