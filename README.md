# JSONS

A collection of structured JSON datasets for kitchen and recipe-related reference data.

## Files

### `cleanup_difficulty.json`

Rates how difficult kitchen items are to clean on a 1–10 scale, broken down by five dimensions:

| Dimension | Description |
|-----------|-------------|
| **time** | Estimated time to clean (seconds to minutes) |
| **effort** | Physical scrubbing intensity required |
| **complexity** | Shape difficulty (crevices, holes, edges) |
| **care** | Fragility or special handling required |
| **size** | Bulkiness and surface area |

**Scoring** — each item includes an overall `difficulty` score derived from the weighted sum of its dimensions:

```
difficulty = (time × 0.35) + (effort × 0.25) + (complexity × 0.15) + (care × 0.15) + (size × 0.10)
```

The result is scaled to the 1–10 range. This lets you query any item's dimensions directly and compute a comparable score, or just use the pre-assigned `difficulty` value.

**Categories** — items are grouped into six categories:

- **utensils** — forks, knives, whisks, graters, etc.
- **cookware** — pans, pots, baking dishes, etc.
- **dishware** — plates, bowls, glasses, etc.
- **delicate_and_specialty** — crystal, fine china, copper, clay, etc.
- **large_and_bulky** — turkey roasters, stockpots, BBQ grates, etc.
- **notoriously_difficult** — burnt cookware, fondue pots, meat grinders, etc.

---

### `ingredients.json`

Scores a recipe's ingredient complexity on a 1–10 scale:

| Dimension | Weight | Description |
|-----------|--------|-------------|
| **count** | 0.30 | Number of distinct ingredients required |
| **sourcing** | 0.25 | Difficulty of finding ingredients (pantry staple vs specialty) |
| **prep_complexity** | 0.20 | Amount of prep work ingredients need before use |
| **caloric_density** | 0.15 | How calorie-dense the ingredient mix is per unit weight |
| **macro_balance** | 0.10 | How balanced the macronutrient profile is |

**Anchors** — toast with butter (1), spaghetti aglio e olio (3), pad thai (5), pho from scratch (8), beef wellington (10)

---

### `cooking_steps.json`

Scores a recipe's step complexity on a 1–10 scale:

| Dimension | Weight | Description |
|-----------|--------|-------------|
| **count** | 0.25 | Number of discrete steps |
| **sequential_dependency** | 0.20 | How much each step depends on the previous |
| **active_attention** | 0.20 | Hands-on focus required vs passive waiting |
| **complexity_per_step** | 0.20 | Number of sub-actions per step |
| **critical_timing** | 0.15 | How time-sensitive the steps are |

**Anchors** — make tea (1), scrambled eggs (2), pasta from scratch with sauce (4), croissant (8), beef wellington (10)

---

### `technicality.json`

Scores a recipe's technical difficulty on a 1–10 scale:

| Dimension | Weight | Description |
|-----------|--------|-------------|
| **skill_level** | 0.25 | Minimum cooking skill required |
| **technique_count** | 0.20 | Number of distinct culinary techniques involved |
| **error_tolerance** | 0.25 | How unforgiving the recipe is to mistakes |
| **temperature_precision** | 0.15 | How exact temperature control must be |
| **knife_work** | 0.15 | Level of knife skill required |

**Anchors** — cereal with milk (1), grilled cheese (2), stir fry (4), souffle (8), tempering chocolate (10)

---

### `time_to_cook.json`

Scores a recipe's total time investment on a 1–10 scale:

| Dimension | Weight | Description |
|-----------|--------|-------------|
| **prep_time** | 0.30 | Time preparing ingredients before cooking |
| **cook_time** | 0.30 | Time actively cooking with heat |
| **passive_time** | 0.15 | Unattended time (marinating, proofing, chilling) |
| **post_cook_time** | 0.25 | Resting, cooling, plating, finishing |

**Anchors** — instant noodles (1), scrambled eggs (2), spaghetti bolognese (4), slow roasted pork shoulder (7), beef wellington (10)

---

### `output_yield.json`

Scores a recipe's output quantity and quality on a 1–10 scale:

| Dimension | Weight | Description |
|-----------|--------|-------------|
| **servings** | 0.20 | Number of servings produced |
| **scalability** | 0.20 | How easily the recipe scales up or down |
| **consistency_of_yield** | 0.20 | How predictable output quantity is across attempts |
| **waste_ratio** | 0.20 | Ratio of waste to final edible output |
| **leftover_quality** | 0.20 | How well the output holds up as leftovers |

**Anchors** — single serving sandwich (1), batch of cookies (3), pot of soup serves 6 (5), wedding cake serves 50 (8), commercial batch (10)

---

### `reproducibility.json`

Scores how difficult a recipe is to reproduce consistently on a 1–10 scale (higher = harder):

