# MXB109 Practice Exam 4 (short)

**Total: 40 marks · Suggested time: 80 minutes · Resource sheet allowed** (see [resource sheet](../notes/00_START_HERE.md#the-resource-sheet-you-get-this-in-the-exam))

Short questions in the style of the lecture revision pracs: one task each, small numbers. Show your working.

Solutions: [Practice_Exam_4_Solutions.md](Practice_Exam_4_Solutions.md).

---

## Question 1: Formulation (3 marks)

A juice bar makes Berry smoothies and Green smoothies. Profit is $4 per Berry and $3 per Green.

* A Berry uses 2 cups of fruit and 1 scoop of yoghurt. A Green uses 1 cup of fruit and 1 scoop of yoghurt.
* Each day there are 100 cups of fruit and 80 scoops of yoghurt.
* At least 10 Greens must be made.
* The bar makes no more than twice as many Berries as Greens.

Formulate an LP to maximise daily profit. Define your variables.

---

## Question 2: Standard form (3 marks)

```
min z = 3x₁ + 2x₂ + 4x₃
s.t.  x₁ +  x₂ +  x₃ ≥ 10
     2x₁ −  x₂       = 4
            x₂ + 2x₃ ≤ 16
      x₁       −  x₃ ≥ −2
      x₁, x₂, x₃ ≥ 0
```

Write this LP in standard form, ready for the Big M method. How many artificial variables are needed?

---

## Question 3: Graphical method (4 marks)

```
max z = 5x₁ + 4x₂
s.t.  x₁ + x₂ ≤ 7
     2x₁ + x₂ ≤ 10
           x₂ ≤ 5
      x₁, x₂ ≥ 0
```

(a) Sketch the feasible region and list every corner point with its z value. **(3)**

(b) State the optimal solution and which constraints are binding. **(1)**

---

## Question 4: Simplex method (5 marks)

```
max z = 4x₁ + 3x₂
s.t. 2x₁ +  x₂ ≤ 8
      x₁ + 2x₂ ≤ 10
      x₁, x₂ ≥ 0
```

(a) Solve using the simplex method. Show each tableau, the ratio test, and the entering and leaving variables. **(4)**

(b) State the optimal solution and the shadow price of each constraint. **(1)**

---

## Question 5: Big M method (5 marks)

A farmer mixes feed A ($4 per kg) and feed B ($5 per kg). The mix needs at least 8 units of protein and at least 7 units of fibre.

```
min z = 4x₁ + 5x₂
s.t. 2x₁ +  x₂ ≥ 8      protein
      x₁ + 2x₂ ≥ 7      fibre
      x₁, x₂ ≥ 0
```

(a) Write the initial Big M tableau, with the M's cleared from the objective row. **(2)**

(b) Solve it. **(2)**

(c) State the cheapest mix and its cost. **(1)**

---

## Question 6: Sensitivity analysis (4 marks)

A workshop makes desks (x₁), shelves (x₂) and stools (x₃), with profit $600, $500 and $400 each (z in **$100s**).

```
max z = 6x₁ + 5x₂ + 4x₃
s.t.  x₁ +  x₂ +  x₃ ≤ 50      labour (hours)
     3x₁ + 2x₂ + 2x₃ ≤ 120     machine (hours)
      x₁             ≤ 30      desk kits in stock
      x₁, x₂, x₃ ≥ 0
```

The final tableau is:

| Basis | x₁ | x₂ | x₃ | s₁ | s₂ | s₃ | RHS |
|---|---|---|---|---|---|---|---|
| s₃ | 0 | 0 | 0 | 2 | −1 | 1 | 10 |
| x₂ | 0 | 1 | 1 | 3 | −1 | 0 | 30 |
| x₁ | 1 | 0 | 0 | −2 | 1 | 0 | 20 |
| z | 0 | 0 | 1 | 3 | 1 | 0 | 270 |

(a) Give the shadow price of each resource in dollars. Which resources are fully used? **(2)**

(b) Over what range of labour hours is the labour shadow price valid? Should the workshop pay **$2,000** for **8 extra labour hours**? **(1)**

(c) Why are no stools made? How much would a stool need to earn before it is worth making? **(1)**

---

## Question 7: Duality (4 marks)

```
max z = 3x₁ + 4x₂
s.t.  x₁ + 2x₂ ≤ 10
     2x₁ + 2x₂ ≤ 14
      x₁, x₂ ≥ 0
```

(a) Write the dual. **(2)**

(b) Analyst A says x = (4, 3) is optimal. Analyst B says y = (1, 1) is optimal for the dual. Without using the simplex method, show that they are both right. **(2)**

---

## Question 8: Transportation (5 marks)

|  | D1 | D2 | D3 | Supply |
|---|---|---|---|---|
| P1 | 4 | 6 | 8 | 50 |
| P2 | 5 | 3 | 7 | 70 |
| **Demand** | 30 | 40 | 20 | |

Costs are $ per unit.

(a) Balance the problem. **(1)**

(b) Find the northwest corner starting solution and its cost. **(1)**

(c) Use u and v to improve the solution until it is optimal. Give the optimal plan and its cost. **(3)**

---

## Question 9: Game theory (4 marks)

Payoffs to the row player:

|  | C1 | C2 | C3 |
|---|---|---|---|
| R1 | 3 | −1 | 4 |
| R2 | −2 | 2 | 1 |

(a) Show that the game has no saddle point. **(1)**

(b) Use dominance to reduce the game to 2 × 2. Find both players' optimal mixed strategies and the value of the game. **(3)**

---

## Question 10: Networks (3 marks)

| Edge | S–A | S–B | A–B | A–C | B–C | B–D | C–D | C–T | D–T |
|---|---|---|---|---|---|---|---|---|---|
| Length | 3 | 5 | 1 | 6 | 3 | 7 | 2 | 5 | 4 |

(a) Find the shortest path from S to T and its length. **(2)**

(b) Find the minimum spanning tree and its total length. **(1)**
