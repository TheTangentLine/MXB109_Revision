# 1. Writing the Problem: Formulation and Standard Form

> **In one sentence:** before you can solve anything, you turn the word problem into maths (formulation), then rewrite every limit as an equation by adding "leftover" variables (standard form).

---

## 1.1 The big idea

Every problem in this unit is a **linear program (LP)**. It always has three parts:

| Part | The question to ask | Farmer example (week 1) |
|---|---|---|
| **Decision variables** | What do I get to choose? | P = hectares of pineapples, B = hectares of bananas |
| **Objective** | What am I trying to make biggest or smallest? | profit: z = 100P + 30B |
| **Constraints** | What's stopping me from doing more? | land, labour, the café contract |

Plus: you can't plant negative hectares, so **P, B ≥ 0**.

"Linear" just means no powers or products of variables: no P², no P×B, no √P. Only numbers × variables, added up.

---

## 1.2 Writing an LP from words: the farmer, step by step

**The story:** a farmer has 7 ha of land and 40 hours of labour. Pineapples earn $100 per ha and need 10 hours per ha. Bananas earn $30 per ha and need 4 hours per ha. A café contract says the farmer must supply at least 30 kg of bananas, and each hectare of bananas yields 10 kg.

**Step 1: what do I choose?** How much of each crop to plant.
→ P = ha of pineapples, B = ha of bananas. **Always write the units.**

**Step 2: what's the goal, as a sentence?** "Make as much profit as possible."
→ profit = $100 per ha × P + $30 per ha × B
→ **max z = 100P + 30B**

**Step 3: each limit, as a sentence, then in symbols.**

| Sentence | Symbols |
|---|---|
| "Land used can't be more than 7 ha." | P + B ≤ 7 |
| "Hours used can't be more than 40." 10 h for each ha of P, 4 h for each ha of B | 10P + 4B ≤ 40 |
| "Bananas supplied must be at least 30 kg." 10 kg for each ha of B | 10B ≥ 30 |
| "Can't plant negative hectares." | P, B ≥ 0 |

**Step 4: check the units on both sides.** 10P + 4B ≤ 40: (hours/ha × ha) on the left, hours on the right ✓. If one side is hours and the other is kg, you've made a mistake.