| Dimension | Weight | Description |
|-----------|--------|-------------|
| **instruction_precision** | 0.25 | Clarity and completeness of the written recipe |
| **ingredient_specificity** | 0.20 | How precisely ingredients must be specified |
| **environmental_sensitivity** | 0.20 | How much altitude, humidity, oven variance affect results |
| **technique_dependence** | 0.20 | How much the result depends on cook's technique |
| **measurement_tolerance** | 0.15 | How precise measurements need to be |

**Anchors** — boil water (1), boxed mac and cheese (2), chocolate chip cookies (3), sourdough bread (7), tempered chocolate (10)

---

### `health.json`

Scores a recipe's health profile on a 1–10 scale (1 = healthiest, 10 = least healthy):

| Dimension | Weight | Description |
|-----------|--------|-------------|
| **caloric_load** | 0.20 | Total calories per serving |
| **macro_profile** | 0.25 | Quality of macronutrient balance |
| **micronutrient_density** | 0.25 | Presence of key vitamins and minerals |
| **sodium_level** | 0.15 | Sodium content per serving |
| **sugar_profile** | 0.15 | Total and added sugar content |

**Anchors** — mixed green salad with grilled chicken (1), oatmeal with berries (2), grilled salmon with rice (3), fettuccine alfredo (7), deep fried twinkie (10)

---

### `satiety.json`

Scores how filling a recipe is on a 1–10 scale (1 = least satiating, 10 = most):

| Dimension | Weight | Description |
|-----------|--------|-------------|
| **fullness_index** | 0.30 | Immediate fullness after a serving |
| **duration** | 0.25 | How long fullness lasts before hunger returns |
| **caloric_efficiency** | 0.20 | Satiety per calorie consumed |
| **volume** | 0.10 | Physical volume of food per serving |
| **glycemic_impact** | 0.15 | Blood sugar stability after eating |

**Anchors** — celery sticks (1), green salad no protein (2), oatmeal with nuts (5), steak with potatoes (8), chili with beans and meat (10)

---

### `sections.json`

Scores a recipe's multi-section complexity on a 1–10 scale:

| Dimension | Weight | Description |
|-----------|--------|-------------|
| **section_count** | 0.15 | Number of distinct sub-recipes or sections |
| **coordination_complexity** | 0.25 | Difficulty of timing and synchronizing sections |
| **parallelizability** | 0.20 | Whether sections can be made in parallel or must be sequential |
| **interdependence** | 0.20 | How much one section's result affects another |
| **assembly_complexity** | 0.20 | Difficulty of combining sections into the final dish |

**Anchors** — scrambled eggs (1), pancakes with syrup (2), burger with patty/bun/toppings (3), cake with frosting (5), lasagna with pasta/sauce/bechamel/layers (7), croquembouche (10)

---

### `pan_efficiency.json`

Scores a recipe's pan/vessel efficiency on a 1–10 scale (1 = most efficient, 10 = least):

| Dimension | Weight | Description |
|-----------|--------|-------------|
| **total_pans** | 0.35 | Total pans, pots, and bakeware needed |
| **sequential_reuse** | 0.20 | How often the same pan can be reused across steps |
| **cross_step_reuse** | 0.15 | Whether the primary vessel is used for multiple steps |
| **pan_to_dish_ratio** | 0.15 | Ratio of pans used to servings produced |
| **clean_between** | 0.15 | Whether pans need washing between reuses |

**Anchors** — one-pan egg scramble (1), sheet pan dinner (2), pasta pot + sauce pan (4), stir fry wok + rice pot + steamer (6), full thanksgiving dinner (10)

---

### `social.json`

Recipe-level social and community metrics (not a 1–10 scale — uses tiers and counts):

| Metric | Description |
|--------|-------------|
| **followers** | Users following the recipe author; tiers from Newcomer (0–49) to Celebrity (250k+) |
| **forks** | Times a recipe was copied and modified; tracks fork type (adaptation, variation, dietary conversion, port, improvement) and source recipe |
| **stars** | Users who bookmarked the recipe; tiers from Unnoticed (0–9) to Legendary (10k+) |
| **thumbs_up** | Approval rating as a percentage with confidence levels based on sample size |

**Composite scores**:

- **popularity** — `normalize(stars) × 0.40 + positive_rate_weighted × 0.35 + normalize(total_ratings) × 0.25`
- **influence** — `normalize(fork_count) × 0.50 + normalize(follower_count) × 0.25 + normalize(fork_descendants) × 0.25`

---

## Coaching Files

These JSON files are designed for nutritionists, fitness coaches, and wellness professionals who use the scoring datasets above to guide clients toward healthier, easier, and goal-appropriate meals.

---

### `coaching_profiles.json`

Defines coaching personas that a professional can adopt, each with distinct focus areas and dimension weightings:

| Profile | Primary Focus | Key Dimensions |
|---------|--------------|----------------|
| **nutritionist** | Dietary quality, micronutrients, long-term health | health (0.35), satiety (0.20), ingredients (0.15) |
| **fitness_coach** | Meal timing, protein, energy for training | satiety (0.30), health (0.25), time_to_cook (0.15) |
| **meal_prep_coach** | Batch efficiency, cleanup, scalability | time_to_cook (0.20), pan_efficiency (0.18), cleanup_difficulty (0.17) |
| **wellness_coach** | Holistic health, stress reduction, low-complexity | health (0.30), satiety (0.20), cooking_steps (0.12), technicality (0.12) |

