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