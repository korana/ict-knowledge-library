# Retracement

**Category:** 01-market-structure
**Aliases:** pullback, throwback, price-delivery retracement
**ICT Confidence:** high
**Year Introduced:** 2018
**Year Refined:** 2026
**Source IDs:** ICT-2018-IPDA, ICT-2016-FVG-INTRO, THAI-COMMUNITY-2026-PRICE-DELIVERY
**Tags:** structure, retracement, fvg, liquidity-void, rebalance, ipda

## Definition

Retracement is the [Price Delivery Cycle](price-delivery-cycle.md) context in which price moves back into the price range it just vacated during [range-expansion](range-expansion.md), without breaking the origin of that displacement leg. ICT's framing differs from generic technical-analysis "pullback": a Retracement is not random profit-taking, it is price returning specifically to **rebalance** the [fair-value-gap](../06-fair-value-gaps/fair-value-gap.md) or [liquidity-void](../02-liquidity/liquidity-void.md) that the displacement candle(s) left behind, because that gap represents an inefficient (one-sided) print that the algorithm must correct before continuing. Once rebalanced, price is expected to resume the original directional [range-expansion](range-expansion.md) — this is what separates Retracement from [Reversal](price-delivery-cycle.md#formal-criteria), where price does not resume the original direction.

## Formal Criteria

- A displacement leg must have already occurred (an Expansion out of a prior Consolidation), producing at least one unmitigated FVG or Liquidity Void.
- Price closes back inside the price range of the displacement leg, moving opposite to the leg's direction.
- The retracement does not close beyond the origin of the displacement leg (the [equilibrium](../27-equilibrium/equilibrium-definition.md) of the prior Consolidation, or the Order Block it left behind) — if it does, this reclassifies as a [Reversal](price-delivery-cycle.md), not a Retracement.
- The entry zone of interest during a Retracement is the FVG / Liquidity Void itself, not an arbitrary Fibonacci ratio.

## Formula / Math

```
displacement_leg: origin O -> extreme E   (direction D)
FVG_or_LV: [g_low, g_high]  ⊂  range(O, E)

is_retracement(candle_close) :=
    candle_close moves opposite to D
    AND candle_close ∈ [g_low, g_high]      # touches/rebalances the gap
    AND candle_close does NOT cross O        # origin (prior EQ / OB) intact

is_reversal(candle_close) :=
    candle_close crosses O                   # origin breached → reclassify as Reversal
```

## Machine-Readable

```json
{
  "id": "retracement",
  "category": "01-market-structure",
  "aliases": ["pullback", "throwback"],
  "criteria": [
    {"id": "c1", "expr": "prior_displacement_leg_exists == true"},
    {"id": "c2", "expr": "close_enters_FVG_or_liquidity_void == true"},
    {"id": "c3", "expr": "close_does_not_cross_displacement_origin == true"}
  ],
  "timeframes": ["M5","M15","H1","H4","D"],
  "confidence": "high",
  "year_introduced": "2018",
  "year_refined": "2026",
  "related": ["price-delivery-cycle","range-expansion","fair-value-gap","liquidity-void","fvg-mitigation","equilibrium-definition","consequent-encroachment"],
  "sources": ["ICT-2018-IPDA","ICT-2016-FVG-INTRO","THAI-COMMUNITY-2026-PRICE-DELIVERY"]
}
```

## Visual Pattern

```
High ─────────●────────────────────────────
             ╱ ╲
            ╱   ╲          ┌─ FVG/Liquidity Void
           ╱     ╲         │  left by displacement
          ╱       ●────────┘
 origin ●╱         ╲
                     ╲___________●  ← Retracement: closes back
                                      into the gap, then resumes up
Low ─────────────────────────────────────────
        (Expansion)   (Retracement)   (Expansion resumes)
```

## Timeframes

M5 → D. Retracements on HTF (D/H4) can take days to complete; on LTF (M5/M15) they often complete within one session and are the primary entry mechanism for intraday continuation setups.

## Examples

**Example 1 — bullish continuation via Retracement:**
- EURUSD displaces upward out of the Asian range, leaving a bullish FVG at 1.0820–1.0835.
- Price pulls back and closes at 1.0828 (inside the FVG) without trading back below the Asian-range equilibrium.
- → Retracement confirmed. Expect Expansion to resume upward toward the next liquidity target.

## Common Mistakes

- **Treating any pullback as a Retracement.** If price closes back through the origin of the displacement leg (the prior Consolidation's equilibrium or Order Block), it has become a Reversal, not a Retracement — the forward bias flips.
- **Entering on Fibonacci ratios instead of the FVG/Liquidity Void.** ICT's Retracement entry zone is the specific inefficiency left by the displacement candle(s), not a generic 50%/61.8% level (though EQ often coincides with 50%).
- **Ignoring which type of gap formed.** A [delayed-rebalance-fvg](../06-fair-value-gaps/delayed-rebalance-fvg.md) may not be revisited for many bars; don't assume every Expansion is immediately followed by a Retracement.

## Related Concepts

- [price-delivery-cycle](price-delivery-cycle.md) — the state machine this concept is a branch of.
- [range-expansion](range-expansion.md) — the leg that produces the gap a Retracement fills.
- [fair-value-gap](../06-fair-value-gaps/fair-value-gap.md), [liquidity-void](../02-liquidity/liquidity-void.md) — what Retracement enters.
- [fvg-mitigation](../18-mitigation/mitigation-of-fvg.md), [consequent-encroachment](../06-fair-value-gaps/consequent-encroachment.md) — the mechanics of the fill.
- [equilibrium-definition](../27-equilibrium/equilibrium-definition.md) — the line that separates Retracement from Reversal.

## Citations

- `ICT-2016-FVG-INTRO` — Fair Value Gap first defined as the artifact retracements target.
- `ICT-2018-IPDA` — Retracement framed as an algorithmic rebalance requirement, not discretionary pullback.
- `THAI-COMMUNITY-2026-PRICE-DELIVERY` — explicit distinction between Retracement (resumes direction) and Reversal (flips direction) inside the Price Delivery framework.
