# Top-Down Analysis

**Category:** 25-htf-bias
**Aliases:** TDA, top-down, multi-TF analysis, HTF-to-LTF read
**ICT Confidence:** high
**Year Introduced:** 2017
**Year Refined:** 2026
**Source IDs:** ICT-2017-CHARTER-OVERVIEW, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-ORDER-BLOCK, THAI-COMMUNITY-2026-LIQUIDITY-TRADING
**Tags:** top-down, multi-tf, framework

## Definition

Top-down analysis is ICT's **prescribed analysis sequence**: start from the highest-relevant TF (typically monthly), descend through weekly, daily, H4, H1 to the entry TF (M15 / M5). Each TF's bias and structural context conditions the lower TF's read. Top-down is the practical implementation of [htf-bias-framework](htf-bias-framework.md). The "down" direction is non-negotiable — analyzing M5 first and projecting upward produces backward-fitted bias.

## Formal Criteria

The standard 6-step top-down sequence:

1. **Monthly:** dealing range, EQ side, last external break.
2. **Weekly:** same checks within monthly context.
3. **Daily:** same within weekly context; identify today's DOL.
4. **H4:** confirm or refine daily; identify the active HTF PD array.
5. **H1:** entry zone setup confirmation.
6. **M15 / M5:** entry trigger (FVG, MSS, OB at the H1-or-better PD array).

Each step inherits the previous step's bias as a constraint. If TF n's bias conflicts with TF n-1's, flag the conflict and reduce conviction.

**Discrete skip-a-rung pairing table (community-attributed):** rather than the adjacent-step ladder above, a 2026 community source pairs an already-identified HTF Order Block ("POI") directly with a specific entry timeframe, skipping intermediate rungs:

| Higher Timeframe (POI) | Lower Timeframe (Entry) |
|---|---|
| Weekly | 4 Hour |
| Daily | 1 Hour |
| 4 Hour | 30 Minute / 15 Minute |
| 1 Hour | 15 Minute |

This is an alternative convention for OB-specific entries, not a correction to the 6-rung ladder above — see [order-block-trading-framework](../07-order-blocks/order-block-trading-framework.md) for the full pipeline this table belongs to.

**Major / Medium / Minor Liquidity tiers (community-attributed):** another 2026 community source names the same TF-banding idea from the liquidity side instead of the entry-pipeline side — swing highs/lows on Session/Daily/Weekly/Monthly are "Major Liquidity," on 15m/1H "Medium Liquidity," and on 1m/5m "Minor Liquidity." The source states outright that this is the same Top-Down Analysis principle applied to liquidity levels rather than to entries, and restates the requirement that the paired TFs stay at least one full step apart (e.g. HTF=Weekly/LTF=H4, or HTF=H4/LTF=M30/M15) — no new pairing rule, just a liquidity-specific vocabulary for the existing ladder. See [buy-side-liquidity](../02-liquidity/buy-side-liquidity.md) and [sell-side-liquidity](../02-liquidity/sell-side-liquidity.md) for the underlying liquidity-pool mechanics these tiers classify.

## Formula / Math

```
top_down_analysis():
    for tf in [MN, W, D, H4, H1, M15, M5]:
        bias[tf]      = read_bias(tf)
        structure[tf] = read_structure(tf)
        constraints[tf] = constraints[tf-1] + this_tf_constraints
        if conflict_with_higher_TFs:
            flag_conflict()
    return entry_setup_filtered_by_all_constraints
```

## Machine-Readable

