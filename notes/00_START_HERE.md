# MXB109 Revision Notes: Start Here

> These notes use the same examples as your lectures and pracs (the farmer, the energy co-op, the grain mix, Powerco, Seervada Park…), explained from the beginning.
> Each note starts with **the big idea in plain words**, then works **one example step by step**, saying *what* we're doing and *why*.

## How to read these notes

* **VS Code:** open a file and press `Cmd+Shift+V` for the preview. Pictures are in `img/` and show up straight away.
* Every table has a **"Reading it:"** line underneath that says what the table means. Read those lines. They're the point of the table.
* **Check yourself** questions at the end of each note have the answer hidden. Click to open it **after** you've tried.

## The order to read them in

Each note builds on the one before, so read them in order the first time.

| # | Note | What it's about, in plain words |
|---|---|---|
| 1 | [01_Formulation_and_Standard_Form.md](01_Formulation_and_Standard_Form.md) | Turning a word problem into maths. Slack, excess and artificial variables |
| 2 | [02_Graphical_Method.md](02_Graphical_Method.md) | Solving a 2-variable problem by drawing it. Why the answer is always at a corner |
| 3 | [03_Simplex_Method.md](03_Simplex_Method.md) | Solving with tables instead of a drawing: walking from corner to corner |
| 4 | [04_BigM_and_Special_Cases.md](04_BigM_and_Special_Cases.md) | What to do when you can't start at (0, 0). Problems with no answer or many answers |
| 5 | [05_Sensitivity_Shadow_Price_Reduced_Cost.md](05_Sensitivity_Shadow_Price_Reduced_Cost.md) | "What if" questions: what is one more hour worth? Why don't we make product X? |
| 6 | [06_Duality.md](06_Duality.md) | Every problem has a partner problem whose answer is the shadow prices |
| 7 | [07_Transportation.md](07_Transportation.md) | Shipping goods from factories to cities as cheaply as possible |
| 8 | [08_Game_Theory.md](08_Game_Theory.md) | Two opponents choosing at the same time |
| 9 | [09_Networks.md](09_Networks.md) | Shortest route, and connecting everything with the least cable |
| 10 | [10_Cheat_Sheet.md](10_Cheat_Sheet.md) | Everything for the exam on one sheet: rules, formulas, sentences to write |

Notes 1 → 5 are one connected story. Notes 6 → 9 can be read in any order after that.

---

## The one big idea of the whole unit

Every problem in MXB109 has the same three parts:

1. **Things you choose** (how many of each product, how much to ship on each route…)
2. **A goal** (make the most profit, or spend the least)
3. **Limits** (only so much land, labour, supply…)

That is a **linear program (LP)**. The topics differ only in the *shape* of the problem, and the shape tells you which method to use.

### Which method? Ask these questions in order

1. **Is there a grid of supplies, demands and shipping costs?** → Transportation (note 7)
2. **Are there two opponents and a table of payoffs?** → Game theory (note 8)
3. **Are there points joined by roads, pipes or cables?** → Networks (note 9)
   * "quickest route from A to B" → shortest path
   * "connect everything as cheaply as possible" → minimum spanning tree
4. **Otherwise it's a plain LP:**
   * only **2 variables** → you can draw it: graphical method (note 2)
   * more variables, and (0, 0) is allowed → simplex (note 3)
   * more variables, and (0, 0) is **not** allowed (there's a `≥` or `=`) → Big M, then simplex (note 4)
   * afterwards, the "what if" questions → shadow prices and reduced costs (note 5), duality (note 6)

### Words in the question → what to use

| If the question says… | Use… |
|---|---|
| "maximise / minimise … subject to", resources | write the LP, then graphical or simplex |
| "at least", "minimum requirement", "exactly" | `≥` or `=` constraints, so **Big M** |
| "one more unit", "worth", "how much would you pay", "binding" | **shadow price** |
| "not produced", "how much would its profit need to rise" | **reduced cost** |
| "partner problem", "bound", "buyer of your resources", "smallest offer you can't refuse" | **duality** |
| "supply", "demand", "depots", a cost table | **transportation** |
| "zero-sum", "payoff", "opponent" | **game theory** |
| "quickest / shortest route" | **shortest path** |
| "connect every…", "least cable / pipe" | **minimum spanning tree** |

---

## The extra variables, in one table

You'll meet these in note 1, and every later note uses them. Come back here whenever you forget.

| Constraint | What you add | Name | What it means in real life |
|---|---|---|---|
| `≤` (a limit, like "only 40 hours") | `+ s` | **slack** | how much is **left over** (unused hours) |
| `≥` (a requirement, like "at least 30 kg") | `− e` | **excess** (also called surplus) | how much you went **over** the requirement |
| `≥` or `=` | `+ a` | **artificial** | nothing real. A temporary helper so simplex has somewhere to start. Must be 0 by the end |

**At the answer:**
* slack or excess = **0** → that limit is completely used up. We say it's **binding**.
* slack or excess **> 0** → there's room to spare. We say it's **non-binding**.

---

## The resource sheet (you get this in the exam)

You don't need to memorise these. You need to know **when** to use each one.

* General LP: max/min z = c₁x₁ + … + cₙxₙ subject to constraints with ≤, =, ≥, and xⱼ ≥ 0
* Row operations: Rᵢ′ = mRᵢ (multiply a row), Rᵢ′ = Rᵢ + nRⱼ (add a multiple of another row)
* Slope of the line ax + by = c is **−a/b**
* **Shadow price = (new best z) − (old best z)** when that constraint's right-hand side goes up by **one**
* **Big M:** for a max, subtract Maᵢ for each artificial. For a min, add Maᵢ.
* Transportation: a starting plan uses **m + n − 1** cells. uᵢ + vⱼ = cᵢⱼ on filled cells. c̄ᵢⱼ = cᵢⱼ − uᵢ − vⱼ. θ = smallest amount on a "−" cell.
* Networks: at every node except the start and the end, flow in = flow out.

## How marks are given

* **Say which method and why:** "This is a transportation problem because there are supplies, demands and a cost per route."
* **Show every step:** which variable enters, which leaves, and the row operations.
* **Finish in words:** "Make 2 battery systems and 6 arrays, for 18 MWh per year. All rooftops and installer-days are used."