Each profile includes:
- **primary_dimensions** — weighted scoring dimensions for recipe ranking
- **recommendation_thresholds** — max/min dimension scores for recommending recipes
- **client_tiers** — beginner / intermediate / advanced with tighter thresholds for newer clients
- **typical_goals** — links to `dietary_goals.json` keys

---

### `dietary_goals.json`

Defines dietary and health goals with nutritional targets and dimension constraints:

| Goal | Key Constraints |
|------|----------------|
| **weight_loss** | health ≤ 4, satiety ≥ 6, technicality ≤ 4 |
| **muscle_gain** | satiety ≥ 5, output_yield ≥ 4, health ≤ 5 |
| **heart_health** | health ≤ 3, satiety ≥ 5, reproducibility ≤ 5 |
| **diabetes_management** | health ≤ 3, satiety ≥ 6, reproducibility ≤ 4 |
| **anti_inflammatory** | health ≤ 3, ingredients ≤ 6 |
| **endurance_fueling** | health ≤ 4, output_yield ≥ 4, time_to_cook ≤ 5 |
| **gut_health** | health ≤ 3, ingredients ≤ 5, reproducibility ≤ 4 |
| **stress_reduction** | technicality ≤ 3, cooking_steps ≤ 3, cleanup ≤ 3 |
| **budget_optimization** | output_yield ≥ 4, satiety ≥ 5, ingredients ≤ 4 |
| **family_meal_planning** | satiety ≥ 5, output_yield ≥ 5, pan_efficiency ≤ 4 |
| **general_wellness** | health ≤ 4, satiety ≥ 5, reproducibility ≤ 4 |
| **sleep_optimization** | health ≤ 3, satiety 5–7, technicality ≤ 3 |

Each goal includes `target_macros`, `caloric_target`, `dimension_constraints` with rationale, and `coaching_strategy`.

---

### `meal_recommendations.json`

Provides recommendation logic connecting dimension scores to coaching decisions:

- **recommendation_thresholds** — Four tiers (Easy / Moderate / Challenging / Advanced) with dimension score ranges that determine which recipes to show which clients
- **meal_plan_templates** — Structured weekly and monthly plans:
  - *Weight Loss Quick Week* — high satiety, low time, easy recipes
  - *Athlete Fueling Week* — timed around training, moderate complexity
  - *Beginner Cook Month* — progressive 4-week skill-building plan
  - *Heart Health Weekly* — low sodium, high fiber, reliable recipes
  - *Sunday Meal Prep* — batch-oriented, high yield, low cleanup
- **substitution_strategies** — How to adjust a recipe when dimension scores exceed a client's thresholds (reduce complexity, improve health, reduce time, reduce cleanup)
- **conflict_resolution** — Rules for handling goal conflicts (e.g., healthy but time-consuming, easy but boring)

---

### `skill_building_paths.json`

Defines progressive cooking skill paths with milestones tied to scoring dimensions:

**Skill Levels** (from novice to expert):
- **Novice** (technicality 1–2) — boiling water, basic knife safety, simple salads
- **Beginner** (2–3) — sauteing, roasting, pasta cooking, basic seasoning
- **Intermediate** (3–5) — braising, pan sauces, flavor layering, batch cooking
- **Advanced Intermediate** (5–7) — yeast dough, risotto, custards, compound butter
- **Advanced** (7–8) — laminated dough, tempering chocolate, sous vide, fermentation
- **Expert** (8–10) — molecular gastronomy, advanced butchery, sugar work, recipe development

**Progression Paths:**
- *Quick Weeknight Mastery* — 4 milestones from one-pan basics to 10+ recipe rotation
- *Health-Focused Cooking* — 4 milestones from nutrition basics to recipe modification
- *Technique Building* — 6 milestones from stovetop fundamentals to showpiece skills
- *Family Cooking Path* — 4 milestones from kid-friendly basics to family meal prep

Each milestone includes duration, dimension constraints, graduation criteria, and coaching approach.

---

### `coaching_tips.json`

Actionable coaching messages indexed by dimension and score range. For each of the 8 dimensions (technicality, time_to_cook, health, cooking_steps, cleanup_difficulty, ingredients, satiety, reproducibility, pan_efficiency, sections), the file provides:

- **coaching_message** — What the coach should communicate to the client
- **client_encouragement** — Motivational language for the client
- **preparation_tips** / **common_mistakes** / **nutrition_highlights** — Contextual advice
- **healthier_swaps** — Substitution suggestions (in the health dimension)

Score ranges are binned (1–2, 3–4, 5–6, 7–8, 9–10) with appropriate guidance at each level, enabling coaches to give targeted, dimension-aware advice.