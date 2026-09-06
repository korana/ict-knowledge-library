# FVG Setup Checklist

**Category:** 06-fair-value-gaps
**Aliases:** FVG checklist, FVG trade filter, FVG-Checklist
**ICT Confidence:** community-attributed
**Year Introduced:** 2026
**Year Refined:** 2026
**Source IDs:** THAI-COMMUNITY-2026-FVG
**Tags:** fvg, checklist, displacement, mss, community-attributed

## Definition

The FVG Setup Checklist is a **3-part pre-condition filter** this community source applies before treating any [fair-value-gap](fair-value-gap.md) as tradeable: a Fair Value Gap alone is not enough — it must sit inside a specific sequence of prior liquidity and structure events. All three components are individually ICT-original concepts already documented elsewhere in this library; this file's contribution is the author's specific **ordering and combination** of them into one filter, not the components themselves.

## Formal Criteria

An FVG qualifies for this checklist only if, in this order:

1. **Sweep Liquidity** — price first runs a liquidity pool (old high/low, session high/low, or [buy-side](../02-liquidity/buy-side-liquidity.md)/[sell-side](../02-liquidity/sell-side-liquidity.md) liquidity) via a [liquidity-sweep](../02-liquidity/liquidity-sweep.md).
2. **Displacement (Imbalance)** — the reversal off that sweep is a genuine [displacement](../09-displacement/displacement-definition.md) candle, leaving an FVG behind.
3. **Market Structure Shift** — the same displacement move breaks a prior swing point, per [mss](../01-market-structure/mss.md).

The FVG used for entry is the one created by the displacement candle in step 2. If any of the three steps is missing — no prior sweep, no real displacement (just drift), or no structural break — this source treats the FVG as lower-conviction and outside this checklist's scope.

## Formula / Math

```
fvg_setup_valid(fvg) :=
    prior_liquidity_sweep_occurred
    AND fvg.origin_candle == genuine_displacement_candle   # see displacement-definition
    AND mss_confirmed_by_same_move                          # see mss

# if any term is false, the FVG does not pass this checklist
# (it may still be a valid FVG per fair-value-gap.md — just not
#  a qualifying entry under this source's filter)
```

## Machine-Readable

```json
{
  "id": "fvg-setup-checklist",
  "category": "06-fair-value-gaps",
  "aliases": ["fvg-checklist", "fvg-trade-filter"],
  "criteria": [
    {"id": "c1", "expr": "prior_liquidity_sweep_occurred == true"},
    {"id": "c2", "expr": "displacement_candle_present == true"},
    {"id": "c3", "expr": "mss_confirmed_by_same_move == true"}
  ],
  "timeframes": ["M15","H1","H4","D"],
  "confidence": "community-attributed",
  "year_introduced": "2026",
  "year_refined": "2026",
  "related": ["fair-value-gap","liquidity-sweep","displacement-definition","mss","mss-vs-choch","unicorn-model","three-drive-pattern"],
  "sources": ["THAI-COMMUNITY-2026-FVG"]
}
```

## Visual Pattern

```
   FVG Setup Checklist (bullish):

   ☐ Sweep Liquidity?           [price wicks below Old Low / SSL, then reverses]
   ☐ Displacement present?      [Marubozu/Engulfing candle breaks back up through prior structure]
   ☐ MSS confirmed?             [break closes above the most recent Lower High]
   ☐ FVG formed by that candle? [gap between candle n-1 high and candle n+1 low]

   All checked → the FVG is a qualifying entry per this checklist.
```

## Timeframes

M15+. The source applies this on the timeframe where the MSS itself occurs; entries can be refined on a lower TF inside the qualifying FVG.

## Examples

**Example 1 — qualifying bullish FVG:**
- Price sweeps a prior session's Old Low (Sellside Liquidity taken).
- Next candle is a wide-body Marubozu closing back above the most recent Lower High — Displacement + MSS in the same candle.
- The FVG this candle leaves behind qualifies under all 3 checklist items.

**Example 2 — FVG that fails the checklist:**
- Price drifts up through a range, printing a small FVG along the way — no prior liquidity sweep, no structural break, gradual candles (not displacement).
- Still a valid FVG per [fair-value-gap](fair-value-gap.md)'s Formal Criteria, but this source treats it as a weaker, non-checklist entry.

## Common Mistakes

- **Trading any FVG without checking the sequence.** An FVG that formed without a prior sweep or without breaking structure is still technically an FVG, but this source treats it as materially lower-conviction.
- **Confusing this with [unicorn-model](../31-models/unicorn-model.md).** The Unicorn Model is a different, ICT-adjacent 4-part confluence stack (breaker + nested FVG + HTF bias + prior sweep) built around a breaker/FVG overlap. This checklist is a simpler 3-step sequence (sweep → displacement/FVG → MSS) from a different source, with no breaker-block requirement. Don't merge the two frameworks.
- **Confusing this with [three-drive-pattern](../01-market-structure/three-drive-pattern.md).** Three Drive's entry trigger is the same sweep + displacement + FVG triad, cited from the same author's later chapter — the difference is upstream: Three Drive additionally requires a three-leg approach structure into an Old High/Low before that trigger applies. A qualifying triad with no prior multi-drive approach is this checklist, not a Three Drive entry.
- **Treating this as an ICT-published checklist.** The three components (sweep, displacement, MSS) are each ICT-original; this specific ordered combination and the "checklist" framing are this community source's own synthesis.

## ICT vs Community

ICT teaches Sweep Liquidity, Displacement, and Market Structure Shift as separate, ICT-original concepts (see their individual files) — none of the three components is community-attributed on its own. What ICT does not publish is this specific 3-item ordered checklist that gates FVG entries on all three occurring together in sequence. This source's author packages the combination as an explicit "FVG Setup Checklist," presented as his own operational filter derived from applying ICT's individual concepts, not as an ICT-published requirement. Treat each component as ICT-original (high confidence, per its own file) and this specific checklist packaging as community-attributed.

## Related Concepts

- [fair-value-gap](fair-value-gap.md) — the object being filtered.
- [liquidity-sweep](../02-liquidity/liquidity-sweep.md) — checklist step 1.
- [displacement-definition](../09-displacement/displacement-definition.md) — checklist step 2.
- [mss](../01-market-structure/mss.md), [mss-vs-choch](../01-market-structure/mss-vs-choch.md) — checklist step 3.
- [unicorn-model](../31-models/unicorn-model.md) — a different, superficially similar confluence checklist; see Common Mistakes.
- [three-drive-pattern](../01-market-structure/three-drive-pattern.md) — same trigger triad, gated on a prior three-leg approach structure; see Common Mistakes.

## Citations

- `THAI-COMMUNITY-2026-FVG` — "FVG Setup Checklist," pp. 87–88.
