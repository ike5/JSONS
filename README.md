# JSONS

A collection of structured JSON datasets for kitchen-related reference data.

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
