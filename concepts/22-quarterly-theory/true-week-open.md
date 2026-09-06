# True Week Open (TWO)

**Category:** 22-quarterly-theory
**Aliases:** TWO, weekly true open, Sunday/Monday open
**ICT Confidence:** high
**Year Introduced:** 2017
**Year Refined:** 2026
**Source IDs:** ICT-2017-CHARTER-OVERVIEW, ICT-2023-QUARTERLY-THEORY, THAI-COMMUNITY-2026-DAILY-WEEKLY-PROFILE
**Tags:** quarterly-theory, true-week-open

## Definition

The **True Week Open (TWO)** is the **first traded price of the new trading week** — typically **Sunday 18:00 NY** (FX broker open) or **Monday 00:00 NY** depending on broker convention. TWO functions as a horizontal premium/discount reference for the entire week, the way TDO does for the day. ICT teaches TWO as a major weekly pivot: price above TWO = weekly premium (favor shorts in bearish weeks); price below TWO = weekly discount (favor longs in bullish weeks).

## Formal Criteria

- TWO = first traded price of the new week:
  - **18:00 NY Sunday** (most FX brokers).
  - **00:00 NY Monday** (some brokers / instruments).
  - Verify which the broker uses.
- Acts as horizontal weekly reference.
- Combines with TDO for layered intraday/weekly bias context.

**TWO/TDO interaction (community-attributed):** a 2026 community source gives a specific bullish-bias checkpoint — Wednesday's [true-day-open](true-day-open.md) (00:00 NY) should sit **above** the TWO for a buy bias to hold; TDO below TWO on Wednesday is a warning the bullish read is weakening. The same source gives an earlier, coarser version of the same check on Wednesday's session open itself (not the 00:00 NY TDO specifically): if Wednesday's session opens above the week's Monday open, bias the week to continue up; if below, bias it to continue down.

## Formula / Math

```
two = open_price_at_first_tick_of_new_week

# typical:
two = open at 18:00 NY Sunday (FX)
    OR open at 00:00 NY Monday (some FX / futures)

weekly_premium_vs_TWO := price > two
weekly_discount_vs_TWO := price < two
```

## Machine-Readable

```json
{
  "id": "true-week-open",
  "category": "22-quarterly-theory",
  "aliases": ["TWO", "weekly-true-open", "Sunday-Monday-open"],
  "criteria": [
    {"id": "c1", "expr": "first traded price of new week (broker-anchored)"},
    {"id": "c2", "expr": "horizontal weekly premium/discount reference"}
  ],
  "timeframes": ["H1","H4","D"],
  "confidence": "high",
  "year_introduced": "2017",
  "year_refined": "2023",
  "related": ["quarterly-theory-overview","weekly-quarters","true-day-open","time-of-day-pivots","sunday-open-gap","nwog","htf-bias-framework"],
  "sources": ["ICT-2017-CHARTER-OVERVIEW","ICT-2023-QUARTERLY-THEORY","THAI-COMMUNITY-2026-DAILY-WEEKLY-PROFILE"]
}
```

## Visual Pattern

```
   TWO as weekly pivot:

   weekly premium (above TWO)
   ───────── TWO (Sunday 18:00 NY) ─────────
   weekly discount (below TWO)

   weekly bullish + price below TWO = layered long-zone
   weekly bearish + price above TWO = layered short-zone
```

## Timeframes

H1 / H4 / D.

## Examples

**Example 1 — TWO + weekly bias:**
- Weekly bias bullish.
- TWO = 1.0858 (Sunday 18:00 NY open).
- By Wednesday: current price 1.0830 → weekly discount vs TWO.
- → swing long setups have TWO + weekly bias confluence.

## Common Mistakes

- **Wrong broker time.** Some brokers open 18:00 NY Sunday, others 22:00 NY Sunday, others 00:00 Monday. Verify.
- **Treating TWO as the weekly EQ.** TWO is the open, not the midpoint of the weekly range.

## Related Concepts

- [quarterly-theory-overview](quarterly-theory-overview.md), [weekly-quarters](weekly-quarters.md), [true-day-open](true-day-open.md), [time-of-day-pivots](../04-time-cycles/time-of-day-pivots.md), [sunday-open-gap](../31-models/sunday-open-gap.md), [nwog](../31-models/nwog.md), [htf-bias-framework](../25-htf-bias/htf-bias-framework.md).
- [weekly-profile-patterns](weekly-profile-patterns.md) — named weekly shapes several of which measure sweeps and reversals against TWO.

## Citations

- `ICT-2017-CHARTER-OVERVIEW`, `ICT-2023-QUARTERLY-THEORY`.
- `THAI-COMMUNITY-2026-DAILY-WEEKLY-PROFILE` — Wednesday TDO-vs-TWO bullish checkpoint and the coarser Wednesday-open-vs-Monday-open continuation rule, pp.562, 565.
