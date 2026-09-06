# Silver Bullet — Overview

**Category:** 11-silver-bullet
**Aliases:** SB, silver bullet setup, ICT SB
**ICT Confidence:** high
**Year Introduced:** 2022
**Year Refined:** 2026
**Source IDs:** ICT-2022-SILVER-BULLET, ICT-2025-MACRO-PRECISION, ICT-2026-LONDON-SB-SHIFT, THAI-COMMUNITY-2026-SILVER-BULLET
**Tags:** silver-bullet, setup, foundational

## Definition

The Silver Bullet is one of ICT's most-cited named setups: a **60-minute window** during which a specific liquidity-sweep + displacement + FVG sequence has high probability of producing a tradeable move. ICT teaches three Silver Bullet windows per trading day, each tied to a specific session: London (02:00–03:00 NY, shifted from 03:00–04:00 in 2026 per liquidity-routing changes post-MiFID III — see [silver-bullet-london](silver-bullet-london.md)), NY AM (10:00–11:00 NY), and NY PM (14:00–15:00 NY). The setup is **time-and-pattern combined** — the time window matters as much as the pattern.

## Formal Criteria

The three Silver Bullet windows (NY time):

| Window | Time | Parent killzone | Probability rank |
|---|---|---|---|
| London | 02:00 – 03:00 | London Open KZ | Medium |
| NY AM | 10:00 – 11:00 | NY AM KZ + LDN-Close overlap | **Highest** |
| NY PM | 14:00 – 15:00 | NY PM KZ | Lowest |

*London window time is disputed for 2026 — a same-year community source states 03:00–04:00 instead; see [silver-bullet-london](silver-bullet-london.md)'s Time Conflict note. Not adopted here.*

Within any SB window, the operational sequence is:

1. **Liquidity sweep** — price takes a known pool (Asian range, lunch range, prior session high/low).
2. **Displacement** — strong directional candle in the bias direction.
3. **FVG forms** — inside or after the displacement.
4. **Entry on FVG retest** at CE (per 2025 default).
5. **SL** beyond the swept liquidity pool.
6. **Targets** via SD projections / DOL.

## Formula / Math

```
silver_bullet_window in [
  ("london", 02:00, 03:00),   # shifted from 03:00-04:00 in 2026
  ("ny_am", 10:00, 11:00),
  ("ny_pm", 14:00, 15:00),
]   # all NY time

silver_bullet_setup(window) :=
  in_window(now, window)
  AND HTF_bias_clear
  AND liquidity_sweep_just_occurred
  AND displacement_after_sweep_with_fvg
```

## Machine-Readable

```json
{
  "id": "silver-bullet-overview",
  "category": "11-silver-bullet",
  "aliases": ["SB", "silver-bullet-setup", "ICT-SB"],
  "criteria": [
    {"id": "c1", "expr": "time in [(02:00,03:00), (10:00,11:00), (14:00,15:00)] NY"},
    {"id": "c2", "expr": "sweep + displacement + FVG + retest sequence"},
    {"id": "c3", "expr": "HTF bias agreement"}
  ],
  "timeframes": ["M1","M5","M15"],
  "confidence": "high",
  "year_introduced": "2022",
  "year_refined": "2026",
  "related": ["silver-bullet-london","silver-bullet-ny-am","silver-bullet-ny-pm","silver-bullet-rules","silver-bullet-formalized-2025","silver-bullet-failure-modes","killzone-overview","macro-times-overview","ce-as-primary-entry","liquidity-sweep","displacement-definition"],
  "sources": ["ICT-2022-SILVER-BULLET","ICT-2025-MACRO-PRECISION","ICT-2026-LONDON-SB-SHIFT","THAI-COMMUNITY-2026-SILVER-BULLET"]
}
```

## Visual Pattern

```
   24h NY clock — 3 Silver Bullet windows:

   00 ─ 02 ─ 03 ─ 08 ─ 10 ─ 11 ─ 13:30 ─ 14 ─ 15 ─ 16 ─ 24
        ████ ←  London SB (shifted 2026)
                            ████ ←  NY AM SB (highest probability)
                                              ████ ←  NY PM SB
```

## Timeframes

M1 / M5 / M15. The window is 60 minutes; M5 is the natural execution TF.

## Examples

**Example 1 — bullish NY AM Silver Bullet:**
- HTF bullish; lunch low at 1.0902.
- 10:05 NY: M5 wicks 1.0900 (lunch SSL swept on the bullish-bias side), closes 1.0908.
- 10:15 NY: M5 displacement candle, 22-pip green, leaves bullish FVG at 1.0911–1.0915.
- 10:25 NY: pulls back to FVG CE at 1.0913. Long entry.
- SL below sweep low at 1.0898 (2-pip buffer). Risk = 15 pips.
- Target -1.5 SD or PDH BSL at 1.0942 → ~29 pips → ~2R. Extended target -2.0 SD at 1.0966 → ~3.5R.

## Sideways-Week Behavior (community-attributed)

A 2026 community source (`THAI-COMMUNITY-2026-SILVER-BULLET`) describes a **U-shape range pattern** during sideways weeks: over a 1–2 or 2–3 day consolidation, price often prints an extreme at a Silver Bullet window on one day, then returns to roughly the same level at the **same SB window exactly 24 hours later** — e.g. a Monday high set during the London SB (03:00–04:00 NY per that source) reappears at Tuesday's London SB. Illustrated with two GBPJPY 15m charts (23–25 Jan 2024); the source states no formal threshold (no tolerance band, no minimum consolidation length) — a behavioral tendency to watch for, not a formal criterion.

## Common Mistakes

- **Trading any sweep in any of the 3 windows.** The sweep direction must align with HTF bias; counter-bias SBs fail more often.
- **Skipping the macro check.** SB windows overlap with macro times (e.g., 10:00–10:10 macro is inside NY AM SB); macro-aligned SBs are higher conviction.
- **NY PM as default.** PM is the lowest-probability window; only take it when AM didn't deliver and the trend is clean.

## Related Concepts

- [silver-bullet-london](silver-bullet-london.md), [silver-bullet-ny-am](silver-bullet-ny-am.md), [silver-bullet-ny-pm](silver-bullet-ny-pm.md) — per-window deep dives.
- [silver-bullet-rules](silver-bullet-rules.md), [silver-bullet-formalized-2025](silver-bullet-formalized-2025.md), [silver-bullet-failure-modes](silver-bullet-failure-modes.md).
- [killzone-overview](../10-killzones/killzone-overview.md), [macro-times-overview](../04-time-cycles/macro-times-overview.md), [ce-as-primary-entry](../06-fair-value-gaps/ce-as-primary-entry.md), [liquidity-sweep](../02-liquidity/liquidity-sweep.md), [displacement-definition](../09-displacement/displacement-definition.md).

## Citations

- `ICT-2022-SILVER-BULLET` — three SB windows formalized in 2022 mentorship.
- `ICT-2025-MACRO-PRECISION` — SB execution timing refined in 2025.
- `ICT-2026-LONDON-SB-SHIFT` — London SB window shifted 03:00–04:00 → 02:00–03:00 NY.
- `THAI-COMMUNITY-2026-SILVER-BULLET` — U-shape sideways-week behavior; also restates the London window as 03:00-04:00, conflicting with the shift above (see [silver-bullet-london](silver-bullet-london.md)).