```json
{
  "id": "top-down-analysis",
  "category": "25-htf-bias",
  "aliases": ["TDA", "top-down", "multi-tf-analysis"],
  "criteria": [
    {"id": "c1", "expr": "analysis_sequence_starts_at_highest_TF"},
    {"id": "c2", "expr": "each_TF_inherits_higher_TF_constraints"},
    {"id": "c3", "expr": "entry_TF_is_last_step"}
  ],
  "timeframes": ["M5","M15","H1","H4","D","W","MN"],
  "confidence": "high",
  "year_introduced": "2017",
  "year_refined": "2026",
  "related": ["htf-bias-framework","monthly-bias","weekly-bias","daily-bias","bias-confluence","bias-invalidation","htf-pd-array-hierarchy","order-block-trading-framework","buy-side-liquidity","sell-side-liquidity"],
  "sources": ["ICT-2017-CHARTER-OVERVIEW","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-ORDER-BLOCK","THAI-COMMUNITY-2026-LIQUIDITY-TRADING"]
}
```

## Visual Pattern

```
   top-down analysis funnel:

   MN  ────  bullish, in discount, monthly DOL upside
       ↓
   W   ────  bullish, just had CHoCH up
       ↓
   D   ────  bullish, current range 1.0820-1.0950, targeting PWH
       ↓
   H4  ────  bullish OB at 1.0840-1.0850 (the entry zone)
       ↓
   H1  ────  inside H4 OB; bullish FVG at 1.0843-1.0847
       ↓
   M5  ────  entry trigger: FVG CE retest with bullish wick

   → entry: M5 long at 1.0845
   → SL beyond H1 OB low at 1.0838
   → TP at HTF DOL (PWH 1.0985)
```

## Timeframes

M5 → MN (full ladder).

## Examples

**Example 1 — full top-down for a swing-day setup:**
- MN: bullish, current 1.0850 in MN discount.
- W: bullish, current week's PWL at 1.0820 already swept Mon morning.
- D: bullish, today's range building 1.0830-1.0865; targeting PDH 1.0925.
- H4: bullish, OB at 1.0830-1.0840 (today's discount).
- H1: bullish FVG forming at 1.0833-1.0838.
- M5: 09:55 NY macro: SSL sweep + bullish CHoCH + FVG retest.
- → entry trigger valid; long 1.0838, SL 1.0826, target PDH.

## Common Mistakes

- **Bottom-up analysis.** Reading M5 first and projecting up produces a confirmation-biased read; always go top-down.
- **Skipping HTF in fast markets.** When session is moving, the temptation is "no time for top-down" — but skipping HTF is precisely when bias mistakes happen.
- **Treating each TF as independent.** Each TF inherits constraints from above; an isolated H1 bullish setup against a monthly bearish backdrop is risky.
- **Conflating the 6-rung ladder with the skip-a-rung pairing table.** The ladder above sets bias across every TF in sequence; the community pairing table (Weekly→4H, Daily→1H, etc.) is a narrower OB-entry-specific convention that deliberately skips intermediate TFs — don't treat them as the same tool.

## Related Concepts

- [htf-bias-framework](htf-bias-framework.md), [monthly-bias](monthly-bias.md), [weekly-bias](weekly-bias.md), [daily-bias](daily-bias.md), [bias-confluence](bias-confluence.md), [bias-invalidation](bias-invalidation.md), [htf-pd-array-hierarchy](../05-pd-arrays/htf-pd-array-hierarchy.md).
- [order-block-trading-framework](../07-order-blocks/order-block-trading-framework.md) — uses the skip-a-rung pairing table for OB-specific entries.
- [buy-side-liquidity](../02-liquidity/buy-side-liquidity.md), [sell-side-liquidity](../02-liquidity/sell-side-liquidity.md) — Major/Medium/Minor Liquidity tiers restate this file's TF-pairing rule from the liquidity side.

## Citations

- `ICT-2017-CHARTER-OVERVIEW`, `ICT-2022-MENTORSHIP-OVERVIEW`.
- `THAI-COMMUNITY-2026-ORDER-BLOCK` — discrete HTF/LTF pairing table, p.205.
- `THAI-COMMUNITY-2026-LIQUIDITY-TRADING` — Major/Medium/Minor Liquidity TF tiers, citing ICT Mentorship 2022 for the Major tier, pp.314–316.
