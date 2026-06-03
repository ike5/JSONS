# JSONS

A collection of structured JSON datasets for kitchen and recipe-related reference data.

The scoring system is built around **7 atomic recipe metrics** designed to be the spokes of a
multidimensional filter mesh — each one answers a single, intuitive question a person actually
asks when deciding whether to cook something.

## Metrics

| Metric | File | Unit / Scale | Answers |
|--------|------|--------------|---------|
| **time_to_cook** | `time_to_cook.json` | minutes → 1–10 axis | How long, start to plate? |
| **steps** | `steps.json` | count → 1–10 axis | How many steps? |
| **ingredients** | `ingredients.json` | count → 1–10 axis | How many ingredients? |
| **cleanup** | `cleanup.json` | 1–10 | How big is the mess? |
| **nutrition** | `nutrition.json` | per-serving values (+ optional 1–10 axis) | Is it nutritious? |
| **reproducibility** | `reproducibility.json` | 1–10 (crowd-sourced) | Will mine turn out like the original? |
| **cost** | `cost.json` | currency → 1–10 axis | What will it cost me? |

All 1–10 axes share one orientation: **higher = more (more time, more steps, more cleanup, less
healthy, harder to reproduce, more expensive)**, so a single drag direction on the mesh reads
consistently across spokes.

---

### `time_to_cook.json`

Total time to make the recipe, accounting for time reclaimed by running steps in parallel.

| Dimension | Description |
|-----------|-------------|
| **prep_time** | Minutes preparing ingredients before cooking |
| **cook_time** | Minutes actively cooking |
| **parallel_savings** | Minutes reclaimed by overlapping steps (subtracted) |

`effective_minutes = max(0, prep_time + cook_time - parallel_savings)`, mapped to a 1–10 axis.

---

### `steps.json`

A simple count of discrete steps. Parallel/simultaneous steps are counted individually, since even
"simple" recipes can hide 20+ steps in a single section. Raw count mapped to a 1–10 axis.

---

### `ingredients.json`

A simple count of distinct ingredients — nothing else. Raw count mapped to a 1–10 axis.

---

### `cleanup.json`

How much cleanup a recipe creates, rolled up from the tools it uses (equipment requirements live
here too). The file keeps a large per-tool reference table (`items`) grouped into utensils,
cookware, dishware, delicate/specialty, large/bulky, and notoriously difficult — each with a
`difficulty` (wash difficulty) and a per-tool breakdown.

Recipe-level rollup inputs:

| Input | Description |
|-------|-------------|
| **tool_count** | Number of distinct tools the recipe uses |
| **wash_events** | Times each tool must be washed (a cutting board used for raw meat then produce = 2; a tool reused without washing between = 1) |
| **wash_difficulty** | Per-tool wash difficulty from the `items` table (a pan is harder than a spoon) |

`cleanup_score = scale_to_10( Σ over distinct tools ( wash_difficulty × wash_events ) )`. A tool
shared across steps is counted once unless it must be washed between uses — so reuse lowers the score.

---

### `nutrition.json`

Per-serving nutritional values. Core fields are always present; additional fields are captured when
the nutrition data API provides them.

- **calories_per_serving** (kcal)
- **macros** — protein, fat, sugar, fiber (g)
- **glycemic_index** (0–100) — important for diabetic users
- **optional_fields** — sodium, carbs, saturated fat, micronutrients, glycemic load, etc.

An optional derived **mesh_axis** maps these to a 1–10 healthiness score (1 = healthiest), or the
front-end can filter on any raw field directly (e.g. a calories slider, a glycemic_index cap).

---

### `reproducibility.json`

**Crowd-sourced.** Populated by users who attempted the recipe and rated how closely their result
matched the original.

| Dimension | Description |
|-----------|-------------|
| **taste_match** | How closely the result tasted like the original (1–10) |
| **visual_match** | How closely it looked like the original (1–10) |

`reproducibility = 11 - weighted_average(taste_match, visual_match)`, so higher submitted matches
produce a lower (easier-to-reproduce) score. Includes a submission schema and a confidence tier
based on number of submissions.

---

### `cost.json`

Author-provided estimated cost for the recipe's stated number of servings. `cost_per_serving =
estimated_total / servings`, and the serving calculator scales it to any requested serving count.
`cost_per_serving` maps to a 1–10 axis.

---

## Coaching Files

These files are designed for nutritionists, fitness coaches, and wellness professionals who use the
metrics above to guide clients toward healthier, easier, goal-appropriate meals. They reference the
7 metrics above.

- **`coaching_profiles.json`** — coaching personas (nutritionist, fitness_coach, meal_prep_coach,
  wellness_coach) with weighted `primary_dimensions` (normalized to 1.0), recommendation thresholds,
  and beginner/intermediate/advanced client tiers.
- **`dietary_goals.json`** — dietary goals (weight_loss, heart_health, diabetes_management, etc.)
  with target macros, caloric targets, and metric-based `dimension_constraints`.
- **`meal_recommendations.json`** — recommendation tiers (Easy → Advanced), weekly/monthly meal-plan
  templates, substitution strategies (with per-metric `dimension_impact`), and conflict-resolution rules.
- **`skill_building_paths.json`** — progressive skill levels (novice → expert) and progression paths
  (quick weeknight, health-focused, technique building, family cooking) with milestones tied to metrics.
- **`coaching_tips.json`** — actionable coaching messages indexed by metric and score range
  (1–2, 3–4, 5–6, 7–8, 9–10), including the crowd-sourced reproducibility scale and cost guidance.