**The finished LP:**
```
max z = 100P + 30B
s.t.   P +  B ≤ 7      land (ha)
     10P + 4B ≤ 40     labour (hours)
          10B ≥ 30     café contract (kg)
        P, B ≥ 0
```
(The answer, which we'll find later: P = 2.8, B = 3, profit $370.)

### Tips

* What you **choose** becomes the variables. What **follows** from those choices (profit, hours used) becomes the objective and constraints. If you find yourself "choosing the profit", something's wrong.
* "**at most**", "no more than", "only … available" → `≤`
* "**at least**", "a minimum of", "must supply" → `≥`
* "**exactly**" → `=`
* Pick variables that make sense as fractions (hectares, hours, tonnes), so an answer like 2.8 still means something.

### Two common shapes

| Shape | Goal | Constraints are mostly… | Examples |
|---|---|---|---|
| **Making things** | max profit | `≤` (limited resources) | farmer, co-op, bakery |
| **Meeting requirements** | min cost | `≥` (must provide at least…) | grain mix, seed mix, diet |

---

## 1.3 Standard form: why we turn `≤` into `=`

The simplex method (note 3) works with **equations**, not inequalities. So we add a variable that measures the **gap**.

### Slack: what's left over (for `≤`)

Land: P + B ≤ 7. Add **s₁ = land not used**:
```
P + B + s₁ = 7
```
If you plant 5.8 ha, then s₁ = 7 − 5.8 = 1.2 ha spare.

### Excess: how much you went over (for `≥`)

Contract: 10B ≥ 30. Subtract **e₃ = kg of bananas above the 30 kg minimum**:
```
10B − e₃ = 30
```
If you grow 4 ha of bananas (40 kg), then e₃ = 40 − 30 = 10 kg extra.

The sign is different because slack fills the gap up to a **maximum**, while excess is the amount **over** a **minimum**.

### The farmer in standard form
```
max z = 100P + 30B
s.t.   P +  B + s₁           = 7
     10P + 4B      + s₂      = 40
          10B           − e₃ = 30
     P, B, s₁, s₂, e₃ ≥ 0
```

### What slack and excess look like

![Slack and excess shown as bars](img/slack_excess.png)

**Reading the picture:**
* **Left:** the allowed region. Plan **A** = (2.8, 3) is the best plan. Plan **B** = (2, 4) is allowed but not the best.
* **Right:** one bar per constraint, showing how much the plan **uses** against the limit (dashed line).
  * **Slack** = the gap **before** the limit (resource not used).
  * **Excess** = the bit **past** the requirement (over-delivered).

Calculating them for both plans:

| | Plan A (2.8, 3), the best | Plan B (2, 4) |
|---|---|---|
| land: s₁ = 7 − (P + B) | 7 − 5.8 = **1.2** ha spare | 7 − 6 = 1 |
| labour: s₂ = 40 − (10P + 4B) | 40 − 40 = **0** (all used) | 40 − 36 = 4 |
| contract: e₃ = 10B − 30 | 30 − 30 = **0** (exactly met) | 40 − 30 = 10 kg extra |

**Reading it:** at the best plan, labour and the contract are at exactly 0. They're what is stopping the farmer from making more money. Land has 1.2 ha spare, so land is not the problem.

### Binding and non-binding

| Slack or excess at the answer | Means | Word |
|---|---|---|
| **= 0** | the limit is used up exactly. The point sits **on** that constraint's line | **binding** |
| **> 0** | there's room to spare | **non-binding** |

Why this matters later (note 5):
* Land has 1.2 ha spare, so **one more hectare is worth $0**. You already have land you're not using.
* Labour is binding, so **one more hour is worth money** ($10, it turns out).
* The contract is binding, so making it bigger would **cost** the farmer ($1 per extra kg).

> **Slack tells you where the pressure is.** A resource with slack isn't holding you back.

---

## 1.4 Artificial variables: a temporary helper

You only need these for the **simplex method**. If you solve with Excel Solver or by drawing a graph, you never see them.

**The problem:** simplex always starts at (0, 0), with every decision variable at 0 (note 3). Try that with the contract row:
```
10B − e₃ = 30
B = 0  →  −e₃ = 30  →  e₃ = −30   ✗
```
A variable can't be negative, so (0, 0) isn't an allowed starting point. Simplex has nowhere to start.

**The fix:** add a made-up variable **a₃ ≥ 0** to that row:
```
10B − e₃ + a₃ = 30
B = 0, e₃ = 0  →  a₃ = 30   ✓
```
Now simplex can start. You can think of a₃ as "how many kg short of the contract we are". At the start, that's 30 kg.

**The catch:** a₃ isn't real. It must be **0** in the final answer. We make sure of that by giving it a huge penalty in the objective, called **M** (note 4).

### Which rows need an artificial?

**Put zeros in for every decision variable.** Any constraint that breaks gets an artificial.

| Constraint | At (0, 0) | Artificial? |
|---|---|---|
| P + B ≤ 7 | 0 ≤ 7 ✓ | no, the slack s₁ = 7 starts the row |
| 10P + 4B ≤ 40 | 0 ≤ 40 ✓ | no |
| 10B ≥ 30 | 0 ≥ 30 ✗ | **yes** |

In practice: every `≥` with a positive right-hand side, and every `=`.

---

## 1.5 Two small fixes before you start

### A negative right-hand side

Standard form needs every right-hand side (RHS) to be **≥ 0**. If one is negative, multiply the whole row by −1. That **flips** the inequality:
```
−x₁ + x₂ ≤ −2          RHS is negative ✗
× (−1):   x₁ − x₂ ≥ 2   now it's a ≥ constraint
→  x₁ − x₂ − e₂ = 2     (and it will need an artificial)
```

### Minimising

The method is set up for **max**. To minimise cost, maximise **negative cost** instead:
```
min z = 5x₁ + 2x₂   →   max z′ = −5x₁ − 2x₂      (where z′ = −z)
```
At the end, flip the sign back: if best z′ = −24, the minimum cost is z = 24.

---

## 1.6 Full worked conversion (revision prac Q3)

```
min z = 5x₁ + 2x₂ + 4x₃
s.t. 3x₁ +  x₂ + 2x₃ ≥ 12
      x₁ + 2x₂       = 8
            x₂ + 4x₃ ≤ 20
```

**Step 1: min → max.** max z′ = −5x₁ − 2x₂ − 4x₃

**Step 2: one row at a time.**

| Row | Type | What to add | Why |
|---|---|---|---|
| 1 | `≥` | − e₁ + a₁ | excess measures how far over 12. At (0, 0, 0), 0 ≥ 12 fails, so it needs an artificial |
| 2 | `=` | + a₂ | no gap to measure, so no slack or excess. But 0 = 8 fails, so it needs an artificial |
| 3 | `≤` | + s₃ | slack = unused amount. 0 ≤ 20 is fine, so no artificial |

**Result:**
```
max z′ = −5x₁ − 2x₂ − 4x₃
s.t. 3x₁ +  x₂ + 2x₃ − e₁ + a₁           = 12
      x₁ + 2x₂                 + a₂      = 8
            x₂ + 4x₃                + s₃ = 20
     all variables ≥ 0
```
(For Big M you'd also subtract Ma₁ + Ma₂ in the objective. See note 4.)

---

## Common mistakes

1. Forgetting the units, or mixing units on the two sides of a constraint.
2. `≥` with **+e** instead of **−e**. Excess is *subtracted*.
3. Leaving a negative RHS. Multiply the row by −1 and flip the sign.
4. Forgetting to flip z′ back to z at the end of a minimisation.

---

## Check yourself

<details><summary>1. A constraint is x₁ + 2x₂ ≥ 10. At the answer, x₁ = 4 and x₂ = 5. What is the excess, and is the constraint binding?</summary>

Left side: 4 + 10 = 14. Excess e = 14 − 10 = **4**. It's more than 0, so the constraint is **non-binding** (the requirement is beaten by 4).
</details>

<details><summary>2. Why does an "=" row get an artificial but no slack or excess?</summary>

The two sides must be exactly equal, so there's no gap to measure, and no slack or excess. But at (0, 0) the left side is 0, which doesn't equal the RHS, so simplex still needs an artificial to start.
</details>

<details><summary>3. At the answer, s₂ = 0. What do you tell the manager?</summary>

"Resource 2 is completely used up. It's a bottleneck (binding), and getting more of it would probably increase profit."
</details>

<details><summary>4. A bakery makes x₁ sourdough and x₂ rye. Each sourdough uses 2 kg flour, each rye 1 kg, and there's 16 kg flour. Write the constraint and its standard form.</summary>

2x₁ + x₂ ≤ 16 → **2x₁ + x₂ + s₁ = 16**, where s₁ = kg of flour left over.
</details>
