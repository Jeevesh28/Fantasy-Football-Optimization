# Fantasy Football Optimization

Picks an optimal 10-player fantasy football squad (5 starters and 5 substitutes) as an integer linear program: maximize total player rating subject to position, nationality, club and footedness rules. Built for the Advolution 7.0 competition.

**Stack:** Python · PuLP · pandas · Matplotlib · Seaborn · Plotly

---

## Problem

From a database of players and their attributes, build:

- a **main team** of 5: one forward, one midfielder, one defender, one goalkeeper, and a fifth outfield player in any position except goalkeeper;
- a **substitute team** of 5, drawn only from players listed as `SUB` or `RES`.

Across the squad:

- no two players may share a **nationality** or a **club**;
- each team needs at least one **left-footed** player.

Positions are grouped from the dataset's codes: forwards (`CF, RF, LF, ST, LS, RS, LW, RW`), midfielders (`LM, RM, CM, CAM, CDM, LAM, LCM, LDM, RCM, RAM, RDM`), defenders (`CB, LB, RB, LCB, RCB, LWB, RWB`) and goalkeepers (`GK`).

## Approach

**1. Clean the data.** Analyze and impute missing values, then map each player's position code to one of the four groups.

**2. Split the pool.** Separate main-team candidates from `SUB` / `RES` players.

**3. Solve the main team as an ILP** (PuLP, `LpMaximize`). With a binary variable *x<sub>i</sub>* per player:

```
maximize    Σ_i rating_i · x_i
subject to  Σ x_i (left-footed)          ≥ 1
            Σ x_i (in position p)        ≤ slots_p     for each position p
            Σ x_i (from club c)          ≤ 1           for each club c
            Σ x_i (of nationality n)     ≤ 1           for each nationality n
```

**4. Solve the substitutes as a second ILP** with the same structure, plus constraints that exclude every club and nationality already used by the main team. Solving in two stages keeps each model small and lets the main team take priority on the best players.

**5. Verify visually.** Plots check the chosen squad against every constraint and show the final lineup.

## Result

**Main team**

| Name | Club | Nationality | Position | Foot | Rating |
|---|---|---|---|---|---|
| J. Oblak | Atlético de Madrid | Slovenia | GK | Right | 91 |
| R. Varane | Manchester United | France | DEF | Right | 88 |
| V. van Dijk | Liverpool | Netherlands | DEF | Right | 89 |
| K. De Bruyne | Manchester City | Belgium | MID | Right | 91 |
| L. Messi | Paris Saint-Germain | Argentina | FWD | Left | 93 |

**Substitute team**

| Name | Club | Nationality | Position | Foot | Rating |
|---|---|---|---|---|---|
| J. Pavlenka | SV Werder Bremen | Czech Republic | GK | Right | 82 |
| G. Chiellini | Juventus | Italy | DEF | Left | 86 |
| J. Boateng | Olympique Lyonnais | Germany | DEF | Right | 83 |
| Xavi | FC Barcelona | Spain | MID | Right | 86 |
| Z. Ibrahimović | AC Milan | Sweden | FWD | Right | 84 |

![Team lineup](https://i.imgur.com/HLP9f5b.png)

## Repository layout

```
Advolution 7.0.ipynb                 data cleaning, both ILPs, visualizations
Advolution 7.0 Data.csv              player database
Lone Wolf_Advolution 7.0.pdf / .pptx competition write-up and slides
```

## Limitations

- Solving main and substitute teams in sequence is greedy across the two stages; a single joint ILP could find a higher combined rating.
- Rating is the only objective. Cost, form or position-specific attributes would change the squad.
