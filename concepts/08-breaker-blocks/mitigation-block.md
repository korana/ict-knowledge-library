# Mitigation Block

**Category:** 08-breaker-blocks
**Aliases:** MB, mitigation, hedge block
**ICT Confidence:** disputed
**Year Introduced:** 2018
**Year Refined:** 2026
**Source IDs:** ICT-2018-BLOCKS, ICT-2022-MENTORSHIP-OVERVIEW, THAI-COMMUNITY-2026-MITIGATION-BLOCK, THAI-COMMUNITY-2026-OLD-HIGH-LOW
**Tags:** mitigation-block, breaker-related, foundational, disputed

## Definition

A mitigation block is a structural reference closely related to a breaker but distinguished by **what came before**: a mitigation block forms when an OB-zone is **failed without first triggering a CHoCH/BOS in the breaker direction** — instead, it forms during a continued trend where institutions are presumed to be hedging or "mitigating" earlier positions taken at the OB. ICT's framing of mitigation blocks varies; the concept is less standardized than breakers. Often used as a continuation reference in trending markets where price returns to a prior failed-OB area without flipping bias.

> **Disputed term (2026):** a separate community source describes "Mitigation Block" quite differently — as the last opposite-color candle immediately before an MSS/CHoCH (i.e. a **reversal**-anchored reference, not a continuation one). That reading is functionally the same object as this library's [reversal-order-block](../07-order-blocks/reversal-order-block.md). See `## ICT vs Community` below for both readings side by side before applying either one.

## Formal Criteria

A mitigation block forms when:

- An OB-like zone existed.
- Price violated the OB but the structural break was a **BOS in the existing trend** (not a CHoCH).
- The OB body now serves as a **continuation reference** (same direction as before).
- Distinct from a breaker because there's no polarity flip — direction stays the same.

Operationally fuzzy; many practitioners use "mitigation block" and "breaker" interchangeably. ICT's specific 2018 framing kept them distinct via the BOS-vs-CHoCH context.

## Formula / Math

```
mitigation_block(ob) := ob was violated
                         AND structural_break_was_BOS (existing trend)
                         AND OB_acts_as_same_polarity_continuation_zone
```

## Machine-Readable

```json
{
  "id": "mitigation-block",
  "category": "08-breaker-blocks",
  "aliases": ["MB", "mitigation", "hedge-block"],
  "criteria": [
    {"id": "c1", "expr": "OB violated"},
    {"id": "c2", "expr": "break_was_BOS_not_CHoCH == true"},
    {"id": "c3", "expr": "no_polarity_flip == true"}
  ],
  "timeframes": ["M15","H1","H4","D"],
  "confidence": "disputed",
  "year_introduced": "2018",
  "year_refined": "2026",
  "related": ["breaker-block","breaker-vs-mitigation","bullish-order-block","bearish-order-block","mitigated-order-block","mitigation-definition","reversal-order-block","pd-array-stack","three-drive-pattern"],
  "sources": ["ICT-2018-BLOCKS","ICT-2022-MENTORSHIP-OVERVIEW","THAI-COMMUNITY-2026-MITIGATION-BLOCK","THAI-COMMUNITY-2026-OLD-HIGH-LOW"]
}
```

## Visual Pattern

```
   bullish mitigation block (in continuing uptrend):

   ▲▲▲ ▼ ▼ ▲▲▲▲   ← uptrend with pullback OB at ▼▼
                ▲▲▲    ← BOS continuation through the OB area
                       (no CHoCH; trend stays bullish)
                            ↓
                       price returns to OB area later
                       acts as continuation support (same polarity)
```

## Timeframes

M15+.

## Examples

**Example 1 — bullish mitigation block in trend:**
- H1 bullish OB formed at body 1.0820–1.0830 during a clean uptrend.
- Hours later H1 wicks below 1.0820 (briefly, no decisive close) on a deep pullback, then prints a strong bullish BOS to a new high.
- The OB is "violated" but trend stays bullish.
- → mitigation block. On future return to 1.0825, treat as continuation long support.
- Distinct from a breaker because there was no CHoCH-up; the trend was already up.

## Common Mistakes

