# Weekly Quarters

**Category:** 22-quarterly-theory
**Aliases:** weekly days, days-of-week QT
**ICT Confidence:** high
**Year Introduced:** 2023
**Year Refined:** 2026
**Source IDs:** ICT-2023-QUARTERLY-THEORY, THAI-COMMUNITY-2026-STD-PROJECTION, THAI-COMMUNITY-2026-DAILY-WEEKLY-PROFILE
**Tags:** quarterly-theory, weekly

## Definition

Weekly Quarters split each trading week into **four day-periods** mapped to AMD-X: Monday (Q1, A), Tuesday (Q2, M), Wednesday (Q3, D), Thursday (Q4, X), with Friday treated as a closing/continuation day outside the canonical 4-quarter map. This is the **most-traded QT scale for day-traders** — many setups gain conviction from being aligned with weekly-Q3 (Wednesday distribution).

## Formal Criteria

The weekly map:

| Day | Quarter | Phase | Typical character |
|---|---|---|---|
| Monday | Q1 | Accumulation | tight range; PWL/PWH often respected; "Monday range" forms |
| Tuesday | Q2 | Manipulation | sweep PWL or PWH (which one depends on weekly bias); week's manipulation move |
| Wednesday | Q3 | Distribution | major directional move; weekly HOD/LOD often set |
| Thursday | Q4 | X | continuation or reversal |
| Friday | (closing) | profit-taking | week's structure often resolves |

**Thursday closing-time caution (community-attributed):** a 2026 community source instructs closing any profitable position **before ~23:00 Thai time (GMT+7)** on Thursday — roughly **11:00–12:00 NY**, depending on DST (see [dst-handling](../04-time-cycles/dst-handling.md)) — because past that point price is often already at (or near) the week's low or high. This is a specific operational instant inside the Q4/X window above, not a new phase.

**Friday mechanic (community-attributed):** see [tgif-weekly-po3](../31-models/tgif-weekly-po3.md) for a specific, named Friday setup — a Thursday-liquidity sweep lining up with a weekly/daily HTF FVG, retraced into during the London Killzone — that this table's Friday row previously left unelaborated. Backtested by its source but explicitly not yet used live; confidence set accordingly on that file. A later chapter by the same author states more generally that **Monday and Friday should not be traded** (Friday range is typically a tight 400–500 point band, and the week's overall move tends to retrace 20–30% of its full travel on Friday) — this is a broader "don't trend-trade Friday" caution, not in conflict with TGIF's narrower claim of one specific retracement setup existing inside that same quiet day; see the reconciliation note on [tgif-weekly-po3](../31-models/tgif-weekly-po3.md).

**Weekly shape taxonomy (community-attributed):** the Mon-Tue-Wed-Thu default this table describes fits roughly half of all weeks (see Common Mistakes below); see [weekly-profile-patterns](weekly-profile-patterns.md) for six named alternate shapes covering the rest.

Common adage: "Tuesday lows on bullish weeks, Tuesday highs on bearish weeks" — referring to the manipulation-direction sweep; this is [weekly-profile-patterns](weekly-profile-patterns.md)'s Pattern #1 (Classic Tuesday Low/High of Week).

## Formula / Math

```
weekly_quarters:
    Monday    (Q1, A)
    Tuesday   (Q2, M)
    Wednesday (Q3, D)
    Thursday  (Q4, X)
    Friday    (closing, separate)
```

## Machine-Readable

```json
{
  "id": "weekly-quarters",
  "category": "22-quarterly-theory",
  "aliases": ["weekly-days", "days-of-week-QT"],
  "criteria": [
    {"id": "c1", "expr": "Mon=Q1(A), Tue=Q2(M), Wed=Q3(D), Thu=Q4(X)"},
    {"id": "c2", "expr": "Friday closing day, separate from QT structure"}
  ],
  "timeframes": ["H1","H4","D"],
  "confidence": "high",
  "year_introduced": "2023",
  "year_refined": "2023",
  "related": ["quarterly-theory-overview","monthly-quarters","daily-quarters","htf-amd","tgif-weekly-po3","weekly-profile-patterns"],
  "sources": ["ICT-2023-QUARTERLY-THEORY","THAI-COMMUNITY-2026-STD-PROJECTION","THAI-COMMUNITY-2026-DAILY-WEEKLY-PROFILE"]
}
```

## Visual Pattern

```
   weekly AMD-X:

   Mon   | Tue   | Wed   | Thu   | Fri
   Q1(A) | Q2(M) | Q3(D) | Q4(X) | close
   range   sweep   major   cont/   week
   build   PWL/H   move    rev     resolve
```

## Timeframes

H1 / H4 / D.

## Examples

**Example 1 — clean weekly MMBM:**
- Mon: 50-pip range, tight (Q1, A).
- Tue: wicks 1.0815 (PWL SSL swept) at London open, reverses (Q2, M).
- Wed: 130-pip rally, takes PWH 1.0985 (Q3, D).
- Thu: extends to 1.1010, then consolidates (Q4, X).
- Fri: closes 1.0995 (closing day).

## Common Mistakes

- **Forcing every week into Mon-Tue-Wed-Thu pattern.** ~50% of weeks follow it; macro events / news shift the rhythm.
- **Skipping Tuesday context.** A clean Tuesday manipulation is often the highest-conviction setup window of the week.

## Related Concepts

- [quarterly-theory-overview](quarterly-theory-overview.md), [monthly-quarters](monthly-quarters.md), [daily-quarters](daily-quarters.md), [htf-amd](../12-power-of-three/htf-amd.md).
- [tgif-weekly-po3](../31-models/tgif-weekly-po3.md) — the Friday-specific mechanic this table's Friday row was missing.
- [weekly-profile-patterns](weekly-profile-patterns.md) — six named alternate weekly shapes for the ~50% of weeks that don't fit this table's default.

## Citations

- `ICT-2023-QUARTERLY-THEORY`.
- `THAI-COMMUNITY-2026-STD-PROJECTION` — TGIF, the Friday mechanic cross-linked above, pp.534–543.
- `THAI-COMMUNITY-2026-DAILY-WEEKLY-PROFILE` — Thursday closing-time caution and Monday/Friday "don't trade" guidance, pp.563–565.
