# Redelivery Rebalance (RDRB)

**Category:** 06-fair-value-gaps
**Aliases:** RDRB, Re-Delivery Re-Balance, +RDRB, -RDRB
**ICT Confidence:** community-attributed
**Year Introduced:** 2026
**Year Refined:** 2026
**Source IDs:** THAI-COMMUNITY-2026-FVG-TECHNIQUE
**Tags:** fvg, rdrb, repricing, balance, community-attributed

## Definition

A **Redelivery Rebalance (RDRB)** is a 3-candle repricing pattern this source presents as a newer addition to its FVG taxonomy (dated by the author to "around 2023"). It occurs during a strong, continuous directional run — similar in setting to a [liquidity-void](../02-liquidity/liquidity-void.md) — but where price does **not** fully rebalance in the usual FVG sense. Across 3 consecutive candles, the middle candle (candle 2) has a wick exceeding 50% of its own range sitting inside what looks like a balance/consolidation pocket; the source uses the wick's starting point (candle 1) and the high/low of candle 3 as the two edges of the RDRB zone — comparable to how a normal FVG's boundaries are drawn from its outer candles. `+RDRB` forms in bullish continuation, `-RDRB` in bearish continuation.

## Formal Criteria

- Price is in a strong, continuous directional run (bullish for +RDRB, bearish for -RDRB).
- Three consecutive candles (1, 2, 3) are identified.
- Candle 2's wick, in the direction opposing the trend, exceeds 50% of candle 2's own high-low range.
- The zone is bounded by candle 1's extreme (start of the long wick) and candle 3's extreme (the far edge), similar to a standard FVG's boundary-drawing convention.
- An untested "Break Away Gap" (a BISI, for +RDRB, or SIBI, for -RDRB) sitting below (for +RDRB) or above (for -RDRB) the RDRB zone is optional confluence — if present and still untested, price is expected to stop at the RDRB and not need to reach the Break Away Gap.
- On a later retest, the RDRB zone is expected to act as support (+RDRB) or resistance (-RDRB).

## Formula / Math

```
rdrb_candidate(c1, c2, c3) :=
    strong_directional_run_context
    AND opposing_wick_pct(c2) > 0.5     # candle 2's counter-trend wick > 50% of its range
    AND zone := [c1.extreme, c3.extreme]

# +RDRB (bullish continuation): zone acts as support on retest
# -RDRB (bearish continuation): zone acts as resistance on retest
```

## Machine-Readable

```json
{
  "id": "redelivery-rebalance",
  "category": "06-fair-value-gaps",
  "aliases": ["RDRB", "re-delivery-re-balance", "+RDRB", "-RDRB"],
  "criteria": [
    {"id": "c1", "expr": "strong_directional_run_context == true"},
    {"id": "c2", "expr": "opposing_wick_pct(candle_2) > 0.5"},
    {"id": "c3", "expr": "zone_bounded_by_candle1_and_candle3_extremes == true"}
  ],
  "timeframes": ["M15","H1","H4","D"],
  "confidence": "community-attributed",
  "year_introduced": "2026",
  "year_refined": "2026",
  "related": ["fair-value-gap","liquidity-void","rejection-block","reaper-pd-array","balanced-price-range"],
  "sources": ["THAI-COMMUNITY-2026-FVG-TECHNIQUE"]
}
```

## Visual Pattern

```
   +RDRB (bullish continuation):

        ▲
        █  ← candle 3 (far edge of RDRB zone)
       ▲
       █   ← candle 2: long lower wick > 50% of its range
      ▓▓▓▓ +RDRB zone (candle 1 extreme to candle 3 extreme)
       █
      ▲
      █    ← candle 1 (start of the wick / near edge)
      ▼

   Zone later acts as support on retest.
```

## Timeframes

M15+. The source illustrates this mainly on H1/H4 and Daily continuation legs.

## Examples

**Example 1 — bullish +RDRB during a sustained rally (per source, pp.163–165):**
- Price rallies hard toward Buyside Liquidity without a normal FVG-style rebalance.
- Within the run, candle 1 opens the sequence; candle 2 prints a lower wick exceeding 50% of its own range inside what looks like a consolidation pocket; candle 3 continues the rally.
- The zone bounded by candle 1's low and candle 3's low is the +RDRB.
- An untested Break Away Gap (BISI) sits below the +RDRB, unreached — the source notes price often doesn't need to retrace that far and instead reacts at the +RDRB first.
- On the later pullback, price holds at the +RDRB zone rather than continuing down to the Break Away Gap.

## Common Mistakes

- **Confusing this with [rejection-block](../19-rejection-blocks/rejection-block.md).** Rejection Block is a single-candle wick-rejection pattern (≥60% wick) anchored to a pre-existing key level. RDRB is a 3-candle pattern where the wick belongs to the *middle* candle of the sequence and the zone is anchored to the outer two candles, not to an independent prior level.
- **Treating RDRB as a guaranteed stopping point.** The source frames the untested Break Away Gap beneath (or above) the RDRB as a fallback target if the RDRB itself fails to hold — RDRB is the first, not the only, reference.
- **Mistaking this for a standard FVG.** RDRB spans 3 candles like an FVG, but its criteria (opposing wick on the middle candle, formed inside a strong directional run) are distinct from the 3-candle non-overlapping-wick FVG definition.
- **Treating this as ICT-published terminology.** RDRB is this community source's own name and packaging; see `## ICT vs Community` below.

## ICT vs Community

The underlying mechanic — a directional run leaving a repricing zone the market later returns to for support/resistance — draws on ICT-original ideas about draws on liquidity and PD arrays generally. What ICT does not publish, per this source, is the specific "Redelivery Rebalance" pattern and name: a 3-candle, opposing-wick-on-the-middle-candle construction the author says entered common community usage "around 2023." The author cites no ICT lecture or timestamp for it. Treat the general repricing/PD-array concept as ICT-original context and this specific 3-candle RDRB construction and naming as community-attributed.

## Related Concepts

- [fair-value-gap](fair-value-gap.md) — the base 3-candle pattern RDRB visually resembles but differs from in construction.
- [liquidity-void](../02-liquidity/liquidity-void.md) — the directional-run context RDRB tends to form within.
- [rejection-block](../19-rejection-blocks/rejection-block.md) — a different single-candle wick-rejection pattern; see Common Mistakes.
- [reaper-pd-array](reaper-pd-array.md) — another technique from the same chapter/source.
- [balanced-price-range](balanced-price-range.md) — a different "balance" concept from the same broader FVG taxonomy.

## Citations

- `THAI-COMMUNITY-2026-FVG-TECHNIQUE` — "Redelivery Rebalance (RDRB)," pp. 163–167.