- **Treating MB as a breaker.** Breaker requires polarity flip; MB doesn't.
- **Loose qualification.** Without a clear OB lineage and BOS context, MB classification is arbitrary.
- **Over-relying on MB.** They're lower-conviction than fresh OBs; some practitioners skip MBs entirely in favor of cleaner setups.
- **Discarding a failed [Three Drive](../01-market-structure/three-drive-pattern.md) attempt instead of falling back to MB.** A 2026 community source treats a Three Drive whose final leg fails to exceed the prior leg as a plain Failure Swing, not a dead setup — the next PD array to check per [pd-array-stack](../05-pd-arrays/pd-array-stack.md) is Mitigation Block, the layer nearest equilibrium.

## ICT vs Community

Two incompatible readings of "Mitigation Block" circulate, and this library does not pick a winner — read both before applying the term.

**Reading 1 — ICT-2018-BLOCKS (continuation, no polarity flip).** As defined above: an OB violated by a **BOS** in the existing trend. No CHoCH occurs; the OB keeps acting as a same-direction continuation reference. This is the original reading this file was built around, and it's the reading assumed by [breaker-vs-mitigation](breaker-vs-mitigation.md).

**Reading 2 — Thai community source, `THAI-COMMUNITY-2026-MITIGATION-BLOCK` (reversal-anchored).** This source defines Mitigation Block as **the last opposite-color candle immediately before an MSS/CHoCH**, formed after a **Failure Swing** (price fails to print a new Higher High in an uptrend, or a new Lower Low in a downtrend, then breaks structure the other way). Under this reading, Mitigation Block is a *reversal* reference — functionally the same object this library calls [reversal-order-block](../07-order-blocks/reversal-order-block.md) ("the last opposite-color candle before the reversal-direction displacement"). The source explicitly ranks it as the PD-array layer nearest equilibrium in its [pd-array-stack](../05-pd-arrays/pd-array-stack.md), ahead of Breaker Block, Liquidity Void, FVG, Order Block, Rejection Block, and Old High/Low, in that order.

The entry mechanics that come with reading 2 are this source's own, backtest-derived rules, not an ICT teaching — treat them as community technique, not formal criteria:

- If the qualifying candle's range exceeds 25 pips, the entry is the **50% midpoint** of that candle's body.
- If the candle's range is 10–15 pips or less, any price inside the candle qualifies as an entry.
- If the candle is a small-bodied type (Doji, Pinbar, Hammer, Spinning top), the author treats the **entire candle including wicks** as the zone (his "D&S" — Demand & Supply — framing; the equivalent term in RTM theory is "SRF").
- Stop-loss: beyond the swept Higher Low / Lower High, +5 pips buffer. Target: the prior swing extreme (Old Low/Old High), or a 1:3 R:R minimum.
- The author states a personal preference for this reading of Mitigation Block over Breaker Block specifically because the shallower pullback lets him set a tighter, more favorable stop-loss.

**How to use this file:** if you're working from 2018–2022-era ICT material or [breaker-vs-mitigation](breaker-vs-mitigation.md), assume reading 1 (continuation). If you're working from the 2026 community source or cross-referencing [pd-array-stack](../05-pd-arrays/pd-array-stack.md) or [reversal-order-block](../07-order-blocks/reversal-order-block.md), assume reading 2 (reversal). Do not mix the two within a single analysis.

## Related Concepts

- [breaker-block](breaker-block.md), [breaker-vs-mitigation](breaker-vs-mitigation.md), [bullish-order-block](../07-order-blocks/bullish-order-block.md), [bearish-order-block](../07-order-blocks/bearish-order-block.md), [mitigated-order-block](../07-order-blocks/mitigated-order-block.md), [mitigation-definition](../18-mitigation/mitigation-definition.md).
- [reversal-order-block](../07-order-blocks/reversal-order-block.md) — the same object as reading 2 above.
- [pd-array-stack](../05-pd-arrays/pd-array-stack.md) — where reading 2 places Mitigation Block in its retest-order layering.
- [three-drive-pattern](../01-market-structure/three-drive-pattern.md) — a failed final leg falls back to MB as the next stack layer.

## Citations

- `ICT-2018-BLOCKS`, `ICT-2022-MENTORSHIP-OVERVIEW` — reading 1 (continuation).
- `THAI-COMMUNITY-2026-MITIGATION-BLOCK` — reading 2 (reversal-anchored), pp. 24–40.
- `THAI-COMMUNITY-2026-OLD-HIGH-LOW` — failed Three Drive falls back to Mitigation Block as the next stack layer, p.258.

> Confidence is `disputed` (raised from `medium` in 2026) because two structurally incompatible definitions of "Mitigation Block" are both in circulation — see `## ICT vs Community` above.
