# Breaker Block

**Category:** 08-breaker-blocks
**Aliases:** BB, breaker, broken OB
**ICT Confidence:** high
**Year Introduced:** 2017
**Year Refined:** 2026
**Source IDs:** ICT-2017-CHARTER-OVERVIEW, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-BREAKER-BLOCK
**Tags:** breaker, ob-flipped, foundational

## Definition

A **breaker block** is an order block that **failed in its original direction** — price violated the OB by closing through it with displacement — and now **flips polarity**: a failed bullish OB becomes a bearish breaker (resistance); a failed bearish OB becomes a bullish breaker (support). ICT teaches breakers as **high-conviction continuation references in the new direction** because the failure is itself an institutional signal of intent change. Breakers are the OB-side analogue of [inversion-fvg](../06-fair-value-gaps/inversion-fvg.md).

## Formal Criteria

A bullish OB → bearish breaker transformation:

- An originally bullish OB existed (last bearish candle before bullish displacement).
- Price subsequently breaks below the OB body (close below the OB low) with displacement.
- A bearish CHoCH or BOS typically accompanies the break.
- On the retest from below, the original bullish OB body now acts as **resistance** (the bearish breaker zone).

Bearish OB → bullish breaker: symmetric.

## Formula / Math

```
breaker_break_event(ob) := close_t < low(ob_body)        # for bull→bear
                            AND displacement_present_in_break

breaker_active_after_retest(ob, retest) := high(retest) reaches low(ob_body)
                                            AND rejection with displacement
                                            in opposite direction
```

## Machine-Readable

```json
{
  "id": "breaker-block",
  "category": "08-breaker-blocks",
  "aliases": ["BB", "breaker", "broken-OB"],
  "criteria": [
    {"id": "c1", "expr": "original_OB_was_violated_by_close_with_displacement == true"},
    {"id": "c2", "expr": "OB_body_now_acts_as_opposite_polarity_zone == true"},
    {"id": "c3", "expr": "retest_with_displacement_confirms_new_polarity == true"}
  ],
  "timeframes": ["M15","H1","H4","D"],
  "confidence": "high",
  "year_introduced": "2017",
  "year_refined": "2026",
  "related": ["bullish-breaker","bearish-breaker","mitigation-block","breaker-vs-mitigation","failed-breaker","bullish-order-block","bearish-order-block","inversion-fvg","pd-array-hierarchy","pd-array-stack"],
  "sources": ["ICT-2017-CHARTER-OVERVIEW","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-BREAKER-BLOCK"]
}
```

## Visual Pattern

```
   bullish OB → bearish breaker:

   Step 1: bullish OB forms (last down candle, then bullish displacement)
          ▼
          ▼  ← original OB
                ▲▲▲▲

   Step 2: later, price breaks BELOW the OB with bearish displacement
                                ▼▼▼▼
                                ▼▼▼▼ ← decisive close below OB low

   Step 3: price retraces UP to the OB body
                                       ▲▲▲
                                       ▲▲▲ ← retest reaches OB body
                                            (now bearish breaker)

   Step 4: rejection at OB body with displacement down → confirmed breaker
                                            ▼▼▼▼
```

## Timeframes

M15+. M5 breakers exist but lower conviction.

## Examples

**Example 1 — H1 bull OB → bearish breaker:**
- H1 bullish OB formed at 14:00 NY: body 1.0820–1.0830.
- 03:00 NY next day: H1 closes at 1.0815 (below 1.0820) with bearish displacement; bearish CHoCH on H4.
- Hours later: H1 retraces up to 1.0828 (inside original OB body).
- Bearish reaction with displacement → confirmed bearish breaker.
- Short on retest at MT (1.0825), SL above OB high at 1.0833 (3-pip buffer). Risk = 8 pips.

**Example 2 (2026) — worked bullish sequence, per `THAI-COMMUNITY-2026-BREAKER-BLOCK` pp. 57–60:** HTF bearish CHoCH occurs at/below equilibrium (discount zone); price sweeps sell-side liquidity (a recent Equal Low / SSL pool) before failing to make a new Lower Low and instead breaking back up through the most recent Lower High — an MSS. The failed bearish OB below that swept low flips to a bullish breaker. Of 3 candidate zones this source works through, only the ones sitting in discount/equilibrium are treated as valid breaker candidates; a structurally identical zone sitting in premium is flagged invalid by the source's own premium/discount discipline (see Common Mistakes).

## Common Mistakes

- **Wick-only break.** Wick through OB body without close-through doesn't qualify as a breaker.
- **No retest.** A break without subsequent retest is just a violated OB; the breaker action requires the retest with rejection.
- **Confusing breaker with mitigation block.** They're related but distinct — see [breaker-vs-mitigation](breaker-vs-mitigation.md). Note (2026): `THAI-COMMUNITY-2026-BREAKER-BLOCK` (p.63) observes that its Breaker Block reacts slower than its Mitigation Block, because that source's Mitigation Block gets a bonus effect from the Failure Swing that precedes it — see [breaker-vs-mitigation](breaker-vs-mitigation.md) for the full note.
- **Ignoring premium/discount placement (2026 community source, not an ICT-published gate).** `THAI-COMMUNITY-2026-BREAKER-BLOCK` treats a bullish breaker sitting deep in premium (or a bearish breaker sitting deep in discount) as a much weaker candidate — one worked example discards a structurally valid-looking zone purely because it sits on the wrong side of equilibrium. This is a conviction modifier already captured by [pd-array-hierarchy](../05-pd-arrays/pd-array-hierarchy.md)'s depth ranking, not a new qualification criterion for this file's `## Formal Criteria`.
- **Treating a plain SR Flip as an ICT breaker.** The same source distinguishes its ICT-based Breaker Block from generic "SR Flip (SRF)": a true breaker requires price to first sweep BSL/SSL before the opposing zone fails, which plain SRF does not require. See GLOSSARY.md's SRF entry.

## Related Concepts

- [bullish-breaker](bullish-breaker.md), [bearish-breaker](bearish-breaker.md) — directional variants.
- [mitigation-block](mitigation-block.md), [breaker-vs-mitigation](breaker-vs-mitigation.md), [failed-breaker](failed-breaker.md).
- [bullish-order-block](../07-order-blocks/bullish-order-block.md), [bearish-order-block](../07-order-blocks/bearish-order-block.md).
- [inversion-fvg](../06-fair-value-gaps/inversion-fvg.md) — FVG-side analogue.
- [pd-array-hierarchy](../05-pd-arrays/pd-array-hierarchy.md) — where premium/discount placement is scored as a conviction modifier.
- [pd-array-stack](../05-pd-arrays/pd-array-stack.md) — spatial retest ordering; breaker is layer 2 (nearer equilibrium than FVG/Liquidity Void, further than mitigation block).

## Citations

- `ICT-2017-CHARTER-OVERVIEW`, `ICT-2022-MENTORSHIP-OVERVIEW`.
- `THAI-COMMUNITY-2026-BREAKER-BLOCK` — worked bullish/bearish sequence examples (pp. 57–64), premium/discount conviction note, SRF distinction, reaction-speed-vs-Mitigation-Block observation (p.63).
